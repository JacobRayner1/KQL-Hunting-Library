# Find failed sign in attempts followed by a successful sign in

## Description

This script can be used when investigating brute force activity

Table: 
`SignInLogs`

## MITRE ATT&CK

T1110.001 - Password Guessing

## Query

```kusto
let Failed =
    SigninLogs
    | where TimeGenerated > ago(24h)
    | where ResultType != 0
    | summarize FailedAttempts = count() by UserPrincipalName, IPAddress;

SigninLogs
| where TimeGenerated > ago(24h)
| where ResultType == 0
| join kind=leftouter Failed on UserPrincipalName, IPAddress
| where FailedAttempts > 0
| project
    TimeGenerated,
    UserPrincipalName,
    IPAddress,
    AppDisplayName,
    FailedAttempts
| order by FailedAttempts desc
```

## Comments
