# Format IPs into KQL ready string

## Description

This can be used when looking to gather and format IP information from a default query into KQL ready output that can be used in dynamic arrays for investigation 

## Query

```kusto
| summarize IPs = strcat_array(make_set(strcat('"',IPAddress, '"')), ", ")
```

## Comments

