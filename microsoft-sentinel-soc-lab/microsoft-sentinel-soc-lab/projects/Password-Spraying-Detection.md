### OVERVIEW

This project demonstrates how to detect potential password-spraying activity using Microsoft Sentinel and Kusto Query Language (KQL).

Password spraying is an authentication attack pattern in which an actor attempts a small number of passwords against multiple accounts. This detection identifies a source IP address associated with failed logons across five or more distinct accounts within a 15-minute time window.

Objective: Create and validate a Microsoft Sentinel analytics rule that identifies suspicious failed-logon patterns and generates an alert or incident for investigation.

### Lab Environment

- SIEM: Microsoft Sentinel
- Log source: Windows Security Events
- Detection language: Kusto Query Language (KQL)
- Testing environment: Isolated Windows Active Directory lab
- Test accounts: Dedicated, non-privileged lab accounts

### Configuring the Analytics Rule

The rule configuration includes a descriptive name, a detection description, severity, MITRE ATT&CK mapping where applicable, and the query used to identify the activity.

<img width="975" height="578" alt="image" src="https://github.com/user-attachments/assets/1689d053-920f-4d72-aca2-ec146eacafb2" />

<img width="975" height="485" alt="image" src="https://github.com/user-attachments/assets/6a631c0f-8bef-4946-99ef-fe5a3dd3f315" />

Query:

                                SecurityEvent
                                | where EventID == 4625
                                | where isnotempty(IpAddress) and IpAddress != "-"
                                | where isnotempty(TargetAccount)
                                | summarize FailedAttempts = count(), TargetedAccounts = dcount(TargetAccount), Accounts = make_set(TargetAccount, 50), FirstSeen = min(TimeGenerated), LastSeen = max(TimeGenerated) by IpAddress, bin(TimeGenerated, 15m)
                                | where TargetedAccounts >= 5
                                | order by TargetedAccounts desc


<img width="975" height="460" alt="image" src="https://github.com/user-attachments/assets/8fc9f453-6ba9-4e1d-8dfd-0523f53c9413" />

### Creating the Lab Test Accounts

To validate the detection, I prepared dedicated test accounts in Active Directory.

- Created a Lab-Testing organizational unit.

<img width="975" height="663" alt="image" src="https://github.com/user-attachments/assets/6ade560f-5f6b-4b10-a3a2-a8538b57d2fa" />

- Created non-privileged test accounts within the lab OU.

<img width="975" height="664" alt="image" src="https://github.com/user-attachments/assets/fb373ca7-0b1e-4681-8bd3-4d551a4ca3e6" />

- Confirmed the test accounts were visible in Active Directory Users and Computers.

<img width="975" height="683" alt="image" src="https://github.com/user-attachments/assets/f97fd098-e31b-43c2-a06f-e794b7e141fe" />


### Testing

- Opened the Windows sign-in screen.
- Selected Other user.
- Used a dedicated lab test account.
- Entered an intentionally incorrect password for the test.

<img width="975" height="448" alt="image" src="https://github.com/user-attachments/assets/dd15d611-7695-49e1-8983-ac572c1653f9" />

<img width="975" height="425" alt="image" src="https://github.com/user-attachments/assets/cdc3c9f1-1ae2-46ad-b589-f757fd9c03d3" />

### Post Incident Measures

- Review the source IP address and the affected accounts.
- Check the number and timing of failed logons.
- Look for successful logons from the same source IP around the alert time.
- Determine whether the source is a known, trusted system or an unexpected source.
- Correlate the activity with other endpoint, identity, and authentication events.
- Escalate confirmed suspicious activity according to the organization's incident-response process.
