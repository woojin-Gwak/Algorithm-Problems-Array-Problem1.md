## BFS란 무엇인가?

**BFS**는 그래프나 트리 구조에서 **너비 우선 탐색**을 의미합니다. 즉, 시작 정점에서 가까운 노드부터 먼저 방문하고, 점차 멀어지는 방식으로 탐색하는 알고리즘입니다.

### BFS의 특징:

- **레이어별 탐색**: 먼저 시작 노드의 인접 노드를 모두 방문한 후, 그 다음 레벨의 노드를 방문합니다.
- **큐(Queue) 사용**: BFS는 방문할 노드를 순서대로 저장하고 꺼내기 위해 큐 자료구조를 사용합니다.
- **최단 경로 보장**: 무방향 그래프에서 BFS를 사용하면 시작 노드에서 다른 모든 노드까지의 최단 경로를 찾을 수 있습니다.

## BFS의 기본 구조

BFS를 구현하기 위해서는 다음과 같은 기본 단계가 필요합니다:

1. **그래프 표현**: 그래프는 인접 리스트(각 노드에 연결된 노드 목록)를 사용하여 표현합니다.
2. **방문 체크**: 각 노드를 방문했는지 여부를 기록하기 위해 방문 배열을 사용합니다.
3. **큐 초기화**: 시작 노드를 큐에 넣고 방문 표시를 합니다.
4. **탐색 반복**:
    - 큐에서 노드를 하나 꺼냅니다.
    - 해당 노드의 모든 인접 노드를 확인합니다.
    - 방문하지 않은 인접 노드를 큐에 넣고 방문 표시를 합니다.
5. **종료 조건**: 큐가 빌 때까지 반복합니다.

### BFS의 흐름도

```
코드 복사
시작 노드 → 인접 노드 1 → 인접 노드 2 → 인접 노드 3 → ...

```

## 예제 코드와 함께 이해하기

간단한 그래프를 예로 들어 BFS를 구현해보겠습니다.

### 예제 그래프

다음과 같은 그래프가 있다고 가정해봅시다:

```lua
lua
코드 복사
1 -- 2
|    |
4 -- 3

```

이 그래프를 인접 리스트로 표현하면 다음과 같습니다:

```python
python
코드 복사
graph = [
    [],         # 0번 노드는 사용하지 않음
    [2, 4],     # 1번 노드와 연결된 노드: 2, 4
    [1, 3],     # 2번 노드와 연결된 노드: 1, 3
    [2, 4],     # 3번 노드와 연결된 노드: 2, 4
    [1, 3]      # 4번 노드와 연결된 노드: 1, 3
]

```

### BFS 구현하기

이제 위 그래프를 BFS로 탐색하는 코드를 작성해보겠습니다.

```python
python
코드 복사
from collections import deque

def bfs(start, graph, visited):
    queue = deque([start])  # 큐 초기화
    visited[start] = True   # 시작 노드 방문 표시

    while queue:
        current = queue.popleft()  # 큐에서 노드 꺼내기
        print(current, end=' ')    # 현재 노드 출력

        for neighbor in graph[current]:  # 인접 노드 확인
            if not visited[neighbor]:
                queue.append(neighbor)    # 큐에 인접 노드 추가
                visited[neighbor] = True # 인접 노드 방문 표시

# 그래프 정의
graph = [
    [],         # 0번 노드는 사용하지 않음
    [2, 4],     # 1번 노드와 연결된 노드: 2, 4
    [1, 3],     # 2번 노드와 연결된 노드: 1, 3
    [2, 4],     # 3번 노드와 연결된 노드: 2, 4
    [1, 3]      # 4번 노드와 연결된 노드: 1, 3
]

n = 4  # 노드의 개수
visited = [False] * (n + 1)  # 방문 체크 리스트 초기화

bfs(1, graph, visited)  # 1번 노드부터 BFS 시작

```

### 코드 설명

1. **그래프 정의**:
    - 인접 리스트 `graph`를 사용하여 그래프를 표현합니다.
    - `graph[i]`는 `i`번 노드에 인접한 노드들의 리스트입니다.
2. **방문 체크 리스트**:
    - `visited = [False] * (n + 1)`은 각 노드의 방문 여부를 저장합니다.
    - 노드 번호가 1부터 시작하므로 인덱스 0은 사용하지 않습니다.
3. **큐 초기화**:
    - `queue = deque([start])`는 시작 노드를 큐에 넣습니다.
    - `visited[start] = True`는 시작 노드를 방문한 것으로 표시합니다.
4. **탐색 반복**:
    - `while queue:`는 큐가 빌 때까지 반복합니다.
    - `current = queue.popleft()`는 큐에서 현재 노드를 꺼냅니다.
    - `print(current, end=' ')`는 현재 노드를 출력합니다.
    - `for neighbor in graph[current]:`는 현재 노드의 모든 인접 노드를 확인합니다.
    - `if not visited[neighbor]:`는 인접 노드가 아직 방문되지 않았다면,
        - `queue.append(neighbor)`는 인접 노드를 큐에 추가합니다.
        - `visited[neighbor] = True`는 인접 노드를 방문한 것으로 표시합니다.

### 실행 결과

위 코드를 실행하면 다음과 같이 출력됩니다:

```
코드 복사
1 2 4 3

```

이 결과는 BFS가 시작 노드 1에서 시작하여 인접 노드 2와 4를 먼저 방문하고, 그 다음 인접 노드 3을 방문했음을 보여줍니다.

## BFS와 DFS의 차이점

- **BFS (너비 우선 탐색)**:
    - 레벨별로 탐색합니다.
    - 최단 경로를 찾는 데 유용합니다.
    - 큐를 사용하여 구현합니다.
- **DFS (깊이 우선 탐색)**:
    - 한 경로를 끝까지 탐색한 후, 다른 경로로 이동합니다.
    - 스택(재귀)을 사용하여 구현합니다.
    - 특정 조건을 만족하는 노드를 찾는 데 유용합니다.

### 예제 비교

위 예제 그래프에서 DFS를 사용하면 다음과 같이 탐색됩니다:

```
코드 복사
1 2 3 4

```

반면, BFS는 다음과 같이 탐색됩니다:

```
코드 복사
1 2 4 3

```

이는 BFS가 너비 우선으로 탐색하기 때문에 먼저 레벨 1의 노드들을 모두 방문하고, 그 다음 레벨로 넘어가기 때문입니다.

## BFS를 활용하는 문제들

BFS는 다양한 문제에서 유용하게 사용됩니다. 몇 가지 예를 들어보겠습니다:

1. **최단 경로 찾기**:
    - 미로 찾기, 그래프에서 두 노드 간의 최단 경로를 찾을 때 사용됩니다.
2. **레벨 순회**:
    - 트리의 각 레벨을 순회할 때 BFS를 사용합니다.
3. **네트워크 연결 확인**:
    - 모든 노드가 연결되어 있는지 확인할 때 사용됩니다.
4. **퍼즐 문제**:
    - 스도쿠, 퍼즐 게임 등에서 최단 이동 횟수를 찾을 때 활용됩니다.

## 연습 문제

BFS를 더 잘 이해하기 위해 간단한 연습 문제를 풀어보세요.

### 연습 문제: 미로 탈출

**문제**: NxM 크기의 미로가 주어졌을 때, (1,1)에서 (N,M)까지 이동하는 최단 경로의 길이를 구하세요. 미로는 0과 1로 이루어져 있으며, 1은 이동할 수 있는 길, 0은 이동할 수 없는 벽을 나타냅니다. 상하좌우로만 이동할 수 있습니다.

**입력 예시**:

```
코드 복사
4 6
1 0 1 1 1 1
1 0 1 0 1 0
1 1 1 0 1 1
0 0 0 0 1 1

```

**출력 예시**:

```
코드 복사
15

```

이 문제는 BFS를 사용하여 최단 경로를 찾는 전형적인 예입니다. 직접 코드를 작성해보며 BFS를 연습해보세요!

## 마무리

**BFS**는 그래프 탐색에서 매우 중요한 알고리즘 중 하나입니다. 너비 우선으로 노드를 탐색하며, 큐를 사용하여 구현됩니다. BFS를 잘 이해하면 다양한 문제를 효율적으로 해결할 수 있습니다.

### 요약

- **BFS**는 너비 우선으로 그래프를 탐색합니다.
- **큐** 자료구조를 사용하여 구현합니다.
- **최단 경로**를 찾는 데 유용합니다.
- **방문 체크**를 통해 중복 방문을 방지합니다.

[백준 1697번: 순간이동](https://www.notion.so/1697-122900cfb74d80759d73d4ed5fbd2d87?pvs=21)

[백준 14940번: 최단거리(미로)](https://www.notion.so/14940-126900cfb74d80dcae2eec981cd1a696?pvs=21)

[백준 7576: 토마토 (여러 시작점)](https://www.notion.so/7576-128900cfb74d80a19540d14e70deafec?pvs=21)

[SWEA 1954 - 달팽이 숫자 (Snail Number)](https://www.notion.so/SWEA-1954-Snail-Number-129900cfb74d8036a762dcf0ad038ab3?pvs=21)

[백준 16953번: A를 B로 만들기](https://www.notion.so/16953-A-B-134900cfb74d80679876fd65ada98da8?pvs=21)
