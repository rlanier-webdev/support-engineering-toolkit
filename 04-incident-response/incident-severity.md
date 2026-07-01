# Incident Severity Guide

Use this guide to classify incidents based on **customer and business impact**, ensuring a consistent response and escalation process.


## Purpose

Not every issue is an incident, and not every incident is critical.

This guide provides a standardized framework for determining incident severity based on impact rather than technical complexity. Consistent classification helps teams prioritize work, coordinate response efforts, and communicate effectively with stakeholders.


## Guiding Principle

> Severity should reflect **customer and business impact**, not the technical difficulty of resolving the issue.

A simple configuration error causing a production outage is more severe than a complex software bug affecting a single user.


# Severity 1 (Critical)

## Definition

A critical incident causing widespread service disruption or complete loss of a core business function.

## Business Impact

- Production service unavailable
- Multiple customers or tenants affected
- Critical business operations blocked
- Significant financial or contractual impact
- No viable workaround exists

## Common Examples

- Complete production outage
- Authentication service unavailable
- Database outage
- Payment processing failure
- Major infrastructure failure

## Immediate Response

- Declare an incident
- Notify the incident owner or on-call team
- Begin an incident timeline
- Engage required technical teams
- Provide regular stakeholder updates

## Questions to Ask

- Is production unavailable?
- Are multiple customers impacted?
- Is there data loss or corruption?
- Is business-critical functionality unavailable?
- Is there a viable workaround?


# Severity 2 (High)

## Definition

A significant service disruption affecting important functionality but not resulting in a complete outage.

## Business Impact

- Core functionality degraded
- Multiple users impacted
- Limited workaround available
- Elevated business risk
- Customer operations partially blocked

## Common Examples

- API failures for a major feature
- Significant performance degradation
- Integration failures
- Partial service outage
- High error rates

## Response

- Assign high priority investigation
- Notify appropriate stakeholders
- Coordinate technical response
- Monitor customer impact
- Provide regular status updates

## Questions to Ask

- Is customer productivity significantly affected?
- Is the issue widespread?
- Is performance degraded?
- Can customers continue working with limitations?
- Does this require cross-team coordination?


# Severity 3 (Medium)

## Definition

A functional issue with limited customer impact where acceptable workarounds are available.

## Business Impact

- Limited customer impact
- Individual features affected
- Workaround available
- No immediate business risk

## Common Examples

- Feature-specific defects
- Individual customer issues
- Moderate performance degradation
- Configuration problems
- Reporting discrepancies

## Response

- Prioritize investigation
- Assign ownership
- Track progress
- Communicate status as needed

## Questions to Ask

- Is the issue isolated?
- Can the customer continue working?
- Does a documented workaround exist?
- Is business impact limited?


# Severity 4 (Low)

## Definition

A low-impact issue with minimal operational risk that can be addressed through normal development or maintenance processes.

## Business Impact

- Minimal or no customer impact
- Cosmetic or usability issue
- Documentation improvement
- Enhancement request
- Routine maintenance

## Common Examples

- UI formatting issues
- Documentation corrections
- Minor visual defects
- Non-blocking usability improvements
- Low-priority enhancements

## Response

- Document the issue
- Schedule for future work
- Track through normal backlog processes

## Questions to Ask

- Does this impact functionality?
- Is the issue purely cosmetic?
- Can it wait for a future release?
- Is there any measurable customer impact?


# Severity Assessment Checklist

Before assigning a severity, consider the following:

- How many customers are affected?
- Is production impacted?
- Is there a workaround?
- Is data integrity at risk?
- Are critical business processes blocked?
- Is customer impact increasing?
- Does the issue require immediate cross-team coordination?


# Escalation Guidelines

Escalate when:

- Customer impact increases
- Additional services become affected
- A workaround is no longer available
- Data integrity is at risk
- Incident scope expands beyond the original assessment

Severity should be re-evaluated throughout the investigation as new information becomes available.


# Key Principle

> Classify incidents based on **impact**, communicate clearly, and adjust severity as the situation evolves.

Accurate severity assessment enables faster response, better coordination, and more effective incident management.