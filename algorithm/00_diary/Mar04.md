# Mar 04

> Queue 실습

## SWEA_5097_회전

> 간단

```python
def rotation(numbers, M):
    idx = M % N
    return numbers[idx]

T = int(input())

for test_case in range(1, T+1):
    N, M = map(int, input().split())
    numbers = list(map(int, input().split()))
    print(f'#{test_case} {rotation(numbers, M)}')
```





## SWEA_5099_피자굽기

> 피자가 화덕에 들어가서 회전, 원형큐를 생각하고 시도하려 했지만 인덱스를 보내야하는 것이기 때문에 인덱스에 해당하는 큐를 생성했다.

```python
def last_pizza(M, N):
    Q = [i for i in range(N)] # 피자 인덱스 정보를 Q에 저장
    Q2 = [i for i in range(N, M)] # 화로에 안들어간 피자들의 idx

    while len(Q) > 1:

        idx = Q.pop(0)
        pizzas[idx] //= 2

        if pizzas[idx] != 0:
            Q.append(idx)
        elif Q2:
            Q.append(Q2.pop(0))

    return Q[0] + 1

T = int(input())

for test_case in range(1, T+1):
    N, M = map(int, input().split())
    pizzas = list(map(int, input().split()))

    print(f'#{test_case} {last_pizza(M, N)}')
```





## SWEA_5102_노드의 거리

> 방향성이 없는 그래프이므로, 양방향의 path를 생성하려고 하니 오류가 났다. (이유는 모르겠다.) 그래서 함수 내에 양쪽으로 확인하는 방식으로 진행했다.

```python
def graph_dist(S, G):
    Q = []
    Q.append(S)
    dist = [0 for _ in range(V + 1)]
    visited = [0 for _ in range(V + 1)]
    visited[S] = 1
    while Q:
        tmp = Q.pop(0)

        for i in range(len(path)):
            if path[i][0] == tmp and visited[path[i][1]] == 0:
                visited[path[i][1]] = 1
                Q.append(path[i][1])
                dist[path[i][1]] = dist[path[i][0]] + 1
            elif path[i][1] == tmp and visited[path[i][0]] == 0:
                visited[path[i][0]] = 1
                Q.append(path[i][0])
                dist[path[i][0]] = dist[path[i][1]] + 1
    return dist[G]

T = int(input())

for test_case in range(1, T + 1):
    V, E = map(int, input().split())
    path = [[0, 0] for _ in range(E)]
    for i in range(E):
        path[i] = list(map(int, input().split()))

    S, G = map(int, input().split())

    print(f'#{test_case} {graph_dist(S, G)}')
```





## SWEA_5105_미로의 거리

> 거리에 대한 array를 추가로 만들어서 각 지점에 도착하는 거리를 기록하는 방식을 사용했다.

```python
def distance(si, sj, N):
    Q = []                                  # 스택 초기화
    visited = [[0]*N for _ in range(N)]         # 방문 기록 array 생성
    dist = [[0] * N for _ in range(N)]

    for i in range(N):                          # 벽은 전부 방문한 것으로 처리
        for j in range(N):
            if maze[j][i] == 1:
                visited[j][i] = 1
    visited[sj][si] = 1                         # 시작 지점 방문기록 남기고
    Q.append((si, sj))                      # 스택에 push

    while Q:
        i, j = Q.pop(0)
        for di, dj in [(0, 1), (1, 0), (0, -1), (-1, 0)]:
            ni = i + di
            nj = j + dj

            if 0 <= ni < N and 0 <= nj < N and visited[nj][ni] == 0:
                Q.append((ni, nj))
                visited[nj][ni] = 1
                dist[nj][ni] = dist[j][i] + 1
        if maze[j][i] == 3:
            return dist[j][i]-1
    return 0

T = int(input())

for test_case in range(1, T+1):
    N = int(input())
    maze = [list(map(int, input())) for _ in range(N)]

    for i in range(N):
        for j in range(N):
            if maze[j][i] == 2:
                si, sj = i, j
    print(f'#{test_case} {distance(si, sj, N)}')
```





## 7일차 미로1

> 이전에 했던 미로와 똑같은 방식인데 Q를 활용하는 방법으로 바꾸었다. 어떤 차이인지는 이론적인 공부를 다시 추가적으로 해봐야 할 것 같다.

```python
def possibility(si, sj, N):
    Q = []                                  # 스택 초기화
    visited = [[0]*16 for _ in range(16)]         # 방문 기록 array 생성
    for i in range(16):                          # 벽은 전부 방문한 것으로 처리
        for j in range(16):
            if maze[j][i] == 1:
                visited[j][i] = 1
    visited[sj][si] = 1                         # 시작 지점 방문기록 남기고
    Q.append((si, sj))                      # 스택에 push

    while Q:
        i, j = Q.pop(0)

        if maze[j][i] == 3:
            return 1
        for di, dj in [(0, 1), (1, 0), (0, -1), (-1, 0)]:
            ni = i + di
            nj = j + dj

            if 0 <= ni < 16 and 0 <= nj < 16 and visited[nj][ni] == 0:
                Q.append((ni, nj))
                visited[nj][ni] = 1

    return 0

T = 10

for test_case in range(1, T+1):
    N = int(input())
    maze = [list(map(int, input())) for _ in range(16)]

    for i in range(16):
        for j in range(16):
            if maze[j][i] == 2:
                si, sj = i, j
    print(f'#{test_case} {possibility(si, sj, N)}')
```





## 느낀 점

Queue에 대해서 완전하게 이해하지는 못했지만, 실습은 무난하게 통과할 수 있었던 것 같다.

무난하게 통과할 수 있었던 이유는 이전에 했던 코드를 참조해가면서 조금씩 수정해서 가능했던 것 같다.

이론적인 공부를 토대로 조금 더 완전하게 이해해서 구현한다면 이전 코드를 하나도 안봐도 해낼 수 있을 것이라 생각한다.