# 권진호 | 실시간 시스템 통합 · 센서융합 · 신호처리

동적 시스템에서 발생하는 이기종 센서 데이터를 **시간축과 좌표계 기준으로 통합**하고, 상태추정·신호처리 알고리즘을 **검증 가능한 소프트웨어 파이프라인**으로 구현해 왔습니다.

> **Positioning:** Real-Time System Integration | Sensor Fusion | Signal Processing

## 지원 분야

- 방산 무인체계 SW 통합·아키텍처
- 자동차 전장 시스템 SW·알고리즘
- 실시간 데이터 통합, 센서융합, 상태추정

## 핵심 역량

| 역량 | 구현 및 연구 경험 |
|---|---|
| **실시간 시스템 통합** | Unity 기반 동적 환경과 Python 신호처리 파이프라인 구축, ROS 2 기반 frame 단위 데이터 흐름으로 확장 중 |
| **센서융합·상태추정** | Camera·IMU·UAV state 통합, EKF 및 신경망 기반 추정, MSCKF localization 구현 중 |
| **좌표계·기하 처리** | Camera local → UAV local → World 좌표변환, 영상 검출 결과의 3차원 방향벡터 변환 |
| **신호처리 알고리즘** | FMCW Radar, MIMO 채널추정, beamforming, MUSIC·ESPRIT·OMP, model-driven deep learning |
| **AI 모델 설계·검증** | YOLO fine-tuning, FNN·CNN-LSTM sensor fusion, DDPM, deep unfolding/fixed-point network |
| **성능평가** | RMSE·각도오차·beamforming efficiency·모델 복잡도 비교, 시뮬레이션 기반 정량 검증 |

## 대표 프로젝트

### Unity–ROS 2–Python 기반 UAV Multi-Sensor Real-Time Framework `진행 중`

Unity 6에서 UAV–기지국 동적 시나리오와 Camera·IMU·UAV state를 생성하고, ROS 2를 통해 Python의 인식·센서융합·상태추정 알고리즘을 frame 단위로 연결하는 프로젝트입니다.

**현재 구현**

- UAV 이동·자세 변화와 jitter/noise를 포함한 Unity 시뮬레이터
- Camera image, YOLO label, UAV pose·velocity·direction 데이터 생성
- YOLO 기반 기지국 검출 및 camera–UAV–world 좌표변환
- FNN·CNN-LSTM 기반 방향 추정 보정과 beam alignment 성능평가

**현재 통합 중**

- Unity ↔ ROS 2 ↔ Python 양방향 데이터 흐름
- timestamp·frame ID·QoS를 포함한 실시간 센서 인터페이스
- Camera–IMU 기반 MSCKF localization
- frame latency, 누락률, localization 오차의 end-to-end 평가

**직접 기여:** Unity 시나리오 및 센서 데이터 생성, YOLO 학습·추론, 좌표변환, 신경망 sensor fusion, 성능평가, 논문 작성, ROS 2·MSCKF 통합 설계·구현(진행 중)

[대표 프로젝트 상세 보기](PROJECTS.md#1-unityros-2python-기반-uav-multi-sensor-real-time-framework) · [프로젝트 저장소](https://github.com/jinhokwon9910/uav-multisensor-real-time-framework)

## 주요 프로젝트·연구

### UAV Multi-Sensor Localization

동적 UAV 환경에서 Camera·IMU 기반 측정값을 구성하고, 6차원 상태벡터에 대한 EKF로 위치·속도·방향을 추정했습니다. 시뮬레이터의 process/measurement noise 통계를 추정 과정과 성능평가에 연결했습니다.

### FMCW Radar Signal Processing Simulator

77 GHz FMCW radar의 range–velocity–angle 추정 과정을 MATLAB/Python으로 구성하고, FFT·MUSIC·compressed sensing 계열 알고리즘의 분해능과 추정 성능을 비교했습니다.

### Model-Driven AI Signal Processing

ADMM·EM과 같은 반복 신호처리 알고리즘을 deep unfolding 및 fixed-point network로 확장해, 추정 성능과 연산 복잡도를 함께 개선하는 연구를 수행했습니다.

### DDPM 기반 MIMO Channel Estimation

MIMO 채널의 통계적 구조와 diffusion model을 결합해 SNR 및 angular spread 변화에 강인한 채널추정 기법을 설계하고 성능을 분석했습니다.

[전체 프로젝트 보기](PROJECTS.md) · [논문·특허·수상 보기](PUBLICATIONS.md)

## 연구 성과

- 국제 저널: **IEEE WCL 1편, IEEE TVT 1편 게재**
- 국제학회: **ICTC 3편 발표**
- 국내학회: **제1저자 4편 발표**
- 후속 연구: **IEEE 논문 1편 제출, 1편 제출 준비 중**
- 특허: **3건 출원 기여**
- 학술대회: **논문 경진대회 우수상 2회, 아이디어 경진대회 수상 2회**
- NRF·KIAT·IITP 연구과제 참여

## 기술 스택

| 구분 | 기술 |
|---|---|
| Languages | Python, C#, MATLAB |
| System & Robotics | Unity 6, ROS 2, WSL2, Git |
| AI | PyTorch, TensorFlow, Ultralytics YOLO |
| Estimation & Fusion | EKF, MSCKF(구현 중), FNN, CNN-LSTM |
| Signal Processing | MIMO, Beamforming, FMCW Radar, MUSIC, ESPRIT, OMP, ADMM, EM, DDPM |

## 개발 관점

알고리즘의 단일 정확도보다 **입출력 정의, 좌표계 일관성, timestamp 동기화, 지연시간, 실패 조건과 재현성**까지 함께 설계하는 것을 중요하게 생각합니다.
