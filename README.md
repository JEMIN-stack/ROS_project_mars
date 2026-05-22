# ROS2 기반 화성 탐사 로봇 프로젝트 / ROS_project_mars

> AI융합 로봇 SW 개발자 과정에서 진행한 팀 프로젝트입니다.  
> 본 저장소는 팀 프로젝트 결과물을 fork하여 정리한 저장소이며, 제가 담당한 ROS2 Navigation 및 센서 연동 내용을 중심으로 정리했습니다.

## My Role

- TurtleBot3에 초음파 센서를 추가하여 LiDAR 사각지대 보완
- 초음파 Range 데이터를 Nav2에서 활용 가능한 LaserScan 형태로 변환
- local_costmap obstacle_layer에 초음파 센서 데이터 반영
- obstacle_range, raytrace_range 등 Nav2 파라미터 조정
- 실제 주행 중 작은 장애물 인식 및 회피 반응 확인

## System Flow

본 프로젝트는 사전에 저장된 map을 사용하는 방식이 아니라, `slam_toolbox`를 통해 실시간으로 지도를 생성하면서 탐색을 수행하는 구조로 진행했습니다.

### Navigation Flow

- TurtleBot3 LiDAR에서 `/scan` 데이터 발행
- `slam_toolbox`가 `/scan`, `/odom`, `/tf`를 활용하여 실시간 `/map` 생성
- `explore_lite`가 생성 중인 map에서 미탐색 영역(frontier)을 탐색
- `explore_lite`가 Nav2에 탐색 goal 전송
- Nav2가 현재 map과 costmap을 기반으로 경로 계획 및 `/cmd_vel` 생성
- RViz에서 `/map`, `/scan`, TF, costmap, robot pose, goal 상태 확인

### Ultrasonic Sensor Flow

- 초음파 센서 데이터 `/ultrasonic/front` 수신
- `range_to_scan`을 통해 Nav2에서 활용 가능한 `/ultrasonic/scan` 형태로 변환
- Nav2 `local_costmap`의 `obstacle_layer`에 초음파 센서 데이터 반영
- LiDAR 사각지대에 있는 작은 장애물 인식 및 회피 반응 확인

본 프로젝트에서 핵심적으로 확인한 부분은 자율 탐사 패키지(explore_lite)를 실행하는 것에 추가로 SLAM으로 생성되는 map, Nav2 costmap, 센서 데이터 흐름이 실제 주행 반응으로 이어지는지를 검증하는 것이었습니다.

### Environment Data Flow

- OpenCR/Arduino 계열 보드에 조도 센서와 온습도 센서 연결
- 센서 데이터를 Raspberry Pi/Linux 환경에서 수신
- Python 기반 파싱 및 DB 저장
- 저장된 환경 데이터를 웹 화면에서 조회
  
## Project Structure

- ros2/ : ROS2 navigation, SLAM, explore_lite, sensor integration settings
- arduino/ : OpenCR/Arduino 계열 보드 기반 환경 센서 데이터 수집 코드
- python/ : 센서 데이터 파싱, DB 저장, 웹 연동 코드
- db/ : 환경 데이터 저장을 위한 database schema and queries


## Serial Permission
```bash
sudo usermod -a -G dialout $USER
reboot
```

## 🚀 Project Presentation

> ROS2 기반 알약 배송 로봇 시스템 발표 자료

[![presentation](./preview.png)](./MARS_PROJECT_final.pdf)
