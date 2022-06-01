Welcome to the final lesson for this week
이번 주 마지막 수업에 오신 것을 환영합니다
In the previous lesson, we learned how to perform semantic segmentation using convolutional neural networks
이전 수업에서, 우리는 컨볼루션 신경망을 사용하여 의미론적 세분화를 수행하는 방법을 배웠다
In this video, we will learn how to use the output of these networks for scene understanding of road scenes
이 비디오에서, 우리는 도로 장면에 대한 장면 이해를 위해 이러한 네트워크의 출력을 사용하는 방법을 배울 것입니다
Specifically, you will learn how to use the output of semantic segmentation models to estimate the drivable space and lane boundaries
특히, 당신은 의미론적 세분화 모델의 출력을 사용하여 운전 가능한 공간과 차선 경계를 추정하는 방법을 배우게 될 것입니다
Let's quickly review what we expect as an output from a semantic segmentation model
의미론적 세분화 모델의 출력으로 기대하는 것을 빠르게 검토해 봅시다
A semantic segmentation model takes an image as an input, and provides us output, a category classification for every pixel
시맨틱 세분화 모델은 이미지를 입력으로 취하고, 모든 픽셀에 대한 카테고리 분류인 출력을 제공합니다
Now let's use this output to perform some useful tasks for self-driving cars
이제 이 출력을 사용하여 자율주행 자동차에 몇 가지 유용한 작업을 수행합시다
The first task we will be discussing is the estimation of a drivable surface from semantic segmentation output in 3D
우리가 논의할 첫 번째 작업은 3D의 의미론적 세분화 출력에서 운전 가능한 표면을 추정하는 것이다
Drivable space is defined as the region in front of the vehicle where it is safe to drive
운전 가능한 공간은 운전하기에 안전한 차량 앞의 지역으로 정의된다
In the context of semantic segmentation, the drivable surface includes all pixels from the road, crosswalks, lane markings, parking spots, and even sometimes rail tracks
의미론적 세분화의 맥락에서, 운전 가능한 표면은 도로, 횡단보도, 차선 표시, 주차 공간, 심지어 때로는 철도 선로의 모든 픽셀을 포함한다
Estimating a drivable surface is very important as it is one of the main steps for constructing occupancy grids from 3D depth sensors
운전 가능한 표면을 추정하는 것은 3D 깊이 센서에서 점유 그리드를 구성하는 주요 단계 중 하나이기 때문에 매우 중요합니다
You will learn more about occupancy grids in course 4, where they will be used to represent where obstacles are located in the environment during collision avoidance
충돌 방지 동안 환경에 장애물이 어디에 있는지 나타내는 데 사용되는 코스 4에서 점유 그리드에 대해 자세히 배우게 될 것입니다
But for now, let's describe how to perform drivable surface estimation from the semantic segmentation output
하지만 지금은 의미론적 세분화 출력에서 운전 가능한 표면 추정을 수행하는 방법을 설명합시다
First, we use a ConvNet to generate the semantic segmentation output of an image frame, we then generate 3D coordinates of some of the pixels in this frame, either from stereo data or by projecting a lighter point cloud to the image plane
첫째, ConvNet을 사용하여 이미지 프레임의 시맨틱 세분화 출력을 생성한 다음 스테레오 데이터에서 또는 더 가벼운 포인트 클라우드를 이미지 평면에 투영하여 이 프레임의 일부 픽셀의 3D 좌표를 생성합니다
With a known extrinsic calibration between sensors, we can project lidar points into the image plane and match them to the corresponding pixels
센서 간의 알려진 외부 교정으로, 우리는 라이더 포인트를 이미지 평면에 투사하고 해당 픽셀과 일치시킬 수 있습니다
We then proceed to choose 3D points that belong to the drivable surface category
그런 다음 운전 가능한 표면 범주에 속하는 3D 포인트를 선택합니다
As we mentioned earlier, this category should at least include the road, lane markings, and pedestrian crossings
앞서 언급했듯이, 이 범주에는 적어도 도로, 차선 표시 및 보행자 횡단이 포함되어야 합니다
In certain scenarios, other classes such as railroad tracks for example might also be included, depending on the driving context
특정 시나리오에서는 운전 상황에 따라 철도 선로와 같은 다른 클래스도 포함될 수 있습니다
All other classes are excluded even if their height is similar to the drivable surface
다른 모든 클래스는 높이가 운전 가능한 표면과 비슷하더라도 제외됩니다
Finally, we use this subset of 3D points to estimate a drivable surface model
마지막으로, 우리는 운전 가능한 표면 모델을 추정하기 위해 이 3D 점의 하위 집합을 사용합니다
The complexity of this model can range from a simple plane to more complex spline surface models
이 모델의 복잡성은 간단한 평면에서 더 복잡한 스플라인 표면 모델에 이르기까지 다양할 수 있다
Let's describe how to robustly fits a planar drivable surface model given segmented image data and lidar points
분할된 이미지 데이터와 라이더 포인트가 주어진 평면 운전 가능한 표면 모델에 강력하게 맞는 방법을 설명합시다
We first define the model of a plane as ax plus by plus z equals d, where x, y, z is any point on the plane, the coefficients a, b, and 1 define the plane normal vector, and d is a constant offset
우리는 먼저 평면의 모델을 ax plus by plus z로 정의하며, 여기서 x, y, z는 평면의 모든 점이고, 계수 a, b, 1은 평면 정규 벡터를 정의하고, d는 상수 오프셋이다
We can form a set of linear equations to estimate the parameters of this plane model using as measurements, each of the points identified as belonging to the drivable surface
우리는 운전 가능한 표면에 속하는 것으로 확인된 각 점인 측정으로 사용하여 이 평면 모델의 매개 변수를 추정하기 위해 선형 방정식 세트를 형성할 수 있습니다
The parameters of the model are now summarized by the vector p, and the measurements are separated into the matrices A and B
모델의 매개 변수는 이제 벡터 p로 요약되며, 측정값은 행렬 A와 B로 분리됩니다
As formulated in course 2, we can find a solution for this system of linear equations using the method of least squares
코스 2에서 공식화된 바와 같이, 우리는 최소 제곱의 방법을 사용하여 이 선형 방정식 시스템에 대한 해결책을 찾을 수 있다
As a result, our plane parameter vector p is equal to the pseudoinverse of A times B
결과적으로, 우리의 평면 매개 변수 벡터 p는 A배 B의 의사 반대와 같다
This model has three free parameters to be estimated, and as such, we need at least three non-colinear 3D points to fit the plane
이 모델에는 추정할 세 가지 무료 매개 변수가 있으므로 평면에 맞게 적어도 세 개의 비콜리니어 3D 포인트가 필요합니다
In practice, we will have many more points than are necessary, so we can apply the method of least squares once again to identify parameters that minimize the mean square distance of all points from the plane
실제로, 우리는 필요한 것보다 더 많은 점을 가질 것이므로, 평면에서 모든 점의 평균 제곱 거리를 최소화하는 매개 변수를 식별하기 위해 최소 제곱 방법을 다시 한 번 적용할 수 있습니다
Of course, some points will be labeled incorrectly and may not truly belong to the drivable surface
물론, 일부 포인트는 잘못 표시되며 진정으로 운전 가능한 표면에 속하지 않을 수 있습니다
So how can we avoid incorrect semantic labels negatively affecting the quality of a drivable surface plane estimation
그렇다면 운전 가능한 표면 평면 추정의 품질에 부정적인 영향을 미치는 잘못된 의미 라벨을 어떻게 피할 수 있을까요
Fortunately for us, we learned a very powerful and robust estimation method in week 2 of this course
다행스럽게도, 우리는 이 과정의 2주차에 매우 강력하고 강력한 추정 방법을 배웠다
Specifically, we can use the RANSAC algorithm to robustly fit a drivable surface plane model even with some errors in our semantic segmentation output
특히, 우리는 RANSAC 알고리즘을 사용하여 시맨틱 세분화 출력의 일부 오류에도 불구하고 운전 가능한 표면 평면 모델에 강력하게 맞출 수 있습니다
Let's go through the RANSAC algorithm for the drivable surface estimation as a refresher
재교육으로 운전 가능한 표면 추정을 위한 RANSAC 알고리즘을 살펴봅시다
First, we randomly select the minimum number of data points required to fit our model
먼저, 우리는 모델에 맞는 데 필요한 최소 데이터 포인트 수를 무작위로 선택합니다
In this case, we randomly choose three points in 3D
이 경우, 우리는 무작위로 3D로 세 점을 선택합니다
Second, we use these three points to compute the model parameters a, b, and d, and use the method of least squares to solve for our plane parameters
둘째, 우리는 이 세 점을 사용하여 모델 매개 변수 a, b 및 d를 계산하고, 평면 매개 변수를 해결하기 위해 최소 제곱 방법을 사용합니다
We then proceed to determine the number of 3D points that satisfy these model parameters
그런 다음 이러한 모델 매개 변수를 충족하는 3D 포인트의 수를 결정합니다
Usually for drivable surface estimation, most of the outliers are a result of the erroneous segmentation outputs located at the boundaries
일반적으로 운전 가능한 표면 추정의 경우, 대부분의 이상값은 경계에 위치한 잘못된 세분화 출력의 결과이다
If the number of outliers is low, we terminate and return the computed plane parameters
이상값 수가 적으면, 계산된 평면 매개 변수를 종료하고 반환합니다
Otherwise, we sample three new points at random and repeat the process
그렇지 않으면, 우리는 무작위로 세 개의 새로운 점을 샘플링하고 과정을 반복합니다
Then once the algorithm meets its termination condition, we calculate the final planar surface model of the road from all of the inliers in the largest inlier set
그런 다음 알고리즘이 종료 조건을 충족하면, 가장 큰 inlier 세트의 모든 inliers에서 도로의 최종 평면 표면 모델을 계산합니다
The use of a planar surface model works well if the road is actually flat, a valid assumption in many driving scenarios
평면 표면 모델의 사용은 도로가 실제로 평평하다면 잘 작동하며, 많은 운전 시나리오에서 유효한 가정이다
For more complex scenarios, such as entering a steeply climbing highway entrance from a flat roadway for example, more complex models are needed
예를 들어 평평한 도로에서 가파르게 등반하는 고속도로 입구에 들어가는 것과 같은 더 복잡한 시나리오의 경우, 더 복잡한 모델이 필요하다
Although we estimate the drivable surface, we still have not determined where the car is allowed to drive on this surface
우리는 운전 가능한 표면을 추정하지만, 우리는 여전히 차가 이 표면에서 운전할 수 있는 곳을 결정하지 못했다
Usually, a vehicle should stay within its lane, determined by lane markings or the road boundaries
보통, 차량은 차선 표시나 도로 경계에 의해 결정된 차선 내에 있어야 한다
Lane estimation is the task of estimating where a self-driving car can drive given a drivable surface
차선 추정은 자율주행 자동차가 운전 가능한 표면을 감안할 때 운전할 수 있는 곳을 추정하는 작업이다
Many methods exist in the literature to accomplish this task
이 임무를 완수하기 위해 문학에는 많은 방법이 존재한다
For example, some methods directly estimate lane markings from ConvNets to determine where the car can drive
예를 들어, 일부 방법은 ConvNets의 차선 표시를 직접 추정하여 자동차가 운전할 수 있는 곳을 결정합니다
However, for higher-level decision-making, a self-driving car should also be aware of what is at the boundary of the lane
그러나, 더 높은 수준의 의사 결정을 위해, 자율주행 자동차는 차선의 경계에 무엇이 있는지 알아야 한다
Classes at the boundary of the lame can range from a curb, a road, where opposite traffic resides or dynamic in parked vehicles
절름발이의 경계에 있는 수업은 연석, 반대 교통이 상주하거나 주차된 차량에서 역동적인 도로에서 다양할 수 있다
The self-driving car has to base its maneuvers on what objects occur at the boundary of the lane, especially during emergency pull overs
자율주행 자동차는 특히 비상 풀오버 중에 차선의 경계에서 어떤 물체가 발생하는지 기동을 기반으로 해야 한다
We will refer to the task of estimating the lane and what occurs at its boundaries as semantic lane estimation
우리는 차선을 추정하는 작업과 그 경계에서 일어나는 일을 의미론적 차선 추정으로 언급할 것이다
Notice that if we estimate the lane using the output of semantic segmentation, we get boundary classification for free
의미 세분화의 출력을 사용하여 차선을 추정하면 경계 분류를 무료로 받을 수 있습니다
Let's go through a simple approach to this problem to clarify the lane estimation task
차선 추정 작업을 명확히 하기 위해 이 문제에 대한 간단한 접근 방식을 살펴보겠습니다
Given the output of a semantic segmentation model, we first extract a binary mask of the pixels belonging to classes that occur as lane separators
시맨틱 세분화 모델의 출력을 감안할 때, 우리는 먼저 차선 구분자로 발생하는 클래스에 속하는 픽셀의 이진 마스크를 추출합니다
Such classes can include curbs, lane markings, or rails for example
이러한 클래스에는 예를 들어 커브, 레인 표시 또는 레일이 포함될 수 있습니다
Then we apply an edge detector to the binary mask
그런 다음 이진 마스크에 가장자리 탐지기를 적용합니다
As you remember from the first week of this course, edge detectors can be as simple as estimating gradients from convolutions
이 과정의 첫 주부터 기억하시듯이, 가장자리 탐지기는 컨볼루션에서 그라디언트를 추정하는 것만큼 간단할 수 있습니다
Here, we use a famous edge detector, the canny edge detector
여기서, 우리는 유명한 가장자리 탐지기인 도니 에지 탐지기를 사용합니다
The output are pixels classified as edges that will be used to estimate the lane boundaries
출력은 차선 경계를 추정하는 데 사용될 가장자리로 분류된 픽셀이다
The final step is to determine which model is to be used to estimate the lanes
마지막 단계는 차선을 추정하는 데 사용할 모델을 결정하는 것이다
The choice of models defines what the next step will be
모델의 선택은 다음 단계가 무엇인지 정의한다
Here we choose a linear lane model, where each lane is assumed to be made up of a single line
여기서 우리는 각 차선이 단일 선으로 구성되어 있다고 가정하는 선형 차선 모델을 선택합니다
To detect lines in the output edge map, we need aligned detector
출력 가장자리 지도에서 선을 감지하려면 정렬된 탐지기가 필요합니다
The Hough transform line detection algorithm is widely used and capable of detecting multiple lines in an edge map
Hough 변환 라인 감지 알고리즘은 널리 사용되며 에지 맵에서 여러 라인을 감지할 수 있습니다
Given an edge map, the Hough transform can generate a set of lines that link pixels belonging to edges in the edge map
가장자리 맵이 주어지면, Hough 변환은 가장자리 지도의 가장자리에 속하는 픽셀을 연결하는 선 세트를 생성할 수 있다
The minimum length of the required lines can be set as a hyperparameter to force the algorithm to only detect lines that are long enough to be part of lane markings
필요한 선의 최소 길이는 알고리즘이 차선 표시의 일부가 될 만큼 충분히 긴 선만 감지하도록 강요하기 위해 하이퍼파라미터로 설정할 수 있다
Further refinement can be applied based on the scenario at hand
당면한 시나리오에 따라 더 많은 개선이 적용될 수 있다
For example, we know that our lane should not be a horizontal line if our camera is placed forward facing in the direction of motion
예를 들어, 우리는 카메라가 움직임 방향으로 앞으로 배치되면 차선이 수평선이 되어서는 안 된다는 것을 알고 있습니다
Furthermore, we can remove any line that does not belong to the drivable surface to get a final set of lane boundary primitives
게다가, 우리는 최종 차선 경계 프리미티브 세트를 얻기 위해 운전 가능한 표면에 속하지 않는 선을 제거할 수 있습니다
The last step would be to determine the classes that occur at both sides of the lane, which can easily be done by considering the classes on both sides of the estimated lane lines
마지막 단계는 차선의 양쪽에서 발생하는 클래스를 결정하는 것이며, 이는 예상 차선의 양쪽에 있는 클래스를 고려하여 쉽게 수행할 수 있다
We will not discuss edge detectors and Hough transforms in detail, as these topics deserve a separate discussion outside the scope of this course
우리는 이 과정의 범위를 벗어나 별도의 토론을 받을 자격이 있기 때문에 에지 탐지기와 Hough 변환에 대해 자세히 논의하지 않을 것입니다
However, powerful computer vision libraries such as Open CV, have open-source implementations, and tutorials on how to detect lines using the Hough transform, and how to detect edges using the Canny edge detector
그러나 Open CV와 같은 강력한 컴퓨터 비전 라이브러리에는 오픈 소스 구현과 Hough 변환을 사용하여 선을 감지하는 방법과 Canny edge 검출기를 사용하여 가장자리를 감지하는 방법에 대한 튜토리얼이 있습니다
If interested, take a look at how these algorithms are used in practice using the links provided in the supplementary material
관심이 있다면, 보충 자료에 제공된 링크를 사용하여 이러한 알고리즘이 실제로 어떻게 사용되는지 살펴보세요
In summary, semantic segmentation can be used to estimate the drivable space, to determine what occurs at the boundary of the drivable space, and to estimate lanes on the drivable surface
요약하면, 의미론적 세분화는 운전 가능한 공간을 추정하고, 운전 가능한 공간의 경계에서 일어나는 것을 결정하고, 운전 가능한 표면의 차선을 추정하는 데 사용될 수 있다
The applications discussed so far are very active areas of research, and what you've learned during this lesson provides a solid starting point and competitive baselines for the task of semantic lane detection and drivable surface estimation
지금까지 논의된 응용 프로그램은 매우 활발한 연구 분야이며, 이 수업에서 배운 것은 의미론적 차선 감지 및 운전 가능한 표면 추정 작업에 대한 견고한 출발점과 경쟁력 있는 기준선을 제공합니다
Furthermore, semantic lane detection and drivable surface estimation are the most prominent uses for semantic segmentation models in the context of self-driving cars
게다가, 시맨틱 레인 감지 및 운전 가능한 표면 추정은 자율주행 자동차의 맥락에서 시맨틱 세분화 모델의 가장 두드러진 용도이다
However, semantic segmentation has many more useful applications
그러나, 의미론적 세분화는 더 많은 유용한 응용 프로그램을 가지고 있다
Most importantly, aiding the self-driving car in performing both 2D object detection and localization
가장 중요한 것은 자율주행 자동차가 2D 물체 감지와 현지화를 모두 수행하는 것을 돕는 것이다
With information about which pixels to evaluate for objects or weather features are on static or moving objects, the robustness of the perception system can be significantly improved
물체나 날씨 기능에 대해 평가할 픽셀이 정적 또는 움직이는 물체에 있는지에 대한 정보를 통해 인식 시스템의 견고성을 크게 향상시킬 수 있습니다
It can act as a sanity check or a filter to avoid including incorrect information in other perception tasks
그것은 다른 인식 작업에 잘못된 정보를 포함하지 않도록 정신 검사나 필터 역할을 할 수 있다
Semantic segmentation is a powerful tool for self-driving cars and a core component of the high level perception stack
시맨틱 세분화는 자율주행 자동차를 위한 강력한 도구이자 높은 수준의 인식 스택의 핵심 구성 요소이다
You will have the chance to validate its usefulness next week when we discuss our final assignment
다음 주에 최종 과제를 논의할 때 유용성을 확인할 수 있습니다
See you then
그때 보자


