**Volume 01. Electrical Architecture Fundamentals**


# Chapter 05. Physical AI Electrical Architecture

##  

## 05.01. Edge AI Integration

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

Edge AI integration places artificial intelligence computation directly within the physical system, close to sensors, actuators, and real-time controllers. In the Physical AI electrical architecture, the edge computing layer connects conventional robot control electronics with perception, learning, and decision functions while avoiding continuous dependence on remote cloud infrastructure.

A practical architecture separates deterministic machine control from computationally intensive AI processing. Motor control, servo loops, emergency handling, and basic motion functions remain on MCUs, dedicated controllers, or real-time processors, while an edge AI computer executes perception, localization, prediction, planning, and higher-level decision algorithms. This separation preserves predictable control timing while enabling advanced intelligence.

The resulting system normally operates at multiple processing rates. A motor controller may execute current or torque regulation at kilohertz frequencies, while a robot controller performs trajectory and motion control at hundreds of hertz. Camera or LiDAR perception may operate at tens of frames per second, and complex AI planning can operate more slowly. Edge integration must therefore coordinate asynchronous information without forcing every subsystem into one execution cycle.

Sensors form the primary input boundary of the edge AI platform. Cameras, LiDAR, radar, ultrasonic sensors, IMUs, GNSS receivers, encoders, force sensors, and other devices generate data with different rates, bandwidths, formats, and timing characteristics. The electrical architecture must provide suitable physical interfaces, synchronization mechanisms, power distribution, grounding, and communication bandwidth so that AI software receives reliable observations.

High-bandwidth sensors are commonly connected through interfaces such as Ethernet, automotive Ethernet, MIPI, USB, or dedicated high-speed links. Lower-bandwidth control and status information may use CAN, CAN FD, CANopen, EtherCAT, RS-485, or similar networks depending on the robot architecture. Edge AI integration therefore requires communication architecture to be designed according to latency, determinism, bandwidth, fault containment, and physical implementation requirements.

The edge computer converts sensor information into increasingly meaningful representations. Raw measurements may first pass through signal conditioning, synchronization, calibration, preprocessing, and sensor fusion before entering neural networks or other perception algorithms. AI models can then generate objects, free-space estimates, semantic information, terrain representations, localization features, occupancy information, or other machine-readable descriptions of the surrounding environment.

Perception results become inputs to higher-level reasoning and planning functions. Depending on the system, the edge AI computer may estimate trajectories, predict environmental changes, evaluate possible actions, generate navigation paths, or calculate motion commands. These outputs should normally be expressed through controlled interfaces rather than allowing an AI model to directly manipulate power electronics or actuator signals without an intermediate control layer.

The interface between AI computation and deterministic control is therefore a critical architectural boundary. High-level outputs such as target velocity, steering request, waypoint, trajectory, joint target, or behavioral mode can be transferred to the real-time controller. The controller then converts these commands into precisely timed actuator operations while enforcing limits associated with velocity, acceleration, torque, current, position, and machine safety.

This layered approach also supports graceful degradation. If an AI workload becomes overloaded, a neural network fails, or the edge computer temporarily loses a sensor stream, the underlying controller can retain essential deterministic functions. Depending on the application, the system may reduce speed, hold position, enter a predefined fallback state, request remote assistance, or perform a controlled stop rather than allowing computational failure to propagate directly to actuators.

Electrical integration must account for the substantial power demand of modern AI processors. GPUs, NPUs, CPUs, memory, storage, and high-speed networking can create rapidly changing electrical loads and significant thermal dissipation. The power architecture must therefore consider converter capacity, transient response, voltage stability, startup sequencing, protection, grounding, cooling, and the interaction between AI computing loads and motors or other high-current equipment.

Thermal design is particularly important because inference performance can change when processors reach thermal or power limits. An edge computer capable of high peak AI performance may deliver substantially lower sustained performance if cooling is insufficient. Electrical and mechanical architecture must consequently treat compute power, cooling capacity, enclosure design, environmental temperature, airflow, and sustained AI workload as parts of the same engineering problem.

Data movement can consume significant system resources independently of neural-network computation. Multiple high-resolution cameras and 3D sensors may generate far more raw information than the AI algorithms ultimately require. Efficient edge architectures reduce unnecessary copying, use hardware acceleration where appropriate, manage memory bandwidth carefully, and process sensor information close to its acquisition path before forwarding compact representations to other controllers.

Time synchronization is equally important for Physical AI. Sensor measurements generated at different moments can create incorrect spatial or dynamic interpretations even when every individual sensor is accurate. Hardware timestamps, synchronized clocks, deterministic acquisition, and carefully defined latency budgets allow the edge computer to associate camera images, point clouds, inertial measurements, encoder states, and control information with a consistent representation of system time.

Edge AI also changes the role of the robot communication network. The network no longer carries only commands and diagnostic signals; it becomes part of the perception-to-action information pipeline. High-bandwidth Ethernet networks can transport sensor and AI data, while deterministic buses can maintain actuator control. Gateways or compute nodes may bridge these domains while controlling traffic priority, timing, security, and fault propagation.

Functional safety should remain architecturally distinguishable from probabilistic AI behavior. Safety controllers, emergency-stop circuits, safe torque off, protective sensors, and deterministic safety logic should retain authority over hazardous motion where required. AI can provide rich environmental understanding and operational decisions, but safety mechanisms must be capable of restricting or overriding AI-generated commands when predefined safety conditions are violated.

Cybersecurity becomes more important as edge computers introduce operating systems, middleware, neural-network runtimes, storage, Ethernet connectivity, and software update mechanisms into the robot. Secure boot, authenticated software, access control, network segmentation, encrypted communication where appropriate, logging, and controlled update procedures help prevent the intelligence layer from becoming an uncontrolled path into safety-critical or motion-control electronics.

Edge AI integration also provides a foundation for local autonomy when external connectivity is unreliable. The robot can continue perception, localization, planning, and essential decision making without depending on cloud round trips. Cloud or on-premise systems can instead support model distribution, fleet learning, large-scale analytics, data management, simulation, and computationally expensive training while operational inference remains close to the physical machine.

The boundary between edge device and edge AI computer should be defined explicitly. A compact controller near motors and actuators can maintain fast local control, while a GPU-class edge computer handles computationally intensive intelligence. Ethernet can connect the higher-level compute domain, while CAN, CANopen, EtherCAT, or other deterministic networks connect lower-level devices according to application requirements. This creates a hierarchical compute and communication structure.

Such hierarchy makes Physical AI fundamentally different from simply installing a GPU inside a robot. Successful integration requires coordinated design of sensors, compute hardware, networks, power distribution, thermal management, timing, control interfaces, safety mechanisms, and software deployment. The electrical architecture determines whether AI outputs can reach the physical system with sufficient reliability, latency, bandwidth, and operational predictability.

Scalability should also be considered from the beginning. Additional cameras, manipulators, accelerators, communication interfaces, or AI models can increase power, bandwidth, thermal load, and timing complexity. Modular compute interfaces, standardized communication boundaries, reserved power capacity, expandable networking, and clearly separated control responsibilities allow the architecture to evolve without requiring a complete redesign whenever intelligence capability increases.

Ultimately, Edge AI integration establishes the bridge between digital intelligence and physical action. Sensors observe the environment, edge computing transforms observations into useful representations and decisions, deterministic controllers convert decisions into precisely timed commands, and actuators interact with the physical world. The resulting feedback continuously returns new sensor information, forming the electrical and computational foundation for increasingly autonomous Physical AI systems.

엣지 AI 통합(Edge AI Integration)은 인공지능(Artificial Intelligence) 연산을 센서(Sensor), 액추에이터(Actuator), 실시간 제어기(Real-Time Controller)와 가까운 물리 시스템 내부에 직접 배치하는 것을 의미한다. 피지컬 AI 전기 아키텍처(Physical AI Electrical Architecture)에서 엣지 컴퓨팅 계층(Edge Computing Layer)은 기존 로봇 제어 전자장치와 인지(Perception), 학습(Learning), 의사결정(Decision) 기능을 연결하며, 원격 클라우드 인프라(Cloud Infrastructure)에 지속적으로 의존하지 않고도 시스템을 동작시킬 수 있게 한다.

실용적인 아키텍처에서는 결정론적 기계 제어(Deterministic Machine Control)와 계산량이 많은 AI 처리(AI Processing)를 분리한다. 모터 제어(Motor Control), 서보 루프(Servo Loop), 비상 처리(Emergency Handling), 기본 모션 기능(Motion Function)은 MCU, 전용 제어기(Dedicated Controller), 실시간 프로세서(Real-Time Processor)에 유지하고, 엣지 AI 컴퓨터(Edge AI Computer)는 인지, 위치추정(Localization), 예측(Prediction), 계획(Planning), 상위 수준 의사결정 알고리즘을 실행한다. 이러한 분리는 예측 가능한 제어 타이밍을 유지하면서 고급 지능 기능을 가능하게 한다.

이러한 시스템은 일반적으로 서로 다른 여러 처리 주기(Processing Rate)에서 동작한다. 모터 제어기는 수 kHz 수준으로 전류(Current) 또는 토크(Torque)를 제어할 수 있고, 로봇 제어기(Robot Controller)는 수백 Hz 수준으로 궤적(Trajectory)과 모션을 제어할 수 있다. 카메라(Camera)나 라이다(LiDAR) 기반 인지는 초당 수십 프레임으로 동작하며, 복잡한 AI 계획은 이보다 느리게 수행될 수 있다. 따라서 엣지 통합은 모든 서브시스템을 하나의 실행 주기로 강제하지 않고 비동기 정보(Asynchronous Information)를 조정해야 한다.

센서(Sensor)는 엣지 AI 플랫폼(Edge AI Platform)의 주요 입력 경계를 형성한다. 카메라, 라이다, 레이더(Radar), 초음파 센서(Ultrasonic Sensor), 관성측정장치(IMU), 위성항법장치(GNSS), 엔코더(Encoder), 힘 센서(Force Sensor) 등은 서로 다른 속도, 대역폭(Bandwidth), 데이터 형식, 타이밍 특성을 가진 정보를 생성한다. 전기 아키텍처는 AI 소프트웨어가 신뢰할 수 있는 관측 정보를 받을 수 있도록 적절한 물리 인터페이스, 동기화(Synchronization), 전력 분배(Power Distribution), 접지(Grounding), 통신 대역폭을 제공해야 한다.

고대역폭 센서는 일반적으로 이더넷(Ethernet), 자동차 이더넷(Automotive Ethernet), MIPI, USB 또는 전용 고속 링크(High-Speed Link)를 통해 연결된다. 낮은 대역폭의 제어 및 상태 정보에는 시스템 아키텍처에 따라 CAN, CAN FD, CANopen, EtherCAT, RS-485 등의 네트워크를 사용할 수 있다. 따라서 엣지 AI 통합에서는 지연시간(Latency), 결정성(Determinism), 대역폭, 고장 격리(Fault Containment), 물리적 구현 요구사항에 따라 통신 아키텍처를 설계해야 한다.

엣지 컴퓨터(Edge Computer)는 센서 정보를 점차 의미 있는 표현으로 변환한다. 원시 측정값(Raw Measurement)은 신호 조정(Signal Conditioning), 동기화, 보정(Calibration), 전처리(Preprocessing), 센서 융합(Sensor Fusion)을 거쳐 신경망(Neural Network) 또는 다른 인지 알고리즘에 입력될 수 있다. AI 모델은 객체(Object), 주행 가능 공간(Free Space), 의미 정보(Semantic Information), 지형 표현(Terrain Representation), 위치추정 특징, 점유 정보(Occupancy Information) 등 주변 환경을 기계가 이해할 수 있는 형태로 생성한다.

인지 결과(Perception Result)는 상위 수준의 추론(Reasoning)과 계획 기능의 입력이 된다. 시스템에 따라 엣지 AI 컴퓨터는 궤적을 추정하고, 환경 변화를 예측하며, 가능한 행동(Action)을 평가하고, 주행 경로(Navigation Path)를 생성하거나 모션 명령(Motion Command)을 계산할 수 있다. 이러한 출력은 AI 모델이 중간 제어 계층 없이 전력 전자장치(Power Electronics)나 액추에이터 신호를 직접 조작하도록 하기보다는 통제된 인터페이스를 통해 전달하는 것이 일반적이다.

따라서 AI 연산과 결정론적 제어 사이의 인터페이스는 핵심적인 아키텍처 경계(Architectural Boundary)가 된다. 목표 속도(Target Velocity), 조향 요청(Steering Request), 웨이포인트(Waypoint), 궤적, 관절 목표(Joint Target), 행동 모드(Behavioral Mode) 등의 상위 수준 출력이 실시간 제어기로 전달될 수 있다. 제어기는 이러한 명령을 정밀하게 타이밍된 액추에이터 동작으로 변환하면서 속도, 가속도, 토크, 전류, 위치 및 기계 안전과 관련된 제한 조건을 적용한다.

이러한 계층적 접근은 성능 저하 상태에서도 안전한 동작(Graceful Degradation)을 지원한다. AI 워크로드가 과부하되거나 신경망에 문제가 발생하거나 엣지 컴퓨터가 일시적으로 센서 스트림을 잃더라도 하위 제어기는 필수적인 결정론적 기능을 유지할 수 있다. 응용 분야에 따라 시스템은 속도를 낮추거나 위치를 유지하고, 사전에 정의된 폴백 상태(Fallback State)로 전환하거나 원격 지원(Remote Assistance)을 요청하고, 계산 오류가 액추에이터까지 직접 전파되는 대신 제어된 정지(Controlled Stop)를 수행할 수 있다.

전기적 통합에서는 최신 AI 프로세서가 요구하는 상당한 전력도 고려해야 한다. GPU, NPU, CPU, 메모리(Memory), 저장장치(Storage), 고속 네트워크는 빠르게 변화하는 전기 부하와 상당한 열을 발생시킬 수 있다. 따라서 전력 아키텍처(Power Architecture)는 컨버터 용량(Converter Capacity), 과도응답(Transient Response), 전압 안정성(Voltage Stability), 시동 순서(Startup Sequencing), 보호(Protection), 접지, 냉각(Cooling), 그리고 AI 컴퓨팅 부하와 모터 등 고전류 장치 사이의 상호작용을 고려해야 한다.

열 설계(Thermal Design)는 프로세서가 열 또는 전력 한계에 도달하면 추론 성능(Inference Performance)이 변할 수 있기 때문에 특히 중요하다. 높은 최대 AI 성능을 제공하는 엣지 컴퓨터라도 냉각이 충분하지 않으면 지속적으로 제공할 수 있는 성능이 크게 감소할 수 있다. 따라서 전기 및 기계 아키텍처는 컴퓨팅 전력, 냉각 용량, 인클로저 설계(Enclosure Design), 주변 온도, 공기 흐름(Airflow), 지속적인 AI 워크로드를 하나의 통합된 엔지니어링 문제로 다루어야 한다.

데이터 이동(Data Movement)은 신경망 연산 자체와 별개로 상당한 시스템 자원을 소비할 수 있다. 여러 고해상도 카메라와 3D 센서는 AI 알고리즘이 최종적으로 사용하는 양보다 훨씬 많은 원시 정보를 생성할 수 있다. 효율적인 엣지 아키텍처는 불필요한 데이터 복사를 줄이고, 필요한 경우 하드웨어 가속(Hardware Acceleration)을 사용하며, 메모리 대역폭을 효율적으로 관리하고, 센서 획득 경로 가까이에서 정보를 처리한 후 압축된 표현을 다른 제어기로 전달한다.

시간 동기화(Time Synchronization) 역시 피지컬 AI(Physical AI)에서 매우 중요하다. 서로 다른 시점에 생성된 센서 측정값은 각각의 센서가 정확하더라도 잘못된 공간적 또는 동적 해석을 만들 수 있다. 하드웨어 타임스탬프(Hardware Timestamp), 동기화된 클록(Synchronized Clock), 결정론적 데이터 획득, 명확하게 정의된 지연시간 예산(Latency Budget)을 사용하면 카메라 영상, 포인트 클라우드(Point Cloud), 관성 측정값, 엔코더 상태, 제어 정보를 일관된 시스템 시간 기준으로 결합할 수 있다.

엣지 AI는 로봇 통신 네트워크(Robot Communication Network)의 역할도 변화시킨다. 네트워크는 더 이상 명령과 진단 신호만 전달하는 것이 아니라 인지에서 행동으로 이어지는 정보 파이프라인(Perception-to-Action Information Pipeline)의 일부가 된다. 고대역폭 이더넷은 센서 및 AI 데이터를 전송하고, 결정론적 버스(Deterministic Bus)는 액추에이터 제어를 유지할 수 있다. 게이트웨이(Gateway) 또는 컴퓨팅 노드(Compute Node)는 트래픽 우선순위, 타이밍, 보안, 고장 전파를 관리하면서 이러한 영역을 연결할 수 있다.

기능 안전(Functional Safety)은 확률적 AI 동작(Probabilistic AI Behavior)과 아키텍처적으로 구분되어야 한다. 안전 제어기(Safety Controller), 비상 정지 회로(Emergency-Stop Circuit), 안전 토크 차단(Safe Torque Off), 보호 센서(Protective Sensor), 결정론적 안전 로직(Deterministic Safety Logic)은 필요한 경우 위험한 움직임에 대한 최종 제어 권한을 유지해야 한다. AI가 풍부한 환경 이해와 운용 의사결정을 제공하더라도 사전에 정의된 안전 조건을 위반하면 안전 메커니즘이 AI 명령을 제한하거나 무효화할 수 있어야 한다.

사이버보안(Cybersecurity)은 엣지 컴퓨터가 운영체제(Operating System), 미들웨어(Middleware), 신경망 런타임(Neural Network Runtime), 저장장치, 이더넷 연결, 소프트웨어 업데이트 기능을 로봇 내부에 도입하면서 더욱 중요해진다. 보안 부팅(Secure Boot), 인증된 소프트웨어, 접근 제어(Access Control), 네트워크 분할(Network Segmentation), 필요한 경우 암호화 통신, 로그 기록(Logging), 통제된 업데이트 절차를 통해 지능 계층이 안전 핵심 또는 모션 제어 전자장치로 접근하는 통제되지 않은 경로가 되는 것을 방지할 수 있다.

엣지 AI 통합은 외부 연결이 불안정한 환경에서도 로컬 자율성(Local Autonomy)을 유지할 수 있는 기반을 제공한다. 로봇은 클라우드 왕복 통신(Cloud Round Trip)에 의존하지 않고 인지, 위치추정, 계획 및 필수 의사결정을 계속 수행할 수 있다. 클라우드 또는 온프레미스 시스템(On-Premise System)은 모델 배포(Model Distribution), 플릿 학습(Fleet Learning), 대규모 분석, 데이터 관리, 시뮬레이션, 계산량이 큰 학습을 지원하고, 실제 운용을 위한 추론은 물리 시스템 가까이에서 수행하도록 구성할 수 있다.

엣지 디바이스(Edge Device)와 엣지 AI 컴퓨터(Edge AI Computer) 사이의 경계도 명확하게 정의해야 한다. 모터와 액추에이터 가까이에 있는 소형 제어기는 빠른 로컬 제어(Local Control)를 유지하고, GPU급 엣지 컴퓨터는 계산량이 많은 지능 기능을 담당할 수 있다. 상위 컴퓨팅 영역은 이더넷으로 연결하고, 하위 장치는 응용 요구사항에 따라 CAN, CANopen, EtherCAT 등의 결정론적 네트워크로 연결함으로써 계층적 컴퓨팅 및 통신 구조를 구성할 수 있다.

이러한 계층 구조는 피지컬 AI가 단순히 로봇 내부에 GPU를 설치하는 것과 근본적으로 다르다는 점을 보여준다. 성공적인 통합을 위해서는 센서, 컴퓨팅 하드웨어, 네트워크, 전력 분배, 열 관리, 타이밍, 제어 인터페이스, 안전 메커니즘, 소프트웨어 배포를 함께 설계해야 한다. 전기 아키텍처는 AI 출력이 충분한 신뢰성, 지연시간, 대역폭 및 운용 예측성을 가지고 물리 시스템에 전달될 수 있는지를 결정한다.

처음부터 확장성(Scalability)도 고려해야 한다. 추가 카메라, 매니퓰레이터(Manipulator), 가속기(Accelerator), 통신 인터페이스 또는 AI 모델은 전력, 대역폭, 열 부하 및 타이밍 복잡도를 증가시킬 수 있다. 모듈형 컴퓨팅 인터페이스(Modular Compute Interface), 표준화된 통신 경계, 예비 전력 용량, 확장 가능한 네트워크, 명확하게 분리된 제어 책임을 적용하면 지능 기능이 증가할 때마다 전체 아키텍처를 다시 설계하지 않고도 시스템을 발전시킬 수 있다.

궁극적으로 엣지 AI 통합(Edge AI Integration)은 디지털 지능(Digital Intelligence)과 물리적 행동(Physical Action)을 연결하는 핵심 다리를 형성한다. 센서는 환경을 관측하고, 엣지 컴퓨팅은 관측 정보를 유용한 표현과 의사결정으로 변환하며, 결정론적 제어기는 이러한 결정을 정밀한 시간 기반 명령으로 변환하고, 액추에이터는 물리 세계와 상호작용한다. 그 결과 새로운 센서 정보가 지속적으로 피드백되어 점점 더 높은 자율성을 갖는 피지컬 AI 시스템의 전기적·계산적 기반을 형성한다.

##  

## 05.02. Sensor Compute Actuator Pipeline

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

The sensor-compute-actuator pipeline defines the fundamental information and control flow through which a Physical AI system observes its environment, interprets physical conditions, makes decisions, and produces actions. Within the Physical AI electrical architecture, this pipeline connects sensing hardware, computing resources, communication networks, real-time controllers, and actuators into a continuous closed-loop system.

The pipeline begins with sensors that convert physical phenomena into electrical or digital information. Cameras capture visual appearance, LiDAR measures three-dimensional geometry, radar estimates range and velocity, IMUs measure acceleration and angular motion, encoders observe joint or wheel position, and force or torque sensors measure mechanical interaction. Each sensor provides a different view of the robot and its surroundings.

Sensor signals must pass through an acquisition layer before they become useful computational inputs. Depending on the sensor, this layer may include analog conditioning, analog-to-digital conversion, packet reception, timestamp generation, buffering, calibration, filtering, and synchronization. The objective is not merely to collect data, but to preserve measurement quality and temporal relationships required for reliable perception and control.

Different sensors operate at different sampling frequencies and produce dramatically different data volumes. Encoders and inertial sensors may generate measurements at hundreds or thousands of hertz, while cameras commonly provide images at tens of frames per second. LiDAR and radar operate according to their own scanning cycles. The architecture must therefore manage asynchronous streams without assuming that every measurement arrives simultaneously.

Time synchronization provides the common temporal reference required to combine these streams. Hardware timestamps, synchronized clocks, trigger signals, Precision Time Protocol mechanisms, or equivalent techniques can associate measurements with their actual acquisition times. Without accurate timing, sensor fusion may combine observations representing different physical states, creating errors in localization, velocity estimation, mapping, prediction, or motion control.

After acquisition, sensor data enters the compute domain. Preprocessing operations can remove noise, compensate for calibration parameters, resize or normalize images, transform coordinate systems, filter point clouds, and convert raw packets into representations suitable for algorithms. Efficient preprocessing is important because unnecessary movement or duplication of high-bandwidth sensor data can consume memory bandwidth and increase end-to-end latency.

Sensor fusion combines complementary measurements into a more complete representation of the physical state. Camera information can provide semantic detail, LiDAR can provide accurate geometry, radar can contribute robust range and velocity information, and IMU or encoder measurements can provide rapid motion estimates. Fusion may occur at raw-data, feature, object, or state level depending on computational resources and application requirements.

The perception stage converts processed sensor information into representations that are useful for autonomous behavior. Typical outputs include detected objects, semantic regions, depth estimates, free space, occupancy maps, terrain characteristics, robot pose, landmarks, obstacles, and tracked dynamic objects. These representations reduce large quantities of raw sensor information into structured information that downstream decision functions can use efficiently.

The compute layer may contain heterogeneous processing devices because different workloads have different computational characteristics. CPUs are effective for general-purpose logic and system management, GPUs provide highly parallel processing for neural networks and vision, NPUs or dedicated AI accelerators can improve inference efficiency, and MCUs or real-time processors provide deterministic execution for time-critical functions. The pipeline coordinates these resources rather than treating them as interchangeable.

Once the current environment and robot state have been estimated, reasoning and planning functions determine the desired behavior. Navigation software may select a path around obstacles, a manipulator planner may generate a collision-free joint trajectory, or an autonomous vehicle planner may determine target velocity and steering behavior. AI models can contribute prediction and decision capabilities while conventional algorithms enforce geometric, dynamic, or operational constraints.

Planning outputs normally represent desired behavior rather than direct electrical actuator commands. Examples include target position, velocity, acceleration, steering angle, trajectory, joint configuration, torque request, or operating mode. This separation establishes an important boundary between higher-level computation and lower-level deterministic control, allowing AI decisions to be validated and constrained before they influence physical hardware.

The real-time control layer converts these higher-level requests into commands that actuators can execute. Motion controllers compare desired states with measured states and calculate appropriate control outputs using feedback algorithms. Position, velocity, torque, and current loops may operate at progressively faster rates as computation moves closer to the actuator, allowing the physical system to respond rapidly even when high-level AI decisions are generated more slowly.

For example, an edge computer may update a desired trajectory at tens of hertz while a robot controller tracks that trajectory at hundreds of hertz. A motor controller can simultaneously regulate current or torque at kilohertz rates. The pipeline therefore behaves as a hierarchy of nested control loops rather than a single sequential program, with each layer operating according to the timing requirements of its physical responsibility.

Communication networks connect the pipeline stages and must be selected according to their traffic characteristics. High-resolution cameras and LiDAR may require Ethernet or other high-bandwidth interfaces, while motor controllers and distributed I/O may use CAN, CAN FD, CANopen, EtherCAT, or similar control networks. The electrical architecture must prevent heavy sensor traffic from interfering with time-critical actuator communication.

The actuator stage transforms electrical commands into physical effects. Motors generate rotational or linear motion, steering actuators change direction, brakes generate stopping forces, robotic joints position links, and grippers interact with objects. Power electronics such as inverters, servo amplifiers, and motor drivers translate low-power control signals into the voltage and current required by the mechanical system.

Actuation immediately changes the physical state observed by the sensors, closing the feedback loop. Wheel rotation changes encoder measurements, steering modifies vehicle motion, manipulator movement changes camera geometry, and interaction forces appear in force sensors. The next sensing cycle therefore contains the consequences of the previous command, allowing the controller and AI system to continuously evaluate and correct their behavior.

Latency must be considered across the entire sensor-to-actuator path rather than at individual components alone. Sensor exposure, communication, buffering, preprocessing, inference, planning, network transmission, controller execution, and actuator response all contribute to end-to-end delay. Excessive or unpredictable latency can cause decisions to be based on outdated states and may reduce stability, tracking accuracy, or operational safety.

Reliability requires fault handling throughout the pipeline. Missing sensor frames, corrupted packets, communication timeout, compute overload, invalid AI outputs, controller faults, and actuator failures should be detected as close as practical to their source. Health monitoring and diagnostic information can propagate through the architecture so that higher layers understand when data or control capability has degraded.

Safety supervision operates alongside the normal pipeline rather than depending entirely on it. Emergency-stop circuits, safety sensors, safety controllers, motion limits, watchdogs, and safe torque off mechanisms can restrict or disable actuator commands when hazardous conditions occur. This ensures that failures in perception, AI reasoning, networking, or general-purpose computing do not automatically remove the system\'s final protective mechanisms.

Power distribution is another physical dependency spanning every pipeline stage. Sensors require stable low-noise supplies, compute platforms can create large dynamic loads, communication devices require reliable rails, and actuators may demand high transient current. Proper power-domain separation, grounding, protection, conversion, and sequencing prevent actuator disturbances or compute transients from degrading sensor measurements and control electronics.

A well-designed pipeline also supports modularity. Sensors can be upgraded without redesigning motor control, AI computers can evolve independently from actuator electronics, and control devices can be replaced while preserving defined command and feedback interfaces. Standardized electrical, communication, timing, and software boundaries make it possible to scale the architecture from simple mobile robots to complex autonomous machines.

The sensor-compute-actuator pipeline is therefore more than a linear chain of components. It is a multi-rate, closed-loop architecture in which sensing provides evidence about the physical world, computing transforms that evidence into state and intent, deterministic controllers translate intent into precisely timed commands, and actuators change the environment. Feedback continuously reconnects physical action with digital intelligence.

For Physical AI, the quality of this pipeline determines how effectively intelligence becomes physical behavior. High-performance AI models alone cannot provide reliable autonomy if sensor timing is inconsistent, communication is congested, control interfaces are poorly defined, power is unstable, or actuator response is unpredictable. Coordinated electrical and computational design transforms perception, reasoning, control, and physical action into one integrated autonomous system.

센서-컴퓨팅-액추에이터 파이프라인(Sensor-Compute-Actuator Pipeline)은 피지컬 AI 시스템(Physical AI System)이 환경을 관측하고, 물리적 상태를 해석하며, 의사결정을 수행하고, 실제 행동을 생성하는 기본적인 정보 및 제어 흐름을 정의한다. 피지컬 AI 전기 아키텍처(Physical AI Electrical Architecture)에서 이 파이프라인은 센싱 하드웨어(Sensing Hardware), 컴퓨팅 자원(Computing Resources), 통신 네트워크(Communication Networks), 실시간 제어기(Real-Time Controllers), 액추에이터(Actuators)를 하나의 연속적인 폐루프 시스템(Closed-Loop System)으로 연결한다.

파이프라인은 물리적 현상을 전기적 또는 디지털 정보로 변환하는 센서(Sensor)에서 시작한다. 카메라(Camera)는 시각적 정보를 획득하고, 라이다(LiDAR)는 3차원 기하 구조를 측정하며, 레이더(Radar)는 거리와 속도를 추정한다. 관성측정장치(IMU)는 가속도와 각운동을 측정하고, 엔코더(Encoder)는 관절이나 바퀴의 위치를 관측하며, 힘 또는 토크 센서(Force/Torque Sensor)는 기계적 상호작용을 측정한다. 각각의 센서는 로봇과 주변 환경에 대한 서로 다른 관점을 제공한다.

센서 신호는 유용한 컴퓨팅 입력으로 사용되기 전에 데이터 획득 계층(Acquisition Layer)을 통과해야 한다. 센서 종류에 따라 이 계층에는 아날로그 신호 조정(Analog Conditioning), 아날로그-디지털 변환(Analog-to-Digital Conversion), 패킷 수신(Packet Reception), 타임스탬프 생성(Timestamp Generation), 버퍼링(Buffering), 보정(Calibration), 필터링(Filtering), 동기화(Synchronization)가 포함될 수 있다. 목적은 단순한 데이터 수집이 아니라 신뢰성 있는 인지와 제어에 필요한 측정 품질과 시간적 관계를 유지하는 것이다.

서로 다른 센서는 서로 다른 샘플링 주파수(Sampling Frequency)로 동작하며 데이터 양에도 큰 차이가 있다. 엔코더와 관성 센서는 초당 수백 또는 수천 번의 측정값을 생성할 수 있지만, 카메라는 일반적으로 초당 수십 프레임의 영상을 제공한다. 라이다와 레이더 역시 각각 고유한 스캔 주기(Scanning Cycle)에 따라 동작한다. 따라서 아키텍처는 모든 측정값이 동시에 도착한다고 가정하지 않고 비동기 데이터 스트림(Asynchronous Data Stream)을 관리해야 한다.

시간 동기화(Time Synchronization)는 이러한 데이터 스트림을 결합하기 위한 공통 시간 기준을 제공한다. 하드웨어 타임스탬프(Hardware Timestamp), 동기화된 클록(Synchronized Clock), 트리거 신호(Trigger Signal), 정밀 시간 프로토콜(Precision Time Protocol) 또는 이에 상응하는 기술을 이용하여 측정값을 실제 획득 시점과 연결할 수 있다. 정확한 타이밍이 없으면 센서 융합(Sensor Fusion)이 서로 다른 물리 상태를 나타내는 관측값을 결합하여 위치추정, 속도 추정, 매핑(Mapping), 예측, 모션 제어에 오류를 발생시킬 수 있다.

데이터 획득 이후 센서 데이터는 컴퓨팅 영역(Compute Domain)으로 전달된다. 전처리(Preprocessing)는 잡음을 제거하고, 보정 파라미터를 적용하며, 이미지를 크기 조정하거나 정규화하고, 좌표계를 변환하며, 포인트 클라우드(Point Cloud)를 필터링하고, 원시 패킷을 알고리즘에 적합한 표현으로 변환할 수 있다. 불필요한 고대역폭 센서 데이터의 이동이나 복제는 메모리 대역폭을 소비하고 전체 지연시간을 증가시키므로 효율적인 전처리가 중요하다.

센서 융합(Sensor Fusion)은 상호 보완적인 측정값을 결합하여 물리적 상태에 대한 보다 완전한 표현을 생성한다. 카메라 정보는 의미적 세부정보(Semantic Detail)를 제공하고, 라이다는 정확한 기하 정보를 제공하며, 레이더는 강건한 거리 및 속도 정보를 제공할 수 있다. IMU 또는 엔코더 측정값은 빠른 운동 추정(Motion Estimation)을 제공한다. 융합은 컴퓨팅 자원과 응용 요구사항에 따라 원시 데이터, 특징(Feature), 객체(Object), 상태(State) 수준에서 수행될 수 있다.

인지 단계(Perception Stage)는 처리된 센서 정보를 자율 행동에 유용한 표현으로 변환한다. 일반적인 출력에는 검출된 객체, 의미 영역(Semantic Region), 깊이 추정(Depth Estimation), 자유 공간(Free Space), 점유 지도(Occupancy Map), 지형 특성(Terrain Characteristics), 로봇 자세(Robot Pose), 랜드마크(Landmark), 장애물, 추적된 동적 객체(Tracked Dynamic Object) 등이 포함된다. 이러한 표현은 대량의 원시 센서 정보를 하위 의사결정 기능이 효율적으로 사용할 수 있는 구조화된 정보로 축약한다.

컴퓨팅 계층(Compute Layer)은 각 작업이 서로 다른 계산 특성을 가지므로 이기종 처리 장치(Heterogeneous Processing Device)로 구성될 수 있다. CPU는 범용 로직과 시스템 관리에 적합하고, GPU는 신경망과 비전 처리를 위한 대규모 병렬 연산을 제공하며, NPU 또는 전용 AI 가속기(AI Accelerator)는 추론 효율을 향상시킬 수 있다. MCU 또는 실시간 프로세서(Real-Time Processor)는 시간에 민감한 기능을 위한 결정론적 실행(Deterministic Execution)을 제공한다. 파이프라인은 이러한 자원을 동일한 장치로 취급하지 않고 역할에 따라 조정한다.

현재 환경과 로봇 상태가 추정되면 추론(Reasoning) 및 계획(Planning) 기능이 원하는 행동을 결정한다. 내비게이션 소프트웨어(Navigation Software)는 장애물을 회피하는 경로를 선택하고, 매니퓰레이터 플래너(Manipulator Planner)는 충돌 없는 관절 궤적을 생성하며, 자율주행 차량의 플래너는 목표 속도와 조향 행동을 결정할 수 있다. AI 모델은 예측과 의사결정 기능을 제공하고, 기존 알고리즘은 기하학적, 동역학적 또는 운용상의 제약조건을 적용할 수 있다.

계획 출력(Planning Output)은 일반적으로 직접적인 전기적 액추에이터 명령이 아니라 원하는 행동을 표현한다. 대표적인 예로 목표 위치(Target Position), 속도(Velocity), 가속도(Acceleration), 조향각(Steering Angle), 궤적(Trajectory), 관절 구성(Joint Configuration), 토크 요청(Torque Request), 운용 모드(Operating Mode)가 있다. 이러한 분리는 상위 수준 컴퓨팅과 하위 수준 결정론적 제어 사이에 중요한 경계를 형성하며, AI의 의사결정이 실제 하드웨어에 영향을 주기 전에 검증되고 제한될 수 있도록 한다.

실시간 제어 계층(Real-Time Control Layer)은 이러한 상위 수준 요청을 액추에이터가 실행할 수 있는 명령으로 변환한다. 모션 제어기(Motion Controller)는 목표 상태와 측정된 상태를 비교하고 피드백 알고리즘(Feedback Algorithm)을 사용하여 적절한 제어 출력을 계산한다. 위치, 속도, 토크, 전류 제어 루프(Control Loop)는 연산이 액추에이터에 가까워질수록 점차 빠른 주기로 동작할 수 있으며, 이를 통해 상위 AI 의사결정이 느리게 생성되더라도 물리 시스템은 빠르게 반응할 수 있다.

예를 들어 엣지 컴퓨터(Edge Computer)는 초당 수십 회 수준으로 목표 궤적을 업데이트하는 반면, 로봇 제어기(Robot Controller)는 수백 Hz 수준으로 해당 궤적을 추종할 수 있다. 동시에 모터 제어기(Motor Controller)는 수 kHz 수준에서 전류 또는 토크를 제어할 수 있다. 따라서 파이프라인은 하나의 순차적인 프로그램이라기보다 여러 계층의 중첩된 제어 루프(Nested Control Loops)로 동작하며, 각 계층은 자신이 담당하는 물리적 기능의 타이밍 요구사항에 따라 실행된다.

통신 네트워크(Communication Network)는 파이프라인의 각 단계를 연결하며 전송되는 데이터의 특성에 따라 선택해야 한다. 고해상도 카메라와 라이다는 이더넷(Ethernet) 또는 기타 고대역폭 인터페이스(High-Bandwidth Interface)를 필요로 할 수 있으며, 모터 제어기와 분산 입출력(Distributed I/O)은 CAN, CAN FD, CANopen, EtherCAT 또는 유사한 제어 네트워크를 사용할 수 있다. 전기 아키텍처는 대용량 센서 트래픽이 시간에 민감한 액추에이터 통신을 방해하지 않도록 설계되어야 한다.

액추에이터 단계(Actuator Stage)는 전기 명령을 실제 물리적 효과로 변환한다. 모터(Motor)는 회전 또는 직선 운동을 생성하고, 조향 액추에이터(Steering Actuator)는 이동 방향을 변경하며, 브레이크(Brake)는 정지력을 발생시킨다. 로봇 관절(Robotic Joint)은 링크를 원하는 위치로 이동시키고, 그리퍼(Gripper)는 객체와 상호작용한다. 인버터(Inverter), 서보 앰프(Servo Amplifier), 모터 드라이버(Motor Driver) 등의 전력 전자장치는 저전력 제어 신호를 기계 시스템에 필요한 전압과 전류로 변환한다.

액추에이터의 동작은 센서가 관측하는 물리적 상태를 즉시 변화시키면서 피드백 루프(Feedback Loop)를 완성한다. 바퀴 회전은 엔코더 측정값을 변화시키고, 조향은 차량 운동을 변화시키며, 매니퓰레이터의 움직임은 카메라의 기하학적 관계를 변화시킨다. 또한 물체와의 상호작용으로 발생한 힘은 힘 센서에 나타난다. 따라서 다음 센싱 주기에는 이전 명령의 결과가 포함되며, 제어기와 AI 시스템은 자신의 행동을 지속적으로 평가하고 수정할 수 있다.

지연시간(Latency)은 개별 구성요소만이 아니라 전체 센서-액추에이터 경로(Sensor-to-Actuator Path)를 기준으로 고려해야 한다. 센서 노출(Sensor Exposure), 통신, 버퍼링, 전처리, 추론(Inference), 계획, 네트워크 전송, 제어기 실행, 액추에이터 응답이 모두 종단간 지연시간(End-to-End Latency)에 영향을 준다. 지나치거나 예측할 수 없는 지연은 오래된 상태 정보를 기반으로 의사결정을 수행하게 만들어 안정성, 추종 정확도 또는 운용 안전성을 저하시킬 수 있다.

신뢰성(Reliability)을 확보하려면 파이프라인 전체에서 고장 처리(Fault Handling)가 이루어져야 한다. 센서 프레임 손실, 손상된 패킷, 통신 타임아웃(Communication Timeout), 컴퓨팅 과부하, 잘못된 AI 출력, 제어기 고장, 액추에이터 고장 등을 가능한 한 발생 위치 가까이에서 감지해야 한다. 상태 모니터링(Health Monitoring)과 진단 정보(Diagnostic Information)는 아키텍처를 통해 전달되어 상위 계층이 데이터 또는 제어 능력이 저하되었는지를 판단할 수 있도록 한다.

안전 감독(Safety Supervision)은 정상적인 파이프라인에 완전히 의존하지 않고 병렬적으로 동작한다. 비상 정지 회로(Emergency-Stop Circuit), 안전 센서(Safety Sensor), 안전 제어기(Safety Controller), 모션 제한(Motion Limit), 워치독(Watchdog), 안전 토크 차단(Safe Torque Off) 메커니즘은 위험한 상황이 발생할 경우 액추에이터 명령을 제한하거나 비활성화할 수 있다. 이를 통해 인지, AI 추론, 네트워크 또는 범용 컴퓨팅에 장애가 발생하더라도 시스템의 최종 보호 기능을 유지할 수 있다.

전력 분배(Power Distribution)는 파이프라인의 모든 단계에 걸쳐 존재하는 또 하나의 물리적 의존 요소이다. 센서는 안정적이고 노이즈가 적은 전원을 필요로 하고, 컴퓨팅 플랫폼은 큰 동적 부하(Dynamic Load)를 발생시킬 수 있으며, 통신 장치는 안정적인 전원 레일(Power Rail)을 필요로 한다. 액추에이터는 순간적으로 매우 높은 전류를 요구할 수 있다. 적절한 전력 영역 분리, 접지, 보호, 전력 변환 및 시퀀싱(Sequencing)을 통해 액추에이터의 전기적 교란이나 컴퓨팅 부하 변화가 센서 측정과 제어 전자장치에 영향을 주는 것을 방지해야 한다.

잘 설계된 파이프라인은 모듈성(Modularity)도 지원한다. 모터 제어 시스템을 다시 설계하지 않고 센서를 업그레이드할 수 있고, 액추에이터 전자장치와 독립적으로 AI 컴퓨터를 발전시킬 수 있으며, 정의된 명령 및 피드백 인터페이스를 유지하면서 제어 장치를 교체할 수도 있다. 표준화된 전기, 통신, 타이밍 및 소프트웨어 경계는 단순한 이동 로봇부터 복잡한 자율 기계까지 아키텍처를 확장할 수 있도록 한다.

따라서 센서-컴퓨팅-액추에이터 파이프라인(Sensor-Compute-Actuator Pipeline)은 단순한 구성요소의 선형적인 연결이 아니다. 이것은 센싱(Sensing)이 물리 세계에 대한 증거를 제공하고, 컴퓨팅(Computing)이 그 증거를 상태와 의도(Intent)로 변환하며, 결정론적 제어기(Deterministic Controller)가 의도를 정밀한 시간 기반 명령으로 변환하고, 액추에이터가 환경을 변화시키는 다중 주기 폐루프 아키텍처(Multi-Rate Closed-Loop Architecture)이다. 피드백은 물리적 행동과 디지털 지능을 지속적으로 다시 연결한다.

피지컬 AI(Physical AI)에서 이 파이프라인의 품질은 지능이 실제 물리적 행동으로 얼마나 효과적으로 변환되는지를 결정한다. 센서 타이밍이 일관되지 않거나, 통신이 혼잡하거나, 제어 인터페이스가 명확하지 않거나, 전력이 불안정하거나, 액추에이터 응답을 예측할 수 없다면 고성능 AI 모델만으로는 신뢰할 수 있는 자율성을 구현할 수 없다. 전기 시스템과 컴퓨팅 시스템을 통합적으로 설계함으로써 인지, 추론, 제어, 물리적 행동을 하나의 완전한 자율 시스템으로 연결할 수 있다.

##  

## 05.03. AI Native Architecture

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

An AI-native architecture treats artificial intelligence as a fundamental system capability rather than an optional application added after the electrical and computing architecture has been designed. In a Physical AI system, sensing, computation, communication, control, power, and safety are therefore organized from the beginning around continuous perception, inference, decision making, and interaction with the physical world.

Traditional robot architectures often begin with deterministic control functions and later attach AI processors to support perception or advanced autonomy. An AI-native design reverses this assumption by considering intelligent workloads during the initial architecture definition. Sensor bandwidth, accelerator capacity, memory movement, network latency, power consumption, thermal limits, and software deployment become first-order electrical design parameters.

The architecture still preserves deterministic control where physical timing requires it. AI-native does not mean that neural networks replace every controller, nor does it imply that probabilistic models should directly operate power electronics. Instead, AI computation and conventional control are assigned to appropriate layers, allowing perception and reasoning to evolve rapidly while motor, servo, protection, and safety functions retain predictable real-time behavior.

Sensing becomes an integrated information infrastructure rather than a collection of independent devices. Cameras, LiDAR, radar, IMUs, encoders, force sensors, and other sensing devices provide complementary observations that can be synchronized and fused. Their electrical interfaces, timestamps, bandwidth requirements, calibration information, and physical placement are designed according to the representations required by downstream AI models.

The compute architecture is inherently heterogeneous because Physical AI workloads contain different types of computation. CPUs can manage operating systems, middleware, planning logic, and general algorithms; GPUs can accelerate vision and neural-network processing; NPUs or dedicated accelerators can improve inference efficiency; and MCUs, DSPs, FPGAs, or real-time processors can execute deterministic or specialized functions close to sensors and actuators.

Memory architecture becomes as important as raw processor performance. High-resolution cameras and three-dimensional sensors can generate large continuous data streams, while modern AI models require substantial parameter, activation, and intermediate-data movement. Shared memory, high-speed interconnects, direct memory access, efficient buffering, and minimized data copying can significantly reduce latency and energy consumption across the AI processing pipeline.

Communication networks must support both data-intensive intelligence and deterministic machine control. Ethernet-class networks can carry images, point clouds, AI features, maps, logs, and software updates, while CAN, CAN FD, CANopen, EtherCAT, or similar networks can serve distributed controllers and actuators. Network segmentation and traffic prioritization prevent high-bandwidth AI data from disrupting time-critical control communication.

AI-native systems naturally operate as multi-rate architectures. Sensor acquisition, neural-network inference, world-state estimation, planning, trajectory generation, servo control, and motor-current regulation do not need to execute at the same frequency. A perception model may operate at tens of hertz while trajectory control operates at hundreds of hertz and current control at several kilohertz, with defined interfaces connecting these different temporal domains.

The intelligence pipeline transforms raw observations into increasingly abstract representations. Sensor data can be calibrated, synchronized, filtered, and fused before perception models identify objects, geometry, free space, terrain, motion, or semantic relationships. Higher layers can then construct state representations that summarize what exists around the machine, how the environment is changing, and which information is relevant to future action.

Reasoning and planning operate on these representations to generate intent. Depending on the machine, this may include selecting navigation goals, predicting object motion, evaluating traversability, coordinating manipulation, generating trajectories, or selecting behavioral modes. The architecture should expose explicit interfaces between AI-generated intent and execution so that commands can be checked against physical constraints before reaching lower-level controllers.

This separation creates an important control boundary. AI may determine where the robot should move or what action it should attempt, while deterministic controllers determine precisely how motors and actuators execute that request. Position, velocity, torque, and current loops remain close to the physical hardware, allowing fast feedback control to continue independently between successive AI inference or planning updates.

An AI-native architecture must also be designed for uncertainty. Neural-network outputs may contain confidence values, ambiguous classifications, incomplete observations, or predictions that become invalid as the environment changes. Instead of assuming every AI output is correct, downstream functions can evaluate confidence, consistency, freshness, operational limits, and alternative information before converting an AI decision into physical action.

Fault containment is especially important because an AI compute platform may host many functions simultaneously. Excessive processing load, memory exhaustion, software failure, corrupted input, communication loss, or accelerator malfunction should not automatically disable basic motion control or safety functions. Architectural partitioning allows essential controllers to maintain controlled operation or transition the machine into a predefined degraded or safe state.

Functional safety therefore remains an independent authority within the overall system. Emergency-stop circuits, safety controllers, protective sensing, safe torque off, watchdogs, and deterministic safety logic can supervise or override AI-generated commands. The AI layer can improve environmental awareness and operational intelligence, but safety mechanisms must remain capable of restricting physical behavior when hazardous conditions are detected.

Power architecture must be designed around dynamically changing compute demand as well as actuator demand. GPUs and accelerators can transition rapidly between idle and intensive inference states, while motors produce their own large transient loads. Power distribution units, DC/DC converters, voltage rails, protection devices, grounding, filtering, and energy-storage components must maintain stable operation across these interacting electrical load profiles.

Thermal architecture is closely coupled with AI performance. Accelerator frequency, inference throughput, memory performance, and model execution can be reduced when thermal limits are reached. Cooling should therefore be sized according to sustained workloads rather than only nominal or peak processor specifications. Temperature monitoring can also become part of system-level resource management, allowing workloads to adapt before thermal throttling affects autonomy.

Software deployment becomes part of the electrical architecture lifecycle because AI capability changes after hardware production. Models, inference runtimes, calibration data, middleware, and configuration parameters may require controlled updates. Secure boot, authenticated packages, version management, rollback mechanisms, diagnostics, and over-the-air or service-based updates allow intelligence to evolve while maintaining configuration traceability and operational integrity.

AI-native design also encourages modularity between hardware generations and model generations. A sensor may be replaced by a higher-resolution device, an accelerator may be upgraded, or a perception model may change without redesigning every actuator interface. Stable data contracts, communication interfaces, timing definitions, command boundaries, and power interfaces reduce coupling between rapidly evolving AI technology and longer-lived electromechanical hardware.

Local edge autonomy is a central characteristic of this architecture. Critical perception, planning, and control functions should remain available without continuous cloud connectivity when the application requires autonomous operation. On-premise or cloud infrastructure can provide large-scale training, fleet analytics, simulation, model management, and data aggregation, while edge computing performs latency-sensitive inference and decision making near the machine.

Data generated during operation can also support a continuous improvement cycle. Selected sensor observations, AI outputs, uncertainty information, failures, interventions, and performance metrics can be recorded and transferred to development infrastructure. These data can support model evaluation, retraining, simulation, validation, and subsequent deployment, connecting the electrical machine to an evolving AI engineering lifecycle.

Cybersecurity becomes essential because an AI-native robot contains interconnected computers, software-defined functions, stored models, network services, and update mechanisms. Authentication, network segmentation, encrypted communication where appropriate, access control, secure storage, logging, and trusted software execution protect both information and physical control paths from unauthorized manipulation.

Observability should therefore be designed into every major layer. Sensor health, communication latency, processor utilization, inference timing, memory consumption, temperatures, power conditions, controller status, actuator faults, and AI confidence can be monitored together. This allows engineers to determine whether degraded physical behavior originates from sensing, computation, networking, software, control, power, thermal conditions, or mechanical hardware.

Scalability is achieved by treating compute, communication, power, and software resources as coordinated architectural domains. Adding sensors or AI models affects not only processing capacity but also memory bandwidth, network traffic, thermal dissipation, electrical load, storage, synchronization, and validation requirements. Capacity margins and modular interfaces should therefore be planned before additional intelligence is introduced.

Ultimately, an AI-native architecture integrates intelligence into the fundamental structure of the physical machine. Sensors continuously observe the world, heterogeneous computers transform observations into representations and decisions, real-time controllers convert intent into deterministic execution, and actuators create physical change that is sensed again. Power, communication, safety, security, timing, and software lifecycle functions support this loop as inseparable architectural elements.

The defining characteristic of AI-native Physical AI is therefore not the presence of a powerful GPU or a large neural network. It is the coordinated co-design of electrical hardware, computing, sensing, communication, control, safety, power, and software around an intelligence-driven closed loop. This approach enables increasingly capable AI models to evolve while preserving the timing, reliability, controllability, and physical integrity required by real machines.

AI 네이티브 아키텍처(AI-Native Architecture)는 전기 및 컴퓨팅 아키텍처가 설계된 이후 인공지능(Artificial Intelligence)을 선택적으로 추가하는 응용 기능이 아니라, 처음부터 시스템의 핵심 역량으로 취급한다. 피지컬 AI 시스템(Physical AI System)에서는 센싱(Sensing), 컴퓨팅(Computing), 통신(Communication), 제어(Control), 전력(Power), 안전(Safety)이 물리 세계에 대한 지속적인 인지(Perception), 추론(Inference), 의사결정(Decision Making), 상호작용(Interaction)을 중심으로 구성된다.

전통적인 로봇 아키텍처(Traditional Robot Architecture)는 일반적으로 결정론적 제어 기능(Deterministic Control Function)을 먼저 구성하고 이후 인지 또는 고급 자율성을 지원하기 위해 AI 프로세서를 추가하는 방식으로 발전해 왔다. AI 네이티브 설계(AI-Native Design)는 이러한 접근을 전환하여 초기 아키텍처 정의 단계부터 지능형 워크로드(Intelligent Workload)를 고려한다. 센서 대역폭, 가속기 용량, 메모리 이동, 네트워크 지연시간, 전력 소비, 열적 한계, 소프트웨어 배포가 주요 전기 설계 파라미터가 된다.

이러한 아키텍처에서도 물리적인 타이밍이 요구되는 영역에는 결정론적 제어(Deterministic Control)가 유지된다. AI 네이티브라는 개념은 신경망(Neural Network)이 모든 제어기를 대체한다는 의미가 아니며, 확률적 모델(Probabilistic Model)이 전력 전자장치(Power Electronics)를 직접 제어해야 한다는 의미도 아니다. AI 연산과 기존 제어 기능을 적절한 계층에 배치함으로써 인지와 추론 기능은 빠르게 발전시키면서 모터, 서보, 보호, 안전 기능에서는 예측 가능한 실시간 동작을 유지할 수 있다.

센싱(Sensing)은 독립적인 장치들의 집합이 아니라 통합된 정보 인프라(Information Infrastructure)가 된다. 카메라(Camera), 라이다(LiDAR), 레이더(Radar), 관성측정장치(IMU), 엔코더(Encoder), 힘 센서(Force Sensor) 및 기타 센싱 장치는 서로 보완적인 관측 정보를 제공하며, 이러한 정보를 동기화하고 융합할 수 있다. 센서의 전기 인터페이스, 타임스탬프(Timestamp), 대역폭 요구사항, 보정 정보(Calibration Information), 물리적 배치는 하위 AI 모델이 요구하는 표현을 기준으로 설계된다.

피지컬 AI 워크로드는 서로 다른 계산 특성을 포함하기 때문에 컴퓨팅 아키텍처(Compute Architecture)는 본질적으로 이기종 구조(Heterogeneous Architecture)를 가진다. CPU는 운영체제, 미들웨어(Middleware), 계획 로직, 범용 알고리즘을 관리하고, GPU는 비전 및 신경망 처리를 가속한다. NPU 또는 전용 AI 가속기(AI Accelerator)는 추론 효율을 높이며, MCU, DSP, FPGA 또는 실시간 프로세서(Real-Time Processor)는 센서와 액추에이터 가까이에서 결정론적 또는 특수 목적 기능을 수행할 수 있다.

메모리 아키텍처(Memory Architecture)는 프로세서의 순수 연산 성능만큼 중요해진다. 고해상도 카메라와 3차원 센서는 대규모 연속 데이터 스트림을 생성할 수 있으며, 최신 AI 모델은 많은 파라미터(Parameter), 활성값(Activation), 중간 데이터의 이동을 요구한다. 공유 메모리(Shared Memory), 고속 인터커넥트(High-Speed Interconnect), 직접 메모리 접근(Direct Memory Access), 효율적인 버퍼링(Buffering), 데이터 복사 최소화는 AI 처리 파이프라인 전체의 지연시간과 에너지 소비를 크게 줄일 수 있다.

통신 네트워크(Communication Network)는 데이터 집약적인 지능 기능과 결정론적 기계 제어를 동시에 지원해야 한다. 이더넷(Ethernet) 계열 네트워크는 이미지, 포인트 클라우드(Point Cloud), AI 특징(Feature), 지도(Map), 로그(Log), 소프트웨어 업데이트를 전달할 수 있으며, CAN, CAN FD, CANopen, EtherCAT 등의 네트워크는 분산 제어기와 액추에이터를 연결할 수 있다. 네트워크 분할(Network Segmentation)과 트래픽 우선순위 지정(Traffic Prioritization)을 통해 고대역폭 AI 데이터가 시간에 민감한 제어 통신을 방해하지 않도록 해야 한다.

AI 네이티브 시스템은 자연스럽게 다중 주기 아키텍처(Multi-Rate Architecture)로 동작한다. 센서 데이터 획득, 신경망 추론, 월드 상태 추정(World-State Estimation), 계획, 궤적 생성, 서보 제어, 모터 전류 제어는 동일한 주파수로 실행될 필요가 없다. 인지 모델은 수십 Hz로 동작하고 궤적 제어는 수백 Hz, 전류 제어는 수 kHz로 동작할 수 있으며, 정의된 인터페이스가 서로 다른 시간 영역(Temporal Domain)을 연결한다.

지능 파이프라인(Intelligence Pipeline)은 원시 관측값을 점차 높은 수준의 추상적 표현으로 변환한다. 센서 데이터는 보정, 동기화, 필터링, 융합 과정을 거친 후 인지 모델을 통해 객체, 기하 구조, 자유 공간(Free Space), 지형(Terrain), 움직임(Motion), 의미적 관계(Semantic Relationship) 등으로 변환될 수 있다. 상위 계층은 이를 이용하여 기계 주변에 무엇이 존재하고 환경이 어떻게 변화하며 향후 행동에 어떤 정보가 중요한지를 요약하는 상태 표현(State Representation)을 구성한다.

추론(Reasoning)과 계획(Planning)은 이러한 표현을 기반으로 의도(Intent)를 생성한다. 기계의 종류에 따라 내비게이션 목표 선택, 객체 움직임 예측, 주행 가능성(Traversability) 평가, 매니퓰레이션(Manipulation) 조정, 궤적 생성, 행동 모드(Behavioral Mode) 선택 등이 포함될 수 있다. AI가 생성한 의도와 실제 실행 사이에는 명확한 인터페이스를 두어 명령이 하위 제어기에 도달하기 전에 물리적 제약조건을 기준으로 검증될 수 있도록 해야 한다.

이러한 분리는 중요한 제어 경계(Control Boundary)를 형성한다. AI는 로봇이 어디로 이동해야 하는지 또는 어떤 행동을 시도해야 하는지를 결정할 수 있지만, 모터와 액추에이터가 해당 요청을 정확히 어떻게 실행할지는 결정론적 제어기(Deterministic Controller)가 담당한다. 위치, 속도, 토크, 전류 제어 루프(Control Loop)는 물리적 하드웨어 가까이에 유지되며, 연속적인 AI 추론 또는 계획 업데이트 사이에서도 빠른 피드백 제어(Feedback Control)를 지속할 수 있다.

AI 네이티브 아키텍처는 불확실성(Uncertainty)을 고려하여 설계되어야 한다. 신경망 출력에는 신뢰도(Confidence), 모호한 분류, 불완전한 관측 또는 환경 변화로 인해 더 이상 유효하지 않은 예측이 포함될 수 있다. 따라서 모든 AI 출력을 항상 정확하다고 가정하는 대신 하위 기능에서 신뢰도, 일관성(Consistency), 정보의 최신성(Freshness), 운용 제한, 대체 정보를 평가한 후 AI 의사결정을 물리적 행동으로 변환할 수 있다.

AI 컴퓨팅 플랫폼이 여러 기능을 동시에 수행할 수 있기 때문에 고장 격리(Fault Containment)는 특히 중요하다. 과도한 처리 부하, 메모리 고갈, 소프트웨어 장애, 손상된 입력, 통신 손실 또는 가속기 고장이 기본적인 모션 제어나 안전 기능을 자동으로 중단시켜서는 안 된다. 아키텍처 분할(Architectural Partitioning)을 통해 필수 제어기는 제한된 운전을 유지하거나 기계를 사전에 정의된 성능 저하 상태(Degraded State) 또는 안전 상태(Safe State)로 전환할 수 있다.

따라서 기능 안전(Functional Safety)은 전체 시스템 내부에서 독립적인 제어 권한을 유지한다. 비상 정지 회로(Emergency-Stop Circuit), 안전 제어기(Safety Controller), 보호 센싱(Protective Sensing), 안전 토크 차단(Safe Torque Off), 워치독(Watchdog), 결정론적 안전 로직(Deterministic Safety Logic)은 AI가 생성한 명령을 감시하거나 무효화할 수 있다. AI 계층이 환경 인식과 운용 지능을 향상시키더라도 위험한 조건이 감지되면 안전 메커니즘이 물리적 행동을 제한할 수 있어야 한다.

전력 아키텍처(Power Architecture)는 액추에이터 부하뿐만 아니라 동적으로 변화하는 컴퓨팅 부하를 고려하여 설계해야 한다. GPU와 AI 가속기는 유휴 상태에서 고강도 추론 상태로 빠르게 전환될 수 있으며, 모터 역시 큰 과도 부하(Transient Load)를 발생시킨다. 전력분배장치(PDU), DC/DC 컨버터, 전압 레일(Voltage Rail), 보호 장치, 접지, 필터링, 에너지 저장장치는 서로 영향을 주는 이러한 전기 부하 조건에서도 안정적인 동작을 유지해야 한다.

열 아키텍처(Thermal Architecture)는 AI 성능과 밀접하게 연결된다. 가속기가 열적 한계에 도달하면 동작 주파수, 추론 처리량(Inference Throughput), 메모리 성능, 모델 실행 성능이 감소할 수 있다. 따라서 냉각 시스템(Cooling System)은 단순한 프로세서의 정격 또는 최대 사양이 아니라 지속적인 워크로드(Sustained Workload)를 기준으로 설계해야 한다. 온도 모니터링도 시스템 수준 자원 관리의 일부가 되어 열 스로틀링(Thermal Throttling)이 자율성에 영향을 주기 전에 워크로드를 조절할 수 있다.

AI 기능은 하드웨어 생산 이후에도 변화하기 때문에 소프트웨어 배포(Software Deployment)는 전기 아키텍처 수명주기(Electrical Architecture Lifecycle)의 일부가 된다. 모델, 추론 런타임(Inference Runtime), 보정 데이터, 미들웨어, 구성 파라미터는 통제된 방식으로 업데이트될 수 있어야 한다. 보안 부팅(Secure Boot), 인증된 패키지, 버전 관리(Version Management), 롤백(Rollback), 진단, 무선 업데이트(OTA) 또는 서비스 기반 업데이트를 통해 구성 추적성과 운용 무결성을 유지하면서 지능 기능을 발전시킬 수 있다.

AI 네이티브 설계는 하드웨어 세대와 AI 모델 세대 사이의 모듈성(Modularity)도 강화한다. 센서를 더 높은 해상도의 장치로 교체하거나, 가속기를 업그레이드하거나, 인지 모델을 변경하더라도 모든 액추에이터 인터페이스를 다시 설계할 필요가 없어야 한다. 안정적인 데이터 계약(Data Contract), 통신 인터페이스, 타이밍 정의, 명령 경계, 전력 인터페이스는 빠르게 발전하는 AI 기술과 상대적으로 긴 수명을 가지는 전기기계 하드웨어(Electromechanical Hardware) 사이의 결합도를 낮춘다.

로컬 엣지 자율성(Local Edge Autonomy)은 이러한 아키텍처의 핵심 특성이다. 응용 시스템이 자율 운전을 요구하는 경우 핵심적인 인지, 계획, 제어 기능은 지속적인 클라우드 연결 없이도 사용할 수 있어야 한다. 온프레미스(On-Premise) 또는 클라우드 인프라(Cloud Infrastructure)는 대규모 학습, 플릿 분석(Fleet Analytics), 시뮬레이션, 모델 관리, 데이터 집계를 담당하고, 엣지 컴퓨팅(Edge Computing)은 기계 가까이에서 지연시간에 민감한 추론과 의사결정을 수행할 수 있다.

운용 과정에서 생성되는 데이터는 지속적인 개선 사이클(Continuous Improvement Cycle)을 지원할 수도 있다. 선택된 센서 관측값, AI 출력, 불확실성 정보, 장애, 사람의 개입(Intervention), 성능 지표를 기록하여 개발 인프라로 전달할 수 있다. 이러한 데이터는 모델 평가, 재학습(Retraining), 시뮬레이션, 검증(Validation), 이후의 재배포에 활용되며, 전기적 기계를 지속적으로 발전하는 AI 엔지니어링 수명주기(AI Engineering Lifecycle)와 연결한다.

AI 네이티브 로봇에는 상호 연결된 컴퓨터, 소프트웨어 정의 기능(Software-Defined Function), 저장된 모델, 네트워크 서비스, 업데이트 메커니즘이 포함되므로 사이버보안(Cybersecurity)이 필수적이다. 인증(Authentication), 네트워크 분할, 필요한 경우 암호화 통신, 접근 제어(Access Control), 보안 저장장치(Secure Storage), 로깅(Logging), 신뢰할 수 있는 소프트웨어 실행(Trusted Software Execution)을 통해 정보와 물리적 제어 경로 모두를 승인되지 않은 조작으로부터 보호해야 한다.

따라서 관측 가능성(Observability)은 모든 주요 계층에 포함되어야 한다. 센서 상태, 통신 지연시간, 프로세서 사용률, 추론 시간, 메모리 사용량, 온도, 전력 상태, 제어기 상태, 액추에이터 고장, AI 신뢰도를 함께 모니터링할 수 있어야 한다. 이를 통해 엔지니어는 물리적 동작의 성능 저하가 센싱, 컴퓨팅, 네트워크, 소프트웨어, 제어, 전력, 열 조건 또는 기계 하드웨어 중 어디에서 발생했는지를 판단할 수 있다.

확장성(Scalability)은 컴퓨팅, 통신, 전력, 소프트웨어 자원을 서로 연계된 아키텍처 영역으로 취급함으로써 확보할 수 있다. 센서 또는 AI 모델을 추가하면 처리 용량뿐만 아니라 메모리 대역폭, 네트워크 트래픽, 열 방출, 전기 부하, 저장공간, 동기화 및 검증 요구사항까지 변화한다. 따라서 추가적인 지능 기능을 도입하기 전에 충분한 용량 여유(Capacity Margin)와 모듈형 인터페이스(Modular Interface)를 계획해야 한다.

궁극적으로 AI 네이티브 아키텍처(AI-Native Architecture)는 지능(Intelligence)을 물리적 기계의 기본 구조 안에 통합한다. 센서는 지속적으로 세계를 관측하고, 이기종 컴퓨터(Heterogeneous Computer)는 관측 정보를 표현과 의사결정으로 변환하며, 실시간 제어기는 의도를 결정론적인 실행으로 변환하고, 액추에이터는 다시 센싱되는 물리적 변화를 만들어낸다. 전력, 통신, 안전, 보안, 타이밍, 소프트웨어 수명주기 기능은 이러한 폐루프를 지원하는 분리할 수 없는 아키텍처 요소가 된다.

따라서 AI 네이티브 피지컬 AI(AI-Native Physical AI)를 정의하는 핵심 특성은 단순히 강력한 GPU나 대규모 신경망을 탑재하는 것이 아니다. 핵심은 지능 중심 폐루프(Intelligence-Driven Closed Loop)를 기준으로 전기 하드웨어, 컴퓨팅, 센싱, 통신, 제어, 안전, 전력, 소프트웨어를 통합적으로 공동 설계(Co-Design)하는 것이다. 이러한 접근을 통해 실제 기계에 필요한 타이밍, 신뢰성, 제어 가능성(Controllability), 물리적 무결성(Physical Integrity)을 유지하면서 더욱 발전된 AI 모델을 지속적으로 적용할 수 있다.

##  

## 05.04. Heterogeneous Computing

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

Heterogeneous computing combines multiple processor types within one Physical AI system so that each workload can execute on hardware suited to its computational and timing characteristics. Instead of requiring a single processor to perform perception, planning, communication, safety, and motor control, the architecture distributes these functions across CPUs, GPUs, NPUs, MCUs, DSPs, FPGAs, and specialized real-time controllers.

The need for heterogeneous computing arises because Physical AI contains fundamentally different workloads. Neural-network inference requires large parallel matrix operations, image processing demands high data throughput, planning requires flexible general-purpose computation, and motor control requires deterministic execution with very low timing variation. No single processing architecture provides the optimum performance, efficiency, latency, and determinism for all of these requirements.

The CPU typically provides the general-purpose computing foundation. It can execute operating systems, middleware, communication stacks, navigation logic, task management, diagnostics, and algorithms containing complex branching or sequential processing. CPUs also coordinate other accelerators, manage memory and I/O resources, and provide the software environment in which multiple Physical AI functions are integrated into a complete application.

GPUs provide massively parallel computing resources and are particularly effective for workloads involving neural networks, computer vision, point-cloud processing, and large numerical operations. Camera perception, semantic segmentation, object detection, depth estimation, sensor fusion, and learned prediction models can benefit from GPU acceleration. GPU performance allows complex AI models to operate locally on an edge computer rather than depending entirely on remote infrastructure.

NPUs and dedicated AI accelerators provide another processing domain optimized specifically for neural-network inference. These devices can execute common tensor and matrix operations with lower power consumption than general-purpose processors for supported workloads. In mobile robots, autonomous machines, and battery-powered Physical AI platforms, inference performance per watt can be as important as maximum computational throughput.

MCUs remain essential because many physical functions require predictable execution rather than massive parallel computation. They can manage sensor acquisition, low-level communication, power sequencing, actuator interfaces, watchdogs, and local control loops. A motor-control MCU may execute current or torque regulation thousands of times per second while the edge AI processor performs perception and planning at substantially lower frequencies.

Digital signal processors(DSPs) are useful for workloads dominated by repetitive numerical signal processing. Filtering, spectral analysis, radar processing, audio processing, sensor conditioning, and some control algorithms can execute efficiently on DSP architectures. Processing data close to the sensor can also reduce the amount of raw information that must be transferred to higher-level processors, decreasing communication and memory bandwidth requirements.

FPGAs provide configurable hardware parallelism and can be valuable when very low latency, deterministic pipelines, or custom interfaces are required. They can implement sensor preprocessing, protocol conversion, timestamping, high-speed data routing, synchronization, or specialized acceleration. Unlike fixed processors, FPGA logic can be configured around a particular data path, although this flexibility introduces additional development and verification complexity.

Real-time processors and dedicated control units form another important part of heterogeneous Physical AI architecture. These devices execute trajectory tracking, servo control, vehicle dynamics, actuator coordination, or machine-control functions with bounded timing behavior. Their role is complementary to AI processors: AI determines higher-level intent while deterministic controllers ensure that physical execution follows that intent predictably.

The architecture therefore forms a hierarchy from intelligence-oriented computing toward increasingly time-critical physical control. High-performance edge computers may execute perception, world-state estimation, reasoning, and planning. Intermediate controllers transform planned behavior into trajectories or actuator targets, while local controllers execute position, velocity, torque, and current loops close to the hardware.

Different processing domains also operate at different rates. A vision model may update at 20 or 30 Hz, planning may execute at 10 Hz, trajectory control may operate at several hundred hertz, and motor-current regulation may exceed several kilohertz. Heterogeneous computing allows each processing element to operate at the rate appropriate to its responsibility without forcing the entire machine into one global execution cycle.

Data movement between processors becomes a major architectural concern. Sensor frames may move from an acquisition interface into memory, then into a GPU or accelerator, while inference results move back to the CPU for planning and subsequently to a real-time controller. Excessive copying can increase latency, memory bandwidth, processor utilization, and energy consumption even when the individual computation stages are highly optimized.

Shared memory, direct memory access(DMA), high-speed internal interconnects, zero-copy mechanisms, and accelerator-aware software can reduce this overhead. The objective is to move information through the compute architecture with as few unnecessary transformations and copies as possible. In high-bandwidth Physical AI systems, efficient data movement may provide greater practical improvement than simply adding additional peak computing performance.

Communication between separate computing nodes must also match the characteristics of the data being exchanged. Ethernet and other high-bandwidth links can connect cameras, LiDAR, edge computers, and high-performance controllers, while CAN, CAN FD, CANopen, EtherCAT, or similar networks can connect distributed real-time devices. Gateways may bridge these networks while preserving timing and fault-containment boundaries.

Task partitioning determines which processor should execute each function. This decision should consider computational complexity, latency, determinism, data locality, memory demand, power consumption, thermal behavior, safety requirements, and software maintainability. Assigning every available AI workload to a GPU may simplify early development but can create resource contention and unpredictable latency as system complexity increases.

Resource contention becomes particularly important when several AI models share the same accelerator. Perception, localization, prediction, and planning workloads may compete for GPU execution time, memory capacity, and memory bandwidth. Scheduling policies, workload priorities, execution budgets, and performance monitoring are therefore necessary to ensure that lower-priority processing does not delay functions required for immediate physical operation.

Power efficiency strongly influences heterogeneous computing design. CPUs, GPUs, accelerators, communication devices, and controllers have different power characteristics, and their utilization changes dynamically during operation. Workloads can sometimes be assigned to specialized processors that perform the required function with less energy, reducing battery consumption, thermal load, cooling requirements, and electrical infrastructure demand.

Thermal constraints are directly connected to processor allocation. Concentrating many workloads on a single high-performance processor may create localized heat and cause thermal throttling, reducing sustained computational performance. Distributing appropriate workloads across specialized devices can improve thermal balance, although additional processors also increase hardware complexity, power conversion requirements, packaging, and communication interfaces.

Reliability requires that failures in one compute domain do not unnecessarily propagate throughout the machine. A GPU failure or overloaded AI process should not automatically eliminate emergency handling or basic actuator control. Partitioning critical functions onto independent controllers enables graceful degradation, allowing the system to reduce capability, enter a fallback mode, maintain limited control, or transition safely when high-level computing becomes unavailable.

Functional safety further strengthens this separation. Safety-related monitoring, emergency-stop handling, safe torque off, and protective control may require dedicated safety hardware or certified processing paths rather than execution within the same general-purpose AI environment. Heterogeneous computing therefore supports not only performance optimization but also architectural independence between intelligent behavior and safety-critical authority.

Software architecture must hide unnecessary hardware complexity while preserving control over processor assignment. Middleware, runtime systems, drivers, communication frameworks, inference engines, and hardware abstraction layers can provide standardized interfaces between applications and processing devices. Well-defined APIs allow algorithms to evolve without exposing every higher-level function to detailed electrical or processor-specific implementation.

Diagnostics and observability must extend across all compute domains. CPU load, GPU utilization, accelerator execution time, memory usage, network traffic, controller cycle time, temperature, voltage, power consumption, and communication errors should be measurable. Correlating these signals helps engineers determine whether performance degradation originates from an algorithm, processor bottleneck, thermal condition, network delay, or electrical limitation.

Scalability depends on maintaining modular boundaries between processing resources. Future systems may add higher-resolution sensors, larger AI models, additional accelerators, more actuators, or new safety functions. Standardized interfaces and clearly defined compute responsibilities allow individual processing domains to evolve without requiring complete redesign of the electrical architecture whenever computational capability increases.

Heterogeneous computing also supports the separation between edge, on-premise, and cloud resources. Latency-sensitive perception and decision functions can execute on the robot, deterministic control remains near actuators, while computationally expensive training, fleet analytics, simulation, and model management can execute on larger external systems. The location of computation becomes another architectural dimension that can be optimized according to operational requirements.

Ultimately, heterogeneous computing provides the computational foundation required to connect AI intelligence with deterministic physical execution. CPUs coordinate, GPUs and accelerators provide intensive AI computation, specialized processors handle signal processing, MCUs and real-time controllers maintain fast physical control, and communication networks connect these domains. Each processor contributes according to the workload it can execute most effectively.

For Physical AI electrical architecture, the objective is therefore not to maximize the capability of one processor but to create a balanced computing system. Performance, latency, determinism, memory bandwidth, energy efficiency, thermal capacity, reliability, safety, and upgradeability must be considered together. Proper heterogeneous computing design enables increasingly sophisticated intelligence while preserving the predictable behavior required by real physical machines.

이기종 컴퓨팅(Heterogeneous Computing)은 하나의 피지컬 AI 시스템(Physical AI System) 안에서 여러 종류의 프로세서를 결합하여 각각의 워크로드(Workload)를 계산 특성과 타이밍 특성에 가장 적합한 하드웨어에서 실행하도록 하는 구조이다. 하나의 프로세서가 인지, 계획, 통신, 안전, 모터 제어를 모두 수행하도록 하는 대신 CPU, GPU, NPU, MCU, DSP, FPGA 및 전용 실시간 제어기(Real-Time Controller)에 기능을 분산한다.

이기종 컴퓨팅이 필요한 이유는 피지컬 AI(Physical AI)가 근본적으로 서로 다른 특성을 가진 워크로드를 포함하기 때문이다. 신경망 추론(Neural-Network Inference)은 대규모 병렬 행렬 연산을 요구하고, 이미지 처리는 높은 데이터 처리량(Data Throughput)을 필요로 하며, 계획 기능은 유연한 범용 연산을 요구한다. 반면 모터 제어는 타이밍 변화가 매우 작은 결정론적 실행(Deterministic Execution)을 필요로 한다. 하나의 프로세서 아키텍처만으로 이러한 모든 요구사항에 대해 최적의 성능, 효율, 지연시간, 결정성을 제공하기는 어렵다.

CPU는 일반적으로 범용 컴퓨팅(General-Purpose Computing)의 기반을 제공한다. 운영체제(Operating System), 미들웨어(Middleware), 통신 스택(Communication Stack), 내비게이션 로직(Navigation Logic), 작업 관리(Task Management), 진단(Diagnostics), 복잡한 분기나 순차 처리를 포함하는 알고리즘 등을 실행할 수 있다. 또한 CPU는 다른 가속기를 조정하고 메모리와 입출력 자원을 관리하며, 여러 피지컬 AI 기능을 하나의 완전한 응용 시스템으로 통합하는 소프트웨어 환경을 제공한다.

GPU는 대규모 병렬 컴퓨팅(Massively Parallel Computing) 자원을 제공하며 특히 신경망, 컴퓨터 비전(Computer Vision), 포인트 클라우드(Point Cloud) 처리, 대규모 수치 연산에 효과적이다. 카메라 인지, 의미론적 분할(Semantic Segmentation), 객체 검출(Object Detection), 깊이 추정(Depth Estimation), 센서 융합(Sensor Fusion), 학습 기반 예측 모델(Learned Prediction Model)은 GPU 가속의 이점을 활용할 수 있다. GPU 성능을 이용하면 복잡한 AI 모델을 원격 인프라에 전적으로 의존하지 않고 로컬 엣지 컴퓨터(Edge Computer)에서 실행할 수 있다.

NPU와 전용 AI 가속기(AI Accelerator)는 신경망 추론에 특화된 또 다른 처리 영역을 제공한다. 이러한 장치는 지원되는 워크로드에 대해 범용 프로세서보다 낮은 전력 소비로 일반적인 텐서(Tensor) 및 행렬 연산을 실행할 수 있다. 이동 로봇(Mobile Robot), 자율 기계(Autonomous Machine), 배터리 기반 피지컬 AI 플랫폼에서는 최대 연산 처리량뿐만 아니라 와트당 추론 성능(Inference Performance per Watt)도 매우 중요한 설계 요소가 된다.

MCU는 많은 물리적 기능에서 대규모 병렬 연산보다 예측 가능한 실행이 중요하기 때문에 여전히 필수적인 역할을 담당한다. MCU는 센서 데이터 획득, 저수준 통신, 전원 시퀀싱(Power Sequencing), 액추에이터 인터페이스, 워치독(Watchdog), 로컬 제어 루프(Local Control Loop)를 관리할 수 있다. 모터 제어 MCU는 엣지 AI 프로세서가 훨씬 낮은 주기로 인지와 계획을 수행하는 동안 초당 수천 회의 전류 또는 토크 제어를 실행할 수 있다.

디지털 신호 프로세서(DSP)는 반복적인 수치 신호 처리가 중심이 되는 워크로드에 유용하다. 필터링(Filtering), 스펙트럼 분석(Spectral Analysis), 레이더 처리, 오디오 처리, 센서 신호 조정(Sensor Conditioning), 일부 제어 알고리즘을 DSP 아키텍처에서 효율적으로 실행할 수 있다. 센서 가까이에서 데이터를 처리하면 상위 프로세서로 전송해야 하는 원시 정보의 양도 감소시킬 수 있으므로 통신 및 메모리 대역폭 요구사항을 줄일 수 있다.

FPGA는 구성 가능한 하드웨어 병렬성(Configurable Hardware Parallelism)을 제공하며 매우 낮은 지연시간, 결정론적 파이프라인(Deterministic Pipeline), 맞춤형 인터페이스가 필요한 경우 유용하다. 센서 전처리, 프로토콜 변환(Protocol Conversion), 타임스탬프 생성, 고속 데이터 라우팅(Data Routing), 동기화 또는 특수 가속 기능을 구현할 수 있다. 고정형 프로세서와 달리 FPGA 로직은 특정 데이터 경로에 맞게 구성할 수 있지만, 이러한 유연성은 추가적인 개발 및 검증 복잡성을 수반한다.

실시간 프로세서(Real-Time Processor)와 전용 제어 장치(Dedicated Control Unit) 역시 이기종 피지컬 AI 아키텍처의 중요한 부분을 구성한다. 이러한 장치는 제한된 타이밍 특성(Bounded Timing Behavior)을 유지하면서 궤적 추종(Trajectory Tracking), 서보 제어(Servo Control), 차량 동역학(Vehicle Dynamics), 액추에이터 협조 제어(Actuator Coordination), 기계 제어 기능을 실행한다. AI 프로세서가 상위 수준의 의도를 결정한다면 결정론적 제어기는 물리적 실행이 해당 의도를 예측 가능한 방식으로 따르도록 한다.

따라서 아키텍처는 지능 중심 컴퓨팅(Intelligence-Oriented Computing)에서 점차 시간에 민감한 물리적 제어로 이어지는 계층 구조를 형성한다. 고성능 엣지 컴퓨터는 인지, 월드 상태 추정(World-State Estimation), 추론(Reasoning), 계획(Planning)을 실행할 수 있다. 중간 제어기는 계획된 행동을 궤적 또는 액추에이터 목표로 변환하고, 로컬 제어기는 하드웨어 가까이에서 위치, 속도, 토크, 전류 제어 루프를 실행한다.

서로 다른 처리 영역은 서로 다른 주기로 동작한다. 비전 모델(Vision Model)은 20\~30 Hz로 업데이트될 수 있고, 계획 기능은 10 Hz 수준으로 실행될 수 있으며, 궤적 제어는 수백 Hz, 모터 전류 제어는 수 kHz 이상의 주기로 동작할 수 있다. 이기종 컴퓨팅은 전체 기계를 하나의 전역 실행 주기(Global Execution Cycle)에 맞추지 않고 각각의 처리 요소가 담당 기능에 적합한 주기로 동작하도록 한다.

프로세서 사이의 데이터 이동(Data Movement)은 중요한 아키텍처 설계 요소가 된다. 센서 프레임은 데이터 획득 인터페이스에서 메모리로 이동한 후 GPU 또는 가속기로 전달될 수 있으며, 추론 결과는 계획을 위해 다시 CPU로 전달되고 이후 실시간 제어기로 전송될 수 있다. 과도한 데이터 복사는 각각의 계산 단계가 충분히 최적화되어 있더라도 지연시간, 메모리 대역폭, 프로세서 사용률, 에너지 소비를 증가시킬 수 있다.

공유 메모리(Shared Memory), 직접 메모리 접근(DMA), 고속 내부 인터커넥트(High-Speed Internal Interconnect), 제로 카피(Zero-Copy) 메커니즘, 가속기 인식 소프트웨어(Accelerator-Aware Software)를 이용하면 이러한 오버헤드를 줄일 수 있다. 목표는 불필요한 변환과 복사를 최소화하면서 컴퓨팅 아키텍처 전체로 정보를 전달하는 것이다. 고대역폭 피지컬 AI 시스템에서는 단순히 최대 연산 성능을 추가하는 것보다 효율적인 데이터 이동이 실제 성능을 더 크게 향상시킬 수도 있다.

서로 분리된 컴퓨팅 노드(Computing Node) 사이의 통신 역시 교환되는 데이터의 특성에 적합해야 한다. 이더넷(Ethernet) 및 기타 고대역폭 링크는 카메라, 라이다, 엣지 컴퓨터, 고성능 제어기를 연결할 수 있으며, CAN, CAN FD, CANopen, EtherCAT 등의 네트워크는 분산 실시간 장치(Distributed Real-Time Device)를 연결할 수 있다. 게이트웨이(Gateway)는 타이밍과 고장 격리(Fault Containment) 경계를 유지하면서 이러한 네트워크를 연결할 수 있다.

작업 분할(Task Partitioning)은 각각의 기능을 어떤 프로세서에서 실행할 것인지를 결정한다. 이러한 결정에서는 계산 복잡도, 지연시간, 결정성, 데이터 지역성(Data Locality), 메모리 요구량, 전력 소비, 열 특성, 안전 요구사항, 소프트웨어 유지보수성을 함께 고려해야 한다. 사용 가능한 모든 AI 워크로드를 GPU에 배치하면 초기 개발은 단순해질 수 있지만, 시스템 복잡도가 증가하면 자원 경합(Resource Contention)과 예측하기 어려운 지연시간을 발생시킬 수 있다.

여러 AI 모델이 동일한 가속기를 공유할 경우 자원 경합은 특히 중요한 문제가 된다. 인지, 위치추정, 예측, 계획 워크로드는 GPU 실행 시간, 메모리 용량, 메모리 대역폭을 서로 경쟁하여 사용할 수 있다. 따라서 낮은 우선순위의 처리가 즉각적인 물리적 동작에 필요한 기능을 지연시키지 않도록 스케줄링 정책(Scheduling Policy), 워크로드 우선순위, 실행 예산(Execution Budget), 성능 모니터링(Performance Monitoring)이 필요하다.

전력 효율(Power Efficiency)은 이기종 컴퓨팅 설계에 큰 영향을 미친다. CPU, GPU, 가속기, 통신 장치, 제어기는 서로 다른 전력 특성을 가지며 운용 과정에서 사용률도 동적으로 변화한다. 필요한 기능을 더 적은 에너지로 수행할 수 있는 특화 프로세서에 워크로드를 할당하면 배터리 소비, 열 부하, 냉각 요구사항, 전기 인프라 요구량을 줄일 수 있다.

열 제약조건(Thermal Constraint)은 프로세서 할당과 직접적으로 연결된다. 많은 워크로드를 하나의 고성능 프로세서에 집중하면 국부적인 열이 발생하여 열 스로틀링(Thermal Throttling)을 유발하고 지속적인 연산 성능을 저하시킬 수 있다. 적절한 워크로드를 특화된 여러 장치에 분산하면 열 균형을 개선할 수 있지만, 추가적인 프로세서는 하드웨어 복잡성, 전력 변환 요구사항, 패키징(Packaging), 통신 인터페이스를 증가시킨다.

신뢰성(Reliability)을 확보하려면 하나의 컴퓨팅 영역에서 발생한 장애가 불필요하게 기계 전체로 전파되지 않아야 한다. GPU 장애나 AI 프로세스의 과부하가 비상 처리 또는 기본적인 액추에이터 제어 기능까지 자동으로 제거해서는 안 된다. 핵심 기능을 독립된 제어기에 분할하면 성능 저하 허용(Graceful Degradation)이 가능해지고, 시스템은 상위 컴퓨팅을 사용할 수 없을 때 기능을 축소하거나 폴백 모드(Fallback Mode)로 전환하고 제한된 제어를 유지하거나 안전한 상태로 이동할 수 있다.

기능 안전(Functional Safety)은 이러한 분리를 더욱 강화한다. 안전 관련 모니터링, 비상 정지 처리(Emergency-Stop Handling), 안전 토크 차단(Safe Torque Off), 보호 제어(Protective Control)는 일반적인 AI 실행 환경과 동일한 컴퓨팅 영역에서 실행하기보다 전용 안전 하드웨어 또는 인증된 처리 경로(Certified Processing Path)를 요구할 수 있다. 따라서 이기종 컴퓨팅은 성능 최적화뿐만 아니라 지능적 행동과 안전 핵심 제어 권한 사이의 아키텍처적 독립성을 지원한다.

소프트웨어 아키텍처(Software Architecture)는 프로세서 할당에 대한 제어 능력을 유지하면서 불필요한 하드웨어 복잡성을 상위 소프트웨어에서 감출 수 있어야 한다. 미들웨어, 런타임 시스템(Runtime System), 드라이버(Driver), 통신 프레임워크, 추론 엔진(Inference Engine), 하드웨어 추상화 계층(Hardware Abstraction Layer)은 응용 프로그램과 처리 장치 사이에 표준화된 인터페이스를 제공할 수 있다. 명확하게 정의된 API를 사용하면 상위 기능이 프로세서별 세부 구현에 지나치게 의존하지 않고 알고리즘을 발전시킬 수 있다.

진단(Diagnostics)과 관측 가능성(Observability)은 모든 컴퓨팅 영역에 걸쳐 적용되어야 한다. CPU 부하, GPU 사용률, 가속기 실행 시간, 메모리 사용량, 네트워크 트래픽, 제어기 주기 시간, 온도, 전압, 전력 소비, 통신 오류를 측정할 수 있어야 한다. 이러한 신호를 연계하여 분석하면 성능 저하의 원인이 알고리즘, 프로세서 병목, 열 조건, 네트워크 지연 또는 전기적 한계 중 어디에서 발생했는지를 판단할 수 있다.

확장성(Scalability)은 처리 자원 사이에 모듈형 경계(Modular Boundary)를 유지하는 것에 달려 있다. 미래의 시스템에는 더 높은 해상도의 센서, 더 큰 AI 모델, 추가 가속기, 더 많은 액추에이터 또는 새로운 안전 기능이 추가될 수 있다. 표준화된 인터페이스와 명확하게 정의된 컴퓨팅 책임을 적용하면 계산 능력이 증가할 때마다 전체 전기 아키텍처를 다시 설계하지 않고 개별 처리 영역을 발전시킬 수 있다.

이기종 컴퓨팅은 엣지(Edge), 온프레미스(On-Premise), 클라우드(Cloud) 자원 사이의 역할 분리도 지원한다. 지연시간에 민감한 인지와 의사결정 기능은 로봇에서 실행하고, 결정론적 제어는 액추에이터 가까이에 유지하며, 계산량이 많은 학습, 플릿 분석(Fleet Analytics), 시뮬레이션, 모델 관리는 더 큰 외부 시스템에서 실행할 수 있다. 따라서 컴퓨팅이 실행되는 위치 자체도 운용 요구사항에 따라 최적화할 수 있는 하나의 아키텍처 차원이 된다.

궁극적으로 이기종 컴퓨팅(Heterogeneous Computing)은 AI 지능과 결정론적인 물리적 실행을 연결하는 데 필요한 컴퓨팅 기반을 제공한다. CPU는 시스템을 조정하고, GPU와 가속기는 대규모 AI 연산을 수행하며, 특화 프로세서는 신호 처리를 담당하고, MCU와 실시간 제어기는 빠른 물리적 제어를 유지한다. 통신 네트워크는 이러한 컴퓨팅 영역을 연결하며, 각각의 프로세서는 자신이 가장 효과적으로 수행할 수 있는 워크로드를 담당한다.

따라서 피지컬 AI 전기 아키텍처(Physical AI Electrical Architecture)의 목표는 하나의 프로세서 성능을 최대화하는 것이 아니라 균형 잡힌 컴퓨팅 시스템(Balanced Computing System)을 구성하는 것이다. 성능, 지연시간, 결정성, 메모리 대역폭, 에너지 효율, 열 용량, 신뢰성, 안전, 업그레이드 가능성(Upgradeability)을 함께 고려해야 한다. 적절한 이기종 컴퓨팅 설계는 실제 물리적 기계가 요구하는 예측 가능한 동작을 유지하면서 더욱 정교하고 발전된 지능 기능을 구현할 수 있도록 한다.

##  

## 05.05. Physical AI Power Budget

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

A Physical AI power budget defines how electrical energy is allocated across sensing, computing, communication, control, actuation, safety, and supporting electronics. Unlike conventional electronic systems with relatively predictable loads, Physical AI machines combine high-current electromechanical devices with rapidly changing AI computing workloads, making power allocation a system-level architectural problem rather than a simple sum of component ratings.

The power budget begins by identifying every electrical load and assigning its operating characteristics. Sensors, edge computers, GPUs, controllers, communication devices, storage, cooling systems, motor drives, actuators, safety equipment, lighting, and auxiliary electronics all consume power differently. Their nominal, peak, transient, startup, idle, and fault-state requirements must be distinguished because these conditions can produce substantially different demands.

Average power determines energy consumption over time, while peak power determines whether the electrical architecture can support demanding operating conditions without instability. A mobile robot may consume moderate average power while traveling normally but experience much higher demand during acceleration, steering, manipulation, braking transitions, intensive AI inference, or simultaneous operation of several actuators. Both values must therefore be represented in the design.

Transient power is particularly important because motors and compute accelerators can change their demand rapidly. A motor can request high current during acceleration or sudden load changes, while a GPU can transition from an idle state to intensive inference within a short period. The power system must respond without excessive voltage droop, converter saturation, processor reset, communication disturbance, or degradation of sensitive sensor measurements.

Actuators normally represent one of the largest power consumers in mobile and robotic systems. Drive motors, steering actuators, manipulators, joints, pumps, fans, grippers, and braking systems convert electrical energy into physical work. Their consumption depends on torque, speed, duty cycle, mechanical efficiency, payload, terrain, acceleration, and operating mode, so actuator power cannot be represented accurately by rated power alone.

AI computing introduces a different type of load. CPUs, GPUs, NPUs, memory, storage, and high-speed interfaces consume power according to workload intensity rather than mechanical demand. Running several perception networks, processing multiple camera streams, executing a world model, or performing complex planning can increase compute consumption even when the robot is mechanically stationary, creating a power domain that behaves independently from propulsion.

Sensors usually consume less power individually than motors or high-performance computers, but their combined demand can become significant. Multiple cameras, LiDAR units, radar sensors, GNSS receivers, IMUs, encoders, safety scanners, and auxiliary sensing devices may operate continuously. Sensor heaters, illumination systems, cleaning mechanisms, and environmental conditioning can further increase the total sensing power requirement.

Communication equipment also contributes to the power budget. Ethernet switches, gateways, wireless radios, CAN interfaces, time-synchronization devices, routers, and network processors may remain active throughout operation. High-speed networking can require additional power for transceivers and switching hardware, particularly when multiple high-bandwidth sensors continuously transmit images, point clouds, maps, or diagnostic information.

Cooling must be treated as an electrical load rather than a secondary mechanical consideration. Fans, pumps, liquid-cooling components, and thermal-control devices consume energy to maintain processors, batteries, power electronics, and motors within acceptable temperature ranges. Increasing computational performance can therefore create both direct processor power demand and indirect cooling demand, amplifying the effect of AI workloads on the overall power budget.

The electrical architecture normally separates loads into power domains according to voltage, function, noise sensitivity, safety, and fault behavior. High-power actuators may operate from 48 V or higher-voltage buses, while computers and communication devices use regulated intermediate rails and sensors require lower-voltage supplies. DC/DC converters provide these rails while electrically organizing the machine into manageable distribution domains.

Converter efficiency must be included because energy is lost during every voltage transformation. If a compute platform requires a lower voltage than the battery bus, the DC/DC converter supplying it dissipates part of the input energy as heat. Similar losses occur in motor drives, regulators, protection devices, wiring, and connectors. The battery must therefore provide more energy than the loads themselves ultimately consume.

Power-distribution losses become increasingly important as current increases. Cable resistance, connectors, bus bars, fuses, relays, contactors, and PCB conductors produce voltage drop and heat proportional to electrical loading. Appropriate wire gauge, conductor length, connector rating, distribution topology, and grounding must therefore be considered together with the power budget rather than calculated independently after load selection.

Design margin is necessary because component specifications and real operating conditions are never perfectly fixed. Additional sensors may be installed, AI workloads may grow, processors may operate at higher utilization, motors may encounter heavier loads, and environmental temperature may reduce component capability. Reserve capacity prevents small system changes from immediately requiring redesign of converters, wiring, protection, or battery capacity.

However, excessive margin also increases mass, volume, cost, and potentially conversion losses. Oversized converters, wiring, batteries, and cooling systems can reduce overall system efficiency. Power budgeting should therefore distinguish realistic worst-case operation from theoretically possible combinations of loads that cannot occur simultaneously, using operational scenarios and duty cycles to establish credible design conditions.

Load simultaneity is especially important in Physical AI systems. Maximum motor torque, maximum GPU utilization, full sensor operation, peak communication activity, and maximum cooling demand may not always occur at the same moment. Conversely, some critical scenarios may cause several of these loads to coincide. Scenario-based analysis identifies which combinations must genuinely be supported by the electrical system.

Energy budgeting extends power analysis into operating time. For a battery-powered robot, energy capacity determines mission duration and must account for propulsion, computing, sensing, communication, cooling, conversion losses, standby consumption, and reserve energy. A system with adequate peak power can still fail operational requirements if sustained AI or sensor workloads reduce battery endurance below the required mission duration.

AI workload management can therefore become part of energy management. Models may operate at different inference frequencies, sensors may change operating modes, accelerators may enter low-power states, and noncritical computation can be delayed when energy is constrained. Dynamic power management allows computational performance to adapt to mission conditions rather than assuming maximum AI processing must operate continuously.

Power management can also coordinate physical and computational priorities. During demanding acceleration or manipulation, the system may reserve electrical capacity for actuators while limiting nonessential compute workloads. During stationary inspection, propulsion demand may decrease while AI perception and analysis increase. Such coordination treats available electrical power as a shared system resource that can be allocated according to operational priorities.

Battery architecture must support both energy capacity and instantaneous power delivery. Cell chemistry, pack voltage, internal resistance, state of charge, temperature, aging, and battery-management-system limits influence the available power. A battery with sufficient nominal energy may still be unable to provide a required transient current under low temperature, low state of charge, or degraded aging conditions.

Regenerative energy introduces another consideration in mobile platforms. During braking or deceleration, motors may operate as generators and return electrical energy toward the DC bus or battery. The architecture must determine whether the battery can accept this energy, whether bus voltage remains controlled, and whether braking resistors or other energy-management mechanisms are required when regenerative power cannot be absorbed.

Protection devices must be coordinated with the expected load profile. Fuses, circuit breakers, relays, contactors, current sensors, and electronic protection should tolerate legitimate startup and transient currents while responding appropriately to overloads and faults. Incorrect protection sizing can either create nuisance interruptions during normal peak operation or fail to protect wiring and equipment during abnormal conditions.

Power integrity is particularly important for sensing and computing. Voltage disturbances generated by motors, inverters, switching converters, or large transient loads can affect cameras, communication equipment, processors, and precision sensors. Separate rails, filtering, grounding, decoupling, local energy storage, and carefully designed distribution paths help prevent high-power actuator activity from degrading the intelligence and control domains.

Monitoring converts the static power budget into an operational resource-management capability. Voltage, current, power, energy, temperature, battery state, converter status, and rail faults can be measured throughout the architecture. These measurements allow the system to compare actual consumption with expected behavior, identify abnormal loads, estimate remaining mission time, and detect degradation before it becomes a system-level failure.

Power information can also become an input to Physical AI decision making. A robot with limited remaining energy may select a shorter route, reduce speed, postpone computationally expensive tasks, return to a charger, or modify its mission priorities. Energy state therefore evolves from a passive electrical constraint into part of the machine\'s operational state and autonomous decision process.

Safety functions require protected power availability. Emergency-stop circuits, safety controllers, braking systems, communication needed for controlled shutdown, and other critical functions may require power even when nonessential loads are disconnected. The architecture should define which loads remain energized during faults and how power domains are isolated or shut down without eliminating the functions required to reach a safe state.

Scalability requires the power budget to anticipate future system evolution. Higher-performance AI computers, additional sensors, larger manipulators, faster communication, and more sophisticated cooling can substantially change electrical demand. Modular power distribution, reserved converter capacity, expandable protection, defined voltage rails, and measurable power domains make future upgrades more manageable.

Ultimately, a Physical AI power budget connects electrical energy with intelligence and physical capability. Battery capacity, power conversion, sensing, AI computation, networking, control, actuation, thermal management, protection, and safety must be evaluated as one interacting system. The objective is not merely to provide enough watts, but to deliver the correct power at the required voltage, location, time, and reliability.

A well-designed power budget enables the Physical AI machine to sustain perception, reasoning, deterministic control, and physical action throughout its intended mission. By combining peak-power analysis, energy budgeting, transient response, conversion efficiency, thermal constraints, protection coordination, monitoring, and design margin, the electrical architecture provides a stable foundation on which increasingly capable autonomous systems can operate.

피지컬 AI 전력 예산(Physical AI Power Budget)은 센싱(Sensing), 컴퓨팅(Computing), 통신(Communication), 제어(Control), 구동(Actuation), 안전(Safety), 지원 전자장치(Supporting Electronics)에 전기 에너지를 어떻게 할당할 것인지를 정의한다. 비교적 예측 가능한 부하를 가지는 기존 전자 시스템과 달리 피지컬 AI 기계는 고전류 전기기계 장치와 빠르게 변화하는 AI 컴퓨팅 워크로드를 함께 사용하므로, 전력 할당은 단순한 부품 정격의 합이 아니라 시스템 수준의 아키텍처 문제로 다루어야 한다.

전력 예산은 모든 전기 부하를 식별하고 각각의 운용 특성을 정의하는 것에서 시작한다. 센서, 엣지 컴퓨터(Edge Computer), GPU, 제어기, 통신 장치, 저장장치, 냉각 시스템(Cooling System), 모터 드라이브(Motor Drive), 액추에이터, 안전 장비, 조명 및 보조 전자장치는 서로 다른 방식으로 전력을 소비한다. 정격, 피크(Peak), 과도(Transient), 시동(Startup), 유휴(Idle), 고장 상태(Fault State)의 요구사항을 구분해야 하며, 각 상태에서 요구되는 전력은 크게 달라질 수 있다.

평균 전력(Average Power)은 시간에 따른 에너지 소비량을 결정하고, 피크 전력(Peak Power)은 높은 부하가 발생하는 운용 조건에서도 전기 아키텍처가 불안정해지지 않고 시스템을 지원할 수 있는지를 결정한다. 이동 로봇은 정상 주행 시에는 중간 수준의 평균 전력을 소비하지만, 가속, 조향, 매니퓰레이션(Manipulation), 제동 전환, 고부하 AI 추론 또는 여러 액추에이터의 동시 작동 시에는 훨씬 높은 전력을 요구할 수 있다. 따라서 설계에서는 두 값을 모두 고려해야 한다.

과도 전력(Transient Power)은 모터와 컴퓨팅 가속기의 전력 요구가 빠르게 변화할 수 있기 때문에 특히 중요하다. 모터는 가속 또는 갑작스러운 부하 변화 시 높은 전류를 요구할 수 있으며, GPU는 짧은 시간 안에 유휴 상태에서 고강도 추론 상태로 전환될 수 있다. 전력 시스템은 과도한 전압 강하(Voltage Droop), 컨버터 포화(Converter Saturation), 프로세서 리셋, 통신 장애 또는 민감한 센서 측정의 성능 저하 없이 이러한 변화에 대응해야 한다.

액추에이터(Actuator)는 일반적으로 이동 시스템과 로봇 시스템에서 가장 큰 전력 소비원 중 하나이다. 구동 모터, 조향 액추에이터, 매니퓰레이터, 관절, 펌프, 팬, 그리퍼(Gripper), 제동 시스템은 전기 에너지를 물리적인 일로 변환한다. 소비 전력은 토크, 속도, 듀티 사이클(Duty Cycle), 기계 효율, 페이로드(Payload), 지형(Terrain), 가속도, 운용 모드에 따라 달라지므로 정격 전력만으로 액추에이터의 실제 전력 소비를 정확하게 표현하기 어렵다.

AI 컴퓨팅은 액추에이터와는 다른 형태의 부하를 발생시킨다. CPU, GPU, NPU, 메모리, 저장장치, 고속 인터페이스는 기계적인 요구가 아니라 워크로드의 강도에 따라 전력을 소비한다. 여러 인지 네트워크를 동시에 실행하거나 다수의 카메라 스트림을 처리하고, 월드 모델(World Model)을 실행하거나 복잡한 계획을 수행하면 로봇이 기계적으로 정지해 있는 상황에서도 컴퓨팅 전력 소비가 증가할 수 있다. 따라서 추진 시스템과 독립적으로 변화하는 별도의 전력 영역으로 고려해야 한다.

센서는 개별적으로는 모터나 고성능 컴퓨터보다 적은 전력을 소비하는 경우가 많지만, 여러 센서를 결합하면 전체 소비량이 상당해질 수 있다. 다수의 카메라, 라이다(LiDAR), 레이더(Radar), 위성항법장치(GNSS), 관성측정장치(IMU), 엔코더(Encoder), 안전 스캐너(Safety Scanner), 보조 센싱 장치는 지속적으로 동작할 수 있다. 센서 히터, 조명 시스템, 세척 장치, 환경 조절 장치까지 포함되면 전체 센싱 전력 요구량은 더욱 증가한다.

통신 장비도 전력 예산에 포함되어야 한다. 이더넷 스위치(Ethernet Switch), 게이트웨이(Gateway), 무선 통신 장치, CAN 인터페이스, 시간 동기화 장치, 라우터(Router), 네트워크 프로세서는 운용 중 지속적으로 활성화될 수 있다. 특히 여러 고대역폭 센서가 이미지, 포인트 클라우드(Point Cloud), 지도, 진단 정보를 지속적으로 전송하는 경우 고속 네트워크의 트랜시버(Transceiver)와 스위칭 하드웨어가 추가적인 전력을 요구한다.

냉각(Cooling)은 부수적인 기계 설계 요소가 아니라 하나의 전기 부하로 취급해야 한다. 팬, 펌프, 액체 냉각 장치(Liquid-Cooling Component), 열 제어 장치는 프로세서, 배터리, 전력 전자장치, 모터를 허용 가능한 온도 범위 내에서 유지하기 위해 에너지를 소비한다. 따라서 컴퓨팅 성능을 증가시키면 프로세서 자체의 직접적인 전력 요구뿐만 아니라 냉각을 위한 간접적인 전력 요구도 증가하여 AI 워크로드가 전체 전력 예산에 미치는 영향이 확대된다.

전기 아키텍처는 일반적으로 전압, 기능, 노이즈 민감도, 안전, 고장 동작에 따라 부하를 여러 전력 영역(Power Domain)으로 분리한다. 고출력 액추에이터는 48V 또는 그 이상의 고전압 버스에서 동작할 수 있으며, 컴퓨터와 통신 장치는 안정화된 중간 전압 레일을 사용하고 센서는 더 낮은 전압의 전원을 사용할 수 있다. DC/DC 컨버터는 이러한 전압 레일을 제공하면서 기계를 관리 가능한 여러 전력 분배 영역으로 구성한다.

전압을 변환할 때마다 에너지 손실이 발생하므로 컨버터 효율(Converter Efficiency)을 반드시 고려해야 한다. 컴퓨팅 플랫폼이 배터리 버스보다 낮은 전압을 요구한다면 이를 공급하는 DC/DC 컨버터에서 입력 에너지의 일부가 열로 소모된다. 모터 드라이브, 레귤레이터(Regulator), 보호 장치, 배선, 커넥터에서도 유사한 손실이 발생한다. 따라서 배터리는 실제 부하가 최종적으로 소비하는 에너지보다 더 많은 에너지를 공급해야 한다.

전류가 증가할수록 전력 분배 손실(Power-Distribution Loss)은 더욱 중요해진다. 케이블 저항, 커넥터, 버스바(Bus Bar), 퓨즈(Fuse), 릴레이(Relay), 컨택터(Contactor), PCB 도체에서는 전기 부하에 따라 전압 강하와 열이 발생한다. 따라서 적절한 와이어 굵기(Wire Gauge), 도체 길이, 커넥터 정격, 전력 분배 토폴로지(Distribution Topology), 접지(Grounding)는 부하 선정 이후 별도로 계산하는 것이 아니라 전력 예산과 함께 고려해야 한다.

부품 사양과 실제 운용 조건은 완전히 고정되어 있지 않기 때문에 설계 여유(Design Margin)가 필요하다. 추가 센서가 설치될 수 있고, AI 워크로드가 증가하거나 프로세서 사용률이 높아질 수 있으며, 모터가 더 큰 부하를 받거나 환경 온도 상승으로 부품 성능이 감소할 수도 있다. 적절한 예비 용량(Reserve Capacity)을 확보하면 작은 시스템 변경만으로 컨버터, 배선, 보호 장치 또는 배터리 용량 전체를 다시 설계해야 하는 상황을 방지할 수 있다.

그러나 지나치게 큰 설계 여유는 질량, 부피, 비용을 증가시키고 경우에 따라 변환 손실까지 증가시킬 수 있다. 과도하게 큰 컨버터, 배선, 배터리, 냉각 시스템은 전체 시스템 효율을 낮출 수 있다. 따라서 전력 예산에서는 실제 운용 시나리오(Operational Scenario)와 듀티 사이클을 이용하여 현실적인 최악 조건과 실제로 동시에 발생할 수 없는 이론적인 최대 부하 조합을 구분해야 한다.

부하 동시성(Load Simultaneity)은 피지컬 AI 시스템에서 특히 중요하다. 최대 모터 토크, 최대 GPU 사용률, 전체 센서 동작, 최대 통신 활동, 최대 냉각 요구가 항상 동시에 발생하는 것은 아니다. 반대로 일부 중요한 운용 시나리오에서는 이러한 부하 중 여러 개가 실제로 동시에 발생할 수 있다. 시나리오 기반 분석(Scenario-Based Analysis)을 통해 전기 시스템이 실제로 지원해야 하는 부하 조합을 식별해야 한다.

에너지 예산(Energy Budget)은 전력 분석을 운용 시간까지 확장한 개념이다. 배터리 기반 로봇에서는 에너지 용량이 임무 지속시간(Mission Duration)을 결정하며 추진, 컴퓨팅, 센싱, 통신, 냉각, 변환 손실, 대기 전력, 예비 에너지를 모두 고려해야 한다. 충분한 피크 전력을 제공할 수 있는 시스템이라도 지속적인 AI 또는 센서 워크로드로 인해 배터리 운용시간이 요구되는 임무 시간보다 짧아진다면 운용 요구사항을 만족하지 못한다.

따라서 AI 워크로드 관리(AI Workload Management)는 에너지 관리(Energy Management)의 일부가 될 수 있다. AI 모델은 서로 다른 추론 주파수로 동작할 수 있고, 센서는 운용 모드를 변경할 수 있으며, 가속기는 저전력 상태(Low-Power State)로 전환될 수 있다. 또한 에너지가 제한된 상황에서는 중요하지 않은 연산을 지연시킬 수도 있다. 동적 전력 관리(Dynamic Power Management)를 통해 최대 AI 처리를 항상 유지하는 대신 임무 조건에 따라 컴퓨팅 성능을 조정할 수 있다.

전력 관리는 물리적 기능과 컴퓨팅 기능 사이의 우선순위도 조정할 수 있다. 높은 가속이나 매니퓰레이션이 필요한 상황에서는 액추에이터에 전기 용량을 우선 할당하면서 중요도가 낮은 컴퓨팅 워크로드를 제한할 수 있다. 반대로 정지 상태에서 검사를 수행할 때는 추진 전력 요구가 감소하는 동안 AI 인지와 분석의 비중을 증가시킬 수 있다. 이러한 방식은 사용 가능한 전력을 운용 우선순위에 따라 할당할 수 있는 공유 시스템 자원(Shared System Resource)으로 취급한다.

배터리 아키텍처(Battery Architecture)는 에너지 용량뿐만 아니라 순간적인 전력 공급 능력도 지원해야 한다. 셀 화학(Cell Chemistry), 팩 전압, 내부 저항(Internal Resistance), 충전 상태(State of Charge), 온도, 노화(Aging), 배터리 관리 시스템(BMS)의 제한 조건은 실제 사용 가능한 전력에 영향을 준다. 충분한 정격 에너지를 가진 배터리라도 낮은 온도, 낮은 충전 상태 또는 노화된 조건에서는 필요한 과도 전류를 공급하지 못할 수 있다.

회생 에너지(Regenerative Energy)는 이동 플랫폼에서 추가적으로 고려해야 하는 요소이다. 제동이나 감속 과정에서 모터가 발전기처럼 동작하여 전기 에너지를 DC 버스 또는 배터리로 되돌려 보낼 수 있다. 아키텍처는 배터리가 이러한 에너지를 받아들일 수 있는지, 버스 전압이 안정적으로 유지되는지, 회생 전력을 흡수할 수 없는 경우 제동 저항(Braking Resistor)이나 다른 에너지 관리 메커니즘이 필요한지를 판단해야 한다.

보호 장치(Protection Device)는 예상되는 부하 프로파일(Load Profile)과 협조되어야 한다. 퓨즈, 회로 차단기(Circuit Breaker), 릴레이, 컨택터, 전류 센서, 전자식 보호 장치는 정상적인 시동 전류와 과도 전류를 허용하면서 과부하나 고장에는 적절하게 반응해야 한다. 보호 장치의 용량을 잘못 선정하면 정상적인 피크 운전 중 불필요한 차단이 발생하거나 비정상 상태에서 배선과 장비를 충분히 보호하지 못할 수 있다.

전력 무결성(Power Integrity)은 센싱과 컴퓨팅 영역에서 특히 중요하다. 모터, 인버터(Inverter), 스위칭 컨버터(Switching Converter), 대규모 과도 부하가 발생시키는 전압 교란은 카메라, 통신 장비, 프로세서, 정밀 센서에 영향을 줄 수 있다. 분리된 전원 레일, 필터링, 접지, 디커플링(Decoupling), 로컬 에너지 저장(Local Energy Storage), 신중하게 설계된 전력 분배 경로를 통해 고출력 액추에이터의 동작이 지능 및 제어 영역을 저하시키는 것을 방지할 수 있다.

모니터링(Monitoring)은 정적인 전력 예산을 실제 운용 자원 관리 기능으로 확장한다. 전압, 전류, 전력, 에너지, 온도, 배터리 상태, 컨버터 상태, 전원 레일 고장을 아키텍처 전반에서 측정할 수 있다. 이러한 측정값을 통해 실제 소비량과 예상 동작을 비교하고, 비정상 부하를 식별하며, 남은 임무 시간을 추정하고, 성능 저하가 시스템 수준의 장애로 발전하기 전에 이를 감지할 수 있다.

전력 정보는 피지컬 AI 의사결정(Physical AI Decision Making)의 입력으로도 사용할 수 있다. 남은 에너지가 제한된 로봇은 더 짧은 경로를 선택하거나 속도를 낮추고, 계산량이 많은 작업을 연기하거나 충전기로 복귀하며, 임무 우선순위를 변경할 수 있다. 따라서 에너지 상태(Energy State)는 수동적인 전기적 제약조건에서 벗어나 기계의 운용 상태와 자율 의사결정 과정의 일부로 발전할 수 있다.

안전 기능(Safety Function)은 보호된 전력 공급 능력을 필요로 한다. 비상 정지 회로, 안전 제어기, 제동 시스템, 제어된 종료(Controlled Shutdown)에 필요한 통신 및 기타 핵심 기능은 비필수 부하가 차단된 이후에도 전력을 필요로 할 수 있다. 따라서 아키텍처에서는 고장 발생 시 어떤 부하에 계속 전력을 공급할 것인지 정의하고, 안전 상태에 도달하는 데 필요한 기능을 제거하지 않으면서 전력 영역을 격리하거나 차단할 수 있어야 한다.

확장성(Scalability)을 확보하려면 전력 예산에서 미래의 시스템 발전을 예상해야 한다. 더 높은 성능의 AI 컴퓨터, 추가 센서, 더 큰 매니퓰레이터, 고속 통신, 고성능 냉각 시스템은 전기적 요구량을 크게 변화시킬 수 있다. 모듈형 전력 분배(Modular Power Distribution), 예비 컨버터 용량, 확장 가능한 보호 시스템, 정의된 전압 레일, 측정 가능한 전력 영역을 적용하면 향후 시스템 업그레이드를 보다 효율적으로 관리할 수 있다.

궁극적으로 피지컬 AI 전력 예산(Physical AI Power Budget)은 전기 에너지를 지능(Intelligence) 및 물리적 능력(Physical Capability)과 연결한다. 배터리 용량, 전력 변환, 센싱, AI 컴퓨팅, 네트워킹(Networking), 제어, 구동, 열 관리(Thermal Management), 보호, 안전을 하나의 상호작용하는 시스템으로 평가해야 한다. 목표는 단순히 충분한 와트(Watt)를 제공하는 것이 아니라 필요한 전력을 필요한 전압, 위치, 시간, 신뢰성으로 공급하는 것이다.

잘 설계된 전력 예산은 피지컬 AI 기계가 계획된 임무 전체에서 인지, 추론, 결정론적 제어, 물리적 행동을 지속적으로 수행할 수 있도록 한다. 피크 전력 분석, 에너지 예산, 과도응답(Transient Response), 변환 효율, 열 제약조건, 보호 협조(Protection Coordination), 모니터링, 설계 여유를 통합함으로써 전기 아키텍처는 점점 더 높은 수준의 자율 시스템이 안정적으로 동작할 수 있는 기반을 제공한다.
