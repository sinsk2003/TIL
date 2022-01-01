# 매핑형 타입

- **딕셔너리**: 해시 자료구조
- 형태: { key:value, key:value, ... }


- key를 직접 정의 가능

- key, value 모두 숫자, 문자열 가능

- 인덱스가 자동으로 생성되지 않음

  - key를 통해 참조

  ```python
  hash = {'first': 10, 'second': 20}
  hash['first'] 	# 10
  ```

- key가 존재하면 값을 업데이트, 존재하지 않으면 추가

- 원소 추가 명령어 없음

- key 수정 불가능, value 수정 가능

- key 삭제: del

```python
del hash['first']
hash 	# {'second': 20}
```

- key 및 value 확인

```python
hash = {'first': 10, 'second': 20}
print( hash.keys() )	# dict_keys(['second', 'first'])
print( hash.values() )	# dict_values([20, 10])
print( hash.items() )	# dict_items([('second', 20), ('first', 10)])
# 위 세 자료형은 참조 및 할당 불가능
# 리스트 및 튜플로 변환하면 가능
```

