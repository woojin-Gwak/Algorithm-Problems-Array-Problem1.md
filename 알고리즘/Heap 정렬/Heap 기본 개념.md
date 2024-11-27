# <Heap 정렬>
: 힙(Heap)은 데이터의 우선순위를 관리하기 위한 효율적인 자료구조입니다. 주로 우선순위 큐(Priority Queue)를 구현하는 데 사용됩니다. 
### 1. 힙의 기본 개념

- **힙**: 완전 이진 트리의 특성을 가진 자료구조로, 데이터의 추가 및 삭제를 효율적으로 처리합니다.
- **우선순위 큐**: 데이터가 들어오는 순서와 관계없이 우선순위에 따라 데이터를 처리할 수 있도록 해줍니다.

### 2. 힙의 유형

- **최소 힙 (Min Heap)**:
    - 부모 노드의 값이 자식 노드의 값보다 작거나 같은 구조.
    - 루트 노드에 가장 작은 값이 위치합니다.
- **최대 힙 (Max Heap)**:
    - 부모 노드의 값이 자식 노드의 값보다 크거나 같은 구조.
    - 루트 노드에 가장 큰 값이 위치합니다.

### 3. 힙의 특징

- **완전 이진 트리**: 모든 레벨이 완전히 채워져 있으며, 마지막 레벨은 왼쪽부터 채워집니다.
- **삽입과 삭제**: O(log n) 시간 복잡도로 수행됩니다. 삽입 시에는 새로운 값을 추가하고, 삭제 시에는 루트 노드를 제거한 후 힙 구조를 재정렬합니다.
- **배열 기반 구현**: 일반적으로 배열로 구현되며, 부모와 자식 간의 인덱스 관계를 통해 관리됩니다.

### 4. Python에서 힙 사용하기

Python에서는 `heapq` 모듈을 사용하여 힙을 쉽게 구현하고 관리할 수 있습니다.

### 4.1. 기본 사용법

1. **모듈 임포트**
    
    ```python
    python
    코드 복사
    import heapq
    
    ```
    
2. **빈 힙 생성**
    
    ```python
    python
    코드 복사
    heap = []
    
    ```
    
3. **요소 추가**
    - `heapq.heappush(힙, 요소)`: 요소를 힙에 추가합니다.
    
    ```python
    python
    코드 복사
    heapq.heappush(heap, 5)
    heapq.heappush(heap, 1)
    heapq.heappush(heap, 3)
    
    ```
    
4. **가장 작은 요소 꺼내기**
    - `heapq.heappop(힙)`: 힙에서 가장 작은 요소를 제거하고 반환합니다.
    
    ```python
    python
    코드 복사
    smallest = heapq.heappop(heap)  # 1
    
    ```
    
5. **리스트를 힙 구조로 변환**
    - `heapq.heapify(리스트)`: 주어진 리스트를 힙 구조로 변환합니다.
    
    ```python
    python
    코드 복사
    nums = [5, 1, 3]
    heapq.heapify(nums)  # nums가 힙 구조로 변환됨
    
    ```
    
6. **최소 요소 접근**
    - `heap[0]`: 현재 힙에서 가장 작은 요소에 접근합니다.
    
    ```python
    python
    코드 복사
    print(heap[0])  # 현재 힙의 최소 요소
    
    ```
    
7. **여러 요소를 한 번에 추가**
    - `heappush()`를 반복적으로 호출할 필요 없이, 한 번에 여러 요소를 추가할 수 있습니다.
    
    ```python
    python
    코드 복사
    elements = [4, 6, 2]
    for elem in elements:
        heapq.heappush(heap, elem)
    
    ```
    

### 4.2. 최대 힙 구현

Python의 `heapq`는 기본적으로 최소 힙을 제공합니다. 최대 힙을 구현하기 위해서는 다음과 같이 음수로 변환하여 사용합니다.

```python
python
코드 복사
import heapq

# 원래 리스트
nums = [5, 1, 3, 7, 2]

# 최대 힙으로 변환
max_heap = [-num for num in nums]  # 음수로 변환
heapq.heapify(max_heap)              # 최소 힙으로 변환

# 최대 힙으로 사용
print([-heapq.heappop(max_heap) for _ in range(len(max_heap))])  # [7, 5, 3, 2, 1]

```

### 5. 사용 사례

- **다익스트라 알고리즘**: 최단 경로 알고리즘에서 사용됩니다.
- *A 알고리즘*: 경로 탐색 알고리즘에서 활용됩니다.
- **스케줄링 문제**: 작업 우선순위를 관리하는 데 유용합니다.

### 6. 결론

- 힙은 우선순위 큐를 구현하는 데 적합한 자료구조로, 삽입 및 삭제가 효율적입니다.
- Python의 `heapq` 모듈을 사용하여 간편하게 힙을 관리할 수 있으며, 최소 힙과 최대 힙을 모두 구현할 수 있습니다.

### 힙으로 절댓값 출력하기

```python
import heapq
import sys
input = sys.stdin.readline

n = int(input())
heap = []

for _ in range(n):
    x = int(input())
    if x != 0:
        # 절댓값 기준으로 추가
        heapq.heappush(heap, (abs(x), x))  # (절댓값, 원래 값) 형태로 추가
    else:
        if len(heap) > 0:
            # 가장 작은 절댓값을 출력하고, 원래 값 출력
            print(heapq.heappop(heap)[1])  # 원래 값 출력
        else:
            print(0)  # 힙이 비어있다면 0 출력

```
