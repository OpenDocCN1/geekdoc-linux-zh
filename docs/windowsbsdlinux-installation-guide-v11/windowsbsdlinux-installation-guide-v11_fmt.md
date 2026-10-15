
# Windows+BSD+Linux 安装指南, v1.1

## 修订历史

- v1.0：初始发布，由Linux文档项目（LDP）审阅。做了一些结构性更改和小的修正；新增了“故障排除”和“安装OpenBSD 3.2-RELEASE”两章。
- v1.1：进行了修正并添加了信息。FreeBSD -RELEASE的信息已更新至4.8-RELEASE。新增“安装NetBSD 1.6.1”一章，并对本指南做了一些小的修改。

> 欢迎！本文档说明了如何在一台计算机的同一块硬盘上安装和配置三种不同的操作系统。读者可以从以下组合中选择：Microsoft Windows 95/98（第二版）/Millennium版（ME）/NT/2K/XP + FreeBSD 4.8-RELEASE/OpenBSD 3.2-RELEASE/NetBSD 1.6.1 + Linux。本文仅讨论Intel架构的多重引导，并且GNU GRUB是首选引导加载程序。如果您有任何问题或评论，欢迎通过电子邮件与我联系，邮箱地址：subhasish_ghosh@linuxwaves.com。谢谢！

注意：在“内容组织”部分，读者必须选择执行第3章、第4章或第5章。

## 目录

1. 引言
2. 常见问题解答（FAQ）
3. 内容组织
4. 故障排除
5. 结论

## 1. 引言

### 1.1 本指南的目的

虽然我们中的许多人在日常工作中更喜欢在个人电脑上只使用一个操作系统，但有时我们可能希望在同一台计算机上安装两个或更多的操作系统。假设您需要使用MATLAB 6.0进行工程应用；使用PHP设计、编程和实现一个网站，并使用MySQL作为后端数据库（作为企业级公寓开发项目的一部分）；同时还要学习如何使用IPFW配置包过滤防火墙。恰巧，MATLAB软件运行在Microsoft Windows平台上，您想将MySQL数据库部署在Linux操作系统上，最后但同样重要的是，您大学的教授正在使用FreeBSD操作系统软件教授“如何使用IPFW配置包过滤防火墙”。在这种情况下，您可以放心地采用“多重引导”机制，当然也可以不时参考本指南。

本文档以指南的形式呈现，旨在帮助那些信奉“在做中学”方法的Windows、Linux和FreeBSD/OpenBSD/NetBSD用户。多系统引导并非一门精确的科学。你偶然发现一篇文档，阅读它，觉得有趣，自己动手实践，犯错误，然后最终达到预期的目标。这就是你应该学习的方式。我就是这样学会的。Unix专家们很久以前也是这样学会的。当读者读完本指南时，他将会清楚地理解在同一台计算机的硬盘上成功安装和配置三种不同操作系统所需的基本主题。我已尽最大努力以清晰、易于理解的简单语言来描述每一个主题。

互联网上提供的大多数安装HOWTO和指南（适用于Linux、FreeBSD和OpenBSD操作系统）都不完整，因为它们预设了太多的前提，让读者自己去做大部分困难的工作。在本指南中，我逐步演示每一个步骤，从而使整个过程变得简单易懂。

### 1.2 什么是多重引导？

Bryan Pfaffenberger编著的《韦氏新世界计算机词典》（第9版）将“双引导”一词定义为：“一台允许用户在启动时从两个操作系统之间进行选择的计算机”。确实如此。将此定义作为我们的基础，我们可以构建自己对“多重引导”（简称多引导）系统的定义，即：一台允许用户在启动时从两个以上操作系统之间进行选择的计算机。

本文档说明了如何在同一台计算机的硬盘上成功安装和配置三种不同的操作系统，从而使其成为“多引导”系统。本说明所选的操作系统包括：Microsoft Windows 95/98（第二版）/Millennium版（ME）/NT/2K/XP、FreeBSD 4.8-RELEASE/OpenBSD 3.2-RELEASE/NetBSD 1.6.1和Red Hat Linux 7.3。

我将首先安装Microsoft Windows操作系统，然后安装FreeBSD 4.8-RELEASE或OpenBSD 3.2-RELEASE 或 NetBSD 1.6.1 最后通过安装 Red Hat Linux 7.3 (Valhalla) 完成。GNU GRUB 是用于启动这三个操作系统的引导加载程序。

### 1.3 多启动的利弊

“嘿！双启动和多启动计算机系统只有优点绝对没有缺点”这样的想法或观点是错误的。读者经常会问的一个重要问题是：在哪里多启动 PC 才有意义？这个问题答案很简单：多启动系统只有在你想要尝试的配置数量（或操作系统总体）超过你拥有的电脑数量，并且更重要的是数据不会有风险的情况下才有意义。

让我们考虑这样一种情况：Peter 家里有一台运行 Slackware Linux 的单台 PC。他的所有重要文档和从互联网下载的文件都存储在上面。现在他决定学习和练习破解 FreeBSD 内核。因此，他决定将他的 PC 变成双启动系统。将唯一或换句话说，家庭或工作中的主要 PC 转换为双启动或多启动系统是一个糟糕的选择。如果主要家庭 PC 必须用作双启动或多启动系统，更安全的做法是添加一块第二硬盘并让第一块基本保持不变。像 GRUB 这样强大的引导加载程序将允许从另一块硬盘启动。

我大学的计算机科学系有 15 个用于不同目的的实验室，运行的硬件从 i386 到 Sun SPARCs 不等。在数据和安全绝对重要时，计算机只运行一个操作系统，无论是 Windows 2000 Professional、Red Hat Linux、Slackware、FreeBSD 还是 Sun Solaris。然而，我们确实有大约 10–12 台 PC 的“测试实验室”，其中我们有运行 ASP Linux、Red Hat Linux、Slackware、Windows 2000 Professional、FreeBSD 等的双启动和多启动系统。这可以被视为理想情况。

### 1.4 假设列表

尽管从最基础开始解释了每个必要的步骤，但编写本指南时仍考虑了一些重要假设，其中包括：

如果你还不了解其中一些内容，不用担心，继续阅读，因为最重要的步骤将在后续章节中根据需要详细解释。无论如何，在继续之前，请确保浏览本指南的常见问题解答 (FAQ) 部分。

### 1.5 致谢

我谨向以下所有人员和项目表示感谢，没有他们的帮助和积极参与，本文件就不可能实现。其中包括：

此外，在编写本指南时，我查阅了以下印刷书籍、在线期刊、杂志和官方论文：

### 1.6 法律声明

### 1.7 关于作者

Subhasis “savvy” Ghosh 从学生时代起就从事 GNU/Linux 和 FreeBSD（以及最近的 OpenBSD、NetBSD、Sun Solaris 和其他 UNIX 变体）操作系统方面的工作，至今已有约 7 年。在此期间，Ghosh 参与了多个 Linux 及 Linux 相关项目，包括 Linux 内核源代码的修改；在 Linux 和 FreeBSD 中分析、设计和实现进程间通信（IPC）机制；以及 Red Hat Linux 桌面、工作站和服务器的安装、配置和故障排除等工作。此外，在过去几年中，Ghosh 为 Linux.com、Linuxgazette.com 和 Linuxfocus.org 在线杂志撰写了许多关于 Linux 内核编译、GNOME 编程及其他主题的文章。

目前，22 岁的 Ghosh 是俄罗斯联邦莫斯科动力工程学院（Technical University）的工程专业学生，专攻“信息学与计算机科学工程”领域。他是微软认证专家（MCP）、MCSD，并持有 NT 4.0 的 MCP 认证；此外还拥有许多其他 GNU/Linux 及计算机行业相关认证。他的网页可在 http://groups.msn.com/Linuxdump 访问。

## 2. 常见问题（FAQ）

读者会有问题。因此，本 FAQ 部分旨在从读者的角度回答一些最明显的问题。请所有读者通读本节，找到个人问题的答案。

通读整个 FAQ 后，如果读者仍觉得自己还有“一两个问题”要问，请随时发邮件至 sahibshah_ghosh@linuxwaves.com。

### Linux 和其他？

1. **本指南的目的是什么？**

本指南可供任何人使用，用于在一台计算机的同一硬盘上安装和配置 3 个操作系统（OS）。首先安装 Microsoft Windows 操作系统（根据读者的选择），然后安装 FreeBSD 4.8–RELEASE 或 OpenBSD 3.2–RELEASE 或 NetBSD 1.6.1，最后，我们通过安装 Red Hat Linux 7.3 来完成本指南。虽然我一直使用这种特定的顺序，但读者可以根据自己的习惯选择安装顺序。

2. **为什么本指南使用了“3”个操作系统？**

当前的情况是，Microsoft Windows 操作系统统治着桌面市场，而 GNU/Linux 发行版和 *BSD 版本（FreeBSD/OpenBSD/NetBSD）则在服务器市场竞争“全球统治”，因此，我认为将它们全部包含在本指南中是最好的选择。第一个操作系统是 Microsoft Windows 操作系统，第二个属于 *BSD 家族，最后一个是常用的 GNU/Linux 发行版（Red Hat）。因此，操作系统的数量最终为“3”。



## 3. 你自己是否尝试过本指南中提到的步骤？你在什么配置的计算机系统上测试了本指南中提到的所有内容？

我向大家保证，我在自己的个人计算机系统上测试了本指南中提到的每一步。之后它们也在配置各异的其他计算机上成功测试过。我的计算机有一台 266.87 MHz Intel Pentium 2 处理器，64MB 物理 DIMM RAM，一块 20.0 GB Maxtor IDE 硬盘和其他常用配件，运行 Microsoft Windows 98(SE)、FreeBSD 4.8–RELEASE 和 Red Hat Linux 7.3。另一台配置基本相同，运行 FreeBSD 4.8–RELEASE、OpenBSD 3.2–RELEASE 和 Red Hat Linux 7.3。经验法则是：“资源越好，计算机性能越好”。

## 4. 你的所有安装都是“CD–ROM”基于的安装类型。如何“Ethernet”、“FTP”、“HTTP”、“NFS”安装类型呢？

我决定让本指南尽可能简单。由于我们大多数人通常使用本地 CD–ROM 上的光盘来安装操作系统，我假设读者采用 CD–ROM 基于的安装来安装所涵盖的操作系统。此外，本指南面向所有类型的用户，从中级 Linux 用户到经验丰富的 Unix 专家。由于 NFS、HTTP、FTP 和其他此类安装类型通常需要运行服务器的网络，而普通家庭用户无法访问。我只涵盖了 CD–ROM 基于的安装类型。对“网络”爱好者造成的不便表示抱歉。

## 5. 为什么有人会需要在同一台计算机的同一硬盘上运行 3 个操作系统？我要在 2 个独立的硬盘上运行 3 个操作系统。这本指南到底有什么大不了的？

有很多原因。为乐趣、为学习新的安装和引导方法、为获得“多重引导”、分区方案、引导加载程序等方面的内部知识，或者仅仅因为你负担不起 2 个独立的 40.0 GB 硬盘来安装你想要摆弄的 3 个不同的操作系统。对我来说，我想最后一个理由“最合适”。

最后，如果你确实想要，你始终可以安装和配置你的计算机系统，在 2 个独立的硬盘上安装 3 个不同的操作系统。

## 6. 为什么是 Red Hat？为什么不是 Debian GNU/Linux、Slackware、Caldera、SuSE、TurboLinux 等？

由于我过去的大多数 Linux 项目和工作通常都与 Red Hat Linux 发行版相关；不断安装、配置和管理 Red Hat Linux 个人桌面和工作站。目前，Red Hat Linux 是世界上“最”领先的 Linux 解决方案提供商，大型企业实时系统使用 Red Hat 操作系统软件实现。此外，Red Hat 文档和支持很容易找到。因此，选择了 Red Hat Linux。其他发行版，即 Debian GNU/Linux、Slackware 和 Mandrake 都很好，我可能会稍后添加更多涵盖其他 Linux 发行版的部分。

## 7. 为什么是 FreeBSD、OpenBSD 和 NetBSD 操作系统？为什么不是 BSD/OS、Darwin、Irix、Sun Solaris、Digital UNIX、HP-UX、IBM-AIX 等？

我个人在 FreeBSD 和 OpenBSD 机器上拥有网络和源代码黑客经验。最近，我可以访问 NetBSD 1.6.1 和 Sun Microsystems 的 SunOS 操作系统在 Solaris 操作环境中。我“没有”使用 Irix、Ultrix、Minix、HP-UX、IBM-AIX、Darwin 等的经验。因此，选择了 FreeBSD、OpenBSD 和 NetBSD。

## 8. 你为 GNU/Linux 使用了哪个内核版本？

Linux Kernel 2.4.18-3 已用于 Red Hat Linux 发行版（Valhalla）。写作当时最新的内核是 Kernel 2.4.20。

## 9. 我按照你在本指南中说明的方式在我的计算机上安装了 3 个操作系统。不幸的是，出了点问题。我的计算机崩溃了，我丢失了所有数据。你能否好心地为这一切混乱负责？

好吧，首先我对你的数据丢失和所有这些明显的混乱表示“最深切”的慰问。我很乐意承担所有责任，但就目前而言，我自己有足够的问题需要处理。因此，我“不”准备为任何地方发生的任何错误负责。至少，我可以说，本指南中提到的所有步骤和方法都已在配置各异的多个系统上彻底测试，迄今为止没有发现任何问题。

## 10. 你使用了 GNU GRUB 来引导全部 3 个操作系统。你能告诉我原因吗？为什么不使用流行的 Linux Loader（LILO）或 FreeBSD 或 NT 引导加载程序来实现这一目的？

众所周知，引导加载程序在配置时发挥着非常重要的作用

multiple-booting systems where you can use any suitable boot loader which is capable of booting multiple operating systems. I chose GRUB in this guide for three specific reasons: 1) GNU GRUB is the "default" boot loader in Red Hat distribution releases currently. 2) As mentioned in the 'Release Notes' of Red Hat Linux 8.0, the use of LILO is deprecated and the package would be removed from one of its future releases. 3) GRUB is a very powerful (x86) PC-compatible boot loader which supports a number of operating systems "directly" and other proprietary ones too via "chain-loading" for booting them. Thus, GRUB is used instead of other boot loaders.

## 11. I have older Red Hat, FreeBSD and OpenBSD distributions and/or releases. Will they work?

I am sure they would with a few modifications at places. All steps mentioned should behave in a normal manner if you are using Kernel 2.2.x or higher (for Linux). For FreeBSD users, if you are using not earlier than 4.X–RELEASES, there should not be any problems whatsoever. Just take a deep breath, and start doing as given in this guide. If in case, at some place it does "not" work, make sure you are using the right step and commands etc. Most times, it is human error rather than computer-related error which lets big servers and networks down. Always remember this!

## 12. I would like to have access to good resources on Linux and FreeBSD. Could you suggest a few?



Yes, definitely I could. There is a lot of very good technical information on all the "open-source" operating systems out there on the Internet. For Linux, make sure you often visit `http://www.linuxgazette.com`, `http://www.linuxfocus.org`, `http://www.linux.com` and a host of others. Besides, "The Linux Documentation Project" (TLDP) provides excellent resources on all topics related to GNU/Linux. As for printed books, these are some of my absolute favorites: Red Hat Linux 8.0 Bible, Understanding the Linux Kernel, Modern Operating Systems, Linux Kernel Programming, The FreeBSD Handbook at `http://www.freebsd.org`, The Design of the UNIX Operating System, The Design and Implementation of the 4.4BSD Operating System. That would be enough for the time-being!

## 13. I have a few suggestions, new ideas and exciting comments. Can I send them to you?

Without asking, please do. Only by hearing from others, I can make this guide a better one in the near future. So, drop a line if you want to.

## 14. I have "installation-specific" questions/queries or something "failed" or "this quite didn't work"? Can I send these reports to you?

Of course do. But please be patient, cause I am busy with lots of things at my university; tests, exams, assignments, dating my "infinitely patient FreeBSD-compatible rock-stable girlfriend", maintaining this guide, other Linux assignments etc. So, I cannot promise to get back to you immediately. I need some time solving your problems.

## 15. Will you be updating this guide from time to time? Will "my" problems be listed here?

Yes, I would definitely update this guide from time to time with changes, updates, fixes, additions and so on.

## 16. Does this guide have any newest version on the Internet?

As of now, no, it does not. This is the only place where it will be updated from time to time.

## 17. (For people living in and around Moscow, Russia) I have a computer system and I would love to install 3 operating systems on them. Would you be kind enough to come to my place and do the installation and configuration?

If you do live in Moscow, or on the outskirts of Moscow; drop me a line. I would come down to your place and do everything that is required for free. Cannot help others living far.

## 18. (For people of Russia) We love Microsoft Windows, FreeBSD and OpenBSD operating systems. But "why" have you NOT used the common Russian GNU/Linux distributions? I mean "ASP Linux", "Black Cat Linux", "ALT Linux" and others?

All the above-mentioned GNU/Linux distributions are basically Red Hat-based Linux distributions. They heavily rely on Red Hat for package installation procedures, Kernel hacking, Kernel updates etc. I have used ASP Linux 7.2 myself, and though it does offer a few new and exciting features, but I personally prefer working with Red Hat Linux. I have "no" experience using Black Cat and ALT GNU/Linux distributions.

## 3. 组织

本指南的内容已拆分为 7 个不同的部分，称为“章节”，如下图所示，以便读者更方便地搜索和阅读。读者预计会从第 2 章提及的列表中选择任意一个 Microsoft Windows 操作系统，因此关于 Microsoft Windows 操作系统的其他部分可以完全“无”风险地跳过。读者在选择好要安装的 Microsoft OS 后，即可进行安装，然后依次进行 FreeBSD/OpenBSD/NetBSD 和 Linux 的安装。

第 1 章：**_关于操作系统_** 涵盖了对 Windows OS 家族（_我选择对 Microsoft Windows XP Professional 说几句话_）、Linux、FreeBSD、OpenBSD 和 NetBSD 操作系统的简要讨论。每个操作系统的一般信息、法律事项等均在此讨论。如需更官方和详尽的信息，请参阅列出的产品和项目的官方网站。

第 2 章：**_安装 Microsoft Windows_** 涵盖在新硬盘上安装读者选择的任意一个 Microsoft Windows 操作系统。读者在此选择的要安装的 OS 最终将与 FreeBSD/OpenBSD/NetBSD 和 Red Hat Linux OS 共存。Windows 下的磁盘分区和标签方案在此进行了详细讨论。

第 3 章：**_安装 FreeBSD 4.8-RELEASE_** 涵盖了在已存在的 Microsoft Windows 操作系统上安装和配置 FreeBSD 4.8-RELEASE 所需的主题。如果读者选择安装 OpenBSD 3.2-RELEASE 而非 FreeBSD 4.8-RELEASE，则可以跳过本章并进入下一章。



> **_警告：_** 由于 FreeBSD 和 OpenBSD 操作系统都是 POSIX 兼容的 BSD 衍生系统，两者都使用相同的 BSD 风格的硬盘分区和标签方案，并且从用户层面看两者具有相同的命令集。因此，FreeBSD 部分中涵盖的分区和文件系统命名将不会在下一章中重复。如果您碰巧是完全的 OpenBSD 新手，或者“OpenBSD”这个词听起来像希腊神话中的人物，那么最好您通读本章的所有信息并安装和配置 FreeBSD。OpenBSD 安装虽然简单整洁，但完全是基于文本的安装程序，并假定用户对硬件、BSD 风格的硬盘切片和标签方案有扎实的了解。在任何一个阶段操作失误，都会导致整个安装失败，甚至可能使最初安装的 Microsoft Windows OS 完全无法访问。经验告诉我，在进行此类安装时应妥善备份。不要事后发送问题报告。你已被警告！

# 第 4 章：第 4 章，**_安装 OpenBSD 3.2-RELEASE_**

涵盖了在已存在的 Microsoft Windows 操作系统上安装和配置 OpenBSD 3.2-RELEASE 所需的主题。如果读者选择安装 FreeBSD 4.8-RELEASE 而非 OpenBSD 3.2-RELEASE，则可以跳过本章并瞥一眼前一章。分区和基本引导过程细节等在此讨论。

## 3.1 关于操作系统

本指南中涵盖的操作系统的总体概述已在此提供。读者必须注意，这些是我个人的观点（和评论），与 Linux/FreeBSD/OpenBSD/NetBSD 或更一般地，与开源社区的观点无关。

### 3.1.1 Microsoft Windows

Microsoft Corp. 拥有一个冗长（却致命脆弱且 buggy）的操作系统列表，目标范围从温和而孱弱的家庭用户到真正多任务、多处理、多编程、容错、抗黑客的实时系统；从 MS Windows 95 到最近发布的 Microsoft Windows Server 2003。读者可根据自己的个人喜好和/或目标环境自由选择任何操作系统。我个人“不”认为 Microsoft Windows 2000 系列操作系统（包括 Windows 2000 Professional、Windows 2000 Server、Windows 2000 Advanced Server 和 Windows 2000 Datacenter server）是“企业”环境的非常好的选择。如果考虑软件工程的 PASSME 主题，其中 PASSME = 性能、可用性、可扩展性、安全、维护性和可扩展性等任何受审查软件的特性；Microsoft Windows 2000 服务器（以及操作系统，一般而言）的评级远低于 UNIX SVR4、*BSDs、Sun Solaris、Linux 以及其他商业 UNIX 变体，如 IBM-AIX、HP-UX、Digital UNIX 等。

无论如何，我个人认为，“操作系统选择的自由是每个人的与生俱来的权利”。因此，使用 Windows 98 还是 Windows 2000 Professional 是读者的选择。个人而言，我喜欢折腾 Microsoft Windows XP，它是 Windows 2000 和 Windows Millennium 之后的下一个版本的 Microsoft Windows。Windows XP 带来了 Windows 操作系统的融合，通过整合 Windows 2000 的优势——基于标准的

GNU 通用公共许可证（GPL）。Linux 源代码中附有一份 GPL 副本；你也可以从 ftp://prep.ai.mit.edu/pub/gnu/COPYING...”。

读者必须注意一个事实：尽管全球许多 Linux 用户简单地将 GNU/Linux 操作系统称为“Linux”，但更恰当的做法是将其称为 GNU/Linux 系统，而在特别谈论内核时，只称其为 Linux。此外，Linux 新用户中一个非常流行的误解是：“嘿！Linux 就是 UNIX！”不，绝对“不是”。再次提醒读者：Linux 内核是一个 UNIX 克隆，换句话说，是对 UNIX 内核的重实现，但它本身并不是 UNIX。另一方面，BSD 系统，例如 FreeBSD 和 OpenBSD，并不仅仅是内核。它们更接近真正的 UNIX（AT&T 官方发布的 UNIX SVR4）。它们代表了一整个操作系统，包含一整套应用程序、工具、用户实用程序、shell、游戏、文档、开发工具、系统和用户级二进制文件，以及操作系统的完整源代码。

### 3.1.3 FreeBSD：

FreeBSD，代表伯克利软件发行版操作系统软件的自由版本（尽管所有的 BSD 本质上都是“开源”或“自由”的），从技术上讲，是当今地球上最强大、最具专业品质、最先进的 UNIX 兼容操作系统软件。FreeBSD 最初基于 4.4BSD-Lite（也少量包含了 4.4BSD-Lite2 代码库），由加州大学伯克利分校在伯克利电气工程与计算机科学系计算机科学部的计算机系统研究组（CSRG）授权下开发。FreeBSD 操作系统（就像 Linux 发行版一样）附带一整套软件包，包括用户应用程序、工具、用户实用程序、shell、游戏、文档、开发工具、系统和用户级二进制文件，以及操作系统的完整源代码。FreeBSD 项目网站可以访问：http://www.freebsd.org。

近来，大量媒体聚光灯将 GNU/Linux 系统（更具体地说是 Linux 内核）推上了明星地位。有些人将 Linux 评价为有史以来最好的 UNIX 克隆，它会给市场上的 UNIX 以及其他 UNIX 克隆和 UNIX 兼容系统带来灾难。但事实并非如此。读者必须注意：正如汽车的动力来自引擎盖下运转的发动机质量，操作系统软件的稳定性、可靠性、可扩展性和健壮性等特性同样来自内核或相应操作系统核心的内部结构。我个人认为，Linux 内核和 FreeBSD 内核都是创造性与巨大努力的伟大作品，仅仅在用户层面或技术层面对两者进行比较是没有意义的。在内存稀缺且受到极端压缩和压力的情况下，Linux 内核会崩溃。而 FreeBSD 凭借其高度优化且先进的 VM/Swap 系统可以救急！另一方面，在特定情况下，Linux 可能远远胜过 FreeBSD。读者需要注意并记住的重要一点是：Linux 内核偏爱简单，而不是高度优化的、动态但更复杂的代码；而 FreeBSD 内核则通过引入更复杂的代码，并不断重新排列和重写一些更重要的内部算法和数据结构来重度优化代码库，从而优化性能。

关于 Linux 和 FreeBSD 内核的完整详尽讨论超出了本指南的范围。如果读者感兴趣，可以上网搜索更多 Linux 和/或 FreeBSD 的特定信息。我建议读者阅读 Bovet 和 Cesati 所著的《深入理解 Linux 内核》以深入了解 Linux 内核的内部运作，以及《4.4BSD 操作系统的设计与实现》以

FreeBSD/OpenBSD 等系统，以及 M. Bach 所著的《UNIX 操作系统设计》（The Design of the UNIX Operating System）一书，涉及 UNIX SVR4 内部原理。

### 3.1.4 OpenBSD：

BSD 家族除了占主导地位的“老大哥”FreeBSD 之外，还包括 OpenBSD、NetBSD、BSD/OS 和 Darwin 操作系统。OpenBSD 是一个功能完备、多平台的类 UNIX 操作系统，基于 Berkeley Networking Release 2（Net/2）和 4.4BSD-Lite。OpenBSD 团队致力于实现所谓的“默认安全”（secure by default）状态。这意味着 OpenBSD 用户应当感到放心，他们新安装的机器不会受到入侵。这一“默认安全”目标是通过在安全方面采取主动姿态来实现的。FreeBSD 的发行版追求在最为恶劣的条件下保持稳定性和可靠性，而 OpenBSD 的发行版则追求企业环境中的最佳安全性。OpenBSD 操作系统软件被称为“主动安全的类 UNIX 操作系统”。OpenBSD 内核经过大量安全特性的深度优化，从而为客户提供最为安全、难以被黑客攻破的实时系统。OpenBSD 项目网站可访问：http://www.openbsd.org。

OpenBSD 操作系统软件已将强加密技术集成到基础系统中。它提供了功能完备的 IPsec（因特网协议安全）实现，并支持 SSL（安全套接层）和 SSH（安全外壳）等常见协议。网络过滤和监控工具，如数据包过滤、NAT（网络地址转换）和桥接，也一并包含在内。为了满足高性能需求，基础系统还增加了硬件加密支持。OpenBSD 尽可能提供多种安全选项，让用户能够享受安全的计算体验，而不会感到负担。

### 3.1.5 NetBSD：

NetBSD 内核注重清晰的设计和良好的架构方案。NetBSD 从单一源代码树支持极为广泛的硬件平台，包括在所有平台上同步发布，尽管缺乏媒体曝光和商业支持，它依然持续吸引着用户和经验丰富的开发者——这完全归功于对代码质量的重视。NetBSD 操作系统内核以“可移植性”为目标，力求在尽可能多的平台上运行。NetBSD 项目网站可访问：http://www.netbsd.org

下表展示了本指南所涵盖的每个操作系统的主要“目标”：

|   |   |



|---|---|

| Windows | 去问盖茨先生本人吧……或许问问我们的钱包…… |

| Linux | Linux 的目标是新颖、激动人心且前沿的特性，如超线程（HyperThreading）、USB、无线网卡等。 |

| FreeBSD | FreeBSD 的目标是稳定性和健壮性；优化内核代码库，以便在繁重网络负载下获得最佳性能。 |

| OpenBSD | OpenBSD 的目标是最佳安全性。它是最主动安全的类 UNIX 操作系统。 |

| NetBSD | NetBSD 的目标是可移植性。在尽可能多的平台上运行是其首要目标。 |

### 3.2 安装 Microsoft Windows

我将 Microsoft Windows 操作系统作为计算机上的“第一”操作系统。我的计算机上安装了 MS Windows 98（SE）。读者可以从下面列出的任何一款 Microsoft 操作系统中进行选择。假设你也想将 Microsoft Windows 98（SE）作为你的第一个操作系统。那么请阅读 B 节：安装 MS Windows 98（SE）中的信息，并按照该节所述进行操作之后，再继续安装 FreeBSD 4.8-RELEASE、OpenBSD 3.2-RELEASE 或 NetBSD 1.6.1。

因此，我们有以下各节：

- F 节：安装 MS Windows XP（Home/Professional）

可以使用 Windows 的 `fdisk` 和 `format` 工具来对一块新的未格式化硬盘进行分区。我假设读者拥有一块新的未格式化硬盘，并希望对其进行分区，然后格式化以安装 Microsoft Windows 操作系统。下面提到的内容适用于 Microsoft Windows 95、Microsoft Windows 98（SE）和 Microsoft Windows Millennium（ME）。如果你打算安装 Windows NT、Windows 2000 或 Windows XP，则可以跳过本节，直接转到对应 D、E 和 F 节的部分。

#### A 节：安装 MS Windows 95

#### B 节：安装 MS Windows 98（SE）

#### C 节：安装 MS Windows Millennium（ME）

下面提到的内容适用于 Microsoft Windows 95、Microsoft Windows 98（SE）和 Microsoft Windows Millennium（ME）。因此，如果你要安装其中任何一个系统，请务必通读此处描述 `Fdisk` 和 `Format` 工具，并解释如何使用它们对硬盘进行分区或重新分区的所有内容。这些内容描述了以下主题：

在安装操作系统之前，你必须首先在计算机的硬盘（磁盘 1）上创建一个主分区，然后在该分区上格式化一个文件系统。`Fdisk` 工具是一个基于 MS-DOS 的工具，可用于准备（分区）硬盘。你可以使用 `Fdisk` 工具创建、更改、删除或显示硬盘上的当前分区，然后

每个分配在硬盘上的空间（主分区、扩展分区或逻辑驱动器）都会被分配一个驱动器号。磁盘 1 可能包含一个扩展分区，而第二块硬盘可能包含主分区或扩展分区。扩展分区可包含一个或多个逻辑 MS-DOS 驱动器。

使用 `Fdisk` 工具对硬盘进行分区后，您可以使用 `Format` 工具使用文件系统格式化这些分区。文件系统 File Allocation Table（FAT）允许硬盘接收、存储和检索数据。Windows 95、Windows 98（SE）、Windows Millennium（ME）和 Windows 2000 支持 FAT16 和 FAT32 文件系统。当您在大于 512 兆字节（MB）的硬盘上运行 `Fdisk` 工具时，会提示您选择以下文件系统之一：FAT16 或 FAT32。FAT16 文件系统每个分配的空间或驱动器号的最大容量为 2 千兆字节（GB）。例如，如果您使用 FAT16 文件系统并且拥有一块 6 GB 的硬盘，您可以拥有三个驱动器号（C、D 和 E），每个分配的空间为 2 GB。至于 FAT32 文件系统，它支持最大为 2 太字节的驱动器，并且将文件存储在比 FAT16 文件系统更小的硬盘区域中。这导致硬盘上有更多的可用空间。请注意，FAT32 文件系统不支持小于 512 MB 的驱动器。当您运行 `fdisk` 和 `format` 命令时，会创建主引导记录（MBR）和文件分配表。MBR 和文件分配表存储必要的磁盘几何结构，允许硬盘接收、存储和检索数据。

请注意，我假设您拥有一台可以无故障运行的计算机系统，并且您可以使用可启动的 Microsoft Windows CD-ROM。如果您在从 CD-ROM 启动或使用启动磁盘时遇到问题，请咨询您的硬件制造商以获取 CD-ROM 设备驱动程序。对于分区主硬盘，您必须运行 `fdisk` 命令。首先将启动磁盘插入软盘驱动器，重新启动计算机，然后根据您的操作系统使用以下方法之一。

#### For a Windows 95/98/ME Startup disk:

在命令提示符下，键入 `fdisk`，然后按 enter。如果您的硬盘大于 512 MB，您会收到以下消息：

> *Your computer has a disk larger than 512 MB. This version of Windows includes improved support for large disks, resulting in more efficient use of disk space on large drives, and allowing disks over 2 GB to be formatted as a single drive.*

如果您启用大磁盘支持并在此磁盘上创建任何新驱动器，您将**无法**使用其他操作系统访问新驱动器，包括某些版本的 Windows 95 和 Windows NT，以及更早版本的 Windows 和 MS-DOS。此外，未明确指定用于 FAT32 文件系统的磁盘实用程序将无法与此磁盘一起使用。如果您需要使用其他操作系统或旧的磁盘实用程序访问此磁盘，请勿启用大驱动器支持。

Do you wish to enable large disk support?

如果您想使用 FAT32 文件系统，请按 Y 然后按 enter。如果您想使用 FAT16 文件系统，请按 N，然后按 enter。按 enter 后，会显示以下 `Fdisk` Options 菜单：

**请注意，只有在计算机中有两块物理硬盘时，选项 5 才可用。**

按 1 选择 Create DOS partition or Logical DOS Drive 菜单选项，然后按 enter。按 1 选择 Create Primary DOS Partition 菜单选项，然后按 enter。按 enter 后，您会收到以下消息：

Do you wish to use the maximum available size for primary DOS partition?

收到此消息后，根据您选择的文件系统使用以下方法之一。

#### For a FAT32 File System:

如果您在步骤 2 中为 FAT32 文件系统按 Y，并且希望将硬盘上的所有空间分配给驱动器 C，请按 Y，然后按 enter。按 ESC，然后按 ESC 退出 `Fdisk` 工具并返回命令提示符。

#### For a FAT16 File System:

如果您在步骤 2 中为 FAT16 文件系统按 N，您可以接受分区大小的默认 2 GB 大小，也可以自定义分区大小。

如果您想自定义硬盘上分区（驱动器号）的大小，请按 N，然后按 enter。会显示一个对话框，您可以在其中键入您希望主分区大小的 MB 或磁盘空间百分比。请注意，对于运行 Windows 98（SE）或 Windows ME 的计算机，Microsoft 建议您将主分区大小至少设为 500 MB。键入您想要创建的分区的大小，然后按 enter。按 ESC 返回 Options 菜单。要为硬盘上的额外空间分配驱动器号，请按 1，然后按 enter。按 2 选择 Create Extended DOS Partition 菜单选项，然后按 enter。您会收到一个对话框，显示扩展分区可用的最大空间。您可以调整分区大小或使用默认大小。请注意，默认最大空间是推荐的，但您可以将空间分配给多个驱动器号。键入您想要的空间量，按 enter，然后按 ESC。会显示 Create Logical DOS Drive(s) in the Extended DOS Partition 菜单。这是您可以使用该菜单将剩余硬盘空间分配给额外驱动器号的菜单。在 Enter logical drive size in Mbytes or percent of disk space (%) 框中键入您想要分配给下一个驱动器号的空间量，然后按 enter。之后，您必须激活计划从中启动的分区。这通常是驱动器 C。因此，按 2 选择 Set active partition 菜单选项，然后输入您想要设为活动状态的分区的编号。



创建分区后，您必须格式化分区以便访问和使用它们。如果您使用的是 Windows 95 启动磁盘，会显示命令提示符，您可以跳到步骤 2。如果您使用的是 Windows 98 第二版或 Windows ME 启动磁盘，请在显示 Windows 98 启动菜单时选择 Start computer without CD-ROM support 菜单选项。当显示命令提示符时，键入 `format c:`，然后按 enter。此命令格式化驱动器 C（或您的“活动”驱动器）。对于所有其他分区，键入 `format drive:`（其中 drive 是您想要格式化的分区的字母）。

读者必须注意，我在这里本节中谈论的是使用 Microsoft fdisk 实用程序“分区硬盘”，目的是为绝对的新手提供有关如何分区和格式化新硬盘驱动器的一般信息。

#### 第 D 节：安装 MS Windows NT（4.0）

#### 第 E 节：安装 MS Windows 2000（专业版）

#### 第 F 节：安装 MS Windows XP（家庭版/专业版）

要安装上述 3 种操作系统中的任意一种，首先使用`fdisk`工具分区硬盘。然后再选择文件系统类型。

在全新安装 Windows NT、2000 或 XP 期间，您可能需要选择计算机应使用哪种文件系统。在我的另一台电脑上，我个人使用的是支持以下功能的 Microsoft Windows XP Professional：

但非常“重要”的信息：转换到 NTFS 是一条单向路；如果您将 FAT 或 FAT32 文件系统转换为 NTFS，就无法稍后将硬盘转换回 FAT。

如果您不确定使用哪种文件系统，我建议使用 FAT32。如果您想更改文件系统，这里有几点建议：

您可以选择任何您想要的文件系统类型。选择文件系统后，照常继续进行 Windows NT/2000/XP 安装。安装后，随意配置您的新系统。我个人选择了“FAT32”文件系统来格式化我安装 Microsoft Windows XP Professional（最终版）的分区。它构成了我电脑上的第一个操作系统。

#### 实际步骤摘要：

好吧，关于不同的 Microsoft 操作系统就说到这里。现在让我们更仔细地看看我们将如何分区硬盘。如上所述，我们使用 Microsoft fdisk，然后创建一个大约 2000MB 的主 DOS 分区。在我的电脑上，我有一个 999MB 的主分区，其中包含 Microsoft Windows 98（SE）。我使用这么小的空间是因为我几乎不在 Windows 上做任何工作，从而为 FreeBSD 和 Linux 保留空间！读者如果愿意，可以选择多一点空间。创建此分区后，不要忘记使用`Format`工具对其进行格式化。在我的系统上，我有一个 FAT32 主分区。

创建此主分区（假设为 999MB）后，我们就（我再重复一遍：不需要）使用 Microsoft fdisk 实用程序创建任何其他分区。例如，我有一块 20.0 GB 的 Maxtor 硬盘。我使用`fdisk`创建了一个大约 1000MB 的主分区。读者显而易见的问题是：剩下的 19GB 怎么办？它会怎样？好吧，答案很简单。我将其保持原样未动，因为我会将这块可用空间分成两半，用于在安装 FreeBSD 4.8-RELEASE 或 OpenBSD 3.2-RELEASE 或 NetBSD 1.6.1 时使用 FreeBSD 分区编辑器或 OpenBSD 分区编辑器安装 FreeBSD 或 OpenBSD 和 Linux。因此，完全不必担心，跟着我走就行。我保证，等你读完本指南后，你硬盘上不会浪费一个字节。

因此，在我们最终进入下一节安装和配置 FreeBSD 4.8-RELEASE 或 OpenBSD 3.2-RELEASE 或 NetBSD 1.6.1 之前，我想用一个“分区检查”来结束本章。在此步骤之后（从 Microsoft fdisk 观察），我的电脑上的分区表如下：

#### 显示分区信息

| 分区 | 状态 | 类型 | 卷标 | Mbytes | 系统 | 用量 |
|-----------|--------|------|--------------|--------|--------|-------|
| `C:1` | A | PRI DOS | WIN | 1000 | FAT32 | 5% |

完成此操作后，重新启动计算机并使用可启动的 Microsoft Windows CD-ROM（取决于您选择的系统），照常安装操作系统。进行通常的系统配置并登录 Windows 以检查一切是否正常工作。就本节而言，到此为止，现在休息一下，喝杯咖啡，然后继续下一章，第 3 章：安装 FreeBSD 4.8-RELEASE。

### 3.3 安装 FreeBSD 4.8-RELEASE

本章重点介绍安装 FreeBSD 4.8-RELEASE 并使系统多启动，以便它能与计算机上已有的 Windows 操作系统成功共存。与 Windows 安装一样，它也侧重于基于 CD-ROM 的安装。专家可以照常自行进行，而对于新手，请务必查看 FreeBSD 文档项目中的 FreeBSD 2.X、3.X 和 4.X 常见问题解答，网址为 http://www.freebsd.org。有关带屏幕截图的分步 FreeBSD 安装程序，请参阅 FreeBSD 手册第 2 章：安装 FreeBSD，网址为 http://www.freebsd.org/doc/en_US.ISO8859-1/books/handbook/index.html。这些以及 FreeBSD 项目主页上提供的其他文档对 FreeBSD 软件的所有相关方面提供了详尽而广泛的覆盖。在继续本指南之前，请务必从该网站获取尽可能多的信息。

读者必须注意，在撰写本文时，FreeBSD 操作系统存在两个并行的分支。最新的 -STABLE 版本是 FreeBSD 4.8-RELEASE，而最新的 -CURRENT 版本是 FreeBSD 5.1-RELEASE。在本章中，我们将讨论安装 FreeBSD 4.8-RELEASE 的一些理论方面、磁盘分区（在 FreeBSD 术语中更常称为切片），然后进入实际安装本身。因此，本章的内容可归类为以下提及的部分：

### 1. FreeBSD 中的切片

在安装 FreeBSD 之前，先简要了解一下 FreeBSD 所称的“切片”是个不错的主意。如果你已经了解这些内容，可以随意跳过此部分并阅读标题为“安装步骤摘要”的部分。

FreeBSD 操作系统根据特定选择的方案对硬盘进行分区并标记分区，该方案与 NetBSD、OpenBSD、Ultrix、Digital Unix 和 SunOS 等其他基于 BSD 的 Unix 系统相似。让我们看看 FreeBSD 软件如何“切片”你的硬盘，然后在其中“创建分区”以供使用。每个包含文件系统的分区都存储在 FreeBSD 所称的“切片”中。切片是 FreeBSD 对过去所称分区所使用的术语。切片从 1 编号，至 4 止（在 Windows 术语中，它们将被称为“主分区”，从 1 编号，至 4 止）。因此，读者必须注意，Windows 中的“主分区”指的是 FreeBSD 术语中的“切片”，而“包含逻辑磁盘驱动器的扩展分区”在 FreeBSD 术语中 simply 称为“分区”。扩展分区内的逻辑磁盘驱动器在 FreeBSD 中也可能称为“物理切片内的逻辑切片”。有时看起来有点别扭，但读者越早习惯这些术语越好！

现在，重要部分。有一些操作系统即使其对应的引导文件存储在扩展分区的逻辑磁盘驱动器中也能引导。对于 FreeBSD 来说，这种机制“不”起作用。FreeBSD 必须需要其中一个切片（即计算机硬盘上分区表中的 4 个条目，在 Windows 术语中将被称为“主分区”）。然后它使用一个名为`disklabel`的程序在此切片中创建多达八个分区。读者必须注意：你不能在 Linux（或 DOS）创建的扩展分区中安装 FreeBSD。

FreeBSD 对硬盘和分区进行如下标记：

其中，`/dev` 是 FreeBSD 根（`/`）目录下的目录，其中包含与设备关联的所有设备特殊文件。读者必须注意，我假设读者使用的是 FreeBSD 4.X-RELEASE。FreeBSD 4.0-RELEASE 之前的 IDE 硬盘驱动器命名为`wd`。

SCSI 驱动器呢？好吧，FreeBSD 也对它进行标记！

其中，`/dev` 是 FreeBSD 根（`/`）目录下的目录，其中包含与设备关联的所有设备文件。

现在，让我们谈谈 FreeBSD 下的分区方案。它与 Linux 中的类似，只是分区命名方式不同。在 FreeBSD 中，我们首先考虑一个特定的硬盘驱动器，无论是 IDE 还是 SCSI 硬盘驱动器。然后，我们考虑其上的分区。例如，IDE 驱动器上的分区命名如下（以 `/dev/ad0` 为例）：



上述驱动器也可能包含分区。FreeBSD 也对它们进行标记，并且每个标记都有其自己的对应挂载点。让我们考虑一个例子。一台计算机的硬盘命名为 `/dev/ad0`，包含 2 个切片；第一个切片是 FAT32 分区，第二个是包含 4 个逻辑切片 [逻辑磁盘驱动器] 的 BSD/i386 分区。那么，在这种情况下，分区表会是什么样子以及意味着什么？让我们看看 FreeBSD 如何标记此方案。FreeBSD 会将其表示为：

- `/dev/ad0`
  - `/dev/ad0s1`
  - `/dev/ad0s2`
    - `/dev/ad0s2a`
    - `/dev/ad0s2b`
    - `/dev/ad0s2e`
    - `/dev/ad0s2f`

其中，`ad0s2a` 指的是“第一块 IDE 磁盘（`ad0`）上的第二个切片（`s2`）上的第一个分区（`a`）”。在上面的示例中，`/dev/ad0s1` 是包含 FAT32 文件系统的切片，而 `/dev/ad0s2` 是正在检查的硬盘驱动器上的第二个切片。读者必须注意，FreeBSD 从 `/dev/ad0s1` 开始对切片进行标记，直到 `/dev/ad0s4`，最多可有 8 个逻辑切片，命名为 `a`、`b`、`c`、`d`、`e`、`f`、`g` 和 `h`。在此示例中，“逻辑切片”`a`、`b`、`e` 和 `f` 在 FreeBSD 中有其对应的挂载点。

这里，挂载点如下：

如需更详尽的信息，请参阅“FreeBSD 手册”。

### 2. FreeBSD 中的文件系统

Microsoft Windows 操作系统使用 FAT16、FAT32、NTFS 4.0 和 NTFS 5.0 文件系统来存储和检索数据。最近发布的 NTFS 5.0 已在所有 Windows 2000 操作系统中实现。Linux 内核使用“第三代扩展原生文件系统”，表示为 `ext3fs`。Linux 还支持 `ext`（现已过时且不再支持）和 `ext2fs` 文件系统。“第二代扩展文件系统”`ext2fs` 是为 Linux 操作系统开发的高级分层文件系统，其中包含高级功能，如最大文件大小为 2.0 GB、最大文件名长度为 255 个字符以及支持三个时间/日期戳。它们分别是创建日期、最后修改日期和最后访问日期。“第三代扩展文件系统”具有所有这些功能，并且还实现了“日志文件系统架构”`JFS`。`JFS` 架构确保在非计划关机（例如停电引起）事件中存储在硬盘上的数据完整性。日志文件系统维护所有读写事件的日志；此日志使磁盘能够恢复到最后稳定状态，并且还允许尽可能最大程度地恢复未完全写入的数据。

FreeBSD 操作系统基本上使用 Unix 文件系统 `UFS` 架构作为其底层文件系统。伯克利对其进行了更多改进，被称为“伯克利改进”或“伯克利扩展”。这个文件系统目前被 FreeBSD 用作其原生文件系统，通常被称为“快速文件系统”或 `FFS`，因为访问存储在 `FFS` 中的数据读取和写入非常快。该架构比 Linux 的 `ext2fs` 稍微复杂一些。它提供了一种更好的方式来确保文件系统数据完整性，主要是通过“softupdates”选项。此选项减少同步 I/O 并增加同步 I/O，因为对 `UFS` 文件系统的写入不是按扇区同步，而是根据文件系统结构进行同步。这确保了文件系统在两次更新之间始终保持一致。

FreeBSD 文件系统还支持文件标志，可以阻止潜在入侵者。您可以向文件添加多个标志，例如不可变标志。不可变 `schg` 标志不允许对文件或目录进行任何更改，除非您将其移除。其他非常实用的标志还有仅追加 `sappnd`、不可删除 `sunlnk` 和归档 `arch`。当您将这些标志与内核安全级别选项结合使用时，您将拥有一个非常难以渗透的系统。简而言之，FreeBSD 内核使用 `UFS = UFS+FFS+Softupdates+dirpref+dirhash` 功能来存储和检索数据

#### 3. 安装步骤摘要

FreeBSD 中涵盖的分区方案和文件系统已经介绍完毕，现在是时候进入实际的 FreeBSD 安装了。要完整逐步了解 FreeBSD 安装，请参阅 FreeBSD 项目网站上提供的安装指南。与上一章一样，在这里，我也只会提及安装的重要步骤。使用这些步骤在您的计算机上安装 FreeBSD 并配置为“多重启动”：

`have a lot of temporary files to deal with. I create a /, swap, /usr, /var and other usual partitions in my FreeBSD slice (named as /dev/ad0s2).`

Previous      Home      Next

### 3.4 安装 OpenBSD 3.2–RELEASE

本章重点介绍安装 OpenBSD 3.2–RELEASE 并多重启动系统，使其能够与计算机上已有的 Windows 操作系统成功共存。与 Windows 和 FreeBSD 安装一样，它也侧重于基于 CD–ROM 的安装。专家可以照常自行操作，而对于新手，请务必查看 OpenBSD 的常见问题解答，网址为 OpenBSD 项目主页 `http://www.openbsd.org`。有关带屏幕截图的分步 OpenBSD 安装程序，请参阅 OpenBSD 项目主页上的“Installing OpenBSD”在线手册。这些以及 OpenBSD 3.2–RELEASE CD–ROM 上提供的其他文档对 OpenBSD 的各个方面提供了详尽而广泛的覆盖。在继续本指南之前，请务必从该网站获取尽可能多的信息。

由于 FreeBSD 和 OpenBSD 操作系统都是 BSD–衍生系统，两个系统上 `/usr/share/doc` 目录中的 UNIX 相关信息都提供了有关如何安装、使用和定制 UNIX 系统的高质量技术信息。如果你还不是 FreeBSD/OpenBSD 专家，我谦卑而诚恳的建议是阅读这些系统上的“Unix User's Supplementary Documents (USD)”、“Unix System Manager's Manual (SMM)”和“Unix Programmer's Supplementary Documents (PSD)”。

注意：我在此假设执行本章的读者在继续之前已对 BSD 风格的硬盘分区和标签方案、设备命名约定等有扎实的理解和知识。如果您对我所说的内容完全没有概念，或者一般来说对 OpenBSD 一无所知，我强烈建议您回到前面的章节并阅读整章的内容。虽然材料是 FreeBSD 特定的，但其中大部分也适用于 OpenBSD，因为 OpenBSD 与其他 BSD 一样遵循“slicing”方案。

需要记住的几点重要事项：在 Linux 中，像 `/dev/hda1` 这样的条目指的是一个分区，在 FreeBSD 中可能标记为 `/dev/ad0s1`。OpenBSD 的对应项为 `/dev/wd0a` 代表第一个硬盘驱动器，`/dev/wd1a` 代表第二个硬盘驱动器，以此类推。OpenBSD `disklabel` 允许最多 16 个分区。它可以检测并表示硬盘上存在的所有主分区。OpenBSD `disklabel` 虽然可以看到扩展分区内的所有分区，但它不会列出扩展分区容器。读者必须注意，OpenBSD 保留 `c:` 分区，它代表整个硬盘，`i:` 到 `p:` 保留给除 OpenBSD 之外的其他操作系统（例如 Windows 或 Linux 分区），而 `a:`、`b:` 和 `d:` – `h:` 可用于 OpenBSD 特定分区。因此，一个重要事实是，未加限定词的“分区”一词通常指的是将要挂载文件系统的 UNIX 磁盘区域。

### 安装步骤摘要

有关 OpenBSD 安装的完整分步介绍，请参阅 OpenBSD 项目网站上提供的“Installing OpenBSD Manual”。与上一章一样，这里我也只会提及安装的重要步骤。利用这些步骤在计算机上安装 OpenBSD 并配置“多重启动”：

```
Disk:wd0        geometry: 1274 / 255 / 63        [ 20466810 Sectors ]
Offset:0

          Starting          Ending          LBA Info:
#  Id  C   H   S   C   H   S   Size    
0:  0B  0   1   1   249 254 63  4016187 Win95 FAT32
*1: A6  250 1   1   1273 254 63  16450497 OpenBSD
```

| # | Id | Starting C | H | S | Ending C | H | S | Size | Info |
|---|----|------------|---|---|----------|---|---|------|------|
| 0: | 0B | 0 | 1 | 1 | 249 | 254 | 63 | 4016187 | Win95 FAT32 |
| *1: | A6 | 250 | 1 | 1 | 1273 | 254 | 63 | 16450497 | OpenBSD |



editor. 读者必须注意：输入 `quit` 表示保存更改后退出编辑器，而 `exit` 表示不保存任何更改就退出编辑器。因此，我们执行 `quit`，而不是 `exit`。

### 3.5 安装 NetBSD 1.6.1

本章重点介绍安装 NetBSD 1.6.1 并多重启动系统，使其能够与计算机上已存在的 Windows 操作系统成功共存。与 Windows、FreeBSD 和 OpenBSD 安装一样，它也侧重于基于 CD-ROM 的安装。专家可以照常进行，无需帮助，对于新手来说，请确保查看 NetBSD 主页 http://www.netbsd.org 上提供的文档。这些和其他可在 NetBSD 1.6.1 CD-ROM 上获得的文档提供了有关 NetBSD 的所有方面的详尽和广泛的覆盖。在继续本指南之前，请确保从该网站获取尽可能多的信息。

**Note:** 我在此假设执行本章的读者在继续之前对 BSD 风格的硬盘分区和标签方案、设备命名约定等具有扎实的理解和知识。如果在这种情况下你对我所谈论的内容完全没有概念，或者一般对 NetBSD 一无所知，我强烈建议你回到涵盖 FreeBSD 的章节。

需要记住的几点重要事项：NetBSD 与 OpenBSD 类似地标记硬盘，使用 `/dev/wd0` 表示第一个硬盘，`/dev/wd1` 表示第二个硬盘，依此类推。NetBSD `disklabel` 允许最多 16 个分区。它可以检测并表示硬盘上存在的所有主分区。NetBSD `disklabel` 虽然可以看到扩展分区内的所有分区，但它不会列出扩展分区容器。读者必须注意 NetBSD 保留 `c:` 分区，该分区代表整个硬盘。`i:` 到 `p:` 保留给属于 NetBSD 以外的其他操作系统（例如 Windows 或 Linux 分区）的分区，而 `a:`、`b:` 和 `d:` – `h:` 可用于 NetBSD 特定分区。

### 安装步骤摘要

有关 NetBSD 安装的完整逐步介绍，请参阅 NetBSD 项目网站上提供的文档。与上一章一样，在这里我也只会提及安装的重要步骤。使用这些步骤在你的计算机上安装 NetBSD 并为其配置“多重启动”：

#### BIOS# cylinders heads sectors

| BIOS# | cylinders | heads | sectors |
|---|---|---|---|
| 0 | 1023 | 255 | 63 |

#### Total disksize 19541 MB.

| Start(MB) | Size(MB) | End(MB) | Kind |
|---|---|---|---|
| 0: 0 | 9774 | 9774 | Windows FAT32, LBA |
| 1: 9773 | 3001 | 12775 | NetBSD |
| 2: 12774 | 6766 | 19540 | old NetBSD/FreeBSD/386BSD |
| 3: | | | unused |

#### Total disksize 19541 MB.

| Start(MB) | Size(MB) | End(MB) | Kind |
|---|---|---|---|
| 0: 0 | 9774 | 9774 | Windows FAT32, LBA |
| 1: 9773 | 4001 | 13774 | NetBSD |
| 2: | | | unused |
| 3: | | | unused |

读者必须注意：我们仍需安装和配置 Linux。因此，为了完成这一步以及更多后续工作，我们进入下一章，第 6 章：安装 Red Hat Linux 7.3 (Valhalla)。

### 6. 安装 Red Hat Linux 7.3 (Valhalla)

本章重点介绍如何安装 Red Hat Linux 7.3，并配置它与计算机上已有的操作系统一起引导启动。它主要介绍基于 CD-ROM 的安装方式，因此非常适合希望获得快速、简单安装方案的新老用户。如果你是一位经验丰富的 Linux 用户，可以直接跳过本章，并在自己的系统上安装 Red Hat Linux。如果你有足够的实际经验，也可以略过本章的所有内容。但如果你是一个十足的 Linux 新手，或者只是出于好玩而决定体验一下 Linux，那么你可能需要了解更多关于如何将 Linux 与计算机上已有的另一个操作系统一同安装的信息。Red Hat 在安装过程中提供了出色的安装工具。但是，当你要在计算机上多引导 3 个操作系统时，始终建议使用“Custom（自定义）”安装，这会让 Linux 新手感到有些棘手。使用 Linux `fdisk` 或 Disk Druid 很容易；如果你使用的是 Red Hat 官方盒装版本，请务必使用随包装附带的《Red Hat Linux x86 官方安装指南》。否则，你随时可以查阅 Red Hat 官方网站上针对特定发行版的安装手册。Red Hat 的官方网站位于 http://www.redhat.com。请务必查阅 Red Hat 常见问题解答，以获得安装之前、期间或之后可能出现的问题和故障的答案。你可以在以下网址找到在线 FAQ：http://www.redhat.com/support/resources/faqs/rhl_general_faq/s1-contact.html。

Red Hat Linux 拥有一些令人兴奋且重要的安装特性。随着第 6 版的问世，安装过程得到了大幅改进。如今，在最新的 7.3 (Valhalla) 和 8.0 (Psyche) 版本中，Red Hat Linux 的安装过程非常流畅，Anaconda 为你完成了大部分繁重的工作。一些重要的安装特性包括“Kudzu”和“Kernel 2.4”。本章的内容可分为以下几个部分：

#### 1. Linux 中的磁盘驱动器与分区命名

在动手安装 Red Hat Linux 之前，让我们先简要了解一下 Linux 中磁盘驱动器和分区的命名约定。值得一提的是，我此前在讨论安装 FreeBSD 时，已经详细介绍过 FreeBSD 中驱动器和分区的命名约定。

Linux 使用一种特殊的方式来命名硬盘驱动器以及你在其中创建的分区。在 UNIX 术语中（请始终记住，Linux 内核只是 UNIX 的重新实现！），UNIX 系统（更具体地说是内核）无法读取和理解“设备”。对 UNIX 内核来说，一切都被抽象为“包含 ASCII 字符的文件”。这意味着，在 Linux 中，像“我有一个 30.0 GB 的 C: 驱动器”这样的说法根本没有任何意义。那么，让我们来看看在 Linux 下硬盘驱动器和分区是如何命名的。

其中，`/dev` 是 Linux 中根（“/”）目录下的目录，包含所有与设备相关联的设备文件。

那么 SCSI 驱动器呢？Linux 也会为它们命名！

其中，`/dev` 是 Linux 中根（“/”）目录下的目录，包含所有与设备相关联的设备文件。

现在，我们来谈谈 Linux 下的分区方案。在 Linux 中，我们首先要考虑一个特定的硬盘，无论是 IDE 硬盘还是 SCSI 硬盘。然后，再考虑它上面的分区。例如，IDE 驱动器上的分区按以下方式命名（以 `/dev/hda` 为例）：

如果在 Linux 下有一个“扩展分区”，其中包含几个逻辑磁盘驱动器，那该怎么办呢？实际上，Linux 内核也会将这些分区映射到存储在 `/dev` 目录中相应的“块设备文件”。让我们假设上面示例中的 `/dev/hda` 包含 1 个主分区和 1 个扩展分区，而该扩展分区中又有 5 个逻辑磁盘驱动器。那么，在这种情况下，分区表会是什么样子，又意味着什么呢？让我们看看 Linux 如何标记这种方案。Linux 会将其表示为：

- `/dev/hda`
  - `/dev/hda1`
  - `/dev/hda2`
    - `/dev/hda5`
    - `/dev/hda6`
    - `/dev/hda7`
    - `/dev/hda8`
    - `/dev/hda9`

其中，`/dev/hda1` 是所讨论硬盘上唯一的主分区，`/dev/hda2` 是唯一的扩展分区。请注意，Linux 将主分区从 `/dev/hda1` 一直标记到 `/dev/hda4`，而逻辑磁盘驱动器则从 5 延伸到 16。因此，在上面的示例中，`hda5` 到 `hda9` 是存在于该扩展分区上的 5 个逻辑磁盘驱动器。事实上，最近在我一位朋友的电脑上，我对硬盘进行了分区，并安装了 Microsoft Windows Millennium (ME)、Microsoft Windows XP Professional 和 Red Hat Linux 8.0 (Psyche)。执行 Linux `fdisk` 时，它显示的分区表与上面给出的完全一致。他使用一块 IDE 硬盘驱动器，在 Windows 下有一个标记为 `C:` 驱动器的主分区，其中包含 WinXP（FAT32 文件系统），而 `hda5` 和 `hda6` 被标记为



`D:` 和 `E:` 驱动器在 Windows 下（其中 `hda5` 实际上包含 Windows ME 版本（`FAT32` 文件系统）），而 `hda7`、`hda8` 和 `hda9` 用于 Linux。`hda7` 是 `/boot` 分区，`hda8` 是“根”（`/`）文件系统，`hda9` 是`swap`文件系统。这是在 Linux 中分区表的一个简单示例。如果您有相当多的分区并计划安装几个操作系统，请准备好在执行类似 `/sbin/fdisk /dev/hda` 的命令时看到更复杂的分区表（其中 `/dev/hda` 是您计算机上的主主盘）。

例如，当我在朋友的电脑上执行 Linux `fdisk` 时，它给出的输出类似于这样：

```
Command (m for help): p

Disk /dev/hda: 255 heads, 63 sectors, 5005 cylinders

Units = cylinders of 16065 * 512 bytes
```

| Device | Boot | Start | End | Blocks | Id | System |
|---|---|---|---|---|---|---|
| `/dev/hdc1` | * | 1 | 1275 | 10241406 | `c` | `Win95 FAT32 (LBA)` |
| `/dev/hdc2` |  | 1276 | 5005 | 29961225 | `f` | `Win95 Ext'd (LBA)` |
| `/dev/hdc5` |  | 1276 | 2550 | 10241406 | `b` | `Win95 FAT32` |
| `/dev/hdc6` |  | 2551 | 3825 | 10241406 | `b` | `Win95 FAT32` |
| `/dev/hdc7` |  | 3826 | 3831 | 48163+ | `83` | `Linux` |
| `/dev/hdc8` |  | 3832 | 4213 | 3068383+ | `83` | `Linux` |
| `/dev/hdc9` |  | 4214 | 4246 | 265041 | `82` | `Linux swap` |

## 2. Linux 中的文件系统

在简要讨论了 Linux 中的驱动器和分区标记方案之后，让我们谈谈 Linux 文件系统。Microsoft Windows 操作系统使用 `FAT16`、`FAT32`、`NTFS 4.0` 或最近发布的 `NTFS 5.0` 文件系统。GNU/Linux 内核最初使用的是“第一扩展文件系统”，通常表示为 `ext` 或 `extfs`。它现在已被 `ext2` 和 `ext3` 文件系统取代。内核 2.4 目前使用 Linux 原生的“第三扩展文件系统”，通常表示为`ext3`或`ext3fs`。尽管内核 2.2.x 和 2.4.x 支持 `ext2fs` 和 `ext3fs`，但最新的稳定版本即内核 2.4.20 使用`ext3fs`作为默认文件系统。`ext3fs` 是对 `ext2fs` 功能的扩展，就像 Windows 中 `NTFS 5.0` 对 `NTFS 4.0` 的扩展一样。`ext2fs` 和 `ext3fs` 文件系统之间的显著区别在于 `ext3fs` 是一个“日志文件系统”，而 `ext2fs` 不是。我们将在后面详细讨论这些文件系统，当我们将它们与 Unix 文件系统（`UFS`）进行比较时，后者是 FreeBSD 下的原生文件系统。

“Linux 程序员手册”中有一个名为`FILESYSTEMS(5)`的部分。它解释了 Linux 支持哪些文件系统类型。可以在 Linux 工作站的命令行上简单输入`man fs`来访问所有详细信息。它包括以下文件系统：`minix`、`ext`、`ext2`、`ext3`、`xia`、`msdos`、`umsdos`、`vfat`、`proc`、`nfs`、`iso9660`、`hpfs`、`sysv`、`smb`、`ncpfs`。当文件系统按惯例挂载在 `/proc` 上时，您可以在文件 `/proc/filesystems` 中找到当前内核支持的文件系统。如果您需要一个当前不支持的文件系统，您可以插入相应的模块或重新编译内核以创建新的内核。然后，只需安装新的自定义内核即可访问您选择的文件系统。要使用文件系统，您必须挂载它。

下面是对一些可用文件系统的简要描述。`minix` 是 Minix 操作系统中使用文件系统，是第一个在 Linux 下运行的操作系统。它有许多缺点：64MB 分区大小限制、短文件名、单一时间戳等。它仍然可用于软盘和 RAM 磁盘。`ext` 是 `minix` 文件系统的精细扩展。它已被完全扩展文件系统的第二版（`ext2`）取代，并在内核中被移除（在 2.1.21 中）。`ext2fs` 是 Linux 用于固定磁盘以及可移动介质的高性能磁盘文件系统。第二扩展文件系统被设计为扩展文件系统（`ext`）的扩展。`ext2` 在 Linux 支持的文件系统中提供了最佳性能（就速度和 CPU 使用率而言）。`ext3` 是 `ext2` 文件系统的日志版本。在 `ext2` 和 `ext3` 之间切换很容易。`xia` 是通过扩展 Minix 文件系统代码而设计和实现为稳定、安全的文件系统。它在不增加不必要的复杂性的情况下提供了最基本、最常请求的功能。`xia` 文件系统不再积极开发或维护。它在 2.1.21 中从内核中移除。`msdos` 是 DOS、Windows 和一些 OS/2 计算机使用的文件系统。`msdos` 文件名不能超过 8 个字符，后跟可选的句点和 3 个字符的扩展名。`umsdos` 是 Linux 使用的扩展 DOS 文件系统。它在 DOS 文件系统下增加了长文件名、UID/GID、POSIX 权限和特殊文件（设备、命名管道等）的功能，而不会牺牲与 DOS 的兼容性。

`vfat` 是 Microsoft Windows 95 和 Windows NT 使用的扩展 DOS 文件系统。`VFAT` 在 `MSDOS` 文件系统下增加了使用长文件名的功能。`proc` 文件系统不是通用文件系统。它是一个“伪文件系统”，用作内核数据结构的接口，而不是读取和解释 `/dev/kmem`。特别是，其文件不占用磁盘空间。`iso9660` 是符合 ISO 9660 标准的 CD-ROM 文件系统类型。Linux 支持 High Sierra，即 ISO 9660 标准的 CD-ROM 文件系统的前身。它在 Linux 下的 `iso9660` 文件系统支持中自动识别。Linux 还支持由 Rock Ridge Interchange Protocol 指定的 System Use Sharing Protocol 记录。它们用于进一步描述 `iso9660` 文件系统中的文件给 UNIX 主机，并提供诸如长文件名、UID/GID、POSIX 权限和设备等信息。它在 Linux 下的 `iso9660` 文件系统支持中自动识别。`hpfs` 是 OS/2 中使用的高性能文件系统。由于缺乏可用文档，该文件系统在 Linux 下是只读的。`sysv` 是为 Linux 实现的 SystemV/Coherent 文件系统。它实现了所有 `Xenix FS`、`SystemV/386 FS` 和 `Coherent FS`。`nfs` 是用于访问远程计算机上磁盘的网络文件系统。`smb` 是一个支持 SMB 协议的网络文件系统，由 Windows for Workgroups、Windows NT 和 Lan Manager 使用。要使用 `smbfs`，您需要一个特殊的挂载程序，可以在 `ksmbfs` 包中找到。`ncpfs` 是一个支持 NCP 协议的网络文件系统，由 Novell NetWare 使用。

## 3. 安装步骤摘要

现在我们已经在 Linux 下的分区方案和文件系统方面做了相当多的介绍，是时候进入实际的 Linux 安装了。有关 Red Hat Linux 安装的完整逐步介绍，请参阅 Red Hat 官方网站上的发行版特定安装指南。它们涵盖了所有类型的安装，并为 Linux 安装所需的所有步骤提供了适当的屏幕截图和技巧。在这里，我只会提到安装的重要步骤。使用这些步骤在您的计算机：

- 我保留 `/dev/hda1` 和 `/dev/hda2` 不变，并删除 `/dev/hda3`。结果，我获得了一些可用空间。然后我添加一个约 100MB 的 `/boot` 作为 `ext2fs`，接着添加一个约 128MB 的交换分区，最后通过将驱动器上的剩余空间分配给它来创建根分区（`/`）。这就是需要做的全部工作。因此，我们得到如下内容：

```
Command (m for help): p

Disk /dev/hda: 255 heads, 63 sectors, 2491 cylinders
Units = cylinders of 16065 * 512 bytes
```

| 设备 | 引导 | 开始 | 结束 | 块数 | Id | 系统 |
|---|---|---|---|---|---|---|
| `/dev/hda1` | 1 | 125 | 1004031 | `b` | `Win95 FAT32` |
| `/dev/hda2 *` | 126 | 1399 | 10233405 | `a5` | `FreeBSD` |
| `/dev/hda3` | 1400 | 1412 | 104422+ | `83` | `Linux` |



| `/dev/hda4` | 1413 | 2491 | 8667067+ | f | Win95 Ext'd (LBA) |
| `/dev/hda5` | 1413 | 1428 | 128488+ | 82 | Linux swap |
| `/dev/hda6` | 1429 | 2491 | 8538516 | 83 | Linux |

如上所示，`/dev/hda3`挂载为`/boot`，`/dev/hda5`是 Linux 交换文件系统，`/dev/hda6`挂载为`/`。

- 像往常一样继续安装，直到到达提示你选择引导加载程序的界面。这是本次安装中非常重要的一步，事实上，是最重要的一步。引导加载程序可以说是打开计算机后运行的第一个软件程序。主引导记录（MBR）是硬盘驱动器上的一个特殊区域，由计算机的 BIOS 自动加载。它是引导加载程序（无论是 LILO 还是 GRUB）控制整个引导过程的最早时机。GRUB 运行时，会读取其自身配置文件传递给它的指令（例如，Linux 加载程序的配置文件是 `/etc/lilo.conf`，GRUB 的配置文件是 `/boot/grub/grub.conf`），将重要指令传递给 BIOS，然后将相应的操作系统引导文件加载到计算机内存中。这进而使正确的文件系统能在正确的挂载点被挂载，从而让计算机为接下来的使用做好准备。因此，引导加载程序对于操作系统能否正确引导至关重要。
- 你可以使用 Linux 中可用的 2 个引导加载程序中的任意一个：Linux 加载程序（LILO）或 GNU 大统一引导加载程序（GRUB）。读者可以自由选择自己喜欢的任何一个。出于 FAQ 中所述的原因，我更喜欢使用 GNU GRUB。读者必须注意，本指南省略了 GRUB 的设计、实现和配置细节，因为这些内容超出了本指南的范围。互联网上有大量关于这些及其他“自由”和“专有”引导加载程序的信息。如果需要，可以去了解一下。

GRUB 是一个非常强大的基于 x86 的引导加载程序，可用于引导多种操作系统。GRUB 直接支持所有 GNU/Linux 发行版、FreeBSD、NetBSD、OpenBSD、Sun Solaris 等。它还支持使用“链式加载”技术引导其他专有操作系统。无论你的计算机上首先安装的是 Microsoft Windows 95/98 (SE)/Millennium Edition/NT/2K/XP，然后是 FreeBSD 4.8-RELEASE 或 OpenBSD 3.2-RELEASE；尽管放心，因为 GRUB 会凭借其强大的功能和动态特性处理好一切。如果你的计算机安装的是默认没有引导加载程序的 Microsoft Windows 95/98 (SE)/Millennium Edition（不同于 Microsoft Windows NT/2K/XP），那么就“将 GRUB 添加到 MBR”。

- 启动后，你会看到 GRUB 界面，提示你选择操作系统。如果你的计算机安装的是 Microsoft Windows NT/2K/XP，它默认使用“NT 引导加载程序”来引导操作系统软件，那么也请“将 GRUB 添加到 MBR”。不要惊慌！这完全不会造成任何问题。只是在这种情况下，成功启动后，你会看到 GRUB 界面提示你选择操作系统。列表中会有 2 个条目，例如，我有“Windows”和“Linux”。选择“Linux”并按回车会将 Red Hat Linux 引导文件加载到计算机内存中，然后计算机自举进入 Linux。然而，在另一方面，选择“Windows”并按下回车键会利用“链加载”机制，调用“FreeBSD 引导加载器”。FreeBSD 引导加载器随后会将 Microsoft Windows 98（SE）加载到计算机内存中。

10. 这基本上解释了一切。将 GRUB 添加到主引导记录（MBR）后，照常进行安装。读者必须注意，他/她可以将 GRUB 安装在两个位置之一：要么是 MBR，要么是活动分区的引导扇区。如果你计划在系统上使用另一个引导加载器（例如 OS/2 的 Boot Manager、Windows NT 的 NT 引导加载器，或任何商业引导加载器，如 System Commander 和 Partition Magic），请将 GRUB 添加到“你的根分区的第一个扇区”，然后配置其他引导加载器来启动 GRUB（GRUB 随后会引导 Red Hat Linux）。

11. 一旦你创建了分区并将 GRUB 安装到 MBR 中，剩下的就是照常进行安装，按你的意愿选择要安装的软件包（之后你也可以在命令行中使用 `RPM` 命令安装它们），以此类推。最后，完成 Red Hat Linux 的安装。当提示创建“引导盘”时，请务必创建一张。在系统崩溃时它会派上用场。你之后也可以随时在命令行界面（CLI）模式下使用 `/sbin/mkbootdisk` 命令创建“安装引导盘”。

12. 根据你之前选择的软件包数量以及计算机的资源，安装完成将需要一些时间。在软件包安装期间，请坐下来放松一下。或者跑去附近的麦当劳买个汉堡包，一两个也行。对于各位专家而言，读完所有这些内容后，如果你确实觉得有什么地方表述或解释有误，请务必给我留几句话。对于绝对的新手，我有一个简单的建议：练习、练习、再练习，直到你变得完美。成功绝对没有捷径。这是完全不可能的。

13. 在所有软件包成功安装并配置好后，你的 Red Hat Linux 安装即告完成，Linux CD-ROM 会从光驱中弹出，计算机将自动重启。如前所述，成功启动后，你会看到 GRUB 屏幕，提示你选择要引导的操作系统。根据你安装时的配置，列表中会有 2 个条目，例如，我有“Windows”和“Linux”两个选项。通过依次引导进入每个操作系统，检查两者是否都能正常工作。我 100% 确定一切都会运行良好。

14. 如果一切正常，那么就该欢呼了。如果不巧某个地方出了问题，那么根据具体是哪里出了什么问题，可以采取许多措施。我真诚地请求读者，如果某个地方出了差错，一定要记下一切。如有必要，可以在纸上写一份简短报告。这对后续诊断大有帮助。现在，是时候在 Red Hat Linux 环境中配置 FreeBSD，使 GRUB 也能通过“链加载”机制引导 FreeBSD 了。

15. 登录 Red Hat Linux，使用 `vi` 编辑器打开 `/boot/grub/grub.conf` 文件。编辑时务必非常小心。由于 GRUB 在引导计算机时会读取 `/boot/grub/grub.conf` 文件，因此该文件中的拼写错误可能导致灾难性后果。读者必须注意：GRUB 没有像 LILO 那样的工具来检查配置；LILO 使用命令提示符下的 `/sbin/lilo -v -v` 命令来检查 `/etc/lilo.conf`。因此，在使用 GRUB 引导操作系统时请格外小心。现在，在“Windows”条目之前添加一个 FreeBSD 条目。编辑后的 `/boot/grub/grub.conf` 文件应该类似于这样：

```
default=0
timeout=150
splashimage=(hd0,2)/grub/splash.xpm.gz

title Linux (2.4.18-3)
    root (hd0,2)
    kernel /vmlinuz-2.4.18-3 ro root=/dev/hda6

title FreeBSD
    root (hd0,a)
    kernel /boot/loader ro root=/dev/hda2

title Windows
    rootnoverify (hd0,0)
    chainloader +1
```

16. 如上所示，第一个块用于引导 Linux，第二个块用于引导 FreeBSD，最后一个块用于引导 Windows 98（SE）。读者必须注意第一块和第二块第二行中 `root` 一词之后的条目。它定义了计算机硬盘上引导操作系统所需的启动文件所在的确切位置。在 Linux 系统中，我们可以看到 `(hd0,2)` 指的是第 3 个分区，即 `/dev/hda3`。而我们已经知道，`/dev/hda3` 指的是包含启动文件的 `/boot` 分区。类似地，在 FreeBSD 系统中，我们可以看到 `(hd0,a)` 指的是 `/dev/ad0s2a`，即根（/）文件系统，在 Linux 系统中它被映射为 `/dev/hda2`。Windows 块中提到的 `rootnoverify` 告诉 Linux 内核不要挂载 `/dev/hda1` 分区，因为它不是 Linux 文件系统。

17. 现在当你重新启动时，你就拥有了一个多引导系统，可以引导进入三个操作系统中的任意一个：Windows 98（SE）（在我的计算机上）、FreeBSD 4.8-RELEASE 或 OpenBSD 3.2-RELEASE 或 NetBSD 1.6.1，以及 Red Hat Linux 7.3。这就是准备一个功能齐全的多引导系统真正需要做的全部工作。如果你想知道如何在不同操作系统上挂载不同的文件系统，请继续阅读下一章，第 7 章：挂载文件系统。

### 3.7 挂载文件系统



你的电脑现在安装了 Microsoft Windows 操作系统，要么是 FreeBSD 4.8-RELEASE，要么是 OpenBSD 3.2-RELEASE 或 NetBSD 1.6.1 以及 Red Hat Linux 7.3，并且它们和平共处。够了吗？够了吗？我敢肯定，不够！

我之所以在我的电脑上同时运行 Microsoft Windows 98(SE) + FreeBSD 4.8-RELEASE + Red Hat Linux 7.3（我正在用这台电脑编写你现在阅读的本指南的一部分），其中一个最重要的原因是我大部分时间都在 FreeBSD 和 Linux 上工作，但由于大学的项目，我需要访问 Windows。因此，我需要不时地访问 Windows 分区上存储的数据。

但是，每当我在 FreeBSD 上工作并且需要访问 Windows 分区上的某些数据时，我根本负担不起重新启动电脑，登录 Windows，将文件复制到软盘，然后注销，再次重新启动，登录 FreeBSD，然后将软盘的内容复制到 FreeBSD 系统上的 `/home/ghosh` 目录的过程。这种过程既不漂亮，也不合逻辑，更不可行。

多亏了 FreeBSD 和 Linux 系统上的 `mount` 命令，我每次偶尔需要访问 Windows 分区上的某些数据时，就不必经历这个“不漂亮，也不合逻辑，更不可行”的过程。

`mount` 命令绝对是 *nix 系统上超级用户（或 `root`）账户可用的最重要的命令之一。它允许 *nix 系统的 `root` 用户挂载文件系统（供普通用户访问和使用），这些文件系统可能位于同一台计算机上，也可能不在同一台计算机上。换句话说，`mount` 命令允许你使用访问远程节点的适当路径来挂载本地文件系统（物理上存在于同一台计算机上）或远程文件系统。`mount` 命令首次出现在 Version 1 ATTUNIX 中。请参阅你 FreeBSD 或 OpenBSD 或 Linux 系统上 `mount` 命令的手册页，以深入分析可以传递给 `mount` 命令的所有可能选项。

尽管它在 Unix 或类 Unix 系统上是一个非常强大的命令，但 `mount` 命令本身非常简单易用。`mount` 命令的语法是：`mount -t filesystem device_name mount_point`。这意味着你指示 `mount` 命令考虑名为 `device_name` 的设备文件，其文件系统类型由开关 `-t filesystem` 指定，然后将其 graft 到现有 FreeBSD/OpenBSD/Linux 系统的名为 `mount point` 的目录上。很可爱！

本章分为以下几个部分：

## 1. 在 FreeBSD 中挂载文件系统

要在 FreeBSD 系统上挂载 Linux 第二扩展文件系统（ext2fs），我必须构建并安装一个定制的 FreeBSD 内核。在 FreeBSD 中构建和安装自定义内核很容易。我以 `"root"` 身份登录并执行以下步骤来构建一个：

完成此操作后，我尝试使用命令挂载 Linux 分区：

```
mount -t ext2fs /dev/ad0s3 /mnt/linux
```

假设 `/dev/ad0s3` 是代表 Linux 文件系统的 FreeBSD 分区，并且 `/mnt/linux` 目录存在。文件系统应在指定的目录作为挂载点处挂载。

要挂载 MSDOS 分区以及 Windows 95/98(SE)/ME 格式的 FAT16 和/或 FAT32 文件系统，我执行以下命令：

```
mount -t msdos /dev/ad0s1 /mnt/windows
```

其中，`/dev/ad0s1` 是代表我电脑上 Windows 98(SE) 分区的 FreeBSD 分区，并且 `/mnt/windows` 目录存在。要卸载，我简单地执行：

```
umount /mnt/windows
```

要挂载基于 MSDOS 的软盘，我执行：

```
mount -t msdos /dev/fd0 /mnt/floppy
```

要卸载，我简单地执行：

```
umount /mnt/floppy
```

对于拥有 NTFS 文件系统的人，他们可以尝试使用命令挂载：

```
mount -t ntfs /dev/fd0 /mnt/floppy
```

并使用以下命令卸载：

```
umount -t ntfs /dev/fd0 /mnt/floppy
```

读者必须注意：NTFS 文件系统的写入支持有限。

## 2. 在 Linux 中挂载文件系统

在 Linux 下挂载 FreeBSD 文件系统即 UFS（Unix FileSystem）需要构建并安装自定义 Linux 内核。构建 Linux 内核是一项简单的工作，你可以参考你能获取的任何文档。在这里，我只是指定主要步骤。要构建自定义 Linux 内核，我以 `root` 身份登录并执行以下步骤：

`Makefile.bak.`

一旦新构建的自定义 Linux 内核安装完成，你就可以开始使用它来挂载 UFS 文件系统。使用此命令：

```
mount -t ufs /dev/hda2 /mnt/bsd
```

前提是 `/dev/hda2` 是 FreeBSD 切片且 `/mnt/bsd` 存在。使用命令简单卸载：

```
umount /mnt/bsd
```

要在 Linux 上挂载 Windows 95/98/ME FAT32 文件系统，请使用命令：

```
mount -t vfat /dev/hda1 /mnt/windows
```

`/mnt/windows` 目录必须存在于系统上。通过执行命令简单卸载：

```
umount /mnt/windows
```

对于使用 NTFS 文件系统的读者，有坏消息！他们必须在配置文件中包含 NTFS 文件系统支持并构建自定义 Linux 内核。读者必须注意：NTFS 写入支持是危险的且有限的。

## 4. 故障排除

尽管 FreeBSD、OpenBSD 和 GNU/Linux 操作系统都是非常出色的软件，但在将它们全部或组合双启动或多启动 PC 时，人们经常会遇到问题。问题范围从易于检测和排除的到非常奇怪的问题。故障排除，正如所有 UNIX 老手所知（并欣赏），并不是一门精确的艺术。在本章中，我列出了我在双启动和多启动系统时遇到的一些问题，这些系统使用不同的操作系统和硬件。

读者必须注意，根据使用的特定硬件和发行版/版本，他们可能会遇到下面列出问题的略有不同版本。如果你遇到一个全新的问题，或者可以通过提供下面列出问题的更好解决方案为本指南做出贡献，请务必给我发邮件至：`subhasish_ghosh@linuxwaves.com`。

我个人在多启动系统方面的经验看到了一些奇怪的故障类型，并且经常出现不稳定的行为，但大多来自 Linux 的 `fdisk` 和安装程序。我经常为以后诊断和排除故障而做笔记。正如我所能得出的结论，在 Linux 发行版（包括 Red Hat、Slackware、SuSE 和 Mandrake）、OpenBSD 和 FreeBSD 版本中，FreeBSD 的 `fdisk`、`disklabel` 和整体安装程序（`/stand/sysinstall`）是其中最好的，绝对没有错误和突然崩溃。

最初，我总是认为必须有一种精确的方式来安装所有这些操作系统，或者必须遵循一个确切的顺序，但随着时间的推移，我学到了真相：只要硬件支持良好，安装 CD-ROM 没问题，安装程序的不稳定行为是由于之前安装的未擦除数据造成的。因此，在致力于创建多启动系统之前，请确保在全新格式化的硬盘上开始安装。继续阅读以了解该程序的详细信息！

一些常见的读者问题包括：

### Q1. 我创建了一个扩展分区，其中包含逻辑磁盘驱动器或其内的子分区。但当我安装 FreeBSD 时，它完全忽略了该分区内的内部分区。这是正常的吗？

**Ans1:** 是的，这绝对正常。FreeBSD 操作系统软件只能检测并表示它称为“slices”的主硬盘分区。扩展分区虽然会在 FreeBSD `fdisk` 中表示，但不会表示容器的组成部分。

### Q2. 我已成功在我的 PC 上安装了 FreeBSD 和 OpenBSD 操作系统。当我尝试安装 Red Hat Linux 时，Linux 的 `fdisk` 显示了“too many partitions”错误消息。这是什么意思？我现在可以做什么？

### Q3. 我删除了我 PC 上 FreeBSD、OpenBSD 和/或 NetBSD 操作系统的早期安装。当我尝试安装 Red Hat Linux 时，Linux 的 `fdisk` 显示了“too many partitions”错误消息。我现在应该做什么？

**Ans2 and Ans3:** 正如读者所见，由 Red Hat Linux `fdisk` 工具标记的此错误信息可能在多种条件下出现。我自己在多系统启动 PC 时就曾遇到过这两种情况。当此信息显示时，Linux 的 `fdisk` 无法对磁盘进行任何更改。

个人而言，我强烈感觉到此信息：“分区太多（16，最大为 8）”通常在你有来自之前安装的 FreeBSD 和/或 OpenBSD 和/或 NetBSD 的未擦除数据时出现。这通常发生在那些数据分区被删除，但包含在主引导记录（MBR）中的主分区表（MPT）未被覆盖时。由于此问题似乎不会出现在干净的硬盘上，我得出结论，它只会在你的硬盘上存在旧的 BSD 磁盘标签数据时出现。



一旦此错误被标记，你几乎无能为力，因为无论你做什么或输入什么，都不会有任何内容写入磁盘。如果碰巧你在执行全新安装时遇到此错误，请从 MS-DOS 提示符下执行`fdisk /mbr`，然后再次尝试安装 Red Hat Linux。如果碰巧你的系统上已经安装了 FreeBSD/OpenBSD/NetBSD，那么（对不起兄弟！）请擦除所有之前的安装，使用`dd`实用程序或你手头可用的任何工具彻底擦拭磁盘，然后重新开始安装所有内容。

#### Q4. 我在我的 PC 上执行 Red Hat Linux 的全新安装，该 PC 之前有多重 FreeBSD 和/或 OpenBSD 和/或 NetBSD 安装。我从 Red Hat Linux `fdisk` 获得了 “分区太多” 错误。我不能在我的硬盘上执行 Red Hat Linux 的完整安装来删除硬盘上的 BSD 磁盘标签数据吗？

Ans4: 不行。一旦此错误被标记，即使是通常会清除所有分区信息的 `fdisk` 的 `o` 选项也不会起作用。即使你使用 Disk Druid 磁盘分区工具成功完成仅 Linux 的 “整盘” 完整安装，这也不会擦除旧的且已存在的 BSD 磁盘标签信息。迟早，你会遇到麻烦。

#### Q5. 我删除了 PC 上包含数据的所有现有分区。但我想确保并使用某种 “专业” 磁盘擦除实用程序彻底擦拭我的磁盘。我可以使用哪些？该如何使用？

Ans5: 专门设计用于擦除磁盘的第三方分区管理器和安全软件可用于此目的。个人而言，我没有使用任何第三方工具擦拭硬盘的经验，因为我更喜欢使用基于 UNIX 的`dd`实用程序。

UNIX 的`dd`也可用于彻底擦拭磁盘。它将零写入可从 FreeBSD、OpenBSD 和 Linux 安装光盘访问的磁盘表面。这可通过从 OpenBSD 安装光盘选择 shell 选项而不是安装，或在任何时候使用 [Ctrl+C] 退出 OpenBSD 安装来轻松访问。清除第一块 IDE 硬盘的 OpenBSD 命令是`dd if=/dev/zero of=/dev/wd0c`。Red Hat Linux 安装光盘的救援模式是一个单用户提示。你不必挂载系统，因为你是要擦除它，而不是 “救援” 它。一旦获得`#`提示，`dd if=/dev/zero of=/dev/hda`将清除第一块磁盘。FreeBSD 主安装菜单中的 “Fixit” 选项可访问单用户提示；需要四个安装光盘中的第二个。命令`dd if=/dev/zero of=/dev/ad0`似乎会清除第一块磁盘。一旦完成，你可以确信你的硬盘已被彻底擦拭干净！

#### Q6. 我使用 UNIX `dd` 实用程序彻底擦拭了我的硬盘。随后我在我的 PC 上执行了 Red Hat Linux 的全新安装，然后是 FreeBSD 安装。我将 FreeBSD 引导管理器安装到 MBR 中。现在我的系统无法启动！发生了什么？我做错了什么？或，

#### Q7. 我使用 UNIX `dd` 实用程序彻底擦拭了我的硬盘。随后我在我的 PC 上执行了 Red Hat Linux 的全新安装，然后是 OpenBSD 安装。我将 OpenBSD 引导管理器安装到 MBR 中。现在我的系统无法启动！发生了什么？我做错了什么？

Ans6 and Ans7: 到处都没有出错。但你在最开始犯了一个小却致命的错误。务必记住，当你使用 UNIX`dd`实用程序将零写入硬盘表面时，它也包括主引导记录（MBR）区域。具有地址（0,0,1）的 MBR 区域：柱面地址 0，磁头地址 0 和扇区地址 1，也就是说，硬盘的前 512 字节，其中包含主分区表（MPT）和初始程序加载（IPL）代码。当此区域被零覆盖时，不同的操作系统会以不同的方式反应和行为。它们反应奇怪，因为它们期望标准的 IPL 代码，但却发现没有。

例如，Red Hat Linux `fdisk`将零化的分区表报告为无效并可以重新创建空表；它安装的唯一 IPL 代码是 LILO 或 GRUB，而不是标准 IPL 代码。OpenBSD 只是显示一个空的分区表，并且在这种硬盘上引导时会造成大量问题。据报道，唯一能从完全零化的磁盘无错误地完美引导的操作系统是 FreeBSD。但我个人确实遇到过一种情况（由于奇怪的原因）FreeBSD 引导被锁定，根本无法引导。

为防止所有这些发生，只需从带有`FDISK.EXE`的 Windows 9x 或 DOS v6 启动盘启动系统。一旦系统启动到 MS-DOS 提示符，输入以下内容：`A:\>fdisk /mbr`。它会将 MBR 重新初始化为正常状态并重写 MPT 并创建标准 IPL。继续按通常方式安装操作系统。

#### Q8. 我在我的 PC 上安装了 Red Hat Linux，但在将 LILO 安装到主引导记录（MBR）时，我收到错误提示，安装程序无法将此信息写入 MBR。发生了什么？

Ans8: 你要么在 PC 上锁定了硬盘的 MBR，要么启用了病毒扫描软件阻止写入 MBR。你必须访问计算机系统的 BIOS 并验证 MBR 未被写保护。根据系统，你的 MBR 中可能已经有另一个与 LILO 冲突的引导加载程序。尝试从 MS-DOS 命令提示符执行`fdisk /mbr`并安装 LILO。

#### Q9. 我前几天在我的 PC 上安装 OpenBSD 3.2。在 OpenBSD `fdisk` 中创建分区后，当我保存更改并使用`quit`选项退出 `fdisk` 时，它以亮白色在蓝色背景上标记了一些警告： “`wd0`: no disk label”。这是什么意思？我做错了什么？

Ans9: 绝对没有。你什么也没做错。当你退出 OpenBSD `fdisk`（使用`quit`选项保存更改），并且 OpenBSD 分片不在与之前安装的 OpenBSD 系统相同的偏移量时，`fdisk`会显示`wd0: no disk label`消息。虽然它看起来像警告信息或明显错误，但实际上它是一个重要信息

flagged by OpenBSD 安装程序，该程序向你保证虽然数据和 OpenBSD 特定分区已经创建，但 OpenBSD 磁盘标签仍需设置。磁盘标签定义了 OpenBSD 文件系统在硬盘上 OpenBSD 分区上的布局。

在双启动和多启动系统中，此消息几乎是正确 OpenBSD 安装的先决条件。如果在保存对 OpenBSD `fdisk` 的更改后，你没有看到此消息，则意味着 OpenBSD 磁盘标签正在读取并使用来自之前安装的信息。这是危险的情况，因为如果磁盘标签使用旧的磁盘标签数据，并且自其最初创建以来任何分区信息已发生变化，则磁盘标签的行为会变得不稳定，你可能会遇到奇怪的问题。为防止这种情况发生，请确保在执行 OpenBSD 干净安装之前先清除磁盘。

#### Q10. 我的 PC 上安装了 FreeBSD 4.8-RELEASE 和 OpenBSD 3.2-RELEASE 操作系统。我尝试在剩余的硬盘空间上安装 Red Hat Linux。但每次我尝试使用 `fdisk` 或 Disk Druid 磁盘分区工具时，它都会标记出奇怪的错误信息。为什么会这样？ 我该如何将 Red Hat Linux 安装到我的系统上？

Ans10: 对此问题的诚实回答是：“没人确切知道为什么！”。多年来在执行双启动和多启动安装时，我注意到只要 OpenBSD 操作系统在附近，Red Hat Linux 的 `fdisk` 和 Disk Druid 就会标记出最多的错误信息。OpenBSD 对分区表的 `fdisk` 处理方式与 FreeBSD 和 Linux 不同，并且不符合标准。这可能是众多可能解释之一。

例如，让我描述一个真实情况。这发生在几周前（撰写本指南时）。我在测试 PC 上安装了 OpenBSD 3.2，然后安装了 FreeBSD 4.8。然后我尝试将 Red Hat Linux 8.0（Psyche 版）安装到计算机上剩余的硬盘空间上。读者必须注意：我的系统上没有任何有故障的硬件，我满足所有硬件兼容性要求，我使用 UNIX `dd` 实用程序在开始安装前清除了磁盘，我系统上可用的内存（物理 RAM）绝对是 100% 正确，并且 Red Hat Linux 8.0 安装 CD-ROM 完好无损。然而，每次我尝试将 Linux 安装到我的系统上时（每次使用不同的启动时命令行选项），Linux 的 `fdisk` 都开始出现多个对话框。第一个说“`/tmp/hda`上存在无效分区”。当我忽略该错误时，一个新的对话框显示“无法正确对齐分区。这可能意味着另一个分区工具生成了不正确的分区表，因为它没有正确的 BIOS 几何结构。可以安全忽略，但忽略可能会导致某些引导加载程序出现（可修复的）问题”。`Fdisk` 然后显示“分区过多”错误。错误、错误、错误就是我得到的一切！所以，我切换到 Red Hat Disk Druid 来碰碰运气！

Red Hat 的 Disk Druid 显示了“`/tmp/hda`上存在无效分区”消息，忽略后显示 OpenBSD 分区未使用且 `/dev/hda` 为 BSD/386 分区。我强制执行“自动分区”过程，但它在一段时间后以“未处理的异常”惨败。我没有将崩溃转储保存到软盘，因为我没有发送错误报告的计划。



这种情况发生在 Red Hat Linux 8.0（Psyche）上。我在 Red Hat Linux 发行版 7.3 和 7.1 上也遇到了相同的问题。但当我尝试安装 Red Hat Linux 7.0 时，它毫无痛苦地安装，没有任何喊叫和哭泣。有谁在那里（或更具体地说在 Red Hat Inc.）能请解释一下到底发生了什么，或者 Red Hat Linux 7.0 有什么特别之处，其他版本没有？我仍在试图弄清这个问题！

## Q11. 我读了上面的 PR（问题报告）。我的 PC 上也安装了 FreeBSD 和 OpenBSD 操作系统。但我想在我的系统上安装除 Red Hat 之外的 Linux 发行版。你建议哪一个？

Ans11: 如果你已经阅读并理解了上面的 PR，那么你尝试在系统上安装哪个 Linux 发行版根本毫无意义。我在尝试在测试计算机上安装 Mandrake 9.0 以及 SuSE 7.0 时也遇到了类似问题。Mandrake Linux 管理创建分区、格式化它们，但在安装软件包时也惨败。SuSE 7.0 在一开始就崩溃了！在不久的将来，我想测试 Red Hat Linux 9 在此类系统上的完整性！

## Q12. 在我的计算机上安装 FreeBSD 4.X-RELEASE 时，FreeBSD `fdisk`（或 `disklabel`）使用了 `'X'` 分区名称而不是 `/dev/ad[0-3]s[1-4]n` 标记方案。嘿！到底发生了什么？那个 `'X'` 代表什么？

Ans12: FreeBSD 操作系统软件允许每个切片 7 个分区（`c:` 保留用于整个硬盘空间）。如果你在 PC 上创建了太多分区，FreeBSD `fdisk` 会使用 `'X'` 分区而不是有效的分区名称，例如 `/dev/ad0s1a`。如果你有一个标记为 `'X'` 的分区，你必须立即删除它，而不要继续进行。如果不删除此分区，FreeBSD `disklabel` 会让你继续整个安装，然后当你最终完成完整安装后，当你的系统启动时，你会遇到错误并被放入单用户模式进行维护。因此，换句话说，如果你不删除标记为 `'X'` 的分区，FreeBSD 将无法完成启动序列。相反它会显示错误消息并进入单用户模式。

Previous    Home    Next

## 5. 结论

各位朋友，这就将我们带到了创建配置了三种现代操作系统的多启动系统的旅程的终点。假设你已按照本指南的每一步操作并且一切顺利，请允许我祝贺你的成功。如果出现问题，请确保阅读相关操作系统的文档和手册。否则你也可以随时参考在线手册和资源。

请务必浏览以下链接：

- Distribution specific Official Red Hat Linux Installation and Upgrade manuals
- Linux Kernel resources
- Linux Loader (LILO) and other boot loader questions
- Red Hat Linux Hardware questions

对于专门涉及“多启动”的在线手册，我认为以下是最好的：

- Installing and Using FreeBSD With Other Operating Systems
- An excellent page explaining booting process and methodologies.

最终，尽管如此，任何你可能发现的错误或遗漏的责任在我，我独自承担，所以请将你的不满发送到 subhasish_ghosh@linuxwaves.com。对于希望发送 PR（问题报告）的人，请确保发送足够有效且相关的信息供我使用。如果你只是发送类似“这搞砸了！”、“那不工作！”之类的邮件，我无法帮助你。尝试发送详细的 PR。你的评论、建议和更正很可能会反映在本指南的下一个版本中。谢谢！
