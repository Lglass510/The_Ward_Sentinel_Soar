# Playbook Audit and Remediation: Making the Block-User Response Actually Work

**Follows:** [T1098.003 investigation writeup](T1098.003_investigation_writeup.md), Section 8 ("Known limitation")
**Environment:** `MicrosoftDefenderLab` resource group, North Central US, workspace `law-defenderlab`
**Author:** Lourie Glass
**Dates:** September 29-30, 2026

---

## 1. Where this started

The original T1098.003 writeup ended with an open item: the Sentinel playbook `Block-Entra-ID-user---Incident` ran and reported success, but it never disabled anyone. I disabled `testattacker` by hand during incident closure and documented the automation as unfinished.

I was tempted to delete the resource group and rebuild. Instead I audited what was deployed first. The audit was run with Claude Code as a lab partner, reading configuration through Azure CLI and the Microsoft Graph and ARM REST APIs. I made the fixes myself in the portal and in PowerShell.

The playbook design (for reference; the logic did not change, only its configuration and permissions):

![Playbook canvas](playbook.png)
*Trigger on incident, get Account entities, loop over each account: PATCH the user through Graph, then comment on the incident with the result.*

## 2. Audit: what was in the resource group

| Resource | State found | Decision |
|---|---|---|
| `law-defenderlab` + Sentinel + UEBA | Healthy, Entra logs arriving | Keep |
| Analytics rule "Privilege Escalation - Entra Role Assignment" | Query good, entity mapping wrong | Fix |
| Automation rule "Role Escalation" | No conditions | Fix |
| Playbook `Block-Entra-ID-user---Incident` | Never disabled a user | Fix |
| `microsoftsentinel-...` API connection | Ready, used by the playbook | Keep |
| `azuread-...`, `office365-...` API connections | Error: not authenticated, unused | Delete |
| `azuread-1` API connection | Connected (holding a sign-in token), unused | Delete |

Outside the resource group:

- A second Sentinel workspace in a separate East US resource group (`Microsoft-Sentinel-Resource-Group`).
- Five Global Administrators. Three were test accounts left over from the 9/27 simulation, including one named `testattacker`.
- Entra diagnostic settings still exporting to two workspaces that no longer exist (`evidence-law`, `law-the-ward`).
- `SignInLogs` not included in the export to `law-defenderlab`.

Ingestion over 30 days was about 0.17 GB, mostly `MicrosoftGraphActivityLogs`, so cost was not a factor.

## 3. Why the old runs looked green

![9/27 run marked Succeeded](logic%20app%20success.png)
*A 9/27 run marked Succeeded. At that point the playbook's managed identity had no Microsoft Graph permissions, so this run could not have disabled anyone.*

"Succeeded" on a Logic App run means no action ended in an unhandled failure. When `Entities - Get Accounts` returns nothing, the loop runs zero times and the run still succeeds. The latest pre-fix run (9/28) showed exactly that: every action inside the loop was `Skipped`. Two runs that did reach the disable step failed.

## 4. The five bugs and the fixes

### Bug 1: Entity mapping put a UPN in the object-ID slot

The analytics rule mapped the `TargetUser` column (a UPN like `testattacker@...onmicrosoft.com`) to the Account identifier `AadUserId`. That identifier expects the Entra object ID, a GUID.

![Entity mapping before](../screenshots/entitiy_map_mistake.png)
*Before: `AadUserId` mapped to `TargetUser`.*

The playbook builds its Graph call from that value:

```
PATCH https://graph.microsoft.com/v1.0/users/@{item()?['aadUserId']}
```

The query already computed the GUID as `TargetResourceId` but dropped it in the final `project`. I added it back:

![Rule query with TargetResourceId](../screenshots/role_esc_rule_query.png)

and remapped the entity:

![Entity mapping after](../screenshots/entity_map_fix.png)
*After: `AadUserId` mapped to `TargetResourceId`.*

The mapping dropdown did not list the new column until the query change was saved. Saving once with the old mapping, then reopening the rule, fixed it.

Why the GUID and not the UPN: the object ID never changes, while a UPN can change on a rename or domain move. Automation that disables accounts should key on the value that can't drift.

**Verified:** rule config read back through the Sentinel API showed `AadUserId <- TargetResourceId`, last modified 2026-09-29 19:45 UTC.

### Bug 2: Automation rule fired on every incident

![Automation rule before](automation_rule.png)
*Before: "No conditions defined," Analytic rule name = Any.*

With no conditions, the block-user playbook would run on every incident in the workspace, including Fusion detections and Defender sample alerts. Once the playbook could actually disable accounts, that would mean any incident naming an account (including mine) could disable it.

I added one condition: **Analytic rule name contains "Privilege Escalation - Entra Role Assignment."**

**Verified:** the saved rule stores the condition by rule ID, not name:

```
IncidentRelatedAnalyticRuleIds  Contains  .../alertRules/eeeeeeee-eeee-eeee-eeee-eeeeeeeeeeee
```

Renaming the analytics rule later won't break the automation rule.

### Bug 3: Success comment was posted to a tenant ID

Inside the loop, `item()` is the current account. The success branch had:

```
"incidentArmId": "@item()?['AadTenantId']"
```

That's the account's tenant ID, not an incident, so the comment action failed. The error branch was already correct, so I made the success branch match it in the designer, using the trigger's **Incident ARM ID**:

```
"incidentArmId": "@triggerBody()?['object']?['id']"
```

I also replaced the literal text "current time" in the message with the `Current time` action's output.

**Verified:** workflow definition read back after save (changed 2026-09-29 20:02 UTC).

### Bug 4: Managed identity had no Graph permissions

The disable step authenticates as the Logic App's system-assigned managed identity. Graph returned an empty list for that identity's app role assignments. Per the [Graph user update docs](https://learn.microsoft.com/graph/api/user-update?view=graph-rest-1.0#request-body), the least-privileged combination for changing `accountEnabled` is `User.EnableDisableAccount.All` + `User.Read.All`.

There's no portal button for granting Graph application permissions to a managed identity, so I did it with Microsoft Graph PowerShell:

![Granting Graph app roles in PowerShell](../screenshots/mggraph_permissions_ps.png)

```powershell
Connect-MgGraph -TenantId "<tenant-id>" -Scopes "Application.Read.All","AppRoleAssignment.ReadWrite.All"

$miId  = "cccccccc-cccc-cccc-cccc-cccccccccccc"   # playbook managed identity
$graph = Get-MgServicePrincipal -Filter "appId eq '00000003-0000-0000-c000-000000000000'"

$roles = $graph.AppRoles | Where-Object {
    $_.Value -in "User.EnableDisableAccount.All","User.Read.All" -and
    $_.AllowedMemberTypes -contains "Application"
}

foreach ($r in $roles) {
    New-MgServicePrincipalAppRoleAssignment -ServicePrincipalId $miId `
        -PrincipalId $miId -ResourceId $graph.Id -AppRoleId $r.Id
}
```

I ran the loop twice by accident. The second run failed with `Permission being assigned already exists on the object`. Nothing changed, but it showed me this command isn't idempotent, and a reusable script needs to check for an existing assignment first.

**Design decision:** the Graph docs also say that in app-only scenarios, disabling some admin accounts requires the app to hold a higher-privileged Entra role (for example Privileged Authentication Administrator). I chose not to grant that. Anyone who can edit this Logic App can make its identity do whatever that identity is allowed to do, so giving it a top-tier Entra role would turn "Logic App Contributor" into a tenant takeover path. Automation handles what the Graph permissions allow; anything beyond that falls to the error branch and a human.

**Verified:** Graph showed both app role assignments on the identity, created 2026-09-30 12:36 UTC.

### Bug 5: Playbook identity had more Sentinel access than it needed

The identity held **Microsoft Sentinel Contributor** and **Microsoft Sentinel Playbook Operator** on the whole resource group. The playbook only reads the incident and adds comments, which **Microsoft Sentinel Responder** covers. Playbook Operator is for whoever triggers playbooks, which Sentinel's own service identity already has.

I added Responder at the workspace scope first, then removed the two broader roles, so the playbook never had a gap in access:

![Narrowing Azure RBAC](../screenshots/narrow_permissions.png)

```powershell
New-AzRoleAssignment    -ObjectId $mi -RoleDefinitionName "Microsoft Sentinel Responder"         -Scope $ws
Remove-AzRoleAssignment -ObjectId $mi -RoleDefinitionName "Microsoft Sentinel Contributor"       -Scope $rg
Remove-AzRoleAssignment -ObjectId $mi -RoleDefinitionName "Microsoft Sentinel Playbook Operator" -Scope $rg
```

**Verified:** `Get-AzRoleAssignment` and a separate `az role assignment list` both return one assignment: Responder on `law-defenderlab`.

This fix and Bug 4 touch two different permission systems. Graph app roles control what the identity can do in Entra ID. Azure RBAC controls what it can do to Azure resources. Holding one grants nothing in the other.

## 5. Cleanup

**Unused API connections.** A Logic App lists every connection it uses in its `$connections` parameter. This playbook listed only `microsoftsentinel`, and it was the only Logic App in the subscription. `azuread-1` mattered most: its status was Connected, meaning it stored a delegated sign-in token that anyone able to edit a Logic App in the subscription could have used.

![Removing unused connections](../screenshots/remove_unused_connections_ps.png)

After deletion the resource group holds five resources: workspace, Sentinel, UEBA, playbook, and its Sentinel connection. The connection still reports Ready and the playbook is Enabled.

**Duplicate workspace.** I deleted the East US Sentinel resource group. Confirmed gone.

**Leftover Global Admins.** I removed Global Administrator from `testattacker`, `aldous.huxley`, and `testuser1` with Graph PowerShell (`Remove-MgRoleManagementDirectoryRoleAssignment`, with a check that the assignment exists before removing it). Global Admins went from five to two: my account and the `breakglass` emergency-access account.

## 6. End-to-end test

At 13:14 UTC I assigned **Security Administrator** to `testattacker`, a role on the detection's watch list. Everything below comes from AuditLogs, the Sentinel incidents API, and the Logic App run history.

| Time (UTC) | Event |
|---|---|
| 13:11:43 | Global Administrator removed from three test accounts |
| 13:14:01 | `Add member to role`: Security Administrator to `testattacker` |
| 13:32:13 | Incident #37 created (Defender XDR ID 261), Account entity `aadUserId = aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa` |
| 13:32:42 | Automation rule starts the playbook |
| 13:32:43 | `PATCH /v1.0/users/aaaaaaaa-...` returns HTTP 204; AuditLogs record `Disable account` initiated by `Block-Entra-ID-user---Incident` |
| 13:32:44 | Success comment added to incident #37 |

Detection to containment took about 18 minutes, almost all of it the rule's 15-minute schedule plus audit log delay. From incident creation to a disabled account took 30 seconds.

![testattacker disabled](../screenshots/testattacker_diabled.png)
*`testattacker` after the test: Account status Disabled. Assigned roles shows 0 because I removed the Security Administrator assignment after the test.*

Each fix showed up in this run:

| Fix | Evidence from the run |
|---|---|
| Entity mapping | Incident entity carried the GUID, and the Graph URI used it |
| Automation rule condition | Playbook ran for this rule's incident |
| Graph permissions | HTTP 204 and a `Disable account` audit event |
| Comment target | Comment posted on incident #37 |
| Responder role | Sufficient to post that comment |

## 7. A prediction that was wrong

Before the test I expected Graph to refuse the disable, since the target had just been made an admin. It didn't. A Security Administrator was disabled with only `User.EnableDisableAccount.All` + `User.Read.All`. Graph's extra protection for sensitive actions depends on which role the target holds, and Security Administrator wasn't enough to trigger it.

**Not verified:** whether a Global Administrator target would be blocked. I expect it would, based on the docs, but haven't tested it.

## 8. Still open

- Remove the stale Entra diagnostic settings pointing at `evidence-law` and `law-the-ward`.
- Add `SignInLogs` to the `law-defenderlab` export.
- The success comment rendered as `...at 2026-09-30T13:32:44.0343912Ztestattacker`: the account name token sits right after the timestamp. Move it next to "Account."
- Add `FullName <- TargetUser` as a second Account identifier so incidents show a readable name.
- Test against a Global Administrator target (Section 7).
- Add a Sentinel watchlist of accounts the playbook must never touch (starting with `breakglass`) and check it in the automation rule. Without it, a role change on the break-glass account would trigger an automatic disable.
- Triage the backlog: about 35 incidents are still New, most of them from the 9/27-9/28 testing.

## 9. What I took from this

- A green run history doesn't prove the action happened. The audit log entry `Disable account` does.
- The portal and the saved config can disagree. Reading the rule back through the API after saving caught that the FullName identifier never saved.
- Before granting an automation identity more power, ask who can edit that automation. They inherit everything the identity can do.
- Tests leave residue. Three test accounts held Global Administrator for three days after the original simulation because cleanup wasn't part of the test plan.
