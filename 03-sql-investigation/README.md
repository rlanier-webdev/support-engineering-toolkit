# SQL Investigation Toolkit

A structured approach for investigating data-related support issues using SQL-based validation, anomaly detection, and root cause analysis.

This toolkit is used when API behavior, UI data, or system reports do not match expected results.

---

## Purpose

Many support issues are not caused by the API or application logic itself, but by underlying data inconsistencies.

This toolkit helps:

- Validate whether data is correct at the source
- Detect inconsistencies between systems
- Confirm whether issues are data-related vs system-related
- Support engineering escalations with concrete evidence

---

## When to Use This Toolkit

Use this when investigating:

- Missing or incorrect data in UI or API responses
- Data mismatch between systems
- Unexpected null or empty values
- Duplicate or inconsistent records
- Delayed or missing updates
- Reporting or analytics discrepancies

---

## Core Investigation Principles

> Always verify the data layer before assuming application failure.

Most “bugs” are actually:
- data sync issues
- incorrect joins
- stale records
- missing relationships
- delayed ingestion

---

## 1. Data Validation Checks

Start by confirming raw data integrity.

- Are expected records present?
- Are fields populated correctly?
- Are null values expected or abnormal?
- Are timestamps aligned with expected updates?

---

## 2. Consistency Checks

Compare across sources or states.

- API response vs database state
- UI display vs backend data
- Source system vs downstream system
- Before vs after update events

---

## 3. Relationship & Join Verification

Most support issues come from broken assumptions in joins.

Check:

- Missing foreign keys
- Incorrect join conditions
- One-to-many vs one-to-one mismatches
- Orphaned records
- Duplicated join results

---

## 4. Temporal Analysis

Many issues are time-based, not logic-based.

Investigate:

- Delayed writes or sync lag
- Timezone mismatches
- Out-of-order updates
- Event processing delays
- Stale cache behavior

---

## 5. Null & Edge Case Analysis

Null behavior often explains “missing data” reports.

Check for:

- unexpected NULL values
- default value overrides
- partial writes
- incomplete ingestion pipelines

---

## 6. Common Root Cause Patterns

Most SQL-related support issues fall into:

- Incorrect joins causing missing data
- Delayed sync between systems
- Partial ingestion failures
- Schema mismatch between services
- Filtering logic removing valid data
- Cache returning stale results

---

## 7. Investigation Output Standard

Every SQL investigation should produce:

- What data was expected
- What data was actually present
- Where the mismatch occurred
- Whether issue is data, API, or system layer
- Recommended escalation path (if needed)

---

## Key Principle

> If the data is wrong, everything built on top of it will appear broken.

Always validate the source before moving upward in the system stack.