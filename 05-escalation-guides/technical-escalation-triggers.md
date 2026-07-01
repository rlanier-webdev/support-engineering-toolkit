# Technical Escalation Triggers

Defines when to escalate based on measurable signals, not intuition or feelings.

Escalation timing here works alongside `escalation-matrix.md`. A trigger firing below should set the severity, which then determines the escalation chain and timing.


## Guiding Principle

> If a signal crosses a threshold, escalate. Do not wait to see if it self-corrects.

Escalating on a signal that turns out to be a false alarm costs a few minutes. Waiting on a real one costs customer impact.


## Escalate Immediately (Sev 1) If

- Error rate exceeds 5% for 5 consecutive minutes
- Full service outage or complete loss of a core function
- Database CPU exceeds 90%, sustained for 10 minutes
- Multiple services are degraded simultaneously
- No clear root cause identified within 15 minutes (see "Unknown Cause Rule" below)


## Escalate as Sev 2 If

- Error rate exceeds 2% for 10 consecutive minutes
- p95 latency exceeds 2x baseline for 10 minutes
- A single dependency or downstream service is degraded but the core system is still functioning
- Saturation signals (CPU, memory, connection pool, queue depth) exceed 80% sustained for 15 minutes


## Metric Categories

### Error Rate Triggers
- Track 4xx vs 5xx separately — 5xx spikes are a stronger signal than 4xx spikes
- A sudden change in error rate matters more than the absolute number if it's a sharp deviation from baseline

### Latency Triggers
- Compare against rolling baseline, not a fixed number — "normal" latency varies by time of day and load
- Escalate when p95/p99 latency crosses 2x baseline, not just when it "feels slow"

### Saturation Signals
- CPU, memory, disk I/O, connection pool exhaustion, thread pool exhaustion
- Escalate when sustained above 80–90% for the stated window, not on a single spike

### Replication / Data Lag
- Escalate if replication lag grows continuously rather than plateauing
- Escalate immediately if lag affects read-after-write consistency for customer-facing data


## The Unknown Cause Rule

This is the trigger most teams skip, and the one that matters most.

> If there is no clear root cause hypothesis within 15 minutes of investigation, escalate automatically — regardless of current severity.

Not knowing the cause is itself a risk signal. It means the blast radius is unknown, which means the incident could be worse than it currently looks. Escalating here brings in more eyes before the situation gets harder to unwind, not after.


## What Not to Do

- Do not wait for a second data point once a documented threshold is crossed
- Do not downgrade severity because "it looks like it's stabilizing" — confirm the trend for a full observation window first
- Do not treat "no customers have complained yet" as a reason to hold off — trailing indicators lag actual impact
