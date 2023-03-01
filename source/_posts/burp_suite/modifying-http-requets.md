---
title: 使用 Burp Proxy 修改 HTTP 请求
date: 2023-03-01 23:49:52
updated: 2023-03-01 23:49:52
categories: Burp Suite
tags:
    - Burp Suite
description:
top_img: https://iili.io/HGl4Et1.png
cover: https://iili.io/HGl4Et1.png
---

原文地址: [Modifying HTTP requests with Burp Proxy](https://portswigger.net/burp/documentation/desktop/getting-started/modifying-http-requests)

## 在 Burp 浏览器中访问网页

确保关闭拦截，启动 Burp 浏览器请访问下面的网址:

```http
https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-excessive-trust-in-client-side-controls
```

点击 **Access the lab** 进入购物网站。

![购物网站](https://iili.io/HVRuqkG.png)

## 登录你的网站账号

点击 **My account** 使用以下的身份登录:

用户名: `wiener`
密码: `peter`

![My Account](https://iili.io/HVRRRbj.png)

## 购物

在 Home 页点击商品 **Lightweight "l33t" leather jacket** 进入详情页。

## 研究添加购物车方法

在 Burp 中，在 **Proxy > Intercept** 打开拦截。然后在浏览器中点击 **Add to cart** 将商品添加至购物车，拦截 `POST /cast` 请求。

![拦截请求](https://iili.io/HVRYkrB.png)

研究此拦截的方法，发现有一个 `price` 参数正好和页面中的价格相同。

## 修改请求

将 `price` 参数的值修改为 1 , 点击 **Forward** 将修改后的请求发送给服务器。

![修改请求](https://iili.io/HVRcXix.png)

## 利用此漏洞

在购物车中可以看到，商品的价格变为了 $0.01.
