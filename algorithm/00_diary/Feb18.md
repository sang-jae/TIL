# Feb18

> Algorithm_String 실습

## GNS

> Feb17 수행.

복잡하게 엄청나게 많은 반복문을 이용해서 구현.

다른 사람들의 코드.

→ dict 활용. (나는 아직 dict가 안익숙한가보다. 자꾸 사용하질 못한다. 의식적으로 써먹어봐야지)



## 문자열 비교

보이어-무어 알고리즘을 활용.

100% 활용한건진 몰라도, 그 내용을 최대한 응용해서 했다.

우선 긴 문자열 내에 있는, 짧은 문자열에 포함되는 알파벳의 위치를 저장했다.



그 이후에는 그 위치에만 짧은 문자열을 대보며

다 같으면 통과 다른게 있으면 탈락 하는 방식으로 반복하였다.

코드는 아래와 같다.

```python
T = int(input())

for test_case in range(1, T + 1):
    s = input() # 짧은 문자열 short
    l = input() # 긴 문자열 long
    idx = [] # 긴 문자열 내에 짧은 문자열에 속한 알파벳의 위치를 저장할 list
    result = 0

    for i in range(len(l)): # 긴 문자열 내, 짧은 문자열에 속한 알파벳의 위치를 idx에 append 해줌
        if l[i] in s:
            idx.append(i)

    for i in idx: # 그 인덱스마다 돌면서 slicing 한 구간이 short와 같으면 통과
        if i + len(s) > len(l): # 인덱스가 넘으면 어차피 그 이후에 단어가 나올 순 없으므로 오류가 나지 않게 조건문
            break
        if l[i:i+len(s)] == s: # slicing == short -> 1 출력
            result = 1
            break

    print(f'#{test_case} {result}')
```





## 회문

너무 어렵게 생각했나. 너무 복잡하게 코드가 짜여서, 완성도 못하고 중도 포기.

다른 문제로 refresh 한 뒤 다시 도전해볼 것.



처음에 어렵게 생각한 방법은 문자열 자체로 받지 않고, 한글자 한글자 리스트를 받아서

한글자 한글자 비교하는 방법이었다. 왜냐면 `s[::-1]`에 대해서 몰랐기 때문이다.

그렇게 작성한 코드는 아래와 같았다.

#### 실패한 코드

```python
import sys
sys.stdin = open("input_palindrome1.txt")

T = int(input())

for test_case in range(1, T + 1):
    NM = list(map(int, input().split()))
    N = NM[0]
    M = NM[1]
    arr = [list(input()) for _ in range(N)]
    result = ''
    # 가로로 찾기
    for i in range(N): # y축 인덱스 i 에 대해서 반복
        for j in range(N-M+1): # x축 인덱스, M개 단위로 비교하는 작업 반복할거임
            c = 0
            for k in range(M//2): # 홀수 일 때
                if arr[i][j + k] == arr[i][M - 1 - j - k]:
                    c += 1 # 만약에 c가 M//2 이 된다면 모든 글자가 같다는 말과 같다.
                else:
                    break
            if c == M//2:
                for k in range(j, j+M):
                    result += arr[i][k]
    for i in range(N): # x축 인덱스 i 에 대해서 반복
        for j in range(N-M+1): # y축 인덱스, M개 단위로 비교하는 작업 반복할거임
            c = 0
            for k in range(M//2): # 홀수 일 때
                if arr[j + k][i] == arr[M - 1 - j - k][i]:
                    c += 1 # 만약에 c가 M//2 이 된다면 모든 글자가 같다는 말과 같다.
                else:
                    break
            if c == M//2:
                for k in range(j, j+M):
                    result += arr[k][i]

    print(f'#{test_case} {result}')
```

예시 1,2 에서는 잘 되었는데 3에서 막혔고, 제출 시, 총 10개의 test case에서 3개 밖에 통과하지 못했다.

어디가 문제인지 찾기 힘들었고 다른 사람들의 코드를 조금씩 참고했다.



참고하다보니 내가 파이썬의 능력에 대해서 과소 평가했던 것 같다.

한글자씩 내가 최대한 알려줘야 처리할 수 있을 것이라 생각했고, 그러다보니 코드는 길어지고 오류는 군데군데 생겨난 것 같았다.



최종적으로 수정한 코드는 아래와 같다.

훨씬 간단해진 것을 볼 수 있다. 

#### 최종 코드

``` python
T = int(input())

for test_case in range(1, T+1):
    N, M = list(map(int, input().split()))
    arr = [input() for _ in range(N)]

    # 가로줄 부터
    for i in range(N):
        for j in range(N-M+1):
            s = arr[i][j:j+M]
            if s == s[::-1]:
                print(f'#{test_case} {s}')

    # 세로줄은 문자열이 아니기 때문에 일단 문자열로 만드는 작업이 중간에 필요

    for i in range(N):
        for j in range(N-M+1):
            s = ''
            for k in range(j, j+M):
                s += arr[k][i]
            if s == s[::-1]:
                print(f'#{test_case} {s}')
```





## 글자수

```python
T = int(input())

for test_case in range(1, T+1):
    str1 = input()
    str2 = input()
    max_alpha = ''
    max_value = 0

    for i in str1:
        c = 0
        for j in str2:
            if i == j:
                c += 1
        if c > max_value:
            max_value = c

    print(f'#{test_case} {max_value}')
```

진짜로 회문을 너무 어렵게 생각했나. 글자수는 엄청 간단하게 해결했다.

그냥 str1 내의 모든 알파벳에 대해서

str2 내의 모든 알파벳과 비교하고 같으면 count를 올렸다.

그리고 str1 알파벳 1개 분량의 반복문을 돌고나면 max_value와 비교하여 더 큰 값을 저장하는 방식을 사용했다.



## 회문 2

회문 1도 못했는데 회문 2를 할 수 있을까?

회문 1을 조금 더 간단하게 풀어내야 하지 않을까

문제 이해를 잘못한 것일까?

회문1 먼저 하고 오자





회문 1을 해결하였고, 남들 다 끝내고 놀고 있는 동안. 나는 이제서야 (4시) 오후 과제로 나온 것에 돌입하고 있다.



회문 1 코드를 그대로 가져와서 수정하여 작성하는 과정에서 자꾸 INDEX에러가 떴다.

그 코드는 아래와 같다.

```PYTHON
import sys
sys.stdin = open("input_palindrome2.txt")

T = 10

for test_case in range(1, T+1):
    N = int(input())
    arr = [input() for _ in range(N)]
    max_p = 0

    for M in range(100):
        # 가로줄 부터
        for i in range(100):
            for j in range(100 - M + 1):
                s = arr[i][j:j + M]
                if s == s[::-1] and M > max_p:
                    max_p = M
                else:
                    pass

        # 세로줄은 문자열이 아니기 때문에 일단 문자열로 만드는 작업이 중간에 필요

        for i in range(100):
            for j in range(100 - M + 1):
                s = ''
                for k in range(j, j + M):
                    s += arr[k][i]
                if s == s[::-1] and M > max_p:
                    max_p = M
                else:
                    pass
    print(f'#{test_case} {max_p}')

```

아무리 봐도 이유를 모르겠던 중, `arr = [input() for _ in range(N)]`으로 입력이 100줄씩 안들어가고 N줄씩 들어가서 첫번째 케이스에 1줄이 들어간 사실을 확인할 수 있었다.

수정하여 아래와 같이 코드를 작성하였다.



#### 완성 코드

```python
import sys
sys.stdin = open("input_palindrome2.txt")

T = 10

for test_case in range(1, T+1):
    N = int(input())
    arr = [input() for _ in range(100)]
    max_p = 0

    for M in range(100):
        # 가로줄 부터
        for i in range(100):
            for j in range(100 - M + 1):
                s = arr[i][j:j + M]
                if s == s[::-1] and M > max_p:
                    max_p = M
                else:
                    pass

        # 세로줄은 문자열이 아니기 때문에 일단 문자열로 만드는 작업이 중간에 필요

        for i in range(100):
            for j in range(100 - M + 1):
                s = ''
                for k in range(j, j + M):
                    s += arr[k][i]
                if s == s[::-1] and M > max_p:
                    max_p = M
                else:
                    pass
    print(f'#{test_case} {max_p}')

```





리스트를 새로 생성하는 것은

속도 & 메모리 면에서 좋지 않다.



비교할 문자열을 긴 문자열을 만들어 놓고 하는 것이 아니라

원본의 인덱스만 갖고 할 수 있겠는가 확인해보기



## 쇠막대 자르기

### IDEA 1

() : 레이저 → / 로 치환

(/) : 가장 작은 쇠막대

작은 막대부터 잘라나가는 순서로 코드 작성

#### Code

```python
T = int(input())

for test_case in range(1, T+1):
    pattern = input()

    pattern = pattern.replace('()', '/') # 레이저의 위치를 전부 / 로 치환


    N = pattern.count('/') # 쇠막대를 자를 레이저의 개수 파악
    c = 0 # 자르는 횟수 초기화

    for i in range(1, N+1):
        while True: # 한 레이저로 똑같은 개수를 자르는 크기 다른 막대가 있을 수 있으니 계속 반복한다. (조건 나올때까지)
            # 괄호 바깥의 레이저를 전부 삭제
            if pattern[0] == '/':
                pattern = pattern[1:]
            if pattern[-1] == '/':
                pattern = pattern[:-1]
            # 작은 것 부터 잘라나갈거라 잘라야 하는 문자열 생성
            s = '(' + '/' * i + ')'
            c += pattern.count(s) * (i+1)
            pattern = pattern.replace(s, '/'*i)

            if ('(' + '/'*i + ')') not in pattern: # 더 이상 자를 막대가 없으면 while 문을 벗어나고 다음 크기로 넘어간다.
                break

    print(f'#{test_case} {c}')

```

#### 결과

시간 초과.

생각과 달리 너무 오래 걸렸다. 결과는 맞게 나오지만 시간이 너무 오래걸려 결과적으로 통과하지 못했다.

다른 아이디어가 필요하다.





## List 부분 복습

list2 출제될 만한 것.
색칠하기에서 생각할 만한 것
	문제의 조건에서는 같은 색인 영역은 겹치지 않는다고, 칠하진 영역을 줄 때부터 조건을 주는데, 조건이 없으면 주의해야한다. 비슷한게 있다.
	보라색 영역으로 칠해진 둘레의 총 합 -> 델타 배열에서 보라색이 아닌 칸 수를 다 더하면 외곽 길이가 된다.

특별한 정렬
	선택정렬 or 버블 등. 수도코드를 정확히 구현해서 쓰는 것이 중요
	전체 정렬을 한방에 해놨으면 앞뒤에서 교대로 꺼내도 되고
	sort는 반칙

부분집합의 합
	