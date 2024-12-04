---
title : Semi-Automatic Classification Plugin 설치 방법 (Remotior Sensus 에러 해결 방법)
categories: [QGIS] 
date: 2024-12-02
last_modified_at: 2024-12-02
---
## 1. QGIS에서 Semi-Automatic Classification Plugin 설치

* 플러그인 -> 플러그인 관리 및 설치
![qgis_plugin](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-12-02-QGIS/qgis_plugin.png?raw=true)

* 모두 -> Semi-Automatic Classification 검색 -> 플러그인 설치
![qgis_install](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-12-02-QGIS/qgis_install.png?raw=true)

여기까지한다면 QGIS 상단에 노란색 박스로

Semi-Automatic Classification Plugin: Warning. Python library Remotior Sensus is outdated.This could cause errors, please update Remotior Sensus. 

이런 경고창이 뜨면서 scp 플러그인을 찾을 수 없다....


## 2. Remotior Sensus 에러 해결 방법
Semi-Automatic Classification Plugin: Warning. Python library Remotior Sensus is outdated.This could cause errors, please update Remotior Sensus.

해당 에러는 Semi-Automatic Classification Plugin에서 발생한 경고로, Remotior Sensus라는 Python 라이브러리가 구버전이어서 오류가 발생할 가능성이 있다는 내용이다.

나는 해당 에러를 해결하려고 구글링을 열심히 해봤지만... 이 에러를 해결한 블로그의 최신 글이 23년도라서 그 글의 해결방법대로 따라했으나 해결되지 못하였다.

그래서 더 구글링해본 결과...공식문서 발견!!!
공식문서는 참 따뜻하고 친절하구나.. 프로그램마다 불친절하게 작성해놓은 문서도 있어서 잘 참고는 안했는데 앞으로는 공식문서부터 보는 습관을 기르도록 하자!!
![qgis_manual](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-12-02-QGIS/qgis_manual.png?raw=true)

그래서 해결방법은

### 2.1. 필수 종속성 설치
Semi-Automatic Classification Plugin은 대부분의 기능에 Remotior Sensus, GDAL, NumPy 및 SciPy가 필요하다. 특히 머신 러닝에는 scikit-learn와 PyTorch가 필요하다고 한다.

따라서 QGIS 설치에 포함되지 않은 종속성을 설치해야한다.

* QGIS를 닫는다
* OSGeo4W Shell을 관리자 권한으로 연다 
![qgisshell](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-12-02-QGIS/qgisshell.png?raw=true)
* 다음 명령어를 입력
```python
pip3 install --upgrade remotior-sensus
```
* 또는 머신러닝기능이 필요할 경우 해당 명령어를 입력
```python
pip3 install --upgrade remotior-sensus scikit-learn torch
```

그리고 QGIS를 열어보면
![qgis_scpyab](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-12-02-QGIS/qgis_scpyab.png?raw=true)
이렇게 SCP 탭이 생긴것을 볼 수 있다!



출처: [Semi-Automatic Classification Plugin manual](https://semiautomaticclassificationmanual.readthedocs.io/pt/latest/installation_win64.html)

---
