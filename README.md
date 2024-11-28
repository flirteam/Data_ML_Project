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
