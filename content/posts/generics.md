---
title: "泛型"
date: 2020-06-24T12:40:35+08:00
draft: false
tags: [programing]
categories: [programming]
summary: "about generics"
---

## Why is generics

> 在談論泛型之前先瞭解為何我們需要泛型

首先來看 function 是如何重複使用的

假設有個需求某一個人會說 hello, 你好, Yo，我們可寫成 3 個 function

```typescript
function sayHello(person: string): string {
  return `${person}: hello`;
}

function sayHelloTW(person: string): string {
  return `${person}: 你好`;
}

function sayYo(person: string): string {
  return `${person}: Yo`;
}
```

這樣確實可以滿足需求，但若是這個人需要說更多的話，我們就必須建立更多的 function，所以一般會建立可重複使用的 function 然後傳入參數，看要說什麼都可以用一個 function 來解決需求。

```typescript
function say(person: string, words: string): string {
  return `${person}: ${words}`;
}
```

現在假設需要建立一個 class，可能某個 data 會是 number, string, boolean 這些可能，會寫成 3 個 class

```typescript
class HoledNumber {
  constructor(public data: number) {}
}

class HoledString {
  constructor(public data: string) {}
}

class HoledBoolean {
  constructor(public data: boolean) {}
}
```

當然這一定是不好的寫法，現在我們需求出來了，我們希望可以類似使用 function 參數的方式傳入型別，讓一個 class 就可以完成所有的事情。

**而這就是泛型(Generics)的工作**。

## What is generics

如前面所述，泛型類似於 function 的參數，它可以讓我們的 code reuse 更容易的維護與使用。

```typescript
class HoledAny<TypeOfData> {
  constructor(public data: TypeOfData) {}
}
```

這樣一個 class 就可以達成我們的目的了
