[MUSIC] In the last video, we described feature detection or the process of identifying feature points in an image in a variety ways
[음악] 마지막 비디오에서, 우리는 다양한 방법으로 이미지에서 기능 감지 또는 기능 지점을 식별하는 과정을 설명했습니다
However, remember that our end goal is to use match features between two different images for localization, object detection, and other perception tasks that require depth estimation to points in the environment
그러나, 우리의 최종 목표는 지역화, 물체 감지 및 환경의 지점에 깊이 추정이 필요한 기타 인식 작업을 위해 두 개의 다른 이미지 간의 일치 기능을 사용하는 것입니다
To do so, we need to describe features in a way that it allows for feature comparison to determine the best match between frames
그렇게 하려면, 프레임 간의 가장 잘 일치하는 것을 결정하기 위해 기능 비교를 허용하는 방식으로 기능을 설명해야 합니다
We therefore assign a descriptor to every feature point in an image
따라서 이미지의 모든 기능 지점에 설명자를 할당합니다
In this video, you will learn what makes a good feature descriptor for computer vision applications
이 비디오에서는 컴퓨터 비전 애플리케이션을 위한 좋은 기능 설명자를 만드는 것이 무엇인지 배우게 될 것입니다
You'll learn how to derive these descriptors from images so we can use them in autonomous driving
자율주행에 사용할 수 있도록 이미지에서 이러한 설명자를 도출하는 방법을 배우게 될 것입니다
Let's begin by defining what a feature descriptor is
기능 설명자가 무엇인지 정의하는 것으로 시작합시다
Mathematically, we define a feature point by its coordinates u and v in the image frame
수학적으로, 우리는 이미지 프레임에서 좌표 u와 v로 특징점을 정의합니다
We describe a descriptor f as an n dimensional vector associated with each feature
우리는 설명자 f를 각 기능과 관련된 n차원 벡터로 묘사합니다
The descriptor has the task of providing a summary of the image information in the vicinity of the feature itself, and can take on many forms
설명자는 기능 자체 근처에 이미지 정보의 요약을 제공하는 작업을 수행하며, 많은 형태를 취할 수 있습니다
Similar to the design of feature detectors we also have some favorable characteristics required for the design of descriptors to allow for robust feature matching
기능 검출기의 설계와 마찬가지로 우리는 또한 강력한 기능 매칭을 허용하기 위해 설명자의 설계에 필요한 몇 가지 유리한 특성을 가지고 있습니다
As with feature detectors descriptors should be repeatable, that means that regardless of shifts in position, scale, and illumination, the same point of interest in two images should have approximately the same descriptor
기능 검출기와 마찬가지로 설명자는 반복 가능해야 하며, 이는 위치, 규모 및 조명의 변화에 관계없이 두 이미지에 대한 동일한 관심 지점이 거의 동일한 설명자를 가져야 한다는 것을 의미합니다
This invariance in transformations is one of the most researched topics when it comes to descriptor design
이러한 변형의 불변성은 설명자 설계와 관련하여 가장 많이 연구된 주제 중 하나이다
And a large amount of work has been done to provide descriptors that are invariant to scale, illumination, and other variables in image formation
그리고 이미지 형성에서 스케일, 조명 및 기타 변수에 불변하는 설명자를 제공하기 위해 많은 작업이 수행되었다
The second important characteristic of a feature descriptor is distinctiveness
특징 설명자의 두 번째 중요한 특징은 독특함이다
Two nearby features should not have similar descriptors, as this will confuse our feature matching process later on
근처의 두 기능에는 유사한 설명자가 없어야 하며, 이는 나중에 기능 매칭 프로세스를 혼란스럽게 할 것이기 때문입니다
Finally, descriptors should be compact and efficient to compute
마지막으로, 설명자는 컴팩트하고 계산에 효율적이어야 한다
This is because we will usually require matching to be performed in real time for autonomous driving applications
이것은 우리가 보통 자율주행 애플리케이션을 위해 실시간으로 매칭을 수행해야 하기 때문입니다
A wide variety of effective descriptors have been developed for feature matching
기능 매칭을 위해 다양한 효과적인 설명자가 개발되었다
So let's take a look at a specific case study on the design of a single feature descriptors to give you sense for descriptors work
따라서 설명자 작업에 대한 감각을 제공하기 위해 단일 기능 설명자의 설계에 대한 특정 사례 연구를 살펴봅시다
We will describe how to compute the shift features descriptors specifically designed by David Lowe in 1999
우리는 1999년 데이비드 로우가 특별히 설계한 교대 기능 설명자를 계산하는 방법을 설명할 것이다
The procedure for computing shift feature descriptors is as follows
컴퓨팅 시프트 기능 설명자를 위한 절차는 다음과 같습니다
Given a feature in the image, the shift descriptor takes a 16 by 16 window of pixels around it, we call this window the features local neighborhood
이미지의 기능을 감안할 때, 시프트 설명자는 주변에 16 x 16 픽셀 창을 취하며, 우리는 이 창을 지역 이웃의 특징이라고 부릅니다
We then separate this window in to four, 4 by 4 cells such that each cell contains 16 pixels
그런 다음 각 셀에 16픽셀이 포함하도록 이 창을 4개, 4 x 4개의 셀로 분리합니다
Next we compute the edges and edge orientation of each pixel in each cell using the gradient filters we discussed in module one
다음으로 모듈 1에서 논의한 그라디언트 필터를 사용하여 각 셀의 각 픽셀의 가장자리와 가장자리 방향을 계산합니다
For stability of the descriptor, we suppress weak edges using a predefined threshold as they are likely to vary significantly in orientation with small amounts of noise between images
설명자의 안정성을 위해, 우리는 이미지 사이의 소량의 소음으로 방향이 크게 다를 수 있기 때문에 미리 정의된 임계값을 사용하여 약한 가장자리를 억제합니다
Finally, we compute a 32 dimensional histogram of orientations for each cell
마지막으로, 우리는 각 셀에 대한 32차원 방향 히스토그램을 계산합니다
And concatenate the histograms for all four cells to get a final 128 dimensional histogram for the feature at hand, we call this histogram or descriptor
그리고 네 개의 세포 모두에 대한 히스토그램을 연결하여 당면한 기능에 대한 최종 128차원 히스토그램을 얻으면, 우리는 이것을 히스토그램이나 설명자라고 부릅니다
Some additional post processing is done as well in that it helps the 128 dimensional vector retain stable values under variable contrast, game, and other fundametric variations
일부 추가 후처리는 128차원 벡터가 가변 대비, 게임 및 기타 펀다메트릭 변형에서 안정적인 값을 유지하는 데 도움이 된다는 점에서 수행됩니다
SIFT is an example of a very well human engineered feature descriptor, and is used in many state-of-the-art systems
SIFT는 인간 공학 기능 설명자의 예이며, 많은 최첨단 시스템에서 사용된다
It is usually computed over multiple scales and orientations for better scale and rotation invariants
그것은 보통 더 나은 스케일과 회전 불변성을 위해 여러 스케일과 방향으로 계산된다
Finally, when combined with a scale invariant feature detector, such as the difference of Gaussian's detector, it results in a highly robust feature detector and descriptor pair
마지막으로, 가우스 검출기의 차이와 같은 스케일 불변 피처 검출기와 결합하면 매우 강력한 기능 검출기와 설명자 쌍이 발생합니다
It is worth mentioning that there is huge literature out there for feature detectors and descriptors
기능 탐지기와 설명자를 위한 거대한 문헌이 있다는 것은 언급할 가치가 있다
The surf descriptive for example uses similar concepts to SIFT while being significantly faster to compute
예를 들어, 서프 설명은 계산이 훨씬 빠르면서 SIFT와 유사한 개념을 사용합니다
Many other variants exist in the literature including the Gradient Location-Orientation Histogram or GLOH descriptor
그라디언트 위치-오리엔테이션 히스토그램 또는 GLOH 설명자를 포함한 다른 많은 변형이 문헌에 존재한다
The Binary Robust Independent Elementary Features descriptor or BRIEF, and the Oriented Fast and Rotated Brief descriptor or ORB
바이너리 견고한 독립 기본 기능 설명자 또는 BRIEF, 그리고 지향적인 빠르고 회전된 간략한 설명자 또는 ORB
This is a lot of acronyms to remember, but don't worry, we don't expect you to remember all of these
이것은 기억해야 할 많은 약어이지만, 걱정하지 마세요, 우리는 당신이 이 모든 것을 기억할 것으로 기대하지 않습니다
But you may see them in the implementations available for use in Open Source Computer Vision Libraries
하지만 오픈 소스 컴퓨터 비전 라이브러리에서 사용할 수 있는 구현에서 볼 수 있습니다
We've now completed our discussion on feature detectors and descriptors
이제 기능 탐지기 및 설명자에 대한 논의를 완료했습니다
Although most of the discussed algorithms have open source implementations, some like SIFT and SURF are patented and should not be used commercially without approval of the authors
논의된 대부분의 알고리즘에는 오픈 소스 구현이 있지만, SIFT 및 SURF와 같은 일부는 특허를 받았으며 저자의 승인 없이 상업적으로 사용해서는 안 됩니다
Fortunately, the feature detector and descriptor literature up there is vast and some really good algorithms such as ORB match the performance of SIFT and SURF and are free to use even commercially
다행히도, 기능 탐지기와 설명자 문헌은 방대하며 ORB와 같은 정말 좋은 알고리즘은 SIFT와 SURF의 성능과 일치하며 상업적으로도 자유롭게 사용할 수 있습니다
In this lesson, you learned what comprises a feature descriptor, what characteristics are favorable when designing these descriptors
이 수업에서, 당신은 기능 설명자를 구성하는 것, 이러한 설명자를 디자인할 때 어떤 특성이 유리한지 배웠습니다
And different algorithms that are available in the open source libraries to extract feature descriptors as you need them
그리고 오픈 소스 라이브러리에서 필요에 따라 기능 설명자를 추출할 수 있는 다양한 알고리즘
In combination with the feature extractors we talked about in the previous video, you're now ready to take on the challenging tasks of matching features between images using their computed descriptors
이전 비디오에서 이야기한 기능 추출기와 함께, 이제 계산된 설명자를 사용하여 이미지 간에 기능을 일치시키는 어려운 작업을 수행할 준비가 되었습니다
You'll learn more about this in the next video
당신은 다음 비디오에서 이것에 대해 더 배우게 될 것입니다
See you then
그때 보자
[MUSIC]
[음악]
