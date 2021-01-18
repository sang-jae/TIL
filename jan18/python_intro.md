# Python_intro

알고 있던 내용들은 제외하고 새롭게 배웠거나, 잊어버렸던 개념들 위주로 정리!



### 주석

`#`  : 한줄 주석

`'''` : 여러줄 주석 (위 아래로 표시)

### 코드라인

1줄에 1문장 원칙

### 식별자 (Identifiers)

```python
import keyword
print(keyword.kwlist)
```

### 부동소수점

실수를 컴퓨터가 표현하는 과정에서 항상 같은 값으로 일치되지 않는다.

2진수를 통해 숫자를 표현하는 과정에서 생기는 오류.

값을 비교할 때 문제가 발생할 수 있다.

```python
import math
math.isclose(a,b)
```

### 이스케이프 시퀀스

`\n` : 줄 바꿈

`\t` : 탭

`\\` : \ (백슬래시)

`\'` : '

`\"` : "

### string interpolation

2가지를 기억할 것. 수업에서는 f-string을 사용하는데, 알고리즘의 경우, str.format()을 사용해야 할 것. (파이썬 버전의 차이인 듯)

- `str.format()`

  ```python
  name = 'Kim'
  score = 4.5
  print('Hello, {}. 내 성적은 {}'.format(name, score))
  ```

- `f-string`

  ```python
  name = 'Kim'
  score = 4.5
  print(f'Hello, {name}. 내 성적은 {score}')
  ```

### 형변환 (Type conversion)

- 암시적 형변환 : 파이썬이 내부적으로 자동으로 변환
  - bool
  - Numbers (int , float , complex) : int와 float을 더하는 식을 작성하면 자동으로 float으로 변경
- 명시적 형변환 : 직접 변환
  - string → integer : 형식에 맞는 숫자만
  - integer → string : 모두 가능
  - int() : string, float 를 int 로
  - float() : string, int 를 float 로
  - str() : int, float, list, tuple, dictionary를 문자열로

### 연산자

헷갈리는 건. `//` : 몫 , `%` : 나머지 , `**` : 거듭제곱

### 단축평가

첫번째 값이 확실할 때, 두번째 값은 확인하지 않음

