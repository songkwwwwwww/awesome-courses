In the last lesson, we described the general object detection problem as well as how to evaluate the performance of 2G object detectors using average precision
마지막 수업에서, 우리는 일반적인 물체 감지 문제와 평균 정밀도를 사용하여 2G 물체 검출기의 성능을 평가하는 방법을 설명했습니다
This lesson will describe the steps involved in performing 2D object detection using convNets
이 수업에서는 convNets를 사용하여 2D 물체 감지를 수행하는 것과 관련된 단계를 설명합니다
Keep in mind that the field of 2D object detection is rapidly changing with new methods emerging everyday
2D 물체 감지 분야는 매일 새로운 방법이 등장함에 따라 빠르게 변화하고 있다는 것을 명심하세요
What we will be describing is a modern approach to 2D object detection using ConvNets, but without many of the intricacies that allow state of the art detectors to eke out the best possible performance
우리가 설명할 것은 ConvNets를 사용하여 2D 물체 감지에 대한 현대적인 접근 방식이지만, 최첨단 탐지기가 최상의 성능을 발휘할 수 있는 많은 복잡성은 없습니다
If you find this topic is exciting as we do, check out the list of some of the current top 2D object detection papers we've included in the supplementary material
이 주제가 우리처럼 흥미롭다면, 보충 자료에 포함시킨 현재 상위 2D 물체 감지 논문 목록을 확인하세요
In this lesson, you will learn how to build a standard single-stage ConvNet architecture for 2D object detection using the network layers we learned about in module three
이 수업에서는 모듈 3에서 배운 네트워크 레이어를 사용하여 2D 객체 감지를 위한 표준 단일 단계 ConvNet 아키텍처를 구축하는 방법을 배우게 됩니다
In addition, we will discuss some common designs that researchers have formulated for ConvNets used for 2D object detection
또한, 우리는 연구자들이 2D 물체 감지에 사용되는 ConvNets를 위해 공식화한 몇 가지 일반적인 설계에 대해 논의할 것입니다
Let's begin by reviewing the 2D object detection problem
2D 물체 감지 문제를 검토하는 것으로 시작합시다
Given an image as an input, we want to simultaneously localize all objects in the scene and determine which class they belong to
이미지를 입력으로 감안할 때, 우리는 장면의 모든 객체를 동시에 현지화하고 그들이 속한 클래스를 결정하고 싶습니다
Let's see how we can perform this task using a ConvNet
ConvNet을 사용하여 이 작업을 어떻게 수행할 수 있는지 봅시다
This figure shows the basic ConvNet configuration used for 2D object detection
이 그림은 2D 객체 감지에 사용되는 기본 ConvNet 구성을 보여줍니다
We call this configuration a neural network architecture
우리는 이 구성을 신경망 아키텍처라고 부른다
The architecture takes as an input an image and a set of manually crafted prior boxes
아키텍처는 입력 이미지와 수동으로 제작된 이전 상자 세트로 사용합니다
First, the image is processed using a feature extractor
먼저, 이미지는 기능 추출기를 사용하여 처리됩니다
Second, a set of fully connected layers take as an input, the output of the feature extractor and provide a location refinement of each 2D prior box as well as a classification
둘째, 완전히 연결된 레이어 세트는 입력, 기능 추출기의 출력을 취하고 각 2D 이전 상자의 위치 개선과 분류를 제공합니다
Finally, non maximum suppression is performed on the output of the fully connected layers to generate the final detections
마지막으로, 최종 탐지를 생성하기 위해 완전히 연결된 레이어의 출력에서 비최대 억제가 수행됩니다
Let's delve deeper into each of these steps
이 단계들 각각에 대해 더 깊이 탐구해 봅시다
We will begin our discussion with the feature extraction stage
우리는 기능 추출 단계에 대한 논의를 시작할 것이다
Feature extractors are the most computationally expensive component of the 2D object detector
기능 추출기는 2D 물체 검출기의 가장 계산적으로 비싼 구성 요소이다
It is typical to have as much as 90 percent of the total architectures required computation used at this stage
이 단계에서 필요한 전체 아키텍처의 90%를 계산하는 것이 일반적이다
The output of feature extractors usually has much lower width and height than those of the input image
피처 추출기의 출력은 일반적으로 입력 이미지보다 너비와 높이가 훨씬 낮다
However, its depth is usually two to three orders of magnitude greater than that of the input image
그러나, 그것의 깊이는 보통 입력 이미지의 깊이보다 2~3배 더 크다
The design of feature extractors is a very active area of research with new extractors emerging on a regular basis
특징 추출기의 설계는 새로운 추출기가 정기적으로 등장하는 매우 활발한 연구 분야이다
The most common feature extractors used are VGG, ResNet, and Inception
사용되는 가장 일반적인 기능 추출기는 VGG, ResNet 및 Inception이다
We will be focusing on the VGG feature extractor as our running example throughout the rest of this lesson
우리는 이 수업의 나머지 부분에서 실행 예시로 VGG 기능 추출기에 초점을 맞출 것입니다
The VGG feature extractor is based on the convolutional layers of the VGG 16 classification network proposed by the Visual Geometry Group at Oxford University
VGG 기능 추출기는 옥스퍼드 대학교의 시각 기하학 그룹이 제안한 VGG 16 분류 네트워크의 컨볼루션 계층을 기반으로 합니다
It is one of the first feature extractors to be proposed for detection and is quite simple to build
그것은 탐지를 위해 제안된 최초의 특징 추출기 중 하나이며 구축하기가 매우 쉽다
As with most ConvNets, the VGG feature extractor is built by alternating convolutional layers and pooling layers
대부분의 ConvNets와 마찬가지로, VGG 기능 추출기는 컨볼루션 레이어와 풀링 레이어를 번갈아 가며 만들어졌다
All convolutional layers are of size three by three by K, with a stride of one and a zero-padding of one, by which we mean that the padding of size one is filled with zeros
모든 컨볼루션 레이어는 3 x 3 x 3 x K이며, 1의 보폭과 제로 패딩이 있으며, 이는 1사이즈의 패딩이 0으로 채워져 있다는 것을 의미합니다
All max-pooling layers are of size two by two with stride two and no padding
모든 최대 풀링 레이어는 2 x 2단계이며 패딩이 없습니다
These particular hyper parameters were arrived at through intensive experimentation and have performed extremely well in a wide range of problems making VGG and extremely popular extractor
이러한 특정 하이퍼 매개 변수는 집중적인 실험을 통해 도착했으며 VGG와 매우 인기 있는 추출기를 만드는 광범위한 문제에서 매우 잘 수행되었다
Let's see how these layers affect our output volume shape
이 층들이 우리의 출력 볼륨 모양에 어떤 영향을 미치는지 봅시다
Last week, we derive the three equations for the output width, height, and depth based on the input volume after it has been passed through the convolutional layer
지난 주에, 우리는 컨볼루션 레이어를 통과한 후 입력 볼륨을 기반으로 출력 너비, 높이 및 깊이에 대한 세 가지 방정식을 도출합니다
For the VGG feature extractor, all convolutions are of size three by three by K, with a stride of one and zero padding of one
VGG 기능 추출기의 경우, 모든 컨볼루션은 3 x 3 x K이며, 1의 보폭과 제로 패딩이 있습니다
That means the passing an input volume through any of the convolutional layers only changes its depth to K
그것은 컨볼루션 레이어를 통해 입력 볼륨을 전달하는 것이 깊이를 K로만 바꾼다는 것을 의미합니다
On the other hand, the pooling layers of the VGG extractor are two by two with stride two and no padding
반면에, VGG 추출기의 풀링 층은 2단계와 패딩이 없는 2대 2이다
Repeating the same analysis using the equations for the pooling layer, we noticed that the max-pooling layers of VGG extractors reduce the width and height of the input volume by two, while maintaining the depth constant
풀링 레이어의 방정식을 사용하여 동일한 분석을 반복하면서, 우리는 VGG 추출기의 최대 풀링 레이어가 깊이 상수를 유지하면서 입력 볼륨의 너비와 높이를 2로 줄인다는 것을 알아차렸다
Let's now see how the VGG extractor processes an input image
이제 VGG 추출기를 입력 이미지를 어떻게 처리하는지 봅시다
Given an M by N by three input image, we pass it through the first two convolutional layers of depth 64 followed by the first pooling layer
M x N을 세 개의 입력 이미지로 감안할 때, 우리는 깊이 64의 처음 두 컨볼루션 레이어와 첫 번째 풀링 레이어를 통과합니다
At this point, the output volume width and height are reduced by a factor of two, while the depth is expanded to 64
이 시점에서, 출력 볼륨 너비와 높이는 2배로 줄어들고, 깊이는 64로 확장된다
We can separate the VGG feature extractor into subsections, where each subsection ends with a pooling layer
VGG 기능 추출기를 각 하위 섹션이 풀링 레이어로 끝나는 하위 섹션으로 분리할 수 있습니다
The first subsection is called the Conv1 subsection of the VGG extractor
첫 번째 하위 섹션은 VGG 추출기의 Conv1 하위 섹션이라고 불린다
We then proceed to pass the output volume through the rest of the five subsections to arrive at our final output volume of shape M over 32, N over 32, and 512
그런 다음 나머지 5개의 하위 섹션을 통해 출력 볼륨을 통과하여 32 이상의 모양 M, 32 이상의 N 및 512의 최종 출력 볼륨에 도달합니다
As an example, if we have a 1,240 by 960 by 3 image as our input, our final output volume shape will be 40 by 30 by 512
예를 들어, 입력으로 1,240 x 960 x 3 이미지가 있다면, 최종 출력 볼륨 모양은 40 x 30 x 512가 될 것입니다
We will be using this output volume to generate our final detections
우리는 최종 탐지를 생성하기 위해 이 출력 볼륨을 사용할 것이다
The next step to describe in our neural network architecture is the concept of prior boxes
신경망 아키텍처에서 설명하는 다음 단계는 이전 상자의 개념이다
Also called anchor boxes
앵커 박스라고도 불린다
To generate 2D bounding boxes, we usually do not start from scratch and estimate the corners of the bounding box without any prior
2D 경계 상자를 생성하기 위해, 우리는 보통 처음부터 시작하지 않고 사전 없이 경계 상자의 모서리를 추정하지 않습니다
We assume that we do have a prior on where the boxes are in image space and how large these boxes should be
우리는 상자가 이미지 공간에 어디에 있고 이 상자들이 얼마나 커야 하는지에 대한 사전이 있다고 가정합니다
These priors are called anchor boxes and are manually defined over the whole image usually on an equally-spaced grid
이 프라이어들은 앵커 박스라고 불리며 일반적으로 동등한 간격의 그리드에서 전체 이미지에 수동으로 정의됩니다
Let's assume that we have a set of anchors close to our ground-truth boxes
지상 진실 상자 근처에 앵커 세트가 있다고 가정해 봅시다
During training, the network learns to take each of these anchors and tries to move it as close as possible to the ground truth bounding box in both the centroid location and box dimensions
훈련하는 동안, 네트워크는 이러한 각 앵커를 가져가는 법을 배우고 중심 위치와 상자 크기 모두에서 지상 진실 경계 상자에 가능한 한 가깝게 이동하려고 시도한다
This is termed residual learning and it takes advantage of the notion that it is easier to nudge and existing box a small amount to improve it rather than to search the entire image for possible object locations
이것은 잔류 학습이라고 불리며 전체 이미지에서 가능한 개체 위치를 검색하는 것보다 적은 양의 찔러지고 기존 상자를 개선하는 것이 더 쉽다는 개념을 활용합니다
In practice, residual learning has proven to provide much better results than attempting to directly estimate bounding boxes without any prior
실제로, 잔류 학습은 사전 없이 경계 상자를 직접 추정하려고 시도하는 것보다 훨씬 더 나은 결과를 제공하는 것으로 입증되었다
Many different methods have been proposed in the literature on how to use the anchor bounding boxes to generate the final prediction
앵커 경계 상자를 사용하여 최종 예측을 생성하는 방법에 대한 문헌에서 많은 다른 방법이 제안되었다
Usually, the anchors interact with the feature map to generate fixed sized feature vectors for every anchor
일반적으로 앵커는 기능 맵과 상호 작용하여 모든 앵커에 대해 고정된 크기의 피처 벡터를 생성합니다
We'll explain one of the first methods proposed for this interaction by Microsoft Research in their architecture Faster R-CNN
Microsoft Research가 아키텍처 Faster R-CNN에서 이 상호 작용을 위해 제안한 첫 번째 방법 중 하나를 설명할 것입니다
However, keep in mind that this is not the only way to perform such an interaction
그러나, 이것이 그러한 상호 작용을 수행하는 유일한 방법은 아니라는 것을 명심하세요
The Faster R-CNN interaction method is quite simple
더 빠른 R-CNN 상호 작용 방법은 매우 간단하다
For every pixel in the feature map, we associate k anchor boxes
기능 맵의 모든 픽셀에 대해, 우리는 k 앵커 상자를 연결합니다
We then perform a three by three by D star convolution operation on that pixels neighborhood
그런 다음 픽셀 근처에서 D 별 컨볼루션 작업으로 3 x 3을 수행합니다
This results in a one by one by D star feature vector for that pixel
이것은 그 픽셀에 대해 하나씩 D 별 특징 벡터를 초래한다
We use this one by one by D star feature vector as the feature vector of every one of the k anchors associated with that pixel
우리는 이것을 하나씩 D 별 특징 벡터를 해당 픽셀과 관련된 모든 k 앵커의 피처 벡터로 사용합니다
We then proceed to feed the extracted feature vector to the output layers in the neural network
그런 다음 추출된 피처 벡터를 신경망의 출력 계층에 공급합니다
The output layers of a 2D object detector usually comprise of a regression head and a classification head
2D 물체 검출기의 출력 레이어는 일반적으로 회귀 헤드와 분류 헤드를 포함한다
The regression head usually includes multiple fully-connected hidden layers with a linear output layer
회귀 헤드는 일반적으로 선형 출력 레이어가 있는 완전히 연결된 여러 개의 숨겨진 레이어를 포함한다
The regressed output is typically a vector of residuals that need to be added to the anchor that hand to get the ground truth bounding box
회귀 출력은 일반적으로 지상 진실 경계 상자를 얻기 위해 그 손에 있는 앵커에 추가해야 하는 잔류물의 벡터이다
Another method to update the dimension of the anchors is to regress a residual from the center of the anchor to the center of the ground truth bounding box in addition to two scale factors that correct the ground truth bounding box width and height when multiplied with an anchor's width and height
앵커의 치수를 업데이트하는 또 다른 방법은 앵커의 너비와 높이를 곱할 때 지상 진실 경계 상자 너비와 높이를 수정하는 두 가지 스케일 요인 외에도 앵커 중앙에서 지상 진실 경계 상자의 중심으로 잔류물을 회귀하는 것입니다
The classification head is also comprised of multiple fully-connected hidden layers, but with a final softmax output layer
분류 헤드는 또한 완전히 연결된 여러 개의 숨겨진 레이어로 구성되어 있지만, 최종 소프트맥스 출력 레이어가 있다
The softmax output is a vector with a single score per class
소프트맥스 출력은 클래스당 단일 점수를 가진 벡터이다
The highest score usually defines the class of the anchor at hand
가장 높은 점수는 보통 손에 있는 앵커의 클래스를 정의한다
You might note that based on what we described so far, we will end up with k bounding boxes per pixel of the output feature map
지금까지 설명한 내용을 바탕으로 출력 기능 맵의 픽셀당 k 경계 상자로 끝날 것입니다
Even if we consider boxes with high classification score for all classes of interest, we still will have many redundant detections in the image
모든 관심 클래스에 대해 높은 분류 점수를 가진 상자를 고려하더라도, 우리는 여전히 이미지에 많은 중복 감지 사항이 있을 것이다
During average precision computation, we only consider one detection per ground truth bounding box
평균 정밀 계산 동안, 우리는 지상 진실 경계 상자당 하나의 탐지만 고려합니다
Any redundant detections are considered false positives and results in lower precision and thus a lower average precision overall
중복 검출은 오탐으로 간주되며 정밀도가 낮아지고 전체적으로 평균 정밀도가 낮아집니다
Recall, we're aiming for perfect detection, which means we want an output of one box per object in the image
기억하세요, 우리는 완벽한 탐지를 목표로 하고 있으며, 이는 이미지에서 물체당 한 상자의 출력을 원한다는 것을 의미합니다
So, we will need to do something to eliminate the many redundant detections produced by our network
그래서, 우리는 네트워크에서 생성된 많은 중복 탐지를 제거하기 위해 무언가를 해야 할 것이다
In fact, this is only an issue of inference and it turns out to be beneficial to drive the network to output the best possible residuals for every anchor during training
사실, 이것은 추론의 문제일 뿐이며 훈련 중에 모든 앵커에 대해 가능한 최상의 잔류물을 출력하기 위해 네트워크를 구동하는 것이 유익한 것으로 밝혀졌다
Before going deeper into this issue, let's summarize what you learned this lesson
이 문제에 대해 더 자세히 살펴보기 전에, 이 교훈을 배운 내용을 요약해 봅시다
First, you learned that convolutional neural networks can be used to solve the 2D object detection problem and study the details of the VGG feature extractor architecture
첫째, 컨볼루션 신경망을 사용하여 2D 물체 감지 문제를 해결하고 VGG 기능 추출기 아키텍처의 세부 사항을 연구할 수 있다는 것을 배웠습니다
Second, you learned how to use anchor boxes as object location priors and estimate the bounding box residuals to output the final object locations
둘째, 앵커 박스를 객체 위치 프라이어로 사용하고 최종 객체 위치를 출력하기 위해 경계 상자 잔류물을 추정하는 방법을 배웠습니다
In the next lesson, we'll describe how to train 2D object detectors using classification and regression loss functions
다음 수업에서는 분류 및 회귀 손실 함수를 사용하여 2D 개체 탐지기를 훈련시키는 방법을 설명하겠습니다
For that, we will use most of the k output boxes
그것을 위해, 우리는 대부분의 k 출력 상자를 사용할 것이다
We'll then return to the challenge of outputting a single bounding box per object and introduce the concept of non-maximum suppression to solve it
그런 다음 객체당 단일 경계 상자를 출력하는 문제로 돌아가서 그것을 해결하기 위해 최대가 아닌 억제 개념을 도입할 것입니다
See you then
그때 보자


