Building this out

let AlertTime = datetime(2026-08-18T00:05:31.7807194Z);
DeviceNetworkEvents
| where DeviceName =~ "DeviceName"
| where TimeGenerated between (AlertTime - 5m .. AlertTime + 1m)
| summarize
    FirstSeen=min(TimeGenerated),
    LastSeen=max(TimeGenerated),
    Connections=count()
    by RemoteUrl, RemoteIP
| order by FirstSeen asc


Ideally better to use referrer header to confirm website that is hosting ad, although this is not included in DeviceNetworkEvents schema, which focuses on transport and socket connections rather than full HTTP history. That said, the above can still be used to construct network traffic that occurred before an ad hosting IP or URL was seen. This can be used when investigating 'Connection to a custom network indicator' events in the SIEM.
