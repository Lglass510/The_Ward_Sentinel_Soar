# The Ward

> Azure security lab, telemetry pipeline, and detection engineering workspace.

The Ward is now a real Microsoft Sentinel lab, not just a future plan. The focus today was building a working flow from Azure control-plane telemetry and Entra ID activity into Microsoft Sentinel, then validating the data with KQL and turning that into the first scheduled analytics rule.

This is the point where The Ward stopped being a concept and became a hands-on security operations environment with a clear operational model.

## Current direction

The work is centered on one question: can I take Azure telemetry, investigate it, and turn it into a valid Sentinel detection workflow? The answer today was yes, at least at the baseline level.

The Ward is now the dedicated home for Azure security operations in this environment. The work is intentionally organized around a single path:

1. Resource group and workspace creation
2. Data connector onboarding
3. Telemetry validation
4. KQL investigation
5. Detection engineering
6. Incident workflow and automation

## What I built today

### Azure security foundation

- Created the `rg-the-ward` resource group
- Created the `law-the-ward` Log Analytics workspace
- Enabled Microsoft Sentinel on the workspace
- Installed the Azure Activity solution from the Content Hub
- Configured the Azure Activity data connector and connected the subscription
- Generated a real control-plane event by modifying a resource tag and confirmed it landed in `AzureActivity`

### Entra ID identity telemetry

- Confirmed the Entra ID data connector is active for the Sentinel workspace
- Verified the `AuditLogs` table exists in the workspace
- Generated fresh identity activity and confirmed ingestion
- Inspected a real event and identified the significant fields for investigation: `TimeGenerated`, `OperationName`, `Result`, `InitiatedBy`, `TargetResources`, and `AdditionalDetails`

### KQL investigation workflow

I moved from reading about KQL to using it against real data. This included queries such as:

```kusto
AuditLogs
| where TimeGenerated > ago(30m)
| order by TimeGenerated desc
```

```kusto
AzureActivity
| where TimeGenerated > ago(24h)
| order by TimeGenerated desc
```

The biggest lesson was not to assume the schema or table names in the docs match the actual tenant environment. The habit that mattered most was inspecting the data you actually have before writing the query you wish you had.

## Detection engineering milestone

The biggest step forward was creating the first scheduled query analytics rule in Sentinel.

This is the moment The Ward became a SIEM lab instead of a logging lab. The working pipeline is now:

```text
Azure Activity / Entra ID telemetry
        ↓
AzureActivity + AuditLogs
        ↓
law-the-ward
        ↓
Microsoft Sentinel
        ↓
KQL investigation
        ↓
Analytics rule
        ↓
Alert / incident
        ↓
Automation and playbook workflow
```

## Lessons from the setup

- The issue was not just Azure portal behavior; it was missing a clean operational model.
- Azure Activity, Defender, and Sentinel need to be intentionally aligned rather than treated as separate silos.
- A clear resource-group and workspace structure reduces confusion immediately.
- The initial drift was caused by assumptions about table names and log schemas, not by a lack of effort.
- Real progress started when the environment was treated as a telemetry-to-detection pipeline rather than a set of disconnected portal tasks.

## Current state

- [x] The Ward resource group created
- [x] Log Analytics workspace created
- [x] Microsoft Sentinel enabled
- [x] Azure Activity connector configured and event validated
- [x] Entra ID connector confirmed and identity logs validated
- [x] Real KQL investigation completed against live tables
- [x] First Sentinel analytics rule created as a scheduled query rule
- [ ] Generate a deliberate event for the analytics rule
- [ ] Confirm the resulting alert and incident
- [ ] Investigate the incident with evidence and timeline
- [ ] Build the first automation rule and playbook
- [ ] Add controlled remediation and data-plane telemetry
- [ ] Expand detections and document the full Ward architecture

## What matters now

The Ward is no longer a place where I keep planning Azure security work. It is the working environment where the telemetry path, detection logic, and investigation process are being built and tested in real time.

The next session can legitimately start with incident investigation and SOAR. That is the right stopping point after today's progress.

## Safety and discipline

- Only test in authorized environments and accounts
- Keep the lab isolated from production systems
- Sanitize and protect evidence before sharing it
- Prefer reversible actions and controlled validation
- Document both success and failure so the process improves in a measurable way

## Summary

Today was the moment The Ward moved from setup and exploration into active security operations work. I created the Azure security baseline, validated telemetry, ran KQL against live data, and created the first analytics rule. That is the foundation for the next stage: alerts, investigation, and automation.

