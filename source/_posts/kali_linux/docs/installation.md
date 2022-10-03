---
title: Kali Linux 官方文档 Installation
date: 2022-10-02 11:39:42
updated: 2022-10-02 11:39:42
categories: kali-linux
tags: 
    - kali
    - kali-linux
    - docs
description:
top_img: https://iili.io/iJ2mSp.jpg # https://iili.io/PezYlI.png
cover: https://iili.io/iJ2yHN.png # https://iili.io/PezYlI.png
---

## Bare-bones Kali | 裸露 Kali

Kali traditionally has been solely recommended as a penetration testing distribution, and for good reason. However, through the years Kali has become more stable and evolved into something that users can use no matter what their reasoning is. While still primarily a penetration testing distribution, we accept that many users may not even be in the cybersecurity field. For those users wanting to install Kali, but may not need the tools or just want the UI, this guide is for you.

传统上，Kali 仅仅作为一个渗透测试（好的方向）发行版被推荐。然而经过这些年的发展，Kali 变得更加稳定且不论是何用途都可以使用。尽管首要目的还是渗透测试，但我们发现很多用户并不工作在渗透测试领域。对于这些想要安装 Kali 的用户，但不想要各种工具或者只是想要 UI ，此文档正是为你准备的。

### Installing a bare-bones Kali | 安装裸露 Kali

To get a Kali without any tools is quite easy. We will be following the [hard disk install](https://www.kali.org/docs/installation/hard-disk-install/) for the most part. The important part is to select the following packages:

安装一个不带任何工具的 Kali 是非常容易的。大部分跟着 [硬盘安装](/kali_linux/docs/installation/#installing-kali-linux-安装-kali-linux) 的步骤即可。最重要的部分就是选择下面的这些包：

![Installing a bare-bones Kali](https://www.kali.org/docs/installation/barebone-kali/bare-bones-install.png)

Of course, you can select whichever desktop environment you wish. It is worth mentioning now that KDE has great support for Wacom tablets! Be careful not to mix KDE with another desktop distribution however, as there are some bugs that can occur when this happens.

当然，你可以选择你你想要的桌面环境。KDE 现在已经很好的支持了 Wacom 数位板。但是，注意不要和其它桌面混合使用，因为可能导致一些 bug 。

Now that we are installed and logged in, there are a few things we should do. Keep in mind, these should always be done, not just for a daily use case! Let’s first change the root user’s password:

现在我们安装完成并成功登录系统，还有一些操作需要完成。这些操作总是要做的，并不是只有日常使用时才要做的。首先我们修改 root 用户密码：

```shell
kali@kali:~$ sudo su
[sudo] password for kali:
root@kali:/home/kali#
root@kali:/home/kali# passwd
New password:
Retype new password:
passwd: password updated successfully

root@kali:/home/kali#
```

After this we can make sure our system is up-to-date:

之后我们可以确保我们的系统是最新的：

```shell
kali@kali:~$ sudo apt update && sudo apt upgrade -y
....
kali@kali:~$
kali@kali:~$ [ -f /var/run/reboot-required ] && sudo reboot -f
```

We can now finish off our setup by making sure kali-tweaks is configured properly:

现在，我们可以通过确保正确配置Kali-Tweaks来完成我们的安装：

```shell
kali@kali:~$ kali-tweaks
```

What we are looking for are changes required in ‘Hardening’, unchecking any options to make our system more secure.

我们会查找必须强制更新的软件，并不提供任何选项以保证系统的安全。

*Updated on: 2022-Jul-26*
*Author: [gamb1t](https://gitlab.com/gamb1t)*

---

## Installing Kali Linux | 安装 Kali Linux

Installing Kali Linux (single boot) on your computer is an easy process. This guide will cover the basic install (which can be done on bare metal or [guest VM](https://www.kali.org/docs/virtualization/)), with the option of encrypting the partition. At times, you may have sensitive data you would prefer to encrypt using Full Disk Encryption (FDE). During the setup process you can initiate an LVM encrypted install on either Hard Disk or USB drives.

在电脑上安装 Kali Linux (单启动) 是一件很容易的事。本文档涵盖基本安装（可以安装在实机或者虚拟机），可以选择加密分区。有时，你有一些敏感信息。你想要全盘加密（FDE）。在安装的过程中，不管是硬盘还是 USB 驱动器，你都可以启动 LVM 加密。

First, you’ll need compatible computer hardware. Kali Linux is supported on amd64 (x86_64/64-bit) and i386 (x86/32-bit) platforms. Where possible, we would recommend using the amd64 images. The hardware requirements are minimal as listed in the section below, although better hardware will naturally provide better performance. You should be able to use Kali Linux on newer hardware with UEFI and older systems with BIOS.

首先，你需要兼容的计算机硬件。Kali Linux 支持 amd64 (x86_64/64-bit) 和 i386 (x86/32-bit) 平台。如果可以，我们建议使用 amd64 镜像。最小硬件要求如下所列，当然更好的硬件可以提供更好的体验。你可以在新的硬件上使用 UEFI 或者在老的硬件上使用 BIOS 安装 kali。

Our i386 images, by default use a [PAE kernel](https://pkg.kali.org/pkg/linux), so you can run them on systems with over 4 GB of RAM.

我们的 i386 镜像默认使用 [PAE 内核](https://zh.wikipedia.org/wiki/%E7%89%A9%E7%90%86%E5%9C%B0%E5%9D%80%E6%89%A9%E5%B1%95)，所以你可以在超过 4 GB 的内存上运行。

In our example, we will be installing Kali Linux in a fresh guest VM, without any existing operating systems pre-installed. We will explain other possible scenarios throughout the guide.

在我们的例子中，我们在一个全新的虚拟机中安装 Kali Linux ，没有任何预安装的系统。我们和解释其他可能的情形。

### System Requirements | 系统要求

The installation requirements for Kali Linux will vary depending on what you would like to install and your setup. For system requirements:

Kali Linux 的安装要求根据安装内容和设置的不同而不同。对于系统要求：

+ On the low end, you can set up Kali Linux as a basic Secure Shell (SSH) server with no desktop, using as little as 128 MB of RAM (512 MB recommended) and 2 GB of disk space.

  在低端，你可以将 Kali Linux 作为一个 SSH 服务器安装而不安装桌面，至少需要 128 MB 内存（推荐 512 MB） 和 2 GB 的磁盘空间。

+ On the higher end, if you opt to install the default Xfce4 desktop and the `kali-linux-default` [metapackage](https://www.kali.org/docs/general-use/metapackages/), you should really aim for **at least 2 GB of RAM** and **20 GB of disk space**.

  在高端，如果你选择安装默认的 Xfce4 桌面并且安装 `kali-linux-default` [元包](), 你真的需要**至少 2 GB 内存**和 **20 GB 的磁盘空间**。

  + When using resource-intensive applications, such as Burp Suite, [they recommend](https://portswigger.net/support/burp-suite-software-faqs) at least **8 GB of RAM** (and even more if it is a large web application!) or using simultaneous programs at the same time.

  如果你需要使用资源密集型应用程序，如 Burp Suite ，他们推荐至少 **8 GB 内存** （如果是一个大型的 web 应用可能还需要更多）或者使用同步程序。
  