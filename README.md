# 권진호 | Jinho Kwon

**UAV System Integration · Model-Driven AI · Wireless Signal Processing**

Unity–ROS 2–Python 기반 UAV 실시간 프레임워크를 구현하고, 반복 신호처리 알고리즘을 deep unfolding 및 fixed-point network로 확장하는 연구를 수행해왔습니다.

`IEEE 저널 2편 게재` · `IEEE 저널 1편 심사 중` · `국제학회 발표 3건(IEEE Xplore 2건 · Recent Results 1건)` · `국내학회 7건(제1저자 4건)` · `특허 3건 출원 기여`

---

## Representative Work

### 1. Unity–ROS 2–Python UAV Real-Time Framework

**ICTC 2025 제1저자 연구의 후속 구현 · Unity 6 · ROS 2 · Python · YOLO**

ICTC 2025에서 발표한 UAV–기지국 다중모달 시뮬레이터와 beam search 연구를 ROS 2 기반 online 양방향 구조로 확장했습니다. Unity의 Camera·UAV state를 하나의 sensor frame으로 전달하고, Python의 YOLO·좌표변환·빔 방향 예측 결과를 같은 source sequence로 Unity에 실시간 반환합니다.

```text
Unity SensorFrame
→ ROS-TCP / ROS 2 DDS
→ Python YOLO · Coordinate Transform · Beam Direction
→ Unity Feedback
```

Sequence 일치 검사, stale 결과 거부, timeout과 simulation state 복원까지 구현하고 실제 Unity–ROS 2–YOLO–Unity 왕복 경로를 검증했습니다.

[Source Code & Evidence](https://github.com/jinhokwon9910/uav-multisensor-real-time-framework)

### 2. Fixed-Point Network 기반 Phase-Noise Compensation

**IEEE Transactions on Vehicular Technology · 공동 제1저자 · Early Access · 특허 1건**

OFDM 위상잡음 추정과 데이터 복호를 반복하는 EM 구조에 neural posterior inference와 fixed-point termination을 결합한 model-driven AI 연구입니다.

[Paper](https://ieeexplore.ieee.org/abstract/document/11657521)

### 3. Deep Unfolding / Fixed-Point Network 기반 UAV-RIS Channel Estimation

**IEEE Wireless Communications Letters · 제2저자 · 게재 · 관련 특허 2건**

Atomic norm minimization의 ADMM 반복을 DADU-Net으로 전개하고, learnable fixed-point iteration을 사용하는 DADF-Net으로 확장해 gridless UAV-RIS 채널추정의 정확도와 확장성을 함께 다뤘습니다.

[Paper](https://doi.org/10.1109/LWC.2025.3592730)

### 4. Rainbow Beamforming under Array–Orbit Misalignment

**IEEE Transactions on Wireless Communications · 공동 제1저자 · 심사 중**

게재된 선행연구가 제시한 LEO NTN one-shot multi-satellite acquisition을 실제 단말의 array–orbit coordinates로 확장한 연구입니다. 심사 중인 연구이므로 제목과 연구 관계만 공개하고, 세부 방법·수식·수치결과와 코드는 공개하지 않습니다.

**Submitted manuscript:** “Rainbow Beamforming under Array–Orbit Misalignment: One-Shot Multi-Satellite Acquisition in LEO Non-Terrestrial Networks”

**Cited prior work:** J. Park, I. P. Roberts, and W. Shin, “[Beyond Beam Sweeping: One-Shot Satellite Acquisition With Doppler-Aware Rainbow Beamforming](https://doi.org/10.1109/TVT.2026.3675366),” *IEEE Transactions on Vehicular Technology*, 2026.

### 5. ISAC Tx/Rx Hybrid Beamformer Optimization

**제1저자 · 제출 준비**

통합 센싱·통신 환경에서 sensing과 communication 성능을 함께 고려하는 송수신 hybrid beamformer 공동 최적화를 연구하고 있습니다.

### 6. DDPM 기반 MIMO Channel Estimation

**ICTC 2024 Recent Results 제1저자 · 포스터 발표 · KICS 2025 제1저자**

복소 MIMO 채널의 통계 구조에 diffusion forward/reverse process를 적용해 특정 학습 SNR에 종속되지 않는 channel denoising 및 estimation 구조를 연구했습니다. ICTC 발표 실적은 정식 proceedings 게재 논문과 구분하였습니다.

---

## Other Research

RIS·채널추정, 레이더 지원 빔탐색, FMCW 기반 초기 빔 방향 탐색, 생성모델 기반 신호처리 등을 주제로 **국내학회 논문 7건**을 발표했습니다. 제1저자 및 공동저자 실적을 포함한 전체 서지정보는 [Publications · Patents · Awards](PUBLICATIONS.md)에 정리합니다.

NRF · KIAT · IITP 연구과제 참여 · 특허 3건 출원 기여

---

## Technical Stack

| Category | Tools & Methods |
|---|---|
| Languages | Python, C#, MATLAB, C/C++ |
| System Integration | Unity 6, ROS 2, ROS-TCP, DDS, WSL2, Git |
| AI | PyTorch, TensorFlow, Ultralytics YOLO, Deep Unfolding, Fixed-Point Network, DDPM |
| Signal Processing | Channel Estimation, Beamforming, ISAC, NTN, FMCW Radar, ANM, ADMM, EM |
| Estimation & Geometry | Sensor Fusion, Coordinate Transform, Quaternion Geometry |

---

## Contact

- Email: jinhokwon9910@gmail.com
- Full record: [Publications · Patents · Awards](PUBLICATIONS.md)

