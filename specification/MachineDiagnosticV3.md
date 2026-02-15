# MachineDiagnosticV3

The `MachineDiagnosticV3` message is an extension of the [MachineDiagnosticV2](/specification/MachineDiagnosticV2.md) message and includes additional metadata for each diagnostic to enable sending information relevant to a controller for that diagnostic.

Each Fault Data `key:value` pair is specific to the `CID:FaultCode` from a particular OEM. The `key:value` pairs are pre-determined and documented by the OEM, just like the `CID:FaultCode` list is. The recipient should use these to add context to the fault string associated with the `CID:FaultCode`.

 Because the Fault Data is not translatable and is used as-is by the recipient, care should be taken by the OEM to avoid string values that represent a sentence or words that should ultimately be translated to the local language.

|Sender| Triggered by | 
|---|---|
|`AHS` |  At connection |
|`AHS` |  At Runtime change |

## Message attributes

### Array Of `[ ]`
| Key                      | Req. Level | Type                           | Unit | Description                                                      | Example |
|--------------------------|------------|--------------------------------|------|------------------------------------------------------------------|---------|
| `"ComponentId"`          | shall      | Integer                        | -    | A component code number, e.g. a sub system | `555`  |
| `"FaultCode"`            | shall      | Integer                        | -    | A number that explains the fault | `2110`  |
| `"FaultData"`            | shall      | Dictionary<`string`:`string`> | -    | An object/dictionary containing additional contextual data in key/value pairs of strings | `"Coolant Temp"`:`"186.2"`  |


# MachineDiagnosticV2 Message Example
### Two active faults
```json
{
  "Protocol":"Open-Autonomy",
  "Version": 1,
  "Timestamp": "2025-01-31T09:40:20.316Z",
  "EquipmentId": "1c558480-cb1c-4bae-bbc7-89b12516aca5",
  "MachineDiagnosticV2": [
    {
      "ComponentId": 555,
      "FaultCode": 2110,
      "FaultData":
      {
        {"Coolant Temp In": "130.5"},
        {"Coolant Temp Out": "186.2"}
      }
    },
    {
      "ComponentId": 14,
      "FaultCode": 9999,
      "FaultData": {}
    }
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
  "MachineDiagnosticV3": [
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
