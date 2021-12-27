# 다이나믹 프로그래밍

- 동적 계획법: 메모리를 적절히 사용하여 수행 시간 효율성을 비약적으로 향상시키는 방법
  - 동적 할당: 프로그램이 실행되는 도중에 실행에 필요한 메모리를 할당하는 기법
- 이미 계산된 결과는 별도의 메모리 영역에 저장하여 다시 계산하지 않도록 한다.
- 조건
  - 최적 부분 구조: 큰 문제를 작은 문제로 나눌 수 있으며 작은 문제의 답을 모아서 큰 문제를 해결 가능
  - 중복되는 부분 문제: 동일한 작은 문제를 반복적으로 해결해야 함
- 피보나치 수열: 단순 재귀 소스 코드

```python
def fibo(x):
  if x == 1 or x == 2:
    return 1
  return fibo(x - 1) + fibo(x - 2)

print(fibo(4)) # 3
```

- 단순 재귀 함수로 피보나치 수열을 해결하면 지수 시간 복잡도를 가짐(중복되는 부분 문제)
  - 시간 복잡도: O(2^N)
- 메모이제이션: 한 번 계산한 결과를 메모리 공간에 메모하는 기법(=캐싱)
- 탑다운(메모이제이션) 방식은 하향식이라고도 하며 보텀업 방식은 상향식이라고도 함
- 다이나믹 프로그래밍의 전형적인 형태는 보텀업 방식
  - 결과 저장용 리스트는 DP테이블이라고 부름
- 엄밀히 말하면 메모이제이션은 이전에 계산된 결과를 일시적으로 기록해 놓는 넓은 개념을 의미
  - 따라서 메모이제이션은 다이나믹 프로그래밍에 국한된 개념이 아님
  - 한 번 계산된 결과를 담아 놓기만 하고 다이나믹 프로그래밍을 위해 활용되지 않을 수도 있음
- 피보나치 수열: 탑다운 다이나믹 프로그래밍 소스 코드
  - 시간 복잡도: O(N)

```python
d = [0] * 100

def fibo(x):
  if x == 1 or x == 2:
    return 1
  if d[x] != 0:
    return d[x]
  d[x] = fibo(x - 1) + fibo(x - 2)
  return d[x]

print(fibo(99))
```

- 피보나치 수열: 보텀업 다이나믹 프로그래밍 소스 코드

```python
d = [0] * 100

d[1] = 1
d[2] = 1
n = 99

for i in range(3, n + 1):
  d[i] = d[i - 1] + d[i - 2]
  
print(d[n])
```

- 다이나믹 프로그래밍과 분할 정복은 모두 최적 부분 구조를 가질 때 사용 가능
- 다이나믹 프로그래밍과 분할 정복의 차이점은 부분 문제의 중복
  - 다이나믹 프로그래밍 문제에서는 각 부분 문제들이 서로 영향을 미치며 부분 문제가 중복됨
  - 분할 정복 문제에서는 동일한 부분 문제가 반복적으로 계산되지 않음
    - 피봇이 자리를 변경해서 자리를 잡으면 그 기준 원소의 위치는 바뀌지 않음
    - 분할 이후에 해당 피벗을 다시 처리하는 부분 문제는 호출되지 않음
- 다이나믹 프로그래밍 문제에 접근하는 방법
  - 주어진 문제가 다이나믹 프로그래밍 유형임을 파악
  - 가장 먼저 그리디, 구현, 완전 탐색 등의 아이디어로 문제를 해결할 수 있는지 검토 가능
    - 다른 알고리즘으로 풀이 방법이 떠오르지 않으면 다이나믹 프로그래밍 고려
  - 일단 재귀 함수로 비효율적인 완전 탐색 프로그램을 작성한 뒤에 (탑다운) 작은 문제에서 구한 답이 큰 문제에서 그대로 사용될 수 있으면, 코드를 개션하는 방법을 사용할 수 있음

# 문제 풀이

## 개미 전사

- 인접한 식량창고를 못 턴다고 할 때, 털 수 있는 식량의 최댓값 구하기
- a(i) = i번째 식량창고까지의 최적의 해, k(i) = i번째 식량창고에 있는 식량의 양
- a(i) = max(a(i-1), a(i-2) + k(i))

```python
n = int(input())
array = list(map(int, input().split()))

d = [0] * 100
d[0] = array[0]
d[1] = max(array[0], array[1])
for i in range(2, n):
  d[i] = max(d[i - 1], d[i - 2] + array[i])
  
print(d[n - 1])
```

## 1로 만들기

- 2, 3, 5로 나누어 떨어지면 나누고 나누어 떨어지지 않으면 1 빼기
- a(i) = i를 1로 만들기 위한 최소 연산 횟수
- a(i) = min(a(i-1), a(i/2), a(i/3), a(i/5)) + 1
- 단, 1을 빼는 연산을 제외하고는 해당 수로 나누어떨어질 때에 한해 점화식 적용 가능

```python
x = int(input())
d = [0] * 30001

for i in range(2, x + 1):
  d[] = d[i - 1] + 1
  if i % 2 == 0:
    d[i] = min(d[i], d[i // 2] + 1)
  if i % 3 == 0:
    d[i] = min(d[i], d[i // 3] + 1)
  if i % 5 == 0:
    d[i] = min(d[i], d[i // 5] + 1)
 
print(d[x])
```

## 효율적인 화폐 구성

- a(i) = 금액 i를 만들 수 있는 최소한의 화폐 개수
- k = 각 화폐의 단위
- 점화식: 각 화폐 단위인 k를 하나씩 확인하며
  - a(i-k)를 만드는 방법이 존재하는 경우, a(i) = min(a(i), a(i-k) + 1)
  - a(i-k)를 만드는 방법이 존재하지 않는 경우, a(i) = INF

```python
n, m = map(int, input().split())
array = []
for i in range(n):
  array.append(int(input()))
  
d = [10001] * (m + 1)

d[0] = 0 
for i in range(n):
  for j in range(aray[i], m + 1):
    if d[j - array[i]] != 10001:
      d[j] = min(d[j], d[j - array[i]] + 1)
    
if d[m] == 10001:
  print(-1)
else:
  print(d[m])
```

# 금광

- 왼쪽 아무 행이나 시작해서 오른쪽으로 가면서 얻을 수 있는 금의 최대 크기
- 왼쪽 위, 왼쪽, 왼쪽 아래에서 오는 경우
- `array[i][j] `= i행 j열에 존재하는 금의 양
- `dp[i][j]`= i행 j열까지의 최적의 해 (얻을 수 있는 금의 최댓값)
- `dp[i][j] = array[i][j] + max(dp[i-1][j-1], dp[i][j-1], dp[i+1][j-1])`
- 이 때 테이블에 접근할 때마다 리스트의 범위를 벗어나지 않는지 체크해야 함
- 편의상 초기 데이터를 담는 변수 array를 사용하지 않아도 됨
  - 바로dp테이블에 초기 데이터를 담아서 적용

```python
for tc in range(int(input())):
  n, m =map(int, input().split())
  array = list(map(int, input().split()))
  dp = []
  index = 0
  for i in range(n):
    dp.append(array[index:index + m])
    index += m
  for j in range(1, m):
    for i in range(n):
      if i == 0: left_up = 0
      else: left_up = dp[i-1][j-1]
      if i == n - 1: left_down = 0
      else: left_down = dp[i+1][j-1]
      left = dp[i][j-1]
      dp[i][j] = dp[i][j] + max(left_up, left_down, left)
  result = 0
  for i in range(n):
    result = max(result, dp[i][m-1])
  print(result)
```

# 병사 배치하기

- 전투력이 높은 병사가 앞쪽에 오도록 내림차순으로 배치
- 배치 과정에서는 특정한 위치에 있는 병사를 열외하면서도 남아 있는 병사의 수 최대
- 가장 긴 증가하는 부분 수열(Longest Increasing Subsequence, LIS)와 같은 아이디어
  - D[i] = array[i] 를 마지막 원소로 가지는 부분 수열의 최대 길이
  - 모든 0 <= j < i 에 대하여, D[i] = max(D[i], D[j] + 1) if array[j] < array[i]

```python
n = int(input())
array = list(map(int, input().split()))
array.reverse()

dp = [1] * n

for i in range(1, n):
  for j in range(0, i):
    if array[j] < array[i]:
      dp[i] = max(dp[i], dp[j] + 1)
      
print(n - max(dp))
```

