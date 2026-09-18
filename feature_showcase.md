# The Ward: AI-Assisted Azure Security Operations Lab

## Project positioning

This project is designed as a polished LinkedIn feature and portfolio asset. It frames The Ward as a real Azure security operations lab that combines:

- Azure security baseline setup
- Microsoft Sentinel and Log Analytics telemetry
- Entra ID investigation and identity telemetry
- KQL investigation work
- analytics rule creation
- AI-assisted investigation and triage support
- automation and response workflows

The goal is to communicate that this is not a conceptual demo — it is a working, evolving security operations environment with real operational logic behind it.

---

## Recommended feature format

This should be presented as a 12–14 slide carousel or project showcase. Each slide should include one strong screenshot and one short caption that explains the value of the work.

---

## Slide 1 — Title slide

### Title
The Ward: AI-Assisted Azure Security Operations Lab

### Caption
Building a real Azure security operations environment focused on telemetry, investigation, detection, and response — with AI assisting the analyst workflow.

### Screenshot
- Clean project title slide
- The Ward branding
- a small architecture summary or simple diagram

### Why this works
This immediately positions the project as modern, technical, and professional.

---

## Slide 2 — Problem statement

### Title
Why this project exists

### Caption
Most Azure security work is fragmented across portals, logs, and dashboards. I wanted a single operating model for telemetry, investigation, and response.

### Screenshot
- a visual of disconnected tools or a simple “fragmented workflow” diagram
- optional note: Azure Activity, Entra ID, Sentinel, Defender, KQL

### Why this works
It shows intentional problem-solving, not just random lab work.

---

## Slide 3 — Architecture overview

### Title
Telemetry to detection pipeline

### Caption
The Ward is built as a direct pipeline from Azure control-plane and identity telemetry into Log Analytics and Microsoft Sentinel for investigation and detection.

### Screenshot
- architecture diagram showing:
  - Azure Activity
  - Entra ID
  - Log Analytics workspace
  - Microsoft Sentinel
  - KQL investigations
  - Analytics rule
  - alert / incident / automation

### Why this works
This is the clearest “big picture” slide and tells recruiters everything they need to know.

---

## Slide 4 — Azure foundation

### Title
Dedicated lab environment

### Caption
Created the dedicated Azure security lab environment for The Ward, including the resource group and Log Analytics workspace.

### Screenshot
- Azure portal with resource group view
- Log Analytics workspace overview
- naming conventions and secure layout

### Why this works
It demonstrates real infrastructure-building discipline and cloud operations experience.

---

## Slide 5 — Sentinel onboarding

### Title
Microsoft Sentinel enabled

### Caption
Enabled Microsoft Sentinel and established the security monitoring foundation for the lab.

### Screenshot
- Sentinel overview page
- workspace connected
- content hub or connectors screen
- onboarding status

### Why this works
This makes the project feel operational and SIEM-focused.

---

## Slide 6 — Azure Activity validation

### Title
Validated control-plane telemetry

### Caption
Generated a real Azure control-plane event and confirmed the telemetry landed in AzureActivity.

### Screenshot
- Azure Activity connector configuration
- event generation in portal
- AzureActivity query output
- result showing telemetry landed successfully

### Why this works
It proves the telemetry pipeline is real, not hypothetical.

---

## Slide 7 — Entra ID telemetry

### Title
Identity investigation started in the same pipeline

### Caption
Connected Entra ID activity and verified AuditLogs ingestion so identity events became part of the same investigation model.

### Screenshot
- Entra ID connector status
- AuditLogs table view
- query output showing real activity
- fields like OperationName, Result, InitiatedBy, TargetResources

### Why this works
This adds identity security depth and a stronger enterprise story.

---

## Slide 8 — KQL investigation workflow

### Title
Real log investigation, not just theory

### Caption
I moved from reading about KQL to running live investigations against real telemetry and validating the data schema before assuming field names.

### Screenshot
- KQL editor with queries such as:
  - AzureActivity | where TimeGenerated > ago(24h)
  - AuditLogs | where TimeGenerated > ago(30m)
- result tables and investigation filters

### Why this works
This is one of the strongest proof points for hiring managers and SOC-focused employers.

---

## Slide 9 — AI-assisted analysis

### Title
AI as an analyst partner

### Caption
AI is used to support investigation logic, summarize findings, recommend next steps, and accelerate triage without skipping evidence-based thinking.

### Screenshot
- AI summarization of suspicious event
- recommended investigation path
- suggested KQL query
- analyst-facing reasoning output

### Why this works
This is the part that makes the project feel modern and differentiated.

---

## Slide 10 — Detection engineering

### Title
The first analytics rule

### Caption
Created the first scheduled query analytics rule, turning the environment from a logging lab into a working SIEM detection workflow.

### Screenshot
- analytics rule configuration screen
- KQL logic and rule settings
- detection schedule and alert logic

### Why this works
This is a major milestone and signals real detection engineering capability.

---

## Slide 11 — Alert and incident lifecycle

### Title
From telemetry to alert to incident

### Caption
The pipeline now supports alert generation and incident progression, setting up the next stage: investigation, response, and automation.

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
