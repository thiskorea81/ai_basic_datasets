# ai_basic_datasets

인공지능 기초(씨마스) 교과서 데이터셋을 모아놓은 공간입니다.
# 기계학습
# 1-3 데이터 전치리
### 1. 데이터가져오기
- 코랩에서 다음 명령어를 사용하여 가져올 수 있습니다.
```python
!git clone https://github.com/thiskorea81/ai_basic_datasets.git
```
데이터 경로는 다음과 같습니다.

> iris1: '/content/ai_basic_datasets/Iris1.csv'

> iris2: '/content/ai_basic_datasets/Iris2.csv'

### 2. 데이터셋 불러오기
```python
import pandas as pd
df1 = pd.read_csv('/content/ai_basic_datasets/Iris1.csv', encoding='cp949')
df2 = pd.read_csv('/content/ai_basic_datasets/Iris2.csv', encoding='cp949')
df1.head() # dataset 맨 위 5개 데이터 확인하기
```
### 3. 두 개의 데이터 합치기
```python
df = pd.concat([df1, df2])
df
 ```
### 위 작업을 하나로 합쳐놓았습니다.   
```python
# 1. 데이터 다운로드
!git clone https://github.com/thiskorea81/ai_basic_datasets.git
# 2. 데이터셋 불러오기
import pandas as pd
df1 = pd.read_csv('/content/ai_basic_datasets/Iris1.csv', encoding='cp949')
df2 = pd.read_csv('/content/ai_basic_datasets/Iris2.csv', encoding='cp949')
df1.head() # dataset 맨 위 5개 데이터 확인하기
# 3. 두 개의 데이터 합치기
df = pd.concat([df1, df2])
df
```
### 4.1 결측치 확인하고 처리하기
### 4.1.1 결측치 확인 isna()
### 4.1.2 결측치 제거 dropna()
### 4.2 이상치 확인하고 처리하기
### 4.2.1 기초 통계량으로 이상치 확인하기 describe()
### 4.2.2 히스토그램으로 이상치 확인하기 histplot()
```python
# 모듈 설치
!pip install koreanize-matplotlib

# 모듈 불러오기
import koreanize_matplotlib  # 한글 출력 가능한 그래프 모듈
import matplotlib.pyplot as plt
import seaborn as sns

# figure 크기 설정
plt.figure(figsize=(12, 10))

# 1. 꽃받침 길이
plt.subplot(2, 2, 1)
sns.histplot(data=df3, x='꽃받침 길이', hue='종류', kde=True)
plt.title('꽃받침 길이 분포')

# 2. 꽃받침 너비
plt.subplot(2, 2, 2)
sns.histplot(data=df3, x='꽃받침 너비', hue='종류', kde=True)
plt.title('꽃받침 너비 분포')

# 3. 꽃잎 길이
plt.subplot(2, 2, 3)
sns.histplot(data=df3, x='꽃잎 길이', hue='종류', kde=True)
plt.title('꽃잎 길이 분포')

# 4. 꽃잎 너비
plt.subplot(2, 2, 4)
sns.histplot(data=df3, x='꽃잎 너비', hue='종류', kde=True)
plt.title('꽃잎 너비 분포')

# 전체 간격 조정
plt.tight_layout()
plt.show()
```
### 4.2.3 박스 플롯으로 이상치 확정하기 boxplot()
```python
# 모듈 불러오기
import koreanize_matplotlib
import matplotlib.pyplot as plt
import seaborn as sns

# figure 크기 설정
plt.figure(figsize=(12, 10))

# 1. 꽃받침 길이
plt.subplot(2, 2, 1)
sns.boxplot(y='꽃받침 길이', x='종류', data=df3, hue='종류')
plt.title('꽃받침 길이(Boxplot)')

# 2. 꽃받침 너비
plt.subplot(2, 2, 2)
sns.boxplot(y='꽃받침 너비', x='종류', data=df3, hue='종류')
plt.title('꽃받침 너비(Boxplot)')

# 3. 꽃잎 길이
plt.subplot(2, 2, 3)
sns.boxplot(y='꽃잎 길이', x='종류', data=df3, hue='종류')
plt.title('꽃잎 길이(Boxplot)')

# 4. 꽃잎 너비
plt.subplot(2, 2, 4)
sns.boxplot(y='꽃잎 너비', x='종류', data=df3, hue='종류')
plt.title('꽃잎 너비(Boxplot)')

# 범례 중복 방지 및 레이아웃 조정
plt.tight_layout()
plt.show()
```
### 4.2.4 이상치 제거하기 drop()
```python
Q1 = df3.groupby('종류')['꽃받침 길이'].quantile(0.25) # 제1사분위수
Q3 = df3.groupby('종류')['꽃받침 길이'].quantile(0.75) # 제3사분위수
IQR = Q3 - Q1 # 사분위수 범위
print('Q1:', Q1); print('Q3:', Q3); print('IQR:', IQR)
```
```python
lower = Q1 - 1.5 * IQR; upper = Q3 + 1.5 * IQR
print('lower:', lower); print('upper:', upper)
```
```python
df4 = df3[df3['종류'] == '버시컬러']
df4[(df4['꽃받침 길이'] < lower['버시컬러'] ) | (df4['꽃받침 길이'] > upper['버시컬러'])]
```
```python
df3 = df3.drop(index = [3, 5, 6, 10, 13, 14, 18, 20, 22, 23, 24, 35, 43, 44, 98, 106], axis = 0) # 제거하려는 인덱스 설정
```
### 5. 핵심 속성 알기
### 5.1 선점도
```python
sns.pairplot(df3, hue = '종류', markers = ['o','s','D'])
plt.show()
```
### 5.2 히트맵
```python
irisData = df3.corr(method = 'pearson', numeric_only = True)
plt.figure(figsize = (10, 10))
sns.heatmap(data = irisData, annot = True, fmt = '.2f', linewidth = .5,
cmap = 'RdYlGn_r')
plt.show()
```
# 1.4 기계학습 유형과 알고리즘 선정

# 1.5 모델 학습과 성능 평가

### 1. 훈련 데이터, 테스트 데이터 준비
```python
X = df3[['꽃잎 길이', '꽃잎 너비']] # 독립 변수(핵심속성)
y = df3['종류']                    # 종속 변수
```

```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=7)
```

### 2.1 모델 생성(기계학습)
```python
from sklearn.neighbors import KNeighborsClassfier
model = KNeighborsClassifier() # k-최근접 이웃 모델 생성
```
### 2.2 모델 훈련
```python
model.fit(X_train, y_train)
```
### 3. 성능평가
### 3.1 테스트데이터로 정확도 확인
### 3.2 혼동행렬로 성능 확인
### 3.3 모델 개선
### 3.4 모델 활용
