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

![SwapDisabled2](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-19-kubernetes/SwapDisabled2.png?raw=true)

![SwapDisabled1](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-19-kubernetes/SwapDisabled1.png?raw=true)


## 단계3. 재부팅 및 재접속
```
reboot
```

![reboot](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-19-kubernetes/Reboot.png?raw=true)


## 단계4. IPv4를 포워딩하여 iptables가 브리지된 트래픽을 보게 하기
```
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
overlay
br_netfilter
EOF

su -

sudo modprobe overlay 
```
![IPv41](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-19-kubernetes/IPv41.png?raw=true)

```
sudo modprobe br_netfilter 

cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables  = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward                 = 1
EOF

# 재부팅하지 않고 sysctl 파라미터 적용
sudo sysctl --system
```
![IPv42](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-19-kubernetes/IPv42.png?raw=true)


## 단계5. containerd
* containerd는 kubernetes의 하이 레벨 런타임 표준인 CRI(container runtime interface)런타임이다.

```
sudo apt-get install -y containerd
sudo systemctl status containerd.service
```

![containerd1](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-19-kubernetes/containerd1.png?raw=true)
![containerd2](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-19-kubernetes/containerd2.png?raw=true)


* SystemCgroup = true
```
sudo mkdir -p /etc/containerd
containerd config default | sudo tee /etc/containerd/config.toml
```

![containerd3](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-19-kubernetes/containerd3.png?raw=true)

```
sudo vim /etc/containerd/config.toml

# 아래 내용으로 수정
SystemdCgroup = true
```

![containerd4](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-19-kubernetes/containerd4.png?raw=true)

![containerd5](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-19-kubernetes/containerd5.png?raw=true)


* restart containerd
```
sudo systemctl restart containerd.service
sudo systemctl status containerd.service
```

![containerd6](https://github.com/yyeongha/yyeongha.github.io/blob/main/assets/img/favicons/2024-4-19-kubernetes/containerd6.png?raw=true)


## 단계6. kubeadm, kub;elet and kubectl 설치
* apt-transport-https : 패키지 관리자가 https를 통해 데이터 및 패키지에 접근할 수 있도록 한다. 
* ca-certificates : ca-certificate는 certificate authority에서 발행되는 디지털 서명, SSL 인증서의 PEM파일이 포함되어 있어 SSL 기반 앱이 SSL 연결이 되어있는지 확인할 수 있다.
* curl : 특정 웹사이트에서 데이터를 다운로드 받을 때 사용

* Update the apt package index and install packages needed to use the apt repository

```
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl
```

![]()














---