# 디지털 트윈 개발 전략

> **Physical AI: 실제 로봇의 완벽한 가상 복제와 학습 생태계 구축**

## 📋 개요

이 문서는 POLLUX에서 3년간(2022-2025) 휴머노이드 로봇과 물류 자동화 시스템을 개발하면서 구축한 **디지털 트윈 개발 전략**을 분석합니다. NVIDIA Omniverse와 Isaac Sim 플랫폼을 핵심 기반으로 하여, 물리적 실체를 가상 공간에 정밀하게 구현하고 이를 통해 AI를 학습시키는 구체적인 방법론을 담고 있습니다.

---

## 🎯 전략 1: 계층적 디지털 트윈 아키텍처 (Omniverse Tech Stack)

### 설계 철학
물리적 로봇과 가상 시뮬레이션, 그리고 지능형 AI가 유기적으로 연결되는 **3-Layer Architecture**를 구축합니다.

### Layer 1: Physical Layer (물리 계층)
실제 현장에서 작동하는 로봇과 환경입니다.
- **Robot Hardware**: NVIDIA Jetson 모듈이 탑재된 AMR 및 휴머노이드.
- **Real Sensors**: LiDAR, Camera, IMU 등 물리 센서 네트워크.
- **Actuators**: 모터 드라이버 및 실제 구동부.

### Layer 2: Virtual Layer (가상 계층 - Omniverse/Isaac Sim)
NVIDIA Omniverse 플랫폼 위에 구축된 정밀한 디지털 복제본입니다.
- **USD (Universal Scene Description)**: 로봇, 센서, 환경 등 모든 자산을 USD 포맷으로 표준화하여 관리합니다.
- **PhysX 5**: 질량, 마찰, 탄성 등 물리 법칙을 리얼타임으로 연산하여 현실과 동일한 역학 관계를 구현합니다.
- **Virtual Testbed**: 실제 물류 창고나 실험실 환경을 3D 스캔 데이터 기반으로 1:1 모델링합니다.

### Layer 3: Intelligence Layer (지능 계층 - Isaac Lab)
가상 환경에서 생성된 데이터를 기반으로 학습하고 추론하는 두뇌입니다.
- **Reinforcement Learning (RL)**: Isaac Lab(구 Orbit)을 활용하여 수천 개의 병렬 환경에서 로봇 정책을 학습시킵니다.
- **Imitation Learning**: VR 등을 통해 수집된 인간의 데모 데이터를 학습합니다.
- **Sim-to-Real Policy**: 학습된 신경망 모델을 실제 로봇 제어기에 배포합니다.

---

## 🎯 전략 2: Sim-to-Real Pipeline (NVIDIA Isaac Sim Features)

### 핵심 문제: Reality Gap
시뮬레이션과 현실 사이의 미세한 차이(마찰력, 센서 노이즈, 조명 등)로 인해 가상에서 잘 동작하던 AI가 현실에서 실패하는 문제를 해결합니다.

### 2.1 Domain Randomization (도메인 랜덤화)
Isaac Sim의 **Domain Randomization** 기능을 활용하여 불확실성에 강한 AI를 만듭니다.
- **Visual Randomization**: 조명 밝기, 색상, 텍스처, 카메라 위치 등을 무작위로 변경하여 시각적 변화에 강건하게 만듭니다.
- **Physics Randomization**: 바닥의 마찰 계수, 로봇 링크의 질량, 모터의 댐핑 값을 튜닝 범위 내에서 무작위로 변동시켜 물리적 오차를 극복합니다.

### 2.2 Real Data Injection (하이브리드 데이터 학습)
순수 시뮬레이션 데이터만으로는 부족한 부분을 실제 데이터로 보완합니다.
- **Log Replay**: 실제 로봇이 주행하며 수집한 ROS bag 데이터를 Isaac Sim 내에서 재생(Replay)하여 시뮬레이션의 정확도를 검증합니다.
- **Hybrid Dataset**: 시뮬레이션에서 생성한 수만 건의 합성 데이터와, 실제 현장에서 수집한 고품질 데이터를 혼합하여 학습 효율과 정확도를 동시에 잡습니다.

---

## 🎯 전략 3: 인간 행동 디지털화 (Human-in-the-Loop)

### 3.1 VR Motion Capture & Retargeting
고가의 모션 캡처 장비 대신 상용 VR 기기를 활용하여 인간의 유연한 움직임을 데이터화합니다.
- **OpenXR to Omniverse**: Meta Quest 등 VR 기기의 6-DOF 트래킹 데이터를 Omniverse로 실시간 스트리밍합니다.
- **Online Retargeting**: 인간의 골격 구조를 로봇의 USD Skel(스켈레톤) 구조에 실시간으로 매핑(Mapping)합니다. 이 과정에서 관절 한계(Joint Limits)와 자가 충돌(Self-Collision)을 실시간으로 보정합니다.

### 3.2 Teleoperation (원격 제어)
- **Zero-Latency Control**: WebRTC 및 ROS2 Bridge를 통해 엔지니어가 가상 공간의 로봇을 1인칭 시점에서 직접 조조종하며 고난이도 작업(Edge Case) 데이터를 생성합니다.

---

## 🎯 전략 4: 고신뢰 물리 시뮬레이션 (High-Fidelity Physics)

### 4.1 Kinematic Fidelity (기구학적 정밀도)
로봇의 관절 구조와 움직임을 USD Articulation으로 완벽히 정의합니다.
- CAD 모델을 USD로 변환할 때, 모든 링크의 부모-자식 관계와 관절 타입(Revolute, Prismatic)을 실제 도면과 일치시킵니다.

### 4.2 Dynamic Fidelity (동역학적 정밀도)
PhysX 5 물리 엔진을 통해 보이지 않는 힘까지 모사합니다.
- **Inertia Tensor**: 단순 질량이 아닌, 회전 관성 모멘트까지 CAD에서 추출하여 적용합니다.
- **Friction Material**: 바닥 재질(콘크리트, 에폭시 등)에 따른 정지/운동 마찰 계수를 실험 데이터 기반으로 튜닝합니다.

### 4.3 Sensor Fidelity (RTX Sensors)
NVIDIA RTX 렌더링 기술을 활용하여 센서 데이터를 물리적으로 정확하게 생성합니다.
- **RTX Lidar**: 레이저의 빔 패턴, 반사율, 회전 속도, 노이즈 모델까지 실제 센서(예: SOSLAB, Velodyne) 스펙과 동일하게 설정합니다.
- **Isaac Camera**: 렌즈의 왜곡(Distortion), 심도(Depth), 모션 블러(Motion Blur) 효과를 적용하여 실제 카메라와 구분하기 힘든 이미지를 생성합니다.

---

## 🎯 전략 5: 모듈화 및 재사용 (USD Composition)

### 철학: Build Once, Use Everywhere
Omniverse의 USD 레이어링 시스템을 활용하여 재사용성을 극대화합니다.

- **Component-based Design**: 로봇의 바퀴, 센서, 매니퓰레이터 등을 독립된 USD 파일로 관리합니다.
- **Layering & Delta**: 기본 로봇 모델(Base USD)을 건드리지 않고, 특정 프로젝트를 위한 수정 사항(새로운 센서 부착, 파라미터 변경)만을 별도의 레이어(Delta USD)에 저장하여 관리 효율을 높입니다.

---

## 🎯 전략 6: AI 모델 통합 (NVIDIA AI Ecosystem)

### 6.1 Foundation Model 활용 (Project GR00T)
바닥부터 모든 것을 학습시키는 대신, NVIDIA의 로봇 파운데이션 모델을 활용합니다.
- **Fine-tuning**: 일반적인 지능을 가진 파운데이션 모델에 우리 현장의 특수 데이터(특정 물류 프로세스, 부품 조작법)를 추가 학습시켜 빠르게 전문성을 확보합니다.

### 6.2 Cloud Training & Edge Inference
- **Training (DGX/Cloud)**: Isaac Sim에서 생성된 막대한 데이터를 활용해 클라우드 상의 GPU 클러스터에서 대규모 모델을 학습시킵니다.
- **Inference (Jetson/NIM)**: 학습된 모델을 경량화(Quantization)하고 TensorRT로 최적화하여 로봇의 임베디드 컴퓨터(Jetson)에서 실시간으로 실행합니다. NVIDIA NIM(NVIDIA Inference Microservices)을 활용하여 배포 복잡도를 낮춥니다.

---

## 🎯 전략 7: 안전 및 검증 (Safety & Validation)

### 7.1 Virtual Commissioning (가상 시운전)
실제 로봇을 투입하기 전, 가상 환경에서 수천 번의 테스트를 수행합니다.
- 1,000개 이상의 자동화된 테스트 시나리오(장애물 회피, 비상 정지, 통신 두절 등)를 Isaac Sim에서 실행합니다.
- 시뮬레이션 상에서의 충돌이나 실패 사례를 분석하여 로봇 제어 코드를 수정합니다.

### 7.2 Continuous Monitoring
가상 검증을 통과한 정책이라도 실제 현장에서는 안전장치가 필요합니다.
- 실제 로봇에는 AI의 판단과 별개로 작동하는 하드웨어 레벨의 안전 레이어(Safety PLC, 하드웨어 리밋 스위치)를 유지합니다.

---

## 📊 요약: 우리의 경쟁력

이 전략을 통해 우리는 다음과 같은 성과를 달성했습니다.
1.  **개발 속도 혁신**: 하드웨어 제작 전 소프트웨어 검증 완료 (Sim-first Approach).
2.  **데이터 비용 절감**: 값비싼 실제 데이터 수집을 시뮬레이션 합성 데이터로 90% 대체.
3.  **현장 적응력**: Domain Randomization을 통해 다양한 환경에서도 강건한 로봇 시스템 구축.
