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
3. **Agree the plan per item.** Offer: collect and keep enrolled, or lock until collected. Do not propose a wipe or disenroll. If the user asks for one by name for a specific Device (for example to reassign a company-owned laptop, or to release a personal phone, where disenroll removes company data and management but not the person's data), follow rule 4 in CONNECTORS.md: one Device at a time, with its name and serial shown and the action confirmed by name.
4. **Check access.** *List Access* for Applivery console access the person still holds. Offer *Revoke Access* with confirmation.
5. **Execute with confirmation.** Show the final list (action, Device, serial). Run only after confirmation. Wipe and disenroll are never part of a batch: each one is confirmed and run on its own.
6. **Verify and record.** Re-read each Device's command status. Update inventory items (*Update Inventory Item* or *Add Note to Inventory Item*) with what was collected. Report what is still pending.

## Output

```markdown
## Offboarding: [name], last day [date]

| Item | Type | Serial | Plan | Status |
|---|---|---|---|---|
| [MacBook Pro] | Device (company) | [x] | Lock until collected | Command acknowledged |

Console access: [revoked/none]
Pending: [items]
```
