---
title: "Sliding Window"
date: 2020-07-04T21:13:16+08:00
tags: [algorithm]
categories: [algorithm]
summary: "about sliding window pattern"
---

直接從範例來理解，假設有一組數字 [12, 2, 54, 17, 18, 25, 9]，現在我們有個目標是希望找到 3 個連續加起來最大的數字。

在例子中可以顯而易見的最大是[54, 17, 18] 這三個加起來的數字。

那麼在程式中我們會如何達成呢？

- 這是一般常見的解法，使用雙重 for loop 來一個個加總比大小

```javascript
function normalSolution(digits, num) {
  if (digits.length < num) return;

  let maxCount = -Infinity;

  for (let i = 0; i < digits.length - num + 1; i += 1) {
    let tempCount = 0;

    for (let j = i; j < i + num; j += 1) {
      tempCount += digits[j];
    }

    maxCount = maxCount < tempCount ? tempCount : maxCount;
  }

  return maxCount;
}
```

- 這是 sliding window 的解法

```javascript
function slidingWindow(digits, num) {
  if (digits.length < num) return null;

  let maxCount = -Infinity;
  let tempCount = 0;

  for (let i = 0; i < num; i += 1) {
    tempCount += digits[i];
  }

  maxCount = tempCount;

  for (let i = num; i < digits.length; i += 1) {
    tempCount = tempCount - digits[i - num] + digits[i];
    maxCount = tempCount > maxCount ? tempCount : maxCount;
  }

  return maxCount;
}
```

可以看出從 O(n^2) -> O(n)效率提升許多

它的邏輯是這樣的

它將原本加總完的數保存，之後每次位移加後面一位,減前面一位

**12, 2, 54**, 17, 18, 25, 9 (12+2+54) = n

12, **2, 54, 17**, 18, 25, 9 (n-12+17) = n

12, 2, **54, 17, 18**, 25, 9 (n-2+18) = n

依序以此類推下去，將整群相對的位移這就是 Sliding Window ，常用於陣列或字串上。
