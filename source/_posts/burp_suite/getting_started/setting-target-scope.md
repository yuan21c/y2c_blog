---
title: 设置目标范围
date: 2023-03-02 00:31:01
updated: 2023-03-02 00:31:01
categories: Burp Suite
tags:
    - Burp Suite
description: 
top_img: https://iili.io/HVEfKa1.jpg
cover: https://iili.io/HGl4Et1.png
---

> 原文地址: [Set the target scope](https://portswigger.net/burp/documentation/desktop/getting-started/setting-target-scope)

## 启动 Burp 浏览器

启动 Burp 浏览器并访问下面的地址:

```http
https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-in-error-messages
```

点击 **Access the lab** 进入购物网站。

## 浏览目标网页

在浏览器中随意浏览一些商品页。

## 研究 HTTP 历史

打开 Burp 的 **Proxy > HTTP history** 标签。为了便于阅读，将最左边的列按降序排列。这样就可以在上面看到最近的请求。

![HTTP history](https://iili.io/HVRWxZ7.png)

注意到，浏览器的每一次请求都在这里显示出来了。包括一些你不感兴趣的第三方网站的请求，比如 Youtube 和 Google Analytics 。

## 设置目标范围

在 **Target > Site map** 标签的左侧面板中你可以看到所有浏览器通信过的主机，在你需要选择的目标站点上右键并选择 **Add to scope** 。

![设置目标范围](https://iili.io/HVRht3u.png)

## 过滤 HTTP 历史

点击 HTTP history 上面的过滤器, 并选择 **Show only in-scope items** 。

![过滤 HTTP 历史](https://iili.io/HVRNsCN.png)

现在 HTTP 历史中，只显示目标网站。如果你继续浏览目标网页，你就会发现目标范围外的流量不再被记录。

![只显示目标网站](https://iili.io/HVReigt.png)