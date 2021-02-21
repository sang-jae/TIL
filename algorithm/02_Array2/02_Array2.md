# Array2

### 배열 : 2차 배열

> 1차원 List를 묶어놓은 List

#### 배열 순회

```python
# 행 우선 순회
for i in range(len(Array)):
    for j in range(len(Array[i])):
        Array[i][j]
```

```python
# 열 우선 순회
for j in range(len(Array[0])):
    for i in range(len(Array)):
        Array[i][j]
```

``` python
# 지그재그 순회
for i in range(len(Array)):
    for j in range(len(Array[0])):
        Array[i][j + (m-1-2*j) * (i % 2)]
```

``` python
# 델타를 이용한 2차 배열 탐색
# - 2차 배열의 한 좌표에서 4방향의 인접 배열 요소를 탐색하는 방법

arr[0...n-1][0...n-1]
dx[] <- [0, 0, -1, 1] # 상 하 좌 우
dy[] <- [-1, 1, 0, 0] # 상 하 좌 우

for x in range(len(arr)):
    for y in range(len(arr[x])):
        for I in range(4):
            testX <- x + dx[mode]
            testY <- y + dy[mode]
            test(arr[testX][testY])
```
→ **많이 활용되는 스킬!**
```python
# 전치 행렬
# i : 행의 좌표, len(arr)
# j : 열의 좌표, len(arr[0])
arr = [[1,2,3],[4,5,6],[7,8,9]] # 3*3 행렬

for i in range(3):
    for j in range(3):
        if i < j:
            arr[i][j], arr[j][i] = arr[j][i], arr[i][j]
```

fsdf

### 부분집합 생성

> 부분집합 중, 원소 합이 0이 되거나 특정 조건을 만족하는 부분집합이 있는지 알아내는 문제

**1. 부분 집합 생성하기**

```python
# 각 원소가 부분집합에 포함되었는지 loop를 이용하여 확인하고 부분집합을 생성하는 방법 
bit = [0, 0, 0, 0]
for i in range(2):
    bit[0] = i
    for j in range(2):
        bit[1] = j
        for k in range(2):
            bit[2] = k
            for l in range(2):
                bit[3] = l
                print(bit) # 각 원소가 포함 or 비포함으로 부분집합이 생성됨
```

**2. 비트 연산자**

>  숫자를 2진수로 표현했을 때, 각 자리수를 비트라고 생각하면 편하다.

`&` : 비트 단위로 AND 연산

`|` : 비트 단위로 OR 연산

`<<` : 피연산자의 비트 열을 왼쪽으로 이동시킨다.

​	즉, 0001의 경우 1000이 되는 것이기 때문에 2^n이라는 결과가 나올 수 있다.

`>>` : 피연산자의 비트 열을 오른쪽으로 이동시킨다.

​	즉, 1000의 경우 0001이 되는 형식



`1<<n` : 2^n. 즉, 원소가 n개일 경우 모든 부분집합 수를 의미

```python
for i in range(1<<n): # n개 원소의 부분집합 개수만큼 반복!
    실행문
```

`i & (1<<j)` : i 의 j 번째 비트가 1인지 아닌지를 리턴한다.



``` python
# 비트 연산자를 활용해서 보다 간결하게 부분집합을 생성하는 방법
arr = [3, 6, 7, 1, 5, 4]
n = len(arr) # n : 원소의 개수

for i in range(1<<n): # 1<<n : 부분 집합의 개수
    for j in range(n+1): # 원소의 수만큼 비트를 비교함
        if i & (1<<j): # i의 j 번째 비트가 1이면 j 번째 원소 출력
            print(arr[j], end=", ")
    print()
print()
```



**부분집합 합 문제 구현**

> 10개의 정수를 입력 받아 부분집합의 합이 0이 되는 것이 존재하는지 계산하는 함수

```python
for i in range(1<<10): # 10개 원소의 각 부분집합에 대해서
	for j in range(11):
        
```



### 바이너리 서치 (Binary Search)

> 검색 (Search) : 저장된 자료 중, 원하는 항목을 찾는 작업
>
> 검색의 종류에는 '순차검색 (Sequential Search)' / '이진검색 (Binary Search)' / '해쉬 (Hash)' 등이 있다.
>
> 바이너리 서치
>
> : 자료의 가운데에 있는 항목의 키 값과 비교하여 다음 검색의 위치를 결정하고 검색을 계속 진행하는 방식

**검색 과정**

1) 자료 중앙에 있는 원소를 고른다.

2) 중앙 원소의 값과 찾고자 하는 목표 값을 비교한다.

3) 목표 값이 중앙 원소의 값보다 작으면 자료의 완쪽 반에 대해서 새로 검색을 수행하고, 크다면 자료의 오른쪽 반에 대해서 새로 검색을 수행한다.

4) 찾고자 하는 값을 찾을 때까지 1) ~ 3) 의 과정을 반복한다.

계속 반으로 나눠서 위치를 찾는다.

```python
def binarySearch(a, key):
    start <- 0 end <- length(a)-1
    while start <= end:
        middle = (start + end)//2
        if a[middle] == key:
            return true
        elif a[middle] > key:
            end = middle - 1
        else:
            start = middle + 1
    return false
```

```python
# 재귀 함수 이용
def binarySearch2(a, low, high, key):
    if low > high: # 검색 실패
        return False
    else:
        middle = (low + high)//2
        if key == a[middle]: # 검색 성공
            return True
        elif key < a[middle]:
            return binarySearch2(a, low, middle - 1, key)
        elif a[middle] < key:
            return binarySearch2(a, middle + 1, high, key)
```



### 셀렉션 알고리즘 (Selection Algorithm)

> 저장되어 있는 자료로부터 k 번째로 큰 혹은 작은 원소를 찾는 방법
>
> 최소값, 최대값, 중간값을 찾는 알고리즘

**선택 과정**

1) 정렬 알고리즘을 이용하여 자료 정렬하기

2) 원하는 순서에 있는 원소 가져오기





### 선택 정렬 (Selection Sort)

```python
def SelectionSort(a[], n)
    for i from 0 to n-1
        a[i], ... , a[n-1] 원소 중 최소값 a[k] 찾음
        a[i]와 a[k] 교환
```

```python
def selectionSort(a):
    for i in range(0, len(a)-1):
        min = i
        for j in range(i+1, len(a)):
            if a[min] > a[j]:
                min = j
        a[i], a[min] = a[min], a[i]
```



### 실습 1, 2

달팽이 문제!!!

