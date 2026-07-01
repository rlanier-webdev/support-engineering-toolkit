# Escalation Guides

This section defines how incidents are escalated across teams, services, and functional domains.

Escalation is rule-based, not judgment-based. It ensures the right responders are engaged quickly and consistently under pressure.


## System Components

This module is composed of interconnected systems:

### Escalation Matrix
Severity-based escalation timing and paging rules  
→ `escalation-matrix.md`

### Service Ownership Map
Defines primary and backup ownership for all production systems  
→ `service-escalation-map.md`

### Technical Escalation Triggers
Metric-based severity classification rules  
→ `technical-escalation-triggers.md`

### Functional Escalation Guide
Domain-specific escalation rules (DB, infra, security, etc.)  
→ `functional-escalation-guide.md`

### After-Hours Escalation Rules
Behavioral adjustments outside business hours  
→ `after-hours-escalation.md`

### Escalation Playbooks
Predefined response patterns for common incident scenarios  
→ `escalation-playbooks.md`


## Escalation Principles

All escalation behavior follows these rules:

### 1. Time is deterministic
If a threshold is reached, escalation occurs immediately without review or delay.

### 2. Impact overrides hierarchy
Customer impact determines urgency, not team structure or ownership boundaries.

### 3. Signals override intuition
Metrics and system behavior take precedence over assumptions or anecdotal interpretation.

### 4. Ownership is explicit
Every system has a defined primary and backup owner. No ambiguity is acceptable during incidents.

### 5. Silence is a failure mode
Lack of acknowledgment or response is treated as a trigger for escalation.


## Operational Flow (Parallel Execution Model)

During an incident, these actions occur simultaneously:

### 1. Severity Classification
Use `incident-severity.md` to determine initial severity.

### 2. Ownership Resolution
Identify service owner via `service-escalation-map.md`.

### 3. Signal Evaluation
Apply `technical-escalation-triggers.md` to validate severity or detect escalation conditions.

### 4. Functional Engagement
Engage specialists immediately when symptom patterns match `functional-escalation-guide.md`.

### 5. Timing Enforcement
Apply escalation timing rules from `escalation-matrix.md` without delay.


## Source of Truth Hierarchy

If rules appear to conflict:

1. Technical Escalation Triggers (severity definition)
2. Escalation Matrix (timing and paging behavior)
3. Functional Escalation Guide (specialist engagement)
4. Service Ownership Map (assignment routing)
5. Playbooks (scenario guidance)
6. After-Hours Rules (context modifiers only)


## Common Failure Modes This Prevents

- Delayed escalation due to uncertainty
- Misrouted ownership during active incidents
- Over-reliance on individual judgment
- Sequential thinking during parallel systems failure
- Confusion during after-hours incidents
- Inconsistent escalation across teams


## Design Intent

This system exists to:

- Minimize time to effective response
- Remove ambiguity during high-pressure incidents
- Ensure consistent escalation behavior across all teams
- Enable parallel execution rather than sequential decision-making
- Make incident response predictable, auditable, and repeatable