---
name: policy-change
description: Plan and apply a change to an Applivery Policy, Segment, Device Audience or Smart Attribute safely by reading the current configuration, previewing exactly which Devices are affected, proposing a staged rollout, applying with confirmation and checking sync status afterwards. Use when someone wants to create or edit a Policy, change a restriction, move Devices between Segments, build an audience, or asks what a change would affect.
argument-hint: "<what you want to change>"
---

# Safe policy change

> Shared safety rules and the action catalogue are in [CONNECTORS.md](../../CONNECTORS.md). Follow them on every run.

Most fleet incidents come from a correct change applied to the wrong set of Devices. This skill makes the blast radius visible before anything moves.

## Workflow

1. **Restate the change** in one sentence and confirm it with the user.
2. **Read the current state.** *Get Policy Detail* and *Get Policy Composition* for the Policy, *Get Policy Assignations* for where it applies, *Get Segment Tree* and *Get Segment Detail* for the hierarchy. For a new Policy, check *List Policy Templates* first. Cite the relevant Applivery Docs page for the setting.
3. **Preview the impact.** Use *Preview Device Audience*, *Preview User Audience* or *Preview Segment Permission* when the change targets an audience or permission. Otherwise derive the affected Devices from the assignations. Report the count and a sample of names, broken down by platform.
4. **Flag risks.** Settings that can lock users out (passcode, kiosk, network, certificates, OS updates), conflicts with other Policies in the composition, and Devices that are offline and will apply the change later.
5. **Propose a rollout.** Default: a small pilot (a test Segment or audience), then the rest. Show the plan.
6. **Apply with confirmation.** Run *Create Policy*, *Update Policy*, *Manage Policy Apps*, *Manage Policy Scripts*, *Move Device to Segment* or the audience action only after the user confirms the exact change and target.
7. **Verify.** *Get Policy Sync Status* after applying. Report synced, pending and failed counts as observed, and offer `/device-investigate` for failures.

## Output

```markdown
## Change: [one sentence]
Target: [Policy/Segment/Audience] | Devices affected: [n] ([platform split])
Risks: [list]
Rollout: 1) pilot [n Devices] 2) rest [n]

Before → After
| Setting | Before | After |
|---|---|---|

Confirm to apply step 1.
```
