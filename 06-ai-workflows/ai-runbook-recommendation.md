# AI Runbook Recommendation

Recommend the most relevant operational runbooks based on observed incident signals, allowing engineers to move from diagnosis to execution more quickly.

> **This workflow recommends existing runbooks—it does not execute them.**
>
> Every recommendation should be validated by an engineer before following operational procedures.


## Purpose

Many production incidents resemble problems that have already been documented.

The challenge is rarely missing documentation—it's locating the correct runbook while responding to an active incident.

This workflow analyzes structured incident signals and recommends the most relevant operational runbooks based on symptom similarity and documented trigger conditions.


## Objectives

This workflow helps engineers:

- Locate relevant runbooks quickly
- Reduce manual searching during incidents
- Recommend multiple possible operational procedures
- Explain why each recommendation was made
- Identify incidents that have no documented operational guidance


## Inputs

Structured outputs from previous investigation workflows, including:

- Ticket triage summary
- Log summary
- Root cause hypotheses
- Service names
- Error patterns
- Existing runbook library


## Workflow

### Step 1 — Collect Incident Signals

Gather structured information from earlier investigation stages.

Examples:

- affected services
- observed symptoms
- error messages
- monitoring alerts
- deployment events


### Step 2 — Compare Against Runbook Library

Evaluate each runbook based on:

- trigger conditions
- affected systems
- symptom similarity
- failure signatures
- historical usage


### Step 3 — Rank Recommendations

Generate a ranked list of candidate runbooks.

Each recommendation should include:

- confidence level
- matching symptoms
- reasons for recommendation
- sections most relevant to the current incident


### Step 4 — Handle No Match

If no suitable runbook exists:

- state that no strong match was found
- avoid forcing a recommendation
- suggest documenting the incident for future runbook creation if appropriate


## Example Output

```text
RUNBOOK RECOMMENDATIONS

Recommendation 1

Runbook:
Database Connection Pool Exhaustion

Confidence:
High

Matching Signals

• Database timeout pattern
• Replica fallback observed
• Error timeline aligns with documented trigger conditions

Relevant Sections

• Initial validation
• Connection pool diagnostics
• Recovery procedure
-----------------------------------------------

Recommendation 2

Runbook:
Database Primary Failover

Confidence:
Low

Matching Signals

• Database dependency involved

Reason for Lower Confidence

Current symptoms indicate connection exhaustion rather than failover.
-----------------------------------------------

No Additional Matches

No other runbooks exceeded the minimum confidence threshold.
```


## Recommendation Guidelines

### High Confidence

- Multiple trigger conditions match
- Affected services align
- Failure signature closely resembles documented behavior


### Medium Confidence

- Several symptoms match
- Some investigation is still required before execution


### Low Confidence

- Limited symptom overlap
- Similar technology but different failure pattern


### No Match

No existing runbook sufficiently matches the observed incident.

This is a valid outcome and may indicate:

- a new failure pattern
- incomplete documentation
- a missing operational procedure


## Rules

Always:

- Recommend only existing runbooks
- Explain why each recommendation was made
- Rank recommendations by confidence
- Highlight relevant sections within each runbook

Never:

- Invent runbooks
- Force a recommendation
- Execute operational steps
- Assume the recommendation is correct


## Quality Checklist

- Every recommendation references an existing runbook
- Matching criteria are explained
- Confidence reflects observable evidence
- No-match scenarios are handled explicitly
- Relevant runbook sections are identified


## Related Workflows

- `ai-ticket-triage.md`
- `ai-log-summarization.md`
- `ai-root-cause-hypothesis-generator.md`
- `ai-investigation-plan-generator.md`


## Key Principle

> Engineers should spend their time resolving incidents—not searching for documentation.

Finding the right runbook quickly is often the difference between a 10-minute incident and a 60-minute incident.