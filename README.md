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
### 4.2 이상치 확인하고 처리하기
### 4.2.1 기초 통계량으로 이상치 확인하기
### 4.2.2 히스토그램으로 이상치 확인하기
```python
# 모듈 설치
!pip install koreanize-matplotlib # 한글 폰트 설정 라이브러리 설치
# 모듈 불러오기
import koreanize_matplotlib # 한글 출력 가능한 그래프 모듈
import matplotlib.pyplot as plt # 그래프 그리기에 필요한 모듈
import seaborn as sns # 시각화하기 위해 seaborn 모듈 불러오기
#히스토그램으로 확인하기
sns.histplot(data = df3, x = '꽃받침 길이', hue = '종류')
sns.histplot(data = df3, x = '꽃받침 너비', hue = '종류')
sns.histplot(data = df3, x = '꽃잎 길이', hue = '종류')
sns.histplot(data = df3, x = '꽃잎 너비', hue = '종류')
```
### 4.2.3 박스 플롯으로 이상치 확정하기
```python
sns.catplot(y = '꽃받침 길이', x = '종류', kind = 'box', data = df3, hue ='종류')
sns.catplot(y = '꽃받침 너비', x = '종류', kind = 'box', data = df3, hue = '종류')
sns.catplot(y = '꽃잎 길이', x = '종류', kind = 'box', data = df3, hue = '종류')
sns.catplot(y = '꽃잎 너비', x = '종류', kind = 'box', data = df3, hue = '종류')
```
### 4.2.4 이상치 제거하기
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
