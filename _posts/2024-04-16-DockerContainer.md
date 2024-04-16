---
title: \[Docker\] Container 예제 (nginx)
---
## 단계1. 도커 이미지 조회

이미지가 없다는 것을 확인한다.

```
docker images
```

![image](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-16-docker/DockerImagesEmpty.png?raw=true)


## 단계2. Docker Hub -> nginx 이미지 조회
* docker Search <이미지 이름>

```
docker search nginix
```

![searcgnginx](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-16-docker/SearchNginx.png?raw=true)


## 단계3. Docker Hub -> nginx 이미지 다운로드
* docker pull nginx

```
docker pull nginx
```

![pull](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-16-docker/PullNginx.png?raw=true)


## 단계4. 도커 이미지 조회 -> nginx 이미지 확인

```
docker images
```

![DockerImagesNginx](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-16-docker/DockerImagesNginx.png?raw=true)


## 단계5. nginx 이미지 -> 컨테이너 생성
* docker run --name <컨테이너 이름> -d -p 80:80 <이미지 이름>
  * -d : 백그라운드 모드로 실행
  * -p : 포트 연결

```
docker run --name web-server -d -p 80:80 nginx
```

![RunNginx](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-16-docker/RunNginx.png?raw=true)


## 단계6. 실행 중인 컨테이너 -> nginx 컨테이너 확인

```
docker ps
```

![docker ps](https://github.com/good593/course_dev_basic/raw/main/docker/samples/1.%20%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88%20%EC%98%88%EC%A0%9C/img/image-7.png)

## 단계7. nginx 서버 접속
* http://localhost:80/

![localhost80](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-16-docker/localhost80.png?raw=true)

## 단계8. nginx 컨테이너 중지
* docker stop <컨테이너 이름>

```
docker stop web
docker ps
```

![StopWeb](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-16-docker/StopWeb.png?raw=true)


## 단계9. nginx 서버 접속 불가
* http://localhost:80/

![]()










---