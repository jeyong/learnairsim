# [Simple Avoidance](https://github.com/simondlevy/AirSimTensorFlow)

## 목적

* python script
* image data를 수집
* train
* deep-learning neural net in TensorFlow

## 사전 준비

* Windows 10 PC
* 설치
  * Unreal Engine 4
  * Python3
  * TensorFlow
    * CUDA 및 CuDNN 설치

## 따라하기

1. [repo](https://github.com/simondlevy/AirSimTensorFlow)를 clone
2. [Neighborhood ](https://github.com/Microsoft/AirSim/releases/download/v1.1.7/Neighbourhood.zip)예제 다운로드 후 run.bat 실행하여 AirSim 실행
3. 프롬프트 나오면 car simulation 선택. 키보드에서 숫자 3 누르고 neural net이 train될 image 보게 됨
4. repo에서 image_collection.py 실행. car가 움직이다가 충돌하면 정지. 생성된 carpix 폴더는 다음 단계에서 train할 image들이 들어가 있음.
5. repo에서 collision_training.py 실행. NVIDIA GeForce 1080Ti에서 500 training iteration을 완료하는데 몇 초내에 가능
6. repod에서 collision_testing.py 실행. car를 전과 같이 전진 운행하지만 벽에 부딪히기 전에 바로 stop하는데 neural net에서 예측한 collision을 기반.

## 동작원리

* image_collection script는 1개의 가장 최신 image를 queeu에 유지하고 carpix 폴더에 숫자를 붙여서 저장한다.
* collision_training script는 color image를 greyscale로 변환. 이후 모든 images에서 training set을 만들고 마지막 image를 제외하고 safe로 label을 붙이고(no collision; code [1 0]). 마지막 image에는 collision (code [0 1])로 label 붙인다.
* 마지막 단계로 이 training script은 Python의 built-in pickle library를 사용하여 trained network parameters(weight와 biases)를 저장한다. collision_testing script은 pickle를 사용하여 이 parameters를 restore하고 나서 이를 바탕으로 TensorFlow neural net을 재구성한다.(일너 접근법은 TensorFlow의 save-and-restore API를 사용하는 것보다 더 쉽다는 것을 알았다)
* 마지막으로 collision_testing script으로 car를 이동시키고 live image를 grayscale로 변환하고 collision/no-collision prediction을 할 수 있는 network를 통해서 실행한다. "collision bit"의 값은 0.5를 초과할때 script는 breke로 car를 멈추게 한다.

## 향후 작업

* single-layer logistic regression network은 단순한 proof-of-concept 예제를 제공한다. 하지만 다른 종류의 물체와 충돌하는 좀더 사실적인 data set에 대해서는 convolutional network이 더 잘 된다(make more sense). AirSim은 자율주행차에 Lidar와 같이 depth images에 접근을 제공하며(키보드에서 숫자 1을 누르면) 충돌 회피에 필요한 가치 있는 추가 정보를 제공받을 수 있다.
