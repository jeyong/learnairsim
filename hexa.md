# Hexa 적용

## PX4 수정
 * rotor : 6개
 * HIL Hexacopter를 현재 QGC에서 지원하지 않음
 * PX4 수정
   * > cd ROMFS/px4fmu_common/init.d
   * > cp 1001_rc_quad_x.hil 1004_rc_hex_x.hil
   * > gedit 1004_rc_hex_x.hil
```bash
#!nsh
#
# @name HIL Quadcopter +
#
# @type Simulation
#
# @maintainer Anton Babushkin <anton@px4.io>
#

sh /etc/init.d/rc.mc_defaults

set MIXER hexa_x

# Need to set all 8 channels
set PWM_OUT 12345678

set HIL yes
```
 * > make px4fmu-v3_default
 * QGC 설정 파일
   * %APPDATA%\QGroundControl.org\PX4AirframeFactMetaData.xml
   * 이 파일에서 airframe id="1001" 부분
```xml
 <airframe id="1004" maintainer="Anton Babushkin &lt;anton@px4.io&gt;" name="HIL Hexacopter X">
      <maintainer>Anton Babushkin &lt;anton@px4.io&gt;</maintainer>
      <type>Simulation</type>
    </airframe>
```
   * 위와 같이 수정하기
   * QGC의 "HIL" airframe 타입에 추가된 것 확인 
     * HIL Hexacopter X 
## AirSim
 * settings.json 파일 
   * "Model": "Hexacopter"
 * Px4MultiRotor.hpp 파일의 setupFrameGenericHex()
   * initializeRotorHexX 호출

## redering
 * 