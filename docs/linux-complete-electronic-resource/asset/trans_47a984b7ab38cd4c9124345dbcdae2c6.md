

# 第三部分 网络

![](img/a3584dae761d2e3abed8bf40d7637389_186_0.png)

## 第 7 章
### 网络概览

本章提供了 Linux 网络功能的完整概览。每个功能或可用的软件包都会进行简要描述，并指向更多信息以及工具本身。

每次遇到新的网络相关问题时，你都可以将本章作为参考。如今使用 Linux 的人非常多，因此肯定已经有人遇到过同样的问题，而且得益于 Linux 社区的精神，他们很可能已经与所有人分享了他们的解决方案。如果是这样，这里可能会有相关描述。

> “网络概览”重印自 1998 年 7 月 10 日的《Linux 网络概览 HOWTO》，版本 0.2，作者为 Daniel López Ridruejo。

### 简介

本文档旨在概述 Linux 操作系统的网络功能。虽然 Linux 的优势之一在于几乎每个主题都有大量的信息可供查阅，但其中大多数都侧重于实现细节。大多数新用户，特别是那些来自 Windows 环境的人，并不了解 Linux 的网络可能性。本文档旨在通过简要描述每一种可能性以及进一步信息的指引，展示这些可能性的总体图景。信息汇集自许多来源：HOWTO、FAQ、项目的网页以及我个人的实践经验。我们向作者们致敬。没有他们和他们的程序，本文档既不可能存在，也没有存在的必要。

### 什么是 Linux？

Linux 的主要作者是 Linus Torvalds。自他的原始版本以来，无数的人对它进行了改进。它是对 Unix 操作系统的一个克隆，完全从头开始编写。关于 Linux 一个更有趣的事实是，开发是在全球范围内同时进行的。

Linux 在 GNU 通用公共许可证条款下进行版权保护（见附录 D）。这是由自由软件基金会（FSF）编写的一种许可证，旨在防止人们限制软件的分发。简而言之，虽然可以为副本收费，但接收副本的人不能被阻止免费将其分发。这也意味着源代码必须是可用的。这对程序员很有用。任何人都可以修改 Linux，甚至可以分发他的/她的修改版本，前提是他们保持代码在相同的版权下。

### 是什么让 Linux 与众不同？

为什么要使用 Linux？Linux 通常比其他操作系统更便宜（或者至少不更贵），而且比许多商业系统更少出现问题。但让 Linux 与众不同的不是它的价格（毕竟，如果一个操作系统不够好，即使它是免费的，谁又想要呢？），而是其出色的功能：

- Linux 是一个真正的 32 位多任务操作系统，健壮且功能强大，足以被从大学到大型企业的各种组织使用。
- 它可以从低端的 386 机器运行到研究中心中大规模的超并行机器。
- 有现成的 Intel/ Sparc/ Alpha 架构版本，并且对 Power PC 和嵌入式系统（如 SGI, Ultra Sparc, AP1000+, Strong ARM, MIPS R5000/R4000 等）提供实验性支持。
- 最后，谈到网络时，Linux 是首选。不仅因为网络与操作系统本身紧密集成，且有大量应用程序可以免费获取，还因为其在重负载下的健壮性，这是仅在开源项目中经过多年调试和测试后才能实现的。

## 网络协议

Linux 支持许多不同的网络协议。

### TCP/IP

互联网协议最初是在二十年前为美国国防部（DoD）开发的，主要目的是连接不同品牌的计算机。TCP/IP 协议套件通过其分层结构，实现了应用程序与网络硬件的隔离。

虽然基于分层模型，但它更侧重于提供互连性，而不是严格遵循功能层。这是 TCP/IP 成为事实上的标准互联网协议而非 OSI 的原因之一。

TCP/IP 网络自 Linux 诞生之初就已存在。它是从头开始实现的。它是最健壮、快速且可靠的实现之一，也是 Linux 成功的关键因素之一。

### TCP/IP 版本 6

IPv6，有时也称为 IPng（下一代 IP），是 IPv4 协议的升级版本，解决了许多问题。这些问题包括：可用 IP 地址短缺、缺乏处理对时间敏感流量的机制、缺乏网络层安全性等。

地址空间的增加将伴随着扩展的寻址方案，这将对路由性能产生巨大影响。Linux 已经有一个 beta 版本的实现，预计在生产版本中，将随 2.2.0 Linux 内核发布。Linux IPv6 HOWTO 可以在 http://www.terra.net/ipv6/linux-ipv6.faq.html 找到，IPv6 主页可以在 http://playground.sun.com/pub/ipng/html/ipng-main.html 找到。

### IPX/SPX

IPX/SPX（互联网数据包交换/排序数据包交换）是 Novell 开发的一个专有协议栈，基于 Xerox 网络系统（XNS）协议。IPX/SPX 在 20 世纪 80 年代初随着 Novell Inc. 的 NetWare 成为重要部分而声名鹊起。NetWare 成为第一代局域网的事实标准网络操作系统（NOS）。Novell 通过商务导向的应用套件和客户端连接工具来补充其 NOS。

Linux 有一个非常干净的 IPX/SPX 实现，允许其被配置为：

- IPX 路由器
- IPX 网桥
- NCP 客户端和/或 NCP 服务器（用于文件共享）
- Novell 打印客户端，Novell 打印服务器

它还具有启用以下功能的能力：

- PPP/IPX，允许 Linux 机器充当 PPP 服务器/客户端
- 通过 IP 进行 IPX 隧道，允许通过仅支持 IP 的链路连接两个 IPX 网络

此外，Caldera（http://www.caldera.com）提供在 Linux 下对 Novell NetWare 的商业支持。Caldera 提供一个功能齐全的 Novell NetWare 客户端，基于从 Novell 公司获得技术许可构建。

该客户端提供对 Novell 3.x 和 4.x 文件服务器的完整客户端访问，并包含诸如 NetWare 目录服务（NDS）和 RSA 加密等功能。关于 IPX 的 HOWTO 可以在 http://MetaLab.unc.edu/mdw/HOWTO/IPX-HOWTO.html 找到。

### AppleTalk 协议套件

AppleTalk 是 Apple 的互联网协议栈的名称。它允许一种点对点网络模型，提供文件和打印机共享等基本功能。每台机器可以同时充当客户端和服务器，且所需的软件和硬件都包含在每台 Apple 计算机中。

Linux 提供完整的 AppleTalk 网络支持。Nettalk 是 AppleTalk 协议套件的内核级实现，最初为基于 BSD 的系统设计。它包括对路由 AppleTalk 的支持，通过 AFP（AppleShare）提供 Unix 和 AFS 文件系统服务，以及通过 PAP 提供 Unix 打印机和访问 Apple/Talk 打印机。

### 广域网网络：X.25, 帧中继等。

多家第三方为 Linux 提供 T-1, T-3, X.25 和帧中继产品。通常这些类型的连接需要特殊的硬件。提供硬件的供应商也提供支持协议驱动程序。你可以在 http://www.secretagent.com/networking/wan.html 找到 Linux 的广域网资源。

### ISDN

Linux 内核内置了 ISDN 功能。Isdn4linux 控制 ISDN PC 卡，并可以使用 Hayes 命令集（“AT”命令）模拟调制解调器。其可能性范围从使用终端程序，到通过 HDLC（使用包含的设备）进行连接，到通过 PPP 完全连接到互联网，再到音频应用。你可以在 http://tsikora.tiac.net/i41-faq-eng-i41-faq.html 找到 isdn4linux 的 FAQ。

### PPP, SLIP, PLIP

Linux 内核内置了对 PPP（点对点协议）、SLIP（串行线 IP）和 PLIP（并行线 IP）的支持。PPP 是最流行的

