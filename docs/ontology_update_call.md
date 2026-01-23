# Ontology Update Parameters Guide

In order to update the ontology, we need to call the API /ontology/update, which will rollback the ontology service to an old version or create a new one.

This document describes **all supported parameters** for updating the ontology (that you should pass).

[!NOTE] There will be a file available with all the parameters for each version. In a good environment, we would be able to update the ontology without making the system go down.

**Important rules:**
- You should ONLY pass these parameters in the BODY of your request, in a json format.
- DO NOT change the keys. USE THEM as IS.
- Do NOT modify internal logic, pipelines, scripts, or database logic.
- Any parameter not provided will automatically keep its existing default value.
- In most cases, you only need to set `new_version` and `capabilities_chroma` (which are currently changing every version). Everything else can remain unchanged unless major alterations are made.

---

## Required Parameter

### `new_version` (string) **[REQUIRED]**

Defines the new ontology version identifier.

**Purpose:**
- Controls versioning for the ontology update
- Used for tagging, tracking, and deployment consistency

**Example:**
```text
new_version="KOIN-v1.1"
```

### `cap_collection_name` (string)

[!IMPORTANT] ***Most of the times we will have to be passing this for the new version. The names follow a simple pattern of `capabilities_KOIN_v1.0` or `capabilities_KOIN_v1.1`. UNLESS nothing changes, this will have to be passed as a parameter.

Capability embeddings collection name.

### `trace_id` (string)

Trace identifier used for logging and debugging. Even though there is random id generation if the value is not passed, it is an important parameter for logging purposes (`trace_id` follows the whole request throughout all the services).

If not passed, logging will proceed without a custom trace label.

---
---

## Optional Collection Parameters

These control which vector or embedding collections are used.
If not provided, the system will reuse the currently configured collections.

---

### `paths_dna_collection_name` (string, optional)

Paths DNA embeddings collection.

---

### `paths_desc_collection_name` (string, optional)

Paths description embeddings collection.

---

## Git / Version Control

### `commit_message` (string, optional)

Commit message for the ontology update. It is NICE to have it some sort of message as to why the change happened.

**Default:**

```text
"Ontology update to our newest and freshest version"
```

---

## Ontology File Parameters

### `ttl_file_name` (string, optional)

TTL ontology file name to use for the update.

If omitted, the currently configured TTL file will be reused.

---

## Database Table Parameters

These control table names for capabilities, predictions, mappings, and paths.

Only override these if you are intentionally targeting a different table.

---

### Capability Tables

* `cap_table_name` (string, optional)
  Main capabilities table

* `cap_pred_table_name` (string, optional)
  Capability prediction output table

* `cap_mapping_table_name` (string, optional)
  Capability-to-ontology mapping table

* `cap_suggestions_table_name` (string, optional)
  Capability suggestions output table

---

### Paths Tables

* `paths_table_name` (string, optional)
  Main paths table

* `paths_mapping_table_name` (string, optional)
  Paths mapping table

* `paths_suggestions_table_name` (string, optional)
  Paths suggestions output table

---

## Embedding Configuration

These should only be changed when intentionally migrating embedding models.

### `embedding_model_name` (string, optional)

Embedding model identifier.

---

### `embedding_size` (integer, optional)

Embedding vector dimensionality.

---

## Minimal Recommended Usage

For most updates, **this is all you need** when calling the API `/ontology/update`:

```json
{
    "new_version": "KOIN-v1.5",
    "cap_collection_name": "capabilities_KOIN_v1.5",
    "commit_message": "Updated ontology to our newest version, KOIN-v1.5.",
    "trace_id": "1234567890"
}
```

Everything else should remain untouched unless you explicitly know why you're changing it.

---

## Final Reminder

You are responsible ONLY for passing these parameters.

You should NOT:

* Touch database logic
* Modify ontology processing code
* Change pipeline behavior
* Alter internal defaults manually

If you need behavior changes, that is a separate engineering task — not part of the ontology update interface.
