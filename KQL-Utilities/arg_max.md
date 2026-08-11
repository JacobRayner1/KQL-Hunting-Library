# Use to find the latest event

## Description

This can be find the latest event in query output. The below can be added to the end of a query to return the entire row associated with the most recent timestamp.

## Query

```kusto
summarize arg_max(Timestamp, *)
```

## Comments

