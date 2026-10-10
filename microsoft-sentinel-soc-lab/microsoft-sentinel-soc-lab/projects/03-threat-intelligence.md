# 3. Threat Intelligence and IoCs

## Objective
Explore threat-intelligence integration with Microsoft Sentinel.

## Background
Threat intelligence helps security analysts investigate suspicious indicators and understand potential malicious activity.
An Indicator of Compromise (IoC) may include an IP address, domain, URL, file hash, or another observable associated with suspicious or malicious activity.
PulseDive was selected as the threat intelligence platform in this lab.

## Sources and concepts in the lab notes
- PulseDive threat-intelligence platform.
- STIX (Structured Threat Information eXpression), a format for representing threat intelligence.
- TAXII (Trusted Automated eXchange of Intelligence Information), a protocol for exchanging STIX data.
- Microsoft Defender Threat Intelligence connector and IoCs.

## Procedure
1. Open the PulseDive platform.

<img width="975" height="467" alt="image" src="https://github.com/user-attachments/assets/b264b8f5-97f5-41d5-a3b6-ebfa9ba88510" />

2. Review the account or integration settings referenced in the lab.
 
   <img width="975" height="569" alt="image" src="https://github.com/user-attachments/assets/e3841860-f493-49fd-9880-f2957dcebe4c" />

3. Open Microsoft Sentinel and explore the Content hub.
4. Locate the relevant threat intelligence solution or connector.
 
   <img width="975" height="439" alt="image" src="https://github.com/user-attachments/assets/a92792f4-c0cc-435d-9b93-f7b71a7bde42" />

5. Review its prerequisites and supported integration method.
6. Configure the integration 
 
   <img width="975" height="544" alt="image" src="https://github.com/user-attachments/assets/eb433a88-0df9-4dd6-acd7-fac28f51c2d6" />
                                  _Password is the api key found under account section_ 
 
   <img width="975" height="188" alt="image" src="https://github.com/user-attachments/assets/1f3efd32-5ed1-4a51-a0ba-a8dae089903a" />

7. Check connector status and verify whether threat intelligence records are available in the workspace.

    <img width="498" height="650" alt="image" src="https://github.com/user-attachments/assets/d79c19cd-f791-4642-ab76-85ea57ab9a56" />

