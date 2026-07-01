# Post-Incident Review

**Incident ID:** [YYYYMMDD-###]
**Review Date:** [YYYY-MM-DD]
**Facilitator:** [Name]
**Participants:** [Names + Roles]


## Summary

**What happened:**
[Concise, factual summary of the incident]

**Impact:**
[Who/what was affected and how]

**Root Cause (1 sentence):**
[Direct cause without context or narrative]


## Key Metrics

- **Duration:** [Xh Ym]
- **Severity:** [SEV 1–4]
- **Detection Time:** [Time to detect]
- **Time to Mitigation:** [Time to mitigate]
- **Time to Recovery:** [Time to full recovery]


## Timeline Highlights

See: `incident-timeline.md`

- **Detected:** [Time] – [how it was detected]
- **Acknowledged:** [Time]
- **Mitigation Started:** [Time]
- **Resolved:** [Time]


## Root Cause Analysis

### Direct Cause
[Immediate technical cause of failure]

### Systemic Cause
[Deeper system/design/process failure that allowed it]

### Contributing Factors
- [Factor 1]
- [Factor 2]
- [Factor 3]


## Impact

- **Services Affected:** [List + duration]
- **User Impact:** [Count, %, or qualitative description]
- **Revenue Impact:** [If applicable]
- **Data Integrity:** [OK / Risk / Loss + details]
- **SLO Impact:** [Which SLOs were breached]


## Response Evaluation

### What Worked
- [Effective detection, mitigation, communication, etc.]

### What Slowed Us Down
- [Operational friction points]

### Detection Gaps
- [Why we didn’t catch it earlier]

### Response Gaps
- [Why mitigation wasn’t faster]


## Action Items

| Action | Type | Owner | Priority | Due Date |
|------|------|------|----------|----------|
| [Fix recurrence issue] | Prevention | [Name] | High | [Date] |
| [Improve alerting] | Detection | [Name] | High | [Date] |
| [Update runbook] | Response | [Name] | Medium | [Date] |


## Prevention Plan

**Controls to implement:**

1. [Engineering fix]
2. [Monitoring improvement]
3. [Process improvement]
4. [Documentation/training update]


## Linked Artifacts

- Timeline: `incident-timeline.md`
- Lessons: `lessons/INC-YYYYMMDD-###.md`
- Runbooks affected: [links]
- Alerts impacted: [links]
- GitHub issues: [links]


## Lessons Captured

- [DET-XXX] Detection lesson summary
- [RESP-XXX] Response lesson summary
- [PRE-XXX] Prevention lesson summary


## Sign-Off

- [ ] Root cause agreed by team
- [ ] Impact validated
- [ ] Action items assigned with owners
- [ ] Lessons captured in registry
- [ ] Stakeholders notified

**Approved by:** [Name]
**Date:** [Date]