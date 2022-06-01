Welcome to the first lesson of week two. 
2주차 첫 수업에 오신 것을 환영합니다. 

This week we will discuss many details about the hardware and software architecture used in today's self-driving cars. 
이번 주에 우리는 오늘날의 자율주행 자동차에 사용되는 하드웨어 및 소프트웨어 아키텍처에 대한 많은 세부 사항을 논의할 것입니다. 

In particular, we will cover the various sensors that can be used for perception. 
특히, 우리는 인식에 사용될 수 있는 다양한 센서를 다룰 것이다. 

The computing platforms available today. The basics of designing sensor configurations for self-driving cars. 
오늘날 이용 가능한 컴퓨팅 플랫폼. 자율주행 자동차를 위한 센서 구성을 설계하는 기본 사항. 

The components of a typical autonomy software stack. 
일반적인 자율 소프트웨어 스택의 구성 요소. 

And finally, we will conclude by discussing the various ways which we can represent the environment for self-driving. 
그리고 마지막으로, 우리는 자율주행 환경을 대표할 수 있는 다양한 방법을 논의함으로써 결론을 내릴 것이다. 

Hopefully by the end of this week you will have a broad understanding of the equipment and software ideas that go into making a self-driving car. 
이번 주 말까지 자율주행 자동차를 만드는 데 들어가는 장비와 소프트웨어 아이디어에 대한 폭 넓은 이해를 갖기를 바랍니다. 

Let's begin this video. In this video, we will define sensors, and discuss the various types of sensors available for the task of perception. 
이 비디오를 시작하자. 이 비디오에서, 우리는 센서를 정의하고, 인식 작업에 사용할 수 있는 다양한 유형의 센서에 대해 논의할 것입니다. 

And we will then discuss the self-driving car hardware available nowadays. Let's begin by talking about sensors. 
그리고 우리는 요즘 이용 가능한 자율주행 자동차 하드웨어에 대해 논의할 것이다. 
센서에 대해 이야기하는 것으로 시작합시다. 

Even the best perception algorithms are limited by the quality of their sensor data. And careful selection of sensors can go a long way to simplifying the self-driving perception task. 
최고의 인식 알고리즘조차도 센서 데이터의 품질에 의해 제한된다. 그리고 센서의 신중한 선택은 자율주행 인식 작업을 단순화하는 데 큰 영향을 미칠 수 있다. 

So what is a sensor? A sensor is any device that measures or detects some property of the environment, or changes to that property over time. 
그래서 센서가 뭐야? 센서는 환경의 일부 특성을 측정하거나 감지하거나 시간이 지남에 따라 해당 속성을 변경하는 장치입니다. 

Sensors are broadly categorized into two types, depending on what property they record. 
센서는 기록하는 속성에 따라 크게 두 가지 유형으로 분류됩니다. 

If they record a property of the environment they are exteroceptive. 
만약 그들이 환경의 재산을 기록한다면 그들은 외적 수용적이다. 

Extero means outside, or from the surroundings. 
Extero는 외부 또는 주변을 의미합니다. 

On the other hand, if the sensors record a property of the ego vehicle, they are proprioceptive. 
반면에, 센서가 자아 차량(ego vehicle)의 특성을 기록한다면, 그들은 자기 수용적이다. 

Proprios means internal, or one's own. 
Proprios는 내부 또는 자신의 것을 의미한다. 

Let's start by discussing common exteroceptive sensors. 
일반적인 외수용 센서에 대해 논의하는 것으로 시작합시다. 

We start with the most common and widely used sensor in autonomous driving, the camera. 
우리는 자율주행에서 가장 일반적이고 널리 사용되는 센서인 카메라로 시작합니다. 

Cameras are a passive, light-collecting sensor that are great at capturing rich, detailed information about a scene. 
카메라는 장면에 대한 풍부하고 상세한 정보를 캡처하는 데 능대한 수동적이고 빛을 수집하는 센서입니다. 

In fact, some groups believe that the camera is the only sensor truly required for self-driving. 
사실, 일부 그룹은 카메라가 자율주행에 진정으로 필요한 유일한 센서라고 믿는다. 

But state of the art performance is not yet possible with vision alone. 
하지만 최첨단 공연은 아직 비전만으로는 불가능하다. 

While talking about cameras, we usually tend to talk about three important comparison metrics. 
카메라에 대해 이야기하는 동안, 우리는 보통 세 가지 중요한 비교 지표에 대해 이야기하는 경향이 있다. 

We select cameras in terms of their resolution. The resolution is the number of pixels that create the image. 
우리는 그들의 해상도 측면에서 카메라를 선택한다. 해상도는 이미지를 생성하는 픽셀 수입니다. 

So it's a way of specifying the quality of the image. 
그래서 그것은 이미지의 품질을 지정하는 방법이다. 

We can also select cameras on the basis of field of view. 
우리는 또한 시야(화각,fov)를 기반으로 카메라를 선택할 수 있습니다. 

The field of view is defined by the horizontal and vertical angular extent that is visible to the camera, and can be varied through lens selection and zoom. 
시야는 카메라에 보이는 수평 및 수직 각도로 정의되며, 렌즈 선택과 줌을 통해 다양할 수 있습니다. 

Another important metric is the dynamic range. 
또 다른 중요한 지표는 동적 범위이다. 

The dynamic range of the camera is the difference between the darkest and the lightest tones in an image. 
카메라의 동적 범위는 이미지에서 가장 어두운 톤과 가장 밝은 톤의 차이이다. 

High dynamic range is critical for self-driving vehicles due to the highly variable lighting conditions encountered while driving especially at night. 
높은 다이내믹 레인지는 특히 밤에 운전하는 동안 발생하는 매우 다양한 조명 조건으로 인해 자율주행 차량에 매우 중요합니다. 

There is an important trade off cameras and lens selection, that lies between the choice of field of view and resolution. 
중요한 카메라와 렌즈 선택에는 시야(fov)와 해상도(resolution) 사이에서서의 중요한 트레이드 오프가 있다.

Wider field of view permit a lager viewing region in the environment. 
더 넓은 시야(fov)는 환경에서 영역을 보다 넓게 볼 수 있도록 허용한다. 

But fewer pixels that absorb light from one particular object. 
하지만 특정 물체의 빛을 흡수하는 픽셀은 적다. 

As the field of view increases, we need to increase resolution to still be able to perceive with the same quality, the various kinds of information we may encounter. 
시야가 증가함에 따라, 우리는 여전히 동일한 품질, 우리가 만날 수 있는 다양한 종류의 정보로 인식할 수 있도록 해상도를 높여야 한다. 

Other properties of cameras that affect perception exist as well, such as focal length, depth of field and frame rate. 
초점 거리, 피사계 심도 및 프레임 속도와 같은 인식에 영향을 미치는 카메라의 다른 특성도 존재합니다. 

We'll go into much more detail on cameras and computer vision in course three on visual perception. 
우리는 시각적 인식에 대한 과정 3에서 카메라와 컴퓨터 비전에 대해 훨씬 더 자세히 설명할 것이다. 

The combination of two cameras with overlapping fields of view and aligned image planes is called the stereo camera. 
겹치는 시야와 정렬된 이미지 평면과 두 카메라의 조합을 스테레오 카메라라고 한다. 

Stereo cameras allow depth estimation from synchronized image pairs. 
스테레오 카메라는 동기화된 이미지 쌍의 깊이 추정을 허용합니다. 

Pixel values from image can be matched to the other image producing a disparity map of the scene. 
이미지의 픽셀 값은 장면의 격차 지도를 생성하는 다른 이미지와 일치할 수 있습니다. 

This disparity can then be used to estimate depth at each pixel. 
이 격차는 각 픽셀의 깊이를 추정하는 데 사용될 수 있다.

Next we have LIDAR which stands for light detection and ranging sensor. 
다음으로 우리는 빛 감지 및 범위 센서를 의미하는 LIDAR를 가지고 있습니다.

LIDAR sensing involves shooting light beams into the environment and measuring the reflected return. 
LIDAR 감지는 빛 빔을 환경으로 쏘고 반사된 것을 측정하는 것을 포함한다.

By measuring the amount of returned light and time of flight of the beam. 
반환된 빛의 양과 빔의 비행 시간을 측정함으로써. 

Both in intensity in range to the reflecting object can be estimated. 
반사 물체에 대한 범위의 강도 둘 다 추정할 수 있다.

LIDAR usually include a spinning element with multiple stacked light sources. 
LIDAR는 보통 여러 개의 쌓인 광원을 가진 회전 요소를 포함한다. 

And output a three dimensional point cloud map, which is great for assessing scene geometry. 
그리고 장면 기하학을 평가하는 데 좋은 3차원 포인트 클라우드 맵을 출력합니다. 

Because it is an active sensor with it's own light sources, LIDAR are not effected by the environments lighting. 
자체 광원이 있는 활성 센서이기 때문에 LIDAR는 환경 조명에 영향을 받지 않습니다. 

So LIDAR do not face the same challenges as cameras when operating in poor or variable lighting conditions. 
따라서 LIDAR는 열악하거나 다양한 조명 조건에서 작동할 때 카메라와 같은 문제에 직면하지 않습니다. 

Let's discuss the important comparison metrics for selecting LIDAR. 
LIDAR를 선택하는 데 중요한 비교 지표에 대해 논의해 봅시다.

The first is the number of sources it contains with 8, 16, 32, and 64 being common sizes. 
첫 번째는 8, 16, 32, 64가 일반적인 크기인 소스의 수이다. 

And the second is the points per second it can collect. 
그리고 두 번째는 수집할 수 있는 초당 포인트이다. 

The faster the point collection, the more detailed the 3D point cloud can be. 
포인트 수집이 빠를수록 3D 포인트 클라우드가 더 상세해질 수 있다. 

Another characteristic is the rotation rate. 
또 다른 특징은 회전 속도이다. 

The higher this rate, the faster the 3D point clouds are updated. 
이 속도가 높을수록 3D 포인트 클라우드가 더 빨리 업데이트됩니다. 

Detection range is also important, and is dictated by the power output of the light source. 
감지 범위도 중요하며, 광원의 전원 출력에 의해 결정된다. 

And finally, we have the field of view, which once again, is the angular extent visible to the LIDAR sensor. 
그리고 마지막으로, 우리는 다시 한 번 LIDAR 센서에 보이는 각도인 시야(fov)를 가지고 있다. 

Finally, we should also mention the new LIDAR types that are currently emerging. 
마지막으로, 우리는 또한 현재 등장하고 있는 새로운 LIDAR 유형을 언급해야 한다. 

High-resolution, solid-state LIDAR. 
고해상도 고체 LIDAR. 

Without a rotational component of the typical LIDARs, these sensors stand to become extremely low-cost and reliable. 
일반적인 LIDAR의 회전 구성 요소가 없다면, 이 센서는 매우 저렴하고 신뢰할 수 있다. 

Thanks to being implemented entirely in silicon. HD solid-state LIDAR are still a work in progress. 
완전히 실리콘으로 구현된 덕분에. HD 고체 LIDAR는 여전히 진행 중인 작업이다. 

But definitely something exciting for the future of affordable self-driving. 
하지만 확실히 저렴한 자율주행의 미래를 위한 흥미로운 것. 

Our next sensor is RADAR, which stands for radio detection and ranging. 
우리의 다음 센서는 무선 감지 및 범위를 의미하는 레이더입니다. 

RADAR sensors have been around longer than LIDAR and robustly detect large objects in the environment. 
레이더 센서는 LIDAR보다 길었고 환경의 큰 물체를 강력하게 감지한다. 

They are particularly useful in adverse weather as they are mostly unaffected by precipitation. 
그들은 대부분 강수량의 영향을 받지 못하기 때문에 악천후에 특히 유용하다. 

Let's discuss some of the comparison metrics for selecting RADAR. 
레이더를 선택하기 위한 몇 가지 비교 지표에 대해 논의해 봅시다. 

RADAR are selected based on detection range, field of view, and the position and speed measurement accuracy. 
레이더는 감지 범위, 시야, 위치 및 속도 측정 정확도에 따라 선택됩니다. 

RADAR are also typically available as either having a wide angular field of view but short range. 
레이더는 또한 일반적으로 넓은 각 시야를 가지고 있지만 범위는 짧다. 

Or having a narrow filed of view but a longer range. 
또는 좁은 시야가 있지만 더 긴 범위를 가지고 있다. 

The next sensor we are going to discuss are ultrasonics or sonars. 
우리가 논의할 다음 센서는 초음파나 소나이다. 

Originally so named for sound navigation and ranging. 
원래 사운드 내비게이션과 범위의 이름을 따서 명명되었다. 

Which measure range using sound waves. 
음파를 사용하여 범위를 측정하는 것. 

Sonar are sensors that are short range in inexpensive ranging devices. 
Sonar는 저렴한 범위의 장치에서 단거리인 센서이다. 

This makes them good for parking scenarios, where the ego-vehicle needs to make movements very close to other cars. 
이것은 자아 차량이 다른 자동차와 매우 가깝게 움직여야 하는 주차 시나리오에 좋다. 

Another great thing about sonar is that they are low-cost. 
소나에 대한 또 다른 좋은 점은 그들이 저렴하다는 것이다. 

Moreover, just like RADAR and LIDAR, they are unaffected by lighting and precipitation conditions. 
게다가, 레이더와 라이더와 마찬가지로, 그들은 조명과 강수량 조건의 영향을 받지 않는다. 

Sonar is selected based on a few key metrics. 
Sonar는 몇 가지 주요 평가 기준에 따라 선택됩니다. 

The maximum range they can measure, the detection field of view, and their cost. 
그들이 측정할 수 있는 최대 범위, 감지 시야 및 비용. 

Now let's discuss the proprioceptive sensors, the sensors that sense ego properties. 
이제 고유 수용성 센서, 자아 특성을 감지하는 센서에 대해 논의해 봅시다. 

The most common ones here are Global Navigation Satellite Systems, GNSS for short, such as GPS or Galileo.
여기서 가장 흔한 것은 GPS나 갈릴레오와 같은 GNSS인 글로벌 내비게이션 위성 시스템이다. 

An inertial measurement units or IMU's. 
관성 측정 장치 또는 IMU. 

GNSS receivers are used to measure ego vehicle position, velocity, and sometimes heading. 
GNSS 수신기는 자아 차량(ego vehicle)의 위치, 속도 및 때로는 제목을 측정하는 데 사용됩니다. 

The accuracy depends a lot on the actual positioning methods and the corrections used. 
정확성은 실제 포지셔닝 방법과 사용된 수정에 크게 의존한다. 

Apart from these, the IMU also measures the angular rotation rate, accelerations of the ego vehicle, 
이 외에도, IMU는 또한 각 회전 속도, 자아 차량의 가속도를 측정하며, 

and the combined measurements can be used to estimate the 3D orientation of the vehicle. 
결합된 측정을 사용하여 차량의 3D 방향을 추정할 수 있습니다. 

Where heading is the most important for vehicle control. 
heading은 차량 제어에 가장 중요한 곳이다. 

And finally we have wheel odometry sensors. 
그리고 마지막으로 우리는 바퀴 거리 측정 센서를 가지고 있다. 

This sensor tracks the wheel rates of rotation, and uses these to estimate the speed and heading rate of change of the ego car. 
이 센서는 바퀴 회전 속도를 추적하며, 이를 사용하여 자아 자동차의 변화 속도의 헤딩 속도를 추정합니다. 

This is the same sensor that tracks the mileage on your vehicle. 
이것은 차량의 마일리지를 추적하는 것과 동일한 센서입니다. 

So, to summarize, the major sensors used nowadays for autonomous driving perception include cameras, RADAR, LIDAR, sonar, GNSS, IMUs, and wheel odometry modules. 
요약하자면, 오늘날 자율주행 인식에 사용되는 주요 센서에는 카메라, 레이더, LIDAR, 소나, GNSS, IMU 및 휠 거리 측정 모듈이 포함됩니다. 

These sensors have many characteristics that can vary wildly, including resolution, detection range, and field-of-view. 
이 센서들은 해상도, 감지 범위 및 시야를 포함하여 크게 달라질 수 있는 많은 특성을 가지고 있다. 

Selecting an appropriate sensor configuration for a self-driving car is not trivial. 
자율주행 자동차에 적합한 센서 구성을 선택하는 것은 사소한 것이 아니다. 

Here's a simple graphic that shows each of the sensors and where they usually go on a car. 
다음은 각 센서와 그들이 보통 차에서 어디로 가는지 보여주는 간단한 그래픽입니다. 

We will revisit this chart again in the next video, when we discuss how to select sensor configurations to achieve a particular operational design domain. 
우리는 특정 운영 설계 도메인을 달성하기 위해 센서 구성을 선택하는 방법을 논의할 때 다음 비디오에서 이 차트를 다시 방문할 것입니다. 

Finally, let's discuss a little bit about the computing hardware most commonly used in today's self-driving cars. 
마지막으로, 오늘날의 자율주행 자동차에서 가장 일반적으로 사용되는 컴퓨팅 하드웨어에 대해 조금 논의해 봅시다. 

The most crucial part is the computing brain, the main decision making unit of the car. 
가장 중요한 부분은 자동차의 주요 의사 결정 단위인 컴퓨팅 두뇌이다. 

It takes in all sensor data and outputs the commands needed to drive the vehicle. 
그것은 모든 센서 데이터를 가져오고 차량을 운전하는 데 필요한 명령을 출력한다. 

Most companies prefer to design their own computing systems that match the specific requirements of their sensors and algorithms. 
대부분의 회사는 센서와 알고리즘의 특정 요구 사항에 맞는 자체 컴퓨팅 시스템을 설계하는 것을 선호합니다. 

Some hardware options exist, however, that can handle self-driving computing loads out of the box. 
그러나 자체 운전 컴퓨팅 부하를 처리할 수 있는 일부 하드웨어 옵션이 존재합니다. 

The most common examples would be Nvidia's Drive PX and Intel & Mobileye's EyeQ. 
가장 일반적인 예는 엔비디아의 드라이브 PX와 인텔 & 모빌아이의 아이Q일 것이다. 

Any computing brain for self-driving needs both serial and parallel compute modules. 
자율주행을 위한 모든 컴퓨팅 두뇌는 직렬 및 병렬 컴퓨팅 모듈이 모두 필요하다. 

Particularly for image and LIDAR processing to do segmentation, object detection, and mapping. 
특히 세분화, 물체 감지 및 매핑을 위한 이미지 및 LIDAR 처리를 위해. 

For these we employ GPUs, FPGAs and custom ASICs, which are specialized hardware to do a specific type of computation. 
이를 위해 우리는 특정 유형의 계산을 수행하기 위한 특수 하드웨어인 GPU, FPGA 및 맞춤형 ASIC을 사용합니다. 

For example; the drive PX units include multiple GPUs. 
예를 들어, 드라이브 PX 장치는 여러 GPU를 포함한다. 

And the EyeQs have FPGAs both to accelerate parallalizable compute tasks, such as image processing or neural network inference. 
그리고 EyeQ에는 이미지 처리나 신경망 추론과 같은 마비 가능한 컴퓨팅 작업을 가속화하기 위한 FPGA가 있습니다. 

And finally, a quick comment about synchronization. 
그리고 마지막으로, 동기화에 대한 빠른 논평. 

Because we want to make driving decisions based on a coherent picture of the road scene. 
왜냐하면 우리는 도로 장면의 일관된 그림을 바탕으로 운전 결정을 내리고 싶기 때문이다. 

It is essential to correctly synchronize the different modules in the system, and serve a common clock. 
시스템의 다른 모듈을 올바르게 동기화하고 공통 시계를 제공하는 것이 필수적이다. 

Fortunately, GPS relies on extremely accurate timing to function, and as such can act as an appropriate reference clock when available. 
다행히도, GPS는 작동하기 위해 매우 정확한 타이밍에 의존하며, 가능한 경우 적절한 참조 시계 역할을 할 수 있다. 

Regardless, sensor measurements must be timestamped with consistent times for sensor fusion to function correctly. 
그럼에도 불구하고, 센서 측정은 센서 융합이 올바르게 작동하려면 일관된 시간으로 타임스탬프되어야 한다. 

Let's summarize. 
요약해 봅시다. 

In this video, we learned about sensors and their different types based on what they measure. 
이 비디오에서, 우리는 그들이 측정하는 것을 바탕으로 센서와 그들의 다양한 유형에 대해 배웠다. 

We covered the major sensors used in self-driving hardware systems, and discussed the advantages and comparison metrics. 
우리는 자율주행 하드웨어 시스템에 사용되는 주요 센서를 다루었고, 장점과 비교 지표에 대해 논의했다. 

And then we briefly discussed the self-driving computing hardware available today. 
그리고 나서 우리는 오늘날 이용 가능한 자율주행 컴퓨팅 하드웨어에 대해 간략하게 논의했다. 

Hopefully, this solidifies some of the concepts we learned last week for doing autonomous perception. 
바라건대, 이것이 우리가 자율 인식을 하기 위해 지난 주에 배운 몇 가지 개념을 확고히 하기를 바랍니다. 

In the next lesson, we'll take a step further and look at how to select an appropriate sensor configuration for your self-driving car. 
다음 수업에서, 우리는 한 걸음 더 나아가 자율주행 자동차에 적합한 센서 구성을 선택하는 방법을 살펴볼 것입니다. 

See you in the next video. 
다음 비디오에서 보자.