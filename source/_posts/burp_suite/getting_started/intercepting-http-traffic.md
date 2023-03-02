---
title: 使用 Burp Proxy 拦截 HTTP 流量
date: 2023-03-01 23:45:15
updated: 2023-03-01 23:45:15
categories: Burp Suite
tags:
    - Burp Suite
description:
top_img: https://iili.io/HVEfKa1.jpg
cover: https://iili.io/HGl4Et1.png
---

> 原文地址: [Intercept HTTP traffic with Burp Proxy](https://portswigger.net/burp/documentation/desktop/getting-started/intercepting-http-traffic)

## 第一步: 启动 Burp 浏览器

打开 Proxy > Intercept 标签, 点击 `Open browser` 打开浏览器。

![启动 Burp 浏览器](https://iili.io/HGlPijS.png)

## 第二步: 拦截请求

尝试访问 `https://portswigger.net`, Burp Proxy 拦截了请求。可在 Proxy > Intercept 标签查看被拦截的请求。

![被拦截的请求](https://iili.io/HVR3jWJ.png)

## 第三步: 转发请求

点击 **Forward** 按钮以转发被拦截的请求。

## 第四步: 关闭拦截

当不想再拦截请求的时候，点击 **Itercept is on** 以关闭拦截。

![关闭拦截](https://iili.io/HVRFiTF.png)

## 第五步: 查看 HTTP 历史

打开 **Proxy > HTTP history** 标签，可以查看所有的 HTTP 流量，即使 拦截被关闭了。

![查看 HTTP 历史](https://iili.io/HVRKe9I.png)
