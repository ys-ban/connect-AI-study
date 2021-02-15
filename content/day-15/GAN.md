# Generative Model

## Introduction
- what you cannot create is what you do not know(Richard Feynman)
- what is generative model
  - suppose that we are given images of dogs
  - we want to learn a probability distribution $p(x)$ such that

        1. generation: if we sample $x_{new}~p(x)$, $x_{new}$ should look like a dog
        2. density estimation: $p(x)$ should be high if $x$ looks like a dog, and low otherwise(anomaly detection)
        3. unsupervised representation learning: we should be able to learn what these images have in common, e.g. ears, tail, etc(feature leaning)
  - the, how can we represent $p(x)$?
- basic discrete distributions
  - Bernoulli distribution: (biased) coin flip
    - $D = \{H, T\}$
    - specify $P(X=H)=p$. then $P(X=T)=1-p$
    - write: $X  Ber(p)$
  - Categorical distribution: (biased) m-sided dice
    - $D = \{1, \dotsb, m \}$
    - specify $P(Y=i) = p_i$, such that $\sum_{i=1}^mp_i = 1$
    - write: $Y~Cat(p_1, \dotsb, p_m)$

## Structure Through Independece

- what if $X_1, \dotsb, X_n$ are independent, then
  $$
  p(x_1, \dotsb, x_n) = p(x_1)p(x_2)\dotsb p(x_n)
  $$
- possible state: $2^n$
- parameters to specify: $n$
- easy to deal but too simple to model distributions to work well


## Conditional Independence
- the important rules:
  - chain rule:
  $$
  p*(x_1, \dotsb, x_n)= p(x_1)p(x_2|x_1)\dotsb p(x_n| x_1, \dotsb, x_{n-1})
  $$
  - Bayes' rule:
  $$
  p(x|y) = \frac{p(x, y)}{p(y)} = \frac{p(y|x)p(x)}{p(y)}
  $$
  - conditional independence:
  $$
  if x\bot y|z, \; then p(x|y, z) = p(x|z)
  $$
- now, by the Markov assumption, we can deal with problems by only $2n-1$ parameters

## Auto-regressive Model

- suppose that we have $28\times 28$ binary pixels
- out goal is to learn $p(x) = p(x_1, \dotsb, x_{784})$ over $x \in {0, 1}^{784}$
- how to parametrize $p(x)$
  - use the chain rule to factor the joint distribution
  - $p(x_{1:784}) = p(x_1)p(x_2|x_1)\dotsb$
  - this is called an autoregressive model
  - need an ordering of all random variables

## NADE: Neural Autoregressive Density Estimator
- NADE is an explicit model that can compute the density of the given inputs
- how to compute the density of the given image
  - suppose that we have a binary image with 784 binary pixels, $\{x_1, x_2, \dotsb, x_{784}\}$
  - then, the joint probability is computed by
  $$
  p(x_1, \dotsb, x_{784}) = p(x_1)p(x_2|x_1)\dotsb p(x_{784}|x_{1:783})
  $$
  where each conditional probability $p(x_i | x_{1:i-1}$ is computed independently
- in case of modeling continuous random variables, a mixture of Gaussian can be used

## Pixel RNN
- RNNs can be used to define an auto-regressive model
- 2 model architectures in Pixel RNN based on ordering of chain:
  - Row LSTM
  - Diagonal BiLSTM


