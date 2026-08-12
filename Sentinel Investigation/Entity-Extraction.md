# Extract Entity information when investigating security alerts.

## Description

This script can be used when looking to extract command line entity information from default system alerts. This can be particularly useful when investigating Multi-stage incidents where entity information is nested in the alert output

Table: 
`SecurityAlert`

## Query

```kusto
SecurityAlert
| summarize arg_max(TimeGenerated, *) by SystemAlertId
| where SystemAlertId in (<Alert IDs>)
| extend Entities = todynamic(Entities)
| mv-expand Entities
| extend
    EntityType = tostring(Entities.Type),
    CommandLine = tostring(Entities.CommandLine),
    ParentProcess = tostring(Entities.ParentProcess.ImageFile)
| where isnotempty(CommandLine)
| project
    SystemAlertId,
    EntityType,
    CommandLine,
    ParentProcess
```

## Comments


