In the last video, you were introduced to the final course assessment in which you will have to develop three major aspects of the procession stack of a self-driving car
마지막 비디오에서, 당신은 자율주행 자동차의 행렬 스택의 세 가지 주요 측면을 개발해야 하는 최종 코스 평가를 소개받었습니다
This lesson, we will expose you to some algorithmic concepts that will be useful to finish this assessment
이 수업에서, 우리는 이 평가를 완료하는 데 유용한 몇 가지 알고리즘 개념에 당신을 노출시킬 것입니다
The first thing to be aware of while attempting the assignment, is the coordinate frames you are working in
과제를 시도하는 동안 가장 먼저 알아야 할 것은 작업 중인 좌표 프레임입니다
All the required 3D estimation will be performed in the camera coordinate frame
필요한 모든 3D 추정은 카메라 좌표 프레임에서 수행될 것이다
That includes the ground plane, distance to impact, and other 3D quantities
여기에는 지상 평면, 충격까지의 거리 및 기타 3D 수량이 포함됩니다
However, the camera as a sensor is usually oriented with its y-axis pointing downward
그러나, 센서로서의 카메라는 보통 y축이 아래쪽을 가리키는 방향으로 향한다
What does that mean for you while working on the assessment
평가를 진행하는 동안 그것이 당신에게 어떤 의미인가요
The only thing you will need to be careful about, is the sign of the height value of pixels
조심해야 할 유일한 것은 픽셀의 높이 값의 표시입니다
Points higher than the camera will have a negative height, while points lower than the camera will have a positive height
카메라보다 높은 점은 음의 높이를 가진 반면, 카메라보다 낮은 점은 긍정적인 높이를 가질 것이다
The second topic you should be aware of, is how to solve linear least squares problems for plane estimation in Python
당신이 알아야 할 두 번째 주제는 파이썬에서 평면 추정을 위한 선형 최소 제곱 문제를 해결하는 방법입니다
For this part of the assessment, you will have a couple of alternatives
평가의 이 부분에 대해, 당신은 몇 가지 대안이 있을 것입니다
We provide you with a function that does the plane estimation for you using singular value decomposition or SVD for short
우리는 단수 값 분해 또는 짧은 SVD를 사용하여 평면 추정을 수행하는 함수를 제공합니다
However, if you want to challenge, you could try solving the plane estimation problem yourself by solving the least squares problem using the NumPy native function lstsq
그러나, 도전하고 싶다면, NumPy 네이티브 함수 lstsq를 사용하여 최소 제곱 문제를 해결하여 평면 추정 문제를 직접 해결할 수 있습니다
If you choose this path, be careful to choose more than three points for each iteration of RANSAC, as the solver might not provide any useful results in certain edge cases where the system is poorly conditioned
이 경로를 선택하는 경우, 시스템이 제대로 조절되지 않은 특정 에지 케이스에서 솔버가 유용한 결과를 제공하지 않을 수 있으므로 RANSAC의 각 반복에 대해 3개 이상의 점을 선택하십시오
A greater challenge would be to implement SVD plane fitting from scratch
더 큰 과제는 처음부터 SVD 평면 피팅을 구현하는 것이다
SVD almost always provides a numerically stable solution
SVD는 거의 항상 수치적으로 안정적인 해결책을 제공한다
In addition, it can be faster than the NumPy lstsq function
게다가, 그것은 NumPy lstsq 함수보다 빠를 수 있다
It's up to you which path to take to estimate the plane
비행기를 추정하기 위해 어떤 경로를 택해야 하는지는 당신에게 달려 있습니다
As long as the plane is correct, the method that generated it will be given full marks
평면이 정확한 한, 그것을 생성한 방법은 완전한 표시가 주어질 것이다
The second perception task that needs to be performed, is lane boundary detection
수행해야 할 두 번째 인식 작업은 차선 경계 감지이다
The output of the Hough transform line detection, is any line belonging to the boundary of the lane including horizontal ones and lines on the far side of sidewalks
Hough 변환 라인 감지의 출력은 수평선과 보도의 먼 쪽에 있는 선을 포함하여 차선의 경계에 속하는 모든 선이다
Furthermore, each of the lane boundaries will have multiple associated output lines from the Hough transform line estimator
게다가, 각 차선 경계는 Hough 변환선 추정기에서 여러 개의 관련 출력 라인을 가질 것이다
You are required to filter out all irrelevant lines and merge relevant lines to produce one line per lane boundary
모든 관련 없는 선을 필터링하고 관련 라인을 병합하여 차선 경계당 한 줄을 생성해야 합니다
To filter out the horizontal lines, we can rely on the slope of the estimated lines
수평선을 필터링하기 위해, 우리는 예상 선의 기울기에 의존할 수 있다
Horizontal lines and images tend to have a slope very close to zero
수평선과 이미지는 기울기가 0에 매우 가까운 경향이 있다
However, we also want to remove heavily slanted lines
그러나, 우리는 또한 심하게 기울어진 선을 제거하고 싶다
As such, a threshold is introduced as a lower limit of allowed slopes for the output of this filtering step
따라서, 임계값은 이 필터링 단계의 출력에 허용된 기울기의 하한으로 도입된다
The exact value of this threshold needs to be determined empirically, try values between 0
이 임계값의 정확한 값은 경험적으로 결정되어야 하며, 최상의 결과를 얻으려면 0
1 and 0
1에서 0
3 for best results
3 사이의 값을 시도하십시오
Having removed horizontal lines from the output of the half transform, you will need to cluster similar lines and then merge them to produce a single line per lane boundary
반 변환 출력에서 수평선을 제거하려면 유사한 선을 클러스터한 다음 병합하여 차선 경계당 단일 선을 생성해야 합니다
A simple clustering algorithm would be to first choose a cluster center at random from the remaining filter lines, then add to the cluster any lines that have a similar slope or intercept to the cluster line
간단한 클러스터링 알고리즘은 먼저 나머지 필터 라인에서 무작위로 클러스터 센터를 선택한 다음 클러스터 라인에 비슷한 기울기 또는 가로채기를 가진 줄을 클러스터에 추가하는 것입니다
A line is considered close to the cluster center if the difference between its slope and slope of the cluster center is less than a specific slope threshold, and the distance between its intercept and the intercept of the cluster center is less than a specific intercept threshold as well
클러스터 센터의 기울기와 기울기의 차이가 특정 기울기 임계값보다 작고, 인터셉트와 클러스터 센터의 인터셉트 사이의 거리가 특정 인터셉트 임계값보다 작으면 선은 클러스터 센터에 가까운 것으로 간주됩니다
The slope difference threshold is usually chosen to be a maximum of 0
기울기 차이 임계값은 일반적으로 최대 0
3, while the intercept difference threshold is defined in pixels, and is usually chosen between 20 and 50 pixels
3으로 선택되는 반면, 요격 차이 임계값은 픽셀로 정의되며 일반적으로 20픽셀에서 50픽셀 사이에서 선택됩니다
You will need to test various values before arriving at a satisfactory threshold for the assessment
평가를 위한 만족스러운 임계값에 도달하기 전에 다양한 값을 테스트해야 합니다
The final step to produce one line per lane boundary, is to merge lines inside each cluster
차선 경계당 한 줄을 생성하는 마지막 단계는 각 클러스터 내부의 선을 병합하는 것이다
The simplest way to do so is through averaging the slope and intercept of all cluster members
그렇게 하는 가장 간단한 방법은 모든 클러스터 구성원의 경사와 가로채기를 평균하는 것이다
The final concept that you will need to finish the assessment, is how to filter out uncertain output of object detectors using the output from the semantic segmentation
평가를 완료하는 데 필요한 최종 개념은 의미론적 세분화의 출력을 사용하여 객체 검출기의 불확실한 출력을 필터링하는 방법입니다
The output of object detection is usually reliable
물체 감지의 출력은 보통 신뢰할 수 있다
But for this assessment, you are given a high recall low precision detector that detects all objects in the scene, but also provides some false positives
그러나 이 평가를 위해, 장면의 모든 물체를 감지하지만 몇 가지 오탐을 제공하는 높은 리콜 저정밀 검출기가 주어집니다
You are required to use the output from semantic segmentation to eliminate these false positives before estimating the distance to the obstacles
장애물까지의 거리를 추정하기 전에 이러한 오탐을 제거하기 위해 의미론적 세분화의 출력을 사용해야 합니다
The results should be bounding boxes that reliably contain obstacles
결과는 장애물을 안정적으로 포함하는 경계 상자여야 한다
To perform this filtering, you will need to use the semantic segmentation output to count the number of pixels in the bounding box that have the same category as the classification output from the 2D object detector
이 필터링을 수행하려면 시맨틱 세분화 출력을 사용하여 2D 개체 검출기의 분류 출력과 동일한 범주를 가진 경계 상자의 픽셀 수를 계산해야 합니다
The trick here, is that this number will depend on the size of the bounding box
여기서 트릭은 이 숫자가 경계 상자의 크기에 달려 있다는 것이다
You will need to normalize the pixel count by the area of the bounding box before attempting to filter out the detections with a threshold
임계값으로 탐지를 필터링하기 전에 경계 상자의 영역별로 픽셀 수를 정규화해야 합니다
The final normalized count is equivalent to computing the area inside the bounding box occupied by pixels belonging to the correct category
최종 정규화된 수는 올바른 범주에 속하는 픽셀이 차지하는 경계 상자 내부의 영역을 계산하는 것과 같다
At this point, you should be ready to tackle the final assessment confidently
이 시점에서, 당신은 최종 평가를 자신 있게 다룰 준비가 되어 있어야 합니다
As a final note, I encourage you to think of different ways you could achieve the final output for the required tasks, other than the suggested outline
마지막으로, 제안된 개요 외에 필요한 작업에 대한 최종 출력을 달성할 수 있는 다양한 방법을 생각하는 것이 좋습니다
I hope you enjoy this assessment and find it beneficial to your learning
저는 당신이 이 평가를 즐기고 그것이 당신의 학습에 도움이 되기를 바랍니다


