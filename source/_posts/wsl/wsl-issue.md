---
title: WSL2 kali win-kex 报错
date: 2023-02-19 11:15:55
updated: 2023-02-19 11:15:55
categories: wsl
tags:
    - wsl
    - kex
    - win-kex
description: 
top_img: https://iili.io/iJ2mSp.jpg
cover: https://iili.io/iJ2mSp.jpg
---

WSL2 Kali Linux 在启动 `kex` 时报如下错误:

> failed to connect to "127.0.0.1"
>
> unable to connect to socke: 由于目标计算机积极拒绝，无法连接（10061）

解决方法:

```bash
sudo mount -o remount,rw /tmp/.X11-unix
```

原文地址:

* [Github - kex unable to connect to socket: connection refused(10061)](https://github.com/microsoft/WSL/discussions/6675#discussioncomment-5012927)

* [Github - /tmp/.X11-unix is being mounted read-only](https://github.com/microsoft/WSL/issues/9303#issuecomment-1345615675)
