---
title: "프로그래밍 용어 정리"
excerpt: "프로그래밍을 할때 쓰이는 용어들을 정리"

categories:
toc: true
toc_sticky: true
date: 2023-03-18
last_modified_at: 2023-03-18
---

### 용어 정리

프로그래밍을 할때 쓰는 용어들을 가끔씩 잊을때가 있어서 나중에 찾아볼수있게 정리해놓은 곳

사이드 이펙트(Side Effect): 함수가 리턴값외의 함수 외부의 상태를 변경해서 의도치않은 결과를 내는것을 함수의 부작용 또는 사이드 이펙트라고 함

순수 함수(Pure Function): 수학의 함수처럼 부작용이 없는 함수, 함수에 동일한 인자를 넣었을때 항상 같은 값만 리턴하는 함수 외부상태에 관여하지 않아야함

```python
def add(a: int, b: int):    # add함수는 a와 b의 값이 같다면 항상 같은 값을 반환하므로 순수함수
    return a + b

c = 0
"""
add2함수는 외부의 c값을 사용하는데 리턴값이 c가 바뀔때마다 영향을 받으므로 순수함수가 아님
만약 c가 바꿀수없는 상수(const)변수라면 add2는 순수함수가 될수있음
"""
def add2(a: int, b: int):
    return a + b + c
```
