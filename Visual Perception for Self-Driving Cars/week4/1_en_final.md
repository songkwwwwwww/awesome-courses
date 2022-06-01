Hello, and welcome to week four of our Visual Perception for Autonomous Driving Course
안녕하세요, 자율주행 과정에 대한 시각적 인식 4주차에 오신 것을 환영합니다
This week, we'll dive into object detection, a core requirement for any self-driving car perception stack
이번 주에, 우리는 자율주행 자동차 인식 스택의 핵심 요구 사항인 물체 감지에 뛰어들 것입니다
Object detection is a top level module required to identify the locations of vehicles, pedestrians, signs, and lights, so our car knows where and how it can drive
물체 감지는 차량, 보행자, 표지판 및 조명의 위치를 식별하는 데 필요한 최상위 모듈이므로 자동차는 어디서 어떻게 운전할 수 있는지 알 수 있습니다
This week, we will be going in depth to define the 2D object detection problem, how to apply ConvNets to tackle it, and why the problem of 2D object detection is difficult
이번 주에, 우리는 2D 물체 감지 문제, ConvNets를 적용하여 해결하는 방법, 그리고 2D 물체 감지 문제가 왜 어려운지 자세히 정의할 것입니다
We will then explain how object detection is used as input for the 2D object tracking problem, and how to perform the tracking task in the context of self-driving cars
그런 다음 물체 감지가 2D 물체 추적 문제에 대한 입력으로 어떻게 사용되는지, 그리고 자율주행 자동차의 맥락에서 추적 작업을 수행하는 방법을 설명할 것입니다
This lesson will formulate the object detection problem in 2D
이 수업은 물체 감지 문제를 2D로 공식화할 것이다
You will also learn how to evaluate 2D object detectors using standard performance metrics established by researchers in the field
또한 현장에서 연구원들이 설정한 표준 성능 지표를 사용하여 2D 물체 검출기를 평가하는 방법을 배우게 될 것입니다
Let's get started
시작하자
The history of 2D object detection begins in 2001 when Paul Viola and Michael Jones invented a very efficient algorithm for face detection
2D 물체 감지의 역사는 2001년 폴 비올라와 마이클 존스가 얼굴 탐지를 위한 매우 효율적인 알고리즘을 발명했을 때 시작된다
This algorithm now called the Viola, Jones Object Detection Framework, was the first object detection framework to provide reliable, real-time 2D object detections from a simple webcam
현재 비올라라고 불리는 이 알고리즘인 존스 객체 탐지 프레임워크는 간단한 웹캠에서 신뢰할 수 있는 실시간 2D 물체 감지를 제공하는 최초의 물체 감지 프레임워크였다
The next big breakthrough in object detection happened four years later when Navneet Dalal and Bill Triggs formulated the histogram of oriented gradient feature descriptor
물체 감지의 다음 큰 돌파구는 4년 후 Navneet Dalal과 Bill Triggs가 지향 그라데이션 기능 설명자의 히스토그램을 공식화했을 때 일어났다
Their algorithm applied to the 2D pedestrian detection problem, outperformed all other proposed methods at the time
그들의 알고리즘은 2D 보행자 탐지 문제에 적용되었고, 당시 제안된 다른 모든 방법을 능가했다
The Dalal, Triggs algorithm remained on the top of the charts until 2012 when Alex Krizhevsky, Ilya Sutskever and Geoffrey Hinton from the Computer Science Department here at the University of Toronto, shook the computer vision world with their convolutional neural network dubbed AlexNet
달랄, 트릭스 알고리즘은 토론토 대학교 컴퓨터 과학부의 알렉스 크리제예프스키, Ilya Sutskever, Geoffrey Hinton이 AlexNet이라고 불리는 컨볼루션 신경망으로 컴퓨터 비전 세계를 흔들었을 때까지 차트 상단에 남아 있었다
AlexNet won the ImageNet Large Scale Visual Recognition Challenge in 2012 with a wide margin over the algorithm that took second place
AlexNet은 2012년에 2위를 차지한 알고리즘보다 넓은 차이로 ImageNet 대규모 시각적 인식 챌린지에서 우승했다
In 2012, it was the only deep learning-based entry in the challenge
2012년에, 그것은 도전에서 유일한 딥 러닝 기반 항목이었다
But since then, all winning entries in this competition are based on convolutional neural networks with the entry surpassing the human recognition rate of 95 percent recently
하지만 그 이후로, 이 대회에서 우승한 모든 출품작은 최근 95%의 인간 인식률을 능가하는 컨볼루션 신경망을 기반으로 한다
This performance extended from 2D object recognition to 2D object detection with current day detectors being almost exclusively based on convolutional neural networks
이 성능은 2D 물체 인식에서 2D 물체 감지로 확장되었으며, 현재 검출기는 거의 독점적으로 컨볼루션 신경망을 기반으로 한다
Before we go through how to use ConvNets for object detection and self-driving cars, let's formulate the general 2D object detection problem
물체 감지 및 자율주행 자동차에 ConvNets를 사용하는 방법을 살펴보기 전에, 일반적인 2D 물체 감지 문제를 공식화합시다
Given a 2D image's input, we are required to estimate the location defined by a bounding box and the class of all objects in the scene
2D 이미지의 입력이 주어지면, 경계 상자로 정의된 위치와 장면의 모든 객체의 클래스를 추정해야 합니다
Usually, we choose classes that are relevant to our application
보통, 우리는 지원서와 관련된 수업을 선택합니다
For self-driving cars, we usually are most interested in object classes that are dynamic, that is ones that move through the scene
자율주행 자동차의 경우, 우리는 보통 역동적인 객체 클래스, 즉 현장을 통과하는 것에 가장 관심이 있다
These include vehicles in their subclasses, pedestrians, and cyclists
여기에는 하위 클래스의 차량, 보행자 및 자전거 운전자가 포함됩니다
The problem of 2D object detection is not trivial
2D 물체 감지 문제는 사소하지 않다
The extent of objects we require to estimate are not always fully observed in the image space
우리가 추정해야 하는 물체의 범위가 이미지 공간에서 항상 완전히 관찰되는 것은 아니다
As an example, background objects are usually occluded by foreground objects
예를 들어, 배경 물체는 보통 전경 물체에 의해 가려진다
This requires any algorithm we use to be able to hallucinate the extent of objects to properly detect them
이것은 우리가 물체의 범위를 적절하게 감지하기 위해 환각할 수 있도록 사용하는 모든 알고리즘이 필요하다
Furthermore, objects that are near the edge of the image are usually truncated
게다가, 이미지의 가장자리 근처에 있는 물체는 보통 잘린다
This phenomenon creates huge variability in the bounding box sizes, where the size of the estimated bounding box depends on how truncated the object is
이 현상은 예상 경계 상자의 크기가 물체가 얼마나 잘렸는지에 따라 달라지는 경계 상자 크기에 큰 변동성을 만들어낸다
Another issue faced by 2D object detection algorithms is that of scale
2D 물체 감지 알고리즘이 직면한 또 다른 문제는 규모의 문제이다
Objects tend to appear very small as they go further away from our censor
물체는 검열에서 더 멀어질 때 매우 작게 보이는 경향이 있다
Our algorithm is expected to determine the class of these objects at variable scales
우리의 알고리즘은 변수 규모로 이러한 객체의 클래스를 결정할 것으로 예상된다
Finally, our algorithm should also be able to handle illumination changes
마지막으로, 우리의 알고리즘은 조명 변경도 처리할 수 있어야 한다
This is especially important in the context of self-driving cars, where images can be affected by whole image illumination variations from bright sun to night driving, and partial variations due to reflections, shadows, precipitation, and other nuisance effects
이것은 밝은 태양에서 야간 운전으로의 전체 이미지 조명 변화와 반사, 그림자, 강수량 및 기타 성가신 효과로 인한 부분적인 변화에 영향을 받을 수 있는 자율주행 자동차의 맥락에서 특히 중요합니다
Now that we've intuitively understood what object detection is, let us formalize the problem mathematically
이제 물체 감지가 무엇인지 직관적으로 이해했으니, 문제를 수학적으로 공식화합시다
Object detection can be defined as a function estimation problem
객체 감지는 함수 추정 문제로 정의될 수 있다
Given an input image x, we want to find the function f of x in Theta that produces an output vector that includes the coordinates of the top-left of the box, xmin and ymin, and the coordinates of the lower right corner of the box, xmax and ymax, and a class score Sclass1 to Sclassk
입력 이미지 x를 감안할 때, 우리는 세타에서 상자의 왼쪽 상단 좌표, xmin과 ymin, 상자의 오른쪽 하단 모서리 좌표, xmax와 ymax, 클래스 점수 Sclass1에서 Sclassk를 포함하는 출력 벡터를 생성하는 x의 함수 f를 찾고 싶습니다
Sclassi specifies how confident our algorithm is that the object belongs to the class i, and i ranges from one to k, where k is the number of classes of interest
Sclassi는 알고리즘이 객체가 클래스 i에 속한다는 것을 얼마나 확신하는지 지정하고, i는 1에서 k까지 다양하며, 여기서 k는 관심 클래스 수입니다
Can you think of any way to estimate this function
이 기능을 추정할 방법을 생각할 수 있나요
Convolutional neural networks, which we described last week are an excellent tool for estimating this kind of function
우리가 지난 주에 설명한 컨볼루션 신경망은 이런 종류의 기능을 추정하는 훌륭한 도구이다
For object detection, the input data is defined on a 2D grid, and as such, we use ConvNets as our chosen function estimators to perform this task
객체 감지의 경우, 입력 데이터는 2D 그리드에 정의되므로 ConvNets를 선택한 함수 추정기로 사용하여 이 작업을 수행합니다
We will discuss how to perform 2D object detection with ConvNets in the next lesson
다음 수업에서 ConvNets로 2D 물체 감지를 수행하는 방법에 대해 논의할 것입니다
But first, we need to figure out how to measure the performance of our algorithm
하지만 먼저, 우리는 알고리즘의 성능을 측정하는 방법을 알아내야 한다
Given the output of a 2D object detector in red, we want to be able to compare how well it fits the true output, usually labeled by humans
빨간색의 2D 물체 검출기의 출력을 감안할 때, 우리는 그것이 보통 인간이 표시하는 실제 출력에 얼마나 잘 맞는지 비교할 수 있기를 원합니다
We call the true output our ground truth bounding box
우리는 진정한 출력을 우리의 지상 진실 경계 상자라고 부른다
The first step of our evaluation process is to compare our detector localization output to the ground truth boxes via the Intersection-Over-Union metric, or IOU for short
평가 프로세스의 첫 번째 단계는 Intersection-Over-Union 메트릭 또는 IOU를 통해 검출기 현지화 출력을 지상 진실 상자와 비교하는 것입니다
IOU is defined as the area of the intersection of two polygons divided by the area of their union
IOU는 연합의 영역으로 나눈 두 다각형의 교차점 영역으로 정의된다
However, calculating the intersection-over-union does not take into consideration the class scores
그러나, 교차로 연봉을 계산하는 것은 수업 점수를 고려하지 않는다
To account for class scores, we define true positives
수업 점수를 설명하기 위해, 우리는 진정한 긍정적인 점을 정의한다
True positives are output bounding boxes that have an IOU greater than a predefined threshold with any ground truth bounding box
진정한 긍정은 지상 진실 경계 상자가 있는 미리 정의된 임계값보다 큰 IOU를 가진 출력 경계 상자이다
In addition, the class of those output boxes should also match the class of their corresponding ground truth
또한, 그 출력 상자의 클래스는 해당 지상 진실의 클래스와 일치해야 한다
That means that the 2D detector should give the highest class score to the correct class, have a score that is greater than a score threshold
그것은 2D 탐지기가 올바른 클래스에 가장 높은 학급 점수를 주고, 점수 임계값보다 큰 점수를 가져야 한다는 것을 의미합니다
On the other hand, false positives are the output boxes that have a score greater than the score threshold, but an IOU less than the IOU threshold with all ground truth bounding boxes
반면에, 오탐은 점수 임계값보다 큰 점수를 가진 출력 상자이지만, 모든 지상 진실 경계 상자가 있는 IOU 임계값보다 적은 IOU이다
This can be easily computed as the total number of detected objects after the application of the score threshold minus the number of true positives
이것은 점수 임계값을 적용한 후 감지된 물체의 총 수에서 실제 양성 수를 뺀 것으로 쉽게 계산할 수 있다
The final base quantity we would like to estimate is the number of false negatives
우리가 추정하고 싶은 최종 기본 수량은 거짓 네거티브의 수이다
False negatives are the ground truth bounding boxes that have no detections associated with them through IOU
거짓 네거티브는 IOU를 통해 그들과 관련된 탐지가 없는 지상 진실 경계 상자이다
Once we have determined the true positives, false positives, and false negatives; we can determine the precision and recall of our 2D object detector according to the following
일단 우리가 진정한 양성, 오탐 및 거짓 네거티브를 결정하면; 우리는 다음에 따라 2D 물체 검출기의 정밀도와 리콜을 결정할 수 있습니다
The precision is the number of true positives divided by the sum of the true positives and the false positives
정확성은 진정한 긍정의 수와 거짓 긍정의 합으로 나눈 진정한 긍정의 수이다
The recall on the other hand is the number of true positives divided by the total number of ground truth objects, which is equal to the number of true positives added to the number of false negatives
반면에 리콜은 지상 진리 물체의 총 수로 나눈 진정한 양성의 수이며, 이는 거짓 음성의 수에 추가된 진정한 양성의 수와 같다
Once we determine the precision and recall, we can vary the object class score threshold to get a precision recall curve, and finally, we determine the average precision as the area under the precision-recall curve
정밀도와 리콜을 결정하면, 정밀 리콜 곡선을 얻기 위해 객체 클래스 점수 임계값을 변경할 수 있으며, 마지막으로, 정밀도 리콜 곡선 아래의 영역으로 평균 정밀도를 결정합니다
The area under the curve can be computed using numerical integration, but is usually approximated using an average of the precision values at 11 recall points ranging from zero to one
곡선 아래의 영역은 수치 통합을 사용하여 계산할 수 있지만, 일반적으로 0에서 1에 이르는 11개의 리콜 포인트에서 정밀도 값의 평균을 사용하여 근사치된다
I know these are quite a few concepts to understand the first time through
나는 이것들이 처음으로 이해해야 할 꽤 많은 개념이라는 것을 알고 있다
But don't worry, as you'll soon get a chance to work through a step-by-step practice notebook on how to code all of these methods in Python in the assessments
하지만 곧 평가에서 파이썬에서 이러한 모든 메소드를 코딩하는 방법에 대한 단계별 연습 노트북을 통해 작업할 기회를 갖게 될 테니 걱정하지 마세요
Let's work through an example on how to assess the performance of a 2D object detection network using the learned metrics
학습된 메트릭을 사용하여 2D 객체 감지 네트워크의 성능을 평가하는 방법에 대한 예를 살펴보겠습니다
We are interested in detecting only cars in a road scene
우리는 도로 장면에서 자동차만 감지하는 데 관심이 있다
That means that we have a single class of interest, and therefore only one set of scores to consider
그것은 우리가 하나의 관심 클래스가 있다는 것을 의미하며, 따라서 고려해야 할 점수는 하나뿐이다
We are given ground truth bounding boxes of cars labeled by human beings and shown in green
우리는 인간이 라벨을 붙이고 녹색으로 표시된 자동차의 지상 진실 경계 상자를 받는다
We process our image with a confinet to get the detection output bounding boxes, shown in red
우리는 빨간색으로 표시된 감지 출력 경계 상자를 얻기 위해 confinet으로 이미지를 처리합니다
You can notice that the network mistakenly detects the front of a large truck as a car
네트워크가 대형 트럭의 전면을 자동차로 잘못 감지한다는 것을 알 수 있습니다
Looking at the scores, we see that our confinet gave this miss detection quite a high score of being a car
점수를 보면, 우리는 우리의 confinet이 이 미스 탐지를 자동차라는 점에서 꽤 높은 점수를 주었다는 것을 알 수 있다
Let's now evaluate the performance of our confinet using average precision
이제 평균 정밀도를 사용하여 confinet의 성능을 평가해 봅시다
The first step is to take all of our estimated bounding boxes and sort them according to object class score
첫 번째 단계는 모든 예상 경계 상자를 가져와 객체 클래스 점수에 따라 정렬하는 것입니다
We then proceed to compute the IOU between each predicted box and the corresponding ground truth box
그런 다음 각 예측 상자와 해당 지상 진실 상자 사이의 IOU를 계산합니다
If a box does not intersect any ground-truth boxes, it's IOU is set to zero
상자가 접지 진실 상자와 교차하지 않으면, IOU는 0으로 설정됩니다
First, we said a class score threshold, let's say 0
먼저, 우리는 수업 점수 임계값을 말했다, 0
9
9라고 합시다
This threshold means that we only trust our network prediction, if it returns a score that is greater than nine, and we eliminate any bounding boxes with a score less than 0
이 임계값은 9보다 큰 점수를 반환하고 0
9
9 미만의 점수로 경계 상자를 제거하는 경우에만 네트워크 예측을 신뢰한다는 것을 의미합니다
Next, we set an IOU threshold, we'll use 0
다음으로, 우리는 IOU 임계값을 설정하고, 이 경우 0
7 in this case and proceed to eliminate any remaining predictions with an IOU less than 0
7을 사용하고 IOU가 0
7
7 미만인 나머지 예측을 제거할 것입니다
In this case, both the remaining predictions have an IOU of greater than 0
이 경우, 나머지 두 예측 모두 0
7, and so we don't eliminate any
7보다 큰 IOU를 가지고 있으므로, 우리는 아무것도 제거하지 않습니다
We can now compute the number of true positives as the number of remaining bounding boxes after the application of both the score and the IOU thresholds, which in this case is two
이제 점수와 IOU 임계값을 모두 적용한 후 남은 경계 상자의 수로 진정한 긍정의 수를 계산할 수 있으며, 이 경우 2입니다
The number of false positives is zero in this case, since all boxes remaining after the application of the score thresholds also remain after the application of the IOU threshold
점수 임계값 적용 후 남은 모든 상자도 IOU 임계값 적용 후에도 남아 있기 때문에 이 경우 오탐의 수는 0입니다
Finally, the number of false negatives are boxes in the ground truth that have no detections associated with them after the application of both the score and the IOU thresholds
마지막으로, 거짓 네거티브의 수는 점수와 IOU 임계값을 모두 적용한 후 그들과 관련된 탐지가 없는 지상 진실의 상자이다
In this case, the number of false negatives is two
이 경우, 거짓 네거티브의 수는 두 개이다
The precision of our neural network is computed as the number of true positives divided by their sum with the number of false positives
우리 신경망의 정밀도는 진정한 양성의 수를 오탐의 수와 합으로 나눈 것으로 계산된다
In this case, we don't have false positives
이 경우, 우리는 거짓 긍정이 없다
So the precision is 2 over 2 equal to 1
그래서 정밀도는 2보다 2가 1과 같다
To compute the recall, we divide the number of true positives by the number of ground truth bounding boxes, which is equal to the number of false positives summed with the number of false negatives
리콜을 계산하기 위해, 우리는 진정한 양성의 수를 지상 진실 경계 상자의 수로 나눕니다
The recall in this case is 2 over 4
이는 거짓 네거티브의 수로 합산된 거짓 양성의 수와 같습니다
The detector in this case is a high precision low recall detector
이 경우의 리콜은 4개 이상이다
This means that the detector misses some objects in the scene, but when it does detect an object, it makes very few mistakes in category classification and bounding box location
이 경우 검출기는 고정밀 낮은 리콜 검출기이다
Let's see how the performance of our detector changes when we decrease the score threshold from 0
이것은 탐지기가 장면에서 일부 물체를 놓쳤다는 것을 의미하지만, 물체를 감지할 때 카테고리 분류와 경계 상자 위치에서 실수를 거의 하지 않는다
9 to 0
점수 임계값을 0
7
9에서 0
All bounding boxes have a score greater than 0
7로 낮출 때 탐지기의 성능이 어떻게 변하는지 봅시다
7, so we do not eliminate any of them through score thresholding
모든 경계 상자는 0
However, when we examine the IOU of the remaining boxes, we can see that two of them have an IOU less than 0
7보다 큰 점수를 가지고 있으므로 점수 임계값을 통해 그 중 어느 것도 제거하지 않습니다
7
그러나, 우리가 나머지 상자의 IOU를 검토할 때, 우리는 그들 중 두 개가 0
By eliminating these two boxes, we get three true positives
7 미만의 IOU를 가지고 있다는 것을 알 수 있다
To compute the number of false positives, we need to look at how many detections remained after the application of the score threshold, but before the application of the IOU threshold
이 두 상자를 제거함으로써, 우리는 세 가지 진정한 긍정적인 면을 얻는다
In this case, the number of false positives is two
오탐의 수를 계산하려면, 점수 임계값을 적용한 후 IOU 임계값을 적용하기 전에 얼마나 많은 탐지가 남아 있는지 살펴볼 필요가 있다
Finally, we take a look at the number of ground truth bounding boxes that have remained without an associated detection after the application of both the IOU and score thresholds to get one as the number of false negatives
이 경우, 거짓 긍정의 수는 두 개이다
Notice that the precision has dropped after decreasing the score threshold from one to 0
마지막으로, 우리는 IOU와 점수 임계값을 모두 적용한 후 관련 탐지 없이 남아 있는 지상 진실 경계 상자의 수를 살펴보고 거짓 네거티브의 수로 얻습니다
6, while the recall has increased from 0
점수 임계값을 1에서 0
5 to 0
6로 낮춘 후 정밀도가 떨어졌고, 리콜은 0
75
5에서 0
We can conclude that the effect of lowering the score threshold is less accurate detection results at the expense of detecting more objects in the scene
75로 증가했습니다
If we continue this process and estimate the score threshold at decrements of 0
우리는 점수 임계값을 낮추는 효과가 장면에서 더 많은 물체를 감지하는 비용으로 덜 정확한 감지 결과라고 결론지을 수 있다
01, we arrive at the following table
이 과정을 계속하고 점수 임계값을 0
We then proceed to plot the precision-recall curve, using the precision values on the y-axis and the recall values on the x-axis
01 감소로 추정하면 다음 표에 도달합니다
Note that we also add the precision recall points of one and zero as the first in the plot, and zero one as the final point in the plot
그런 다음 y축의 정밀도 값과 x축의 리콜 값을 사용하여 정밀 리콜 곡선을 플로팅합니다
This allows us to approximate the average precision by calculating the area under the P-R curve using 11 recall points between zero and one, at 0
우리는 또한 플롯의 첫 번째로 1과 0의 정밀 리콜 포인트를 추가하고, 플롯의 마지막 포인트로 0을 추가한다는 점에 유의하십시오
01 recall increments
이를 통해 0
Computing this average produces an AP of 0
01 리콜 단위로 0에서 1 사이의 11개의 리콜 포인트를 사용하여 P-R 커브 아래의 영역을 계산하여 평균 정밀도를 근사화할 수 있습니다
75 for a car detector
이 평균을 계산하면 자동차 탐지기의 경우 0
The value of the average precision of the detector can be thought of as an average of performance over all score thresholds allowing objective comparison of the performance of detectors without having to consider the exact score threshold that generated those detections
75의 AP가 생성됩니다
In this video, you learned how to formulate the 2D object detection problem and how to evaluate a 2D object detectors performance using the average precision performance metric
검출기의 평균 정밀도 값은 모든 점수 임계값에 대한 평균 성능으로 생각할 수 있으며, 이러한 탐지를 생성한 정확한 점수 임계값을 고려하지 않고도 검출기의 성능을 객관적으로 비교할 수 있습니다
Next lesson, you will learn how to use confinet as 2D object detectors for self-driving cars
이 비디오에서는 2D 물체 감지 문제를 공식화하는 방법과 평균 정밀 성능 메트릭을 사용하여 2D 객체 검출기 성능을 평가하는 방법을 배웠습니다
See you then
다음 수업에서는 자율주행 자동차를 위한 2D 물체 검출기로 confinet을 사용하는 방법을 배우게 될 것입니다

그때 보자


