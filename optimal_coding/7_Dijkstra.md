# 다익스트라 최단 경로 알고리즘

- 특정 노드에서 다른 모든 노드로 가는 최단 경로 계산

- 그리디 알고리즘: 매 상황에서 가장 비용이 적은 노드 선택
- 기본 방법

 ```python
 import sys
 input= sys.stdin.readline
 INF = int(1e9)
 
 n, m = map(int, input().split())
 start = int(input())
 graph = [[] for i in range(n+1)]
 visited = [False] * (n+1)
 distance = [INF] * (n+1)
 
 for _ in range(m):
     a, b, c = map(int, input().split())
     graph[a].append((b, c))
     
 def get_smallest_node():
     min_value = INF
     index = 0
     for i in range(1, n+1):
         if distance[i] < min_value and not visited[i]:
             min_value = distance[i]
             index = i
         return index
 
 def dijkstra(start):
     distance[start] = 0
     visited[start] = True
     for j in graph[start]:
         distance[j[0]] = j[1]
     
     for i in range(n-1):
         now = get_smallest_node()
         visited[now] = True
         for j in graph[now]:
             cost = distance[now] + j[1]
             if cost < distance[j[0]] = cost
             
 dijkstra(start)
 
 for i in range(1, n+1):
     if distance[i] == INF:
         print("INFINITY")
     else:
         print(distance[i])
 ```

- 최소 힙

```python
import heapq

def heaqsort(iterable):
    h = []
    result= []
    for value in iterable:
        heapq.heaqqush(h, value)
    for i in range(len(h)):
        result.append(heapq.heappop(h))
    return result

result = heapsort([1, 3, 5, 7, 9, 2, 4, 6, 8, 0])
print(result)
```

- 개선된 다익스트라

```python
import heapq
import sys
input= sys.stdin.readline
INF = int(1e9)

n, m = map(int, input().split())
graph = [[] for i in range(n+1)]
distance = [INF] * (n+1)

for _ in range(m):
    a, b, c = map(int, input().split())
    graph[a].append((b, c))
    
def dijkstra(start):
    q=[]
    heapq.heaqqush(q, start)
    distance[start] = 0
    while q:
        dist, now = heapq.heappop(q)
        if distance[now] < dist:
            continue
        for i in graph[now]:
            cost = dist + i[1]
            if cost < distance[i[0]]:
                distance[i[0]] = cost
                heapq.heappush(q, (cost, i[0]))
                
dijkstra(start)

for i in range(1, n+1):
    if distance[i] == INF:
        print("INFINITY")
    else:
        print(distance[i])
    
```

