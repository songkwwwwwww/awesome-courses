Hello again, and welcome to the second week of the course
안녕하세요, 코스의 두 번째 주에 오신 것을 환영합니다
This week, we will be learning about image features, which are distinctive points of interest in the image
이번 주에, 우리는 이미지의 독특한 관심 지점인 이미지 기능에 대해 배울 것입니다
We use image features for several computer vision applications in self-driving cars
우리는 자율주행 자동차의 여러 컴퓨터 비전 애플리케이션에 이미지 기능을 사용합니다
For example, we can use these feature points to localize our car across image frames or to get a global location in a predefined map
예를 들어, 이러한 기능 지점을 사용하여 이미지 프레임에서 자동차를 현지화하거나 미리 정의된 지도에서 글로벌 위치를 얻을 수 있습니다
All of these tasks share a general framework comprising of feature detection, description, and finally matching
이러한 모든 작업은 기능 감지, 설명 및 최종 일치로 구성된 일반적인 프레임워크를 공유합니다
In this video, we will cover the first step of this framework namely feature extraction
이 비디오에서, 우리는 이 프레임워크의 첫 번째 단계, 즉 기능 추출을 다룰 것이다
You will learn what comprises good image features and different algorithms that perform feature extraction
당신은 좋은 이미지 기능과 기능 추출을 수행하는 다양한 알고리즘을 포함하는 것을 배우게 될 것입니다
Let's begin describing this process by taking a real application, image stitching
실제 응용 프로그램, 이미지 스티칭으로 이 과정을 설명하기 시작합시다
We're given two images from two different cameras, and we would like to stitch them together to form a panorama
우리는 두 개의 다른 카메라에서 두 개의 이미지를 받았고, 파노라마를 형성하기 위해 그것들을 함께 꿰매고 싶습니다
First, we need to identify distinctive points in our images
먼저, 우리는 이미지의 독특한 점을 식별해야 한다
We call this point image features
우리는 이 포인트 이미지 기능이라고 부른다
Second, we associate a descriptor for each feature from its neighborhood
둘째, 우리는 이웃의 각 기능에 대한 설명자를 연결합니다
Finally, we use these descriptors to match features across two or more images
마지막으로, 우리는 이 설명자를 사용하여 두 개 이상의 이미지의 기능을 일치시킵니다
For our application here, we can use the matched features in an image stitching algorithm to align the two images and create lovely panorama
여기 애플리케이션의 경우, 이미지 스티치 알고리즘에서 일치하는 기능을 사용하여 두 이미지를 정렬하고 사랑스러운 파노라마를 만들 수 있습니다
Take a look at the details of the stitched panorama
바느질된 파노라마의 세부 사항을 살펴보세요
You can see the two images have been stitched together from some of the artifacts at the edge of the image
이미지 가장자리에 있는 일부 아티팩트에서 두 이미지가 함께 바느질된 것을 볼 수 있습니다
So how do we do it
그래서 우리는 그걸 어떻게 해
Don't worry
걱정하지 마
We'll explain each of the above three steps in detail
위의 세 단계 각각에 대해 자세히 설명하겠습니다
But first, let's begin by defining what an image feature really is
하지만 먼저, 이미지 기능이 실제로 무엇인지 정의하는 것으로 시작합시다
Features are points of interest in an image
특징은 이미지의 관심 지점이다
This definition is pretty vague, as it poses the following question
이 정의는 다음과 같은 질문을 제기하기 때문에 꽤 모호하다
What is considered an interesting point
흥미로운 점은 무엇인가요
Points of interest should be distinctive, and identifiable, and different from its immediate neighborhood
관심 지점은 독특하고, 식별할 수 있어야 하며, 가까운 이웃과 달라야 한다
Features should also be repeatable
특징 또한 반복 가능해야 한다
That means that we should be able to extract the same features from two independent images of the same scene
그것은 우리가 같은 장면의 두 개의 독립적인 이미지에서 동일한 기능을 추출할 수 있어야 한다는 것을 의미한다
Third, features should be local
셋째, 특징은 지역적이어야 한다
That means the features should not change if an image region far away from the immediate neighborhood changes
그것은 이웃에서 멀리 떨어진 이미지 영역이 바뀌면 기능이 바뀌어서는 안 된다는 것을 의미합니다
Forth, our features should be abundant in an image
따라서, 우리의 특징은 이미지에 풍부해야 한다
This is because many applications such as calibration and localization require a minimum number of distinctive points to perform effectively
이는 캘리브레이션 및 현지화와 같은 많은 응용 프로그램이 효과적으로 수행하기 위해 최소 수의 고유 지점이 필요하기 때문입니다
Finally, generating features should not require a large amount of computation, as it is usually used as a pre-processing step for the applications that we've described
마지막으로, 기능을 생성하려면 일반적으로 우리가 설명한 응용 프로그램의 전처리 단계로 사용되기 때문에 많은 양의 계산이 필요하지 않습니다
Take a look at the following images
다음 이미지를 보세요
Can you think of pixels that abide by the above characteristics
위의 특성을 준수하는 픽셀을 생각할 수 있나요
Repetitive texture less patches are very hard to localize
반복적인 텍스처 더 적은 패치는 현지화하기가 매우 어렵다
So these are definitely not feature locations
그래서 이것들은 확실히 특징 위치가 아니다
You can see that the two red rectangles located on the road are almost identical
도로에 위치한 두 개의 빨간색 직사각형이 거의 동일하다는 것을 알 수 있습니다
Patches with large contrast change, where there's a strong gradient, are much easier to localize, but the patches along a certain image edge might still be confusing
그라디언트가 강한 콘트라스트 변경이 있는 패치는 현지화하기가 훨씬 쉽지만, 특정 이미지 가장자리를 따라 패치는 여전히 혼란스러울 수 있습니다
As an example, the two red rectangles on the edge of the same lane marking look very similar
예를 들어, 같은 차선 표시의 가장자리에 있는 두 개의 빨간색 직사각형은 매우 비슷해 보인다
So again, these are challenging locations to use as features
다시 말하지만, 이것들은 기능으로 사용하기 어려운 장소들이다
The easiest concept to localize in images is that of a corner
이미지에서 현지화하는 가장 쉬운 개념은 모서리의 개념이다
A corner occurs when the gradients in at least two significantly different directions are large
모서리는 적어도 두 개의 상당히 다른 방향의 그라디언트가 클 때 발생한다
Examples of corners are shown in the red rectangles
모서리의 예는 빨간색 직사각형에 나와 있다
The most famous corner detector is the Harris Corner Detector, which uses image gradient information to identify pixels that have a strong change in intensity in both x and y directions
가장 유명한 코너 검출기는 이미지 그라데이션 정보를 사용하여 x와 y 방향 모두에서 강도가 크게 변하는 픽셀을 식별하는 해리스 코너 검출기입니다
Many implementations are available online in different programming languages
다양한 프로그래밍 언어로 온라인으로 많은 구현을 사용할 수 있습니다
However, the corners detected by Harris corner detectors are not scale invariant, meaning that the corners can look different depending on the distance the camera is away from the object generating the corner
그러나 해리스 코너 탐지기에 의해 감지된 모서리는 스케일 불변이 아니며, 이는 카메라가 모서리를 생성하는 물체에서 멀리 떨어져 있는 거리에 따라 모서리가 다르게 보일 수 있음을 의미합니다
To remedy this problem, researchers proposed the Harris-Laplace corner detector
이 문제를 해결하기 위해, 연구자들은 해리스-라플라스 코너 탐지기를 제안했다
Harris-Laplace detectors detect corners at different scales and choose the best scale based on the Laplacian of the image
Harris-Laplace 검출기는 다른 스케일에서 모서리를 감지하고 이미지의 Laplacian을 기반으로 최고의 스케일을 선택합니다
Furthermore, researchers have also been able to machine learn corners
게다가, 연구자들은 또한 기계 학습 코너를 할 수 있었다
One prominent algorithm, the fast corner detector, is one of the most used feature detectors due to its very high computational efficiency and solid detection performance
한 가지 눈에 띄는 알고리즘인 빠른 모서리 탐지기는 매우 높은 계산 효율성과 고체 감지 성능으로 인해 가장 많이 사용되는 기능 검출기 중 하나이다
Other scale invariant feature detectors are based on the concept of blobs such as the Laplacian of Gaussian or the difference of Gaussian feature detectors of which there are many variance
다른 스케일 불변 특징 검출기는 가우스의 라플라시아와 같은 물방울 개념이나 많은 차이가 있는 가우스 특징 탐지기의 차이를 기반으로 한다
We will not be discussing these detectors in great depth here, as they represent a complex area of ongoing research, but we can readily use a variety of feature extractors
우리는 진행 중인 연구의 복잡한 영역을 나타내기 때문에 이 탐지기에 대해 깊이 논의하지 않을 것이지만, 다양한 특징 추출기를 쉽게 사용할 수 있습니다
Thanks to robust open source implementations like OpenCV
OpenCV와 같은 강력한 오픈 소스 구현 덕분에
Now let's see some examples of these detectors in action
이제 작동하는 이러한 탐지기의 몇 가지 예를 봅시다
Here you can see corners detected by the Harris Corner Detector
여기서 해리스 코너 탐지기에 의해 감지된 모서리를 볼 수 있습니다
The features primarily capture corners as expected, where strong illumination changes are visible
이 기능은 주로 강한 조명 변화가 보이는 예상대로 모서리를 포착한다
Here you can see Harris-Laplace features on the same image
여기서 같은 이미지에서 Harris-Laplace 기능을 볼 수 있습니다
By using the Laplacian to determine scale, we can detect scale and variant corners that can be more easily matched as a vehicle moves relative to the scene
라플라시안을 사용하여 스케일을 결정함으로써, 우리는 차량이 장면을 기준으로 움직일 때 더 쉽게 일치할 수 있는 스케일과 변형 모서리를 감지할 수 있다
Scale is represented here by the size of the circle around each feature
스케일은 각 기능 주변의 원의 크기로 표시됩니다
The larger the circle, the larger the principal scale of that feature
원이 클수록, 그 특징의 주요 척도가 커진다
In this lesson, you learn what characteristics are required for good image features
이 수업에서는 좋은 이미지 기능에 필요한 특징에 대해 알아봅니다
You also learn the different methods that can be used to extract image features
또한 이미지 기능을 추출하는 데 사용할 수 있는 다양한 방법을 배웁니다
Most of these methods are already implemented in many programming languages including Python and C plus plus, and are ready for you to use whenever needed
이러한 방법의 대부분은 이미 파이썬과 C 플러스 플러스를 포함한 많은 프로그래밍 언어로 구현되었으며, 필요할 때마다 사용할 준비가 되어 있습니다
As a matter of fact, you will be using the OpenCV Python implementation of the Harris-Laplace corner detector for this week's programming assignment
사실, 이번 주 프로그래밍 할당을 위해 Harris-Laplace 코너 탐지기의 OpenCV Python 구현을 사용할 것입니다
In the next video, we will learn about the second step of our feature extraction framework, the feature descriptors
다음 비디오에서, 우리는 기능 추출 프레임워크의 두 번째 단계인 기능 설명자에 대해 배울 것입니다


