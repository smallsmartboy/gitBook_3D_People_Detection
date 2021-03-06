# Open Data
## 1. Lidar

### 1.1 L-CAS 3D Point Cloud People Dataset

- [Lincoln Centre for Autonomous Systems](https://lcas.lincoln.ac.uk/wp/research/data-sets-software/l-cas-3d-point-cloud-people-dataset/)
- 센서 :  Velodyne VLP-16
- 수집 데이터 : 영국 링컨 대학교에서 49분간, 28,002 Velodyne scan frames, [[다운로드]](https://lcas.lincoln.ac.uk/owncloud/index.php/s/wu2NILXZ7mzjovS), 

- 제공 데이터
  - Robot Operating System (ROS) rosbag files recording ground truth from the 3D LiDAR, robot odometry, ROS transform tree, as well as a panoramic camera.
  - Point Cloud Data (PCD) files corresponding to each scan frame, which is the official file format supported by the Point Cloud Library (PCL).
  - Annotation files in text format, including single-person (pedestrian) labels and human-group (group) labels.
  - A Qt-based GUI tool for data annotation, providing a semi-automatic labelling function, released as open-source.

- label data

```
pedestrian 16.8915 0.282575 0.0424143 16.7578 0.0922886 -0.296726 17.0572 0.498739 0.297738 0
pedestrian 6.55263 0.582247 0.132658 6.34313 0.284879 -0.561632 6.95758 0.850341 0.822374 0
pedestrian 7.62397 -0.641525 0.162471 7.3658 -0.872086 -0.67842 7.73205 -0.440035 0.662384 0
pedestrian 13.5868 1.9875 0.214493 13.4329 1.83353 -0.241367 13.8208 2.21375 0.724958 0
pedestrian -3.31128 -3.02812 -0.0352137 -3.61874 -3.23663 -0.392724 -3.1304 -2.77111 0.408237 0
pedestrian 1.13967 -8.59664 0.111699 0.982876 -8.71929 -0.444542 1.29828 -8.34763 0.455323 0
pedestrian 12.6652 2.21514 0.47063 12.508 2.12521 0.22175 12.7653 2.35142 0.679425 0
pedestrian 14.9873 0.837819 -0.262016 14.8933 0.72961 -0.264125 15.1031 0.947489 -0.26032 0
```

Column 1:	category (pedestrian or group)
Column 2-4:	centroid (x-y-z)
Column 5-7:	minimum bounds (x-y-z)
Column 8-10:	maximum bounds (x-y-z)
Column 11:	visibility (0 = visible, 1 = partially visible)



> [Annotation tool](https://github.com/lcas/cloud_annotation_tool) 제공


### 1.2 Stanford Track Collection

- about 1.3 million labeled point clouds in about 14,000 tracks recorded from an autonomous vehicle 

- The TorontoCity benchmark [12] collects LIDAR data and images including stereo and panoramas from both drones and moving vehicles.


## 2. image

[Indoor Multi-Camera Pedestrian Datasets](https://www.tugraz.at/institute/icg/research/team-bischof/lrs/downloads/MultiCam/)

[Apollo Scape](http://apolloscape.auto/index.html): [논문](https://arxiv.org/abs/1803.06184), [정리](https://medium.com/syncedreview/baidu-apollo-releases-massive-self-driving-dataset-teams-up-with-berkeley-deepdrive-5e785ab4053b)

---


# 툴 활용 방안

## 1. 3D ANNOTATION TOOL

- annotate objects in a point cloud scene
- 원래는 it was developed with the aim to annotate the objects of a table

### 1.1 L-CAS Annotation tool

- [깃허브](https://github.com/lcas/cloud_annotation_tool)
- 개발 환경 : VTK5, Qt4, and PCL1.7 under Ubuntu 14.04.
- qt4 docker : `docker pull msoares/qt4-dev`

- Prerequisites
```
sudo apt-get install libqt4-dev qt4-qmake
sudo apt-get install libvtk5-dev python-vtk
sudo apt-get install libpcl-1.7-all-dev # add-apt-repository ppa:v-launchpad-jochen-sprickerhof-de/pcl
```

- Build script
```
git clone https://github.com/LCAS/cloud_annotation_tool.git
cd cloud_annotation_tools
mkdir build
cd build
cmake .. # apt-get install cmake
make
```

에러 #1 : libGL error: failed to load driver: swrast -> [nvidia 드라이버 재설치](https://github.com/adioshun/System_Setup/wiki/4_CUDA_CuDNN-Setup#%EC%B0%B8%EA%B3%A0-%EB%93%9C%EB%9D%BC%EC%9D%B4%EB%B2%84-%EC%84%A4%EC%B9%98)

에러 #2 : Xlib: extension "NV-GLX" missing on display "localhost:10.0".-> remove the nouveau module `sudo apt-get --purge remove xserver-xorg-video-nouveau`


## 2. 시뮬레이터 툴

### 2.1 Velodyne Simulator

- [Velodyne Simulator](https://github.com/LCAS/velodyne_simulator)

### 2.2 Google 3D Warehouse

[Object Recognition in 3D Point Clouds Using Web Data and Domain Adaptation](https://pdfs.semanticscholar.org/ecc2/ea05877d720b725fb89bc3b0586a51cabdc7.pdf): Lai, K, 2011


## 9. IDEA

- [People font](https://flowingdata.com/2018/02/09/people-font/)를 학습용 데이터로 사용하는것은 어떨까?


---

# 업체 


![image](https://user-images.githubusercontent.com/17797922/39740494-c7ecef8a-52d0-11e8-9c18-7de1aae07b69.png)


|구분|이름|특징|
|-|-|-|
|Tool(2D)|[LanelImg](https://github.com/tzutalin/labelImg)|TFRecord로 변경 가능 |
|Tool(2D)|[FIAT (Fast Image Data Annotation Tool)](https://github.com/christopher5106/FastAnnotationTool)||
|Tool(2D)|[Yolo_mark](https://github.com/AlexeyAB/Yolo_mark)|YOLO용, Windows & Linux GUI|
|Tool(2D)|sloth||
|Took(2D)|[Supervisely-Smart Tool](https://supervise.ly/smart-tool/)|웹기반|
|Tool(2D)|[The Human Annotation Tool](https://www2.eecs.berkeley.edu/Research/Projects/CS/vision/shape/hat/)|사람 Part별 라벨링, 2011|
|Tool(3D)|[SceneNN](http://people.sutd.edu.sg/~saikit/projects/sceneNN/)|RGB-D, 세그멘테이션, 라벨링|
|Tool(3D)|[3D ANNOTATION TOOL](http://strands.readthedocs.io/en/latest/annotation_tool_kth/annotation-tool.html)|ROS, PCD, XML, 2015|
|Tool(3D)|[L-CAS](https://github.com/yzrobot/cloud_annotation_tool)|**추천 방안**|
|Tool(3D)|[]()||
|Service|[CrowdFlower](https://www.crowdflower.com/)|해외업체, |
|Service|[CrowdAI ](https://crowdai.com/)|해외업체, 항공사진등에서 물체, 도로 라벨링|
|Service|[Amazon’s Mechanical Turk](https://www.mturk.com/mturk/welcome)|해외업체|
|Service|[supervise.ly](https://supervise.ly/company)|해외업체|
|Service|[crowdworks](http://www.crowdworks.kr)|국내업체|
|Service|[playment](https://playment.io/image-annotation/)|해외업체|
|Service|[Mighty AI](https://mty.ai/)||

- [List of manual image annotation tools](https://en.wikipedia.org/wiki/List_of_manual_image_annotation_tools): 위키 정리
- [Annotating Large Datasets with the TensorFlow Object Detection API](http://andrew.carterlunn.co.uk/programming/2018/01/24/annotating-large-datasets-with-tensorflow-object-detection-api.html): 딥러닝 기 라벨링 기법

# 협력 업체 확용 방안

### CrowdFlower

- 데이터 수집, 2D 라벨링
- 3D 라벨링 문의 메일 발송

### Amazon’s Mechanical Turk

- 데이터 수집, 2D 라벨링
- 3D 라벨링 문의 메일 발송

### supervise.ly

- 데이터 수집, 2D 라벨링
- 3D 라벨링 문의 메일 발송 -> 현재 지원 안함, 향후 지원 예정

### crowdworks

- 중계 업체 (사용자-요청자) : 요청자가 가격을 제시, 사용자가 원하는 작업 선택 진행
- 성별 판단의 경우 약 200,000이미지를 112명이 3,300,000원에 17일간 작업 진행 (이미지당 5원)
- 강남삼성사옥 건너편 강남역 2번출구 메리츠타워 16층입니다


