# 핵심 엔지니어링 도전과제 및 아키텍처 심층 분석
*(English translation follows below)*

이 문서는 개발 과정에서 직면하고 해결한 구체적인 기술적 난제들과 이를 극복하기 위한 아키텍처 설계를 상세히 다룹니다.

## 1. AMR의 IMU Drift 해결
### 도전 과제 (The Challenge)
저가형 IMU는 시간이 지남에 따라 오차(Drift)가 누적되어 로봇의 추정 방향(Heading)이 실제와 달라지는 현상이 발생했습니다. 이는 장시간 운용 시 내비게이션 실패로 이어졌습니다.

### 분석 (The Analysis)
- 산업 현장의 신뢰성을 확보하기 위해서는 단순한 IMU + 휠 오도메트리 통합만으로는 충분하지 않음.
- 외부의 절대적인 기준점(Ground Truth) 없이는 누적되는 오차를 보정할 수 없음.

### 해결책 (The Solution): Vision-Aided Reset
- **아키텍처 변경:** IMU를 "보조 센서" 역할로 격하.
- **새로운 파이프라인:** 바닥의 라인이나 마커를 인식하는 비전 시스템 도입.
- **로직:** 시각적 특징(Visual Feature)이 확인될 때마다, 방향 추정값을 시각적 진실값으로 "강제 초기화(Hard-reset)"하여 누적된 IMU 오 차를 소거.

### 결과
- 장기적인 드리프트 문제 제거.
- 수동 재보정 없이 무기한 연속 운용 가능.

---

## 2. Jetson 엣지 대역폭 한계 극복
### 도전 과제 (The Challenge)
Jetson Xavier 모듈 하나에서 다중 카메라 스트림, LiDAR 데이터, SLAM, 모터 제어를 동시에 처리하다 보니 과부하가 발생했습니다. 프레임 드랍이 발생하고, 이는 제어 루프의 불안정성으로 이어졌습니다.

### 분석 (The Analysis)
- 모든 기능을 하나의 Jetson에서 처리하는 모놀리식(Monolithic) 구조는 확장성이 없음.
- 대역폭을 많이 차지하는 작업(Vision AI)이 실시간성이 중요한 작업(모터 제어)의 자원을 잠식하고 있었음.

### 해결책 (The Solution): 아키텍처 분리 (Decoupled Architecture)
- **관심사의 분리:** 무거운 이미지 처리(YOLO/사람 인식)를 별도의 추론 모듈/보드로 이관.
- **Jetson의 역할:** Jetson은 상위 경로 계획(Path Planning), 센서 퓨전, WES 통신에만 집중하도록 역할 축소.
- **프로토콜:** 모듈 간 ROS2/TCP를 이용한 효율적인 통신 체계 구축.

### 결과
- 제어 루프 주파수의 안정화.
- 향후 모든 프로젝트의 표준이 되는 확장 가능한 아키텍처 확립.

---

## 3. Real-to-Sim 제어 로직 불일치 해결
### 도전 과제 (The Challenge)
실제 제어 로직을 시뮬레이션(Omniverse)으로 옮길 때 문제가 발생했습니다:
- **현실:** 산업용 모터는 "S-커브" 속도 프로파일(서서히 가속 -> 고속 주행 -> 서서히 감속)을 따름.
- **시뮬레이션:** 일반적인 물리 엔진은 목표 지점으로 즉시 이동하려는 단순 PD(비례-미분) 제어기를 주로 사용.
- **결과:** 시뮬레이션 움직임이 뚝뚝 끊기거나 너무 기계적으로 보여, 실제 공정 사이클 타임을 예측하는 데 실패.

### 해결책 (The Solution): 가상 MCU ("Virtual MCU")
- 시뮬레이션 루프 내부에 순수 소프트웨어 기반의 **S-커브 생성기**를 구현.
- 이 "가상 MCU"는 로봇이 실제 기계라면 매 밀리초마다 어디에 있어야 하는지를 계산하고, 물리 엔진이 **그 궤적을 강제로 따르도록** 명령.

### 결과
- **99% 사이클 타임 정확도:** 시뮬레이션 처리량이 실제 공장 처리량과 거의 완벽하게 일치.

---

## 4. RL Ground Truth 검증 ("도대체 왜 실패하는가?")
### 도전 과제 (The Challenge)
심층 강화학습(RL) 정책은 "블랙박스"와 같습니다. 로봇이 물체를 잡는 데 실패했을 때, 원인을 알기가 어렵습니다. 잘못된 관측 때문인지, 네트워크 지연인지, 물리 엔진의 버그인지 파악이 불가능했습니다.

### 해결책 (The Solution): 단계별 검증 프레임워크 (Step-by-Step Validation)
- 모든 단계를 기록하는 로깅 프레임워크 구축:
    1. **관측(Observation):** 로봇이 무엇을 "보았는가"?
    2. **행동(Action):** 신경망이 어떤 명령을 내렸는가?
    3. **실행(Execution):** 관절이 실제로 그 위치로 이동했는가?
- 이 로그를 훈련 환경(Isaac Lab)과 배포 환경(ROS2) 간에 1:1로 비교.

### 결과
- **버그 감소:** 배포 단계에서 발생하는 버그를 **90%** 이상 감소.
- **원인 규명:** Python(학습)과 C++(추론) 사이의 미세한 부동소수점 정밀도 차이로 인한 수치적 불일치를 발견 (이 도구 없이는 발견 불가능했을 문제).

---
---

# [EN] Key Engineering Challenges & Architecture Deep Dive

This document details specific technical hurdles overcome during development, showcasing problem-solving skills and architectural leadership.

## 1. Solving the IMU Drift in AMRs
### The Challenge
Low-cost IMUs suffer from drift over time, causing the robot's estimated heading to diverge from reality. This led to navigation failures in long-duration operations.

### The Analysis
- Relying purely on IMU+Wheel Odometry integration is insufficient for industrial reliability.
- The drift accumulates and cannot be corrected without an external reference ground truth.

### The Solution: Vision-Aided Reset
- **Architecture Shift:** Downgraded IMU to a "supporting sensor" role.
- **New Pipeline:** Implemented a vision system (camera) that detects floor lines/markers.
- **Logic:** Whenever a visual feature is confirmed, the heading estimate is "hard-reset" to the visual truth, clearing accumulated IMU error.

### Result
- Eliminated long-term drift issues.
- Robot could operate indefinitely without manual recalibration.

---

## 2. Overcoming Jetson Edge Bandwidth Limitations
### The Challenge
The Jetson Xavier module became overloaded when processing multiple camera streams + LiDAR data + SLAM + Motor Control simultaneously. Frame rates dropped, causing control loop instability.

### The Analysis
- Monolithic architecture (everything running on one Jetson) is not scalable.
- High-bandwidth tasks (Vision AI) were starving critical real-time tasks (Motor Control).

### The Solution: Decoupled Architecture
- **Separation of Concerns:** Moved heavy image processing (YOLO/People Detection) to a dedicated separate inference module/board.
- **Jetson's Role:** Focused the Jetson strictly on high-level path planning, sensor fusion, and WES communication.
- **Protocol:** Established efficient inter-module communication using ROS2/TCP.

### Result
- Stable control loop frequencies.
- Scalable architecture that became the standard for future projects.

---

## 3. Real-to-Sim Control Logic Mismatch
### The Challenge
When moving a Real-world controller logic into Simulation (Omniverse):
- **Real World:** Industrial motors follow "S-curve" velocity profiles (slow start -> fast move -> slow stop).
- **Simulation:** Standard physics engines often use simple PD (Proportional-Derivative) controllers that snap instantly to targets.
- **Result:** The simulation looked "robotic" and jerky, failing to predict real-world cycle times.

### The Solution: The "Virtual MCU"
- Implemented a purely software-based **S-curve generator** inside the simulation loop.
- This "Virtual MCU" calculates exactly where the robot *should* be at every millisecond if it were a real machine, and forces the physics engine to follow *that* trajectory.

### Result
- **99% Cycle Time Accuracy:** The simulation throughput matched the real factory throughput almost perfectly.

---

## 4. Validating Ground Truth for RL (The "Why is it failing?" Problem)
### The Challenge
Deep Reinforcement Learning (RL) policies are "black boxes." When a robot fails to grasp an object, it's hard to know *why*. Was it a bad observation? A network delay? A physics bug?

### The Solution: Step-by-Step Validation Framework
- Built a logging framework that records every single step:
    1. **Observation:** What did the robot "see"?
    2. **Action:** What command did the neural network output?
    3. **Execution:** Did the joint *actually* move there?
- Compared these logs between the Training Environment (Isaac Lab) and the Deployment Environment (ROS2).

### Result
- **Bug Reduction:** Reduced deployment bugs by **90%**.
- **Found the Root Cause:** Discovered a numerical inconsistency (floating point precision) between Python (Training) and C++ (Inference), which would have been impossible to find without this tool.
