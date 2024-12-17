---
title : 파이썬 Geopandas 설치하는 방법
categories: [Python] 
date: 2024-12-16
last_modified_at: 2024-12-16
---
## Geopandas란?
GeoPandas는 Python의 데이터 분석 라이브러리인 Pandas를 확장하여 지리공간 데이터를 쉽게 다룰 수 있게 해주는 라이브러리이다. 지도 데이터나 위치 정보를 분석하고 시각화하는 데 특화되어 있다.

## Geopandas 설치 가이드
### 설치 과정에서 겪었던 문제들
GeoPandas를 설치하면서 저는 꽤 많은 시행착오를 겪었다. 처음에는 여러 블로그를 참고해서 설치를 시도했는데, 그렇게 하면 설치는 되는 것 같은데 geopandas를 import 하면 자꾸 오류가 발생했다.

### 시도했던 방법들
1. pip install geopandas - 기본적인 pip 설치
2. pipwin을 사용한 설치 - 일부 블로그에서 추천하는 방법
3. .whl 파일을 직접 다운로드해서 설치 - 일부 블로그에서 추천하는 방법

### 해결 방법: 공식 문서가 답이다~
결국 해답은 가장 기본적인 곳에 있었다. 바로 GeoPandas 공식 문서! 여러 블로그를 전전하다가 공식 문서를 확인했더니, 설치 방법이 매우 명확하게 안내되어 있었다.
공식 문서에서는 conda를 통한 설치를 주로 권장하고 있지만, 나는 pip로 설치하겠다.

### 1. 종속성 설치
```
pip install numpy
pip install pandas
pip install shapely
pip install pyogrio
pip install pyproj
pip install packaging
```
공식문서에서는 모든 종속성을 설치할 수 있는 경우 pip로 설치가능하다고 나와있다.
공식문서에서 말하는 종속성은 

![Dependencies](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-12-16-install_geopandas/Dependencies.png?raw=true)

해당 종속성들이 있다. 그 중 필수 종속성에 대해서만 설치를 해준다.

### 2. Geopandas 설치
```
pip install geopandas
```

### 3. Geopandas 임포트해서 잘 설치되었는지 확인
```
import geopandas as gpd
```
임포트 코드를 실행하고 모듈이 없다는 오류가 안뜨면 성공이다!


출처: [GeoPandas 설치 공식문서](https://geopandas.org/en/stable/getting_started/install.html)

---
