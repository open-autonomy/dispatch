# BasicMachineHealthV2

|Sender| Triggered by | 
|---|---|
|`AHS` |  At Runtime change |

## Message attributes

| Key                  | Req. Level | Type          | Unit  | Description                                             |
|-------------------------|-----------|--------------|------|---------------------------------------------------------|
| `"FuelLevel"`           | shall     | integer      | %    | Current Fuel level                   |
| `"TotalMachineHour"`    | should    | decimal      | h    | Number of hours the Machine has been running       |
| `"TotalEngineHour"`     | shall     | decimal      | h    | Number of hours the Machine has been running        | 
| `"Tire"`               | should    | Array<TireStatus> | -    | A list of tire information       | 
| `"Additional"`         | may       | Array<SensorReading>      | -    | Additional sensor measurements |

### Tire Status Object

The Tire Status Object is used to represent the status of individual tires on the machine. Each tire status includes the position of the tire, its pressure, and its temperature.

| Key             | Req. Level | Type    | Unit  | Description                            | 
|-------------------|-----------|--------|------|--------------------------------|
| `"TirePosition"`  | shall     | string  | -    |           |       
| `"TirePressure"`  | shall     | integer | kPa  | Pressure for the actual tire      |
| `"TireTemperature"` | shall     | integer | °C   | Temperature for the actual tire       |

### Sensor Reading Object

The Sensor Reading Object is used to represent additional sensor measurements that are not covered by the standard fields in the BasicMachineHealthV2 message. Each sensor reading includes a unique identifier, the measured value, and the unit of measurement.

| Key             | Req. Level | Type    | Unit  | Description                            | 
|-------------------|-----------|--------|------|--------------------------------|
| `"SensorId"`      | shall     | string  | -    | Unique identifier for the sensor      |       
| `"Value"`        | shall     | decimal | -    | Measured value from the sensor       |
| `"Unit"`         | shall      | string  | -    | Unit of the measured value       |

> [!NOTE]
> The "Additional" field allows for flexibility in reporting various sensor data that may be specific to different machine types or configurations.


# BasicMachineHealthV2 Message Example
```json
{
  "Protocol":"Open-Autonomy",
  "Version": 1,
  "Timestamp": "2024-10-31T09:30:10.316Z",
  "EquipmentId": "f4d95a41-831e-4a27-9353-32872b7d6103",
  "BasicMachineHealthV2": {
    "FuelLevel": 74,
    "TotalMachineHour": 4511.4,
    "TotalEngineHour": 93.1,
    "Tire": [
      {"TirePosition":"1.7", "TirePressure": 123, "TireTemperature": 42},
      {"TirePosition":"1.9", "TirePressure": 124, "TireTemperature": 42},
      {"TirePosition":"2.7", "TirePressure": 111, "TireTemperature": 43},
      {"TirePosition":"2.9", "TirePressure": 125, "TireTemperature": 43},
      {"TirePosition":"3.7", "TirePressure": 131, "TireTemperature": 41},
      {"TirePosition":"3.9", "TirePressure": 132, "TireTemperature": 41}
    ],
    "Additional": [
      {
        "SensorId": "EngineOilTemperatureSensor1",
        "Value": 85.5,
        "Unit": "°C"
      },
      {
        "SensorId": "HydraulicPressureSensor2",
        "Value": 2500,
        "Unit": "kPa"
      },
      {
        "SensorId": "AdBlue",
        "Value": 45,
        "Unit": "%"
      }
    ]
  }
}
```
