# Self-Supervised Pre-Training Models - GPT-1 & BERT

## recent trends
- transformer model and its selfattention block has become a general-purpose sequebce encoder and decoder in recent NLP applications as well as in other areas
- training deeply stacked transformer models via a self-supervised learning framework has significantly advanced vairous NLP tasks through transfer learning, e.g. BERT, GPT-3, XLNet, ALBERT, RoBERTa, Reformer, t5, ELECTRA...
- other applications are fast adopting the self-attention and transformer architecture as well as self-supervised approach, e.g. recommender systems, drug discovery, computer vision...
- as for natural generation, self-attention models still requires a greedy decoding of words one at a time

## GPT-1
- it introduces special tokens, such as \<S>, \<E>, $, to achieve effective transfer learning during fine-tuning
- it does not need to use additional task-specific architectures on top of transferred
![transformer_usage](../../img/transformer_usage.png)
