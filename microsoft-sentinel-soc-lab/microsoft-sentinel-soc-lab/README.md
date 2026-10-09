# Microsoft Sentinel SOC Lab

A hands-on learning portfolio documenting Microsoft Sentinel configuration and SOC workflows in an Azure lab environment.

> **Portfolio accuracy note:** This repository documents the activities described in the lab notes. Only claim a step as completed when you have verified it in your own Azure environment and can explain the configuration and results. Some steps may be limited by student-subscription permissions.

## Lab objectives

- Set up an Azure resource group, Log Analytics workspace (LAW), and Microsoft Sentinel.
- Explore data connectors and Windows event log ingestion.
- Integrate threat intelligence sources, including PulseDive via the available Content Hub/data-connector workflow.
- Review Microsoft Defender Threat Intelligence integration and Indicators of Compromise (IoCs).
- Explore KQL-based threat hunting and scheduled analytics rules.
- Understand how Sentinel playbooks/Logic Apps and Workbooks can support incident response and SOC monitoring.

## Repository structure

- `screenshots/` — images extracted from the original lab document. Review each image and rename it to a descriptive filename before publishing.
- `projects/` — individual lab write-ups and evidence checklists.
- `queries/` — a starter KQL query file. Validate table names and schema in your workspace before running queries.

## Lab environment

- Cloud platform: Microsoft Azure
- SIEM: Microsoft Sentinel
- Log storage/querying: Log Analytics workspace
- Threat intelligence mentioned in notes: PulseDive and Microsoft Defender Threat Intelligence
- Query language: Kusto Query Language (KQL)

## Projects

1. [Azure Sentinel setup](projects/01-azure-sentinel-setup.md)
2. [Data connectors](projects/02-data-connectors.md)
3. [Threat intelligence and IoCs](projects/03-threat-intelligence.md)
4. [Windows log ingestion](projects/04-windows-log-ingestion.md)
5. [Threat detection with KQL](projects/05-threat-detection-kql.md)
6. [Automation and workbooks](projects/06-automation-and-workbooks.md)

## How to use this repository

1. Read the project notes and compare them with your actual lab configuration.
2. Rename screenshots so filenames match the evidence shown.
3. Add a short **What I did / What I observed / Troubleshooting** section to each project.
4. Add sanitized screenshots of successful configuration and query results.
5. Remove any secrets, API keys, tenant IDs, subscription IDs, email addresses, public IPs, or other sensitive information before publishing.

## Limitations and honesty

The source notes mention that some threat-intelligence steps could not be completed under a student Azure subscription. Mark these steps as **attempted**, **partially completed**, or **not completed** as appropriate. Do not describe an integration or automation as working unless you verified it.

## Suggested resume entry

**Microsoft Sentinel SOC Lab | Azure, Microsoft Sentinel, KQL, Threat Intelligence**
- Built and documented a hands-on Microsoft Sentinel lab covering workspace setup, log ingestion, threat-intelligence connector exploration, and KQL-based detection workflows.
- Practiced reviewing IoCs, Windows event logs, and scheduled analytics-rule concepts; documented configuration steps and lab limitations.

Edit these bullets to include only tasks you personally completed and validated.
