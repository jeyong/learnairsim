* Visual Model
  * Content Browser -> View Options -> Show Plugin Contents 
  * BluePrints/BP_FlyingPawn
* BP_FlyingPawn 
  * BodyMesh 살펴보기
  * Event Graph 살펴보기 
    * AFlyingPawn 소스코드와 매핑
  * SetupPropRatationMovement
    * Prop 속도 조절
  * 핵심 : FlyingPawn 상속 받은 BluePrints 생성
* 참고 강의 : https://cafe.naver.com/unrealenginekr/735
----
* 비행체 선택
  * ASimHUD::createSimMode()
    * ASimModeWorldMultiRotor (멤버)
      * ASimModeWorldBase
        * ASimModeBase
  * 
* Parameter
  * MultiRotorParamsFactory::createConfig 호출
    * Px4MultiRotorParams로 MultirotorParams을 설정
    * 
* 새로운 모델 추가
  * Px4MultiRotorParams::setupParams()
    * else if (connection_info_.model == "HDcopter") {
        setupFrameHDcopter(params);
    }
   * setupFrameHDcopter(params) 정의
    * setupFrameGenericQuad 참고
      * rotor 수
      * arm 길이 (450/2로 설정)
      * mass : 1 kg (1.0f) 전체 질량
      * 모터 무게 : 55g (0.055f)
      * box_mass : mass - (모터 총 무게)
      * calculateMaxThrust() : 최대 thrust 계산 (thrust 계수, max_rpm, prop 직경에 따라 계산)
      * body_box.x(), y(), z() : arm을 제외한 중앙 몸체 길이
      * rotor pose 계산
      * inertiamatrix 계산
----
* Sensor 추가
  * AirLib/include/sensors 에 원하는 센서명으로 디렉토리 생성
  * Subak Sensor인 경우
  * AirLib/include/sensors/subak 디렉토리 생성
  * AirLib/include/sensors/subak에 subakBase.hpp, subakSimple.hpp, subakSimpleParams.hpp 생성
  * subakSimple.hpp에 reset(), update() 추가
    * update()에 실제 실행시 마다 측정하는 내용을 구현
  * 외부에서 getOutput()으로 정보를 얻어감

