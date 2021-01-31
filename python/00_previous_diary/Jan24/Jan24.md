# Jan 24

### 요약

Jan25 월말평가 대비, 예시 문제 풀이



### 느낀점

예시 처럼 문제가 나온다면 쉽게 풀어낼 수 있을 것으로 보임.

하지만 실수를 하면 안된다. 실수해서 변수에 내장함수를 선언해버리면 내장함수 못쓰고 초기화 하는 동안 시간을 다 사용해버리는 문제가 발생할 수 있을 것 같다.



### 내용

#### 월말평가 대비

- **전체 폴더를 압축**하고, **서울1반_김상재** 로 이름을 변경하여 제출할 것!

- **월말평가 예시**

  list 와 dict 자료를 다루는 방법을 알아야 한다.

  list에 데이터 추가 - `list.append()`

  dict에 데이터 추가 - `dict['key'] = value`

  dict내 원하는 key의 value 값을 뽑아내는 방법 - `value = dict.get('key')`

  - dict의 key를 

  dict내 원하는 value의 key를 뽑아내는 방법 - ???

  반복문으로 dict의 자료를 뽑아내는 방법 `dict.items()`

  ```python
  # 예시
  list = {'george':16, 'amber':19}
  search_age = raw_input('이름을 입력해주세요')
  for name, age in dict.items():
  	if age == search_age:
  		print name
  ```

- 그 외 주의 사항

  `list` `max`등 내장함수를 변수로 사용하지 말 것.