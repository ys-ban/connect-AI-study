# Convolution Neural Network

## Usual MLP

- using fully connected neural network
  $$
  h_i = \sigma (\sum_{j=1}^{p} W_{ij}x_j)
  $$
  - $h_i$ is i-th value of a hidden layer
  - $W_{ij}$ is a $(i, j)$ component of a weight matrix
  - $x_j$ is a i-th value of an input
  - $\sigma$ is an activation function
- it needs many parameters to caculate and update
- too easy to overfit


# CNN

 - moving kernel along rows and columns of inputs
 - compairing to MLP, smaller amount of parameters
  $$
  [f*g](x) =   \int_{\mathbb{R}^d}f(z)g(x+z)dz = \int_{\mathbb{R}^d}f(x+z)g(z)dz = [g*f](x) \\
  \;\\
  [f*g](i) =   \sum_{a \in\mathbb{Z}^d}f(a)g(i+a) = \sum_{a \in\mathbb{Z}^d}f(i+a)g(a) = [g*f](i)
  $$
- the above definition is 1-dimensional version of convolution
  $$
   [f*g](i) = \sum_{a \in\mathbb{Z}^d}f(a)g(i+a) \\
   [f*g](i, j) = \sum_{p,\;q}f(p, q)g(i+p, j+q) \\
   [f*g](i, j, k) = \sum_{p,\;q,\;r}f(p, q,r)g(i+p, j+q,k+r)
  $$
- calculation of convolution under the condition suggested below
  $$
  K = \begin{pmatrix}0 & 1 \\ 2 & 3 \end{pmatrix},\;A = \begin{pmatrix}0 & 1 & 2 \\ 3 & 4 & 5 \\ 6 & 7 & 8 \end{pmatrix} \\
  \;\\
  K*A = \begin{pmatrix}19 & 22\\ 37 & 43 \end{pmatrix}
  $$
- if the input size is $(H,W)$ and the kernel size is $(K_H, K_W)$, then the output size will be
  $$
  O_H = H-K_H +1 \\
  O_W = H-K_W+1
  $$
- like RGB data of image, some data looks like 3-dimensional but it is called 2-dimensional data with mulltiple channels
- for convolution of 2-dimensional with multiple channels the same number of kernels are needed
- after calculating convolutions for each channels the final output is calcullated by adding each output of channels
  
# Back propagation of CNN

- partial derivative of convolution(continuous case)
  $$
  \frac{\partial}{\partial x}[f*g](x) = \partial\int_{\mathbb{R}^d}f(y)g(x-y)dy \\
  =\int_{\mathbb{R}^d}f(y) \frac{\partial g}{\partial x}(x-y)dy = [f*g'](x)
  $$
- partial derivative of convolution(a specific discrete case)
  $$
  if \; X = \begin{pmatrix} x_1 \\ x_2 \\ x_3 \\ x_4 \\ x_5 \end{pmatrix}\;and\;\;K=\begin{pmatrix} w_1 \\ w_2 \\ w_3 \end{pmatrix}\\
  \;\\
  \frac{\partial\mathcal{L}}{\partial w_1}=\delta_1x_1+\delta_2x_2+\delta_3x_3
  $$
  where $o_i$ is an output of convolution and $\delta_i$ is a partial derivative of $o_i$
- partial derivative of convolution(discrete case)
  $$
  if \; X = \begin{pmatrix} x_1 \\ x_2 \\ \vdots \\ x_{n-1} \\ x_n \end{pmatrix}\;and\;\;K=\begin{pmatrix} w_1 \\ w_2 \\ \vdots \\ w_d \end{pmatrix}\\
  \;\\
  \frac{\partial\mathcal{L}}{\partial w_i}=\sum_j \delta_jx_{i+j-1}
  $$
  where $o_i$ is an output of convolution and $\delta_i$ is a partial derivative of $o_i$
