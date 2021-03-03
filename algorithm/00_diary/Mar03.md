# Mar 03

> Queue

스택과 마찬가지로 삽입과 삭제의 위치가 제한적인 자료구조.

선입선출구조 (First In First Out)

| 연산            | 기능                                                 |
| --------------- | ---------------------------------------------------- |
| `enQueue(item)` | 큐의 뒤쪽 (rear 다음)에 원소를 삽입하는 연산         |
| `deQueue()`     | 큐의 앞쪽 (front)에서 원소를 삭제하고 반환하는 연산  |
| `createQueue()` | 공백 상태의 큐를 생성하는 연산                       |
| `isEmpty()`     | 큐가 공백상태인지를 확인하는 연산                    |
| `isFull()`      | 큐가 포화상태인지를 확인하는 연산                    |
| `Qpeek()`       | 큐의 앞쪽 (front)에서 원소를 삭제 없이 반환하는 연산 |

### 선형큐

> 1차원 배열을 이용한 큐

`front` : 저장된 첫번째 원소의 인덱스

`rear` : 저장된 마지막 원소의 인덱스

초기상태 : `front` = `rear` = -1

공백상태 : `front` = `rear`

포화상태 : `rear` = `n-1` (`n` : 배열의 크기, `n-1` : 배열의 마지막 인덱스)





### 원형큐





### 암호생성기

> 8개의 숫자를 입력 받아, 사이클을 반복한 후 마지막 자리가 0이 되면 해당 배열을 암호로 출력

```python
def password(numbers):
    while True:
        for j in range(1, 6):

            tmp = numbers.pop(0)
            tmp2 = tmp - j
            if tmp2 <= 0:
                numbers.append(0)
                break
            else:
                numbers.append(tmp2)
        if tmp2 <= 0: break
    return numbers

for _ in range(10):
    test_case = int(input())
    numbers = list(map(int, input().split()))


    print(f'#{test_case}', *password(numbers))
```

1사이클이 1~5를 순차적으로 빼면서 자리를 바꾸는 것이기 때문에 while 문 내에 for 문을 사용하고 같은 조건으로 두번 break 하는 방식을 사용했다.

다른 사람의 코드를 보다보니 두번의 반복문을 사용하지 않고 count를 활용해서 5로 나눈 나머지만큼을 빼주는 방식을 사용해도 더 좋을 것 같았다.