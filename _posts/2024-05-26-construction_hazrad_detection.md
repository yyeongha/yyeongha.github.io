---
title: 건설 현장 위험 감지 프로젝트
date: 2024-05-26
last_modified_at: 2024-05-26
---

# 깃 설치
```
sudo apt-get update
sudo apt-get install git
```

# 아나콘다 설치 
```
wget https://repo.anaconda.com/archive/Anaconda3-2024.02-1-Linux-x86_64.sh
```
![installconda]()

```
bash Anaconda3-2024.02-1-Linux-x86_64.sh
```
![bash]()
- yes/no 나오면 yes
- more 나오면 enter 계속 누르기
- Enter/Ctrl C 나오면 enter

* 설치 이후 conda --version을 누르면 coynda 명령어를 사용할 수 없다고 나옴. 터미널을 껐다가 재실행하면 작동됨

![condaver]()


# 가상환경 생성
```
conda create -n p310_construction python=3.10
conda env list
```

![envlist2]()


# 필요한 라이브러리 설치
```
pip3 install opencv-python==4.7.0.72 \
opencv-python-headless==4.7.0.72 \
Pillow==10.3.0 \
torch==2.3.0 \
torchvision==0.18.0 \
ultralytics==8.2.21 \
imageio==2.34.1 \
imgaug==0.4.0 \
numpy==1.26.4 \
python-dotenv==1.0.1 \
sahi==0.11.16 \
pycocotools==2.0.7 \
onnx==1.16.1 \
gunicorn==22.0.0 \
imagecorruptions==1.1.2 \
Flask-JWT-Extended==4.6.0 \
Flask-Limiter==3.7.0 \
Flask-SQLAlchemy==3.1.1 \
redis==5.0.4 \
apscheduler==3.10.4 \
speedtest-cli==2.1.3 \
streamlink==6.7.4 \
tenacity==8.3.0 \
Flask==3.0.3 \
Flask-SocketIO==5.3.6 \
Flask-Cors==4.0.1 \
eventlet==0.36.1

```


























---