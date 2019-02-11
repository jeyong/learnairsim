# Multiple Vehicles
 * AirSim 1.2 버전부터 지원
## 설정
 * settings.json 파일 수정
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
 * Vehicles 엘리먼트의 속성을 지원하는 방식
 * XYZ는 NED 좌표로 SI unit 사용하는 초기 위치
 * 방향은 Yaw, Pitch, Roll을 지정 가능
 * 각 vehicle을 조정하기 위해 API를 사용하는 경우 지정한 vehicle_name을 이용(Drone1, Drone2)

