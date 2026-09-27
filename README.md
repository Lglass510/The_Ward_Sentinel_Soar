# The Ward

> Azure security operations lab for telemetry, detection engineering, identity defense, and incident response.

## Recruiter summary

The Ward is a hands-on Azure security operations project built to demonstrate how I turn cloud telemetry into detections, investigations, and response workflows in a real lab environment. It shows that I can work across Azure infrastructure, Entra ID identity security, Microsoft Sentinel, KQL, and incident response automation rather than only documenting theory.

This project is focused on building a real operational pipeline: ingest telemetry, validate it, investigate suspicious activity, write detection logic, trigger incidents, and document response actions with evidence.

## At a glance

- Status: Active and progressing from baseline setup to detection engineering and response testing
- Focus: Azure control-plane telemetry, Entra ID identity activity, Microsoft Sentinel, KQL, and analytical workflow design
- Core capability: build a complete telemetry-to-detection pipeline and validate it with real incidents
- Current milestone: simulated privilege escalation investigation using T1098.003 and Global Administrator assignment abuse
- Primary outcome: a working lab that demonstrates how Azure security operations work end to end

## What I have built

### 1. Azure security foundation

- Created the `rg-the-ward` resource group
- Created the `law-the-ward` Log Analytics workspace
- Enabled Microsoft Sentinel
- Connected Azure Activity telemetry into the workspace
- Verified Entra ID audit logs were ingested and usable
- Confirmed that control-plane and identity events can be investigated with real data

### 2. Detection engineering

- Built the first scheduled analytics rule in Microsoft Sentinel
- Validated a role-assignment event from live telemetry into an alert and incident
- Tested the gap between raw logs and high-fidelity detections
- Used KQL to investigate `AuditLogs` and `AzureActivity` with live evidence rather than simulated data only

### 3. Identity-focused escalation case study

The strongest proof point in this repo is the simulated T1098.003 investigation.

This project demonstrates an attacker path in which a newly created or low-privilege identity is assigned the Global Administrator role, the event is captured in Entra ID audit logs, the alert fires in Sentinel, and the incident is triaged with timeline, evidence, and incident-response documentation.

This is not a conceptual exercise. It is a functioning detection engineering workflow built in a lab environment.

### 4. Automation and response workflow

- Built and documented a Logic App / playbook response path for incident-triggered actions
- Tested the incident-to-automation handoff
- Documented both the working logic and the limitations discovered during implementation
- Demonstrated the difference between signal generation, entity mapping, and real containment automation

## The most important proof points

The Ward is now more than a setup repo. It contains working artifacts that show practical security engineering progress.

- Real Azure telemetry ingestion and validation
- Real Entra ID audit log validation
- KQL-based investigation against live data
- Sentinel alert creation and incident generation
- Role-assignment escalation simulation and detection
- Response workflow documentation and limitations captured honestly

## Featured work in this repo

### Azure & Sentinel lab setup
- Azure Activity telemetry pipeline
- Log Analytics workspace configuration
- Microsoft Sentinel enablement and validation

### Identity defense case study
- T1098.003 investigation and detection workflow
- Simulated role escalation scenario
- Evidence package and screenshots

### Key documentation and assets
- `README.md` - project overview and current status
- `Azure-Security-Progress-Sept-21-2026.md` - security progression notes
- `Simulated Priv Esc/` - the working investigation, screenshots, and evidence set
- `screenshots/` - supporting visual documentation

## Project status

### Completed

- [x] Azure lab foundation created
- [x] Sentinel workspace enabled
- [x] Azure Activity and Entra ID telemetry validated
- [x] KQL investigation workflows executed against live data
- [x] First analytics rule created and validated
- [x] Incident generation confirmed
- [x] Automation workflow documented and tested in concept
- [x] Privilege escalation investigation documented as a real case study

### In progress

- [ ] Expand detection library beyond the first role-assignment rule
- [ ] Add more identity-based attack scenarios
- [ ] Improve and harden automation and containment actions
- [ ] Turn this into a repeatable SOC-style workflow with broader coverage and reporting

## What I want to do next

The Ward is moving toward a more complete Azure security operations workflow. The next objective is to build a repeatable set of investigations and detections that show not just setup, but operational maturity.

- Add more Entra ID and Azure control-plane attack simulations
- Expand the detection library to cover persistence and lateral movement paths
- Build a reusable investigation playbook for identity abuse and tenant compromise
- Improve automation with cleaner entity mapping and more reliable response logic
- Continue documenting progress in a way that is easy for hiring managers, recruiters, and technical reviewers to understand quickly

## Why this matters

This project demonstrates that I can work across several important security engineering domains:

- Azure and cloud infrastructure
- Microsoft Sentinel and SIEM operations
- KQL investigation and detection design
- Entra ID / identity defense
- Incident response and automation thinking
- Translating technical implementation into clear, evidence-backed storytelling

## Career impact

This work shows I can build security capability from the ground up in a cloud environment and communicate the outcome clearly. It is relevant for roles in:

- Security engineering
- Cloud security operations
- Identity and access security
- Detection engineering
- SOC / detection content development
- Azure security engineering

## Repo structure

- `README.md` - landing page and project narrative
- `Azure-Security-Progress-Sept-21-2026.md` - progress narrative
- `Simulated Priv Esc/` - privilege escalation investigation writeup and support images
- `screenshots/` - general visual records
- `SSH/` - lab tooling and access artifacts

## Final summary

The Ward is the working record of an Azure security lab that has moved past planning and into active detection engineering. It shows real telemetry, real investigation, and real security operational thinking. The project is still evolving, but the current state is strong enough to demonstrate capability, depth, and a clear path toward more advanced Azure and identity security work.

