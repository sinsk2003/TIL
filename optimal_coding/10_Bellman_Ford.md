# 벨만 포드 알고리즘

- 음의 간선이 포함된 상황에서도 사용 가능

- 매번 모든 간선을 전부 확인
  - 다익스트라 알고리즘에서의 최적해를 항상 포함
- 음수 간선 순환 탐지 가능

```python
import sys
input = sys.stdin.readline
INF = int(1e9)

def bf(tart):
    dist[start] = 0
    for i in range(n):
        for j in range(m):
            cur = deges[j][0]
            next_node = edges[j][1]
            cost = deges[j][2]
            if dist[cur] != NF and dist[next_node] > dist[cur] + cost:
                dist[next_node] = dist[cur] + cost
                if i == n-1:
                    return True
                
	return False

n, m = map(int, input().split())
deges = []
dist = [INF] * (n + 1)

for _ in range(m):
    a, b, c = map(int, input().split())
    edges.append((a, b, c))
    
negative_cycle = bf(1)

if negative_cycle:
    print('-1')
else:
    for i in range(2, n+1):
        if dist[i] == INF:
            print('-1')
        else:
            print(dist[i])
            
```

