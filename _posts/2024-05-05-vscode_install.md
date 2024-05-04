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


## vscode IDE
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






















































---