[MUSIC] [SOUND] [MUSIC] Hello and welcome to Week 3 of the course
[음악] [소리] [음악] 안녕하세요 그리고 코스의 3주차에 오신 것을 환영합니다
This week, you will learn about a topic that has changed the way we think about autonomous perception, artificial neural networks
이번 주에, 당신은 자율 인식, 인공 신경망에 대해 생각하는 방식을 바꾼 주제에 대해 배우게 될 것입니다
Throughout this module, you will learn how these algorithms can be used to build a self-driving car perception stack, and you'll learn the different components to design and train a deep neural network
이 모듈을 통해 이러한 알고리즘을 사용하여 자율주행 자동차 인식 스택을 구축하는 방법을 배우게 되며, 심층 신경망을 설계하고 훈련시키는 다양한 구성 요소를 배우게 됩니다
Now we won't be able to teach you everything you need to know about artificial neural networks, but this module is a good introduction to the field
이제 인공 신경망에 대해 알아야 할 모든 것을 가르칠 수는 없지만, 이 모듈은 이 분야에 대한 좋은 소개입니다
If artificial neural networks is a topic that you're interested in, feel free to check out some of the deep learning and machine learning courses offered on Coursera
인공 신경망이 관심 있는 주제라면, Coursera에서 제공되는 딥 러닝 및 기계 학습 과정을 자유롭게 확인하세요
In this lesson, you will learn about the building blocks of feedforward neural networks, a very useful basic type of artificial neural network
이 수업에서는 매우 유용한 기본 유형의 인공 신경망인 피드포워드 신경망의 구성 요소에 대해 배우게 됩니다
Specifically, we'll look at the hidden layers of a feedforward neural network
특히, 우리는 피드포워드 신경망의 숨겨진 층을 살펴볼 것이다
The hidden layers are important, as they differentiate the mode of action of neural networks from the rest of machine learning algorithms
숨겨진 계층은 신경망의 행동 방식을 나머지 기계 학습 알고리즘과 구별하기 때문에 중요하다
We'll begin by looking at the mathematical definition of feedforward neural networks, so you can start to understand how to build these algorithms for the perception stack
피드포워드 신경망의 수학적 정의를 살펴보는 것으로 시작하겠습니다
A feedforward neural network defines a mapping from an input x to an output y through a function f of x and theta
그래서 당신은 인식 스택을 위해 이러한 알고리즘을 구축하는 방법을 이해하기 시작할 수 있습니다
For example, we use neural networks to produce outputs such as the location of all cars in a camera image
피드포워드 신경망은 x와 세타의 함수 f를 통해 입력 x에서 출력 y로의 매핑을 정의한다
The function f takes an input x, and uses a set of learned parameters theta, to interact with x, resulting in the output y
예를 들어, 우리는 신경망을 사용하여 카메라 이미지의 모든 자동차의 위치와 같은 출력을 생성합니다
The concept of learned parameters is important here, as we do not start with the correct form of the function f, which maps our inputs to our outputs directly
함수 f는 입력 x를 취하고, 학습된 매개 변수 세타 세트를 사용하여 x와 상호 작용하여 출력 y를 생성합니다
Instead, we must construct an approximation to the true function using a generic neural network
학습된 매개 변수의 개념은 입력을 출력에 직접 매핑하는 함수 f의 올바른 형태로 시작하지 않기 때문에 여기서 중요합니다
This means that neural networks can be thought of as function approximators
대신, 우리는 일반적인 신경망을 사용하여 실제 기능에 대한 근사치를 구성해야 한다
Usually we describe a feedforward neural network as a function composition
이것은 신경망이 기능 근사치로 생각할 수 있다는 것을 의미한다
In a sense, each function f of i is a layer on top of the previous function, f of i- 1
보통 우리는 피드포워드 신경망을 기능 구성으로 묘사한다
Usually we have N functions in our compositions where N is a large number, stacking layer upon layer for improved representation
어떤 의미에서, i의 각 함수 f는 이전 함수 위에 있는 레이어이며, i- 1의 f이다
This layering led to the name deep learning for the field describing these sequences of functions
보통 우리는 N이 많은 숫자인 구성에 N 함수를 가지고 있으며, 향상된 표현을 위해 레이어 위에 층을 쌓는다
Now let us describe this function composition visually
이 레이어링은 이러한 함수 시퀀스를 설명하는 분야의 딥 러닝이라는 이름으로 이어졌다
Here you can see a four-layer feedforward neural network
이제 이 기능 구성을 시각적으로 설명합시다
This neural network has an input layer which describes the data input x to the function approximator
여기서 4층 피드포워드 신경망을 볼 수 있습니다
Here x can be a scalar, a vector, a matrix or even a n-dimensional tensor such as images
이 신경망에는 함수 근사치에 대한 데이터 입력 x를 설명하는 입력 계층이 있다
The input gets processed by the first layer of the neural network, the function f1 of x
여기서 x는 스칼라, 벡터, 매트릭스 또는 이미지와 같은 n차원 텐서가 될 수 있습니다
We call this layer the first hidden layer
입력은 신경망의 첫 번째 계층인 x의 함수 f1에 의해 처리된다
Similarly, the second hidden layer processes the output of the first hidden layer through the function f2 of x
우리는 이 레이어를 첫 번째 숨겨진 레이어라고 부른다
We can add as many hidden layers as we'd like, but each layer adds additional parameters to be learned, and more computations to be performed at run time
마찬가지로, 두 번째 숨겨진 레이어는 x의 함수 f2를 통해 첫 번째 숨겨진 레이어의 출력을 처리합니다
We will discuss how the number of hidden layers affects the performance of our system later on in the course
원하는 만큼 숨겨진 레이어를 추가할 수 있지만, 각 레이어는 배울 추가 매개 변수와 런타임에 수행할 더 많은 계산을 추가합니다
The final layer of the neural network is called the output layer
우리는 나중에 숨겨진 레이어의 수가 우리 시스템의 성능에 어떤 영향을 미치는지 논의할 것이다
It takes the output of the last hidden layer and transforms it to a desired output Y
신경망의 최종 계층은 출력 계층이라고 불린다
Now, we should have the intuition on why these networks are called feedforward
마지막 숨겨진 레이어의 출력을 가져와 원하는 출력 Y로 변환합니다
This is because information flows from the input x through some intermediate steps, all the way to the output Y without any feedback connections
이제, 우리는 왜 이 네트워크들이 피드포워드라고 불리는지에 대한 직감을 가져야 한다
The terms are used in the same way as we use them in Course 1, when describing control for our self-driving car
이것은 정보가 입력 x에서 몇 가지 중간 단계를 거쳐 피드백 연결 없이 출력 Y까지 흐르기 때문입니다
Now let us go back to the network definition and check out how our visual representation matches our function composition
이 용어는 자율주행 자동차에 대한 통제를 설명할 때 코스 1에서 사용하는 것과 같은 방식으로 사용됩니다
In this expression we see x, which is called the input layer
이제 네트워크 정의로 돌아가서 시각적 표현이 함수 구성과 어떻게 일치하는지 확인해 봅시다
We see the outer most function f sub N, which is the output layer
이 표현식에서 우리는 입력 레이어라고 불리는 x를 본다
And we see each of the functions f1 to f N-1 in between, which are the hidden layers
우리는 출력 레이어인 가장 바깥쪽 함수 f 서브 N을 본다
Now before we delve deeper into these fascinating function approximators, let's look at a few examples of how we can use them for autonomous driving
그리고 우리는 숨겨진 레이어인 f1에서 f N-1 사이의 각 함수를 본다
Remember, this course is on visual perception, so we'll restrict our input x to always be an image
이제 이러한 매혹적인 기능 근사치를 더 깊이 탐구하기 전에 자율주행에 어떻게 사용할 수 있는지에 대한 몇 가지 예를 살펴보겠습니다
The most basic perception task is that of classification
기억하세요, 이 과정은 시각적 인식에 관한 것이므로, 우리는 입력 x를 항상 이미지로 제한할 것입니다
Here we require the neural network to tell us what is in the image via a label
가장 기본적인 인식 작업은 분류 작업이다
We can make this task more complicated by trying to estimate a location as well as a label for objects in the scene
여기서 우리는 신경망이 라벨을 통해 이미지에 무엇이 있는지 알려주도록 요구한다
This is called object detection
우리는 장면의 물체에 대한 라벨뿐만 아니라 위치를 추정함으로써 이 작업을 더 복잡하게 만들 수 있다
Another set of tasks we might be interested in are pixel-wise tasks
이것은 물체 감지라고 불린다
As an example we might want to estimate a depth value for every pixel in the image
우리가 관심을 가질 수 있는 또 다른 작업 세트는 픽셀별 작업이다
This will help us determine where objects are
예를 들어 이미지의 모든 픽셀에 대한 깊이 값을 추정할 수 있습니다
Or, we might want to determine which class each pixel belongs to
이것은 우리가 물체가 어디에 있는지 결정하는 데 도움이 될 것이다
This task is called semantic segmentation, and we'll discuss this in depth along with object detection later in the course
또는 각 픽셀이 어떤 클래스에 속하는지 결정하고 싶을 수도 있습니다
In each case, we can use a neural network to learn the complex mapping between the raw pixel values from the image to the perception outputs we're trying to generate, without having to explicitly model how that mapping works
이 작업은 의미론적 세분화라고 불리며, 우리는 과정의 뒷부분에서 물체 감지와 함께 이것을 깊이 논의할 것입니다
This flexibility to represent hard-to-model processes is what makes neural networks so popular
각각의 경우, 우리는 신경망을 사용하여 매핑이 어떻게 작동하는지 명시적으로 모델링하지 않고도 이미지에서 생성하려는 인식 출력에 이르기까지 원시 픽셀 값 사이의 복잡한 매핑을 배울 수 있습니다
Now let's take a look at how to learn the parameters needed to create robust perception models
모델화하기 어려운 프로세스를 나타내는 이러한 유연성은 신경망을 매우 인기 있게 만드는 것이다
During a process referred to as Neural Network Training, we drive the neural network function f of (x) and theta to match a true function f*(x) by modifying the parameters theta that describe the network
이제 강력한 인식 모델을 만드는 데 필요한 매개 변수를 배우는 방법을 살펴보겠습니다
The modification of theta is done by providing the network pairs of input x and its corresponding true out output f*(x)
신경망 훈련이라고 불리는 과정에서, 우리는 네트워크를 설명하는 매개 변수 세타를 수정하여 (x)의 신경망 함수 f와 세타를 실제 함수 f*(x)와 일치시킵니다
We can then compare the true output to the output produced by the network and optimize the network parameters to reduce the output error
세타의 수정은 입력 x의 네트워크 쌍과 그에 상응하는 true 출력 f*(x)를 제공함으로써 수행됩니다
Since only the output of the neural network is specified for each example, the training data does not specify what the network should do with its hidden layers
그런 다음 실제 출력을 네트워크에서 생성된 출력과 비교하고 네트워크 매개 변수를 최적화하여 출력 오류를 줄일 수 있습니다
The network itself must decide how to modify these layers to best implement an approximation of f*(x)
각 예제에 대해 신경망의 출력만 지정되기 때문에, 훈련 데이터는 네트워크가 숨겨진 계층으로 무엇을 해야 하는지 지정하지 않는다
As a matter of fact, hidden units are what make neural networks unique when compared to other machine learning models
네트워크 자체는 f*(x)의 근사치를 가장 잘 구현하기 위해 이러한 레이어를 수정하는 방법을 결정해야 합니다
So let us define more clearly the hidden layer structure
사실, 숨겨진 단위는 다른 기계 학습 모델과 비교할 때 신경망을 독특하게 만드는 것이다
The hidden layer is comprised of an affine transformation followed by an element wise non-linear function g
그래서 숨겨진 레이어 구조를 더 명확하게 정의합시다
This non-linear function is called the activation function
숨겨진 레이어는 아핀 변환과 요소 현명한 비선형 함수 g로 구성되어 있다
The input to the nth hidden layer is h of n- 1, the output from the previous hidden layer
이 비선형 함수는 활성화 함수라고 불린다
In the case where the layer is the first hidden layer, its input is simply the input image x
N번째 숨겨진 레이어에 대한 입력은 n- 1의 h이며, 이전 숨겨진 레이어의 출력이다
The affine transformation is comprised of a multiplicative weight matrix W, and an additive bias Matrix B
레이어가 첫 번째 숨겨진 레이어인 경우, 입력은 단순히 입력 이미지 x입니다
These weights and biases are the learn parameters theta in the definition of the neural network
아핀 변환은 곱셈 가중 행렬 W와 첨가제 편향 행렬 B로 구성되어 있다
Finally, the transformed input is passed through the activation function g
이러한 가중치와 편향은 신경망의 정의에서 학습 매개 변수 세타이다
Most of the time, g does not contain parameters to be learned by the network
마지막으로, 변환된 입력은 활성화 함수 g를 통과한다
As an example, let us take a look at the rectified linear unit, or ReLU, the default choice of activation functions in most neural networks nowadays
대부분의 경우, g는 네트워크에서 배울 매개 변수를 포함하지 않는다
ReLUs use the maximum between zero and the output of the affine transformation as their element-wise non-linear function
예를 들어, 오늘날 대부분의 신경망에서 활성화 함수의 기본 선택인 정류된 선형 단위 또는 ReLU를 살펴보겠습니다
Since they are very similar to linear units, they're quite easy to optimize
ReLU는 0 사이의 최대값과 아핀 변환의 출력을 요소별 비선형 함수로 사용합니다
Let us go through an example of a ReLU hidden-layer computation
그것들은 선형 단위와 매우 유사하기 때문에 최적화하기가 매우 쉽다
We are given the output of the previous hidden layer hn- 1, the weight matrix W, and the bias matrix b
ReLU 숨겨진 계층 계산의 예를 살펴보겠습니다
We first need to evaluate the affine transformation
이전 숨겨진 레이어 hn- 1, 가중치 행렬 W 및 바이어스 행렬 b의 출력이 주어집니다
Remember, the weight matrix is transposed in the computation
우리는 먼저 아핀 변환을 평가해야 한다
Let's take a look at the dimensions of each of the matrices in this expression
무게 매트릭스는 계산에서 전치된다는 것을 기억하세요
hn- 1 is a 2x3 matrix in this case
이 표현식에서 각 행렬의 크기를 살펴보겠습니다
W is a 2x5 matrix
hn- 1은 이 경우 2x3 행렬입니다
The final result of our affine transformation is a 5 by 3 matrix
W는 2x5 매트릭스이다
Now, let us pass this matrix through the ReLU non-lineary
우리의 아핀 변환의 최종 결과는 5x3 매트릭스이다
We can see that the ReLU prevents any negative outputs from the affine transformation from passing through to the next layer
이제, 이 매트릭스를 ReLU 비선형으로 통과합시다
There are many additional activation functions that can be used as element wise non-linearities in hidden layers for neural networks
우리는 ReLU가 아핀 변환의 음수 출력이 다음 레이어로 통과하는 것을 방지한다는 것을 알 수 있다
In fact, the design of hidden units is another extremely active area of research in the field and does not yet have many guiding theoretical principles
신경망의 숨겨진 계층에서 요소 현명한 비선형성으로 사용할 수 있는 많은 추가 활성화 기능이 있습니다
As an example, certain neural network architectures use the sigmoid non-linearity, the hyperbolic tangent non-linearity, and the generalization of ReLU, the maxout non-linearity as their hidden layer activation functions
사실, 숨겨진 단위의 설계는 현장에서 또 다른 매우 활발한 연구 분야이며 아직 많은 지침 이론적 원리가 없다
If you're interested in learning more about neural network architectures, I strongly encourage you to check out some of the deep learning courses offered on Coursera
예를 들어, 특정 신경망 아키텍처는 시그모이드 비선형성, 쌍곡선 접선 비선형성, 최대 비선형성인 ReLU의 일반화를 숨겨진 레이어 활성화 기능으로 사용합니다
They're amazing
신경망 아키텍처에 대해 더 알고 싶다면, Coursera에서 제공되는 딥 러닝 과정을 확인하는 것이 좋습니다
In this lesson, you learned the main building blocks of feedfoward neural networks including the hidden layers that comprise the core of the machine learning models we use
그들은 놀라워
You also learned different types of activation functions with ReLUs being the default choice for many practitioners in the field
이 수업에서, 당신은 우리가 사용하는 기계 학습 모델의 핵심을 구성하는 숨겨진 레이어를 포함한 피드포워드 신경망의 주요 구성 요소를 배웠습니다
In the next lesson, we'll explore the output layers and then study how to learn the weights and bias matrices from training data, setting the stage for training our first neural network later on in the module
또한 ReLU가 이 분야의 많은 실무자들에게 기본 선택인 다양한 유형의 활성화 기능을 배웠습니다
[MUSIC]
다음 수업에서는 출력 레이어를 탐색한 다음 훈련 데이터에서 가중치와 편향 행렬을 배우는 방법을 연구하여 나중에 모듈에서 첫 번째 신경망을 훈련하기 위한 단계를 설정할 것입니다

[음악]
