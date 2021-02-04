# 1 Introduction


## 1.1 Generalization

 - How well the learned model will behave on unseen data
 - Generalization gap means the difference between test error and training error



## 1.2 Under-fitting vs Over-fitting

- if a model underfits the data, both test error and training error will be higher than what we expected
- if a model overfits the data, test error will be low but training error will be high
- need to find the sweet spot between underfitted model and overfitted model
- the definition of sweet spot varies according to the conditions or purposes of modelㅜ

## 1.3 Cross Validation

- cross-validation is a model validation technique for assessing how the model will generalized to an nidependent (test) data set
- there is many techniques of cross validation
- one thing we have to memorize is that in the process of training model(finding optimal parameters) we have to use only training data not valllidation data nor testing data



## 1.4 Bias-variance Tradeoff

- we can derive what we are minimizing *cost* can be decomposed into three parts: bias, variance and noise
- but minimizing three parts suggested above simutaneously is hard or impossible

$$
\mathbf{E}[(t-\hat{f})^2] = \mathbf{E}[(t-f+f-\hat{f})^2 = \mathbf{E}[(t-\mathbf{E}[\hat{f}])^2]]+\mathbf{E}[(\mathbf{E}(\hat{f})-\hat{f})^2]+\mathbf{E}(\epsilon)
$$
- the first term of the last is squared bias, the second term is variance and the last term is noise



## 1.5 Bootstrapping

- bootstraping is any test or metric that uses random sampling with replacment


## 1.6 Bagging and Boosting

- bagging(bootstraping aggregating)
  - multiple models are being trained with bootstraping
    - ex) base classifiers are fitteed on random subset where individual predictions are aggregated(voting or averaging)
- boosting
  - it focuses on those specific training samples that are hard to classify
  - a strong model is built by combining weak learners in sequence where each learner learns from the mistakes of the previous weak learner


# 2 Optimization

## 2.1 Introduction to Gradient Descent Methods

- First-Order iterative optimization algorithm for finding a local minimum of a differentiable function

- evoked by Newton's method
- stochastic gradient descent
  - upgrade with the gradient computed from a single sample

- mini-batch gradient descent
  - update with the gradient computed from a subset of data

- batch gradient descent
  - update with the gradient computed from the whole data


## 2.2 Batch-size Matters

- "it has been observed in practive that when using a larger batch there is a degradation in the quality of the model, as measured by its ability to generalize"
- "we .. present numerical evidence that supports the view that large batch methods tend to converge to ***sharp minimizers*** of the training and testing functions. in contrast, small-batch methods consistently converge to ***flat minimizers***.. this due to the inherent noise in the gradient extimation."
- if we have to choose one of them, ***flat minimizers*** are the better choice
  - if ***sharp minimizers*** are choosen, a small difference of input data results in a bigger difference of output

## 2.3 Well-known Optimizers


- stochastic gradient descent
  $$W_{t+1} \leftarrow W_{t} - \eta g_{t}$$
  - $\eta$ is a learning rate and $g_t$ is a gradient

- momentum
  - $\beta$ is a momentum and the iteration is suggested below.
  $$
  \alpha_{t+1} \leftarrow \beta \alpha_{t} + g_{t} \\
  W_{t+1} \leftarrow W_{t}-\eta \alpha_{t+1} \\
  $$
- nesterov accelerated gradient
  - the concept of lookahead gradient is introduced
  $$\alpha_{t+1} \leftarrow \beta \alpha_{t} + \nabla \mathcal{L}(W_{t} - \eta \beta \alpha_{t}) \\ W_{t+1} \leftarrow W_{t}-\eta \alpha_{t+1}$$
- adagrad
  - adagrad adapts the learning rate, performing larger updates for infrequent and smaller updates for frequent parameters
  $$
  W_{t+1} \leftarrow W_{t} - \frac{\eta}{\sqrt{G_{t}+\epsilon}}g_t
  $$
  - $G_t$ is a sum of gradient squares and it measures the total change of a parameter
  - $G_t$ is increasing every steps so learning rate will converging to 0
  - it results in slow convergence or misleading of convergence
- adadelta
  - adadelta extends adagrad to reduce its monotonically decreasing the learning rate by restriction the accumulation window
  $$
  G_t \leftarrow \gamma G_{t-1} + (1-\gamma)g_t^2 \\
  W_{t+1} \leftarrow W_{t} - \frac{\sqrt{H_{t-1}+\epsilon}}{\sqrt{G_{t}+\epsilon}}g_t \\
  H_t \leftarrow \gamma H_{t-1} + (1-\gamma)(\Delta W_t)^2
  $$
  - there is no learning rate in adadelta
  - $G_t$ is EMA of gradient squares
  - $H_t$ is EMA of difference squares
- rmsprop
  - rmsprop is an unpublished, adaptive learning rate method proposed by **Geoff Hinton** in his lecture
  - $\eta$ is a stepsize
  $$
  G_t \leftarrow \gamma G_{t-1} + (1-\gamma)g_t^2 \\
  W_{t+1} \leftarrow W_{t} - \frac{\eta}{\sqrt{G_{t}+\epsilon}}g_t$$
- adam
  - adaptive momentum estimation(adam) leverages both past gradients and squared gradients
  $$
  m_t \leftarrow \beta_1 m_{t-1}+(1-\beta_1)g_t \\
  v_t \leftarrow \beta_2 v_{t-1}+(1-\beta_2)g_t^2 \\
  W_{t+1} \leftarrow W_{t} - \frac{\eta}{\sqrt{v_{t}+\epsilon}}\frac{\sqrt{1-\beta_2^t}}{1-\beta_1^t}g_t
  $$
  - adam effectively combines momentum with adaptive learning rate approach


## 2.4 Regularization

- early stopping
  - note that we need additional validation data
 to do ealy stopping
- parameter norm penalty
  - it adds smoothness to the function space
  $$
  total \;cost = loss(\mathcal{D};W)+\frac{\alpha}{2}||W||^2
  $$
  - the second term of the right-hand side is called ***parameter norm penalty*** or ***weight decay***
  - the assumption:
     as the function smoother, as the generalization performance grows

- data augmentation
  - if the size of data is small, ML or traditional prediction model probably works better
  - to make better DL model, more data are always welcomed
  - in most cases, training data are given in advance
  - in such cases, we need data augmentation
- noise robustness
  - add random noises input or weights
  - until now, the reason why it works is still mistery
- label smoothing
  - mix-up constructs augmented training examples by mixing both input and output of two randomly selected training data
  - cutmix constructs augmented training examples by mixing inputs with cut and paste and outputs with soft labels of two randomly selected training data
  - until now, the reason why it works is still mistery
- dropout
  - in each forward pass, randomly set some neurons to zero
  - it can be explained informally
  - but the reason why it works is also still mistery
- batch normalization
  - it makes a lot of disputation
  - batch normalization compute the empirical mean and variance independently for each dimension(layers) and normalize
  $$
  \mu_B = \frac{1}{m}\sum_{i=1}^mx_i \\
  \sigma_B^2 = \frac{1}{m}\sum_{i=1}^m(x_i-\mu_B)^2 \\
  \hat{x_i} = \frac{x_i-\mu_B}{\sqrt{\sigma_B^2+\epsilon}}
  $$
  - many papers rejects batch normalization
  - but in DL, it works
  - there are different variances of normalizations
    - batch norm: each channel along layers
    - layer norm: each layer along channels
    - instance norm: each channel for each layer
    - group norm: grouped by the rule researchers made
  