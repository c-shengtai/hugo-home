---
title: "Basic Sort"
date: 2020-07-12T22:29:39+08:00
tags: [algorithm]
categories: [algorithm]
summary: "about bubble sort, insertion sort and insertion sort"
---

## Bubble Sort

> 氣泡排序，在數值接近已完成排序時 O(n), 最糟 O(n^2)

`[8, 1, 2, 3, 4, 5, 6, 7]`取 0 和 1 比較，之後 1 和 2，3 和 4...第一輪排序完後最大的數已經確認在最後 1 位，再從 0, 1 比較

若確認在這次的循環內並無交換，則可確定已經排序完成

{{< figure src="/images/posts/basic_sort/bubble_sort.gif" >}}

```python
def bubble_sort(arr):
    is_swap = False
    for i in range(len(arr) - 1, -1, -1):
        is_swap = False
        for j in range(i):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                is_swap = True
        if (not is_swap):
            break
    return arr


print(bubble_sort([8, 1, 2, 3, 4, 5, 6, 7]))

```

## Selection Sort

> 選擇排序，在數值接近已完成排序時 O(n), 最糟 O(n^2)

選擇最小的與所有比較，進行排序

{{< figure src="/images/posts/basic_sort/selection_sort.gif" >}}

```python
def selection_sort(arr):
    for i in range(len(arr)):
        min_index = i
        for j in range(i, len(arr)):
            if arr[min_index] > arr[j]:
                min_index = j
        if i == min_index:
            continue
        arr[i], arr[min_index] = arr[min_index], arr[i]
    return arr


print(selection_sort([1, 2, 12, 42, 52, 34, 66, 19, - 3]))

```

## Insertion Sort

> 插入排序，在最好與最糟 O(n^2)，如果有資料不停的進來，你必須將它一直排序的話，可以考慮使用此方法

從第二個元素與前面比較，叫小則繼續往前，較大就插入

{{< figure src="/images/posts/basic_sort/insertion_sort.gif" >}}

```python
def insertion_sort(arr):
    for i in range(1, len(arr)):
        current_val = arr[i]
        for j in range(i-1, -1, -1):
            if current_val < arr[j]:
                arr[j+1] = arr[j]
            if current_val > arr[j]:
                arr[j + 1] = current_val
                break
            if current_val < arr[j] and j == 0:
                arr[j] = current_val
    return arr


print(insertion_sort([4, 24, 5, 12, 76, 32, -5]))

# i = 1, j = 0, cur = arr[i] = 24, [4, 24, ....]
# i = 2, j = 1, cur = arr[i] = 5, [4,24,24]
# i = 2, j = 0, cur = arr[i] = 5, [4, 5, 24]

```
