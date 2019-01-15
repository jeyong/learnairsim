# 센서
 * 현재 지원하는 센서 : Camera, IMU, Magnetometer, GPS, Barometer, Lidar
 * 카메라 관련 내용은 별도로

## 기본 센서
 * settings.json 파일에 별도로 센서를 지정하지 않는 경우 활성화 되는 센서들
   * IMU, Magnetometer, GPS, Barometer

 * settings.json 파일에 기본 센서 목록 설정
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

 * vehicle에서 센서 목록을 지정하는 경우 반드시 해당 목록에 대한 설정을 해야함
 * 실행 중에 센서의 추가/삭제/업데이트 등은 지원하지 않음 
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
```

 * 