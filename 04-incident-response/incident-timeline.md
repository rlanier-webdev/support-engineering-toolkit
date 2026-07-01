# Incident Timeline

Use this template to document the sequence of events during an incident.

A well-maintained timeline helps teams understand what happened, when it happened, how the issue evolved, and how it was resolved. It also provides the foundation for post-incident reviews and future process improvements.


# Purpose

An accurate timeline should answer four questions:

- **When** did the incident begin?
- **What** happened?
- **Who** responded?
- **How** was the incident resolved?

Record confirmed events as they occur. Avoid assumptions or retrospective estimates whenever possible.


# Incident Summary

| Field | Value |
|-------|-------|
| Incident ID | |
| Severity | |
| Status | |
| Start Time (UTC) | |
| End Time (UTC) | |
| Total Duration | |
| Incident Owner | |


# Timeline of Events

| Time (UTC) | Event | Owner | Notes |
|------------|-------|-------|-------|
| HH:MM | Issue detected | | Detection source, alert, or customer report |
| HH:MM | Investigation started | | Initial findings |
| HH:MM | Incident escalated | | Teams or stakeholders notified |
| HH:MM | Mitigation initiated | | Temporary actions taken |
| HH:MM | Root cause identified | | Confirmed cause |
| HH:MM | Permanent fix deployed | | Configuration, code, or infrastructure change |
| HH:MM | Service verified | | Monitoring confirms recovery |
| HH:MM | Incident resolved | | Normal operations restored |

Add additional rows as needed to accurately reflect the investigation.


# Customer Impact

Document the observable impact rather than assumptions.

| Category | Details |
|----------|---------|
| Affected Services | |
| Customer Impact | |
| Estimated Users Affected | |
| Error Symptoms | |
| Data Integrity Impact | None / Suspected / Confirmed |
| Workaround Available | Yes / No |


# Investigation Summary

Document the key findings.

## Root Cause

Brief summary of the confirmed cause.


## Resolution

Describe the actions that restored service.


## Validation

Explain how normal operation was confirmed.

Examples:

- Monitoring returned to normal
- Error rate returned to baseline
- Customer validation received
- Automated health checks passed


# Key Decisions

Record important decisions made during the incident.

| Time | Decision | Reason |
|------|----------|--------|
| | | |
| | | |


# Follow-Up Actions

Capture improvements identified during the investigation.

| Action | Owner | Status |
|--------|-------|--------|
| | | |
| | | |


# Timeline Checklist

Before closing an incident, verify that the timeline includes:

- Detection time
- Investigation start
- Escalation events
- Mitigation actions
- Root cause identification
- Resolution steps
- Service validation
- Follow-up actions


# Key Principle

> A timeline should document **facts, not opinions**.

Accurate timelines improve communication during an incident, simplify post-incident reviews, and help teams identify opportunities to reduce future response times.