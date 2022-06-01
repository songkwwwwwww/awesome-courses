[MUSIC] So far in this module, we have reviewed what comprises a feedforward neural network model, and how to evaluate the performance of a neural network model using loss functions
[음악] 지금까지 이 모듈에서, 우리는 피드포워드 신경망 모델로 구성된 것과 손실 함수를 사용하여 신경망 모델의 성능을 평가하는 방법을 검토했습니다
This lesson will explain the final major component of designing neural networks, the training process
이 수업은 신경망 설계의 최종 주요 구성 요소인 훈련 과정을 설명할 것이다
Specifically, we will be answering the following question
구체적으로, 우리는 다음 질문에 대답할 것이다
How can we get the best parameter set theta for a feedforward neural network given training data
주어진 훈련 데이터에 대한 피드포워드 신경망에 대한 최고의 매개 변수 세트 세타를 어떻게 얻을 수 있을까요
The answer lies in using an iterative optimization procedure with proper parameter initialization
답은 적절한 매개 변수 초기화와 함께 반복적인 최적화 절차를 사용하는 것이다
Let us first revisit the feedforward neural network training procedure we described previously
먼저 이전에 설명한 피드포워드 신경망 훈련 절차를 다시 살펴보겠습니다
Given a training data input x and the corresponding correct output, f star of x, we first pass the input x through the hidden layers, then through the output layer to get the final output y
훈련 데이터 입력 x와 해당 올바른 출력인 f star of x를 감안할 때, 우리는 먼저 숨겨진 레이어를 통해 입력 x를 통과한 다음 출력 레이어를 통과하여 최종 출력 y를 얻습니다
We see here that the output y is a function of the parameters theta
여기서 출력 y는 매개 변수 세타의 함수라는 것을 알 수 있습니다
And remember, that theta comprises the weights and the biases of our affine transformations inside the network
그리고 세타는 네트워크 내부의 아핀 변환의 가중치와 편견을 포함한다는 것을 기억하세요
Next, we compare our predicted output f of x and theta with the correct output, f star of x through the loss function
다음으로, 우리는 x의 예측된 출력 f와 세타를 손실 함수를 통해 올바른 출력인 x의 f 별과 비교합니다
Remember that the loss function measures how large the error is between the network output and our true output
손실 함수는 네트워크 출력과 실제 출력 사이의 오류가 얼마나 큰지 측정한다는 것을 기억하십시오
Our goal is to get a small value for the loss function across the entire data set
우리의 목표는 전체 데이터 세트에서 손실 함수에 대한 작은 가치를 얻는 것입니다
We do so by using the loss function as a guide to produce a new set of parameters theta that are expected to give a lower value of the loss function
손실 함수를 가이드로 사용하여 손실 함수의 더 낮은 값을 제공할 것으로 예상되는 새로운 매개 변수 세타 세트를 생성합니다
Specifically, we use the gradient of the loss function to modify the parameters theta
특히, 우리는 매개 변수 세타를 수정하기 위해 손실 함수의 그라디언트를 사용합니다
This optimization procedure is known as gradient descent
이 최적화 절차는 그라데이션 하강으로 알려져 있다
Before describing gradient descent in detail, let's take another look at the neural network loss function
그라데이션 하강을 자세히 설명하기 전에, 신경망 손실 기능을 다시 살펴봅시다
Usually, we have thousands of training example pairs, x and f star of x, available for autonomous driving tasks
보통, 우리는 자율주행 작업에 사용할 수 있는 수천 개의 훈련 예제 쌍, x와 f star of x가 있습니다
We can compute the loss over all training examples, as the mean of the losses over the individual training examples
우리는 개별 훈련 사례에 대한 손실의 의미로 모든 훈련 예에 대한 손실을 계산할 수 있습니다
We can then compute the gradient of the training loss with respect to the parameters theta which is equal to the mean of the gradient of the individual losses over every training example
그런 다음 모든 훈련 예에서 개인 손실의 그라디언트의 평균과 동일한 매개 변수 세타에 대해 훈련 손실의 그라디언트를 계산할 수 있습니다
Here we use the fact that the gradient and the sum are linear operators
여기서 우리는 그라디언트와 합이 선형 연산자라는 사실을 사용합니다
So the gradient of a sum is equal to the sum of the individual gradients
따라서 합계의 그라디언트는 개별 그라디언트의 합과 같다
Using the formulated gradient equation, we can now describe the batch gradient descent optimization algorithm
공식화된 그라데이션 방정식을 사용하여, 우리는 이제 배치 그라데이션 하강 최적화 알고리즘을 설명할 수 있습니다
Batch gradient descent is a linear first order optimization method
배치 그라데이션 하강은 선형 1차 최적화 방법이다
Iterative means that it starts from an initial guess of parameters theta and improves on these parameters iteratively
반복은 매개 변수 세타의 초기 추측에서 시작하여 이러한 매개 변수를 반복적으로 개선한다는 것을 의미합니다
First order means that the algorithm only uses the first order derivative to improve the parameters theta
첫 번째 순서는 알고리즘이 매개 변수 세타를 개선하기 위해 첫 번째 순서 미분만 사용한다는 것을 의미합니다
Batch gradient descent goes as follows
배치 그라데이션 하강은 다음과 같습니다
First, the parameters theta of the neural network are initialized
첫째, 신경망의 매개 변수 세타가 초기화된다
Second, a stopping condition is determined, which terminates the algorithm and returns a final set of parameters
둘째, 알고리즘을 종료하고 최종 매개 변수 세트를 반환하는 정지 조건이 결정됩니다
Once the iterative procedure begins, the first thing to be performed by the algorithm is to compute the gradient of the loss function with respect to the parameters theta, denoted del sub theta
반복 절차가 시작되면, 알고리즘에 의해 가장 먼저 수행되는 것은 델 서브 세타로 표시된 매개 변수 세타에 대한 손실 함수의 그라디언트를 계산하는 것이다
The gradient can be computed using the equation we derived earlier
그라디언트는 이전에 파생된 방정식을 사용하여 계산할 수 있습니다
Finally, the parameters theta are updated according to the computed gradient
마지막으로, 매개 변수 세타는 계산된 그라디언트에 따라 업데이트됩니다
Here, epsilon is called the learning rate and controls how much we adjust the parameters in the direction of the negative gradient at every iteration
여기서 엡실론은 학습 속도라고 불리며 모든 반복에서 음수 그라디언트 방향으로 매개 변수를 조정하는 양을 제어합니다
Let's take a look at a visual example of batch gradient descent in the 2D case
2D 케이스에서 배치 그라데이션 하강의 시각적 예를 살펴보겠습니다
Here, we are trying to find the parameters theta one and theta two that minimize our function J of theta
여기서, 우리는 세타의 함수 J를 최소화하는 매개 변수 세타 원과 세타 2를 찾으려고 노력하고 있습니다
Theta is shaped like an oblong ball shown here with contour lines of equal value
세타는 동등한 가치의 윤곽선으로 표시된 직사각형 공 모양이다
Gradient descent iteratively finds new parameters theta that take us a step down the bowl at each iteration
그라디언트 하강은 각 반복에서 그릇을 한 단계 내려가는 새로운 매개 변수 세타를 반복적으로 찾습니다
The first step of the algorithm is to initialize the parameters theta
알고리즘의 첫 번째 단계는 매개 변수 세타를 초기화하는 것이다
Using our initial parameters, we arrive at an initial value for our loss function denoted by the red dot
초기 매개 변수를 사용하여 빨간색 점으로 표시된 손실 함수의 초기 값에 도달합니다
We start gradient descent by computing the gradient of the loss function at the initial parameter values theta 1 and theta 2
우리는 초기 매개 변수 값 세타 1과 세타 2에서 손실 함수의 그라디언트를 계산하여 그라디언트 하강을 시작합니다
Using the update step, we then get the new parameters to arrive at a lower point on our loss function
업데이트 단계를 사용하여 손실 함수의 더 낮은 지점에 도달하기 위해 새로운 매개 변수를 얻습니다
We repeat this process until we achieve our stopping criteria
우리는 정지 기준을 달성할 때까지 이 과정을 반복한다
We then get the last set of the parameters, theta 1 and theta 2 as our optimal set that minimizes our loss function
그런 다음 손실 함수를 최소화하는 최적의 세트로 매개 변수 세타 1과 세타 2의 마지막 세트를 얻습니다
Two pieces are still missing from the presented algorithm
제시된 알고리즘에서 두 조각이 여전히 누락되었다
How do we initialize the parameter's data and how do we decide when to actually stop the algorithm
매개 변수의 데이터를 어떻게 초기화하고 알고리즘을 실제로 중지할 시기를 어떻게 결정하나요
The answer to both of these questions is still highly based on heuristics that work well in practice
이 두 질문에 대한 답은 여전히 실제로 잘 작동하는 휴리스틱에 기반을 두고 있다
For parameter initialization, we usually initialized the weights using a standard normal distribution and set the biases to 0
매개 변수 초기화를 위해, 우리는 보통 표준 정규 분포를 사용하여 가중치를 초기화하고 편향을 0으로 설정합니다
It is worth mentioning that there are other heuristics specific to certain activation functions that are widely used in a literature
문학에서 널리 사용되는 특정 활성화 기능에 특정한 다른 휴리스틱이 있다는 것은 언급할 가치가 있다
We provide some of these heuristics in a supplementary material
우리는 이러한 휴리스틱 중 일부를 보충 재료로 제공합니다
Defining the gradient descent's stopping conditions is a bit more complex
그라데이션 하강의 정지 조건을 정의하는 것은 조금 더 복잡하다
There are three ways to determine when to stop the training algorithm
훈련 알고리즘을 언제 중단할지 결정하는 세 가지 방법이 있다
Most simply, we can decide to stop when a predefined maximum number of gradient descent iterations is reached
가장 간단히 말해서, 우리는 미리 정의된 최대 그라디언트 하강 반복 수에 도달하면 중단하기로 결정할 수 있다
Another heuristic is based on how much the parameters theta changed between iterations
또 다른 휴리스틱은 반복 사이에 매개 변수 세타가 얼마나 변했는지에 달려 있다
A small variation means the algorithm is not updating the parameters effectively anymore, which might mean that a minimum has been reached
작은 변화는 알고리즘이 더 이상 매개 변수를 효과적으로 업데이트하지 않는다는 것을 의미하며, 이는 최소값에 도달했다는 것을 의미할 수 있다
The last widely used stopping criteria is the change in the loss function value between iterations
마지막으로 널리 사용되는 정지 기준은 반복 간의 손실 함수 값의 변화이다
Again, as the changes in the loss function between iterations become small, the optimization is likely to have converged to a minimum
다시 말하지만, 반복 간의 손실 함수의 변화가 작아짐에 따라, 최적화는 최소한으로 수렴되었을 가능성이 높다
Choosing one of these stopping conditions is very much a matter of what works best for the problem at hand
이러한 정지 조건 중 하나를 선택하는 것은 당면한 문제에 가장 적합한 것의 문제이다
We will revisit the stopping conditions in the next lesson, as we study some of the pitfalls of the training process, and how to avoid them
우리는 훈련 과정의 함정 중 일부와 이를 피하는 방법을 연구하면서 다음 수업에서 정지 조건을 재검토할 것입니다
Unfortunately, the batch gradient descent algorithm suffers from severe drawbacks
불행하게도, 배치 그라데이션 하강 알고리즘은 심각한 단점을 겪고 있다
To be able to compute the gradient we use backpropogation
그라디언트를 계산하기 위해 우리는 백프로포그를 사용한다
Backpropogation involves computing the output of the network for the example on which we would like to evaluate the gradient
백프로포깅은 그라디언트를 평가하려는 예시에 대한 네트워크의 출력을 계산하는 것을 포함한다
And batch gradient descent evaluates the gradient over the whole training set
그리고 배치 그라디언트 하강은 전체 훈련 세트에서 그라디언트를 평가합니다
Making it very slow to perform a single update step
단일 업데이트 단계를 수행하는 것이 매우 느리게 만든다
Luckily, the laws function as well as its gradient are means over the training dataset
다행히도, 법칙은 기능하고 그라디언트는 훈련 데이터 세트에 대한 수단이다
For example, we know that the standard error in a mean estimated from a set of N samples is sigma over the square root of N
예를 들어, 우리는 N 샘플 세트에서 추정된 평균의 표준 오류가 N의 제곱근 위의 시그마라는 것을 알고 있습니다
Where sigma is the standard deviation of the distribution and N as the number of samples used to estimate the mean
여기서 시그마는 분포의 표준 편차이고 N은 평균을 추정하는 데 사용되는 샘플의 수이다
That means that the rate of decrease in error in the gradient estimate is less than linear in the number of samples
그것은 그라데이션 추정치의 오차 감소율이 샘플 수에서 선형보다 적다는 것을 의미합니다
This observation is very important, as we now can use a small sub-sample of the training data or a mini batch to compute our gradient estimate
이 관찰은 이제 훈련 데이터의 작은 하위 샘플이나 미니 배치를 사용하여 그라데이션 추정치를 계산할 수 있기 때문에 매우 중요합니다
So how does using mini batches modify our batch gradient descent algorithm
그렇다면 미니 배치를 사용하여 배치 그라데이션 하강 알고리즘을 어떻게 수정하나요
The modification is actually quite simple
수정은 사실 꽤 간단하다
The only alteration to the base algorithm is at the sampling step
기본 알고리즘의 유일한 변경은 샘플링 단계이다
Here we choose the sub sample n prime of the training data as our mini batch
여기서 우리는 훈련 데이터의 하위 샘플 n 프라임을 미니 배치로 선택합니다
We can now evaluate the gradient and perform the update steps in an identical manner to batch grading descent
이제 그라디언트를 평가하고 배치 등급 하강과 동일한 방식으로 업데이트 단계를 수행할 수 있습니다
This algorithm is called stochastic or minibatch gradient descent, as we randomly select samples to include in the minibatches at each iteration
이 알고리즘은 각 반복의 미니배치에 포함할 샘플을 무작위로 선택하기 때문에 확률 또는 미니배치 그라데이션 하강이라고 불린다
However, this algorithm results in an additional parameter to be determined, which is the size of the minibatch that we want to use
그러나, 이 알고리즘은 우리가 사용하려는 미니배치의 크기인 추가 매개 변수를 결정하게 한다
To pick an appropriate minibatch, it has to be noted that some kinds of hardware achieve better runtime with specific sizes of data arrays
적절한 미니배치를 선택하려면, 어떤 종류의 하드웨어가 특정 크기의 데이터 어레이로 더 나은 런타임을 달성한다는 점에 유의해야 합니다
Specifically when using GPUs, it is common to use power of two mini batch sizes which match GPU computing and memory architecture as well
특히 GPU를 사용할 때, GPU 컴퓨팅과 메모리 아키텍처와 일치하는 두 가지 미니 배치 크기의 힘을 사용하는 것이 일반적이다
And therefore, use the GPU resources efficiently
따라서 GPU 리소스를 효율적으로 사용하세요
Let's look at some of the factors that drive batch size selection
배치 크기 선택을 주도하는 몇 가지 요소를 살펴봅시다
Multi-core architectures such as GPUs are usually under-utilized by extremely small batch sizes, which motivates using some absolute minimum batch size below which there's no reduction in the time to process a minibatch
GPU와 같은 멀티코어 아키텍처는 일반적으로 매우 작은 배치 크기에 의해 활용도가 낮으며, 이는 미니배치를 처리하는 시간을 줄일 수 없는 절대적인 최소 배치 크기를 사용하도록 동기를 부여합니다
Furthermore, large batch sizes usually provide a more accurate estimate of the gradient
게다가, 큰 배치 크기는 보통 그라디언트의 더 정확한 추정치를 제공한다
Ensuring descent in a direction that improves the network performance more reliably
네트워크 성능을 더 안정적으로 향상시키는 방향으로 하강을 보장합니다
However as noted previously, this improvement in the accuracy of the estimate is less than linear
그러나 앞서 언급했듯이, 추정치의 정확성의 개선은 선형보다 적다
Small batch sizes on the other hand have been seen to offer a regularlizing effect
반면에 작은 배치 크기는 정규화 효과를 제공하는 것으로 보였다
With the best generalization often seen at a batch size of one
종종 배치 크기로 볼 수 있는 최고의 일반화
If you're not sure what we mean by generalization, don't worry
일반화가 무엇을 의미하는지 잘 모르겠다면, 걱정하지 마세요
As we'll be exploring it more closely in the next lesson
우리는 다음 수업에서 그것을 더 자세히 탐구할 것이다
Furthermore, optimization algorithms usually converge more quickly if they're allowed to rapidly compute approximate estimates of the gradients and iterate more often rather than computing exact gradients and performing fewer iterations
게다가, 최적화 알고리즘은 일반적으로 그라디언트의 대략적인 추정치를 빠르게 계산하고 정확한 그라디언트를 계산하고 더 적은 반복을 수행하기보다는 더 자주 반복할 수 있다면 더 빨리 수렴한다
As a result of these trade-offs, typical power of two mini batch sizes range from 32 to 256, with smaller sizes sometimes being attempted for large models or to improve generalization
이러한 절충의 결과로, 두 개의 미니 배치 크기의 일반적인 전력은 32에서 256까지 다양하며, 더 작은 크기는 때때로 대형 모델이나 일반화를 개선하려고 시도된다
One final issue to keep in mind is the requirement to shuffle the dataset before sampling the minibatch
명심해야 할 마지막 문제는 미니배치를 샘플링하기 전에 데이터 세트를 섞어야 한다는 것이다
Failing to shuffle the dataset at all can reduce the effectiveness of your network
데이터 세트를 전혀 섞지 않으면 네트워크의 효율성을 줄일 수 있습니다
There exist many variants of stochastic gradient descent in the literature, each having their own advantages and disadvantages
문학에는 확률적 그라데이션 하강의 많은 변형이 존재하며, 각각 고유한 장점과 단점이 있다
It might be difficult to choose which variant to use, and sometimes one of the variants works better for certain problem than another
사용할 변형을 선택하는 것은 어려울 수 있으며, 때로는 변형 중 하나가 다른 문제보다 특정 문제에 더 잘 작동합니다
As a simple rule of thumb for autonomous driving applications, a safe choice is the ADAM optimization method
자율주행 애플리케이션을 위한 간단한 경험 법칙으로서, 안전한 선택은 ADAM 최적화 방법이다
It is quite robust to initial parameters theta, and widely use
그것은 초기 매개 변수 세타에 매우 강력하며, 널리 사용된다
If you are interest in learning more about this variance, have a look at the resources listed in the supplemental notes
이 차이에 대해 더 알고 싶다면, 보충 노트에 나열된 리소스를 살펴보세요
In this lesson, you learned how to optimize the parameters of a neural network using batch gradient descent
이 수업에서는 배치 그라데이션 하강을 사용하여 신경망의 매개 변수를 최적화하는 방법을 배웠습니다
You also learned that there are a lot of proposed variance of this optimization algorithm, with a safety fault choice being ADAM
당신은 또한 이 최적화 알고리즘의 제안된 차이가 많다는 것을 배웠고, 안전 결함 선택은 ADAM입니다
Congratulations, you've finished the essential steps required to build and train an neural network
축하합니다, 당신은 신경망을 구축하고 훈련시키는 데 필요한 필수 단계를 마쳤습니다
In the next lesson, we will discuss how you can choose some of the optimization parameters to improve network training, such as the learning rate
다음 수업에서는 학습 속도와 같은 네트워크 교육을 개선하기 위해 최적화 매개 변수를 선택하는 방법에 대해 논의할 것입니다
Also we'll discuss how to evaluate the performance of our neural network using validation sets
또한 검증 세트를 사용하여 신경망의 성능을 평가하는 방법에 대해 논의할 것입니다
See you next time
다음에 보자
[MUSIC]
[음악]
