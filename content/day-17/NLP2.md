# 1. Basic of Recurrent Neural Networks

## types of RNNs
- inputs and outputs of RNNs
  - we usually want to predict a vector at some time steps
- how to calculate the hidden state of RNNs
  - we can process a sequence of vectors by applying a recurrence formula at every time step
  - $h_{t-1}$: old hidden state vector
  - $x_t$: input vector at some time step
  - $h_t$: new hidden state vector
  - $f_W$: RNN function with parameters $W$
  - $y_t$: output vector at time step t
  - $h_t = f_W(h_{t-1}, x_t)$
  - the state consists of a single hidden vector $\mathbf{h}$
  - ex.
    - $h_t = f_W(h_{t-1}, x_t)$
    - $h_t = tanh(W_{hh}h_{t-1} + W_{xh}x_t)$
    - $y_t = W_{hy}h_t$
    $$
    if \;x_{t}\in\mathbb{R}^3, h_{t-1}\in\mathbb{R}^2, \; then \;
    W = \left( \begin{matrix}
    W_{xh} | W_{hh}
    \end{matrix} \right) \\
    where\; W_{xh} \in \mathbb{R}^{2\times 3} \;\&\;W_{hh} \in \mathbb{R}^{2\times 2}
    $$
# 2. Category of Mapping
- one to one
  - standard neural network
- one to many
  - image captioning(from image to objects)
- many to one
  - sentiment classification(from sequence of text to sentiment)
- many to many with delay
  - machine translation
- many to many without delay(realtime model)
  - video classification on frame level
  - predicting POS(part of speech)

# 3. Character-level Language Model
- example of training sequence "hello"
  - vocab: [h, e, l, o]
  - example training sequence: "hello"

# 4. Vanishing/Exploding Gradient Problem in RNNs
- RNNs are excellent, but deploying the same matrix at each time step during backpropagation causes gradient vanishing or exploding
- $W_{hh}$ is multiplied so many times
- if $W_{hh}$ has size larger than 1, $W_{hh}$ goes to infinite
- if $W_{hh}$ has size smaller than 1, $W_{hh}$ goes to zero
- this problem results from chain rule used through BPTT(backpropagation through time)
- this problem can be solved by many method(e.g. LSTM, GRU, transtormer, self-attention and so on)