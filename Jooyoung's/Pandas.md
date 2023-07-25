
- 파이썬에서 사용하는 데이터 분석 라이브러리
- 2차원 데이터를 주로 분석
```python
import pandas as pd
```

--- 
# 1. Series
- 1차원 데이터를 의미
	- 정수, 실수, 문자열등

## Series 객체 생성
- ex) 1월부터 4월까지 평균 온도 데이터(-20, -10, 10, 20)
```python
temp = pd.Series([-20,-10,10,20])
```

- result

|index|value|
|---|---|
|0|-20|
|1|-10|
|2|10|
|3|20|

```python
print(temp[0])
# -20 출력
```
- 리스트 인덱스 접근하듯 사용 가능

### Index를 지정하여 Series객체 생성
```python
temp = pd.Series([-20,-10,10,20], index=['Jan', 'Feb', 'Mar', 'Apr'])
```

- result

|index|value|
|---|---|
|Jan|-20|
|Feb|-10|
|Mar|10|
|Apr|20|

- 인덱스의 이름을 지정하였으므로 딕셔너리처럼 접근 가능
```python
print(temp['Jan'])
#-20출력
```

--- 
# 2. DataFrame
- 2차원 데이터(Series들의 모음)
- 딕셔너리 자료구조를 통해 생성가능
	- 예) 슬램덩크 주요 인물 8명에 대한 데이터
```python
data = { 
		'이름' : ['채치수', '정대만', '송태섭', '서태웅', '강백호', '변덕규', '황태산', '윤대협'], 
		'학교' : ['북산고', '북산고', '북산고', '북산고', '북산고', '능남고', '능남고', '능남고'], 
		'키' : [197, 184, 168, 187, 188, 202, 188, 190], '국어' : [90, 40, 80, 40, 15, 80, 55, 100], '영어' : [85, 35, 75, 60, 20, 100, 65, 85], 
		'수학' : [100, 50, 70, 70, 10, 95, 45, 90], 
		'과학' : [95, 55, 80, 75, 35, 85, 40, 95], 
		'사회' : [85, 25, 75, 80, 10, 80, 35, 95], 
		'SW특기' : ['Python', 'Java', 'Javascript', '', '', 'C', 'PYTHON', 'C#'] }
```

## DataFrame 객체 생성
```python
#data는 위의 딕셔너리
df = pd.DataFrame(data)
```

- 출력 결과
![[[스크린샷 2023-07-25 오후 9.04.18.png](https://github.com/soyesenna/DataAnalysisStudy/blob/main/Jooyoung's/resource/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202023-07-25%20%EC%98%A4%ED%9B%84%209.04.18.png)]]

### 데이터 접근
```python
print(df['이름'])
'''
0    채치수
1    정대만
2    송태섭
3    서태웅
4    강백호
5    변덕규
6    황태산
7    윤대협
Name: 이름, dtype: object
'''
```

```python
print([['이름', '키']])
'''
    이름    키
0  채치수  197
1  정대만  184
2  송태섭  168
3  서태웅  187
4  강백호  188
5  변덕규  202
6  황태산  188
7  윤대협  190
'''
```
- 두개 이상의 컬럼을 가져오려면 키들을 리스트로 감싸서 전달해야함

## DataFrame 객체 생성(Column지정)
- data중에서 원하는 column만 선택하거나 순서 변경 가능
```python
df = pd.DataFrame(data, columns=['이름', '학교', '키'])
print(df)
'''
    이름   학교    키
0  채치수  북산고  197
1  정대만  북산고  184
2  송태섭  북산고  168
3  서태웅  북산고  187
4  강백호  북산고  188
5  변덕규  능남고  202
6  황태산  능남고  188
7  윤대협  능남고  190
'''
```

--- 
# 3. Index
- 데이터에 접근할 수 있는 주소 값
- Series나 DataFrame에서 Index를 임의 지정 가능
	- 기본 Index는 0부터 시작하는 정수값
```python
print(df.index)
# 인덱스들 모두 출력
#RangeIndex(start=0, stop=8, step=1)
```

## Index 이름 설정
```python
df.index.name = '지원번호'
print(df)
'''
       이름   학교    키   국어   영어   수학  과학  사회        SW특기
지원번호                                                  
0     채치수  북산고  197   90   85  100  95  85      Python
1     정대만  북산고  184   40   35   50  55  25        Java
2     송태섭  북산고  168   80   75   70  80  75  Javascript
3     서태웅  북산고  187   40   60   70  75  80            
4     강백호  북산고  188   15   20   10  35  10            
5     변덕규  능남고  202   80  100   95  85  80           C
6     황태산  능남고  188   55   65   45  40  35      PYTHON
7     윤대협  능남고  190  100   85   90  95  95          C#
'''
```

## Index 초기화
```python
df.reset_index()
```
- 원래 있던 Index를 Column으로 넘겨버리고 RangeIndex(0부터 시작하는 정수값)으로 초기화

```python
df.reset_index(drop=True, inplace=True)
```
- drop 파라미터를 True로 하면 원래 있던 Index를 버림
- inplace 파라미터를 이용해 실제 데이터에 바로 반영
	- inplace가 False일 경우는 실제 데이터에 반영되지 않음

## Index 설정
- 지정한 column으로 Index를 설정
```python
df.set_index('이름', inplace=True)
print(df)
'''
      학교    키   국어   영어   수학  과학  사회        SW특기
이름                                              
채치수  북산고  197   90   85  100  95  85      Python
정대만  북산고  184   40   35   50  55  25        Java
송태섭  북산고  168   80   75   70  80  75  Javascript
서태웅  북산고  187   40   60   70  75  80            
강백호  북산고  188   15   20   10  35  10            
변덕규  능남고  202   80  100   95  85  80           C
황태산  능남고  188   55   65   45  40  35      PYTHON
윤대협  능남고  190  100   85   90  95  95          C#
'''
```

## Index 정렬
- Index를 기준으로 오름차순, 내림차순 설정
```python
df.sort_index(inplace=True)
print(df)
'''
      학교    키   국어   영어   수학  과학  사회        SW특기
이름                                              
강백호  북산고  188   15   20   10  35  10            
변덕규  능남고  202   80  100   95  85  80           C
서태웅  북산고  187   40   60   70  75  80            
송태섭  북산고  168   80   75   70  80  75  Javascript
윤대협  능남고  190  100   85   90  95  95          C#
정대만  북산고  184   40   35   50  55  25        Java
채치수  북산고  197   90   85  100  95  85      Python
황태산  능남고  188   55   65   45  40  35      PYTHON
'''
```
- 오름차순 정렬

```python
df.sort_index(ascending=False,inplace=True)
print(df)
'''
      학교    키   국어   영어   수학  과학  사회        SW특기
이름                                              
황태산  능남고  188   55   65   45  40  35      PYTHON
채치수  북산고  197   90   85  100  95  85      Python
정대만  북산고  184   40   35   50  55  25        Java
윤대협  능남고  190  100   85   90  95  95          C#
송태섭  북산고  168   80   75   70  80  75  Javascript
서태웅  북산고  187   40   60   70  75  80            
변덕규  능남고  202   80  100   95  85  80           C
강백호  북산고  188   15   20   10  35  10            
'''
```
- ascending 파라미터가 False면 내림차순 정렬

--- 
# 4. 파일 저장 및 열기
- DataFrame 객체를 excel, csv, txt 등 형태의 파일로 저장 및 열기

## 저장하기
- csv 파일로 저장
```python
df.to_csv('score.csv', encoding='utf-8-sig')
```
- 한글이 꺠지지 않기 위해 utf-8 인코딩 지정

- 파라미터에 파일 명을 지정
```python
df.to_csv('score.csv', index=False)
```
- 인덱스를 제외하고 저장

- txt파일로 저장
```python
df.to_csv('score.txt', sep='\t')
```
- sep 파라미터로 구분자 선택 가능

- 엑셀 파일로 저장
```python
df.to_excel('score.xlsx')
```

## 열기
- csv파일 열기
```python
df = pd.read_csv('score.csv', skiprows=1)
```
- 지정된 개수만큼의 row를 건너뜀

```python
df = pd.read_csv('score.csv', skiprows=[1,3,5])
```
- 1, 3, 5 row는 제외(row는 0부터 시작)

```python
df = pd.read_csv('score.csv', nrows=4)
```
- 4개의 row만 가져오기

```python
df = pd.read_csv('score.csv', skiprows=2, nrows=4)
```
- 2개의 row 스킵 후 4개 row가져오기

- 엑셀 파일 열기
```python
df = pd.read_excel('score.xlsx')
```

--- 
# 5. 데이터 확인

## DataFrame 확인
```python
df.describe()
```
- 계산 가능한 데이터에 대해 Column 별로 데이터의 갯수, 평균, 표준편차, 최소/최대값등의 정보를 보여줌

![[스크린샷 2023-07-25 오후 9.39.29.png]]

```python 
df.info()
```
- 각 Column에 대해 타입, 메모리등의 정보를 보여줌

```python
df.head()
#df.head(7) -> 7개 가져옴
```
- 처음 5개의 row를 가져옴

```python
df.tail()
#df.tail(3) -> 마지막 3개 가져옴
```
- 마지막 5개의 row를 가져옴

```python
df.values
```
- DataFrame을 array로 변환해서 보여줌

```python
df.index
```
- 현재 인덱스를 보여줌

```python
df.columns
```
- 현재 DataFrame의 Column 이름을 보여줌

```python
df.shape
```
- DataFrame의 형태(2차원 튜플형태)로 보여줌
- row, column 개수(row, column)

## Series 확인
```python
df['키'].describe()
df['키'].min()
df['키'].nlargest(3) #키가 제일 큰 순서대로 3개
df['키'].mean()
df['키'].sum()
df['SW특기'].count()
df['학교'].unique() #중복을 제외한 데이터
df['학교'].nuniaue() #중복을 제외한 데이터의 개수s
```
