# Skip-Gram 

```py
corpus = ['king is a strong man', 
          'queen is a wise woman', 
          'boy is a young man',
          'girl is a young woman',
          'prince is a young king',
          'princess is a young queen',
          'man is strong', 
          'woman is pretty',
          'prince is a boy will be king',
          'princess is a girl will be queen']
```
위와 같은 데이터를 가지고 임베딩을 구현해보자.


![Image](../img/SkipGramSimpleResult.png)


## nn.Linear vs nn.Embedding 

https://datascience.stackexchange.com/questions/32460/nn-embedding-layer
```
nn.embedding,  nn.Linear 는 사실상 같은 역할을한다. 
하지만,  nlp task는 인풋이 원핫벡터로 sparse하기 때문에 matmul 등을 수행하면 연산이 매우 느릴것이다(리니어의 방법)
임베딩은 이때 matmul을 수행하지않고 lookup하기 때문에 매우빠르다
이런 이유로 같은 역할이지만 nn.Embedding 을 쓴다.
(코드에 명시적으로 Embedding 이라고 적어주는 효과도 있을듯)
```