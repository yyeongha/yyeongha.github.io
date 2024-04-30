---
title: 1. master 인스턴스 생성
---
## 인스턴스 최소 스펙
* CPU: 2 core
* RAM: 2 GiB
* Storage: 30 GB
![InterfaceSpec](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-19-kubernetes/InterfaceSpec.png?raw=true)


## 단계1. master 생성 & 어댑터에 브리지
![GenerateMaster](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-19-kubernetes/GenerateMaster.png?raw=true)

## 단계2. update & install
```
sudo apt-get -y update && \
sudo apt-get -y upgrade && \
sudo apt-get -y dist-upgrade && \
sudo apt-get install -y vim wget unzip ssh openssh-* net-tools chrony
```

![Update&Install](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-19-kubernetes/Update&Install.png?raw=true)


## 단계3. ssh start
* xshell과 연결하기 위해 실행
```
sudo service ssh start
sudo sytmctl status sshd
```
![ssh start](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-19-kubernetes/ssgstart.png?raw=true)


## 단계4.chrony
* chorny는 NTP(network time protocol) 구현이다.

```
sudo vim /etc/chrony/chrony.conf

# 아래내용 수정 
#pool ntp.ubuntu.com        iburst maxsources 4
#pool 0.ubuntu.pool.ntp.org iburst maxsources 1
#pool 1.ubuntu.pool.ntp.org iburst maxsources 1
#pool 2.ubuntu.pool.ntp.org iburst maxsources 2
server 203.248.240.140 iburst maxsources 2
```

![chrony1](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-19-kubernetes/chrony1.png?raw=true)

![chrony2](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-19-kubernetes/chrony2.png?raw=true)


* 재실행
```
sudo systemctl restart chrony
sudo systemctl status chrony
chronyc sources
```

![restart1](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-19-kubernetes/restart1.png?raw=true)

![restart2](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-19-kubernetes/restart2.png?raw=true)


## 단계5. timezone
```
sudo timedatectl set-timezone Asia/Seoul
date
```

![timezone](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-19-kubernetes/timezone.png?raw=true)


## 단계6. hostname
```
sudo hostnamectl set-hostname master
hostname
```
![]()


## 단계7. master ip 확인
```
ifconfig
```

![Checkmasterip](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-19-kubernetes/Checkmasterip.png?raw=true)


## 단계8. xshell의 세션 생성
* 이름: master
* 호스트: master ip (ifconfig해서 나온 inet 입력)
* 로그인할 아이디: ubuntu
* 로그인할 비번: ubuntu

![]()

---