# Image Classification

## Image Classifier
- a mapping $f$ that maps an image to a category level

## Approach for Image Recognition
- what if we could memorize all the data in the world
------------
- all the classification problems could be solved by k-NN(k Nearest Neighbors)
- k-NN
  - classifies a query data point according to reference points closest to the query
  - all the classification problems could be solved by k-NN
  - but it is not realizable(because of memory and time complexity
------------
- we can use simple linear layer(fully connected neural network)
- MLP
  - take every pixel of an image as input
  - using weights and activation function, calculate the probability meaning what object is in the image
  - but it is easy to overfit(generalization performance decreases easily)
-------------
- we can use convolutional neural network(CNN)
- CNN
  - take a part of pixels as input
  - locally connected layer
  - able to learn local feature using only the smaller amount of parameter than fully connected layer(sharing weights)
  - CNN in used as a backbone of many CV tasks
    - image level classification
    - classification + regression
    - pixel level classification(semantic)

## Brief History of CV
- AlexNet
  - the first successful CNN on the ILSVRC
  - activation function ReLU
  - dropout technique(regularization)
  - LRN(local response normalization) is used(recently deprecated, use batch normalization instead)
  - large size filters are used to cover a wider range of the input image
- VGGNet
  - deeper and simpler architecture
  - no LRN
  - only $3\times 3$ conv filters and $2\times 2$ max poolings are used
  - better performance
  - better generalization
- GoogLeNet
  - deeper network with computational efficiency
- ResNet
  - ultra deep network with resicual connections
- Beyond ResNet
  - DenseNet
  - SENet
  - EfficientNet