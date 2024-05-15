---
title: wsl을 이용하여 ubuntu 설치하기
---
나는 원래 있었던 ubuntu20.04를 삭제하고 ubuntu 22.04를 설치하고 싶기 때문에 기존에 있던 wsl과 ubuntu를 삭제한다.

# 0. 기존 wsl, ubuntu 삭제
## ubuntu 삭제
* 설정 -> 시스템 -> 저장소 -> 설치된 앱 -> ubuntu 검색 -> ubuntu 삭제
![deleteubuntu]()


## wsl 제거
* 검색 -> window 기능 켜기/끄기 -> Linux용 Window 하위시스템 체크박스 해제 -> 확인 -> 재부팅
![window기능]()

![forlinux]()


---------------------------------------------------------------------
기존에 wsl이 없었다면 이 단계부터 시작하면 된다.


# 1. wsl 설치
## window powershell 관리자 권한으로 실행
```
wsl --install
``` 
* username과 password 설정


## WSL버전의 기본값을 2로 변경
```
wsl --set-default-version 2
```

# 2. ubuntu 설치 확인

![installedubuntu]()
![ubuntucmd]() 


# 3. Ubuntu22.04 설치
## microsoft store에서 Ubuntu22.04 설치
![microsoft store]()

## Ubuntu22.04 실행
* username, password 설정

![ubuntu22.04]()


![]()
![]()
![]()
![]()



---