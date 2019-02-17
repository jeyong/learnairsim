(용어)[http://api.unrealengine.com/KOR/GettingStarted/Terminology/index.html]

GameMode
 * 게임의 규칙을 설정
 * 게임 참가 방식, 일시정지, 레벨 전환, 승리 조건
 * GameMode와 상관없이 level당 오직 하나의 게임 모드가 존재 
 * 멀티플레이어 게임에서는 gamemode는 서버에 존재하고 이를 각 client가 복사해서 가져간다

GameStates
 * 게임에 속한 모든 client가 복사해서 가져야하는 정보 (기본적으로 모두 가져야하는 GameState)
 * ex) 게임 점수, 경기 시작 여부, world에 있는 플레이어 수에 따른 생성(spawn)할 AI 수, 기타 게임 정보
 * 멀티플레이어 게임의 경우 각 플레이어의 PC마다 GameState instance가 하나 있고, 서버의 instance는 authority가 된다.

PlayerStates
 * 사람 플레이어 또는 플레이어를 흉내내는 봇과 같은 게임내 참여자의 상태
 * AI의 경우 PlayerState가 없음
 * ex) player의 이름, 점수, 생명력 등
 * 멀티플레이어 게임에서 모든 player의 PlayerState 정보는 모든 PC에 존재

AGameModeBase
 * 진행하는 game을 정의
 * game 룰, 스코어, 어떤 actor가 존재하는지, game에 들어오는 사람
 * server에만 존재하고 client는 존재하지 않음
 * UGameEngine::LoadMap()에서 level이 초기화할때 인스턴스가 생성된다
 * https://api.unrealengine.com/INT/API/Runtime/Engine/Engine/UEngine/Tick/index.html
 * UEngine::Tick()

Vehicle 만들기
 * https://docs.unrealengine.com/en-US/Engine/Physics/Vehicles/VehicleUserGuide


AActor
 * level에서 위치시키고 spawn이 가능한 object
 * 여러 ActorComponent를 가지며 Actor의 움직임이나 랜더링에 사용
 * 
Components
 * Actor에 기생
 * 일단 Actor에 추가되면 독립적인 기능 부분
 * ex) 스포트라이트 컴포넌트 : Actor가 빛을 내도록, rotating component : actor가 회전하도록

Pawns
 * Actor의 subclass
 * 게임에서 아바타나 페르소나 역할처럼 캐릭터가 예
 * AI 제어 받는 것이 가능

Character
 * Pawn Actor의 subclass 
 * Player의 캐릭터에 사용
 * subclass에는 충돌전 셋업, 이족 보행을 위한 키바인딩

PlayerController
 * player 입력을 받아 시뮬레이션 내에서 상호작용으로 변환하는데 사용하는 base class
 * 최소 1개의 playercontroller는 있어야 함
 * playercontroller는 player를 대표하여 pawn이나 character로 빙의


Levels
 * map이라고 부리는 play가 일어나는 영역
 * 레벨 안에 actor를 배치하고 트랜스폼을 적용한 뒤 프로퍼티를 편집

World
 * level의 목록을 갖고
 * 직접 world를 참조하여 사용하는 경우는 적다
