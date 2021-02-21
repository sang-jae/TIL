# Array 1

> 배열 1 (Array 1)

### 알고리즘

좋은 알고리즘 : 정확성 / 작업량(연산량) / 메모리 사용량 / 단순성 / 최적성(개선여지 X)

시간 복잡도 ≒ 빅-오(O) 표기법 : 가장 큰 영향력을 주는 n에 대한 항만을 표시

​	N = 1억 / O(N) 일 때, 실제 실행시간은 약 0.1초

​	N = 1억 / O(N^2) 일 때, 실제 실행시간은 약 115.7일



### 배열

Gravity - 2중 for 문

Baby-gin 



### 완전검색 (Exaustive Search)

> Brute-force 혹은 generate-and-test 기법이라고도 한다.

생각할 수 있는 모든 경우의 수를 테스트 한 후, 최종 해법을 도출.

경우의 수가 상대적으로 작을 때 유용



수행 속도는 느리지만, 해답을 찾아내지 못할 확률이 작다.



자격검정평가 등에서 주어진 문제를 풀 때, 완전검색으로 접근해 해답 도출 후 성능개선을 위해 다른 알고리즘을 사용하는 것이 바람직하다.



Baby-gin 풀 때 모든 순열을 생성해서 앞 3자리 뒤 3자리 잘라서 run과 triplet 여부 테스트 후 판단.



#### 순열 (Permutation , nPr)

각 자리수 별로 loop를 이용해 구현할 수 있다.

(다 중 for 문)



### 그리디 (Greedy Algorithm)

여러 경우 중 하나를 결정해야 할 때마다 그 순간에 최적이라고 생각되는 것을 선택해 나가는 방식으로 진행하여 최종적인 해답에 도달.



#### 거스름돈 줄이기



Baby-gin : counts에 갯수를 넣어서 run 조사 후, run 데이터 완전 삭제 or triplet 조사 후, triplet 데이터 완전 삭제



### 정렬

정렬의 종류

- 버블 정렬 (Bubble Sort)
- 카운팅 정렬 (Counting Sort)
- 선택 정렬 (Selection Sort)
- 퀵 정렬 (Quick Sort)
- 삽입 정렬 (Insertion Sort)
- 병합 정렬(Merge Sort)



### 버블 정렬 (Bubble Sort)

> 인접한 두 개의 원소를 비교하며 자리를 계속 교환하는 방식

`O(n^2)`

```python
def BubbleSort(a): # 정렬할 List
    for i in range(len(a)-1, 0, -1): # 범위의 끝 위치
        for j in range(0, i):
            if a[j] > a[j+1]:
                a[j], a[j+1] = a[j+1], a[j]
```



### 카운팅 정렬 (Counting Sort)

> 항목들의 순서를 결정하기 위해 집합에 각 항목이 몇 개씩 있는지 세는 작업을 하여, 선형 시간에 정렬하는 효율적인 알고리즘

`O(n+k)` : n은 리스트 길이, k는 정수의 최대값





다시 할 것.



### 실습 1, 2





