So far, we have learned how to extract feature positions in the image and how to extract descriptors from the local neighborhood of these features
지금까지, 우리는 이미지의 기능 위치를 추출하는 방법과 이러한 기능의 지역 이웃에서 설명자를 추출하는 방법을 배웠습니다
This video, will teach you about the last step of using features for computer vision applications in autonomous driving feature matching
이 비디오는 자율주행 기능 매칭에서 컴퓨터 비전 애플리케이션에 대한 기능을 사용하는 마지막 단계에 대해 가르쳐 줄 것입니다
Specifically, we will cover how to match features based on distance functions, we will then describe brute force matching as simple but powerful feature matching algorithm
특히, 우리는 거리 함수를 기반으로 기능을 일치시키는 방법을 다룰 것이며, 무차별 대입 매칭을 간단하지만 강력한 기능 매칭 알고리즘으로 설명할 것입니다
But first, let's remind ourselves of how we intend to use features for a variety of perception tasks
하지만 먼저, 다양한 인식 작업에 기능을 어떻게 사용하려고 하는지 상기시켜 봅시다
First, we identify image features, distinctive points in our images
먼저, 우리는 이미지의 특징, 이미지의 독특한 점을 식별합니다
Second, we associate a descriptor for each feature from its neighborhood
둘째, 우리는 이웃의 각 기능에 대한 설명자를 연결합니다
Finally, we use descriptors to match features across two or more images
마지막으로, 우리는 두 개 이상의 이미지의 기능을 일치시키기 위해 설명자를 사용합니다
Afterwards, we can use the matched features for a variety of applications including state estimation, visual odometry, and object detection
그 후, 상태 추정, 시각적 거리 측정 및 물체 감지를 포함한 다양한 응용 분야에 일치하는 기능을 사용할 수 있습니다
It is essential to identify matches correctly however, as these applications are susceptible to catastrophic failures if incorrect matches are provided too frequently
그러나 잘못된 일치가 너무 자주 제공되면 이러한 응용 프로그램은 치명적인 실패에 취약하기 때문에 일치 항목을 올바르게 식별하는 것이 필수적입니다
As a result, feature matching plays a critical role in robust perception methods for self-driving cars
결과적으로, 기능 매칭은 자율주행 자동차를 위한 강력한 인식 방법에 중요한 역할을 한다
Here's an example of a feature matching problem
다음은 기능 매칭 문제의 예입니다
Given a feature and it's descriptor in image one, we want to try to find the best match for the feature in image two
기능과 이미지 1의 설명자를 감안할 때, 우리는 이미지 2의 기능에 가장 적합한 것을 찾고 싶습니다
So how can we solve this problem
그렇다면 우리는 이 문제를 어떻게 해결할 수 있을까요
The simplest solution to the matching problem is referred to as brute force feature matching, and is described as the following
매칭 문제에 대한 가장 간단한 해결책은 무차별 대입 특징 매칭이라고 하며, 다음과 같이 설명된다
First, define a distance function d that compares the descriptors of two features fi and fj, and defines the distance between them
먼저, 두 피처 fi와 fj의 설명자를 비교하고 그들 사이의 거리를 정의하는 거리 함수 d를 정의하십시오
The more similar the two descriptors are to each other, the smaller the distance between them
두 설명자가 서로 더 비슷할수록, 그들 사이의 거리가 작아진다
Second, for every feature fi in image one, we apply the distance function d to compute the distance with every feature fj in image two
둘째, 이미지 1의 모든 기능 fi에 대해 거리 함수 d를 적용하여 이미지 2의 모든 기능 fj로 거리를 계산합니다
Finally, we will return the feature which we'll call fc from image two with the minimum distance to the feature fi in image one as our match
마지막으로, 우리는 이미지 1의 기능 fi까지의 최소 거리를 가진 이미지 2에서 fc를 호출할 기능을 일치로 반환할 것입니다
This feature is known as the nearest neighbor, and it is the closest feature to the original one in the descriptor space
이 기능은 가장 가까운 이웃으로 알려져 있으며, 설명자 공간에서 원본과 가장 가까운 기능이다
The most common distance function used to compare descriptors is the sum of squared distances or SSD
설명자를 비교하는 데 사용되는 가장 일반적인 거리 기능은 제곱 거리 또는 SSD의 합이다
Which penalizes variations between two descriptors quadratically making it sensitive to large variations in the descriptor, but insensitive to smaller ones
두 설명자 간의 변화를 이차적으로 처벌하여 설명자의 큰 변형에 민감하지만 더 작은 변형에는 민감하지 않습니다
Other distance functions such as the sum of absolute differences or the Hamming distance are also viable alternatives
절대 차이의 합이나 해밍 거리와 같은 다른 거리 기능도 실행 가능한 대안이다
The sum of absolute difference penalizes all variations equally while the Hamming distance is used for binary features, for which all descriptor elements are binary values
절대 차이의 합은 모든 변형을 동등하게 처벌하는 반면 해밍 거리는 모든 설명자 요소가 이진 값인 이진 기능에 사용된다
We will be using the SSD distance function for our examples to follow
우리는 우리의 예를 따르기 위해 SSD 거리 기능을 사용할 것이다
Our matching technique and distance choices are really quite simple
우리의 매칭 기술과 거리 선택은 정말 간단하다
But what do you think might go wrong with our proposed nearest neighbor matching technique
하지만 우리가 제안한 가장 가까운 이웃 매칭 기술에 무엇이 잘못될 수 있다고 생각하나요
Let's look at our first case and see how our brute force matcher works in practice
우리의 첫 번째 사례를 살펴보고 우리의 무차별 대입 matcher가 실제로 어떻게 작동하는지 봅시다
Consider the feature inside the yellow bounding box
노란색 경계 상자 안의 특징을 고려해 보세요
For simplicity, this feature has a four-dimensional descriptor, which we'll call f1
단순함을 위해, 이 기능에는 f1이라고 부를 4차원 설명자가 있습니다
Let's compute the distance between f1 and the first feature in the image two, which we'll label f2
F1과 f2에 라벨을 붙일 이미지 2의 첫 번째 기능 사이의 거리를 계산해 봅시다
We get a sum of squared difference or SSD value of nine
우리는 제곱 차이 또는 SSD 값의 합계 9를 얻습니다
We then compute the distance between f1 and the second feature in image two, which we'll label f3
그런 다음 이미지 2의 f1과 두 번째 기능 사이의 거리를 계산하여 f3에 라벨을 붙일 것입니다
Here, we get an SSD of 652
여기서, 우리는 652의 SSD를 얻는다
We can now repeat this process for every other feature in the second image and find out that all the other distances are similarly large relative to the first one
이제 두 번째 이미지의 다른 모든 기능에 대해 이 과정을 반복하고 다른 모든 거리가 첫 번째 거리에 비해 비슷하게 크다는 것을 알 수 있습니다
We therefore choose feature f2 to be our match as it has the lowest distance to f1
따라서 우리는 f1까지의 거리가 가장 낮기 때문에 기능 f2를 우리의 일치로 선택합니다
Visually, our brute force approach appears to be working
시각적으로, 우리의 무차별 대입 접근 방식은 효과가 있는 것으로 보인다
As humans, we can immediately see that feature f1 in the image is indeed the same point of interest as feature f2 in image two
인간으로서, 우리는 이미지의 기능 f1이 실제로 이미지 2의 피처 f2와 같은 관심 지점이라는 것을 즉시 알 수 있다
Now, let us consider a second case where our feature detector tries to match a feature from image one, for which there is no corresponding feature in image two
이제 기능 탐지기가 이미지 1의 기능과 일치하려고 시도하는 두 번째 경우를 고려하여 이미지 2에 해당 기능이 없습니다
Let's take a look at what the brute force approach will do when our feature detector encounters this situation
우리의 기능 탐지기가 이 상황에 직면했을 때 무차별 대입 접근 방식이 무엇을 할 것인지 살펴봅시다
Following the same procedure as before, we compute the SSD between the descriptors of a feature f1 in image one, and all the features in image two
이전과 같은 절차에 따라, 우리는 이미지 1의 기능 f1의 설명자와 이미지 2의 모든 기능 사이에서 SSD를 계산합니다
Assume that f2 and f3 are the nearest neighbors of f1 and with f2 having the lowest score
F2와 f3이 f1의 가장 가까운 이웃이고 f2가 가장 낮은 점수를 가지고 있다고 가정하십시오
Although at 441, it is still rather dissimilar to the f1 feature descriptor from the original image
441이지만, 여전히 원본 이미지의 f1 기능 설명자와 다소 다르다
As a result, f2 will be returned as our best match
결과적으로, f2는 우리의 최고의 경기로 반환될 것이다
Clearly, this is not correct
분명히, 이것은 옳지 않다
Because feature f1 is not the same point of interest as feature f2 in the scene
기능 f1은 장면의 기능 f2와 같은 관심 지점이 아니기 때문이다
So how can we solve this problem
그렇다면 우리는 이 문제를 어떻게 해결할 수 있을까요
We can solve this problem by setting a distance threshold Delta on the acceptance of matches
우리는 경기 수락에 대한 거리 임계값 델타를 설정하여 이 문제를 해결할 수 있다
This means that any feature in image two with a distance greater than Delta to f1, is not considered a match even if it has the minimum distance to f1 among all the features in image two
이것은 델타에서 f1까지의 거리가 큰 이미지 2의 모든 기능이 이미지 2의 모든 기능 중에서 f1까지의 최소 거리가 있더라도 일치하는 것으로 간주되지 않는다는 것을 의미합니다
Now, let's update our brute force matcher algorithm with our threshold
이제 무차별 대입 매칭 알고리즘을 임계값으로 업데이트합시다
We usually define Delta empirically, as it depends on the application at hand and the descriptor we are using
우리는 보통 당면한 응용 프로그램과 우리가 사용하고 있는 설명자에 따라 델타를 경험적으로 정의합니다
Once again, we define our distance function to quantify the similarity of two feature descriptors
다시 한번, 우리는 두 기능 설명자의 유사성을 정량화하기 위해 거리 함수를 정의합니다
We also fix a maximum distance threshold Delta for acceptable matches
우리는 또한 허용 가능한 경기를 위해 최대 거리 임계값 델타를 수정합니다
Then, for every feature in image one, we compute the distance to each feature in image two and store the shortest distance or nearest neighbor as the most likely match
그런 다음 이미지 1의 모든 기능에 대해 이미지 2의 각 기능까지의 거리를 계산하고 가장 짧은 거리 또는 가장 가까운 이웃을 가장 가능성이 높은 것으로 저장합니다
Brute force matching is suitable when the number of features we want to match is reasonable, but has quadratic computational complexity making it ill-suited as the number of features increases
무차별 대입 매칭은 우리가 일치시키고자 하는 기능의 수가 합리적이지만 이차 계산 복잡성이 있어 기능의 수가 증가함에 따라 부적합할 때 적합합니다
For large sets of features, special data structures such as k-d trees are used to enhance computation time
대규모 기능 세트의 경우, k-d 트리와 같은 특수 데이터 구조는 계산 시간을 향상시키는 데 사용됩니다
Both brute force and k-d tree-based matchers are implemented as part of OpenCV, making them easy for you to try out
무차별 대입과 k-d 트리 기반 매처는 모두 OpenCV의 일부로 구현되어 쉽게 사용해 볼 수 있습니다
Just follow the links shown at the bottom of this slide
이 슬라이드 하단에 표시된 링크를 따라가세요
As a reminder, you can download these lecture slides for your review
다시 말씀드리지만, 검토를 위해 이 강의 슬라이드를 다운로드할 수 있습니다
By now, you should have a much better understanding of feature detection, description, and matching
지금까지는 기능 감지, 설명 및 매칭에 대해 훨씬 더 잘 이해해야 합니다
These three steps are required to use features for various self-driving applications, such as visual odometry and object detection
이 세 단계는 시각적 거리 측정 및 물체 감지와 같은 다양한 자율주행 애플리케이션에 기능을 사용하는 데 필요합니다
Our brute force matcher is pretty deep, but still far from perfect
우리의 무차별 대입 matcher는 꽤 깊지만, 여전히 완벽과는 거리가 멀다
We really need precise results to create safe and reliable self-driving car perception
우리는 안전하고 신뢰할 수 있는 자율주행 자동차 인식을 만들기 위해 정확한 결과가 정말로 필요하다
So in the next lesson, we will learn how to improve our brute force matcher to accommodate some of the troublesome and ambiguous matches that frequently lead to incorrect results
그래서 다음 수업에서, 우리는 종종 잘못된 결과로 이어지는 번거롭고 모호한 경기를 수용하기 위해 무차별 대입 matcher를 개선하는 방법을 배울 것입니다
See you in the next video
다음 비디오에서 보자


