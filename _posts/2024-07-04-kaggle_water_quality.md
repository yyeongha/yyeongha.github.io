---
title: kaggle_Water Quality 데이터를 이용하여 수질 예측 및 정확도 계산
categories: [kaggle] 
date: 2024-07-04
last_modified_at: 2024-07-04
---

# 1. 문제 정의 및 데이터 탐색

## 1) 문제 정의
* 목표 : 제공된 수질 관련 특징들을 기반으로 음용 가능 여부(Potable/Not potable)를 분류하는 모델 개발
* 데이터 : 'water_potability.csv' 파일 사용
* 특징: pH, 경도, 고형물(TDS), 클로라민, 황산염, 전도도, 유기 탄소, 트리할로메탄, 탁도
* 타겟 변수: Potability (1: 음용 가능, 0: 음용 불가)
* 데이터 탐색 결과:
    * 특징 데이터 타입: 대부분 float64 (실수형), Potability는 int64 (정수형)
    * 결측값: ph, Sulfate, Trihalomethanes 열에 존재
    * 불균형: Potability 값이 0인 데이터가 더 많음
    * 통계 분석: Potability 값에 따른 각 특징의 평균 및 표준편차 비교
    * 이상치: 다수 존재

![waterQuality]()
![waterQuality_exel]()

## 2) 특징 세부 정보
(1) pH value:
* pH는 물의 산-염기 균형을 평가하는 중요한 매개변수이다. 또한 물 상태의 산성 또는 알칼리성 상태를 나타내는 지표이다.
* WHO는 6.5에서 8.5 사이의 최대 허용 pH 한도를 권장한다.
* 현재 조사 범위는 6.52-6.83이며 WHO 표준 범위 내에 있다.

(2) 경도 (Hardness):
* 경도는 주로 칼슘 및 마그네슘 염에 의해 발생한다. 이러한 염은 물이 통과하는 지질 퇴적물에서 용해된다.
* 물이 경도 생성 물질과 접촉하는 시간이 길수록 원수의 경도가 높아진다.
* 경도는 원래 칼슘 및 마그네슘에 의한 물의 비누 침전 능력으로 정의되었다.

(3) 고형물 (Solids, 총 용존 고형물 - TDS):
* 물에는 칼륨, 칼슘, 나트륨, 중탄산염, 염화물, 마그네슘, 황산염 등과 같은 다양한 무기 및 일부 유기 미네랄 또는 염을 용해시키는 능력이 있다.
* 이러한 미네랄은 원치 않는 맛을 내고 물의 외관에 희석된 색을 생성한다. 이는 물 사용에 중요한 매개변수이다.
* 높은 TDS 값은 물이 고도로 미네랄화되어 있음을 나타낸다.
* 음용 목적으로 TDS의 바람직한 한도는 500mg/L이며 최대 한도는 1000mg/L이다.

(4) 클로라민 (Chloramines):
* 염소 및 클로라민은 공공 상수도 시스템에서 사용되는 주요 소독제이다.
* 클로라민은 암모니아가 염소에 첨가되어 식수를 처리할 때 가장 일반적으로 형성된다.
* 염소 수준은 최대 4mg/L (또는 4ppm)까지 식수에서 안전한 것으로 간주된다.

(5) 황산염 (Sulfate):
* 황산염은 미네랄, 토양 및 암석에서 발견되는 자연 발생 물질이다. 주변 공기, 지하수, 식물 및 식품에도 존재한다.
* 황산염의 주요 상업적 용도는 화학 산업이다.
* 해수의 황산염 농도는 약 2,700mg/L
* 대부분의 담수 공급원에서는 3 ~ 30mg/L이지만 일부 지역에서는 훨씬 더 높은 농도(1000mg/L)가 발견됨

(6) 전도도 (Conductivity):
* 순수는 전류를 잘 전도하지 않으며 오히려 좋은 절연체이다.
* 이온 농도 증가는 물의 전기 전도도를 향상시킨다.
* 일반적으로 물에 용해된 고형물의 양이 전기 전도도를 결정한다.
* 전기 전도도(EC)는 용액이 전류를 전달할 수 있도록 하는 이온 과정을 측정한다.
* WHO 표준에 따르면 EC 값은 400μS/cm를 초과해서는 안된다.

(7) 유기 탄소 (Organic_carbon):
* 원수의 총 유기 탄소(TOC)는 부패하는 자연 유기 물질(NOM) 및 합성 소스에서 비롯된다.
* TOC는 순수한 물에서 유기 화합물의 총 탄소량을 측정한다.
* 미국 EPA에 따르면 처리/음용수의 TOC는 2mg/L 미만, 처리에 사용되는 원수의 TOC는 4mg/L 미만이다.

(8) 트리할로메탄 (Trihalomethanes):
* THMs는 염소로 처리된 물에서 발견될 수 있는 화학 물질이다.
* 식수에서 THMs의 농도는 물 속 유기 물질 수준, 물 처리에 필요한 염소량 및 처리되는 물의 온도에 따라 다르다.
* THM 수준은 최대 80ppm까지 식수에서 안전한 것으로 간주된다.

(9) 탁도 (Turbidity):
* 물의 탁도는 부유 상태에 있는 고형물의 양에 따라 달라진다.
* 빛 방출 특성을 측정하며, 콜로이드 물질과 관련하여 폐기물 배출 품질을 나타내는 데 사용된다.
* Wondo Genet Campus에서 얻은 평균 탁도 값(0.98 NTU)은 WHO 권장 값인 5.00 NTU보다 낮다.

(10) 음용 가능성 (Potability):
* 물이 인간이 섭취하기에 안전한지 여부를 나타넨다.
* 1은 음용 가능(Potable)을 의미
* 0은 음용 불가(Not potable)를 의미


# 2. 데이터 전처리
* 데이터 타입 변환: Potability를 category 타입으로 변환
```
df.info()
```
![dfinfo]()
위 정보를 보면 목표 특징을 제외하고 다른 특징들은 float(실수)이며 연속적인 값을 가진다. Potability 특징은 범주형 특징으로 변환할 수 있다.
```
df['Potability']=df['Potability'].astype('category')
```

* 결측값 처리: Potability 값에 따른 각 특징의 평균값으로 대체
```
df.isnull().sum()
```
![isnullsum]()
위 결과를 보면 ph, Sulfate 및 Trihalomethanes에 null 값이 있다. 이 값들을 자세히 확인하고 처리하는 과정을 다음과 같이 나타낸다.

```
df[df['Sulfate'].isnull()]
df[df['ph'].isnull()]
df[df['Trihalomethanes'].isnull()]
```
![isnull]()
위 데이터프레임을 보면 결측값이 두 클래스(Potability 1 & 0) 모두에 존재하므로, 전체 모집단 평균으로 대체할 수 있다. 따라서, 각 클래스의 표본 평균을 기반으로 NaN 값을 대체한다.

```
#Replace null values based on the group/sample mean

# Potability 그룹별로 ph 열의 평균을 계산하고, 결측값(NaN)을 해당 그룹의 평균 값으로 채움
df['ph']=df['ph'].fillna(df.groupby(['Potability'])['ph'].transform('mean'))

# Potability 그룹별로 Sulfate 열의 평균을 계산하고, 결측값(NaN)을 해당 그룹의 평균 값으로 채움
df['Sulfate']=df['Sulfate'].fillna(df.groupby(['Potability'])['Sulfate'].transform('mean'))

# Potability 그룹별로 Trihalomethanes 열의 평균을 계산하고, 결측값(NaN)을 해당 그룹의 평균 값으로 채움
df['Trihalomethanes']=df['Trihalomethanes'].fillna(df.groupby(['Potability'])['Trihalomethanes'].transform('mean'))
```
```
df.isna().sum()
```
![isnull2]()


# 3. 탐색적 데이터 분석 (EDA)
* 시각화:
    * Potability 값 분포: 목표변수에 불균형이 존재한다. 이는 모델링 시 고려해야한다.
    ![patabilityFeature]()
    * 특징 분포: Potability 값에 따른 각 특징의 분포 비교, 승인 기준과의 비교
    * 상관관계 분석: 특징 간의 상관관계 확인 (선형 모델 적합성 판단)
    * PCA: 주성분 분석을 통한 차원 축소 효과 확인 (차원 축소 효과 미미)
* 통계 분석:
    * t-검정: Potability 값에 따른 각 특징의 평균 차이 유의성 검정 (Solids, Organic_carbon 특징에서 유의미한 차이 발견)












































---