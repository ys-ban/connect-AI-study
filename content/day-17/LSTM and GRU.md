# dLong Short-Term Memory and Gated Recurrent Unit
## Long Short-Term Memory
- core idea: pass cell state information straightly without any transformation
  - solving long-term dependency problem
- what is LSTM?
  - $c_t$ is added which has a cell state information
  - $\{c_t, h_t\}=LSTM(x_t, c_{t-1}, h_{t-1})$
- Long short-term memory
  - $i$: input, whether to write to cell
  - $f$: forget gate, whether to erase cell
  - $o$: output gate, how much to reveal cell
  - $g$: gate gate, how much to write to cll
    $$
    \left(
    \begin{matrix}
    i \\
    f \\
    o \\
    g
    \end{matrix}
    \right) =
    \left(
    \begin{matrix}
    \sigma \\
    \sigma \\
    \sigma \\
    tanh
    \end{matrix}
    \right)
    W
    \left(
    \begin{matrix}
    h_{t-1} \\
    x_t
    \end{matrix}
    \right) \\
    c_t = f \circledcirc c_{t-1} + i \circledcirc g \\
    h_t = o \circledcirc tanh(c_t)
    $$
- a gate exists for controlling how much information could flow from cell state
  - forget gate
    - $f_t = \sigma (W_f \sdot \left[ h_{t-1}, x_t \right] + b_f)$
  - gate gate
    - generate information to be added and cut it by input gate
      - $i_t = \sigma (W_i \sdot \left[ h_{t-1}, x_t \right] + b_i)$
      - $\tilde{C_t} = tanh(W_C \sdot \left[ h_{t-1}, x_t \right] + b_C)$
    - generate new cell state by adding current information to previous cell state
      - $C_t=f_t\sdot C_{t-1} + i_t \sdot \tilde{C_t}$
  - hidden state vector
    - generate hidden state by passing cell states to tanh and output gate
    - pass this hidden state to next time step, and output or next layer if needed
      - $o_t=\sigma (W_o \sdot \left[ h_{t-1}, x_t \right] + b_o)$
      - $h_t = o_t \sdot tanh(C_t)$

## Gated Recurrent Unit(GRU)
- what is GRU
  - $z_t = \sigma(W_z \sdot \left[ h_{t-1}, x_t \right])$
  - $r_t = \sigma(W_r \sdot \left[ h_{t-1}, x_t \right])$
  - $\tilde{h_t}=tanh(W \sdot \left[ r_t \sdot h_{t-1}, x_t \right])$
  - $h_t = (1-z_t) \sdot h_{t-1} + z_t \sdot \tilde{h_t}$
  - c.f) $C_t = f_t \sdot C_{t-1} + i_t \sdot \tilde{C_t}$ in LSTM


## Backpropagation in LSTM and GRU
- uninterrupted gradient flow


## Summary on RNN/LSTM/GRU
- RNNs allow a lot of flexibility in architecture design
- Vanilla RNNs are simple but do not work very well
- Backward flow of gradients in RNN can explode or vanish
- Common to use LSTM or GRU: their additive interactions improve gradient flow