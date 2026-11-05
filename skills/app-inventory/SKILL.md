---
name: app-inventory
description: Review installed apps and app usage on Applivery-managed Devices, find unapproved or outdated apps, and install or uninstall apps with confirmation. Use when someone asks what is installed on a device or a group, looks for shadow IT, wants to know whether an app is used before renewing a licence, or asks to push or remove an app.
argument-hint: "<app name, device or segment>"
---

# App inventory

> Shared safety rules and the action catalogue are in [CONNECTORS.md](../../CONNECTORS.md). Follow them on every run.

## Workflow

1. **Scope.** One Device, a Segment, or the whole Workspace. For more than about 50 Devices, agree a sample or a Segment first, because app lists are read per Device.
2. **Read.** For each Device in scope: *Get Device Apps*, and *Get Device App Usage* when the question is about usage. Record how many Devices you covered.
3. **Compare.** Against the apps the Policies deliver (*Get Policy Detail*, *Get Policy Composition*) and any approved list the user provides. Mark apps as: delivered by Policy, installed outside Policy, or missing.
4. **Report usage carefully.** State the usage window the tool returned. Do not infer "unused" from missing data.
5. **Act with confirmation.** *Install App on Device* or *Uninstall App from Device*, or a Policy change through `/policy-change` when many Devices are involved. Verify with *Get Device Apps* afterwards.

## Output

```markdown
## Apps: [scope] as of [time]
Devices covered: [n] of [total]

| App | Version(s) | Devices | Delivered by Policy | Usage ([window]) |
|---|---|---|---|---|

Outside Policy: [list]
Missing where expected: [list]
```
