# FleetDefinitionV2

This message is the first message sent by both actors at connection. 

|Sender| Triggered by | 
|---|---|
|`AHS` |  At Connection |
|`AHS` |  At Runtime change |
|`FMS` |  At Connection |
|`FMS` |  At Runtime change |



## Message attributes

| key             | Req. Level |  format            | Description                                                             
|-------------------|------------|----------------|
| `"AHSId"`         | shall | GUID           | Unique identifier for the AHS instance                                  |
| `"Equipment"`     | shall | Array of objects | List of equipments. Can be empty but not null        |
| `"EquipmentId"`     | shall | GUID           | Unique key for the specific equipment          | 
|`"HID"`            | shall | String         |  Human readable string (name) for the equipment                    | 
|`"StationId"`      | may | String         |  Unique V2X Station ID (if available)                   |
|`"Type"`           | shall | Enumeration    |  Category (see furhter down)                                                   | 
| `"OEM"`          | shall | String         | Original Equipment Manufacturer                                         | 
| `"Model"`       | shall | String         | OEM model name                                                   | 
| `"Autonomous"`    | shall | Boolean        | IAutonomoy or not?                                         | 
| `"Length"`        | shall | Decimal        | Distance from front to rear in meters                                   | 
| `"Width"`            | shall | Decimal        | Distance from left to right in meters                                   | 


## Fleet ID

- The **Fleet ID** shall be **unique** across all fleets connecting to an FMS instance.
- It **must be immutable** across connections and system reboots.
- Each **Fleet Definition** must have exactly **one Fleet ID**.

> **Use Cases for Fleet ID:**  
> - Multiple different AHS fleets connecting to a single FMS.  
> - A single AHS instance managing multiple fleets within one FMS.  
> - A single AHS establishing multiple concurrent sessions with an FMS.

---

### Type Enumerations

Only valid enumerations from the list below shall be used as **Type**:

```json
{
  "HaulTruck", "Shovel", "Excavator", "Loader", "LightVehicle", 
  "WaterCart", "Grader", "FuelTruck", "LubeTruck", "Dozer", 
  "RubberTireDozer", "Drill", "Crusher", "Scraper", "BellyDumper", 
  "EmergencyVehicle", "Ambulance", "Dragline", "SurfaceMiner", 
  "Bus", "Train", "Trailer"
}
```

### FleetDefinitionV2 Message Example
```json
{
  "Protocol": "Open-Autonomy",
  "Version": 1,
  "Timestamp": "2025-01-30T11:20:13.316Z",
  "FleetDefinitionV2": {
    "AHSId": "6c5e8648-7ea5-43bf-942b-2051b4b79d9b",
    "Equipment": [
      {
        "EquipmentId": "f4d95a41-831e-4a27-9353-32872b7d6103",
        "HID": "HT042",
        "Type": "HaulTruck",
        "OEM": "Scania",
        "Model": "ATS",
        "Autonomous": true,
        "Length": 9.51,
        "Width": 2.85
      },
      {
        "EquipmentId": "3f4964b3-66a2-41ef-89b1-83b5af0da44e",
        "HID": "LV033",
        "StationId": "V2X12345",
        "Type": "LightVehicle",
        "OEM": "Toyota",
        "Model": "Landcruiser",
        "Autonomous": false,
        "Length": 4.97,
        "Width": 2.44
      }
    ]
  }
}
```
