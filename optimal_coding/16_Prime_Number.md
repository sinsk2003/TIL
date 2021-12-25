# 소수 판별 알고리즘

- 기본: X가 2 ~ X-1 로 나눠떨어지는지 확인
  - 시간 복잡도: O(X)

```python
def is_prime_number(x):
  for i in range(2, x):
    if x % i == 0:
      return False
  return True
```

- 개선: X가 2 ~ |X^1/2| 로 나눠떨어지는지 확인
  - 시간 복잡도: O(X^1/2)

```python
import math

def is_prime_number(x):
  for i in range(2, int(math.sqrt(x)) + 1):
    if x % i == 0:
      return False
  return True
```

# 에라토스테네스의 체 알고리즘

- 다수의 소수 판별 알고리즘
- N보다 작거나 같은 모든 소수를 찾을 수 있음
- 동작 과정
  1. 2부터 N까지의 모든 자연수 나열
  2. 남은 수 중에서 아직 처리하지 않은 가장 작은 수 i를 찾는다.
  3. 남은 수 중에서 i를 제외한 i의 배수를 모두 제거(i <= N^1/2)
- 시간 복잡도: O(NloglogN)
- 메모리가 많이 필요

```python
import math

n = 1000
array = [True for i in range(n + 1)]

for i in range(2, int(math.sqrt(n)) + 1):
  if array[i] == True:
    j = 2
    while i * j <= n:
      array[i * j] = False
      j += 1
      
for i in range(2, n + 1):
  if array[i]:
    print(i, end=' ')
```

