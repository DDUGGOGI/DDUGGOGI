# 포괄적 피지컬 AI 및 로보틱스 엔지니어링 포트폴리오

**직무**: Physical AI Engineer / Robotics Specialist  
**전문 분야**: Digital Twin, Humanoid Control, Foundation Models, AMR Deployment, Multimodal AI Infrastructure

---

## 🚀 전문가 요약

저는 **물리적 로보틱스(Physical Robotics)**와 **첨단 AI(Advanced AI)**의 간극을 좁히는 전문 엔지니어입니다.
로봇이 복잡한 현실 환경을 인지하고, 판단하며, 행동할 수 있도록 지원하는 **End-to-End 파이프라인** 구축에 주력하고 있습니다.
**NVIDIA Isaac Ecosystem** (Sim, Lab, Gym)과 **Foundation Models** (GR00T, VLMs)을 활용하여, 자율 물류 시스템부터 정교한 휴머노이드 조작에 이르는 핵심 산업 문제를 해결하는 지능형 디지털 트윈을 구현합니다.

---

## 🛠️ 핵심 기술 역량

| 도메인 | 주요 기술 및 스킬 |
|---|---|
| **Humanoid Robotics** | **NVIDIA GR00T**, Teleoperation (VR-to-Sim), Whole Body Control (WBC), Retargeting (Unity → Isaac) |
| **Mobile Robotics (AMR)** | **ROS 1/2**, SLAM, Navigation Stack, 현장 배포(Deployment), 센서 캘리브레이션 (Lidar/IMU), 관제 시스템 (WCS) |
| **Simulation & Digital Twin** | **Omniverse Isaac Sim**, USD GenAI, 물리 기반 렌더링, Sim-to-Real Transfer |
| **AI & Learning** | **Reinforcement Learning (PPO)**, **Foundation Model Fine-tuning**, VLM (Vision-Language Models), RAG |
| **Infrastructure** | **Docker Containerization**, NVIDIA DGX/L40S 최적화, 마이크로서비스 (FastAPI, WebSockets) |

---

## 🏆 주요 프로젝트

### 1. **휴머노이드 파운데이션 모델 통합 (Project "Titan")**
*범용 로봇 기술(Generalist Robot Technology)을 활용한 휴머노이드 개발의 대중화 이니셔티브.*

*   **목표**: 대규모 파운데이션 모델을 미세 조정(Fine-tuning)하여 휴머노이드 로봇(GR1T2)이 복잡한 조작 작업을 수행하도록 구현.
*   **핵심 기여**:
    *   **Foundation Model Fine-tuning**: 도메인 특화 데이터셋(`PickNPlace`, `CanSort`)을 사용하여 **GR00T-N1-2B** 모델을 커스터마이징. Diffusion Head와 Vision Backbone의 하이퍼파라미터 최적화 수행.
    *   **Inference Architecture**: AI 모델의 16-step 예측(Action Horizon)을 로봇 제어기로 실시간 스트리밍하는 확장 가능한 **Server-Client 추론 시스템** 개발.
    *   **Action Mapping**: 고수준의 AI 액션(7-DoF Arm, 6-DoF Hand)을 특정 하드웨어(GR1T2) 명령으로 변환하는 정교한 조인트 매핑 로직 구현.
    *   **Sim-Integrated Testing**: 물리적 배포 전 모델 예측을 시각화하고 검증하기 위해 Isaac Sim 내부에 **소켓 기반 수신 모듈(Receiver)** 구축.

### 2. **몰입형 원격 제어 및 리타게팅 시스템**
*가상 현실(VR)과 물리적으로 정확한 시뮬레이션을 연결하는 고정밀 원격 제어 인터페이스.*

*   **목표**: 모방 학습(Imitation Learning) 정책 훈련을 위한 고품질 인간 모션 데이터셋 캡처 파이프라인 구축.
*   **핵심 기여**:
    *   **VR-to-Sim Bridge**: Unity와 WebSockets을 활용하여 **Meta Quest와 Isaac Sim**을 실시간 연동.
    *   **Real-time Retargeting**: Unity(왼손 좌표계)와 Isaac(오른손 좌표계) 간의 **좌표 변환 알고리즘** 및 부드러운 모션 전송을 위한 **Quaternion Slerp** 필터링 구현.
    *   **Dexterous Hand Tracking**: VR 컨트롤러의 벡터 연산을 통해 정밀한 손가락 관절 각도를 산출하여 섬세한 조작 기능 구현.

### 3. **산업용 AMR 플릿 현장 배포 (Project "Velocity")**
*물류 센터 내 자율 이동 로봇(AMR) 플릿의 풀스택 개발 및 현장 배포.*

*   **목표**: 창고 환경에서 랙(Rack) 이송 자동화를 위한 AMR(MK3) 플릿을 안정화하고 배포.
*   **핵심 기여**:
    *   **Field Engineering**: 양지 현장 등에서 발생한 **Lidar/IMU 캘리브레이션**, **엔코더 드리프트**, **네트워크 지연** 등 치명적인 하드웨어-소프트웨어 통합 이슈 해결.
    *   **Navigation Logic**: 정밀한 "랙 진입(Rack Entry)" 및 "격자 주행"을 위해 **ROS Navigation Stack** 파라미터 최적화.
    *   **System Stability**: 다수의 로봇에 일관된 배포를 위해 전체 소프트웨어 스택(드라이버, 제어, UI)을 **Docker**로 컨테이너화.
    *   **Legacy Support**: 커스텀 브릿지 노드를 통해 최신 ROS2 Humble 시스템과 레거시 ROS1 컴포넌트 간의 호환성 유지.

### 4. **엔터프라이즈 멀티모달 데이터 파이프라인**
*물리 기반 AI 학습을 위한 대용량 산업용 비디오 데이터 처리 이중 계층 시스템.*

*   **목표**: 비정형 비디오 로그에서 의미론적(Semantic) 및 물리적 메타데이터를 자동 추출.
*   **핵심 기여**:
    *   **LangGraph Orchestration**: **VLM (Vision-Language Model)** 추론과 **OCR** 작업을 조율하는 Directed Cyclic Graph (DCG) 파이프라인 설계.
    *   **Hybrid Architecture**: 경량화된 **Media Engine** (정규화/압축)과 고성능 **Semantic Engine** (NVIDIA Spark/DGX 기반)으로 구성된 2-Tier 아키텍처 구축.
    *   **Optimization**: NVIDIA L40S 서버에서의 추론 처리량 극대화를 위해 **FP8 Quantization** 및 **vLLM** 기술 활용.

---

## 📈 엔지니어링 철학

*   **"Sim-First Development"**: 모든 코드는 실제 하드웨어에 적용하기 전에 고정밀 시뮬레이터(Isaac Sim)에서 검증되어야 한다고 믿습니다. 이는 리스크를 최소화하고 반복 주기(Iteration Cycle)를 가속화합니다.
*   **"Data-Centric AI"**: 피지컬 AI 모델의 성능은 결국 체화된 데이터(Embodiment Data)의 품질에 달려 있습니다. 저는 데이터의 수집, 정제, 증강을 위한 견고한 파이프라인 구축에 집중합니다.
*   **"Full-Stack Robotics"**: 성공적인 로봇 시스템을 위해서는 임베디드 드라이버와 네트워크 프로토콜 같은 로우 레벨부터, 추론 에이전트와 클라우드 인프라 같은 하이 레벨까지 전체 스택에 대한 이해가 필수적입니다.

---
*본 포트폴리오는 개발 워크스페이스 내의 프로젝트 산출물과 기술 문서를 바탕으로 작성되었습니다.*
