---
title: "Pandas 10minute"
categories:
- Python
- Assignment
output:
 html_document:
   keep_md: true
date: '2022-06-28'
---


```python
import numpy as np
import pandas as pd
```

## 객체 생성
- Series : 기본 정수 인덱스를 생성하도록 값 목록을 전달하여 생성


```python
s = pd.Series([1,3,5,np.nan,6,8])
s
```




    0    1.0
    1    3.0
    2    5.0
    3    NaN
    4    6.0
    5    8.0
    dtype: float64



- DataFrame : 여러 인덱스와 레이블이 지정된 열이 있는 NumPy 배열을 전달하여 생성


```python
dates = pd.date_range("20130101", periods = 6)
dates
df = pd.DataFrame(np.random.randn(6,4), index=dates, columns=list("ABCD")) #6행 4열
print(df)
```

                       A         B         C         D
    2013-01-01  0.865728  0.292457  1.067028 -0.253106
    2013-01-02 -1.909402  1.527000 -0.386110 -0.500735
    2013-01-03  0.075965  1.552591  1.350081 -1.812949
    2013-01-04 -0.887034 -0.790107 -1.427116  0.506210
    2013-01-05 -0.405688  0.656769  2.117183 -0.219086
    2013-01-06 -0.425787  1.433215  0.707955 -1.778100
    

- 시리즈와 같은 구조로 변환할 수 있는 객체 사전을 전달하여 생성


```python
df2 = pd.DataFrame(
    {
        "A" : 1.0,
        "B" : pd.Timestamp("20130102"),
        "C" : pd.Series(1, index=list(range(4)), dtype='float32'),
        "D" : np.array([3] * 4, dtype='int32'),
        "E" : pd.Categorical(["test","train", "test", "train"]),
        "F" : "foo",   
    }
)
print(df2)
print(df2.dtypes)
```

         A          B    C  D      E    F
    0  1.0 2013-01-02  1.0  3   test  foo
    1  1.0 2013-01-02  1.0  3  train  foo
    2  1.0 2013-01-02  1.0  3   test  foo
    3  1.0 2013-01-02  1.0  3  train  foo
    A           float64
    B    datetime64[ns]
    C           float32
    D             int32
    E          category
    F            object
    dtype: object
    

## 데이터 보기 

### 데이터의 상단 및 하단 행 보기


```python
print(df.head())
```

                       A         B         C         D
    2013-01-01  0.865728  0.292457  1.067028 -0.253106
    2013-01-02 -1.909402  1.527000 -0.386110 -0.500735
    2013-01-03  0.075965  1.552591  1.350081 -1.812949
    2013-01-04 -0.887034 -0.790107 -1.427116  0.506210
    2013-01-05 -0.405688  0.656769  2.117183 -0.219086
    


```python
print(df.tail(3))
```

                       A         B         C         D
    2013-01-04 -0.887034 -0.790107 -1.427116  0.506210
    2013-01-05 -0.405688  0.656769  2.117183 -0.219086
    2013-01-06 -0.425787  1.433215  0.707955 -1.778100
    

### 인덱스, 열 표시 

- 인덱스 표시


```python
print(df.index)
```

    DatetimeIndex(['2013-01-01', '2013-01-02', '2013-01-03', '2013-01-04',
                   '2013-01-05', '2013-01-06'],
                  dtype='datetime64[ns]', freq='D')
    

- 열 표시


```python
print(df.columns)
```

    Index(['A', 'B', 'C', 'D'], dtype='object')
    

- Numpy를 사용하여 차원형식으로 표현


```python
print(df.to_numpy())
```

    [[ 0.86572765  0.29245708  1.06702782 -0.25310621]
     [-1.9094016   1.5270004  -0.38610994 -0.5007352 ]
     [ 0.07596547  1.5525908   1.35008097 -1.81294929]
     [-0.88703364 -0.79010667 -1.42711619  0.50621017]
     [-0.40568757  0.65676859  2.11718261 -0.21908563]
     [-0.42578651  1.4332152   0.70795455 -1.77810017]]
    

- type이 여러가지인경우 상대적으로 비용이 많이든다.


```python
print(df2.to_numpy())
```

    [[1.0 Timestamp('2013-01-02 00:00:00') 1.0 3 'test' 'foo']
     [1.0 Timestamp('2013-01-02 00:00:00') 1.0 3 'train' 'foo']
     [1.0 Timestamp('2013-01-02 00:00:00') 1.0 3 'test' 'foo']
     [1.0 Timestamp('2013-01-02 00:00:00') 1.0 3 'train' 'foo']]
    

### 통계요약 


```python
print(df.describe())
```

                  A         B         C         D
    count  6.000000  6.000000  6.000000  6.000000
    mean  -0.447703  0.778654  0.571503 -0.676294
    std    0.930715  0.927330  1.278356  0.929863
    min   -1.909402 -0.790107 -1.427116 -1.812949
    25%   -0.771722  0.383535 -0.112594 -1.458759
    50%   -0.415737  1.044992  0.887491 -0.376921
    75%   -0.044448  1.503554  1.279318 -0.227591
    max    0.865728  1.552591  2.117183  0.506210
    

### 데이터 전치
- 행과 열을 서로 바꿈


```python
print(df.T)
```

       2013-01-01  2013-01-02  2013-01-03  2013-01-04  2013-01-05  2013-01-06
    A    0.865728   -1.909402    0.075965   -0.887034   -0.405688   -0.425787
    B    0.292457    1.527000    1.552591   -0.790107    0.656769    1.433215
    C    1.067028   -0.386110    1.350081   -1.427116    2.117183    0.707955
    D   -0.253106   -0.500735   -1.812949    0.506210   -0.219086   -1.778100
    

### 행으로 정렬 
- index를 기준으로 정렬
- 기본 방식은 오름차순
  - axis = 1 : 내림차순


```python
print(df.sort_index(axis=1, ascending=False))
```

                       D         C         B         A
    2013-01-01 -0.253106  1.067028  0.292457  0.865728
    2013-01-02 -0.500735 -0.386110  1.527000 -1.909402
    2013-01-03 -1.812949  1.350081  1.552591  0.075965
    2013-01-04  0.506210 -1.427116 -0.790107 -0.887034
    2013-01-05 -0.219086  2.117183  0.656769 -0.405688
    2013-01-06 -1.778100  0.707955  1.433215 -0.425787
    

### 열로 정렬 


```python
print(df.sort_values(by="B")) # B를 기준으로 오름차순
```

                       A         B         C         D
    2013-01-04 -0.887034 -0.790107 -1.427116  0.506210
    2013-01-01  0.865728  0.292457  1.067028 -0.253106
    2013-01-05 -0.405688  0.656769  2.117183 -0.219086
    2013-01-06 -0.425787  1.433215  0.707955 -1.778100
    2013-01-02 -1.909402  1.527000 -0.386110 -0.500735
    2013-01-03  0.075965  1.552591  1.350081 -1.812949
    

## 인덱싱 

### 단일 열 
- 결괏값이 Series로 나온다


```python
print(df["A"]) 
```

    2013-01-01    0.865728
    2013-01-02   -1.909402
    2013-01-03    0.075965
    2013-01-04   -0.887034
    2013-01-05   -0.405688
    2013-01-06   -0.425787
    Freq: D, Name: A, dtype: float64
    

- 행을 슬라이스 


```python
print(df[0:3]) # 1~3행 까지 인덱싱
```

                       A         B         C         D
    2013-01-01  0.865728  0.292457  1.067028 -0.253106
    2013-01-02 -1.909402  1.527000 -0.386110 -0.500735
    2013-01-03  0.075965  1.552591  1.350081 -1.812949
    

### 인덱스를 기준으로 해당 인덱스에 포함되는 열값 추출


```python
print(df.loc[dates[0]]) # 1행의 값을 열별로 구분
```

    A    0.865728
    B    0.292457
    C    1.067028
    D   -0.253106
    Name: 2013-01-01 00:00:00, dtype: float64
    

- 다중 열 추출


```python
print(df.loc[:, ["A", "B"]]) # A와 B열을 추출
```

                       A         B
    2013-01-01  0.865728  0.292457
    2013-01-02 -1.909402  1.527000
    2013-01-03  0.075965  1.552591
    2013-01-04 -0.887034 -0.790107
    2013-01-05 -0.405688  0.656769
    2013-01-06 -0.425787  1.433215
    

- 행의 범위안의 원하는 열 추출


```python
print(df.loc["20130102":"20130104",["A","B"]]) 
# 행을 슬라이싱하여 해당 행에 포함된 A,B열의 값을 추출
```

                       A         B
    2013-01-02 -1.909402  1.527000
    2013-01-03  0.075965  1.552591
    2013-01-04 -0.887034 -0.790107
    


```python
print(df.loc["20130102",["A","B"]]) 
# 해당되는 행의 크기 축소
```

    A   -1.909402
    B    1.527000
    Name: 2013-01-02 00:00:00, dtype: float64
    

- 스칼라값 얻기


```python
print(df.loc[dates[0],"A"])
# 1행과 A열에 포함되는 값 추출
# = df.at[dates[0],"A"]
```

    0.8657276483198485
    

### 위치별 추출


```python
print(df.iloc[3]) # 3번째 index에 해당하는 값 추출
```

    A   -0.887034
    B   -0.790107
    C   -1.427116
    D    0.506210
    Name: 2013-01-04 00:00:00, dtype: float64
    


```python
print(df.iloc[3:5, 0:2]) # 3~4번째 index에 해당하는 0~1번째 열
```

                       A         B
    2013-01-04 -0.887034 -0.790107
    2013-01-05 -0.405688  0.656769
    


```python
print(df.iloc[[1,2,4],[0,2]]) # 1,2,4번째 행의 0,2 번째 열 추출
```

                       A         C
    2013-01-02 -1.909402 -0.386110
    2013-01-03  0.075965  1.350081
    2013-01-05 -0.405688  2.117183
    


```python
print(df.iloc[1,1]) # 1행 1열값 추출
# = df.iat[1,1]
```

    1.5270003991486507
    

### Boolean indexing


```python
print(df[df["A"] > 0])
```

                       A         B         C         D
    2013-01-01  0.865728  0.292457  1.067028 -0.253106
    2013-01-03  0.075965  1.552591  1.350081 -1.812949
    

- isin()필터링 사용


```python
df2 = df.copy()
df2["E"]= ["one","one","two","three","four","three"]
print(df2[df2["E"].isin(["two","four"])])  
# E라는 열에 "two"와 "four"가 포함된 행을 추출
```

                       A         B         C         D     E
    2013-01-03  0.075965  1.552591  1.350081 -1.812949   two
    2013-01-05 -0.405688  0.656769  2.117183 -0.219086  four
    

### 설정 

- 새 열을 설정 하면 해당 인덱스별로 데이터가 자동으로 정렬 


```python
import pandas as pd
s1 = pd.Series([1, 2, 3, 4, 5, 6], index=pd.date_range("20130102", periods=6))
print(s1)
df["F"]=s1
```

    2013-01-02    1
    2013-01-03    2
    2013-01-04    3
    2013-01-05    4
    2013-01-06    5
    2013-01-07    6
    Freq: D, dtype: int64
    

- 인덱스 지정 값 설정


```python
df.at[dates[0],"A"] = 0
```

- 위치 지정 값 설정 


```python
df.iat[0,1] = 0
```

- Numpy 배열로 할당하여 설정 


```python
df.loc[:,"D"] = np.array([5] * len(df))
```


```python
print(df)
```

                       A         B         C  D    F
    2013-01-01  0.000000  0.000000  1.067028  5  NaN
    2013-01-02 -1.909402  1.527000 -0.386110  5  1.0
    2013-01-03  0.075965  1.552591  1.350081  5  2.0
    2013-01-04 -0.887034 -0.790107 -1.427116  5  3.0
    2013-01-05 -0.405688  0.656769  2.117183  5  4.0
    2013-01-06 -0.425787  1.433215  0.707955  5  5.0
    

- 설정이 있는 작업 


```python
df2 = df.copy()
df2[df2 > 0] = -df2
print(df2)
```

                       A         B         C  D    F
    2013-01-01  0.000000  0.000000 -1.067028 -5  NaN
    2013-01-02 -1.909402 -1.527000 -0.386110 -5 -1.0
    2013-01-03 -0.075965 -1.552591 -1.350081 -5 -2.0
    2013-01-04 -0.887034 -0.790107 -1.427116 -5 -3.0
    2013-01-05 -0.405688 -0.656769 -2.117183 -5 -4.0
    2013-01-06 -0.425787 -1.433215 -0.707955 -5 -5.0
    

## 누락된 데이터


```python
df1 = df.reindex(index=dates[0:4], columns=list(df.columns)+["E"])
df1.loc[dates[0] : dates[1],"E"] = 1
print(df1)
```

                       A         B         C  D    F    E
    2013-01-01  0.000000  0.000000  1.067028  5  NaN  1.0
    2013-01-02 -1.909402  1.527000 -0.386110  5  1.0  1.0
    2013-01-03  0.075965  1.552591  1.350081  5  2.0  NaN
    2013-01-04 -0.887034 -0.790107 -1.427116  5  3.0  NaN
    

###  누락된 데이터가 있는 행 삭제  
- dropna()
  - default = dropna(axis = 'index', how = 'any')
  - 인덱스 방향으로 훑으면서 nan값이 하나라도 있으면 해당 행 삭제


```python
print(df1.dropna(how="any"))
```

                       A      B        C  D    F    E
    2013-01-02 -1.909402  1.527 -0.38611  5  1.0  1.0
    

### 누락된 데이터 채우기
- fillna()


```python
print(df1.fillna(value=5)) 
# nan값을 value값으로 채운다
```

                       A         B         C  D    F    E
    2013-01-01  0.000000  0.000000  1.067028  5  5.0  1.0
    2013-01-02 -1.909402  1.527000 -0.386110  5  1.0  1.0
    2013-01-03  0.075965  1.552591  1.350081  5  2.0  5.0
    2013-01-04 -0.887034 -0.790107 -1.427116  5  3.0  5.0
    

### nan값이 존재하는지 확인
- pd.isna() 


```python
print(pd.isna(df1))
```

                    A      B      C      D      F      E
    2013-01-01  False  False  False  False   True  False
    2013-01-02  False  False  False  False  False  False
    2013-01-03  False  False  False  False  False   True
    2013-01-04  False  False  False  False  False   True
    

## Operations(작업) 

### 통계
- 일반적으로 누락된 데이터는 제외 


```python
df.mean()
# 기술통계
```




    A   -0.591991
    B    0.729911
    C    0.571503
    D    5.000000
    F    3.000000
    dtype: float64




```python
df.mean(1)
```




    2013-01-01    1.516757
    2013-01-02    1.046298
    2013-01-03    1.995727
    2013-01-04    0.979149
    2013-01-05    2.273653
    2013-01-06    2.343077
    Freq: D, dtype: float64



- 차원이 다르고 정렬이 필요한 개체로 작업 


```python
s=pd.Series([1,3,5,np.nan,6,8], index=dates).shift(2)
s
```




    2013-01-01    NaN
    2013-01-02    NaN
    2013-01-03    1.0
    2013-01-04    3.0
    2013-01-05    5.0
    2013-01-06    NaN
    Freq: D, dtype: float64



- 판다스는 지정된 차원을 자동으로 브로드캐스트한다 


```python
print(df.sub(s,axis="index"))
```

                       A         B         C    D    F
    2013-01-01       NaN       NaN       NaN  NaN  NaN
    2013-01-02       NaN       NaN       NaN  NaN  NaN
    2013-01-03 -0.924035  0.552591  0.350081  4.0  1.0
    2013-01-04 -3.887034 -3.790107 -4.427116  2.0  0.0
    2013-01-05 -5.405688 -4.343231 -2.882817  0.0 -1.0
    2013-01-06       NaN       NaN       NaN  NaN  NaN
    

### 데이터에 함수 입력 


```python
print(df.apply(np.cumsum))
```

                       A         B         C   D     F
    2013-01-01  0.000000  0.000000  1.067028   5   NaN
    2013-01-02 -1.909402  1.527000  0.680918  10   1.0
    2013-01-03 -1.833436  3.079591  2.030999  15   3.0
    2013-01-04 -2.720470  2.289485  0.603883  20   6.0
    2013-01-05 -3.126157  2.946253  2.721065  25  10.0
    2013-01-06 -3.551944  4.379468  3.429020  30  15.0
    


```python
df.apply(lambda x :x.max()-x.min())
```




    A    1.985367
    B    2.342697
    C    3.544299
    D    0.000000
    F    4.000000
    dtype: float64



### 히스토그램
- 분포정도


```python
s = pd.Series(np.random.randint(0,7,size=10))
s
```




    0    4
    1    0
    2    2
    3    2
    4    2
    5    5
    6    6
    7    3
    8    6
    9    0
    dtype: int64




```python
s.value_counts()
```




    2    3
    0    2
    6    2
    4    1
    5    1
    3    1
    dtype: int64



### 문자열 


```python
s = pd.Series(["A",'B','C','Aaba', 'Baca', np.nan, "CABA", "dog","cat"])
print(s.str.lower())
print("-----upper-----")
print(s.str.upper())
```

    0       a
    1       b
    2       c
    3    aaba
    4    baca
    5     NaN
    6    caba
    7     dog
    8     cat
    dtype: object
    -----upper-----
    0       A
    1       B
    2       C
    3    AABA
    4    BACA
    5     NaN
    6    CABA
    7     DOG
    8     CAT
    dtype: object
    

## 병합 
- Series 및 DataFrame을 쉽게 결합
- concat


```python
df = pd.DataFrame(np.random.randn(10,4))
print(df)
```

              0         1         2         3
    0  0.449724  0.286135  0.502216  0.573424
    1  0.777551 -0.485242  1.342152 -0.293918
    2 -1.760999  1.052294  0.699095  1.558663
    3  1.535162  1.099069  0.609733 -0.577464
    4  0.987425  0.175097 -0.239427  0.011823
    5 -0.804263  0.216801  0.135882 -0.252641
    6 -0.953844  0.527005 -0.209263 -1.696837
    7 -0.726548  0.974055 -0.660680 -0.950009
    8 -0.889739 -0.793810  0.403333 -0.295826
    9  0.001348 -2.033730 -0.657308 -0.347856
    


```python
pieces = [df[:3], df[3:7],df[7:]] # 리스트형식
pieces
```




    [          0         1         2         3
     0  0.449724  0.286135  0.502216  0.573424
     1  0.777551 -0.485242  1.342152 -0.293918
     2 -1.760999  1.052294  0.699095  1.558663,
               0         1         2         3
     3  1.535162  1.099069  0.609733 -0.577464
     4  0.987425  0.175097 -0.239427  0.011823
     5 -0.804263  0.216801  0.135882 -0.252641
     6 -0.953844  0.527005 -0.209263 -1.696837,
               0         1         2         3
     7 -0.726548  0.974055 -0.660680 -0.950009
     8 -0.889739 -0.793810  0.403333 -0.295826
     9  0.001348 -2.033730 -0.657308 -0.347856]




```python
print(pd.concat(pieces))
```

              0         1         2         3
    0  0.449724  0.286135  0.502216  0.573424
    1  0.777551 -0.485242  1.342152 -0.293918
    2 -1.760999  1.052294  0.699095  1.558663
    3  1.535162  1.099069  0.609733 -0.577464
    4  0.987425  0.175097 -0.239427  0.011823
    5 -0.804263  0.216801  0.135882 -0.252641
    6 -0.953844  0.527005 -0.209263 -1.696837
    7 -0.726548  0.974055 -0.660680 -0.950009
    8 -0.889739 -0.793810  0.403333 -0.295826
    9  0.001348 -2.033730 -0.657308 -0.347856
    

## Join
- db스타일이 병합
- merge


```python
left = pd.DataFrame({"Key":["foo","foo"], "lval":[1,2]})
right = pd.DataFrame({"Key":["foo","foo"], "rval":[4,5]})
print(left)
print('----right----')
print(right)
```

       Key  lval
    0  foo     1
    1  foo     2
    ----right----
       Key  rval
    0  foo     4
    1  foo     5
    


```python
print(pd.merge(left,right,on="Key"))
```

       Key  lval  rval
    0  foo     1     4
    1  foo     1     5
    2  foo     2     4
    3  foo     2     5
    


```python
left = pd.DataFrame({"Key":["foo","bar"], "lval":[1,2]})
right = pd.DataFrame({"Key":["foo","bar"], "rval":[4,5]})
print(left)
print('----right----')
print(right)
```

       Key  lval
    0  foo     1
    1  bar     2
    ----right----
       Key  rval
    0  foo     4
    1  bar     5
    


```python
print(pd.merge(left,right,on="Key"))
```

       Key  lval  rval
    0  foo     1     4
    1  bar     2     5
    

## Grouping
- 하나 이상을 포함하는 프로세스를 의미
  - 기준에 따라 데이터를 구룹으로 분할
  - 각 그룹에 독립적으로 기능 적용
  - 결과를 데이터 구조로 결합 


```python
df = pd.DataFrame(
    {
        "A": ["foo", "bar", "foo", "bar", "foo", "bar", "foo", "foo"],
        "B": ["one", "one", "two", "three", "two", "two", "one", "three"],
        "C": np.random.randn(8),
        "D": np.random.randn(8),
    }
)
print(df)
```

         A      B         C         D
    0  foo    one  0.844088 -0.974067
    1  bar    one -2.392914  0.557553
    2  foo    two  0.667617  0.410376
    3  bar  three  0.271053  1.160380
    4  foo    two  0.844380 -0.665977
    5  bar    two  0.366607  1.947910
    6  foo    one -0.480591  0.607410
    7  foo  three -1.137906 -0.628921
    

### A를 기준으로 그룹화 후 더하기 


```python
print(df.groupby("A").sum())
```

                C         D
    A                      
    bar -1.755254  3.665843
    foo  0.737587 -1.251179
    

### A와 B를 그룹화 후 더하기 


```python
print(df.groupby(["A","B"]).sum())
```

                      C         D
    A   B                        
    bar one   -2.392914  0.557553
        three  0.271053  1.160380
        two    0.366607  1.947910
    foo one    0.363496 -0.366657
        three -1.137906 -0.628921
        two    1.511997 -0.255601
    

## Reshaping 


```python
tuples = list(
    zip(
        *[
            ["bar", "bar", "baz", "baz", "foo", "foo", "qux", "qux"],
            ["one", "two", "one", "two", "one", "two", "one", "two"],
        ]
    )
)
```


```python
index = pd.MultiIndex.from_tuples(tuples, names=["first","second"])
df = pd.DataFrame(np.random.randn(8,2), index=index, columns=["A","B"])
df2 = df[:4]
print(df2)
```

                         A         B
    first second                    
    bar   one     2.536753 -0.409669
          two     0.248299  0.410299
    baz   one    -0.791332 -1.745028
          two    -1.678724 -0.540814
    

### 압축
- stacked()


```python
stacked = df2.stack()
stacked
```




    first  second   
    bar    one     A    2.536753
                   B   -0.409669
           two     A    0.248299
                   B    0.410299
    baz    one     A   -0.791332
                   B   -1.745028
           two     A   -1.678724
                   B   -0.540814
    dtype: float64



#### 역연산
- 기본적으로 마지막 레벨의 스택을 해제한다. 


```python
stacked.unstack()
```





  <div id="df-7e782d4e-2c2e-4d9f-84d9-fff75c75b680">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
    <tr>
      <th>first</th>
      <th>second</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">bar</th>
      <th>one</th>
      <td>2.536753</td>
      <td>-0.409669</td>
    </tr>
    <tr>
      <th>two</th>
      <td>0.248299</td>
      <td>0.410299</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">baz</th>
      <th>one</th>
      <td>-0.791332</td>
      <td>-1.745028</td>
    </tr>
    <tr>
      <th>two</th>
      <td>-1.678724</td>
      <td>-0.540814</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-7e782d4e-2c2e-4d9f-84d9-fff75c75b680')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-7e782d4e-2c2e-4d9f-84d9-fff75c75b680 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-7e782d4e-2c2e-4d9f-84d9-fff75c75b680');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
stacked.unstack(1)
```





  <div id="df-7102b4b7-9e7c-481f-ba6b-47189da0300a">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>second</th>
      <th>one</th>
      <th>two</th>
    </tr>
    <tr>
      <th>first</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">bar</th>
      <th>A</th>
      <td>2.536753</td>
      <td>0.248299</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-0.409669</td>
      <td>0.410299</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">baz</th>
      <th>A</th>
      <td>-0.791332</td>
      <td>-1.678724</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-1.745028</td>
      <td>-0.540814</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-7102b4b7-9e7c-481f-ba6b-47189da0300a')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-7102b4b7-9e7c-481f-ba6b-47189da0300a button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-7102b4b7-9e7c-481f-ba6b-47189da0300a');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
stacked.unstack(0)
```





  <div id="df-9ded9c36-310c-40d0-b603-267ce2d5171d">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>first</th>
      <th>bar</th>
      <th>baz</th>
    </tr>
    <tr>
      <th>second</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">one</th>
      <th>A</th>
      <td>2.536753</td>
      <td>-0.791332</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-0.409669</td>
      <td>-1.745028</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">two</th>
      <th>A</th>
      <td>0.248299</td>
      <td>-1.678724</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.410299</td>
      <td>-0.540814</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-9ded9c36-310c-40d0-b603-267ce2d5171d')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-9ded9c36-310c-40d0-b603-267ce2d5171d button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-9ded9c36-310c-40d0-b603-267ce2d5171d');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




### Pivot table
- 데이터프레임의 액셀화 

- 데이터 불러오기


```python
df = pd.DataFrame(
    {
        "A":["one", "one", "two", "three"] * 3,
        "B":["A","B","C"] * 4,
        "C":["foo", "foo", "foo", "bar", "bar", "bar"]*2,
        "D":np.random.randn(12),
        "E":np.random.randn(12),
    }
)
df
```





  <div id="df-fa05ce2d-067b-468a-ba23-e4cfdde96e51">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>one</td>
      <td>A</td>
      <td>foo</td>
      <td>0.472353</td>
      <td>1.319584</td>
    </tr>
    <tr>
      <th>1</th>
      <td>one</td>
      <td>B</td>
      <td>foo</td>
      <td>0.814895</td>
      <td>0.186319</td>
    </tr>
    <tr>
      <th>2</th>
      <td>two</td>
      <td>C</td>
      <td>foo</td>
      <td>-1.231097</td>
      <td>0.146430</td>
    </tr>
    <tr>
      <th>3</th>
      <td>three</td>
      <td>A</td>
      <td>bar</td>
      <td>-0.048371</td>
      <td>0.301440</td>
    </tr>
    <tr>
      <th>4</th>
      <td>one</td>
      <td>B</td>
      <td>bar</td>
      <td>0.118259</td>
      <td>-0.269829</td>
    </tr>
    <tr>
      <th>5</th>
      <td>one</td>
      <td>C</td>
      <td>bar</td>
      <td>1.188139</td>
      <td>-1.339077</td>
    </tr>
    <tr>
      <th>6</th>
      <td>two</td>
      <td>A</td>
      <td>foo</td>
      <td>1.183869</td>
      <td>-0.878976</td>
    </tr>
    <tr>
      <th>7</th>
      <td>three</td>
      <td>B</td>
      <td>foo</td>
      <td>-0.419601</td>
      <td>0.990978</td>
    </tr>
    <tr>
      <th>8</th>
      <td>one</td>
      <td>C</td>
      <td>foo</td>
      <td>-0.613792</td>
      <td>-1.098215</td>
    </tr>
    <tr>
      <th>9</th>
      <td>one</td>
      <td>A</td>
      <td>bar</td>
      <td>-0.002902</td>
      <td>-0.330832</td>
    </tr>
    <tr>
      <th>10</th>
      <td>two</td>
      <td>B</td>
      <td>bar</td>
      <td>-0.253640</td>
      <td>0.929601</td>
    </tr>
    <tr>
      <th>11</th>
      <td>three</td>
      <td>C</td>
      <td>bar</td>
      <td>-0.666981</td>
      <td>-0.285138</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-fa05ce2d-067b-468a-ba23-e4cfdde96e51')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-fa05ce2d-067b-468a-ba23-e4cfdde96e51 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-fa05ce2d-067b-468a-ba23-e4cfdde96e51');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




- 피벗테이블 만들기 


```python
# A와 B의 컬럼으로 그룹바이를 하는데 컬럼명은 C, values값은 D로한다.
pd.pivot_table(df, values="D", index=["A","B"], columns=["C"])
```





  <div id="df-a59c0ebb-b0bf-477a-90e0-523290a3d371">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>C</th>
      <th>bar</th>
      <th>foo</th>
    </tr>
    <tr>
      <th>A</th>
      <th>B</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">one</th>
      <th>A</th>
      <td>-0.002902</td>
      <td>0.472353</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.118259</td>
      <td>0.814895</td>
    </tr>
    <tr>
      <th>C</th>
      <td>1.188139</td>
      <td>-0.613792</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">three</th>
      <th>A</th>
      <td>-0.048371</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>B</th>
      <td>NaN</td>
      <td>-0.419601</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-0.666981</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">two</th>
      <th>A</th>
      <td>NaN</td>
      <td>1.183869</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-0.253640</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>C</th>
      <td>NaN</td>
      <td>-1.231097</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-a59c0ebb-b0bf-477a-90e0-523290a3d371')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-a59c0ebb-b0bf-477a-90e0-523290a3d371 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-a59c0ebb-b0bf-477a-90e0-523290a3d371');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




## Time series
- pandas는 시간변환에 엄청 강하고 효율적이다 


```python
rng = pd.date_range("1/1/2012", periods=100, freq="S") # Second단위
ts = pd.Series(np.random.randint(0,500,len(rng)), index=rng)
ts.resample("5Min").sum()
```




    2012-01-01    25887
    Freq: 5T, dtype: int64



### 시간 표현 


```python
rng = pd.date_range("3/6/2012 00:00", periods=5, freq="D") # Day단위
ts = pd.Series(np.random.randn(len(rng)), rng)
ts
```




    2012-03-06   -1.056279
    2012-03-07    1.689753
    2012-03-08    0.581104
    2012-03-09    0.274412
    2012-03-10   -0.611934
    Freq: D, dtype: float64




```python
# 협정시계시
ts_utc = ts.tz_localize("UTC")
ts_utc
```




    2012-03-06 00:00:00+00:00   -1.056279
    2012-03-07 00:00:00+00:00    1.689753
    2012-03-08 00:00:00+00:00    0.581104
    2012-03-09 00:00:00+00:00    0.274412
    2012-03-10 00:00:00+00:00   -0.611934
    Freq: D, dtype: float64



### 다른 시간대로 변환 


```python
# 미국 동부로 시간변환
ts_utc.tz_convert("US/Eastern")
```




    2012-03-05 19:00:00-05:00   -1.056279
    2012-03-06 19:00:00-05:00    1.689753
    2012-03-07 19:00:00-05:00    0.581104
    2012-03-08 19:00:00-05:00    0.274412
    2012-03-09 19:00:00-05:00   -0.611934
    Freq: D, dtype: float64



### 시간범위 표현 간 변환


```python
rng = pd.date_range("1/1/2012", periods=5,freq="M") # Month 단위
ts = pd.Series(np.random.randn(len(rng)),index=rng)
ts
```




    2012-01-31    1.219098
    2012-02-29   -0.532026
    2012-03-31    0.642991
    2012-04-30    0.993084
    2012-05-31   -0.744262
    Freq: M, dtype: float64




```python
ps = ts.to_period() # 달까지 표시하겠다
ps
```




    2012-01    1.219098
    2012-02   -0.532026
    2012-03    0.642991
    2012-04    0.993084
    2012-05   -0.744262
    Freq: M, dtype: float64




```python
ps.to_timestamp()
```




    2012-01-01    1.219098
    2012-02-01   -0.532026
    2012-03-01    0.642991
    2012-04-01    0.993084
    2012-05-01   -0.744262
    Freq: MS, dtype: float64



### 마침표와 타임스탬프 사이 변환 


```python
prng = pd.period_range("1990Q1","2000Q4", freq="Q-NOV")
ts = pd.Series(np.random.randn(len(prng)),prng)
ts.index = (prng.asfreq("M","e")+1).asfreq("H","s")+9
ts.head()
```




    1990-03-01 09:00    1.084262
    1990-06-01 09:00   -0.958435
    1990-09-01 09:00    1.222262
    1990-12-01 09:00   -0.644455
    1991-03-01 09:00   -0.278623
    Freq: H, dtype: float64



## 범주(Categoricals)
- 범주형 데이터를 DataFrame으로 부른다 


```python
df = pd.DataFrame(
     {"id": [1, 2, 3, 4, 5, 6], "raw_grade": ["a", "b", "b", "a", "a", "e"]}
)

```


```python
df["grade"]=df["raw_grade"].astype("category") # grade라는 Series에 카테고리 생성해주기
df["grade"]
```




    0    a
    1    b
    2    b
    3    a
    4    a
    5    e
    Name: grade, dtype: category
    Categories (3, object): ['a', 'b', 'e']




```python
df["grade"].cat.categories=["very good", "good", "very bad"]
```

- 범주를 재정렬 후 누락된 범주 추가


```python
df["grade"] = df["grade"].cat.set_categories(
    ["very bad", "bad", "medium", "good", "very good"]
)

df["grade"]
```




    0    very good
    1         good
    2         good
    3    very good
    4    very good
    5     very bad
    Name: grade, dtype: category
    Categories (5, object): ['very bad', 'bad', 'medium', 'good', 'very good']



- 정렬은 범주의 순서에 따라 이루어진다 


```python
df.sort_values(by="grade") # grade 범주 순으로 정렬
```





  <div id="df-7950f959-d73a-49fb-b9f3-31dcceafff7d">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>raw_grade</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>e</td>
      <td>very bad</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>b</td>
      <td>good</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>b</td>
      <td>good</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>a</td>
      <td>very good</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>a</td>
      <td>very good</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>a</td>
      <td>very good</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-7950f959-d73a-49fb-b9f3-31dcceafff7d')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-7950f959-d73a-49fb-b9f3-31dcceafff7d button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-7950f959-d73a-49fb-b9f3-31dcceafff7d');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




- 범주형 열을 기준으로 그룹화하면 빈 범주도 표시 


```python
df.groupby("grade").size() # bad, medium도 표시된다
```




    grade
    very bad     1
    bad          0
    medium       0
    good         2
    very good    3
    dtype: int64



## 시각화 


```python
import matplotlib.pyplot as plt
plt.close("all")
```


```python
ts = pd.Series(np.random.randn(1000), index=pd.date_range("1/1/2000",periods=1000))
ts = ts.cumsum() # 누적합 구하기
ts.plot()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f49f08c3910>




    
![png](/images/assignment/Pandas/output_142_1.png)
    


- plot()메서드는 레이블이 있는 모든열을 그리는데 편리 


```python
df = pd.DataFrame(
    np.random.randn(1000,4), index=ts.index, columns=["A","B","C","D"]
)
df = df.cumsum()
df.plot()
plt.legend(loc='best'); # 범례 추가
```


    
![png](/images/assignment/Pandas/output_144_0.png)
    


## 데이터 입출력
  

### csv 파일 쓰기



```python
df.to_csv("foo.csv")
```

### csv 파일에서 읽기 


```python
pd.read_csv("foo.csv")
```





  <div id="df-68336ae4-99f1-418e-b521-f47bcd21d551">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000-01-01</td>
      <td>0.060692</td>
      <td>0.105831</td>
      <td>1.634998</td>
      <td>0.772662</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2000-01-02</td>
      <td>0.504047</td>
      <td>0.861909</td>
      <td>0.919295</td>
      <td>1.285729</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2000-01-03</td>
      <td>0.147256</td>
      <td>2.801748</td>
      <td>1.466028</td>
      <td>0.051882</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2000-01-04</td>
      <td>-0.188261</td>
      <td>1.605617</td>
      <td>3.807387</td>
      <td>0.548725</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000-01-05</td>
      <td>-1.284756</td>
      <td>1.304981</td>
      <td>4.781101</td>
      <td>0.764170</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>995</th>
      <td>2002-09-22</td>
      <td>67.967114</td>
      <td>16.397385</td>
      <td>0.346370</td>
      <td>-42.046715</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2002-09-23</td>
      <td>68.446463</td>
      <td>17.084053</td>
      <td>1.419101</td>
      <td>-41.482823</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2002-09-24</td>
      <td>67.728754</td>
      <td>16.569164</td>
      <td>2.337529</td>
      <td>-41.447092</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2002-09-25</td>
      <td>66.412904</td>
      <td>16.833811</td>
      <td>3.513496</td>
      <td>-41.535883</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2002-09-26</td>
      <td>69.982266</td>
      <td>15.368470</td>
      <td>2.753197</td>
      <td>-42.219712</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 5 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-68336ae4-99f1-418e-b521-f47bcd21d551')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-68336ae4-99f1-418e-b521-f47bcd21d551 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-68336ae4-99f1-418e-b521-f47bcd21d551');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




### HDF5 파일 쓰기 


```python
df.to_hdf("foo.h5","df")
```

### HDF5 파일 읽기 


```python
pd.read_hdf("foo.h5","df")
```





  <div id="df-251bd0cf-e0ab-472e-8ca9-f2462a84c5b3">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-01-01</th>
      <td>0.060692</td>
      <td>0.105831</td>
      <td>1.634998</td>
      <td>0.772662</td>
    </tr>
    <tr>
      <th>2000-01-02</th>
      <td>0.504047</td>
      <td>0.861909</td>
      <td>0.919295</td>
      <td>1.285729</td>
    </tr>
    <tr>
      <th>2000-01-03</th>
      <td>0.147256</td>
      <td>2.801748</td>
      <td>1.466028</td>
      <td>0.051882</td>
    </tr>
    <tr>
      <th>2000-01-04</th>
      <td>-0.188261</td>
      <td>1.605617</td>
      <td>3.807387</td>
      <td>0.548725</td>
    </tr>
    <tr>
      <th>2000-01-05</th>
      <td>-1.284756</td>
      <td>1.304981</td>
      <td>4.781101</td>
      <td>0.764170</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2002-09-22</th>
      <td>67.967114</td>
      <td>16.397385</td>
      <td>0.346370</td>
      <td>-42.046715</td>
    </tr>
    <tr>
      <th>2002-09-23</th>
      <td>68.446463</td>
      <td>17.084053</td>
      <td>1.419101</td>
      <td>-41.482823</td>
    </tr>
    <tr>
      <th>2002-09-24</th>
      <td>67.728754</td>
      <td>16.569164</td>
      <td>2.337529</td>
      <td>-41.447092</td>
    </tr>
    <tr>
      <th>2002-09-25</th>
      <td>66.412904</td>
      <td>16.833811</td>
      <td>3.513496</td>
      <td>-41.535883</td>
    </tr>
    <tr>
      <th>2002-09-26</th>
      <td>69.982266</td>
      <td>15.368470</td>
      <td>2.753197</td>
      <td>-42.219712</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 4 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-251bd0cf-e0ab-472e-8ca9-f2462a84c5b3')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-251bd0cf-e0ab-472e-8ca9-f2462a84c5b3 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-251bd0cf-e0ab-472e-8ca9-f2462a84c5b3');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




###  엑셀 파일 쓰기 


```python
df.to_excel("foo.xlsx",sheet_name="sheet1")
```

### 엑셀 파일 읽기 


```python
pd.read_excel("foo.xlsx", "sheet1", index_col=None, na_values=["NA"]) # 결측치를 NA로 표시
```





  <div id="df-935c1612-11ff-4175-b303-402eea5e8869">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000-01-01</td>
      <td>0.060692</td>
      <td>0.105831</td>
      <td>1.634998</td>
      <td>0.772662</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2000-01-02</td>
      <td>0.504047</td>
      <td>0.861909</td>
      <td>0.919295</td>
      <td>1.285729</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2000-01-03</td>
      <td>0.147256</td>
      <td>2.801748</td>
      <td>1.466028</td>
      <td>0.051882</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2000-01-04</td>
      <td>-0.188261</td>
      <td>1.605617</td>
      <td>3.807387</td>
      <td>0.548725</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000-01-05</td>
      <td>-1.284756</td>
      <td>1.304981</td>
      <td>4.781101</td>
      <td>0.764170</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>995</th>
      <td>2002-09-22</td>
      <td>67.967114</td>
      <td>16.397385</td>
      <td>0.346370</td>
      <td>-42.046715</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2002-09-23</td>
      <td>68.446463</td>
      <td>17.084053</td>
      <td>1.419101</td>
      <td>-41.482823</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2002-09-24</td>
      <td>67.728754</td>
      <td>16.569164</td>
      <td>2.337529</td>
      <td>-41.447092</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2002-09-25</td>
      <td>66.412904</td>
      <td>16.833811</td>
      <td>3.513496</td>
      <td>-41.535883</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2002-09-26</td>
      <td>69.982266</td>
      <td>15.368470</td>
      <td>2.753197</td>
      <td>-42.219712</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 5 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-935c1612-11ff-4175-b303-402eea5e8869')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-935c1612-11ff-4175-b303-402eea5e8869 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-935c1612-11ff-4175-b303-402eea5e8869');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>



