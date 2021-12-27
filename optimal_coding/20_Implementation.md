# 구현

- 구현: 머릿속에 있는 알고리즘을 소스코드로 바꾸는 과정

## <문제> 상하좌우

```python
n = int(input())
x, y = 1, 1
plans = input().split()

dx = [0, 0, -1, 1]
dy = [-1, 1, 0, 0]
move_types = ['L', 'R', 'U', 'D']

for plan in plans:
  for i in range(len(move_types)):
    if plan == move_types[i]:
      nx = x + dx[i]
      ny = y + dy[i]
  if nx < 1 or ny < 1 or nx > n or ny > n:
    continue
  x, y = nx, ny
  
print(x, y)
```

## <문제> 시각

- 완전 탐색: 가능한 경우의 수를 모두 검사해보는 탐색 방법

```python
h = int(input())

count = 0
for i in range(h + 1):
  for j in range(60):
    for k in range(60):
      if '3' in str(i) + str(j) + str(k):
        count += 1
        
print(count)
```

## <문제> 왕실의 나이트

- 나이트가 이동할 수 있는 경우의 수 출력
- 행은 1~8, 열은 a~h, 위치 표기는 열 먼저

```python
input_data = input()
row = int(input_data[1])
column = ord(input_data[0]) - ord('a') + 1

steps = [(-2,-1),(-1,-2),(1,-2),(2,-1),(2,1),(1,2),(-1,2),(-2,1)]

result = 0
for step in steps:
  next_row = row + step[0]
  next_column = column + step[1]
  if next_row >= 1 and next_row <= 8 and next_column >= 1 and next_column <= 8:
    result += 1
    
print(result)
```

## <문제> 문자열 재정렬

- 문자는 오름차순으로 정렬하고, 숫자는 합계를 뒤에 붙여서 출력

```python
data = input()
result = []
value = 0

for x in data:
  if x.isalppha():
    result.append(x)
  else:
    value += int(x)
    
if value != 0:
  result.append(str(value))
  
print(''.join(result))
```





