Congratulations for making it this far in the course
코스에서 여기까지 온 걸 축하해
You're almost done
넌 거의 끝났어
Now it's time to take everything you learned and put it together for the final project
이제 당신이 배운 모든 것을 가지고 최종 프로젝트를 위해 조립할 때입니다
This video will provide you with the requirements needed to complete the final course assessment
이 비디오는 최종 과정 평가를 완료하는 데 필요한 요구 사항을 제공합니다
We will also discuss the grading scheme, and how to submit the final assessment through the provided YAML file
우리는 또한 채점 체계와 제공된 YAML 파일을 통해 최종 평가를 제출하는 방법에 대해 논의할 것입니다
Let's begin by listing the objectives of this assessment
먼저 이 평가의 목표를 나열해 봅시다
The final project requires using what you learned throughout the course to implement an environment perception stack for self-driving cars
최종 프로젝트는 과정 전반에 걸쳐 배운 것을 사용하여 자율주행 자동차를 위한 환경 인식 스택을 구현해야 합니다
Specifically, you will be using the output from semantic segmentation neural networks to: implement drivable space estimation in 3D, implement lane estimation, and filter out unreliable estimates in the output of 2D object detectors
특히, 의미 세분화 신경망의 출력을 사용하여 3D로 운전 가능한 공간 추정을 구현하고, 차선 추정을 구현하고, 2D 물체 검출기의 출력에서 신뢰할 수 없는 추정치를 필터링할 것입니다
Finally, you will use the filtered 2D object detection output to determine how far obstacles are from the self-driving car
마지막으로, 필터링된 2D 물체 감지 출력을 사용하여 자율주행 자동차에서 장애물이 얼마나 멀리 떨어져 있는지 결정할 것입니다
By finishing this project, you will be ready to develop baseline perception stacks that would allow a self-driving car to know where it can drive in roads scenes, what obstacles are within view which may affect its decision-making, and how far away these obstacles are
이 프로젝트를 마치면 자율주행 자동차가 도로 장면에서 운전할 수 있는 곳, 의사 결정에 영향을 미칠 수 있는 어떤 장애물이 있는지, 그리고 이러한 장애물이 얼마나 멀리 떨어져 있는지 알 수 있는 기본 인식 스택을 개발할 준비가 될 것입니다
You have already learned how to perform most of the required tasks for this assessment in the previous lessons
이전 수업에서 이 평가에 필요한 대부분의 작업을 수행하는 방법을 이미 배웠습니다
Let us list the reference lessons that can be useful while tackling this assignment
이 과제를 다루는 동안 유용할 수 있는 참조 수업을 나열해 봅시다
For drivable space estimation, you can refer to Module 1, Lesson 3 to estimate the x, y, z coordinates of pixels from depth, and Module 5, Lesson 3 to estimate the ground plane from semantic segmentation output
운전 가능한 공간 추정의 경우, 모듈 1, 3과를 참조하여 깊이에서 픽셀의 x, y, z 좌표를 추정하고, 모듈 5, 수업 3을 참조하여 의미론적 세분화 출력에서 접지면을 추정할 수 있습니다
For Lane estimation, you can refer to Module 5, Lesson 3 for estimating lane lines
차선 추정의 경우, 차선 선 추정에 대해서는 모듈 5, 수업 3을 참조할 수 있습니다
For estimating the minimum distance to impact, Module 4, Lesson 4 will be useful for reference
충격까지의 최소 거리를 추정하기 위해, 모듈 4, 수업 4는 참조에 유용할 것이다
Now let's describe in detail why the required tasks are important for self-driving cars
이제 자율주행 자동차에 필요한 작업이 왜 중요한지 자세히 설명합시다
Drivable space estimation in 3D is important for self-driving cars to safely traverse the environment
3D의 운전 가능한 공간 추정은 자율주행 자동차가 환경을 안전하게 통과하는 데 중요하다
Using the given sensor input as well as semantic segmentation data from a neural network, you are required to estimate the equation of the ground plane in 3D
주어진 센서 입력과 신경망의 의미 세분화 데이터를 사용하여 지상 평면 방정식을 3D로 추정해야 합니다
Then determine pixels belonging to the ground plane based on a distance threshold
그런 다음 거리 임계값에 따라 접지면에 속하는 픽셀을 결정하십시오
Yellow here specifies the pixels your algorithm should label as a drivable space
여기서 노란색은 알고리즘이 운전 가능한 공간으로 표시해야 하는 픽셀을 지정합니다
We will provide you with code to visualize the ground plane you estimated in 3D as an occupancy grid
우리는 당신이 점유 그리드로 3D로 추정한 지상 비행기를 시각화하는 코드를 제공할 것입니다
A topic that will be covered in the next course in this specialization
이 전문 분야의 다음 과정에서 다룰 주제
Note that drivable space does not mean road
운전할 수 있는 공간은 도로를 의미하지 않는다는 점에 유의하세요
As you can see, a portion of an area behind the sidewalk was labeled as drivable space two
보시다시피, 보도 뒤의 한 지역의 일부는 운전 가능한 공간 2로 표시되었습니다
Drivable space based on ground plane estimation provides the 3D space where the car is physically capable of driving
지상 비행기 추정에 기반한 운전 가능한 공간은 자동차가 물리적으로 운전할 수 있는 3D 공간을 제공한다
To specify where the car is legally allowed to drive, you are required to perform lane boundary estimation
자동차가 합법적으로 운전할 수 있는 곳을 지정하려면 차선 경계 추정을 수행해야 합니다
To perform this task, you are provided with the output of semantic segmentation
이 작업을 수행하려면 의미론적 세분화의 출력이 제공됩니다
You are required to use this output to estimate the left and right lane boundaries for your current lane
현재 차선 경계와 오른쪽 차선 경계를 추정하려면 이 출력을 사용해야 합니다
The final task for this assessment requires you to estimate the distance to impact to objects in the scene provided by an object detection neural network
이 평가의 최종 작업은 물체 감지 신경망이 제공하는 장면의 물체에 대한 충격까지의 거리를 추정해야 합니다
The problem is that, the neural network model has a high recall but a low precision and provide some errors in its output
문제는 신경망 모델이 리콜이 높지만 정밀도가 낮고 출력에 몇 가지 오류를 제공한다는 것이다
You are required to first use the output of the semantic segmentation network to filter out erroneous results from the object detection network
먼저 시맨틱 세분화 네트워크의 출력을 사용하여 객체 감지 네트워크에서 잘못된 결과를 필터링해야 합니다
Then you are required to compute the minimum distance to impact with every obstacle in the scene
그런 다음 장면의 모든 장애물에 영향을 미칠 최소 거리를 계산해야 합니다
Let's check what the final output of the whole system would look like
전체 시스템의 최종 출력이 어떻게 생겼는지 확인해 봅시다
Using the estimated ground plane, the self-driving car will be able to determine where it can physically drive in the environment
예상 지상 비행기를 사용하여, 자율주행 자동차는 환경에서 물리적으로 운전할 수 있는 곳을 결정할 수 있을 것이다
Using the estimated lane boundaries, the self-driving car will be able to abide by the rules of the road
예상 차선 경계를 사용하여 자율주행 자동차는 도로의 규칙을 준수할 수 있을 것이다
Finally, using the filtered object detection output along with the distance to impact estimation, the self-driving car will be able to localize obstacles on the road to determine if any obstacles or blocking its path
마지막으로, 필터링된 물체 감지 출력과 충격 추정까지의 거리를 사용하여 자율주행 자동차는 도로의 장애물을 현지화하여 장애물이 있는지 또는 경로를 차단할 수 있습니다
For the final project, keep in mind that the provided algorithmic guidelines are not rigid, and there exist many alternative approaches that you could use at each step of the assessment
최종 프로젝트의 경우, 제공된 알고리즘 지침은 엄격하지 않으며, 평가의 각 단계에서 사용할 수 있는 많은 대체 접근 방식이 존재한다는 것을 명심하십시오
You are encouraged to diverge from the provided algorithm outlines wherever you believe you could do better in terms of results or efficiency
결과나 효율성 측면에서 더 잘할 수 있다고 생각하는 곳 어디에서나 제공된 알고리즘 개요에서 벗어나도록 권장됩니다
If you have any questions that I didn't answer in this video, there are further instructions in the Jupiter Notebook itself and don't be afraid to ask in the discussion forums as well
이 비디오에서 대답하지 않은 질문이 있다면, 목성 노트북 자체에 추가 지침이 있으며 토론 포럼에서도 물어보는 것을 두려워하지 마세요
I hope you have fun with this final project
네가 이 마지막 프로젝트를 즐기길 바라
I'll see you once again, once it's complete to close out the course
과정을 마치기 위해 완료되면 다시 한 번 뵙겠습니다
Good luck, and have fun
행운을 빌어, 그리고 재밌게 놀아


