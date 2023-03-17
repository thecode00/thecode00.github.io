---
title: "선택 정렬 이해하기"
excerpt: "선택 정렬(Selection sort)에 대해 정리"

categories: algorithm
toc: true
toc_sticky: true
date: 2023-03-18
last_modified_at: 2023-03-18
---

### 선택 정렬(Selection sort) 알고리즘

## 작동 원리

배열의 첫번째 원소부터 끝까지 훑어본다음 가장 작은값을 첫번째에 둔다, 그다음은 두번째부터 시작해서 작은값을 두번째위치에 다음은 세번째...  
이걸 총 N - 1번반복한다.

선택 정렬이 어떤방식으로 작동하는지 보여주는 애니메이션:

<div style='position:relative; padding-bottom:calc(50.00% + 44px)'><iframe src='https://gfycat.com/ifr/ShallowHideousFruitbat' frameborder='0' scrolling='no' width='100%' height='100%' style='position:absolute;top:0;left:0;' allowfullscreen></iframe></div>

## Python

```python
def selection_sort(arr: List[int]) -> List[int]:
    length = len(arr)
    for i in range(length - 1):
        min_index = i   # 최소값을 가진 원소의 인덱스
        for j in range(i, length):
            if arr[j] < arr[min_index]:
                min_index = j
        arr[i], arr[min_index] = arr[min_index], arr[i] # 탐색이 끝난후 최소값을 가진 원소를 맨 앞으로 보냄
    return arr
print(selection_sort([4, 1, 2, 3, 5]))
```

## 시간 복잡도

처음에 끝까지 탐색을 하고 그다음 탐색범위가 1개씩 줄어들기 때문에 N + (N - 1) + (N - 2) + ... + 2 + 1로 볼수있습니다.  
위의 코드는 남은원소가 2개면 정렬을 멈추므로 + 2까지만 계산해야하지만 1차이가 컴퓨터상에서는 무시해도될정도로 작기 때문에 그냥 보기 편하려고 넣었습니다.

<iframe src="https://giphy.com/embed/xhKdtuT56I3HNUpgOY" width="480" height="480" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/HBOMax-romance-hbomax-made-for-love-xhKdtuT56I3HNUpgOY">via GIPHY</a></p>

최악의 경우에는 O(N ^ 2), 평균도 O(N ^ 2), 최선의 경우도 O(N ^ 2)인 일관성있는 알고리즘
