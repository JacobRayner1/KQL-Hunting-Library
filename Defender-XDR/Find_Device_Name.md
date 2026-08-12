# Find Devices based on the MDATP Device ID

## Description

This can be used when looking to match a device name to a device MDATP Device ID

## Query

```kusto
DeviceInfo
| where DeviceId == "MDATPDeviceID"
| project DeviceName
```

## Comments

 
