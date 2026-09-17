# Protecting the Realm

## Date
2026-09-17

## Objective
Build the Azure security baseline for The Ward and turn it into a working telemetry-to-detection pipeline in Microsoft Sentinel.

## What I accomplished

Today I built the actual Azure security foundation for The Ward and moved the lab into a real operational state. I created the dedicated resource group, the Log Analytics workspace, enabled Sentinel, connected the Azure Activity solution, validated Entra ID logs, and created the first scheduled analytics rule.

This was not just setup work. It was hands-on infrastructure and detection work that produced a functioning pipeline from telemetry to KQL investigation to an analytics rule.

## Why this mattered

The real issue was not simply that Azure was confusing. It was that the environment was missing a clear security model. I spent time reconciling the difference between:

- Azure Activity control-plane telemetry
- Entra ID identity activity
- Log Analytics workspace data
- Microsoft Sentinel analytics and detections
- Defender and Sentinel operating context

Once I shifted from portal clicking to an intentional telemetry flow, the environment started working like a security operations lab instead of a disconnected collection of settings.

## Environment snapshot

- Resource group: `rg-the-ward`
- Log Analytics workspace: `law-the-ward`
- Microsoft Sentinel: enabled on the workspace
- Azure Activity telemetry: configured and validated
- Entra ID connector: confirmed and verified
- Data path: `AzureActivity` and `AuditLogs` into the workspace and Sentinel

## What was validated

### Azure Activity

- Installed the Azure Activity solution
- Configured the data connector
- Generated a control-plane activity event by modifying a tag
- Confirmed the record landed in `AzureActivity`
- Queried the data successfully from Defender / Advanced Hunting

### Entra ID

- Confirmed the connector and Audit Logs are enabled
- Verified the `AuditLogs` table exists
- Generated fresh identity activity and confirmed ingestion
- Reviewed a real event and identified the key investigation fields

### KQL

- Ran live queries against `AuditLogs` and `AzureActivity`
- Learned the importance of checking the actual table schema before assuming column names
- Realized the docs and actual tenant environment do not always match one-to-one

### Detection engineering

- Created the first Sentinel scheduled query analytics rule
- Got the rule configuration working after troubleshooting the editor and rule setup
- Established the basic telemetry → detection path

## Lessons learned

- The resource group is not just a container; it is the foundation of an organized security workflow.
- Azure Activity, Sentinel, and Entra ID telemetry all need to be intentionally aligned.
- The habit that mattered most was inspecting the actual logs before writing assumptions into the query.
- The first real progress happened when I stopped treating each Azure feature as separate and started viewing the lab as one detection pipeline.
- The Ward is now a practical SOC-style environment instead of a future concept.

## Operational direction

The Ward will continue to grow around a simple and realistic progression:

1. validate telemetry
2. investigate the data with KQL
3. create alerts and detections
4. confirm alert generation and incident creation
5. build an automated response and playbook
6. document the workflow and improve it repeatedly

## Success criteria for this phase

This phase is successful when the telemetry path is stable, the workspace is actively ingesting relevant logs, the investigation workflow is working, and the first analytics rule is producing a proper alert path.

## Next step

The right next session is incident investigation and SOAR. That is the natural continuation after building the Azure and Sentinel baseline.

## Closing note

Today was the first time The Ward felt like a real security lab rather than an idea I was trying to preserve. The biggest win was not just creating the workspace; it was building a working telemetry-to-detection pipeline and showing that the lab can now support actual investigation and detection work.

