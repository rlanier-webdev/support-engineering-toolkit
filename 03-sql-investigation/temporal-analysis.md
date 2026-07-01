# ⏱️ Temporal Analysis

Use this guide when investigating issues related to timing, synchronization, or delayed data updates.

Many production issues are not caused by incorrect data, but by **when** data becomes available across systems.


## Purpose

Temporal analysis helps determine whether an issue is caused by timing rather than application logic or data integrity.

Use this guide to identify:

- Delayed updates
- Synchronization lag
- Out-of-order processing
- Stale data
- Timezone inconsistencies
- Scheduled job failures


## When to Use This Guide

Use these checks when:

- Data appears to be missing but shows up later
- API responses differ from database values
- Reports are inconsistent
- Changes are delayed between systems
- Users report intermittent issues
- Scheduled processes appear to have failed


# 1. Verify Timestamps

Start by reviewing key timestamp fields.

Examples include:

- `created_at`
- `updated_at`
- `processed_at`
- `completed_at`
- `deleted_at`

Questions to ask:

- Are timestamps present?
- Are they in the expected order?
- Were updates recorded when expected?
- Do timestamps match the reported timeline?


# 2. Check Synchronization Delays

Many systems update asynchronously.

Investigate:

- Replication lag
- Background workers
- Queue processing
- Scheduled jobs
- Event-driven updates

Questions:

- Has the downstream system processed the change?
- Is there a known synchronization delay?
- Is the delay within expected limits?


# 3. Validate Event Order

Systems often rely on events occurring in sequence.

Look for situations where:

- Updates occur before record creation
- Older events overwrite newer data
- Duplicate events are processed
- Events are processed out of order

Incorrect sequencing can produce inconsistent application behavior.


# 4. Review Timezone Handling

Timezone issues often appear as missing or incorrect data.

Verify:

- Database timezone
- Application timezone
- API timestamps
- User-local display times

Common symptoms include:

- Incorrect reporting periods
- Missing daily activity
- Off-by-one-day results


# 5. Investigate Scheduled Processes

Some systems rely on scheduled jobs to update data.

Check:

- Import jobs
- Export jobs
- Batch processing
- Cleanup tasks
- Scheduled synchronizations

Questions:

- Did the job run?
- Did it complete successfully?
- Were any errors reported?


# 6. Identify Stale Data

The correct data may exist but not yet be visible.

Potential causes:

- Cache expiration
- Replication delay
- Background processing
- Long-running transactions

Determine whether the issue is temporary or persistent.


# 7. Compare Expected vs Actual Timeline

Build a timeline using available evidence.

Example:

| Event | Expected Time | Actual Time |
|--------|---------------|-------------|
| Record Created | 10:00 | 10:00 |
| API Updated | 10:01 | 10:06 |
| UI Refreshed | 10:02 | 10:07 |

Even small timing differences can explain customer-reported issues.


# Investigation Checklist

Before escalating:

- Timestamp fields reviewed
- Synchronization verified
- Event order confirmed
- Timezones validated
- Scheduled jobs checked
- Cache behavior considered
- Timeline reconstructed


# Common Root Causes

Temporal issues are commonly caused by:

- Background processing delays
- Queue backlogs
- Replication lag
- Cache synchronization
- Scheduled job failures
- Timezone conversion errors
- Event ordering issues
- Long-running transactions


# Key Principle

> When the data is correct but the behavior is inconsistent, investigate **when** the data changed—not just **what** changed.

Understanding the timeline is often the fastest path to identifying the true root cause.