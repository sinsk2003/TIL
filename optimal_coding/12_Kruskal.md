# 크루스칼 알고리즘

- 신장 트리: 그래프에서 모든 노드를 포함하면서 사이클이 존재하지 않는 부분 그래프

- 대표적인 최소 신장 트리 알고리즘
- 그리디 알고리즘
- 동작 과정
  - 간선 데이터를 비용에 따라 오름차순으로 정렬
  - 간선을 하나씩 확인하며 현재의 간선이 사이클을 발생시키는지 확인
    - 사이클 발생하지 않는 경우 최소 신장 트리에 포함시킴
    - 사이클이 발생하는 경우 최소 신장 트리에 포함시키지 않음

```python
def find_parent(parent, x):
    if parent[x] != x:
        return find_parent(parent, parent[x])
    return x

def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b
        
v, e = map(int, input().split())
parent = [0] * (v+1)
edges = []
result = 0

for i in range(1, v+1):
    parent[i] = i

for _ in range(e):
    a, b, cost = map(int, input().split())
    edges.append((cost, a, b))
    
edges.sort()

for edge in edges:
    cost, a, b = edge
    if find_parent(parent, a) != find_parent(parent, b):
        union_parent(parent, a, b)
        result += cost
        
print(result)
```
