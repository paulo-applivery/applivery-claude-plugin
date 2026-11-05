---
name: applivery-setup
description: Connect Applivery to Claude, confirm which Workspace is active and recommend tool permissions. Use when someone installs the plugin, says Applivery is not answering, asks which Workspaces they can reach, or wants to switch Workspace.
argument-hint: "[workspace name]"
---

# Applivery setup

> Shared safety rules and the action catalogue are in [CONNECTORS.md](../../CONNECTORS.md). Follow them on every run.

Get the user from "installed" to "a real answer from their fleet" in one pass.

## Workflow

1. **Check the connection.** Call *List Workspaces*. If the call fails or the tools are missing, tell the user to open **Settings > Connectors > Applivery > Connect** in Claude (or restart Claude Code after installing the plugin) and sign in with their Applivery account. Stop there.
2. **Confirm the Workspace.** Show the Workspaces returned and which one is active. If `$ARGUMENTS` names a Workspace, or the user asks to switch, call *Switch Workspace* after confirming the target by name. The switch lasts for this conversation only.
3. **Prove it works with a read.** Call *Get Workspace Stats* and report the enrolled Device count and the platform split exactly as returned.
4. **Recommend permissions.** Explain the three settings Claude offers per tool and recommend:
   - Read-only tools: *Needs approval* at first, *Always allow* once the team trusts the workflows.
   - Write tools: *Needs approval*.
   - *Wipe Device* and *Disenroll Device*: *Blocked* unless the team needs them in chat.
5. **Point to next steps.** Suggest `/fleet-health` as the first workflow.

## Output

```markdown
**Connected to Applivery** as of [time]
- Workspace: [name] ([n] Workspaces available)
- Devices enrolled: [n] ([platform split])
- Recommended permissions: [summary]
- Next: run /fleet-health
```

## Troubleshooting

| Symptom | Meaning | Fix |
|---|---|---|
| Answers without calling Applivery | Connector not enabled in this chat | Enable it and start a new conversation |
| 403 insufficient permissions | The user's Applivery role does not allow that action | Ask an Applivery admin; it is not a connector fault |
| An action is missing | Not published on this channel or plan | Continue without it and say so |
| Repeated rate-limit errors | Too many calls in a short window | Stop, wait, and narrow the request |
