# 머신러닝 기반 당뇨병 발병 사전 예측 모델
### 실제 임상데이터(Real World Data)를 활용한 당뇨병 발병 사전 예측 모델 개발

---

```
# 참고: 프로젝트에 대한 자세한 overview는 첨부된 PROJECT_OVERVIEW.md 파일을 확인 바랍니다.
```

## 목차
* [1. 프로젝트 배경](#c1)
* [2. 데이터 소개](#c2)
* [3. EDA 및 전처리](#c3)
* [4. 모델링](#c4)
* [5. 모델링 결과](#c5)
* [6. 결론](#conclusion)
* [7. 한계 및 향후 과제](#c6)

---
## 프로젝트 배경<a class="anchor" id = "c1"> </a>

- '당뇨'란 혈액 속의 포도당 수치가 정상인보다 높은 상태를 말하며, 혈당이 높은 상태로 오랜 시간이 지나면 심근경색, 뇌졸중, 망막질환, 신장질환, 동맥경화와 같은 만성 합병증을 일으킬 수 있는 질환으로 **점차 유병률이 증가하고 있으며, 우리 일상을 위협하는 심각한 질환**이다.
- 코로나19(코로나 바이러스) 이후 실내 활동이 증가하고, 일상 생활 활동량 감소, 운동 빈도와 운동량의 감소, 식이 변화 등 일상 생활에서의 많은 변화가 있었다. 그리고 장기화 된 코로나 상황 속에서, 대한민국 국민 10명 중 약 5명은 코로나 이후 뭄무게가 3kg 이상 증가한 것으로 나타났다. 더 큰 문제는, 바로 이러한 모든 요인들이 **당뇨 유병률을 증가시키는 요인**이 된다는 것이다.
- **당뇨병 환자는 코로나19에 특히 더 취약**하다. 당뇨병은 우리 몸의 면역체계를 무너뜨려 감염병에 취약하게 만들며, 특히 당뇨병 환자는 일반인에 비해 코로나19의 감염 위험이 1.2배 더 높아 더 쉽게 감염 될 수 있다고 한다. 또한, 일반인에 비해 당뇨병 환자가 코로나19에 감염됐을 경우 예후가 나쁘다. 국내 코로나19 환자의 14.5~21.8%가 당뇨병 환자였고, 국내 5천여명의 코로나19 환자를 대상으로 한 연구에 따르면 당뇨병 환자가 코로나19 감염 시 기계호흡이 필요한 경우는 1.93배, 사망률은 2.66배 높았다.
- **코로나19 시대의 당뇨병 자가관리는 더욱 중요**해졌다. 특히 당뇨병에 취약한 한국인의 특성을 고려할 때, **만약 자기의 건강상태와 당뇨병 위험을 사전에 예측 할 수 있다면, 당뇨병으로 진행되는 것을 적절한 사전 대응과 신체 및 혈당 관리를 통해 예방** 할 수 있을 것이다. 이는 나아가 코로나19 감염을 예방하고 발생률 감소에도 영향을 줄 수 있을 것이며, 코로나19로 인한 중증도와 사망률 또한 감소시킬 수 있을 것이다.

---
## 데이터 소개<a class="anchor" id = "c2"> </a>
- 당뇨병 사전 진단 예측 모델링을 위해 당뇨병 진단 관련 실제 임상데이터(Real World Data)를 확보하여 사용하였다.
- 데이터셋은 성별, 나이 등 환자에 대한 기본 정보와 당뇨병 진단 여부, 그리고 혈압, 혈당, 콜레스테롤, 간, 신장 등과 관련된 여러 검사 수치에 대한 데이터로 이루어져 있다.
- 총 2,438개의 행과 26개의 컬럼/피처로 구성되어 있는데, 이 중 당뇨병 진단을 받은 데이터가 206개인 **불균형 데이터**이다.

---
## EDA 및 전처리<a class="anchor" id = "c3"> </a>

### 각 피처별 분포도

![image](https://user-images.githubusercontent.com/38115693/155295628-a33c5f53-4211-4056-8723-d01ea15b012f.png)

- 대부분의 피처가 정규성을 띄고 있는 것으로 보인다.
- 하지만 `Cr, AST, ALT, GGT, ALP` 등이 왼쪽으로 치우친 분포를 보인다.

### 라벨별 각 피처 분포도
![image](https://user-images.githubusercontent.com/38115693/147484996-1f8a17f3-2d3a-4ee3-af73-69b5245a755d.png)

- 종속변수인 labels별(당뇨병 진단을 받은 경우 1, 아닌 경우 0) 각 피처의 분포도 확인 결과, HbA1c, FBG, HDL 등 **혈당 관련 수치는 당뇨병 진단을 받은 집단이 좀 더 높은 값에 분포**해 있다.
- `HDL`의 경우 **당뇨병 진단을 받은 데이터의 고밀도 콜레스테롤(HDL)이 더 낮은 값에 분포**해 있다.

### 각 피처별 분포도

![image](https://user-images.githubusercontent.com/38115693/147485404-fa76fccc-bf2c-4350-9514-a6b4a38dfbd5.png)

- 이상치로 보이는 값들이 존재하지만, 조사 결과, **이러한 수치들 또한 의미가 있는 것으로 판단되어 제거하지 않고 그대로 사용하는 것으로 결정**하였다.
  - 예를 들어, TG가 1000mg/dL이 넘는 경우는 심한 고중성지방혈증으로 췌장염 발생의 위험이 증가하는데, 고중성지방혈증 환자 다수가 당뇨와 고혈압 등 대사성질환을 함께 가진 경우가 많다.

### 피처별 상관관계

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147489463-6a5c8922-0b9a-4693-b00a-bde84458eebd.png" width="75%" height=""></p>

아래의 변수들간 강한 양의 상관관계(0.7<=r)를 보인다.
- `Wt-Ht`
- `BMI-Ht`
- `DBP-SBP`
- `LDL-TC` (매우 강한 상관관계, 0.9<=r)
- `ALT-AST`

비교적 강한 음의 상관관계(0.5<=r<0.7)를 보이는 변수들은 아래와 같다.
- `CrCl-Cr`

### 로지스틱 회귀분석

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/148719024-157c2b26-9378-4422-bd92-23ab280bc64f.png" width="55%" height=""></p>

- labels에 대하여 연속형 독립변수들로 **로지스틱 회귀분석** 수행
  - **회귀계수(coef)**의 오즈비 출력 결과, `HbA1C`가 15.9698로 가장 큰 값으로 나타나며, 당뇨병 발병에 가장 큰 영향을 준다고 볼 수 있다. 이는, HbA1c가 1 증가할 때마다 당뇨병 진단 확률이 15.9698배 증가한다는 것이다.
  - 독립변수의 **유의확률(P>|z|)**을 보면, `age, HbA1c, FBG, TC, ALP` 변수들이 통계적으로 유의한 것으로 나타난다.

### VIF(Variance Inflation Factor)

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/148717942-abe8e428-9672-43ea-bfd1-8001a1bcfa21.png" width="15%" height=""></p>

- **VIF를 통해 다른 독립변수에 의존하는 가장 의존적인 변수 조회**
  - 각 변수별로 VIF가 10 이상인 경우에 다중공선성이 있다고 판단할 수 있다. Ht, TC, Alb, BMI, Wt, HbA1c 등이 특별히 높은 VIF 값을 가지며, 다른 독립변수들에 의존적인 변수들임을 의미한다.
  - VIF 값이 가장 큰 변수들 중 Ht, Wt 그리고 TC와 Alb도 순차적으로 제외하여 VIF 값 변화량을 확인했고, 이후 모델링 과정에서 추가적인 전처리를 시도할 때 참고하였다.

### 당뇨병 진단 데이터 특성 조회

- 당뇨병 진단을 받은 데이터(labels=1)에 대한 특성들을 살펴보았으며, 종속변수와의 상관관계가 높아보이는 독립변수들 위주로 조회하였다.

**당뇨병 진단을 받은 사람들의 성별 조회**

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147491151-79f0adea-648e-4b2c-86f8-fee3919649b1.png" width="40%" height=""></p>

- 여성보다 남성이 더 많다.

**당뇨병 진단을 받은 사람들의 연령 조회**

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147491301-bd7bfad2-f3cc-466f-afb7-cb2b8199839b.png" width="40%" height=""></p>

- 연령대로 구분하여 범주화한 후 표현하였다. 연령대가 높은 순서대로 많은 빈도수를 보인다.

**당뇨병 진단을 받은 사람들의 체질량지수(BMI) 조회**

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147491478-b46878e6-6bb3-4daf-a78d-3b2653b8f9de.png" width="40%" height=""></p>

- 상위 15개 수치를 조회한 것인데, 23 이상의 수치에 대한 빈도수가 높다. 23이상이면 비만 전단계이고, 25이상부터 비만으로 부른다. 

**당뇨병 진단을 받은 사람들의 당화혈색소(HbA1c) 조회**

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147493085-0e9a450d-dabf-4691-a8c5-9fede6ff6730.png" width="40%" height=""></p>

- 상위 15개 수치 값 조회 결과, HbA1c의 5.7 이상의 빈도수가 많은 것으로 나타난다. 5.7-6.4%는 당뇨 전단계로 부르며, 6.5% 이상은 당뇨로 진단한다.

**당뇨병 진단을 받은 사람들의 공복혈당(FBG) 조회**

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147493131-86f270cb-f369-4e4f-b4c8-590a29fa5e8e.png" width="40%" height=""></p>

- 상위 15개 수치 값 조회 결과, 100 이상의 수치 값들에 대한 빈도수가 많다. 100-125는 공복혈당장애(당뇨병 전단계)이며, 126 이상은 당뇨병으로 진단한다.

### 결측치 처리

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147493976-370db9bb-482e-4367-a416-b4b531f6383e.png" width="30%" height=""></p>

- `PR, TG, LDL, HDL, Alb, ALP` 피처에서 결측치 확인
  - PR의 경우 age 피처를 연령대별로 나누어 범주화한 피처를 사용하여, 동일한 연령대 PR의 평균값으로 대체
  - TG의 경우 총 콜레스테롤(TC) 산식(TC = LDL + HDL + TG/5)을 이용해 역산을 통해 TG를 계산
  - Index 254번 데이터는 TG, LDL, HDL, Alb, AlP 모두 Null값이어서 해당 row 전체를 삭제

### 각 검사 수치에 대한 범주형 컬럼 추가 생성

![image](https://user-images.githubusercontent.com/38115693/147495420-d4b0e495-a424-4c63-afba-1a8057e99f16.png)

- 각 검사항목별로 **정상 또는 판단 기준 범위에 따라 나누고 그룹화한/범주화한 파생 변수를 생성**하였다.
- 추가적으로
  - 맥압, BUN/Cr 비율, AST/ALT 비율 등 **당뇨병 진단과 밀접하게 관련된 다른 검사에 대해서도 조사하여 산식을 적용하여 범주화 된 변수를 생성**하였다.
  - DLP(이상지질혈증), MS(대사증후군) 등 **당뇨로 발생 할 수 있는 질병과 합병증에 대한 정보도 확인하여 관련 산식을 적용하여 생성**하였다.

---

```
# 참고: 프로젝트에 대한 자세한 overview는 첨부된 PROJECT_OVERVIEW.md 파일을 확인 바랍니다.
```

## 모델링<a class="anchor" id = "c4"> </a>

### 모델링 과정

![image](https://user-images.githubusercontent.com/38115693/147495960-f9e2e82c-6d3d-4d84-a875-f63e3d33732a.png)

모델링은 크게 세 가지 과정을 거친다:
  1. 데이터 전처리
  2. Imbalanced 데이터 처리를 위한 오버샘플링
  3. 파라미터 튜닝

### 사용한 데이터 처리 기법 및 학습/예측 모델

![image](https://user-images.githubusercontent.com/38115693/147496168-a3211c99-e055-4805-bbf3-1771d3072fcf.png)

1. 범주형 데이터를 사용한 모델링시 인코딩은 **Label Encoding**과 **One-Hot Encoding**을 각각 사용하였고, 연속형 데이터만으로 **Standard Scaling**을 적용하여 모델링
2. Label 2437개 중 0: 2231개 / 1: 206개의 불균형 데이터이기 때문에 불균형 데이터 처리를 위해 리샘플링을 하였고, 데이터 양이 많지 않아 **오버샘플링** 사용
3. DecisionTree, KNN, LogisticRegression, RandomForest, XGBoost, SVM 분류기 등 + 비교용의 MLP 모델을 포함하여 총 9개의 모델을 사용해서 학습과 모델링

### 세부 모델링 과정

#### 1. 데이터 전처리

![image](https://user-images.githubusercontent.com/38115693/147497046-b62286eb-5ead-44c8-9515-808e3f3152ab.png)

- 모델링은 3가지로 나눠서 접근해 시도하였다.
  - 기존의 각 검사수치 변수(연속형)들을 그룹핑하고 범주화한 범주형 변수들로에 대해 **(1) Label Encoding**과 **(2) One-Hot Encoding**을 각각 적용하여 모델링
  - 마지막으로, 기존의 연속형 변수들만을 사용하여 **(3) Standard Scaling** 적용 후 모델링

#### 2. 오버샘플링

![image](https://user-images.githubusercontent.com/38115693/147497557-b2dab919-761d-4e4f-bd84-620556ee9de4.png)

- 오버샘플링은 5가지 기법을 사용하였으며, 적용 대상 데이터셋의 특성(범주형, 연속형, 범주형+연속형)에 맞춰 적절한 기법을 사용했다.
  1. `Random Oversampling(ROS)`: 기존에 존재하는 소수의 클래스(Minority)를 복제하여 비율을 맞춰주는 기법으로, 숫자가 늘어나기 때문에 더 많은 가중치를 받게 되는 원리
  2. `SMOTE`: 임의의 소수 클래스 데이터로부터 인근 소수 클래스(minor class) 사이에 새로운 데이터를 생성하는 기법
  3. `ADASYN`: Borderline-SMOTE에서 조금 더 변주를 준 알고리즘으로, 인접한 다수 클래스의 비율에 따라 가중치를 줘 SMOTE를 적용시키는 방식
  4. `SMOTE-NC`: SMOTE가 수치형/연속형 데이터로만 이루어진 데이터에 적합한 반면, SMOTE-NC는 범주형과 수치형이 믹스된 데이터에 적용할 수 있는 기법
  5. `SMOTE-N`: SMOTE-N은 범주형으로만 이루어진 데이터에 적합한 SMOTE 기법

#### 3. 하이퍼파라미터 튜닝

![image](https://user-images.githubusercontent.com/38115693/147499588-35f33d6b-5fb9-4902-93bf-a9c3bdb873e1.png)

- 각 전처리 및 오버샘플링 과정별로 하이퍼파라미터 튜닝을 진행하였는데, DecisionTree와 KNN을 베이스 모델로 시작하여 다른 여러 모델들을 시도해 보면서 **성능을 비교하며 파라미터 옵션을 추가하거나 값을 변경**했다.
- **암 진단과 같이 당뇨병 진단도 실제 양성을 양성으로 예측하는 것이 중요**하다고 판단하여, **accuracy(정확도)와 함께 recall(재현율) 예측률을 높이는 것에 중점**을 두어 파라미터 튜닝을 진행했다.

![image](https://user-images.githubusercontent.com/38115693/147500056-cbd7a551-021a-4775-8f66-d14874de4910.png)

- 이후, 각 과정별 성능이 좋은 모델을 선별하여 교차검증과 GridSearchCV를 사용하여 최적의 파라미터를 찾아보았다.
- 성능을 테스트해 가며 파라미터 옵션이나 값을 추가하거나 변경하였다.
- 하지만 **기대했던 좋은 결과를 얻지 못 하여, 주요 모델에 대해 GridSearchCV에 구체적인 평가(evaluatoin) 메트릭스를 단일과 다중으로 지정하여서 파라미터 튜닝 시도했다.

![image](https://user-images.githubusercontent.com/38115693/147500254-bc1d381d-6bd5-4cb6-865d-cc6e9479a1ff.png)

- 그럼에도 기대했던 좋은 결과를 얻지는 못하였다. Accuracy에 대해선 높은 결과를 얻을 수 있었지만, accuracy와 recall 모두 좋은 성능을 보이는 모델을 찾기는 쉽지 않았다.
- 직접 튜닝을 했을 때의 결과가 더 이상적이었기 때문에, 결국 직접 튜닝해 가며 여러 시나리오별로 학습과 테스트를 진행하였다.
- 그리고 **여러 evaluation metrics로 평가해 mean값을 정리**해 주고자 cross_val_score 모듈을 사용하지 않고, **Stratified K-Fold와 반복문을 사용해 index를 반환받아 교차 학습 및 평가를 진행**하였다.
  - 각 모델별로 평가 지표(accuracy, precision, recall, f-1, roc-auc)의 **평균 값으로 모델 성능을 평가**하였다.
  - 이와 같이 진행하며, accuracy와 recall에 대한 성능을 높여나갔다.

![image](https://user-images.githubusercontent.com/38115693/147502491-7d5359ca-5468-4df2-b4df-99d05f03380a.png)

---

```
# 참고: 프로젝트에 대한 자세한 overview는 첨부된 PROJECT_OVERVIEW.md 파일을 확인 바랍니다.
```

## 모델링 과정 및 결과<a class="anchor" id = "c5"> </a>

---
### I. 범주형 데이터 기준 모델링

**모델링 내용**
1. One-Hot Encoding 적용
2. 범주형+연속형 데이터에 적합한 SMOTE-NC와 RandomOversampling로 오버샘플링

**모델링 결과**

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147502365-93d6dfdc-13af-4d72-bcc2-f4812c19e3ea.png" width="40%" height=""></p>

---
### II. 기존 연속형 데이터 기준 모델링

### 1. Trial 1

**모델링 내용**
1. gender, age 피처에 대해 One-Hot Encoding을 적용
2. 기존 연속형 변수들에 대해 Standard Scaling을 적용 (Data Leakage를 피하기 위해 train-test split 이후 적용)
3. 범주형+연속형 데이터에 적합한 SMOTE-NC와 RandomOversampling로 오버샘플링

**모델링 결과**

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147503805-fc4534c4-4bc3-454a-b1fb-79cc92202e5b.png" width="75%" height=""></p>

- Standard Scaling을 적용한 두 모델 모두 성능은 비슷하게 나타났다.
- **Standard Scaling을 적용한 두 결과 모두 범주화한 데이터셋을 사용하여 모델링한 결과보다 성능이 더 좋게 나타났다.**

### 2. Trial 2

**모델링 내용**
- 상관관계가 높은 Wt(몸무게), Ht(키) 변수 제외
- 나머지는 Trial 1과 동일하게 학습과 테스트를 진행

**모델링 결과**

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147504188-68227819-e075-4056-989c-174eb6976814.png" width="75%" height=""></p>

- Wt, Ht 피처들을 제외한 두 모델도 구간으로 나누어 범주화한 데이터셋을 사용하여 모델링한 결과보다는 예측 성능이 더 좋은 것으로 나타났다.
- Wt, Ht를 포함하여 모델링 했을 때의 결과와 비교하면, accuracy 결과는 비슷하지만 recall은 Wt, Ht 피처들을 포함했을 때의 결과가 더 낫다. 따라서, **Wt, Ht 피처들을 포함하는 경우 더 좋은 모델로 학습이 가능**하다.

### 3. Trial 3

**모델링 내용**
1. 기존 연속형 피처들을 Standard Scaling을 적용하는 것에 age 피처를 포함하여 진행 
  - gender 피처에 대해서만 One-Hot Encoding 적용
  - age 피처를 Standard Scaling 과정에 포함하여 다른 연속형 변수들과 함께 Standard Scaling 적용
2. 다시 Wt, Ht 피처들을 포함하여 진행
3. 범주형+연속형 데이터에 적합한 SMOTE-NC와 RandomOversampling로 오버샘플링

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147504845-ca463740-bcfd-4eb4-9f09-9d6a08092a8b.png" width="75%" height=""></p>

- 모델링 결과, 마지막 모델이 가장 좋은 예측 성능을 보여줬다.

---
### 변수 중요도 확인

**RandomForest의 Feature Importances**

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147505056-2387a2e8-3405-4b62-baf3-ca0748616b6d.png" width="50%" height=""></p>

- RandomForest의 Feature Importances로 변수 중요도 확인 결과, `FBG, HbA1c, GGT, ALP, BMI, Wt` 등이 당뇨병 진단 예측에 높은 중요도를 가지는 것으로 나타났다.

**Permutation Importance**

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147505301-bdd4fd36-1e3f-4523-8b52-c6fcfbdec4de.png" width="50%" height=""></p>

- Permutation Importance로 당뇨병 진단 예측에 있어 변수 중요도 확인 결과, `FBG, HbA1c, BMI, age, Wt, gender_F, ALP, GGT` 등의 순서로 변수 중요도가 높다. 이 중, `FBG, HbA1c, age, GGT, ALP` 피처들은 모두 회귀분석 결과 통계적으로 유의했던 변수들이기도 하다.

---
## 결론 <a class="anchor" id = "conclusion"> </a>

- 변수 중요도 결과들을 종합하면, **당뇨병 진단에 있어 공복시혈당(FBG), 당화혈색소(HbA1c), 체질량지수(BMI), 몸무게(Wt), 나이(age), 감마글루타밀전이효소(GGT), 알칼라인산분해효소(ALP) 수치가 중요한, 유의한 연관성이 있는 변수**인 것으로 보인다. 그렇다면, **당뇨병 진단 리스크에 대한 사전 예측과 이러한 수치들에 대한 적절한 관리를 통해 당뇨병을 예방하고 코로나19에 대한 취약성 또한 감소**시킬 수 있을 것이라 생각한다.
- 당뇨병 치료에 새로운 가능성을 열어준 인슐린이 발견된지 100년의 시간이 흘렀지만, 여전히 당뇨병에 대한 두려움은 크다. 고령화가 심화되면서 당뇨병 환자의 수는 증가하고 있고, 코로나19로 인해 당뇨병에 대한 위험 요인 또한 늘어났으며, 무엇보다 당뇨병 환자들은 큰 위협을 받고 있다. 그러니 이 코로나 시대에, 모두 경각심을 갖고 당뇨병 리스크를 사전에 파악하고, 이에 따른 당뇨병 자가 관리를 해 나가는 것이 그 어느 때 보다 필요하다.

---
## 한계 및 향후 과제<a class="anchor" id = "c6"> </a>

- 도메인 지식을 더 쌓아, 더 심도 깊은 분석과 모델링을 시도해 보겠다.
- 온라인 자료, 연구/학술자료, 또 분야 별로 검사하고 진단하는 수치들에 대한 판단 기준이 다른 경우가 많았다. 이에 따라, 변수들에 대한 범위를 나누고 범주화 하는 과정에서 기준 값을 잡는 것에 어려움이 있었다. 이에 대한 연구를 더 진행하여, 더 구체적인 기준을 잡아 모델링을 진행해 보겠다.
- 향후엔 성별과 연령대에 따른 더 세분화 된 분류 기준을 활용하고 적용하여 학습과 모델링을 해 보겠다. 더 세분화 한다면, 더 구체적인 기준들을 적용한다면 더 성능 좋은 모델이 만들어질 것으로 기대한다.
- 그리고 데이터가 불균형적이고, 범주형 피처와 연속형 피처가 섞여 있는 데이터를 처리하는 데에 더욱 효과적이고 적합한 기법(리샘플링, 차원축소 등)들에 대해 더 연구해 보고, 향후 적용과 모델 업그레이드를 해 보겠다.
