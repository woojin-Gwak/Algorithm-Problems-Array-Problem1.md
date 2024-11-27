### DFS와 BFS 모두 포함된 코드:

```python
python
코드 복사
import sys
from collections import deque
input = sys.stdin.readline

# 입력 처리
n, m, v = map(int, input().split())  # 정점 개수 n, 간선 개수 m, 시작 정점 v
graph = [[] for _ in range(n+1)]  # 그래프 초기화

# 간선 정보 입력 받기
for _ in range(m):
    a, b = map(int, input().split())
    graph[a].append(b)
    graph[b].append(a)

# DFS 함수 정의
def dfs(v):
    visit[v] = 1  # 현재 정점 방문 처리
    print(v, end=' ')  # 방문한 정점 출력
    for i in sorted(graph[v]):  # 오름차순으로 인접 정점 탐색
        if not visit[i]:  # 방문하지 않은 정점일 경우
            dfs(i)

# BFS 함수 정의
def bfs(v):
    queue = deque([v])  # 시작 정점을 큐에 넣기
    visit[v] = 1  # 시작 정점 방문 처리
    while queue:
        node = queue.popleft()  # 큐에서 정점 꺼내기
        print(node, end=' ')  # 방문한 정점 출력
        for i in sorted(graph[node]):  # 인접 정점 오름차순 탐색
            if not visit[i]:  # 방문하지 않은 정점일 경우
                queue.append(i)  # 큐에 추가
                visit[i] = 1  # 방문 처리

# 방문 체크 리스트 초기화
visit = [0] * (n+1)
dfs(v)
print()  # DFS와 BFS 사이의 구분을 위해 줄바꿈

# 방문 체크 리스트 초기화 (BFS 실행 전)
visit = [0] * (n+1)
bfs(v)

```

### 주요 설명:

1. **DFS 함수**:
    - `visit` 배열을 사용해 방문한 정점을 기록하며, 인접한 정점들을 재귀적으로 탐색합니다.
    - `sorted(graph[v])`를 사용해 오름차순으로 인접 정점들을 탐색합니다.
2. **BFS 함수**:
    - BFS에서는 `deque`를 사용해 큐를 구현합니다. 큐에 탐색할 정점을 추가하고, `popleft()`를 사용해 앞에서 하나씩 꺼내며 너비 우선으로 탐색합니다.
    - `visit` 배열을 사용해 방문 여부를 체크합니다.
3. **방문 배열 초기화**:
    - DFS와 BFS를 둘 다 실행하려면 방문 배열을 다시 초기화해 주어야 합니다. 각 탐색이 끝난 후, `visit` 배열을 `[0] * (n+1)`로 다시 초기화합니다.
