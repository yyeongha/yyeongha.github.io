---
title: Ubuntu22.04 딥러닝 학습 서버 환경 구축 (cuda, cudnn 설치)
---
* gpu : nvidia GeForce RTX 3060
* Ubuntu 22.04

cuda driver 510.108.03, 528.79, 531.41, 536

python 3.10.11

cuda 툴킷 11.8, 11.5, 11.7

cudnn 8.9.6, 8.5.1, 8.8.1

compute capability 8.6인 경우 
CUDA 11.1부터 최신 버전인 12.4까지 사용할 수 있음

0. driver 설치
https://www.nvidia.com/Download/index.aspx


1. turm window feature

virtual machine platform 
window subsystem for linux 
체크 ->  reboot

2. setting defualt wsl version to wsl2
* command prompt
```
wsl --set-default-version 2

wsl --list --online

wsl --install -d Ubuntu
```

* ubuntu
```
username
password

cd /mnt/c

dir

exit
```

3. how to install nvidia cuda for wsl2
* command prompt
```
wsl --list --verbose

wsl -t Ubuntu

wsl --list --verbose

wsl --distribution Ubuntu

exit
```

* ubuntu
```
gcc --version

sudo apt install gcc --fix-missing
```

* cuda toolkit, linux ->  x86_64 -> wsl-ubuntu -> 2.0 -> deb(local)
```
wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-wsl-ubuntu.pin
sudo mv cuda-wsl-ubuntu.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/11.7.0/local_installers/cuda-repo-wsl-ubuntu-11-7-local_11.7.0-1_amd64.deb
sudo dpkg -i cuda-repo-wsl-ubuntu-11-7-local_11.7.0-1_amd64.deb
sudo cp /var/cuda-repo-wsl-ubuntu-11-7-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda
```

4. how to set path variable for nvidia cuda on linux
```
cd ~

nano .bashrc

export PATH=/usr/local/cuda-11.8/bin${PATH:+:${PATH}}

source ~/.bashrc

echo $PATH


sudo apt install nvidia-cuda-toolkit

nvcc -V

nvidia-smi
```
```
sudo apt-get install python3-pip
```

* pytorch : stable -> linux -> pip -> python -> cuda11.8
https://pytorch.org/get-started/locally/
```
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
python3
import torch
torch.cuda.is_available()
torch.__version__
```

5. compliling cuda program to see if cuda works
```
cd ~
nano test.cu
nvcc test.cu -o test
./test
nvprof ./test
```

6. fix nvidia profiler error
* nvidia control panel
desktop -> enable developer settings
developer -> manage gpu -> allow access 

* ubuntu 
```
nvprof ./test

```













---