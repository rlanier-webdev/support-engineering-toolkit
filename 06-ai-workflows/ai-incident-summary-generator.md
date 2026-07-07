# AI Incident Summary Generator

AI-assisted system for drafting incident documentation from resolved incident data, including timelines, impact summaries, and post-incident review skeletons.

> This workflow is for documentation acceleration only. It does not generate authoritative incident records.


## Purpose

After an incident is resolved, critical documentation still needs to be produced:

* timeline reconstruction
* customer and business impact summary
* technical explanation of what happened
* postmortem structure for follow-up work

This workflow uses AI to transform structured incident artifacts into draft documentation so humans can focus on validation, correction, and decision-making rather than rewriting.


## What This Workflow Does

* Reconstructs a chronological timeline from event data
* Produces separate summaries for:

  * technical audiences (engineers, responders)
  * business audiences (stakeholders, leadership)
* Generates a structured postmortem draft (not final)
* Preserves source fidelity from incident logs and confirmed investigation outputs


## What This Workflow Does Not Do

This system must NEVER:

* Publish or finalize postmortems without human approval
* Invent missing timeline events or details
* Assign blame to individuals, teams, or systems
* Override or reinterpret confirmed root cause statements
* Introduce new facts not present in source material
* Resolve ambiguity without explicitly marking it as unresolved


## Input Requirements

Accepted inputs include:

* timestamped event logs
* incident declarations
* investigation notes
* confirmed findings (clearly labeled)

Example:

```id="2m9k4c"
09:12 UTC - reports-service begins timing out connecting to db-primary
09:15 UTC - incident declared, SEV-2
09:18 UTC - db-primary connection pool at 100% utilization confirmed
09:24 UTC - pool size increased, service recovery begins
09:31 UTC - error rate returns to baseline
CONFIRMED ROOT CAUSE: connection pool exhaustion due to batch job traffic spike
```


## Output Structure

All outputs must follow a consistent, reviewable format:

```id="w8qk1n"
INCIDENT SUMMARY DRAFT (FOR HUMAN REVIEW ONLY)


## Timeline (Source-Aligned)
- 09:12 UTC — reports-service begins failing to connect to db-primary
- 09:15 UTC — Incident declared (SEV-2)
- 09:18 UTC — db-primary connection pool reaches 100% utilization
- 09:24 UTC — Pool size increased; recovery begins
- 09:31 UTC — Error rate returns to baseline

Duration: 19 minutes (09:12–09:31 UTC)


## Technical Summary (Engineering View)
reports-service experienced connection timeouts to db-primary due to exhaustion of the database connection pool. Investigation confirmed full pool utilization during the incident window. Service recovery occurred after increasing pool capacity.

Root cause status:
- If explicitly confirmed in input: state as confirmed
- If not confirmed: explicitly write “Root cause: pending confirmation”


## Business Summary (Stakeholder View)
Customers experienced a brief period of degraded service where report loading failed or timed out. The issue lasted approximately 19 minutes and has been resolved. No data loss occurred.


## Postmortem Draft (Human Review Required)

### Summary
[2–3 sentence high-level description — must be reviewed]

### Impact
[Customer/business impact — must reflect only confirmed data]

### Root Cause
Connection pool exhaustion on db-primary due to increased batch job traffic
Status: CONFIRMED (only if explicitly provided in input)

### Resolution
Increased connection pool capacity on db-primary restored service stability

### Detection
[Required field — must be filled by human if not present in input]

### Contributing Factors
[Optional / to be completed during review]

### Action Items
- [To be defined during review]
- [Monitoring / scaling / scheduling improvements]


NOTE:
This document is an AI-generated draft derived from incident artifacts. It is not an authoritative record and must be reviewed before sharing or filing.
```


## Prompt Rules

```
You are generating incident documentation drafts from structured incident data.

STRICT RULES:
- Use only information present in the input
- Do not invent missing events or details
- Maintain strict chronological ordering in the timeline
- Separate technical and business summaries clearly
- Only mark root cause as confirmed if explicitly labeled in input
- If missing information exists, write "pending human input"
- Do not assign blame or evaluate performance
- Do not introduce new facts under any circumstance

Incident data:
"""
{incident_data}
"""
```


## Dual-Audience Rules

### Technical Summary

* Includes system names, metrics, failure modes
* Focuses on mechanism and resolution path
* May reference infrastructure components directly

### Business Summary

* Focuses on customer impact and duration
* Avoids internal system naming unless necessary
* Must remain consistent with technical summary

Both summaries must describe the same incident truth, just at different levels of abstraction.


## Quality Checklist

Before output is accepted:

* Timeline strictly matches source timestamps
* No invented events or inferred gaps
* Root cause is only stated if explicitly confirmed
* Technical and business summaries align
* Postmortem clearly labels incomplete fields
* No blame or performance judgment included
* All unknowns explicitly marked


## Key Principle

AI’s role is to compress incident data into readable structure — not to interpret authority over it.

Every summary is a draft artifact meant to reduce writing effort, not replace human validation.
