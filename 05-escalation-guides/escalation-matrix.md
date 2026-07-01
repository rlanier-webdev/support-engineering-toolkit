# Escalation Matrix

Defines who is contacted, when, and why during an active incident.

This is the authoritative source for escalation timing and escalation chains.

Severity definitions are defined in `04-incident-response/incident-severity.md`.


## Guiding Principle

> Escalation is time-driven, not judgment-driven.

If a threshold is met, escalate immediately. Do not wait for confirmation, resolution, or additional signals.


## Severity 1 (Critical)

- Page on-call engineer immediately
- If no acknowledgment within **10 minutes** → escalate to next escalation tier (team lead)
- If no mitigation progress within **30 minutes** → escalate to engineering manager
- If no mitigation progress within **60 minutes** → escalate to director/VP engineering + notify customer-facing leadership
- Customer communication begins within 15 minutes (see `communication-templates.md`)


## Severity 2 (High)

- Page on-call engineer immediately
- If no acknowledgment within **20 minutes** → escalate to next escalation tier (team lead)
- If no active mitigation within **60 minutes** → escalate to engineering manager
- If impact expands or degrades → reclassify severity and reapply this matrix at the new level


## Severity 3 (Medium)

- No paging by default
- Assign ownership via normal on-call or ticketing workflow
- Escalate to team lead if unowned after one business day or if impact increases


## Severity 4 (Low)

- No paging
- Track in backlog
- Escalate only if later reclassified due to increased impact or risk


## Escalation Rules (Universal)

These rules apply to all severities during an active incident:

| Condition | Action |
|----------|--------|
| No acknowledgment within threshold | Escalate to next escalation tier |
| No mitigation state change within threshold | Escalate regardless of current activity |
| Scope or impact increases | Reclassify severity immediately and reapply this matrix |
| Owner unreachable | Escalate immediately to next tier without retry delay |


## Functional Escalation (Specialists)

Severity defines urgency. It does not define technical expertise required.

Use:

- `service-escalation-map.md` → identify system owners
- `functional-escalation-guide.md` → bring in domain specialists (DB, infra, security, etc.)

Specialists should be engaged immediately when their signal domain is suspected, not after escalation thresholds are reached.


## After-Hours Behavior

Escalation rules do not change outside business hours.

See `after-hours-escalation.md` for operational adjustments during overnight and weekend incidents.


## Escalation Flow Summary

1. Page on-call engineer
2. Wait only for acknowledgment window (severity-defined)
3. Escalate to next tier if no acknowledgment
4. Escalate leadership if mitigation thresholds are breached
5. Engage specialists in parallel when signals require it
6. Reclassify severity if impact changes


## Key Principle

> Time without acknowledgment or mitigation is itself a failure state requiring escalation.