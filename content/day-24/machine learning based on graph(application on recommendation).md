# Machine Learning Based on Graph: Application on Recommendation System
## 1. Review on Recommendation System
### 1.1. examples of recommendation system
- amazon, netflix, youtube, facebook

### 1.2. recommendation system and graph
- the main task of recommendation system is<br>
  to predict preference of users<br>
  to predict objects that users might buy
- in the aspect of graph, the problems to solve are<br>
  to predict edges that might be added soon<br>
  to predict missing weights of edges


### 1.3. content-based recommendation system
- to recommend objects that are similar with the objects that user purchased before or was satisfied to
- need to construct item profiles and user profiles
- pros
  - other user profiles are not required
  - appliable to one with unique preference
  - appliable to new items(no one purchased)
  - explainable model(give reasons)
- cons
  - additional information is required(to build item profile)
  - not appliable to users without purchase history
  - it tend to be overfitted(the range of recommedation tends to be narrower)


### 1.4. collaborative filter
- to recommend objects that many other users having similar preference were satisfied to
- pros
  - additional information is not required(no item profile)
- cons
  - the size of review data has to be large enough to work well
  - not appliable to newbie user or new arrival item
  - not appliable to user with unique preference


### 1.5. evaluation of recommendation system
- MSE
- RMSE


## 2. Netflix Challenge
### 2.1. netflix challenge dataset
- data consists of grades for movie
- as a training data, 100M grade data of 480K users was given
- as a test data, 2.8M grade data was given


### 2.2. netflix challenge competition
- the goal of this competition was to decrease RMSE by 10%
- if the goal was achived, the competitor get 1M dollars
- during the time from 2006 to 2009, the performance leaped and bounded


## 3. Basic Latent Factor Model
### 3.1. intro to latent factor model
- to represent users and products as vectors in some vector space
- in other words, use node embedding
- the goal of latent factor model is to learn effective latent factor(get a better node embedding)


### 3.2. loss function
- the criterior
  - the result of inner product of user and product approximates the grade which user made for product as closely as possible
  - in mathematical, minimize $|p_x^Tq_i-r_{xi}|$
- loss function:<br>
  $$
  \mathcal{L} = \sum_{(i, x)\in R}(r_{xi}-p_x^Tq_i)^2
  $$
  but it is easy to overfit the model(learn noises in training data)
- loss function with penalty:
  $$
  \mathcal{L} = \sum_{(i, x)\in R}(r_{xi}-p_x^Tq_i)^2+\left[ \lambda_1 \sum_x||p_x||^2+\lambda_2\sum_i||q_i||^2 \right]
  $$
  where $\lambda_i$ is a hyperparameter which means an amplitude of $L-2$ regularization
  <br>(the added term is called complexity of model)


### 3.3. optimization
- to opmtimize latent factor(node embedding), SGD is used
- gradient descent vs stochastic gradient descent


## 4. Advanced Latent Factor Model
### 4.1. latent factor model with bias of user and product
- bias of a user is the difference of the mean score which the user gave and the global mean score
- bias of a product is the difference of the mean score of the product and the global mean score
- modified latent factor model:
  $$
  r_{xi} = \mu + b_x + b_i + p_x^Tq_i
  $$
  where <br>$\mu$ is the global mean score,<br>$b_x$ is bias of user<br>$b_i$ is bias of product<br>$p_x^Tq_i$ is interaction term
- loss function:
  $$
  \mathcal{L} = \sum_{(i, x)\in R}(r_{xi}-(\mu + b_x + b_i + p_x^Tq_i))^2+\left[ \lambda_1 \sum_x||p_x||^2+\lambda_2\sum_i||q_i||^2 +\lambda_3\sum_x||b_x||^2 +\lambda_4\sum_i||b_i||^2 \right]
  $$


### 4.2. latent factor model with bias of time
- motivation:
  1. the change of netflix system led to the change of mean score
  2. as time goes, the mean score of each movie increases
- modified latent factor model:
  $$
  r_{xi} = \mu + b_x(t) + b_i(t) + p_x^Tq_i
  $$
  where <br>$\mu$ is the global mean score,<br>$b_x(t)$ is bias of user at time $t$<br>$b_i(t)$ is bias of product at time $t$<br>$p_x^Tq_i$ is interaction term


## 5. Practice