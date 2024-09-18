# DFS & BFS
- 그래프: 정점과 간선으로 이어진 자료구조
- 그래프 탐색: 하나의 정점에서 시작하여 모든 정점들을 한번씩 방문하는 것
- DFS와 BFS는 그래프 탐색의 고전적인 방법


## DFS(Depth-First Search)
- 깊이 우선 탐색: 그래프에서 깊은 부분을 우선 탐색하는 알고리즘
- 한 노드에서 한 방향으로 계속 가다가 더 이상 진행할 수 없으면 다시 이전 노드로 돌아와 다른 경로를 탐색
- 모든 경로를 끝까지 탐색하여 목표를 찾을 때까지 경로를 계속 탐색 -> 특정 경로에서 목표를 빨리 찾을 수 있지만 목표를 찾았더라도 최단 경로를 보장하지 않음

### 자료구조
- **스택** 또는 **재귀 함수**를 이용하여 노드 탐색
- **스택**(동작 원리): FILO(First In Last Out) 구조로 가장 마지막에 삽입된 노드를 먼저 탐색
- **재귀 함수**(구현 방법): 자기 자신을 다시 출하는 함수

### 동작 과정(스택 동작 원리)
1. 탐색 시작 노드를 스택에 삽입하고 방문 처리
2. 스택의 최상단 노드에 방문하지 않은 인접 노드가 있으면 그 인접 노드를 스택에 넣고 방문 처리, 방문하지 않은 인접 노드가 없을 경우 스택에서 최상단 노드를 꺼냄
3. 2번 과정을 더 이상 수행할 수 없을 때까지 반복

### 재귀 함수로 구현
- DFS는 스택을 이용하는 알고리즘으로 주로 재귀 함수로 구현
- 매우 간결하게 구현 가능
```python
# DFS 알고리즘
# graph: 각 노드의 연결 정보 리스트
# start: 탐색을 시작할 노드
# visited: 각 노드의 방문 정보 리스트
def dfs(graph, start, visited): 
    visited[start] = True # 현재 노드 방문 처리
    print(start, end=' ') # 현재 방문한 노드 출력

    # 현재 노드의 모든 이웃 노드 탐색
    for neighbor in graph[start]:
        if not visited[neighbor]: # 이웃 노드가 아직 방문되지 않았을 경우
            dfs(graph, neighbor, visited) # 재귀 함수로 이웃 노드 탐색
```

### 시간 복잡도
> O(N)   
> N: 데이터의 개수


## BFS(Breadth-First Search)
- 너비 우선 탐색: 가까운 노드부터 탐색하는 알고리즘
- 시작 노드에서 가까운 노드부터 탐색하고 점차 멀리 있는 노드를 순차적으로 탐색
- 같은 레벨의 노드를 모두 탐색한 후에 그 다음 레벨의 노드를 탐색
- 최단 경로 탐색에 유리
- DFS보다 실제 수행 시간이 좋은 편
- DFS보다 메모리 사용량이 클 수 있음 -> 큐에 모든 레벨의 노드를 저장해야 하기 때문

### 자료구조
- **큐**를 이용하여 노드 탐색
- **큐**: FIFO(First In First Out) 구조로 탐색할 노드를 큐에 차례대로 넣고 큐에서 꺼내면서 탐색

### 동작 과정
1. 탐색 시작 노드를 큐에 삽입하고 방문 처리
2. 큐에서 노드를 꺼내 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고 방문 처리
3. 2번 과정을 더 이상 수행할 수 없을 때까지 반복
```python
# deque 자료구조 이용(파이썬)
# deque: 스택과 큐의 장점을 모두 채택 -> 데이터를 넣고 빼는 속도가 리스트 자료형에 비해 효율적
from collections import deque

# BFS 알고리즘
# graph: 각 노드의 연결 정보 리스트
# start: 탐색을 시작할 노드
# visited: 각 노드의 방문 정보 리스트
def bfs(graph, start, visited):
    queue = deque([start]) # deque 라이브러리를 이용하여 큐 구현
    visited[start] = True # 현재 노드 방문 처리

    # 큐가 빌 때까지 반복 
    while queue:
        node = queue.popleft() # 큐에서 하나의 원소 뽑음
        print(node, end=' ')
        # 해당 원소와 연결되어 있고 아직 방문하지 않은 원소들을 큐에 삽입
        for neighbor in graph[node]:
            if not visited[node]:
                visited[neighbor] = True # 현재 이웃 노드 방문 처리
                queue.append(neighbor) # 큐에 삽입
```

### 시간 복잡도
> O(N)   
> N: 데이터의 개수

![img](https://github.com/user-attachments/assets/0b86efbb-27bc-450a-a986-de452ca7253e)

---
#### 참고자료 및 출처
- [서적]이것이 취업을 위한 코딩테스트다   
- [사진 출처](https://namu.wiki/jump/JPkbS%2Brz2XNGVohWpoM2khgfYbZZFtSHQQTF3U6pSblXF1Xh%2Ba7uvzKTw05kaN%2BVUX6lqT3r4UFd7iFLlTISZfACksCDG%2BkMofwCy5x3Lu2%2Bsdr2L8SLsKCnUzEJng%2BV)
