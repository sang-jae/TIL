# Feb16

> List 2 Algorithm. Samsung SW Expert Academy



## Ladder

#### 실패한 코딩

```python
import sys
sys.stdin = open("input_ladder.txt")

def ladder(arr, pnt = [0,0]): # 아래로 내려가는 함수
    # 3방향의 데이터에 따라서 좌로 갈지, 우로 갈지, 아래로 갈지 함수 호출 방식
    if pnt[1] == 99: # 맨 아래줄로 왔다면, 결과값으로 출력
        if arr[pnt[0]][pnt[1]] == 2:
            return 1
        else:
            return 0
    else: # 맨 아래줄 아닌 경우
        if pnt[0] == 0:
        # 맨 왼쪽 줄일 때는 아래나 오른쪽으로만
            if arr[pnt[0] + 1][pnt[1]] == 1:
                return ladder_right(arr, [pnt[0]+1, pnt[1]])
            else:
                return ladder(arr, [pnt[0], pnt[1] + 1])
        elif pnt[0] == 99:
        # 맨 오른쪽 줄 일떄는 아래나 왼쪽으로만
            if arr[pnt[0] - 1][pnt[1]] == 1:
                return ladder_left(arr, [pnt[0]-1, pnt[1]])
            else:
                return ladder(arr, [pnt[0], pnt[1] + 1])

        else:
        # 그 외에는 전부 가능
            if arr[pnt[0] - 1][pnt[1]] == 1:
                return ladder_left(arr, [pnt[0]-1, pnt[1]])
            elif arr[pnt[0] + 1][pnt[1]] == 1:
                return ladder_right(arr, [pnt[0]+1, pnt[1]])
            else:
                return ladder(arr, [pnt[0], pnt[1] + 1])

def ladder_right(arr, pnt = [0,0]):
    if arr[pnt[0]+1][pnt[1]] == 0:
        return ladder(arr, [pnt[0], pnt[1] + 1])
    else:
        return ladder_right(arr, [pnt[0]+1, pnt[1]])

def ladder_left(arr, pnt = [0,0]):
    if arr[pnt[0]-1][pnt[1]] == 0:
        return ladder(arr, [pnt[0], pnt[1] + 1])
    else:
        return ladder_left(arr, [pnt[0]-1, pnt[1]])

T = 10

for test_case in range(1, T + 1):
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(100)]
    for i in range(100):
        final = ladder(arr, [i, 0])
        if final == 1:
            result = i
            break
        else:
            pass

    print(f'#{test_case} {result}')
```

#### 실패한 이유

→ `x, y`를 바꿔서 생각하고 코드를 짰다.

→ 재귀를 사용해서 너무 복잡하고, 재귀 제한을 넘어가는 문제도 있었던 것 같다.

→ if 문이 너무 많이 들어가면서 코드가 길어졌고, index를 확실하게 제한하지 못했던 것 같다.



#### 수정 방안

아래 사진 처럼 도표를 짰다.

![feb16_img_ladder](C:\Users\sangj\TIL\algorithm\00_diary\feb16_img_ladder.jpg)

이 도표를 토대로 아래와 같이 코드를 작성할 예정.

문제점 1. 1칸을 나아간 후, 좌 우 모두 1인 경우가 생김. = 지나간 칸은 0으로 만들기.

#### 수정 코드 (수정 필요)

```python
import sys
sys.stdin = open("input_ladder.txt")

def fuction():
    pass

T = 10
for test_case in range(1, T + 1):
    N = int(input())
    
```



#### 다른 아이디어

사다리는 n 개의 선택지를 기준으로 n개의 축을 가지고 이루어져 있다.

사다리에서 point가 움직이는 기준은 1칸 기준이 아니라, 교차점 기준이라고 생각할 수 있다.

세로 축에 대한 정보를 list에 저장하고 교차점에서 좌우를 살핀 다음, 그 방향으로 다음 index의 y값으로 이동.

도표는 아래와 같다.





#### 느낀 점

차분하게 코드를 작성해야겠다는 생각이 들었다.

지금까지는 머리 속으로만 코딩을 하느라, 더 복잡하고 깔끔하지 않은 형태로 진행 되었던 것 같다. 위와 같은 도표를 그려서 코딩을 더욱 간단하게 할 수 있도록 구상하고, 그 후 구현하는 것이 가장 중요할 것 같다.



사실 설 연휴부터 지금까지 공부를 조금 소홀히 했다.

어느 정도 따라갈 수 있구나 라는 생각으로 안일하게 공부량을 줄이고 TIL 작성도 미뤄두고 쉬었다. Python 과정과 Web 과정을 빡세게 따라가느라, 조금 지쳤던 것은 아닐까 싶기도 했다.

이제 다시 TIL 도 열심히 작성하고, 사소한 알고리즘이라도 위 사진과 같은 도표를 작성하면서 코딩하는 습관을 길러봐야겠다.