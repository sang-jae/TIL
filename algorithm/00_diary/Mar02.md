# Mar 02

## SWEA_4874_Forth

> 후위표기법으로 나타난 식을 계산하는 알고리즘

계속 수정을 거치는데 런타임에러가 일어났었다.

```python
# 수정 전 코드
def calculator(text):
    sign = ['+', '*', '/', '-']
    stack = []
    for i in text:
        if i == '.':
            if len(stack) == 1:
                return int(stack.pop())
            else:
                break
        elif i in sign:
            if len(stack) >= 2:
                a = int(stack.pop())
                b = int(stack.pop())
                if i == '+':
                    c = a + b
                elif i == '*':
                    c = a * b
                elif i == '-':
                    c = b - a
                elif i == '/':
                    c = b / a
                stack.append(c)
            else:
                break
        else:
            stack.append(i)
    return 'error'

T = int(input())

for test_case in range(1, T+1):
    text = input().split()

    print(f'#{test_case} {calculator(text)}')
```

```python
# 수정 후 코드
def calculator(text):
    sign = ['+', '*', '/', '-']
    stack = []
    for i in text:
        if i == '.':
            if len(stack) == 1:
                return int(stack.pop())
            else:
                break
        elif i in sign:
            if len(stack) >= 2:
                a = int(stack.pop())
                b = int(stack.pop())
                if i == '+':
                    c = a + b
                elif i == '*':
                    c = a * b
                elif i == '-':
                    c = b - a
                elif i == '/':
                    c = b / a
                stack.append(c)
            else:
                break
        else:
            stack.append(i)
    return 'error'

T = int(input())

for test_case in range(1, T+1):
    text = input().split()

    print(f'#{test_case} {calculator(text)}')
```

둘의 차이는 `c`를 계산 후, push할 때 `str`로 push 했는가 아니면 그냥 push 했는가의 차이였다.



문제는 이 것

`20/4`를 파이썬이 계산하면 `5.0`이라는 값이 나온다.

여기에 `int`를 그대로 씌워 `int(20/4)`를 한다면 정상적으로 5라는 값으로 반환되지만

`str`을 씌우는 과정을 거치고 다시 `int`를 씌운다면 `int(str(20/4))`= `int('5.0')`이 되면서 형 변환을 할 수 없게 된다. 따라서 이 코드 때문에 계속 런타임 에러가 났던 것.

해결하기 위해서 str을 제거하고 계속 float 형태로 인식되던 것을 int로 형변환 해도 되지만

애초 식 자체를 `b//a`로 변경하는 방법도 좋을 것 같다.





## SWEA_4875_미로

> 미로 통과할 수 있는 방법이 있는지 유무를 찾는 알고리즘

```python
def possibility(si, sj, N):
    stack = []                                  # 스택 초기화
    visited = [[0]*N for _ in range(N)]         # 방문 기록 array 생성
    for i in range(N):                          # 벽은 전부 방문한 것으로 처리
        for j in range(N):
            if maze[j][i] == 1:
                visited[j][i] = 1
    visited[sj][si] = 1                         # 시작 지점 방문기록 남기고
    stack.append((si, sj))                      # 스택에 push

    while stack:
        i, j = stack.pop()

        if maze[j][i] == 3:
            return 1
        for di, dj in [(0, 1), (1, 0), (0, -1), (-1, 0)]:
            ni = i + di
            nj = j + dj

            if 0 <= ni < N and 0 <= nj < N and visited[nj][ni] == 0:
                stack.append((ni, nj))
                visited[nj][ni] = 1

    return 0


T = int(input())

for test_case in range(1, T+1):
    N = int(input())
    maze = [list(map(int, input())) for _ in range(N)]

    for i in range(N):
        for j in range(N):
            if maze[j][i] == 2:
                si, sj = i, j
    print(f'#{test_case} {possibility(si, sj, N)}')
```

다양한 방법을 교수님이 알려주셨지만, 처음부터 방문기록을 확인하려고 했었기 때문에 그 방법을 사용해서 정리해보았다. 벽은 전부 처음부터 방문처리를 해둔다면 방문기록을 확인하는 방식이 훨씬 편해질 것이라는 생각이 들었고, 성공할 수 있었던 것 같다.



## SWEA_4880_토너먼트 카드게임

> 토너먼트로 가위바위보를 하는 게임 알고리즘

여기서 중요한 것은 조를 어떻게 반복해서 나누느냐 인 것 같다.

재귀를 사용

```python
def rsp(i, j): # 가위, 바위, 보 정리
    if card[i] == 1 and card[j] == 1: # 가위, 가위
        return i
    elif card[i] == 1 and card[j] == 2: # 가위, 바위
        return j
    elif card[i] == 1 and card[j] == 3: # 가위, 보
        return i
    elif card[i] == 2 and card[j] == 1: # 바위, 가위
        return i
    elif card[i] == 2 and card[j] == 2: # 바위, 바위
        return i
    elif card[i] == 2 and card[j] == 3: # 바위, 보
        return j
    elif card[i] == 3 and card[j] == 1: # 보, 가위
        return j
    elif card[i] == 3 and card[j] == 2: # 보, 바위
        return i
    elif card[i] == 3 and card[j] == 3: # 보, 보
        return i

def win(i, j):
    if (j-i) <= 1: # 범위를 줄여나가면서 범위가 0 또는 1일 때는 바로 값을 출력하고
        return rsp(i, j)
    else: # 아닐 경우에는 조건 대로 계속 재귀를 활용
        return rsp(win(i, (i+j)//2), win((i+j)//2+1, j))

T = int(input())

for test_case in range(1, T+1):
    N = int(input())
    card = list(map(int, input().split()))

    print(f'#{test_case} {win(0, N-1)+1}') # 인덱스를 받아와서 실행해왔으므로 마지막에는 +1을 해야 한다.
```

함수를 두 개 작성하여, 하나는 가위바위보 승자를 출력하는 함수, 하나는 재귀함수를 만들었다.

재귀 회수 제한에 걸리지 않아 이 방법이 가능했지만, 재귀를 사용하지 않고 할 수 있는 방법이 있다면 알아두는 것이 좋을 것 같다.



## 6일차 계산기3

```python
def postfix(text): # 후위 표기법으로 변환하는 함수
    numbers = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9'] # 받은 텍스트는 +와 * 때문에 문자열로 인식된다. 편의를 위해 문자열로 정리
    sign = {'(' : 0, '+' : 1, '*' : 2} # 우선순위를 둬야하기 때문에 dict 형식을 선택했다.
    new_str = '' # 후위 표기법으로 변환한 문자를 정리할 새 문자열 초기화
    stack = [] # 부호 스택 초기화
    for i in text: # 문자열의 각 자리 모두에 대해서
        if i in numbers: # 문자열에 해당 자리가 숫자면 그냥 바로 새 문자열 뒤에 붙인다.
            new_str += i
        elif i == '(': # 여는 괄호는 무조건 스택에 push 한다.
            stack.append(i)
        elif i in sign.keys(): # 문자열에 해당 자리가 부호라면 스택을 확인한다. 괄호 제외
            if len(stack) == 0 or sign[i] > sign[stack[-1]]: # 스택의 길이가 0 이거나 우선순위가 높으면 바로 스택에 push 했다.
                stack.append(i)
            else: # 아닌 경우, 조건에 맞을 때까지 stack의 top을 pop 한 후, 새 문자열 뒤에 추가했다.
                while True:
                    j = stack.pop()
                    if j != '(': # 만약에 괄호를 스택에서 뽑아낸 경우에는 패스하고 나머지만 문자열에 추가한다.
                        new_str += j
                    else:
                        pass
                    if len(stack) == 0 or sign[i] > sign[stack[-1]]:
                        break
                stack.append(i) # 조건에 맞게 되면 해당 문자열을 스택에 추가
        elif i == ')': # 닫는 괄호가 나왔을 때
            while stack[-1] != '(': # 여는 괄호 나올때까지 계속 pop 해서 문자열에 추가하고
                new_str += stack.pop()
            stack.pop() # 다 pop하고 나서는 여는 괄호도 제거한다.
    if len(stack) != 0: # 다 끝나고 난 후, 스택에 부호들이 없어질때까지 pop해서 새 문자열 뒤에 추가
        while stack:
            new_str += stack.pop()

    return new_str

def calculator(text): # 위 함수를 통해 만든 후위 표기법을 계산.
    numbers = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9']
    sign = ['+', '*']
    stack = []
    for i in text: # 모든 문자에 대해서 아래 과정을 반복했다.
        if i in numbers: # 숫자라면 스택에 넣고
            stack.append(i)
        elif i in sign: # 부호라면 스택의 top을 2번 pop 해서 연산했다.
            a = int(stack.pop())
            b = int(stack.pop())
            if i == '+':
                c = b + a # a와 b는 문자열로 인식되어 있기 때문에 int로 변환하는 과정이 필요했고
            elif i == '*':
                c = b * a
            stack.append(c) # 다시 스택에 넣을 때는 수식이 꼬이지 않게 하기 위해 다시 str으로 변환하여 넣었다.
    result = stack.pop()
    return result

T = 10

for test_case in range(1, T+1):
    N = int(input())
    text = input()

    print(f'#{test_case} {calculator(postfix(text))}')
```

이전에 작성했던 계산기2의 코드에 괄호 연산을 추가했다.

괄호를 추가하는 것이 생각보다 복잡했다. 그 이유는 괄호를 스택에 넣을 때는 우선순위 상관 없이 넣었었는데

부호끼리 우선순위를 비교하려니 우선순위가 없는 괄호가 걸렸고, 그렇다고 우선순위를 주는 dict에 넣자니 입력할 때가 문제였다.

따라서 if문을 하나 더 추가하여 괄호만 따로 먼저 넣고 그 외의 부호에 대해서 우선순위를 적용하는 방식으로 함수를 짰다.

