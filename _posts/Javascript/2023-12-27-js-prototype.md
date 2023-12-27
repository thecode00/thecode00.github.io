---
title: "Javascript 객체의 Prototype"
excerpt: "Javascript의 객체의 Prototype에 대해 알아보자"

categories: javascript
toc: true
toc_sticky: true
date: 2023-12-27
last_modified_at: 2023-12-27
---

## 존재 이유

여러분들은 자바스크립트를 객체에 어떻게 자기가 객체에 넣지않은 toString과 같은 메소드가 있는것을 본적 있을겁니다.

이 메소드들은 객체들이 자신의 상위 객체인 프로토타입 객체에서 상속받아와서 사용할수 있는것인데요 자바스크립트에서는 OOP(객체 지향 프로그래밍)에서 사용하는 상속의 개념을 프로토타입을
이용해 구현해 놨습니다.

## 작동방식

객체는 프로토타입은 참조 링크형식으로 "[[Prototype]]" 이라는 내부 프로퍼티에 저장됩니다.

참조 링크형식이기 때문에 해당 프로토타입 객체의 내용이 변하면 해당 프로토타입을 링크로 가지고 있는 모든 객체들은 변경된 내용이 적용됩니다.

```js
const blank = {};

consolg.log(blank); // 콘솔에서 [[Prototype]]을 확인하실수 있습니다!
console.log(blank.toString()); // [Object object]
```

이 빈 객체에는 toString이라는 메소드가 없지만 프로토타입에 정의되어있는 toString을 상속받아 사용할수 있습니다.

이처럼 빈 객체에서 상위 프로토타입의 toString을 검색해 가져오는 작업을 프로토타입 체이닝이라고 합니다.

## Object.prototype

이 프로토타입은 모든 객체의 최상위 객체입니다 모든 객체의 뿌리라고도 볼수있습니다.

배열은 일반적은 객체와는 다른 Array.prototype을 가지고있는데요 이 Array 프로토타입도 Object.prototype의 하위 객체로 연결되어있습니다.
