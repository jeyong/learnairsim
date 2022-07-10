# [Actor Communication](https://docs.unrealengine.com/4.27/en-US/ProgrammingAndScripting/ActorCommunication/)
* 구현 방법 선택
  * Blueprint script과 C++
    * Actors 사이 정보 공유 및 통신하는 다양한 방법 제공
  * 어떤 경우에 해당 방법을 사용하는지 소개
* 종류
  * 직접 통신
  * Casting
  * Interfaces
  * Event Dispatchers

## 직접 통신(Direct Communication)
  * 같은 level에서 Actors 사이에 가장 일반적인 통신 방법
  * working Actor -> target Actor에 대한 refrence를 이용
  * Actors간에 1:1 관계 
  * 언제 사용해야할까?
    * 같은 level에서 특정 Actor에 대한 reference를 갖고 있으면서 해당 정보가 필요한 경우
  * 예제
    * Actor의 event가 발생
    * Level에 있는 Actor로부터 정보 얻기

## Casting
* Actor에 대한 reference를 가지고 이를 다른 class로 변환하고자 할때
* 만약 변환이 성공적이면 해당 Actor에 대한 정보와 기능에 직접 통신을 사용할 수 있다.
* 언제 사용할까?
  * Actor에 대한 reference를 가지고 있고 해당 Actor가 어떤 class의 정보에 접근가능한지를 검사하고자 할때
* 예제
  * 모든 Pawn을 포함하는 volume을 사용하고 해당 Pawn reference를 특정 subclass(Chracter처럼)로 cast하여 정보에 접근
  * Actor의 reference를 사용하여 parent class로 cast하고 정보를 접근 
## Interfaces
* 공통 behaviors 정의
* 동일한 behaviors를 가지는 Actor class 정의
* 각 Actor에 대한 behaviors 접근
* 언제 사용할까?
  * 다양한 타입의 Actors에 공통 기능을 생성하는 경우 이 method 사용
* 예제
  * 각 Actor
  * damage를 다른 Actor에 적용
  * 
## Event Dispatchers
* 어떤 Actor가 event를 발생시키고 다른 Actors들이 이 event 통지를 받는 통신 방법
* working Actor에 대한 Event Dispatchers를 생성하고 target Actors를 여기에 bind 시키는 방식
* 1:다 관계
* 언제 사용할까?
  * 하나의 event가 여러 Actors에 영향을 주고자 하는 경우
