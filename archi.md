# Architecture
![구조](https://microsoft.github.io/AirSim/docs/paper/overview.png)

## 코드 구조
### AirLib
 * 대부분 코드는 AirLib
 * C++11 컴파일러 사용
 * AirLib 구성
   * Physics engine
   * Sensor Model
   * Vehicle Model
   * Control library
 
 ### Unreal/Plugins/AirSim
  * Unreal engine에 의존하는 유일한 부분
  * 다른 플랫폼(unity)에서도 돌아가게 하기 위해서 독립적으로 유지
  * Blueprints를 포함한 UObject based class의 장점을 이용
    * SimMode_ 클래스
    * VehiclePawnBase
    * VehicleBase

### MavLinkCom
 * Mavlink 장치와 통신하는 C++ class
 * 이 library는 독립적으로 존재하므로 다른 프로젝트에서 사용 가능

### Sample Programs
 * API를 사용하는 방법을 보여주는 프로그램
 * HelloDrone, DroneShell(UDP로 시뮬레이터에 연결하는 방법을 보여줌)
 * 시뮬레이터가 server를 실행

## Unreal 프레임워크
 ![Framework](https://microsoft.github.io/AirSim/docs/images/airsim_startup.png)
 ![Game Flow](https://docs.unrealengine.com/portals/0/images/Gameplay/Framework/GameFlow/GameFlowChart.png)
