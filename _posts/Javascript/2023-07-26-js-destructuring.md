---
title: "자바스크립트의 구조분할"
excerpt: "자바스크립트의 구조분할을 정리해보자"

categories: javascript
toc: true
toc_sticky: true
date: 2023-07-26
last_modified_at: 2023-07-26
---

## 구조분할(Destructuring)

배열의 원소나 객체의 프로퍼티를 꺼내서 변수에 저장할수있게 해준다  
하는일을 봐서는 스프레드 연산자와 비슷해보이지만 스프레드연산자는 배열이나 원소에 있는것을 모두 펼쳐서 주지만 구조분할은 특정 원소나 프로퍼티만 추출해준다

## 예시

```javascript
let arr = [1, 2, 3, 4];
let obj = { a: 1, b: 2 };

[var1, var2] = arr; // arr배열에서 원소 추출
console.log(var1, var2); // 1, 2
console.log(...arr); // 스프레드 연산자는 모든 원소를 펼침
let { a } = obj; // 객체에서 a프로퍼티 추출
console.log(a); // 만약 a가아닌 b를출력한다면 추출한적이 없으므로 undefind가 나옴
```
