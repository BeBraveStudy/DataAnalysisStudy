--- 
- 다양한 형태의 그래프를 통해서 데이터 시각화를 할 수 있는 라이브러리

# 1. 그래프 기본
```python
import matplotlib.pyplot as plt

x = [1,2,3]
y = [2,4,8]
plt.plot(x,y)
```

## Title 설정
```python
plt.plot(x,y)
plt.title("line graph") #제목 설정
```

## 폰트 설정
```python
import matplotlib
matplotlib.rcParams['font.family'] = 'Malgun Gothic' #Windows
matplotlib.rcParams['font.family'] = 'AppleGothic' #mac
matplotlib.rcParams['font.size'] = 15 #폰트 크기
matplotlib.rcParams['axes.unicode_minus'] = False #한글 폰트 사용시 마이너스 글자 깨지는거 해결
```

--- 
# 2. 축
```python
plt.plot(x,y)
plt.xlabel('X축') #x축 쪽에 글자 출력
plt.ylabel('Y축') #y축 쪽에 글자 출력

plt.xlabel('X축', loc='right') #글자 위치 (left, right, center)

plt.xticks([1,2,3]) #x축 범위(그래프에 표시되는 숫자)
plt.yticks([3,6,9,12])
```

--- 
# 3. 범례(legend)
```python
plt.plot(x,y, label='무슨 데이터') #데이터가 무엇을 의미하는지 그래프에 그려줌
plt.legend(loc='upper right')
plt.legend(loc=(0.5, 0.5)) # 튜플로 위치 좌표를 줄 수 있음
```

--- 
# 4. 스타일

## 마커(marker)
```python
plt.plot(x,y, linewidth=5) #선 두계
plt.plot(x,y, marker='o') #데이터가 있는 곳에 표시
plt.plot(x,y, marker='o', linestyle='None') #라인 생략
plt.plot(x,y, marker='o', markersize=10) #마커 크기
plt.plot(x,y, marker='o', markeredgecolor='red')#마커 외각선 색
plt.plot(x,y, marker='o', markerfacecolor='yellow') #마커 내부 색
```

## 선 스타일
```python
plt.plot(x,y, linestyle=':') # 선 스타일
plt.plot(x,y, color='pick') #선 색깔
```

## 포맷
```python
plt.plot(x,y, 'ro--') ## color, marker, linestyle 정보를 string으로 줄수 있음
```

## 축약어
```python
plt.plot(x,y, marker='o', mfc='red', ms=10, mec='blue', ls=':')
```

## 투명도
```python
plt.plot(x, y, alpha=0.3) #알파값은 투명도, 낮을수록 투명함
```

## 그래프 크기
```python
plt.figure(figsize=(10,5), dpi=200) #가로 세로, dpi=확대 정도(해상도)
plt.plot(x,y)
```

## 배경색
```python
plt.figure=(facecolor='yellow')
```

--- 
# 5. 파일 저장
```python
plt.plot(x,y)
plt.savefig('graph.png', dpi=100)
```

--- 
# 6. 텍스트
```python
plt.plot(x,y)
plt.plot(x,y, marker='o')

x = [1,2,3]
y = [2,4,8]
for idx, txt in enumerate(y):
	plot.text(x[idx], y[idx], txt, ha='center', color='blue') #ha:글자 위치
```

--- 
# 7. 여러 데이터
```python
days = [1,2,3]
az = [2,4,8]
pfizer = [5,1,3]
moderna = [1,2,5]

plt.plot(days, az)
plt.plot(days, pfizer)
plt.plot(days, moderna)
#여러개를 plot하면 하나의 그래프에 여러 선을 그려줌
```

--- 
# 8. 막대 그래프(기본)
```python
labels = ['강백호', '서태웅', '정대만']
values = [190, 187, 184]
colors = ['r','g', 'b']

plt.bar(labels, values, color=colors, alpha=0.5, width=0.5) #막대 그래프, width: 굵기
plt.ylim(175,195) #y축의 크기 제한
plt.xticks(rotation=45) #x축의 이름 데이터 각도를 45도로 설정
plt.yticks(rotation=45)

ticks = ['1', '2', '3']
plt.xticks(labels, ticks) # x축 데이터를 ticks로 바꿈
```

--- 
# 9. 막대 그래프(심화)
```python
plt.barh(labels, values) # 옆으로 누운 그래프
plt.xlim(175, 195)
bar = plt.bar(labels, values)
bar[0].set_hatch('/') # 강백호 선수 바 모양

for idx, rect in enumerate(bar):
	plt.text(idx, rect.get_height(), values[idx])
```

--- 
# 10. DataFrame 활용
```python
df = pd.read_excel('score.xlsx')
plt.plot(df['지원번호'], df['키'])

plt.plot(df['지원번호'], df['영어'])
plt.plot(df['지원번호'], df['수학'])
# 두 성적을 한 그래프에

plt.grid() #그래프에 격자그림 표시해줌
```

--- 
# 11. 누적 막대 그래프
```python
plt.bar(df['이름'], df['국어'])
plt.bar(df['이름'], df['영어'])
#하나의 이름에 국어와 영어 성적을 합해서 보여줌

plt.bar(df['이름'], df['영어'], bottom=df['국어'])
#영어 성적을 국어성적 위에 그려줌(단순히 국어성적을 받아서 국어성적~ 시작하는 그래프를 그려주기 때문에 국어 성적을 안넣어주면 영어 성적이 위로 뜸
plt.bar(df['이름'], df['수학'], bottom=df['국어']+df['영어'])

plt.xticks(rotation=45)
```

--- 
# 12. 다중 막대 그래프
```python
N = df.shape[0]
index = np.arrange(N)

w = 0.25
plt.bar(index - w, df['국어'], width=0.25, label='국어')
plt.bar(index, df['영어'], width=w, label='영어')
plt.bar(index + w, df['수학'], width=w, label='수학')
plt.xticks(index, df['이름']) #index(0,1,...,7을 이름값으로 바꿔줌)
```

--- 
# 13. 원 그래프(기본)
```python
values = [30, 25, 20, 13, 10, 2]
labels = ['python', 'java', 'javascript', 'c#', 'c', 'ETC']
explode = [0.2, 0.1, 0,0,0,0]

plt.pie(values, labels=labels, autopct="%.1f%%", explode=explode) #autopct: 자동으로 퍼센트를 그려줌, explode: 해당 위치의 영역을 주어진 비율만큼 떨어뜨려줌
plt.legend(loc=(1.2, 0.3), title='언어별 선호도') #범례위에 타이틀을 보여줌
```

--- 
# 14. 원 그래프(심화)
```python
wedgeprops={'width':0.2, edgecolor:'w', 'linewidth':5}
#width: 원 그래프 중앙의 빈 원의 크기(클수록 원이 작아짐), edgecolor: 데이터 가장자리 색, linewidth: 떨어진 정도
plt.pie(values, labels=labels, autopct="%.1f%%", explode=explode, wedgeprops=wedgeprops)
```

```python
def custom_autopct(pct):
	return ('%.1f%%' % pct) if pct >= 10 else ''

plt.pie(values, labels=labels, autopct=cutom_autopct, explode=explode, wedgeprops=wedgeprops, pctdistance=0.7) #pctdistance: 퍼센트 값들의 위치 지정
```

## DataFrame 활용
```python
grp = df.groupby('학교')

values = [grp.size()['북산고'], grp.size()['능담고']]
lables = ['북산고', '능담고']

plt.pie(values, labels=labels)

```

--- 
# 15. 산점도 그래프
```python
df.scatter(df['영어'], df['수학'])
plt.xlabel('영어 점수')
plt.ylabel('수학 점수')

sizes = np.random.rand(8) * 1000
df.scatter(df['영어'], df['수학'], s=sizes, c=df['학년'], cmap='viridis') #s: 점들의 크기를 설정, c: 점들의 색을 설정(지금은 학년에 따라)
plt.colorbar() # 색을 설정한 기준을 바 형태로 보여줌
plt.colorbar(ticks=[1,2,3], label='학년', shrink=0.3, orientation='horizontal')# shrink: 바 축소, orientation: 바 위치(가로, 세로)
```

--- 
# 16. 여러 그래프
```python
fig, axs = plt.subplots(2,2, figsize=(15,10)) #세로로 2개, 가로로 2개
fig.suptitle('여러 그래프 넣기') #가장 상위 제목

#첫번째 그래프
axs[0,0].bar(df['이름'], df['국어'], label='국어') #데이터 설정
axs[0,0].set_title('첫번쨰 그래프') # 데이터 제목
axs[0,0].legend() # 범례
axs[0,0].set(xlabel='이름', ylabel='점수') # x,y축 label
axs[0,0].set_facecolor('lightyellow') #배경 색
axs[0,0].grid()

#두번째 그래프
axs[0,1].plot(df['이름'], df['수학'], label='수학')
axs[0,1].plot(df['이름'], df['영어'], label='영어')
axs[0,1].legend()

#세번째 그래프
axs[1,0].barh(df['이름'], df['키'])

#네번쨰 그래프
axs[1,1].plot(df['이름'], df['사회'])
```