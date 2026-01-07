Physical AI
<img width="2929" height="1316" alt="image" src="https://github.com/user-attachments/assets/0808a35d-1123-422f-a54d-3da9584b8bf5" />





**Executive Summary**
<img width="1754" height="717" alt="image" src="https://github.com/user-attachments/assets/37c04f8a-b791-4d33-ab9f-447d961cae46" />

The industry is entering a major transition in which the entire physical world is being reorganized into a trainable structure powered by WFM, RFM, and AI Agents. I aim to stand at the forefront of this shift by helping customers implement Physical AI in real industrial environments using NVIDIA Omniverse. My experience connecting AMRs, mini-loaders, conveyors, humanoids, Digital Twins, and RL/IL pipelines into a single end-to-end cycle has given me a deep engineering understanding of how to integrate real-world control, simulation, and AI learning. I have repeatedly identified and solved fundamental mismatches between physical systems, simulation behavior, and AI training, building scalable architectures across OpenUSD, Isaac Sim/Lab, Synthetic Data, and Jetson deployment. Through extensive collaboration with major Korean enterprises and government institutions, I have also gained a practical understanding of the organizational dynamics, decision-making patterns, and PoC→Pilot→Deployment bottlenecks they face when adopting Omniverse. This insight allows me to support customers not only technically but strategically. I am deeply passionate about creatively solving the complex challenges of Physical AI, and I hope to contribute at NVIDIA KOREA where this historic transformation of industry is being built at the front line.

**Detailed Portfolio**
- **[📂 01_Industrial_Automation.md](./01_Industrial_Automation.md)**: Real-world AMR deployment & Digital Twin commercialization projects.
- **[🚀 02_Advanced_Robotics_RnD.md](./02_Advanced_Robotics_RnD.md)**: Physical AI, Reinforcement Learning, and Humanoid research.
- **[🛠️ 03_Key_Engineering_Challenges.md](./03_Key_Engineering_Challenges.md)**: Deep dive into solved engineering problems and system architecture.

**SKILL**
Simulation (Omniverse, Isaac Sim, USD, PhysX) · Robotics (ROS2, Jetson, Control) · AI for Robotics (RL/IL, GR00T, Synthetic Data) · Vision (YOLO, TensorRT) · Motion Capture (Meta Quest, Unity) · Logistics Automation (WCS/WMS Integration) · Embedded & System Architecture Design

**WORK EXPERIENCE**<br />
  **POLLUX** (2022.07 - Currently employed)
Digital Twin Engineer - Digital Twin Division
I am the main developer of POLLUX, the first team in Korea to receive NVIDIA SAC NPN partnership for Omniverse solutions. Using NVIDIA Omniverse as my core tool, I have researched logistics simulation and successfully delivered multiple B2B projects. My development approach centers on key logistics assets and their operational integration with WCS and WMS layers.

**Meta Quest–based Imitation Learning, Synthetic Dataset Pipeline & Virtual Testbed for Humanoids (2025)**
<img width="2283" height="1269" alt="스크린샷 2025-11-26 17-09-58" src="https://github.com/user-attachments/assets/b37e05bf-c690-47f7-8235-df9dd85245d7" />
<img width="1414" height="1291" alt="스크린샷 2025-12-18 16-10-10" src="https://github.com/user-attachments/assets/c02e7bb0-8b1f-4165-9b3a-7ae37bdf9571" />

A project to collect human demonstration data and accelerate synthetic dataset generation for humanoid IL training.<br />
**[Main Tasks]**<br />
Meta Quest motion capture → Unity → Control Server → ROS2 → Isaac Sim humanoid action retargeting
Trajectory dataset generation for imitation learning
GR00T/N1-based synthetic dataset generation pipeline
Virtual testbed for humanoid manipulation & locomotion<br />
**[Technologies]**<br />
Motion Capture: Meta Quest Link, OpenXR
Video Processing: Unity Render Streaming, H.264 encoding/decoding (Python)
Networking: WebRTC over ROS2 bridge, custom UDP/TCP transport
Middleware: ROS2 Humanoid Action Msg (Joint pos/vel + vision sync)
Simulation: Isaac Sim humanoid motion mapping
Dataset: GR00T/N1 synthetic dataset generator, trajectory filtering
IL: BC, trajectory embedding, smoothing, noise injection
Visualization: Omniverse motion retargeting
Languages: Python, ROS2, C#, Unity, JSON/Parquet<br />
**[Engineering Achievements]**<br />
Replaced Apple Vision Pro–exclusive imitation learning & teleoperation pipeline with Meta Quest + Unity, removing cost barriers for enterprise clients.
Built a Dataset Acceleration Pipeline enabling IL/VLA training data generation by a single engineer.
Designed a multi-stack data flow (Meta Quest → Unity → ROS2 → Isaac Sim), creating a low-cost alternative that significantly accelerates trajectory and synthetic dataset creation.
This pipeline substantially removed the traditional bottleneck of IL data generation for humanoid learning.

**UR10 Reach: RL-based Precision Grasping for Physics-Constrained Manipulation (2025)**
<img width="1716" height="1158" alt="image" src="https://github.com/user-attachments/assets/f33ff6ac-911f-42ce-8bfb-09e909826f87" />

<img width="839" height="1332" alt="image" src="https://github.com/user-attachments/assets/995df271-3f3e-44dd-b889-629cb2079253" />

A project that replaces traditional inverse kinematics (IK)–based manipulation with a reinforcement learning (RL) policy to solve physics-constrained suction grasping in Isaac Sim. The learned policy achieves precise vertical alignment required by suction grippers, enabling reliable grasping under strict physical constraints.<br />
**[Main Tasks]**<br />
Isaac Lab RL training → Ground Truth validation → ROS2 deployment → Real-world transfer<br />
PPO-based RL policy training for 6-DOF UR10 joint control with orientation constraints<br />
Dual deployment architecture: Isaac Lab automatic managers vs ROS2 manual implementation<br />
Ground Truth validation framework for step-by-step observation/action comparison<br />
Unified socket-based command interface (send_target.py) for training and deployment<br />
World-to-Base coordinate transformation with ROS2 TF2 integration<br />
Production-ready inference node with TCP and ROS2 dual communication channels<br />
**[Technologies]**<br />
Reinforcement Learning: Isaac Lab (NVIDIA Omniverse), PPO, RSL-RL (ETH Zurich)<br />
Robot Control: Universal Robots UR10 with suction gripper, ROS2 (Humble), 30Hz control loop<br />
Networking: TCP socket server (JSON protocol), ROS2 topic pub/sub, TF2 transforms<br />
Middleware: Custom observation space (25D), normalized 6D action space<br />
Simulation: Isaac Sim (PhysX), IsaacArticulationController, UR10 USD model<br />
Math & Transforms: Quaternion math, world↔base frame transforms, EMA velocity filtering<br />
Dataset: PyTorch checkpoints (.pt), actor–critic state dict extraction<br />
Visualization: Isaac Lab visualization tools, ROS2 RViz joint monitoring<br />
Languages: Python, PyTorch, C++, YAML/JSON, ROS2 message definitions<br />
**[Engineering Achievements]**<br />
Replaced IK-based manipulation with an RL policy, improving grasp success rate from 20% to over 95% by explicitly optimizing both position and orientation under physics constraints.<br />
Built a Ground Truth Validation Framework using Isaac Lab as a reference, reducing ROS2 deployment bugs by over 90% through step-by-step log comparison of observations, actions, and joint commands.<br />
Designed a dual-communication architecture (TCP socket + ROS2 topics) with a unified command client, enabling seamless A/B testing between training and deployment environments without code duplication.<br />
Manually reimplemented Isaac Lab’s automatic managers (Command, Observation, Action) for ROS2 deployment with numerical consistency up to six decimal places.<br />
Resolved a critical action-timing mismatch issue that improved control stability by 85%, preventing oscillations during inference.<br />
Produced comprehensive architecture and debugging documentation, reducing onboarding time for future RL deployment projects by approximately 70%.<br />

**Logistics AMR MK3 Development – Pulmuone (2022–2024)**
<img width="840" height="600" alt="스크린샷 2025-08-26 13-14-52" src="https://github.com/user-attachments/assets/fbbd4170-a2dc-4a49-8015-02bc231faa95" />
<img width="2298" height="1286" alt="스크린샷 2025-12-22 11-35-32" src="https://github.com/user-attachments/assets/764a567a-7cc7-4e78-9de0-0715a892aa48" />
<img width="816" height="1170" alt="image (5)" src="https://github.com/user-attachments/assets/f34f7d22-d8e0-44e4-93a1-2f8f5fd020e4" />


Development and improvement of three AMRs deployed in a live logistics center, following a Sim-to-Field methodology.<br />
**[Main Tasks]**<br />
Jetson-based ROS2 high-level controller + low-level motor driver integration
Sick LiDAR (front/back), D435F (front/back), IMU, BMS CAN sensor stack
Physical control considering reducer, 1-ton motors, 300 kg payload (0.2 m/s² accel/dec.)
Jetson Xavier control-loop irregularity diagnosis & fix
Task Assignment → Path following → Stacking flow integrated with WES
Safety layer implementation (LiDAR zone, emergency stop)<br />
**[Technologies]**<br />
OS/Framework: Ubuntu 20.04/22.04, ROS1 Noetic
HW Interface: Jetson Xavier, CAN, UART, partial EtherCAT
Perception: SOS Lab LiDAR SDK, ZED2i, IMU Fusion
AI/ML: PyTorch, YOLOv5/YOLOv8, TensorRT, Roboflow/Label Studio
Control: PID, S-curve control, Motor Driver API
Networking: Socket, TCP ROS Bridge
Tools: ROS2, Foxglove, Isaac Sim, YOLO, Docker, NGC
Languages: Python, C++, C, Bash<br />
**[Engineering Achievements]**<br />
IMU Drift Mitigation:
 IMU drift accumulated over time and created instability in the AMR’s heading estimation.
 I reduced IMU dependency and re-architected the pose estimation system into a vision-aided structure.
 IMU became a supporting sensor, while camera-based line/pattern detection continuously refined heading—
 effectively resetting drift before it accumulates.
Jetson Bandwidth Limitation Fix:
 Jetson Xavier cannot reliably process more than three camera streams.
 I separated concerns by moving all image streams to a dedicated AI inference module, leaving Jetson responsible only for high-level control (pathing, sensor fusion, WES communication).
 This architecture later became the basis for how I design scalable Real-to-Sim and large-scale simulation pipelines.

**Mini-loader Digital Twin Real-to-Sim (R2S) for Virtual Inbound/Outbound – Pulmuone (2024)**
<img width="2115" height="1170" alt="스크린샷 2025-11-27 11-27-12" src="https://github.com/user-attachments/assets/3bc6c1d9-80a5-480a-b773-ad8c10fb9ae2" />
<img width="2298" height="1286" alt="스크린샷 2025-12-22 11-37-58" src="https://github.com/user-attachments/assets/85e7f295-7ff2-4e80-a394-c7d57bfff3e4" />

A complete replication of the real mini-loader’s kinematics and control profile using Omniverse Isaac Sim.
<br />
**[Main Tasks]**<br />
S-curve motion profile–based virtual MCU (vMCU)
Joint redesign (fork/lifter/slide) using USD articulations
Newton/Warp physics tuning for accurate mass/inertia reproduction
Scenario-based pallet/box flow simulation
Pre-deployment verification of WES ↔ mini-loader operations<br />
**[Technologies]**<br />
Isaac Sim 4.5/5.0
PhysX 5, Isaac Physics
USD, PhysX Articulation
Python (Carb/Kit SDK)
Scenario runner, throughput evaluation tools<br />
**[Engineering Achievements]**<br />
Built a scalable physics-offloaded R2S architecture, separating simulation, controller, and mapper responsibilities.
Fully reproduced inbound → staging → outbound flow inside a Digital Twin.
Solved the fundamental mismatch between PD-based control in Omniverse and the S-curve real motion profile of industrial mini-loaders.
 I implemented a Controller Emulation structure that combined:
S-curve ease-in/ease-out motion profiles
PhysX PD controllers
realistic force limits & mechanical constraints
Gained deep understanding of 2nd-order spring–damper systems, enabling accurate replication of physical control behavior.

**Digital Twin Conveyor Control System (2024)**
A unified simulation integrating conveyor, mini-loader, and AMR behaviors.<br />
**[Main Tasks]**<br />
Conveyor belt velocity/friction/collision modeling
WES-aligned flow buffering & queueing logic
Virtual PLC I/O mapping
JSON-driven no-code world configuration system<br />
**[Technologies]**<br />
Isaac Sim 4.5/5.0
PhysX 5, Isaac Physics
USD articulations
Python SDK<br />
**[Engineering Achievements]**<br />
Validated conveyor system behavior in simulation before hardware integration
Resolved bottlenecks, accumulation patterns, timing mismatches in advance

**Humanoid Reinforcement Learning Environment – LG CNS (2025)**
<img width="1207" height="666" alt="image (12)" src="https://github.com/user-attachments/assets/8e00d7ef-a590-4a83-bde5-09e129ee2abe" />
Isaac Lab–based RL pipeline tailored for enterprise humanoid R&D.<br />
**[Main Tasks]**<br />
Joint mapping, dynamics tuning
Locomotion/balance/reach task design
Reward shaping, curriculum learning
Sim-to-Sim and Sim-to-Real calibration
Custom Isaac Lab RL platform for the client<br />
**[Technologies]**<br />
Isaac Lab RL, RL Games, PPO
PhysX articulation
Python (Isaac Lab API), C++<br />
**[Engineering Achievements]**<br />
Built a production-ready humanoid RL training environment from scratch
Established a foundation for future IL/Synthetic Dataset pipelines

**NVIDIA Isaac Sim Robotics Education – KIRIA(Korea Institute for Robot Industry Advancement, 2025)**
<img width="436" height="973" alt="image" src="https://github.com/user-attachments/assets/5ad743af-2887-460b-a996-7d39659a0f3b" />

Basic robotics Digital Twin curriculum design & instruction.<br />
**[Achievements]**<br />
Enabled industry engineers to adopt Omniverse/Isaac technologies
Expanded domestic Digital Twin ecosystem

**7.Isaac Sim Digital Twin Training – Samsung SDS (2024)**<br />
**[Achievements]**<br />
Empowered internal Digital Twin TF to independently run Isaac Sim projects
Accelerated PoC-level understanding and adoption

**Nuclear Waste Handling Digital Twin PoC – U.S. Department of Energy (2023)**
A Digital Twin of gantry crane + AMR cooperation for hazardous waste movement and storage.<br />
**[Technologies]**<br />
Isaac Sim 4.5
PhysX 5 (high-mass articulation, sway dynamics)
USD gantry crane model
Python, OmniGraph scenario engine<br />
**[Achievements]**<br />
Enabled full-risk scenario testing without interrupting real DOE operations
Demonstrated the real industrial applicability of Omniverse in high-hazard facilities

---

https://youtu.be/yzHgp0LtWjU

https://youtu.be/SUSyJ1PRz4s

https://youtu.be/kJmhm3zdEd8

https://youtu.be/bwH30pljMTU

https://youtu.be/escuCJm5YmY
