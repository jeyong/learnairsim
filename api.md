# api 종류
## 좌표
 * AirSim API는 모두 NED 사용 (m 단위)
 * Unreal엔진은 NEU 사용 (cm 단위)
 * 변환
   * 시작지점 - 현재지점 -> 100으로 나누기 (cm -> m)
 * settings.json에서 OriginGeopoint에 위도, 경도, 고도 지정
## 비행체 상태 정보
 * 상태 정보 종류
   * collision
   * estimated kinematics
     * position
     * orientation
     * linear 및 angular velocity
     * linear 및 angular acceleration (PX4의 경우 angular acceleration 불가)
   * timestamp

## python
### 환경
 * reset
   * 초기 상태로 설정
 * confirmConnection
   * 1초마다 연결 상태 검사하고 console로 리포팅하여 사용자가 확인할 수 있게
 * enableApiControl
   * API를 통해 제어권을 요청
 * isApiControlEnabled
   * API 제어가 가능하게 되면 true를 반환
 * ping
   * 연결이 되면 true를 반환
 * simPrintLogMessage
   * 시뮬레이터 윈도우에 지정한 메시지를 출력
 * simGetObjectPose, simSetObjectPose
   * UE환경에서 지정한 객체의 pose를 get/set
   * 여기서 객체라 함은 'actor'을 뜻함
   * 객체를 찾을 때는 tag나 name으로 검색
   * 
### 연결
```python
import airsim 

client = airsim.MultirotorClient()
client.confirmConnection()
client.enableApiControl(True)
client.armDisarm(True)
```
### 비행
 * 비행체 제어 
   * angle
   * velocity vector
   * destination position
   * 위의 조합 
   * move* 형태의 API 제공
 * high-level 제어
   * carrot following 알고리즘으로 path following (high-level)
 * low-level 제어
   * moveByAngleThrottleAsync
```python
client.takeoffAsync().join()
client.moveToPositionAsync(-10, 10, -10, 5).join()
```
 * takeoffAsync
 * moveToPositionAsync
#### 사용법
 * API의 인자 중에 duration이나 max_wait_seconds의 경우 Async접두사를 갖고 있다.(takeoffAsync)
 * task를 시작하자마자 바로 return하므로 taks가 실행되는 동안 다른 일을 할 수 있다.
 * 만약 완료될때 까지 기다릴려면 waitOnLastTask를 호출한다.
```c++
//c++
client.takeoffAsync()->waitOnLastTask();
```

```python
#python
client.takeoffAsync().join()
```

##### 비행 방향 설정
 * drivetrain 파라미터
   * airsim.DrivetrainType.ForwardOnly
   * airsim.DrivetrainType.MaxDegreeOfFreedom

##### yaw 방향
 * yaw_mode는 구조체 YawMode
   * yaw_or_rate
   * is_rate
     * true : rate 모드
     * false : angle 모드
 * yaw_mode.is_rate == true
   * drivetrain


## Tips
 * 백그라운드로 계속 실행 시키기 
   * 'Edit->Editor Preferences' 이동 후 'Search'박스에서 'CPU'로 검색하면 'Use Less CPU when in Background'의 체크를 해제
