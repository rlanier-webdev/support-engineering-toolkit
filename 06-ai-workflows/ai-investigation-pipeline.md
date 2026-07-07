# AI Investigation Pipeline

Defines how the AI workflows in this folder work together to support incident investigation from initial intake through post-incident learning.

This is the **architecture document** for the AI-assisted investigation framework. Individual files describe each workflow; this document explains how they connect into a complete investigation pipeline.


## Purpose

Each workflow in this folder solves a specific investigation challenge:

- Converting unstructured tickets into usable signals
- Summarizing large volumes of logs
- Correlating events across multiple systems
- Generating investigation hypotheses
- Recommending relevant runbooks
- Building structured investigation plans
- Producing incident summaries
- Capturing lessons learned

Individually, these workflows improve one part of the investigation.

Together, they create a repeatable process that helps engineers investigate incidents faster while maintaining human oversight.


## End-to-End Investigation Pipeline

```text
Raw Ticket / Alert
        │
        ▼
AI Ticket Triage
        │
        ▼
AI Log Summarization
        │
        ▼
AI Signal Correlation
        │
        ▼
AI Root Cause Hypothesis Generator
        │
        ▼
AI Runbook Recommendation
        │
        ▼
AI Investigation Plan Generator
        │
        ▼
Human Investigation
        │
        ▼
AI Incident Summary Generator
        │
        ▼
Human Review & Postmortem
        │
        ▼
AI Learning Feedback Loop
```

Throughout every stage, **`ai-incident-reasoning-limits.md`** provides guardrails for confidence labeling, uncertainty handling, and escalation.


## Pipeline Overview

| Stage | Workflow | Purpose |
|--------|----------|---------|
| 1 | `ai-ticket-triage.md` | Convert unstructured tickets into structured incident signals |
| 2 | `ai-log-summarization.md` | Summarize high-volume logs into actionable context |
| 3 | `ai-signal-correlation.md` | Correlate logs, metrics, alerts, and events into investigation clusters |
| 4 | `ai-root-cause-hypothesis-generator.md` | Generate ranked investigation hypotheses |
| 5 | `ai-runbook-recommendation.md` | Recommend relevant operational runbooks |
| 6 | `ai-investigation-plan-generator.md` | Produce a prioritized investigation checklist |
| 7 | Human Investigation | Validate hypotheses through evidence |
| 8 | `ai-incident-summary-generator.md` | Generate timelines, summaries, and draft postmortems |
| 9 | `ai-learning-feedback-loop.md` | Capture verified knowledge for future investigations |


## Stage Breakdown

### 1. Investigation Intake

**Workflow**

- `ai-ticket-triage.md`

**Purpose**

Normalize customer reports, alerts, and internal tickets into structured incident signals.

**Output**

- Symptoms
- Customer impact
- Severity indicators
- Likely ownership
- Missing information


### 2. Context Generation

**Workflows**

- `ai-log-summarization.md`
- `ai-signal-correlation.md`

**Purpose**

Transform large volumes of operational data into an organized investigation context.

**Output**

- Log summaries
- Investigation clusters
- Correlated operational signals
- Incident timeline


### 3. Hypothesis Generation

**Workflow**

- `ai-root-cause-hypothesis-generator.md`

**Purpose**

Generate evidence-based hypotheses that prioritize likely investigation paths.

**Output**

- Ranked hypotheses
- Supporting evidence
- Confidence levels
- Recommended next steps


### 4. Investigation Planning

**Workflows**

- `ai-runbook-recommendation.md`
- `ai-investigation-plan-generator.md`

**Purpose**

Recommend operational guidance and convert hypotheses into an actionable investigation plan.

**Output**

- Recommended runbooks
- Investigation checklist
- Validation steps


### 5. Human Investigation

Engineers validate each hypothesis using:

- Logs
- Metrics
- Database queries
- Monitoring systems
- Operational runbooks
- Production evidence

Only confirmed findings become part of the incident record.


### 6. Documentation

**Workflow**

- `ai-incident-summary-generator.md`

**Purpose**

Generate consistent technical documentation after the investigation.

Outputs may include:

- Executive summary
- Technical summary
- Timeline
- Customer impact
- Draft postmortem

All documentation requires human review before distribution.


### 7. Continuous Learning

**Workflow**

- `ai-learning-feedback-loop.md`

**Purpose**

Convert confirmed postmortem findings into reusable operational knowledge.

Future investigations can reference:

- Similar incidents
- Proven investigation paths
- Successful runbooks
- Historical failure patterns

Only verified findings are added to the knowledge base.


## Integration with the Toolkit

This pipeline integrates with the broader Support Engineering Toolkit.

| Toolkit Module | Integration |
|----------------|-------------|
| `01-intake-and-triage/` | AI triage complements manual intake and severity assessment |
| `02-api-troubleshooting/` | Investigation plans reference API troubleshooting workflows |
| `03-sql-investigation/` | Hypotheses may require SQL validation and data investigation |
| `04-incident-response/` | AI-generated summaries support timelines and postmortems |
| `05-escalation-guides/` | Escalation occurs when investigation confidence remains low or engineering intervention is required |


## Human Decision Points

AI accelerates investigation—it does not replace engineering judgment.

Human review is required to:

- Confirm severity
- Validate hypotheses
- Execute runbooks
- Confirm root cause
- Approve customer communication
- Finalize postmortems


## Design Principles

This framework follows five principles:

1. Normalize before analyzing.
2. Summarize before hypothesizing.
3. Correlate before concluding.
4. Verify before communicating.
5. Learn from every confirmed incident.


## Key Principle

> AI accelerates investigation by organizing information, reducing noise, and prioritizing likely paths—not by replacing engineering judgment.

Every workflow in this folder exists to help engineers make faster, better-informed decisions while keeping humans responsible for verification, diagnosis, and final communication.