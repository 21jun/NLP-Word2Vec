# Skip-Gram Negative Sampling

![Image](img/SGNS structure.png)

위 구조를 구현하기 위해 두개의 embedding layer(u, v)를 두고
center word는 u로 임베딩하고,

negative sampling 된 word와 neighbor word를 v로 임베딩하여 구현

Cross Entropy Loss를 모든 vocab에 대해서 계산하지 않고,

center+neighbor+negative samples 에 대해서 만 계산하기 위해 

forward 에서 loss를 계한하여 return 하도록 구현 (nn.CrossEntropyLoss 를 사용하지 않음)

![Image](img/SGNS result.png)