# Connectors and safety rules

## Servers in this plugin

| Server | URL | Sign-in | Used for |
|---|---|---|---|
| `applivery` | `https://mcp.applivery.ai/mcp/anthropic` | OAuth 2.1 (your Applivery account) | Everything that reads or changes your Workspace |
| `applivery-docs` | `https://docs.applivery.com/mcp` | None | Citing the official documentation and API reference |

Skills refer to Applivery actions by the title Claude shows for them (for example *Search Devices* or *Lock Device*). Which actions you see depends on your platform mix, your Applivery plan, your role and the channel. If an action a skill mentions is missing, say so and continue with what is available.

## Actions by area

| Area | Read-only | Changes state (always confirmed) |
|---|---|---|
| Workspace | List Workspaces, Get Workspace Stats | Switch Workspace |
| Devices | Search Devices, List Devices, Get Device Detail, Get Device Apps, Get Device App Usage, Get Device Data Usage, Get Device Policies, Get Device Commands, Get Device Commands Grouped, Get Device Location, Get Device Location History, Get Device Scripts, Get Device Script Logs | Lock Device, Restart Device, Shutdown Device, Sync Device, Rename Device, Update Device Tags, Enable Lost Mode, Disable Lost Mode, Clear Passcode, Install App on Device, Uninstall App from Device, Move Device to Segment, Manage Device Policy Assignment, Manage Device Scripts, Wipe Device, Disenroll Device |
| People | List Device Employees, Get Device Employee Detail, List People (Directory) | Create Device Employee, Assign Device to Employee |
| Policies | List Policies, List Policy Templates, Get Policy Detail, Get Policy Assignations, Get Policy Composition, Get Policy Sync Status | Create Policy, Update Policy, Delete Policy, Manage Policy Apps, Manage Policy Scripts |
| Segments and permissions | List Segments, Get Segment Tree, Get Segment Detail, List Segment Permissions, Get Segment Permission(s), Get User Segment Permissions, Preview Segment Permission | Create/Update/Delete Segment, Create/Update/Delete Segment Permission |
| Device Audiences | List Device Audiences, Get Device Audience Detail, Preview Device Audience | Create/Update/Delete Device Audience |
| Smart Attributes | List Smart Attributes, Get Smart Attribute Detail | Create/Update/Delete Smart Attribute, Assign/Unassign Smart Attribute |
| Enrollment | List Enrollment Tokens, List Smart Enrollments, List VPP Assets | Create/Delete Enrollment Token, Create or Update Smart Enrollment, Delete Smart Enrollment |
| Scripts | Get Script Content, Get Script Assignations | Create Script |
| Inventory | List Inventory Items, Search Inventory Items, Get Inventory Item Detail | Create/Update/Delete Inventory Item, Add/Remove Note, Link Inventory Item to MDM Device |
| Automation | List Automation Rules, Get Automation Rule Detail, Get Automation Rule Logs | Create/Update/Delete Automation Rule |
| Audit | Get Audit Log, Get Audit Entry Detail | |
| Access | List Access | Grant Access, Update Access, Revoke Access |

The connector also exposes App Distribution actions (builds, publications, stores). No skill in this version targets them.

## Safety rules every skill follows

1. **Read before you write.** Gather the current state with read-only actions first, and show it.
2. **Name the blast radius.** Before any change, list exactly which Devices, people, Policies or Segments it touches, with a count. For Segment, Audience or permission changes, use the Preview action when one exists.
3. **One confirmation per change set.** Ask once for the exact list shown. If the list changes, ask again.
4. **Never wipe or disenroll on your own initiative.** Do not propose *Wipe Device* or *Disenroll Device* as a next step. Offer Lost Mode, lock or collection instead. Run a wipe or disenroll only when the user asks for it by name in the current conversation, for one named Device at a time, after you have shown that Device's name and serial and the user has confirmed in words that name the action. Never batch them, and never run them from a scheduled or automated task. Deletes follow the same rule.
4b. **Respect a block.** If the user or the organization has set a tool to *Blocked*, do not look for another tool that achieves the same effect.
5. **Verify after acting.** Re-read the object (Device detail, command status, Policy sync status) and report the observed result, not the intended one.
6. **Say what you did not check.** Every count states the query and time it came from. If results were paginated or sampled, say how many were covered.
7. **Stay in one Workspace.** State the Workspace at the start. Never mix data across Workspaces in one answer.
8. **Cite the docs.** When explaining how a feature works, use the Applivery Docs server and link the page.
