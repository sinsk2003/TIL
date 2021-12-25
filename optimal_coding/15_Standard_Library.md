# 실전에서 유용한 표준 라이브러리

- 내장 함수: sum, min, max, eval, sorted

  ```python
  print( sum([1,2,3,4,5],6) ) # 21
  print( eval("(3+5)*7") )

  array = [('홍길동', 35), ('이순신', 75), ('아무개', 50)]
  print( sorted(array, key=lambda x: x[1], reverse=True) ) 
  # [('이순신', 75), ('아무개', 50), ('홍길동', 35)]
  ```

- itertools: 반복되는 형태의 데이터를 처리하기 위한 유용한 기능들 제공

  ```python
  from itertools import permutations # 순열
  data = ['A', 'B', 'C']
  print( list(permutations(data, 3)) )
  # [('A','B','C'),('A','C','B'),('B','A','C')('B','C','A'),('C','A','B'),('C','B','A')]

  from itertools import combinations # 조합
  print( list(combinations(data, 2)) ) # [('A','B'),('A','C'),('B','C')]

  from itertools import product # 중복 순열
  print( list(product(data, repeat=2)) )

  from itertools import combinations_with_replacement # 중복 조합
  print( list(combinations_with_replacement(data, 2)) )
  ```

- heapq

- bisect: 이진 탐색 기능 제공

- collections: deque, Counter 등

  ```python
  from collections import Counter
  counter = Counter(['red', 'blue', 'red', 'gree', 'blue', 'blue'])
  print( counter['blue'] ) # 3
  print( dict(counter) ) # {'red': 2, 'blue': 3, 'green': 1}
  ```

- math

  ```python
  import math

  def lcm(a, b): # 최소 공배수(LCM) 구하는 함수
    return a * b // math.gcd(a, b)

  a, b = 21, 14

  print( math.gcd(21, 14) ) # 최대 공약수(GCD) 계산
  print( lcm(21, 14) ) # 최소 공배수(LCM) 계산
  ```