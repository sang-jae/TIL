# Jan28

> OOP3 - 상속
>
> practice / homework / workshop

### 요약

OOP 마지막 순서인 상속에 대해서 배우고, 객체지향 프로그래밍에 대한 지식을 실습을 통해서 익힘.

### 느낌

완벽하게 다룰 순 없지만, 명세서가 주어진다면 클래스를 어느 정도 선까지는 짜볼 수 있을 것 같다는 생각이 들었다. 또한, 클래스와 메서드를 생성하면서 개념 정립이 어렵지, 실제 작동하는 로직은 지금까지 했던 것과 크게 다를 바가 없다는 것을 느꼈던 것 같다.

practice와 homework 그리고 workshop 실습을 통해서 조금 더 OOP에 대해서 이해도가 높아졌다는 생각이 들었다.

내일 있을 PJT와 주말 공부를 통해서 조금 더 익숙해졌으면 좋겠다.

### 공부내용

> 공부하면서 중간중간 기록한 내용.

grouping!

```python
class ChildClass(ParentClass):
	<code block>
```

부모의 기능을 그대로 내려받아서 새로운 클래스가 만들어진다.

```python
class Person:
    population = 0
    
    def __init__(self, name='사람'):
        self.name = name
        Person.population += 1
        
    def talk(self):
        print(f'반갑습니다. {self.name}입니다.')
# 부모 클래스

class Student(Person):
    def __init__(self, name, student_id):
        self.name = name
        self.student_id = student_id
# 그대로 상속받아, student_id는 자식 클래스에서만 사용되는 메서드
```



상속 자체는 안어려운데 `super()`에서 좀 어려웠을 것. 그대로 가져온다??





메소드 생성할 때 (self)를 안넣으면

```python
area() takes 0 positional arguments but 1 was given
```

라고 에러가 뜨더라.



