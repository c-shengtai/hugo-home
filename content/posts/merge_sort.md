---
title: "Merge Sort"
date: 2020-07-14T22:27:00+08:00
tags: [algorithm]
categories: [algorithm]
summary: "merge sort"
---

## Merge Sort

merge sort 是典型的使用分而治之(Divide and conquer)的方式執行的演算法，

它將各個元素分成最小塊在進行比較排序，然後再合併。例子如下

[4, 2, 5, 6]

[4, 2][5, 6]

[4][2][5][6]

[2, 4][5, 6]

[2, 4, 5, 6]

1. 將每個元素分離出來
2. 比較每個元素進行排序
3. 合併

```python
from math import floor


def merge_sort(arr):
    def merge_helper(arr1=[], arr2=[]):
        i, j = 0, 0
        result = []
        while i < len(arr1) and j < len(arr2):
            if (arr1[i] < arr2[j]):
                result.append(arr1[i])
                i += 1
            else:
                result.append(arr2[j])
                j += 1
        if i == len(arr1) and j < len(arr2):
            result.extend(arr2[j:])
        elif j == len(arr2) and i < len(arr1):
            result.extend(arr1[i:])
        return result

    if len(arr) <= 1:
        return arr

    mid = floor(len(arr) / 2)
    left = merge_sort(arr[0:mid])
    right = merge_sort(arr[mid:])
    return merge_helper(left, right)

print(merge_sort([2, 64, 12, 7, 9, -4]))

```

困難點在於`mid = floor(len(arr) / 2)` `left = merge_sort(arr[0:mid])` `right = merge_sort(arr[mid:])`
要寫成遞歸的方式需要思考較久
{{< figure src="/images/posts/merge_sort/merge_sort_recursive.png" >}}

## Time Complexity and Space Complexity

Big O(n \* log(n))

陣列長度為 8 需要分割 3 次

陣列長度為 32 需要分割 5 次

log(n)

每次分個的每個元素都需要進行比較，所以是 n

每個元素都會儲存成一個陣列，所以空間是 n

結論 Time O(n \* log(n)), Space O(n)
