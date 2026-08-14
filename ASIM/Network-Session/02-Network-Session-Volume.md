# Gather traffic volume information around the time of the alert

## Description

This is used to gather some immediate information as to the traffic volume around the time of the alert. We can also use this as a means of confirming the schema that we can use for further investigation
## Query

```kusto
let AlertTime = datetime(2099-01-01T22:42:53.8565818Z);

_Im_NetworkSession
| where TimeGenerated between (
    AlertTime - 60m .. AlertTime + 15m
)
| summarize Sessions=count()
    by bin(TimeGenerated, 10m)
| order by TimeGenerated asc
```

## Comments

Adjust the date time as required to match the time of the system alert
