# Check host traffic around time of alert using sources IPs found from query in step 5

## Description

Check the top source IPs in step 5 to work on determining whether the traffic looks legitimate

## Query

```kusto
let AlertTime = datetime(2099-01-01T22:42:53.8565818Z);
let TargetHost = "10.1.2.199";

_Im_NetworkSession
| where TimeGenerated between (
    AlertTime - 15m .. AlertTime + 15m
)
| where SrcIpAddr == TargetHostIP
| where DstIpAddr != "127.0.0.1"
| summarize
    Sessions=count()
    by
    DstIpAddr,
    DstHostname,
    DstAppName,
    DstPortNumber,
    NetworkProtocol
| order by Sessions desc
| take 50
```

## Comments

Adjust the date time to match the time of the system alert. If the traffic is distributed across multiple endpoints, use an array for TargetHost
