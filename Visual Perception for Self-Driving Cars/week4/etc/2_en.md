In the last lesson, we described the general object detection problem as well as how to evaluate the performance of 2G object detectors using average precision. This lesson will describe the steps involved in performing 2D object detection using convNets. Keep in mind that the field of 2D object detection is rapidly changing with new methods emerging everyday. What we will be describing is a modern approach to 2D object detection using ConvNets, but without many of the intricacies that allow state of the art detectors to eke out the best possible performance. If you find this topic is exciting as we do, check out the list of some of the current top 2D object detection papers we've included in the supplementary material. In this lesson, you will learn how to build a standard single-stage ConvNet architecture for 2D object detection using the network layers we learned about in module three. In addition, we will discuss some common designs that researchers have formulated for ConvNets used for 2D object detection. Let's begin by reviewing the 2D object detection problem. Given an image as an input, we want to simultaneously localize all objects in the scene and determine which class they belong to. Let's see how we can perform this task using a ConvNet. This figure shows the basic ConvNet configuration used for 2D object detection. We call this configuration a neural network architecture. The architecture takes as an input an image and a set of manually crafted prior boxes. First, the image is processed using a feature extractor. Second, a set of fully connected layers take as an input, the output of the feature extractor and provide a location refinement of each 2D prior box as well as a classification. Finally, non maximum suppression is performed on the output of the fully connected layers to generate the final detections. Let's delve deeper into each of these steps. We will begin our discussion with the feature extraction stage. Feature extractors are the most computationally expensive component of the 2D object detector. It is typical to have as much as 90 percent of the total architectures required computation used at this stage. The output of feature extractors usually has much lower width and height than those of the input image. However, its depth is usually two to three orders of magnitude greater than that of the input image. The design of feature extractors is a very active area of research with new extractors emerging on a regular basis. The most common feature extractors used are VGG, ResNet, and Inception. We will be focusing on the VGG feature extractor as our running example throughout the rest of this lesson. The VGG feature extractor is based on the convolutional layers of the VGG 16 classification network proposed by the Visual Geometry Group at Oxford University. It is one of the first feature extractors to be proposed for detection and is quite simple to build. As with most ConvNets, the VGG feature extractor is built by alternating convolutional layers and pooling layers. All convolutional layers are of size three by three by K, with a stride of one and a zero-padding of one, by which we mean that the padding of size one is filled with zeros. All max-pooling layers are of size two by two with stride two and no padding. These particular hyper parameters were arrived at through intensive experimentation and have performed extremely well in a wide range of problems making VGG and extremely popular extractor. Let's see how these layers affect our output volume shape. Last week, we derive the three equations for the output width, height, and depth based on the input volume after it has been passed through the convolutional layer. For the VGG feature extractor, all convolutions are of size three by three by K, with a stride of one and zero padding of one. That means the passing an input volume through any of the convolutional layers only changes its depth to K. On the other hand, the pooling layers of the VGG extractor are two by two with stride two and no padding. Repeating the same analysis using the equations for the pooling layer, we noticed that the max-pooling layers of VGG extractors reduce the width and height of the input volume by two, while maintaining the depth constant. Let's now see how the VGG extractor processes an input image. Given an M by N by three input image, we pass it through the first two convolutional layers of depth 64 followed by the first pooling layer. At this point, the output volume width and height are reduced by a factor of two, while the depth is expanded to 64. We can separate the VGG feature extractor into subsections, where each subsection ends with a pooling layer. The first subsection is called the Conv1 subsection of the VGG extractor. We then proceed to pass the output volume through the rest of the five subsections to arrive at our final output volume of shape M over 32, N over 32, and 512. As an example, if we have a 1,240 by 960 by 3 image as our input, our final output volume shape will be 40 by 30 by 512. We will be using this output volume to generate our final detections. The next step to describe in our neural network architecture is the concept of prior boxes. Also called anchor boxes. To generate 2D bounding boxes, we usually do not start from scratch and estimate the corners of the bounding box without any prior. We assume that we do have a prior on where the boxes are in image space and how large these boxes should be. These priors are called anchor boxes and are manually defined over the whole image usually on an equally-spaced grid. Let's assume that we have a set of anchors close to our ground-truth boxes. During training, the network learns to take each of these anchors and tries to move it as close as possible to the ground truth bounding box in both the centroid location and box dimensions. This is termed residual learning and it takes advantage of the notion that it is easier to nudge and existing box a small amount to improve it rather than to search the entire image for possible object locations. In practice, residual learning has proven to provide much better results than attempting to directly estimate bounding boxes without any prior. Many different methods have been proposed in the literature on how to use the anchor bounding boxes to generate the final prediction. Usually, the anchors interact with the feature map to generate fixed sized feature vectors for every anchor. We'll explain one of the first methods proposed for this interaction by Microsoft Research in their architecture Faster R-CNN. However, keep in mind that this is not the only way to perform such an interaction. The Faster R-CNN interaction method is quite simple. For every pixel in the feature map, we associate k anchor boxes. We then perform a three by three by D star convolution operation on that pixels neighborhood. This results in a one by one by D star feature vector for that pixel. We use this one by one by D star feature vector as the feature vector of every one of the k anchors associated with that pixel. We then proceed to feed the extracted feature vector to the output layers in the neural network. The output layers of a 2D object detector usually comprise of a regression head and a classification head. The regression head usually includes multiple fully-connected hidden layers with a linear output layer. The regressed output is typically a vector of residuals that need to be added to the anchor that hand to get the ground truth bounding box. Another method to update the dimension of the anchors is to regress a residual from the center of the anchor to the center of the ground truth bounding box in addition to two scale factors that correct the ground truth bounding box width and height when multiplied with an anchor's width and height. The classification head is also comprised of multiple fully-connected hidden layers, but with a final softmax output layer. The softmax output is a vector with a single score per class. The highest score usually defines the class of the anchor at hand. You might note that based on what we described so far, we will end up with k bounding boxes per pixel of the output feature map. Even if we consider boxes with high classification score for all classes of interest, we still will have many redundant detections in the image. During average precision computation, we only consider one detection per ground truth bounding box. Any redundant detections are considered false positives and results in lower precision and thus a lower average precision overall. Recall, we're aiming for perfect detection, which means we want an output of one box per object in the image. So, we will need to do something to eliminate the many redundant detections produced by our network. In fact, this is only an issue of inference and it turns out to be beneficial to drive the network to output the best possible residuals for every anchor during training. Before going deeper into this issue, let's summarize what you learned this lesson. First, you learned that convolutional neural networks can be used to solve the 2D object detection problem and study the details of the VGG feature extractor architecture. Second, you learned how to use anchor boxes as object location priors and estimate the bounding box residuals to output the final object locations. In the next lesson, we'll describe how to train 2D object detectors using classification and regression loss functions. For that, we will use most of the k output boxes. We'll then return to the challenge of outputting a single bounding box per object and introduce the concept of non-maximum suppression to solve it. See you then.