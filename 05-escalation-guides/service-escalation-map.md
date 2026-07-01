# Service Escalation Map

Defines ownership for production systems to eliminate delay caused by unclear responsibility during incidents.

This file is used immediately after severity classification and before applying `escalation-matrix.md`.


## How to Use This

1. Identify affected service or system
2. Page primary owner immediately
3. Page backup owner in parallel (do not wait for primary response)
4. If no acknowledgment within escalation window → follow `escalation-matrix.md`
5. If ownership is unclear → escalate immediately and flag as a documentation gap


## Ownership Rules

- Primary owner = first responder and incident driver for that service
- Backup owner = parallel responder and failover support
- Platform Team = shared systems support (infra, edge, cross-service dependencies)

Backup owners are not passive — they should actively engage if paging occurs.


## Services

### Payment API

- Primary owner: Payments Team
- Backup owner: Platform Team
- Paging channel: `#payments-oncall` (Slack / paging alias)
- On-call system: PagerDuty / Opsgenie schedule


### Auth Service

- Primary owner: Identity Team
- Backup owner: Platform Team
- Paging channel: `#identity-oncall`
- On-call system: PagerDuty / Opsgenie schedule


### Database / Data Platform

- Primary owner: Database Team
- Backup owner: Infra Team
- Paging channel: `#db-oncall`
- On-call system: PagerDuty / Opsgenie schedule


### API Gateway / Edge

- Primary owner: Platform Team
- Backup owner: Infra Team
- Paging channel: `#platform-oncall`
- On-call system: PagerDuty / Opsgenie schedule


### Notifications (Email / SMS)

- Primary owner: Messaging Team
- Backup owner: Platform Team
- Paging channel: `#messaging-oncall`
- On-call system: PagerDuty / Opsgenie schedule


### Third-Party Integrations

- Primary owner: Integrations Team
- Backup owner: Platform Team
- Paging channel: `#integrations-oncall`
- On-call system: PagerDuty / Opsgenie schedule


### Customer-Facing Web / App

- Primary owner: Product Engineering Team
- Backup owner: Platform Team
- Paging channel: `#product-eng-oncall`
- On-call system: PagerDuty / Opsgenie schedule


## Missing Ownership Rule

If a service is not listed:

- Treat as **unknown ownership**
- Page Platform Team immediately
- Simultaneously escalate per `escalation-matrix.md`
- Log as a documentation gap in `incident-timeline.md`

Do not spend time investigating ownership during an active incident.


## Parallel Paging Rule

Primary and backup owners must be paged at the same time for SEV 1 and SEV 2 incidents.

Do not wait for acknowledgment from primary before paging backup.


## Incident Commander Override

During SEV 1 incidents:

- Incident Commander can reassign ownership dynamically
- Service ownership map is a starting point, not a constraint
- Coordination responsibility overrides static ownership mapping


## Keeping This File Accurate

Update when:

- Ownership of a service changes teams
- On-call rotations or paging systems change
- New production services are introduced
- Backup ownership changes


## Principle

> The fastest way to slow down an incident is uncertainty about who owns the problem.