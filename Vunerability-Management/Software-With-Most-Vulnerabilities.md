# Find software with the highest amount of critical and high vulnerabilities

Table: 
`DeviceTvmSoftwareVulnerabilities`

## Query

```kusto
DeviceTvmSoftwareVulnerabilities
| where VulnerabilitySeverityLevel has_any ('Critical', 'High')
| summarize count(), VulnerableCVE = make_set(CveId) by SoftwareName
```

## Comments

This should be used to prioritise software patching against applications that are most vulnerable to attacl=k
