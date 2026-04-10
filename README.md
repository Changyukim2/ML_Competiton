# iM Digital Banker Academy Machine Learning Competition

## 📌 Bank Customer Churn Prediction

은행 고객 데이터를 기반으로 **고객 이탈(Churn) 여부를 예측**하고,  
이탈에 영향을 미치는 **주요 요인**을 분석한 프로젝트입니다.

---

## 1. Project Overview

본 프로젝트의 목표는 은행 고객 데이터를 활용하여  
고객의 이탈 여부를 예측하는 머신러닝 모델을 구축하고,  
이탈 가능성이 높은 고객의 특성을 파악하는 것입니다.

이를 통해 고객 유지 전략 수립에 활용할 수 있는 인사이트를 도출하고자 했습니다.

---

## 2. Dataset

- **Dataset**: Bank Customer Churn Dataset ( 캐글 , row:10000, col:12)
- **Target**: `Churn`  
  - `1` = 이탈 고객
  - `0` = 유지 고객
- **Data Characteristics**
  - 고객 이탈 비율 약 **20%**
  - 클래스 불균형 데이터

---

## 3. Workflow

### ① Data Preprocessing
- `customer_id` 제거  
  → 식별 변수이므로 예측에 불필요
- 범주형 변수 인코딩  
  → `LabelEncoder` 사용
- `train / validation` 데이터 분할  
  → `stratify` 적용으로 클래스 비율 유지

### ② Exploratory Data Analysis (EDA)
- 전체 `churn` 비율 확인  
  → 불균형 데이터임을 확인
- `country`, `gender`, `age` 기준 그룹별 차이 분석
- 특히 `age` 변수에서  
  이탈 고객이 상대적으로 높은 연령대에 집중되는 경향 확인

### ③ Feature Selection
- `RandomForest`의 feature importance 기반으로 상위 7개 변수 선택
- 주요 변수:
  - `age`
  - `balance`
  - `products_number`
  - `credit_score`
  - 그 외 주요 파생 변수

### ④ Model Comparison & Tuning
- `PyCaret`을 활용하여 다양한 모델 성능 비교
- 평가 기준은 **F1 Score**
- `Optuna`를 활용해 하이퍼파라미터 튜닝 진행
- `5-Fold Cross Validation` 기반으로 모델 성능 검증

### ⑤ Final Modeling
- **Best Single Model**: RandomForest
- **Stacking Model** 구성:
  - Logistic Regression
  - Tree-based Models

---

## 4. Model Performance

| Model | F1 Score | Accuracy |
|------|---------:|---------:|
| RandomForest | 0.6049 | 0.8210 |
| Stacking | 0.5718 | 0.8540 |

### ✅ Interpretation
불균형 데이터에서는 단순 정확도(Accuracy)보다  
**F1 Score가 더 중요한 평가 지표**입니다.

따라서 Accuracy는 Stacking 모델이 더 높았지만,  
**F1 Score 기준으로는 RandomForest가 더 적합한 모델**이라고 판단했습니다.

---

## 5. SHAP-based Insights

SHAP 분석을 통해 고객 이탈에 큰 영향을 주는 주요 변수를 확인했습니다.

### 주요 영향 변수
- `age`
- `products_number`
- `balance`

### 해석
- **age 증가**
  - 고객 이탈 확률이 높아지는 경향
- **products_number**
  - 특정 구간에서 이탈 가능성이 증가하는 비선형 패턴 확인
- **balance 증가**
  - 이탈 확률이 높아지는 경향 확인

---

## 6. Business Insight

분석 결과를 바탕으로, 다음과 같은 고객군에 대해  
맞춤형 유지 전략이 필요하다고 해석할 수 있습니다.

- **고연령 고객**
- **상품 이용 패턴이 특이한 고객**
- **잔고가 높은 고객**

즉, 단순히 이탈 여부를 예측하는 데 그치지 않고,  
이탈 가능성이 높은 고객군을 조기에 식별하여  
차별화된 고객 유지 전략 수립에 활용할 수 있습니다.

---

## 7. Tech Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge&logo=plotly&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-4C72B0?style=for-the-badge&logo=python&logoColor=white)
![Scikit--learn](https://img.shields.io/badge/Scikit--learn-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white)
![PyCaret](https://img.shields.io/badge/PyCaret-1C1C1C?style=for-the-badge&logo=python&logoColor=white)
![Optuna](https://img.shields.io/badge/Optuna-3B82F6?style=for-the-badge&logo=optuna&logoColor=white)
![SHAP](https://img.shields.io/badge/SHAP-FF6F61?style=for-the-badge&logo=python&logoColor=white)

---

## 8. Conclusion

본 프로젝트에서는 은행 고객 데이터를 기반으로  
고객 이탈 예측 모델을 구축하고, 주요 영향 요인을 해석했습니다.

특히 불균형 데이터 환경에서는 Accuracy보다  
**F1 Score 중심의 모델 평가가 중요함**을 확인할 수 있었으며,  
최종적으로 **RandomForest 모델이 가장 적합한 성능**을 보였습니다.

또한 SHAP 분석을 통해 고객 이탈에 영향을 주는 핵심 변수를 해석하여,  
실제 비즈니스 관점에서 활용 가능한 인사이트까지 도출할 수 있었습니다.
