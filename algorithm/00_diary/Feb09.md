# Feb 09

> Algorithm

### 요약

SW Expert Academy에 있는 다양한 알고리즘 문제 풀이를 통해 알고리즘에 대해서 공부를 진행했다.



### 느낌

역량을 키우기 위해서 내장함수 사용하지 않는 조건으로 문제풀이를 하다보니 조금 난감한 부분이 있었다.

특히 마지막 문제 같은 경우에는 어떤 부분에서 오류가 났는지 전혀 발견을 하지 못해서 아직도 Fail인 상태로 남아있고, 잠시 포기하고 이제서야 TIL을 작성한다.



### 공부내용

min max / 구간합 / 숫자 카드 / 전기버스 / 간단한 소인수분해 / 현주의 상자 바꾸기 / Flatten

총 7개의 문제를 풀었다. Flatten의 경우 풀리지 않아 일단은 오늘은 그만두고 내일 다시 풀려고 한다.

잊지 않도록 오늘 작성했던 Flatten 코드와 결과를 아래에 기록해두려고 한다.

```python
T = 10
# 여러개의 테스트 케이스가 주어지므로, 각각을 처리합니다.
for test_case in range(1, T + 1):
    N = int(input())
    boxes = list(map(int, input().split()))

    # 최대 최소를 계속 찾아야하는데 max min 사용 X????
    # 최대와 최소를 찾는 과정을 계속 반복해야 하는데

    for i in range(N): # 일단은 필요한 전체 반복문을 돌리자.
        max_box = boxes[0]     # 내부에 최대 높이와 최소 높이를 초기화
        min_box = boxes[0]

        for box in boxes:
            if box > max_box:
                max_box = box
            if box < min_box:
                min_box = box

        for i in range(100):
            if boxes[i] == max_box:
                boxes[i] -= 1
                break  # 중복 제거 되지 않게 안전하게 break

        for j in range(100):
            if boxes[j] == min_box:
                boxes[j] += 1
                break

    for box in boxes:   # 최대 최소값이 중복인 경우나 중복이 아닌 경우에 따라 다르기 때문에 최종적으로 다시 최대최소 체크
        if box > max_box:
            max_box = box
        if box < min_box:
            min_box = box

    result = max_box - min_box

    print(f'#{test_case} {result}')
```

```html
<!--결    과-->
#1 13
#2 32
#3 54
#4 25
#5 87
#6 15
#7 39
#8 26
#9 13
#10 29
```

#6 에 나와야 하는 결과는 15가 아닌 14이고 어느 부분에서 실수가 있었는지 다시 처음부터 작성하며 확인해봐야할 것 같다.

내일 TIL에 다시 정리하도록 하겠다.



