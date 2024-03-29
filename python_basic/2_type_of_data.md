# 자료의 타입

- 자료: 프로그래밍 대상
- 자료의 형태: 문자 or 숫자
  - 정확하게는 숫자 하나
  - 컴퓨터에서 보여지는 모든 것들은 전부 숫자로 표현 가능
- 기본 타입: 숫자(자료를 구성하는 가장 기본적인 `최소 단위`)

## 숫자

- 정수, 실수, 불리언
  - 분수, 복소수도 표현 가능
  - 파이썬의 실수는 정확하게는 소수(decimal number)에 대한 표현

### 정수(int)

- 음수, 0, 양수를 표현
- 크기: 크기 제한 없음. 4bytes

### 실수(float)

- 부동소수점 방식: 움직이는 소수점 방식

### 불리언(bool)

- True = 1, False = 0

## 문자열

- 파이썬은 단일 문자라는 개념이 없고, 그냥 다 문자열
- 표현 방법: ' / ", ''' / """ (멀티라인 문자열)
  - '와 ''의 차이는 없음
  - 다만, Opening Quotations와 Closing Quatations는 반드시 한 쌍


- print는 기본적으로 `문자열` 출력임을 가정
- display는 출력된 결과의 타입도 함께 표현
- 다음 라인으로 넘어가는 경우, \를 붙여 줌

```python
'Hello \
Python'		# 'Hello Python'

'''Hello
Python'''	# 'Hello\nPython'
```

- 한 줄에 여러 개의 명령어를 사용하고 싶은 경우, ;를 붙여 줌

```python
print('Hello') ; print('Python')
# Hello
# Python
```

### 문자열을 처리하는 방법

- 기본적으로 컴퓨터는 숫자만 처리 가능

  - 정확하게는 이진수로만 처리 가능
  - 덧셈만 가능
    - 뺄셈 불가능(2의 보수를 통한 뺄셈을 구현)

- 아스키 코드: 0부터 127까지 총 128개의 문자에 대해서 대응되는 숫자 테이블

  ![img](https://3.bp.blogspot.com/-aw0f_TovMoU/WNxD0O5hTjI/AAAAAAAAQGU/33SBPQ-jLo4pMk0jv42YsjinfBlG4JbdgCLcB/s640/%25EC%2595%2584%25EC%258A%25A4%25ED%2582%25A4%25EC%25BD%2594%25EB%2593%259C%25ED%2591%259C_01.jpg)![img](https://1.bp.blogspot.com/-NINVWqe17ug/WNxD0PQ-vnI/AAAAAAAAQGQ/13iKgvNkaocCGwqlV9BLbZf06oOVYIsWwCLcB/s640/%25EC%2595%2584%25EC%258A%25A4%25ED%2582%25A4%25EC%25BD%2594%25EB%2593%259C%25ED%2591%259C_02.jpg)
  - 모든 시스템이 동일한 값을 사용
  - 1바이트가 8비트인 이유: MSB(Most Signature Bit/최상위부호비트)를 제외한 7개의 비트로 표현을 하면 2^7=128개 만큼 표현이 가능하고, 이는 문자 체계를 모두 표현하는 데 충분

- 문자 표현 최소 크기: 2바이트(아시아권 국가들의 문자 표현을 위해 )

- 한글의 숫자 표현 방법

  - 아스키 테이블 사용 불가
  - 한글을 표현할 수 있는 새로운 문자 인코딩 셋: UTF-8, CP949, EUC-KR
    - 파이썬은 기본 UTF-8을 기본 인코딩 셋으로 사용
    - 한글 윈도우즈 같은 경우 기본 EUC-KR을 사용
    - 문자 => 숫자(인코딩), 숫자 => 문자(디코딩)

#### 눈에 보이지 않는 문자

- 엔터는 두 개의 문자로 표현
  - CR(Carriage Return/해당 라인의 가장 앞으로 이동)
  - LF(Line Feed/종이를 말아 올리는 작업)
    - 타자기에서 사용하던 용어를 그대로 엔터의 값으로 사용
    - 그런데 요즘은 `LF` 하나로만 표현하는게 추세
    - 에디터의 설정이나 운영체제에 따라서 달라짐
    - 윈도우즈는 CR/LF의 두 문자를 모두 사용하는 것이 일반적
    - 맥/리눅스는 LF 한 문자로 표현
- 빈 문자와 공백도 문자이며, 엄연히 다른 문자
  - 빈 문자의 표현: ''

#### 아스키 코드 값과 문자

- 다른 문자처럼 보여도 같은 아스키 코드 값을 가지면 같은 문자
  - 역슬래시와 원화 문자는 다르게 보이지만 같은 아스키 코드값을 가지므로 같은 문자
- 같은 문자처럼 보여도 인코딩 셋이 다르면 다른 문자
- 문자도 대소 비교 가능: 아스키 코드 값으로 비교

#### 아스키 코드 값과 숫자

- 숫자는 대/소 구분하지 않음

```python
print( 10 == 0x0a ) # True
print( 0x0a == 0x0A ) # True
```

- 파이썬 문자열에서는 문자열 내 숫자를 입력할 수 있음
  - 16진수 이용

```python
'\x68 \x65 \x6c \x6c \x6f' # 'h e l l o '
```

### 문자열 이스케이프

- 용도가 이미 정해진 문자를 출력하고자 할 때, 충돌 발생 -> 문자열 이스케이프(역슬래시)  
  - 따옴표 출력 방법: 
    1. 출력하려는 따옴표와 문자열을 표현하는 따옴표를 다르게 사용
    2. 탈출하고자 하는 문자 앞에 \를 붙임
  - 역슬래시 출력

```python
# C:\Users\student\Videos\Captures
print('C:\\Users\\student\\Videos\\Captures')
```

- 문자열 내 표현하기 힘든 문자들(엔터, 탭, 백스페이스 등) 입력

```python
# 엔터를 문자열에서 표현
# \n은 뉴라인(LF)
print("다음 라인에 출력하고 싶은데 \n 어? 되네?")
print("다음 라인에 출력하고 싶은데 \x0a 어? 되네?")
'''
다음 라인에 출력하고 싶은데 
 어? 되네?
다음 라인에 출력하고 싶은데 
 어? 되네?
 '''
# 파이썬 인터프리터는 이스케이프 문자를 해석하지 않음
# 그래서 display를 이용하면 입력된 문자 그대로 출력
# display는 인터프리터의 실행 결과를 유지하는 목적
display("다음 라인에 출력하고 싶은데 \x0a 어? 되네?")
'''
다음 라인에 출력하고 싶은데 \n 어? 되네?
'''
```

```python
print("잘 쓰지는 않지만 백스페이스\b")
print("잘 쓰지는 않지만 백스페이스\x08")
'''
잘 쓰지는 않지만 백스페이
잘 쓰지는 않지만 백스페이
'''
```

```python
print('탭은 \t 많이 사용하죠?')
print('탭은 \x09 많이 사용하죠?')
'''
탭은 	 많이 사용하죠?
탭은 	 많이 사용하죠?
'''
```

