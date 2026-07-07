# AI Investigation Plan Generator

AI system for converting ranked incident hypotheses into a structured, prioritized investigation checklist.

> This workflow does not analyze root cause. It operationalizes investigation effort.


## Purpose

During incidents, engineers waste time deciding *what to check first* rather than actually checking things. This leads to:

* duplicated checks
* missed obvious signals
* inefficient hypothesis testing
* slow time-to-mitigation

This workflow eliminates that decision overhead by turning hypotheses into an ordered, executable investigation plan.


## What This Workflow Does

* Converts ranked hypotheses into step-by-step investigation actions
* Prioritizes checks by:

  * confidence level
  * likelihood of confirmation speed
  * blast radius relevance
* Adds explicit “confirm vs rule out” conditions for each step
* Includes environmental checks (deploys, config changes, infra events)
* Produces a deterministic execution order for investigation


## What This Workflow Does Not Do

This system must NEVER:

* Perform the investigation itself
* Assume outcomes of any check
* Skip hypothesis validation steps, even if they appear obvious
* Reorder steps based on intuition after generation
* Merge multiple hypotheses into a single check unless explicitly justified
* Declare root cause or eliminate hypotheses without evidence


## Input Format

Ranked hypotheses from upstream analysis (e.g. `ai-root-cause-suggestion.md`):

```id="k3m9p1"
1. Database connectivity failure (db-primary) — Confidence: High
2. Connection pool exhaustion in reports-service — Confidence: Medium
3. Auth-service anomaly unrelated to incident — Confidence: Low
```


## Planning Model

Each hypothesis must be translated into a **verification step**, not a vague action.

Every step must include:

* What to check
* Why it matters (linked to hypothesis)
* What confirms it
* What rules it out
* Estimated effort/time


## Prioritization Rules

### Primary Ordering Signals (in order of importance)

1. Hypothesis confidence (High → Medium → Low)
2. Speed of validation (fast signal first)
3. Proximity to user impact (customer-facing systems first)
4. Dependency relationships (downstream effects after upstream checks)


### Mandatory Inclusions

The plan must always include:

* Infrastructure / environment change check (deploys, config, scaling events)
* Core service health checks for top-ranked hypotheses


## Step Construction Rules

Each step must:

* Map to exactly one hypothesis OR one environmental factor
* Be independently executable
* Avoid combining unrelated checks into a single step
* Define explicit success and failure conditions
* Use observable signals only (metrics, logs, dashboards, traces)


## Output Format

```id="7v8q2x"
INVESTIGATION PLAN (EXECUTION ORDERED)


## Step 1 — Validate: Database connectivity failure (db-primary)
Priority: High | Effort: Low | Est. time: 2–3 min

Why this step:
Top-confidence hypothesis affecting core data layer.

Action:
- Check db-primary health dashboard
- Review active connections, CPU, and error rate

Confirms hypothesis if:
- Connection saturation observed
- Elevated DB error rates or failed connections align with incident start

Rules out hypothesis if:
- All metrics within normal operating range during incident window


## Step 2 — Validate: Connection pool exhaustion (reports-service)
Priority: High | Effort: Low | Est. time: 2–4 min

Why this step:
Common failure mode causing DB saturation symptoms.

Action:
- Inspect reports-service connection pool metrics
- Review recent deploys or config changes affecting DB connections

Confirms hypothesis if:
- Pool utilization near maximum
- Recent change correlates with connection spike

Rules out hypothesis if:
- Pool utilization stable and no relevant configuration changes


## Step 3 — Check infrastructure and deployment changes (last 60 minutes)
Priority: High | Effort: Low | Est. time: 1–2 min

Why this step:
Recent changes frequently introduce cascading failures.

Action:
- Review deploy logs
- Check config changes, feature flags, scaling events

Confirms contributing factor if:
- Change aligns with incident start time and affected services

Rules out contributing factor if:
- No relevant changes detected in timeframe


## Step 4 — Validate: Auth-service anomaly (unrelated hypothesis)
Priority: Low | Effort: Low | Est. time: 2–3 min

Why this step:
Ensures symptom overlap is not misleading correlation.

Action:
- Check auth-service error logs and affected user sessions
- Compare with reports-service failure timeline

Confirms relevance if:
- Shared session/user correlation across both services

Rules out hypothesis if:
- No temporal or user-level correlation exists


## Estimated Total Investigation Time: 7–12 minutes

Recommended Execution Order:
Step 1 → Step 2 → Step 3 → Step 4


## Notes
- Do not skip steps based on perceived obviousness
- Do not reorder during execution without new evidence
- Record results per step before proceeding
```


## Prompt Rules

```id="p9c1k7"
You are generating an investigation execution plan from ranked incident hypotheses.

STRICT RULES:
- Convert each hypothesis into exactly one validation step
- Do not merge hypotheses into shared steps unless explicitly environmental
- Always include infrastructure/deploy/config change check
- Order by confidence, speed of validation, and system criticality
- Every step must include:
  - action
  - why it matters
  - confirms condition
  - rules-out condition
  - time estimate
- Do not assume outcomes
- Do not remove low-confidence hypotheses

Input hypotheses:
"""
{ranked_hypotheses}
"""
```


## Execution Discipline Rules

* Each step is atomic and independently verifiable
* No step may depend on the assumed outcome of another step
* Environmental checks are always separate, not embedded inside hypothesis checks
* Steps are executed in order unless new evidence explicitly invalidates sequence


## Quality Checklist

* Every hypothesis has a corresponding validation step
* Every step has explicit confirm and rule-out conditions
* Environmental changes are included as a mandatory step
* Steps are ordered by confidence and effort, not narrative flow
* No inference about outcomes is embedded in instructions
* Plan is executable without reinterpretation


## Key Principle

Investigation time is spent verifying reality, not deciding what to check next.

A good plan removes ambiguity before execution begins.
