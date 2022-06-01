
Welcome to the third and final video of this week. 
이번 주 세 번째이자 마지막 비디오에 오신 것을 환영합니다. 

In this video, we will be discussing decision-making in the self-driving car system. 
이 비디오에서, 우리는 자율주행 자동차 시스템의 의사 결정에 대해 논의할 것이다. 

Recall that in the last video, we discussed the perception which forms the first step in performing a driving task. 
마지막 비디오에서, 우리는 운전 작업을 수행하는 첫 번째 단계를 형성하는 인식에 대해 논의했다는 것을 기억하세요. 

The other steps in driving include decision-making and then, finally, executing the decisions. 
운전의 다른 단계에는 의사 결정과 마지막으로 결정을 실행하는 것이 포함된다. 

In this video, we will categorize planning informally on the basis of the window of time over which the decision has to be made and discuss some examples. 
이 비디오에서, 우리는 결정을 내려야 하는 시간을 기준으로 비공식적으로 계획을 분류하고 몇 가지 예를 논의할 것입니다. 

Then we will go over a simple intersection scenario and try to list out some of the various decisions needed to complete the driving task successfully. 
그런 다음 간단한 교차로 시나리오를 살펴보고 운전 작업을 성공적으로 완료하는 데 필요한 다양한 결정을 나열하려고 노력할 것입니다. 

We will then categorize planning formerly based on the type of logic we use to make the decisions. 
그런 다음 우리는 결정을 내리는 데 사용하는 논리의 유형에 따라 이전에 계획을 분류할 것이다. 

So, is our logic made up of well-defined rules that react only to currently available information about the driving environment? 
그래서, 우리의 논리는 운전 환경에 대한 현재 이용 가능한 정보에만 반응하는 잘 정의된 규칙으로 구성되어 있나요? 

Or is it also dependent on trajectory predictions of other agents?
아니면 다른 요원의 궤적 예측에도 의존하나요? 

Let's get started. Making driving decisions falls under the bigger umbrella of planning. 
시작하자.  운전 결정을 내리는 것은 계획의 더 큰 우산 아래에 있다. 

When we make driving decisions, we usually have three kinds of decisions to make. 
우리가 운전 결정을 내릴 때, 우리는 보통 세 가지 종류의 결정을 내려야 한다. 

The first type is a long-term planning decision. 
첫 번째 유형은 장기적인 계획 결정이다. 

A question such as, how do I navigate from New York to Los Angeles or from my home to work? 
뉴욕에서 로스앤젤레스로 또는 집에서 직장으로 어떻게 이동하나요? 이 질문에 답함으로써, 우리는 전체 운전 작업에 대한 높은 수준의 계획인 임무 계획을 가지고 있다. 

By answering this question, we have a mission plan, a high-level plan for the entire driving task. 
Mapping applications that you use today are able to give you these driving instructions: which roads to take, which lanes to be in, and so on. 
But driving needs much more than that. 
The second type is a short-term driving decision with questions like, is it safe to change lanes now? Or when should I execute a left turn at an intersection? Driving also needs some immediate decisions or reactions. 
These decisions involve control and trajectory planning and answer questions like, how do I follow my lane on this curved road? 
What steering input should I apply? 
Should I accelerate or brake? If so, by how much. 
Let's discuss a very simple example of a driving task and try to think about 
what kind of decisions are involved. 

Note that throughout this specialization, we will assume right-handed driving for all scenarios. 
Suppose you are approaching an intersection on your way home. 
The long-term planning stage requires you to turn left at this intersection. 




오늘 사용하는 매핑 애플리케이션은 다음과 같은 운전 지침을 제공할 수 있습니다: 어떤 도로를 택할지, 어떤 차선에 들어갈지 등. 
하지만 운전은 그것보다 훨씬 더 필요하다. 
두 번째 유형은 다음과 같은 질문이 있는 단기 운전 결정입니다. 
지금 차선을 바꾸는 것이 안전한가요? 아니면 교차로에서 언제 좌회전해야 하나요? 운전은 또한 즉각적인 결정이나 반응이 필요하다. 
이러한 결정에는 통제 및 궤적 계획이 포함되며, 이 구부러진 도로에서 내 차선을 어떻게 따라가나요? 어떤 스티어링 입력을 적용해야 하나요? 가속해야 하나요 아니면 브레이크를 밟아야 하나요? 만약 그렇다면, 얼마나. 운전 작업의 매우 간단한 예를 논의하고 어떤 종류의 결정이 관련되어 있는지 생각해 봅시다. 
이 전문 분야 전반에 걸쳐, 우리는 모든 시나리오에 대해 오른손잡이 운전을 가정할 것입니다. 
집에 가는 길에 교차로에 접근하고 있다고 가정해 봅시다. 장기 계획 단계는 이 교차로에서 좌회전해야 합니다.



Now, let's look at the intermediate and short-term decisions that need to be made. First, let's assume that the intersection is controlled. That is, it has traffic lights. Since you are turning left, you have to identify if you need to make a lane change into a left turning lane. Then, as you're approaching this intersection, you choose to slow down, and to do so smoothly so that the passengers don't experience discomfort. Nobody likes a jerky driver after all. You then come to a stop just before the stop line, before a pedestrian crossing. These decisions on lane changes and stopping locations are all short-term planning decisions. But wait! You also need to think and respond to situations that arise along the way. We still need object and event detection and response. What if a vehicle pulls into the turn lane in front of you? You would want to stop earlier to make room for the other vehicle. What if the stop lines weren't marked? You would have to approximately judge where the implied stop line is and stop before the pedestrian crossing. What if there were other vehicles behind you or even stalled in the intersection? How does the decision to execute a left turn change based on the many possible scenarios that can rapidly arise in normal driving? All of these decisions fall into the immediate decision category and requires safe reactions from the planning system. The end result is an exploding list of possible decisions to evaluate on different timescales, even for a simple left turn scenario. This amounts to talking about different cases for the same intersection crossing or scenarios. In each scenario, we need a consistent set of choices to be evaluated in real time and updated as new information about the scene becomes available. Furthermore, because decisions to change lanes affect where to drive and which cars to regulate our position relative to, even a seemingly simple driving scenario requires three or four levels of decisions, and must then still be executed with careful vehicle control. This example is really only scratching the surface of the constant stream of decisions needed for motion planning. The bottom line is, driving is complicated. 

이제, 내려야 할 중기 및 단기 결정을 살펴보자. 먼저, 교차로가 통제된다고 가정해 봅시다. 즉, 신호등이 있다. 좌회전하기 때문에, 좌회전 차선으로 차선을 변경해야 하는지 식별해야 합니다. 그런 다음, 이 교차로에 접근하면서, 속도를 늦추고 승객들이 불편함을 느끼지 않도록 부드럽게 하기로 선택합니다. 결국 아무도 육포 운전자를 좋아하지 않는다. 그런 다음 정지선 바로 앞에, 보행자가 건너기 전에 멈추세요. 차선 변경과 정지 위치에 대한 이러한 결정은 모두 단기 계획 결정이다. 하지만 기다려! 당신은 또한 그 과정에서 발생하는 상황을 생각하고 대응해야 합니다. 우리는 여전히 객체와 이벤트 감지 및 대응이 필요하다. 차량이 당신 앞에 있는 회전 차선으로 당기면 어떨까요? 당신은 다른 차량을 위한 공간을 만들기 위해 더 일찍 멈추고 싶을 것입니다. 정지선이 표시되지 않으면 어떻게 하나요? 묵시적 정지선이 어디에 있는지 대략 판단하고 보행자 횡단 전에 멈춰야 합니다. 당신 뒤에 다른 차량이 있거나 교차로에서 멈춘다면 어떨까요? 정상 운전에서 빠르게 발생할 수 있는 많은 가능한 시나리오에 따라 좌회전 실행 결정은 어떻게 바뀌나요? 이러한 모든 결정은 즉각적인 결정 범주에 속하며 계획 시스템의 안전한 반응을 필요로 한다. 최종 결과는 간단한 좌회전 시나리오에서도 다른 시간 척도에서 평가할 수 있는 가능한 결정의 폭발적인 목록이다. 이것은 같은 교차로 교차 또는 시나리오에 대한 다른 사례에 대해 이야기하는 것과 같다. 각 시나리오에서, 우리는 실시간으로 평가하고 장면에 대한 새로운 정보를 사용할 수 있게 되면 일관된 선택 세트가 필요합니다. 게다가, 차선을 변경하기로 한 결정은 운전할 곳과 어떤 자동차가 상대적으로 우리의 위치를 규제할지에 영향을 미치기 때문에, 겉보기에 간단한 운전 시나리오조차도 3~4단계의 결정이 필요하며, 여전히 신중한 차량 제어로 실행되어야 한다. 이 예는 실제로 모션 계획에 필요한 일정한 결정 흐름의 표면만 긁고 있다. 결론은 운전이 복잡하다는 것이다.

Let's go ahead and discuss a possible structure to represent these decisions in software. One method to address the challenge of multilevel decision-making is reactive planning. In reactive planning, we define sets of rules that take into account the current state of the ego vehicle and other objects in the environment and produce immediate actions. So, these are rules that only consider the current state and not future predictions. Some examples of such rules would be, if there is a pedestrian on the road, stop. Or if the speed limit changes, adjust your speed to match it. In both of these rules, we just observe what is happening right now and make our decision based on immediately available information. But there are other kinds of planning as well. In predictive planning, we make predictions on how other agents in the environment, like vehicles and pedestrians, will move over time. We use this current state and prediction information to define all of our decisions. Some examples of rules in predictive planning would be, that car has stopped for the last 10 seconds. It's probably going to stay stopped for the next few seconds. So, perhaps there is a way that I can move past it safely. Or a pedestrian is jaywalking. They will enter our lane by the time I get close to them. Let me slow down and give them a chance to cross the road ahead of me. As you can see, this is a more natural way to think, and relates closely to how humans operate vehicles. We predict where other objects on the road will be in the future before we make our decisions. This type of planning, however, relies on accurate predictions of the actions of the other actors in the environment, which adds a significant layer of complexity to the perception tasks. Nonetheless, predictive planning is the predominant method for self-driving cars, as it greatly expands the scenarios a vehicle can handle safely. We will discuss all aspects of planning in a further detail in course four on planning for self-driving cars, where we will show you the methods to solve long-term, short-term, and immediate-term planning problems. All right. Let's summarize this video. We discussed the planning problem and the different types of planning based on the window of time over which we have to act. These types are long-term, short-term, and immediate planning. Then we discussed a simple intersection scenario, where we had to make a left turn. We concluded that driving is a really hard problem since we have so many variables and possibilities that result. Then we discussed two different planning approaches: reactive planning and predictive planning. This is just the tip of the iceberg. There's clearly so much more we need to think about before making a decision during the driving task. Once again, we will go through all of these ideas in much greater detail in course four. That brings us to the end of the first week of course one in our self-driving car specialization. Let's quickly recap what we learned this week. In this module, we explored the basic autonomous driving terminology that's useful for later weeks of the specialization. We then discussed the levels of automation, and came up with a taxonomy to characterize self-driving capabilities. Then we define the driving task and the major components of driving: perception, planning, and execution. We then listed the elements and agents in the environment we need to identify and track for perception. We also discussed why perception is so hard. Then we discussed planning with its different horizons, and looked at some decision-making approaches. In the next module, we will define the main components of self-driving cars, including both the hardware and software elements that make up a complete system. See you then.

소프트웨어에서 이러한 결정을 표현할 수 있는 가능한 구조에 대해 논의해 봅시다. 다단계 의사 결정의 문제를 해결하는 한 가지 방법은 반응형 계획이다. 반응형 계획에서, 우리는 자아 차량과 환경의 다른 물체의 현재 상태를 고려하고 즉각적인 조치를 취하는 일련의 규칙을 정의합니다. 그래서, 이것들은 미래의 예측이 아닌 현재 상태만을 고려하는 규칙이다. 그러한 규칙의 몇 가지 예는 도로에 보행자가 있다면 멈추는 것이다. 또는 속도 제한이 변경되면, 속도에 맞게 조정하세요. 이 두 규칙 모두에서, 우리는 지금 무슨 일이 일어나고 있는지 관찰하고 즉시 이용 가능한 정보를 바탕으로 결정을 내립니다. 하지만 다른 종류의 계획도 있다. 예측 계획에서, 우리는 차량과 보행자와 같은 환경의 다른 요원들이 시간이 지남에 따라 어떻게 움직일지 예측한다. 우리는 이 현재 상태와 예측 정보를 사용하여 모든 결정을 정의합니다. 예측 계획의 규칙의 몇 가지 예는 그 차가 지난 10초 동안 멈췄다는 것이다. 아마 앞으로 몇 초 동안 멈출 거야. 그래서, 아마도 내가 그것을 안전하게 지나갈 수 있는 방법이 있을 것이다. 아니면 보행자가 무단횡단을 하고 있다. 내가 그들과 가까워질 때까지 그들은 우리 차선에 들어갈 것이다. 내가 속도를 늦추고 그들에게 내 앞에 있는 길을 건널 기회를 줄게. 보시다시피, 이것은 생각하는 더 자연스러운 방법이며, 인간이 차량을 어떻게 운영하는지 밀접한 관련이 있습니다. 우리는 결정을 내리기 전에 미래에 도로의 다른 물건들이 어디에 있을지 예측한다. 그러나 이러한 유형의 계획은 환경에서 다른 행위자의 행동에 대한 정확한 예측에 의존하며, 이는 인식 작업에 상당한 복잡성을 더한다. 그럼에도 불구하고, 예측 계획은 차량이 안전하게 처리할 수 있는 시나리오를 크게 확장하기 때문에 자율주행 자동차의 주된 방법이다. 우리는 자율주행 자동차 계획에 대한 코스 4에서 계획의 모든 측면을 더 자세히 논의할 것이며, 장기, 단기 및 즉각적인 계획 문제를 해결하는 방법을 보여줄 것입니다. 알았어. 이 비디오를 요약해 봅시다. 우리는 우리가 행동해야 하는 시간의 창을 기반으로 계획 문제와 다양한 유형의 계획에 대해 논의했다. 이러한 유형은 장기, 단기 및 즉각적인 계획입니다. 그런 다음 우리는 좌회전해야 하는 간단한 교차로 시나리오에 대해 논의했다. 우리는 너무 많은 변수와 가능성을 가지고 있기 때문에 운전이 정말 어려운 문제라고 결론지었다. 그런 다음 우리는 두 가지 다른 계획 접근 방식에 대해 논의했습니다: 반응형 계획과 예측 계획. 이건 빙산의 일각일 뿐이야. 운전 중에 결정을 내리기 전에 생각해야 할 것이 훨씬 더 많다. 다시 한번, 우리는 코스 4에서 이 모든 아이디어를 훨씬 더 자세히 살펴볼 것이다. 그것은 물론 우리의 자율주행 자동차 전문 분야의 첫 주 말까지 우리를 데려온다. 우리가 이번 주에 배운 것을 빠르게 요약해 봅시다. 이 모듈에서, 우리는 몇 주간의 전문 분야에 유용한 기본적인 자율주행 용어를 탐구했다. 그런 다음 우리는 자동화 수준에 대해 논의했고, 자율주행 능력을 특성화하기 위한 분류법을 생각해냈다. 그런 다음 운전 작업과 운전의 주요 구성 요소를 정의합니다: 인식, 계획 및 실행. 그런 다음 인식을 식별하고 추적해야 하는 환경의 요소와 에이전트를 나열했습니다. 우리는 또한 인식이 왜 그렇게 어려운지에 대해 논의했다. 그런 다음 우리는 다른 지평선으로 계획에 대해 논의했고, 몇 가지 의사 결정 접근 방식을 살펴보았다. 다음 모듈에서는 완전한 시스템을 구성하는 하드웨어 및 소프트웨어 요소를 포함하여 자율주행 자동차의 주요 구성 요소를 정의할 것입니다. 그때 보자.