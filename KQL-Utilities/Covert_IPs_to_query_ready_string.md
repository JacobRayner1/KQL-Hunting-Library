# Format IPs into KQL ready string

## Description

This can be used when looking to gather and format IP information from a default query into KQL ready output that can be used in dynamic arrays for investigation 

## Query

```kusto
| summarize IPs = strcat_array(make_set(strcat('"',IPAddress, '"')), ", ")
```

## Comments

This will output the IPs in your original query into a "IP1", "IP2" format. If this query if being built without use of a table, the below can be ran using a ready IP list instead:

```kusto
print IPList = 
"8.8.8.8, 4.4.4.4, 1.1.1.1, 8.8.4.4"
| extend IPList = split(IPList, ",")
| mv-expand IPList
| extend IPList = strcat('"', trim(" ", tostring(IPList)), '"')
| summarize IPList = strcat_array(make_list(IPList), ", ")
```
