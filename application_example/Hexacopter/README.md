# [Hexacopter 만들기](https://github.com/Microsoft/AirSim/wiki/hexacopter)

* 수정할 부분
  * PX4 Firmware
  * AirSim Physics
  * rendering model

## PX4 수정

* 6개 motor 출력을 생성하는 hexacopter mode가 필요
* QGC "HIL Quadrocopter" Airframe이 있지만 HIL Hexacopter는 없다.
* PX4를 HIL mode에서 제대로 동작시키기 위해서 특별한 Airframe을 만들 필요는 없다.
* HIL Hexacopter airframe 옵션을 만드는 방법
  * px4 git repo 받기
  * cd ROMFS/px4fmu_common/init.d
  * 1001_rc_quad_x.hil을 104_rc_hex_x.hil 이름으로 복사
  * 1004_rc_hex_x.hil 수정

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


## Physics

* 이 model에 대해서 setting json 파일에 추가

```json
"Model": "Hexacopter",
```


* 이 선언이 하는 일은 내부적으로 Px4MultiRotoer.hpp가 setupFrameGenericHex()를 호출하도록 한다. 이 함수는 initializeRotorHexX를 호출한다.

```c++
static void initializeRotorHexX(vector<RotorPose>& rotor_poses /* the result we are building */,
    uint rotor_count /* must be 6 */,
    real_T arm_lengths[],
    real_T rotor_z /* z relative to center of gravity */)
{
    Vector3r unit_z(0, 0, -1);  //NED frame
    if (rotor_count == 6) {
        rotor_poses.clear();
        /* Note: rotor_poses are built in this order: rotor 0 is CW

            x-axis
          (2)    (4)
            \  /
             \/
        (1)-------(0) y-axis
             /\
            /  \
          (5)  (3)

        */

        // vectors below are rotated according to NED left hand rule (so the vectors are rotated counter clockwise).
        Quaternionr quadx_rot(AngleAxisr(M_PIf / 6, unit_z));
        Quaternionr no_rot(AngleAxisr(0, unit_z));
        rotor_poses.emplace_back(Vector3r(0, arm_lengths[0], rotor_z),
            unit_z, RotorTurningDirection::RotorTurningDirectionCW);
        rotor_poses.emplace_back(Vector3r(0, -arm_lengths[1], rotor_z),
            unit_z, RotorTurningDirection::RotorTurningDirectionCCW);
        rotor_poses.emplace_back(VectorMath::rotateVector(Vector3r(arm_lengths[2], 0, rotor_z), quadx_rot, true),
            unit_z, RotorTurningDirection::RotorTurningDirectionCW);
        rotor_poses.emplace_back(VectorMath::rotateVector(Vector3r(-arm_lengths[3], 0, rotor_z), quadx_rot, true),
            unit_z, RotorTurningDirection::RotorTurningDirectionCCW);
        rotor_poses.emplace_back(VectorMath::rotateVector(Vector3r(0, arm_lengths[4], rotor_z), quadx_rot, true),
            unit_z, RotorTurningDirection::RotorTurningDirectionCCW);
        rotor_poses.emplace_back(VectorMath::rotateVector(Vector3r(0, -arm_lengths[5], rotor_z), quadx_rot, true),
            unit_z, RotorTurningDirection::RotorTurningDirectionCW);
    }
    else
        throw std::invalid_argument("Rotor count other than 6 is not supported by this method!");
}
```

* 이제 위에 Vector3r parameters에 대한 설명이 필요하다. 첫번째 motor (0)은 y-axis에 있어서 vector는 Vector3r(0, arm_lengths[0], rotor_z)...

## Rendering

* DJI S900 모델
