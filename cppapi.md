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
   * 

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

