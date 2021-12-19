# 최소 공통 조상

1. 모든 노드에 대한 깊이 계산
2. 두 노드의 깊이가 동일하도록 거슬러 올라간 후, 부모가 같아질 때까지 반복적으로 두 노드의 부모 방향으로 거슬러 올라감

```python
import sys
sys.setrecursionlimit(int(1e5))
n = int(input())

parent = [0] * (n+1)
d = [0] * (n+1) # 깊이
c = [0] * (n+1) # 깊이 계산 여부
graph = [[] for _ in range(n+1)]

for _ in range(n-1):
    a, b = map(int, input().split())
    graph[a].append(b)
    graph[b].append(a)
    
def dfs(x, depth):
    c[x] = True
    d[x] = depth
    for y in graph[x]:
        if c[y]:
            continue
        parent[y] = x
        dfs(y, depth + 1)
        
def lca(a, b):
    while d[a] != d[b]:
        if d[a] > d[b]:
            a = parent[a]
        else:
            b = parent[b]
    while a != b:
        a = parent[a]
        b = parent[b]
    return a

dfs(1, 0)

m = int(input())

for i in range(m):
    a, b = map(int, input().split())
    print(lca(a, b))
```

- 개선: 모든 노드에 대하여 깊이와 2^i 번째 부모에 대한 정보를 계산

```python
import sys

input = sys.stdin.readline

sys.setrecursionlimit(int(1e5))
LOG = 21 # 2^20 = 1,000,000

n = int(nput())
parent = [[0] * LOG for _ in range(n+1)]
d = [0] * (n+1) # 깊이
c = [0] * (n+1) # 깊이 계산 여부
graph = [[] for _ in range(n+1)]

for _ in range(n-1):
    a, b = map(int, input().split())
    graph[a].append(b)
    graph[b].append(a)
    
def dfs(x, depth):
    c[x] = True
    d[x] = depth
    for y in graph[x]:
        if c[y]:
            continue
        parent[y][0] = x
        dfs(y, depth + 1)

def set_parent():
    dfs(1, 0)
    for i in range(1, LOG):
        for j in range(1, n+1):
            parent[j][i] = parent[parent[j][i-1]][i-1]
            
def lca(a, b):
    if d[a] > d[b]:
        a, b = b, a
    for i in range(LOG -1, -1, -1):
        if d[b] - d[a] >= (1 << i):
            b = parent[b][i]
    if a == b:
        return a:
    for i in range(LOG - 1, -1, -1):
        if parent[a][i] != parent[b][i]:
            a = parent[a][i]
            b = parent[b][i]
    return parent[a][0]

set_parent()

m = int(input())

for i in range(m):
    a, b = map(int, nput().split())
    print(lca(a, b))
        
        
```



import sys

input = sys.stdin.readline

sys
