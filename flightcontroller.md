# Flight controller
## FC란?
 * desired state (input)
 * sensor 데이터를 이용한 실제 state를 estimation
 * actuator를 동작시켜 최대한 현재 상태를 desired 상태로 만드는 것이 목적
 * quadrotor 예제
   * desired state
     * roll, pitch, yaw
   * estimation
     * gyro, accel를 이용한 roll, pitch, yaw
   * motor 신호 생성

## Simulator가 FC를 사용하는 방법
 * simulator는 각 actuator가 생성한 force와 thrust를 얻기 위해서 FC가 생성한 생성한 motor 신호를 사용
 * 비행체의 kinetic 속성을 계산하여 물리 엔진이 사용
 * 결국 시물레이션된 센서 데이터를 생성하고 FC로 피드백 된다. 

## 지원하는 FC
 * simple_flight
   * built-in
 * PX4
 * 향후
   * ROSFlight
   * Hackflight
