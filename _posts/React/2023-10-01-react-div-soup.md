---
title: "리액트의 div soup방지하기"
excerpt: "리액트의 div soup가 왜 생기는지 그리고 해결법은 뭔지 알아보자"

categories: react
toc: true
toc_sticky: true
date: 2023-10-01
last_modified_at: 2023-10-01
---

### div soup란? 그리고 생기는 이유는?

JSX는 무조건 1개의 루트를 반환해야하는 제한이있다. 아래 Temp컴포넌트로 예를들어 그 이유를 설명하겠다.

```javascript
function Temp(props) {
  return (
    <h1>HELLO!</h1>
    <p>world!</p>
  );
}
```

JSX는 표준 자바스크립트 코드가 아니므로 리액트는 뒤에서 JSX를 표준 자바스크립트코드로 변환해주는데 그럼 아래코드처럼 변환한다.

```javascript
function Temp(props) {
  return (
    React.createElement("h1", {}, "HELLO!")
    React.createElement("p", {}, "world!")
  );
}
```

Temp컴포넌트는 1개의 루트가아닌 동시에 2가지컴포넌트를 반환하고있다.  
자바스크립트의 문법은 동시에 2가지를 반환하는것을 허용하지않는다 그래서 우리는 무조건 1개의 루트를 반환하는것이다.

div soup는 흔히 루트로 사용하는 div태그가 자바스크립트의 콜백지옥처럼 여러번 중첩되는 현상을 말한다.

```html
<div>
  <div>
    <div>
      <div>
        <div><h2>Hello!</h2></div>
      </div>
    </div>
  </div>
</div>
```

이렇게 쓸데없는 div들을 렌더링 하기때문에 성능이 안좋아진다.

### 해결법 1: 래퍼(Wrapper) 사용하기

루트로 사용되는 div를 아예 아무것도 하지않고 자신의 자식 컴포넌트들만 반환하는 래퍼(Wrapper) 컴포넌트를 루트로 사용하는 방법이다.

```javascript
function Wrapper(props) {
  return props.children;
}
```

JSX 우리가 명시하지않아도 자동으로 props.children에 컴포넌트 태그 사이에있는 자식 컴포넌트들을 다 넣어준다.
이제 이 Wrapper컴포넌트를 div대신 루트로 사용하면 Wrapper는 아무것도 하지않고 자식 컴포넌트들을 반환하는 컴포넌트이므로 루트가 생기지않고 자식 컴포넌트들만 표시된다.

### 해결법 2: 조각(Fragment) 사용하기

사실 래퍼는 리액트에서 Fragment라는 래퍼와 같은기능을 하는것을 만들어놨기 때문에 우리가 직접만들어서 사용할 필요가 없다.

```javascript
function Temp() {
  return (
    <>
      <h1>HELLO!</h1>
      <p>world!</p>
    </>
  );
}
```

사용법은 <></>나 <React.Fragment></React.Fragment>를 루트로 사용하면 된다.
래퍼(Wrapper)와 조각(Fragment)모두 렌더링되지 않기 때문에 쓸데없는 요소들이 줄어들어서 성능을 최적화할수있다.

### 마치며

웹의 성능최적화를 위해선 기본지식들이 많이 필요한거같다.  
웹을 예쁘게 꾸미는법과, 기능만 공부하지말고 성능최적화에도 관심을 많이 가져야겠다.
