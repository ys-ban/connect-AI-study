# Transformer
## transformer: high-level view
- attention is all you need, NeurlPS'17
  - no more RNN or CNN modules
- in usual RNNs
  - $h_t$ is generated every time step
  - at time step $t$, the portion of input at distant time step $s$ can be underevaluated
  - the usual RNNs are called forward RNN
  - because of this problem, backward RNNs are designed
  - Bi-directional RNN is the model where forward RNN and abckward RNN works and learns in parellel
-  