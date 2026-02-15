# MachineDiagnosticV2

|Sender| Triggered by | 
|---|---|
|`AHS` |  At connection |
|`AHS` |  At Runtime change |

## Message attributes

### Array Of `[ ]`
| Key                      | Req. Level | Type          | Unit | Description                                                      | Example |
|--------------------------|-----------|--------------|------|------------------------------------------------------------------|---------|
| `"ComponentId"`          | shall     | Integer      | -    | A component code number, e.g. a sub system | `555`  |
| `"FaultCode"`            | shall     | Integer      | -    | A number that explains the fault | `2110`  |


# MachineDiagnosticV2 Message Example
### Two active faults
```json
{
  "Protocol":"Open-Autonomy",
  "Version": 1,
  "Timestamp": "2025-01-31T09:40:20.316Z",
  "EquipmentId": "1c558480-cb1c-4bae-bbc7-89b12516aca5",
  "MachineDiagnosticV2": [
    {"ComponentId": 555, "FaultCode": 2110 },
    {"ComponentId": 14, "FaultCode": 9999 }
  ],
  "MachinePositionV1": {
    "Timestamp": "2025-01-31T09:40:20.316Z",
    "Heading":"222",
    "Latitude":"65.176854",
    "Longitude":"-23.071800",
    "Elevation":"2.23",
    "LatitudeAccuracy":"0.31",
    "LongitudeAccuracy":"0.27",
    "HeightAccuracy":"0.58",
    "HeadingAccuracy":"2.1",
    "Speed":"43.1"
  }
}
```

### Clearing the faults
```json
{
  "Protocol":"Open-Autonomy",
  "Version": 1,
  "Timestamp": "2025-01-31T09:40:20.316Z",
  "EquipmentId": "1c558480-cb1c-4bae-bbc7-89b12516aca5",
  "MachineDiagnosticV2": [
  ],
  "MachinePositionV1": {
    "Timestamp": "2025-01-31T09:40:20.316Z",
    "Heading":"222",
    "Latitude":"65.176854",
    "Longitude":"-23.071800",
    "Elevation":"2.23",
    "LatitudeAccuracy":"0.31",
    "LongitudeAccuracy":"0.27",
    "HeightAccuracy":"0.58",
    "HeadingAccuracy":"2.1",
    "Speed":"43.1"
  }
}
```
