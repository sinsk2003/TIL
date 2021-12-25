# 이진 탐색

- 순차 탐색: 앞에서부터 하나씩 확인
- 이진 탐색: 정렬되어 있는 리스트에서 탐색 범위를 절반씩 좁혀가며 데이터 탐색
  - 시작점, 끝점, 중간점을 이용하여 탐색 범위 설정
- 시간 복잡도: O(logN)
- 재귀함수를 이용한 코드

```python
def binary_search(array, target, start, end):
  if start > end:
    return None
  mid = (start + end) // 2
  if array[mid] > target:
    return mid
  elif arra[mid] > target:
    return binary_search(array, target, start, mid -1)
  else:
    return binary_search(array, target, mid + 1, end)
  
n, target = list(map(int, input().split()))
array = list(map(int, input().split()))

result = binary_search(array, target, 0, n-1)
if result == None:
  print("원소가 존재하지 않습니다.")
else:
  print(result + 1)
```

- 반복문을 이용한 코드

```python
def binary_search(array, target, start, end):
  while
  tart <= end:
    mid = (start + end) // 2
    if array[mid] == target:
      return mid
    elif array[mid] > target:
      end = mid - 1
    else:
      start = mid + 1
  return None
```

- 이진 탐색 라이브러리
  - bisect_left(a, x): 정렬된 순서를 유지하면서 배열 a에 x를 삽입할 가장 왼쪽 인덱스를 반환
  - bisect_right(a, x): 정렬된 순서를 유지하면서 배열 a에 x를 삽입할 가장 오른쪽 인덱스를 반환

```python
from bisect import bisect_left, bisect_right
a = [1, 2, 4, 4, 8]
x = 4

print( bisect_left(a, x) ) # 2
print( bisect_right(a, x) ) # 4
```

- 값이 특정 범위에 속하는 데이터 개수 구하기

```python
from bisect import bisect_left, bisect_right

def count_by_range(a, left_value, right_value):
  right_index = bisect_right(a, right_value)
  left_index = bisect_left(a, left_value)
  return right_index - left_index

a = [1,2,3,3,3,3,4,4,8,9]
print( count_by_range(a,4,4) ) # 2
print( count_by_range(a,-1,3) ) # 6    
```

- 파라메트릭 서치

  - 최적화 문제를 결정 문제로 바꾸어 해결하는 기법
  - 이진 탐색을 이용하여 해결 가능

- 떢볶이 떡 만들기

  - 적어도 M만큼의 떡을 얻기 위해 절단기에 설정할 수 있는 높이의 최댓값을 구하라.
  - '현재 이 높이로 자르면 조건을 만족할 수 있는가?'를 확인한 뒤에 조건의 만족 여부에 따라서 탐색 범위를 좁혀서 해결

  ```python
  n, m = list(map(int, input().split(' ')))
  array = list(map(int, input().split()))

  start = 0
  end = max(array)

  result = 0
  while start <= end:
    total =0
    mid = (start + end) //2
    for x in array:
      if x > mid:
        total += x - mid
    if total < m:
      end = mid - 1
    else:
      result = mid
      start = mid + 1
     
  print(result)
  ```



























