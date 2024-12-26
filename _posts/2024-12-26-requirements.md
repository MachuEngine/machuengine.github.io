---
layout: "single"
title: "[AI] requirements.txt와 environment.yml 파일 생성"
categories:
  - ai
tags:
  - requirements
  - environment
description: "requirements.txt와 environment.yml 파일 생성"
author: "안종민"
date: "2024-12-19"
---
## requirements.txt 파일 생성
- conda 가상환경이 활성화된 상태
```bash
conda activate <myenv>
```
- 현재 conda 환경에서 실제 사용되고 있는 필요 패키지만 requirements.txt 생성
```bash
pip freeze | findstr /V "@" > requirements.txt
```
- 생성된 requirements.txt 파일 확인 시 출력 내용 확인
```bash
matplotlib==3.9.2
mkl-service==2.4.0
ply==3.11
PyQt5==5.15.10
pywin32==307
torch==2.5.1
torchvision==0.20.1
```
---

## environment.yml 파일 생성
- conda 가상환경이 활성화된 상태
```bash
conda activate <myenv>
```
- 현재 conda 환경에서 실제 사용되고 있는 필요 패키지만 environment.yml 생성
```bash
conda env export --from-history > environment.yml
```
- 생성된 environment.yml 파일 확인 시 출력 내용 확인
```bash
name: cifar_env
channels:
defaults
https://repo.anaconda.com/pkgs/main
https://repo.anaconda.com/pkgs/r
https://repo.anaconda.com/pkgs/msys2
dependencies:
python=3.10
matplotlib
numpy
pandas
pytorch
scikit-learn
torchvision
ipykernel
prefix: C:\Users\Admin\anaconda3\envs\cifar_env
```