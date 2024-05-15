---
title: vscode 설치
---

# 개발 환경 구축
## 1. powershell 실행 권한 추가
### 1. 윈도우 Powershell을 관리자 권한으로 실행

### 2. 권한 확인

```
get-ExecutionPolicy
```
'Restricted' 상태일 가능성이 높음

### 3. PowerShell 스크립트의 실행 정책을 RemoteSigned로 설정
```
Set-ExecutionPolicy RemoteSigned
```

### 4. Y를 입력하여 실행 정책을 변경

### 5. 권한 확인
```
get-ExecutionPolicy
```

RemoteSigned 상태로 변경되어 있어야 한다.

![powershell](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-04-python_install/powershell.png?raw=true)


## 2. vscode IDE
### 1. vscode 설치

https://code.visualstudio.com/download


### extension 설치

git graph
indent-rainbow
jupyter
material icon theme
prettier - code formatter
pylance
python

+
auto close tag
auto rename tag
code snap
css peek
html css support
live server
postman

![auto](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-05-vscode_install/auto.png?raw=true)
![git graph](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-05-vscode_install/git%20graph.png?raw=true)
![htmlcss](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-05-vscode_install/htmlcss.png?raw=true)
![indent](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-05-vscode_install/indent.png?raw=true)
![jupyter](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-05-vscode_install/jupyter.png?raw=true)
![liveserver](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-05-vscode_install/liveserver.png?raw=true)
![postman](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-05-vscode_install/postman.png?raw=true)
![py](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-05-vscode_install/py.png?raw=true)
![spring](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-05-vscode_install/spring.png?raw=true)


## 3. 개발 폰트 설치
### D2 Coding 글꼴 다운로드

* 맨 밑 D2Coding-Ver1.3.2 들어가기

https://github.com/naver/d2codingfont

![d2codingfont](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-05-vscode_install/d2codingfont.png?raw=true)

* 다운로드

![d2codingfont2](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-05-vscode_install/d2codingfont2.png?raw=true)

* vscode에 글꼴 적용
file -> preference -> settings

![d2codingfont5](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-05-vscode_install/d2codingfont5.png?raw=true)

* font 검색 -> Font Family에 D2Coding ligature 넣기
```
D2Coding ligature
```

![d2codingfont6](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-05-vscode_install/d2codingfont6.png?raw=true)

* Font Ligatures에서 Edit in settings.json 클릭

![d2codingfont7](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-05-vscode_install/d2codingfont7.png?raw=true)

* settings.json에서 editer.fontfamily, editer.fontLigatures 확인
![d2codingfont9](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-05-vscode_install/d2codingfont9.png?raw=true)




















































---