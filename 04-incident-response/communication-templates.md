# Communication Templates

Use these templates to provide clear, consistent updates during incident response.

The goal is to communicate what is known, what is being done, and what stakeholders should expect next.


# Communication Principles

During an incident:

- Communicate facts, not assumptions.
- Keep updates concise and actionable.
- Avoid assigning blame.
- Clearly separate confirmed information from ongoing investigation.
- Update stakeholders whenever meaningful information becomes available.


# Internal – Incident Acknowledged

**Subject**

```
[SERVICE] Incident | SEV[Level] | Investigation Started
```

**Message**

```
An incident has been identified affecting [SERVICE].

Status
- Investigating

Impact
- [Brief description of customer or business impact]

Current Actions
- Initial investigation in progress
- Relevant teams have been engaged

Next Update
- Additional information will be shared as it becomes available.
```


# Internal – Investigation Update

**Subject**

```
[SERVICE] Incident Update | Investigation Ongoing
```

**Message**

```
Current Status
- Investigation continues.

Findings
- [Confirmed observations]

Impact
- [Updated customer or system impact]

Current Actions
- [Actions currently being performed]

Risks
- [Known risks, if any]

Next Update
- Following significant progress or change in status.
```


# Internal – Root Cause Identified

**Subject**

```
[SERVICE] Incident Update | Root Cause Identified
```

**Message**

```
Root Cause

[Concise explanation of the confirmed cause.]

Current Actions

- Implementing mitigation
- Validating recovery
- Monitoring affected systems

Estimated Recovery

[If known]
```


# Internal – Incident Resolved

**Subject**

```
[SERVICE] Incident Resolved
```

**Message**

```
The incident affecting [SERVICE] has been resolved.

Summary

- Start Time:
- End Time:
- Duration:
- Customer Impact:

Root Cause

[Short summary]

Resolution

[What restored service]

Next Steps

A post-incident review will capture lessons learned and improvement opportunities.
```


# External – Service Disruption

```
We are aware of an issue affecting [SERVICE].

Our team is actively investigating and working to restore normal service.

Current Impact

[Brief customer-friendly description]

We will provide additional updates as more information becomes available.
```


# External – Service Restored

```
The issue affecting [SERVICE] has been resolved, and normal service has been restored.

Summary

- Service Restored:
- Customer Impact:
- Resolution:

We appreciate your patience while we worked to resolve the issue.
```


# Communication Checklist

Before sending an update, verify:

- Information is confirmed
- Customer impact is accurately described
- Current status is clear
- Next steps are communicated
- Technical jargon is appropriate for the audience


# Key Principle

> Good incident communication reduces uncertainty by explaining what is known, what is being done, and what comes next.