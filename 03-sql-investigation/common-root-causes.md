# Common Root Causes in SQL Investigations
## What patterns explain recurring issues?

This guide helps identify **repeatable failure patterns** behind SQL-related support incidents. Instead of treating each query issue as unique, this framework focuses on the *underlying system behavior that keeps breaking the same way*.


## 1. Data Pipeline Misalignment

### Pattern
Data arrives correctly in one system but is **shifted, delayed, or transformed incorrectly** in downstream tables.

### What it looks like
- Missing rows in reporting tables but present in raw tables
- Unexpected nulls after ETL runs
- “Why does staging match but warehouse doesn’t?”

### Common causes
- Broken or partial ETL job runs
- Schema changes not propagated downstream
- Overwritten partitions or late-arriving data not handled


## 2. Key Mismatch Across Systems

### Pattern
Records exist in multiple systems but **cannot be reliably joined**.

### What it looks like
- Join returns fewer rows than expected
- Duplicate or orphaned records
- Inconsistent user/order identifiers

### Common causes
- Different ID systems (UUID vs internal integer IDs)
- Missing mapping tables or stale reference data
- Silent type mismatches (string vs int joins)


## 3. Time Window Drift

### Pattern
Data is correct, but **the time boundaries used in queries are wrong or inconsistent**.

### What it looks like
- Reports differ by date range even when logic seems identical
- “Yesterday’s data is missing”
- Partial daily aggregates

### Common causes
- Timezone mismatches (UTC vs local)
- Off-by-one date filters (`<` vs `<=`)
- Delayed ingestion vs query cutoff mismatch


## 4. Schema Evolution Breakage

### Pattern
Upstream schema changes silently break downstream assumptions.

### What it looks like
- Suddenly null columns
- Query errors after deployment
- Aggregations returning incorrect results

### Common causes
- Renamed or dropped columns not reflected in queries
- New nullable fields introduced without safeguards
- Backwards-incompatible type changes


## 5. Duplicate or Replayed Data

### Pattern
The same logical record appears multiple times due to ingestion or retry behavior.

### What it looks like
- Inflated counts
- Duplicate users/orders/events
- Non-idempotent pipeline behavior

### Common causes
- Retry logic without deduplication keys
- Event reprocessing after partial failures
- Missing uniqueness constraints


## 6. Partial or Failed Loads

### Pattern
Data pipelines succeed partially but fail silently or inconsistently.

### What it looks like
- Missing recent records only
- Inconsistent row counts across partitions
- “Yesterday is fine, today is broken”

### Common causes
- Job timeout mid-run
- Partition-level failure not surfaced
- Dependency job not completing


## 7. Business Logic Drift

### Pattern
SQL is correct syntactically but no longer matches **current business definitions**.

### What it looks like
- Metrics disagree with dashboards
- Confusion over definitions like “active user” or “revenue”
- Stakeholders disputing correctness despite identical queries

### Common causes
- Metric definitions updated in documentation but not queries
- Multiple competing definitions across teams
- Hardcoded filters that no longer match policy


## 8. Hidden Data Quality Issues

### Pattern
Data exists, but is **unreliable or malformed in subtle ways**.

### What it looks like
- Aggregations seem “slightly off”
- Sporadic null spikes
- Hard-to-reproduce inconsistencies

### Common causes
- Upstream validation missing
- Dirty source data (manual entry, integrations)
- Encoding, formatting, or casing inconsistencies


## How to Use This Guide

When debugging SQL issues, don’t jump straight into query fixes.

Instead:
1. Identify *which pattern this resembles*
2. Validate upstream assumptions first
3. Check joins, time filters, and ingestion behavior before rewriting logic
4. Confirm whether this is a **data issue or a definition issue**

Most recurring SQL incidents are not query problems — they are **system consistency problems revealed through SQL**.