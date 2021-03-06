# 180730

## 오전수업 배로쌤

### 1. 국민청원 카테고리 분류하기

#### 지난 시간 회고

머신러닝을 이용하여 국민청원의 이진분류를 시행했음. (vote가 평균 이상인가/아닌가?)

이번 시간에는 카테고리의 분류에 관한 내용을 다룰 것임.

Random Forest 방법을 이용하면 decision tree를 랜덤으로 여러개 만드는 개념이라 정확도가 더 높아질 수 있음. decision tree 를 그리게 된다면 처음부터 True/False를 나누어 밑으로 내려가는 방식이라 나중으로 갈수록 한 번 위에서 정했던 가지를 타고 내려가기 때문에 정확도가 비교적 낮음.(읽어보기: http://swalloow.tistory.com/92)

##### 국민청원 데이터 카테고리 분류하기

binary classification 과 multy~~ classification의 차이점.

어떤 카테고리가 가장 많은 지 예측하는 과정.

예측 비율을 높일 수 있는 몇 가지 방법

1. 테스트 데이터 전처리하기
2. 학습세트와 테스트세트 다시 만들기(단 학습세트와 테스트세트의 비율을 7:3으로 유지합니다.)
3. 텍스트 데이터 벡터화 할 때 파라메터 조정하기
4. 랜덤 포레스트의 파라메터 조정하기
5. (선택) 랜덤 포레스트 외의 알고리즘 사용해 보기 (eg) xgboost 
   1. xgb 사용 시 colab에서 설치 후 사용해야 합니다.

train set으로 학습시키기 : 기출문제를 학습한다. 모의고사를 보아 얼마나 잘 학습했는 지 평가할 수 있음. 여러 번 시험을 보아, 평가 정확도 점수를 높인 후 test set으로 실제 정확도를 평가하기. 만약, 모든 기출문제와 모의고사를 몽땅 학습하여 train set 에서의 정확도가 100%가 나온다고 하여도, 그 모델은 기출문제와 모의고사라는 특정 문제에만 매우 잘 맞는 모델이 됨. test set에 적용시켜 보면 100%가 안될 수 있음.

#### 국민청원 카테고리 분류 정확도 높이기 실습

우리 조에서 처리해준 것들

- 전체 데이터 투표가 100개 이상, 20만개 이하인 데이터 10026개
- 전처리 안녕,안녕하세요,안녕하십니까,저도,저는,제가
- 기타 카테고리 제외
- 벡터화 -> char단위로 analyzer를 바꿔줌
- 불용어 영어 날리기
- max features - 1000
- random forest
  - min_samples_leaf 10
  - min_samples_split 10
  - n estimator 300

또 다른 방법들

- 중복청원삭제
- 불용어 처리 보다는 개행문자만 확실히 제거
- 7:3 비율을 랜덤하게 들어가도록 설정
- RF 파라미터 값 변경



> 추가설명

벡터라이징 파라미터

Random Forest 파라미터

- `n jobs` 사용 할 cpu 코어 -1인 경우 최대로 사용
- `n_estimators` : 더 알아보기
- `random_state` :  원래 매 번 실행시킬 때 마다 랜덤한 결과가 나오기 때문에 파라미터 값을 변경하였을 때 그 변화한 값이 랜덤값때문인지, 파라미터값의 변경인지 정확히 알 수 없음. 하지만 random_state를 지정해 주면 오직 파라미터 값의 변화에 따른 정확도가 산출됨.



### 2. Kaggle NLP

- 스테밍
- 전처리과정
- 파이프라인

쓰는 것이 저번 실습과 다른 점. 25000개의 데이터를 돌려야 하기 때문에 파이프라인을 사용함.