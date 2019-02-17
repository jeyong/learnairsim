AirSim
 * 기본 틀은 AirSimGameMode
   * AirSim의 큰 규칙을 설정(충돌하면 종료된다던가..)
 * Player 설정
   * Pawn을 빙의(Possess)하는 PlayerController
     * Pawn은 player의 물리적인 측면
     * Controller은 동작의 규칙에 대한 설정
     * 달리기나 점프 같은 특성이 필요한 경우는 Pawn 대신 Character를 사용
     * Pawn 자체에 이동이나 로직 규칙을 포함 가능하고 Controller에도 포함 가능
     * AirSim의 경우 Joystic이나 키보드, 외부 API로 제어하기 때문에 Pawn을 사용
   * Controller
     * Player의 입력을 받는 PlayerController
     * AI의 제어를 받는 AIController
 * Camera
   * 사용자가 조정하는 Pawn을 대상으로 하므로 Vehicle Pawn에 있는 CameraComponent 하나만 PlayerCamera로 사용.

 * Input
   * 시뮬레이션 도중에 받은 Input으로 Vehicle을 움직임
 * HUD
   * Camera로부터의 View 위에 비행과 관련된 정보들을 보여주는 HUD

---------------
Unreal Engine 구동
 * http://api.unrealengine.com/images/Gameplay/Framework/GameFlow/GameFlowChart.png
 * Editor로 실행하는 경우와 exe 파일로 생성하여 구동하는 경우에 대한 설명


