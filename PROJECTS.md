# 프로젝트 포트폴리오

[← 프로필로 돌아가기](README.md)

## 1. Unity–ROS 2–Python 기반 UAV Multi-Sensor Real-Time Framework

> **상태:** 진행 중
>
> **핵심 분야:** Real-Time System Integration · Sensor Fusion · State Estimation
>
> **기술:** Unity 6, C#, ROS 2, Python, YOLO, PyTorch, TensorFlow

### 프로젝트 목표

Unity의 동적 UAV 시뮬레이션에서 Camera·IMU·UAV state를 생성하고, Python 기반 인식·센서융합·상태추정 알고리즘과 연결합니다. 기존의 파일 단위 후처리 파이프라인을 ROS 2 기반 frame 단위 처리 구조로 전환하는 것이 현재 통합 목표입니다.

### 현재 구현된 데이터 흐름

```text
Unity UAV–기지국 시나리오
 ├─ Camera image / YOLO label
 ├─ UAV pose / velocity / attitude
 └─ Camera / UAV / World 좌표계 정보
              ↓
YOLO 기지국 검출
              ↓
Camera-local bearing 계산
              ↓
Camera → UAV → World 좌표변환
              ↓
FNN 또는 CNN-LSTM 기반 방향 보정
              ↓
방향 오차 및 beamforming efficiency 평가
```

### ROS 2 통합 후 데이터 흐름

```text
Unity 6
 ├─ Camera frame
 ├─ IMU frame
 └─ UAV ground-truth state
              ↓ ROS 2
Python nodes
 ├─ YOLO perception
 ├─ MSCKF localization
 ├─ Neural sensor fusion
 └─ Frame-level evaluation
```

### 직접 구현한 기능

- Unity 기반 UAV–기지국 시뮬레이터와 LTI/N-LTV 동적 시나리오
- 자세 jitter, 이동속도 변화, 센서 noise 및 sampling mismatch 모델
- Camera image·YOLO label·UAV state 데이터 생성
- YOLO 학습·추론과 기지국 bounding box 검출
- pixel 좌표의 camera ray 변환
- Camera local → UAV local → World 좌표변환
- 기지국 azimuth/elevation 및 3차원 방향벡터 추정
- FNN·CNN-LSTM 기반 sensor fusion
- 방향 오차 및 beam alignment 성능평가
- 실험 설계, 결과 분석 및 논문 작성

### 주요 입출력

| 단계 | 입력 | 출력 |
|---|---|---|
| Unity simulation | 시나리오·noise 설정 | Camera image, UAV pose·velocity·attitude, ground truth |
| YOLO | Camera image | Bounding box, confidence |
| Geometry | Bounding box, camera/UAV attitude | World-frame direction, azimuth, elevation |
| Neural fusion | Geometry direction, camera bearing, attitude sequence | 보정된 방향 추정값 |
| Evaluation | 추정 방향, ground truth | Angular error, beamforming efficiency |

### 현재 구현 중인 항목

- ROS 2 topic/message 및 QoS 설계
- Unity publisher와 Python subscriber 연결
- Python 처리 결과의 Unity 반환 경로
- sensor timestamp 및 coordinate frame 규약
- raw IMU와 Camera frame 기반 MSCKF localization
- 처리 지연시간·frame 누락률·ATE/RPE 측정

### 공개 원칙

직접 작성한 코드와 재현 가능한 최소 예제만 공개합니다. 상용 Unity asset, 외부 데이터셋, 대용량 학습 산출물, 로컬 환경정보는 저장소에 포함하지 않습니다.

---

## 2. UAV Multi-Sensor Localization: EKF-Based Approach

### 문제

동적 UAV 환경에서는 단일 센서의 잡음과 비선형 관측모델 때문에 위치·속도·방향 추정오차가 누적됩니다.

### 접근

- 위치와 속도로 구성된 6차원 상태벡터 정의
- constant-velocity 기반 상태천이 모델
- Camera 방향정보와 IMU 속도정보를 결합한 비선형 관측모델
- Jacobian 기반 EKF prediction/update
- 시뮬레이터 데이터에서 process/measurement covariance 산출

### 결과

노이즈 측정값과 비교해 속도축 RMSE를 약 63–72%, azimuth/elevation RMSE를 약 91%/95% 감소시켰습니다. 결과는 ICTC 2025 국제학회 논문으로 발표했습니다.

---

## 3. FMCW Radar Signal Processing Simulator

### 구현 범위

- 77 GHz FMCW waveform 및 beat/Doppler 신호 모델링
- 거리 감쇠, RCS, matched filtering, 위상배열 안테나 모델
- fast-time 기반 range, slow-time 기반 velocity 추정
- antenna-domain FFT·MUSIC 기반 angle estimation
- compressed sensing 기반 resolution 개선 실험

### 검증 관점

거리·속도·각도 축의 추정오차와 분해능을 비교하고, antenna 수와 SNR 변화가 결과에 미치는 영향을 분석했습니다.

---

## 4. Model-Driven AI Signal Processing

### Deep Alternating Direction Network

UAV–RIS 채널추정을 위한 atomic norm minimization/ADMM 반복구조를 신경망 layer로 전개했습니다. spectral shift와 learnable fixed-point iteration을 적용해 low-pilot 환경의 추정 성능과 계산구조를 개선했습니다.

### EM-Based Fixed-Point Network

OFDM 위상잡음 추정과 데이터 복호를 반복하는 EM 구조를 신경망과 결합했습니다. 신호처리 모델의 구조적 해석 가능성과 학습 기반 보정능력을 함께 활용했습니다.

---

## 5. DDPM 기반 MIMO Channel Estimation

### 접근

- MIMO channel covariance와 angular spread 모델링
- 복소 채널에 대한 diffusion forward/reverse process 구성
- noise predictor 학습을 통한 channel denoising
- SNR과 angular spread 조건별 성능 비교

### 기여

특정 학습 SNR에 종속되지 않는 추정 구조를 설계하고, sparse channel 환경에서 통계 기반 기준기법과 성능을 비교했습니다. 결과는 ICTC 2024 국제학회에서 발표했습니다.
