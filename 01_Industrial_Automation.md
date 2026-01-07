# 산업 자동화 및 디지털 트윈 상용화
*(English translation follows below)*

이 문서는 실제 산업 현장에 배치되어 시스템의 안정성과 비즈니스 가치를 입증한 프로젝트들에 초점을 맞춥니다.

## 1. 풀무원 물류 AMR MK3 개발 (2022–2024)
> **목표:** 실제 가동 중인 물류 센터에 자율 주행 모바일 로봇(AMR) 개발 및 배치.

### 시스템 개요
- **배치:** 실제 물류 환경에서 3대의 AMR 운용.
- **통합:** WES(물류 창고 통합 관리 시스템)와 연동하여 작업 할당 자동화.
- **하드웨어:** Jetson 기반 상위 제어기 + 하위 모터 드라이버 통합.

### 핵심 엔지니어링 도전과제 및 해결책
*   **안전성 및 안정성:** 다중 LiDAR와 비상 정지 프로토콜을 활용한 엄격한 안전 레이어를 구현하여 작업자와 공존 가능한 주행 환경 구축.
*   **센서 퓨전:** LiDAR, 카메라, IMU, BMS CAN 데이터를 통합하여 강건한 인식 성능 확보.
*   **화물 제어:** 1톤급 모터와 300kg 가반 하중을 고려하여 부드러운 가감속 프로파일을 갖춘 물리 제어 로직 설계.

### 성과
- 시뮬레이션에서 현장 적용(Sim-to-Field)으로의 전환 성공.
- 실제 센터 내에서 신뢰할 수 있는 자동화 물류 흐름 구축.

---

## 2. 미니로더 디지털 트윈 (Real-to-Sim) – 풀무원 (2024)
> **목표:** 가상 시운전(Virtual Commissioning)을 위한 실제 미니로더의 1:1 디지털 트윈 구축.

### 시스템 개요
- **플랫폼:** NVIDIA Omniverse Isaac Sim.
- **범위:** 물리 장비의 기구학 및 제어 프로파일 완벽 복제.

### 핵심 엔지니어링 도전과제 및 해결책
*   **물리적 불일치 해결:** Isaac Sim의 PD 제어기와 산업용 S-커브 모션 프로파일 간의 근본적인 차이를 해결. 실제 PLC 제어 장비처럼 동작하도록 강제하는 **"Controller Emulation"** 레이어 구현.
*   **흐름 검증:** 입고 → 적재 → 출고의 전체 사이클을 가상 공간에서 재현.

### 성과
- 물리적 장비 설치 전 WES 연동 및 제어 로직 사전 검증 완료.
- 디지털 트윈을 통한 로직 사전 검증으로 현장 디버깅 시간 단축.

---

## 3. 디지털 트윈 컨베이어 제어 시스템 (2024)
> **목표:** 컨베이어 벨트, 미니로더, AMR이 통합된 대규모 시뮬레이션 구축.

### 시스템 개요
- **범위:** 다중 시스템이 상호작용하는 대규모 설비 시뮬레이션.
- **기술 스택:** Isaac Sim, PhysX 5, Python SDK.

### 핵심 엔지니어링 도전과제 및 해결책
*   **병목 구간 분석:** 물류 적체 패턴 및 타이밍 불일치를 사전에 식별 및 해결.
*   **No-Code 설정:** 비개발자도 코드를 수정하지 않고 창고 레이아웃을 변경할 수 있도록 JSON 기반 월드 생성기 개발.

### 성과
- 하드웨어 설치 전 시스템 처리량(Throughput) 및 로직 효율성 입증.
- 복합 물류 시스템에서의 "Simulation-First" 설계 가치 증명.

---

## 4. 원자력 폐기물 처리 PoC – 미국 에너지부 (DOE) (2023)
> **목표:** 위험 폐기물 처리 과정의 무위험 시뮬레이션.

### 시스템 개요
- **시나리오:** 갠트리 크레인과 AMR의 협업을 통한 위험 물질 이송.
- **기술 스택:** Isaac Sim, PhysX 5 (정밀 충돌 및 흔들림 동역학).

### 성과
- 인명이나 장비 위험 없이 고위험 시나리오 제어 테스트 가능.
- 고위험 시설보안 구역에서의 Omniverse 산업적 적용 가능성 제시.

---
---

# [EN] Industrial Automation & Digital Twin Commercialization

This document focuses on projects deployed in real-world environments, demonstrating the ability to deliver stable, business-critical solutions.

## 1. Logistics AMR MK3 Development – Pulmuone (2022–2024)
> **Goal:** Develop and deploy autonomous mobile robots (AMRs) in a live logistics center.

### System Overview
- **Deployment:** 3 AMRs operating in a real-world logistics environment.
- **Integration:** Full integration with WES (Warehouse Execution System) for task assignment.
- **Hardware:** Jetson-based high-level controller + low-level motor drivers.

### Key Engineering Challenges & Solutions
*   **Safety & Stability:** Implemented rigorous safety layers using multiple LiDARs and emergency stop protocols to ensure safe operation alongside human workers.
*   **Sensor Fusion:** Integrated LiDAR, Cameras, IMU, and BMS CAN sensor stack for robust perception.
*   **Payload Control:** Engineered physical control logic to handle 1-ton motors and 300kg payloads with smooth acceleration/deceleration profiles.

### Impact
- Successfully transitioned from simulation to field operation (Sim-to-Field).
- Established a reliable automated logistics flow in a working center.

---

## 2. Mini-loader Digital Twin (Real-to-Sim) – Pulmuone (2024)
> **Goal:** Create a 1:1 Digital Twin of a real mini-loader for Virtual Commissioning.

### System Overview
- **Platform:** NVIDIA Omniverse Isaac Sim.
- **Scope:** Complete kinematic and control profile replication of the physical machine.

### Key Engineering Challenges & Solutions
*   **Physics Mismatch Resolution:** Solved the fundamental difference between Isaac Sim's PD controllers and the industrial S-curve motion profiles. Implemented a **"Controller Emulation"** layer to force the simulation to behave like the real PLC-controlled hardware.
*   **Flow Validation:** Reproduced the entire Inbound → Staging → Outbound cycle virtually.

### Impact
- Validated WES integration and logic before any physical deployment.
- Reduced on-site debugging time by pre-verifying control logic in the digital twin.

---

## 3. Digital Twin Conveyor Control System (2024)
> **Goal:** Unified simulation integrating conveyor belts, mini-loaders, and AMRs.

### System Overview
- **Scope:** Large-scale facility simulation involving multiple interacting systems.
- **Tech Stack:** Isaac Sim, PhysX 5, Python SDK.

### Key Engineering Challenges & Solutions
*   **Bottleneck Analysis:** Identified accumulation patterns and timing mismatches in advance.
*   **No-Code Configuration:** Developed a JSON-driven world generator, allowing non-engineers to modify the warehouse layout without touching code.

### Impact
- Proved system throughput and logic efficiency before hardware installation.
- Demonstrated the value of "Simulation-First" design in complex logistics.

---

## 4. Nuclear Waste Handling PoC – U.S. DOE (2023)
> **Goal:** Risk-free simulation of hazardous waste handling.

### System Overview
- **Scenario:** Cooperation between a gantry crane and an AMR for moving hazardous materials.
- **Tech Stack:** Isaac Sim with PhysX 5 for accurate collision and sway dynamics.

### Impact
- Enabled testing of high-risk scenarios without endangering personnel or equipment.
- Showcased the industrial applicability of Omniverse in critical safety sectors.
