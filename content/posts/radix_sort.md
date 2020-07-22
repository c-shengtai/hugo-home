---
title: "Radix Sort"
date: 2020-07-22T20:56:25+08:00
summary: "about radix sort"
tags: [algorithm]
categories: [algorithm]
---

## Radix Sort

radix sort 是一個很有趣很特別的演算法，與其他排序也算法不同，他不使用數字比較大小的方式而是使用數字長度來排序。

假設有個陣列 `[123, 32, 2235, 255, 1]`

可以看出最長的數字是`2235` 它有 4 個數字，代表我們會重新排序 4 次，什麼意思呢？

想像我們有個編號 0-9 的盒子，先取每個數字的個位數，依序放到對應的盒子中，此時大概長這樣`[[], [1], [32], [123], [], [2235, 255], [], [], [], []]`

之後再將陣列按照順序取回來變成`[1, 32, 123, 2235, 255]`

再來換十位 `[[1], [], [123], [32, 2235], [], [255]]` 再依序取回 `[1, 123, 32, 2235, 255]`然後依此類推執行 4 次

如圖所示
{{< figure src="/images/posts/radix_sort/radix_sort.gif" >}}

## Code

```python
import math


def get_digits(num, place):
    return math.floor(num / math.pow(10, place)) % 10


def digit_count(num):
    if num == 0:
        return 1
    return math.floor(math.log10(num)) + 1


def most_digits(num_arr):
    max_digits = 0
    for i in num_arr:
        max_digits = max(digit_count(i), max_digits)
    return max_digits


def radix_sort(num_arr):
    max_digits = most_digits(num_arr)
    for k in range(max_digits):
        buckets = []
        new_arr = []
        for i in range(10):
            buckets.append([])

        for num in num_arr:
            digit = get_digits(num, k)
            buckets[digit].append(num)

        for bucket in buckets:
            if len(bucket):
                print(bucket)
                new_arr.extend(bucket)

        num_arr = new_arr
    return num_arr


radix_sort([123, 31, 2, 51, 5, 13677, 1])

```
