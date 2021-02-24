# Machine Learning Based on Graph: Recommendation System

## 1. Recommendation System around us
### 1.1. product recommendation at Amazon
- Amazon shows a list of products for the current user
- if a user sees a detail of some product, Amazon will show him/her products good to buy together or instead
 

### 1.2. movie recommendation at Netflix
- Netflix shows a list of movies for the current user

### 1.3. video recommendation at Youtube
- Youtube shows a list of videos for the current user
- Youtube shows a list of videos related with the current playing video

### 1.4. friend recommendation at Facebook
- Facebook shows a list of users good to be a friend

### 1.5. recommendation system and graph
- recommendation system shows a list of objects that the current user might prefer or purchase
- purchase history can be transformed into a graph
- if reviews and grades are considered, the graph will be weighted
- in the aspect of graph, the key tasks of recommendation system are to predict edges that seem to be added soon and to infer missing weights

## 2. Content-Based Recommendation System
### 2.1. principle of recommendation system
- content based recommendation system gives a list of objects that are similar with products previously purchased
  - recommend movies with same genre
  - recommend movies whose director is same
  - recommend products with same category
  - recommend friends who graduated same schools

- process
  1. collect item profiles that a user prefers
     -  item profile is a vector representing properties of item
     -  for example, one-hot encoding vector for genre, director, actor, etc can be a item profile of movie 
  2. form a user profile
     -  user profile is a vector calculated by weighted mean of item profiles preferred
  3. match item profiles with the user profile
     - for user profile $u$ and item profile $v$, cosine similarity suggested below is obtained
    $$
    \frac{\vec{u} \cdot \vec{v}}{||\vec{u}||\cdot ||\vec{v}||}
    $$

### 2.2. pros and cons
- pros
  1. it does not need other user profiles
  2. it is appliable to users with unusual preference
  3. it is appliable to new items which no one purchased
  4. it is explainable

- cons
  1. if an item has no additional information, it can be recommended by the system
  2. it is not appliable to newbies(without purchase history)
  3. it is easy to recommend too narrow range of items because of overfitting


## 3. Collaborative Filtering
### 3.1. principle of collaborative filtering
- process<br>let $x$ be the current user 
  1. find users with preference similar with $x$
      - similarity of preference can be obtained from correlation coefficient
      $$
      sim(x, y) = \frac{\sum_{s\in S_{xy}}(r_{xs}-\bar{r_{x}})(r_{ys}-\bar{r_{y}})}{\sqrt{\sum_{s\in S_{xy}}(r_{xs}-\bar{r_{x}})^2} \sqrt{\sum_{s\in S_{xy}}(r_{ys}-\bar{r_{y}})^2}}
      $$
  2. find items that they preferred
  3. recommend items to $x$ with inference of grades for items
      $$
      \hat{r_{xs}} = \frac{ \sum_{y\in N(x;s)}sim(x, y)\cdot r_{ys} }{\sum_{y\in N(x;s)}sim(x, y)}
      $$
      where $N(x;s)$ is the set of users which have the most similar preference

### 3.2. pros and cons
- pros
  1. an additional information of products is not required

- cons
  1. it is effective only if a size of the grade data is sufficient
  2. it is not appliable to new products and new users
  3. it is not appliable to users with unusual preference

## 4. Evaluation of Recommendation System
### 4.1. splitting data
- in the usual sense

### 4.2. evaluation index
- MSE
- RMSE

## 5. Practice

