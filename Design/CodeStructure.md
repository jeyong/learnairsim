# Code Structure
## AirLib
1. Physics Engine
   * header-only physics engine
2. Sensor models
   * header-only models for Barometer, IMU, GPS, ...
3. Vehicle models
   * header-only models for vehicle configurations and models
4. API-related files
   * MavLink, RPC client와 server

## Unreal/Plugins/AirSim
1. SimMode classes
2. PawnSimApi
   * 모든 vehicle pawn visualizations을 위한 base class
   * 각 vehicle는 자신의 child(Multirotor|Car|ComputerVision)Pawn class 가진다.
3. UnrealSensors
   * Distance와 Lidar sensors의 구현
4. WorldSimApi
   * environment와 vehicle-agnostsic API 관련 구현

* 이와는 별도로 PIPCamera는 camera 초기화와 UnrealImageCapture & RenderRequest를 포함. AirBlueprintLib는 UE4 engine와 인터페이스에 사용되는 utility와 wrapper methods를 가진다.


## MAVLinkCom
* MavLink 장치와 통신하는 C++ classes
* 독립적으로 다른 프로젝트에서도 사용 가능

## 