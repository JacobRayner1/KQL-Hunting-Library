# Find events where powershell has been spawned by services.exe

## Description

This can be used when investigating suspicious process spawning

Table: 
`DeviceProcessEvents`

## Query

```kusto
DeviceProcessEvents
| where TimeGenerated > ago(7d)
| where FileName =~ "powershell.exe"
| where InitiatingProcessParentFileName =~ "services.exe"
| project
    Timestamp,
    DeviceName,
    AccountName,
    ProcessCommandLine,
    InitiatingProcessFileName,
    InitiatingProcessParentFileName
| order by Timestamp desc
```

## Comments
