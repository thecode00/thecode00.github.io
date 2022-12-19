---
title: "파이썬 팁"

toc: true
toc_sticky: true
date: 2022-12-20
last_modified_at: 2022-12-20
---

파이썬은 모든것이 객체
크게 두가지 객체가 있는데 불변객체(Immutable Object) 가변객체(Mutable Object)가 있다

불변객체는 바꿀수없는 객체이므로 dict의 key로 사용할수있다

가변객체는 대표적으로 list가 있는데 변수에 할당된후에도 값이 변할수있다
'''python
a = [1, 2, 3]
b = a

a[1] = 1 # 여기서 b의 값도 바뀌게 된다
print(a) # [1, 1, 3]
print(b) # [1, 1, 3]
'''

is와 ==의 차이
is는 id값을 비교하고 ==는 값을 비교한다.
'''python
a = [1, 2, 3]
b = a

print(a == b) # True
print(a is b) # True

b = [1, 2, 3]

print(a == b) # True
print(a is b) # False
'''
