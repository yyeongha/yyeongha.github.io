---
title: 알약 프로젝트 준비
categories: [Project] 
date: 2024-06-08
last_modified_at: 2024-06-08
---

# 사용할 모델의 requiremets 찾기
## yolov8
python >= 3.8
PyTorch>=1.8.
setuptools>=57.0.0
wheel
"matplotlib>=3.3.0",
"opencv-python>=4.6.0",
"pillow>=7.1.2",
"pyyaml>=5.3.1",
"requests>=2.23.0",
"scipy>=1.4.1",
"torch>=1.8.0",
"torchvision>=0.9.0",
"tqdm>=4.64.0",
"psutil",
"py-cpuinfo",
"pandas>=1.1.4",
"seaborn>=0.11.0",
"ultralytics-thop>=0.2.5",
"ipython",
"check-manifest",
"pre-commit",
"pytest",
"pytest-cov",
"coverage[toml]",
"mkdocs>=1.6.0",
"mkdocs-material>=9.5.9",
"mkdocstrings[python]",
"mkdocs-jupyter",
"mkdocs-redirects",
"mkdocs-ultralytics-plugin>=0.0.45"
"onnx>=1.12.0",
"coremltools>=7.0; platform_system != 'Windows' and python_version <= '3.11'",
"openvino>=2024.0.0",
"tensorflow>=2.0.0",
"tensorflowjs>=3.9.0",
"keras",
"flatbuffers>=23.5.26,<100; platform_machine == 'aarch64'",
"numpy==1.23.5; platform_machine == 'aarch64'",
"h5py!=3.11.0; platform_machine == 'aarch64'"
"lancedb",
"duckdb<=0.9.2",
"streamlit",
"comet",
"tensorboard>=2.13.0",
"dvclive>=2.12.0"
"hub-sdk>=0.0.5",
"ipython",
"albumentations>=1.4.6",
"pycocotools>=2.0.7",



## labelimg
pyqt5==5.14.1,  Python >=3.7
lxml==4.9.1, Python >=2.7, !=3.0.*, !=3.1.*, !=3.2.*, !=3.3.*, != 3.4.*


## EAST : 이미지의 글씨 영역 알아냄
Shapely==1.5.13, Python :: 2.6, Python :: 2.7, Python :: 3
Flask==0.10.1
matplotlib==1.5.1
scipy==0.19.0
plumbum==1.6.2
numpy==1.12.1
ipython==6.1.0
Pillow==4.2.1
-> east는 마지막 업데이트가 7년전. 너무 오래 되서 다른 모델과 호환이 어려울 것 같아 사용하지 않겠음


## tesseract ocr, naver clova
### tesseract ocr
* 윈도우는 직접 설치
https://github.com/UB-Mannheim/tesseract/wiki

* 쓰는 방법
https://blog.naver.com/dnjswns2280/221564812092

### naver clova ocr (처방전 한글 인식 때문)
100회까지는 무료
100회 이상부터는 호출당 3원

* 쓰는 방법
https://yunwoong.tistory.com/153

























---