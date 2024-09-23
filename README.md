# Title (Please modify the title)
## Team

| ![박패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![이패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![최패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![김패캠](https://avatars.githubusercontent.com/u/156163982?v=4) |
| :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: |
|            [이민석](https://github.com/UpstageAILab)             |            [권세진](https://github.com/UpstageAILab)             |            [한성범](https://github.com/UpstageAILab)             |            [김동호](https://github.com/UpstageAILab)             |    
|                            팀장, 담당 역할                             |                            담당 역할                             |                            담당 역할                             |                            담당 역할                             

## 0. Overview
### Environment
- 3090 GPU 서버를 VSCode와  SSH로 연결하여 사용

### Requirements
- VPN, SSH key, VSCode

## 1. Competiton Info

### Overview

- 본 대회는 House Price Prediction 경진대회는 주어진 데이터를 활용하여 서울의 아파트 실거래가를 효과적으로 예측하는 모델을 개발하는 대회이다.

- 부동산은 의식주에서의 주로 중요한 요소 중 하나입니다. 이러한 부동산은 아파트 자체의 가치도 중요하고, 주변 요소 (강, 공원, 백화점 등)에 의해서도 영향을 받아 시간에 따라 가격이 많이 변동합니다. 개인에 입장에서는 더 싼 가격에 좋은 집을 찾고 싶고, 판매자의 입장에서는 적절한 가격에 집을 판매하기를 원합니다. 부동산 실거래가의 예측은 이러한 시세를 예측하여 적정한 가격에 구매와 판매를 도와주게 합니다. 그리고, 정부의 입장에서는 비정상적으로 시세가 이상한 부분을 체크하여 이상 신호를 파악하거나, 업거래 다운거래 등 부정한 거래를 하는 사람들을 잡아낼 수도 있습니다. 

저희는 이러한 목적 하에서 다양한 부동산 관련 의사결정을 돕고자 하는 부동산 실거래가를 예측하는 모델을 개발하는 것입니다. 특히, 가장 중요한 서울시로 한정해서 서울시의 아파트 가격을 예측하려고합니다.

### Timeline

- September 02, 2024 - Start Date
- September 13, 2024 - Final submission deadline

## 2. Components

### Directory

- _Insert your directory structure_

e.g.
```
├── code
│   ├── Collection    <- Code for handling external data sources & merging them with original dataset
    ├── EDA           <- Initial data exploration & analysis to uncover patterns, spot anomalies, test hypotheses.
    ├── Preprocessing <- Code for data cleaning, transformation, and preparation for modeling
    └── Mdoel         <- Model Trained and Predict target of test data, or model Ensembles
```
<!--```
│   │   └── model_train.ipynb
│   └── train.py
├── docs
│   ├── pdf
│   │   └── (Template) [패스트캠퍼스] Upstage AI Lab 1기_그룹 스터디 .pptx
│   └── paper
└── input
    └── data
        ├── eval
        └── train
``'-->

## 3. Data descrption

### Dataset overview

- 데이터 형태 : .csv 파일
- 데이터 개수: train(1118822개), test(9272개)
- 아파트 정보에 대한 변수: 52개
- 서울시 지하철역, 버스정류장 데이터 추가

  ![image](https://github.com/user-attachments/assets/6488188a-aeda-4980-8c5b-9b7621984fb7)

- 변수별 결측치 비율
    - 'k-'가 붙은 변수들은 결측치 비율이 높은 것을 확인할 수 있음
    - x,y 좌표의 결측 비율이 높기 때문에 QGIS를 활용하여 좌표값 대체
 
  ![image](https://github.com/user-attachments/assets/ee959df0-7014-4c90-83d3-b1dba5ede320)

 - 아파트 실거래가 예측에 지하철역과 버스정류장 데이터를 추가하였다. 이는 교통 접근성이 주거지 선택에 있어 매우 중요한 요소이기 때문입니다. 지하철역과 버스정류장은 거주자의 출퇴근 편의성과 이동성을 크게 좌우하며, 이러한 교통망의 접근성은 아파트 가격에 직접적인 영향을 미칩니다. 특히 대중교통과 가까울수록 아파트의 가치가 높아질 가능성이 크기 때문에, 이를 고려한 예측 모델은 보다 정확한 가격 예측을 가능하게 합니다.
 
 ![image](https://github.com/user-attachments/assets/470e31d6-9c3b-44e8-a6cc-7955e5f4e0bb)



### EDA

- _Describe your EDA process and step-by-step conclusion_

### Data Processing

- _Describe data processing process (e.g. Data Labeling, Data Cleaning..)_

**외부데이터 활용**

 - _외부데이터_

## 4. Modeling

### Model Select

- 머신러닝을 이용한 아파트 매매가격 예측을 진행한 선행 연구를 참고하여 모델을 선정하였습니다.
- 선행 연구에서는 모델의 파라미터 범위 범위를 제공하지 않아 임의의 값으로 모델링을 진행하였습니다.
- 선행 연구에서 참고한 모델은 XGBoost, CatBoost, LGBM으로 총 3가지 모델의 성능일 비교하였습니다.

| 모델명 | RMSE | 특징 |
| :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: |
|           XGBRegression             |            **3818.69**            |      objective='reg:squarederror', n_estimators=2000, learning_rate=0.1, max_depth=10, random_state  =1  |    
|           CatBootRegressor          |            3968.73            |     loss_function='RMSE', random_seed=1, n_estimators=2000, max_depth=10, learning_rate=0.1              |
|           LGBMRegressor             |           4335.44             |     n_estimators=2000, max_depth=10, random_state  =1                                                    |

### Model descrition

- <img src="https://github.com/user-attachments/assets/39b584bb-de72-40fb-8239-c66bfea65287" alt="XGBoost란?" width="30" height="30">  XGBoost란?

    + XGBoost는 Extreme Gradient Boosting의 약자
    + Boosting 기법을 활용한 알고리즘 중에서는 Gradient Boost가 가장 대표적
    + XGBoost는 알고리즘을 병렬 학습이 지원되도록 구현한 라이브러리
    + 회귀 및 분류 문제에 적용이 가능하며, 뛰어난 성능과 효율적인 자원 사용으로 널리 사용되고 있는 알고리즘
 
- <img src="https://github.com/user-attachments/assets/535f69f9-d2ff-47ea-b7f1-77a30123f7c1" alt="?" width="30" height="30">  XGBoot 장점
?

   + GBM 대비 빠른 수행시간
   + 병렬 처리 학습으로 분류 속도가 빠름
   + 과적합 규제(Regularization)
   + 회기 및 분류에서 뛰어난 예측 성능을 발휘
   + CART(Classification and regression tree) 앙상블 모델을 사용
   + Early Stopping(조기 종료) 기능이 있음
   + 결측치를 내부적으로 처리 가능

### Modeling Process

- _Write model train and test process with capture_

## 5. Result

### Leader Board

- _Insert Leader Board Capture_
- _Write rank and score_

### Presentation

- _Insert your presentaion file(pdf) link_

## etc

### Meeting Log

- _Insert your meeting log link like Notion or Google Docs_

### Reference

- _Insert related reference_
