---
title: "react-router-dom의 loader 함수"
excerpt: "react-router-dom의 loader 함수에 대해 알아보자"

categories: react-router-dom
toc: true
toc_sticky: true
date: 2023-11-18
last_modified_at: 2023-11-18
---

### loader의 필요성

서버에서 데이터를 가져와서 그 데이터를 토대로 렌더링하는 컴포넌트가 있다고 가정해보겠습니다.

서버와 통신하는 sideEffect 작업을 위한 useEffect hook을 사용한다고 했을 때 문제점은 useEffect hook은 컴포넌트의 렌더링이 끝난뒤 실행된다는 점입니다.

컴포넌트의 자식 컴포넌트가 많을경우 그 자식 컴포넌트를 다 렌더링한뒤 그제서야 useEffect가 실행되서 서버에서 데이터를 가져오는데

이럴때 react-router-dom에서 각 route에서 loader라는 함수를 정의할수 있습니다.

이 loader라는 함수는 element 프로퍼티에 있는 컴포넌트가 렌더링되기전에 실행되는 함수이므로 위의 예제에 알맞은 해결법이라고 할수있습니다.

### loader 사용법

사용법은 매우 간단한데 router에 넣었던 route객체의 loader프로퍼티에 원하는 함수를 정의해주면 됩니다.

```javascript
{
    element: <Home />,
    path: "/",
    loader: () => {
      // 원하는 작업 넣기
      console.log("Hello!")
    }
}
```

컴포넌트 안에 loader에 사용할 함수를 정의한뒤 export하고 그 함수를 route가 정의된곳에서 import해서 사용하는 방식이 일반적으로 많이 쓰인다고 합니다.

```javascript
// Home.js
// ...
export const loaderFunc = () => {
    // ...
}

// App.js
import {loaderFunc} from "./Home.js"

// ...
{
    element: <Home />,
    path: "/",
    loader: loaderFunc
}
```

### loader에서 데이터 가져오기

이제 loader함수를 사용하는 법은 알았는데 loader는 route가 설정되어있는곳에 있으니 어떻게 거기서 데이터를 가져오는지 궁금하실겁니다.

이럴때 사용하는 hook이 바로 useLoaderData hook입니다.

이 hook는 "가장 가까운" loader함수가 리턴한 값을 제공해줍니다.

```javascript
// 만약 loader함수가 5를 리턴했다면 data는 5가 됨
const data = useLoaderData();
```

주의할점이 1개 있는데요 loader에서 값을 가져오는건 그 loader의 상위 route에서는 불가능하다는 점입니다.

만약 "/"의 children으로 "/a"라는 경로에서 loader를 사용했을때 "/" route의 element는 "/a"의 loader 데이터를 가져올수없습니다.

### 출처

https://reactrouter.com/en/main/route/loader
