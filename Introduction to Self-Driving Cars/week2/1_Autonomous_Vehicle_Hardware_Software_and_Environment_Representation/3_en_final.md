In the previous videos, we discussed sensors, computing hardware, and hardware configurations for autonomous vehicles
이전 비디오에서, 우리는 자율주행 차량을 위한 센서, 컴퓨팅 하드웨어 및 하드웨어 구성에 대해 논의했습니다

In this video we will learn about a representative modular software architecture for self driving cars
이 비디오에서 우리는 자율주행 자동차를 위한 대표적인 모듈식 소프트웨어 아키텍처에 대해 배울 것입니다

The architecture will use the information provided by the hardware components and allow us to achieve our goal of autonomous driving
아키텍처는 하드웨어 구성 요소에서 제공하는 정보를 사용하고 자율주행 목표를 달성할 수 있게 해준다

Let's go over a detailed decomposition of each module of the software stack
소프트웨어 스택의 각 모듈의 상세한 분해를 살펴봅시다

This will allow us to discuss each segment more carefully by taking a look at the inputs which they receive, the computations they need to make, and the outputs that they provide
이를 통해 그들이 받는 입력, 필요한 계산 및 제공하는 출력을 살펴봐 각 세그먼트에 대해 더 신중하게 논의할 수 있습니다

We will discuss the following five software modules, environment perception, environment mapping, motion planning, vehicle control, and finally the system supervisor
우리는 다음 다섯 가지 소프트웨어 모듈, 환경 인식, 환경 매핑, 모션 계획, 차량 제어 및 마지막으로 시스템 감독관에 대해 논의할 것입니다

While this overview of the software stack will not provide implementation detail, it should give you a good understanding of all of the software components required to make a self driving car function
소프트웨어 스택에 대한 이 개요는 구현 세부 사항을 제공하지 않지만, 자율주행 자동차 기능을 만드는 데 필요한 모든 소프트웨어 구성 요소를 잘 이해할 수 있어야 합니다

The entire specialization is organized around this structure so we'll return to it regularly
전체 전문 분야는 이 구조를 중심으로 구성되어 있으므로 우리는 정기적으로 돌아갈 것이다

Also note this is not the only software architecture used in autonomous driving, but is a good representation of the necessary functions for full vehicle autonomy
또한 이것은 자율주행에 사용되는 유일한 소프트웨어 아키텍처는 아니지만, 전체 차량 자율성에 필요한 기능을 잘 표현합니다

Let's take a look at the high level software architecture for a self driving car's software stack
자율주행 자동차의 소프트웨어 스택을 위한 높은 수준의 소프트웨어 아키텍처를 살펴봅시다

As discussed in a previous video, the car observes the environment around it, using a variety of sensors
이전 비디오에서 논의했듯이, 자동차는 다양한 센서를 사용하여 주변 환경을 관찰한다

The raw sensor measurements are passed into two sets of modules dedicated to understanding the environment around the car
원시 센서 측정은 자동차 주변 환경을 이해하는 데 전념하는 두 세트의 모듈로 전달됩니다

The environment perception modules have two key responsibilities, 
환경 인식 모듈에는 두 가지 주요 책임이 있습니다

first, identifying the current location of the autonomous vehicle in space, 
첫째, 공간에서 자율주행 차량의 현재 위치를 식별하고, 

and second, classifying and locating important elements of the environment for the driving task
둘째, 운전 작업을 위해 환경의 중요한 요소를 분류하고 찾는 것입니다

Examples of these elements include other cars, bikes, pedestrians, the road, road markings, and road signs, anything that directly affects the act of driving
이러한 요소의 예로는 다른 자동차, 자전거, 보행자, 도로, 도로 표시 및 도로 표지판이 있으며, 운전 행위에 직접적인 영향을 미치는 모든 것이 있습니다

The environment mapping module creates a set of maps which locate objects in the environment around the autonomous vehicle for a range of different uses, from collision avoidance to egomotion tracking and motion planning
환경 매핑 모듈은 충돌 회피에서 egomotion 추적 및 모션 계획(motion planning)에 이르기까지 다양한 용도로 자율주행 차량 주변 환경에서 물체를 찾는 지도 세트를 만듭니다

The third module is known as motion planning
세 번째 모듈은 모션 계획으로 알려져 있다

The motion planning module makes all the decisions about what actions to take and where to drive based on all of the information provided by the perception and mapping modules
모션 계획 모듈은 인식 및 매핑 모듈에서 제공하는 모든 정보를 기반으로 어떤 조치를 취하고 어디로 운전해야 하는지에 대한 모든 결정을 내립니다

The motion planning module's main output is a safe, efficient and comfortable planned path that moves the vehicle towards its goal
모션 계획 모듈의 주요 출력은 차량을 목표로 움직이는 안전하고 효율적이며 편안한 계획 경로이다

The planned path is then executed by the fourth module, the controller
그런 다음 계획된 경로는 네 번째 모듈인 컨트롤러에 의해 실행됩니다

The controller module takes the path and decides on the best steering angle, throttle position, brake pedal position, and gear settings to precisely follow the planned path
The fifth and final module is the system supervisor
컨트롤러 모듈은 경로를 취하고 계획된 경로를 정확하게 따르기 위해 최고의 스티어링 각도, 스로틀 위치, 브레이크 페달 위치 및 기어 설정을 결정합니다

The system supervisor monitors all parts of the software stack, as well as the hardware output, to make sure that all systems are working as intended
다섯 번째이자 마지막 모듈은 시스템 감독관이다

The system supervisor is also responsible for informing the safety driver of any problems found in the system
시스템 관리자는 소프트웨어 스택의 모든 부분과 하드웨어 출력을 모니터링하여 모든 시스템이 의도한 대로 작동하는지 확인합니다

Now that we have a general idea of the function of the main modules, 
시스템 감독관은 또한 시스템에서 발견된 문제를 안전 운전자에게 알릴 책임이 있다

let's take a closer look at each module individually
이제 메인 모듈의 기능에 대한 일반적인 아이디어가 생겼으니, 각 모듈을 개별적으로 자세히 살펴봅시다

First, let's start with environment perception
먼저, 환경 인식부터 시작합시다

As discussed previously, there are two important parts of the perception stack, localizing the ego-vehicle in space, as well as classifying and locating the important elements of the environment
앞서 논의했듯이, 인식 스택에는 공간에서 자아 차량을 현지화하고 환경의 중요한 요소를 분류하고 찾는 두 가지 중요한 부분이 있습니다

The localization module takes in multiple streams of information, such as the current GPS location, IMU measurements and wheel odometry
현지화 모듈은 현재 GPS 위치, IMU 측정 및 휠 거리 측정과 같은 여러 정보 스트림을 취합니다

It then combines them to output an accurate vehicle location
그런 다음 정확한 차량 위치를 출력하기 위해 그것들을 결합합니다

For greater accuracy, some localization modules also incorporate LIDAR and camera data
정확성을 높이기 위해, 일부 현지화 모듈은 LIDAR와 카메라 데이터를 통합합니다

This localization problem will be discussed in much greater detail in the next course of this specialization on state estimation
이 현지화 문제는 주 추정에 대한 이 전문화의 다음 과정에서 훨씬 더 자세히 논의될 것이다

Typically, the problem of classification and localization of the environmental elements is divided into two segments, 
first, detecting dynamic objects in the environment, and second, detecting the static objects in the environment
일반적으로 환경 요소의 분류 및 현지화 문제는 첫째, 환경의 동적 물체를 감지하고, 둘째, 환경의 정적 물체를 감지하는 두 부분으로 나뉩니다

The dynamic object detection module uses a set of camera inputs as well as LIDAR point clouds to create 3D bounding boxes around dynamic objects in the scene
동적 물체 감지 모듈은 카메라 입력 세트와 LIDAR 포인트 클라우드를 사용하여 장면의 동적 물체 주위에 3D 경계 상자를 만듭니다

The 3D bounding boxes encode the class or type of object as well as the exact position, orientation and size of the object
3D 경계 상자는 객체의 클래스 또는 유형뿐만 아니라 객체의 정확한 위치, 방향 및 크기를 인코딩합니다

Once detected, the dynamic objects are tracked over time by a tracking module
일단 감지되면, 동적 물체는 추적 모듈에 의해 시간이 지남에 따라 추적됩니다

The tracker module provides not only the current position of the dynamic objects but also the history of its path through the environment
트래커 모듈은 동적 객체의 현재 위치뿐만 아니라 환경을 통한 경로의 역사도 제공합니다

The history of the path is used along with the roadmaps In order to predict the future path of all dynamic objects
경로의 역사는 모든 동적 물체의 미래 경로를 예측하기 위해 로드맵과 함께 사용됩니다

This is usually handled by a prediction module, which combines all information regarding the dynamic object and the current environment to predict the path of all dynamic objects
이것은 일반적으로 동적 객체와 현재 환경에 관한 모든 정보를 결합하여 모든 동적 객체의 경로를 예측하는 예측 모듈에 의해 처리됩니다

The static object detection module also relies on a combination of camera input and LIDAR data to identify significant static objects in the scene
정적 물체 감지 모듈은 또한 장면에서 중요한 정적 물체를 식별하기 위해 카메라 입력과 LIDAR 데이터의 조합에 의존한다

Such important data include the current lane in which the self-driving vehicle is found, and the location of regulatory elements such as signs and traffic lights
이러한 중요한 데이터에는 자율주행 차량이 발견되는 현재 차선과 표지판과 신호등과 같은 규제 요소의 위치가 포함된다

The problem of environment perception will be the focus of course three in this specialization on visual perception
환경 인식의 문제는 시각적 인식에 대한 이 전문 분야의 세 가지의 초점이 될 것이다

Now that we have a better idea of how the perception stack works, let's move on to the environment mapping modules
이제 인식 스택이 어떻게 작동하는지 더 잘 알고 있으니, 환경 매핑 모듈로 넘어갑시다

Environment maps create several different types of representation of the current environment around the autonomous car
환경 지도는 자율주행차 주변의 현재 환경에 대한 몇 가지 유형의 표현을 만든다

There are three types of maps that we discuss briefly, the occupancy grid map, the localization map and the detailed road map
우리가 간략하게 논의하는 세 가지 유형의 지도가 있습니다: 점유 그리드 지도, 현지화 지도 및 상세한 로드맵

The occupancy grid is a map of all static objects in the environment surrounding the vehicle
점유 그리드는 차량을 둘러싼 환경의 모든 정적 물체의 지도이다

LIDAR is predominantly used to construct the occupancy grid map
LIDAR는 주로 점유 그리드 지도를 구성하는 데 사용된다

A set of filters are first applied to the LIDAR data to make it usable by the occupancy grid
필터 세트는 점유 그리드에서 사용할 수 있도록 LIDAR 데이터에 먼저 적용됩니다

For example, the drivable surface points and dynamic object points are removed
예를 들어, 운전 가능한 표면 점과 동적 물체 지점이 제거됩니다

The occupancy grid map represents the environment as a set of grid cells and associates a probability that each cell is occupied
점유 그리드 맵은 환경을 그리드 셀 세트로 나타내며 각 셀이 점유될 확률을 연관시킨다

This allows us to handle uncertainty in the measurement data and improve the map over time
이를 통해 측정 데이터의 불확실성을 처리하고 시간이 지남에 따라 지도를 개선할 수 있습니다

The localization map, which is constructed from LIDAR, or camera data, is used by the localization module in order to improve eco state estimation
LIDAR 또는 카메라 데이터로 구성된 현지화 맵은 환경 상태 추정을 개선하기 위해 현지화 모듈에서 사용됩니다

Sensor data is compared to this map while driving to determine the motion of the car relative to the localization map
센서 데이터는 현지화 지도에 비해 자동차의 움직임을 결정하기 위해 운전하는 동안 이 지도와 비교된다

This motion is then combined with other proprioceptor sensor information to accurately localize the eco vehicle
그런 다음 이 움직임은 다른 고유 수용체 센서 정보와 결합하여 에코 차량을 정확하게 현지화합니다

The detailed road map provides a map of road segments which represent the driving environment that the autonomous vehicle is currently driving through
상세한 도로 지도는 자율주행 차량이 현재 운전하고 있는 운전 환경을 나타내는 도로 부문 지도를 제공한다

It captures signs and lane markings in a manner that can be used for motion planning
모션 계획에 사용할 수 있는 방식으로 표지판과 차선 표시를 캡처합니다

This map is traditionally a combination of prerecorded data as well as incoming information from the current static environment gathered by the perception stack
이 지도는 전통적으로 미리 녹음된 데이터와 인식 스택에 의해 수집된 현재 정적 환경에서 들어오는 정보의 조합이다

The environment mapping and perception modules interact significantly to improve the performance of both modules
환경 매핑 및 인식 모듈은 두 모듈의 성능을 향상시키기 위해 크게 상호 작용합니다

For example, the perception module provides the static environment information needed to update the detailed road map, which is then used by the prediction module to create more accurate dynamic object predictions
예를 들어, 인식 모듈은 상세한 로드맵을 업데이트하는 데 필요한 정적 환경 정보를 제공하며, 예측 모듈에서 더 정확한 동적 객체 예측을 만드는 데 사용됩니다

Next, we'll take a closer look at how the output from both the environment maps and the perception modules are combined and used by the motion planning module to create a path through the environment
다음으로, 환경 맵과 인식 모듈의 출력이 모션 계획 모듈에서 어떻게 결합되고 사용되는지 자세히 살펴보겠습니다

Motion planning for self-driving cars is a challenging task, and it's hard to solve in a single integrated process
자율주행 자동차를 위한 모션 계획은 어려운 작업이며, 단일 통합 프로세스에서 해결하기 어렵다

Instead, most self-driving cars today use a decomposition that divides the problem into several layers of abstraction as follows
대신, 오늘날 대부분의 자율주행 자동차는 다음과 같이 문제를 여러 겹의 추상화로 나누는 분해를 사용한다

At the top level, the mission planner handles long term planning and defines the mission over the entire horizon of the driving task, from the current location, through the road network to its final destination
최상위 수준에서, 미션 플래너는 장기 계획을 처리하고 현재 위치에서 도로 네트워크를 통해 최종 목적지에 이르기까지 운전 작업의 전체 지평선에 걸쳐 임무를 정의합니다

To find the complete mission, the mission planner determines the optimal sequence of road segments that connect your origin and destination, and then passes this to the next layer
완전한 임무를 찾기 위해, 미션 플래너는 출발지와 목적지를 연결하는 최적의 도로 세그먼트 시퀀스를 결정한 다음 다음 레이어로 전달합니다

The behavior planner is the next level of abstraction, solving short term planning problems
행동 플래너는 단기 계획 문제를 해결하는 다음 단계의 추상화이다

The behaviour planner is responsible for establishing a set of safe actions or maneuvers to be executed while travelling along the mission path
행동 계획자는 임무 경로를 따라 여행하는 동안 실행할 일련의 안전한 행동이나 기동을 수립할 책임이 있다

An example of the behaviour planner decisions would be whether the vehicle should merge into an adjacent lane given the desired speed and the predicted behaviors of nearby vehicles
행동 계획자 결정의 예는 인근 차량의 원하는 속도와 예측된 행동을 감안할 때 차량이 인접한 차선으로 병합되어야 하는지 여부이다

Along with the maneuver of decisions, the behavior planner also provides a set of constrains to execute with each action, such as how long to remain in the current lane before switching
결정의 기동과 함께, 행동 플래너는 전환하기 전에 현재 차선에 머무는 기간과 같은 각 작업으로 실행할 일련의 제약을 제공합니다

Finally, the local planner performs immediate or reactive planning, and is responsible for defining a specific path and velocity profile to drive
마지막으로, 로컬 플래너는 즉각적이거나 반응적인 계획을 수행하며, 운전할 특정 경로와 속도 프로필을 정의할 책임이 있다

The local plan must be smooth, safe, and efficient given all the current constraints imposed by the environment and maneuver
지역 계획은 환경과 기동에 의해 부과된 현재의 모든 제약을 감안할 때 매끄럽고 안전하며 효율적이어야 한다

In order to create such a plan, the local planner combines information provided by the behavior planner, occupancy grid, the vehicle operating limits, and other dynamic objects in the environment
이러한 계획을 만들기 위해, 로컬 플래너는 행동 플래너, 점유 그리드, 차량 작동 제한 및 환경의 다른 동적 물체가 제공하는 정보를 결합합니다

The output of the local planner is a planned trajectory which is a combined desired path and velocity profile for a short period of time into the future
지역 플래너의 출력은 미래로의 짧은 기간 동안 결합된 원하는 경로와 속도 프로필인 계획된 궤적이다

The fourth course of this specialization is dedicated to motion planning
이 전문 분야의 네 번째 과정은 모션 계획에 전념한다

Next, let's see how a typical vehicle controller takes the given trajectory and turns it into a set of precise actuation commands for the vehicle to apply
다음으로, 일반적인 차량 컨트롤러가 주어진 궤적을 어떻게 가져와 차량이 적용할 수 있는 정확한 작동 명령 세트로 바꾸는지 봅시다

A typical controller separates the control problem into a longitudinal control and a lateral control
일반적인 컨트롤러는 제어 문제를 세로 제어와 측면 제어로 분리합니다

The lateral controller outputs the steering angle required to maintain the planned trajectory, whereas the longitudinal controller regulates the throttle, gears and braking system to achieve the correct velocity
측면 컨트롤러는 계획된 궤적을 유지하는 데 필요한 스티어링 각도를 출력하는 반면, 세로 컨트롤러는 올바른 속도를 달성하기 위해 스로틀, 기어 및 제동 시스템을 조절합니다

Both controllers calculate current errors and tracking performance of the local plan, and adjust the current actuation commands to minimize the errors going forward
두 컨트롤러 모두 로컬 계획의 현재 오류와 추적 성능을 계산하고, 현재 작동 명령을 조정하여 향후 오류를 최소화합니다

We'll dig into vehicle control later in this course
우리는 이 과정의 뒷부분에서 차량 제어를 파헤칠 것이다

Finally, let's take a closer look at the system supervisor and its functions
마지막으로, 시스템 감독관과 그 기능을 자세히 살펴봅시다

The system supervisor is the module that continuously monitors all aspects of the autonomous car and gives the appropriate warning in the event of a subsystem failure
시스템 감독관은 자율주행차의 모든 측면을 지속적으로 모니터링하고 하위 시스템 고장 시 적절한 경고를 제공하는 모듈이다

There are two parts, the hardware supervisor, and the software supervisor
하드웨어 감독관과 소프트웨어 감독관의 두 부분이 있다

The hardware supervisor continuously monitors all hardware components to check for any faults, such as a broken sensor, a missing measurement, or degraded information
하드웨어 감독관은 고장난 센서, 측정 누락 또는 손상된 정보와 같은 결함을 확인하기 위해 모든 하드웨어 구성 요소를 지속적으로 모니터링합니다

Another responsibility of the hardware supervisor is to continuously analyze the hardware outputs for any outputs which do not match the domain which the self-driving car was programmed to perform under
하드웨어 감독관의 또 다른 책임은 자율주행 자동차가 수행하도록 프로그래밍된 도메인과 일치하지 않는 출력에 대한 하드웨어 출력을 지속적으로 분석하는 것이다

For example, if one of the camera sensors is blocked by a paper bag or if snow is falling and corrupting the LIDAR point cloud data
예를 들어, 카메라 센서 중 하나가 종이 봉지에 의해 막히거나 눈이 내리고 LIDAR 포인트 클라우드 데이터가 손상되는 경우

The software supervisor has the responsibility of validating this software stack to make sure that all elements are running as intended at the right frequencies and providing complete outputs
The software supervisor also is responsible for analyzing inconsistencies between the outputs of all modules
소프트웨어 감독관은 모든 요소가 올바른 주파수에서 의도한 대로 실행되고 완전한 출력을 제공하기 위해 이 소프트웨어 스택을 검증할 책임이 있습니다
In this video, we looked at the basic software architecture of a typical self-driving software system
소프트웨어 감독관은 또한 모든 모듈의 출력 간의 불일치를 분석할 책임이 있다
In fact, we looked at the decomposition of five major modules and their responsibilities
이 비디오에서, 우리는 전형적인 자율주행 소프트웨어 시스템의 기본 소프트웨어 아키텍처를 살펴보았다
These included: environment perception, environment mapping, motion planning, vehicle controller and, finally, the system supervisor
사실, 우리는 다섯 가지 주요 모듈의 분해와 그 책임을 살펴보았다
In the next video, we'll take a closer look at environment mapping
여기에는 환경 인식, 환경 매핑, 모션 계획, 차량 컨트롤러 및 마지막으로 시스템 관리자가 포함됩니다
We'll look at the three maps used throughout the software architecture, the occupancy grid, the localization map, and the detailed road map
다음 비디오에서, 우리는 환경 매핑을 자세히 살펴볼 것이다
See you in the next video
소프트웨어 아키텍처 전반에 걸쳐 사용되는 세 가지 지도, 점유 그리드, 현지화 지도 및 자세한 로드맵을 살펴보겠습니다
[MUSIC]
다음 비디오에서 보자

[음악]
