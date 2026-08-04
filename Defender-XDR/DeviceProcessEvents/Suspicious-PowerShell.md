# Suspicious PowerShell Execution

## Description

Detects potentially suspicious PowerShell execution patterns.

## Data Source

Microsoft Defender XDR

Table:
`DeviceProcessEvents`

## MITRE ATT&CK

T1059.001 - PowerShell

## Query

```kusto
DeviceProcessEvents
| where FileName =~ "powershell.exe"
| project Timestamp,
          DeviceName,
          AccountName,
          ProcessCommandLine
| order by Timestamp desc
```

## Investigation Notes

Review:

- Command line arguments
- Parent process
- User account
- Device timeline

## False Positives

Legitimate administration scripts and automation tools.
```
