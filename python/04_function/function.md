# Function
> 함수

기본 인자 값을 가지는 인자 다음에 기본 값이 없는 인자를 사용할 수 없음

```
# SyntaxError: non-default argument follows default argument
# 기본 인자 뒤에 기본이 아닌 인자가 따라왔어...
def greeting(name='익명', age):
    print(f'안녕? 난{name}, {age}살이야')

# age를 두번째에 놓고 싶은데..
# 놓을 수가 없네..
# greeting(100)
```

함수 호출 시, 키워드 인자를 활용한 다음에 위치 인자를 활용할 수 없다.
```
# SyntaxError: positional argument follows keyword argument
# 위치인자가 키워드 인자 뒤에 옴...
greeting(age=3000, '곰')
```
**LEGB Rule**
정의된 함수 - 상위 함수 - 함수 밖의 변수 or import 모듈 - 내장 함수 or 속성

**변수의 수명주기**
built in scope : 파이썬 이 실행된 후 영훤히
global scope : 