
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

--- 
# 6. 데이터 선택(기본)

## Column 선택
```pyhon
df['키]
df['이름']
df[['이름', '키']]
```

## Column 선택(정수 Index)
```python
print(df.columns[0])
# 이름
print(df[df.columns[0]])
# == df['이름']
```

## 슬라이싱
```python
df['영어'][0:4]
#0~4까지 영어 점수 데이터 가져옴
```

--- 
# 7. 데이터 선택(loc)
- 이름을 이용하여 원하는 row에서 원하는 col선택

```python
df.loc['1번']
# 1번(index)값의 모든 row가져옴

df.loc['1번', '국어']
#index 1번에 해상하는 국어 데이터

df.loc[['1번', '2번'], '영어']
#index 1,2번에 해당하는 영어 데이터

df.loc[['1번', '2번'], ['영어', '수학']]
#index 1,2번에 해당하는 영어,수학 데이터

df.loc['1번':'5번', '국어':'사회']
#index 1번부터 5번까지, 국어부터 사회까지
#슬라이싱과 다르게 마지막 포함
```

--- 
# 8. 데이터 선택(iloc)
- 위치(정수)를 이용하여 원하는 row에서 원하는 col 선택

```python
df.iloc[0]
#0 번째 위치의 데이터(row)

df.iloc[0:5]
#0~4번째 위치의 데이터

df.iloc[0, 1]
#0번째 위치의 1번째(학교) 데이터

df.iloc[4, 2]
#5번학생의 키 데이터

df.iloc[[0,1], [2]]
#0,1번째위치의 학생의 2번째(키)데이터 

df.iloc[0:5, 3:8]
#0~4번째 위치의 학생중에서, 3~7번째 데이터
```

--- 
# 9. 데이터 선택(조건)
- 조건에 해당하는 데이터 선택

```python
df['키'] >= 185
#학생들의 키가 185이상이지 여부를 True/False로 알려줌

filt = (df['키'] >= 185)
print(df[filt])
#키가 185이상인 데이터만 가져옴
print(df[~filt])
#filt를 역으로 적용

df.loc[df['키'] >= 185, '수학']
#키가 185잇앙인 학생들의 수학데이터
```

## 다양한 조건
### & 그리고
```python
df.loc[df['키'] >= 185 & df['학교'] == '북산고']
#키가 185이상인 북산고 학생 데이터
```

### | 또는
```python
df.loc[(df['키'] < 170) | df['키'] > 200]
#키가 170미만이거나 키가 200초과인 학생데이터
```

### str 함수
```python
filt = df['이름'].str.startwith('송')
print(df[filt])
# '송'씨 성을 가진 사람

filt = df['이름'].str.contiains('태')
print(df[filt])
#이름에 태가 들어가는 사람

langs = ['Python', 'Java']
filt = df['SW특기'].isin(langs)
#sw 특기가 python이거나 java인 사람
#문자열이 완벽히 일치해야만 가져옴(대소문자 구분)

langs = ['python', 'java']
filt = df['SW특기'].str.lower().isin(langs)
#소문자로 변환후 비교

df['SW특기'].str.contains('java', na=True)
#Nan 데이터(없는 데이터)에 대해서 True 적용
```

--- 

# 10. 결측치
- 비어있는 데이터(NaN)

## 데이터 채우기 fillna
```python
df.fillna('', inplace=True)
#모든 NaN데이터를 빈칸으로 채움

df['SW특기'].fillna('없음', inplace=True)
#SW특기 Col의 데이터의 NaN만 채움
```

## 데이터 제외하기 dropna
```python
df.dropna()
#전체 데이터 중에서 NaN을 포함하는 데이터 삭제
```

- axis : index or column
    - index : NaN이 포함된 row를 지움
    - columns : NaN이 포함된 column을 지움
- how : any or all
    - any : NaN이 하나라도 있으면 지움
    - all : 모든 칸이 NaN이어야 지움
```python
df.dropna(axis='index', how='any')
#NaN이 하나라도 있는 row지움
```

--- 
# 11. 데이터 정렬

```python
df.sort_values("키")
#키순으로 오름차순 정렬

df.sort_values('키', ascending=False)
#키순으로 내림차순 정렬

df.sort_values(['수학', '영어'], ascending=False)
#수학점수로 내림차순 정렬하다가 같으면 영어 점수로 내림차순 정렬

df.sort_values(['수학', '영어'], ascending=[True, False])
#수학점수는 오름차순, 영어점수는 내림차순으로 정렬

df.sort_index()
#index를 기준으로 오름차순 정렬
```

--- 
# 12. 데이터 수정

## Column 수정
```python
df['학교'].replace({'북산고':'상북고', '능담고':'무슨고'}, inplcae=True)
#학교 col의 북산고를 상북고로 능담고를 무슨고로 바꿈

df['SW특기'] = df['SW특기'].str.lower()
#sw특기의 모든 col을 소문자로 바꿈

df['학교'] = df['학교'] + '등학교'
#학교데이터 + 등학교
```

## Column 추가
```python
df['총합'] = df['국어'] + df['영어']
#없는 col은 알아서 추가함

df['결과'] = 'Fail'
#결과 col을 추가하고 전체 데이터는 Fail 로 초기화
df.loc[df['총합'] > 400, '결과', 'Pass']
#총합이 400보다 큰 데이터에 대해서 결과를 Pass로 업데이트
```

## Column 삭제
```python
df.drop(columns=['총합','영어'])
#총합, 영어 col을 삭제
```

## row 삭제
```python
df.drop(index='4번')
#4번 학생 데이터 row를 삭제

filt = df['수학'] < 80
df.drop(index=df[filt].index)
#수학 점수가 80미만인 row 전부 지움
```

## row 추가
```python
df.loc['9번'] = ['이정환', '해남고등학교', 184, 90,90,90,90,90,'Kotlin', 450, 'Pass']
#새로운 row추가
```

## Cell 수정
```python
df.loc['4번', 'SW특기'] = 'Python'
#4번학생의 특기를 python으로 변경

df.loc['5번', ['학교', 'SW특기']] = ['능담고등학교', 'C']
#5번학생의 학교는 능담고등학교, 특기는 C로 변경
```

## Column순서 변경
```python
cols = list(df.columns)
df = df[[cols[-1]] + cols[0:-1]]
```

## Column 이름 변경
```python
df.columns = ['Result', 'Name', 'School']
```

--- 
# 13. 함수 적용

## 데이터에 함수 적용(apply)
```python
#키 뒤에 cm를 붙이는 역할
def add_cm(height):
	return str(height) + 'cm'

df['키'] = df['키'].apply(add_cm)
#키 데이터에 대해서 add_cm 함수를 호출한 결과 데이터를 반영
```

```python
def capitalize(lang):
	if pd.notnull(lang): #NaN인지 아닌지
		return lang.capitalize() #첫글자는 대문자로 나머지는 소문자로

df['SW특기'] = df['SW특기'].apply(capitalize)
```

--- 
# 14. 그룹화
- 동일한 값을 가진 것들끼리 합쳐서 통계 또는 평균등의 값을 계산하기 위해 사용
```python
df.groupby('학교').get_group('능담고')
df.groupby('학교').mean() #계산 가능한 데이터들의 평균값
df.groupby('학교').size() #각 그룹의 크기
df.groupby('학교').size()['능담고'] #학교로 그룹하를 한 뒤에 능담고에 해당하는 데이터의 수
df.groupby('학교')['키'].mean() #학교로 그룹화를 한 뒤에 키의 평균데이터
df.groupby('학교')[['국어', '수학', '영어']].mean() #학교로 그룹화를 한 뒤에 국어, 여어 수학 평균 데이터
```

```python
df.groupby(['학교', '학년']).mean() #학교별, 학년별 평균 데이터
```

```python
school = df.groupby('학교')
school['학년'].value_counts().loc['능담고']
#학교로 그룹화를 한뒤에 북산고에 대해서 학년별 학생 수를 가져옴

school['학년'].value_counts(normalize=True).loc['능담고']
#학생들의 수 데이터를 퍼센트로 비교하여 가져옴
```

--- 
