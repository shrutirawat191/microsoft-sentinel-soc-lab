### Incident Response Report: Brute-Force Attempt Investigation

- Incident Type: Suspected Brute-Force Attempt
- SIEM Platform: Microsoft Sentinel

### Executive Summary

An incident was reported involving a suspected brute-force attempt against an account. The investigation focused on tracing additional records associated with the known source IP address using Microsoft Sentinel

### Incident Details

| Field | Details |
|---|---|
| Incident | Suspected brute-force attempt against an account |
| Target account | Not specified |
| Source IP address | `177.69.131.119` |
| Incident date | 13 oct 2026 |
| SIEM | Microsoft Sentinel |
| Log table | `SecurityEvent` |
| Event IDs investigated | `4625` |
| VirusTotal verdict | Clean |
| Confirmed account compromise | No Successful Login |
| Incident status | Closed |

### Investigation Procedure

<img width="975" height="580" alt="image" src="https://github.com/user-attachments/assets/233761f4-f98c-455d-8125-63c67aa8f0d9" />

<img width="975" height="566" alt="image" src="https://github.com/user-attachments/assets/575797e6-a036-4965-ae25-6ff28aad2ccb" />

<img width="975" height="558" alt="image" src="https://github.com/user-attachments/assets/a3ec6ea4-493c-4b51-a0cb-b4c0bfec39b4" />

Search for the Source IP in Microsoft Sentinel for additional information

                                                    let SuspectIP = "x.x.x.x";
                                                    SecurityEvent
                                                    | where IpAddress == SuspectIP
                                                    | where EventID in (4624, 4625)
                                                    | project TimeGenerated, Computer, Account, EventID, Activity, IpAddress, LogonType
                                                    | order by TimeGenerated desc

<img width="975" height="464" alt="image" src="https://github.com/user-attachments/assets/c139c3fe-68e9-4337-a768-7f9da9c84a5e" />

No successsful login was observed against this IP, Lets check Ip reputation in virustotal for addition information

<img width="975" height="388" alt="image" src="https://github.com/user-attachments/assets/9bd7a05f-2647-48b6-ad72-b4161a69f473" />

Verdict as per virustotal clean

**NOTE**: The clean verdict indicates that VirusTotal reported the IP as clean at the time of the check. This does not independently prove that the observed authentication activity was legitimate. The result should be considered alongside the available Sentinel logs.



### Investigation Findings

| Investigation Item | Finding |
|---|---|
| Suspected brute-force incident reported | Yes |
| Authentication events searched | Event IDs `4624` and `4625` |
| Failed logon count | 180 |
| Successful logon identified |0 |
| VirusTotal verdict | Clean |

### Action taken

- Added IP in blocked list.
- In this scenario, no compromise was detected but if compromise is suspected or confirmed, follow your organisation's procedures to reset credentials, revoke active sessions, and enforce MFA or stronger authentication.
- Check for further suspicious activity: no activity was found.
