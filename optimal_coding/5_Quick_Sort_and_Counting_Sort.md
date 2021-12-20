# 퀵 정렬

- 기준 데이터(=피벗)(주로 첫 번째 데이터)를 설정하고 그 기준보다 큰 데이터와 작은 데이터의 위치를 바꾸는 방법
  - Step 1:  왼쪽에서부터는 피벗보다 큰 데이터를, 오른쪽에서부터는 피벗보다 작은데이터를 선택하고 서로 위치 변경
  - Step 2: 위치가 엇갈리는 경우 피벗과 작은 데이터의 위치를 서로 변경(왼쪽 데이터<피벗<오른쪽 데이터)
    - 분할: 피벗을 기준으로 데이터 묶음을 나누는 작업

  - 각 데이터 묶음에 대해서 퀵 정렬 재귀적 수행
- 일반적으로 가장 많이 사용되는 정렬 알고리즘
- 시간 복잡도: O(NlogN)
  - 이미 정렬된 경우 O(N^2) 
- 일반 코드

```python
array = [5,7,9,0,3,1,6,2,4,8]

def quick_sort(array, start, end):
    if start >= end:
        return
    pivot = start
    left = start +1
    right = end
    while left <= right:
        while(left <= end) and (array[left] <= array[pivot]):
            left += 1
        while (right > start) and (array[right] >= array[pivot]):
            right -= 1
        if left > right:
            array[right], array[pivot] = array[pivot], array[right]
        else:
            array[left], array[right] = array[right], array[left]
    
    quick_sort(array, start, right-1)
    quick_sort(array, right+1, end)

quick_sort(array, 0, len(array) -1)
print(array)
```

- 더 간단한 코드

```python
array = [5,7,9,0,3,1,6,2,4,8]

def quick_sort(array):
    if len(array) <= 1:
        retrun array
    pivot = array[0]
    tail = array[1:]
    
    left_side = [x for x in tail if x <= pivot]
    right_side - [x for x in tail if x > pivot]
    
    return quick_sort(left_side) + [pivot] + quick_sort(right_side)

print(quick_sort(array))
```

# 계수 정렬

- 특정 조건이 부합할 때만 사용할 수 있지만 매우 빠르게 동작

  - 데이터의 크기 범위가 제한되어 정수 형태로 표현할 수 있을 때 사용 가능

- 시간복잡도: 데이터(양수) 중 최댓값이 K일 때, 최악의 경우에도 O(N+K)

- 정렬 방법

  - Step 0: 가장 작은 데이터부터 가장 큰 데이터까지의 범위가 모두 담길 수 있도록 리스트 생성

  - Step 1: 데이터를 하나씩 확인하며 데이터의 값과 동일한 인덱스의 데이터를 1씩 증가
  - Step 2: 리스트의 첫 번째 데이터부터 하나씩 그 값만큼 반복하여 인덱스 출력

```python
array = [7,5,9,0,3,1,6,2,9,1,4,8,0,5,2]
count = [0] * (max(array) +1)

for i in range(len(array)):
    count[array[i]] += 1
for i in range(len(count)):
    for j in range(count[i]):
        print(i, end=' ')
```

- 동일한 값을 가지는 데이터가 여러 개 등장할 때 효과적으로 사용 가능
