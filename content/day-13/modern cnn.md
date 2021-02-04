# Modern CNN - $1\times1$ Convolution

## Overview

- the term "modern " does not make sense
  - it is not a highend technique
  - it was used frequently until 2018
  - "modern" is a relative expression
- real modern ones will be introduced after
- we will cover 4~5 models
  - AlexNet
  - VGGNet
  - GoogLeNet
  - ResNet
  - DenseNet
- the remarkable fact is that the number of parameters decreases and the performance is improved although the number of layers decreases


## AlexNet
- ILSVRC
  - imagenet large scale visual recognition challenge
  - classification / detection / localization / segmentation
  - 1,000 different categories
  - over 1 million images
  - training set: 456,567 images
- as time goes, error rate goes down
- AlexNet consists of 5 convolution layers and 3 fully connected layers
- key ideas:
  - rectified linear unit(ReLU) activation
  - GPU implementation
  - local response normalization
  - overlapping pooling
  - data augmentation
  - dropout
- details of ReLU:
  - preserves properties of linear model
  - easy to optimize with gradient descent
  - good generalization
  - overcome the vanishing gradient problem <span style="color:red">$\star\star\star$</span>
  
## VGGNet
- increasing depth with $3\times3$ convolution filters(with stride 1)
  - compare the number of parameters when using 2 $3\times3$ convolutions and the number of parameters when using 1 $5\times5$ convolution
  - actually both case we can extract the same feature(not literally same, in aspects of information)
  - in this way, it decreases the number of parameters while sustaining the size of receptive field
- $1\times1$ convolution for fully connected layers
- dropout(p=0.5)
- VGG16, VGG19


## GoogLeNet

- it has 22 layers
- network in network structure
- inception block
  - various responses can be concatenated
  - reduce the number of parameters
  - $1\times1$ convolution can be seen as channel-wise dimension reduction


## ResNet
- deeper neural networks are hard to train
  - overfitting is usually caused by an excessive number of parameters
  - but not in case...
- add an identity map(skip connection)
  - $f(x) \leftarrow x+f(x)$
  - add an identity map after nonlinear activations
    - simple shortcut
    - projected short cut(need $1\times1$ conv to match the channel depth)
- batch normalization after convolutions
- bottleneck architecture

## DenseNet

- DenseNet uses concatenation instead of addition
- dense block
  - each layer concatenates the feature maps of all preceding layers
  - the number of channels increases exponentially
- transition block
  - batch norm $\rightarrow$ $1\times1$ conv $\rightarrow$ $2\times2$ avgpooling
  - dimension reduction


## Summary
- key takeaways
  - VGG: repeated $3\times3$ blocks
  - GoogLeNet: $1\times1$ convolution
  - RestNet: skip-connection
  - DenseNet: concatenation