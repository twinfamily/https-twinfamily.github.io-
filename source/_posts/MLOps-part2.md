title: MLOps -part2
author: Daehan Kang
tags:
  - MLOps
categories:
  - MLOps
date: 2023-09-04 15:57:00
subTitle:
---
- mlflow 개념
- mlflow 설치 및 사용 방법
- mlflow 로컬 실행 시 에러 처리 (로컬 저장 안될 때)

## 1. MLflow 개념
MLflow는 A Machine Learning Lifecycle Platform이라는 컨셉을 가지고 있다.

MLflow는 머신러닝(Machine learning) 모델의 실험을 tracking하고 model을 공유 및 deploy 할 수 있도록 지원하는 라이브러리다. 즉, 머신러닝 학습과 관련된 전반적인 lifecycle을 지원해주는 라이브러리 라고 볼 수 있다.

[databricks의 mlflow 오픈소스 링크](https://www.databricks.com/product/managed-mlflow)
<br>
[mlflow 공식링크](https://mlflow.org/)

## 2. 주요 기능

1.  MLflow Tracking
- 머신러닝 모델( Machine Learning model)을 학습시킬 때 생기는 각종 파라미터, 그리고 머신러닝 모델 training이 끝난 후 metric의 결과 등을 logging하고 그 기록 결과를 web ui로도 확인할 수 있다.
2.  MLflow Projects
- Anaconda나 (Anaconda 없이도 사용 가능) docker 등을 사용해서 만들어 둔 모델을 reproducible 하고 실행할 수 있도록 코드 패키지 형식으로 지원해준다. 이러한 형식으로 만들어진 환경을 재사용할 수 있다.
3.  MLflow Models
- 동일한 모델을 Docker, Apache Spark, AWS 등에서 쉽게 배치할 수 있도록 지원한다.
4.  MLflow Model Registry
- MLflow 모델의 전체 라이브사이클을 공동으로 관리하기 위한 centralized model store, set of API, UI를 지원 한다.

## 3. 사용법

먼저 기본 환경 설정이 필요하다.
- python3.6 버전 이상 설치
- conda : mlflow models serve 할 때(서빙할 때) 필요

```
# 새로운 디렉토리를 하나 생성한 뒤, 해당 디렉토리로 이동 후 설치
mkdir mlflow-test
cd mlflow-test 

# python 버전 확인 
python -V 
pip install mlflow
mlflow --version
```

## 4. MLflow tracking server 띄우기

