# 우선순위 큐 (Priority Queue)

- 우선순위가 가장 높은 데이터를 가장 먼저 삭제하는 자료구조

자료구조|추출되는 데이터
:--:|:--:
스택(Stack)|가장 나중에 삽입된 데이터
큐(Queue)|가장 먼저 삽입된 데이터
우선순위 큐(Priority Queue)|가장 우선순위가 높은 데이터

- 구현
    - 리스트, 힙(heap)
    
        우선순위 큐 구현 방식|삽입 시간|삭제 시간
        :--:|:--:|:--:
        리스트|O(1)|O(N)
        힙(Heap)|O(logN)|O(logN)
    
    - 단순히 N개의 데이터를 힙에 넣었다가 모두 꺼내는 작업 = 정렬(힙정렬) => O(NlogN)

## 우선순위 큐 라이브러리를 활용한 힙 정렬 구현

```python
import sys
import heapq
input = sys.stdin.readline

def heapsort(iterable):
    h = []
    result = []
    # 모든 원소를 차례대로 힙에 삽입
    for value in iterable:
        heapq.heappush(h, value)
    
    # 힙에 삽입된 모든 원소를 차례대로 꺼내어 담기
    for i in range(len(h)):
        result.append(heapq.heappop(h))
    
    return result

n = int(input())
arr = []

for i in range(n):
    arr.append(int(input()))

res = heapsort(arr)

for i in range(n):
    print(res[i])
```