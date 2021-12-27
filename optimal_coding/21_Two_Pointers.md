# 투 포인터

- 리스트에 순차적으로 접근해야 할 때 두 개의 점의 위치를 기록하면서 처리
- 시작점과 끝점으로 범위 표현 가능

## <문제> 특정한 합을 가지는 부분 연속 수열 찾기

1. start와 end이 첫 번째 원소의 인덱스(0)을 가리키도록 한다.
2. 현재 부분 합이 M과 같다면, 카운트한다.
3. 현재 부분 합이 M보다 작다면, end를 1 증가시킨다.
4. 현재 부분 합이 M보다 크거나 같다면, start를 1 증가시킨다.
5. 모든 경우를 확인할 때까지 2~4 반복

```python
n = 5 # 데이터 개수
m = 5 # 찾고자 하는 부분합
data = [1, 2, 3, 2, 5]

count = 0
interval_sum = 0
end = 0

for start in range(n):
  while interval_sum < m and end < n: 
    interval_sum += data[end]
    end += 1
  if interval_sum == m:
  	count += 1
  interval_sum -= data[start]

print(count)
```

# 구간 합

- 접두사 합: 배열의 맨 앞부터 특정 위치까지의 합을 미리 구해 놓은 것
- 구간 합 = P[Right] - P[Left - 1]

```python
n = 5
data = [10, 20, 30, 40, 50]

sum_value = 0
prefix_sum = [0]
for i in data:
  sum_value += i
  prefix_sum.append(sum_value)
  
left = 3
right = 4
print(prefix_sum[right] - prefix_sum[left - 1])
```

