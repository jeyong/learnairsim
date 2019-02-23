## AHUD
 * 상속
   * class AHUD : public AActor
 * 내용
   * 헤드업 디스플레이의 base class
   * canvas와 debugcanvas를 가짐
   * 클릭을 감지하는 hit box 리스트를 포함
   * debug text를 렌더링하는 method 포함
   * 블루프린트에서 접근이 가능한 method 제공

## AActor
 * 상속
   * class AActor : public UObject
 * 내용
   * level에서 생성되고 위치시킬 수 있는 객체의 base class
   * Actor는 ActorComponents의 집합을 포함할 수 있는데, actor가 움직이는 방식, 렌더링하는 방식 등을 제어하는데 사용할 수 있다.

## APAWN
 * 상속
   * class APawn :
      public AActor ,
      public INavAgentInterface
 * 내용
   * player나 AI로 빙의(posses)될 수 있는 모든 actor의 base class
   * level 상에서 player나 물체의 물리적 특성을 대표한다. 

## ACameraActor
 * 상속
   * class ACameraActor : public AActor
 * 내용
   * level에 위치하는 camera viewpoint
 * 상세
   * 모든 프로젝트에서 들여다보는 방법이 필요하다.
   * 가장 일반적인 방법이 Camera Actor를 이용하는 것이다.
   * 주로 Matinee와 결합하여 사용
   * Camera Actor를 선택하면, 메인 3D viewport는 PIP view를 가짐
   * Camera Actor 위치시키기
     * 'All Classes' 카테고리 -> Modes 패턴에 있음
     * 'Modes' 패널에서 하나를 끌어서 game world에 두기
   * Camera Actor 사용법
     * Modes 패널에서 선택하는 것만큼 사용하기 쉽다.
     * world에 Camera Actor가 생성되면 Blueprints나 Matinee를 결합하여 view point로 사용이 가능하다. 
## FRenderCommand
 * 상속
   * 독립
 * 렌더링 명령 큐에 저장된 명령의 parent class

## AGameModeBase
 * 상속
   * class AGameModeBase : public AInfo
 * 내용
   * GameModeBase는 플레이하는 game을 정의
   * game 룰, 점수, actor 존재 여부, game에 들어올 수 있는 사람
   * 서버쪽에서만 instance가 존재
   * level이 초기화되는 UGameEngine::LoadMap() 시점에 instance로 생성
   * GameMode Override 값은 World Settings에, DefaultGameMode entry는 게임의 Project Settings에 설정

## ACharacter
 * 상속
   * class ACharacter : public APawn
 * 내용
   * Pawn에서 메쉬, 충돌, built-in 움직임 로직을 가짐
   * player와 world 사이에 물리적인 상호작용에 대한 책임
   * 기본 네트워킹과 입력 모델이 구현되어 있음
   * CharacterMovementComponent 를 이용하여 world 상에서 걷기, 점프, 날기, 수영하기 등의 직립보행 player를 위한 설계

## IModuleInterface
 * 상속
   * x
 * 내용
   * 모든 module implementation이 이 interface에 상속 받아야 함
   * 모듈이 로딩된 후에 모듈을 초기화하고 모듈이 unload되기 전에 clean up을 수행

## AGameMode
 * 상속
   * class AGameMode : public AGameModeBase
 * 내용
   * 멀티 플레이어 매핑 기반 게임과 같이 동작하는 GameModeBase의 subclass
   * spawn point와 상태 매칭을 고르는 기본 동작을 가짐
   * 더 단순한 base를 원하다면 GameModeBase를 상속받아라

## Blueprint Function Librarion
 * 개발에 도움이 되는 function의 집합
 * Blueprint로 개발하는 겨웅에도 동일한 요구가 있음
 * Blueprint에 object의 함수와 properties를 expose하는 방법에 대해서 알고 있음
   * 특정 gameplay object type에 이런 함수들을 묶어서 expose하지 않아도 되는 경우에 Blueprint Function Libraries라고 한다.
 * 특정 gameplay object에 묶이지 않는 utility function의 집합
 * 논리 함수 집합 예제
   * AI Blueprint Library
   * System Blueprint Library
 * Blueprint Function Library 만들기
   * UFUNCTION() 매크로를 이용하여 Blueprint로 함수를 exposing하는 것과 비슷
   * Actor나 UObject로 상속받는 대신에 UBlueprintFunctionLibrary로부터 상속받는다.
   * static method만 포함
   * 간접적으로 UObject로부터 상속되므로
     * UCLASS()와 GENRATED_UCLASS_BODY() 매크로가 필요함

## Player Start
 * player를 world의 특정 위치에 spawn하기
 * Player Start라고 불리는 특별한 Actor를 제공
 * Player Start는 game world에서 player가 시작하는 위치를 지정
 * 위치 지정
   * 'Basic'카테고리 -> Modes 패널에서 Player Start 찾기
   * world에 위치시키기 위해서 Modes 패널에서 끌어서 game world로 두기
 * 사용법
   * world에서 원하는 위치에 player를 spawn 시키기 위해서 Blueprint와 함께 사용
 * Tip
   * No Player Start : Player Start를 추가하지 않고 game을 play하면 player는 0, 0, 0 위치에서 시작. 이런 이유로 Player Start를 world에 위치시켜야 함.
   * Play From Here : 가끔 Player Start가 아니라 특정 위치에서 play하길 원하는 경우. 오른쪽 클릭 -> Play From Here 옵션 사용
   * Bad Size : "BADsize"가 표시되는 경우. 다른 객체와 교차되지 않도록 위치를 이동시킨다. 

## PlayerController
 * Pawn <-> 사람 player 사이에 제어를 위한 interface
 * PlayerController는 사람 player의 의지를 대표!

## Camera 사용법
  * camera를 level에 위치시키면, PIP 윈도우가 Viewport에 추가되며 Camera의 보는 각도가 나타난다.
  * Camera의 이름이 윈도우의 상단 중간에 표시