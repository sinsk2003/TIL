# DFS

- 깊이 우선 탐색
- 스택 자료구조 재귀적 이용

```python
def dfs(graph, v, visited):
    visited[v] = True
    print(v, end=' ')
    for i in graph[v]:
        if not visited[i]:
            dfs(graph, i, visited)
            
graph = [ [], [2,3,8], [1,7], [1,4,5], [3,5], [3,4], [7], [2,6,8], [1,7] ]
visited = [False] * 9
dfs(graph, 1, visited)
```

# BFS

- 너비 우선 탐색
- 큐 자료구조 재귀적 이용

```python
from collections import deque

def bfs(graph, start, visited):
    queue = deque([start])
    visited[start] = True
    while queue:
        v= queue.popleft()
        print(v, end=' ')
        for i in graph[v]:
            queue.append(i)
            visited[i] = True

graph = [ [], [2,3,8], [1,7], [1,4,5], [3,5], [3,4], [7], [2,6,8], [1,7] ]
visited = [False] * 9
bfs(graph, 1, visited)
            
```
