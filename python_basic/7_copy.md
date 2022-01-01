# 복사

## 메모리 복사

- 동일한 주소를 나타내는 경우 같은 변수

```python
arr = [10, 20, 30]
other = arr # 메모리 복사
print(other) # [10, 20, 30] 
print( hex( id(arr))) 	# 0x7f78851855a0
print( hex( id(other))) # 0x7f78851855a0
```

## 주소(값) 복사

- 주소가 다르므로 다른 변수
- 리스트만 적용

### 얕은 복사

- copy()와 전체 슬라이스는 동일한 연산
- 리스트 자체의 주소는 다른 주소를 참조하지만, 리스트 내 리스트의 주소는 같은 주소 참조

```python
arr = [[1,2,3],[4,5,6]]

other = arr.copy() 			# 얕은 복사
print( hex(id(arr))) 		# 0x7f788507a7d0
print( hex(id(other)))		# 0x7f7885115aa0

other = arr[:] 				# 얕은 복사
print( hex(id(arr)))		# 0x7f788507a7d0
print( hex(id(other)))		# 0x7f78851eac30

# 리스트 내 리스트는 복사가 되지 않았음
print( hex(id(arr[0])))		# 0x7f78850bd460
print( hex(id(other[0])))	# 0x7f78850bd460
```

### 깊은 복사

- 리스트 자체의 주소는 물론, 리스트 내 리스트의 주소도 다른 주소 참조

```python
from copy import deepcopy

arr = [[1,2,3],[4,5,6]]
other = deepcopy(arr)		# 깊은 복사

print( hex(id(arr)))		# 0x7f7885107230
print( hex(id(other)))		# 0x7f78850ee5f0

# 리스트 내 리스트도 복사됨
print( hex(id(arr[0])))		# 0x7f788507a4b0
print( hex(id(other[0])))	# 0x7f78850e9af0
```



