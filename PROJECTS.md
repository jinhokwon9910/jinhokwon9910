# 프로젝트 포트폴리오

[← 프로필로 돌아가기](README.md)

연구는 `Sensing → Estimation → Beam / Link Decision → Feedback` 축을 따라 세 묶음으로 구성했습니다. 저자 기여와 서지정보는 [논문 · 특허 · 수상](PUBLICATIONS.md)에 정리했습니다.

| | 프로젝트 | 상태 |
|---|---|---|
| **P1** | Deep Alternating Direction Network — UAV-RIS 채널추정 | IEEE WCL · 게재 |
| **P2** | EM-Based Fixed-Point Network — OFDM 위상잡음 보상 | IEEE TVT · 게재 |
| **P3** | LEO NTN One-Shot 다중위성 획득 | IEEE TWC · 심사 중 |
| **P4** | ISAC 빔포머 최적화 | 진행 중 |
| **P5** | UAV Multi-Sensor Localization (EKF) | ICTC 2025 |
| **P6** | FMCW Radar Signal Processing Simulator | — |
| **P7** | DDPM 기반 MIMO 채널추정 | ICTC 2024 |
| **P8** | Unity–ROS 2–Python UAV Sensor-Frame Integration | 구현·검증 |

---

# Part 1. 무선 신호처리 알고리즘

반복 최적화 알고리즘이 갖는 구조적 해석 가능성과 학습 기반 기법의 보정 능력을 결합해, 추정 성능과 연산 복잡도를 함께 다루는 것이 이 묶음의 공통 주제입니다.

## P1. Deep Alternating Direction Network — UAV-RIS 채널추정

> **IEEE Wireless Communications Letters** · 제2저자 · 게재 (2025.11) · [DOI](https://doi.org/10.1109/LWC.2025.3592730)

### 문제

mmWave UAV-RIS 링크에서 수신단이 관측하는 것은 송신–RIS 채널과 RIS–수신 채널이 겹쳐진 cascaded 채널이며, 여기에 RIS의 수동 반사와 UAV 이동에 따른 Doppler가 더해집니다. 각도를 격자로 이산화하는 압축센싱 계열 기법은 off-grid 오차를 남기고, 이를 피하는 atomic norm minimization의 SDP 정식화는 대규모 안테나 배열에서 행렬 연산 비용이 급격히 커집니다. 추정 정확도와 pilot overhead, 연산량이 동시에 제약되는 문제입니다.

### 접근

- ADMM 반복을 신경망 layer로 전개한 심층 구조(DADU-Net) 구성
- spectral shift 연산으로 최적화 제약을 근사하여 대규모 배열에 대한 확장성 확보
- 수렴 상황에 따라 layer 수를 조절하는 learnable fixed-point iteration으로 확장(DADF-Net)
- 기존 알고리즘의 하이퍼파라미터를 학습 대상으로 전환하고, 반복 구조의 학습 파라미터를 재사용

### 결과

낮은 pilot overhead 조건에서 gridless 추정을 유지하면서 SDP 기반 정식화의 확장성 한계를 완화했습니다. RIS 크기, 경로 수, SNR을 변화시킨 조건에서 격자 기반 기법 및 기존 unfolding 기법과 성능을 비교했습니다.

---

## P2. EM-Based Fixed-Point Network — OFDM 위상잡음 보상

> **IEEE Transactions on Vehicular Technology** · 공동 제1저자 · 게재

### 문제

국부발진기의 위상잡음은 OFDM 부반송파 간 직교성을 무너뜨려 간섭을 발생시킵니다. 위상잡음을 알아야 데이터를 복호할 수 있고, 데이터를 알아야 위상잡음을 정확히 추정할 수 있는 결합 문제이므로 두 과정을 번갈아 수행하는 EM 반복이 자연스러운 해법이 되지만, 반복 횟수와 초기값에 따라 성능이 크게 달라집니다.

### 접근

- a posteriori symbol expectation(E-step)과 위상잡음 추정(M-step)으로 구성된 EM 반복 구조 정식화
- E-step을 신경망 posterior inference로 대체하여, 신호처리 모델의 구조와 학습 기반 보정을 하나의 반복 안에서 결합
- termination test를 둔 고정점 반복으로 반복 횟수를 입력 조건에 맞춰 제어

### 결과

신호처리 기법과 신경망을 각각 단독으로 적용한 경우 대비 위상잡음 추정 성능과 복호 성능을 함께 개선했습니다. 관련 기법은 특허로 출원했습니다.

---

## P3. LEO NTN One-Shot 다중위성 획득

> **IEEE Transactions on Wireless Communications** · 공동 제1저자 · **심사 중**

### 배경

저궤도 위성은 수 분 단위로 하늘을 가로지르므로 단말은 반복적으로 위성을 획득하고 추적해야 하며, 코드북을 훑는 통상적 빔 관리는 매 패스마다 훈련 부담을 발생시킵니다. 광대역 배열에서 주파수에 따라 빔 방향이 흔들리는 beam squint는 보통 보상 대상으로 다뤄지지만, rainbow beamforming은 이를 주파수–각도 매핑 자원으로 전환해 단일 아날로그 설정으로 궤도면의 다중 위성을 한 번에 획득합니다 [R1].

### 본 연구

이 획득 구조가 전제하는 정렬 기하가 실제 단말에서는 성립하지 않는다는 점에서 출발해, 배열–궤도 오정렬 기하로 문제를 확장했습니다.

> 심사 중인 논문입니다. **본문 · 수식 · 수치결과 · 코드는 공개하지 않으며**, 제목과 저자 기여만 표기합니다.

**[R1]** J. Park, I. P. Roberts, and W. Shin, "Rainbow Beamforming: One-Shot Acquisition of Multiple Satellites in LEO Non-Terrestrial Networks," *IEEE Transactions on Vehicular Technology*, 2026.

---

## P4. ISAC 빔포머 최적화

> **진행 중**

통합 센싱·통신 환경에서의 빔포머 최적화를 진행하고 있습니다. 공개 가능한 시점에 갱신합니다.

---

# Part 2. 다중센서 상태추정

앞선 묶음이 RF 관측으로부터 채널을 추정하는 문제라면, 이 묶음은 이기종 센서 관측으로부터 이동체의 상태를 추정하는 문제를 다룹니다. 관측모델의 비선형성과 센서별 잡음 통계를 어떻게 추정 과정에 연결하는가가 공통 쟁점입니다.

## P5. UAV Multi-Sensor Localization: EKF-Based Approach

> **ICTC 2025** · 발표

### 문제

동적 UAV 환경에서는 단일 센서의 잡음과 비선형 관측모델 때문에 위치·속도·방향 추정오차가 누적됩니다.

### 접근

- 위치와 속도로 구성된 6차원 상태벡터 정의
- constant-velocity 기반 상태천이 모델
- Camera 방향정보와 IMU 속도정보를 결합한 비선형 관측모델
- Jacobian 기반 EKF prediction/update
- 시뮬레이터 데이터에서 process/measurement covariance를 산출해 추정과 성능평가에 연결

### 결과

노이즈 측정값과 비교해 속도축 RMSE를 약 **63–72%**, azimuth/elevation RMSE를 약 **91% / 95%** 감소시켰습니다.

---

## P6. FMCW Radar Signal Processing Simulator

### 구현 범위

- 77 GHz FMCW waveform 및 beat/Doppler 신호 모델링
- 거리 감쇠, RCS, matched filtering, 위상배열 안테나 모델
- fast-time 기반 range, slow-time 기반 velocity 추정
- antenna-domain FFT · MUSIC 기반 angle estimation
- compressed sensing 기반 resolution 개선 실험

### 검증 관점

거리·속도·각도 축의 추정오차와 분해능을 비교하고, antenna 수와 SNR 변화가 결과에 미치는 영향을 분석했습니다.

---

## P7. DDPM 기반 MIMO 채널추정

> **ICTC 2024** · 제1저자

### 접근

- MIMO channel covariance와 angular spread 모델링
- 복소 채널에 대한 diffusion forward/reverse process 구성
- noise predictor 학습을 통한 channel denoising
- SNR과 angular spread 조건별 성능 비교

### 결과

특정 학습 SNR에 종속되지 않는 추정 구조를 설계하고, sparse channel 환경에서 통계 기반 기준기법과 성능을 비교했습니다.

---

# Part 3. 실시간 시스템 통합

앞의 두 묶음에서 성능을 확인한 알고리즘이 실제 시간축 위에서도 같은 성능을 내는지가 이 묶음의 질문입니다.

## P8. Unity–ROS 2–Python UAV Sensor-Frame Integration

> 상태: ROS 2 sensor-frame vertical slice 구현·검증, localization·closed-loop 제어 후속
>
> 기술: Unity 6, C#, ROS 2, Python, YOLO, PyTorch, TensorFlow

### 목표

기존의 Unity–Python 파일 후처리 파이프라인을 ROS 2 기반 online 경로로 확장했습니다. Unity의 Camera image · noisy UAV pose · Camera orientation · FoV · sequence를 한 message로 전달하고, Python의 YOLO 및 기하 계산 결과를 같은 source sequence로 Unity에 반환합니다.

### 신호처리 데이터 흐름

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
→ BeamDirectionEstimate(source_sequence = N)
→ Unity sequence match / lockstep 해제 / cyan ray
```

### 직접 구현한 기능

- Unity 기반 UAV–기지국 시뮬레이터와 LTI/N-LTV 동적 시나리오
- 자세 jitter, 이동속도 변화, 센서 noise 및 sampling mismatch 모델
- Camera image · YOLO label · UAV state 데이터 생성
- YOLO 학습·추론과 기지국 bounding box 검출
- pixel 좌표의 camera ray 변환
- Camera local → UAV local → World 좌표변환
- 기지국 azimuth/elevation 및 3차원 방향벡터 추정
- FNN · CNN-LSTM 기반 sensor fusion
- 방향 오차 및 beam alignment 성능평가
- 실험 설계, 결과 분석 및 논문 작성
- `SensorFrame` · `BeamDirectionEstimate` custom message와 Unity C# bridge
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

- FNN · CNN-LSTM 보정의 live callback 통합과 offline regression
- raw IMU · Camera 기반 MSCKF localization 및 ATE/RPE 평가
- failure injection과 반복 latency/drop p50 · p95 측정
- 빔 방향과 UAV state를 활용한 action command 및 Unity dynamics 적용

### 공개 원칙

직접 작성한 핵심 integration code와 sanitized evidence만 선별해 공개합니다. 상용 Unity asset, 외부 데이터셋, 학습 weight, 로컬 실행환경과 학습용 구축 가이드는 저장소에 포함하지 않습니다.

[저장소](https://github.com/jinhokwon9910/uav-multisensor-real-time-framework)
