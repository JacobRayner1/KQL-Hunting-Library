Password Cracking Attempts  

## Description

Used to investigate sign in logs when reviewing Distributed Password cracking attempts in Microsoft Entra ID

## Data Source

Microsoft Defender XDR

Table:
`SigninLogs`, `AADNonInteractiveUserSignInLogs`

## MITRE ATT&CK

T1059.001 - PowerShell

## Query

```kusto
union SigninLogs, AADNonInteractiveUserSignInLogs
| where TimeGenerated > ago(50d)
| where ResultType in ("50126", "50053" , "50055", "50056")
| where UserPrincipalName == "user@domain.com"
| where Location !contains "AU"
| summarize count() by ResultSignature
```

## Investigation Notes

Review:

- Command line arguments
- Parent process
- User account
- Device timeline

## False Positives

Legitimate administration scripts and automation tools.

## Comments
