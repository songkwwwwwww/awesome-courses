So far in this module, you've learned how to detect, describe and match features, as well as how to handle outliers in our feature matching results
지금까지 이 모듈에서는 기능을 감지, 설명 및 매칭하는 방법과 기능 매칭 결과에서 이상값을 처리하는 방법을 배웠습니다
We've also explored an example of how to use features to localize an object in an image, which could be used to estimate the depth to the object from a pair of images
우리는 또한 한 쌍의 이미지에서 물체의 깊이를 추정하는 데 사용할 수 있는 이미지에서 개체를 현지화하는 방법에 대한 예를 살펴보았다
In this lesson, you will learn how to perform visual odometry, a fundamental task for vision-based state estimation in autonomous vehicles
이 수업에서는 자율주행 차량에서 비전 기반 상태 추정을 위한 기본적인 작업인 시각적 거리 측정을 수행하는 방법을 배우게 됩니다
Visual odometry, or VO for short, can be defined as the process of incrementally estimating the pose of the vehicle by examining the changes that motion induces on the images of its onboard cameras
시각 거리계 또는 간단히 말해서 VO는 온보드 카메라의 이미지에서 움직임이 유도하는 변화를 조사하여 차량의 포즈를 점진적으로 추정하는 과정으로 정의될 수 있다
It is similar to the concept of wheel odometry you learned in the second course, but with cameras instead of encoders
두 번째 과정에서 배운 휠 거리 측정의 개념과 비슷하지만 인코더 대신 카메라가 있습니다
What do you think using visual odometry might offer over regular wheel odometry for autonomous cars
시각 거리계를 사용하는 것이 자율주행차를 위한 일반 휠 거리계를 통해 무엇을 제공할 수 있다고 생각하십니까
Visual odometry does not suffer from wheel slip while turning or an uneven terrain and tends to be able to produce more accurate trajectory estimates when compared to wheel odometry
시각 거리계는 회전하는 동안 휠 슬립이나 고르지 않은 지형을 겪지 않으며 휠 거리 측정에 비해 더 정확한 궤적 추정치를 생성할 수 있는 경향이 있다
This is because of the larger quantity of information available from an image
이것은 이미지에서 사용할 수 있는 더 많은 양의 정보 때문입니다
However, we usually cannot estimate the absolute scale from a single camera
그러나, 우리는 보통 단일 카메라에서 절대 스케일을 추정할 수 없다
What this means is that estimation of motion produced from one camera can be stretched or compressed in the 3D world without affecting the pixel feature locations by adjusting the relative motion estimate between the two images
이것이 의미하는 바는 한 카메라에서 생성된 움직임의 추정이 두 이미지 사이의 상대적인 모션 추정치를 조정하여 픽셀 피처 위치에 영향을 미치지 않고 3D 세계에서 확장되거나 압축될 수 있다는 것이다
As a result, we need at least one additional sensor, often a second camera or an inertial measurement unit, to be able to provide accurately scaled trajectories when using VO
결과적으로, VO를 사용할 때 정확하게 확장된 궤적을 제공하기 위해 적어도 하나의 추가 센서, 종종 두 번째 카메라 또는 관성 측정 장치가 필요합니다
Furthermore, cameras are sensitive to extreme illumination changes, making it difficult to perform VO at night and in the presence of headlights and streetlights
게다가, 카메라는 극심한 조명 변화에 민감하여 밤과 헤드라이트와 가로등이 있는 곳에서 VO를 수행하기가 어렵다
Finally, as seen with other odometry estimation mechanisms, pose estimates from VO will always drift over time as estimation errors accumulate
마지막으로, 다른 거리 측정 추정 메커니즘에서 볼 수 있듯이, VO의 포즈 추정치는 추정 오류가 축적됨에 따라 항상 시간이 지남에 따라 표류할 것이다
For this reason, we often quote VO performance as a percentage error per unit distance traveled
이러한 이유로, 우리는 종종 VO 성능을 이동한 단위 거리당 백분율 오류로 인용합니다
Let's define the visual odometry problem mathematically
시각 거리 측정 문제를 수학적으로 정의해 봅시다
Given two consecutive image frames, I_k minus one and I_k, we want to estimate a transformation matrix T_k defined by the translation T and a rotation R between the two frames
두 개의 연속 이미지 프레임인 I_k 마이너스 1과 I_k를 감안할 때, 우리는 번역 T에 의해 정의된 변환 행렬 T_k와 두 프레임 사이의 회전 R을 추정하고 싶습니다
Concatenating the sequence of transformations estimated at each time step k from k naught to capital K will provide us with the full trajectory of the camera over the sequence of images
K에서 대문자 K로 k단계할 때마다 추정되는 변환 시퀀스를 연결하면 이미지 시퀀스에 대한 카메라의 전체 궤적을 제공할 것이다
Since the camera is rigidly attached to the autonomous vehicle, this also represents an estimate of the vehicle's trajectory
카메라가 자율주행 차량에 단단히 부착되어 있기 때문에, 이것은 또한 차량의 궤적 추정치를 나타낸다
Now we'll describe the general process of visual odometry
이제 우리는 시각적 거리 측정의 일반적인 과정을 설명할 것이다
We are given two consecutive image frames, I_k and I_k minus one, and we want to estimate the transformation T_k between these two frames
우리는 두 개의 연속 이미지 프레임인 I_k와 I_k 마이너스 1이 주어지며, 이 두 프레임 사이의 변환 T_k를 추정하고 싶습니다
First, we perform feature detection and description
먼저, 기능 감지 및 설명을 수행합니다
We end up with a set of features f_k minus one in image k minus one and F_k in image of k
우리는 이미지 k에서 f_k 마이너스 1과 k 이미지에서 F_k를 뺀 기능 세트로 끝납니다
We then proceed to match the features between the two frames to find the ones occurring in both of our target frames
그런 다음 두 프레임 사이의 기능을 일치시켜 두 대상 프레임에서 발생하는 기능을 찾습니다
After that, we use the matched features to estimate the motion between the two camera frames represented by the transformation T_k
그 후, 우리는 일치하는 기능을 사용하여 변환 T_k로 표시되는 두 카메라 프레임 사이의 움직임을 추정합니다
Motion estimation is the most important step in VO, and will be the main theme of this lesson
모션 추정은 VO에서 가장 중요한 단계이며, 이 수업의 주요 주제가 될 것이다
The way we perform the motion estimation step depends on what type of feature representation we have
우리가 모션 추정 단계를 수행하는 방법은 우리가 어떤 유형의 기능 표현을 가지고 있는지에 달려 있다
In 2D-2D motion estimation, feature matches in both frames are described purely in image coordinates
2D-2D 모션 추정에서, 두 프레임의 기능 일치는 순전히 이미지 좌표에 설명된다
This form of visual odometry is great for tracking objects in the image frame
이러한 형태의 시각적 거리계는 이미지 프레임의 물체를 추적하는 데 적합합니다
This is extremely useful for visual tracking and image stabilization in videography, for example
이것은 예를 들어 비디오그래피의 시각적 추적 및 이미지 안정화에 매우 유용합니다
In 3D-3D motion estimation, feature matches are described in the world 3D coordinate frame
3D-3D 모션 추정에서, 기능 일치는 세계 3D 좌표 프레임에 설명되어 있다
This approach requires the ability to locate new image features in 3D space, and is therefore used with depth cameras, stereo cameras, and other multi-camera configurations that can provide depth information
이 접근 방식은 3D 공간에서 새로운 이미지 기능을 찾을 수 있는 기능이 필요하므로 깊이 정보를 제공할 수 있는 깊이 카메라, 스테레오 카메라 및 기타 멀티 카메라 구성과 함께 사용됩니다
These two cases are important and follow the same general visual odometry framework that we'll use for the rest of this lesson
이 두 경우는 중요하며 이 수업의 나머지 부분에 사용할 것과 동일한 일반적인 시각적 거리 측정 프레임워크를 따릅니다
Let's take a closer look at 3D-2D motion estimation, where the features from frame k minus one are specified in the 3D world coordinates while their matches in frame k are specified in image coordinates
프레임 k 마이너스 1의 특징이 3D 세계 좌표에 지정되고 프레임 k의 일치가 이미지 좌표에 지정되는 3D-2D 모션 추정을 자세히 살펴보겠습니다
Here's how 3D-2D motion estimation is performed
3D-2D 모션 추정이 수행되는 방법은 다음과 같습니다
We are given the set of features in frame k minus one and estimates of their 3D world coordinates
프레임 k 마이너스 원의 기능 세트와 3D 세계 좌표 추정치가 주어집니다
Furthermore, through feature matching, we also have the 2D image coordinates of the same features in the new frame k
게다가, 기능 매칭을 통해, 우리는 또한 새로운 프레임 k에서 동일한 기능의 2D 이미지 좌표를 가지고 있습니다
Note that since we cannot recover the scale for a monocular visual odometry directly, we include a scaling parameter S when forming the homogeneous feature vector from the image coordinates
단안 시각적 거리 측정의 스케일을 직접 복구할 수 없기 때문에 이미지 좌표에서 균일한 피처 벡터를 형성할 때 스케일링 매개 변수 S를 포함합니다
We want to use this information to estimate the rotation matrix R and a translation vector t between the two camera frames
우리는 이 정보를 사용하여 두 카메라 프레임 사이의 회전 매트릭스 R과 번역 벡터 t를 추정하고 싶습니다
Does this figure remind you of something that we've learned about previously
이 수치는 우리가 이전에 배운 것을 생각나게 하나요
If you're thinking of camera calibration, you're correct
카메라 보정을 생각하고 있다면, 당신이 옳습니다
In fact, we use the same projective geometry equations we used for calibration in visual odometry as well
사실, 우리는 시각적 거리 측정에서 교정하는 데 사용한 것과 동일한 투영 기하학 방정식을 사용합니다
A simplifying distinction to note between calibration and VO is that the camera intrinsic calibration matrix k is already known
교정과 VO 사이의 단순화된 구별은 카메라 본질적인 교정 매트릭스 k가 이미 알려져 있다는 것이다
So we don't have to solve for it again
그래서 우리는 그것을 다시 해결할 필요가 없다
Our problem now reduces to the estimation of the transformation components R and t from the system of equations constructed using all of our matched features
우리의 문제는 이제 일치하는 모든 기능을 사용하여 구성된 방정식 시스템에서 변환 구성 요소 R과 t의 추정으로 줄어듭니다
One way we can solve for the rotation and translation t is by using the Perspective-n-Point algorithm
회전과 번역 t를 해결할 수 있는 한 가지 방법은 Perspective-n-Point 알고리즘을 사용하는 것이다
Given feature locations in 3D, their corresponding projection in 2D, and the camera intrinsic calibration matrix k, PnP solves for the extrinsic transformations as follows
3D의 기능 위치, 해당 투영 2D 및 카메라 본질 교정 매트릭스 k가 주어진 PnP는 다음과 같이 외부 변환을 해결합니다
First, PnP uses the Direct Linear Transform to solve for an initial guess for R and t
첫째, PnP는 직접 선형 변환을 사용하여 R과 t에 대한 초기 추측을 해결합니다
The DLT method for estimating R and t requires a linear model and constructs a set of linear equations to solve using standard methods such as SVD
R과 t를 추정하는 DLT 방법은 선형 모델이 필요하며 SVD와 같은 표준 방법을 사용하여 해결하기 위해 선형 방정식 세트를 구성합니다
However, the equations we have are nonlinear in the parameters of R and t
그러나, 우리가 가진 방정식은 R과 t의 매개 변수에서 비선형이다
In the next step, we'll refine the initial DLT solution with an iterative nonlinear optimization technique such as the Luvenburg Marquardt method
다음 단계에서는 Luvenburg Marquardt 방법과 같은 반복적인 비선형 최적화 기술로 초기 DLT 솔루션을 개선할 것입니다
The PnP algorithm requires at least three features to solve for R and t
PnP 알고리즘은 R과 t를 해결하기 위해 적어도 세 가지 기능이 필요하다
When only three features are used, four possible solutions results, and so a fourth feature point is employed to decide which solution is valid
세 가지 기능만 사용하면 네 가지 가능한 솔루션 결과가 나오므로, 어떤 솔루션이 유효한지 결정하기 위해 네 번째 기능 지점이 사용됩니다
Finally, RANSAC can be incorporated into PnP by assuming that the transformation generated by PnP on four points is our model
마지막으로, RANSAC은 PnP가 4개 지점에서 생성한 변환이 우리의 모델이라고 가정함으로써 PnP에 통합될 수 있다
We then choose a subset of all feature matches to evaluate this model and check the percentage of inliers that result to confirm the validity of the point matches selected
그런 다음 모든 기능 일치의 하위 집합을 선택하여 이 모델을 평가하고 결과의 이상값의 비율을 확인하여 선택한 포인트 일치의 유효성을 확인합니다
The PnP method is an efficient approach to solving the visual odometry problem, but uses only a subset of the available matches to compute the solution
PnP 방법은 시각적 거리 측정 문제를 해결하는 효율적인 접근 방식이지만, 해결책을 계산하기 위해 사용 가능한 일치의 하위 집합만 사용합니다
We can improve on PnP by applying the batch estimation techniques you studied in course two
우리는 당신이 코스 2에서 공부한 배치 추정 기술을 적용하여 PnP를 개선할 수 있습니다
By doing so, we can also incorporate additional measurements from other onboard sensors and incorporate vision into the state estimation pipeline
그렇게 함으로써, 우리는 또한 다른 온보드 센서의 추가 측정을 통합하고 시야를 상태 추정 파이프라인에 통합할 수 있습니다
With vision included, we can better handle GPS-denied environments and improve both the accuracy and reliability of our pose estimates
비전을 포함하여, 우리는 GPS 거부 환경을 더 잘 처리하고 포즈 추정치의 정확성과 신뢰성을 모두 향상시킬 수 있습니다
There are many more interesting details to consider when implementing VO algorithms
VO 알고리즘을 구현할 때 고려해야 할 더 많은 흥미로운 세부 사항이 있습니다
Fortunately, the PnP method has a robust implementation available in OpenCV
다행히도, PnP 방법은 OpenCV에서 사용할 수 있는 강력한 구현을 가지고 있다
In fact, OpenCV even contains a version of PnP with RANSAC incorporated for outlier rejection
사실, OpenCV에는 이상치 거부를 위해 RANSAC이 통합된 PnP 버전도 포함되어 있습니다
You can follow the link in the supplementary reading for a description on how to use PnP in OpenCV
추가 읽기에 있는 링크를 따라 OpenCV에서 PnP를 사용하는 방법에 대한 설명을 확인할 수 있습니다
In this lesson, you learned why visual odometry is an attractive solution to estimate the trajectory of a self-driving car and how to perform visual odometry for 3D-2D correspondences
이 수업에서는 시각적 거리 측정이 자율주행 자동차의 궤적을 추정하는 매력적인 솔루션인 이유와 3D-2D 서신에 대한 시각적 거리 측정을 수행하는 방법을 배웠습니다
Next week, we'll delve into a fundamental approach to extracting information from images for self-driving car perception, deep neural networks
다음 주에, 우리는 자율주행 자동차 인식, 심층 신경망을 위한 이미지에서 정보를 추출하는 근본적인 접근 방식을 탐구할 것입니다
By this point, you've now finished the second week of visual perception for self-driving cars
이 시점까지, 당신은 이제 자율주행 자동차에 대한 시각적 인식의 두 번째 주를 마쳤습니다
Don't worry if you did not acquire a full grasp of all the material explained in this week
이번 주에 설명된 모든 자료를 완전히 이해하지 못했다면 걱정하지 마세요
In this week's assignment, you'll be gaining hands-on experience on all of these topics
이번 주 과제에서, 당신은 이 모든 주제에 대한 실무 경험을 쌓게 될 것입니다
You'll use feature detection, matching, and the PnP algorithm to build your own autonomous vehicle visual odometry system in Python
기능 감지, 매칭 및 PnP 알고리즘을 사용하여 파이썬에서 자신만의 자율주행 차량 시각적 거리 측정 시스템을 구축할 것입니다
See you in the next module
다음 모듈에서 뵙겠습니다


