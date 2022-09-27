---
title: Kali Linux 官方文档 Introduction
date: 2022-09-13 14:51:33
updated: 2022-09-24 01:49:19
categories: kali-linux
tags: 
    - kali
    - kali-linux
    - docs
description:
top_img: https://iili.io/iJ2mSp.jpg # https://iili.io/PezYlI.png
cover: https://iili.io/iJ2yHN.png # https://iili.io/PezYlI.png
---

> 此翻译为个人学习目的，水平有限，难免有谬误之处。请以官方英文文档为准。
>
> 官方文档源地址：[https://www.kali.org/docs/introduction/](https://www.kali.org/docs/introduction/)

## What is Kali Linux? | 什么是 Kali Linux

### About Kali Linux | 关于 Kali Linux

Kali Linux (formerly known as BackTrack Linux) is an open-source, Debian-based Linux distribution aimed at advanced Penetration Testing and Security Auditing. It does this by providing common tools, configurations, and automations which allows the user to focus on the task that needs to be completed, not the surrounding activity.

[Kali Linux](https://www.kali.org/) *（以前叫做 [BackTrack Linux](https://www.backtrack-linux.org/)）* 是一个开源的、基于 Debian 的 Linux 发行版，目的在于高级渗透测试以及安全审查。Kali Linux 提供常见工具、配置以及自动化，由此可以让用户聚焦在任务上而不是其他的周边活动。

Kali Linux contains industry specific modifications as well as several hundred tools targeted towards various Information Security tasks, such as Penetration Testing, Security Research, Computer Forensics, Reverse Engineering, Vulnerability Management and Red Team Testing.

Kali Linux 包含针对各种信息安全任务的的几百个工具，例如渗透测试，安全研究，计算机取证，逆向工程，脆弱性管理和红队测试。

> Red Teaming, in contrast to penetration testing, is focused on target objectives. Rather than putting a priority on finding as many vulnerabilities as possible, a red team attempts to test how an organization’s security team responds to various threats. The Red Team will always focus on the objectives, seeking to gain access to sensitive information in stealth, avoiding detection. [See more](https://www.packetlabs.net/posts/red-teaming/).
>
> 红队测试，相较于渗透测试，更加注重于目标。红队测试的目的是测试一个组织的安全团队如何应对各式各样的威胁，而不是尽可能地找到更多的漏洞。红队测试总是聚焦于目标，企图隐蔽地、不被检测到地获取到敏感信息。

Kali Linux is a multi-platform solution, accessible and freely available to information security professionals and hobbyists.

kali Linux 是一个多平台解决方案，对于信息安全的专业从业者或业余爱好者，它是可以免费获取到的。

### Kali Linux Features | Kali Linux 特性

+ **More than 600 penetration testing tools included**: After reviewing every tool that was included in BackTrack, we eliminated a great number of tools that either simply did not work or which duplicated other tools that provided the same or similar functionality. Details on what’s included are on the [Kali Tools](https://www.kali.org/tools/) site.

    **包含超过600个渗透测试工具**：在审查BackTrack中的每一个工具后，我们淘汰了大量不能工作或者与其他工具功能相似或重复的工具。具体包含哪些工具，请见 [kali tools](https://www.kali.org/tools/) 网站

+ **Free (as in beer) and always will be**: Kali Linux, like BackTrack, is completely free of charge and always will be. You will never, ever have to pay for Kali Linux.

    **免费且永久免费**：Kali Linux 和 BackTrack 一样是免费且永久免费的。你永远不需要为 Kali Linux 付费。

+ **Open source Git tree**: We are committed to the open source development model and our development tree is available for all to see. All of the source code which goes into Kali Linux is available for anyone who wants to tweak or rebuild [packages](https://pkg.kali.org/) to suit their specific needs.

    **开源 Git 树**：我们致力于开源开发，且我们的开发树所有人都可以访问。所有想要调整和重构包以适应他们的特殊需求的人都可以访问 Kali Linux 的源代码。

+ **FHS compliant**: Kali adheres to the Filesystem Hierarchy Standard, allowing Linux users to easily locate binaries, support files, libraries, etc.

    **符合 FHS 标准**：Kali 遵循文件系统层次结构标准，用户可以方便地访问二进制文件、支持文件、库等等。

+ **Wide-ranging wireless device support**: A regular sticking point with Linux distributions has been support for wireless interfaces. We have built Kali Linux to support as many wireless devices as we possibly can, allowing it to run properly on a wide variety of hardware and making it compatible with numerous USB and other wireless devices.

    **广泛的无线设备支持**：Linux 发行版的常见痛点是对无线设备的支持。我们尽可能地支持无线设备，允许它在各种硬件上正确运行，并使其与众多USB和其他无线设备兼容。

+ **Custom kernel, patched for injection**: As penetration testers, the development team often needs to do wireless assessments, so our kernel has the latest injection patches included.

    **自定义内核，注入补丁**：作为渗透测试人员，开发团队经常需要做无线评估，所以我们的内核包含了最新的注入补丁。

+ **Developed in a secure environment**: The Kali Linux team is made up of a small group of individuals who are the only ones trusted to commit packages and interact with the repositories, all of which is done using multiple secure protocols.

    **在安全环境中开发**：Kali Linux 团队由一小群个人组成，这群人是唯一被信任的可提交包和与存储库交互的人。所有工作都是使用多种安全协议完成的。

+ **GPG signed packages and repositories**: Every package in Kali Linux is signed by each individual developer who built and committed it, and the repositories subsequently sign the packages as well.

    **使用 GPG 签名软件包和存储库**：Kali Linux 中的每个包都由构建和提交它的个人签名，而且随后存储库同样对包签名。
    > GPG: [GNU Privacy Guard](https://www.gnupg.org/)

+ **Multi-language support**: Although penetration tools tend to be written in English, we have ensured that Kali includes true multilingual support, allowing more users to operate in their native language and locate the tools they need for the job.

    **多语言支持**：尽管渗透工具倾向于使用英语，我们确保 Kali 支持多种语言，使更多的用户能够使用他们的母语操作系统并定位他们需要的工具。

+ **Completely customizable**: We thoroughly understand that not everyone will agree with our design decisions, so we have made it as easy as possible for our more adventurous users to customize Kali Linux to their liking, all the way down to the kernel.

    **完全可定制化**：我们完全理解不是所有人都同意我们的设计策略，所以我们尽可能让我们的冒险用户容易地根据他们的喜好定制 Kali Linux，一直到内核。

+ **ARMEL and ARMHF support**: Since ARM-based single-board systems like the Raspberry Pi and BeagleBone Black, among others, are becoming more and more prevalent and inexpensive, we knew that Kali’s ARM support would need to be as robust as we could manage, with fully working installations for both ARMEL and ARMHF systems. Kali Linux is available on a wide range of ARM devices and has ARM repositories integrated with the mainline distribution so tools for ARM are updated in conjunction with the rest of the distribution.

    **支持 ARMEL 和 ARMHF**：鉴于基于 ARM 的单板计算机——例如：树莓派， BeagleBone Black 等等——越来越流行，我们知道 Kali 对于 ARM 的支持需要尽可能强大，针对 ARMEL 和 ARMHF 系统，Kali 支持完整安装。Kali Linux 在很多 ARM 设备上可用，而且 ARM 存储库和主线发行版融合，所以 ARM 与其他发行版一同更新。

+ For more features of Kali Linux, please see the following page: [Kali Linux Overview](https://www.kali.org/features/).

  更多的 Kali Linux 特性，请访问 [https://www.kali.org/features/](https://www.kali.org/features/)：

Kali Linux is specifically tailored to the needs of penetration testing professionals, and therefore all documentation on this site assumes prior knowledge of, and familiarity with, the Linux operating system in general. Please see [Should I Use Kali Linux?](https://www.kali.org/docs/introduction/should-i-use-kali-linux/) for more details on what makes Kali unique.

Kali Linux专门针对渗透测试专业人员的需求量身定制，因此本网站的所有文档假设你掌握了前置知识和类 Linux 操作系统的使用。是什么让 Kali 如此与众不同，请看[我该使用 Kali Linux 吗？](#should-i-use-kali-linux-我该使用-kali-linux-吗)

Updated on: 2022-Sep-09
Author: [*g0tmi1k*](https://gitlab.com/g0tmi1k)

---

## Should I Use Kali Linux? |我该使用 Kali Linux 吗?

### What’s Different About Kali Linux? | Kali Linux 有何不同?

Kali Linux is specifically geared to meet the requirements of professional penetration testing and security auditing. To achieve this, several core changes have been implemented in Kali Linux which reflect these needs:

Kali Linux 旨在满足专业化渗透测试和安全审查。为了实现这一目标，Kali Linux 实现了一些内核更改，以反映这些需求。

1. **Network services disabled by default**: Kali Linux contains systemd hooks that disable network services by default. These hooks allow us to install various services on Kali Linux, while ensuring that our distribution remains secure by default, no matter what packages are installed. Additional services such as Bluetooth are also blocklisted by default.

    **网络服务默认关闭**：Kali Linux 包含 systemd 钩子以默认关闭网络服务。这些钩子允许我们在 Kali Linux 中安装多种服务，同时不管什么软件包被安装，都确保我们的发行版保持安全。额外的服务，如蓝牙，也被默认阻止了。

2. **Custom Linux kernel**: Kali Linux uses an upstream kernel, patched for wireless injection.

    **自定义 Linux 内核**：Kali Linux 使用上游内核，修复了无线注入。

3. **A minimal and trusted set of repositories**: given the aims and goals of Kali Linux, maintaining the integrity of the system as a whole is absolutely key. With that goal in mind, the set of upstream software sources which Kali uses is kept to an absolute minimum. Many new Kali users are tempted to add additional repositories to their `sources.list`, but doing so runs a very serious risk of breaking your Kali Linux installation.

    **一个最小化且可信任的存储库设置**：鉴于 Kali Linux 的目标，保持系统为一个完整的整体是关键。为了这个目标，Kali 使用的上游软件必须保证最小。许多新 Kali 用户急于向 `sources.list` 添加额外的存储库，但是如此做会有很大的风险破坏 Kali Linux 安装。

### Is Kali Linux Right For You? | Kali Linux 是你的正确选择吗?

As the distribution’s developers, you might expect us to recommend that everyone should be using Kali Linux. The fact of the matter is, however, that Kali is a Linux distribution specifically geared towards professional penetration testers and security specialists, and given its unique nature, it is NOT a recommended distribution if you’re unfamiliar with Linux or are looking for a general-purpose Linux desktop distribution for development, web design, gaming, etc.

作为发行版的开发者，你也许会认为我们会所有人推荐 Kali Linux 。事实上，问题在于 Kali Linux 是一个专门面向专业的渗透测试人员何安全专家的 Linux 发行版，并且鉴于它独特的特质，如果你不熟悉 Linux 或者你想要一个用于一般的开发、web 设计、游戏开发等目的的 Linux 桌面发行版，我们不推荐你使用 Kali Linux 。

Even for experienced Linux users, Kali can pose some challenges. Although Kali is an open source project, it’s not a wide-open source project, for reasons of security. The development team is small and trusted, packages in the repositories are signed both by the individual committer and the team, and - importantly - the set of upstream repositories from which updates and new packages are drawn is very small. Adding repositories to your software sources which have not been tested by the Kali Linux development team is a good way to cause problems on your system.

即使是有经验的 Linux 用户，Kali 也可能带来一些挑战。尽管 Kali 是一个开源项目，但基于安全的缘故，它不是完全开源的项目。开发团队是很小但值得信任的，发行版中的软件包都是经过个人提交者和团队双重签名的，而且，重要的是，用于更新和保存新的软件包的上游存储库是非常小的。向你软件源添加未经 Kali Linux 开发团队测试过的存储库很容易在你系统上发生问题。

While Kali Linux is architected to be highly customizable, do not expect to be able to add random unrelated packages and repositories that are “out of band” of the regular Kali software sources and have it Just Work. In particular, there is absolutely no support whatsoever for the apt-add-repository command, LaunchPad, or PPAs. Trying to install ***Steam*** on your Kali Linux desktop is an experiment that will not end well. Even getting a package as mainstream as NodeJS onto a Kali Linux installation can take [a little extra effort and tinkering](http://www.acme-dot.com/stupid-problems-deserve-stupid-solutions/).

尽管 Kali Linux 的架构是高度可自定义的，但不要期望添加一些随机的、无关的，不属于 Kali 软件源的软件包和存储库，它们还能正常工作。尤其，无论如何绝对不支持 `apt-add-repository` 命令、[LaunchPad](https://launchpad.net/)、PPA (个人软件包存档 Personal Package Archive)。尝试在 Kali Linux 桌面安装 ***Stream*** 是一个不会有积极结果的尝试。即使是在 Kali Linux 上安装如 NodeJS 一般主流的软件包也需要一些额外的设置。

If you are unfamiliar with Linux generally, if you do not have at least a basic level of competence in administering a system, if you are looking for a Linux distribution to use as a learning tool to get to know your way around Linux, or if you want a distro that you can use as a general purpose desktop installation, Kali Linux is probably not what you are looking for.

如果你不熟悉一般的 Linux ，如果你没有管理系统的基本能力，如果你想要一个 Linux 发行版来学习 Linux 相关工具，又或者你想要一个一般目的的Linux 发行版桌面安装，Kali Linux 或许不是你想要的。

In addition, misuse of security and penetration testing tools within a network, particularly without specific authorization, may cause irreparable damage and result in significant consequences, personal and/or legal. “Not understanding what you were doing” is not going to work as an excuse.

此外，在网络中对安全和渗透工具错误使用——特别是，没有经过特别授权——可能导致对个人或法律上的不可挽回的损坏和严重后果，

However, if you’re a professional penetration tester or are studying penetration testing with a goal of becoming a certified professional, there’s no better toolkit - at any price - than Kali Linux.

然而，如果你是一个专业的渗透测试人员或者以成为认证专家而正在学习渗透测试的学生，无论如何，你找不到不 Kali Linux 更好的工具包。

> If you are looking for a Linux distribution to learn the basics of Linux and need a good starting point, Kali Linux is not the ideal distribution for you. You may want to begin with [Ubuntu](https://www.ubuntu.com/), [Mint](https://www.linuxmint.com/), or [Debian](https://www.debian.org/) instead. If you’re interested in getting hands-on with the internals of Linux, take a look the [Linux From Scratch](https://www.linuxfromscratch.org/) project.
>
> 如果你需要一个 Linux 发行版来学习 Linux 基础并想要一个好的起点， Kali Linux 不是一个理想发行版。你或许可以从 [Ubuntu](https://www.ubuntu.com/), [Mint](https://www.linuxmint.com/) 或者 [Debian](https://www.debian.org/) 开始。如果你有兴趣从头构建 Linux 系统，请访问 [LFS](https://www.linuxfromscratch.org/) 。

### Summary | 总结

So, after having read this you should have figured out if Kali Linux is the distribution you were looking for or at least got an idea about your choice.

所以，在阅读完上面的内容后，你应该知道 Kali Linux 是不是你需要的发行版，或者至少对你的选择有了想法。

If still you have not figured it out, here is a summary that will hopefully remove your remaining doubts:

如果你还没有想明白，希望这份总结能够解开你的困惑。

+ Kali Linux is made with pentesters and pentesting in mind so, expecting it to fit with your necessity might not be as simple even though it’s completely possible.

   Kali Linux 是为了渗透测试而设计，希望能够满足你需求，这可能不容易，即使这是完全可能的。

+ If you are new to Linux or have less experience with command line you might find Kali Linux to be not so user-friendly, even though our developers try to make it as user-friendly as possible some things might be intimidating to you if you are new.

    如果你是 Linux 新手或者只有很少的命令行经验，你会发现 Kali Linux 对用户没有那么友好，尽管我们的开发人员尽可能让它对用户友好，但有些东西可能会劝退你。

+ The developers always try to make Kali Linux as much hardware compatible as possible but, still some hardware/s might not work as expected or not work at all. So, its better to research hardware compatibility beforehand rather than breaking your computer later.

    开发者总是尝试让 Kali Linux 尽可能兼容更多的硬件，但是仍然有一些硬件可能无法如预期一样工作，甚至可能完全不工作。所以，你最好提前检查硬件兼容性以免损坏你的计算机。

+ If you are installing Kali Linux for the first time, it is recommended to install first in Virtual Machine then, after getting familiar with it, you can install it in your own hardware.

    如果你是第一次安装 Kali Linux ， 建议先在虚拟机中安装，等你熟悉它之后再在硬件上安装。

Hopefully, now you know if you need to install Kali Linux or not. If you have decided to install Kali Linux then, we welcome you to our community.

希望，现在你知道你是否需要安装 Kali Linux 。如果准备安装 Kali Linux ，我们欢迎你加入我们的社区。

If not, then see you later, and remember always “Try Harder”.

如果你决定不安装 Kali Linux ，那就再见，永远记住 “再加把劲”。

Updated on: 2022-Jul-25
Author: [*g0tmi1k*](https://gitlab.com/g0tmi1k)

---

## Which Image Should I Download? |我该下载哪个镜像

In this section, we will describe the process of installing Kali Linux on 32-bit and 64-bit hardware using the images published on the Kali Linux download page.

在这部分，我们会讲解使用发布在 Kali Linux 页面上的镜像在 32 位和 64 位硬件上安装 Kali Linux 的过程。

### Content | 内容

+ [Which image to choose |选择哪个镜像](#which-image-to-choose-选择哪个镜像)
+ [Which desktop environment and software collection to choose during installation |在安装过程中选择哪种桌面环境以及软件集合](/kali_linux/docs/introduction/#which-desktop-environment-and-meta-packages-to-choose-during-installation-安装时选择哪个桌面环境和-元-软件包)

### Which Image to Choose |选择哪个镜像

The [Kali Linux download page](https://www.kali.org/get-kali/) offers different image types (**Installer**, **NetInstaller** and **Live**) for download, each available for both 32-bit and 64-bit architectures. Additionally, there is an [**Everything**]() flavor of the Installer and Live images, for 64-bit architectures only.

[Kali Linux 下载页](https://www.kali.org/get-kali/)提供不同的镜像（**Installer**, **NetInstaller** and **Live**），每种镜像都提供了 32 位和 64 位镜像。此外，还有包含所有工具包的安装程序和 Live 镜像，仅适用于 64 位架构。

If in doubt, use the “Installer” image. You will need to check your system architecture to know whether to get 32-bit or 64-bit. If you don’t know it, you’re best to research how to find out (As a rule of thumb, if your machine’s newer than 2005 you should be okay with amd64/x64/64-bit)

如有疑问，请使用 “Installer” 镜像。你需要知道你的系统架构是 32 位还是 64 位的。如果你不知道，你最好搞清楚（一般情况下，如果你的机器是 2005 年之后的，那应该是 amd64/x64/64-bit）

#### Installer

**This is the recommended image to install Kali Linux**. It contains a local copy of the [(meta)packages](https://www.kali.org/docs/general-use/metapackages/) listed (top10, default & large) so it can be used for complete offline installations without the need of a network connection.

**这是 Kali Linux 推荐的安装镜像**。它包含[(元)软件包]()（default 包和 large 包中的前 10 个）的本地拷贝，所以它可以完全离线安装而不需要网络连接。

This image cannot be used to boot a live system *(such as directly running Kali from a USB)*. It is only an installer image.

此镜像不能用于制作 Live 启动 *（比如：直接从U盘中启动 Kali）* 。它只是一个安装镜像。

#### NetInstaller

This image can be used if you want the latest package every time you install Kali Linux or the standard installer image is too big to download. This image is very small because it does not contain a local copy of [(meta)packages](https://www.kali.org/docs/general-use/metapackages/) to install. They will all be downloaded during installation, so as a result this requires a network connection which will slow down the installation time.

此镜像用于你希望每次安装 Kali Linux 时都能安装最新的软件包或者标准的安装程序太大不易于下载。此镜像非常小，因为它不包含[(元)软件包]()的本地拷贝。它们都会在安装的过程中下载，所以必须保持网络连接而且会拖慢安装速度。

Only use this image if you have reasons not to use the standard installer image above.

只有当你有特定的原因无法使用上面的标准安装程序时才使用此镜像。

This image cannot be used to boot a live system *(such as directly running Kali from a USB)*. It is only an installer image.

此镜像不能用于制作 Live 启动 *（比如：直接从U盘中启动 Kali）* 。它只是一个安装镜像。

#### Live

This image is for running Kali Linux without installing it first so it is perfect for running off a [USB drive](https://www.kali.org/docs/usb/) (or a CD/DVD).

此镜像用于不需要安装即可启动的 Kali Linux ，因此它非常适合用于运行于 [USB 设备]()（或者 CD/DVD）

You are able to install Kali Linux in its default configuration from this image but you will not be able to choose between desktop environments or to specify additional [(meta)packages](https://www.kali.org/docs/general-use/metapackages/) to install.

你可以从此镜像的默认配置安装 Kali Linux ，但你无法选择桌面环境，也无法指定[(元)软件包]()。

#### Everything

This image is meant for offline scenarios, when you want to use Kali Linux in a place that has no network connectivity. The image is huge (more than 9GB), as it contains nearly all of Kali’s tools already. It’s only available for the 64-bit architecture, and it can be downloaded via BitTorrent only.

此镜像适用于离线方案，你可以在一个无法连接网络的地方安装 Kali Linux 。此镜像非常大（超过 9GB），因为它几乎包含了 kali 已经拥有的所有软件包。它只适用于 64 位架构，而且只能通过 BitTorrent 下载。

Kali “everything” is not exactly an image, it’s a flavor. You can download either the **Installer Everything** image or the **Live Everything** image. In both case, all the tools are already there, no need for an Internet connection.

kali 的 “everything” 确切地说不是一个镜像，而是一个 flavor 。可以下载 **Installer Everything** 或者 **Live Everything** 镜像。不管哪种，都包含了所有的软件包，不需要网络连接。

### Which Desktop Environment and (Meta)Packages to Choose During Installation |安装时选择哪个桌面环境和(元)软件包

Each Kali Linux installer image *(not live)* allows the user to select the preferred “Desktop Environment (DE)” and software collection ([metapackages](https://www.kali.org/docs/general-use/metapackages/)) to be installed with operating system (Kali Linux).

每个 Kali Linux 安装镜像 *（不包括 live ）* 允许用户选择他们想要安装的“桌面环境”和软件集合（[元包]()）。

We recommend sticking with the default selections and add further packages after the installation as required. `Xfce` is the default desktop environment, and `kali-linux-top10` and `kali-linux-default` are the tools which get installed at the same time.

我们建议保持默认选择，并在安装结束后安装需要去安装软件包。`Xfce` 是默认的桌面环境， `kali-linux-top10` 和 `kali-linux-default` 是也会同时被安装。

![Kali Linux 安装界面](https://www.kali.org/docs/introduction/what-image-to-download/setup-default-metapackages.png)

At this screen, you may wish to not install a desktop environment, then Kali Linux becomes “headless” (no graphic interface) which uses less system resources up and commonly found on servers, dropboxes, low powered ARM devices, and the cloud. This is meant for people who are completely comfortable with the command line. You are able to install multiple Desktop Environments, allowing you to switch, we wouldn’t recommend it. You may change your mind and [switch desktop environments](https://www.kali.org/docs/general-use/switching-desktop-environments/) at a later date.

在这个界面，也许你希望不要安装桌面环境，Kali Linux 会变成无显示的（没有图形接口），这将会消耗更少的系统资源，一般用于服务器，dropbox，低功率的 ARM 设备和云。这适用于那些完全适应命令行的用户。你可以安装多个桌面环境并随意切换，我们不推荐如此做法。你应该改变你想法并在以后再切换桌面环境。

May wish to not to install any of the pre-defined software packages/bundles/collections ([metapackages](https://www.kali.org/docs/general-use/metapackages/)), giving you a finer degree of control of manually installing exactly what software you want. Alternatively you may want to be more prepared and install more than the default toolset. Please be aware, that there are more tools available in Kali which has be manually installed after the setup (as they all cannot be stored in the setup image).

你也许希望不安装任何预定义的软件包/捆绑/集合（[元包]()），这样你就可以更好地手动控制安装所需的软件。或者你希望安装比默认工具集更多的软件。请注意，有更多的工具可以在安装结束后手动安装（因为它们不可能都被保存在安装镜像里）。

Overall, these extra choices are for a more efficient installation experience, meant for advanced users. Please be aware of their pitfalls.

综上，这些额外的选项是为了适用于高级用户的更高效的安装体验。请注意可能存在的问题。

The following sections in the “Kali Documentation Installation” of this documentation, will be using the “Installer” image for the guides unless stated otherwise.

接下来在“Kali 安装文档”的单元里，如果没有特别说明，都是使用 “Installer” 镜像。

---

## Downloading Kali Linux |下载 Kali linux

{% note warning %}
IMPORTANT! Never download Kali Linux images from anywhere other than the official sources.
重要！永远不要从非官方源下载 Kali Linux 的镜像。
Always be sure to verify the SHA256 checksums of the file you’ve downloaded against our [official values](https://www.kali.org/docs/introduction/download-images-securely/).
永远记住校验 SHA256 值，确认你下载和文件的 SHA256 值和[官方值]()相同。
It would be easy for a malicious entity to modify a Kali installation to contain exploits or malware and host it unofficially.
对于一个恶意实体来说，修改 kali 安装文件以包含漏洞或者恶意软件是很容易的事。
{% endnote %}

### Where to Get Official Kali Linux Images |哪里能获取到 Kali Linux 镜像

#### ISO Files for Intel-based PCs |基于 Intel 芯片的 计算机所用的 ISO 文件

In order to run Kali “Live” from a [USB drive](https://www.kali.org/docs/usb/) on standard Windows and Apple PCs, you’ll need a Kali Linux [bootable ISO image](https://www.kali.org/docs/installation/), in either 32-bit or 64-bit format.

为了能在标准 windows 和苹果电脑中才 USB 设备运行 “Live” kali ，你需要一个 32 位或 64 位[可启动的 ISO 镜像]()。

If you’re not sure of the architecture of the system you want to run Kali on, on Linux or macOS, you can run the command:

如果你不确定你的系统所采用的架构，可以执行下面的这个命令：

```bash
uname -m
```

If you get the response, “x86_64”, use the 64-bit ISO image (the one containing “amd64” in the file name); if you get “i386”, use the 32-bit image (the one containing “i386” in the file name).

如果结果中含有 “x86_64” ，就用 64 位 ISO 镜像（文件名里包含 “amd64” 的那个）；如果结果中含有 “i386” ，就用 32 位 ISO 镜像（文件名中包含 “i386” 的那个）。

If you’re on a Windows system, the procedure for determining whether your architecture is [detailed on Microsoft’s website](http://windows.microsoft.com/en-us/windows7/find-out-32-or-64-bit).

如果你使用的是 windows 系统，如何确定你的系统架构，请访问[微软官网站](http://windows.microsoft.com/en-us/windows7/find-out-32-or-64-bit)。

The Kali Linux images are available both as directly downloadable “.iso/.img” files or via “.torrent” files.

Kali Linux 镜像可以直接下载 “.iso/.img” 文件或者通过 “.torrent” 文件下载。

+ [Official Kali ISOs for Intel-based PCs](https://www.kali.org/get-kali/)

Building your own Kali Linux ISO, standard or customized, is [a very simple process](https://www.kali.org/docs/development/live-build-a-custom-kali-iso/).

标准化和定制化构建你自己的 Kali Linux ISO 文件是一个[非常简单的过程]()。

#### Virtual Machines Images |虚拟机镜像

If you want to run Kali Linux as a “guest” under [VMware or VirtualBox](https://www.kali.org/docs/virtualization/), Kali Linux is available as a pre-built virtual machines with any guest tools already installed. These image are available in a 64-bit (amd64), and 32-bit PAE (i*86) formats.

如果你想要将 Kali Linux 作为 [VMware 或者 VirtualBox]() 的客户机使用，Kali Linux 拥有安装了一些客户机软件的预构建的虚拟机。这些镜像支持 64 位和 32 位格式。

+ [Official Kali Linux VMware and VirtualBox Images](https://www.kali.org/get-kali/#kali-virtual-machines)

#### ARM Images | Arm 镜像

The hardware architectures of [ARM-based devices](https://www.kali.org/docs/arm/) vary considerably, so it is not possible to have a single image that will work across all of them. Pre-built Kali Linux images for the [ARM architecture](https://www.kali.org/get-kali/) are available for a wide range of devices.

基于 [ARM 架构]()的设备硬件差异非常大，所以不太可能有一个镜像能够运行在所有的设备上。为了 [ARM 架构](https://www.kali.org/get-kali/)预构建的 Kali Linux 镜像在一大众设备上都是可用的。

Scripts for building your own ARM images locally are also [available on GitLab](https://gitlab.com/kalilinux/build-scripts/kali-arm). For more details, see the articles on [setting up an ARM cross-compilation environment](https://www.kali.org/docs/development/arm-cross-compilation-environment/) and [building a custom Kali Linux ARM chroot](https://www.kali.org/docs/development/kali-linux-arm-chroot/).

用于本地自行构建 ARM 架构镜像的脚本请访问 [GitLab](https://gitlab.com/kalilinux/build-scripts/kali-arm)。更详细的信息请查看 [setting up an ARM cross-compilation environment](https://www.kali.org/docs/development/arm-cross-compilation-environment/) 和 [building a custom Kali Linux ARM chroot](https://www.kali.org/docs/development/kali-linux-arm-chroot/)。

### Verifying Your Downloaded Kali Image | 验证你下载的 kali 镜像

#### Why do I need to do this? | 为什么我需要这么做?

Before you run Kali Linux Live, or install it to your hard disk, you want to be very sure that what you’ve got actually is Kali Linux, and not an imposter. Kali Linux is a professional penetration testing and forensics toolkit. As a professional penetration tester, having absolute confidence in the integrity of your tools is critical: if your tools are not trustworthy, your investigations will not be trustworthy, either.

在运行 Kali Linux Live 或者将 Kali Linux 安装到硬盘之前，你需要非常确认你下载的确实是 Kali Linux ，而不是一个冒牌货。 Kali Linux 是一个渗透测试和取证的工具集。作为一名职业的渗透测试工程师，对你的工具的可靠性有绝对的信心是一种非常危险的想法：如果你的工具不可信，那么的调查也就不可信。

Moreover, as the leading penetration testing distribution, Kali’s strengths mean that a bogus version of Kali Linux could do a tremendous amount of damage if it were deployed unwittingly. There are plenty of people with plenty of reason to want to stick very sketchy stuff into something that looks like Kali, and you absolutely do not want to find yourself running something like that.

此外，作为领先的渗透测试发行版，kali 的优势意味着如果在不知情的情况下部署了一个伪造的 Kali Linux 可能造成巨大的损坏。有许多人有许多理由想要将一些未经过完整性检查的东西塞进 kali 中，而你绝对不想发现你自己就在运行着这些东西。

Avoiding this is simple:
简单地避免这些情况：

+ Only download Kali Linux via the official download page at [kali.org/get-kali/](https://www.kali.org/get-kali/) - you will not be able to browse to these pages without SSL; encrypting the connection makes it much harder for an attacker to use a “man-in-the-middle” attack to modify your download. There are a few potential weaknesses to even these sources - see the sections on verifying the download with the SHA256SUMS file and its signature against the official Kali Development team private key for something much closer to absolute assurance.

    仅从 Kali Linux [官方下载页面](https://www.kali.org/get-kali/) 下载 Kali Linux —— 你将无法在不通过 SSL 的情况下浏览这些页面；加密连接使得攻击者更难通过发动中间人攻击篡改你的下载。即使是这些来源，也存在一些潜在的弱点——请参阅有关使用 SHA256SUMS 文件验证下载，它是 Kali 官方开发团队使用私钥签名的，以此来获得更接近绝对保证的内容。

+ Once you’ve downloaded an image, and before you run it, always validate that it really is what it’s supposed to be by verifying its checksum using one of the procedures detailed below.

    下载镜像后，在你运行它之前，通过下面提供的方法之一验证其校验值以保证它的完整性。

There are several methods for verifying your download. Each provides a certain level of assurance, and involves a corresponding level of effort on your part. We list 3 of these methods below:

有几种方法来验证你的下载。每种方法都提供了一定程度的保证，并涉及你的相应程度的付出。我们在下面列举了3中方法：

1. You can download an ISO image from an official Kali Linux “Downloads” mirror, calculate the ISO’s SHA256 hash and compare it by inspection with the value listed on the Kali Linux site. This is quick and easy, but potentially susceptible to subversion via a DNS poisoning: it assumes that the site to which, for example, the domain “kali.org” resolves is in fact the actual Kali Linux site. If it somehow were not, an attacker could present a “loaded” image and a matching SHA256 signature on the fake web page. See the section [“Manually Verify the Signature on the ISO (Direct Download)”](), below.

    你可以通过 Kali Linux 官方下载镜像下载 ISO 镜像，计算 ISO 的 SHA256 哈希值然后和 Kali Linux 网站上列出的值进行对比。这很快而且很容易，但是这也可能因为DNS缓存中毒而遭到破坏：DNS 会呈现你访问的站点，比如："kali.org", 那个真的 Kali Linux 站点。如果你访问的不是真的站点，攻击者就能在假的网站上发布一个加载了恶意软件的镜像并发布与之匹配的 SHA256 签名。访问下面的 [手动校验 ISO 签名(直接下载)]() 。

2. You can download an ISO image through the torrents, and it will also pull down a file - unsigned - containing the calculated SHA256 signature. You can then use the shasum command (on Linux and macOS) or a utility (on Windows) to automatically verify that the file’s computed signature matches the signature in the secondary file. This is even easier than the “manual” method, but suffers from the same weakness: if the torrent you pulled down is not really Kali Linux, it could still have a good signature. See the section “Verify the Signature on the ISO Using the Included Signature File (Torrent Download)”, below.

    你可以通过 torrents 下载 ISO 镜像，同时会下载一个未签名的包含计算出的 SHA256 值的签名文件。你可以通过 `shasum` 命令(在 Linux 和 macOS 中)或者程序(在 windows 上) 自动校验 ISO 文件的计算出的签名和第二个文件中的签名是否一致。这比手动的方法更容易，但是它有同样的弱点：如果你下载的 torrents 并非 Kali Linux，它依然被很好的签名了。请看下面的 [使用包含的签名文件校验 ISO 签名(Torrent 下载)]()

+ To be as close to absolutely certain as possible that the Kali Linux download you’ve obtained is the real thing, you can download both a cleartext signature file and and version of the same file that has been signed with the official Kali Linux private key and use GNU Privacy Guard (GPG) to first, verify that the computed SHA256 signature and the signature in the cleartext file match and second, verify that the signed version of the file containing the SHA256 hash has been correctly signed with the official key.

    为了尽可能保证你你下载 Kali Linux 是真的 Kali Linux ，你可以下载明文的签名文件和使用 Kali Linux 官方私钥签名的且使用了 GPG 签名的相同文件。首先，校验计算出的 SHA256 签名和明文签名文件一致，然后，校验签名的文件包含的 SHA256 哈希值被相同的官方密钥签名。

If you use this more complicated process and successfully validate your downloaded ISO, you can proceed with pretty complete assurance that what you’ve got is the official image and that it has not been tampered with in any way. This method, while the most complex, has the advantage of providing independent assurance of the integrity of the image. The only way this method can fail is if the official Kali Linux private key is not only subverted by an attacker, but also not subsequently revoked by the Kali Linux development team. For this method, see the section on [verification using the SHA256SUMS file]().

如果你使用了这个更加复杂的方式验证了你下载的 ISO，你可以完全保证你获得了没有被篡改的官方镜像。这种复杂的方法，在提供独立的完整性检查上更具优势。这种方法失效的唯一可能就是 Kali Linux 官方的私钥不仅被攻击者破坏，而且之后没有被 Kali Linux 开发团队废除。请看 [使用 SHA256SUMS 文件校验]()

<!-- ## Download Kali Linux Images Securely

## Kali's Default Credentials

## Kali Undercover

## Kali Press Release

## Kali Linux History

## Kali ARM History

## Kali NetHunter History -->