# ROS2 기반 화성 탐사 로봇 프로젝트 / ROS_project_mars

> AI융합 로봇 SW 개발자 과정에서 진행한 팀 프로젝트입니다.  
> 본 저장소는 팀 프로젝트 결과물을 fork하여 정리한 저장소이며, 제가 담당한 ROS2 Navigation 및 센서 연동 내용을 중심으로 정리했습니다.

## My Role

- TurtleBot3에 초음파 센서를 추가하여 LiDAR 사각지대 보완
- 초음파 Range 데이터를 Nav2에서 활용 가능한 LaserScan 형태로 변환
- local_costmap obstacle_layer에 초음파 센서 데이터 반영
- obstacle_range, raytrace_range 등 Nav2 파라미터 조정
- 실제 주행 중 작은 장애물 인식 및 회피 반응 확인


## Project Structure

- arduino/ : Sensor data acquisition (CDS, IMU)
- python/  : Serial parsing and DB storage
- db/      : Database schema and queries

## Serial Permission
```bash
sudo usermod -a -G dialout $USER
reboot
```

## 🚀 Project Presentation

> ROS2 기반 알약 배송 로봇 시스템 발표 자료

[![presentation](./preview.png)](./MARS_PROJECT_final.pdf)
