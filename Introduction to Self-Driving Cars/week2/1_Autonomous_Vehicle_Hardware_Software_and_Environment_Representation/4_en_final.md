[MUSIC] [MUSIC] In this lesson we'll take a closer look at the maps created to represent the environment around our car
[음악] [음악] 이 수업에서 우리는 자동차 주변 환경을 나타내기 위해 만들어진 지도를 자세히 살펴볼 것입니다
I'll present an overview of the three different map types traditionally used for autonomous driving, which you saw briefly in the previous video
이전 비디오에서 간략하게 본 자율주행에 전통적으로 사용된 세 가지 지도 유형에 대한 개요를 제시하겠습니다
Then I'll give you a more detailed explanation about each of the maps so you can better understand How they're created and used throughout the specialization
그런 다음 전문 분야 전반에 걸쳐 어떻게 만들어지고 사용되는지 더 잘 이해할 수 있도록 각 지도에 대해 더 자세히 설명하겠습니다
The first map we will discuss is the localization map
우리가 논의할 첫 번째 지도는 현지화 지도이다
This map is created using a continuous set of lidar points or camera image features as the car moves through the enviromment
이 지도는 자동차가 환경을 통과할 때 지속적인 라이더 포인트 또는 카메라 이미지 기능을 사용하여 만들어집니다
This map is then used in combination with GPS, IMU and wheel odometry by the localization module To accurately estimate the precise location of the vehicle at all times
그런 다음 이 지도는 항상 차량의 정확한 위치를 정확하게 추정하기 위해 현지화 모듈에 의해 GPS, IMU 및 휠 거리계와 함께 사용됩니다
The second map is the occupancy grid map
두 번째 지도는 점유 그리드 지도이다
The occupancy grid also uses a continuous set of LIDAR points to build a map of the environment which indicates the location of all static, or stationary, obstacles
점유 그리드는 또한 연속적인 LIDAR 포인트 세트를 사용하여 모든 정적 또는 고정식 장애물의 위치를 나타내는 환경 지도를 구축합니다
This map is used to plan safe, collision-free paths for the autonomous vehicle
이 지도는 자율주행 차량을 위한 안전하고 충돌 없는 경로를 계획하는 데 사용됩니다
The third and final map that we'll discuss in this video is the detailed road map
이 비디오에서 논의할 세 번째이자 마지막 지도는 상세한 로드맵입니다
It contains detailed positions for all regulatory elements, regulatory attributes and lane markings
여기에는 모든 규제 요소, 규제 속성 및 차선 표시에 대한 자세한 위치가 포함되어 있습니다
This map is used to plan a path from the current position to the final destination
이 지도는 현재 위치에서 최종 목적지까지의 경로를 계획하는 데 사용됩니다
Let's take a closer look at the localization map
현지화 지도를 자세히 살펴보자
As I mentioned previously, the localization map uses recorded LIDAR points or images, which are combined to make a point cloud representation of the environment
앞서 언급했듯이, 현지화 맵은 기록된 LIDAR 포인트나 이미지를 사용하여 환경을 포인트 클라우드로 표현합니다
As new LIDAR camera data is received it is compared to the localization map and a measurement of the eagle vehicles position is created by aligning the new data with the existing map
새로운 LIDAR 카메라 데이터가 수신되면 현지화 지도와 비교되며 새 데이터를 기존 지도와 정렬하여 독수리 차량 위치 측정이 생성됩니다
This measurement is then combined with other sensors to estimate eagle motion and ultimately used to control the vehicle Here we have some recorded LIDAR data from our self-driving car
그런 다음 이 측정은 다른 센서와 결합하여 독수리 움직임을 추정하고 궁극적으로 차량을 제어하는 데 사용됩니다
The movement of the vehicle is clear based on the evolution of the LIDAR points in this video
여기에 자율주행 자동차에서 기록된 LIDAR 데이터가 있습니다
As the car drives out of a driveway and onto the street ahead
차량의 움직임은 이 비디오의 LIDAR 포인트의 진화를 기반으로 명확하다
This detailed evolving representation of the motion of a car through its environment Is extremely valuable for the localization module
차가 진입로에서 나와 앞으로 거리로 운전할 때
The localization map can be quite large, and many methods exist to compress it's contents and keep only those features that are needed for localization
환경을 통한 자동차의 움직임에 대한 상세한 진화하는 표현은 현지화 모듈에 매우 가치가 있다
The construction of this map will be more rigorously explained in the next course of this specialization
현지화 맵은 꽤 클 수 있으며, 내용을 압축하고 현지화에 필요한 기능만 유지하는 많은 방법이 존재합니다
Where we discuss localization in detail
이 지도의 건설은 이 전문 분야의 다음 과정에서 더 엄격하게 설명될 것이다
The occupancy grid is a 2D or 3D discretized map of the static objects in the environments surrounding the eagle vehicle
현지화에 대해 자세히 논의하는 곳
This map is created to identify all static objects around the autonomous car, once again, using point clouds as our input
점유 그리드는 독수리 차량을 둘러싼 환경에서 정적 물체의 2D 또는 3D 이산 지도이다
The objects which are classified as static include trees, buildings, curbs, and all other nondriveable surfaces
이 지도는 포인트 클라우드를 입력으로 사용하여 자율주행차 주변의 모든 정적 물체를 다시 한 번 식별하기 위해 만들어졌습니다
For example, in this grid map, if all occupied grids were colored in, this is what the occupancy grid may look like
정적으로 분류되는 물체는 나무, 건물, 연석 및 기타 모든 비동할 수 없는 표면을 포함한다
As the occupancy grid only represents the static objects from the environment, all dynamic objects must first be removed
예를 들어, 이 그리드 지도에서, 점유된 모든 그리드가 채색되었다면, 점유 그리드는 이렇게 보일 수 있다
This is done by removing all lidar points that are found within the bounding boxes of detected dynamic objects identified by the perception stack
점유 그리드는 환경의 정적 객체만 나타내기 때문에, 모든 동적 객체는 먼저 제거되어야 합니다
Next, static objects which will not interfere with the vehicle are also removed
이것은 인식 스택으로 식별된 감지된 동적 물체의 경계 상자 내에서 발견되는 모든 라이더 포인트를 제거함으로써 수행됩니다
Such as dryable service or any over hanging tree branches
다음으로, 차량을 방해하지 않는 정적 물체도 제거됩니다
As result of these steps only the relevent writer points from static objects from the environment remain
건조 가능한 서비스나 매달린 나뭇가지와 같은 것
The filtering process is not perfect and so it is not possible to blindly trust the remaining points are in fact obstacles The occupancy grid, therefore, represents the environment probabilistically, by tracking the likelihood that a grid cells occupy over time
이 단계의 결과로 환경의 정적 객체에서 방출되는 작성자 포인트만 남아있다
This map is then relied on to create paths for the vehicle which are collusion-free
필터링 프로세스는 완벽하지 않으므로 나머지 지점이 실제로 장애물이라고 맹목적으로 신뢰할 수 없습니다
Both the creation of this map and its application to the local planning problem will be covered in much greater detail
따라서 점유 그리드는 그리드 셀이 시간이 지남에 따라 점유할 가능성을 추적함으로써 확률적으로 환경을 나타냅니다
In course four of the specialization
그런 다음 이 지도는 공모가 없는 차량의 경로를 만들기 위해 의존한다
Let's look at an example of an occupancy grid updating over time
이 지도의 생성과 지역 계획 문제에 대한 적용은 훨씬 더 자세히 다루어질 것이다
Here, we see the occupancy grid visualized as the light gray square area, under the autonomous car
물론 네 가지 전문 분야
Updating the position of static objects in the environment with black squares
시간이 지남에 따라 업데이트되는 점유 전력망의 예를 살펴보겠습니다
As the autonomous car moves through the environment, all stationary objects in the environment such as poles, buildings, and parked cars, are shown as occupied grid cells
여기서, 우리는 자율주행차 아래의 밝은 회색 정사각형 영역으로 시각화된 점유망을 본다
Finally, the detailed roadmap is a map of the full road network which can be driven by the self-driving car
검은색 사각형으로 환경에서 정적 물체의 위치를 업데이트합니다
This map contains information regarding the lanes of a road, as well as any traffic regulation elements which may affect them
자율주행차가 환경을 통과함에 따라, 기둥, 건물 및 주차된 자동차와 같은 환경의 모든 고정 물체는 점유된 그리드 셀로 표시됩니다
The detailed road map is used to plan a safe and efficient path to be taken by the self-driving car
마지막으로, 상세한 로드맵은 자율주행 자동차가 운전할 수 있는 전체 도로 네트워크의 지도이다
The detailed road map can be created in one of three ways
이 지도에는 도로의 차선에 관한 정보와 영향을 미칠 수 있는 교통 규제 요소가 포함되어 있습니다
Fully online, fully offline, or created offline and updated online
상세한 도로 지도는 자율주행차가 취할 안전하고 효율적인 경로를 계획하는 데 사용됩니다
A map which is created fully online relies heavily on the static object proportion of the perception stack to accurately label and correctly localize all relevant static objects to create the map
상세한 로드맵은 세 가지 방법 중 하나로 만들 수 있다
This includes all lane boundaries in the current driving environment, any regulation elements, such as traffic lights or traffic signs, any regulation attributes of the lanes, such as right turn markings or crosswalks
완전 온라인, 완전 오프라인 또는 오프라인으로 생성되고 온라인으로 업데이트됩니다
This method of map creation is rarely used due to the complexity of creating such a map in real time
완전히 온라인으로 생성된 맵은 인식 스택의 정적 객체 비율에 크게 의존하여 모든 관련 정적 객체에 정확하게 라벨을 붙이고 올바르게 현지화하여 지도를 만듭니다
A map which is created entirely offline is usually done by collecting data of a given road several times
여기에는 현재 운전 환경의 모든 차선 경계, 신호등이나 교통 표지판과 같은 규제 요소, 우회전 표시 또는 횡단보도와 같은 차선의 규제 속성이 포함됩니다
Specialized vehicles with high accuracy sensors are driven along roadways regularly to construct offline maps
이 지도 생성 방법은 실시간으로 그러한 지도를 만드는 복잡성으로 인해 거의 사용되지 않습니다
Once the collection is complete, the information is then labelled with the use of a mixture of automatic labelling from static object perception and human annotation and correction
완전히 오프라인으로 만들어진 지도는 보통 주어진 도로의 데이터를 여러 번 수집하여 수행됩니다
This method of map creation, while producing very detailed and accurate maps, is unable to react or adapt to a changing environment
고정밀 센서가 장착된 특수 차량은 오프라인 지도를 구성하기 위해 정기적으로 도로를 따라 구동됩니다
The third method of creating detailed roadmaps is to create them offline and then update them online with new, relevant information
컬렉션이 완료되면, 정보는 정적 물체 인식과 인간 주석 및 보정에서 자동 라벨링의 혼합물로 표시됩니다
This method of map creation takes advantage of both methods, creating a highly accurate roadmap which can be updated while driving
이 지도 생성 방법은 매우 상세하고 정확한 지도를 생성하면서 변화하는 환경에 반응하거나 적응할 수 없습니다
In course four on motion planning, we will present a method for storing all of the information present in a detailed roadmap called the lane length model
자세한 로드맵을 만드는 세 번째 방법은 오프라인으로 만든 다음 새로운 관련 정보로 온라인으로 업데이트하는 것입니다
Let's look at an example of a detailed roadmap
이 지도 생성 방법은 두 가지 방법을 모두 활용하여 운전 중에 업데이트할 수 있는 매우 정확한 로드맵을 만듭니다
As you can see, the lane boundaries of the detailed roadmap are visualized in red Along with the boundaries, the center of each lane is also visualized in red
모션 계획에 관한 코스 4에서, 우리는 차선 길이 모델이라는 상세한 로드맵에 존재하는 모든 정보를 저장하는 방법을 제시할 것이다
This information is vitally important for path-following as it provides a default path along the lane
자세한 로드맵의 예를 살펴보자
As you can see in this video the vehicle, while autonomously driving, neatly follows the center of the lane
보시다시피, 상세한 로드맵의 차선 경계는 빨간색으로 시각화됩니다
That completes our discussion of mapping for self-driving cars
경계와 함께 각 차선 중앙도 빨간색으로 시각화됩니다
In this video, you learned about three types of maps commonly used for autonomous driving: The localization map, the occupancy grid, and the detailed road map
이 정보는 차선을 따라 기본 경로를 제공하기 때문에 경로를 따르는 데 매우 중요합니다
You'll study each of these map types further as we dive into localization, collision avoidance, and motion planning In the remaining courses of the specialization
이 비디오에서 볼 수 있듯이, 차량은 자율적으로 운전하는 동안 차선 중앙을 깔끔하게 따라가세요
Congratulations, you completed the second module in this introduction to self-driving cars course
그것은 자율주행 자동차 매핑에 대한 우리의 논의를 완성한다
In this module, you learned how to select sensing and computing hardware in self-driving car, how to design specific sensors [INAUDIBLE] based on the requirements of driving
이 비디오에서는 자율주행에 일반적으로 사용되는 세 가지 유형의 지도에 대해 배웠습니다: 현지화 지도, 점유 그리드 및 상세한 로드맵
How to decompose the software system for autonomous driving
전문화의 나머지 과정에서 현지화, 충돌 회피 및 모션 계획에 뛰어들면서 이러한 각 지도 유형을 더 연구할 것입니다
And what the three main types of maps are that represent the environment
축하합니다, 당신은 자율주행 자동차 코스에 대한 이 소개에서 두 번째 모듈을 완료했습니다
In the next module, we will take a closer look at the vehicle modeling for the purpose of precision control
이 모듈에서는 자율주행 자동차에서 감지 및 컴퓨팅 하드웨어를 선택하는 방법, 운전 요구 사항에 따라 특정 센서 [INAUDIBLE]를 설계하는 방법을 배웠습니다
I'll see you in the next module
자율주행을 위해 소프트웨어 시스템을 분해하는 방법
[SOUND]
그리고 환경을 대표하는 세 가지 주요 유형의 지도가 무엇인지

다음 모듈에서는 정밀 제어를 목적으로 차량 모델링을 자세히 살펴볼 것입니다

다음 모듈에서 뵙겠습니다

[소리]
