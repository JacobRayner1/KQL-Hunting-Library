# Find rare user agents in sign in activity

## Description

This script can be used when investigating for rare user agent activity

Table: 
`SignInLogs`

## Query

```kusto
SigninLogs
| where TimeGenerated > ago(30d)
| where isnotempty(UserAgent)
| summarize
    SignInCount = count(),
    UniqueUsers = dcount(UserPrincipalName),
    Users = make_set(UserPrincipalName, 10),
    IPAddresses = make_set(IPAddress, 10),
    Applications = make_set(AppDisplayName, 10),
    Countries = make_set(tostring(LocationDetails.countryOrRegion), 10),
    FirstSeen = min(TimeGenerated),
    LastSeen = max(TimeGenerated)
    by UserAgent
| where SignInCount <= 10
| order by SignInCount asc
```

## Comments
