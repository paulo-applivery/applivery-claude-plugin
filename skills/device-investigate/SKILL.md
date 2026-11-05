---
name: device-investigate
description: Troubleshoot a single Device in Applivery by reading its detail, applied Policies, pending and failed commands, installed apps, scripts and recent audit entries. Use when someone says a device is non-compliant, missing an app or a setting, not reporting, slow to receive a Policy, or behaving strangely, or asks "what is going on with this laptop/phone".
argument-hint: "<device name, serial number or user>"
---

# Device investigation

> Shared safety rules and the action catalogue are in [CONNECTORS.md](../../CONNECTORS.md). Follow them on every run.

## Workflow

1. **Find the Device.** Call *Search Devices* with `$ARGUMENTS`. If several match, list them (name, platform, serial, owner, last check-in) and ask which one. Never guess.
2. **Read everything relevant, in parallel where possible:**
   - *Get Device Detail*: OS, model, encryption, storage, last check-in, Segment, tags, owner.
   - *Get Device Policies*: what is applied and its status.
   - *Get Device Commands Grouped* (or *Get Device Commands*): pending, failed and recent commands.
   - *Get Device Apps*: when the issue is about an app.
   - *Get Device Scripts* and *Get Device Script Logs*: when scripts are involved.
   - *Get Audit Log* filtered to this Device: recent changes by people or automation.
3. **Explain the cause.** Tie each conclusion to the field that supports it ("Policy X shows status failed since [date]"). When several causes fit, rank them and say what would tell them apart.
4. **Check the docs.** Use the Applivery Docs server for the relevant troubleshooting page and link it.
5. **Propose the fix.** Typical fixes: *Sync Device*, *Restart Device*, re-assigning a Policy, moving the Device to the right Segment, reinstalling an app. Show the exact action and target, then wait for confirmation. After acting, re-read the Device and report the observed result.

## Output

```markdown
## [Device name] ([platform], serial [x])
Owner: [name] | Segment: [path] | Last check-in: [time] | Encrypted: [yes/no]

**Most likely cause:** [one sentence] (evidence: [field/value])
**Other possibilities:** [list]

| Area | Finding |
|---|---|
| Policies | ... |
| Commands | ... |
| Apps / scripts | ... |
| Recent changes | ... |

**Proposed fix:** [action] on [Device]. Confirm to run it.
Docs: [link]
```
