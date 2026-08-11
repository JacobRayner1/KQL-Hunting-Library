# Use to find the oldest/earliest event

## Description

This can be find the earliest event in query output. The below can be added to the end of a query to return the entire row associated with the earliest or oldest timestamp.

## Query

```kusto
summarize arg_min(Timestamp, *)
```

## Comments
This can be particularly useful when gathering information on brute force activity for example, to find the first attempted brute force attack.
