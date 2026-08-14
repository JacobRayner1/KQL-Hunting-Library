# Correlate network session logs with DeviceNetwork telemetry to gather further info if available

## Description

Use if ASIM doesn't provide sufficient output in step 6

## Query

```kusto
let AlertTime = datetime(2099-01-01T22:42:53.8565818Z);
let TargetIP = "10.0.0.0";

DeviceNetworkEvents
| where Timestamp between (
    AlertTime - 15m .. AlertTime + 15m
)
| where LocalIP == TargetIP
| where RemotePort == 443
| project
    Timestamp,
    DeviceName,
    LocalIP,
    RemoteIP,
    RemotePort,
    Protocol,
    InitiatingProcessFileName,
    InitiatingProcessCommandLine,
    InitiatingProcessAccountName,
    InitiatingProcessParentFileName
| order by Timestamp asc

## Comments

Adjust the date time to match the time of the system alert
