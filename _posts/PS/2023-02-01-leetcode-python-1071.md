---
title: "[Leetcode Python] 1071. Greatest Common Divisor of Strings"
excerpt: "Solve leetcode problem"

date: 2023-02-01
last_modified_at: 2023-02-01
---

# Problem site address

<a href="https://leetcode.com/problems/greatest-common-divisor-of-strings/description/" target="_blank">1071. Greatest Common Divisor of Strings</a>

```python
from math import lcm


class Solution:
    def gcdOfStrings(self, str1: str, str2: str) -> str:
        l1, l2 = len(str1), len(str2)
        gcd_length = l1 * l2 // lcm(l1, l2)
        gcd_str = str1[:gcd_length]
        if str1 == gcd_str * (l1 // gcd_length) and str2 == gcd_str * (l2 // gcd_length):
            return gcd_str
        return ""
```
