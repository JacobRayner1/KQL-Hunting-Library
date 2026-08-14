# Used to determine how wide-spread the traffic is

## Description

This is used to confirm whether the spike is a result of environment wide traffic increase, or just a couple devices with large spikes. Ultimately just trying to confirm if the spike is indicative of C2 activity or potentially benign updates with this one.

## Query for Source

```kusto
_Im_NetworkSession
| where TimeGenerated between (
    AlertTime - 15m .. AlertTime + 15m
)
| where SrcIpAddr != "127.0.0.1"
| where DstIpAddr != "127.0.0.1"
| summarize
    Sessions=count(),
    UniqueDestinations=dcount(DstIpAddr)
    by SrcIpAddr
| order by Sessions desc
| take 30
```

## ## Query for Destination

let AlertTime = datetime(2026-07-27T22:42:53.8565818Z);

```kusto
let AlertTime = datetime(2099-01-01T22:42:53.8565818Z);

_Im_NetworkSession
| where TimeGenerated between (
    AlertTime - 15m .. AlertTime + 15m
)
| where SrcIpAddr != "127.0.0.1"
| where DstIpAddr != "127.0.0.1"
| summarize
    Sessions=count(),
    UniqueSources=dcount(SrcIpAddr)
    by DstIpAddr
| order by Sessions desc
| take 20
```

## Comments

Adjust the date time to match the time of the system alert
