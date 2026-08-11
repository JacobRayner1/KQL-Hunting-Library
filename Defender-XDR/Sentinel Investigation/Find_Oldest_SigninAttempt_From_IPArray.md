# Find the oldest sign in attempt from dynamic array of IPs

## Description

This script can be used when investigating activity from known malicious IPs to confirm the first instance of malicious activity. 

## Data Source

Microsoft Defender XDR

Table: 
`SecurityEvent`

## MITRE ATT&CK

T1110.001 - Password Guessing

## Query

```kusto
let MaliciousIPs = dynamic([
"8.8.8.8", "4.4.4.4"
]);
SecurityEvent
| where EventID == "4625"
| where IPAddress in (MaliciousIPs)
| where TimeGenerated > ago(30d)
| summarize arg_min(TimeGenerated, *) by IpAddress, Account
```

## Comments

This script can also be used when gathering IP addresses from other tables, such as ClientIP from the OfficeActivity table.
