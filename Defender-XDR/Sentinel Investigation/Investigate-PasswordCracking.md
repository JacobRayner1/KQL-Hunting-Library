The below KQL can be used to check sign in logs for any successful attempts when investigating Distributed Password cracking attempts in Microsoft Entra ID rule

union SigninLogs, AADNonInteractiveUserSignInLogs
| where TimeGenerated > ago(50d)
| where ResultType in ("50126", "50053" , "50055", "50056")
| where UserPrincipalName contains "wes.trotter"
| where Location !contains "AU"
| summarize count() by ResultSignature
