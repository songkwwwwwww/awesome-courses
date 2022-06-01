So far we have described the three steps we need to use image features for autonomous vehicle applications
지금까지 우리는 자율주행 차량 애플리케이션을 위해 이미지 기능을 사용하는 데 필요한 세 단계를 설명했습니다
We also mentioned that feature matchers are not very robust to outliers
우리는 또한 기능 매칭이 이상값에 그다지 강력하지 않다고 언급했다
In this lesson, we will describe what outliers are and how they might affect our usage of image features to solve real-world problems
이 수업에서는 이상값이 무엇이며 실제 문제를 해결하기 위해 이미지 기능 사용에 어떤 영향을 미칠 수 있는지 설명할 것입니다
We will also provide a powerful method to handle outliers called random sample consensus, or RANSAC for short
우리는 또한 무작위 샘플 합의 또는 줄여서 RANSAC이라는 이상값을 처리하는 강력한 방법을 제공할 것입니다
This method will help us account for and eliminate outliers, as they can have a strong negative impact on the use of features in other perception tasks
이 방법은 다른 인식 작업에서 기능 사용에 강한 부정적인 영향을 미칠 수 있으므로 이상값을 파악하고 제거하는 데 도움이 될 것입니다
But first, let us introduce the use of the three-step feature extraction framework for the real-world problem of vehicle localization
하지만 먼저, 차량 현지화의 실제 문제를 위한 3단계 기능 추출 프레임워크의 사용을 소개하겠습니다
Our localization problem is defined as follows: given any two images of the same scene from different perspectives, find the translation T, between the coordinate system of the first image shown in red, and the coordinate system of the second image shown in green
우리의 현지화 문제는 다음과 같이 정의됩니다: 다른 관점에서 같은 장면의 두 이미지를 감안할 때, 빨간색으로 표시된 첫 번째 이미지의 좌표계와 녹색으로 표시된 두 번째 이미지의 좌표계 사이의 번역 T를 찾으십시오
In practice, we'd also want to solve for the scale and skew due to different viewpoints
실제로, 우리는 또한 다른 관점으로 인해 규모와 왜곡을 해결하고 싶다
But we'll keep this example simple to stay focused on the current topic
하지만 우리는 이 예시를 현재 주제에 집중하기 위해 간단하게 유지할 것이다
To solve this localization problem, we need to perform the following steps
이 현지화 문제를 해결하려면 다음 단계를 수행해야 합니다
First, we need to find the displacement of image one on the u image axis of image two
먼저, 이미지 2의 u 이미지 축에서 이미지 1의 변위를 찾아야 합니다
We call this displacement t sub u
우리는 이 변위 t sub u라고 부른다
Second, we need to find the displacement of image one on the v axis of image two, and we'll call this displacement t sub v
둘째, 우리는 이미지 2의 v축에서 이미지 1의 변위를 찾아야 하며, 이 변위 t sub v라고 부를 것이다
We will find t sub u and t sub v by matching features between the images, and then solving for the displacements that best align these matched features
이미지 간의 기능을 일치시킨 다음 이러한 일치하는 기능을 가장 잘 정렬하는 변위에 대해 해결하여 t sub u와 t sub v를 찾을 것입니다
We begin by computing features and their descriptors in image one and image two
우리는 이미지 1과 이미지 2의 기능과 설명자를 계산하는 것으로 시작합니다
We then match these features using the brute force matcher we developed in the previous lesson
그런 다음 이전 수업에서 개발한 무차별 대입 matcher를 사용하여 이러한 기능을 일치시킵니다
Do you notice anything a little off in the results from our brute force match
우리의 무차별 대입 경기 결과에서 조금 벗어난 것이 있나요
Don't worry
걱정하지 마
We will come back to these results in a little bit
우리는 조금 있다가 이 결과로 돌아올 것이다
But first, let's define the solution of our problem mathematically in terms of our matched features
하지만 먼저, 일치하는 특징의 관점에서 문제의 해결책을 수학적으로 정의해 봅시다
We denote a feature pair from images one and two, as f1 sub i and f2 sub i
우리는 이미지 1과 2의 기능 쌍을 f1 서브 i와 f2 서브 i로 나타냅니다
Where i ranges between zero and n, the total number of feature pairs returned by our matching algorithm
여기서 i는 0에서 n 사이이며, 일치하는 알고리즘에 의해 반환되는 총 기능 쌍 수입니다
Each feature in the feature pair is represented by its pixel coordinates ui and vi
기능 쌍의 각 기능은 픽셀 좌표 UI와 vi로 표시됩니다
Note that every pixel in the image ones should coincide with its corresponding pixel in image two after application of the translation t sub q and t sub v
이미지의 모든 픽셀은 번역 t sub q와 t sub v를 적용한 후 이미지 2의 해당 픽셀과 일치해야 합니다
We can then use our feature pairs to model the translation as follows: the location of a feature in image one is translated to a corresponding location in image two through model parameters t sub u and t sub v
그런 다음 기능 쌍을 사용하여 다음과 같이 번역을 모델링할 수 있습니다: 이미지 1의 피처의 위치는 모델 매개 변수 t sub u 및 t sub v를 통해 이미지 2의 해당 위치로 변환됩니다
Here the translations on the u image axis t sub u, and the v image axis t sub v, are the same for all feature pairs
여기서 u 이미지 축 t sub u와 v 이미지 축 t sub v의 번역은 모든 기능 쌍에 대해 동일합니다
Since we assume a rigid body motion
우리가 딱딱한 신체 움직임을 가정하기 때문에
Now we can solve for t sub u and t sub v using least squares estimation
이제 최소 제곱 추정치를 사용하여 t sub u와 t sub v를 해결할 수 있습니다
The solution to the least squares problem will be the values for t sub u and t sub v that minimize the sum of squared errors between all pairs of pixels
최소 제곱 문제에 대한 해결책은 모든 픽셀 쌍 사이의 제곱 오류의 합을 최소화하는 t sub u와 t sub v의 값일 것이다
Now that we have our localization problem defined, let's return to the results of our feature matching
이제 현지화 문제가 정의되었으므로, 기능 일치의 결과로 돌아가 봅시다
By observing the feature locations visually, it can be seen that the feature pair in the purple circles is actually an incorrect match
기능 위치를 시각적으로 관찰함으로써, 보라색 원의 기능 쌍이 실제로 잘못 일치하는 것을 알 수 있습니다
This happens even though we use the distance ratio method, and is a common occurrence in feature matching
이것은 우리가 거리 비율 방법을 사용하더라도 발생하며, 기능 매칭에서 흔한 발생이다
We call such feature pairs outliers
우리는 그러한 기능 쌍을 이상값이라고 부른다
Outliers can comprise a large portion of our feature set, and typically have an out-sized negative effect on our model solution, especially when using least squares estimation
이상값은 기능 세트의 상당 부분을 포함할 수 있으며, 일반적으로 특히 최소 제곱 추정치를 사용할 때 모델 솔루션에 큰 부정적인 영향을 미칩니다
Let us see if we can identify these outliers and avoid using them in our least squares solution
이러한 이상값을 식별하고 최소 제곱 솔루션에서 사용하지 않도록 할 수 있는지 봅시다
Outliers can be handled using a model-based outlier rejection method called Random Sample Consensus, or RANSAC for short
이상값은 무작위 샘플 합의 또는 줄여서 RANSAC라는 모델 기반 이상치 거부 방법을 사용하여 처리할 수 있습니다
RANSAC developed by Martin Fischler and Robert Bolles in 1981 is one of the most used model-based methods for outlier rejection in robotics
1981년 Martin Fischler와 Robert Bolles가 개발한 RANSAC은 로봇 공학에서 이상치 거부에 가장 많이 사용되는 모델 기반 방법 중 하나이다
The RANSAC algorithm proceeds as follows: first, given a model for identifying a problem solution from a set of data points, find the smallest number M of data points or samples needed to compute the parameters of this model
RANSAC 알고리즘은 다음과 같이 진행됩니다: 첫째, 데이터 포인트 집합에서 문제 해결책을 식별하기 위한 모델을 감안할 때, 이 모델의 매개 변수를 계산하는 데 필요한 가장 작은 수의 M의 데이터 포인트 또는 샘플을 찾으십시오
In our case, the problem localization and the model parameters, are the t sub u and t sub v offsets of the least square solution
우리의 경우, 문제 현지화와 모델 매개 변수는 최소 제곱 솔루션의 t sub u 및 t sub v 오프셋입니다
Second, randomly select M samples from your data
둘째, 데이터에서 M 샘플을 무작위로 선택하세요
Third, compute the model parameters using only the M samples selected from your data set
셋째, 데이터 세트에서 선택한 M 샘플만 사용하여 모델 매개 변수를 계산하십시오
Forth, use the computed parameters and count how many of the remaining data points agree with this computed solution
앞으로, 계산된 매개 변수를 사용하고 나머지 데이터 포인트 중 몇 개가 이 계산된 솔루션에 동의하는지 계산하십시오
The accepted points are retained and referred to as inliers
허용된 포인트는 유지되고 이상값이라고 불린다
Fifth, if the number of inliers C is satisfactory, or if the algorithm has iterated a pre-set maximum number of iterations, terminate and return the computed solution and the inlier set
다섯째, inliers C의 수가 만족스럽거나 알고리즘이 미리 설정된 최대 반복 수를 반복한 경우, 계산된 솔루션과 inlier 세트를 종료하고 반환합니다
Else, go back to step two and repeat
그렇지 않으면, 2단계로 돌아가서 반복하세요
Finally, recompute and return the model parameters from the best inlier set
마지막으로, 최고의 inlier 세트에서 모델 매개 변수를 재컴퓨팅하고 반환하십시오
The one with the largest number of features
특징이 가장 많은 것
Now we can revisit our localization problem and try to accommodate for the outliers from our feature matcher
이제 현지화 문제를 다시 검토하고 기능 매처의 이상값을 수용하려고 노력할 수 있습니다
As a reminder, our model parameters t sub u and t sub v, shift each feature pair equally from the first image to the second
다시 말씀드리지만, 우리의 모델 매개 변수 t sub u와 t sub v는 각 기능 쌍을 첫 번째 이미지에서 두 번째 이미지로 동등하게 이동합니다
To estimate t sub u and t sub v, we need one pair of features
T sub u와 t sub v를 추정하려면 한 쌍의 기능이 필요합니다
Now, let us go through the RANSAC algorithm for this problem
이제, 이 문제에 대한 RANSAC 알고리즘을 살펴보자
First, we randomly select one feature pair from the matched samples
먼저, 일치하는 샘플에서 하나의 기능 쌍을 무작위로 선택합니다
Now, we need to estimate our model using the computed feature pair
이제, 우리는 계산된 기능 쌍을 사용하여 모델을 추정해야 합니다
Using the feature pair, we compute the displacement along the u image axis, t sub u, and the displacement along the v image axis, t sub v
기능 쌍을 사용하여 u 이미지 축, t sub u 및 v 이미지 축을 따라 변위를 계산합니다
We now need to check if our model is valid by computing the number of inliers
이제 inliers 수를 계산하여 모델이 유효한지 확인해야 합니다
Here, we use a tolerance to determine the inliers, since it is highly unlikely that we satisfy the model with a 100 percent precision
여기서, 우리는 100% 정밀도로 모델을 만족시킬 가능성은 거의 없기 때문에 인라이어를 결정하기 위해 공차를 사용합니다
Unfortunately, our first iteration chose a poor feature match to compute the model parameters
불행하게도, 우리의 첫 번째 반복은 모델 매개 변수를 계산하기 위해 열악한 기능 일치를 선택했다
When using this model to compute how many features in image one translate to their matched location in image two, we notice that none of them do
이 모델을 사용하여 이미지 1의 얼마나 많은 기능이 이미지 2의 일치하는 위치로 변환되는지 계산할 때, 우리는 그들 중 누구도 그렇지 않다는 것을 알 수 있습니다
Since our number of inliers is zero, we go back and choose another feature pair at random, and restart the RANSAC process
우리의 이상값 수는 0이기 때문에, 우리는 돌아가서 무작위로 다른 기능 쌍을 선택하고 RANSAC 프로세스를 다시 시작합니다
Once again, we compute t sub u and t sub v, using a new randomly sampled feature pair to get our new model parameters
다시 한번, 우리는 새로운 모델 매개 변수를 얻기 위해 무작위로 샘플링된 새로운 기능 쌍을 사용하여 t sub u와 t sub v를 계산합니다
Using the model, we compute how many features and image one translate to their match in image two
모델을 사용하여, 우리는 이미지 2에서 얼마나 많은 기능과 이미지가 일치하는지 계산합니다
This time we can see that most of the features actually fit this model
이번에는 대부분의 기능이 실제로 이 모델에 맞는다는 것을 알 수 있습니다
In fact 11 out of 12 features are considered in inliers
사실 12개의 기능 중 11개는 이상값으로 간주됩니다
Since most of our features are inliers, we're satisfied with this model, and we can stop the RANSAC algorithm
대부분의 기능은 이상값이기 때문에, 우리는 이 모델에 만족하며, RANSAC 알고리즘을 중지할 수 있습니다
At this point you should now understand the proper use of image features for an autonomous vehicle applications
이 시점에서 당신은 이제 자율주행 차량 애플리케이션을 위한 이미지 기능의 적절한 사용을 이해해야 합니다
You've learned what outliers are within the scope of feature matching, and how to handle outliers through the RANSAC algorithm
기능 매칭 범위 내에서 이상값이 무엇인지, 그리고 RANSAC 알고리즘을 통해 이상값을 처리하는 방법을 배웠습니다
Outlier removal is a key process in improving robustness when using feature matching, and greatly improves the quality of localization results
이상치 제거는 기능 매칭을 사용할 때 견고성을 향상시키는 핵심 과정이며, 현지화 결과의 품질을 크게 향상시킵니다
In the next video, we will use what we learned so far to estimate the position of our autonomous vehicle using camera image features
다음 비디오에서, 우리는 지금까지 배운 것을 사용하여 카메라 이미지 기능을 사용하여 자율주행 차량의 위치를 추정할 것입니다
This will help us track our own vehicles motion through the environment
이것은 우리가 환경을 통해 우리 자신의 차량의 움직임을 추적하는 데 도움이 될 것이다
Which is a process known as Visual Odometry, and is essential to navigating smoothly and safely
시각 거리 측정으로 알려진 과정이며, 매끄럽고 안전하게 탐색하는 데 필수적이다


