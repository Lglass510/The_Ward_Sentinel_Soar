 # ReaperSOC Lab

ReaperSOC is a personal security operations lab used to practice, document, and demonstrate the skills I am building on my journey toward earning CompTIA Security+.

The lab is a hands-on environment for learning how security teams monitor systems, investigate alerts, respond to incidents, and improve their processes. Each exercise should leave behind enough notes and evidence to explain what was attempted, what happened, and what I learned.

## Goals

- Build practical experience with security monitoring and incident response.
- Reinforce Security+ topics through repeatable, hands-on exercises.
- Learn how SIEM and SOAR platforms support detection, investigation, and response.
- Create automation playbooks that are understandable, testable, and safe to run.
- Document both successful outcomes and failures instead of recording only the final result.
- Develop a portfolio of lab work that demonstrates technical growth over time.

## Current Lab Focus

The next milestone is to use SIEM and SOAR tools to:

1. Collect or ingest security-relevant logs.
2. Create or tune a detection and generate a test alert.
3. Investigate the alert and record the relevant evidence.
4. Build an automated SOAR playbook for a defined response.
5. Test the playbook with safe, authorized lab activity.
6. Record successes, failures, limitations, and improvements.

The playbook should begin with a clear trigger and include appropriate validation, decision points, actions, and a final record of the result. Automation must be limited to this isolated lab and should avoid destructive actions unless they are explicitly required by the exercise.

## Lab Topology

The current environment includes:

| System | Role |
| --- | --- |
| Rocky Linux (`reaper1`) | Linux workstation and SSH client |
| DC1 | Windows domain controller and SSH target |
| VS Code | Remote administration and documentation environment |

See [SSH/sshconfig.md](SSH/sshconfig.md) for the remote administration setup.

## Suggested Learning Areas

- Networking, ports, protocols, and segmentation
- Identity, authentication, authorization, and account management
- Windows and Linux administration
- Log sources, parsing, normalization, and detection logic
- Vulnerability and configuration management
- Incident response processes and evidence handling
- SIEM dashboards, searches, alerts, and correlation rules
- SOAR integrations, playbooks, enrichment, and response actions
- Security controls, risk, governance, and operational documentation

## Exercise Documentation

Each exercise should answer the following questions:

- **Objective:** What skill or Security+ topic is being practiced?
- **Scenario:** What happened, and why does it matter?
- **Environment:** Which systems, tools, and accounts were involved?
- **Procedure:** What steps were performed?
- **Evidence:** What logs, alert details, commands, screenshots, or timestamps support the result?
- **Result:** What worked, what failed, and what was unexpected?
- **Lessons learned:** What would be changed in a production environment or on the next attempt?
- **Cleanup:** What data, rules, accounts, integrations, or test artifacts were removed or reset?

## SIEM/SOAR Playbook Record

For each playbook, document:

| Field | Description |
| --- | --- |
| Name and version | A clear name and revision number |
| Trigger | The alert, event, or condition that starts the playbook |
| Inputs | Fields and context required from the SIEM or integration |
| Enrichment | Lookups or context added during investigation |
| Decisions | Conditions that determine the next action |
| Actions | Notifications, tickets, containment, or other responses |
| Safeguards | Approval gates, allowlists, rate limits, and failure handling |
| Expected result | The outcome that indicates a successful run |
| Test result | Actual behavior, including errors and skipped steps |
| Improvements | Changes planned for the next version |

Example playbook ideas include enriching a suspicious IP, notifying an analyst when a detection fires, opening an incident ticket, or requiring analyst approval before containment. Start with reversible actions and expand only after the workflow is understood.

## Repository Structure

As the lab grows, organize work by topic or exercise. A possible structure is:

```text
ReaperSOC/
├── README.md
├── SSH/
│   └── sshconfig.md
├── SIEM/
│   └── <exercise-notes>.md
├── SOAR/
│   └── <playbook-notes>.md
├── Detection Engineering/
│   └── <detection-notes>.md
└── Evidence/
	└── <sanitized-artifacts>/
```

Keep each exercise self-contained when possible. Use sanitized screenshots and sample data that do not expose personal information, real credentials, private keys, public IP addresses, or other sensitive details.

## Security and Safety

- Perform testing only on systems and accounts I own or am explicitly authorized to use.
- Keep the lab isolated from production and unnecessary external networks.
- Never commit passwords, tokens, private keys, or unredacted logs to this repository.
- Use least-privilege accounts and temporary test data.
- Add approval or confirmation steps before high-impact automated actions.
- Clean up test alerts, accounts, rules, and integrations after each exercise.
- Sanitize evidence before sharing it publicly.

## Progress

- [x] Build the initial Rocky Linux and DC1 SSH administration path
- [ ] Configure or select a SIEM for lab log collection
- [ ] Create and test a SIEM detection
- [ ] Select a SOAR tool or integration
- [ ] Build and test the first automated playbook
- [ ] Document successful and failed playbook runs
- [ ] Review the exercise against relevant Security+ objectives

## What Success Looks Like

Success is not limited to a playbook completing without errors. A successful exercise produces a repeatable workflow, explains why each action exists, captures useful evidence, identifies limitations, and records how the process could be made safer or more effective.
