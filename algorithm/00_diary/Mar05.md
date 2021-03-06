# Mar 05

> 문제 풀이

## SWEA_1258_행렬찾기

> 접근 방법이 잘못 됐던 것 같다. 상자의 시작점과 끝점의 인덱스를 받아 길이를 구하는 방식을 생각했는데, 다른 사람들의 코드를 보고 변경했다. 시작 지점을 받아서 바로 길이를 구하고 그 상자 구간을 0으로 초기화 하는 방식으로 변경

### 내가 사용했던 방식

0이 아니고 방문 기록이 없는 점을 찾는다.

시작점의 인덱스를 저장하고, x방향, y방향 끝점의 인덱스도 함께 저장한다.

3개의 인덱스를 가지고, 상자의 사이즈를 저장하고, 정렬한다.

그 상자의 영역만큼 모두 방문처리한다.

```python
def matrix(array):
    visited = [[0 for _ in range(N)] for _ in range(N)]
    for i in range(N):
        for j in range(N):
            if array[j][i] == 0:
                visited[j][i] = 1
    size = []
    while True:
        for i in range(N):
            for j in range(N):
                if array[j][i] != 0 and visited[j][i] == 0:
                    lux = i
                    luy = j
                    break
            if array[luy][i] != 0 and visited[luy][i] == 0: break

        for i in range(lux, N):
            if array[luy][i] == 0:
                rux = i
                break
        for i in range(luy, N):
            if array[j][lux] == 0:
                ldy = i
                break

        size.append([rux-lux, ldy-luy])

        for i in range(lux, rux):
            for j in range(luy, ldy):
                visited[j][i] = 1

        if 0 not in visited:
            break
    result = []
    size.sort(key=lambda x : x[0]*x[1])
    for i in range(len(size)):
        for j in range(2):
            result.append(size[i][j])

    return result

T = int(input())

for test_case in range(1, T+1):
    N = int(input())
    array = [list(map(int, input().split())) for _ in range(N)]

    print(f'#{test_case}', *matrix(array))
```

이유를 모르겠는 에러로 직접 수정할 수 없어서 다른 답안을 보고 방향을 수정했다.



### 수정한 방향

전체 배열 중, 0이 아닌 곳을 찾는다.

처음 나온 지점에서 각각 x방향 y방향으로 반복문을 시행하고, 0 이 아닌 지점의 위치를 탐색한다. (while 문 사용)

탐색한 위치를 토대로 그만큼의 구간을 0으로 초기화 해서 다음 탐색에서 걸리지 않도록 한다.

반환은 길이를 탐색해서 출력한다.

```python
# 참고한 코드
def find_basket(start):
    x = start[0]
    y = start[1]
 
    # 길이찾기
    while x<N and arr[x][y] != 0:
        x += 1
    x -= 1
    while y<N and arr[x][y] != 0:
        y += 1
    y -= 1
 
    # 방문한 곳 0 초기화
    for i in range(start[0], x+1):
        for j in range(start[1], y+1):
            arr[i][j] = 0
 
    return (x-start[0]+1,y-start[1]+1)
 
 
T = int(input())
for tc in range(1,T+1):
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(N)]
 
    result = []
    for i in range(N):
        for j in range(N):
            if arr[i][j] != 0:
                result.append(find_basket((i, j)))
 
    result.sort(key= lambda x: [x[0]*x[1], x[0]])
    print(f'#{tc}', len(result), end=' ')
    for i in result:
        for j in i:
            print(j, end=' ')
    print()
```



