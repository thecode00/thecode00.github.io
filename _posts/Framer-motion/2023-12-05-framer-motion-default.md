---
title: "framer-motion의 사용법 기본편"
excerpt: "framer-motion의 기본 사용법에 대해 알아보자"

categories: framer-motion
toc: true
toc_sticky: true
date: 2023-12-07
last_modified_at: 2023-12-07
---

### 프레이머 모션(framer-motion)이란?

프레이머 모션 라이브러리는 애니메이션 라이브러리입니다. 애니메이션은 css로도 구현가능하지만 복잡한 애니메이션이 복잡해지거나 DOM에 관련된 애니메이션을 사용하려면 css로는 부족하거나 구현이 매우 복잡해지는데 이럴때 도움이 되는 라이브러리입니다.

또 프레이머 모션을 이용해서 애니메이션을 구현하면 css애니메이션과는 다르게 물리현상이 적용된 자연스러운 애니메이션이 만들어집니다.

<!-- TODO: 애니메이션 샘플 가져오기 -->

### 기본 사용법

## motion component

프레이머 모션에는 motion이라는 특수한 컴포넌트가 있는데요 애니메이션을 적용하고 싶은부분의 태그에 motion을 추가하면 됩니다. 예를들어 div에 애니메이션을 적용하고 싶다면 <motion.div> 컴포넌트를 사용하면 됩니다.

이 motion컴포넌트는 애니메이션 재생시 컴포넌트의 불필요한 리렌더링을 방지하는등 애니메이션 성능에 특화된 컴포넌트 입니다.

```js
// 일반
<div></div>
// 애니메이션 특화 컴포넌트
<motion.div></motion.div>
```

## animate prop

이제 motion컴포넌트에 애니메이션을 추가하려면 animate라는 prop을 전달해주면 됩니다.  
animate prop은 재생할 애니메이션에 대한 정보를 담은 객체를 전달받는데요 만약 x방향으로 100을 움직이는 애니메이션을 재생하고 싶다면 {x: 100}이라는 객체를 animate prop에 전달해주면 됩니다.

motion에 전달된 animate의 값이 변경될경우 프레이머 모션이 자동으로 animate가 변경되기 전 값과 변경된 후의 값의 차이를 가지고 애니메이션을 재생합니다.

```js
// x좌표가 30, y좌표가 100움직이는 애니메이션이 재생됨
<motion.div animate={{ x: 30, y: 100 }}></motion.div>
```

## initial prop

이 prop은 요소가 DOM에 추가된 후 실행될 애니메이션의 초기 상태를 전달받습니다.

## exit prop

이 prop은 요소가 DOM에서 사라지기 전에 재생할 애니메이션에 대한 정보를 전달받습니다.

이 prop이 css대신 프레이머 모션을 사용하는 이유중 1개가 될수있는데요 DOM에서 사라지는 요소에 애니메이션을 적용하려면 자바스크립트의 도움없이는 css혼자서 할수없는 작업입니다.

exit prop은 initial prop과는 다르게 exit 애니메이션을 적용할 요소를 <AnimatePresense/>라고 하는 특수한 컴포넌트로 감싸야합니다.

AnimatePresense 컴포넌트는 AnimatePresense 안에 있는 요소들중에 DOM에서 사라지는 요소가 exit 애니메이션을 가지고 있는지 확인하고 가지고 있다면 DOM에서 바로 사라지는것을 막고 exit애니메이션을 재생한뒤 DOM에서 사라지게 해줍니다.

AnimatePresense 컴포넌트는 이것말고도 다른 기능도 많이 있는데요 다른 기능들은 추후에 다른글에 정리 해보겠습니다.

### 출처

https://www.framer.com/motion/introduction/
