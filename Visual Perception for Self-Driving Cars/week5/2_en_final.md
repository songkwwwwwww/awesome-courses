In the first lesson of this module, we define the semantic segmentation problem and saw how to evaluate the performance of semantic segmentation algorithm by calculating the class IOU
이 모듈의 첫 번째 수업에서, 우리는 의미론적 세분화 문제를 정의하고 클래스 IOU를 계산하여 의미론적 세분화 알고리즘의 성능을 평가하는 방법을 보았다
In this video, we will learn how to use convolutional neural networks to perform the semantic segmentation task
이 비디오에서, 우리는 컨볼루션 신경망을 사용하여 의미론적 세분화 작업을 수행하는 방법을 배울 것입니다
Using confidence for semantic segmentation is actually a little easier than using them for object detection
의미론적 세분화에 자신감을 사용하는 것은 실제로 물체 감지에 사용하는 것보다 조금 쉽다
Unlike ConvNets for object detection, the training and inference stages are practically the same for semantic segmentation
물체 감지를 위한 ConvNets와 달리, 훈련과 추론 단계는 의미론적 세분화를 위해 실질적으로 동일하다
However, there are some intricacies to semantic segmentation that we need to be aware of
그러나, 우리가 알아야 할 의미론적 세분화에 대한 복잡성도 있다
Let's begin with a quick review of the semantic segmentation problem
의미론적 세분화 문제에 대한 빠른 검토부터 시작합시다
Semantic segmentation takes a camera images input and provides a category classification for every pixel in that image as output
시맨틱 세분화는 카메라 이미지 입력을 취하고 해당 이미지의 모든 픽셀에 대한 카테고리 분류를 출력으로 제공합니다
This problem can be modeled as a function approximation problem, and ConvNets can once again be used to approximate the required function
이 문제는 함수 근사치 문제로 모델링될 수 있으며, ConvNets는 필요한 함수를 근사하는 데 다시 한 번 사용될 수 있다
What kind of ConvNet model can we use to perform this function approximation
이 함수 근사치를 수행하기 위해 어떤 종류의 ConvNet 모델을 사용할 수 있나요
One idea is to use the same ConvNet model we used for object detection
한 가지 아이디어는 우리가 물체 감지에 사용한 것과 동일한 ConvNet 모델을 사용하는 것이다
That is, a feature extractor followed by an output layer
즉, 기능 추출기 뒤에 출력 레이어가 뒤따른다
We do not need anchors here as we are not trying to localize objects
우리는 물체를 현지화하려고 하지 않기 때문에 여기에 앵커가 필요하지 않습니다
Let's see how effective this architecture is for performing semantic segmentation
이 아키텍처가 의미론적 세분화를 수행하는 데 얼마나 효과적인지 봅시다
You'll start by analyzing the feature extractor
기능 추출기를 분석하는 것으로 시작하겠습니다
As with the feature extractor used for object detections, we can use the VGG architecture
물체 감지를 위해 사용되는 기능 추출기와 마찬가지로, 우리는 VGG 아키텍처를 사용할 수 있습니다
Let's see what happens to the size of M by N by three input image, as we go through this feature extractor
이 기능 추출기를 거치면서 M x N의 크기에 3개의 입력 이미지가 어떻게 되는지 봅시다
As with object detection, our resolution will be reduced by half after every pooling layer
물체 감지와 마찬가지로, 우리의 해상도는 모든 풀링 레이어 후에 절반으로 줄어들 것이다
On the other hand, our depth will increase due to the convolutional layers
반면에, 우리의 깊이는 컨볼루션 층으로 인해 증가할 것이다
The output feature map of our convolutional feature extractor will be downsampled by 16 times
우리의 컨볼루션 피처 추출기의 출력 피처 맵은 16번 다운샘플링될 것이다
We can add as many convolutional pooling blocks as needed, but that will further shrink our feature map
우리는 필요한 만큼의 컨볼루션 풀링 블록을 추가할 수 있지만, 그것은 우리의 기능 맵을 더욱 축소시킬 것이다
However, we want our output to have a classification for every pixel in the image
그러나, 우리는 우리의 출력이 이미지의 모든 픽셀에 대해 분류되기를 원한다
So how can we achieve this given a down sampled feature map that is 16 times smaller than our original input
그렇다면 원래 입력보다 16배 작은 다운 샘플링 기능 맵을 감안할 때 이것을 어떻게 달성할 수 있을까요
A simple solution would be the following
간단한 해결책은 다음과 같다
We can first compute the output by passing the 16 times downsampled output feature map through a softmax layer
먼저 소프트맥스 레이어를 통해 16번의 다운샘플링된 출력 기능 맵을 전달하여 출력을 계산할 수 있습니다
We can then determine the class of every pixel in the subsampled output by taking the highest class score obtained by the softmax layer
그런 다음 소프트맥스 레이어가 얻은 가장 높은 클래스 점수를 취하여 서브샘플링된 출력의 모든 픽셀의 클래스를 결정할 수 있습니다
The final step would be to proceed to upsample, the downsampled output back to the original image resolution
마지막 단계는 다운샘플링된 출력을 원래 이미지 해상도로 되돌리는 것이다
How well do you think the described approach will work
설명된 접근 방식이 얼마나 잘 작동할 것이라고 생각하십니까
To understand why naive upsampling might produce inadequate results, let's take a look at how upsampling increases the image resolution
왜 순진한 업샘플링이 부적절한 결과를 낳을 수 있는지 이해하려면, 업샘플링이 이미지 해상도를 어떻게 증가시키는지 살펴봅시다
We want to use the nearest neighbor upsampling on a two-by-two image patch
우리는 2 x 2 이미지 패치에 가장 가까운 이웃 업샘플링을 사용하고 싶습니다
The color of the pixels of the image patch represent different values of every pixel
이미지 패치의 픽셀 색상은 모든 픽셀의 다른 값을 나타냅니다
We want to upsample our patch to double its original size
우리는 원래 크기를 두 배로 늘리기 위해 패치를 업샘플링하고 싶습니다
So have an upsampling multiplier S of two
그래서 두 개의 업샘플링 승수 S를 가지세요
Nearest neighbor upsampling generates an empty initial upsampled grid by multiplying Win an Hin by the upsampling multiplier
가장 가까운 이웃 업샘플링은 Win an Hin에 업샘플링 승수를 곱하여 빈 초기 업샘플링 그리드를 생성합니다
Each pixel in the upsampled grid is then filled with the value of the nearest pixel in the original image patch
그런 다음 업샘플링된 그리드의 각 픽셀은 원본 이미지 패치에서 가장 가까운 픽셀 값으로 채워집니다
This process is repeated until all the pixels in the upsampled grid are filled with values from the image patch
이 과정은 업샘플링된 그리드의 모든 픽셀이 이미지 패치의 값으로 채워질 때까지 반복됩니다
The depth of the output upsampled grid remains the same as the input image patch
출력 업샘플링 그리드의 깊이는 입력 이미지 패치와 동일하게 유지됩니다
The problem induced by upsampling is that the upsampled output image has very coarse boundaries
업샘플링에 의해 유발된 문제는 업샘플링된 출력 이미지가 매우 거친 경계를 가지고 있다는 것이다
As you can remember from the last lesson, one of the most challenging problems in semantic segmentation is attaining smooth and accurate boundaries around the objects
마지막 수업에서 기억할 수 있듯이, 의미론적 세분화에서 가장 어려운 문제 중 하나는 물체 주변의 매끄럽고 정확한 경계를 달성하는 것입니다
Smooth boundaries are hard to attain as in general boundaries in the image space are ambiguous, especially for thin objects such as pools, similar looking objects such as roads and sidewalks, and far away objects
이미지 공간의 일반적인 경계에서 특히 수영장과 같은 얇은 물체, 도로와 보도와 같은 비슷한 모양의 물체, 멀리 떨어진 물체의 경우 모호하기 때문에 부드러운 경계는 달성하기 어렵다
Naive upsampling also induces two additional problems
순진한 업샘플링은 또한 두 가지 추가적인 문제를 유발한다
Any object less than 16 pixels in width or height usually fully disappears in their upsampled image
너비나 높이가 16픽셀 미만인 물체는 일반적으로 업샘플링된 이미지에서 완전히 사라집니다
This affects both thin objects such as pools and far away objects
이것은 풀과 멀리 떨어진 물체와 같은 얇은 물체 모두에 영향을 미친다
As they are below the minimum dimensions required for the pixels to appear from the original image
픽셀이 원본 이미지에서 나타나는 데 필요한 최소 치수보다 낮기 때문입니다
To remedy these problems, researchers have formulated what is commonly referred to as a feature decoder
이러한 문제를 해결하기 위해, 연구자들은 일반적으로 기능 디코더라고 불리는 것을 공식화했다
The feature decoder can be thought of as a mirror image of the feature extractor
기능 디코더는 기능 추출기의 거울 이미지로 생각할 수 있다
Instead of using the convolution pooling paradigm to downsample the resolution, it uses upsampling layers followed by a convolutional layer to upsample the resolution of the feature map
컨볼루션 풀링 패러다임을 사용하여 해상도를 다운샘플링하는 대신, 업샘플링 레이어와 컨볼루션 레이어를 사용하여 기능 맵의 해상도를 업샘플링합니다
The upsampling usually using nearest neighbor methods achieves the opposite effect to pooling, but results in an inaccurate feature map
일반적으로 가장 가까운 이웃 방법을 사용하는 업샘플링은 풀링과 반대의 효과를 얻지만, 부정확한 기능 맵을 초래한다
The following convolutional layers are then used to correct the features in the upsampled feature map with learnable filter banks
그런 다음 다음 컨볼루션 레이어는 학습 가능한 필터 뱅크로 업샘플링된 기능 맵의 기능을 수정하는 데 사용됩니다
This correction usually provides the required smooth boundaries as we go forward through the feature decoder
이 수정은 일반적으로 기능 디코더를 진행할 때 필요한 부드러운 경계를 제공합니다
Let's now go through an analysis of the dimensions of the feature map as it travels forward through the feature decoder
이제 기능 디코더를 통해 앞으로 이동하면서 기능 맵의 크기를 분석해 봅시다
As a reminder, the input feature map is downsampled 16 times with a depth of 512
다시 말씀드리지만, 입력 기능 맵은 깊이 512로 16번 다운샘플링됩니다
Similar to the feature extractor, each upsampling convolution block is referred to as a deconvolution
기능 추출기와 마찬가지로, 각 업샘플링 컨볼루션 블록은 디컨볼루션이라고 불린다
There is of course a debate among current researchers on whether this terminology is accurate
물론 현재 연구자들 사이에서 이 용어가 정확한지에 대한 논쟁이 있다
But we will use it here to refer to the reverse of the convolutional pooling block
하지만 우리는 컨볼루션 풀링 블록의 반대를 언급하기 위해 그것을 사용할 것이다
As we go through the first deconvolution block, our input feature map is upsampled to twice the input resolution
첫 번째 디컨볼루션 블록을 거치면서, 우리의 입력 기능 맵은 입력 해상도의 두 배로 업샘플링됩니다
The depth is controlled by how many filters are defined for each successive convolutional layer
깊이는 각 연속적인 컨볼루션 레이어에 대해 정의된 필터의 수에 따라 제어됩니다
As we go forward through the rest of the decoder, we finally arrive at a feature map of similar resolution to the input image
나머지 디코더를 진행하면서, 우리는 마침내 입력 이미지와 비슷한 해상도의 기능 지도에 도달합니다
For reduced computational complexity, we usually shrink the depth of the map as we go forward
계산 복잡성을 줄이기 위해, 우리는 보통 앞으로 나아갈 때 지도의 깊이를 줄인다
But this is a design choice that depends on your application
하지만 이것은 당신의 응용 프로그램에 따라 달라지는 디자인 선택입니다
Note, this upsampling mechanism is the simplest among many of the proposed methods for semantic segmentation
이 업샘플링 메커니즘은 제안된 많은 의미 세분화 방법 중 가장 간단합니다
Please take a look at the supplementary material provided for more efficient, powerful, and complex upsampling models that have been proposed for semantic segmentation
의미 세분화를 위해 제안된 보다 효율적이고 강력하며 복잡한 업샘플링 모델을 위해 제공된 보충 자료를 살펴보세요
Now that we have a similar sized feature map to our input image, we need to generate the semantic segmentation output
이제 입력 이미지와 비슷한 크기의 기능 맵을 가지고 있으므로, 의미론적 세분화 출력을 생성해야 합니다
We can perform semantic segmentation through a linear output layer, followed by a softmax function
선형 출력 레이어를 통해 시맨틱 세분화를 수행하고 소프트맥스 함수를 수행할 수 있습니다
This layer is very similar to the classification output layer we described in object detection
이 레이어는 객체 탐지에서 설명한 분류 출력 레이어와 매우 유사합니다
In fact, this layer provides a k-dimensional vector per pixel with the kth element being how confident the neural network is that the pixel belongs to the kth class
사실, 이 레이어는 픽셀당 k차원 벡터를 제공하며 kth 요소는 신경망이 픽셀이 kth 클래스에 속한다는 것을 얼마나 확신하는지 알고 있다
Let's investigate the expected output visually
예상 출력을 시각적으로 조사해 봅시다
Given an image patch and its corresponding ground truth label, we can represent each pixel as a k-dimensional one-hot vector
이미지 패치와 해당 지상 진실 라벨이 주어지면, 우리는 각 픽셀을 k차원 원샷 벡터로 표현할 수 있습니다
A one hot vector assigns the value of one to the correct class and zero to the remaining classes
하나의 핫 벡터는 하나의 값을 올바른 클래스에 할당하고 나머지 클래스에 0을 할당합니다
Since only that one value is non-zero or hot
그 하나의 값만이 0이 아니거나 뜨겁기 때문이다
In this case, we have two classes and a background class, so we are working with a three-dimensional ground truth vector per pixel
이 경우, 우리는 두 개의 클래스와 배경 클래스가 있으므로 픽셀당 3차원 지상 진실 벡터로 작업하고 있습니다
The neural network drives the output of the softmax to be as close to one as possible for the correct class, and is close to zero as possible for the rest of the classes for each pixel
신경망은 softmax의 출력을 올바른 클래스에 대해 가능한 한 가깝게 구동하며, 각 픽셀의 나머지 클래스에 대해 가능한 한 0에 가깝다
We then take the index of the maximum score to recover the required output representation
그런 다음 필요한 출력 표현을 복구하기 위해 최대 점수의 인덱스를 가져옵니다
Note however, that we only perform this step during inference
그러나, 우리는 추론 중에만 이 단계를 수행한다는 점에 유의하십시오
For training, we use the softmax output score directly
훈련을 위해, 우리는 softmax 출력 점수를 직접 사용합니다
The problem of semantic segmentation by definition requires the neural network to provide a single class for every pixel classification
정의상 의미론적 세분화의 문제는 신경망이 모든 픽셀 분류에 대해 단일 클래스를 제공하도록 요구한다
To learn how to perform this task, the cross entropy classification loss is used to train the neural network once again
이 작업을 수행하는 방법을 배우기 위해, 교차 엔트로피 분류 손실은 신경망을 다시 한 번 훈련시키는 데 사용됩니다
This loss is similar to the one we used for the object detection classification hit
이 손실은 우리가 물체 감지 분류 히트를 위해 사용한 것과 비슷하다
Cross entropy drives the neural network to learn a probability distribution per pixel that is closest to the ground truth class probability distribution
교차 엔트로피는 지상 진실 클래스 확률 분포에 가장 가까운 픽셀당 확률 분포를 배우기 위해 신경망을 구동한다
Here, N total is the total number of classified pixels in all the images of a mini-batch
여기서, 총 N은 미니 배치의 모든 이미지에서 분류된 픽셀의 총 수입니다
Usually, a mini-batch would comprise of eight to 16 images, and the choice of this number depends on how much memory your GPU has
보통, 미니 배치는 8개에서 16개의 이미지로 구성되며, 이 숫자의 선택은 GPU가 얼마나 많은 메모리를 가지고 있는지에 달려 있습니다
Finally, the cross entropy loss compares Si, the output of the neural network for every pixel with Si star, the ground truth classification for that pixel
마지막으로, 교차 엔트로피 손실은 Si, 모든 픽셀의 신경망 출력과 Si star, 그 픽셀의 지상 진실 분류를 비교한다
In summary, we arrived at the following ConvNet model for semantic segmentation
요약하면, 우리는 의미론적 세분화를 위해 다음과 같은 ConvNet 모델에 도달했다
The feature extractor takes the image as an input and provides an expressive, but low resolution feature map as an output
기능 추출기는 이미지를 입력으로 가져와 표현력이 뛰어나지만 저해상도 기능 맵을 출력으로 제공합니다
The decoder then takes this feature map and upsamples it to get a final feature map of equal resolution to the original input image
그런 다음 디코더는 이 기능 맵을 가져와 업샘플하여 원본 입력 이미지와 동일한 해상도의 최종 피처 맵을 얻습니다
Finally, a linear layer followed by a softmax function generates the class ConvNets vector for each pixel in the input image
마지막으로, 선형 레이어 뒤에 softmax 함수가 입력 이미지의 각 픽셀에 대해 ConvNets 클래스 벡터를 생성합니다
The architecture we described in this lesson is one of the simpler models that can be used for semantic segmentation
우리가 이 수업에서 설명한 아키텍처는 의미론적 세분화에 사용할 수 있는 더 간단한 모델 중 하나이다
A lot of research on the optimal neural network model for semantic segmentation has been performed
의미 세분화를 위한 최적의 신경망 모델에 대한 많은 연구가 수행되었다
Ideas such as propagating the indices from pooling layers in the extractor to upsampling layers in the decoder have shown to provide a boost in performance as well as computational speed for semantic segmentation models
추출기의 풀링 레이어에서 디코더의 업샘플링 레이어에 이르기까지 인덱스를 전파하는 것과 같은 아이디어는 시맨틱 세분화 모델의 성능 향상과 계산 속도를 제공하는 것으로 나타났다
We've included a list of recent manuscripts describing architecture used for semantic segmentation in the supplementary material
우리는 보충 자료에 의미론적 세분화에 사용되는 아키텍처를 설명하는 최근 원고 목록을 포함시켰습니다
Congratulations, you should now have grasp the basics of using ConvNets to solve the semantic segmentation problem
축하합니다, 이제 의미론적 세분화 문제를 해결하기 위해 ConvNets를 사용하는 기본 사항을 이해해야 합니다
Most state of the art segmentation networks share the structure we described in this video
대부분의 최첨단 세분화 네트워크는 우리가 이 비디오에서 설명한 구조를 공유합니다
With a feature extractor, a decoder and then an output layer as the main building blocks
기능 추출기, 디코더 및 주요 빌딩 블록으로 출력 레이어를 사용합니다
We provide some links to recent methods as a reference if you're interested in diving deeper into current top performing algorithms
현재 최고 성능의 알고리즘에 대해 더 깊이 파고들고 싶다면 최근 방법에 대한 몇 가지 링크를 참조로 제공합니다
In the next lesson, we will describe how to use the semantic segmentation output to help self-driving cars perceive a road seen
다음 수업에서, 우리는 자율주행 자동차가 보이는 도로를 인식할 수 있도록 의미론적 세분화 출력을 사용하는 방법을 설명할 것이다
See you next time
다음에 보자


