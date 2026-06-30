# Data Validation Checks

Use this file when verifying whether database data is correct, complete, and structurally valid before moving into deeper debugging (joins, API behavior, or system logic).

This is the first step in SQL-based investigation.

---

## Purpose

Many support issues are incorrectly assumed to be system or API bugs when the root cause is actually data-level inconsistency.

This checklist ensures you confirm data integrity before escalating or debugging further.

---

## 1. Record Existence Check

Verify the data actually exists in the expected location.

### Checks:
- Does the record exist in the database?
- Is it in the correct table?
- Has it been soft-deleted or archived?
- Is it being filtered out by default scopes?

### Example:
```sql
SELECT *
FROM table_name
WHERE id = 'target_id';
```

---

## 2. Field Completeness Check

Ensure required fields are populated and usable.

### Checks:
- Are required fields NULL?
- Are values empty strings instead of NULL?
- Are partially written records present?
- Are defaults masking missing data?

### Example:
```sql
SELECT *
FROM table_name
WHERE required_field IS NULL;
```

---

## 3. Schema Integrity Check

Confirm structure matches expected design.

### Checks:
- Are column names still valid?
- Have fields been renamed or deprecated?
- Are data types correct?
- Are systems writing to outdated schema versions?

### Example:
```sql
DESCRIBE table_name;
```

---

## 4. Basic Targeted Query Pattern

Start broad, then narrow down.

### Pattern:
```sql
SELECT *
FROM table_name
WHERE id = 'target_id'
  AND created_at >= NOW() - INTERVAL '7 days';
```

Use filtering to progressively isolate the issue.

---

## 5. Null & Data Quality Check

Identify missing or invalid data patterns.

### Checks:
- Unexpected NULL values
- Empty or placeholder values
- Incomplete ingestion

### Example:
```sql
SELECT *
FROM table_name
WHERE column_name IS NULL
   OR column_name = '';
```

---

## 6. Quick Validation Mental Checklist

Before moving to joins or deeper debugging:

- Does the record exist?
- Are required fields populated?
- Is the schema correct?
- Is the data current?
- Is anything silently missing?

---

## Key Principle

Never assume a system or API issue before confirming data integrity.

If validation fails here, everything built on top of it will appear broken.
