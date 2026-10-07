

所显示的项目是网络参数，实际上调整这些值超出了本书的讨论范围。然而，如果我们想更改某个值，可以使用 `-w` 命令：

```bash
# sysctl -w net.ipv4.tcp_retries = 20
```

这会增加该特定内核参数的值。

> 注意
> Red Hat 在 `redhat-config-proc` 中为 `sysctl` 命令提供了一个图形界面。这是一个测试版本的应用程序，必须从命令行启动。该界面本身平平无奇，它没有提供操作所有可能值的方法，但为内核变量的地址提供了非常有用的帮助。

如果你发现某个设置很有用，可以将其输入 `/etc/sysctl.conf` 文件。格式如下，与之前的示例相同：

```
net.ipv4.tcp_retries = 20
```

对于内核黑客来说，比普通用户更有趣的是，`sysctl` 是一个极其强大的工具，并且一直在持续开发和编写文档。

- 相关的 Red Hat 和 Linux 命令
  在 Red Hat Linux 中管理内核及其模块时，你将使用以下命令：
  - gcc—GNU 编译器系统
  - make—GNU 项目和文件管理命令
  - mkbootdisk—Red Hat 的启动盘工具
  - sysctl—运行时操作内核变量的接口
  - mknitrd—为启动加载创建 RAM 磁盘系统

# 参考文献

http://www.kernel.org/—内核存档。Linux 内核所有开发讨论的源头。

http://kt.zork.net/kernel-traffic/—Linux 内核流量。每周生成的 Linux 内核邮件列表的汇编版本和评论。

http://www.gnu.org/—自由软件基金会。整个内核编译过程中使用的手册和软件程序的源处。`make` 和 `gcc` 等工具在这里有它们的官方文档。

http://slashdot.org/article.pl?sid=01/08/22/14532288&mode=thread—著名的 Alan Cox AC 补丁（补丁以他的名字命名）。

http://www.tld.org/LDP/tlk/—Linux 内核。关于 2.2 Linux 内核的在线书籍，描述了内核的内部结构。

http://www.tld.org/HOWTO/KernelAnalysis-HOWTO.html—KernelAnalysis-HOWTO。描述了内核的神秘本质。

http://www.tld.org/HOWTO/Module-HOWTO/index.html—内核模块 HOWTO。包含了关于未解析符号的良好讨论。

http://www.tld.org/—Linux 文档项目。所有 Linux 文档的圣地。关于 Linux 的操作指南、常见问题解答（FAQs）以及在线书籍的优秀来源。

http://www.minix.org—minix 的非官方网站。它包含了指向 minix 信息的链接以及指向实际主页的链接。虽然 minix 仍受版权保护，但所有者已向所有人授予无限权利。请亲自查看用于开发 Linux 的操作系统。

http://ftp.linux.org.uk/pub/linux/links/~ 嵌入式 Linux 内核子集的首页；其目标是在处理器和内存有限的机器上运行 Linux 子集。它似乎不再处于活跃开发状态。

http://jungla.dit.upm.es/~jmseys/linux/kernel/hackers-docs.html—一个网页，包含指向 Linux 内核文档、书籍、黑客专著以及其他对初学者和丰富的 Linux 内核及内核模块开发者有用信息的链接。如果你安装了 Red Hat Linux 内源码，此列表位于 `/usr/src/linux-2.4/Documentation/kernel-docs.txt` 文件中。

# 第 25 章

# 办公生产力应用

# 本章内容

- Red Hat Linux 办公套件
- PDA 连接
- Red Hat Linux 扫描仪应用程序
- Web 设计工具
- 传真客户端软件
- Red Hat Linux 包含的其他办公和生产力工具
- 为 Microsoft Windows 编写的生产力应用
- 参考文献

今天的现代企业开始学习丰富的 Red Hat Linux 用户多年来一直知道的事情：使用 Linux 和免费生产力软件具有巨大的成本效益。脱离软件许可和升级的“跑步机”将有助于增加底线。本章提供了有关 Red Hat Linux 包含和可用的流行办公软件的一些细节。尽管少数行业专家持反对意见，但 Red Hat Linux 可用于支持商业环境下的桌面操作。通过仔细选择和安装特定的生产力软件软件包，Red Hat Linux 可以获得大量可用、可靠且免费的软件。

生产力客户端包括免费的办公套件和工具，可用于创建文档以及调度、组织和计算。

在本章中，我们将检查 Red Hat 提供的默认办公生产力应用。你将学习到 Red Hat Linux 提供的替代应用程序，以及一些你可以安装的应用程序。本章描述了如何安装、配置和启动这些应用程序；提供有关使用这些应用程序的信息仅是为了让你了解与使用特定应用程序相关的特殊问题。

> 当选择并非良策时
> 与 Mac 和 Windows 用户通常只提供一个版本的生产力应用（以及一个桌面环境）不同，Linux 用户在应用程序和桌面环境方面都有许多选择。传统上，主菜单为你提供了所有的应用程序。从许多不同的桌面环境（例如几十种文本编辑器）中进行选择的必要性，对于新的 Linux 用户来说是一项艰巨的任务，这也是许多企业用户投诉的源头。此外，Red Hat 必须为其包含在发行版中的每个应用程序提供支持。

从 8.0 版本开始，Red Hat 通过限制主菜单中提供的可用选择和限制可用应用程序的总数来解决这些疑虑。现在，主菜单中任何类别的应用程序只呈现一个：只有一个处理器，只有一个地址簿，以此此类推。在进行限制的的同时，Red Hat 选择了它认为最好的可用生产力应用，选择了一个基于 OpenOffice.org 套件的非官方“Red Hat 套件”。因此，Red Hat 添加了来自 GNOME 办公应用和 KDE 桌面的应用程序。

Red Hat 选择的办公组件可以在主菜单的“附件 (Accessories)”、“图形 (Graphics)”、“办公 (Office)”和“声音与视频 (Sound & Video)”菜单可用。所有其他应用程序都在“额外 (Extras)”菜单中，该菜单包含了主菜单的副本。额外菜单包含了 Red Hat 提供的未进入默认选择的所有应用程序的菜单项。对于企业 IT 经理和 Red Hat 来说，对配置文件进行简单的编辑即可从视图中移除“额外”，并简化必须提供的支持。

对于个人用户来说，Red Hat 的方法导致了一个问题，因为 Red Hat 将应用程序散落在整个菜单树中。糟糕的是，Red Hat 选择的默认桌面环境（GNOME 2.0）没有提供菜单编辑器。显然，Red Hat 还没有完成它的菜单设计，未来可能会发生变化。随着你对 Red Hat 安装系统的更新，你会看到这些变化。

# Red Hat Linux 办公套件

大多数办公套件包括生产力应用，如文字处理器、电子表格程序、计算器、数据库程序和绘图工具。许多办公套件是为 Linux 创建的。其中许多是免费的，但也有许多商业产品可供选择。Red Hat 没有开发自己的办公套件，但它提供了一组默认的办公应用程序，这些应用旨在广泛适用并提供通用功能。Red Hat 核心办公套件、OpenOffice.org 和 GNOME 办公套件包含在书中（原文注：Red Hat 核心办公套件、OpenOffice.org 和 GNOME 办公套件包含在本书的光盘中）。在接下来的章节中，你将了解这些生产力软件包中包含的应用程序，并获得一些安装和配置它们的提示。你还将了解 KDE 办公套件（KOffice）以及其他可以免费下载或购买用于 Red Hat Linux 的办公套件。

# 使用 OpenOffice.org

如果你的主要需求是与专有的 Microsoft 文件格式兼容，OpenOffice.org 应用程序套件是满足你需求的首选。

