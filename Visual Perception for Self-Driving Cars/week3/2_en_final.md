In the last lesson, we introduced feed-forward neural networks, a powerful machine learning model
마지막 수업에서, 우리는 강력한 기계 학습 모델인 피드 포워드 신경망을 도입했다
We saw the tasks we would like this model to perform such as object detection, semantic segmentation and depth estimation
우리는 물체 감지, 의미론적 세분화 및 깊이 추정과 같이 이 모델이 수행하기를 원하는 작업을 보았다
In this lesson, we will first review the general process of designing machine-learning algorithms
이 수업에서, 우리는 먼저 기계 학습 알고리즘을 설계하는 일반적인 과정을 검토할 것이다
We will then introduce the missing components still required to define a suitable neural network for a specific perception tasks including the choice of a loss function
그런 다음 손실 기능 선택을 포함한 특정 인식 작업에 적합한 신경망을 정의하는 데 여전히 필요한 누락된 구성 요소를 도입할 것입니다
Let's begin with a general machine learning algorithm design process
일반적인 기계 학습 알고리즘 설계 과정부터 시작합시다
Generally, supervised machine learning models including neural networks have two modes of operation, inference and training
일반적으로, 신경망을 포함한 감독된 기계 학습 모델에는 추론과 훈련의 두 가지 작동 모드가 있다
Recall are basic neural network formulation
리콜은 기본적인 신경망 제형이다
Given a set of parameters data, the input x is passed through the model f of x and data to get an output y
매개 변수 데이터 집합이 주어지면, 입력 x는 출력 y를 얻기 위해 x의 모델 f와 데이터를 통과한다
This mode of operation is called inference, and is usually the one we usually deploy the machine learning algorithms in the real world
이 작동 모드는 추론이라고 불리며, 보통 우리가 보통 현실 세계에 기계 학습 알고리즘을 배포하는 것이다
The network and its parameters are fixed and we use it to extract perception information from new input data
네트워크와 그 매개 변수는 고정되어 있으며 우리는 그것을 사용하여 새로운 입력 데이터에서 인식 정보를 추출합니다
However, we still need to define how to obtain the parameter set data
그러나, 우리는 여전히 매개 변수 세트 데이터를 얻는 방법을 정의해야 한다
Here we need a second mode of operation involving optimization over the network parameters
여기서 우리는 네트워크 매개 변수를 통한 최적화와 관련된 두 번째 작동 모드가 필요합니다
This mode is called training and has the sole purpose of generating a satisfactory parameter set for the task at hand
이 모드는 훈련이라고 불리며 당면한 작업에 대한 만족스러운 매개 변수를 생성하는 유일한 목적을 가지고 있습니다
Let's see how training is usually performed
훈련이 보통 어떻게 수행되는지 봅시다
We start with the same workflow as inference
우리는 추론과 같은 워크플로우로 시작합니다
However, during training we have training data
그러나, 훈련 중에 우리는 훈련 데이터를 가지고 있다
As such we know what f star of x is, the expected output of the model
따라서 우리는 x의 f 별이 무엇인지, 모델의 예상 출력이다
For self-driving, this training data often takes the form of human annotated images which take a long time to produce
자율주행의 경우, 이 훈련 데이터는 종종 생산하는 데 오랜 시간이 걸리는 인간의 주석이 달린 이미지의 형태를 취한다
We compare our inference to a predicted output y, to the true output f star of x, through a loss or a cost function
우리는 손실이나 비용 함수를 통해 추론을 예측된 출력 y, x의 실제 출력 f 별과 비교합니다
The loss function takes as an input the predicted output y from the network, and the true output f star of x, and provides a measure of the difference between the two
손실 함수는 네트워크에서 예측된 출력 y와 x의 진정한 출력 f 별을 입력으로 취하고, 둘 사이의 차이의 척도를 제공한다
We usually try to minimize this measure by modifying the parameters data so that the output y from the network is as similar as possible to the f star of x
우리는 보통 네트워크의 출력 y가 x의 f 별과 가능한 한 유사하도록 매개 변수 데이터를 수정하여 이 측정을 최소화하려고 노력합니다
We do this modification to data via an optimization procedure
우리는 최적화 절차를 통해 데이터에 대한 이 수정을 수행합니다
This optimization procedure takes in the output of the loss function and provides a new set of parameters data that provide a lower value for that loss function
이 최적화 절차는 손실 함수의 출력을 취하고 손실 함수에 대해 더 낮은 값을 제공하는 새로운 매개 변수 데이터 세트를 제공합니다
We will learn about this optimization process in detail during the next lesson
우리는 다음 수업에서 이 최적화 과정에 대해 자세히 배울 것이다
But for now, let's extend the design process to neural networks
하지만 지금은 설계 과정을 신경망으로 확장합시다
We discussed in the last lesson a feed-forward neural network which takes an input x, passes it through a sequence of hidden layers, then passes the output of the hidden layers through an output layer
우리는 마지막 수업에서 입력 x를 취하고 숨겨진 레이어의 시퀀스를 통과한 다음, 출력 레이어를 통해 숨겨진 레이어의 출력을 전달하는 피드 포워드 신경망에 대해 논의했습니다
This is the end of the inference stage of the neural network
이것은 신경망의 추론 단계의 끝이다
For training, we pass the predicted output through the loss function, then use an optimization procedure to produce a new set of parameters data that provide a lower value for the loss function
훈련을 위해, 우리는 손실 함수를 통해 예측된 출력을 전달한 다음 최적화 절차를 사용하여 손실 함수에 대해 더 낮은 값을 제공하는 새로운 매개 변수 데이터 세트를 생성합니다
The major difference between the design of traditional machine learning algorithms in the design of artificial neural networks, is that the neural network only interacts with the loss function via the output layer
인공 신경망 설계에서 전통적인 기계 학습 알고리즘 설계의 주요 차이점은 신경망이 출력 계층을 통해서만 손실 기능과 상호 작용한다는 것이다
Therefore, it is quite reasonable that the output layer and the loss function are designed together depending on the task at hand
따라서, 출력 레이어와 손실 기능이 당면한 작업에 따라 함께 설계되는 것은 매우 합리적이다
Let's dig deeper into the major perception tasks we usually encounter in autonomous driving
자율주행에서 보통 마주치는 주요 인식 작업을 더 깊이 파고들자
The first important task that we use for autonomous driving perception is classification
자율주행 인식에 사용하는 첫 번째 중요한 과제는 분류이다
Classification can be described as taking an input x and mapping it to one of k classes or categories
분류는 입력 x를 취하고 k 클래스나 카테고리 중 하나에 매핑하는 것으로 설명될 수 있다
Examples include, image classification, where we just want to map an image to a particular category, to say whether or not it contains cats or dogs for example and semantic segmentation where we want to map every pixel in the image to a category
예를 들어, 이미지를 특정 범주에 매핑하려는 이미지 분류, 예를 들어 고양이나 개가 포함되어 있는지 여부와 이미지의 모든 픽셀을 카테고리에 매핑하려는 의미론적 세분화가 있습니다
The second task that we usually use for autonomous driving perception is a regression
우리가 보통 자율주행 인식에 사용하는 두 번째 작업은 회귀이다
In regression, we want to map inputs to a set of real numbers
회귀에서, 우리는 입력을 실수 집합에 매핑하고 싶습니다
Examples of regression include, depth estimation, where we want to estimate a real depth value for every pixel in an image
회귀의 예로는 이미지의 모든 픽셀에 대한 실제 깊이 값을 추정하려는 깊이 추정이 있습니다
We can also mix the two tasks together
우리는 또한 두 과제를 함께 섞을 수 있다
For example, object detection is usually comprised of a regression task where we estimate the bounding box that contains an object and a classification task where we identify which type of object is in the bounding box
예를 들어, 객체 탐지는 일반적으로 객체가 포함된 경계 상자와 경계 상자에 있는 객체 유형을 식별하는 분류 작업을 추정하는 회귀 작업으로 구성됩니다
We will now describe the output layer loss function pairs associated with each of these basic perception tasks
이제 이러한 기본 인식 작업 각각과 관련된 출력 계층 손실 함수 쌍을 설명할 것입니다
Let's start with the classification task first
먼저 분류 작업부터 시작하겠습니다
Usually, for a k class classification tasks, we use the softmax output layer
보통, k 클래스 분류 작업의 경우, 우리는 softmax 출력 레이어를 사용합니다
Softmax output layers are capable of representing a probability distribution over k classes
소프트맥스 출력 레이어는 k 클래스에 대한 확률 분포를 나타낼 수 있다
The softmax output layer takes as input h, the output of the last hidden layer of the neural network
소프트맥스 출력 레이어는 신경망의 마지막 숨겨진 레이어의 출력인 입력 h로 취한다
It then passes it through an affine transformation resulting in a transformed output vector z
그런 다음 아핀 변환을 통해 변환된 출력 벡터 z를 생성합니다
Next, the vector z is transformed into a discrete probability distribution using the softmax element-wise function
다음으로, 벡터 z는 softmax 요소별 함수를 사용하여 이산 확률 분포로 변환됩니다
For each element z_i, this function computes the ratio of the exponential of element z_i over the sum of the exponentials of all of the elements of z
각 요소 z_i에 대해, 이 함수는 z의 모든 요소의 지수 합에 대한 요소 z_i의 지수 비율을 계산한다
The result is a value between zero and one and the sum of all of these elements is one, making it a proper probability distribution
결과는 0과 1 사이의 값이며 이 모든 요소의 합은 하나이며, 적절한 확률 분포이다
Let's take a look at a numerical example to better explain the softmax output layer
Softmax 출력 레이어를 더 잘 설명하기 위해 숫자 예를 살펴보겠습니다
In this example, we'd like to classify images containing a cat, a dog or a fox
이 예에서는 고양이, 개 또는 여우가 포함된 이미지를 분류하고 싶습니다
First we define the first element of our output vector to correspond to the probability that the image is a cat according to our network
먼저 우리는 네트워크에 따라 이미지가 고양이일 확률에 대응하도록 출력 벡터의 첫 번째 요소를 정의합니다
The ordering of classes is arbitrary and has no impact on network performance
클래스의 순서는 임의적이며 네트워크 성능에 영향을 미치지 않습니다
Taking the output of the affine transformation, we compute the probability by dividing the exponential of each elements of the output by the sum of the exponentials of all of the elements
아핀 변환의 출력을 취하여 출력의 각 요소의 지수를 모든 요소의 지수 합으로 나누어 확률을 계산합니다
Given values of 13 minus seven and 11 as the outputs of the linear transformation layer, we achieve a probability of 88 percent that this image is a cat, 11
선형 변환 층의 출력으로 13 마이너스 7 및 11의 값을 감안할 때, 우리는 이 이미지가 고양이일 확률이 88%, 이 이미지가 여우이고 이 이미지가 개일 확률이 매우 낮습니다
9 percent that this image is a fox and a very low probability that this image is a dog
이제, 우리의 추정치가 얼마나 정확한지 보여주기 위해 softmax 출력 레이어의 출력을 사용하는 손실 함수를 설계하는 방법을 봅시다
Now, let's see how to design a loss function that uses the output of the softmax output layer to show us how accurate our estimate is
Softmax 출력 레이어와 함께 사용할 표준 손실 함수는 softmax 함수의 음수 로그를 사용하여 형성되는 Cross-Entropy Loss입니다
The standard loss function to be used with the softmax output layer is the Cross-Entropy Loss, which is formed by taking the negative log of the softmax function
교차 엔트로피 손실에는 네트워크의 출력이 실제 확률에 얼마나 가까운지 제어하는 두 가지 용어가 있다
The Cross-Entropy Loss has two terms to control how close the output of the network is to the true probability
Z_i는 softmax 함수를 통과하기 전에 true 클래스에 해당하는 숨겨진 레이어의 출력이다
Z_i is the output of the hidden layer corresponding to the true class before being passed through the softmax function
이것은 보통 로지스틱 회귀 분야에서 나오는 클래스 로지트라고 불린다
This is usually called the class logit which comes from the field of logistic regression
이 손실 함수를 최소화할 때, 클래스 logit z_i의 음수는 네트워크가 올바른 클래스의 확률에 대해 큰 값을 출력하도록 장려한다
When minimizing this loss function, the negative of the class logit z_i encourages the network to output a large value for the probability of the correct class
반면에 두 번째 용어는 아핀 변환의 생산량이 작도록 장려한다
The second term on the other hand, encourages the output of the affine transformation to be small
두 용어는 네트워크가 예측된 클래스 확률과 실제 클래스 확률의 차이를 최소화하도록 장려한다
The two terms together encourages the network to minimize the difference between the predicted class probabilities and the true class probability
이 손실을 더 잘 이해하기 위해
To understand this loss better
교차 엔트로피 손실이 분류 신경망의 출력에서 어떻게 계산되는지에 대한 수치적 예를 살펴보겠습니다
Let's take a look at a numerical example on how the Cross-Entropy Loss is computed from the output of a classification neural network
이전 예시를 재검토하면서, 우리는 먼저 z 서브 i가 무엇인지 선택해야 합니다
Revisiting our previous example, we first need to choose what our z sub i is
Z 서브 i는 진정한 입력 클래스에 해당하는 선형 변환 출력이다
Z sub i is the linear transformation output corresponding to the true class of inputs
이 경우, z_i는 cat 클래스에 해당하는 선형 변환 출력 요소이다
In this case, z_i is the element of the output of the linear transformation corresponding to the cat class
Z 하위 i를 결정하면, 교차 엔트로피를 사용하여 최종 손실 값을 계산합니다
Once we determine z sub i, we use the Cross-Entropy to compute the final loss value
이 경우, 네트워크는 입력이 고양이임을 올바르게 예측하고 0
In this case, the network correctly predicts that the input is a cat and sees a loss function value of 0
12의 손실 함수 값을 본다
12
이제 잘못된 네트워크 출력으로 계산을 다시 합시다
Let us now do the computation again but with an erroneous network output
네트워크에 대한 입력은 여전히 고양이 이미지이다
The input to the network is still a cat image
네트워크는 여전히 선형 변환 출력의 고양이 항목에 13의 값을 할당한다
The network still assigns the value of 13 to the cat entry of the output of the linear transformation
하지만 이번에는 여우 항목은 14의 값을 얻을 것이다
But this time the fox entry will get a value of 14
교차 엔트로피 손실을 계산하면 이전 슬라이드의 값의 10배 이상 1
Computing the Cross-Entropy Loss, we find that it evaluates to 1
31로 평가된다는 것을 발견했습니다
31 more than ten times the value of the previous slide
손실 함수가 출력의 차이가 하나일 때에도 잘못된 예측에 얼마나 큰 불이익을 주는지 주목하세요
Note how the loss function heavily penalizes erroneous predictions even when the difference in output is only one
이러한 차이는 학습 과정을 가속화하고 교육 중에 네트워크 출력을 진정한 가치로 빠르게 조정합니다
This difference accelerates the learning process and rapidly steers network outputs to the true values during training
지금까지 우리는 분류 작업과 관련된 출력 계층과 손실 함수를 제시했습니다
So far we've presented an output layer and loss functions specific to the classification task
이제 회귀 작업을 위한 가장 일반적인 출력 계층을 살펴보겠습니다
Let's now go through the most common output layer for the regression task
선형 출력 계층은 주로 공통 확률 분포의 통계를 모델링하는 회귀 작업에 사용된다
The linear output layer is mostly used for regression tasks to model statistics of common probability distributions
선형 출력 계층은 단순히 비선형성 없이 단일 아핀 변환으로 구성되어 있다
The linear output layer is simply comprised of a single affine transformation without any non-linearity
선형 출력 레이어로 모델링할 통계는 우리가 선택한 손실 함수에 따라 다릅니다
The statistics to be modeled with the linear output layer depends on the loss function we choose to go with it
예를 들어, 확률 분포의 평균을 모델링하기 위해, 우리는 평균 제곱 오류를 손실 함수로 사용합니다
For example, to model the mean of a probability distribution, we use the mean squared error as our loss function
위에서 설명한 선형 및 소프트맥스 출력 장치는 오늘날 신경망에서 사용되는 가장 일반적인 출력 계층이며 자율주행을 위한 다양한 유용한 인식 작업을 수행하기 위해 다양한 작업별 손실 기능과 결합될 수 있습니다
The linear and softmax output units described above are the most common output layers used in neural networks today and can be coupled with a variety of tasks specific loss functions to perform a variety of useful perception tasks for autonomous driving
다른 많은 출력 계층과 손실 기능이 존재하며 이것은 딥 러닝에서 활발한 연구 영역으로 남아있다
Many other output layers and loss functions exist and this remains an active area of research in deep learning
이 수업에서는 기계 학습 모델을 구축하려면 네트워크 모델, 손실 기능 및 네트워크 매개 변수를 배우기 위한 최적화 절차를 정의해야 한다는 것을 배웠습니다
In this lesson, you learned that to build a machine learning model you need to define a network model, a loss function and an optimization procedure to learn the network parameters
또한 신경망 모델이 수행해야 하는 작업에 따라 어떤 손실 기능을 선택해야 하는지 배웁니다
You also learn what loss function to choose based on the task that needs to be done by the neural network model
다음 비디오에서, 우리는 신경망 설계 프로세스의 최종 구성 요소에 대해 논의할 것입니다; 특정 작업에 가장 적합한 매개 변수 세트 데이터를 얻는 방법을 포함하는 최적화
In the next video, we will be discussing the final components of our neural network design process; optimization, which involves how to get the best parameter set data for a specific task
다음에 보자
See you next time



