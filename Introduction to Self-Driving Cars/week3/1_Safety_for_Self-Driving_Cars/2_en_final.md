Welcome to the second lesson this week
이번 주 두 번째 수업에 오신 것을 환영합니다
In this lesson, we will discuss the various industry perspectives on safety and testing
이 수업에서, 우리는 안전과 테스트에 대한 다양한 산업적 관점에 대해 논의할 것이다
Specifically, we'll first analyze the safety perspectives of two big names in the industry: Waymo and GM
특히, 우리는 먼저 업계의 두 유명 인사인 Waymo와 GM의 안전 관점을 분석할 것이다
Then we'll discuss two different approaches to assessing safety: analytical versus empirical
그런 다음 우리는 안전을 평가하기 위한 두 가지 접근 방식에 대해 논의할 것이다: 분석 대 경험적
Let's begin
시작하자
As we saw in the last video, the NHTSA requested that each self-driving developer, should develop and describe a comprehensive safety strategy that covered the 12 concepts included in their guidance document
지난 비디오에서 보았듯이, NHTSA는 각 자율주행 개발자가 지침 문서에 포함된 12가지 개념을 다루는 포괄적인 안전 전략을 개발하고 설명해야 한다고 요청했다
To date, two prominent reports have emerged from Waymo and GM, and we'll use both as our basis for our discussion of industry approaches to safety
지금까지 웨이모와 GM에서 두 개의 저명한 보고서가 나왔고, 우리는 둘 다 안전에 대한 산업 접근 방식에 대한 논의의 기초로 사용할 것이다
The Waymo Safety Report was released in 2017, and has a lot of great insight into how to organize a comprehensive safety strategy for self-driving cars
웨이모 안전 보고서는 2017년에 발표되었으며 자율주행 자동차를 위한 포괄적인 안전 전략을 구성하는 방법에 대한 많은 통찰력을 가지고 있다
Waymo covers all 12 of the NHTSA concepts, but organizes them into a five level safety approach
웨이모는 12가지 NHTSA 개념을 모두 다루지만, 5단계 안전 접근 방식으로 구성한다
First, Waymo systems are designed to perform safe driving at the behavioral level
첫째, 웨이모 시스템은 행동 수준에서 안전한 운전을 수행하도록 설계되었습니다
This includes decisions that follow the traffic rules, can handle a wide range of scenarios within the ODD, and maintain vehicle safety through it
여기에는 교통 규칙을 따르고, ODD 내에서 광범위한 시나리오를 처리할 수 있으며, 이를 통해 차량 안전을 유지하는 결정이 포함됩니다
Second, Waymo ensures that the systems have backups and redundancies
둘째, Waymo는 시스템에 백업과 중복이 있는지 보장한다
This is so that even if a fault or failure occurs, the car can switch to a secondary component or a backup process to minimize the severity of failures and return the vehicle to a safe state, continuing the drive if possible
이것은 결함이나 고장이 발생하더라도 자동차가 보조 구성 요소나 백업 프로세스로 전환하여 고장의 심각성을 최소화하고 차량을 안전한 상태로 되돌릴 수 있으며, 가능하면 드라이브를 계속할 수 있습니다
This is referred to as Functional Safety
이것은 기능 안전이라고 불린다
Next, Waymo emphasizes crash safety as recommended by the NHTSA
다음으로, 웨이모는 NHTSA가 권장하는 충돌 안전을 강조한다
It designs systems that ensure minimum damage to people inside the car in the event of a crash
충돌 시 차 안에 있는 사람들에게 최소한의 손상을 보장하는 시스템을 설계합니다
Next, it tries to ensure Operational Safety
다음으로, 그것은 운영 안전을 보장하려고 노력한다
So, that means its interfaces are usable and convenient and intuitive
그래서, 그것은 인터페이스가 유용하고 편리하며 직관적이라는 것을 의미합니다
The focus here is on allowing passengers to have some level of control over the vehicle, but only in ways that maintain system safety
여기서 초점은 승객들이 차량에 대한 어느 정도 통제할 수 있도록 하는 것이지만, 시스템 안전을 유지하는 방식으로만 하는 것이다
Finally, Waymo fosters Non-collision safety
마지막으로, 웨이모는 충돌 방지 안전을 촉진한다
This refers to system designs that minimize the danger to people that may interact with the system in some way, first responders, mechanics, hardware engineers, and so on
이것은 어떤 식으로든 시스템과 상호 작용할 수 있는 사람들, 최초 대응자, 역학, 하드웨어 엔지니어 등에 대한 위험을 최소화하는 시스템 설계를 의미합니다
These five pillars form Waymo's safety by design system, and leads to a system of extensive requirement definition, design iteration, and testing to ensure that the objectives of the system are met by each component
이 다섯 개의 기둥은 설계 시스템에 의한 웨이모의 안전을 형성하며, 시스템의 목표가 각 구성 요소에 의해 충족되도록 광범위한 요구 사항 정의, 설계 반복 및 테스트 시스템으로 이어집니다
The process uses several tools from existing domains and we'll go into more details of these tools in the next video
이 프로세스는 기존 도메인의 여러 도구를 사용하며 다음 비디오에서 이러한 도구에 대한 자세한 내용을 살펴보겠습니다
At the outset, the Waymo team identifies as many hazard scenarios as possible and analyzes possible mitigation strategies for each, that is, how to ensure that the vehicle can still reach a safe state when a hazard occurs
처음에 웨이모 팀은 가능한 한 많은 위험 시나리오를 식별하고 각각에 대한 가능한 완화 전략, 즉 위험이 발생할 때 차량이 여전히 안전한 상태에 도달할 수 있도록 하는 방법을 분석합니다
Then, they use a hazard assessment method to identify more specific safety requirements
그런 다음, 그들은 더 구체적인 안전 요구 사항을 식별하기 위해 위험 평가 방법을 사용합니다
The various methods they use are preliminary analysis of possible safety risk, a fault tree hazard assessment which works from the top down in terms of the dynamic driving task, and some design failure modes and effects analysis which works from the bottom-up assessing the effects of small subsystem failures on the overall capabilities of the system
그들이 사용하는 다양한 방법은 가능한 안전 위험에 대한 예비 분석, 동적 운전 작업 측면에서 위에서 아래로 작동하는 결함 트리 위험 평가, 작은 하위 시스템 고장이 시스템의 전반적인 기능에 미치는 영향을 평가하는 상향식에서 작동하는 일부 설계 고장 모드와 효과 분석이다
Finally, they perform lots of testing to ensure that the requirements are met
마지막으로, 그들은 요구 사항이 충족되는지 확인하기 위해 많은 테스트를 수행합니다
Let's discuss the kind of testing procedures that Waymo follows specifically to evaluate its software, as it is the most publicly visible and well-documented program out there
Waymo가 가장 공개적으로 눈에 띄고 잘 문서화된 프로그램이기 때문에 소프트웨어를 평가하기 위해 특별히 따르는 테스트 절차에 대해 논의해 봅시다
First, they test all software changes in simulation on the order of 10 million miles of simulation per day
첫째, 그들은 하루에 천만 마일의 시뮬레이션 순서로 시뮬레이션의 모든 소프트웨어 변화를 테스트합니다
This represents an enormous computing effort running continuously to confirm the expected improvements to safety requirements for the system
이것은 시스템의 안전 요구 사항에 대한 예상 개선을 확인하기 위해 지속적으로 실행되는 엄청난 컴퓨팅 노력을 나타낸다
To do this, they mine all of their on-road experiences for challenging scenarios and perform systematic scenario fuzzing, which changes the position and velocity parameters of other vehicles and pedestrians randomly, so they can test if the ego-vehicle behaves safely throughout all of them
이를 위해, 그들은 도전적인 시나리오에 대한 모든 온로드 경험을 채굴하고 체계적인 시나리오 퍼징을 수행하여 다른 차량과 보행자의 위치와 속도 매개 변수를 무작위로 변경하여 자아 차량이 모두 안전하게 작동하는지 테스트할 수 있습니다
This approach is particularly useful for finding hard edge cases, with hard to resolve time gaps for merging or crossing intersections for example
이 접근 방식은 예를 들어 교차로를 병합하거나 건너기 위한 시간 간격을 해결하기 어려운 하드 에지 케이스를 찾는 데 특히 유용합니다
Then they do Closed-course Testing, in which they test their software on private tracks
그런 다음 비공개 트랙에서 소프트웨어를 테스트하는 폐쇄 과정 테스트를 수행합니다
They cover 28 core scenarios as identified by an UC Berkeley study, as well as 19 additional scenarios that Waymo added
그들은 UC 버클리 연구에서 확인된 28개의 핵심 시나리오와 웨이모가 추가한 19개의 추가 시나리오를 다룹니다
These scenarios are organized around avoiding the four most common accident scenarios which are rear-end, intersection, road departure, and lane change
이러한 시나리오는 후방, 교차로, 도로 출발 및 차선 변경이라는 네 가지 가장 일반적인 사고 시나리오를 피하는 것으로 구성되어 있다
There are obviously many variations of each of these categories but together they account for over 84 percent of all crashes
분명히 각 범주에는 많은 변형이 있지만 함께 모든 충돌의 84% 이상을 차지한다
Finally, they do real-world testing which are regularly seen on the streets of many different cities in the United States, including Mountain View California right near the main Google campus
마지막으로, 그들은 메인 구글 캠퍼스 바로 근처의 마운틴 뷰 캘리포니아를 포함하여 미국의 여러 도시의 거리에서 정기적으로 볼 수 있는 실제 테스트를 한다
This testing allows them to identify more and more cases that are out of the ordinary and primarily rely on the dynamic driving task fallback strategy of having humans monitor the autonomy software during testing
이 테스트를 통해 그들은 평범하지 않은 점점 더 많은 사례를 식별하고 주로 인간이 테스트 중에 자율 소프트웨어를 모니터링하도록 하는 동적 운전 작업 대체 전략에 의존할 수 있다
The combination of these strategies for testing is by no means unique to Waymo, but has emerged as the de facto standard as it provides the maximum flexibility and feedback for a fixed investment, focusing each test method on what it does best, simulation on manipulating scenarios that make them hard, closed-course testing on confirming specific gains in safety performance and real-world testing on finding evermore challenging scenarios, and increasing public confidence in the technology
이러한 테스트 전략의 조합은 결코 Waymo에만 국한된 것은 아니지만, 고정 투자에 대한 최대한의 유연성과 피드백을 제공하고, 각 테스트 방법을 가장 잘하는 것에 초점을 맞추고, 안전 성능의 특정 이득을 확인하고 점점 더 도전적인 시나리오를 찾기 위한 실제 테스트에 대한 폐쇄적인 테스트를 조작하고, 기술에 대한 대중의 신뢰를 높이기 때문에 사실상 표준으로 부상했습니다
Okay
알았어
Now let's turn our attention to the safety ideology for General Motors, who acquired Cruise Automation in 2016 and has propelled itself to a leading position in self-driving development as a result
이제 2016년에 크루즈 오토메이션을 인수하고 결과적으로 자율주행 개발에서 선도적인 위치로 성장한 제너럴 모터스의 안전 이데올로기에 주목합시다
GM strategy follows the NHTSA safety framework very closely and addresses each of the 12 main areas individually
GM 전략은 NHTSA 안전 프레임워크를 매우 밀접하게 따르고 12개의 주요 영역을 개별적으로 다룹니다
GM's safety strategy does not try to reorganize or simplify the NHTSA guidance, but instead focuses on its implementation strategies for achieving the required safety assessments
GM의 안전 전략은 NHTSA 지침을 재구성하거나 단순화하려고 하지 않고, 대신 필요한 안전 평가를 달성하기 위한 구현 전략에 초점을 맞추고 있다
First and foremost, GM emphasized their iterative design model, in which the first analyze scenarios, then build software, then simulate the scenarios, and test their software
무엇보다도, GM은 먼저 시나리오를 분석한 다음 소프트웨어를 구축한 다음 시나리오를 시뮬레이션하고 소프트웨어를 테스트하는 반복적인 설계 모델을 강조했다
Finally, deploy their software on real world cars, and they keep adding improvements and refinements to both the requirements and the autonomous system iteratively
마지막으로, 실제 자동차에 소프트웨어를 배포하고, 요구 사항과 자율 시스템 모두에 개선 사항과 개선을 계속 반복적으로 추가합니다
Second, whereas Waymo relies on OEMs to design its vehicles and only discusses mechanical and electrical hazards related to its autonomy hardware, GM manufactures their cars entirely themselves and so can enforce a more integrated design with consistent quality standards throughout the self-driving hardware
둘째, 웨이모는 OEM에 의존하여 차량을 설계하고 자율 하드웨어와 관련된 기계적 및 전기적 위험만 논의하는 반면, GM은 자동차를 완전히 스스로 제조하므로 자율주행 하드웨어 전반에 걸쳐 일관된 품질 표준으로 보다 통합된 설계를 시행할 수 있다

다음으로, GM은 포괄적인 위험 관리 계획을 통해 안전을 보장한다

그들은 위험을 식별하고 해결하며 단지 완화할 뿐만 아니라 완전히 제거하려고 노력한다

마지막으로, 그들의 모든 시스템은 내부적으로 잘 정의된 안전, 신뢰성, 보안 표준을 따른다
Next, GM ensures safety through a comprehensive risk management scheme
그들은 자동차 산업에서 차량을 개발한 다년간의 경험을 가지고 있으며, 결과적으로 광범위한 안전 프로세스를 개발했다
They identify and address risks and try to eliminate them completely and not just mitigate them
그들의 안전 프로세스는 세 가지 유형의 분석을 포함한다
Finally, all their systems follow there internally well defined standards of safety, reliability, security, and so on
첫째, 그들은 오류 트리 방법을 통해 연역 분석을 수행하고 결함이 있고 해결할 수 있는 구성 요소를 정확히 찾아냅니다
They have years of experience of developing vehicles in the automotive industry, and have developed extensive safety processes as a result
다음으로, 그들은 설계, FMEA를 통해 유도 분석을 수행합니다
Their safety processes involve three types of analysis
그래서, 그들은 실패 모드와 설계 제안에 영향을 분석하고, 아래에서부터 안전을 보장하려고 노력한다
First, they perform deductive analysis through the fault tree method and pinpoint components that could possibly have faults and address them
마지막으로, 그들은 위험 및 작동성 연구를 사용하여 탐색 분석을 수행하고 시스템이 잠재적으로 예상대로 작동하지 않을 수 있는 시기를 파악합니다
Next, they perform inductive analysis through design, FMEA
이제, 이것은 모두 친숙하게 들릴 수 있으며, 실제로, 이것들은 Waymo가 설명하는 것과 같은 분석 기둥이다
So, they do a failure modes and effect analysis on their design proposals, and try to ensure safety from the bottom up
다음 비디오에서, 우리는 이러한 방법들이 실제로 어떻게 작동하는지에 대한 자세한 내용을 살펴볼 것이다
Finally, they employ hazard and operability studies to perform exploratory analysis, and figure out when the system may potentially not work as expected
안전 임계값과 GM 차량에 대해 이야기해 봅시다
Now, this may all sound familiar and indeed, these are the same pillars of analysis that Waymo describes
모든 GM 차량은 적어도 두 가지 중요한 안전 임계값을 따라야 한다
In the next video, we'll go through more details on how these methods actually work
첫째, GM은 고장 후에도 시스템이 계속 작동하도록 다양한 구성 요소에 대한 명확한 장애 금고, 백업 시스템 및 중복 세트를 정의합니다
Let's talk about safety thresholds and GM vehicles
둘째, 구성 요소는 다음 비디오에서 더 자세히 논의할 SOTIF 평가를 통과해야 합니다
All GM vehicles have to follow two critical safety thresholds at the very least
이 평가를 통해, 우리는 모든 중요한 기능이 알려진 시나리오와 알려지지 않은 시나리오 모두에서 평가되도록 보장합니다
First, the GM defines a clear set of fail safes, back-up systems, and redundancies for different components so that the system continues to work even after a failure
마지막으로, GM은 성능 테스트, 요구 사항 검증, 결함 주입, 침입 테스트 및 내구성 테스트, 시뮬레이션 기반 테스트로 구성된 엄격한 테스트 메커니즘을 따릅니다
Second, the components must pass the SOTIF evaluation which we'll discuss in more detail in the next video
이 두 회사 모두 안전 표준을 엄격하게 따르므로 실질적이고 효과적으로 안전을 수행하는 방법에 대한 좋은 예입니다
With this evaluation, we ensure that all critical functionalities are evaluated in both known and unknown scenarios
그래서, 우리는 이제 업계에서 안전 평가가 어떻게 수행되는지에 대한 더 명확한 그림을 가지고 있지만, 여전히 이 질문이 남아 있습니다: 자율주행차가 안전한지 진정으로 정확하게 평가하는 것이 정말 가능한가요
Finally, GM follows a rigorous testing mechanism consisting of performance testing, requirements validation, fault injection, intrusive testing, and durability tests, and simulation-based testing
아니면 적어도 인간 운전자보다 안전한가요
Both these companies rigorously follow safety standards and are therefore great examples of how to do safety practically and effectively
자율주행 시스템의 안전성을 평가하는 데 사용할 수 있는 다양한 접근 방식에 대해 논의해 봅시다
So, we now have a clearer picture of how safety assessment is performed in industry, but we're still left with this question: is it really possible to truly precisely assess whether an autonomous car is safe
우리는 두 가지 가능한 접근 방식을 가지고 있습니다: 분석 또는 데이터 기반 안전 평가
Or at least safer than a human driver
분석 안전 평가를 통해, 우리는 위험과 시나리오에 대한 중요한 평가를 기반으로 정량화 가능한 안전 성능 또는 실패율을 정의하기 위해 시스템을 분석할 수 있다는 것을 의미합니다
Let's discuss the various approaches that can be used to assess the safety of an autonomous driving system
분석을 통해 전반적인 시스템 고장률을 결정할 수 있다면, 시스템의 어떤 측면이 전반적인 안전에 가장 큰 기여자인지에 대한 강력한 지침을 제공할 수 있다
We have two possible approaches: analytical or data-driven safety assessment
좋은 예는 분석 실패율의 초기 추정치가 100,000편의 항공편 중 하나로 고정된 우주왕복선 프로그램이다
By analytical safety assessment, we mean that the system can be analyzed to define quantifiable safety performance or failure rates based on critical assessment of hazards and scenarios
그러나 프로그램이 끝난 후, 법의학 연구에 따르면 초기 셔틀 프로그램 비행은 실패율이 10명 중 1에 가까웠고, 이는 프로그램이 끝날 때까지 100명 중 1로만 진행되었다
If the overall system failure rates can be determined through analysis, it can provide strong guidance on which aspects of the system are the biggest contributors to overall safety
셔틀 발사에 들어가는 수천 개의 하위 시스템과 이러한 시스템의 작동에 영향을 미칠 수 있는 수백만 개의 변수를 고려할 때 그러한 복잡한 시스템에서 그러한 분석이 가능하다는 것은 놀라운 일이다
A great example is the Space Shuttle program for which initial estimates of analytical failure rates were pegged at one in 100,000 flights
이러한 종류의 상세한 분석은 자율주행 자동차에도 적용 가능하지만, 차량에 국한된 차량의 무한한 다양한 상황으로 인해 틀림없이 더 복잡할 수 있다
After the program ended however, a forensic study revealed that early shuttle program flights had failure rates closer to one in 10, and that this only progressed to one in a hundred by the end of the program
결국, 분석 방법은 자율주행 시스템의 안전 성능에 대한 지침만 제공할 수 있으며, 그 결과는 경험을 통해 검증되어야 한다
It is a marvel that such analysis is even possible for such a complex system when considering all of the thousands of subsystems that go into a shuttle launch, and all of the millions of variables that can affect the operations of these systems
경험을 평가하기 위해, 우리는 데이터 기반 테스트를 사용합니다
This sort of detailed analysis is also applicable to self-driving cars, but may arguably be more complex due to the infinite variety of situations of vehicle confined itself in
이것은 특정 버전의 소프트웨어를 사용하여 운영 설계 도메인에 포함된 일련의 도로와 시나리오에서 원하는 실패율을 달성할 수 있다는 것을 증명했기 때문에 시스템이 안전하다는 것을 확신하는 개념입니다
In the end, analytic methods can only provide guidance on the safety performance of the self-driving system, and their results need to be validated through experience
자율주행의 경우, 이러한 원하는 고장율은 인간 수준의 운전 성과와 연관될 수 있으며, 오늘날 운전자의 성능에 비해 사고를 10배 또는 100배 줄이기를 희망합니다
To evaluate experience, we use data-driven testing
그래서, 데이터는 무엇을 말하나요
This is the concept whereby we are assured that the system is safe because it has demonstrated that, using a specific version of the software, it can achieve desired failure rates on a set of roads and scenarios that are included in the operational design domain
자율주행차가 실제로 더 안전한가요
In the case of self-driving, these desired failure rates can be tied to human level driving performance, where we hope to reduce accidents by 10x or 100x over the performance of today's drivers
첫째, 운전이 인간의 기준으로 여전히 위험하다는 것을 알아라
So, what does the data say
2015년 보고서는 운전의 모든 사망자 중 약 90%가 인간의 실수, 때로는 판단력 부족, 때로는 인간 인식 등의 실패 등으로 인해 발생했다고 결론지었다
Are autonomous cars actually safer
그러나 인간은 또한 운전을 매우 잘하며, 실제로 전체 운전 환경은 인간의 인식과 계획 능력을 기반으로 설계되었습니다
First, know the driving is still dangerous by human standards
미국에서는 1억 4천 6백만 킬로미터당 약 1명의 사망자가 발생한다
A report in 2015 concluded that of all the fatalities in driving, about 90 percent of these occurred due to human errors, sometimes through a lack of judgment, sometimes through a failure of human perception, et cetera
210만 킬로미터당 한 번의 부상과 400,000km당 약 1건의 충돌
But humans are also extremely good at driving, and indeed, the entire driving environment has been designed based on human perception and planning abilities
이 마지막 숫자는 대부분의 작은 충돌이 실제로 보고되지 않기 때문에 추정된다
In the United States, there is roughly one fatality per 146 million kilometres driven
사실, 자율주행은 우리가 사용할 수 있는 추가 센서로 훨씬 더 포괄적인 보고와 재건이 가능하기 때문에 이러한 통계를 더 밝히기 위해 많은 일을 할 수 있다
One injury per 2
이제 예비 자율주행 차량 통계, 더 구체적으로는 캘리포니아에서 테스트되는 모든 자율주행 차량이 발표한 이탈률을 고려해 봅시다
1 million kilometres driven, and approximately one collision per 400,000 kilometres
이탈은 이 자율 소프트웨어가 운전자에게 통제권을 요청하거나 안전 운전자가 개입할 필요성을 느낄 때이다
This last number is only estimated as most smaller collisions are not actually reported
민감한 통계이기 때문에 테스트 중인 전체 함대에 대한 진정한 충돌 통계를 얻는 것은 당연히 어렵다
In fact, autonomous driving may do a lot to shed more light on these statistics as much more comprehensive reporting and reconstruction will be possible with the additional sensors available to us
다행히도, 캘리포니아에서의 테스트는 몇 가지 유용한 보고 요구 사항과 함께 제공됩니다
Now, let's consider the preliminary self-driving vehicle statistics, more specifically, the disengagement rates published by all autonomous driving vehicles being tested in California
2017년에 웨이모는 캘리포니아에서 563,000km를 운전했고 9,000km마다 약 1번의 이탈률로 63번의 이탈을 경험했다
A disengagement is when either this autonomy software requests the driver to take over control or the safety driver feels the need to intervene
GM 크루즈는 캘리포니아에서 210,000km를 운전했고 약 2,000km마다 105개의 이탈을 했다
It is understandably challenging to get true crash statistics for the entire fleets being tested as these are sensitive statistics
둘 다 일년 내내 빠르게 개선되어 12,500킬로미터마다 한 번, 그리고 연중 마지막 3개월 동안 각각 8,300킬로미터마다 이탈률에 도달했다
Fortunately, testing in California comes along with some useful reporting requirements
이것들은 인간 성과와 관련된 어려운 숫자이지만 대략 전형적인 통근자가 자율 체계의 실패를 위해 일 년에 한 번만 개입해야 한다는 것을 의미한다
In 2017, Waymo drove 563,000 kilometres in California and experienced 63 disengagement for a rate of roughly one disengagement every 9,000 kilometres
이것은 엄청난 진전이지만 여전히 인간이 매년 수조 마일로 달성하는 충돌 사이의 400,000km에서 벗어난 방법이다
GM Cruise drove 210,000 kilometres in California with 105 disengagement for roughly one every 2,000 kilometres
주파수 순서대로 63개의 웨이모 이탈의 주요 원인은 원치 않는 차량 기동, 인식 불일치, 하드웨어 문제, 소프트웨어 문제, 행동 예측, 그리고 마지막으로 무모한 도로 사용자의 단일 사례였다
Both were improving quickly throughout the year reaching disengagement rates of once every 12,500 kilometres, and every 8,300 kilometres respectively for the last three months of the year
인식, 예측 및 행동 계획의 핵심 과제는 여전히 도전적인 문제로 남아 있으며, 여전히 많은 작업이 이루어져야 한다는 것은 분명하다
These are hard numbers to relate to in terms of human performance but roughly mean that a typical commuter would only have to intervene once a year for a failure of the autonomy system
마지막으로, 통계적 중요성에 관한 한 마디
This is enormous progress but also still a ways off from the 400,000 kilometres between crashes that humans achieve on trillions of miles every year
오늘날의 함대에서 관찰된 성능은 인상적이지만, 인간의 능력과 얼마나 잘 비교하는가
The primary causes of the 63 Waymo disengagements in order of frequency, were unwanted vehicle manoeuvres, perception discrepancies, hardware issues, software issues, behavior predictions, and finally, a single case of a reckless road user
자율주행차가 특히 사망자 측면에서 인간 운전자보다 안전하다는 것을 증명하기 위해 몇 마일을 운전해야 하나요
It's clear that the core tasks of perception, prediction and behavior planning remain challenging problems, and much work still needs to be done
보충 자료에, 우리는 이 문제를 해결하려고 시도하는 Rand Corporation의 보고서에 대한 링크를 포함시켰고, 그 숫자는 놀랍다
Lastly, a word about statistical significance
사망자는 매우 드문 사건이며 수많은 요인이 고려되고 있기 때문에, 보고서는 자율주행 시스템의 안전 사례를 검증하는 데 순수한 도로 테스트를 사용한다면 80억 마일 이상이 필요할 것이라고 명시하고 있다
The performance observed from today's fleet are impressive, but how well do they represent an accurate comparison to human capabilities
연중무휴로 여행하는 100대의 차량으로 그렇게 하려면 적어도 400년이 걸릴 것이다, 기다리는 데 오랜 시간이 걸린다
How many miles do we really need to drive to demonstrate autonomous vehicles are safer than human drivers, particularly in terms of fatalities
이러한 이유로 우리는 안전에 대한 다각적인 접근 방식을 보고 있으며, 모든 회사는 도로에서 자율 시스템으로 얻은 경험을 높이기 위해 차량 함대를 확장하고 있다
In the supplemental material, we've included a link to a report by Rand Corporation that attempts to address this question, and the numbers are startling
요약하자면, 이 비디오에서, 우리는 자율주행 안전 평가에 대한 두 가지 업계 관점을 살펴보았고, Waymo와 GM, 다른 산업에서 빌린 많은 방법을 발견했다
Since fatalities are such rare events and with a numerous factors under consideration, the report states that upwards of 8 billion miles would be needed if pure on road testing is used to validate the safety case for a self-driving system
우리는 인간의 성과보다 더 나은 것을 보여주기 위해 현재의 이탈률과 도로 테스트 요구 사항에 대해 논의했다
It would take at least 400 years to do so with a fleet of 100 vehicles traveling 24/7, that's a long time to wait
다음 수업에서, 우리는 가장 일반적으로 사용되는 몇 가지 안전 프레임워크와 방법론을 탐구할 것입니다
It is for this reason that we see such multifaceted approaches to safety, and every company is expanding vehicle fleets to increase the experience gained with autonomous systems on the road
거기서 보자
To summarize, in this video, we looked at two industry perspectives on autonomous driving safety assessment, Waymo and GM, and found many methods borrowed from other industries

We discussed the current disengagement rates and road testing requirements to demonstrate better than human performance

In the next lesson, we'll explore a few of the most commonly used safety framework and methodologies

We'll see you there



