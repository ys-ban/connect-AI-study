# CNN

## Definition of Convolution

- continuous version
  $$
  (f*g)(t) = \int f(\tau)g(t-\tau)d\tau = \int f(t-\tau)g(\tau)d\tau
  $$
- discrete version
  $$
  (f*g)(t) = \sum_{i = -\infty }^{\infty} f(i)g(t-i) = \sum_{i = -\infty }^{\infty} f(t-i)g(i)
  $$
- 2D image version
  $$
  (I*K)(i, j) = \sum_m\sum_nI(m, n)K(i-m, j-n) = \sum_m\sum_nI(i-m, j-n)K(m, n)
  $$
- in the above definition, we do not consider stride nor padding

## What Convolution Does

- we can extract, filter  or enhance some features
- it helps DL model learn and work well

## The Number of Parameters

- if an input size is $(I_W, I_H, I_C)$ and there are $M$ kernels whose size is $(K_W, K_H, K_C)$, then the output has $(I_W-K_W+1, I_H-K_H+1, M)$ size and $I_C$ has to be equal to $K_C$.
- in the above case, we didn't consider stride nor padding
  - ex) if padding:1, stride:1, $3\times 3$ kernel, input: $(40, 50, 128)$, output: $(40, 50, 64)$, then the number of parameters is $3\times 3 \times 128 \times 64$ $=73,728$

## Pooling Layer
 - CNN consists of convolution layer, pooling layer and fully connected layer
   - convolution and pooling layers: feature extraction
   - fully connected layer: decision making(e.g., classification)
   - recently, the number of fullly connected layers is decreasing
     - as the number of parameters increases, the generalzation performance gets worse
     - as the number of parameters increases, the time for DL model to learn increases
 - there exist various pooling layers
   - max pooling
   - min pooling
   - average pooling
  
  ## Stride & Padding

  - the size of step
  - in 1D case, stride is a positive integer
  - likewise in 2D case, stride is a tuple of 2 positive integers
  - padding means the data that will be filled for values whose index is out of range
  - both concepts can be used for setting the output size as wanted
  
## $1\times1$ Convolution

- fully connected layers increase drastically the number of parameters
- too many parameters for DL model to learn, work well(generalization performance), to be paid and so on...
- $1\times1$ convolution reduces dimension
- it also reduces the number of parameters while increasing the depth(the number of layers)
- e.g., bottleneck architencure