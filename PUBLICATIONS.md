# 논문 · 특허 · 수상

[← 프로필로 돌아가기](README.md)

> 최종 갱신: 2026-08-31
>
> **†** 는 공동 제1저자를 나타냅니다.

---

## 국제 저널

**[J1]** J. Jeon, **J. Kwon**, J. Jung, J. Song, and S. Noh, “[Deep Alternating Direction Networks for UAV-RIS-Assisted Channel Estimation](https://doi.org/10.1109/LWC.2025.3592730),” *IEEE Wireless Communications Letters*, vol. 14, no. 11, pp. 3410–3414, Nov. 2025. — **제2저자**

> UAV-RIS 환경의 gridless 채널추정을 위해 atomic norm minimization의 ADMM 반복을 신경망으로 전개하고(DADU-Net), learnable fixed-point iteration으로 확장했습니다(DADF-Net).

**[J2]** J. Jeon†, **J. Kwon†**, J. Jung, J. Lee, and S. Noh, “[Joint Phase Noise Estimation and Data Decoding with Expectation-Maximization-Based Fixed-Point Network](https://ieeexplore.ieee.org/abstract/document/11657521),” *IEEE Transactions on Vehicular Technology*, Early Access, Aug. 2026, doi: 10.1109/TVT.2026.3724612. — **공동 제1저자**

> OFDM 위상잡음 추정과 데이터 복호를 번갈아 수행하는 EM 반복 구조에서 E-step을 신경망 posterior inference로 대체하여, 단일 기법 대비 추정 성능을 개선했습니다.
> 공동저자로써, 신경망 기반 구조 및 데이터 복호 구조를 담당하였으며, 선행 data-driven(AI) 기법들과의 비교분석을 통해 연구에 기여하였습니다.

**[J3]** J. Jung†, **J. Kwon†**, Q. Li, and S. Noh, “Rainbow Beamforming under Array–Orbit Misalignment: One-Shot Multi-Satellite Acquisition in LEO Non-Terrestrial Networks,” *IEEE Transactions on Wireless Communications*. — **공동 제1저자 · 심사 중**

> 게재된 rainbow beamforming 기반 one-shot satellite acquisition 연구 [R1]을 실제 단말의 array–orbit misalignment 조건으로 확장했습니다. 심사 중인 연구이므로 제목과 연구 관계만 공개하며, 세부 방법·수식·수치결과와 코드는 공개하지 않습니다.

**[R1]** J. Park, I. P. Roberts, and W. Shin, “[Beyond Beam Sweeping: One-Shot Satellite Acquisition With Doppler-Aware Rainbow Beamforming](https://doi.org/10.1109/TVT.2026.3675366),” *IEEE Transactions on Vehicular Technology*, 2026. *(J3의 출발점이 된 게재 선행연구)*

---

## 국제학회 발표 예정

**[C1]** J. Jung†, **J. Kwon†**, J. Kim, S. Park, E. Cha, and S. Noh, “Slope-Rescaled Rainbow Beamforming for One-Shot LEO Satellite Acquisition on Off-Plane Passes,” *IEEE GLOBECOM 2026*. — **공동 제1저자 · 발표 예정**

> Off-plane LEO pass 환경의 one-shot satellite acquisition을 위한 slope-rescaled rainbow beamforming 연구입니다. 현재는 제목과 연구 범위만 공개하며, 세부 방법·수식·수치결과와 코드 및 원고 PDF는 공개하지 않습니다.

---

## 제출 준비 중인 연구

**[W1]** **J. Kwon**, J. Jung, and S. Noh, “ISAC Tx/Rx Hybrid Beamformer Optimization.” — **제1저자** · **2026 제출 예정**

> 통합 센싱·통신 환경에서 sensing과 communication 성능을 함께 고려하는 송수신 hybrid beamformer 공동 최적화 연구입니다.

---

## 국제학회 논문 · IEEE Xplore 게재

1. **J. Kwon**, J. Jung, J. Jeon, and S. Noh, “[A Multi-Modal Simulator for Aerial Communication with Applications to Beam Search](https://ieeexplore.ieee.org/abstract/document/11388995),” *2025 16th International Conference on Information and Communication Technology Convergence (ICTC)*, Jeju, Korea, Oct. 2025, pp. 524–525, doi: 10.1109/ICTC66702.2025.11388995. — **제1저자**

>  Unity6기반의 드론-기지국 시뮬레이터를 구축하고, Jittering 및 노이즈 센서 환경에서 카메라 기반 방향추정을 시변 3D-coordinats상에서 수행하였습니다. AI기반의 refinement를 통해 state의 비선형 오차(서로다른 Axis간의 오차발생시 coupling, state추정 오차(속도,가속도등)시 발생하는 비선형 오차)를 보완, 성능을 평가하였습니다.

2. J. Jung, **J. Kwon**, J. Jeon, and S. Noh, “[A Multi-Sensor Simulator for UAV Localization: Kalman Filter-Based Approach](https://ieeexplore.ieee.org/abstract/document/11389103),” *2025 16th International Conference on Information and Communication Technology Convergence (ICTC)*, Jeju, Korea, Oct. 2025, pp. 2095–2096, doi: 10.1109/ICTC66702.2025.11389103. — **제2저자**

>  Unity6기반의 드론-기지국 시뮬레이터 중, 등속-등방향 운동의 드론상황 가정 후, EKF로 localization을 수행하였습니다.

## 국제학회 발표 · recentresult

1. **J. Kwon**, J. Jeon, and S. Noh, “Denoising Diffusion Probabilistic Model for Channel Estimation,” *ICTC 2024 Recent Results*, 2024. — **제1저자 · 포스터 발표** · [발표 포스터 (PDF)](assets/posters/ictc-2024-ddpm-channel-estimation-poster.pdf)

>  Multi-Input Multi-Ouput 환경의 3GPP fading(NLoS) 채널에서, Diffusion-based 모델 기반의 채널추정을 수행하였습니다. Diffusion 확산과정의 학습을 통해, 기존 supervised AI기반의 '학습데이터에 specific한' 특징을 완화하였습니다.
>  Recent Results 발표는 연구 수행 및 발표 실적으로 포함하되, 정식 proceedings 게재 논문과 구분해 표기합니다.

---

## 국내학회

1. 황석준**†**, **권진호†**, 서경식, 전정원, 노송, “[밀리미터파 대역 지능형 반사 표면 기반 채널 추정 기술 분석](https://www.dbpia.co.kr/journal/articleDetail?nodeId=NODE11227785),” 한국통신학회 동계종합학술발표회, 2023.
2. **권진호**, 전정원, 황석준, 노송, “[통합 센싱 및 통신 시스템 기반 레이더 지원 빔탐색 기법](https://www.dbpia.co.kr/journal/articleDetail?nodeId=NODE11487193),” 한국통신학회 하계종합학술발표회, 2023. — **제1저자 · 학부 우수 논문상**
3. **권진호**, 노송, “[FMCW 레이더 기반 초기 빔포밍 방향 탐색](https://www.dbpia.co.kr/journal/articleDetail?nodeId=NODE11737569),” 한국통신학회 동계종합학술발표회, 2024. — **제1저자 · 학부 우수 논문상**
4. 전정원, **권진호**, 정지혁, 노송, “[비대각 지능형 재구성 반사패턴 및 빔포밍 설계 기술 동향](https://www.dbpia.co.kr/journal/articleDetail?nodeId=NODE11906152),” 한국통신학회 하계종합학술발표회, 2024. — **제2저자**
5. 정지혁, 전정원, **권진호**, 노송, “[지능형 재구성 반사체의 양자화 기법에 따른 성능 분석](https://www.dbpia.co.kr/journal/articleDetail?nodeId=NODE12132365),” 한국통신학회 동계종합학술발표회, 2025. — **제3저자**
6. **권진호**, 전정원, 정지혁, 노송, “[잡음 제거 확산 확률 모델 기반 다중 입력 다중 출력 통신시스템의 채널정제 기법](https://www.dbpia.co.kr/journal/articleDetail?nodeId=NODE12132810),” 한국통신학회 동계종합학술발표회, 2025. — **제1저자**
7. 정지혁, 전정원, **권진호**, 노송, “[비대각 지능형 재구성 반사표면 지원 모노스태틱 통합 센싱 및 통신 시스템의 반사 행렬 최적화 기법 연구 동향](https://www.dbpia.co.kr/journal/articleDetail?nodeId=NODE12360895),” 한국통신학회 하계종합학술발표회, 2025. — **제3저자**

---

## 특허 출원 기여

1. “재구성 가능한 지능형 표면을 통한 통신 경로 환경에서의 채널 추정 방법 및 시스템,” 2024.
2. “심층 고정점 네트워크 기반 지능형 반사 표면체의 방향 탐지 기법,” 2025.
3. “심층 고정점 네트워크 기반 위상 잡음 보상 기법,” 2025.

---

## 연구과제 참여

NRF · KIAT · IITP 연구과제 5건 참여

---

## 수상

- 한국통신학회 학부 논문 경진대회 우수상, 2023.06
- 한국통신학회 학부 논문 경진대회 우수상, 2024.02
- 한국통신학회 아이디어 경진대회 후원기관상(LG U+), 2024.06
- 한국통신학회 아이디어 경진대회 장려상, 2025.02

## 교육 · 기타

- 인천대학교 정보기술대학 디지털논리회로 TA, 2023.09–2023.12 *(단과대학 최우수 TA)*
- 인천대학교 정보기술대학 전자계산기구조 TA, 2024.03–2024.06
- LG Aimers 7기 AI 해커톤 수료, 2025.07–2025.08 (시계열 모델 기반 식료품 매장 매출 예측, LSTM-CNN 기반 방법으로 다중 시계열 데이터 간 correlation 분석하여 성능향상)
- LG Aimers 8기 AI 해커톤 수료, 2026.01–2026.02 (EXAONE 4.0 40% 경량화 수행, linear-layer quantization으로 용량 확보)

