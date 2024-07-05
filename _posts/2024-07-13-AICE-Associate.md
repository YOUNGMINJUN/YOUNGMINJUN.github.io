---
title: "AICE Associate 시험 준비"
date: 2024-07-05
categories: AI 자격증 AICE
---
# 탐색적 데이타 분석
## 라이브러리 로드
> 없는 라이브러리는 `!pip install`로 설치 후 로드

- scikit-learn
```
import sklearn as sk
```
- pandas
```
import pandas as pd
```
- numpy
```
import numpy as np
```
- matplotlib
```
import matplotlib.pyplot as plt
```
- seaborn
```
!pip install seaborn
import seaborn as sns
```

## 데이타 로드 및 확인
```
// csv 데이타 로드
df = pd.read_csv('data.csv')

// json 데이타 로드
df = pd.read_json('data.json')

// 앞행 n개 확인(default: 5)
df.head(n)

// 뒷행 n개 확인(default: 5)
df.tail(n)

// 데이타 프레임 열 이름 확인
df.columns

// 데이터 프레임 행, 열 개수 확인
df.shape

// 데이타 열 정보, Null 개수, 열 타입, 사이즈 등의 데이타 프레임 정보 확인
df.info()

// 계산 가능한 값(수치형 변수)에 대한 통계 정보 확인
df.describe()

// Null인 데이타 확인
// 단순히 isnull() 만 사용하기도 하지만 sum()과 함께 사용하여 행이나 열별로의 Null개수를 세기 위해 주로 사용
df.isnull().sum()

// 범주형 변수에 대한 각 범주별 빈도수 확인
// - normalize = True 를 주면 정규화된 값으로 범주별 비율을 확인
df[열 이름].value_counts(normalize=True)

// 원하는 데이타 타입에 해당하는 열만 데이타 프레임 형태로 확인
// - type : int, float, str 등의 원하는 데이터 타입의 열만 추출
// .columns 를 활용해 열 이름만 추출할 수 있다.
df.select_dtypes(type)

```

---

# 데이터 전처리

## 데이터 프레임 제거 및 변환
```
// 선택 열 제거
// - axis : 행(=0)과 열(=1)을 주어 원하는 방향으로 제거할 수 있음
// - inplace = TRUE : 변수를 할당하지 않고 바로 적용할 수 있음
df.drop(axis=0/1, inplace=True)

// 값 변경
// 원하는 값으로 변경하기 위해 사용하며 결측값 대체나 범주형 변수를 라벨링할 때 사용
// - to_replace : 주로 {'바꾸고자 하는 값' : '바뀌는 값'} 의 딕셔너리 형태로 주어짐
df.replace({'바꾸고자 하는 값': '바뀌는 값'}, inplace = False/True)

// 결측값 대체
// - inplace = True : 변수를 할당하지 않고 바로 적용할 수 있음
df['열이름'].fillna('바뀌는 값', inplace = False/True)

// 데이터 프레임 열 타입 변환
// astype은 바꾸고자 하는 열에 할당해주어야 변환 값이 적용된다
// - type : int, float, str 등으로 원하는 타입으로 변환
df['열이름'] = df['열이름'].astype(type)

// 그룹별 집계 함수
// 집계 함수에 맞게 그룹볍ㄹ로 원하는 열로 집계할 수 있다.
// - by : 그룹의 기준이 되는 열로 여러 열을 기준으로 할 수 있다.
// - as_index = bool : 그룹 기준 열을 인덱스화 할지 여부를 선택할 수 있다.
// - 집계함수 : sum(합), mean(평균), count(개수) 등의 집계함수
df.groupby(by=['그룹기준 열'])['집계 대상 열'].집계함수()
```

## 정규화/표준화(스케일링)
```
// MinMaxScaler를 사용하기 위해서 로드하는 과정이 필요
// - fit : 기준이 되는 데이터를 기반으로 스케일러 값을 맞춘다
// - transform : 기준 값을 기반으로 스케일링을 적용한다.
from sklearn.preprocessing import MinMaxScaler

mms = MinMaxScaler()

# 스케일링 적용
X_train = mms.fit_transform(X_train)
X_test = mms.transform(X_test)
```

## 인코딩
```
// LabelEncoder를 사용하기 위해서는 로드하는 과정이 필요하다.
// - fit: 기준이 되는 데이터를 기반으로 인코더 값을 맞춘다.
// - transform: 기준 값을 기반으로 인코딩을 적용한다.
from sklearn.preprocessing import LabelEncoder

le = LabelEncoder()

# 인코딩 적용
df['범주형 열'] = le.fit_transform(df['범주형 열'])


// 원-핫 인코딩 One-Hot Encoding
// 원-핫 인코딩은 pandas내의 메소드로 적용한다.
// - columns: 원-핫 인코딩을 적용할 열 리스트
// - drop_first=True: 첫번째 범주는 제외하고 원-핫 인코딩 적용.
df = pd.get_dummies(df, columns=['범주형 열'], drop_first=True)
```

## 데이터 분할
```
// train_test_split를 사용하기 위해서는 로드하는 과정이 필요하다.
// X_train, X_test, y_train, y_test 순으로 분할한 데이터 값을 반환한다.
// - train_size/test_size: 학습용/검증용 데이터를 분할할 기준이 된다. (주로 8:2나 7:3으로 분할한다.)
// - stratify: 타겟 변수의 불균형이 심할 때 범주를 균형있게 분할 해준다.
// - random_state: 랜덤 시드를 줌으로써 매번 같은 결과가 나올 수 있도록 설정한다.
from sklearn.model_selection import train_test_split

# 데이터 분할
X_train, X_test, y_train, y_test = train_test_split(X, y, train_size=.8, stratify=y, random_state=2023)
```



---

# 머신러닝 / 딥러닝 모델링
## 모델에서 사용하는 명령어
### 모델 학습
```
// fit()
// 생성된 모델을 학습용 데이터를 기반으로 학습한다.
# 모델 학습
model.fit(X_train, y_train)
```

### 모델 검증
```
// score()
// 생성된 모델의 성능을 평가한다.
// 분류 모델은 정확도로, 회귀 모델은 결정계수로 검증한다.
# 모델 검증
model.score(X_test, y_test)
```

### 모델 예측
```
// predict()
// 생성된 모델로 데이터의 예측값을 계산한다.
# 모델 예측
model.predict(X_test)
```

### 모델 검증
```
// 모델 검증에 사용되는 지표도 모델에 따라 달라진다.
// - 회귀 모델: MSE, RMSE, MAE, ...
// - 분류 모델: Accuracy, Precision, Recall, F1 Score, ...
```

---
## 머신러닝 모델링
### Logistic Regression (로지스틱 회귀, 분류)

```
// LogisticRegression
// Logistic Regression을 사용하기 위해서는 로드하는 과정이 필요하다.
// - C: 규제 강도
// - max_iter: 반복 횟수
# import
from sklearn.linear_model import LogisticRegression

# 모델 생성
lg = LogisticRegression(C=1.0, max_iter=1000)

# 모델 학습
lg.fit(X_train, y_train)

# 모델 평가
lg.score(X_test, y_test)
```

### Decision Tree (의사결정 나무, 분류/회귀)
```
// DecisionTreeClassifier / DecisionTreeRegressor
// Decision Tree를 사용하기 위해서는 로드하는 과정이 필요하다.
// - max_depth: 트리 깊이
// - random_state: 랜덤 시드
# import
from sklearn.tree import DecisionTreeClassifier # 분류
from sklearn.tree import DecisionTreeRegressor # 회귀

# 모델 생성
dt = DecisionTreeClassifier(max_depth=5, random_state=2023)

# 모델 학습
dt.fit(X_train, y_train)

# 모델 평가
dt.score(X_test, y_test)
```

### Random Forest (랜덤 포레스트, 분류/회귀)
```
// RandomForestClassifier / RandomForestRegressor
// Random Forest를 사용하기 위해서는 로드하는 과정이 필요하다.
// - n_estimators: 사용하는 트리 개수
// - random_state: 랜덤 시드
# import
from sklearn.ensemble import RandomForestClassifier # 분류
from sklearn.ensemble import RandomForestRegressor # 회귀

# 모델 생성
rf = RandomForestClassifier(n_estimators=100, random_state=2023)

# 모델 학습
rf.fit(X_train, y_train)

# 모델 평가
rf.score(X_test, y_test)
```

### XGBoost (분류/회귀)
```
// XGBClassifier / XGBRegressor
// XGBoost를 사용하기 위해서는 설치 및 로드하는 과정이 필요하다.
// - n_estimators: 사용하는 트리 개수
# install
!pip install xgboost

# import
from xgboost import XGBClassifier # 분류
from xgboost import XGBRegressor # 회귀

# 모델 생성
xgb = XGBClassifier(n_estimators=100)

# 모델 학습
xgb.fit(X_train, y_train)

# 모델 평가
xgb.score(X_test, y_test)
```

### Light GBM (분류/회귀)
```
// LGBMClassifier / LGBMRegressor
// Light GBM을 사용하기 위해서는 설치 및 로드하는 과정이 필요하다.
// - n_estimators: 사용하는 트리 개수
# install
!pip install lightgbm

# import
from lightgbm import LGBMClassifier # 분류
from lightgbm import LGBMegressor # 회귀

# 모델 생성
lgbm = LGBMClassifier(n_estimators=100)

# 모델 학습
lgbm.fit(X_train, y_train)

# 모델 평가
lgbm.score(X_test, y_test)

```

## 딥러닝 모델링
> 딥러닝은 tensorflow를 활용하여 모델링 한다.

```
# import
import tensorflow as tf
from tensorflow import keras
```

### 모델 생성
- Sequential한 방법으로 레이어를 쌓는 문제

```
# 첫번째 레이어 - unit: 128, activation: relu, input_shape: (26,)
# 두번째 레이어 - unit: 64, activation: relu
# 세번째 레이어 - unit: 32, activation: relu
# 각 히든 레이어 사이에는 0.3비율의 Dropout 적용
# 아웃풋 레이어 - activation: sigmoid
```

- 문제 풀이

```
# import
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Dropout

# 모델 생성
model = Sequential()

# 모델 구조
model.add(Dense(128, input_shape=(26,), activation='relu'))
model.add(Dropout(.3))
model.add(Dense(64, activation='relu'))
model.add(Dropout(.3))
model.add(Dense(32, activation='relu'))
model.add(Dropout(.3))
# output layer의 unit 수는 타겟 변수의 범주 개수와 동일하다.
model.add(Dense(1, activation='sigmoid')) 

# 모델 요약
model.summary()
```

### 모델 학습
```
// compile
// 딥러닝은 머신러닝과 달리 모델링 과정에서 컴파일이 필요하다.
// - optimizer: 모델링을 최적화하는 방법. 주로 Adam을 사용한다.
// - loss: 손실함수 - 타겟변수에 맞는 손실함수를 사용해야 한다.
//   - 회귀: mse
//   - 이진분류: binary_crossentropy
//   - 다중분류: sparse_categorical_crossentropy, categorical_crossentropy
// - metrics: 모니터링 지표로, 사용자 정의 함수를 사용할 수 있다.
/    - 회귀: mse, rmse
//   - 분류: accuracy
# 모델 컴파일
model.compile(optimizer='adam',  loss='binary_crossentropy', metrics=['accuracy'])
```

```
// EarlyStopping
// 모델의 과대적합을 방지하기 위해 학습이 개선되지 않는다면 학습을 종료시킨다.
// - monitor: 학습되는지 확인하는 기준
// - mode: 모델 최적화의 기준 - 최대화/최소화
// - patience: 모델 성능이 개선되지 않을때 지켜보는 횟수
# import
from tensorflow.keras.callbacks import EarlyStopping

es = EarlyStopping(monitor='val_loss', mode='min')
```

```
// ModelCheckpoint
// 모델을 학습하는 과정에서 일정한 간격으로 모델의 가중치를 저장하며 최적 모델을 선택한다.
// - filepath: 모델 저장 경로
// - monitor: 모니터링하는 지표
// - mode: 모델 최적화의 기준 - 최대화/최소화
// - verbose: 정보 표시 정도(0, 1, 2)
// - save_best_only=True: 가장 좋은 성능의 모델만 저장
# import
from tensorflow.keras.callbacks import ModelCheckpoint

mc = ModelCheckpoint('my_checkpoibnt.ckpt', monitor='val_loss', mode='min', save_best_only=True)
```

```
// fit
// 모델을 학습한다.
// - validation_data: 검증용 데이터. 종속변수와 타겟변수의 쌍으로 입력해야 한다.
// - epochs: 학습 반복 횟수
// - batch_size: 학습 시 한 번에 학습하는 데이터 사이즈
// - callbacks: EarlyStopping, ModelCheckpoint와 같은 학습 과정에서 호출되는 함수
history = model.fit(X_train, y_train, validation_data = (X_test, y_test), epochs=epochs, batch_size=batch_size, callbacks=[es, mc])
```

### 모델 검증
```
// history
// 모델 학습 과정에서 모델 학습 결과를 저장함으로써 학습 과정의 변화를 확인할 수 있다.
// history는 딕셔너리 형태로 저장되어 key값으로 접근할 수 있다.
// - loss: 학습 loss.
// - val_loss: 검증 loss.
// - accuracy: 학습 accuracy.
// - val_accuracy: 검증 accuracy.
# 시각화 예시
plt.plot(history.history['loss'], label='Train Loss')
plt.plot(history.history['val_loss'], label='Validation Loss')
plt.xlabel('Epochs') 	# X축 라벨
plt.ylabel('Loss')		# Y축 라벨
plt.legend()			# 범례 표시 - label값
plt.show()
```
# 모델 성능평가