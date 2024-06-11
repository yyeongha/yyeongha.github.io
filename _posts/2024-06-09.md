---
title: AI-DX education 3조_알약 프로젝트 구상
categories: [Project] 
date: 2024-06-09
last_modified_at: 2024-06-12
---
1. 데이터 준비
이미지 수집 및 라벨링
data/images/ 폴더에 이미지 파일을 저장합니다.
LabelImg를 사용하여 이미지 파일을 라벨링하고, 라벨 파일을 data/labels/ 폴더에 저장합니다.

2. 데이터셋 구성
데이터셋 구성
data/dataset/ 폴더 안에 train/, val/, test/ 폴더를 생성하고 이미지를 적절히 분할하여 저장합니다.
각 이미지에 대응하는 라벨 파일도 동일한 폴더 구조로 저장합니다.

3. 모델 학습
ResNet 학습

notebooks/resnet_training.ipynb 노트북을 실행하여 ResNet 모델을 학습합니다.
학습이 완료되면 모델 가중치를 models/resnet/best.pt 파일로 저장합니다.
YOLOv8 학습

notebooks/yolov8_training.ipynb 노트북을 실행하여 YOLOv8 모델을 학습합니다.
학습이 완료되면 모델 가중치를 models/yolov8/best.pt 파일로 저장합니다.

4. 모델 검증 및 실험
모델 검증 및 실험
학습된 모델을 검증하고, 필요하면 추가적인 실험을 수행합니다.

5. 실시간 검출 및 인식
실시간 검출 및 인식
scripts/pill_detection.py 스크립트를 실행하여 실시간으로 알약을 검출하고 각인을 인식합니다.
이 스크립트는 학습된 YOLOv8과 ResNet 모델을 사용합니다.

6. 기타 유틸리티 및 설정
유틸리티 및 설정
scripts/clova_ocr.py 파일을 통해 Naver Clova OCR API를 설정합니다.
scripts/utils.py 파일을 통해 필요한 유틸리티 함수를 정의합니다.

7. 프로젝트 설정 및 설치
프로젝트 설정 및 설치
requirements.txt 파일을 사용하여 필요한 패키지를 설치합니다:
bash
코드 복사
pip install -r requirements.txt
LabelImg 설치 스크립트를 실행합니다:
bash
코드 복사
bash labelimg/labelimg_install.sh




































---