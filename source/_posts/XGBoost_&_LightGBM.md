---
title: "XGBoost & LightGBM (2016 ~ 2017)"
output:
  html_document:
    keep_md: true
categories: XGBoost & LightGBM
clearReading: true
thumbnailImage: image.png
thumbnailImagePosition: left
autoThumbnailImage: yes
metaAlignment: center
date: '2022-07-04 12:50:55'
---

XGBoost & LightGBM 방식 구별
<!-- excerpt -->

## XGBoost & LightGBM (2016 ~ 2017)
- 전통적인 머신러닝 알고리즘의 융합
  + 선형회귀 릿지 라쏘, 과적합 방지 위한 규제
  + 결정 트리의 핵심적인 알고리즘
  + 경사 하강법
  + 부스팅 기법
- 문제점 : 파라미터의 개수가 너무 많음
- 근데 왜 많이 쓰느냐
  + 모델 학습 속도
  + 성능
  + 가장 좋은 모델이란, 학습속도 + 성능 (지금까지 나온 알고리즘 보다)이 좋은 것
- 개발자로 성공하고 싶다?
- Python으로 시작 하지만
  + JAVA, C, C++ 을 배워야 함
  + 이 알고리즘들도 C, C++ 로 만들었음
- 큰 회사들의 개발
  + 1. 우리가 자체적으로 배포를 해보자 --> Python Wrapper API
  + 2. 파이썬 머신러닝 = Scikit-Learn 이 돼버림 --> Scikit-Learn에서 쉽게 쓸 수 있도록 개발하자
- 시장성은 Scikit-Learn 이 지배
- 방식구분을 잘 해야됨
  + 왜? 방식마다 지원하거나 지원 안하는 코드가 다 다름

### Python Wrapper 방식
- X_train, y_train
- 각 모듈에 맞도록 행렬을 재변환 해야 함.


```python
import xgboost as xgb 
from sklearn.model_selection import train_test_split
import seaborn as sns 

# 데이터 분리
titanic = sns.load_dataset('titanic')
titanic.info()

# X, 독립변수, y 종속변수
X = titanic[['pclass', 'parch', 'fare']]
y = titanic['survived']

# 훈련데이터, 테스트 데이터 분리
X_train, X_test, y_train, y_test = train_test_split(X, 
                                                    y, 
                                                    stratify = y, 
                                                    test_size = 0.3, 
                                                    random_state=42)

X_train.shape, X_test.shape, y_train.shape, y_test.shape
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 891 entries, 0 to 890
    Data columns (total 15 columns):
     #   Column       Non-Null Count  Dtype   
    ---  ------       --------------  -----   
     0   survived     891 non-null    int64   
     1   pclass       891 non-null    int64   
     2   sex          891 non-null    object  
     3   age          714 non-null    float64 
     4   sibsp        891 non-null    int64   
     5   parch        891 non-null    int64   
     6   fare         891 non-null    float64 
     7   embarked     889 non-null    object  
     8   class        891 non-null    category
     9   who          891 non-null    object  
     10  adult_male   891 non-null    bool    
     11  deck         203 non-null    category
     12  embark_town  889 non-null    object  
     13  alive        891 non-null    object  
     14  alone        891 non-null    bool    
    dtypes: bool(2), category(2), float64(2), int64(4), object(5)
    memory usage: 80.7+ KB
    




    ((623, 3), (268, 3), (623,), (268,))



- 여기가 핵심


```python
dtrain = xgb.DMatrix(data = X_train, label = y_train)
dtest = xgb.DMatrix(data = X_test, label = y_test)
# 이 코드 형태를 보면 'Python Wrapper API 형태로 코드를 짰구나.' 하고 알아야 한다.

print(dtrain)
```

    <xgboost.core.DMatrix object at 0x7f3dfa354610>
    

- 머신러닝 코드


```python
# from sklearn.tree import Class~~~~ 코드가 없이 바로 xgb.train 으로 간다
params = {
    'max_depth' : 3,
    'n_estimators' : 100,
    'eta' : 0.1,
    'objective' : 'binary:logistic'
}
num_rounds = 400   # 내가 얘를 400번 돌리겠다

w_list = [(dtrain, 'train'), (dtest, 'test')]
xgb_ml = xgb.train(params = params, 
                   dtrain = dtrain, 
                   num_boost_round = 400,
                   early_stopping_rounds = 100,    # 의미 없이 돌리지말고 100번만 돌리겠다
                   evals = w_list)  # dtrain = X_train 쓰면 에러난다. 변환을 해줘야 됨
```


```python
# 평가
from sklearn.metrics import accuracy_score
pred_probs = xgb_ml.predict(dtest)
y_pred = [1 if x > 0.5 else 0 for x in pred_probs]

# 예측 라벨과 실제 라벨 사이의 정확도 측정
accuracy_score(y_pred, y_test)
```




    0.6865671641791045



### Scikit-Learn API 방식


```python
from sklearn.tree import DecisionTreeClassifier
from xgboost import XGBClassifier # <--- 이 코드가 보이면 Scikit-Learn API 방식을 사용했다

# dt = DecisionTreeClassifier()
xgb_model = XGBClassifier(objective = 'binary:logistic', 
                          n_estimators=100, 
                          max_depth=3, 
                          learning_rate = 0.1, 
                          num_rounds = 400,
                          random_state=42)

w_list = [(X_train, y_train), (X_test, y_test)]

xgb_model.fit(X_train, y_train, eval_set = w_list, eval_metric='error', verbose=True)

y_probas = xgb_model.predict_proba(X_test)
y_pred = [1 if x > 0.5 else 0 for x in pred_probs]

# 예측 라벨과 실제 라벨 사이의 정확도 측정
accuracy_score(y_pred, y_test)
```

### LightGBM Python Wrapper 방식


```python
import lightgbm as lgb 
from sklearn.model_selection import train_test_split 
from sklearn.metrics import accuracy_score
import seaborn as sns 

# tips 데이터셋 
titanic = sns.load_dataset('titanic')

X = titanic[['pclass', 'parch', 'fare']]
y = titanic['survived']

# 훈련데이터, 테스트 데이터 분리
X_train, X_test, y_train, y_test = train_test_split(X, y, stratify = y, test_size = 0.3, random_state=42)

# XGBoost 코드와 유사하다. 
dtrain = lgb.Dataset(data = X_train, label = y_train)
dtest = lgb.Dataset(data = X_test, label = y_test)

params = {'max_depth':3,
          'n_estimators':100,
          'learning_rate': 0.1,
          'objective':'binary',
          'metric' : 'binary_error', 
          'num_boost_round' : 400, 
          'verbose' : 1} 

w_list = [dtrain, dtest]
lgb_ml = lgb.train(params=params, train_set = dtrain,\
                  early_stopping_rounds=100, valid_sets= w_list)

pred_probs = lgb_ml.predict(X_test)
y_pred=[1 if x > 0.5 else 0 for x in pred_probs]

# 예측 라벨과 실제 라벨 사이의 정확도 측정
accuracy_score(y_pred, y_test)
```

### LightGBM Scikit-Learn API 방식


```python
from lightgbm import LGBMClassifier
from sklearn.metrics import accuracy_score

# model 
w_list = [dtrain, dtest]
model = LGBMClassifier(objective = 'binary', 
                       metric = 'binary_error',
                       n_estimators=100, 
                       learning_rate=0.1, 
                       max_depth=3, 
                       num_boost_round = 400,
                       random_state = 32)
model.fit(X_train, 
          y_train, 
          eval_set = [(X_train, y_train), (X_test, y_test)], 
          verbose=1,
          early_stopping_rounds = 100)
y_probas = model.predict_proba(X_test) 
y_pred=[1 if x > 0.5 else 0 for x in y_probas[:, 1]] # 예측 라벨(0과 1로 예측)

# 예측 라벨과 실제 라벨 사이의 정확도 측정
accuracy_score(y_pred, y_test)
```
