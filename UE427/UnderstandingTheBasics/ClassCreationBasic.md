# [Class 생성 기초](https://docs.unrealengine.com/4.27/en-US/ProgrammingAndScripting/ClassCreation/)
* 생성 종류
  * Blueprint Only
  * C++ Only
  * Blueprint and C++ 

* Class 생성하는 3가지 방법을 소개
* 새로운 LightSwitch class를 생성하여 level에 추가
  * LightSiwtch는 Actor class를 상속
  * PointLightComponent를 포함, SphereComponent
  * 각 LightSwitch class는 
  * 기본 동작은 player가 SphereComponet에 들어오거나 나가면 PointLightComponent의 visibility가 토글
## Blueprint Only
* [Blueprint Only](https://docs.unrealengine.com/4.27/en-US/ProgrammingAndScripting/ClassCreation/BlueprintOnly/)
* Blueprint class는 Blueprint Visual Scripting 시스템을 사용하여 새로운 class를 생성가능.
* 새로운 Blueprint class를 생성한 후에 component를 추가하고 visual scripting으로 기능, gameplay, design behavior를 설정할 수 있다. 그리고 class 변수에 대한 default 값을 설정한다.
* LightSwitch class는 LightSwitch_BPOnly라는 Blueprints만 사용한다.

### Class 설정
* 