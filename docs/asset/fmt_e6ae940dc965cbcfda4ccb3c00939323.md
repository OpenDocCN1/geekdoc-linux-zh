
在此类别中，最常见的问题涉及 LILO 配置问题。这些问题的诊断和解决方案可在 Linux 文档项目网站上的 LILO mini-HOWTO 中找到，网址为 http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/LILO.html。

如果你遇到 GRUB 问题，GRUB 手册可在网上查阅，网址为 http://www.gnu.org/software/grub/manual/。

### TIP

要获得最佳效果，请前往 http://www.google.com/linux 在互联网上查找所有关于 Linux 的内容。Google 已专门创建了其数据库中的 Linux 区域，这应该能让你比任何其他搜索引擎更快地访问 Linux 相关信息。

Usenet 新闻组帖子可在 http://www.google.com/grphp 搜索。邮件列表讨论可在邮件列表 ARCHives（MARC）中搜索，网址为 http://marc.theaimsgroup.com/。

### 相关 Ubuntu 和 Linux 命令

在 Ubuntu 中管理内核及其模块时，你将使用以下命令：

- `gcc`—GNU 编译器系统
- `make`—GNU 项目和文件管理命令
- `mkbootdisk`—Ubuntu 的启动磁盘创建工具
- `sysctl`—运行时操作内核变量的接口
- `mkinitrd`—为引导加载支持创建 RAM 磁盘文件系统
- http://www.kernel.org/—Linux 内核档案。所有 Linux 内核开发讨论的源头。
- http://www.kerneltraffic.org/kernel-traffic/index.html—Linux 内核动态。每周发布的 Linux 内核邮件列表的摘要和评论。
- http://www.gnu.org/—自由软件基金会。内核编译过程中所用程序的手册和软件来源。诸如 `make` 和 `gcc` 的工具的官方文档均在此处。
- http://slashdot.org/article.pl?sid=01/08/22/1453228&mode=thread—著名的 Alan Cox AC 补丁，以其名字命名。
- http://www.digitalhermit.com/linux/Kernel-Build-HOWTO.html—Linux 内核重建指南；配置、编译和故障排除。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/KernelAnalysis-HOWTO.html—内核分析 HOWTO。描述内核神秘的内部工作机制。
- http://www.tldp.org/HOWTO/Module-HOWTO/—内核模块 HOWTO。包含关于未解析符号的精彩讨论。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Modules.html—Linux 内核模块安装 HOWTO；一篇关于重新编译内核模块的较老文档。
- http://www.tldp.org/—Linux 文档项目。所有 Linux 文档的圣地。优秀的 HOWTO 文档、常见问题解答和在线书籍的来源，全部关于 Linux。
- http://www.minix.org/—非官方的 Minix 网站。它包含一系列指向 Minix 信息的链接以及到其实际主页的链接。虽然 Minix 仍受版权保护，但其所有者已授予所有人无限权利。亲自看看用于开发 Linux 的操作系统吧。
- http://jungla.dit.upm.es/~jmseya/linux/kernel/hackers-docs.html—网页，包含 Linux 内核文档、书籍、黑客巨著以及其他对新手和经验丰富的 Linux 内核及内核模块开发者有帮助的信息。如果你安装了 Ubuntu 内核源码，也可以在文件 `/usr/src/linux-2.6/Documentation/kernel-docs.txt` 中找到此列表。

# 附录 A

## Ubuntu 内部探秘

正如任何新事物一样，了解一下它的历史是值得的。Ubuntu 也不例外，在本附录中，你将进一步了解 Linux（以及 Ubuntu）的由来。

### 什么是 Linux？

Linux 是由 Linus Benedict Torvalds 于 1991 年首次开发并发布给世界的自由操作系统的核心，即内核。当时 Torvalds 是芬兰赫尔辛基大学的研究生，现在是 Linux 基金会（http://www.linux-foundation.org/）的研究员。他是一名工程师，之前曾在 CPU 设计和制造公司 Transmeta, Inc. 工作。对所有 Linux 用户来说幸运的是，Torvalds 选择在名为 GNU 通用公共许可证（GPL）的自由软件许可证下分发 Linux。

> **注意**
>
> 免费的在线资源维基百科上有一篇关于 Linus Torvalds 的精彩传记，记述了他的生平和显著成就。你可以在 http://en.wikipedia.org/wiki/Linux_Torvalds 找到它。或者你可以前往 http://groups.google.com/group/comp.os.minix/msg/b813d52cbc5a044b?hl=en 阅读 Linus 向世界发布的关于 Linux 的第一篇帖子的副本。

### 本附录内容

- 什么是 Linux？
- 为什么要使用 Linux？
- 什么是 Ubuntu？
- 面向企业的 Ubuntu
- 家庭中的 Ubuntu
- 64 位 Ubuntu
- PPC 平台上的 Ubuntu
- 多核机器上的 Ubuntu
- 充分利用 Ubuntu 和 Linux 文档
- Ubuntu 开发者与文档
- 参考

GNU GPL 是自由软件基金会创始人 Richard M. Stallman 的杰作。Stallman 是 Emacs 编辑环境和 GCC 编译器系统的著名作者，他精心制定了 GPL，以确保使用 GPL 许可的软件始终是自由的，并以源代码形式提供。GPL 是 Linux 及其所有权、分发和版权的指导性文件。Torvalds 持有 Linux 商标的权利，但得益于他的慷慨、互联网、全球数千名程序员、GNU 软件以及 GNU GPL，Linux 将永远保持自由，不受许可或版税问题的困扰。

### 发行版本与内核编号方案

Linux 内核、内核开发以及 Ubuntu 的内核版本有一套特定的编号系统。请注意，这些数字与你的 Ubuntu Linux 发行版的版本号没有任何关系。Ubuntu 发行版的版本号由 Ubuntu 开发者指定，而大多数 Linux 内核版本号则由 Linus Torvalds 和他的内核开发者大军指定。

要查看你的 Linux 内核的编译日期，请使用带 `-v` 命令行选项的 `uname` 命令。要查看你的 Linux 内核版本，请使用 `-r` 选项。数字（如 2.6.24-5）代表主版本号（2）、次版本号（6）和补丁级别（24）。最后一个数字（5）是开发者补丁级别，由 Ubuntu 开发者指定。

偶数次版本号被认为是“稳定版”，通常适合在生产环境中使用，而奇数次版本号（如尚不存在的 Linux 2.7 源代码树）代表正在开发和测试的 Linux 内核版本。本书只包含 Linux 内核的稳定版。你可以选择下载并安装内核的测试版，但对于用于日常使用的系统，不建议这样做。大多数情况下，安装测试版内核是为了提供对新硬件或操作系统功能的支持与测试。

Linux（发音为“lih-nucks”）是自由软件。将 Linux 内核与 GNU 软件工具（驱动程序、实用程序、用户界面以及诸如 X.Org 基金会的 X Window 系统等其他软件）相结合，就构成了一个 Linux 发行版。有许多来自不同供应商的 Linux 发行版，但许多都源自或紧密模仿 Debian Linux 发行版，Ubuntu 正是基于 Debian 发行版。

> **注意**
>
> 要了解有多少发行版基于 Debian Linux，请访问 http://www.linux.org/，点击“发行版”，然后搜索“Debian-based”。在撰写本文时，已有 52 个发行版得益于 Debian。

## 为什么使用 Linux？

数百万聪明的计算机用户已将 Linux 用于工作超过 14 年。过去一年里，来自多个国家的个人、小型办公室/家庭办公室（SOHO）用户、企业和公司、学院、非营利组织以及政府机构（地方、州和联邦）都已成功地将 Linux 纳入使用。而且，今天 Linux 正被纳入许多信息服务/信息技术（IS/IT）环境中，作为提高效率、安全性和成本节约的一部分。出于以下等原因，使用 Linux 是一个好主意：
