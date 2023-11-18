---
title: "리액트 Hooks rule"
excerpt: "리액트의 훅을 쓸때의 규칙들을 알아보자"

categories: react
toc: true
toc_sticky: true
date: 2023-10-02
last_modified_at: 2023-10-02
---

## 리액트 Hook를 쓸때 지켜야할 규칙들

### 1. 리액트 Hook는 무조건 리액트 함수내에 있어야한다

Hook는 컴포넌트 함수와 사용저 설정 Hook내에 있어야한다.

```javascript
function temp() {
  useState(); // <= 오류!
}
```

temp함수는 JSX를 반환하는 컴포넌트 함수도 아니고 사용자 설정 Hook도 아니기 때문에 오류가 뜬다 오류내용에도 똑같은 설명이 나온다

### 2. Hook을 리액트 함수의 최상위 수준에서만 호출해야한다

```javascript
const Temp = () => {
  useEffect(() => {
    useContext(); // <= 에러!
  }, []);

  if (true) {
    useState(); // <= 에러!
  }
  return <div>Hello</div>;
};
```

Hook를 중첩함수나 if문에도 호출하지말아야 한다
