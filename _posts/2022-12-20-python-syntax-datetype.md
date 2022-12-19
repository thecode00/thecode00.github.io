---
title: "파이썬 자료형 종류"

toc: true
toc_sticky: true
date: 2022-12-20
last_modified_at: 2022-12-20
---

파이썬의 대표적인 자료형에는 int, str, float, bool, set, list, dict등등이 있는데
그중에 기초가되는 기본적인 자료형들을 정리해보겠습니다.

'''python
print(type(3.14)) # float
print(type("ABC")) # str
'''

## int

1, 4, -10같은 정수들을 나타냅니다
3.14같은 실수들을 int()함수를 이용하면 정수로 만들수있습니다.
'''python
PI = 3.14
print(int(PI)) # 3
print(type(int(PI))) # int
'''
실수를 정수로 타입변환을할때 실수부분을 반올림하지않고 버리기때문에 주의해야합니다.
'''python
Temp_float = 3.8
print(int(Temp_float)) # 3
'''

## float

3.14, -8.0, 4.77과 같은 실수들을 나타냅니다
3같은 정수뒤에 .을 찍어주면 정수도 float타입으로 바꿀수 있습니다.
'''python
print(type(3.0)) # float
print(type(3.14)) # float
'''
