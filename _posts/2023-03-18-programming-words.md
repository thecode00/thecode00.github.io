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

운영체제(Operating System): 줄여서 OS라고도 부른다. 하드웨어와 소프트웨어를 관리하는 소프트웨어로서 사용자가 컴퓨터를 쉽고 효율적으로 사용할수있게 해준다. 프로세스 관리, 저장장치 관리,  
네크워킹, 사용자 관리, 디바이스 드라이버 등 여러가지 작업을 수행

커널(Kernel): OS의 핵심적인 부분 OS의 심장이라고도 불림, OS의 맨 하부에서 돌아가며 하드웨어와 프로세스의 보안, 시스템의 자원관리 등등 여러가지 작업들을 수행함

인스턴스(Instance): 객체나 클래스를 실체화한것
