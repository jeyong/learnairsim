## AHUD
 * 상속
   * class AHUD : public AActor
 * 내용
   * 헤드업 디스플레이의 base class
   * canvas와 debugcanvas를 가짐
   * 클릭을 감지하는 hit box 리스트를 포함
   * debug text를 렌더링하는 method 포함
   * 블루프린트에서 접근이 가능한 method 제공

## ACameraActor
 * 상속
   * class ACameraActor : public AActor
 * 내용
   * level에 위치하는 camera viewpoint

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
     