# Applivery for Claude

Run your Apple, Android and Windows fleet from a conversation. This plugin gives Claude the Applivery MCP server, the Applivery Docs server and a set of skills that turn everyday IT work into guided workflows: checking fleet health, troubleshooting a device, responding to a lost laptop, onboarding and offboarding people, rolling out a policy change safely, and answering "who changed this?" from the audit trail.

Claude acts as you. It sees only the Workspaces and actions your Applivery role allows, and it asks before it changes anything.

## What's inside

| Component | What it does |
|---|---|
| **Applivery MCP server** (`https://mcp.applivery.ai/mcp/anthropic`) | About 140 purpose-built actions on your Workspace: Devices, Policies, Segments, Device Audiences, Smart Attributes, enrollment, scripts, inventory, automation rules and the audit log. Reads and writes are separate actions, and every write is labelled destructive so Claude always asks first. |
| **Applivery Docs server** (`https://docs.applivery.com/mcp`) | Public documentation and REST API reference, so answers can link to the official page. No sign-in. |
| **Skills** | Step-by-step workflows, listed below. Each one runs as a slash command in Claude Code and loads automatically in Claude when your request matches. |

## Skills

| Skill | Use it to |
|---|---|
| `/applivery-setup` | Connect Applivery, confirm the right Workspace and set sensible tool permissions |
| `/fleet-health` | Get a fleet health report: stale check-ins, OS versions, encryption, policy sync |
| `/device-investigate` | Find out why one device is non-compliant, missing an app or not reporting |
| `/lost-device` | Handle a lost or stolen device: locate it, then Lost Mode or lock. It never suggests a wipe |
| `/employee-onboarding` | Prepare enrollment for a new hire and assign their devices |
| `/employee-offboarding` | List everything assigned to a leaver and run the collection or lock plan |
| `/policy-change` | Preview who a policy or Segment change affects, stage it, apply it and check sync |
| `/audit-trail` | Answer who did what, when and on which Device or Policy |
| `/app-inventory` | Review installed apps and app usage on Devices, and install or uninstall with confirmation |
| `/asset-reconcile` | Reconcile non-managed inventory items with enrolled Devices |
| `/it-weekly-digest` | Write a weekly summary for the IT lead: fleet changes, risks, automation results |

## Install

**Claude (web, desktop and mobile):** open **Settings > Connectors**, find **Applivery** and select **Connect**. Sign in with your Applivery account and authorize the Workspace on the consent screen.

**Claude Code:**

```
/plugin marketplace add paulo-applivery/applivery-claude-plugin
/plugin install applivery@applivery
```

Restart Claude Code, then run `/applivery-setup`.

## Requirements

- An Applivery account with access to at least one Workspace. The plugin never creates accounts or Workspaces.
- Applivery Endpoint Manager (UEM/MDM) for the device skills.
- A Claude plan that supports connectors.

## Permissions and safety

- **Your role is the ceiling.** Authorization is OAuth 2.1 with PKCE against your own Applivery account. There is no shared service account and no API key to paste.
- **Reads and writes are separate.** Read actions are labelled read-only; anything that changes state, including remote commands such as lock or restart, is labelled destructive.
- **Recommended settings in Claude:** leave read-only tools on *Needs approval* until you trust the workflows, then switch them to *Always allow*. Keep write tools on *Needs approval*. Set *Wipe Device* and *Disenroll Device* to *Blocked*: wiping or releasing a Device is best done from the Applivery dashboard.
- **The skills add their own gates.** Before any change they show the exact Devices or objects affected and wait for you to confirm. They never suggest a wipe or disenroll, never run one in a batch, and run one only when you ask for it by name for a single Device. If a tool is blocked, they stop instead of working around it.

## What the plugin runs, sends and fetches

- The plugin contains only Markdown skills and two remote MCP server references. It runs no local code, hooks or scripts, and it installs no packages.
- **To Applivery (`mcp.applivery.ai`, `docs.applivery.com`):** the action to run, its parameters (for example a Device identifier, a search term or a date range) and your access token. Applivery does not receive your conversation, prompt history, files or Claude's memory.
- **Back to Claude:** the result of that action, trimmed to what the request needs. It then becomes part of your conversation and follows your Claude data settings.
- **Applivery's operational logs** record which action ran, its parameters, a summary of the response, timing, Workspace, user, client, IP address and user agent, for support, debugging and abuse prevention. Parameters and summaries can include Device names, user names and email addresses.

## Privacy

Applivery's privacy policy applies to data the Applivery servers process: https://www.applivery.com/legal/privacy-policy/

## Support

- Documentation: https://docs.applivery.com/en/intelligence/applivery-mcp/
- Support: support@applivery.com
- Help center: https://www.applivery.com/help-center/

## License

MIT. See [LICENSE](LICENSE).
