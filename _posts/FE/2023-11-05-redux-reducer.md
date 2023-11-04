---
title: "Redux의 reducer함수에 대해 알아보자"
excerpt: "Redux의 reducer함수에 대해 알아보자"

toc: true
toc_sticky: true
date: 2023-11-05
last_modified_at: 2023-11-05
---

### Reducer함수를 쓸때 지켜야할 점

Reducer함수는 부수 효과 (Side effect)가 없는 순수함수여야한다.

Reducer함수에는 state, action매개변수가 있는데 데이터를 수정하기 위해서는 state의 값을 변경해서는 안돼고 반드시 새 데이터를 리턴하는 방식을 써야한다.
