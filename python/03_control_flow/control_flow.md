# Control_Flow

**continue 와 pass 의 차이**
> continue 는 바로 다음 순번의 loop로 가고, pass는 다음 작업이 수행 된다.

```
# pass
for i in [1,2,3]:
    if i:
        print(i)
        pass
    print('df')

# continue
for i in [4,5,6]:
    if i:
        print(i)
        continue
    print('df')
```
```
1
df
2
df
3
df
4
5
6s
```