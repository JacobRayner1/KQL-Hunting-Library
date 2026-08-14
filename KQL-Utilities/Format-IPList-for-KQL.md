# Format IPs into KQL ready string without use of a table to pull IP data.

## Description

This can be used when looking to gather and format IP information from a default query into KQL ready output that can be used in dynamic arrays for investigation, much like [Convert IPs to KQL Ready String](https://github.com/JacobRayner1/KQL-Hunting-Library/blob/main/KQL-Utilities/Covert_IPs_to_query_ready_string.md?plain=1). 
However, this can be used when working with an existing IP list that needs to be formatted for KQL investigation use. Use cases include exporting IP lists to csvs for IOC investigation, app transaction history investigation etc.

## Query

```kusto
print IPList = 
"8.8.8.8, 4.4.4.4, 1.1.1.1, 8.8.4.4"
| extend IPList = split(IPList, ",")
| mv-expand IPList
| extend IPList = strcat('"', trim(" ", tostring(IPList)), '"')
| summarize IPList = strcat_array(make_list(IPList), ", ")
```

## Comments

This will output the IPs in your original query into a "IP1", "IP2" format.
