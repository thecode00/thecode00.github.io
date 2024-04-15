---
title: "Javascript의 잘 안 쓰이지만 재밌는 기능들이나 신기한 사실들"
excerpt: "Javascript의 잘 안 쓰이지만 재밌는 기능들에 대해 알아보자"

categories: javascript
toc: true
toc_sticky: true
date: 2024-04-08
last_modified_at: 2024-04-08
---

### 머릿말

자바스크립트를 공부하면서 잘 쓰이지 않지만 신기한 기능들이나 신기한 사실들을 정리해봤습니다.

### 태그된 템플릿 리터럴(Tagged template literal)

백틱을 사용한 템플릿 리터럴은 다들 익숙하실텐데요 백틱앞에 함수(태그) 이름이 있으면 템플릿안에 있는 텍스트와 표현식의 평가값이 해당 함수로 인수로 전달됩니다.

```js
function tagged(tempString) {
  return tempString + "Tagged";
}

console.log(`String`.length); // 6
console.log(tagged`String`.length); // 12, tagged 함수에서 Tagged를 더한 문자열을 반환
```

### typeof null === "object"

자바스크립트에는 Number, String, Boolean, null, undefined, Symbol, BigInt 7가지 원시타입이 있습니다. 그리고 typeof라는 데이터 타입을 알려주는 키워드도 있는데요

null에 typeof를 사용할경우 "null"이 나올거라는 예상과는 다르게 "object"가 나옵니다. null과 비슷한 특징을 가지고 있는 undefined는 "undefined"를 반환합니다.

### 타입 변환

자바스크립트는 타입을 강제하지 않고 예상되는 타입이 있으면 그 타입이 아닌 값이 들어와도 예상 타입으로 변환합니다. 이 성질을 이용해서 String() 같은 함수를 사용하지않고 타입을 변환할수 있습니다.

```js
n + ""; // String(n)
+n; // Number(n)
n - 0; // Number(n)
```

### 점프 문(Statement)와 라벨 문의 조합

자바스크립트의 문(Statement)에는 라벨을 붙일수 있는데요 break와 continue같은 점프문에서 해당 라벨을 사용해서 신기한 기능을 사용할수 있습니다.

# break

break문은 루프나 switch문을 탈출하기 위해 사용하지만 라벨과 함께 사용하면 해당 라벨을 가진 문에서 탈출할수 있게 할수있습니다.

```javascript
let complete = false;
iAmALabel: if (true) {
  for (let idx = 0; idx < 5; idx++) {
    break iAmALabel;
  }
  complete = true;
}
console.log(complete); // false, break문이 for루프를 탈출하는게 아닌 라벨이 붙은 if문을 탈출
```

# continue

### yield

제너레이터 함수에서 쓰는 문으로써 return과 매우 비슷하지만 return은 함수를 종료시키고 제어권을 넘기지만 yield는 제어권을 넘기지 않습니다.

### Object.create(null)

객체를 생성할때 Object.create()함수에 첫번째 인자로 새 객체의 프로토타입이 될 객체를 넘겨줄수있는데 이떄 null을 넘겨주면 아무것도 상속받지않은 기본 메소드조차 없는 새 객체가 만들어집니다.

```js
let newObj = Object.create(null);
newObj.toString(); // TypeError, 아무것도 상속받지않은 객체기 때문에 toString 메소드가 존재하지않습니다.

let newObj2 = {};
newObj2.toString(); // '[object Object]', 객체 리터럴을 사용할경우 Object.prototype에서 상속받음
```

### 객체의 프로퍼티 이름 목록 배열을 가져오는 법

객체에 있는 프로퍼티들의 배열을 가져오는 법들중에 프로퍼티 이름의 타입이나 열거 가능 속성에 따라 다른 배열을 반환합니다.

# Object.keys()

객체의 자체 프로퍼티중에 이름이 문자열인 프로퍼티의 이름만 배열에 담아 반환합니다.

# Object.getOwnPropertyNames()

객체의 자체 프로퍼티중 이름이 문자열인 프로퍼티의 이름을 배열에 담아 반환합니다. Object.keys()와는 다르게 열거 가능 속성을 무시합니다.

# Object.getOwnPropertySymbols()

객체의 자체 프로퍼티중 이름이 심볼인 프로퍼티의 이름만 배열에 담습니다. 얘도 Object.getOwnPropertyNames()와 마찬가지로 열거 가능 속성을 무시합니다.

# Reflect.ownKeys()

객체의 자체 프로퍼티 이름을 모두 담아 배열에 담습니다.
