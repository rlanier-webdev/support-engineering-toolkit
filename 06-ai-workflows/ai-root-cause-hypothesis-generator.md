# AI Root Cause Hypothesis Generator

Generate evidence-based investigation hypotheses that help engineers prioritize where to begin troubleshooting during an active incident.

> **This workflow does not determine root cause.**
>
> It generates ranked hypotheses based on observed signals. Every hypothesis must be validated through investigation before it can be considered a confirmed root cause.


## Purpose

When an incident begins, engineers are often faced with multiple possible explanations and limited evidence.

This workflow analyzes structured incident signals to identify the most probable failure domains, reducing the time spent deciding where to begin the investigation.

The goal is to prioritize investigative effort—not replace it.


## Objectives

This workflow helps engineers:

- Generate evidence-based investigation hypotheses
- Prioritize likely failure domains
- Correlate signals across multiple systems
- Reduce investigation time
- Identify weak or contradictory evidence
- Provide clear next investigative steps


## Inputs

Structured outputs from earlier workflows, including:

- Ticket triage summary
- Log summary
- Monitoring alerts
- Infrastructure events
- Deployment history
- Related historical incidents (if available)


## Workflow

### Step 1 — Collect Signals

Gather structured observations from available sources.

Examples:

- application logs
- infrastructure alerts
- customer reports
- monitoring systems
- deployment records


### Step 2 — Identify Failure Domains

Map observed symptoms to likely system components.

Examples include:

- Database
- API
- Authentication
- Infrastructure
- Networking
- Third-party integrations
- Application logic


### Step 3 — Correlate Evidence

Evaluate:

- timing relationships
- affected services
- dependency chains
- error frequency
- historical similarity

Contradictory evidence should reduce confidence—not be ignored.


### Step 4 — Rank Hypotheses

Produce a prioritized list based on available evidence.

Each hypothesis should include:

- confidence level
- supporting evidence
- conflicting evidence (if any)
- recommended investigation steps


## Example Output

```text
ROOT CAUSE HYPOTHESES

Hypothesis 1

Failure Domain:
Database Connectivity

Confidence:
High

Supporting Evidence

• 412 connection timeout events
• Replica failover observed
• Timeline matches incident start

Conflicting Evidence

None observed.

Suggested Investigation

• Check database health
• Review connection pool utilization
• Inspect recent infrastructure changes

Status

Hypothesis only—not confirmed.
-----------------------------------------------

Hypothesis 2

Failure Domain:
Application Connection Pool

Confidence:
Medium

Supporting Evidence

• Timeouts without outright connection failures
• Elevated request latency

Conflicting Evidence

No direct pool metrics available.

Suggested Investigation

• Review connection pool metrics
• Inspect recent application deployments

Status

Hypothesis only—not confirmed.
```


## Confidence Guidelines

### High

Multiple independent signals support the hypothesis.

Examples:

- logs
- monitoring
- deployment timing
- historical matches


### Medium

Evidence supports the hypothesis but important validation is still missing.


### Low

Limited or weak evidence.

Should remain a secondary investigation path.


## Rules

Always:

- Explain why each hypothesis was generated
- Cite supporting evidence
- Include conflicting evidence when present
- Recommend a concrete next investigation step
- State confidence explicitly

Never:

- Present a hypothesis as fact
- Ignore contradictory observations
- Recommend customer communication based on AI output alone
- Skip investigation


## Quality Checklist

- Every hypothesis references observable evidence
- Confidence reflects available evidence
- Contradictory signals reduce confidence
- Next investigation steps are actionable
- No hypothesis is presented as a confirmed root cause


## Related Workflows

- `ai-ticket-triage.md`
- `ai-log-summarization.md`
- `ai-investigation-plan-generator.md`
- `ai-learning-feedback-loop.md`


## Key Principle

> AI reduces the search space—it does not determine the answer.

A hypothesis becomes a root cause only after it has been verified through investigation and supported by evidence.