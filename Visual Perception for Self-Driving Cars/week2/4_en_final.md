So, far this week we've learned how to detect features, compute their descriptors, and perform brute force matching using distance functions
그래서, 이번 주까지 우리는 기능을 감지하고, 설명자를 계산하고, 거리 함수를 사용하여 무차별 대입 매칭을 수행하는 방법을 배웠습니다
We're almost ready to start applying feature detection, description, and matching to self-driving car perception
우리는 자율주행 자동차 인식에 기능 감지, 설명 및 매칭을 적용할 준비가 거의 되어 있습니다
In this video, we will explore the issue of ambiguous matches and how to make our matches more robust to matching errors caused by similar feature descriptors through the distance ratio formulation
이 비디오에서, 우리는 모호한 경기 문제와 거리 비율 제형을 통해 유사한 기능 설명자로 인한 매칭 오류에 대한 경기를 더 강력하게 만드는 방법을 탐구할 것입니다
But first, let's review the two feature matching cases we discussed in the last lesson
하지만 먼저, 지난 수업에서 논의한 두 가지 기능 매칭 사례를 검토해 봅시다
In the first case, we have a useful feature descriptor that clearly gives a small distance to the feature f2 and a large distance to other features in the second image
첫 번째 경우, 우리는 기능 f2에 대한 작은 거리와 두 번째 이미지의 다른 기능과의 큰 거리를 명확하게 제공하는 유용한 기능 설명자를 가지고 있습니다
In this case we can successfully identify the correct match to the feature f1 and image one
이 경우 f1 및 이미지 1 기능과 올바른 일치 항목을 성공적으로 식별할 수 있습니다
Our brute force matching algorithm works well with this descriptor and as seamlessly capable of finding the right match in image two
우리의 무차별 대입 매칭 알고리즘은 이 설명자와 잘 작동하며 이미지 2에서 올바른 일치를 원활하게 찾을 수 있습니다
In the second case, the feature f1 in image one does not have a match at all in image two
두 번째 경우, 이미지 1의 기능 f1은 이미지 2에서 전혀 일치하지 않습니다
We modified our brute force matching algorithm with a threshold delta to eliminate incorrect matches in this case
우리는 이 경우 잘못된 일치를 제거하기 위해 무차별 대입 매칭 알고리즘을 임계값 델타로 수정했습니다
Since both features and image two have a distance greater than the distance threshold Delta, the brute force matcher rejects both the features f2 and f3 as potential matches and no match is returned
피처와 이미지 2 모두 거리 임계값 델타보다 큰 거리를 가지고 있기 때문에, 무차별 대입 매처는 f2와 f3 기능을 모두 잠재적인 일치로 거부하고 일치가 반환되지 않습니다
But, let us consider a third case, once again we are trying to match feature f1 in image one to a corresponding feature in image two
하지만, 세 번째 사례를 고려해 봅시다, 다시 한번 우리는 이미지 1의 기능 f1을 이미지 2의 해당 기능과 일치시키려고 노력하고 있습니다
With the feature vectors presented here, feature f1 gets an SSD value of nine with feature two in image two
여기에 제시된 기능 벡터를 사용하면, 기능 f1은 이미지 2의 기능 2로 9의 SSD 값을 얻습니다
We test another feature f3, and we also get an SSD of nine
우리는 또 다른 기능 f3를 테스트하고, 또한 9개의 SSD를 얻습니다
Both of these features have an SSD less than Delta which was 20 in this case, and as such are valid matches
이 두 기능 모두 이 경우 델타보다 작은 SSD를 가지고 있으며, 따라서 유효한 일치입니다
So what should we do
그래서 우리는 무엇을 해야 할까요
We refer to feature fi in case three as a feature with ambiguous matches
우리는 3의 경우 기능 fi를 모호한 일치가 있는 기능으로 언급합니다
An elegant solution to this problem was proposed by David Lowe in 1999
이 문제에 대한 우아한 해결책은 1999년 데이비드 로우에 의해 제안되었다
The solution goes as follows
해결책은 다음과 같다
First, we compute the distance between feature fi in image one and all the features fj in image two, similar to our previous algorithm, we choose the feature fc in image two with the minimum distance to feature fi in image of one as our closest match
첫째, 우리는 이전 알고리즘과 마찬가지로 이미지 1의 기능 fi와 이미지 2의 모든 기능 fj 사이의 거리를 계산하며, 가장 가까운 일치로 이미지에서 fi를 특징으로 하는 최소 거리를 가진 이미지 2의 기능 fc를 선택합니다
We then proceed to get feature fs the feature in image two with the second closest distance to the feature fi
그런 다음 기능 fi에 두 번째로 가까운 거리에 있는 이미지 2의 기능을 얻습니다
Finally, we find how much nearer our closest match fc is over our second closest match fs
마지막으로, 우리는 두 번째로 가까운 경기 fs보다 가장 가까운 경기 fc가 얼마나 가까운지 찾습니다
This can be done through the distance ratio
이것은 거리 비율을 통해 이루어질 수 있다
The distance ratio can be defined as the distance computed between feature fi in image one and fc the closest match in image two
거리 비율은 이미지 1의 피처 fi와 이미지 2에서 가장 가까운 fc 사이의 거리로 정의될 수 있다
Over the distance computed between feature fi and fs, the second closest match in image two
피처 fi와 fs 사이에서 계산된 거리에서, 이미지 2에서 두 번째로 가까운 일치
If the distance ratio is close to one, it means that according to our descriptor and distance function, fi matches both fs and fc
거리 비율이 하나에 가깝다면, 설명자와 거리 함수에 따라 fi가 fs와 fc와 일치한다는 것을 의미합니다
In this case, we don't want to use this match in our processing later on, as it clearly is not known to our matcher which location in image two corresponds to the feature in image one
이 경우, 이미지 2의 어느 위치가 이미지 1의 기능에 해당하는지 명확하게 알려져 있지 않기 때문에 나중에 프로세싱에 이 일치를 사용하고 싶지 않습니다
Let us update our brute force matcher algorithm with the distance ratio formulation
무차별 대입 매처 알고리즘을 거리 비율 제형으로 업데이트합시다
The updates replace the distance with the ratio of distance as our metric to keep matches
업데이트는 경기를 유지하기 위한 미터법으로 거리를 거리 비율로 대체합니다
We usually set the distance ratio threshold which we'll refer to as row somewhere around 0
우리는 보통 약 0
5, which means that we require our best match to be at least twice as close as our second best match to our initial features descriptor
5에서 행이라고 부를 거리 비율 임계값을 설정했는데, 이는 우리가 초기 기능 설명자와 두 번째로 잘 일치하는 것보다 적어도 두 배나 가까울 것을 의미합니다
Revisiting case three, we can see that using the distance ratio and a corresponding threshold row set to 0
사례 3을 다시 보면, 우리는 거리 비율과 0
5, we discard our ambiguous matches and retain the good ones
5로 설정된 해당 임계값 행을 사용하여 모호한 경기를 버리고 좋은 경기를 유지한다는 것을 알 수 있습니다
In this video, you've learned what ambiguous matches are, and how to handle these ambiguous matches through the distance ratio formulation
이 비디오에서, 당신은 모호한 경기가 무엇인지, 그리고 거리 비율 제형을 통해 이러한 모호한 일치를 처리하는 방법을 배웠습니다
Unfortunately, even with the distance ratio formulation, as much as 50 percent of typical matches can still be wrong when using modern descriptors
불행하게도, 거리 비율 공식에도 불구하고, 현대 설명자를 사용할 때 일반적인 일치의 50%가 여전히 틀릴 수 있다
This is because, repetitive patterns in images and small variations in pixel values, are often sufficient to confuse the matching process
이미지의 반복적인 패턴과 픽셀 값의 작은 변화는 종종 매칭 프로세스를 혼란스럽게 하기에 충분하기 때문이다
We call these erroneous matches outliers
우리는 이러한 잘못된 경기를 이상값이라고 부른다
For our next lesson, I will describe a method to account for and eliminate outliers before using are matched features for further perception tasks
다음 수업을 위해, 추가 인식 작업에 일치하는 기능을 사용하기 전에 이상값을 설명하고 제거하는 방법을 설명하겠습니다


