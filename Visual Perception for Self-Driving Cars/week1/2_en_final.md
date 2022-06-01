Welcome to the visual perception course of the University of Toronto self-driving car specialization
토론토 대학교 자율주행 자동차 전문 분야의 시각적 인식 과정에 오신 것을 환영합니다
My name is Steve and I'll be your instructor once again throughout this course
제 이름은 스티브이고 이 과정을 통해 다시 한 번 당신의 강사가 될 것입니다
By now, you should have completed the first two courses in the self-driving car specialization
지금까지, 당신은 자율주행 자동차 전문 분야의 처음 두 과정을 완료했어야 합니다
In these two courses, you learned how to build, model, control, and localize the self-driving car using a variety of sensors including GPS, IMU, and LIDAR sensors
이 두 과정에서는 GPS, IMU 및 LIDAR 센서를 포함한 다양한 센서를 사용하여 자율주행 자동차를 제작, 모델링, 제어 및 현지화하는 방법을 배웠습니다
This course will focus on one of the most versatile sensors for the self-driving car, the camera
이 과정은 자율주행 자동차를 위한 가장 다재다능한 센서 중 하나인 카메라에 초점을 맞출 것이다
Cameras act as the eyes of the self-driving car
카메라는 자율주행 자동차의 눈 역할을 한다
The cars use cameras to detect agents on the road, model their movement, and model their behaviors
자동차는 카메라를 사용하여 도로의 요원을 감지하고, 움직임을 모델링하고, 행동을 모델링한다
Images from the camera can also be used to detect and localized road markings, signals, and signs to allow for safe and lawful driving behavior
카메라의 이미지는 또한 안전하고 합법적인 운전 행동을 허용하기 위해 도로 표시, 신호 및 표지판을 감지하고 현지화하는 데 사용될 수 있습니다
We can use cameras for localization similar to the LIDAR sensors
우리는 LIDAR 센서와 유사한 현지화를 위해 카메라를 사용할 수 있습니다
By the end of this course, you'll be able to use and calibrate these cameras to build a baseline perception stack for self-driving cars
이 과정이 끝나면, 이 카메라를 사용하고 보정하여 자율주행 자동차를 위한 기본 인식 스택을 구축할 수 있습니다
So, now let's go through the course syllabus to see what you will learn about each week
그래서, 이제 과정 강의 계획서를 통해 매주 무엇을 배울지 봅시다
The first module of this course we will introduce the basics of 3D computer vision
이 과정의 첫 번째 모듈에서는 3D 컴퓨터 비전의 기초를 소개합니다
You will learn how images are formed, the camera projective geometry, how to calibrate cameras, and how to generate 3D point clouds from the cameras through stereovision
이미지가 어떻게 형성되는지, 카메라 투영 기하학, 카메라를 보정하는 방법, 스테레오비전으로 카메라에서 3D 포인트 클라우드를 생성하는 방법을 배우게 됩니다
Finally, you'll learn how to process images with common image filters
마지막으로, 일반적인 이미지 필터로 이미지를 처리하는 방법을 배우게 될 것입니다
In the second module, you will learn how to extract useful information from images through hand engineered features
두 번째 모듈에서는 손 조작 기능을 통해 이미지에서 유용한 정보를 추출하는 방법을 배우게 됩니다
You will learn how to extract these features, provide them with descriptors, and learn how to match these features with each other
이러한 기능을 추출하고, 설명자를 제공하고, 이러한 기능을 서로 일치시키는 방법을 배우게 될 것입니다
Finally, we'll use these matched features to localize a camera, a process known as visual odometry
마지막으로, 우리는 이러한 일치하는 기능을 사용하여 시각적 거리 측정으로 알려진 프로세스인 카메라를 현지화할 것입니다
In the third module, we will cover neural networks, a concept that has changed how we think of perception for self-driving cars
세 번째 모듈에서, 우리는 자율주행 자동차에 대한 인식에 대한 생각을 바꾼 개념인 신경망을 다룰 것이다
During this module, you will learn about the building blocks of feedforward neural networks, how to train these networks, and how to evaluate their performance
이 모듈에서는 피드포워드 신경망의 구성 요소, 이러한 네트워크를 훈련시키는 방법 및 성능을 평가하는 방법에 대해 배우게 됩니다
Also, you will learn about a special type of feedforward neural network, convolutional neural networks, that are tailored to process images from cameras
또한, 카메라의 이미지를 처리하도록 맞춤화된 특별한 유형의 피드포워드 신경망, 컨볼루션 신경망에 대해 배우게 될 것입니다
In the fourth module, you will use neural networks to perform 2D object detection, a joint classification and regression task
네 번째 모듈에서는 신경망을 사용하여 2D 물체 감지, 공동 분류 및 회귀 작업을 수행합니다
You will learn how to formulate the 2D object detection problem, how to evaluate 2D object detection models, how to build neural networks that perform the 2D object detection task, and how to use the output of 2D object detectors in the context to self-driving cars
2D 물체 감지 문제를 공식화하는 방법, 2D 물체 감지 모델을 평가하는 방법, 2D 물체 감지 작업을 수행하는 신경망을 구축하는 방법, 자율주행 자동차에 맥락에서 2D 물체 검출기의 출력을 사용하는 방법을 배우게 될 것입니다
Specifically, you will use 2D object detection results to predict 3D position and track objects of interest in road scenes
특히, 2D 물체 감지 결과를 사용하여 3D 위치를 예측하고 도로 장면에 관심 있는 물체를 추적할 것입니다
The fifth week of the course will cover semantic segmentation, another important component of a self-driving cars perception stack
이 과정의 다섯 번째 주는 자율주행 자동차 인식 스택의 또 다른 중요한 구성 요소인 의미론적 세분화를 다룰 것이다
Similar to the 2D detection module, you will learn to formulate the semantic segmentation problem, evaluate semantic segmentation models, and perform semantic segmentation tasks using convolutional neural networks
2D 감지 모듈과 마찬가지로, 당신은 의미론적 세분화 문제를 공식화하고, 의미론적 세분화 모델을 평가하고, 컨볼루션 신경망을 사용하여 의미론적 세분화 작업을 수행하는 방법을 배우게 될 것입니다
Finally, you will learn how to use semantic segmentation output to perform drivable space estimation and line boundary detection
마지막으로, 의미 세분화 출력을 사용하여 운전 가능한 공간 추정과 선 경계 감지를 수행하는 방법을 배우게 될 것입니다
For the final week of the course, you will apply everything you've learned to the final course project
과정의 마지막 주 동안, 당신은 당신이 배운 모든 것을 최종 과정 프로젝트에 적용할 것입니다
This project will require you to implement a self-driving car obstacle avoidance system using only camera data as your input
이 프로젝트는 입력으로 카메라 데이터만 사용하여 자율주행 자동차 장애물 회피 시스템을 구현해야 합니다
By finishing this course, you will have a good starting point for developing the major elements of the complex perception system needed in self-driving cars
이 과정을 마치면 자율주행 자동차에 필요한 복잡한 인식 시스템의 주요 요소를 개발하기 위한 좋은 출발점을 갖게 될 것입니다
Hopefully you will find this course enjoyable and beneficial for your career, whether you want to become a self-driving car researcher, perception developer, or a system integrator
자율주행 자동차 연구원, 인식 개발자 또는 시스템 통합자가 되고 싶든, 이 과정이 당신의 경력에 즐겁고 유익하기를 바랍니다
It's a great day to build self-driving cars
자율주행 자동차를 만들기에 좋은 날이다


