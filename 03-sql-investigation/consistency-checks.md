# Consistency Checks

Use this file when verifying whether data is consistent across multiple systems such as API responses, database records, UI output, or downstream services.

This is used when data exists but does not match between sources.

---

## Purpose

Many support issues are not caused by missing data, but by mismatches between systems.

This checklist helps determine:

- where inconsistencies originate
- which system is out of sync
- whether the issue is delay, transformation, or failure
- what system should be treated as source of truth

---

## 1. Cross-System Comparison

Compare the same entity across systems.

### Check:
- API response vs database state
- UI display vs backend values
- source system vs replicated system
- event source vs processed output

---

## 2. State Mismatch Detection

Identify differences in expected state.

### Common patterns:
- API shows success but DB not updated
- DB updated but API still stale
- UI shows outdated or cached values
- partial updates across services

---

## 3. Timing & Sync Issues

Check if mismatch is caused by delay rather than failure.

### Check:
- async processing lag
- queue backlog
- eventual consistency delay
- cache invalidation timing
- batch processing intervals

---

## 4. Basic Comparison Query Pattern

Use this to compare recent updates:

```sql
SELECT id, status, updated_at
FROM table_name
WHERE updated_at >= NOW() - INTERVAL '24 hours';
```

---

## 5. Source of Truth Identification

Determine authoritative system:

- Which system owns the data?
- Is replication one-way or bi-directional?
- Is transformation happening between layers?
- Is caching overriding fresh data?

---

## 6. Common Root Causes

Most inconsistencies come from:

- replication lag
- caching issues
- async processing delays
- partial write failures
- transformation layer bugs
- schema mismatches between services

---

## Key Principle

Data mismatch does not always mean data is wrong.

Often it means systems are temporarily out of sync.
