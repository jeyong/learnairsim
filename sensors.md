<<<<<<< HEAD
﻿# Sensors
## 현재 지원 Sensor
 * Camera
   * 다른 센서와 설정이 좀 다르다. 
 * IMU
 * Magnetometer
 * GPS
 * Barometer
 * Lidar (Distance)

## 기본 Sensor
 * settings.json에서 센서를 지정하지 않으면 simmode 기반으로 다음 센서들이 활성화
 * simmode가 multirotor인 경우
   * IMU
   * Magnetometer
   * GPS
   * Barometer

## default sensor 목록
```json
    "DefaultSensors": {
        "Barometer": {
             "SensorType": 1,
             "Enabled" : true
        },
        "Gps": {
             "SensorType": 1,
             "Enabled" : true
        },
        "Lidar1": { 
             "SensorType": 6,
             "Enabled" : true,
             "NumberOfChannels": 16,
             "PointsPerSecond": 10000
        },
        "Lidar2": { 
             "SensorType": 6,
             "Enabled" : false,
             "NumberOfChannels": 4,
             "PointsPerSecond": 10000
        }
    },
```

### vehilce에 따른 sensor settings 지정
```json
    "Vehicles": {

        "Drone1": {
            "VehicleType": "simpleflight",
            "AutoCreate": true,
            ...
            "Sensors": {
                "MyLidar1": { 
                    "SensorType": 6,
                    "Enabled" : true,
                    "NumberOfChannels": 16,
                    "PointsPerSecond": 10000,
                    "X": 0, "Y": 0, "Z": -1,
                    "DrawDebugPoints": true
                },
                "MyLidar2": { 
                    "SensorType": 6,
                    "Enabled" : true,
                    "NumberOfChannels": 4,
                    "PointsPerSecond": 10000,
                    "X": 0, "Y": 0, "Z": -1,
                    "DrawDebugPoints": true
                }
            }
        }
   }

