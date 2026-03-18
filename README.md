**Physical AI**
<img width="2929" height="1316" alt="image" src="https://github.com/user-attachments/assets/0808a35d-1123-422f-a54d-3da9584b8bf5" />

**Executive Summary**
<img width="1888" height="730" alt="image" src="https://github.com/user-attachments/assets/0a616526-154f-42f4-b146-bf120df4fa64" />
산업계는 전 세계의 모든 물리적 요소가 WFM, RFM, AI 에이전트로 구동되는 훈련 가능한 구조로 재편되는 대전환기에 진입하고 있습니다. 저는 NVIDIA Omniverse를 활용하여 실제 산업 현장에 Physical AI를 구현함으로써 이러한 변화의 최전선에 서고자 합니다. AMR, 미니 로더, 컨베이어, 휴머노이드, Digital Twin, RL/IL 파이프라인을 하나의 End-to-End 사이클로 연결한 경험을 통해 실제 제어, 시뮬레이션, AI 학습을 통합하는 엔지니어링에 대한 깊은 이해를 갖추게 되었습니다. 물리 시스템, 시뮬레이션 동작, AI 학습 간의 근본적인 불일치를 반복적으로 식별하고 해결하며, OpenUSD, Isaac Sim/Lab, 합성 데이터, Jetson 배포를 아우르는 확장 가능한 아키텍처를 구축해왔습니다. 국내 주요 기업 및 공공기관과의 협업을 통해 Omniverse 도입 시 직면하는 조직 역학, 의사결정 패턴, PoC→Pilot→Deployment 단계의 병목 현상에 대한 실질적인 이해도 쌓았습니다. 이러한 통찰력을 바탕으로 고객을 기술적으로뿐만 아니라 전략적으로 지원할 수 있습니다. 저는 Physical AI의 복잡한 문제를 창의적으로 해결하는 데 깊은 열정을 가지고 있으며, 산업의 역사적 변혁이 이루어지는 최전선인 NVIDIA KOREA에서 기여하고 싶습니다.

- **[🚀 2025_Comprehensive_Portfolio.md](./02_Comprehensive_Portfolio.md)**: **Physical AI 포트폴리오** (프로젝트 상세 및 기술 스택)
- **[🚀 2026_AMR_RDS.md](./05_AMR_RDS.md)**: **AMR RDS 개발** (프로젝트 구조 및 문제해결 전략)<br />
- **[🚀 2026_Curse of Dimensionality Robotics.md](./06_Curse_of_Dimensionality_Robotics.md)** (프로젝트 구조 및 문제해결 전략)<br />
- **[🚀 2026_Curse of Dimensionality Pick and Place.md](./07_Curse_of_Dimensionality_PickPlace.md)** (프로젝트 구조 및 문제해결 전략)<br />


**SKILL**
Simulation (Omniverse, Isaac Sim, USD, PhysX) · Robotics (ROS2, Jetson, Control) · AI for Robotics (RL/IL, GR00T, Synthetic Data) · Vision (YOLO, TensorRT) · Motion Capture (Meta Quest, Unity) · Logistics Automation (WCS/WMS Integration) · Embedded & System Architecture Design

**WORK EXPERIENCE**<br />
  **POLLUX** (2022.07 - 현재 재직 중)
Digital Twin Engineer - Digital Twin Division
국내 최초로 NVIDIA SAC NPN 파트너십을 획득한 POLLUX의 메인 개발자로서 Omniverse 솔루션을 리딩하고 있습니다. NVIDIA Omniverse를 핵심 도구로 사용하여 물류 시뮬레이션을 연구하고 다수의 B2B 프로젝트를 성공적으로 수행했습니다. 저의 개발 접근 방식은 핵심 물류 자산과 WCS 및 WMS 레이어와의 운영 통합에 중점을 둡니다.

**Meta Quest 기반 모방 학습, 합성 데이터셋 파이프라인 & 휴머노이드 가상 테스트베드 (2025)**
<img width="2283" height="1269" alt="스크린샷 2025-11-26 17-09-58" src="https://github.com/user-attachments/assets/b37e05bf-c690-47f7-8235-df9dd85245d7" />
<img width="1414" height="1291" alt="스크린샷 2025-12-18 16-10-10" src="https://github.com/user-attachments/assets/c02e7bb0-8b1f-4165-9b3a-7ae37bdf9571" />

휴머노이드 IL(Imitation Learning) 학습을 위해 인간 시연 데이터를 수집하고 합성 데이터셋 생성을 가속화하는 프로젝트입니다.<br />
**[주요 업무]**<br />
Meta Quest 모션 캡처 → Unity → 제어 서버 → ROS2 → Isaac Sim 휴머노이드 동작 리타겟팅
모방 학습을 위한 궤적(Trajectory) 데이터셋 생성
GR00T/N1 기반 합성 데이터셋 생성 파이프라인 구축
휴머노이드 조작(Manipulation) 및 보행(Locomotion) 가상 테스트베드 구축<br />
**[사용 기술]**<br />
Motion Capture: Meta Quest Link, OpenXR
Video Processing: Unity Render Streaming, H.264 인코딩/디코딩 (Python)
Networking: WebRTC over ROS2 bridge, 커스텀 UDP/TCP 전송
Middleware: ROS2 Humanoid Action Msg (관절 위치/속도 + 비전 동기화)
Simulation: Isaac Sim 휴머노이드 모션 매핑
Dataset: GR00T/N1 합성 데이터셋 생성기, 궤적 필터링
IL: BC, Trajectory Embedding, Smoothing, Noise Injection
Visualization: Omniverse 모션 리타겟팅
Languages: Python, ROS2, C#, Unity, JSON/Parquet<br />
**[엔지니어링 성과]**<br />
Apple Vision Pro 전용 모방 학습 및 원격 제어 파이프라인을 Meta Quest + Unity로 대체하여 엔터프라이즈 고객의 비용 장벽을 제거했습니다.
단일 엔지니어가 IL/VLA 학습 데이터를 생성할 수 있는 데이터셋 가속 파이프라인을 구축했습니다.
멀티 스택 데이터 흐름(Meta Quest → Unity → ROS2 → Isaac Sim)을 설계하여, 궤적 및 합성 데이터셋 생성을 획기적으로 가속화하는 저비용 대안을 마련했습니다.
이 파이프라인은 휴머노이드 학습의 고질적인 병목이었던 IL 데이터 생성 문제를 크게 해소했습니다.

**UR10 Reach: 물리 제약 기반 조작을 위한 RL 기반 정밀 파지 (2025)**
<img width="1716" height="1158" alt="image" src="https://github.com/user-attachments/assets/f33ff6ac-911f-42ce-8bfb-09e909826f87" />

<img width="839" height="1332" alt="image" src="https://github.com/user-attachments/assets/995df271-3f3e-44dd-b889-629cb2079253" />

Isaac Sim에서 물리적 제약이 있는 흡착 파지(Suction Grasping) 문제를 해결하기 위해 기존의 역운동학(IK) 기반 조작을 강화학습(RL) 정책으로 대체한 프로젝트입니다. 학습된 정책은 흡착 그리퍼에 필요한 정밀한 수직 정렬을 달성하여 엄격한 물리적 제약 하에서도 안정적인 파지를 가능하게 합니다.<br />
**[주요 업무]**<br />
Isaac Lab RL 학습 → Ground Truth 검증 → ROS2 배포 → 실환경 전이(Real-world Transfer)<br />
방향 제약을 포함한 6 자유도 UR10 관절 제어를 위한 PPO 기반 RL 정책 학습<br />
이중 배포 아키텍처: Isaac Lab 자동 매니저 vs ROS2 수동 구현<br />
단계별 관측/행동 비교를 위한 Ground Truth 검증 프레임워크 구축<br />
학습 및 배포를 위한 통합 소켓 기반 명령 인터페이스(send_target.py)<br />
ROS2 TF2 통합을 통한 World-to-Base 좌표 변환<br />
TCP 및 ROS2 이중 통신 채널을 갖춘 프로덕션급 추론 노드<br />
**[사용 기술]**<br />
Reinforcement Learning: Isaac Lab (NVIDIA Omniverse), PPO, RSL-RL (ETH Zurich)<br />
Robot Control: 흡착 그리퍼가 장착된 Universal Robots UR10, ROS2 (Humble), 30Hz 제어 루프<br />
Networking: TCP 소켓 서버 (JSON 프로토콜), ROS2 토픽 Pub/Sub, TF2 Transforms<br />
Middleware: 커스텀 관측 공간 (25D), 정규화된 6D 행동 공간<br />
Simulation: Isaac Sim (PhysX), IsaacArticulationController, UR10 USD 모델<br />
Math & Transforms: 쿼터니언 연산, World↔Base 프레임 변환, EMA 속도 필터링<br />
Dataset: PyTorch 체크포인트 (.pt), Actor–Critic 상태 dict 추출<br />
Visualization: Isaac Lab 시각화 도구, ROS2 RViz 관절 모니터링<br />
Languages: Python, PyTorch, C++, YAML/JSON, ROS2 메시지 정의<br />
**[엔지니어링 성과]**<br />
IK 기반 조작을 RL 정책으로 대체하여, 물리적 제약 하에서 위치와 방향을 명시적으로 최적화함으로써 파지 성공률을 20%에서 95% 이상으로 향상시켰습니다.<br />
Isaac Lab을 기준으로 하는 Ground Truth 검증 프레임워크를 구축하여, 관측, 행동, 관절 명령의 로그를 단계별로 비교함으로써 ROS2 배포 버그를 90% 이상 줄였습니다.<br />
통합 명령 클라이언트를 갖춘 이중 통신 아키텍처(TCP 소켓 + ROS2 토픽)를 설계하여, 코드 중복 없이 학습 환경과 배포 환경 간의 원활한 A/B 테스트를 가능하게 했습니다.<br />
ROS2 배포를 위해 Isaac Lab의 자동 매니저(명령, 관측, 행동)를 수동으로 재구현하여 소수점 여섯째 자리까지의 수치적 일관성을 확보했습니다.<br />
추론 중 진동을 방지하고 제어 안정성을 85% 향상시킨 치명적인 행동 타이밍 불일치 문제를 해결했습니다.<br />
포괄적인 아키텍처 및 디버깅 문서를 작성하여 향후 RL 배포 프로젝트의 온보딩 시간을 약 70% 단축했습니다.<br />

**물류 AMR MK3 개발 – 풀무원 (2022–2024)**
<img width="840" height="600" alt="스크린샷 2025-08-26 13-14-52" src="https://github.com/user-attachments/assets/fbbd4170-a2dc-4a49-8015-02bc231faa95" />
<img width="2298" height="1286" alt="스크린샷 2025-12-22 11-35-32" src="https://github.com/user-attachments/assets/764a567a-7cc7-4e78-9de0-0715a892aa48" />
<img width="816" height="1170" alt="image (5)" src="https://github.com/user-attachments/assets/f34f7d22-d8e0-44e4-93a1-2f8f5fd020e4" />


실제 물류 센터에 배치된 AMR 3대의 개발 및 개선 프로젝트로, Sim-to-Field 방법론을 따랐습니다.<br />
**[주요 업무]**<br />
Jetson 기반 ROS2 상위 제어기 + 하위 모터 드라이버 통합
Sick LiDAR (전/후), D435F (전/후), IMU, BMS CAN 센서 스택 구성
감속기, 1톤급 모터, 300kg 가반하중(0.2 m/s² 가감속)을 고려한 물리 제어
Jetson Xavier 제어 루프 불규칙성 진단 및 수정
작업 할당(Task Assignment) → 경로 추종(Path Follow) → 적재 흐름(Stacking Flow)과 WES 통합
안전 레이어 구현 (LiDAR 존, 비상 정지)<br />
**[사용 기술]**<br />
OS/Framework: Ubuntu 20.04/22.04, ROS1 Noetic
HW Interface: Jetson Xavier, CAN, UART, 부분 EtherCAT
Perception: SOS Lab LiDAR SDK, ZED2i, IMU Fusion
AI/ML: PyTorch, YOLOv5/YOLOv8, TensorRT, Roboflow/Label Studio
Control: PID, S-curve 제어, Motor Driver API
Networking: Socket, TCP ROS Bridge
Tools: ROS2, Foxglove, Isaac Sim, YOLO, Docker, NGC
Languages: Python, C++, C, Bash<br />
**[엔지니어링 성과]**<br />
IMU 드리프트 완화:
 시간이 지남에 따라 누적되는 IMU 드리프트로 인해 AMR의 방향 추정이 불안정해지는 문제가 있었습니다.
 IMU 의존도를 낮추고 비전 기반 구조로 자세 추정 시스템을 재설계했습니다.
 IMU는 보조 센서로 활용하고, 카메라 기반 라인/패턴 감지를 통해 방향을 지속적으로 보정하여 드리프트가 누적되기 전에 효과적으로 리셋했습니다.
Jetson 대역폭 제한 해결:
 Jetson Xavier가 3개 이상의 카메라 스트림을 안정적으로 처리하지 못하는 문제가 있었습니다.
 모든 영상 스트림을 별도의 AI 추론 모듈로 이동시켜 역할을 분리하고, Jetson은 상위 제어(경로 생성, 센서 퓨전, WES 통신)만 담당하도록 했습니다.
 이 아키텍처는 훗날 확장 가능한 Real-to-Sim 및 대규모 시뮬레이션 파이프라인 설계의 기반이 되었습니다.

**미니 로더 Digital Twin Real-to-Sim (R2S) 및 가상 입출고 – 풀무원 (2024)**
<img width="2115" height="1170" alt="스크린샷 2025-11-27 11-27-12" src="https://github.com/user-attachments/assets/3bc6c1d9-80a5-480a-b773-ad8c10fb9ae2" />
<img width="2298" height="1286" alt="스크린샷 2025-12-22 11-37-58" src="https://github.com/user-attachments/assets/85e7f295-7ff2-4e80-a394-c7d57bfff3e4" />

Omniverse Isaac Sim을 사용하여 실제 미니 로더의 기구학과 제어 프로파일을 완벽하게 복제했습니다.
<br />
**[주요 업무]**<br />
S-curve 모션 프로파일 기반 가상 MCU (vMCU) 구현
USD Articulation을 활용한 관절 재설계 (포크/리프터/슬라이드)
정확한 질량/관성 재현을 위한 Newton/Warp 물리 튜닝
시나리오 기반 팔레트/박스 흐름 시뮬레이션
WES ↔ 미니 로더 간 운영의 배포 전 검증<br />
**[사용 기술]**<br />
Isaac Sim 4.5/5.0
PhysX 5, Isaac Physics
USD, PhysX Articulation
Python (Carb/Kit SDK)
시나리오 러너, 처리량 평가 도구<br />
**[엔지니어링 성과]**<br />
시뮬레이션, 컨트롤러, 매퍼의 책임을 분리하여 확장 가능한 물리 오프로딩 R2S 아키텍처를 구축했습니다.
입고 → 대기 → 출고의 전체 흐름을 Digital Twin 내에서 완벽하게 재현했습니다.
Omniverse의 PD 기반 제어와 산업용 미니 로더의 S-curve 실제 모션 프로파일 간의 근본적인 불일치를 해결했습니다.
 다음을 결합한 Controller Emulation 구조를 구현했습니다:
  S-curve 가속/감속 모션 프로파일
  PhysX PD 제어기
  현실적인 힘 제한 및 기구적 제약
 2차 스프링-댐퍼 시스템에 대한 깊은 이해를 바탕으로 물리적 제어 거동을 정확하게 복제했습니다.

**Digital Twin 컨베이어 제어 시스템 (2024)**
컨베이어, 미니 로더, AMR의 동작을 통합한 시뮬레이션입니다.<br />
**[주요 업무]**<br />
컨베이어 벨트 속도/마찰/충돌 모델링
WES 연동 흐름 버퍼링 및 큐 로직 구현
가상 PLC I/O 매핑
JSON 기반 노코드(No-code) 월드 구성 시스템<br />
**[사용 기술]**<br />
Isaac Sim 4.5/5.0
PhysX 5, Isaac Physics
USD Articulation
Python SDK<br />
**[엔지니어링 성과]**<br />
하드웨어 통합 전 시뮬레이션에서 컨베이어 시스템 동작을 검증했습니다.
병목 현상, 축적 패턴, 타이밍 불일치를 사전에 파악하고 해결했습니다.

**휴머노이드 강화학습 환경 – LG CNS (2025)**
<img width="1207" height="666" alt="image (12)" src="https://github.com/user-attachments/assets/8e00d7ef-a590-4a83-bde5-09e129ee2abe" />
엔터프라이즈 휴머노이드 R&D에 맞춤화된 Isaac Lab 기반 RL 파이프라인입니다.<br />
**[주요 업무]**<br />
관절 매핑, 동역학 튜닝
보행/균형/리치(Reach) 태스크 설계
보상 설계(Reward Shaping), 커리큘럼 학습
Sim-to-Sim 및 Sim-to-Real 보정
고객을 위한 커스텀 Isaac Lab RL 플랫폼 구축<br />
**[사용 기술]**<br />
Isaac Lab RL, RL Games, PPO
PhysX Articulation
Python (Isaac Lab API), C++<br />
**[엔지니어링 성과]**<br />
프로덕션 레벨의 휴머노이드 RL 학습 환경을 처음부터 구축했습니다.
향후 IL/합성 데이터셋 파이프라인을 위한 기반을 마련했습니다.

**NVIDIA Isaac Sim 로보틱스 교육 – 한국로봇산업진흥원 (KIRIA, 2025)**
<img width="436" height="973" alt="image" src="https://github.com/user-attachments/assets/5ad743af-2887-460b-a996-7d39659a0f3b" />

기초 로보틱스 Digital Twin 커리큘럼 설계 및 강의.<br />
**[성과]**<br />
산업계 엔지니어들이 Omniverse/Isaac 기술을 채택하도록 지원했습니다.
국내 Digital Twin 생태계 확장에 기여했습니다.

**7. Isaac Sim Digital Twin 교육 – 삼성 SDS (2024)**<br />
**[성과]**<br />
사내 Digital Twin TF가 Isaac Sim 프로젝트를 독립적으로 수행할 수 있도록 역량을 강화했습니다.
PoC 수준의 이해와 도입을 가속화했습니다.

**핵폐기물 처리 Digital Twin PoC – 미국 에너지부 (DOE) (2023)**
유해 폐기물 이동 및 저장을 위한 갠트리 크레인 + AMR 협업 Digital Twin 프로젝트입니다.<br />
**[사용 기술]**<br />
Isaac Sim 4.5
PhysX 5 (고중량 아티큘레이션, 흔들림 동역학)
USD 갠트리 크레인 모델
Python, OmniGraph 시나리오 엔진<br />
**[성과]**<br />
실제 DOE 운영을 중단하지 않고 전체 위험 시나리오 테스트를 가능하게 했습니다.
고위험 시설에서의 Omniverse 실제 산업 적용 가능성을 입증했습니다.

---

https://youtu.be/yzHgp0LtWjU

https://youtu.be/SUSyJ1PRz4s

https://youtu.be/kJmhm3zdEd8

https://youtu.be/bwH30pljMTU

https://youtu.be/escuCJm5YmY
