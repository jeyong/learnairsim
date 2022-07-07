# Vehicles

* Code 구조
* 하는 일
* 사용방법

## Code 구조

* car
  * api
    * CarApiBase.hpp
    * CarRpcLibAdaptors.hpp
    * CarRpcLibClient.hpp
    * CarRpcLibServer.hpp
  * firmware
    * ardurover
      * ArduRoverApi.hpp
    * physxcar
      * PhysXCarApi.hpp
  * CarApiFactory.hpp
* multirotor
  * api
    * MultirotorApiBase.hpp
    * MultirotorCommon.hpp
    * MultirotorRpcLibAdaptors.hpp
    * MultirotorRpcLibClient.hpp
    * MultirotorRpcLibServer.hpp
  * firmwares
    * arducopter
    * mavlink
      * MavLinkMultirotorApi.hpp
      * Px4MultiRotorParams.hpp
    * simple_flight
  * MultiRotorParams.hpp
  * MultiRotorParamsFactory.hpp
  * MultiRotorPhysicsBody.hpp
  * RotorActuator.hpp
  * RotorParams.hpp
