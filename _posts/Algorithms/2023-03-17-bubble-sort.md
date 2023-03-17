---
title: "거품 정렬 이해하기"
excerpt: "거품 정렬(Bubble sort)에 대해 정리"

categories: algorithm
toc: true
toc_sticky: true
date: 2023-03-17
last_modified_at: 2023-03-17
---

<!-- TODO: 공간복잡도 내용 추가하기-->

### 거품 정렬(Bubble sort) 알고리즘

시간복잡도가 O(N ^ 2)이라 크기가 커질수록 매우 느려져서 진짜 특수한상황이 아니면 쓰면 안되는 알고리즘  
이에 대한 오바마 전 대통령의 재밌는 영상도 있다. [Youtube](https://www.youtube.com/watch?v=k4RRi_ntQc8)

이름의 유래는 원소들이 거품이 올라오는것처럼 보여서 거품정렬이라는데 솔직히 봐도 잘 모르겠다..

<div style='position:relative; padding-bottom:calc(50.00% + 44px)'><iframe src='https://gfycat.com/ifr/EqualPointlessIrishdraughthorse' frameborder='0' scrolling='no' width='100%' height='100%' style='position:absolute;top:0;left:0;' allowfullscreen></iframe></div><p> <a href="https://gfycat.com/equalpointlessirishdraughthorse">via Gfycat</a></p>

## 작동 원리

배열의 두 수(a, b)를 선택한뒤 정렬된상태인지 확인하고 정렬되어있지 않다면 두 수를 위치를 바꾼다 이때 정렬순서가 오름차순(a < b), 내림차순(a > b)인지에 따라  
정렬된상태의 조건이 변한다.

## Python

```python
# 배열을 오름차순으로 정렬하는 코드
def bubble_sort(arr: List[int]) -> List[int]:
    length = len(arr) - 1   # 두 원소를 비교하기 때문에 최대탐색 길이는 len(arr) - 1입니다
    for i in range(length):
        for j in range(length - i):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr
print(bubble_sort([4, 1, 3, 2, 5]))
```

## 시간 복잡도

시간복잡도는 원소가 1개씩 정렬될때마다 비교할 원소의 수가 1씩 작아지기때문에 (N - 1) + (N - 2) + (N - 3) + ... + 2 + 1 = (N \* (N - 1)) / 2 => O(N ^ 2)로 표시할수있다.

최악의 경우는 O(N ^ 2), 평균의 경우도 O(N ^ 2), 처음부터 정렬이 되어있는 최선의 경우여도 배열이 모두 정렬되어있는지 확인하는 작업을 하기때문에 O(N)이다.
