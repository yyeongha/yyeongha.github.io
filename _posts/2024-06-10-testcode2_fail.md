---
title: AI-DX education 3조_알약 프로젝트 실패기록 (test_code2)
categories: [Project] 
date: 2024-06-10
last_modified_at: 2024-06-10
---
# 1. data
## 1) data 폴더 구조
📦test_code2
 ┣ 📂data
 ┃ ┣ 📂images # 원본 이미지 
 ┃ ┣ 📂labels # 원본 라벨
 ┃ ┣ 📂dataset
 ┃ ┃ ┣ 📂test
 ┃ ┃ ┃ ┣ 📂images
 ┃ ┃ ┃ ┗ 📂labels
 ┃ ┃ ┣ 📂train
 ┃ ┃ ┃ ┣ 📂images
 ┃ ┃ ┃ ┗ 📂labels
 ┃ ┃ ┗ 📂valid
 ┃ ┃ ┃ ┣ 📂images
 ┃ ┃ ┃ ┗ 📂labels
 ┃ ┗ 📂database
 ┃ ┃ ┗ 📜pills_info.csv


## 2) 데이터 수집 방법
### (1) aihub
* 경구약제 이미지 데이터
https://www.aihub.or.kr/aihubdata/data/view.do?currMenu=&topMenu=&aihubDataSe=data&dataSetSn=576

* 166.약품식별 - 01.데이터 - 원천데이터 - 단일경구약제5000종 - TS_51단일.zip 다운

* TS_51단일.zip 을 까서 프로젝트에 필요한 약만 남기고 삭제
![TL_51]()
-> D:\3조_의약품\dataset\data_test2\원천_단일 경구약제 이미지 데이터_51_59\01.데이터\1.Training\원천데이터\단일경구약제 5000종\TS_51_단일 \
이 경로에 있음

* TS_51_단일 파일에서 각 약당 한개의 사진만 있는 폴더를 만듦 (원천_jpg_51)
-> D:\3조_의약품\dataset\data_test2\원천_jpg_51 \
이 경로에 있음

-> 이 폴더를 만든 이유는 roboflow에서 라벨링 작업을 할건데 각 약 폴더에 조명, 회전이 다른 약들이 있기 때문에 조명, 회전이 디폴트값인 약 사진 하나씩만 폴더에 넣었다.

?강사님에게 물어볼 질문? 
-> 모델을 학습시키려면 이미지와 라벨 데이터가 있어야 하는데, 우리 팀이 가지고 있는 이미지 데이터는 약 하나당 조명과 회전이 각각 다른 사진이 대략 20장씩 있다. 시간상 각 이미지를 라벨링을 못할 것 같은데, 각 약당 대표 이미지를 뽑아서 그것만 라벨링을 한 후 데이터 증강을 해서 모델을 학습시켜도 되는지? 

### (2) roboflow
* roboflow에서 이미지 데이터 자동 라벨링 후 데이터 증강
![roboflow]()


## 2) dataset
* roboflow에서 만든 데이터셋(train, valid, test)을 dataset폴더에 저장


## 3) database
### (1) aihub
* 166.약품식별 - 01.데이터 - 라벨링데이터 - 단일경구약제5000종 - TS_51단일.zip

* TS_51단일.zip 을 까서 프로젝트에 필요한 약만 남기고 삭제
![TL_51]()
-> D:\3조_의약품\dataset\data_test2\라벨링_단일_경구약제 이미지 데이터_51\01.데이터\1.Training\라벨링데이터\단일경구약제 5000종\TL_51_단일 \
이 경로에 있음

* TS_51단일.zip 을 까서 프로젝트에 필요한 약만 남기고 삭제
-> D:\3조_의약품\dataset\data_test2\라벨링_json_51
이 경로에 있음

* 위의 파일(json)들을 csv 파일로 dl_name을 기준으로 합쳤다.
-> pills_info.csv 파일
![pills_info]()


* pills_info.csv 파일을 프로젝트의 database 폴더에 넣음


# 2. models
## 1) models 폴더 구조

📦test_code2
┣ 📂models
 ┃ ┣ 📂yolov8
 ┃ ┃ ┗ 📜best.pt
 ┃ ┗ 📂resnet
 ┃ ┃ ┗ 📜best.pt

## 2) resnet 학습
### (1) colab => resnet_training.ipynb
```
from google.colab import drive
drive.mount('/content/drive')

import torch
import torch.nn as nn
import torch.optim as optim
from torchvision import datasets, transforms, models
from torch.utils.data import DataLoader
```
```
# 데이터셋 로드
transform = transforms.Compose([
    transforms.Resize((224, 224)),
    transforms.ToTensor(),
])

train_dataset = datasets.ImageFolder('/content/drive/MyDrive/Team3_pill/data/dataset/train/images', transform=transform)
train_loader = DataLoader(train_dataset, batch_size=32, shuffle=True)
```
```
# ResNet 모델 정의
class ResNet(nn.Module):
    def __init__(self, num_classes):
        super(ResNet, self).__init__()
        # pretrained=False 대신 weights=None 사용
        self.model = models.resnet18(weights=None)
        num_ftrs = self.model.fc.in_features
        self.model.fc = nn.Linear(num_ftrs, num_classes)

    def forward(self, x):
        return self.model(x)

# 클래스 수 설정
num_classes = 15  # 예시로 클래스 수를 15로 설정

# 모델 초기화
model = ResNet(num_classes=num_classes)
```
-> 지금 가지고 있는 train 데이터셋이 적어서 resnet18 사용함
-> 클래스 수 = 약의 갯수(약의 폴더 수)

```
# 손실 함수와 옵티마이저 정의
criterion = nn.CrossEntropyLoss() 
optimizer = optim.Adam(model.parameters(), lr=0.001) 
```
-> criterion : 모델의 출력(각 클래스에 대한 확률 분포)과 실제 정답 레이블을 비교하여 손실을 계산
-> optimizer : 옵티마이저를 사용하여 모델의 가중치를 업데이트할 방법을 설정. 학습률은 0.001로 설정

```
# 학습 루프
num_epochs = 10 # 전체 학습 반복 횟수를 10으로 설정
for epoch in range(num_epochs):
    model.train()
    running_loss = 0.0 
    for images, labels in train_loader:
        optimizer.zero_grad() 
        outputs = model(images) 
        loss = criterion(outputs, labels) 
        loss.backward() 
        optimizer.step() 
        running_loss += loss.item() 

    print(f"Epoch [{epoch+1}/{num_epochs}], Loss: {running_loss/len(train_loader)}")
```
![resnet_epoch]()

-> num_epochs = 10 : 전체 학습 반복 횟수를 10으로 설정, 데이터 수가 적어서 높은 epoch으로 설정할 경우 과적합이 발생할 수 있기 때문에
-> running_loss = 0.0 : 한 에폭 동안 발생하는 총 손실 값을 누적하기 위한 변수를 초기화
-> optimizer.zero_grad() : 옵티마이저의 기울기(gradient)를 초기화
-> outputs = model(images) : 모델에 이미지 데이터(images)를 입력으로 넣어 예측값(outputs)을 얻음
-> loss = criterion(outputs, labels) : 손실 함수(criterion)를 사용하여 모델의 예측값(outputs)과 실제 정답 레이블(labels) 간의 차이를 계산하여 손실 값(loss)
-> loss.backward() : 역전파(backpropagation) 알고리즘을 통해 손실 값을 기반으로 각 가중치에 대한 기울기를 계산
-> optimizer.step() : 계산된 기울기를 사용하여 옵티마이저가 모델의 가중치를 업데이트
-> running_loss += loss.item() : 현재 배치의 손실 값을 running_loss에 누적하여 한 에폭 동안의 총 손실 값을 계산

```
# 모델 저장
torch.save(model.state_dict(), '/content/drive/MyDrive/Team3_pill/model/resnet/best.pt')
print("Model saved successfully!")
```

* 저장된 best.pt파일을 프로젝트의 model/resnet 폴더에 저장

## 3) yolov8 학습
### (2) colab => yolov8_training.ipynb
```
from google.colab import drive
drive.mount('/content/drive')
```

```
import torch
from torch.utils.data import DataLoader
from torchvision import datasets, transforms
import torch.nn as nn
import torch.optim as optim
```

```
# 데이터셋 로드
transform = transforms.Compose([
    transforms.Resize((224, 224)),
    transforms.ToTensor(),
])

train_dataset = datasets.ImageFolder('/content/drive/MyDrive/Team3_pill/data/dataset/train/images', transform=transform)
train_loader = DataLoader(train_dataset, batch_size=32, shuffle=True)
```
```
class YOLOv8(nn.Module):
    def __init__(self, num_classes):
        super(YOLOv8, self).__init__()
        # YOLOv8 레이어 정의
        self.conv1 = nn.Conv2d(3, 16, kernel_size=3, stride=1, padding=1)
        self.conv2 = nn.Conv2d(16, 32, kernel_size=3, stride=1, padding=1)
        self.fc1 = nn.Linear(32 * 224 * 224, 1000)
        self.fc2 = nn.Linear(1000, num_classes)  # 클래스 수에 맞게 업데이트

    def forward(self, x):
        x = torch.relu(self.conv1(x))
        x = torch.relu(self.conv2(x))
        x = x.view(x.size(0), -1)
        x = torch.relu(self.fc1(x))
        x = self.fc2(x)
        return x

num_classes = 15  # 클래스 수 = 약 폴더 수 
model = YOLOv8(num_classes)
```

```
# 손실 함수와 옵티마이저 정의
criterion = torch.nn.CrossEntropyLoss()
optimizer = torch.optim.Adam(model.parameters(), lr=0.001)
```
```
# 훈련 루프
num_epochs = 10
for epoch in range(num_epochs):
    model.train()
    running_loss = 0.0
    for images, labels in train_loader:
        optimizer.zero_grad()
        outputs = model(images)
        loss = criterion(outputs, labels)
        loss.backward()
        optimizer.step()
        running_loss += loss.item()

    print(f"Epoch [{epoch+1}/{num_epochs}], Loss: {running_loss/len(train_loader):.4f}")
```
![yolo_epoch]()

```
# 모델 저장
torch.save(model.state_dict(), '/content/drive/MyDrive/Team3_pill/model/yolov8/best.pt')
```

* 저장된 best.pt파일을 프로젝트의 model/yolov8 폴더에 저장


# 3. scripts
## 1) scripts 폴더 구조
📦test_code2
📂scripts
    ┣ 📂__pycache__
    ┃ ┣ 📜utils.cpython-38.pyc
    ┃ ┣ 📜yolov8.cpython-38.pyc
    ┃ ┣ 📜resnet.cpython-38.pyc
    ┃ ┣ 📜pill_detection.cpython-38.pyc
    ┃ ┗ 📜clova_ocr.cpython-38.pyc
    ┣ 📜pill_detection.py
    ┣ 📜utils.py
    ┣ 📜yolov8.py
    ┣ 📜resnet.py
    ┗ 📜clova_ocr.py

## 2) utils.py
```
import torch

def load_model(model_path, model_class):
    """
    모델을 로드하는 함수
    """
    model = model_class()
    model.load_state_dict(torch.load(model_path))
    model.eval()
    return model
```
공통으로 사용되는 유틸리티 함수들을 포함하는 파일이다. 주로 모델을 로드하는 함수를 정의

## 3) resnet.py
```
import torch
import torch.nn as nn
import torchvision.models as models

class ResNet(nn.Module):
    def __init__(self, num_classes=15):  # 필요한 클래스 수에 따라 수정
        super(ResNet, self).__init__()
        self.model = models.resnet18(pretrained=False)  # pretrained=False로 변경
        num_ftrs = self.model.fc.in_features
        self.model.fc = nn.Linear(num_ftrs, num_classes)

    def forward(self, x):
        return self.model(x)
```
ResNet 모델을 정의하는 파일이다. ResNet 모델의 구조를 정의하고, 분류를 수행할 수 있도록 한다.


## 4) yolov8.py
```
import torch
from ultralytics import YOLO

class YOLOv8:
    def __init__(self):
        # YOLOv8 모델 초기화
        self.model = YOLO('yolov8n.pt')  # YOLOv8n 모델을 사용합니다. 다른 모델을 원할 경우 경로를 변경하세요.

    def detect(self, image):
        # 모델을 사용하여 이미지에서 객체 검출
        results = self.model(image)
        return results
```
YOLOv8 모델을 정의하고 객체 탐지를 수행하는 파일


## 5) clova_ocr.py
```
import requests
import cv2
import json
import uuid
import time

# Clova OCR API 정보 (환경 변수나 설정 파일로부터 로드)
CLOVA_OCR_URL = 'put your url'
CLOVA_OCR_KEY = 'put your ocr key'

def call_clova_ocr(image):
    """
    Clova OCR API를 호출하여 이미지에서 텍스트를 인식하는 함수
    """
    print("Starting OCR process...")
    _, encoded_image = cv2.imencode('.jpg', image)
    image_data = encoded_image.tobytes()
    print("Image encoded successfully.")

    headers = {
        'X-OCR-SECRET': CLOVA_OCR_KEY,
    }
    print("Headers set.")

    request_json = {
        'images': [{'format': 'jpg', 'name': 'demo'}],
        'requestId': str(uuid.uuid4()),
        'version': 'V2',
        'timestamp': int(round(time.time() * 1000))
    }

    payload = {'message': json.dumps(request_json).encode('UTF-8')}
    files = [('file', image_data)]

    response = requests.post(CLOVA_OCR_URL, headers=headers, data=payload, files=files)
    print(f"OCR request sent. Status code: {response.status_code}")

    if response.status_code == 200:
        result = response.json()
        print("OCR request successful.")
        if 'images' in result and len(result['images']) > 0:
            return result['images'][0]['inferResult']
        else:
            print("No 'images' field in OCR response.")
            return None
    else:
        print(f"Error {response.status_code}: {response.text}")
        return None
```

네이버 클로바 OCR API를 호출하여 이미지에서 텍스트를 인식하는 파일


## 6) pill_detection.py
```
import cv2
import pandas as pd
import torch
from PIL import Image
from torchvision import transforms
import matplotlib.pyplot as plt
from ultralytics import YOLO

# Load YOLOv8 and ResNet models
from scripts.yolov8 import YOLOv8
from scripts.resnet import ResNet
from scripts.utils import load_model
from scripts.clova_ocr import call_clova_ocr

# YOLOv8 및 ResNet 모델 로드
yolov8_model = YOLOv8()
resnet_model = load_model('models/resnet/best.pt', ResNet)

# 알약 정보 데이터베이스 로드
pill_info_df = pd.read_csv('data/database/pills_info.csv')

def detect_pills(image):
    """
    YOLOv8를 사용하여 이미지에서 알약을 검출하는 함수
    """
    results = yolov8_model.detect(image)
    return results

def recognize_imprint(pill_image):
    """
    네이버 클로바 OCR을 사용하여 알약의 각인 인식
    """
    print("Starting to recognize imprint...")
    result = call_clova_ocr(pill_image)
    if result and 'fields' in result:
        imprint_text = ' '.join([field['inferText'] for field in result['fields']])
        return imprint_text
    print("No text recognized.")
    return ""

def classify_pill(pill_image):
    """
    ResNet을 사용하여 알약을 분류하는 함수
    """
    transform = transforms.Compose([
        transforms.Resize((224, 224)),
        transforms.ToTensor(),
    ])
    pill_image = transform(Image.fromarray(pill_image))
    pill_image = pill_image.unsqueeze(0)  # 배치 차원 추가
    output = resnet_model(pill_image)
    _, predicted = torch.max(output, 1)
    return predicted.item()

def get_pill_info(imprint):
    """
    각인을 통해 알약 정보를 조회하는 함수
    """
    if 'print_front_x' not in pill_info_df.columns:
        raise KeyError("'print_front_x' column not found in the pill information database.")
    
    pill_info = pill_info_df[pill_info_df['print_front_x'] == imprint]
    if not pill_info.empty:
        return pill_info.iloc[0]
    else:
        return None

def plot_results(image, boxes, imprints):
    """
    검출 결과와 각인을 시각화하는 함수
    """
    for (box, imprint) in zip(boxes, imprints):
        x1, y1, x2, y2 = box.xyxy[0].tolist()
        conf = box.conf[0].item()
        cls = box.cls[0].item()
        cv2.rectangle(image, (int(x1), int(y1)), (int(x2), int(y2)), (0, 255, 0), 2)
        label = f"pill"
        cv2.putText(image, label, (int(x1), int(y1) - 10), cv2.FONT_HERSHEY_SIMPLEX, 0.9, (0, 255, 0), 2)
    
    plt.figure(figsize=(10, 10))
    plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
    plt.axis('off')
    plt.show()

def main(image_path):
    """
    메인 함수
    """
    image = cv2.imread(image_path)
    results = detect_pills(image)  # 모델을 사용하여 객체 검출
    print("Detection results:", results)  # 결과 구조 확인

    if results[0].boxes is not None:  # 결과가 존재하는 경우
        boxes = results[0].boxes
    else:
        print("No detections found.")
        return

    imprints = []
    for box in boxes:
        x1, y1, x2, y2 = map(int, box.xyxy[0].tolist())
        pill_image = image[y1:y2, x1:x2]
        imprint = recognize_imprint(pill_image)
        
        if imprint:
            print(f"Recognized Imprint: {imprint}")
        else:
            print("알약 글씨 인식 못함")
        
        imprints.append(imprint)
        
        pill_class = classify_pill(pill_image)
        print(f"Pill Class: {pill_class}")

        pill_info = get_pill_info(imprint)
        if pill_info is not None:
            print(f"알약 이름: {pill_info['dl_name']}")
            print(f"성분: {pill_info['dl_material_x']}")
        else:
            print("알약 정보를 찾을 수 없습니다.")

    plot_results(image, boxes, imprints)

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Pill Detection Project Main Script")
    parser.add_argument('--image', type=str, help='Path to the image file', required=True)
    args = parser.parse_args()

    main(args.image)

```

모든 모듈을 통합하여 알약을 검출하고, 분류하며, OCR을 통해 각인을 인식하는 메인 파일

* YOLOv8를 사용하여 알약 검출
* ResNet을 사용하여 알약 분류
* Clova OCR을 사용하여 각인 인식
* 결과 시각화 및 출력

# 4. main.py
```
import argparse
from scripts.pill_detection import main as detect_pills

def main():
    parser = argparse.ArgumentParser(description="Pill Detection Project Main Script")
    parser.add_argument('--image', type=str, help='Path to the image file', required=True)
    args = parser.parse_args()

    # 실시간 알약 검출 및 인식 수행
    detect_pills(args.image)

if __name__ == "__main__":
    main()
```
main.py는 전체 프로젝트의 메인 엔트리 포인트이다. 이 파일은 사용자가 지정한 이미지를 입력으로 받아, 이를 처리하여 알약을 검출하고, 각인 인식을 수행하며, 분류된 결과를 출력한다.

* 명령줄 인수로 입력 이미지를 받음
* pill_detection.py에서 정의한 main 함수를 호출하여 전체 검출 및 인식 과정을 실행

# 4. 프로젝트 실행 방법
## 1) 가상환경 설정
### anaconda powershell prompt 에서
```
conda create -n p38_testcode2 python=3.8
```

## 2) python interpreter에서 가상환경을 p38_testcode2로 설정한 후 requirements.txt 설치
```
pip install -r requirements.txt
```

## 3) 예제 코드 실행

```
python main.py --image data/dataset/test/images/K-021652_0_0_0_0_75_000_200_png.rf.47d73f507a96d4e700c76101cd196592.jpg
```

* 결과
알약 정보를 찾을 수 없음......ㅠㅠ
![fail]()
![pillDetect]()

-> 처음엔 약과 처방전 둘 다 인식할 수 있는 OCR을 찾다가 네이버 클로바 OCR을 선택했었다. 한글과 영어 모두 지원한다고 해서 딱이라고 생각했는데, 알고 보니 알약 각인 인식은 잘 안됐다ㅠㅜㅠㅜ

그래서 다음 테스트에서는 Tesseract OCR을 써보기로 결정했다. 한글 인식률이 낮다는 말도 있어서 아마 처방전 인식은 잘 못할 것 같지만, 알약 각인에 특화된 학습을 시키면 알약 글씨는 잘 인식할 것 같다. Tesseract OCR을 알약 각인에 맞춰 학습시켜서 다시 도전해 보자!!

---