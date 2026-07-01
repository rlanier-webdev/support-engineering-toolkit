# After-Hours Escalation

This document defines what changes (and what does not change) during after-hours incidents.

Its purpose is to remove hesitation during low-staff periods. Most after-hours failures are caused by delayed escalation, not incorrect escalation.


## Guiding Principle

> Customer impact is not time-bound. Escalation rules are not time-bound.

All escalation rules defined in `escalation-matrix.md` remain fully active outside business hours.

A SEV 1 at 03:00 follows the same escalation timing as a SEV 1 at 15:00.


## Non-Negotiable Rules

These rules always apply, regardless of time of day:

- Page primary on-call immediately for all SEV 1 and SEV 2 incidents
- Do not delay escalation due to time of day, holidays, or staffing concerns
- If customer impact is active, escalate according to standard severity rules
- If no acknowledgment occurs within defined thresholds, escalate automatically
- Waking someone is an acceptable and expected action for SEV 1 and SEV 2 incidents


## Escalation Timers (After-Hours)

After-hours does not modify escalation thresholds:

- SEV 1: escalate if no acknowledgment within 10–15 minutes
- SEV 1: escalate leadership if no mitigation progress within 30–60 minutes
- SEV 2: escalate if no acknowledgment within ~20 minutes

(See `escalation-matrix.md` for exact timing rules.)


## Secondary On-Call Escalation

Escalate to secondary on-call when:

- Primary on-call does not acknowledge within 15 minutes
- Primary on-call is unreachable after repeated paging attempts
- Additional expertise is required and primary requests help

Do not delay escalation while waiting for a “convenient time” response.


## Leadership Escalation Overnight

Escalate to engineering leadership (manager/director) when:

- SEV 1 is not mitigated within 30–60 minutes
- Customer communication decisions require approval or coordination
- Public-facing updates (status page, customer notifications) are required
- Incident scope expands beyond a single team or system

Leadership escalation is expected, not exceptional, during SEV 1 incidents.


## What Changes After Hours

Only the following adjustments are expected:

### 1. Response latency
- Slight delays due to wake-up time are expected
- This does not change escalation rules

### 2. Communication channels
- Customer updates may shift toward asynchronous channels (status page, email)
- Internal communication remains real-time (paging, chat, calls)

### 3. Non-critical incidents
- SEV 3–4 incidents may be deferred or summarized until business hours
- SEV 1–2 incidents are never deferred


## What Does NOT Change

- Escalation thresholds
- Severity definitions
- Ownership responsibilities
- Requirement to page on-call engineers
- Requirement to involve leadership when thresholds are met


## Common Failure Modes This Prevents

- “Let’s wait until morning”
- Delayed paging due to uncertainty or politeness bias
- Under-escalation during low-staff hours
- Over-reliance on a single engineer overnight
- Assuming reduced visibility means reduced urgency


## Core Principle

> If it is worth waking someone up, it is worth escalating immediately.

This document exists to ensure that decision is never deferred or avoided.