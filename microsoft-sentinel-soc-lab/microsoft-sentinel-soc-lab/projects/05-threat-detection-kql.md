# 5. Threat Detection with KQL

## Objective
Explore KQL queries and scheduled analytics rules for SOC detection workflows.

## Workflow
1. Confirm which tables are available in your workspace.
2. Write and test a query against actual lab data.
3. Review matching events and tune the time range and filters.
4. If appropriate, create a scheduled analytics rule with a meaningful name, severity, and entity mappings.
5. Validate the rule using safe test data or document that end-to-end validation was not performed.

## KQL starter example

```kusto
// Inspect recent Windows security events if SecurityEvent is available.
SecurityEvent
| where TimeGenerated > ago(24h)
| summarize EventCount = count() by EventID
| order by EventCount desc
```

This is an exploratory query, not a malicious-activity detection rule. It will only work if the `SecurityEvent` table exists and contains data in your workspace.

## Evidence to add
- Query editor with the query.
- Results pane.
- Analytics rule configuration and generated incident, if actually tested.

## Results
- **Status:** Update to your actual result.
- **Detection logic:** Explain the behavior you intended to detect.
- **Validation:** Record what happened during testing.
