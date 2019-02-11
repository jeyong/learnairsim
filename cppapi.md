## AirSim APis
외부에서 비행체에 접근할 수 있는 인터페이스로 API를 제공.
프로그래밍으로 접근이 가능하며 비행제어, image, state 정보를 가져오기가 가능.

### API 종류
#### Common API
 * reset
   * 비행체를 원래 시작 상태로 reset
   * 초기 상태로 돌아왔으므로 다시 enableApiControl과 armDisarm을 다시 호출해야함
 * confirmConnection
   * 매 1초마다 연결 상태를 검사하고 Console에 연결 상태 리포팅 출력
 * enableApiControl
   * safety 목적으로 기본적으로 API를 통한 control이 disable되어 있으므로 api 제어를 위해서 enable 시켜야함.
 * isApiControlEnabled
   * API control이 설정 여부를 확인
 * ping
   * 연결된 경우 true를 반환
 * simPrintLogMessage
   * simulator 창에 특정 메시지를 출력
 * simGetObjectPose, simSetObjectPose
   * Unreal 환경에 있는 특정 객체의 pose를 set/get. Unreal에서 객체는 'actor'를 뜻하며 tag나 이름으로 검색이 가능.
#### Image / Computer Vision APIs
 * depth, disparity, surface 포함한 다양한 카메라로부터 동기화된 image를 추출 가능.
 * 설정 : resolution, FOV, motion, blur 등의 파라미터를 settings.json에서 설정
 * 충돌 상태에 대한 API도 제공
 * steremo image 수를 지정, depth, disparity 이미지 계산, pfm 포맷으로 저장.
#### 일시정지 / 재개 APIs
 * pause(is_paused) API로 일시정지 및 재개 가능
 * reinforcement learning에서 활용
    * 특정 시간 동안 시뮬레이션 수행 -> 자동 정지 (계산이 많은 동작 가능)
 * continueForTime(seconds) : 특정 시간 동안 수행하고 pause

#### Collision API
 * simGetCollisionInfo API : 충돌 정보 얻기
   * 구조체
   * collision 발생 여부
   * 충돌 position
   * penetration depth (관통 깊이)

#### Time Of Day API
 * 구형태의 하늘을 나타내는 class : EngineSky/BP_Sky_Sphere
 * 태양의 위치는 시간에 따라 변화지 않고 위도, 경도, 날짜 시간 설정에 따라서 태양의 위치를 계산한다. 

#### Weather APIs
 * 날씨 설정
   * simEnableWeather(True)
 * 날씨 효과
   * client.simSetWeatherParameter(airsim.WeatherParameter.Rain, 0.25);
   * Rain, Roadwetness, Snow, RoadSnow, MapleLeaf, RoadLeaf, Dust, Fog

#### Lidar APIs
 * Lidar 센서로부터 point cloud 데이터 추출
 * 설정 : 채널의 수, 초당 point, FOV 등을 settings.json

### Multirotor용 APIs
 * 각도, 속도 벡터, 목적지 위치 혹은 이들의 조합으로 제어
 * move* API 형태
 * position 제어하는 경우 path following 알고리즘이 필요한데 이 경우 carrot following 알고리즘을 사용. (상위 레벨 제어)
 * 최하위 레벨 제어 : moveByAngleThrottleAsync API
#### getMultirotorState
 * 한 번 호출로 비행체 상태 가져오기
 * collision, estimated kinematics, timestamp를 포함
 * 

### 좌표계 
 * 모든 AirSim API에서 NED 좌표계 사용
 * SI 단위 (미터 단위)
 * Unreal Engine 내부에서 사용하는 좌표시스템과 차이나는 점
   * +Z 가 Up
   * cm 단위 
  * AirSim API에서 변환
    * 비행체의 시작 지점은 항상 (0, 0, 0) NED 시스템
    * Unreal 좌표계 -> NED 변환
      * 먼저 시작 offset을 빼주기
      * cm -> m로 변환하기 위해서 100으로 나누기
    
### C++ APIs
 * 학습 방법
   * AirSim/HelloDrone 살펴보기
     * 개발설정
       * include path
       * lib path
     * 소스코드 사용법
```c++
MultirotorRpcLibClient client;
client.enableApiControl(true);
client.armDisarm(true);
client.takeoffAsync(5)->waitOnLastTask();
```

### Python
 * Python AirSim API 사용하기
 * 환경 설정
   * > pip install msgpack-rpc-python
   * > pip install airsim
```python
import airsim

client = airsim.MultirotorClient()
client.confirmConnection()
client.enableApiControl(True)
client.armDisarm(True)

client.takeoffAsync().join()
client.moveToPositionAsync(-10, 10, -10, 5).join()

for response in responses:
    if response.pixels_as_float:
        
```

