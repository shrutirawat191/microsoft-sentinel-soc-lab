# 4. Windows Log Ingestion

## Objective
Configure a Data Collection Rule (DCR) in Azure Monitor to collect Windows event logs from a Windows virtual machine and send them to a Log Analytics workspace used by Microsoft Sentinel.

## Procedure

We have a VM windows in place in cental india region **VM= Windows01**

_Create a Data Collection Rule_
- Opened the Azure portal and navigated to Monitor → Data Collection Rules.
- Selected Create to configure a new Data Collection Rule.
- Entered Windows as the Data Collection Rule name.
- Selected the Azure for Students subscription.
- Selected the resource group mySentinelRG.
- Set the region to Central India.
- Selected Agent-based – Windows or Linux as the telemetry type.
- Left the user-assigned managed identity option disabled in this configuration.

<img width="748" height="598" alt="image" src="https://github.com/user-attachments/assets/ff8035f0-b6c4-45fc-83c0-a41c444158d9" />

<img width="994" height="450" alt="image" src="https://github.com/user-attachments/assets/2ddc1951-cb58-4d57-85cc-03c3bedf4fdb" />

_Configure Windows Event Logs_
- Opened the Collect and deliver section and selected Add new data source.
- Selected Windows Event Logs as the data source type.
- Chose Custom as the Event Log Selection Mode to specify which event logs to collect.
- Configured the event log collection entries shown in the screenshot:
                    Microsoft-Windows-Windows Defender/Operational!*
                    Microsoft-Windows-Sysmon/Operational!*
                    Microsoft-Windows-PowerShell/Operational!*
- These event channels provide telemetry that can support endpoint security monitoring, process-related investigations, and PowerShell activity analysis.

<img width="1023" height="584" alt="image" src="https://github.com/user-attachments/assets/815b95ed-e071-4396-8638-8795ed600b9b" />

<img width="1030" height="593" alt="image" src="https://github.com/user-attachments/assets/c2b39344-0a4a-467d-9c60-705b2ea46d75" />

_Review the Windows VM_
- Opened Task Manager on the Windows virtual machine.
- Reviewed the running applications and background processes to confirm access to the Windows environment being configured for log collection.

<img width="769" height="580" alt="image" src="https://github.com/user-attachments/assets/d72426aa-b52c-4853-a81b-41e814f6e033" />

<img width="975" height="531" alt="image" src="https://github.com/user-attachments/assets/6d4f83d4-6fc4-49f3-854b-52b262c844e7" />

**Verification:**
To verify data ingestion, open the Log Analytics workspace connected to Microsoft Sentinel and run a query against the relevant table. For example:

                                      Event
                                      | where TimeGenerated > ago(1h)
                                      | summarize Events = count() by EventLog
                                      | order by Events desc

<img width="1142" height="522" alt="image" src="https://github.com/user-attachments/assets/e9127150-92f2-4a88-abb5-3cb6894a9eb2" />


- **Events observed:** Add only what you verified.
- **Troubleshooting:** Document missing logs, permissions, or connectivity issues.
