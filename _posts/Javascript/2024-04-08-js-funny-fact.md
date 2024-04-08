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
