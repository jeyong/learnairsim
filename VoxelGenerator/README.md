# [Voxel Generator](https://microsoft.github.io/AirSim/voxel_grid/)

* Unreal Engine으로부터 world의 voxel grid를 생성하는 기능을 제공
* voxel grid는 world/map의 occupancy를 표현하기 위해서 특정 size의 cell로 discretizing 방법을 사용한다. 특정 location이 채워져 있는지 여부를 voxel로 저장

## Voxel grid 생성

* WorldSimApi.cpp->createVoxelGrid() 내에 logic
* 가정 : voxel grid는 cube로

```python

simCreateVoxelGrid(self, position, x, y, z, res, of)

position (Vector3r): Global position around which voxel grid is centered in m
x, y, z (float): Size of each voxel grid dimension in m
res (float): Resolution of voxel grid in m
of (str): Name of output file to save voxel grid as
```

* createVoxelGrid() 내에서 occupancy를 반환하는 Unreal Engine 메인 함수는 OverlapBlockingTestByChannel이다.
* ![img](https://microsoft.github.io/AirSim/images/octomap.png)
* 예제에서 voxel grid는 다음과 같이 생성될 수 있다.


```python

import airsim
c = airsim.VehicleClient()
center = airsim.Vector3r(0, 0, 0)
output_path = os.path.join(os.getcwd(), "map.binvox")
c.simCreateVoxelGrid(center, 100, 100, 100, 0.5, output_path)
```

* viewvox map.binvox를 통해서 시각화
