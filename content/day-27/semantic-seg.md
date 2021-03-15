# Semantic Segmentation
## What is Semantic Segmentation
- classify each pixel of an image into a category
- do not care of instances, only care about semantic category
## Where Can Semantic Segmentation Be Applied To
- medical images
- autonomous driving
- computational photography

# Semantic Segmentation Architectures
## Fully Convolutional Networks
- the first end to end architerture for semantic segmentation
- take an image of an arbitrary size as input
- and output a segmentation map of the corresponding size to the input
- **fully connected layer:** output a fixed dimensional vector and discard spatial coordinates
  - it classifies a single feature vector
- **fully convolutional layer:** output a classification map which has spatial coordinates
  - it classifies every feature vector of the convolutional feature map
  - limitation: predicted score map is in a very low resolution
  - solution: enlarge the score map by upsampling
- **upsampling:** upsampling is used to resuze a small activation map to the size of the input image
  - unpooling
  - transposed convolution
  - upsample and convolution
## Hypercolumns for Object Segmentation
## U-Net
## Deeplab