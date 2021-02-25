# Feb 23



## 종이 붙이기

```python
# 각 경우의 수를 a_n이라고 했을 때
# a_n = a_(n-1) + 2 * (a_(n-2))
# 라고 할 수 있다.

def paper(n):
    p_case = [1, 1] # N이 10인 경우에도 경우의 수는 1개라고 가정해도 계산에는 문제가 되지 않는다.

    for i in range(2, n+1): # index가 2일 때 이후부터
        p_case.append(p_case[i-1] + 2 * p_case[i-2]) # 위의 수식을 반복해서 작업한다.

    return p_case[n]

T = int(input())

for test_case in range(1, T+1):
    N = int(input()) # 10 단위로 받은 입력값을
    n = N//10 # 10으로 나누어서 함수에 넣기 편하게 만들어주었다.
    print(f'#{test_case} {paper(n)}')
```



## 괄호검사

자꾸 런타임 에러가 난다.

어떤 이유일까

```python
def bracket(txt):
    stack = []
    for i in txt:
        if i == '{' or i == '(':
            stack.append(i)
        if i == '}' and stack[-1] == '{':
            stack.pop()
        elif i == ')' and stack[-1] == '(':
            stack.pop()
        elif i == '}' or i == ')':
            if len(stack) == 0:
                return 0

    if len(stack) == 0:
        return 1
    else:
        return 0

T = int(input())

for test_case in range(1, T+1):
    txt = input()

    print(f'#{test_case} {bracket(txt)}')
```

#### 런타임 에러!

런타임 에러가 발생하는 이유

1. 배열에 할당된 크기를 넘어서 접근했을 때
2. 전역 배열의 크기가 메모리 제한을 초과할 때
3. 지역 배열의 크기가 스택 크기 제한을 넘어갈 때
4. 0으로 나눌 떄
5. 라이브러리에서 예외를 발생시켰을 때
6. 재귀 호출이 너무 깊어질 때
7. 이미 해제된 메모리를 또 참조할 때



문제는 아직도 어떤 부분에서 런타임 에러가 났는지 모르겠다는 것.



## 그래프 경로

#### 교수님 해답

```python
import sys
sys.stdin = open('input.txt')

def f(s, g, V): # s에서 g에 도착할 수 있는지 확인하는 함수
    # 중복 없이 빠짐없이 탐색하는 dfs
    stack = []
    visited = [0] * (V + 1) # 방문기록표 생성
    stack.append(s) # push(s) 갈림길 목록에 시작점 추가
    visited[s] = 1 # visited[s] <- 1 방문예약 표시 (중복된 push 방지)
    while stack: # 스택이 비어있지 않으면 (방문할 곳이 남아있으면)
        n = stack.pop() # 방문할 목록에서 마지막에 기록된 노드를 꺼내
        if n==g: # 방문한 노드가 목적지 g 인지 확인
            return 1 # 경로가 존재
        for i in range(1, V+1):# 모든 노드에 대해, 현재 노드에서 방문할 수 있는 곳인지 검토
            if adj[n][i] == 1 and visited[i] == 0: # 인접하고 미방문인 노드 i를 찾으면
                stack.append(i) # push(i)
                visited[i] = 1
    return 0 # 목적지에 도달하지 못하고 탐색할 노드가 더 이상 없는 경우

T = int(input())

for test_case in range(1, T + 1):
    V, E = map(int, input().split()) # V개의 vertex(node), E개의 edge
    adj = [[0] * (V + 1) for _ in range(V + 1)] # 인접행렬 생성. 초기화 .
    for _ in range(E): # 간선 정보 읽기
        n1, n2 = map(int, input().split()) # 한개의 간선
        adj[n1][n2] = 1 # n1 에서 n2 로 이어짐
        # adj[n2][n1] = 1 # 지금은 방향성 그래프이지만, 무향 그래프에서는 필요

    s, g = map(int, input().split()) # 출발점, 목적지

    print(f'#{test_case} {f(s, g, V)}')
```

교수님은 각 노드에 대해서 검토하는 방법으로 반복문을 돌렸지만

나는 그 접근법을 생각하지 못하고, 입력 받은 그대로 간선 마다 검토하는 방법으로 재귀호출을 하려고 했다.

한 두군데가 아닌 너무 많은 곳에서 오류가 났고, 교수님 답변만 참고해서 이 유형의 슈더코드를 익혀둬야 할 것 같다.





## 반복문자 지우기



```python
import sys
sys.stdin = open('input.txt')

def repeat(text):
    if len(text) < 2:
        return len(text)
    else:
        count = 0
        for i in range(len(text)-1):
            if text[i] == text[i + 1]:
                if i == 0:
                    new_text = text[2:]
                elif i == len(text)-1:
                    new_text = text[:len(text)-2]
                else:
                    new_text = text[:i] + text[i+2:]
                count += 1
                break
        if count == 0:
            return len(text)
        else:
            return repeat(new_text)

    return len(text)

T = int(input())

for test_case in range(1, T+1):
    text = input()

    print(f'#{test_case} {repeat(text)}')
```



그래프 문제보다 먼저 푼 문제로, 계속 습관적으로 재귀를 이용한다.

코드를 잘 짜면 이 문제 처럼 실행이 되지만, 재귀는 꼬이기 십상인 것 같다.

반복문과 재귀를 잘 활용할 수 있는 방법을 다양한 예제를 풀면서 찾아내야 겠다.



## 느낀 점

아직 많이 코드를 짜봐야 할 것 같다.

하루종일 그래프를 붙잡고 있느라 너무 오랜 시간이 걸려 github에 푸시할 시간도 지나버렸지만

고민을 계속 해본데에 의의를 둬야할 것 같다.



## 해야할 것

- [x] python3.5.3 설치
- [ ] 예은님이 올려주신 IM 대비 문제 다 풀어보기
- [ ] 기본형 슈더코드를 익히고 외우자

