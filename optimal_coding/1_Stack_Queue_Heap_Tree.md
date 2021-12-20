# 스택

- 선입 후출

# 큐

- 선입 선출

```python
from collections import deque
queue = deque()
queue.append(5)
queue.popleft()
```

# 우선순위 큐

- 우선순위가 높은 게 먼저 나간다
- 리스트 또는 힙으로 구현

# 힙

- 완전 이진 트리의 일종
- 우선 순위: 루트 노드부터 제거
- 최소 힙: 루트 노드가 가장 작은 값
- 최대 힙: 루트 노드가 가장 큰 값
- 시간 복잡도: O(NlogN)

# 완전이진트리

- 루트 -> 왼쪽 자식 -> 오른쪽 자식 순으로 데이터가 삽입되는 트리

# 최소 힙 구성함수

- Min-Heapify()

- 삽입: 부모보다 자신의 값이 더 작은 경우에 위치 교체(상향식)

- 제거: 루트 노드 제거 후 마지막 노드가 루트 노드의 위치에 오도록 한다. 이후 heapify 진행(하향식)

- 파이썬은 min-heapify 제공

  ```python
  import heapq
  def heapsort(iterable):
  	h=[]
  	result=[]
  	for value in iterable:
  		heapq.heaqqush(h, value)
  	for i in range(len(h)):
  	return result
  ```

  - 입력과 출력에 - 붙이면 min<->max 가능

# 트리

- 루트 노드: 부모가 없는 최상위 노드
- 단말 노드(leaf node): 자식이 없는 노드
- 크기: 노드 개수
- 깊이: 루트 노드로부터의 거리
- 높이: 깊이 중 최댓값
- 차수: 각 노드의 자식 방향 간선 개수
  - 기본적으로 트리의 크기가 N일 때, 전체 간선의 개수는 N-1

# 이진 탐색 트리

- 왼쪽 자식 노드<부모노드<오른쪽 자식 노드
- 탐색 과정: 부모 노드 방문 -> 찾으려는 값과 비교 -> 자식 노드로 이동
  - 원하는 값을 찾을 때까지 위 과정 반복
