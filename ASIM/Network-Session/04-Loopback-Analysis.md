# Determine whether the anomaly was caused by localhost or external network communication

## Description

Aims to narrow down the cause of the alert

## Query

```kusto
let AlertTime = datetime(2099-01-01T22:42:53.8565818Z);

_Im_NetworkSession
| where TimeGenerated between (
    AlertTime - 15m .. AlertTime + 15m
)
| summarize
    Sessions=count()
    by TrafficType=case(
        SrcIpAddr == "127.0.0.1" and DstIpAddr == "127.0.0.1",
            "Loopback",
        SrcIpAddr == "127.0.0.1",
            "SourceLoopback",
        DstIpAddr == "127.0.0.1",
            "DestinationLoopback",
        "NonLoopback"
    )
| order by Sessions desc
```

## Comments

Adjust the date time to match the time of the system alert
