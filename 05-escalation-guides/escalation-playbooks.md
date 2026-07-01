# Escalation Playbooks

Step-by-step escalation patterns for common incident scenarios.

These are operational guides, not strict scripts. If a situation diverges, default to:
- `escalation-matrix.md`
- `technical-escalation-triggers.md`
- `functional-escalation-guide.md`

Those are the source of truth.


## Usage Principle

Playbooks are meant to accelerate response, not replace judgment.

In all cases:
- Assume highest plausible severity until confirmed otherwise
- Execute escalation and investigation in parallel, not sequentially
- Follow escalation rules exactly as defined in `escalation-matrix.md`


## Playbook: Payment Outage

### Initial Actions (Parallel)

- Classify as SEV 1 (payment failure = critical by default)
- Page Payments on-call (`service-escalation-map.md`)
- Start incident timeline logging (`incident-timeline.md`)
- Begin customer impact assessment


### Escalation Flow

- At 10 minutes no acknowledgment → escalate to team lead
- At 30 minutes no mitigation progress → escalate to engineering manager
- At 60 minutes unresolved → escalate to VP Engineering + customer-facing leadership

(All timing governed by `escalation-matrix.md`)


### Investigation

- If root cause unclear after 15 minutes → invoke Unknown Cause escalation rule
- If third-party dependency suspected → immediately involve Platform + vendor support
- Record vendor ticket in timeline immediately


### Communication

- Start customer communication within 15 minutes using `communication-templates.md`
- Avoid vendor attribution until confirmed
- Maintain update cadence per severity rules


## Playbook: Database Overload

### Initial Actions (Parallel)

- Validate trigger against `technical-escalation-triggers.md`
- Assume SEV 1 if customer impact exists
- Page Database on-call (`service-escalation-map.md`)
- Start timeline logging


### Escalation

- Apply standard escalation matrix based on confirmed severity
- If multi-node or systemic → immediately involve Infra team


### Investigation Paths

- Query saturation → DB team lead ownership
- Infrastructure bottleneck → Infra escalation
- Unknown cause after 15 minutes → escalate per matrix rules


## Playbook: Third-Party API Failure

### Initial Actions

- Confirm external dependency failure (do not assume immediately)
- Classify severity based on customer impact (assume SEV 1 if core flow blocked)
- Page owning service team
- Engage vendor support immediately


### Escalation Rules

- Follow `escalation-matrix.md` regardless of vendor status
- Vendor delay does NOT reduce internal escalation urgency
- Maintain internal communication cadence independently


### Communication

- Inform customers using approved templates
- Do not assign blame until root cause confirmed
- Clearly state impact and mitigation path


## Playbook: Suspected Security Incident

### Critical Rule

Security escalation is immediate and bypasses normal severity evaluation.


### Initial Actions (Parallel)

- Page Security team immediately
- Preserve logs and system state
- Begin timeline logging
- Assume SEV 1 until downgraded by Security


### Handling Rules

- Do not remediate or modify systems before Security review
- Follow Security instructions for containment
- Limit external communication until guided


## Playbook: Multi-Service Degradation

### Immediate Classification

- Automatically SEV 1 per `technical-escalation-triggers.md`


### Initial Actions (Parallel)

- Page all affected service owners
- Engage Infra team immediately
- Assign incident commander
- Start timeline logging


### Coordination

- Incident commander coordinates cross-team actions
- Avoid parallel conflicting remediation attempts
- Focus on shared dependency analysis (DNS, infra, auth, deploy pipeline)


## Incident Command Requirement

For any SEV 1 incident involving multiple teams:

- A single incident commander must be assigned within 10 minutes
- All updates flow through that role
- Coordination responsibility is not optional


## Key Principle

> Escalation is not a sequence of steps. It is a set of parallel actions triggered by conditions.