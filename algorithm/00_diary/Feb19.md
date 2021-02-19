# Feb19

> Algorithm

## 의석이의 세로로 말해요

비교적 간단한 코딩 이었던 것 같다.

방법은 빈 문자열로 채워진 직사각형 형태의 새로운 array를 만들어

입력 받은 문자열을 채워 넣고 빈 문자열은 그대로 '' 상태로 뒀다.



그렇게 새로 생성한 array를 통해 빈문자열이 확인되면 pass 하고

나머지는 문자열에 추가하는 방법으로 코드를 짰다.

#### Code

```python
import sys
sys.stdin = open("input.txt")

T = int(input())

for test_case in range(1, T + 1):
    str = [list(input()) for _ in range(5)]
    max_len = 0 # 가장 긴 가로 문자열을 찾자.
    result = ''
    # 빈칸은 index 에러가 뜬다.
    for i in range(5): # 가장 긴 가로 문자열 찾기
        if len(str[i]) > max_len:
            max_len = len(str[i])
    # 새로운 리스트를 만든다. 가장 긴 가로 문자열 * 5 에 빈문자열('') 으로 채워진 리스트
    # 그 리스트에 str을 채워 넣고 빈공간은 '-' 으로 둔다.
    new_str = [['' for i in range(max_len)] for i in range(5)]
    for i in range(5):
        for j in range(len(str[i])):
            new_str[i][j] = str[i][j]
    for i in range(max_len): # 가장 긴 가로 문자열 만큼은 반복할 것
        for j in range(5): # 세로 길이만큼 갔다가 위로
            if new_str[j][i] == '':
                pass
            else:
                result += new_str[j][i]

    print(f'#{test_case} {result}')
```



## 쇠막대 자르기

어제까지 2중 for 문으로 구현하였으나, 시간이 초과되어서 방법을 못찾았었다.

강의를 통해

( : count += 1

) : 바로 앞에 ( 가 있다면 레이저로 처리 없다면 막대로 처리. count -= 1









## 시험 전에 체크할 것

1. 파이참으로 디버깅 하는 방법

2. 시간 초과되는지 체크할 방법 (제출하기 전에)

   ```python
   import time
   start = time.time()
   
   print('time :', time.time() - start)
   ```

   

3. A4용지 사두기. 받침대도.



```python
try:
	result += word
except:
	pass
```





## 1979. 어디에 단어가 들어갈 수 있을까

> IM 수준에서 쉬운건 아니다. 비슷?
>
> 210216_2차원 배열







## 과목평가 대비

과목평가는 재주있으면 풀어봐 느낌이 아니라

1문제 = 누구나 풀겠지 / 30분 이내에는 무조건 풀 수준

2문제 = 100점자를 양산시킬 순 없는 문제



문제 내 조건이 꼼꼼하게 적혀있으니 잘 보고 해야 한다.



실행시간이나, 메모리가 초과되는 경우를 어떻게 체크해야 할지

​	과목평가에서는 실행시간이나 메모리는 상관 안해도 되는 듯

​		but 거의 무한루프 수준이면 감점처리 함.

​	IM에서는 체크할 수 있다 사이트에서



#### 추천 문제

오목 판정(D3)





## 오늘의 Tip

2중 3중 포문 1번에 다 빠져나오는건 같은 조건으로 빠져나오는 if 문을 쓰면 된다.