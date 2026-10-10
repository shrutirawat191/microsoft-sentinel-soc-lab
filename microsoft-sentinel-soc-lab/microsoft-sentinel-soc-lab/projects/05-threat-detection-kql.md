# 5. Threat Detection (Analytics) in Microsoft Sentinel

## Objective
Analytics in Microsoft Sentinel are automated rules and processes that analyze security data to detect suspicious activities or threats. They use built-in or custom queries to continuously monitor logs and trigger alerts, helping security teams identify and respond to potential attacks quickly and efficiently.


## Schedule a Query Rule

<img width="975" height="443" alt="image" src="https://github.com/user-attachments/assets/015c0984-afea-48f3-8e57-4978b6e09b6a" />

_Describe the Rule (Ex: Brute Force)_

1. Include severity and MITRE ATT&CK Technique
      a. MITRE ATT&CK is a globally recognized knowledge base that catalogs and describes the tactics, techniques, and procedures used by cyber attackers. It helps security professionals
         understand how adversaries operate, enabling better detection, prevention, and response to cyber threats by providing a detailed framework of attacker behaviors across different           stages of an attack.
   
2. For MITRE ATT&CK, I selected initial access (attacker tries to gain entry) and credential access (attacker attempts to gain valid credentials)
                 a. T1110 - Brute Force
                 b. T1110.001 - Password Guessing
                 c. T1110.002 - Password Spraying

<img width="975" height="750" alt="image" src="https://github.com/user-attachments/assets/6fdfae7b-af52-49bc-abd9-e608d25579bf" />

_Create a Rule Query_

Use the following query:
                      SecurityEvent
                      |where EventID == 4625
                      |project TimeGenerated, Account, EventID, IpAddress
                      |where IpAddress != "-"
                      |summarize count() by Account, EventID, IpAddress, bin(TimeGenerated, 1m)
                      |where count_ >= 5

This query searches for failed login events (EventID 4625) in SecurityEvent logs, extracts the IP address involved in each failure, then counts how many times each account is targeted from each IP address within 1-minute intervals. It filters to show only cases where there are 5 or more failed attempts in one minute from the same IP and account, which helps identify
possible brute force attacks.

Complete the remaining steps and create the rule

<img width="975" height="426" alt="image" src="https://github.com/user-attachments/assets/ad730d64-8555-4b8e-897a-400880b1c2be" />

<img width="975" height="444" alt="image" src="https://github.com/user-attachments/assets/6fff2242-3dd0-4c35-86d0-5b4e41f59e0d" />


Check Incidents Tab
Any incidents relating to a brute force attack will now be reported in Incidents & Alerts > Incidents
After Brute Force Attack:

<img width="975" height="442" alt="image" src="https://github.com/user-attachments/assets/4c0ea3b5-2c3f-4db3-91cf-0ff9d49e5a7e" />

<img width="975" height="466" alt="image" src="https://github.com/user-attachments/assets/87c56ff7-577a-4122-b468-ecb1a4b68d52" />

### Create NRT Query Rules

Near Real-Time analytic rules are designed to detect and alert on suspicious activity within a minute or so of the event being ingested, instead of running on a schedule like regular analytic tools.
These rules should be used for account compromise attempts, malware beaconing, privilege escalation, suspicious login locations, ransomware indicators, and more.
It’s important to note that these can generate more alerts if not tuned properly, so filtering with precise KQL queries is important.
In this example, we will create a rule for Audit Logs being cleared in a critical server. This is a strong indicator of malicious activity, as attackers often do cover their tracks after gaining access.

MITRE ATT&CK Mappings:
• T1070.001 – Indicator Removal on Host: Clear Windows Event Logs
• T0872 – Indicator Removal on Host
• T1630—Indicator Removal on Host
• TA0005 – Defense Evasion

<img width="975" height="516" alt="image" src="https://github.com/user-attachments/assets/58a03a88-a76b-4d85-9308-e6332b8d1ada" />

<img width="975" height="515" alt="image" src="https://github.com/user-attachments/assets/e306d7be-7ce6-42a2-8766-5e72820f2437" />

<img width="975" height="514" alt="image" src="https://github.com/user-attachments/assets/c5de0f2a-89a1-4b75-80fb-b6c76fae291d" />

This query finds all cases where the Windows Security Audit Log was cleared, and lists the computer name, event details, and activity description.

<img width="975" height="379" alt="image" src="https://github.com/user-attachments/assets/502b9db9-2145-4e5b-809d-b746be7ea3e4" />

**Test the NRT Rule**

Cleared logs on my VM

<img width="975" height="670" alt="image" src="https://github.com/user-attachments/assets/90aa4d44-50b7-41c1-a095-d6ea74ad29be" />

Checked Incidents, and sure enough an incident was reported

<img width="975" height="541" alt="image" src="https://github.com/user-attachments/assets/8d7b9dad-063d-4bd0-9b9c-90851a199fd7" />

<img width="975" height="459" alt="image" src="https://github.com/user-attachments/assets/d6801cb4-33ff-4843-bdc1-c6909f0b543d" />

**Next Steps as a SOC Analyst**

• Triage the incident
  o Check the incident details to get the machine name, username, time of event, and any other related information.
  o Confirm it’s not a false positive (Was this done by the IT department during maintenance?)
  
• Investigate in depth
  o Run a query to see what happened right before the log was cleared
  o Look for suspicious logon events, privilege changes, multiple failed logins, etc.
  
• Correlate with other Data Sources
  o Check Defender for Endpoint, firewall logs, or more.
  o Look for file access, PowerShell commands, or process creation events around the same time.
  
• Determine severity
  o Escalate to incident response if necessary
  
• Document everything
  o Add investigation steps, findings, and decision-making to the incident record
  o Include all information found
  
• Take preventative measures
  o Learn from the experience, and take measures to prevent it in the future
