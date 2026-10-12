### Detecting Active Directory Delegation Changes with Microsoft Sentinel

### Overview
This hands-on lab focuses on detecting Active Directory delegation-related changes using Microsoft Sentinel. 
It covers enabling auditing on a domain controller, writing a custom KQL query, configuring a scheduled analytics rule, and validating detection using test accounts in a lab environment.

### Lab Environment
- SIEM: Microsoft Sentinel
- Operating System: Windows Server 2025
- Active Directory Domain: sentinel.local
- Test Computer: Client VM (domain-joined)
- Service Principal Name (SPN): HTTP/labweb.sentinel.local

All testing should be performed in an isolated lab using disposable, non-privileged accounts.

### Enable Auditing on the Domain Controller

- Open Group Policy Management using gpmc.msc.

<img width="975" height="691" alt="image" src="https://github.com/user-attachments/assets/c31d4400-a2c4-44b6-aab7-00825e68c9b4" />

- Edit the policy applied to the Domain Controllers OU.

<img width="975" height="687" alt="image" src="https://github.com/user-attachments/assets/c1f2dd37-5461-4c78-92e8-36ce12138d03" />

- Navigate to:  Advanced Audit Policy Configuration → System Audit Policies → DS Access

<img width="975" height="690" alt="image" src="https://github.com/user-attachments/assets/2f6c1c51-0718-499c-ab54-f9f3fa95331d" />

- Enable Audit Directory Service Changes for Success.

<img width="975" height="677" alt="image" src="https://github.com/user-attachments/assets/7655081d-160c-4f3a-8e4f-7cc4fb2c3b01" />

<img width="975" height="684" alt="image" src="https://github.com/user-attachments/assets/2e0251b7-e311-4100-b8c2-4ea8ed1a41a8" />

<img width="975" height="721" alt="image" src="https://github.com/user-attachments/assets/5df09720-c4b8-4d6b-9adb-a4a9dbdb0092" />

<img width="975" height="720" alt="image" src="https://github.com/user-attachments/assets/6ffa6435-c895-43f5-bb79-7d876ebfd522" />

- Apply the policy and verify that the updated settings are active.

<img width="974" height="400" alt="image" src="https://github.com/user-attachments/assets/40ae724b-044f-47fb-a980-d3bb594ea689" />

### Create the KQL Detection Query

The following query searches Windows Security events for the AllowedToDelegateTo field.

                                              let exclusions = dynamic(["-", "0x0"]);
                                              SecurityEvent
                                              | where EventData contains "AllowedToDelegateTo"
                                              | extend AllData = tostring(parse_xml(EventData))
                                              | extend DelegatedTo = parse_json(AllData)['EventData']['Data'][20]["#text"]
                                              | where not (DelegatedTo in (exclusions))

**Note**: The extraction using Data[20] must be validated against the actual event payload in your environment. XML field ordering can vary, so confirm that the extracted value corresponds to AllowedToDelegateTo before relying on this query.

### Create a Scheduled Analytics Rule

- Navigate to Analytics.
- Create a new scheduled analytics rule.

<img width="975" height="492" alt="image" src="https://github.com/user-attachments/assets/911e36f6-d255-45a8-a5d5-01e597f2afc2" />

- Add the KQL detection query.

<img width="975" height="346" alt="image" src="https://github.com/user-attachments/assets/e86edb7f-5b4e-4312-acd6-1b4179636cc9" />

- Configure the rule schedule and lookup period.
- Configure alert details and entity mapping where appropriate.
- Save and enable the rule.

<img width="975" height="435" alt="image" src="https://github.com/user-attachments/assets/036843ef-10f2-447d-bd03-795ebdcd3cab" />


### Verification

Create a disposable service account and acquire SPN

<img width="808" height="489" alt="image" src="https://github.com/user-attachments/assets/d7cc6f0c-d3b6-4189-816e-f656442aeeb2" />

<img width="975" height="161" alt="image" src="https://github.com/user-attachments/assets/508d9fd3-5004-449a-9569-2a3d019e565c" />

SPN: HTTP/labweb.sentinel.local

Make changes in domain joined ClientVM delegation properties to trigger the alert

<img width="975" height="514" alt="image" src="https://github.com/user-attachments/assets/755c777f-bbfd-4000-950a-9228afabedec" />

<img width="736" height="828" alt="image" src="https://github.com/user-attachments/assets/500d0d1d-b369-4c1c-8209-14a62a90643c" />

<img width="728" height="822" alt="image" src="https://github.com/user-attachments/assets/8e4f45c5-8105-4b3e-8185-6b2aa5a95854" />

<img width="638" height="641" alt="image" src="https://github.com/user-attachments/assets/2c7d770d-85a8-4895-acbe-3eebb0c475a6" />

<img width="730" height="830" alt="image" src="https://github.com/user-attachments/assets/21ca51b2-dc09-479a-91b4-3275113131ed" />


**Incident**

<img width="975" height="502" alt="image" src="https://github.com/user-attachments/assets/79225761-c328-4011-8053-f922ae01a011" />

<img width="975" height="676" alt="image" src="https://github.com/user-attachments/assets/f03d8a70-3088-438b-a003-644de58ee69f" />


