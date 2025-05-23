---
title: "순환 연결리스트의 루프 시작 노드를 찾는 수학적 증명"
toc: true
toc_sticky: true
date: 2025-04-21
last_modified_at: 2025-04-21
---

# 개요

순환 연결리스트가 주어졌을 때 루프의 시작 노드를 찾는 문제를 풀고 있었습니다.

처음에는 해시를 이용해 문제를 해결했지만, 더 효율적인 알고리즘이 있다는 걸 알게 되었습니다.  
작동만 확인하고 넘어가지 않고, 이 알고리즘이 **왜** 동작하는지에 대한 수학적 증명을 기록하고 싶어 이 글을 작성했습니다..

# 알고리즘

이 문제를 해결하는 알고리즘은 다음과 같습니다:

1. `slow`와 `fast`라는 두 포인터를 순환 연결리스트의 첫 번째 노드를 가리키게 합니다.
2. **토끼와 거북이 알고리즘**(fast-slow pointer)을 사용하여, 두 포인터가 만날 때까지 이동시킵니다. (`slow`: 1칸, `fast`: 2칸)
3. 만난 이후 `slow`를 다시 연결리스트의 시작 노드로 되돌립니다.
4. `slow`와 `fast`를 1칸씩 이동시키며, 두 포인터가 다시 만나는 노드가 루프의 시작 노드입니다.

# 수학적 증명

## 궁금증

이 알고리즘을 처음 봤을 때 두 가지 의문이 들었습니다:

1. **slow와 fast가 반드시 만날 수 있을까?**
2. **두 번째 만난 지점이 왜 루프의 시작 노드일까?**

---

## 1. slow와 fast가 반드시 만나는 이유

slow와 fast 포인터가 루프 안에 들어왔다고 가정합니다.  
만약 두 포인터가 절대로 만나지 않는다고 가정하면, 모순이 발생합니다.

- `slow`는 한 번에 1칸씩, `fast`는 2칸씩 이동합니다.
- `fast`가 `slow`를 계속해서 지나치면서 만나지 않으려면, 매번 지나치는 시점마다 `fast = slow + 1`이어야 합니다.
- 그런데 그 이전 단계에서는 `slow = i - 1`, `fast = i + 1 - 2 = i - 1`이 됩니다.
- 즉, `slow`와 `fast`가 같은 위치에 있게 되고, **결국 만나게 됩니다.**

따라서 **루프가 있다면 언젠가는 반드시 만납니다.**

---

## 2. 두 번째 만난 지점이 루프의 시작 노드인 이유

### 전제

- 연결리스트의 시작부터 루프의 시작 노드까지의 거리: `k`
- 루프의 길이: `L` (`loop_length`)
- 처음 만난 지점에서 `slow`를 시작 노드로 되돌립니다.

### slow가 루프 시작 노드에 도착했을 때

- `slow`는 `k`만큼 이동했고 루프의 시작 노드에 도착했습니다.
- `fast`는 `2k`만큼 이동했고 루프 내에서 `k`만큼 이동했습니다. 루프는 원이기 때문에 루프 시작 노드에서 `L - k`만큼 뒤에 있다고 볼수도 있습니다.

### 첫 번째 충돌 시

- `slow`는 1칸씩 `fast`는 2칸씩 이동하기 때문에 1번 이동할때마다 `fast`가 `slow`에 1칸씩 가까워집니다.
- `fast`는 `slow(루프 시작 노드)`에서 `L - k`만큼 뒤에 있습니다. 그래서 `fast`와 `slow`가 만나기 위해선 `L - k`번 이동해야 합니다.
- 첫 번째 충돌 지점은 루프의 시작 노드에서 `L - k`만큼 이동해야하는 곳에 위치합니다.

이제 slow를 시작 지점으로 되돌리고, 두 포인터 모두 1칸(매우 중요!)씩 이동합니다.

- `slow`: 시작부터 `k`칸 이동 → 루프의 시작 노드 도달
- `fast`: 충돌 지점에서 `k`칸 더 이동 → **루프 한 바퀴 돌아서 루프 시작 노드 도달**`(L - k) + k`

결과적으로 **두 포인터는 루프의 시작 노드에서 만나게 됩니다.**
