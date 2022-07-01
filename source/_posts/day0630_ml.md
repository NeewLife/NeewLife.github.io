---
title: "day 0630"
output:
  html_document:
    keep_md: true
disqusIdentifier: fdsF34ff34
categories: Python
clearReading: true
thumbnailImage: source/images/0629/Untitled.png
thumbnailImagePosition: left
autoThumbnailImage: yes
metaAlignment: center
date: '2022-06-29 18:59:30'
---

## 새로운 모델 제안
- Default : 정확도 100%
- 새롭게 제안 : 정확도 71%

--> 실험단계 --> 이것저것 다 해보고 정확도가 가장 높은 모델 채택

- 하이퍼 파라미터 세팅
  + n_neighbors = 49

- default : 100%
- default 값은 KNeighborsClassifier default 이런식으로 구글링 하면 나옴

## 머신러닝 알고리즘 두개의 흐름
- 인공지능 → 머신러닝 → 딥러닝
- 머신러닝 알고리즘
    - 선형회귀, 결정트리
    - 결과에 대한 해석 요구
    - 통계분석 같이 해야함
    - 정형데이터(=엑셀 데이터, 테이블)
- 딥러닝 알고리즘(p.340~)
    - 인공신경망
    - 이미지(=영상인식), 자연어(=음성인식)
    - 성능이 좋은지?
    
- 분석의 흐름
1. 데이터 수집
2. 데이터 가공
3. 데이터 시각화
4. 데이터 (예측)모델링 
    
    ⇒ 예측 평가지표가 중요함
    
    ⇒ 알고리즘 공부
    
    ⇒ 알고리즘 종류 수백가지
    
    R : 데이터 (통계)모델링 
    
    ⇒ 해석에 포커싱 
    
    ⇒ 변수(=컬럼=피처)간의 관계
    
    ⇒ 가설 검정이 중요
    
5. 보고서를 작성(상사, 갑, 의사결정자)
    - 면접자료 : 소스코드 & PPT


- 선형모델 : 선형회귀, 로지스틱 회귀, 서포트 벡터 머신
- 의사결정트리 모델 : 1975년 의사결정트리 모델, KNN
  + Kaggle에서 자주쓰는 모델 
  + 랜덤포레스트
  + 부스팅계열 : LightGBM(2017), XGBoost(2016)

- 알고리즘 공부를 꼭 해야겠다 => 선형회귀, 로지스틱회귀, 랜덤포레스트, ***LightGBM(=XGBoost)***


```python
kn49 = KNeighborsClassifier(n_neighbors=49)   # default 값을 49로 한 kn49모델
kn49.fit(fish_data, fish_target)
kn49.score(fish_data, fish_target)
```




    0.7142857142857143



## 훈련 세트와 테스트 세트
- 이미 도미 / 빙어 박스가 분류가 되어 있음
- 두 박스를 섞었을 때도 분류가 되는지 확인
- 처음에 바로 하기는 힘드니 샘플링을 통해 학습


```python
fish_length = [25.4, 26.3, 26.5, 29.0, 29.0, 29.7, 29.7, 30.0, 30.0, 30.7, 31.0, 31.0, 
                31.5, 32.0, 32.0, 32.0, 33.0, 33.0, 33.5, 33.5, 34.0, 34.0, 34.5, 35.0, 
                35.0, 35.0, 35.0, 36.0, 36.0, 37.0, 38.5, 38.5, 39.5, 41.0, 41.0, 9.8, 
                10.5, 10.6, 11.0, 11.2, 11.3, 11.8, 11.8, 12.0, 12.2, 12.4, 13.0, 14.3, 15.0]
fish_weight = [242.0, 290.0, 340.0, 363.0, 430.0, 450.0, 500.0, 390.0, 450.0, 500.0, 475.0, 500.0, 
                500.0, 340.0, 600.0, 600.0, 700.0, 700.0, 610.0, 650.0, 575.0, 685.0, 620.0, 680.0, 
                700.0, 725.0, 720.0, 714.0, 850.0, 1000.0, 920.0, 955.0, 925.0, 975.0, 950.0, 6.7, 
                7.5, 7.0, 9.7, 9.8, 8.7, 10.0, 9.9, 9.8, 12.2, 13.4, 12.2, 19.7, 19.9]
```

- 2차원 파이썬 리스트
- 라벨링


```python
fish_data = [[l, w] for l, w in zip(fish_length, fish_weight)]
fish_target = [1] * 35 + [0] * 14
print(fish_target[0:40:5])
print(fish_data[0:40:5])
```

    [1, 1, 1, 1, 1, 1, 1, 0]
    [[25.4, 242.0], [29.7, 450.0], [31.0, 475.0], [32.0, 600.0], [34.0, 575.0], [35.0, 725.0], [38.5, 920.0], [9.8, 6.7]]
    

- Sample (모든 도미, 빙어가 아니라 일부만 추출한 것)
- 도미 35마리, 빙어 14마리
- 49개의 샘플 존재
- 처음 35개를 훈련 / 나머지 14개를 테스트


```python
from sklearn.neighbors import KNeighborsClassifier

# 클래스 인스턴스화 (kn 으로 안 써도 됨)
kn = KNeighborsClassifier()

# 훈련 세트로 0:34 인덱스 활용
train_input = fish_data[:35]
train_target = fish_target[:35]

# 테스트 세트로 35:마지막 인덱스 활용
test_input = fish_data[35:]
test_target = fish_target[35:]

# 모형 학습
kn = kn.fit(train_input, train_target)
print(kn.score(test_input, test_target))
```

    0.0
    

- 도미만 35개 보여주고 빙어 14개를 테스트 해버림..
- 샘플링 편향
=> 훈련세트와 테스트 세트가 골고루 섞이지 않음

## 샘플링 작업


```python
import numpy as np

input_arr = np.array(fish_data)
target_arr = np.array(fish_target)
print(input_arr[0:49:7])
print(input_arr.shape, target_arr.shape)
```

    [[ 25.4 242. ]
     [ 30.  390. ]
     [ 32.  600. ]
     [ 34.  685. ]
     [ 36.  850. ]
     [  9.8   6.7]
     [ 11.8   9.9]]
    (49, 2) (49,)
    


```python
np.random.seed(42)    # 42seed로 무작위로 계속 섞는 함수(seed 번호가 달라지면 index 순서도 바뀜)
index = np.arange(49)
np.random.shuffle(index)
print(index)
```

    [13 45 47 44 17 27 26 25 31 19 12  4 34  8  3  6 40 41 46 15  9 16 24 33
     30  0 43 32  5 29 11 36  1 21  2 37 35 23 39 10 22 18 48 20  7 42 14 28
     38]
    


```python
train_input = input_arr[index[:35]]
train_target = target_arr[index[:35]]

test_input = input_arr[index[35:]]
test_target = target_arr[index[35:]]
```

## 시각화


```python
print(train_input[:,0], train_input[:,1])
```

    [32.  12.4 14.3 12.2 33.  36.  35.  35.  38.5 33.5 31.5 29.  41.  30.
     29.  29.7 11.3 11.8 13.  32.  30.7 33.  35.  41.  38.5 25.4 12.  39.5
     29.7 37.  31.  10.5 26.3 34.  26.5] [ 340.    13.4   19.7   12.2  700.   714.   720.   725.   955.   650.
      500.   430.   950.   450.   363.   500.     8.7   10.    12.2  600.
      500.   700.   700.   975.   920.   242.     9.8  925.   450.  1000.
      500.     7.5  290.   685.   340. ]
    


```python
import matplotlib.pyplot as plt
fig, ax = plt.subplots()
ax.scatter(train_input[:,0], train_input[:,1])
ax.scatter(test_input[:,0], test_input[:,1])
ax.set_xlabel("length")
ax.set_ylabel("weight")
plt.show()
```


    
![png](/images/0630/output_45_0.png)
    


## 두번째 머신러닝 프로그램


```python
kn.fit(train_input, train_target)
kn.score(test_input, test_target)
```




    1.0




```python
kn.predict(test_input)  # 예측 데이터
```




    array([0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 0, 1, 1, 0])




```python
test_target  # 실제 데이터
```




    array([0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 0, 1, 1, 0])



## 데이터 전처리
- 머신러닝 시, 데이터 전처리
- 결측치 처리, 이상치 처리

## 데이터 불러오기


```python
fish_length = [25.4, 26.3, 26.5, 29.0, 29.0, 29.7, 29.7, 30.0, 30.0, 30.7, 31.0, 31.0, 
                31.5, 32.0, 32.0, 32.0, 33.0, 33.0, 33.5, 33.5, 34.0, 34.0, 34.5, 35.0, 
                35.0, 35.0, 35.0, 36.0, 36.0, 37.0, 38.5, 38.5, 39.5, 41.0, 41.0, 9.8, 
                10.5, 10.6, 11.0, 11.2, 11.3, 11.8, 11.8, 12.0, 12.2, 12.4, 13.0, 14.3, 15.0]
fish_weight = [242.0, 290.0, 340.0, 363.0, 430.0, 450.0, 500.0, 390.0, 450.0, 500.0, 475.0, 500.0, 
                500.0, 340.0, 600.0, 600.0, 700.0, 700.0, 610.0, 650.0, 575.0, 685.0, 620.0, 680.0, 
                700.0, 725.0, 720.0, 714.0, 850.0, 1000.0, 920.0, 955.0, 925.0, 975.0, 950.0, 6.7, 
                7.5, 7.0, 9.7, 9.8, 8.7, 10.0, 9.9, 9.8, 12.2, 13.4, 12.2, 19.7, 19.9]
```


```python
# column_stack() 활용
# 리스트 만들고 2차원 변형하고 배열하는 그 과정들을 생략
np.column_stack(([1, 2, 3], [4 ,5 ,6]))
```




    array([[1, 4],
           [2, 5],
           [3, 6]])




```python
fish_data = np.column_stack((fish_length, fish_weight))
print(fish_data[:5])
```

    [[ 25.4 242. ]
     [ 26.3 290. ]
     [ 26.5 340. ]
     [ 29.  363. ]
     [ 29.  430. ]]
    

- 종속변수 = Y = 타겟 데이터 = Target


```python
fish_target = np.concatenate((np.ones(35),np.zeros(14)))
print(fish_target)
```

    [1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.
     1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.
     0.]
    

### scikit-learn 훈련세트와 테스트 세트 나누기


```python
# 위에 두줄은 암기!!
from sklearn.model_selection import train_test_split
train_input, test_input, train_target, test_target = train_test_split(
    # 독립변수, 종속변수, 난수 고정
    fish_data, fish_target, random_state = 42
)

train_input.shape, test_input.shape, train_target.shape, test_target.shape
# 항상 변수가 같은지 체크(2, 2, 0, 0 등)
```




    ((36, 2), (13, 2), (36,), (13,))



- 도미와 빙어가 잘 섞여 있는지 확인하기


```python
print(test_target)
```

    [1. 0. 0. 0. 1. 1. 1. 1. 1. 1. 1. 1. 1.]
    

- 35(도미) : 14(빙어)
  + 2.5 : 1 비율
- 테스트 셋
  + 3.3 : 1 비율
- 비율이 맞지 않으면 최종적인 머신러닝 결괏값이 왜곡될 수 있다.

## 층화 샘플링
- 기초 통계, 설문조사
- 비율
- 여론조사
  + 남성 속옷 판매회사에서는 속옷을 구매하는 비율(남자 9, 여자1)
  + 그런데 신제품 출시시 (남자 5, 여자 5) 비율의 설문이면 결과가 왜곡될 수 있다.
- stratify = y, 옵션 함수 사용


```python
train_input, test_input, train_target, test_target = train_test_split(
    # 독립변수, 종속변수, 난수 고정
    fish_data, fish_target, stratify = fish_target, random_state = 42
)

train_input.shape, test_input.shape, train_target.shape, test_target.shape
# 항상 변수가 같은지 체크(2, 2, 0, 0 등)
```


```python
print(test_target)
```

    [1. 0. 0. 0. 1. 1. 1. 1. 1. 1. 1. 1. 1.]
    

- 테스트 세트의 비율이 2.25:1


## 수상한 도미 한 마리


```python
from sklearn.neighbors import KNeighborsClassifier
kn = KNeighborsClassifier()
kn.fit(train_input, train_target)
kn.score(test_input, test_target)
```




    1.0




```python
print(kn.predict([[25,150]]))
```

    [0.]
    


```python
import matplotlib.pyplot as plt
fig, ax = plt.subplots()
ax.scatter(train_input[:,0], train_input[:,1])
ax.scatter(25, 150, marker='^')     # marker = '^' 매개변수 모양을 지정하는 것(주황색 삼각형)
ax.set_xlabel("length")
ax.set_ylabel("weight")
plt.show()
```


    
![png](/images/0630/output_69_0.png)
    


- 왜 도미 쪽 데이터가 더 가까운데 빙어로 인식했을까?
- 알고리즘 문제


```python
distances, indexes = kn.kneighbors([[25,150,]])
import matplotlib.pyplot as plt
fig, ax = plt.subplots()
ax.scatter(train_input[:,0], train_input[:,1])
ax.scatter(25, 150, marker='^')     # marker = '^' 매개변수 모양을 지정하는 것(주황색 삼각형)
ax.scatter(train_input[indexes,0], train_input[indexes,1], marker='D')  # 이웃 샘플 5개를 다이아몬드로 표시
ax.set_xlabel("length")
ax.set_ylabel("weight")
plt.show()
```


    
![png](/images/0630/output_71_0.png)
    


- 두 특성(길이와 무게)의 값이 놓인 범위가 매우다름
- 알고리즘은 두 특성(길이, 무게)을 같다고 판단함
- 두 특성의 스케일이 같도록 통계 처리가 필요
  + Feature Engineering
## 머신러닝 진행시 습관적으로 사용할 순서
  + 전체데이터 전처리(결측치 처리, 이상치 처리)
  + 데이터 분리 (임의 샘플링 < 층화 샘플링)
  + Feature Engineering

### 표준점수
- z 점수
- (산술식 찾아 채워보기)


```python
mean = np.mean(train_input, axis = 0)
std = np.std(train_input, axis = 0)

print(mean, std)
```

    [ 26.175      418.08888889] [ 10.21073441 321.67847023]
    

- 표준 점수 구하기


```python
# 브로드캐스팅 서로 다른 배열을 계산할 때
print(train_input.shape, mean.shape, std.shape)
train_scaled = (train_input - mean) / std     # train_scaled 로 데이터 전처리 진행
```

    (36, 2) (2,) (2,)
    


```python
new = ([25, 150] - mean) / std
plt.scatter(train_scaled[:,0], train_scaled[:,1])
plt.scatter(new[0], new[1], marker='^')     # marker = '^' 매개변수 모양을 지정하는 것(주황색 삼각형)
plt.xlabel("length")
plt.ylabel("weight")
plt.show()
```


    
![png](/images/0630/output_77_0.png)
    


- 통계처리 전 : KNN --> 예측이 틀렸음
- 통계처리 후 : KNN --> 예측이 정확하게 맞음
-- 통계처리 --> Feature Engineering

- 모형학습


```python
kn.fit(train_scaled, train_target)
```




    KNeighborsClassifier()




```python
test_scaled = (test_input -mean) / std
kn.score(test_scaled, test_target)
```




    1.0



- 예측 해보기


```python
print(kn.predict([new]))
distances, indexes = kn.kneighbors([new])
plt.scatter(train_scaled[:,0], train_scaled[:,1])
plt.scatter(new[0], new[1], marker='^')
plt.scatter(train_scaled[indexes,0], train_scaled[indexes,1], marker='D')
plt.xlabel('length')
plt.ylabel('weight')
plt.show()
```

    [1.]
    


    
![png](/images/0630/output_83_1.png)
    

