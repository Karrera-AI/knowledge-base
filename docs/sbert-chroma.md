# **SENTENCE EMBEDDINGS & CHROMADB**

## 1. **OVERVIEW**
This document walks through how we generate sentence embeddings using Sentence-BERT (or any modern embedding model), how we store them in ChromaDB, and how we query them efficiently. Embeddings give us a vector representation of text, making it possible to compute semantic similarity, cluster concepts, and perform large‑scale retrieval.

Right now, we have been using SBERT to capture the semantic meaning of:
* ***Capabilities***
* ***Paths Descriptions***

And we use a normal embeddings for the:
* ***Paths WORKDNAs***

### **High‑Level Flow** (for a SBERT embedding)
```
           Text / Sentence
                  |
                  v
        Sentence Transformer Model
                  |
                  v
           1024‑dim Embedding
                  |
                  v
+----------------------------------------------------+
|                    ChromaDB                        |
|                                                    |
|   Stores: ids | embedding vectors | metadata       |
+----------------------------------------------------+
                  ^
                  |
        Query Embedding (same model)
```
---

## 2. **SENTENCE TRANSFORMERS: THE EMBEDDING ENGINE**
We use the `sentence-transformers` library:

```bash
pip install sentence-transformers
```

### **Choosing a Model**
Right now, we use **Qwen3-Embedding-0.6B**, which performs extremely well on:
- Semantic Textual Similarity (STS)
- Clustering tasks
- General retrieval performance

The model outputs **1024‑dimensional vectors**. We currently use it at full size for maximum quality, but smaller variants exist if we need lighter inference. We are still testing which one will have the best combination of performance and accuracy.

### **Example Usage**
```python
from sentence_transformers import SentenceTransformer
model = SentenceTransformer("Qwen/Qwen3-Embedding-0.6B")  # Example, adjust as needed

text = "This is a sentence about embeddings."
vector = model.encode(text).tolist()  # 1024 dims
```
### **ENCODING LOGIC FOR EACH TYPE**
To maintain consistency and reliable clustering, every text type follows strict encoding rules before generating embeddings. Everything is normalized to **lowercase**, stripped of any whitespaces or extra unnecessary characters in front or back.

#### **1. Capabilities**
We encode capabilities using:
```
"name (type): description"
```
- All lowercase.
- Example:
  ```
  python (skill): programming using the python language.
  ```
- If the capability **does not have one of the 7 WorkDNA types** ***(attribute, ability, work activity, work context, knowledge, motivation, or skill)***, we simply omit the type and encode:
  ```
  "name: description"
  ```
  - PS: We are trying to create a method to use an model to assign a type based on the name and description.

- If a capability **lacks a description**, we generate one automatically using our AI system (details in WorkDNA Ontology section of the broader documentation).

#### **2. Path Descriptions (Occupations)**
We encode **only the occupation description**, all in lowercase.
- These descriptions always begin with the occupation name + a verb:
  - Example:
    ```
    software engineers design, develop, and maintain software systems...
    ```
- If an occupation has **no description**, we generate one automatically.

---

## 3. **CHROMADB SETUP**
We interact with ChromaDB via **HTTP client**.

We use the `chromadb` library:

```bash
pip install chromadb
```


### **Client Creation**
All configuration values (hosts, ports, authentication, collection names) are stored securely in `.env` files and cloud secrets.

```python
from chromadb import HttpClient

client = HttpClient(
    host=CHROMA_HOST,
    port=CHROMA_PORT,
)
```

### **Collections**
A collection defines how vectors are indexed.

We configure **HNSW** with **cosine similarity**, because cosine is the metric used for semantic similarity between SBERTs.

We also configure `ef_construction`, which determines the size of the candidate list used to select neighbors during index creation. A higher value improves index quality at the cost of more memory and time, while a lower value speeds up construction with reduced accuracy. The default value is `100`, but we should analyze it based on the potential size of the collection.

```python
collection = client.create_collection(
    name="capabilities_embeddings",
    configuration={
        "hnsw": {
            "space": "cosine",   # critical for semantic similarity
            "ef_construction": 900 
        }
    }
)
```

---

## 4. **ADDING DATA: EMBEDDINGS, METADATA & IDS**
ChromaDB stores:
- **ids** (strings)
- **embeddings** (lists of floats)
- **metadata** (dictionaries)

### **ID Strategy Used in Our System**
- **Capabilities in DB** → use their **unique table id**
- **Capabilities for clustering** → use the format: `name (type)`
- **Paths** → use the id from the table

### **Single Insert Example**
```python
collection.add(
    ids=["123"],
    embeddings=[vector],
    metadatas=[{"name": "Python",
                "type": "skill",
                "description": "...",
                "taxonomy_id": "KOIN-v1.0" # Essential for when we use query.
                }]
)
```

### **Batching Rules**
Chroma’s max recommended batch size:
```
5000 for add()
5000 for get()
```

### **Batch Insert Example**
```python
BATCH_SIZE = 5000

for i in range(0, len(vectors), BATCH_SIZE):
    batch_vecs = vectors[i:i+BATCH_SIZE]
    batch_ids = ids[i:i+BATCH_SIZE]
    batch_meta = metadata[i:i+BATCH_SIZE]

    collection.add(
        ids=batch_ids,
        embeddings=batch_vecs,
        metadatas=batch_meta
    )
```

---

## 5. **MOVING COLLECTIONS BETWEEN DATABASES**
We sometimes migrate collections between environments (local → staging → production).

Below is the full migration logic, with batching and metadata preservation.

```python
# assume you are moving from One environment to another:
old_client = ... # Either HTTPClient, PersistentClient, etc
new_client = ... # Either HTTPClient, PersistentClient, etc
list_of_collections = [...] # LIST of COLLECTIONS you want to move from one environment to another;

# for every collection in the list of collections, move it from one environment to the other.
for collection_name in list_of_collections:
    print("Getting the old collection")
    old_collection = old_client.get_collection(name=collection_name)

    print(f"Getting or Creating new collection: {collection_name}")
    new_collection = new_client.get_or_create_collection(
        name=collection_name,
        configuration={"hnsw": {
            "space": "cosine",
            "ef_construction": 900,
        }}
    )

    BATCH_SIZE = 5000
    total_items = old_collection.count()
    migrated_count = 0

    if total_items == 0:
        print("Old collection empty. No migration.")
    else:
        print(f"Migrating {total_items} items in batches of {BATCH_SIZE}...")

        for i in range(0, total_items, BATCH_SIZE):
            batch_start = i
            batch_end = min(i + BATCH_SIZE, total_items)
            print(f"Batch {batch_start} → {batch_end}")

            batch_data = old_collection.get(
                offset=batch_start,
                limit=BATCH_SIZE,
                include=["embeddings", "metadatas"]
            )

            new_collection.add(
                ids=batch_data["ids"],
                embeddings=batch_data["embeddings"],
                metadatas=batch_data["metadatas"]
            )

            migrated_count = batch_end
            print(f"Migrated: {migrated_count}")

        print(f"✔ Migration complete for {collection_name}")
```

---

## 6. **UPDATING EXISTING COLLECTION DATA**
Updating data in ChromaDB is essentially a re‑insert with the same id. We cannot change the id value, so if we want to change the id, we have to delete it and then add again.

### **Updating Embeddings**
```python
collection.update(
    ids=["123"],
    embeddings=[new_vector]
)
```

### **Updating Metadata**
```python
collection.update(
    ids=["123"],
    metadatas=[{"name": "Python Scripting"}]
)
```

### **Updating Everything Together**
```python
collection.update(
    ids=["123"],
    embeddings=[new_vector],
    metadatas=[{"taxonomy_id": "KOIN-v1.1"}]
)
```

### **UPSERT**
If we are trying to do a big update in our collection, and potentially add new elements, we can use Chroma's `upsert` method, which updates existing items, or adds them if they don't yet exist. If the  `ids` don't exist yet, the `upsert` method will work like an `add`.

---

## **SUMMARY**
This guide covers the entire lifecycle:
1. Create embeddings with Sentence Transformers
2. Choose high‑quality models (currently Qwen3‑Embedding‑0.6B)
3. Configure ChromaDB with cosine‑based HNSW
4. Insert, batch process, and manage ids + metadata
5. Migrate collections safely between environments
6. Update embeddings and metadata when needed

The system gives us a scalable, fast semantic search and clustering pipeline across hundreds of thousands of capabilities, paths, and other text entities.

