title: MLOps - part1
author: Daehan Kang
categories:
  - MLOps
  - ''
tags:
  - MLOps
  - ''
date: 2023-02-07 17:27:00
---
# 머신러닝 모델 개발에서 마주하는 난관
---
<br>

### 정제되지 않은 파이프라인으로 인한 부진한 진척도
- 머신러닝 모델 개발 작업은 반복적이고 비선형적인 프로세스를 따름.
- 데이터를 기반으로 하고 있기 때문에 모니터링 결과를 바탕으로 주기적인 업데이트 필요
- 많은 기업들이 이 단계를 원활히 수행할 수 있는 파이프라인을 마련하지 못해 모델 개발단계에서 배포 단계까지 진척이 늦어짐

### 불필요한 리소스 활용 증가
- 데이터의 가변성으로 인해 특정 모델 배포 후 새로운 데이터 기반의 지속적인 모니터링, 학습, 업데이트 필요
- 체계화된 파이프라인이 없는 상태에서 운영팀으로부터 머신러닝 팀에 새로운 데이터 전달하는데 많은 리소스 및 시간이 소요됨.

### 데이터 사이언티스트와 소프트웨어 개발자 간의 데이터 사일로 (Data Silo)
- 머신러닝 리서처 및 엔지니어와 소프트웨어 개발자 간의 업무 공유와 협업이 어려워지는 문제가 발생.

* 데이터 사일로 (Data Silo) : 조직 내에 존재하는 일련의 정보가 조직 내 다른 부서와 공유되지 않아 특정 부서만의 데이터로 남게 되는 현상<br><br><br>

# MLOps 상세 개념
---

MLOps의 목표는 DevOps의 목표와 마찬가지로 사용자에게 서비스를 빠르게 전달하는 개발 문화이다.

## 코드 통합
이 과정에서는 원활한 실험을 위해 샘플링된 데이터를 사용하기도 하며, 최적화를 위한 다양한 시도들이 코드로 작성된다. 운영을 위해선 프로덕션 데이터의 ELT, 분산처리, 불필요한 로직 제거, 예측 추론 시간을 서비스 수준에 맞게 학습 단계 단순화와 같이 운영 수준의 변형과정이 필요하다.

<div style="text-align:center;"><img src="https://user-images.githubusercontent.com/79561091/217190764-1d47d855-0273-4b75-971a-f043d295ca5c.jpg" /></div><br>
<center>[그림1] 일반적인 머신러닝 파이프라인</center>

MLOps 의 통합은 실험환경에서 결정된 데이터 변형, 학습, 평가, 재학습 주기, 모니터링 지표 설정 등 실제 서비스 운영환경으로 통합되는 것을 의미한다.

## 테스트
예측 모델을 단순하게 생각하면 `output = model.predict(inputData)` 이다. 일반적인 소프트웨어 개발이라면 `predict()` 의 내부 동작을 알기 때문에, 다양한 시나리오를 만들어 테스트할 수 있다. 하지만 모델의 경우 내부 동작 방식을 이해할 수 없는 경우가 대부분이다. 그렇기 때문에 `output` 에 대한 검증을 하기 어렵다. 일반적인 소프트웨어의 유닛테스트와 같이 `assert output == 0.5` 와 같이 나온다고 모델이 정상이라고 판단할 수 없다. 모델을 테스트하기 위해선 Accuracy, Precision/Recall curve, Confusion matrix 와 같은 다양한 지표들을 활용해야 한다.

## 모니터링
모델 endpoint 에 요청된 데이터와 예측했던 값들을 수집하고, 이것들이 학습된 데이터와 Statistical distance 를 계산하는 것이다. 프로젝트의 목적, 알고리즘, 데이터의 특성에 따라 판단 방법은 달라질 수 있기 때문에, 어떤 방법을 사용할지 결정하는 것도 중요하다.

## 배포
MLOps 의 배포는 코드 통합, 새로운 데이터의 학습, 서비스로 모델 전달, 모니터링 방식 적용까지의 파이프라인의 배포이다. 이 파이프라인이 배포되면 Raw data에서 모델이 서비스 전달되고 모니터링되는 과정이 동작하게 된다. 중요한 점은 MLOps 의 파이프라인은 일회용 아니라는 것이다. 배포 이후 다시 모델 개발 단계로 신속하게 전환이 되어야 한다. 이전 모델과 운영된 데이터의 분석 후 다시 통합, 학습, 전달, 모니터링이 이루어져야 한다.

<div style="text-align:center;"><img src="https://user-images.githubusercontent.com/79561091/217190755-01dc0594-574e-456f-b6ef-1b70e2a8468e.jpg" /></div><br>
<center>[그림2] ML 개발, 통합, 테스트, 배포, 모니터링 프로세스</center>