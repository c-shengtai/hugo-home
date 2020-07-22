---
title: "Quick Sort"
date: 2020-07-18T18:12:04+08:00
summary: "about quick sort"
---

## Quick Sort

也是使用 Divide and conquer 的方法，每次結束時會有一個元素擺在正確的位置上，小於它的在左、大於在右，直到找不到為止。

{{< figure src="/images/posts/quick_sort/quick_sort.gif" >}}

```python
def pivot_helper(arr, start=0, end=None):
    if end is None:
        end = len(arr)
    pivot_index = start
    for i in range(start + 1, end):
        if arr[i] < arr[start]:
            pivot_index += 1
            arr[i], arr[pivot_index] = arr[pivot_index], arr[i]
    arr[start], arr[pivot_index] = arr[pivot_index], arr[start]
    return pivot_index


def quick_sort(arr, left=0, right=None):
    if right is None:
        right = len(arr)
    if left < right:
        pivot_index = pivot_helper(arr, left, right)
        quick_sort(arr, left, pivot_index)
        quick_sort(arr, pivot_index + 1, right)
    return arr

```

需要注意的是並不是產生新的陣列，而是在相同的陣列下執行排序，遞迴的部分也需要想一下。

## Time Complexity and Space Complexity

最好的情況下是 O(n \* logn), 最糟是每次都選到最大或最小的數 O(n^2)

最好的情況是分解時 logn 次比較 n 次所以是 n\*logn

最糟的情況下每次都需要分解例如已排序的陣列(可以透過隨機取 start 來解決)n \* n

space O(logn)
