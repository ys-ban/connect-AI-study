# RNN - Recurrent Neural Network

## Sequence Data
- a data which consists of sequences of some type of data is called sequence data
  - ex) sound wave, string, stock price, etc
- every data which arranged along time-series is sequence data
- sequence data is easy to violate the i.i.d assumption
- thus a loss of data or a change of order leads to different probability distribution
- conditional probability can be used to deal with sequence data
  $$
  P(X_1, X_2, \dotsc, X_t) = P(X_t|X_1, \dotsc, X_{t-1})P(X_1,\dotsc, X_{t-1}) \\
  =P(X_t|X_1, \dotsc, X_{t-1})P(X_{t-1}|X_1, \dotsc, X_{t-2})P(X_1, \dotsc, X_{t-2})\\
  = \dotsc = \prod_{s=1}^tP(X_s|X_{s-1}, \dotsc, X_1)
  $$
- using the previous data, a squence daata can be dealt with
- but to analyze sequence data, all previous data is not always necessary
- to deal with sequence data, a model which can treat a data of various size is needed
- if only a data of constant size $\tau$ is used in model, it is called Autoregressive model with period $\tau$
- to decide whether a $\tau$ is good or not, the background knowledge is required
- a model where all previous data except immediately preceding data is encoded to $H_t$ is called a latent autoregressive model

## RNN
- a basic structure of RNN looks similiar with MLP
  $$
  O_t = H_tW^{(2)}+b^{(2)}\\
  H_t = \sigma (X_tW_X^{(1)}+H_{t-1}W_H^{(1)+b^{(1)}})
  $$
- RNN is modeled by using the previous latant $H_{(t-1)}$ and the current input data
- weight matrix is invariant through the time $t$
- the backward propagation of RNN is calculated along the order of adjacent graphs
  $$
  \partial_{w_h}h_t = \partial_{w_h}f(x_t, h_{t-1}, w_h)+\sum_{i=1}^{t-1}\prod_{h=i+1}^{y}\partial_{h_{j-1}}f(x_j, h_{j-1}, w_h)\partial_{w_h}f(x_i, h_{i-1}, w_h)
  $$
- using BPTT we can calculate the backward propagation but the product term is un stable(converge to zero or diverge)
- thus we need to trucate data or model(truncated BPTT)
- but it also can be unstable if the length of data is very long


