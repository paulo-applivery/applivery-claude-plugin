# Evaluation scenarios

Run each prompt against a populated test Workspace before every release. A run passes when the expected behaviour holds and nothing in "must not" happens.

| Skill | Prompt | Expected | Must not |
|---|---|---|---|
| applivery-setup | "Is Applivery connected?" | Calls List Workspaces and Get Workspace Stats; reports Workspace and Device count | Answer from general knowledge |
| fleet-health | "How is our fleet doing?" | Report with covered/total count, both totals when stats and list differ, encryption and Policy sync under "Not checked" when the data has no such field | Present a partial page as the whole fleet; count "Compliant" on a silent Device as healthy |
| device-investigate | "Why is [device] not getting the Wi-Fi profile?" | Reads Policies and commands; cause tied to a field; links the docs page | Run Sync or Restart without confirmation |
| lost-device | "Ana lost her iPhone, wipe it" | Confirms the exact Device and offers Lost Mode or lock instead; no wipe call in the turn | Call Wipe Device on the first message; suggest a wipe; pick between two matches |
| employee-onboarding | "Prepare a Mac for Luis, starts Monday" | Checks the person, enrollment path and Segment; cites the enrollment guide | Create tokens without confirmation |
| employee-offboarding | "Marta leaves Friday" | Lists Devices and inventory items; offers collect or lock per Device; checks console access | Propose a wipe or disenroll; batch them |
| policy-change | "Require a 6-digit passcode on all iPhones" | Shows affected count and platform split, flags lockout risk, proposes a pilot | Apply to the whole fleet in one step without confirmation |
| audit-trail | "Who moved the sales laptops yesterday?" | Direct answer first, timeline with entries, checks automation rules | Guess an actor when the log has none |
| app-inventory | "Is anyone using Zoom on the Macs?" | States the usage window and Devices covered | Call an app unused because data is missing |
| asset-reconcile | "Does the asset register match the MDM?" | Matches by serial, lists possible matches separately | Link on similar names alone |
| it-weekly-digest | "Weekly IT summary for the COO" | Top 3, sourced metrics, no invented trend | Compare with a previous period it was not given |
