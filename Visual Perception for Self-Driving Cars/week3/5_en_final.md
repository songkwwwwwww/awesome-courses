[MUSIC] In the last lesson, we described how to divide data sets into training, validation, and testing splits, and interpret the results of evaluating the loss function on each of these splits
[음악] 마지막 수업에서, 우리는 데이터 세트를 훈련, 검증 및 테스트 분할로 나누고 이러한 각 분할에서 손실 함수를 평가한 결과를 해석하는 방법을 설명했습니다
We also emphasize that most of the time we tend to suffer from overfitting rather than underfitting after training the network
우리는 또한 대부분의 경우 네트워크를 훈련한 후 과복하기보다는 과복으로 고통받는 경향이 있다고 강조한다
In this lesson, we'll explore some ways to reduce overfitting by applying regularization strategies during training
이 수업에서는 교육 중에 정규화 전략을 적용하여 과적합을 줄이는 몇 가지 방법을 살펴볼 것입니다
As a result of regularization, our networks will generalize well to new data, and we'll be able to use them more effectively outside of the lab
정규화의 결과로, 우리의 네트워크는 새로운 데이터로 잘 일반화될 것이며, 실험실 밖에서 더 효과적으로 사용할 수 있을 것이다
Let's walk through an iteration of neural network development on a toy example
장난감 예시에서 신경망 개발의 반복을 살펴봅시다
We want to separate a 2D Cartesian space into two components, orange and blue
우리는 2D 데카르트 공간을 주황색과 파란색의 두 가지 구성 요소로 분리하고 싶습니다
Any point belonging to the blue space should be labelled class 1, while any point belonging to the orange space should be labelled class 2
파란색 공간에 속하는 모든 점은 클래스 1로 표시되어야 하며, 주황색 공간에 속하는 모든 점은 클래스 2로 표시되어야 합니다
However, we do not have direct access to these classes or their boundaries
그러나, 우리는 이러한 클래스나 그들의 경계에 직접 접근할 수 없다
Instead we only have access to sensor measurements that provide us with examples of points and their corresponding class
대신 우리는 점과 해당 클래스의 예를 제공하는 센서 측정에만 접근할 수 있습니다
Unfortunately, our sensor is also noisy, that means it sometimes provides the incorrect label
불행하게도, 우리의 센서도 시끄럽습니다, 그것은 때때로 잘못된 라벨을 제공한다는 것을 의미합니다
The label points in the blue space as class 2, and in orange space as class 1
라벨은 파란색 공간을 클래스 2로, 주황색 공간은 클래스 1로 가리킨다
Our problem amounts to finding the space classification from the noisy sensor data
우리의 문제는 시끄러운 센서 데이터에서 공간 분류를 찾는 것과 같다
We begin by collecting data from the sensor and splitting them into 60-40 training validation splits
우리는 센서에서 데이터를 수집하여 60-40개의 훈련 검증 분할로 나누는 것으로 시작합니다
The training splits is shown here as points with white out lines, and the validation splits is shown here as points with black out lines
훈련 분할은 화이트 아웃 라인이 있는 점으로 여기에 표시되며, 검증 분할은 블랙아웃 라인이 있는 포인트로 여기에 표시됩니다
Let's use a simple neuron network with one layer and two hidden units per layer to classify measurements
한 층과 두 개의 숨겨진 단위가 있는 간단한 뉴런 네트워크를 사용하여 측정을 분류해 봅시다
Using this design choice, we get that following space classification
이 디자인 선택을 사용하여, 우리는 다음과 같은 공간 분류를 얻습니다
The training set loss is 0
훈련 세트 손실은 0
264 close to the validation set loss of 0
2268의 유효성 검사 세트 손실에 가깝다
2268
하지만 그것은 여전히 0
But it's still much higher than the minimum achievable loss of 0
1의 최소 달성 가능한 손실보다 훨씬 높다
1
이것은 적절한 경우이다
This is a clear case of underfitting
네트워크 분류 결과를 실제 공간 분류와 비교할 때, 신경망이 당면한 문제의 복잡성을 포착하지 못하고 필요에 따라 공간을 네 개의 구획으로 올바르게 분할하지 못했다는 것을 알 수 있습니다
When we compare the results of our network classification to the true space classification, we see that the neural network fail to capture the complexity of the problem at hand, and did not correctly segment the space into four compartments as required
적절한 문제를 해결하기 위해, 우리는 5개의 추가 레이어를 추가하여 네트워크 크기를 늘리고, 숨겨진 유닛 수를 레이어당 6개로 늘립니다
To resolve underfitting issues, we increase the network size by adding five additional layers, and increase the number of hidden units to six units per layer
우리의 모델은 이제 훨씬 더 표현력이 풍부하므로, 진정한 분류를 더 잘 표현할 수 있어야 한다
Our model is now much more expressive, so it should be able to better represent the true classification
우리는 계속해서 모델을 다시 훈련시킨 다음, 우리가 얼마나 잘 해냈는지 테스트합니다
We go ahead and train our model again, then test to see how well we have done
우리는 0
We noticed that our validation set loss result of 0
45의 검증 세트 손실 결과가 0
45 is much higher than our training set loss result of 0
1의 훈련 세트 손실 결과보다 훨씬 높다는 것을 알아차렸다
1
그러나 훈련 세트 손실은 이 작업에서 0
The training set loss, however, is equal to the minimum achievable loss of 0
1의 최소 달성 가능한 손실과 같다
1 on this task
우리는 훈련 데이터에 과장된 상태에 있다
We are in a state of overfitting to the training data
과복합은 훈련 데이터의 소음을 배우는 네트워크로 인해 발생합니다
Overfitting is caused by the network learning the noise in the training data
신경망에는 매개 변수가 너무 많기 때문에, 빨간색 원 안에 표시된 것처럼 시끄러운 훈련 예시에 해당하는 공간의 작은 영역을 구부릴 수 있다
Because the neural network has so many parameters, it is able to curve out small regions in the space that correspond to the noisy training examples as shown inside the red circles
이것은 보통 당면한 문제에 비해 네트워크 크기를 너무 많이 늘릴 때 발생한다
This usually happens when we increase the network size too much for the problem at hand
다시 말하지만, 우리는 피팅을 치료하는 한 가지 방법은 정규화를 통해서라는 것을 배웠다
Again, we have learned that one way to remedy over fitting is through regularization
신경망에 일반적으로 사용되는 첫 번째 정규화 방법을 확인해 봅시다
Let's check out the first regularization method commonly used for neural networks
신경망에 적용할 수 있는 가장 전통적인 형태의 정규화는 매개 변수 규범 처벌의 개념이다
The most traditional form of regularization applicable to neural networks is the concept of parameter norm penalties
이 접근법은 목적 함수에 세타의 페널티 오메가를 추가하여 모델의 용량을 제한한다
This approach limits the capacity of the model by adding the penalty omega of theta to the objective function
가중치 매개 변수 알파를 사용하여 기존 손실 함수에 표준 페널티를 추가합니다
We add the norm penalty to our existing loss function using our weighting parameter alpha
알파는 손실 함수의 총 가치에 대한 표준 페널티의 상대적 기여를 가중하는 새로운 하이퍼파라미터이다
Alpha is a new hyperparameter that weights the relative contribution of the norm penalty to the total value of loss function
보통, 세타의 오메가는 세타의 가치가 얼마나 큰지에 대한 척도이다
Usually, omega of theta is a measure of how large the value of theta is
가장 일반적으로 이 조치는 Lp 규범이다
Most commonly this measure is an Lp Norm
P가 1일 때 우리는 절대 합계를 가지고 있고, P가 2일 때 우리는 이차 합계 등을 얻는다
When P is 1 we have an absolute sum, and when P is 2 we get the quadratic sum, etc
게다가, 우리는 보통 신경망의 가중치만 제한한다
Furthermore, we usually only constrain the weights of the neural network
이것은 가중치의 수가 신경망의 편향 수보다 훨씬 많다는 사실에 의해 동기 부여된다
This is motivated by the fact that the number of weights is much larger than the number of biases in the neural network
따라서 체중 벌금은 최종 네트워크 성능에 훨씬 더 큰 영향을 미친다
So weight penalty have a much larger impact on the final network performance
신경망에서 사용되는 가장 일반적인 규범 처벌은 L2 규범 페널티이다
The most common norm penalty used in neural networks is the L2-norm penalty
L2 규범 페널티는 신경망의 각 층의 모든 가중치의 L2 규범을 최소화하려고 한다
The L2-norm penalty tries to minimize the L2-norm of all the weights in each layer of the neural network
L2 규범 페널티가 우리 문제에 적용된 효과를 살펴봅시다
Let's take a look at the effect of the L2-norm penalty applied to our problem
우리의 최신 디자인은 훈련 데이터 세트에 과장되었다는 것을 기억하세요
Remember that our latest design resulted in overfitting on the training data set
L2 규범 페널티를 추가하면 손실 함수는 비정규화된 네트워크에 대한 낮은 검증 세트 손실로 인해 공간 분류를 훨씬 더 잘 추정할 수 있습니다
Adding the L2-norm penalty the loss function results in a much better estimate of the space classification, due to a lower validation set loss over the unregularized network
그러나, 이 낮은 검증 세트 손실은 훈련 세트 손실이 0
However, this lower validation set loss is coupled with an increase in the training set loss from 0
1에서 0
1 to 0
176으로 증가하는 것과 결합된다
176
이 경우 일반화 격차의 감소는 훈련 세트 손실의 증가보다 높다
In this case the decrease in the generalization gap is higher than the increase in training set loss
그러나, 다시 한 번 적절한 정권에 빠지지 않도록 너무 많이 정규화하지 않도록 주의하십시오
Do be careful not to regularize too much, however, to avoid falling into the underfitting regime once again
대부분의 신경망 패키지에서 표준 페널티를 추가하는 것은 매우 쉽다
Adding a norm penalty is quite easy in most neural network packages
피팅이 의심된다면, L2 규범 처벌은 설계 과정에서 많은 시간 낭비를 방지하는 매우 쉬운 치료법일 수 있습니다
If you suspect over fitting, L2-norm penalties might be a very easy remedy that will prevent a lot of waste of time during the design process
이 비디오의 앞부분에서 언급했듯이, 연구자들은 신경망에 특정한 정규화 메커니즘을 개발했다
As we mentioned earlier in this video, researchers have developed regularization mechanisms that are specific to neural networks
정기적으로 사용되는 강력한 메커니즘 중 하나는 탈락이라고 불린다
One powerful mechanism used regularly is called dropout
네트워크 교육 중에 중퇴가 어떻게 적용되는지 보자
Lets see how dropout gets applied during network training
중퇴자의 첫 번째 단계는 우리가 P 서브 keep라고 부를 확률을 선택하는 것이다
The first step of dropout is to choose a probability which we'll call P sub keep
모든 훈련 반복에서, 이 확률은 네트워크에 보관할 네트워크 노드의 하위 집합을 선택하는 데 사용됩니다
At every training iteration, this probability is used to choose a subset of the network nodes to keep in the network
이 노드들은 숨겨진 단위, 출력 단위 또는 입력 단위일 수 있다
These nodes can be either hidden units, output units, or input units
그런 다음 이 장치에서 나오는 모든 연결을 절단한 후 출력 y를 평가합니다
We then proceed to evaluate the output y after cutting all the connections coming out of this unit
우리는 아마도 유지에 비례하는 유닛을 제거하고 있기 때문에, 우리는 훈련이 끝날 때 최종 가중치를 P 서브 유지로 곱합니다
Since we are removing units proportional to the keep probably, P sub keep, we multiply the final weights by P sub keep at the ending of training
이것은 전체 네트워크에 대한 추론으로 전환할 때 출력을 잘못 확장하지 않는 데 필수적이다
This is essential to avoid incorrectly scaling the outputs when we switch to inference for the full network
드롭아웃은 누락된 입력과 숨겨진 단위로 모델을 강제로 배우도록 강요하는 것으로 직관적으로 설명될 수 있다
Dropout can be intuitively explained as forcing the model to learn with missing input and hidden units
즉, 그 자체의 다른 버전으로
Or in other words, with different versions of itself
그것은 훈련 과정에서 광범위한 신경망 모델을 정규화하는 계산적으로 저렴하지만 강력한 방법을 제공하여 수유와 연습을 크게 줄인다
It provides a computationally inexpensive but powerful method of regularizing a broad family of neural network models during the training process, leading to significant reductions in over feeding and practice
게다가, 탈락은 사용할 수 있는 훈련 절차의 유형이나 모델을 크게 제한하지 않는다
Furthermore, dropout does not significantly limit the type or model of training procedure that can be used
그것은 분산된 매개 변수 표현을 사용하는 거의 모든 모델에서 잘 작동하며, 확률적 그라데이션 하강으로 훈련할 수 있다
It works well with nearly any model that uses a distributed over parameterized representation, and that can be trained with stochastic gradient descent
마지막으로, 모든 신경망 라이브러리에는 드롭아웃 계층이 구현되어 사용할 준비가 되어 있습니다
Finally, all neural network libraries have a dropout layer implemented and ready to be used
밀집된 피드 포워드 신경망 계층이 있을 때마다 드롭아웃을 사용하는 것이 좋습니다
We recommend using drop out whenever you have dense feed forward neural network layers
당신이 알아야 할 정규화의 최종 형태는 일찍 멈추는 것이다
The final form of regularization you should know about is early stopping
조기 정지를 시각적으로 설명하기 위해, 우리는 훈련 세트에서 평가된 신경망의 손실 기능의 진화를 살펴본다
To explain early stopping visually, we look at the evolution of the loss function of a neuro network evaluated on the training set
충분한 용량을 감안할 때, 신경망이 훈련 데이터를 암기하기 때문에 훈련 손실은 0에 가까운 값으로 감소할 수 있어야 한다
Given enough capacity, the training loss should be able to decrease to a value close to zero, as the neuro network memorizes the training data
그러나, 독립적인 훈련과 검증 세트가 있다면, 검증 손실은 증가하기 시작하는 지점에 도달한다
However, if we have independent training and validation sets, the validation loss reaches a point where it starts to increase
이 행동은 과적합 체제 동안 전형적이며, 조기 중단으로 알려진 방법을 통해 해결될 수 있다
This behaviour is typical during the overfitting regime, and can be resolved via a method known as early stopping
우리는 이전에 다양한 정지 기준에 따라 최적화를 중단할 수 있다고 논의했다
We discussed earlier that we can stop the optimization according to various stopping criteria
사전 설정된 반복 횟수에 대한 검증 손실이 계속 증가할 때 조기 정지는 훈련을 끝낸다
Early stopping ends training when the validation loss keeps increasing for a preset number of iterations or epochs
이것은 보통 신경망이 과적합 체제에 들어가기 직전에 해석된다
This is usually interpreted at the point just before the neural network enters the overfitting regime
훈련 알고리즘을 중지한 후, 유효성 검사 손실이 가장 낮은 매개 변수 집합이 반환됩니다
After stopping the training algorithm, the set of parameters with the lowest validation loss is returned
마지막으로, 조기 정지는 정규화를 위한 첫 번째 선택으로 사용해서는 안 된다
As a final note, early stopping should not be use as a first choice for regularization
또한 교육 시간을 제한하기 때문에 전반적인 네트워크 성능을 방해할 수 있습니다
As it also limits the training time, which may interfere with the overall network performance
축하합니다, 이제 자신만의 신경망을 구축할 준비가 되었습니다
Congratulations, you are now ready to start building your own neural networks
이 수업에서, 당신은 과적합 체제에 빠지면서 신경망의 성능을 향상시키는 방법을 배웠습니다
In this lesson, you learned how to improve the performance of the neural network in the key as it falls into an overfitting regime
신경망 설계 및 훈련에는 더 많은 흥미로운 측면이 있으며, 이 모듈에 포함시킨 추가 리소스를 통해 이 매혹적인 분야를 계속 탐구할 것을 촉구합니다
There are many more interesting aspects to neural network design and training, and I urge you to keep exploring this fascinating field through the additional resources that we've included with this module
이 모듈의 다음이자 마지막 수업에서, 우리는 비전 기반 인식에 대한 매우 실용적이고 역사적으로 중요한 신경망 아키텍처인 컨볼루션 신경망에 대해 이야기할 것입니다
In the next and final lesson in this module, we will talk about a neural network architecture of huge practical and historical importance for vision based perception, the convolutional neural network
그때 보자 [음악]
See you then [MUSIC]

