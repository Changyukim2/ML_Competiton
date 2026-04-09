# iM-BANK-_-ML_Competiton
IM Digital banker Academy Machine Learning Competiton



📌 Bank Customer Churn Prediction
1. 프로젝트 개요

은행 고객 데이터를 기반으로 고객 이탈(churn)을 예측하는 모델을 구축하고,
이탈에 영향을 미치는 주요 요인을 분석하는 것을 목표로 했다.

2. 데이터 및 목표
데이터: Bank Customer Churn Dataset
목표: 고객의 이탈 여부(Churn = 1)를 예측
특징: 이탈 고객 비율 약 20%로 불균형 데이터
3. 진행 과정
① 전처리
customer_id 제거 (식별 변수)
범주형 변수(LabelEncoder로 변환)
stratify를 사용해 train/valid 분할
② EDA
churn 비율 확인 → 불균형 데이터 확인
country, gender, age에서 그룹별 차이 확인
특히 age에서 이탈 고객이 높은 연령대에 집중되는 경향 확인
③ Feature Selection
RandomForest importance 기반 상위 7개 변수 선택
주요 변수:
age, balance, products_number, credit_score 등
④ 모델 비교 및 튜닝
PyCaret으로 여러 모델 성능 비교 (F1 기준)
Optuna로 하이퍼파라미터 튜닝
5-fold CV 기반 모델 성능 비교
⑤ 모델 구성
Best Single Model: RandomForest
Stacking 모델 구성:
Logistic Regression + Tree 기반 모델
4. 모델 성능
Model	F1 Score	Accuracy
RandomForest	0.6049	0.821
Stacking	0.5718	0.854

👉 불균형 데이터 특성상 F1 score 기준으로 RandomForest가 더 적합

5. SHAP 기반 인사이트
주요 영향 변수:
age
products_number
balance
해석:
age ↑ → 이탈 확률 증가
products_number → 특정 구간에서 이탈 증가 (비선형 패턴)
balance ↑ → 이탈 가능성 증가

👉 따라서

고연령 고객
상품 이용 패턴이 특이한 고객
잔고가 높은 고객

을 중심으로 맞춤형 유지 전략이 필요
