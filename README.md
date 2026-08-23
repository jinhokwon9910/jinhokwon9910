# 권진호 | Jinho Kwon

**센싱 · 추정 · 빔/링크 결정을 하나의 실시간 루프로 닫는 무선 신호처리 엔지니어**

동적 환경에서 얻어지는 이기종 센서·RF 관측을 시간축과 좌표계 기준으로 통합하고, 그 관측으로부터 상태와 채널을 추정하며, 추정 결과를 빔 방향과 링크 설정이띴는 실제 결정까지 연결하는 연구를 해왔습니다. 알고리즘은 IEEE 저널 논문으로, 시스템은 동작하는 실시간 파이프라인으로 각각 검증했습니다.

`Sensing → Estimation → Beam / Link Decision → Feedback`

---

## 지원 분야

- 방산 무인체계·위성통신 신호처리 및 SW 통합
- 자동차 전장 시스템 알고리즘 (레이더 신호처리, V2X)
- 무선 신호처리 연구 (채널추정, 빔포밍, ISAC, NTN)

---

## 연구 실적

| 성과 | 게재지 | 상태 | 기여 |
|---|---|---|---|
| Deep Alternating Direction Networks for UAV-RIS-Assisted Channel Estimation | IEEE Wireless Commun. Lett. | **게재** (2025.11) | 제2저자 |
| Joint Phase Noise Estimation and Data Decoding with EM-Based Fixed-Point Network | IEEE Trans. Veh. Technol. | **게재** | **공동 제1저자** |
| Rainbow Beamforming under Array–Orbit Misalignment: One-Shot Multi-Satellite Acquisition in LEO Non-Terrestrial Networks | IEEE Trans. Wireless Commun. | 심사 중 | **공동 제1저자** |
| ISAC 빔포머 최적화 | — | 진행 중 | — |
| A Multi-Modal Simulator for Aerial Communication with Applications to Beam Search | ICTC 2025 | 발표 | 제1저자 |
| Denoising Diffusion Probabilistic Models for Channel Estimation | ICTC 2024 | 발표 | 제1저자 |

특허 3건 출원 기여 · NRF · KIAT · IITP 연구과제 참여

전체 목록은 [논문 · 특허 · 수상](PUBLICATIONS.md)에서 확인하실 수 있습니다.

---

## 핵심 역량

| 축 | 역량 | 근거 |
|---|---|---|
| **Sensing** | 다중센서·RF 관측 모델링 | Unity 기반 다중센서 시뮬레이터, 77 GHz FMCW 레이더 시뮬레이터, IMU·Camera 노이즈 및 비동기 모델링 |
| **Estimation** | 상태추정 · 채널추정 | EKF, MSCKF(구현 중), ANM · ADMM · EM 기반 추정, deep unfolding 및 fixed-point network |
| **Decision** | 빔 정렬 · 빔포밍 설계 | 다중센서 기반 beam alignment, LEO NTN 빔 획득, ISAC 빔포머 최적화 |
| **Integration** | 실시간 파이프라인 | Unity–ROS 2–Python sensor-frame 왕복, source sequence · lockstep · timeout 기반 흐름 검증 |
| **Evaluation** | 정량 검증 | RMSE · 각도오차 · beamforming efficiency · 연산 복잡도 비교, 이론 하한 대비 분석 |

---

## 연구 1. 무선 신호처리 알고리즘

### Model-Driven AI 기반 채널추정 — IEEE WCL 2025 (제2저자)

UAV-RIS 환경의 gridless 채널추정을 위해 atomic norm minimization의 ADMM 반복을 신경망 layer로 전개했습니다. spectral shift 연산으로 확장성을 확보하고, learnable fixed-point iteration으로 layer 수를 수렴 상황에 맞춰 조절하여 낮은 pilot overhead에서 추정 성능과 연산 구조를 함께 개선했습니다.

> J. Jeon, **J. Kwon**, J. Jung, J. Song, and S. Noh, *IEEE Wireless Communications Letters*, vol. 14, no. 11, pp. 3410–3414, Nov. 2025. [DOI](https://doi.org/10.1109/LWC.2025.3592730)

### EM 기반 위상잡음 보상 — IEEE TVT (공동 제1저자)

OFDM 위상잡음 추정과 데이터 복호를 번갈아 수행하는 EM 반복 구조에서, E-step을 신경망 posterior inference로 대체했습니다. 신호처리 모델이 주는 구조적 해석 가능성과 학습 기반 보정 능력을 함께 활용해 단일 기법 대비 추정 성능을 높였습니다.

### LEO NTN 다중위성 One-Shot 획득 — IEEE TWC 심사 중 (공동 제1저자)

저궤도 위성 링크에서 광대역 배열의 beam squint는 통상 보상 대상으로 다룄지지만, rainbow beamforming은 이를 주파수–각도 매핑 자원으로 전환해 단일 아날로그 설정으로 궤도면의 다중 위성을 한 번에 획득합니다 [Park *et al.*, IEEE TVT 2026]. 본 연구는 이 획득 구조를 실제 단말에서 성립하는 배열–궤도 오정렬 기하로 확장합니다.

> 심사 중인 논문으로 상세 내용과 코드는 공개하지 않습니다. 제목과 저자 기여만 표기합니다.

### ISAC 빔포머 최적화 — 진행 중

통합 센싱·통신 환경에서의 빔포머 최적화를 진행하고 있습니다.

---

## 연구 2. 다중센서 상태추정

### UAV Multi-Sensor Localization — ICTC 2025

위치와 속도로 구성된 6차원 상태벡터에 constant-velocity 상태천이 모델을 두고, Camera 방향정보와 IMU 속도정보를 결합한 비선형 관측모델에 대해 EKF prediction/update를 구성했습니다. 시뮬레이터에서 산출한 process/measurement covariance를 추정과 성능평가에 그대로 연결했습니다.

노이즈 측정값 대비 **속도축 RMSE 63–72%, azimuth/elevation RMSE 91%/95% 감소**를 확인했습니다.

### FMCW Radar Signal Processing Simulator

77 GHz FMCW waveform과 beat/Doppler 신호, 거리 감쇠, RCS, 위상배열 안테나를 모델링하고 range–velocity–angle 추정 경로를 구성했습니다. FFT · MUSIC · compressed sensing 계열 알고리즘의 분해능과 추정오차를 안테나 수와 SNR 조건별로 비교했습니다.

### DDPM 기반 MIMO 채널추정 — ICTC 2024 (제1저자)

MIMO 채널의 covariance와 angular spread를 모델링하고 복소 채널에 대한 diffusion forward/reverse process를 구성해, 특정 학습 SNR에 종속되지 않는 채널 정제 구조를 설계했습니다.

---

## 연구 3. 실시간 시스템 통합

### Unity–ROS 2–Python UAV Sensor-Frame Integration

Unity 6의 UAV Camera image와 noisy pose를 하나의 SensorFrame으로 묶어 ROS 2를 거칠 전달하고, Python의 YOLO 검출과 좌표변환 결과를 같은 source sequence로 Unity에 반환하는 online 경로를 구현했습니다. 파일 후처리 기반이던 기존 연구 파이프라인을 실시간 경로로 옮긴 작업입니다.

**검증한 데이터 흐름**

```text
Unity SensorFrame(N)
→ ROS-TCP Connector → ROS 2 DDS → WSL ROS 2 adapter
→ Windows Conda persistent YOLO worker
→ pixel-to-bearing / quaternion geometry
→ BeamDirectionEstimate(source_sequence = N)
→ Unity sequence match → lockstep 해제
```

- WSL ROS 2 node와 Windows Conda YOLO runtime의 process boundary 분리
- `source_sequence` 일치 검사, stale 결과 거부, wall-clock timeout, simulation pause·복원
- 실제 YOLO 경로 단일 smoke run에서 `STATUS_OK` 3회와 마지막 publish/accept sequence 일치 확인

**직접 기여** — Unity 시나리오·센서 데이터 생성, YOLO 학습·추론, 좌표변환, 신경망 sensor fusion, 성능평가·논문 작성, ROS 2 message/bridge와 heterogeneous runtime 통합

**후속 범위** — live FNN·CNN-LSTM 통합, Camera–IMU MSCKF, 반복 latency/drop p50·p95 측정, 제어명령 적용

[프로젝트 상세](PROJECTS.md) · [저장소](https://github.com/jinhokwon9910/uav-multisensor-real-time-framework)

---

## 기술 스택

| 구분 | 기술 |
|---|---|
| Languages | Python, C#, MATLAB, C/C++ |
| Signal Processing | MIMO, Beamforming, ISAC, NTN, FMCW Radar, MUSIC, ESPRIT, OMP, ANM, ADMM, EM |
| Estimation & Fusion | EKF, MSCKF(구현 중), FNN, CNN-LSTM |
| AI | PyTorch, TensorFlow, Ultralytics YOLO, Deep Unfolding, Fixed-Point Network, DDPM |
| System & Robotics | Unity 6, ROS 2, WSL2, Git |

---

## 개발 관점

알고리즘의 단일 정확도보다 입출력 정의, 좌표계 일관성, timestamp 동기화, 지연시간, 실패 조건과 재현성까지 함께 설계하는 것을 중요하게 생각합니다. 논문에서 성능을 보인 알고리즘이 실제 시스템의 시간축 위에서도 같은 성능을 내는지가 제 연구의 기준입니다.

---

## Summary in English

Wireless signal processing engineer working across the full loop from multi-sensor observation to estimation to beam and link decision. Published in IEEE Wireless Communications Letters (2025) and IEEE Transactions on Vehicular Technology (co-first author), with a co-first-authored manuscript under review at IEEE Transactions on Wireless Communications on one-shot multi-satellite acquisition in LEO non-terrestrial networks, and ongoing work on ISAC beamformer optimization. Research spans gridless channel estimation via deep unfolding, phase noise compensation, multi-sensor state estimation with EKF, and real-time Unity–ROS 2–Python integration.

---

## 연락

- Email: jino101999@gmail.com
- Google Scholar: *(링크 추가 예정)*
- ORCID: *(링크 추가 예정)*
