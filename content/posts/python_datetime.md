---
title: 'Python常用的時間'
date: 2020-08-26T21:40:25+08:00
draft: false
---

## 現在

`datetime.today(tz=None)`, `datetime.now()`
2 只區別在於 now() 可以設定 timezone

```python
from datetime import datetime

datetime.today() # datetime.datetime(2020, 8, 26, 21, 42, 33, 228739)
datetime.now() # datetime.datetime(2020, 8, 26, 21, 42, 40, 284184)

datetime.today().date() # get now date without time
datetime.today().time() # get now time without date
```

## 字串轉時間 ＆ 時間轉字串

`datetime.strptime(date_string, format)`, `datetime.strftime(format)`

```python
from datetime import datetime

datetime.strptime('2020/08/12', '%Y/%m/%d') # datetime.datetime(2020, 8, 12, 0, 0)
datetime.now().strftime('%Y/%m/%d') # '2020/08/26'
```

| 參數 |                  描述                   |                  範例                  |
| :--- | :-------------------------------------: | :------------------------------------: |
| %a   |               星期幾縮寫                |        Sun, Mon, …, Sat (en_US)        |
| %A   |             星期幾完整名稱              |  Sunday, Monday, …, Saturday (en_US)   |
| %w   | 星期幾使用數字表示 0=sunday, 6=saturday |          0, 1, 2, 3, 4, 5, 6           |
| %d   |               幾號 2 位數               |             01, 02, …, 31              |
| %b   |                 月縮寫                  |        Jan, Feb, …, Dec (en_US)        |
| %B   |               月完整名稱                | January, February, …, December (en_US) |
| %m   |                月 2 位數                |              01, 02 … 12               |
| %y   |                年 2 位數                |              01, 02, … 99              |
| %Y   |                年 4 位數                |          0001, 0002, … , 9999          |
| %H   |                 時(24h)                 |             01, 02, … , 23             |
| %I   |                 時(12h)                 |             01, 02, … , 12             |
| %p   |                pm or am                 |                 AM, PM                 |
| %M   |                   分                    |             01, 02, … , 59             |
| %S   |                   秒                    |             01, 02, … , 59             |
| %z   |               UTC offset                |      empty), +0000, -0400, +1030       |
| %Z   |             time zone name              |             UTC, IST, CST              |
| %j   |              一年的第幾天               |            001, 002, …, 366            |
| %U   |        一年的第幾週,週日為起始 0        |             00, 01, …, 53              |
| %W   |        一年的第幾週,週一為起始 0        |             00, 01, …, 53              |
| %c   |       當地時間表示法,date & time        |        Tue Aug 16 21:30:00 1988        |
| %x   |           當地時間表示法,date           |   08/16/88 (None) 08/16/1988 (en_US)   |
| %X   |           當地時間表示法,time           |            21:30:00 (en_US)            |

## 時間差

`datetime.timedelta(days=0, seconds=0, microseconds=0, milliseconds=0, minutes=0, hours=0, weeks=0)`

```python
from datetime import datetime, timedelta

datetime.now() - timedelta(days=12) # datetime.datetime(2020, 8, 14, 22, 24, 47, 788886)
```
