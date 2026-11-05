---
name: it-weekly-digest
description: Write a weekly digest of an Applivery Workspace for an IT lead or management covering fleet size and health changes, notable changes from the audit log, automation rule results, incidents and recommended next steps. Use when someone asks for a weekly or monthly IT summary, a status update for leadership, or a fleet report for a meeting.
argument-hint: "[period, default last 7 days] [audience]"
---

# IT weekly digest

> Shared safety rules and the action catalogue are in [CONNECTORS.md](../../CONNECTORS.md). Follow them on every run.

This skill is read-only.

## Workflow

1. **Period and audience.** Default: last 7 days, for the IT lead. For management, shorten to outcomes and risks.
2. **Gather.** *Get Workspace Stats*; the fleet health checks from `/fleet-health` on the current state; *Get Audit Log* for the period (Policy changes, wipes, disenrollments, access changes); *List Automation Rules* and *Get Automation Rule Logs* for what ran and what failed.
3. **Compare with last period** only if the user provides the previous digest or figures. Do not invent trends.
4. **Write the digest.** Lead with the three things that matter most. Every number names its source.

## Output

```markdown
# IT digest: [Workspace], [from–to]

**Top 3**
1. ...

| Metric | Value | Source |
|---|---|---|
| Devices enrolled | | Workspace stats |
| Not reporting > 7 days | | Device list |
| Not encrypted | | Device list |
| Policy changes | | Audit log |
| Automation failures | | Rule logs |

**Changes this period:** ...
**Risks:** ...
**Recommended next steps:** ...
**Not checked:** ...
```
