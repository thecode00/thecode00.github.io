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

## 실행 컨텍스트의 생김새

실행 컨텍스트는 크게 Lexical Environment(LE)와 Variable Environment(VE) 이 두 가지 요소로 이루어져있습니다.

해당 요소들은 Environment Records(ER)을 바인딩 하고있습니다 ER에 대한 정보는 아래에서 서술하겠습니다.

ES5이전버젼까지는 this의 정보를 가지고 있는 this 바인딩이 저 두 요소와 같은레벨에 위치해서 3개의 요소가 있었지만 해당 부분이 Environment Records(ER)이 담당하도록 바뀌면서 실행 컨텍스트는 두 가지 요소를 가지도록 변했습니다.

# Lexical Environment(LE), Variable Environment(VE)

Lexical Environment(LE)과 Variable Environment(VE)는 둘다 ER에 있는 정보를 찾을수있는 컴포넌트입니다.

var로 선언된 변수는 VE에 저장되고 나머지 정보들은 다 LE에 저장됩니다.

# Environment Records(ER)

실행 컨텍스트 요소인 LE와 VE는 모두 ER을 가지고 있습니다.

ER은 현재 스코프의 식별자(변수, 함수등등)와 this의 값, 상위 스코프의 ER의 참조를 가지고 있습니다.

ER에는 OuterEnv필드에 자신의 상위 렉시컬 스코프의 ER의 참조를 저장합니다.

이 OuterEnv필드를 통해 상위 스코프의 ER에서 식별자를 찾는 스코프체인이 가능합니다.
