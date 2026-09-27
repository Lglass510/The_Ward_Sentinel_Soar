# The Ward: AI-Assisted Azure Security Operations Lab

## Project positioning

The Ward is a portfolio-ready Azure security operations project designed to show how I build a real detection and response capability from the ground up. It combines Azure infrastructure, Entra ID investigation, Microsoft Sentinel telemetry, KQL analysis, and response automation in one working lab.

This is intentionally framed as more than a lab tutorial. It is a documented example of how I move from raw cloud telemetry to usable detections and analyst workflows.

---

## Why this matters

Most Azure security work is fragmented across portals, logs, dashboards, and documentation. The Ward is meant to show a cleaner operating model: one environment where telemetry is validated, suspicious activity is investigated, detections are tuned, and response actions are considered.

This makes the project valuable to recruiters, hiring managers, and technical reviewers because it demonstrates breadth and practical operating discipline.

---

## Recommended feature format

This should be presented as a 10–12 slide carousel or project showcase. Each slide should include a single strong screenshot and a concise explanation of the operational value.

---

## Slide 1 — Title slide

### Title
The Ward: Azure Security Operations Lab

### Caption
Building a real Azure security operations environment focused on telemetry, identity defense, detection engineering, and response workflow design.

### Screenshot
- Clean project title slide
- The Ward branding
- minimal architecture diagram

### Why this works
This immediately communicates that the project is technical, modern, and serious.

---

## Slide 2 — Problem statement

### Title
Why this project exists

### Caption
Cloud telemetry is often scattered across different tools and dashboards. The Ward creates a single operational flow for validation, investigation, and detection.

### Screenshot
- Fragmented workflow diagram or simple portal-to-Sentinel flow illustration

### Why this works
It presents the project as a solution to a real operational problem.

---

## Slide 3 — Architecture overview

### Title
Telemetry to detection pipeline

### Caption
The Ward is built as a direct pipeline from Azure Activity and Entra ID telemetry into Log Analytics and Microsoft Sentinel, then into investigation and detection work.

### Screenshot
- Azure Activity
- Entra ID
- Log Analytics
- Microsoft Sentinel
- KQL
- Analytics rule
- alert / incident

### Why this works
This is the clearest one-slide summary of the project and the easiest for a recruiter to understand.

---

## Slide 4 — Azure foundation

### Title
Dedicated lab environment

### Caption
Created a dedicated Azure lab environment for The Ward, including the resource group and Log Analytics workspace.

### Screenshot
- Resource group view
- Log Analytics workspace overview
- properly named lab resources

### Why this works
It demonstrates cloud infrastructure setup discipline and operating maturity.

---

## Slide 5 — Sentinel onboarding

### Title
Microsoft Sentinel enabled

### Caption
Enabled Sentinel and established the monitoring foundation required for a real detection workflow.

### Screenshot
- Sentinel overview page
- workspace connected
- connector or content hub view

### Why this works
It makes the project feel operational, not academic.

---

## Slide 6 — Azure Activity validation

### Title
Validated control-plane telemetry

### Caption
Generated and confirmed a real Azure Activity event so the pipeline was proven before moving to detection work.

### Screenshot
- Azure Activity query output
- event generation screenshot
- connector validation screen

### Why this works
It proves the foundation is real and not just configured on paper.

---

## Slide 7 — Entra ID telemetry

### Title
Identity investigation enters the same pipeline

### Caption
Connected Entra ID audit logs and validated that identity events could be investigated alongside Azure activity in the same operational model.

### Screenshot
- Entra ID connector status
- AuditLogs output with fields like InitiatedBy and TargetResources

### Why this works
This strengthens the story by adding identity security depth and enterprise relevance.

---

## Slide 8 — KQL investigation workflow

### Title
Real investigation with KQL

### Caption
The project moved from reading about KQL to running live investigations against real logs and checking schemas instead of assuming field names.

### Screenshot
- KQL queries against `AuditLogs` and `AzureActivity`
- output tables and investigation filters

### Why this works
This is one of the strongest proof points for SOC, detection, and cloud-security employers.

---

## Slide 9 — Detection engineering

### Title
First analytics rule created

### Caption
Built the first scheduled query analytics rule, moving the environment from a logging lab to a genuine detection workflow.

### Screenshot
- Analytics rule configuration screen
- KQL logic and rule settings
- rule criteria and schedule

### Why this works
It highlights a real technical milestone that feels like measurable engineering progress.

---

## Slide 10 — Simulated privilege escalation

### Title
T1098.003 investigation in practice

### Caption
Demonstrated identity abuse through a simulated Global Administrator role assignment and validated the full detection-to-incident path.

### Screenshot
- Entra audit log or incident screenshot
- role-assignment view
- KQL query results
- incident timeline

### Why this works
This is the most compelling story in the project because it shows real-world attack logic and detection capability.

---

## Slide 11 — Response automation

### Title
From alert to automation

### Caption
Built the first response workflow and documented both the working logic and limitations discovered during implementation.

### Screenshot
- Logic App or playbook diagram
- automation rule config
- incident trigger flow

### Why this works
It shows maturity beyond alert generation and into security operations workflow design.

---

## Slide 12 — Final takeaway

### Title
A real Azure security operations lab

### Caption
The Ward demonstrates that I can build, validate, and document a cloud security operations environment that links telemetry, detection, identity defense, and response thinking.

### Screenshot
- final architecture diagram or project status board

### Why this works
This gives the project a clean close and makes the value obvious to a recruiter or hiring manager.

---

## Short portfolio summary

The Ward is an Azure security operations lab built to validate the full workflow from telemetry ingestion to detection engineering and incident response. It includes live Azure and Entra ID log validation, Microsoft Sentinel analytics rule creation, KQL investigation, and a simulated T1098.003 privilege escalation case study. The project demonstrates practical cloud security engineering, SIEM workflow design, and a working understanding of identity-centered attack paths.

### Screenshot
- alert overview
- incident timeline
- entity mapping
- triage summary

### Why this works
It shows the project has operational depth beyond setup.

---

## Slide 12 — Automation foundation

### Title
Operational response thinking

### Caption
Using PowerShell and automation concepts to support repeatable investigation and response tasks, reinforcing a practical security operations workflow.

### Screenshot
- PowerShell script or runbook concept
- checklist or remediation workflow
- response action plan

### Why this works
This connects the project to automation, which is a high-value employer signal.

---

## Slide 13 — Lessons learned

### Title
What changed

### Caption
The biggest win was moving from fragmented portal work to a single telemetry model. A clean operational structure made the environment far more repeatable and easier to investigate.

### Screenshot
- before/after comparison
- short lessons list
- “what changed” summary

### Why this works
This makes the project feel mature and reflective instead of just a lab build.

---

## Slide 14 — Final summary

### Title
The Ward is now a working security operations lab

### Caption
This project combines Azure security, KQL, detection engineering, AI-assisted investigation, and automation into a practical foundation for real security operations work.

### Screenshot
- final summary slide with four pillars
  - Azure
  - Security telemetry
  - AI-assisted investigation
  - Automation
- optional roadmap line: next phase = automated response + SOAR

### Why this works
It closes the feature with a strong, memorable statement and positions the project as ongoing and credible.

---

## Suggested short caption for LinkedIn post

Building a real Azure security operations lab focused on telemetry, detection, and response. The Ward combines Azure Activity, Entra ID, Microsoft Sentinel, KQL investigations, and AI-assisted analysis into a working environment for investigation and detection engineering.

#Azure #AzureSecurity #MicrosoftSentinel #CyberSecurity #AI #ArtificialIntelligence #KQL #PowerShell #CloudSecurity #SecurityOperations #ThreatDetection #SOC #Automation

---

## Best positioning statement for recruiters

This project demonstrates hands-on experience with Azure security operations, Microsoft Sentinel, identity telemetry, KQL investigation, AI-assisted triage, and automation-focused security workflows — bridging cloud security engineering with modern AI-enabled operations.

---

## Screenshot order summary

1. Title slide
2. Why this project exists
3. Architecture overview
4. Resource group + workspace
5. Sentinel enablement
6. Azure Activity validation
7. Entra ID validation
8. KQL investigation
9. AI assistance
10. Analytics rule
11. Alert and incident path
12. Automation foundation
13. Lessons learned
14. Final summary

---

## Recommended project story in one sentence

The Ward is a practical Azure security operations lab that turns telemetry into detection, investigation, and response workflows with AI support and automation built in.
