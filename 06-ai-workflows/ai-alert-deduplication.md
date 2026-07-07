# AI Alert Deduplication (v2)

AI-powered clustering system for reducing alert noise by grouping duplicate and near-duplicate monitoring signals before incident declaration.


## Purpose

Monitoring systems often generate multiple alerts for the same underlying issue across hosts, pods, or retries. This creates alert fatigue and hides meaningful signals.

This workflow consolidates repeated signals into structured groups so on-call engineers see one coherent view of what is happening, while preserving every original alert as evidence.

It improves signal clarity without changing alerting behavior.


## Core Principles

* Preserve all raw alerts (never delete or discard)
* Reduce noise through grouping, not suppression
* Group by shared failure condition, not wording similarity alone
* Avoid merging unrelated systems, even if messages look similar
* Separate duplication from correlation (do not confuse the two)


## Key Definitions

### Duplicate Alert

Multiple alerts representing the same failure condition within the same service and time window (e.g., per pod or instance duplication).

### Related Alert

Different alert types that may share a broader incident context but do not represent the same failure condition.

### Standalone Alert

A unique alert that does not reasonably match others in condition or scope.


## Input Format

Alerts may arrive as semi-structured text logs:

```
[09:12:03] Alert: High latency - reports-service-pod-1
[09:12:04] Alert: High latency - reports-service-pod-2
[09:12:05] Alert: High latency - reports-service-pod-3
[09:12:06] Alert: DB connection errors - reports-service
[09:13:10] Alert: High latency - auth-service-pod-1
```

Preferred structured format (if available):

```
timestamp | service | alert_type | host | message
```


## Grouping Rules

### Strong Match (Always Group)

Group alerts when all are true:

* Same service
* Same failure type or metric signature
* Same or overlapping time window (default: 10 minutes)
* Differences only at host/pod/instance level


### Medium Match (Group with Confidence Flag)

Group when:

* Same service
* Closely related failure signals (e.g., latency + timeout errors)
* Same time window
* Evidence suggests shared underlying system stress

Mark as:

* confidence: medium
* requires correlation review


### Do NOT Group (Hard Constraints)

Never merge if any of the following differ:

* Service
* Environment (prod vs staging vs dev)
* Metric category (latency vs errors vs saturation vs availability)
* Time gap exceeds threshold without continuity evidence
* Only similarity is wording or template text


## Related Signal Detection (Not Grouping)

If alerts are not duplicates but appear related:

* Flag relationship only
* Do NOT merge groups
* Suggest correlation analysis

Examples:

* DB errors + service latency spike
* queue backlog + downstream timeout increase


## Output Format

```
DEDUPLICATED ALERTS

Group 1: High latency — reports-service (3 occurrences)
Confidence: High
Type: Duplicate group
Time range: 09:12:03–09:12:05

Sources:
- reports-service-pod-1
- reports-service-pod-2
- reports-service-pod-3

Summary:
Same latency condition across multiple pods indicating service-level degradation.


Group 2: DB connection errors — reports-service (1 occurrence)
Confidence: Medium
Type: Related signal (not duplicate)

Source:
- reports-service (09:12:06)

Notes:
May be contributing factor to latency group above.
Flagged for correlation analysis.


Standalone: High latency — auth-service (1 occurrence)
Confidence: High
Type: Standalone

Source:
- auth-service-pod-1 (09:13:10)

Notes:
Same symptom type but different service and independent failure domain.
```


## Time Window Rule

Default grouping window:

* 10 minutes rolling window

Extend only if:

* alerts show continuous recurrence pattern
* same signature persists without resolution gap


## Quality Checklist

* Every alert is either grouped or explicitly standalone
* No silent drops
* Groups are based on shared failure conditions, not text similarity
* Related signals are flagged, not merged
* Confidence level is included for every group
* Time boundaries are explicitly shown


## Key Principle

Deduplication reduces volume. It does not interpret priority, ownership, or root cause.

That responsibility belongs to incident correlation systems and human responders.
