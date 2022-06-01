Hello and welcome to the final technical module of the visual perception for self-driving course
안녕하세요, 자율주행 과정에 대한 시각적 인식의 최종 기술 모듈에 오신 것을 환영합니다
This module will be dedicated to another important perception task for self-driving cars, semantic segmentation
이 모듈은 자율주행 자동차, 시맨틱 세분화를 위한 또 다른 중요한 인식 작업에 전념할 것이다
Semantic segmentation is useful for a range of self-driving perception tasks such as identifying where the road boundaries are and tracking motion relative to lane markings
시맨틱 세분화는 도로 경계가 어디에 있는지 식별하고 차선 표시에 대한 움직임을 추적하는 것과 같은 다양한 자율주행 인식 작업에 유용합니다
By the end of this module, you will also be able to use semantic segmentation results to aid in 2D object detection
이 모듈이 끝날 때까지, 당신은 또한 2D 물체 감지를 돕기 위해 의미론적 세분화 결과를 사용할 수 있을 것입니다
Semantic segmentation is also very important for domains other than self-driving cars
시맨틱 세분화는 자율주행 자동차 이외의 도메인에서도 매우 중요하다
Medical image segmentation is a rapidly growing field with recent methods using the models you will learn this week to perform tasks ranging from tumor segmentation in CAT scans to cavity segmentation in tooth x-ray images
의료 이미지 세분화는 CAT 스캔의 종양 세분화에서 치아 엑스레이 이미지의 캐비티 세분화에 이르기까지 작업을 수행하기 위해 이번 주에 배우게 될 모델을 사용하여 빠르게 성장하는 분야입니다
In fact, during an international medical imaging segmentation challenge in 2017, ConvNets demonstrated abilities within one percent of human level performance
사실, 2017년 국제 의료 이미징 세분화 과제 동안 ConvNets는 인간 수준의 성능의 1% 내에서 능력을 입증했다
The semantic segmentation models we will learn about in this course are versatile and usually transfer well to tasks outside the domain of self-driving cars
우리가 이 과정에서 배우게 될 의미론적 세분화 모델은 다재다능하며 일반적으로 자율주행 자동차의 영역 외부의 작업으로 잘 전달됩니다
In this lesson, you will learn how to formulate the problem of semantic segmentation
이 수업에서, 당신은 의미론적 세분화의 문제를 공식화하는 방법을 배우게 될 것입니다
You will also learn how to evaluate semantic segmentation models using common evaluation metrics such as the class IOU
또한 수업 IOU와 같은 일반적인 평가 평가 기준을 사용하여 의미론적 세분화 모델을 평가하는 방법을 배우게 됩니다
Let's begin by defining the semantic segmentation problem
의미론적 세분화 문제를 정의하는 것으로 시작합시다
Given an input image, we want to classify each pixel into a set of preset categories
입력 이미지가 주어지면, 우리는 각 픽셀을 사전 설정된 카테고리 세트로 분류하고 싶습니다
The categories can be static road elements such as roads, sidewalk, pole, traffic lights, and traffic signs or dynamic obstacles such as cars, pedestrians, and cyclists
카테고리는 도로, 보도, 극, 신호등, 교통 표지판과 같은 정적 도로 요소 또는 자동차, 보행자 및 자전거 운전자와 같은 역동적인 장애물이 될 수 있습니다
Also, we always have a background class that encompasses any category we do not include in our preset categories
또한, 우리는 항상 사전 설정 범주에 포함되지 않은 카테고리를 포함하는 배경 클래스를 가지고 있습니다
As with object detection, we realize the semantic segmentation through a function estimator
물체 감지와 마찬가지로, 우리는 함수 추정기를 통해 의미론적 세분화를 실현한다
So, how do we adapt our generic neural network to work for segmentation
그렇다면, 세분화를 위해 일반적인 신경망을 어떻게 조정하나요
Given an image, we take every pixel as an input and output a vector of class scores per pixel
이미지가 주어지면, 우리는 모든 픽셀을 입력으로 받아들이고 픽셀당 클래스 점수 벡터를 출력합니다
A pixel belongs to the class with the highest class score
픽셀은 학급 점수가 가장 높은 클래스에 속한다
Therefore, we want our estimator to give the highest score to the correct class for every pixel in an image
따라서, 우리는 추정기가 이미지의 모든 픽셀에 대해 올바른 클래스에 가장 높은 점수를 주기를 원합니다
As an example, a road pixel should have a very high road score and much lower scores for other classes
예를 들어, 도로 픽셀은 다른 수업에서 도로 점수가 매우 높고 점수가 훨씬 낮아야 한다
When we look at a pixel belonging to the sidewalk, the function estimator should provide a higher sidewalks score than all other class scores
보도에 속한 픽셀을 볼 때, 함수 추정기는 다른 모든 수업 점수보다 더 높은 보도 점수를 제공해야 합니다
When attempting to perform semantic segmentation, we usually face many of the same problems as object detection
의미 세분화를 수행하려고 할 때, 우리는 보통 물체 감지와 같은 많은 문제에 직면한다
As such, semantic segmentation is a non-trivial problem
따라서, 의미론적 세분화는 사소한 문제이다
Occlusion and truncation, for example, make it hard to accurately predict object boundaries
예를 들어, 폐색과 절단은 물체 경계를 정확하게 예측하기 어렵게 만든다
Scale is also a major issue as we need to handle both close-by objects with fine detail and far away objects captured by only a few pixels
스케일은 또한 미세한 디테일로 가까운 물체와 몇 픽셀로 캡처된 멀리 떨어진 물체를 모두 처리해야 하기 때문에 주요 문제이다
We also need to be able to handle illumination changes in the scene
우리는 또한 현장의 조명 변화를 처리할 수 있어야 한다
However, semantic segmentation also has a major problem specific difficulty
그러나, 의미론적 세분화는 또한 주요 문제별 어려움을 가지고 있다
This difficulty is caused by an ambiguity of boundaries in image space, especially for thin objects such as poles, similar looking objects such as a road and a sidewalk and far away objects
이러한 어려움은 이미지 공간의 경계 모호함, 특히 극과 같은 얇은 물체, 도로와 보도와 같은 유사한 모양의 물체 및 멀리 떨어진 물체에 의해 발생합니다
Later on, we will see how to handle this problem when designing semantic segmentation algorithms
나중에, 우리는 의미론적 세분화 알고리즘을 설계할 때 이 문제를 처리하는 방법을 볼 것이다
What algorithms do you think we can use to solve semantic segmentation
의미론적 세분화를 해결하기 위해 어떤 알고리즘을 사용할 수 있다고 생각하십니까
If you answered ConvNets, you are correct
만약 당신이 ConvNets에 대답했다면, 당신이 옳습니다
Similar to object detection ConvNets have proven to be very efficient options for solving semantic segmentation problems
물체 감지 ConvNets와 마찬가지로 의미론적 세분화 문제를 해결하기 위한 매우 효율적인 옵션으로 입증되었다
We will discuss the details of this solution in the next lesson, but first, let's determine how to measure the performance of a semantic segmentation network
다음 수업에서 이 솔루션의 세부 사항을 논의할 것이지만, 먼저 의미론적 세분화 네트워크의 성능을 측정하는 방법을 결정합시다
Let's begin by reviewing some basic classification metrics
몇 가지 기본적인 분류 평가 기준을 검토해 봅시다
The first metric to define is the true positives
정의해야 할 첫 번째 메트릭은 진정한 긍정이다
The number of correctly classified pixels belonging to a certain class X
특정 클래스 X에 속하는 올바르게 분류된 픽셀의 수
The second metric is the number of pixels that do not belong to the class X but are classified as that class
두 번째 메트릭은 클래스 X에 속하지 않지만 해당 클래스로 분류되는 픽셀 수입니다
This metric is termed the false positives
이 지표는 거짓 긍정이라고 불린다
Finally, the false negatives are computed as the number of pixels that belong to the class X but are not classified as that class
마지막으로, 거짓 네거티브는 클래스 X에 속하지만 해당 클래스로 분류되지 않는 픽셀 수로 계산됩니다
These terms are identical to those used in object detection
이 용어들은 물체 감지에 사용되는 것과 동일하다
Using these three metrics, we can compute the most commonly used semantic segmentation evaluation metric, the class IOU
이 세 가지 메트릭을 사용하여 가장 일반적으로 사용되는 의미 세분화 평가 메트릭인 클래스 IOU를 계산할 수 있습니다
The class IOU is computed as the total true positives divided by the sum of the true positives, false positives, and false negatives
클래스 IOU는 진정한 긍정, 거짓 긍정, 거짓 네거티브의 합으로 나눈 총 진정한 양성으로 계산된다
Let's take a look at a visual example of this calculation
이 계산의 시각적 예를 살펴보자
The ground truth segmentation data is represented as a single class per pixel
지상 진실 세분화 데이터는 픽셀당 단일 클래스로 표현된다
Similarly, by taking the class with the maximum output score as our predicted class, the prediction can be put in a similar format
마찬가지로, 예상 클래스로 최대 출력 점수로 수업을 수강함으로써, 예측은 비슷한 형식으로 넣을 수 있다
We now begin by computing the class IOU for the road class represented by R
우리는 이제 R로 대표되는 도로 클래스에 대한 클래스 IOU를 계산하는 것으로 시작합니다
The first metric to measure is the number of true positives
측정해야 할 첫 번째 메트릭은 진정한 긍정의 수이다
We can determine the true positives by counting the correctly classified road pixels in our prediction
우리는 예측에서 올바르게 분류된 도로 픽셀을 계산하여 진정한 긍정적인 면을 결정할 수 있다
In this case, three
이 경우, 셋
The second metric, the false positives is zero in our case as our algorithm did not classify any of the sidewalk pixels as road
두 번째 지표인 오탐은 알고리즘이 보도 픽셀을 도로로 분류하지 않았기 때문에 우리의 경우 0이다
Finally, our algorithm classified to road pixels as sidewalk, hence the false-negative count is two
마지막으로, 우리의 알고리즘은 도로 픽셀로 보도로 분류되므로 허위 음성 수는 두 개입니다
Our final IOU for the road is then three-fifths
도로에 대한 우리의 마지막 IOU는 5분의 3이다
Let's follow this procedure for the sidewalk class
보도 수업을 위해 이 절차를 따르자
We can see that we have four correctly classified pixels, hence our true positive count as four
우리는 4개의 올바르게 분류된 픽셀을 가지고 있다는 것을 알 수 있으므로, 우리의 진정한 양수는 4로 계산됩니다
Furthermore, our algorithm mistakenly assigns two pixels to the sidewalk class where, in fact, they belong to the road class
게다가, 우리의 알고리즘은 실제로 도로 클래스에 속하는 보도 클래스에 두 픽셀을 잘못 할당합니다
Therefore, our false positive count is two
그러므로, 우리의 거짓 양성 수는 두 가지이다
Finally, the algorithm did not miss any sidewalk pixels, so it's false-negative count is zero
마지막으로, 알고리즘은 보도 픽셀을 놓치지 않았기 때문에 허위 음성 수는 0이다
We can then compute the sidewalk class IOU as four-sixths
그런 다음 보도 클래스 IOU를 46분의 4로 계산할 수 있습니다
We have performed the class IOU computation over a single image
우리는 단일 이미지로 클래스 IOU 계산을 수행했습니다
When performing this computation on multiple images, one has to keep in mind to compute the true positives, false positives, and false negatives over all of the images and then compute the IOU
여러 이미지에서 이 계산을 수행할 때, 모든 이미지에 대한 진정한 긍정, 오탐 및 허위 네거티브를 계산한 다음 IOU를 계산하는 것을 명심해야 합니다
Computing the IOU per image and then averaging will actually give you an incorrect class IOU score
이미지당 IOU를 계산한 다음 평균하면 실제로 잘못된 클래스 IOU 점수를 받을 수 있습니다
Furthermore, it is usually a better idea to independently look at each class IOU score rather than averaging them
게다가, 보통 각 클래스 IOU 점수를 평균하기보다는 독립적으로 보는 것이 더 좋은 생각이다
This is because a global IOU measure is biased towards object incidences that cover a large image area
이것은 글로벌 IOU 조치가 큰 이미지 영역을 덮는 물체 발생률에 편향되어 있기 때문이다
In street scenes with their strong scale variation, this can be problematic
스케일이 강한 거리 장면에서, 이것은 문제가 될 수 있다
Other metrics such as per instance IOU are usually used to remedy this problem
인스턴스별 IOU와 같은 다른 지표는 보통 이 문제를 해결하는 데 사용된다
The Cityscapes benchmark is one of the most used benchmarks for evaluating semantic segmentation algorithms for self-driving cars
Cityscapes 벤치마크는 자율주행 자동차의 의미론적 세분화 알고리즘을 평가하는 데 가장 많이 사용되는 벤치마크 중 하나이다
The per class IOU is used as the main ranking metric for semantic segmentation models submitted to the Cityscapes benchmark
클래스별 IOU는 Cityscapes 벤치마크에 제출된 시맨틱 세분화 모델의 주요 순위 지표로 사용됩니다
Although, the instance level IOU is also computed for each model
하지만, 인스턴스 레벨 IOU도 각 모델에 대해 계산됩니다
In this lesson, you learned that semantic segmentation consists of providing a class label for every pixel in a 2D image
이 수업에서, 당신은 의미론적 세분화는 2D 이미지의 모든 픽셀에 대한 클래스 라벨을 제공하는 것으로 구성되어 있다는 것을 배웠습니다
You also learned how to evaluate semantic segmentation models using the per class IOU
또한 수업별 IOU를 사용하여 의미론적 세분화 모델을 평가하는 방법을 배웠습니다
In the next lesson, we will learn how to use convolutional neural networks to solve the semantic segmentation problem
다음 수업에서, 우리는 의미론적 세분화 문제를 해결하기 위해 컨볼루션 신경망을 사용하는 방법을 배울 것이다
See you then
그때 보자


