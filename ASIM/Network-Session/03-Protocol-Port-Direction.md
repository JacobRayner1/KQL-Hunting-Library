# Establish a general baseline to determine what network activity actually existed around the alert.

## Description

This query is used to identify the type of traffic that caused the spike. As noted in the README, this can often just be attributed to benign traffic over 443.

## Query

```kusto
let AlertTime = datetime(2099-01-01T22:42:53.8565818Z);

_Im_NetworkSession
| where TimeGenerated between (
    AlertTime - 60m .. AlertTime + 15m
)
| summarize Sessions=count()
    by
    NetworkProtocol,
    DstPortNumber,
    NetworkDirection,
    bin(TimeGenerated, 10m)
| order by TimeGenerated asc, Sessions desc
```

## Comments

Adjust the date time to match the time of the system alert
