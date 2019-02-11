# 설정
 * Documents\AirSim 위치에 settings.json 파일
 * json 형태
 * ASCII 포맷 사용
```json
{
  "SettingsVersion": 1.2,
  "SimMode": "Multirotor"
}
```


## 기본 설정
 * ViewMode ("FlyWithMe")
   * "FlyWithMe"
   * "GroundObserver
   * "Fpv"
   * "Manual"
   * "SprintArmChase"
   * "NoDisplay"

 * TimeOfDay ("Enable=False")
   * 

 * OriginGeopoint
   * Unreal Engine에서 Player Start 컴포넌트의 위도, 경도, 고도를 지정
   * 비행체의 home point가 이 transformation을 이용해서 계산
   * NED 시스템(SI 단위)을 사용한 API를 통해 좌표계 제공
   * 각 비행체는 (0,0,0)의 NED 시스템에서 시작
   * Time of Day 설정은 OriginGeopoint에 지정한 좌표로 계산

 * SubWindows
   * 