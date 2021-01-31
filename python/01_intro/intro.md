# Python_Intro
> 파이썬을 이용하는데 필요한 기초 문법과 변수, 데이터 타입, 연산자 등에 대해서 알아보았다.

### 기초문법
#### 주석 (Comment)
- `#` 한줄의 주석
- `'''` 여러줄의 주석

#### 코드라인
- 1줄에 1문장(statement) 원칙
- 문장 (statement) : 파이썬이 실행가능한 최소한의 코드 단위

ex1) 원칙을 따르지 않아 `SyntaxError : invalid syntax`가 나오는 예시
```
print('hello')print('world')
```
ex1) 오류를 해결하는 방법 (; 이용)
```
print('hello');print('world')
```
ex2) 원칙을 따르지 않아 `SyntaxError : EOL while scanning string literal`가 나오는 예시
```
print('hello
world')
```
ex2) 오류를 해결하는 방법 (\ 이용)
```
print('hello\
world')
```
ex2) 여러줄 문자열을 쓰는 관례
```
print("""hello
world""")
```

### 변수
#### 할당 연산자(Assignment Operator) (=)

#### 식별자(Identifiers) (이름(name))
- 첫글자 숫자 X
- 길이 제한 X
- 대소문자 구별
- 키워드 사용 불가 (`import keyword`)
- 내장함수나 모듈의 이름도 불가
ex)
```
print = 'hi' # print라고 하는 내장함수 이름과 겹침
print(5) # 내장함수가 식별자로 인해 이전의 기능을 수행하지 못하고 에러가 남
del print # 내장함수를 쓰기 위해서는 방금 생성한 식별자 print를 삭제
print('hi') # 정상적으로 동작
```
### 데이터 타입 (Data Type)
#### 숫자(Number)
정수형(int), 실수(float), 복소수 (complex)
이 중, 실수형(float)의 부동소수점에 대해서 알아야 한다.

실수를 컴퓨터가 표현하는 과정에서 부동소수점을 사용하는데, 컴퓨터가 2진수(비트)를 통해 숫자를 표현하는 과정에서 오류가 생겨 항상 같은 값으로 일치되지는 않는다. (값이 같은지 비교하는 과정에서 문제 발생할 수 있음)

```
3.5 - 3.12 # 답은 0.38인데 0.3799999로 나옴
round(3.5 - 3.12, 2) # 반올림하는 것

3.5 - 3.12 == 0.38 # False

a = 3.5 - 3.12
b = 0.38
abs(a - b) <= 1e-10 # True

import sys #sys 모듈에서 epsilon은 부동소수점 연산에서 반올림을 함으로 발생하는 오차를 상환함
abs(a-b) <= sys.float_info.epsilon # True

import math
math.isclose(a, b) #math 모듈 통해 처리
```

복소수(complex)에서 주의할 점은
문자열을 복소수로 변환할 때 연산자 주위에 공백을 포함하면 안된다.
```
complex('1 + 2j') # 에러 나옴
complex('1+2j') # (1+2j)로 정상 출력
```

#### 글자(String)
input()은 기본적으로 str이다.
문자열 안에 같은 문장부호를 사용하면 오류 `print('말했다. '안녕'')`
문자열 안에 서로다른 문장부호로 오류 수정 `print('말했다. "안녕"')` or `print('말했다. \'안녕\'')`

**이스케이프 시퀀스**
\n : 줄바꿈
\t : 탭
\r : 캐리지리턴
\0 : Null
\\ : \
\' : '
\" : "

**String interpolation**
f-string `print(f'hello, {name}.')`

#### 참/거짓(Boolean)
False로 변환되는 값들
0, 0.0, (), [], {}, '', None

#### 형변환
암시적 형변환 / 명시적 형변환
```
# 암시적 형변환 (숫자끼리 더하거나 연산할 때, 자동으로 형변환)
True + 5                               # 6
int_number = 3                         # int 형
float_number = 5.0                     # float 형
complex_num = 3+5j                     # complex 형
result1 = int_number + float_number    # result1 = 8.0 (float 형)
result2 = int_number + complex_num     # result2 = 6+5j (complex 형)
```
```
# 명시적 형변환 (위의 상황을 제외하고는 모두 명시적으로 변환 해줘야 함)
int()           # string, float를 int로 변환
float()         # string, int를 float로 변환
str()           # int, float, list, tuple, dictionary 를 문자열로 변환
a = '3.5'       # str(문자열) 3.5
int(a)          # error
a = 3.5         # float(실수) 3.5
int(a)          # 3 : 내림??
```

### 연산자 (Operator)
// : 몫
% : 나머지
** : 거듭제곱
숫자 앞에 - 붙여서 음수 양수 표현 `negative_num = -4; print(-negative_num) # 4`

논리 연산자 (and, or, not)
and : 모두 True 시, True
or : 모두 False 시, False
not a : True 는 False로 False는 True로

vowels : 모음 (aeiou)

**단축평가**
and의 경우에 모두 true여야 하니까, 앞이 false가 아니면 뒤까지 보고 뒤 값을 반환
or의 경우 하나만 true여도 되니까 바로 처음 true를 반환
```
print(3 and 5) # 5
print(3 and 0) # 0
print(0 and 3) # 3
```

**`is`Identity**
-5 ~ 256 까지 숫자의 id(객체의 주소)는 동일. 그 이후는 다르다.
값은 같지만, 객체는 다를 수 있다.
공백없는 알파벳 문자열은 같은 객체로 인식하도록 되어있다.
! 같은 기호가 있으면 달라진다.

**연산자 우선순위**
()을 통한 grouping
Slicing
Indexing
제곱연산자 **
단항연산자 +, - (음수/양수 부호)
산술연산자 *, /, %
산술연산자 +, -
비교연산자, in, is
not
and
or

() s i ^ +_(부호) */% +_ in,is not and or
괄호 슬라이싱 인덱싱 제곱 부호 곱 합 비교 not and or

괄 슬 인 제 부 곱 합 비 not and or

