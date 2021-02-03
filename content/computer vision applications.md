# Computer Vision Application

## Semantic Segmentation


### Overview

- identify which object a pixel belongs to
- in an ordinary CNN, there is a fully connected layer at last
- fully convolution network is implemented
- the process where fully connecPted layer is replaced by convolution layer is called convolutianalization
- the number of parameters does not change
- transforming fully connected layers into convolution layers enables a classification net to output a heat map
- while FCN can run with inputs of any size, the output dimensions are typically reduced by subsampling
- so we need a way to connect the coarse outputs to the dense pixels


### Deconvolution
- it can be understood as an inverse of convolution
- but it is not an true inverse of convolution(there is no inverse of convolution)
- it is called also convolution transpose


## Object Detection

- R-CNN
  - process overview
    - take an input image
    - extract around 2,000 region proposal(using selective search)
    - comput features for each proposal(using AlexNet)
    - classify with linear SVM
  - in R-CNN, the number of crop/warp is usually over 2,000 meaning that CNN must run more than 2,000 times

- SPPNet
- Fast R-CNN
  - process overview
    - take an input and a set of bounding boxes
    - generate convolution feature map
    - for each region, get a fixed length feature from ROI pooling
    - two outputs: class and bounding-box regressor
- Faster R-CNN
  - region proposal network + Fast R-CNN
  - anchor box: detection box with predefined sizes

- YOLO
  - YOLO is an extremely fast object detection algorithm
    - baseline:45fps / smaller version: 155fps
  - it simultaneously predicts multiple bounding boxes and class probabilities
    - no explicit bounding box sampling
  - given an image, YOLO divides it into $S\times S$ grid
    - if the center of an object falls into the grid cell, that grid cell is responsible for detection
  - each cell predicts B bounding boxes
  - each cell predicts C class probabilities
  - inn total, it becomes a tensor with $S\times S \times (5B+C)$ size