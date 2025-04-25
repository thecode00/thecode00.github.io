---
title: "LeetCode 2845. Count of Interesting Subarrays 문제의 알고리즘"
toc: true
toc_sticky: true
date: 2025-04-25
last_modified_at: 2025-04-25
---

# 문제 설명

문제 링크: [https://leetcode.com/problems/count-of-interesting-subarrays/description](https://leetcode.com/problems/count-of-interesting-subarrays/description)

이 문제에서는 정수 배열 `nums`, 정수 `modulo`, 정수 `k`가 주어집니다.  
우리는 이 배열에서 `interesting`한 부분 배열이 총 몇 개인지 구해야 합니다.

`interesting`한 부분 배열이란 다음의 조건을 만족하는 배열을 의미합니다:

- 인덱스 범위 `[l, r]` 사이에서 `nums[i] % modulo == k`인 인덱스의 개수를 `cnt`라고 할 때,
- 이 `cnt`가 `cnt % modulo == k`를 만족해야 합니다.

# 코드

```python
class Solution:
    def countInterestingSubarrays(self, nums: List[int], modulo: int, k: int) -> int:
        count = 0
        prefix = 0
        freq = defaultdict(int)
        freq[0] = 1  # 초기 상태: prefix % modulo가 0인 경우를 하나 포함합니다.

        for num in nums:
            if num % modulo == k:
                prefix += 1

            target = (prefix - k) % modulo
            count += freq[target]

            freq[prefix % modulo] += 1

        return count
```

# 코드 설명

이 코드는 누적합과 해시맵을 활용하여 `interesting`한 부분 배열의 개수를 효율적으로 세는 방식으로 동작합니다.

우선 `prefix`라는 변수는 현재까지 `nums[i] % modulo == k`인 원소의 개수를 누적한 값입니다.  
즉, 인덱스 `0`부터 현재 위치까지 조건을 만족하는 값이 몇 개인지를 세는 용도로 사용됩니다.

문제의 조건을 만족하는 부분 배열 `[i, j]`를 구하기 위해서는,  
해당 구간 내에서 조건을 만족하는 원소의 개수인 `cnt`가 `cnt % modulo == k`를 만족해야 합니다.  
이때 `cnt`는 누적합을 이용해 `prefix[j] - prefix[i - 1]`의 형태로 나타낼 수 있습니다.

이 식을 모듈로 연산으로 바꾸면 다음과 같은 형태가 됩니다:

```
(prefix[j] - prefix[i - 1]) % modulo == k
→ prefix[i - 1] % modulo == (prefix[j] - k) % modulo
```

즉, 현재 `prefix`에 대해 `(prefix - k) % modulo`인 이전 `prefix` 값의 개수를 세면 됩니다.  
이를 위해 `freq`라는 딕셔너리를 사용해, 각 `prefix % modulo` 값을 몇 번 만났는지를 저장해두고,  
필요할 때마다 그 값을 조회하여 카운트를 누적하는 방식으로 구현하였습니다.

# 수학적 설명

## 왜 `(prefix - k) % modulo` 값을 찾는가?

문제에서 원하는 조건은 부분 배열 내의 조건 만족 개수인 `cnt`가  
`cnt % modulo == k`를 만족하는 경우입니다.

이 `cnt`는 결국 어떤 범위 `[i, j]`에 대해 `prefix[j] - prefix[i - 1]`로 계산할 수 있으므로,  
조건은 아래와 같이 변형됩니다:

```
(prefix[j] - prefix[i - 1]) % modulo == k
```

이 식을 정리하면:

```
prefix[i - 1] % modulo == (prefix[j] - k) % modulo
```

즉, 현재 prefix 값이 주어졌을 때, 그 이전에 등장한 prefix 중  
`(prefix - k) % modulo`와 같은 값을 갖는 prefix의 개수를 찾으면,  
그만큼의 부분 배열이 조건을 만족하게 됩니다.

그래서 우리는 해시맵에 prefix 값들을 기록해두고,  
필요할 때마다 해당 `target prefix`(prefix[i - 1])의 개수를 더해주어 전체 개수를 계산할 수 있게 되는 것입니다.
