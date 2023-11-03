# 신장트리(Spanning Tree)

- 그래프에서 모든 노드를 포함하면서 사이클이 존재하지 않는 부분 그래프
- 정점의 개수가 n개일 때, 간선의 수는 n-1개
- 가중치의 합이 최소가 되는 신장 트리 => 최소 신장 트리(Minimum Spanning Tree, MST)

# 크루스칼(Kruskal)

- 최소 신장 트리를 구하기 위한 알고리즘
- 그리디 알고리즘의 일종
- 그래프 간선들을 가중치의 오름차순으로 정렬 => 사이클을 형성하지 않는 선에서 정렬된 순서대로 간선 선택
- 간선의 개수가 E개일 때, O(E logE)의 시간복잡도를 가짐

## 사이클 판단

- Union & Find 자료구조 사용
    - 서로소 집합을 표현하는 자료구조
    - Union : 서로 다른 두 집합을 병합하는 연산
    - Find : 집합 원소가 어떤 집합에 속해있는지 찾는 연산

- 각 정점의 루트 노드를 표현한 배열을 만들어 초기값으로 자기 자신이 루트 노드가 되게 초기화
- 가중치의 오름차순 정렬한 순서대로 간선 선택
- 간선을 연결하면서 Union 연산에 의해 집합을 합침 (각 집합의 루트 노드가 다른 값이었으므로) => 집합 내 가장 작은 숫자가 그 집합에서의 루트 노드가 되게끔 설정

=> 루트 노드가 다른지 판단 후 다르다면 Union 연산으로 합침

- 루트 노드가 같다면 Union 연산 하지 않음 => 사이클 형성되기 때문

```python
# 특정 원소가 속한 집합을 찾기
def find_parent(parent, x):
    # 루트 노드를 찾을 때까지 재귀 호출
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]

# 두 원소가 속한 집합을 합치기
def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b

# 노드의 개수와 간선(Union 연산)의 개수 입력 받기
v, e = map(int, input().split())
# 부모 테이블 초기화
parent = [0] * (v + 1)

# 모든 간선을 담을 리스트와 최종 비용을 담을 변수
edges = []
result = 0

# 부모 테이블상에서, 부모를 자기 자신으로 초기화
for i in range(1, v + 1):
    parent[i] = i

# 모든 간선에 대한 정보를 입력 받기
for _ in range(e):
    a, b, cost = map(int, input().split())
    # 비용 순으로 정렬하기 위해서 튜플의 첫 번째 원소를 비용으로 설정
    edges.append((cost, a, b))

# 간선을 비용순으로 정렬
edges.sort()

# 간선을 하나씩 확인하며 사이클이 발생하지 않는 경우에만 집합에 포함
for edge in edges:
    cost, a, b = edge
    if find_parent(parent, a) != find_parent(parent, b):
        union_parent(parent, a, b)
        result += cost

print(result)
```


[참고 사이트](https://chanhuiseok.github.io/posts/algo-33/)