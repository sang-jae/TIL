# Python 조건문과 반복문 추가 내용

1. 조건 표현식 (18일 라이브 내용에서 추가로 공부할 것)

   다른 이름으로 **삼항 연산자** (Ternary Operator)

   `true_value if <조건식> else false_value`

   원래는 4줄 5줄로 들어갈 코드를 1줄로 표현.

   하지만 가독성이 조금 떨어지기 때문에 지양하는 편.

   다른 사람이 볼 때 한눈에 알아보기 힘듬.

   배우는 이유는 다른 사람의 코드를 봤을 때 읽을 수는 있어야 함.

   특히 알고리즘 공부를 할 때, 다른 사람들의 코드를 계속 보게 될 텐데, 숏코딩 변태들이 있다. 읽기 위함.

2. while 문 (조건이 부합하는 동안 코드를 실행해)

   while true : 무한루프에 빠진다. 컴퓨터가 뻗을 때까지

   2.1.4 실습 합 : 자꾸 에러가 났다. 뭐가 문제였는가?

   ​	`TypeError: 'int' object is not callable`

   ​	내가 int라는 함수를 변수 이름으로 사용하게 되면서, int에서 함수가 사라지고 변수가 됨.

   ​	그래서 이후 int를 호출해도 함수로 인식하지 못해서 생겨난 오류.

3. for 문

   **enumerate()** : list 데이터의 인덱스와, value 값을 tuple 형식으로 같이 출력해줌.

   ```python
   lunch = ['짜장면', '초밥', '피자', '햄버거']
   for l in enumerate(lunch):
   	print(l)
   ```

   ```
   (0, '짜장면')
   (1, '초밥')
   (2, '피자')
   (3, '햄버거')
   ```

   ```python
   lunch = ['짜장면', '초밥', '피자', '햄버거']
   for index, menu in enumerate(lunch):
   	print(index)
   	print(menu)
   ```

   ```
   0
   짜장면
   1
   초밥
   2
   피자
   3
   햄버거
   ```

   ```python
   # 숫자를 1부터 카운트 하려면
   for index, menu in enumerate(lunch, start = 1):
       print(index)
       print(menu)
   ```

   ```
   1
   짜장면
   2
   초밥
   3
   피자
   4
   햄버거
   ```

   **else** : 반복문이 종료되고 실행. 마지막까지 돌았는지 체크하기 위해서 실행.

   ```python
   numbers = [1, 3, 7, 9]
   
   for number in numbers:
       if number == 4:
           print(True)
           break
   else:
       print(False)
   ```

   ```
   False
   ```

   **pass** : 문장이 필요하지만, 프로그램이 특별히 할 일이 없을 때 자리를 채우는 용도로.

   ```python
   if True:
   ```

   `error`

   ```python
   if True:
   	pass
   ```

   `실행가능`

   **continue와 pass의 차이** : continue는 넘어가는 것. pass는 할 일이 없을 때 오류가 나지 않게 자리 채우기.