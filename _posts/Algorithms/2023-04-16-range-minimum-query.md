---
title: "구간 최소 질의 이해하기"
excerpt: "구간 최소 질의(Range minimum query)에 대해 정리"

categories: algorithm
toc: true
toc_sticky: true
date: 2023-04-16
last_modified_at: 2023-04-16
---

### 최소 구간 질의(Range minimum query) 알고리즘

배열의 원소가 변하지않는 정적배열에서 배열의 일부구간의 최소값을 찾는 알고리즘  
배열 arr의 left ~ right인덱스중 최소값을 찾는 방법들은 쿼리당 O(N)의 시간복잡도를가진 브루트포스, O(N)의 전처리 시간 복잡도와 쿼리당 O(√N)의 시간복잡도를 갖는 Sqrt Decomposition 방법,  
O(n log n)의 전처리 시간복잡도와 쿼리당 O(1)의 시간복잡도를 가진 희소 테이블 알고리즘(Sparse table algorithm)이 있다.

## 브루트포스 방법

위 방법중 가장 직관적으로 알수있는 방법이지만 쿼리마다 O(right - left + 1) = O(N)만큼 걸리므로 쿼리가 많아지면 많아질수록 시간이 많이걸릴수 있다.
방법은 간단하다 arr의 left에서 right사이의 값중 최소값을 알고싶을때 left ~ right에있는 원소들을 쿼리마다 살펴보면 된다.

```python
def bruteforce(arr: List[int], left: int, right: int) -> int:
    min_value = float("inf")
    for idx in range(left, right + 1):
        min_value = min(min_value, arr[idx])
    return min_value

print(bruteforce([5, 1, 2, 3, 4], 1, 3))   # 1
```

## Sqrt Decomposition

배열의 길이 n에서 루트를 적용하여 배열을 √n길이를 가진 부분배열로 나눠서 부분배열의 최소값을 저장하는 방식으로 전처리를 한다.  
전처리를 하는데 O(N)의 시간이 걸리고 쿼리당 O(√N)의 시간이 걸린다

## 희소 테이블 알고리즘(Sparse table algorithm)

작성중...
