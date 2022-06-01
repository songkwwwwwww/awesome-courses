So far, in this module, we've discussed what a neural network is and how to arrive at the best weights given training data
지금까지, 이 모듈에서, 우리는 신경망이 무엇이며 훈련 데이터가 주어진 최고의 가중치를 도달하는 방법에 대해 논의했습니다
However, we still need to explore more deeply how to train neural networks efficiently
그러나, 우리는 여전히 신경망을 효율적으로 훈련시키는 방법을 더 깊이 탐구할 필요가 있다
This lesson will discuss how to split your data for an unbiased estimate of performance on your neural network model and what insights you can get from observing your neural network's performance on various data splits
이 수업에서는 신경망 모델의 성능에 대한 편견 없는 추정치를 위해 데이터를 분할하는 방법과 다양한 데이터 분할에 대한 신경망의 성능을 관찰함으로써 얻을 수 있는 통찰력에 대해 논의할 것입니다
Let's begin by describing the usual data splits we use to evaluate a machine learning system
기계 학습 시스템을 평가하는 데 사용하는 일반적인 데이터 분할을 설명하는 것으로 시작합시다
Let's take as an example a real life problem
실제 문제를 예로 들어 봅시다
We're given a dataset of 10,000 images of traffic signs with corresponding classification labels
해당 분류 라벨이 있는 10,000개의 트래픽 표지판 이미지의 데이터 세트가 제공됩니다
We want to train our neural network to perform traffic sign classification
우리는 교통 신호 분류를 수행하기 위해 신경망을 훈련시키고 싶다
How do we approach this problem
우리는 이 문제에 어떻게 접근하나요
Do we train on all the data and then deploy our traffic sign classifier
우리는 모든 데이터를 훈련한 다음 교통 표지판 분류기를 배포하나요
That approach is guaranteed to fail for the following reason
그 접근 방식은 다음과 같은 이유로 실패할 것으로 보장된다
Given a large enough neural network, we are almost guaranteed to get a very low training loss
충분히 큰 신경망을 감안할 때, 우리는 매우 낮은 훈련 손실을 얻을 것이 거의 보장된다
This is due to the very large number of parameters in a typical deep neural network allowing it to memorize the training data to a large extent given a large enough number of training iterations
이것은 충분한 수의 훈련 반복을 감안할 때 훈련 데이터를 크게 암기할 수 있는 전형적인 심층 신경망의 매우 많은 매개 변수 때문입니다
A better approach is to split this data into three parts, the training split, the validation split, and the testing split
더 나은 접근 방식은 이 데이터를 훈련 분할, 검증 분할 및 테스트 분할의 세 부분으로 나누는 것입니다
As the name suggests, the training split is directly observed by the model during neural network training
이름에서 알 수 있듯이, 훈련 분할은 신경망 훈련 중에 모델에 의해 직접 관찰된다
The loss function is directly minimized on this training set
손실 기능은 이 훈련 세트에서 직접 최소화됩니다
But as we've stated earlier, we are expecting the value of this function to be very low over the set
하지만 앞서 언급했듯이, 우리는 이 함수의 가치가 세트보다 매우 낮을 것으로 예상하고 있다
The validation split is used by developers to test the performance of the neural network when hyperparameters are changed
검증 분할은 개발자가 하이퍼파라미터가 변경될 때 신경망의 성능을 테스트하는 데 사용됩니다
Hyperparameters are those parameters that either modify our network structure or affect our training process, but are not a part of the network parameters learned during training
하이퍼파라미터는 네트워크 구조를 수정하거나 교육 프로세스에 영향을 미치는 매개 변수이지만 교육 중에 배운 네트워크 매개 변수의 일부가 아닙니다
Examples include; the learning rate, the number of layers, the number of units per layer, and the activation function type
예로는 학습 속도, 레이어 수, 레이어당 단위 수 및 활성화 기능 유형이 포함됩니다
The final split is called the testing split and is used to get an unbiased estimate of performance
최종 분할은 테스트 분할이라고 불리며 성능에 대한 편견 없는 추정치를 얻는 데 사용됩니다
The test splits should be off limits when developing a neural network architecture so that the neural network never sees this data during the training or hyperparameter optimization process
신경망이 훈련이나 하이퍼파라미터 최적화 과정에서 이 데이터를 볼 수 없도록 신경망 아키텍처를 개발할 때 테스트 분할은 제한을 벗어나야 합니다
The only use of the test set should be to evaluate the performance of the final architecture and hyperparameter set before it is deployed on a self-driving vehicle
테스트 세트의 유일한 사용은 자율주행 차량에 배치되기 전에 최종 아키텍처와 하이퍼파라미터 세트의 성능을 평가하는 것이다
Let us now determine what percentage of data goes into each split
이제 각 분할에 몇 퍼센트의 데이터가 들어가는지 결정합시다
Before the big data error, it was common to have datasets on the order of thousands of examples
빅데이터 오류가 발생하기 전에, 수천 개의 예제의 순서에 데이터 세트를 갖는 것이 일반적이었다
In that case, the default percentage of data that goes into each split was approximately 60 percent for training, 20 percent for validation, and 20 percent held in reserve for testing
이 경우, 각 분할에 들어가는 데이터의 기본 비율은 훈련의 경우 약 60%, 검증의 경우 20%, 테스트를 위해 예비된 20%였다
However, nowadays, it is not uncommon to have datasets on the order of millions of examples having 20 percent of the data in the validation and test sets is unnecessary as the validation and test would contain far more samples than are needed for the purpose
그러나, 오늘날, 검증과 테스트 세트에 필요한 것보다 훨씬 더 많은 샘플을 포함할 것이기 때문에 검증과 테스트 세트에 데이터의 20%를 가진 수백만 개의 예제의 순서에 데이터셋을 갖는 것은 드문 일이 아니다
In such cases, we would find that a training set of 98 percent of the data with a validation and test set of one percent of the data each is not uncommon
그러한 경우, 우리는 데이터의 1%의 검증 및 테스트 세트를 가진 데이터의 98%의 훈련 세트가 드문 일이 아니라는 것을 알게 될 것이다
Let us go back to our traffic sign detection problem
교통 표지판 탐지 문제로 돌아가자
We assume that our traffic sign dataset is comprised of 10,000 labeled examples
우리는 트래픽 신호 데이터 세트가 10,000개의 라벨이 붙은 예시로 구성되어 있다고 가정합니다
We can separate our dataset into a training validation and testing split according to the 602020 small dataset heuristic
602020 소형 데이터 세트 휴리스틱에 따라 데이터셋을 교육 검증 및 테스트 분할로 분리할 수 있습니다
We now evaluate the performance of our neural network on each of these splits using the loss function
우리는 이제 손실 기능을 사용하여 이러한 각 분할에 대한 신경망의 성능을 평가합니다
For a classification problem, the loss function is defined as the cross entropy between the prediction and the ground truth labels
분류 문제의 경우, 손실 함수는 예측과 지상 진실 라벨 사이의 교차 엔트로피로 정의됩니다
Cross entropy is strictly greater than zero, so the higher its value, the worse the performance of our classifier
교차 엔트로피는 엄격하게 0보다 크므로, 값이 높을수록 분류기의 성능이 더 나빠집니다
Keep in mind that the neural network only directly observes the training set
신경망은 훈련 세트만 직접 관찰한다는 것을 명심하세요
All the developers use the validation set to determine the best hyperparameters to use
모든 개발자는 유효성 검사 세트를 사용하여 사용하기에 가장 적합한 하이퍼파라미터를 결정합니다
The ultimate goal of the training is still minimizing the error on the test set since it is an unbiased estimate of performance of our system and the data has never been observed by the network
교육의 궁극적인 목표는 시스템의 성능에 대한 편견 없는 추정치이며 네트워크에서 데이터를 관찰한 적이 없기 때문에 테스트 세트의 오류를 최소화하는 것입니다
Let us first consider the following scenario
먼저 다음 시나리오를 고려해 봅시다
Let us assume that our estimator gave a cross entropy loss of 0
우리의 추정기가 훈련 세트에서 0
21 on the training set, and a loss of 0
21의 교차 엔트로피 손실과 검증 세트에서 0
25 on the validation set, and finally, a loss of 0
25의 손실, 그리고 마지막으로 테스트 세트에서 0
3 on the test set
3의 손실을 주었다고 가정해 봅시다
Furthermore, due to errors in the labels of the dataset, the minimum cross entropy loss that we can expect is 0
게다가, 데이터 세트 라벨의 오류로 인해, 우리가 기대할 수 있는 최소 교차 엔트로피 손실은 0
18
18이다
In this case, we have quite a good classifier as the loss on the three sets are fairly consistent and the loss is close to the minimum achievable loss on the entire task
이 경우, 우리는 세 세트의 손실이 상당히 일관되고 손실이 전체 작업의 최소 달성 가능한 손실에 가깝기 때문에 꽤 좋은 분류기를 가지고 있습니다
Let's consider a second scenario where the training loss is now 1
훈련 손실이 최소 손실의 약 10배인 두 번째 시나리오를 생각해 봅시다
9 around ten times that of the minimum loss
이전 수업에서 논의했듯이, 우리는 합리적인 크기의 신경망이 충분한 훈련 시간이 주어진 데이터에 거의 완벽하게 맞출 수 있을 것으로 기대합니다
As we discussed in the previous lesson, we expect any reasonably sized neural network to be able to almost perfectly fit the data given enough training time
하지만 이 경우, 네트워크는 그렇게 할 수 없었다
But in this case, the network was not able to do so
우리는 신경망이 훈련 손실을 과소평가하지 못하는 이 시나리오라고 부른다
We call this scenario where the neural network fails to bring the training loss down underfitting
우리가 직면할 수 있는 또 다른 시나리오는 훈련 세트 손실이 낮지만 검증과 테스트 세트 손실이 높을 때이다
One other scenario we might face is when we have a low training set loss but a high validation and testing set loss
예를 들어, 검증 손실이 훈련 손실의 약 10배인 경우에 도달할 수 있습니다
For example, we might arrive at the case where the validation loss is around ten times that of the training loss
이 경우는 과적합이라고 하며 신경망이 훈련 데이터 출력을 정확하게 재현하기 위해 매개 변수를 최적화함으로써 발생합니다
This case is referred to as overfitting and is caused by the neural network optimizing its parameters to precisely reproduce the training data output
검증 세트에 배포할 때, 네트워크는 새 데이터로 잘 일반화할 수 없습니다
When we deploy on the validation set, the network cannot generalize well to the new data
훈련과 검증 손실 사이의 격차는 일반화 격차라고 불린다
The gap between training and validation loss is called the generalization gap
우리는 훈련 손실이 충분히 낮으면서도 이 격차가 가능한 한 낮기를 원한다
We want this gap to be as low as possible while still having low enough training loss
우리가 어떻게 속옷이나 과장 정권에서 좋은 추정치로 갈 수 있는지 봅시다
Let's see how we can try to go from the underfitting or overfitting regime to a good estimator
우리는 부합을 치료하는 방법부터 시작한다
We begin with how to remedy underfitting
부합을 치료하는 첫 번째 옵션은 더 오래 훈련하는 것이다
The first option to remedy underfitting is to train longer
아키텍처가 당면한 작업에 적합하다면, 더 긴 훈련은 보통 더 낮은 훈련 손실로 이어진다
If the architecture is suitable for the task at hand, training longer usually leads to a lower training loss
아키텍처가 너무 작다면, 더 긴 훈련은 도움이 되지 않을 수 있다
If the architecture is too small, training longer might not help
이 경우, 신경망에 더 많은 레이어를 추가하거나 레이어당 더 많은 매개 변수를 추가하고 싶습니다
In that case, you would want to add more layers to your neural network or add more parameters per layer
위의 두 옵션 모두 도움이 되지 않는다면, 아키텍처는 당면한 작업에 적합하지 않을 수 있으며, 피팅을 줄이기 위해 다른 아키텍처를 시도하고 싶을 것입니다
If both of the above options don't help, your architecture might not be suitable for the task at hand and you would want to try a different architecture to reduce underfitting
이제, 과적합을 줄이기 위한 가장 일반적인 접근 방식으로 진행합시다
Now, let's proceed to the most common approaches to reduce overfitting
과적합의 경우, 가장 쉬운 방법은 더 많은 데이터를 수집하는 것이다
In the case of overfitting, the easiest thing to do is to just collect more data
불행히도, 자율주행 자동차의 경우, 데이터 수집을 위한 엔지니어링 시간과 실제 출력을 올바르게 정의하는 데 엄청난 양의 주석기 시간이 필요하기 때문에 훈련 데이터를 수집하는 것은 매우 비쌉니다
Unfortunately, for self-driving cars, collecting training data is very expensive as it requires engineering time for data collection and a tremendous amount of annotator time to properly define the true outputs
과적합을 위한 또 다른 해결책은 정규화이다
Another solution for overfitting is regularization
정규화는 일반화 격차를 낮추려는 의도로 학습 알고리즘에 대한 수정이지만 훈련 손실은 아니다
Regularization is any modification made to the learning algorithm with an intention to lower the generalization gap but not the training loss
다른 모든 것이 실패하면, 최종 해결책은 아키텍처를 다시 방문하여 당면한 작업에 적합한지 확인하는 것입니다
If all else fails, the final solution is to revisit the architecture and check if it is suitable for the task at hand
이 수업에서, 우리는 훈련, 검증 및 테스트 분할에서 신경망의 다양한 성능 시나리오를 해석하는 방법을 배웠습니다
In this lesson, we have learned how to interpret the different performance scenarios of our neural network on the training, validation, and test splits
우리 네트워크가 적합하지 않다고 판단되면, 가장 쉬운 해결책은 더 오래 훈련하거나 더 큰 신경망을 사용하는 것이다
If it is determined that our network is underfitting, the easiest solution is to train for a longer time or to use a larger neural network
그러나 자율주행 자동차 인식에서 훨씬 더 일반적으로 직면한 시나리오는 훈련 데이터의 좋은 성능이 항상 실제 로봇에서 좋은 성능으로 전환되지 않는 곳에 과장되고 있다
However, a much more commonly faced scenario in self-driving car perception is overfitting where good performance on the training data does not always translate to good performance on actual robots
다음 수업에서, 우리는 다양한 정규화 전략으로 과복합의 영향을 완화하는 방법에 초점을 맞출 것이다
In the next lesson, we'll focus on how to mitigate the effects of overfitting with various regularization strategies
이러한 전략을 통해 라벨이 지정되지 않은 데이터 세트를 능가하도록 훈련된 인식 알고리즘이 우리 주변의 끊임없이 변화하는 세계를 운전할 때 계속 잘 작동할 수 있습니다
These strategies will allow perception algorithms trained to excel unlabeled datasets to continue to work well when driving through the ever-changing world around us



