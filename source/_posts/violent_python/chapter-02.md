---
title: 学习笔记 —— 《Python 绝技》 第2章 用 Python 进行渗透测试
date: 2022-09-06 13:52:37
updated: 2022-09-06 13:52:37
categories: violent python
tags:
    - python 
    - hacker
description: 
top_img: https://iili.io/6vlEXf.jpg
cover: https://iili.io/6vlGs4.jpg
---

## 编写一个端口扫描器

### 了解 socket 模块

使用 Python 扫描 TCP 端口需要导入 Python 的 BSD *套接字* API —— `socket` 模块。其官方文档[见此](https://docs.python.org/zh-cn/3/library/socket.html)。

为了完成端口扫描器，我们需要了解：

+ [`socket.gethostbyname(hostname)`](https://docs.python.org/zh-cn/3/library/socket.html#socket.gethostbyname)

    > 将主机名转换为 IPv4 地址格式。IPv4 地址以字符串格式返回，如 '100.50.200.5'。
    >
    > 如果主机名本身是 IPv4 地址，则原样返回。
    >
    > 更完整的接口请参考 [`gethostbyname_ex()`](https://docs.python.org/zh-cn/3/library/socket.html#socket.gethostbyname_ex)。
    >
    > `gethostbyname()` 不支持 IPv6 名称解析，应使用 [`getaddrinfo()`](https://docs.python.org/zh-cn/3/library/socket.html#socket.getaddrinfo) 来支持 IPv4/v6 双协议栈。

+ [`socket.gethostbyaddr(ip_address)`](https://docs.python.org/zh-cn/3/library/socket.html#socket.gethostbyaddr)

    > 返回三元组 `(hostname, aliaslist, ipaddrlist)`，其中
    >
    > *hostname* 是响应给定 *ip_address* 的主要主机名，
    >
    > *aliaslist* 是相同地址的其他可用主机名的列表（可能为空），
    >
    > *ipaddrlist* 是 IPv4/v6 地址列表，包含相同主机名、相同接口的不同地址（很可能仅包含一个地址）。
    >
    > 要查询[全限定域名](https://baike.baidu.com/item/FQDN/5102541)，请使用函数 [`getfqdn()`](https://docs.python.org/zh-cn/3/library/socket.html#socket.getfqdn)。
    >
    > `gethostbyaddr()` 支持 IPv4 和 IPv6。

+ [`class socket.socket(family=AF_INET, type=SOCK_STREAM, proto=0, fileno=None)`](https://docs.python.org/zh-cn/3/library/socket.html#socket.socket)

    > 使用给定的 *family (地址族)* 、 *type (套接字类型)* 和 *proto (协议号)* 创建一个新的套接字。
    >
    > *地址族* 应为 [`AF_INET`](https://docs.python.org/zh-cn/3/library/socket.html#socket.AF_INET) (默认值), [`AF_INET6`](https://docs.python.org/zh-cn/3/library/socket.html#socket.AF_INET6), [`AF_UNIX`](https://docs.python.org/zh-cn/3/library/socket.html#socket.AF_UNIX), [`AF_CAN`](https://docs.python.org/zh-cn/3/library/socket.html#socket.AF_CAN), [`AF_PACKET`](https://docs.python.org/zh-cn/3/library/socket.html#socket.AF_PACKET) 或 [`AF_RDS`](https://docs.python.org/zh-cn/3/library/socket.html#socket.AF_RDS) 之一。
    >
    > *套接字类型* 应为 [`SOCK_STREAM`](https://docs.python.org/zh-cn/3/library/socket.html#socket.SOCK_STREAM) (默认值), [`SOCK_DGRAM`](https://docs.python.org/zh-cn/3/library/socket.html#socket.SOCK_DGRAM), [`SOCK_RAW`](https://docs.python.org/zh-cn/3/library/socket.html#socket.SOCK_DGRAM) 或其他可能的 `SOCK_` 常量之一。
    >
    > *协议号* 通常为零并且可以省略，或在协议族为 [`AF_CAN`](https://docs.python.org/zh-cn/3/library/socket.html#socket.AF_CAN) 的情况下，协议应为 `CAN_RAW`, [`CAN_BCM`](https://docs.python.org/zh-cn/3/library/socket.html#socket.CAN_BCM), [`CAN_ISOTP`](https://docs.python.org/zh-cn/3/library/socket.html#socket.CAN_ISOTP) 或 [`CAN_J1939`](https://docs.python.org/zh-cn/3/library/socket.html#socket.CAN_J1939) 之一。
    >
    > 如果指定了 *fileno* ，那么将从这一指定的文件描述符中自动检测 *family* 、 *type* 和 *proto* 的值。如果调用本函数时显式指定了 *family* 、 *type* 或 *proto* 参数，可以覆盖自动检测的值。这只会影响 Python 表示诸如 [`socket.getpeername()`](https://docs.python.org/zh-cn/3/library/socket.html#socket.socket.getpeername) 一类函数的返回值的方式，而不影响实际的操作系统资源。与 [`socket.fromfd()`](https://docs.python.org/zh-cn/3/library/socket.html#socket.fromfd) 不同， *fileno* 将返回原先的套接字，而不是复制出新的套接字。这有助于在分离的套接字上调用 [`socket.close()`](https://docs.python.org/zh-cn/3/library/socket.html#socket.close) 来关闭它。

+ [`socket.create_connection(address[, timeout[, source_address]])`](https://docs.python.org/zh-cn/3/library/socket.html#socket.create_connection)

    > 连接到一个在互联网 *address* (以 `(host, port)` 2 元组表示) 上侦听的 TCP 服务，并返回套接字对象。 这是一个相比 [`socket.connect()`](https://docs.python.org/zh-cn/3/library/socket.html#socket.socket.connect) 层级更高的函数：如果 host 是非数字的主机名，它将尝试将其解析为 [`AF_INET`](https://docs.python.org/zh-cn/3/library/socket.html#socket.AF_INET) 和 [`AF_INET6`](https://docs.python.org/zh-cn/3/library/socket.html#socket.AF_INET6) ，然后依次尝试连接到所有可能的地址直到连接成功。 这使编写兼容 IPv4 和 IPv6 的客户端变得很容易。
    >
    > 传入可选参数 *timeout* 可以在套接字实例上设置超时（在尝试连接前）。如果未提供 *timeout* ，则使用由 [`getdefaulttimeout()`](https://docs.python.org/zh-cn/3/library/socket.html#socket.getdefaulttimeout) 返回的全局默认超时设置。
    >
    > 如果提供了 *source_address* ，它必须为二元组 `(host, port)` ，以便套接字在连接之前绑定为其源地址。如果 host 或 port 分别为 '' 或 0，则使用操作系统默认行为。

### 了解 argparse 库

为了才用户那里获得 *主机名* 和 *端口* ，我们需要使用 argparse 库来解析命令行参数。其官方文档[见此](https://docs.python.org/zh-cn/3/library/argparse.html)。

调用 `argparse.ArgumentParser()` 创建一个 [ArgumentParser](https://docs.python.org/zh-cn/3/library/argparse.html#argumentparser-objects) 对象。

> `class argparse.ArgumentParser(prog=None, usage=None, description=None, epilog=None, parents=[], formatter_class=argparse.HelpFormatter, prefix_chars='-', fromfile_prefix_chars=None, argument_default=None, conflict_handler='error', add_help=True, allow_abbrev=True, exit_on_error=True)`
>
> + [prog](https://docs.python.org/zh-cn/3/library/argparse.html#prog) - 程序的名称 (默认值: `os.path.basename(sys.argv[0])`)
>
> + [usage](https://docs.python.org/zh-cn/3/library/argparse.html#usage) - 描述程序用途的字符串（默认值：从添加到解析器的参数生成）
>
> + [description](https://docs.python.org/zh-cn/3/library/argparse.html#description) - 在参数帮助文档之前显示的文本（默认值：无）
>
> + [epilog](https://docs.python.org/zh-cn/3/library/argparse.html#epilog) - 在参数帮助文档之后显示的文本（默认值：无）
>
> + [parents](https://docs.python.org/zh-cn/3/library/argparse.html#parents) - 一个 ArgumentParser 对象的列表，它们的参数也应包含在内
>
> + [formatter_class](https://docs.python.org/zh-cn/3/library/argparse.html#formatter-class) - 用于自定义帮助文档输出格式的类
>
> + [prefix_chars](https://docs.python.org/zh-cn/3/library/argparse.html#prefix-chars) - 可选参数的前缀字符集合（默认值： '-'）
>
> + [fromfile_prefix_chars](https://docs.python.org/zh-cn/3/library/argparse.html#fromfile-prefix-chars) - 当需要从文件中读取其他参数时，用于标识文件名的前缀字符集合（默认值： `None`）
>
> + [argument_default](https://docs.python.org/zh-cn/3/library/argparse.html#argument-default) - 参数的全局默认值（默认值： `None`）
>
> + [conflict_handler](https://docs.python.org/zh-cn/3/library/argparse.html#conflict-handler) - 解决冲突选项的策略（通常是不必要的）
>
> + [add_help](https://docs.python.org/zh-cn/3/library/argparse.html#add-help) - 为解析器添加一个 -h/--help 选项（默认值： `True`）
>
> + [allow_abbrev](https://docs.python.org/zh-cn/3/library/argparse.html#allow-abbrev) - 如果缩写是无歧义的，则允许缩写长选项 （默认值：`True`）
>
> + [exit_on_error](https://docs.python.org/zh-cn/3/library/argparse.html#exit-on-error) - 决定当错误发生时是否让 ArgumentParser 附带错误信息退出。 (默认值: `True`)

定义单个的命令行参数应当如何解析。

> `ArgumentParser.add_argument(name or flags...[, action][, nargs][, const][, default][, type][, choices][, required][, help][, metavar][, dest])`
>
> + [name or flags](https://docs.python.org/zh-cn/3/library/argparse.html#name-or-flags) - 一个命名或者一个选项字符串的列表，例如 `foo` 或 `-f, --foo`。
>
> + [action](https://docs.python.org/zh-cn/3/library/argparse.html#action) - 当参数在命令行中出现时使用的动作基本类型。
>
> + [nargs](https://docs.python.org/zh-cn/3/library/argparse.html#nargs) - 命令行参数应当消耗的数目。
>
> + [const](https://docs.python.org/zh-cn/3/library/argparse.html#const) - 被一些 [action](https://docs.python.org/zh-cn/3/library/argparse.html#action) 和 [nargs](https://docs.python.org/zh-cn/3/library/argparse.html#nargs) 选择所需求的常数。
>
> + [default](https://docs.python.org/zh-cn/3/library/argparse.html#default) - 当参数未在命令行中出现并且也不存在于命名空间对象时所产生的值。
>
> + [type](https://docs.python.org/zh-cn/3/library/argparse.html#type) - 命令行参数应当被转换成的类型。
>
> + [choices](https://docs.python.org/zh-cn/3/library/argparse.html#choices) - 可用的参数的容器。
>
> + [required](https://docs.python.org/zh-cn/3/library/argparse.html#required) - 此命令行选项是否可省略 （仅选项可用）。
>
> + [help](https://docs.python.org/zh-cn/3/library/argparse.html#help) - 一个此选项作用的简单描述。
>
> + [metavar](https://docs.python.org/zh-cn/3/library/argparse.html#metavar) - 在使用方法消息中使用的参数值示例。
>
> + [dest](https://docs.python.org/zh-cn/3/library/argparse.html#dest) - 被添加到 [parse_args()](https://docs.python.org/zh-cn/3/library/argparse.html#argparse.ArgumentParser.parse_args) 所返回对象上的属性名。

### TCP 扫描器

```python
import argparse
from socket import AF_INET, SOCK_STREAM, gethostbyaddr, gethostbyname, setdefaulttimeout, socket
from threading import Thread, Semaphore


screen_lock = Semaphore(value=1)  # 创建信号量对象

def conn_scan(target_host, target_port):
    try:
        conn_skt = socket()  # 创建套接字对象
        conn_skt.connect((target_host, target_port))
        screen_lock.acquire() # 获取一个信号量。
        print(f"[+] port {target_port} tcp open")
    except:
        screen_lock.acquire()
        print(f"[-] port {target_port} tcp close")
    finally:
        screen_lock.release()  # 释放一个信号量
        conn_skt.close()


def port_scan(target_host, target_ports):
    try:
        # 尝试通过主机名获取 IP 地址
        target_IP = gethostbyname(target_host)
    except:
        print(f"[-] Cannot resolve {target_host}: Unkown host")
        return
    try:
        # 通过 IP 获取主机名
        target_name = gethostbyaddr(target_IP)
        print(f"[+] Scan Results for: {target_name[0]}")
    except:
        print(f"[+] Scan Results for: {target_IP}")

    setdefaulttimeout(1)  # 设置 socket 默认超时时间
    for target_port in target_ports:
        # 遍历端口，尝试连接
        t = Thread(target=conn_scan, args=(target_host, int(target_port)))
        t.start()


def main():
    parser = argparse.ArgumentParser()
    parser.add_argument(
        "-H",
        dest="target_host",
        type=str,
        required=True,
        help="specify target host"
    )
    parser.add_argument(
        "-p",
        dest="target_port",
        type=str,
        required=True,
        nargs="+",
        help="specify target port[s], separated by blank"
    )

    args = parser.parse_args()  # 获取到用户输入参数对象
    target_host = args.target_host
    target_ports = args.target_port

    port_scan(target_host, target_ports)


if __name__ == "__main__":
    main()
```

我们使用以上代码来扫描 [scanme.nmap.org](scanme.nmap.org) 的 20, 80, 135 端口，得到以下结果：

```plain
[+] Scan Results for: scanme.nmap.org
[+] port 22 tcp open
[+] port 80 tcp open
[-] port 135 tcp close
```

### 使用 Python-Nmap 增强扫描

```python
import nmap
import argparse
from dns.resolver import resolve


def nmap_scan(target_host, target_port):
    nm = nmap.PortScanner()
    nm.scan(target_host, target_port)
    state = nm[target_host]['tcp'][int(target_port)]['state']
    print(f"[*] {target_host} tcp/ {target_port} {state}")


def main():
    parser = argparse.ArgumentParser()
    parser.add_argument(
        "-H",
        dest="target_host",
        type=str,
        required=True,
        help="specify target host"
    )
    parser.add_argument(
        "-p",
        dest="target_port",
        type=str,
        required=True,
        nargs="+",
        help="specify target port[s], separated by blank"
    )

    args = parser.parse_args()
    target_host = args.target_host
    target_ports = args.target_port

    # 使用 dnspython 解析 IP 地址
    target_IP = resolve(target_host, "A")[0].address 

    print(f"[+] Scan Results for: {target_host}")
    for tartget_port in target_ports:
        nmap_scan(target_IP, tartget_port)

if __name__ == "__main__":
    main()
```

同样扫描[scanme.nmap.org](scanme.nmap.org) 的 20, 80, 135 端口， 得到如下结果：

```plain
[+] Scan Results for: scanme.nmap.org
[*] 45.33.32.156 tcp/ 22 open
[*] 45.33.32.156 tcp/ 80 open
[*] 45.33.32.156 tcp/ 135 filtered
```

可以看到 TCP 135 端口的结果出现了变化，这是因为 TCP 135 端口的请求被服务器或防火墙过滤掉了，而不是真的关闭了。显然，Nmap 要比我们自己写的扫描器更强大。
