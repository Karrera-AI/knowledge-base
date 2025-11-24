# **WORK DNA AI** 

## 1. Overview

This document explains the logic behind the **WorkDNA AI** for the Karrera App.  
It describes how the ontology was created, how capabilities are collected, cleaned, and classified, and how these outputs are used to generate a **Work DNA** for users.  

Our objective is not only to build a final capability table or a static ontology —  
it is to **use the ontology as the foundation** for extracting capabilities from a user’s Professional Identity and generating a personalized **WorkDNA profile**.  

This involves:  

- **Defining the ontology**: The WorkDNA Ontology is a structured knowledge graph of 312 capability nodes, each representing a distinct skill or competency, organized into seven major capability types.  
- **Ingesting raw capabilities**: Pulling capabilities from CSVs, resumes, or embedding databases (ChromaDB) with associated descriptions and metadata.  
- **Deduplicating capabilities**: Using both **MinHash** (text similarity) and **HDBSCAN** (semantic similarity) to merge duplicates and near-duplicates.  
- **Classifying capabilities**: Running each deduplicated capability through trained neural networks to assign the most likely WorkDNA node(s).  
- **Building the capability table**: Producing a clean, enriched table with capability names, descriptions, predicted ontology nodes, and metadata for downstream use.  
- **Generating WorkDNA profiles**: Aggregating mapped capabilities into a structured Professional Identity that aligns with the ontology and can be compared, analyzed, and recommended within the Karrera ecosystem.  

The methods described here are designed to:  
1. **Ensure data quality** by removing duplicates and inconsistencies.  
2. **Leverage AI models** for accurate capability-to-ontology mapping.  
3. **Translate raw user data** into a meaningful Professional Identity.  
4. **Support scalability** for datasets containing hundreds of thousands of capabilities.  
5. **Integrate seamlessly** with the Karrera App for user-facing recommendations, career paths, and insights.

## 2. Ontology Creation

### Purpose
The **WorkDNA Ontology** serves as the backbone of the entire capability mapping process.  
It defines a structured network of **capability nodes**, grouped into **seven major capability types**, and enriched with descriptions, relationships, and identifiers.  

This ontology is used to:
- Standardize capability definitions across datasets.
- Provide a **common language** for AI classification outputs.
- Enable structured Professional Identity generation for users.

---

### Structure
- **File format**: Turtle (`.ttl`)
- **Content**:
  - **Nodes**: 312 unique capability nodes.
    - Each node has:
      - A unique ID (e.g., `K101a01`)
      - A descriptive definition
      - A capability type (one of seven types: Ability, Activity, Attribute, Context, Knowledge, Motivation, Skill)
  - **Edges**: (Optional for current scope) Hierarchical and associative relationships between nodes.

Example (simplified):

```ttl
<#K101a01> # Information Ordering
    a schema:DefinedTerm ;
    schema:termCode "K101a01" ;
    schema:name "Information Ordering" ;
    schema:description "The ability to arrange things or actions in a certain order or pattern according to a specific rule or set of rules (e.g., patterns of numbers, letters, words, pictures, mathematical operations)." ;
    schema:bestRating "5".
```
### Loading the Ontology

The ontology is loaded into memory using the **`WorkDNAOntologyService`** class. We will discuss later the purposes of the class

#### Responsibilities of `WorkDNAProcessorService`:

- **Read and parse the `.ttl` ontology file**  
  Uses `rdflib.Graph` to load the ontology and extract node information.

- **Store ontology in a structured form**  
  Ontology nodes are stored in a Python dictionary keyed by node ID, with their descriptions and types:  

- **Provide helper methods for querying and mapping ontology data.** 
    We will also discuss these methods after

##### Data Structure Example
```python
{
  "K101a01": {
    "description": "...",
    "type": "ability"
  }
}
```
### Role in the Pipeline
The ontology is not just a static reference — it plays an active role in:

- **Mapping raw model outputs (node IDs) into meaningful descriptions.**

- **Enforcing consistency across classification and profile generation.**

- **Serving as the backbone for WorkDNA profile construction.**

## 3. Capability Table Creation & Deduplication
### 3.1: Introduction
Before the ontology can be used to generate WorkDNA profiles, we first need to **create a capability table**. The point of this capability is to extend the **WorkDNA** so that we can know to what node a certain skill points to. This creation stage is critical because raw capability data is often ***messy, redundant, and inconsistent***. Without preprocessing, mapping capabilities to ontology nodes would be unreliable and inaccurate.

The process is divided into three main components:
1. **Capability Dataset Construction** – assembling raw capabilities from source databases into a unified dataset.
2. **Embedding Creation** – generating high-dimensional vector representations of capability names and descriptions.
3. **Deduplication and Clustering** – removing redundant or near-duplicate capabilities using a hybrid approach that combines **MinHash similarity detection** and **embedding-based clustering with HDBSCAN**.

The outcome of this stage is a curated set of unique capabilities that serve as the input for ontology alignment and downstream WorkDNA profile construction.

### 3.2 Capability Dataset Creation

The raw input to our pipeline consists of large datasets of **capabilities (skills, attributes, activities, etc.)** extracted from external sources. Each capability typically has:

* **A name:** short label such as `"Python"`, `"Team Leadership"`, or `"Strategic Thinking"`
* **A description:** longer explanatory text when available, e.g., `"The ability to design and implement solutions in Python programming language.`"
* **A type:** one of the seven WorkDNA categories (`skill`, `attribute`, `context`, `knowledge`, `ability`, `motivation`, `activity`).

Because different sources may describe the same capability differently (e.g., `"Python"` vs. `"Python Programming"` vs. `"Python scripting"`), we cannot assume names are clean or unique.

The dataset creation process includes:

1. **Extracting raw capabilities using GEMINI AI** from WorkDNA Nodes and our Occupations database.
    1. **Creating a prompt for the AI to generate content**, like the example below: 
    ```python
    def generate_ability_prompt(node_name: str, node_description: str, num_examples: int, existing_capabilities: list[str], parent_nodes: list[str]) -> str:
    """
    Generates a prompt string for the Gemini-Flash 2.0 model to create new 'Ability' capabilities.

    This function constructs a detailed prompt that guides the model to generate a specified
    number of diverse, specific, and distinct abilities. It includes the work DNA node's
    name and description, specifies the desired output format (JSON), and provides a list
    of existing capabilities to avoid generating duplicates.

    Args:
        node_name (str): The name of the work_dna_node (e.g., "Problem Solving").
        node_description (str): The definition or description of the work_dna_node,
                                specifically related to an 'Ability'.
        num_examples (int): The desired number of ability examples to generate.
        existing_capabilities (list[str]): A list of previously generated ability names
                                           that the model should avoid duplicating. If
                                           empty, no exclusion clause is added.
        parent_nodes (list[str]): A list of parent node names for the current work_dna_node,
                                  ordered from immediate parent to highest ancestor.

    Returns:
        str: A formatted string representing the prompt for the Gemini-Flash 2.0 model.
    """
    existing_capabilities_str = f"Ensure these new abilities are distinct from the following: {', '.join(existing_capabilities)}." if existing_capabilities else ""

    parent_info_str = ""
    if parent_nodes:
        parent_info_str = f" This node is part of the following taxonomy hierarchy: { ' -> '.join(parent_nodes) } -> {node_name}."

    prompt = (
        f'''Given the work DNA node "{node_name}" focused on "Ability", defined as "{node_description}".
        Generate exactly {num_examples} diverse, specific, and distinct **abilities** (enduring individual attributes influencing performance) that a person might possess and apply in various occupations, directly related to and falling under the "{node_name}" node.
        {parent_info_str}

        For each ability, provide:
        1.  A concise `name` (e.g., "Critical Thinking").
        2.  A clear and specific `description` explaining what the ability entails and how it influences performance.
        3.  An `importance` score (an integer from 1 to 10), indicating how crucial this ability is for someone proficient in "{node_name}" to perform effectively (10 being very important).

        {existing_capabilities_str}

        Output the result as a JSON array of objects, where each object has "name", "description", and "importance" keys. Do NOT include any additional text or formatting outside the JSON array.
        '''
    )
    return prompt
    ```
    2. **Running the process** at least 8 times for each WorkDNA node, only once per occupation (20,000+ occupations)
    
2. **Normalizing text** (lowercasing, trimming whitespace, removing punctuation, lemmatizing when appropriate).
3. **Storing the results in a table**, with the columns: `name`, `type`, `description`, `importance` (not very relevant), `node_reference` or `occupation_reference`, like shown in the json sructure below
```json
{
  "name": "python programming",
  "description": "The capability to design and implement solutions using the Python programming language.",
  "type": "skill",
  "node_reference": "K403a10",
  "importance": 10
}
```

At the end, we would have **two big tables**: `workDNA_extension.csv` and `occupations_extension.csv`, with a total of more than 1,300,000 capabilities. This provides a unified structure for downstream processing.

### 3.3 Embedding Creation

Once the dataset is normalized, we generate **dense vector embeddings** for each capability. These embeddings are crucial for semantic comparison and clustering.
* We use a **sentence transformer model** (we first started with `all-mpnet-base-v2` but then improved to use `Qwen/Qwen3-Embedding-0.6B`, which is a state-of-the-art model with a great combination of effieciency and performance) to encode both capability names, types and descriptions into 1024-dimensional vectors.
    * First, we would **clean the description**, by removing trailing whitespaces, quote marks ("), and dots (.), and removing any unnecessary texts.
    * Second, we would get the **name, type and clean description** and use `.lower()` on all of them.
    * Third, we would encode the text like this:
    ```python
     embedding = model.encode(f'{name} ({t}): {description}', device=device)
    ```
* The embeddings are stored in a **ChromaDB vector database**, enabling fast similarity queries and clustering.

This embedding layer forms the semantic backbone of the deduplication pipeline. By comparing vector distances, we can identify capabilities that are semantically similar, even when their names differ significantly (e.g., ***“Project Coordination”*** vs ***“Managing Projects”***).

### 3.4 Deduplication Process

The deduplication process is performed in **three major stages**:

#### 3.4.1 **Selecting Unique Names and rewriting descriptions in an standardized way**
- On a first go, the descriptions were not very good -- many of them described specific aspects of the name in specific situations.
- Since some cpabilities appeared more than once in different scenarios, they had different descriptions.
- The best approach we found was to rewrite the descriptions using `gemini-flash-2.0` and having `temperature = 0` as a parameter.
- This way, we already reduced the number of capabilities from **1.3M** to **240K**.

#### 3.4.2 **MinHash-Based Similarity Clustering** 
Even with embeddings, we need to handle **textual duplicates** that differ slightly in wording. So, the first stage uses **MinHashing**, a probabilistic technique for estimating text similarity. This is especially efficient for large-scale datasets because it avoids full pairwise comparisons.
* **Shingling**: Each capability name was broken into character-level n-grams.
* **MinHash Signatures**: A compact signature was generated for each capability.
* **Similarity Estimation**: Capabilities with signatures exceeding a predefined **Jaccard similarity threshold** (default is **0.8**, but I tested with a lot of different values and liked the **0.85-0.88** range) were flagged as potential duplicates

We tested different strategies for selecting a representative:
- **Shortest string** in the cluster (e.g., "Python" instead of "Python Programming Language").
- **Most frequent variant** across the dataset, based on count (useful when integrating from multiple sources).

This step drastically reduced the candidate space, eliminating trivial duplicates while preserving semantically distinct entries. Here, we reduced **hundreds of thousands of raw entries** into a more manageable set of **unique capability names**. 

#### 3.4.3 **Embedding-Based Semantic Clustering with HDBSCAN**  
While MinHash handles near-identical strings, embeddings allow us to group **semantically related capabilities** that might not look alike textually. For example, `"software development"` and `"application engineering"` should cluster together.

* **Clustering Algorithm**: **HDBSCAN** (Hierarchical Density-Based Spatial Clustering of Applications with Noise) was applied directly to the embeddings.
    * We used **HDBSCAN** from the **CuML** library, since we were running this process on GPU to save hundreds of hours.
* **Parameters**: Key hyperparameters include `min_cluster_size` and `min_samples`, which were tuned experimentally to balance **cluster granularity** (avoiding overly broad clusters) and **noise detection** (isolating capabilities with unique meanings).
* **Semantic Grouping**: Capabilities with high embedding similarity were grouped together, even if their textual representatives diverged.
    * Again, we select a **representative capability** per cluster (using the frequency-based or medoid representative rule).
    * In more recent versions, we plan to use **AI** or a **generalization score** to define the cluster names.
Example: ***“Data Visualization”, “Creating Charts”,*** and ***“Data Presentation”*** would all be clustered together despite lexical differences.

We also ran this process a couple of times, to reduce even more the number of redundant capabilities.

This three-stage approach balances **speed and textually cleaness(via MinHash)** with **semantic precision (via embeddings + clustering)**.

### 3.5 Outputs of Deduplication = FINAL CAPABILITY TABLE
After deduplication and clustering, we build the final capability table, which serves as the input to the ontology mapping step. Each row contains:
- `name`: the representative string for the capability.
- `description`: cleaned description.
- `type`: one of the seven WorkDNA categories.
- `id`: (we used integers starting at 1) unique identifier of the representative.
- `version`: (if applicable) the version of the capability table

This table is now **clean, deduplicated, and semantically organized**, ready for integration with the **WorkDNA Ontology Service.**

### 3.6 Role in the WorkDNA Pipeline
This deduplication step is foundational for all subsequent stages:
- **Ontology Mapping**: Clean capabilities can be reliably mapped to WorkDNA nodes without duplication errors.
- **Model Training**: The reduced dataset provides higher-quality training samples for WorkDNA node classifiers.
- **Profile Building**: Deduplication ensures that user or organizational profiles are not inflated by repeated or redundant capabilities.

In short, this stage transforms messy raw data into a **structured, semantically consistent capability set**, ready to be aligned with the WorkDNA ontology.

With a deduplicated capability dataset in place, the next step is to connect these capabilities to the **WorkDNA Ontology**. This is where the `WorkDNAOntologyService` class comes into play, providing the mechanisms to load the ontology, perform fast lookups, and map capabilities into human-readable descriptions.

### Before talking about the Ontology Integration, here is the code used for the deduplication process

```python
import pandas as pd
import numpy as np
from datasketch import MinHash, MinHashLSH
from tqdm.auto import tqdm
from cuml.cluster import HDBSCAN, DBSCAN
from sklearn.metrics import pairwise_distances_argmin_min
from sklearn.preprocessing import normalize # Import normalize
import chromadb

# ----------------------------------------
# Step 1: MinHash Deduplication on Names
# ----------------------------------------

def get_minhash(text: str, num_perm: int = 128) -> MinHash:
    m = MinHash(num_perm=num_perm)
    for token in set(text.lower().split()):
        m.update(token.encode('utf8'))
    return m

def minhash_cluster(names: list[str], threshold: float = 0.8, num_perm: int = 128) -> list[list[str]]:
    """
    Cluster names by MinHash + LSH and return list of clusters (each a list of names).
    """
    lsh = MinHashLSH(threshold=threshold, num_perm=num_perm)
    minhashes = {}

    print("Indexing names with MinHash...")
    for name in tqdm(names):
        mh = get_minhash(name, num_perm)
        lsh.insert(name, mh)
        minhashes[name] = mh

    print("Querying clusters from LSH...")
    visited = set()
    clusters = []

    for name in tqdm(names):
        if name in visited:
            continue
        cluster = lsh.query(minhashes[name])
        clusters.append(cluster)
        visited.update(cluster)

    return clusters

def get_cluster_representatives(clusters: list[list[str]], name_counts: pd.Series) -> dict[str, str]:
    """
    Pick a representative name per cluster.
    The representative is chosen based on the highest count,
    or the shortest string if counts are equal or not available.
    Returns map: name -> cluster_rep_name
    """
    rep_map = {}
    for cluster in clusters:
        # Get counts for names in the current cluster
        cluster_counts = name_counts.reindex(cluster, fill_value=0)
        
        # Find the name with the maximum count
        # If there's a tie, min() will pick the one that comes first alphabetically,
        # but we want to break ties by shortest length. So we'll find max count first.
        max_count = cluster_counts.max()
        
        # Get all names with the maximum count
        candidates = cluster_counts[cluster_counts == max_count].index.tolist()
        
        # From the candidates, pick the one with the shortest length
        rep = min(candidates, key=len)

        for name in cluster:
            rep_map[name] = rep
    return rep_map


# ----------------------------------------
# Step 2: Load Embeddings and IDs from ChromaDB
# ----------------------------------------

# def load_all_embeddings(chroma_collection_names: list[str]) -> pd.DataFrame:
    # """
    # Fetch all embeddings + ids + names from multiple ChromaDB collections, combine into one DataFrame.
    # Returns DataFrame with columns: id, name, embedding (np.array)
    # """
    # chroma_client = chromadb.HttpClient(host = '34.71.102.215', port = 8000)
    # all_data = []

    # for collection_name in chroma_collection_names:
    #     collection = chroma_client.get_collection(collection_name)
    #     results = collection.get(include=["embeddings", 'metadatas'])
    #     # ids = unique IDs in collection
    #     # embeddings = list of vectors
    #     ids = results["ids"]
    #     embeddings = results["embeddings"]
    #     metadatas = results['metadatas']

    #     df = pd.DataFrame({"id": ids})
    #     df["embedding"] = [e for e in embeddings]
    #     df['name'] = [meta['name'] for meta in metadatas]
    #     all_data.append(df)

    # full_df = pd.concat(all_data, ignore_index=True)
    # # Remove duplicate names keeping first appearance
    # full_df = full_df.drop_duplicates(subset="id").reset_index(drop=True)
    # return full_df
def load_all_embeddings(name_df: pd.DataFrame, chroma_collection_names: list[str]) -> pd.DataFrame:
    """
    Fetch all embeddings + ids + names from multiple ChromaDB collections, combine into one DataFrame.
    
    Args:
        name_df: DataFrame containing 'id' and 'name' columns to match with embeddings
        chroma_collection_names: List of ChromaDB collection names to fetch embeddings from
        
    Returns:
        DataFrame with columns: id, name, embedding (np.array)
    """
    chroma_client = chromadb.HttpClient(host='34.71.102.215', port=8000)
    
    # Create a dictionary to store embeddings by ID for faster lookup
    embeddings_dict = {}
    
    for collection_name in chroma_collection_names:
        try:
            collection = chroma_client.get_collection(collection_name)
            results = collection.get(include=["embeddings"])
            
            # Store each id and its corresponding embedding in the dictionary
            # for id_, embedding in zip(results["ids"], results["embeddings"]):
            for id_, embedding in zip(results["ids"], normalize(results["embeddings"], norm = 'l2')):
                embeddings_dict[id_] = np.array(embedding)
                
        except Exception as e:
            print(f"Error loading collection {collection_name}: {str(e)}")
            continue
    
    # Create a new DataFrame with the same rows as name_df
    full_df = name_df.copy()
    
    # Add embeddings to the DataFrame
    full_df['embedding'] = full_df['id'].map(embeddings_dict)
    
    # Drop rows where no embedding was found (if desired)
    full_df = full_df.dropna(subset=['embedding'])
    
    return full_df

# ----------------------------------------
# Step 3: Filter Embeddings to MinHash Cluster Representatives
# ----------------------------------------

def filter_to_representatives(full_df: pd.DataFrame, rep_map: dict[str, str]) -> pd.DataFrame:
    """
    Filter full_df rows to only those whose name is a cluster representative.
    """
    reps = set(rep_map.values())
    filtered = full_df[full_df["name"].isin(reps)].reset_index(drop=True)
    return filtered

# ----------------------------------------
# Step 4: HDBSCAN Clustering on Embeddings
# ----------------------------------------

def hdbscan_cluster_embeddings(embeddings: np.ndarray, min_cluster_size: int = 5, min_samples: int = None,
                              epsilon_value: float = 0.0) -> np.ndarray:
    """
    Run cuML HDBSCAN clustering on embeddings array.
    """
    clusterer = HDBSCAN(min_cluster_size=min_cluster_size, 
                        min_samples=min_samples, 
                        cluster_selection_epsilon = epsilon_value,
                        metric = 'euclidean',
                        verbose = 3
                       )
    labels = clusterer.fit_predict(embeddings)
    return labels

def dbscan_cluster_embeddings(embeddings: np.ndarray, min_cluster_size: int = 5, min_samples: int = None,
                              epsilon_value: float = 0.0) -> np.ndarray:
    """
    Run cuML HDBSCAN clustering on embeddings array.
    """
    clusterer = DBSCAN(
                        # min_cluster_size=min_cluster_size, 
                        min_samples=min_samples, 
                        eps = epsilon_value,
                        metric = 'cosine',
                        verbose = 3
                       )
    labels = clusterer.fit_predict(embeddings)
    return labels

# ----------------------------------------
# Step 5: Assign Medoid as Cluster Representative ID
# ----------------------------------------

def assign_medoid_representative(embeddings: np.ndarray, labels: np.ndarray, ids: list[str]) -> dict[int, str]:
    """
    For each cluster, find medoid (closest embedding to cluster centroid).
    Returns dict: cluster_label -> medoid_id
    """
    cluster_medoid = {}
    for cluster_label in set(labels):
        if cluster_label == -1:
            # Noise cluster: no medoid
            continue
        cluster_indices = np.where(labels == cluster_label)[0]
        cluster_embeds = embeddings[cluster_indices]

        # Compute centroid
        centroid = cluster_embeds.mean(axis=0).reshape(1, -1)

        # Find closest embedding to centroid (medoid)
        medoid_idx, _ = pairwise_distances_argmin_min(centroid, cluster_embeds)
        medoid_id = ids[cluster_indices[medoid_idx[0]]]
        cluster_medoid[cluster_label] = medoid_id
    return cluster_medoid

def assign_count_based_representative(rep_df: pd.DataFrame, cluster_labels: np.ndarray) -> dict[int, str]:
    """
    For each cluster, find the representative with the highest count.
    If 'count' column is not available, falls back to medoid logic.
    Returns dict: cluster_label -> count_based_rep_id
    """
    cluster_rep_ids = {}
    if "count" not in rep_df.columns:
        print("Warning: 'count' column not found in representative DataFrame. Falling back to medoid-based representatives.")
        embeddings_array = np.vstack(rep_df["embedding"].values).astype(np.float32)
        return assign_medoid_representative(embeddings_array, cluster_labels, rep_df["id"].tolist())

    for cluster_label in set(cluster_labels):
        if cluster_label == -1:
            continue
        
        cluster_rows = rep_df[cluster_labels == cluster_label]
        
        # Find the row with the maximum count
        # In case of a tie, `idxmax` will return the first occurrence, which is fine
        max_count_row = cluster_rows.loc[cluster_rows["count"].idxmax()]
        
        cluster_rep_ids[cluster_label] = max_count_row["id"]
        
    return cluster_rep_ids


# ----------------------------------------
# Step 6: Build Final DataFrame with cluster_id and cluster_rep_id per original id
# ----------------------------------------

def build_final_mapping(
    full_df: pd.DataFrame,
    rep_df: pd.DataFrame,
    rep_map: dict[str, str],
    cluster_labels: np.ndarray,
    use_count_rep: bool = False
) -> pd.DataFrame:
    """
    Assign cluster_id and cluster_rep_id for all original ids.

    Args:
        full_df: DataFrame with all original ids, names, embeddings, and optionally a 'count' column.
        rep_df: DataFrame with representatives only, their embeddings and cluster labels.
        rep_map: map original name -> representative name (string)
        cluster_labels: HDBSCAN cluster labels for rep_df rows.
        use_count_rep: If True, uses the highest-count item as cluster representative.
                       Otherwise, uses the medoid.

    Returns:
        DataFrame with columns: id, name, cluster_id, cluster_rep_id, count (if present in input)
    """
    rep_df = rep_df.copy()
    rep_df["cluster_id"] = cluster_labels

    # Choose representative assignment method
    if use_count_rep and "count" in rep_df.columns:
        print("Assigning cluster representatives based on highest count...")
        cluster_rep_map = assign_count_based_representative(rep_df, cluster_labels)
    else:
        print("Assigning cluster representatives based on medoid (closest to centroid)...")
        embeddings_array = np.vstack(rep_df["embedding"].tolist())
        cluster_rep_map = assign_medoid_representative(embeddings_array, cluster_labels, rep_df["id"].tolist())

    # Map representative name to ID
    rep_name_to_id = dict(zip(rep_df["name"], rep_df["id"]))

    rows = []
    noise_count = 0
    total = len(full_df)
    total_count = 0

    for _, row in full_df.iterrows():
        name = row["name"]
        orig_id = row["id"]
        count = row.get("count", 1)  # Default to 1 if no count column
        total_count += count

        rep_name = rep_map.get(name, name)
        rep_id = rep_name_to_id.get(rep_name)

        cluster_id = None
        if rep_id:
            rep_cluster_idx = rep_df.index[rep_df["id"] == rep_id]
            if len(rep_cluster_idx) == 1:
                cluster_id = rep_df.loc[rep_cluster_idx[0], "cluster_id"]

        if cluster_id == -1:
            cluster_rep_id = rep_id
            noise_count += 1
        else:
            cluster_rep_id = cluster_rep_map.get(cluster_id, rep_id)

        row_data = {
            "id": orig_id,
            "name": name,
            "cluster_id": cluster_id,
            "cluster_rep_id": cluster_rep_id,
        }
        if "count" in full_df.columns:
            row_data["count"] = count

        rows.append(row_data)

    result_df = pd.DataFrame(rows)

    # Log cluster summary
    num_clusters = len(set(cluster_labels)) - (1 if -1 in cluster_labels else 0)
    print(f"✅ Mapping complete: {total} rows, {total_count} total count")
    print(f"📦 {num_clusters} clusters formed")
    print(f"🌪️ {noise_count} items marked as noise (singleton clusters)")

    # Optional: Summary of total count per cluster rep
    if "count" in result_df.columns:
        cluster_summary = (
            result_df.groupby("cluster_rep_id")["count"]
            .sum()
            .sort_values(ascending=False)
        )
        print("\n🔢 Top cluster representatives by total count:")
        print(cluster_summary.head(10))

    return result_df


# ----------------------------------------
# Main pipeline function
# ----------------------------------------

def full_deduplication_pipeline(
    all_names: list[str],
    full_df: pd.DataFrame,
    minhash_threshold: float = 0.8,
    num_perm: int = 128,
    hdbscan_min_cluster_size: int = 5,
    hdbscan_min_samples: int = None,
    epsilon_value:float = 0.0,
    use_count_rep: bool = False
) -> pd.DataFrame:
    """
    Run full deduplication pipeline:
    1. MinHash deduplication on names
    2. Load embeddings and IDs from ChromaDB collections -- this wil be done before
    3. Filter embeddings to MinHash cluster representatives
    4. Run HDBSCAN on embeddings of representatives
    5. Assign medoid representatives per cluster
    6. Map all original ids to cluster_id and cluster_rep_id

    Returns:
        DataFrame with columns: id, name, cluster_id, cluster_rep_id
    """

    print("Running MinHash deduplication on names...")
    # Get a Series of counts for MinHash clustering representative selection
    if "count" in full_df.columns:
        name_counts = full_df.groupby("name")["count"].sum()
    else:
        name_counts = pd.Series(1, index=full_df["name"].unique())

    clusters = minhash_cluster(all_names, threshold=minhash_threshold, num_perm=num_perm)
    rep_map = get_cluster_representatives(clusters, name_counts)


    print(f"Filtering embeddings to {len(set(rep_map.values()))} cluster representatives...")
    rep_df = filter_to_representatives(full_df, rep_map)

    print("Running HDBSCAN on representative embeddings...")
    embeddings_array = np.vstack(rep_df["embedding"].values).astype(np.float32)
    cluster_labels = hdbscan_cluster_embeddings(
        embeddings_array, 
        min_cluster_size=hdbscan_min_cluster_size, 
        min_samples=hdbscan_min_samples, 
        epsilon_value = epsilon_value
    )
    # cluster_labels = dbscan_cluster_embeddings(
    #     embeddings_array, 
    #     min_cluster_size=hdbscan_min_cluster_size, 
    #     min_samples=hdbscan_min_samples, 
    #     epsilon_value = epsilon_value
    # )

    print("Building final mapping of all IDs to cluster IDs and representative IDs...")
    final_df = build_final_mapping(full_df, rep_df, rep_map, cluster_labels, use_count_rep=use_count_rep)

    return final_df
    
def deduplication_pipeline_testing(
    all_names: list[str],
    full_df: pd.DataFrame,
    rep_map,
    hdbscan_min_cluster_size: int = 5,
    hdbscan_min_samples: int = None,
) -> pd.DataFrame:
    """
    Run full deduplication pipeline:
    1. MinHash deduplication on names
    2. Load embeddings and IDs from ChromaDB collections -- this wil be done before
    3. Filter embeddings to MinHash cluster representatives
    4. Run HDBSCAN on embeddings of representatives
    5. Assign medoid representatives per cluster
    6. Map all original ids to cluster_id and cluster_rep_id

    Returns:
        DataFrame with columns: id, name, cluster_id, cluster_rep_id
    """
    print(f"Filtering embeddings to {len(set(rep_map.values()))} cluster representatives...")
    rep_df = filter_to_representatives(full_df, rep_map)

    print("Running HDBSCAN on representative embeddings...")
    embeddings_array = np.vstack(rep_df["embedding"].values).astype(np.float32)
    cluster_labels = hdbscan_cluster_embeddings(
        embeddings_array, min_cluster_size=hdbscan_min_cluster_size, min_samples=hdbscan_min_samples
    )

    print("Building final mapping of all IDs to cluster IDs and representative IDs...")
    final_df = build_final_mapping(full_df, rep_df, rep_map, cluster_labels)

    return final_df
```
---
## 4. WorkDNA Ontology Service
The **WorkDNA Ontology Service** is the core component that bridges the structured ontology with the cleaned and deduplicated capability dataset. After the capability table has been created, embedded, and clustered into unique entries (Step 1–3), the service provides functionality to load, interpret, and query the WorkDNA ontology in a systematic way. This enables mapping real-world capabilities to the WorkDNA ontology structure, ensuring semantic consistency and interoperability across applications.

### 4.1 Structure of the Ontology

At its core, our WorkDNA ontology defines a taxonomy of professional identity, organized into seven primary node types:

Skill – practical competencies (e.g., Python programming, financial modeling).

Knowledge – theoretical or domain-specific expertise (e.g., statistics, constitutional law).

Attribute – inherent traits or characteristics (e.g., adaptability, critical thinking).

Ability – broader capacities that enable action (e.g., problem-solving, systems thinking).

Motivation – drivers of behavior and preferences (e.g., curiosity, achievement orientation).

Context – environments or conditions where capabilities are applied (e.g., startup setting, regulated industries).

Activity – concrete tasks or roles performed (e.g., debugging code, conducting interviews).

Each node is defined not only by its label but also by its relationships to other nodes, making the ontology a connected structure rather than a flat hierarchy.

### 4.1 Purpose

The service is designed to:
- Load the WorkDNA ontology from a **Turtle (TTL)** file, which encodes hierarchical relationships among nodes.
- Represent the ontology as a navigable structure, where each node corresponds to a defined WorkDNA category (e.g., Skill, Attribute, Ability).
- Support capability-to-ontology matching, allowing new or external capabilities to be classified under one of the predefined WorkDNA nodes.
- Provide querying and inspection tools for analyzing ontology nodes, relationships, and matched capabilities.

This abstraction makes it possible to align raw, unstructured capability data with the formal WorkDNA taxonomy.