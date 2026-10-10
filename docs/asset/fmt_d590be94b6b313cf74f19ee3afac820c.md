
- http://www.tldp.org/HOWTO/Module-HOWTO/—内核模块 HOWTO。包含关于未解析符号的良好讨论。

- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Modules.html—Linux 内核模块安装 HOWTO；一份较旧的文档，讨论重新编译内核模块。

- http://www.tldp.org/—Linux 文档项目。它是所有 Linux 文档的圣地。它是 HOWTO 文档、常见问题解答（FAQ）以及在线书籍的极佳来源，内容全部关于 Linux。

- http://www.minix.org/—非官方 minix 网站。它包含关于 minix 的信息链接列表以及实际主页的链接。虽然 minix 仍然受版权保护，但所有者已授予每个人无限的权利。亲自看看用于开发 Linux 的操作系统吧。

- http://jungle.dit.upm.es/~jmseayas/linux/kernel/hackers-docs.html—一个包含 Linux 内核文档、书籍、黑客技术手册以及其他有助于初涉和有经验的 Linux 内核及内核模块开发者的有用信息的网页。如果你安装了 Fedora 内核源代码，在这个列表中也会发现在 `/usr/src/kernels/linux-2.6/Documentation/kernel-docs.txt` 文件中。

## 第七部分

## 附录

- 附录 A Red Hat 和 Fedora 的历史 813

- 附录 B 安装资源 821

- 附录 C Fedora 和 Linux 互联网资源 847

### 附录 A

#### Red Hat 和 Fedora 的历史

##### 本附录内容

- 什么是 Fedora？

- 用于商业的 Fedora

- 家庭中的 Fedora

- 64 位 Fedora

- PPC 平台上的 Fedora

- 多核机器上的 Fedora

本书的主要目的是为你提供关于让 Fedora 8 运行起来的实用建议，因此我们并没有花太多时间探讨 Fedora 的起源及其如何发展到今天的地位。本附录提供了能让你将 Fedora 置于背景中并理解 Fedora 8 背后历史的信息。

Fedora 代表了其赞助商 Red Hat 在业务方向上的一次进化。Red Hat 本身是世界上最大的商业 Linux 开发商，总部位于北卡罗来纳州罗利市。在近 10 年里，Red Hat 通过互联网免费提供其商业 Linux 发行版 Red Hat Linux 的副本，同时也向消费者和企业出售盒装副本。这一切在 2003 年 10 月发生了改变，当时 Red Hat 停止销售和商业版 Red Hat Linux 的免费分发。

自公司成立以来，Red Hat 随后将其在前一个商业发行版中所有关于开源软件的工作公开。这项工作将成为 Red Hat Linux 的一个新版本，随后与现有的 Fedora Linux 项目合并，并重生为 Fedora Core。Red Hat 现在将其重点努力放在基于 Linux 的企业和公司产品及服务上，但同样，它继续为其所有受开源许可证保护的产品提供源代码。

Red Hat 的企业版 Linux 是一系列旨在用于企业和大型机构迁移、部署和使用的软件产品。虽然由于所有 Linux 发行版都使用 Linux 内核，因此可以在底层被视为相同，但 Red Hat 特别注重创建、测试、销售和支持针对多种硬件和 CPU 架构进行优化的商业 Linux 发行版。这些高性能增强功能包括经过硬件调整的内核、故障转移和负载均衡集群，以及集成的 Java 支持——这对于关键任务应用程序和生产环境至关重要。

### 关于 Red Hat

Red Hat 是世界上领先的开源开发机构之一，并将其几乎所有的开发努力回馈给 Linux 开发社区。

该公司参与了众多开源和 GNU GPL 项目，例如 Apache Web 服务器、glibc 软件库、GNU 网络对象模型环境（GNOME）、各种 GNU 软件工具和软件包、Linux 内核和设备驱动程序、PostgreSQL 数据库系统以及 Red Hat 软件包管理器（RPM）。

Red Hat 还通过提供 FTP 服务和 Web 托管支持许多其他项目，并且是积极推广和使用开源业务发展模式的少数公司之一。这意味着，虽然其许多产品是免费的，但收入来源来自衍生和相关技术及服务。

Linux 成功的一个可能原因是“最佳黑客获胜”。换句话说，工作良好、满足关键需求、易于以源代码形式获得，并在免费软件许可证（如 GNU GPL）下分发的软件，将迅速传播并得到广泛使用。Linux 在全球范围内受欢迎程度的增长和广泛采用证明了 Linux 的质量、许可证和需求的结合。

UNIX 在 20 世纪 70 年代初分发后也经历了类似的快速采用，并在多个方面满足了用户需求。然而，其许可证具有限制性，给某些开源社区（如教育界）带来了很多痛苦，并且至今仍不断引发问题。

就在不久以前，任何涉及大型企业、政府（无论哪个级别）或学术界使用 Linux 的新重大项目都会成为大新闻。如今，Linux 越来越多地被 IS/IT 战略家用于计算解决方案。Linux 和相关开源软件在互联网上占据主导地位。它是传统服务器操作的首选宿主平台。Linux 正准备接管桌面市场，仅次于一家垄断性的软件实体，占据第二位。

> **注意**
>
> Linux 项目、努力和伙伴关系的名单就像软件行业的名人录：Amazon、Ameritrade、Borland、Computer Associates、Dell、Hewlett-Packard、IBM、Oracle 和 SAP 只是使用 Linux 的一些企业级参与者。Linux 也是一个关键成分，并且占各大供应商（如 IBM、Hewlett-Packard 和 Dell）服务器硬件销售额中不断增长的比例。

### 什么是 Fedora？

Fedora 是 Red Hat Linux 的继承者，包含许多先前 Red Hat Linux 发行版中附带的特性和软件工具，以及许多增强功能。在过去十年中，Red Hat Linux 在 Linux 世界孕育了许多模仿者，其中许多模仿者已开发出可信的产品和发行版。感谢获取 Fedora 的不同方式，你不再需要担心下载多张 CD。随本书附带的光盘中有一张 DVD，其中包含 3GB 随时等待安装到你硬盘上的软件包。或者，如果你想要一个可用但轻便的安装，你可以选择带有 Gnome 界面的 Live CD 或带有 KDE 界面的 KDE Live CD（颇具讽刺意味的是）。Fedora 中包含超过 5,000 个独立的软件包。该发行版由 Linux 内核、安装实用程序、数千页文档、数千种字体、全面的图形网络界面以及数千个单独的命令和客户端组成。

Fedora 提供一个基础或核心框架操作系统和桌面，完全由免费软件组成。Fedora 包含 Nodoka 桌面主题，并在两个主要可用的图形桌面 Gnome 和 KDE 之间具有改进的一致性。

你可以预期 Fedora 将支持大量的 Linux 软件，事实上，除了 Fedora 发布版本之外，还可通过第三方存储库获得大量软件包库。这意味着你的第一张 Fedora CD-ROM 或 DVD 只是大量 Linux 软件收藏的开始！

Fedora 提供最新版本的 X Window System 及其服务器 X11R7，该版本拥有改进的集成字体处理功能。Linux 桌面从未看起来更好过，当你浏览网页、使用 Fedora 附带的十几个文字处理器和文本编辑器之一，或在终端窗口中查看命令行文本时，你会注意到这种差异。

根据 Fedora 项目，Fedora 计划每年升级两到三次。然而，实际上，发行版的开发工作从未停止，因为开源开发者与 Red Hat 工程师一起，通过软件包升级、安全更新和错误修复，在 Red Hat 的企业版 Linux 和 Fedora 之间进行“异花授粉”。Fedora 的免费在线升级系统可通过互联网访问。

Red Hat 为企业版 Linux 遵循大约 18 个月的发布周期。这个周期是必需的，以便为第三方应用程序开发者提供测试、部署和推广产品的时间。过去，Red Hat 曾对消费者版本的 Red Hat Linux 使用 6 个月的发布计划，开发周期为 3 到 4 个月的 beta 测试周期。Fedora 将拥有类似的计划；Fedora 项目声明其打算“每年大约两次发布基于时间表的 Fedora 版本”。

### 发行版本与内核编号方案

Linux 内核、内核开发以及 Fedora 内核版本有一套特定的编号系统。请注意，这些编号与您 Fedora Linux 发行版的版本号无关。Fedora 发行版版本号由 Fedora 项目分配，而大部分 Linux 内核版本号则由 Linus Torvalds 及其众多内核开发人员分配。
