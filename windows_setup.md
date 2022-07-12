## Windows 환경
### Visual Studio 2017 Community 설치
 * 다운로드 : https://visualstudio.microsoft.com/downloads/ 
 * 다운받은 community.exe 파일 실행 
 * 설치 옵션에서 'Windows SDK version 8.1'을 반드시 선택!
   * 현재 Windows SDK version 10.x가 최신이라 8.1을 별도로 선택하지 않으면 설치가 되지 않아서 AirSim 빌드가 되지 않는다.

### Unreal Engine 설치
 * Epic Games Launcher 다운로드 받기 https://www.unrealengine.com/en-US/download
   * Unreal Engine 사이트에서 등록이 필요
 * Epic Games Launcher 실행
   * 왼쪽 패널에서 'Library' 클릭
   * 'Add Versions' 을 클릭해서 'Unreal 4.18.x'을 다운로드 받기
 * 영문 설정
   * 메뉴나 항목이 모두 영어로 되어 있는 경우가 많아서 현재 한글과 영어로 혼용된 설정을 영문으로 바꾸기
   * Epic Games -> Settings -> Language -> English
   * Engine Editor -> Edit -> Editor Preferences -> Region & Language -> Editor Language -> English

### Unreal Project 빌드
 * VS 2017용 x64 네이티브 도구 명령 프롬프트 실행
```bash
> git clone https://github.com/Microsoft/AirSim.git
> cd AirSim
> build.cmd
```
  * bulid 시 error 발생 원인 : 한글 windows 10 사용시 파일 인코딩 문제로 인한 컴파일 오류 발생
    * 해결방법 : 해당 파일을 메모장에서 열어서 'utf-8'로 다시저장

### 최신 코드로 유지하기
 * airsim 프로젝트가 자주 변경되기 때문에 업데이트된 소스를 받는 것이 중요
 * 최신 상태로 유지하는 방법 (AirSim Project)
   * clean.bat 파일 실행
     * 빌드하면서 생성된 파일들 제거
   * > git pull 
   * > build.cmd
   * AirSim/Unreal/Plugins 폴더를 기존에 사용하던 프로젝트에 덮어쓰기
   * 해당 프로젝트에서 .uproject에 대해서 "Generate Visual Studio project files" 실행하기
  
### 단순 환경
#### Block Environment
 * 저사양 환경하여 AirSim 맛보기 가능한 환경
 * 빌드 하기
   * 윈도우 탐색기로 git으로 다운받은 AirSim Project 폴더로 이동
     * AirSim\Unreal\Environments\Blocks 로 이동하여 update_from_git.bat 파일 더블 클릭하여 실행
     * AirSim\Unreal\Environments\Blocks 폴더에 xxxx.sln 파일이 생성된 것을 확인하고 이 xxxx.sln 파일 더블클릭하면 Visual Studio 2017이 실행됨
     * Visual Studio 2017의 Blocks 프로젝트가 나타나면 정상
     * 'DebugGame_Editor', 'Win64'로 설정한 후에 F5 키 누르면 디버깅 모드로 실행
     * Unreal Editor 화면이 나타나면 우측 상단에 'Play'아아콘을 클릭하면 실행됨

#### Landscape Environment
 * 

#### Neighborhood Environment
 * Editor -> New Project -> C++  -> Basic Code -> No Starter Content -> NHTest -> Create Project
 * Epic -> Library -> Modular Neighborhood Pack -> Add To Project -> NHTest -> Add to Project -> NHTest 실행
 * Edit -> Project Settings -> Maps & Modes -> Default Maps를 Demo_Map으로 변경
 * Content Browser -> ModularNeighborHoodPack -> Mpas -> Demo_Map  

 * 다른 화면이 실행되는 경우
   * MatineeActor로 환경이 실행되는 경우로 이것을 삭제
   * Blueprint에서 삭제 방법
     * Blueprint
     * Event graph에서 Begin Play event를 살펴보기
     * "matinee"를 구동시키는 연결을 끊어주기 
     * 'World Outliner'에서 삭제 or Blueprints -> Open Level Blueprint 에서 삭제(matinee와 actor 삭제)
 * Unreal Editor 설정
   * Edit -> Project Settings -> Maps & Modes 로 진입
   * Editor Starter Map와 Game Default Map을 모두 Demo_Map 으로 설정
 * NHTest
   * AirSim/unreal/Plugins 를 복사해서 NHTest 프로젝트에 복사
   * NHTest.uproject 파일 열기
```json
{
	"FileVersion": 3,
	"EngineAssociation": "4.18",
	"Category": "",
	"Description": "",
	"Modules": [
		{
			"Name": "NHTest",
			"Type": "Runtime",
			"LoadingPhase": "Default",
			"AdditionalDependencies": [
                "AirSim"
            ]
		}
	],
	"Plugins": [
        {
            "Name": "AirSim",
            "Enabled": true
        }
    ]
}
```
   * NHTest.uproject -> 오른쪽 클릭 -> Generate Visual Studio Project Files... 
   * NHTest.sln 파일 열기 (VS 2017 실행)
   * VS 2017 -> Debug GameEditor -> Win64 로 설정 후 -> F5로 실행
   * Editor -> World Settings -> Game Mode Override -> AirSimGameMode 
