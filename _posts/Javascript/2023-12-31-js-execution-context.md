---
title: "Javascript 실행 컨텍스트(Execution context)"
excerpt: "Javascript의 실행 컨텍스트에 대해 알아보자"

categories: javascript
toc: true
toc_sticky: true
date: 2023-12-31
last_modified_at: 2023-12-31
---

### 실행 컨텍스트란?

실행 컨텍스트란 자바스크립트의 코드를 실행할때 필요한 정보들을 제공해주는 환경을 뜻합니다.

코드가 실행중에 현재 실행 컨텍스트와 상관없는 새로운 코드가 실행되면 해당 컨텍스트를 스택에 쌓은다음 실행 컨텍스트를 해당 컨텍스트로 변경합니다.

그런다음 현재 실행 컨텍스트의 작업이 모두 종료되면 스택에서 컨텍스트를 제거한뒤 실행 컨텍스트를 스택의 맨위에 있는 컨텍스트로 변경합니다.

```js
// 1. 자바스크립트는 코드를 시작할때 먼저 스택에 전역 컨텍스트를 쌓음
const a = 1;

function b() {
  // 함수 b 컨텍스트
  const c = 2;
  console.log(c);
  // 4. 이제 함수 b의 작업이 종료되므로 함수 b의 컨텍스트를 스택에서 제거, 실행 컨텍스트는 전역 컨텍스트로 변경
}

// 2. 현재 실행 컨텍스트인 전역 컨텍스트에서 변수 a의 정보를 찾아서 출력
console.log(a);

b(); // 3. 함수 b가 실행되면서 함수 b의 컨텍스트가 스택에 쌓임, 스택의 맨위에 있는 컨텍스트는 함수 b의 컨텍스트이므로 실행 컨텍스트는 함수 b의 컨텍스트로 변경됨
```

하지만 컨텍스트가 제거되는 부분에서 예외가 있을수도 있는데요 자세한 부분은 클로저에 대해 알아보시길 바랍니다.

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures
https://www.w3schools.com/js/js_function_closures.asp

### 실행 컨텍스트의 구조

자바스크립트의 버젼이 바뀌어감에 따라 실행 컨텍스트의 구조도 변경되었습니다 구글에 실행컨텍스트를 치면 버젼별로 구분을 해놓지않고 그냥 예전버젼의 구조가 올라와있는것이 많아서
실행 컨텍스트 구조가 버젼별로 어떻게 바뀌었는지 정리해보겠습니다.

### ES5 이전 버젼

ES5 이전 버젼에서는 실행 컨텍스트는 크게 LexicalEnvironment(LE), VariableEnvironment(VE) 그리고 This binding이 3가지 컴포넌트로 구성되어있습니다.

https://262.ecma-international.org/5.1/#sec-10.3

# LexicalEnvironment(LE)

LE는 lexical nesting structure구조에 따라 변수나 함수에대한 식별자를 저장합니다.

# VariableEnvironment(VE)

실행 컨텍스트가 처음 만들어질때 LE와 VE는 동일한 값을 가지지만 코드가 실행되면 LE의 값은 변경될수있지만 VE는 항상 초기의 값을 가지고 있습니다.

# ThisBinding

this에 대한 정보를 담고있습니다.

### ES6 이후 버젼

ES6에서 실행 컨텍스트의 구조가 변경되었습니다 this를 관리하던 this binding이 ER이 관리하는것으로 변경되어 실행 컨텍스트가 2가지 컴포넌트로 줄었습니다.

https://262.ecma-international.org/6.0/#table-23

# LexicalEnvironment(LE), VariableEnvironment(VE)

Lexical Environment(LE)과 Variable Environment(VE)는 둘다 ER에 있는 정보를 찾을수있는 컴포넌트입니다.

var로 선언된 변수는 VE에 저장되고 나머지 정보들은 다 LE에 저장됩니다.

# Environment Records(ER)

실행 컨텍스트 컴포넌트인 LE와 VE는 모두 ER을 가지고 있습니다.

ER은 현재 스코프의 식별자(변수, 함수등등)와 this의 값, 상위 스코프의 ER의 참조를 가지고 있습니다.

ER에는 OuterEnv필드에 자신의 상위 렉시컬 스코프의 ER의 참조를 저장합니다.

현재 실행 컨텍스트에 없는 정보를 찾으면 OuterEnv필드에 있는 상위 렉시컬 스코프 ER에서 해당 값을 찾거나 상위 ER의 OuterEnv가 없을때 까지 값을 찾습니다.

이 작업은 흔히 스코프 체인이라고 알려져있지만 lexical nesting structure가 맞는 말이라고 합니다.

### ES2022

ES2022에서 실행 컨텍스트에 PrivateEnvironment라는 컴포넌트가 추가되었습니다.

https://262.ecma-international.org/13.0/#table-additional-state-components-for-ecmascript-code-execution-contexts

# PrivateEnvironment

이 컴포넌트는 클래스에서 생성된 Private Names들을 담고있는 컴포넌트입니다.
