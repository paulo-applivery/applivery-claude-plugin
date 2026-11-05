---
name: employee-offboarding
description: Offboard a leaver in Applivery by listing every Device and inventory item assigned to them, recording state, and running the agreed return, lock, wipe or disenroll plan with confirmation per Device. Use when someone leaves the company, a contract ends, or IT asks what equipment a person still has.
argument-hint: "<person name or email> [last day]"
---

# Employee offboarding

> Shared safety rules and the action catalogue are in [CONNECTORS.md](../../CONNECTORS.md). Follow them on every run.

## Workflow

1. **Find the person.** *List Device Employees* or *List People (Directory)* with `$ARGUMENTS`. Confirm the exact person.
2. **List what they hold.** *Get Device Employee Detail* and *Search Devices* for Devices assigned to them; *Search Inventory Items* for non-managed assets (monitors, keys, accessories). Show one table with name, platform, serial, ownership (company or personal) and last check-in.
3. **Agree the plan per item.** Typical choices: collect and keep enrolled; lock until collected; wipe company-owned Devices before reassignment; disenroll personal Devices (this removes company data and management, not the person's data). Ask the user to choose for each Device. Never assume a wipe.
4. **Check access.** *List Access* for Applivery console access the person still holds. Offer *Revoke Access* with confirmation.
5. **Execute with confirmation.** Show the final list (action, Device, serial). Run only after confirmation. Wipe and disenroll need the user to name the action in their confirmation.
6. **Verify and record.** Re-read each Device's command status. Update inventory items (*Update Inventory Item* or *Add Note to Inventory Item*) with what was collected. Report what is still pending.

## Output

```markdown
## Offboarding: [name], last day [date]

| Item | Type | Serial | Plan | Status |
|---|---|---|---|---|
| [MacBook Pro] | Device (company) | [x] | Wipe after collection | Command acknowledged |

Console access: [revoked/none]
Pending: [items]
```
