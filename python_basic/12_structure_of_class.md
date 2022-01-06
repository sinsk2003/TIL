# 클래스의 구조

- 클래스의 구조
  - 클래스의 속성: 클래스 내부에서 정의되는 변수 = 클래스 변수
  - 클래스의 기능: 클래스 내부에서 정의되는 함수 = 메소드
- 한 클래스는 클래스 변수와 메소드로 정의될 수 있음
  - 클래스 변수와 메소드는 클래스의 특징을 반영

## 객체변수

- 객체가 생성된 이후에 정의 가능
- 같은 타입이라고 해도, 객체와 객체간에는 객체변수를 서로 공유하지 않음
  - 객체 고유의 메모리에 생성되는 객체 고유의 변수

```python
class Person:
  pass

장동건 = Person() # 객체 생성

# 객체 변수 정의
장동건.name = '장동건' 
장동건.age = 20

# 객체 변수 참조
print(장동건.name) # 장동건
print(장동건.age) # 20
# 파이썬에서 `.`의 의미: 소속을 알리는 역할
```

## 클래스 변수

- 객체와는 무관하며, 객체 없이도 참조 가능한 변수
- 클래스 내부, 메소드 외부에 정의가 되면 `클래스 변수`
- 공유변수: 모든 객체가 하나의 동일한 클래스 변수를 참조

```python
class Person:
  nation = 'korea'
  
 Person.nation # 'korea'
```

- 대부분의 언어와 달리, 파이썬은 객체를 통해서 클래스 변수에 대한 참조가 가능: 문제 발생 가능
  - 클래스 변수는 클래스를 통해서만 접근하도록 하면 문제 없음

```python
장동건 = Person()

# 객체를 통해 클래스 변수 참조
print( 장동건.nation ) # korea

장동건.nation = 'German' # 객체 변수 생성
print( 장동건.nation ) # German
# 객체변수인지 클래스변수인지 헷갈리는 문제 발생
```

## 메소드(Method)

- 클래스 내에서 정의된 함수

```python
class Person:
  nation = 'Korea'

  # 메소드의 첫 번째 파라미터는 무조건 self
  def method(self):
    print('클래스 내에서 정의가 되었을 뿐 함수와 동일')
```

- 메소드는 객체를 통해서만 호출 가능

```python
장동건 = Person()
장동건.method() # 클래스 내에서 정의가 되었을 뿐 함수와 동일
```

### self

- 함수는 호출이 되면 실행 => 메모리에 생성
- 메소드는 객체가 먼저 만들어져야 메소드를 호출 => 실행 => 메모리에 생성
  - 객체가 생성되는 시점과 메소드가 호출이 되어 메모리에 만들어지는 시점이 다름
- 메소드를 호출할 때는, 어떤 객체가 호출했는지 알 수 있도록 파라미터를 통해서 객체를 전달
  - 직접 전달하지 않고, 파이썬 인터프리터에 의해서 자동으로 전달
- 메소드는 반드시 첫 번째 파라미터로 `self`를 정의해야 함
- 메소드는 self를 통해서 호출한 객체를 구분

```python
class Person:
  nation = 'Korea'

  def method(self):
    print('self is: ', self)
    
장동건 = Person()

# self에 대한 입력을 넣어준적이 없지만, 파이썬 인터프리터에 의해서 자동 전달
장동건.method() # self는 직접 전달하지 않음
# self is:  <__main__.Person object at 0x7f390b9f9750>
print( 장동건 ) # <__main__.Person object at 0x7f390b9f9750>
```

- 객체.attribute와 self.attribute는 같은 표현
- self를 제외한 나머지 파라미터는 입력값을 전달

```python
class Person:
  nation = 'Korea'

  def method(self, a, b):
    return a + b
    
장동건 = Person()

# self를 제외한 나머지 입력값만 전달
장동건.method(10, 20) # 30
```

### 매직 메소드

- 특별한 의미를 가지고 있는 미리 정의된 메소드들
- 메소드 이름 앞과 뒤에 `__`(더블언더바, 더블언더스코어, 던더)가 붙어 있는 메소드(던더 메소드)
- 매직 메소드마다 호출 방식이 다름

```python
class Person:
  pass

# 매직 메소드들 확인
dir(Person) # ['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__']
```

#### 생성자

- `__init__`: 객체가 생성될 때, 인터프리터에 의해서 자동으로 호출되는 메소드

```python
class Person:

  def __init__(self):
    print('call __init__')
    
장동건 = Person() # call __init__
```

- 생성자를 통한 객체변수의 초기화: 모든 객체가 동일한 속성을 가지게 할 수 있음

```python
class Person:
  def __init__(self):
    self.age = 0
    
장동건 = Person()
print( 장동건.age ) # 0
```

```python
class Person:
  # 객체가 생성될 때, 생성자를 자동으로 호출하며,
  # 생성자를 호출할 때, 입력값을 전달받도록 하면
  # 전달받은 값으로, 객체변수 초기화 가능
  def __init__(self, name, age):
    # self.객체변수 = 지역변수
    self.name = name
    self.age = age
```

```python
장동건 = Person() 
# TypeError: __init__() missing 2 required positional arguments: 'name' and 'age'
# 생성자 때문에 객체 생성할 때 ()가 있음
```

```python
장동건 = Person('장동건', 20)
print( 장동건.name ) # 장동건
print( 장동건.age ) # 20
```

#### 연산자

- 연산자 오버로딩: 매직 메소드를 이용해서 연산자에 대한 다양한 형태(다형성)를 제공

```python
# 시퀀스 타입에서 덧셈과 곱셈이 가능한 이유
# 리스트 클래스 내에서 __add__, __mull__ 이 두 매직 메소드를 새로 정의
[1, 2, 3] + [4, 5, 6] # [1, 2, 3, 4, 5, 6]
```

```python
class Person:

  def __init__(self, name, age):
    self.name = name
    self.age = age
  
  # 호출 방식은 같지만, 결과는 다름
  def __add__(self, obj):
    print('덧셈처럼 보이지만, 메소드 호출')
    return (self.name + obj.name, self.age + obj.age)

장동건 = Person('장동건', 20)
원빈 = Person('원빈', 22)

print( 장동건 + 원빈 )
# 덧셈처럼 보이지만, 메소드 호출
# ('장동건원빈', 42)
```

#### 함수

- 파이썬에서는 함수도 객체
  - function 클래스로 만들어진 객체
  - function 클래스의 객체는 `()`를 붙여서 호출
  - 매직 메소드의 하나

```python
class UserFunction:

  # 기본적으로는 __call__ 매직 메소드가 구현된 클래스의 객체가 함수가 됨
  def __call__(self):
    print('함수가 호출 되었음')
    
function = UserFunction()
function() # 함수가 호출 되었음
```

#### 파이썬의 매직 메소드들

- 더 다양한 형태의 매직 메소드들: [데이터 모델](https://docs.python.org/ko/3.7/reference/datamodel.html#special-method-names)

### Static Method Vs. Class Method

- 객체와 상관없이 클래스를 통해서 호출 가능한 메소드(클래스 변수의 메소드 버젼)
- 메소드는 객체를 통해서만 호출이 가능하다고 하면, 메소드를 통해서 클래스 변수를 참조 하려고 할 때, 반드시 객체가 필요한 이상한 상황이 발생

```python
class Person:
  nation = 'Korea'
  
  # static method
  # 데코레이터를 통해서 메소드를 정의
  # 스태틱 메소드로 정의하고 싶은 메소드 앞에 데코레이터를 붙여주면 됨 
  # 스태틱 메소드는 self 파라미터를 정의하지 않습니다.(객체와 상관없으므로)

  @staticmethod # 데코레이터
  def staticMethod():
    return Person.nation

  def __init__(self, name, age):
    self.name = name
    self.age = age
    
Person.staticMethod() # 'Korea'
```

```python
class Person:
  nation = 'Korea'

  # class method 역시 데코레이터를 통해서 정의
  # 첫 번째 파라미터로 'cls'를 정의해야 함
  # 객체를 구분하는 self와 동일한 역할을 하는 cls가 존재
  # 클래스 메소드는 cls라는 파라미터를 통해서 클래스를 구분

  @classmethod # 데코레이터
  def classMethod(cls):
    return cls.nation

  def __init__(self, name, age):
    self.name = name
    self.age = age
    
Person.classMethod() # 'Korea'
```

