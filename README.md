*<img width="1254" height="706" alt="스크린샷 2025-10-31 18-01-51" src="https://github.com/user-attachments/assets/44aa934b-862f-4978-8f82-2c8de99803fa" />
*Executive Summary**
The industry is entering a major transition in which the entire physical world is being reorganized into a trainable structure powered by WFM, RFM, and AI Agents. I aim to stand at the forefront of this shift by helping customers implement Physical AI in real industrial environments using NVIDIA Omniverse. My experience connecting AMRs, mini-loaders, conveyors, humanoids, Digital Twins, and RL/IL pipelines into a single end-to-end cycle has given me a deep engineering understanding of how to integrate real-world control, simulation, and AI learning. I have repeatedly identified and solved fundamental mismatches between physical systems, simulation behavior, and AI training, building scalable architectures across OpenUSD, Isaac Sim/Lab, Synthetic Data, and Jetson deployment. Through extensive collaboration with major Korean enterprises and government institutions, I have also gained a practical understanding of the organizational dynamics, decision-making patterns, and PoC→Pilot→Deployment bottlenecks they face when adopting Omniverse. This insight allows me to support customers not only technically but strategically. I am deeply passionate about creatively solving the complex challenges of Physical AI, and I hope to contribute at NVIDIA KOREA where this historic transformation of industry is being built at the front line.

**SKILL**
Simulation (Omniverse, Isaac Sim, USD, PhysX) · Robotics (ROS2, Jetson, Control) · AI for Robotics (RL/IL, GR00T, Synthetic Data) · Vision (YOLO, TensorRT) · Motion Capture (Meta Quest, Unity) · Logistics Automation (WCS/WMS Integration) · Embedded & System Architecture Design

**WORK EXPERIENCE**
2022.07 - Currently employed
**POLLUX**, Digital Twin Engineer - Digital Twin Division
I am the main developer of POLLUX, the first team in Korea to receive NVIDIA SAC NPN partnership for Omniverse solutions. Using NVIDIA Omniverse as my core tool, I have researched logistics simulation and successfully delivered multiple B2B projects. My development approach centers on key logistics assets and their operational integration with WCS and WMS layers.

**1.Meta Quest–based Imitation Learning, Synthetic Dataset Pipeline & Virtual Testbed for Humanoids (2025)**
<img width="823" height="642" alt="스크린샷 2025-08-26 13-15-49" src="https://github.com/user-attachments/assets/05a767a6-6d27-4160-9780-144de696dbc8" />

A project to collect human demonstration data and accelerate synthetic dataset generation for humanoid IL training.
[Main Tasks]
Meta Quest motion capture → Unity → Control Server → ROS2 → Isaac Sim humanoid action retargeting
Trajectory dataset generation for imitation learning
GR00T/N1-based synthetic dataset generation pipeline
Virtual testbed for humanoid manipulation & locomotion
[Technologies]
Motion Capture: Meta Quest Link, OpenXR
Video Processing: Unity Render Streaming, H.264 encoding/decoding (Python)
Networking: WebRTC over ROS2 bridge, custom UDP/TCP transport
Middleware: ROS2 Humanoid Action Msg (Joint pos/vel + vision sync)
Simulation: Isaac Sim humanoid motion mapping
Dataset: GR00T/N1 synthetic dataset generator, trajectory filtering
IL: BC, trajectory embedding, smoothing, noise injection
Visualization: Omniverse motion retargeting
Languages: Python, ROS2, C#, Unity, JSON/Parquet
[Engineering Achievements]
Replaced Apple Vision Pro–exclusive imitation learning & teleoperation pipeline with Meta Quest + Unity, removing cost barriers for enterprise clients.
Built a Dataset Acceleration Pipeline enabling IL/VLA training data generation by a single engineer.
Designed a multi-stack data flow (Meta Quest → Unity → ROS2 → Isaac Sim), creating a low-cost alternative that significantly accelerates trajectory and synthetic dataset creation.
This pipeline substantially removed the traditional bottleneck of IL data generation for humanoid learning.

**2.Logistics AMR MK3 Development – Pulmuone (2022–2024)**
Development and improvement of three AMRs deployed in a live logistics center, following a Sim-to-Field methodology.
[Main Tasks]
Jetson-based ROS2 high-level controller + low-level motor driver integration
Sick LiDAR (front/back), D435F (front/back), IMU, BMS CAN sensor stack
Physical control considering reducer, 1-ton motors, 300 kg payload (0.2 m/s² accel/dec.)
Jetson Xavier control-loop irregularity diagnosis & fix
Task Assignment → Path following → Stacking flow integrated with WES
Safety layer implementation (LiDAR zone, emergency stop)
[Technologies]
OS/Framework: Ubuntu 20.04/22.04, ROS1 Noetic
HW Interface: Jetson Xavier, CAN, UART, partial EtherCAT
Perception: SOS Lab LiDAR SDK, ZED2i, IMU Fusion
AI/ML: PyTorch, YOLOv5/YOLOv8, TensorRT, Roboflow/Label Studio
Control: PID, S-curve control, Motor Driver API
Networking: Socket, TCP ROS Bridge
Tools: ROS2, Foxglove, Isaac Sim, YOLO, Docker, NGC
Languages: Python, C++, C, Bash
[Engineering Achievements]
IMU Drift Mitigation:
 IMU drift accumulated over time and created instability in the AMR’s heading estimation.
 I reduced IMU dependency and re-architected the pose estimation system into a vision-aided structure.
 IMU became a supporting sensor, while camera-based line/pattern detection continuously refined heading—
 effectively resetting drift before it accumulates.
Jetson Bandwidth Limitation Fix:
 Jetson Xavier cannot reliably process more than three camera streams.
 I separated concerns by moving all image streams to a dedicated AI inference module, leaving Jetson responsible only for high-level control (pathing, sensor fusion, WES communication).
 This architecture later became the basis for how I design scalable Real-to-Sim and large-scale simulation pipelines.

**3.Mini-loader Digital Twin Real-to-Sim (R2S) for Virtual Inbound/Outbound – Pulmuone (2024)**
A complete replication of the real mini-loader’s kinematics and control profile using Omniverse Isaac Sim.
[Main Tasks]
S-curve motion profile–based virtual MCU (vMCU)
Joint redesign (fork/lifter/slide) using USD articulations
Newton/Warp physics tuning for accurate mass/inertia reproduction
Scenario-based pallet/box flow simulation
Pre-deployment verification of WES ↔ mini-loader operations
[Technologies]
Isaac Sim 4.5/5.0
PhysX 5, Isaac Physics
USD, PhysX Articulation
Python (Carb/Kit SDK)
Scenario runner, throughput evaluation tools
[Engineering Achievements]
Built a scalable physics-offloaded R2S architecture, separating simulation, controller, and mapper responsibilities.
Fully reproduced inbound → staging → outbound flow inside a Digital Twin.
Solved the fundamental mismatch between PD-based control in Omniverse and the S-curve real motion profile of industrial mini-loaders.
 I implemented a Controller Emulation structure that combined:
S-curve ease-in/ease-out motion profiles
PhysX PD controllers
realistic force limits & mechanical constraints
Gained deep understanding of 2nd-order spring–damper systems, enabling accurate replication of physical control behavior.

**4.Digital Twin Conveyor Control System (2024)**
A unified simulation integrating conveyor, mini-loader, and AMR behaviors.
[Main Tasks]
Conveyor belt velocity/friction/collision modeling
WES-aligned flow buffering & queueing logic
Virtual PLC I/O mapping
JSON-driven no-code world configuration system
[Technologies]
Isaac Sim 4.5/5.0
PhysX 5, Isaac Physics
USD articulations
Python SDK
[Engineering Achievements]
Validated conveyor system behavior in simulation before hardware integration
Resolved bottlenecks, accumulation patterns, timing mismatches in advance

**5.Humanoid Reinforcement Learning Environment – LG CNS (2025)**
Isaac Lab–based RL pipeline tailored for enterprise humanoid R&D.
[Main Tasks]
Joint mapping, dynamics tuning
Locomotion/balance/reach task design
Reward shaping, curriculum learning
Sim-to-Sim and Sim-to-Real calibration
Custom Isaac Lab RL platform for the client
[Technologies]
Isaac Lab RL, RL Games, PPO
PhysX articulation
Python (Isaac Lab API), C++
[Engineering Achievements]
Built a production-ready humanoid RL training environment from scratch
Established a foundation for future IL/Synthetic Dataset pipelines

**6.NVIDIA Isaac Sim Robotics Education – KIRIA(Korea Institute for Robot Industry Advancement, 2025)**
Basic robotics Digital Twin curriculum design & instruction.
[Achievements]
Enabled industry engineers to adopt Omniverse/Isaac technologies
Expanded domestic Digital Twin ecosystem

**7.Isaac Sim Digital Twin Training – Samsung SDS (2024)**
[Achievements]
Empowered internal Digital Twin TF to independently run Isaac Sim projects
Accelerated PoC-level understanding and adoption

**8.Nuclear Waste Handling Digital Twin PoC – U.S. Department of Energy (2023)**
A Digital Twin of gantry crane + AMR cooperation for hazardous waste movement and storage.
[Technologies]
Isaac Sim 4.5
PhysX 5 (high-mass articulation, sway dynamics)
USD gantry crane model
Python, OmniGraph scenario engine
[Achievements]
Enabled full-risk scenario testing without interrupting real DOE operations
Demonstrated the real industrial applicability of Omniverse in high-hazard facilities

---

https://youtu.be/yzHgp0LtWjU

https://youtu.be/SUSyJ1PRz4s

https://youtu.be/kJmhm3zdEd8

https://youtu.be/escuCJm5YmY

https://youtu.be/bwH30pljMTU
