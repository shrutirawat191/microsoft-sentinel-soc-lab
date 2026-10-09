# 3. Threat Intelligence and IoCs

## Objective
Explore threat-intelligence integration with Microsoft Sentinel.

## Sources and concepts in the lab notes
- PulseDive threat-intelligence platform.
- STIX (Structured Threat Information eXpression), a format for representing threat intelligence.
- TAXII (Trusted Automated eXchange of Intelligence Information), a protocol for exchanging STIX data.
- Microsoft Defender Threat Intelligence connector and IoCs.

## Procedure
1. Review the relevant Content Hub solution and connector prerequisites.
2. Configure the source only using authorized credentials and supported settings.
3. Never commit API keys, passwords, tokens, or other secrets to GitHub.
4. Check whether the integration successfully ingests indicators.
5. Record the actual result and any subscription/permission limitations.

## Validation and evidence
- Sanitized connector setup screenshot.
- Query results showing indicators, if ingestion succeeded.
- If the student subscription blocked setup, document the exact limitation and label the integration as attempted or partially completed.

## Results
- **Status:** Update to your actual result.
- **What I learned:** Explain how IoCs can support threat hunting and alert enrichment.
