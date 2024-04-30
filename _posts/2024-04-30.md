---
title: [kospeech] Open-source toolkit for end-to-end Korean speech recognition 논문 리뷰
---

논문 링크 : https://www.sciencedirect.com/science/article/pii/S2665963821000026

코드 링크 : https://github.com/sooftware/kospeech?tab=readme-ov-file

* end-to-end 
: 입력에서 출력까지 파이프라인 네트워크 없이 신경망으로 한번에 처리한다는 의미이다. 

![end-to-end](https://images.velog.io/images/jeewoo1025/post/c07c47d5-fc1b-4212-9a08-193646604898/image.png)


## 1. Introduction
 전통적인 자동 음성 인식(Automatic Speech Recognition, ASR) 시스템은 음향 모델, 어휘 사전 및 언어 모델을 포함합니다. 이러한 매우 복잡한 구조는 단일 디코딩 네트워크를 구축하는 데 사용됩니다.
 반대로 end-to-end ASR 시스템은 많은 장점을 가지고 있습니다. 우선 위에 작성된 모든 프로세스를 하나의 시스템으로 관리하기 때문에 훨씬 편리합니다. 그래서 deep speech 2, Listen, Attend and Spell (LAS), Transformer, RNN-Transducer 및 Joint CTC-Attenetion LAS 등 많은 end-to-end 모델이 제안되었습니다.
 도메인 지식 없이도 접근할 수 있을 정도로 간단하고 모델 구조가 명확하고 간결하기 때문에 더 직관적입니다. ASR의 다양한 구현이 그렇게 공개됩니다. 그러나 LibriSpeech, WSJ, Switchboard, CallHome과 같은 이러한 오픈 소스의 대부분은 영어와 같은 비한국어를 다루고 있습니다. 한국어 ASR 오픈 소스의 부재는 한국어 음성 인식의 진입 장벽을 높이는 주요 요인 중 하나가 되었습니다.
 따라서 지금까지 출시된 한국어 음성 데이터 세트 중 가장 큰 KsponSpeech를 처리할 수 있는 툴킷인 Kospeech를 열기로 결정했습니다. KsponSpeech는 1000시간 분량의 음성 데이터 전사 쌍으로 구성되어 있습니다. 

* ksponspeech 논문 : https://www.mdpi.com/2076-3417/10/19/6936

KsponSpeech의 텍스트 전처리가 어렵기 때문에 KsponSpeech 데이터 세트에 대한 전처리 방법도 설명합니다. 사용자는 음성 전사와 철자 전사 중에서 선택하는 방법이나 특수 문자를 제거하는 방법 등을 참조할 수 있습니다.
 또한 다양한 유닛에서 한국어 음성 인식을 수행하려는 연구자를 위해 문자, 하위 단어 및 자소 단위의 데이터 세트를 처리하는 방법을 구성했습니다. 모델 부분에서 KoSpeech는 딥 러닝 기반 end-to-end 음성 인식 모델인 Deep Speech 2, LAS, Transformer 및 Joint CTC-Attention LAS를 제공합니다.
 또한 특징 추출 방법, 순환 신경망(RNN), 장단기 메모리(LSTM), 게이트 순환 유닛(GRU)과 같은 순환 신경망 유형과 같은 다양한 옵션이 제공됩니다. 이들은 모델 성능과 높은 상관 관계가 있습니다.
연구자들은 다양한 옵션으로 음성 인식 작업을 실험할 수 있습니다. 또한 연구자의 시간과 비용을 절약하기 위해 사전 훈련된 모델과 사전 처리된 녹취록을 무료로 개방했습니다. 우리는 이 소프트웨어를 계속 개발할 것입니다. 우리의 연구가 팔로워와 초보자를 위한 지침이 될 수 있기를 바랍니다.


## 2. ASR system
 ASR 작업은 상당히 복잡한 파이프라인으로 구성되어 있습니다. KoSpeech는 특징 추출, 모델 훈련 및 디코딩과 같은 모든 복잡한 파이프라인을 지원하며 사용자에게 이 과정에서 필요한 옵션을 선택할 수 있도록 제공합니다. KoSpeech에는 50개 이상의 옵션이 있지만 세 가지 중요한 사항에 대해서는 간략하게 설명합니다. 위의 세 가지 옵션 외에도 옵티마이저, 모델 차원 및 손실 함수와 같은 옵션이 있습니다.

### 2.1. Output-unit
 음성 인식 작업에서 출력 단위는 중요한 하이퍼 파라미터입니다. KoSpeech는 표 1에 시각화된 문자, 하위 단어 및 자소 단위의 처리를 제공합니다. 연구자는 원하는 출력 단위를 지정할 수 있습니다.

![Table1](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-04-30-kospeech/Table1.png?raw=true)

### 2.2. Model architecture
 KoSpeech의 모델 아키텍처는 다음과 같습니다. (a) Deep Speech 2, (b) Listen Attend and Spell, (c) Transformer, (d) Joint CTC-Attention LAS 

#### (a) Deep speech 2
 Deep Speech 2는  Connectionist Temporal Classification (CTC) 손실이 있는 ASR 작업에서 더 빠르고 정확한 성능을 보여주었습니다
(그림 1 참조).

![Fig. 1](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-04-30-kospeech/Fig.%201.png?raw=true)

※ Connectionist Temporal Classification (CTC, 연결 시간 분류)
: 시퀀스 데이터에서 정렬이 없거나 부분적으로만 알려진 학습데이터를 다루기 위한 기계학습 방법이다. 특히 음성 인식이나 필기인식 같은 분야에서 많이 사용된다. CTC는 입력데이터의 시간적 순서를 유지하면서, 출력 시퀀스의 길이가 입력 시뭔스와 다를 수 있는 상황을 효과적으로 처리할 수 있다.
 CTC는 전체 시퀀스를 고려하여 최적의 경로를 찾는 동적 프로그래밍 기법을 사용한다. 이는 각 시간 단계에서 발생할 수 있는 모든 가능한 라벨 시퀀스의 확률을 계산하고, 가장 높은 확률을 가진 시퀀스를 최종 츌력으로 선택한다. 이 과정은 시퀀스 길이가 다른 입력과 출력 사이의 정렬 문제를 효과적으로 해결한다. CTC는 특히 빠른 속도의 음성이나 필기체 텍스트에서 높은 인식 성능을 보여준다.


 이 모델은 이전 end-to-end 모델에 비해 훨씬 우수한 성능으로 강조되었습니다(그림 2 참조).

![Fig. 2. Architecture of LAS](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-04-30-kospeech/Fig.%202.%20Architecture%20of%20LAS.png?raw=true)


#### (b) Listen, Attend and Spell (LAS)
 이전에 Listen, Attend and Spell (LAS)에서 제안한 아키텍처를 기반으로 성능을 향상시키기 위해 일부 부분을 수정합니다. 저희는 scaled dot-product attention, additive attention, location aware attention, multi-head attention의 네 가지 attention 메커니즘을 제공합니다. attention 메커니즘은 모델의 성능에 많은 영향을 미칩니다(그림 3 참조)

![Fig. 3. Architecture of Transformer](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-04-30-kospeech/Fig.%203.%20Architecture%20of%20Transformer.png?raw=true)


#### (c) Transformer
 Transformer는 자연어 처리(NLP) 분야에서 강력한 아키텍처 중 하나입니다. 이 아키텍처는 또한 ASR 작업에서 우수한 성능을 보였습니다. 트랜스포머의 개선은 추가 연구를 위한 것입니다 (그림 4 참조).

![Fig. 4. Architecture of Joint CTC-Attention](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-04-30-kospeech/Fig.%204.%20Architecture%20of%20Joint%20CTC-Attention.png?raw=true)


#### (d) Joint CTC-Attention LAS
 이 모델은 (b)에서 설명한 LAS 아키텍처의 보완 버전입니다. CTC 기반 모델과 attention 기반 모델을 모두 사용하여 제안된 아키텍처는 naive CTC 및 attention 모델보다 더 나은 성능을 보였습니다.


### 2.3. Feature extraction
 KoSpeech를 통해 연구자들은 오디오 데이터에서 추출된 다음과 같은 네 가지 주요 특성 중에서 선택할 수 있습니다: Spectrogram, Mel-Spectrogram, Filter-bank, Mel Frequency Cepstral Coefficient (MFCC).
 연구자들은 윈도우 크기, stride 양, mel filter-bank의 수 등 특성 추출에 관련된 파라미터를 설정할 수 있습니다.

※ Spectrogram
: 소리나 파동을 시각화하여 파악하기 위한 도구로, 파형과 스펙트럼의 특징이 조합되어 있다.
![Spectrogram](https://sethares.engr.wisc.edu/banuelos/spectrogram.jpg)

※ Mel-Spectrogram
: 음성 신호를 처리하고 분석하는 데 사용되는 시각적 도구로서, 주파수 스펙트럼의 시간적 변화를 보여주는 이미지입니다. 기본적인 스펙트로그램은 시간에 따른 신호의 주파수와 강도를 표시하지만, 멜-스펙트로그램은 멜 척도를 사용하여 주파수를 인간의 청각 인지와 더 유사하게 매핑합니다. 멜 척도는 인간이 듣는 소리의 피치가 선형적이지 않고 로그 스케일에 가깝게 인지된다는 점을 반영한 것입니다.

※ Filter-bank
: 입력 신호를 여러 구성요소로 분리하는 대역 통과 필터 배열이다. 여러 개의 밴드 패스 필터로 구성되어 있으며, 각 필터는 특정 주파수 대역을 통과시키고 다른 주파수는 차단합니다. 이를 통해 신호를 다양한 주파수 대역으로 나누어 분석할 수 있습니다.
ex) mel filter-bank
: 인간의 귀가 소리의 높이를 인식하는 방식을 모방하여 설계된 필터 뱅크입니다. 저주파수에서는 더 많은 필터를 사용하고 고주파수로 갈수록 필터의 밀도를 낮춥니다.

※ Mel Frequency Cepstral Coefficient (MFCC)
: 음성 인식을 위하여 가장 먼저 해야할 것은 입력된 신호에서 노이즈 및 배경 소리로 부터 실제 유효한 소리의 특징을 추출하는 것이다. MFCC는 바로 소리의 특징을 추출하는 기법인데, 입력된 소리 전체를 대상으로 하는 것이 아니라, 일정 구간(Short time)식 나누어, 이 구간에 대한 스펙트럼을 분석하여 특징을 추출하는 기법이다.



## 3. Evaluation
 성능 메트릭으로 문자 오류율(Character Error Rate, CER)을 사용하였습니다

![cer](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-04-30-kospeech/cer.png?raw=true)

여기에서 X와 Y는 각각 예측된 스크립트와 실제 정답 스크립트를 의미합니다. D는 X와 Y 사이의 레벤슈타인 거리이며, L은 실제 정답 스크립트 Y의 길이입니다.
 여러 실험을 수행하고 KoSpeech를 기준 모델로 사용하여 결과를 벤치마크로 발표하였습니다.
기준 모델은 필터 뱅크 특성과 multi-head attention 메커니즘을 사용하여 10.31%의 CER을 달성하였습니다. 특성 벡터와 attention 메커니즘에 따른 비교 결과는 표 2와 코드 메타데이터에서 확인할 수 있습니다.

![Table 2](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-04-30-kospeech/Table%202.png?raw=true)



## 4. Impact overview
 KoSpeech는 실험을 위한 확장성을 제공하며 다양한 옵션을 통해 훈련 환경을 맞춤 설정할 수 있습니다. 모델 구조, 출력 단위, 특성 추출, 모델 크기 등을 사용자가 선택할 수 있습니다. 이는 한국어 작업을 처리하는 오픈 소스 ASR 프로젝트로, 단일 연구 목적이 아니라 사용자의 편의성과 확장성을 위한 것입니다.
 또한, KoSpeech는 처음으로 대규모 한국어 말뭉치인 KsponSpeech를 다룰 수 있는 도구입니다. 이 데이터셋은 지금까지 오픈 소스에서 다루지 않았습니다.
 KoSpeech는 또한 잘 정리된 문서를 제공합니다. 이 문서에는 도구의 설명과 KoSpeech의 다양한 옵션 설정 방법, 이 옵션들이 무엇을 하는지에 대한 정보가 포함되어 있습니다. 또한, 연구자를 위해 사전 처리된 전사본과 사전 훈련된 모델을 제공합니다. 데이터 전처리의 흐름에 대한 세부 사항도 설명되어 있습니다. 이러한 전처리 방법은 향후 출시될 다른 한국어 데이터셋에도 널리 적용될 수 있습니다.
 새롭고 혁신적인 기술, 예를 들어 SpecAugment의 개정 버전과 AdamP 최적화기 같은 것이 출시될 때마다 KoSpeech를 지속적으로 업데이트합니다. KsponSpeech 데이터셋을 처리하는 것 외에도, 영어나 중국어와 같은 비한국어 언어를 위한 다양한 레시피를 제공할 계획입니다. 이미 KoSpeech는 가장 잘 알려진 영어 말뭉치 중 하나인 LibriSpeech 레시피를 제공하고 있습니다.
 KoSpeech 코드는 가독성이 좋으며 한국어 음성 인식을 공부하는 초보자에게 유용할 수 있습니다. 또한, KoSpeech의 모든 기능은 최대한의 모듈성을 가지고 작성되어 있어 연구자들이 필요할 때 다른 작업이나 프로젝트에서 이 기능들을 쉽게 사용할 수 있습니다.
 이러한 가독성과 모듈성 덕분에 KoSpeech는 여러 오픈 소스 프로젝트에서 참조로 사용되고 있습니다. 또한, KoSpeech는 백 명 이상의 GitHub 사용자들로부터 관심을 받고 있으며, 이들과 활발히 피드백을 교환하고 있습니다.
 앞으로 KoSpeech의 개발이 연구 최전선에서 강력한 음성 인식 성능을 유지하는 데 기여하고, 안정적이고 확장 가능한 오픈 소스 도구를 제공하기를 기대합니다.


---