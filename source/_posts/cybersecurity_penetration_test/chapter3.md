---
title: 第3章 信息收集原理与实践
date: 2023-03-04 03:56:46
updated: 2023-03-04 03:56:46
categories: cybersecurity 
tags:
    - cybersecurity
    - penetration test
description:
top_img: https://iili.io/6vlEXf.jpg
cover: https://iili.io/HGleMOu.jpg
---

## 搜索引擎

### Google Hacking

|关键字|说明|
|:-----:|---|
|`*`|通配符|
|`-`|逻辑非|
|site|指定域名|
|intext|正文中存在关键字的网页|
|intitle|标题中存在关键字的网页|
|inurl|Url 中存在关键字的网页|
|filetype|指定搜索文件类型|

### Shodan

[Shodan](https://fofa.info/)

### ZoomEye

[ZoomEye](https://www.zoomeye.org/)

### FOFA

[FOFA](https://www.shodan.io/)

## 域名信息收集

### Whois 查询

```bash
$ whois baidu.com
   Domain Name: BAIDU.COM
   Registry Domain ID: 11181110_DOMAIN_COM-VRSN
   Registrar WHOIS Server: whois.markmonitor.com
   Registrar URL: http://www.markmonitor.com
   Updated Date: 2022-09-01T03:54:43Z
   Creation Date: 1999-10-11T11:05:17Z
   Registry Expiry Date: 2026-10-11T11:05:17Z
   Registrar: MarkMonitor Inc.
   Registrar IANA ID: 292
   Registrar Abuse Contact Email: abusecomplaints@markmonitor.com
   Registrar Abuse Contact Phone: +1.2086851750
   Domain Status: clientDeleteProhibited https://icann.org/epp#clientDeleteProhibited
   Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited
   Domain Status: clientUpdateProhibited https://icann.org/epp#clientUpdateProhibited
   Domain Status: serverDeleteProhibited https://icann.org/epp#serverDeleteProhibited
   Domain Status: serverTransferProhibited https://icann.org/epp#serverTransferProhibited
   Domain Status: serverUpdateProhibited https://icann.org/epp#serverUpdateProhibited
   Name Server: NS1.BAIDU.COM
   Name Server: NS2.BAIDU.COM
   Name Server: NS3.BAIDU.COM
   Name Server: NS4.BAIDU.COM
   Name Server: NS7.BAIDU.COM
   DNSSEC: unsigned
   URL of the ICANN Whois Inaccuracy Complaint Form: https://www.icann.org/wicf/
```

### 备案信息查询

[工信部备案管理系统](https://beian.miit.gov.cn/#/Integrated/index)

### 子域名信息查询

* 在线字典爆破

* 本地字典爆破工具

  * [SubDomainsBrute](https://github.com/lijiejie/subDomainsBrute)
  * [LayerDomainFinder](https://github.com/euphrat1ca/LayerDomainFinder)

* API 子域名查询接口

  * [OneForAll](https://github.com/shmilylty/OneForAll)

## 服务器信息收集

### 真实 IP 探测

#### CDN 判断方法

* ping 命令

```bash
$ ping www.aliyun.com -c 4
PING www.aliyun.com.w.cdngslb.com (42.59.1.231) 56(84) bytes of data.
64 bytes from 42.59.1.231 (42.59.1.231): icmp_seq=1 ttl=62 time=0.290 ms
64 bytes from 42.59.1.231 (42.59.1.231): icmp_seq=2 ttl=62 time=0.275 ms
64 bytes from 42.59.1.231 (42.59.1.231): icmp_seq=3 ttl=62 time=0.185 ms
64 bytes from 42.59.1.231: icmp_seq=4 ttl=62 time=0.234 ms

--- www.aliyun.com.w.cdngslb.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 4260ms
rtt min/avg/max/mdev = 0.185/0.246/0.290/0.040 ms
```

使用 ping 命令时，可能看到 wsf 、cdn 等字样的域名，这就表示目标服务器使用了 CDN 。不过有很多厂商可能只让 www 主站域名使用 CDN，空域名或者子域名并没有使用 CDN 缓存，所以这种情况下直接使用 `ping xxx.com` 就可得到真实的 IP 地址。

```bash
$ ping aliyun.com -c 4
PING aliyun.com (106.11.253.86) 56(84) bytes of data.
64 bytes from 106.11.253.86: icmp_seq=1 ttl=62 time=0.345 ms
64 bytes from 106.11.253.86 (106.11.253.86): icmp_seq=2 ttl=62 time=0.381 ms
64 bytes from 106.11.253.86 (106.11.253.86): icmp_seq=3 ttl=62 time=0.257 ms
64 bytes from 106.11.253.86: icmp_seq=4 ttl=62 time=0.285 ms

--- aliyun.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 13259ms
rtt min/avg/max/mdev = 0.257/0.317/0.381/0.048 ms
```

* nslookup 查询

如果解析多个 IP 地址，则可能使用了 CDN 。

```bash
$ nslookup www.aliyun.com
Server:         172.31.240.1
Address:        172.31.240.1#53

Non-authoritative answer:
www.aliyun.com  canonical name = www-jp-de-intl-adns.aliyun.com.
www-jp-de-intl-adns.aliyun.com  canonical name = www-jp-de-intl-adns.aliyun.com.gds.alibabadns.com.
www-jp-de-intl-adns.aliyun.com.gds.alibabadns.com       canonical name = www.aliyun.com.w.cdngslb.com.
Name:   www.aliyun.com.w.cdngslb.com
Address: 42.59.1.230
Name:   www.aliyun.com.w.cdngslb.com
Address: 42.59.1.231
Name:   www.aliyun.com.w.cdngslb.com
Address: 42.59.1.232
Name:   www.aliyun.com.w.cdngslb.com
Address: 42.59.1.233
Name:   www.aliyun.com.w.cdngslb.com
Address: 42.59.1.234
Name:   www.aliyun.com.w.cdngslb.com
Address: 42.59.1.235
Name:   www.aliyun.com.w.cdngslb.com
Address: 42.59.1.236
Name:   www.aliyun.com.w.cdngslb.com
Address: 42.59.1.229
Name:   www.aliyun.com.w.cdngslb.com
Address: 2408:8630:20b0:7:3::c
Name:   www.aliyun.com.w.cdngslb.com
Address: 2408:8630:20b0:7:3::b
```

如果只有单个域名，则很可能没有使用 CDN 。

```bash
$ nslookup www.sqlsec.com
Server:         172.31.240.1
Address:        172.31.240.1#53

Non-authoritative answer:
Name:   www.sqlsec.com
Address: 121.196.37.183
```

#### 绕过 CDN 查询真实 IP

* **多地 ping 查询**

  某些情况下，由于 CDN 高昂的费用，使用者可能为了节约成本会让 CDN 只覆盖一小部分高流量地区，所以这样就有可能被攻击者利用而探测到服务器的真实地址。

* **域名历史解析记录查询**

  有时候查询域名之前的 IP 解析记录，也可能会发现使用 CDN 之前的 IP 信息。

  * [securitytrails](https://securitytrails.com/)
  * [iphistory](https://viewdns.info/iphistory/)
  * [dnsdb](https://www.dnsdb.io/zh-cn/)
  * [netcraft](https://sitereport.netcraft.com/)
  * [ip138](https://site.ip138.com/)

* **子域名绕过**

  由于 CDN 费用昂贵，很多网站主站的访问量大往往使用 CDN 服务，而子网站就不一定使用 CDN 了。因此可以利用之前的[子域名爆破](/cybersecurity_penetration_test/chapter3/#子域名信息查询)来进行真实 IP 地址收集。

* **站点功能请求**

  一些网站提供注册服务，可能会验证邮件，还有 RSS 订阅邮件、忘记密码等业务。如果使用服务器本身带的 sendmail 直接发送邮件，就可以通过邮件中的显示邮件原文功能查看到邮件发送者的 IP 地址。

  还可以利用对网站请求的特点让目标服务器访问 DNSlog 这类可以记录 IP 者信息的网站，以此查看目标服务器的真实 IP 地址。

* **利用网站漏洞**

  网站本身存在漏洞，服务器主动和我们发起请求连接，我们也可以获取到目标站点的真实 IP 地址。

### 端口信息探测

#### 渗透测试中的常见端口

|端口|协议|
|:-:|-|
|21|FTP|
|22|SSH|
|23|Telnet 服务|
|25|SMTP 邮件传输协议|
|80|HTTP 服务相关端口|
|110|POP3 E-mail|
|135|共享文件或共享打印机|
|443|HTTP 服务相关常用端口 SSL|
|445|文件或打印机共享服务|
|1443|Microsoft SQL Server 数据库|
|1521|Oracle 数据库|
|3306|MySQL 数据库|
|3389|Windows 远程桌面服务|
|5432/5433|PostgreSQL 数据库端口|
|6379|Redis 存储默认端口|
|7001|Weblogic 默认端口|
|8080|HTTP 服务常用端口|
|8000 - 8100|HTTP 服务常用端口|
|9200|Elasticsearch 默认端口|
|11211|Memcached 分布式缓存系统端口|

#### Nmap 简单扫描

```bash
$ nmap 192.168.127.135
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-06 07:52 CST
Nmap scan report for localhost (192.168.127.135)
Host is up (0.0022s latency).
Not shown: 991 filtered tcp ports (no-response)
PORT      STATE SERVICE
21/tcp    open  ftp
22/tcp    open  ssh
80/tcp    open  http
4848/tcp  open  appserv-http
8080/tcp  open  http-proxy
8383/tcp  open  m2mservices
9200/tcp  open  wap-wsp
49153/tcp open  unknown
49154/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 19.06 seconds
```

<center> <b>Nmap 返回状态及说明</b></center>

|状态|说明|
|:-:|-|
|open|端口对外开放|
|closed|端口对外关闭|
|filtered|无法判断，被防火墙设备拦截过滤|
|unfiltered|未被过滤，使用 ACK 扫描才可能出现这种情况|
|open\|filtered|不能确定是开放还是被过滤，可能被专业设备阻止探测了|
|closed\|filtered|表确定是关闭还是被过滤|

#### Ping 扫描

Ping 扫描可以显示出在线的主机，可以比较快速地获取目标信息而不被轻易地发现。使用 Nmap 中的 `-sP` 命令即可对网段进行 Ping 扫描。

```bash
$ nmap 192.168.127.1/24 -sP
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-06 08:07 CST
Nmap scan report for localhost (192.168.127.1)
Host is up (0.0029s latency).
Nmap scan report for localhost (192.168.127.2)
Host is up (0.0056s latency).
Nmap scan report for localhost (192.168.127.135)
Host is up (0.027s latency).
Nmap done: 256 IP addresses (3 hosts up) scanned in 14.96 seconds
```

<!-- ### 操作系统类型探测

#### 使用 TTL 值进行系统探测 -->
