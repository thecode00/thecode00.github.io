---
title: "react-router-dom 기본 사용법에 대해 알아보자"
excerpt: "react-router-dom 기본 사용법에 대해 알아보자"

categories: react-router-dom
toc: true
toc_sticky: true
date: 2023-11-05
last_modified_at: 2023-11-05
---

### 설치방법

`npm install react-router-dom`

특정 버젼을 설치하고 싶다면
`npm install react-router-dom@<원하는 버젼>`
을 사용하면 됩니다.

ex. `npm install react-router-dom@6.3.0`

### 사용방법 (v6.4이후)

v6.4부터 Router를 사용하는 방식이 달라졌습니다.

이전에는 <Routes>태그 안에 루트들을 넣는 JSX방식을 썼지만 v6.4이후에는 createBrowserRouter함수를 사용하여 Router 싱글톤을 생성합니다.

v6.4미만 버젼코드:

```jsx
import { BrowserRouter, Link, Route, Routes } from "react-router-dom";

export default function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/blog/*" element={<BlogApp />} />
        <Route path="/users/*" element={<UserApp />} />
      </Routes>
    </BrowserRouter>
  );
}
```

이 글에서는 v6.4이후에 달라진 방식을 소개합니다.

### Router 설정

1. 우리가 지원하고자 하는 경로들을 추가
   createBrowserRouter에 각 Route객체들을 담은 배열을 전달합니다.

```jsx
const browserRouter = createBrowserRouter([
  {
    path: "/",
    element: <Home />,
  },
  {
    path: "/blog",
    element: <BlogApp />,
  },
  {
    path: "/users",
    element: <UserApp />,
  },
]);
```

각 Route객체는 경로를 담당하는 path와 그 path로 갔을때 표시할 컴포넌트를 정의한 element프로퍼티가 존재합니다.

path 프로퍼티는 `https://www.example.com/blog`라는 url에서 도메인뒤에 있는 `/blog`부분이 path입니다.

element 프로퍼티는 해당 Route객체가 활성화 되었을때 표시할 컴포넌트에 대한 정보입니다.  
예를 들어 `https://www.example.com`이라는 사이트에서 `https://www.example.com/blog`라는 경로에서 `<BlogApp />`이라는 컴포넌트를 표시하고 싶을때  
`{path: '/blog', element: <BlogApp/>}`를 추가하면 됩니다.

2.  Router를 활성화
    `<RouterProvider/>` 컴포넌트를 임포트 해온후 router프로퍼티에 browserRouter를 넣습니다.

```jsx
export default function App() {
  return <RouterProvider router={browserRouter} />;
}
```

이러면 Router는 url을 살펴본뒤 현재 활성화된 path가 무엇인지 확인한후 해당 path가 지원되는 path라면 해당 객체의 element에 있는 컴포넌트를 가져옵니다.

최종 코드

```jsx
import { createBrowserRouter, RouterProvider } from "react-router-dom";

const browserRouter = createBrowserRouter([
  {
    path: "/",
    element: <Home />,
  },
  {
    path: "/blog",
    element: <BlogApp />,
  },
  {
    path: "/users",
    element: <UserApp />,
  },
]);

export default function App() {
  return <RouterProvider router={browserRouter} />;
}
```

### Route 사이의 이동을 담당하는 Link

html에서는 페이지 이동을 위해 "a" 앵커태그를 사용하지만 앵커태그를 클릭하면 서버에 새로운 html페이지를 요청하게 됩니다.

SPA에서는 처음에 모든 javascript, css, html파일들을 불러오는데 서버에 새로운 요청을 보내게되면 다시 모든 파일들을 불러오고 react는 애플리케이션을 재시작합니다.

이런 불필요한 작업을 방지하기위해 react-router-dom에는 "Link"라는 컴포넌트가 존재합니다.

```jsx
export default function Home() {
  return <Link to="/">Go to </Link>;
}
```

앵커태그는 href 속성으로 경로를 지정하는데요 Link 컴포넌트는 to 속성으로 경로를 지정합니다.

### 참조

https://reactrouter.com/en/main/start/tutorial
https://reactrouter.com/en/main/upgrading/v6-data
