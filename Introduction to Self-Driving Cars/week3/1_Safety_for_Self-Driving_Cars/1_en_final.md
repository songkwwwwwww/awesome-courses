Welcome to the third week of this course
이 과정의 세 번째 주에 오신 것을 환영합니다
This week we will dive into the basics of incorporating safety into autonomous vehicle design
이번 주에 우리는 자율주행 차량 설계에 안전을 통합하는 기본 사항을 살펴볼 것입니다
Throughout this module, we'll discuss some of the recent autonomous vehicle crash reports, then we will formally define safety concepts for self-driving cars, and discuss the most common sources of hazard that occur
이 모듈을 통해, 우리는 최근의 자율주행 차량 충돌 보고서 중 일부를 논의한 다음, 자율주행 자동차의 안전 개념을 공식적으로 정의하고, 발생하는 가장 일반적인 위험 원인에 대해 논의할 것입니다
We'll discuss some industry perspectives on safety, and finally, we'll wrap up by discussing some of the common frameworks that are used in safe system design
우리는 안전에 대한 몇 가지 업계의 관점에 대해 논의할 것이며, 마지막으로 안전한 시스템 설계에 사용되는 몇 가지 공통 프레임워크에 대해 논의함으로써 마무리할 것입니다
In this lesson, we will discuss some of the first incidence of self-driving car crashes from 2017 and 2018
이 수업에서, 우리는 2017년과 2018년의 자율주행 자동차 충돌의 첫 번째 발생률에 대해 논의할 것입니다
Then, we will define some basic safety concepts and list some of the most common causes for autonomous vehicle hazards, and discuss the low level and high level requirements for safety
그런 다음, 우리는 몇 가지 기본 안전 개념을 정의하고 자율주행 차량 위험의 가장 일반적인 원인 중 일부를 나열하고, 안전에 대한 낮은 수준의 높은 수준의 요구 사항에 대해 논의할 것입니다
We should point out that the material in this module is mostly taken from the published guidelines, by the International Organization for Standards, ISO
우리는 이 모듈의 자료가 대부분 국제표준기구, ISO에 의해 출판된 지침에서 가져온 것임을 지적해야 한다
You'll find a more comprehensive version of these frameworks online
온라인에서 이러한 프레임워크의 보다 포괄적인 버전을 찾을 수 있습니다
Let's start with a discussion of some of the more prominent autonomous vehicle failures to date
지금까지 더 눈에 띄는 자율주행차 고장의 일부에 대한 논의부터 시작합시다
In March 2016, a self-driving Google car now Waymo, ran into the side of a bus when it attempted to pull out from behind an obstacle in its way
2016년 3월, 자율주행 구글 자동차인 웨이모는 장애물 뒤에서 철수하려고 시도했을 때 버스 옆으로 달려갔다
A bus was approaching from the rear and was aiming to pass the Google car in its lane, which was over to the right of its lane prepared to turn
버스가 뒤쪽에서 접근하고 있었고 돌릴 준비가 된 차선 오른쪽에 있는 차선에서 구글 자동차를 통과하는 것을 목표로 하고 있었다
The Google car software believed the bus would not attempt to pass it, as the gap between itself and the cars in the next lane was too narrow
구글 자동차 소프트웨어는 버스와 다음 차선에서 자동차 사이의 격차가 너무 좁기 때문에 버스가 그것을 통과하려고 시도하지 않을 것이라고 믿었다
It turns out buses habitually shoot through smaller gaps than Google anticipated leading to the crash in this case
버스는 구글이 예상했던 것보다 더 작은 격차를 통해 습관적으로 충돌로 이어지는 것으로 밝혀졌다
By the time the Google car could react to the new measurements of the bus location, it was too late
구글 자동차가 버스 위치의 새로운 측정에 반응할 수 있을 때, 너무 늦었다
This is just one example of how hard it is to predict all other vehicles actions before they happen
이것은 다른 모든 차량 행동이 일어나기 전에 예측하는 것이 얼마나 어려운지에 대한 한 예일 뿐입니다
A year later, an Uber self-driving vehicle overreacted during a minor collision caused by another vehicle and ended up overturning
1년 후, 우버 자율주행 차량은 다른 차량으로 인한 경미한 충돌 중에 과민반응하여 결국 전복했다
Since the dynamic models of the vehicle don't assume significant disturbance forces from other vehicles acting on the car, the controller had likely not been tested for such a scenario and overreacted
차량의 동적 모델은 자동차에 작용하는 다른 차량의 상당한 교란력을 가정하지 않기 때문에, 컨트롤러는 그러한 시나리오에 대해 테스트되지 않았고 과민반응했을 가능성이 높다
This crash highlights the need for robustness integrated into the control system and for exploratory testing that covers as many foreseeable events as possible
이 충돌은 제어 시스템에 통합된 견고성과 가능한 한 많은 예측 가능한 많은 이벤트를 다루는 탐색 테스트의 필요성을 강조한다
In the late 2017, a GM Cruise Chevy Bolt knocked over a motorcyclist after it aborted a lane change maneuver
2017년 말, GM 크루즈 시보레 볼트는 차선 변경 기동을 중단한 후 오토바이 운전자를 쓰러뜨렸다
After the Bolt initiated the maneuver, the gap it was hoping to enter closed rapidly due to a braking lead vehicle in the adjacent lane
볼트가 기동을 시작한 후, 인접한 차선에서 제동 리드 차량으로 인해 들어가기를 희망했던 간격이 빠르게 닫혔다
The motorcyclist who was lane splitting, moved forward beside the Bolt and blocked the return maneuver
차선이 갈라지고 있던 오토바이 운전자는 볼트 옆으로 앞으로 나아가 돌아오는 기동을 막았다
The Bolt was stuck in a dilemma situation; to collide with the motorcycle or to crash into both cars in the adjacent lane
볼트는 오토바이와 충돌하거나 인접한 차선에서 두 차에 충돌하기 위해 딜레마 상황에 갇혔다
It's not clear that a specific decision was made here to choose one or the other outcome, and a lawsuit has buried the details of the case
여기서 하나 또는 다른 결과를 선택하기 위한 구체적인 결정이 내려졌다는 것은 분명하지 않으며, 소송이 사건의 세부 사항을 묻었다
However, because other agents are also predicting the self-driving cars actions, it is very challenging to assess what the right action is in many situations
그러나, 다른 요원들도 자율주행 자동차 행동을 예측하고 있기 때문에, 많은 상황에서 올바른 행동이 무엇인지 평가하는 것은 매우 어렵다
As it's possible, the merging might have been possible with a more aggressive driving style or a slightly delayed abort might have been enough time to avoid the motorcyclist
가능하다면, 더 공격적인 운전 스타일로 합병이 가능했을 수도 있고 약간 지연된 중단은 오토바이 운전자를 피하기에 충분한 시간이었을 수도 있다
This tight interaction of decision-making is still a big challenge in self-driving cars
의사 결정의 빡빡한 상호 작용은 여전히 자율주행 자동차에서 큰 도전이다
Finally, we should talk a little bit about the Uber crash that led to a pedestrian fatality in early 2018
마지막으로, 우리는 2018년 초에 보행자 사망자로 이어진 우버 사고에 대해 조금 이야기해야 합니다
Operating in Tempe, Arizona, Uber had an extensive testing program at the time, with safety drivers monitoring the autonomy software
애리조나주 템피에서 운영되는 우버는 당시 안전 운전자들이 자율 소프트웨어를 모니터링하는 광범위한 테스트 프로그램을 가지고 있었다
The incident occurred on a wide multilane divided road at night, where a pedestrian was walking her bicycle across the road in an unmarked area
그 사건은 밤에 넓은 다층 분할 도로에서 발생했으며, 보행자가 표시가 없는 지역의 도로를 가로질러 자전거를 걷고 있었다
The victim, Elaine Herzberg, was a 49 year-old woman from Tempe
희생자인 일레인 헤르츠버그는 템피 출신의 49세 여성이었다
This is the car and the scene depicted from a bird's eye view
이것은 새의 시선에서 묘사된 차와 장면이다
You can see the pedestrian entering from the left and the vehicle traveling along the road way from the bottom of the image
왼쪽에서 들어오는 보행자와 이미지 하단에서 도로를 따라 이동하는 차량을 볼 수 있습니다
The preliminary investigation revealed that there were multiple failures that led to the incident
예비 조사에 따르면 그 사건으로 이어진 여러 실패가 있었다
Let's walk through the different contributing factors
다양한 기여 요인을 살펴보자
First, there were no real-time checks on the safety driver
첫째, 안전 운전자에 대한 실시간 검사는 없었다
In this case, the safety driver was inattentive and allegedly watching Hulu at the time
이 경우, 안전 운전자는 부주의했고 당시 훌루를 보고 있었다고 한다
The safety driver could have been doing anything and Uber didn't have any way in the vehicle to assess the drivers attentiveness
안전 운전자는 무엇이든 할 수 있었고 우버는 운전자의 주의를 평가할 방법이 없었다
Because watching an autonomous driving system operate is a difficult task to stay focused on, it is really important to have a safety driver monitoring system
자율주행 시스템이 작동하는 것을 보는 것은 집중하기 어려운 일이기 때문에, 안전 운전자 모니터링 시스템을 갖는 것이 정말 중요하다
Second, there was significant confusion in the software detection system
둘째, 소프트웨어 탐지 시스템에 상당한 혼란이 있었다
Upon initial detection at six seconds to impact, the victim was first classified as an unknown object, then misclassified as a vehicle, and then misclassified as a bicycle
영향을 미치기 위해 6초에 처음 감지되었을 때, 피해자는 먼저 알려지지 않은 물체로 분류된 다음 차량으로 잘못 분류된 다음 자전거로 잘못 분류되었다
In the end, the decision made by the autonomy software was to ignore the detections, possibly because they were too unreliable
결국, 자율 소프트웨어가 내린 결정은 탐지를 무시하는 것이었는데, 아마도 너무 신뢰할 수 없었기 때문일 것이다
Perception is not perfect and the switching classifications should not have led the vehicle to ignore an object like that completely
인식은 완벽하지 않으며 스위칭 분류로 인해 차량이 그런 물체를 완전히 무시하지 말았어야 했다
Finally, 1
마침내, 충돌 1
3 seconds before the crash, the Volvo emergency braking system did detect the pedestrian and would have applied the brakes rapidly to reduce the impact speed, potentially saving the life of Elaine Herzberg
3초 전에, 볼보 비상 제동 시스템은 보행자를 감지했고 충격 속도를 줄이기 위해 브레이크를 빠르게 적용하여 잠재적으로 일레인 헤르츠버그의 생명을 구했을 것이다
However, it is not safe to have multiple collision avoidance systems operating simultaneously during testing, so Uber had disabled the Volvo system when in autonomous mode
그러나 테스트 중에 여러 충돌 방지 시스템이 동시에 작동하는 것은 안전하지 않으므로 우버는 자율 모드에서 볼보 시스템을 비활성화했습니다
Ultimately, the autonomous vehicle did not react to the pedestrian's path and the inattentive driver was unable to react quickly enough to avoid the collision
궁극적으로, 자율주행차는 보행자의 경로에 반응하지 않았고 부주의한 운전자는 충돌을 피할 만큼 충분히 빨리 반응할 수 없었다
The combination of the failure of the perception system to correctly identify the pedestrian, with a bicycle and of the planning system to avoid the detective object even though it's class was uncertain, led to the autonomy failure, and the lack of human or emergency braking backup ultimately led to the fatality
보행자를 올바르게 식별하지 못하는 인식 시스템의 실패와 자전거 및 탐정 물체를 피하기 위한 계획 시스템의 조합은 불확실했고, 자율 실패로 이어졌고, 인간 또는 비상 제동 백업의 부족은 궁극적으로 사망자로 이어졌다
So, we can see that from this set of incidents, every aspect of the autonomous driving system; the perception, planning, and control, can all lead to failures and crashes, and that often the interaction of multiple systems or multiple decision-makers, can lead to unanticipated consequences
그래서, 우리는 이러한 일련의 사건에서 자율주행 시스템의 모든 측면, 인식, 계획 및 통제가 모두 실패와 충돌로 이어질 수 있으며, 종종 여러 시스템이나 여러 의사 결정권자의 상호 작용이 예상치 못한 결과를 초래할 수 있다는 것을 알 수 있습니다
In fact, there are many more ways an autonomous system can fail
사실, 자율 시스템이 실패할 수 있는 더 많은 방법이 있다

우리가 안전에 대한 엄격하고 철저한 접근이 필요하다는 것은 분명하며, 산업과 규제 기관 모두 안전 문제를 정면으로 해결하고 있다

알았어

이제 안전 평가의 과제에 대한 감각이 있으니, 몇 가지 기본적인 안전 용어를 공식적으로 정의해 봅시다
It is clear that we need rigorous and exhaustive approaches to safety, and both industry and the regulators are tackling the safety challenge head-on
우리는 이 용어를 사용하여 생명체에 대한 신체적 해를 지칭할 것이며, 사건이 발생할 확률과 함께 사건이 발생할 확률을 설명하기 위해 위험이라는 용어를 사용할 것입니다
Okay
우리는 이제 안전을 생명체에 해를 끼칠 불합리한 위험을 피하는 과정으로 묘사할 수 있다
Now, that we have a sense for the challenges of safety assessment, let's formally define some basic safety terms
예를 들어, 교통 신호가 빨간색일 때 교차로로 운전하는 것은 차량의 탑승자와 교차로를 통과하는 다른 차량에 해를 끼칠 불합리한 위험을 초래하기 때문에 안전하지 않을 것이다
We will use the term, harm to refer to the physical harm to a living thing, and we will use the term risk to describe the probability that an event occurs, combined with the severity of the harm, that the event can cause
마지막으로, 위험은 불합리한 피해 위험이나 안전 위협의 잠재적인 원인이다
We can now describe safety as the process of avoiding unreasonable risk of harm to a living thing
그래서, 내 시스템 소프트웨어에 잠재적으로 사고를 일으킬 수 있는 버그가 있다면, 소프트웨어 버그는 위험할 것이다
For example, driving into an intersection when the traffic signal is red would be unsafe as it leads to unreasonable risk to harm of the occupants of the vehicle and to other vehicles moving through the intersection
이제, 자율주행 차량 위험의 가장 흔한 원원은 무엇이라고 생각하십니까
Finally, a hazard is a potential source of unreasonable risk of harm or a threat to safety
음, 위험은 기계적일 수 있으므로, 조숙한 고장을 일으키는 브레이크 시스템의 잘못된 조립일 수도 있습니다
So, if my system software has a bug that could potentially cause an accident, the software bug would be a hazard
그것들은 전기적일 수 있으므로 내부 배선에 결함이 있어 표시등이 손실됩니다
Now, what do you think are the most common sources of autonomous vehicle hazards
위험은 또한 자율주행에 사용되는 하드웨어 칩을 계산하는 실패일 수 있다
Well, hazards can be mechanical, so maybe incorrect assembly of a brake system causing a premature failure
앞서 설명한 바와 같이, 그들은 자율 소프트웨어의 오류나 버그 때문일 수 있다
They can be electrical, so faulty internal wiring leading to a loss of indicator lighting
센서 데이터가 나쁘거나 시끄럽거나 부정확한 인식으로 인해 발생할 수 있습니다
Hazards could also be a failure of computing hardware chips used for autonomous driving
잘못된 계획이나 의사 결정으로 인해 위험도 발생할 수 있으며, 특정 시나리오의 행동 선택이 올바르게 설계되지 않았기 때문에 실수로 위험한 행동을 선택할 수 있습니다
They can, as described earlier, be due to errors or bugs in the autonomy software
또한 인간 운전자에 대한 대체가 운전자에게 책임을 재개할 충분한 경고를 제공하지 않거나 자율주행 자동차가 악의적인 단체에 의해 해킹당할 수도 있다
They might be caused by bad or noisy sensor data or inaccurate perception
이것들은 정기적으로 고려되는 위험의 모든 주요 범주입니다; 기계, 전기, 컴퓨팅 하드웨어, 소프트웨어, 인식, 계획, 운전 작업 대체 및 사이버 보안
Hazards can also arise due to incorrect planning or decision-making, inadvertently selecting hazardous actions because the behavior selection for a specific scenario wasn't designed correctly
이러한 각 위험은 전반적인 시스템 안전을 평가할 때 다른 접근 방식을 요구한다
It's also possible that the fallback to a human driver fails by not providing enough warning to the driver to resume responsibility or maybe a self-driving car gets hacked by some malicious entity
우리는 이후 비디오에서 이러한 카테고리를 다루는 방법에 대해 더 많이 볼 것입니다
These are all the main categories of hazards that are regularly considered; mechanical, electrical, computing hardware, software, perception, planning, driving-task fallback, and cybersecurity
이제 안전과 관련된 기본 용어를 알았으니, 다음 질문에 대해 생각해 봅시다
Each of these hazards requires different approaches when assessing overall system safety
자율주행차가 정말 안전한지 어떻게 보장할 수 있을까요
We'll see more on how to deal with these categories in later videos
즉, 복잡한 운전 작업과 발생할 수 있는 많은 위험을 어떻게 취하고 완전한 자율주행 시스템을 위한 안전 평가 프레임워크를 정의합니까
Now that we know the basic terminology involved in safety, let's think about the following question
미국에서는 국립 고속도로 교통 안전국 또는 NHTSA가 자율주행을 위한 안전 평가를 구성하기 위한 12부작 안전 프레임워크를 정의했다
How do we ensure our self-driving car is truly safe
이 모듈의 다음 비디오에서 볼 수 있듯이, 이 프레임워크는 이미 업계에서 여러 기존 방법과 표준을 결합한 출발점이며 다른 접근 방식이 이미 등장했습니다
That is, how do we take the complex task of driving and the many hazards that can occur, and define a safety assessment framework for a complete self-driving system
그럼, 먼저 NHTSA의 안전 권장 사항에 대해 논의해 봅시다
In the US, the National Highway Transportation Safety Administration or NHTSA, has defined a twelve-part safety framework to structure safety assessment for autonomous driving
이 프레임워크는 2017년에 따라야 할 필수 프레임워크가 아닌 제안된 프레임워크로 출시되었다
As we'll see in the next videos in this module, this framework is only a starting point and different approaches that combine multiple existing methods and standards have already emerged in the industry
프레임워크 자체는 자율주행 회사가 집중해야 하거나 오히려 집중하도록 권장되는 12가지 영역이나 요소로 구성되어 있다
So, let's first discuss the NHTSA's safety recommendations
첫째, 안전에 대한 시스템 설계 접근 방식을 채택해야 하며, 이는 전체 프레임워크 문서에 실제로 스며든다
This framework was released as a suggested, not mandatory framework to follow in 2017
잘 계획되고 통제된 소프트웨어 개발 프로세스는 필수적이며, 자동차, 항공 우주 및 기타 관련 산업의 기존 SAE 및 ISO 표준의 적용은 적절한 경우 적용되어야 합니다
The framework itself consists of 12 areas or elements any autonomous driving company should focus on or rather, are encouraged to focus on
나머지 11개 영역의 경우, 우리는 그것들을 느슨하게 두 가지 범주로 구성할 수 있다
First, a system design approach to safety should be adopted, and this really permeates the entire framework document
자율 소프트웨어 스택에 특정 구성 요소를 포함하고 고려해야 하는 자율 설계와 자율 기능 테스트 접근 방식과 실패의 부정적인 영향을 줄이고 학습하는 방법을 다루는 테스트 및 충돌 완화
Well-planned and controlled software development processes are essential, and the application of existing SAE and ISO standards from automotive, aerospace, and other relevant industries should be applied where relevant
자율 설계 범주에서, 우리는 이미 익숙한 몇 가지 구성 요소를 볼 수 있다
For the remaining 11 areas, we can organize them loosely into two categories
NHTSA는 설계자가 이것의 결함과 시스템의 한계를 잘 인식하고 테스트 또는 배포 전에 어떤 시나리오가 지원되고 안전한지 평가할 수 있도록 잘 정의된 운영 설계 도메인을 장려합니다
Autonomy design, which requires certain components to be included and considered in the autonomy software stack, and testing and crash mitigation, which covers approaches to testing the autonomy functions and ways to reduce the negative effects of failures, as well as learning from them
다음으로, 그것은 인식과 충돌 회피에 중요한 잘 테스트된 물체와 이벤트 탐지 및 대응 시스템을 장려한다
In the autonomy design category, we see some components we're already familiar with
그런 다음, 그것은 자동차가 운전자에게 경고를 받거나 자동차가 자율적으로 안전에 복귀하는 안정적이고 편리한 대체 메커니즘을 갖도록 장려한다
The NHTSA encourages a well-defined operational design domain, so that the designers are well aware of the flaws of this and limitations of the system, and can make an assessment as to which scenarios are supported and safe in advance of testing or deployment
운전자가 부주의할 수 있다는 것을 명심하고 이 메커니즘을 개발하는 것이 필수적이다
Next, it encourages a well-tested object and event detection and response system, which is critical to perception and crash avoidance
그래서, 이런 일이 발생하면 시스템을 최소한의 위험 상태로 만드는 방법에 대한 몇 가지 생각이 들어가야 한다
Then, it encourages the car to have a reliable and convenient fallback mechanism by which the driver is alerted or the car is brought to safety autonomously
운전 시스템은 또한 모든 연방 수준, 주 수준 및 지역 교통법이 ODD 내에서 준수되고 준수되도록 설계되어야 한다
It is essential to develop this mechanism keeping in mind that the driver may be inattentive
다음으로, 이 프레임워크는 디자이너들이 사이버 보안 위협과 악성 에이전트로부터 운전 시스템을 보호하는 방법에 대해 생각하도록 장려한다
So, some thoughts should go into how to bring the system to a minimal risk condition if this happens
마지막으로, 인간 기계 인터페이스 또는 HMI에 약간의 생각이 있어야 한다
The driving system should also be designed such that all the federal level, state level, and local laws for traffic are followed and obeyed within the ODD
그래서, 자동차는 언제든지 승객이나 운전자에게 기계의 상태를 잘 전달할 수 있어야 한다
Next, the framework encourages designers to think about cybersecurity threats, and how to protect the driving system from malicious agents
표시할 수 있는 상태 정보의 중요한 예는 모든 센서가 작동하는지 여부, 현재 모션 계획이 무엇인지, 환경의 어떤 물체가 우리의 운전 행동에 영향을 미치는지 등입니다
Finally, there should be some thought put into the human machine interface, or HMI
우리는 이제 테스트 및 충돌 완화 영역으로 이동합니다
So, the car should be able to well convey the status of the machine at any point in time to the passengers or the driver
무엇보다도, NHTSA는 대중에게 서비스가 시작되기 전에 강력하고 광범위한 테스트 프로그램을 권장합니다
Important examples of status information that can be displayed, are whether all sensors are operational, what the current motion plans are, which objects in the environment are affecting our driving behavior, and so on
이 테스트는 세 가지 일반적인 기둥에 의존할 수 있다; 시뮬레이션, 근접 트랙 테스트 및 공공 도로 운전
We now move to the testing and crash mitigation areas
다음으로, 충돌 사건 중에 발생하는 부상이나 손상의 정도를 완화하는 방법을 신중하게 고려해야 한다
First and foremost, the NHTSA recommends a strong and extensive testing program before any service is launched for the public
충돌은 충돌 제한, 에어백 및 충돌 가치 측면에서 충돌 에너지를 최소화하고 승객 안전 기준을 초과할 수 있는 공공 도로 운전 및 자율 시스템의 현실로 남아있다
This testing can rely on three common pillars; simulation, close track testing, and public road driving
다음으로, 충돌 후 행동에 대한 지원이 있어야 한다
Next, there should be careful consideration of methods to mitigate the extent of injury or damage that occurs during a crash event
예를 들어, 자동차는 연료 펌프가 연료를 고정하고 멈추는 안전한 상태로 빠르게 반환되어야 하며, 첫 번째 응답자들은 경고했다
Crashes remain a reality of public road driving and autonomy systems that can minimize crash energy and exceed passenger safety standards in terms of restraints, airbags, and crash worthiness should be the norm
또한, 자동화된 데이터 기록 기능이나 블랙박스 레코더가 있어야 합니다
Next, there should be support for post crash behavior
이 충돌 데이터를 사용하여 향후 특정 종류의 충돌을 피할 수 있는 시스템을 분석하고 설계하고, 무엇이 잘못되었는지, 그리고 이벤트 중에 누가 잘못되었는지에 대한 질문을 해결하는 것은 매우 도움이 된다
The car must be rapidly returned to a safe state, for example, brought to a stop with fuel pumps securing the fuel, first responders alerted, and so on
마지막으로, 잘 정의된 소비자 교육과 훈련이 있어야 한다
Further, there should be an automated data recording function or black box recorder
따라서 소비자 운전자와 승객을 테스트하고 훈련하는 동안 대체 운전자가 배치된 자율 시스템의 기능과 한계를 더 잘 이해할 수 있는 과정
It is very helpful to have this crash data to analyze and design systems that can avoid the specific kind of crash in the future, and to resolve questions about what went wrong, and who was at fault during the event
이 마지막 단계는 자동화에 대한 자연스러운 과신뢰를 보장하는 데 필수적이며, 얼리 어답터들이 불필요한 위험을 도입하지 않는다
Finally, there should be well-defined consumer education and training
이것들은 모든 회사가 작업해야 할 제안된 영역이라는 것을 명심하세요
So, courses for the fallback driver during testing and training for consumer drivers and passengers to better understand both the capabilities and limits of the deployed autonomous system
아직 필수 요건은 아니다
This final step is essential to ensuring our natural overconfidence in automation, does not lead to unnecessary hazards being introduced by early adopters
NHTSA의 주요 목표는 혁신을 과도하게 제한하지 않고 자율주행 자동차를 만드는 회사를 안내하는 것이다
Keep in mind that these are suggested areas that any company should work on
우리는 기술을 미리 선택하고 있다
Not mandatory requirements, yet
시장 진입이 등장하기 시작하면서, 안전 평가에 대한 더 확실한 요구 사항도 나타날 가능성이 높다
The main objective of the NHTSA is to guide companies building self-driving cars without overly restricting innovation
알았어
We're pre-selecting technologies
요약해 봅시다
As entrance to the market start to emerge, it is likely that more definitive requirements for safety assessment will also emerge
이 비디오에서, 우리는 자율주행 산업이 본 첫 번째 사고 중 몇 가지에 대해 논의했고, 자율 소프트웨어가 실패할 수 있는 여러 가지 방법을 밝혀냈다
Okay
그런 다음 우리는 공식적으로 피해, 위험, 위험 및 안전을 정의하고 자율주행 차량 위험의 주요 원인을 나열했습니다
Let's summarize
그런 다음 NHTSA 안전 프레임워크를 검토했습니다
In this video, we discussed a few of the first accidents that the self-driving industry has seen, and revealed the many ways in which autonomy software can fail
다음 비디오에서, 우리는 자율주행 안전에 대한 업계의 관점과 자율주행 자동차에 대한 몇 가지 안전 권장 사항에 대해 논의할 것입니다
We then formally defined harm, risk, hazard, and safety, and listed out the major sources of autonomous vehicle hazards
그때 보자
We then reviewed the NHTSA safety framework

In the next video, we'll discuss some industry perspectives on self-driving safety, as well as some safety recommendations for self-driving cars

See you then



