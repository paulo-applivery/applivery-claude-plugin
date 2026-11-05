---
name: employee-onboarding
description: Prepare Applivery for a new hire by finding or creating the person, choosing the enrollment method, checking enrollment tokens and Smart Enrollments, and assigning the Device to them once enrolled. Use when someone asks to onboard a new employee, prepare a laptop or phone for a starter, or set up enrollment for a team.
argument-hint: "<person name or email> [platform] [start date]"
---

# Employee onboarding

> Shared safety rules and the action catalogue are in [CONNECTORS.md](../../CONNECTORS.md). Follow them on every run.

## Workflow

1. **Find the person.** *List Device Employees* or *List People (Directory)* with the name or email in `$ARGUMENTS`. If they do not exist, offer *Create Device Employee* with the fields the user gives you. Do not invent fields.
2. **Pick the enrollment path.** Ask for the platform and ownership (company-owned or personal) if not given. Check what the Workspace already has with *List Smart Enrollments*, *List Enrollment Tokens* and, for Apple, whether automated enrollment is in place. Use the Applivery Docs server to cite the matching enrollment guide (for example Apple automated enrollment, Android Zero-Touch, Windows Autopilot or Entra ID).
3. **Check the destination.** *Get Segment Tree* to confirm the Segment the Device should land in, and *Get Policy Assignations* for the Policies it will inherit. Summarise what the new Device will receive.
4. **Create what is missing, with confirmation.** If a token or Smart Enrollment is needed, show the exact settings and run *Create Enrollment Token* or *Create or Update Smart Enrollment* only after the user confirms.
5. **After enrollment.** When the Device appears in *Search Devices*, offer *Assign Device to Employee* and, if needed, *Move Device to Segment*. Verify with *Get Device Detail*.

## Output

```markdown
## Onboarding: [name] ([email]), starts [date]
Platform: [x] | Enrollment: [method] | Segment: [path]
Policies the Device will receive: [list]

Checklist
- [ ] Person exists in Applivery
- [ ] Enrollment ready ([token/smart enrollment])
- [ ] Device enrolled and assigned
- [ ] Policies in sync

Guide: [docs link]
```
