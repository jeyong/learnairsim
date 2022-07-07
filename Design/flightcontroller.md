# Flight controller

## FC란?

* input -> desired state 를 얻기 위해서
* 원리
  * sensor 데이터를 이용한 현재 state를 추정
  * actuator를 동작시켜 현재 state에서 desired state로 만드는 것이 목적
* quadrotor 예제
  * desired state
    * roll, pitch, yaw
  * 현재 상태 추정
    * gyro, accel를 이용한 roll, pitch, yaw
  * motor 신호 생성
    * desired state로 전환

## Simulator가 FC를 사용하는 방법

* simulator는 각 actuator가 생성한 force와 thrust를 얻기 위해서 FC가 생성한 생성한 motor 신호를 사용
* 비행체의 kinetic 속성을 계산하여 물리 엔진이 사용
* 결국 시물레이션된 센서 데이터를 생성하고 FC로 피드백 된다.

## 지원하는 FC

* AirSim 내부 제어기
  * simple_flight
* AirSim 외부 제어기
  * PX4
  * ArduPilot

## HITL vs. SITL

* 실제 HW에서 동작하는가? 아니면 simulation에서 동작하는가?

## FC 없이 AirSim 이용하기

* flight controller 없이 AirSim 이용 가능
* 소위 "Computer Vision" 모드를 사용
* vehicle dynamic이 필요 없는 경우 이 mode를 사용
