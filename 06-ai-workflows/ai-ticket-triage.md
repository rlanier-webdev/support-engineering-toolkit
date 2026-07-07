# AI Ticket Triage

Convert unstructured support requests into structured incident signals that provide a consistent starting point for technical investigation.

> **This workflow extracts facts—it does not diagnose problems.**
>
> The output becomes the structured input for downstream workflows such as log summarization, signal correlation, hypothesis generation, and investigation planning.


## Purpose

Support tickets rarely arrive in a format that's immediately useful for technical investigation.

Customers describe symptoms using natural language, often mixing observations, assumptions, business impact, and urgency into a single narrative.

This workflow extracts objective incident signals from those reports, producing a structured summary that engineers can immediately use.


## Objectives

This workflow helps engineers:

- Extract observable symptoms
- Identify business impact
- Estimate incident severity
- Identify likely service ownership
- Highlight missing investigation data
- Standardize ticket quality before investigation begins


## Inputs

Raw support requests, including:

- Customer tickets
- Internal reports
- Chat conversations
- Email requests
- Help desk submissions

No preprocessing is required.


## Workflow

### Step 1 — Extract Observable Symptoms

Identify only what has been directly observed.

Examples:

- page does not load
- timeout occurs
- stale data displayed
- login fails
- report generation is slow

Avoid interpreting **why** the symptom exists.


### Step 2 — Identify Customer Impact

Determine how the issue affects users.

Examples:

- single user
- department
- multiple customers
- organization-wide
- production outage

Capture business impact separately from technical symptoms.


### Step 3 — Identify Severity Signals

Look for indicators such as:

- blocked business processes
- revenue impact
- deadline risk
- urgency language
- affected user count
- workaround availability

Severity remains a recommendation until confirmed.


### Step 4 — Identify Likely Ownership

Suggest likely service ownership based on observed symptoms.

Examples:

- Reporting Service
- Authentication
- API Gateway
- Database
- Billing Platform

Ownership suggestions should be treated as investigative guidance.


### Step 5 — Identify Missing Information

List information that would materially improve investigation.

Examples:

- exact start time
- affected users
- browser or client version
- screenshots
- request IDs
- reproduction steps


## Example Output

```text
STRUCTURED INCIDENT SIGNAL

Observed Symptoms

• Reports page remains in a loading state
• Some users receive stale data

Customer Impact

• Month-end financial close is blocked
• Multiple users affected

Severity Signals

• Business-critical workflow impacted
• Urgent customer request
• Suggested Severity: SEV-2 (pending confirmation)

Likely Service Ownership

Primary:
Reporting Service

Secondary:
Caching Layer

Missing Information

• Exact incident start time
• Number of affected users
• Browser version
• Request ID

Confidence

Medium

Based solely on customer-reported information.
```


## Extraction Rules

Always:

- Extract observable facts
- Preserve customer wording where appropriate
- Separate symptoms from assumptions
- Flag missing information
- Recommend—not assign—severity

Never:

- Infer root cause
- Invent missing details
- Rewrite customer intent
- Remove uncertainty


## Quality Checklist

- Every extracted symptom appears in the original request
- Business impact is separated from technical symptoms
- Missing information is identified explicitly
- Severity remains a recommendation
- Confidence reflects available evidence


## Related Workflows

- `ai-log-summarization.md`
- `ai-signal-correlation.md`
- `ai-root-cause-hypothesis-generator.md`
- `ai-investigation-plan-generator.md`


## Key Principle

> Good investigations begin with good signal extraction.

A well-triaged ticket reduces ambiguity without introducing assumptions.