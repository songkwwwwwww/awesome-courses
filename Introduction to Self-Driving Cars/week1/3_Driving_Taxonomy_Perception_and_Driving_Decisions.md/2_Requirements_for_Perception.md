Welcome to the second lesson in this module. In the previous lesson, we learned how to classify automation according to its capabilities and operational design domain. In this lesson, we will start analyzing how a driving task is performed. More specifically, we will go over the many processes of perception. We will first define the perception task, listing out the requirements for perceptions such as what static and dynamic objects we need to identify, and what needs we have for tracking the ego vehicles motion through the environment. Finally, we will conclude with a discussion on some challenges to robust perception. So let's dive in. Very roughly speaking, any driving tasks can be broken down into two components. First, we need to understand what's happening around us and where we are. So, we need to perceive our surroundings. Secondly, we need to make a driving decision. For example, should we accelerate or stop before a pedestrian about to enter the roadway? Recall from the previous lesson the concept of OEDR or object and event detection and response. Any driving task requires some kind of OEDR, that is, we need some way of identifying objects around us, recognizing events happening near us, and then responding to it. Recall that the classification of automated systems that we discussed had OEDR as one of the criteria. In other words, if we want to build a self-driving car, we need to be able to perform OEDR. Let's go further and analyze a crucial part of OEDR perception. So, what is perception? As we discussed, we want to be able to make sense of the environment around us and the way we're moving within it. In particular, for any agent or element on the road, we need to first identify what it is; a car, a cyclist, a bus, etc. And second, we want to understand its motion; has it been moving in a certain way that can tell us what it will do next. As humans, we're really good at understanding patterns. However, it's still difficult for computer systems to be able to recognize these same patterns around us as quickly as we do. We can point to a car going straight and say, "Oh, it will be in this position in some amount of time in the future." This is what makes driving possible for us. So, this ability of predicting the trajectory of a moving object is really important to perception. If we can do this prediction correctly, we can make informed decisions. For example, if I know what the car in front of me is going to do next, then I can decide what to do next in such a way that both of our goals are met. Let's discuss the various elements we need to be able to identify for the perception task. First, we need to identify static elements. These are elements like roads and lane markings, things that segregate regions on the roads like zebra crossings, and important messages such as school up ahead. These are all on the road area. Then there are off-road elements like curbs that define the boundaries within which we can drive. There are the on-road traffic signals that periodically change and signal whether you are allowed to move forward, or left, or right, or just stay stopped. Then there are all kinds of road signs like those telling you the speed limit, indicating direction, whether there is a hospital coming up, or a school coming up, and so on. Again, these are off-road elements. Finally, there are road obstructions. So, the orange cones that tell you construction is happening or that there is roadblock edge and so on. 


이 모듈의 두 번째 수업에 오신 것을 환영합니다. 

이전 수업에서, 우리는 기능과 운영 설계 영역에 따라 자동화를 분류하는 방법을 배웠습니다. 

이 수업에서, 우리는 운전 작업이 어떻게 수행되는지 분석하기 시작할 것이다. 
더 구체적으로, 우리는 많은 인식 과정을 검토할 것이다. 
우리는 먼저 인식 작업을 정의하고, 식별해야 할 정적 및 동적 물체, 그리고 환경을 통한 자아 차량의 움직임을 추적하기 위한 요구 사항과 같은 인식 요구 사항을 나열할 것입니다. 
마지막으로, 우리는 강력한 인식에 대한 몇 가지 도전에 대한 논의로 결론을 내릴 것이다. 

그럼 뛰어들자. 매우 대략적으로 말하자면, 모든 운전 작업은 두 가지 구성 요소로 나눌 수 있다. 

먼저, 우리는 우리 주변에서 무슨 일이 일어나고 있는지 그리고 우리가 어디에 있는지 이해해야 한다. 
그래서, 우리는 우리의 주변 환경을 인식해야 한다. 
둘째, 우리는 운전 결정을 내려야 한다. 예를 들어, 보행자가 도로에 들어가기 전에 가속하거나 멈춰야 하나요? 이전 수업에서 OEDR 또는 객체 및 이벤트 감지 및 응답의 개념을 상기하십시오.
모든 운전 작업에는 일종의 OEDR이 필요합니다. 
즉, 우리 주변의 물체를 식별하고, 우리 근처에서 일어나는 사건을 인식한 다음, 대응하는 방법이 필요합니다. 우리가 논의한 자동화된 시스템의 분류에는 OEDR이 기준 중 하나라는 것을 기억하세요. 즉, 자율주행 자동차를 만들고 싶다면, OEDR을 수행할 수 있어야 한다. 
더 나아가 OEDR 인식의 중요한 부분을 분석해 봅시다. 
그래서, 인식이 뭐야? 우리가 논의했듯이, 우리는 우리 주변의 환경과 그 안에서 움직이는 방식을 이해할 수 있기를 원한다. 
특히, 도로의 모든 에이전트나 요소에 대해, 우리는 먼저 그것이 무엇인지 식별해야 합니다; 
자동차, 사이클리스트, 버스 등. 
그리고 둘째, 우리는 그것의 움직임을 이해하고 싶습니다; 
그것은 다음에 무엇을 할 것인지 우리에게 알려줄 수 있는 특정한 방식으로 움직이고 있나요? 
인간으로서, 우리는 패턴을 이해하는 데 정말 능숙하다. 
그러나, 컴퓨터 시스템이 우리 주변의 이러한 패턴을 빠르게 인식할 수 있는 것은 여전히 어렵다. 
우리는 곧장 가는 차를 가리키며 "오, 그것은 미래에 어느 정도 이 위치에 있을 것이다"라고 말할 수 있다. 
이것이 우리에게 운전을 가능하게 하는 것이다. 그래서, 움직이는 물체의 궤적을 예측하는 이 능력은 인식에 정말 중요하다. 
우리가 이 예측을 올바르게 할 수 있다면, 우리는 정보에 입각한 결정을 내릴 수 있다. 
예를 들어, 내 앞에 있는 차가 다음에 무엇을 할 것인지 안다면, 나는 우리의 두 목표가 모두 충족되는 방식으로 다음에 무엇을 할지 결정할 수 있다. 
인식 작업을 위해 식별할 수 있는 다양한 요소에 대해 논의해 봅시다. 
먼저, 우리는 정적 요소를 식별해야 한다. 
이것들은 도로와 차선 표시, 얼룩말 횡단과 같은 도로의 지역을 분리하는 것들, 그리고 학교와 같은 중요한 메시지와 같은 요소이다. 
이것들은 모두 도로 지역에 있다. 그런 다음 우리가 운전할 수 있는 경계를 정의하는 연석과 같은 오프로드 요소가 있습니다. 
주기적으로 바뀌고 앞으로 나아갈 수 있는지, 왼쪽 또는 오른쪽으로 움직일 수 있는지, 아니면 그냥 멈추는 것을 알리는 도로 교통 신호가 있습니다. 
그런 다음 속도 제한을 알려주는 것과 같은 모든 종류의 도로 표지판이 있으며, 방향을 나타내며, 병원이 올라오든, 학교가 올라오든 등과 같은 모든 종류의 도로 표지판이 있습니다. 
다시 말하지만, 이것들은 오프로드 요소이다. 
마지막으로, 도로 장애물이 있다. 
그래서, 건설이 일어나고 있거나 장애물 가장자리가 있다는 것을 알려주는 주황색 원뿔.
  

Also, these are on road elements. 

Second, let's discuss the dynamic elements that we need to identify for perception. These are the elements whose motion we need to predict to make informed driving decisions. We need to identify other vehicles on the road, so four wheelers like trucks, buses, cars, and so on, and then we also need to identify and predict the motion of two wheelers, like motorcycles, bicycles, and so forth. These are all moving systems with more freedom than four wheelers, and so they are harder to predict. Finally, we should also be able to identify and predict the motion of pedestrians around us. How pedestrians behave is very different from vehicles as pedestrians are known to be much more erratic than vehicles in their motion because of the inherent freedom that humans have in the way they move. Another crucial goal for perception is ego localization. We need to be able to estimate where we are and how we are moving at any point in time. Knowing our position and how we are moving in the environment is crucial to making informed and safe driving decisions. The data used for ego motion estimation comes from GPS, IMU, and odometry sensors, and needs to be combined together to generate a coherent picture of our position. The second and third courses of this specialization will dive deeply into these essential perception tasks, starting with ego localization in course two, and followed by on and off road object detection and tracking in course three. Now that we've discussed the main goals for perception, let's conclude this discussion by going over why perception is also a difficult problem. First, performing robust perception is a huge challenge. Detection and segmentation can be approached with modern machine learning methods, but there is much ongoing research to improve the reliability and performance to achieve human level capability. Access to large datasets is critical to this effort. With more training data, our segmentation and detection models perform better and more robustly, but collecting and labeling data for all possible vehicle types, weather conditions, and road surfaces is a very expensive and time-consuming process. Second, perception is not immune to censor uncertainty. There are many times that visibility can be challenging, or GPS measurements get corrupted, or LIDAR and Radar returns are noisy in terms of their position value. Every subsystem that relies on these sensors must take uncertain measurements into account. This is why it is absolutely crucial to design subsystems that can accommodate sensor uncertainty and corrupted measurements in every perception task. Then there are effects such as occlusion and reflection in camera or LIDAR data. These can confuse perception methods with ambiguous information that is challenging to resolve into accurate estimates of object locations. There are also effects such as drastic illumination changes and lens flare, or GPS outages and tunnels which makes some sensor data completely unusable or unavailable. Perception methods need multiple redundant sources of information to overcome sensor data loss. Finally, there's weather and precipitation that can adversely affect the quality of input data from sensors. So, it is crucial to have at least some sensors that are immune to different weather conditions, for example radar. Let's summarize. In this video, we briefly went through the main tasks for perception. The task of detecting and assessing various types of static and dynamic objects and agents in the environment, and the task of making sense of how the ego vehicle is moving through the environment. Finally, we concluded with a discussion of why perception is a hard problem. That's it for this video. See you in the next video where we will be discussing the decision-making aspects of autonomous driving.

또한, 이것들은 도로 요소에 있다. 

둘째, 인식을 위해 식별해야 할 역동적인 요소에 대해 논의해 봅시다. 
이것들은 정보에 입각한 운전 결정을 내리기 위해 우리가 예측해야 하는 요소들이다. 
우리는 도로에서 다른 차량을 식별해야 하므로 트럭, 버스, 자동차 등과 같은 네 대의 휠러를 식별해야 하며, 오토바이, 자전거 등과 같은 두 개의 휠러의 움직임을 식별하고 예측해야 합니다. 
이것들은 모두 네 개의 휠러보다 더 많은 자유를 가진 움직이는 시스템이기 때문에 예측하기가 더 어렵다. 

마지막으로, 우리는 또한 우리 주변의 보행자의 움직임을 식별하고 예측할 수 있어야 한다. 
보행자의 행동은 인간이 움직이는 방식에 내재된 자유 때문에 움직이는 차량보다 훨씬 더 불규칙한 것으로 알려져 있기 때문에 보행자의 행동 방식은 차량과 매우 다르다. 인식의 또 다른 중요한 목표는 자아 현지화이다. 
우리는 우리가 어디에 있고 언제라도 어떻게 움직이고 있는지 추정할 수 있어야 한다. 
우리의 입장과 환경에서 어떻게 움직이고 있는지 아는 것은 정보에 입각하고 안전한 운전 결정을 내리는 데 매우 중요하다. 
자아 모션 추정에 사용되는 데이터는 GPS, IMU 및 거리 측정 센서에서 나오며, 우리의 위치에 대한 일관된 그림을 생성하기 위해 함께 결합되어야 합니다. 
이 전문 분야의 두 번째와 세 번째 과정은 코스 2의 자아 현지화를 시작으로, 코스 3의 온/오프로드 물체 감지 및 추적에 이어 이러한 필수 인식 작업에 깊이 파고들 것이다. 

이제 인식의 주요 목표에 대해 논의했으므로, 왜 인식이 어려운 문제인지 검토하여 이 토론을 마무리합시다. 

첫째, 강력한 인식을 수행하는 것은 큰 도전이다. 감지 및 세분화는 현대 기계 학습 방법으로 접근할 수 있지만, 인간 수준의 능력을 달성하기 위해 신뢰성과 성능을 향상시키기 위한 연구가 많이 진행되고 있다. 
대규모 데이터 세트에 대한 접근은 이러한 노력에 매우 중요하다. 
더 많은 훈련 데이터를 통해, 우리의 세분화 및 감지 모델은 더 강력하고 강력하게 수행되지만, 가능한 모든 차량 유형, 기상 조건 및 도로 표면에 대한 데이터를 수집하고 라벨링하는 것은 매우 비싸고 시간이 많이 걸리는 과정입니다. 

둘째, 인식은 검열 불확실성에 면역되지 않는다. 
가시성이 어려울 수 있거나, GPS 측정이 손상되거나, LIDAR 및 레이더 반환이 위치 값 측면에서 시끄러운 경우가 많습니다. 이러한 센서에 의존하는 모든 하위 시스템은 불확실한 측정을 고려해야 한다. 
이것이 모든 인식 작업에서 센서 불확실성과 손상된 측정을 수용할 수 있는 하위 시스템을 설계하는 것이 절대적으로 중요한 이유입니다. 
그런 다음 카메라나 LIDAR 데이터의 폐색 및 반사와 같은 효과가 있습니다. 
이것들은 인식 방법과 물체 위치의 정확한 추정치로 해결하기 어려운 모호한 정보와 혼동할 수 있다. 
또한 과감한 조명 변경과 렌즈 플레어 또는 일부 센서 데이터를 완전히 사용할 수 없거나 사용할 수 없게 만드는 GPS 정전 및 터널과 같은 효과도 있습니다. 
인식 방법은 센서 데이터 손실을 극복하기 위해 여러 중복 정보 소스가 필요하다. 

마지막으로, 센서의 입력 데이터의 품질에 부정적인 영향을 미칠 수 있는 날씨와 강수량이 있습니다. 
따라서 레이더와 같은 다른 기상 조건에 면역이 되는 적어도 일부 센서를 갖는 것이 중요합니다. 

요약해 봅시다. 이 비디오에서, 우리는 인식을 위한 주요 작업을 간략하게 살펴보았다. 
환경에서 다양한 유형의 정적 및 동적 물체와 에이전트를 감지하고 평가하는 작업, 
그리고 자아 차량이 환경을 통해 어떻게 움직이고 있는지 이해하는 작업. 

마지막으로, 우리는 왜 인식이 어려운 문제인지에 대한 논의로 결론을 내렸다. 

이 비디오는 그게 다야. 자율주행의 의사 결정 측면에 대해 논의할 다음 비디오에서 뵙겠습니다.