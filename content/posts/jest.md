---
title: "Jest"
date: 2020-07-27T22:39:02+08:00
---

## Jest

facebook 建立的測試 library

## 安裝

使用`npm install jest`

## 使用

- 同步

```javascript
const db = ["cates.com", "dogs.com", "cutedogs.com", "abc.com", "cctv.com"];

const search = (searchInput, db) => {
  const matches = db.filter((web) => {
    return web.includes(searchInput);
  });

  return matches.length > 3 ? matches.slice(0, 3) : matches;
};

describe("search", () => {
  it("search test", () => {
    expect(search("test", db)).toEqual([]);
    expect(search("dog", db)).toEqual(["dogs.com", "cutedogs.com"]);
  });

  it("test undefined and null", () => {
    expect(search(null, db)).toEqual([]);
    expect(search(undefined, db)).toEqual([]);
  });
});
```

- 非同步

測試偶爾會出現相依其他 function 的問題，此時主要要測試的 function 稱為 SUT(system under test)和 DOC(depended-on component),
過多的非同步測試會導致測試效能降低,等待許久的時間。

此時可以使用 mock 來代替 DOC, mock 類似一個替身,回傳類似相同的假資料來取代 DOC function 等。

```javascript
const fetch = require("node-fetch");

const getRequest = async (fetch) => {
  const res = await fetch("https://swapi.dev/api/people");
  const data = await res.json();

  return {
    count: data.count,
    results: data.results,
  };
};

const fetch = require("node-fetch");

it("async test", () => {
  expect.assertions(1);
  return getRequest(fetch).then((data) => {
    expect(data.count).toEqual(82);
  });
});

it("mock function", () => {
  const mockFunction = jest.fn().mockReturnValue(
    Promise.resolve({
      json: () =>
        Promise.resolve({
          count: 82,
          results: [0, 1, 2, 3, 4, 5],
        }),
    })
  );

  expect.assertions(3);
  return getRequest(mockFunction).then((data) => {
    expect(mockFunction.mock.calls.length).toEqual(1);
    expect(data.count).toEqual(82);
    expect(data.results.length).toBeGreaterThan(5);
  });
});
```

## Ref

- [Jest cheat sheet](https://github.com/sapegin/jest-cheat-sheet)
- [Jest - 神 Q 超人](https://medium.com/enjoy-life-enjoy-coding/jest-jojo%E6%98%AF%E4%BD%A0-%E6%88%91%E7%9A%84%E6%9B%BF%E8%BA%AB%E8%83%BD%E5%8A%9B%E6%98%AF-mock-4de73596ea6e)
