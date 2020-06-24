---
title: "時間與空間複雜度(Big O Notation)"
date: 2020-06-23T23:25:06+08:00
draft: false
tags: [algorithm]
categories: [algorithm]
summary: "About Big O Notation"
---

## Why is Big O

> 在談論 Big O 之前，先瞭解我們為何需要 Big O

當我們程式在執行程式時，我們該如何代表我們程式執行的效率呢?  
最直覺的方法可能是使用**時間**來計時，在 js 中可能可以使用`performance.now()`

```js
const startTime = performance.now();
doSomething();
const endTime = performance.now();

console.log(`doSomething執行了${startTime - endTime}`); // 印出執行的時間
```

但這樣做有許多不確定的因素

1. 每台電腦設備配置皆不相同，執行速度當然會不同
2. 相同電腦每次執行的速度也會略有所不同

---

所以在這種情況下使用執行的時間來判斷程式的效能是不聰明的作法，所以我們使用**Big O**來代表演算法的執行效率。

## What is Big O

如前面所述我們無法單看執行的時間來判斷演算法的效率，時間會被硬體等因素限制，導致無法準確的判斷出該程式的效能。

而 **Big O 只考慮演算法的執行效率，並不會被其它的因素所影響。**

它只考慮執行最糟糕的狀態，常數與其他非最大的數影響不大，並不是最大的影響因子，所以將它省略，只著重最大的數。

- 去掉所有的常數
- 只取最大數

例如某一程式的執行速度是 5n^2+4n+3，在考慮最糟糕的情況下，若 n 是某一非常大的數那對比起來其它的常數對它的影響是可以忽略不計的。  
例如當 n 是 1 兆，那麼 3 和 4\*1 兆 兆對比 5\*1 兆^2 的平方來說真的非常的小，而前面的\*5 也不是影響程式效能的主要因素。

所以我們可以說該程式的時間複雜度是 **Big O(n^2)**

## 時間複雜度

> 時間複雜度表一演算法所執行的時間

可以看到下方的`countAll()`的函數，假設 array 的長度是 n，那麼此程式運算子"+"必須執行 n 次，可以判斷出 Big O(n)。

```python
def countAll(array):
  total = 0
  for i in array:
    total += i
  return total
```

再來是此下方程式可以看出當 length = n，運算子"\*"必須執行 n^2 次，所以可以表示 Big O(n^2)

```python
def doSomething(length):
  for i in range(length):
    for j in range(length):
      print(i * j)
```

該程式無論 n 給多少，最多就是執行 5 次，所以 Big O(1)

```python
def countMost5Times(n):
  for i in range(min(n, 5)):
    print(i)

```

時間複雜度的執行效率可以參考下圖

{{< figure src="/images/posts/time_space_complexity/time_complexity.svg" >}}

## 空間複雜度

> 空間複雜度表示一演算法所佔用的空間，通常不考慮初始輸入值

可以簡單地從"="來做出判斷

下方的程式`total = 0`可以算 1 次，可以注意下+=並不算重新佔用空間，還是 total 此變數的空間，所以該程式的空間複雜度 Big O(1) space

```python
def countAll(array):
  total = 0
  for i in array:
    total += i
  return total
```

若是 array 賦值就要考量到 array 的長度了

array 每元素佔用的空間是不同的，所以空間複雜度是 Big O(n)

```python
def doSomething(length):
  arr = []
  for i in range(length):
    arr[i] = 1
```
