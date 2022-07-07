# Point Cloud

* point_cloud.py script로 AirSim에서 받은 depth image를 point cloud로 변환
* 아래 depth image는 Modular Neighborhood 환경에서 얻은 것이다.
  ![img](https://microsoft.github.io/AirSim/images/depth.png)
* 적절한 projection matrix로 OpenCV reprojectImageTo3D function은 이 image를 point cloud로 변환할 수 있다.
* 아래는 변환 결과로 [여기서](https://sketchfab.com/3d-models/cloud-1c687dd6a03445879b0bade0f0b46ee5) 확인 가능
  ![img](https://microsoft.github.io/AirSim/images/point_cloud.png)
* [SketchFab](https://sketchfab.com/) 사이트에 cloud.asc를 올리면 랜더링해서 보여준다.
