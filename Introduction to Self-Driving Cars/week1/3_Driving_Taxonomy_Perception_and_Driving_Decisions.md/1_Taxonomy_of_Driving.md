Welcome to the first module of the Introduction to Self-driving Cars course. Throughout this module you will learn about the main components needed to create a self-driving car and the technical requirements that drive their design. Before we begin, it's important that you understand autonomous vehicle requirements or how we define self-driving for a car. This first week is meant to give you a high level survey of the terms and concepts that we'll explore more deeply throughout the specialization. So in module one, I will introduce you to the taxonomy for self-driving cars or a system of classification that we use to define driving automation. Next, I'll describe the perception needs for the driving task or those items that we need to be able to identify properly. Finally, we will tackle the question of how to make driving decisions and discuss a few approaches for making choices about how a vehicle moves through the environment. The goal of this first module is to remind you just how many assessments and decisions the driving task truly requires. Hopefully this will help you appreciate just how much complexity we as humans can manage effectively when it comes to staying safe on the road. So, let's begin. In this video we will cover the basic self-driving terminology, then discuss some requirements leading to a classification system for driving automation levels. Define the task of driving and the various components of driving. Formulate a taxonomy based on our requirements and levels of autonomy needed for a driving task. And finally we will conclude with the limitations of our proposed taxonomy classification system. Let's get started with some technical terms and definitions. We will use these throughout the specialization and they're helpful to know, if you're working in this industry. The first term on our list is the driving task. Broadly speaking, the driving task is made up of three sub-tasks. The first sub-task is perception, or perceiving the environment that we're driving in. This includes tracking a car's motion in identifying the various elements in the world around us, like the road surface, road signs, vehicles, pedestrians and so on. We also need to track all moving objects and predict their future motions. So we can drive safely and accurately. The second sub-task is motion planning. This allows us to reach our destination successfully. For example, you may want to drive from your home to your office. So you'll need to consider which roads you should take, when you should change lanes or cross an intersection and how to execute a swerve maneuver around a pothole along the way. Finally, we need to operate the vehicle itself with vehicle control. So we need to take the appropriate steering, break and acceleration decisions to control the vehicle's position and velocity on the road. These three sub-tasks form the main driving task and need to be performed constantly while driving a vehicle. The next concept I'll introduce, is called the Operational Design Domain or ODD for short. 


자율주행 자동차 소개 과정의 첫 번째 모듈에 오신 것을 환영합니다. 

이 모듈을 통해 자율주행 자동차를 만드는 데 필요한 주요 구성 요소와 설계를 구동하는 기술 요구 사항에 대해 배우게 됩니다. 
시작하기 전에 자율주행차 요구 사항이나 자동차의 자율주행을 어떻게 정의하는지 이해하는 것이 중요합니다. 

이번 첫 주는 전문 분야 전반에 걸쳐 더 깊이 탐구할 용어와 개념에 대한 높은 수준의 조사를 제공하기 위한 것입니다. 

그래서 모듈 1에서 자율주행 자동차에 대한 분류법이나 운전 자동화를 정의하는 데 사용하는 분류 시스템을 소개하겠습니다. 

다음으로, 운전 작업에 대한 인식 요구 사항이나 우리가 제대로 식별할 수 있어야 하는 항목에 대해 설명하겠습니다. 

마지막으로, 우리는 운전 결정을 내리는 방법에 대한 질문을 해결하고 차량이 환경을 통해 어떻게 움직이는지에 대한 몇 가지 접근 방식에 대해 논의할 것입니다.

이 첫 번째 모듈의 목표는 운전 작업에 얼마나 많은 평가와 결정이 정말로 필요한지 상기시키는 것입니다. 

이것이 우리가 도로에서 안전하게 지낼 때 인간으로서 얼마나 많은 복잡성을 효과적으로 관리할 수 있는지 이해하는 데 도움이 되기를 바랍니다. 

그럼, 시작하자. 이 비디오에서 우리는 기본적인 자율주행 용어를 다루고, 자동화 수준을 추진하기 위한 분류 시스템으로 이어지는 몇 가지 요구 사항에 대해 논의할 것입니다. 

운전 작업과 운전의 다양한 구성 요소를 정의하세요. 

운전 작업에 필요한 요구 사항과 자율성 수준에 따라 분류를 공식화하십시오. 

그리고 마지막으로 우리는 제안된 분류 시스템의 한계로 결론을 내릴 것이다. 

몇 가지 기술적인 용어와 정의로 시작합시다. 
우리는 전문 분야 전반에 걸쳐 이것들을 사용할 것이며, 당신이 이 업계에서 일하고 있는지 아는 데 도움이 될 것입니다. 

우리 목록의 첫 번째 용어는 운전 작업이다. 

대체로 말하자면, 운전 과제는 세 가지 하위 작업으로 구성되어 있다. 

첫 번째 하위 과업은 인식 또는 우리가 운전하고 있는 환경을 인식하는 것이다. 여기에는 도로 표면, 도로 표지판, 차량, 보행자 등과 같은 주변 세계의 다양한 요소를 식별하는 자동차의 움직임을 추적하는 것이 포함됩니다. 우리는 또한 움직이는 모든 물체를 추적하고 미래의 움직임을 예측해야 한다. 그래서 우리는 안전하고 정확하게 운전할 수 있다. 

두 번째 하위 작업은 모션 계획이다. 이것은 우리가 목적지에 성공적으로 도달할 수 있게 해준다. 예를 들어, 집에서 사무실까지 운전하고 싶을 수도 있습니다. 따라서 어떤 도로를 취해야 하는지, 차선을 변경하거나 교차로를 건너야 할 때, 그리고 길을 따라 구덩이 주변에서 회전 기동을 실행하는 방법을 고려해야 합니다. 

마지막으로, 우리는 차량 제어로 차량 자체를 작동해야 한다. 그래서 우리는 도로에서 차량의 위치와 속도를 제어하기 위해 적절한 스티어링, 브레이크 및 가속 결정을 내려야 합니다. 이 세 가지 하위 작업은 주요 운전 작업을 형성하며 차량을 운전하는 동안 지속적으로 수행해야 합니다. 제가 소개할 다음 개념은 운영 설계 도메인 또는 ODD라고 합니다.
  

The ODD constitutes the operating conditions under which a given system is designed to function. It includes environmental, time of day, roadway and other characteristics under which the car will perform reliably. Clearly defining the operating conditions for which a self-driving car is designed, is crucial to ensuring the safety of the system. So the ODD needs to be planned out carefully in advance. Now that we know some of the basic terms, let's get to the big question. How do we classify the level of automation in a driving system? Here are some things to consider. First how much driver attention is needed? For example, can you watch a movie while driving to work? Or do you need to keep your attention on the steering wheel at all times? Driver attention is one of the crucial questions to consider when defining the level of autonomy. Second, how much driver action is actually needed? For example do you need to steer? Does the car take care of the speed or do you control that as well? Do you need to change lanes or can the car stay in the current lane without any intervention? What exactly do we need to expect when we say that the car can automatically drive? We defined the driving task broadly in the previous slides. But we will need to discuss this in more depth. All of these questions lead us to the autonomous driving taxonomy. The standards are continuously evolving but for the purposes of our classification, we will use the decomposition suggested by the Society of Automotive Engineers in 2014. You can find a link to this resource in the lesson's supplementary reading. Let's now discuss a way to describe the driving task in increasing levels of automation. First, we have lateral control which refers to the task of steering and navigating laterally on the road. Turning left, right, going straight or tracking a curve and so on. Next we have longitudinal control. This is the task where we control the position or velocity of the car along the roadway, through actions like breaking or acceleration. Then we have Object and Event Detection and Response or OEDR for short. OEDR is essentially the ability to detect objects and events that immediately affect the driving task and to react to them appropriately. OEDR really encompasses a large portion of autonomous driving. So, is used in conjunction with the specific Operational Design Domain to categorize current self-driving systems. Next we have planning. Planning is another important aspect of driving. As immediate response is already part of OEDR, planning is primarily concerned with the long and short term plans needed to travel to a destination or execute maneuvers such as lean changes and intersection crossings. Finally, there are some miscellaneous tasks that people do while driving as well. These include actions like signaling with indicators, hand-waving, interacting with other drivers and so on. Now we have a clear description of what tasks we expect a self-driving car to perform. Let's now discuss the questions that can lead us to the taxonomy for classifying the level of automation in a self-driving car. First, can this system handle steering tasks or lateral control? Second, can it perform acceleration, braking and velocity manipulation tasks or longitudinal control? Third, can the system perform object and event detection and response and to what degree? Crucially, can the system handle emergency situations by itself or does it always need a driver to be attentive during emergencies? Finally, can the system perform in all scenarios and all conditions? Or does it have a limited ODD or set of operating conditions that it can handle safely? 

ODD는 주어진 시스템이 작동하도록 설계된 작동 조건을 구성한다. 
그것은 환경, 시간, 도로 및 자동차가 안정적으로 작동할 다른 특성을 포함한다. 

자율주행 자동차가 설계된 작동 조건을 명확하게 정의하는 것은 시스템의 안전을 보장하는 데 매우 중요하다. 

그래서 ODD는 미리 신중하게 계획되어야 한다. 

이제 몇 가지 기본 용어를 알았으니, 큰 질문으로 들어가자. 

운전 시스템의 자동화 수준을 어떻게 분류하나요? 여기 고려해야 할 몇 가지 사항이 있습니다. 

먼저 운전자의 관심이 얼마나 필요한가요? 예를 들어, 운전해서 출근하는 동안 영화를 볼 수 있나요? 아니면 항상 핸들에 주의를 기울여야 하나요? 운전자의 관심은 자율성 수준을 정의할 때 고려해야 할 중요한 질문 중 하나이다. 

둘째, 실제로 얼마나 많은 운전자 행동이 필요한가요? 예를 들어 조종해야 하나요? 차가 속도를 관리하나요, 아니면 당신도 그것을 통제하나요? 차선을 바꿔야 하나요, 아니면 차가 개입 없이 현재 차선에 머무를 수 있나요? 차가 자동으로 운전할 수 있다고 말할 때 정확히 무엇을 기대해야 하나요? 우리는 이전 슬라이드에서 운전 작업을 광범위하게 정의했다. 하지만 우리는 이것을 더 깊이 논의해야 할 것이다. 이 모든 질문들은 우리를 자율주행 분류로 이끈다. 

표준은 지속적으로 진화하고 있지만, 우리의 분류를 위해, 우리는 2014년에 자동차 엔지니어 협회가 제안한 분해를 사용할 것이다. 
이 리소스에 대한 링크는 수업의 보충 읽기에서 찾을 수 있습니다. 
이제 자동화 수준을 높이는 데 있어 운전 작업을 설명하는 방법에 대해 논의해 봅시다.

첫째, 우리는 도로에서 옆으로 조종하고 항해하는 작업을 가리키는 측면 통제가 있다. 좌회전, 우회전, 직진 또는 곡선을 추적하는 등. 

다음으로 우리는 종단 통제가 있다. 이것은 우리가 파손이나 가속과 같은 행동을 통해 도로를 따라 자동차의 위치나 속도를 제어하는 작업이다. 

그런 다음 개체 및 이벤트 감지 및 응답 또는 OEDR이 있습니다. OEDR은 본질적으로 운전 작업에 즉시 영향을 미치는 물체와 이벤트를 감지하고 적절하게 반응하는 능력이다. OEDR은 자율주행의 많은 부분을 포함한다. 따라서 특정 운영 설계 도메인과 함께 현재 자율주행 시스템을 분류하는 데 사용됩니다. 

다음으로 우리는 계획이 있어. 계획은 운전의 또 다른 중요한 측면이다. 즉각적인 대응은 이미 OEDR의 일부이기 때문에, 계획은 주로 목적지로 여행하거나 마른 변화와 교차로 교차로와 같은 기동을 실행하는 데 필요한 장기 및 단기 계획과 관련이 있다. 

마지막으로, 사람들이 운전 중에 하는 몇 가지 기타 작업이 있다. 여기에는 표시기로 신호를 표시하고, 손을 흔들고, 다른 드라이버와의 상호 작용 등과 같은 행동이 포함됩니다. 

이제 우리는 자율주행 자동차가 어떤 작업을 수행할 것으로 예상하는지에 대한 명확한 설명을 가지고 있습니다. 

이제 자율주행 자동차의 자동화 수준을 분류하기 위한 분류로 이어질 수 있는 질문에 대해 논의해 봅시다. 

첫째, 이 시스템은 스티어링 작업이나 측면 제어를 처리할 수 있나요? 
둘째, 가속, 제동 및 속도 조작 작업 또는 종단 제어를 수행할 수 있나요? 셋째, 시스템이 물체와 이벤트 감지 및 응답을 어느 정도까지 수행할 수 있나요? 결정적으로, 시스템은 비상 상황을 스스로 처리할 수 있나요, 아니면 비상시 운전자가 항상 주의를 기울여야 하나요? 

마지막으로, 시스템이 모든 시나리오와 모든 조건에서 작동할 수 있나요? 아니면 안전하게 처리할 수 있는 제한된 ODD 또는 일련의 작동 조건이 있나요?  

Based on these questions let's walk through the commonly-used levels of automation defined by the SAE Standard J3 016. Let's start with full human perception, planning and control and call this level 0. In this level, there is no driving automation whatsoever and everything is done by the driver. If an autonomous system assist the driver by performing either lateral or longitudinal control tasks, we are in level one autonomy. Adaptive cruise control is a good example of level one. In adaptive cruise control or ACC, the system can control the speed of the car. But it needs the driver to perform steering. So it can perform longitudinal control but needs the human to perform lateral control. Similarly, lane keeping assist systems are also Level one. In lane keeping assistance, the system can help you stay within your lane and warn you when you are drifting towards the boundaries. Today's systems rely on visual detection of lane boundaries coupled with lane centering lateral control. Let's move on to the next level, the level of partial automation. In level two the system performs both the control tasks, lateral and longitudinal in specific driving scenarios. Some simple examples of level two features are GM Super Cruise and Nissan's Pro Pilot Assist. These can control both your lateral and longitudinal motion but the driver monitoring of the system is always required. Nowadays, many automotive manufacturers offer level two automation products including Mercedes, Audi, Tesla and Hyundai. Next up is level three. In level three or the level of conditional automation, the system can perform Object and Event Detection in Response to a certain degree in addition to the control tasks. However, in the case of failure the control must be taken up by the driver. The key difference between level two and three, is that the driver does not need to pay attention in certain specific situations, as the vehicle can alert the driver in time to intervene. This is a controversial level of automation as it is not always possible for an autonomy system to know when it is experiencing a failure. An example of level three systems, would be the Audi A Luxury Sedan, which was an automated driving system that can navigate unmonitored in slow traffic. In the next level, we arrive at highly automated vehicles, where the system is capable of reaching a minimum risk condition, in case the driver doesn't intervene in time for an emergency. Level four systems can handle emergencies on their own but may still ask drivers to take over to avoid pulling over to the side of the road unnecessarily. With this amount of automation, the passengers can check their phone or watch a movie knowing that the system is able to handle emergencies and is capable of keeping the passengers safe. However, level four still permits self-driving systems with a limited ODD. As of fall 2018, only Waymo has deployed vehicles for public transport with this level of autonomy. The Waymo fleet can handle the driving task in a defined geographic area with a nominal set of operating conditions, without the need for a human driver. Finally, in level five the system is fully autonomous and its ODD is unlimited. Meaning that it can operate under any condition necessary. Level five is the point where our society undergoes transformational change. With driverless taxis shuttling people in packages wherever we need them. We don't have any examples for level five yet, but maybe you'll be the one to bring these to reality someday soon. I think to note the levels of autonomy or actually a coarse measure of automation. In fact, it is possible for two car models to claim level four autonomy but have very different capabilities in ODDs. So, let's summarize. In this video we covered various concepts relating to automation. We covered some basic definitions including the Operational Design Domain and the concept of the driving task. And we explored the five levels of driving automation. You can now assess the level of automation in a self-driving system. In the next lesson we will explore the requirements for perception,a crucial aspect for Autonomous System Design.

이러한 질문을 바탕으로 SAE 표준 J3 016에 의해 정의된 일반적으로 사용되는 자동화 수준을 살펴보겠습니다. 

완전한 인간의 인식, 계획 및 통제로 시작하고 이 레벨 0이라고 부르자. 이 수준에서는 운전 자동화가 전혀 없으며 모든 것은 운전자가 수행한다. 

자율 시스템이 측면 또는 종단 제어 작업을 수행하여 운전자를 지원한다면, 우리는 레벨 1 자율성에 있습니다. 
어댑티브 크루즈 컨트롤은 레벨 1의 좋은 예이다. 
어댑티브 크루즈 컨트롤이나 ACC에서, 시스템은 자동차의 속도를 제어할 수 있다. 하지만 운전자가 스티어링을 수행해야 한다. 그래서 그것은 종단 제어를 수행할 수 있지만 인간이 측면 제어를 수행해야 한다. 
마찬가지로, 차선 유지 보조 시스템도 레벨 1이다. 차선 유지 지원에서, 시스템은 차선 내에 머물면서 경계를 향해 표류할 때 경고하는 데 도움이 될 수 있습니다. 오늘날의 시스템은 측면 제어를 중심으로 하는 차선과 결합된 차선 경계의 시각적 탐지에 의존한다. 다음 단계인 부분 자동화 수준으로 넘어갑시다. 

레벨 2에서 시스템은 특정 운전 시나리오에서 측면 및 종단 제어 작업을 모두 수행합니다. 
레벨 2 기능의 몇 가지 간단한 예는 GM 슈퍼 크루즈와 닛산의 프로 파일럿 어시스트입니다.
이것들은 측면과 세로 운동을 모두 제어할 수 있지만 시스템의 운전자 모니터링은 항상 필요합니다. 
오늘날, 많은 자동차 제조업체들은 메르세데스, 아우디, 테슬라, 현대를 포함한 레벨 2 자동화 제품을 제공한다. 

다음은 레벨 3입니다. 레벨 3 또는 조건부 자동화 수준에서, 시스템은 제어 작업 외에도 어느 정도에 대응하여 객체와 이벤트 감지를 수행할 수 있다. 
그러나, 실패의 경우 운전자가 통제해야 한다. 레벨 2와 3의 주요 차이점은 차량이 제 시간에 운전자에게 개입하도록 경고할 수 있기 때문에 운전자가 특정 상황에서 주의를 기울일 필요가 없다는 것이다. 이것은 자율 시스템이 언제 실패를 겪고 있는지 항상 알 수 있는 것은 아니기 때문에 논란의 여지가 있는 수준의 자동화이다. 
레벨 3 시스템의 예는 느린 트래픽에서 모니터링되지 않고 탐색할 수 있는 자동 운전 시스템인 아우디 A 럭셔리 세단이 있다. 

다음 단계에서, 우리는 운전자가 비상 사태에 맞춰 개입하지 않을 경우를 대비하여 시스템이 최소 위험 상태에 도달할 수 있는 고도로 자동화된 차량에 도착합니다. 
레벨 4 시스템은 비상 사태를 스스로 처리할 수 있지만 불필요하게 도로 옆으로 차를 세우는 것을 피하기 위해 운전자에게 인수하도록 요청할 수 있습니다. 
이 양의 자동화로 승객들은 시스템이 비상 사태를 처리할 수 있고 승객을 안전하게 지킬 수 있다는 것을 알고 휴대폰을 확인하거나 영화를 볼 수 있다. 
그러나, 레벨 4는 여전히 제한된 ODD를 가진 자율주행 시스템을 허용한다. 
2018년 가을 현재, 웨이모만이 이 수준의 자율성으로 대중교통을 위한 차량을 배치했다. 
웨이모 함대는 인간 운전자 없이 명목상 작동 조건으로 정의된 지리적 영역에서 운전 작업을 처리할 수 있다. 

마지막으로, 레벨 5에서 시스템은 완전히 자율적이며 ODD는 무제한이다.
그것은 필요한 어떤 조건에서도 작동할 수 있다는 것을 의미한다. 레벨 5는 우리 사회가 변혁적인 변화를 겪는 지점이다. 
무인 택시가 우리가 필요한 곳 어디에서나 사람들을 패키지로 폐쇄한다. 
우리는 아직 레벨 5에 대한 예가 없지만, 아마도 당신은 언젠가 이것들을 현실로 가져올 사람이 될 것입니다. 
나는 자율성 수준이나 실제로 거친 자동화 척도에 주목해야 한다고 생각한다. 

사실, 두 개의 자동차 모델이 레벨 4 자율성을 주장할 수 있지만 ODD에서는 매우 다른 기능을 가지고 있다. 

그럼, 요약해 봅시다. 

이 비디오에서 우리는 자동화와 관련된 다양한 개념을 다루었다. 

우리는 운영 설계 영역과 운전 작업의 개념을 포함한 몇 가지 기본 정의를 다루었습니다. 
그리고 우리는 운전 자동화의 다섯 가지 단계를 탐구했다. 
이제 자율주행 시스템에서 자동화 수준을 평가할 수 있습니다. 
다음 수업에서 우리는 자율 시스템 설계의 중요한 측면인 인식 요구 사항을 탐구할 것입니다.
