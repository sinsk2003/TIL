# 그리디 알고리즘

- 현재 상황에서 당장 좋은 것만 고르는 방법(탐욕법)
- 일반적으로 문제를 풀기 위한 최소한의 아이디어를 떠올릴 수 있는 능력 요구
- 정당성 분석: 단순히 가장 좋아 보이는 것을 반복적으로 선택해도 최적의 해를 구할 수 있는 지 검토

## 거스름 돈

- 시간 복잡도: O(K)
  - 금액과는 무관하며, 동전의 총 종류에만 영향 받음

```python
n = 1260
count = 0
array = [500, 100, 50, 10]
for coin in array:
  count += n // coin
  n %= coin
print(count)
```

## 1이 될 때까지

- N에서 1을 빼거나 N을 K로 나누기

```python
n, k = map(int, input().split())
result = 0
while True:
  target = (n//k)*k
  result += (n - target)
  n = target
  if n < k:
    break
  result += 1
  n //= k
result += (n - 1)
print(result)
```

## 곱하기 혹은 더하기

- 왼쪽부터 오른쪽으로 하나씩 모든 숫자를 확인하며 * 혹은 + 연산자를 넣어 결과적으로 만들어질 수 있는 가장 큰 수를 구하기
- 모든 연산은 왼쪽에서부터 순서대로

```python
data = input()
result = int(data[0])
for i in range(1, len(data)):
  sum = int(data[i])
  if num <= 1 or result <= 1:
    result += num
  else:
    result *= num
      
print(result)
```

## 모험가 길드

- 공포도가 X인 모험가는 반드시 X명 이상으로 구성한 모험가 그룹에 참여
- 여행을 떠날 수 있는 그룹 수의 최댓값 구하기

```python
n = int(input())
data = list(map(int, input().split()))
data.sort()

result = 0
count = 0

for i in data:
  count += 1
  if count >= i:
    result += 1
    count+0
    
print(result)
```



