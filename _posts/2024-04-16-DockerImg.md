---
title: 도커 이미지 예제
---
## 단계1. hello.js 확인
![CheckHellojs](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-16-DockerImg/CheckHellojs.png?raw=true)

```js
const http = require('http');
const os = require('os');
console.log("Test server starting...");

const handler = function(req, res) {
  console.log("Received request from "+req.connection.remoteAddress);
  res.writeHead(200);
  res.end("Container Hostname: "+os.hostname()+"\n");
};

let www = http.createServer(handler);
www.listen(8080);

```

## 단계2. Dockerfile 확인
![CheckDockerfile](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-16-DockerImg/CheckDockerfile.png?raw=true)

## 단계3. Dockerfile과 hello.js이 있는 폴더로 이동
터미널을 열고 Dockerfile, hello.js 파일 확인
```
ls
```

## 단계4. Dockerfile을 이용하여 hellojs 이미지 생성
* docker build -t <이미지명>:<태그> <기준이 되는 폴더 위치>

```
docker build -t hellojs:latest
``` 

## 단계5. 생성된 hellojs 이미지 확인
```
docker image ls
```

![CheckHellojsImage](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-16-DockerImg/CheckHellojsImage.png?raw=true)

## 단계6. hellojs-web 컨테이너 생성
* 태그가 latest인 경우 생략 가능

```
docker run --name hellojs-web -d -p 8080:8080 hellojs
```

![GenerateHellojsContainer](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-16-DockerImg/GenerateHellojsContainer.png?raw=true)


## 단계7. 작동중인 hellojs-web 컨테이너 확인
```
docker ps
```

![](https://github.com/good593/course_dev_basic/raw/main/docker/samples/2.%20%EB%8F%84%EC%BB%A4%20%EC%9D%B4%EB%AF%B8%EC%A7%80%20%EC%98%88%EC%A0%9C/img/image-7.png)


## 단계8. hellojs-web에 접속
* http://localhost:8080/
![AccessHellojs](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-16-DockerImg/AccessHellojs.png?raw=true)


## 단계9. 실행중인 컨테이너 삭제
```
docker rm -f hellojs-web
docker ps -a
```

![RemoveContainer](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-16-DockerImg/RemoveContainer.png?raw=true)


## 단계10. 도커허브 -> repositories -> 아이디 확인
* 도커허브 :  https://hub.docker.com/

![]()



---