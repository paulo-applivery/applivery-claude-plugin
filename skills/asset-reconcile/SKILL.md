---
name: asset-reconcile
description: Reconcile Applivery inventory items (non-managed assets) with enrolled Devices, find assets with no matching Device and Devices with no asset record, and link or update them with confirmation. Use when someone prepares an asset audit, a hardware refresh, an insurance or finance count, or asks whether the asset register matches the MDM.
argument-hint: "[segment or asset type]"
---

# Asset reconciliation

> Shared safety rules and the action catalogue are in [CONNECTORS.md](../../CONNECTORS.md). Follow them on every run.

## Workflow

1. **Pull both sides.** *List Inventory Items* (or *Search Inventory Items* for a type) and *List Devices*. Page through everything and record the counts.
2. **Match** by serial number first, then by exact name. Never match on similar names alone; list those as "possible match" for the user to decide.
3. **Classify:** linked; asset with no Device; Device with no asset; possible match.
4. **Fix with confirmation.** *Link Inventory Item to MDM Device* for confirmed matches, *Create Inventory Item* for Devices without a record, *Add Note to Inventory Item* for assets that need follow-up. Show the list first.
5. **Report** the before and after counts.

## Output

```markdown
## Asset reconciliation as of [time]
Inventory items: [n] | Devices: [n]

| Status | Count |
|---|---|
| Linked | |
| Asset, no Device | |
| Device, no asset | |
| Possible match | |

Proposed links: [list]. Confirm to apply.
```
