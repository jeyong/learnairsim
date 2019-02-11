# PX4 Setup
## 하드웨어
 * Pixhawk2.1

## PX4 HITL
 1. 준비
   * Pixhawk2.1, 조정기, 수신기
 2. QGC 실행하고 Pixhawk2.1과 USB 연결
 3. QGC로 PX4 최신 버전 업로드
 4. QGC에서 airframe 설정 : "HIL Quadrocopter X" airframe 선택
 5. QGC에서 Radio 탭으로 이동하여 calibration 수행
 6. Flight Mode 탭으로 이동하여 Stabilized와 Attitude flight mode 설정
 7. QGC의 Tuning 섹션으로 이동하여 적절한 값으로 설정(옵션)
 8. settings.json
 ```json
 {
  "SettingsVersion": 1.2,
  "SimMode": "Multirotor",
  "Vehicles": {
    "PX4": {
      "VehicleType": "PX4Multirotor"
    }
  }
}
 ```
 9. 