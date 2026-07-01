# Functional Escalation Guide

Defines when to involve domain specialists based on symptoms, not organizational hierarchy.

This is separate from `escalation-matrix.md`, which governs timing and management escalation.

Functional escalation and management escalation happen in parallel.


## Guiding Principle

> If a domain might be responsible, involve that domain immediately.

Do not wait for confirmation before engaging specialists.

If uncertain, escalate anyway.


## Database Team

Engage immediately when symptoms suggest data-layer issues:

- Query latency increases without corresponding traffic spike (e.g., P95 latency doubles while RPS is flat)
- Replication lag that increases over time (not stabilizing)
- Connection pool exhaustion (e.g., "too many connections" errors)
- Lock contention or long-running transactions blocking reads/writes
- Data inconsistencies (duplicate rows, missing records, constraint violations)


## Infrastructure Team

Engage when symptoms suggest platform or system-level instability:

- CPU or memory saturation across multiple nodes or services
- Kubernetes issues (CrashLoopBackOff, failed scheduling, node pressure)
- Autoscaling not responding to increased load
- Internal network timeouts (service-to-service latency spikes)
- DNS failures or load balancer health check degradation
- TLS / certificate failures affecting service communication


## Security Team

Engage immediately when there is any plausible security signal.

Do not wait for confirmation.

- Spike in failed authentication attempts across users or endpoints
- Unusual traffic patterns (geo-spikes, single-source floods, bot-like behavior)
- Token misuse or session anomalies (invalid token reuse, session hijacking signals)
- Any indication of unauthorized access or data exposure
- Behavior inconsistent with normal user or system activity patterns

If Security is a possible factor, they must be involved immediately.


## Product Team

Engage when behavior may be intentional or customer-facing definition related:

- Uncertainty whether behavior is a bug or expected product behavior
- Feature flags or configuration changes may explain the incident
- Customer messaging requires product context or interpretation
- Contractual or UX expectations may affect communication decisions


## Third-Party / Vendor

Engage when external dependencies are suspected:

- Confirmed vendor outage via status page or multiple external reports
- Rate limiting or quota enforcement from external APIs
- Partial or degraded vendor performance impacting core flows

Actions:

- Open vendor support ticket immediately
- Record ticket ID in `incident-timeline.md`
- Continue internal escalation independently of vendor response time


## Boundary Rules

- Database team = data integrity, query execution, storage layer
- Infrastructure team = system platform, compute, networking, orchestration
- Security team = authentication, access control, data exposure risk
- Product team = intended behavior vs unexpected behavior ambiguity


## Interaction With Severity

- Functional escalation is independent of severity level
- A low-severity incident can still require Security involvement
- A high-severity incident may require multiple functional teams simultaneously


## Key Principle

> If you are deciding whether to escalate to a specialist, that decision itself is a reason to escalate.