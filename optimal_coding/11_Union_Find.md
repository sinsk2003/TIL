# 서로소 집합 자료구조

- 서로소 집합: 공통 원소가 없는 두 집합
- 서로소 부분 집합들로 나누어진 원소들의 데이터를 처리하기 위한 자료구조
  - 합집합
  - 찾기
- 합치기 찾기(Union Find) 자료구조

- 동작 과정: A, B의 루트 노드 A', B' 를 찾고 A' < B'이면 A'를 B'의 부모 노드로 설정

- 연결성: 루트 노드를 찾기 위해 부모 테이블을 계속해서 확인

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
parent = [0] * (v +1)

for i in range(1, v+1):
    parent[i] = i
    
for i in range(e):
    a, b = map(int, input().split())
    union_parent(parent, a, b)
    
print('각 원소가 속한 집합: ', end='')
for i in range(1, v+1):
    print(find_parent(parent, i), end=' ')
    
print()

print('부모 테이블: ', end='')
for i in range(1, v+1):
    print(parent[i], end=' ')
```

- 경로 압축
  - 찾기 함수를 최적화하기 위한 방법
  - 찾기 함수를 재귀적으로 호출한 뒤에 부모 테이블 값을 바로 갱신

```python
def find_parent(parent, x):
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]
```

- 서로소 집합은 무방향 그래프 내 사이클 판별 시 사용 가능
  - 각 간선을 하나씩 확인하며 두 노드의 루트노드를 확인
    - 루트 노드가 서로 다르다면 합집합 연산 수행
    - 루트 노드가 서로 같다면 사이클이 발생한 것

```python
cycle = False

for _ in range(e):
    a, b = map(int, input().split())
    if find_parent(parent, a) == find_parent(parent, b):
        cycle = True
        break
    else:
        union_parent(parent, a, b)

if cycle:
    print('사이클이 발생했습니다.')
else:
    print('사이클이 발생하지 않았습니다.')
```

