---
title: "[Python]파이썬 자료형 종류"
excerpt: "파이썬의 자료형을 정리해보자"

categories: python

toc: true
toc_sticky: true
date: 2022-12-20
last_modified_at: 2022-12-20
---

파이썬의 대표적인 자료형에는 int, str, float, bool, set, list, dict등등이 있는데
그중에 기초가되는 기본적인 자료형들을 정리해보겠습니다.

```python
print(type(3.14)) # float
print(type("ABC")) # str
```

## int

1, 4, -10같은 정수들을 나타냅니다  
3.14같은 실수들을 int()함수를 이용하면 정수로 만들수있습니다.

```python
PI = 3.14
print(int(PI)) # 3
print(type(int(PI))) # int
```

실수를 정수로 타입변환을할때 실수부분을 반올림하지않고 버리기때문에 주의해야합니다.

```python
Temp_float = 3.8
print(int(Temp_float)) # 3
```

## float

3.14, -8.0, 4.77과 같은 실수들을 나타냅니다  
3같은 정수뒤에 .을 찍어주면 정수도 float타입으로 바꿀수 있습니다.

```python
print(type(3.0)) # float
print(type(3.14)) # float
```

## str

문자를 나타내는 타입입니다 큰 따옴표나 작은 따옴표로 값을 감싸 사용합니다.  
불변객체라 값을 바꿀수없습니다.

```python
# 작은 따옴표, 큰 따옴표 둘중 아무거나 써도 상관이없습니다.
print(type("hello"))    # str
print(type('hello'))    # str

s = "string"
s[0] = "a"  # Error! str은 불변객체라 list같이 값을 바꿀수 없습니다.

# 문자열 합쳐 새로운 문자열을 생성하는것도 가능합니다.
a = "str"
b = "ing"
print(a + b)    # string
```

## bool

참과 거짓을 나타내는 타입입니다.  
조건문을 사용할때 쓰는 데이터 타입입니다.  
True와 False중 한개의 값을 가지고있으며 True는 1, False는 0으로 쓸수도 있습니다.

```python
condition = True    # False를 할당할시 else문에있는 코드가 실행됨
if condition:   # 조건문은 조건이 True일때 실행됩니다 만약 조건이 False인경우 else문을 실행합니다.
    print("True")
else:
    print("False")

print(False == 0)   # True
print(True == 1)    # True
print(True == 2)    # False

print(10 > 5)   # True
print(10 == 10) # True
print(10 < 5)   # False
```

##
