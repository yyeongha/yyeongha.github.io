---
title: CNN architecture
---
Alexnet Architecture
* Convolutoion layer 5개 + fully connected layer 3개
![Alexnet Architecture](/assets/img/favicons/Alexnet%20Architecture.png)
# Convolution
## Convolution operation
stride = 1 : 한번에 한칸씩 이동함

## 2-D convolution

## Activation
딥러닝 네트워크에서 노드에 입력된 값들을 비선형 함수에 통과시킨 후 다음 레이어에 전달하는데, 이 함수를 활성함수라고 한다.
선형함수가 아니라 비선형함수를 사용하는 이유는 딥러닝 모델의 층을 깊게 가져갈 수 있기 때문
활성함수는 입력데이터를 다음레이어로 어떻게 출력할 수 있을지 결정한다. 즉 활성함수는 입력을 받아 활성화 혹은 비활성화를 결정함.

### sigmoid function
x의 값에 따라 0~1사이의 값을 출력하는 s자형 함수
음수값을 0에 가깝게 표현하기 때문에 입력값이 최종레이어에 미치는 영향이 적게 미침
모든 실수값 0~1인 미분가능한 수라서 분류문제, 비용함수에서 많이 씀
리턴값이 확률값이라서 결과를 확률로 해석할때 유용하다.

### ReLU (rectified linear unit)
시그모이드 함수가 갖는 gradient vanishing(기울기 소실) 문제를  해결하기 위한 함수.
x가 0보다 크면 기울기가 1인 직선, x가 0보다 작으면 함수값이 0이되어 0보다 작은값들에서는 뉴런이 죽을 수 있는 단점이 있음

### Leaky ReLU

### softmax

## Pooling
### MaxPooling
### AvgPooling
### GlovalAvgPooling

## Dropout, Fully Connected layer
### Dropout
### Fully Connected layer

---
