---
title: 'Docker (一)'
date: 2020-09-01T22:04:47+08:00
summary: '介紹基本的Docker'
tags: ['docker']
---

## 關於 Docker

> 簡單介紹關於 Docker 這項技術的應用與傳統的區別

### 為何使用 Docker

在軟體的世界中時常發生在開發者的電腦中可以正常的執行，但在生產端卻發生不可預期的錯誤，造成此原因可能是生產環境中與開發環境不同(OS、版本、套件互相依賴等)，在以前會使用 virtual box 或 vm ware 建立 virtual machine，盡可能地將開發環境與生產環境的配置一致，但使用 virtual machine 卻非常地吃資源，建立乾淨的環境也非常的麻煩，Docker 可以使用簡單的方法解決這些問題。

### Docker 與 傳統的 Virtual Box 或 VM Ware 有何不同

首先先講 Virtual Box 與 VM Ware， 傳統的方式是透過虛擬化硬體在其上建立一套 OS 的系統，在使用該 OS 系統在上面執行程式。

Docker 則是利用 Docker engine 建立 Container，區別在於 Docker 並不會建立虛擬化硬體，而是直接透過本地電腦的作業系統去執行，相比來更輕量。

### Docker 的應用

因為 Docker 非常的輕便且易於擴展(一台 server 可以跑上百個至上千個 container)，所以時常用於微服務([何謂微服務](https://zh.wikipedia.org/wiki/%E5%BE%AE%E6%9C%8D%E5%8B%99))中，將每個 container 都跑各自的應用程式。

## Docker 基礎操作

可以使用 `docker info` 來顯示 docker 的基本訊息、版本等資訊
{{< figure src="/images/posts/docker/docker-info.png" >}}
運行 `docker run -i -t /bin/bash`，會先確認在 local 端是否有 ubuntu 的 image 後，如果有就不會從 docker hub 上下載下來，若沒有就會下載下來並執行。其中`-i`代表建立輸入, `-t`表示建立 tty 的終端機。

之後就可以像在一般的 linux 操作環境一樣執行 ubuntu。
{{< figure src="/images/posts/docker/docker-run-ubuntu.png" >}}

在其中**f3ca77473072**代表這容器的 id，若想替容器命名可以加上`--name [名稱]`即可，例如`docker run --name test_name -i -t ubuntu /bin/bash`打完後可以輸入`docker ps -a`會印出所有執行過的容器。
{{< figure src="/images/posts/docker/docker-ps-and-docker-name.png" >}}
可以看到容器有被正確的命名**test_name**。

若想要重新啟動**test_name**這個容器，可以輸入`docker start test_name`或是輸入 id`docker start 1c0e64e8bda6`都可以重新啟動容器。
{{< figure src="/images/posts/docker/docker-start.png" >}}

要確認是否有重新建立成功，輸入`docker ps`印出所有正在執行的容器。
{{< figure src="/images/posts/docker/docker-start-and-ps.png" >}}

若想要再重新進去**test_name**容器的 bash，輸入`docker attach test_name`，一樣輸入 id 也會有相同的效果`docker attach 1c0e64e8bda6`。
{{< figure src="/images/posts/docker/docker-attach.png" >}}
docker 不只可以創建類似**test_name**這種交互操作的容器(interactive container)，也可以創建一直在後台的執行容器(daemonized container)，大多數的 server 都是如此。

執行`docker run --name centos-linux -d centos /bin/sh -c "while true; do ping google.com; done"`
{{< figure src="/images/posts/docker/docker-daemon-container.png" >}}
可以看見容器仍正在執行，`-d`代表程序在後台執行。

若要觀看執行的內容可以輸入`docker logs centos-linux`
{{< figure src="/images/posts/docker/docker-logs.png" >}}
可以加上`-ft`會持續查看且加上時間。
{{< figure src="/images/posts/docker/docker-logs-ft.png" >}}
`docker stats centos-linux`可以查看 container 的執行狀態
{{< figure src="/images/posts/docker/docker-stats.png" >}}
若要停止容器可以使用`docker stop [name||id]`或`docker kill [name||id]`，2 者區別在於 kill 會強制停止程式。
{{< figure src="/images/posts/docker/docker-kill.png" >}}
最後若要刪除容器可以使用`docker rm [name||id]`
{{< figure src="/images/posts/docker/docker-rm.png" >}}
要刪除全部的 container

```bash
docker rm `docker ps -a -q`
```

{{< figure src="/images/posts/docker/docker-rm-a.png" >}}
`-q`代表只回傳 id

## Summary

```bash
docker info # show docker info
docker run [image-name] [--name 'name'] [-i,-t,-d] # 建立容器, -i stdin, -t tty, -d daemon, --name alias
docker stop [name||id] # 停止容器
docker kill [name||id] # 強制中斷容器
docker logs [name||id] # 查看執行結果
docker attach [name||id] # 進入交互介面
docker stats [name||id] # 查看容器執行狀態
docker ps [-a, -q] # 查看正在執行的容器 -a 所有容器, -q 只回傳id
```
