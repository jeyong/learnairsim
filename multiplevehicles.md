# 다중 비행체
## 다중 비행체 생성
 * settings.json 에서 지정
```json
{
    "SettingsVersion": 1.2,
    "SimMode": "Multirotor",

    "Vehicles": {
        "Drone1": {
          "VehicleType": "SimpleFlight",
          "X": 4, "Y": 0, "Z": -2,
      "Yaw": -180
        },
        "Drone2": {
          "VehicleType": "SimpleFlight",
          "X": 8, "Y": 0, "Z": -2
        }

    }
}
```
 * vehicle_name을 지정