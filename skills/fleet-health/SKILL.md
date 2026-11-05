---
name: fleet-health
description: Produce a fleet health report for an Applivery Workspace covering Devices that stopped checking in, outdated OS versions, missing encryption, Policies that failed to sync and Devices without an owner. Use when the user asks how the fleet is doing, wants a compliance snapshot, prepares an audit or a QBR, or asks which Devices need attention.
argument-hint: "[segment, platform or days since last check-in]"
---

# Fleet health

> Shared safety rules and the action catalogue are in [CONNECTORS.md](../../CONNECTORS.md). Follow them on every run.

## Workflow

1. **Scope.** State the Workspace. Read `$ARGUMENTS` for a Segment, platform (iOS, iPadOS, macOS, Android, Windows) or a check-in threshold. Default threshold: 7 days without check-in.
2. **Baseline.** Call *Get Workspace Stats* for totals and the platform split. The Device list can return a different total (duplicate enrollments of the same serial, enrollments that never completed). Report both numbers and explain the gap instead of picking one.
3. **Pull the Device list.** Use *List Devices* (or *Search Devices* with the scope filters). Page through all results. Record how many Devices you covered; if you could not cover all of them, say so and report on the covered set only.
4. **Score each finding** from the Device fields returned:
   - **Not reporting:** last check-in older than the threshold.
   - **OS behind:** OS version below the most common current version for that platform in this fleet. Do not invent vendor support dates; if the user wants them, cite them from a source.
   - **Not encrypted:** only when the Device data has an encryption field (for example a BitLocker or FileVault Smart Attribute). If it has none, list encryption under "Not checked". Never infer it.
   - **No owner:** no Device Employee assigned.
   - **Policy not in sync:** call *Get Policy Sync Status* for Policies assigned to the scope. Count a failure only when the result carries an explicit success or error field. If it returns only the composed configuration, list Policy sync under "Not checked".
   - **Compliance:** report the compliance flag as returned, but treat "Compliant" on a Device that is not reporting as stale and flag it. A Device silent for months is not evidence of compliance.
5. **Prioritise.** Rank by risk: not encrypted and not reporting first, then Policy sync failures, then OS behind, then no owner.
6. **Offer actions, do not take them.** Suggest next steps (for example *Sync Device* on stale Devices, `/device-investigate` on the worst ones, `/policy-change` for a fix). Run nothing that changes state unless the user asks, and then follow the safety rules.

## Output

```markdown
## Fleet health: [Workspace] as of [date time]
Scope: [segment/platform] | Devices covered: [n] of [total]

| Check | Devices | Share |
|---|---|---|
| Not reporting (> [d] days) | [n] | [%] |
| Not encrypted | [n] | [%] |
| OS behind | [n] | [%] |
| Policy not in sync | [n] | [%] |
| No owner | [n] | [%] |

### Fix first
1. [Device name] ([platform], last seen [date]): [issue] → [suggested action]

### Not checked
- [anything the tools did not return]
```
