[TOC]

# 1 AI for MATH - Bayes' theorem


## 1.1 조건부 확률(Conditional probability)

<br>

$P(A|B)$는 사건 $B$가 일어났을 때 $A$가 일어날 확률을 의미하고 이는 조건부 확률이라고 한다. 그리고 일반적으로 아래와 같이 계산된다.
<br/>
$$
P(A|B) = \frac{P(A \cap B)}{P(B)}
$$

<br/>

위 식을 사용하면 $P(A\cap B)$는 두 가지 방식으로 표현될 수 있다.
<br/>

$$
P(A\cap B) = P(B)P(A|B) = P(A)P(B|A)
$$
<br/>

이를 통해 $P(A|B)$는 아래와 같이 재표현될 수 있다.
$$
P(A|B) = P(A) \frac{P(B|A)}{P(B)}
$$

<br/>
<br/>
<br/>

## 1.2 베이즈 정리와 그 용어

<br>

$$
P(\theta | \mathcal{D}) = P(\theta) \frac{P( \mathcal{D} | \theta )}{P(\mathcal{D})}
$$

$P(\theta | \mathcal{D})$ : 사후확률(posterior)  
$P(\theta)$ : 사전확률(prior)  
$P( \mathcal{D} | \theta )$ : 가능도(llikellilhood)  
${P(\mathcal{D})}$ : Evidence

$\mathcal{D}$는 관측자가 관찰하는 데이터를 의미한다고 생각하면 된다. 그리고 $\theta$는 어떤 가정(hyperthesis) 또는 모델링하는 이벤트, 추정 및 계산하고 싶은 모수라고 생각하면 된다.  
사전확률이란 모델링 이전에 관측자가 가정한 확률값이다.  
그리고 가능도는 사전에 가정한 모수 또는 확률값 하에 어떤 데이터가 관측될 확률이다.  
Evidence는 데이터 자체의 분포이다.  

즉, 사전확률과 데이터를 기반으로 베이즈정리를 이용해 사후확률을 구할 수 있다는 것이다.  

<br/>

### **EX.1**
*COVID-99의 발병률이 10%로 알려져있다. COVID-99에 실제로 걸렸을 때 검진될 확률은 99%이고 실제로 걸리지 않았을 때 오검진될 확률이 1%라고 할 때, 어떤 사람이 질병에 걸렸다고 검진결과가 나왔을 때 정말로 COVID-99에 감염되었을 확률은?*
  
우선 이 상황에서 사전확률을 발병률로 $\mathcal{D}$는 관촬된 결과를 통해 얻은 검사에 대한 오진과 정진의 관찰결과 데이터라고 가정하자.

그렇다면 검진결과가 양성일 때 실제로 COVID-99의 감염되었을 확률은 아래와 같이 계산할 수 있다.  


$$
P(\theta | \mathcal{D}) = P(\theta)\frac{P( \mathcal{D} | \theta )}{P(\mathcal{D})}
= 0.1 \times {\frac{0.99}{ \sum_{x \in \Omega} P(\mathcal{D} | x)P(x) } } 
= 0.1 \times {\frac{0.99}{ 0.99\times 0.1 + 0.01\times 0.9 } }=\frac{11}{12}$$

즉, 주어진 상황에서 베이즈 정리를 통해 구한 확률은 $0.916$이다.

<br/>


### **EX.2**
*COVID-99의 발병률이 10%로 알려져있다. COVID-99에 실제로 걸렸을 때 검진될 확률은 99%이고 실제로 걸리지 않았을 때 오검진될 확률이 10%라고 할 때, 어떤 사람이 질병에 걸렸다고 검진결과가 나왔을 때 정말로 COVID-99에 감염되었을 확률은?*

첫 예시와 다르게 $P(\mathcal{D} | \neg \theta)=0.1$로 계산해주면 되고 그 결과값은 $0.524$ 정도의 값으로 극격히 낮아진 값을 얻을 수 있다.

## 1.3 오류와 그 종류

오류는 말 그대로 정확하지 않은 결과를 낸 것을 뜻한다. 그리고 세부적으로는 1종 오류와 2종 오류라는 두 가지가 있다.  
1종 오류는 영어로 False Positive라고 한다. 즉 양성이 나왔지만 실제로는 음성일 때의 오류를 뜻한다.  
2종 오류는 그 반대인 False Negative이다. 즉 음성이 나왔지만 사실은 양성일 때의 오류를 뜻한다.  
물론 모든 오류가 최소화된 상태가 바람직하다고 볼 수 있지만 실제 데이터 분석이나 어떤 기계학습의 모델링을 할 때 그 조건과 상황에 따라 1종 오류는 증가해도 2종 오류를 줄이거나 그 반대의 상황으로 적합시키기도 한다.

## 1.4 베이저 정리를 통한 정보의 갱신

베이즈 정리를 통해 새로운 데이터가 들어왔을 때 앞서 계산한 사후확률을 사전확률로 사용하여 갱신된 사후확률을 계산할 수 있다.

그 말은 즉 $P(\theta)$를 기존에 계산한 $P(\theta|\mathcal{D})$로 대치시켜 계산한다는 뜻이다.

*앞서 COVID-99 판정을 받은 사람이 두 번째 검진을 받을 때도 양성이ㅣ 나왔을 때 진짜 COVID-99에 걸렸을 확률은?*

$$
P(\mathcal{D}^*) = P(\mathcal{D}^* | \theta)P(\theta) + P(\mathcal{D}^* | \neg\theta)P(\neg\theta) = 0.99\times 0.524+0.1\times 0.476 = 0.917...
$$

즉, 두 번째도 양성일 때 그 사람이 실제로 양성일 확률은 0.917정도로 매우 높은 정확도를 확보할 수 있게 된다는 것이다.

## 1.5 주의할 점(분석의 시사점)

조건부 확률은 유용한 통계적 해석을 제공하지만 인과관계를 추론할 때 함부로 사용해서는 안된다. 실제 인과관계는 데이터 분포의 변화에 강건한 예측모형을 만들 때 필요하다(robust를 번역한 것). 조건부확률을 이용해서 예측모형을 만들면 실제 훈련 데이터에 대해서는 높은 정확도를 보여줄 수 있지만 새로운 데이터에는 잘 적합되지 않는 결과를 초래하기도 한다.

인과관계를 알아내기 위해서는 중첩요인(confounding factor)의 효과를 제거하고 원인에 해당하는 변수만의 인과관계를 계산해야 한다.

예를 들어 키와 지능지수의 상관관계를 실제 아무런 전처리나 과정 없이 분석한다면 놀랍게도 그 둘은 양의 상관관계를 갖는다. 그러나 그 이유는 사실 두 변수 사이에 중첩되어 있는 나이라는 변수 때문이다. 사실 나이가 많아지면 키는 커진다(아동과 성인). 그리고 성인이 되어가면서 인지능력이 발달한다. 그렇기 때문에 이런 나이라는 변수 때문에 둘 사이에는 인과관계가 있다는 잘못된 예측을 하게 되는 것이다. 그러기에 인과관계를 만들 때에는 늘 여러 변수들 사이에 중첩요인을 제거하고 원인에 해당하는 변수만의 인과관계를 만들어야 한다.


||overall|patients with small stone|patients with large stone|
|----|----|----|----|
|treatment a|78%(273/350)|93%(81/87)|73%(192/263)|
|treatment b|83%(289/350)|87%(234/270)|69%(55/80)|  


<br><br><br><br><br>



# 2 Introduction to Deeplearning - Opening
좋은 딥러너의 조건은 무엇인가?(what makes you a good deep learner)
1. 구현 능력(implementation skills)
2. 수학적 능력(mathematical skills) - linear algebra, probability and so on
3. 최근 연구의 흐름에 대한 인지(knowing a lot of recent papers)

위와 같은 세 가지가 좋은 DL 전문가가 되기 위한 조건이라고들 한다.

그렇다면 우선 DL이 무엇인지 알아볼 필요가 있다. 대다수의 사람들은 인공지능, ML, DL 등의 개념을 서로 혼동하며 쓴다. 물론 사람, 시각, 책에 따라 완벽히 동일한 정의를 갖고 있지는 않지만 AL > ML > DL 순으로 그 개념을 정리할 수도 있다.  
AI는 인간의 지능을 흉내내는 전반의 것을 포함한다. 그리고 이 AI의 영역 속에서 ML은 일반적인 프로그래밍의 패턴인 INPUT + RULE = OUTPUT이 아닌 INPUT + OUTPUT = RULE의 방식으로 데이터 기반의 룰을 만드는 학문 또는 그 기술이라고 볼 수 있다.  
그리고 여기서 더 나아가 DL은 ML을 여러 층으로 쌓아가면서 neural network를 만들어 ML이 풀지 못하거나 그보다 더 뛰어난 성능을 내는 결과를 만드는 학문 또는 그 기술이라고 볼 수 있다.  

그렇다면 deep learning의 중요한 구성요소는 무엇이 있는가 보면 다음과 같다고 말할 수 있다.
1. data that the model can learn from
2. model how to transform the data
3. loss funciton taht quantifies the badness of model
4. algorithm to adjust the parameters to minimize the loss

그러기 때문에 앞으로 DL과 관련된 어떤 논문 또는 페이퍼를 보게 될 떄 위의 네 가지를 유의하며 보는 것이 그 아티클을 이해하는데 매우 도움이 될 것이다.




# Introduction to Deeplearning - Historical review

1. 2012 - AlexNet - 딥러닝이라는 블랙매직이 정말로 성능을 발휘하기 시작한 사례
2. 2013 - DQN - Q러닝이라는 강화학습 방법을 적용한 DL
3. 2014 - Encoder/Decoder, Adam - NLP, 기계번역의 큰 발전과 웬만하면 잘 돌아가는 옵티마이ㅣ저의 발견
4. 2015 - GAN, ResNet - 딥러닝의 딥러닝이 가능하진 계기, 왜 딥러닝이 잘 될 수 있는가에 대한, 
5. 2017 - Transformer - Attention
6. 2018 - BERT - 바이디렉션, fine-tuned NLP model, 기존의 학습된 모델을 기반으로 특성에 맞게 조정된 NLP모델
7. 2019 - GPT - BERT의 끝판왕
8. 2020 - self-supervised learning - 지도학습을 할 때 비지ㅣ도 데이터를 이용해 더 정교한 모델을 만들어가는 것

