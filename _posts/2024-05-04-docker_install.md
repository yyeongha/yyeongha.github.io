---
title: docker 설치 (window)
---
# docker 설치하는 법
## WSL 설치 가능 여부 확인
### 1. 윈도우 검색창에서 PC 정보 실행

![1.pcInformation](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-04-docker_install/1.pcInformation.png?raw=true)


### 2. window 사양에서 버전이 20H1, 20H2, 21H1 혹은 그보다 높은 버전인지 확인한다.

* 만약 이 버전들보다 낮다면, 윈도우 업그레이드한 후 설치해야 한다.

## WSL2를 설치하고 활성화하는 방법
### 1. 윈도우 검색창에서 powershell 관리자로 실행

### 2. wsl 설치
```
wsl --install
```

![wslinstall](https://github.com/good593/google_lecture/raw/15cc6e3e7aecd6d5975c07f8a966154f882db132/08.spark/docker/img/install/image-2.png)


### wsl 버전의 기본값을 2로 변경
```
wsl --set-default-version 2
```
![3.wlsversion](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-04-docker_install/3.wlsversion.png?raw=true)


## docker desktop 다운로드
### 1. docker 다운로드
https://www.docker.com/products/docker-desktop/

![dockerdesktopdown](https://github.com/good593/google_lecture/raw/15cc6e3e7aecd6d5975c07f8a966154f882db132/08.spark/docker/img/install/image-6.png)

### 2. 설치 파일 실행 후 예 클릭

![yes](https://github.com/good593/google_lecture/raw/15cc6e3e7aecd6d5975c07f8a966154f882db132/08.spark/docker/img/install/image-8.png)


### 3. ok 클릭

![ok](https://github.com/good593/google_lecture/raw/15cc6e3e7aecd6d5975c07f8a966154f882db132/08.spark/docker/img/install/image-9.png)


### 4. 설치가 완료되면 close and restart 클릭

![close and restart](https://github.com/good593/google_lecture/raw/15cc6e3e7aecd6d5975c07f8a966154f882db132/08.spark/docker/img/install/image-7.png)

### 5. docker desktop 실행한 후 

* 설정 -> General -> Use the WSL 2 based engine 체크

![6. check](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-04-docker_install/6.%20check.png?raw=true)

### 6. 설정에서 WSL2 통합 기능이 활성화 되어있는지 확인
* 설정 -> Resources -> Enable integration with my default WSL distro

![7.check](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-04-docker_install/7.check.png?raw=true)


## 설치가 잘 되었는지 확인
### 1. powershell 탭을 열고 wsl 명령어로 docker 전용 머신이 실행 중인 것을 확인 가능

```
wsl -l -v
```

![wsl -l -v](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-04-docker_install/check.png?raw=true)

### 2. wsl로 docker-desktop 리눅스에 명령어를 실행 가능

```
wsl -d docker-desktop busybox
```
![wsl -d docker-desktop busybox](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-04-docker_install/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202024-05-04%20204254.png?raw=true)


### 3. docker version 명령으로 Docker 서버와 클라이언트 정보를 확인

```
docker --version
```

![docker --version](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-05-04-docker_install/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202024-05-04%20204310.png?raw=true)













---