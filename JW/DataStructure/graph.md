
## 그래프

- 무향 그래프, 유향 그래프, 가중치 그래프, 사이클 없는 방향 그래프(DAG)
- |V|: 정점의 개수,  |E|: 그래프에 포함된 간선의 개수
- 인접: 두 개의 정점에 간선이 존재하면 서로 인접해 있다고 한다.
- 순회 방법으로는 크게 DFS > BFS, 백트래킹(가지치기)

---

## 그래프의 표현

1. 인접 행렬

 - 이해하기 쉽고 간선의 존재 여부를 즉각 알 수 있다.
 - $theta(n^2)$ 의 공간, 시간 복잡도
 - 밀도가 높은 그래프에서 적합
    
2. 인접 리스트
- 전통적으로는 연결 리스트에 매달아 구현
- 공간의 낭비가 거의 없으며 간선의 수가 적을 때 유용함
- 밀도가 높을 경우 연결 리스트의 링크 정보를 표현하기 위한 오버헤드만 더 든다.
- 파이썬의 경우 인접 배열을 주로 사용

1. 인접 배열
    
 - 배열 헤더에 연결된 노드 수 저장(여러 개의 배열 사용)
 - 배열 헤더에 인접 배열의 끝 인덱스 저장(하나의 배열 사용)
- 노드들이 메모리에 흩어져서 존재하는 불안 해소
- 연결 리스트의 링크를 위한 오버헤드 절약 가능
- 그래프가 변하지 않는 경우 배열을 사용하면 효율적
- 배열을 정렬하면 이진 탐색도 가능

```python
# 주로 사용하는 방법
graph = {
    1: [2, 3, 4]
    2: [5],
    3: [5],
    4: [],
    5: [6, 7],
    6: [],
    7: [3],
}
```

1. 인접 해시 테이블
- 2배 크기에 해당하는 공간을 할당, 크기로 나눈 나머지를 사용하는 선형 탐색 방법
- 해시 함수는 곱하기 방법 혹은 다른 적절한 방법 사용 가능

---
## 최소신장트리(MST)

- **트리**: 싸이클이 없는 연결된 그래프, 즉 최소한의 간선을 사용하면서 연결된 그래프
- **신장 트리:** 간선을 |V|-1개만 남겨 트리가 되도록 만듦
- **최소 신장 트리**: 무향 그래프에서 만들 수 있는 모든 신장 트리 중 가중치의 합이 가장 낮은 트리

---

## 프림 알고리즘

- 아무 간선도 없는 상태에서 간선을 하나씩 더하는 작업을 |V|-1번 반복
- 정점 집합에 연결하는 데 최소 비용이 드는 정점을 포함(그리디)

    
- 구현
    
    ```python
    def MST_PRIM(G, s): # G: 그래프, s: 시작점
        key = [INF] * N # 가중치를 무한대로 초기화 (최대값으로 설정)
        pi = [None] * N # 트리에서 연결될 부모 정점 초기화
        visited = [False] * N # 방문 여부 초기화
        key[s] = 0 # 시작 정점의 가중치를 0 으로 설정
    
        for _ in range(N):
            minIndex = -1
            min = INF
            for i in range(N):
                # 방문 안한 정점중 최소 가중치 정점 찾기
                if not visited[i] and key[i] < min:
                    min = key[i]
                    minIndex = i
            visited[minIndex] = True # 최소 가중치 정점 방문 처리
    
            for v, val in G[minIndex]: # 선택 정점의 인접한 정점
                if not visited[v] and val < key[v]:
                    key[v] = val       # 가중치 갱신
                    pi[v] = minIndex   # 트리에서 연결될 부모 정점
    
    # heapq 사용 버전
    from collections import defaultdict
    import heapq
    
    def prim(graph, r):
        '''
        Args:
            graph (dict): graph
            r (int): start node
        Returns: None, print weight of MST
        '''
        # 큐 변수: [(거리, 정점)]
        Q = [(0, r)]
        dist = defaultdict(int)
        answer = 0
    
        # 우선순위 큐 최솟값 기준으로 정점연결, 가중치 계산
        while Q:
            d, node = heapq.heappop(Q)
            if node not in dist:
                dist[node] = d
                answer += d
                for v, w in graph[node]:
                    heapq.heappush(Q, (w, v))
        print(answer)
    
    # main
    V, E = map(int, input().split())
    graph = defaultdict(list)
    for _ in range(E):
        u, v, w = map(int, input().split())
        graph[u].append((v, w))
        graph[v].append((u, w))
    prim(graph, 1)
    ```

- 시간복잡도: O(ElogV)
    
    

---

## 크루스칼 알고리즘

- 프림 알고리즘은 하나의 정점 집합을 점점 키워나가는 방식
- 크루스칼 알고리즘은 여러 정점 집합으로 시작해서 집합들을 합쳐나가는 방식
- 각 정점 집합은 싸이클이 없는 연결된 그래프(트리)
- n개의 트리로 시작 → n-1번 트리를 합침
- 모든 트리를 연결하는 간선 중 최소 비용 간선 선택
- 구현
    
    ```python
    # Union-Find
    
    def find(x):
        # find 거슬러 올라가면서 parent[x] 값도 갱신
        if parent[x] == x:
            return x
        parent[x] = find(parent[x])
        return parent[x]
    
    def union(a, b):
        # 제일 작은 원소가 집합을 대변
        a = find(a)
        b = find(b)
    
        if a < b:
            parent[b] = a
        else:
            parent[a] = b
    
    def same_parent(a, b):
        return find(a) == find(b)
    
    # main
    V, E = map(int, input().split())
    edges = []
    for _ in range(E):
        u, v, w = map(int, input().split())
        edges.append((u, v, w))
    edges.sort(key=lambda x: x[2])  # w(weight)가 적은 것부터 정렬
    parent = [i for i in range(V+1)]
    
    ans = 0  # 최소 스패닝 트리의 가중치
    for u, v, w in edges:
        # cost가 작은 edge부터 하나씩 추가해가면서 같은 부모를 공유하지 않을 때(사이클 없을 때)만 확정
        if not same_parent(u, v):
            union(u, v)
            ans += w
    print(ans)
    ```
- 시간복잡도

---

## 안전성 정리

그리디하게 동작하는 두 알고리즘을 통해 만든 신장 트리가 최소 신장 트리임을 보장할 수 있는가?

프림 알고리즘과 크루스칼 알고리즘의 무결성은 아래 정리에 기반한다.

> 간선이 가중치를 갖는 무방향 그래프 G=(V, E)의 정점들이 임의의 두 집합 S와 V-S로 나누어져 있다고 하자. 간선 (u-v)가 S와 V-S 사이의 최소 교차 간선이면 (u-v)를 포함하는 그래프 G의 최소 신장 트리가 반드시 존재한다.
> 

귀류법으로 증명

- 최소 교차 간선 u-v를 포함하지 않으면
- u에서 v로 가는 유일한 path가 존재 → 두 개 이상이라면 cycle이 만들어져 트리가 아니다.
- 여기서 집합 S에서 V-S에 이르는 edge는 최소가 아니므로 최소 신장 트리가 아니게 된다.
---

## 다익스트라 알고리즘(최단경로)

- 모든 간선 가중치가 음이 아닌 경우 → 다익스트라 알고리즘으로 최단 경로를 구할 수 있다.
- 프림 알고리즘과 유사하게 동작
    - 아무 간선도 없는 상태에서 간선을 하나씩 더하는 작업을 |V|-1번 반복
    - 시작 정점에서 정점에 이르는 거리를 저장 → 최단 거리가 가장 짧은 정점을 집합에 추가
- pseudo code

- 작동 과정

- 우선순위 큐 활용 구현
    
    ```python
    def dijkstra(graph, r):
        '''
    
        Args:
            graph (dict):
            r (int): 시작점
    
        Returns:
    
        '''
        # 큐 변수: [(거리, 정점)]
        Q = [(0, r)]
        dist = defaultdict(int)
    
        # 우선순위 큐 최솟값 기준으로 정점까지 최단 경로 삽입
        while Q:
            d, node = heapq.heappop(Q)  # 거리, 노드번호
            if node not in dist:
                dist[node] = d
    						# 후보군 우선순위 큐에 추가
                for v, w in graph[node]:
                    alt = d + w
                    heapq.heappush(Q, (alt, v))
    
    		# 모든 노드의 최단 경로 존재 여부 판별
        if len(dist) == N:
            return max(dist.values())
        return -1
    ```