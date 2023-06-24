---
title: "C++ sort함수의 compare함수에 대해 헷갈리는것을 정리"
excerpt: "C++ sort함수의 compare함수에 대해 헷갈리는것을 정리"

categories: c++
toc: true
toc_sticky: true
date: 2023-06-24
last_modified_at: 2023-06-24
---

### 발단

c++를 배우고있는 도중 leetcode의 문제를 풀고있는데 조건이 필요한 정렬이 필요해서 관련내용을 찾아보니 sort함수의 세번째 인자로 compare함수를  
넘겨주면 조건정렬이 가능한것을 알게됐다. 그런데 compare함수는 bool을 반환하는 함수인데 true와 false를 반환하는게 무슨의미인지 궁금해졌다.

```cpp
bool compare(int a, int b){ // 올림차순 정렬조건
    return a < b;
}

bool compare(int a, int b){ // 내림차순 정렬조건
    return a > b;
}
```

## Chat gpt

처음엔 gpt에게 물어봤다.  
Q. sort함수의 compare함수의 반환값에따라 하는 작업알려줘

A.
C++의 std::sort 함수에서 compare 함수의 반환값에 따라 다음과 같은 작업이 수행됩니다:

Compare 함수가 true를 반환하는 경우:

두 요소의 순서가 바뀌어야 하므로, 요소들이 재배치됩니다. 첫 번째 요소가 두 번째 요소보다 작은 순서로 정렬됩니다.
Compare 함수가 false를 반환하는 경우:

두 요소의 순서가 바뀌지 않아도 되므로, 요소들의 상대적인 순서는 유지됩니다. 정렬이 필요하지 않은 것으로 간주됩니다.
정리하면, compare 함수가 true를 반환하면 요소들의 순서가 변경되고, false를 반환하면 요소들의 순서가 유지됩니다. 이를 통해 std::sort 함수는 정렬 조건에 따라 요소들을 재배치합니다.

Gpt의 말에 따르면 compare함수가 true를 반환하면 두 요소의 위치가 바뀌고 false를 반환하면 정렬된상태로 판단하고 넘어가는거 같다.  
그런데 뭔가 조금 이상해서 한번 더 물어봤다.

A. 죄송합니다. 이전 답변에서 실수가 있었습니다. 제가 잘못된 정보를 전달한 것 같습니다. 올바른 설명을 다시 제공드리겠습니다.

C++의 std::sort 함수에서 compare 함수의 반환값에 따라서 정렬이 수행되는 것은 아닙니다. 실제로 compare 함수의 반환값이 true인지 false인지에 상관없이, std::sort 함수는 비교 함수의 반환값에 의존하여 요소들을 재배치합니다.

비교 함수의 반환값이 true인 경우, std::sort 함수는 두 요소의 순서를 바꾸고 정렬을 수행합니다. 그러나 비교 함수의 반환값이 false인 경우에는 두 요소의 순서를 바꾸지 않으며, 정렬이 수행되지 않습니다. 따라서, compare 함수의 반환값이 true 또는 false인지에 따라서 정렬의 방향이 결정되는 것은 아닙니다.

정리하면, std::sort 함수는 비교 함수의 반환값을 사용하여 요소들을 정렬합니다. 반환값이 true인 경우와 false인 경우에 따라서 요소들이 재배치되는 것이 아니라, 비교 함수의 반환값을 기준으로 정렬이 수행됩니다.

gpt의 답변이 마음에 안들어서 cppreference에서 sort함수에 관한부분을 찾아봤다.
https://en.cppreference.com/w/cpp/algorithm/sort  
그리고 또 이분의 블로그도 도움이 되었다.
https://velog.io/@dlsghl92/Strict-Weak-Ordering

## 결론

compare함수가 a, b를 입력으로 받고 true를 반환했다면 a가 b보다 정렬순서상 앞에 있어야한다는것을 의미한다.  
다만 true와 false 둘중 뭘 반환하든 요소들을 재배치하는것까지는 확인을 못했다 stackoverflow에서도 그건 알고리즘이 하는일이라 알 필요가 없다고 나왔다.  
gpt의 답변이 맞는거같으면서 아닌거같은 느낌이 든다.
