---
title: "react-router-dom 서버와 통신할때 유용한 useNavigation hook"
excerpt: "react-router-dom의 useNavigation hook에 대해 알아보자"

categories: react-router-dom
toc: true
toc_sticky: true
date: 2023-11-15
last_modified_at: 2023-11-15
---

### useNavigation hook란?

useNavigation hook는 react-router-dom이 제공하는 hook입니다 useNavigate와 이름은 비슷하지만 매우 다른 기능을 가지고 있으니 주의해서 사용해야합니다.

이 hook는 페이지 전환 상태나 form 제출 데이터등의 정보를 제공하는데요 서버와 통신할때 피드백을 주기위한 UI를 만들때 특히 유용합니다.

### 사용법

useNavigation은 사용법도 간단합니다. useNavigation()함수로 새 navigation을 만든 뒤 원하는 프로퍼티를 가져와 사용하면 됩니다.

```javascript
import { useNavigation } from "react-router-dom";

function SomeComponent() {
  const navigation = useNavigation();
  // useNavigation hook이 제공하는 정보 프로퍼티들
  navigation.state;
  navigation.location;
  navigation.formData;
  navigation.json;
  navigation.text;
  navigation.formAction;
  navigation.formMethod;
}
```

### navigation.state

useNavigation hook는 state 프로퍼티를 가지고 있습니다.
이 state 프로퍼티는 문자열인데요 idle, loading, submitting중 1개의 값을 가지고 있습니다.

idle: 말 그대로 아무것도 하지않는 기본상태일때입니다.

loading: 여기도 말 그대로 로딩중일때 상태입니다.

submitting: "PUT", "POST", "PATCH", "DELETE"같이 form을 제출하는 상태입니다.

form제출이 없는 "GET"같은 경우에는 idle -> loading -> idle순으로 상태가 변합니다.

form제출이 있는 경우에는 idle -> submitting -> loading -> idle순으로 상태가 변합니다.

### navigation.formData

"PUT", "POST", "PATCH", "DELETE"같이 데이터를 보내는 작업을 하면 첨부되는 데이터가 있을겁니다.

formData 프로퍼티는 그 추가되는 데이터들의 값들입니다.

이 프로퍼티는 사용자 경험을 위해 서버의 응답을 기다리지 않고 바로 UI에 결과를 노출하는 Optimistic UI을 만들때 유용합니다.

특별한 form제출이 없는 "GET"같은 경우에는 formData는 빈 값이 됩니다.

### 출처

https://reactrouter.com/en/main/hooks/use-navigation
