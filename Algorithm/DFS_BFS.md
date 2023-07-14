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

## 유클리드 호제법
- 최대공약수 계산
- 두 개의 자연수에 대한 최대공약수를 구하는 대표적인 알고리즘
- 