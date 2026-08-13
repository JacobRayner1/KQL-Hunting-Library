# Extract Entity information when auditing alert rule changes in Sentinel

## Description

This script can be used when looking to extract alert rule information like query and description

Table: 
`_SentinelAudit`

## Query

```kusto
_SentinelAudit()
| where OperationName contains "Microsoft.SecurityInsights/alertRules/Delete"
| extend EP = todynamic(ExtendedProperties)
| extend ORS = parse_json(tostring(EP["OriginalResourceState"]))
| project
    TimeGenerated, SentinelResourceName,
    Query = tostring(ORS["properties"]["query"]),
    Descrption = tostring(ORS["properties"]["description"])
```

## Comments

Operation name can be expanded to capture further activity beyond 'Delete' and project can be expanded to gather more items:

    RuleName = tostring(ORS["properties"]["displayName"]),
    Description = tostring(ORS["properties"]["description"]),
    Severity = tostring(ORS["properties"]["severity"]),
    Enabled = tostring(ORS["properties"]["enabled"]),
    Query = tostring(ORS["properties"]["query"]),
    QueryFrequency = tostring(ORS["properties"]["queryFrequency"]),
    QueryPeriod = tostring(ORS["properties"]["queryPeriod"]),
    Tactics = tostring(ORS["properties"]["tactics"]),
    Techniques = tostring(ORS["properties"]["techniques"])
