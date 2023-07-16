# 그래프 탐색 알고리즘 (DFS & BFS)

- 경로탐색 유형 (최단거리, 시간)
- 네트워크 유형 (연결)
- 조합 유형 (모든 조합 만들기)
- DFS : 하나만 끝까지 => 재귀함수, 탈출조건 도달
- BFS : 여러 개 한번씩 => Queue, Linked List, 가장 먼저 넣었던 것을 꺼내서 연결된 점을 Queue에 넣고, Queue가 빌 때까지 반복
- DFS가 BFS보다 시간복잡도가 낮다.

## 스택
- 선입후출 (입구 = 출구)

## 큐
- 선입선출

## 재귀함수 (Recursive Function)
- 자기 자신을 다시 호출하는 함수
- 종료 조건을 반드시 명시해야 함
### 재귀함수 예시
```
n! = 1 * 2 * 3 * ... * (n-1) * n
수학적으로 0!과 1!의 값은 1
```
```python
# 반복적으로 구현한 n!
def factorial_iterative(n):
    result = 1
    # 1부터 n까지의 수를 차례대로 곱하기
    for i in range(1, n+1):
        result *= i
        return result

# 재귀적으로 구현한 n!
def factorial_recursive(n):
    # n이 1 이하인 경우 1을 반환
    if n <= 1:
        return 1
    # n! = n * (n-1)!를 그대로 코드로 작성하기
    return n * factorial_recursive(n-1)
```

### 재귀함수 유의 사항
- 모든 재귀 함수는 반복문을 이용하여 동일한 기능을 구현 가능
- 컴퓨터가 함수를 연속적으로 호출하면 컴퓨터 메모리 내부의 스택 프레임에 쌓임
    - 스택 사용 시 구현상 스택 라이브러리 대신 재귀 함수 이용하는 경우 多

## 유클리드 호제법
- 최대공약수 (GCD) 계산
- 두 개의 자연수에 대한 최대공약수를 구하는 대표적인 알고리즘
```
두 자연수 A, B에 대하여 (A > B) A를 B로 나눈 나머지를 R
이때 A와 B의 최대공약수는 B와 R의 최대공약수와 같다.
```
- 예시

    단계|A|B
    :--:|:--:|:--:
    1|192|162
    2|162|30
    3|30|12
    4|12|6

### 유클리드 호제법 예시
```python
def gcd(a, b):
    if a % b == 0:
        return b
    else:
        return gcd(b, a % b)
```

---

# DFS (Depth-First Search)
- 깊이 우선 탐색
- 스택 자료구조(or 재귀 함수) 이용
    1. 탐색 시작 노드를 스택에 삽입하고 방문 처리
    2. 스택의 최상단 노드에 방문하지 않은 인접한 노드가 하나라도 있으면 그 노드를 스택에 넣고 방문 처리, 방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼냄
    3. 더 이상 2번의 과정을 수행할 수 없을 때까지 반복.
- 방문 기준 : 번호가 낮은 인접 노드

## DFS 예시
```python
# DFS 메서드 정의
def dfs(graph, v, visited):
    # 현재 노드를 방문 처리
    visited[v] = True
    print(v, end=' ')
    # 현재 노드와 연결된 다른 노드를 재귀적으로 방문
    for i in graph[v]:
        if not visited[i]:
            dfs(graph, i, visited)

# 각 노드가 연결된 정보를 표현 (2차원 리스트)
# 그래프 문제 출제 시 1번부터 시작되는 경우 多 => 인덱스 0은 비워둠
graph = [
    [],
    [2, 3, 8],
    [1, 7],
    [1, 4, 5],
    [3, 5],
    [3, 4],
    [7],
    [2, 6, 8],
    [1, 7]
]

# 각 노드가 방문된 정보를 표현 (1차원 리스트)
# 인덱스 0은 사용하지 않기 때문에 하나 더 큰 크기로 리스트 초기화
visited = [False] * 9
dfs(graph, 1, visited)

# 결과 : 1 2 7 6 8 3 4 5
```

---

# BFS (Breadth-First Search)
- 너비 우선 탐색
- 그래프에서 가까운 노드부터 우선적으로 탐색
- 큐 자료구조 이용
    1. 탐색 시작 노드를 큐에 삽입하고 방문 처리
    2. 큐에서 노드를 꺼낸 뒤에 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고 방문 처리
    3. 더 이상 2번의 과정을 수행할 수 없을 때까지 반복
- 방문 기준 : 번호가 낮은 인접 노드

## BFS 예시
```python
from collections import deque

# BFS 메서드 정의
def bfs(graph, start, visited):
    # 큐(Queue) 구현을 위해 deque 라이브러리 사용
    queue = deque([start])
    visited[start] = True
    # 큐가 빌 때까지 반복
    while queue:
        # 큐에서 하나의 원소를 뽑아 출력하기
        v = queue.popleft()
        print(v, end=' ')
        # 아직 방문하지 않은 인접한 원소들을 큐에 삽입
        for i in graph[v]:
            if not visited[i]:
                queue.append(i)
                visited[i] = True

# 각 노드가 연결된 정보를 표현 (2차원 리스트)
# 그래프 문제 출제 시 1번부터 시작되는 경우 多 => 인덱스 0은 비워둠
graph = [
    [],
    [2, 3, 8],
    [1, 7],
    [1, 4, 5],
    [3, 5],
    [3, 4],
    [7],
    [2, 6, 8],
    [1, 7]
]

# 각 노드가 방문된 정보를 표현 (1차원 리스트)
# 인덱스 0은 사용하지 않기 때문에 하나 더 큰 크기로 리스트 초기화
visited = [False] * 9
bfs(graph, 1, visited)

# 결과 : 1 2 3 8 7 4 5 6

```