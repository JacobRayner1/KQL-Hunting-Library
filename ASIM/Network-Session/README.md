# ASIM Network Session Investigation

## Use Case

Investigation workflow for Sentinel's:

"Anomaly found in Network Session Traffic (ASIM Network Session schema)"

Use when the alert provides limited or no useful entity information.

## Investigation Flow

1. Establish network volume
2. Identify dominant protocol/port
3. Separate loopback traffic
4. Identify destination concentration
5. Identify source concentration
6. Identify application/service
7. Drill into high-volume hosts
8. Correlate with endpoint telemetry if required

## Primary Data Source

_Im_NetworkSession

## Related Sentinel Analytic

Anomaly found in Network Session Traffic (ASIM Network Session schema)
