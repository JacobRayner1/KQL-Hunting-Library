# Summarise sign-in attempts

## Description

This script can be used when investigating brute force activity from known malicious IPs to confirm if any attempts have been successful. This can be combined with [Convert IPs to Query Ready String](https://github.com/JacobRayner1/KQL-Hunting-Library/blob/main/KQL-Utilities/Covert_IPs_to_query_ready_string.md) 

Table: 
`OfficeActivity, SignInLogs, AADNonInteractiveSigninLogs`

## MITRE ATT&CK

T1110.001 - Password Guessing

## Query

```kusto
let MaliciousIPs = dynamic([
"8.8.8.8", "4.4.4.4"
]);
union SigninLogs, AADNonInteractiveSigninLogs
| where IPAddress in (MaliciousIPs)
| where TimeGenerated > ago(30d)
| where ResultSignature == "SUCCESS" or ResultSignature == "FAILURE"
| summarize count() by ResultSignature, UserPrincipalName
| sort by count_ desc
```

## Comments

This script can also be used when gathering IP addresses from other tables, such as ClientIP from the OfficeActivity table.
