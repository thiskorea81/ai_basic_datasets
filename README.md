# ai_basic_datasets

인공지능 기초(씨마스) 교과서 데이터셋을 모아놓은 공간입니다.

1. 데이터가져오기
- 코랩에서 다음 명령어를 사용하여 가져올 수 있습니다.
```python
!git clone https://github.com/thiskorea81/ai_basic_datasets.git
```
데이터 경로는 다음과 같습니다.
```python
iris1 '/content/ai_basic_datasets/Iris1.csv'
iris2 '/content/ai_basic_datasets/Iris2.csv'
```
2. 데이터셋 불러오기
```python
import pandas as pd
df1 = pd.read_csv('/content/ai_basic_datasets/Iris1.csv', encoding='cp949')
df2 = pd.read_csv('/content/ai_basic_datasets/Iris2.csv', encoding='cp949')
df1.head() # dataset 맨 위 5개 데이터 확인하기
```
4. 두 개의 데이터 합치기
```python
df = pd.concat([df1, df2])
 ```
   
