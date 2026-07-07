# AI Log Summarization

Transform high-volume log data into concise, structured incident context that accelerates investigation without replacing human analysis.


## Purpose

During an incident, the challenge is rarely a lack of logs—it's identifying the important information hidden within them.

This workflow uses AI to organize and summarize large volumes of log data into meaningful patterns, allowing engineers to quickly understand what changed, when it changed, and which systems are affected.

The goal is to reduce time spent scanning repetitive log entries while preserving access to the original data for deeper investigation.


## Objectives

This workflow helps engineers:

- Identify dominant error patterns
- Detect sudden changes in system behavior
- Separate high-value signals from routine operational noise
- Summarize stack traces into plain-language explanations
- Build an investigation starting point without making diagnostic conclusions


## Supported Log Sources

This workflow can summarize logs from:

- Application logs
- API request logs
- Authentication logs
- Infrastructure logs
- Container logs
- Reverse proxy logs
- Load balancer logs
- Structured JSON logs
- Plain text log files


## Input

Raw log data in any supported format.

Examples include:

- JSON logs
- Plain text logs
- Stack traces
- Multi-service log excerpts
- Aggregated log exports


## Workflow

### Step 1 — Parse

Identify:

- timestamps
- services
- severity levels
- request identifiers
- correlation IDs
- exception types


### Step 2 — Group

Cluster repeated events into logical patterns.

Examples:

- identical exceptions
- repeated timeout messages
- authentication failures
- connection retries


### Step 3 — Detect Anomalies

Identify significant behavioral changes, including:

- sudden increases in error rate
- new error types
- service degradation
- recurring failures
- correlated events across services


### Step 4 — Separate Signal from Noise

Highlight investigation-worthy events while reducing visual clutter.

High signal:

- rapid error spikes
- first occurrence of new failures
- cascading service failures
- repeated exceptions

Noise:

- successful health checks
- expected background jobs
- repetitive informational logs
- routine cache activity

Noise is summarized—not discarded.


### Step 5 — Generate Summary

Produce a concise incident overview that includes:

- affected services
- dominant error patterns
- event timeline
- anomaly summary
- confidence level
- links back to supporting log entries


## Example Output

```text
LOG SUMMARY

Incident Window:
09:12:03 – 09:16:40 UTC

Affected Service:
reports-service

Primary Pattern
412 database connection timeout events

Observed Behavior

• Three retry attempts before replica failover
• Pattern began at 09:12 UTC
• Error rate increased from 0/min to approximately 90/min
• Condition remained active through the final log entry

Secondary Pattern

3 authentication failures affecting a single user

Assessment:
Low confidence that these events are related.

Noise Summary

• Routine health checks
• Cache hit/miss debug messages
• Scheduled maintenance logs

Confidence

High confidence in observed behavior.

No root cause determination has been made.
```


## Prompt Template

```text
You are summarizing logs for an engineer responding to an active production incident.

Your responsibilities:

- Group repeated events into patterns
- Count occurrences
- Summarize stack traces in plain language
- Detect spikes and behavioral changes
- Separate likely signal from routine noise
- Reference supporting log entries
- Do not speculate about root cause

Logs:

"""
{log_excerpt}
"""
```


## Quality Checklist

- Similar log events are grouped together
- Every pattern includes occurrence counts
- Time windows are clearly defined
- Stack traces are summarized into plain language
- Raw logs remain available for verification
- Noise is identified but not removed
- No assumptions are made about causality


## Related Workflows

- `02-api-troubleshooting/`
- `04-incident-response/`
- `06-ai-workflows/ai-root-cause-suggestion.md`
- `06-ai-workflows/ai-investigation-assistant.md`


## Key Principle

> Log summaries describe system behavior—they do not explain system behavior.

Summarization answers **what happened**.

Root cause analysis answers **why it happened**.