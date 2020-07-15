---
title: "常用的Python OS 模組"
date: 2020-07-09T22:57:01+08:00
tags: ["python", "os", "module", "standard library"]
categories: [python]
summary: "python os"
---

## 路徑

### 建立跨 os 的路徑

`os.path.join()`

```python
import os
os.path.join('usr', 'bin')
# linux or mac output 'usr/bin'
# windows 'usr\\bin'
```

### 目前的目錄

`os.getcwd()`

```python
os.getcwd()
# /Users/APPLE
```

### 建立資料夾

`os.makedirs()`

```python
os.makedirs('/Users/APPLE/123/test')
# 若沒有123的資料夾也會一併建立
```

### 相對路徑轉絕對路徑

`os.path.abspath()`

```python
os.path.abspath('.')
# '/private/tmp'
```

### 確認是否是相對位子

`os.path.isabs(path)`

```python
os.path.isabs('.')
# False
```

### 回傳相對路徑

`os.path.relpath(path, start='./')`

```python
os.path.relpath('/', './)
# ../..
```

### 分割 Path

- 分割目錄與名稱

`os.path.basename(path)`
`os.path.dirname(path)`
`os.path.split(path)`

```python
path = '/tmp/com.google.Keystone/.keystone_install_lock'
os.path.basename(path) # '.keystone_install_lock'
os.path.dirname(path) # '/tmp/com.google.Keystone'
os.path.split(path) # ('/tmp/com.google.Keystone', '.keystone_install_lock')
```

- 分割每個路徑

使用字串`split` method 與 `os.path.sep`得到 os 的分割線

```python
path.split(os.path.sep)
# ['', 'tmp', 'com.google.Keystone', '.keystone_install_lock']
```

## 檔案與資料夾

### 檔案大小

`os.path.getsize(path)`

```python
os.path.getsize('./test/txt')
# 5
```

### ls

`os.listdir(path='./')`

```python
os.listdir()
# ['com.apple.launchd.NzQy05oBUn', 'com.google.Keystone', 'test.text', 'powerlog', '.vbox-sheng-tai-ipc', 'test.txt']
```

### 檔案或資料夾是否存在

`os.path.exits(path)`

```python
os.path.exits('/tmp') # True
```

### 是否為檔案

`os.path.isfile(path)`

```python
os.path.isfile('/tmp') # False
```

### 是否為資料夾

`os.path.isdir(path)`

```python
os.path.isdir('/tmp') # True
```
