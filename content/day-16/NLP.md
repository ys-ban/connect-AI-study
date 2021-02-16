# 1. Introduction to NLP

## goal of this course

- NLP which aims at properly understanding and generating human languages, emerges as a crucial application of AI with the advancements of deep lneural networks
- this course will cover various deep learning approaches as well as their applications such as language modelings, machine translation, question answering, document classification, and dialog systems

## NLP(major conferences: ACL, EMNLP, NAACL)
- includes state of the art deep learning-based models and tasks
- low-level parsing
  - tokenization, stemming
- word and phrase level
  - named entity recognition, part of speech tagging, noun-phrase chunking, dependency parsing, coreference resolution
- sentence level
  - sentiment analysis, machine translation
- multi-sentence and paragraph level
  - entailment prediction, question answering, dialog systems, summarization


## academic disciplines related to NLP
### text mining(major conferences: KDD, the WebConf(formerly, WWW), WSDM, CIKM, ICWSM)
- extract useful information and insights from text and document data
- document clustering
- highly related to computational social science

### information retriecal(major conferences: SIGIR, WSDM, CIKM, RecSys)
- highly related to computational social science

## trends of NLP
- text data can basically be viewed as a sequence of words, and each word can bne represented as a vector through a technique shck as Word2Vec or GloVe
- RNN-family models(LSTMs and GRUs), which takes the sequence of these vectors of words as input, are the main architecture of NLP tasks
- overall performance of NLP tasks has been improved since attention modules and Transformation models, which replaced RNNs with self-attention, have been introduced a few year ago
- as is the case for Transformer models, most of the advanced NLP models have been originally developed for improving machine translation tasks
- in the early days, customized models for different NLP tasks had developed separately
- since Transformer was introduced, huge models were released by stacking its basic module, self-attention, and these models are trained with large sized datasets through language modeling tasks, one of the self-supervised training setting that does not require additional labels for a particular task
- afterwards, above models were applied to other tasks through transfer learning, and they outperformed all other customized models in each task
- currently, these models has now become essential part in numerous NLP tasks, so NLP research become difficult with limited GPU resources, since they are too large to train


# 2. Bag of Words

## bag of words representation
- step 1. constructing the vocab containing unique words
- step 2. encoding unique words to one-hot vectors
  - a sentence can be represented as the sum of noe-hot-vectors

## naive bayes classifier for document classification
- for a document $d$ and a class $c$
  $$
  c_{MAP} = \argmax_{c\in \mathcal{C}}P(c|d) \\
  = \argmax_{c\in \mathcal{C}} \frac{P(d|c)P(c)}{P(d)} \\
  \argmax_{c\in \mathcal{C}} P(d|c)P(c)
  $$
- with independent condition,
  $$
  P(d|c)P(c) =  P(c)\prod_{i=1}^nP(w_i|c)
  $$

# 3. Word Embedding(Word2Vec, GloVe)

## what is word embedding?
- express a word as a vector
- cat and kitty are similar words, so they have similar vector representations -> short distance
- hamburger is not similar with cat or kitty, so they have different vector representation -> far distance

## Word2Vec
- an algorithm for training vector representation of a word from context words
- assumption: words in similar context will have similar meanings
- e.g.
  - the cat purrs
  - the cat hunts mice
- suppose that we read the word cat
  - what is the probability of some words $\mathbb{W}$ nearby cat?
- distributional hypothesis: the meaning of cat is captured by the probability distribution $P(\mathbb{W}|cat)$

