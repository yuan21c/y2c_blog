---
title: Burp Intruder 入门
date: 2023-03-02 23:30:42
updated: 2023-03-02 23:30:42
categories: Burp Suite
tags:
    - Burp Suite
description:
top_img: https://iili.io/HVEqFV4.jpg
cover: https://iili.io/HGl4Et1.png
---

> 原文地址: [Getting started with Burp Intruder](https://portswigger.net/burp/documentation/desktop/tools/intruder/getting-started)

## 接入实验室

访问下方地址：

```http
https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-different-responses
```

点击 **Access the lab** 进入实验室。

## 尝试登录

点击 **My account**， 然后使用一个无效的用户名和密码尝试登录。

![尝试登录](https://iili.io/HVMMFu1.png)

在 **Proxy > HTTP history** 找到 `POST /login` 请求，右键单击并选择 **Send to Intruder** 。

![发送给 Intruder](https://iili.io/HVM8xK7.png)

## 设置载荷位置

打开 **Intruder** 标签，Burp Intruder 自动在一些位置插入了 `§` 符号，这标记着载荷的开始位置和结束位置。Burp Intruder 会在攻击期间自动在这些位置插入载荷。

![载荷位置](https://iili.io/HVVv8zv.png)

在此例中，只需要 `username` 参数这一个载荷位置。点击 `Clear §` 清除默认位置。

选中 `username` 参数的值，然后单击 `Add §` 。

![设置载荷位置](https://iili.io/HVhuvBp.png)

## 设置攻击模式

在屏幕上方，将攻击模式设置为 **狙击手模式(Snipper)** 。

![设置攻击模式](https://iili.io/HVj2OOP.png)

## 添加载荷

配置一个你想要的载荷列表。在本例中，我们尝试发送不同的用户名去测试登录的运行机理。

候补用户名:

```username
carlos
root
admin
test
guest
info
adm
mysql
user
administrator
oracle
ftp
pi
puppet
ansible
ec2-user
vagrant
azureuser
academico
acceso
access
accounting
accounts
acid
activestat
ad
adam
adkit
admin
administracion
administrador
administrator
administrators
admins
ads
adserver
adsl
ae
af
affiliate
affiliates
afiliados
ag
agenda
agent
ai
aix
ajax
ak
akamai
al
alabama
alaska
albuquerque
alerts
alpha
alterwind
am
amarillo
americas
an
anaheim
analyzer
announce
announcements
antivirus
ao
ap
apache
apollo
app
app01
app1
apple
application
applications
apps
appserver
aq
ar
archie
arcsight
argentina
arizona
arkansas
arlington
as
as400
asia
asterix
at
athena
atlanta
atlas
att
au
auction
austin
auth
auto
autodiscover
```

* 打开 **Payloads** 标签页。
* 将 **Payload type** 设置为 **Simple list** 。
* 在 **Payload settings** 区域， 点击 **Paste** 以添加复制的用户名。
* 在 **Payload sets** 区域，可以看到添加的载荷的数量，以及会发送多少次攻击。

![添加载荷](https://iili.io/HVO9jLu.png)

## 开始攻击

在右上角点击 **Start attack** 开始攻击。Burp Intruder 会打开一个新的窗口。

![攻击](https://iili.io/HVvYiHG.png)

## 查找不同寻常的响应

攻击结束后，按照 **Length** 列排序，会发现有一个响应的长度与其他的不同。

![不同寻常的响应](https://iili.io/HVvcChl.png)

## 研究响应

通过研究多个响应发现，大部分都包含 `Invalid username` 的错误信息，但其中一个包含的错误信息是 `Incorrect password` 。这表明此用户名很有可能是有效的。

![可能的用户名](https://iili.io/HVUC6mP.png)

## 破解密码

使用相同的方法破解密码。

![破解密码](https://iili.io/HVgQ0yQ.png)
