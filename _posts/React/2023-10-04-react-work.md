---
title: "리액트가 작동하는 방식"
excerpt: "리액트가 어떤방식으로 작동하는지 알아보자"

categories: react
toc: true
toc_sticky: true
date: 2023-10-04
last_modified_at: 2023-10-04
---

### React

리액트는 자바스크립트의 UI인터페이스 라이브러리이다.

### React DOM

리액트는 웹페이지를 관리하는 라이브러리가 아니다 그냥 컴포넌트의 변경 전후의 상태를 확인해서 변경된내용들과 화면에 표시되야 할 내용들을 React DOM에게 전해준다.  
사실은 React DOM이 DOM에 관련된 작업들을 하기 때문에 사용자의 화면에 무언가를 표시하는 역할들은 리액트가 아닌 React DOM이 한다.
\*\*리액트는 컴포넌트만 신경쓴다!

### 리액트의 데이터들

props: 부모-자식 컴포넌트간의 데이터 부모에서 자식으로만 가능 단방향 데이터
state: 컴포넌트 내부의 데이터
context: 전체 컴포넌트의 데이터, 전역변수와 비슷한 개념

props, state, context가 변경되면 이 데이터를 컴포넌트들을 리액트가 변경하고, 화면에 새로운것을 표시하는지에 대해 확인한다.  
만약 화면에 새롭게 표시할것이 있다면 리액트는 React DOM에 이것을 알려줘서 React DOM이 새로운 컴포넌트와 화면들을 표시할수있게 해준다.

### 가상 DOM(Virtual DOM)

실제 DOM과는 다른 메모리상에만 존재하는 앱이 마지막에 만들어내는 컴포넌트 트리 실제DOM을 사용하는 작업은 자원이 많이들기때문에 가상DOM을 사용한다.  
컴포넌트들이 JSX코드를 반환하면 이 정보를 바탕으로 컴포넌트 트리를 만든다.  
컴포넌트의 State나 props, context가 변경되면 컴포넌트 함수가 재실행되는데 이때 가상DOM의 변경 전후 상태를 비교한다음 실제DOM에 변경이 필요할때만 실제DOM이 업데이트 된다.

```html
<!-- 변경 전 -->
<div>
  <h1>Hello!</h1>
</div>
```

```html
<!-- 변경 후 -->
<div>
  <h1>Hello!</h1>
  <p>World!</p>
</div>
```

리액트는 두 스냅샷간의 차이점을 확인한다음 이것을 React DOM에 알려주고 React DOM은 실제DOM을 변경한다.  
위 예시에선 <p>World!</p>만 추가되었으므로 실제DOM전체를 리렌더링하는게 아닌 변경이 필요한 p태그만 추가한다.
