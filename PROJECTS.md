# 프로젝트 포트폴리오

[← 프로필로 돌아가기](README.md)

## 1. Unity–ROS 2–Python UAV Sensor-Frame Integration

> **상태:** ROS 2 sensor-frame vertical slice 구현·검증, localization·closed-loop 제어 후속
>
> **핵심 분야:** Heterogeneous Runtime Integration · Frame Correlation · Beam Direction Estimation
>
> **기술:** Unity 6, C#, ROS 2, Python, YOLO, PyTorch, TensorFlow

### 프로젝트 목표

기존 Unity–Python 파일 후처리 파이프라인을 ROS 2 기반 online 경로로 확장했습니다. Unity의 Camera image·noisy UAV pose·Camera orientation·FoV·sequence를 한 message로 전달하고, Python의 YOLO·기하 계산 결과를 같은 source sequence로 Unity에 반환합니다.

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

### 검증한 ROS 2 데이터 흐름

```text
Unity SensorFrame(N)
  → ROS-TCP Connector / TCP
  → ROS-TCP Endpoint / ROS 2 DDS
  → WSL ROS 2 Python adapter
  → Windows Conda persistent YOLO worker
  → pixel-to-bearing / quaternion geometry
  → BeamDirectionEstimate(source_sequence=N)
  → Unity sequence match / lockstep 해제 / cyan ray
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
- `SensorFrame`·`BeamDirectionEstimate` custom message와 Unity C# bridge
- same-sequence 수락, stale 거부, wall-clock timeout, `Time.timeScale` 복원
- WSL ROS 2와 Windows Conda YOLO를 분리한 persistent worker 경계
- ROS graph roundtrip과 Unity–ROS 2–YOLO–Unity 통합 smoke run

### 주요 입출력

| 단계 | 입력 | 출력 |
|---|---|---|
| Unity simulation | 시나리오·noise 설정 | Camera image, UAV pose·velocity·attitude, ground truth |
| YOLO | Camera image | Bounding box, confidence |
| Geometry | Bounding box, camera/UAV attitude | World-frame direction, azimuth, elevation |
| Neural fusion | Geometry direction, camera bearing, attitude sequence | 보정된 방향 추정값 |
| Evaluation | 추정 방향, ground truth | Angular error, beamforming efficiency |

### 현재 검증 범위

- Unity publisher → Python subscriber → Python publisher → Unity subscriber 왕복
- `source_sequence`에 의한 원본 frame과 결과 correlation
- Python estimator 측 `RELIABLE`, `VOLATILE`, `KEEP_LAST(1)` QoS
- 검출 실패 status와 응답 timeout에서 simulation state 복원
- 실제 YOLO workload 기준 단일 smoke run `STATUS_OK` 3회

### 후속 항목

- FNN·CNN-LSTM 보정의 live callback 통합과 offline regression
- raw IMU·Camera 기반 MSCKF localization 및 ATE/RPE 평가
- failure injection과 반복 latency/drop p50·p95 측정
- 빔 방향과 UAV state를 활용한 action command 및 Unity dynamics 적용

### 공개 원칙

직접 작성한 핵심 integration code와 sanitized evidence만 선별해 공개합니다. 상용 Unity asset, 외부 데이터셋, 학습 weight, 로컬 실행환경과 학습용 구축 가이드는 저장소에 포함하지 않습니다.

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
