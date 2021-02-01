# Data_Container
> 여러개의 값을 저장할 수 있는 객체. Sequence 형 (순서(ordered)가 있음. list, tuple 등). Non_sequence 형 (순서가 없음.(unordered). set, dict)

### Sequence 형
#### list

#### tuple
list와 달리 수정 불가능 (불변, immutable)
```
my_list = [1, 3]
my_list[0] = '첫번째'
print(my_list)           # ['첫번째', 3]

my_tuple = (1, 3)
my_tuple[0] = '첫번째'    # error point
print(my_tuple)          # TypeError : 'tuple' object does not support item assignment
```

하나의 항목으로 구성된 튜플은 값 뒤에 심표를 붙여서 만든다.
```
tuple1 = ('hello')
type(tuple1)             # str
tuple2 = ('hello', )
type(tuple2)             # tuple
```



#### range()
range(n) : 0 ~ n-1
range(n, m) : n ~ m-1
range(n, m, s) : n ~ m-1 까지 +s 만큼 증가한다. `list(range(0, -10, -1))` = `[0, -1, -2, ..., -9]`

range 자체는 list는 아니기 때문에 list처럼 사용하려면 `list(range())`를 해주어야 한다.
```
range(3)        # range(0, 3) 출력
list(range(3))  # [0, 1, 2]
```

#### Sequence 형 에서 활용 가능한 연산자 / 함수
`x in s`
`x not in s`
`s1 + s2`
`s * n` : s를 n번만큼 반복하여 더하기
`s[i]` : indexing, `s[i:j]` : slicing, `s[i:j:k]` : k 간격으로 slicing
`len(s)` , `min(s)` , `max(s)` , `s.count(x)` : x의 개수

### Non_Sequence 형
> set . dictionary
#### set
> 순서 없고, 중복된 값이 없다.
`list(set(list))`를 이용해서 리스트의 중복된 값을 제거할 수 있다.

#### dictionary
> key와 value로 이루어져 있다.
key에는 immutable 데이터만 가능 (string, integer, float, boolean, tuple, range)
value에는 list, dictionary를 포함한 모든 것이 가능.

index가 아니라 key로 접근

```
phone = {'서울': '02', '경기': '031'}
phone                           # {'서울': '02', '경기': '031'}
phone['서울']                   # '02'
phone.keys()                    # dict_keys(['서울', '경기'])
phone.values()                  # dict_values(['02', '031'])
phone.items()                   # dict_items([('서울', '02'),('경기', '031')])
```

range는 dict의 key 값으로도 들어갈 수 없다?! 되는디...?

### Mutable vs Immutable
#### Immutable
Number, String, Bool, range(), tuple()

#### Mutable
list, dict, set