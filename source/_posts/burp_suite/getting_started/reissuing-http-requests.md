---
title: 使用 Burp Proxy 重复发送请求
date: 2023-03-02 01:22:10
updated: 2023-03-02 01:22:10
categories: Burp Suite
tags:
    - Burp Suite
description:
top_img: https://iili.io/HVEfKa1.jpg
cover: https://iili.io/HGl4Et1.png
---

> 原文地址: [Reissue requests with Burp Repeater](https://portswigger.net/burp/documentation/desktop/getting-started/reissuing-http-requests)

## 将请求发送到 Burp Repeater

### 定位一个感兴趣的请求

之前，我们的虚拟购物网站中，每一次访问一个商品页，浏览器都会发送一个带有 `productId` 参数的 `GET /product` 请求。

![商品详情页请求](https://iili.io/HVRtHG9.png)

### 将此请求发送到 Burp Repeater

在任意一个 `GET /product?productId=[...]` 请求上右键点击并选择 **Send to Repeater**

![将请求发送到 Burp Repeater](https://iili.io/HVRD0DQ.png)

### 发送请求并查看响应

在 **Repeater** 标签中点击 **Send** 发送请求，并查看服务器返回的响应。你想发送多少次就可以发送多少次每次的响应都会更新

![发送请求并查看响应](https://iili.io/HVRbdej.png)

## 使用 Burp Repeater 测试不同的输入

通过重复发送拥有不同输入的相同请求，可以确认基于输入的各种漏洞。

### 重新发送拥有不同输入的请求

更改 `productId` 参数的值，并重新发送请求。尝试几次，包括一些很大的数。

![productId 为 233 的响应](https://iili.io/HVRpuiN.png)

### 查看请求历史

![请求历史](https://iili.io/HVRyGpa.png)

### 输入非预期请求

服务器看起来似乎通过 `productId` 参数接收一个整数值。如果我们发送一个其他类型的数据会如何？

![productId 为 test 的响应](https://iili.io/HV5HhgI.png)

### 研究响应

发送一个非整型 `productId` 引发了一个异常。

注意到，响应告诉了我们网站在使用 Apache Struts 框架，甚至显示了版本号。

![异常显示了网站框架及其版本号](https://iili.io/HV5Jc42.png)

现实中，这种类型信息的泄漏对于攻击者是非常有用的，特别当前版本包含一些已知的漏洞。
