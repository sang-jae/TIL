# Feb 24

> Algorithm_stack2

## 계산기

> 문자열로 표현된 계산 식이 주어질 때, 스택을 활용하여 값을 구한다.

step 1. 후위표기법으로 변경 (스택 이용)

step 2. 후위표기법의 수식을 스택을 이용하여 계산.

#### Step 1. 중위 표기법에서 후위 표기법으로의 변환 알고리즘

> 중위표기법 (infix notation)
>
> 후위표기법 (postfix notation)

숫자는 순서대로 새로운 문자열에 넣는다.

부호나 괄호는 우선순위에 따라서 스택에 push 하거나 pop 하여 새로운 문자열에 넣는다.

​	괄호의 경우 스택에서 빠져나올 때 일정 조건에 따라 제거된다.

과정이 익숙하지 않다. 반복을 통해서 익숙해질 것

```python
icp(in-coming priority)
isp(in-stack priority)

if (icp > isp) push()
else pop()
```

| 토큰  | isp  | icp  |
| :---: | :--: | :--: |
|   )   |  -   |  -   |
| * , / |  2   |  2   |
| + , - |  1   |  1   |
|   (   |  0   |  3   |



#### Step2. 후위 표기법에서 계산하는 알고리즘 (Stack)

이번에는 부호가 아닌 숫자를 스택에 push or pop 한다.

후위 표기법으로 표기된 계산식을 가지고, 숫자는 순서대로 스택에 push 한다.

부호가 나오면, 2개를 pop 하여 계산하고 다시 스택에 push 한다.

최종적으로 스택에 남는 1개의 값이 최종 결과 값이 된다.



#### 계산기2

위의 두가지 step을 활용하여 +와 * 만 연산하는 계산기를 만들어보았다.

코드는 아래와 같이, 각 step에 따라 2가지의 함수로 작성하였고 오랜만에 한 번에 성공해보았다.

```python
def postfix(text): # 후위 표기법으로 변환하는 함수
    numbers = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9'] # 받은 텍스트는 +와 * 때문에 문자열로 인식된다. 편의를 위해 문자열로 정리
    sign = {'+' : 1, '*' : 2} # 우선순위를 둬야하기 때문에 dict 형식을 선택했다.
    new_str = '' # 후위 표기법으로 변환한 문자를 정리할 새 문자열 초기화
    stack = [] # 부호 스택 초기화
    for i in text: # 문자열의 각 자리 모두에 대해서
        if i in numbers: # 문자열에 해당 자리가 숫자면 그냥 바로 새 문자열 뒤에 붙인다.
            new_str += i
        elif i in sign.keys(): # 문자열에 해당 자리가 부호라면 스택을 확인한다.
            if len(stack) == 0 or sign[i] > sign[stack[-1]]: # 스택의 길이가 0 이거나 우선순위가 높으면 바로 스택에 push 했다.
                stack.append(i)
            else: # 아닌 경우, 조건에 맞을 때까지 stack의 top을 pop 한 후, 새 문자열 뒤에 추가했다.
                while True:
                    new_str += stack.pop()
                    if len(stack) == 0 or sign[i] > sign[stack[-1]]:
                        break
                stack.append(i) # 조건에 맞게 되면 해당 문자열을 스택에 추가
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
            a = stack.pop()
            b = stack.pop()
            if i == '+':
                c = int(a) + int(b) # a와 b는 문자열로 인식되어 있기 때문에 int로 변환하는 과정이 필요했고
            elif i == '*':
                c = int(a) * int(b)
            stack.append(str(c)) # 다시 스택에 넣을 때는 수식이 꼬이지 않게 하기 위해 다시 str으로 변환하여 넣었다.
    result = stack.pop()
    return result

T = 10

for test_case in range(1, T+1):
    N = int(input())
    text = input()

    print(f'#{test_case} {calculator(postfix(text))}')
```





## 백트래킹 (Backtracking)

> 해를 찾는 도중에 '막히면' (즉, 해가 아니면) 되돌아가서 다시 해를 찾아가는 기법

최적화 (optimization) 문제와 결정 (decision) 문제를 해결할 수 있다.

​	결정 문제 : 문제의 조건을 만족하는 해가 존재하는지 여부를 yes or no로 답하는 문제

​			미로찾기 문제 / n-Queen 문제 / Map coloring / 부분집합의 합 (Subset Sum) 문제 등

### 백트래킹과 깊이우선탐색 (DFS) 의 차이

|           백트래킹            |         깊이우선탐색         |
| :---------------------------: | :--------------------------: |
| 해당 경로가 해결책 X 더이상 X |                              |
|   불필요한 경로를 조기 차단   |       모든 경로를 추적       |
|       일반적으론 줄어듬       | 경우의 수가 너무나 많음 (N!) |
|     최악의 경우 처리 불가     |                              |

### 백트래킹 알고리즘 절차

step 1. 상태 공간 트리의 깊이 우선 검색을 실시

step 2. 각 노드가 유망한지 점검

step 3. 만일 그 노드가 유망하지 않으면, 그 노드의 부모 노드로 돌아가서 검색 계속

```python
# 일반 백트래킹 알고리즘
def checknode(v): # node
    if promising(v):
        if there is a solution at v:
            write the solution
        else:
            for u in each child of v:
                checknode(u)
```

### 상태 공간 트리

순수한 깊이 우선 탐색 : 155 노드

백트래킹 : 27 노드

둘이 어떻게 저 수치가 나올까? 강의를 다시 확인하기

### 부분집합 구하기

```python
# powerset을 구하는 백트래킹 알고리즘
def backtrack(a, k, input):
    global MAXCANDIDATES
    c = [0] * MAXCANDIDATES
    
    if k == input:
        process_solution(a, k) # 답이면 원하는 작업을 한다.
    else:
        k += 1
        ncandidates = construct_candidates(a, k, input, c)
        for i in range(ncandidates):
            a[k] = c[i]
            backtrack(a, k, input)
            
def construct_candidates(a, k, input, c):
    c[0] = True
    c[1] = False
    return 2

MAXCANDIDATES = 100
NMAX = 100
a = [0] * NMAX
backtrack(a, 0, 3)
```



### 순열 구하기

```python
# 순열을 구하는 백트래킹 알고리즘. 접근 방법은 앞서와 유사
def backtrack(a, k, input):
    global MAXCANDIDATES
    c = [0] * MAXCANDIDATES
    
    if k == input:
        for i in range(1, k+1):
            print(a[i], end="")
        print()
    else:
        k += 1
        ncandidates = construct_candidates(a, k, input, c)
        for i in range(ncandidates):
            a[k] = c[i]
            backtrack(a,k,input)

def construct_candidates(a, k, input, c):
    in_perm = [false] * NMAX
    
    for i in range(1, k):
        in_perm[a[i]] = True
    
    ncandidates = 0
    for i in range(1, input+1):
        if in_perm[i] == False:
            c[ncandidates] = i
            ncandidates += 1
    return ncandidates
```



## 분할 정복 알고리즘







## 퀵정렬







## 느낀 점

계산기에서 뿌듯함을 느낌과 동시에 몰아치는 내용들에 멘붕도 함께 찾아왔다.

1차적으로 이전 stack1에서 어떤 부분을 stack에 사용해야할지에 대해서 고민을 했다면, 이번 내용들은 그런 고민은 조금 덜 수 있었던 것 같아서 다행이였다. 물론 아직 완벽히 몰라서 이런 말을 할 수 있는 것이기도 하겠다.



