# Relationship & Join Verification

Use this guide when investigating missing, duplicated, or inconsistent data caused by relationships between tables.

Many application issues originate from incorrect assumptions about how records are related—not because the data itself is missing.


## Purpose

Relationship verification helps determine whether records are correctly linked before investigating application logic or API behavior.

Use this guide to identify:

- Missing related records
- Incorrect joins
- Duplicate results
- Broken relationships
- Orphaned records


## When to Use This Guide

Use these checks when:

- Data appears missing in the UI or API
- Duplicate records are returned
- Related information is incomplete
- Child records aren't associated with parent records
- Reports show unexpected totals
- A feature behaves differently than the underlying data suggests


# 1. Verify the Relationship

Before writing complex queries, confirm the relationship exists.

### Questions

- Which table owns the data?
- What column links the records?
- Is the relationship one-to-one, one-to-many, or many-to-many?
- Is the expected foreign key populated?


# 2. Validate Foreign Keys

Missing or incorrect foreign keys are a common source of support issues.

### Check for

- NULL foreign keys
- Invalid references
- Incorrect IDs
- Unexpected relationship values

### Example

```sql
SELECT *
FROM child_table
WHERE parent_id IS NULL;
```


# 3. Check for Orphaned Records

Orphaned records exist without a matching parent record.

### Example

```sql
SELECT c.*
FROM child_table c
LEFT JOIN parent_table p
    ON c.parent_id = p.id
WHERE p.id IS NULL;
```

Common causes:

- Deleted parent records
- Failed imports
- Partial data migrations
- Synchronization failures


# 4. Review Join Types

Choosing the wrong join can completely change your results.

## INNER JOIN

Returns only matching records.

Use when matching data is required.


## LEFT JOIN

Returns all records from the left table, including unmatched rows.

Useful when identifying missing relationships.


## RIGHT JOIN

Less commonly used.

Returns all rows from the right table.


## FULL OUTER JOIN

Returns every record from both tables where supported.

Helpful for comparison and reconciliation.


# 5. Look for Duplicate Rows

Duplicates are often caused by one-to-many relationships that were expected to behave as one-to-one.

### Example

```sql
SELECT
    id,
    COUNT(*)
FROM table_name
GROUP BY id
HAVING COUNT(*) > 1;
```

Consider:

- Missing DISTINCT
- Incorrect join conditions
- Multiple child records
- Duplicate source data


# 6. Validate Cardinality

Confirm the relationship matches expectations.

Examples:

- One customer → many orders
- One order → many line items
- One user → one profile

Unexpected cardinality often explains inconsistent results.


# 7. Compare Expected vs Actual Results

Ask:

- How many records should exist?
- How many were returned?
- Which records are missing?
- Which records appear multiple times?

Small comparisons often reveal relationship issues quickly.


# Investigation Checklist

Before moving to application debugging:

- Relationship is understood
- Foreign keys are valid
- No orphaned records
- Correct join type selected
- Duplicate rows investigated
- Record counts match expectations


# Common Root Causes

Relationship issues are commonly caused by:

- Missing foreign keys
- Incorrect join conditions
- One-to-many duplication
- Deleted parent records
- Partial synchronization
- Data migration inconsistencies
- Filtering before joining
- Incorrect assumptions about the data model


# Key Principle

> When data appears missing, verify the relationship before assuming the data is gone.

Many support issues are caused by how data is joined—not by the data itself.