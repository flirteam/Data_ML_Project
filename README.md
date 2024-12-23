# Data_ML_Project

[ML프로젝트 간이 절차]


[BMI DATA 확인]

1. 데이터 탐색 및 준비
* 데이터 확인: 741명의  키, 몸무게, BMI, 성별, 나이 등의 정보가 있음
* 결측치 처리: 데이터에서 누락된 값이 있는지 확인하고, 필요하면 채우거나 제거
* 데이터 변환: BMI 값에 따라 사용자들을 분류하거나, 나이, 성별, 체중 등을 바탕으로 새로운 피처를 생성할 수 있음.
* 관련 코드 부분 예시:https://www.kaggle.com/code/ahthneeuhl/bmi-data-analysis-visualization-and-predictions
* 

2. 운동 추천 기준 설정
* 운동 추천 로직: BMI와 같은 데이터를 기반으로 다음과 같은 운동을 추천할 수 있음.
    * 저체중: 체중 증가를 위한 근력 운동 + 고칼로리 식단.
    * 정상체중: 균형 잡힌 운동(유산소 + 근력 운동).
    * 과체중: 체중 감소를 위한 유산소 운동 중심 프로그램.
    * 비만: 저강도 유산소 + 식단 조절.
* 기타 기준: 성별, 나이, 활동 수준에 따라 추천을 세분화합니다.

3. 모델 개발
* 데이터 라벨링: 기존 데이터를 이용해 운동 추천을 위한 라벨을 추가. 예를 들어, "운동 유형" 컬럼에 "유산소", "근력", "혼합" 등의 값을 할당. 식단은 “채식”, “육식”
* 모델 학습:
    * 머신러닝 알고리즘(예: 분류 모델): 사용자 데이터를 입력하면 운동 유형을 예측하도록 학습.
    * 추천 시스템: 비슷한 BMI, 나이, 성별을 가진 사용자 그룹을 생성하고 운동과 식단을 추천.
 

4. 예측 및 평가
* 모델 테스트: 새로운 사용자 데이터를 입력해 운동 추천 결과를 확인할 예정.
* 모델 평가: 정확도, F1-score 등을 통해 추천 정확도를 평가할 예정.


아래는 딥러닝 모델과 관련된 내용을 중심으로 작성된 README 문서입니다. 프로젝트의 주요 딥러닝 관련 파일, 학습 및 배포 과정, 그리고 관련 내용이 포함되어 있습니다.

README: 딥러닝 기반 목표 예측 서비스
프로젝트 개요
이 프로젝트는 Feedforward Neural Network (FFNN) 기반으로 사용자의 목표 체중 달성일을 예측하는 딥러닝 모델을 구현하고 배포합니다. Google Colab에서 딥러닝 모델을 학습하였으며, Flask 및 Python 스크립트를 통해 예측 서비스를 제공합니다.

주요 기능
목표 체중 달성일 예측

기능: 사용자의 신체 정보(BMI, 체중, 활동량 등)를 바탕으로 딥러닝 모델이 목표 체중까지 소요되는 기간을 예측.
사용 데이터:
BMI 데이터 (체중, 키, 목표 체중)
사용자 활동 수준 (TDEE, BMR)
예측 결과:
json
코드 복사
{
  "username": "홍길동",
  "days_to_goal": 45,
  "message": "홍길동님, 목표 체중 달성 예상 소요 기간은 약 45일입니다."
}
딥러닝 모델 설계 및 학습

신경망 구조: Feedforward Neural Network (FFNN)
은닉층: [128, 64, 32]
활성화 함수: LeakyReLU
최적화 기법: Adam Optimizer
학습 데이터:
입력 데이터: 사용자의 나이, 키, 현재 체중, 목표 체중, BMI, TDEE 등
출력 데이터: 목표 체중 달성일까지 예상 소요 일수
하이퍼파라미터 탐색: Grid Search를 통해 최적 하이퍼파라미터를 선택.
모델 배포 및 운영

배포 방식:
Python 스탠드얼론 스크립트를 사용하여 모델 예측 수행.
Flask API 서버를 통해 RESTful 서비스로 배포 가능.
입력 방식: JSON 형식.
출력 방식: JSON 형식으로 예측 결과 반환.
프로젝트 파일 구조
plaintext
코드 복사
Project/
│
├── src/
│   ├── python/
│   │   ├── main_predictor.py         # 딥러닝 모델 기반 목표 예측 코드
│   │   ├── Data/
│   │   │   ├── feature_columns.json  # 모델 입력 피처 정보
│   │   │   ├── scaler.joblib         # 데이터 스케일링 파일
│   │   │   ├── P_model.pth           # 학습된 PyTorch 모델
│   │
│   ├── chatbot/
│   │   ├── chatbot_handler.py        # 챗봇 핸들러 코드
│   │   ├── sendbird_integration.py   # SendBird 플랫폼 연동
│   │   ├── gpt_integration.py        # OpenAI GPT API 호출 코드
│   │
├── data/
│   ├── bmi_data.csv                  # BMI 및 체중 데이터셋
│   ├── exercise.csv                  # 운동 추천 데이터셋
│   ├── food_data.csv                 # 식단 추천 데이터셋
│
├── requirements.txt                  # 필요 라이브러리 목록
└── README.md                         # 프로젝트 설명서
딥러닝 모델 설계
Feedforward Neural Network (FFNN)

입력층: 사용자 데이터를 기반으로 한 총 25개의 입력 피처
은닉층: [128, 64, 32]
활성화 함수: LeakyReLU
정규화: Batch Normalization 및 Dropout(0.2)
출력층: 1개의 예측값 (목표 달성일까지의 소요 기간)
최적화 및 손실 함수

최적화 기법: Adam Optimizer
손실 함수: Mean Squared Error (MSE)
하이퍼파라미터 탐색

탐색 기법: Grid Search
탐색 범위:
은닉층 크기: [128, 64, 32]
학습률: [0.01, 0.005]
배치 사이즈: [128, 256]
최적 결과:
은닉층: [128, 64, 32]
학습률: 0.005
배치 사이즈: 256
필요 라이브러리
requirements.txt 파일에서 다음 라이브러리 설치:

plaintext
코드 복사
torch==1.13.1
pandas==1.5.3
numpy==1.22.4
flask==2.2.3
scikit-learn==1.1.3
matplotlib==3.5.3
seaborn==0.11.2
joblib==1.1.0
json==2.0.9
모델 학습 및 실행
데이터 준비

BMI, 체중, TDEE, 활동 수준 등 사용자 데이터를 준비합니다.
데이터는 CSV 형식으로 제공되며, bmi_data.csv를 통해 학습합니다.
모델 학습 (Google Colab)

Google Colab에서 GPU 환경을 사용하여 모델 학습.
학습 코드 (src/python/main_predictor.py) 실행:
python
코드 복사
python main_predictor.py
모델 실행 (Standalone Script)

표준 입력(JSON 형식)을 받아 예측 결과 반환:
bash
코드 복사
python main_predictor.py < input.json
모델 배포 (Flask API)

Flask를 사용해 RESTful API로 배포:
bash
코드 복사
flask run
모델 평가
평가 지표:

MAE (Mean Absolute Error): 8.65
R² (결정계수): 0.99
결과 해석:

높은 R² 값은 모델의 높은 예측 정확도를 나타냅니다.
평균적으로 목표 달성일 예측은 ±8.65일의 오차를 가집니다.
챗봇 연동
SendBird 플랫폼 사용

사용자의 질의에 대해 딥러닝 예측 결과를 응답합니다.
chatbot_handler.py를 실행하여 챗봇 테스트.
OpenAI GPT API 통합

자연어 처리를 위해 GPT API를 호출하여 사용자와 상호작용.


[목표 예측 및 추천 서비스 데이터 파이프라인]
1. 데이터 탐색 및 준비
데이터 확인

BMI 데이터: 741명의 키, 몸무게, 성별, 나이, BMI 및 목표 체중 정보를 포함.
운동 데이터: 운동 이름, 소모 칼로리, 운동 부위(상체, 하체 등), 운동 유형(근력, 유산소 등) 포함.
식단 데이터: 음식 이름, 칼로리, 탄수화물, 단백질, 지방 등 식품 영양 정보를 포함.
데이터셋 구조:
plaintext
코드 복사
BMI 데이터셋: 키, 몸무게, 성별, 나이, BMI, 목표 체중
운동 데이터셋: 운동 이름, 운동 부위, 소모 칼로리, 운동 유형
식단 데이터셋: 음식 이름, 칼로리, 탄수화물, 단백질, 지방
결측치 처리

BMI 데이터: 결측값을 평균 또는 중앙값으로 채움.
Weight, Height, Age의 결측값 → 평균으로 대체.
TargetWeight: 체중의 90% 또는 체중 -10kg로 설정.
운동/식단 데이터: 결측값이 존재하지 않음.
데이터 변환 및 추가 피처 생성

BMI 계산:
BMI = 체중(kg) / (키(m)^2)
BMR 및 TDEE 계산:
BMR (기초대사량):
남성: 10 * 체중 + 6.25 * 키(cm) - 5 * 나이 + 5
여성: 10 * 체중 + 6.25 * 키(cm) - 5 * 나이 - 161
TDEE (하루 총 에너지 소비량): BMR * 활동 수준 계수
새로운 컬럼 생성:
TargetBMI: 목표 체중으로 BMI 재계산.
Calorie_Target: TDEE의 80%로 설정.
관련 코드 예시:

python
코드 복사
# 결측값 처리
bmi_data.fillna({
    'Weight': bmi_data['Weight'].mean(),
    'Height': bmi_data['Height'].mean(),
    'Age': bmi_data['Age'].median(),
    'TargetWeight': bmi_data['Weight'] * 0.9  # 체중의 90%로 기본 설정
}, inplace=True)

# BMI 계산
bmi_data['BMI'] = bmi_data['Weight'] / (bmi_data['Height'] ** 2)
bmi_data['TargetBMI'] = bmi_data['TargetWeight'] / (bmi_data['Height'] ** 2)

# BMR 및 TDEE 계산
bmi_data['BMR'] = 10 * bmi_data['Weight'] + 6.25 * (bmi_data['Height'] * 100) - 5 * bmi_data['Age']
bmi_data['BMR'] += bmi_data['Gender'].map({'Male': 5, 'Female': -161})
bmi_data['TDEE'] = bmi_data['BMR'] * bmi_data['ActivityLevel']
2. 운동 및 식단 추천 기준 설정
운동 추천 기준

BMI 및 활동 수준 기반으로 추천:
저체중 (BMI < 18.5): 체중 증가를 위한 근력 운동 + 고칼로리 식단.
정상 체중 (18.5 ≤ BMI < 25.0): 균형 잡힌 운동(유산소 + 근력 운동).
과체중 (25.0 ≤ BMI < 30.0): 체중 감소를 위한 유산소 운동 중심 프로그램.
비만 (BMI ≥ 30.0): 저강도 유산소 + 식단 조절.
운동 부위 선택: 사용자가 선호하는 부위(예: 하체, 상체) 기반 추천.
식단 추천 기준

목표 칼로리(TDEE 80%)에 맞춰 하루 식단을 구성.
식사 시간(아침, 점심, 저녁, 간식)에 따라 추천.
영양소 비율:
벌크업: 탄수화물 50%, 단백질 30%, 지방 20%.
체중 감소: 탄수화물 40%, 단백질 40%, 지방 20%.
음식 카테고리(밥, 국, 찌개 등)별 추천.
3. 딥러닝 모델 개발
데이터 라벨링

BMI 및 목표 유형(벌크업, 감량 등)에 따라 운동 및 식단을 라벨링.
예:
운동 유형: 유산소, 근력, 혼합
식단 유형: 고단백, 저지방
모델 학습

입력 피처: 나이, 키, 체중, 목표 체중, BMI, 활동 수준, 성별, 목표 유형 등.
출력 피처: 목표 체중 달성일까지 예상 소요 기간.
모델 구조: Feedforward Neural Network (FFNN).
은닉층: [128, 64, 32]
활성화 함수: LeakyReLU
최적화 기법: Adam Optimizer
모델 학습 및 최적화: Grid Search를 사용하여 하이퍼파라미터 최적화.
관련 코드 예시:

python
코드 복사
# Feedforward Neural Network 정의
class FeedforwardNN(nn.Module):
    def __init__(self, input_dim):
        super(FeedforwardNN, self).__init__()
        self.layers = nn.Sequential(
            nn.Linear(input_dim, 128),
            nn.LeakyReLU(),
            nn.Linear(128, 64),
            nn.LeakyReLU(),
            nn.Linear(64, 32),
            nn.LeakyReLU(),
            nn.Linear(32, 1)
        )

    def forward(self, x):
        return self.layers(x)
4. 예측 및 평가
모델 테스트

새로운 사용자 데이터를 입력해 목표 달성일을 예측.
예시 입력:
json
코드 복사
{
  "age": 25,
  "height": 170,
  "current_weight": 75,
  "target_weight": 65,
  "bmi": 25.9,
  "tdee": 2200,
  "activity_level": 3,
  "gender": "Male",
  "goal_type": "저지방 고단백"
}
모델 평가

평가 지표:
Mean Absolute Error (MAE): 8.65
R² (결정계수): 0.99
결과 해석

예측 결과는 ±8.65일의 오차 내에서 정확하게 목표 달성일을 예측.
위 내용은 데이터 준비, 가공, 추천 로직, 모델 학습 및 평가까지 딥러닝 기반 목표 예측 서비스의 전체 파이프라인을 정리한 것입니다

