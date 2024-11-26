# DFS (깊이 우선 탐색) 기본 개념 및 팁

## 1. DFS(Depth-First Search)란?

DFS는 **깊이 우선 탐색**으로, 그래프 또는 트리의 노드를 탐색하는 알고리즘입니다. DFS는 한 방향으로 깊게 탐색을 진행하다가 더 이상 진행할 수 없으면, 이전 노드로 돌아가서 다른 방향을 탐색하는 방식입니다.

### DFS의 특징
- **스택 방식**: DFS는 현재 노드에서 인접한 노드를 방문하고, 다시 그 노드의 인접 노드로 가는 방식입니다. 깊이 우선으로 탐색하므로, 후입선출(LIFO) 방식의 스택을 사용하여 구현됩니다.
- **재귀적 구현**: DFS는 보통 재귀를 사용하여 구현되며, 각 노드를 방문할 때마다 그 노드의 인접 노드를 계속 탐색합니다.

## 2. DFS의 구현 방법

### 1) 그래프의 표현 방법
- **인접 행렬**: 2차원 배열을 사용하여 노드 간의 연결 여부를 나타냅니다.
- **인접 리스트**: 각 노드에 연결된 노드를 리스트 형태로 저장합니다.

### 2) DFS 알고리즘 구현 (재귀 방식)

```python
def dfs(graph, node, visited):
    # 현재 노드를 방문 처리
    visited[node] = True
    print(node, end=' ')

    # 인접 노드 방문
    for neighbor in graph[node]:
        if not visited[neighbor]:
            dfs(graph, neighbor, visited)
3) DFS 알고리즘 구현 (스택 방식)
python
def dfs(graph, start):
    visited = [False] * len(graph)
    stack = [start]

    while stack:
        node = stack.pop()
        if not visited[node]:
            visited[node] = True
            print(node, end=' ')

            # 인접한 노드를 스택에 넣기 (역순으로 넣어야 깊이 우선)
            for neighbor in reversed(graph[node]):
                if not visited[neighbor]:
                    stack.append(neighbor)
3. DFS 활용 팁
그래프 탐색: DFS는 트리나 그래프에서 특정 조건을 만족하는 노드를 찾을 때 유용합니다.
경로 찾기: 경로가 존재하는지 여부를 확인할 때 DFS를 사용할 수 있습니다. (예: 미로 찾기)
최단 경로가 아닐 수 있음: DFS는 깊이를 우선으로 탐색하므로, 반드시 최단 경로를 찾지 않습니다. 최단 경로를 찾는 문제에서는 BFS를 사용하는 것이 적합합니다.
백트래킹: DFS는 백트래킹(Backtracking) 문제에서 매우 효과적입니다. 예를 들어, 가능한 모든 경로를 탐색하고 조건에 맞는 경로를 선택하는 문제에서 사용됩니다.
4. 시간 복잡도
그래프가 V개의 정점과 E개의 간선을 가질 때, DFS의 시간 복잡도는 O(V + E)입니다. 각 정점과 간선을 한 번씩만 방문하기 때문입니다.
5. 예시 문제
문제: 주어진 그래프에서 DFS를 이용해 모든 노드를 탐색하시오.

입력
코드 복사
5
0 1 2
1 0 3 4
2 0
3 1
4 1
출력
코드 복사
0 1 3 4 2
코드
python
코드 복사
graph = {
    0: [1, 2],
    1: [0, 3, 4],
    2: [0],
    3: [1],
    4: [1]
}

visited = [False] * 5

def dfs(graph, node, visited):
    visited[node] = True
    print(node, end=' ')
    
    for neighbor in graph[node]:
        if not visited[neighbor]:
            dfs(graph, neighbor, visited)

dfs(graph, 0, visited)

6. 추가 참고 사항
DFS vs BFS: DFS는 스택 방식으로 구현되고, BFS는 큐 방식으로 구현됩니다. DFS는 깊이를 우선적으로 탐색하지만, BFS는 너비를 우선적으로 탐색합니다. 문제의 특성에 따라 적절한 탐색 방법을 선택해야 합니다.
재귀 깊이 제한: 파이썬에서는 재귀 깊이에 제한이 있을 수 있으므로, 깊이가 깊은 문제를 풀 때는 스택 방식으로 구현하는 것이 좋습니다.
