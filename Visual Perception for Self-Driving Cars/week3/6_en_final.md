If you've been monitoring the latest news on self-driving cars, you would have heard the phrase convolutional neural networks or ConvNets for short at least a few times
자율주행 자동차에 대한 최신 뉴스를 모니터링해 왔다면, 컨볼루션 신경망이나 ConvNets라는 문구를 적어도 몇 번은 들었을 것입니다
In fact, we currently use ConvNets to perform a multitude of perception tasks on our own self-driving car the autonomoose
사실, 우리는 현재 ConvNets를 사용하여 자율주행 자동차 자율주행 자동차에서 수많은 인식 작업을 수행합니다
In this lesson, we will take a deeper look at these fascinating architectures to understand their importance for visual perception
이 수업에서, 우리는 시각적 인식의 중요성을 이해하기 위해 이러한 매혹적인 아키텍처를 더 깊이 살펴볼 것이다
Specifically, you will learn how convolutional layers use cross-correlation instead of general matrix multiplication to tailor neural networks for image input data
특히, 컨볼루션 레이어가 이미지 입력 데이터에 대한 신경망을 조정하기 위해 일반 매트릭스 곱셈 대신 상호 상관 관계를 사용하는 방법을 배우게 될 것입니다
We'll also cover the advantages these models incur over standard feed-forward neural networks
우리는 또한 이러한 모델이 표준 피드 포워드 신경망에 비해 발생하는 이점을 다룰 것입니다
Convolutional neural networks are a specialized kind of neural network for processing data that has a known grid-like topology
컨볼루션 신경망은 알려진 그리드와 같은 토폴로지를 가진 데이터를 처리하기 위한 특화된 종류의 신경망이다
Examples of such data can be 1D time-series data sampled at regular intervals, 2D images or even 3D videos
이러한 데이터의 예는 정기적으로 샘플링된 1D 시계열 데이터, 2D 이미지 또는 3D 비디오일 수 있습니다
ConvNets are mainly comprised of two types of layers; convolutional layers and pooling layers
ConvNets는 주로 두 가지 유형의 레이어로 구성되어 있다; 컨볼루션 레이어와 풀링 레이어
A simple example of a convNet architecture is VGG 16
convNet 아키텍처의 간단한 예는 VGG 16이다
This network takes in the image and passes it through a set of convolutional layers, a pooling layer, and another couple of convolutional layers, and then more pooling layers and convolutional layers and so on
이 네트워크는 이미지를 가져와 컨볼루션 레이어 세트, 풀링 레이어, 그리고 또 다른 몇 개의 컨볼루션 레이어, 그리고 더 많은 풀링 레이어와 컨볼루션 레이어 등을 통과합니다
Don't worry too much about the specifics of the VGG 16 architecture design for now, we will discuss this architecture in detail in a later video when we learn about object detection
지금은 VGG 16 아키텍처 디자인의 세부 사항에 대해 너무 걱정하지 마세요, 물체 감지에 대해 배울 때 나중에 비디오에서 이 아키텍처에 대해 자세히 논의할 것입니다
Let's see how these two types of layers work in practice
이 두 종류의 레이어가 실제로 어떻게 작동하는지 봅시다
The neural network, hidden layers we have described so far are usually called fully connected layers
우리가 지금까지 설명한 신경망, 숨겨진 층은 보통 완전히 연결된 계층이라고 불린다
As their name suggests, fully connected layers connect each node output to every node input in the next layer
이름에서 알 수 있듯이, 완전히 연결된 레이어는 각 노드 출력을 다음 레이어의 모든 노드 입력에 연결합니다
That means that every element of the input contributes to every element of the output
그것은 입력의 모든 요소가 출력의 모든 요소에 기여한다는 것을 의미한다
This is implemented in software through dense matrix multiplication
이것은 조밀한 행렬 곱셈을 통해 소프트웨어로 구현된다
Although counter-intuitive, convolutional layers use cross-correlation not convolutions for their linear operator instead of general matrix multiplication
직관에 어긋나는 컨볼루션 레이어는 일반 매트릭스 곱셈 대신 선형 연산자에 대한 컨볼루션이 아닌 교차 상관 관계를 사용한다
The logic behind using cross-correlation is that if the parameters are learned, it does not matter if we flip the output or not
상호 상관관계를 사용하는 논리는 매개 변수를 배우면 출력을 뒤집는지 여부는 중요하지 않다는 것이다
Since we are learning the weights of the convolutional layer, the flipping does not affect our results at all
우리는 컨볼루션 층의 가중치를 배우고 있기 때문에, 뒤집기는 우리의 결과에 전혀 영향을 미치지 않는다
This results in what we call sparse connectivity
이것은 우리가 희박한 연결이라고 부르는 것을 초래한다
Each input element to the convolutional layer only affects a few output elements, thanks to the use of a limited size kernel for the convolutional operation
컨볼루션 레이어에 대한 각 입력 요소는 컨볼루션 작업에 제한된 크기의 커널을 사용하기 때문에 몇 가지 출력 요소에만 영향을 미친다
Let's begin by describing how convolutional layers work in practice
컨볼루션 레이어가 실제로 어떻게 작동하는지 설명하는 것으로 시작합시다
We'll assume that we want to apply a convolutional layer to an input image
우리는 입력 이미지에 컨볼루션 레이어를 적용하고 싶다고 가정할 것이다
We will refer to this image as our input volume, as we will see convolutional layers taking output of other layers as their inputs as well
우리는 컨볼루션 레이어가 다른 레이어의 출력을 입력으로 받아들이는 것을 볼 것이기 때문에 이 이미지를 입력 볼륨이라고 부를 것입니다
The width of our input volume is its horizontal dimension, the height is its vertical dimension, and the depth is the number of channels
입력 볼륨의 너비는 수평 치수이고, 높이는 수직 치수이며, 깊이는 채널 수입니다
In our case, all three characteristics have a value of three
우리의 경우, 세 가지 특성 모두 세 가지 값을 가지고 있다
But why didn't we consider the gray pixels in our height or width computation
하지만 왜 우리는 높이 또는 너비 계산에서 회색 픽셀을 고려하지 않았나요
The gray pixels are added to the image through a process called padding
회색 픽셀은 패딩이라는 과정을 통해 이미지에 추가됩니다
The number of pixels added on each side is called the padding size in this case one
양쪽에 추가된 픽셀 수는 이 경우 패딩 크기라고 불린다
Padding is essential for retaining the shape required to perform the convolutions
패딩은 컨볼루션을 수행하는 데 필요한 모양을 유지하는 데 필수적이다
We perform the convolution operations through a set of kernels or filters
우리는 커널이나 필터 세트를 통해 컨볼루션 작업을 수행합니다
Each Filter is comprised of a set of weights and a single bias
각 필터는 가중치 세트와 단일 바이어스로 구성되어 있다
The number of channels of the kernel needs to correspond to the number of channels of the input volume
커널의 채널 수는 입력 볼륨의 채널 수에 해당해야 합니다
In this case, we have three weight channels per filter corresponding to red, green, and blue channels of the input image
이 경우, 입력 이미지의 빨간색, 녹색 및 파란색 채널에 해당하는 필터당 세 개의 무게 채널이 있습니다
Usually we have multiple filters per convolutional layer
보통 우리는 컨볼루션 레이어당 여러 개의 필터를 가지고 있다
Let's see how to apply our two filters to get an output volume from our input volume
입력 볼륨에서 출력 볼륨을 얻기 위해 두 개의 필터를 적용하는 방법을 봅시다
We start by taking each channel of the filter and perform cross-correlation between that channel and its corresponding channel in the input volume
우리는 필터의 각 채널을 취하고 입력 볼륨에서 해당 채널과 해당 채널 간의 상호 상관 관계를 수행합니다
We then proceed to add the output of the cross-correlation of all channels with the bias of the filter to arrive at the final output value
그런 다음 모든 채널의 상호 상관 관계의 출력을 필터의 편향과 추가하여 최종 출력 값에 도달합니다
Notice that we get one output channel per filter
필터당 하나의 출력 채널을 얻는다는 것을 주목하세요
We will get back to this point in a bit
우리는 조금 있다가 이 지점으로 돌아갈 것이다
Let's now see how to get the rest of the output volume
이제 나머지 출력 볼륨을 얻는 방법을 봅시다
After we're done with the first computation, we shift the filter location by a preset number of pixels horizontally
첫 번째 계산을 마친 후, 필터 위치를 사전 설정된 수의 픽셀 수로 수평으로 이동합니다
When we reach the end of the input volume width, we shift the filter location by a preset number of pixels vertically
입력 볼륨 너비의 끝에 도달하면, 필터 위치를 미리 설정된 수의 픽셀로 수직으로 이동합니다
The vertical and horizontal shifts are usually the same value, and we refer to this value as the stride of our convolutional layer
수직 및 수평 변화는 일반적으로 동일한 값이며, 우리는 이 값을 컨볼루션 층의 보폭이라고 부릅니다
We arrive to a final output volume with its own width, depth, and height values
우리는 자체 너비, 깊이 및 높이 값을 가진 최종 출력 볼륨에 도달합니다
Assuming that the filters are M by M, and we have K filters, a stride of S, a padding P, we can derive expressions for the width, height, and depth of our output volume
필터가 M by M이고 K 필터, S의 보폭, 패딩 P가 있다고 가정하면 출력 볼륨의 너비, 높이 및 깊이에 대한 표현을 도출할 수 있습니다
You would think this gets challenging to keep track of, but when designing ConvNets, it is very important to know what size output layers you'll end up with
당신은 이것이 추적하기 어렵다고 생각하겠지만, ConvNets를 설계할 때, 어떤 크기의 출력 레이어로 끝날지 아는 것이 매우 중요합니다
As an example, you don't want to reduce the size of your output volume too much if you are trying to detect small traffic signs and traffic lights on road scenes
예를 들어, 도로 장면에서 작은 교통 표지판과 신호등을 감지하려고 한다면 출력 볼륨의 크기를 너무 많이 줄이고 싶지 않습니다
They only occupy a small number of pixels in the image, and their visibility might get lost if the output volume is too compact
이미지에서 소수의 픽셀만 차지하며, 출력 볼륨이 너무 컴팩트하면 가시성이 손실될 수 있습니다
Let us now continue to describe the second building block of ConvNets, pooling layers
이제 ConvNets의 두 번째 빌딩 블록인 풀링 레이어를 계속 설명합시다
A pooling layer uses pooling functions to replace the output of the previous layer with a summary statistic of the nearby outputs
풀링 레이어는 풀링 함수를 사용하여 이전 레이어의 출력을 인근 출력의 요약 통계로 대체합니다
Pooling helps make the representations become invariant to small translations of the input
풀링은 표현을 입력의 작은 번역에 불변하게 만드는 데 도움을 준다
If we translate the input a small amount, the output of the pooling layer will not change
입력을 소량으로 번역하면 풀링 레이어의 출력은 변경되지 않습니다
This is important for object recognition for example, as if we shift a car a small amount in an image space, it should still be recognizable as a car
이것은 물체 인식에 중요합니다
Let us take an example of the most commonly used pooling layer, Max pooling
예를 들어, 이미지 공간에서 차를 소량으로 옮기는 것처럼, 여전히 자동차로 인식할 수 있어야 합니다
Max pooling summarizes output volume patches with the max function
가장 일반적으로 사용되는 풀링 레이어인 맥스 풀링의 예를 들어 봅시다
Given the input volume in gray, Max Pooling applies the max function to an M by M region, then shifts this region in strides similar to the convolutional layer
최대 풀링은 최대 함수로 출력 볼륨 패치를 요약합니다
Once again we can derive expressions for the output width, height, and depth of the pooling layers according to the following equations
회색의 입력 볼륨을 감안할 때, 최대 풀링은 M by M 영역에 최대 함수를 적용한 다음, 컨볼루션 레이어와 유사한 보폭으로 이 영역을 이동합니다
In our previous example, the filter size M is two, and we get a stride of two, so we end up with a two-by-two output
다시 한번 우리는 다음 방정식에 따라 풀링 레이어의 출력 너비, 높이 및 깊이에 대한 표현식을 도출할 수 있습니다
Let's see how this pooling layer can help us with translation invariance
이전 예에서, 필터 크기 M은 2이고, 우리는 2의 보폭을 얻으므로, 우리는 2 x 2 출력으로 끝납니다
As an example, let's shift the previous input volume by one pixel
이 풀링 레이어가 번역 불변성에 어떻게 도움이 될 수 있는지 봅시다
The added pixels due to the shift are shown in blue, whereas the removed pixels are shown in red
예를 들어, 이전 입력 볼륨을 1픽셀로 바꾸자
We can go ahead and apply Max Pooling to this input volume, as we did in the previous slide
시프트로 인해 추가된 픽셀은 파란색으로 표시되는 반면, 제거된 픽셀은 빨간색으로 표시됩니다
When comparing our new output to the original volume output, we find that only one element has changed
이전 슬라이드에서 했던 것처럼 이 입력 볼륨에 Max Pooling을 적용할 수 있습니다
So far, we've discussed how ConvNets operate but still did not provide a reason for their usefulness in the context of self-driving cars
새 출력을 원래 볼륨 출력과 비교할 때, 우리는 하나의 요소만 변경되었다는 것을 알게 된다
There are really two important reasons for the effectiveness of ConvNets
지금까지, 우리는 ConvNets가 어떻게 작동하는지 논의했지만 여전히 자율주행 자동차의 맥락에서 유용성에 대한 이유를 제공하지 않았다
First, they usually have far fewer parameters in their convolutional layers than a similar network with fully connected layers
ConvNets의 효과에는 정말 두 가지 중요한 이유가 있다
This reduces the chance of over-fitting through parameters sharing, and allows ConvNets to operate on larger images
첫째, 그들은 보통 완전히 연결된 계층이 있는 유사한 네트워크보다 컨볼루션 레이어에 매개 변수가 훨씬 적다
Perhaps more importantly, is translation invariance
이것은 매개 변수 공유를 통해 과도하게 피팅할 가능성을 줄이고 ConvNets가 더 큰 이미지에서 작동할 수 있게 해준다
By using the same parameters to process every block of the image, ConvNets are capable of detecting an object or classifying a pixel even if it is shifted with a translation on the image plane
아마도 더 중요한 것은 번역 불변성이다
This means we can detect cars wherever they appear
동일한 매개 변수를 사용하여 이미지의 모든 블록을 처리함으로써 ConvNets는 이미지 평면에서 번역으로 이동하더라도 물체를 감지하거나 픽셀을 분류할 수 있습니다
Before we end this lesson, I would like to shed light on the history of convolutional neural networks
이것은 우리가 자동차가 어디에 나타나든 감지할 수 있다는 것을 의미한다
Convolutional neural networks have played an important role in the history of deep learning
이 수업을 끝내기 전에, 나는 컨볼루션 신경망의 역사를 밝히고 싶다
As a matter of fact, ConvNets were one of the first neural network models to perform well at a time where other feed-forward architectures failed, particularly on image classification tasks related to the ImageNet dataset
컨볼루션 신경망은 딥 러닝의 역사에서 중요한 역할을 해왔다
In many ways, ConvNets carry the torch for the rest of deep learning, and pave the way to the relatively new acceptance of neural networks in general
사실, ConvNets는 특히 ImageNet 데이터 세트와 관련된 이미지 분류 작업에서 다른 피드 포워드 아키텍처가 실패한 시기에 잘 수행된 최초의 신경망 모델 중 하나였다
Finally, convolutional networks were some of the first neural networks to solve important commercial applications, the most famous being Yann LeCun's handwritten digit recognizer in the early nineties, and remain at the forefront of commercial applications of deep learning today
여러 면에서, ConvNets는 나머지 딥 러닝을 위해 횃불을 들고 있으며, 일반적으로 신경망의 비교적 새로운 수용으로 가는 길을 닦는다
In fact, in the next week of this course, we will show you how to use ConvNets to detect a range of different objects in roads scenes, 2D object detection
마지막으로, 컨볼루션 네트워크는 중요한 상용 애플리케이션을 해결한 최초의 신경망 중 일부였으며, 가장 유명한 것은 90년대 초 Yann LeCun의 필기 숫자 인식기이며, 오늘날 딥 러닝의 상업적 적용의 최전선에 남아 있다
We'll see you then
사실, 이 과정의 다음 주에는 ConvNets를 사용하여 도로 장면에서 다양한 물체, 2D 물체 감지를 감지하는 방법을 보여드리겠습니다

그럼 그때 보자


