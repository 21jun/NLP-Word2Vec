공부하며 생각과 코드를 정리해두는 저장소

# Word2Vec

## Word2Vec 개요

NN에 input으로 text를 넣을 수 없다.
> text를 vector로 바꾸는 작업이 필요하다.

가장 간단한 방법은 encoding이다. 그 중에서도 one-hot encoding을 사용해보자.
> encoding은 말 그대로 각 단어를 하나의 벡터로 맵핑만 한 것
> 각각의 벡터간의 similarity가 없다.


encoding의 문제점을 해결하기 위해서, embedding을 사용해보자
> one-hot encoding 의 차원(단어 수) 보다 작은 차원 공간으로 embedding 벡터를 만들자.

즉, 기존의 one-hot encoding 의 sparse 한 행렬이라는 문제점을 차원 축소로 dense한 행렬를 생성하여 해결하자.
> embedding 벡터끼리 simiarity를 계산할 수 있게된다.


차원 축소 알고리즘은 여러가지(PCA, AutoEncoder..)가 있지만
> word embedding을 구현하기 위해서 word2vec을 사용해보자.
 
word2vec의 기본 전제는 같이나오는 단어(윈도우 내에 존재)끼리 유사도가 있을 것이라는 가정이 있다.
> 같이 나오는 단어가 꼭 유사도가 있지는 않지만 이를 감안하고 수행 (한계점)

## CBOW와 Skip-Gram

## Skip-Gram 의 학습방식

## Skip-Gram 이 CBOW 보다 좋은 성능을 갖는 이유

```
학습 후 사용할 벡터는 중심단어에 대한 임베딩이다.
CBOW는 중심단어(벡터)의 업데이트 기회는 단 한번이다.
(주변 단어 N 개를 가지고 중심단어 1번 업데이트)
하지만 Skip-gram은 1개의 중심단어에 대해서 N개의 주변단어를 각각 학습 시키므로 총 N번의 업데이트를 수행한다.
예를들어 윈도우 크기가 2인 Skip-gram은 중심단어가 4번(주변 단어수) 업데이트됨
```
![Image](img/SkipGramExample.png)

위와 같이 skip-gram은 중심단어가 여러번의 update 기회를 갖는다.

그러므로 보통 skip-gram이 CBOW보다 좋은 성능을 낸다고 알려져있다.

![Image](img/SkipGram.png)
```
word2vec은 일종의 NN으로 AutoEncoder와 비슷한 구조를 가진다.
하지만, input과 label 이 동일한 autoencoder와 다르게 
skip-gram은 input이 중심단어, label 이 주변단어가 된다.
```
## 흔한 오해

실제로 NLP를 위한 NN을 구성할때 word2vec을 사용하지는 않는다. 
(word2vec을 사용한다는 것은 pre-trained된 임베딩을 사용하겠다는 소리. 즉, 데이터가 적다면 고려해 볼 수 있다.)

그 이유는 실제로 해결하려는 task에 필요한 임베딩이 word2vec의 같이 등장하는 단어가 유사도가 높다고 계산한 임베딩과는 다를 것이기 때문이다.

그렇다면 실제 NN에서 임베딩을 어떻게 구하는가?
> input layer에 embedding layer를 사용하자. 

(embedding layer) y = emb(x) = Wx

W = d * |V| 크기의 2차원 행렬

input으로 one-hot vector(단어)가 들어오면 W의 특정 행 만 반환
> 해당 행이 해당 단어의 임베딩 벡터 

그 뒤로는 NN을 구성하고, 최종적으로 모델으로부터 구한 Loss에 따라 역전파 및 경사하강법을 수행하여 embedding layer의 W(가중치)를 변경할 수 있다.
> 풀려고하는 task에 알맞은 임베딩이 생성될 것.

pytorch에서의 구현은 nn.Embedding layer를 입력단에 넣어 구현할 수 있다.



