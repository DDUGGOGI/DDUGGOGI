# 첨단 로보틱스 R&D: Physical AI & 휴머노이드
*(English translation follows below)*

이 문서는 강화학습(RL), 모방학습(IL), 휴머노이드 로봇 공학을 포함한 미래 지향적인 선행 연구 프로젝트들을 소개합니다.

## 1. Meta Quest 기반 모방학습 및 합성 데이터 파이프라인 (2025)
> **목표:** 고가의 특수 장비를 소비자용 VR 기기로 대체하여 휴머노이드 학습 데이터 생성을 대중화.

### 혁신 기술
- **비용 절감:** Apple Vision Pro 전용 파이프라인을 **Meta Quest + Unity** 솔루션으로 대체.
- **1인 파이프라인:** 대규모 팀 없이 엔지니어 1명이 대량의 궤적 데이터를 생성할 수 있는 워크플로우 설계.

### 기술 아키텍처
1.  **모션 캡처:** Meta Quest Link (OpenXR)를 통한 사용자 모션 캡처.
2.  **처리:** Unity를 활용해 실시간으로 휴머노이드 스켈레톤에 모션 리타겟팅.
3.  **전송:** ROS2 / WebRTC를 통해 통제 서버로 데이터 전송.
4.  **시뮬레이션:** Isaac Sim에서 수집된 궤적을 기반으로 시각적(Visual) 및 물리적(Physical) 합성 데이터셋 생성.

### 성과
- 휴머노이드/VLA(Vision-Language-Action) 연구 진입 장벽이었던 높은 비용 문제를 해결.
- 모방학습을 위한 데이터 수집 단계를 획기적으로 가속화.

---

## 2. UR10 RL 기반 정밀 파지 (2025)
> **목표:** 기존 역운동학(IK)을 강화학습(RL)으로 대체하여 물리적 제약이 있는 환경에서의 조작 문제 해결.

### 문제점 (Problem)
기존 IK 방식은 흡착 그리퍼의 수직 정렬과 같은 엄격한 방향성 제약 조건과 동적인 물리 상호작용을 처리하는 데 한계가 있음.

### 해결책 (Solution): RL Policy
- **학습:** Isaac Lab 기반의 PPO 강화학습 정책 훈련.
- **제약 조건 처리:** 수직 정렬 유지 및 부드러운 접근 벡터에 명시적인 보상을 부여하여 학습 유도.
- **Sim-to-Real:** 커스텀 추론 노드를 사용하여 학습된 정책을 실제 UR10 로봇에 배포.

### 정량적 성과
- **성공률:** 까다로운 파지 시나리오에서 **20% (IK 기반)** 수준이던 성공률을 **>95% (RL 기반)** 로 향상.

---

## 3. 휴머노이드 RL 환경 구축 – LG CNS (2025)
> **목표:** 기업 R&D를 위한 상용 수준의 강화학습 훈련 환경 구축.

### 주요 과업
- **동역학 튜닝:** 실제 로봇과 동일한 질량, 마찰, 관절 제한 범위 보정.
- **커리큘럼 러닝:** 서기(Standing) → 균형 잡기(Balancing) → 걷기(Walking)로 이어지는 단계별 학습 과정 설계.
- **Sim-to-Real 준비:** 현실 세계의 노이즈에 강건하도록 도메인 랜덤화(Domain Randomization) 적용.

### 사용 기술
- **프레임워크:** Isaac Lab, RL Games, PPO.
- **물리 엔진:** PhysX 5 Articulation.

### 성과
- 미래의 합성 데이터 생성 및 모방학습 연구를 위한 기반 환경 구축 완료.

---
---

# [EN] Advanced Robotics R&D: Physical AI & Humanoids

This document highlights forward-looking projects involving Reinforcement Learning (RL), Imitation Learning (IL), and Humanoid Robotics.

## 1. Meta Quest–based Imitation Learning & Synthetic Data Pipeline (2025)
> **Goal:** Democratize humanoid training data generation by replacing expensive equipment with consumer VR gear.

### Innovation
- **Cost Reduction:** Replaced Apple Vision Pro-exclusive pipelines with a **Meta Quest + Unity** solution.
- **Single-Engineer Pipeline:** Designed a workflow where one engineer can generate massive amounts of trajectory data without a dedicated team.

### Technical Architecture
1.  **Motion Capture:** Meta Quest Link (OpenXR) captures human motion.
2.  **Processing:** Unity retargets motion to a humanoid skeleton in real-time.
3.  **Transport:** Data sent via ROS2 / WebRTC to the control server.
4.  **Simulation:** Isaac Sim generates synthetic datasets (visual + physical) based on these trajectories.

### Impact
- Removed the cost barrier for enterprise clients wanting to start Humanoid/VLA (Vision-Language-Action) research.
- Significantly accelerated the data collection phase for Imitation Learning.

---

## 2. UR10 RL-based Precision Grasping (2025)
> **Goal:** Replace traditional Inverse Kinematics (IK) with Reinforcement Learning to solve physics-constrained manipulation.

### The Problem
Traditional IK struggles with strict orientation constraints (e.g., suction grippers must be perfectly vertical) and dynamic physics interactions.

### The Solution: RL Policy
- **Training:** PPO-based RL policy trained in Isaac Lab.
- **Constraint Handling:** Explicitly rewarded the policy for maintaining vertical alignment and smooth approach vectors.
- **Sim-to-Real:** Deployed the trained policy to a real UR10 robot using a custom inference node.

### Quantitative Result
- **Success Rate:** Improved from **20% (IK-based)** to **>95% (RL-based)** in challenging grasp scenarios.

---

## 3. Humanoid RL Environment – LG CNS (2025)
> **Goal:** Build a production-ready RL training environment for enterprise R&D.

### Key Tasks
- **Dynamics Tuning:** Calibrated mass, friction, and joint limits to match the physical robot.
- **Curriculum Learning:** Designed a step-by-step learning process (Standing → Balancing → Walking).
- **Sim-to-Real Prep:** Implemented domain randomization to make the policy robust against real-world noise.

### Technologies
- **Framework:** Isaac Lab, RL Games, PPO.
- **Physics:** PhysX 5 Articulation.

### Impact
- Established a foundational environment for future Synthetic Data and IL research for the client.
