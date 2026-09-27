# The Ward

> Azure security operations lab for telemetry, detection engineering, identity defense, and incident response.

## Executive summary

The Ward is a hands-on Azure security operations project built to demonstrate how I turn cloud telemetry into detections, investigations, and response workflows in a real lab environment. It shows that I can work across Azure infrastructure, Entra ID security, Microsoft Sentinel, KQL, and automation rather than only documenting theory.

This project is focused on building a real operational pipeline: ingest telemetry, validate it, investigate suspicious activity, write detection logic, trigger incidents, and document response actions with evidence.

## Why this project matters

The Ward is designed to prove that security engineering is not just about tools; it is about building a working operating model. The repo shows a realistic progression from baseline lab creation to telemetry validation, detection engineering, identity attack simulation, and response workflow design.

It is relevant for roles in:

- Azure security engineering
- Microsoft Sentinel / SIEM operations
- Identity and access security
- Detection engineering
- Cloud security operations
- SOC / IR workflow design

## At a glance

- Status: Active and progressing from foundational setup into detection engineering and response testing
- Core focus: Azure control-plane telemetry, Entra ID activity, KQL analysis, and incident response automation
- Primary proof point: simulated T1098.003 privilege escalation investigation with live detection and incident workflow
- Overall value: demonstrates end-to-end security operations capability in a lab environment

## What is already built

### Azure security foundation

- Created the `rg-the-ward` resource group
- Created the `law-the-ward` Log Analytics workspace
- Enabled Microsoft Sentinel
- Configured Azure Activity telemetry
- Confirmed Entra ID AuditLogs ingestion
- Validated that control-plane and identity events flow into the workspace and can be investigated

### Detection engineering

- Built the first scheduled analytics rule in Microsoft Sentinel
- Converted raw telemetry into investigations and alert logic
- Validated a role-assignment event from live data into an incident workflow
- Built KQL workflows that work against real tables instead of assumptions from documentation

### Identity-focused escalation case study

The strongest proof point in this repo is the simulated privilege escalation workflow built around MITRE ATT&CK T1098.003.

This scenario shows a low-privilege or newly created identity being assigned the Global Administrator role, the event being captured in `AuditLogs`, the alert being generated in Sentinel, and the incident being investigated with evidence, timeline, and response actions.

This is a concrete example of how identity abuse is detected and triaged in a realistic Azure environment.

### Automation and response workflow

- Built a Logic App response path
- Explored incident trigger automation and entity mapping
- Documented the technical and operational limitations of the automation layer
- Demonstrated the difference between alerting, incident creation, and true containment automation

## Featured work in this repo

### 1. Azure & Sentinel lab setup
- Azure Activity telemetry pipeline
- Log Analytics workspace setup
- Microsoft Sentinel enablement and validation

### 2. Identity defense case study
- T1098.003 investigation and detection workflow
- Simulated role escalation scenario
- Evidence package and screenshots

### 3. Security operations narrative
- Progress documentation and milestone tracking
- Investigation workflow examples
- Detection and automation learning notes

## Repo map

- `README.md` - landing page and portfolio summary
- `Azure-Security-Progress-Sept-21-2026.md` - milestone narrative and technical progress log
- `protecting_the_realm.md` - earlier security baseline memo and lab foundation notes
- `feature_showcase.md` - project positioning and potential portfolio slide structure
- `Simulated Priv Esc/` - working investigation writeup, screenshots, and evidence set
- `screenshots/` - supporting visual artifacts
- `SSH/` - lab tooling and access material

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
- [ ] Add more identity-based attack simulations
- [ ] Improve and harden automation and containment actions
- [ ] Turn this into a repeatable SOC-style workflow with broader coverage and reporting

## What I want to do next

The Ward is moving toward a more complete Azure security operations workflow. The next objective is to build a repeatable set of investigations and detections that show not just setup, but operational maturity.

- Add more Entra ID and Azure control-plane attack simulations
- Expand the detection library to cover persistence and lateral movement paths
- Build a reusable investigation playbook for identity abuse and tenant compromise
- Improve automation with cleaner entity mapping and more reliable response logic
- Continue documenting progress in a way that is easy for hiring managers and technical reviewers to understand quickly

## Final summary

The Ward is the working record of an Azure security lab that has moved past planning and into active detection engineering. It shows real telemetry, real investigation, and real security operational thinking. The project is still evolving, but the current state is strong enough to demonstrate capability, depth, and a clear path toward more advanced Azure and identity security work.

