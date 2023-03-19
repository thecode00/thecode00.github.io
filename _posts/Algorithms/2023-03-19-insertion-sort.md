---
title: "삽입 정렬 이해하기"
excerpt: "삽입 정렬(Insertion sort)에 대해 정리"

categories: algorithm
toc: true
toc_sticky: true
date: 2023-03-19
last_modified_at: 2023-03-19
---

### 삽입 정렬(Insertion sort) 알고리즘

## 작동 방식

두번째 부터 시작해서 선택한 원소의 왼쪽 원소들을 탐색하면서 적절한 위치에 원소를 배치함

<div style='position:relative; padding-bottom:calc(100.00% + 44px)'><iframe src='https://gfycat.com/ifr/CornyThickGordonsetter' frameborder='0' scrolling='no' width='100%' height='100%' style='position:absolute;top:0;left:0;' allowfullscreen></iframe></div><p> <a href="https://gfycat.com/cornythickgordonsetter">via Gfycat</a></p>

## Python

```python
def insertion_sort(arr: List[int]) -> List[int]:
    length = len(arr)
    for i in range(1, length):
        for j in range(i - 1, -1, -1):  # 현재 선택한 원소의 왼쪽을 탐색
            if arr[j] < arr[j + 1]:
                break
            arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr
print(insertion_sort([3, 1, 4, 5, 2]))
```

## 시간 복잡도

최악의 경우과 평균의 경우에는 (N - 1) + (N - 2) + ... + 2 + 1 => (N \* (N - 1)) / 2 => O(N ^ 2)를 가진다.  
하지만 최선의 경우(모두 정렬되어있는 경우)에는 각 원소를 1번씩만 비교하므로 O(N)을 가진다.
