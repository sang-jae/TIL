# Feb 25

>IM 대비 알고리즘 풀어보기

## SWEA_1289_메모리 복구

```python
def memory(G):
    S = ['0'] * len(G)
    count = 0
    for i in range(len(G)):
        if G[i] == S[i]:
            continue
        else:
            if G[i] == '1':
                S[i:] = ['1'] * len(S[i:])
            elif G[i] == '0':
                S[i:] = ['0'] * len(S[i:])
            count += 1
        if S == G:
            break
    return count

T = int(input())

for test_case in range(1, T+1):
    G = list(input())
    print(f'#{test_case} {memory(G)}')
```

## SWEA_3499_퍼펙트 셔플

```python
def shuffle(card):
    if N%2 == 1:
        c = N//2 +1
    else:
        c = N//2
    pass

    shuffle_card = []
    for i in range(N//2):
        shuffle_card.append(card[i])
        shuffle_card.append(card[i + c])

    if N%2 == 1:
        shuffle_card.append(card[N//2])
    else:
        pass

    return ' '.join(shuffle_card)

T = int(input())

for test_case in range(1, T+1):
    N = int(input())
    card = list(map(str, input().split()))

    print(f'#{test_case} {shuffle(card)}')
```

## SWEA_1859_백만장자

Runtime error

test case 1000개 중 900개 가량 맞추고 실패



## SWEA_4615_오셀로

``` python
def Oselo(N, turn_info):
    board = [[0 for _ in range(N)] for _ in range(N)] # board 초기화
    board[N//2][N//2] = 2# board 가운데 색상 설정. 1: 흑 2: 백
    board[N//2 - 1][N//2 - 1] = 2
    board[N//2 - 1][N//2] = 1
    board[N//2][N//2 - 1] = 1

    # 방향 설정
    dx = [0, 1, 1, 1, 0, -1, -1, -1]
    dy = [-1, -1, 0, 1, 1, 1, 0, -1]

    for i in turn_info: # 모든 turn_info 정보에 대해서
        x = i[0] - 1 # x, y 좌표를 index에 맞게 -1
        y = i[1] - 1
        c = i[2]
        board[y][x] = c
        for j in range(8): # 놓은 자리 주변 8방향에 놓은 돌과 다른 색인 돌을 찾기 위해 각 방향을 탐색한다.
            nx = x + dx[j]
            ny = y + dy[j]
            # 먼저 nx, ny가 board 경계 밖으로 나가지 않는 경우만 탐색해야 한다. 또한 돌이 채워지지 않거나 색이 같은 경우도 제외한다.
            if 0 <= nx < N and 0 <= ny < N and board[ny][nx] != 0 and board[ny][nx] != c:
                # 만약에 다른색이 있는 방향을 찾았다면? 그 방향으로 계속 탐색해서 다른 색이 나오거나 끝이 나오는지 확인해야 한다.
                change_list = []# 탐색해서 바꾸어주어야 할 리스트를 초기화 시켜둔다.
                while True:
                    change_list.append([nx, ny])
                    nx += dx[j]
                    ny += dy[j]
                    if nx < 0 or nx >= N or ny < 0 or ny >= N:
                        break
                    else:
                        if board[ny][nx] == c:
                            for [a, b] in change_list:
                                board[b][a] = c
                            break
                        elif board[ny][nx] == 0:
                            break
    count1 = 0
    count2 = 0
    for i in range(N):
        for j in range(N):
            if board[i][j] == 1:
                count1 += 1
            elif board[i][j] == 2:
                count2 += 1

    return [str(count1), str(count2)]

T = int(input())

for test_case in range(1, T+1):
    N , M = map(int, input().split())
    turn_info = [list(map(int, input().split())) for _ in range(M)]
    result = ' '.join(Oselo(N, turn_info))
    print(f'#{test_case} {result}')
```





## 진기의 최고급 붕어빵

도착 순서대로 시간이 나오는게 아니다.

연속해서 오는게 아니다. 그냥 0에서부터 오는 거







## 오셀로

진짜로 모르겠다 감도 못잡겠음

참고할 코드들

```python
# 전선규 님 코드


T = int(input())
 
for tc in range(1, T+1):
    n, m = map(int, input().split())  # n: 한 변의 길이, m: 플레이 횟수
 
    # 오셀로 판 만들기
    board = [[0] * n for _ in range(n)]
 
    # 초기 돌 4개 초기화
    point = n // 2 - 1
    board[point][point] = 'w'
    board[point+1][point+1] = 'w'
    board[point+1][point] = 'b'
    board[point][point+1] = 'b'
 
    # delta
    delta_x = [0, 1, 1, 1, 0, -1, -1, -1]
    delta_y = [-1, -1, 0, 1, 1, 1, 0, -1]
    for _ in range(m):
        y, x, stone = map(int, input().split())
        y -= 1
        x -= 1
 
        # 돌 바꾸기
        if stone == 1:
            stone = 'b'
        else:
            stone = 'w'
 
        # 우선 돌 놓기
        board[y][x] = stone
 
        # 8방 검사
        for i in range(8):
            nx = x+delta_x[i]
            ny = y+delta_y[i]
 
            if 0 <= nx < n and 0 <= ny < n and board[ny][nx] != stone and board[ny][nx] != 0:
                _nx = nx
                _ny = ny
                check = False
                while 0 <= _nx < n and 0 <= _ny < n:  # 0~n 사이에서 돌면서 확인
                    _nx += delta_x[i]
                    _ny += delta_y[i]
                    if 0 <= _nx < n and 0 <= _ny < n:
                        if board[_ny][_nx] == stone:
                            check = True
                            break
                        elif board[_ny][_nx] == 0:
                            break
 
                if check:  # 뒤에 같은 색깔 돌이 있으면 nx~흰돌 나올 때까지 stone으로 변경
                    __nx = nx
                    __ny = ny
                    while board[__ny][__nx] != stone:
                        board[__ny][__nx] = stone
                        __nx += delta_x[i]
                        __ny += delta_y[i]
 
 
    w_cnt = 0
    b_cnt = 0
    for i in range(n):
        for j in range(n):
            if board[i][j] == 'w':
                w_cnt += 1
            elif board[i][j] == 'b':
                b_cnt += 1
 
    print(f'#{tc} {b_cnt} {w_cnt}')
```





```python
# 강인영 님 코드

def othello(arr, n, r, c, p):
    r = r-1
    c = c-1
 
    # 상하좌우대각선 탐색
    dr = [-1, 1, 0, 0, -1, 1, 1, -1]
    dc = [0, 0, -1, 1, 1, 1, -1, -1]
 
    for i in range(8):
        rr = r + dr[i]
        cc = c + dc[i]
        change = []
        while 0 <= rr < n and 0 <= cc < n and arr[rr][cc] > 0 :
                if arr[rr][cc] != p:
                    change.append([rr, cc])
                    rr += dr[i]
                    cc += dc[i]
 
                elif arr[rr][cc] == p:
                    if len(change) != 0:
                        arr[r][c] = p
                        for k in change:
                            arr[k[0]][k[1]] = p
                        break
 
                    else:
                        break
 
    return arr
 
 
t = int(input())
 
for tc in range(1, t+1):
    n, m = map(int, input().split())
    arr = []
    for _ in range(n):
        arr.append([0] * n)
 
    # 최초 돌 세팅
    arr[n//2-1][n//2-1] = arr[n//2][n//2] = 2
    arr[n//2-1][n//2] = arr[n//2][n//2-1] = 1
 
    for _ in range(m):
        r, c, p = map(int, input().split())
        arr = othello(arr, n, r, c, p)
 
    cnt_B = 0
    cnt_W = 0
    for x in range(n):
        for y in range(n):
            if arr[x][y] == 1:
                cnt_B += 1
            elif arr[x][y] == 2:
                cnt_W += 1
 
    print(f'#{tc} {cnt_B} {cnt_W}')
```



```python
# 이용훈님 코드

T = int(input())
for tc in range(1, T + 1):
    N, M = map(int, input().split())
    # 8방향
    dr = [-1,-1,-1, 0, 1, 1, 1, 0]
    dc = [-1, 0, 1, 1, 1, 0, -1, -1]
     
    arr = [[0] * (N+2) for _ in range(N+2)]
    # 정가운데에 돌 놓고 시작해야함.. 이거 뺴고 해서 틀림
    arr[N//2][N//2] = 2
    arr[N//2][N//2 + 1] = 1
    arr[N//2 + 1][N//2 + 1] = 2
    arr[N//2 + 1][N//2] = 1
    stack = []
    # 탐색 종료 조건 : 0을 만났을 때는 그냥 stack 초기화, 같은 색 돌을 만났으면 스택 안에 든 다른 색 돌을 같은 색 돌로 바꾸기
 
    # 1은 흑돌, 2는 백돌, 0은 무소유
    for _ in range(M):
        r, c, color = map(int, input().split())
        # 돌 놓기
        arr[r][c] = color
 
        # 8방향 탐색
        for i in range(8):
            temp_r = r
            temp_c = c
            while True:
 
                temp_r = temp_r + dr[i]
                temp_c = temp_c + dc[i]
                if arr[temp_r][temp_c] == 0:
                    stack = []
                    break
                elif arr[temp_r][temp_c] != color:
                    stack.append([temp_r, temp_c])
                else:
                    for idx in stack:
                        arr[idx[0]][idx[1]] = color
                    stack = []
                    break
 
    black = 0
    white = 0
    for i in range(1, N+1):
        for j in range(1, N+1):
            if arr[i][j] == 1: black+=1
            elif arr[i][j] == 2: white+=1
 
    print(f'#{tc} {black} {white}')
```

