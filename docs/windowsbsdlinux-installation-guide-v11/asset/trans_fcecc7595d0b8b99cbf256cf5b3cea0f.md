

OpenBSD 3.2-RELEASE 或 NetBSD 1.6.1 最后通过安装 Red Hat Linux 7.3 (Valhalla) 完成。GNU GRUB 是用于启动这三个操作系统的引导加载程序。

## 1.3 多启动的利弊

“嘿！双启动和多启动计算机系统只有优点绝对没有缺点”这样的想法或观点是错误的。读者经常会问的一个重要问题是：在哪里多启动 PC 才有意义？这个问题答案很简单：多启动系统只有在你想要尝试的配置数量（或操作系统总体）超过你拥有的电脑数量，并且更重要的是数据不会有风险的情况下才有意义。

让我们考虑这样一种情况：Peter 家里有一台运行 Slackware Linux 的单台 PC。他的所有重要文档和从互联网下载的文件都存储在上面。现在他决定学习和练习破解 FreeBSD 内核。因此，他决定将他的 PC 变成双启动系统。将唯一或换句话说，家庭或工作中的主要 PC 转换为双启动或多启动系统是一个糟糕的选择。如果主要家庭 PC 必须用作双启动或多启动系统，更安全的做法是添加一块第二硬盘并让第一块基本保持不变。像 GRUB 这样强大的引导加载程序将允许从另一块硬盘启动。

我大学的计算机科学系有 15 个用于不同目的的实验室，运行的硬件从 i386 到 Sun SPARCs 不等。在数据和安全绝对重要时，计算机只运行一个操作系统，无论是 Windows 2000 Professional、Red Hat Linux、Slackware、FreeBSD 还是 Sun Solaris。然而，我们确实有大约 10–12 台 PC 的“测试实验室”，其中我们有运行 ASP Linux、Red Hat Linux、Slackware、Windows 2000 Professional、FreeBSD 等的双启动和多启动系统。这可以被视为理想情况。

## 1.4 假设列表

尽管从最基础开始解释了每个必要的步骤，但编写本指南时仍考虑了一些重要假设，其中包括：

- 1. 读者拥有使用 Microsoft fdisk、BSD 风格分区表编辑器、Linux fdisk 等对硬盘进行分区划分的理论和实践经验。
- 2. 理解硬盘几何结构、主分区概念、扩展分区、扩展分区内的逻辑磁盘；Linux 磁盘命名和分区方案，BSD 风格磁盘标记和分区方案。
- 3. 拥有编译和配置自定义 Linux 和 BSD 内核的理论和实践经验。
- 4. 了解 Linux 和 FreeBSD/OpenBSD/NetBSD 操作系统通用的基本 Unix 命令。例如，挂载文件系统，编辑配置文件如 Linux 上的 /boot/grub/grub.conf 以及其他此类琐碎任务。
- 5. 读者使用的是 Intel x86 计算机系统。我将在 IA32 平台上安装 Windows、FreeBSD/OpenBSD/NetBSD 和 Linux 操作系统。
- 6. 读者使用的是其 BIOS 支持逻辑块寻址 (LBA) 模式表示磁盘上数据的硬盘。通过使用 LBA 模式，旧硬盘上的 1024 柱面限制问题得以解决。

如果你还不了解其中一些内容，不用担心，继续阅读，因为最重要的步骤将在后续章节中根据需要详细解释。无论如何，在继续之前，请确保浏览本指南的常见问题解答 (FAQ) 部分。

## 1.5 致谢

我谨向以下所有人员和项目表示感谢，没有他们的帮助和积极参与，本文件就不可能实现。其中包括：

- 1. Guyhem Aznar <guylhem at metalab dot unc dot edu>，TLDP 的首席协调员、主要联系人，使本指南成为可能。
- 2. Tabatha Persad <tabatha at merlimonroe dot com>，Linux 文档项目评审协调员，负责技术评审并回答我的无数疑问。
- 3. Michael K. Johnson <johnsonm at redhat dot com>，提供其在 TLDP 网站上的“Linux 信息表”摘录，本指南第 1 章关于 Linux 的内容中提到了该表。
- 4. Microsoft Corporation 提供本指南第 2 章中提到的 Microsoft 工具和技术的重要信息。
- 5. 每一位开源社区贡献者和我世界各地的朋友们。

此外，在编写本指南时，我查阅了以下印刷书籍、在线期刊、杂志和官方论文：

- 1. Modern Operating Systems，作者 Andrew S. Tanenbaum
- 2. Understanding the Linux Kernel，作者 Daniel P. Bovet，Marco Cesati
- 3. Red Hat Linux 8 Bible，作者 Christopher Negus
- 4. Red Hat Linux Official x86 Installation Guides at http://www.redhat.com
- 5. Linux Gazette 和 Linux Focus 在线杂志分别位于 http://www.linuxgazette.com 和 http://www.linuxfocus.org。
- 6. The FreeBSD Handbook at http://www.freebsd.org
- 7. The FreeBSD FAQ at http://www.freebsd.org
- 8. The OpenBSD FAQ at http://www.openbsd.org
- 9. The Official Microsoft Windows Installation Guides and FAQs at http://www.microsoft.com

## 1.6 法律声明

商标归其所有者所有。

尽管本文档中的信息被认为正确，但作者不对本文档内容承担任何责任。请自行承担风险使用本文档中提供的提示和示例。

Copyright (c) 2003, Subhasish Ghosh

