# AI Incident Signal Correlation

Correlate logs, metrics, alerts, and operational events into coherent incident narratives that help engineers understand what is happening across the system.

> **This workflow identifies relationships—not root causes.**
>
> Signals may be related in time or topology without sharing the same underlying cause.


## Purpose

Modern distributed systems produce large volumes of independent operational signals.

During an incident, engineers often receive monitoring alerts, log events, infrastructure notifications, deployment records, and customer reports simultaneously.

This workflow groups related signals into investigation clusters, reducing alert fatigue and providing a structured view of the incident before root cause analysis begins.


## Objectives

This workflow helps engineers:

- Correlate signals across multiple monitoring sources
- Build a unified incident timeline
- Separate related events from unrelated operational noise
- Identify affected services and dependencies
- Reduce duplicate investigation effort


## Supported Signal Sources

Signals may include:

- Monitoring alerts
- Application logs
- Infrastructure logs
- Metrics
- Traces
- Deployment events
- Health checks
- Customer reports
- Status page events


## Inputs

A collection of operational signals occurring during an investigation window.

Example:

```text
09:12  Alert    reports-service error rate increased
09:12  Metric   Database connection pool utilization reached 100%
09:12  Log      412 database timeout events
09:13  Alert    API Gateway latency exceeded threshold
08:47  Alert    Authentication 4xx increase
```


## Workflow

### Step 1 — Normalize Signals

Extract common attributes:

- timestamp
- service
- severity
- source
- infrastructure component
- environment


### Step 2 — Identify Relationships

Evaluate relationships based on:

- time proximity
- service dependencies
- shared infrastructure
- deployment timing
- request path
- correlated behavioral changes


### Step 3 — Form Investigation Clusters

Group signals that likely describe the same operational event.

Each cluster should include:

- affected systems
- investigation window
- supporting signals
- confidence level

Signals that do not belong in an existing cluster should remain independent.


### Step 4 — Generate Incident Narrative

Summarize each cluster using factual observations.

Example:

```text
Cluster

Reports Service Degradation

Investigation Window

09:12–09:16 UTC

Affected Components

• reports-service
• db-primary
• API Gateway

Observed Behavior

• Database connection pool reached capacity
• Connection timeout events increased rapidly
• API latency increased shortly afterward

Relationship Assessment

These signals describe the same operational event.

No causal relationship has been established.
```


## Correlation Guidelines

### Strong Correlation

Signals share:

- similar timestamps
- dependency relationships
- infrastructure components
- synchronized behavioral changes


### Moderate Correlation

Signals overlap but require additional investigation.


### Weak Correlation

Minimal overlap or limited supporting evidence.

Should remain separate until additional data is available.


## Rules

Always:

- Preserve original timestamps
- Explain why signals were grouped
- Identify affected services
- Keep unrelated signals separate
- Assign confidence levels

Never:

- Assume causation
- Force unrelated signals into a cluster
- Hide unclustered signals
- Replace engineering investigation


## Quality Checklist

- Every cluster has a defined investigation window
- Relationships are supported by observable evidence
- Confidence reflects available evidence
- Independent signals remain visible
- Incident narratives are descriptive rather than speculative


## Related Workflows

- `ai-ticket-triage.md`
- `ai-log-summarization.md`
- `ai-root-cause-hypothesis-generator.md`
- `ai-investigation-plan-generator.md`


## Key Principle

> Correlation identifies patterns—not causes.

This workflow explains **which signals appear related**.

Determining **why they are related** belongs to the investigation and root cause analysis process.