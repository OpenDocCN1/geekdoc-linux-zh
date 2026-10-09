

## 目录

- 引言 1
    - 本书适合谁？ 1
    - 使用本书所需的条件 2
    - 什么是 Linux？ 2
    - 本书涵盖的内容 6
    - 本书中的约定 8
    - 客户支持 9
- 1. 安装 Red Hat Linux 9 13
    - 为安装做准备 14
    - 安装过程 18
- 2. Red Hat Linux 9 基础知识 47
    - 在桌面上移动 48
    - 文件系统 58
    - 管理硬件 70
    - 配置桌面 83
    - 管理用户 92
- 3. 连接互联网 97
    - 连接互联网 97
    - 管理多个 IP 地址和连接 108
    - 软件与配置 112
- 4. 安装软件 125
    - 什么是 RPM？ 126
    - RPM 命令行工具 134
- 5. 日常应用 151
    - 办公应用 152
    - 互联网应用 170
    - 个人信息管理 175
    - 多媒体应用 184
    - 系统应用 195
- 6. Shell 203
    - Shell 作为命令行界面 203
    - 内置程序与外部程序 205
    - 一些常用的 Shell 命令 206
    - 特殊按键与快捷键 217
    - 命令行语法 222
    - 配置 Shell 229
    - 管理任务 230
    - Shell 脚本 234
- 7. 文件系统 241
    - 什么是文件系统？ 241
    - 文件搜索工具 256
    - 在文件系统中导航 265
    - 管理磁盘驱动器和分区 272
    - 文件系统维护 283
- 8. 管理你的用户账户 287
    - 不同用户账户的用途 288
    - Red Hat 用户管理器 290
    - Linux 如何存储用户账户信息 296
    - 高级用户账户管理 302
    - 高级用户组管理 313
    - 用户、用户组和文件系统权限 315
    - 何时不需要 Root 权限 321
    - 谁已登录？ 329
- 9. 构建网络 333
    - 网络 334
    - 设置 Web 服务器 340
    - 设置 FTP 服务器 350
    - 设置打印服务器 360
    - 设置文件服务器 366
    - 设置邮件服务器 383
    - 设置 DHCP 服务器 394
- 10. 高级系统管理 405
    - 系统配置 406
    - 日志记录 415
    - 备份与归档 421
    - 从源代码构建 432
    - 重建 Linux 内核 439
- 11. 使用 Perl 管理系统 453
    - 什么是 Perl？ 454
    - 安装 457
    - 学习 Perl 460
    - 最后…… 496
- 12. 安全性 499
    - 什么是计算机安全？ 499
    - 对抗威胁 502
    - 硬件 502
    - 本地安全 504
    - 保持软件更新 512
    - 监控安全性 513
    - 网络安全 525
    - 如何获取更多资源 547
- 13. 接下来怎么办？ 549
    - 在线资源与许可方案 550
    - 系统管理应用 553
    - 开发应用 558
- 索引 571
- GNU 通用公共许可证 591

# 引言

Linux 正在迅速成为世界操作系统领域的主要力量——它速度快、稳定性高，而且最重要的是，它是免费可用的。在 Linux 市场中，Red Hat Linux 拥有最流行发行版的殊荣，而使用 Red Hat Linux 9，它的安装和使用比以往任何时候都更容易！

本书教你安装、配置、使用和维护 Red Hat Linux 系统所需知道的一切。它是专门为 Red Hat Linux 9 编写的，但如果你计划使用其较旧的版本 Red Hat Linux 8.0 以及任何后续版本的 Red Hat Linux，你会发现它也是一份非常实用的指南。

## 本书适合谁？

本书主要面向那些第一次使用（或计划使用）Red Hat Linux 操作系统的读者。它提供了简单、直白的指导，帮助你开始探索开源软件的巨大潜力。

我们假设读者在接触 Linux 之前已经熟悉使用操作系统，例如 Apple 的 Macintosh、Unix 或众多版本的 Microsoft Windows 操作系统。了解文件系统、应用程序以及用户和权限等概念会有帮助，但并非必需；本书将为那些尚未考虑过这些概念的读者提供见解。

本书不假设读者具备任何 Linux 的先前知识。

## 使用本书所需的条件

使用本书，你只需要一台**机器**和一份 Red Hat Linux 9 **发行版**。最简单的选项（也是我们在本书中使用的选项）需要：

- 一台你可以专门用于安装 Red Hat Linux 9 的机器。Red Hat 建议最低配置为 Pentium 级别 CPU，配有 650MB 硬盘空间和 128MB 内存，但为了获得更好的性能，推荐 200MHz Pentium 处理器，配有 2.5GB 硬盘空间和 192MB 内存。它还表示，过去两年内制造的大多数工厂组装机器都兼容 Red Hat Linux 9，许多较旧的机器也兼容。（有关硬件兼容性的更多信息，请参见第 1 章和 http://hardware.redhat.com。）
- 随本书附带的一份 Red Hat Linux 9 副本。

### 其他替代方案

获取 Red Hat Linux 9 发行版还有其他方法。你可以：

- 通过 FTP 免费下载 Red Hat Linux 9 发行版镜像，并将其刻录到 CD 上。然而，这相当复杂——例如，你需要一个 ISO 刻录软件（这是一种在将 ISO 文件刻录到你选择的介质时解包 ISO 文件的软件）。如果你觉得有挑战性，请遵循 http://www.redhat.com/download/howto_download.html 上的指南；该发行版在全球多个镜像站点均可获得。
- 从第三方供应商处以低价购买安装光盘。然而，这些光盘通常不提供技术支持，也没有文档。

也可以将 Red Hat Linux 9 作为双启动设置的一部分安装在你的机器上。如果你只有一台机器，并且不想放弃你的 Windows 或其他操作系统，这将给你一个选择。

虽然欢迎探索这些替代方案，而且它们与你在本书中发现的内容完全兼容，但我们不会详细讨论它们。

# 什么是 Linux？

当你问一个 Linux 爱好者这个问题时，他们的答案几乎总会提到 Linus Torvalds 和开源社区。正如你将在我们简要的历史中看到的那样，Linux 在 Linux 的创建和发展中是一个关键角色，而 Linux 的开源根源是其受欢迎程度的核心。

## Linus Torvalds 和 Linux 的诞生

Linus Benedict Torvalds 当时在芬兰的赫尔辛基大学学习，他对计算的兴趣导致他对操作系统以及如何在当时的现有系统——特别是各种 Unix 衍生系统——上做出改进感到好奇。随着这一小步，Linux 内核（其核心）的开发开始了；并在 1991 年 10 月，版本 0.02 通过以下这一著名的帖子发布到互联网上：

> From: torvalds@klaava.Helsinki.FI (Linus Benedict Torvalds)
> Newsgroups: comp.os.minix
> Subject: Free minix-like kernel sources for 386-AT
> Message-ID: <1991Oct5.054106.4647@klaava.Helsinki.FI>
> Date: 5 Oct 91 05:41:06 GMT
> Organization: University of Helsinki
>
> Do you pine for the nice days of minix-1.1, when men were men and wrote their own device drivers? Are you without a nice project and just dying to cut your teeth on an OS you can try to modify for your needs? Are you finding it frustrating when everything works on minix? No more all-nighters to get a nifty program working? Then this post might be just for you :-)
>
> As I mentioned a month(?) ago, I'm working on a free version of a minix-lookalike for AT-386 computers. It has finally reached the stage where it's even usable (though may not be depending on what you want), and I am willing to put out the sources for wider distribution. It is just version 0.02 (+1 (very small) patch already), but I've successfully run bash/gcc/gnu-make/gnu-sed/compress etc under it.
>
> Sources for this pet project of mine can be found at nic.funet.fi (128.214.6.100) in the directory /pub/OS/Linux.
>
> The directory also contains some README-file and a couple of binaries to work under linux (bash, update and gcc, what more can you ask for :-). Full kernel source is provided, as no minix code has been used. Library sources are only partially free, so that cannot be distributed currently. The system is able to compile "as-is" and has been known to work. Heh. Sources to the binaries (bash and gcc) can be found at the same place in /pub/gnu.

这听起来并不像那种你可以用来处理家庭账户的系统，对吧？然而，关于这个软件发布有一个非常重要的一点：它是根据 **GNU 通用公共许可证** 发布的，该许可证允许源代码免费分发给任何想要它的人，并且允许这些人随意扩展它。

很快，感兴趣的程序员和测试员群体采用了 Linus 的原始代码，并以各种方式对其进行扩展。他们扩展了 Linux 可以运行的硬件配置范围，增加了为 Linux 编写的软件范围，并提高了整个 Linux 系统的稳定性。这种支持和开发一直持续到今天，遍布全球并涵盖了整个开发者社区。

