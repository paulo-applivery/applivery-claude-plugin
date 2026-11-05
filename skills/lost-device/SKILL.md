---
name: lost-device
description: Respond to a lost or stolen Device with Applivery by confirming the Device, checking its last location and status, enabling Lost Mode or locking it, and wiping only on explicit confirmation. Use when someone reports a lost, stolen or missing phone, tablet or laptop, or asks to lock, locate or wipe a device.
argument-hint: "<device name, serial number or owner>"
---

# Lost or stolen device

> Shared safety rules and the action catalogue are in [CONNECTORS.md](../../CONNECTORS.md). Follow them on every run.

Speed matters, and so does not wiping the wrong Device. Follow the steps in order.

## Workflow

1. **Identify the Device exactly.** *Search Devices* with `$ARGUMENTS`. Show name, platform, serial, owner and last check-in. If more than one matches, ask which one. Do not continue until there is exactly one.
2. **Read current state.** *Get Device Detail* and, when the platform supports it, *Get Device Location* (and *Get Device Location History* if the user wants the trail). Report the time each value was recorded. Location data is personal data: show it only to the person handling the incident.
3. **Recommend the least destructive step that meets the goal:**
   - **Lost Mode** (*Enable Lost Mode*), where supported, to lock the Device with a message and phone number. Ask for the message and number.
   - **Lock** (*Lock Device*) when Lost Mode is not available.
   - **Never suggest a wipe.** Even when the user's first message says "wipe it", answer with the Device you found and offer Lost Mode or lock first. Run *Wipe Device* only if the user, after seeing that offer, asks again for a wipe of that exact Device by name. Explain that a wipe cannot be undone and that the Device may need re-enrollment if it is found. If *Wipe Device* is blocked or missing, say so and stop; do not work around it.
4. **Confirm and act.** Show the action, the Device and its serial. Run it only after the user confirms.
5. **Verify.** Read *Get Device Commands* for the command status and report it as observed (queued, sent, acknowledged, failed). A queued command reaches the Device only when it next connects; say so.
6. **Close the loop.** Suggest recording the incident (`/audit-trail` shows the trace), updating the inventory item, and *Disable Lost Mode* if the Device is recovered.

## Output

```markdown
## Incident: [Device name] ([serial]), owner [name]
Last check-in: [time] | Last location: [place/coordinates, recorded at time] 

Action taken: [Lost Mode/Lock/Wipe] at [time] → command status: [observed]
Next: [steps]
```
