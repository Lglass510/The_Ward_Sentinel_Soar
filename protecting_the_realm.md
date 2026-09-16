# Protecting the Realm

## Date
2026-09-16

## Objective
Create a clean, dedicated Azure security working area for The Ward and establish the foundation for security monitoring in Microsoft Sentinel and Microsoft Defender for Cloud using Azure Activity telemetry.

## What I accomplished

Today I created the Azure resource group for The Ward and used it as the single working space for Azure security operations. I established the connection between the Azure workspace and Microsoft Sentinel, and I configured Azure Activity so it is part of the Microsoft Defender / Sentinel monitoring model.

This is the spot I want to work out of going forward for Azure security work. The goal is to keep all relevant telemetry, configuration, and evidence in one place instead of bouncing across disconnected resources or incomplete setups.

## Why this mattered

I spent a lot of time fighting misconfiguration, misunderstanding, and the wrong mental model for how Azure security telemetry is connected. The main issue was not just the platform itself but the confusion between:

- Azure Activity logs
- Microsoft Defender for Cloud
- Microsoft Sentinel workspaces
- Log Analytics / diagnostic settings
- resource group organization and operational scope

The fix was to build a deliberate Azure security baseline instead of trying to patch together ad hoc pieces. The ward now represents a more intentional structure for Azure security monitoring, evidence retention, and future detection work.

## Environment setup

- Azure subscription with a dedicated resource group named The Ward
- Microsoft Sentinel workspace connected to the Azure environment
- Azure Activity configured to feed security monitoring and investigation workflows
- Microsoft Defender integration aligned to the central operational area

## Configuration approach

1. Create a dedicated Azure resource group for The Ward.
2. Place the operational Azure security workspace in that resource group.
3. Connect Microsoft Sentinel to the workspace and validate the environment is operational.
4. Configure Azure Activity to send relevant telemetry into the monitoring path.
5. Align the environment with Microsoft Defender so Azure security work flows through one consistent security posture.
6. Use this setup as the central place for all future Azure security investigation and detection work.

## Lessons learned

- The resource group is more than just storage; it is the backbone of an organized security workflow.
- Azure Activity, Sentinel, and Defender are not interchangeable, but they need to be aligned intentionally.
- Misunderstandings often come from treating each Azure security feature as an isolated tool instead of a connected monitoring architecture.
- A clean workspace and naming structure reduces the confusion that comes from fragmented or accidental configuration.
- It is better to slow down and build the right operational foundation than to keep chasing broken settings.

## Operational direction

Going forward, The Ward is the only place I want to work out of for Azure security. That means:

- all Azure security work lives in The Ward resource group and workspace
- Sentinel remains the central security monitoring plane
- Azure Activity is part of the evidence and detection pipeline
- Microsoft Defender is part of the same operating model
- future work stays organized around one repeatable security workflow instead of scattered experiments

## Success criteria

This effort is considered successful when the environment is stable, the Azure telemetry path is clear, and security work can proceed from a single baseline without constant reset or reconfiguration.

## Future milestones

- validate telemetry flow and confirm event visibility
- build detection logic in Sentinel
- tune investigation workflows
- connect responses and evidence tracking
- turn the Ward into a repeatable Azure security operations base

## Closing note

This is not a perfect environment yet, but it is a real and useful foundation. The biggest win today was creating the right structure and removing the confusion that was slowing the work down. The Ward is now the place where the Azure security story begins.
