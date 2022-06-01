[MUSIC] Last lesson we learned a baseline approach to perform object detection using convenance
[음악] 마지막 수업에서 우리는 편리함을 사용하여 물체 감지를 수행하기 위한 기본 접근 방식을 배웠다
However, processing all the anchors in our anchor grid led to multiple bounding boxes being detected per object rather than the expected single locks per object
그러나 앵커 그리드의 모든 앵커를 처리하면 개체당 예상되는 단일 잠금이 아닌 개체당 여러 경계 상자가 감지되었습니다
This lesson, we will discuss the final components we need to build and train convolutional neural networks for 2D object detection
이 수업에서는 2D 물체 감지를 위한 컨볼루션 신경망을 구축하고 훈련시키는 데 필요한 최종 구성 요소에 대해 논의할 것입니다
Specifically, you will learn how to handle multiple regressed anchors per object during training through mini batch selection and during inference through non-maximum suppression
특히, 미니 배치 선택을 통해 훈련하는 동안 그리고 비최대 억제를 통해 추론 중에 물체당 여러 개의 회귀된 앵커를 처리하는 방법을 배우게 될 것입니다
Let's begin by reviewing neural network training
신경망 훈련을 검토하는 것으로 시작합시다
We are given our cond net model and training data pairs, x, the input image, and f star of x, the bounding box locations and class
우리는 cond net 모델과 훈련 데이터 쌍, x, 입력 이미지, f star of x, 경계 상자 위치 및 클래스가 제공됩니다
We want to approximate f star of x with our output bounding boxes y equal to f of x and theta
우리는 출력 경계 상자 y가 x와 세타의 f와 같은 x의 f 별을 근사하고 싶습니다
Recall from last week that we performed training by first evaluating a loss function that measures how similar our predicted bounding boxes are to the ground truth bounding boxes
지난 주부터 예측된 경계 상자가 지상 진실 경계 상자와 얼마나 유사한지 측정하는 손실 함수를 먼저 평가하여 훈련을 수행했다는 것을 상기하십시오
Then we feed the resultant loss function to our optimizer that outputs a new set of parameters theta to be used for the second iteration
그런 다음 결과 손실 함수를 두 번째 반복에 사용할 새로운 매개 변수 세타 세트를 출력하는 옵티마이저에 공급합니다
Notice that both the feature extractor and the output layers are modified during training
기능 추출기와 출력 레이어가 모두 훈련 중에 수정된다는 것을 주목하세요
Now if f star of x and f of x theta are one to one, our problem would have been easy
이제 x 세타의 x와 f의 f 별이 일대일이라면, 우리의 문제는 쉬웠을 것이다
However, the outputs of our network is multiple boxes that can be associated with a single ground truth box
그러나, 우리 네트워크의 출력은 단일 지상 진실 상자와 연관될 수 있는 여러 상자이다
Let's see how we can work to resolve this issue
이 문제를 해결하기 위해 우리가 어떻게 노력할 수 있는지 봅시다
Remember that for each pixel in the feature map, we associate k anchors
기능 맵의 각 픽셀에 대해 k 앵커를 연결한다는 것을 기억하십시오
Where do these anchors appear in the original image
원본 이미지에서 이 앵커들은 어디에 나타나나요
As we've learnt earlier, our feature extractor reduces the resolution of the initial input by a factor of 32
앞서 배웠듯이, 우리의 기능 추출기는 초기 입력의 해상도를 32배 줄입니다
That means that if we associate every pixel in the feature map with a set of anchors, these anchors will be transferred to the initial image by placing them on a grid with stride 32
즉, 기능 맵의 모든 픽셀을 앵커 세트와 연결하면 이러한 앵커를 보폭 32가 있는 그리드에 배치하여 초기 이미지로 전송됩니다
We can then visualize the ground truth bounding box alongside these anchors
그런 다음 우리는 이 앵커와 함께 지상 진실 경계 상자를 시각화할 수 있다
You can notice that some anchors overlap and some don't
일부 앵커가 겹치고 일부는 그렇지 않다는 것을 알 수 있습니다
We quantify this overlap with IOU and categorize the anchors into two categories
우리는 이 중복을 IOU와 정량화하고 앵커를 두 가지 범주로 분류합니다
We first specify two IOU thresholds, a positive anchor threshold, and a negative anchor threshold
먼저 두 개의 IOU 임계값, 양의 앵커 임계값 및 음의 앵커 임계값을 지정합니다
Any anchor with an IOU greater than the positive anchor threshold is called a positive anchor
IOU가 포지티브 앵커 임계값보다 큰 앵커는 포지티브 앵커라고 불린다
And similarly, any anchor with an IOU less than the negative anchor threshold is called a negative anchor
그리고 마찬가지로, IOU가 음의 앵커 임계값보다 작은 앵커는 음수 앵커라고 불린다
Any anchor with an IOU in between the two thresholds is fully discarded
두 임계값 사이에 IOU가 있는 앵커는 완전히 폐기됩니다
So now, how do we use these positive and negative anchors in training
그래서 이제, 우리는 훈련에서 이 긍정적이고 부정적인 앵커를 어떻게 사용하나요
Let's now see how to assign the classification and regression targets for the positive and negative anchors
이제 양수 및 음수 앵커에 대한 분류 및 회귀 목표를 할당하는 방법을 살펴보겠습니다
For classification, we want the neural network to predict that the negative anchors belong to the background class
분류를 위해, 우리는 신경망이 부정적인 앵커가 백그라운드 클래스에 속한다고 예측하기를 원한다
Background is usually a class we add to our classes of interest to describe anything non-included in these classes
배경은 보통 이 수업에 포함되지 않은 것을 설명하기 위해 관심 있는 수업에 추가하는 수업이다
On the other hand, we want the neural network to assign ground truth class to any positive anchor intersecting that ground truth
반면에, 우리는 신경망이 지상 진실과 교차하는 긍정적인 앵커에 지상 진실 클래스를 할당하기를 원한다
For regression, we want to shift the parameters of the positive anchor to be aligned with those of the ground truth bounding box
회귀를 위해, 우리는 양의 앵커의 매개 변수를 지상 진실 경계 상자의 매개 변수와 일치하도록 바꾸고 싶습니다
The negative anchors are not used in bounding box regression as they are assumed to be background
음의 앵커가 배경이라고 가정하기 때문에 경계 상자 회귀에 사용되지 않습니다
This approach of handling multiple regressed anchors during training is not free from problems
훈련 중에 여러 개의 회귀된 앵커를 처리하는 이러한 접근 방식은 문제에서 자유롭지 않다
The proposed IOU thresholding mechanism results in most of the regressed anchors being negative anchors
제안된 IOU 임계값 메커니즘은 대부분의 회귀된 앵커가 부정적인 앵커로 이어진다
When training with all these anchors, the network will be observing far more negative than positive examples leading to a biased towards the negative class
이 모든 앵커로 훈련할 때, 네트워크는 부정적인 클래스로 편향되는 긍정적인 예보다 훨씬 더 부정적인 것을 관찰할 것이다
The solution to this problem is actually quite simple, instead of using all anchors to compute the lost function, we sample the chosen minibatch size with a three to one ratio of negative to positive anchors
이 문제에 대한 해결책은 실제로 매우 간단하며, 손실된 함수를 계산하기 위해 모든 앵커를 사용하는 대신, 우리는 음수와 양의 앵커를 3대 1 비율로 선택한 미니배치 크기를 샘플링합니다
The negatives are chosen through a process called online hard negative mining, in which negative minibatch members are chosen as the negative anchors with the highest classification loss
네거티브는 온라인 하드 네거티브 마이너스 마이닝이라는 프로세스를 통해 선택되며, 마이너스 멤버는 분류 손실이 가장 높은 네거티브 앵커로 선택됩니다
This means that where we've training to fix the biggest errors in negative classification
이것은 우리가 부정적인 분류에서 가장 큰 오류를 해결하기 위한 훈련을 받았다는 것을 의미한다
As an example, if we have a minibatch of 64 examples, the negative minibatch will be the 48 negative examples with the highest classification loss, and the 16 remaining anchors will be positive anchors
예를 들어, 64개의 예제의 미니배치가 있다면, 네거티브 미니배치는 분류 손실이 가장 높은 48개의 네거티브 예가 될 것이며, 나머지 16개의 앵커가 포지티브 앵커가 될 것이다
If the number of positives is less than 16, we either copy some of the positives to pad the minibatch or fill the remaining spots with negative anchors
양성자 수가 16개 미만인 경우, 일부 양성을 복사하여 미니배치를 패딩하거나 나머지 지점을 음의 앵커로 채웁니다
As we described earlier last week, we used the cross entropy loss function for the classification head of our ConvNet
지난 주 초에 설명했듯이, 우리는 ConvNet의 분류 책임자를 위해 교차 엔트로피 손실 함수를 사용했습니다
The total classification loss is the average of the cross entropy loss of all anchors in the minibatch
총 분류 손실은 미니배치의 모든 앵커가 교차 엔트로피 손실의 평균이다
The normalization constant and total is the chosen minibatch size
정규화 상수와 합계는 선택된 미니배치 크기이다
Si is the output of the classification head
Si는 분류 헤드의 출력이다
And Si star is the ground truth classification which is set to background for negative anchors and to the class of the ground truth bounding box for the positive anchors
그리고 Si 별은 부정적인 앵커에 대한 배경과 긍정적인 앵커를 위한 지상 진실 경계 상자의 클래스로 설정된 지상 진실 분류이다
For regression, we use the L2 norm loss in a similar manner
회귀를 위해, 우리는 비슷한 방식으로 L2 표준 손실을 사용합니다
However, we only attempt to modify an anchor if it is a positive anchor
그러나, 우리는 그것이 긍정적인 앵커인 경우에만 앵커를 수정하려고 시도한다
This is expressed mathematically with a multiplier Pi on the L2 norm
이것은 L2 표준에서 승수 Pi로 수학적으로 표현된다
It is 0 if the anchor is negative and 1 if the anchor is positive
앵커가 음수인 경우 0이고 앵커가 양수인 경우 1입니다
To normalize, we divide by the number of positive anchors, and just as a reminder, bi star is the ground truth bounding box representation, while bi is the estimated bounding box
정상화하기 위해, 우리는 양의 앵코의 수로 나뉘며, 상기시켜 드리자면, 바이 스타는 지상 진실 경계 상자 표현이며, 바이는 추정 경계 상자이다
Remember that we don't directly estimate box parameters, but rather, we modify the anchor parameters by an additive residual or a multiplicative scale
박스 매개 변수를 직접 추정하는 것이 아니라 적층 잔류 또는 곱셈 척도로 앵커 매개 변수를 수정한다는 것을 기억하십시오
So bi must be constructed from the estimated residuals
따라서 bi는 예상 잔류물로 구성되어야 한다
Let's visualize what we are trying to teach the neural network to learn with these loss functions
이러한 손실 기능으로 배우기 위해 신경망에 무엇을 가르치려고 하는지 시각화합시다
Given an input image, a ground truth bounding box, and a set of input anchors from the anchor prior, we are teaching the neural network to classify anchors as containing background in purple or a car in blue
입력 이미지, 지상 진실 경계 상자 및 앵커 이전의 입력 앵커 세트를 감안할 때, 우리는 신경망에 앵커를 보라색 배경이나 파란색의 배경을 포함하는 것으로 분류하도록 가르치고 있습니다
This is done by minimizing the cross entropy loss defined above
이것은 위에 정의된 교차 엔트로피 손실을 최소화함으로써 이루어진다
Then we want the neural network to move only anchors that contain a class of interest, in a way that matches the closest ground truth bounding box
그런 다음 우리는 신경망이 가장 가까운 지상 진실 경계 상자와 일치하는 방식으로 관심 클래스가 포함된 앵커만 이동하기를 원합니다
This is done by minimizing the L2 norm loss defined above
이것은 위에 정의된 L2 표준 손실을 최소화함으로써 이루어진다
By now, you should have a good grasp on how to handle multiple output boxes for object during training
지금까지는 훈련 중에 물체에 대한 여러 출력 상자를 처리하는 방법을 잘 이해해야 합니다
But what do we do when we run the neural network in real time during inference
하지만 추론 중에 실시간으로 신경망을 실행할 때 우리는 무엇을 하나요
Remember, during inference, we do not have ground truths to determine positive and negative anchors and we do not evaluate loss functions
추론하는 동안, 우리는 긍정적이고 부정적인 앵커를 결정할 근거가 없으며 손실 기능을 평가하지 않는다는 것을 기억하십시오
We just want a single output box per object in the scene
우리는 장면에서 객체당 단일 출력 상자를 원합니다
Here is when non max suppression comes into play, an extremely powerful approach to improving inference output for anchor based neuron networks
다음은 비최대 억제가 작용할 때, 앵커 기반 뉴런 네트워크의 추론 출력을 개선하는 매우 강력한 접근 방식입니다
Non-max suppression takes as an input a list of predicted boundary boxed b, and each bounding blocks is comprised of the regressed coordinates in the class output score
비최대 억제는 입력으로 예측된 경계 박스 b의 목록을 취하며, 각 경계 블록은 클래스 출력 점수의 회귀 좌표로 구성됩니다
It also needs as an input a predefined IOU threshold which we'll call ada
그것은 또한 입력으로 우리가 ada라고 부를 미리 정의된 IOU 임계값이 필요하다
The algorithm then goes as follows, we first sort the bounding boxes in list B according to their output score
그런 다음 알고리즘은 다음과 같이 진행되며, 먼저 출력 점수에 따라 목록 B의 경계 상자를 정렬합니다
We also initialize an empty set D to hold output bounding boxes
우리는 또한 출력 경계 상자를 보관하기 위해 빈 세트 D를 초기화합니다
We then proceed to iterate overall elements in the sorted box list B bar
그런 다음 정렬된 상자 목록 B 표시줄에서 전체 요소를 반복합니다
Inside the for loop, we first determine the box B max with the highest score in the list B, which should be the first element in B bar
For 루프 내부에서, 우리는 먼저 B 막대의 첫 번째 요소여야 하는 목록 B에서 가장 높은 점수를 가진 상자 B max를 결정합니다
We then remove this bounding box from the bounding box set D bar and add it to the output set D
그런 다음 경계 상자 세트 D 막대에서 이 경계 상자를 제거하고 출력 세트 D에 추가합니다
Next, we find all boxes remaining in the set B bar that have an IOU greater than ada with the box B max
다음으로, 우리는 상자 B max가 있는 ada보다 큰 IOU를 가진 세트 B 바에 남아있는 모든 상자를 찾습니다
These boxes significantly overlap with the current maximum box, B max
이 상자들은 현재 최대 상자인 B max와 크게 겹친다
Any box that satisfies this condition gets removed from the list B bar
이 조건을 충족하는 모든 상자는 목록 B 바에서 제거됩니다
We keep iterating through the list B bar until is empty, and then we return the list D
우리는 비어있을 때까지 목록 B 막대를 계속 반복한 다음, 목록 D를 반환합니다
D now contains a single bounding box per object
D는 이제 객체당 단일 경계 상자를 포함한다
Let's go through a visual example to understand how non-max suppression algorithms work in practice
비최대 억제 알고리즘이 실제로 어떻게 작동하는지 이해하기 위해 시각적 예를 살펴보겠습니다
Let's assume that we have sorted the bounding box list in decreasing order
경계 상자 목록을 줄어든 순서로 분류했다고 가정해 봅시다
We also show the score list explicitly here for better visibility on how non-max suppression works
우리는 또한 비최대 억제가 어떻게 작동하는지에 대한 더 나은 가시성을 위해 여기에 점수 목록을 명시적으로 보여줍니다
b max will be the first bounding box of the sorted list B bar
b max는 정렬된 목록 B 막대의 첫 번째 경계 상자가 될 것입니다
We then proceed to compare each bounding box to b max
그런 다음 각 경계 상자를 b max로 비교합니다
In this case, only one box, B3, has a non zero IOU with b max
이 경우, 하나의 상자인 B3만 b max를 가진 0이 아닌 IOU를 가지고 있다
We compute that IOU and compare it with our IOU threshold ada
우리는 그 IOU를 계산하고 그것을 우리의 IOU 임계값 ada와 비교한다
In this case, the IOU is greater than the threshold ada, so we remove box 3 from the list B bar
이 경우, IOU는 임계값 ada보다 크므로 목록 B 표시줄에서 상자 3을 제거합니다
We repeat the process for the next highest score that remains in the list
우리는 목록에 남아있는 다음으로 높은 점수에 대한 과정을 반복합니다
Again, only one box has a non-zero IOU with b max, box 4 in this case
다시 말하지만, 하나의 상자에만 b max, 상자 4가 있는 0이 아닌 IOU가 있습니다
Computing the IOU and comparing with the threshold, we eliminate box 4 from list B bar, and add box 2 to the output list D
IOU를 계산하고 임계값과 비교하면 목록 B 표시줄에서 상자 4를 제거하고 출력 목록 D에 상자 2를 추가합니다
We notice that our initial list, B bar, is now empty
우리는 우리의 초기 목록인 B 바가 이제 비어 있다는 것을 알아차렸다
So our non-max suppression algorithm exits and returns the output box list D that contains one bounding box per object as expected
따라서 우리의 비최대 억제 알고리즘은 예상대로 객체당 하나의 경계 상자를 포함하는 출력 상자 목록 D를 종료하고 반환합니다
Congratulations, you have now completed the content required to train and deploy ConvNet based 2D object detectors for self-driving cars
축하합니다, 이제 자율주행 자동차용 ConvNet 기반 2D 물체 탐지기를 훈련하고 배포하는 데 필요한 콘텐츠를 완료했습니다
In this video, we explored how to adjust network output during training to maintain class balance, and to restrict network output during inference to select one output bounding box per object
이 비디오에서는 클래스 균형을 유지하기 위해 훈련 중에 네트워크 출력을 조정하고 추론 중에 네트워크 출력을 제한하여 객체당 하나의 출력 경계 상자를 선택하는 방법을 살펴보았다
In the next lesson, we will discuss how we can use the output of these 2D object detectors for a variety of tasks that are important for self driving cars
다음 수업에서, 우리는 자율주행 자동차에 중요한 다양한 작업에 이러한 2D 물체 감지기의 출력을 어떻게 사용할 수 있는지 논의할 것입니다
Including transforming 2D object detection to 3D, tracking object motion, and applying 2D object detection to traffic sign, and signal detection
2D 물체 감지를 3D로 변환하고, 물체 움직임을 추적하고, 교통 신호에 2D 물체 감지를 적용하고, 신호 감지를 포함합니다
See you there
거기서 보자
[MUSIC]
[음악]
