Welcome to the final video of this week
이번 주 마지막 비디오에 오신 것을 환영합니다
In this video, we will discuss some popular safety frameworks, some of which we encountered in the last lesson
이 비디오에서, 우리는 지난 수업에서 만난 몇 가지 인기 있는 안전 프레임워크에 대해 논의할 것입니다
More specifically, we will describe some generic, analytical frameworks including fault trees, failure modes and effects analyses or FMEA, and hazard and operability analysis or HAZOP
더 구체적으로, 우리는 오류 트리, 고장 모드 및 효과 분석 또는 FMEA, 위험 및 작동성 분석 또는 HAZOP을 포함한 몇 가지 일반적인 분석 프레임워크를 설명할 것입니다
Then we will focus on automotive and autonomous safety frameworks and discuss functional safety or FUSA, and safety of intended functionality, or SOTIF
그런 다음 우리는 자동차 및 자율 안전 프레임워크에 초점을 맞추고 기능 안전 또는 FUSA, 의도된 기능의 안전 또는 SOTIF에 대해 논의할 것입니다
We'll define these terms later on in the video
우리는 나중에 비디오에서 이 용어들을 정의할 것이다
Let's begin
시작하자
We'll start off with fault tree analysis
우리는 오류 트리 분석으로 시작할 것이다
Fault trees can be used as a preliminary analysis framework, and can be steadily expanded to encompass as much details necessary
결함 트리는 예비 분석 프레임워크로 사용될 수 있으며, 필요한 만큼의 세부 사항을 포함하도록 꾸준히 확장될 수 있다
Fault trees are top-down flows in which we analyze a possible failure of a system to be avoided, and then identify all of the ways in which it can occur from events and failures at lower levels of the system
오류 트리는 시스템의 가능한 실패를 분석한 다음 시스템의 낮은 수준의 이벤트와 실패로 인해 발생할 수 있는 모든 방법을 식별하는 하향식 흐름입니다
The top node in a fault tree is the root or top event
오류 트리의 상단 노드는 루트 또는 상단 이벤트입니다
The intermediate nodes in the fault tree are logic gates, that define possible causes for the root event
오류 트리의 중간 노드는 루트 이벤트의 가능한 원인을 정의하는 논리 게이트이다
The decomposition continues to a level of detail for which a probability of such an event can be defined
분해는 그러한 사건의 확률을 정의할 수 있는 세부 수준으로 계속된다
The fault tree can then be analyzed by combining the probabilities using the laws of Boolean logic
그런 다음 오류 트리는 부울 논리의 법칙을 사용하여 확률을 결합하여 분석할 수 있다
To assess the overall probability of root cause event and the causes that most contribute to its occurrence
근본 원인 사건의 전반적인 확률과 그 발생에 가장 기여하는 원인을 평가하기 위해
Let's consider a simple example, and take a car crash as our root event
간단한 예를 고려하고, 자동차 사고를 우리의 루트 이벤트로 삼자
The cause of a car crash could be broken down into either a software failure or a hardware failure, amongst many other possibilities that we've described as hazard classes in our earlier videos
자동차 충돌의 원인은 이전 비디오에서 위험 클래스로 설명한 다른 많은 가능성 중 소프트웨어 오류 또는 하드웨어 오류로 분류될 수 있습니다
Very crudely, the hardware failure could be because of manufacturing defects or material imperfections, for example
매우 조잡하게, 하드웨어 고장은 예를 들어 제조 결함이나 재료 결함 때문일 수 있다
Similarly, a software error could be due to malfunctioning perception code or some cybersecurity problem, say, if we were hacked
마찬가지로, 소프트웨어 오류는 오작동하는 인식 코드나 일부 사이버 보안 문제로 인한 것일 수 있습니다
From there, we can proceed to software subsystems and specific calculations within those subsystems deepening the tree at each successive branching
거기에서, 우리는 각 연속적인 분기에서 트리를 심화시키는 하위 시스템 내의 소프트웨어 하위 시스템과 특정 계산으로 진행할 수 있습니다
Ultimately, we'll arrive at specific failure rates for which we can assign probabilities of occurrence per hour or per mile of operation
궁극적으로, 우리는 시간당 또는 작동 마일당 발생할 확률을 할당할 수 있는 특정 실패율에 도달할 것이다
We have now arrived at the leaf nodes of the fault tree
우리는 이제 결함 트리의 잎 노드에 도착했다
Then using the logic gates structure, we can explicitly compute statistics of overall failure rates given assessments of the individual leaf node failure rates
그런 다음 논리 게이트 구조를 사용하여 개별 리프 노드 오류율에 대한 평가를 감안할 때 전체 실패율의 통계를 명시적으로 계산할 수 있습니다
The operations used to propagate these probabilities upwards would be the same as the rules of probability when events follow set theory
이러한 확률을 위쪽으로 전파하는 데 사용되는 연산은 사건이 집합 이론을 따를 때 확률 규칙과 동일할 것이다
So, for example, for independent events, the OR and AND probabilities would be the sum or product of children node probabilities
따라서, 예를 들어, 독립적인 사건의 경우, OR와 AND 확률은 자식 노드 확률의 합계 또는 곱이 될 것이다
This is the general idea behind fault trees, which are referred to as probabilistic fault trees, when probabilities are included at the leaf nodes
이것은 확률이 리프 노드에 포함될 때 확률적 오류 트리라고 불리는 오류 트리 뒤에 있는 일반적인 아이디어이다
Probabilistic fault trees are a top-down approach to safety that has been widely used in the nuclear and aerospace industries, and can similarly be applied to autonomous driving
확률적 단층 나무는 핵 및 항공 우주 산업에서 널리 사용되어 온 안전에 대한 하향식 접근 방식이며, 자율주행에도 마찬가지로 적용될 수 있다
The challenge lies in building a comprehensive tree and incorrectly identifying the probabilities of the leaf node events
문제는 포괄적인 트리를 만들고 리프 노드 이벤트의 확률을 잘못 식별하는 데 있다
Let's now look at FMEA, which stands for failure modes and effects analyses
이제 실패 모드와 효과 분석을 의미하는 FMEA를 살펴보겠습니다
Whereas fault trees flow down from a system failure to all of its possible causes, FMEA is a bottom-up process that looks at individual causes and determines all the possible effects that might occur
오류 트리는 시스템 오류에서 가능한 모든 원인으로 흘러내리는 반면, FMEA는 개별 원인을 살펴보고 발생할 수 있는 모든 가능한 효과를 결정하는 상향식 과정이다
Often, FTA's and FMEA's are used together to assess safety critical systems
종종 FTA와 FMEA는 안전에 중요한 시스템을 평가하기 위해 함께 사용된다
Failure modes are modes or ways in which a particular component of the overall system can cause the system to fail
고장 모드는 전체 시스템의 특정 구성 요소가 시스템을 실패시킬 수 있는 모드 또는 방법입니다
Effects analysis refers to analyzing all of the possible effects these mode failures can cause
효과 분석은 이러한 모드 실패가 일으킬 수 있는 모든 가능한 효과를 분석하는 것을 말한다
Often, the effects analysis seeks to identify those modes that bring about the most critical failures, which can then lead to improved designs that add more redundancy or higher reliability to the system
종종 효과 분석은 가장 중요한 실패를 초래하는 모드를 식별하려고 하며, 이는 시스템에 더 많은 중복성이나 더 높은 신뢰성을 추가하는 개선된 디자인으로 이어질 수 있다
Let's come to the big idea behind FMEA
FMEA의 큰 아이디어로 가자
The goal is to categorize failure modes by priority
목표는 우선 순위별로 실패 모드를 분류하는 것이다
So, we ask questions like, how serious are the effects, how frequently do these failures happen, and how easy is it to detect these failures
그래서, 우리는 그 효과가 얼마나 심각한지, 이러한 실패가 얼마나 자주 발생하는지, 그리고 이러한 실패를 감지하는 것이 얼마나 쉬운지와 같은 질문을 한다
Then we quantify all the failures using priority values, then we start addressing the failures with the highest priority first
그런 다음 우선 순위 값을 사용하여 모든 실패를 정량화한 다음, 우선 순위가 가장 높은 실패를 해결하기 시작합니다
Here are the steps
여기 단계가 있습니다
The goal is to construct a table of all possible risky situations, and we start off by, first discussing with field experts and identifying processes at the level of detail we want in the table
목표는 가능한 모든 위험한 상황의 테이블을 구성하는 것이며, 먼저 현장 전문가와 논의하고 테이블에서 원하는 세부 수준에서 프로세스를 식별하는 것으로 시작합니다
Then, we question the purpose of the system and list all failure possibilities
그런 다음, 우리는 시스템의 목적에 의문을 제기하고 모든 실패 가능성을 나열합니다
Then for each failure possibility, we identify the possible consequences and assign each consequence a severity rating between one and 10, 10 being the most severe
그런 다음 각 실패 가능성에 대해, 우리는 가능한 결과를 식별하고 각 결과에 가장 심각한 1에서 10 사이의 심각도 등급을 할당합니다
For each consequence, we identify the possible root causes, and for each route cause, we assign another number between one and 10, to denote how frequently this cause occurs
각 결과에 대해, 우리는 가능한 근본 원인을 식별하고, 각 경로 원인에 대해 이 원인이 얼마나 자주 발생하는지 나타내기 위해 1에서 10 사이에 다른 숫자를 할당합니다
Then, we identify all the ways in which the failure mode can be detected by operator, maintenance, inspection, or a fault detection system
그런 다음 작업자, 유지 보수, 검사 또는 오류 감지 시스템이 고장 모드를 감지할 수 있는 모든 방법을 식별합니다
We assess the overall mode detection likelihood before it causes an effect and assign another score from 1-10, with one being guaranteed to be detected and 10 being impossible to detect
우리는 효과를 일으키기 전에 전체 모드 감지 가능성을 평가하고 1-10에서 다른 점수를 할당하며, 하나는 감지되고 10은 감지할 수 없습니다
Finally, we compute a final number called the risk priority number, which is the product of the severity, the occurrence, and the detection
마지막으로, 우리는 심각도, 발생 및 탐지의 산물인 위험 우선 순위 번호라고 불리는 최종 숫자를 계산합니다
The higher this value is, the higher the priority is
이 값이 높을수록 우선순위가 높아진다
Eventually, we address the most problematic failure modes by modifying our implementation of the system until we reduce the risks to an acceptable level
결국, 우리는 위험을 수용 가능한 수준으로 줄일 때까지 시스템 구현을 수정함으로써 가장 문제가 되는 실패 모드를 해결합니다
It is also possible to perform FMEA with actual failure probabilities as in fault tree analysis, and to define acceptable risk levels in terms of the likelihood of a critical event occurring over a fixed period of operation
또한 오류 트리 분석과 같이 실제 실패 확률로 FMEA를 수행하고 고정 작동 기간 동안 중요한 사건이 발생할 가능성 측면에서 허용 가능한 위험 수준을 정의할 수 있습니다
The method doesn't change just the meaning of the numbers and the complexity of completing the entire analysis
이 방법은 숫자의 의미와 전체 분석을 완료하는 복잡성만을 바꾸지 않는다
Let's stick with the simple scoring approach and make the FMEA process more concrete with a brief example
간단한 채점 접근 방식을 고수하고 간단한 예시로 FMEA 프로세스를 더 구체적으로 만들어 봅시다
Consider, a specific failure where the vehicle has driven onto a gravel patch that appears in its test area due to road construction, which leads to controller instability
차량이 도로 공사로 인해 시험 구역에 나타나는 자갈 패치로 운전한 특정 고장을 고려하여 컨트롤러 불안정성으로 이어집니다
The worst-case effect could be a physical crash, which would be severity 10
최악의 경우 효과는 심각도 10인 물리적 충돌일 수 있다
It might also lead to driver discomfort, or a near miss, but these would be lower severity events
그것은 또한 운전자의 불편함이나 거의 놓칠 수 있지만, 이것들은 더 낮은 심각도 사건일 것이다
This event could happen regularly in urban environments wherever construction of a particular type occurs
이 행사는 특정 유형의 건설이 일어나는 모든 도시 환경에서 정기적으로 일어날 수 있다
So, it is somewhat likely
그래서, 그것은 다소 가능성이 있다
Let's say we're able to assess the occurrence number at four
4시에 발생 번호를 평가할 수 있다고 가정해 봅시다
Similarly, we can assign a current scores to the other effects
마찬가지로, 우리는 다른 효과에 현재 점수를 할당할 수 있다
Let's assume this problem is not currently detectable as the road surface texture is not actively monitored during operation of our autonomy software
자율 소프트웨어 작동 중에 도로 표면 텍스처가 적극적으로 모니터링되지 않기 때문에 이 문제가 현재 감지할 수 없다고 가정해 봅시다
So, detectability would be at number 10 for all of these effects
그래서, 탐지 가능성은 이 모든 효과에 대해 10위가 될 것이다
The risk priority number for a crash would then be 10 times 4 times 10, which is 400
충돌의 위험 우선 순위 번호는 10배 4배, 10배, 400이 될 것이다
In the same way, we could have other failure modes as well
같은 방식으로, 우리는 다른 실패 모드도 가질 수 있다
A sign perception failure with the priority number of a 100, let's say, a GPS synchronization failure with a priority number of 300, and maybe a vehicle motion prediction failure with the priority of 150
우선 순위 번호가 100인 기호 인식 실패, 우선 순위 번호가 300인 GPS 동기화 실패, 그리고 우선 순위가 150인 차량 모션 예측 실패일 수도 있습니다
So, we would go about addressing these failures in implementation by focusing on driving on gravel than GPS failure, than motion prediction, and finally sign perception
그래서, 우리는 모션 예측보다 GPS 실패보다 자갈로 운전하는 데 집중함으로써 이러한 구현 실패를 해결하고, 마침내 인식에 서명할 것이다
And so this is the general framework behind FMEA
그래서 이것이 FMEA의 일반적인 틀이다
FMEA is a risk assessment idea that was developed by the military and aerospace industries and later brought to the automotive industry
FMEA는 군사 및 항공 우주 산업에서 개발하고 나중에 자동차 산업에 도입된 위험 평가 아이디어이다
It provides a really structured way to quantify risks and deal with them
그것은 위험을 정량화하고 처리할 수 있는 정말 구조화된 방법을 제공한다
The most important first
가장 중요한 첫 번째
Lastly, a common variation on FMEA that appears frequently, is the Hazard and Operability Study or HAZOP
마지막으로, 자주 나타나는 FMEA의 일반적인 변형은 위험 및 작동성 연구 또는 HAZOP이다
HAZOP is more of a qualitative process as compared to FMEA, where we seek to define the risks quantitatively
HAZOP은 위험을 정량적으로 정의하고자 하는 FMEA에 비해 질적 과정에 가깝다

그래서, HAZOP에서, 주요 목적은 발생할 수 있는 일련의 가능한 위험에 대해 효과적으로 브레인스토밍하는 것이다

복잡한 프로세스의 경우, 발생, 심각도 및 탐지에 특정 값을 할당하지 않고도 위험을 평가할 수 있으며, 이는 어려울 수 있습니다
So, in HAZOP, the main purpose is to brainstorm effectively over the set of possible hazards that can arise
HAZOP은 종종 개념 설계 단계를 안내하기 위해 설계 프로세스 초기에 사용된다
For complex processes, the risks can be assessed without having to assign specific values to occurrence, severity and detection, which may be hard to do
HAZOP의 주요 추가 사항은 가이드 단어가 각 시스템 요구 사항에 적용되는 브레인스토밍을 이끄는 데 사용된다는 것이다
HAZOP is often used earlier in the design process to guide the conceptual design phase
이 가이드 단어에는 더 많이, 더 적게, 일찍, 늦은 것과 같은 것들이 포함되며, 그렇지 않으면 고려되지 않을 수도 있는 가능한 실패 모드로 이어진다
The key addition in HAZOP is that, guide words are used to lead the brainstorm applied to each system requirement
따라서 HAZOP을 단순화된 진행 중인 FMEA 브레인스토밍 접근법으로 생각하십시오
These guide words include things like not, more, less, early, late and lead to possible failure modes that might not otherwise be considered
이제 좀 더 구체적인 유형의 안전에 초점을 맞추고 자율주행차의 하드웨어 및 소프트웨어 오류를 평가하는 데 자주 사용되는 자동차 및 저수준 자율 기능 개발을 위한 기존 안전 프레임워크에 대해 논의합시다
So think of HAZOP as a simplified ongoing FMEA brainstorming approach
특히, ISO 26262에 설명된 기능 안전 접근 방식과 ISO에서 26262로 확장되고 ISOPAR 21448
Let's now focus on a more specific type of safety and discuss existing safety frameworks for automotive and low-level autonomy feature development, which are often used in assessing hardware and software failures in autonomous vehicles
1에 정의된 의도된 기능 접근 방식의 안전성에 대해 논의해 봅시다
In particular, let's discuss the functional safety approach described in ISO 26262 and the safety of intended functionality approach which extends on ISO to 26262 and is defined in ISOPAR 21448
우리는 두 과정 모두에 대해 크게 자세히 설명할 수 없지만, 더 알고 싶다면 보충 자료에 대한 링크를 포함시켰습니다
1
기능 안전 또는 FUSA는 자동차의 하드웨어 및 소프트웨어 고장이나 의도한 설계와 관련하여 발생하는 의도하지 않은 행동으로 인한 오작동으로 인한 불합리한 위험이 없는 것입니다
We won't be able to go into significant detail on either process, but I've included links to supplemental materials, if you'd like to learn more
ISO 262 표준은 자동차 내의 전기 및 전자 시스템에 대한 기능 안전 용어와 활동을 정의합니다
Functional Safety or FUSA, is the absence of unreasonable risk from malfunctioning behavior caused by failures of the hardware and software in a car, or unintended behaviors arising with respect to its intended design
따라서 자율주행 차량 안전에 영향을 미칠 수 있는 하드웨어 및 소프트웨어 위험만 해결합니다
The ISO 262 standard defines functional safety terms and activities for electrical and electronic systems within motor vehicles
이 표준은 네 가지 자동차 안전 무결성 수준 또는 ASIL을 정의한다
As such, addresses only the hardware and software hazards that can affect autonomous vehicle safety
ASIL D가 가장 엄격하고 A가 가장 적다
The standard defines four Automotive Safety Integrity Levels or ASIL
각 레벨은 인증을 위해 준수해야 하는 특정 개발 요구 사항과 관련이 있습니다
With ASIL D being the most stringent and A being the least
기능 안전 과정은 V자형 흐름을 따른다
Each level has associated with it specific development requirements, that must be adhered to for certification
요구 사항 사양으로 왼쪽 상단부터 시작하여 위험과 위험을 분석하고 기능 구현을 진행하십시오
The functional safety process follows a V-shaped flow
그런 다음 우리는 디자인 목표가 충족되었는지 확인하기 위해 올바른 지점에 올라갑니다
Starting at the top left with requirements specification then analysis of hazards and risks and proceeding to implementation of functionality
우리는 소프트웨어 단위 테스트와 같은 낮은 수준의 검증으로 시작한 다음 시뮬레이션, 테스트 트랙, 운영 및 온로드 테스트를 통해 하위 시스템 및 전체 시스템 검증을 진행합니다
We then climb up the right branch to confirm the design goals have been met
왼쪽의 V를 내려가면서, 높은 수준의 요구 사항은 낮은 수준의 구현으로 바뀝니다
We start with low-level verifications such as software unit tests, and then proceed to subsystem and full system validation through simulation, test track, operations and on-road testing
그리고 오른쪽의 V를 올라가면서, 안전한 작동을 위한 시스템 요구 사항을 확인하기 위해 결합하기 전에 각 저수준 함수 구현을 확인합니다
As we descend the V on the left, high-level requirements turn into low-level implementations
마지막 단계는 잔류 위험을 평가하고 시스템이 허용 가능한 수준의 안전 수준에 도달했는지 결정하기 위한 요약 기능 안전 평가입니다
And as we climb the V on the right, we confirm each low-level function implementation before combining them to confirm system requirements for safe operation
기능 안전 V가 시작될 때, 우리는 HARA 또는 위험 및 위험 평가를 사용합니다
The final step is a summary functional safety assessment, to evaluate residual risk and determine if our system has reached an acceptable level of safety
HARA에서는 위험한 사건을 식별하고 분류하고 불합리한 위험을 피하기 위한 요구 사항을 지정합니다
At the start of the functional safety V, we use HARA or Hazard and Risk Assessment
이 과정은 이 시점 이상의 모든 시스템 개발과 테스트를 주도한다
In HARA, we identify and categorize hazardous events and specify requirements to avoid unreasonable risk
이를 위해, 우리는 먼저 가능한 하드웨어 및 소프트웨어 결함이나 오작동과 자동차 안전에 영향을 미칠 수 있는 의도하지 않은 기능을 식별합니다
This process drives all of the system development and testing beyond this point
이것은 FMEA 또는 HAZOP이 기능 안전 프레임워크에 사용되고 우리 시스템에 특정 위험으로 이어지는 곳입니다
To do so, we first identify possible hardware and software faults or malfunctions and unintended functions that can affect car safety
그런 다음 시스템이 이 목록을 만들기 위해 ODD를 그릴 때 작동해야 하는 시나리오나 상황 목록을 정의합니다
This is where FMEA or HAZOP are used in the functional safety framework and leads to a specific set of hazards to our system
다음으로, 우리는 위험과 상황을 위험한 사건으로 결합하고, 예상 피해를 설명하고, 위험 매개 변수를 결정하여 상황과 위험의 각 조합에 대한 잠재적 위험의 수치 값을 계산합니다
We then define a list of scenarios or situations that the system must operate in drawing on our ODD to create this list
위험 평가 후, 우리는 가장 높은 위험 시나리오를 선택합니다
Next, we combine hazards and situations into hazardous events, describe expected damages, and determine risk parameters, to calculate numerical values of potential risk for each combination of situation and hazard
각각의 가능한 오작동과 관련하여 발생할 수 있는 최악의 사건
After the risk assessment, we choose the highest risk scenarios
마지막으로, 우리는 이러한 최악의 시나리오를 기반으로 안전 요구 사항을 정의합니다
The worst-case events that can happen with respect to each possible malfunction
HARA 프로세스는 발생할 수 있는 최악의 문제를 모두 인식하는 방식으로 시스템의 설계 목표를 설정합니다
Then finally, we define our safety requirements based on these worst-case scenarios
검증을 통해 이러한 최악의 경우 실패는 합리적인 위험으로만 처리된다는 것을 확인합니다
The HARA process sets the design goals for the system in a way that is aware of all of the worst-case failures that can occur
그리고 이것이 기능적 안전의 주요 아이디어이다
Through validation confirms that these worst-case failures are handled with only reasonable risk
최악의 요구 사항에 초점을 맞춘 다음 적어도 이러한 최악의 요구 사항을 처리할 수 있는 하드웨어와 소프트웨어를 구현합니다
And this is the main idea behind functional safety
마지막으로, ISOPAS 21448 문서에 공식적으로 정의된 의도된 기능 표준 또는 SOTIF의 안전성을 간략하게 살펴봅시다
You focus on worst-case requirements and then implement hardware and software that can at least handle these worst-case requirements
SOTIF는 특히 시스템 성능 제한과 시스템의 예측 가능한 오용과 관련된 실패 원인에 관심이 있다
Finally, let's briefly explore the Safety of Intended Functionality Standard or SOTIF, which is formally defined in the ISOPAS 21448 document
센서 성능 제한 및 소음과 같은 기술 제한 또는 물체 감지 실패 및 액추에이터 기술의 한계와 같은 알고리즘의 한계로 인해 구현된 기능의 성능 제한 또는 불충분
SOTIF is specifically concerned with failure causes related to system performance limitations and predictable misuse of the system
하드웨어 및 소프트웨어 오류는 ISO 26262의 기능 안전 표준에 의해 해결되며 SOTIF의 범위를 벗어납니다
Performance limitations or insufficiencies of the implemented functions due to technology limitations such as sensor performance limitations and noise, or limitations of algorithms such as object detection failures and limitations of actuator technology
SOTIF는 또한 사용자가 예측할 수 있는 오용으로 인해 안전하지 않은 작업을 다룹니다
Hardware and software failures are addressed by the functional safety standard in ISO 26262 and are out of the scope of SOTIF
사용자 혼란, 사용자 과부하 및 사용자 과신과 같은
SOTIF also addresses unsafe actions due to foreseeable misuse by the user
현재 SOTIF 표준은 자동화 수준인 0, 1 및 2를 목표로 한다
Such as user confusion, user overload and user overconfidence
또한 그 방법은 3단계, 4단계, 5단계 자율성에 적용될 수 있지만 추가 조치가 필요할 수 있다고 명시하고 있다
The current SOTIF standard targets automation levels, zero, one and two
SOTIF는 자율주행 기능의 문제를 해결하기 위해 특별히 설계된 기능 안전 프로세스의 확장으로 볼 수 있다
It also states that its methods can be applied to levels three, four, and five autonomy but additional measures may be required
따라서, 그것은 매우 동일한 V자형 개발 철학을 따르지만, 증강 구성 요소를 따른다
SOTIF can be seen as an extension of the functional safety process, specifically designed to address the challenges of automated driving functions
SOTIF는 또한 성능 제한과 오용으로 인해 발생하는 위험을 식별하기 위해 HARA를 사용합니다
As such, it follows very much the same V-shaped development philosophy, but with augmented components
그런 다음 안전 요구 사항이 충족되었는지 확인하기 위해 유사한 설계, 단위 테스트 및 검증 및 검증을 수행합니다
SOTIF also employs HARA to identify the hazards that arise from performance limitations and misuse
기능 안전 또는 SOTIF 표준에 대해 더 깊이 파고들고 싶다면, 보충 자료의 링크를 확인하세요
And then performs a similar sequence of design, unit testing and verification and validation, to confirm the safety requirements have been met
이 비디오에서 배운 것을 요약해 봅시다
If you'd like to dive deeper into either the functional safety or SOTIF standards, please check out the links in the supplemental materials
우리는 일반적인 안전 프레임워크에 대한 논의로 시작했다
Let's summarize what we've learned about in this video
안전 평가 및 고장 모드에 대한 하향식 접근 방식으로서의 결함 트리 분석 및 안전에 대한 상향식 접근 방식으로서의 효과 분석
We started off with a discussion of generic safety frameworks
그런 다음 소프트웨어 및 하드웨어 위험 평가에서 일반적으로 사용되는 기능 안전에 대한 아이디어를 논의하고 성능 제한과 오용을 설명하는 기능 안전의 확장으로 SOTIF에 대해 논의했습니다
Fault tree analysis as a top-down approach to safety assessment and failure modes and effects analysis as a bottom-up approach to safety
이러한 모든 아이디어는 안전 평가에서 거의 모든 기술을 사용하는 Waymo와 GM 모두에서 보았듯이 업계에서 많이 사용됩니다
Then we discussed the ideas of functional safety which are used commonly in software and hardware risk assessments and discussed SOTIF as an extension to functional safety, that accounts for performance limitations and misuse
축하해
All of these ideas are used a lot in the industry, as we saw with both Waymo and GM which use nearly all of these techniques in their safety assessments
이 안전 평가 모듈이 끝날 때까지 완료했습니다
Congratulations
우리가 이번 주에 배운 것을 요약해 봅시다
You've made it to the end of this safety assessment module
우리는 안전이 왜 중요한지, 특히 광범위한 뚜렷한 실패가 자율주행 사고로 이어질 수 있는지에 대한 논의로 시작했다
Let's summarize what we learned this week
그런 다음 우리는 공식적으로 안전 개념을 정의하고 자율주행 차량에 대한 NHTASA의 안전 권장 사항에 대해 논의했습니다
We started off with discussions on why safety is important specifically how a broad range of distinct failures can lead to self-driving accidents
그런 다음 웨이모와 GM이 자율주행 안전에 대해 어떻게 생각하는지 논의했다
Then we formally defined safety concepts and discussed the NHTASA's safety recommendations for autonomous vehicles
그런 다음 우리는 안전을 입증하기 위한 분석 및 데이터 중심의 접근 방식을 설명했습니다
We then discussed how Waymo and GM think about self-driving safety
마지막으로, 오늘의 비디오에서, 우리는 일반적인 안전 평가 프레임워크에 대해 논의했다
Then we described analytic and data-driven approaches to demonstrating safety
결함 트리, 고장 모드 및 효과 분석, 기능 안전 및 의도된 기능의 안전을 포함합니다
Finally, in today's video, we discussed common safety assessment frameworks
바라건대, 이번 주에 안전한 자율주행 시스템을 설계하고 구축한 시스템을 적절하게 평가하는 데 대한 통찰력을 제공하기를 바랍니다
Including fault trees, failure modes and effects analysis, functional safety and safety of intended functionality
이번 주에 마무리하기 전에, 우리는 자율 안전 평가 전문가인 워털루 대학교의 Krzysztof Czarnecki 교수와 논의할 것입니다
Hopefully, this week give you insight into designing safe self-driving systems and into properly assessing the systems you built
나는 물어볼 흥미로운 질문이 많다
Before we wrap up this week, we'll have a discussion with Professor Krzysztof Czarnecki from the University of Waterloo, an expert on autonomous safety assessment
계속 지켜봐 주세요
I have lots of interesting questions to ask

Stay tuned



