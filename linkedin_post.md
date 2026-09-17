Today was a real Azure security milestone for The Ward.

I finally moved from portal confusion into a working telemetry-to-detection pipeline.

I created the resource group, built the Log Analytics workspace, enabled Microsoft Sentinel, connected Azure Activity, validated Entra ID audit logs, ran live KQL investigations, and created the first scheduled analytics rule.

That is the point where The Ward stopped being a concept and started becoming a real lab for detection engineering and investigation work.

The biggest lesson was not just learning Azure — it was learning that the real problem was the lack of a clean operational model. Once the telemetry flow and workspace structure were aligned, progress became much more tangible.

I also had a helpful reminder that in security work, not every schema or table name matches the docs exactly. The habit that mattered most was inspecting the data you actually have before assuming the query you want to write.

This is the foundation for the next phase: alert validation, incident investigation, and automation.

I’m documenting the work as I go, and The Ward is now the place where this Azure security story is being built.

#Azure #AzureSecurity #MicrosoftSentinel #MicrosoftDefender #CloudSecurity #CyberSecurity #ThreatDetection #SIEM #KQL #SecurityOperations #ContinuousLearning #SOC
