Windows Updates - Find the exact KB needed to resolve a CVE

## Description

Used to find the KB that is required to patch Windows CVEs

## Data Source

Microsoft Defender XDR

Table:
`DeviceTvmSoftwareVulnerabilities`

## Query

```kusto
DeviceTvmSoftwareVulnerabilities
| where CveId == "CVE-2025-47981" //Change "CVE-2025-24076" to CVE you want to investigate
| join kind=inner (DeviceTvmInfoGathering | project LastSeenTime, DeviceName) on DeviceName
| project DeviceName, SoftwareName, LastSeenTime, SoftwareVersion, RecommendedSecurityUpdateId
| project-rename
    ["Device Name"] = DeviceName,
    ["Operating System"] = SoftwareName,
    ["Last Seen"] = LastSeenTime,
    ["Version"] = SoftwareVersion,
    ["KB Needed"] = RecommendedSecurityUpdateId
```

## Investigation Notes

Review:

- Command line arguments
- Parent process
- User account
- Device timeline

## Comments
