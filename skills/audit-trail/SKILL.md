---
name: audit-trail
description: Investigate the Applivery audit log to answer who did what, when and on which Device, Policy, Segment or setting, and build a timeline. Use when someone asks who changed a policy, why a device was wiped or moved, what happened during an incident, or needs evidence for a security or compliance review.
argument-hint: "<object, person or time window>"
---

# Audit trail

> Shared safety rules and the action catalogue are in [CONNECTORS.md](../../CONNECTORS.md). Follow them on every run.

This skill is read-only.

## Workflow

1. **Frame the question.** Object (Device, Policy, Segment, user), actor, and time window. Default window: the last 7 days. Ask if the object is ambiguous.
2. **Query.** *Get Audit Log* with the filters available, then *Get Audit Entry Detail* for entries that matter. For automation, also check *List Automation Rules* and *Get Automation Rule Logs*, because a rule can act without a person.
3. **Build the timeline** in time order, with actor (person, automation rule or system), action, target and source of each line.
4. **Answer the question directly** in the first line, then show the evidence. If the log does not cover the window or the object, say so; do not fill gaps with assumptions.

## Output

```markdown
**Answer:** [who did what, when]

| Time | Actor | Action | Target | Entry |
|---|---|---|---|---|

Window searched: [from–to] | Entries reviewed: [n]
Not covered: [gaps]
```
