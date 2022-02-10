[velog](https://velog.io/@yst3147/MF-Recsys)

## Abstract

- Matrix Factorization model은 기존 nearest-neighbor 기법보다 제품 추천에서 우수하다.

## Introduction

- 소비자에게 가장 적합한 제품을 매칭하는 것은 사용자 만족도와 충성도를 높이는 데 있어 중요하다.
- 따라서 더 많은 소매업체가 제품에 대한 사용자의 관심 패턴을 분석하여 사용자의 취향에 맞는 개인화된 추천을 제공하는 추천 시스템에 관심을 갖게 되었다.
- 좋은 개인화된 추천은 사용자 경험에 또다른 차원을 추가할 수 있기 때문에 이커머스 기업들은 추천시스템을 웹사이트의 주 구성요소로 만들었다.
- 고객은 특정 제품에 대한 만족도를 기꺼이 나타내므로 어떤 제품이 어떤 고객에게 어필하는지에 대한 방대한 양의 데이터를 수집할 수 있다. 
- 기업은 해당 데이터를 분석하여 특정 고객에게 제품을 추천할 수 있다.

## Recommender system strategies

### Content Filtering(콘텐츠 필터링)

- 각 사용자 또는 제품의 특성을 특성화하기 위한 프로필을 생성한다.
- 사용자 프로필에는 설문지에 제공된 인구통계 정보 또는 답변이 포함될 수 있다.
- 프로필을 통해 사용자를 잘 맞는 제품과 연결할 수 있다.
- 콘텐츠 필터링은 이용 가능하지 않을 정보나 수집하기 쉬운 외부 정보를 수집해야 한다.

ex) Music Genome Project(Pandora.com에서 사용)

### Collaborate Filtering(협업 필터링)

- 콘텐츠 필터링의 대안
- 명시적 프로필을 만들 필요 없이 이전 거래 또는 제품 평가 등 과거 사용자 행동에만 의존한다.
- 장점으로는 파악하기 어렵고 프로파일링하기 어려운 데이터를 처리할 수 있다는 것이다.
- 단점으로는 시스템의 새로운 제품과 사용자를 처리할 수 없기 때문에 Cold start 문제가 발생한다는 것이다.
  - Cold start : 정보가 충분하지 않은 상태에서 사용자에게 추천을 해줄 수 없는 문제

> #### 협업 필터링의 주 영역

- Neighborhood Methods
- Latent Factor Models

#### Neighborhood Methods(이웃방법)

아이템 간 관계 또는 사용자 간 관계를 계산하는데 중점을 둔다.

- 아이템 중심 접근 방법
  
  - 사용자가 인접한 아이템의 평가를 기반으로 해당 아이템에 대한 선호도를 평가한다.
  - 아이템의 이웃은 동일한 사용자가 평가할 때 유사한 평가를 받는 경향이 있는 다른 아이템이다.
  - 특정 아이템에 대한 특정 사용자의 평가를 예측하기 위해 이 사용자가 실제로 평가한 영화의 최근접 이웃을 찾는다.

- 사용자 중심 접근 방법
  
  - 특정 사용자가 선호하는 아이템들을 선호하는 비슷한 유저들을 찾는다.
  - 찾은 유저들이 선호하는 또 다른 아이템을 찾아서 추천한다.
    
    

![](https://images.velog.io/images/yst3147/post/8e764871-ef30-430d-98d8-20ab1eabfd35/image.png)

**<center>Fig 1. 서로의 평가를 보완할 수 있는 같은 생각을 가진 사용자를 식별한다.</center>**

#### Latent Factor Models(잠재 요인 모델)

- 평가 패턴에서 추론된 20개에서 100개 사이의 요인에 대해 아이템과 사용자를 모두 특성화하여 평가를 설명하려는 접근 방식이다.
- 아이템에서 발견된 요소는 명백한 차원을 측정할 수 있다.
- 덜 정의된 차원이나 완전히 해석할 수 없는 차원도 존재한다.
- 사용자의 경우 각 요소는 해당 아이템 요소에서 높은 평가를 받은 아이템을 사용자가 얼마나 좋아하는지 측정한다.

![](https://images.velog.io/images/yst3147/post/7960a339-ff4d-4499-bebf-2ed5c4301738/image.png)

**<center>Fig 2. Latent Factor Models 시각화, 2차원 축을 활용해서 사용자와 아이템을 특성화한다.</center>**

## Matrix factorization methods(행렬 분해)

- 잠재 요인 모델의 가장 성공적인 구현 중 일부이다.
- 아이템 평가 패턴에서 추론된 요소의 벡터로 아이템과 사용자를 특성화한다.
- 아이템과 사용자 요소 간의 일치도가 높으면 추천으로 이어진다.

### 데이터

- 사용자를 나타내는 한 차원과 관심 아이템을 나타내는 다른 차원에 있는 매트릭스에 배치되는 다양한 유형의 입력 데이터에 의존한다.
- 아이템에 대한 사용자의 관심을 표현하는 사용자의 명시적(explicit) 피드백이 포함된 데이터가 편리한 데이터이다.
  - 이 때 명시적인 사용자 피드백을 평가라고 한다.
- 명시적 피드백은 희소 행렬로 구성된다.
  - 단일 사용자가 가능한 항목의 적은 비율만 평가했을 가능성이 높기 때문이다.

### 장점

- 추가적인 정보를 통합할 수 있다.
  - 명시적(explicit) 피드백을 사용할 수 없는 경우 암시적(implicit) 피드백을 사용하여 사용자 선호도를 추론할 수 있다.

#### 암시적(implicit) 피드백

- 구매 내역, 검색 내역, 검색 패턴 또는 마우스 움직임 등의 사용자 행동을 관찰하여 의견을 간접적으로 반영한다.
- 일반적으로 이벤트의 존재 또는 부재를 나타낸다.
  - 조밀하게 채워진 행렬로 표현된다.

## A Basic Matrix Factorization Model

- Matrix Factorization 모델은 사용자와 아이템을 차원 f의 joint latent factor space에 매핑한다.
- 사용자-아이템 상호 작용이 해당 space의 내적(inner products)으로 모델링되도록 한다.

### 벡터

- 각 아이템 $i$는 벡터 $q_i$로 연결된다.
  
  - 주어진 아이템 $i$에 대하여 $q_i$ elements는 해당 아이템이 긍정적이거나 부정적인 요소를 소유하는 정도를 측정한다.

- 각 사용자 $u$는 벡터 $p_u$로 연결된다.
  
  - 주어진 사용자 $u$에 대하여 $p_u$ elements는 사용자의 항목에 대한 긍정적이거나 부정적인 요소를 활용해서 관심 정도를 측정한다.

### dot product

- 결과 dot product $q_i^Tp_u$은 사용자 $u$와 아이템 $i$ 간의 상호 작용(아이템 특성에 대한 사용자의 전반적인 관심)을 나타낸다.
- 아이템 $i$에 대한 사용자 $u$의 평가를 근사하고 추정으로 이어진다.
- 각 아이템과 사용자를 factor 벡터에 매핑하면 아래 식 (1)을 사용해서 사용자가 아이템에 부여할 평가를 쉽게 추정할 수 있다.

![](https://images.velog.io/images/yst3147/post/05e8f744-0f3a-4e17-8f00-7cc643652602/image.png)
**<center>식 1</center>**

### 특이값 분해(SVD)

- 정보 검색에서 잠재 의미 요소(latent semantic factors)를 식별하기 위해 사용하는 기술
- 협업 필터링에서 SVD를 적용하려면 user-item rating matrix를 고려해야 한다.
- user-item rating matrix의 희소성으로 인한 높은 결측치 비율이 어려움을 야기한다.
- Conventional SVD는 행렬에 대한 지식이 불완전할 때 정의되지 않는다.
- 상대적으로 적은 수의 known entries들만 부주의하게 처리하면 과적합이 발생하기 쉽다.

### 결측치 처리

- 이전 시스템은 결측 평가를 채우고 평가 매트릭스를 조밀하게 만들기 위해 imputation에 의존했다.
  - 하지만 imputation은 데이터 양을 크게 증가시키기 때문에 비용이 많이 들 수 있다.
  - 부정확한 imputation으로 인해 데이터가 상당히 왜곡될 수도 있다.
- 논문 작성 당시의 최근 연구에서는 정규화된 모델을 통해 과적합을 피하면서 관찰된 평가만을 직접모델링하는 방법을 제안하였다.
- factor 벡터($p_u$ 및 $q_i$)를 학습하기 위해, 시스템은 known rating set에서 정규화된 squared error(제곱 오차)를 최소화시킨다.
- κ는 $r_{ui}$가 알려진 (u,i) 쌍의 집합이다. (train set)

![](https://images.velog.io/images/yst3147/post/d606c40e-6d4f-462f-8ae5-39d5168954a6/image.png)
**<center>식 2</center>**

### 이전에 관찰된 rating 활용

- 시스템은 이전에 관찰된 평가를 fitting하여 모델을 학습한다.
- 그러나 목표는 미래의 알려지지 않은 unknown 평가를 예측하는 방식으로 이전 평가를 일반화하는 것이다.
- 따라서 시스템은 학습된 파라미터를 정규화하여 데이터의 과적합을 피해야 한다.
  - 과적합 크기에 따라 패널티가 부여된다.
- 상수 λ는 정규화의 범위를 제어하며 일반적으로 교차 검증(cross-validation)에 의해 결정된다.

## Learning Algorithms

> - 다음과 같은 방법들을 활용해 2번 식 (squared error)을 최소화한다.
>   - Stochastic Gradient Descent
>   - Alternating Least Squares

### Stochastic Gradient Descent(확률적 경사하강법)

- 주어진 각 훈련 case에 대해 시스템은 $r_{ui}$를 예측하고 예측 오류를 계산한다.
  ![](https://images.velog.io/images/yst3147/post/f8cacfb0-6471-4848-be87-158239178d43/image.png)

- 기울기의 반대 방향으로 학습률에 비례하는 크기로 파라미터를 수정하여 아래 값들을 생성한다.

![](https://images.velog.io/images/yst3147/post/0aee5bcc-02e2-40fe-b827-b64472594fd0/image.png)

- 구현하기 쉽고 비교적 빠르지만 어떤 경우에서는 ALS 최적화를 사용하는 것이 좋다.

### Alternating least squares

- $q_i$와 $p_u$는 모두 미지수이므로 2번 식 (square error)은 볼록하지 않다.
  - 이 때 미지수 중 하나를 수정하면 최적화 문제는 2차식이 되어 optimally하게 해결할 수 있다.
- ALS 기술은 $q_i$를 고정하는 것과 $p_u$를 고정하는 것 사이에서 순환한다.
  - 모든 $p_u$가 고정되면 시스템은 최소 제곱 문제를 해결하여 $q_i$를 계산한다. 그 반대도 마찬가지이다.
- 위의 과정을 반복하여 2번 식 (square error)를 최소화한다.

#### SGD와 비교했을 때 유리한 경우

- 시스템이 병렬화를 사용할 수 있는 경우
  
  - ALS에서 시스템은 다른 아이템 factor와 독립적으로 각 $q_i$를 계산하고 다른 아이템 factor와 독립적으로 각 $p_u$를 계산한다.
  - 이를 통해 알고리즘의 잠재적인 대규모 병렬화를 발생시킨다.

- 암시적(implicit) 데이터에 중점을 둔 시스템인 경우
  
  - train 데이터셋은 희소(sparce)한 것으로 간주될 수 없기 때문에 경사하강법과 같은 단일 훈련 사례를 반복하는 것은 실용적이지 않다. -> ALS는 이러한 경우를 효율적으로 처리 가능하다.

## Adding Biases

### 협업 필터링에서 MF의 이점

- 다양한 데이터 aspects와 기타 응용 프로그램별 요구 사항을 처리할 수 있는 유연성을 가진다.
     -> 이를 위해서는 동일한 학습 프레임워크 내에서 식 1의 조정이 필요하다.

### 평가에 bias가 미치는 영향

- 식은 다른 평가 값을 생성하는 사용자와 아이템 사이의 interaction을 확인하려고 한다.
- 그러나 평가 값에서 관찰된 변동의 대부분은 interaction과 무관한 bias 또는 절편으로 알려진 사용자 또는 아이템과 관련된 효과로 인해 생긴다.
  - 일부 사용자가 bias를 통해 다른 사용자보다 높은 평가를 부여하고 일부 아이템이 다른 아이템보다 높은 평가를 받는 경향을 보인다.
      -> 결국 일부 item은 bias로 인해 다른 item보다 더 낫거나 나쁜 것으로 인식된다.

### $r_{ui}$ rating bias

- $q_i^Tp_u$ 형식의 interaction으로 전체 평가 값을 설명하는 것은 현명하지 않다.
    -> 대신 시스템은 개별 사용자 또는 아이템 bias가 설명할 수 있는 이러한 값의 부분을 식별하려고 시도하고 실제 interaction 부분만 factor 모델링에 활용한다. 
- $r_{ui}$ 평가와 관련된 bias의 1차 근사치는 다음과 같다.

![](https://images.velog.io/images/yst3147/post/854068dd-9560-4d74-9964-f40419a9227b/image.png)
**<center>식 3</center>**

- $r_{ui}$ 평가와 관련된 bias는 $b_{ui}$로 표시된다.
  - 사용자와 아이템 효과를 설명한다.
- 전체 평균 평가는 $\mu$로 표시된다.
- parameter ${b_u}$와 ${b_i}$는 각각 사용자 u와 아이템 i의 관찰된 편차(deviation)을 나타낸다.

ex) Titanic 영화에 대한 $\mu$ = 3.7, ${b_i}$ = 0.5, ${b_u}$ = -0.3일 때
    -> 사용자 u가 평가한 Titanic 평점 (3.7 + 0.5 - 0.3) = 3.9 

### bias를 통한 rating 및 loss 계산

#### rating

- bias는 식 1을 다음과 같이 확장한다.

![](https://images.velog.io/images/yst3147/post/c0087248-c21a-4c75-8a39-253bc315514f/image.png)
**<center>식 4</center>**

- 식 4에서 관찰된 평가 구성 요소
  - global average
  - 아이템 bias
  - 사용자 bias
  - 아이템-사용자 interaction
    -> 각 구성 요소는 관련된 signal의 일부만 설명 가능하다.

#### loss

- squared error(제곱 오차) 함수를 최소화하여 학습한다. (식 5)

![](https://images.velog.io/images/yst3147/post/0fa7ef81-2493-4f5e-b228-1f748445ab80/image.png)
**<center>식 5</center>**

- bias는 관찰된 signal의 대부분을 포착하는 경향이 있으므로 정확한 모델링이 중요하다.

## Additional Input Sources

### Cold Start 문제 및 해결책

#### 문제

- 시스템은 Cold Start 문제를 처리해야 한다.
- 많은 사용자는 매우 적은 점수만을 제공하여, 그들의 취향에 대한 일반적인 결론을 내기 어렵다.

#### 해결책

- 해결책은 사용자에 대한 추가 정보 소스를 통합하는 것이다.

### Implicit 피드백

- 추천 시스템은 암시적(implicit) 피드백을 사용하여 사용자 선호도에 대한 insight를 얻는다.
- 실제로 사용자가 명시적(explicit) 평가를 제공하려는 의지와 상관없이 행동 정보를 수집할 수 있다.
    -> 사용자가 제공하는 평가 외에도 사용자의 구매 혹은 검색 기록을 사용하여 경향을 파악할 수 있다.

### Boolean Implicit 피드백

- 단순함을 위해 Boolean Implicit 피드백을 고려할 수 있다.
- $N(u)$는 사용자 u가 암시적으로 선호를 나타낸 아이템 집합을 의미한다.
- 시스템은 사용자가 암시적으로 선호하는 아이템을 통해 사용자를 프로파일링한다.
  - 이 때 $x_i$가 latent factor space $R^f$ 에 속하는 아이템 i와 연관되는 새로운 아이템 factor들이 필요하다.
- 따라서 $N(u)$에 속한 항목에 대한 선호도를 보인 사용자들을 다음과 같은 벡터로 나타낸다.

![](https://images.velog.io/images/yst3147/post/88b2a360-c1dd-4b20-bb0c-7503b74e2fae/image.png)

- 합을 다음 식과 같이 normalizing 하는 것이 이득일 수도 있다.

![](https://images.velog.io/images/yst3147/post/33ea06f2-ea26-459d-a025-dbfaa7da2ca3/image.png)

### Known User Attributes

- 인구, 통계 등 알려진 사용자 속성은 또다른 정보 속성이다.
- $A(u)$는 사용자 u에 대해 설명할 수 있는 속성 집합이다
     -> 단순성을 위해 Boolean 속성을 사용한다.
- latent factor space $R^f$에 속하는 $y_a$는 고유한 factor vector이다.
    -> 사용자 관련 속성 집합을 통해 사용자를 설명하는 각 속성에 해당한다.

![](https://images.velog.io/images/yst3147/post/5af8ef89-a112-45d7-9735-339eb8581d63/image.png)

### Enhanced User Representation

- Matrix Factorization 모델은 향상된 사용자 표현과 함께 모든 signal 소스를 포함해야 한다.

![](https://images.velog.io/images/yst3147/post/b8cdc4d1-7785-473b-9172-fbc46a16bb0d/image.png)
**<center>식 6</center>**

- 논문에서는 향상된 사용자 표현을 주로 다뤘지만 필요에 따라 아이템에 대해서도 유사한 처리를 할 수 있다.

## Temporal Dynamics

### Temporal Effect

- 지금까지 제시된 모델은 static 모델이었다.
- 하지만 실제로 아이템에 대한 인식과 인기는 새로운 선택이 등장함에 따라 끊임없이 변한다.
- 마찬가지로 사용자의 성향도 진화하여 사용자들의 스스로 취향을 재정의한다.
- 따라서 시스템은 사용자-아이템 interaction은 동적, time-drifting 특성을 반영하는 temporal effect를 설명해야 한다.

### MF에서의 Temporal Effect 모델링

- Matrix Factorization 접근 방식은 temporal effect를 모델링하는데 적합하여 정확도를 크게 향상시킬 수 있다.
- 평가를 별개의 term으로 분해하면 시스템은 서로 다른 temporal aspect를 개별적으로 처리할 수 있다.
- 다음 용어들은 시간이 지남에 따라 달라진다.
  - item biases : $b_i(t)$
  - user biases : $b_u(t)$
  - user preferences : $p_u(t)$

### 여러 Temporal Effect

#### 아이템

- 아이템의 인기도가 시간이 지남에 따라 변할 수 있다.
- 외부 이벤트에 의해 인기가 올라가거나 내려갈 수 있다.
- 이러한 모델은 item bias $b_i$를 시간 함수로 취급한다.

#### 사용자

- 사용자는 시간이 지남에 따라 baseline 평가를 바꿀 수 있다. 
- 다음과 같은 여러 요인들을 반영한다
  - 사용자 평가 scale의 natural drift
  - 사용자가 다른 최근 평가와 관련되게 평가한다는 사실
  - 가정 내 평가자의 identity가 시간이 지남에 따라 변할 수 있다는 사실
- 이러한 모델에서 user bias $b_u$는 시간 함수이다.

### Temporal Dynamics

- Temporal dynamics(시간적 역학)은 사용자 선호에 영향을 미치고 아이템-사용자 interaction에 영향을 준다.
- 사용자는 그들의 선호를 시간이 지남에 따라 바꾼다.
  - ex) 선호 장르의 변화, 특정 배우와 감독에 대한 인식 변화
- 모델은 사용자 factor($p_u$ vector) 를 시간함수로 사용하여 이 효과를 설명한다.
- 아이템은 사람과 달리 static하기 때문에 static 아이템 특성 $q_i$를 지정한다.
- time-varying 파라미터에 대한 정확한 파라미터화는 식 4를 시간 t에서의 평가에 대한 dynamic 예측 규칙(식 7)으로 대체한다.

![](https://images.velog.io/images/yst3147/post/0f638f1f-3b11-473e-90b2-c7b8e3fef685/image.png)
**<center>식 7</center>**

## Input With Varying Confidence Levels

- 몇몇 설정에서, 관찰된 모든 등급이 동일한 weight(가중치)나 confidence(신뢰도)를 갖는 것은 아니다.
  - ex) 대규모 광고는 특정 항목에 대한 투표에 영향을 미칠 수 있다.
- 시스템은 특정 항목의 평가를 tilt하려는 adversarial 사용자를 직면할 수도 있다.

### Implicit Feedback Base System

- Implicit Feedback을 기반으로 구축된 시스템에서는 사용자의 진짜 선호도를 정량화하기 어렵다.
- 따라서 item을 좋아할지 싫어할지와 같은 cruder binary 표현으로 작동한다.

#### Confidence Scores

- 이러한 경우 추정된 선호도와 함께 confidence scores(신뢰도 점수)를 추가하는 것이 중요하다.
- action 빈도(ex. 사용자의 프로그램 시청 시간, 특정 item 구매 빈도)를 설명하는 사용 가능한 숫자 값에서 신뢰도를 얻을 수 있다. 
- 숫자 값들은 각 관측치에 대한 confidence(신뢰도)를 나타낸다.

#### Event(일회성 이벤트)

- 사용자 선호도와 관련 없는 다양한 factor들로 인해 One-Time event(일회성 이벤트)가 발생할 수 있다.
- 하지만 반복되는 이벤트는 사용자 의견을 반영할 가능성이 높다.

### MF에서의 Confidence Levels

- Matrix Factorization 모델은 다양한 confidence level(신뢰 수준)을 쉽게 수용할 수 있으므로 덜 의미있는 관측치에 가중치를 덜 줄 수 있다.
- 관측치 $r_{ui}$에 대한 신뢰도가 $c_{ui}$로 표시된다.
- 모델은 다음과 같이 신뢰도를 설명하기 위해 squared error(제곱 오차) cost function(식 5)를 향상시킨다(식 8). 

![](https://images.velog.io/images/yst3147/post/8a684435-b701-4c88-a5ae-2170cf6f096c/image.png)
**<center>식 8</center>**

## Netflix Prize Competition

### Netflix Data Matrix Factorization Factor

Figure 3은 Netflix data matrix factorization의 첫 2가지 factor를 보여 준다.

- 선택된 영화들은 2차원 공간에서 그들의 factor vectors들에 의해 적절한 spot에 위치한다.
- 각 plot은 독특한 장르들을 보여 준다.

![](https://images.velog.io/images/yst3147/post/5001970a-e38a-4bd0-be21-58081ed353fb/image.png)

**<center>Fig 3. Netflix data matrix factorization의 첫 2가지 factor 시각화</center>**

### Matrix Factorization Model Accuracy

Figure 4는 다양한 모델과 파라미터들이 RMSE와 factorization의 구현 성능에 미치는 영향을 보여 준다.

> - factor 모델 종류
>   - plain factor
>   - bias 추가
>   - 암시적(implicit) 피드백으로 사용자 profile 강화
>   - temporal 구성요소를 추가한 두 가지 변형(v1, v2)

- 시각화는 각 factor 모델의 RMSE(Root-Mean-Square-Error) 수치를 보여준다.
- 정확도는 factor model의 차원(plot에서 숫자로 표시된)이 증가하면 향상된다.
- description이 더 뚜렷한 파라미터들이 포함된 more refined factor 모델이 더 정확하다. 

![](https://images.velog.io/images/yst3147/post/732f239b-6a9f-40d5-85b5-fb880f5a5061/image.png)
**<center>Fig 4. Matrix Factorization Model Accuracy</center>**

## Conclusion

- 논문 작성 기준으로 Matrix Factorization 기술은 collaborative filtering 추천에서 지배적인 방법론이 되었다.
    -> Netflix Prize 데이터와 같은 데이터 세트에 적용했을 때 nearest-neighbor 기술보다 더 높은 정확도를 제공한다.
- 시스템이 비교적 쉽게 학습할 수 있는 컴팩트한 메모리 효율을 갖는 모델을 제공한다.
- 모델이 다양한 형태의 피드백, temporal dynamics, confidence level(신뢰 수준)과 같은 데이터의 많은 중요한 측면을 자연스럽게 통합할 수 있다.
