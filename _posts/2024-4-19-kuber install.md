---
title: 2. kubernetes 설치 및 설정
---
## 단계1. root 계정으로 변경
* root 계정의 비번 정의
```
sudo passwd root
```
![]()

* root 계정으로 접속
```
su -
```

![]()


## 단계2. swap disabled
* Swap 메모리는 하드디스크의 일부를 RAM처럼 사용하도록 만들어진 메모리이다.

```
sudo swapoff -a
sudo vim /etc/fstab
``` 

![]()

---