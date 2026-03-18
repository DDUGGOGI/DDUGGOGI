# 2026 AMR RDS · Sim-to-Real 개발 요약

**최종 갱신: 2026-03**  
**프로젝트:** DAVID-C RDS / david50c — 자율주행 · 담당자 추적 · 도킹 · Nav2 · RMS 연동  
**작업 지향:** AMR **전체 생태계를 빠르게 완성** — **Sim 디지털 엔지니어링**으로 개발 가속, Real은 S2R·현장 마감에 집중.  
**상세 원본:** `knowledge_base/05_물류_자동화_시스템/AMR RDS in sim to real/` (2026 개발 과정 문서)

---

## 0. AMR RDS 개발 구조 (Sim · Real 이원화)

**목표:** **AMR 전체 생태계**(주행·도킹·맵·추적·시나리오·RMS·API 등)를 **빠르게 한 바퀴 완성**하는 것.  
그래서 **실기 투입 전에 할 수 있는 일은 최대한 Sim(Isaac)에서 처리**한다. Sim을 **디지털 엔지니어링 허브**로 쓰면 — TF·도킹 파이프라인·Nav2·멀티로봇·USD/카메라 정합 등을 **가상에서 반복 검증**하고, 실기는 **S2R 갭·현장 이슈·튜닝**에 시간을 쓰게 되어 **전체 리드타임이 줄어든다.** 이게 2026 작업의 **가속 타겟**이다.

개발할 때 **가상에서 먼저 깨는 문제**와 **실기(david50c)에서 맞추는 문제**가 다르다.  
`knowledge_base/…/AMR RDS in sim to real` 아래 **sim_docs / real_docs** 나눔은 폴더 규칙이 아니라, 위 목표에 맞춰 **Sim으로 압축한 축**과 **Real로 마감하는 축**을 그대로 옮겨 둔 구조다.

- **Sim 축 (디지털 엔지니어링):** 통제 가능한 가상 환경에서 파이프라인·파라미터 초안·실패 재현을 **빠르게 돌려** 생태계 조각을 **먼저 완성**한다.
- **Real 축:** 모터·MPPI·맵 드리프트·현장 시나리오·RMS 등 **실물 전용 갭**만 실기에서 맞춘다.
- **본 문서(05):** “생태계 어디까지 Sim에서 닫았는지 / Real에서 남았는지”를 한눈에 보는 **작업 대시보드**.

```mermaid
%%{init: {'theme':'base', 'themeVariables': { 'primaryColor':'#2d2d2d', 'primaryTextColor':'#f0f0f0', 'primaryBorderColor':'#555', 'lineColor':'#888' }}}%%
flowchart TB
    GOAL["목표\nAMR 생태계 조기 완성\n(Sim 디지털 엔지니어링으로 가속)"]
    subgraph Hub["작업 허브"]
        ME["05_AMR_RDS.md\n전체 그림·우선순위"]
    end
    subgraph SimAxis["Sim 축 — 디지털 엔지니어링 (가속)"]
        S0["Isaac + Nav2·도킹\n환경 재현·반복"]
        S1["AprilTag·TF·frame_id\n파이프라인 선검증"]
        S2["파라미터·플로우 초안\n실기 전 압축 완료"]
        S0 --> S1 --> S2
    end
    subgraph RealAxis["Real 축 — 검증·S2R·현장 마감"]
        R0["동일 스택 bringup"]
        R1["Sim-to-Real 갭\n모터·MPPI·코스트맵"]
        R2["현장 기능\n추적·도킹·시나리오·RMS"]
        R0 --> R1 --> R2
    end
    subgraph Log["기록"]
        SD["sim_docs/\n가상 쪽 작업 로그"]
        RD["real_docs/\n실기 쪽 작업 로그"]
    end
    GOAL --> ME
    ME --> SimAxis
    ME --> RealAxis
    S2 -.->|초안·검증분| R0
    R1 -.->|원인 재현·설계| S0
    SimAxis --> SD
    RealAxis --> RD
```

| 내가 쓰는 축 | 디렉터리 | 이 축에서 주로 하는 일 |
|--------------|----------|------------------------|
| **Sim** | `sim_docs/davidc_virtual_testbed/` | USD·카메라·TF·도킹 시퀀스를 Sim에서 끝까지 재현 |
| **Sim** | `sim_docs/work_report/` | Sim 관점 일지, sim↔real 비교 메모 |
| **Real** | `real_docs/work_report/` | 실기 튜닝, 추적 주행, 시나리오 큐, 현장 이슈 |
| **Real·설계** | `real_docs/*.md` (구조·API) | Nav2/RDS 역할 정리, RMS API 전략 등 “실제 배포 전 설계” |

폴더 이름은 **Sim/Real 갈래의 아카이브**이고, 위 다이어그램은 **생태계 조기 완성을 위해 Sim으로 먼저 닫고 Real로 마감하는 흐름**에 맞춰져 있다.

---

## 1. 한눈에 보는 RDS 스택

**RDS** = 로봇 1대당 1세트. 내부는 **ROS2**이며 **Nav2**가 주행 오케스트레이터, **OpenNav Docking**이 도킹 시 cmd_vel을 담당. 외부 **RMS**와는 API·시나리오 큐·Web 등으로 연동하는 방향으로 확장 중이다.

```mermaid
%%{init: {'theme':'base', 'themeVariables': { 'primaryColor':'#2d2d2d', 'primaryTextColor':'#f0f0f0', 'primaryBorderColor':'#555', 'lineColor':'#888' }}}%%
flowchart TB
    subgraph EXT["외부"]
        RMS["RMS / Web UI\n(FastAPI·rosbridge 등)"]
    end
    subgraph RDS["RDS (로봇 1대)"]
        subgraph ORCH["오케스트레이션 (확장)"]
            SQ["scenario_queue_node\nNav2·도킹 순차"]
            API["API 레이어\n(REST·브리지·향후)"]
        end
        subgraph ROS2["ROS2 레이어"]
            N2["Nav2\n주행 오케스트레이터"]
            DK["opennav_docking"]
            MAP["map_server · AMCL"]
            ZL["zlac8015d → odom"]
        end
        CV["cmd_vel\n단일 토픽"]
    end
    RMS <-->|시나리오·명령| SQ
    API -.->|향후 통합| SQ
    SQ -->|NavigateToPose| N2
    SQ -->|DockRobot| DK
    RMS -.->|API 경로| API
    N2 -->|주행 시| CV
    DK -->|도킹 시| CV
    MAP --> N2
    ZL --> CV
    CV --> DRV["구동"]
```

---

## 2. Nav2 = 주행 오케스트레이터

목표 수신부터 **전역 경로 → 스무딩 → MPPI 로컬 제어 → cmd_vel**까지 한 파이프라인으로 묶인다.

```mermaid
%%{init: {'theme':'base', 'themeVariables': { 'primaryColor':'#2d2d2d', 'primaryTextColor':'#f0f0f0', 'primaryBorderColor':'#555', 'lineColor':'#888' }}}%%
flowchart LR
    subgraph In["입력"]
        G[Goal 액션]
        S["/scan"]
        O["/odom"]
        M[정적 map]
    end
    subgraph Nav2["Nav2"]
        BT[BT Navigator]
        P[Planner\nNavFn]
        SM[Smoother]
        CO[Global/Local\nCostmap]
        A[AMCL\nmap→odom]
        C[Controller\nMPPI]
    end
    subgraph Out["출력"]
        V[cmd_vel]
    end
    G --> BT
    M --> A
    M --> CO
    S --> A
    S --> CO
    O --> C
    A --> P
    A --> C
    CO --> P
    CO --> C
    BT --> P
    BT --> C
    P --> SM --> C
    C --> V
```

| 구성요소 | 역할 |
|----------|------|
| BT Navigator | 목표·리플랜·리커버리 시퀀스 |
| Planner + Costmap | 전역 경로 |
| Controller (MPPI) | 추종·cmd_vel (DWB 대체 튜닝) |
| AMCL | map→odom TF |

---

## 3. 시나리오 큐 (`scenario_queue`) — 2026-03 진행

Nav2 **바깥**에서 **시나리오를 한 건씩** 실행한다. Nav2는 “지금 받은 한 목표”만 수행하고, **순서·큐·Nav+Dock 혼합**은 큐 노드가 담당한다.

```mermaid
%%{init: {'theme':'base', 'themeVariables': { 'primaryColor':'#2d2d2d', 'primaryTextColor':'#f0f0f0', 'primaryBorderColor':'#555', 'lineColor':'#888' }}}%%
flowchart LR
    subgraph In["입력"]
        ADD["scenario_queue/add\n(PoseStamped 등)"]
        RMS_UI["RMS Web\n배치 전송"]
    end
    subgraph Q["scenario_queue_node"]
        QUEUE["내부 큐"]
        EXEC["순차 실행"]
    end
    subgraph Actions["액션"]
        NAV["NavigateToPose"]
        DOCK["DockRobot"]
    end
    ADD --> QUEUE
    RMS_UI --> QUEUE
    QUEUE --> EXEC
    EXEC --> NAV
    EXEC --> DOCK
    NAV -->|result| EXEC
    DOCK -->|result| EXEC
```

**진행 단계 요약 (문서 260313 기준):**  
Nav2만 큐 → 도킹 타입 추가 → 큐 삭제·수정 → 상태·피드백 퍼블리시 → rosbridge + `rms_server` + Web UI → GUI 맵 기반 Nav/Dock·로그 등. **다중 로봇·UX 고도화**는 이후 확장.

---

## 4. Sim-to-Real 정규화 (실기 david50c)

Isaac Sim에서는 양호하나 실기에서 **스핀·휘청·가다 서다·도킹 속도** 이슈가 있어, **모터 → Nav2(코스트·경로) → 도킹** 순으로 맞춤.

```mermaid
%%{init: {'theme':'base', 'themeVariables': { 'primaryColor':'#2d2d2d', 'primaryTextColor':'#f0f0f0', 'primaryBorderColor':'#555', 'lineColor':'#888' }}}%%
flowchart LR
    subgraph P["Sim vs Real 차이"]
        P1["모터 램프\n~1000ms"]
        P2["스핀·휘청"]
        P3["경로·코스트맵"]
        P4["도킹 체감 속도"]
    end
    subgraph S["조치"]
        S1["가·감속\n200ms 파라미터"]
        S2["글로벌 코스트·\n로컬 반영"]
        S3["MPPI·출발·\nprogress 튜닝"]
        S4["도킹 파라미터\n문서화·조정"]
    end
    subgraph R["목표"]
        R1["cmd_vel 응답 정렬"]
        R2["주행 안정"]
        R3["도킹 재현성"]
    end
    P1 --> S1 --> R1
    P2 --> S3 --> R2
    P3 --> S2 --> R2
    P4 --> S4 --> R3
```

| 조치 | 내용 |
|------|------|
| zlac8015d | `accel_time_ms` / `decel_time_ms` 기본 **200ms** |
| Nav2 | MPPI critic·temperature·velocity smoother, 코스트맵 강화 |
| 참고 문서 | `260309_sim_to_real_normalization.md`, `260303_nav2_sim_vs_real_analysis.md`, `260226_isaac_sim_vs_real_spin_wobble_analysis.md` |

---

## 5. 도킹 파이프라인 (AprilTag → cmd_vel)

**실기·Sim 공통 개념:** 근처 이동(Nav2) → 태그 인식 → 브리지 → 도킹 서버 → **후진** 등으로 접촉.

```mermaid
%%{init: {'theme':'base', 'themeVariables': { 'primaryColor':'#2d2d2d', 'primaryTextColor':'#f0f0f0', 'primaryBorderColor':'#555', 'lineColor':'#888' }}}%%
flowchart TB
    subgraph Nav["1. 접근"]
        N2[Nav2 NavigateToPose\n스테이징 근처]
    end
    subgraph Sense["2. 인지"]
        IMG[카메라 이미지·camera_info]
        AT[AprilTag\nTF parent→tag_0]
        BR[april_bridge\n/detected_dock_pose]
    end
    subgraph Dock["3. 도킹"]
        DS[opennav_docking\nGraceful Controller]
        CV[cmd_vel]
    end
    N2 --> IMG
    IMG --> AT
    AT --> BR
    BR --> DS
    DS --> CV
```

**Sim에서 중요한 점:** `header.frame_id`(예: `camera_optical_link` vs `sim_camera`)를 AprilTag·브리지·**map까지 TF 체인**과 일치시켜야 한다. 상세: `2026-03-05_도킹_apriltag_파이프라인_구조.md`, `260309_docking_tf_tag0_flow.md`.  
**실기 이슈:** 글로벌 맵·환경 변화 시 AMCL 드리프트 → 도킹 정렬 오차. 대응 방향: `260309_global_map_vs_changing_env_docking.md`.

---

## 6. 담당자 추적 주행 (person follow)

**cmd_vel을 직접 내지 않음.** RealSense ×2 + YOLOv8-nano(TensorRT) → 3D pose → **NavigateToPose**만 주기 갱신.

```mermaid
%%{init: {'theme':'base', 'themeVariables': { 'primaryColor':'#2d2d2d', 'primaryTextColor':'#f0f0f0', 'primaryBorderColor':'#555', 'lineColor':'#888' }}}%%
flowchart TB
    subgraph sensors["센서"]
        RS_R[RealSense\nfront_right]
        RS_L[RealSense\nfront_left]
    end
    subgraph perception["인지"]
        PD[person_detection_node\nYOLOv8n + TensorRT]
        TPP[target_pose_publisher_node\n깊이 최소 1명]
    end
    subgraph control["제어"]
        FG[follow_goal_node\n목표 → map]
    end
    subgraph nav["Nav2"]
        BT[NavigateToPose]
    end
    RS_R -->|image_raw| PD
    RS_R -->|depth, camera_info| TPP
    RS_L -.->|선택| TPP
    PD -->|Detection2DArray| TPP
    TPP -->|target_person_pose| FG
    FG -->|Goal| BT
    BT -->|cmd_vel| ROBOT[로봇]
    SVC[set_tracking] <--> FG
```

| 항목 | 내용 |
|------|------|
| 플랫폼 | ROS2 Humble, Jetson, TensorRT 10.x |
| 전략 | 목표 = 로봇 + ratio×(사람−로봇), `lateral_boost`, `min_follow_distance` |
| 문서 | `260310_담당자_추적_주행_예상_작업.md`, 전략 구상, `person_follow_params.yaml` |

---

## 7. cmd_vel 소스·모드 (통합 뷰)

```mermaid
%%{init: {'theme':'base', 'themeVariables': { 'primaryColor':'#2d2d2d', 'primaryTextColor':'#f0f0f0', 'primaryBorderColor':'#555', 'lineColor':'#888' }}}%%
flowchart TB
    subgraph modes["목표 유입"]
        RVIZ[Rviz 목표]
        TRK[담당자 추적 ON]
        SCQ[시나리오 큐]
        DOCK_ACT[DockRobot 직접]
    end
    subgraph nav2["Nav2"]
        BT[bt_navigator]
    end
    subgraph docking["도킹"]
        DSV[opennav_docking]
    end
    CV[cmd_vel]
    RVIZ --> BT
    TRK -->|NavigateToPose| BT
    SCQ -->|NavigateToPose| BT
    SCQ -->|DockRobot| DSV
    DOCK_ACT --> DSV
    BT --> CV
    DSV --> CV
    CV --> ZLAC[zlac8015d]
```

---

## 8. RMS · API 레이어 (로드맵)

다수 로봇 **RMS** ↔ 로봇별 **RDS**는 **API 레이어**로 ROS2를 캡슐화하는 것이 목표. REST/gRPC vs ROS2 직접 등 옵션 비교·단계적 노출은 `04-RDS-API-Layer-Analysis-and-Strategy.md` 참고.

```mermaid
%%{init: {'theme':'base', 'themeVariables': { 'primaryColor':'#2d2d2d', 'primaryTextColor':'#f0f0f0', 'primaryBorderColor':'#555', 'lineColor':'#888' }}}%%
flowchart LR
    RMS[RMS] <-->|HTTP·WS 등| API[API·브리지]
    API <-->|액션·토픽| N2[Nav2]
    API <-->|도킹| DK[Docking]
    API <-->|맵·포즈| ML[Map·AMCL]
```

**노출 기능 후보:** 주행 목표·취소, 도킹, 맵·초기 포즈, 로봇 상태·헬스.

---

## 9. 업무 영역 요약표

| 영역 | 내용 | 산출·문서 |
|------|------|-----------|
| 주행 안정화 | MPPI, 모터 200ms, 코스트맵 | zlac8015d, nav2_params |
| Sim-to-Real | Isaac ↔ 실기 갭 분석·튜닝 | sim_docs + `260309_sim_to_real_normalization.md` |
| 시나리오·RMS | 큐 노드, Web UI, rms_server | `260313_시나리오_큐_노드_진행.md` |
| 담당자 추적 | YOLO+깊이+Nav2 목표만 | person_follow_* 패키지 |
| 도킹 | AprilTag·TF·Sim frame 정합 | docking_flow, apriltag 파이프라인 문서 |
| API 전략 | RMS 연동 설계 | `04-RDS-API-Layer-Analysis-and-Strategy.md` |
| 기타 | Premise·QR·Kyverno 등 | 각 모듈 work_report |

---

## 10. 타임라인 (개념)

```mermaid
%%{init: {'theme':'base', 'themeVariables': { 'primaryColor':'#2d2d2d', 'primaryTextColor':'#f0f0f0', 'primaryBorderColor':'#555', 'lineColor':'#888' }}}%%
gantt
    title 2026 AMR RDS 업무 흐름 (개념)
    dateFormat YYYY-MM-DD
    section Sim
    Isaac Nav2·도킹·TF     :2026-02-20, 14d
    section Real
    Sim-to-Real·MPPI       :2026-03-01, 10d
    도킹·맵 드리프트 분석   :2026-03-09, 5d
    section 기능
    담당자 추적 파이프라인 :2026-03-10, 14d
    시나리오 큐·RMS·GUI    :2026-03-13, 14d
```

---

## 11. 빠른 링크 (knowledge_base 상대 경로)

| 주제 | 경로 |
|------|------|
| Nav2 구조 | `real_docs/ROS2-RDS-Structure-Nav2-Orchestrator.md` |
| API 전략 | `real_docs/04-RDS-API-Layer-Analysis-and-Strategy.md` |
| Sim 정규화 | `real_docs/work_report/260309_sim_to_real_normalization.md` |
| 도킹 플로우 | `real_docs/work_report/260309_docking_flow.md` |
| 시나리오 큐 | `real_docs/work_report/260313_시나리오_큐_노드_진행.md` |
| AprilTag Sim | `sim_docs/davidc_virtual_testbed/2026-03-05_도킹_apriltag_파이프라인_구조.md` |
| MPPI 튜닝 | `real_docs/work_report/260309_MPPI-performance-tuning-options.md` |

---

## 12. 요약

- **RDS**는 Nav2(주행)·도킹·맵/AMCL·구동으로 구성되며, **2026년에는 시나리오 큐 + RMS Web**으로 다단계 임무를 오케스트레이션한다.
- **Sim-to-Real**은 Isaac 가상 테스트베드에서 TF·도킹 파이프라인을 검증하고, 실기에서는 **모터 응답·MPPI·코스트맵**으로 갭을 줄인다.
- **담당자 추적**은 Nav2만 사용해 장애물 회피를 유지한다.
- **RMS·API**는 다로봇 운영을 위한 다음 레이어로 문서화되어 있다.

본 문서는 **Sim·Real 두 축으로 쌓아 온 2026 작업**을 한 화면에서 잡기 위한 것이고, 구현·실험 디테일은 각 축의 `.md`에 남겨 둔다.
