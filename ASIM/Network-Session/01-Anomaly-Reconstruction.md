# Establish a general baseline to determine what network activity actually existed around the alert.

## Description

This query is using the same values as the original rule to determine anomalous traffic, namely:
- DvcAction
- NetworkDirection
- NetworkProtocol
- Overall network-session volume

## Query

```kusto
let AlertTime = datetime(2099-01-01T22:42:53.8565818Z);

let min_t = ago(14d);
let max_t = now();

_Im_NetworkSession
| where TimeGenerated between (AlertTime - 15m .. AlertTime + 15m)
| summarize
    Sessions=count()
    by
    NetworkProtocol,
    NetworkDirection,
    DvcAction,
    bin(TimeGenerated, 10m)
| order by TimeGenerated asc
```

## Comments

Adjust the date time to match the time of the system alert
