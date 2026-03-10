# Company Matching Service

## Overview

The company matching service provides fuzzy matching for company names in the database using PostgreSQL's `pg_trgm` trigram extension. It enables fast, efficient similarity-based searches across large datasets (10M+ rows) with optional filtering by industry.

## Architecture

### Database Index

The service relies on a **GIN (Generalized Inverted Index)** trigram index on the company name column:

```sql
CREATE INDEX idx_company_name_gin ON organizations USING GIN (name gin_trgm_ops);
```

- **GIN** provides fast candidate filtering via the `<%` operator
- All filtering and scoring happens in PostgreSQL—no candidates are loaded into Python memory
- Scales efficiently to millions of rows

### Query Strategy

For a query like "Google", the service:

1. **Normalizes** the input (strips leading/trailing whitespace)
2. **Filters** candidates using `%s <% name` (GIN index seek)
3. **Scores** remaining rows with `word_similarity(%s, name)` (asymmetric: query tokens inside stored name)
4. **Orders** by similarity descending and returns top results

Example SQL:
```sql
SELECT organization_id, name, industry, country, website,
       ROUND((word_similarity('google', name) * 100)::numeric, 2) AS similarity_score
FROM organizations
WHERE 'google' <% name
ORDER BY similarity_score DESC
LIMIT 20;
```

> **Things to consider:** Maybe the word_similarity() is not the best fit. Maybe we have to change to strictr_word_similarity().

## Key Concepts

### `word_similarity()` vs `similarity()`

- **`word_similarity(query, name)`**: Asymmetric. Checks if query tokens appear as a contiguous unit within the stored name.
  - `word_similarity("google", "google llc")` → ~1.0 (full match)

- **`similarity(query, name)`**: Symmetric. Compares trigram sets of both strings.
  - `similarity("google", "google llc")` → ~0.53 (penalized by length difference)

For company matching, `word_similarity` is more intuitive — abbreviated or shortened queries match their full stored versions.

### The `<%` Operator

The `<%` operator (word similarity distance) triggers **GIN index candidate filtering**. It's fast but doesn't enforce a threshold—it relies on the session `pg_trgm.word_similarity_threshold` (default 0.6).

Since we cannot control the threshold per-query with GIN, we score all candidates with `word_similarity()` and let the application layer sort by relevance.

## API Endpoint

### POST `/match_companies`

Matches companies by name with optional industry filtering.

**Request body:**
```json
{
  "name": "Google",
  "industry": "Technology",
  "limit": 20,
  "trace_id": "optional-trace-id"
}
```

- `name` (required): Company name to search for
- `industry` (optional): Filter results by industry
- `limit` (optional, default 20): Maximum number of results to return
- `trace_id` (optional): Trace ID for logging correlation

**Response:**
```json
{
  "success": true,
  "message": "Found 3 matching companies for 'Google'",
  "matches": [
    {
      "organization_id": 12345,
      "name": "Google LLC",
      "industry": "Technology",
      "country": "USA",
      "website": "google.com",
      "similarity_score": 98.5
    },
    {
      "organization_id": 12346,
      "name": "Google Canada",
      "industry": "Technology",
      "country": "Canada",
      "website": "google.ca",
      "similarity_score": 95.2
    },
    {
      "organization_id": 12347,
      "name": "Google Germany",
      "industry": "Technology",
      "country": "Germany",
      "website": "google.de",
      "similarity_score": 92.8
    }
  ],
  "total_matches": 3,
  "query": {
    "name": "Google",
    "industry": "Technology",
    "limit": 20
  }
}
```

## Implementation Details

### CompanyMatcher Class

Located in `src/companyMatcher.py`, the `CompanyMatcher` class handles all matching logic:

```python
matcher = CompanyMatcher(postgres_conn_info, company_table_name="organizations")
results = matcher.match_companies(
    name="Google",
    industry="Technology",
    min_similarity=50,
    limit=20
)
```

**Methods:**

- `match_companies(name, industry=None, min_similarity=50, limit=20)` — Main matching method
  - Returns list of dicts with matching companies ordered by similarity

- `get_company_count()` — Get total number of companies in the database

- `_normalize_company_name(name)` — Static helper for name normalization
  - Strips legal suffixes (Inc, LLC, Corp, GmbH, etc.)
  - Normalizes '&' to 'and'
  - Removes punctuation
  - Collapses whitespace

### API Integration

The endpoint is defined in `src/APIs.py`:

- Initializes `CompanyMatcher` on service startup
- Validates database connectivity during initialization
- Returns 503 if matcher service is unavailable
- Logs all matches with trace/span IDs for observability
- Handles errors gracefully with proper HTTP status codes

## Performance Notes

- **Index creation**: One-time operation, typically <30 seconds for 10M rows
- **Query latency**: Usually <100ms for "top-20" queries on large tables
- **Memory usage**: Minimal—all filtering happens in PostgreSQL
- **Industry filtering**: Applied in database (reduces candidate set before scoring)

## Future Optimization: GiST Index

If you need **top-K results without a minimum threshold** (e.g., "give me the 5 most similar regardless of score"), consider adding a **GiST index**:

```sql
CREATE INDEX idx_company_name_gist ON organizations USING GIST (name gist_trgm_ops);
```

Then refactor the query to use the KNN operator `<<->`:
```sql
SELECT ... FROM organizations
ORDER BY name <<-> 'google'
LIMIT 5;
```

**Benefits of GiST + KNN:**
- PostgreSQL stops scanning the index once it has K results
- No need to score all candidates
- Better for arbitrary top-K (no threshold needed)

**Trade-offs:**
- Slightly larger index size than GIN
- Requires building a separate index (can coexist with GIN)
- Good when you always want top-K sorted by distance

## Troubleshooting

### No results returned but companies exist

**Cause:** The `<%` operator filtering is too strict with default threshold.
**Solution:** Manually verify with:
```sql
SELECT name, word_similarity('query', name) FROM organizations ORDER BY 2 DESC LIMIT 5;
```

### Service initialization fails

**Cause:** Database connection string invalid or `organizations` table doesn't exist.
**Solution:** Check logs for `"CompanyMatcher initialization failed"` and verify:
- PostgreSQL connection string is correct
- Table name is `organizations` (or update `PG_COMPANY_TABLE_NAME` in `APIs.py`)
- GIN index exists on the `name` column

### Slow queries on large tables

**Cause:** GIN index not created or query planner choosing sequential scan.
**Solution:**
1. Verify index exists: `\d organizations` in psql
2. Disable sequential scan for testing: `SET enable_seqscan = OFF;`
3. Update query stats: `ANALYZE organizations;`
