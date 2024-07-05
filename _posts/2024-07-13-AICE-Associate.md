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

# 데이터 전처리

# 머신러닝 / 딥러닝 모델링

# 모델 성능평가