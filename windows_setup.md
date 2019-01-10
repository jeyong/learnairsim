Windows 환경
=== Visual Studio 2017 Community 설치 ===
 * 다운로드 : https://visualstudio.microsoft.com/downloads/ 
 * 다운받은 community.exe 파일 실행 
 * 설치 옵션에서 'Windows SDK version 8.1'을 반드시 선택!
   * 현재 Windows SDK version 10.x가 최신이라 8.1을 별도로 선택하지 않으면 설치가 되지 않아서 AirSim 빌드가 되지 않는다.

=== Unreal Engine 설치 ===
 * Epic Games Launcher 다운로드 받기 https://www.unrealengine.com/en-US/download
   * Unreal Engine 사이트에서 등록이 필요
 * Epic Games Launcher 실행
   * 왼쪽 패널에서 'Library' 클릭
   * 'Add Versions' 을 클릭해서 'Unreal 4.18.x'을 다운로드 받기

=== Unreal Project 빌드 ===
 * VS 2017용 x64 네이티브 도구 명령 프롬프트 실행
```bash
> git clone https://github.com/Microsoft/AirSim.git
> cd AirSim
> build.cmd
```
  * bulid 시 error 발생 원인 : 한글 windows 10 사용시 파일 인코딩 문제로 인한 컴파일 오류 발생
    * 해결방법 : 해당 파일을 메모장에서 열어서 'utf-8'로 다시저장

=== 단순 환경 ===
==== Block Environment ====
 * 저사양 환경하여 AirSim 맛보기 가능한 환경
 * 빌드 하기
   * 윈도우 탐색기로 git으로 다운받은 AirSim Project 폴더로 이동
     * AirSim\Unreal\Environments\Blocks 로 이동하여 update_from_git.bat 파일 더블 클릭하여 실행
     * AirSim\Unreal\Environments\Blocks 폴더에 xxxx.sln 파일이 생성된 것을 확인하고 이 xxxx.sln 파일 더블클릭하면 Visual Studio 2017이 실행됨
     * Visual Studio 2017의 Blocks 프로젝트가 나타나면 정상
     * 'DebugGame_Editor', 'Win64'로 설정한 후에 F5 키 누르면 디버깅 모드로 실행
     * Unreal Editor 화면이 나타나면 우측 상단에 'Play'아아콘을 클릭하면 실행됨

==== Landscape Environment ====
 * 

==== Neighborhood Environment ====
 * 
