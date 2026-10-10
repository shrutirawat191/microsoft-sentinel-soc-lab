# Microsoft Sentinel SOC Lab

A hands-on learning portfolio documenting Microsoft Sentinel configuration and SOC workflows in an Azure lab environment.


## Lab objectives

- Set up an Azure resource group, Log Analytics workspace (LAW), and Microsoft Sentinel.
- Explore data connectors and Windows event log ingestion.
- Integrate threat intelligence sources, including PulseDive via the available Content Hub/data-connector workflow.
- Review Microsoft Defender Threat Intelligence integration and Indicators of Compromise (IoCs).
- Explore KQL-based threat hunting and scheduled analytics rules.
- Understand how Sentinel playbooks/Logic Apps and Workbooks can support incident response and SOC monitoring.

## Technologies and Tools

- Microsoft Azure
- Microsoft Sentinel
- Azure Log Analytics
- Microsoft Defender Threat Intelligence
- PulseDive
- Windows Event Viewer
- Kusto Query Language (KQL)
- Azure Logic Apps
- Sentinel Playbooks

## Repository structure

- `screenshots/` — images extracted from the original lab document. 
- `projects/` — individual lab write-ups and evidence checklists.
- `queries/` — a starter KQL query file.

## Lab environment

The lab uses an Azure environment with a Resource Group (RG) and Log Analytics Workspace (LAW).

Microsoft Sentinel is used to explore security monitoring, threat detection, and incident response workflows.

Some exercises depend on connector availability, permissions, licensing, and Azure subscription capabilities. The completion status of each activity is documented separately.

## Projects

1. [Azure Sentinel setup](projects/01-azure-sentinel-setup.md)
2. [Data connectors](projects/02-data-connectors.md)
3. [Threat intelligence and IoCs](projects/03-threat-intelligence.md)
4. [Windows log ingestion](projects/04-windows-log-ingestion.md)
5. [Threat detection with KQL](projects/05-threat-detection-kql.md)
6. [Automation](projects/06-automation.md)
7. [Visualize security data](projects/07-Visualize-Security-Data-in-MS-Sentinel.md)
