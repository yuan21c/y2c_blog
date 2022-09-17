---
title: Kali Linux 官方文档 —— Introduction
date: 2022-09-13 14:51:33
updated: 2022-09-13 14:51:33
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

## Which Image Should I Download?

## Downloading Kali Linux

## Download Kali Linux Images Securely

## Kali's Default Credentials

## Kali Undercover

## Kali Press Release

## Kali Linux History

## Kali ARM History

## Kali NetHunter History
