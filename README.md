# 머신러닝 기반 당뇨병 발병 사전 예측 모델
### 실제 임상데이터(Real World Data, RWD)를 활용한 당뇨병 발병 사전 예측 모델 개발

---

## 목차
* [1. 프로젝트 배경](#c1)
* [2. 데이터 소개](#c2)
* [3. EDA 및 전처리](#c3)
* [4. 모델링](#c4)
* [5. 모델링 결과](#c5)
* [6. 한계 및 과제](#c6)

---
## 프로젝트 배경<a class="anchor" id = "c1"> </a>

11월의 두 번째 일요일은 국제당뇨병연맹(IDF)와 세계보건기구(WHO)가 정한 세계당뇨의날(World Diabetes Day)이다. 폐렴, 고혈압, 뇌졸증 등 유병률, 심각도 등에서 중요도가 큰 질환들은 모두 자기만의 기념일을 가지고 있다. 그만큼 당뇨병은 점점 유병률이 증가하고 우리 일상을 위협하는 심각한 질환이라는 의미이다.

'당뇨'란 혈액 속의 포도당 수치가 정상인보다 높은 상태를 말하며, 우리 몸이 섭취한 음식물을 에너지로 적절하게 사용되지 못 하고 포도당이 소변으로 배출된다고 하여 이름 붙여진 병이다. 정상인의 경우 소변으로 당이 넘쳐나지 않을 정도로 혈당이 조절된다. 여기에는 췌장에서 분비되는 '인슐린'이라는 호르몬이 중요한 작용을 한다. 이러한 인슐린이 모자라거나 제대로 일을 못 하는 상태가 되면 혈당이 상승하며, 이로 인해 혈당이 지속적으로 높은 상태가 된다. 이러한 상태를 당뇨병이라고 하는데, 이렇게 혈당이 높은 상태로 오랜 시간이 지나면 심근경색, 뇌졸중, 망막질환, 신장질환, 동맥경화와 같은 만성 합병증을 일으킬 수 있는 무서운 질환이다.

코로나19(코로나 바이러스) 이후 실내 활동이 증가하고, 일상 생활 활동량 감소, 운동 빈도와 운동량의 감소, 식이 변화 등 일상 생활에서의 많은 변화가 있었다. 장기화 된 코로나 상황 속에서, 대한비만학회의 '코로나19시대 국민 체중 관리 현황 및 인식 조사'에 따르면 10명 중 약 5명은 코로나 이후 뭄무게가 3kg 이상 증가한 것으로 나타났다. 또한, 많은 사람들이 재택 근무, 온라인 수업 등으로 불규칙적인 생활과 식습관으로 영양 불균형의 상태 등도 겪고 있다. 하지만 더 큰 문제는, 바로 이러한 모든 요인들이 당뇨 유병률을 증가시키는 요인이 된다는 것이다.

전 세계의 위협이 되고 있는 코로나19로 인해 당뇨병 환자들의 우려는 더욱 커졌다. 당뇨병 환자는 코로나19에 특히 더 취약하다. 당뇨병은 우리 몸의 면역체계를 무너뜨려 감염병에 취약하게 만들며, 특히 당뇨병 환자는 일반인에 비해 코로나19의 감염 위험이 1.2배 더 높아 더 쉽게 감염 될 수 있다고 한다. 또한, 당뇨병은 만성질환 중에서도 가장 코로나19의 예방에 주의를 기울여야 하는 것으로 나타났는데, '코로나19에 어떤 사람들이 더 위험한가?'라는 질문에 미 질병통제예방센터(CDC)는 “지금까지의 연구 결과에 의하면 65세 이상의 노인, 장기요양시설 생활자, 만성 폐질환, 천식, 비만, 당뇨병 등 기저질환을 가진 사람들에게 더 위험할 수 있다”고 답했다. 실제로 일반인에 비해 당뇨병 환자가 코로나19에 감염됐을 경우 예후가 나쁜 것으로 알려져 있다. 대한당뇨병학회에 따르면 국내 코로나19 환자의 14.5~21.8%가 당뇨병 환자였고, 국내 5천여명의 코로나19 환자를 대상으로 한 연구에 따르면 당뇨병 환자가 코로나19 감염 시 기계호흡이 필요한 경우는 1.93배, 사망률은 2.66배 높았다. 또한, 인슐린 치료를 받는 당뇨병 환자들은 감염 위험이 25% 증가했다. 미국의 경우 코로나19 감염증 사망자 중 40%가 당뇨병 환자였다는 한 연구 결과도 나왔다.

그렇기에 코로나19 시대의 당뇨병 자가관리는 더욱 중요해졌다. 특히 당뇨병에 취약한 한국인의 특성을 고려할 때, 만약 자기의 건강상태와 당뇨병 위험을 사전에 예측 할 수 있다면, 당뇨병으로 진행되는 것을 적절한 사전 대응과 신체 및 혈당 관리를 통해 예방 할 수 있을 것이다. 이는 나아가 코로나19 감염을 예방하고 발생률 감소에도 영향을 줄 수 있을 것이며, 코로나19로 인한 중증도와 사망률 또한 감소시킬 수 있을 것이다. 그것을 목적으로, 이 프로젝트를 통해 머신러닝과 실제 진료 데이터를 활용하여 당뇨병 진단에 대한 사전 예측 모형을 개발하게 되었다.

---
## 데이터 소개<a class="anchor" id = "c2"> </a>
당뇨병 사전 진단 예측 모델링을 위해 당뇨병 관련 실제 임상데이터(Real World Data, RWD)를 확보하여 사용하였다. 데이터셋은 성별, 나이 등 환자에 대한 기본 정보와 당뇨병 진단 여부, 그리고 혈압, 혈당, 콜레스테롤, 간, 신장 등과 관련된 여러 검사 수치에 대한 데이터로 이루어져 있다.

총 2,438개의 행과 26개의 컬럼/피처로 구성되어 있는데, 이 중 당뇨병 진단을 받은 데이터가 206개인 **불균형 데이터**이다.

---
## EDA 및 전처리<a class="anchor" id = "c3"> </a>

### 각 피처별 분포도

![image](https://user-images.githubusercontent.com/38115693/147487886-2d334533-b961-4329-b518-6b92a723abad.png)

각 피처별 분포도 조회 결과, age, Wt, BMI, SBP, PR 등 일부 피처들을 제외한 대부분의 피처가 정규성을 띄고 있는 것으로 보인다. 하지만 Cr, AST, ALT, GGT, ALP 등이 왼쪽으로 치우친 분포를 보인다.

### 라벨별 각 피처 분포도
![image](https://user-images.githubusercontent.com/38115693/147484996-1f8a17f3-2d3a-4ee3-af73-69b5245a755d.png)

종속변수인 labels별(당뇨병 진단을 받은 경우 1, 아닌 경우 0) 각 피처의 분포도 확인 결과, 많은 변수들이 당뇨병 진단 여부와 상관없이 비슷한 분포를 띄고 있는 것처럼 보인다. 그 중에서 눈에 띄는 것은 혈당과 관련 된 피처들인 HbA1c, FBG, HDL 등인데, 혈당 관련 수치는 당뇨병 진단을 받은 집단이 좀 더 높은 값에 분포해 있는 것으로 보인다.

실제로 각 라벨별 피처의 평균값을 계산해 보면, 대부분의 피처에서 당뇨병 진단을 받은 데이터인 labels 1의 평균 수치가 더 높게 나타지만, HDL의 경우 labels 0이 55.5로 labels 1의 49.8에 비해 더 높은 평균 수치를 가지고 있다. 당뇨병 진단을 받은 데이터의 고밀도 콜레스테롤(HDL)이 낮은 값에 분포해 있는데, 이 수치가 낮을 수록 저밀도 콜레스테롤 (LDL)을 잘 배출하지 못하게 된다. 이로 인해, 산화된 LDL이 혈전이 발생하여 혈압이 증가하고 모세혈관 괴사가 발생 할 수 있다.

### 각 피처별 분포도

![image](https://user-images.githubusercontent.com/38115693/147485404-fa76fccc-bf2c-4350-9514-a6b4a38dfbd5.png)

각 피처별 분포도를 보면 대부분의 피처들에 이상치로 보이는 값들이 존재한다. 하지만 조사 결과, 이러한 수치들 또한 의미가 있는 것으로 판단되어 제거하지 않고 그대로 사용하는 것으로 결정하였다. 예를 들어, TG가 1000mg/dL이 넘는 경우는 심한 고중성지방혈증으로 췌장염 발생의 위험이 증가하는데, 고중성지방혈증 환자 다수가 당뇨와 고혈압 등 대사성질환을 함께 가진 경우가 많다.

### 피처별 상관관계

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147489463-6a5c8922-0b9a-4693-b00a-bde84458eebd.png" width="75%" height=""></p>

아래의 변수들간 강한 양의 상관관계(0.7<=r)를 보인다.
- Wt-Ht
- BMI-Ht
- DBP-SBP
- LDL-TC (매우 강한 상관관계, 0.9<=r)
- ALT-AST

비교적 강한 음의 상관관계(0.5<=r<0.7)를 보이는 변수들은 아래와 같다.
- CrCl-Cr

### 로지스틱 회귀분석

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/148719024-157c2b26-9378-4422-bd92-23ab280bc64f.png" width="55%" height=""></p>

labels에 대하여 연속형 독립변수들로 로지스틱 회귀분석을 실시한 결과:
- 결정계수(R-sqaured)는 전체 데이터 중 해당 회귀모델이 설명 할 수 있는 데이터의 비율, 회귀식의 설명력을 나타내는데(1에 가까울수록 높은 설명력), 여기선 0.3707로 모형적합도는 낮은 편이다. 하지만 로지스틱 회귀분석에서는 보통 R제곱값은 낮게 나오기 때문에, R제곱에 의존할 필요는 없다고 본다.
- 회귀계수(coef)의 절대값으로 미루어보면 HbA1c가 2.7707으로 가장 높다. 오즈비 출력 결과, HbA1C가 15.9698로 역시 가장 큰 값으로 나타나며, 당뇨병 발병에 가장 큰 영향을 주는 것임을 알 수 있다. 즉, HbA1c가 1 증가할 때마다 당뇨병 진단 확률이 15.9698배 증가한다는 것이다.
- z-statistic 결과, 독립변수와 종속변수 사이의 상관관계를 의미하는 z 값(값이 클수록 상관도가 큼)이 상대적으로 큰 변수들로는 age, HbA1c, FBG, TC, ALP 등으로 나타나는데, 독립변수의 유의확률(P>|z|)을 보면, 이 중 age, HbA1c, FBG, TC, ALP 변수들이 통계적으로 유의한 것으로 나타난다(0.05보다 작으면 유의미).

### VIF(Variance Inflation Factor)

VIF란 독립변수를 다른 독립변수로 선형회귀한 성능을 나타내며, 다른 독립변수에 의존하는 가장 의존적인 변수를 찾을 수 있다 (다른 변수에 의존적일 수록 VIF가 커진다).

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/148717942-abe8e428-9672-43ea-bfd1-8001a1bcfa21.png" width="15%" height=""></p>

- 각 변수별로 VIF가 10 이상인 경우에 다중공선성이 있다고 판단할 수 있다. 4개 변수를 제외한 대부분의 변수들이 10 이상의 VIF 값으로 나타나는데, 이 중, Ht, TC, Alb, BMI, Wt, HbA1c 등이 특별히 높은 VIF 값을 가진다. 다른 독립변수들에 의존적인 변수들임을 의미한다.

이에 따라, VIF 값이 가장 큰 변수들 중 Ht, Wt를 제외하고 VIF 값의 변화량을 보았고, 또 TC와 Alb도 순차적으로 제외해 가며 VIF를 다시 계산하였다. 이후 모델링 과정에서 추가적인 전처리를 시도할 때, 확인한 VIF를 참고하였다.

### 당뇨병 진단 데이터 특성 조회

이어서, 당뇨병 진단을 받은 데이터(labels=1)에 대한 특성들을 살펴보았으며, 종속변수와의 상관관계가 높아보이는 독립변수들 위주로 조회하였다.

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

**당뇨병 진단을 받은 사람들의 총 콜레스테롤(TC) 조회**

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147493176-e520f3d7-9a49-474b-99bc-a838d1c101fa.png" width="40%" height=""></p>

**당뇨병 진단을 받은 사람들의 감마글루타밀전이효소(GGT) 조회**

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147493255-adcfa5d1-8a7d-4345-b267-4d3fd839d64c.png" width="40%" height=""></p>

**당뇨병 진단을 받은 사람들의 알칼라인산분해효소(ALP) 조회**

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147493284-2dac9629-2ca4-4dba-9964-f6db2e9d1db8.png" width="40%" height=""></p>

### 결측치 처리

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147493976-370db9bb-482e-4367-a416-b4b531f6383e.png" width="30%" height=""></p>

결측치 조회 결과 PR, TG, LDL, HDL, Alb, ALP 피처에서 결측치가 확인 되었으며, 아래와 같이 처리하였다.
- PR의 경우 age 피처를 연령대별로 나누어 범주화한 피처를 사용하여, 동일한 연령대 PR의 평균값으로 대체하였다. 
- TG의 경우 총 콜레스테롤(TC) 산식(TC = LDL + HDL + TG/5)을 이용해 역산을 통해 TG를 계산하여 채웠다.
- Index 254번 데이터는 TG, LDL, HDL, Alb, AlP 모두 Null값이어서 해당 row 전체를 삭제하였다.

### 각 검사 수치에 대한 범주형 컬럼 추가 생성

![image](https://user-images.githubusercontent.com/38115693/147495420-d4b0e495-a424-4c63-afba-1a8057e99f16.png)

각 검사항목별로 정상 또는 판단 기준 범위에 따라 나누고 그룹화한/범주화한 파생 변수를 생성하였다.

추가적으로, 맥압, BUN/Cr 비율, AST/ALT 비율 등 당뇨병 진단과 밀접하게 관련된 다른 검사에 대해서도 조사하여 산식을 적용하여 범주화 된 변수를 생성하였고, DLP(이상지질혈증), MS(대사증후군) 등 당뇨로 발생 할 수 있는 질병과 합병증에 대한 정보도 확인하여 관련 산식을 적용하여 생성하였다.

---
## 모델링<a class="anchor" id = "c4"> </a>

### 모델링 과정

![image](https://user-images.githubusercontent.com/38115693/147495960-f9e2e82c-6d3d-4d84-a875-f63e3d33732a.png)

모델링은 크게 세 가지 과정을 거친다.
1. 데이터 전처리
2. Imbalanced 데이터 처리를 위한 오버샘플링
3. 파라미터 튜닝

### 사용한 데이터 처리 기법 및 학습/예측 모델

![image](https://user-images.githubusercontent.com/38115693/147496168-a3211c99-e055-4805-bbf3-1771d3072fcf.png)

1. 범주형 데이터를 사용한 모델링시 인코딩은 **Label Encoding**과 **One-Hot Encoding**을 각각 사용하였고, 연속형 데이터만으로 **Standard Scaling**을 따로 적용하여서도 모델링해 보았다.
2. Label 2437개 중 0: 2231개 / 1: 206개의 불균형 데이터이기 때문에, 불균형 데이터 처리를 위해 리샘플링을 하였는데, 데이터 양이 많지 않아 오버샘플링을 하기로 결정하였다.
3. DecisionTree, KNN, LogisticRegression, RandomForest, XGBoost, SVM 분류기 등 9개의 모델을 사용해서 학습과 모델링을 진행하였다.

### 세부 모델링 과정

#### 1. 데이터 전처리

![image](https://user-images.githubusercontent.com/38115693/147497046-b62286eb-5ead-44c8-9515-808e3f3152ab.png)

모델링은 3가지로 나눠서 접근해 시도하였다.

우선, 기존의 각 검사수치 변수(연속형)들을 그룹핑하여 범주화하였고, 해당 범주형 변수들로만 학습/예측 모델링을 시도했다. 범주형 데이터 처리를 위해 인코딩을 하였는데, 아래와 같은 이유로 Label Encoding과 One-Hot Encoding을 각각 진행하게 되었다:
1. 데이터를 그룹화 하여 나눠 놨지만, 레이블 인코딩을 했을 때 각각의 수치 값이, 예를 들어, 정상 미만(0), 정상(1), 정상 이상(2) 등과 같은 순서가 있는 데이터처럼 되었기에, 레이블 인코딩를 사용해도 각 수치 값의 의미가 보존되지 않을까 생각하여 레이블 인코딩도 진행하였다.
2. 선형 계열 모델(로직스틱회귀, SVM, 신경망 등)의 경우 숫자의 차이가 모델에 영향을 미치기 때문에, 레이블 인코딩된 결과에 이에 대한 영향이 있을 수도 있어 원핫인코딩 또한 별도로 적용하여 진행하였다.

마지막으로, 당뇨병에 대한 조사를 하면서, 각 검사 수치에 대한 판단 기준이 자료마다, 병원마다 달랐고, 따라서 조사한 것과 자료들을 기반으로 판단하여 범주화한 것이 예측 성능에 영향을 줄 수도 있을 것 같아 기존의 연속형 변수들만을 사용하여 Standard Scaling 적용 후 모델링하는 것 또한 시도하였다.

그리고 성능 테스트 과정에서 의미가 있을 것으로 판단되는 경우 범주화된 데이터셋에 일부 스케일링된 변수를 추가하거나, 반대로 스케일링된 데이터셋에 범주형 변수를 합쳐서도 시도하였으며, 불필요하다고 여겨지거나 상관관계가 높은 변수들을 빼보기도 하였다.

#### 2. 오버샘플링

![image](https://user-images.githubusercontent.com/38115693/147497557-b2dab919-761d-4e4f-bd84-620556ee9de4.png)

오버샘플링은 5가지 기법을 사용하였으며, 적용 대상 데이터셋의 특성(범주형, 연속형, 범주형+연속형)에 맞춰 적절한 기법을 사용했다.

1. `Random Oversampling(ROS)`: 기존에 존재하는 소수의 클래스(Minority)를 복제하여 비율을 맞춰주는 기법다. 숫자가 늘어나기 때문에 더 많은 가중치를 받게 되는 원리이다.
2. `SMOTE`: 임의의 소수 클래스 데이터로부터 인근 소수 클래스(minor class) 사이에 새로운 데이터를 생성하는 기법이다. 임의의 소수 클래스에 해당하는 관측치 X를잡고, 그 X로부터 가장 가까운 K개의 이웃을 찾아 그 사이에 임의의 새로운 X를 생성하는 데이터로부터 인근 소수 클래스 사이에 새로운 데이터를 생성한다. 
3. `ADASYN`: Borderline-SMOTE에서 조금 더 변주를 준 알고리즘으로, 인접한 다수 클래스의 비율에 따라 가중치를 줘 SMOTE를 적용시키는 방식이다.
4. `SMOTE-NC`: SMOTE가 수치형/연속형 데이터로만 이루어진 데이터에 적합한 반면, SMOTE-NC는 범주형과 수치형이 믹스된 데이터에 적용할 수 있는 기법이다.
5. `SMOTE-N`: SMOTE-N은 범주형으로만 이루어진 데이터에 적합한 SMOTE 기법이다.

#### 3. 하이퍼파라미터 튜닝

![image](https://user-images.githubusercontent.com/38115693/147499588-35f33d6b-5fb9-4902-93bf-a9c3bdb873e1.png)

각 전처리 및 오버샘플링 과정별로 하이퍼파라미터 튜닝을 진행하였는데, DecisionTree와 KNN을 베이스 모델로 시작하여, 다른 여러 모델들을 시도해 보면서 성능을 비교하며 파라미터 옵션을 추가하거나 값을 변경해 갔다.

암 진단과 같이 당뇨병 진단도 실제 양성을 양성으로 예측하는 것이 중요하다고 판단하여, **accuracy(정확도)와 함께 recall(재현율) 예측률을 높이는 것에 중점**을 두어 파라미터 튜닝을 진행하였다.

![image](https://user-images.githubusercontent.com/38115693/147500056-cbd7a551-021a-4775-8f66-d14874de4910.png)

이후, 각 과정별 성능이 좋은 모델을 선별하여 교차검증과 GridSearchCV를 사용하여 최적의 파라미터를 찾아보았다. 성능을 테스트해 가며 파라미터 옵션이나 값을 추가하거나 변경해 갔다. 

하지만 기대했던 좋은 결과를 얻지 못 하여, 주요 모델에 대해 GridSearchCV에 구체적인 평가(evaluatoin) 메트릭스를 단일 지정하여서 시도해 보고, 다중으로 지정하여서도 파라미터 튜닝을 시도해 보았다.

![image](https://user-images.githubusercontent.com/38115693/147500254-bc1d381d-6bd5-4cb6-865d-cc6e9479a1ff.png)

그럼에도 기대했던 좋은 결과를 얻지는 못하였다. Accuracy에 대해선 높은 결과를 얻을 수 있었지만, accuracy와 recall 모두 좋은 성능을 보이는 모델을 찾기는 쉽지 않았다. 직접 튜닝을 했을 때의 결과가 더 이상적이었기 때문에, 결국 직접 튜닝해 가며 여러 시나리오별로 학습과 테스트를 진행하였다.

그리고 여러 evaluation metrics로 평가해 mean값을 정리해 주고자 cross_val_score 모듈을 사용하지 않고, Stratified K-Fold와 반복문을 사용해 index를 반환받아 교차 학습 및 평가를 진행하였으며, 각 모델별로 평가 지표(accuracy, precision, recall, f-1, roc-auc)의 평균 값으로 모델 성능을 평가하였다. 이와 같이 진행하며, accuracy와 recall에 대한 성능을 높여나갔다.

![image](https://user-images.githubusercontent.com/38115693/147502491-7d5359ca-5468-4df2-b4df-99d05f03380a.png)


---
## 모델링 결과<a class="anchor" id = "c5"> </a>

### 각 수치를 구간별로 나눠 범주화 한 데이터 기준 모델링

우선 각 수치별로 기준 범위에 따라 구간으로 나누고 범주화 하여 생성한 데이터를 사용하였다.
- (1) One-Hot Encoding을 적용하고,
- (2) 별도로 범주화하지 않은 연속형으로 남아있는 Wt, Ht 피처들을 포함하여 그리고 포함하지 않고 Standard Scaling을 적용하여 합쳤다.
- (3) 이후, 오버샘플링으로 범주형+연속형 데이터에 적합한 SMOTE-NC와 RandomOversampling를 적용하였다.

테스트 결과 중, ROS을 적용했을 때의 모델의 예측 성능이 가장 좋았으며, (2) 연속형인 Wt, Ht를 제외하고, 범주화 한 피처들만을 사용했을 때가 결과적으로 더 나은, 아래와 같은 예측 성능을 가져왔다.

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147502365-93d6dfdc-13af-4d72-bcc2-f4812c19e3ea.png" width="40%" height=""></p>

One-Hot Encoding과 ROS를 적용한 테스트 결과는 평균적으로 이와 같은 예측 성능을 얻었다.
- Random Forest: accuracy 82%, recall 75%
- Logistic Regression: accuracy 79%, recall 74%
- SVM: accuracy 77%, recall 74%

### 기존 연속형 데이터 기준 모델링

기존 연속형 데이터 기준으로 Standard Scaling을 적용하여 모델링을 하였다.

- (1) 우선 gender, age 피처에 대해 One-Hot Encoding을 적용하고,
- (2) 'Data Leakage'를 피하기 위해 train-test split을 먼저 한 후, 기존 연속형 변수들에 대해 Standard Scaling을 적용하였다.
- (3) 마지막으로, oversampling(SMOTENC, RandomOversampling) 기법을 적용하고 모델 학습과 테스트를 진행한 결과는 아래와 같다.

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147503805-fc4534c4-4bc3-454a-b1fb-79cc92202e5b.png" width="75%" height=""></p>

SMOTE-NC를 적용했을 때에, 평균적으로 이와 같은 예측 성능을 얻었다.
- Logistic Regression: accuracy 83%, recall 79%
- SVM: accuracy 81%, recall 79%

Random Oversampling을 적용했을 때엔, 평균적으로 이와 같은 예측 성능을 얻었다.
- Logistic Regression: accuracy 83%, recall 80%
- SVM: accuracy 82%, recall 81%

Standard Scaling을 적용한 두 모델 모두 성능은 비슷하게 나타났으며, 두 결과 모두 구간으로 나누어 범주화한 데이터셋을 사용하여 모델링한 결과보다 성능이 더 좋게 나타났다.

**상관관계가 높은 변수 처리 후 재시도**

이어서 상관관계가 높은 변수를 처리한 후 다시 동일하게 학습과 테스트를 진행하였다.
- Wt(몸무게), Ht(키)간의 그리고 BMI(체질량지수)와 Ht간의 양적 상관관계가 높고, BMI에 이미 Wt, Ht가 사용되어 계산된 것이기 때문에 Wt, Ht 피처는 제외하였다.
- DBP(이완기혈압), SBP(수축기혈압)도 높은 양의 상관관계를 보이나, DBP와 SBP의 차이('맥압') 또한 의미가 있을 수 있다 생각되어 제외하지 않기로 하였다.
- TC(총 콜레스테롤)를 계산하자면 HDL+LDL+(TG/5)이며, LDL이 TC 계산에 포함되고 양적 상관관계 또한 높아 학습시 해당 변수를 제외할까 고민했지만, 이 계산식은 어디까지나 간이 계산법이며, 검사를 한 것이 보다 정확한 수치라고 한다 (콜레스테롤의 경우 오차범위가 큰 편이다). 따라서, TC, HDL(고밀도콜레스테롤), LDL(저밀도콜레스테롤), TG(중성지방) 각각의 수치가 가지는 의미나 영향이 있을 수 있다 생각되어, 제외하기 않고 사용하였다.
- ALT(알라닌아미노전이효소), AST(아스파르테이트아미노전달효소) 두 피처도 높은 양의 상관관계를 보이는데, AST/ALT 비율이 간 기능의 데미지를 파악하는 지표로도 사용되기에 제외하지 않고 사용하였다.
- CrCl(크레아티닌청소율)과 Cr(크레아티닌)은 비교적 강한 음의 상관관계를 보인다. Cr은 낮을수록, CrCl은 높을수록 좋은 것인데, Cr이 증가하면 CrCl은 감소한다. Cr과 CrCL 수치엔 연령, 체중, 성별 등의 변수도 영향을 주기에 두 피처 모두 그대로 포함하여 진행하였다.

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147504188-68227819-e075-4056-989c-174eb6976814.png" width="75%" height=""></p>

SMOTE-NC를 적용했을 때에, 평균적으로 이와 같은 예측 성능을 얻었다.
- Logistic Regression: accuracy 84%, recall 77%
- SVM: accuracy 82%, recall 77%

Random Oversampling을 적용했을 때엔, 평균적으로 이와 같은 예측 성능을 얻었다.
- Logistic Regression: accuracy 83%, recall 80%
- SVM: accuracy 82%, recall 82%

Wt, Ht 피처들을 제외한 두 모델도 구간으로 나누어 범주화한 데이터셋을 사용하여 모델링한 결과보다는 예측 성능이 더 좋은 것으로 보여진다. Wt, Ht를 포함하여 모델링 했을 때의 결과와 비교하면, accuracy 결과는 비슷하지만, recall은 Wt, Ht 피처들을 포함했을 때의 결과가 더 좋기 때문에, Wt, Ht 피처들을 포함하는 경우 더 좋은 모델로 판단된다.

다음으로, 기존 연속형 피처들을 Standard Scaling을 적용하는 것에 age 피처를 포함하여 진행하였다. 
- (1) gender 피처에 대해서만 One-Hot Encoding을 적용하고,
- (2) 이번엔 age 피처를 Standard Scaling 과정에 포함하여 다른 연속형 변수들과 함께 스케일링하여 진행하였다.
- (3) 그리고 앞서 설명한 과정과 동일한 과정을 거쳐 학습과 테스트를 진행하였으며, Wt, Ht 피처들을 포함하였을 때의 결과가 아래와 같다.

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147504845-ca463740-bcfd-4eb4-9f09-9d6a08092a8b.png" width="75%" height=""></p>

SMOTE-NC를 적용했을 때에, 평균적으로 이와 같은 예측 성능을 얻었다.
- Logistic Regression: accuracy 85%, recall 82%
- SVM: accuracy 84%, recall 82%

Random Oversampling을 적용했을 때엔, 평균적으로 이와 같은 예측 성능을 얻었다.
- Logistic Regression: accuracy 84%, recall 83%
- SVM: accuracy 83%, recall 82%

이는 앞서, 스케일링을 적용한 기존 연속형 변수들에 age 피처를 범주화 및 인코딩 과정에 포함시키고, Wt, Ht 피처들을 포함하여 모델링을 했을 때의 결과보다도 더 좋은 예측 성능을 보여준다.

### 변수 중요도 확인

**RandomForest의 Feature Importances**

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147505056-2387a2e8-3405-4b62-baf3-ca0748616b6d.png" width="50%" height=""></p>

RandomForest의 Feature Importances로 변수 중요도 확인 결과, FBG, HbA1c, GGT, ALP, BMI, Wt 등이 당뇨병 진단 예측에 높은 중요도를 가지는 것으로 나타났다.

하지만 RandomForest의 Feature Importances는 다소 편향성(bias)이 있는 것으로 알려져 있다. 특히, RandomForest는 연속형 변수 또는 카테고리 개수가 매우 많은 변수, 즉 ‘high cardinality’ 변수들의 중요도를 더욱 부풀릴 가능성이 높다고 한다. 'Cardinality'가 큰 변수일 수록, 노드를 나눌 것이 훨씬 더 많아서 노드 중요도 값이 높게 나오는 것으로 추측된다. 또한, 이 불순도를 기반으로 한 변수 중요도는 train 과정에서 얻은 중요도이기 때문에, test 데이터셋에서는 이 변수 중요도가 어떻게 변하는지 알 수 없다. 실제 test 데이터셋에서는 중요하지 않은 변수가 train 과정에서는 중요한 변수로 계산 될 수 있다. 따라서, RandomForest의 Feature Importances 외에 Permutation Feature Importance와 같은 다른 방법을 혼합해서 사용하는 것이 좋다.

**Permutation Importance**

Permutation Importance는 모델 예측에 가장 큰 영향을 미치는 피처를 파악하는 방법으로 훈련된 모델이 특정 피처를 사용하지 않았을 때 이것이 성능 손실에 얼마만큼의 영향을 주는지를 통해 그 피처의 중요도를 파악한다. 특히, Permutation Importance는 모델 훈련이 끝난 뒤에 계산 되기에 모델을 재학습 시킬 필요가 없으며, 어떤 모델이든 적용할 수 있는 것으로 알려져 있다.

<p align="center"><img src="https://user-images.githubusercontent.com/38115693/147505301-bdd4fd36-1e3f-4523-8b52-c6fcfbdec4de.png" width="50%" height=""></p>

Permutation Importance로 당뇨병 진단 예측에 있어 변수 중요도 확인 결과, FBG, HbA1c, BMI, age, Wt, gender_F, ALP, GGT 등의 순서로 변수 중요도가 높다. 이 중, FBG, HbA1c, age, GGT, ALP 피처들은 모두 회귀분석 결과 통계적으로 유의했던 변수들이기도 하다.

변수 중요도 결과들을 종합하면, 당뇨병 진단에 있어 공복시혈당(FBG), 당화혈색소(HbA1c), 체질량지수(BMI), 몸무게(Wt), 나이(age), 감마글루타밀전이효소(GGT), 알칼라인산분해효소(ALP) 수치가 중요한, 유의한 연관성이 있는 변수인 것으로 보인다. 그렇다면, 당뇨병 진단 리스크에 대한 사전 예측과 이러한 수치들에 대한 적절한 관리를 통해 당뇨병을 예방하고 코로나19에 대한 취약성 또한 감소시킬 수 있을 것이라 생각한다.

당뇨병 치료에 새로운 가능성을 열어준 인슐린이 발견된지 100년의 시간이 흘렀지만, 여전히 당뇨병에 대한 두려움은 크다. 고령화가 심화되면서 당뇨병 환자의 수는 증가하고 있고, 코로나19로 인해 당뇨병에 대한 위험 요인 또한 늘어났으며, 무엇보다 당뇨병 환자들은 큰 위협을 받고 있다. 그러니 이 코로나 시대에, 모두 경각심을 갖고 당뇨병 리스크를 사전에 파악하고, 이에 따른 당뇨병 자가 관리를 해 나가는 것이 그 어느 때 보다 필요하다.

---

## 한계 및 과제<a class="anchor" id = "c6"> </a>

![image](https://user-images.githubusercontent.com/38115693/147505395-b6e6d8e0-55d1-4983-b8eb-0cfb173ddd64.png)

1. 모델을 충분히 학습시키기에 데이터가 조금 부족했지 않나 생각 되었다. 만약 데이터를 더 확보 할 수 있었다면, 더 좋은 예측 모형을 만들 수 있었을 것 같다.
2. 데이터에 대한, 각 변수들에 대한 정보가 없어 일일이 조사하고 확인해 보았지만, 그럼에도 불구하고 결국 활용하지 못한 피처도 있어 아쉬움으로 남는다.
3. 셋째는 도메인 지식이다. 당뇨병에 대한 의료적인 지식이 부족했다는 점인데, 만약 더 깊은 도메인 지식이 있었다면, 더 심도 깊은 분석과 모델링을 시도해 볼 수 있지 않았을까 생각이 들었다.
4. 마지막으로, 온라인 자료, 연구/학술자료, 또 분야 별로 검사하고 진단하는 수치들에 대한 판단 기준이 다른 경우가 많았다. 이에 따라, 변수들에 대한 범위를 나누고 범주화 하는 과정에서 기준 값을 잡는 것에 어려움이 있었다.

![image](https://user-images.githubusercontent.com/38115693/147505585-0cc82c61-471a-4619-9ad5-6fa45dd10040.png)

1. 향후엔 성별과 연령대에 따른 더 세분화 된 분류 기준을 활용하고 적용하여 학습과 모델링을 해 보겠다. 더 세분화 한다면, 더 구체적인 기준들을 적용한다면 더 성능 좋은 모델이 만들어질 것으로 기대한다.
2. 그리고 데이터가 불균형적이고, 범주형 피처와 연속형 피처가 섞여 있는 데이터를 처리하는 데에 더욱 효과적이고 적합한 기법(리샘플링, 차원축소 등)들에 대해 더 연구해 보고, 향후 적용과 모델 업그레이드를 해 보겠다.

---

## 참고 자료

- https://www.amc.seoul.kr/asan/healthinfo/disease/diseaseDetail.do?contentId=31596
- https://www.kosso.or.kr/newsletter/202104/sub02.html
- https://www.hidoc.co.kr/healthstory/news/C0000633143
- https://www.joongang.co.kr/article/24109084#home
- https://kdca.go.kr/board/board.es?mid=a40303030000&bid=0034&act=view&list_no=716754
- https://www.e-jkd.org/upload/pdf/jkd-2020-21-1-27.pdf
- http://www.lecturernews.com
- https://www.koreascience.or.kr/article/JAKO200560537773551.pdf
- http://www.monews.co.kr/news/articleView.html?idxno=203842
- http://www.docdocdoc.co.kr
- https://ko.wikipedia.org/wiki/%EB%8B%B9%EB%87%A8%EB%B3%91
- https://smtmap.com/%EA%B0%84%EC%88%98%EC%B9%98/
- http://guro.kumc.or.kr/dept/main/index.do?DP_CODE=GRCP&MENU_ID=003036050045
- https://www.koreascience.or.kr/article/JAKO201354840931827.pdf
- https://www.schlab.org/guide/item/261/
- https://m.khan.co.kr/life/health/article/201511101537195#c2b
- http://seoulnim.com/news/lecture_v.asp?srno=7628&page=70&gubun=&keyword=
- https://blog.naver.com/PostView.naver?blogId=i-doctor&logNo=221450543662
- https://www.joongang.co.kr/article/21657194#home
- https://www.ibric.org/myboard/view.php?Board=review0&id=529&filename=bc0602.pdf&fidx=2&mode=down
- https://blog.naver.com/hyouncho2/60170417299
- https://www.paik.ac.kr/busan/medicine/disease_info_view.asp?p_sid=1040&p_cate=A
- https://www.cheric.org/PDF/PIC/PC19/PC19-2-0085.pdf
- https://labtestsonline.kr/tests
- https://m.amc.seoul.kr/asan/mobile/healthinfo/
- https://amc.seoul.kr/asan/healthinfo/
- https://kormedi.com/
- http://drug.co.kr/abbreviation/
- https://m.blog.naver.com/sorak123/222052778113
- http://guro.kumc.or.kr/
- https://medgongbu.tistory.com/92
- https://wyatt37.tistory.com/10
- http://www.koreanhypertension.org/
