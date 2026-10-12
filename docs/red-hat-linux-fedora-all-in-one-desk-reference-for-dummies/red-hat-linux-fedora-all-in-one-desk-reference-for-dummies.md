# 红帽 Linux Fedora 一站式桌面参考傻瓜书



























![](img/a7eec43a54473e95dc5ea333fecf1bd7_5_0.png)


## 关于作者

**Naba Barkakati** 是一名电气工程师，也是成功的计算机书籍作者，拥有从 MS-DOS 和 Windows 到 UNIX 和 Linux 等各种系统的经验。他在 1984 年获得马里兰大学学院公园分校电气工程博士学位后购买了第一台个人电脑——IBM PC-AT。在从事全职工程职业的同时，Naba 梦想为新兴的 PC 软件市场编写软件。命运使然，他没有像微软那样建立软件帝国，而是撰写了成功的计算机书籍。目前，Naba 是美国政府问责办公室技术与工程中心的高级技术专家。

过去 15 年里，Naba 写了 25 多本计算机书籍，涵盖从使用 C++ 进行 Windows 编程到 Linux 等多个主题。他撰写了多本畅销书，如 *The Waite Group’s Turbo C++ Bible*、*Object-Oriented Programming in C++*、*X Window System Programming*、*Visual C++ Developer’s Guide*、*Borland C++ 4 Developer’s Guide* 和 *Linux Secrets*。他的书籍已被翻译成多种语言，包括西班牙语、法语、波兰语、希腊语、意大利语、中文、日语和韩语。Naba 最近的书籍是 ***Red Hat Linux 9 Secrets***，同样由 Wiley Publishing, Inc. 出版。

Naba 与妻子 Leha 以及女儿 Ivy、Emily 和 Ashley 一起居住在马里兰州的北波托马克。

## 致谢

我谨将本书献给我的妻子 Leha，以及女儿 Ivy、Emily 和 Ashley。

## 作者致谢

我非常感谢 Terri Varveris 让我开始撰写这本书——一套关于 Red Hat Linux 各方面的九本快速参考指南。作为项目编辑，Nicole Sholly 指导我完成了手稿提交流程并保持了工作的推进。我感谢 Terri 和 Nicole 在此项目中给予我的指导和支持。

我谨感谢 Jason Luster 审阅手稿的技术准确性，并提供了许多改进本书内容的宝贵建议。

感谢 Wiley Publishing 的所有人将我的原始手稿改造成这本编辑精良、包装精美的书籍。

当然，如果没有 Linux，就不会有这本书的理由。对于这一点，我们要感谢 Linus Torvalds 和世界各地的 Linux 开发者群体。感谢 Red Hat 提供了 Red Hat Linux 的测试版副本以及随本书附带的出版商版 CD。

最后，也是始终如此，我最深切的感谢献给我的妻子 Leha 和我们的女儿 Ivy、Emily 和 Ashley——是她们的爱和支持让我坚持下去。感谢你们一直陪伴在我身边！

## 出版社致谢

我们为这本书感到自豪；请通过位于 www.dummies.com/register/ 的在线注册表发送您的评论。

以下是有助于将本书推向市场的一些人员：

### 收购、编辑和媒体开发

- **副项目编辑：** Nicole Sholly
- **收购编辑：** Terri Varveris
- **高级校对编辑：** Barry Childs-Helton
- **技术编辑：** Jason Luster
- **编辑经理：** Kevin Kirschner
- **许可编辑：** Laura Moss
- **媒体开发专家：** Angela Denny
- **媒体开发经理：** Laura VanWinkle
- **媒体开发主管：** Richard Graves
- **编辑助理：** Amanda Foxworth, Virginia Sanders
- **漫画：** Rich Tennant
  (www.the5thwave.com)

### 生产

- **项目协调员：** Regnia Snyder
- **版式和图形：** Seth Conley, Joyce Haughey, Stephanie D. Jumper, Jacque Schneider, Julie Trippetti, Shae Wilson, Melanie Wolven
- **校对员：** John Greenough, Andy Hollandbeck, Susan Moritz, Linda Quigley
- **索引：** Infobox Indexing Services Inc.

### 技术 Dummies 出版和编辑

- **Richard Swadley,** 副总裁兼执行集团出版人
- **Andy Cummings,** 副总裁兼出版人
- **Mary C. Corder,** 编辑总监

### 消费 Dummies 出版

- **Diane Graves Steele,** 副总裁兼出版人
- **Joyce Pepple,** 收购总监

### 排版服务

- **Gerry Fahey,** 生产服务副总裁
- **Debbie Stalley,** 排版服务总监











































## xiv
## Red Hat Linux Fedora 一站式参考手册 傻瓜版






















xix













633



641



669












## 引言

Red Hat 持续改进其 Linux 版本。最近发布的 Red Hat Linux 包含许多新的系统组件，包括 Linux 2.4.22 内核、XFree86 4.3.0、GNOME 2.4、KDE 3.1、GCC 3.3 编译器以及 glibc 2.3.2 系统库。此版本支持许多新功能，例如高级配置和电源接口 (ACPI)、蓝牙无线连接，以及在用户友好的屏幕中显示系统启动消息的图形化启动屏幕。

Red Hat Linux 还包含 OpenOffice.org 办公套件。更棒的是，Red Hat Linux 附带了一个图形化安装程序，使安装变得简单！

最后，从本版本开始，Red Hat Linux *产品* 正在成为 *Fedora 项目*——一个协作开发项目，对所有具备技能和兴趣参与并贡献的人开放。在这种新的开发模式下，原开发人员（而不是 Red Hat 开发人员）将控制构成 Red Hat Linux 的各个软件包。

> 注：在印刷时，Red Hat 已将其 Linux 产品更名为 Fedora 项目。在本书的整个过程中，我将该产品称为 Red Hat Linux 或简称为 Red Hat。您可能会在新闻、网络以及其他地方看到该产品被称为 Fedora 项目，但请放心，如本书所用，不同的术语指的是同一产品。

## 关于 Red Hat Linux Fedora 一书通

Red Hat Linux Fedora All-in-One Desk Reference For Dummies 遵循 All-in-One Desk Reference 的成功模式，在一本书中为您提供九种不同的快速参考指南。合在一起，这九本迷你书提供了有关安装、配置和使用 Red Hat Linux 的详细信息。

您最喜欢这本书的地方在于，您不必按章节顺序逐章阅读，甚至不必按章节内的部分阅读。您可以几乎直接翻到想要的主题，快速获得有关 Red Hat Linux 的紧迫问题的答案，无论是关于使用 OpenOffice.org 文字处理器还是设置 Apache Web 服务器。

## 2 本书使用的约定

以下是您可以使用本书完成的一些事情：

- 从随书附带的 DVD 安装和配置 Red Hat Linux。
- 通过 DSL 或有线调制解调器将 Red Hat Linux PC 连接到 Internet。
- 使用 PPP 设置拨号网络。
- 获取有关 Red Hat Linux 特定用途的提示、技术和快捷方式，例如
  - 设置和使用 Internet 服务，如 Web、Mail、News、FTP、NFS、NIS 和 DNS
  - 使用 Samba 设置 Windows 服务器
  - 使用 Red Hat Linux 命令
  - 在 Red Hat Linux 上使用 Perl、shell 和 C 编程
  - 使用随 Red Hat Linux 提供的 OpenOffice.org 办公套件和其他应用程序
  - 了解系统和网络安全的基础知识
  - 执行系统管理任务

### 本书使用的约定

我在这本书中使用简单的记号风格。所有列表、文件名、函数名、变量名和关键字都以等宽字体排版，便于阅读。我对新术语和概念的首次出现使用斜体，并在此处提供定义。命令的输出跟在键入的命令之后，输出以等宽字体显示。

### 您不必阅读的内容

每本迷你参考书都聚焦于特定的任务领域，例如使用 Internet 或运行 Internet 服务器，然后提供有关如何执行一系列相关任务的实践说明。您可以直接跳转到某个部分并阅读有关特定任务的内容。您无需阅读与您的问题相关的几段文字或步骤列表以外的任何内容。使用目录或索引找到与您的问题相关的页面。

您可以安全地忽略“Technical Stuff”图标旁边的文字以及侧边栏。



3

## 你是谁？

我假设你对个人电脑有一定熟悉——你知道如何开关机，并且已经在 Windows 上尝试过一些操作。考虑到大多数新电脑都预装了 Windows，这应该是一个安全的假设，对吧？

当谈到在你的电脑上安装 Red Hat Linux 时，如果你想保留 Windows 2000 或 Windows XP 安装完好无损，我假设你不会介意投资一个好的磁盘分区工具，例如 *PowerQuest's PartitionMagic*，可在 www.powerquest.com/partitionmagic 获取（不，我与 PowerQuest 没有任何关系）。

我还假设你愿意接受在尝试安装 Red Hat Linux 时某些东西可能无法正常工作的风险。这可能会发生在你拥有一些不常见类型的硬件时。如果你担心损坏系统，可以尝试找一台稍旧的备用 Pentium 电脑作为牺牲品，然后在那台电脑上安装 Red Hat Linux。

## 本书的组织结构

*Red Hat Linux Fedora All-in-One Desk Reference For Dummies* 有九个迷你书，每本都专注于一组相关的主题。如果你正在寻找特定主题的信息，请查看书脊上的书名或查阅目录。

这本桌面参考书首先用一本迷你书解释 Red Hat Linux 的基础知识并指导你完成安装过程（这是本书的一个独特之处，因为你通常不会购买预装 Red Hat Linux 的电脑）。第二本迷你书作为 Red Hat Linux 的用户指南——它专注于探索 Red Hat Linux 工作站的各个方面，包括 GNOME 和 KDE 图形用户界面以及随 Red Hat Linux 捆绑的许多应用程序。第三本迷你书是 OpenOffice.org 办公应用程序的用户指南。第四本迷你书涵盖网络，而第五本书则深入介绍互联网的使用。第六本书介绍系统管理。第七本迷你书转向 Red Hat Linux 系统及其相关网络的重要安全主题。第八本书教授如何运行各种互联网服务器，从邮件到 Web 服务器。第九本也是最后一本迷你书向你介绍编程。

以下是九本书的快速概述及其包含内容：

- **第 1 书：Fedora 基础：** Red Hat Linux 是什么？安装、配置和故障排除 Red Hat Linux。试用 Red Hat Linux。

## 4  本书的组织结构

- **第 II 书：工作站和应用程序：** 探索 GNOME 和 KDE。学习如何使用 shell（什么是 shell 呢？）。学习如何在 Red Hat Linux 文件系统中导航。探索诸如多媒体软件以及文本编辑器（vi 和 Emacs）等应用程序。
- **第 III 书：OpenOffice.org：** 使用 OpenOffice.org Writer 进行写作。使用 OpenOffice.org Calc 准备电子表格。使用 OpenOffice.org Impress 制作演示文稿。使用 OpenOffice.org Draw 准备绘图。
- **第 IV 书：网络：** 通过拨号连接或 DSL 或有线调制解调器等高速常在线连接将 Red Hat Linux PC 连接到互联网。配置和管理 TCP/IP 网络，包括无线以太网。
- **第 V 书：互联网：** 使用各种互联网服务，例如电子邮件、网页浏览和阅读新闻组。使用 FTP 传输文件。
- **第 VI 书：管理：** 学习执行基本系统管理。管理用户账户和文件系统。安装应用程序。处理设备和打印机。使用 USB 设备。升级和定制 Linux 内核。
- **第 VII 书：安全：** 了解网络和主机安全。学习保护主机和网络的技术。执行安全审计。
- **第 VIII 书：互联网服务器：** 管理互联网服务。配置 Apache Web 服务器。设置 FTP 服务器（包括匿名 FTP）。配置邮件和新闻服务器。提供 DNS 和 NIS。使用 NFS 进行文件共享。使用 Samba 设置 Windows 服务器。
- **第 IX 书：编程：** 学习编程基础。探索 Red Hat Linux 中的软件开发工具。编写 shell 脚本。学习 C 和 Perl 编程。

附录：**关于 DVD：** 总结本书随附 DVD 的内容。

## 侧边栏

我在全书中使用侧边栏来突出有趣但非关键的信息。侧边栏解释你可能尚未遇到过的概念，或提供相关主题的一些见解。如果你很赶时间，可以安全地跳过侧边栏。

## DVD 上有什么？

DVD 包含来自 Red Hat, Inc. 的 Red Hat Linux。你可以根据随软件提供的许可协议使用 DVD。要了解有关 DVD 内容的更多信息，请参阅附录。

## 本书中使用的图标

遵循 *All-in-One Desk Reference For Dummies* 系列的悠久传统，我使用图标帮助你快速找到有用的信息。图标包括以下内容：

![](img/a7eec43a54473e95dc5ea333fecf1bd7_32_0.png)

记住图标标记一个一般的有趣事实——是我认为你会想知道并记住的东西。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_32_1.png)

提示图标标记你可以做的事情来让工作更轻松。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_32_2.png)

警告图标突出潜在的陷阱。有了这个图标，我在告诉你：“当心！这可能会伤害你的系统！”

![](img/a7eec43a54473e95dc5ea333fecf1bd7_32_3.png)

技术资料图标标记可能对高级用户感兴趣的技术信息（或那些渴望成为高级用户的我们）。

## 从这里开始

是时候开始你的 Red Hat Linux 之旅了。取出 DVD 并安装 Red Hat Linux。然后，翻到相关章节，让乐趣开始。使用目录和索引来确定你想去哪里。在你意识到之前，你将成为 Red Hat Linux 的专家！

如果你想参与 Red Hat Linux 项目，请访问项目的网站 `rhl.redhat.com` 了解更多信息。

我希望你能像我写这本书一样喜欢查阅它！

## 第 I 书

## Fedora 基础

## 第五波

作者 Rich Tennant

![](img/a7eec43a54473e95dc5ea333fecf1bd7_34_0.png)

> “我不在乎你在欧洲的电子邮件朋友说什么，你不能用波罗尼亚三明治配一杯基安蒂酒。”

## 一目了然的内容

- 第 1 章：介绍 Red Hat Linux........................................................................................................9
- 第 2 章：安装 Red Hat Linux........................................................................................................................27
- 第 3 章：故障排除和配置 Red Hat Linux ................................................................................55
- 第 4 章：试用 Red Hat Linux ..................................................................................................................73

### 第 1 章：介绍 Red Hat Linux

## 本章内容

- 解释 Red Hat Linux 是什么
- 概述 Red Hat Linux 包含的内容
- 发现 Red Hat Linux 如何帮助你管理
- 开始使用

我敢打赌你听说过 Linux，而且你也可能知道 Red Hat 这个名字。如果你想知道 Red Hat Linux 究竟是什么以及它能帮助你做什么，本章就是全部关于回答这些问题的。这里我对 Red Hat Linux 做一个宽泛的概述，并告诉你如何立即开始使用它。我还简要提及 Fedora 项目。

顺便说一下，本书涵盖适用于 Intel 80x86 和 Pentium 处理器（基本上任何可以运行任何 Windows 版本的 PC）的 Red Hat Linux Fedora。

## Red Hat Linux 是什么？

试图描述 Red Hat Linux 有点像六个盲人试图描述大象的故事。你知道那个故事——一个盲人触摸大象的侧面并说大象像一堵墙，另一个点击象牙并得出大象像矛的结论，等等。沿着这条思路，Red Hat Linux 似乎是许多不同的东西，这取决于你的体验。你可以把它看作图形用户界面或只是运行你的电子邮件程序的 PC，但从根本上说，它是一个操作系统。以下各节解释我的意思。

## 操作系统和 Linux

你知道你的 PC 是一堆硬件——你可以触摸的东西，比如系统箱、显示器、键盘和鼠标。系统箱包含最重要的硬件——*中央处理器*（CPU），运行 *软件*（任何告诉计算机如何执行你命令的程序）的微芯片——你实际上 *不能* 触摸。在典型的 Pentium 4 PC 中，Pentium 4 微处理器就是 CPU。其他重要硬件在


## 10 什么是 Red Hat Linux？

系统盒包含内存（RAM 芯片）和硬盘——而有一个程序必须运行所有这些东西并让它们和谐工作：操作系统。

*操作系统* 是管理所有硬件并按你的指令运行其他软件的软件。你，用户，通过点击菜单和图标或输入一些晦涩的文本来提供这些指令。Linux 是一个操作系统——UNIX、Windows 98、Windows 2000 和 Windows XP 也是如此。Linux 操作系统以 UNIX 为模型；在最基本、无花哨的形式下，它也被称为 *Linux 内核*。

操作系统赋予计算机——任何计算机——其个性。例如，你可以在 PC 上运行 Windows 98 或 Windows XP——并且在同一台 PC 上，你可以 *也* 安装并运行 Linux。这意味着，根据安装并运行的操作系统，同一台 PC 可以是 Windows 98、Windows XP 或 Linux 系统。

操作系统的首要任务是从硬盘（或其他永久存储）中加载软件（计算机程序）到内存中，并让 CPU 运行这些程序。你用计算机所做的一切都是因为操作系统的存在；所以如果操作系统出了问题，整个系统就会冻结。你知道当你最喜欢的操作系统——也许就是随 PC 提供的那个——在你刚刚写完那封长邮件准备点击发送按钮时突然罢工时有多令人抓狂。你尝试三指连击（Ctrl+Alt+Del），但什么也没发生。然后就该按重置按钮了（前提是你的电脑制造商足够明智地装了它）。幸运的是，这种情况在 Linux 上几乎从不发生——它以非常可靠的操作系统著称。

### Linux 真的能在任何计算机上运行吗？

Linux 运行在许多不同类型的计算机系统上——而且似乎能够运行在几乎任何类型的计算机上。Linus Torvalds 和其他程序员最初为 Intel 80x86 系列处理器开发了 Linux。如今，Linux 也可用于基于其他处理器的系统——例如采用英特尔新的 64 位 IA-64 架构（称为 Itanium 处理器）的系统；Motorola 68000 系列；Alpha AXP；Sun SPARC 和 UltraSPARC；Hewlett-Packard 的 HP PA-RISC；PowerPC 和 PowerPC64 处理器；以及 MIPS R4000 和 R5000。最近，IBM 还为其 S/390 大型机发布了自己的 Linux 版本。本书涵盖面向 Intel 80x86 和 Pentium 处理器的 Red Hat Linux（它们共有的基本物理结构称为 *IA-32 架构*）。

### 什么是 Red Hat Linux？

![](img/a7eec43a54473e95dc5ea333fecf1bd7_38_0.png)

在技术术语里，Linux 是一个多用户、多任务操作系统。这仅仅意味着 Linux 允许多个用户登录，并且 Linux 可以同时运行多个程序。如今几乎所有操作系统都是多用户和多任务的，但在 Linux 于 1994 年首次推出时，多用户和多任务是很大的卖点。

### Linux 发行版

Red Hat Linux 是一个特定的 Linux 发行版——本质上是一个功能包。Red Hat Linux 由 Linux 内核（操作系统）和一组应用程序组成，并配有一个易于使用的安装程序。

有很多 Linux 发行版，每个都包含标准的 Linux 操作系统：

- The XFree86 X Window System: This is the graphical user interface.
- One or more graphical desktops: Among the most popular are GNOME and KDE.
- A selection of applications: Linux programs come in the form of ready-to-run software, but the source code (the commands we humans use to tell the computer what to do, but you don’t need the source code to run the operating system or any applications) is included, as is its documentation.

当前 Linux 发行版包含海量的软件——多到需要多张 CD-ROM 或一张 DVD（本书就包含）。

像许多其他 Linux 发行版一样，Red Hat Linux 是一种商业产品，你可以在电脑商店和书店购买。如果你听说过开源和 GNU（GNU’s Not UNIX）许可证，你可能会认为没人能为了盈利而出售 Linux。幸运的是，对于 Red Hat 这样的公司，GNU 许可证——也称为 GNU 通用公共许可证（GPL）——确实允许商业盈利性分发，但要求软件以源代码形式分发，并规定任何人都可以将软件以源代码形式复制并分发给他人。这意味着我的出版商可以将 Red Hat Linux DVD 与本书一起提供，而你可以随意复制 DVD 任意多份。

### 理解版本号

Linux 内核和 Red Hat Linux 各自都有自己的版本号，更不用说随 Red Hat Linux 提供的众多其他软件程序（如 GNOME 和 KDE）。Linux 内核和 Red Hat Linux 的版本号无关，但各自都有特定意义。

### Linux 内核版本号

在 Linux 内核 1.0 版本于 1994 年 3 月 14 日发布后，松散的 Linux 开发社区采用了一种版本号方案。版本号如 1.X.Y 和 2.X.Y，其中 X 为偶数，被认为是稳定版本。最后一个数字 Y 是补丁级别，随着问题的修复而递增。例如，2.4.21 是 Linux 内核的一个典型稳定版本。请注意，这些版本号的形式为三个用点分隔的整数——Major.Minor.Patch——其中 Major 和 Minor 是表示主次版本号的数字，Patch 是表示补丁级别的另一个数字。

形式为 2.X.Y 且 X 为奇数的版本号是仅供开发者的测试版；它们可能不稳定，因此你不应将其用于日常使用。例如，当你看到 Linux 内核的 2.5.75 版本时，注意其中的 5——这告诉你它是一个测试版。开发者会在这些奇数版本的 Linux 中添加新功能。

你可以在 www.kernel.org 在线了解 Linux 内核的最新版本。

### Red Hat Linux 版本号

Red Hat 分配 Red Hat Linux 的版本号，例如 7.3 或 8.0。它们的形式为 X.Y，其中 X 是主版本号，Y 是次版本号。如今如果次版本号为零，则直接省略——如 Red Hat Linux 9。与 Linux 内核版本号不同，奇偶次版本号没有特殊含义。每个版本的 Red Hat Linux 都包含特定版本的 Linux 内核和其他主要组件，如 GNOME、KDE 和各种应用程序。

Red Hat 会定期发布新版本的 Red Hat Linux。例如，Red Hat Linux 7.0 于 2000 年 9 月发布，7.3 于 2002 年 5 月发布，8.0 于 2002 年 9 月发布，而 Red Hat Linux 9 于 2003 年 3 月 31 日发布。通常，每个新的主要版本的 Red Hat Linux 都提供重要的新功能。

### 过渡到 Fedora 项目

2003 年 9 月下旬，Red Hat 宣布了 Fedora 项目——一个由 Red Hat 赞助的开源项目，开发者社区可以参与并继续发展原先的 Red Hat Linux 产品。新产品名为 Fedora Core，预计每四到六个月发布一次 Fedora Core。Red Hat 将继续参与 Fedora 项目并帮助准备 Fedora Core 的发布，但所有工作将在开源社区的参与下按照公开的发布计划进行。正如你所预期的那样，Fedora Core 将免费提供，就像 Red Hat Linux 以前一样，你可以期待像本书这样的书籍随附 DVD 或 CD 上的 Fedora Core。

### 什么是 GNU 项目？

GNU 是一个递归缩写，代表 GNU’s Not UNIX。GNU 项目由 Richard Stallman 于 1984 年发起，旨在开发一个完整的类 UNIX 操作系统。GNU 项目开发了构建完整操作系统所需的一切，除了操作系统内核。所有 GNU 软件都在 GNU 通用公共许可证（GPL）下分发。GPL 基本上要求软件以源代码形式分发，并规定任何用户都可以将软件以源代码形式复制、修改并分发给他人。用户可能需要为其个人副本支付费用。

自由软件基金会（FSF）是一个免税慈善机构，为 GNU 项目的工作筹集资金。要了解更多关于 GNU 项目的信息，请访问其主页 www.gnu.org。在那里你可以找到如何联系自由软件基金会以及如何帮助 GNU 项目的信息。

Red Hat 继续销售其商业 Linux 发行版——称为 Red Hat Enterprise Linux。Red Hat 预计首次出现在 Fedora Core 中的新技术和增强功能最终会进入 Red Hat Enterprise Linux。这样，Fedora 项目应作为未来 Linux 开发的孵化器和试验场。

要了解更多关于 Fedora 项目的信息，请访问 fedora.redhat.com。

### Red Hat Linux 包含的内容

Red Hat Linux 随带 Linux 内核和大量其他软件。这些软件包包括从图形桌面到 Internet 服务器以及创建新软件的编程工具。在本节中，我简要描述了一些随 Red Hat Linux 捆绑的主要软件包。没有这些捆绑软件，Red Hat Linux 不会像今天这样受欢迎。

### GNU 软件

我从 GNU 项目提供的软件集合开始。只有当你通过文本终端（或模拟它的图形窗口）使用 Red Hat Linux 系统时，你才会接触到这些 GNU 工具——这是一个基本的命令行界面，屏幕上几乎什么都没有，只有一个提示符供你输入命令。GNU 软件是 Red Hat Linux 的基本组成部分之一。

作为 Red Hat Linux 用户，你可能没有意识到 Red Hat Linux（以及事实上所有 Linux 发行版）在多大程度上依赖 GNU 软件。



在 Red Hat Linux 系统中执行的几乎所有任务都涉及一个或多个 GNU 软件包。例如，GNOME 图形用户界面（GUI）和命令解释器（即 Bash shell）都是 GNU 软件程序。顺便说一下，*shell* 是命令解释应用程序，它接受你输入的命令并据此运行程序。如果你重新编译内核或开发软件，你使用的是 GNU C 和 C++ 编译器（它是随 Red Hat Linux 提供的 GNU 软件的一部分）。如果你使用 ed 或 Emacs 编辑器编辑文本文件，你又在使用 GNU 软件包。列表不胜枚举。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_41_0.png)

表 1-1 列出了随 Red Hat Linux 提供的一些知名 GNU 软件包。我只展示此表是为了让你感受一下使用 GNU 软件可以做到的各种不同事情。根据你的兴趣，你可能永远不需要使用其中许多包，但了解它们存在以备不时之需是好的。

| Software Package | Description |
|---|---|
| Autoconf | 生成自动配置源代码包的 shell 脚本 |
| Automake | 生成用于 Autoconf 的 `Makefile.in` 文件 |
| Bash | Red Hat Linux 中的默认 shell——命令解释——程序 |
| Bc | 具有任意精度数字的交互式计算器 |
| Binutils | 一个包含多个用于处理二进制文件的实用程序的包：ar, as, gasp, gprof, ld, nm, objcopy, objdump, ranlib, readelf, size, strings, and strip |
| Coreutils | 一个将名为 Fileutils、Shellutils 和 Textutils 的三个独立包合并并实现诸如：chgrp, chmod, chown, cp, dd, df, dir, dircolors, du, install, ln, ls, mkdir, mknod, mktemp, mv, rm, rmdir, sync, touch, vdir, basename, chroot, date, dirname, echo, env, expr, factor, false, groups, hostname, id, login, logname, nice, nohup, pathchk, printenv, printf, pwd, seq, sleep, stty, su, tee, test, true, tty, uname, uptime, users, who, whoami, yes, cut, join, nl, split, tail, wc, and so on 之类的实用程序的包 |
| Cpio | 将文件归档复制到磁盘或文件系统的另一部分，或从磁盘或文件系统的另一部分复制文件归档。 |
| Diff | 比较文件，以多种不同格式显示逐行更改。 |
| Ed | 行式文本编辑器 |
| Emacs | 可扩展、可定制的全屏文本编辑器和计算环境 |
| Findutils | 一个包含 find、locate 和 xargs 实用程序的包 |
| Finger | 一种实用程序，旨在使 Internet 上的用户能够相互获取信息 |

## What Red Hat Linux Includes

![](img/a7eec43a54473e95dc5ea333fecf1bd7_42_0.png)

| Software Package | Description |
|---|---|
| Gawk | GNU 项目对 AWK 编程语言的实现 |
| GCC | C, C++, Objective C 和其他语言的编译器 |
| Gdb | C, C++ 和 Fortran 的源代码级调试器 |
| Gdbm | 传统 dbm 和 ndbm 数据库库的替代品 |
| Gettext | 一组实用程序，使软件维护人员能够国际化（即使软件的用户消息适用于英语、法语、西班牙语等不同语言）软件包的用户消息 |
| Ghostscript | Postscript 和便携式文档格式（PDF）语言的解释器 |
| Ghostview | 一个 X Window System 应用程序，使 Ghostscript 可从 GUI 访问，使用户能够在窗口中查看 Postscript 或 PDF 文件 |
| The GIMP | GNU 图像处理程序是一个类似 Adobe Photoshop 的图像处理程序 |
| GNOME | 为 Linux 用户可能执行的各种任务提供图形用户界面（GUI） |
| GNU C Library | 用于所有 Linux 程序 |
| Gnuchess | 一个下棋程序 |
| Gnumeric | 一个在 GNOME 中工作的图形电子表格（类似于 Microsoft Excel） |
| grep package | 包含用于查找匹配指定文本模式的行 的 grep、egrep 和 fgrep 命令 |
| Groff | 一个类似于 troff 的文档格式化系统 |
| GTK+ | X Window System 的 GUI 工具包（用于开发 GNOME 应用程序） |
| Gzip | 用于压缩和解压缩文件的 GNU 实用程序 |
| Indent | 通过以几种不同样式缩进格式化 C 源代码 |
| Less | 一个逐页显示程序，类似于 more，但具有额外功能 |
| Libpng | 用于便携式网络图形（PNG）格式图像文件的库 |
| m4 | 传统 UNIX 宏处理器的实现 |
| Make | 一个实用程序，用于确定大型软件包中哪些文件需要重新编译，并发出重新编译它们的命令 |
| Mtools | 一组程序，使用户能够读取、写入和操作 DOS 文件系统（通常是软盘）上的文件 |
| Ncurses | 用于在纯文本终端上显示和更新文本的包 |
| Patch | Larry Wall 程序的 GNU 版本，用于获取 diff 的输出并将这些差异应用到原始文件以生成修改后的版本 |
| RCS | 修订控制系统；用于软件项目中源文件的版本控制和管理 |
| Sed | ed 文本编辑器的流式版本 |
| Sharutils | 一个包含 `shar`（用于将多个文件制作为 shell 归档）和 `unshar`（用于解包这些 shell 归档）的包 |
| Tar | 一个磁带归档程序，包括多卷支持；归档稀疏文件、处理压缩和解压缩以及创建远程归档的能力；以及用于增量和完整备份的其他特殊功能 |
| Texinfo | 一组实用程序，生成印刷手册、纯 ASCII 文本和在线超文本文档（称为 Info），并使用户能够查看和阅读在线 Info 文档 |
| Time | 一个实用程序，报告进程使用的用户时间、系统时间和实际时间 |

## GUIs and applications

说实话 — 在终端上输入晦涩的 Linux 命令很无聊。对于我们这样的普通用户来说，通过 *图形用户界面（GUI，发音为“gooey”）* 使用系统要容易得多，它提供可点击的图片和可打开的窗口（小 *w*）。这就是 X Window System，或 X，发挥作用的地方。

X 有点像 Microsoft Windows，但 X 的底层工作原理与 Windows 完全不同。与 Windows 不同，X 提供了在屏幕上显示窗口的基本功能，但它不提供图形应用程序的特定外观或感觉。这种外观和感觉来自 GNOME 和 KDE 等 GUI，它们使用 X Window System。

Red Hat Linux 以 XFree86 的形式提供 X Window System — 这是为 80x86 系统实现的 X Window System。XFree86 可与当今 PC 上可用的各种视频卡配合使用。

至于 GUI，Red Hat Linux 包含两个强大的 GUI 桌面：KDE（K Desktop Environment）和 GNOME（GNU Object Model Environment）。如果在 PC 上同时安装了 GNOME 和 KDE，你可以选择默认的桌面 — 或在两者之间切换。KDE 和 GNOME 提供了类似于 Microsoft Windows 和 Macintosh OS 的桌面。GNOME 还附带 Nautilus 图形 shell，可轻松查找文件、运行应用程序并配置你的 Red Hat Linux 系统。有了 GNOME 或 KDE，你就可以开始使用 Red Hat Linux 工作站，而无需学习晦涩的 Linux 命令。然而，如果你确实需要直接使用这些命令，只需打开一个终端窗口并在提示符下输入即可。

## What Red Hat Linux Includes

Red Hat Linux 还附带许多图形应用程序。最值得注意的程序是 GIMP（GNU Image Manipulation Program，也称为“The Gimp”），一个用于处理照片和其他图像的程序。GIMP 的功能与 Adobe Photoshop 不相上下。

提供常见的生产力软件 — 如文字处理、电子表格和数据库应用程序 — 曾是 Linux 的薄弱环节。这种情况已经改变。Red Hat Linux 附带 OpenOffice.org 办公生产力应用程序。此外，你可能还想查看这些在 Linux 上广受欢迎的商业办公生产力应用程序，它们未包含在随附 DVD 上：

- *Applixware Office — 现在称为 Anyware Desktop for Linux — 是 Linux 生产力软件的一个很好的例子。你可以在 www.vistasource.com 找到它。*
- *来自 Sun Microsystems 的 StarOffice（www.sun.com/staroffice）是另一个广为人知的生产力软件包。*
- *来自 CodeWeavers 的 CrossOver Office（www.codeweavers.com/products/office/）使你能够在 Linux 中安装你的 Microsoft Office 应用程序（仅限 Office 97 或 Office 2000，而不是 Office XP）。*

正如你所见，Linux 上没有缺少与 Microsoft Office 兼容的办公应用程序。

## Networks

Red Hat Linux 附带了使用系统在网络中所需的一切，以便系统可以与其他系统交换数据。在网络中，交换数据的计算机必须遵循明确定义的规则或协议。网络协议是发送方和接收方就如何在网络上交换数据达成一致的方法。这种协议类似于你在聚会上与某人进行礼貌交谈时可能遵循的规则。你通常会先说你好，交换名字，然后轮流说话。网络协议的工作方式也差不多。两台计算机使用协议在网络上传输位和字节。

最知名和流行的网络协议之一是传输控制协议/互联网协议（*TCP/IP*）。TCP/IP 是互联网 — 现在遍及全球的“网络的网络” — 的首选协议。Red Hat Linux 支持 TCP/IP 协议以及使用 TCP/IP 的任何网络应用程序。

## Internet servers

一些流行的网络应用程序专门设计用于从一个系统向另一个系统传递信息。当你发送电子邮件（e-mail



## 18 Red Hat Linux 包含的内容

或使用网页浏览器访问网站时，您使用这些网络应用程序（也称为 Internet 服务）。以下是一些常见的 Internet 服务：

- 电子邮件（e-mail）您使用它通过类似 `joe@someplace.com` 的地址向 Internet 上任何其他人发送消息。
- 万维网（或简称为 Web）您使用网页浏览器浏览。
- 新闻服务，您可以在其中阅读新闻组并向名称如 `comp.os.linux.networking` 或 `comp.os.linux.setup` 的新闻组发布新闻项目。
- 文件传输实用程序，您可以使用它下载文件。
- 远程登录，您可以使用它连接到 Internet 上的另一台计算机（远程计算机）并与其工作——前提是您拥有访问该远程计算机所需的用户名和密码。

任何 Red Hat Linux PC 都可以提供这些 Internet 服务。为此，PC 必须连接到 Internet，并且必须运行我们称为 *Internet 服务器* 的特殊服务器软件。每个服务器都使用特定的协议来传输信息。例如，以下是您在 Red Hat Linux 中会找到的一些常见 Internet 服务器：

- `sendmail` 是用于使用 SMTP（*简单邮件传输协议*）在系统之间交换电子邮件的邮件服务器。
- Apache `httpd` 是用于使用 HTTP（*超文本传输协议*）从一个系统向另一个系统发送文档的 Web 服务器。
- `vsftpd` 是用于使用 FTP（*文件传输协议*）在 Internet 上的计算机之间传输文件的服务器。
- `innd` 是用于使用 NNTP（*网络新闻传输协议*）以存储转发方式在 Internet 上分发新闻文章的新闻服务器。
- `in.telnetsd` 允许一个系统上的用户使用 TELNET 协议登录 Internet 上的另一个系统。

## 软件开发

Red Hat Linux 特别适合软件开发。开箱即用，它已装满了软件开发工具，例如构建程序所需的编译器和代码库。如果您碰巧了解 UNIX 和 C 编程语言，您在 Red Hat Linux 中编程时会感到宾至如归。

就开发环境而言，Red Hat Linux 具有与您可能在其他 UNIX 工作站上使用的相同基本工具（例如编辑器、编译器和调试器），例如 IBM、Sun Microsystems 和 Hewlett-Packard（HP）的产品。这意味着，如果您白天在一台这样的 UNIX 工作站上工作，您可以在晚上在家中使用 Red Hat Linux PC 以极低的成本复制该开发环境。然后，您可以在家完成工作项目，或将时间投入到您为娱乐而编写并在 Internet 上分享的软件上。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_46_0.png)

只是为了让您了解 Linux 的软件开发支持，这里列出了使 Linux 成为高效软件开发环境的各种功能：

- GNU C 编译器 gcc 可以编译 ANSI 标准 C 程序。
- GNU C++ 编译器（g++）支持 ANSI 标准 C++ 功能。
- GNU Java 编译器（gcj）可以编译用 Java 编程语言编写的程序。
- GNU make 实用程序使您能够编译和链接大型程序。
- GNU 调试器 gdb 使您能够逐步执行程序以查找问题并确定程序失败的位置和方式。（失败程序的内存映像保存在名为 core 的文件中；gdb 可以检查此文件。）
- GNU 配置文件实用程序 gprof 使您能够确定软件使用计算机处理器时间的程度。
- 并发版本系统（CVS）和修订控制系统（RCS）维护版本信息并控制对源文件的访问，以便两个程序员不会无意中修改同一源文件。
- GNU Emacs 编辑器准备源文件，甚至启动编译链接过程来构建程序。
- Perl 是一种脚本语言，您可以使用它编写脚本来完成特定任务，将许多较小的程序与 Linux 命令结合起来。
- 工具命令语言及其图形工具包（Tcl/Tk）使您能够快速构建图形应用程序。
- Python 是一种解释型编程语言，可与 Perl 和 Tcl 相媲美（Red Hat Linux 安装程序 anaconda 就是用 Python 编写的）。
- 动态链接的共享库允许您的实际程序文件更小，因为多个程序可能需要的库代码是共享的——系统内存中只加载一份副本。

## 在线文档

随着您对使用 Red Hat Linux 越来越熟练，您可能希望快速查找信息——例如，无需翻阅（咳咳）这本优秀书籍的页面。幸运的是，Red Hat Linux 提供了足够的在线信息，以便在您模糊记得命令名称但记不起应输入的确切语法时提醒您。

如果您使用 Linux 命令，您可以通过使用 man 命令查看命令的手册页——通常称为 man 页面。（您确实需要记住该命令才能访问在线帮助。）

您也可以从 GUI 桌面获得帮助。GNOME 和 KDE 桌面都附带帮助查看器来查看在线帮助信息。在 GNOME 中，选择 Main Menu::Help。然后您会看到两大类信息：

- **GNOME - 桌面** 是有关如何使用 GNOME 桌面和一些 GNOME 应用程序的信息。
- **附加文档** 包括 GNU 软件（主要为软件开发工具）的在线文档以及在线手册页（简称为 man 页面）的集合。

然后您可以通过单击初始帮助窗口上的链接来浏览主题。图 1-1 显示了 GNOME 中典型的帮助文件。

在 KDE 桌面中，您可以通过选择 Main Menu::Help 来启动 KDE 帮助。KDE 帮助应用程序看起来与 GNOME 帮助浏览器相似（图 1-2）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_47_0.png)

图 1-1：以下是 GNOME 桌面中在线帮助的典型示例。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_48_0.png)

然后您可以单击链接查看特定的在线帮助信息。有链接可学习如何使用 KDE，并获取有关 KDE 项目的信息。另一组链接提供了对 man 页面和 GNU info 页面的访问，就像 GNOME 帮助浏览器一样。

## 20 Red Hat Linux 包含的内容

## Red Hat Linux 帮助您管理的内容

作为操作系统，Red Hat Linux 充当您作为“系统主人”管理所有硬件的中介。硬件包括系统机箱、显示器、键盘、鼠标以及连接到系统机箱的任何其他设备。统称 *外设* 指的是连接到系统的任何设备。如果您使用笔记本电脑，所有硬件都集成在笔记本电脑中。

在该系统机箱内部是系统的“大脑”——微处理器（例如 Intel Pentium 4）或中央处理器（CPU），它 *执行* 计算机程序中包含的指令。当微处理器运行计算机程序时，该程序的指令存储在内存或 RAM 中。RAM 代表 *随机存取存储器*（这意味着内存的任何部分都可以随机访问——按任意顺序）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_48_1.png)

系统机箱还有另一个关键组件——硬盘或有时称为硬盘驱动器。硬盘是计算机程序和数据的永久存储空间。它的“永久”是指在关闭 PC 电源时内容不会消失。硬盘按文件组织，而文件又以分层方式组织成目录和子目录（有点像将纸质文件夹整理到文件柜的抽屉中）。

为了使 Red Hat Linux 系统正常运行，您或他人必须确保硬件正常工作并且文件定期备份。还有安全问题——确保只有合法人员可以访问和使用系统。这些任务就是我们所说的 *系统管理*。

如果您在拥有许多计算机的大型设施中使用 Red Hat Linux，可能有一名全职系统管理员负责所有系统管理任务。另一方面，如果您在家庭 PC 上运行 Red Hat Linux，您就是系统管理员。不要让这个想法吓到您。要成为系统管理员，您不必学习任何魔法咒语或准备晦涩的配置文件。Red Hat Linux 包含许多图形工具，例如 GNOME 的 Nautilus 图形 shell，使系统管理成为“点按”工作，就像运行任何其他应用程序一样。

那么您要做哪些事情来管理硬件和文件呢？让我们来看看。

## 磁盘、CD-ROM 和 DVD-ROM

Red Hat Linux 包含在两个或多个 CD-ROM 或单个 DVD 上。安装后，Linux 内核和所有应用程序都存储在您的硬盘上——当您告诉它执行某项操作时，PC 首先会查找此处。

通常，在安装过程中会准备硬盘以使用 Red Hat Linux。此后，您通常会让硬盘保持原样，除非备份存储在其中的数据或（偶尔）安装新应用程序。

在 Red Hat Linux 中使用 CD-ROM 或 DVD-ROM 很简单。当您登录到 GNOME 或 KDE 桌面时，只需将 CD 或 DVD-ROM 放入驱动器中，CD 或 DVD 的内容应自动出现在窗口中。从 Red Hat Linux 访问 CD 或 DVD 上的文件这一整个过程称为 *挂载 CD 或 DVD*。



## Red Hat Linux 帮助您管理的内容

除了硬盘和 DVD/CD-ROM 驱动器之外，当然，您的 PC 可能还有其他驱动器，例如软盘驱动器或 Zip 驱动器，而在 Red Hat Linux 中使用这些磁盘也很简单：您只需插入磁盘，然后在 GUI 桌面上双击代表磁盘驱动器的图标即可。这样就会挂载磁盘，以便您开始使用它。

### 外设设备

任何连接到您 PC 的设备都是外设设备，系统机箱内部安装的一些组件（如声卡）也是如此。您可以在 Red Hat Linux 中配置和管理这些外设设备。

常见外设之一是打印机，通常连接到您 PC 的并行端口。（Red Hat Linux 附带了一个图形化打印机配置工具，您可以用它来配置打印机。）

另一个需要配置的外设设备是声卡。与 Windows 不同，Red Hat Linux 要求您在声音工作之前执行配置步骤。同样，您可以运行图形化声卡检测实用程序来测试声卡（从图形桌面中选择 主菜单 > 系统设置 > 声卡检测）。

Red Hat Linux 会在安装时配置鼠标和键盘等其他外设设备。安装后您基本上可以不用再管它们。

如今 PC 都配备了 USB（通用串行总线）接口，许多设备，如打印机和扫描仪，都可以插入 PC 的 USB 端口。USB 设备的一个优点是您可以随时将其插入 USB 端口并拔出——设备不必在系统启动时连接。这就是人们所说的热插拔，因为您可以在系统处于热状态时，即运行时插入设备。Red Hat Linux 支持许多热插拔 USB 设备。当您将设备插入 USB 端口时，Red Hat Linux 会加载正确的驱动程序并使设备可供应用程序使用。

### 文件系统和共享

目录和文件的整体组织称为 *文件系统*。当然，您可以使用 Red Hat Linux 管理文件系统。当您从 GNOME 或 KDE 图形桌面浏览文件时，您会使用熟悉的文件夹图标。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_50_0.png)

维护文件系统的一项关键任务是备份重要文件。在 Red Hat Linux 中，您可以使用 `tar` 程序将一个或多个目录归档到软盘或 Zip 驱动器上。您甚至可以将文件备份到磁带上（如果您有磁带驱动器）。如果您有 CD 烧录机，您还可以刻录一张 CD，其中包含您想要备份或保存的文件。

## 如何开始？

Red Hat Linux 还可以与其他系统在网络上共享文件系统的部分内容。例如，您可以使用网络文件系统（NFS）在网络上的其他系统之间共享文件。对于系统上的用户来说，远程系统的文件似乎位于本地系统的目录中。

Red Hat Linux 还附带 Samba 软件包，它支持与 Microsoft Windows 系统的文件共享。Samba 使 Red Hat Linux 系统像 Windows 文件或打印服务器一样工作。

### 网络

现在大多数 PC 都在局域网中或连接到互联网，您也需要管理网络。Red Hat Linux 附带了网络配置工具来设置局域网。要使用调制解调器连接到互联网，您可以使用互联网配置向导（选择 主菜单→系统工具→互联网配置向导）。

如果您使用 DSL（即电话公司提供的快速互联网连接）或有线调制解调器连接到互联网，那么您需要一台配备以太网卡的 PC，该卡连接到电缆或 DSL。这也意味着您必须设置局域网并配置以太网卡。但幸运的是，这些步骤通常是 Red Hat Linux 安装的一部分。如果您想稍后进行配置，也可以——使用网络配置工具（选择 主菜单→系统设置→网络）。

Red Hat Linux 还包括用于配置 *防火墙* 的工具，防火墙是一种保护缓冲区，有助于防止任何人通过您的互联网连接窥探而使系统相对安全。您可以通过运行防火墙配置工具来配置防火墙（从图形桌面中选择 主菜单→系统设置→安全级别）。

### 如何开始？

根据我个人学习新主题的经验，我建议使用四步流程来开始使用 Red Hat Linux：

- 1. **安装** Red Hat Linux 到您的 PC 上。
- 2. **配置** Red Hat Linux 使一切按您的喜好工作。
- 3. **探索** GUI 桌面和应用程序。
- 4. **学习** 诸如互联网服务器等特定主题的细节。

在以下各节中，我将更详细地解释这一建议。

### 安装

Microsoft Windows 预装在您的新 PC 上，但 Red Hat Linux 通常没有。因此，您面临的第一个障碍是将 Red Hat Linux 安装到您的 PC 上。

在您克服了最初对未知的人类恐惧之后，我敢打赌您会发现 Red Hat Linux 相当容易安装——但首先您从哪里获得它呢？好消息是它是免费的——只需下载即可。例如，您可以访问 Linux Online 网站 www.linux.org 并点击下载按钮。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_52_0.png)

由于完整发行版非常庞大——它占用多个 CD 或一张 DVD——您最好的选择是购买一本（例如这本）附带 Red Hat Linux DVD 的书籍。然后您可以按照书中的说明进行安装。

为了引起您的好奇心，安装涉及在硬盘上为 Windows 和 Linux 创建空间。然后有一个步骤来创建 Linux 分区并从 DVD 安装 Red Hat Linux。在此过程中，您需要配置从以太网卡（如果有）到 X Window 系统的许多项目。

### 配置

当您完成 Red Hat Linux 的安装后，下一步是配置各个系统组件（例如声卡和打印机）并调整安装期间未配置的任何所需设置。

例如，如果您没有获得图形登录屏幕，Red Hat Linux 附带了帮助您排除该问题的工具（通常通过配置 X Window 系统）。

您还希望配置您选择的 GUI 桌面——GNOME 或 KDE。每个都有配置工具。您可以使用这些工具调整桌面的外观和感觉（背景、标题字体，甚至整个配色方案）。

完成配置步骤后，系统上的所有硬件和应用程序都应按您的意愿运行。

### 探索

在拥有配置良好的 Red Hat Linux PC 后，您就可以准备好探索 Red Hat Linux 本身了。您可以在登录后获得的 GUI 桌面上开始探索。

探索 GUI 桌面——GNOME 和 KDE——以及构成 Linux 文件系统的文件夹和文件。您还可以尝试桌面上的应用程序。您会找到办公、多媒体应用程序和数据库可供探索。

您还应该尝试 `shell`——打开一个终端窗口并在该窗口中输入一些 Linux 命令。您还可以探索在文本模式下工作的文本编辑器。了解如何在没有 GUI 的情况下编辑文本文件是很有用的，以防 GUI 不可用。至少您不会束手无策。

### 学习

在您探索了 Red Hat Linux 的全貌并了解了各种内容之后，您就可以深入学习特定主题领域。例如，您可能对设置互联网服务器感兴趣。然后您可以学习设置单个服务器的细节，例如用于电子邮件的 sendmail、用于 Web 服务器的 Apache 以及用于新闻的 INN 服务器。

您还可以选择学习更多领域，例如安全、编程和系统管理。

当然，您可以预期这一步骤会持续下去，即使在您让系统按您想要的方式运行之后——就目前而言。毕竟，学习是一生的旅程。

Bon voyage!



### 第二章：安装 Red Hat Linux

### 本章内容

- 列出你的 PC 硬件清单
- 创建 Red Hat 安装启动盘
- 为 Red Hat Linux 预留磁盘空间
- 开始 Red Hat Linux 安装
- 为 Red Hat Linux 创建硬盘分区
- 设置关键系统参数
- 选择要安装的软件包

PCs 预装了 Microsoft Windows。如果您想使用 Red Hat Linux，首先必须安装它。本书附带 Red Hat Linux DVD — 您要做的就是按照本章中解释的步骤进行安装。

您可能会担心在 PC 上安装新的操作系统。您可能会觉得这就像脑外科手术——或者更确切地说，更像是移植一个新大脑，因为您可以除了 Microsoft Windows 之外再安装 Red Hat Linux。像这样安装两个操作系统时，您可以在开机时选择启动其中一个。将 Red Hat Linux 添加到装有 Windows 的 PC 上最大的麻烦是创建新的磁盘分区——基本上是为 Red Hat Linux 预留磁盘的一部分。剩下的安装过程相当常规，只需按照说明进行即可。我在本章中解释了所有内容。

## 按照安装步骤操作

安装 Red Hat Linux 涉及多个步骤——我希望在不涉及细节的情况下简要带您了解它们。然后您可以按照详细步骤，从本书的附带 DVD 安装 Red Hat Linux。

第一步是快速盘点 PC 中的一些关键硬件组件，并确保它们在 Red Hat Linux 中都能正常工作。

如果您正在购买新 PC，请在购买前确保其组件对 Linux 友好。如果您计划在旧 PC 上安装 Red Hat Linux，请收集有关硬件的信息（制造商、型号等），并将其与 Red Hat Linux 支持的硬件列表进行核对（该列表可在网页 `hardware.redhat.com/hcl` 上获取）。如果旧 PC 的某些组件在 Red Hat Linux 中无法工作——而没有它们就无法运行——那么就不要在该 PC 上安装 Red Hat Linux。

第二步——如果您的 PC 无法从 DVD-ROM 驱动器启动——是准备一个 Red Hat *安装启动盘*——一张软盘，您可以在开始安装时用它来启动 PC。您可以在 Windows 中使用专门为此目的设计的程序（包含在附带 DVD-ROM 上）来准备启动盘。

第三步是在 PC 的硬盘上为 Red Hat Linux 腾出空间。如果您正在运行 Microsoft Windows，此步骤可能容易也可能困难，这取决于您是想用 Red Hat Linux *替换* Windows 还是保留 *两者* Windows 和 Red Hat Linux。

如果您想在不删除（或干扰）Windows 的情况下安装 Red Hat Linux，请记住您现有的操作系统——我假设是 Windows 95、98、Me、NT、2000 或 XP——目前正在使用整个硬盘。这意味着您必须 *分区*（划分）硬盘，以便 Windows 位于其一部分，Red Hat Linux 位于另一部分。这样做可能令人害怕，因为您有损坏硬盘并抹去其上所有内容的风险。

在创建 Red Hat Linux 安装程序可用的硬盘新位置之前，您可能希望使用程序来帮助您创建分区，以保持安心。如果您的 Windows 版本是 NT、2000 或 XP，请考虑投资购买 PartitionMagic 等商业硬盘分区产品。对于 Windows 95/98/Me 系统，您可以使用名为 `FIPS` 的程序（包含在本書 DVD 上）。

在为 Red Hat Linux 预留硬盘分区后，您可以开始最后一步——从 Red Hat 安装启动盘启动 PC 并开始 Red Hat Linux 安装。安装过程中有相当多的步骤，但到目前为止，应该会顺利进行。只需浏览安装屏幕，您应该在一两个小时内完成。Red Hat 安装程序会启动图形用户界面（GUI）并引导您完成所有步骤。其中一个关键步骤再次涉及分区硬盘，但这次您只需分割之前创建的额外分区。完成一些配置步骤后，例如设置网络和时区，您选择要安装的软件包，然后让安装程序完成剩余的安装任务。

## 检查 PC 硬件

在做任何其他事情之前，您首先需要检查 PC 的硬件是否与 Red Hat Linux 兼容。您可以直接开始安装，但如果 Red Hat Linux 无法识别 PC 中的某些硬件，安装可能不会成功。因此，在开始安装 *之前* 请先检查硬件与 Red Hat Linux 的兼容性。

*注意：并非每件硬件都必须与 Red Hat Linux 兼容——只有您想与之一起使用的硬件。例如，您可以在带有不受支持的声卡的 PC 上安装 Red Hat Linux——只要您不在 Red Hat Linux 中关心播放任何音频 CD 即可。*

那么，这里有一份简短的 PC 硬件清单，这些硬件在 Red Hat Linux 中 *必须* 正常工作，否则您无法继续：

- 处理器（也称为中央处理器，或 CPU）
- 硬盘
- DVD-ROM 驱动器（如果您只有 CD-ROM 驱动器，则必须使用本书背面的优惠券订购 CD-ROM 版 Red Hat Linux）
- 键盘

所有这些都必须与 Red Hat Linux 兼容。要使 GNOME 和 KDE 等 GUI 桌面正常工作，PC 还必须具有兼容的鼠标、显卡和显示器。

### 列出清单，再检查一遍

在您能够检查 Red Hat Linux 是否支持 PC 中的硬件之前，您必须先了解 PC 中有什么。要列出 PC 的硬件清单，请按照以下步骤操作：

1. 从 Windows（任何版本）打开控制面板并双击系统图标。

系统属性窗口出现。初始窗口显示一些重要信息，例如 Windows 版本、处理器类型（例如 GenuineIntel Pentium II Processor）和内存容量（例如 128.0MB RAM）。记下这些信息。

2. 在 Windows 95/98/Me 中，单击设备管理器选项卡。在 Windows NT/2000/XP 中，单击硬件选项卡，然后单击设备管理器按钮。

PC 所有设备的信息出现。

3. 浏览按类型显示设备的树状分层组织中的信息。

例如，您会看到 *CDROM, Disk drives, Display adapters* 等标签。单击标签旁边的加号（⊕）可查看该设备类型的详细信息。例如，当我单击 *Display adapters* 旁边的加号时，我会看到 *ATI Xpert98 AGP 2X*，这是我 PC 上显示适配器（显卡）的型号名称。

4. 写下以下设备的制造商、型号以及其他任何信息，以创建您的硬件清单：

- DVD/CD-ROM 驱动器
- 磁盘驱动器
- 显卡
- 显示器
- 键盘
- 鼠标
- 任何网卡、SCSI 控制器、声卡和调制解调器

完成这些步骤后，您需要安装 Red Hat Linux。总结一下，在开始 Red Hat 安装之前，您通常需要收集 PC 中以下一些或全部关键组件的信息：

- **处理器：** 400 MHz Pentium II 或更好为最佳。处理器速度以 *MHz（兆赫）* 或 *GHz（吉赫）* 表示，只要超过 400 MHz 就不是那么重要，但越快越好。Red Hat Linux 也可运行在其他 Intel 兼容处理器上，如 AMD K5、K6 和 Cyrix 以及 IBM 处理器。

- **RAM：** 这是系统拥有的内存量。与处理速度一样，RAM 越多越好。您至少需要 128MB 来安装 Red Hat Linux 并运行 GUI 桌面。（好吧，我承认。我曾在 233 MHz Pentium II、64MB RAM 的 PC 上安装过 Red Hat Linux，它运行良好，但一切——从安装到日常使用——都痛苦地缓慢。至少它能工作！）

- **DVD/CD-ROM：** 具体型号无关紧要。重要的是 DVD/CD-ROM 驱动器如何连接到 PC。大多数新 PC 的 DVD/CD-ROM 驱动器都连接到硬盘控制器（称为 *IDE 即集成驱动电子设备*）。任何 IDE DVD/CD-ROM 在 Red Hat Linux 中都能工作。

- **硬盘：** 如果在磁盘驱动器名称中看到 *IDE* 这个词，那么它就是 IDE 驱动器，应该能在 Red Hat Linux 中工作。另一种硬盘控制器类型是 SCSI（*小型计算机系统接口*），Red Hat Linux 也支持它。您还需要知道硬盘的大小。要查找磁盘大小，请双击 *我的电脑* 图标 on the

在 Windows 桌面上，然后右键单击磁盘驱动器图标（例如，标记为 C），并从弹出菜单中选择“属性”。随后会显示一个窗口，其中包含有关磁盘驱动器的信息，包括总容量和可用空间大小。要舒适地安装并使用 Red Hat Linux，您大约需要 4GB 的磁盘空间。

- 键盘：所有键盘都应能与 Red Hat Linux 配合使用。您只需记下键盘的类型（例如标准 101/102 键键盘）。
- 鼠标：您需要鼠标的类型（例如 PS/2 或 USB）和型号（例如 Microsoft IntelliMouse）来配置 X Window 系统。
- 显卡：您需要显卡的品牌和型号（也称为显示适配器）来配置 X Window 系统。Red Hat Linux 在文本模式下可与所有显卡正常工作，但如果您想要图形界面，则需要能与 X Window 系统配合使用的显卡。
- 显示器：显示器的种类不是特别关键，只要它能够显示显卡使用的屏幕分辨率即可。屏幕分辨率以水平和垂直方向的像素数表示（例如 1024 x 768）。记下显示器的品牌和型号（可在显示器背面找到）。
- 网卡：并非所有 PC 都有网卡，但如果有，请记下其品牌和型号（例如 Linksys LNE100TX 快速以太网适配器）。如果安装程序无法检测到网卡，您需要此信息来设置网络。
- SCSI 控制器：一些高性能 PC 具有连接磁盘驱动器和其他外设到 PC 的 SCSI 控制器。如果您的 PC 恰好有 SCSI 控制器，请记下控制器的名称。
- 声音卡：如果您的 PC 有声卡并且您希望在 Red Hat Linux 中使用声音，您必须知道声卡的品牌和型号并确保其兼容。您可以在成功安装 Red Hat Linux 后配置声卡。
- 调制解调器：如果您计划拨号上网，您需要调制解调器型号信息（例如 Sportster 56k）。

除了这些硬件之外，您还应查明计划在 Red Hat Linux 中使用的任何打印机的品牌和型号。

## 检查 Red Hat 兼容性

手头有硬件清单后，请访问 Red Hat 的网站 hardware.redhat.com/hcl。点击硬件兼容性列表（HCL）链接。从该网页上的搜索表单中，您可以查询硬件是否受支持。

Red Hat 使用以下其中一种方式列出每个硬件组件的状态：

- **已认证**：硬件已由 Red Hat 测试并认证。此类硬件得到完全支持。安装程序会自动检测已认证硬件并安装适当的驱动程序。
- **兼容**：硬件已由 Red Hat 审核并受支持。此类硬件通常已知可正常工作，但 Red Hat 并未认证该硬件。安装程序应能够检测并使用兼容硬件。
- **社区知识**：硬件未经过 Red Hat 测试或支持。要使用此硬件，您可能需要执行一些显式步骤，例如手动加载驱动程序并编辑配置文件。
- **不受支持**：硬件已由 Red Hat 测试并发现无法在 Red Hat Linux 中正常工作。

如果运气好，您 PC 的大多数硬件（例如显卡、显示器和网卡）将是已认证或兼容的。

## 创建 Red Hat 安装启动盘

要启动您的 PC 并开始 Red Hat Linux 安装程序，您需要一个 Red Hat 安装 *启动盘*（如果您的 PC 可以直接从 DVD 启动，则可以跳过此步骤）。要在 Windows 中准备启动盘，使用本书附带 DVD 中的第一个光盘上的程序。

创建启动盘，请按以下步骤操作：

- 1. 在 Windows 95/98/Me 中，通过选择“开始”>“运行”，然后在文本字段中输入单词 Command 来打开 MS-DOS 提示窗口。点击“确定”或按 Enter 运行该程序。
- 2. 在 Windows NT/2000/XP 中，选择“开始”>“运行”。然后在文本字段中输入单词 Command 并按 Enter 或点击“确定”运行该程序。
- 3. 将 DVD 放入 DVD-ROM 驱动器。然后在步骤 1 或 2 中打开的窗口中输入以下命令（我的注释在括号中，您的输入以 **粗体** 显示）：

```
d: (use the drive letter for your DVD-ROM drive)
cd \dosutils
rawrite
Enter disk image source filename: \images\bootdisk.img
Enter target diskette drive: a
Please insert a formatted diskette into drive A: and
press -ENTER-:
```

按说明，将一张已格式化的磁盘放入 PC 的 A 驱动器，然后按 Enter。该磁盘将成为 Red Hat 安装启动盘。

- 4. 当您再次看到命令提示符时，将 Red Hat 安装启动盘从 A 驱动器取出，并在（如果尚未这样做）对其进行标记，以便您知道该磁盘是什么，然后将其放在一旁。

## 为 Red Hat Linux 预留空间

在典型的 Windows PC 中，Windows 位于一个大分区上，占据整个磁盘。您希望缩小该分区并为 Linux 创建空间。在 Linux 安装期间，安装程序会使用该空闲空间作为 Linux 分区。

挑战在于在不破坏硬盘上任何内容的情况下调整当前分区的大小。我将介绍有助于调整分区大小的工具，但在开始之前，您必须确保磁盘上所有已使用的区域都是连续的，或尽可能紧密地排列。这就是碎片整理发挥作用的地方。

### 碎片整理您的硬盘

“碎片整理磁盘”是许多帮助台的咒语。它是帮助台对所有 PC 疾病的处方。好吧，这次他们是对的——您确实需要碎片整理硬盘以腾出空间给 Red Hat Linux。碎片整理所做的是将所有文件移动到分区的开头并紧密排列。结果是分区末尾出现空闲空间，因此分区可以缩小而不会破坏任何数据。

要碎片整理硬盘，请按以下步骤操作：

- 1. **从桌面双击“我的电脑”，右键单击磁盘图标，然后从弹出菜单中选择“属性”。**
- 2. **在“属性”窗口中，点击“工具”选项卡，然后点击“立即碎片整理”按钮。**
- 3. **等待。并且等待。并且等待。**

在磁盘驱动器移动文件时，您会听到很多噪音。几个小时后，碎片整理应该完成。

这些说明有一些需要注意的地方。首先，在碎片整理硬盘时不要使用 PC 或其他程序。关闭所有程序，包括系统托盘中的程序。一种好方法是按 Ctrl-Alt-Del（这会调出任务管理器），点击您想要停止的程序，然后点击“结束任务”按钮。

第二个需要注意的地方是碎片整理程序不会移动隐藏文件——而您的系统中有很多此类文件。您在

![](img/a7eec43a54473e95dc5ea333fecf1bd7_61_0.png)

文件夹中看不到它们，因为（猜猜看）它们是隐藏的。您可能需要手动查找隐藏文件并查看是否可以删除那些看起来像垃圾的文件。（别担心；马上会有说明。）

您可以使用一个简单命令找到 PC 中所有隐藏文件。打开一个命令提示符窗口，然后输入以下命令：

```
cd \
dir /a/h /s > hidden.txt
```

命令完成后，您将在名为 `hidden.txt` 的文本文件中获得所有隐藏文件的列表。您可以在 Microsoft Word 中打开该文件，或直接输入 **edit hidden.txt** 在文本编辑器中浏览该文件。当我尝试此操作时，我注意到有很多文件名类似 ~WRL0004.TMP 的文件——它们明显是临时文件，由某些 Microsoft 软件（可能是 Word）创建。谁知道为什么它们被隐藏了？无论如何，我必须使用类似 `ATTRIB -H ~WRL0004.TMP` 的 MS-DOS 命令更改文件属性，然后输入 `ERASE ~WRL0004.TMP` 来最终删除该文件。我必须对更多垃圾文件重复此操作。真糟糕——但值得花时间仔细操作！

处理隐藏文件的另一个选项是直接取消隐藏它们然后运行碎片整理程序。要取消隐藏 PC 中的所有文件，请在 MS-DOS 窗口中输入以下命令：

```
attrib -h *.* /s
```

坐下来休息一下。经过很长时间后，此命令会取消隐藏所有文件。*然后* 您可以运行碎片整理程序。

### 调整硬盘分区大小

在碎片整理硬盘后，您就可以缩小现有的硬盘分区了。您希望在不损坏硬盘当前内容的情况下执行此操作。您有两个选择：

- **PartitionMagic**：这是一款商业产品，可以调整任何版本的 Microsoft Windows 的硬盘分区大小并创建新分区。
- **FIPS**：这是一款免费程序，可在 MS-DOS 模式下运行并可将现有分区拆分为两个。FIPS 仅适用于 Windows 95/98/Me 系统。更准确地说，FIPS *不* 与 Windows NT/2000/XP 系统中常用的 NTFS 文件系统一起使用。对于这些系统，您最好的选择是 PartitionMagic。

我将快速介绍使用 PartitionMagic 和 FIPS 进行重新分区。



## 使用 PartitionMagic 进行重新分区
PartitionMagic 来自 PowerQuest，可以在从 Windows 95/98/Me 到 Windows NT/2000/XP 的所有 Microsoft 操作系统中调整和分割磁盘分区。它是一款商业产品，所以你必须购买才能使用。在我撰写本文时，PartitionMagic 8.0 的标价为 $69.95。你可以在 `www.powerquest.com/partitionmagic` 上阅读相关信息并购买它。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_62_0.png)

调整磁盘分区始终存在丢失硬盘上所有数据的风险。因此，在使用 PartitionMagic 等磁盘分区工具调整硬盘分区之前，你应该 ***备份你的硬盘***。在备份之后——并且在对分区执行 ***任何*** 操作之前——请确保你能从备份中恢复文件。

当你运行 PartitionMagic 时，它会在一个窗口中显示当前分区。如果你正在运行 Windows XP，你的硬盘通常有两个分区：一个包含 Windows XP 安装文件的小型隐藏分区，以及一个用作 C 驱动器的巨大的第二个 NTFS 分区。你必须减小现有 C 驱动器的大小。这样会在该分区之后创建未使用的空间。然后，在 Red Hat Linux 安装期间，安装程序可以在未使用的空间中创建新的 Linux 分区。

要减小 Windows 分区的大小，请按照以下步骤操作：
- 1. **在 PartitionMagic 主窗口的分区映射中，右键单击分区并从菜单中选择 *Resize/Move*。**
  Resize Partition 对话框出现。
- 2. **在 *Resize Partition* 对话框中，单击并拖动分区的右边缘使其变小。**
  对于大型硬盘（超过 10GB 的任何硬盘），将 Windows 分区减小到 5GB，剩余部分留给 Red Hat Linux。
- 3. **单击 *OK* 然后单击 *Apply* 以应用更改。PartitionMagic 完成更改后，单击 *OK*。**
- 4. **重新启动 PC。**
- 5. **选择 Start::Programs::Accessories::System Tools::ScanDisk 以运行 *ScanDisk*。**

在缩小原来是 C 驱动器的分区后，你无需对剩余的磁盘空间做任何处理。在安装期间，Red Hat 安装程序会使用该空闲空间来安装 Red Hat Linux。

## 使用 FIPS 进行重新分区
随附的 DVD 包含一个名为 FIPS 的实用程序 (*the First Nondestructive Interactive Partition Splitting Program*)，它可以将现有磁盘分区拆分为两个分区。FIPS 会圈出硬盘上未使用的部分，并从该未使用部分创建一个新分区，而不会破坏任何现有数据。FIPS 无法拆分使用 NTFS 文件系统的分区，而该文件系统常用于 Windows NT/2000/XP 系统。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_63_0.png)

在使用 FIPS 重新分区硬盘之前请注意以下几点。用 FIPS 作者 Arno Schaaf 的话说，“FIPS 仍然有些实验性，尽管它已被许多人成功使用且没有严重问题。” 这简明扼要地告诉你，使用 FIPS 时你只能自负其责。出版商或我都不能对因使用或误用 FIPS 造成的损坏承担责任或法律责任。FIPS 有可能损坏你的硬盘，使其无法使用。你只有在确保已备份硬盘上的所有内容并且备份可用后才应尝试使用 FIPS。此外，在使用 FIPS 之前，请检查你的硬盘是否已准备就绪：
- 你的硬盘起初应只有 FAT 或 FAT32 分区。
- 驱动器应有足够的可用空间用于有用的 Red Hat Linux 安装——这意味着 3 到 4 GB（3–4GB）的可用空间。
- 驱动器必须在你使用 FIPS 之前进行碎片整理。
- 驱动器必须未在使用中。你不能在使用硬盘的同时对其进行分区，这意味着（除其他事项外）你不能从 Windows 内部运行 FIPS。你必须关闭 Windows，从启动盘启动，并单独运行 FIPS。

当你准备好使用 FIPS 时，请按照以下步骤操作（仅在运行 Windows 95/98/Me 时使用 FIPS）：
- 1. 通过选择 Start→Settings→Control Panel 打开控制面板。
- 2. 在控制面板窗口中双击添加/删除程序图标。
- 3. 单击“启动盘”选项卡，单击“创建磁盘”按钮，然后按照说明操作。
- 4. 将本书的 DVD-ROM 插入 DVD-ROM 驱动器。
- 5. 使用 Explorer 查看 DOSUTILS 文件夹的内容。然后将 FIPS.EXE 和 RESTORRB.EXE 复制到 A 驱动器中的启动盘。FIPS.EXE 是拆分分区的程序。RESTORRB.EXE 是可以从 FIPS 创建的区域的备份中恢复硬盘部分程序的程序（如果出现问题则使用 RESTORRB）。
- 6. 进入 DVD 上 DOSUTILS 文件夹内的 FIPSDOCS 文件夹。将 ERRORS.TXT 文件复制到启动盘。

ERRORS.TXT 是 FIPS 错误消息的列表。请查阅此列表以了解 FIPS 显示的任何错误消息的解释。
- 7. **将启动盘留在 A 驱动器中，并重新启动 PC。**
  PC 从 A 驱动器启动并显示 `A:\>` 提示符。
- 8. **输入 FIPS。**
  FIPS 程序运行，显示有关你的硬盘的信息。FIPS 在你继续之前给你一个机会保存重要磁盘区域的备份副本。之后，FIPS 会显示可以开始新分区的第一个空闲 *cylinder*（磁盘部分）——以及以兆字节为单位的分区大小。忽略柱面号，关注兆字节数。你需要 3 到 4 千个（即 3 到 4 GB）。
- 9. **使用左右箭头键调整新分区的大小——即从现有分区拆分后得到的新分区。**
  按左箭头会缩小现有分区；按右箭头会在现有分区中留下更多空间，但会减小你正在创建的新分区的大小。
- 10. **当你对新分区的大小满意时，按 Enter。**
  FIPS 显示修改后的分区表并提示你按 C 继续或按 R 重新编辑分区表。
- 11. **按 C 继续。**
  FIPS 显示有关磁盘的一些信息并询问你是否要将新的分区信息写入磁盘。
- 12. **按 Y。**
  FIPS 将新的分区表写入硬盘然后退出。
- 13. **从 A 驱动器中取出磁盘并重新启动 PC。**
  系统重新启动后，你的硬盘上的所有内容应保持完好，但 C 驱动器会变小。这是因为你已从旧 C 驱动器的未使用部分创建了一个新分区。
- 14. **选择 Start::Programs:: Accessories::System Tools::ScanDisk 以运行 ScanDisk。**
  运行此程序可确保 Windows 调整为 C 驱动器的新大小。

在 DOS 下你无需对新创建的分区做任何操作。稍后，在 Red Hat Linux 安装期间，你会从这个新分区创建两个或更多 Linux 分区。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_65_0.png)

使用 FIPS 后，Windows 可能会为 PC 上的其他磁盘和 DVD/CD-ROM 驱动器分配不同的驱动器号。（例如，你的 D 驱动器可能变为 E。）不过，FIPS 确实会确保 C 驱动器保持为 C，因此在 FIPS 拆分分区后你应该能够启动系统。记住这些不同的驱动器名称（例如 E 而不是 D），当你想要访问 C 以外的驱动器上的程序和文件时。至少在你习惯之前，保留它们的清单不会有什么坏处。

## 开始 Red Hat Linux 安装
要安装 Linux，请将 DVD 插入 DVD 驱动器，将 Red Hat 安装启动盘放入 A 驱动器，然后重新启动 PC（在 Windows 中选择 Start→ Shutdown 然后从对话框中选择 Restart）。安装启动盘包含 Linux 内核的较小版本和安装程序。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_65_1.png)

如果你的 PC 可以从 DVD 驱动器启动，你就不需要启动盘。大多数新 PC 可以直接从 DVD 驱动器启动，但某些 PC 可能需要你进行干预。要设置 PC 从 DVD 驱动器启动，你必须在 PC 启动时进入 SETUP。进入 SETUP 并设置启动设备的确切步骤因 PC 而异，但通常涉及按 F2 等键。在 PC 启动时，应该会显示一条简短消息，告诉你按哪个键进入 SETUP。在 SETUP 中，你可以将 DVD 驱动器指定为启动设备。设置好 PC 从 DVD 驱动器启动后，只需将 DVD 放入 DVD 驱动器并重新启动 PC 即可。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_65_2.png)

PC 启动后，它会从启动盘加载 Linux 内核，Linux 内核开始运行 Red Hat 安装程序。剩下的安装过程中，你将使用安装程序的 GUI 屏幕。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_65_3.png)

如果你使用的是 Red Hat 安装启动盘，并且在重新启动 PC 时驱动器中没有 DVD，安装程序将以文本模式启动并提示你插入 DVD。只有在那时它才会启动 X Window System 并切换到图形安装屏幕。

经过几秒钟后，文本屏幕会显示欢迎消息和 `boot:` 提示。欢迎消息告诉你可以通过按 F1 到 F5 之间的功能键获得帮助。要立即开始安装 Red Hat Linux，请按 Enter。然后你有机会测试 DVD 媒体是否存在任何问题。按 Enter 执行媒体检查。媒体检查后，你可以继续安装。

在快速（400MHz 或更好）的 Pentium PC 上，从随附 DVD 安装 Red Hat Linux 大约需要一个小时，如果你安装几乎所有软件包的话。



Red Hat 安装程序会探测——尝试确定——特定硬件的存在，并据此调整安装步骤。例如，如果安装程序检测到网卡，程序会自动显示配置你的 PC 在 Linux 中使用网络所需的屏幕。你可能会看到与本章所示不同的屏幕顺序；确切的顺序取决于你 PC 的具体硬件配置。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_66_0.png)

如果在安装过程中遇到任何问题，请参阅本迷你书的第 3 章。该章说明如何排查常见的安装问题。

## 选择键盘、鼠标和安装类型

这是安装的第一阶段，在此阶段你需要完成一系列步骤，然后再继续为 Red Hat Linux 创建磁盘分区。以下是第一阶段的步骤：

- 1. 安装程序会显示一个语言列表，你可以在整个安装过程中使用这些语言。使用鼠标从显示的列表中选择你想要的语言，然后单击“下一步”继续到下一步。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_66_1.png)

每个屏幕的左侧都有在线帮助可用。你可以阅读帮助信息以了解更多关于在特定屏幕中应该做什么的内容。

- 2. 安装程序会显示键盘布局列表，如图 2-1 所示。

选择适合你语言字符集的键盘布局（例如，美国的美国英语）。

- 3. 安装程序会显示一个屏幕（见图 2-2），你可以在此配置系统中的鼠标。

树状列表显示鼠标类型，按制造商字母顺序组织。你应该知道你的鼠标类型以及它是否连接到 PC 的串行端口或 PS/2 端口（小圆连接器）。如果鼠标名称出现在列表中，请选择它。否则选择通用鼠标类型。大多数新 PC 都有 PS/2 鼠标。最后，对于双按钮鼠标，选择“模拟 3 个按钮”选项。因为许多 X 应用程序假定你使用的是三按钮鼠标，所以应选择此选项。（在典型的双按钮鼠标上，你可以通过同时按下两个按钮来模拟中键单击。在 Microsoft Intellimouse 上，滚轮充当中键。）

Figure 2-1:
从此屏幕选择键盘配置。

### 键盘配置

选择你希望系统使用的键盘布局类型（例如，美国英语）。

- 俄语 (Microsoft)
- 俄语 (ru)
- 俄语 (ru2)
- 俄语 (win)
- 斯洛伐克语
- 斯洛文尼亚语
- 西班牙语
- Speakup
- Speakup (laptop)
- 瑞典语
- 瑞士法语
- 瑞士法语 (latin1)
- 瑞士德语
- 瑞士德语 (latin1)
- 土耳其语
- 乌克兰语
- 英国
- 美国英语
- 美国国际

![](img/a7eec43a54473e95dc5ea333fecf1bd7_67_0.png)

Figure 2-2:
在此屏幕中配置你的鼠标。

### 鼠标配置

为你的系统选择正确的鼠标类型。

你有 PS/2、USB、总线或串行鼠标吗？（提示：如果鼠标插入的连接器是圆形的，则是 PS/2 或总线鼠标；如果是矩形的，则是 USB 鼠标；如果是梯形的，则是串行鼠标。）

尝试找到完全匹配项。如果找不到完全匹配项，请选择与你的兼容的项。否则，选择适当的通用鼠标类型。

如果你有串行鼠标，请选择设备和端口...

- ATI 总线鼠标
- 通用
- 2 键鼠标 (PS/2)
- 2 键鼠标 (串行)
- 2 键鼠标 (USB)
- 3 键鼠标 (PS/2)
- 3 键鼠标 (串行)
- 3 键鼠标 (USB)
- 滚轮鼠标 (PS/2)
- 滚轮鼠标 (USB)
- Genius

- /dev/ttyS0 (COM1 under DOS)
- /dev/ttyS4 (COM2 under DOS)
- /dev/ttyS2 (COM3 under DOS)
- /dev/ttyS3 (COM4 under DOS)

![](img/a7eec43a54473e95dc5ea333fecf1bd7_67_1.png)

如果你选择带串行接口的鼠标，你必须指定鼠标连接的串行端口。对于 COM1，指定 `/dev/ttyS0` 作为设备；对于 COM2，设备名称是 `/dev/ttyS1`。

安装程序尝试检测显示器并显示结果屏幕，无论检测是否正确（见图 2-3）。

- 4. **如果 Red Hat 安装程序显示的显示器错误或为通用项，请滚动列表并从列表中选择你显示器的正确名称。**

（显示器的一个好处是，你总能很容易地在显示器背面查到品牌和型号。）

- 5. **安装程序会显示一个屏幕，询问你是否要安装新系统或升级旧的 Red Hat 安装。对于新的 Red Hat Linux 安装，单击“安装”。然后一个屏幕（见图 2-4）会提示你选择安装类型。**

对于新安装，你必须选择安装类型 — 个人桌面、工作站、服务器或自定义。个人桌面、工作站和服务器安装通过预定义的方式分区磁盘来简化安装过程。个人桌面安装为家庭、笔记本或桌面使用创建 Red Hat Linux 系统。图形环境将与生产力应用程序一起安装。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_68_0.png)

Figure 2-3:
从此屏幕选择你的显示器类型。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_69_0.png)

Figure 2-4:
选择你想要的安装类型。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_69_1.png)

![](img/a7eec43a54473e95dc5ea333fecf1bd7_69_2.png)

工作站类安装会安装图形环境以及软件开发工具。此类安装还会删除所有当前存在的 Linux 相关分区，为 Linux 创建一组新分区。

服务器类安装会删除所有现有磁盘分区，包括任何现有的 Windows 分区，并创建大量 Linux 分区。服务器类安装不安装图形环境。

为了获得最大灵活性，请选择自定义安装。这样你就可以只选择想要尝试的软件包。

安装的下一个主要阶段涉及为 Red Hat Linux 分区硬盘。

## 为 Red Hat Linux 分区磁盘

Red Hat 安装程序会显示一个屏幕（见图 2-5），你可以在此选择分区策略。

屏幕为你提供了以下用于分区和使用硬盘的选项：

- **自动分区：** 此选项（大多数用户选择的选项）会使 Red Hat 安装程序根据你选择的安装类型（如工作站或服务器）创建用于安装 Linux 的新分区。自动分区后，你有机会自定义分区。
- **使用 Disk Druid 手动分区：** 使用此选项，你可以使用 Disk Druid 程序，该程序可让你分区磁盘，同时指定要加载的 Linux 文件系统的哪些部分，以及在哪个分区（或分区）上。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_70_0.png)

从磁盘分区策略屏幕（参见图 2-5）中，选择第一个选项，让安装程序为你自动分区磁盘。Red Hat 安装程序随后会显示另一个屏幕（见图 2-6），询问你希望如何进行自动分区。

你可以从三个选项中选择：

- **删除此系统上的所有 Linux 分区：** 此选项会导致 Red Hat 安装程序删除所有现有的 Linux 分区并创建用于安装 Red Hat Linux 的新分区。如果你已在 PC 上安装了任何版本的 Linux 并希望将其清除并安装最新版本的 Red Hat Linux，可以使用此选项。
- **删除此系统上的所有分区：** 此选项与第一个选项类似，只是安装程序会删除所有分区，包括由其他操作系统（如 Microsoft Windows）使用的分区。只有当你希望 Red Hat Linux 成为 PC 的唯一操作系统时才使用此选项。
- **保留所有分区并使用现有空闲空间：** 如果你已使用 PartitionMagic 或 FIPS 实用程序为 Linux 创建了空间，请选择此选项以使用硬盘上的空闲空间创建 Linux 分区。如果你是在调整分区大小后在新 PC 上安装 Red Hat Linux，这是要选择的选项。

选择适当的选项并单击“下一步”。例如，如果你选择第一个选项，Red Hat Linux 安装程序会显示一个对话框以确认你的选择，并指出现有 Linux 分区中的所有数据将被丢失。单击“是”继续。安装程序会显示它已准备好的分区，如图 2-7 所示。此屏幕的确切外观取决于你硬盘的当前分区。

此磁盘设置屏幕显示磁盘驱动器的列表以及其中一个驱动器的当前分区信息。如果你想按原样接受这些分区，请单击“下一步”继续。




![](img/a7eec43a54473e95dc5ea333fecf1bd7_71_0.png)

Figure 2-5:
从此屏幕选择磁盘分区策略。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_71_1.png)

Figure 2-6:
从此屏幕选择自动分区选项。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_72_0.png)

Figure 2-7: Red Hat 安装程序创建的磁盘分区。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_72_1.png)

如果你的 PC 内存不足（通常少于 128MB），安装程序会询问是否可以写入分区表并激活交换分区。执行此操作后，你的硬盘分区将被更改。只有在你确定要使用新分区并且确实要安装 Red Hat Linux 时才单击“是”。

## 设置关键系统参数

磁盘分区完成后，你几乎就可以开始安装软件包了。首先，Red Hat 安装程序会提示你设置一些关键系统参数。具体来说，你需要执行以下操作：

- 安装引导加载程序
- 配置网络
- 配置防火墙
- 选择要支持的语言
- 设置时区
- 设置 root 密码

你可以相当快速地完成这些步骤。

### 安装引导加载程序

你可以安装两种引导加载程序之一——GRUB 或 LILO。GRUB 是 GRand Unified Bootloader 的缩写，LILO 是 Linux Loader 的缩写。引导加载程序是一个微小的程序，驻留在硬盘上，并在你启动 PC 时启动操作系统。如果你硬盘上有 Windows，你可以配置引导加载程序以加载其他已安装的操作系统。

Red Hat 安装程序显示引导加载程序安装屏幕（见图 2-8），提示你选择要安装的引导加载程序——以及安装位置。

屏幕顶部说明 GRUB 是默认引导加载程序，并且默认安装。如果你愿意，可以单击“更改引导加载程序”来选择较旧的 LILO 引导加载程序。你也可以完全跳过引导加载程序安装。如果你选择不安装任何引导加载程序，你应该务必创建启动磁盘。否则，在重新启动 PC 时将无法启动 Red Hat Linux。你可以在安装的最后阶段创建启动磁盘。

引导加载程序安装屏幕中间列出了可以从中启动 PC 的磁盘分区。表格列出了 Linux 分区以及可能包含其他操作系统（如 Windows XP 或 2000）的任何其他分区。该表格中的每个条目都是引导加载程序可以加载和启动的操作系统。任何 Windows 操作系统都以 DOS 标签显示。默认操作系统是图 2-8 所示“默认”列中带有复选标记的那个（在本例中，Red Hat Linux 是默认操作系统）。

为了获得更高的安全性（以免任何人未经密码启动你的系统），请选择“使用引导加载程序密码”复选框。安装程序会显示一个对话框，你可以在其中为 GRUB 指定密码。

如果你选择“配置高级引导加载程序选项”复选框（图 2-8）并单击“下一步”，下一个屏幕会提供在以下两个位置之一安装引导加载程序的选项：

- 主引导记录（MBR），位于你的 PC 硬盘（C 驱动器）的第一个扇区
- Linux 启动分区的第一个扇区

除非你使用的是另一个操作系统加载程序，例如 BootMagic 或 Windows NT/2000/XP 启动管理器，否则应将引导加载程序安装在主引导记录中。做出选择后，单击“下一步”继续。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_74_0.png)

Figure 2-8:
指示是否安装引导加载程序以及安装位置。

### 配置网络

假设 Linux 内核检测到网卡，Red Hat 安装程序会显示网络配置屏幕（如图 2-9 所示）。

从此屏幕，你可以设置网卡的 IP 地址（以便网络中的其他 PC 可以与你的 PC 通信）。此屏幕显示安装在你的 PC 中的网络设备列表（例如以太网卡）。对于每个网络设备，你可以指示 IP 地址的设置方式。单击列表旁边的“编辑”按钮，会出现一个对话框（如图 2-10 所示）；在那里你可以指定选项。

你有两种选择来指定网卡的 IP（Internet 协议）地址：

- **使用 DHCP 配置：** 如果你的 PC 从动态主机配置协议（DHCP）服务器获取 IP 地址和其他网络信息，请启用此选项。如果你的 PC 连接到 DSL 或有线调制解调器路由器，通常就是这种情况。
- **启动时激活：** 启用此选项可在系统启动时打开网络。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_75_0.png)

Figure 2-9:
从此屏幕配置网络选项。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_75_1.png)

Figure 2-10:
从类似此的对话框配置每个网络接口。

仅当你的局域网上运行着 DHCP 服务器时才选择 DHCP。如果你选择 DHCP，你的网络配置将自动设置，你可以跳过本节的其余部分。

如果你未选择“使用 DHCP 配置”选项，你必须提供 IP 地址和其他网络信息。通过在对话框中出现的文本输入字段中输入所需参数来完成此操作（参见图 2-9）。做出适当的选择并单击“确定”关闭对话框。

在网络配置屏幕的其余部分（图 2-9）中，你指定如何设置主机名。你有两个选项：

- **通过 DHCP 自动：** 启用此选项可使用 DHCP 自动分配主机名（名称形式为 dhcpc1、dhcpc2 等）。
- **手动：** 如果你想手动指定主机名并在单选按钮旁边的文本字段中输入名称，请使用此选项。

输入所需参数并单击“下一步”继续。

### 配置防火墙

在此步骤中，从防火墙配置屏幕（见图 2-11）中选择预定义的安全级别，并根据需要自定义这些安全级别。

从此屏幕，你可以设置 Red Hat Linux PC 的安全级别。你必须从以下选项中选择一个：

- **无防火墙** 表示你的系统接受所有类型的连接且不执行任何安全检查。仅当你的系统在受信任的网络中运行或计划稍后设置防火墙配置时才使用此选项（越早越好）。
- **启用防火墙** 表示你想设置防火墙。然后你可以选择允许通过防火墙的服务，例如邮件和 FTP。你还可以输入允许通过防火墙的端口号。你还可以允许来自特定 NIC 的所有流量。

配置完防火墙后，单击“下一步”继续。

### 选择要支持的语言

在此步骤中，选择安装完成后你的 Red Hat Linux 系统必须支持的一个或多个语言。这些是在完成 Red Hat Linux 安装后重新启动 PC 时系统将支持的语言。从语言支持选择屏幕中选择一个或多个要支持的语言。你还必须选择默认语言。然后单击“下一步”继续。

### 设置时区

完成网络配置后，选择时区——当地时间与格林威治、英格兰当前时间的差值，这是标准参考时间（也称为 *格林威治标准时间* 或 GMT 以及 UTC 或 *协调世界时*）。安装程序会显示一个屏幕（如图 2-12 所示），你可以从中按地理位置选择时区。

当你将鼠标移到地图上时，当前选定位置的名称会出现在文本字段中。如果愿意，你也可以从长长的国家和地区列表中选择你的位置。例如，如果你住在美国东海岸，选择 America/New_York。（当然，最简单的方法是在地图上直接单击美国东部你所在城市附近的位置。）

选择时区后，单击“下一步”继续。

### 设置 root 密码

安装程序显示“设置 root 密码”屏幕（见图 2-13），你可以在其中设置 root 密码。Red Hat 安装程序的早期版本允许你在此时添加一个或多个用户帐户，但现在你可以在系统首次启动时添加用户帐户（参见本小册子的第 4 章）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_77_0.png)

Figure 2-11:
从此屏幕选择安全级别。



### 图 2-12：
按地理位置选择时区。

## 时区选择

通过选择计算机的物理位置来设置时区。

在交互式地图上，点击某个城市（用黄色点标记），会出现一个红色 X 表示您的选择。您也可以滚动可用列表并选择一个时区。

您也可以滚动城市列表并选择所需的时区。

您还可以选择“系统时钟使用 UTC”选项。UTC，也称为 GMT，将允许您的系统

### 图 2-13：
从此屏幕设置 root 密码。

## 设置 Root 密码

仅将 root 账户用于系统管理。安装完成后，为日常使用创建非 root 账户，并在需要快速修复问题时使用 su - 获取 root 权限。这些基本规则将最大限度地降低因输入错误或错误命令而损坏系统的风险。

root 用户是 Linux 中的超级用户——可以在系统中执行任何操作的人。最好将该账户保留供您自己专属使用。您应设置一个自己能记住但他人难以猜到的密码。密码至少应为八个字符长，包含字母和数字的混合，并（为稳妥起见）加入一些特殊字符，例如 + 或 *。

在第一行输入密码，并在下一行重新输入密码。密码中的每个字符在屏幕上都显示为星号 (*)。您必须输入两次密码，并且两次输入必须匹配，安装程序才会接受。这项功能可确保输入错误的（或猜测的）密码无法使用。

您必须在继续安装其余部分之前输入 root 密码。完成后，点击下一步按钮继续安装。

## 选择和安装软件包组

在设置好关键系统参数后，安装程序会显示一个屏幕，您可以从中选择要安装的 Red Hat Linux 软件包组。选择完软件包组后，您可以休息一下，让 Red Hat 安装程序忙于格式化磁盘分区并将所有选定的文件复制到这些分区。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_79_0.png)

软件包组由多个 Red Hat 软件包组成。每个 Red Hat 软件包反过来又包含许多文件，这些文件构成特定的软件。

图 2-14 显示了软件包组列表（实际上是软件组件）的屏幕，您可以从中选择要安装的项目。图标、描述性标签和复选框前缀标识每个软件包组。

一些软件包组已被选中，如复选框中的勾号所示。将选中的软件包组视为 Red Hat 为您选择的安装类型（工作站、服务器或自定义）推荐的最小软件包集。然而，您可以选择安装任何或全部组件。使用鼠标在滚动列表中上下移动，点击复选框以选择或取消选择每个软件包组。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_79_1.png)

在实际的生产 Red Hat Linux 安装中，您只会安装所需的软件包组。然而，当您试图学习有关 Red Hat Linux 的所有内容时，您需要许多不同的软件包。如果 Linux 分区有足够的磁盘空间（至少 6GB），请选择标记为 Everything 的软件包组——这将安装所有软件包组，以便您可以尝试全部功能。

### 图 2-14：
从此屏幕选择要安装的软件包组。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_80_0.png)

![](img/a7eec43a54473e95dc5ea333fecf1bd7_80_1.png)

除了从图 2-14 所示屏幕中选择的软件包组外，Red Hat 安装程序还会自动安装大量运行 Linux 内核和您选择的应用程序所需的软件包。即使您在此屏幕上未选择任何软件包组，安装程序也会安装大量软件包——它们都是运行核心 Linux 操作系统和最小工具集所必需的。

每个软件包组都需要特定的软件包才能运行。Red Hat 安装程序会自动检查任何软件包依赖关系，并向您显示尚未选择的任何必需软件包的列表。在这种情况下，您应安装所需的软件包。

选择完要安装的软件包组后，点击下一步继续。

然后安装程序会显示一个屏幕，告知您安装即将开始。点击下一步继续安装。Red Hat 安装程序格式化磁盘分区并安装软件包。在安装软件包时，安装程序会显示一个状态屏幕以显示安装进度，包括待安装软件包总数、已安装数量、估计所需的磁盘空间量以及安装完成前的估计剩余时间等信息。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_81_0.png)

硬盘格式化和安装可能需要相当长的时间——因此您可以休息一下，大约 15 分钟后再回来。回来后，您可以从不断更新的状态屏幕中大致了解剩余时间。

安装完所有软件包后，安装程序会显示一个屏幕（图 2-15），提示您将一张空白软盘插入 PC 的 A 驱动器。该软盘是启动盘，如果硬盘出现问题（或未安装启动加载器）时，您可以用它来启动 Red Hat Linux。

将一张空白软盘插入 PC 的 A 驱动器并点击下一步（请注意，软盘上的所有数据将被销毁）。安装程序会将 Linux 内核和其他一些文件复制到软盘上。

创建完启动盘后，安装程序会显示一条消息，告知您安装已完成，并提示您访问 Red Hat 网站 www.redhat.com/errata 以获取更新和错误修复信息。点击退出按钮重新启动您的 PC。

恭喜！您现在拥有一个全新的 Red Hat Linux 系统！

![](img/a7eec43a54473e95dc5ea333fecf1bd7_81_1.png)

### 图 2-15：
选择是，插入一张空白软盘，然后点击下一步创建启动盘。

### 第 3 章：故障排除和配置 Red Hat Linux

### 本章内容

- ✓ 故障排除安装
- ✓ 配置 X
- ✓ 设置打印机
- ✓ 打开声音
- ✓ 添加用户账户
- ✓ 管理 CD-ROM
- ✓ 安装 RPM 软件包

在 Red Hat Linux 安装期间，安装程序会尝试检测关键硬件组件，例如 SCSI 控制器和网卡。然后，根据检测到的内容，程序会引导您完成一系列安装步骤。例如，如果安装程序无法检测到网卡，它将跳过网络配置步骤。

另一个安装问题是在重新启动 PC 时出现，而不是图形登录屏幕，您会得到一个文本终端——这意味着 X Window System（或 X）配置有问题。

此外，Red Hat 通常保持安装简单，并不包含 PC 系统中每件硬件的配置程序。例如，安装不会设置打印机或配置声卡。

在本章中，我将向您展示一些安装 Red Hat Linux 的替代方法，以便您可以强制其配置一些关键硬件，例如网卡和 SCSI 控制器（如果有）。我将向您展示如何重新配置 X 并执行其他一些配置步骤，例如添加用户账户、设置打印机和配置声卡。

您可能还需要从附带的 DVD 安装额外的软件包。我将向您展示如何安装 Red Hat 软件包（RPM）——这是您从该软件中获得最大收益的格式。



## 使用文本模式安装

Red Hat 安装程序尝试使用最小的 X Window System (X) 来显示图形用户安装界面。如果安装程序无法检测到显卡，X 将无法启动。如果——出于此原因或其他任何原因——它无法启动 X，你始终可以退回到文本模式安装。然后你可以手动指定显卡。

要使用文本模式安装，在从 Red Hat 安装启动软盘启动 PC 后，在 boot: 提示符下输入 text。从那时起，安装的基本流程与我在本书第 2 章中描述的图形安装类似。你应该能够响应提示并完成安装。

在文本模式下，如果安装程序无法检测到显卡，它会显示一个显卡列表供你选择。通过选择显卡，可以使 X 在重新启动 PC 时正常工作的可能性更大。如果不行，你可以使用 Xconfigurator 程序来配置 X（我在本章后面会介绍）。

## 使用 linux noprobe 命令

如果 Red Hat 安装程序未检测到 SCSI 控制器或网卡，你可以通过在 boot: 提示符下输入 linux noprobe 手动指定这些设备。

要查看安装程序是否检测到硬件，请在 Linux 内核启动时显示的消息中查找 SCSI 或网络设备的任何迹象。要在安装过程中查看这些消息，请按 Ctrl+Alt+F4。这会将显示切换到文本模式虚拟控制台，消息会显示在该控制台上。（虚拟控制台是存储在内存中的文本或图形信息屏幕，你可以通过按特定键序列在物理屏幕上查看它。）

未检测到硬件的另一个迹象是安装程序跳过某个步骤。例如，如果 Linux 内核未检测到网卡，安装程序将跳过网络配置步骤。

要手动安装设备，请按以下步骤操作：

- 1. 在初始文本屏幕的 boot: 提示符下输入 linux noprobe。
安装程序随后会显示一个对话框，让你有机会添加设备。
- 2. **按 Tab 键突出显示 Add Device 按钮；然后按 Enter。**
安装程序显示一个对话框，提示你输入设备类型——SCSI 或 Network。
- 3. **如果有任何 SCSI 设备，例如 SCSI 硬盘，请选择 SCSI 并按 Enter。**
安装程序显示 SCSI 控制器列表。当你选择系统上的控制器并按 Enter 时，安装程序会加载相应的驱动模块。SCSI 驱动程序会自动探测并确定 SCSI 控制器的设置。

在添加任何 SCSI 控制器后，你会回到初始对话框——从那里你可以添加网卡。
- 4. **如果从列表中选择 Network 并按 Enter，安装程序会显示一个网卡列表供你选择网卡。**
当你按 Enter 时，安装程序会加载所选网卡的驱动模块。然后该驱动程序会探测并确定网卡设置。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_84_0.png)

- 5. **[可选] 如果你需要一个不随 Red Hat Linux 提供的 Linux 设备驱动程序，请尝试查看厂商的网站或搜索引擎（如 Google — www.google.com）。**
许多硬件厂商为 Linux 设备驱动程序提供下载，就像他们提供 Windows 驱动程序一样。

在你完成添加 SCSI 控制器和网卡后，安装程序会切换到图形模式并引导你完成剩余的安装。

## 故障排除 X

我在每次在旧 PC 上安装 Red Hat Linux 时都会遇到这个问题：在安装期间，GUI 安装工作正常——但在安装后首次重新启动 PC 时，图形登录屏幕不会出现。相反，启动过程似乎在启动 `firstboot` 时就挂起了。如果这也发生在你身上，以下是如何排除故障。

该 `firstboot` 过程是一个特殊步骤，如果一切顺利，Red Hat 设置代理将启动并允许你执行一次性设置（如日期和时间配置）以及从其他 CD 安装程序。`firstboot` 可能卡住的原因是你的系统上图形 X 环境无法工作。你必须绕过 firstboot 过程并重新配置 X，然后才能继续 Red Hat 为你规划的正常流程。以下是你应该做的：

- 1. **按 Ctrl+Alt+F1 返回到启动屏幕。**
你会看到文本显示，启动消息停止在显示 firstboot 信息的行。
- 2. **按 Ctrl+Alt+Del 重新启动 PC。**
PC 开始启动，你会看到一个屏幕，GRUB 启动加载程序提示你，按 Enter 启动 Red Hat Linux。
- 3. **按 A 添加供 Linux 内核使用的选项。**
然后 GRUB 启动加载程序会显示 Linux 内核的命令行并提示你添加想要的内容。
- 4. **输入一个空格后跟单词 single，然后按 Enter。**
Linux 内核以单用户模式启动并显示如下提示符：
```
sh-2.05b#
```
现在你可以配置 X 了。

X 使用一个名为 XF86Config 的配置文件来确定显示卡类型、监视器以及你想要的屏幕分辨率类型。Red Hat 安装程序会准备配置文件，但有时配置不正确。

要快速创建一个可用的 XF86Config 文件，请按以下步骤操作：

- 1. **输入以下命令：**
```
/usr/X11R6/bin/XFree86 -configure
```
屏幕变空白，然后 XFree86 在显示一些消息后退出。消息的最后一行如下：
```
To test the server, run 'XFree86 -xf86config /root/XF86Config.new'
```
- 2. **通过输入以下命令尝试新的配置文件：**
```
/usr/X11R6/bin/XFree86 -xf86config /root/XF86Config.new
```
如果你看到一个带有 X 形光标的空白屏幕，配置文件可能工作正常。
- 3. **按 Ctrl+Alt+Backspace 终止 X 服务器。**
- 4. **使用以下命令将新的 XF86Config 文件复制到 /etc/X11 目录：**
```
cp /root/XF86Config.new /etc/X11/XF86Config
```
这应该能提供一个可用的 X 配置文件。

**通过按 Ctrl+Alt+Del 或输入 reboot 重新启动 PC。**

如果一切顺利，你将经历正常的 Red Hat Linux 初始设置屏幕并（最终）获得图形登录屏幕。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_86_0.png)

使用 X 服务器的 -configure 选项创建的 XF86Config 文件无法以最佳分辨率显示。为了微调配置文件，你应在系统重新启动后运行显示设置实用程序（选择主菜单：系统设置：显示）。使用该实用程序，你可以通过图形用户界面配置显卡、监视器和显示设置。

## 解决其他安装问题

我确信我没有穷尽所有潜伏在外的安装问题。没人能做到。Intel x86 PC 中组件的组合如此之多，以至于墨菲定律几乎要求存在某种硬件组合，安装程序无法处理。本节列出了一些已知问题。对于其他问题，我建议你前往 Google Groups（groups.google.com）并输入一些故障症状。假设其他人也遇到类似问题，你应该能得到一些关于如何排除你特定困境的提示。

### 无法从启动磁盘启动

有时 PC 无法使用 Red Hat 安装启动磁盘启动。如果发生这种情况，请尝试使用全新软盘创建另一个启动磁盘，看看是否能解决问题。否则你可能需要更新的启动映像（一个小型程序，运行 Linux 内核然后从 DVD 加载 Red Hat 安装程序以开始操作）。新的启动映像（如有）应可在 Red Hat 支持网站（www.redhat.com/apps/support/errata/）获得。下载映像文件后，将其保存在 Windows 系统上，给它一个简短的名称，例如 new.img，然后按照本书第 2 章中解释的步骤创建新的启动磁盘。记住在被询问映像源文件名的问题时指定新的启动映像文件。



## 致命的信号 11 错误

安装过程中有些人会收到致命的信号 11 错误信息——并且会使进程完全停止。这通常发生在初始启动画面之后，当 anaconda 安装程序开始其图形用户界面或文本界面时。安装期间出现信号 11 错误的最可能原因是与内存或 CPU（微处理器）相关的缓存有关的硬件错误。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_87_0.png)

信号 11，也称为 SIGSEGV（Segment Violation Signal 的缩写），也可能在其他 Linux 应用程序中出现。当进程尝试访问其不应该访问的内存位置时，就会发生段违规。操作系统会在问题发生前捕获它，并通过发送信号 11 来停止违规进程。当安装过程中发生这种情况时，意味着 anaconda 在访问内存时出现了错误，最可能的原因是某些硬件问题。针对信号 11 问题常被建议的解决方法是在 BIOS 中关闭 CPU 缓存。为此，你需要在 PC 启动时进入设置（通过按 F2 等功能键），然后从 BIOS 设置菜单中关闭 CPU 缓存。

如果问题是由于内存中的硬件错误（换句话说，是坏内存芯片的结果）引起的，你可以尝试在插槽中交换内存模块的位置。如果你手头有备用的内存模块，也可以考虑用另一个内存模块替换现有的内存模块。

你可以在 www.bitwizard.nl/sig11/ 阅读更多关于信号 11 问题的介绍。

## 设置打印机

Red Hat 安装程序不包括打印机配置步骤，但你可以通过图形实用程序轻松配置打印机。设置打印机，请按照以下步骤操作：

- 1. **从图形登录屏幕，以 root 身份登录。**
如果你未以 root 身份登录，请继续下一步，打印机配置工具会提示你输入 root 密码。
- 2. **从 GNOME 或 KDE 桌面，选择 主菜单→系统设置→打印。**
打印机配置工具名为 `redhat-config-printer`。
图 3-1 显示了其主窗口。

图 3-1：
使用打印机配置工具配置和管理打印机。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_88_0.png)

- 3. 单击“新建”按钮以配置新打印机。
这将启动 Red Hat 的打印机配置向导。初始屏幕会显示一条消息，保证在你点击所有步骤末尾的“应用”按钮之前不会进行任何更改。单击“向前”继续。

- 4. 在下一屏幕（见图 3-2）中，输入打印队列的名称和打印队列的简短描述；然后单击“向前”。
为打印队列命名时应采用某种系统化的方法。例如，如果我在二楼 210 房间有一台 HP LaserJet 5000 打印机，我可能会将队列命名为 Room210HPLJ5000，因为这样可以轻松找到打印机。有时系统管理员会选择可爱的名字，如 kermit、piggy、elmo、cookiemonster 等，但当打印机数量太多时，这种可爱方案就不太好用了。最好在打印队列名称中提供有关打印机位置以及品牌和型号的线索。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_88_1.png)

图 3-2：
输入打印队列名称和描述。

- 5. 在下一屏幕（见图 3-3）中，从下拉选择框中选择队列类型；然后单击“向前”。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_89_0.png)

图 3-3：
从此窗口选择打印队列类型。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_89_1.png)

选择适用于你的情况的打印队列类型。例如，如果你想在共享的 Windows 打印机上打印，请选择“Windows 打印机”复选框。

要设置连接到 PC 并行端口的打印机，请选择“本地连接”。

以下类型的打印队列可用：
- **本地连接：** 指直接连接到 PC 的串行、并行或 USB 端口的打印机。
- **网络 CUPS（IPP）：** 指网络上另一台服务器上的通用 UNIX 打印系统（CUPS）打印队列。（IPP 指用于与远程 CUPS 服务器通信的 Internet 打印协议。）
- **网络 UNIX（LPD）：** 指由本地网络上另一台 UNIX 系统上的 LPD 服务器管理的打印队列。（LPD 指 Line Printer Daemon——UNIX 系统的另一种打印调度程序。）
- **网络 Windows（SMB）：** 指连接到本地网络上另一台 PC 上的打印机并使用服务器消息块（SMB）协议的打印机，这是 Windows 文件和打印共享的基础协议。
- **网络 Novell（NCP）：** 指连接到本地网络上 Novell Netware 服务器的打印机。
- **网络 JetDirect：** 指直接连接到本地网络的 HP JetDirect 打印机。

- 6. 如果你选择“本地打印机”，下一屏幕将显示检测到的并行端口信息；单击“向前”继续。

对于其他选项，你会看到一个提示你识别网络打印机的屏幕。指定网络打印机的方式取决于网络类型。例如，要在本地局域网上使用 IP 地址为 192.168.0.8 的主机上的网络 CUPS 打印机，你必须输入类似 http://192.168.0.8:631/printers/HPLaserjetRoom210 的名称，其中 *HPLaserjetRoom210* 是网络打印机的名称。

- 7. 从图 3-4 所示的屏幕中选择打印机的品牌和型号，然后单击“向前”。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_90_0.png)

图 3-4：
从此窗口选择打印机的品牌和型号。

单击下拉列表（滚动列表上方）以显示打印机制造商列表。当你从此列表中选择打印机制造商时，滚动列表会显示该制造商的不同打印机型号名称，如图 3-4 所示（适用于 HP）。如果你有一台 PostScript 打印机，可以直接进入“通用”列表（通用是制造商列表中的一个选项）并选择 PostScript 打印机。

最后一个屏幕（图 3-5）显示有关新打印队列的信息。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_90_1.png)

图 3-5：
检查信息的准确性。

- 8. **查看所有信息以确保其正确，然后单击“完成”以创建打印队列。**
- 9. **当出现对话框询问是否要打印测试页时，单击“是”。**
这样会应用所有更改并重新启动负责打印的打印调度程序程序。打印机现在应打印测试页，之后会出现一个消息框，提示你检查测试页。
- 10. **单击“确定”以关闭消息框。**
新打印队列应出现在打印机配置窗口中，你应该能够向此队列提交打印作业。
- 11. **退出打印机配置工具。**
你可以通过选择“操作→退出”或关闭打印机配置窗口（单击窗口框架右上角的 X 按钮）来实现。

## 打开声音

你的 PC 必须具有声卡和扬声器才能播放音频 CD。如果你的 PC 有声卡，请根据 PC 制造商的说明连接扬声器。

当你首次使用 Red Hat Linux 启动 PC 时，一个名为 Kudzu 的实用程序会检测声卡并安装驱动程序。如果你已完成该步骤，就可以尝试使用声卡。否则，你可以通过以下步骤设置声卡：

- 1. **在图形登录屏幕，以 root 身份登录。**
- 2. **进入 GNOME 桌面后，选择 主菜单→系统设置→声卡检测。**
这将运行 Red Hat 声卡配置实用程序。
声卡配置实用程序从另一个名为 Kudzu 的程序获取有关声卡的信息，并显示检测到的声卡信息（图 3-6）。
- 3. **单击“播放测试声音”按钮以播放测试音。**
如果一切顺利，你应该能听到声音。
- 4. **单击“确定”以退出声卡配置实用程序。**

配置声卡后，你可以在 Red Hat Linux 中播放音频 CD 和其他声音文件。




## 添加用户账户

Figure 3-6:
声卡配置实用程序显示有关声卡的信息。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_92_0.png)

当你第一次启动 Red Hat Linux 时，你有机会添加一个个人用户账户。如果你在首次启动时没有按照本迷你书第 4 章所述添加用户账户（或如果你想为家庭成员或同事添加更多用户账户），你可以使用 Red Hat 用户管理器随时进行操作。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_92_1.png)

除了 root 之外设置一个个人用户账户是个好主意。root 的问题在于该超级用户账户拥有绝对权力——你几乎可以做任何事情，甚至轻松破坏关键系统文件。以普通用户身份登录更安全。当你必须以 root 身份执行某些操作时，只需输入 su 命令即可。你会被提示输入 root 密码；在输入该密码后你将成为 root。完成超级用户任务后，输入 exit 即可返回到你普通的身份。

使用 Red Hat 用户管理器添加用户账户，请按以下步骤操作：

- 1. 从 GNOME 桌面选择 主菜单→系统设置→用户和组。

如果你未以 root 身份登录，Red Hat 用户管理器会提示你输入 root 密码（见图 3-7），你必须输入该密码才能运行管理器。

Figure 3-7:
在此输入 root 密码。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_92_2.png)

- 2. 输入密码并单击“确定”。

Red Hat 用户管理器窗口（见图 3-8）包含两个标签页：用户 和 组。用户标签页显示当前用户账户列表。组标签页列出你的当前组。例如，图 3-8 列出了我的 Red Hat Linux 系统上的用户；你的系统上的列表会有所不同。

- 3. 要添加新用户，请在工具栏上单击“添加用户”按钮。

创建新用户对话框出现，如图 3-9 所示。

- 4. 填写所需信息，然后单击“确定”。

新用户现在会出现在 Red Hat 用户管理器窗口中用户标签页的列表中。

Figure 3-8:
Red Hat 用户管理器窗口显示当前用户账户。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_93_0.png)

Figure 3-9:
输入有关新用户账户的信息。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_93_1.png)

- 5. 重复步骤 3 和 4 以添加任意数量的用户账户。
- 6. 完成后，选择 文件→退出 以退出 Red Hat 用户管理器。

要编辑现有用户账户信息，请从用户标签页的列表中选择用户名，然后在工具栏上单击“属性”按钮。所选用户的信息会出现在用户属性对话框中，你可以在其中编辑；单击“确定”以应用更改。

如果你想删除用户账户，请在用户标签页中单击用户名。然后在工具栏上单击“删除”按钮。

## 管理 CD-ROM

GNOME 桌面使在 Red Hat Linux 中使用 CD-ROM 变得简单。只需将 CD-ROM 放入驱动器中，桌面上就会出现一个图标。在幕后，一个名为 Magicdev 的特殊实用程序始终在运行，等待检测 CD-ROM 的插入或移除。当你插入带有 autorun 文件的 CD 时，Magicdev 会询问是否要运行该文件（图 3-10）。

Figure 3-10:
Magicdev 提示。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_94_0.png)

通常，运行 autorun 文件会启动一个安装程序，可安装 CD 上的软件。

Magicdev 还会自动启动 Nautilus 文件管理器，该管理器显示 CD-ROM 的内容（如图 3-11 所示）。

最后，Magicdev 在 GNOME 桌面上放置一个 CD-ROM 图标。然后你可以通过 Nautilus 文件管理器或桌面上的图标使用该 CD。要访问文件和文件夹，只需在 Nautilus 窗口中双击图标即可。

CD-ROM 图标是对于某些任务例如使用完毕后弹出 CD 的最佳选择。如果你右键单击 CD-ROM 图标，会出现一个弹出菜单，列出你可以对 CD-ROM 执行的操作（如图 3-12 所示）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_95_0.png)

Figure 3-11:
当你插入 CD 时，Nautilus 显示 CD 的内容。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_95_1.png)

Figure 3-12:
选择要对 CD-ROM 执行的操作。

使用完 CD 后，从弹出菜单中选择“弹出”以将 CD-ROM 从驱动器中弹出。这样会自动移除图标。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_96_0.png)

如果 CD-ROM 驱动器中有 CD，但你在 GNOME 桌面上看不到 CD-ROM 图标，只需弹出 CD（按 CD-ROM 驱动器上的弹出按钮）。再次插入 CD，Magicdev 应该能识别该 CD。

KDE 桌面也会自动在名为 Konqueror 的文件管理器中打开 CD-ROM 的内容。例如，图 3-13 显示了在 KDE 桌面中插入 CD 的结果。

Figure 3-13:
KDE 自动在 Konqueror 文件管理器中显示 CD 的内容。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_96_1.png)

## 安装 RPM 软件包

有时你需要安装或移除软件来排查故障或配置 Red Hat Linux 系统。大多数 Red Hat Linux 软件以 Red Hat 软件包管理器（RPM）文件的形式提供。RPM 文件基本上是一个单一的软件包，其中包含安装软件产品所需的一切——所有文件和配置信息。本节介绍如何安装 RPM 软件包。

从 GNOME 桌面使用“添加和删除软件”实用程序——一个用于安装和卸载 RPM 的图形实用程序。按以下步骤操作：

- 1. 选择 主菜单→系统设置→添加/删除应用程序。
- 2. 输入 root 密码并按 Enter。

如果你未以 root 身份登录，对话框会提示你输入 root 密码。

“添加和删除软件”实用程序启动并收集系统上已安装软件包的状态信息。在整理完所有已安装软件包的信息后，实用程序会显示所有软件包的列表（图 3-14）。窗口左侧有两个大按钮：安装软件 和 移除软件。默认情况下选择“安装软件”按钮。

Figure 3-14: “添加和删除软件”实用程序显示有关软件包组的信息。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_97_0.png)

实用程序以软件包组的形式显示软件包信息，例如桌面和应用程序（软件包组是一组相关的 RPM）。每个软件包组都有一个图形图标、一个标签（如 X Window System 或 GNOME 桌面环境）以及简短描述。对于每个软件包组，实用程序显示已安装的软件包数量。如果某个软件包组有未安装的软件包，实用程序会显示“安装”超链接。

- 3. 要安装任何未安装的软件包，请单击该软件包旁边的“安装”超链接。

会出现一个对话框，显示你即将安装的内容的详细信息以及新软件包所需的磁盘空间。图 3-15 显示了在图 3-14 中单击 KDE 桌面环境旁边的“安装”超链接后的结果。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_98_0.png)

Figure 3-15:
软件包组的详细信息。

- 4. 单击“安装软件包”以安装所选软件包。

要移除一个或多个软件包组，请在“添加和删除软件”窗口的左侧面板中单击“移除软件”按钮。现在“添加和删除软件”窗口显示已安装的软件包，并带有“移除”超链接。要从软件包组中移除软件包，请单击该软件包组旁边的“移除”超链接。会弹出一个对话框，列出你可以移除的软件包。单击“移除软件包”，这些软件包就成为历史了！

### 第 4 章：试用 Red Hat Linux

### 本章内容

- ✔ 启动 Red Hat Linux
- ✔ 登录
- ✔ 查看 GUI 桌面
- ✔ 使用 shell
- ✔ 关闭系统

你正坐在电脑前，准备开机。你知道这台电脑已安装了 Red Hat Linux（也许是你自己安装的，但谁在跟踪呢？）你想知道开机后会发生什么以及之后应该做什么。不用担心。如果这是你第一次使用 Red Hat Linux，本章将向你展示如何登录、查看图形桌面、尝试一些神秘的 Linux 命令，最后关闭电脑。

如果你已经了解一些关于 Red Hat Linux 的知识，请翻阅这些页面，看看是否有任何新内容。你永远不知道自己可能不知道什么！

### 启动 Red Hat Linux

当你启动电脑时，它会经过正常的开机序列并加载引导加载程序——GRUB 或 LILO，具体取决于 Red Hat Linux 安装时选择了哪一个。引导加载程序是一个微小的计算机程序，它将操作系统的其余部分从磁盘加载到计算机的内存中。这些程序现在被称为引导加载程序（以前称为引导程序）。启动计算机的整个过程称为引导。

引导加载程序是 LILO 还是 GRUB 并没有太大关系。在任何一种情况下，都会出现一个图形屏幕，显示引导加载程序可以加载的操作系统名称。例如，如果你的电脑同时安装了 Windows 和 Red Hat Linux，你会看到两个名称都被列出。然后你可以使用上、下箭头键选择要使用的操作系统。如果电脑设置成

默认加载 Red Hat Linux，等待几秒钟后引导加载程序启动 Red Hat Linux。更准确地说，引导加载程序将 *Linux 内核* —— Linux 操作系统的核心 —— 加载到 PC 的内存中。

随着 Linux 内核启动，你应该会看到一长串启动消息，通常被称为 *启动消息*（你可以通过在终端窗口中输入 `dmesg` 命令随时查看这些消息）。这些消息包括 Linux 检测到的设备的名称。启动消息中的第一行之一是

```
Calibrating delay loop... 2955.67 BogoMIPS
```

*BogoMIPS* 是 Linux 行话（此处在方便的侧边栏中解释）用于表示时间的一种度量。在 *BogoMIPS* 前面的数字取决于 PC 的处理器速度，无论是旧的 200MHz Pentium 还是新的 4GHz Pentium 4。内核在需要等待某个事件发生的一小段时间时使用 BogoMIPS 测量值（例如在磁盘控制器准备就绪时获取响应）。

在启动消息之后，Red Hat Linux 切换到图形启动屏幕，显示系统启动进度的信息。具体来说，你会看到诸如服务器正在启动和硬件正在探测等信息。

当你安装后首次启动 Red Hat Linux 时，会出现 Red Hat 设置代理，它显示欢迎屏幕，然后引导你进行日期和时间设置（图 4-1）、用户账户设置、声卡检查，并给你机会注册 Red Hat Network 并从任何额外的 CD 安装程序。

## 什么是 BogoMIPS？

随着 Red Hat Linux 启动，你会看到一条消息，内容为 *校准延迟循环... 421.23 BogoMIPS*，其中 *BogoMIPS* 前面有一个数字。*BogoMIPS* 是令新 Linux 用户困惑的词之一，但它只是含义简单的行话。

*BogoMIPS* 是 Linux 的发明（是的，就是启动 Linux 的那位 Linus Torvalds），它意味着 *虚假 MIPS*。如你所知，*MIPS* 是 *每秒数百万条指令* 的缩写 —— 衡量计算机运行程序速度的指标。不幸的是，MIPS 并不是一个很好的性能衡量标准；不同类型计算机的 MIPS 测量值难以准确比较。*BogoMIPS* 基本上是一种与具体处理器类型无关的衡量计算机速度的方法。Linux 使用 *BogoMIPS* 数字来校准 *延迟循环*，在该循环中，计算机不断运行一些无用的指令，直到经过指定的时间。显然，这样浪费宝贵的处理器时间的原因是为了等待某个慢吞吞的设备准备好工作。

图 4-1：从 Red Hat 设置代理中的此屏幕配置日期和时间。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_102_0.png)

如果屏幕变暗且没有活动，首次配置实用程序可能在启动 X Window System 时遇到问题。不幸的是，如果不解决此问题，你无法尝试 Red Hat Linux。有时即使在安装期间图形界面似乎工作正常，图形环境也会失败。有办法修复此问题。请参阅本迷你书的第 3 章，了解如何排查此问题的更多信息。

Red Hat 设置代理的第一个配置步骤是日期和时间设置。你可以从日期和时间窗口（请参阅图 4-1）设置日期和时间，然后单击下一步。

如果你的系统已连接到 Internet，请选择启用网络时间协议复选框，然后从服务器下拉列表中选择一个服务器。这样系统就可以直接从网络上的超精确时间服务器获取时间值。Red Hat 设置代理的第二个配置步骤是设置用户账户。在图 4-2 所示的屏幕中输入账户信息。

输入用户账户信息后，单击下一步。Red Hat 设置代理随后会显示有关声卡的信息，并给你机会播放测试声音。单击下一步继续。Red Hat 设置代理会提示你注册 Red Hat Network（图 4-3）。要注册，请单击下一步并响应所需的信息。完成该步骤后，再次单击下一步。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_103_0.png)

图 4-2：
从此窗口设置用户账户。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_103_1.png)

图 4-3：
您有机会注册 Red Hat Network。

Red Hat 设置代理随后会显示一个窗口，可从中安装来自额外 CD 的程序（图 4-4）。如果有要安装的额外 CD，请单击相应的图标。否则，单击正向。

完成 Red Hat 设置代理后，你就真正完成了，因为它仅在首次启动时运行一次一次。如果由于某种原因，你想再次执行这些步骤（也许你想设置时间或注册 Red Hat Network —— 尽管你可以在不运行设置代理的情况下执行这些操作），以下是再次运行 Red Hat 设置代理的方法：

以 root 身份登录并在终端窗口中输入以下命令（要打开终端窗口，请选择主菜单→系统工具→终端）：

```
rm /etc/sysconfig/firstboot
chkconfig --level 5 firstboot on
```

就这样！下次重新启动 PC 时，你将有机会再次见到 Red Hat 设置代理。如果你想从 GNOME 或 KDE 交互式运行 firstboot，可以以 root 身份登录并在终端窗口中输入以下命令：

```
rm /etc/sysconfig/firstboot
firstboot
```

完成 Red Hat 设置代理后，你应该会看到图形登录屏幕（图 4-5 所示）。

屏幕中间的登录窗口显示一条欢迎消息，其中包含你的 PC 名称 —— 它被称为主机名。名称在网络配置时分配。如果网络未配置，则主机名为 localhost.localdomain。如果你的 PC 从动态主机配置协议（DHCP）服务器获取网络地址（IP地址），则该服务器会为你的 PC 提供一个晦涩的主机名。登录窗口还包含一个文本输入字段，提示你输入用户名。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_104_0.png)

图 4-4：
您可以安装您可能拥有的任何其他 CD。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_105_0.png)

图 4-5：
欢迎屏幕是您以用户身份登录的地方。

屏幕中间的登录窗口显示一个文本输入字段，提示你输入用户名。屏幕右下角显示你的 PC 名称 —— 它被称为主机名。名称在网络配置时分配。如果网络未配置，则主机名为 localhost.localdomain。如果你的 PC 从动态主机配置协议（DHCP）服务器获取网络地址（IP地址），该服务器会为你的 PC 提供一个晦涩的主机名。

例如，要以用户 spiderman 登录，在第一个文本字段中输入 spiderman 并按 Enter（在开始输入前将鼠标移到登录对话框上）。然后输入 spiderman 的密码并按 Enter。你应该会看到初始图形用户界面（GUI —— 简称发音为 gooey）出现。你得到的内容取决于你选择的 GUI —— GNOME 或 KDE。如果有人为你做了选择，不用担心，GNOME 和 KDE 都非常好用且多功能。

## 探索 GUI 桌面

Red Hat Linux 带有两个 GUI 桌面 —— GNOME 和 KDE。如果你同时安装了两者，可以尝试每个 GUI。在登录系统之前很容易选择其中一个桌面 —— 下面我向你展示如何操作。

GNOME 通常是 Red Hat Linux 中的默认 GUI，因此你可以从 GNOME 开始。然后注销并重新登录，但选择 KDE 作为 GUI。这样你就可以尝试两个桌面。

## GNOME

GNOME 是 GNU Network Object Model Environment 的缩写（GNU 如你所知，代表 GNU's Not UNIX）。GNOME 是一个图形用户界面（GUI）和一个编程环境。从用户角度来看，GNOME 就像 Microsoft Windows。在幕后，GNOME 具有许多功能，允许程序员编写可以很好地协同工作的图形应用程序。在本章中，我只指出 GNOME GUI 的一些关键功能，细节留给你在闲暇时自行探索。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_106_0.png)

如果你好奇，可以随时通过访问 GNOME 主页 www.gnome.org 了解有关 GNOME 的最新信息。

通常，GNOME 是 Red Hat Linux 中的默认值。登录后，你会看到 GNOME GUI 桌面。图 4-6 显示了我使用用户名 naba 登录后的 GNOME 桌面。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_106_1.png)

当你以 root 身份登录时，你可能会意外损坏系统，因为作为 root 你可以做任何事情。始终以普通用户身份登录。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_106_2.png)

图 4-6：
初始
GNOME GUI
桌面
登录后

GNOME 桌面的具体外观取决于当前会话（即此时正在运行的应用程序集合）。如你所见，图 4-6 所示的初始 GNOME 桌面与 Windows 桌面非常相似。它具有 GNOME 面板，或简称为面板（类似于 Windows 任务栏）沿底部排列，并且文件夹和应用程序的图标直接显示在桌面上。这与你可以直接将图标放置在 Windows 桌面上的方式相似。

你可以像在 Microsoft Windows 中一样移动和调整窗口大小。此外，与 Microsoft Windows 中的窗口框架一样，窗口标题栏的右上角包含三个按钮。最左边的按钮将窗口缩小为图标，中间的按钮将窗口最大化以填满整个屏幕，最右边的按钮关闭窗口。

## GNOME 面板

GNOME 面板是 GNOME 桌面的关键特性。面板是一个独立的 GNOME 应用程序。如图 4-7 所示，它提供了一个用于菜单和小型面板小程序的显示区域。每个面板小程序都是一个专为在面板内工作而设计的小程序。例如，面板最右侧的时钟小程序显示当前日期和时间。

Figure 4-7:
GNOME 面板。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_107_0.png)

除了最右侧边缘的时钟小程序外，面板还包含其他几个小程序：

- **GNOME Pager 插件：** 提供一个比系统屏幕物理尺寸更大的虚拟桌面。在图 4-7 中，分页器在小型显示区域中显示四个页面。每个页面代表一个与显示屏幕大小相等区域。要转到特定页面，请在分页器窗口中单击该页面。GNOME Pager 插件为当前虚拟页面中显示的每个窗口显示按钮。
- **启动器小程序：** Red Hat 图标右侧的按钮是启动器小程序。这些小程序中的每一个都显示一个带有应用程序图标的按钮。单击按钮会启动（启动）该应用程序。尝试单击这些按钮中的每一个，看看会发生什么。鼠标和地球按钮启动 Mozilla Web 浏览器，而单击钢笔和纸图标则打开 OpenOffice.org Writer 文字处理器。将鼠标移到图标上时，会出现一个小帮助消息，其中包含有关该图标的信息。
- **GNOME 天气小程序：** 显示本地天气。你在启动它之前看不到此小程序。你可以从右键单击面板窗口空白区域时出现的菜单中启动它。

## 主菜单按钮，或“Red Hat Logo”

在图 4-6 中，面板的最左侧边缘显示一个带有熟悉 Red Hat 标志的按钮。那个“红帽子”就是主菜单按钮——GNOME 面板中最重要的部分。就像 Microsoft Windows 中的“开始”按钮一样，你可以从单击红帽子时弹出的菜单中启动应用程序。图 4-8 显示了 Red Hat Linux PC 上主菜单的典型视图。

通常，主菜单及其子菜单列出启动应用程序的项目。有些菜单项带有箭头。将鼠标指针移到带箭头的项目上，另一个菜单就会弹出。在图 4-8 中，菜单选择为 Main Menu→System Settings→Server Settings→Services。请注意，当你指向菜单选择时，会弹出一个气球帮助，其中包含有关该选择的信息。

Figure 4-8: 单击红帽子（主菜单）并将鼠标指针从一个菜单移到另一个菜单以启动你想要的程序。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_108_0.png)

![](img/a7eec43a54473e95dc5ea333fecf1bd7_109_0.png)

你可以从右键单击 GNOME 面板时出现的菜单启动诸如天气小程序之类的程序。要启动天气小程序，请右键单击面板并选择 Add to Panel→Accessories→Weather Report（图 4-9）。在 Add to Panel 菜单中，你会找到更多可以尝试的小程序类别。

Figure 4-9:
右键单击面板并单击 Add to Panel 以查看可用的小程序。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_109_1.png)

浏览主菜单中的所有项目，以查看可从此菜单执行的所有任务。特别是，将鼠标指针移到 Main Menu→Preferences 项目上，以查看更改桌面外观的选项（图 4-10）。例如，你可以从此菜单更改桌面的背景。

Figure 4-10:
自定义桌面的选项。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_109_2.png)

## 自定义 GNOME

到现在你可能已经跃跃欲试，想要做一些装饰。没有人喜欢坚持使用朴素的蓝色 GNOME 桌面。毕竟，这是你的桌面。你应该能够按自己想要的方式设置它。你可以通过从 Main Menu→Preferences 菜单中选择各种选项来配置 GNOME 桌面外观和行为的大多数方面。

### 更改背景

要了解桌面装饰的工作原理，请先选择 Main Menu→Preferences→Background，然后会出现一个对话框，如图 4-11 所示。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_110_0.png)

Figure 4-11: 更改 GNOME 桌面的背景。

从此对话框中，你可以选择纯色背景或颜色渐变背景，或选择壁纸（用作背景的图像）。颜色渐变背景从一种颜色开始，逐渐变为另一种颜色。渐变可以在垂直方向（从上到下）或水平方向（从左到右）进行。

要选择水平颜色渐变，请尝试以下步骤：

- 1. 从 Background Style 下拉框中——即当前显示为 Solid color 的那个（见图 4-11）——选择 Horizontal gradient。
- 2. 单击标签 Left Color 旁边的显示颜色的按钮。
这会打开一个颜色选择对话框（如图 4-12 所示），你可以在其中选择一种颜色。
- 3. 重复相同过程以选择右侧颜色。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_111_0.png)

Figure 4-12:
Pick a Color 对话框。

完成这些步骤后，对话框中监视器图像会显示新背景颜色的预览。

如果你想使用图像作为壁纸，请单击对话框左上角的 Select Picture 框。会显示一个对话框，其中包含 /usr/share/backgrounds/images 目录的内容。该目录具有 default.png 文件，其中包含你在 GNOME 桌面上看到的默认壁纸。要获取更多壁纸图像，请更改到目录 /usr/share/backgrounds/wallpapers 并选择你想要的图像。当你单击图像文件名时，你会看到该图像的预览（图 4-13）。你可以选择任何 Joint Photographic Experts Group（JPEG）或 Portable Network Graphics（PNG）格式的图像文件作为壁纸。选择图像后，单击 OK。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_111_1.png)

Figure 4-13:
从此对话框中选择要用作壁纸的图像。

新壁纸应立即出现在桌面上（如图 4-14 所示）。完成更改后，单击 OK 按钮关闭对话框并应用更改。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_112_0.png)

Figure 4-14:
新选择的壁纸。

### 选择主题

另一个更令人兴奋的自定义是为整个用户界面选择新主题。主题是指所有用户界面组件——按钮、复选框、滚动条等——的外观和行为（外观和感觉）的集合。

要尝试一些新主题，请选择 Main Menu→Preferences→Theme。从 Theme Preferences 对话框（见图 4-15）中，你可以尝试不同的主题并选择你喜欢的一个。默认主题称为 Bluecurve。要尝试另一个主题，请从列表中选择主题，桌面的外观将更改为与该主题相匹配。

继续尝试一些可用的主题。当你选择一个主题时，你可以在桌面和 Theme Preference 窗口本身中看到结果。如果你喜欢某个主题，请单击 Close 按钮使用该主题。否则，在单击 Close 之前选择 Bluecurve 主题。

## 注销 GNOME

如果你想尝试 KDE GUI，必须先注销。选择 Main Menu→Log out。当对话框询问是否真的要注销时，单击 Yes。



![](img/a7eec43a54473e95dc5ea333fecf1bd7_113_0.png)

图 4-15:
为桌面选择新主题。

## KDE

KDE 代表 K Desktop Environment（K 桌面环境）。KDE 项目始于 1996 年 10 月，旨在为使用 X Window System 的 UNIX 系统开发一个通用的 GUI。KDE 的第一个测试版于一年后 1997 年 10 月发布。KDE 1.0 版本于 1998 年 7 月发布；KDE 2.0 于 2000 年 10 月 23 日发布；KDE 3.0 于 2002 年 4 月 3 日发布；最新版本——KDE 3.1.2——于 2003 年 5 月 19 日发布。

从用户角度来看，KDE 提供了一个图形桌面环境，其中包括窗口管理器、Konqueror 网络浏览器和文件管理器、用于启动应用程序的面板、帮助系统、配置工具以及许多应用程序，包括 OpenOffice.org 办公套件、图像查看器、PostScript 查看器以及邮件和新闻程序。

从开发人员角度来看，KDE 拥有类库和对象模型，便于使用 C++ 进行应用程序开发。KDE 是一个拥有众多协作者的大型开发项目。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_113_1.png)

你可以随时通过访问 KDE 主页 www.kde.org 获取有关 KDE 的最新信息。

要尝试 KDE GUI，你必须在系统上安装 KDE。如果你没有安装 KDE，你可能一开始就不想要 KDE GUI。如果你系统上只安装了 KDE，你在登录后立即获得 KDE GUI。

如果你同时在系统上安装了 GNOME 和 KDE，你可以在登录前选择 GUI。从登录窗口，点击 Session，然后在弹出对话框（见图 4-16）中，选择 KDE 以进行 KDE 会话，然后像往常一样登录。对话框会询问是否要将 KDE 设为未来会话的默认值。根据你的喜好点击 Yes 或 No。

选择 KDE 会话后登录，你将获得此会话的 KDE 桌面。下次登录时，系统将继续使用 KDE，直到你切换回 GNOME 为止。

选择 KDE 作为会话的 GUI 并登录后，你应该会看到与图 4-17 所示类似的初始 KDE 桌面。初始 KDE 会话包含一个显示有用提示的窗口。这就是该桌面与你在 GNOME 中获得的桌面看起来不同的唯一部分。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_114_0.png)

图 4-16:
选择 KDE 会话。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_114_1.png)

图 4-17:
典型用户的初始 KDE 桌面。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_114_2.png)

你会发现 KDE 非常易于使用，并且在许多方面与 Windows GUI 相似。你可以从类似于 Windows 开始菜单的菜单启动应用程序。与 Windows 一样，你可以直接将文件夹和应用程序放置在 KDE 桌面上。

## KDE 面板

出现在屏幕底部边缘的 KDE 面板用于启动应用程序。面板的右端显示一个指向右方的箭头。你可以点击此箭头隐藏面板，为桌面上的应用程序腾出更多空间。当面板隐藏时，它仍显示一个带箭头的小条。要再次查看整个面板，点击该箭头，面板就会滑出。

面板最重要组件是面板左侧的 Red Hat 按钮。（在默认的 KDE 安装中，菜单显示为大写字母 K，但 Red Hat 已将其替换为 Red Hat 标志。）该按钮类似于 Windows 中的开始按钮。点击 Red Hat 按钮时，会出现一个弹出菜单。从此菜单中，你可以通过将鼠标指针移到显示右向箭头的项目上来访问其他菜单。例如，图 4-18 显示了更改桌面背景的典型菜单选择。

图 4-18：点击 Red Hat（主菜单）按钮，然后将鼠标指针从一个菜单移到另一个菜单以打开 KDE 菜单。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_115_0.png)

你可以从此菜单启动应用程序。这就是为什么 KDE 文档将 Red Hat 按钮（当然，KDE 文档称该按钮为 K 按钮）称为应用程序启动器的原因。

Red Hat 按钮旁边，面板还包含许多其他按钮。如果你不知道某个按钮的作用，只需将鼠标指针移到该按钮上；一个小弹出窗口会显示关于该按钮的简短信息。

表 4-1 让你了解点击 KDE 面板上每个主要按钮时会发生什么。找点时间逐一尝试这些按钮，以感受你在 KDE 中可以做的事情。

**表 4-1 KDE 面板按钮**

| 当你点击这个 | 它执行此操作 |
|---|---|
| [帽子图标] | 显示应用程序菜单，从中可以启动任何应用程序。 |
| [头盔图标] | 启动 Mozilla 网络浏览器。 |
| [信封 / 记事本图标] | 启动 Ximian Evolution 电子邮件和日历软件。 |
| [带铅笔的文档图标] | 运行 OpenOffice.org Writer，一款类似 Microsoft Word 的文字处理器。 |
| [演示 / 监视器图标] | 运行类似 Microsoft PowerPoint 的 OpenOffice.org Impress 幻灯片演示程序。 |
| [电子表格 / 磁盘图标] | 运行类似 Microsoft Excel 的 OpenOffice.org Calc 电子表格程序。 |
| [打印机图标] | 运行打印管理器，一种用于设置和监控打印队列的实用程序。 |
| [桌面切换器 1 2 3 4 图标] | 切换到你点击的编号的桌面。 |
| [剪贴板 / Klipper 图标] | 运行 Klipper，KDE 用于剪切和粘贴信息的剪贴板实用程序。 |
| 20:42 | 显示当前时间。点击以查看当前月份的日历。右键单击菜单以调整日期和时间。 |

## 自定义 KDE 桌面

KDE 使自定义 KDE 桌面的外观和感觉变得非常容易。装饰桌面的所有内容都在一个地方：KDE 控制中心。要启动 KDE 控制中心，选择主菜单：控制中心。

KDE 控制中心启动时，会显示主窗口，左侧为树形菜单，右侧工作区显示有关系统的一些摘要信息，如图 4-19 所示。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_117_0.png)

图 4-19:
KDE 控制中心的初始窗口。

KDE 控制中心树形菜单显示了你可以用此程序自定义的项目。树形菜单按类别组织，例如外观和主题、互联网和网络、外设、安全和隐私等。点击项目左侧的加号 (+) 以查看该项目的子类别。要更改项目，请通过树形菜单找到该项目然后点击它。该项目的配置选项随后会出现在窗口右侧的选项卡对话框中。

### 更改背景

要更改桌面的背景，选择外观和主题→背景。会出现一个选项卡（如图 4-20 所示），显示自定义桌面背景的选项。

如果你想更改特定桌面的背景，请取消选择“通用背景”复选框（以移除勾选标记）。然后，从桌面列表中选择你想要更改背景的桌面。

你可以选择纯色背景（带多种渐变，即颜色从一种颜色逐渐变化到另一种颜色）或壁纸（用作背景的图像）。对于纯色背景，你可以从“模式”下拉菜单中选择渐变。然后，你可以通过点击“颜色 1”和“颜色 2”颜色按钮来选择两种颜色。做出选择后，点击“应用”以试用背景。（如果不喜欢结果，点击“重置”以恢复到之前的背景。）

如果你想使用壁纸作为背景，点击“壁纸”选项卡进行壁纸选择。然后点击“浏览”按钮。这会弹出一个对话框，显示 /usr/share/backgrounds/wallpapers 目录中的 JPEG 图像。你可以选择其中任意一张图像并点击“确定”。然后在 KDE 控制中心点击“应用”按钮将此壁纸应用到桌面。如果不喜欢外观，点击“重置”。

### 选择主题

如 KDE 控制中心“外观和主题”类别中的菜单项所示（参见图 4-20），你可以自定义许多外观和感觉方面的内容，从颜色和字体到图标。我不会在这里逐一介绍所有项目，但你应该尝试一些项目，看看你想要什么样的 KDE 桌面。

选择一种打包的外观和感觉的一种快速简便的方法是使用主题管理器提供的主题之一。要选择主题，选择外观和主题→主题管理器。这会打开主题管理器选择，你可以点击主题名称并查看该主题的预览，如图 4-21 所示。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_118_0.png)

图 4-20:
使用 KDE 控制中心更改桌面背景。



![](img/a7eec43a54473e95dc5ea333fecf1bd7_119_0.png)

图 4-21:
在 KDE 控制中心中选择和预览主题。

要尝试一个主题，请单击“应用”。如果不喜欢，可以单击“重置”以恢复到当前的显示效果。

## 从 KDE 注销

当您探索完 KDE 后，请注销。要从 KDE 注销，请选择 K→注销。您也可以右键单击桌面空白区域，然后从出现的弹出菜单中选择“注销”。

## 玩转 Shell

Red Hat Linux 基本上是 UNIX，而除非您能在文本终端中输入晦涩的命令，否则 UNIX 就感觉不像 UNIX。虽然 GNOME 和 KDE 做了很多工作让我们进入窗口、图标、鼠标和指针的世界（亲切地称为 WIMP :-)），有时您只能面对一个纯文本屏幕，提示符看起来像这样（以 root 登录时）：

```
[root@dhcppc4 etc]#
```

这种情况最常见于 X Window System 出了问题，而 X Window System 本质上就是运行您通常看到的窗口和菜单的机制。在这种情况下，您必须使用 shell 并学习一些晦涩的 Linux 命令。

您可以通过在 GNOME 或 KDE 图形界面中于终端窗口尝试一些 Linux 命令来为意外的 shell 遭遇做好准备。熟练之后，您甚至可以一直保持终端窗口打开，只是为了使用其中一个晦涩的命令，因为它比尝试指向和点击更快（那些双字母命令确实威力十足！）。

## 启动 Bash shell

简单来说，shell 是 Linux 命令解释器——一个程序，它读取您输入的内容，将该文本解释为命令，并执行命令应做的事情。

在开始玩转 shell 之前，请打开一个终端窗口。在 GNOME 或 KDE 中，选择“主菜单→系统工具→终端”。出现的窗口带有一个提示符，如图 4-22 所示。这就是终端窗口，它的工作方式就像老式终端一样。shell 程序正在运行并准备接受您输入的任何文本。您输入文本，按 Enter，事情就会发生（取决于您输入的内容）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_120_0.png)

图 4-22: 您可以在终端窗口的 shell 提示符处输入 Linux 命令。

您看到的提示符取决于该终端窗口中运行的 shell。默认的 Linux shell 称为 Bash。

Bash 理解大量标准 Linux 命令，您可以用它们查看文件、从一个目录切换到另一个目录、查看正在运行的程序（以及还有谁登录），等等。

除了 Linux 命令外，Bash 还可以运行存储在可执行文件中的任何程序。Bash 还可以执行 shell 脚本，即包含 Linux 命令的文本文件。

## 理解 shell 命令

由于 shell 会解释您输入的内容，因此了解 shell 如何解析您输入的文本非常重要。所有 shell 命令都有以下通用格式：

```
command option1 option2 ... optionN
```

这样的一行命令通常称为命令行。在命令行中，您输入一个命令，后跟一个或多个可选参数（或参数）。这些命令行选项（或命令行参数）有助于指定您希望命令执行的操作。

一个基本规则是，您必须使用空格或制表符将命令与选项分隔开。您还必须用空格或制表符分隔选项。如果您想使用包含嵌入空格的选项，必须将该选项放在引号内。例如，要在密码文件中搜索两个单词的文本，我输入以下 grep 命令（grep 是用于在文件中搜索文本的那些晦涩命令之一）：

```
grep "Font Server" /etc/passwd
```

当 grep 打印包含这些单词的行时，它看起来像这样：

```
xfs:x:43:43:X Font Server:/etc/X11/fs:/sbin/nologin
```

如果您以自己的名字创建了用户账户，请继续输入 grep 命令并将您的名字作为参数，但请记住将名字用引号括起来。

## 尝试一些 Linux 命令

在终端窗口打开时，试着为好玩执行几个 Linux 命令。我将引导您完成一些随机示例，让您感受在 shell 提示符下可以做什么。

要查看 Red Hat Linux PC 自上次开机以来运行了多长时间，请输入以下内容。（注意：我以粗体显示输入的命令，后跟该命令的输出。）

```
uptime
```

```
7:13pm up 29 days, 55 min, 3 users, load average: 1.00, 1.00, 1.00
```

部分 up 29 days, 55 min 告诉您这台特定 PC 已运行近一个月。嗯……Windows 能做到吗？

要查看系统运行的 Linux 内核版本，请使用 uname 命令，如下所示：

```
uname -srv
```

```
Linux 2.4.21-20.1.2024.2.1.nptl #1 Fri Jul 11 06:04:52 EDT 2003
```

在这种情况下，系统运行的是 Linux 内核版本 2.4.21。

要读取文件，请使用 more 命令。以下是一个示例：

```
more /etc/passwd
```

```
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
... lines deleted ...
```

要查看系统当前运行的所有程序的列表，请使用 ps 命令，如下所示：

```
ps ax
```

```
PID TTY   STAT   TIME COMMAND
1 ?       S      0:04 init
2 ?       SW     0:00 [keventd]
3 ?       SW     0:00 [kapmd]
4 ?       SWN    0:00 [ksoftirqd_CPU0]
5 ?       SW     0:44 [kswapd]
6 ?       SW     0:00 [bdflush]
7 ?       SW     0:00 [kupdated]
8 ?       SW     0:00 [mdrecoveryd]
12 ?      SW     0:17 [kjournald]
91 ?      SW     0:00 [khubd]
194 ?     SW     0:00 [kjournald]
604 ?     S      0:04 syslogd -m 0
609 ?     S      0:00 klogd -x
629 ?     S      0:00 portmap
657 ?     S      0:00 rpc.statd
... lines deleted ...
```

即使只有您作为用户登录，系统上也能运行如此多程序，真是令人惊讶，不是吗？

正如您所猜测的那样，您可以从 shell 提示符执行所有操作，但确实需要一些时间来适应。

## 关闭系统

当您准备关闭 Red Hat Linux 时，必须有序地进行。即使您是 Red Hat Linux PC 的唯一用户，后台通常仍在运行多个其他程序。此外，像 Linux 这样的操作系统会尝试优化写入磁盘的方式。由于磁盘访问相对较慢（与访问内存位置所需的时间相比），数据通常保存在内存中并以大块写入磁盘。因此，如果您直接关闭电源，就有风险某些文件不会被正确更新。

任何用户（您甚至不必登录）都可以从桌面或图形登录屏幕关闭系统。选择“主菜单”。会出现一个“注销”对话框，提供重新启动或停止系统或简单注销的选项。要关闭系统，只需选择“关机”，然后单击“确定”。系统随后会有序地关闭。

如果您在图形登录屏幕上，请单击屏幕底部部分的“关机”标签。然后会出现另一个对话框，要求您确认是否真的要停止系统。单击“是”按钮。系统随后会有序地关闭。

随着系统关闭，您会看到有关进程正在关闭的消息。即使没有人明确运行任何程序，您可能会惊讶于进程的数量之多。如果系统在关机时不会自动断电，您可以手动关闭电源。

请注意，以这种方式关闭或重新启动系统不需要 root 权限。请确保控制台的物理访问得到充分保护。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_123_0.png)

## 第二部分

## 工作站和应用程序

## 第五波

作者 Rich Tennant

© RICH TENNANT

![](img/a7eec43a54473e95dc5ea333fecf1bd7_124_0.png)

> "这款软件真的相当有趣。有过山车般的刺激、悬念和戏剧性，技巧和策略在胜负之间较量。而我本以为管理我们的预算会很枯燥。"



## 内容一览

- 第 1 章：探索 GNOME..................................................99
- 第 2 章：探索 KDE..................................................119
- 第 3 章：学习 Shell..................................................141
- 第 4 章：浏览 Red Hat Linux 文件系统..................................................161
- 第 5 章：探索 Red Hat Linux 应用程序..................................................177
- 第 6 章：使用文本编辑器..................................................209

### 第 1 章：探索 GNOME

### 本章内容

- ✓ 了解 GNOME 概况
- ✓ 使用 GNOME 面板
- ✓ 检查主菜单
- ✓ 运行小程序
- ✓ 使用 Nautilus Shell
- ✓ 配置 GNOME

GNOME（发音为 Guh-NOME）是 Red Hat Linux 的 GUI。GNOME 与 Microsoft Windows 相似，但也有其不同之处。与 Microsoft Windows 不同，您可以在 Red Hat Linux 中选择 GUI。如果您不喜欢 GNOME，只需注销并使用 KDE（另一个 GUI）重新登录即可。试试在 Microsoft Windows 上这样做吧！

了解 GNOME 的最佳方式是以用户身份探索它。在本章中，我将为您简要介绍 GNOME。然后，您可以在继续使用 GNOME 的过程中继续探索并学习更多内容。

顺便说一下，GNOME 是独立于 Linux 开发的。事实上，GNOME 还可以在除 Linux 之外的其他 UNIX 操作系统上运行。访问 GNOME 主页 www.gnome.org 了解 GNOME 的最新信息。

### 了解 GNOME 概况

使用 GNOME 时，您所看到和体验到的全部是 GUI 桌面。然而，GNOME 远不止 GUI 桌面。例如，这里是关于 GNOME 的一些关键事实：

- ♦ GNOME 为 GUI 应用程序提供开发环境。它附带一套编程工具包，程序员可以使用它来创建 GUI 应用程序。
- ♦ GNOME 支持对象模型——它定义了软件组件的结构，以便它们能够相互通信。
- GNOME GUI 是模块化的，因此它可与为 X Window System 设计的任何窗口管理器配合使用。例如，Red Hat Linux 附带了多个窗口管理器，如 Metacity、MWM 和 TWM。每个窗口管理器都有自己的外观和感觉。GNOME 可与这些窗口管理器中的任何一个配合使用。
- 所有 GNOME 文档均使用标准通用标记语言（SGML）编写。这意味着您可以在任何 Web 浏览器上查看 GNOME 应用程序的手册。
- GNOME 附带了一套名为 OpenOffice.org 的办公应用程序。它包括 Writer 文字处理器、Calc 电子表格、Impress 演示程序和 Draw 绘图程序。有关 OpenOffice.org 的更多信息，请参阅第三册。

好吧，我想你明白了。GNOME 在那漂亮的外表下是一个强大的工作马。

### GNOME 桌面

通常，GNOME 是 Red Hat Linux 中的默认 GUI；如果您登录时未选择特定 GUI，则会获得 GNOME 桌面。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_127_0.png)

如果您的系统上同时安装了 GNOME 和 KDE，您可以在登录前选择想要使用的 GUI。从图形登录窗口中，选择 Session: GNOME 以选择 GNOME 会话，然后照常登录。

初始 GNOME 桌面（如图 1-1 所示）看起来像任何其他流行的 GUI，例如 Microsoft Windows 或 Mac 上的 Apple 桌面。

桌面显示您文件夹的图标、已删除文件的废纸篓图标以及 CD-ROM 驱动器中任何 CD-ROM 的图标。双击“Start Here”图标即可启动 Nautilus 文件管理器。

GNOME 桌面的另一个主要功能是底部的栏，被称为 GNOME 面板或简称面板。面板类似于 Windows 任务栏。左侧有按钮（各种程序的快捷方式），右侧显示日期和时间。面板中间部分显示您可能正在运行的应用程序的按钮。

### 桌面弹出菜单

右键单击 GNOME 桌面上的空白区域，即会出现一个菜单（如图 1-2 所示）。

您可以使用这些菜单选项执行多项任务——从打开 Nautilus 窗口到更改桌面背景。表 1-1 解释了每个菜单选项的作用。菜单项为灰色表示不适用。不妨试试这些菜单选项中的一些。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_128_0.png)

图 1-1：
GNOME 桌面看起来像其他流行的 GUI 桌面。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_128_1.png)

图 1-2：
右键单击 GNOME 桌面即可弹出此菜单。

表 1-1 GNOME 桌面菜单选项

| 当您选择此选项时 | 其作用如下 |
|---|---|
| 打开新窗口 | 打开一个新的 Nautilus 窗口，显示您的主目录（文件夹）。 |
| 打开新终端 | 打开一个终端窗口，您可以在其中输入 Linux 命令。 |
| 创建文件夹 | 在桌面上创建新文件夹并等待您编辑文件夹的名称。 |
| 创建启动器 | 弹出一个对话框，您可以在其中设置新的启动器——桌面上的一个图标，可作为应用程序的快捷方式。 |
| 按名称整理 | 按名称按字母顺序排列桌面图标。 |
| 保持对齐 | 选中后，将桌面图标对齐。 |
| 粘贴文件 | 将文件粘贴到桌面（图标随后出现）。 |
| 磁盘 | 弹出可移动驱动器和 CD-ROM 驱动器的菜单，您可以从中选择要访问的驱动器。 |
| 使用默认背景 | 将桌面背景重置为默认值。 |
| 更改桌面背景 | 弹出一个对话框，您可以从中选择新的背景。 |

### 图标弹出菜单

右键单击任何桌面图标都会导致另一个菜单出现。此弹出菜单有一些适用于任何图标的选项，但最后一个选项取决于所单击的图标。例如，图 1-3 显示了右键单击废纸篓图标时出现的菜单。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_129_0.png)

图 1-3：
右键单击 GNOME 桌面上的图标即可弹出此类型的菜单。

请注意，最后一个选项是“清空废纸篓”，这对于废纸篓图标是合适的。表 1-2 概述了图标弹出菜单中的常见菜单选项。正如您所料，不适用于图标的菜单项为灰色。

表 1-2 GNOME 图标菜单选项

| 当您选择此选项时 | 其作用如下 |
|---|---|
| 打开 | 打开文件（通常在 Nautilus 窗口中）。 |
| 使用...打开 | 使用查看器或应用程序打开文件（由您选择）。 |
| 剪切文件 | 剪切所选文件。 |
| 复制文件 | 复制所选文件。 |
| 创建链接 | 创建该图标的链接（链接是快捷方式）。 |
| 重命名 | 重命名图标（您必须输入新名称）。 |
| 移至废纸篓 | 将图标移至废纸篓。 |
| 拉伸图标 | 拉伸图标（您必须拖动鼠标以指示新大小）。 |
| 恢复图标原始大小 | 将图标恢复到之前的大小。 |
| 添加到归档 | 显示一个对话框，允许您使用 GNOME File Roller 应用程序将废纸篓中的项目添加到归档中（仅在单击文件或文件夹图标时出现）。 |
| 属性 | 显示有关图标的信息。 |
| 清空废纸篓 | 永久删除废纸篓中的项目（您有机会选择是或否）——此项目仅在右键单击废纸篓图标时出现。 |

![](img/a7eec43a54473e95dc5ea333fecf1bd7_130_0.png)

好吧。你看出了这里的规律吗？我敢打赌你看出来了。无论您是在探索 GNOME（或者说任何 GUI），在选择之前始终右键单击。您会惊讶于右键单击时弹出的菜单可以完成各种各样的操作！

### 使用 GNOME 面板

GNOME 面板，或简称面板，是横跨 GNOME 桌面底部的长方形窗口。图 1-4 显示了面板的典型视图。



Figure 1-4:
这是 GNOME 面板的典型视图。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_131_0.png)

面板是图标的停放处。点击其中一些可以启动程序。有些显示状态（如当前正在运行的程序），以及日期和时间等信息。

从左侧开始，Red Hat 图标是 GNOME 的主菜单按钮——它类似于 Microsoft Windows 中的“开始”按钮。随后是一些启动各种程序的图标。表 1-3 简要说明了这些图标的作用。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_131_1.png)

顺便说一下，如果将鼠标指针移到图标上方，会弹出一个小帮助气泡，提供有关该图标的有用提示。

表 1-3 GNOME 面板上的图标

| 点击此图标时 | 其执行以下操作 |
|---|---|
| 帽子图标 | 弹出主菜单，从中可选择要运行的应用程序。 |
| 地球图标 | 运行 Mozilla Web 浏览器。 |
| 笔记本图标 | 启动 Ximian Evolution 电子邮件和日历软件。 |
| 文档图标 | 运行 OpenOffice.org Writer，一款类似 Microsoft Word 的文字处理器。 |
| 演示文稿图标 | 运行 OpenOffice.org Impress 幻灯片演示程序（类似于 Microsoft PowerPoint）。 |
| 电子表格图标 | 运行 OpenOffice.org Calc，一款类似 Microsoft Excel 的电子表格程序。 |
| 打印机图标 | 运行 GNOME 打印管理器，可从中设置和监控打印机。 |

在这些图标的右侧，工作区切换器图标显示四个矩形区域，每个区域代表一个虚拟桌面。你可以点击其中一个矩形切换到不同的虚拟桌面。此功能似乎提供了四个独立的桌面供使用。说实话，我似乎一直停留在同一个虚拟屏幕上，但知道其他虚拟桌面在那里，以备不时之需，很不错。

分页器图标右侧的区域显示迄今为止已启动程序的按钮。如果尚未启动任何程序，此区域为空。

分页器旁边可能还有其他图标，但日期和时间始终出现在面板的最右侧边缘。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_132_0.png)

现在来谈谈面板上这些图标的一些技术细节。面板本身是一个 GNOME 应用程序；每个图标都是一个名为 applet（小应用程序）的程序。这些面板小程序可以执行诸如启动其他程序或显示日期和时间等操作。

如果右键单击任何图标或面板上的任何位置，会弹出一个菜单，可从中了解更多信息或执行某些任务。例如，如果右键单击从左数第二个图标，则会弹出图 1-5 所示的菜单。如你所见，你可以从弹出菜单中执行诸如从面板中移除图标、在面板上移动图标以及查看其属性等任务。如果右键单击面板的空白区域，甚至可以访问菜单以启动任何程序。

## 主菜单

就像任何自尊的 GUI 一样，GNOME 重视便利性和易用性。事实上，它提供了一个地方，你可以在其中找到并启动 Red Hat Linux 中想要运行的一切。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_132_1.png)

GNOME 面板上的 Red Hat 图标是 Red Hat Linux 的主菜单按钮。我不会用冗长的列表来让你厌烦主菜单中的所有内容；相反，我提供一个概述并指出一些有趣的项目。你可以自己探索。

图 1-5：右键单击 GNOME 面板上的图标以查看其弹出菜单。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_132_2.png)

单击主菜单按钮以调出初始菜单。然后将指针移到菜单项旁边的箭头上以调出下一个菜单，依此类推。你可以浏览菜单层次结构并从最终菜单中进行选择。如果将光标定位在菜单项上，小帮助气泡可能会提供有关该项的更多信息。图 1-6 显示了一个典型的菜单层次结构，显示了对网络浏览器的选择。请注意在 Mozilla Web Browser 菜单项旁边的矩形小窗口中出现的气泡帮助。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_133_0.png)

你无论如何也会猜到，但还是说一下。我使用表示法 Main Menu→Internet→Mozilla Web Browser 来表示用于选择网络浏览器的菜单选择序列，如图 1-6 所示。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_133_1.png)

图 1-6：
单击主菜单按钮并将鼠标悬停以查看程序菜单。

作为层次结构中的第一个菜单，“程序”项可让你访问 Red Hat Linux 中的所有应用程序和实用程序。它们按在下一个菜单窗格中看到的菜单类别进行组织：

- **附件：** 此菜单可让你访问诸如计算器、词典、文件归档管理器、文本编辑器以及用于与 Palm 或 Handspring 个人数字助理（PDA）同步的工具等实用程序。
- **游戏：** 此菜单有一系列——还有什么？——游戏。
- **图形：** 此菜单具有诸如 The GIMP（类似 Adobe Photoshop 的程序）、数码相机接口、扫描仪接口和 Adobe Acrobat 查看器等程序。
- **Internet：** 此菜单用于 Internet 应用程序，如 Mozilla Web 浏览器、Ximian Evolution 电子邮件和个人信息管理（PIM）软件以及 Gaim AOL 即时通讯客户端。
- **办公：** 此菜单调出 OpenOffice.org 办公应用程序菜单，其中包括 Writer 文字处理器、Calc 电子表格、Draw 绘图程序、Impress 幻灯片演示程序以及其他几个应用程序。
- **首选项：** 此菜单具有可用于配置 GNOME 桌面各个方面的实用程序。
- **编程：** 此菜单可让你启动一些软件开发工具，如程序员编辑器（Emacs）。
- **声音和视频：** 此菜单具有多媒体应用程序，如 CD 播放器、声音记录器和音量控制。
- **系统设置：** 此菜单具有系统配置实用程序，可用于执行许多系统管理任务，如添加用户帐户和设置日期和时间。
- **系统工具：** 这是找到系统管理实用程序的菜单，如软盘格式化程序、系统监视器、Internet 配置向导、系统日志查看器和终端。

系统设置还可让你访问“服务器设置”子菜单；在这里你可以配置和管理服务器——如 Web 服务器、域名系统（DNS）服务器和网络文件系统（NFS）服务器。你还可以配置各种服务器在系统启动时自动启动。

主菜单上的其他菜单项用于一些常见任务。它们的作用如下：

- **主菜单→帮助** 调出 GNOME 帮助浏览器。
- **主菜单→主文件夹** 在 Nautilus 文件管理器中打开你的主目录。
- **主菜单→网络服务器** 在 Nautilus 文件管理器中显示你的网络服务器。你可以从此 Nautilus 窗口访问网络上的任何 Windows 服务器。
- **主菜单→运行程序** 显示一个对话框，你可以在其中输入要运行的程序的名称，然后单击“运行”以启动该程序。
- **主菜单→搜索文件** 运行一个搜索工具，可从中搜索文件。
- **主菜单→锁定屏幕** 启动屏幕保护程序并锁定屏幕。
- **主菜单→注销** 注销你的登录（你有机会确认是否真的要注销）。

好吧。这就是我要告诉你的全部内容。随着你使用 Red Hat Linux，你会经常使用主菜单。即使起初看起来太多，随着你花更多时间使用 Red Hat Linux，一切都会变得非常熟悉。

## 小程序

小程序是运行在 GNOME 面板内部的小程序。这意味着小程序执行一些有用的任务，然后在面板上显示一些有趣的信息。例如，面板右侧边缘的日期和时间显示是 Clock 小程序的输出。你可以从右键单击面板空白区域时出现的菜单中启动一个小程序。当你想监视某些信息或只是想要一种方便的方式来运行某些应用程序时，小程序非常方便。

一个有趣的实用小程序是 Weather Report。假设你的 Red Hat Linux PC 有 Internet 连接，此小程序会下载天气并显示出来。你可以在小程序中设置你的地理位置。

要将 Weather Report 小程序添加到面板，请右键单击面板的空白区域并选择 添加到面板→附件→Weather Report。图 1-7 显示了从中选择 GNOME Weather Report 的菜单。

图 1-7：
你可以通过右键单击 GNOME 面板并选择“添加到面板”来选择小程序。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_135_0.png)

Weather Report 小程序运行后，它最初出现在面板空白区域的中间。右键单击图标并选择“移动”。然后你可以将其定位到面板上的所需位置。

要在 Weather report 小程序中设置地理位置，请右键单击并选择“首选项”。Weather Preferences 菜单出现，如图 1-8 所示。



Figure 1-8:
从“天气首选项”菜单设置地理位置。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_136_0.png)

对于美国地区，向下滚动到您的州并单击加号。然后从列表中选择您的位置并单击确定。然后右键单击 GNOME 天气报告小程序图标并选择更新。小程序现在应显示您所在位置的天气。图 1-9 显示了天气报告小程序的典型天气显示。

Figure 1-9:
天气报告小程序在面板上显示天气信息。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_136_1.png)

![](img/a7eec43a54473e95dc5ea333fecf1bd7_136_2.png)

如果您不再想要该小程序，请右键单击并从菜单中选择“从面板中移除”。

GNOME 还有许多更多的小程序（事实上超过 20 个）可供尝试。几乎形成了一个小程序的“小作坊”产业。例如，请参阅图 1-7：第一个菜单显示了五类小程序以及一些按钮小程序，例如注销按钮和锁定按钮。表 1-4 为您提供了这些类别中小程序的概览。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_136_3.png)

如果表 1-4 中列出的任何小程序引起您的兴趣，请尽管尝试。要查找小程序，请右键单击面板的空白区域，选择“添加到面板”，然后在适当的类别菜单中查找。

Table 1-4 GNOME Applets
表 1-4 GNOME 小程序

| Applet | What It Does |
| 小程序 | 其功能 |
|---|---|
| *Accessories* | |
| *附件* | |
| Clock | Displays the current time (and date, when you mouse over the applet). |
| 时钟 | 显示当前时间（将鼠标悬停在小程序上时显示日期）。 |
| Dictionary Lookup | Displays a small text input area and a Lookup button so you can type a word and look up its meaning by using the GNOME Dictionary program. |
| 词典查找 | 显示一个小的文本输入区域和一个查找按钮，以便您可以通过使用 GNOME 词典程序输入单词并查找其含义。 |
| Stock Ticker | Displays stock quotes in a scrolling stock ticker. |
| 股票行情 | 在滚动的股票行情中显示股票报价。 |
| Weather Report | Displays weather information. |
| 天气报告 | 显示天气信息。 |
| *Amusements* | |
| *娱乐* | |
| Fish | Displays a small fish. |
| 鱼 | 显示一条小鱼。 |
| Geyes | A pair of eyes that follows your mouse around the screen. |
| Geyes | 屏幕上的一对眼睛会跟随您的鼠标。 |
| *Internet* | |
| *互联网* | |
| Inbox Monitor | Checks for e-mail and lets you know when you have new mail. |
| 收件箱监视器 | 检查电子邮件并在您有新邮件时通知您。 |
| Modem Lights | Provides an interface for dialing out with the modem and viewing status information about the modem when you're using it. |
| 调制解调器指示灯 | 提供使用调制解调器拨号以及在您使用时查看调制解调器状态信息的界面。 |
| Terminal Server Client | Runs an application that can connect as a client to Microsoft Windows 2000 Terminal Server and display a remote desktop from that server (available only if you install the tsclient package). |
| 终端服务器客户端 | 运行一个可以作为客户端连接到 Microsoft Windows 2000 终端服务器并显示该服务器远程桌面的应用程序（仅在安装 tsclient 软件包时可用）。 |
| Wireless Link Monitor | Displays the status of your PC's wireless link, provided you have a wireless link up and running. |
| 无线链路监视器 | 在您已建立并运行无线链路的情况下显示您 PC 无线链路的状态。 |
| *Multimedia* | |
| *多媒体* | |
| CD Player | Provides the user interface for a CD player. |
| CD 播放器 | 提供 CD 播放器的用户界面。 |
| Volume Control | Provides an interface for controlling sound volume and launching an audio mixer application. |
| 音量控制 | 提供控制音量和启动音频混音器应用程序的界面。 |
| *Utility* | |
| *实用工具* | |
| Battery Charge Monitor | Displays the charge status of your laptop's battery (so this applet is for laptops only). |
| 电池电量监视器 | 显示笔记本电脑电池的充电状态（因此此小程序仅适用于笔记本电脑）。 |
| Character Palette | Shows accented versions of a character (you type the character) so that you can copy and paste it into documents. |
| 字符调色板 | 显示字符的重音版本（您输入字符），以便您可以将其复制并粘贴到文档中。 |
| Command Line | Adds a small command line where you can type Linux commands. |
| 命令行 | 添加一个小的命令行，您可以在其中输入 Linux 命令。 |
| Disk Mounter | Displays a disk drive icon that you can click to access a drive. |
| 磁盘挂载器 | 显示一个磁盘驱动器图标，您可以单击它来访问驱动器。 |
| Keyboard Layout Switcher | Displays an icon through which you can switch the keyboard layout from one country to another. |
| 键盘布局切换器 | 显示一个图标，通过它您可以将键盘布局从一个国家切换到另一个国家。 |
| *Utility* | |
| *实用工具* | |
| Notification Area | Sets up an area where notification icons appear. |
| 通知区域 | 设置一个区域，在该区域中显示通知图标。 |
| Pilot Applet | Displays an icon for synchronizing your Palm Pilot with the Red Hat Linux system. |
| Pilot 小程序 | 显示用于将 Palm Pilot 与 Red Hat Linux 系统同步的图标。 |
| Show Desktop Button | Displays a button that lets you hide all windows and show the desktop. |
| 显示桌面按钮 | 显示一个按钮，可让您隐藏所有窗口并显示桌面。 |
| System Monitor | Shows you how busy your PC is. |
| 系统监视器 | 显示您的 PC 的繁忙程度。 |
| Window List | Displays buttons for each of the running applications. |
| 窗口列表 | 为每个正在运行的应用程序显示按钮。 |
| Workspace Switcher | Displays a rectangle that contains four small rectangular areas, each representing a virtual desktop that you can click to switch to that virtual desktop. |
| 工作区切换器 | 显示一个矩形，其中包含四个小的矩形区域，每个区域代表一个虚拟桌面，您可以单击它来切换到该虚拟桌面。 |
| *Launchers* | |
| *启动器* | |
| Launcher... | Brings up a dialog box from where you can set up a new launcher — an icon on the panel that acts as a shortcut to an application. |
| Launcher... | 弹出一个对话框，您可以在其中设置新的启动器——面板上的一个图标，可作为应用程序的快捷方式。 |
| Launcher from menu | Provides access to the entire Main Menu hierarchy from which you can pick a program and create a launcher for that program on the panel. |
| 从菜单启动 | 提供对整个主菜单层次结构的访问，您可以从中选择一个程序并在面板上为该程序创建启动器。 |
| *Other* | |
| *其他* | |
| Button | Brings up a list from which you can select a button to add to the panel (the buttons enable the user to perform specific tasks such as log out, lock the screen, take a screenshot, perform a search, and run a command). |
| 按钮 | 弹出一个列表，您可以从中选择一个按钮添加到面板（按钮使用户能够执行特定任务，例如注销、锁定屏幕、截屏、执行搜索和运行命令）。 |
| Main Menu | Adds a Main Menu button to the panel (this is the Red Hat button from which you can access the entire menu hierarchy and start any application). |
| 主菜单 | 在面板上添加主菜单按钮（这是 Red Hat 按钮，您可以从中访问整个菜单层次结构并启动任何应用程序）。 |
| Drawer | Adds a drawer, which acts as a storage area for other applets (it looks like a real drawer — you can open and close it by clicking). |
| 抽屉 | 添加一个抽屉，可作为其他小程序的存储区域（它看起来像一个真正的抽屉——您可以通过单击打开和关闭它）。 |

## Using the Nautilus Shell
## 使用 Nautilus Shell

The Nautilus file manager, or more accurately graphical shell, is intuitive to use — it's similar to the Windows Active Desktop. You can manage files and folders and also manage your system with Nautilus.
Nautilus 文件管理器，或更准确地说图形 shell，使用起来很直观——它类似于 Windows Active Desktop。您可以使用 Nautilus 管理文件和文件夹，也可管理您的系统。

### Viewing files and folders
### 查看文件和文件夹

When you double-click a file or a folder, Nautilus starts automatically. For example, double-click the home icon in the upper-left corner of the GNOME desktop. Nautilus runs and displays the contents of your home directory
(think of a directory as a folder that can contain other files and folders). If you want to see the folders you're browsing, choose View→Side Pane from the Nautilus menu. Figure 1-10 shows a typical user's home directory in the Nautilus file manager after you choose View→Side Pane.
当您双击文件或文件夹时，Nautilus 会自动启动。例如，双击 GNOME 桌面左上角的主目录图标。Nautilus 运行并显示您主目录的内容（将目录视为可包含其他文件和文件夹的文件夹）。如果您想查看正在浏览的文件夹，请从 Nautilus 菜单中选择“查看→侧边窗格”。图 1-10 显示了在选择“查看→侧边窗格”后 Nautilus 文件管理器中典型用户的主目录。

With the side pane open, the Nautilus window is vertically divided into two parts. The left window shows different views of the file system and other objects that you can browse with Nautilus. The right window shows the files and folders in the currently selected folder in the left window. Nautilus displays icons for files and folders. For image files, it shows a thumbnail of the image.
打开侧边窗格时，Nautilus 窗口垂直分为两部分。左侧窗口显示文件系统的不同视图以及您可以使用 Nautilus 浏览的其他对象。右侧窗口显示左侧窗口中当前所选文件夹中的文件和文件夹。Nautilus 为文件和文件夹显示图标。对于图像文件，它显示图像的缩略图。

The Nautilus window's title bar shows the name of the currently selected folder. The Location text box along the top of the window shows the full name of the directory in Linuxspeak — in this case, Figure 1-10 is showing the contents of the /home/naba directory.
Nautilus 窗口的标题栏显示当前所选文件夹的名称。窗口顶部的“位置”文本框显示目录在 Linux 术语中的全名——在本例中，图 1-10 显示的是 /home/naba 目录的内容。

If you have used Windows Explorer, you can use Nautilus in a similar manner. To view the contents of another directory, do the following:
如果您使用过 Windows 资源管理器，您可以以类似的方式使用 Nautilus。要查看另一个目录的内容，请执行以下操作：

- 1. **Choose Tree from the Information drop-down menu (located in the left window).**
  - 1. **从信息下拉菜单中选择树（位于左侧窗口）。**
  A tree menu of directories appears in that window. Initially the tree shows the root directory as a folder labeled /.
  目录的树状菜单出现在该窗口中。最初，树将根目录显示为标记为 / 的文件夹。
- 2. **Click the right arrow next to the / folder; in the resulting tree view, locate the directory you want to browse.**
  - 2. **单击 / 文件夹旁边的右箭头；在 resulting 树视图中，找到您要浏览的目录。**
  For example, to look at the /etc directory, click the right arrow next to the /etc directory. This causes Nautilus to display the subdirectories in /etc and to change the right arrow to a down arrow. X11 is one of the subdirectories in /etc that you'd view in the next step.
  例如，要查看 /etc 目录，请单击 /etc 目录旁边的右箭头。这会导致 Nautilus 显示 /etc 中的子目录，并将右箭头更改为下箭头。X11 是 /etc 中的子目录之一，您将在下一步中查看它。
- 3. **To view the contents of the X11 subdirectory, click X11.**
  - 3. **要查看 X11 子目录的内容，请单击 X11。**
  The window on the right now shows the contents of the /etc/X11 directory, as shown in Figure 1-11.
  右侧窗口现在显示 /etc/X11 目录的内容，如图 1-11 所示。

Nautilus displays the contents of the selected directory using different types of icons. Each directory appears as a folder, with the name of the directory shown underneath the folder icon. Ordinary files, such as XF86Config, appear as a sheet of paper. The file named X is a link to an executable file. The pref dm file is another executable file.
Nautilus 使用不同类型的图标显示所选目录的内容。每个目录都显示为文件夹，目录名称显示在文件夹图标下方。普通文件，例如 XF86Config，显示为纸张。名为 X 的文件是可执行文件的链接。pref dm 文件是另一个可执行文件。

The Nautilus window has the usual menu bar and a toolbar. Notice the View as Icons button in Figure 1-11 on the right side of the toolbar. That means Nautilus is displaying the directory contents using large icons. Click the button, and a drop-down list appears. Select View as List from the list; this
causes Nautilus to display the contents by using smaller icons in a list format, along with detailed information, such as the size of each file or directory and the time when each was last modified, as shown in Figure 1-12.
Nautilus 窗口具有通常的菜单栏和工具栏。请注意图 1-11 中工具栏右侧的“以图标查看”按钮。这意味着 Nautilus 使用大图标显示目录内容。单击该按钮，会出现一个下拉列表。从列表中选择“以列表查看”；这
会导致 Nautilus 使用较小的图标以列表格式显示内容，并附带详细信息，例如每个文件或目录的大小以及上次修改的时间，如图 1-12 所示。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_140_0.png)

Figure 1-10:
You can view files and folders in Nautilus.
图 1-10:
您可以在 Nautilus 中查看文件和文件夹。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_140_1.png)

Figure 1-11:
The Nautilus file manager shows the contents of the /etc/X11 directory.
图 1-11:
Nautilus 文件管理器显示 /etc/X11 目录的内容。




Figure 1-12:
Nautilus 文件管理器显示 /etc/X11 目录的列表视图。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_141_0.png)

如果你点击列表视图顶部任意列标题——文件名、大小、类型或修改日期，Nautilus 会根据该列对列表进行排序。例如，点击修改日期列标题。Nautilus 现在会按文件和目录最后修改时间排序显示列表。点击文件名列标题会按字母顺序对文件和文件夹进行排序。

不仅可以使用 Nautilus 在不同文件夹间移动，你还可以执行诸如将文件从一个文件夹移动到另一个文件夹或删除文件等操作。我不会详细说明每一步，因为它们很直观，与你在 Windows 或 Mac 等任何 GUI 中所做的操作类似。以下是你可以在 Nautilus 中执行的一些操作：

- 要将文件移动到不同文件夹，请将文件图标拖放到你想要存放文件的目标文件夹上。
- 要将文件复制到新位置，请选择文件图标并从 Nautilus 菜单中选择 Edit→Copy File。你也可以右键单击文件图标并从弹出菜单中选择 Copy File。然后移动到你想要复制文件的目标文件夹并选择 Edit→Paste Files。
- 要删除文件或目录，请右键单击图标并从弹出菜单中选择 Move to Trash（你只能在有权限删除文件时执行此操作）。要永久删除文件，请右键单击桌面上的 Trash 图标并从弹出菜单中选择 Empty Trash。当然，只有在你真的想要删除文件时才这样做。如果需要从回收站恢复文件，请双击 Trash 图标，然后将文件图标拖回你想要保存它的文件夹。你可以在清空回收站之前随时从回收站恢复文件。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_141_1.png)

- 要重命名文件或目录，请右键单击图标并从弹出菜单中选择 Rename。然后你可以输入新名称或编辑名称。
- 要创建新文件夹，请在右侧窗口的空白区域右键单击并从弹出菜单中选择 New Folder。新文件夹图标出现后，你可以通过右键单击并选择 Rename 从弹出菜单中重命名它。如果没有权限创建文件夹，该菜单项将被置灰。

## Configuring GNOME

要配置 GNOME（以及 Red Hat Linux 的其他部分），只需双击地图和指南针的 Start Here 图标（是的，图标很难识别，但你可以看到标签）。图 1-13 显示了由此产生的 Nautilus 窗口。

Figure 1-13:
你可以在 Start Here 窗口中配置桌面和系统。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_142_0.png)

这个 Nautilus 窗口看起来有点像 Microsoft Windows 中的控制面板。与 Windows 控制面板一样，你可以在 Start Here 窗口中执行许多操作。

要从图 1-13 所示的窗口配置 GNOME 桌面，请执行以下操作：

1. 双击 Preferences 图标。

Nautilus 显示 Preferences 窗口，如图 1-14 所示，你可以在其中配置许多不同的项目。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_143_0.png)

Figure 1-14:
在此窗口中指定你的偏好设置。

2. 要选择背景，请双击 Background 图标。

Nautilus 启动 Background Preferences 对话框（图 1-15）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_143_1.png)

Figure 1-15:
从此对话框中选择背景颜色或壁纸。

在此对话框中，你现在可以为桌面选择背景颜色或壁纸（用作背景的图像）：

- a. 要选择壁纸，请点击窗口左上角的 Select Picture 按钮（参见图 1-15）并浏览目录以选择任意 JPEG 文件作为壁纸。
- b. 选择 `/usr/share/wallpaper` 目录中的其中一个图像，然后点击 OK；点击 Close 退出对话框。

图 1-16 显示了我将 alien-night.jpg 文件选为背景后的 GNOME 桌面。

3. 如果你想配置 GNOME 桌面或 Red Hat Linux 的其他方面，只需双击图 1-14 中的其中一个图标并试用。当完成后，点击 Preferences 窗口右上角的 X 按钮退出。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_144_0.png)

Figure 1-16:
使用新壁纸后，GNOME 桌面看起来更具吸引力。

### Chapter 2: Exploring KDE

## In This Chapter

- 了解 KDE
- 使用 KDE 面板
- 检查 KDE 主菜单
- 运行 KDE 小程序
- 使用 Konqueror
- 配置 KDE

KDE（发音为 kay-dee-ee）是 Red Hat Linux 的 GUI。KDE 与 Microsoft Windows 相似，但扮演不同的角色：与 Microsoft Windows 也是操作系统不同，KDE 只是一个在 Linux 操作系统上运行的 GUI。从你的角度来看，这意味着如果你不喜欢 KDE，只需注销然后使用另一个 GUI——GNOME 重新登录即可。（试试在 Microsoft Windows 上这样做！再想想，还是别试了。）

了解 KDE 的最佳方式是作为用户去探索它。本章我将带你简要参观 KDE。然后你可以在继续使用 KDE 的过程中继续探索并学习更多。

顺便说一下，KDE 是独立于 Linux 开发的。事实上，KDE 还可以在 Linux 以外的其他 UNIX 操作系统上运行。访问 KDE 主页 www.kde.org 以了解 KDE 的最新动态。

## Taking Stock of KDE

KDE 是用户使用的完整桌面环境，但也是开发人员的编程环境。以下是关于 KDE 的一些关键事实：

- KDE 用 C++ 编写并使用面向对象开发。
- KDE 包含一个 GUI 工具包，以便开发人员使用该工具包编写 GUI 应用程序。
- KDE 支持对象模型——可以相互交互的软件组件。
- KDE 包含一个办公应用程序套件。办公套件 KOffice 包括电子表格（KSpread）、类似 FrameMaker 的文字处理器（KWord）、演示应用程序（KPresenter）和绘图程序（KIllustrator）。然而，Red Hat 决定仅在 KDE 中安装和设置 OpenOffice.org 应用程序。
- KDE 支持国际化，大多数 KDE 应用程序已被翻译成 25 多种语言。

好了，你明白了。KDE 不仅仅是好看的外表——在那光鲜的外表下有一些相当强大的机制。

## KDE desktop

![](img/a7eec43a54473e95dc5ea333fecf1bd7_147_0.png)

如果你的系统同时安装了 GNOME 和 KDE，你可以在登录前选择想要使用的 GUI。要选择 KDE 会话，请按照以下步骤操作：

- 1. 点击图形登录屏幕底部的 Session（如图 2-1 所示）。

一个对话框出现，其中列出了会话。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_147_1.png)

Figure 2-1:
点击 Session 然后点击 KDE 以获取 KDE 桌面。

- 2. 在对话框中点击 KDE 单选按钮，然后点击 OK 继续。
- 3. 输入你的用户名和密码以正常登录。

之后一个屏幕（图 2-2）显示 KDE 启动时的进度。

Figure 2-2:
此屏幕显示图形桌面准备就绪时的进度。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_148_0.png)

初始的 KDE 桌面（图 2-3）看起来像任何其他流行的 GUI，如 Microsoft Windows 或 Apple 的 Mac。更重要的是，KDE 桌面现在看起来出人意料地与 GNOME 桌面相似（以前不是这样）。这并非偶然——Red Hat 希望通过为 GNOME 和 KDE 采用相似的外观和感觉来让我们这些可怜的用户更轻松。

KDE 桌面显示你的文件夹图标、已删除文件的废纸篓以及软盘驱动器图标。你还找到一个 Start Here 快捷方式，可用于配置 KDE 桌面（以及更多功能）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_148_1.png)

KDE 桌面的另一个主要特性是底部的栏：KDE 面板，或简称为面板。与 Windows 任务栏类似，面板具有各种应用程序的按钮，以及右侧的日期和时间显示。面板中间部分显示你已启动（或自动启动）的任何应用程序的按钮。




![](img/a7eec43a54473e95dc5ea333fecf1bd7_149_0.png)

图 2-3：
KDE 桌面看起来与其他流行的 GUI 桌面相似。

## 桌面弹出菜单

在 KDE 桌面上右键单击空白区域，菜单就会弹出（如图 2-4 所示）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_149_1.png)

图 2-4：
右键单击 KDE 桌面以显示此弹出菜单。

从此桌面菜单中，你可以做很多事情。你可以在桌面上创建项目——从目录和文档到用于访问 CD-ROM 驱动器的图标。你还可以排列图标、锁定屏幕（如果你暂时离开电脑），或注销。

带有右指向箭头的桌面菜单选项在将鼠标指针移到箭头上时会显示其他菜单。例如，图 2-4 显示了将鼠标移至“新建”时出现的菜单。你可以从中选择要在桌面上创建的确切内容。

表 2-1 解释了每个菜单选项的作用。 不适用的菜单项为灰色显示。 不妨点击一些这些菜单选项看看会发生什么。 如果你现在在桌面上创建一些文件夹和其他图标，日后随时可以删除它们。

**表 2-1 KDE 桌面菜单选项**

| 选择此选项时 | 执行以下操作 |
|---|---|
| 新建 | 弹出另一个菜单，从中可以选择要创建的内容——目录、各种类型的文档、设备的快捷方式或网站。 |
| 书签 | 启动书签编辑器。 |
| 撤销 | 撤消对桌面项目执行的上一个移动、剪切或粘贴操作。 |
| 粘贴 | 粘贴之前剪切或复制的项目。 |
| 打开终端 | 打开一个终端窗口，在其中可以输入 Linux 命令。 |
| 运行命令 | 提示输入要运行的 Linux 命令，然后运行它（如果点击“运行”）。 |
| 图标 | 弹出另一个菜单，从中可以排列桌面图标并以各种方式排列它们。 |
| 窗口 | 显示一个菜单，从中可以层叠（将窗口彼此重叠放置，连续窗口之间略有偏移）或整理当前显示在桌面上的窗口。 |
| 刷新桌面 | 重新绘制桌面（消除任何故障，例如行为不佳的程序在桌面上留下的混乱）。 |
| 配置桌面 | 启动 KDE 控制中心，可在此处自定义桌面（包括点击鼠标各按钮时弹出的菜单）。 |
| 帮助 | 打开 KDE 帮助中心窗口。 |
| 锁定屏幕 | 启动屏幕保护程序并锁定屏幕（你必须输入密码才能退出屏幕保护程序模式）。 |
| 注销 | 允许你注销。 |

![](img/a7eec43a54473e95dc5ea333fecf1bd7_150_0.png)

如果你的鼠标有三个按钮（或带滚轮）并且在 X Window System 中设置正确，请尝试使用鼠标中键单击 KDE 桌面的空白区域（你也可以在带滚轮的鼠标上使用滚轮滚动，但仅在有内容可滚动的窗口中）。你应该会看到另一个菜单。默认情况下，此类中键单击会弹出一个菜单，其中列出了当前打开的窗口和桌面。然后你可以点击一个项目切换到该窗口或桌面。如果中键单击时没有任何反应，不用担心——你仍然可以访问 KDE 中的所有内容。

## 图标弹出菜单

右键单击任何桌面图标都会导致另一个菜单出现。 无论点击哪个图标，此弹出菜单上的许多项目都相同——但右键单击某些图标（例如“回收站”图标）会产生略有不同的菜单。 图 2-5 显示了右键单击“主文件夹”图标时出现的菜单。

图 2-5：
右键单击 KDE 桌面上的图标以显示此类型的弹出菜单。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_151_0.png)

表 2-2 提供了图标弹出菜单中常见菜单选项的概述。 如你所料，任何不适用的菜单选项都是灰色的。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_151_1.png)

我敢打赌你在这里看到了一个模式。 就是右键单击。 无论你在 KDE 的哪个位置，挑选之前总是先右键单击。 右键单击时你总会找到有用的东西！

注：如果将鼠标指针简单地停留在桌面图标上，KDE 会显示一个弹出窗口，其中包含有关该图标的详细信息。

**表 2-2 KDE 图标菜单选项**

| 选择此选项时 | 执行以下操作 |
|---|---|
| 打开 | 在新的 Konqueror 窗口中打开文件。 （Konqueror 是 KDE 中的文件管理器兼网页浏览器。） |
| 撤销 | 假设你刚刚执行了其中一项操作，则撤消上一次复制、剪切或粘贴操作。 |
| 剪切 | 剪切有关图标的信息并显示一个菜单，其中包含诸如通过电子邮件发送项目或编辑其内容之类的选项。 |
| 复制 | 复制有关图标的信息并显示一个菜单，其中包含诸如通过电子邮件发送项目或编辑其内容之类的选项。 |
| 重命名 | 重命名图标（你必须输入新名称）。 |
| 移至回收站 | 询问是否要将图标移至回收站（如果回答“是”，则执行此操作）。 |
| 删除 | 询问是否真的要删除图标（如果回答“是”，则执行此操作）。 |
| 添加到书签 | 将有关图标的信息添加到书签中。 |
| 使用...打开 | 打开一个对话框，在其中可以选择要打开该图标所代表的项目的应用程序。 |
| 复制到 | 显示另一个菜单，从中可以选择要复制该图标所代表的项目的位置。 |
| 移动到 | 显示另一个菜单，从中可以选择要移动该图标所代表的项目的位置。 |
| 编辑文件类型 | 弹出文件类型编辑器，可在其中编辑有关该图标的一些信息。 |
| 属性 | 显示图标的属性。 |

## 使用 KDE 面板

KDE 面板是横跨 KDE 桌面底部的长条。 图 2-6 显示了面板的典型视图。

面板上有许多图标。 点击其中一些图标会启动程序。 其中一些显示状态信息（例如当前正在运行哪些程序），以及日期和时间等其他信息。

从左侧开始，Red Hat 图标是 KDE 文档中所称的 K 按钮——它类似于 Microsoft Windows 中的“开始”按钮。 然后是一系列启动各种程序的图标。

图 2-6：
这是 KDE 面板的典型视图。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_152_0.png)

![](img/a7eec43a54473e95dc5ea333fecf1bd7_153_0.png)

当你将鼠标移至图标上方时，会弹出一个小帮助气球，提供有关该图标的有用提示。 对于某些图标，气球帮助提示非常有用。 对于其他图标，它可能只是 KDE 应用程序的名称（通常都以 K 开头）。 名称可能立即告诉你一些有用的信息，也可能不告诉。 使用 KDE 一段时间后，你会认识这些名称； 在此期间，气球帮助提供了有关每个图标功能的温和提醒。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_153_1.png)

在这些应用程序图标的右侧，你会看到桌面分页器图标。 该图标显示四个编号为 1 到 4 的小矩形。 每个矩形代表一个虚拟桌面。 点击一个数字即可切换到该虚拟桌面。 此功能让你感觉拥有四个独立的桌面可供使用。 说实话，我最终只使用一个桌面，但知道其他桌面在需要时可用也很好。 另一方面，如果你正在编写代码并为新程序准备用户指南，你可以使用一个桌面进行所有编码工作，第二个桌面用于编写用户指南。 当然，你也可以通过单击鼠标即可从一个桌面切换到另一个桌面。

面板任务栏出现在虚拟桌面分页器图标的右侧。 任务栏在面板上的矩形区域中为每个正在运行的应用程序显示一个按钮。 你可以点击一个按钮将该应用程序缩小为图标或切换到该应用程序。

面板最右侧的项目是一个数字时钟，显示当前时间。 如果将鼠标移至时间上方然后暂停，日期会出现在一个小弹出窗口中。 右键单击时钟会弹出一个菜单，可从中调整日期和时间。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_153_2.png)

现在关于面板和图标的一些技术细节。 面板本身是一个名为 Kicker 的 KDE 应用程序。 其每个图标要么是按钮，要么是小程序。 按钮启动应用程序或执行特殊功能，例如隐藏所有打开的窗口。 小程序是小型应用程序（也称为插件）。 小程序在面板中运行并执行有用的操作（例如显示当前日期和时间）。

如果你右键单击任何图标——或在面板上的任何位置右键单击——你会得到一个弹出菜单，可在其中执行与该图标相关的操作（例如移动它或完全删除它）。 你还可以设置一些首选项并向面板添加更多按钮和小程序。

## 主菜单

KDE 面板上最左侧的图标是 KDE 文档中所称的 K 菜单按钮。 （现在 Red Hat 让 GNOME 和 KDE 面板看起来几乎相同，我称之为“主菜单”按钮）。 你会在那里找到

在 Red Hat Linux 中运行所需的一切。本节中，我将概述主菜单并指出一些有趣的项目。你可以自行进一步探索。

单击“主菜单”按钮以调出第一级菜单。然后将鼠标悬停在带有箭头的任何菜单项上以调出下一级菜单，依此类推。你可以浏览菜单层次结构并从最终菜单中进行选择。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_154_0.png)

关于我引用菜单选择的方式说明。我使用记法 主菜单→互联网→Evolution Email 来表示你用来选择邮件阅读器的菜单选择序列（图 2-7）。同样，我会说选择 主菜单→互联网→Mozilla 网页浏览器 来启动 Mozilla 网页浏览器。你明白了。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_154_1.png)

Figure 2-7:
单击“主菜单”按钮并将鼠标悬停在项目上以查看菜单层次结构。

在层次结构中的第一个菜单中，顶部的前十几个项目左右可让你访问 Red Hat Linux 中的所有应用程序和实用程序。将鼠标指针移到其中每个项目上会调出其他菜单，从中你可以挑选要运行的应用程序或实用程序。在下面的列表中，我描述了你在主菜单的第一菜单窗格中看到的菜单类别。（如果你在系统上安装其他软件包，可能会出现其他类别。）

- **附件：** 此菜单包含大量实用程序，例如科学计算器、字符选择器、软盘格式化工具、词典、Palm Pilot 或 Handspring 同步等。
- **游戏：** 此菜单会调出菜单，内容是什么呢，当然是游戏（而且有很多）。
- **图形：** 此菜单包含诸如 GIMP（类似 Adobe Photoshop 的程序）、数码相机接口、扫描仪接口、屏幕捕获程序和 Adobe Acrobat 阅读器等程序。
- **互联网：** 此菜单（参见图 2-7）用于互联网应用程序，例如网页浏览器、电子邮件阅读器和即时通讯工具。
- **办公：** 此菜单会调出 OpenOffice.org 办公套件的应用程序菜单（包括 Writer 文字处理器、Calc 电子表格、Impress 幻灯片演示程序、Draw 绘图程序等等）。
- **首选项：** 此菜单会调出另一个菜单，从中你可以配置系统的许多方面。特别是，首选项→桌面设置向导 可让你自定义 KDE 桌面的外观和行为。你也可以从首选项→密码 菜单更改密码。
- **编程：** 此菜单可让你运行软件开发工具，例如 Emacs 编辑器和 KDE 开发环境（KDevelop），前提是你已安装这些工具。
- **声音和视频：** 此菜单包含多媒体应用程序，例如 CD 播放器、声音混音器、声音记录器和音量控制。
- **系统设置：** 此菜单列出了 15 多种用于设置 Red Hat Linux 系统的工具。它包括管理用户账户、配置打印机和更改 root 密码的工具。服务器设置 子菜单提供了配置 Web 服务器、域名系统（DNS）服务器和网络文件系统（NFS）服务器的工具的访问权限。你也可以从此菜单打开或关闭各种服务。
- **系统工具：** 此菜单包含许多用于执行诸如配置互联网连接、查看系统日志、向 Red Hat Network 注册以及打开可输入 Linux 命令的终端窗口等任务的工具。更多系统工具 子菜单可让你运行更多工具，包括 CD 刻录机、启动盘创建器、桌面切换工具、IBM 3278 终端等等。
- **控制中心：** 此项打开 KDE 控制中心窗口，从中你可以配置 KDE 桌面（除首选项菜单中可执行的操作外）。
- **查找文件：** 此项调出查找文件工具，从中你可以搜索系统中的文件。
- **帮助：** 此项启动 KDE 帮助中心——KDE 中的在线帮助。
- **主目录：** 此项在 Konqueror 文件管理器窗口中显示你的主文件夹的内容。
- **运行命令：** 此项显示一个对话框，你可以在其中输入要运行的程序的名称。
- **锁定屏幕：** 此项启动屏幕保护程序并锁定屏幕，以便你暂时离开工作站。当你想返回桌面时，KDE 会提示你输入密码（图 2-8）。
- **注销：** 此项正如其名——注销（当然，只有在你确认确实要注销后才会执行）。

Figure 2-8:
KDE 在打开锁定屏幕前会提示输入密码。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_156_0.png)

好了。关于 KDE 的主菜单，我就讲这么多。你在使用 Red Hat Linux 时会经常使用主菜单。即使起初看起来有点多，随着你使用 Red Hat Linux 时间的增加，你会非常熟悉这些菜单。

## 小程序

小程序是运行在 KDE 面板内的微型程序。你可以通过右键单击 KDE 面板上的空白区域并从弹出菜单中选择 添加→小程序 来启动一个小程序。当你想监视某些信息或只是想要一种方便的方式来运行某些应用程序时，小程序非常实用。

其中一个有趣的小程序是词典。此小程序在面板上显示一个文本输入区域。你可以输入一个单词并按 Enter 键查找其定义。假设你的 Red Hat Linux PC 已连接互联网，此小程序会连接到服务器 dict.org 并下载你输入的单词的定义，并在新窗口中显示。

要将词典小程序添加到面板，请右键单击 KDE 面板上的空白区域并选择 添加→小程序→词典。图 2-9 显示了从中选择词典的菜单层次结构。

Figure 2-9:
这是从主菜单向面板添加小程序的位置。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_157_0.png)

词典小程序启动并在面板上显示一个文本输入区域（如图 2-10 所示）。

Figure 2-10:
词典小程序在面板上显示一个文本输入区域，用于查找单词的定义。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_157_1.png)

要在词典中查找单词，请单击文本输入区域并输入单词。然后按 Enter 键。词典小程序会从 dict.org 下载该单词的定义并在新窗口中显示结果。例如，图 2-11 显示了查找单词 profiler 的结果。

Figure 2-11:
词典小程序在新窗口中显示单词的定义。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_158_0.png)

![](img/a7eec43a54473e95dc5ea333fecf1bd7_158_1.png)

如果你不再想要该小程序，请将其删除：右键单击 KDE 面板上的空白区域并选择 删除→小程序→词典。

KDE 还有许多其他小程序（超过 15 个，但谁在计数呢？）你可以尝试。它们的名字显示在图 2-9 中的小程序菜单中。（灰显的项目是已在运行且只能启动一次的小程序。）表 2-3 为你提供了 KDE 中小程序的概述。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_158_2.png)

如果表 2-3 中列出的任何小程序引起你的兴趣，请尝试一下。要查找小程序，请右键单击 KDE 面板的空白部分，选择 添加→小程序，然后单击小程序的名称。

### 表 2-3 KDE 小程序概述

| 小程序 | 其功能 |
|---|---|
| Application Launcher | 添加一个小型命令行，可在其中输入 Linux 命令并运行。 |
| Clock | 在小型数字时钟中显示当前时间，并在下方显示日期。 |
| Color Picker | 显示一个滴管图标，可用于从桌面任何位置拾取颜色（然后你可以将该颜色值复制到其他配置文件中）。 |
| Dictionary | 添加一个小型文本输入区域，可在其中输入单词并在词典中查找（结果显示在新窗口中）。 |

(continued)

| 小程序 | 功能说明 |
|---|---|
| KCharSelect | 显示可复制粘贴到文档中的带重音符号的字符版本。 |
| KMix Applet | 提供控制音量和启动音频混音器应用程序的界面。 |
| KNewsTicker | 以滚动 ticker 的形式显示来自各种来源（例如 www.slashdot.org 和 www.kde.org）的最新新闻。 |
| KSysGuard | 收集并绘制来自网络上一台或多台系统的 CPU 和内存使用信息（用于监控服务器）。 |
| Klipper | 提供剪切和粘贴信息的剪贴板实用程序。 |
| Lock/Logout Applet | 提供两个图标——一个锁图标用于锁定屏幕，一个关机开关用于注销。 |
| MediaControl | 显示音频和视频播放器的控制面板。 |
| Pager | 显示虚拟桌面的视图；用它在桌面之间切换（登录时此小程序已在运行）。 |
| Public File Server | 提供公共 Web 服务器（您可以配置共享的目录和数据传输速率）。 |
| Quick Launcher | 包含许多应用程序的小图标（单击图标即可启动该应用程序）。 |
| Runaway Process Catcher | 显示一个笑脸，当任何进程开始使用过多 CPU 时间或内存时笑脸会变得愤怒。 |
| System Monitor | 以图形方式显示正在使用的系统资源（内存、CPU 时间）的数量。 |
| System Tray | 提供一个区域可容纳 Klipper 等特殊应用程序。 |
| Taskbar | 为每个正在运行的应用程序显示一个按钮（登录时此小程序已在运行）。 |

## 使用 Konqueror

Konqueror 既是文件管理器也是 Web 浏览器。它使用直观——有点类似于 Windows Active Desktop。你可以用 Konqueror 管理文件和文件夹（也可以查看网页）。

## 查看文件和文件夹

当你在桌面上双击文件夹图标时，Konqueror 会自动启动。例如，双击 KDE 桌面左上角的主目录图标。Konqueror 运行并显示你的主目录内容（把目录想象成可包含其他文件和文件夹的文件夹）。图 2-12 显示了 Konqueror 中典型用户的主目录。

如果你使用过 Windows Explorer，可以以类似的方式使用 Konqueror。

Konqueror 窗口垂直分为三部分：

- 窄的左侧窗口显示可点击以在 Konqueror 中执行各种任务的图标。
- 更宽的中间窗口显示当前文件夹的树视图。
- 最宽的窗口（在右侧）使用图标显示当前文件夹中的文件和文件夹。

Konqueror 为不同文件使用不同类型的图标并显示每个文件内容预览。对于图像文件，预览是图像的缩略图版本。

Konqueror 窗口的标题栏显示当前选定目录的名称。位置文本框（沿窗口顶部）显示目录的完整名称，使用 Konqueror 的术语——在此情况下，图 2-12 显示的是 /home/naba 目录的内容。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_160_0.png)

Figure 2-12:
您可以在 Konqueror 中查看文件和文件夹。

在左右窗口之间，垂直的按钮行用于选择其他浏览内容。当你点击其中一个按钮时，左侧窗口会显示可浏览项目的树菜单。例如，要浏览文件系统的其他部分，请执行以下操作：

1. **从 Konqueror 窗口最左侧的垂直图标列（参见图 2-12）中，点击文件夹图标（它出现在星形图标正上方的那个）。**
   目录树菜单出现在中间窗口中。
2. **在树视图中，找到你想要浏览的文件夹。**
   例如，要查看 `etc` 文件夹，点击 `etc` 文件夹旁边的加号。Konqueror 显示 `etc` 中的其他文件夹并将加号更改为减号。
3. **要查看 X11 子目录的内容，向下滚动并点击 X11。**
   右侧窗口现在显示 `/etc/X11` 目录的内容，如图 2-13 所示。

Konqueror 使用不同类型的图标显示文件夹内容。每个目录都显示为文件夹，目录名称显示在文件夹图标下方。普通文件，如 `XF86Config`，显示为纸张。名为 X 的文件是可执行文件的快捷方式。`prefdm` 文件是另一个可执行文件。

Konqueror 窗口具有通常的菜单栏和工具栏。你也可以以其他格式查看文件和文件夹。例如，选择 View→View Mode→Detailed List View 以使用较小的图标以列表格式查看文件夹内容（图 2-14），并附带详细信息（如每个文件或目录的大小，以及上次修改的时间）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_161_0.png)

Figure 2-13:
Konqueror 显示 /etc/X11 目录的内容。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_162_0.png)

Figure 2-14: Konqueror 显示 /etc/X11 目录的详细列表视图。

如果你点击列表视图顶部列标题中的任意一个——Name、Size、File Type 或 Modified——Konqueror 会根据该列对列表进行排序。例如，点击 Modified 列标题，Konqueror 会根据上次修改时间对文件和文件夹列表进行排序。点击 Name 列标题会按字母顺序对文件和目录进行排序。

不仅可以使用 Konqueror 在不同文件夹之间移动，你还可以执行诸如将文件从一个文件夹移动到另一个文件夹或删除文件等操作。我不会逐一列出每一步，因为这些步骤很直观，与你在任何 GUI（如 Windows 或 Mac 界面）中所做的工作相似。以下是你可以在 Konqueror 中执行的一些操作：

- 查看文本文件：点击文件名，Konqueror 运行 KWrite 文字处理器，在新窗口中显示文件。
- 将文件复制或移动到不同文件夹：将文件图标拖放到你想要文件去的文件夹上。会出现一个菜单，询问你是否要复制、移动或仅将文件链接到该目录。
- 删除文件或目录：右键点击图标，从弹出菜单中选择 Move to Trash。要永久删除文件，右键点击桌面上的废纸篓图标，从弹出菜单中选择 Empty Trash。当然，只有在你真的想删除文件时才这样做。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_162_1.png)

如果你想从回收站恢复文件，双击桌面上的废纸篓图标，然后从该窗口将文件图标拖放到你想要保存文件的[content]
| 小程序 | 功能说明 |
|---|---|
| KCharSelect | 显示可复制粘贴到文档中的带重音符号的字符版本。 |
| KMix Applet | 提供控制音量和启动音频混音器应用程序的界面。 |
| KNewsTicker | 以滚动 ticker 的形式显示来自各种来源（例如 www.slashdot.org 和 www.kde.org）的最新新闻。 |
| KSysGuard | 收集并绘制来自网络上一台或多台系统的 CPU 和内存使用信息（用于监控服务器）。 |
| Klipper | 提供剪切和粘贴信息的剪贴板实用程序。 |
| Lock/Logout Applet | 提供两个图标——一个锁图标用于锁定屏幕，一个关机开关用于注销。 |
| MediaControl | 显示音频和视频播放器的控制面板。 |
| Pager | 显示虚拟桌面的视图；用它在桌面之间切换（登录时此小程序已在运行）。 |
| Public File Server | 提供公共 Web 服务器（您可以配置共享的目录和数据传输速率）。 |
| Quick Launcher | 包含许多应用程序的小图标（单击图标即可启动该应用程序）。 |
| Runaway Process Catcher | 显示一个笑脸，当任何进程开始使用过多 CPU 时间或内存时笑脸会变得愤怒。 |
| System Monitor | 以图形方式显示正在使用的系统资源（内存、CPU 时间）的数量。 |
| System Tray | 提供一个区域可容纳 Klipper 等特殊应用程序。 |
| Taskbar | 为每个正在运行的应用程序显示一个按钮（登录时此小程序已在运行）。 |

## 使用 Konqueror

Konqueror 既是文件管理器也是 Web 浏览器。它使用直观——有点类似于 Windows Active Desktop。你可以用 Konqueror 管理文件和文件夹（也可以查看网页）。

## 查看文件和文件夹

当你在桌面上双击文件夹图标时，Konqueror 会自动启动。例如，双击 KDE 桌面左上角的主目录图标。Konqueror 运行并显示你的主目录内容（把目录想象成可包含其他文件和文件夹的文件夹）。图 2-12 显示了 Konqueror 中典型用户的主目录。

如果你使用过 Windows Explorer，可以以类似的方式使用 Konqueror。

Konqueror 窗口垂直分为三部分：

- 窄的左侧窗口显示可点击以在 Konqueror 中执行各种任务的图标。
- 更宽的中间窗口显示当前文件夹的树视图。
- 最宽的窗口（在右侧）使用图标显示当前文件夹中的文件和文件夹。

Konqueror 为不同文件使用不同类型的图标并显示每个文件内容预览。对于图像文件，预览是图像的缩略图版本。

Konqueror 窗口的标题栏显示当前选定目录的名称。位置文本框（沿窗口顶部）显示目录的完整名称，使用 Konqueror 的术语——在此情况下，图 2-12 显示的是 /home/naba 目录的内容。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_160_0.png)

Figure 2-12:
您可以在 Konqueror 中查看文件和文件夹。

在左右窗口之间，垂直的按钮行用于选择其他浏览内容。当你点击其中一个按钮时，左侧窗口会显示可浏览项目的树菜单。例如，要浏览文件系统的其他部分，请执行以下操作：

1. **从 Konqueror 窗口最左侧的垂直图标列（参见图 2-12）中，点击文件夹图标（它出现在星形图标正上方的那个）。**
   目录树菜单出现在中间窗口中。
2. **在树视图中，找到你想要浏览的文件夹。**
   例如，要查看 `etc` 文件夹，点击 `etc` 文件夹旁边的加号。Konqueror 显示 `etc` 中的其他文件夹并将加号更改为减号。
3. **要查看 X11 子目录的内容，向下滚动并点击 X11。**
   右侧窗口现在显示 `/etc/X11` 目录的内容，如图 2-13 所示。

Konqueror 使用不同类型的图标显示文件夹内容。每个目录都显示为文件夹，目录名称显示在文件夹图标下方。普通文件，如 `XF86Config`，显示为纸张。名为 X 的文件是可执行文件的快捷方式。`prefdm` 文件是另一个可执行文件。

Konqueror 窗口具有通常的菜单栏和工具栏。你也可以以其他格式查看文件和文件夹。例如，选择 View→View Mode→Detailed List View 以使用较小的图标以列表格式查看文件夹内容（图 2-14），并附带详细信息（如每个文件或目录的大小，以及上次修改的时间）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_161_0.png)

Figure 2-13:
Konqueror 显示 /etc/X11 目录的内容。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_162_0.png)

Figure 2-14: Konqueror 显示 /etc/X11 目录的详细列表视图。

如果你点击列表视图顶部列标题中的任意一个——Name、Size、File Type 或 Modified——Konqueror 会根据该列对列表进行排序。例如，点击 Modified 列标题，Konqueror 会根据上次修改时间对文件和文件夹列表进行排序。点击 Name 列标题会按字母顺序对文件和目录进行排序。

不仅可以使用 Konqueror 在不同文件夹之间移动，你还可以执行诸如将文件从一个文件夹移动到另一个文件夹或删除文件等操作。我不会逐一列出每一步，因为这些步骤很直观，与你在任何 GUI（如 Windows 或 Mac 界面）中所做的工作相似。以下是你可以在 Konqueror 中执行的一些操作：

- 查看文本文件：点击文件名，Konqueror 运行 KWrite 文字处理器，在新窗口中显示文件。
- 将文件复制或移动到不同文件夹：将文件图标拖放到你想要文件去的文件夹上。会出现一个菜单，询问你是否要复制、移动或仅将文件链接到该目录。
- 删除文件或目录：右键点击图标，从弹出菜单中选择 Move to Trash。要永久删除文件，右键点击桌面上的废纸篓图标，从弹出菜单中选择 Empty Trash。当然，只有在你真的想删除文件时才这样做。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_162_1.png)

如果你想从回收站恢复文件，双击桌面上的废纸篓图标，然后从该窗口将文件图标拖放到你想要保存文件的



2. 要选择壁纸，请单击壁纸选项卡（图 2-17），然后单击当前壁纸名称旁边的浏览按钮。
控制中心会打开“选择壁纸”对话框（如图 2-18 所示）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_165_0.png)

图 2-17：
从此窗口选择背景颜色或壁纸。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_165_1.png)

图 2-18：
从此对话框中选择壁纸图像。

3. 单击工具栏上的向上箭头前往 `root` 目录。

4. 在 `root` 目录中，导航到 `/usr/share/wallpapers` 目录。

5. 从文件列表中选择一个 JPEG 图像文件，然后单击“确定”。
6. 返回控制中心窗口后，单击“应用”使新更改生效。
7. 如果你想配置 KDE 桌面的其他方面，请在“外观和主题”列表中选择另一项（参见图 2-17）并试用。

图 2-19 显示了我将 alien-night.jpg 文件选为壁纸后的 KDE 桌面。

单击“应用”尝试新的配置；如果不喜欢结果，请单击“重置”恢复到旧设置。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_166_0.png)

图 2-19：
选择合适的壁纸后，KDE 桌面看起来极具科幻感。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_166_1.png)

### 第 3 章：学习 Shell

### 本章内容

- ✓ 打开终端窗口和虚拟控制台
- ✓ 使用 Bash shell
- ✓ 学习一些 Linux 命令
- ✓ 编写 shell 脚本

有时事情就是不工作。如果图形用户界面桌面停止响应鼠标点击怎么办？如果图形界面根本无法启动怎么办？你仍然可以告诉 Red Hat Linux 系统该做什么，但你必须通过在文本屏幕上输入命令来完成。在这些情况下，你将使用 shell — Linux 命令解释器。本章介绍 Bash shell（Red Hat Linux 中的默认 shell）。

学会使用 shell 后，你甚至可能会喜欢 Linux 命令的简洁性和强大功能。然后，即使你是一个图形界面爱好者，很快你可能会发现自己打开一个终端窗口，用由奇怪的标点字符连接起来的两三个字母的命令让系统歌唱跳舞。（嘿，我可以做梦，对吧？）

## 打开终端窗口和虚拟控制台

首先，首先。如果你在 GNOME 或 KDE 中工作，你在哪里为 shell 输入命令？好问题。

最简单的方法是打开一个终端（也称为控制台）窗口。GNOME 和 KDE 面板都有打开终端窗口的图标。该图标看起来像一台显示器。单击该图标即可打开终端窗口。现在你可以尽情输入命令了。

如果由于某种原因图形界面似乎卡住了（你点击和输入但没有任何反应），你可以转向虚拟控制台。（物理控制台是显示器和键盘的组合。）虚拟控制台的想法是让你能够在多个文本控制台之间切换，即使你只有一个物理控制台。无论你是否运行图形界面，你都可以使用不同的文本控制台输入不同的命令。

从 GNOME 或 KDE 桌面进入第一个虚拟控制台，请按 Ctrl+Alt+F1。按 Ctrl+Alt+F2 进入第二个虚拟控制台，以此类推。每个虚拟控制台都是一个文本屏幕，你可以在其中登录并输入 Linux 命令执行各种任务。完成后，输入 exit 注销。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_169_0.png)

你最多可以使用六个虚拟控制台。第七个用于图形界面桌面。要返回图形界面桌面，请按 Ctrl+Alt+F7。

## 使用 Bash Shell

如果你使用过 MS-DOS，你可能熟悉 COMMAND.COM，即 DOS 命令解释器。该程序显示臭名昭著的 C:\> 提示符。在 Windows 中，如果你打开命令窗口就可以看到此提示符。（要在 Microsoft Windows 中打开命令窗口，请选择 Start→Run，在文本框中输入 command，然后单击 OK。）

Red Hat Linux 附带了一个命令解释器，它类似于 DOS 中的 COMMAND.COM，但功能强大得多。Red Hat Linux 命令解释器称为 shell。

Red Hat Linux 中的默认 shell 是 Bash。当你打开终端窗口或在文本控制台登录时，Bash shell 会提示你输入命令。然后，当你输入命令时，shell 会执行你的命令。

除了标准 Linux 命令外，Bash 还可以执行任何计算机程序。因此，你可以在 shell 提示符下输入应用程序的名称（该名称通常比你在 GNOME 或 KDE 菜单中看到的名称更晦涩），shell 就会启动该应用程序。

### 学习 shell 命令的语法

由于 shell 会解释你输入的内容，因此了解 shell 如何处理你输入的文本非常重要。所有 shell 命令都有这种通用格式，以命令开头，后跟选项（某些命令没有选项）：

```
command option1 option2 ... optionN
```

这种单行屏幕命令通常称为命令行。在命令行中，你输入一个命令，后跟零个或多个选项（或参数）。这些选项字符串——命令行
选项（或命令行参数）——修改命令的工作方式，以便你可以让它执行特定任务。

shell 使用空白或制表符来区分命令和选项。当然，你应该通过使用空格或制表符将命令与选项以及选项彼此分开来帮助它。

选项可以包含空格——你所要做的就是将该选项放在引号内以包含空格。例如，要在密码文件中搜索我的名字，我输入以下 grep 命令（grep 用于在文件中搜索文本）：

```
grep "Naba Barkakati" /etc/passwd
```

当 grep 打印包含我名字的行时，它看起来像这样：

```
naba:x:500:500:Naba Barkakati:/home/naba:/bin/bash
```

如果你创建了一个使用你的用户名的用户账户，请使用你的用户名作为参数输入 grep 命令。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_170_0.png)

在 grep 命令的输出中，你可以看到 shell 的名称（/bin/bash）在最后一个冒号（:）之后。

命令行选项的数量和格式当然取决于实际命令。通常，这些选项看起来像 -X，其中 X 是一个字符。例如，ls 命令列出目录的内容。你可以使用 -l 选项查看更多详细信息，如下所示：

```
[ashley@dhcppc4 ashley]$ ls -l
total 8
drwxrwxr-x 2 ashley ashley 4096 Jun 29 13:35 Directory
drwx------ 7 ashley ashley 4096 Jun 29 11:44 Mail
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_170_1.png)

[ashley@dhcppc4 ashley]$ 部分是名为 ashley 的用户的 shell 提示符。在你的系统上，提示符取决于你的用户名。在展示示例时，我省略了提示符。

如果命令太长而无法在一行内容纳，你可以按反斜杠（\ ）键然后按 Enter。然后，在下一行继续输入命令。例如，输入以下命令（每行后按 Enter）：

```
cat \
/etc/passwd
```

`cat` 命令然后显示 `/etc/passwd` 文件的内容。

你可以在单行上连接多个较短的命令。只需用分号（`;`）分隔命令即可。例如，以下命令

```
cd; ls -l; pwd
```

将当前目录更改为你的主目录，列出该目录的内容，然后显示该目录的名称。

### 组合 shell 命令

你可以组合简单的 shell 命令来创建更复杂的命令。假设你想查明名为 `sbpcd` 的设备文件是否位于系统的 `/dev` 目录中，因为某些文档说你需要该设备文件用于 Sound Blaster Pro CD-ROM 驱动器。你可以使用命令 `ls /dev` 获取 `/dev` 目录的目录列表，然后浏览它以查看该列表是否包含 `sbpcd`。

不幸的是，`/dev` 目录有大量条目，因此你很难找到名称中包含 `sbpcd` 的项目。但是，你可以将 `ls` 命令与 `grep` 结合起来，得到一个完全符合你需求的命令行。以下是该命令行：

```
ls /dev | grep sbpcd
```

shell 将 `ls` 命令的输出（目录列表）发送到 `grep` 命令，后者搜索字符串 `sbpcd`。那个竖线（`|`）被称为管道，因为它在两个程序之间充当传导（想想水管），第一条命令的输出被送入第二条命令的输入。

### 控制命令输入和输出

大多数 Linux 命令都有一个共同特点——它们总是从标准输入（通常是键盘）读取并写入标准输出（通常是屏幕）。错误消息发送到标准错误（通常也发送到屏幕）。这三个设备通常被称为 `stdin`、`stdout` 和 `stderr`。

你可以让命令从文件获取输入然后将输出发送到另一个文件。顺便说一下，这个功能的正式术语是输入和输出重定向或 I/O 重定向。



## 从文件获取命令输入

如果你希望命令从文件读取，可以将标准输入重定向到该文件而不是键盘。例如，输入以下命令：

```
sort < /etc/passwd
```

该命令会显示 /etc/passwd 文件中各行的排序列表。在此情况下，小于号（<）重定向 stdin，使 sort 命令从 /etc/passwd 文件读取输入。

## 将命令输出保存到文件

要将命令的输出保存到文件中，请将标准输出重定向到文件。例如，输入 cd 切换到你的主目录，然后输入以下命令：

```
grep typedef /usr/include/* > typedef.out
```

该命令会在 /usr/include 目录下的所有文件中搜索文本 typedef 的出现情况——然后将输出保存到名为 typedef.out 的文件中。大於号（>）将 stdout 重定向到文件。

该命令还说明了 Bash 的另一个特性。当你使用星号（*）时，Bash 会用指定目录中的所有文件名列表替换该星号。因此，/usr/include/* 表示 /usr/include 目录中的所有文件。

## 将错误信息保存到文件

有时你输入一个命令，它会产生大量错误信息，滚动得太快以至于你无法弄清发生了什么。一种查看所有错误信息的方法是将其保存到文件中以便查看发生了什么。你可以通过将 stderr 重定向到文件来实现。

例如，输入以下命令：

```
find / -name isapnp -print 2> finderr
```

该命令会在整个文件系统中查找名为 isapnp 的文件，但将所有错误信息保存到名为 finderr 的文件中。数字 2 后跟大于号（2>）将 stderr 重定向到文件。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_173_0.png)

如果你想直接丢弃错误信息而不是将其保存到文件中，请使用 /dev/null 作为文件名，如下所示：

```
find / -name isapnp -print 2> /dev/null
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_173_1.png)

该 /dev/null 是一个特殊文件——通常称为位桶，有时被美化为天上的大位桶——它会简单地丢弃接收到的任何内容。所以现在你知道当你听到诸如“你的邮件可能落入了位桶”之类的说法时是什么意思了。

## 使用自动命令补全减少输入

许多命令以文件名作为参数。例如，要查看名为 /etc/modules.conf 的文本文件的内容，输入以下命令：

```
cat /etc/modules.conf
```

该 cat 命令会显示文件 /etc/modules.conf。对于任何以文件名作为参数的命令，你都可以使用 Bash 的一个特性来避免输入完整的文件名。你只需输入最少的内容（仅前几个字符）即可在目录中唯一标识该文件。

要看一个例子，输入 cat /etc/mod 但不要按 Enter；改为按 Tab。Bash 会自动补全文件名，因此命令变为 cat /etc/modules.conf。现在按 Enter 运行命令。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_173_2.png)

每当你输入文件名时，在文件名前几个字符后按 Tab。Bash 很可能可以补全文件名，这样你就不必输入整个名称。如果输入的字符不足以唯一标识文件，Bash 会发出蜂鸣声。只需再输入几个字符并再次按 Tab 即可。

## 尽情使用星号和问号

还有一种避免输入长文件名的方法。（毕竟，让用户少做工作就是计算机的理念，不是吗？）

这个特定的技巧涉及使用星号（*）和问号（?）以及一些其他技巧。这些特殊字符称为通配符，因为它们匹配文本行中的零个或多个字符。

```
COPY *.* A:
```

你可以在 Bash 中使用三种类型的通配符：

- 星号（*）字符匹配文件名中的零个或多个字符。这意味着 * 表示目录中的所有文件。
- 问号（?）匹配任意单个字符。因此，如果你输入 test?，它将匹配以 test 开头的任何五个字符的文本。
- 方括号中的字符集合匹配该集合中的任意单个字符。例如，字符串 [aB]* 匹配以 a 或 B 开头的任何文件名。

通配符在你想对大量文件执行某些操作时非常方便。例如，要将 /mnt/cdrom 目录中的所有文件复制到当前目录，输入以下内容：

```
cp /mnt/cdrom/* .
```

Bash 用 /mnt/cdrom 目录中所有文件的名称替换通配符 *。命令末尾的句点代表当前目录。

你可以将星号与其他文件名部分一起使用以选择更具体的[content]
## 从文件获取命令输入

如果你希望命令从文件读取，可以将标准输入重定向到该文件而不是键盘。例如，输入以下命令：

```
sort < /etc/passwd
```

该命令会显示 /etc/passwd 文件中各行的排序列表。在此情况下，小于号（<）重定向 stdin，使 sort 命令从 /etc/passwd 文件读取输入。

## 将命令输出保存到文件

要将命令的输出保存到文件中，请将标准输出重定向到文件。例如，输入 cd 切换到你的主目录，然后输入以下命令：

```
grep typedef /usr/include/* > typedef.out
```

该命令会在 /usr/include 目录下的所有文件中搜索文本 typedef 的出现情况——然后将输出保存到名为 typedef.out 的文件中。大於号（>）将 stdout 重定向到文件。

该命令还说明了 Bash 的另一个特性。当你使用星号（*）时，Bash 会用指定目录中的所有文件名列表替换该星号。因此，/usr/include/* 表示 /usr/include 目录中的所有文件。

## 将错误信息保存到文件

有时你输入一个命令，它会产生大量错误信息，滚动得太快以至于你无法弄清发生了什么。一种查看所有错误信息的方法是将其保存到文件中以便查看发生了什么。你可以通过将 stderr 重定向到文件来实现。

例如，输入以下命令：

```
find / -name isapnp -print 2> finderr
```

该命令会在整个文件系统中查找名为 isapnp 的文件，但将所有错误信息保存到名为 finderr 的文件中。数字 2 后跟大于号（2>）将 stderr 重定向到文件。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_173_0.png)

如果你想直接丢弃错误信息而不是将其保存到文件中，请使用 /dev/null 作为文件名，如下所示：

```
find / -name isapnp -print 2> /dev/null
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_173_1.png)

该 /dev/null 是一个特殊文件——通常称为位桶，有时被美化为天上的大位桶——它会简单地丢弃接收到的任何内容。所以现在你知道当你听到诸如“你的邮件可能落入了位桶”之类的说法时是什么意思了。

## 使用自动命令补全减少输入

许多命令以文件名作为参数。例如，要查看名为 /etc/modules.conf 的文本文件的内容，输入以下命令：

```
cat /etc/modules.conf
```

该 cat 命令会显示文件 /etc/modules.conf。对于任何以文件名作为参数的命令，你都可以使用 Bash 的一个特性来避免输入完整的文件名。你只需输入最少的内容（仅前几个字符）即可在目录中唯一标识该文件。

要看一个例子，输入 cat /etc/mod 但不要按 Enter；改为按 Tab。Bash 会自动补全文件名，因此命令变为 cat /etc/modules.conf。现在按 Enter 运行命令。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_173_2.png)

每当你输入文件名时，在文件名前几个字符后按 Tab。Bash 很可能可以补全文件名，这样你就不必输入整个名称。如果输入的字符不足以唯一标识文件，Bash 会发出蜂鸣声。只需再输入几个字符并再次按 Tab 即可。

## 尽情使用星号和问号

还有一种避免输入长文件名的方法。（毕竟，让用户少做工作就是计算机的理念，不是吗？）

这个特定的技巧涉及使用星号（*）和问号（?）以及一些其他技巧。这些特殊字符称为通配符，因为它们匹配文本行中的零个或多个字符。

```
COPY *.* A:
```

你可以在 Bash 中使用三种类型的通配符：

- 星号（*）字符匹配文件名中的零个或多个字符。这意味着 * 表示目录中的所有文件。
- 问号（?）匹配任意单个字符。因此，如果你输入 test?，它将匹配以 test 开头的任何五个字符的文本。
- 方括号中的字符集合匹配该集合中的任意单个字符。例如，字符串 [aB]* 匹配以 a 或 B 开头的任何文件名。

通配符在你想对大量文件执行某些操作时非常方便。例如，要将 /mnt/cdrom 目录中的所有文件复制到当前目录，输入以下内容：

```
cp /mnt/cdrom/* .
```

Bash 用 /mnt/cdrom 目录中所有文件的名称替换通配符 *。命令末尾的句点代表当前目录。

你可以将星号与其他文件名部分一起使用以选择更具体的组文件。假设你想使用 grep 命令在 /usr/include 目录中符合以下条件的所有文件中搜索文本 typedef struct：

- 文件名以 s 开头。
- 文件名以 .h 结尾。

通配符规范 s*.h 表示符合这些条件的所有文件名。因此你可以使用以下命令执行搜索：

```
grep "typedef struct" /usr/include/s*.h
```

该字符串包含一个空格，你希望 grep 命令找到它，因此你必须用引号将该字符串括起来。这样 Bash 就不会尝试将每个单词解释为单独的命令行参数。

问号（?）匹配单个字符。假设当前目录中有四个文件——image1.pcx、image2.pcx、image3.pcx 和 image4.pcx。要将这些文件复制到 /mnt/floppy 目录，请使用以下命令：

```
cp image?.pcx /mnt/floppy
```

Bash 用任意单个字符替换问号，并将四个文件复制到 /mnt/floppy。

第三种通配符格式——[...]——匹配方括号中特定字符集合中的单个字符。你可能希望将此格式与其他通配符结合使用，以将匹配的文件名缩小到更小的集合。要列出 /etc/X11/xdm 目录中以 x 或 X 开头的所有文件名，输入以下命令：

```
ls /etc/X11/xdm/[xX]*
```

## 重复先前输入的命令

为了让你重复长命令变得容易，Bash 会存储多达 500 个旧命令。Bash 保留一个命令历史记录（旧命令列表）。要查看命令历史记录，输入 history。Bash 会显示旧命令的编号列表，包括你在之前的登录期间输入的命令。

如果命令列表太长，你可以限制要查看的旧命令数量。要仅查看最近的 10 个命令，输入此命令：

```
history 10
```

要重复 history 命令显示的列表中的命令，只需输入感叹号（!），后跟该命令的编号。要重复第 3 个命令，输入 !3。

有一种方法可以在不知道命令编号的情况下重复旧命令。假设几分钟前你输入了 more /usr/lib/X11/xdm/xdm-config，现在你想再次查看该文件。要重复之前的 more 命令，输入以下内容：

```
!more
```

通常，你可能希望重复刚刚输入的最后一个命令，也许稍作更改。例如，你可能已使用 ls -l 命令显示目录的内容。要重复该命令，输入两个感叹号如下：

```
!!
```

有时，你可能希望重复上一个命令但为其添加额外参数。假设 ls -l 显示的文件太多。只需重复该命令，但将输出通过管道传输到 more 命令，如下所示：

```
!! | more
```

Bash 用上一个命令替换两个感叹号，然后在该命令后附加 | more。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_176_0.png)

这是召回以前命令的最简单方法。只需按向上箭头键，Bash 就会一直向后浏览你之前输入的命令历史记录。要在命令历史记录中向前移动，请按向下箭头键。

## 学习 Linux 命令

你在 shell 提示符下输入 Linux 命令。所谓 Linux 命令，我指的是 Bash shell 理解的一些命令以及随 Linux 提供的命令行实用程序。在本节中，我向你介绍 Linux 命令的几个主要类别。

我不可能在本章中涵盖所有 Linux 命令，但我想通过向你展示表 3-1 中的常见 Linux 命令列表，让你感受到命令的广度。它按类别列出常见的 Linux 命令。在开始学习任何 Linux 命令之前，你应该浏览此表。

| Table 3-1 | Overview of Common Linux Commands |
|---|---|
| Command Name | Action |
| **Getting Online Help** | |
| apropos | Finds online manual pages for a specified keyword. |
| info | Displays online help information about a specified command. |
| man | Displays online help information. |
| whatis | Similar to apropos, but searches for complete words only. |
| **Making Commands Easier** | |
| alias | Defines an abbreviation for a long command. |
| type | Shows the type and location of a command. |
| unalias | Deletes an abbreviation defined using alias. |
| | (continued) |

Book II
Chapter 3
Learning the Shell



**表 3-1（续）**

| 命令名称 | 操作 |
|---|---|
| *管理文件和目录* | |
| cd | 更改当前目录。 |
| chmod | 更改文件权限。 |
| chown | 更改文件所有者和组。 |
| cp | 复制文件。 |
| ln | 为文件和目录创建符号链接。 |
| ls | 显示目录的内容。 |
| mkdir | 创建目录。 |
| mv | 重命名文件以及将文件从一个目录移动到另一个目录。 |
| rm | 删除文件。 |
| rmdir | 删除目录。 |
| pwd | 显示当前目录。 |
| touch | 更新文件的时间戳。 |
| *查找文件* | |
| find | 根据指定的条件（如名称、大小等）查找文件。 |
| locate | 使用定期更新的数据库查找文件。 |
| whereis | 在通常存放可执行文件（也称为二进制文件）的典型目录中查找文件。 |
| which | 在 PATH 环境变量列出的目录中查找文件。 |
| *处理文件* | |
| cat | 在标准输出上显示文件（可用于将多个文件连接成一个大文件）。 |
| cut | 从文件中的每一行文本中提取指定的部分。 |
| dd | 从一个文件复制数据块到另一个文件（用于从设备复制数据）。 |
| diff | 比较两个文本文件并查找任何差异。 |

## 处理文件

| 命令名称 | 操作 |
|---|---|
| expand | 将所有制表符转换为空格。 |
| file | 显示文件中的数据类型。 |
| fold | 将每一行文本换行以适应指定的宽度。 |
| grep | 在文本文件中搜索正则表达式。 |
| less | 一页一页地显示文本文件（也可以向后翻）。 |
| lpr | 打印文件。 |
| more | 一页一页地显示文本文件（仅向前）。 |
| nl | 为文本文件中的所有非空白行编号并将行打印到标准输出。 |
| paste | 连接来自多个文件的对应行。 |
| patch | 使用原始文件和修订副本之间的差异更新文本文件。 |
| sed | 在应用指定的编辑命令的同时将文件复制到标准输出。 |
| sort | 对文本文件中的行进行排序。 |
| split | 将文件拆分为几个指定大小的较小文件。 |
| tac | 反转文件（从最后一行开始，依此类推）。 |
| tail | 显示文件的最后几行。 |
| tr | 在整个文件中用另一组字符替换一组字符。 |
| uniq | 从文本文件中删除重复行。 |
| wc | 统计文本文件中的行数、单词数和字符数。 |
| zcat | 显示压缩文件（解压后）。 |
| zless | 一页一页地显示压缩文件（也可以向后翻）。 |
| zmore | 一页一页地显示压缩文件。 |

**表 3-1（续）**

| 命令名称 | 操作 |
|---|---|
| *归档和压缩文件* | |
| compress | 压缩文件。 |
| cpio | 将文件复制到归档文件和从归档文件复制。 |
| gunzip | 解压缩使用 GNU ZIP（gzip）压缩的文件。 |
| gzip | 使用 GNU ZIP 压缩文件。 |
| tar | 创建一个或多个目录中文件的归档（最初用于磁带归档）。 |
| uncompress | 解压缩使用 compress 压缩的文件。 |
| *管理进程* | |
| bg | 在后台运行被中断的进程。 |
| fg | 在前台运行进程。 |
| free | 显示系统中空闲和已使用的内存量。 |
| halt | 关闭 Linux 并停止计算机。 |
| kill | 向进程发送信号（通常用于终止进程）。 |
| ldd | 显示运行程序所需的共享库。 |
| nice | 以较低优先级运行进程（称为 nice 模式）。 |
| ps | 显示当前正在运行的进程列表。 |
| printenv | 显示当前环境变量。 |
| pstree | 类似于 ps，但更清晰地显示父子关系。 |
| reboot | 停止 Linux 然后重新启动计算机。 |
| shutdown | 关闭 Linux。 |
| top | 显示最占用处理器和内存的进程列表。 |
| uname | 显示有关系统和 Linux 内核的信息。 |

| 命令名称 | 操作 |
|---|---|
| *管理用户* | |
| chsh | 更改 shell（命令解释器）。 |
| groups | 打印包含指定用户的组列表。 |
| id | 显示指定用户名的用户和组 ID。 |
| passwd | 更改密码。 |
| su | 启动另一个用户或 root 的新 shell（在不带任何参数调用时）。 |
| *管理文件系统* | |
| df | 汇总所有已挂载存储设备中的可用和空闲空间。 |
| du | 显示磁盘使用信息。 |
| fdformat | 格式化软盘。 |
| fdisk | 分区硬盘。 |
| fsck | 检查和修复文件系统。 |
| mkfs | 创建新的文件系统。 |
| mknod | 创建设备文件。 |
| mkswap | 在文件或磁盘分区中为 Linux 创建交换空间。 |
| mount | 在文件系统中的目录上挂载设备（例如，CD-ROM）。 |
| swapoff | 停用交换空间。 |
| swapon | 激活交换空间。 |
| sync | 将缓冲（保存在内存中）的数据写入文件。 |
| tty | 显示当前终端的设备名称。 |
| umount | 从文件系统卸载设备。 |
| *处理日期和时间* | |
| cal | 显示指定月份或年份的日历。 |
| date | 显示当前日期和时间或设置新的日期和时间。 |

## 成为 root（超级用户）

当你想做任何需要高特权级别的事情（例如，管理你的系统）时，你必须成为 root。通常你以普通用户身份使用你的普通用户名登录。但是，当你需要超级用户的特权时，使用以下命令成为 root：

```
su -
```

That's su 后跟减号（或连字符）。然后 shell 会提示你输入 root 密码。输入密码并按 Enter。

完成后（并且你拥有 root 的所有特权），输入 exit 返回到你的正常用户。

## 管理进程

每次 shell 执行你输入的命令时，它都会启动一个进程。shell 本身就是一个进程。shell 运行的任何脚本或程序也是如此。

使用 ps ax 命令查看进程列表。当你输入 ps ax 时，Bash 会显示当前进程集。以下是 ps ax 命令输出的几行（我还包含了 --cols 132 选项以确保你可以看到每个命令的完整内容）：

```
ps ax --cols 132
  PID TTY   STAT   TIME COMMAND
    1 ?     S      0:04 init
    2 ?     SW     0:00 [keventd]
    3 ?     SW     0:00 [kapmd]
    4 ?     SWN    0:00 [ksoftirqd_CPU0]
    5 ?     SW     0:30 [kswapd]
    ... lines deleted ...
  28550 pts/0 R 0:00 ps ax --cols 132
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_181_0.png)

在此列表中，第一列的标题为 PID，并为每个进程显示一个数字。PID 代表进程 ID（标识），是 Linux 内核分配的顺序号。如果你查看 ps ax 命令的输出，你会看到 init 命令是第一个进程，并且它的 PID 或进程号为 1。这就是为什么 init 被称为“所有进程之母”。

COMMAND 列显示创建每个进程的命令。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_182_0.png)

进程 ID 或进程号在你需要强制停止一个异常进程时很有用。查看输出的 `ps ax` 命令并记下有问题的进程的 `PID`。然后，使用该进程号使用 `kill` 命令。例如，要停止进程号 28550，输入以下命令：

```
kill -9 28550
```

## 处理日期和时间

你可以使用 `date` 命令显示当前日期和时间或设置新的日期和时间。在 shell 提示符下输入 `date` 命令，你会得到类似以下的结果：

```
date
Sat Jul 26 11:58:06 EDT 2003
```

正如你所见，单独的 `date` 命令会显示当前日期和时间。

要设置日期，以 `root` 身份登录，然后输入 `date` 后跟日期和时间，格式为 `MMDDhhmmYYYY`，其中每个字符都是数字。例如，要将日期和时间设置为 2003 年 12 月 31 日晚上 9:30，你需要输入

```
date 123121302003
```

`MMDDhhmmYYYY` 日期和时间格式类似于 24 小时制军用时间，其含义如下：

- MM 是月份的两位数（01 到 12）。
- DD 是月份中日期的两位数（01 到 31）。
- hh 是 24 小时制中的两位数小时（00 为午夜，23 为晚上 11:00）。
- mm 是分钟的两位数（00 到 59）。
- YYYY 是四位数的年份（如 2003）。

另一个有趣的日期相关命令是 `cal`。如果不带任何选项输入 `cal`，它会打印当前月份的日历。如果在 `cal` 后跟一个数字，`cal` 会将该数字视为年份并打印该年的日历。要查看特定年份中特定月份的日历，

提供月份编号（1 = 一月，2 = 二月，以此类推），后跟年份。因此，要查看 2004 年一月的日历，输入以下内容即可获得该月份的日历：

```
cal 1 2004
January 2004
Su Mo Tu We Th Fr Sa
      1  2  3
4  5  6  7  8  9 10
11 12 13 14 15 16 17
18 19 20 21 22 23 24
25 26 27 28 29 30 31
```

## 处理文件

你可以使用 grep 在文本文件中搜索，并使用 more 一次一屏地查看文本文件。例如，要在 /etc/passwd 文件中搜索我的用户名，我使用

```
grep naba /etc/passwd
```

要查看 /etc/inittab 文件，一次一屏，我输入

```
more /etc/inittab
```

每当屏幕暂停时，我按空格键进入下一页。

还有许多其他可在文件上操作的 Linux 命令——大多数针对文本文件，但某些命令也可用于任何文件。接下来我将介绍一些文件处理工具。

### 在文本文件中统计单词和行数

我总是对文件的大小感到好奇。对于文本文件，字符数基本上就是文件的字节大小（因为每个字符占用一个字节的存储空间）。那么单词数和行数呢？

Linux 的 wc 命令派上用场了。wc 命令会显示文本文件中字符、单词和行的总数。例如，尝试以下命令：

```
wc /etc/inittab
     53      229     1666 /etc/inittab
```

第二行显示输出。在此例中，wc 报告 /etc/inittab 文件中有 53 行、229 个单词和 1,666 个字符。如果只想查看文件中的行数，请使用 -l 选项，如下所示：

```
wc -l /etc/inittab
53 /etc/inittab
```

正如你所见，在这种情况下 wc 仅显示行数。

如果不指定文件名，wc 命令会期望从标准输入接收输入。你可以使用 shell 的管道功能将另一个命令的输出传递给 wc。有时这会很有用。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_184_0.png)

假设你想粗略统计系统中运行的进程数。你可以使用 ps ax 命令获取所有进程的列表，但不必手动计数行数，只需将 ps 的输出通过管道传递给 wc，即可自动获得粗略计数：

```
ps ax | wc -l
76
```

这里 ps 命令产生了 76 行输出。因为第一行只是表格列的标题，所以你可以估计系统上大约有 75 个进程正在运行。（当然，这个计数可能也包括运行 ps 和 wc 命令所使用的进程，但谁真的在计数呢？）

### 排序文本文件

你可以使用 sort 命令对文本文件中的行进行排序。要了解 sort 命令的工作方式，首先输入 more /etc/passwd 查看 /etc/passwd 文件的当前内容。现在输入 sort /etc/passwd 查看按字母顺序排序的行。如果想对文件进行排序并将排序后的版本保存到另一个文件，必须使用 Bash shell 的输出重定向功能，如下所示：

```
sort /etc/passwd > ~/sorted.text
```

此命令对 /etc/passwd 文件中的行进行排序，并将输出保存到你主目录中名为 sorted.text 的文件中。

### 从文件中替换或删除字符

另一个有趣的命令是 tr——它在整个文件中用另一组字符替换一组字符（或删除选定的字符）。假设

你偶尔需要在 Red Hat Linux 系统上使用 MS-DOS 文本文件。虽然你可能期望在任何系统上使用文本文件都不会有问题，但有一个问题：DOS 使用回车后跟换行来标记每行的结束，而 Red Hat Linux 只使用换行。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_185_0.png)

在你的 Red Hat Linux 系统上，你可以使用带 -d 选项的 tr 命令去掉 DOS 文本文件中的额外回车。基本上，要将 DOS 文本文件 filename.dos 转换为名为 filename.linux 的 Linux 文本文件，输入以下内容：

```
tr -d '\015' < filename.dos > filename.linux
```

在此命令中，'\015' 表示八进制表示法中回车字符的代码。

### 将文件拆分为多个较小文件

split 命令在你想将文件复制到软盘但文件太大无法放入单个软盘时非常有用。然后你可以使用 split 命令将文件拆分为较小的多个文件，每个文件都可以放入软盘。

默认情况下，split 将 1,000 行放入每个文件中。文件以字母组命名，如 aa、ab、ac 等。你可以为文件名指定前缀。例如，要将名为 huge file.tar 的大文件拆分为可放入多个高密度 3.5 英寸软盘的较小文件，请按如下方式使用 split：

```
split -b 1440k huge file.tar part.
```

此命令将 huge file.tar 文件拆分为 1440K 的块，以便每个块都能放入软盘。该命令创建名为 part.aa、part.ab、part.ac 等的文件。

要将拆分的文件重新组合成单个文件，请使用 cat 命令，如下所示：

```
cat part.?? > huge file.tar
```

## 编写 Shell 脚本

如果你曾经使用过 MS-DOS，你可能还记得 MS-DOS 批处理文件。这些是包含 MS-DOS 命令的文本文件。类似地，shell 脚本也是包含一堆 shell 命令的文本文件。

如果你不是程序员，你可能会对编程感到畏惧。但 shell 编程可以简单到将几个命令存储在一个文件中。现在你可能还写不出复杂的 shell 脚本，但完全可以尝试一个简单的 shell 脚本。

要尝试一点 shell 编程，请在 shell 提示符下完全按照所示输入以下文本，然后在完成后按 Ctrl+D：

```
cd
cat > simple
#!/bin/sh
echo "This script's name is: $0"
echo Argument 1: $1
echo Argument 2: $2
```

cd 命令将当前目录更改为你的主目录。然后 cat 命令显示你输入的内容；在这种情况下，我将输出发送到名为 simple 的文件。按下 Ctrl+D 后，cat 命令结束，你应该再次看到 shell 提示符。你所做的是创建了一个名为 simple 的文件，其中包含以下 shell 脚本：

```
#!/bin/sh
echo "This script's name is: $0"
echo Argument 1: $1
echo Argument 2: $2
```

第一行导致 Linux 运行 Bash shell 程序（其名称为 /bin/bash）。然后 shell 读取脚本中其余的行。

正如大多数 Linux 命令接受命令行选项一样，Bash 脚本也接受命令行选项。在脚本内部，你可以将选项引用为 $1、$2 等。特殊名称 $0 指的是脚本本身的名称。

要运行此 shell 脚本，首先必须使用以下命令使文件可执行（即将其变成程序）：

```
chmod +x simple
```

现在使用以下命令运行脚本：

```
./simple one two
```

此脚本的名称是: ./simple
参数 1: one
参数 2: two

脚本名称前的 ./ 前缀表示 simple 文件位于当前目录。

此脚本仅打印脚本的名称以及用户在脚本名称后输入的前两个命令行选项。

接下来，尝试使用几个参数运行脚本，如下所示：

```
./simple "This is one argument" second-argument third
This script's name is: ./simple
Argument 1: This is one argument
Argument 2: second-argument
```

shell 将双引号内的整个字符串视为单个参数。否则，shell 使用空格作为命令行上参数之间的分隔符。

大多数有用的 shell 脚本比这个简单脚本更复杂，但这个简单练习可以让你大致了解如何编写 shell 脚本。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_187_0.png)

将 Linux 命令放在文件中并使用 chmod 命令使文件可执行。瞧！你已经创建了一个 shell 脚本！

### 第 4 章：浏览 Red Hat Linux 文件系统

### 本章内容

- 了解 Red Hat Linux 文件系统
- 使用 Linux 命令浏览文件系统
- 了解文件权限
- 使用 Linux 命令操作文件和目录

要很好地使用文件和目录，你需要了解分层文件系统的概念。即使你使用 GUI 文件管理器来访问文件和文件夹（文件夹是目录的另一个名称），了解文件系统的概览也会有所帮助。

在本章中，我向你介绍 Linux 文件系统。然后你将学习使用几个 Linux 命令来操作文件和目录。

### 了解 Red Hat Linux 文件系统

像任何其他操作系统一样，Red Hat Linux 将信息组织在文件和目录中。目录反过来包含文件。目录是一种特殊的文件，可以包含其他文件和目录。因为目录可以包含其他目录，所以这种组织文件的方法产生了分层结构。这种文件的分层组织称为文件系统。

Red Hat Linux 文件系统为你提供 PC 中所有存储的统一视图。文件系统有一个单一的根目录，用正斜杠（/）表示。然后是文件和目录的层次结构。文件系统的部分可以位于不同的物理介质上，例如硬盘、软盘和 CD-ROM。图 4-1 说明了 Red Hat Linux 文件系统的概念（在任何 Linux 系统中都相同）以及它如何跨越多个物理设备。

如果你熟悉 MS-DOS 或 Windows，你可能会发现 Red Hat Linux 文件系统中缺少某些东西：Red Hat Linux 中没有驱动器号。所有磁盘驱动器和 DVD/CD-ROM 驱动器都是单个文件系统的一部分。



图 4-1：
Red Hat Linux 文件系统提供了一个统一的存储视图，该视图可能跨越多个驱动器。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_189_0.png)

在 Red Hat Linux 中，您可以使用长文件名（最长 256 个字符），并且文件名区分大小写。通常，这些文件名具有多个扩展名，例如 `sample.tar.Z`。UNIX 文件名可以采用多种形式，例如以下：`index.html`、`Makefile`、`kernel-smp-2.4.18-3.i686.rpm`、`.bash_profile` 和 `httpd_src.tar.gz`。

要定位一个文件，您需要的不只是文件名。您还需要有关目录层次结构的信息。显示通向文件的完整目录层次结构的扩展文件名称为路径名。顾名思义，它是通过文件系统迷宫到达文件的路径。图 4-2 显示了 Red Hat Linux 中文件的典型路径名。

图 4-2：
文件的路径名显示了通向该文件的一系列目录。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_189_1.png)

如图 4-2 所示，路径名具有以下部分：

- 根目录，由正斜杠 (`/`) 字符表示。
- 目录层次结构，每个目录名与前一个目录名之间由正斜杠 (`/`) 字符分隔。最后一个目录名之后会出现一个 `/`。
- 文件名，具有名称和一个或多个可选扩展名。（每个扩展名前都有一个句点。）

Red Hat Linux 文件系统有一组定义良好的顶级目录，其中一些目录具有特定用途。如果您了解这些目录的用途，您会更容易在文件系统中找到方向。您也会变得善于在遇到新情况时猜测特定类型文件的位置。表 4-1 简要描述了 Red Hat Linux 文件系统中的顶级目录。

**表 4-1 Red Hat Linux 文件系统中的顶级目录**

| Directory | Description |
|---|---|
| / | 这是构成文件系统基础的根目录。所有文件和目录在逻辑上都包含在根目录中，无论其物理位置如何。 |
| /bin | 包含 Linux 操作系统的一部分的可执行程序。许多 Linux 命令，例如 cat、cp、ls、more 和 tar，都位于 /bin 中。 |
| /boot | 包含 Linux 内核和其他文件，这些文件是 LILO 和 GRUB 启动管理器所需的（内核和其他文件可以在任何位置，但通常将其放置在 /boot 目录中）。 |
| /dev | 包含代表连接到系统的设备的特殊文件。 |
| /etc | 包含大多数系统配置文件和初始化脚本（位于 /etc/rc.d 子目录中）。 |
| /home | 所有用户的主目录的常规位置。例如，用户 naba 的主目录为 /home/naba。 |
| /lib | 包含存储在 /sbin 和 /bin 目录中的所有程序的库文件，包括启动 Red Hat Linux 所需的可加载驱动程序模块。 |
| /lost+found | 丢失文件的目录。每个磁盘分区都有一个 lost+found 目录。 |
| /mnt | 用于临时挂载文件系统的目录，例如 CD-ROM 驱动器、软盘和 Zip 驱动器。包含用于挂载软盘的 /mnt/floppy 目录和用于挂载 CD-ROM 以及 DVD-ROM 驱动器的 /mnt/cdrom 目录。 |

**表 4-1（续）**

| Directory | Description |
|---|---|
| /opt | 为大型应用程序软件包提供存储区域。 |
| /proc | 一个特殊目录，包含有关 Red Hat Linux 系统各个方面的信息。 |
| /root | root 用户的主目录。 |
| /sbin | 包含代表通常用于系统管理任务的命令且由 root 用户使用的可执行文件。诸如 halt 和 shutdown 之类的命令位于 /sbin 目录中。 |
| /tmp | 任何用户都可以用作临时目录的临时目录，意味着该目录的内容被认为不重要，通常在系统每次启动时都会被删除。 |
| /usr | 包含许多重要程序的子目录，例如 X Window 系统（位于 /usr/X11R6 目录中）和联机手册。表 4-2 显示了 /usr 中一些标准子目录。 |
| /var | 包含各种系统文件（如日志），以及用于保存其他信息（如 Web 服务器和匿名 FTP 服务器的文件）的目录。 |

/usr 和 /var 目录还包含许多标准子目录。表 4-2 列出了 /usr 中的重要子目录。表 4-3 显示了 /var 目录的类似细分。

**表 4-2**
**重要的 /usr 子目录**

| Subdirectory | Description |
|---|---|
| /usr/X11R6 | 包含 XFree86（X Window 系统）软件。 |
| /usr/bin | 包含许多其他 Linux 命令的可执行文件，包括 Linux 中常见但不属于核心 Linux 操作系统的实用程序程序。 |
| /usr/games | 包含一些旧的 Linux 游戏。 |
| /usr/include | 包含 C 和 C++ 编程语言的头文件（文件名以 .h 结尾的文件）；还包括 /usr/include/X11 目录中的 X11 头文件和 /usr/include/linux 目录中的 Linux 内核头文件。 |
| /usr/lib | 包含 C 和 C++ 编程语言的库；还包含许多其他库，例如数据库库、图形工具包库等。 |
| /usr/local | 包含本地文件。例如，/usr/local/bin 目录本应是您系统上开发的任何可执行程序的位置。 |

| Subdirectory | Description |
|---|---|
| `/usr/sbin` | 包含许多管理命令，例如电子邮件和网络命令。 |
| `/usr/share` | 包含共享数据，例如许多应用程序的默认配置文件和图像。例如，`/usr/share/gnome` 包含 GNOME 桌面的各种共享文件；并且 `/usr/share/doc` 包含许多 Linux 应用程序的文档文件（如 Bash shell、Sawfish 窗口管理器和 The GIMP 图像处理程序）。 |
| `/usr/share/man` | 包含联机手册（您可以使用 `man` 命令阅读）。 |
| `/usr/src` | 包含 Linux 内核（核心操作系统）的源代码。 |

表 4-3 重要的 /var 子目录

| Subdirectory | Description |
|---|---|
| `/var/cache` | 应用程序缓存数据的存储区域。 |
| `/var/lib` | 包含与应用程序当前状态相关的信息。 |
| `/var/lock` | 包含锁文件，以确保资源仅由一个应用程序使用。 |
| `/var/log` | 包含组织在子目录中的日志文件。`syslogd` 服务器将其日志文件存储在 `/var/log` 中，其确切内容取决于 `syslog` 配置文件 `/etc/syslog.conf`。例如，`/var/log/messages` 是主系统日志文件，`/var/log/secure` 包含来自安全服务（如 `sshd` 和 `xinetd`）的日志消息，而 `/var/log/maillog` 包含邮件消息的日志。 |
| `/var/mail` | 包含用户邮箱文件。 |
| `/var/opt` | 包含存储在 `/opt` 目录中的软件包的可变数据。 |
| `/var/run` | 包含自系统启动以来描述系统的信息。 |
| `/var/spool` | 包含正在等待某种处理的资料。 |
| `/var/tmp` | 包含系统重启之间保留的临时文件。 |
| `/var/yp` | 包含网络信息服务（NIS）数据库文件。 |

## 使用 Linux 命令导航文件系统

虽然 Nautilus（GNOME 中）或 Konqueror（KDE 中）等 GUI 文件管理器易于使用，但只有在您拥有可用的 GUI 桌面时才能使用它们。有时，您可能没有图形环境来运行图形文件管理器。例如，您可能通过文本终端登录，或者 X 在您的系统上无法工作。在这些情况下，您必须依靠 Linux 命令来处理文件和目录。当然，您始终可以使用 Linux 命令，即使在图形环境中也是如此——您所要做的就是打开一个终端窗口并输入 Linux 命令。

在下面的各节中，我简要介绍了在 Red Hat Linux 文件系统中移动的一些 Linux 命令。

### 目录导航命令

在 Red Hat Linux 中，当您以 root 身份登录时，您的主目录是 /root。对于其他用户，主目录通常位于 /home 目录中。我的主目录（当我以 naba 登录时）是 /home/naba。此信息存储在 /etc/passwd 文件中。默认情况下，只有您有权将文件保存到主目录中，只有您可以在主目录中创建子目录以进一步组织文件。

Linux 支持当前目录的概念，即所有文件和目录命令在其上操作。登录后，例如，您的当前目录是主目录。要查看当前目录，请键入 pwd 命令。

要更改当前目录，请使用 cd 命令。要将当前目录更改为 /usr/share/doc，请键入以下内容：

```
cd /usr/share/doc
```

然后，要将目录更改为 /usr/share/doc 中的 bash-2.05b 子目录，请键入此命令：

```
cd bash-2.05b
```

现在，如果您使用 pwd 命令，该命令将显示 /usr/share/doc/bash-2.05b 作为当前目录。

这两个示例表明您可以以两种方式引用目录的名称：

- 绝对路径名（例如 `/usr/share/doc`），它指定目录树中的确切目录
- 相对目录名（例如 `bash-2.05b`，它表示当前目录的 `bash-2.05b` 子目录，无论当前目录是什么）

如果您在 /usr/share/doc 中键入 cd bash-2.05b，当前目录将更改为 /usr/share/doc/bash-2.05b。但是，如果我在 /home/naba 中键入相同的命令，shell 将尝试将当前目录更改为 /home/naba/bash-2.05b。



Use the cd command without any arguments to change the current directory back to your home directory. No matter where you are, typing cd at the shell prompt brings you back home!

By the way, the tilde character (~) refers to your home directory. Thus the command cd ~ also changes the current directory to your home directory. You can also refer to another user's home directory by appending that user's name to the tilde. Thus, cd ~superman changes the current directory to the home directory of superman.

Wait, there's more. A single dot (.) and two dots (..) — often referred to as dot-dot — also have special meanings. A single dot (.) indicates the current directory, whereas two dots (..) indicate the parent directory. For example, if the current directory is /usr/share, you go up one level to /usr by typing cd ..

## Commands for directory listings and permissions

You can get a directory listing by using the ls command. By default, the ls command — without any options — displays the contents of the current directory in a compact, multicolumn format. For example, type the next two commands to see the contents of the /etc/X11 directory:

```
cd /etc/X11
ls
```

The output looks like this (on the console you'd see some items in different colors):

```
applnk          prefdm          sysconfig       XftConfig.README-OBSOLETE  xserver
desktop-menus   proxymgr        twm             xinit                       xsm
fs              rstart          X               xkb
 gdm             serverconfig    xdm             Xmodmap
lxbproxy        startthere      XF86Config      Xresources
```

From this listing (without the colors), you cannot tell whether an entry is a file or a directory. To tell the directories and files apart, use the -F option with ls and you'll get more clues:

```
ls -F
applnk/         prefdm*         sysconfig/      XftConfig.README-OBSOLETE  xserver/
desktop-menus/  proxymgr/       twm/            xinit/                      xsm/
fs/             rstart/         X@              xkb@
gdm/            serverconfig/   xdm/            Xmodmap
lxbproxy/       startthere      XF86Config      Xresources
```

The output from ls -F shows the directory names with a slash (/) appended to them. Plain filenames appear as is. The at sign (@) appended to the file named X indicates that this file is a link to another file (in other words, this filename simply refers to another file; it's a shortcut). An asterisk (*) is appended to executable files (see, for example, the prefdm file in the listing). The shell can run any executable file.

You can see even more detailed information about the files and directories with the -l option:

```
ls -l
```

For the /etc/X11 directory, a typical output from ls -l looks like the following:

```
total 80
drwxr-xr-x 4 root root 4096 Sep 24 15:52 applnk
drwxr-xr-x 2 root root 4096 Sep 24 14:59 desktop-menus
drwxr-xr-x 2 root root 4096 Sep 24 16:12 fs
drwxr-xr-x 6 root root 4096 Sep 24 15:37 gdm
drwxr-xr-x 2 root root 4096 Sep 24 15:34 lxbproxy
-rwxr-xr-x 1 root root 1298 Sep 4 13:23 prefdm
drwxr-xr-x 2 root root 4096 Sep 24 15:34 proxymgr
drwxr-xr-x 4 root root 4096 Sep 24 15:34 rstart
drwxr-xr-x 2 root root 4096 Jul 10 2001 serverconfig
drwxr-xr-x 2 root root 4096 Jul 10 2001 startthere
drwxr-xr-x 2 root root 4096 Jul 10 2001 sysconfig
drwxr-xr-x 2 root root 4096 Sep 24 15:36 twm
lrwxrwxrwx 1 root root 27 Sep 24 16:28 X -> ../usr/X11R6/bin/XFree86
drwxr-xr-x 3 root root 4096 Sep 24 15:56 xdm
-rw-r--r-- 1 root root 3323 Sep 24 16:20 XF86Config
< lines deleted >
drwxr-xr-x 2 root root 4096 Sep 24 15:34 xsm
```

This listing shows considerable information about every directory entry — each of which can be a file or another directory. Looking at a line from the right column to the left, you see that the rightmost column shows the name of the directory entry. The date and time before the name show when the last modifications to that file were made. To the left of the date and time is the size of the file, in bytes.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_195_0.png)

The file's group and owner appear to the left of the column that shows the file size. The next number to the left indicates the number of links to the file. (A link is like a shortcut in Windows.) Finally, the leftmost column shows the file's permission settings, which determine who can read, write, or execute the file.

The first letter of the leftmost column has a special meaning, as the following list shows:

- If the first letter is l, the file is a symbolic link (a shortcut) to another file.
- If the first letter is d, the file is a directory.
- If the first letter is a dash (-), the file is normal.
- If the first letter is b, the file represents a block device, such as a disk drive.
- If the first letter is c, the file represents a character device, such as a serial port or a terminal.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_196_0.png)

After that first letter, the leftmost column shows a sequence of nine characters. This appears as `rwxrwxrwx` when each letter is present. Each letter indicates a specific permission. A hyphen (-) in place of a letter indicates no permission for a specific operation on the file. Think of these nine letters as three groups of three letters (rwx), interpreted as follows:

- The leftmost group of rwx controls the read, write, and execute permission of the file's owner. In other words, if you see rwx in this position, the file's owner can read (r), write (w), and execute (x) the file. A hyphen in place of a letter indicates no permission. Thus the string rw- means the owner has read and write permission but no execute permission. Although executable programs (including shell programs) typically have execute permission, directories treat execute permission as equivalent to use permission — a user must have execute permission on a directory before he or she can open and read the contents of the directory.
- The middle three rwx letters control the read, write, and execute permission of any user belonging to that file's group.
- The rightmost group of rwx letters controls the read, write, and execute permission of all other users (collectively referred to as the world).

Thus, a file with the permission setting `rwx------` is accessible only to the file's owner, whereas the permission setting `rwxr-xr--` makes the file readable by the world.

An interesting feature of the `ls` command is that it does not list any file whose name begins with a period. To see these files, you must use the `ls` command with the `-a` option, as follows:

```
ls -a
```

Try this command in your home directory (and then compare the result with what you see when you don't use the -a option):

- 1. Type cd to change to your home directory.
- 2. Type ls -F to see the files and directories in your home directory.
- 3. Type ls -aF to see everything, including the hidden files.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_197_0.png)

Most Linux commands take single-character options, each with a minus sign (think of this sign as a hyphen) as a prefix. When you want to use several options, type a hyphen and concatenate (string together) the option letters, one after another. Thus, ls -al is equivalent to ls -a -l as well as ls -a -l.

## Commands for changing permissions and ownerships

You may need to change a file's permission settings to protect it from others. Use the chmod command to change the permission settings of a file or a directory.

To use chmod effectively, you have to learn how to specify the permission settings. A good way is to concatenate letters from the columns of Table 4-4 in the order shown (Who/Action/Permission).

Note: You use only the single character from each column — the text in parentheses is for explanation only.

Table 4-4 Letter Codes for File Permissions

| Who | Action | Permission |
|---|---|---|
| u (user) | + (add) | r (read) |
| g (group) | - (remove) | w (write) |
| o (others) | = (assign) | x (execute) |
| a (all) | s (set user ID) |  |

For example, to give everyone read access to all files in a directory, pick a (for all) from the first column, + (for add) from the second column, and r (for read) from the third column to come up with the permission setting a+r. Then use the whole set of options with chmod, like this:

```
chmod a+r *.
```

On the other hand, to permit everyone to execute one specific file, type

```
chmod a+x filename
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_197_1.png)

Suppose you have a file named mystuff that you want to protect. You can make it accessible to no one but you if you type the following commands, in this order:

```
chmod a-rwx mystuff
```

```
chmod u+rw mystuff
```



The first command turns off all permissions for everyone, and the second command turns on the read and write permissions for the owner (you). Type ls -l to verify that the change took place (you should see a permission setting of -rw------). Here's a sample output from ls -l:

```
-rw------ 1 naba naba 3 Jun 30 18:45 mystuff
```

Note the third and fourth fields that show naba naba. These two fields show the file's user and group ownership. In this case, the name of the user is naba and the name of the group is naba as well (because Red Hat Linux creates a group for each user).

Sometimes you have to change a file's user or group ownership for everything to work correctly. For example, suppose you are instructed (by a manual, what else) to create a directory named cups and give it the ownership of user ID lp and group ID sys. How would you do it?

Well, you can log in as root and create the directory with the command mkdir:

```
mkdir cups
```

If you check the file's details with the ls -l command, you see that the user and group ownership is root root.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_198_0.png)

To change the owner, use the chown command. For example, to change the ownership of the cups directory to user ID lp and group ID sys, type

```
chown lp.sys cups
```

## Commands for working with files

要从一个目录复制文件到另一个目录，请使用 cp 命令。例如，要将文件 /usr/X11R6/lib/X11/xinit/Xclients 复制到当前目录（例如你的主目录）中的 Xclients.sample 文件，请输入以下内容：

```
cp /usr/X11R6/lib/X11/xinit/Xclients Xclients.sample
```

如果要将文件复制到当前目录但保留原始名称，请将句点（.）用作 cp 命令的第二个参数。因此，以下命令将 /etc/X11 目录中的 XF86Config 文件复制到当前目录（用单个句点表示）：

```
cp /etc/X11/XF86Config .
```

cp 命令会制作文件的新副本并保留原文件不变。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_199_0.png)

如果要将目录的全部内容（包括所有子目录及其内容）复制到另一个目录，请使用命令 cp -ar sourcedir destdir（这会将 sourcedir 目录下的所有内容复制到 destdir）。例如，要将 /etc/X11 目录中的所有文件复制到当前目录，请输入以下命令：

```
cp -ar /etc/X11 .
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_199_1.png)

要将文件移动到新位置，请使用 mv 命令。原始副本将被删除，目标位置会出现新副本。你可以使用 mv 重命名文件。如果要将 today.list 的名称更改为 old.list，请按如下方式使用 mv 命令：

```
mv today.list old.list
```

另一方面，如果要将 today.list 文件移动到名为 saved 的子目录，请使用此命令：

```
mv today.list saved
```

mv 的一个有趣功能是，你可以使用它将整个目录（连同其所有子目录和文件）移动到新位置。如果有一个名为 data 的目录包含许多文件和子目录，你可以使用以下命令将整个目录结构移动到 old_data：

```
mv data old_data
```

要删除文件，请使用 rm 命令。例如，要删除名为 old.list 的文件，请输入以下命令：

```
rm old.list
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_199_2.png)

请小心使用 rm 命令——尤其是在以 root 身份登录时。使用 rm 很容易无意中删除重要文件。

## Commands for working with directories

为了在主目录中组织文件，你必须创建新目录。使用 mkdir 命令创建目录。例如，要在当前目录中创建名为 images 的目录，请输入以下内容：

```
mkdir images
```

创建目录后，你可以使用 cd images 命令切换到该目录。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_200_0.png)

你可以使用 mkdir 命令的 -p 选项创建整个目录树。例如，假设你的系统有 /usr/src 目录，你想创建目录树 /usr/src/book/java/examples/applets。要创建此目录层次结构，请输入以下命令：

```
mkdir -p /usr/src/book/java/examples/applets
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_200_1.png)

当你不再需要目录时，请使用 rmdir 命令删除它。

你只能在目录为空时删除目录。

要删除空目录树，可以使用 -p 选项，如下所示：

```
rmdir -p /usr/src/book/java/examples/applets
```

此命令会删除 applets 的空父目录。命令在遇到非空目录时停止。

## Commands for finding files

find 命令对于查找符合搜索条件的 文件（和目录）非常有用。

当我多年前开始使用 UNIX（20 世纪 80 年代初的 Berkeley UNIX）时，find 命令让我困惑。我很长时间都只使用一种基本的 find 语法，然后才逐渐使用更复杂的语法。我最初学到的基本语法是用于在整个文件系统中查找文件。方法如下：假设你想查找名称以 gnome 开头的任何文件或目录。输入以下 find 命令来查找这些文件：

```
find / -name "gnome*" -print
```

如果未以 root 身份登录，你可能会收到一堆错误消息。如果这些错误消息让你烦恼，只需按如下方式修改命令，错误消息就会成为历史（或者，正如 UNIX 爱好者所说，将它们发送到位桶）：

```
find / -name "gnome*" -print 2> /dev/null
```

此命令告诉 find 从根目录（/）开始查找，查找与 gnome* 匹配的文件名，并显示任何匹配文件的完整路径名。最后一部分（2> /dev/null）只是将错误消息发送到一个特殊文件，这相当于直接忽略它们。

你可以使用这种简单形式的 find 的变体来定位任何目录（以及该目录包含的任何子目录）中的文件。如果你忘记了在主目录中存储了所有名为 report*（名称以 report 开头）的文件的位置，可以使用以下命令搜索文件：

```
find ~ -name "report*" -print
```

当你熟悉这种 find 语法后，就可以使用 find 的其他选项。例如，要仅查找特定类型的文件（如目录），请使用 type 选项。以下命令显示 Linux 系统中的所有顶级目录名称：

```
find / -type d -maxdepth 1 -print
```

在典型的 Linux 系统中，你可能不需要使用 find 的复杂形式——但如果需要，你可以使用以下命令查找其余的 find 选项：

```
man find
```

## Commands for mounting and unmounting

假设你想在文本控制台登录时（没有 GUI 帮助你）访问本书附带的 DVD 上的文件。为此，你必须先将 DVD 驱动器的文件系统挂载到 Red Hat Linux 文件系统中的特定目录上。

以 root 身份登录（或输入 su - 成为 root），将 DVD 插入 DVD 驱动器，然后输入以下命令：

```
mount /dev/cdrom /mnt/cdrom
```

此命令将名为 /dev/cdrom 的设备（指 CD-ROM 以及 DVD-ROM 驱动器）上的文件系统挂载到 Linux 文件系统中的 /mnt/cdrom 目录（也称为挂载点）上。

mount 命令成功完成后，你可以通过将 /mnt/cdrom 目录视为光盘的顶级目录来访问 DVD 上的文件。换句话说，要查看 DVD 的内容，请输入

```
ls -F /mnt/cdrom
```

使用完 DVD 后——并且在从驱动器弹出之前——你必须使用以下 umount 命令“卸载”光盘驱动器：

```
umount /dev/cdrom
```

通常在 /mnt 目录中的目录上挂载设备。Red Hat Linux 附带两个预定义目录：/mnt/cdrom 用于挂载 DVD，/mnt/floppy 用于挂载软盘驱动器。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_202_0.png)

## Commands for checking disk-space usage

我想告诉你两个命令——df 和 du——你可以用它们来检查系统的磁盘空间使用情况。这些命令使用简单。df 命令显示所有已挂载设备的磁盘空间使用情况摘要，如以下示例所示：

```
df
```

| 文件系统 | 1K-块 | 已用 | 可用 | 使用% | 挂载点 |
|------------|-----------|------|-----------|------|------------|
| /dev/hda5 | 7392428 | 3583420 | 3433492 | 52% | / |
| /dev/hda3 | 101107 | 9322 | 8656 | 10% | /boot |
| none | 127376 | 0 | 127376 | 0% | /dev/shm |
| /dev/cdrom | 658144 | 658144 | 0 | 100% | /mnt/cdrom |

输出是一个表格，显示设备、存储总千字节、使用量、可用量、使用百分比和挂载点。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_202_1.png)

要以更易读的格式查看 df 的输出，请输入 df -h。以下是 df -h 命令的输出：

```
df -h
```

| 文件系统 | 大小 | 已用 | 可用 | 使用% | 挂载点 |
|------------|------|------|-------|------|------------|
| /dev/hda5 | 7.1G | 3.5G | 3.3G | 52% | / |
| /dev/hda3 | 99M | 9.2M | 85M | 10% | /boot |
| none | 125M | 0 | 125M | 0% | /dev/shm |
| /dev/cdrom | 643M | 643M | 0 | 100% | /mnt/cdrom |

如果你将此输出与普通 df 的输出（见上一个列表）进行比较，你会看到 df -h 使用 M 表示兆字节、G 表示千兆字节等术语打印大小。这显然比 1K-blocks 更容易理解。

另一个命令——du——对于查找目录占用多少空间很有用。例如，输入以下命令来查看

/etc/rc.d 目录中所有目录的内容（该目录包含系统启动文件）：

```
du /etc/rc.d
288   /etc/rc.d/init.d
4     /etc/rc.d/rc0.d
4     /etc/rc.d/rc1.d
4     /etc/rc.d/rc2.d
4     /etc/rc.d/rc3.d
4     /etc/rc.d/rc4.d

4     /etc/rc.d/rc5.d
4     /etc/rc.d/rc6.d
352   /etc/rc.d
```

每个目录名称前面都有一个数字——它告诉你该目录使用的磁盘空间的千字节数。因此，整个 /etc/rc.d 目录使用 352K 磁盘空间，而 /etc/rc.d/init.d 子目录使用 288K。如果您只想知道目录使用的总磁盘空间（包括该目录包含的所有文件和子目录），请使用 -s 选项，如下所示：

```
du -s /etc/rc.d
352   /etc/rc.d
```

-s 选项会导致 du 仅打印 /etc/rc.d 目录的汇总信息。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_203_0.png)

正如 df -h 以兆字节和千兆字节打印磁盘空间信息一样，您可以使用 du -h 命令以更易于人类阅读的形式查看 du 的输出。例如，以下是我如何将其与 -s 选项结合使用，以查看我的主目录 (/home/naba) 中使用的空间：

```
du -sh /home/naba
29M   /home/naba
```

### 第 5 章：探索 Red Hat Linux 应用程序

### 本章内容

- ✓ 盘点 Red Hat Linux 应用程序
- ✓ 探索办公应用程序
- ✓ 设置数据库
- ✓ 体验多媒体
- ✓ 处理图像

Red Hat Linux 附带了大量应用程序。您只需查看 GNOME 或 KDE 中的菜单就会明白我的意思。通常，每种类型都有不止一个应用程序。GNOME 和 KDE 都附带了 OpenOffice.org 办公应用程序套件，其中包含文字处理器和电子表格软件。还有许多 CD 播放器和多媒体播放器的选择，不提及游戏和实用程序，以及扫描仪和数码相机应用程序等有用工具。

我概述了一些这些应用程序，并简要展示了一些有趣且有用的应用程序。在了解了这些应用程序后，您可以在需要时尝试它们。

### 盘点 Red Hat Linux 应用程序

表 5-1 显示了按类别组织的 Red Hat Linux 主要应用程序的采样。对于主要应用程序，我还显示了您可以获取有关该应用程序更多信息的相关网站。此列表绝不全面。Red Hat Linux 发行版附带的应用程序和实用程序比我在本表中显示的要多得多。

如果您的系统同时安装了 GNOME 和 KDE，那么大多数这些应用程序应该已经可以通过任一 GUI 桌面获得。

我简要介绍了表 5-1 中的一些应用程序，从每个类别中选择一两个。我在第 V 书中描述了 Internet 应用程序。

**表 5-1 Red Hat Linux 应用程序示例**

| 应用程序 | 描述 |
|---|---|
| *办公应用程序* | |
| OpenOffice.org Writer | 一个免费的文字处理程序，类似于 Microsoft Word (www.openoffice.org) |
| OpenOffice.org Calc | 一个类似于 Microsoft Excel 的电子表格程序 (www.openoffice.org) |
| OpenOffice.org Impress | 一个类似于 Microsoft PowerPoint 的演示应用程序 (www.openoffice.org) |
| OpenOffice.org Draw | 一个绘图程序 (www.openoffice.org) |
| OpenOffice.org Math | 一个用于编写数学方程的公式编辑器，您可以将其包含在 OpenOffice.org Writer 文档中 (www.openoffice.org) |
| Dia | 一个绘图程序，设计为类似于 Windows 应用程序 Visio (www.gnome.org/gnome-office/dia.shtml) |
| *办公工具* | |
| GNOME Calculator | 一个简单的计算器 |
| KCalc | 一个计算器（KDE 的一部分） |
| Aspell | 一个文本模式拼写检查器 (aspell.sourceforge.net) |
| Dictionary | 一个用于查询单词的 dict.org 字典服务器的图形客户端 |
| *数据库* | |
| PostgreSQL | 一个支持结构化查询语言（SQL）的高级对象关系数据库管理系统 (www.pgsql.com) |
| MySQL | 一个流行的支持 SQL 的关系数据库管理系统 (www.mysql.com) |
| *多媒体* | |
| GNOME CD Player | 一个音频 CD 播放器（需要工作的声卡） |
| KsCD | 来自 KDE 的音频 CD 播放器（需要工作的声卡） |
| XMMS | X 多媒体系统 — 一个可播放多种不同声音格式的多媒体音频播放器 (www.xmms.org) — 如果您下载插件以用于此目的，包括 MP3 文件 |
| Cdrecord | 一个命令行应用程序，可刻录音频和数据 CD-R 以及 DVD-R (http://www.fokus.gmd.de/research/cc/glone/employees/joerg.schilling/private/cdrecord.html) |
| GnomeToaster | 一个 cdrecord 和 cdrdao 的 GUI 前端，使刻录数据和音频 CD 变得容易 (gnometoaster.rulez.org) |
| Grip | 一个 GUI 实用程序，可从音频 CD 提取音轨并保存为 Ogg Vorbis 文件，您可以使用媒体播放器播放或刻录到音频 CD (www.nostatic.org/grip) |
| Gtkam | 一个与 150 多种数码相机兼容的数码相机应用程序 (gphoto.sourceforge.net/proj/gtkam/) |
| *图形和图像* | |
| The GIMP | GNU 图像处理程序，适用于照片润饰、图像合成和图像创作等任务 (www.gimp.org) |
| GQView | 一个功能强大的图像查看器 (gqview.sourceforge.net) |
| Kview | KDE 的一个简单图像查看器 |
| Kghostview | 一个 PostScript 和 PDF 文件查看器 |
| Xsane | 一个用于使用 SANE（Scanner Access Now Easy）库访问扫描仪的图形前端 (www.xsane.org) |
| Ksnapshot | 一个屏幕捕获程序 |
| *互联网* | |
| Ximian Evolution | 一个个人信息管理应用程序，集成电子邮件、日历、联系人管理和在线任务列表 (www.ximian.com/products/ximian_evolution) |
| GFTP | 一个用于从互联网下载文件的 FTP 客户端 |
| Gaim | 一个 AOL 即时通讯客户端 (gaim.sourceforge.net) |
| Mozilla | 一个著名的开源网页浏览器，源自 Netscape 的源代码 (www.mozilla.org) |
| KMail | KDE 的电子邮件客户端 (kmail.kde.org) |

### 办公应用程序和工具

文字处理器、电子表格、演示软件、日历、计算器——这些是办公室的支柱。GNOME 和 KDE 都附带了 OpenOffice.org（通常缩写为 OO.o 或 Ooo）办公应用程序和工具套件。您可以逐一尝试所有这些，看看哪个更合您心意。每个应用程序都相当直观易用。即使用户界面的某些细微差别对您来说是新的，您也可以在几次使用后学会。我在本节中简要介绍以下几个应用程序：

- OpenOffice.org Writer — 一个类似 Microsoft Word 的文字处理器
- OpenOffice.org Calc — 一个类似 Microsoft Excel 的电子表格程序
- OpenOffice.org Impress — 一个类似 Microsoft PowerPoint 的演示程序
- OpenOffice.org Draw — 一个绘图和插图应用程序
- OpenOffice.org Math — 一个数学公式编辑器
- 计算器 — GNOME 计算器和 KDE 计算器
- aspell — 一个拼写检查器
- Linux 的商业办公应用程序

我在第 III 书的单独章节中介绍了 OpenOffice.org 应用程序。请翻到那本书以了解有关 Writer、Calc、Impress、Draw 和 Math 的更多信息。

### 计算器

您可以选择 GNOME 计算器或 KDE 计算器。两者都是科学计算器，您可以进行典型的科学计算，例如平方根和倒数，以及三角函数，例如正弦、余弦和正切。

要运行 GNOME 计算器，请从 GNOME 桌面选择 主菜单→附件→计算器。图 5-1 显示了 GNOME 计算器。

图 5-1：
在 GNOME 计算器上进行计算。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_207_0.png)



KDE 计算器比 GNOME 计算器功能更强大。例如，它可以以十六进制、十进制、八进制和二进制格式进行计算。从 KDE 桌面，你可以通过选择“主菜单→附件→科学计算器”启动 KDE 计算器。图 5-2 显示了 KDE 计算器。

Figure 5-2:
谁要算平方根？
在 KDE 计算器上算吧。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_208_0.png)

## 适用于 Linux 的商业办公应用程序

由于办公应用程序对许多企业和个人都很重要，我想简要介绍一些适用于 Red Hat Linux 的商业办公应用程序。这些商业产品包括 Anyware Office（前称 Applixware Office）和 StarOffice。这些产品确实需要付费，但费用通常低于 Microsoft Office——Windows 领先的办公套件。（如果您不知道，Microsoft Office 是一组应用程序的集合：用于文字处理的 Microsoft Word、用于电子表格的 Microsoft Excel、用于演示图形的 Microsoft PowerPoint 以及用于数据库的 Microsoft Access。）

另一款近期面向 Linux 的商业产品是 CodeWeavers 的 CrossOver Office。使用 CrossOver Office，您可以在 Linux 和 X Window 系统下运行现有的 Microsoft Office 应用程序，如 Word、Excel 和 PowerPoint。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_208_1.png)

本书的附带 DVD 未包含这些适用于 Red Hat Linux 的商业办公应用程序，但我在接下来的几节中简要介绍了它们。您可以在各厂商的网站上了解更多产品信息。

### Anyware Office

Anyware Office，前身为 Applixware Office，是适用于所有 Linux 发行版（包括 Red Hat Linux）的另一款知名办公套件。

2000 年 4 月，Applix, Inc. 成立了一个专门专注于 Linux 应用程序的独立部门——VistaSource, Inc.。

与其他办公套件类似，Anyware Office 包括 Words（文字处理）、Spreadsheets（电子表格）以及 Graphics and Presentations（演示图形）。此外，它还提供 Mail（电子邮件界面）和 Data（交互式关系数据库浏览工具）。Anyware Office 还可以读取和写入 Microsoft Office 和 Corel WordPerfect 格式的文档，以及多种其他文件格式。虽然不提供试用版，但整个 Anyware Office 套件在美国的售价目前低于 100 美元。

您可以在 VistaSource 网站（www.vistasource.com/products）了解更多关于 Applixware 的信息。

### StarOffice

StarOffice 是另一款商业办公套件；它由德国汉堡的 StarDivision 创建，并最近被 Sun Microsystems 收购。StarOffice 是一款跨平台解决方案——它可在 Linux、Windows 95/98/Me/NT/2000/XP、Sun Solaris SPARC 和 Sun Solaris x86 上运行。此外，StarOffice 提供多种语言版本：英语、法语、德语、西班牙语、意大利语和瑞典语。

StarOffice 的独特之处在于它将所有组件集成到一个通用桌面中，您可以从中打开新文档、将文档从一个应用程序拖放到另一个应用程序，并访问互联网。StarOffice 6.0 包含以下内容：

- 用于文字处理的 StarOffice Writer（兼容 Microsoft Word）
- 用于电子表格的 StarOffice Calc（兼容 Microsoft Excel）
- 用于演示的 StarOffice Impress（兼容 Microsoft PowerPoint）
- 用于矢量图形绘制的 StarOffice Draw
- 用于数据管理的 StarOffice Base

您可以从 www.sun.com/staroffice 购买 StarOffice。您也可以在同一网址找到 Sun 的 StarOffice 许可政策详情。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_209_0.png)

2000 年 10 月，Sun 在开源许可下发布了 StarOffice 的源代码。Sun 支持的开源项目 OpenOffice.org 于 2002 年 5 月发布了 OpenOffice.org 1.0 办公生产力套件。Red Hat Linux 附带 OpenOffice.org 1.0.2。要了解更多关于 OpenOffice.org 的信息，请参阅第三册，同时访问 www.openoffice.org。

### CrossOver Office

很可能您的 PC 上已安装 Windows 和 Microsoft Office。当您决定在 PC 上运行 Red Hat Linux 时，您仍可从 GNOME 或 KDE 桌面继续运行大多数 Microsoft Office 应用程序。在 Linux 中运行 Microsoft Office 的便利性来自一款名为 CrossOver Office 的商业产品。

来自 CodeWeavers 的 CrossOver Office 是一个软件包，可让您在 Linux 中安装 Microsoft Office 应用程序（仅限 Office 97 或 Office 2000，不支持 Office XP）。使用 CrossOver Office 运行 Office 应用程序无需 Microsoft Windows。您只需安装 CrossOver Office，然后从 CD-ROM 安装 Microsoft Office 即可。安装 Microsoft Office 后，Office 应用程序将直接从 GNOME 或 KDE 桌面可用。

CrossOver Office 使用 Wine——一个使用 X Window System 实现的 Windows Win32 和 Win16 应用程序编程接口（API）的开源实现，设计用于在 UNIX 和 Linux 系统中运行。Wine 包括 Wine loader 和 WineLib。Wine loader 可以加载和运行 Windows 应用程序。WineLib 用于在 Linux 中编译和链接 Windows 应用程序。Wine 可免费从 www.winehq.com 获取。

CodeWeavers 使用 Wine 的定制版本创建了 CrossOver Office，以确保 Microsoft Office 应用程序，尤其是来自 Office 97 或 Office 2000 的 Microsoft Word、Excel 和 PowerPoint 在 Wine 上正常运行。CodeWeavers 对 CrossOver Office 收取少量费用——单份的标价为 54.95 美元（多份购买费用更低）——但对 Wine 的所有更改都会返还给 Wine 项目。因此，Wine 开源项目从 CrossOver Office 的销售中受益。

您可以在 CodeWeavers 网站（www.codeweavers.com/products/office/）了解更多关于 CrossOver Office 的信息并购买它。

## aspell spelling checker

aspell 工具是一个交互式拼写检查器。您可以使用它检查文本文件中单词的拼写。为此，只需在终端窗口中输入以下命令：

```
aspell check filename
```

如果您想试用 aspell，请键入一些笔记并将其保存到名为 notes.txt 的文本文件中（文件名可以是任意的，但我在讨论中使用此文件名）。要对该文件运行拼写检查器，请在终端窗口中输入以下命令：

```
aspell check notes.txt
```

这条笔记描述了 8 月 16 日会议上达成的 *concensus*。
1) consensus      6) consensual
2) con census      7) consciences
3) con-census      8) incenses
4) condenses       9) consensus's
5) concerns        0) consensuses
i) Ignore          I) Ignore all
r) Replace         R) Replace all
a) Add             x) Exit
?

从第二行开始的所有内容都是 aspell 显示的内容。当 aspell 找到一个拼写错误的单词（不在其词典中的任何单词）时，它会显示包含该拼写错误单词（concensus）的句子，并通过用一对星号将其括起来来突出显示该单词。在该句子下方，aspell 列出可能的更正，并从 1 开始依次编号。在这种情况下，aspell 将 consensus——正确的选择——列为 concensus 的第一个更正。

在选项列表末尾，aspell 显示另外 16 个选项的列表——十个编号为 0 到 9，六个标记为单个字母 i、r、a、I、R 和 x——后面跟着一个问号提示。您必须按输出中显示的列表中的一个数字或字母，以指示您希望 aspell 执行的操作。编号选项显示拼写错误单词的十个可能的替换词。以下是字母选项的含义：

- 空格表示本次接受该词。
- i 表示忽略拼写错误的单词。
- I 表示忽略该单词的所有出现。
- r 表示替换此出现（您必须键入替换词）。
- R 表示替换所有出现（您必须键入替换词）。
- a 表示接受该词并将其添加到您的私人词典。
- x 表示保存文件的其余部分并退出，忽略拼写错误。

这些选项区分大小写。请确保未启用大写锁定。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_211_0.png)

## Databases

Red Hat Linux 附带两个关系数据库——PostgreSQL 和 MySQL。我将简要向您展示如何使用 MySQL。



MySQL（读作 My Ess Que Ell）是一种流行的关系型数据库（以互联表格集合形式工作的数据库类型）。你可以使用结构化查询语言（SQL）来操作数据库。

一家名为 MySQL AB 的瑞典公司开发了 MySQL（www.mysql.com）。MySQL AB 已将其作为开源产品发布。

检查系统是否已安装 MySQL，输入 rpm -q mysql。如果消息提示软件包未安装，可以使用以下步骤从 DVD 安装：

- 1. 以 root 身份登录并将 DVD 插入光驱。

如果使用 GNOME 或 KDE，DVD 应自动挂载。如果没有，请在终端窗口中输入以下命令挂载 DVD：

```
mount /mnt/cdrom
```

- 2. 输入以下命令安装 MySQL：

```
cd /mnt/cdrom/RedHat/RPMS
rpm -ivh mysql*
```

这将安装使用 MySQL 所需的所有软件包。

要使用 MySQL，首先必须以 root 身份登录并使用以下命令启动数据库服务器：

```
/etc/init.d/mysqld start
```

数据库服务器 mysqld 是一个守护进程（持续运行的后台进程），它接受来自 MySQL 监视器的数据库查询。

现在你需要设计一个数据库，在 MySQL 中创建该数据库并加载数据。为了说明如何创建和加载数据库，我设置了一个简单的图书目录数据库。

## 构建数据库的步骤回顾

按照以下基本步骤序列构建数据库：

- 1. 设计数据库。

这涉及定义用于存储信息的表和属性。

- 2. 创建一个空数据库。

在添加表之前，数据库系统要求你先构建一个空数据库。

### 3. 在数据库中创建表。

在此步骤中，你使用 SQL 的 CREATE TABLE 语句定义表。

### 4. 为表加载任何固定数据。

例如，如果你有一个制造商名称表或出版商名称表（以书籍为例），你希望用已知的[content]
MySQL（读作 My Ess Que Ell）是一种流行的关系型数据库（以互联表格集合形式工作的数据库类型）。你可以使用结构化查询语言（SQL）来操作数据库。

一家名为 MySQL AB 的瑞典公司开发了 MySQL（www.mysql.com）。MySQL AB 已将其作为开源产品发布。

检查系统是否已安装 MySQL，输入 rpm -q mysql。如果消息提示软件包未安装，可以使用以下步骤从 DVD 安装：

- 1. 以 root 身份登录并将 DVD 插入光驱。

如果使用 GNOME 或 KDE，DVD 应自动挂载。如果没有，请在终端窗口中输入以下命令挂载 DVD：

```
mount /mnt/cdrom
```

- 2. 输入以下命令安装 MySQL：

```
cd /mnt/cdrom/RedHat/RPMS
rpm -ivh mysql*
```

这将安装使用 MySQL 所需的所有软件包。

要使用 MySQL，首先必须以 root 身份登录并使用以下命令启动数据库服务器：

```
/etc/init.d/mysqld start
```

数据库服务器 mysqld 是一个守护进程（持续运行的后台进程），它接受来自 MySQL 监视器的数据库查询。

现在你需要设计一个数据库，在 MySQL 中创建该数据库并加载数据。为了说明如何创建和加载数据库，我设置了一个简单的图书目录数据库。

## 构建数据库的步骤回顾

按照以下基本步骤序列构建数据库：

- 1. 设计数据库。

这涉及定义用于存储信息的表和属性。

- 2. 创建一个空数据库。

在添加表之前，数据库系统要求你先构建一个空数据库。

### 3. 在数据库中创建表。

在此步骤中，你使用 SQL 的 CREATE TABLE 语句定义表。

### 4. 为表加载任何固定数据。

例如，如果你有一个制造商名称表或出版商名称表（以书籍为例），你希望用已知的[content]
MySQL（读作 My Ess Que Ell）是一种流行的关系型数据库（以互联表格集合形式工作的数据库类型）。你可以使用结构化查询语言（SQL）来操作数据库。

一家名为 MySQL AB 的瑞典公司开发了 MySQL（www.mysql.com）。MySQL AB 已将其作为开源产品发布。

检查系统是否已安装 MySQL，输入 rpm -q mysql。如果消息提示软件包未安装，可以使用以下步骤从 DVD 安装：

- 1. 以 root 身份登录并将 DVD 插入光驱。

如果使用 GNOME 或 KDE，DVD 应自动挂载。如果没有，请在终端窗口中输入以下命令挂载 DVD：

```
mount /mnt/cdrom
```

- 2. 输入以下命令安装 MySQL：

```
cd /mnt/cdrom/RedHat/RPMS
rpm -ivh mysql*
```

这将安装使用 MySQL 所需的所有软件包。

要使用 MySQL，首先必须以 root 身份登录并使用以下命令启动数据库服务器：

```
/etc/init.d/mysqld start
```

数据库服务器 mysqld 是一个守护进程（持续运行的后台进程），它接受来自 MySQL 监视器的数据库查询。

现在你需要设计一个数据库，在 MySQL 中创建该数据库并加载数据。为了说明如何创建和加载数据库，我设置了一个简单的图书目录数据库。

## 构建数据库的步骤回顾

按照以下基本步骤序列构建数据库：

- 1. 设计数据库。

这涉及定义用于存储信息的表和属性。

- 2. 创建一个空数据库。

在添加表之前，数据库系统要求你先构建一个空数据库。

### 3. 在数据库中创建表。

在此步骤中，你使用 SQL 的 CREATE TABLE 语句定义表。

### 4. 为表加载任何固定数据。

例如，如果你有一个制造商名称表或出版商名称表（以书籍为例），你希望用已知的[content]
MySQL（读作 My Ess Que Ell）是一种流行的关系型数据库（以互联表格集合形式工作的数据库类型）。你可以使用结构化查询语言（SQL）来操作数据库。

一家名为 MySQL AB 的瑞典公司开发了 MySQL（www.mysql.com）。MySQL AB 已将其作为开源产品发布。

检查系统是否已安装 MySQL，输入 rpm -q mysql。如果消息提示软件包未安装，可以使用以下步骤从 DVD 安装：

- 1. 以 root 身份登录并将 DVD 插入光驱。

如果使用 GNOME 或 KDE，DVD 应自动挂载。如果没有，请在终端窗口中输入以下命令挂载 DVD：

```
mount /mnt/cdrom
```

- 2. 输入以下命令安装 MySQL：

```
cd /mnt/cdrom/RedHat/RPMS
rpm -ivh mysql*
```

这将安装使用 MySQL 所需的所有软件包。

要使用 MySQL，首先必须以 root 身份登录并使用以下命令启动数据库服务器：

```
/etc/init.d/mysqld start
```

数据库服务器 mysqld 是一个守护进程（持续运行的后台进程），它接受来自 MySQL 监视器的数据库查询。

现在你需要设计一个数据库，在 MySQL 中创建该数据库并加载数据。为了说明如何创建和加载数据库，我设置了一个简单的图书目录数据库。

## 构建数据库的步骤回顾

按照以下基本步骤序列构建数据库：

- 1. 设计数据库。

这涉及定义用于存储信息的表和属性。

- 2. 创建一个空数据库。

在添加表之前，数据库系统要求你先构建一个空数据库。

### 3. 在数据库中创建表。

在此步骤中，你使用 SQL 的 CREATE TABLE 语句定义表。

### 4. 为表加载任何固定数据。

例如，如果你有一个制造商名称表或出版商名称表（以书籍为例），你希望用已知的[content]
MySQL（读作 My Ess Que Ell）是一种流行的关系型数据库（以互联表格集合形式工作的数据库类型）。你可以使用结构化查询语言（SQL）来操作数据库。

一家名为 MySQL AB 的瑞典公司开发了 MySQL（www.mysql.com）。MySQL AB 已将其作为开源产品发布。

检查系统是否已安装 MySQL，输入 rpm -q mysql。如果消息提示软件包未安装，可以使用以下步骤从 DVD 安装：

- 1. 以 root 身份登录并将 DVD 插入光驱。

如果使用 GNOME 或 KDE，DVD 应自动挂载。如果没有，请在终端窗口中输入以下命令挂载 DVD：

```
mount /mnt/cdrom
```

- 2. 输入以下命令安装 MySQL：

```
cd /mnt/cdrom/RedHat/RPMS
rpm -ivh mysql*
```

这将安装使用 MySQL 所需的所有软件包。

要使用 MySQL，首先必须以 root 身份登录并使用以下命令启动数据库服务器：

```
/etc/init.d/mysqld start
```

数据库服务器 mysqld 是一个守护进程（持续运行的后台进程），它接受来自 MySQL 监视器的数据库查询。

现在你需要设计一个数据库，在 MySQL 中创建该数据库并加载数据。为了说明如何创建和加载数据库，我设置了一个简单的图书目录数据库。

## 构建数据库的步骤回顾

按照以下基本步骤序列构建数据库：

- 1. 设计数据库。

这涉及定义用于存储信息的表和属性。

- 2. 创建一个空数据库。

在添加表之前，数据库系统要求你先构建一个空数据库。

### 3. 在数据库中创建表。

在此步骤中，你使用 SQL 的 CREATE TABLE 语句定义表。

### 4. 为表加载任何固定数据。

例如，如果你有一个制造商名称表或出版商名称表（以书籍为例），你希望用已知的[content]
MySQL（读作 My Ess Que Ell）是一种流行的关系型数据库（以互联表格集合形式工作的数据库类型）。你可以使用结构化查询语言（SQL）来操作数据库。

一家名为 MySQL AB 的瑞典公司开发了 MySQL（www.mysql.com）。MySQL AB 已将其作为开源产品发布。

检查系统是否已安装 MySQL，输入 rpm -q mysql。如果消息提示软件包未安装，可以使用以下步骤从 DVD 安装：

- 1. 以 root 身份登录并将 DVD 插入光驱。

如果使用 GNOME 或 KDE，DVD 应自动挂载。如果没有，请在终端窗口中输入以下命令挂载 DVD：

```
mount /mnt/cdrom
```

- 2. 输入以下命令安装 MySQL：

```
cd /mnt/cdrom/RedHat/RPMS
rpm -ivh mysql*
```

这将安装使用 MySQL 所需的所有软件包。

要使用 MySQL，首先必须以 root 身份登录并使用以下命令启动数据库服务器：

```
/etc/init.d/mysqld start
```

数据库服务器 mysqld 是一个守护进程（持续运行的后台进程），它接受来自 MySQL 监视器的数据库查询。

现在你需要设计一个数据库，在 MySQL 中创建该数据库并加载数据。为了说明如何创建和加载数据库，我设置了一个简单的图书目录数据库。

## 构建数据库的步骤回顾

按照以下基本步骤序列构建数据库：

- 1. 设计数据库。

这涉及定义用于存储信息的表和属性。

- 2. 创建一个空数据库。

在添加表之前，数据库系统要求你先构建一个空数据库。

### 3. 在数据库中创建表。

在此步骤中，你使用 SQL 的 CREATE TABLE 语句定义表。

### 4. 为表加载任何固定数据。

例如，如果你有一个制造商名称表或出版商名称表（以书籍为例），你希望用已知的[content]
MySQL（读作 My Ess Que Ell）是一种流行的关系型数据库（以互联表格集合形式工作的数据库类型）。你可以使用结构化查询语言（SQL）来操作数据库。

一家名为 MySQL AB 的瑞典公司开发了 MySQL（www.mysql.com）。MySQL AB 已将其作为开源产品发布。

检查系统是否已安装 MySQL，输入 rpm -q mysql。如果消息提示软件包未安装，可以使用以下步骤从 DVD 安装：

- 1. 以 root 身份登录并将 DVD 插入光驱。

如果使用 GNOME 或 KDE，DVD 应自动挂载。如果没有，请在终端窗口中输入以下命令挂载 DVD：

```
mount /mnt/cdrom
```

- 2. 输入以下命令安装 MySQL：

```
cd /mnt/cdrom/RedHat/RPMS
rpm -ivh mysql*
```

这将安装使用 MySQL 所需的所有软件包。

要使用 MySQL，首先必须以 root 身份登录并使用以下命令启动数据库服务器：

```
/etc/init.d/mysqld start
```

数据库服务器 mysqld 是一个守护进程（持续运行的后台进程），它接受来自 MySQL 监视器的数据库查询。

现在你需要设计一个数据库，在 MySQL 中创建该数据库并加载数据。为了说明如何创建和加载数据库，我设置了一个简单的图书目录数据库。

## 构建数据库的步骤回顾

按照以下基本步骤序列构建数据库：

- 1. 设计数据库。

这涉及定义用于存储信息的表和属性。

- 2. 创建一个空数据库。

在添加表之前，数据库系统要求你先构建一个空数据库。

### 3. 在数据库中创建表。

在此步骤中，你使用 SQL 的 CREATE TABLE 语句定义表。

### 4. 为表加载任何固定数据。

例如，如果你有一个制造商名称表或出版商名称表（以书籍为例），你希望用已知的[content]
MySQL（读作 My Ess Que Ell）是一种流行的关系型数据库（以互联表格形式工作的数据库类型）。你可以用结构化查询语言（SQL）操作数据库。

瑞典公司 MySQL AB 开发 MySQL（www.mysql.com）。MySQL AB 以开源产品形式发布它。

检查系统是否已安装 MySQL，输入 rpm -q mysql。若提示未安装，可按以下步骤从 DVD 安装：

- 1. 以 root 登录并将 DVD 插入光驱。

使用 GNOME 或 KDE 时 DVD 会自动挂载，否则在终端输入以下命令挂载 DVD：

```
mount /mnt/cdrom
```

- 2. 输入以下命令安装 MySQL：

```
cd /mnt/cdrom/RedHat/RPMS
rpm -ivh mysql*
```

这会安装使用 MySQL 所需的所有软件包。

使用 MySQL 前需以 root 登录并用以下命令启动数据库服务器：

```
/etc/init.d/mysqld start
```

数据库服务器 mysqld 是守护进程（持续运行的后台进程），接受来自 MySQL 监视器的查询。

现在需设计数据库、在 MySQL 中创建并加载数据。为说明创建和加载数据库，我建立了一个简单的图书目录数据库。

## 构建数据库的步骤回顾

构建数据库的基本步骤如下：

- 1. 设计数据库。

定义存储信息的表和属性。

- 2. 创建空数据库。

添加表前需先建空数据库。

### 3. 在数据库中创建表。

使用 SQL 的 CREATE TABLE 语句定义表。

### 4. 为表加载固定数据。

例如制造商名称表或书籍的出版商名称表，需用已知信息填充。

### 5. 备份初始数据库。

此步骤确保必要时可从头创建数据库。

### 6. 向表加载数据。

可从数据库的先前转储加载，或通过表单交互式加载。

### 7. 使用数据库。

使用 SQL 命令查询、更新记录或插入新记录。

## 设计数据库

我的简单示例未遵循数据库构建的所有可能步骤。对示例而言，数据库设计步骤很简单，因为我的图书目录数据库仅包含一个表。该表的属性如下：

- 书名，最多 50 个字符
- 第一作者姓名，最多 20 个字符
- 第二作者姓名（如果有），最多 20 个字符
- 出版社名称，最多 30 个字符
- 页数，数字
- 出版年份，数字（如 2002）
- 国际标准书号（ISBN），10 个字符的文本（如 0764542583）

我存储 ISBN 时不带典型书籍 ISBN 中嵌入的连字符。我还将 ISBN 用作表的 primary key，因为每个 ISBN 都是书籍的全球识别系统。这意味着每个图书条目必须有唯一的 ISBN，我们知道书籍确实如此。

## 创建空数据库

要在 MySQL 中创建空数据库，使用 mysqladmin 程序。例如，要创建名为 books 的空数据库，我输入以下命令：

```
mysqladmin create books
```

运行 mysqladmin 程序需以 root 登录。顾名思义，mysqladmin 是 MySQL 的数据库管理程序。

除创建数据库外，还可使用 mysqladmin 删除数据库、关闭数据库服务器并检查 MySQL 版本。例如，查看版本信息，输入以下命令：

```
mysqladmin version
```

## 使用 MySQL 监视器

创建空数据库后，与数据库的所有交互都通过 mysql 程序进行——作为数据库服务器客户端的 MySQL 监视器。需带数据库名作为参数运行 mysql。mysql 程序随后提示输入。示例如下：

```
mysql books
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 10 to server version: 3.23.49

Type 'help;' or '\h' for help. Type '\c' to clear the buffer.

mysql>
```

创建表或向表加载数据时，典型做法是将 SQL 语句（连同 \g 等 mysql 命令）放在文件中，然后用该文件作为标准输入运行 mysql。例如，假设文件 sample.sql 包含一些要在数据库 books 上尝试的 SQL 命令，则应使用以下命令运行 mysql：

```
mysql books < sample.sql
```

我以此方式使用 mysql 来创建数据库表。

## 定义表

要创建名为 books 的表，我编辑了名为 makedb.sql 的文本文件，并在其中放入以下行：

```
#
# Table structure for table 'books'
#
CREATE TABLE books (
  isbn CHAR(10) NOT NULL PRIMARY KEY,
  title CHAR(50),
  author1 CHAR(20),
  author2 CHAR(20),
  pubname CHAR(30),
  pubyear INT,
  pagecount INT
) \g
```

CREATE TABLE books 是创建名为 books 的表的 SQL 语句。语句末尾的 \g 是 mysql 命令。表属性出现在括号内的行中。

如果表包含固定数据，还可在表创建后立即包含其他 SQL 语句（如 INSERT INTO）以加载数据到表中。

要执行 makedb.sql 文件中的 SQL 语句创建 books 表，我按如下方式运行 mysql：

```
mysql books < makedb.sql
```

现在 books 数据库应有一个名为 books 的表。好吧，也许我应该命名不同，但叫同一个名字很方便。现在我可以开始向表中加载数据。

## 向表插入记录

加载数据到表的一种方法是准备另一个文件中的 SQL 语句，然后以该文件为输入运行 mysql。例如，假设我想向 books 表添加以下图书信息：

```
isbn = '156884798X'
title = 'Linux SECRETS'
author1 = 'Naba Barkakati'
author2 = NULL
pubname = 'IDG Books Worldwide'
pubyear = 1996
pagecount = 900
```

则以下 MySQL 语句将此信息加载到 books 表：

```
INSERT INTO books VALUES
('156884798X', 'Linux SECRETS', 'Naba Barkakati', NULL,
'IDG Books Worldwide', 1996, 900) \g
```

另一方面，假设你拥有的各个字段顺序与 CREATE TABLE 语句定义的表属性顺序不同。在这种情况下，可使用 INSERT INTO 命令的另一种形式添加行，如以下示例所示：

```
INSERT INTO books (pubyear, author1, author2, title,
pagecount, pubname, isbn) values
(1996, 'Naba Barkakati', NULL, 'Linux SECRETS', 900, 'IDG
Books Worldwide', '156884798X')\g
```

本质上，你必须指定属性列表以及值，并确保属性的顺序与值的顺序匹配。

如果我将所有 INSERT INTO 命令保存在名为 additems.sql 的文件中，则可通过 source 命令从 mysql 命令行加载数据库，如下所示（输入 mysql books 启动 SQL 客户端）：

```
mysql> source additems.sql
```

## 查询数据库

你可以通过 mysql 监视器交互式查询数据库。当然，你必须知道 SQL 才能执行此操作。例如，要查询 books 数据库，我使用以下命令启动 SQL 客户端：

```
mysql books
```

然后我在 mysql> 提示符下输入 SQL 命令以从数据库查找项目。完成后，我输入 quit 退出 mysql 程序。以下是一个示例（我在终端窗口中输入的所有内容）：

mysql> select title from books where pubyear < 2000 \g

| title |
|-------|
| Linux SECRETS |
| Red Hat Linux SECRETS, 2nd Edition |

2 rows in set (0.00 sec)
mysql> quit
Bye



## Multimedia Applications

Red Hat Linux 包含相当多的多媒体应用程序——主要是多媒体音频播放器和 CD 播放器，但也包括用于数码相机和刻录 CD-ROM 的应用程序。要播放其他一些多媒体文件（如 MPEG 视频），你需要在 Red Hat Linux 系统中下载并安装额外的软件。下面简要介绍一些典型的多媒体任务以及可用于执行这些任务的应用程序：

- **使用数码相机：** 在 Red Hat Linux 中使用数码相机工具从数码相机下载照片。
- **播放音频 CD：** 使用随 Red Hat Linux 提供的众多音频 CD 播放器之一。
- **播放声音文件：** 使用 XMMS，这是一款多媒体音频播放器（你需要下载一些额外的软件才能用 XMMS 播放 MP3 文件）。你也可以从互联网下载其他播放器。
- **刻录 CD：** 使用 X-CD-Roast 刻录 CD。

## Using digital cameras

Red Hat Linux 附带了 gtkam——一款可用于从数码相机下载图片的数码相机应用程序。gtkam 是 gPhoto2 命令行应用程序的 GUI 前端，可与多种不同品牌和型号的数码相机配合使用。根据型号不同，相机构可连接到串行端口或通用串行总线（USB）端口。访问 gPhoto 网站（www.gphoto.org/gphoto2）以获取最新的支持相机列表。

要使用 gtkam 与数码相机配合使用，请按照以下步骤操作：

1. **将数码相机连接到串行端口或 USB 端口（以相机支持的接口为准）并打开相机。**
2. **选择 主菜单→图形→数码相机工具 以启动 gtkam。**
3. **在 gtkam 菜单中，选择 相机→添加相机。**
4. **在出现的对话框中，单击 检测。**

如果相机受支持，相机应该会被检测到。如果没有，你可以尝试我在下面步骤中描述的替代方法。

gtkam 在左侧面板上显示相机图标和相机名称。

要了解有关 MySQL 的更多信息，请参阅 Janet Valade 所著的 *PHP 和 MySQL 傻瓜书*，Wiley Publishing, Inc. 出版。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_217_0.png)

5. 双击相机图标以在右侧面板中下载并查看缩略图。

6. 单击缩略图以选择要下载的图像；然后选择 文件→保存 或单击工具栏上的保存按钮。

然后 gtkam 下载图像并将每个图像放在主目录中的单独文件中。你现在可以在 The GIMP 或你喜欢的照片编辑器中编辑照片。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_218_0.png)

如果 gtkam 未识别你的数码相机也不必灰心。只要你的相机支持 USB 大容量存储，你仍然可以将数码相机的存储介质（例如 Compact Flash 卡）作为 USB 大容量存储设备访问。要访问数码相机上的图像，请按照以下步骤操作：

1. 阅读相机手册并使用相机的菜单选项将 USB 模式设置为大容量存储。

如果相机不支持 USB 大容量存储，则无法使用此程序访问照片。

2. 使用随相机附带的电缆将数码相机连接到 USB 端口并打开相机。

这会导致 Red Hat Linux 检测到相机，创建 /mnt/camera 目录，并在 /etc/fstab 文件中添加一行，以便你轻松地将相机的存储介质挂载到 /mnt/camera 目录。

3. 要查看相机是否被检测到，请在终端窗口中输入以下命令：

```
cat /proc/bus/usb/devices
```

输出应显示你的相机为大容量存储设备。例如，当我将 Nikon Coolpix 2500 作为 USB 大容量存储设备连接时，我得到以下输出：

```
T:  Bus=01 Lev=00 Prnt=00 Port=00 Cnt=00 Dev#= 1 Spd=12 MxCh= 2
B:  Alloc= 0/900 us ( 0%), #Int= 0, #Iso= 0
D:  Ver=1.10 Cls=09(hub)  Sub=00 Prot=00 MxPS= 8 #Cfgs= 1
P:  Vendor=0000 ProdID=0000 Rev= 0.00
S:  Product=USB UHCI Root Hub
S:  SerialNumber=fc00
C:* #Ifs= 1 Cfg#= 1 Atr=40 MxPwr= 0mA
I:  If#= 0 Alt= 0 #EPs= 1 Cls=09(hub) Sub=00 Prot=00 Driver=hub
E:  Ad=81() Atr=03(Int.) MxPS= 8 Ivl=255ms
T:  Bus=01 Lev=01 Prnt=01 Port=01 Cnt= 1 Dev#= 2 Spd=12 MxCh= 0
D:  Ver=1.10 Cls=00(isc) Sub=00 Prot=00 MxPS=64 #Cfgs= 1
P:  Vendor=04D0 ProdID=0A08 Rev= 1.00
S:  Manufacturer=NIKON
S:  Product=Nikon Digital Camera E2500
S:  SerialNumber=00000336943
C:* #Ifs= 1 Cfg#= 1 Atr=c0 MxPwr= 0mA
I:  If#= 0 Alt= 0 #EPs= 2 Cls=08(stor.) Sub=06 Prot=50 Driver=usb-storage
E:  Ad=04(0) Atr=02(Bulk) MxPS= 64 Ivl=0ms
E:  Ad=83(3) Atr=02(Bulk) MxPS= 64 Ivl=0ms
```

从第二个 T: 行开始的所有行都与 Nikon Coolpix 2500 相机有关。你可以在输出中看到一些详细信息，例如制造商名称和相机型号。

4. 通过输入以下命令挂载相机的存储介质：

```
mount /mnt/camera
```

GNOME 桌面上会出现一个相机图标。

5. 双击 GNOME 桌面上的相机图标。

相机的内容会出现在 Nautilus 文件管理器窗口中。你可以双击文件夹并找到包含照片的文件夹。通常，这些数码照片是带有 .jpg 扩展名的 JPEG 文件，文件名很隐晦。在默认视图中，Nautilus 显示照片的缩略图，因此你不必担心隐晦的文件名。图 5-3 显示了 GNOME 桌面，其中有相机图标和 Nautilus 窗口，显示了我 Nikon Coolpix 2500 的照片。

6. 单击以选择照片并将其复制到你的硬盘。

你也可以在终端窗口中输入 cp 命令，将所有或选定的图像复制到硬盘上的目录。例如，要将相机中的所有 JPEG 照片复制到当前目录，请输入：

```
cp /mnt/camera/*.jpg .
```

Figure 5-3: 你可以将数码相机中的数码照片作为 USB 大容量存储设备访问。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_219_0.png)

7. 下载完照片后，在 GNOME 桌面上右键单击相机图标并从弹出菜单中选择 卸载卷。

这会导致 Red Hat Linux 将相机从 `/mnt/camera` 目录卸载，删除 `/mnt/camera` 目录，并删除添加到 `/etc/fstab` 文件中的行。

8. 关闭相机电源并从 PC 上断开 USB 电缆。

当你可以像访问任何其他存储设备一样访问相机时，还需要 gtkam 吗！

## Playing audio CDs

GNOME 和 KDE 都附带 CD 播放器应用程序。要播放音频 CD，你需要一个声卡，并且该声卡必须配置为在 Red Hat Linux 中工作。

如果你使用的是 GNOME 桌面，你可以使用 GNOME CD Player 应用程序播放音频 CD。通过选择 主菜单→声音和视频→CD 播放器 启动 GNOME CD Player。图 5-4 显示了该 CD 播放器正在播放音频 CD 中的曲目。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_220_0.png)

GNOME CD Player 显示 CD 的标题和当前曲目的名称。GNOME CD Player 从 Compact Disc Database（CDDB）获取歌曲标题——互联网上的一个 CD 数据库（`freedb.freedb.org`）。这意味着 CD 播放器需要从 CD 数据库下载歌曲信息，因此需要一个活动的互联网连接。CD 播放器下载特定 CD 的信息后，会将其缓存在本地数据库中以供将来使用。CD 播放器的用户界面直观，易于学习。一个不错的功能是你可以按标题选择曲目，如图 5-5 所示。

如果你使用 KDE 作为桌面，你会在 KDE 中找到一个类似的音频 CD 播放器。通过选择 主菜单→声音和视频→KsCD 启动 KDE CD 播放器。

Figure 5-5:
在 GNOME CD Player 中，你可以选择特定的音频曲目进行播放。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_221_0.png)

## Playing sound files

你可以使用 X 多媒体系统（XMMS）打开和播放声音文件。XMMS 可以播放多种类型的声音文件，包括 Ogg Vorbis 和 Windows WAV。你会在 Red Hat Linux 系统的 /usr/share/sounds 目录中找到许多 WAV 声音文件——这些文件通常以 .wav 扩展名结尾。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_221_1.png)

你还可以使用 cdda2wav 命令行应用程序从音频 CD 曲目创建 WAV 声音文件。例如，要将音频 CD 中的第二首曲目转换为 WAV 文件，请输入以下命令：

```
cdda2wav -D /dev/cdrom -t2 -O wav
```

cdda2wav 将曲目保存在名为 audio.wav 的 WAV 文件中。然后你可以在 XMMS 中播放该 WAV 文件。不过要注意——音频 CD 的每首曲目在 WAV 格式下通常占用约 60MB 的磁盘空间。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_221_2.png)

Red Hat 已从 XMMS 中移除了播放 MP3 文件所需的代码，因此在播放 MP3 文件之前，你必须将其转换为 WAV 等受支持的格式。Red Hat 建议你对压缩音频文件使用 Ogg Vorbis 格式，因为 Ogg Vorbis 是一种免专利和免版税的格式。



从 GNOME 或 KDE 桌面启动 XMMS，选择 主菜单→声音和视频→音频播放器。XMMS 具有简单的用户界面。要打开声音文件，选择 窗口菜单→播放文件，或按 L 从加载文件对话框中选择 .wav 或 .ogg 文件。选择文件并单击确定。XMMS 开始播放声音文件。图 5-6 显示了 XMMS 播放声音文件时的典型窗口。

图 5-6：您可以在 XMMS 中播放许多不同类型的声音文件。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_222_0.png)

如果 XMMS 出现错误消息，选择 窗口菜单→选项→首选项，然后将 OSS 驱动程序选为输出插件。如果您想调整音量或其他声音属性，通过选择 主菜单→声音和视频→音量控制 启动音频混音器。音量控制窗口出现（图 5-7）。拖动滑块以调整音量、低音、高音和其他声音属性。

图 5-7：您可以在此窗口中调整声音的音量和其他属性。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_222_1.png)

![](img/a7eec43a54473e95dc5ea333fecf1bd7_222_2.png)

当然，许多音乐文件采用 MP3 格式，当您使用 grip 等实用程序抓取 CD 时也会得到 MP3 文件。如果能让 XMMS 播放 MP3 音乐不是很好吗？好吧，您可以轻松做到。您所需要做的就是下载并安装 XMMS 的 MPEG 音频输入插件。该插件以 RPM 文件的形式提供 — `xmms-mpg123-1.2.7-21.i386.rpm` — 可在 `havardk.xmms.org/dist/xmms-1.2.7-rh8-rh9-rpm/xmms-mpg123-1.2.7-21.i386.rpm` 获取（对于 Red Hat Linux 的其他版本，请在 `havardk.xmms.org/dist/` 中的适当目录中查找）。下载 RPM 文件后，以 `root` 身份登录并输入 `rpm -ivh xmms-mpg123*` 安装插件。下次运行 XMMS 时，您就可以在 XMMS 中播放 MP3 文件了。简单吧？

## 烧录 CD

Red Hat Linux 包含 GnomeToaster，这是一款功能丰富的图形化 CD 烧录应用程序。它可以创建数据 CD 和音频 CD。您还可以 *抓取*（复制）音频 CD 上的音乐到硬盘上的文件，然后将其烧录到新的音频 CD 上。如果您碰巧下载了 Red Hat Linux ISO 映像（包含 CD-ROM 精确副本的大型数据文件），您可以使用 GnomeToaster 从该 ISO 映像创建 CD。在接下来的几节中，我将简要介绍如何使用 GnomeToaster。如果您想了解更多信息，请访问 `gnometoaster.rulez.org`。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_223_0.png)

GnomeToaster 依赖许多外部程序来完成其工作。如果这些外部程序不存在，则某些 GnomeToaster 功能将无法工作。虽然 GnomeToaster 使用的大多数程序都随 Red Hat Linux 提供，但其中一些不属于 Red Hat Linux 发行版。例如，GnomeToaster 需要 `mpg123` 程序将 MP3 音频文件转换为适合 CD 录制的格式。Red Hat Linux 不带 `mpg123` 程序，因此您无法创建包含 MP3 歌曲的音频 CD。

在您能够烧录 CD 之前，需要将 CD-R 或 CD-RW 驱动器（CD 烧录机）连接到您的 PC。它可以是内部或外部 CD 烧录机。内部 CD 烧录机通常是 IDE（也称为 ATAPI）设备，连接到支持 PC 硬盘和任何其他 CD-ROM 驱动器的同一卡上。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_223_1.png)

如果您有外部 CD 烧录机，它很可能连接到 PC 的 USB 端口。当您将此类烧录机连接到 USB 端口并为其供电时，Red Hat Linux 应自动识别该设备并加载适当的 USB 驱动程序。当您使用 GnomeToaster 在 USB CD-R/RW 驱动器上烧录 CD 时，无需做任何特殊操作 — GnomeToaster 会自动检测系统上的大多数 CD-ROM 和 CD-R/RW 驱动器。然而，您必须手动识别 ATAPI CD 驱动器。

要启动 GnomeToaster，从 GNOME 或 KDE 桌面选择 主菜单→系统工具→更多系统工具→CD 写入器。如果您未以 `root` 身份登录，将提示输入 `root` 密码。GnomeToaster 主窗口出现，如图 5-8 所示。您可以从主窗口完成所有操作 — 配置 GnomeToaster 并烧录音频和数据 CD。

## 识别 CD 驱动器

启动时，GnomeToaster 会尝试自动检测 CD 烧录机和 CD-ROM 驱动器，但您需要帮助它识别 ATAPI CD 驱动器（大多数内部 CD-ROM 和 CD-R/RW 驱动器属于此类）。我将向您展示如何操作。

要查看 GnomeToaster 是否检测到所有 CD 驱动器，请单击主窗口顶部工具栏上的首选项。GnomeToaster 显示首选项对话框（如图 5-9 所示），其中包含七个选项卡。单击 CDROM and Recorder Setup 选项卡以查看其检测到的 CD 驱动器列表。

图 5-8:
您可以在 GnomeToaster 的主窗口中烧录 CD。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_224_0.png)

图 5-9:
您可从此对话框配置 GnomeToaster 首选项。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_224_1.png)

图 5-9 显示了 GnomeToaster 在具有外部 CD 烧录机和内部 ATAPI CD-ROM 驱动器的系统上检测到的结果。在这种情况下，GnomeToaster 检测到一个 CD 烧录机（驱动器类型列左侧的点告诉我这是 CD 烧录机）。然而，列表中未显示 ATAPI CD-ROM 驱动器。

除非 ATAPI CD-ROM 驱动器配置为通过 ide-scsi 驱动程序访问，否则 GnomeToaster 无法检测到它们。由于这不是 Red Hat Linux 的默认设置，您必须手动将 ATAPI CD 驱动器识别给 GnomeToaster。为此，请按照以下步骤操作：

![](img/a7eec43a54473e95dc5ea333fecf1bd7_225_0.png)

- 1. 在 GnomeToaster 首选项对话框中，单击 CDROM and Recorder Setup 选项卡（图 5-9），然后单击对话框左下角附近的添加按钮。

一个对话框（见图 5-10）会提示您输入有关 CD-ROM 驱动器的信息。

图 5-10：告诉 GnomeToaster 您系统上任何 IDE/ATAPI CD 驱动器的信息。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_225_1.png)

- 2. 填写设备文件和挂载点字段，然后单击确定。

通常，您可以在设备文件名中输入 /dev/cdrom（或 /dev/hdc），在挂载点字段中输入 /mnt/cdrom。

您可以填写 CD 驱动器的型号和制造商，但这些字段并不重要。

## 探索首选项对话框

在 GnomeToaster 首选项对话框（图 5-9 所示）中，您可以检查其他选项卡并配置更多选项。通常，您会将其他所有内容保留为默认设置，但以下是 GnomeToaster 首选项对话框中选项卡可执行操作的概述：

- **Common:** 此选项卡可让您指定临时文件的位置、是否在写入 CD 之前将数据存储在硬盘上，以及 GnomeToaster 可在其中查找 CD 信息的 CD 数据库服务器。默认 CD 数据库服务器为 `freedb.freedb.org.`（端口 888）。您可以将这些选项保留为默认设置。
- **ISO9660:** 此选项卡用于设置在烧录使用 ISO 9660 文件系统的数据 CD 时使用的选项（这是一种国际公认的标准方法，用于在 CD-ROM 上存储文件和目录，以便您可以在任何计算机系统上读取同一 CD-ROM，无论其运行的是 Microsoft Windows、Macintosh 还是 Linux）。
- **CD Digital Audio:** 此选项卡指定使 GnomeToaster 能够与音频 CD 配合工作的设置。例如，默认设置会导致 GnomeToaster 在需要从音频 CD 提取音轨时运行 `cdda2wav` 程序。还有设置指定如何提取有关音频 CD 的信息，包括光盘标题、光盘艺术家以及每个音轨的信息。
- **Filetypes:** 此选项卡包含有关文件类型的信息以及如何将每种类型的文件转换为可记录到 CD 的数据流。每种文件类型由扩展名表示，例如 MP3 文件的 `.mp3`、WAV 文件的 `.wav` 和 Ogg Vorbis 音频文件的 `.ogg`。对于每种文件类型，都有 GnomeToaster 运行的命令行以将该文件转换为适合 CD 录制的数据。
- **CDROM and Recorder Setup:** 此选项卡显示 GnomeToaster 已检测到的 CD-ROM 和 CD-R/RW 驱动器的信息。您也可以在此选项卡中手动添加 ATAPI CD 驱动器到列表中。
- **Audio System:** 此选项卡显示用于播放声音的音频驱动程序。
- **Recorder:** 此选项卡用于指定 GnomeToaster 如何录制 CD。最重要的选项是录制客户端的名称 — 这些是 GnomeToaster 运行以录制 CD 的程序。默认情况下，GnomeToaster 使用 `cdrecord` 或 `cdrdao` 来录制 CD。`cdrecord` 和 `cdrdao` 都随 Red Hat Linux 提供。

## 录制音频 CD

使用 GnomeToaster，您可以复制音频 CD 或通过混合和匹配您想要的音轨来创建新的音频 CD。要使用现有音频 CD 的全部或部分选定音轨制作新的音频 CD，请按照以下步骤操作：

- 1. 将原始 CD 放入 CD 读取设备中（例如，您在 GnomeToaster 首选项的 CDROM and Recorder Setup 选项卡中识别的 ATAPI CD-ROM 驱动器）。



2. **点击 GnomeToaster 窗口左上角窗格中 CD-ROM 驱动器旁边的加号；然后点击 CD 读卡器设备名称。**

GnomeToaster 在右上角窗格中显示音轨（见图 5-11），以便您可以选择要读取的音轨。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_227_0.png)

Figure 5-11:
从 CD 拖放音频音轨以创建您自己的音频合集。

3. **点击 GnomeToaster 窗口下部沿线的标签页窗格中的“轨道编辑器”标签（从上数第二个标签）。**

GnomeToaster 显示轨道编辑器视图，您可以在此准备要刻录到新音频 CD 上的音轨。

4. **从音轨列表中将音轨拖到轨道编辑器窗格上。**

GnomeToaster 运行 `cdda2wav` 将音轨转换为适合 CD 录制的格式并将音轨保存到硬盘。读取并保存一首典型音轨可能需要一两分钟（当然，较长的音轨从 CD 中提取所需时间更长）。GnomeToaster 在信息窗口中显示进度。复制音轨到编辑器后，GnomeToaster 会在 GnomeToaster 窗口底部的状态栏上显示当前音轨所需的兆字节数（参见图 5-11）。这样您就可以跟踪 CD 上剩余的空间，CD 可处理超过 700MB 的数据。

5. **重复步骤 4 以向您的新音频 CD 添加其他音频音轨。**

6. 要从轨道编辑器窗格中删除音轨，请选择该音轨，然后右键单击该音轨并从弹出菜单中选择“删除音轨”。

7. 列表完成后，将一张空白 CD-R 插入 CD 烧录机，然后点击 GnomeToaster 工具栏上的“录制”按钮开始刻录 CD。

然后 GnomeToaster 开始刻录 CD 并在一个窗口中显示进度（见图 5-12）。刻录过程完成后，GnomeToaster 会弹出 CD。

Figure 5-12:
Gnome-Toaster 显示刻录新音频 CD 的进度。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_228_0.png)

8. 在您的 Linux 系统中播放 CD — 只需退出 GnomeToaster 并将 CD 放入 CD-ROM 驱动器即可播放，前提是您的声卡设置正确。

您也可以在 CD 播放器上播放该 CD。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_228_1.png)

默认情况下，GnomeToaster 使用 Track-At-Once（TAO）模式刻录音频 CD，该模式会在每个音轨后放置两秒的暂停。如果您想一次性写入整个音频 CD，可以通过选择 Disk-At-Once（DAO）模式来实现。要选择此模式，请点击下部标签页窗格中从上数最后一个标签的“录音机设置”标签，然后标记“Disc at Once”复选框 — 您可以在图 5-13 的左下区域看到此复选框。您也可以从此窗格修改其他录音机设置。

顺便说一下，图 5-13 中下部窗格右侧的客户端输出区域显示了 GnomeToaster 用于刻录 CD 的外部命令的输出。例如，当它使用 cdrecord 程序刻录 CD 时，cdrecord 的输出会显示在此区域。当前图显示了 cdrecord 命令在刻录包含五首音轨的音频 CD 后的输出。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_229_0.png)

Figure 5-13: 从下部窗格设置各种录音机设置，包括录音机速度。

## 创建数据 CD

将文件从硬盘保存到 CD 上很简单。要创建数据 CD，请按照以下步骤操作：

- 1. **点击 GnomeToaster 窗口左上角窗格中“Unix Tree”标签旁边的加号。**
  GnomeToaster 显示您系统中的目录层次结构。
- 2. **点击一个目录名称。**
  GnomeToaster 在右上角窗格中显示目录的内容。
- 3. **点击 GnomeToaster 窗口下部沿线的标签页窗格中的“文件夹”标签（最上面的标签）。**
  GnomeToaster 显示一个虚拟文件系统，表示您准备刻录的数据 CD 的组织结构。
- 4. **将文件和目录从右上角窗格拖到下右窗格中的虚拟文件系统视图上。**
- 5. **根据需要切换到其他目录并继续操作，直到您选择了要在数据 CD 上使用的所有文件和目录。**
  GnomeToaster 显示当前文件集，包括目录层次结构，如图 5-14 所示。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_230_0.png)

Figure 5-14: 使用 Gnome-Toaster 刻录数据 CD 之前准备文件和目录。

6. 将一张空白 CD 插入 CD 烧录机，然后点击工具栏上的“录制”按钮。

GnomeToaster 开始刻录数据 CD，并在完成后弹出光盘。

## 刻录 ISO 映像

Linux 发行版，包括 Red Hat Linux，可以从各种互联网站点下载为 ISO 映像 — ISO 映像是整个 CD-ROM 在单个巨大文件中的精确副本。这些文件通常具有 .iso 扩展名。名称中的 ISO 部分来自 CD-ROM 使用 ISO 9660 文件系统的事实，而映像意味着该文件是 CD-ROM 上每位数据的精确复制。

您可以使用 GnomeToaster 从 ISO 映像制作 CD。只需按照以下步骤操作：

- 1. **点击 GnomeToaster 窗口左上角窗格中“Unix Tree”标签旁边的加号。**
  GnomeToaster 显示您系统中的目录层次结构。
- 2. **转到包含 ISO 映像文件的目录并点击该目录的名称。**

GnomeToaster 在右上角窗格中显示目录的内容。您应该会看到 ISO 映像文件列出。

3. **点击 GnomeToaster 窗口下部沿线的标签页窗格中的“轨道编辑器”标签（从上数第二个标签）。**

GnomeToaster 显示轨道编辑器视图。

4. **将 ISO 文件从右上角窗格拖到下右窗格中的轨道编辑器视图上。**

GnomeToaster 在轨道编辑器视图中显示 ISO 文件的名称以及它需要的空间，如图 5-15 所示。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_231_0.png)

Figure 5-15:
您可以使用 GnomeToaster 从 ISO 映像创建 CD。

5. **将一张空白 CD 插入 CD 烧录机并点击工具栏上的“录制”按钮。**

GnomeToaster 开始将 ISO 映像刻录到 CD 上，并在完成后弹出光盘。

## 图形和图像处理

您可以使用图形和图像处理应用程序来处理图像和图形（线条图和形状）。我讨论了两个应用程序：

- The GIMP（GNU 图像处理程序）是一个用于查看和执行图像处理任务的程序，例如照片修复、图像合成和图像创建。
- KGhostview 是 KDE 应用程序，能够显示 PostScript 和 PDF 文件。

### The GIMP

The GIMP（GNU 图像处理程序）是由 Peter Mattis 和 Spencer Kimball 编写并在 GNU 通用公共许可证（GPL）下发布的图像处理程序。如果您在从本书附带 DVD 安装 Red Hat Linux 时选择“图形操作”软件包，则会安装它。The GIMP 与其他图像处理程序相当，例如 Adobe Photoshop 和 Corel Photopaint。

要试用 The GIMP，请从 GNOME 或 KDE 桌面选择“主菜单→图形→The GIMP”。The GIMP 启动并显示一个包含版权和许可信息的窗口。点击“继续”按钮继续安装。下一屏幕显示在继续个人安装 The GIMP 时要创建的目录。

GIMP 安装涉及在您的主目录中创建一个名为 .gimp-1.2 的目录并在该目录中放置一些文件。该目录基本上保存了您可能对 The GIMP 所做的任何用户偏好更改的信息。请继续点击窗口底部的“继续”按钮。GIMP 创建必要的目录，将必要的文件复制到这些目录，并引导您完成一系列对话框以完成安装。

安装完成后，点击“继续”按钮。从现在开始，您将不再看到安装窗口；只有在首次运行 The GIMP 时才需要处理安装。

然后 The GIMP 加载任何插件 — 增强其功能的外部模块。它显示一个启动窗口，在每个插件加载时显示一条消息。启动完成后，The GIMP 在一个窗口中显示每日提示。您可以浏览提示并点击“关闭”按钮关闭提示窗口。与此同时，The GIMP 显示多个窗口（图 5-16）。

这些窗口包括标题为 The GIMP 的主工具箱窗口；一个“工具选项”窗口；一个“画笔选择”窗口；以及一个“图层、通道和路径”窗口。其中，主工具箱窗口是最重要的 — 事实上，您可以关闭其他窗口并使用工具箱中的菜单和按钮工作。




![](img/a7eec43a54473e95dc5ea333fecf1bd7_233_0.png)

图 5-16:
修整
你的照片
使用
GIMP。

工具箱在菜单栏上有三个菜单：

-   **文件菜单** 有创建新图像、打开现有图像、保存和打印图像、通过邮件发送图像以及退出 GIMP 的选项。
-   **Xtns 菜单** 让你访问 GIMP 的众多扩展。Xtns 菜单的确切内容取决于系统上安装了哪些扩展。
-   **帮助菜单** 是获取帮助和查看提示的地方。例如，选择 帮助→帮助 以打开 GIMP 帮助浏览器，其中包含有关 GIMP 的在线信息。

要在 GIMP 中打开图像文件，请选择 文件→打开。这会弹出“载入图像”对话框，您可以在其中选择图像文件。您可以更改目录并选择要打开的图像文件。GIMP 可以读取所有常见的图像文件格式，例如 GIF、JPEG、TIFF、PCX、BMP、PNG 和 PostScript。选择文件并单击“确定”按钮后，GIMP 会将图像载入到新窗口中。图 5-16 显示了 GIMP 已打开的图像以及所有其他 GIMP 窗口。

工具箱还包含许多按钮，表示用于编辑图像和应用特殊效果的工具。您可以通过将鼠标指针放在工具按钮上获得每个工具按钮的弹出帮助。您可以通过单击工具按钮来选择工具，并将该工具的效果应用于图像。

为了方便您，GIMP 在您在图像窗口上右键单击鼠标时显示弹出菜单。弹出菜单包含工具箱中“文件”和“Xtns”菜单的大多数选项。然后您可以从这些菜单中选择特定操作。

您可以用 GIMP 做的事情远不止加载和查看图像，但对其所有功能的完整讨论超出了本书的范围。如果您想尝试 GIMP 的其他功能，请参阅 GIMP 用户手册（GUM），可在 manual.gimp.org 在线获取。您也可以选择 Xtns→Web Browser→GIMP.ORG→Documentation 来访问 GIMP 的在线文档（当然，为此需要互联网连接）。

一些关于 GIMP 的文档安装在 `/usr/share/doc` 目录中。要进入该目录，请输入 `cd /usr/share/doc/gimp*`（实际目录名称取决于 GIMP 的当前版本）。该目录中的 README 文件会将您指向 Web 上的其他资源，在那里您可以了解有关 GIMP 的更多信息。特别是，访问 GIMP 主页 www.gimp.org 以了解 GIMP 的最新新闻并找到指向其他资源的链接。

## KGhostview

KGhostview 是 KDE 应用程序，非常适合查看和打印 PostScript 和 PDF 文档。对于长文档，您可以查看和打印选定页面。您还可以通过放大或缩小以各种放大级别查看文档。

要运行 KGhostview，请从 GNOME 或 KDE 桌面选择 主菜单→图形→更多图形应用程序→PS/PDF 查看器。这会导致 KGhostview 应用程序窗口出现。除了顶部边缘的菜单栏和工具栏外，一个垂直分隔线将窗口的主显示区域分成两部分。

要在 KGhostview 中加载和查看 PostScript 文档，请选择 文件→打开，或单击工具栏上的打开文件夹图标。此操作会导致 KGhostview 显示文件选择对话框。使用此对话框导航文件系统并选择 PostScript 文件。您可以选择随 Ghostscript 提供的 PostScript 文件之一。例如，在 `/usr/share/ghostscript/7.07/examples` 目录中打开文件 tiger.ps。（如果您的系统具有 Ghostscript 7.07 之后的版本，则必须使用新版本号代替 7.07。）

要打开所选文件，请在文件选择对话框中单击“打开文件”按钮。KGhostview 打开所选文件，处理其内容，并在其窗口中显示输出，如图 5-17 所示。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_235_0.png)

图 5-17:
KGhostview 可以显示 PostScript 和 PDF 文件。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_235_1.png)

KGhostview 可用于查看各种以 PostScript 和 PDF 格式提供的文档（这些文件通常在其名称中带有 `.ps` 或 `.pdf` 扩展名）。

### 第 6 章：使用文本编辑器

### 本章内容

-   ✓ 使用 GUI 文本编辑器
-   ✓ 学习 ed 文本编辑器
-   ✓ 学习 vi 文本编辑器

在 Red Hat Linux 中，大多数系统配置文件都是文本文件。如果您编写任何 shell 脚本或其他计算机程序，它们也是文本文件。有时您必须使用为此目的设计的程序来编辑这些文件：文本编辑器。例如，您可能需要编辑诸如 `/etc/hosts`、`/etc/modules.conf`、`/etc/X11/XF86Config`、`/etc/xinetd.d/telnet` 等文件。

在本章中，我向您介绍一些文本编辑器——GUI 编辑器和文本模式编辑器。

### 使用 GUI 文本编辑器

每个 GUI 桌面——GNOME 和 KDE——都附带 GUI 文本编辑器（这些是具有图形用户界面的文本编辑器）。

要使用 GNOME 文本编辑器，请从 GNOME 桌面选择 主菜单→附件→文本编辑器。您可以通过单击工具栏上的“打开”按钮来打开文件。这会弹出“打开文件”对话框。然后您可以更改目录并通过单击“确定”按钮选择要编辑的文件。

然后 GNOME 文本编辑器在窗口中加载文件。您可以打开多个文件并在编辑文件时在它们之间切换。图 6-1 显示了使用编辑器的典型编辑会话。

在这种情况下，编辑器有三个文件——`fstab`、`hosts` 和 `inittab`（均来自 `/etc` 目录）——打开以供编辑。文件名显示为编辑器窗口工具栏下方的选项卡。您可以通过单击选项卡在文件之间切换。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_237_0.png)

图 6-1:
您可以使用 GNOME 文本编辑器编辑文本文件。

如果您打开的文件只有读权限，则文件名前面会加上文本 RO - 以表示该文件为“只读”。在图 6-1 中，所有文件都以只读方式打开，因为这里我以普通用户身份登录，而我打开的系统文件只有 root 才能修改。

其余的文本编辑步骤很直观。要输入新文本，请单击以定位光标然后开始输入。您可以使用文本编辑区域上方工具栏上的按钮来选择文本、复制、剪切和粘贴。

从 KDE 桌面，您可以通过选择 主菜单→附件→Kate 来启动 KDE 文本编辑器。要打开文本文件，请从菜单中选择 文件→打开。会出现一个对话框。从此对话框中，您可以进入正确的目录，选择要打开的文件，然后单击“确定”按钮。然后 KDE 文本编辑器打开文件并在窗口中显示其内容。然后您可以编辑文件。

### 使用 ed 和 vi 进行文本编辑

Red Hat Linux 附带两个文本模式文本编辑器：

-   ed, a line-oriented text editor
-   vi, a full-screen text editor that supports the command set of an earlier editor named ex

与图形文本编辑器相比，ed 和 vi 编辑器比较晦涩。然而，您仍应学习 ed 和 vi 的基本编辑命令，因为有时这两个可能是唯一可用的编辑器。

例如，如果 Red Hat Linux 拒绝从硬盘启动，您可能必须从软盘启动。在这种情况下，您必须使用 ed 编辑器编辑系统文件，因为该编辑器足够小，可以放入软盘中。我将引导您了解 ed 和 vi 的基本文本编辑命令。您会看到——它们并不难。

### 使用 ed

通常，您只有在从最小版本的 Linux（例如，您设置为启动磁盘的软盘）启动并且系统不支持全屏模式时才需要使用 ed。在所有其他情况下，您可以使用在全屏文本模式下工作的 vi 编辑器。

使用 ed 时，您在命令模式或文本输入模式下工作：

-   命令模式是默认模式。在此模式下，您输入的任何内容都被解释为命令。ed 文本编辑器具有简单的命令集，其中每个命令由一个或多个字符组成。
-   文本输入模式用于输入文本。您可以使用命令 a（追加）、c（更改）或 i（插入）进入输入模式。输入多行文本后，您可以通过单独一行输入句点（.）来退出输入模式。

要练习编辑文件，请通过发出以下命令将 /etc/fstab 文件复制到您的主目录：

```
cd
cp /etc/fstab .
```

现在您应该在主目录中有一个名为 fstab 的文件。键入以下命令开始在 ed 中编辑文件：

```
ed -p: fstab
621
:
```

此示例使用 -p 选项将提示符设置为冒号字符（:）并打开 fstab 文件（在当前目录中，应为您的主目录）以进行编辑。ed 编辑器打开文件，报告文件中的字符数（621），显示提示符（:），并等待命令。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_238_0.png)

当您使用 ed 编辑时，确保始终打开提示字符（使用 -p 选项）很有帮助。如果没有提示，很难判断 ed 是否处于输入模式或命令模式。



打开文件进行编辑后，ed 的当前行是文件的最后一行。要查看当前行号（当前行是 ed 对其应用命令的行），请使用 .- 命令，如下所示：

```
:.=
9
```

此输出告诉你 fstab 文件有九行。（你的系统中的 /etc/fstab 文件可能有不同行数，在这种情况下 ed 会显示不同的数字。）

可使用 1,$p 命令查看文件中的所有行，如以下示例所示：

```
:1,$p
LABEL=/                /               ext3    defaults        1 1
LABEL=/boot            /boot           ext3    defaults        1 2
none                   /dev/pts        devpts  gid=5,mode=620  0 0
none                   /proc           proc    defaults        0 0
none                   /dev/shm        tmpfs   defaults        0 0
/dev/hda6              swap            swap    defaults        0 0
/dev/cdrom             /mnt/cdrom      udf,iso9660
/dev/fd0               /mnt/floppy     auto    noauto,owner,kudzu 0 0
:
```

要转到特定行，输入行号：

```
:6
/dev/hda6              swap            swap    defaults        0 0
:
```

编辑器会通过显示该行作出响应。

假设你想删除包含 cdrom 的行。要搜索字符串，输入斜杠（/）后跟要定位的字符串：

```
:/cdrom
/dev/cdrom             /mnt/cdrom      udf,iso9660
noauto,owner,kudzu,ro 0 0
:
```

编辑器会定位包含该字符串的行然后显示它。该行成为当前行。

要删除当前行，请按如下方式使用 d 命令：

```
:d
:
```

要将一个字符串替换为另一个字符串，请使用 s 命令。例如，要将 cdrom 替换为字符串 cd，请使用以下命令：

```
:s/cdrom/cd/
:
```

要在当前行前面插入一行，请使用 i 命令：

```
:i
(type the line you want to insert)
.(type a single period to indicate you're done)
:
```

你可以输入任意多行。在最后一行之后，单独一行输入一个句点（.）。该句点标记文本输入模式的结束，编辑器切换到命令模式。在这种情况下，你可以通过看到提示符（:）来判断 ed 已切换到命令模式。

当你对更改满意时，可以使用 w 命令将它们写入文件。如果你想保存更改并退出，输入 wq 以同时执行这两个步骤：

```
:wq
693
```

ed 编辑器会保存文件中的更改，显示已保存字符数，然后退出。如果你想在不保存任何更改的情况下退出编辑器，请使用 q 命令。

这些示例应能让你了解如何使用 ed 命令执行编辑文本文件的基本任务。表 6-1 列出了一些常用的 ed 命令。

表 6-1 常用 ed 命令

| 命令 | 执行以下操作 |
|---|---|
| ! command | 执行 shell 命令（例如，!pwd 显示当前目录）。 |
| $ | 转到缓冲区中的最后一行。 |
| % | 将其后的命令应用于缓冲区中的所有行（例如，%p 打印所有行）。 |
| + | 转到下一行。 |
| +n | 转到第 n 行之后的下一行（其中 n 是你指定的数字）。 |

（续）

表 6-1（续）

| 命令 | 执行以下操作 |
|---|---|
| . | 将其后的命令应用于缓冲区中的所有行（例如，.p 打印所有行）；与 % 类似。 |
| - | 转到前一行。 |
| - n | 转到第 n 行之前的前一行（其中 n 是你指定的数字）。 |
| . | 指缓冲区中的当前行。 |
| /text/ | 向前搜索指定文本。 |
| : | 指一行范围；从当前行到缓冲区中的最后一行。 |
| = | 打印行号。 |
| ?text? | 向后搜索指定文本。 |
| ^ | 转到前一行；另请参阅 - 命令。 |
| ^n | 转到第 n 行之前的前一行（其中 n 是你指定的数字）；另请参阅 -n 命令。 |
| a | 在当前行之后追加。 |
| c | 更改指定行。 |
| d | 删除指定行。 |
| i | 在当前行之前插入文本。 |
| n | 转到行号为 n 的行。 |
| Press Enter | 显示下一行并使该行成为当前行。 |
| q | 退出编辑器。 |
| Q | 不保存更改退出编辑器。 |
| r file | 读取文件内容并在当前行之后插入。 |
| s/old/new/ | 将旧字符串替换为新字符串。 |
| u | 撤销上一个命令。 |
| W file | 将缓冲区内容追加到指定文件的末尾。 |
| w file | 将缓冲区保存到指定文件中（如果未命名文件，则保存到默认文件——ed 当前正在编辑的文件内容）。 |

## 使用 vi

vi 编辑器是一个全屏文本编辑器，因此你可以同时查看多行。大多数 UNIX 系统，包括 Red Hat Linux，都自带 vi。因此，如果你学习 vi 的基本功能，你将能够在几乎任何 UNIX 系统上编辑文本文件。

## 技术说明

当 vi 编辑文件时，它会将文件读入缓冲区——一块内存——以便你可以更改缓冲区中的文本。vi 编辑器在编辑过程中也会使用临时文件，但原始文件在保存更改之前不会被更改。

要启动编辑器，输入 vi 并在其后加上要编辑的文件名，如下所示：

```
vi /etc/fstab
```

vi 编辑器随后将文件加载到内存中，并在文本屏幕上显示前几行，并将光标定位在第一行（图 6-2）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_242_0.png)

图 6-2：
你可以使用 vi 全屏文本编辑器编辑文本文件。

最后一行显示文件的路径名以及文件中的行数（8）和字符数（621）。在这种情况下，文本 [read only] 出现在文件名之后，因为我以普通用户身份登录时打开 /etc/fstab 文件（这意味着我没有权限修改文件）。稍后，vi 显示中的最后一行用作命令输入区。其余行显示文件。如果文件包含的行数少于屏幕，vi 会在第一列用波浪号（~）显示空行。

当前行由光标标记，光标显示为一个小黑矩形。光标出现在字符上方。

使用 vi 时，你工作于以下三种模式之一：

- **视觉命令模式** 是默认模式。在此模式下，你输入的任何内容都被解释为适用于包含光标的行命令。vi 命令与 ed 命令类似。
- **冒号命令模式** 用于读取或写入文件、设置 vi 选项以及退出 vi。所有冒号命令都以冒号（:）开头。当你输入冒号时，vi 将光标定位在最后一行并等待你输入命令。按下 Enter 时命令生效。
- **文本输入模式** 用于输入文本。你可以使用命令 a（在光标后插入）、A（在行尾追加）或 i（在光标后插入）进入输入模式。输入多行文本后，你必须按 Esc 退出输入模式并重新进入视觉命令模式。

所有这些模式的一个问题是，你无法轻松判断 vi 当前处于哪种模式。开始输入后才意识到 vi 不在输入模式中可能会令人沮丧。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_243_0.png)

如果你想确保 vi 处于命令模式，只需按几次 Esc 即可。（多次按 Esc 也不会有问题。）

要在 vi 中查看在线帮助，请在命令模式下输入 :help。完成帮助后，输入 :q 退出帮助屏幕并返回正在编辑的文件。

vi 编辑器最初将光标定位在第一行的第一个字符上——而其中最方便的事情之一就是知道如何移动光标。为了练习一下，请尝试表 6-2 中显示的命令。

**表 6-2 vi 中的光标移动命令**

| 按键 | 执行以下操作 |
|---|---|
| Down arrow | 将光标向下移动一行。 |
| Up arrow | 将光标向上移动一行。 |
| Left arrow | 将光标向左移动一个字符。 |
| Right arrow | 将光标向右移动一个字符。 |
| W | 将光标向前移动一个词。 |
| B | 将光标向后移动一个词。 |
| Ctrl+D | 向下滚动半屏。 |
| Ctrl+U | 向上滚动半屏。 |




你可以在任何时候转到特定的行号。这时冒号命令就派上用场了。例如，要转到第 6 行，请输入以下内容然后按 Enter：

```
:6
```

当你输入冒号时，vi 会在屏幕最后一行显示冒号。从那时起，vi 会将你输入的任何文本作为命令使用。你必须按 Enter 将命令提交给 vi。在冒号命令模式下，vi 接受 ed 编辑器接受的所有命令——还有更多。

要搜索字符串，首先输入斜杠（/）。vi 编辑器会在屏幕最后一行显示斜杠。输入搜索字符串然后按 Enter。vi 编辑器会定位该字符串并将光标置于该字符串的开头。因此，要在文件 /etc/fstab 中定位字符串 cdrom，请输入

```
/cdrom
```

要删除包含光标的行，请输入 dd（两个小写 d）。vi 编辑器会删除该行文本并使下一行成为当前行。

要在光标前开始输入文本，请输入 i（单独一个小写 i）。vi 编辑器切换到文本输入模式。现在你可以输入文本。输入完毕后，按 Esc 返回到可视命令模式。

编辑文件完成后，你可以使用 :w 命令保存文件中的更改。要在不保存任何更改的情况下退出编辑器，请使用 :q! 命令。如果想保存更改并退出，可以输入 :wq 同时执行这两个步骤。vi 编辑器会保存文件中的更改并退出。你也可以通过按 Shift+zz（按住 Shift 键并连续按两次 Z 键）来保存更改并退出编辑器。

除了这些命令之外，vi 还接受大量命令。表 6-3 按任务列出了一些常用的 vi 命令。

表 6-3 常用 vi 命令

| 命令 | 执行以下操作 |
|---|---|
| 插入文本 | |
| a | 在光标后插入文本。 |
| A | 在当前行末尾插入文本。 |
| I | 在当前行开头插入文本。 |
| i | 在光标前插入文本。 |

(续)

**表 6-3（续）**

| 命令 | 执行以下操作 |
|---|---|
| *删除文本* | |
| D | 删除到当前行末尾。 |
| dd | 删除当前行。 |
| dw | 从光标删除到下一个单词末尾。 |
| x | 删除光标所在字符。 |
| *更改文本* | |
| C | 更改到当前行末尾。 |
| cc | 更改当前行。 |
| J | 将当前行与下一行合并。 |
| r x | 用 x（x 为任意字符）替换光标下的字符。 |
| *移动光标* | |
| h or Left arrow | 向左移动一个字符。 |
| j or Down arrow | 向下移动一行。 |
| k or Up arrow | 向上移动一行。 |
| L | 将光标移动到屏幕末尾。 |
| l or Right arrow | 向右移动一个字符。 |
| w | 移动到下一个单词的开头。 |
| *滚动文本* | |
| Ctrl+D | 向前滚动半屏。 |
| Ctrl+U | 向后滚动半屏。 |
| *刷新屏幕* | |
| Ctrl+L | 重绘屏幕。 |
| *剪切和粘贴文本* | |
| P | 将提取的行放在当前行上方。 |
| p | 将提取的行放在当前行下方。 |
| yy | 将当前行提取（复制）到未命名缓冲区。 |
| *冒号命令* | |
| :!command | 执行 shell 命令。 |
| :q | 退出编辑器。 |
| :q! | 不保存更改退出。 |
| :r filename | 读取文件并在当前行后插入。 |
| :w filename | 将缓冲区写入文件。 |
| :wq | 保存更改并退出。 |

| 命令 | 执行以下操作 |
|---|---|
| *搜索文本* | |
| `/string` | 向前搜索字符串。 |
| `?string` | 向后搜索字符串。 |
| *杂项* | |
| `u` | 撤销上一个命令。 |
| `Esc` | 结束输入模式并进入可视命令模式。 |
| `U` | 撤销对当前行的最近更改。 |

## 第三册
## OpenOffice.org
## 第五波
## Rich Tennant 著
## Pauline 的珍珠

![](img/a7eec43a54473e95dc5ea333fecf1bd7_248_0.png)

救命！我失去深度递归了！我的子程序令人困惑！！我的哈希表正在退化- 救命啊！！

## 目录一览

- 第 1 章：使用 OpenOffice.org Writer 编写文档 ........................................ 223
- 第 2 章：使用 OpenOffice.org Calc 准备电子表格 ........................................ 249
- 第 3 章：使用 OpenOffice.org Impress 制作演示文稿 ........................................ 261
- 第 4 章：使用 OpenOffice.org Draw 绘图 ........................................ 275

### 第 1 章：使用 OpenOffice.org Writer 编写文档
## 本章内容

- 从他人获取文档
- 了解 OpenOffice.org Writer
- 开始使用 Writer
- 在 Writer 中准备文档

坦白说！整个世界，似乎都使用 Microsoft Office，尤其是 Microsoft Word 来写东西。要完成工作，你必须与世界接轨。直到最近，缺乏一个免费且良好的兼容 Microsoft Office 的办公套件可能阻碍了你将 Red Hat Linux 用作主要桌面操作系统的使用。好了，你的麻烦结束了。Red Hat Linux 现在附带 OpenOffice.org 办公套件——一套与 Microsoft Office 相当且兼容 Microsoft Office 的办公生产力应用程序。OpenOffice.org 应该已安装在你的系统上——你只需在 Red Hat Linux 安装期间选择 Office/Productivity 软件包组即可。如果你没有安装 Office/Productivity 软件包组，请按照 Book I、第 3 章中描述的步骤现在安装该软件包组。

OpenOffice.org Writer，简称 Writer，是 OpenOffice.org 办公套件的核心。Writer 是一款文字处理器，使你能够轻松地在 Red Hat Linux 系统上准备各种类型的文档，最重要的是，与使用 Microsoft Word 的他人共享文件。

通常你可能会处理同事和朋友（甚至可能是家人）发送给你的 Microsoft Word 文件。本章首先解释了你可能以多种不同方式接收 Microsoft Word 文件——以及收到此类文件时该怎么做。然后，本章概述了如何打开文档、对其进行工作、跟踪更改并将其保存到文件夹的方法。在此过程中，我提供了汇总如何使用 Writer 执行常见文字处理任务的表格。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_251_0.png)

在你的期望飙升之前，让我提醒你，如果你在 Microsoft Word 和 Writer 之间共享文件，你可能会遇到一些转换问题；某些 Word 功能可能无法完全转换为等效的 Writer 功能。然而，如果你只与 Microsoft Word 用户共享简单文档（或只是想准备自己的格式良好的文档），Writer 会很好地为你服务。

顺便说一下，如果你已经是熟练的 Microsoft Word 用户，你应该能够在没有太多困难的情况下开始使用 Writer，因为 Writer 的很大一部分工作方式与 Word 非常相似。

## 从他人获取文档

如果你像我一样，你经常处理与同事共享的文档。你中的某个人可能会准备一份草稿，然后其他人对其进行编辑和补充。你通常会以电子邮件附件或某些存储介质（例如软盘、Zip 磁盘或 CD-ROM）的形式接收文档。

在开始处理文档之前，你必须将其保存在硬盘上的文件夹（目录）中。以下是你可以将文档获取到硬盘上的不同方法：

- ♦ **电子邮件：** 你的电子邮件阅读器（如 Mozilla Mail 或 Ximian Evolution）具有将附件保存到目录的选项。
- ♦ **软盘：** （我假设你使用的是 DOS/Windows 格式的软盘。）将软盘插入 A 驱动器，打开一个终端窗口（通过选择 主菜单→系统工具→终端），并输入 mdir 查看软盘的内容。然后输入以下命令将指定文件复制到当前目录：
- 这里 filename.doc 是你想复制到硬盘的 Microsoft Word 文件。
- ♦ **Zip 磁盘：** Red Hat Linux 应该在 /etc/fstab 文件中为 Zip 驱动器创建一个条目，以便你可以在 /mnt/zip 目录下挂载它。将 Zip 磁盘插入驱动器并输入 mount /mnt/zip 来挂载它。现在你可以在 /mnt/zip 目录下访问 Zip 磁盘上的文件。换句话说，如果 Zip 磁盘的顶级目录上有一个文件，你可以使用以下命令将该文件复制到硬盘上的当前目录：

```
mcopy a:filename.doc .
```

```
cp /mnt/zip/filename.doc .
```

-   **CD-ROM:** 如果你使用 GNOME 或 KDE 桌面，插入 CD-ROM 到光驱后，CD-ROM 的内容应该很快就会在文件管理器窗口中出现。然后你可以将文件拖放到硬盘上的目录中。如果没有使用图形界面桌面，输入 `mount /mnt/cdrom` 来挂载 CD-ROM，然后你就可以在 `/mnt/cdrom` 目录访问 CD-ROM 的内容。

现在你手上已经有 Microsoft Word 文件了，你所需要做的就是在 Writer 中打开它并开始工作！

## 了解 OpenOffice.org Writer

在开始使用 Writer 之前，我想快速概述其主要功能。当你知道 Writer 能做什么时，你可以阅读后续章节，了解如何在 Writer 中执行特定任务，例如格式化表格、打印文档和跟踪更改。

你可以用 Writer 做以下事情：

-   打开和编辑 Microsoft Word 文件，或将 Microsoft Word 文件转换为 Writer 格式。将文件转换为 Writer 格式的一个优点是，Writer 文件的大小远小于对应的 Microsoft Word 文件。
-   以多种不同格式保存文档，包括 Microsoft Word 97/2000/XP、Word 95、Word 6.0、富文本格式 (RTF)、StarWriter 5.0（以及 4.0 和 3.0）、纯文本、Adobe PDF 和网页 (HTML)。
-   插入多种不同格式的图形文件，包括 JPEG、GIF、ZSoft Paintbrush (PCX)、TIFF、Windows BMP、Macintosh PICT、封装式 PostScript (EPS)、Adobe Photoshop (PSD)、AutoCAD DXF 等等。
-   创建可包含计算的表格，并添加在表格内容更改时自动更新的图表。
-   使用桌面出版功能（如文本框和浮动框架）执行复杂的页面布局。
-   轻松创建和组织构成大型项目（如书籍或大型报告）的多个文件。
-   创建一个 *邮件合并*，你只需编写一份包含通用字段的文档，Writer 就会自动根据数据库中的特定字段（如姓名、地址和电话号码）填充内容，从而创建许多不同的定制文档。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_253_0.png)

-   在持续更改文档的同时保存其版本，并在必要时恢复到旧版本。
-   使用版本系统比较更改并协作工作。不仅可以看到发生了什么更改以及谁更改的，还可以根据特定标准单独（或成组）接受或拒绝这些更改。
-   直接从 Writer 发送电子邮件文档。
-   如果你愿意，Writer 可以通过最佳猜测自动完成你正在输入的单词——你可以通过按 Enter 键接受该选择。（如果此功能让你抓狂，你可以简单地将其关闭，就像你可以配置 Writer 中的许多其他功能一样。）

这里需要注意：版本信息并不能完美地导出到某些其他格式——尤其是 Microsoft Word。

Writer 允许你直接将 Writer 文档打印为 Adobe 便携式文档格式 (PDF) 文件。要以最终形式电子共享文档，你可以将文档打印为 PDF 文件并分发该文件。任何人都可以轻松查看和打印 PDF 文件，只需使用免费的 Adobe Reader（可在 www.adobe.com/products/acrobat/readstep2.html 获取）。

## 开始使用 Writer

学习使用 Writer 的最佳方法是直接开始使用。要启动 Writer，请点击面板上的 Writer 图标（显示一些纸张和一支笔的图标）或选择 Main Menu>Office>OpenOffice.org Writer。

如果这是你第一次使用 Writer，地址数据源自动向导会运行并提示你输入系统上已有的地址数据的来源。如果你设置了它，你就可以使用地址数据创建邮件合并信件或文档，利用地址信息填充通用信件中的字段。如果你有 Mozilla 地址簿（例如）或其他地址列表，请选择该来源并点击 Next 以完成自动向导的步骤。否则点击 Cancel 继续使用 Writer。

Writer 也可能会显示一个对话框，提供注册为 OpenOffice.org 用户的机会。做出适当的选择——是否现在注册、稍后提醒、永不注册，或表示你已注册——然后点击 OK。

Writer 显示其主窗口（Figure 1-1），其中包含一个空文档和 Stylist——一个包含样式列表的窗口。在下一节中，我将详细介绍此主窗口。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_254_0.png)

Figure 1-1:
你可以在 Writer 主窗口中开始输入文档。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_254_1.png)

如果 Stylist 窗口挡住了视线，请按 F11 在显示和隐藏之间切换。

使用 Writer 很简单，因为它与你可能使用过的其他文字处理器非常相似，例如 Microsoft Word。例如，你可以向空白文档输入文本、格式化文本，并在完成后保存文本。（我在后面的章节“Preparing Documents in Writer”中描述了这些任务以及更多内容。）

如果你想处理已保存在硬盘上的现有文档（例如 Microsoft Word 文件），请选择 File→Open 然后从 Open 对话框中选择文档。然后你可以处理该文档并将其保存为 Word 格式、其他文字处理格式，或默认的 OpenOffice.org 1.0 Text Document 格式，文件扩展名为 .sxw。

## 检查 Writer 主窗口

为了熟悉 Writer，请先检查其主窗口中包含的用户界面组件，如图 Figure 1-2 所示。

Figure 1-2:
Writer 主窗口包含大量用户界面组件。

对象栏

功能栏

菜单栏

工具栏

状态栏

![](img/a7eec43a54473e95dc5ea333fecf1bd7_255_0.png)

如图 Figure 1-2 所示，你可以将 Writer 窗口视为以下主要部分：

-   **菜单栏** 提供标准的下拉菜单：File、Edit、Help 等等。使用这些菜单执行 Writer 能完成的所有任务。
-   **功能栏** 显示当前打开文件的完整路径名或 URL，并提供执行任务的按钮，例如打开、保存和打印文档。你也可以点击功能栏上的图标打开 Stylist（段落、字符和页面样式的列表）、Navigator（文档部分的列表，如标题、表格和书签）以及 Gallery（预定义图形对象的集合，如 3D 形状、背景和项目符号）。

-   **对象栏** 允许你通过应用样式、选择字体或更改文本属性（如粗体、斜体和下划线）来格式化文档。此栏会根据你点击的对象类型（如纯文本或图形）而变化。
-   **标尺** 显示页面尺寸和制表符位置。
-   **工具栏** 位于窗口左侧，提供可用于执行常见文档准备任务的按钮，例如插入表格、创建表单、检查拼写和显示绘图功能。
-   **状态栏** 显示打开文档的常规信息，包括当前页码和总页数。你也可以点击状态栏中的元素来更改某些设置，例如文本选择模式和查看文档的缩放系数。

除了这些部分之外，Writer 窗口的最大部分是工作区，你的文档显示在那里。那是你主要关注的地方。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_256_0.png)

使用工具提示来了解某个字段或按钮的作用。将鼠标悬停在字段或按钮上，Writer 会显示一个小型工具提示窗口，其中包含简短的帮助信息。如果你想要工具提示中提供更多信息，请通过选择 Help→Extended Tips 来打开扩展工具提示。另一方面，如果你不喜欢这些工具提示，可以通过选择 Help→Tips 和 Help→Extended Tips 来将其关闭。

如果需要，Writer 中提供帮助。从 Writer 菜单中选择 Help→Contents。这会打开 OpenOffice.org Help 窗口，如图 Figure 1-3 所示，其中包含有关 Writer 的帮助信息。点击链接查看特定帮助信息。

## 设置 Writer

你实际上不需要做任何特殊设置即可开始使用 Writer。即使是打印等任务，只要你按照 Book I, Chapter 3 所述的程序设置了打印机，就应该能立即工作。然而，有一些设置你可能想要调整，以便 Writer 按照你的喜好工作。例如，你可能想要关闭 AutoCorrect 以免它建议单词补全，或者你可能想要隐藏一些工具栏以获得更多工作空间。你可以从位于菜单栏（参见 Figure 1-2）的 View 和 Tools 菜单中设置大多数这些选项。特别是，你可以通过选择 Tools→Options 时出现的对话框（Figure 1-4）执行大多数设置任务。



![](img/a7eec43a54473e95dc5ea333fecf1bd7_257_0.png)

图 1-3：
您可以从此窗口获取有关 Writer 的帮助。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_257_1.png)

图 1-4：
可从“工具→选项”对话框设置 Writer 的许多方面。

表 1-1 总结了常见的设置任务以及如何从 Writer 的菜单中执行这些任务。

## 表 1-1 OpenOffice.org Writer 中的常见设置任务

| 执行此操作 | 使用此步骤 |
|---|---|
| 切换 Writer 窗口的各个部分显示或隐藏 | 从“视图”菜单中选择适当的项目，例如标尺、状态栏或工具栏，然后将其打开或关闭。 |
| 自定义工具栏 | 选择“视图→工具栏→自定义”。您也可以选择“工具→配置”，然后单击“状态栏”和“工具栏”选项卡来配置相应的工具栏。您也可以右键单击工具栏并从弹出菜单中选择“配置”。 |
| 自定义菜单 | 选择“工具→配置”，然后单击“菜单”选项卡。 |
| 更改各种文件的默认位置 | 选择“工具→选项”。然后选择“OpenOffice.org→路径”，并单击要更改的路径。例如，单击“我的文档”并指定文档默认位置的路径名。 |
| 在对象栏的下拉字体列表中以其字体显示字体名称 | 选择“工具→选项”。然后选择“OpenOffice.org→视图”，并选中标记为“字体列表中预览”的复选框。 |
| 显示完整菜单，包括不适用的项目 | 选择“工具→选项”。然后选择“OpenOffice.org→视图”，并选中标记为“非活动菜单项”的复选框。 |
| 显示或隐藏工具提示 | 选择“帮助→提示”以打开或关闭工具提示，并选择“帮助→扩展提示”以打开或关闭扩展工具提示。 |
| 始终创建文件的备份副本 | 选择“工具→选项”。然后选择“加载/保存→常规”，并单击“始终创建备份副本”复选框。 |
| 每 XX 分钟自动保存 | 选择“工具→选项”。然后选择“加载/保存→常规”，并单击“每 X 分钟自动保存”复选框，选择指定保存文件频率的分钟数。 |
| 显示不可打印字符，例如段落标记、制表符等 | 选择“工具→选项”。然后选择“文本文档→格式辅助”，并打开要让 Writer 显示的字符的复选框。 |
| 选择语言和货币 | 选择“工具→选项”。然后选择“语言设置→语言”，并选择区域设置、默认货币以及文档的语言。如果使用任何亚洲语言，请在文本 `Asian languages support.` 下方打开“启用”复选框。 |

表 1-1（续）

| 执行此操作 | 使用此步骤 |
|---|---|
| 选择、创建或编辑自定义词典 | 选择“工具→选项”。然后选择“语言设置→写作辅助”，并添加新词典或编辑现有词典中的单词。 |
| 更改跟踪更改的选项 | 选择“工具→选项”。然后选择“文本文档→更改”，并选择显示文档更改的选项。 |
| 更改用户信息 | 选择“工具→选项”。然后选择“OpenOffice.org→用户数据”，并输入有关您自己的信息。 |
| 关闭在首次执行某些任务时弹出的帮助代理 | 选择“工具→选项”。然后选择“OpenOffice.org→常规”，并关闭帮助代理的“激活”复选框。 |
| 设置自动更正和自动格式选项 | 选择“工具→自动更正/自动格式”，并在结果对话框中单击“选项”选项卡。打开（或关闭）自动更正选项以满足您的需求，然后单击“确定”。例如，要关闭自动词完成，请单击“词完成”选项卡并单击“完成单词”复选框以取消选中。 |

## 在 Writer 中准备文档

使用 Writer 准备文档不会有任何问题。通常，您只需单击以定位光标，然后输入文本即可。要格式化文本，请为段落选择样式或选择文本然后应用诸如粗体或斜体之类的格式。在以下各节中，我提供了有关如何在 Writer 中执行特定文档准备任务的快速提示。我将提示按以下任务类别组织：

- 编辑和审阅文档
- 使用样式和模板
- 执行页面布局
- 创建和插入图形
- 使用字段
- 处理大型文档

### 编辑和审阅文档

要编辑文档，您必须打开文件、在文档中移动、插入和删除文本并保存文件。由于这些步骤在大多数文字处理器中相似，因此您可以直观地执行其中大部分任务。因此，我不会详细讨论如何执行每项任务。相反，在下面的段落中，我仅强调了您在工作中会发现特别有用的几个功能。然后，在表 1-2 中，我提供了一份常用任务及其执行方法的列表。

通常，当您与其他人协作处理文档并对文档进行修订时，您会审阅更改。要审阅更改，必须跟踪更改。Writer 具有启用更改跟踪（通常称为红线）的功能。使用 Writer，您可以检查更改、接受或拒绝每个更改，并进行更多编辑更改——甚至添加注释来解释您为何进行更改。

Writer 还有其他便于编辑文档的功能。例如，您可以搜索和替换文本——甚至可以查找具有特定格式样式的文本的所有出现位置并更改每个出现位置。

Writer 的大多数编辑和更改跟踪功能都在“编辑”菜单中（如图 1-5 所示）。一些工具栏图标提供了菜单的快捷方式。

图 1-5：从“编辑”菜单及其子菜单执行大多数编辑和审阅任务。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_260_0.png)

表 1-2 总结了一些常见的编辑和审阅任务以及如何执行这些任务。该表未提及工具栏图标，但您可以始终将鼠标悬停在每个图标上并阅读工具提示，以查看哪些图标可让您进行特定的编辑和审阅更改。

## 表 1-2 常见编辑和审阅任务

| 执行此操作 | 使用这些步骤 |
|---|---|
| 保护文档以进行编辑 | 选择“编辑→更改→保护记录”，并在结果对话框中输入密码。要启用更改，请再次选择“编辑→更改→保护记录”，并输入您之前输入的密码。 |
| 快速跳转到文档的不同部分 | 选择“编辑→导航器”或按 F5。打开适当的类别，例如标题、表格或书签，然后双击项目以跳转到该位置。 |
| 查找并替换具有特定格式和样式的文本 | 选择“编辑→查找和替换”或按 Ctrl+F。在对话框中，输入要查找的文本，包括任何格式，并输入替换文本（如果有）。然后根据您只是想查找文本还是想查找并替换为新文本，单击“查找”或“替换”。 |
| 选择多个文本块以复制、剪切或作为组进行格式设置 | 按住 Ctrl 键的同时选择文本块。另一种方法是单击状态栏上的 STD，直到显示 ADD，然后逐个选择每个文本块。 |
| 插入特殊字符 | 定位光标并选择“插入→特殊字符”。选择要插入的字体和字符。 |
| 将某些文本设为首字母大写 | 选择文本。选择“格式→字符”，并在结果对话框中单击“字体效果”选项卡。从“效果”下拉列表中选择“标题”。 |
| 编辑超链接而不激活 URL | 按住 Alt 键并单击超链接。现在您可以编辑超链接中的文本。 |
| 向上或向下移动段落 | 单击段落，然后按 Ctrl+向上箭头或 Ctrl+向下箭头以向上或向下移动段落。 |
| 启用或禁用更改跟踪 | 选择“编辑→更改→记录”以打开或关闭复选标记。当复选标记打开时，Writer 会跟踪更改。 |
| 显示或隐藏文档上的更改 | 选择“编辑→更改→显示”以打开或关闭复选标记。当复选标记打开时，Writer 会使用修订标记显示更改。 |
| 插入注释以解释更改 | 进行更改，选择“编辑→更改→注释”，然后在出现的对话框中输入您的注释。 |
| 插入注释——与更改无关的注释 | 选择“插入→注释”，并在出现的对话框中输入注释。 |



| 执行此操作 | 使用以下步骤 |
|---|---|
| 将文档打印为 PDF 文件 | 选择 文件→打印。在打印对话框中，点击打印机列表并从下拉列表中选择 PDF 转换器。点击 确定。 |
| 保存文档的版本 | 选择 文件→版本。从出现的对话框中，选择 保存新版本。您只能在保存文档一次后才能创建新版本。 |
| 打开文档的旧版本 | 选择 文件→版本，并在对话框中选择要打开的版本。点击 打开。 |
| 合并文档 | 选择 编辑→更改→合并文档。从出现的插入对话框中，选择要与当前文档合并的文档。 |
| 接受或拒绝更改 | 选择 编辑→更改→接受或拒绝，然后从对话框中出现的列表中接受和拒绝更改。 |
| 创建 AutoText 条目 | 选择 编辑→AutoText 或按 CTRL+F3。然后输入文本和快捷方式。 |
| 插入 AutoText | 输入快捷方式并按 F3。例如，输入 BW 并按 F3 以输入文本 "Best Wishes。" BW 是 Best Wishes 的预定义快捷方式。 |
| 统计文档中的字数 | 选择 文件→属性，并在出现的对话框中点击 统计 选项卡。 |
| 查看文档属性 | 选择 文件→属性。 |
| 检查拼写 | 选择 工具→拼写检查→检查 或按 F7。 |
| 从拼写检查中排除一个词 | 双击选择该词。右键单击并从弹出菜单中选择 字符。然后点击 字体 选项卡并从 语言 下拉列表中选择 [None]。 |

## 使用样式和模板

在 Writer 中，您可以手动格式化页面、段落和文本块。例如，您可以将光标放在段落上，选择 格式→段落，然后格式化段落的各种特征（例如缩进、间距和边框）。这种逐段落的格式化对于短文档来说是可以的，但如果必须一次又一次地格式化数百个段落，就会变得繁琐且耗时。更好的方法是定义一种样式 — 一种存储在特定、通常具有描述性的名称下的格式特征集合。然后您可以将该样式简单地应用于所有段落。如果需要更改段落的任何方面，只需编辑样式即可，瞧 — 所有具有该样式的段落都会获得新的格式。

您可能熟悉 Microsoft Word 中的段落和字符样式，但 Writer 比 Microsoft Word 更依赖样式。Writer 支持五种类型的样式：页面、段落、字符、编号和框架。表 1-3 总结了每种样式控制的内容。

表 1-3 Writer 中的五种样式类型

| 此样式 | 控制此项 |
|---|---|
| 页面样式 | 页面布局，包括页边距、列数、页眉和页脚。 |
| 段落样式 | 段落的外观，例如字体、段落间距、边框、项目符号、编号以及后续段落的样式。 |
| 字符样式 | 段落中选定文本的字体样式。 |
| 编号样式 | 用于编号或项目符号列表的数字或项目符号字符及间距。 |
| 框架样式 | 框架的大小和位置以及文本环绕选项。 |

在 Writer 中，您可以方便地在一个名为 Stylist 的浮动窗口中访问和使用文档的所有样式（图 1-6）。Writer 默认显示 Stylist，但您可以通过按 F11（或选择 格式→Stylist）来显示和隐藏它。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_263_0.png)

图 1-6：按 F11 在打开和关闭之间切换 Stylist。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_264_0.png)

Stylist 使组织和使用样式变得非常容易。Stylist 顶部部分的五个图标指的是五种类型的样式 — 段落、字符、框架、页面和编号 — 从最左边到最右边。您可以点击一个图标来查看该类型的所有样式。要应用样式，将光标定位到要应用样式的位置并从 Stylist 中双击该样式。对于字符样式，选择文本然后双击字符样式。

Writer 也支持模板，就像 Microsoft Word 一样。模板是一个包含文档所需布局类型的样式集合的特殊文档。您可以将模板视为特定类型文档的模型。例如，您可能有备忘录、信件、传真封面、信封等文档的模板。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_264_1.png)

Writer 不附带任何模板，但您可以从网站上创建或下载模板。例如，使用现代语言协会（MLA）样式编写手稿的 Writer 模板（有关 MLA 样式的更多信息，请参阅 owl.english.purdue.edu/handouts/research/r_mla.html），可从 www.cc.mie-u.ac.jp/~lq20100/MLA-Template.stw 获得。您必须先安装模板文件 — MLA-Template.stw — 才能使用该模板创建文档。请注意，.stw 扩展名用于 OpenOffice.org 模板文件。

要安装要在 Writer 中使用的模板文件，请按照以下步骤操作：

- 1. 选择 文件→模板→组织。

模板管理对话框（图 1-7 所示）出现，左侧为模板的默认文件夹，右侧为当前文档列表。

图 1-7：将模板文件导入默认模板文件夹。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_264_2.png)

- 2. 右键单击默认文件夹图标并从弹出菜单中选择 从弹出菜单中导入模板，如图 1-7 所示。
- 打开对话框出现。
- 3. 导航到保存模板文件的目录，选择模板文件并点击 打开。
- 打开对话框关闭；模板现在出现在模板管理对话框的默认文件夹中。
- 4. 点击 关闭 以关闭模板管理对话框。

要从已安装的模板创建新文档，请按照以下步骤操作：

- 1. 选择 文件→新建→模板和文档。
- 出现一个包含模板的对话框。双击默认文件夹以打开它并查看模板。
- 2. 选择要使用的模板并点击 打开。
- 出现一个新文档，通常包含一些说明所选模板样式的文本。
- 3. 删除新文档中的文本并开始输入您想要的内容。
- 要查看该模板中的样式，按 F11 打开 Stylist 并通过在 Stylist 中双击它们来应用样式。

Writer 还使您能够执行与样式和模板相关的许多其他任务。例如，您可以创建样式，将样式应用于文本，将样式从一个模板复制到另一个模板，等等。表 1-4 总结了如何在 Writer 中执行涉及样式和模板的一些常见任务。

表 1-4 涉及样式和模板的常见任务

| 执行此操作 | 执行以下步骤 |
|---|---|
| 确定文档关联的模板 | 选择 文件→属性，并在出现的对话框中点击 常规 选项卡。在该选项卡下部模板字段中查找模板名称。 |
| 安装模板文件 | 选择 文件→模板→组织。右键单击默认文件夹图标并从弹出菜单中选择 导入模板。从打开对话框中选择模板并点击 打开。 |
| 指定默认模板 | 选择 文件→模板→组织。双击对话框左侧的默认文件夹以查看模板（您必须已安装模板）。选择一个模板并点击对话框右侧的 命令。然后从下拉列表中选择 设为默认模板。 |
| 创建新模板 | 创建包含所需样式的文档布局。选择 文件→模板→保存 并指定名称以将当前文件保存为模板。 |
| 编辑模板 | 选择 文件→模板→编辑。从出现的打开对话框中，选择要编辑的模板文件。 |
| 在模板之间复制样式 | 选择 文件→模板→组织。打开两个模板。从一个模板中选择样式并将其拖放到另一个模板上。 |
| 从模板创建新文档 | 选择 文件→新建→模板和文档。在出现的对话框中，打开模板文件夹，选择模板并点击 打开。 |
| 将不同模板应用于文档 | 基于要使用的模板开始新文档。然后将旧文档的内容复制到新文档中。 |
| 将样式应用于文本 | 将光标定位在文本上并选择 格式→样式 或按 F11。点击 Stylist 窗口工具栏上的第一个按钮以查看段落样式。然后双击样式以应用该样式。应用一次段落样式后，该样式会出现在对象栏的下拉列表中。 |
| 重新定义样式 | 在 Stylist 中选择样式，右键单击，选择 修改，或选择 格式→样式→目录，选择样式，点击 修改。 |
| 创建新样式 | 选择 格式→样式→目录，或按 Ctrl+Y。点击 新建 并在出现的对话框中填写信息以定义样式。 |
| 使用 AutoPilot 创建文档 | 选择 文件→AutoPilot，然后选择要创建的文档类型。填写 AutoPilot 请求的信息并点击 创建。 |

## 执行页面布局

在 Writer 中，页面样式控制页面布局，每个页面都可以有自己的样式。通常的做法是定义三种页面样式：第一页、左页和右页。用适用于第一页的任何内容定义第一页，例如特殊页眉和无页码。左页是偶数（=）页的样式，右页是奇数页的样式。对于每个页面样式，您还可以定义适用于下一页的页面样式。想法是定义左页作为第一页的下一页样式，并将右页定义为左页样式之后页面的样式。这样，只要从第一页样式开始，所有页面的页面样式就会正确。您可能还想定义一个横向页面样式，以便用于必须为横向的页面。



![](img/a7eec43a54473e95dc5ea333fecf1bd7_267_0.png)

如果你熟悉 Microsoft Word，你就知道页面设置——纸张大小、方向、页边距等等——适用于文档中的所有页面。在 Writer 中，页面样式不会自动应用于整个文档。相反，每个页面都有自己的页面样式。当然，你可以选择将相同的页面样式应用于所有页面。本质上，你在 Writer 中对页面布局有更精细的控制。

一个典型的页面布局任务是在文档中插入由其他 OpenOffice.org 应用程序创建的对象，例如 Calc 电子表格、Impress 幻灯片或 Draw 绘图。你可以通过选择 插入→对象→OLE 对象 来插入此类对象。顺便说一下，OLE 代表 Object Linking and Embedding，这只是通过添加在不同应用程序中创建的图表和绘图等组件来创建文档的能力的花哨说法。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_267_1.png)

添加组件时，请记住以下注意事项：你只能使用最初创建该组件的应用程序直接在文档中编辑该组件。

可以插入到 Writer 文档中的组件是数学公式，我指的是带有积分符号和希腊字母如 alpha 和 sigma 的严肃公式。如果你正在撰写包含复杂方程的科学论文，你会非常欣赏 OpenOffice.org 的这个功能。以下是将公式插入 Writer 文档的典型步骤序列（此过程与插入其他组件类似）：

- 1. **将光标定位并选择 插入→对象→公式。**
- 用户界面变为 OpenOffice.org Math——一个用于编写数学公式的应用程序，并且文档中会出现一个用于公式的小框架。公式在该框架中排版。
- 
- 2. **从“选择”窗口的前两行中选择公式类型。**
- “选择”窗口中的下几行显示该类型的可用公式。例如，求和类别（用大写希腊字母 sigma 表示）包括积分符号。
- 
- 3. **点击特定的公式，例如积分。**
- 该公式的 Math 命令出现在“命令”窗口中，公式的部分内容出现在文档中。
- 
- 4. **填写公式的参数。**
- 当你使用“命令”窗口中的命令构建公式时，格式化的公式会出现在文档中（图 1-8）。
- 
- 5. **要更改公式的字体大小，请选择 格式→字体大小 并指定字体大小。**

![](img/a7eec43a54473e95dc5ea333fecf1bd7_268_0.png)

图 1-8：
使用 Math 应用程序向 Writer 文档中插入数学公式。

- 6. 在 Writer 文档中的其他位置单击以返回 Writer 用户界面。
- 7. 双击公式再次编辑它。

当然，Writer 具有许多页面布局功能。你可以使用表格、编号和项目符号列表以及列。Writer 还支持框架——矩形框，你可以在其中放置文本、图形甚至其他框架。使用框架，你可以在文档的任何位置放置几乎任何内容。表 1-5 总结了如何在 Writer 中执行一些常见的页面布局任务。

| 表 1-5 | 常见页面布局任务 |
|---|---|
| 执行此操作 | 按以下步骤操作 |
| 插入分页符 | 选择 插入→手动分隔符 然后在结果对话框中选择“分页符”。 |
| 设置页面边距 | 选择 格式→页面。然后单击“页面”选项卡并指定边距。 |

## 表 1-5（续）

| 执行此操作 | 按以下步骤操作 |
|---|---|
| 插入页眉和页脚 | 选择 插入→页眉 或 插入→页脚 并指定你希望页眉或页脚出现在所有页面还是仅第一页。 |
| 仅在第一页插入页眉 | 将光标放在第一页并选择 格式→样式（或按 F5）。单击“页面样式”图标（从左数第四个图标）并双击“第一页”样式。选择 插入→页眉→第一页，然后在第一页页眉中输入你想要的文本。 |
| 从自动编号序列更改页码 | 选择 插入→手动分隔符 然后选择“分页符”以及页面的样式。然后打开标记为“更改页码”的复选框并输入你想要的页码。 |
| 在纵向文档中插入横向页面 | 按 F11 打开“样式”。单击“页面样式”图标（从左数第四个图标）。右键单击“默认”样式并选择“新建”。将新样式命名为“横向”并将“默认”指定为下一个样式，单击“页面”选项卡，选择“横向”方向，然后单击“确定”。现在选择 插入→手动分隔符，选择“分页符”，样式为“横向”。 |
| 将页面布局为列 | 选择 格式→页面 并在结果对话框中单击“列”选项卡。然后选择列数并单击“确定”。 |
| 将选定文本布局为列 | 选择文本。选择 插入→节 并在结果对话框中单击“列”选项卡。然后选择列数并单击“插入”。 |
| 使用框架 | 选择 插入→框架 并从“框架”对话框中的选项卡中选择选项。你可以链接框架，使文本从一个框架流向下一个框架。 |
| 插入表格 | 选择 插入→表格 或按 Ctrl+F12。从结果对话框中格式化表格。 |
| 合并两个表格 | 将两个表格一个接一个地放置，中间没有任何其他文本。右键单击任一表格并选择“合并表格”选项（该选项仅在表格相邻时出现）。 |
| 插入由其他 OpenOffice.org 应用程序创建的对象 | 定位光标并选择 插入→对象→OLE 对象。从“插入 OLE 对象”对话框中，选择你想要的对象类型。如果要从文件插入对象，请选择“从文件创建”单选按钮并单击“确定”。 |

| 执行此操作 | 按以下步骤操作 |
|---|---|
| 插入数学公式 | 定位光标并选择 插入→对象→公式。OpenOffice.org Math 应用程序的用户界面出现。使用公式选择和准备窗口创建公式并调整字体大小。当你构建公式时，它会出现在文档中。单击文档中的其他位置以返回 Writer。双击公式再次编辑它。 |
| 插入图表 | 定位光标并选择 插入→图表 以插入包含虚拟数据的图表。双击图表，Impress 的用户界面会出现。要编辑图表的虚拟数据，请选择 编辑→图表数据。虚拟数据出现在迷你电子表格窗口中。编辑数据并单击绿色复选标记。要更改图表类型，请选择 格式→图表类型。然后从结果对话框中选择图表类型。单击文档中的其他位置以返回 Writer。 |
| 创建大纲样式的编号列表，项目编号为 1、1.1、1.2、... 2、2.1 等 | 输入列表项，选择它们，并按 F11 打开“样式”。单击“编号样式”图标（从左数第五个图标）并双击“编号 5”样式。单击列表并注意对象栏上的右箭头（显示样式名称的栏）。单击右箭头，编号列表图标会出现。单击每个子编号项，然后单击右箭头图标。 |
| 创建悬挂缩进 | 按 F11 显示“样式”（如果尚未可见）。单击“段落样式”图标（从左数第一个图标）。将光标放在文本上，然后在“样式”中双击“悬挂缩进”样式。 |
| 预览页面 | 选择 文件→页面预览。要返回编辑，请再次选择 文件→页面预览。 |
| 显示垂直标尺 | 选择 工具→选项。然后从结果对话框中选择 文本文档→视图。打开标记为“垂直标尺”的复选框并单击“确定”。 |

## 创建和插入图形

Writer 包含一个绘图工具栏，其中包含可在文档中绘图的工具。你还可以将线条图和来自多种不同格式文件的图像插入到文档中。

要在文档中创建简单的图表，请单击“显示绘图功能”图标（在 Writer 窗口左侧的工具栏上）并按住鼠标按钮片刻。绘图功能工具栏会出现，如图 1-9 所示。

图 1-9：
绘图功能工具栏。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_271_0.png)

在文档中单击你想要添加图表的位置。从绘图功能工具栏（图 1-9）中选择一个工具并开始绘图。要更改绘图工具，请再次打开绘图功能工具栏并选择另一个工具。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_271_1.png)

要在创建图表时保持绘图功能工具栏可见，请按通常方式打开工具栏，单击工具栏的顶部部分，然后将其拖离。工具栏随后会变成一个可撕下菜单（一个在文档窗口中浮动的小窗口），你可以从中轻松选择和使用不同的绘图工具。

Writer 还附带一个预定义图形的画廊。要查看画廊（图 1-10 所示），请选择 工具→画廊 或单击画廊图标（功能栏上最右边的图标）。从画廊左侧的主题中进行选择。如果看到你想要使用的图形，请将其从画廊拖放到文档中你想要插入的位置。再次单击画廊图标以隐藏图形画廊。

图 1-10：
将图形从画廊拖放到文档上。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_271_2.png)

表 1-6 总结了你如何在 Writer 中执行涉及图形的一些常见任务。



表 1-6 涉及图形的常见任务

| 执行此操作 | 按以下步骤操作 |
|---|---|
| 创建绘图对象 | 单击左侧工具栏上的“显示绘图功能”图标（将鼠标悬停并阅读工具提示以定位图标）。选择绘图工具，然后在文档上绘图。 |
| 插入图形文件 | 选择 插入→图形→从文件。 |
| 锚定图形 | 右键单击图形，从弹出菜单中选择“锚定”，然后选择锚定图形的选项。 |
| 在图形周围环绕文字 | 右键单击图形，从弹出菜单中选择“环绕”，然后选择其中一种环绕选项。 |
| 为图形创建标题 | 右键单击图形并从弹出菜单中选择“标题”。 |
| 插入水印 | 选择 格式→页面 并单击结果对话框中的“背景”选项卡。从“作为”下拉列表中选择“图形”，单击“浏览”按钮，然后选择图形。选择其他选项，例如是否希望图形平铺页面或仅在指定位置放置一份副本。您也可以使用绘图工具准备图形，右键单击该图形并选择“排列→置于背景”；再次右键单击该图形并选择“排列→置于页面”。图形现在应显示为水印。 |
| 在每一页顶部插入图形（例如徽标） | 通过选择 插入→页眉→全部 在每页上插入页眉。单击页眉中，选择 插入→图形→从文件，然后选择要插入的图形文件。 |

## 使用字段

把字段想象成可能发生变化的信息片段，但你希望为其命名并在文档中使用。例如，你可能希望在文档的页眉中插入今天的日期和页码。你可以通过插入引用日期和页码的字段来实现。一些预定义字段（如日期和页码）很容易使用。只需选择 插入→字段 然后选择要插入的字段（图 1-11）。

除了图 1-11 所示的插入菜单中的字段外，你还可以从更多字段中选择。选择 插入→字段→其他 以打开“字段”对话框（图 1-12），在其中可以浏览并选择要在文档中使用的其他字段。从“字段”对话框中，你还可以更改字段的格式。例如，你可以选择日期字段在文档中的显示方式。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_273_0.png)

图 1-11：
选择 插入→字段 并选择要插入的字段。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_273_1.png)

图 1-12：
使用“字段”对话框选择其他字段或选择格式。

另一种有用的字段类型是 *引用* 或 *书签*。其思想是通过名称标记文档中的位置，然后通过该指定名称在其他地方引用该位置。例如，你可以插入对该位置所在页面的交叉引用。

表 1-7 总结了一些涉及字段的常见任务以及如何在 Writer 中执行这些任务。

| 表 1-7 | 涉及字段的常见任务 |
|---|---|
| 执行此操作 | 按以下步骤操作 |
| 插入字段 | 选择 插入→字段 并选择你想要的预定义字段（如页码、页数、日期、文件名）或选择“其他”以从对话框中选择字段。 |
| 在文本中插入公式的值 | 将光标定位并按 F2。在对象栏上输入公式并单击绿色复选标记。公式的值将作为字段出现在文本中。要再次编辑公式，请选择该字段并按 F2。 |
| 插入书签 | 单击你想要书签的位置，然后选择 插入→书签。输入书签的名称并单击“确定”。 |
| 插入对书签的交叉引用 | 选择 插入→交叉引用。然后选择要插入的书签以及交叉引用在文本中出现的格式（例如页码或书签的名称）。 |
| 设置引用 | 单击文本然后选择 插入→交叉引用。在对话框中单击“设置引用”并为此引用分配一个名称。 |
| 插入对标题的交叉引用 | 在标题处设置引用并将光标定位到想要插入交叉引用的位置。选择 插入→交叉引用 并单击“插入引用”，选择引用，选择引用的格式，然后单击“插入”。 |

## 处理大型文档

什么是大型文档？嗯，我认为任何超过一百页左右的文档都算作大型文档。任何可能包含几章并需要目录和索引的东西肯定属于大型文档——例如，一本书。Writer 包含在处理这些更大、更笨重的文档时你通常想要做的“常规事情”的功能，例如创建目录、插入索引和添加索引条目。

Writer 还使你能够将多个 Writer 文件绑定成一个大型文档——Writer 称之为主文档。例如，主文档非常适合书籍。你可以将章节保存在单独的文件中，然后使用主文档功能将这些文件组织成一本书。对于涉及主文档的大型项目，你需要稍微规划一下并处理以下关键步骤（请参阅表 1-8 了解具体内容）：

- 1. **创建一个包含所需样式以及计划使用的任何字段的模板。**
- 有关样式和模板的更多信息，请参阅本章前面 appropriately named section "使用样式和模板"。
- 2. **使用相同的模板创建各个文件和主文档。**
- 3. **将文件插入主文档——这就是将所有单独部分组合成最终产品的方式。**
- 4. **根据需要添加目录、索引和书目。**
- 5. **处理组件文件。**
- 6. **更新目录和索引。**

表 1-8 总结了一些与大型文档相关的常见任务以及如何在 Writer 中执行这些任务。

### 表 1-8 与大型文档相关的常见任务

| 执行此操作 | 按以下步骤操作 |
|---|---|
| 创建主文档 | 使用你想要的模板创建一个新文件。然后选择 文件→发送→创建主文档。分配名称，选择目录并保存文件。导航窗口出现，你可以从中选择要插入到主文档中的文件。 |
| 将文件插入主文档 | 使用导航器插入文件或选择 插入→文件。 |
| 插入索引条目 | 选择你想要插入到索引中的文本。然后选择 插入→索引和表格→条目。 |
| 创建目录、插图列表或索引 | 选择 插入→索引和表格→索引和表格。单击“索引/表格”选项卡并选择表格类型。对于目录，选择目录作为类型。要选择应包含在表格中的段落样式，请单击“附加样式”复选框，然后单击相邻按钮以指定要包含在表格中的样式。 |
| 更新目录或索引 | 右键单击表格然后选择“更新索引/表格”。 |
| 插入脚注和尾注 | 选择 插入→脚注，选择你的选项，然后单击“确定”。然后输入脚注文本。 |
| 创建书目数据库 | 选择 工具→书目数据库。然后在“书目数据库”窗口中填写书目信息。 |
| 将书目引用插入文本 | 选择 插入→索引和表格→书目条目 并选择要插入的条目。 |

### 第 2 章：使用 OpenOffice.org Calc 准备电子表格

## 本章内容

- ✓ 了解 OpenOffice.org Calc
- ✓ 开始使用 Calc
- ✓ 使用 Calc

VisiCalc 这个名字对你意味着什么？Lotus 1-2-3 呢？我确信你听说过 Lotus 1-2-3，但也许没有听说过 VisiCalc——它是第一款将 IBM PC 变成业务工具的电子表格程序。（信不信由你，你甚至可以在今天的 PC 上下载并运行 VisiCalc——有关更多信息，请访问 Dan Bricklin 的网站 www.bricklin.com/history/vcexecutable.htm。）

电子表格程序仍然是办公套件的主流，OpenOffice.org 套件也不例外。OpenOffice.org Calc，或简称 Calc，是 OpenOffice.org 套件中的电子表格程序。

VisiCalc 之后出现的所有电子表格程序——从 Lotus 1-2-3 到 Microsoft Excel 和 Calc——仍然遵循以行和列排列的电子表格的视觉模型。当然，较新的电子表格（如 Excel 和 Calc）具有更多花哨的功能，包括精美的 GUI。

如果你使用过任何其他电子表格程序，如 Microsoft Excel，你开始使用 Calc 时会感到宾至如归。因此，在本章中，我不试图详细介绍如何使用 Calc；相反，我提供一个快速概述和一些总结如何在 Calc 中执行一些常见任务的表格。

## 了解 OpenOffice.org Calc

在描述你可以在 Calc 中执行的类型任务之前，我想强调 Calc 的关键功能。Calc 可以执行你在电子表格程序中期望的所有基本电子表格功能。以下是你可以用 Calc 做的事情：


- 打开并编辑 Microsoft Excel 文件，或将 Microsoft Excel 文件转换为 Calc 格式。Calc 使用 XML 格式并以 .SXC 扩展名保存文件。
- 以多种不同格式保存文档，包括 Microsoft Excel 97/2000/XP、Excel 95、Excel 5.0、dBASE、StarCalc 5.0（以及 4.0 和 3.0）、SYLK（一种旧的 Microsoft 格式）、逗号分隔值（CSV）和网页（HTML）。
- 使用图表工具以 2D 或 3D 图表可视化数据。
- 插入多种不同格式的图形文件，包括 JPEG、GIF、ZSoft Paintbrush（PCX）、TIFF、Windows BMP、Macintosh PICT、封装式 PostScript（EPS）、Adobe Photoshop（PSD）、AutoCAD DXF 等。
- 在持续更改电子表格的同时保存其版本，以便在必要时恢复到旧版本。
- 使用样式和模板格式化电子表格。
- 定义单元格以根据单元格中的值动态更改格式。
- 通过使用 DataPilot 轻松地与现有数据库交换——导入和导出——数据。
- 设置单元格以接受来自特定值集合或有效值范围的值。
- 锁定单元格以防止数据被意外更改。
- 通过在同一单元格块中存储多个值来执行情景分析——并定义情景，以便您可以为特定情景选择一组值。
- 使用“目标查找”功能确定会使公式产生所需结果的单元格值。

## 开始使用 Calc

最佳学习使用 Calc 的方法是直接开始使用它。要启动 Calc，请在面板上单击 Calc 图标——显示电子表格和饼图的图标——或选择 主菜单→Office→OpenOffice.org Calc。Calc 窗口打开并显示空白电子表格。然后您可以开始在单元格中输入文本和数字，并使用公式计算所需内容。

## 检查 Calc 主窗口

为了熟悉 Calc，请花点时间检查 Calc 主窗口中（如图 2-1 所示）包含的工具和图标。

对象栏

函数栏

菜单栏

函数自动完成功能图标

![](img/a7eec43a54473e95dc5ea333fecf1bd7_278_0.png)

图 2-1：
您可以通过其工具和图标栏控制 Calc。

工具栏

状态栏

选项卡

公式栏

请注意主 Calc 窗口中的以下主要部分（参见图 2-1）：

- 菜单栏提供标准下拉菜单：文件、编辑、帮助等。使用这些菜单执行 Calc 可以完成的所有任务。
- **函数栏**显示当前打开文件的完整路径名或 URL，并提供执行常规任务的按钮：打开、保存和打印文档。您还可以单击函数栏上的图标打开样式（单元格和页面样式列表）、导航器（电子表格项目如工作表和图形的列表）以及画廊（预定义图形对象如 3D 形状、背景和项目符号的集合）。
- **对象栏**使您能够通过应用样式、选择字体或更改文本属性（如粗体、斜体和下划线）来格式化文档。此栏会根据您单击的对象类型（如纯文本或图形）而变化。
- **公式栏**提供一个字段，您可以在其中输入公式、创建求和并启动函数自动完成功能。
- **工具栏**位于窗口左侧，提供可用于执行常见任务的按钮，例如插入图形、排序单元格、检查拼写和分组单元格。
- **选项卡**位于电子表格底部，可让您在同一文件中处理不同的工作表。
- **状态栏**显示有关当前工作表的信息（当前工作表编号、工作表编号、页面样式等）。您还可以单击状态栏中的各个元素来更改设置，例如文本选择模式和查看电子表格的缩放系数。

除了这些工具和图标栏之外，Calc 窗口的最大部分是工作区，您的电子表格显示在其中，您在此处集中大部分注意力。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_279_0.png)

使用工具提示了解图标或菜单选项的作用。将鼠标悬停在工具栏图标或菜单项上，Calc 会显示一个小工具提示窗口，其中包含简短的帮助信息。

注意：对图 2-1 中指出的那个函数自动完成功能图标感到好奇吗？请查看本章后面的“计算和图表数据”部分，我将在其中向您展示如何使用这个方便的小功能。

## 设置 Calc

您可以通过 工具→选项 对话框配置 Calc。在对话框左侧，单击“电子表格”旁边的加号 (+) 。加号变为减号 (-) ，并出现多个不同的选项类别（如图 2-2 所示）。然后您可以单击每个类别来配置 Calc 的各个方面。

图 2-2：
从 工具→选项 对话框中的“电子表格”类别设置 Calc。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_280_0.png)

## 使用 Calc

使用 Calc 准备电子表格很简单。通常，您可以将文本和数字输入单元格，通过拖动垂直线调整列大小，并输入公式来计算所需的答案。为了帮助您执行 Calc 中的一些常见任务，我提供了一些快速参考信息，按两大任务类别组织：

- 输入和格式化数据
- 计算和图表数据

## 输入和格式化数据

在输入和格式化数据时，使用 Calc 的方式与使用 Microsoft Excel 相同。您可以将条目输入单元格，使用公式，并格式化单元格（如指定值的类型和小数点后的位数）。

格式菜单（如图 2-3 所示）包含格式化电子表格的许多选项。借助工具提示，您只需将鼠标悬停在菜单项上即可获得有关该菜单项作用的提示。

在完成电子表格的数据输入后，通过选择 文件→另存为 来保存它。会出现一个对话框，您可以在其中指定文件格式、目录位置和文件名。您以前见过类似的“另存为”对话框无数次。OpenOffice.org Calc 可以以多种格式保存文件，包括 Microsoft Excel 97/2000/XP、Microsoft Excel 95、Microsoft Excel 5.0 以及带逗号分隔值的文本文件（CSV）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_281_0.png)

图 2-3：
从“格式”菜单执行许多格式化任务。

如果您想与 Microsoft Excel 交换文件，请以 Microsoft Excel 格式保存电子表格（选择 Excel 的适当版本）。然后您可以将该文件传输到 Windows 系统并在 Microsoft Excel 中打开它。

保存电子表格一次后，您还可以保存电子表格的中间版本。要保存新版本，请选择 文件→版本，然后在下一个对话框中单击“保存新版本”。

表 2-1 总结了 Calc 中一些常见的数据输入和格式化任务。我还展示了将电子表格打印为 Adobe 便携式文档格式（PDF）文件的步骤。要与不使用 Calc 或 Excel 的人共享电子表格，您可以将电子表格打印为 PDF 文件然后发送给他人，因为任何人都可以轻松地使用免费的 Adobe Reader 查看和打印 PDF 文件（请参阅 www.adobe.com/products/acrobat/readstep2.html）。

表 2-1 常见数据输入和格式化任务

| 执行此操作 | 按以下步骤操作 |
|---|---|
| 创建新的电子表格 | 选择 文件→新建→电子表格。 |
| 从模板创建电子表格 | 选择 文件→新建→模板和文档。在 resulting 对话框中，双击模板文件夹，选择模板，然后单击“打开”。请注意，如果您尚未添加任何模板，这里将看不到任何模板。 |
| 打开现有电子表格 | 选择 文件→打开 并从 resulting 打开对话框中选择文件。 |




| 执行此操作 | 操作步骤 |
|---|---|
| 向电子表格添加工作表 | 右键单击要添加新工作表的[content]

| 执行此操作 | 操作步骤 |
|---|---|
| 向电子表格添加工作表 | 右键单击要添加新工作表的工作表标签。从弹出菜单中选择“插入”，在 resulting 对话框中填写选项，然后单击“确定”。 |
| 在单元格中输入数据或公式 | 单击单元格并输入数据。要输入公式，请单击公式栏中的绿色复选标记。 |
| 自动换行 | 右键单击单元格并从弹出菜单中选择“设置单元格格式”。在对话框中单击“对齐”选项卡，并在对话框底部打开换行。 |
| 直接在单元格中编辑内容 | 双击单元格，游标出现以便您可以编辑内容。 |
| 自动填充单元格 | 用您希望在填充单元格范围时自动递增的数据（例如数字、日期或单元格引用）填充第一个单元格。选择该单元格，然后拖动单元格右下角的填充柄。例如向下移动时，您会看到单元格被自动填充数字，随着移动数字越来越大。 |
| 隐藏行或列 | 右键单击行或列标签并从弹出菜单中选择“隐藏”。 |
| 显示隐藏的行或列 | 选择隐藏行或列两侧的行或列。右键单击行或列标签并从弹出菜单中选择“显示”。 |
| 自动格式化单元格范围 | 拖动并选择单元格。选择“格式→自动格式”。从 resulting 对话框中选择您想要的格式和选项。 |
| 从数据源引入数据 | 选择“数据→数据透视→开始”。使用后续对话框选择数据源并选择要引入电子表格的数据。 |
| 在电子表格中移动 | 选择“编辑→导航器”或按 F5 启动导航器窗口。双击诸如工作表之类的项目即可跳转到该位置。 |
| 在单元格中查找和替换文本 | 选择“编辑→查找和替换”或按 Ctrl+F。在 resulting 对话框中，填写要查找的文本和替换文本。然后单击适当的按钮（如“查找全部”、“查找”、“全部替换”或“替换”）来查找和替换文本。 |
| 创建不滚动的行或列区域 | 选择不应滚动的范围中的最后一行或最后一列。选择“窗口→冻结”。 |
| 对单元格应用样式 | 按 F11 或选择“格式→样式”打开样式窗口。单击要格式化的单元格，然后双击要应用的样式。 |

## 表 2-1（续）

| 执行此操作 | 操作步骤 |
|---|---|
| 根据单元格值应用不同样式 | 选择要进行条件格式化的单元格。选择“格式→条件格式”。在 resulting 对话框中，指定条件（如单元格值是否大于某值）以及要为每个条件应用的样式。 |
| 从文件插入图形 | 单击要插入图形的单元格，然后选择“插入→图形→从文件”。从“插入图形”对话框中选择图形文件，然后单击“打开”。 |
| 保护工作表免受任何更改 | 选择“工具→保护→工作表”。在下一个对话框中输入密码。 |
| 创建电子表格的 PDF 版本 | 选择“文件→打印”。在“打印”对话框中，单击打印机列表，并从下拉列表中选择 PDF 转换器。单击“确定”。 |
| 保存电子表格 | 选择“文件→另存为”。在对话框中，输入文件名并选择要保存文件的格式。 |
| 保存电子表格的版本 | 选择“文件→版本”。从 resulting 对话框中，选择“保存新版本”。（只有在保存电子表格一次后才能创建新版本。） |
| 打开电子表格的旧版本 | 选择“文件→版本”并从对话框中选择要打开的版本。单击“打开”。 |

## 计算和图表数据

要执行计算，请使用您在 Microsoft Excel 中通常使用的公式。例如，使用公式 SUM(D2:D6) 将 D2 到 D6 单元格中的条目相加。要将单元格 D2 设置为 A2 和 C2 条目的乘积，请在单元格 D2 中输入 =A2*C2。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_283_0.png)

要了解 OpenOffice.org Calc 中可用的更多函数，请从菜单中选择“帮助→内容”。这将打开 OpenOffice.org 帮助窗口，您可以按类别浏览函数并单击函数以阅读更多信息。

Calc 的一个有趣功能是对方案的支持。方案只是对一个或多个单元格的值的集合。当您比较某些单元格对电子表格中其他计算的影响时，方案很有用。例如，贷款的月付款将取决于本金、利率和贷款期限。您可以使用 Calc 的方案功能比较多个不同方案的月付款，其中每个方案都有利率和贷款期限（以月为单位）的特定组合。要使用方案进行此比较，请按照以下步骤操作：

- 1. 使用本金、年利率（百分比）和贷款期限（以月为单位）的标签和值设置电子表格单元格。使用以下公式计算月付款：
- 2. 选择要包含在方案中的单元格并选择“工具→方案”。
- 3. 填写方案名称，然后单击“确定”。
- 4. 在单元格中输入值——本金、利率和贷款还款月数。

```
-PMT(MONTHLY_RATE,MONTHS,PRINCIPAL)
```

“创建方案”对话框出现。

方案名称出现在构成方案的单元格上方的下拉菜单中（如图 2-4 所示）。单元格值定义了该方案的含义。

Figure 2-4:
使用方案比较不同值集合对计算的影响。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_284_0.png)

- 5. 对其他方案重复步骤 2、3 和 4，其中每个方案都有本金金额、利率和贷款期限（以月为单位）的组合。
- 6. 从下拉列表中选择一个方案（参见图 2-4）以查看该方案的月付款。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_285_0.png)

要确定某个特定单元格在某些计算中被使用的位置，请单击该单元格然后选择“工具→侦探→追踪依赖项”。Calc 绘制箭头以显示该单元格被使用的位置。

如果您记不起某个函数，请使用函数自动完成功能构建单元格中的公式。要使用函数自动完成功能，请按照以下步骤操作：

- 1. **单击公式栏上的函数自动完成功能图标（参见图 2-1）。**
自动完成功能对话框出现。
- 2. **向下滚动函数列表并双击您想要的函数。**
这样会导致公式及其参数出现（图 2-5），等待您指定要用作参数的值。
- 3. **单击每个参数并确定应用作该参数的单元格。**
当您指定所有参数时，结果字段（图 2-5 中显示）显示该公式的结果。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_285_1.png)

Figure 2-5:
使用函数自动完成功能交互式构建公式。

- 4. **单击“确定”。**
公式出现在电子表格单元格中。

表 2-2 总结了您可以在 Calc 中执行的某些常见计算和数据绘图任务。

| 表 2-2 | 常见计算和图表任务 |
|---|---|
| 执行此操作 | 操作步骤 |
| 求和行或列 | 单击要放置总和的单元格。单击公式栏上的求和图标（大写希腊字母“sigma”）。Calc 插入逻辑单元格范围的总和。要更改单元格范围，请拖动并突出显示要添加的单元格。然后单击公式栏上的绿色复选标记。 |
| 使用函数自动完成功能构建公式 | 单击要放置函数的单元格。单击公式栏上的函数自动完成功能图标（求和图标左侧的图标——大写希腊字母 sigma）。在自动完成功能中单击“函数”选项卡并选择函数类别和特定函数。填写其他必要信息，例如用作函数参数的单元格范围。 |
| 插入图表 | 选择图表的单元格并选择“插入->图表”。从 resulting 自动格式图表对话框中选择选项和图表类型。单击“创建”以插入图表。 |
| 编辑图表 | 双击要编辑的图表部分。从 resulting 对话框中选择选项。使用工具栏上的图标（双击图表时图标会更改）执行其他任务（如打开或关闭图表的各个部分以及更改图表类型）。 |
| 执行“目标求解” | 单击包含公式的单元格。选择“工具->目标求解”。在“目标求解”对话框中，输入公式的目标值。在“可变单元格”字段中，输入应调整其值以达到目标的单元格。单击“确定”完成目标求解。 |
| 创建方案 | 选择计划为每个方案更改其值的单元格。选择“工具->方案”。为方案分配名称并单击“确定”。在单元格中输入值。对要定义的每个方案重复此操作。 |
| 使用方案 | 定义使用方案中包含的单元格的公式。然后，您可以通过从方案下拉列表中选择每个方案来查看不同方案的结果。 |




### 第三章：使用 OpenOffice.org Impress 制作演示文稿

### 本章内容

- ✓ 了解 OpenOffice.org Impress
- ✓ 开始使用 Impress
- ✓ 使用 Impress

看起来商业世界，或者说整个世界，都充斥着 PowerPoint 战士——那些以 PowerPoint 简报包（幻灯片演示）为生的虔诚人士。很难想象一场会议或会议中没有人用 PowerPoint 在屏幕上激烈地阐述观点。说实话：这类程序将会长期存在。制作演示文稿是生活的一部分；商界人士已经期望办公应用套件包含某种演示软件。

与 Microsoft Office 一样，OpenOffice.org 办公应用套件也附带了自己的类似 PowerPoint 的演示软件——OpenOffice.org Impress（简称 Impress）。如果你使用过 Microsoft PowerPoint，并且已经熟悉其原理——幻灯片的概念，如何向幻灯片添加文字和图形，如何组织幻灯片以及如何运行幻灯片放映——那么你会发现开始使用 Impress 很简单。因为执行基本 Impress 任务的某些细节可能与在 PowerPoint 中的做法不同，我提供了一些快速参考表来指引方向。我首先对 Impress 进行概述，然后介绍你在使用 Impress 时可能执行的常见任务类别。

## 了解 OpenOffice.org Impress

你会发现 Impress 可以完成演示软件如 Microsoft PowerPoint 所能完成的所有常规功能。例如，你可以在 Impress 中创建专业外观的幻灯片放映，使用以下功能：

- ♦ 打开和编辑 Microsoft PowerPoint 文件，或将 Microsoft PowerPoint 文件转换为 Impress 格式。转换为 Impress 格式的一个优点是 Impress 文件的大小小于相应的 Microsoft PowerPoint 文件。以 Impress 格式存储的演示文稿文件的文件名带有 .sxi 扩展名。
- 以多种不同格式保存文档，包括 Microsoft PowerPoint 97/2000/XP、StarDraw 5.0 和 3.0 以及 StarImpress 5.0 和 4.0。
- 从多种不同格式的文件中插入图形和剪贴画，包括 JPEG、GIF、ZSoft Paintbrush（PCX）、TIFF、Windows BMP、Macintosh PICT、封装式 PostScript（EPS）、Adobe Photoshop（PSD）、AutoCAD DXF 等等。
- 将其他 OpenOffice.org 文档（来自 Writer、Calc 和 Draw 等程序）插入演示文稿。
- 使用 AutoPilot 快速创建演示文稿。
- 使用 OpenOffice.org Draw 的所有绘图工具向幻灯片添加绘图。
- 将演示文稿导出为带或不带框架的网页（HTML）。你也可以将幻灯片导出为任何受支持的图形文件格式。
- 使用图层分隔幻灯片的各个部分，以便每个部分可以单独编辑或查看。
- 使用特殊效果，如动画文字和图形、声音以及幻灯片切换效果。
- 使用 FontWork（格式→FontWork）创建各种文字效果，如沿曲线对齐文字。
- 将文字渲染为 3D。
- 在继续更改演示文稿的同时保存其版本，必要时可恢复到旧版本。
- 为每张幻灯片添加演讲者备注并创建讲义。

## 开始使用 Impress

使用 Impress 最好的方法就是直接开始使用。要启动 Impress，请在面板上单击 Impress 图标——显示条形图和幻灯片的图标，或选择 主菜单→Office→OpenOffice.org Impress。

AutoPilot 演示窗口（见图 3-1）出现并引导你完成创建新演示文稿的步骤。

如图 3-1 所示，你可以创建空白演示文稿、从模板创建演示文稿或打开现有演示文稿。如果你选择空白演示文稿并单击“下一步”，AutoPilot 会要求你选择幻灯片设计和幻灯片切换效果（即 Impress 如何从一张幻灯片移动到下一张）。然后你可以单击“创建”打开 Impress 窗口，在其中选择第一张幻灯片的版式。完成一张幻灯片的布局后，你可以继续插入新幻灯片。对于每张幻灯片，你都可以选择想要的版式。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_290_0.png)

图 3-1：
此 AutoPilot 可帮助你在 Impress 中开始新的演示文稿。

你可以在 Impress 中打开和编辑 Microsoft PowerPoint 文件。要打开现有文件，请选择 文件→打开，然后选择要打开的文件。

在使用 Impress 创建幻灯片之前，花点时间查看 Impress 窗口（见图 3-2）。

在图 3-2 中，注意 Impress 窗口的主要部分：

- 菜单栏提供标准下拉菜单，如文件、编辑和帮助，用于执行 Impress 可以完成的所有任务。
- 功能栏显示当前打开文件的完整路径名或 URL，并提供执行打开、保存和打印文档等任务的按钮。你也可以单击功能栏上的图标打开样式、导航器和图库。
- 对象栏使你能够通过应用样式、选择字体或更改文字属性（如粗体、斜体和下划线）来格式化文档。此栏会根据你单击的对象类型而变化（例如纯文本或图形图像）。
- 窗口左侧的工具栏提供按钮，可用于执行常见任务，如插入图形、排序单元格、检查拼写和组合单元格。
- 标尺显示垂直和水平页面尺寸。
- 幻灯片底部的导航栏使你能够更改视图并选择要处理的幻灯片。
- 状态栏显示有关当前幻灯片的信息，如当前幻灯片编号和幻灯片总数。你也可以单击状态栏中的元素并更改设置，如查看幻灯片的缩放系数。

对象栏

功能栏

菜单栏

标尺

![](img/a7eec43a54473e95dc5ea333fecf1bd7_291_0.png)

图 3-2：
使用 Impress 中的菜单和工具栏创建幻灯片演示文稿。

状态栏

导航栏

工具栏

样式

除了这些工具和图标栏之外，你还可以打开另外两个工具栏（可见时，这些工具栏出现在窗口底部，状态栏上方）：

- 选择 查看→工具栏→选项栏 以打开出现在导航栏下方的选项栏。选项栏显示图标，通过这些图标可执行某些绘图任务，如编辑曲线、显示网格线以及指示单击文字和其他对象时发生的情况。
- 选择 查看→工具栏→颜色栏 以打开出现在窗口底部、状态栏正上方的颜色栏。颜色栏显示颜色，可供挑选并用于对象。你可以通过单击颜色栏左上角的向下指向箭头来显示或隐藏颜色栏。

Impress 窗口最大的一部分是工作区，在此你处理当前幻灯片，也是你关注的主要区域。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_292_0.png)

使用工具提示来了解图标或菜单选项的作用（图 3-2 显示了示例）。将鼠标悬停在工具栏图标或菜单项上，Impress 会显示一个带有简短帮助信息的工具提示窗口。

你不需要进行任何设置即可开始使用 Impress。然而，如果你需要配置 Impress 的某些方面，可以通过 工具→选项 和 工具→配置 菜单进行。特别是，工具→选项 窗口中的演示文稿类别（图 3-3）包含 Impress 的选项。你应浏览每个演示文稿选项，以查看可以从此窗口配置的内容。

图 3-3：通过演示文稿类别中的选项设置 Impress。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_292_1.png)

## 使用 Impress

启动 Impress 时，AutoPilot 会提示你所需演示文稿的类型。如果 Impress 已在运行，选择 文件→新建→演示文稿 时会出现 AutoPilot。如果你想要空白演示文稿，只需在 AutoPilot 的第一步单击“创建”。Impress 会显示修改幻灯片对话框（见图 3-4），其中包含幻灯片版式的图库。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_293_0.png)

图 3-4：从此对话框中选择幻灯片版式并单击“确定”。

你可以从对话框中（参见图 3-4）选择幻灯片版式并单击“确定”。Impress 然后显示一张带有所选版式的空白幻灯片。

通常幻灯片版式可能包含标题区域和一些文字项目符号。你可以单击并向这些区域中的每一个添加文字。要插入任何图形图像，请选择 插入→图形 并选择要插入的图形文件。你可以使用 Impress 窗口左侧垂直工具栏中的绘图工具直接在幻灯片上绘图。要了解哪个工具做什么，将鼠标移至任何图标上，工具提示会给出提示。

完成对一张幻灯片的工作后，你可以通过选择 插入→幻灯片 来插入另一张幻灯片。Impress 显示插入幻灯片对话框（类似于图 3-4 所示的修改幻灯片对话框），在其中你可以为下一张幻灯片选择版式。

要保存演示文稿，请从菜单中选择 文件→保存。对于新文档，你必须提供文件名并选择保存文件的目录。



简而言之，这就是在 PowerPoint 中创建演示文稿的方式。在以下各节中，我提供了使用 Impress 执行以下类型任务的快速参考提示：

- 准备演示文稿
- 添加图形和特效
- 演示演示文稿

## 准备演示文稿

通常，你从一个具有特定版式的空白幻灯片开始。例如，幻灯片有一个标题区域和一个用于列出你想通过该幻灯片传达的要点的项目符号列表。你可以单击标题区域，输入标题，然后单击项目符号文本区域开始输入文本。然后添加另一张幻灯片并继续此过程，直到完成演示文稿。

如果你要展示的信息已存在于 Writer 文档中（参见本小书第 1 章），你可以使用该 Writer 文档的大纲来开始演示。Writer 文档必须遵循一条规则——它必须为文档中的主要部分使用标题样式 Heading 1、Heading 2 等。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_294_0.png)

要从使用标题样式的 Writer 文档大纲创建演示文稿，请在 Writer 中打开文档并从 Writer 菜单中选择 发送→大纲到演示文稿。你应该会看到一个 Impress 窗口打开，其中包含一个新演示文稿，其幻灯片基于 Writer 文档中的标题。每个 Heading 1 样式都成为一张新幻灯片，而 Heading 2 和 Heading 3 样式则作为幻灯片中的项目符号文本出现。

在处理完一组幻灯片后，你可能想要重新排列幻灯片。要按不同顺序重新排列幻灯片，请选择 视图→主视图→幻灯片视图。Impress 在工作区中以矩形网格排列显示一组迷你尺寸的幻灯片。可以将此视为幻灯片排序视图，因为你可以在此视图中移动幻灯片并对它们进行排序。

在图 3-5 所示的幻灯片排序视图中，你可以拖放幻灯片到不同位置并按你想要的顺序重新排列它们。要在此视图中删除幻灯片，请单击幻灯片以选择它并按 Delete（或选择 编辑→删除）。在提示确认删除时，如果你真的想删除幻灯片，可以单击 是。双击幻灯片即可返回通常的单幻灯片视图。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_295_0.png)

Figure 3-5:
在 Impress 的此幻灯片排序视图中排列幻灯片。

在处理演示文稿时，请记住以下概念：

- **母版幻灯片：**你可以将*母版幻灯片*视为每张幻灯片的背景。如果你在母版幻灯片上放置文本或其他字段（例如日期和页码），这些元素将出现在演示文稿的每张幻灯片上。
- **图层：**你可以在母版幻灯片以及每张单独的幻灯片中都有图层。可以将图层视为放置一些相关文本和图形的透明纸张。幻灯片随后由这些相互叠加的图层组成。你可以使用图层对相关信息进行分组。例如，如果你正在绘制房屋平面图，可以将所有尺寸放在单独的图层上。好处是你可以轻松地隐藏或显示图层。只需单击导航栏上从左数第三个图标（参见图 3-2）或选择 视图→图层。
- **母版备注和母版讲义：**这个想法与母版幻灯片相同。你可以在母版备注或母版讲义上定义一些字段和文本；这些成为你的备注和讲义的背景的一部分。*备注*指的是你在每张幻灯片底部添加的任何解释性文本。*讲义*是幻灯片的打印件，可以在简报会上分发给观众。通常，一页上可以容纳多张幻灯片。

好吧，我可以继续说下去，但你最好通过直接开始使用 Impress 来学习。如果你需要在 Impress 中准备演示文稿时需要一些帮助，请参阅表 3-1，了解如何执行一些常见任务的信息。

表 3-1 常见演示文稿准备任务

| 执行此操作 | 按以下步骤操作 |
|---|---|
| 创建空白演示文稿 | 选择 文件→新建→演示文稿，并在出现的 AutoPilot 窗口中单击 创建。从 插入幻灯片 对话框中选择幻灯片版式。 |
| 从 Writer 文档创建演示文稿 | 从 Writer 菜单中选择 发送→大纲到演示文稿。一个新演示文稿将在 Impress 窗口中出现，其中包含 Writer 文档的大纲，由标题样式 Heading 1、Heading 2 等构建。 |
| 打开现有演示文稿 | 选择 文件→打开，然后选择要打开的文件。如果你处于 AutoPilot 窗口中，请单击 打开现有演示文稿，选择 <Other positions>，然后单击 创建。Impress 然后显示 打开 对话框，你可以从中选择要打开的文件。 |
| 为演示文稿分配标题 | 选择 文件→属性。单击结果对话框中的 说明 选项卡，并在 标题 字段中输入。此标题出现在 Impress 窗口的标题栏中。 |
| 插入幻灯片 | 选择 插入→幻灯片，并从 插入幻灯片 对话框中选择幻灯片版式。 |
| 复制当前幻灯片 | 选择 插入→复制幻灯片。 |
| 删除幻灯片 | 右键单击幻灯片选项卡并从弹出菜单中选择 删除幻灯片。被要求确认时单击 是。 |
| 更改现有幻灯片的版式 | 选择 格式→修改版式。从 插入幻灯片 对话框中选择一个版式并单击 确定。 |
| 创建模板 | 准备一个包含你想要的所有样式的幻灯片的演示文稿。选择 文件→另存为 并将文件保存为 OpenOffice.org 演示文稿模板。 |
| 切换到幻灯片视图 | 单击幻灯片底部导航栏上的最左侧图标或选择 视图→幻灯片。 |
| 编辑母版幻灯片 | 单击幻灯片底部导航栏上从左数第二个图标（或选择 视图→母版→幻灯片）。编辑母版幻灯片（用作所有幻灯片的背景）。 |
| 编辑母版备注 | 选择 视图→母版→备注。编辑你希望用作所有备注背景的母版备注页。你可以插入诸如页码和日期之类的字段。 |
| 为幻灯片添加备注 | 选择 视图→主视图→备注视图。单击幻灯片的备注区域并输入备注。 |

表 3-1（续）

| 执行此操作 | 按以下步骤操作 |
|---|---|
| 在大纲视图中工作 | 选择 视图→主视图→大纲视图。 |
| 以迷你格式查看幻灯片 | 选择 视图→主视图→幻灯片视图。你可以在此视图中重新排列幻灯片的顺序。 |
| 编辑图层 | 单击幻灯片底部导航栏上从左数第三个图标（或选择 视图→图层）。单击图层选项卡以编辑该图层。 |
| 插入图层 | 在编辑图层时，右键单击图层选项卡并从弹出菜单中选择 插入图层。 |
| 隐藏或显示图层 | 在编辑图层时，右键单击图层选项卡并从弹出菜单中选择 修改图层。取消选择 可见 属性并单击 确定。在 可见 属性上打勾会使图层再次可见。 |
| 更改缩放级别 | 右键单击状态栏上的缩放级别并从弹出菜单中选择新的缩放级别。 |
| 以彩色、灰度或黑白查看幻灯片 | 选择 视图→显示质量，然后选择你想要彩色、灰度还是黑白。 |

## 添加图形和特效

为了让你的演示文稿更生动，你可能想要向幻灯片中添加图形、图表和其他特效。使用 Impress，你可以做几乎你能想到的任何事情——你唯一需要决定的是你的演示文稿需要多少铃铛和口哨。这是你的选择，但我建议谨慎使用这些功能，以免分散演示文稿主要信息的注意力。

如果你想在幻灯片中添加一些简单的绘图，你可以从 Impress 窗口左侧垂直工具栏上的绘图工具中选择并开始在幻灯片上绘图。要将图像插入幻灯片，请选择 插入→图形，然后选择要插入的图像文件。

你还可以插入图表以图形方式描绘数据。你首先插入一个带有虚拟数据的图表，然后编辑数据以及图表的其他功能。要添加图表并编辑数据，请按照以下步骤操作：

1. 选择 插入→图表。

一个带有默认图表类型和虚拟数据的图表出现。



- 2. 通过拖动图表边框周围的控点调整图表大小；然后右键单击图表，从出现的弹出菜单中选择“图表数据”（图 3-6）。
- 3. 编辑行和列标签，并输入希望图表显示的数据。
- 4. 编辑完成后，单击绿色复选标记（位于数据输入区域右侧）以应用更改并关闭“图表数据”窗口。
- 5. 要更改图表类型，请右键单击图表，从出现的弹出菜单中选择“图表类型”；选择新的类型并单击“确定”。

一个迷你电子表格会显示占位图表数据。

你可以做的远不止向幻灯片演示文稿中添加图形和图表。你可以在幻灯片中插入电子表格和 Writer 文档，添加沿曲线运行的文本，并为幻灯片中的各种元素添加特殊效果。表 3-2 总结了一些常见的图形和特效任务，包括如何执行每个任务的信息。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_298_0.png)

Figure 3-6:
右键单击图表以修改数据和图表类型。

### 表 3-2 常见图形和特效任务

| 执行此操作 | 按以下步骤操作 |
|---|---|
| 在幻灯片上绘图 | 从 Impress 窗口左侧的垂直工具栏中选择绘图工具，并使用鼠标在幻灯片上绘图。你还可以添加文本和文本标注（一个带有指向你试图解释的内容的线的文本框）。 |
| 应用文本效果 | 选择“格式：FontWork”。选择文本并使用 FontWork 工具为文本应用特殊效果，例如将文本沿曲线放置并显示阴影。 |
| 将文本或图形转换为 3D | 右键单击文本或图形并选择“转换→转换为 3D”。对于文本，请确保单击文本框，而不是文本本身。 |
| 从文件插入图形 | 选择“插入→图形”，然后选择要插入的图形文件。 |
| 添加图表 | 选择“插入→图表”以插入占位图表。右键单击图表并从弹出菜单中选择“图表数据”。占位数据会出现在迷你电子表格窗口中。编辑数据。要更改图表类型，请右键单击图表并选择“图表类型”。然后从结果对话框中选择一种图表类型。 |
| 向幻灯片添加图形 | 选择“插入→图形”以选择要插入的图形文件。 |
| 插入在 Draw 中准备的绘图 | 选择“插入→OLE 对象”。在结果对话框中，选择“从文件创建→搜索”。从“打开”对话框中选择绘图文件并单击“打开”。单击“确定”以从文件中插入绘图。稍后双击绘图进行编辑。 |
| 插入公式 | 选择“插入→对象→公式”。OpenOffice.org Math 应用程序出现。使用公式选择和准备窗口创建公式并调整字体大小。在构建公式时，它会出现在幻灯片中。单击幻灯片中的其他位置即可返回 Impress。双击公式再次编辑它。 |
| 对幻灯片中的对象应用效果 | 选择“幻灯片放映→效果”以打开“效果”窗口。选择“视图→预览”，以便在尝试时在小预览窗口中看到效果。选择要应用效果的对象，从“效果”窗口中选择效果，然后单击绿色复选标记。在预览窗口中观察效果。满意时停止。如需，可将效果应用于更多对象。 |
| 控制幻灯片切换方式 | 选择“幻灯片放映→幻灯片切换”以打开“幻灯片切换”窗口。选择“视图→预览”，以便在应用每个切换时在小预览窗口中看到切换效果。从“幻灯片切换”窗口中选择切换效果，然后单击绿色复选标记。在预览窗口中观察效果。满意时停止。按需将切换效果应用于其他幻灯片。 |

## 交付演示文稿

在准备好一套精彩的幻灯片后，你需要将其交付给观众。这通常涉及诸如准备演讲者备注、运行幻灯片放映、将演示文稿转换为 HTML 以通过网络交付以及打印讲义等任务。表 3-3 总结了一些常见的演示文稿交付任务。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_300_0.png)

你还可以直接将 Impress 演示文稿打印到 Adobe 便携式文档格式（PDF）文件。这使得电子共享演示文稿变得容易，因为任何人都可以轻松地使用免费的 Adobe Reader 查看和打印 PDF 文件（可在 www.adobe.com/products/acrobat/readstep2.html 获取）。

### 表 3-3 常见演示文稿交付任务

| 执行此操作 | 按以下步骤操作 |
|---|---|
| 编辑主讲义 | 选择“视图→母版→讲义”。编辑用作所有讲义背景的主讲义。 |
| 准备讲义 | 选择“视图→母版视图→讲义视图”。该视图显示讲义页，每页包含若干幻灯片。要更改版式，请右键单击讲义并从弹出菜单中选择“幻灯片→修改幻灯片”。选择你想要的版式（讲义每页的幻灯片数量）。 |
| 打印讲义 | 选择“视图→母版视图→讲义视图”。选择“文件→打印”。 |
| 运行幻灯片放映 | 单击幻灯片放映图标（垂直工具栏上的最后一个）或选择“幻灯片放映→幻灯片放映”或按 Ctrl+F2。单击以浏览幻灯片。按 Esc 停止幻灯片放映，或在最后一张幻灯片单击以结束放映。 |
| 创建自定义幻灯片放映 | 选择“幻灯片放映→自定义幻灯片放映”。在“自定义幻灯片放映”窗口中单击“新建”。分配一个名称，然后按你希望它们出现的顺序选择幻灯片放映中的幻灯片。拖动幻灯片上下以更改该顺序。单击“确定”，然后单击“关闭”。 |
| 运行自定义幻灯片放映 | 选择“幻灯片放映→自定义幻灯片放映”。选择自定义幻灯片放映（你应该会看到创建幻灯片放映时使用的名称）。打开“使用自定义幻灯片放映”旁边的复选框，然后单击“开始”。 |
| 将幻灯片打印到 PDF 文件 | 选择“文件→打印”。在“打印”对话框中，单击打印机列表并从下拉列表中选择 PDF 转换器。单击“确定”。 |
| 创建演示文稿的 HTML 版本 | 选择“文件→导出”。在“导出”对话框中，输入文件名并选择“网页”作为格式。单击“保存”。完成 HTML 导出步骤，选择你想要的文件类型（例如，有或无框架的 HTML）以及用于表示每张幻灯片的图像的格式（JPEG 或 GIF）。 |

### 第 4 章：使用 OpenOffice.org Draw 绘图

### 本章内容

- ✓ 了解 OpenOffice.org Draw
- ✓ 开始使用 Draw
- ✓ 使用 Draw

有时你需要图像、图表和插图来说明观点。无论是快速草图还是复杂图表，OpenOffice.org Draw（简称 Draw）都能为你提供准备绘图所需的工具。

Draw 是 OpenOffice.org 办公套件中的一个独立绘图程序，但你也可以从其他 OpenOffice.org 应用程序（如 Writer 和 Impress）访问许多 Draw 的绘图工具。当你使用 Draw 准备绘图时，会将绘图保存到文件中。稍后你可以将绘图作为 Draw 对象插入到其他 OpenOffice.org 文档中，例如 Writer 文档或 Impress 演示文稿。将 Draw 对象插入 Writer 或 Impress 文档的好处是，你可以随时双击并直接编辑绘图，即使它仍在 Writer 或 Impress 文档中。

在本章中，我向你介绍 Draw 应用程序。我提供概述，然后提供快速参考，帮助你在 Draw 中执行一些常见的绘图任务。

### 了解 OpenOffice.org Draw

你会发现 Draw 可以完成典型绘图程序能完成的所有常规操作。为了让你了解 Draw 的功能，以下是一些你可以用 Draw 完成的事情：

- ♦ 使用一系列标准绘图工具，如多边形、圆形和贝塞尔曲线。
- ♦ 使用智能连接线绘制流程图、组织结构图和网络图。



- 将矢量图形（线条、几何形状、文本）与光栅图像（JPEG、GIF 和其他位图格式）混合。
- 从其他 OpenOffice.org 应用程序（如 Writer 和 Impress）访问 Draw 工具。
- 使用 FontWork 为文本应用特殊效果（如沿曲线排列文本并添加阴影）。
- 在绘图中插入其他 OpenOffice.org 对象（如电子表格和幻灯片）。
- 绘制 3D 形状并相交 3D 对象。
- 将文本和曲线转换为 3D 对象。
- 裁剪图像。
- 控制图像颜色的许多方面，如亮度、对比度和透明度。
- 使用图层分隔绘图的各个部分，以便每个部分可以单独编辑或查看。
- 将绘图导出为网页（HTML）或其他图像文件格式，如 EPS、JPEG 和 GIF。

## 开始使用 Draw

学习使用 Draw 的最佳方法是直接开始使用它。要启动 Draw，请选择 主菜单→Office→OpenOffice.org Draw。Draw 窗口出现，带有空白绘图区域。然后你可以从出现在 Draw 窗口左侧的垂直工具栏中选择工具并开始绘图。图 4-1 显示了 Draw 窗口，其中包含一个不典型的绘图，包括文本、3D 形状和图像。

在开始使用 Draw 之前，花点时间研究 Draw 窗口和各种工具和图标栏（如图 4-1 所示）。请注意，Draw 窗口具有以下主要部分：

- 菜单栏：提供标准下拉菜单（如文件、编辑和帮助），用于执行 Draw 可以完成的所有任务。
- 功能栏：显示当前打开文件的完整路径名或 URL，并提供执行诸如打开、保存和打印文档等任务的按钮。你还可以单击功能栏上的图标打开样式（图形样式列表）、导航器（绘图项目列表）和画廊（预定义图形对象的集合，如 3D 形状、背景和项目符号）。

Figure 4-1:
使用 Draw 中的工具栏中的工具。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_304_0.png)

- 对象栏：显示适用于当前所选对象类型（如文本、图像或矢量图形）的通用格式和样式属性，包括颜色。
- 工具栏：位于窗口左侧，工具栏提供可单击的图标以选择用于在绘图中绘制或编辑对象的工具。

Book III
Chapter 4
使用 OpenOffice.org 绘图
Draw

- **标尺：** 显示垂直和水平页面尺寸。
- **导航栏：** 位于幻灯片底部，导航栏使你能够更改视图并选择要处理的绘图。
- **状态栏：** 显示有关当前绘图的信息，如指针位置和当前选中的对象。你还可以单击状态栏中的元素并更改设置，包括查看绘图的缩放系数。

除这些工具和图标栏外，你还可以打开另外两个工具栏：

- 选择 查看→工具栏→选项栏 以打开出现在导航栏下方的选项栏。选项栏显示图标，通过这些图标执行任务，如编辑曲线、显示网格线以及指示单击文本和其他对象时发生的情况。
- 选择 查看→工具栏→颜色栏 以打开出现在窗口底部、状态栏正上方的颜色栏。颜色栏显示可供挑选并用于对象的颜色。你可以通过单击颜色栏左上角的向下指向箭头来显示或隐藏颜色栏。

与其他 OpenOffice.org 应用程序一样，Draw 窗口的最大部分是工作区，你在此处理当前绘图，并在应用程序中花费大部分时间。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_305_0.png)

如果你不知道某个图标或菜单的作用，将鼠标悬停在该项目上，Draw 会显示一个带有简要帮助消息的小工具提示窗口。

你不需要设置任何东西即可开始使用 Draw。但是，如果你需要配置 Draw 中的任何内容，可以通过 工具→选项 和 工具→配置 菜单进行。特别是，工具→选项 窗口中的 绘图 类别包含 Draw 的选项。浏览每个演示选项，查看可以从此窗口配置的内容。

## 使用 Draw

在大多数情况下，你将使用位于 Draw 窗口左侧的垂直工具栏上的绘图工具（参见图 4-1）。对于某些任务，你将使用菜单和通过选择 查看→工具栏→颜色栏 使其可见的颜色工具栏。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_306_0.png)

使用垂直工具栏中的工具时，你必须学会 *长按*。不用担心，这没什么复杂。你只需单击一个图标并按住鼠标按钮，直到出现额外的工具栏。这就是长按。尝试后看到它实际运行，你会立刻掌握它。

长按适用于任何带有小右指向箭头的图标。图标显示当前选中的工具，但长按会展开所有 *弹出工具栏* 上的图标——一个看起来在屏幕上滑出的工具栏，显示你可以做的其他选择。要使用弹出工具栏，请按以下步骤操作：

1. **长按（单击并按住鼠标）任何带有右指向箭头的图标，直到工具栏弹出（图 4-2）。**

工具栏显示可用工具的图标（如果工具不适用于当前选中的对象，则为灰色）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_306_1.png)

Figure 4-2:
典型的
弹出
工具栏。

2. **要将工具放在 *可撕下菜单*（在 Draw 窗口中浮动的小窗口）中，请拖动弹出工具栏的顶部并将其撕下。**

工具现在保留在可撕下菜单中（图 4-3），标签为你在工具栏上单击的工具名称。你可以单击并使用任何想要的工具。当不再需要可撕下菜单时，单击 X 关闭菜单。

Figure 4-3:
一个可撕下菜单。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_307_0.png)

3. **要直接从弹出工具栏使用工具，请单击想要的工具。**

弹出工具栏消失，光标形状发生变化。你可以使用所选工具绘图。

4. **要重复使用同一工具，请在垂直工具栏上正常单击该图标。**

光标形状发生变化，你可以使用该工具绘图。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_307_1.png)

当你学会如何长按和撕下弹出工具栏时，你可能会想如何记住工具栏上每个图标的作用。我的建议是不要尝试。只需将鼠标悬停并阅读工具提示即可。这就是工具提示的作用！

尝试使用工具准备绘图。查阅表 3-1，了解在 Draw 中执行一些常见绘图任务的提示。

表 3-1 常见绘图任务

| 执行此操作 | 按以下步骤操作 |
|---|---|
| 创建新绘图 | 选择 文件→新建→绘图。 |
| 打开现有绘图文件 | 选择 文件→打开，然后从打开对话框中选择要打开的文件。 |
| 应用样式 | 按 F11 打开样式窗口，如果尚未打开。选择要应用样式的对象。在样式中双击样式。 |
| 向绘图添加文本和图形对象 | 从 Draw 窗口左侧的垂直工具栏中选择绘图工具的图标。使用鼠标并使用所选工具绘图。将鼠标悬停并使用工具提示来了解不同工具的作用。 |
| 更改对象的属性 | 右键单击对象并选择要更改的属性，如线条、区域、位置和大小。 |
| 复制对象 | 选择对象并选择 编辑→复制。在复制对话框中，为放置位置和副本数量做出选择，然后单击确定。 |
| 选择多个对象 | 按住 Shift 键单击对象。 |
| 分组对象 | 选择要分组的对象。右键单击选择，然后从弹出菜单中选择分组。 |
| 取消分组对象 | 右键单击分组并从弹出菜单中选择取消分组。 |
| 旋转对象 | 选择一个或多个对象。单击工具栏上的效果图标（使用工具提示找到此图标）并选择旋转图标。抓住出现在对象上的一个手柄并使用它旋转对象。 |
| 对齐对象 | 选择对象。右键单击选择并选择对齐方式和对齐类型，如左、上、中等。 |
| 均匀分布对象 | 选择三个或更多对象。右键单击选择并选择分布。使用分布对话框选择要在屏幕上如何分布对象。 |
| 安排对象的顺序 | 选择对象。右键单击选择并选择排列和放置顺序，如置于最前、置于后等。 |
| 向绘图添加 3D 对象 | 从工具栏中选择 3D 对象（垂直工具栏中从顶部起的最后一个图标）。 |
| 将文本转换为 3D | 单击选择文本框。然后右键单击该框并选择 转换→转换为 3D。单击并旋转 3D 文本以满足你的喜好。 |
| 为文本应用特殊效果 | 选择 格式→FontWork。选择要应用特殊效果的文本框。从 FontWork 窗口中选择想要的效果。（例如，你可以将文本沿曲线放置并为文本显示阴影。） |
| 为文本添加背景 | 右键单击文本框并选择区域。从结果的区域对话框中选择文本背景选项。 |
| 为文本应用字体效果 | 右键单击文本框并从弹出菜单中选择字符。在结果的字符对话框中单击字体效果选项卡。从字体效果选项卡中选择效果（如浮雕或雕刻字符）。 |
| 裁剪图像 | 选择图像并单击裁剪图标（对象工具栏上最右边的图标）。从裁剪对话框中选择想要的选项并单击确定。 |




## 表 3-1（续）

| 执行此操作 | 操作步骤 |
|---|---|
| 修改图像的特性 | 单击图像并使用对象栏上的选项调整颜色、对比度、亮度和透明度。您可以更改图像颜色中的红色、绿色和蓝色分量，并将屏幕上对象的透明度从 0%（不透明）调整到 100%（完全透明）。 |
| 将两个 3D 对象合并为单个 3D 对象 | 将两个 3D 对象靠近彼此。选择应显示在前面的 3D 对象并按 Ctrl+X 将其剪切。单击第二个对象并按 F3。现在按 Ctrl+V 将前面对象粘贴到第二个对象上。对象现在应显示为已合并。单击并单独调整对象。按 Ctrl+F3 结束合并对象的过程。 |
| 将绘图导出为图像文件 | 选择 File→Export。在生成的导出对话框中，输入文件名并选择所需格式。支持的格式包括 BMP（Windows 位图）、EPS（封装式 PostScript）、GIF、JPEG、PNG（便携式网络图形）、PPM（便携式像素图）、TIFF 等。 |

## 第四卷

## 网络

### 第五波

作者 Rich Tennant

![](img/a7eec43a54473e95dc5ea333fecf1bd7_310_0.png)

"我想你可以说这是我们网络的核心。"

## 目录概览

- 第 1 章：连接到互联网 ................................................... 285
- 第 2 章：设置局域网 ........................................... 309
- 第 3 章：添加无线以太网局域网 ........................................... 321
- 第 4 章：管理网络 ....................................................... 333

### 第 1 章：连接到互联网

### 本章内容

- ✓ 了解互联网
- ✓ 决定如何连接到互联网
- ✓ 使用 DSL 连接到互联网
- ✓ 使用有线调制解调器连接到互联网
- ✓ 设置拨号 PPP 链接

互联网正迅速成为我们大多数人的生命线。似乎我们一天也离不开它（我知道如果没有它我写不了这本书）。有时我会想我们以前没有互联网是怎么度过的——可以肯定的是，你想将你的 Red Hat Linux 系统连接到互联网。本章中，我将向你展示几种不同的连接方式——取决于你拥有的是 DSL、有线调制解调器还是拨号网络连接。

连接到互联网的两个选项——DSL 和有线调制解调器——涉及将专用调制解调器连接到 Red Hat Linux 系统上的以太网卡。在这些情况下，你必须在 Red Hat Linux 系统上设置以太网网络。（我在本迷你书的第 2 章中解释了这一点。）在本章中，我将详细介绍如何设置 DSL 或有线调制解调器连接。

我还将向你展示另一个选项——拨号网络——它涉及从你的 Red Hat Linux 系统拨号到互联网服务提供商（ISP）。

### 了解互联网

你如何看待互联网取决于你的视角。我们这样的普通人会根据我们使用的服务来看待互联网。例如，作为用户，我们认为互联网是一种信息交换媒介——具有以下功能：

- ♦ **电子邮件：** 使用 `mom@home.net` 等地址向互联网上的任何其他用户发送电子邮件。
- **网页：** 从互联网上数百万台服务器下载和查看文档。
- **新闻组：** 阅读新闻组并向名称如 `comp.os.linux.networking` 或 `comp.os.linux.setup` 的新闻组发布新闻。
- **信息共享：** 下载软件、音乐文件、视频等。反过来，你也可以提供文件供其他系统上的用户下载。
- **远程访问：** 登录互联网上的另一台计算机，前提是你有权访问该远程计算机。

我们中的技术人员会说互联网是一个全球性的 *网络的网络*。术语 *internet*（不带大写）是 *internetworking* 的简写——网络的互联。互联网协议（IP）的设计理念是连接多个独立的网络。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_313_0.png)

从物理连接来看，互联网类似于高速公路和道路网络。这种相似性促使大众媒体将互联网称为“信息高速公路”。正如高速公路和道路网络包括一些州际高速公路、许多州道和更多的居民街道一样，互联网也有一些非常高容量的网络（例如，10 Gbps 的骨干网可处理每秒 100 亿位）和大量低容量网络，范围从 56 Kbps 拨号连接到 45 Mbps T3 链路（*Kbps* 为每秒千位，*Mbps* 为每秒百万位）。高容量网络是互联网的骨干。

从管理角度来看，互联网不是由单一组织运行的，也不是由任何中央计算机管理。你可以将物理互联网视为由数千个合作组织共同管理的“网络的网络”。是的，由 *数千个* 组织管理的网络集合——听起来令人惊讶，但它确实有效！

### 决定如何连接到互联网

所以你想连接到互联网，但不知道怎么做？让我数一下方法。如今，你有三种流行的将家庭和小型办公室连接到互联网的选项（当然，庞大的公司和政府有许多其他连接方式）：

- **数字用户线路 (DSL)：** 这是你的本地电话公司以及其他电信公司可能提供的服务。DSL 提供了一种通过普通电话线发送高速数字数据的方式。通常，DSL 的数据传输速率在 128 Kbps 到 1.5 Mbps 之间。你可以以比从你的 PC 向互联网发送数据（*上传*）高得多的速率从互联网下载。DSL 的一个注意事项是，你的家庭必须距离本地中心局（电话公司设施，你的电话线最终到达的地方）12,000 到 15,000 英尺。距离限制因提供商而异。在美国，你可以在 www.dslreports.com/distance 查看许多提供商的距离限制。
- **有线调制解调器：** 如果你所在地区的有线电视公司提供有线互联网接入，你可以使用该服务将你的 Red Hat Linux 系统连接到互联网。通常，有线调制解调器提供的数据传输速率高于 DSL——价格相同。通过有线调制解调器从互联网下载数据比从你的 PC 向互联网发送数据快得多。你可以预期常规下载速度为 1.5 Mbps，上传速度约为 128 Kbps，但有时你可能获得更高的速度。
- **拨号网络：** 在 DSL 和有线调制解调器出现之前，我们大多数人都在使用它。你将 PC 连接到连接到电话线的调制解调器。然后拨号 ISP 以连接到互联网。这就是我们称之为 *拨号网络* 的原因——通过拨号调制解调器在你的 Red Hat Linux PC 与另一个网络（互联网）之间建立网络连接。在这种情况下，最大数据传输速率为 56 Kbps。

DSL 和有线调制解调器服务将你连接到互联网，同时也充当你的互联网服务提供商（ISP）；除了速度提升外，你支付的是 IP 地址和你的电子邮件账户。如果你使用拨号调制解调器连接到互联网，首先你必须连接到电话线（为此你向电话公司付费），然后选择并支付单独的 ISP——它为你提供拨号电话号码以及所有其他必要的服务（例如 IP 地址和电子邮件账户）。

### 表 1-1 拨号、DSL 和有线比较

| 功能 | 拨号 | DSL | 有线 |
|---|---|---|---|
| 设备 | 调制解调器 | DSL 调制解调器，以太网卡 | 有线调制解调器，以太网卡 |
| 还需要 | 电话服务和互联网服务提供商 (ISP) | 电话服务以及距离中心局 12,000 至 15,000 英尺的位置 | 有线电视连接 |
| 连接类型 | 拨号连接 | 始终在线，专用 | 始终在线，共享 |




表 1-1（续）

| 功能 | 拨号 | DSL | 电缆 |
|---|---|---|---|
| 典型速度 | 最高 56 Kbps | 下载 640 Kbps，上传 128 Kbps（更高速度需额外付费） | 下载 1.5 Mbps，上传 128 Kbps |
| 一次性费用（估算） | 无 | 安装 = $100-200；设备 = $200-300（可租赁且可能需要激活费用） | 安装 = $100-200；设备 = $60-100（可租赁） |
| 典型月费（2003 年） | 电话费 = $20/月；ISP 费用 = $15-30/月 | $50/月；可能需要每月调制解调器租赁费 | $50/月；可能需要每月调制解调器租赁费 |

注：费用因地区和提供商而异。所示费用为美国大都市区的典型费用。

## 使用 DSL 连接

DSL 是 Digital Subscriber Line 的缩写。DSL 使用您现有的电话线路，除了正常的模拟语音信号外，还发送数字数据（analog 指连续变化，而 digital 数据由 1s 和 0s 表示）。电话线路从您的家庭延伸到中央办公室，在那里线路连接到电话公司的网络——顺便说一下，从您家到中央办公室的连接称为本地环路。当您[content]
表 1-1（续）

| 功能 | 拨号 | DSL | 电缆 |
|---|---|---|---|
| 典型速度 | 最高 56 Kbps | 下载 640 Kbps，上传 128 Kbps（更高速度需额外付费） | 下载 1.5 Mbps，上传 128 Kbps |
| 一次性费用（估算） | 无 | 安装 = $100-200；设备 = $200-300（可租赁且可能需要激活费用） | 安装 = $100-200；设备 = $60-100（可租赁） |
| 典型月费（2003 年） | 电话费 = $20/月；ISP 费用 = $15-30/月 | $50/月；可能需要每月调制解调器租赁费 | $50/月；可能需要每月调制解调器租赁费 |

注：费用因地区和提供商而异。所示费用为美国大都市区的典型费用。

## 使用 DSL 连接

DSL 是 Digital Subscriber Line 的缩写。DSL 使用您现有的电话线路，除了正常的模拟语音信号外，还发送数字数据（analog 指连续变化，而 digital 数据由 1s 和 0s 表示）。电话线路从您的家庭延伸到中央办公室，在那里线路连接到电话公司的网络——顺便说一下，从您家到中央办公室的连接称为本地环路。当您订阅 DSL 服务时，电话公司必须将您的电话线路连接到中央办公室的某些专用设备。该设备可以分离数字数据和语音。从那时起，您的电话线路可以承载数字数据，然后可直接发送到中央办公室的 Internet 连接。

## DSL 如何工作

一个名为 DSL 调制解调器的专用盒负责通过您的电话线路将数字数据从您的 PC 发送到电话公司的中央办公室。您的 PC 可以使用与正常电话通话相同的电话线路连接到 Internet——即使线路正在用于 DSL，您也可以进行语音通话。图 1-1 显示了典型的 DSL 到 Internet 连接。

您的 PC 通过以太网连接与 DSL 调制解调器通信，这意味着您需要在 Red Hat Linux 系统中安装一个以太网卡。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_316_0.png)

图 1-1：
DSL 通过普通电话线路提供高速 Internet 连接。

您的 PC 通过以太网连接将数字数据发送到 DSL 调制解调器。DSL 调制解调器以与模拟语音信号不同的频率发送数字数据。语音信号只占用电话线路可承载的所有频率中的一小部分。DSL 使用较高的频率传输数字数据，因此语音和数据可以同时在同一电话线路上传输。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_316_1.png)

您家与中央办公室之间的距离——环路长度——是 DSL 性能的一个因素。不幸的是，电话线路只能在有限的距离内可靠地承载 DSL 信号——通常为三英里或更少。这意味着您只能在您家（或办公室）位于电话公司中央办公室约三英里范围内时才能获得 DSL 服务。您的电话公司可以告诉您您的位置是否可以获得 DSL。通常它有一个网站，您可以在其中输入您的电话号码并获得有关 DSL 可用性的回复。例如，对于美国地区，请尝试 www.dslavailability.com。

## DSL 字母汤——ADSL、IDSL、SDSL

我一直在使用 DSL 这个术语，好像只有一种 DSL。您可能已经想象到，事情永远不会那么简单。事实上，DSL 有三种变体，每种都有不同的功能。来看一下：

- **ADSL：** 非对称 DSL，是最常见的 DSL 形式，其下载速度（从 Internet 到您的 PC）远高于上传速度（从您的 PC 到 Internet）。ADSL 的下载速度最高可达 8 Mbps，上传速度最高可达 1 Mbps。当您的位置距离中央办公室约 2½ 英里（12,000 英尺）以内时，ADSL 工作效果最佳。ADSL 服务的价格根据您想要的下载和上传速度而定。一种流行的 ADSL 形式，称为 G.lite，专门设计用于在您用于语音通话的同一线路上工作。G.lite 的最大下载速度为 1.5 Mbps，最大上传速度为 512 Kbps。
- **IDSL：** ISDN DSL（ISDN 是一种较旧的技术，称为 *Integrated Services Digital Network*）是一种特殊的 DSL 类型，可在您的电话与中央办公室之间距离长达五英里时工作。缺点是 IDSL 仅提供最高 144 Kbps 的下行（从 Internet 到您的 PC）和上行（从您的 PC 到 Internet）速度。
- **SDSL：** 对称 DSL 提供最高 1.5 Mbps 的相等下载和上传速度。SDSL 的价格根据您想要的速度而定，速度越高费用越高。您距离电话公司中央办公室越近，连接速度越快。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_317_0.png)

DSL 速度通常由两个用斜杠分隔的数字指定，如下所示：1500/384。这些数字指的是千比特每秒的数据传输速度（即每秒千比特，缩写为 Kbps）。第一个数字是下载速度，第二个是上传速度。因此 1500/384 意味着您最多可以以 1,500 Kbps（或 1.5 Mbps）的速率从 Internet 下载，并以 384 Kbps 的速率上传到 Internet。如果您的电话线路状况不完美，您可能无法获得这些最大速率——ADSL 和 SDSL 都会根据现有的线路状况调整速度。

DSL 服务的价格取决于您选择的变体——ADSL、IDSL 或 SDSL。对于大多数家庭用户，主要选择是 ADSL（或更准确地说，ADSL 的 G.lite 形式），其传输速度评级为 1500/128。

## 典型的 DSL 设置

要为您的家庭或企业获取 DSL，您必须联系 DSL 提供商。除了您的电话公司外，还有许多其他 DSL 提供商。无论谁提供 DSL 服务，都必须在您的中央办公室进行一些工作——即您的电话线路连接到电话网络其余部分的地点。该工作涉及将您的电话线路连接到可在您家或办公室与 DSL 调制解调器配合工作的设备。中央办公室设备和您所在位置的 DSL 调制解调器然后可以执行发送和接收电话线路上数字数据所需的任何魔术。

由于需要在中央办公室设置线路，因此在您下订单后需要一些时间才能使线路准备好使用 DSL。

您要做的第一步是查看提供服务的 DSL 提供商，并查看您是否真的可以获得该服务。由于 DSL 只能在您所在位置与中央办公室之间的一定距离内工作——通常小于 2.5 英里——您必须检查自己是否在该距离限制范围内。联系您的电话公司进行验证。您可能可以在网上检查这一点。尝试在 Google（www.google.com）中输入 DSL availability 和您当地电话公司的名称。您可能会得到一个网站，您可以在其中输入您的电话号码并了解该号码是否可用 DSL。

如果 DSL 可用，您可以查看服务类型——ADSL 与 SDSL——以及价格。价格取决于您想要的下载和上传速度。有时电话公司提供简单的住宅 DSL（基本上是 ADSL 的 G.lite 形式），速度评级为 1500/128——意味着您可以以 1,500 Kbps 的速度下载，以 128 Kbps 的速度上传。当然，这些是最大值，您的实际体验可能有所不同。

在选择 DSL 服务类型和提供商后，您可以下订单并让提供商在您家或办公室安装必要的设备。图 1-2 显示了典型住宅 DSL 服务的示例连接图。

图 1-2：
您可以将 PC 的以太网卡直接连接到 DSL 调制解调器。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_318_0.png)

以下是图 1-2 中需要注意的一些要点：

- 将您的 DSL 调制解调器的数据连接连接到墙板上的电话插孔。
- 将 DSL 调制解调器的以太网连接连接到您 PC 上的以太网卡。
- 当您在同一电话线路上连接其他电话或传真机时，在墙板和每个这些设备之间安装一个 *microfilter*。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_319_0.png)

由于同一电话线路承载语音信号和 DSL 数据，您需要微滤波器来保护 DSL 数据免受可能的干扰。您可以在电子商店或从 DSL 提供商处购买它们。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_319_1.png)

当您使用 DSL 将 Red Hat Linux PC 连接到 Internet 时，连接始终处于打开状态——并且外部人员入侵 PC 的可能性更大。您应确保 Red Hat Linux 防火墙设置设置为高安全性。要配置防火墙设置，请从 GNOME 桌面选择 主菜单→系统设置→安全级别。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_319_2.png)

保护您的 Red Hat Linux 系统免受入侵者侵害的另一种方法，并且作为附加好处，可以与其他 PC 在本地局域网（LAN）中共享高速连接。为此，您需要一个可以执行网络地址转换（NAT）的路由器。这样的 *NAT router* 将内部 LAN 的多个私有 Internet 协议（IP）地址转换为单个公共 IP 地址，从而使所有内部 LAN PC 都可以访问 Internet。

如果您还想设置局域网，则需要一个以太网集线器来将其他 PC 连接到网络。图 1-3 显示了一个典型的设置，通过 NAT 路由器和 DSL 调制解调器将 LAN 连接到 Internet。

设置如图 1-3 所示的连接时，请注意以下几点：

- 您需要一个具有两个 10BaseT 以太网端口的 NAT 路由器（10BaseT 端口看起来像一个大电话插孔，也称为 *RJ-45 jack*）。通常，一个以太网端口标记为 *Internet*（或 External 或 WAN 用于广域网工作），另一个标记为 Local 或 LAN（用于局域网）。
- 您还需要一个以太网集线器。对于小型家庭网络，您可以购买 4 或 8 端口以太网集线器。基本上，您希望集线器的端口数量与您打算连接到局域网的 PC 数量一样多。
- 使用 10BaseT 以太网电缆（这些看起来像带更大 RJ-45 插头的电话线，通常标记为 *Category 5* 或 *Cat 5* 线）将 DSL 调制解调器的以太网端口连接到 NAT 路由器的 Internet 端口。



-   使用 10BaseT 以太网电缆将 NAT 路由器的 Local 以太网端口连接到以太网集线器的其中一个端口上。
-   现在将每台 PC 连接到以太网集线器。（当然，为此你必须先在每台 PC 中安装并配置以太网卡。）

![](img/a7eec43a54473e95dc5ea333fecf1bd7_320_0.png)

你还可以购买内置 4 或 8 端口以太网集线器的 NAT 路由器。 使用这种组合的路由器-集线器，你只需一个设备即可搭建局域网并通过 DSL 调制解调器连接到互联网。 这些设备通常以 Cable/DSL 路由器的名称出售，因为它们同时适用于 DSL 和有线调制解调器。

有关如何在 Red Hat Linux 系统上配置网络以使系统能够访问互联网的信息，请参阅本小册子的第 2 章。

Figure 1-3:
NAT 路由器可将你的 PC 与互联网隔离开来，同时还能让你与其他 PC 在局域网中共享 DSL 连接。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_320_1.png)

## 使用有线调制解调器连接

有线电视公司还通过输送电视信号到你家中的同轴电缆提供高速互联网接入。 在有线电视公司在其设施中安装必要的设备以通过同轴电缆发送和接收数字数据后，客户可以报名使用有线互联网服务。 然后你就可以通过输送有线电视信号到你家的同一根电缆获得高速互联网接入。

### 有线调制解调器的工作原理

盒子 *有线调制解调器* 是通过有线电视网络访问互联网的核心。 有线调制解调器将来自你 PC 以太网卡的数字数据放入一个未使用的频率块中（可以把它想成另一个电视频道，但与画面和声音不同，该频道承载的是数字数据）。

有线调制解调器将 *上行数据* ——从你的 PC 发送到互联网的数据——放在与 *下行* 数据不同的频道中，而 *下行* 数据是从互联网传向你的 PC 的。 设计上，下行数据传输的速度远高于上行传输。 假设人们从互联网下载的东西远多于上传的东西。 （对我们大多数人来说可能确实如此。）

![](img/a7eec43a54473e95dc5ea333fecf1bd7_321_0.png)

Figure 1-4:
有线调制解调器通过有线电视网络提供高速互联网接入。

将数百个有线电视频道输送到你家的同轴电缆是一种非常强大的信号载体。 特别是，同轴电缆可以承载覆盖巨大频率范围的信号——数百兆赫兹（MHz）。 每个电视频道需要 6 MHz——而同轴电缆可以承载数百个这样的频道。 有线调制解调器将上行数据放在一个较小的频段中，并期望在完全不同的频段中接收下行数据。

在你通往互联网的有线连接的另一端是 Cable Modem Termination System（CMTS），由你的有线电视公司在其中央设施安装（参见图 1-4）。 CMTS 将有线电视网络连接到互联网。 它还提取由你的有线调制解调器（以及邻居的调制解调器）发送的上行数字数据并将其全部发送到互联网。 CMTS 还将数字数据放入上行频道，以便你的有线调制解调器可以提取该数据并通过以太网卡提供给你的 PC。

有线调制解调器可以以约 30 Mbps 的速率接收下行数据，并以约 3 Mbps 的速率发送上行数据。 然而，一个社区内的所有有线调制解调器共享相同的下行容量。 每个有线调制解调器都会过滤掉——分离出——它需要的数据，从 CMTS 发送的数据流中分离出来。

实际上，使用有线调制解调器，你可以获得约 1.5 Mbps 的下行传输速率和 128 Kbps 的上行速率。

如果你想检查你的下行传输速度，请访问 bandwidthplace.com/speedtest 并点击链接开始测试。 例如，我的有线调制解调器连接的测试报告下行传输速率约为 1.4 Mbps。

### 典型的有线调制解调器设置

要设置有线调制解调器接入，你的有线电视服务提供商必须提供高速互联网接入。 如果服务可用，你可以致电报名。 有线电视公司通常会有促销优惠，例如免安装费或三个月优惠费率。 寻找这些优惠。 如果你幸运的话，他们可能正好在你想报名时开展促销活动。

安装通常由技术人员完成，他将你的入户电缆分成两路——一路通往电视，另一路通往有线调制解调器。 技术人员会向有线电视公司的前端提供有关有线调制解调器的信息以便在其端进行设置。 全部完成后，你可以将 PC 的以太网卡插入有线调制解调器，即可享受高速互联网接入。 图 1-5 显示了典型的有线调制解调器连接方式。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_323_0.png)

Figure 1-5:
有线电视信号在电视和有线调制解调器之间被分开。

因为有线调制解调器连接到以太网卡，所以你的 PC 需要一块以太网卡。 有线电视公司技术人员通常会提供一块以太网卡。

图 1-5 中有线调制解调器设置需要注意的一些关键点如下：

-   使用 2 路分路器将入户有线电视信号分成两部分（由有线电视公司技术人员安装）。 顺便说一下，2 路分路器应额定为 1 GHz； 否则，它可能无法通过包含来自互联网下行数据的频率。
-   使用同轴电缆将分路器的其中一个视频输出连接到有线调制解调器的 F 型视频连接器。
-   将有线调制解调器的 10BaseT 以太网连接连接到你 PC 上的以太网卡。
-   将你的电视连接到双向分路器的另一个视频输出。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_323_1.png)

当你使用有线调制解调器将 Red Hat Linux PC 连接到互联网时，连接始终处于开启状态，因此有人试图入侵 PC 的可能性更大。 你应将防火墙设置设为高安全性。 要配置防火墙设置，请从 GNOME 桌面选择 主菜单→系统设置→安全级别。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_324_0.png)

你可能希望在 PC 和有线调制解调器之间添加一个 NAT（网络地址转换）路由器。 作为额外的好处，你甚至可以通过添加以太网集线器与你自己的局域网（LAN）中的所有 PC 共享有线调制解调器连接。 更好的选择是购买一个 NAT 路由器和集线器组合，这样只需一个设备即可完成全部工作。 顺便说一下，NAT 路由器/集线器通常以 Cable/DSL 路由器的名称出售，因为它们同时适用于 DSL 和有线调制解调器。

NAT 路由器将私有互联网协议（IP）地址转换为公共 IP 地址。 通过 NAT 路由器连接时，内部局域网中的任何 PC 都可以像拥有自己的唯一 IP 地址一样访问互联网。 结果：单个互联网连接可以被许多 PC 共享。 （整个上网家庭的理想解决方案！）

图 1-6 显示了典型的设置，其中有线调制解调器连接被局域网中的多台 PC 共享。

设置如图 1-6 所示的连接时需要注意以下几点：

-   你需要一个带有两个 10BaseT 以太网端口的 Cable/DSL NAT 路由器（10BaseT 端口——也称为 RJ-45 插孔——看起来像一个大号电话插孔）。 通常，一个以太网端口标记为 Internet（或 External 或 WAN 表示广域网），另一个标记为 Local。
-   如果你计划设置局域网，你还需要一个以太网集线器。 对于小型家庭网络，你可以购买 4 或 8 端口以太网集线器。 基本上，你需要一个具有与你打算连接到局域网的 PC 数量相同端口数的集线器。
-   考虑购买一个既可作为 NAT 路由器又可作为具有多个以太网端口的集线器的单一设备。
-   将视频电缆连接到有线调制解调器的视频输入端口。
-   使用 10BaseT 以太网电缆（看起来像电话线，但以太网电缆的 RJ-45 插头更大，通常标记为 Category 5 或 Cat 5 线）将有线调制解调器的以太网端口连接到 NAT 路由器的 Internet 端口。
-   使用 10BaseT 以太网电缆将 NAT 路由器的 Local 以太网端口连接到以太网集线器的其中一个端口。
-   现在将每台 PC 连接到以太网集线器。 当然，每台 PC 必须具有以太网卡。

在本小册子的第 2 章中，我将解释如何配置此类局域网中的 PC，使它们都能访问互联网。



## 设置拨号网络

图 1-6:
NAT 路由器将你的 PC 与 Internet 隔离开来，同时还能让你与局域网中的其他 PC 共享有线调制解调器连接。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_325_0.png)

拨号网络是指通过拨号调制解调器将 PC 连接到远程网络。如果你足够“古老”，还记得用 Procomm 或某些串行通信软件拨号的时代，那么拨号网络与过去的串行通信之间存在显著差异。这两种方法都使用调制解调器拨号到远程计算机并建立通信路径，但串行通信软件会让你的计算机表现得像连接到远程计算机的哑终端。串行通信软件独占拨号连接。例如，你不能运行另一份通信软件并使用同一个调制解调器连接。

在拨号网络中，你的 PC 和远程系统都运行网络协议（称为 TCP/IP）软件。当你的 PC 拨号并建立通信路径时，网络协议通过该拨号连接交换数据包。好处在于，任意数量的应用程序都可以使用同一个拨号连接发送和接收数据包。因此你的 PC 成为远程计算机所属网络的一部分。（如果远程计算机不在网络上，拨号网络会创建一个由远程计算机和你的 PC 组成的网络。）

在本小书的第 2 章中，我会更详细地描述 TCP/IP 协议，但在描述如何设置拨号网络时，我也必须使用该术语以及其他一些概念——例如 Internet *协议 (IP) 地址和域名系统 (DNS)*。

在拨号链路上设置 TCP/IP 网络涉及指定协议——即在通信链路上打包数据包的约定。*点对点协议 (PPP)* 就是这样一种协议，用于在任何点对点链路上建立 TCP/IP 连接，包括拨号电话线路。Red Hat Linux 支持 PPP，并附带了配置工具，你可以使用它们设置 PPP，以便你的系统能够与 ISP 建立 PPP 连接。

在 Red Hat Linux 中设置拨号网络，你需要做以下事项：

- 1. 在你的 PC 中安装内部或外部调制解调器。如果你的 PC 本身没有内置调制解调器，你可以购买外部调制解调器并将其连接到 PC 的串行或 USB 端口。
- 2. 将调制解调器连接到电话线路。
- 3. 向 ISP 申请一个账号。每个 ISP 都会为你提供拨号电话号码、用户名和密码。此外，ISP 还应提供电子邮件和新闻服务器的完整名称。通常，你的系统会自动获取 IP 地址。
- 4. 测试你的调制解调器并确保其正常工作。你可以使用 Red Hat Linux 附带的串行通信软件包 `minicom` 进行此测试。
- 5. 运行 Internet 配置向导以设置 PPP 连接。
- 6. 激活 PPP 连接以连接到 Internet。

我将在以下各节中简要介绍这些步骤。

### 连接调制解调器

*调制解调器* 是 modulator/demodulator 的缩写——一种设备，可将数字信号（由 1 和 0 组成的串）转换为可通过电话线路和无线电波传输的连续变化的模拟信号。因此，调制解调器是 PC 数字世界与电话模拟世界之间的中介。图 1-7 说明了调制解调器的概念。

在 PC 内部，1 和 0 用电压电平表示，但通过电话线路传输的信号通常是不同频率的音调。调制解调器位于 PC 和电话线路之间，使电话线路上的数据通信成为可能。调制解调器在数字电路的电压/无电压表示与适合通过电话线路传输的不同频率音调之间进行转换。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_326_0.png)

图 1-7:
调制解调器架起了 PC 数字世界与电话模拟世界之间的桥梁。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_327_0.png)

在使用外部调制解调器拨号之前，你必须确保调制解调器已正确连接到 PC 的串行或 USB 端口之一。

如果你有外部调制解调器，请确保调制解调器已正确连接到电源，并且调制解调器已连接到电话线路。购买合适的电缆将调制解调器连接到 PC。你需要一根直通串行电缆将调制解调器连接到 PC。电缆两端的连接器取决于 PC 上串行连接器的类型。电缆的调制解调器端需要一个公头 25 针连接器。电缆的 PC 端通常是一个母头 9 针连接器。你可以在大多数电脑商店购买调制解调器电缆。通常你可以在标有“AT Modem Cable”的标签下找到 9 针母头转 25 针公头的调制解调器电缆。使用 USB 电缆连接 USB 调制解调器。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_327_1.png)

如果你的 PC 有内置调制解调器，你只需将电话线路连接到内置调制解调器卡背面的电话插孔即可。如果是 winmodem，你仍然需要连接电话线路，但你还需要在 Internet 上做一些研究并下载一个使 winmodem 在 Red Hat Linux 中工作的驱动程序。在你为 winmodem 安装了可用的 Linux 驱动程序后，它的工作方式就与旧的串口调制解调器一样。

### 学习串行设备名称

PC 通常有两个串行端口，在 MS-DOS 用语中称为 COM1 和 COM2。许多配备通用串行总线 (USB) 的新 PC 只有一个串行端口。PC 还可以支持另外两个串行端口：COM3 和 COM4。由于这些端口名称，我们经常将串行端口称为 COM 端口。

与其他设备一样，串行端口设备由 /dev 目录中的设备文件表示。串行端口还需要中断请求 (IRQ) 编号和 I/O 端口地址。两个 IRQ——3 和 4——在四个 COM 端口之间共享。表 1-2 列出了 PC COM 端口对应的串行设备名称，以及分配给四个串行端口的 IRQ 和 I/O 端口地址。

### Winmodems：它们只做 Windows

关于许多新 PC 和笔记本电脑附带的 winmodems，有一点需要注意。这些是基于软件的内部调制解调器——与传统的硬件调制解调器完全不同。也称为 Windows 调制解调器或软件调制解调器，它们仅与特殊驱动程序软件一起工作（该软件反过来仅在 Microsoft Windows 上工作）。对于 winmodems 和 Linux 来说，你基本上只能靠自己——但你可以在 Linux Winmodem Support 主页 www.linmodems.org 上找到一些有用的指导。例如，我发现我的笔记本电脑中的 winmodem 使用 Conexant 芯片组，并且 Linux 驱动程序可从 www.linuxant.com/drivers/hsf/download-rh-1686.html 获取。然后我为我的内核版本下载了一个 RPM 文件，并使用 rpm 命令将其安装在笔记本电脑上。之后，我就可以从 Red Hat Linux 应用程序中使用笔记本电脑的 winmodem 了。

表 1-2 串行端口的设备名称

| COM 端口 | 设备名称 | IRQ | I/O 地址 |
|---|---|---|---|
| COM1 | /dev/ttyS0 | 4 | 0x3f8 |
| COM2 | /dev/ttyS1 | 3 | 0x2f8 |
| COM3 | /dev/ttyS2 | 4 | 0x3e8 |
| COM4 | /dev/ttyS3 | 3 | 0x2e8 |

所有这些设备都应该已存在于你的 Red Hat Linux 系统中。在终端窗口中，输入 ls -l /dev/ttyS* 以查看这些设备文件的列表。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_328_0.png)

如果你的调制解调器连接到 USB 端口或你使用的是 winmodem，设备名称会不同。对于 winmodems，你必须先下载并安装驱动程序。你可以通过查看 www.linmodems.org 网站来为许多 winmodems 找到 Linux 驱动程序。在许多情况下，Linux winmodem 驱动程序会将调制解调器设备 /dev/modem 设置为指向实际设备文件的符号链接。这样，你就可以使用通用名称 /dev/modem 来引用调制解调器设备，而不必学习较为复杂的设备名称。

### 检查 Linux 内核是否检测到串行端口

为验证 Linux 内核是否正确检测到串行端口，请使用以下命令检查启动消息：

```
dmesg | grep ttyS
```



如果你看到如下信息，则 Linux 已在你的 PC 中检测到串行端口：

```
ttyS0 at 0x03f8 (irq = 4) is a 16550A
```

在这种情况下，该消息表示 Linux 内核已检测到第一个串行端口（COM1）。它显示了 I/O 地址（十六进制），0x3f8，以及 IRQ 4。消息的最后一部分 — 16550A — 指的是通用异步收发器/发送器（UART）芯片的识别编号，该芯片是所有串行通信硬件的核心（UART 将每个字节转换为 1 和 0 的流，并在接收此类流时反向转换）。

你也可以使用 setserial 命令检查串行端口。输入以下命令以查看有关串行端口的详细信息：

```
setserial -g /dev/ttyS?
```

任何在此命令输出中列出且 UART 未知的设备，要么未安装，要么未被 Linux 内核检测到。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_329_0.png)

## 测试调制解调器

完成调制解调器的物理安装并验证 Linux 内核检测到串行端口后，你可以尝试通过调制解调器拨号。最佳方法是使用随 Red Hat Linux 提供的 Minicom 串行通信程序。

Minicom 类似于你在 MS-DOS 或 Windows 下可能使用过的其他通信软件，例如 Procomm 或 Crosstalk。

要运行 Minicom，请以 root 身份登录，并在终端窗口（或虚拟控制台）中的 shell 提示符下输入 minicom。Minicom 运行并重置调制解调器。图 1-8 显示了在终端窗口中运行 Minicom 的结果。

如果看不到 OK，这可能意味着此特定串行设备名称未设置正确。要设置串行设备，请按照以下步骤操作：

- 1. 按 Ctrl+A 然后按 Z。
- Minicom 显示其帮助屏幕。
- 2. 按 O。
- Minicom 显示其配置菜单。
- 3. 使用方向键选择 Serial port setup 并按 Enter。
- Minicom 显示串行端口设置。
- 4. 按 A。

Minicom 将光标放在显示串行设备名称的行中。编辑设备名称以匹配调制解调器的连接位置。例如，如果调制解调器位于第一个串行端口，请确保设备名称为 /dev/ttyS0。

- 5. 按两次 Enter。
- Minicom 返回到配置菜单。
- 6. 选择 Save setup as dfl 并按 Enter。
- Minicom 保存设置。
- 7. 选择 Exit 并按 Enter。
- Minicom 返回在线模式。
- 8. 按 Ctrl+A 和 X。
- Minicom 提示你是否真的要退出。
- 9. 按 Enter 退出。
- 设置调制解调器所连接串行端口的正确设备名称后，请确保调制解调器已通电并连接到电话线。
- 10. 再次启动 Minicom（在终端窗口中输入 minicom）。
- 11. 按 Ctrl+A 以获取 Minicom 程序的注意。
- 按下 Ctrl+A 后，如果按下 Z，则会以文本窗口的形式显示帮助屏幕。在帮助屏幕中，你可以获取有关其他 Minicom 命令的信息。

图 1-8：你可以使用 Minicom 手动测试调制解调器。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_330_0.png)

12. 从帮助屏幕按 Enter 返回在线模式。

在线模式下，你可以使用调制解调器的 AT 命令拨号。特别是，你可以使用 ATDT 命令拨打另一台调制解调器的电话号码（例如，拨打你的 ISP 号码）。当你收到登录提示时，就知道调制解调器正在工作。图 1-9 显示了使用 Minicom 进行典型拨号的结果：使用 56 Kbps 调制解调器仅为 38.4 Kbps。（难怪我需要 DSL 或有线调制解调器！）

![](img/a7eec43a54473e95dc5ea333fecf1bd7_331_0.png)

图 1-9：
使用 ATDT 命令通过 Minicom 手动拨号。

13. 要退出 Minicom，请按 Ctrl+A 然后输入 X。

14. 再次按 Enter 关闭 Minicom。

## 设置和激活 PPP 连接

大多数 ISP 通过 ISP 维护的一个或多个系统提供对 Internet 的 PPP 拨号访问。如果你注册此类服务，ISP 应该为你提供建立与 ISP 系统的 PPP 连接所需的信息。通常，此信息包括以下内容：

- 拨号以连接到远程系统的电话号码
- 你必须用于登录远程系统的用户名和密码
- ISP 的邮件和新闻服务器的名称
- 你的 PPP 连接的 IP 地址。ISP 不提供此地址如果 IP 地址动态分配（这意味着每次系统建立连接时 IP 地址可能会更改）。
- ISP 的域名服务器（DNS）的 IP 地址。ISP 不提供这些地址如果它动态分配 IP 地址。

这些信息中，前两项是设置 PPP 连接所需的内容。

按照以下步骤使用 Red Hat 的 Internet 配置向导设置 PPP 连接：

- 1. **以 root 身份登录并从 GNOME 桌面选择 主菜单→系统工具→Internet 配置向导。**

如果你未以 root 身份登录，在提示时输入 `root` 密码。

选择设备类型对话框出现（如图 1-10 所示）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_332_0.png)

图 1-10：
从此对话框配置调制解调器连接。

- 2. **从设备类型列表中选择 Modem connection，然后单击 Forward。**

选择调制解调器对话框显示有关你的调制解调器的信息。

- 3. **单击 Forward 继续。**

选择提供商对话框出现。

- 4. **在文本框中填写连接信息 — ISP 的电话号码、你的登录名和密码（见图 1-11）；单击 Forward 继续。**

图 1-11：
在此对话框中填写连接信息。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_333_0.png)

5. 输入 IP 设置 — 是否想要自动获取 IP 地址或提供静态 IP 地址 — 然后单击 Forward 继续。

通常，你会选择从 ISP 自动获取 IP 地址和名称服务器设置的选项。

6. 单击 Apply 保存拨号配置信息，然后关闭 Internet 配置向导。

网络配置对话框出现，其中列出了新拨号连接的名称（图 1-12）。

图 1-12：
在网络配置对话框中单击 Activate 以建立 PPP 连接。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_333_1.png)

7. 选择连接名称，然后单击 Activate。
8. 完成后，单击 Deactivate 关闭 PPP 连接。

## 配置 CHAP 和 PAP 认证

系统上的 PPP 服务器必须在 PPP 连接完全建立之前向 ISP 的 PPP 服务器进行身份验证。身份验证需要证明你拥有 ISP 的有效账户；本质上这涉及提供用户名和密钥（即密码）。PPP 规定了在连接两端之间交换身份验证信息的两种方式：

- **Challenge Handshake Authentication Protocol (CHAP)** 要求远程端发送随机生成的挑战字符串以及远程服务器的名称。本地系统使用服务器名称查找密钥；然后它发送回一个响应，其中包含其名称和一个结合了密钥和挑战的值，使用单向哈希函数。远程系统然后将该值与自己计算的预期哈希值进行比较。如果值匹配，则身份验证成功；否则，远程系统终止连接。在这种情况下，名称和密钥存储在 `/etc/ppp/chap-secrets` 文件中。请注意，远程系统可以在 PPP 链路处于活动状态时随时重复 CHAP 身份验证。
- **Password Authentication Protocol (PAP)** 与正常登录过程类似。使用 PAP 时，本地系统会重复发送用户名（名称）和密码（密钥），直到远程系统确认身份验证或结束连接。名称和密钥存储在 `/etc/ppp/pap-secrets` 文件中。请注意，用户名和密码以明文形式发送（即未加密）。

Linux PPP 服务器支持这两种类型的身份验证。对于 PAP 和 CHAP，PPP 服务器所需的信息是名称和密钥 — 一个用户名-密码对。此身份验证信息存储在以下配置文件中：

- `/etc/ppp/chap-secrets` 存储 CHAP 的信息。典型的 chap-secrets 文件如下所示：

```
# Secrets for authentication using CHAP
# client    server    secret    IP addresses
"naba"      *        "mypassword"
```

- `/etc/ppp/pap-secrets` 存储 PAP 的信息。典型的 pap-secrets 文件如下所示：

```
# Secrets for authentication using PAP
# client    server    secret    IP addresses
"naba"      *        "mypassword"
```



正如你所见，`chap-secrets` 和 `pap-secrets` 两者的条目格式相同。每行包含四个字段，按以下顺序排列：

- 1. `client` — 该字段包含身份验证期间使用的名称。这是你从 ISP 获得的用户名。
- 2. `server` — 该字段包含用于对本地系统进行身份验证的远程系统的名称。如果不知道服务器名称，请使用星号表示任意服务器。
- 3. `secret` — 这是系统 PPP 服务器必须发送给远程系统以进行自身身份验证的密钥。这是你从 ISP 收到的密码。
- 4. `IP addresses` — 此可选字段可包含本地系统在连接指定服务器时可能使用的 IP 地址列表。通常该字段留空，因为本地系统通常从服务器获取动态 IP 地址（因此）不知道将使用什么 IP 地址。

### 第 2 章：设置本地局域网

### 本章内容

- 了解 TCP/IP 网络
- 设置以太网 LAN
- 配置 TCP/IP 网络
- 将你的 LAN 连接到互联网

Red Hat Linux 内置了对 TCP/IP（传输控制协议/互联网协议）网络的支持，大多数现代操作系统从 Windows 到 Mac OS 也是如此。你可以在许多不同的物理接口上使用 TCP/IP 网络，例如以太网卡、串行端口和并行端口。

通常，你使用以太网网络作为你的局域网（LAN）——在办公室甚至家中（如果你恰好在家中有几台系统）。要通过调制解调器连接到远程系统，你使用点对点协议（PPP）上的 TCP/IP 网络。

本章描述如何设置以太网网络。即使你只有一台 PC，你也可能需要设置以太网网络接口，以便将你的 PC 连接到使用 DSL 或电缆调制解调器的高速互联网接入。（我在本迷你书的第 1 章中介绍了 DSL 和电缆调制解调器。）

### 了解 TCP/IP

如果你以四层分层模型来思考，你就能最好地理解 TCP/IP 网络。把每一层都看作负责执行特定任务。分层模型描述了数据在网络的物理连接与最终用户应用程序之间流动的方式。图 2-1 显示了 TCP/IP 的四层网络模型。

在此四层模型中，信息始终从一层移动到下一层。例如，当一个应用程序向另一个应用程序发送数据时，数据按此顺序经过各层：Application→Transport→Network→Physical。在接收端，数据从 Physical→Network→Transport→Application 向上移动。

图 2-1：
你可以使用四层网络模型来理解 TCP/IP。

|   | 层 | 协议 / 注释 |
|---|-------|---------------|
| 4 | Application | Mail, file transfer, TELNET |
| 3 | Transport | TCP (Transmission Control Protocol)<br>UDP (User Datagram Protocol) |
| 2 | Network | IP (Internet Protocol) |
| 1 | Physical | Ethernet |

![](img/a7eec43a54473e95dc5ea333fecf1bd7_337_0.png)

每一层都有自己的一套协议——约定——用于处理和格式化数据。如果你把发送数据想象成通过邮政服务寄信，那么典型的协议就是为某项任务（如写信封地址）提供首选的行动顺序（先写姓名，然后写街道地址，然后写城市、州和邮政编码或其他邮政编码）。

以下是从上到下四层各自的作用：

- **Application layer:** 运行用户使用的应用程序，例如电子邮件阅读器、文件传输和 Web 浏览器。存在应用层协议，例如用于电子邮件的简单邮件传输协议（SMTP）和邮局协议（POP）、用于 Web 的超文本传输协议（HTTP）以及用于文件传输的文件传输协议（FTP）。应用层协议还具有 *port number*，你可以将其视为特定应用程序的标识符。例如，端口 80 与 HTTP 或 Web 服务器相关联。
- **Transport layer:** 将数据从一个应用程序发送到另一个应用程序。该层最重要的两个协议是 *Transmission Control Protocol*（TCP）和 *User Datagram Protocol*（UDP）。TCP 保证数据的交付；UDP 只是发送数据而不确保它实际到达目的地。
- **Network layer:** 该层负责将数据包从一个 *network* 传输到另一个网络。如果网络相距甚远，数据包将被路由从一个网络到下一个网络，直到到达目的地。该层的主要协议是互联网协议（IP）。
- **Physical layer:** 指的是网络中承载数据包的物理网络硬件（例如以太网卡或令牌环卡）。

分层模型的美妙之处在于每一层只负责其特定的任务，其余的留给其他层。各层可以混合搭配——你可以在任何类型的物理网络介质上使用 TCP/IP 网络，从以太网到无线网络中的无线电波。软件也是模块化的，因为每一层都可以实现在不同的模块中。例如，通常传输层和互联网层已作为操作系统的一部分存在；任何应用程序都可以使用这些层。

### TCP/IP 与互联网

TCP/IP 已成为互联网——从 ARPAnet 演变而来的“网络的网络”——的首选协议。美国政府的先进研究项目署（ARPA）在 1970 年代启动了研究，探索使用通过网络发送的数据包以新的方式发送信息的方法。结果是 ARPAnet：一个由联网计算机组成的全国网络。随后，ARPA 获得了国防前缀并成为 DARPA。在 DARPA 的 auspices 下，TCP/IP 协议作为互联网互联——网络间通信——的流行协议集合而出现。

TCP/IP  flourished 因为该协议是开放的。这意味着协议的技术描述出现在公共文档中，因此任何人都可以将 TCP/IP 实现在特定的硬件和软件上。

TCP/IP 也取得了长足进展，因为有稳定的工作软件可用。TCP/IP 协议不是网络架构和协议的纸面描述，而是作为工作软件开始的——谁能反对已经在工作的东西呢？这些天（因此），TCP/IP 统治着互联网。

### IP 地址

当你在一个网络上有许多台计算机时，你需要一种方式唯一地标识每一台。在 TCP/IP 网络中，计算机的地址是 IP 地址。因为 TCP/IP 处理互联网互联，所以地址基于网络地址和主机地址的概念。你可以把网络地址和主机地址的想法看作需要提供两个地址来唯一标识一台计算机：

- 网络地址表示计算机所在的网络。
- 主机地址表示该网络上的特定计算机。

### 下一代 IP（IPv6）

当 4 字节 IP 地址创建时，可用地址的数量似乎足够。现在，然而，4 字节地址正在用完。互联网工程任务组（IETF）在 1991 年认识到可能用完 IP 地址的潜力，并开始着手下一代 IP 地址方案。他们称之为 IPng（Internet Protocol Next Generation 的缩写），并打算最终取代旧的 4 字节地址方案（称为 IPv4，即 IP 版本 4）。

IPv6 设计为从 IPv4 的演进步骤。所提出的标准在旧 IPv4 地址主机和任何新 IPv6 主机之间提供直接互操作性。想法是用户可以在想要时升级系统以使用 IPv6，并且网络运营商可以自由地升级其网络硬件以使用 IPv6，而不影响 IPv4 的当前用户。IPv6 的示例实现正在为许多操作系统开发，包括 Linux。有关 Linux 中 IPv6 的更多信息，请参阅 www.linuxhq.com/IPv6/ 上的 Linux IPv6 FAQ/HOWTO。

提出了并辩论了多种 IPng 的替代寻址方案。最终的竞争者，采用 128 位（16 字节）地址，被称为 IPv6（IP 版本 6）。1995 年 9 月 18 日，IETF 宣布 IPv6 地址协议的核心集为 IETF 拟议标准。

IPv6 128 位寻址方案允许 170,141,183,460,469,232,000,000,000,000,000,000 个唯一主机！这应该能让我们使用一段时间！

网络地址和主机地址共同构成一个 IP 地址，它是一个 4 字节（32 位）值。惯例是以十进制值写出每个字节，并在每个数字后加上一个点（.）。因此你会看到诸如 132.250.112.52 之类的网络地址。这种写法 IP 地址的方式称为点分十进制或点分四组表示法。

在十进制表示法中，一个字节（有 8 位）的值可以在 0 到 255 之间。因此有效的 IP 地址只能在点分十进制表示法中使用 0 到 255 之间的数字。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_339_0.png)

### 互联网服务和端口号

TCP/IP 协议套件已成为互联网的通用语言，因为在支持 TCP/IP 的任何系统上都有许多标准服务可用。这些服务通过促进邮件、新闻和网页的传输使互联网运转。这些服务以众所周知的名称出现，例如以下：

- DHCP（动态主机配置协议）用于动态配置计算机上的 TCP/IP 网络参数。DHCP 主要

用于分配动态IP地址和其他网络信息（如名称服务器、默认网关和域名）以配置TCP/IP网络。DHCP服务器监听67端口。

-   **FTP (文件传输协议)** 用于在Internet上计算机之间传输文件。FTP使用两个端口——数据在20端口传输，而控制信息在21端口交换。
-   **HTTP (超文本传输协议)** 是一种用于从一个系统向另一个系统发送文档的协议。HTTP是Web的基础协议。默认情况下，Web服务器和客户端在80端口通信。
-   **SMTP (简单邮件传输协议)** 用于在系统之间交换电子邮件消息。SMTP使用25端口进行信息交换。
-   **NNTP (网络新闻传输协议)** 用于以存储转发方式在Internet上分发新闻文章。NNTP使用119端口。
-   **TELNET** 用于用户在一个系统上登录Internet上的另一个系统时（用户必须提供有效的用户ID和密码才能登录远程系统）。TELNET默认使用23端口，但TELNET客户端可以连接到任何端口。
-   **SNMP (简单网络管理协议)** 用于管理Internet上各种类型的网络设备。与FTP类似，SNMP使用两个端口：161和162。
-   **TFTP (简单文件传输协议)** 用于从一个系统向另一个系统传输文件（通常由X终端和无盘工作站用于从网络上的另一主机下载引导文件）。TFTP数据传输在69端口进行。
-   **NFS (网络文件系统)** 用于在计算机之间共享文件。NFS使用Sun的远程过程调用（RPC）机制，该机制通过111端口交换信息。

每个这些服务都关联一个众所周知的端口。TCP协议使用每个此类端口在任何系统上定位服务。（服务器进程——在系统上运行的特殊计算机程序——提供每个服务。）

## 设置以太网局域网

以太网是将数据包在连接到单根电缆的两个或多个计算机之间移动的标准方式。（你可以通过网关连接多个以太网段来创建更大的网络。）要设置以太网局域网（LAN），每个PC都需要一张以太网卡。Red Hat Linux 支持多种用于PC的以太网卡。

以太网是物理数据传输机制的良好选择，原因如下：

-   以太网是一种经过验证的技术，自20世纪80年代初以来一直在使用。
-   以太网提供良好的数据传输速率：通常为每秒10兆位（10 Mbps），尽管现在已有100-Mbps以太网和千兆以太网（1,000 Mbps）。
-   以太网硬件相对成本低。（PC以太网卡约花费20美元。）
-   使用无线以太网，你可以轻松地将笔记本电脑连接到你的以太网LAN——无需到处布线。（请参阅本迷你书的第3章，了解有关无线以太网的更多信息。）

## 以太网的工作原理

那么是什么让以太网运转？本质上，它与操场课间活动的工作原理相同：轮流进行。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_341_0.png)

在以太网中，段内的所有系统都连接到同一根导线上。因为使用单根导线，所以必须使用协议来发送和接收数据，因为在任何时候电缆上只能存在一个数据包。以太网LAN使用一种称为载波侦听多路访问/冲突检测（CSMA/CD）的数据传输协议来在所有计算机之间共享单根传输电缆。计算机中的以太网卡遵循CSMA/CD协议来传输和接收以太网数据包。

CSMA/CD协议背后的思想类似于你在聚会上交谈的方式。你倾听暂停（即侦听载波），在没有人说话时讲话。如果你和另一个人同时开始说话，你们双方都会意识到问题（即冲突检测）并暂停片刻；然后其中一人再次开始讲话。正如你从经验中知道的那样，一切都会顺利进行。

在以太网LAN中，每张以太网卡检查电缆上的信号——这就是载波侦听部分。如果信号电平较低，以太网卡就会在电缆上发送其数据包；数据包包含有关发送方和预期接收方的信息。LAN上的所有以太网卡都会监听信号，接收方接收数据包。如果两张卡同时发送数据包，电缆中的信号电平会上升超过阈值，卡就会知道发生了冲突（两个数据包同时发送）。两张卡都会在随机时间后再次发送数据包。

以太网由Robert M. Metcalfe于20世纪70年代初在施乐帕洛阿尔托研究中心（PARC）发明。在20世纪80年代，以太网由三家公司合作标准化：数字设备公司（DEC）、Intel和Xerox。利用公司名称的首字母，该以太网标准被称为DIX标准。后来，DIX标准被纳入电气和电子工程师协会（IEEE）制定的802系列标准。以太网的最终规范正式称为IEEE 802.3 CSMA/CD，但人们仍然称其为以太网。

以太网以数据包（也称为帧的离散块）发送数据。你不必过多关注以太网数据包的内部结构，除了注意6字节的源地址和目的地址。每个以太网控制器都有一个唯一的6字节（48位）地址——在物理层，每个数据包都必须有一个。

## 以太网电缆

只要你听到专家谈论以太网，你也会听到一些令人困惑的术语用于承载数据的电缆。以下是简要概述。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_342_0.png)

最初的以太网标准使用直径近半英寸的粗同轴电缆。这种布线称为粗缆或粗以太网，尽管IEEE 802.3标准称其为10Base5。该命名意味着几件事：数据传输速率为每秒10兆位（10 Mbps）；传输为基带（这仅仅意味着电缆的信号承载能力专门用于传输以太网数据包）；电缆总长度不得超过500米。粗缆价格昂贵，电缆相当笨重。除非你是技术历史爱好者，否则你不必在乎10Base5电缆。

如今，另两种以太网布线形式更受欢迎。粗以太网电缆的第一个替代品是细缆，或10Base2，使用细而柔韧的同轴电缆。细缆以太网段最多可长185米。另一种更新的替代方案是通过非屏蔽双绞线电缆（UTP）的以太网，称为10BaseT。

要设置10BaseT以太网网络，你需要一个以太网集线器——一个带有RJ-45插孔的硬件盒（这些看起来像大电话插孔）。你通过从每台PC的以太网卡到该集线器布设双绞线（通常是五类或Cat5电缆）来构建网络。你可以以约50美元的价格购买一个4端口10BaseT集线器。图2-2显示了你在小型办公室或家中可能设置的一个典型小型10BaseT以太网LAN。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_343_0.png)

图2-2：
你可以使用以太网集线器设置10BaseT以太网LAN。

当你从本书的配套DVD-ROM在连接了以太网卡的PC上安装Red Hat Linux时，Red Hat安装程序应自动检测以太网卡并安装适当的驱动程序。安装程序还应允许你设置TCP/IP网络。

安装正确后，Linux内核应在每次启动时加载以太网卡的驱动程序。要验证以太网驱动程序是否已加载，请在终端窗口中输入以下命令：

```
dmesg | grep `grep eth0 /etc/modules.conf | cut -d ' ' -f 3`
```

此命令搜索启动消息中包含第一张以太网卡名称的任何行（反引号中的命令——`grep eth0 /etc/modules.conf | cut -d ' ' -f 3`——从/etc/modules.conf文件中提取eth0设备的别名）。

在我的PC上，我安装了Intel Ethernet Pro 100（e100）卡，因此在我的系统上输入该命令时得到以下输出：

```
e100: selftest OK.
e100: eth0: Intel(R) PRO/100 WfM PCI Adapter
```

你应该看到类似的内容，显示你的以太网卡名称和其他参数。



## 配置 TCP/IP 网络

当你在 Red Hat Linux 安装期间设置 TCP/IP 网络时，安装程序会使用你提供的信息准备所有适当的配置文件。然而，Red Hat Linux 随带了一个图形化网络配置工具，你可以用它来添加新的网络接口或更改诸如名称服务器和主机名之类的信息。

TIP: 如果你正在添加新的以太网卡（或如果你的以太网卡在安装期间未配置），请使用 Linux 网络配置工具来设置网络。

要启动网络配置工具，请以 root 身份登录，并从 GNOME 桌面中选择 主菜单→系统设置→网络。如果未以 root 身份登录，则会提示输入 root 密码。

网络配置工具显示一个带标签的对话框，如图 2-3 所示。

Figure 2-3: 使用 Red Hat 网络配置工具配置以太网网络。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_344_0.png)

你可以通过对话框顶部出现的四个标签来配置网络。以下是每个标签的作用：

- **Devices:** 在这里你可以找到新网络接口（例如以太网卡）的选项。你可以设置接口的 IP 地址然后激活它。有关设备的输入信息存储在 `/etc/sysconfig` 目录中的各种文件中。
- **Hardware:** 在这里添加新的硬件设备，如以太网卡、调制解调器或 ISDN 设备。然后你可以提供诸如中断请求（IRQ）、I/O 端口号和 DMA 通道等信息。
- **DNS:** 在这里输入系统的主机名并输入名称服务器的 IP 地址。名称服务器地址存储在 `/etc/resolv.conf` 文件中。主机名存储在 `/etc/sysconfig/network` 文件中的 `HOSTNAME` 变量中。
- **Hosts:** 此选项卡显示来自 `/etc/hosts` 文件的主机和 IP 地址的本地表，并允许你添加、删除或编辑条目。

要添加并激活新的以太网网络接口，请执行以下操作：

- 1. **在 Devices 选项卡中，单击新建按钮。**
  选择设备类型对话框出现。
- 2. **选择以太网连接并单击下一步。**
  选择以太网设备对话框出现。
- 3. **选择你的以太网卡并单击下一步。**
  配置网络设置对话框出现（如图 2-4 所示）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_345_0.png)

Figure 2-4: 在此对话框中配置网络设置。

- 4. **选择以太网卡获取其 IP 地址的方式：**
  如果它可以自动获取 IP 地址（当以太网卡连接到 DSL 或有线调制解调器时即为这种情况），请选择使用 DHCP 自动获取 IP 地址设置单选按钮。选择后，还请选中从提供商自动获取 DNS 信息复选框。

  否则，选择静态设置 IP 地址单选按钮，然后在提供的文本框中输入 IP 地址。对于家庭网络，使用私有 IP 地址，例如 192.168.0.2。（以 192.168. 开头的任何地址都可以使用。）
- 5. 单击下一步，然后单击应用以完成以太网设置。

你将返回到网络配置对话框。

- 6. 选择 eth0 设备，然后单击激活以打开以太网网络。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_346_0.png)

如果运行私有网络，你可以使用 192.168.0.0 到 192.168.255.255 范围内的 IP 地址。（为私有网络保留了其他地址范围，但此范围应足以满足大多数需求。）

## 将你的局域网连接到互联网

如果你的局域网中有几台 PC，你可以使用 DSL 或有线调制解调器将整个局域网连接到互联网。基本上，你可以与局域网中的所有 PC 共享高速 DSL 或有线调制解调器连接。

在本迷你书的第 1 章中，我解释了如何设置 DSL 或有线调制解调器。在本节中，我简要说明如何将局域网连接到互联网，以便所有 PC 都可以访问互联网。

通过 DSL 或有线调制解调器连接局域网到互联网最方便的方法是购买一个称为 DSL/有线调制解调器 NAT 路由器的硬件设备，并配有 4 或 8 端口以太网集线器。NAT 代表网络地址转换；NAT 路由器可以将多个私有 IP 地址转换为单个外部已知 IP 地址。以太网集线器部分表现为多个 RJ-45 以太网端口，你可以在此连接 PC 以设置局域网。换句话说，除了 DSL 或有线调制解调器外，你只需要一个额外的设备。

图 2-5 显示了你如何通过内置以太网集线器的 NAT 路由器将局域网连接到互联网。当然，要使其工作，你需要 DSL 或有线调制解调器连接（并且你必须向电话公司注册 DSL 服务或向有线服务提供商注册有线互联网服务）。

当你像这样将局域网连接到互联网时，NAT 路由器充当局域网的网关。NAT 路由器还动态地为局域网中的 PC 提供 IP 地址。因此，在每台 PC 上，你应设置网络选项以指示 IP 地址应动态获取。

Book IV
Chapter 2
Setting Up a Local Area Network

第四卷
第 2 章
设置局域网

Figure 2-5:
通过内置以太网集线器的 NAT 路由器将你的局域网连接到互联网。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_347_0.png)

局域网 (LAN) 中的 PC。
每台 PC 必须具有 10BaseT 以太网卡。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_347_1.png)

你的局域网可以混合搭配各种计算机——有些可能运行 Red Hat Linux，有些可能运行 Microsoft Windows 或任何其他支持 TCP/IP 的操作系统。在 Red Hat Linux PC 上，你可以使用网络配置工具设置以太网网络（从 GNOME 桌面选择主菜单→系统设置→网络）。配置网络设置时（参见图 2-4），请记住选择使用 DHCP 自动获取 IP 地址设置单选按钮。还请选中从提供商自动获取 DNS 信息复选框。

### 第 3 章：添加无线以太网局域网

### 本章内容

- ✔ 了解无线以太网网络
- ✔ 设置无线硬件
- ✔ 配置无线网络

如果你的局域网中有笔记本电脑——或者如果你不想布满一堆电线来连接 PC 到局域网——你可以选择使用无线以太网网络。在典型场景中，你有通过有线调制解调器或 DSL 连接到互联网，并且你希望连接一台或多台带有无线网卡的笔记本电脑通过有线或 DSL 调制解调器访问互联网。本章展示了如何设置无线网络以连接到以太网局域网并访问互联网。

### 了解无线以太网网络

你可能听说过 Wi-Fi 网络。Wi-Fi 代表无线保真网络——一种类似于有线以太网网络的短距离无线网络。由一个名为 IEEE（电气和电子工程师学会）的组织制定的多项标准定义了 Wi-Fi 网络的工作技术细节。制造商使用这些标准来构建你可以购买以设置无线网络的组件。

直到 2003 年中期，无线以太网网络有两个流行的 IEEE 标准——802.11a 和 802.11b。这两个标准于 1999 年最终确定。第三个标准——802.11g——于 2003 年夏季由 IEEE 最终确定。所有这些标准都规定了无线以太网网络在物理层的工作方式。你不需要为设置无线网络而担心所有这些标准的全部细节，但了解一些相关细节是有益的，这样你就可以为你的无线网络购买合适的设备。

三种无线以太网标准具有以下主要特征：

- **802.11b:** 在 2.4GHz 无线电频段（2.4GHz 至 2.4835GHz）中运行，最多可使用三个不重叠的频率带或信道。支持每个信道最高 11Mbps 的比特率。802.11b 的一个缺点是 2.4GHz 频段拥挤——许多设备（如微波炉、无绳电话、医疗和科学设备以及蓝牙设备）都在 2.4GHz 频段工作。尽管如此，802.11b 在企业和家庭网络中非常流行。
- **802.11a:** 在 5GHz 无线电频段（5.725GHz 至 5.850GHz）中运行，最多可使用八个不重叠的信道。支持每个信道最高 54Mbps 的比特率。5GHz 频段不像 2.4GHz 频段那样拥挤，但 5GHz 频段在欧洲未获批准使用。符合 802.11a 标准的产品已在市场上销售，并且有设计用于处理 802.11a 和 802.11b 连接的无线接入点。
- **802.11g:** 在 2.4GHz 频段（与 802.11b 使用的相同频段）支持最高 54Mbps 的数据速率。802.11g 通过使用一种称为 OFDM（正交频分复用）的技术实现更高的比特率，该技术也用于 802.11a。尽管 802.11g 只是最近才最终确定，但符合该标准的设备已在市场上销售。这可能是因为 802.11g 在与 802.11b 相同的频段工作但承诺更高的数据速率而引起了兴奋。供应商目前提供可同时支持 802.11b 和 802.11g 连接标准的接入点。

用户看到的最大数据吞吐量要低得多，因为该无线电信道的全部用户共享该信道的容量。此外，随着用户 PC 与无线接入点之间的距离增加，数据传输速率会下降。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_349_0.png)

要了解更多关于无线以太网的信息，请访问 www.wi-fi.org，这是 Wi-Fi 联盟的主页——一个成立于 1999 年的非营利国际协会，用于认证基于 IEEE 802.11 标准的无线局域网产品的互操作性。

### 了解基础设施和自组织模式

802.11 标准为无线以太网网络定义了两种操作模式：基础设施和自组织。自组织模式仅仅是两个或多个无线以太网卡在没有接入点的情况下相互通信。

*基础设施模式是指所有无线以太网卡通过接入点相互通信并与有线局域网通信的方法。对于本书中考虑的示例，你的无线以太网卡应设置为基础设施模式。在配置文件中，此模式称为受管模式。*



## WEP 流密码足够好吗？

WEP 使用 RC4 加密算法，该算法被称为流密码。此类算法通过取一个短的密钥并生成无限的伪随机比特流来工作。在发送数据之前，发送站对伪随机比特和表示数据包的比特执行异或操作，当两个比特不同时结果为 1，相同则为 0。接收方拥有相同的密钥副本，并生成相同的伪随机比特流——并对该伪随机流和接收到的比特执行相同的异或操作。这样即可重新生成原始的未加密数据包。

这种流密码方法存在一些问题。如果加密数据流中的某一位被翻转（从 0 变为 1 或反之），则解密输出中的对应位也会被翻转——这可以帮助攻击者推导出加密密钥。此外，窃听者如果截获了两个使用相同流编码的消息，可以生成原始消息的异或结果。这一信息足以发动攻击，最终破坏加密。

为抵御这些弱点，WEP 使用了一些防御措施：

- **完整性检查 (IC) 字段** — 为确保数据包在传输过程中未被修改，WEP 在每个数据包中使用完整性检查字段。
- **初始化向量 (IV)** — 为避免用相同的密钥流加密两条消息，WEP 使用 24 位初始化向量 (IV)，该向量增强共享密钥以为每个数据包生成不同的 RC4 密钥。IV 本身也包含在数据包中。

专家表示这两种防御措施都实现不佳，导致 WEP 无效。IC 和 IV 有两个主要问题：

- **完整性检查字段**是通过使用一种称为 32 位循环冗余码 (CRC-32) 的校验和算法来实现的；该校验和随后作为数据包的一部分包含在内。不幸的是，攻击者可以翻转加密消息中的任意位并正确调整校验和，使结果消息看起来有效。
- **24 位 IV**以明文形式发送（未加密）。这意味着只有 2^24 个可能的初始化向量（对快速机器来说不是大挑战），并且在遍历完所有向量后必须重复使用。换句话说，在发送 2^24 也就是 16,777,216 个数据包后，IV 必须重复。这个数字听起来可能很多，但考虑一个繁忙的接入点以 11 Mbps 的速率发送 1,500 字节的数据包的情况。每个数据包有 8 × 1,500 = 12,000 位。这意味着接入点每秒发送 11,000,000/12,000 = 916 个数据包。以此速率，接入点在 16,777,216/916 = 18,315 秒或 5 小时内发送 16,777,216 个数据包。这意味着 IV 在 5 小时后被重复使用，而且时间可能更短，因为许多消息小于 1,500 字节。因此，攻击者有充足的机会收集两条使用相同密钥流加密的加密消息——并执行统计攻击（相当于以非常快的速度尝试可能的“组合”）来解密消息。

## 了解有线等效隐私 (WEP)

802.11 标准包含有线等效隐私 (WEP) 以保护无线通信免受窃听。WEP 依赖于 40 位或 104 位的密钥，该密钥在移动站（例如装有无线以太网卡的笔记本电脑）和接入点（也称为基站）之间共享。密钥用于在传输数据包之前对其进行加密，并执行完整性检查以确保数据包在传输过程中未被修改。802.11 标准并未说明共享密钥是如何建立的。实际上，大多数无线局域网使用单个密钥在所有移动站和接入点之间共享。然而，这种方法在大学校园等环境中扩展性不佳，因为密钥与所有用户共享——你知道如果把“秘密”与数百人共享会怎样。因此，WEP 通常不用于大学等大型无线网络。在此类无线网络中，你必须使用 SSH（安全外壳）等其他安全方法来登录远程系统。然而，WEP 在家庭无线网络中使用是合适的。

WEP 有其弱点，但总比没有好。你可以在较小的无线局域网中使用它，在这些网络中在所有无线站之间共享相同密钥并不是一项繁重的工作。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_351_0.png)

正在进行工作以提供比 WEP 更好的无线网络安全性。正在开发的 802.11i 标准将使用公钥加密和数字证书——以及在 RADIUS（远程身份验证拨入用户服务）服务器上进行的身份验证、授权和计费——为无线以太网网络提供更好的安全性。

在 802.11i 标准进行中，Wi-Fi 联盟——一个支持 Wi-Fi 的多厂商联盟——正在发布一项临时规范，称为 Wi-Fi 保护访问 (WPA)，它是 802.11i 的前身。WPA 将取代现有的 WEP 标准并通过一些更改提高安全性。例如，与 WEP（使用固定密钥）不同，WPA 标准使用临时密钥完整性协议 (TKIP)，该协议为网络上传输的每 10K 数据生成新密钥。这使得 WPA 更难被破解。在 802.11i 工作进展期间，你可能想考虑使用 WPA。

## 设置无线硬件

要设置无线连接，你需要一个无线接入点和每台 PC 中的无线网卡。你也可以在两个或更多具有无线网卡的 PC 之间设置临时无线网络，但这将是仅限于这些 PC 的独立无线局域网。本节重点介绍你想要设置到已建立的局域网的无线连接的场景，该局域网通过电缆调制解调器或 DSL 通过有线方式连接到互联网。

除了无线接入点之外，你还需要电缆调制解调器或 DSL 连接到互联网，以及如前几节所述的 NAT 路由器/集线器。图 3-1 显示了通过现有电缆调制解调器或 DSL 连接进行无线互联网访问的典型设置。

如图 3-1 所示，局域网具有有线和无线 PC。在此示例中，电缆或 DSL 调制解调器通过 NAT 路由器/集线器将局域网连接到互联网。具有无线网卡的笔记本电脑通过连接到集线器上 RJ-45 端口之一的无线接入点连接到局域网。要将台式 PC 连接到此无线网络，可以使用 USB 无线网卡（连接到 USB 端口）。

如果你尚未为电缆或 DSL 连接购买 NAT 路由器/集线器，请考虑购买带有内置无线接入点的路由器/集线器。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_352_0.png)

![](img/a7eec43a54473e95dc5ea333fecf1bd7_352_1.png)

图 3-1：
典型的有线和无线以太网局域网混合连接到互联网。

## 配置无线接入点

配置无线接入点涉及以下任务：

- 为无线网络设置名称（技术术语是 ESSID）。
- 设置无线接入点与无线网卡通信的频率或信道。接入点和卡必须使用相同的信道。
- 决定是否使用加密。
- 如果要使用加密，则设置加密密钥的位数和加密密钥的值。加密密钥的 24 位在接入点内部；你只指定剩余的位。因此，对于 64 位加密，你必须指定 40 位密钥，即 10 个十六进制数字（十六进制数字是 0 到 9 的整数或 A 到 F 的字母）。对于 128 位加密密钥，你指定 104 位，即 26 个十六进制数字。
- 设置无线网卡在连接到接入点时必须使用的访问方法。你可以选择开放访问或共享密钥。开放访问方法很典型（即使使用加密时也是如此）。
- 将无线接入点设置为在基础设施（受管）模式下运行（因为这就是你应该将无线网卡连接到现有以太网局域网的方式）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_353_0.png)

无线接入点的确切配置方法取决于品牌和型号；供应商提供配置无线接入点的说明。你通常会通过 Windows PC 上的图形客户端应用程序进行配置。如果启用加密，请记下加密密钥；你必须为每个无线网卡指定相同的密钥。

## 配置无线网络

在你的 Red Hat Linux 笔记本上，PCMCIA 或 PC 卡管理器应识别无线网卡并加载该卡的适当驱动程序。无线网卡被视为另一个以太网设备——为其分配设备名称，例如 eth0 或 eth1。如果笔记本中已有以太网卡，该卡获得 eth0 设备名称，而无线 PC 卡则成为 eth1 设备。

你必须配置某些参数才能使无线网卡与无线接入点通信。例如，你有

指定分配给接入点的无线网络名称——并且加密设置必须与接入点上的设置相匹配。您可以通过图形化的网络配置工具完成所有操作。

按以下步骤配置并激活 Red Hat Linux 系统上的无线网络连接：

- **1. 在图形登录屏幕以 root 身份登录，然后选择 主菜单→系统设置→网络。**
网络配置工具运行并显示其主窗口。
- **2. 在网络配置窗口的工具栏中单击“新建”。**
显示“添加新设备类型”窗口（见图 3-2）。
- **3. 从窗口中选择“无线连接”（图 3-2），然后单击“前进”。**
“选择无线设备”窗口出现（如图 3-3 所示）。
- **4. 从窗口中的列表中选择您的无线网卡（参见图 3-3），然后单击“前进”。**
“配置无线连接”窗口出现（见图 3-4）。
- **5. 将模式设置为“受管”，指定要连接的无线网络名称，并设置加密密钥（如有）。然后单击“前进”。**
“配置网络设置”窗口出现（见图 3-5）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_354_0.png)

图 3-2
从此窗口选择无线连接以配置无线以太网连接。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_355_0.png)

图 3-3:
从列出的设备中选择您的无线网卡。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_355_1.png)

图 3-4:
从此窗口设置无线连接的参数。

- **6. 选择获取无线网络接口 IP 地址的选项（参见图 3-5）；在做出选择后单击“前进”。**

您也可以指定静态 IP 地址（意味着 IP 地址在每次启动时不会更改），或让 Red Hat Linux 使用 DHCP 自动获取 IP 地址（一种用于从网络上的服务器获取网络配置参数（包括 IP 地址）的协议）。通常，您会选择自动获取 IP 地址的选项。

图 3-5:
从此窗口配置无线网络接口的网络设置。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_356_0.png)

“创建无线设备”窗口（图 3-6）出现，其中包含您即将创建的无线网络连接的摘要。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_356_1.png)

图 3-6:
检查有关无线连接的信息，如果信息正确则单击“应用”。

- **7. 验证图 3-6 中显示的信息是否正确，然后单击“应用”以创建无线设备。**

信息显示您正在创建的设备名称（在本例中为 eth1）。

新设备出现在网络配置窗口中（如图 3-7 所示）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_357_0.png)

图 3-7:
从此窗口激活新的无线设备。

- **8. 选择新的无线设备，然后在工具栏上单击“激活”按钮（参见图 3-7）。**

一个对话框通知您在激活无线设备之前必须保存更改，并询问您是否要继续。

- **9. 当另一个对话框提示您激活网络设备时，单击“是”，然后单击“确定”。**

如果一切顺利，无线网络在几分钟后应该可以正常运行。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_357_1.png)

网络配置工具将您的无线网络设置保存在文本文件中，其名称取决于无线网络设备名称。如果无线网络设备名称为 eth0，则配置存储在文本文件 /etc/sysconfig/network-scripts/ifcfg-eth0 中。如果无线设备名称为 eth1，则文件为 /etc/sysconfig/network-scripts/ifcfg-eth1。该配置文件包含无线网卡的各种设置。表 3-1 解释了设置的含义。下面是我笔记本电脑上 /etc/sysconfig/network-scripts/ifcfg-eth1 文件的略作修改版本：

```
USERCTL=no
PEERDNS=yes
TYPE=Wireless
DEVICE=eth0
HWADDR=00:02:2d:8c:f9:c4
BOOTPROTO=dhcp
ONBOOT=no
DHCP_HOSTNAME=
NAME=
```

```
ESSID='HOME'
CHANNEL=6
MODE=Managed
KEY=aecf-a00f-03
RATE=auto
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_358_0.png)

如果您手动编辑配置文件中的参数，请在编辑配置文件后输入以下命令以重新激活无线网络接口：

```
service pcmcia restart
```

## 表 3-1 无线以太网网络接口配置文件的设置

| 此参数 | 含义如下 |
|---|---|
| BOOTPROTO | 用于获取接口 IP 地址的协议名称。对于以太网接口应为 dhcp 或 bootp。 |
| CHANNEL | 通道号（在美国和加拿大为 1 到 14 之间）。必须与无线接入点设置的相同。在受管模式下，您无需指定通道。 |
| DEVICE | 无线以太网网络接口的设备名称（第一个接口为 eth0，第二个为 eth1，以此类推）。 |
| ESSID | 扩展服务集（ESS）标识符，也称为无线网络名称。它区分大小写，必须与为无线接入点指定的名称相同。请在单引号内提供名称（例如，'HOME'）。 |
| HWADDR | 无线网卡的硬件地址（也称为 MAC 地址）（六对以冒号分隔的十六进制数字；例如，00:02:8c:9c:c4）。该地址由无线网卡的设备驱动程序自动检测。 |
| KEY | 加密密钥；40 位密钥为 10 个十六进制数字（例如，1fdf-3de-fe），104 位密钥为 26 个十六进制数字。（密钥实际上是 64 位和 128 位，但加密算法会自动生成密钥的 24 位，因此您只需指定剩余位。） |
| MODE | 无线网卡的操作模式。对于通过无线接入点连接的典型网络，设置为 Managed。 |
| NAME | 您无线网络的昵称。如果未指定它，则使用主机名作为昵称。 |
| ONBOOT | 设置为 yes 以在启动时激活无线接口；否则设置为 no。 |

### 表 3-1（续）

| 此参数 | 含义如下 |
|---|---|
| PEERDNS | 设置为 yes 以启用接口修改系统的 /etc/resolv.conf 文件以使用从 DHCP 服务器获得的 DNS 服务器（这是提供接口 IP 地址的同一服务器）。如果将其设置为 no，则 /etc/resolv.conf 文件保持不变。 |
| RATE | 无线连接的比特率（设置为 1M、2M、5.5M、11M 或 auto 之一）。M 表示 Mbps 或每秒百万位。设置为 auto 以使用最大可能的传输速率。 |
| TYPE | 对于无线网络接口设置为 Wireless。 |
| USERCTL | 设置为 yes 时，非 root 用户可以控制设备。将其设置为 no 以便只有 root 可以控制设备。 |

![](img/a7eec43a54473e95dc5ea333fecf1bd7_359_0.png)

要检查无线网络接口的状态，请输入以下命令：

```
iwconfig
```

以下是带有无线以太网 PC 卡的 Red Hat Linux 笔记本电脑的典型输出：

```
lo          no wireless extensions.

eth0        no wireless extensions.

eth1        IEEE 802.11-DS  ESSID:"HOME"  Nickname:"localhost.localdomain"
          Mode:Managed  Frequency:2.437GHz  Access Point: 00:30:AB:06:2E:5D
          Bit Rate:11Mb/s   Tx-Power:15 dBm   Sensitivity:1/3
          Retry limit:4   RTS thr:off   Fragment thr:off
          Encryption key:AEF6-A0DF-03
          Power Management:off
          Link Quality:68/92  Signal level:-32 dBm  Noise level:-100 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:136
          Tx excessive retries:1  Invalid misc:0   Missed beacon:0
```

这里 eth1 接口指的是无线网卡。我在此编辑了加密密钥和其他一些参数，但示例输出显示了无线链路正常工作时您通常会看到的内容。




### 第 4 章：管理网络

### 本章内容

- 学习 TCP/IP 配置文件
- 检查 TCP/IP 网络
- 启动时配置网络

与 Red Hat Linux 中的几乎所有其他内容一样，TCP/IP 设置也是通过准备多个配置文件（可以用任何文本编辑器编辑的文本文件）来完成的。其中大多数配置文件位于 /etc 目录中。Red Hat 安装程序通过隐藏 TCP/IP 配置文件的细节来提供帮助。尽管如此，如果你知道文件的名称及其用途会更好，这样如果需要的话，你就可以手动编辑文件。

## 学习 TCP/IP 配置文件

运行 Red Hat 网络配置工具应该足以在你的系统上配置 TCP/IP。然而，如果你想有效地管理网络，你应该熟悉 TCP/IP 配置文件，以便在需要时可以编辑文件。（例如，如果你想检查名称服务器是否正确指定，你必须知道 /etc/resolv.conf 文件，它存储名称服务器的 IP 地址。）

表 4-1 总结了基本 TCP/IP 配置文件。我将在接下来的几节中描述这些配置文件。

表 4-1 基本 TCP/IP 网络配置文件

| 此文件 | 包含以下内容 |
|---|---|
| `/etc/hosts` | 你的本地网络的 IP 地址和主机名以及你经常访问的任何其他系统 |
| `/etc/networks` | 网络的名称和 IP 地址 |
| `/etc/host.conf` | 如何将主机名转换为 IP 地址的说明 |
| `/etc/resolv.conf` | 名称服务器的 IP 地址 |
| `/etc/hosts.allow` | 关于哪些系统可以访问你系统上的 Internet 服务的说明 |
| `/etc/hosts.deny` | 关于哪些系统必须被拒绝访问你系统上的 Internet 服务的说明 |
| `/etc/nsswitch.conf` | 如何将主机名转换为 IP 地址的说明 |

### /etc/hosts

/etc/hosts 文本文件包含本地网络的 IP 地址和主机名列表。在没有名称服务器的情况下，你系统上的任何网络程序都会查阅此文件以确定与主机名对应的 IP 地址。可以把 /etc/hosts 想象成本地电话目录，你可以在其中查找本地主机的 IP 地址（而不是电话号码）。

以下是某个系统的 /etc/hosts 文件，显示了典型局域网上其他主机的 IP 地址和名称：

```
127.0.0.1          localhost          localhost.localdomain
# Other hosts on the LAN
192.168.0.100      lnbp933
192.168.0.50       lnbp600
192.168.0.200      lnbp200
192.168.0.233      lnbp233
192.168.0.40       lnbp400
```

正如示例所示，文件中的每一行都以 IP 地址开头，后跟该 IP 地址的主机名。（任何给定的 IP 地址可以有多个主机名。）

### /etc/networks

/etc/networks 是另一个文本文件，其中包含网络的名称和 IP 地址。这些网络名称通常在路由命令 (/sbin/route) 中使用，以按名称而不是按 IP 地址指定网络。

如果你的 Linux PC 没有 /etc/networks 文件也不必惊慌。没有此文件，你的 TCP/IP 网络也能正常工作。事实上，Red Hat Linux 安装程序不会创建 /etc/networks 文件。

### /etc/host.conf

Red Hat Linux 使用一个特殊的库（即一组计算机代码）称为解析器库来获取与主机名对应的 IP 地址。/etc/host.conf 文件指定名称如何解析（即名称如何转换为数字 IP 地址）。典型的 /etc/host.conf 文件可能包含以下行：

```
order hosts, bind
multi on
```

/etc/host.conf 文件中的条目告诉解析器库使用哪些服务（以及使用顺序）来解析名称。

order 选项表示服务的顺序。示例条目告诉解析器库首先查阅 /etc/hosts 文件，然后检查名称服务器以解析名称。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_362_0.png)

使用 multi 选项来指示 /etc/hosts 文件中的主机是否可以有多个 IP 地址。具有多个 IP 地址的主机称为多宿主，因为多个 IP 地址的存在意味着主机有多个网络接口。（实际上，主机“同时生活”在多个网络中。）

### /etc/resolv.conf

/etc/resolv.conf 文件是解析器使用的另一个文本文件——该库确定主机名的 IP 地址。以下是 /etc/resolv.conf 文件的示例：

```
search mtgmry1.md.home.com
nameserver 164.109.1.3
nameserver 164.109.10.23
```

第一行告诉解析器如何搜索主机名。例如，在尝试定位主机名 myhost 时，示例中的 search 指令会导致解析器首先尝试 myhost.mtgmry1.md.home.com，然后尝试 myhost.md.home.com，最后尝试 myhost.home.com。

nameserver 行提供你域的名称服务器的 IP 地址。如果有多个名称服务器，你应该在单独的行上列出它们。它们按在文件中出现的顺序进行查询。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_362_1.png)

如果你的网络没有名称服务器，你可以安全地忽略此文件。TCP/IP 仍应能工作，即使你可能无法按名称引用主机（除 /etc/hosts 文件中列出的主机之外）。

### /etc/hosts.allow

/etc/hosts.allow 文件指定哪些主机允许使用在你的系统上运行的 Internet 服务（例如 TELNET 和 FTP）。在某些 Internet 服务启动之前会查阅此文件。只有当 hosts.allow 文件中的条目意味着请求主机被允许使用服务时，服务才会启动。

/etc/hosts.allow 中的条目采用 servername:IP address 格式，其中 server 指提供特定 Internet 服务的程序的名称，IP address 标识被允许使用该服务的主机。例如，如果你希望本地网络（网络地址为 192.168.0.0）中的所有主机都可以访问 TELNET 服务（由 in.telnetd 程序提供），请在 /etc/hosts.allow 文件中添加以下行：

```
in.telnetd:192.168.0.
```

如果你希望所有本地主机都可以访问所有 Internet 服务，你可以使用 ALL 关键字并将该行重写如下：

```
ALL:192.168.0.
```

最后，要向所有主机开放所有 Internet 服务，你可以将 IP 地址替换为 ALL，如下所示：

```
ALL:ALL
```

你也可以使用主机名代替 IP 地址。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_363_0.png)

要了解 /etc/hosts.allow 文件中条目的详细语法，请在终端窗口的 shell 提示符下输入 man hosts.allow。

### /etc/hosts.deny

此文件与 /etc/hosts.allow 正好相反——hosts.allow 指定哪些主机可以访问你系统上的 Internet 服务（例如 TELNET 和 TFTP），hosts.deny 文件标识必须被拒绝服务的主机。如果 /etc/hosts.allow 文件中没有适用于请求主机的规则，则会查阅 /etc/hosts.deny 文件。如果 hosts.deny 文件有适用于该主机的规则，则服务将被拒绝。

/etc/hosts.deny 文件中的条目与 /etc/hosts.allow 文件中的格式相同——它们采用 server:IP address 格式，其中 server 指提供特定 Internet 服务的程序的名称，IP address 标识必须不允许使用该服务的主机。

如果你已在 `/etc/hosts.allow` 文件中设置条目以允许特定主机访问，你可以在 `/etc/hosts.deny` 文件中放置以下行以拒绝所有其他主机访问你系统上的任何服务：

```
ALL:ALL
```

要了解 `/etc/hosts.deny` 文件中条目的详细语法，请在终端窗口的 shell 提示符下输入 `man hosts.deny`。

### /etc/nsswitch.conf

此文件，也称为 *名称服务开关*（NSS）文件，指定名称解析器库、NIS、NIS+ 以及本地配置文件（例如 `/etc/hosts` 和 `/etc/shadow`）等服务如何交互。

NIS 和 NIS+ 是 *网络信息服务*——另一种名称查找服务。Linux 内核的新版本使用 `/etc/nsswitch.conf` 文件来确定优先级：是本地配置文件、DNS（域名服务）等服务，还是 NIS。

例如，`/etc/nsswitch.conf` 文件中的以下 `hosts` 条目表示解析器库应首先尝试 `/etc/hosts` 文件，然后尝试 NIS+，最后尝试 DNS：

```
hosts:    files nisplus dns
```

你可以通过在终端窗口中输入 `info libc "Name Service Switch"`（包括引号）来了解有关 `/etc/nsswitch.conf` 文件的更多信息。

## 检查 TCP/IP 网络

在你配置以太网和 TCP/IP 之后（无论是在 Red Hat Linux 安装期间还是之后运行网络配置工具），你应该能够毫无问题地使用各种网络应用程序。如果遇到问题，Red Hat Linux 包含多个工具来帮助你监控和诊断问题。

### 检查网络接口

使用 `/sbin/ifconfig` 命令查看当前配置的网络接口。`ifconfig` 命令用于配置网络接口（即为网络设备关联 IP 地址）。如果不带任何命令行参数运行 `ifconfig`，该命令会显示当前网络接口的信息。以下是 `ifconfig` 的典型调用及其输出结果：


/sbin/ifconfig
eth0  Link encap:Ethernet HWaddr 02:60:8C:8E:C6:A9
      inet addr:192.168.0.5  Bcast:192.168.0.255 Mask:255.255.255.0
      UP BROADCAST NOTRAILERS RUNNING MULTICAST  MTU:1500  Metric:1
      RX packets:8104  errors:0  dropped:0  overruns:0  frame:1
      TX packets:1273  errors:0  dropped:0  overruns:0  carrier:0
      collisions:4  txqueuelen:100
      RX bytes:869342 (848.9 Kb)  TX bytes:232276 (226.8 Kb)
      Interrupt:5  Base address:0x300

lo    Link encap:Local Loopback
      inet addr:127.0.0.1  Mask:255.0.0.0
      UP LOOPBACK RUNNING  MTU:16436  Metric:1
      RX packets:94  errors:0  dropped:0  overruns:0  frame:0
      TX packets:94  errors:0  dropped:0  overruns:0  carrier:0
      collisions:0  txqueuelen:0
      RX bytes:6184 (6.0 Kb)  TX bytes:6184 (6.0 Kb)

此输出显示，当前系统上有两个网络接口处于活动状态——回环接口（lo）和以太网卡（eth0）。对于每个接口，都可以看到 IP 地址，以及发送和接收数据包的统计信息。如果 Red Hat Linux 系统上有拨号 PPP 链接正在运行，则输出中还会看到 ppp0 接口的条目。

## 检查 IP 路由表

另一个网络配置命令 /sbin/route，在不带任何命令行参数运行时也会提供状态信息。如果您在检查到另一个主机（使用 IP 地址指定）的连接时遇到问题，请检查 IP 路由表，查看是否指定了默认网关。然后检查网关的路由表，以确保通往外部网络的路径出现在该路由表中。

/sbin/route 命令的典型输出如下：

/sbin/route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
192.168.0.0     *               255.255.255.0   U     0      0      0     eth0
127.0.0.0       *               255.0.0.0       U     0      0      0     lo
default         192.168.0.1     0.0.0.0         UG    0      0      0     eth0

如该路由表所示，本地网络使用 eth0 以太网接口，默认网关也是该以太网接口。默认网关是处理发往 Red Hat Linux 系统所在网络以外任何网络的数据包的路由设备。在此示例中，发往除以 192.168.0 开头的网络地址之外的任何网络地址的数据包都会发送到网关——192.168.0.1。网关会将这些数据包转发到其他网络（当然，前提是网关已连接到另一个网络，最好是 Internet）。

## 检查主机连通性

要检查到特定主机的网络连接，请使用 ping 命令。ping 命令是广泛使用的 TCP/IP 工具，它使用一系列 Internet 控制消息协议（ICMP，读作 eye-comp）消息。ICMP 提供了 Echo 消息，每台主机都会对其作出响应。利用 ICMP 消息和回复，ping 可以确定另一系统是否存活，并计算与该系统通信的往返延迟。

以下示例展示了我如何运行 ping 来查看网络上的系统是否存活：

```
ping 192.168.0.1
```

这是在我的家庭网络上该命令的显示内容：

```
PING 192.168.0.1 (192.168.0.1) from 192.168.0.7: 56(84) bytes of data.
64 bytes from 192.168.0.1: icmp_seq=1 ttl=254 time=1.36 ms
64 bytes from 192.168.0.1: icmp_seq=2 ttl=254 time=1.23 ms
64 bytes from 192.168.0.1: icmp_seq=3 ttl=254 time=1.36 ms
64 bytes from 192.168.0.1: icmp_seq=4 ttl=254 time=1.34 ms

--- 192.168.0.1 ping statistics ---
4 packets transmitted, 4 received, 0% loss, time 3026ms
rtt min/avg/max/mdev = 1.338/1.352/1.366/0.038 ms
```

在 Red Hat Linux 中，ping 会一直运行，直到您按 Ctrl-C 停止它；然后它会显示摘要统计信息，显示在两个系统之间发送数据包的典型时间。在某些系统上，ping 只是报告远程主机是否存活。但是，您仍可使用适当的命令行参数获取时序信息。

## 检查网络状态

要检查网络状态，请使用 netstat 命令。该命令显示各种类型网络连接的状态（例如 TCP 和 UDP 连接）。可使用 netstat -i 快速查看接口状态，如下所示：

netstat -i
Kernel Interface table
Iface MTU Met RX-OK RX-ERR RX-DRP RX-OVR TX-OK TX-ERR TX-DRP TX-OVR Flg
eth0 1500 0 1678 0 0 0 651 0 0 0 BMNRU
lo 16436 0 50 0 0 0 50 0 0 0 LRU

在此情况下，输出显示了回环和以太网接口的当前状态。表 4-2 描述了各列的含义。

**表 4-2 内核接口表中各列的含义**

| 列 | 含义 |
|---|---|
| Iface | 接口名称 |
| MTU | 最大传输单元 — 数据包可包含的最大字节数 |
| RX-OK, TX-OK | 接收（RX）或发送（TX）的无错误数据包数量 |
| RX-ERR, TX-ERR | 带有错误的数据包数量 |
| RX-DRP, TX-DRP | 被丢弃的数据包数量 |
| RX-OVR, TX-OVR | 因溢出而丢失的数据包数量 |
| Flg | A = 接收多播；B = 允许广播；D = 调试已打开；L = 回环接口（注意 `lo` 上的标志）；M = 接收所有数据包，N = 避免尾部；O = 此接口上无 ARP，P = 点对点接口；R = 接口正在运行；U = 接口已启动。 |

netstat 的另一个有用选项形式是 -t，它显示所有活动的 TCP 连接。以下是某台 Red Hat Linux PC 上 netstat -t 的典型结果：

```
netstat -t
Active Internet connections (w/o servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp   0    0 dhcpcp4:1031    www.redhat.com:http     ESTABLISHED
tcp   0    126 dhcpcp4:telnet  192.168.0.6:1238        ESTABLISHED
tcp   0    0 dhcpcp4:1032    www.redhat.com:https    ESTABLISHED
tcp   0    0 dhcpcp4:1033    www.redhat.com:https    ESTABLISHED
tcp   0    0 dhcpcp4:telnet  192.168.0.6:1238        ESTABLISHED
tcp   0    0 dhcpcp4:ftp     192.168.0.6:1548        TIME_WAIT
```

在此情况下，输出列显示协议（Proto）；接收和发送队列中的字节数（Recv-Q、Send-Q）；本地 TCP 端口，格式为主机名:服务（Local Address）；远程端口（Foreign Address）；以及连接状态。

输入 netstat -la 可查看所有 TCP 连接——包括活动连接以及 Red Hat Linux 系统正在监听但尚未建立连接的连接。例如，以下是 netstat -ta 命令的典型输出：

```
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp   0    0 *:1024                *:*                     LISTEN
tcp   0    0 localhost.localdom:1025 *:*                     LISTEN
tcp   0    0 *:sunrpc              *:*                     LISTEN
tcp   0    0 *:x11                 *:*                     LISTEN
tcp   0    0 *:ftp                 *:*                     LISTEN
tcp   0    0 *:ssh                 *:*                     LISTEN
tcp   0    0 *:telnet              *:*                     LISTEN
```

```
tcp 0 0 localhost.localdom:smtp *: * LISTEN
tcp 0 138 dhcppc3:telnet dhcppc4:1037 ESTABLISHED
tcp 0 0 dhcppc3:ftp dhcppc4:1060 ESTABLISHED
```

## 嗅探网络数据包

嗅探网络数据包——听起来像是非法行为，对吧？并非如此。嗅探只是指查看 TCP/IP 网络数据包。概念是捕获所有网络数据包以便稍后检查。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_368_0.png)

如果您想嗅探 TCP/IP 数据包，可以使用 tcpdump，这是一个随 Red Hat Linux 提供的命令行实用程序。顾名思义，它会“转储”（打印）TCP/IP 网络数据包的头部。

要使用 tcpdump，请以 root 身份登录并在终端窗口中输入 tcpdump 命令。通常，您希望将输出保存到文件中以便稍后检查。否则，tcpdump 会开始输出结果，瞬间闪过窗口。例如，要捕获 1,000 个数据包到名为 tdout 的文件中并尝试将 IP 地址转换为名称，请输入以下命令：

```
tcpdump -a -c 1000 > tdout
```

捕获 1,000 个数据包后，tcpdump 会退出。然后您可以检查输出文件 tdout。它是一个文本文件，因此您可以直接在文本编辑器中打开它，或输入 more tdout 来查看捕获的数据包。

为了满足您的好奇心，以下是 tcpdump 典型输出中的几行：

```
20:39:56.929241 dhcppc3.telnet > 192.168.0.6.4272: P 3225722544:3225722572(28)
 ack 1449012018 win 5840 (DF) [tos 0x0]
20:39:57.120308 192.168.0.6.4272 > dhcppc3.telnet: . ack 28 win 16199 (DF)
20:39:57.155930 arp who-has 192.168.0.1 tell dhcppc6
20:39:57.166515 arp reply 192.168.0.1 is at 0:0:c5:e1:3e:ae
20:39:57.169596 dhcppc6.1025 > 192.168.0.1.domain: 33598+ PTR? 6.0.168.192.in-addr.arpa. (42) (DF)
20:39:57.838984 192.168.0.1.domain > dhcppc6.1025: 33598 NXDomain* 0/1/0 (119) (DF)
20:39:57.840892 dhcppc6.1025 > 192.168.0.1.domain: 33599+ PTR? 1.0.168.192.in-addr.arpa. (42) (DF)
20:39:57.885757 192.168.0.1.domain > dhcppc6.1025: 33599 NXDomain 0/1/0 (119) (DF)
20:40:05.513863 192.168.0.1.router > 192.168.0.255.router: RIPV1-resp [items 2]:
 (0.0.0.0)(1) [68.49.48.0](1) [ttl 1]
... lines deleted...
```

输出确实提供了一些线索——每一行显示一个网络数据包的信息。每一行以时间戳开头，后跟数据包的详细信息，例如其来源和去向。我不会在这里尝试解释细节，但您可以输入

![](img/a7eec43a54473e95dc5ea333fecf1bd7_369_0.png)

使用 man tcpdump 可以了解更多细节（更重要的是，看看 tcpdump 还能用于哪些其他方式）。

Red Hat Linux 还附带了另一个名为 Ethereal 的数据包嗅探器。要了解有关 Ethereal 的更多信息，请访问 www.ethereal.com 并查阅位于 /usr/share/doc/ethereal* 目录中的文档（输入 ls /usr/share/doc/ethereal* 以查看该目录的内容）。

## 启动时配置网络

您希望每次启动系统时网络都能自动启动。为此，各种启动脚本必须包含适当的命令。除了配置网络（在安装期间或稍后使用 Red Hat 网络配置工具）之外，您无需做任何特别的事情。但是，如果网络在启动时出现问题，您可以通过检查本节中提到的文件进行故障排除。

为了初始化网络，网络激活脚本使用 /etc/sysconfig 目录中的一组文本文件。例如，脚本会检查 /etc/sysconfig/network 文件中定义的变量以决定是否激活网络。在 /etc/sysconfig/network 中，您应该看到如下包含 NETWORKING 变量的行：

```
NETWORKING=yes
```

只有当 NETWORKING 变量设置为 yes 时，网络才会被激活。

/etc/sysconfig/network-scripts 目录中的多个脚本激活特定的网络接口。例如，用于激活以太网接口 eth0 的配置文件是 /etc/sysconfig/network-scripts/ifcfg-eth0 文件。下面是一个典型的 /etc/sysconfig/network-scripts/ifcfg-eth0 文件的内容：

```
DEVICE=eth0
BOOTPROTO=dhcp
ONBOOT=yes
```

DEVICE 行提供网络设备名称。BOOTPROTO 变量设置为 dhcp，表示使用动态主机配置协议（DHCP）动态获取 IP 地址，这是一种标准方法。ONBOOT 变量表示 Red Hat Linux 启动时是否应激活此网络接口。如果您的 PC 具有以太网卡并且您希望在启动时激活 eth0 接口，则必须将 ONBOOT 设置为 yes。

当然，/etc/sysconfig/network-scripts 目录中的 ifcfg-eth0 配置文件仅在您的 PC 具有以太网卡并且 Linux 内核已检测到并加载了该卡的特定驱动程序时才有效。

## 第五卷

## 互联网

### 第五波

作者 Rich Tennant

![](img/a7eec43a54473e95dc5ea333fecf1bd7_370_0.png)

“ 我并不是说我相信任何东西。我只知道自从它出现后，我们的服务器运行速度提高了 50%。”

## 一目了然的内容

- 第 1 章：交换电子邮件和即时消息 ........................345
- 第 2 章：使用网络 ........................359
- 第 3 章：阅读新闻组....................379
- 第 4 章：使用 FTP 传输文件 ........................389

### 第 1 章：交换您的电子邮件和即时消息

### 本章内容

- 了解电子邮件
- 盘点邮件阅读器和 IM（即时消息）客户端
- 使用 Ximian Evolution
- 使用 Mozilla Mail
- 使用 Gaim 进行即时消息

电子邮件（e-mail）是互联网的支柱。电子邮件很棒，因为您可以与互联网上的任何人交换消息和文档。人们使用互联网最常见的方式之一就是通过电子邮件与朋友、熟人、亲人和陌生人保持联系。您可以向远在千里之外的朋友发送消息，并在几分钟内收到回复。基本上，您可以从互联网主机向世界任何地方发送消息，而该消息通常会在几分钟内到达目的地——这是使用纸质邮件（也称为蜗牛邮件，很贴切）无法做到的。

我喜欢电子邮件，因为我可以在不必玩“电话追逐”游戏的情况下进行交流，在这种游戏中，两人互相留言却无法成功联系。当我发送电子邮件时，它会留在收件人的邮箱中，等待收件人在方便时阅读。我想我更喜欢相反的情况——当人们给我发电子邮件时，我可以在方便时阅读和回复。

Red Hat Linux 附带了多个可以从您的互联网服务提供商（ISP）下载邮件的邮件客户端。您也可以使用这些邮件客户端阅读和发送电子邮件。在本章中，我提到了 Red Hat Linux 中可用的大多数邮件客户端并描述了其中一些。并且当您熟悉其中一个后，就很容易使用任何邮件阅读器。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_372_0.png)

还有另一种“保持联系”的方式，更符合当今青少年的习惯。我说的是 IM——即时消息。IM 基本上是一对一聊天，Red Hat Linux 包含 AOL 即时消息（或 AIM）的 IM 客户端。我在本章中简要介绍 AIM 客户端。

## 了解电子邮件

电子邮件消息发送到主机上的用户名（host 只是在线计算机的花哨名称）。这意味着如果 John Doe 使用用户名 jdoe 登录，发给他的电子邮件地址就是 jdoe。唯一需要的信息来唯一标识收件人的是收件人系统的完全限定域名。因此，如果 John Doe 的系统名为 someplace.com，他的完整电子邮件地址就变成 jdoe@someplace.com。只要有该地址，互联网上的任何人都可以向 John Doe 发送电子邮件。

### MUA 和 MTA 如何工作

有两种类型的邮件软件：

- **邮件用户代理（MUA）**是邮件阅读器的花哨名称——您用来阅读邮件消息、撰写回复和编写新消息的客户端。通常，邮件用户代理使用 POP3 或 IMAP4 协议从邮件服务器检索消息。POP3 是邮局协议版本 3，IMAP4 是互联网消息访问协议版本 4。Red Hat Linux 附带了 Balsa、Mozilla Mail、KMail 和 Ximian Evolution 等邮件用户代理。
- **邮件传输代理（MTA）**是实际发送和接收邮件消息文本的邮件服务器的花哨名称。邮件传输所使用的方法取决于底层网络。在 TCP/IP 网络中，邮件传输代理使用简单邮件传输协议（SMTP）投递邮件。Red Hat Linux 包含 sendmail，这是一款功能强大且流行的 TCP/IP 网络邮件传输代理。

图 1-1 显示了当 Alice 向 Bob 发送电子邮件时，MUA 和 MTA 如何相互工作。（如果您不知道，通常使用 Alice 和 Bob 来解释电子邮件和密码学——随便拿起一本密码学书籍您就会明白我的意思）。您可能已经知道这一点，但互联网总是被绘制成云——互联网的边界如此模糊，以至于云似乎正好可以代表它（或者是因为没人知道它从哪里开始、在哪里结束？）。

图 1-1 中的场景是大多数人的典型情况。Alice 和 Bob 都通过 ISP 连接到互联网，并通过他们的 ISP 获取和发送电子邮件。当 Alice 输入消息并发送时，她的邮件用户代理（MUA）使用简单邮件传输协议（SMTP）将消息发送到她 ISP 的邮件传输代理（MTA）。发送的 MTA 然后使用 SMTP 将该消息发送到接收 MTA——Bob 的 ISP 的 MTA。当 Bob 连接到互联网时，他的 MUA 使用 POP3（或 IMAP4）协议从他 ISP 的 MTA 下载消息。这就是邮件在互联网上移动的方式——从发送 MUA 到发送 MTA 到接收 MTA 到接收 MUA。

图 1-1：
Alice 如何向 Bob 发送电子邮件（或关于 MUA 和 MTA 的全部内容）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_374_0.png)

### 邮件消息增强

邮件消息过去是纯文本（大多数仍然是），但今天的许多消息包含的内容远不止文本。今天邮件的两个典型新功能是

- **附件：** 今天的许多消息都包含附件文件，可以是文档到图像的任何内容。收件人可以将附件保存到磁盘或直接从邮件阅读器打开。不幸的是，这是黑客试图将病毒和蠕虫带入您的 PC 的一种方式。（如果这能安慰您的话，大多数基于 Windows 的病毒和蠕虫在 Red Hat Linux 中不起作用。）
- **HTML 消息：** 邮件消息可以用 HTML（超文本标记语言）编写，这是用于布局网页的语言。当您在功能强大的邮件阅读器上阅读 HTML 消息时，消息会以其全部风采呈现，带有漂亮的字体和嵌入式图形。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_374_1.png)

虽然 HTML 消息很不错，但在使用基于文本的邮件阅读器时它们不会正确显示。在文本邮件阅读器中，HTML 消息显示为一堆乱码（这只是 HTML 代码）。



![](img/a7eec43a54473e95dc5ea333fecf1bd7_375_0.png)

如果你有一个 ISP 账户，你只需要一个邮件客户端（请原谅我，邮件用户代理）来访问你的电子邮件。在这种情况下，你的电子邮件存储在你的 ISP 服务器上，邮件阅读器在你运行它时下载邮件。在你开始从 ISP 邮件服务器读取邮件之前，你必须进行一些设置。设置本质上需要你输入从 ISP 获得的信息——邮件服务器的名称、服务器类型（例如 POP3）、你的用户名和你的密码。

## Red Hat Linux 中邮件阅读器和 IM 客户端的盘点

过去大多数邮件阅读器都是文本程序，但时代变了。现在邮件阅读器是图形应用程序，能够轻松显示 HTML 消息并处理附件。它们易于使用。如果你会用一个，你就可以使用任何图形邮件阅读器。Red Hat Linux 附带了多个邮件阅读器。

IM（即时消息）是更近期的现象，但 Red Hat Linux 努力紧跟潮流，因此它附带了两个 AOL IM 客户端。表 1-1 为你提供了 Red Hat Linux 中邮件阅读器和 IM 客户端的概览。

| 表 1-1 | Red Hat Linux 邮件阅读器和 AIM 客户端 |
|---|---|
| 软件 | 描述 |
| KMail | 支持 POP3 和 IMAP 的 KDE 邮件客户端 |
| Mozilla Mail | 邮件客户端和新闻阅读器，是 Mozilla 开源网页浏览器的一部分（Netscape Communicator 的开源版本） |
| Ximian Evolution | 个人信息管理器（PIM），包括电子邮件、日历、联系人管理和在线任务列表 |
| Gaim | GNOME 的 IM 客户端，支持多种即时消息协议，如 AOL IM、ICQ、Yahoo!、MSN、Gadu-Gadu 和 Jabber |
| Kit | KDE 的 AOL IM 客户端 |

## 使用 Ximian Evolution

我听说过很多关于 Ximian Evolution 的事情，我想从它开始。有什么比直接上手更好的方法呢！

从 GNOME 或 KDE 桌面选择 主菜单→Internet→Evolution 邮件。如果这是你第一次使用 Evolution，Evolution 设置向导会启动（见图 1-2）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_376_0.png)

图 1-2：
Evolution Setup Assistant 引导你完成初始设置。

在欢迎屏幕中单击“前进”，设置向导会引导你完成以下步骤：

- 1. **在“身份”屏幕中输入你的姓名和电子邮件地址并单击“前进”。**
  例如，如果你的电子邮件地址是 `joe@someplace.com`，那就是你输入的内容。你还可以指定一个签名文件——一个文本文件，其内容会被附加到你发送的每条消息中。通常，你会把你的姓名和联系信息放在签名文件中。
  
- 2. **设置接收电子邮件的选项并单击“前进”。**
  选择邮件下载协议的类型——POP 或 IMAP。然后提供邮件服务器的名称（例如，`mail.comcast.net`）。Evolution 第一次连接到邮件服务器时，会提示你输入密码。
  
- 3. **提供有关接收电子邮件的进一步信息——多久检查一次邮件以及是否将邮件保留在服务器上——然后单击“前进”。**
  通常，你希望下载邮件并将其从服务器删除（否则当你的邮件堆积时 ISP 会抱怨）。
  
- 4. **设置发送电子邮件的以下选项，完成后再单击“前进”：**
  - 选择服务器类型为 SMTP。
  - 输入服务器名称，例如 `smtp.comcast.net`。
  - 如果服务器要求你登录，请选中“服务器需要身份验证”复选框。
  - 输入你的用户名——这与登录 ISP 邮件服务器时使用的用户名相同。（通常发送邮件时无需登录；你只在接收——下载——邮件消息时才登录。）

- 5. 指定是否要将此电子邮件账户设为默认账户，并如需的话为此邮件账户指定一个描述性名称；单击“前进”。
- 6. 通过单击地图设置你的时区；单击“前进”。
- 7. 单击“应用”完成 Evolution 设置。

完成设置后，Evolution 打开其主窗口（见图 1-3）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_377_0.png)

图 1-3：Evolution 处理邮件、日历、联系人管理和待办事项。

主显示区域垂直分为两个窗口：左侧较窄的快捷方式窗口（带有一系列快捷方式图标），以及更大的窗口，在该窗口中 Evolution 显示与当前选定快捷方式相关的信息。

最初，Evolution 显示一个汇总视图，显示有关你的邮件、约会和任务的信息，以及其他有用信息，如天气。默认情况下，Evolution 最初显示的是美国马萨诸塞州波士顿的天气。

汇总视图中你看到的一些信息来自网页链接。例如，Red Hat 勘误列表来自 Red Hat 网站。

你可以单击左侧窗口中的图标来切换到不同的视图。表 1-2 描述了单击 Evolution 快捷方式窗口中的五个快捷方式图标时发生的情况。

表 1-2 Ximian Evolution 中的快捷方式图标

| 图标外观 | 图标名称 | 其作用 |
|---|---|---|
| [icon] | Summary | 显示所有信息的汇总视图——邮件、日历、任务和其他一些信息。 |
| [icon] | Inbox | 显示收件箱内容，可在此阅读邮件和发送邮件。 |
| [icon] | Calendar | 打开你的日历，可在此查找和添加约会 |
| [icon] | Tasks | 显示你的任务（“待办”）列表，可在此添加新任务并查看何时到期。 |
| [icon] | Contacts | 打开你的联系人列表，可在此添加新联系人或从当前列表中查找某人。 |

正如表 1-2 中的按钮所示，Ximian Evolution 具有 PIM 的所有必要组件——电子邮件、日历、任务列表和联系人。

要在 Evolution 中访问你的电子邮件，请单击“收件箱”图标。Evolution 打开你的收件箱（见图 1-4）。如果你已打开定期自动检查邮件的功能，Evolution 已经会提示你输入邮件密码并下载你的邮件。电子邮件收件箱看起来与任何其他邮件阅读器的收件箱非常相似，例如 Outlook Express 收件箱。

要阅读一条消息，请在收件箱的上部窗口中单击该消息，消息文本会出现在下部窗口中。

要回复当前消息，请单击工具栏上的“回复”按钮。消息撰写窗口会弹出（见图 1-5）。你可以撰写回复，然后单击工具栏上的“发送”按钮发送回复。简单，不是吗？

![](img/a7eec43a54473e95dc5ea333fecf1bd7_379_0.png)

图 1-4：
在 Evolution 收件箱中阅读你的电子邮件。

要发送新电子邮件，请单击 Evolution 工具栏上的“新建邮件”按钮。会出现一个新的消息撰写窗口，你可以在其中输入消息；然后单击“发送”。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_379_1.png)

图 1-5：
在此窗口中撰写回复，然后单击“发送”按钮。

Ximian Evolution 附带了广泛的在线帮助。从 Evolution 菜单中选择 帮助→目录，A User's Guide to Ximian Evolution 会在 Mozilla 窗口中出现。然后你可以在 Mozilla 网页浏览器中阅读用户指南。

## 使用 Mozilla Mail

Mozilla Mail 是随 Mozilla 一起提供的邮件和新闻阅读器——Netscape Communicator 的开源继任者。Mozilla 是一个网页浏览器，也包括邮件和新闻阅读器。

要使用 Mozilla Mail，首先运行 Mozilla 网页浏览器。单击面板上的 Mozilla 图标（被鼠标线套住的地球），Mozilla 网页浏览器窗口会出现。要访问 Mozilla Mail 邮件和新闻阅读器，请从菜单中选择 窗口→邮件和新闻组。Mozilla Mail 运行，启动“账户向导”（见图 1-6），并提示你输入有关电子邮件账户的信息。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_380_0.png)

图 1-6
向 Mozilla Mail 的账户向导提供你的电子邮件账户信息。

选择“电子邮件账户”单选按钮并单击“下一步”。账户向导随后会引导你完成以下步骤：

- 1. 输入你的身份信息——你的姓名和完整的电子邮件地址，例如 joe@someplace.com——然后单击“下一步”。
- 2. 提供 ISP 邮件服务器的信息——协议类型（POP 或 IMAP）以及收件和发件服务器名称——然后单击“下一步”。




The incoming server is the POP or IMAP server, whereas the outgoing server is the one through which you send mail out (it's the SMTP server).

接收服务器是 POP 或 IMAP 服务器，而发送服务器则是你用来发送邮件的服务器（它是 SMTP 服务器）。

3. **Enter the username that your ISP has given you; click Next.**

3. **输入你的 ISP 提供的用户名；点击下一步。**

4. **Enter a name that you want to use to identify this account and click Next.**

4. **输入你想要用来标识此账户的名称，然后点击下一步。**

This is just for Mozilla Mail, so you can pick anything you want like “My home account.”

这只是用于 Mozilla Mail，所以你可以随意选择，例如“我的家庭账户”。

The Account Wizard then displays a summary of the information you entered.

账户向导随后会显示你输入的信息摘要。

5. **Verify the information; if it's correct, click Finish. Otherwise click Back and fix the errors.**

5. **核实信息；如果正确，点击完成。否则点击返回并修正错误。**

After you set up the e-mail account, the Mozilla Mail main window appears and shows you the contents of your inbox. Soon a dialog box pops up and asks you for your e-mail password. Mozilla Mail needs this to download your e-mail messages from your ISP. Enter your password and click OK.

设置好电子邮件账户后，Mozilla Mail 主窗口会出现并显示你的收件箱内容。不久一个对话框会弹出，要求你输入电子邮件密码。Mozilla Mail 需要此密码来从你的 ISP 下载电子邮件。输入密码并点击确定。

Mozilla Mail downloads your messages and displays them in a familiar format. To read a message, click that message, and the full text appears in the lower window (as shown in Figure 1-7).

Mozilla Mail 下载你的邮件并以熟悉的格式显示。要阅读邮件，点击该邮件，完整文本会出现在下部窗口中（如图 1-7 所示）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_381_0.png)

Figure 1-7:
You can read and send e-mail messages and a whole lot more from Mozilla Mail.

Figure 1-7:
你可以使用 Mozilla Mail 阅读和发送电子邮件以及更多功能。

Mozilla Mail is intuitive to use. Most of the time you can click the toolbar buttons to do most anything you want to do with the e-mail messages. Here's what each toolbar button does:

Mozilla Mail 使用直观。大多数情况下，你可以点击工具栏按钮来执行几乎所有想要对电子邮件进行的操作。以下是每个工具栏按钮的功能：

- **Get Msgs:** Downloads messages from your e-mail accounts (you can set up as many as you want).
- **获取邮件：** 从你的电子邮件账户下载邮件（你可以设置任意多个）。
- **Compose:** Opens a window where you can compose and send a message.
- **撰写：** 打开一个窗口，可在其中撰写并发送邮件。
- **Reply:** Opens a window where you can send back a reply to the person who sent you the message you are reading now.
- **回复：** 打开一个窗口，可向当前正在阅读的邮件的发送者发送回复。
- **Reply All:** Opens a window for sending a reply to everyone who was on the addressee list of the message you are reading now.
- **回复全部：** 打开一个窗口，可向当前正在阅读的邮件的收件人列表中的所有人发送回复。
- **Forward:** Brings up the current message in a window so that you can forward it to someone else.
- **转发：** 在窗口中调出当前邮件，以便你可以将其转发给他人。
- **File:** Files selected messages in folders.
- **归档：** 将选定的邮件归档到文件夹中。
- **Next:** Shows the next unread message.
- **下一个：** 显示下一封未读邮件。
- **Delete:** Deletes the selected message.
- **删除：** 删除选定的邮件。
- **Print:** Prints the message you are reading now.
- **打印：** 打印当前正在阅读的邮件。
- **Stop:** Stops the current message transfer.
- **停止：** 停止当前邮件传输。

If you use any GUI mail reader — from Microsoft Outlook Express to Novell GroupWise — you should find a similar set of toolbar buttons. In the following sections, I describe how to perform a few common e-mail-related tasks.

如果你使用任何 GUI 邮件阅读器——从 Microsoft Outlook Express 到 Novell GroupWise——你应该会发现类似的一组工具栏按钮。在以下章节中，我将描述如何执行一些常见的电子邮件相关任务。

## Managing your inbox

## 管理你的收件箱

Mozilla Mail downloads your incoming mail and stores it in the inbox folder. You can see the folders organized along the narrow window on the left side (refer to Figure 1-7). There's a set of folders for each e-mail account you have set up. You have the following folders by default:

Mozilla Mail 下载你的来信并将其存储在收件箱文件夹中。你可以在左侧窄窗口中看到组织好的文件夹（参见图 1-7）。每个你设置的电子邮件账户都有一组文件夹。你默认拥有以下文件夹：

- **Inbox:** Holds all of your incoming messages for this e-mail account.
- **收件箱：** 保存此电子邮件账户的所有来信。
- **Drafts:** Contains the messages that you saved as drafts (click the Save button on the message composition window).
- **草稿：** 包含你保存为草稿的邮件（在邮件撰写窗口中点击保存按钮）。
- **Templates:** Contains the messages you saved as templates.
- **模板：** 包含你保存为模板的邮件。
- **Sent:** Holds all the messages you have sent.
- **已发送：** 保存你发送过的所有邮件。
- **Trash:** Contains the messages you have deleted (to empty the Trash folder, choose File→Empty Trash from the Mozilla Mail menu).
- **垃圾箱：** 包含你已删除的邮件（要清空垃圾箱文件夹，请从 Mozilla Mail 菜单中选择文件→清空垃圾箱）。

You can create other folders to better organize your mail. To create a folder, do the following:

你可以创建其他文件夹以更好地组织邮件。要创建文件夹，请执行以下操作：

- 1. Choose File→New→Folder.
- 1. 选择文件→新建→文件夹。
- 2. Fill in the folder name and select where you want to put the folder (Figure 1-8); then click OK.

2. 填写文件夹名称并选择要放置文件夹的位置（图 1-8）；然后点击确定。

The New Folder dialog box appears.

新建文件夹对话框出现。

The new folder appears in the left window of Mozilla Mail.

新文件夹出现在 Mozilla Mail 的左侧窗口中。

Figure 1-8:
You can create new folders to organize your mail messages in Mozilla Mail.

Figure 1-8:
你可以在 Mozilla Mail 中创建新文件夹来组织你的邮件。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_383_0.png)

When you select a folder from the left window, Mozilla Mail displays the contents of that folder in the upper window on the right side. The list is normally sorted by date, with the latest messages shown at the end of the list. If you want to sort the list any other way — say, by sender or by subject — simply click that column heading and Mozilla Mail sorts the list according to that column.

当你从左侧窗口选择一个文件夹时，Mozilla Mail 会在右侧的上部窗口中显示该文件夹的内容。列表通常按日期排序，最新的邮件显示在列表末尾。如果你想以其他方式排序列表——比如按发件人或按主题——只需点击该列标题，Mozilla Mail 就会按该列对列表进行排序。

## Composing and sending messages

## 撰写和发送邮件

To send an e-mail message, you either write a new message or reply to a message you are reading. The general steps for sending an e-mail message are as follows:

要发送电子邮件，你可以撰写新邮件或回复正在阅读的邮件。发送电子邮件的一般步骤如下：

- 1. To reply to a message, click the Reply or Reply All button on the toolbar as you are reading the message. To write a new message, click the Compose button on the toolbar. To forward a message, click the Forward button.

- 1. 要回复邮件，在阅读邮件时点击工具栏上的回复或回复全部按钮。要撰写新邮件，点击工具栏上的撰写按钮。要转发邮件，点击转发按钮。

A message composition window appears (as shown in Figure 1-9).

邮件撰写窗口出现（如图 1-9 所示）。

- 2. In the message composition window, type your message.

- 2. 在邮件撰写窗口中，输入你的邮件内容。

The message can include links to Web sites and images. To insert any of these items, choose Insert→Link or Insert→Image from the menu.

邮件可以包含网站链接和图片。要插入这些项目，请从菜单中选择插入→链接或插入→图片。

- 3. If it's a new message or a forwarded message, also type the e-mail addresses of the recipients.

- 3. 如果是新邮件或转发邮件，还需输入收件人的电子邮件地址。

To select addressees from the Address Book, click the Address button on the toolbar. This opens up your Address Book, from which you can select the addressees.

要从地址簿中选择收件人，点击工具栏上的地址按钮。这将打开你的地址簿，从中你可以选择收件人。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_384_0.png)

Figure 1-9:
Compose your message and then enter the addresses of the recipients.

Figure 1-9:
撰写你的邮件然后输入收件人地址。

- 4. **After preparing and addressing the message, click the Send button.**
  Mozilla Mail asks whether you want to send the message in HTML format or plain text or both.
- 4. **准备并填写好邮件后，点击发送按钮。**
  Mozilla Mail 会询问你是否要以 HTML 格式、纯文本格式或两者都发送邮件。
- 5. **Select a format and then click Send to send the message.**
  If you've inserted images and Web links and you know the recipient can read HTML mail, be sure to select HTML format; otherwise, choose plain text.

- 5. **选择格式然后点击发送以发送邮件。**
  如果你插入了图片和网页链接并且知道收件人可以阅读 HTML 邮件，请务必选择 HTML 格式；否则，选择纯文本。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_384_1.png)

If you want to complete a message later, click Save in the message composition window and then close the window. Mozilla Mail saves the message in the Drafts folder. When you're ready to work on that message again, go to the Drafts folder and then double-click the saved message to open it.

如果你想稍后完成邮件，点击邮件撰写窗口中的保存然后关闭窗口。Mozilla Mail 会将邮件保存在草稿文件夹中。当你准备好再次处理该邮件时，进入草稿文件夹然后双击保存的邮件打开它。

## Instant Messaging with Gaim

## 使用 Gaim 进行即时消息

You can use Gaim to keep in touch with all of your buddies on AOL Instant Messenger (or AIM, as it's commonly known). If you use AOL's AIM, you'll be right at home with Gaim, a client for the AOL AIM service.

你可以使用 Gaim 与 AOL 即时通讯器（或称 AIM）上的所有好友保持联系。如果你使用 AOL 的 AIM，你会觉得 Gaim 很熟悉，Gaim 是 AOL AIM 服务的客户端。

Start Gaim by choosing Main Menu→Internet→Instant Messenger from the GNOME desktop. The initial Gaim window appears (Figure 1-10).

从 GNOME 桌面选择主菜单→互联网→即时通讯器启动 Gaim。初始 Gaim 窗口出现（图 1-10）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_385_0.png)

Figure 1-10:
Sign on to AIM with Gaim.

Figure 1-10:
使用 Gaim 登录 AIM。

If you've used AIM before, you already have a screen name. Just type it in, enter the password, and then click Sign On. Gaim logs you in and opens the standard Buddy List window. The Buddy List is initially empty. To add buddies, choose Buddies→Add a Buddy. In the Add Buddy window that appears, enter the screen name of the buddy and click Add. To create a new group, choose Buddies→Add a Group. Type the name of the new group in the Add Group window that appears and then click Add.

如果你以前使用过 AIM，你已经有一个屏幕名称。只需输入它，输入密码，然后点击登录。Gaim 会登录并打开标准的好友列表窗口。好友列表最初是空的。要添加好友，选择好友→添加好友。在出现的添加好友窗口中，输入好友的屏幕名称并点击添加。要创建新组，选择好友→添加组。在出现的添加组窗口中输入新组的名称然后点击添加。

If any of your buddies are online, their names show up in the Buddy List window. To send a message to a buddy, double-click the name and a message window pops up. And should someone send you a message, a message window pops up with the message and you can begin conversing in that window.

如果你的任何好友在线，他们的名字会显示在好友列表窗口中。要向好友发送消息，双击名字一个消息窗口就会弹出。如果有人给你发送消息，一个消息窗口会弹出显示消息，你可以在该窗口开始交谈。

Well, if you know AIM, you know what to do: Have fun IM'ing with Gaim!

好吧，如果你熟悉 AIM，你就知道该怎么做了：尽情使用 Gaim 进行即时消息吧！

### Chapter 2: Using the Web

### 第 2 章：使用网络

### In This Chapter

### 本章内容

- ✓ Discovering the World Wide Web
- ✓ 探索万维网
- ✓ Understanding a URL
- ✓ 理解 URL
- ✓ Checking out Web servers and Web browsers
- ✓ 查看 Web 服务器和 Web 浏览器
- ✓ Web browsing with Mozilla
- ✓ 使用 Mozilla 进行网页浏览
- ✓ Creating Web pages with Mozilla Composer
- ✓ 使用 Mozilla Composer 创建网页

I suspect you already know about the Web, but did you know that the Web, or more formally the World Wide Web, made the Internet what it is today? The Internet was around for quite a while, but it did not reach the masses until the Web came along in 1993.

我猜你已经了解网络，但你知道网络，或更正式地说万维网，使互联网成为今天的样子吗？互联网存在了相当一段时间，但直到 1993 年网络出现才普及大众。

Before the Web came along, you had to use arcane UNIX commands to download and use files — it was simply too complicated for most of us. With the Web, however, anyone could enjoy the benefits of the Internet by using a Web browser — a graphical application that downloads and displays Web documents. A click of the mouse is all it takes to go from reading a document from your company Web site to downloading a video clip from across the country.

在网络出现之前，你必须使用晦涩的 UNIX 命令来下载和使用文件——这对我们大多数人来说太复杂了。然而，有了网络，任何人只需使用网页浏览器——一种下载并显示网页文档的图形应用程序——就能享受互联网的便利。只需点击鼠标，就能从阅读公司网站上的文档切换到从全国各地下载视频剪辑。

In this chapter, I briefly describe the Web and introduce Mozilla — the primary Web browser (and, for that matter, a mail and news reader, too) in Red Hat Linux. I also briefly discuss how you can create your own Web pages.

在本章中，我简要描述网络并介绍 Mozilla——Red Hat Linux 中的主要网页浏览器（顺便说一下，它也是邮件和新闻阅读器）。我还简要讨论如何创建自己的网页。

## Discovering the World Wide Web

## 探索万维网

If you have used a file server at work, you know the convenience of sharing files. You can use the word processor on your desktop to get to any document on the shared server.

如果你在工作中使用过文件服务器，你就知道共享文件的便利。你可以使用桌面上的文字处理器访问共享服务器上的任何文档。

Now imagine a word processor that enables you to open and view a document that resides on any computer on the Internet. You can view the document in its full glory, with formatted text and graphics. If the document makes a reference to another document (possibly residing on yet another computer), you can open that linked document by clicking the reference. That kind of easy access to distributed documents is essentially what the World Wide Web provides.

现在想象一个文字处理器，它能让你打开并查看互联网上任何计算机上的文档。你可以以其完整形式查看文档，包含格式化的文本和图形。如果文档引用了另一份文档（可能位于另一台计算机上），你可以通过点击引用打开该链接文档。这种对分布式文档的便捷访问本质上就是万维网提供的功能。



当然，文档必须采用标准格式，以便任何计算机（安装了适当的 Web 浏览器软件）都可以访问和解释该文档。而且在不同系统之间传输 Web 文档需要一种标准协议。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_387_0.png)

标准 Web 文档格式是超文本标记语言（HTML），而交换 Web 文档的标准协议是超文本传输协议（HTTP）。HTML 文档是文本文件，不依赖于任何特定的操作系统，因此可以在从 Windows 和 Mac 到任何类型的 UNIX 和 Linux 的任何系统上运行。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_387_1.png)

Web 服务器是一种软件，它向发出适当 HTTP 请求的任何客户端提供 HTML 文档。Web 浏览器是客户端软件，它实际从 Web 服务器下载 HTML 文档并以图形方式显示其内容。

## 像一只巨大的蜘蛛网

万维网是 Web 服务器及其提供的 HTML 文档的组合。这样来看，Web 就像一本巨大的书，其页面散布在整个互联网中。你使用计算机上运行的 Web 浏览器来查看这些页面——页面像巨大的蜘蛛网一样相互连接，文档遍布各地（如图 2-1 所示）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_387_2.png)

图 2-1：
Web 就像数十亿个页面，散布在网络各处，你可以使用 Web 浏览器从计算机上阅读它们。

如果你能想象 Web 页面——HTML 文档——是由类似于巨大蜘蛛网的网络连接链接起来的，你就能明白为什么 Web 被称为“Web”。“World Wide”这一部分源于 Web 页面散布在世界各地这一事实。

## 链接和 URL

就像真正的书籍的页面一样，Web 页面包含文本和图形。然而，与真正的书籍不同，Web 页面可以包含多媒体，例如视频剪辑、声音以及可以实际带你前往这些页面的其他 Web 页面的链接。

Web 页面中的链接是对其他 Web 页面的引用，你可以沿着这些引用从一个页面跳转到另一个页面。Web 浏览器通常将这些链接显示为下划线文本（不同颜色）或图像。每个链接都像是对你的一个指示——类似于你在真正的书中可能会找到的“有关更多信息，请参阅第 4 章”。在 Web 页面中，你只需单击链接即可；Web 浏览器会调出引用的页面，即使该文档实际上可能位于互联网上某个遥远的计算机上。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_388_0.png)

Web 页面中的链接被称为超文本链接，因为当你单击链接时，Web 浏览器会跳转到该链接引用的 Web 页面。

这种安排引发了一个问题。在真正的书中，你可能会要求读者前往书中的特定章节或页面。超文本链接如何指示所引用 Web 页面的位置？在万维网中，每个 Web 页面都有一个特殊名称，称为统一资源定位符（URL）。URL 唯一指定计算机上文件的位置。图 2-2 显示了 URL 的各部分。

图 2-2：
统一资源定位符（URL）的各部分。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_388_1.png)

如图 2-2 所示，URL 有以下各部分：

**协议：** Web 浏览器用于访问 URL 指定的文件数据的协议名称。在图 2-2 中，协议是 `http://`，这意味着 URL 指定了 Web 页面的位置。以下是一些常见的协议类型及其含义：

- `file://` 表示 URL 指向本地文件。你可以使用此 URL 在无需连接到互联网的情况下查看 HTML 文件。例如，`file:///var/www/html/index.html` 打开来自你的 Red Hat Linux 系统的文件 `/var/www/html/index.html`。
- `ftp://` 表示你可以使用文件传输协议（FTP）下载文件。例如，`ftp://ftp.purdue.edu/pub/uns/NASA/nasa.jpg` 指的是 FTP 服务器 `ftp.purdue.edu` 的 `/pub/uns/NASA` 目录中的图像文件 `nasa.jpg`。如果你想通过 FTP 访问特定的用户账户，请使用以下形式的 URL：
  
  `ftp://username:password@ftp.somesite.com/`
  
  用户名和密码嵌入在 URL 中（请注意，密码以明文形式出现且不安全）。
- `http://` 表示文件应使用超文本传输协议（HTTP）下载。这是所有网站的众所周知的 URL 格式，例如 Red Hat 主页的 `http://www.redhat.com`。如果 URL 没有文件名，Web 服务器会发送一个名为 `index.html` 的默认 HTML 文件（这是流行的基于 UNIX 的 Apache Web 服务器的默认文件名；Microsoft Windows Web 服务器使用不同的默认文件名）。
- `https://` 指定文件应通过安全套接字层（SSL）连接访问——该协议由 Netscape Communications 设计，用于在互联网上进行加密数据传输。这种形式的 URL 通常在 Web 浏览器向 Web 服务器发送敏感信息（如信用卡号、用户名和密码）时使用。例如，像 `https://some.site.com/secure/takeorder.html` 这样的 URL 可能会显示一个 HTML 表单，要求提供信用卡信息和其他个人信息（如姓名、地址和电话号码）。
- `mailto://` 指定你可以用来发送电子邮件的电子邮件地址。例如，`mailto:webmaster@someplace.com` 指的是主机 `someplace.com` 上的 Webmaster。
- `news://` 指定你可以通过网络新闻传输协议（NNTP）阅读的新闻组。例如，`news://news.md.comcast.giganews.com/comp.os.linux.setup` 访问新闻服务器 news.md.comcast.giganews.com 上的 comp.os.linux.setup 新闻组。如果你为 Web 浏览器配置了默认新闻服务器，可以省略新闻服务器的名称并使用 URL news:comp.os.linux.setup 来访问新闻组。

- **域名：** 包含具有此 URL 指定的文件的计算机的完全限定域名。你也可以在此字段中提供 IP 地址。域名不区分大小写。
- **端口：** URL 第一部分列出的协议正在使用的端口号。URL 的这一部分是可选的；所有协议都有默认端口。例如，HTTP 的默认端口是 80。如果站点将 Web 服务器配置为侦听不同的端口，则 URL 必须包含端口号。
- **目录路径：** URL 中引用的文件的目录路径。对于 Web 页面，此字段是 HTML 文件的目录路径。目录路径区分大小写。
- **文件名：** 文件的名称。对于 Web 页面，文件名通常以 .htm 或 .html 结尾。如果省略文件名，Web 服务器会返回默认文件（通常名为 index.html）。文件名区分大小写。
- **HTML 锚点：** URL 的可选部分，使 Web 浏览器跳转到文件中的特定位置。如果此部分以问号（?）而不是井号（#）开头，则浏览器会将问号后面的文本视为查询。Web 服务器根据此类查询返回信息。

## Web 服务器和 Web 浏览器

Web 服务器提供 Web 页面，而 Web 浏览器下载它们并向用户显示。这基本上就是这两个协同工作的软件包使 Web 运行的故事。

在典型场景中，用户坐在连接到互联网的计算机前并运行 Web 浏览器。当用户单击链接或在 Web 浏览器中输入 URL 时，浏览器会连接到 Web 服务器并请求服务器上的文档。Web 服务器发送文档（通常为 HTML 格式）并结束连接。Web 浏览器解释并以文本和图形显示 HTML 文档。图 2-3 说明了用户浏览 Web 的这种典型场景。

Web 浏览器与 Web 服务器的连接在服务器发送文档后结束。当用户浏览下载的文档并单击另一个超链接时，Web 浏览器再次连接到超链接中命名的 Web 服务器，下载文档，结束连接并显示新文档。这就是用户可以轻松地从一个文档移动到另一个文档的方式。



![](img/a7eec43a54473e95dc5ea333fecf1bd7_391_0.png)

Figure 2-3:
Web 浏览器请求文档，Web 服务器发送它们。

记住
Web 浏览器不仅仅能与 Web 服务器“对话”HTTP——事实上，Web 浏览器还可以使用 FTP 下载文档，而且许多浏览器还集成了邮件和新闻阅读器。

## 在 Red Hat Linux 中进行网页浏览

网页浏览很有趣，因为当今的许多网页都充满了图形和多媒体内容。还有惊喜的元素——你点击一个链接可能会到达意想不到的网页。链接是网络上最奇特（也是最有用）的方面。你可以从显示今日天气的页面开始，点击几次后，就可能在阅读本周的《时代》杂志。

要浏览网页，你只需要一个网页浏览器和互联网连接。我假设你已经处理好互联网连接了，所以你只需要了解 Red Hat Linux 中的网页浏览器。

## 查看 Red Hat Linux 中的网页浏览器

Red Hat Linux 附带 Mozilla 网页浏览器。Mozilla 是 Netscape Communicator 的开源版本，并且正在取代 Netscape 成为 Red Hat Linux 中的主要网页浏览器。

Red Hat Linux 还包含其他几个网页浏览器。我会简要提及其他浏览器，但在后面的讨论中主要聚焦于 Mozilla。以下是随 Red Hat Linux 提供的[content]
![](img/a7eec43a54473e95dc5ea333fecf1bd7_391_0.png)

Figure 2-3:
Web 浏览器请求文档，Web 服务器发送它们。

记住
Web 浏览器不仅仅能与 Web 服务器“对话”HTTP——事实上，Web 浏览器还可以使用 FTP 下载文档，而且许多浏览器还集成了邮件和新闻阅读器。

## 在 Red Hat Linux 中进行网页浏览

网页浏览很有趣，因为当今的许多网页都充满了图形和多媒体内容。还有惊喜的元素——你点击一个链接可能会到达意想不到的网页。链接是网络上最奇特（也是最有用）的方面。你可以从显示今日天气的页面开始，点击几次后，就可能在阅读本周的《时代》杂志。

要浏览网页，你只需要一个网页浏览器和互联网连接。我假设你已经处理好互联网连接了，所以你只需要了解 Red Hat Linux 中的网页浏览器。

## 查看 Red Hat Linux 中的网页浏览器

Red Hat Linux 附带 Mozilla 网页浏览器。Mozilla 是 Netscape Communicator 的开源版本，并且正在取代 Netscape 成为 Red Hat Linux 中的主要网页浏览器。

Red Hat Linux 还包含其他几个网页浏览器。我会简要提及其他浏览器，但在后面的讨论中主要聚焦于 Mozilla。以下是随 Red Hat Linux 提供的[content]
![](img/a7eec43a54473e95dc5ea333fecf1bd7_391_0.png)

Figure 2-3:
Web 浏览器请求文档，Web 服务器发送它们。

记住
Web 浏览器不仅仅能与 Web 服务器“对话”HTTP——事实上，Web 浏览器还可以使用 FTP 下载文档，而且许多浏览器还集成了邮件和新闻阅读器。

## 在 Red Hat Linux 中进行网页浏览

网页浏览很有趣，因为当今的许多网页都充满了图形和多媒体内容。还有惊喜的元素——你点击一个链接可能会到达意想不到的网页。链接是网络上最奇特（也是最有用）的方面。你可以从显示今日天气的页面开始，点击几次后，就可能在阅读本周的《时代》杂志。

要浏览网页，你只需要一个网页浏览器和互联网连接。我假设你已经处理好互联网连接了，所以你只需要了解 Red Hat Linux 中的网页浏览器。

## 查看 Red Hat Linux 中的网页浏览器

Red Hat Linux 附带 Mozilla 网页浏览器。Mozilla 是 Netscape Communicator 的开源版本，并且正在取代 Netscape 成为 Red Hat Linux 中的主要网页浏览器。

Red Hat Linux 还包含其他几个网页浏览器。我会简要提及其他浏览器，但在后面的讨论中主要聚焦于 Mozilla。以下是随 Red Hat Linux 提供的[content]
![](img/a7eec43a54473e95dc5ea333fecf1bd7_391_0.png)

Figure 2-3:
Web 浏览器请求文档，Web 服务器发送它们。

记住
Web 浏览器不仅仅能与 Web 服务器“对话”HTTP——事实上，Web 浏览器还可以使用 FTP 下载文档，而且许多浏览器还集成了邮件和新闻阅读器。

## 在 Red Hat Linux 中进行网页浏览

网页浏览很有趣，因为当今的许多网页都充满了图形和多媒体内容。还有惊喜的元素——你点击一个链接可能会到达意想不到的网页。链接是网络上最奇特（也是最有用）的方面。你可以从显示今日天气的页面开始，点击几次后，就可能在阅读本周的《时代》杂志。

要浏览网页，你只需要一个网页浏览器和互联网连接。我假设你已经处理好互联网连接了，所以你只需要了解 Red Hat Linux 中的网页浏览器。

## 查看 Red Hat Linux 中的网页浏览器

Red Hat Linux 附带 Mozilla 网页浏览器。Mozilla 是 Netscape Communicator 的开源版本，并且正在取代 Netscape 成为 Red Hat Linux 中的主要网页浏览器。

Red Hat Linux 还包含其他几个网页浏览器。我会简要提及其他浏览器，但在后面的讨论中主要聚焦于 Mozilla。以下是随 Red Hat Linux 提供的[content]
![](img/a7eec43a54473e95dc5ea333fecf1bd7_391_0.png)

Figure 2-3:
Web 浏览器请求文档，Web 服务器发送它们。

记住
Web 浏览器不仅仅能与 Web 服务器“对话”HTTP——事实上，Web 浏览器还可以使用 FTP 下载文档，而且许多浏览器还集成了邮件和新闻阅读器。

## 在 Red Hat Linux 中进行网页浏览

网页浏览很有趣，因为当今的许多网页都充满了图形和多媒体内容。还有惊喜的元素——你点击一个链接可能会到达意想不到的网页。链接是网络上最奇特（也是最有用）的方面。你可以从显示今日天气的页面开始，点击几次后，就可能在阅读本周的《时代》杂志。

要浏览网页，你只需要一个网页浏览器和互联网连接。我假设你已经处理好互联网连接了，所以你只需要了解 Red Hat Linux 中的网页浏览器。

## 查看 Red Hat Linux 中的网页浏览器

Red Hat Linux 附带 Mozilla 网页浏览器。Mozilla 是 Netscape Communicator 的开源版本，并且正在取代 Netscape 成为 Red Hat Linux 中的主要网页浏览器。

Red Hat Linux 还包含其他几个网页浏览器。我会简要提及其他浏览器，但在后面的讨论中主要聚焦于 Mozilla。以下是随 Red Hat Linux 提供的[content]
![](img/a7eec43a54473e95dc5ea333fecf1bd7_391_0.png)

Figure 2-3:
Web 浏览器请求文档，Web 服务器发送它们。

记住
Web 浏览器不仅仅能与 Web 服务器“对话”HTTP——事实上，Web 浏览器还可以使用 FTP 下载文档，而且许多浏览器还集成了邮件和新闻阅读器。

## 在 Red Hat Linux 中进行网页浏览

网页浏览很有趣，因为当今的许多网页都充满了图形和多媒体内容。还有惊喜的元素——你点击一个链接可能会到达意想不到的网页。链接是网络上最奇特（也是最有用）的方面。你可以从显示今日天气的页面开始，点击几次后，就可能在阅读本周的《时代》杂志。

要浏览网页，你只需要一个网页浏览器和互联网连接。我假设你已经处理好互联网连接了，所以你只需要了解 Red Hat Linux 中的网页浏览器。

## 查看 Red Hat Linux 中的网页浏览器

Red Hat Linux 附带 Mozilla 网页浏览器。Mozilla 是 Netscape Communicator 的开源版本，并且正在取代 Netscape 成为 Red Hat Linux 中的主要网页浏览器。

Red Hat Linux 还包含其他几个网页浏览器。我会简要提及其他浏览器，但在后面的讨论中主要聚焦于 Mozilla。以下是随 Red Hat Linux 提供的[content]
![](img/a7eec43a54473e95dc5ea333fecf1bd7_391_0.png)

Figure 2-3:
Web 浏览器请求文档，Web 服务器发送它们。

记住
Web 浏览器不仅仅能与 Web 服务器“对话”HTTP——事实上，Web 浏览器还可以使用 FTP 下载文档，而且许多浏览器还集成了邮件和新闻阅读器。

## 在 Red Hat Linux 中进行网页浏览

网页浏览很有趣，因为当今的许多网页都充满了图形和多媒体内容。还有惊喜的元素——你点击一个链接可能会到达意想不到的网页。链接是网络上最奇特（也是最有用）的方面。你可以从显示今日天气的页面开始，点击几次后，就可能在阅读本周的《时代》杂志。

要浏览网页，你只需要一个网页浏览器和互联网连接。我假设你已经处理好互联网连接了，所以你只需要了解 Red Hat Linux 中的网页浏览器。

## 查看 Red Hat Linux 中的网页浏览器

Red Hat Linux 附带 Mozilla 网页浏览器。Mozilla 是 Netscape Communicator 的开源版本，并且正在取代 Netscape 成为 Red Hat Linux 中的主要网页浏览器。

Red Hat Linux 还包含其他几个网页浏览器。我会简要提及其他浏览器，但在后面的讨论中主要聚焦于 Mozilla。以下是随 Red Hat Linux 提供的[content]
![](img/a7eec43a54473e95dc5ea333fecf1bd7_391_0.png)

Figure 2-3:
Web 浏览器请求文档，Web 服务器发送它们。

记住
Web 浏览器不仅仅能与 Web 服务器“对话”HTTP——事实上，Web 浏览器还可以使用 FTP 下载文档，而且许多浏览器还集成了邮件和新闻阅读器。

## 在 Red Hat Linux 中进行网页浏览

网页浏览很有趣，因为当今的许多网页都充满了图形和多媒体内容。还有惊喜的元素——你点击一个链接可能会到达意想不到的网页。链接是网络上最奇特（也是最有用）的方面。你可以从显示今日天气的页面开始，点击几次后，就可能在阅读本周的《时代》杂志。

要浏览网页，你只需要一个网页浏览器和互联网连接。我假设你已经处理好互联网连接了，所以你只需要了解 Red Hat Linux 中的网页浏览器。

## 查看 Red Hat Linux 中的网页浏览器

Red Hat Linux 附带 Mozilla 网页浏览器。Mozilla 是 Netscape Communicator 的开源版本，并且正在取代 Netscape 成为 Red Hat Linux 中的主要网页浏览器。

Red Hat Linux 还包含其他几个网页浏览器。我会简要提及其他浏览器，但在后面的讨论中主要聚焦于 Mozilla。以下是随 Red Hat Linux 提供的[content]
![](img/a7eec43a54473e95dc5ea333fecf1bd7_391_0.png)

Figure 2-3:
Web 浏览器请求文档，Web 服务器发送它们。

记住
Web 浏览器不仅仅能与 Web 服务器“对话”HTTP——事实上，Web 浏览器还可以使用 FTP 下载文档，而且许多浏览器还集成了邮件和新闻阅读器。

## 在 Red Hat Linux 中进行网页浏览

网页浏览很有趣，因为当今许多网页都充满图形和多媒体。还有惊喜因素——点击链接可能到达意想不到的页面。链接是网络上最奇特也最有用的方面。你可以从显示今日天气的页面开始，几次点击后就可能在阅读本周《时代》杂志。

要浏览网页，只需网页浏览器和互联网连接。我假设你已处理好互联网连接，所以只需了解 Red Hat Linux 中的网页浏览器。

## 查看 Red Hat Linux 中的网页浏览器

Red Hat Linux 附带 Mozilla 网页浏览器。Mozilla 是 Netscape Communicator 的开源版，正取代 Netscape 成为 Red Hat Linux 的主要浏览器。

Red Hat Linux 还包含其他浏览器。我会简要提及它们，后续讨论主要聚焦 Mozilla。以下是随 Red Hat Linux 提供的[content]
![](img/a7eec43a54473e95dc5ea333fecf1bd7_391_0.png)

Figure 2-3:
Web 浏览器请求文档，Web 服务器发送它们。

记住
Web 浏览器不只是与 Web 服务器“对话”HTTP——事实上，Web 浏览器还可使用 FTP 下载文档，许多浏览器还集成了邮件和新闻阅读器。

## 在 Red Hat Linux 中进行网页浏览

网页浏览很有趣，因为当今许多网页充满图形和多媒体。还有惊喜——点击链接可能到达意想不到的页面。链接是网络上最奇特也最有用的方面。你可以从显示今日天气的页面开始，几次点击后就可能在读本周《时代》杂志。

要浏览网页，只需网页浏览器和互联网连接。假设你已处理好互联网连接，那么只需了解 Red Hat Linux 中的网页浏览器。

## 查看 Red Hat Linux 中的网页浏览器

Red Hat Linux 附带 Mozilla 网页浏览器。Mozilla 是 Netscape Communicator 的开源版，正取代 Netscape 成为 Red Hat Linux 的主要浏览器。

Red Hat Linux 还包含其他浏览器。我会简要提及，后续主要聚焦 Mozilla。以下是随 Red Hat Linux 提供的[content]
![](img/a7eec43a54473e95dc5ea333fecf1bd7_391_0.png)

Figure 2-3:
Web 浏览器请求文档，Web 服务器发送它们。

记住
Web 浏览器不只是与 Web 服务器“对话”HTTP——事实上，Web 浏览器还可使用 FTP 下载文档，许多浏览器还集成了邮件和新闻阅读器。

## 在 Red Hat Linux 中进行网页浏览

网页浏览很有趣，因为当今许多网页充满图形和多媒体。还有惊喜——点击链接可能到达意想不到的页面。链接是网络上最奇特也最有用的方面。你可以从显示今日天气的页面开始，几次点击后就可能在读本周《时代》杂志。

要浏览网页，只需网页浏览器和互联网连接。假设你已处理好互联网连接，那么只需了解 Red Hat Linux 中的网页浏览器。

## 查看 Red Hat Linux 中的网页浏览器

Red Hat Linux 附带 Mozilla 网页浏览器。Mozilla 是 Netscape Communicator 的开源版，正取代 Netscape 成为 Red Hat Linux 的主要浏览器。

Red Hat Linux 还包含其他浏览器。我会简要提及，后续主要聚焦 Mozilla。主要浏览器如下：

- **Mozilla：** 老牌工作马 Netscape Communicator 的重生版，更好。包含邮件和新闻阅读器。浏览器称为 Mozilla Navigator，或简称 Navigator。
- **Epiphany：** GNOME 浏览器，使用部分 Mozilla 代码绘制网页，界面更简单。默认未安装，应在本书附带 DVD 上。找不到可从 epiphany.mozdev.org 下载。
- **Konqueror：** KDE 浏览器，同时是文件管理器和通用查看器。

除此三款外，还有许多应用可下载显示网页。

## 启动 Mozilla

从 GNOME 桌面可通过两种方式启动 Mozilla：

- 在 GNOME 或 KDE 面板点击 Web 浏览器图标（地球和鼠标）。
- 选择 主菜单→Internet→Mozilla Web Browser。

启动后显示浏览器窗口及默认主页，可配置为其他页面。

## 学习 Mozilla 用户界面

Figure 2-4 显示 Wiley 网站页面及 Mozilla 浏览器窗口主要元素。

Mozilla 界面功能丰富，易于掌握。可关闭繁杂项目，也可先从基础开始逐步扩展。

点击关闭侧边栏

![](img/a7eec43a54473e95dc5ea333fecf1bd7_393_0.png)

Figure 2-4:
Mozilla 网页浏览器运行中。

From www.dummies.com. Copyright © 2003 by Wiley Publishing, Inc. All rights reserved.
Reproduced here by permission of the publisher.

## Mozilla 工具栏

从窗口顶部起为标准菜单栏，其后为导航工具栏，再为较细的个人工具栏，含 Home、Bookmarks 等图标。个人工具栏下方垂直分为侧边栏和显示当前网页的主区域。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_393_1.png)

注意侧边栏上的 X 按钮，点击后侧边栏消失。建议关闭以显示更多网页内容。

无侧边栏时窗口更简洁（图 2-5）。可清晰看到菜单栏及导航工具栏、个人工具栏。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_394_0.png)

Figure 2-5:
关闭侧边栏以简化 Mozilla 用户界面。

From www.dummies.com. Copyright © 2003 by Wiley Publishing, Inc. All rights reserved.
Reproduced here by permission of the publisher.

菜单栏下方导航工具栏按钮功能：

- **Back：** 返回上一页。
- **Forward：** 前进到后退来源页。
- **Reload：** 重新加载当前页。
- **Stop：** 停止加载。
- **Location text box：** 显示当前页 URL，可输入 URL 访问。
- **Search：** 用当前页 URL 作为搜索串搜索 Netscape 搜索站点（search.netscape.com）。
- **Print：** 打印当前页，可预览。
- **Mozilla icon：** 前往 Mozilla.org 网站（www.mozilla.org）。

其下为个人工具栏，含 Home 和 Bookmarks：

- **Home：** 到主页。
- **Bookmarks：** 显示菜单，可添加书签和管理。

个人工具栏还有 Red Hat Network 链接，可注册接收 Red Hat Linux 更新。其余链接按文件夹组织，点击文件夹显示下拉列表。

## 状态栏

窗口底部为状态栏，中间显示 Mozilla 加载网页时的状态信息。

左侧有多个图标，悬停显示气泡帮助。点击可打开其他 Mozilla 窗口。表 2-1 说明图标功能。

**表 2-1 Mozilla 状态栏上的图标**

| 当点击此图标时 | 其执行以下操作 |
|---|---|
| [icon] | 打开另一个 Navigator 窗口。 |
| [icon] | 打开 Mozilla Mail 窗口阅读邮件和新闻组。 |
| [icon] | 打开 HTML 编辑器窗口准备 HTML 文档。 |
| [icon] | 打开地址簿窗口查找地址。 |
| [icon] | 打开 ChatZilla 窗口加入 IRC 频道聊天。 |

![](img/a7eec43a54473e95dc5ea333fecf1bd7_395_0.png)

状态栏右上角状态信息右侧有两个图标。左侧表示在线，点击可离线。右侧为安全挂锁。Mozilla 支持使用 SSL 协议传输加密数据的 HTTPS。当连接支持安全 HTTP 的服务器时挂锁锁定，否则打开表示不安全。安全 URL 以 https:// 开头。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_396_0.png)

状态栏中间显示状态信息。下载完成后显示耗时秒数。

## Mozilla 菜单

菜单使用较少，但了解其功能有帮助。表 2-2 为概览。

表 2-2 Mozilla 菜单

| 此菜单 | 使你能够执行以下操作 |
|---|---|
| File | 打开文件或网页位置，关闭浏览器，通过邮件发送网页或链接，编辑网页，打印当前页，退出 Mozilla。 |
| Edit | 复制粘贴，查找当前页文本，编辑首选项。 |
| View | 显示/隐藏工具栏，重新加载页面，调整文本大小，查看 HTML 代码，查看页面信息。 |
| Go | 在访问历史中后退/前进，或跳转到最近访问页面。 |
| Bookmarks | 添加书签，管理书签，向个人工具栏文件夹添加链接。 |
| Tools | 搜索网页，管理图像加载、Cookie、存储密码等。 |
| Window | 打开其他 Mozilla 窗口，如 Mozilla Mail、Navigator、地址簿、编辑器。 |
| Help | 获取 Mozilla 在线帮助。 |

## 更改你的主页

主页是 Mozilla 启动时加载的页面。默认从 Mozilla.org 网站加载。更改很简单。



首先找到你想要设为主页的页面。你可以用任何方式到达该页面。你可以在搜索引擎上搜索想要的页面，也可以在位置文本框中输入 URL，甚至可能偶然进入一个你想设为主页的页面。无所谓。

当你正在查看感觉适合作为主页的网页时，从 Mozilla 菜单中选择 编辑→首选项。首选项窗口出现（如图 2-6 所示）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_397_0.png)

图 2-6：
点击“使用当前页面”按钮将当前网页设为主页。

在图 2-6 的右侧，注意到“主页”单选按钮是开启的。这意味着启动时 Mozilla Navigator 应显示主页。然后是主页的 URL，下面有一个“使用当前页面”按钮。点击该按钮即可将当前页面设为主页。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_397_1.png)

你可以使用首选项窗口设置许多其他选项。虽然我没有解释所有选项，但你可以随意点击来探索从此窗口可以做的一切。例如，你可以点击“选择文件”按钮，从本地系统中选择一个文件作为主页。

## 更改 Mozilla 的外观

Mozilla 支持主题。主题基本上是 Mozilla 用户界面的外观和感觉（包括背景和按钮的外观）。默认主题称为 Classic 主题，它提供与 Netscape 以前类似的外观和感觉。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_398_0.png)

Mozilla 还附带一个名为 Modern 的主题，你可以从网络上下载许多其他主题。访问 themes.mozdev.org 浏览一些可用的主题并下载你想要尝试的主题。你也可以通过从 Mozilla 菜单中选择 查看→应用主题→获取新主题 来获取新主题。

更改主题很容易。如果你想在选择主题之前先看到所选主题，请按以下步骤操作：

- 1. 从 Mozilla 菜单中选择 编辑→首选项。
- 首选项窗口出现。
- 2. 点击窗口左侧“外观”旁边的加号。
- “外观”项目展开。
- 3. 点击“主题”项目。
- 右侧现在显示可用的主题。
- 4. 点击你想要的主题。
- 你会在主题列表下方的区域看到按钮和颜色的预览（图 2-7）。

图 2-7：选择主题以更改 Mozilla 的外观。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_398_1.png)

- 5. 选择主题后，点击“确定”关闭首选项窗口。
一个对话框会告诉你新主题将在下次启动 Mozilla 时生效。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_399_0.png)

要查看主题的完整效果，请关闭 Mozilla 然后重新启动。

## 使用 Mozilla 上网冲浪

从 Mozilla 主页开始去哪里取决于你。你所要做的就是点击并看看会到达哪里。随意移动鼠标。当鼠标指针变为带伸出食指的手时，表示你位于一个链接上。点击链接，Mozilla 就会下载该链接引用的网页。

你如何使用网络取决于你想做什么。刚开始时，你可能会大量探索——浏览网站并跟随链接，而没有特定的目标。这可能就是所谓的网络逛街。

网络的另一种更有目的性的用途是从网络上查找特定信息。例如，你可能想要找到包含指定关键词文档的所有网站。对于此类搜索，你可以使用网络上提供的众多网络搜索工具之一。例如，许多人推崇 Google（www.google.com）。Mozilla 的“搜索”按钮会带你到 Netscape 搜索页面（search.netscape.com）。

第三种用途是访问已知 URL 的特定站点。例如，在阅读本书中关于特定主题的内容时，你可能会遇到特定的 URL。在这种情况下，你想直接前往该网页。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_399_1.png)

如果你想使用 Mozilla 上网冲浪，你只需要一个起始网页——然后你可以点击任何吸引你的内容。例如，选择 Mozilla 导航工具栏中位置文本框中的文本，输入 search.netscape.com，然后按 Enter。你将进入显示按主题组织的 Netscape 网络目录的 Netscape 搜索页面。这就是你的起点。你所要做的就是点击，然后出发！

## 创建网页

如果你从 ISP 获取互联网接入，你可能也会获得一个免费的网页。唯一的条件是你必须上传网页的 HTML 文件，这意味着你必须以某种方式准备一个网页。

准备网页的一种方法是简单地使用文本编辑器并输入 HTML 代码。毕竟，网页只是一个带有 HTML 标签的文本文件。即使我不会让任何人经历输入所有那些 HTML 标签的痛苦，我还是想向你展示一个非常基本的 HTML 文档，只是为了让你了解其结构。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_400_0.png)

在进入 HTML 代码之前，我想给你一个好消息。Mozilla 附带了 Composer，你可以用它来准备 HTML 文档——网页——而无需学习 HTML 标签。现在你知道解脱即将到来，我可以快速向你展示 HTML 文档的内部结构。

## 介绍 HTML

通常，当客户端（网页浏览器）连接到 Web 服务器时，服务器会返回一个名为 index.html 的 HTML 文件。当你拥有自己的网站时，index.html 文件就是你的主页。我通过创建 index.html 文件并通过迭代改进它来介绍 HTML。在此过程中，你会看到大多数重要的 HTML 功能。

首先，打开任何文本编辑器并输入以下文本行：

```
<html>

<head>
<TITLE>
My Home Page
</TITLE>
</head>

<body>

<center>
<h1>
My Home Page
</h1>
</center>

<hr>
This page is under construction.
<hr>

Copyright &copy; 2003 Someone
<a href="mailto:webmaster@myplace.com">
<address>
webmaster@myplace.com
</address>
</a>

</body>
</html>
```

这是一个最基本的 HTML 文件。继续将其保存为文件名 index.html。

要查看它是什么样子，请从 Mozilla 菜单中选择 文件→打开文件。浏览目录并从你存储它的位置中选择 index.html 文件。点击“打开”在 Mozilla 中打开该文件。图 2-8 显示了网页在 Mozilla 中的外观。顺便说一下，图 2-8 中显示的 Mozilla 窗口使用的是 Modern 主题。这就是为什么它看起来与通常的 Mozilla 窗口不同（例如，参见图 2-4）。

图 2-8：
在 Mozilla 中查看你的 HTML 文件以了解其外观。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_401_0.png)

回到网页本身，它看起来相当不错，不是吗？难怪我们喜欢网页。

此时，你应该将图 2-8 中的网页与 HTML 代码相关联，以便看到每个 HTML 标签的效果。特别是，注意以下几点：

- HTML 标签用尖括号 `<...>` 括起来，并且有一对标签——开始标签和结束标签——如下所示 `</...>`。
- HTML 标签不区分大小写。因此，你可以将标题标签输入为 `<title>` 或 `<TITLE>`；两者含义相同。
- `<html>...</html>` 标签对只是表示该文档是 HTML 文档；该标签没有视觉效果。
- `<head>...</head>` 标签包含页眉信息。在这种情况下，页眉定义了页面的标题。该标题出现在 Mozilla 窗口的标题栏中。
- `<body>...</body>` 标签对包含整个 HTML 文档。
- 网页正文以标题级别 1（`<h1>...</h1>`）并居中（`<center>...</center>`）显示文本 My Home Page。
- `<hr>` 标签会导致浏览器显示一条水平线。
- HTML 关键字 `&copy;` 显示版权符号。



♦ <a href= ...> ... </a> 标签添加了一个超链接。开始标签 <a href="mailto:webmaster@myplace.com"> 与结束标签 </a> 之间的所有行称为锚（或 <a>）元素。出现在锚元素开始标签中的关键字 href 称为属性。

♦ <address> ... </address> 标签将封闭的文本显示为地址（斜体）。

我不会再进一步介绍 HTML 标签；这些内容应该能让你感受到典型网页的整体结构。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_402_0.png)

如果你对任何网页对应的 HTML 代码感到好奇，只需从 Mozilla 菜单中选择 查看→页面源代码 即可查看当前页面的 HTML 代码。

## 使用 Mozilla Composer 制作网页

Mozilla Composer 是一个图形化工具，用于在无需了解太多 HTML 的情况下创建网页。如果你懂 HTML，当然可以在 Composer 中利用这方面的知识。其中一个优点是，即使你不懂任何 HTML，也能创建出漂亮的网页。

### Composer 中的示例编辑会话

如果你要从头创建新网页，请从 Mozilla 菜单中选择 窗口→ Composer。

如果你想编辑已在 Mozilla 中打开的现有网页，请选择 文件→编辑页面。Mozilla 会打开一个 Composer 窗口，其中包含相同的 HTML 文件。

你可以从图 2-8 所示的页面开始编辑。在 Composer 窗口中，网页看起来与图 2-8 相似，但现在它像文字处理器一样工作。你可以像在文字处理器中一样开始编辑文本和更改版面。要添加文本，只需单击并输入。要应用诸如粗体、斜体和下划线等文本格式效果，请使用文本格式工具栏（它看起来与任何文字处理器中的类似工具栏非常相似）。

你还可以插入图像。方法如下：

- 1. 收集你想要使用的图像文件（格式如 JPEG 或 GIF），然后将它们保存在你的 Red Hat Linux PC 上的某个位置。

你可以在绘图和绘画程序中准备图像，或从其他来源获取图像（例如，从 thefreesite.com/Free_Graphics/Free_clipart/index.html 等网站）。

- 2. 将光标定位到想要插入图像的位置；然后从 Composer 菜单中选择 插入→图像。

图像属性对话框，如图 2-9 所示，会出现。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_403_0.png)

图 2-9：
你可以通过此对话框向网页添加图像。

- 3. 单击 选择文件 并从 选择图像文件 对话框中选择图像文件。

- 4. 为图像输入备用文本——这是文本浏览器中会出现的文本。

你还可以输入工具提示——当用户将鼠标悬停在图像上时会出现的那段文字。

- 5. 填写所有信息后，单击 确定。

图像应出现在你放置光标的位置（图 2-10）。

- 6. 对其他图像重复步骤 2 至 5。插入所有图像后，选择 文件→保存 以保存 HTML 文件。

如果你正在创建新网页，Composer 会提示你输入文件名。

图 2-10 显示了图 2-8 的网页，我在其中添加了一些文本并插入了一张图像。

通过这个简短的示例，我才刚刚触及 Composer 所能做到的表层。如果你开始在示例网页上尝试这些功能，你很快就会掌握 Composer 的功能。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_403_1.png)

在 Composer 中工作时，如果你想知道工具栏按钮的作用，只需将鼠标悬停在按钮上，一个小帮助气球就会弹出，提供有用的提示。图 2-11 显示了将鼠标悬停在 链接 按钮上时会发生的情况。

## Composer 中的视图

请注意，Composer 窗口底部有四个标签。这些标签使你能够以不同形式查看网页。你通常在 正常 视图中编辑文件，但可以切换到其他视图；例如，如果你愿意，也可以直接编辑 HTML。要更改视图，请单击标签。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_404_0.png)

图 2-10：
你可以在 Composer 中创建或编辑网页。

四个标签如下：

- **Normal:** 此视图以接近完整的版面显示网页，同时也允许你编辑页面。你通常在此视图中进行大部分编辑和格式化。
- **HTML Tags:** 此视图以小图标的形式显示网页的 HTML 标签。你可以快速检查哪些 HTML 标签影响文档的哪些部分，并可能修复任何格式问题。

图 2-11：
将鼠标悬停在按钮上，Composer 会显示气球帮助。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_404_1.png)

- **<HTML> Source:** 此视图以其全部内容显示 HTML 文本。如果你使用过 WordPerfect，这就像 WordPerfect 的“显示代码”选项。如果网页版面出现异常，你可以进入此窗口，找到导致问题的代码并修复它。当然，你需要了解一些 HTML，但不用担心——如果你开始使用网页，你会逐渐掌握它。你还可以使用此视图直接用 HTML 编写网页，然后切换到 正常 或 预览 视图来检查版面。

- **Preview:** 此视图基本上显示网页在 Mozilla Navigator 中的外观。这是一种在无需打开 Navigator 窗口的情况下快速检查最终版面的方法。此视图中无法编辑。

HTML 标签 视图在你想快速查找多余的 HTML 标签时很有用。图 2-12 显示了图 2-10 所示网页的 HTML 标签 视图。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_405_0.png)

图 2-12：
HTML 标签 视图以图标形式显示 HTML 标签。

每个标签都以黄色显示，并带有诸如 CENTER（居中文本）、BIG（更大字体）、H1（1 级标题）、IMG（图像）等标签名称。你可以看到网页中是否出现多余的标签——并且如果愿意可以删除它们（尽管它们通常不会造成任何危害——例如居中的空白行）。

### 第 3 章：阅读新闻组

### 本章内容

- 了解新闻组
- 从你的 ISP 阅读新闻组
- 在某些网站上阅读和搜索新闻组

Internet 新闻组就像是网络时代之前的电子公告板系统（BBS）或 AOL 和 MSN 等在线系统提供的论坛。本质上，新闻组提供了一个跨越全球的分布式会议系统。你可以发布文章——本质上是向一群人发送的电子邮件——并回复他人发布的文章。

把 Internet 新闻组想象成一个聚会场所——一个虚拟的会面场所，你可以在那里提问并讨论各种问题（最重要的是，你讨论的一切都会为后世存档）。

要参与新闻组，你需要访问新闻服务器——你的 Internet 服务提供商（ISP）应该为你提供此访问权限。你还需要一个新闻阅读器。幸运的是，Red Hat Linux 附带了可用于阅读新闻组的软件：Pan 和 Mozilla Mail。本章我将介绍新闻组，并向你展示如何使用几种新闻阅读器阅读新闻组。我还将简要说明如何从几个网站免费阅读和搜索新闻组。

### 了解新闻组

新闻组起源于 Usenet——一个广泛用于交换电子邮件和新闻项目的存储转发消息网络。Usenet 的工作原理类似于电报，即新闻和邮件从一个系统 relay 到另一个系统。在 Usenet 中，系统并不在任何网络上；它们只是拨号并使用 UNIX 到 UNIX 复制协议（UUCP）传输文本消息。

尽管 Usenet 是一个非常松散连接的计算机集合，但它运行良好并继续被使用，因为连接它的费用非常低。你只需要一个调制解调器和一个愿意存储和转发你的邮件和新闻的站点。你需要在系统上设置 UUCP，但不需要持续的网络连接；只需几次电话呼叫就能保持电子邮件和新闻的流动。缺点是你无法使用 TCP/IP 服务，如 Web、TELNET 或 FTP。



自 Usenet 起源以来，新闻组现已迁移到互联网（尽管新闻组仍被称为 Usenet 新闻组）。不再使用 UUCP，新闻现在通过网络新闻传输协议（NNTP）传输。

尽管（对于大多数在线世界而言）新闻传输协议已从 UUCP 更改为 NNTP，但新闻传输的存储转发概念仍然保留。因此，如果你想在 Red Hat Linux 系统上获取新闻，你必须找到一个新闻服务器，让你的系统可以从中下载新闻。通常，这将是你的 ISP 的新闻服务器。

## Newsgroup hierarchy

互联网新闻组按层次结构组织，以便于维护和易于使用。新闻组名称显示了层次结构——用互联网术语书写——但经过一点解释后很容易理解。

A typical newsgroup name looks like this:

```
comp.os.linux.announce
```

这个名称表示 comp.os.linux.announce 是一个关于 Linux 操作系统（os.linux）的公告（announce）的新闻组，并且这些主题属于计算机（comp）的广泛类别。

如你所见，新闻组名称的格式是由句点分隔的一系列单词。这些单词表示新闻组的层次结构。图 3-1 说明了新闻组层次组织的概念。

Figure 3-1:
新闻组按层次结构组织，具有许多顶级类别。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_407_0.png)

为了理解新闻组层次结构，将新闻组名称与 Linux 中文件的路径名（例如，`/usr/lib/X11/xinit/xclients`）进行比较。就像文件的路径名显示了文件的目录层次结构一样，新闻组名称显示了新闻组的层次结构。在文件名中，斜杠（`/`）分隔目录名称；在新闻组名称中，句点（`.`）分隔新闻组层次结构中的不同级别。

在新闻组名称中，第一个词代表新闻组类别。例如，`comp.os.linux.announce` 新闻组属于 `comp` 类别，而 `alt.books.technical` 则属于 `alt` 类别。

## Top-level newsgroup categories

表 3-1 列出了一些主要的新闻组类别。你会发现各种各样的新闻组，涵盖从政治到计算机的主题。Linux 相关新闻组位于 `comp.os.linux` 层次结构中。

Table 3-1 Some Major Newsgroup Categories

| Category | Subject |
|---|---|
| alt | "Alternative" newsgroups (not subject to any rules), which run the gamut from the mundane to the bizarre |
| bionet | Biology newsgroups |
| bitnet | Bitnet newsgroups |
| biz | Business newsgroups |
| clari | Clarinet news service (daily news) |
| comp | Computer hardware and software newsgroups (includes operating systems such as Linux and Microsoft Windows) |
| ieee | Newsgroups for the Institute of Electrical and Electronics Engineers (IEEE) |
| k12 | Newsgroups devoted to elementary and secondary education |
| linux | Newsgroups devoted to Linux (includes a linux.redhat hierarchy) |
| misc | Miscellaneous newsgroups |
| news | Newsgroups about Internet news administration |
| rec | Recreational and art newsgroups |
| sci | Science and engineering newsgroups |
| soc | Newsgroups for discussing social issues and various cultures |
| talk | Discussions of current issues (think "talk radio") |

这个类别的简短列表具有误导性，因为它并不能真正告诉你每个类别中可用的各种各样的新闻组。仅顶级类别就接近一千个，但许多顶级类别仅分布在世界特定地区。由于每个新闻组类别包含多个子类别级别，因此新闻组的总数可能接近 60,000 或 70,000！仅 comp 类别就拥有超过 500 个新闻组。

若要浏览新闻组类别并了解新闻组涵盖主题的广度，请访问 newsone.net 上的 Free Usenet Newsgroup News 网站。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_409_0.png)

## Linux-related newsgroups

通常，你必须根据自己的兴趣缩小新闻组的选择范围。例如，如果你对 Linux 感兴趣，你可以选择以下一个或多个新闻组：

- `comp.os.linux.admin` — 关于 Linux 系统管理的信息。
- `comp.os.linux.advocacy` — 关于推广 Linux 的讨论。
- `comp.os.linux.announce` — 关于 Linux 的重要公告。该新闻组是受管理的，这意味着你必须将文章邮件发送给版主，版主在文章适合新闻组时再将其发布到新闻组（这可以防止垃圾信息堵塞新闻组）。
- `comp.os.linux.answers` — 关于 Linux 的问答。所有 Linux HOWTO 都发布在此受管理的新闻组中。
- `comp.os.linux.development` — 当前 Linux 开发工作。
- `comp.os.linux.development.apps` — Linux 应用开发。
- `comp.os.linux.development.system` — Linux 操作系统开发。
- `comp.os.linux.hardware` — 关于 Linux 和各种类型硬件的讨论。
- `comp.os.linux.help` — 有关 Linux 各方面的帮助。
- `comp.os.linux.misc` — 各种 Linux 相关主题。
- `comp.os.linux.networking` — Linux 下的网络。
- `comp.os.linux.redhat` — Red Hat Linux 相关主题。
- `comp.os.linux.setup` — Linux 设置和安装。
- `comp.os.linux.x` — 关于在 Linux 下设置和运行 X Window 系统的讨论。
- `linux.redhat` — 关于 Red Hat Linux 的讨论。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_410_0.png)

你必须有选择地阅读新闻组，因为即使在 Linux 这样特定的领域，也不可能跟上所有的新闻。当你首次安装和设置 Red Hat Linux 时，你可能会阅读诸如 `comp.os.linux.redhat`、`comp.os.linux.setup`、`comp.os.linux.hardware` 和 `comp.os.linux.x`（尤其是在运行 X 时）等新闻组。在 Linux 运行起来后，你可能只想了解 Linux 中发生的新事物。对于此类信息，请阅读 `comp.os.linux.announce` 新闻组。

## Reading Newsgroups from Your ISP

如果你已向 ISP 订阅互联网接入服务，它应该为你提供访问新闻服务器的权限。此类互联网新闻服务器使用网络新闻传输协议（NNTP）进行通信。然后你可以使用支持 NNTP 的新闻阅读器，例如 Pan，来访问新闻服务器并阅读选定的新闻组。你也可以使用随 Mozilla 提供的新闻阅读器（随 Red Hat Linux 包含）来阅读新闻。这是从你的 Red Hat Linux 互联网系统访问新闻的最简单方法。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_410_1.png)

我关于阅读新闻组的讨论假设你已从 ISP 获得新闻服务器的访问权限。ISP 为你提供新闻服务器的名称以及设置新闻阅读器上新闻帐户所需的任何用户名和密码。

要阅读新闻，你需要一个新闻阅读器——一个程序，使你能够选择新闻组并查看该新闻组中的项目。你还必须了解新闻组层次结构和命名约定（在本章“Newsgroup hierarchy”部分中描述）。现在我向你展示如何从新闻服务器阅读新闻。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_410_2.png)

如果你无法通过 ISP 访问新闻组，你可以尝试使用众多公共新闻服务器之一。有关公共新闻服务器的列表，请访问 www.newzbot.com 上的 NewzBot。在此网站上，你可以搜索承载特定新闻组的新闻服务器。

## Reading newsgroups with Mozilla Mail

你可以从 Mozilla 的组件之一 Mozilla Mail 浏览新闻组并发布文章。当你第一次开始阅读新闻组时，请按照以下步骤设置新闻帐户：

1. **单击 Mozilla 图标（地球和鼠标图标）或从 GNOME 面板中选择 主菜单：Internet：Mozilla Web Browser。**
   Mozilla 启动。
2. **从 Mozilla 菜单中选择 Windows：Mail & Newsgroups。**
   如果你尚未定义任何邮件或新闻组帐户，则会出现帐户向导。否则 Mozilla Mail and News（简称为 Mozilla Mail）窗口会出现。
3. **从 Mozilla Mail 菜单中选择 Edit：Mail & Newsgroups Account Settings。**
   出现一个对话框。
4. **单击 Add Account。**
   帐户向导出现（如图 3-2 所示）。
5. **选择 Newsgroup Account 单选按钮（图 3-2）并单击 Next。**
6. **填写你的身份信息——姓名和电子邮件地址——然后单击 Next。**
7. **输入你的新闻服务器名称并单击 Next。**
8. **输入新闻组帐户的描述性名称并单击 Next。**
9. **单击 Finish 完成新闻组帐户设置。**

![](img/a7eec43a54473e95dc5ea333fecf1bd7_411_0.png)

Figure 3-2: Mozilla 的帐户向导引导你完成新闻组帐户设置。

新的新闻组帐户现在出现在 Mozilla Mail 窗口左侧的帐户列表中。单击新闻组帐户名称，窗口右侧将显示新闻组帐户的选项。



点击“订阅新闻组”链接。Mozilla Mail 开始从新闻服务器下载新闻组列表。

如果你的 ISP 的新闻服务器需要用户名和密码，将提示你输入这些信息。之后，Mozilla Mail 下载新闻组列表并在订阅对话框中显示它们。（你可以在文本框中输入搜索字符串来缩小列表范围。）找到想要的新闻组后，勾选复选框以订阅这些新闻组（如图 3-3 所示）。然后点击 OK 关闭对话框。

Figure 3-3:
在此对话框中指定要订阅的新闻组。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_412_0.png)

订阅新闻组后，这些新闻组会出现在 Mozilla Mail 窗口左侧的新闻组账户名称下。然后你可以使用以下步骤阅读新闻组：

- 1. **点击一个新闻组名称（例如，`comp.os.linux.announce`）。**
- 这会弹出一个对话框，询问你想要下载多少条消息头。
- 2. **指定你想要的头数（例如 500），然后点击 OK 继续。**
- Mozilla Mail 从新闻组下载头信息并在窗口右上区域显示列表。
- 3. **从头信息列表中，点击一项来阅读该文章（如图 3-4 所示）。**

要选择其他已订阅的新闻组，只需在窗口左侧点击新闻组名称即可。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_413_0.png)

Figure 3-4:
点击文章在右下窗口中阅读它。

## 新闻组订阅

与杂志或报纸不同，新闻组不需要订阅；你可以阅读新闻服务器上可用的任何新闻组。新闻服务器的管理员可能会决定排除某些新闻组。如果它们未被包含，则无法阅读它们。

唯一可以称为“订阅”的情况是当你指定常规想要阅读的新闻组时。新闻服务器不会收到任何订阅信息——这些信息仅由新闻阅读器用来确定从新闻服务器下载什么内容。

## 如何发布新闻

你可以使用任何新闻阅读器向一个或多个新闻组发布新闻文章（新条目或对旧帖子的回复）。发布新闻项目的确切命令取决于新闻阅读器。例如，在 Mozilla Mail 新闻阅读器中，你按以下步骤发布文章：

- 1. **点击工具栏上的 Reply 以对正在阅读的新闻项目进行跟进。** 要发布新的新闻文章，请点击 Compose。
- 出现一个窗口，你可以在其中撰写消息。
- 2. **输入新闻组名称，就像发送电子邮件时输入收件人地址一样；然后输入主题和你的消息。**

对于此测试发布，请将主题行输入为 `ignore`，并将新闻组名称输入为 `misc.test`。

否则，接收你文章的任何站点都会通过邮件回复，告知你文章已到达该站点；这与 `misc.test` 新闻组的用途一致。Figure 3-5 显示了在 Netscape Communicator 中正在撰写的消息。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_414_0.png)

Figure 3-5:
你可以在 Mozilla Mail 新闻阅读器中发布跟进或新的新闻文章。

3. 完成撰写消息后，点击工具栏上的 Send（见图 3-5）。

Mozilla Mail 将消息发送到新闻服务器，新闻服务器再将其发送到其他新闻服务器，很快它就会遍布全球！

4. 要验证测试消息是否已到达新闻组，请选择 File→Subscribe；然后订阅 `misc.test` 新闻组（你最近发布新文章的地方）。查看 `misc.test` 中的最新文章（或其中一篇最近的文章），应该是你最近发布的文章。

如果你发布文章并立即阅读新闻组，你会看到新文章，但这并不意味着文章已到达互联网上的其他站点。毕竟，你的帖子会立即出现在你的新闻服务器上，因为你就是在那里发布了文章。由于新闻分发的存储转发模式，新闻文章会逐渐从你的新闻服务器传播到世界各地的其他服务器。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_414_1.png)

`misc.test` 新闻组提供了一种查看你的新闻发布是否真正传播的方法。如果你向该新闻组发布文章并且在主题中不包含单词 ignore，新闻服务器会通过向文章头中 Reply To 字段所列地址发送电子邮件来确认收到文章。

## 在网站上阅读和搜索新闻组

如果你无法通过 ISP 访问新闻组，你仍然可以在多个网站上阅读新闻组并向新闻组发布文章。其中一些网站存档旧新闻文章并提供良好的搜索功能，因此你可以搜索与你可能有的某些问题相关的文章。

通过网站阅读新闻组最好的地方在于，你甚至不需要访问新闻服务器，并且可以从你的网页浏览器阅读新闻。

表 3-2 列出了提供 Usenet 新闻组免费访问的网站。有些网站以付费方式提供 Usenet 新闻组服务。我在这里不列出它们，但你可以在 Google（www.google.com）中搜索它们——输入搜索词 usenet newsgroup access，你应该会得到所有提供新闻组访问的网站列表（包括收费的网站）。

**表 3-2 提供 Usenet 新闻组免费访问的网站**

| 网站 | URL |
|---|---|
| Google Groups | groups.google.com |
| NewsOne.Net | newsone.net |
| Mailgate | www.mailgate.org |

其中最好的阅读新闻组、发布文章和搜索旧新闻组存档的地方是 Google Groups——即位于 groups.google.com 的网页上的 Google Usenet 讨论论坛。在该网站上，你可以选择要浏览的新闻组，并可以对各种新闻组发布的文章进行回复。

Google Groups 最好的地方是搜索功能。你已经知道 Google 的网页搜索有多好；你可以使用同样的全面搜索功能来定位与你的搜索词相关的新闻组帖子。要搜索新闻组，请在 groups.google.com 填写搜索表单并按 Enter。

要在 Google Groups 中浏览新闻组，请忽略搜索框并查看高级新闻组类别列表，例如 alt、comp 和 soc。点击类别，你可以逐步深入到特定的新闻组。在 Google Groups 中查看文章时，你可以点击一个链接以发布对该文章的跟进。

### 第 4 章：使用 FTP 传输文件

### 本章内容

- 使用 GNOME FTP 客户端
- 使用 Mozilla 网页浏览器作为 FTP 客户端
- 学习使用 FTP 命令

正如名称所示，*文件传输协议*（FTP）用于在计算机之间传输文件。例如，如果你的互联网服务提供商（ISP）为你提供个人网页的空间，你可能已经使用 FTP 上传网页了。使用计算机上的 FTP 客户端，你登录 ISP 账户，提供密码，然后将文件从你的本地系统复制到 ISP 的服务器。

你也可以使用 FTP 匿名下载其他文件，例如从互联网上其他计算机上的开源软件——在这种情况下，你不需要在远程系统上拥有账户即可下载文件。你只需使用单词 `anonymous` 作为用户名登录，并提供你的电子邮件地址作为密码（事实上，你的网页浏览器可以代表你完成此操作，因此你可能甚至不知道这正在发生）。这种匿名 FTP 对于向任何想要的人分发文件非常有用。例如，硬件供应商可能会使用匿名 FTP 为任何需要的人提供更新的设备驱动程序。

Red Hat Linux 附带了多个 FTP 客户端，既有命令行也有 GUI。在本章中，我向你介绍几个 GUI FTP 客户端，并对于命令行 FTP 客户端，我描述了用于操作远程目录的命令。

## 使用图形化 FTP 客户端

你可以在 Red Hat Linux 中使用以下 GUI FTP 客户端之一：

- gFTP — 一个图形化 FTP 客户端
- Mozilla 网页浏览器用于匿名 FTP 下载



上传文件时，你需要使用 gFTP，因为此类传输通常需要提供用户名和密码。Web 浏览器对于匿名下载效果很好，而这正是你通常从互联网下载软件的方式。

我将在接下来的两个章节中简要介绍这两种 GUI FTP 客户端。

## 使用 gFTP

GNOME 自带 gFTP，这是一款图形化 FTP 客户端。要启动 gFTP，请从 GNOME 或 KDE 桌面选择 主菜单→Internet→更多 Internet 应用→gFTP。gFTP 窗口出现（如图 4-1 所示）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_417_0.png)

图 4-1：
打开到远程 FTP 服务器的连接之前的 gFTP 窗口。

gFTP 窗口有一个菜单栏，其中包含用于执行各种任务的菜单。菜单栏正下方是一个工具栏，包含多个按钮和文本字段。在这里你可以输入远程主机的名称或 IP 地址、登录远程主机所需的用户名和密码。图 4-1 显示了你在填写这些信息后 gFTP 窗口的情形。

使用 gFTP 上传或下载文件，请按以下步骤操作：

- 1. 在 Host 字段中填写远程系统的主机名或 IP 地址。

如果你之前使用过该主机，可以从 Host 字段旁的向下指向箭头出现时显示的下拉列表中选择它。

- 2. **在 User 字段中提供用户名，在 Pass 字段中提供密码，然后单击显示两台计算机图标的按钮（位于 Host 字段左侧）。**

此操作会使 gFTP 连接到你选择的主机，并使用你提供的用户名和密码登录。gFTP 窗口的下半部分显示两台系统之间交换的 FTP 协议消息。

- 3. **观察此区域是否有任何错误消息的提示。**

远程系统的目录列表显示在 gFTP 窗口的右半部分。左半部分显示当前本地目录。

- 4. **要将一个或多个文件从当前系统上传到远程系统，请在左侧列表中选择文件，然后单击右箭头按钮。**

- 5. **要从远程系统下载文件，请在右侧列表中选择文件名，然后单击左箭头按钮。**

- 6. **完成文件传输后，从菜单中选择 FTP→Quit。**

如这些步骤所示，使用 gFTP 等 GUI FTP 客户端传输文件是一项简单的任务。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_418_0.png)

信不信由你，gFTP 不仅用于 FTP 传输。它还可以使用 HTTP 协议传输文件，并使用 Secure Shell（SSH）协议进行安全文件传输。

## 使用 Web 浏览器作为 FTP 客户端

任何 Web 浏览器都可以充当 FTP 客户端，但此类程序最适合匿名 FTP 下载，在这种情况下 Web 浏览器可以使用匿名用户名和任意密码登录。

在 Red Hat Linux 中，你可以使用 Mozilla Web 浏览器作为 FTP 客户端。你需要知道的全部是如何编写 URL，以便 Web 浏览器能够识别你想要使用 FTP 下载文件。FTP URL 的语法如下：

```
ftp://hostname/pathname
```

第一部分（ftp://）表示你想要进行 FTP 传输。hostname 部分应为 FTP 服务器的名称（名称通常以 ftp 开头——例如 ftp.netspace.com）。pathname 是你想要下载的文件的完整目录路径和文件名。

```
ftp://localhost
```

然后按 Enter。Mozilla 显示 Red Hat Linux 系统上匿名 FTP 目录的内容。图 4-2 显示了 Mozilla 中匿名 FTP 目录的典型外观。你可以单击文件夹查看其内容并下载任何文件。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_419_0.png)

图 4-2：
你可以使用 Mozilla 从匿名 FTP 服务器下载文件

![](img/a7eec43a54473e95dc5ea333fecf1bd7_419_1.png)

当你使用 `ftp://localhost` URL 时，如果你没有运行 FTP 服务器或已设置防火墙不允许任何 FTP 连接，则系统不会给出响应。在你的系统上，以 root 身份登录并在终端窗口中输入 `service vsftpd start` 来启动 FTP 服务器。

如果你输入其他匿名 FTP 服务器的主机名，采用相同的方法访问匿名 FTP 站点也是可行的。例如，尝试输入以下 URL：

```
ftp://ftp.netscape.com
```

你应该会得到 `ftp.netscape.com` 服务器的目录。

## 使用命令行 FTP 客户端

了解如何从命令行使用 FTP 是很有用的——以防万一。例如，你的 GUI 桌面可能无法工作，而你需要做的是下载一些文件来修复问题。如果你知道如何使用命令行 FTP 客户端，你就可以下载文件并解决问题。这并不难。

学习命令行 FTP 客户端的最佳方法是实际尝试一下。该命令称为 ftp，你可以在 Red Hat Linux 系统上尝试 ftp 命令。你甚至不需要任何 Internet 连接，因为你可以使用 ftp 命令连接到自己的系统——我会向你展示如何操作。

在下面的示例 FTP 会话中，我使用命令行 FTP 客户端使用我的用户名（naba）登录并浏览系统上的目录。当你尝试类似操作时，请将名称替换为你的用户名并提供你的密码。以下是显示命令的列表（我的注释以斜体显示）：

```
ftp localhost
Connected to localhost (127.0.0.1).
220 (vsFTPd 1.2.0)
Name (localhost:naba): (I press Enter.)
331 Please specify the password.
Password: (I type my password.)
230 Login successful. Have fun.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> help (I type help to see a list of FTP commands.)
Commands may be abbreviated. Commands are:
! debug mdir sendport site
$ dir mget put size
account disconnect mkdir pwd status
append exit mls quit struct
ascii form mode quote system
bell get modtime recv sunique
binary glob mput rget tenex
bye hash newer rstatus tick
case help nmap rhelp trace
cd idle nlist rename type
cdup image ntrans reset user
chmod lcd open prompt restart umask
close ls passive rmdir runique verbose
cr macdef mdelete proxy send
delete mdelete proxy send
ftp> help mget (I can get help on a specific command.)
mget get multiple files
ftp> cd /var/ftp (This changes directory to /var/ftp.)
250 Directory successfully changed.
ftp> ls (This command lists the contents of the directory.)
227 Entering Passive Mode (127,0,0,1,248,180)
150 Here comes the directory listing.
drwxr-xr-x 2 0 0 4096 Jun 26 05:10 pub
226 Directory send OK.
ftp> bye (This command ends the session.)
221 Goodbye.
```

如列表所示，你可以通过输入命令 ftp hostname 启动命令行 FTP 客户端，其中 hostname 是你想要访问的系统的名称。当 FTP 客户端与远程系统上的 FTP 服务器建立连接时，FTP 服务器会提示你输入用户名和密码。提供信息后，FTP 客户端会显示 ftp> 提示符，你可以开始输入命令执行特定任务。如果你记不起某个特定的 FTP 命令，输入 help 即可查看列表。你可以通过输入 help command 获取特定命令的额外帮助，其中 command 是你想要了解的内容。

许多 FTP 命令与用于浏览文件系统的 Linux 命令相似。例如，cd 更改目录，pwd 打印当前工作目录的名称，ls 列出当前目录的内容。另两个常见命令是 get 和 put——get 用于从远程系统下载文件到你的系统，put 则上传（发送）文件从你的系统到远程主机。

表 4-1 描述了一些常用的 FTP 命令。你不必输入完整的 FTP 命令。对于较长的命令，只需输入前几个字符——足以唯一标识该命令即可。例如，要删除文件，可以输入 dele，要将文件传输模式更改为二进制，可以输入 bin。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_421_0.png)

从互联网下载文件时，你几乎总是希望以二进制模式传输文件，因为软件通常以二进制形式归档和压缩（其文件不是纯文本文件）。因此，始终使用 binary 命令将模式设置为二进制。然后使用 get 命令下载文件。

表 4-1 常用 FTP 命令

| 命令 | 描述 |
|---|---|
| ! | 在本地系统上执行 shell 命令。例如，! ls 列出远程系统上当前目录的内容。 |
| ? | 显示命令列表（与 help 相同）。 |
| append | 将本地文件追加到远程文件。 |
| ascii | 将文件传输类型设置为 ASCII（或纯文本）。这是默认的文件传输类型。 |
| binary | 将文件传输类型设置为二进制。 |
| bye | 结束与远程 FTP 服务器的 FTP 会话并退出 FTP 客户端。 |
| cd | 更改远程系统上的目录。例如，cd /pub/Linux 将远程目录更改为 /pub/Linux。 |



| 命令 | 描述 |
|---|---|
| chmod | 更改远程文件的权限设置。例如，`chmod 644 index.html` 更改远程系统上 `index.html` 文件的权限设置。 |
| close | 结束与 FTP 服务器的 FTP 会话并返回到 FTP 客户端的提示符。 |
| delete | 删除远程文件。例如，`delete bigimage.jpg` 删除远程系统上的该文件。 |
| dir | 列出远程系统上当前目录的内容。 |
| disconnect | 结束 FTP 会话并返回到 FTP 客户端的提示符。（与 `close` 相同。） |
| get | 下载远程文件。例如，`get junk.tar.gz junk.tgz` 从远程系统下载文件 `junk.tar.gz` 并将其保存为本地系统上的文件 `junk.tgz`。 |
| hash | 打开或关闭显示文件传输进度的哈希标记（#）打印。当此功能打开时，每从远程系统传输 1,024 字节时会在屏幕上打印一个哈希标记。（它是命令行版的进度条。） |
| help | 显示命令列表。 |
| image | 与 `binary` 相同。 |
| lcd | 更改本地系统上的当前目录。例如，`lcd /var/ftp/pub` 将当前本地目录更改为 `/var/ftp/pub`。 |
| ls | 列出当前远程目录的内容。 |
| mdelete | 删除远程系统上的多个文件。例如，`mdelete *.jpg` 删除当前目录中名称以 `.jpg` 结尾的所有远程文件。 |
| mdir | 列出多个远程文件并将列表保存到指定的本地文件。例如，`mdir /usr/share/doc/* wlist` 将列表保存到名为 `wlist` 的本地文件。 |
| mget | 下载多个文件。例如，`mget *.jpg` 下载所有名称以 `.jpg` 结尾的文件。如果提示已打开，FTP 客户端会在每个文件下载前请求确认。 |
| mkdir | 在远程系统上创建目录。`mkdir images` 在远程系统当前目录中创建一个名为 `images` 的目录。 |
| mls | 与 `mdir` 相同。 |

## 表 4-1（续）

| 命令 | 描述 |
|---|---|
| mput | 上传多个文件。例如，mput *.jpg 将所有名称以 .jpg 结尾的文件发送到远程系统。如果提示已打开，FTP 客户端会在每个文件发送前请求确认。 |
| open | 打开与指定主机上 FTP 服务器的连接。例如，open ftp.netscape.com 连接到主机 ftp.netscape.com 上的 FTP 服务器。 |
| prompt | 打开或关闭提示。当提示打开时，在多文件传输期间，FTP 客户端会在下载或上传每个文件前提示您确认。 |
| put | 将文件发送到远程系统。例如，put index.html 将本地系统的 index.html 文件发送到远程系统。 |
| pwd | 显示远程系统上当前目录的完整路径名。当您以用户身份登录时，初始当前工作目录是您的主目录。 |
| quit | 与 bye 相同。 |
| recv | 与 get 相同。 |
| rename | 重命名远程系统上的文件。例如，rename old.html new.html 将远程系统上的文件 old.html 重命名为 new.html。 |
| rmdir | 删除远程系统上的目录。例如，rmdir images 删除远程系统当前目录中的 images 目录。 |
| send | 与 put 相同。 |
| size | 显示远程文件的大小。例如，size bigfile.tar.gz 显示该远程文件的大小。 |
| status | 显示 FTP 客户端的当前状态。 |
| user | 向 FTP 服务器发送新的用户信息。例如，user naba 发送用户名 naba；FTP 服务器然后提示该用户名的密码。 |

## 第六卷
### 管理
### 第五波

作者 Rich Tennant

![](img/a7eec43a54473e95dc5ea333fecf1bd7_424_0.png)

"这部分测试告诉我们你是否个人适合担任网络管理员的工作。"

## 目录一览

- 第 1 章：执行基本系统管理 .................................... 399
- 第 2 章：管理用户 ................................................... 427
- 第 3 章：管理文件系统 ........................................... 439
- 第 4 章：管理应用程序 .............................................. 463
- 第 5 章：管理设备和打印机 ...................................... 479
- 第 6 章：升级和自定义内核 ................................ 491

### 第 1 章：执行基本系统管理

### 本章内容

- 成为 `root`
- 了解系统启动过程
- 盘点系统配置文件
- 通过 `/proc` 文件系统查看系统信息
- 监控系统性能
- 安排作业

系统管理是指为保持计算机系统正常运行而必须完成的工作；系统管理员是指负责处理这些任务的人。

如果您在家或小型办公室运行 Red Hat Linux，您很可能是系统管理员。也许您是整个 LAN 满是 Red Hat Linux 系统的系统管理员。无论如何，在本章中，我向您介绍基本系统管理程序并向您展示如何执行一些常见任务。

Red Hat Linux 随附了不少用于执行特定系统管理任务的图形工具。我在本章中描述了其中一些工具，以及本迷你书的其他章节。

### 盘点系统管理任务

那么系统管理任务是什么？我脱口而出的回答是您为保持系统良好运行而必须做的一切。更准确地说，系统管理员的职责包括以下内容：

- **添加和删除用户账户。** 您必须添加新的用户账户并删除不必要的用户账户。如果用户忘记密码，您必须更改密码。
- **管理打印系统。** 您必须打开或关闭打印队列，检查打印队列状态，并在必要时删除打印作业。
- **安装、配置和升级操作系统和各种实用程序。** 您必须安装或升级 Linux 操作系统的部分内容以及其他软件包。
- **安装新软件。** 您必须安装以 Red Hat Package Manager（RPM）文件形式提供的软件。您还必须下载并解包以源代码形式提供的软件——然后从源代码构建可执行程序。
- **管理硬件。** 有时您必须添加新硬件并安装驱动程序，以便设备正常工作。
- **制作备份。** 您必须备份文件，要么存放在 Zip 驱动器中，要么存放在磁带上（如果您有磁带驱动器）。
- **挂载和卸载文件系统。** 当您想要访问 CD-ROM（例如）上的文件时，您必须将该 CD-ROM 的文件系统挂载到 Linux 文件系统中的一个目录上。您还必须挂载软盘，包括 Linux 格式和 DOS 格式。
- **自动化任务。** 您必须安排 Linux 任务在特定时间自动执行，或安排人员定期执行的作业。
- **监控系统性能。** 您可能希望关注系统性能，以了解处理器大部分时间花费在何处，并查看系统中空闲和已用内存的数量。
- **启动和关闭系统。** 尽管启动系统通常只需打开 PC 电源，但您在想要关闭 Linux 系统时必须小心一些。如果您的系统设置为图形登录屏幕，您可以通过从登录屏幕中选择菜单项来执行关机操作。否则您应该使用 `shutdown` 命令停止所有程序，然后再关闭 PC 的电源开关。
- **监控网络状态。** 如果您拥有网络存在（无论是 LAN、DSL 线路还是有线调制解调器连接），您可能希望检查各种网络接口的状态并确保网络连接正常运行。
- **设置主机和网络安全。** 您必须确保系统文件受到保护并保护系统免受网络攻击。
- **监控安全。** 您必须留意任何入侵，通常通过检查日志文件。




这是一份很长的任务清单！本章不会涵盖所有内容，但迷你书的其余部分描述了其中大部分任务。在这里，我重点介绍一些基础知识，例如如何成为 root（超级用户）、学习设置系统配置文件、监控系统性能以及设置周期性任务。

## 如何成为 root

您必须以 root 身份登录才能执行系统管理任务。root 用户是超级用户，也是唯一拥有在系统中执行任何操作所需全部权限的账户。

普遍的说法是您不应通常以 root 身份登录。这是因为当您是 root 时，一个小错误就可能导致您轻易删除所有文件——尤其是在输入命令时。例如，您可能会输入命令 rm * .html 来删除所有具有 .html 扩展名的文件。

如果您不小心在星号 (*) 后按了空格键怎么办？shell 会将命令解释为 rm * .html，并且——因为 * 匹配任何文件名——会删除当前目录中的所有内容。直到发生在您身上之前，这似乎难以置信！

## 使用 su - 命令

如果您以普通用户登录，该如何执行系统管理任务呢？好吧，您暂时成为 root。

如果您正在终端窗口或控制台工作，请输入

```
su -
```

然后在提示时输入 root 密码。从此时起，您就是 root。做您需要做的任何事。要返回到您通常的用户身份，请输入

```
exit
```

就这样！就是这么简单。

## 为 GUI 实用程序成为 root

如果您使用 Red Hat 的任何 GUI 实用程序来执行系统管理任务，那就更简单了。通常，实用程序会弹出一个对话框提示您输入 root 密码（如图 1-1 所示）。只需输入密码并按 Enter 即可。如果您不想使用该实用程序，请单击关闭。

图 1-1：
输入 root 密码并按 Enter 以获得 root 权限。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_429_0.png)

## 恢复被遗忘的 root 密码

要执行系统管理任务，您必须知道 root 密码。如果您忘记了 root 密码会怎样？不用担心：只需重新启动 PC 并按照以下步骤重置 root 密码即可：

- **1. 重启 PC（在退出 GUI 屏幕时选择重启）或像往常一样开机。**

不久您会看到图形 GRUB 启动加载器屏幕，显示可启动的操作系统名称。

- **2. 如果安装了多个操作系统，请使用箭头键选择 Red Hat Linux 作为您的操作系统。然后按 *a*（仅字母“a”）。**

GRUB 会提示您输入要添加到其默认启动命令中的命令。

- **3. 按空格键，输入以下内容，然后按 Enter：**

`nogui single`

这会导致 Linux 像往常一样启动，但在无需登录的单用户模式下运行。`nogui` 命令会导致系统启动时显示文本启动消息而不是 GUI 屏幕。Linux 启动后，您会看到以下命令行提示符：

`sh-2.05b#`

- **4. 使用 `passwd` 命令按如下方式更改 root 密码：**

`sh-2.05b# passwd`
正在更改 root 用户的密码。
新密码：

- **5. 输入您想要使用的新 root 密码（屏幕上不会显示），然后按 Enter。**

Linux 会再次要求输入密码，如下所示：

`Retype new password:`

- **6. 再次输入密码，然后按 Enter。**

如果您两次输入相同的密码，passwd 命令会更改密码并显示以下消息：

```
passwd: all authentication tokens updated successfully.
```

- **7. 现在输入 reboot 以重启 PC。**

Linux 启动后，它会显示熟悉的登录屏幕。现在您应该能够使用新密码以 root 身份登录。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_430_0.png)

确保您的 Red Hat Linux PC 物理安全。正如此过程所示，任何能够物理访问您的 Red Hat Linux PC 的人都可以简单地重新启动，设置新的 root 密码，并对系统做任何他们想做的事。防止重置密码的另一种方法是设置 GRUB 密码，这会导致 GRUB 在启动 Red Hat Linux 之前要求输入有效密码。当然，然后您必须在每次启动系统时记住并输入 GRUB 密码！

## 了解 Red Hat Linux 如何启动

了解 Red Hat Linux 在启动时按什么顺序启动进程很重要。您可以使用这些知识来启动和停止服务，例如 Web 服务器和网络文件系统（NFS）。接下来的几节为您提供 Red Hat Linux 如何启动并启动初始进程集的概述。这些部分还让您熟悉启动 Red Hat Linux 系统上各种服务的 shell 脚本。

## 了解 init 进程

当 Red Hat Linux 启动时，它会从硬盘加载并运行核心操作系统程序。核心操作系统设计用于运行其他程序。一个名为 init 的进程启动 Linux 系统上的初始进程集。

```
ps ax | more
```

您会得到一个输出列表，开始如下所示：

```
PID TTY   STAT TIME COMMAND
  1 ?     S    0:03 init
```

第一列，标题为 PID，为每个进程显示一个数字。PID 代表进程 ID（标识）——由 Linux 内核分配的顺序号。进程列表中 PID 为 1 的第一项是 init 进程。它是第一个进程，并启动 Red Hat Linux 系统中的所有其他进程。这就是为什么 init 有时被称为“所有进程之母”。

init 进程启动的内容取决于以下因素：

- 运行级别，一个标识符，用于标识仅选定组进程可以存在的系统配置
- `/etc/inittab` 文件的内容，一个文本文件，指定在不同运行级别启动哪些进程
- 若干 shell 脚本（位于 `/etc/rc.d` 目录及其子目录中），在特定运行级别执行

有七个运行级别——0 到 6——表 1-1 显示了它们的含义。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_431_0.png)

表 1-1 Red Hat Linux 中的运行级别

| 运行级别 | 含义 |
|---|---|
| 0 | 关闭系统 |
| 1 | 以单用户独立模式运行（其他人无法登录；您在文本控制台工作） |
| 2 | 以无网络服务的多用户模式运行（在多用户模式下，其他用户可以登录） |
| 3 | 以完整多用户模式运行，但使用文本模式登录 |
| 4 | Red Hat Linux 中未使用 |
| 5 | 所有服务运行且图形登录已启用 |
| 6 | 重启系统 |

当前运行级别与 `/etc/inittab` 文件的内容一起控制 init 启动哪些进程。初始默认运行级别为文本模式登录屏幕的 3 和图形登录屏幕的 5。您可以通过编辑 `/etc/inittab` 文件中的一行来更改默认运行级别。

要检查当前运行级别，请在终端窗口中输入以下命令：

```
/sbin/runlevel
```

runlevel 命令应打印如下输出：

```
N 5
```

输出的第一个字符显示之前的运行级别（N 表示没有之前的运行级别），第二个字符显示当前的运行级别（5）。在这种情况下，系统是在运行级别 5 下启动的。

## 检查 /etc/inittab 文件

/etc/inittab 文件是理解 init 在各种运行级别启动的进程的关键。您可以使用 more 命令查看文件的内容，如下所示：

```
more /etc/inittab
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_432_0.png)

使用 more 命令查看 /etc/inittab 文件的内容时，您不必以 root 身份登录。

要解释 /etc/inittab 文件的内容，请按照以下步骤操作：

- **1. 查找看起来像这样的行：**
```
id:5:initdefault:
```
该行显示默认运行级别。在本例中为 5。

- **2. 查找所有指定 init 在运行级别 5 应运行的内容的行。查找第一个冒号和第二个冒号之间有 5 的行。以下是两个相关行：**
```
l5:5:wait:/etc/rc.d/rc 5
x:5:respawn:/etc/X11/prefdm -nodaemon
```
第一行指定 init 应执行文件 /etc/rc.d/rc，并以 5 作为参数。第二行导致 init 运行 /etc/X11/prefdm，这是一个启动图形显示管理器的 shell 脚本。显示管理器反过来显示图形登录对话框，使您能够登录系统。

如果您查看文件 /etc/rc.d/rc，您会发现它是一个 shell 脚本。您可以研究此文件以了解它如何为运行级别 1 到 5 启动各种进程。

/etc/inittab 文件中的每个条目都告诉 init 在一个或多个运行级别下做什么——您只需列出进程应运行的所有运行级别。每个 inittab 条目有四个字段——用冒号分隔——格式如下：

```
id:runlevels:action:process
```



表 1-2 显示了这些字段各自的含义。

表 1-2 inittab 条目中各字段的含义

| Field | Meaning |
|---|---|
| id | 一个唯一的一到两个字符的标识符。init 进程在内部使用此字段。您可以使用任何想要的标识符，只要不在多行上使用相同的标识符即可。 |
| runlevels | 零个或多个字符的序列，每个字符表示一个运行级别。例如，如果 runlevels 字段为 12345，则该条目适用于 1 到 5 的每个运行级别。如果 action 字段设置为 sysinit、boot 或 bootwait，则忽略此字段。 |
| action | 告诉 init 进程对该条目执行什么操作。例如，如果此字段为 initdefault，init 会将 runlevels 字段解释为默认运行级别。如果此字段设置为 wait，init 会启动 process 字段指定的程序或脚本并等待该进程退出。 |
| process | init 需要启动的脚本或程序的名称。当然，action 字段的一些设置不需要 process 字段。例如，当 action 为 initdefault 时，无需 process 字段。 |

## 使用 init 命令尝试新的运行级别

要尝试新的运行级别，您不必更改 /etc/inittab 文件中的默认运行级别。如果以 root 身份登录，您可以通过键入 init 后跟运行级别（通常为 1、3 或 5）来更改运行级别（从而更改 Red Hat Linux 中运行的进程）。

例如，要将系统置于单用户模式，请键入以下内容：

```
init 1
```

因此，如果您想在不更改 /etc/inittab 文件的情况下尝试运行级别 5（假设您的系统尚未设置图形登录屏幕），请在 shell 提示符下输入以下命令：

```
init 5
```

系统应结束所有当前进程并进入运行级别 5。默认情况下，init 命令会在停止所有当前进程并启动运行级别 5 的新进程之前等待 20 秒。

要立即切换到运行级别 5，请键入命令 init -t 0 5。-t 选项后的数字表示 init 在更改运行级别之前等待的秒数。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_433_0.png)

您还可以使用 telinit 命令，它只是指向 init 的符号链接（快捷方式）。如果您对 /etc/inittab 文件进行了更改并希望 init 重新加载其配置文件，请使用命令 telinit q。

## 了解 Red Hat Linux 启动脚本

init 进程在系统启动时运行多个脚本。如果查看 /etc/inittab 文件，您会在文件开头附近找到以下行：

```
# System initialization.
si::sysinit:/etc/rc.d/rc.sysinit
```

第一行是注释行。第二行导致 init 运行 /etc/rc.d/rc.sysinit 脚本——init 运行的第一个 Red Hat Linux 启动脚本。rc.sysinit 脚本执行许多初始化任务，例如挂载文件系统、设置时钟、配置键盘布局、启动网络以及加载许多其他驱动模块。rc.sysinit 脚本通过调用许多其他脚本并读取位于 /etc/sysconfig 目录中的配置文件来执行这些初始化任务。

执行 /etc/rc.d/rc.sysinit 脚本后，init 进程会使用运行级别作为参数运行 /etc/rc.d/rc 脚本。例如，对于运行级别 5，/etc/inittab 中的以下行指定了 init 需要执行的内容：

```
15:5:wait:/etc/rc.d/rc 5
```

这表示 init 应执行命令 /etc/rc.d/rc 5 并等待该命令完成。

/etc/rc.d/rc 脚本有点复杂。它的工作原理如下：

- 它切换到与运行级别对应的目录。例如，要切换到运行级别 5，脚本会切换到 /etc/rc.d/rc5.d 目录。
- 在与运行级别对应的目录中，/etc/rc.d/rc 查找所有以 K 开头的文件并使用参数 stop 执行每个文件。这会终止当前正在运行的进程。然后它定位所有以 S 开头的文件并使用参数 start 执行每个文件。这会启动指定运行级别所需的进程。

要查看运行级别 5 执行了什么，请键入以下命令：

```
ls -l /etc/rc.d/rc5.d
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_435_0.png)

在 resulting listing 中，K 脚本——文件名以 K 开头的文件——停止（“kill”）服务器，而 S 脚本启动服务器。`/etc/rc.d/rc` 脚本按它们在目录列表中出现的确切顺序执行这些文件。

名称为 `/etc/rc.d/rc.local` 的脚本在所有其他脚本之后执行。因此，您可以在该脚本中放置任何您希望在 Red Hat Linux 系统启动时执行的命令。

## 手动启动和停止服务器

大多数服务器启动脚本位于 `/etc/init.d` 目录中（脚本实际位于 `/etc/rc.d/init.d`，但 `/etc/init.d` 是指向 `/etc/rc.d/init.d` 的快捷方式）。您可以手动调用此目录中的脚本来启动、停止或重启特定进程——通常是服务器。例如，要停止 Web 服务器（服务器程序称为 `httpd`），请键入以下命令：

```
/etc/rc.d/init.d/httpd stop
```

如果 `httpd` 已在运行并且您想重启它，请键入以下命令：

```
/etc/init.d/httpd restart
```

您可以通过熟悉 `/etc/init.d` 目录中的脚本来提高系统管理技能。要查看其列表，请键入以下命令：

```
ls /etc/init.d
```

例如，以下是我的系统中的典型脚本列表：

```
aep1000 functions keytable nfs lock saslauthd tux
anacron gpm killall nscd sendmail vsftpd
atd help kudu ntpd single winbind
autofs innd lisa pcmcia smartd xfs
bcm5820 iptables named postgresql smmp ypbid
cqarrayd irqbalance netfs random squid smmptrapd ypbind
crond isdn network rawdevices sshd ypserv
cups lvm nfs rhsm syslog
firstboot kdcrotate nfs rhsm syslog
```

脚本名称可以让您大致了解脚本可以启动和停止哪个服务器。例如，nfs 脚本启动和停止 NFS（网络文件系统）服务所需的进程。您可以在空闲时研究其中一些脚本以了解每个脚本的作用。您不必理解所有 shell 编程；注释应有助于您了解每个脚本的目的。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_436_0.png)

使用 service 命令作为快捷方式来运行 /etc/init.d 中的脚本，您可以使用这些脚本来启动、停止或重启服务器。例如，要启动 Web 服务器，您键入此命令：

```
service httpd stop
```

要重启该服务器，请键入以下命令：

```
service httpd restart
```

## 在系统启动时自动启动服务器

您希望某些服务器在每次启动系统时自动启动。例如，如果您运行 Web 服务器，您希望 httpd 服务器在系统启动时启动。您可以使用 chkconfig 命令来实现。例如，要设置 httpd 在系统启动到运行级别 3、4 或 5 时启动，请键入以下命令（以 root 登录时）：

```
chkconfig --level 345 httpd on
```

您还可以使用 chkconfig 命令检查哪些服务器已打开或关闭。例如，要查看所有运行级别的所有服务器的完整列表，请键入以下命令：

```
chkconfig --list
```

如果您想查看单个服务器（如 httpd）的状态，请将该服务器的名称添加到 chkconfig 命令中，如下所示：

```
chkconfig --list httpd
```

您应该会看到类似以下内容的输出：

```
httpd 0:off 1:off 2:off 3:on 4:on 5:on 6:off
```

## 盘点 Red Hat Linux 系统配置文件

Red Hat Linux 包含大量配置文件。所有这些文件都是可以用任何文本编辑器编辑的文本文件。要编辑这些配置文件，您必须以 root 身份登录。我不会单独讨论这些文件，但我在表 1-3 中展示了一些配置文件，并附带每个文件的简要描述。此列表让您了解系统管理员需要处理哪些类型的配置文件。在许多情况下，Red Hat Linux 包含 GUI 实用程序来设置其中许多配置文件。

表 1-3 Red Hat Linux 配置文件

| Configuration File | Description |
|---|---|
| /boot/module-info | Linux 内核的模块信息 |
| /boot/System.map | Linux 内核的映射（将内核地址映射为函数和变量的名称） |
| /boot/vmlinuz | Linux 内核（这是操作系统的核心） |
| /etc/X11/XF86Config | XFree86 4.x 版本的配置文件 |
| /etc/at.allow | 允许使用 at 命令安排稍后执行的作业的用户用户名 |
| /etc/at.deny | 被禁止使用 at 命令的用户用户名 |
| /etc/bashrc | BASH shell 的系统范围函数和别名 |
| /etc/cups/cupsd.conf | Common UNIX Printing System (CUPS) 调度器的打印机配置文件 |
| /etc/fstab | 可用于挂载的文件系统信息 |
| /etc/group | 关于组的信息 |
| /etc/grub.conf | Grand Unified Bootloader (GRUB) 的配置——Red Hat Linux 中的默认引导加载程序 |
| /etc/hosts | IP 号码及其对应主机名的列表 |
| /etc/hosts.allow | 允许访问此系统上 Internet 服务的主机 |
| /etc/hosts.deny | 被禁止访问此系统上 Internet 服务的主机 |
| /etc/httpd/conf/httpd.conf | Apache Web 服务器的配置文件 |
| /etc/init.d | 包含用于启动和停止许多服务器的脚本的目录 |





| Configuration File | Description |
|---|---|
| /etc/inittab | init 进程使用的配置文件，用于启动所有其他进程 |
| /etc/issue | 文件包含在显示文本模式登录提示之前打印的消息（通常是 Red Hat Linux 版本号） |
| /etc/lilo.conf | Linux Loader（LILO）的配置——可从磁盘加载操作系统的引导加载程序之一 |
| /etc/login.defs | 创建用户账户的默认信息，由 useradd 命令使用 |
| /etc/modules.conf | 包含加载内核模块指令的配置文件（例如以太网和声音驱动程序） |
| /etc/mtab | 关于当前已挂载文件系统的信息 |
| /etc/passwd | 关于所有用户账户的信息（实际密码存储在 /etc/shadow 中） |
| /etc/profile | BASH shell 的系统范围环境和启动文件 |
| /etc/rc.d | 存放 Red Hat Linux 系统启动和关闭脚本的目录 |
| /etc/rc.d/rc.sysinit | Red Hat Linux 初始化脚本 |
| /etc/shadow | 包含所有用户账户加密密码的安全文件 [只能由 root 读取] |
| /etc/shells | 系统上用户可用的所有 shell 的列表 |
| /etc/skel | 存放诸如 .bash_profile 等文件初始版本的目录，这些文件会被复制到新用户的主目录 |
| /etc/sysconfig | Red Hat Linux 配置文件 |
| /etc/termcap | 终端功能和选项数据库 |
| /etc/xinetd.conf | 按需启动多个 Internet 服务的 xinetd 守护进程的配置 |
| /var/log/cron | 运行计划任务的 cron 进程的消息日志文件 |
| /var/log/httpd/access_log | Web 服务器访问日志 |
| /var/log/httpd/error_log | Web 服务器错误日志 |
| /var/log/messages | 系统日志 |

## Monitoring System Performance

监控系统性能

When you're the system administrator, you must keep an eye on how well your Red Hat Linux system is performing. You can monitor the overall performance of your system by looking at information such as

作为系统管理员，您必须密切关注 Red Hat Linux 系统的运行状况。您可以通过查看以下信息来监控系统的整体性能，例如

- Central Processing Unit (CPU) usage
- Physical memory usage
- Virtual memory (swap space) usage
- Hard-drive usage

- 中央处理器（CPU）使用情况
- 物理内存使用情况
- 虚拟内存（交换空间）使用情况
- 硬盘使用情况

Red Hat Linux comes with a number of utilities you can use to monitor one or more of these performance parameters. Here I introduce a few of these utilities and show you how to understand the information presented by these utilities.

Red Hat Linux 附带了许多可用于监控一个或多个这些性能参数的实用程序。在这里我介绍其中几个实用程序，并向您展示如何理解这些实用程序提供的信息。

### Using the top utility

使用 top 实用程序

To view the top CPU processes — the ones that are using most of the CPU time — you can use the text mode top utility. To start that utility, type top in a terminal window (or text console). The top utility then displays a text screen listing the current processes, arranged in the order of CPU usage, along with various other information, such as memory and swap space usage. Figure 1-2 shows a typical output from the top utility.

要查看占用 CPU 时间最多的 top CPU 进程，您可以使用文本模式 top 实用程序。要启动该实用程序，在终端窗口（或文本控制台）中输入 top。top 实用程序随后会显示一个文本屏幕，列出当前进程，按 CPU 使用情况排序，并附带其他各种信息，例如内存和交换空间使用情况。图 1-2 显示了 top 实用程序的典型输出。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_439_0.png)

The top utility updates the display every 5 seconds. If you keep top running in a window, you can continually monitor the status of your Red Hat Linux system. To quit top, press Ctrl+C or close the terminal window.

top 实用程序每 5 秒更新一次显示。如果您在窗口中保持 top 运行，可以持续监控 Red Hat Linux 系统的状态。要退出 top，请按 Ctrl+C 或关闭终端窗口。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_439_1.png)

Figure 1-2
You can see the top CPU processes by using the top utility.

图 1-2
您可以使用 top 实用程序查看 top CPU 进程。

The first six lines of the output screen (refer to Figure 1-2) provide summary information about the system. Here is what these six lines show:

输出屏幕的前六行（参见图 1-2）提供了有关系统的摘要信息。以下是这六行显示的内容：

- The first line shows the current time, how long the system has been up, how many users are logged in, and three load averages — the average number of processes ready to run during the last 1, 5, and 15 minutes.
- 第一行显示当前时间、系统已运行的时间、已登录的用户数以及三个负载平均值——过去 1、5 和 15 分钟内准备运行的进程的平均数量。
- The second line lists the total number of processes and the status of these processes.
- 第二行列出进程总数以及这些进程的状态。
- The third line shows CPU usage — what percentage of CPU time is used by user processes, what percentage by system (kernel) processes, and during what percentage of time the CPU is idle.
- 第三行显示 CPU 使用情况——用户进程使用多少百分比的 CPU 时间，系统（内核）进程使用多少百分比，以及 CPU 空闲的百分比。
- The fourth and fifth lines show how the physical memory is being used — the total amount, how much is used, how much is free, how much is shared, and how much is allocated to buffers (for reading from disk, for example).
- 第四行和第五行显示物理内存的使用情况——总量、使用量、空闲量、共享量以及分配给缓冲区（例如从磁盘读取）的量。
- The sixth line shows how the virtual memory (or swap space) is being used — the total amount of swap space, how much is used, how much is free, and how much is being cached.
- 第六行显示虚拟内存（或交换空间）的使用情况——交换空间总量、使用量、空闲量以及被缓存的量。

The table that appears below the summary information (refer to Figure 1-2) lists information about the current processes, arranged in decreasing order by amount of CPU time used. Table 1-4 summarizes the meanings of the column headings in the table that top displays.

出现在摘要信息下方（参见图 1-2）的表格列出了有关当前进程的信息，按使用的 CPU 时间量递减顺序排列。表 1-4 总结了 top 显示的表格中列标题的含义。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_440_0.png)

If the RSS field is drastically smaller than the SIZE field for a process, the process is using too little physical memory compared to what it needs. The result is a lot of swapping as the process runs. You can use the vmstat utility (which I discuss later in this section) to find out how much your system is swapping.

如果进程的 RSS 字段远小于 SIZE 字段，则该进程使用的物理内存相对于其需求来说太少。其结果是进程运行时会进行大量交换。您可以使用 vmstat 实用程序（我在本节后面讨论）来了解系统的交换量。

Table 1-4 Meanings of Column Headings in top Utility's Output

表 1-4 top 实用程序输出中列标题的含义

| Heading | Meaning |
|---|---|
| PID | 进程的进程 ID |
| USER | 进程正在运行的用户名 |
| PRI | 进程的优先级 |
| NI | 进程的 Nice 值——值范围从 -20（最高优先级）到 19（最低优先级），默认值为 0 |
| SIZE | 进程的总大小，以千字节为单位 |
| RSS | 任务使用的总物理内存（通常以千字节显示，但 M 后缀表示兆字节） |

Table 1-4 (continued)

表 1-4（续）

| Heading | Meaning |
|---|---|
| SHARE | 进程使用的共享内存量 |
| STAT | 进程的状态（S 表示睡眠，D 表示不可中断睡眠，R 表示运行，Z 表示僵尸——本应死亡但仍在运行的进程——或 T 表示停止；尾随的 < 表示进程具有负 Nice 值） |
| %CPU | 自上次屏幕更新以来使用的 CPU 时间百分比 |
| %MEM | 进程使用的物理内存百分比 |
| TIME | 进程启动以来使用的总 CPU 时间 |
| CPU | 进程正在运行的处理器（如果系统只有一个处理器，则该字段始终为零） |
| COMMAND | 启动进程的命令的简短形式 |

### Using the GNOME system monitor

使用 GNOME 系统监视器

Like the text mode top utility, the GNOME System Monitor tool also enables you to view the system load in terms of the number of processes that are currently running, their memory usage, and the free disk space on your system. To run the tool, select Main Menu→System Tools→System Monitor. The tool starts and displays its output in a window, as shown in Figure 1-3.

与文本模式 top 实用程序类似，GNOME 系统监视器工具也允许您以当前正在运行的进程数量、其内存使用情况以及系统上的可用磁盘空间来查看系统负载。要运行该工具，请选择 主菜单→系统工具→系统监视器。工具启动并在窗口中显示其输出，如图 1-3 所示。

The output is similar to the output you see when you type top in a text-mode console or a terminal window, except that with the System Monitor, you can decide which columns you want to see. Figure 1-3 shows the default view (the Process Listing tab) with the process name, user who is running the process, memory used, percentage of CPU time, and the process ID. The GNOME System Monitor keeps updating the display to reflect the current state of the system.

输出与在文本模式控制台或终端窗口中输入 top 时看到的输出类似，只是使用系统监视器时，您可以决定要查看哪些列。图 1-3 显示了默认视图（进程列表选项卡），其中包含进程名称、运行进程的用户、使用的内存、CPU 时间百分比和进程 ID。GNOME 系统监视器会不断更新显示以反映系统的当前状态。

The GNOME System Monitor window has another tab labeled System Monitor. Click that tab to view a summary of CPU, memory, and disk usage. Figure 1-4 shows a typical view of the System Monitor tab.

GNOME 系统监视器窗口还有另一个标签页，标记为系统监视器。单击该标签页可查看 CPU、内存和磁盘使用情况的摘要。图 1-4 显示了系统监视器标签页的典型视图。

The upper plot in Figure 1-4 shows the percentage of CPU usage with time. The next plot shows the history of memory use and swap space use. Disk space use is summarized in a table at the bottom.

图 1-4 中的上部图表显示了随时间变化的 CPU 使用百分比。下一个图表显示了内存使用和交换空间使用的历史记录。磁盘空间使用情况在底部的表格中进行了汇总。

### Using the uptime command

使用 uptime 命令

You can use the uptime command to get a summary of the system's state. Just type the command like this:

您可以使用 uptime 命令获取系统状态的摘要。只需像这样输入命令：

```
uptime
```

It displays output similar to the following:

它会显示类似以下内容的输出：

```
15:03:21 up 32 days, 57 min, 3 users, load average: 0.13, 0.23, 0.27
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_442_0.png)

Figure 1-3: Use the GNOME System Monitor to view information about the current processes.

图 1-3：使用 GNOME 系统监视器查看有关当前进程的信息。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_442_1.png)

Figure 1-4: GNOME System Monitor displays summary CPU, memory, and disk usage information.

图 1-4：GNOME 系统监视器显示摘要 CPU、内存和磁盘使用信息。




此输出显示当前时间、系统已运行的时间、用户数量，以及（最后）三个负载平均值——过去 1、5 和 15 分钟内准备运行的进程的平均数量。负载平均值大于 1 表示许多进程同时竞争 CPU 时间。

负载平均值可指示系统繁忙程度。

## 使用 vmstat 工具

你可以使用 vmstat 工具获取有关整体系统使用情况的汇总信息。若要查看按 5 秒间隔平均的系统使用信息，请键入以下命令（第二个参数表示 vmstat 应显示的输出行总数）：

```
vmstat 5 8
```

你应该会看到与以下列表类似的输出：

```
procs swap memory swap bi io system cpu
r b w swpd free buff cache si so bi bo in cs us sy id
1 0 0 0 54652 10620 115648 0 0 123 25 123 212 3 1 96
0 0 0 0 54644 10628 115648 0 0 0 7 108 239 2 0 98
1 0 0 0 54628 10636 115656 0 0 2 3 149 359 5 1 94
0 0 0 0 54244 10644 115956 0 0 0 173 547 13 3 84
2 0 0 0 53748 10668 116280 0 0 60 27 154 652 18 2 80
2 0 1 0 48536 10704 121488 0 0 1046 78 151 508 68 3 29
0 1 0 0 46576 10740 123536 0 0 411 114 162 634 13 2 85
2 0 0 0 45096 10752 123828 0 0 59 10 111 584 10 2 87
```

输出的第一行显示自上次重启以来的平均值。之后，vmstat 再显示七次 5 秒平均数据，涵盖接下来的 35 秒。表格输出按六类信息分组，由输出第一行中的字段指示。第二行显示每个主要字段的进一步详细信息。你可以使用表 1-5 来解释这些字段。

表 1-5 vmstat 工具输出中字段的含义

| 字段名称 | 描述 |
|------------|-------------|
| procs | 进程数量及其类型：r = 等待运行的进程；b = 不可中断睡眠中的进程；w = 已换出但准备运行的进程 |
| memory | 物理内存和交换空间使用情况的信息（所有数字均以千字节为单位）：swpd = 已使用的虚拟内存；free = 空闲物理内存；buff = 用作缓冲区的内存；cache = 已缓存的虚拟内存 |
| swap | 交换量（数字以每秒千字节为单位）：si = 从磁盘换入的内存量；so = 换出到磁盘的内存量 |
| io | 输入输出信息（数字以每秒块数为单位，其中块大小取决于磁盘设备）：bi = 发送到磁盘的块速率；bo = 从磁盘接收的块速率 |
| system | 系统信息：in = 每秒中断数（含时钟中断）；cs = 每秒上下文切换次数——内核更改正在运行进程的次数 |
| cpu | CPU 时间使用百分比：us = 用户进程使用的 CPU 时间百分比；sy = 系统进程使用的 CPU 时间百分比；id = CPU 空闲时间的百分比 |

![](img/a7eec43a54473e95dc5ea333fecf1bd7_444_0.png)

在 vmstat 工具的输出中，si 和 so 字段中的高值表示交换过多（交换是指在物理内存和硬盘上的虚拟内存之间复制信息）。bi 和 bo 字段中的高数值表示磁盘活动过多。

## 检查磁盘性能和磁盘使用情况

Red Hat Linux 附带 `/sbin/hdparm` 程序，你可以使用它来控制大多数 PC 上常见的 IDE 或 ATAPI 硬盘。hdparm 程序的一个功能是，你可以使用 `-t` 选项来确定数据从磁盘读入内存缓冲区中的速率。例如，以下是我的系统上该命令的结果：

/sbin/hdparm -t /dev/hda

/dev/hda:
    Timing buffered disk reads:  64 MB in  3.04 seconds = 21.05 MB/sec

该命令需要 IDE 驱动器的设备名称（`/dev/hda`）作为参数。如果您有 IDE 硬盘，可以尝试此命令来查看可以从系统磁盘驱动器读取数据的速度。

要显示当前已挂载文件系统中的可用空间，请使用 df 命令。如果您想要更易读的 df 输出，请键入以下命令：

```
df -h
```

以下是此命令的典型输出：

```
Filesystem    Size  Used Avail Use% Mounted on
/dev/hda5     7.1G  4.0G  2.8G  59% /
/dev/hda3      99M   14M   80M  15% /boot
none          125M     0  125M   0% /dev/shm
```

正如本示例所示，-h 选项会导致 df 命令以千兆字节（G）和兆字节（M）显示大小。

要检查特定目录使用的磁盘空间，请使用 du 命令——您可以指定 -h 选项以千字节（k）和兆字节（M）查看输出，如以下示例所示：

```
du -h /var/log
```

以下是该命令的典型输出：

```
4.0K  /var/log/vbox
4.0K  /var/log/httpd
4.0K  /var/log/squid
4.0K  /var/log/samba
9.0M  /var/log/cups
480K  /var/log/gdm
4.0K  /var/log/news/OLD
8.0K  /var/log/news
11M   /var/log
```

du 命令显示每个目录使用的磁盘空间，最后一行显示该目录使用的总磁盘空间。如果您只想查看目录使用的总空间，请使用 -s 选项，如下所示：

```
du -s /home
```

```
25M   /home
```

## 通过 /proc 文件系统查看系统信息

您的 Red Hat Linux 系统有一个名为 /proc 文件系统的特殊文件系统。您可以通过此文件系统了解有关系统的许多信息。事实上，您甚至可以通过 /proc 文件系统更改内核参数（只需向该文件系统中的文件写入），从而修改系统的行为。

/proc 文件系统不是磁盘上的真实目录，而是由 Linux 内核管理的内存中的数据结构集合，对您来说表现为一组目录和文件。/proc 的用途（也称为进程文件系统）是让您访问有关 Linux 内核的信息，并帮助您了解系统上当前运行的所有进程。

您可以像访问任何其他目录一样访问 /proc 文件系统，但您需要了解各种文件的含义才能解释信息。通常，您可以使用 cat 或 more 命令查看 /proc 中文件的内容；文件的内容提供有关系统某些方面的信息。

与任何目录一样，首先查看 /proc 的详细目录列表。为此，请以 root 身份登录并在终端窗口中键入 ls -l /proc。在输出中，第一组目录（以行开头字母 d 表示）代表当前在系统上运行的进程。每个对应于进程的目录都以进程 ID（一个数字）作为其名称。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_446_0.png)

还请注意一个名为 /proc/kcore 的非常大的文件；该文件代表系统的整个物理内存。虽然 /proc/kcore 在列表中显示为一个巨大的文件，但没有单个物理文件占用硬盘上那么多空间——因此不要尝试删除该文件以回收磁盘空间。

/proc 中的几个文件和目录包含有关您的 Red Hat Linux PC 的有趣信息。例如，/proc/cpuinfo 文件列出了系统的关键特性，例如处理器类型和浮点处理器信息。您可以通过键入 cat /proc/cpuinfo 来查看处理器信息。例如，以下是我在我的系统上键入 cat /proc/cpuinfo 时得到的结果：

```
processor		: 0
vendor_id		: GenuineIntel
cpu family		: 15
model			: 2
model name		: Mobile Intel(R) Celeron(R) CPU 1.50GHz
stepping		: 7
cpu MHz			: 1495.610
cache size		: 256 KB
fdiv_bug		: no
hlt_bug			: no
f00f_bug		: no
coma_bug		: no
fpu			: yes
fpu_exception	: yes
cpuid level		: 2
wp			: yes
flags			: fpu vme de pse tsc msr pae mce cx8 sep mtrr
			pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2
			ss ht tm
bogomips		: 2981.88
```

此输出来自 1.5 GHZ Celeron 系统。列表显示了处理器的许多有趣特性。请注意以 fdiv_bug 开头的行。还记得臭名昭著的 Pentium 浮点除法错误吗？该错误位于名为 fdiv（浮点除法）的指令中。因此，fdiv_bug 行指示此特定 Pentium 是否存在该错误（幸运的是，我的 PC 的处理器没有）。



`/proc/cpuinfo` 文件中的最后一行显示了在 Linux 内核启动时计算的处理器 BogoMips。BogoMips 是 Linux 内部用于时间延迟循环的东西。

表 1-6 总结了 `/proc` 文件系统中提供有关你的 Red Hat Linux 系统信息的某些文件。你可以在系统上查看这些文件中的一些文件以查看其内容，但请注意，表 1-6 中显示的并非所有文件都存在于你的系统上。`/proc` 文件系统的具体内容取决于内核配置和已加载的驱动模块（这又取决于你的 PC 的硬件配置）。

![](img/a7eec43a54473e95dc5ea333fec1bd7_447_0.png)

你可以像操作 Red Hat Linux 中的任何其他目录和文件一样浏览 `/proc` 文件系统。使用 `more` 或 `cat` 命令查看文件的内容。

表 1-6 /proc 中的一些文件和目录

| 文件名 | 内容 |
|---|---|
| `/proc/apm` | 高级电源管理 (APM) 的信息 |
| `/proc/bus` | 包含每种总线类型（如 PCI）特定信息的目录 |
| `/proc/cmdline` | 用于启动 Linux 内核的命令行（例如，ro root=LABEL=/） |
| `/proc/cpuinfo` | 关于 CPU（微处理器）的信息 |
| `/proc/devices` | 系统中可用的块设备和字符设备 |
| `/proc/dma` | 关于正在使用的 DMA（直接内存访问）通道的信息 |
| `/proc/driver/rtc` | 关于 PC 实时时钟 (RTC) 的信息 |
| `/proc/filesystems` | 支持的文件系统列表 |
| `/proc/ide` | 包含 IDE 设备信息的目录 |
| `/proc/interrupts` | 关于中断请求 (IRQ) 编号及其使用情况的信息 |
| `/proc/ioports` | 关于输入/输出 (I/O) 端口地址及其使用情况的信息 |
| `/proc/kcore` | 物理内存映像 |
| `/proc/kmsg` | 内核消息 |
| `/proc/ksyms` | 内核符号表 |
| `/proc/loadavg` | 负载平均值（过去 1、5 和 15 分钟内等待运行的进程的平均数量） |
| `/proc/locks` | 当前内核锁（用于确保多个进程不会同时写入文件） |
| `/proc/meminfo` | 关于物理内存和交换空间使用情况的信息 |
| `/proc/misc` | 杂项信息 |
| `/proc/modules` | 已加载驱动模块列表 |
| `/proc/mounts` | 已挂载文件系统列表 |
| `/proc/net` | 包含网络信息的目录，其中包含许多子目录 |
| `/proc/partitions` | Linux 内核已知的分区列表 |
| `/proc/pci` | 系统中发现的 PCI 设备信息 |
| `/proc/scsi` | 包含系统中发现的 SCSI 设备信息的目录（仅在有 SCSI 设备时存在） |
| `/proc/stat` | 关于系统的总体统计信息 |
| `/proc/swaps` | 关于交换空间及其使用量的信息 |
| `/proc/sys` | 包含系统信息的目录；你可以通过向此目录中的文件写入来更改内核参数（使用此方法调整系统性能需要专业知识才能正确操作） |
| `/proc/uptime` | 关于系统运行时间的的信息 |
| `/proc/version` | 内核版本号 |

## 在 Red Hat Linux 中调度作业

作为系统管理员，你可能需要在定期间隔自动运行一些程序或在未来指定时间执行一个或多个命令。你的 Red Hat Linux 系统包括设施，可在你想要的任何未来日期或时间调度作业运行。你还可以设置系统定期或仅一次执行任务。以下是一些可以通过在 Linux 系统上调度作业来执行的典型任务：

- 深夜备份文件。
- 在系统不繁忙的清晨下载大文件。
- 向自己发送消息作为会议提醒。
- 定期分析系统日志并查找任何异常活动。

你可以通过使用 at 命令或 Red Hat Linux 的 crontab 功能来设置这些作业。在接下来的几节中，我将介绍 Red Hat Linux 的这些作业调度功能。

### 调度一次性作业

如果你想在稍后时间运行一个或多个命令，可以使用 at 命令。atd 守护进程——一个设计用于处理使用 at 提交的作业的程序——在指定时间运行你的命令并将输出通过邮件发送给你。

![](img/a7eec43a54473e95dc5ea333fec1bd7_449_0.png)

在尝试 at 命令之前，你需要知道以下配置文件控制哪些用户可以使用 at 命令调度任务：

- `/etc/at.allow` 包含可以使用 at 命令提交作业的用户名称。
- `/etc/at.deny` 包含不允许使用 at 命令提交作业的用户名称。

如果这些文件不存在，或者 /etc/at.deny 文件为空，则任何用户都可以使用 at 命令提交作业。Red Hat Linux 的默认设置是空的 /etc/at.deny 文件；在此默认设置下，任何人都可以...使用 at 命令。如果你不希望某些用户使用 at，只需在 /etc/at.deny 文件中列出他们的用户名即可。

要使用 at 在稍后时间调度一次性作业，请按照以下步骤操作：

**1. 使用你想要执行命令的日期或时间运行 at 命令。**

当你按 Enter 时，at> 提示符会出现，如下所示：

```
at 21:30
at>
```

这是指示你想要执行一个或多个命令的时间的最简单方法——只需以 24 小时格式指定时间。在这种情况下，你希望在今晚 9:30 p.m.（或如果现在已过 9:30 p.m. 则为明天）执行命令。你也可以以许多不同的方式指定执行时间（请参阅表 1-7 中的示例）。

**2. 在 at> 提示符下，像在 shell 提示符下输入一样输入你想要执行的命令；每输入一条命令后按 Enter 并继续下一个命令。当你完成输入要执行的命令后，按 Ctrl+D 表示结束。**

表 1-7 使用 at 命令执行时间的格式

| 命令 | 作业将运行的时间 |
|---|---|
| at now | 立即 |
| at now + 15 minutes | 当前时间后 15 分钟 |
| at now + 4 hours | 当前时间后 4 小时 |
| at now + 7 days | 当前时间后 7 天 |
| at noon | 今天中午（如果已过中午则为明天） |
| at now next hour | 恰好 60 分钟后 |
| at now next day | 明天同一时间 |
| at 17:00 tomorrow | 明天 5:00 p.m. |
| at 4:45pm | 今天 4:45 p.m.（如果已过 4:45 p.m. 则为明天） |
| at 3:00 Aug 16, 2003 | 2003 年 8 月 16 日 3:00 a.m. |

在你输入一个或多个作业后，你可以使用 atq 命令查看当前已调度的作业列表：

```
atq
```

输出看起来类似于以下内容：

```
4        2003-08-16 03:00 a root
5        2003-10-26 21:57 a root
6        2003-10-26 16:45 a root
```

每行第一个字段显示作业编号——与你提交作业时 at 命令显示的编号相同。下一个字段显示执行年份、月份、日期和时间。最后一个字段显示在名为 a 的队列中待处理的作业。

如果你想取消作业，使用 atrm 命令从队列中删除该作业。使用 atrm 命令删除作业时，请按如下方式引用作业编号：

```
atrm 4
```

这将删除安排在 2003 年 8 月 16 日 3:00 a.m. 执行的作业 4。

当作业执行时，输出会通过邮件发送给你。在终端窗口中输入 mail 以阅读邮件并查看作业的输出。

![](img/a7eec43a54473e95dc5ea333fec1bd7_450_0.png)

### 调度重复作业

虽然 at 适用于在特定时间运行命令，但它不适用于在重复间隔自动运行程序。你必须使用 crontab 来调度此类重复作业。例如，如果你想每天午夜将文件备份到磁带，就必须这样做。

你通过将作业信息放在特定格式的文件中并使用 crontab 命令提交该文件来调度重复作业。cron 守护进程——crond——每分钟检查一次作业信息并在指定时间执行重复作业。由于 cron 守护进程处理重复作业，因此这些作业也称为 cron 作业。

cron 作业的任何输出都会通过邮件发送给提交作业的用户。（在提交的作业信息文件中，你可以指定邮件输出的不同接收者。）

两个配置文件控制谁可以使用 crontab 调度 cron 作业：

- **/etc/cron.allow** 包含可以使用 crontab 命令提交作业的用户名称。
- **/etc/cron.deny** 包含不允许使用 crontab 命令提交作业的用户名称。

如果 /etc/cron.allow 文件存在，则只有列在此文件中的用户可以调度 cron 作业。如果只有 /etc/cron.deny 文件存在，则列在此文件中的用户不能调度 cron 作业。如果两个文件都不存在，则默认的 Red Hat Linux 设置允许任何用户提交 cron 作业。

要提交 cron 作业，请按照以下步骤操作：

- 1. **准备一个 shell 脚本（或任何编程语言中的可执行程序），该脚本可以执行你想要执行的重复任务。**
- 如果你想定期执行现有程序，可以跳过此步骤。
- 2. **准备一个包含你想要 shell 脚本或程序（来自步骤 1）执行的时间信息的文本文件，然后使用 crontab 提交该文件。**

你可以使用单个文件提交多个重复作业。包含作业时间信息的每一行都有标准格式，包含六个字段——前五个指定作业运行的时间，第六个及后续字段构成实际运行的命令。例如，这里有一行代码，每天午夜过后五分钟执行用户主目录中的 myjob shell 脚本：

```
5 0 * * * $HOME/myjob
```

表 1-8 显示了前五个字段的含义。请注意，星号 (*) 表示该字段的所有可能值。此外，任何

前五个字段可以是一个数字、一个用逗号分隔的数字列表、用连字符分隔的一对数字（表示数字范围），或一个星号。

3. 假设文本文件 jobinfo（在当前目录中）包含作业信息。使用以下命令将此信息提交给 crontab：

```
crontab jobinfo
```

就这样！你应该已经设置好 cron 作业。从现在开始，cron 作业应按定期间隔运行（按作业信息文件中指定的方式），并且你应收到包含作业输出的邮件信息。

要验证作业是否确实已安排，输入以下命令：

```
crontab -l
```

crontab -l 命令的输出显示当前以你的名义安装的 cron 作业。要删除你的 cron 作业，输入 crontab -r。

表 1-8 crontab 文件中执行时间的格式

| 字段编号 | 字段含义 | 可接受的值范围* |
|---|---|---|
| 1 | 分钟 | 0-59 |
| 2 | 一天的小时 | 0-23 |
| 3 | 月份中的日期 | 0-31 |
| 4 | 月份 | 1-12（1 表示一月，2 表示二月，依此类推）或使用前三个字母的月份名称（Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec） |
| 5 | 星期几 | 0-6（0 表示星期日，1 表示星期一，依此类推）或星期几的三个字母缩写（Sun, Mon, Tue, Wed, Thu, Fri, Sat） |

* 字段中的星号表示该字段的所有可能值。例如，如果第三个字段中有一个星号，则作业每天执行。

如果以 root 登录，你还可以为任何用户设置、检查和删除 cron 作业。要为用户设置 cron 作业，使用此命令：

```
crontab -u username filename
```

这里，username 是你要为其安装 cron 作业的用户，filename 是包含有关作业信息的文件。

使用以下形式的 crontab 命令查看用户的 cron 作业：

```
crontab -u username -l
```

要删除用户的 cron 作业，使用以下命令：

```
crontab -u username -r
```

请注意，cron 守护进程还执行系统范围的 cron 作业文件 /etc/crontab 中列出的 cron 作业。以下是 Red Hat Linux 中默认的 /etc/crontab 文件（输入 cat /etc/crontab 查看文件）：

```
SHELL=/bin/bash
PATH=/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/

# run-parts
01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
22 4 0 * * root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly
```

前四行为此文件中列出的作业设置了多个环境变量。MAILTO 环境变量指定接收此文件中 cron 作业输出邮件的用户。

以 # 开头的行是注释行。run-parts 注释后的四行在不同时间执行 run-parts shell 脚本（位于 /usr/bin 目录中），并将特定目录的名称作为参数。run-parts 的每个参数——/etc/cron.hourly、/etc/cron.daily、/etc/cron.weekly 和 /etc/cron.monthly——都是目录。本质上，run-parts 执行位于你作为参数提供的目录中的所有脚本。

表 1-9 列出了这些脚本所在的目录以及执行时间。你必须查看这些目录中的脚本才能知道在这些定期间隔时执行什么。

表 1-9 cron 作业的脚本目录

| 目录名称 | 内容 |
|---|---|
| /etc/cron.hourly | 每小时执行的脚本 |
| /etc/cron.daily | 每天在凌晨 4:02 执行的脚本 |
| /etc/cron.weekly | 每周星期日凌晨 4:22 执行的脚本 |
| /etc/cron.monthly | 每月第一天凌晨 4:42 执行的脚本 |

### 第 2 章：管理用户

### 本章内容

- ✓ 添加用户账户
- ✓ 了解密码文件
- ✓ 管理组
- ✓ 探索用户环境
- ✓ 更改文件和目录的用户和组所有权

Red Hat Linux 是一个多用户系统，因此它有许多用户账户。即使你是系统上唯一的 用户，许多服务器也需要唯一的用户名和组名。例如，Apache Web 服务器。它在用户名 `apache` 下运行。有一整套系统用户不是供人使用，而是仅用于运行特定程序。

此外，用户可以属于一个或多个组。通常，每个用户名都有一个对应的私有组名。默认情况下，每个用户都属于该对应的私有组。然而，你可以定义其他组，以便根据组成员身份提供对特定文件和目录的访问。

文件和组的所有权是一种确保只有正确的人（或正确的进程）可以访问正确的文件和目录的方法。管理用户和组账户是典型的系统管理任务。鉴于 Red Hat Linux 附带的工具，完成这项工作并不难。我会向你展示如何操作。

## 添加用户账户

在安装 Red Hat Linux 后首次启动系统时，你有机会添加用户账户。`root` 账户是在安装期间必须设置的唯一账户。如果你未在初始启动期间添加其他用户账户，可以稍后使用 Red Hat User Manager 或 `useradd` 命令在系统上添加新用户。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_455_0.png)

除了 root 之外创建其他用户账户是个好主意。即使你是系统的唯一用户，以权限较低的用户登录也是良好的做法，因为这样你就不会无意中损坏任何重要的系统文件。如果需要，你可以输入 su 命令以 root 身份登录，然后执行任何系统管理任务。

## 使用 Red Hat User Manager 添加用户账户

你可以使用 Red Hat User Manager 添加用户账户。要启动 Red Hat User Manager，在图形登录屏幕以 root 登录，然后从 GNOME 面板中选择 主菜单->系统设置->用户和组。如果你未以 root 登录，Red Hat User Manager 会提示你输入 root 密码。如果被提示，输入密码并单击确定。然后 Red Hat User Manager 窗口出现。

该窗口显示两个选项卡：Users 和 Groups（如图 2-1 所示）。Users 选项卡显示来自 /etc/passwd 文件的当前用户列表。Groups 选项卡列出来自 /etc/group 的组名。最初，Red Hat User Manager 会过滤掉任何系统用户和组。然而，你可以通过选择 首选项->过滤系统用户和组 来关闭过滤器，使该菜单项旁边的复选标记消失。图 2-1 显示了 Red Hat User Manager 窗口，其中列出了所有用户账户，包括系统账户。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_455_1.png)

图 2-1：你可以在 Red Hat User Manager 窗口中管理用户账户和组。

你可以在 Red Hat User Manager 窗口中添加新用户和组或编辑现有用户和组。

要编辑现有用户的信息，请按照以下步骤操作：

1. 在 Users 选项卡的列表中单击用户名，然后单击工具栏上的属性按钮。

该用户的信息会出现在用户属性对话框中（图 2-2）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_456_0.png)

图 2-2：
在此对话框中编辑现有用户的信息。

2. 编辑信息并单击确定以进行更改。

要添加新用户，请按照以下步骤操作：

1. 单击工具栏上的添加用户按钮（参见图 2-1）。

此操作打开创建新用户对话框（如图 2-3 所示）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_456_1.png)

图 2-3：
通过在此对话框中填写信息来创建新用户账户。

2. 填写所需信息。

特别是，你必须输入用户名和密码。填写所有字段后，单击确定按钮。新用户现在应出现在 Red Hat User Manager 窗口中 Users 选项卡的列表中。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_457_0.png)

注意创建用户的私有组复选框。它默认处于选中状态，这意味着每个新用户都在一个单独的私有用户组中。然而，有时你希望用户属于特定组，以便用户可以访问该组拥有的文件。将用户添加到另一个组很容易。例如，假设我想将用户名 naba 添加到名为 wheel 的组中。我只需在终端窗口中输入以下命令即可完成此操作：

```
usermod -G wheel naba
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_457_1.png)

要删除用户账户，单击 Users 选项卡上显示所有用户账户的列表中的用户名（参见图 2-1）。然后单击工具栏上的删除按钮。

## 使用命令管理用户账户

如果你正在从文本控制台工作，可以使用 useradd 命令创建新用户账户。按照以下步骤为新用户添加账户：

- 1. 以 root 登录。
  
      如果你尚未以 root 登录，输入 su - 成为 root。
  
- 2. 输入以下带有 -c 选项的 useradd 命令以创建账户：
  
      `/usr/sbin/useradd -c "Ashley Barkakati" ashley`
  
- 3. 使用 passwd 命令设置 Ashley 的密码，如下所示：
  
      `passwd ashley`
  
      系统会提示你两次输入密码。如果你输入一个容易被猜到的密码，passwd 程序会拒绝它。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_457_2.png)

useradd 命令会查阅以下配置文件以获取有关新用户账户各种参数的默认信息：

- - /etc/default/useradd — 指定默认 shell (/bin/bash) 和默认主目录位置 (/home)。
- - /etc/login.defs — 提供自动组和用户 ID 的系统范围默认值，以及密码过期参数。



使用 cat 或 more 命令检查这些文件以查看其内容。

你可以使用 userdel 命令删除用户账户。只需在命令提示符下输入 /usr/sbin/userdel username 即可删除用户账户。要同时删除该用户的主目录，请输入 /usr/sbin/userdel -r username。

要修改用户账户中的任何信息，请使用 usermod 命令。例如，如果我想让我的用户名 naba 的主组为 root，我会输入以下内容：

```
usermod -g root naba
```

要了解有关 useradd、userdel 和 usermod 命令的更多信息，请在终端窗口中输入 man useradd、man userdel 或 man usermod。

## 理解 /etc/passwd 文件

/etc/passwd 文件是所有用户账户的列表。它是一个文本文件，任何用户都可以读取——无需特殊权限。/etc/passwd 中的每一行都有七个字段，由冒号 (:) 分隔。

这是 /etc/passwd 文件中的一个典型条目：

```
naba:x:500:10:Naba Barkakati:/home/naba:/bin/bash
```

图 2-4 使用此典型条目来解释七个字段的含义。

图 2-4：此典型的 /etc/passwd 条目说明了各个字段的含义。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_458_0.png)

![](img/a7eec43a54473e95dc5ea333fecf1bd7_458_1.png)

![](img/a7eec43a54473e95dc5ea333fecf1bd7_458_2.png)

正如示例所示，/etc/passwd 中每一行的格式如下：

```
username:password:UID:GID:GECOS:homedir:shell
```

表 2-1 解释了 /etc/passwd 条目中七个字段的含义。

**表 2-1 /etc/passwd 文件中字段的含义**

| 此字段 | 包含 |
|---|---|
| 用户名 | 一个字母数字用户名，通常长度为八个字符且唯一（Red Hat Linux 允许用户名长于八个字符，但某些其他操作系统不允许） |
| 密码 | 当存在时，为 13 个字符的加密密码（空字段表示访问账户无需密码；x 表示密码存储在 /etc/shadow 文件中，这更安全） |
| UID | 一个唯一的数字，用作用户标识符（root 的 UID 为 0，通常 UID 1 到 100 之间保留给非人类用户，如服务器；最好将 UID 保持在 32,767 以下） |
| GID | 用户所属组的默认组 ID（GID 0 用于 root 组；其他组在 /etc/group 中定义，用户可以并且通常同时属于多个组） |
| GECOS | 关于用户的可选个人信息（finger 命令使用此字段，GECOS 是 General Electric Comprehensive Operating System 的缩写，这是一个早已遗忘的操作系统，其名称被 /etc/passwd 中此字段的名称所纪念） |
| 主目录 | 用户主目录的名称 |
| shell | 登录时为该用户执行的命令解释器（shell），例如 Bash (/bin/bash) |

## 管理组

组是用户所属的对象。组有一个名称和一个标识号（ID）。在定义组之后，用户可以属于一个或多个这些组。

你可以在 `/etc/group` 中找到所有现有组的列表。例如，这里是定义名为 `wheel` 的组的行：

```
wheel:x:10:root,naba
```

正如本示例所示，`/etc/group` 中的每一行具有以下格式，由冒号分隔的四个字段：

```
groupname:password:GID:membership
```

表 2-2 解释了组定义中四个字段的含义。

**表 2-2 /etc/group 文件中字段的含义**

| 字段名称 | 含义 |
|---|---|
| `groupname` | 组的名称（例如，`wheel`） |
| `password` | 组密码（x 表示密码存储在 `/etc/shadow` 文件中） |
| `GID` | 数值组 ID（例如，`10`） |
| `membership` | 属于此组的用户的以逗号分隔的用户名列表（例如，`root,naba`） |

如果你想创建一个新组，可以简单地在 Red Hat 用户管理器中单击“添加组”按钮（参见图 2-1）。更快捷的方法是使用 `groupadd` 命令。例如，要添加一个名为 `class` 的新组并自动选择组 ID，只需在终端窗口中输入以下命令（你必须以 `root` 身份登录）：

```
groupadd class
```

然后你可以使用 `usermod` 命令将用户添加到该组。例如，要将用户 `naba` 和 `ashley` 添加到名为 `class` 的组中，输入以下命令：

```
usermod -G class naba
usermod -G class ashley
```

就是这样。现在检查 `/etc/group`，你会发现它包含以下 `class` 的定义：

```
class:x:502:naba,ashley
```

就这么简单！

如果你想删除一个组，请使用 groupdel 命令。例如，要删除名为 class 的组，输入

```
groupdel class
```

## 探索用户环境

当你以用户身份登录时，你会获得一组环境变量，它们控制你在 Red Hat Linux 系统中看到和执行的大多数方面。如果你想查看当前环境，请在终端窗口中输入以下命令：

```
env
```

（顺便说一下，printenv 命令也会显示环境，但 env 更短。）

env 命令应打印出一长串行。这一整组行就是当前环境，每一行定义一个环境变量。例如，以下是 env 命令显示的一个典型行：

```
HOSTNAME=localhost.localdomain
```

这一行定义了环境变量 HOSTNAME，其定义为 localhost.localdomain。

环境变量只不过是与字符串关联的名称。例如，名为 PATH 的环境变量通常定义如下：

```
PATH=/usr/local/bin:/bin:/usr/bin:/usr/X11R6/bin
```

等号右侧的字符串是 PATH 环境变量的值。按惯例，PATH 环境变量是一系列目录名称，每个名称由冒号 (:) 与前一个名称分隔。每个环境变量都有特定的用途。例如，当 shell 需要搜索文件时，它只需搜索 PATH 环境变量中列出的目录。shell 按其出现的顺序搜索 PATH 中的目录。因此，如果两个程序同名，shell 会执行它首先找到的那个。类似于 shell 对 PATH 环境变量的使用，vi 等编辑器使用 TERM 环境变量的值来确定如何显示你正在用 vi 编辑的文件。要查看 TERM 的当前设置，在 shell 提示符下输入以下命令：

```
echo $TERM
```

如果你在终端窗口中输入此命令，输出如下：

```
xterm
```

要在 Bash 中定义环境变量，请使用以下语法：

```
export NAME=Value
```

这里，NAME 表示环境变量的名称，Value 是表示其值的字符串。因此，你可以使用以下命令将 TERM 设置为值 xterm：

```
export TERM=xterm
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_462_0.png)

在你定义环境变量后，你可以通过使用语法 NAME=new-value 指定新值来更改其值。例如，要将 TERM 的定义更改为 vt100，在 shell 提示符下输入 TERM=vt100。

对于 PATH 等环境变量，你通常希望将新目录名追加到现有定义中，而不是从头定义 PATH。以下示例展示了如何完成此任务：

```
export PATH="$PATH:/usr/games"
```

此命令将字符串 :/usr/games 追加到 PATH 环境变量的当前定义中。净效果是将 /usr/games 添加到 PATH 目录列表中。

请注意，你也可以按如下方式编写此 export 命令：

export PATH=${PATH}:/usr/games

在你输入该命令后，你可以访问 /usr/games 目录中的程序，例如 fortune，它会打印简洁且经常机智（有时令人困惑）的句子。如果你好奇，请继续输入以下命令：

fortune

fortune 打印的内容是随机的，但可能很有趣。结果应为简洁、机智和/或令人困惑的句子。



PATH 和 TERM 只是众多常见环境变量中的两个。表 2-3 列出了典型 Red Hat Linux 用户的一些环境变量。

表 2-3 Red Hat Linux 中的典型环境变量

| 环境变量 | 内容 |
|---|---|
| DISPLAY | X Window System 显示输出的显示器名称（通常设置为 :0.0） |
| HOME | 您主目录 |
| HOSTNAME | 系统的主机名 |
| LOGNAME | 您的登录名 |
| MAIL | 邮件目录的位置 |
| PATH | shell 查找程序的目录列表 |
| SHELL | 您的 shell（对于 Bash，SHELL=/bin/bash） |
| TERM | 终端类型 |

## 修改文件的所有者和组所有权

在 Red Hat Linux 中，每个文件或目录都有两个所有者——用户和组。用户和组所有权可用于控制谁可以访问文件或目录。

若要查看文件或目录的所有者，请使用 ls -l 命令查看目录的详细列表。例如，以下是典型文件的信息：

```
-rw-rw-r-- 1 naba naba 40909 07-14 20:37 composer.txt
```

在此示例中，第一组字符显示文件权限设置——谁可以读取、写入或执行该文件。第三和第四个字段（在此示例中为 naba naba）表示文件的所有者和组所有者。每个用户都有一个私有组，其名称与用户名相同。因此，大多数文件的用户和组所有权似乎显示了两次用户名。

作为系统管理员，您可能决定将文件组所有权更改为公共组。例如，假设您想将 composer.txt 文件的组所有权更改为 class 组。为此，以 root 身份登录并输入以下命令：

```
chgrp class composer.txt
```

此 chgrp 命令将 composer.txt 的组所有权更改为 class。尝试此操作后，我再次输入 ls -l 以验证所有权，结果如下：

```
-rw-rw-r-- 1 naba class 40909 07-14 20:37 composer.txt
```

您可以使用 chown 命令更改用户所有者。该命令的格式如下：

```
chown username filename
```

例如，要将名为 sample.jpg 的文件的所有者更改为 naba，请输入：

```
chown naba sample.jpg
```

实际上，chown 可以同时更改用户和组所有者。例如，要将用户所有者更改为 naba 并将组所有者更改为 class，请输入：

```
chown naba.class composer.txt
```

换句话说，您只需在用户名后加上一个点再加上组名，并将其用作所有者名称即可。

### 第 3 章：管理文件系统

### 本章内容

- ✔ 学习 Red Hat Linux 文件系统
- ✔ 使用 NFS 共享文件
- ✔ 备份和恢复文件
- ✔ 访问 MS-DOS 文件

文件系统是指文件和目录的组织方式。作为系统管理员，您必须执行某些操作来管理文件系统。例如，您必须学习如何挂载——通过将其附加到整体 Red Hat Linux 文件系统，将存储介质上的文件系统添加进来。您还必须备份重要数据并学习如何从备份中恢复文件。其他文件系统操作包括使用网络文件系统 (NFS) 共享文件和访问 MS-DOS 文件。在本章中，我将向您展示如何执行所有文件系统管理任务。

## 学习 Red Hat Linux 文件系统

您 PC 中的文件和目录以与纸质归档系统类似的有序方式存储信息。当您在纸上存储信息时，通常将几页纸放入文件夹中，然后将文件夹保存在文件柜中。如果您有许多文件夹，您可能有某种归档系统。例如，您可能会标记每个文件夹的标签，然后按字母顺序将它们排列在文件柜中。您可能有几个文件柜，每个文件柜都有很多抽屉，而抽屉中又装满了文件夹和纸张。

Red Hat Linux 等操作系统以与您的纸质归档系统类似的方式组织计算机中的信息。Red Hat Linux 使用文件系统来组织计算机中的所有信息。当然，与文件柜不同，存储介质不是金属柜和纸张。相反，Red Hat Linux 将信息存储在硬盘驱动器、软盘驱动器和 CD-ROM 驱动器等设备上。

为了在计算机文件系统和纸质归档系统之间建立类比，请将磁盘驱动器视为文件柜。文件柜中的抽屉对应于文件系统中的目录。每个抽屉中的文件夹也是目录——因为计算机文件系统中的目录可以包含其他目录。您可以将文件视为文件夹内的页面——实际信息就存储在那里。图 3-1 说明了文件柜与 Red Hat Linux 文件系统之间的类比。

图 3-1：
有点牵强，但您可以将 Red Hat Linux 文件系统视为类似于文件柜。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_467_0.png)

Red Hat Linux 文件系统具有层次结构——目录可以包含其他目录，而这些目录又包含单个文件。

Red Hat Linux 系统中的所有内容都在文件系统中以文件和目录的形式组织。要访问和使用系统上的文档和程序，您必须熟悉文件系统。

### 了解文件系统层次结构

Red Hat Linux 文件系统像树一样组织，有一个根目录，所有其他目录都从中分支出来。当您编写完整路径名时，根目录由单个斜杠（/）表示。然后是文件和目录的层次结构。文件系统的部分可以位于不同的物理驱动器或不同的硬盘分区中。

Red Hat Linux 使用标准目录层次结构。图 3-2 显示了 Red Hat Linux 文件系统的标准部分。当然，您可以在此结构中的任何位置创建新目录。

图 3-2：
Red Hat Linux 文件系统使用此标准目录层次结构。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_468_0.png)

通过连接标识文件或目录所在位置的目录名称并使用正斜杠（/）作为分隔符来编写任何文件或目录的名称。例如，在图 3-2 中，顶层的 usr 目录写为 /usr，因为根目录（/）包含 usr。另一方面，X11R6 目录位于 usr 目录内，而 usr 目录位于根目录（/）内。因此，X11R6 目录的唯一标识名称为 /usr/X11R6。这种完整名称称为路径名，因为该名称标识了从根目录到达文件的路径。因此 /usr/X11R6 是一个路径名。

Red Hat Linux 文件系统中的每个标准目录都有特定用途。表 3-1 总结了这些目录。

表 3-1 Red Hat Linux 文件系统中的标准目录

| 目录 | 用于存储 |
|---|---|
| /bin | 用户命令的可执行文件（供所有用户使用） |
| /boot | 启动加载器加载 Linux 内核所需的文件 |
| /dev | 设备文件 |
| /etc | 主机特定的系统配置文件 |
| /home | 用户主目录 |
| /lib | 共享库和内核模块 |
| /mnt | 临时挂载文件系统的挂载点 |
| /opt | 附加应用程序软件包 |
| /root | root 用户的主目录 |
| /sbin | 系统管理实用程序 |
| /tmp | 临时文件 |
| The /usr Hierarchy |  |
| /usr/X11R6 | X Window 系统，版本 11 发布版 6 |
| /usr/bin | 大多数用户命令 |
| /usr/include | 用于开发 Linux 应用程序的标准包含文件目录 |
| /usr/lib | 软件包和编程使用的库 |
| /usr/libexec | 应用程序库 |
| /usr/local | 任何本地软件 |
| /usr/sbin | 非必要的系统管理员实用程序 |
| /usr/share | 与系统架构无关的共享数据（无论系统是 Intel PC 还是 Sun SPARC 工作站） |
| /usr/src | 源代码 |
| The /var Hierarchy |  |
| /var/cache | 应用程序的缓存数据 |
| /var/lib | 与应用程序当前状态相关的信息 |
| /var/lock | 确保资源仅由一个应用程序使用的锁文件 |
| /var/log | 组织在子目录中的日志文件 |
| /var/mail | 用户邮箱文件 |
| /var/opt | 存储在 /opt 目录中的软件包的可变数据 |
| /var/run | 自系统启动以来描述系统的信息 |
| /var/spool | 等待某种处理的数据 |
| /var/tmp | 系统重启之间保留的临时文件 |
| /var/yp | 网络信息服务 (NIS) 数据库文件 |

## 在文件系统上挂载设备

您在 Red Hat Linux 中使用的存储设备包含 Linux 文件系统。每个设备都有自己的本地文件系统，由目录层次结构组成。在访问设备上的文件之前，您必须将设备的目录层次结构附加到代表整体 Red Hat Linux 文件系统的树中。

挂载是您执行的操作，使物理存储设备（硬盘分区或 CD-ROM）上的文件系统作为 Linux 文件系统的一部分出现。图 3-3 说明了挂载的概念。

图 3-3 显示每个设备名称以 /dev 开头。例如，/dev/cdrom 是 CD-ROM 驱动器，/dev/fd0 是软盘驱动器。这些物理设备在 Red Hat Linux 文件系统上的特定挂载点上挂载。例如，CD-ROM 驱动器 /dev/cdrom 在文件系统上挂载在 /mnt/cdrom。按此方式挂载 CD-ROM 后，CD-ROM 上的 Red Hat 目录在 Red Hat Linux 文件系统中显示为 /mnt/cdrom/RedHat。



图 3-3:
在访问设备之前，必须先将其挂载到 Red Hat Linux 文件系统上。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_470_0.png)

你可以使用 mount 命令手动将设备挂载到 Red Hat Linux 文件系统的指定目录。该目录即为挂载点。例如，要将 CD-ROM 驱动器挂载到 /mnt/cdrom 目录，需在以 root 身份登录后输入以下命令：

```
mount /dev/cdrom /mnt/cdrom
```

如果 CD-ROM 设备已挂载或驱动器中没有 CD-ROM，mount 命令会报告错误。否则，挂载操作成功，你可以通过 /mnt/cdrom 目录访问 CD-ROM 的内容。

你可以使用任何目录作为挂载点。然而，如果将设备挂载到非空目录上，则在使用 umount 命令卸载设备之前无法访问该目录中的文件。因此，你始终应使用空目录作为挂载点。

Red Hat Linux 自带 /mnt/cdrom 目录用于挂载 CD-ROM，以及 /mnt/floppy 用于挂载软盘驱动器。

当不再需要设备时，使用 umount 命令卸载它。例如，要卸载 CD-ROM 设备，输入

```
umount /dev/cdrom
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_470_1.png)

只要没有人使用 CD-ROM，umount 命令就会成功。如果尝试卸载 CD-ROM 时出现错误，请检查当前工作目录是否在 CD-ROM 上。如果你当前正在 CD-ROM 的某个目录中工作，这也算作使用 CD-ROM。

## 检查 /etc/fstab 文件

mount 命令的一般格式如下：

```
mount device-name mount-point
```

然而，你可以通过输入以下任一命令挂载 CD-ROM：

```
mount /dev/cdrom
mount /mnt/cdrom
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_471_0.png)

由于 /etc/fstab 文件中的内容，你只需指定 CD-ROM 设备名或挂载点名即可挂载。/etc/fstab 文件中有一行对应 /mnt/cdrom 挂载点。该条目指定了 CD-ROM 设备名和文件系统类型。这就是为什么可以用更短的 mount 命令挂载 CD-ROM。

/etc/fstab 文件是一个配置文件——一个包含 mount 和 umount 命令使用的信息的文本文件。/etc/fstab 文件中的每一行都提供了 Red Hat Linux 文件系统中设备及其挂载点的信息。本质上，/etc/fstab 文件将文件系统中的各个挂载点与特定设备关联起来，使得 mount 命令只需在命令行中提供挂载点或设备即可工作。

以下是一个典型的 Red Hat Linux 系统的 /etc/fstab 文件：

```
LABEL=/              /           ext3    defaults        1 1
LABEL=/boot          /boot       ext3    defaults        1 2
none                 /dev/pts    devpts  gid=5,mode=620  0 0
none                 /proc       proc    defaults        0 0
none                 /dev/shm    tmpfs   defaults        0 0
/dev/hda6            swap        swap    defaults        0 0
/dev/cdrom           /mnt/cdrom  udf,iso9660 noauto,owner,kudzu,ro 0 0
/dev/fd0             /mnt/floppy auto    noauto,owner,kudzu 0 0
```

每行第一个字段显示设备名，例如硬盘分区（或通过 LABEL 关键字标识分区）。第二个字段是挂载点，第三个字段表示设备上的文件系统类型。你现在可以忽略最后三个字段。

该 /etc/fstab 文件显示 /dev/hda6 设备（第一块 IDE 硬盘上的第二个逻辑分区）用作虚拟内存的交换设备，因此挂载点和文件系统类型都设置为 swap。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_472_0.png)

Linux 操作系统使用 /etc/fstab 文件的内容自动挂载各种文件系统。在 Red Hat Linux 启动期间，init 进程执行一个运行 mount -a 命令的 shell 脚本。该命令读取 /etc/fstab 文件并挂载所有列出的文件系统（除带有 noauto 选项者外）。/etc/fstab 每行第三个字段指定该设备上的文件系统类型，第四个字段显示 mount 命令在将设备挂载到文件系统时使用的以逗号分隔的选项列表。通常在此字段中会找到 defaults 选项。defaults 选项意味着——其中包括——设备在启动时挂载；只有 root 用户可以挂载设备；并且设备以读写方式挂载。如果选项包含 noauto，则设备在系统启动时不会自动挂载。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_472_1.png)

/etc/fstab 条目第四字段中的 kudzu 选项表示这些行是由 kudzu 硬件检测实用程序添加到 fstab 文件中的——kudzu 运行 updatefstab 命令为其检测到的每个可移动驱动器在 /etc/fstab 文件中添加一个条目。通常你会发现 CD-ROM (/dev/cdrom) 和软盘驱动器 (/dev/fd0) 的条目在第四字段中具有 kudzu 选项。例如，在装有 IDE Zip 驱动器的 PC 上，/etc/fstab 文件中还有一条由 kudzu 设置的条目，将 /mnt/zip 挂载点与 Zip 驱动器设备 (/dev/hdd4) 关联，格式如下：

```
/dev/hdd4  /mnt/zip  auto  noauto,owner,kudzu  0  0
```

## 使用 NFS 共享文件

通过网络文件系统（NFS）共享文件很简单，涉及两个基本步骤：

- 在 NFS 服务器上，通过在 /etc/exports 文件中列出它们并运行 /usr/sbin/exportfs 命令来导出一个或多个目录。此外，你必须运行 NFS 服务器（你可以通过以 root 身份登录并输入 service nfs start 来实现）。
- 在每个客户端系统上，使用 mount 命令挂载服务器导出的目录。

使用 NFS 的唯一问题是每个客户端系统必须支持它。大多数 PC 都不自带 NFS——这意味着如果你想使用 NFS 共享文件，就必须单独购买 NFS 软件。然而，如果局域网上的所有系统都运行 Linux（或其他内置 NFS 支持的 UNIX 变体），那么使用 NFS 就有意义了。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_473_0.png)

请注意，NFS 存在安全漏洞。因此，不应在直接连接到互联网的系统上设置 NFS。

在接下来的章节中，我将通过两个局域网上的 Linux PC 的示例，带你完成 NFS 设置。

## 使用 NFS 导出文件系统

从导出——使客户端系统可用——目录内容的服务器系统开始。在服务器上，你必须运行 NFS 服务，并指定一个或多个要导出的文件系统，或使之对客户端系统可用。

要导出文件系统，你必须在 /etc/exports 文件中添加适当的条目。例如，假设你想导出 /home 目录，并希望名为 LNB P75 的主机能够以读写方式挂载此文件系统（你可以用主机的 IP 地址代替主机名）。你可以通过在 /etc/exports 文件中添加以下条目来实现：

/home LNB P75(rw)

在 /etc/exports 文件中添加条目后，通过在终端窗口中输入 /usr/sbin/exportfs -a 手动导出文件系统。该命令导出 /etc/exports 文件中定义的所有文件系统

```
/usr/sbin/exportfs -a
```

现在启动 NFS 服务器——以 root 身份登录并在终端窗口中输入以下命令：

```
service nfs start
```

要重启 NFS 服务，输入 service nfs restart。

当 NFS 服务运行时，NFS 服务器端已就绪。现在你可以尝试从客户端系统挂载导出的文件系统并访问它。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_473_1.png)

如果你对 /etc/exports 文件中列出的导出文件系统进行任何更改，请记住重启 NFS 服务。为此，在终端窗口中输入 service nfs restart。



## 挂载 NFS 文件系统

为了在客户端系统上访问导出的 NFS 文件系统，你必须将该文件系统挂载到一个挂载点上——从实际角度来看，它不过是一个本地目录。例如，假设你想在客户端系统上的本地目录 /mnt/lnbp200 访问从名为 lnbp200 的服务器导出的 /home 目录。要做到这一点，请按照以下步骤操作：

- 1. 以 root 身份登录，并使用以下命令创建目录：
  `mkdir /mnt/lnbp200`
- 2. 输入以下命令执行挂载操作：
  `mount lnbp200:/home/public /mnt/lnbp200`
- 3. 使用命令 `cd /mnt/lnbp200` 切换到 /mnt/lnbp200 目录
  现在你可以查看和访问此目录中的导出文件。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_474_0.png)

为了确认 NFS 文件系统确实已挂载，请在客户端系统上以 root 身份登录并在终端窗口中输入 mount。你应该会看到关于 NFS 文件系统的类似以下的行：

```
lnbp200:/home/public on /mnt/lnbp200 type nfs (rw,addr=192.168.1.200)
```

## 备份和恢复文件

备份和恢复文件是一项至关重要的系统管理任务。如果系统硬盘出现问题，你必须依靠备份来恢复重要文件。在这里我介绍一些备份策略，描述几种备份介质，并解释如何使用随 Red Hat Linux 提供的磁带归档程序（tar）来备份和恢复文件。此外，你还将了解如何在磁带上执行增量和自动备份。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_474_1.png)

如果你有 CD 刻录机，你也可以通过将文件刻录到 CD-R 上来备份文件。有关如何刻录数据 CD 的信息，请参阅第二册第 5 章。

## 选择备份策略和介质

你的 Red Hat Linux 系统的硬盘包含使系统运行所需的一切——以及其他文件（例如文档和数据库），这些文件使你的业务得以运行。你必须备份这些文件，以便在硬盘崩溃时能够快速恢复并使系统恢复正常。通常，你必须遵循严格的定期备份制度，因为你永远无法确定硬盘何时会故障或文件系统何时会损坏。为了实施这种制度，首先要决定要备份哪些文件、备份频率以及使用什么备份存储介质。这就是我所说的选择备份策略和备份介质的过程。

你的备份策略和备份介质选择取决于你对因硬盘故障导致业务中断风险的评估。根据你使用 Red Hat Linux 系统的方式，磁盘故障可能对你产生很大影响，也可能影响不大。

例如，如果你将 Red Hat Linux 系统用作学习工具（学习 Linux 或编程），你可能只需要一些用于配置 Linux 的系统文件的备份副本。在这种情况下，你的备份策略可以是每次更改任何系统配置时都将重要的系统配置文件保存到一个或多个软盘上。

另一方面，如果你将 Red Hat Linux 系统用作为许多用户提供共享文件存储的办公服务器，则因磁盘故障导致业务中断的风险要高得多。在这种情况下，你必须每周备份所有文件并每天备份任何新文件或更改的文件。你应该以自动方式执行这些备份（这就是你可以使用我在本书迷你书第 1 章中描述的作业调度功能的地方）。此外，你可能需要一种能够在单个磁带上存储大量（数 GB）数据的备份存储介质。换句话说，对于高风险情况，你的备份策略更为复杂，需要额外的设备（例如磁带驱动器）。

你的备份介质选择取决于你需要备份的数据量。对于少量数据（例如系统配置文件），你可以使用软盘作为备份介质。如果你的 PC 有 Zip 驱动器，你可以使用 Zip 磁盘作为备份介质；这些很适合备份单个用户目录。要备份整个服务器，请使用磁带驱动器，通常是连接到 SCSI 控制器的 4mm 或 8mm 磁带驱动器。此类磁带驱动器每盘可存储数 GB 数据，你可以用它们在单个磁带上备份整个文件系统。

将文件备份到这些介质时，你必须按名称引用备份设备。表 3-2 列出了一些常见备份设备的设备名称。

**表 3-2 常见备份设备的设备名称**

| 备份设备 | Linux 设备名称 |
|---|---|
| 软盘 | `/dev/fd0` |
| IDE Zip 驱动器 | `/dev/hdc4` 或 `/dev/hdd4` |
| SCSI Zip 驱动器 | `/dev/sda` (假设它是第一个 SCSI 驱动器；否则，设备名称取决于 SCSI ID) |
| SCSI 磁带驱动器 | `/dev/st0` 或 `/dev/nst0` (n 前缀表示文件复制到磁带后磁带不会回卷) |

## Linux 的商业备份实用程序

在下一节中，我将解释如何使用随 Red Hat Linux 提供的磁带归档程序（tar）来备份和恢复文件。虽然你可以用 tar 管理备份，但许多商业备份实用程序带有图形用户界面和其他功能来简化备份。以下是一些适用于 Red Hat Linux 的知名商业备份实用程序：

- ♦ BRU — 来自 The TOLIS Group, Inc. 的备份和恢复实用程序
  (www.tolisgroup.com)
- ♦ LONE-TAR — 来自 Lone Star Software Corporation 的磁带备份软件包
  (www.cactus.com)
- ♦ Arkeia — 来自 Knox Software 的异构网络备份和恢复软件
  (www.knox-software.com)
- ♦ CTAR — 来自 UniTrends Software Corporation 的 UNIX 系统备份和恢复软件
  (www.unitrends.com)
- ♦ BrightStor ARCserve Backup for Linux — 来自 Computer Associates 的 Linux 系统数据保护技术
  (www3.ca.com/Solutions/Product.asp?ID=3370)

## 使用磁带归档程序 — tar

你可以使用 tar 命令将文件归档到软盘或磁带等设备。tar 程序创建的归档文件可以包含其他目录和文件，并且（可选）压缩归档以实现高效存储。然后归档被写入到指定的设备或另一个文件。事实上，许多软件包都是以压缩的 tar 文件形式分发的。

tar 程序的命令语法如下：

```
tar options destination source
```

这里，options 通常由一系列单个字母指定，每个字母指定 tar 应执行的操作。destination 是备份设备的设备名称。source 是要备份的文件或目录名称的列表。

## 备份和恢复单卷归档

例如，假设你想将 /etc/X11 目录的内容备份到软盘上。以 root 身份登录，将磁盘放入软盘驱动器，然后输入以下命令：

```
tar zcvf /dev/fd0 /etc/X11
```

tar 程序会在每个文件复制到软盘上的压缩 tar 归档时显示文件名列表。在这种情况下，选项为 zcvf，目标为 /dev/fd0（软盘），源为 /etc/X11 目录（隐含其所有子目录及其内容）。你可以使用类似的 tar 命令将文件备份到磁带——只需将 /dev/fd0 替换为磁带设备——例如 SCSI 磁带驱动器的 /dev/st0。

表 3-3 定义了一些常见的 tar 选项。

表 3-3 常见 tar 选项

| 选项 | 执行的操作 |
|---|---|
| c | 创建新的归档 |
| f | 指定命令行的下一个字段中的归档文件或设备名称 |
| M | 指定多卷归档（下一节描述多卷归档） |
| t | 列出归档的内容 |
| v | 显示详细消息 |
| x | 从归档中提取文件 |
| z | 使用 gzip 压缩 tar 归档 |

要查看你在软盘上创建的 tar 归档的内容，请输入以下命令：

```
tar ztf /dev/fd0
```

你应该会看到文件名列表（每个都以 /etc/X11 开头），表明备份中的内容。在此 tar 命令中，t 选项列出 tar 归档的内容。

要从 tar 备份中提取文件，请在以 root 身份登录时执行以下步骤：

- 1. 通过输入以下命令将目录更改为 /tmp：
  `cd /tmp`
  这是你练习从 tar 备份中提取文件的地点。对于实际备份，请更改到适当的位置（通常你会输入 cd /）。
- 2. 输入以下命令：
  `tar zxvf /dev/fd0`
  此 tar 命令使用 x 选项从存储在 /dev/fd0（软盘）上的归档中提取文件。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_477_0.png)



现在如果检查 /tmp 目录的内容，你会注意到 tar 命令会在 /tmp 中创建 etc/X11 目录树，并将 tar 归档中的所有文件恢复到该目录中。tar 命令会去掉归档中文件名的前导 / 并将文件恢复到当前目录。如果你想从软盘上的归档中恢复 /etc/X11 目录，请使用以下命令：

```
tar zxvf /dev/fd0 -C /
```

命令末尾的 / 表示你想要恢复备份文件的目录。

你可以使用 tar 命令创建、查看和恢复归档。你可以将归档存储在文件中或指定设备名称的任何设备中。

## Backing up and restoring a multivolume archive

有时单个存储介质的容量小于存储归档所需的总存储空间。在这种情况下，你可以使用 M 选项创建多卷归档——意味着归档可以跨多个磁带或软盘。然而请注意，你不能创建压缩的多卷归档。这意味着你必须去掉 z 选项。要了解多卷归档的工作原理，以 root 身份登录，将一张磁盘放入软盘驱动器，并输入以下 tar 命令：

```
tar cvfM /dev/fd0 /usr/share/doc/ghostscript*
```

注意选项字母中的 M 选项；它告诉 tar 创建多卷归档。tar 命令在第一张软盘填满时会提示你插入第二张软盘。当你看到以下提示时，取出第一张软盘并插入另一张软盘：

```
Prepare volume #2 for '/dev/fd0' and hit return:
```

当你按下 Enter 时，tar 程序会继续使用第二张软盘。在此示例中，你只需要两张软盘来存储归档；对于更大的归档，tar 程序会继续提示插入软盘，以防需要更多软盘。

要从此多卷归档中恢复，输入 cd /tmp 将目录更改为 /tmp。然后输入

```
tar xvfM /dev/fd0
```

tar 程序会根据需要提示你提供软盘。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_479_0.png)

使用 du -s 命令确定归档目录所需的存储量。例如，以下是如何以千字节为单位获取 /etc 目录的总大小：

```
du -s /etc
11632  /etc
```

结果输出显示 /etc 目录备份至少需要 11,632K 的存储空间。如果你计划在多张高密度软盘上备份，你大约需要 11,632 千字节/1,400 千字节 = 9 张软盘。

## Backing up on tapes

虽然在 tar 命令中使用正确的设备名称进行磁带备份很简单，但你确实需要了解磁带设备的一些细微差别才能很好地使用它。当你使用 tar 将备份写入名为 /dev/st0 的设备（第一个 SCSI 磁带驱动器）时，磁带设备会在 tar 程序完成将归档复制到磁带后自动倒带磁带。/dev/st0 设备被称为可倒带磁带设备，因为它默认会倒带磁带。

如果你的磁带可以容纳数 GB 的数据，你可能希望将多个 tar 归档一个接一个地写入同一盘磁带（否则磁带的大部分可能会空着）。如果你计划这样做，你的磁带设备不应在 tar 程序完成后倒带磁带。为了帮助你处理这种情况，Linux 有几个不可倒带磁带设备。不可倒带的 SCSI 磁带设备称为 /dev/nst0。如果你想在磁带上一个接一个地写入归档，请使用此设备名称。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_479_1.png)

每个归档之后，不可倒带磁带设备会写入一个文件结束 (EOF) 标记以分隔一个归档和下一个。使用 mt 命令控制磁带——你可以从一个标记移动到下一个标记或倒带磁带。例如，在使用 /dev/nst0 设备名称将多个归档写入磁带后，你可以使用以下命令强制磁带倒带：

```
mt -f /dev/nst0 rewind
```

倒带后，你可以使用以下命令将文件从第一个归档提取到当前磁盘目录：

```
tar xvf /dev/nst0
```

之后，你必须越过 EOF 标记到达下一个归档。为此，使用以下 mt 命令：

```
mt -f /dev/nst0 fsf 1
```

这会将磁带定位到下一个归档的开头。现在再次使用 tar xvf 命令读取此归档。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_480_0.png)

如果你在磁带上保存多个归档，你必须自己跟踪归档。这很难记住，因此你最好只在每盘磁带上保存一个归档。

### Performing incremental backups

假设你使用 `tar` 将系统的硬盘备份到磁带上。由于这种完整备份可能需要相当长的时间，你不想每晚重复此任务。（此外，一天内可能只有少数文件发生了更改。）要找到需要备份的文件，你可以使用 `find` 命令列出过去 24 小时内更改过的所有文件：

```
find / -mtime -1 -type f -print
```

此命令打印过去一天内更改过的文件列表。`-mtime -1` 选项表示你想要最后修改时间少于一天的文件。现在你可以将此 `find` 命令与 `tar` 命令结合起来，仅备份过去一天内更改过的文件：

```
tar cvf /dev/st0 `find / -mtime -1 -type f -print`
```

当你将命令放在单反引号之间时，shell 会执行该命令并将输出放在命令行中的该位置。最终结果是 `tar` 程序仅在归档中保存已更改的文件。这项过程为你提供了仅备份自前一天以来更改过的文件的 *增量备份*。

### Performing automated backups

在本迷你书的第 1 章中，我向你展示了如何使用 `crontab` 设置重复性任务（称为 *cron 任务*）。Linux 系统会定期执行这些任务。备份系统是 `crontab` 设施的良好用途。假设你的备份策略如下：

- 每周日凌晨 1:15，系统会在磁带上备份整个磁盘。
- 周一至周六，系统会在凌晨 3:10 执行增量备份，仅保存 24 小时内更改过的文件。

要设置此自动备份计划，以 `root` 身份登录并在名为 `backups` 的文件中输入以下行（此示例假设你使用 SCSI 磁带驱动器）：

```
15 1 * * 0 tar zcvf /dev/st0 /
10 3 * * 1-6 tar zcvf /dev/st0 `find / -mtime -1 -type f -print`
```

接下来，使用以下 `crontab` 命令提交此作业计划：

```
crontab backups
```

现在你应该已设置好自动备份。你所需要做的就是每天在磁带驱动器中放置一盘新磁带。你还应为每盘磁带提供适当的标签。

## Accessing a DOS File System

如果你的硬盘上安装了 Microsoft Windows 95/98/Me，你可能已经在 Red Hat Linux 下挂载了 DOS 分区。如果没有，你可以轻松地在 Red Hat Linux 中挂载 DOS 分区。挂载会使 DOS 目录层次结构作为 Linux 文件系统的一部分出现。为了便于识别 DOS 分区，你可能希望将第一个 DOS 分区挂载为 `/dosc`，第二个挂载为 `/dosd`，以此类推。

要确定你的 DOS 硬盘分区是否设置为自动挂载，输入以下 `grep` 命令在文件 `/etc/fstab` 中查找字符串 `vfat`：

```
grep vfat /etc/fstab
```

如果输出显示包含 `vfat` 的一行或多行，你的 Red Hat Linux 系统会自动挂载 DOS/Windows 硬盘分区。

如果 `grep` 命令在 `/etc/fstab` 中没有显示包含字符串 `vfat` 的行，则你的系统不会自动挂载任何 DOS/Windows 硬盘分区。当然，导致这种情况的非常好的原因可能是你的硬盘上没有 DOS 分区。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_481_0.png)

即使你的硬盘上没有 DOS 分区，你也应该学习如何从 Red Hat Linux 访问 DOS 文件系统，因为你可能需要在 Red Hat Linux 系统上访问 DOS 软盘。

## Mounting a DOS disk partition

要挂载 DOS 硬盘分区或软盘，请使用 `mount` 命令但包含选项 `-t vfat` 以指示文件系统类型为 DOS。例如，如果你的 DOS 分区恰好是你的 `IDE`（Integrated Drive Electronics）驱动器的第一个分区，并且你想将其挂载到 `/dosc` 上，请使用以下 `mount` 命令：

```
mount -t vfat /dev/hda1 /dosc
```



The -t vfat part of the mount command specifies that the device you mount — /dev/hda1 — has an MS-DOS file system. Figure 3-4 illustrates the effect of this mount command.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_482_0.png)

图 3-4：
以下是如何在 /dosc 目录上挂载 DOS 分区的。

图 3-4 显示了 DOS 分区中的目录如何映射到 Linux 文件系统。在 DOS 下的 C:\DOS 目录在 Red Hat Linux 下变为 /dosc/dos。同样，C:\WINDOWS 现在是 /dosc/windows。你可能已经看出规律了。要将 DOS 文件名转换为 Linux（当你将 DOS 分区挂载到 /dosc 时），请执行以下步骤：

- 1. 将 DOS 名称改为小写。
- 2. 将 C:\ 更改为 /dosc/。
- 3. 将所有反斜杠（\）更改为斜杠（/）。

## 挂载 DOS 软盘

就像你在 Red Hat Linux 文件系统上挂载 DOS 硬盘分区一样，你也可以挂载 DOS 软盘。你必须以 root 身份登录才能挂载软盘，但你可以按照本节后半部分所示的步骤设置系统，以便任何用户都可以挂载 DOS 软盘。你还需要知道软盘驱动器的设备名称。默认情况下，Linux 定义了以下两个通用软盘设备名称：

- `/dev/fd0` 是 A 驱动器（第一个软盘驱动器）
- `/dev/fd1` 是 B 驱动器（第二个软盘驱动器，如果你有的话）

关于挂载点，你可以使用文件系统中的任何空目录作为挂载点，但 Red Hat Linux 系统自带一个目录 /mnt/floppy，专门用于挂载软盘。

要将 DOS 软盘挂载到 /mnt/floppy 目录，请将软盘放入驱动器并输入以下命令：

```
mount -t vfat /dev/fd0 /mnt/floppy
```

挂载软盘后，你可以使用 Linux 复制命令（cp）向软盘复制文件或从软盘复制文件。要将当前目录中的文件 gnome1.pcx 复制到软盘，请输入以下内容：

```
cp gnome1.pcx /mnt/floppy
```

同样，要查看软盘的内容，请输入以下内容：

```
ls /mnt/floppy
```

如果你想从驱动器中取出软盘，请先卸载软盘驱动器。卸载会移除软盘文件系统与 Red Hat Linux 文件系统上的挂载点之间的关联。使用 umount 命令像这样卸载软盘：

```
umount /dev/fd0
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_483_0.png)

你可以设置 Red Hat Linux 系统，使任何用户都可以挂载 DOS 软盘。例如，要允许任何用户将 A 驱动器中的 DOS 软盘挂载到 /a 目录，请执行以下步骤：

- 1. **以 root 身份登录。**
- 2. **通过在终端窗口中输入以下命令创建 /a 目录（挂载点）：**
  `mkdir /a`
- 3. **在文本编辑器（如 vi 或 Emacs）中编辑 /etc/fstab 文件，插入以下行，然后保存文件并退出编辑器：**
  `/dev/fd0   /a   vfat   noauto,user   0 0`

该行中的第一个字段是软盘驱动器的设备名称（/dev/fd0）；第二个字段是挂载目录（/a）；第三个字段显示文件系统的类型（vfat）。user 选项（出现在 noauto 旁边）使所有用户能够挂载 DOS 软盘。

4. 注销并以普通用户身份登录。

5. 为确认你能以普通用户而不仅仅是以 root 挂载 DOS 软盘，请将 DOS 软盘插入 A 驱动器并输入以下命令：

```
mount /a
```

挂载操作应成功，并且当你输入命令 ls /a 时，你应该能看到 DOS 软盘的列表。

6. 要卸载 DOS 软盘，请输入 umount /a。

## 使用 mtools

访问 MS-DOS 文件系统的一种方法是使用 mount 命令挂载 DOS 硬盘或软盘，然后使用常规 Linux 命令（如 ls 和 cp）来操作已挂载的 DOS 文件系统。这种挂载 DOS 文件系统的方法对于硬盘来说是可以的。Linux 可以在启动时自动挂载 DOS 分区，并且你可以在任何时候访问硬盘上的 DOS 目录。

然而，如果你想要 DOS 软盘的快速目录列表，挂载很快就会变得相当繁琐。首先，你必须挂载软盘驱动器。然后你必须使用 ls 命令。最后，在弹出软盘之前你必须使用 umount 命令。

这就是 mtools 包派上用场的地方。mtools 包实现了大多数常见的 DOS 命令；命令使用与 DOS 相同的名称，只是每个命令前加上 m 前缀。因此，获取目录列表的命令是 mdir，而 mcopy 用于复制文件。mtools 最好的地方在于，你不必挂载软盘就可以使用 mtools 命令。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_484_0.png)

因为 mtools 命令会读写物理设备（软盘），所以你必须以 root 身份登录才能执行这些命令。如果你希望任何用户都能访问 mtools 命令，你必须更改软盘驱动器设备的权限设置。使用以下命令允许任何人读取和写入第一个软盘驱动器：

```
chmod o+rw /dev/fd0
```

## 尝试 mtools

要尝试 mtools，请按照以下步骤操作：

- 1. **以 root 身份登录或输入 su - 然后输入 root 密码。**
- 2. **将 MS-DOS 软盘放入系统 A 驱动器中。**
- 3. **输入 mdir。**
  你应该会看到软盘的目录（以标准 DOS 目录列表格式显示）。

通常，你会使用 mtools 实用程序来访问软盘。默认配置文件 /etc/mtools.conf 设置为将软盘驱动器作为 A 驱动器访问。虽然你可以编辑该文件为 DOS 硬盘分区定义 C 和 D 驱动器，但你也可以使用 Linux mount 命令挂载它们来访问硬盘分区。因为你可以在启动时自动挂载硬盘分区，所以通过 Linux 命令访问它们通常同样容易。

你也可以通过 mtools 访问 Iomega Zip 驱动器。只需指定一个驱动器字母和相应设备的 filename 即可。对于内置 IDE（ATAPI）Zip 驱动器，请尝试使用 /dev/hdd4 作为设备文件，并在 /etc/mtools.conf 文件中添加以下行：

```
drive e: file="/dev/hdd4"
```

之后你应该能够使用 mtools 命令访问 Zip 驱动器（将其称为 E 驱动器）。例如，要查看目录列表，请将 Zip 磁盘放入 Zip 驱动器并输入：

```
mdir e:
```

## 学习 mtools 命令

mtools 包是一组实用程序的集合。到目前为止，我一直在使用 mdir——它是 DOS 中 DIR 命令的 mtools 对应项。其他 mtools 命令也相当容易使用。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_485_0.png)

如果你熟悉 MS-DOS 命令，使用 mtools 命令就很简单。将 DOS 命令以小写字母输入，并记得在每个命令前加上 m。因为 Linux 命令和文件名区分大小写，所以在输入 mtools 命令时必须全部使用小写字母。

表 3-4 总结了 mtools 中可用的命令。

### 表 3-4 mtools 命令

| mtools 实用程序 | MS-DOS 命令（如果有） | mtools 实用程序的功能 |
|---|---|---|
| mattrib | ATTRIB | 更改 MS-DOS 文件属性标志 |
| mbadblocks |  | 测试软盘并在文件分配表（FAT）中标记坏块 |
| mcd | CD | 更改 MS-DOS 目录 |
| mcopy | COPY | 在 MS-DOS 和 Linux 之间复制文件 |
| mdel | DEL or ERASE | 删除 MS-DOS 文件 |
| mdeltree | DELTREE | 递归删除 MS-DOS 目录 |
| mdir | DIR | 显示 MS-DOS 目录列表 |
| mdu |  | 列出目录及其内容占用的空间 |
| mformat | FORMAT | 在低级格式化的软盘上放置 MS-DOS 文件系统。（在 Red Hat Linux 中使用 fdformat 对软盘进行低级格式化。） |
| minfo |  | 获取有关 MS-DOS 文件系统的信息 |
| mkmanifest |  | 制作短名称等效列表 |
| mlabel | LABEL | 初始化 MS-DOS 卷标 |
| mmd | MD or MKDIR | 创建 MS-DOS 目录 |
| mmove |  | 移动或重命名 MS-DOS 文件或子目录 |
| mmount |  | 挂载 MS-DOS 磁盘 |
| mpartition |  | 创建 MS-DOS 文件系统作为分区 |
| mrd | RD or RMDIR | 删除 MS-DOS 目录 |
| mren | REN or RENAME | 重命名现有 MS-DOS 文件 |
| mshowfat |  | 显示 MS-DOS 文件的 FAT 条目 |
| mtoolstest |  | 测试并显示当前 mtools 配置 |
| mtype | TYPE | 显示 MS-DOS 文件的内容 |
| mwrite | COPY | 将 Linux 文件复制到 MS-DOS |
| mzip |  | 对 SCSI Zip 磁盘执行某些操作 |

你可以像使用相应的 DOS 命令一样使用 mtools 命令。例如，mdir 命令的工作方式与 DOS 中的 DIR 命令相同。表 3-4 中显示的所有其他 mtools 命令也一样。



你可以使用通配符（如 *）与 mtools 命令，但必须记住 Linux shell 是首先看到你命令的程序。如果你不想让 shell 到处展开通配符，请对包含任何通配符的文件名使用引号。例如，要将 A 驱动器中的所有 *.txt 文件复制到当前 Red Hat Linux 目录，请使用以下命令：

```
mcopy "a:*.txt"
```

如果省略引号，shell 会尝试使用当前 Linux 目录中的文件名展开字符串 a:*.txt。它还会尝试从 DOS 软盘复制这些文件（如果有的话）。

另一方面，如果你想从 Linux 目录复制文件到 DOS 软盘，你希望 shell 展开任何通配符。例如，要将当前 Linux 目录中的所有 *.jpg 文件复制到 DOS 软盘，请这样使用 mcopy：

```
mcopy *.jpg a:
```

使用 mtools 实用程序时，你可以使用反斜杠字符 (\ ) 作为目录分隔符，就像在 DOS 中一样。然而，当你输入包含反斜杠字符的文件名时，必须用双引号 ("") 将名称括起来。例如，这里有一个命令可以将 A 驱动器上子目录中的文件复制到当前 Linux 目录：

```
mcopy "a:\test\sample.dat"
```

## 格式化 DOS 软盘

假设你在家用 PC 上运行 Red Hat Linux，且系统上已不再有 MS-DOS，但你想将一些文件复制到 MS-DOS 软盘上并带到办公室。如果已有格式化的 MS-DOS 软盘，你只需挂载该软盘并使用 Linux cp 命令将文件复制到软盘即可。但如果没有格式化的 DOS 软盘怎么办？mtools 软件包再次派上用场。

mtools 软件包提供了 mformat 实用程序，可将软盘格式化为在 MS-DOS 中使用。与一次性格式化软盘的 DOS format 命令不同，mformat 命令要求你遵循两步流程：

- 1. 使用 fdformat 命令对软盘进行低级格式化。

fdformat 命令使用软盘设备名称作为参数；设备名称包含格式化软盘所需的所有参数。

图 3-5 说明了软盘驱动器设备的设备命名约定。如图 3-5 所示，你可以使用以下命令格式化系统 A 驱动器中的 3.5 英寸高密度软盘：

```
fdformat /dev/fd0H1440
```

## 2. 使用 mformat 命令在低级格式化的软盘上放置 MS-DOS 文件系统。

如果软盘在 A 驱动器中，输入以下命令创建格式化的 DOS 软盘：

```
mformat a:
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_488_0.png)

图 3-5：
这就是在 Red Hat Linux 中构造软盘驱动器名称的方法。

表示软盘容量（以千字节为单位）的 3 或 4 位数字：
5.25 英寸：360、720 或 1200
3.5 英寸：360、720 或 1440

以下其中一个字母：
d = 低密度 5.25 英寸
D = 低密度 3.5 英寸
h = 高密度 5.25 英寸
H = 高密度 3.5 英寸

以下其中一个字母：
0 = 第一个软盘驱动器 (A:)
1 = 第二个软盘驱动器 (B:)

### 第 4 章：管理应用程序

## 本章内容

- 学习 RPM
- 安装和移除软件 RPM
- 从源文件构建应用程序
- 使用 Red Hat Network 更新 Red Hat Linux 应用程序

大多数 Red Hat Linux 软件包以名为 Red Hat Package Manager（RPM）文件的特殊文件形式分发，因此你应该知道如何安装或移除以 RPM 文件形式提供的软件包。在本章中，我将向你展示如何使用 RPM 文件。

许多其他开源软件包以源代码形式提供，通常在压缩归档中。你必须构建并安装软件才能使用它。我描述了下载、构建和安装基于源的软件包时通常遵循的步骤。

最后，我简要介绍了 Red Hat Network 以及在注册后如何使用 Red Hat 的 Update 代理来更新 Red Hat Linux 应用程序。

## 使用 Red Hat Package Manager

Red Hat Package Manager（RPM）是一种将软件产品所需的所有文件打包到单个文件中的系统——称为 RPM 文件或简称为 RPM。事实上，整个 Red Hat Linux 发行版就是大量 RPM。处理 RPM 的最佳方式是通过 RPM 命令。你必须在终端窗口或文本控制台的 shell 提示符下输入这些命令。

## 使用 RPM 命令

当你从随附 DVD 安装 Red Hat Linux 时，Red Hat 安装程序使用 rpm 命令解包软件包（RPM 文件）并将内容复制到你的硬盘。

你不必了解 RPM 文件的内部结构，但应该知道如何使用 rpm 命令来处理 RPM 文件。以下是你可以使用 rpm 命令完成的一些操作：

- 查找系统上已安装的 RPM 的版本号和其他信息。
- 从 RPM 安装新的软件包。你可能会安装在初始安装期间跳过的软件包。例如，在重新构建内核之前，你必须安装 Linux 内核的源文件。你可以使用 `rpm` 命令完成此操作。
- 移除（卸载）之前从 RPM 安装的不需要的软件。如果你发现很少（或从不）使用某个软件包，可以卸载它以收回磁盘空间。
- 使用新版本升级旧版本的 RPM。你可以在从 Red Hat 的 FTP 服务器下载软件包的新版本后进行升级。通常你必须升级 RPM 才能受益于新版本中的修复。
- 验证 RPM 是否正常工作。你可以验证软件包以检查所有必要文件是否位于正确的位置。

如你所见，rpm 命令功能多样——它可以根据你使用的选项执行许多不同的操作。

如果你忘记了 rpm 选项，输入以下命令查看列表：

```
rpm --help | more
```

rpm 选项的数量会让你惊讶！

## 了解 RPM 文件名

RPM 包含多个文件，但在 Red Hat Linux 系统上它显示为单个文件。按照惯例，RPM 文件名具有特定格式。要查看随附 DVD 上一些 RPM 文件的名称，请按照以下步骤操作：

- 1. **将第一张 DVD 放入 DVD 驱动器。如果使用 GNOME 或 KDE 图形桌面，DVD 应该会自动挂载。否则，使用以下命令挂载它（你必须以 root 身份登录）：**
- `mount /dev/cdrom`
- 2. **输入以下命令进入 RPM 所在的目录：**
- `cd /mnt/cdrom/RedHat/RPMS`
- 3. **使用 ls 命令查看列表。例如，要查看名称以 cups 开头的 RPM，输入**
- `ls cups*`

你应该会看到如下所示的列表：

```
cups-1.1.19-5.i386.rpm
cups-libs-1.1.19-5.i386.rpm
```

从列表中你可以猜到，RPM 文件名以 .rpm 扩展名结尾。要了解文件名的各个部分，请考虑以下 RPM：

```
cups-1.1.19-5.i386.rpm
```

此文件名由以下部分组成，以连字符 (-) 分隔：

- 软件包名称 — `cups`
- 版本号 — `1.1.19`
- 发布号 — `5`（这是 Red Hat 分配的发布号）
- 架构 — `i386`（该软件包适用于 Intel 80386 兼容处理器）

通常，软件包名称足够描述性，可以让你猜测 RPM 可能包含的内容。版本号与软件包的当前版本号相同（即使以其他形式分发，例如 tar 文件）。Red Hat 分配发布号以跟踪更改。对于要在搭载 Intel x86 兼容处理器的 PC 上安装的 RPM，架构应为 i386 或 noarch。

## 查找 RPM 信息

在安装软件包时，rpm 命令会构建已安装 RPM 的数据库。你可以使用 rpm -q 命令查询此数据库以查找系统上已安装软件包的信息。

例如，要查找系统上安装的 Linux 内核的版本号，输入以下 rpm -q 命令

```
rpm -q kernel
```

你应该会看到类似以下内容的响应：

```
kernel-2.4.20-20.1
```

响应是内核的 RPM 名称（这是内核的可执行版本，而不是源文件）。名称与 RPM 文件名相同，只是最后部分——i386.rpm——未显示。在这种情况下，RPM 的版本部分告诉你内核是 2.4.20。



你可以通过使用以下命令查看所有已安装 RPM 的列表：

```
rpm -qa
```

你会看到一长串 RPM 在屏幕上滚动。要一次查看一屏内容，输入

```
rpm -qa | more
```

如果你想搜索特定软件包，可以将 rpm -qa 的输出传递给 grep 命令。例如，要查看名称中包含 kernel 的所有软件包，输入

```
rpm -qa | grep kernel
```

结果取决于系统上安装了哪些内核 RPM 组件。例如，在我的系统上，该命令显示如下内容：

```
kernel-pcmcia-cs-3.1.31-13
kernel-source-2.4.20-20.1.2013.nptl
kernel-2.4.20-20.1.2013.nptl
```

使用 rpm -q 命令可以查询远不止软件包版本号的信息。通过添加单字母选项，你可以获取其他有用的信息。例如，尝试以下命令查看 kernel 软件包中的文件：

```
rpm -ql kernel
```

以下是该命令输出的几行：

```
/boot/System.map-2.4.20-20.1.2013.nptl
/boot/config-2.4.20-20.1.2013.nptl
/boot/vmlinuz-2.4.20-20.1.2013.nptl
/boot/vmlinuz-2.4.20-20.1.2013.nptl
/dev/shm
/lib/modules
/lib/modules/2.4.20-20.1.2013.nptl/build
/lib/modules/2.4.20-20.1.2013.nptl/kernel
/lib/modules/2.4.20-20.1.2013.nptl/kernel/arch
/lib/modules/2.4.20-20.1.2013.nptl/kernel/arch/i386
/lib/modules/2.4.20-20.1.2013.nptl/kernel/arch/i386/kernel
/lib/modules/2.4.20-20.1.2013.nptl/kernel/arch/i386/kernel/cpuid.o
/lib/modules/2.4.20-20.1.2013.nptl/kernel/arch/i386/kernel/edd.o
/lib/modules/2.4.20-20.1.2013.nptl/kernel/arch/i386/kernel/microcode.o
/lib/modules/2.4.20-20.1.2013.nptl/kernel/arch/i386/kernel/msr.o
(rest of the listing deleted)
```

以下是查询软件包信息的 rpm -q 命令的几种更有用的形式（要使用这些 rpm -q 命令中的任何一个，输入命令，后跟软件包名称）：

- rpm -qc — 列出软件包中的所有配置文件。
- rpm -qd — 列出软件包中的所有文档文件。这些通常是在线手册页（也称为 man 页面）。
- rpm -qf — 显示指定文件所属的软件包名称（如果有）。
- rpm -qi — 显示软件包的详细信息，包括版本号、大小、安装日期和简要描述。
- rpm -ql — 列出软件包中的所有文件。对于某些软件包，这可能是一个非常长的列表。
- rpm -qs — 列出软件包中所有文件的状态。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_494_0.png)

这些 rpm 命令仅提供已安装软件包的信息。如果你想查找未安装的 RPM 文件的信息，请在每个命令的命令行选项后添加字母 p。例如，要查看名为 rdist-6.1.5-27.1.i386.rpm 的 RPM 文件中的文件列表，请使用以下命令：

```
rpm -qpl rdist-*.rpm
```

当然，这仅在当前目录包含该 RPM 文件时才有效。

## 安装 RPM

要安装 RPM，请使用 rpm -i 命令。你必须提供 RPM 文件名作为参数。一个典型示例是从本书附带的包含 Red Hat Linux RPM 的 DVD 安装 RPM。照常，你需要挂载 DVD 并切换到 RPM 所在的目录。然后使用 rpm -i 命令安装 RPM。如果你想查看 RPM 安装的进度，请使用 rpm -ivh。解包软件包时会出现一系列井号（#）。

例如，要从附带 DVD 安装 kernel-source RPM（其中包含 Linux 操作系统的源文件），我插入 DVD 并在挂载后输入以下命令：

```
cd /mnt/cdrom/RedHat/RPMS
rpm -ivh kernel-source*
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_495_0.png)

你不必输入完整的 RPM 文件名——你可以使用名称开头的几个字符后跟一个星号（*）。确保你输入的名称足够以唯一标识 RPM 文件。

如果你尝试安装已安装的 RPM，rpm -i 命令会显示错误消息。例如，当我在系统上输入以下命令安装 man 软件包时，会发生以下情况：

```
rpm -i man-1*
```

我从 rpm -i 命令收到以下错误消息：

```
package man-1.5k-8 is already installed
```

要强制 rpm 命令即使存在错误也安装软件包，只需在 rpm -i 命令中添加 --force，如下所示：

```
rpm -i --force man-1*
```

## 移除 RPM

如果你意识到自己并不真正需要该软件，可能需要移除——卸载——软件包。例如，如果你安装了 X Window System 开发包，但发现自己对编写 X 应用程序不感兴趣，可以通过使用 rpm -e 命令轻松移除该软件包。

在移除软件包之前，你必须知道软件包的名称。找到名称的一个好方法是使用 rpm -qa 结合 grep 搜索适当的 RPM 文件。例如，要定位 X Window System 开发 RPM，请尝试以下命令：

```
rpm -qa | grep XFree86
```

XFree86-devel 恰好是 X Window System 开发 RPM 的软件包名称。要移除该软件包，输入

```
rpm -e XFree86-devel
```

要移除 RPM，你不需要完整的 RPM 文件名；你只需要软件包名称——文件名中版本号前破折号 (-) 之前的第一部分。

rpm -e 命令不会移除其他软件包需要的软件包。例如，要移除 vim-common 软件包，输入以下命令：

```
rpm -e vim-common
```

你会收到以下错误消息：

```
error: Failed dependencies:
vim-common is needed by (installed) vim-minimal-6.2.14-1
vim-common is needed by (installed) vim-enhanced-6.2.14-1
```

## 升级 RPM

使用 rpm -U 命令升级 RPM。你必须提供包含新软件的 RPM 文件名。例如，如果我的系统上安装了 Apache httpd（Web 服务器）的 2.0.40 版本，但我想升级到 2.0.45 版本，我从 Red Hat 更新站点之一（列在 www.redhat.com/mirrors.html）下载 RPM 文件 httpd-2.0.45-10.i386.rpm 并使用以下命令：

```
rpm -U httpd-2.0.45-10.i386.rpm
```

rpm 命令通过移除 httpd 软件包的旧版本并安装新的 RPM 来执行升级。

在可能的情况下，你应该升级而不是移除旧软件包并安装新软件包。升级会自动保存旧的配置文件，这可以免去你在全新安装后重新配置软件的麻烦。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_496_0.png)

当你升级包含可运行 Linux 内核的内核软件包时，请使用 rpm -i 命令（而不是 rpm -U 命令）安装它。这样你就不会覆盖当前内核。

## 验证 RPM

你可能不经常这样做，但如果怀疑软件包未正确安装，请使用 rpm -V 命令验证它。例如，要验证 kernel 软件包，输入以下内容：

```
rpm -V kernel
```

这会导致 rpm 将软件包中每个文件的大小和其他属性与原始文件进行比较。如果一切验证正确，rpm -V 命令不会打印任何内容。如果存在任何差异，你会看到它们的报告。例如，我已修改了 Apache httpd Web 服务器的配置文件。以下是验证 httpd 软件包时我输入的内容：

```
rpm -V httpd
```

我得到的结果如下：

```
S.5....T c /etc/httpd/conf/httpd.conf
```

在这种情况下，rpm -V 的输出告诉我一个配置文件已更改。该命令输出的每一行都有三个部分：

- 该行以八个字符开头：每个字符表示发现的差异类型。例如，S 表示大小不同，T 表示最后修改时间不同。表 4-1 显示了每个字符及其含义。句点表示特定属性与原始属性匹配。
- 对于配置文件，接下来会出现一个 c；否则，该字段为空。这就是判断文件是否为配置文件的依据。通常，如果配置文件已更改，你不必担心；你可能自己做了更改。
- 行的最后一部分是文件的完整路径名。从这一部分，你可以确切地知道文件的位置。

**表 4-1 RPM 验证报告中使用的字符**

| 字符 | 含义 |
|---|---|
| S | 大小已更改。 |
| M | 权限和文件类型不同。 |
| 5 | 使用 MD5 算法计算的校验和不同。 |
| D | 设备类型不同。 |
| L | 符号链接不同。 |
| U | 文件的用户不同。 |
| G | 文件的组不同。 |
| T | 文件的修改时间不同。 |

## 从源文件构建软件包

许多开源软件包以源代码形式分发，没有可执行二进制文件。在你可以使用此类软件之前，你必须通过编译构建可执行二进制文件，并且必须遵循某些说明来安装软件包。在本节中，我将向你展示如何从源文件构建软件包。

### 下载和解包软件

开源软件源文件通常以压缩的 tar 归档形式分发。这些归档由 tar 程序创建并使用 gzip 程序压缩。分发形式是一个带有 .tar.gz 或 .tar.Z 扩展名的单个大文件——通常称为压缩 tar 包。如果你想要该软件，你必须下载压缩的 tar 包并解包它。




使用匿名 FTP 或通过 Web 浏览器下载压缩的 tar 文件。通常，这对你来说几乎不需要任何操作，只需点击链接并将文件保存到系统中的适当目录即可。

如果你想尝试下载和构建软件包，可以练习使用 X 多媒体系统（XMMS）——一个用于播放 MP3 及其他多媒体文件的图形化 X 应用程序。XMMS 已随 Red Hat Linux 捆绑，并且应该已经安装在你的系统上。然而，重新下载并重建 XMMS 包也不会有什么坏处。

从 www.xmms.org/download.php 下载 XMMS 的源文件。这些文件以压缩 tar 归档的形式打包。点击源文件的 ftp 链接，然后将它们保存到 Red Hat Linux 系统中的 /usr/local/src 目录。（请务必以 root 身份登录；否则你无法保存到 /usr/local/src 目录。）

下载压缩的 tar 文件后，使用以下 tar 命令检查其内容：

```
tar ztf xmms*.gz | more
```

你应该会看到类似以下的列表：

```
xmms-1.2.7/
xmms-1.2.7/Makefile.in
xmms-1.2.7/README
xmms-1.2.7/stamp-h.in
xmms-1.2.7/ABOUT-NLS
xmms-1.2.7/AUTHORS
xmms-1.2.7/COPYING
xmms-1.2.7/ChangeLog
xmms-1.2.7/INSTALL
xmms-1.2.7/Makefile.am
xmms-1.2.7/NEWS
xmms-1.2.7/TODO
xmms-1.2.7/acconfig.h
xmms-1.2.7/acinclude.m4
xmms-1.2.7/aclocal.m4
xmms-1.2.7/config.guess
xmms-1.2.7/config.h.in
xmms-1.2.7/config.sub
xmms-1.2.7/configure
... rest of the output not shown ...
```

此 tar 命令的输出显示了归档中的内容，并让你了解解包归档后将创建哪些目录。在本例中，将在当前目录中创建一个名为 xmms-1.2.7 的目录，在我的情况下是 /usr/local/src。从列表中，

你还可以了解到用于编写该包的编程语言。如果看到 `.c` 和 `.h` 文件，这意味着源文件是用 C 编程语言编写的，而 C 语言被用于编写许多开源软件包。

要提取压缩的 `tar` 归档的内容，请输入以下 `tar` 命令：

```
tar zxvf xmms*.gz
```

你将再次看到长长的[content]
使用匿名 FTP 或通过 Web 浏览器下载压缩的 tar 文件。通常，这对你来说几乎不需要任何操作，只需点击链接并将文件保存到系统中的适当目录即可。

如果你想尝试下载和构建软件包，可以练习使用 X 多媒体系统（XMMS）——一个用于播放 MP3 及其他多媒体文件的图形化 X 应用程序。XMMS 已随 Red Hat Linux 捆绑，并且应该已经安装在你的系统上。然而，重新下载并重建 XMMS 包也不会有什么坏处。

从 www.xmms.org/download.php 下载 XMMS 的源文件。这些文件以压缩 tar 归档的形式打包。点击源文件的 ftp 链接，然后将它们保存到 Red Hat Linux 系统中的 /usr/local/src 目录。（请务必以 root 身份登录；否则你无法保存到 /usr/local/src 目录。）

下载压缩的 tar 文件后，使用以下 tar 命令检查其内容：

```
tar ztf xmms*.gz | more
```

你应该会看到类似以下的列表：

```
xmms-1.2.7/
xmms-1.2.7/Makefile.in
xmms-1.2.7/README
xmms-1.2.7/stamp-h.in
xmms-1.2.7/ABOUT-NLS
xmms-1.2.7/AUTHORS
xmms-1.2.7/COPYING
xmms-1.2.7/ChangeLog
xmms-1.2.7/INSTALL
xmms-1.2.7/Makefile.am
xmms-1.2.7/NEWS
xmms-1.2.7/TODO
xmms-1.2.7/acconfig.h
xmms-1.2.7/acinclude.m4
xmms-1.2.7/aclocal.m4
xmms-1.2.7/config.guess
xmms-1.2.7/config.h.in
xmms-1.2.7/config.sub
xmms-1.2.7/configure
... rest of the output not shown ...
```

此 tar 命令的输出显示了归档中的内容，并让你了解解包归档后将创建哪些目录。在本例中，将在当前目录中创建一个名为 xmms-1.2.7 的目录，在我的情况下是 /usr/local/src。从列表中，

你还可以了解到用于编写该包的编程语言。如果看到 `.c` 和 `.h` 文件，这意味着源文件是用 C 编程语言编写的，而 C 语言被用于编写许多开源软件包。

要提取压缩的 `tar` 归档的内容，请输入以下 `tar` 命令：

```
tar zxvf xmms*.gz
```

你将再次看到长长的[content]
使用匿名 FTP 或通过 Web 浏览器下载压缩的 tar 文件。通常，这对你来说几乎不需要任何操作，只需点击链接并将文件保存到系统中的适当目录即可。

如果你想尝试下载和构建软件包，可以练习使用 X 多媒体系统（XMMS）——一个用于播放 MP3 及其他多媒体文件的图形化 X 应用程序。XMMS 已随 Red Hat Linux 捆绑，并且应该已经安装在你的系统上。然而，重新下载并重建 XMMS 包也不会有什么坏处。

从 www.xmms.org/download.php 下载 XMMS 的源文件。这些文件以压缩 tar 归档的形式打包。点击源文件的 ftp 链接，然后将它们保存到 Red Hat Linux 系统中的 /usr/local/src 目录。（请务必以 root 身份登录；否则你无法保存到 /usr/local/src 目录。）

下载压缩的 tar 文件后，使用以下 tar 命令检查其内容：

```
tar ztf xmms*.gz | more
```

你应该会看到类似以下的列表：

```
xmms-1.2.7/
xmms-1.2.7/Makefile.in
xmms-1.2.7/README
xmms-1.2.7/stamp-h.in
xmms-1.2.7/ABOUT-NLS
xmms-1.2.7/AUTHORS
xmms-1.2.7/COPYING
xmms-1.2.7/ChangeLog
xmms-1.2.7/INSTALL
xmms-1.2.7/Makefile.am
xmms-1.2.7/NEWS
xmms-1.2.7/TODO
xmms-1.2.7/acconfig.h
xmms-1.2.7/acinclude.m4
xmms-1.2.7/aclocal.m4
xmms-1.2.7/config.guess
xmms-1.2.7/config.h.in
xmms-1.2.7/config.sub
xmms-1.2.7/configure
... rest of the output not shown ...
```

此 tar 命令的输出显示了归档中的内容，并让你了解解包归档后将创建哪些目录。在本例中，将在当前目录中创建一个名为 xmms-1.2.7 的目录，在我的情况下是 /usr/local/src。从列表中，

你还可以了解到用于编写该包的编程语言。如果看到 `.c` 和 `.h` 文件，这意味着源文件是用 C 编程语言编写的，而 C 语言被用于编写许多开源软件包。

要提取压缩的 `tar` 归档的内容，请输入以下 `tar` 命令：

```
tar zxvf xmms*.gz
```

你将再次看到长长的[content]
使用匿名 FTP 或通过 Web 浏览器下载压缩的 tar 文件。通常，这对你来说几乎不需要任何操作，只需点击链接并将文件保存到系统中的适当目录即可。

如果你想尝试下载和构建软件包，可以练习使用 X 多媒体系统（XMMS）——一个用于播放 MP3 及其他多媒体文件的图形化 X 应用程序。XMMS 已随 Red Hat Linux 捆绑，并且应该已经安装在你的系统上。然而，重新下载并重建 XMMS 包也不会有什么坏处。

从 www.xmms.org/download.php 下载 XMMS 的源文件。这些文件以压缩 tar 归档的形式打包。点击源文件的 ftp 链接，然后将它们保存到 Red Hat Linux 系统中的 /usr/local/src 目录。（请务必以 root 身份登录；否则你无法保存到 /usr/local/src 目录。）

下载压缩的 tar 文件后，使用以下 tar 命令检查其内容：

```
tar ztf xmms*.gz | more
```

你应该会看到类似以下的列表：

```
xmms-1.2.7/
xmms-1.2.7/Makefile.in
xmms-1.2.7/README
xmms-1.2.7/stamp-h.in
xmms-1.2.7/ABOUT-NLS
xmms-1.2.7/AUTHORS
xmms-1.2.7/COPYING
xmms-1.2.7/ChangeLog
xmms-1.2.7/INSTALL
xmms-1.2.7/Makefile.am
xmms-1.2.7/NEWS
xmms-1.2.7/TODO
xmms-1.2.7/acconfig.h
xmms-1.2.7/acinclude.m4
xmms-1.2.7/aclocal.m4
xmms-1.2.7/config.guess
xmms-1.2.7/config.h.in
xmms-1.2.7/config.sub
xmms-1.2.7/configure
... rest of the output not shown ...
```

此 tar 命令的输出显示了归档中的内容，并让你了解解包归档后将创建哪些目录。在本例中，将在当前目录中创建一个名为 xmms-1.2.7 的目录，在我的情况下是 /usr/local/src。从列表中，

你还可以了解到用于编写该包的编程语言。如果看到 `.c` 和 `.h` 文件，这意味着源文件是用 C 编程语言编写的，而 C 语言被用于编写许多开源软件包。

要提取压缩的 `tar` 归档的内容，请输入以下 `tar` 命令：

```
tar zxvf xmms*.gz
```

你将再次看到长长的[content]
使用匿名 FTP 或通过 Web 浏览器下载压缩的 tar 文件。通常，这对你来说几乎不需要任何操作，只需点击链接并将文件保存到系统中的适当目录即可。

如果你想尝试下载和构建软件包，可以练习使用 X 多媒体系统（XMMS）——一个用于播放 MP3 及其他多媒体文件的图形化 X 应用程序。XMMS 已随 Red Hat Linux 捆绑，并且应该已经安装在你的系统上。然而，重新下载并重建 XMMS 包也不会有什么坏处。

从 www.xmms.org/download.php 下载 XMMS 的源文件。这些文件以压缩 tar 归档的形式打包。点击源文件的 ftp 链接，然后将它们保存到 Red Hat Linux 系统中的 /usr/local/src 目录。（请务必以 root 身份登录；否则你无法保存到 /usr/local/src 目录。）

下载压缩的 tar 文件后，使用以下 tar 命令检查其内容：

```
tar ztf xmms*.gz | more
```

你应该会看到类似以下的列表：

```
xmms-1.2.7/
xmms-1.2.7/Makefile.in
xmms-1.2.7/README
xmms-1.2.7/stamp-h.in
xmms-1.2.7/ABOUT-NLS
xmms-1.2.7/AUTHORS
xmms-1.2.7/COPYING
xmms-1.2.7/ChangeLog
xmms-1.2.7/INSTALL
xmms-1.2.7/Makefile.am
xmms-1.2.7/NEWS
xmms-1.2.7/TODO
xmms-1.2.7/acconfig.h
xmms-1.2.7/acinclude.m4
xmms-1.2.7/aclocal.m4
xmms-1.2.7/config.guess
xmms-1.2.7/config.h.in
xmms-1.2.7/config.sub
xmms-1.2.7/configure
... rest of the output not shown ...
```

此 tar 命令的输出显示了归档中的内容，并让你了解解包归档后将创建哪些目录。在本例中，将在当前目录中创建一个名为 xmms-1.2.7 的目录，在我的情况下是 /usr/local/src。从列表中，

你还可以了解到用于编写该包的编程语言。如果看到 `.c` 和 `.h` 文件，这意味着源文件是用 C 编程语言编写的，而 C 语言被用于编写许多开源软件包。

要提取压缩的 `tar` 归档的内容，请输入以下 `tar` 命令：

```
tar zxvf xmms*.gz
```

你将再次看到文件列表，随着它们从归档中提取并复制到硬盘上的适当目录。

现在你可以开始构建软件了。

## 从源文件构建软件

解包压缩的 `tar` 归档后，所有源文件都将位于一个目录中，该目录的名称通常是软件包的名称加上版本号后缀。例如，XMMS 版本 1.2.7 的源文件被提取到 `xmms-1.2.7` 目录。要开始构建软件，使用以下命令更改目录：

```
cd xmms*
```

你不必输入完整名称——shell 可以扩展目录名并更改到 `xmms-1.2.7` 目录。

几乎所有软件包都附带某种 `README` 或 `INSTALL` 文件——一个文本文件，告诉你如何构建和安装该包。XMMS 也不例外；它附带一个 `README` 文件，你可以通过输入 `more README` 来阅读。还有一个 `INSTALL` 文件，其中包含构建和安装 XMMS 的说明。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_499_0.png)

大多数开源软件包，包括 XMMS，还附带一个名为 `COPYING` 的文件。该文件包含 GNU 通用公共许可证（GPL）的全文，其中规定了你可以使用和重新分发软件的条件。如果你不熟悉 GNU GPL，请阅读此文件并将其展示给你的法律顾问，以便全面解释并评估其对你业务的适用性。

要构建软件包，请遵循 `README` 或 `INSTALL` 文件中的说明。对于 XMMS 包，`README` 文件列出了一些先决条件（如库）并告诉你输入哪些命令来构建和安装该包。在 XMMS 的情况下，说明告诉你使用以下步骤：

- 1. **输入 ./configure 以运行一个 shell 脚本，该脚本检查你的系统配置并创建一个名为 Makefile 的文件——make 命令用来构建和安装包的文件。**（你可以输入 ./configure --help 以查看 configure 接受的选项列表。）
- 
- 2. **输入 make 以构建软件。**
  此步骤编译所有子目录中的源文件（编译源代码会将每个源文件转换为对象文件——包含你的 PC 处理器可以理解的二进制指令的文件）。
- 
- 3. **输入 make install 以安装软件。**
  此步骤将库和可执行二进制文件复制到系统上的适当目录。

尽管这些步骤特定于 XMMS，但大多数其他包都遵循这些步骤——configure、make 和 install。configure shell 脚本猜测系统相关变量并创建包含构建和安装软件所需命令的 Makefile。

通常，你只需输入命令来构建软件，但必须在系统上安装软件开发工具。这意味着你在安装 Red Hat Linux 时必须安装 Software Development 包。要构建和运行 XMMS，你还必须安装 X Software Development 包，因为它是一个 X 应用程序。

要开始构建 XMMS，请输入以下命令运行 configure 脚本（输入此命令时你必须位于 xmms-1.2.7 目录中）：

```
./configure
```

configure 脚本开始运行并打印大量消息，因为它检查你系统的各种特性——从 C 编译器的存在到构建 XMMS 所需的各种库。最后，configure 脚本创建一个可用于构建软件的 Makefile。

如果 configure 脚本显示错误消息并失败，请查看 INSTALL 和 README 文件以寻找解决问题的线索。你可以通过命令行参数向 configure 脚本提供一些信息来绕过它。

configure 脚本完成后，通过输入 make 来构建软件。此命令运行 GNU make 实用程序，它读取 Makefile 并根据 Makefile 中指定的信息开始编译源文件。make 命令遍历所有源目录，编译

![](img/a7eec43a54473e95dc5ea333fecf1bd7_500_0.png)

![](img/a7eec43a54473e95dc5ea333fecf1bd7_500_1.png)

Book VI
Chapter 4
Managing Applications

源文件，并创建运行 XMMS 所需的可执行文件和库。你会看到大量消息滚动显示，因为每个文件都在被编译。这些消息显示了用于编译和链接文件的命令。

`make` 命令可能需要 10 到 15 分钟才能完成。`make` 完成后，你可以使用以下命令安装 XMMS 软件：

```
make install
```

此命令也运行 GNU `make`，但 `install` 参数指示 GNU `make` 执行来自 `Makefile` 的特定命令集。这些说明基本上遍历所有子目录并将各种文件复制到其最终位置。例如，二进制可执行文件 `xmms`、`gnomexmms`、`wmxmms` 和 `xmms-config` 被复制到 `/usr/bin` 目录。

现在你已经安装了 XMMS，可以尝试从 GNOME 或 KDE 桌面运行它，通过在终端窗口中输入 `xmms` 或选择 主菜单→声音和视频→音频播放器。XMMS 已随 Red Hat Linux 提供，但现在你应该获得从源文件构建的新版本 XMMS（区别在于新构建的版本可以在没有任何附加组件的情况下播放 MP3 文件）。从 XMMS 窗口中，按 L 获取加载文件对话框并选择要播放的 MP3 文件。你的 PC 必须具有声卡，并且声卡必须配置正确，XMMS 才能工作。图 4-1 显示了 XMMS 播放 MP3 音乐剪辑的典型视图。

图 4-1：
你可以使用从源文件构建的 XMMS 版本播放 MP3 音乐。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_501_0.png)

以下是下载、解包、构建和安装典型软件包的步骤概述：

- 1. 使用 Web 浏览器从匿名 FTP 站点或网站下载源代码，通常以 `.tar.gz` 文件的形式。
- 2. 使用 `tar zxvf filename` 命令解包文件。
- 3. 使用诸如 `cd software_dir` 之类的命令更改到软件解包到的新子目录。



4. 阅读任何 README 或 INSTALL 文件以了解构建和安装软件时必须遵循的特定说明。

5. 从一个软件包到另一个软件包，构建软件的细节可能会略有不同，但通常你输入以下命令来构建和安装软件：

```
./configure
make
make install
```

6. 阅读随软件提供的任何其他文档，以了解如何使用软件以及在使用前是否必须进一步配置软件。

## 安装 SRPMS

你可以直接从源文件安装源文件并构建各种 Red Hat Linux 应用程序。Red Hat 以 RPM 形式提供源代码文件，就像可执行二进制文件一样，这些源 RPM 文件通常称为 SRPMS（源 RPM 的缩写）。

要安装特定的源 RPM 并构建应用程序，请按以下步骤操作：

- 1. 通过输入 `mount /mnt/cdrom` 挂载 DVD，或等待 GNOME 桌面挂载 DVD。
- 2. 通常源 RPM 位于 SRPMS 目录中。通过输入以下命令切换到该目录：
  `cd /mnt/cdrom/SRPMS`
- 3. 使用 `rpm -i` 命令安装源 RPM 文件。例如，要安装 Web 服务器（httpd）源，输入
  `rpm -ivh httpd*.src.rpm`
  文件将被安装在 `/usr/src/redhat/SOURCES` 目录中。带有 `.spec` 扩展名的 spec 文件将被放置在 `/usr/src/redhat/SPECS` 目录中。spec 文件描述了软件，并包含用于构建和安装软件的信息。
- 4. 使用 spec 文件与 `rpmbuild` 命令构建软件。你可以通过使用 `rpmbuild` 命令的不同选项来执行从解包源文件到构建和安装二进制文件的不同任务。例如，要处理整个 spec 文件，输入：
  `rpmbuild -ba packagename.spec`
  这里 `packagename` 是 SRPM 的名称。此命令通常应构建软件并安装二进制文件。

## 使用更新代理更新 Red Hat Linux 应用程序

Red Hat Linux 附带一个名为 Red Hat Network 的服务，旨在使注册用户能够保持其 Red Hat Linux 系统和应用程序为最新。其理念是，你注册 Red Hat Network 并提供有关系统硬件以及当前安装在系统上的 RPM 的信息。完成此操作后，更新代理可以下载系统所需的任何新 RPM 文件并为你安装这些文件。

我简要介绍如何使用更新代理和 Red Hat Network 更新系统的概述。

## 注册 Red Hat Network

要充分利用 Red Hat Network 的功能，你必须注册 Red Hat Network 并提供有关 Red Hat Linux 系统的信息。要注册，请按以下步骤操作：

- 1. **确保你的 Internet 连接已开启；然后选择 主菜单→系统工具→Red Hat Network。**

  出现一个配置对话框，你可以从中配置一些选项（例如对下载的软件包做什么、跳过哪些软件包以及是否验证软件包的真实性）。通常你可以单击 OK 继续。你还会收到一个提示，询问是否要安装 Red Hat 的 GPG 密钥（用于验证软件包是否由 Red Hat 安全签名）。单击 Yes 安装密钥。
- 2. **Red Hat 更新代理运行并显示一条解释程序用途的消息；单击 Forward 继续。**

  当你第一次运行 Red Hat 更新代理时，它会将你注册到 Red Hat Network。它首先显示一份隐私声明，解释在注册期间将被收集并发送到 Red Hat 服务器的信息。这些信息包括系统上 RPM 文件的清单和系统硬件的清单。
- 3. **阅读隐私政策；如果要继续，请单击 Forward。**

  系统会提示你输入用户名和密码以在 Red Hat 建立新的用户账户。
- 4. **填写所需信息并单击 Forward 继续。**

  下一个屏幕要求你输入更多关于你自己的信息，包括你的姓名、地址和电话号码。
- 5. **再次填写所需信息，然后单击 Forward。**

Red Hat 更新代理显示有关系统的一些信息，并要求你为系统配置文件（有关系统的信息集合）提供一个名称。

- 6. **输入一个描述性名称然后单击 Forward。**
  Red Hat 更新代理显示一份 RPM 列表（软件包名称），这些 RPM 将包含在配置文件信息中。当更新代理检查更新的软件时，它会使用此列表。
- 7. **如果你不关心更新某些软件包，请取消选中这些名称；然后单击 Forward。**
  Red Hat 更新代理通知你它即将将你的系统信息发送到 Red Hat Network。
- 8. **单击 Forward 继续。**
  Red Hat 更新代理将你的信息（隐私声明中提到的信息）发送到 Red Hat Network。如果一切顺利，上传开始并显示已发送百分比的进度条。否则，你可能会收到服务器的消息，告知由于负载过高，Red Hat Network 的访问仅限于订阅客户。
- 9. **如果被拒绝访问，你必须等待一段时间后再尝试注册。**
  Red Hat 更新代理成功将系统配置文件上传到 Red Hat Network 后，最终窗口显示一条消息，提示你访问 rhn.redhat.com 登录并访问 Red Hat Network。该网站也是你可以购买 Red Hat Network 订阅的地方。
- 10. **单击 Finish 按钮完成注册过程。**

## 更新 Red Hat Linux 软件包

注册 Red Hat Network 后，你可以使用 Red Hat 更新代理更新 Red Hat Linux。Red Hat 为一台 PC 提供免费的 Red Hat Network 订阅，但超出部分需要付费。如果你想购买订阅，请访问 rhn.redhat.com，登录并按照说明操作。

要更新软件包，请按以下步骤操作：

- 1. **以 root 身份登录，并选择 主菜单→系统工具→Red Hat Network。**
  Red Hat 更新代理启动，并弹出一个对话框提示你将 Red Hat 的公钥安装到你的 GPG 密钥环中。（GPG 指 GNU Privacy Guard 或 GnuPG，一种用于使用 OpenPGP Internet 标准加密、解密和签名电子邮件和其他数据的程序。）Red Hat 的公钥 GPG 密钥用于验证 Red Hat 是否已安全签名更新代理下载的软件包。
- 2. **单击 Yes 按钮安装 Red Hat 的密钥。**
- 3. **Red Hat 更新代理显示带有欢迎消息的窗口后，单击 Forward 按钮继续。**
  更新代理从 Red Hat Network 检索所有可用软件包的列表。（这可能需要几分钟。）然后更新代理下载所有可用软件包的头文件。对于每次下载，进度条显示迄今为止下载的数据百分比。在慢速 Internet 连接上，头文件下载需要相当长的时间。
- 4. **Red Hat 更新代理下载头文件后，它会显示一份要跳过的软件包列表。你可以接受该列表并单击 Forward 按钮继续。**
  更新代理显示 Red Hat Network 可供更新的所有软件包的列表。
- 5. **滚动浏览列表并选择要下载的软件包更新；单击软件包名称左侧的框以选择它。**
  当你选择软件包时，更新代理显示迄今为止所选软件包的总大小。
- 6. **选择软件包后，单击 Forward 按钮继续下载。**
  更新代理然后检查任何软件包依赖关系并开始下载软件包。进度条显示下载状态。
- 7. **下载完成后，单击 Forward 按钮继续安装。**
- 8. **更新代理在安装每个软件包更新时显示进度条。安装完成后单击 Forward 按钮。**
  更新代理显示有关其成功安装的软件包的消息。
- 9. **单击 Finish 按钮退出 Red Hat 更新代理。**

注册 Red Hat Network 后，你可以使用 Red Hat 更新代理使 Red Hat Linux 保持最新。



### 第5章：管理设备和打印机

### 本章内容

- 了解设备驱动程序
- 管理可加载驱动模块
- 管理 USB 设备
- 管理打印队列

你用来操作计算机的一切都是设备。你用来打字和点击的键盘和鼠标、用来存储一切的硬盘、以及用来获取纸质副本的打印机——这些都是设备。猜猜看——你必须管理它们。听起来没那么难。只要加载设备驱动程序并（可能）对设备进行一些配置即可。如果了解一些设备驱动程序并练习使用 Red Hat Linux 提供的用于管理设备的工具，这种管理会更容易一些。在本章中，我提供了设备驱动程序的简要概述，并解释了如何管理驱动模块。由于打印机是你必须管理的常见设备类型，我还展示了如何管理打印队列。

### 了解设备驱动程序

Linux 内核将所有设备都视为文件，并像使用文件一样使用设备——打开它、向其写入数据、从中读取数据，完成时关闭它。这种将每个设备都视为文件的能力是通过使用设备驱动程序实现的。设备驱动程序是一种控制特定类型硬件的特殊程序。当内核向设备写入数据时，设备驱动程序会执行对该设备适当的任何操作。例如，当内核向软盘驱动器写入数据时，软盘设备驱动程序会将该数据写入软盘的物理介质。另一方面，如果内核向并行端口设备写入数据，并行端口驱动程序会将数据发送到连接到并行端口的打印机。

因此，设备驱动程序将设备特定的代码与内核的其余部分隔离开来，并使设备看起来像文件。任何应用程序都可以通过打开特定于该设备的<|message|> 文件来访问设备。图 5-1 说明了 Linux 设备驱动程序的概念。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_507_0.png)

图 5-1:
应用程序可以通过一个特殊文件访问设备，该文件反过来使用设备驱动程序。

### 设备文件

如图 5-1 所示，应用程序可以像文件一样访问设备。这些文件是称为设备文件的特殊文件，它们出现在 Red Hat Linux 文件系统的 /dev 目录中。

如果你使用 ls 命令查看 /dev 目录中的文件列表，你会看到数千个文件。这并不意味着你的系统有数千个设备。/dev 目录为所有可能的设备类型都有文件——这就是设备文件数量如此庞大的原因。

那么内核如何在应用程序打开特定设备文件时知道使用哪个设备驱动程序呢？答案在于两个称为主设备号和次设备号的数字。每个设备文件都通过这些数字映射到特定的设备驱动程序。

要查看主设备号和次设备号的示例，在终端窗口中输入以下命令：

```
ls -l /dev/hda
```

你应该会看到类似以下内容的输出行：

```
brw-rw---- 1 root disk 3, 0 Jul 23 14:50 /dev/hda
```

在这种情况下，主设备号和次设备号出现在日期之前。在此例中，主设备号为 3，次设备号为 0。内核使用主设备号为此设备文件选择设备驱动程序。

你实际上不需要了解太多关于设备文件和设备编号的知识，除了意识到它们的存在。

### 块设备

设备文件列表中的第一个字母也提供了重要线索。对于 /dev/hda 设备，第一个字母是 b，这表明 /dev/hda 是一个块设备——一种可以以块形式接受或提供数据（通常为 512 字节或 1KB）的设备。顺便说一下，/dev/hda 指的是系统上的第一个 IDE 硬盘（Windows 中的 C 驱动器）。硬盘、软盘驱动器和 CD-ROM 驱动器都是块设备的例子。

### 字符设备

如果设备文件列表中的第一个字母是 c，则该设备是字符设备——一种可以一次接收和发送一个字符（一个字节）数据的设备。例如，串行端口和并行端口都是字符设备。要查看字符设备的具体列表，在终端窗口中输入以下命令：

```
ls -l /dev/ttyS0
```

此设备的列表应类似于以下内容：

```
crw-rw--- 1 root uucp 4, 64 Jul 23 14:50 /dev/ttyS0
```

请注意，第一个字母是 c，因为 /dev/ttyS0——第一个串行端口——是字符设备。

### 网络设备

使系统能够与网络交互的网络设备——例如以太网和拨号点对点协议（PPP）连接——有些特殊，因为它们不需要对应设备的文file。相反，内核为设备使用一个特殊名称。例如，以太网设备命名为 eth0 表示第一个以太网卡，eth1 表示第二个，依此类推。PPP 连接命名为 ppp0、ppp1，依此类推。

由于网络设备未映射到设备文件，/dev 目录中没有对应这些设备的文file。

### 管理可加载驱动模块

要使用任何设备，Linux 内核必须包含驱动程序。如果驱动程序代码作为单体程序（以单个大文file形式）链接到内核中，那么添加新驱动程序意味着使用新驱动程序代码重建内核。重建内核意味着你必须使用新内核重新启动 PC 才能使用新的设备驱动程序。幸运的是，Linux 内核使用模块化设计，避免了重新启动的麻烦。Linux 设备驱动程序可以创建为模块形式，内核可以在无需重新启动 PC 的情况下加载和卸载这些模块。

驱动模块是称为可加载内核模块的更广泛软件模块类别的一种类型。其他类型的内核模块包括可以支持新类型文件系统的代码、网络协议的模块以及解释不同格式可执行文file的模块。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_509_0.png)

### 加载和卸载模块

你可以使用一组命令来管理可加载设备驱动模块。你必须以 root 身份登录才能使用其中一些命令。在表 5-1 中，我总结了一些常用的模块命令。

表 5-1 管理内核模块的命令

| 此命令 | 执行以下操作 |
|---|---|
| insmod | 将模块插入内核 |
| rmmod | 从内核中移除模块 |
| depmod | 确定模块之间的相互依赖关系 |
| ksyms | 显示符号列表以及定义该符号的模块名称 |
| lsmod | 列出所有当前已加载的模块 |
| modinfo | 显示有关内核模块的信息 |
| modprobe | 智能地插入或移除一个模块或一组模块（例如，如果模块 A 需要 B，则在要求加载 A 时 modprobe 会自动加载 B） |

如果你必须使用这些命令中的任何一个，请以 root 身份登录或在终端窗口中输入 su - 成为 root。

要查看当前已加载的模块，输入

```
lsmod
```

你应该会看到模块列表。例如，以下是我其中一台 PC 上的列表：

```
Module Size Used by Not tainted
nls_iso8859-1 3516 1 (autoclean)
nls_cp437 5148 1 (autoclean)
sd_mod 13516 2 (autoclean)
vfat 13036 1 (autoclean)
fat 38808 0 (autoclean) [vfat]
usb-storage      74560  1 [sd_mod usb-storage]
scsi_mod        107576  2 [sd_mod usb-storage]
ide-cd          35712  0 (autoclean)
cdrom           33728  0 (autoclean) [ide-cd]
parport_pc      19076  1 (autoclean)
lp              9060   0 (autoclean)
parport         37056  1 (autoclean) [parport_pc lp]
iptables_filter 2444   0 (autoclean) (unused)
ip_tables       15224  1 [iptables_filter]
autofs          13268  0 (autoclean) (unused)
orinoco_cs      5556   1
orinoco         39724  0 [orinoco_cs]
hermes          8100   0 [orinoco_cs orinoco]
ds              8680   1 [orinoco_cs]
yenta_socket    13664  1
pcmcia_core     57248  0 [orinoco_cs ds yenta_socket]
3c59x           30736  0
floppy          56892  0 (autoclean)
keybdev         2976   0 (unused)
mousedev        5556   1
hid             22276  0 (unused)
input           5888   0 [keybdev mousedev hid]
usb-uhci        26412  0 (unused)
usbcore         79136  1 [usb-storage hid usb-uhci]
ext3            73340  2
jbd             52148  2 [ext3]
```

正如你所期望的，模块列表取决于系统上安装的设备类型。

第一列按从后到前的顺序列出模块名称。因此，列表中的第一个模块是最后加载的模块。Size 列显示模块在 PC 内存中占用的字节数。其余列显示有关每个模块的其他信息，例如当前有多少应用程序正在使用该模块以及需要该模块的模块名称。

`lsmod` 显示的列表包括所有类型的 Linux 内核模块，而不仅仅是设备驱动程序。例如，最后两个模块——`jbd` 和 `ext3`——都是 EXT3 文件系统的一部分（Linux 的最新文件系统）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_510_0.png)

除了 `lsmod` 之外，一个常用的模块命令是 `modprobe`。每当你需要手动加载或移除一个或多个模块时，使用 `modprobe`。`modprobe` 最好的地方是你不必担心模块是否需要其他模块才能工作。`modprobe` 命令会自动加载模块所需的任何其他模块。在我的系统上，例如，我可以使用以下命令手动加载声卡驱动程序

```
modprobe sound-slot-0
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_511_0.png)

此命令会使 `modprobe` 加载使声音工作所需的一切。在我的其中一台系统上，`modprobe sound-slot-0` 命令按顺序加载 `soundcore`、`ac97_codec` 和 `i810_audio`。

你可以使用 `-r` 选项与 `modprobe` 一起卸载模块。例如，要移除声音模块，我使用以下命令：

```
modprobe -r sound-slot-0
```

此命令会移除 `modprobe sound-slot-0` 命令之前加载的所有模块。

## 使用 /etc/modules.conf 文件

`modprobe` 命令如何知道当我使用模块名 `sound-slot-0` 时应加载 `opl3sa2` 驱动模块？答案在 `/etc/modules.conf` 配置文件中。该文件包含一行，告诉 `modprobe` 在看到模块名 `sound-slot-0` 时应加载什么。

要查看 `/etc/modules.conf` 的内容，输入

```
cat /etc/modules.conf
```

在我的其中一台 Red Hat Linux PC 上，该文件包含以下行：

```
alias parport_lowlevel parport_pc
alias eth0 eepro100
alias usb-controller usb-uhci
alias sound-slot-0 opl3sa2
```

以关键字 `alias` 开头的每一行都为实际驱动模块定义了一个标准名称。例如，第二行将 `eepro100` 定义为别名 `eth0` 的实际驱动名称，后者代表第一块以太网卡。同样，第四行将 `opl3sa2` 定义为使用名称 `sound-slot-0` 时要加载的模块。

`modprobe` 命令会查阅 `/etc/modules.conf` 文件，将别名转换为驱动模块的真实名称，并执行其他任务，例如获取驱动模块的参数。例如，你可以插入以 `options` 关键字开头的行，为驱动程序可能需要的参数提供值。

例如，要将声卡的 interrupt request（IRQ）参数设为 5，我会在 `/etc/modules.conf` 文件中添加以下行：

```
options opl3sa2 irq=5
```

此行将 `opl3sa2` 模块中名为 `irq` 的参数值指定为 5。

如果你想知道模块接受的参数名称，请使用 `modinfo` 命令。例如，要查看 `opl3sa2` 驱动模块的信息，输入

```
modinfo opl3sa2
```

从输出结果中可以看出，`irq` 是中断请求参数的参数名。

不幸的是，`modinfo` 命令显示的信息可能有些晦涩。唯一的好处是，你可能只需使用图形化工具来配置设备即可，工具会负责将所需内容添加到 `/etc/modules.conf` 等配置文件中。

## 管理 USB 设备

Red Hat Linux 内置了对通用串行总线（USB）的支持——一种串行总线，正在逐渐取代 PC 的串行和并行端口以及键盘和鼠标端口的功能。如今，许多 PC 外设——例如鼠标、键盘、打印机、刻录机、扫描仪、调制解调器、数码相机、存储卡等——都设计为通过 USB 端口连接到 PC。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_512_0.png)

USB 1.1 版支持高达 12 Mbps 的数据传输速率——每秒 1200 万位或每秒 1.5 兆字节——相比之下，标准串行端口的传输速率为 115 Kbps 或 0.115 Mbps。你可以在单个 USB 总线上菊花链连接多达 127 个设备。总线还为设备供电，并且可以在 PC 运行期间连接或移除设备——这种功能通常称为热插拔或热交换。USB 2.0 版（或简称为 USB 2.0 或 USB2）将数据传输速率提高到惊人的 480 Mbps，略快于竞争的 IEEE 1394（FireWire）总线。如今许多设备，例如刻录机和扫描仪，都配备了高速 USB2 接口。如果你的 PC 只有较旧的 USB 1.1 端口，USB2 设备仍然可以工作，只是数据传输速率较低。Red Hat Linux 支持 USB 1.1 和 USB2 接口。

在 Red Hat Linux 中使用 USB 设备很简单。你可以将设备热插拔到 USB 端口，Linux 内核可以检测并加载适当的设备驱动程序，以便应用程序可以使用该设备。更精确地说，`kudzu` 硬件检测实用程序负责使 USB 设备可供应用程序访问所需的任务。对于 USB 大容量存储设备，例如 CD 驱动器或硬盘，`kudzu` 还可以将设备挂载到 Linux 文件系统上。有关使用 USB 大容量存储设备的示例，请参阅第二册第 5 章，其中我讨论了 Red Hat Linux 如何检测 USB CD 刻录机以及如何通过 USB 接口访问数码相机中的照片。

要在 Red Hat Linux 中使用 USB 打印机，只需将打印机连接到 USB 端口，打开电源，然后按照第一册第 3 章中的步骤为打印机配置本地连接队列。打印机应显示为类似 /dev/usb/lp0（由 kudzu 检测到的 USB 打印机）、/dev/usb/lp1（第二台 USB 打印机）等之类的设备名称。

在 Red Hat Linux 中使用 USB 扫描仪与使用 USB 打印机一样简单。只需将扫描仪插入 USB 端口，打开电源，然后你应该可以使用 xsane 访问它——这是一个扫描仪的图形前端，你可以通过选择 Main Menu→Graphics→Scanning 来启动。当然，USB 扫描仪的品牌和型号必须得到 xsane 的支持。要快速检查 kudzu 是否检测到你的 USB 扫描仪，请以 root 身份登录并在终端窗口中输入 sane-find-scanner。

即使 kudzu 没有自动挂载 USB 大容量存储设备以便轻松访问，你也可以手动挂载该设备。例如，考虑 USB 钥匙链存储设备。正如名称所示，这些是小型存储卡，可存储 32MB 到 1GB 之间的任何数据。你可以把它们挂在钥匙链上——实际上，你可以随身携带所有数据。以下是如何使用已格式化为在 Microsoft Windows 中使用的 USB 钥匙链存储设备的方法：

- **1. 将钥匙链存储设备插入 PC 的 USB 端口。**

有时设备可以直接插入端口，但对于某些设备，你必须将钥匙链设备连接到 USB 电缆，然后将电缆插入 USB 端口。

一些 USB 钥匙链设备侧面有一个小开关，用于控制钥匙链是否写保护。如果你计划向设备写入数据，请先确保它未被写保护或锁定。

- **2. 为存储设备创建一个挂载点。例如，我以 root 身份登录并创建以下目录：**

```
mkdir /mnt/key
```

- **3. 如果这是唯一插入的 USB 设备，则设备名为 /dev/sda1（USB 存储设备显示为 SCSI 设备）。使用以下命令挂载它：**

```
mount -o rw -t vfat /dev/sda1 /mnt/key
```

命令中的 -t vfat 部分指定钥匙链存储设备上的文件系统为 VFAT——支持长文件名的 Windows 文件系统。

现在你可以在 /mnt/key 目录访问钥匙链上的文件。要将文件保存到 USB 钥匙链存储设备，请使用以下形式的命令：

```
cp filename /mnt/key
```

其中 filename 是你要保存的文件的名称。

使用完设备后，使用以下命令卸载 USB 钥匙链：

```
umount /dev/sda1
```

就这样！

## 在 Red Hat Linux 中管理打印队列

PC 通常配备一个并行端口，通常用于将打印机连接到 PC。你可以使用 Red Hat 的图形打印机配置实用程序相当轻松地设置打印机，但你也必须学习如何管理打印队列。

### 排队和打印作业

排队是指在后台打印的能力。例如，当你在 Windows 中从文字处理器打印时，输出首先进入磁盘上的文件。然后，在你继续使用文字处理器的同时，后台进程会将该输出发送到打印机。Red Hat Linux 打印环境也支持排队。

打印作业是指使用单个打印命令打印的内容。打印环境通过将打印作业存储在 spool 目录中来排队打印作业。后台进程会定期将 spool 目录中的打印作业发送到打印机。

Red Hat Linux 使用通用 UNIX 打印系统（CUPS）作为其打印环境。CUPS 是一个基于 Internet 打印协议（IPP）的打印系统——一种使用 Internet 技术进行分布式打印的协议。IPP 采用客户端/服务器模型，客户端是应用程序，服务器是“打印机”——输出设备或打印服务提供商的抽象。IPP 支持分布式打印环境，客户端和打印机服务器通过 Internet 进行通信。你可以使用 IPP 客户端在 Internet 上的任何打印机上打印。客户端和打印机使用 HTTP 1.1 协议交换数据——

使用与 Web 服务器相同的协议。客户端应用程序使用 IPP 来查询打印机的功能、提交打印作业，以及查询或取消打印作业。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_515_0.png)

如果您已为连接到 Red Hat Linux 系统的打印机设置了 CUPS 打印队列（按照第一部分第 3 章中的说明操作），则可以从本地局域网上的 Windows XP 和 2000 系统在该打印机上打印。Windows 2000 和 XP 内置支持 IPP —— CUPS 使用的协议。要从 Windows XP 系统打印到 CUPS 打印队列，请在 XP 上添加网络打印机。在添加打印机向导中，选择“连接到 Internet 上的打印机或家庭或办公网络上的打印机”，然后输入 CUPS 打印队列的 URL。例如，对于 IP 地址为 192.168.0.8 的 Red Hat Linux 主机上名为 HPLaserJetRoom210 的 CUPS 打印队列，我输入以下 URL 作为打印队列：

```
http://192.168.0.8:631/printers/HPLaserJetRoom210
```

作为 Red Hat Linux 用户，您使用客户端程序 —— lp 或 lpr —— 通过 TCP/IP 网络连接将待打印文件发送到名为 cupsd 的打印调度程序。cupsd 调度程序随后将文件排队，根据其文件扩展名（如 .txt 或 .ps）进行处理，然后逐个发送到打印机。借助各种配置文件，cupsd 调度程序知道该怎么做，以确保文件 —— 无论是文本文件还是图像文件 —— 都能正确打印。

虽然您通常只在 PC 上连接一台打印机，但 CUPS 打印系统的优点之一是可以打印到网络上另一系统连接的打印机。打印到远程打印机的方式与打印到本地打印机相同：本地 lp 或 lpr 程序只需将文件发送到远程系统的 cupsd 调度程序。

## 使用 lp 命令打印

您可以使用 lp 或 lpr 命令打印文件。例如，要打印文件 /etc/inittab，请在终端窗口中输入以下内容：

```
lp /etc/inittab
```

lp 命令通过将文件和适当的控制信息发送到 cupsd 打印调度程序来排队打印作业。默认情况下，cupsd 打印调度程序接受待打印文件，将其保留在打印队列中，并将其转发到默认打印机（如果默认打印机连接到网络上的远程系统，则转发到另一系统）。默认打印机由 CUPS 配置文件 /etc/cups/cupsd.conf 中的 <DefaultPrinter queuename> 条目标识（其中 queuename 是打印队列的名称）。

## 使用 lpq 检查打印队列

您可以在简单 lp 命令上添加一些选项。如果定义了多个不同的打印队列，您可以使用 -d 选项指定打印作业的目的地。例如，要将打印作业发送到名为 HPLaserJetRoom210 的惠普 LaserJet 打印队列，您应输入以下命令（打印队列名称出现在 /etc/cups/printers.conf 文件中）：

```
lp -d HPLaserJetRoom210 testprint.ps
```

如果您错误地打印了大文件并希望在浪费太多纸张之前停止打印作业，可以使用 lpq 命令查看当前打印作业，然后取消该大打印作业。以下是我在向 HPLaserJetRoom210 打印队列提交文件后输入 lpq 时得到的典型打印作业列表：

```
HPLaserJetRoom210 is ready and printing
Rank Owner Job File(s) Total Size
active root 2 testprint.ps 15360 bytes
```

lpq 命令显示作业编号（2）和我正在打印的文件名称（testprint.ps）。

## 使用 cancel 取消打印作业

要从打印队列中删除作业，请使用 cancel 命令。例如，要删除打印作业 2，请输入以下命令：

```
cancel 2
```

您可以使用以下 lprm 命令获得相同结果：

```
lprm 2
```

如果您急于取消迄今为止提交的所有打印作业，请按如下方式使用 -a 作为 cancel 的参数：

```
cancel -a
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_516_0.png)

## 使用 lpstat 检查打印机状态

要查看打印作业的状态，请使用 lpstat 命令。以下是 lpstat 命令的典型输出：

```
lpstat
HPLaserJetRoom210-2 root 15360 Wed 25 Jan 2003 04:25:48 PM EST
```

## 控制打印队列

输出的第一字段显示队列名称，后面附加了作业编号（该编号标识打印作业）。您需要该作业编号来取消打印作业。

要查看连接到系统的打印机名称，请使用 `lpc status` 命令。在我的系统上，`lpc status` 命令显示如下：

```
lpc status
HPLaserJetRoom210:
    printer is on device 'parallel' speed -1
    queuing is enabled
    printing is enabled
    no entries
    daemon present
```

请注意，此打印机的排队和打印均已启用。最后一行告诉您 `cupsd` 守护进程（始终运行的服务器）正在运行并且可用于处理打印作业。

您可以使用 `accept` 和 `reject` 命令启用或禁用打印队列的排队。例如，要停止为 `HPLaserJetRoom210` 打印机排队进一步的打印作业，我输入

```
reject HPLaserJetRoom210
```

此命令禁用为此打印机排队作业。如果有人尝试使用 `lp` 命令发送打印作业，用户会收到如下错误消息：

```
lp: unable to print file: server-error-not-accepting-jobs
```

如果您希望允许排队打印作业，但希望启动或停止打印，请使用 `enable` 和 `disable` 命令。当您禁用打印时，用户可以提交打印作业，但直到您再次启用打印之前不会打印任何内容。例如，我用来禁用 `HPLaserJetRoom210` 打印机打印的命令如下：`disable HPLaserJetRoom210`

![](img/a7eec43a54473e95dc5ea333fecf1bd7_517_0.png)

如果您尝试打印，但打印机似乎没有输出，请使用 `lpc status` 命令检查打印机状态，并确保 `cupsd` 调度程序存在且排队和打印均已启用。要允许排队打印作业，请使用 `accept` 命令，要开始打印，请使用 `enable` 命令。

### 第 6 章：升级和定制内核

### 本章内容

- ✔ 使用 Red Hat 内核 RPM 升级
- ✔ 配置内核
- ✔ 构建新内核
- ✔ 构建和安装模块
- ✔ 安装内核并设置 GRUB

Linux 如此令人兴奋的一个原因是许多程序员不断改进它。例如，一些程序员编写驱动程序以添加对新硬件的支持，例如新的声卡或新的网络卡。所有这些创新都以 Linux 内核的新版本形式呈现给您。

虽然您不必在每次有新版本可用时都升级或修改 Linux 操作系统 —— 内核 —— 但有时您必须升级，仅仅因为新版本纠正了一些问题或更好地支持您的硬件。另一方面，如果较早的内核版本已包含您所需的一切，则无需急于升级。

有时即使没有修复或增强，您也可能想要重建内核。随附 DVD 上的 Linux 内核是通用的，并使用模块来支持所有类型的硬件。您可能希望构建一个新内核，该内核仅链接到您系统上安装的设备的驱动程序。特别是，如果您有 SCSI 硬盘，您可能希望创建一个支持您的 SCSI 适配器的内核。根据您的需要，您可能还希望更改一些内核配置选项，例如创建特定于您的处理器的内核（而不是通用的 Intel 386 处理器）。

在本章中，我将解释如何使用内核 RPM 升级内核，以及如何重建和安装新的 Linux 内核。

## 使用 Red Hat 内核 RPM 升级

Red Hat 以 RPM 文件的形式分发所有软件更新，包括内核的新版本。要下载和安装内核 RPM，请按照以下步骤操作：

- 1. **使用 Web 服务器从 Red Hat 的 FTP 服务器下载内核 RPM 文件（我在下一节中解释了详细信息）。**
- 如果您想重建内核，您必须下载与新内核版本对应的 `kernel-source` RPM。
- 2. **使用 `rpm -i` 命令安装 RPM。**
- 3. **通过运行 `/sbin/mkinitrd` 命令创建新的初始 RAM 磁盘。**
- 4. **重新配置 GRUB 以启动新内核。**
- 5. **通过重新启动系统来尝试新内核。**

我在接下来的几节中进一步描述这些步骤。

### 下载新的内核 RPM

Red Hat 在其 FTP 服务器或 www.redhat.com/download/mirror.html 上列出的镜像站点之一以 RPM —— 包 —— 的形式提供软件更新。更新按 Red Hat Linux 版本号组织在目录中。例如，Red Hat Linux 9 for Intel x86 系统的任何更新都位于 9/en/os/i386 目录中。使用 Web 浏览器（例如 Mozilla）访问 FTP 站点并下载该站点上可用的任何内核 RPM。

### 安装内核 RPM

要安装内核和模块，请按照以下步骤操作：

- 1. **以 root 身份登录。**
- 2. **使用 `cd` 命令将目录更改为 RPM 文件（即从 Red Hat FTP 服务器下载的文件）所在的位置。**
- 3. **输入以下命令以安装内核 RPM：**
  `rpm -ivh kernel*.rpm`

您只有在想要构建新内核时才需要安装 `kernel-source` RPM。



![](img/a7eec43a54473e95dc5ea333fecf1bd7_520_0.png)

当你安装一个新的内核 RPM 时，安装过程会创建一个新的初始 RAM 磁盘映像——内核可以将其复制到一块内存中并用作内存驻留磁盘的文件。该文件的文件名以 initrd 开头（initrd 是 initial RAM disk 的缩写），并且文件名中包含内核版本号。内核 RPM 安装还会将内核的描述添加到 GRUB 配置文件——/etc/grub.conf 中。例如，我安装新内核 RPM 后，一个典型的 GRUB 配置文件如下：

```
title Red Hat Linux (2.4.20-8)
root (hd0,2)
kernel /vmlinuz-2.4.20-8 ro root=LABEL=/
initrd /initrd-2.4.20-8.img
title Red Hat Linux (2.4.20-6)
root (hd0,2)
kernel /vmlinuz-2.4.20-6 ro root=LABEL=/
initrd /initrd-2.4.20-6.img
```

下次重新启动系统时，这两个内核将作为选项出现在 GRUB 启动屏幕中。从该屏幕中你可以选择要启动的内核。

## 试用新内核

安装新内核 RPM、创建初始 RAM 磁盘文件并重新配置 GRUB 后，就该试用新内核了。要重新启动系统，请以 root 身份登录并从 Linux 提示符输入以下命令：

```
reboot
```

你也可以从图形登录屏幕重新启动系统。在登录对话框的 Options 菜单中选择 Reboot。

当系统重新启动并显示 GRUB 屏幕时，按箭头键选择新内核的名称。

Red Hat Linux 启动后，你应该会看到通常的图形登录屏幕。以用户身份登录，打开一个终端窗口，并输入 uname -sr 命令查看版本号。响应应显示你的系统正在运行新版本的内核。

## 重新构建内核

重新构建内核是指为核心 Linux 操作系统创建新的二进制文件。该二进制文件是在 Red Hat Linux 启动时运行的文件。你可能会想知道为什么要重新构建内核。以下是几个原因：

- 最初安装 Linux 后，你可能希望创建一个仅包含系统上已安装硬件支持的新内核。特别是，如果你有 SCSI 适配器，你可能希望创建一个将 SCSI 驱动程序链接进去的内核。随附 DVD 中的内核将 SCSI 驱动程序作为启动时加载的外部模块包含在内。
- 如果你有一台只有实验性支持的硬件的系统，你必须重新构建内核以将该支持包含到操作系统中。
- 你可能希望重新编译内核并生成在特定 Pentium 处理器上运行良好的代码（而不是标准 Red Hat Linux 发行版中附带的通用 386 处理器代码）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_521_0.png)

切勿在没有先确保拥有紧急启动软盘的情况下重新构建并安装新内核。如果有紧急启动软盘，请使用 mkbootdisk 命令创建启动软盘。输入 man mkbootdisk 以了解该命令的语法。构建紧急启动软盘的确切命令行取决于内核版本号。例如，要为版本 2.4.20-8 创建启动软盘，请以 root 身份登录并在终端窗口中输入以下命令（在提示时必须插入一张空白软盘）：

```
mkbootdisk -device /dev/fd0 2.4.20-8
```

将 2.4.20-8 替换为你的 Linux 内核的版本号（输入 uname -r 命令查看版本号）。

要重新构建 Linux 内核，你需要内核源文件。内核源文件通常未安装。使用以下步骤在系统上安装内核源文件：

- 1. 以 root 身份登录并将 Red Hat Linux DVD-ROM 插入 DVD 驱动器。
- 2. 如果 DVD 驱动器未自动挂载，输入以下命令挂载 DVD 驱动器：
  `mount /mnt/cdrom`
  如果你使用的是 GNOME 或 KDE，DVD 会自动挂载，你无需手动执行此步骤。
- 3. 将目录更改为 DVD 上的 RedHat/RPMS 目录，并使用 rpm 命令安装内核源文件。输入以下命令：
  `cd /mnt/cdrom/RedHat/RPMS`
  `rpm -ivh kernel-source*`
  rpm 命令安装完内核源包后，源文件会出现在 /usr/src/linux-2.4 目录中。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_522_0.png)

如果在本书的 DVD 上找不到 `kernel-source` RPM，你必须从 www.redhat.com/download/mirror.html 上列出的镜像站点之一下载该文件。点击所列 FTP 站点旁边的 Distribution 链接，然后查看对应 Red Hat Linux 版本号的目录。例如，Red Hat Linux 9 的 RPM 文件应位于 `9/en/os/i386/RedHat/RPMS` 目录中。使用 Web 浏览器下载 `kernel-source` RPM 文件并按照之前的步骤安装它。

构建内核涉及以下阶段：

- 配置内核
- 构建内核
- 构建并安装模块（如果有）
- 安装内核并设置 GRUB

我将在接下来的几节中解释这些阶段，但在开始之前，你应该先了解将驱动程序链接进去与将驱动程序作为可加载模块构建之间的区别。

## 创建单体内核 vs. 模块化内核

Linux 中支持各种硬件设备所需的设备驱动程序有两种选择：

- **链接支持：** 你可以将系统上所有硬件的驱动程序链接到内核中。随着设备驱动程序代码被合并到内核中，内核的大小会增加。将所有必要代码链接进去的内核称为 *单体内核*，因为它是一个大文件。
- **使用模块：** 你可以以可加载模块的形式创建设备驱动程序。*模块* 是内核启动运行后可以加载的一段代码。模块的典型用途是在不必为每个新设备重新构建内核的情况下为设备添加支持。模块不一定是设备驱动程序；它们也可以为内核添加新功能。使用模块的内核称为 *模块化内核*。

你不必创建完全单体或完全模块化的内核。事实上，常见的做法是将一些支持直接链接到内核中，但将不常用的设备驱动程序以模块形式构建。对于 Red Hat 这样的公司，分发模块化内核是有意义的。Red Hat 提供一个通用内核，以及大量可以支持许多不同类型硬件的模块。然后 Red Hat 安装程序配置系统仅加载支持用户系统上已安装硬件所需的模块。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_523_0.png)

当你为硬件配置创建自定义内核时，你可能希望将所有必需的设备驱动程序链接到内核中。你可以控制这种单体内核的大小，因为你只链接系统上已安装硬件的设备驱动程序。

## 配置内核

重新构建内核的第一阶段是配置它。要配置内核，请以 root 身份登录。然后使用 cd 命令更改内核源目录，如下所示：

```
cd /usr/src/linux*
```

要配置内核，你必须指出要在 Linux 内核中包含哪些功能和设备驱动程序。从本质上讲，你使用自己想要的功能构建自己的 Linux 内核版本。

Red Hat Linux 提供了几种配置内核的方法：

- 输入 make menuconfig 通过类似于 Red Hat 安装程序使用的基于文本的界面输入内核配置参数。
- 输入 make xconfig 使用基于 X Window 系统的配置程序配置内核。你必须运行 X 才能使用此图形界面配置程序。
- 输入 make config 使用一个逐一提示每个配置选项的 shell 脚本。你可以从 Linux 命令提示符使用此配置程序。使用此选项时，你需要经历一个漫长的问答过程来指定配置参数。对于每个问题，用 y 回答以将支持链接到内核，用 m 回答以构建模块，用 n 回答以跳过该特定设备的支持。

make menuconfig、make xconfig 和 make config 命令达到相同的最终结果——每个命令都将你的选择存储在位于 /usr/src/linux* 目录中的名为 .config 的文本文件中。由于文件名以句点开头，当你单独使用 ls 命令列出目录时看不到它。相反，输入 ls -a 以在目录列表中看到 .config 文件。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_523_1.png)

内核配置步骤仅将你的选择记录在 .config 文件中。（事实上，.config 文件在你配置一次内核之前并不存在。）内核文件在你使用 make 命令编译内核之前不会改变。这意味着你可以多次进行内核配置选项。如果想使用默认设置重新开始，请在开始配置内核前输入以下命令：

```
make mrproper
```



## 运行内核配置工具

你可以使用任何配置工具——make xconfig、make menuconfig 或 make config——来配置内核，但最简单的方法是以 root 用户登录，并在终端窗口中输入以下命令：

```
make xconfig
```

此命令构建基于 X Window System 的配置工具并运行它。初始的 Linux 内核配置窗口显示一组按钮，每个按钮代表一个内核配置选项类别，如图 6-1 所示。

图 6-1：你可以通过此窗口中的按钮配置内核选项组。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_524_0.png)

通过窗口右下角分组的四个按钮，你可以执行诸如保存配置和退出等任务。

要更改配置选项类别，请单击相关按钮。例如，如果你单击左上角的“处理器类型和特性”按钮，配置程序会显示另一个窗口，其中包含你可以设置的所有选项。然后你可以在新窗口中设置特定选项。例如，图 6-2 显示了一个下拉菜单，你可以从中选择特定的处理器类型（本例中为 Pentium III/ Celeron）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_524_1.png)

注意窗口右侧边缘的帮助按钮。每当你对配置选项有疑问时，单击相应的帮助按钮即可查看该选项的帮助信息。图 6-3 显示了单击“处理器类型”选项旁边的帮助按钮后的结果。阅读完信息后单击“确定”关闭帮助窗口。

图 6-2：
从下拉菜单中选择处理器类型。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_525_0.png)

图 6-3：
xconfig 内核配置工具中提供上下文相关帮助。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_525_1.png)

你可以按照以下步骤为每个选项类别指定选项：

- 1. 在主窗口中（参见图 6-1），单击选项类别。

配置程序会显示另一个窗口，其中包含该类别的选项（参见图 6-2）。

- 2. 设置你想要的选项。单击适当的单选框（y 表示是和 n 表示否）来表示你的选择。如果需要某个选项的帮助，请单击该选项旁边的帮助按钮。
- 3. 完成该类别的选项后，单击 Main Menu 返回图 6-1 的窗口或单击 Next 进入下一个选项类别。

我将介绍一些重要且有趣的选项类别。章节标题与图 6-1 中按钮上的标签相匹配，因此你可以轻松找到感兴趣的章节。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_526_0.png)

在开始配置内核选项之前，最后提醒一下。许多内核选项相互依赖。例如，如果并行端口选项未设置为 Yes，则配置程序会将所有与并行端口设备相关的选项变灰。逻辑上进行配置步骤的最佳方式是从左上角的按钮——Code Maturity Level Options——开始，然后在每个后续窗口上单击 Next。这样，你始终按正确的顺序设置选项。

## 代码成熟度级别选项

非常第一个选项组只有一个项目——询问你是否要使用实验性设备驱动程序。如果想尝试一些实验性驱动程序，例如支持 IEEE 1394（FireWire）的驱动程序，则将此选项设置为 Yes。

## 可加载模块支持

此选项组（见图 6-4）询问你关于可加载模块的支持。你希望包含模块支持，因此将第一个选项设置为 Yes。下一个选项是关于在每个模块中包含版本信息。如果模块具有版本信息，则会检查模块与当前内核版本的兼容性。因为卸载不工作的模块很容易，我倾向于将此选项设置为 No。不过，你可以安全地接受默认值并按 Enter。第三个问题询问你是否希望内核能够加载所需的模块。你应该将此选项设置为 Yes。

图 6-4：
从此配置窗口启用可加载模块支持。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_526_1.png)

## 处理器类型和特性

此选项集（图 6-5）用于设置处理器类型和特定处理器相关特性的支持。此集合的第一个选项询问你系统处理器的类型。如果你回答 386，编译后的内核可以在任何其他处理器上运行（如 486 或任何类型的 Pentium）。但是，如果你为系统专门创建内核，请从单击处理器系列时出现的下拉列表中选择处理器类型。你也可以在此窗口中启用对称多处理（SMP）支持，但只有在系统主板上有两个或更多处理器时才应这样做。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_527_0.png)

图 6-5：
在此配置窗口中设置处理器类型和其他处理器相关特性。

## 通用设置

这是一组通用选项（图 6-6），涉及网络、PCI 总线、MCA 总线、并行端口以及高级电源管理（APM）BIOS 支持。你可以简单地接受这些选项的默认设置。如果你不理解某个选项的含义，请单击该选项旁边的帮助按钮获取帮助。

## 并行端口支持

如果你使用任何连接到 PC 并行端口的设备，如打印机或并行端口 Zip 驱动器，这些选项（图 6-7）很重要。将 Parallel port support 和 PC style hardware 选项设置为 Module，以便驱动程序作为模块构建。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_528_0.png)

图 6-6：
你可以在此配置窗口中设置许多通用特性。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_528_1.png)

图 6-7：
从此配置窗口指定并行端口支持的选项。

## 即插即用配置

这些选项（图 6-8）询问你是否要在内核中启用 Plug-and-Play（PnP）支持。如果启用 PnP 支持，内核会自动配置 PnP 设备（就像 Windows 一样）。接受这两个选项的默认设置 Yes。

图 6-8：
通过这些选项打开即插即用支持。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_529_0.png)

## 块设备

块设备（如磁盘驱动器）以块的形式传输数据（与键盘一次传输一个字符不同）。此选项集（如图 6-9 所示）涉及连接到 PC 并行端口的软盘和 IDE（Integrated Drive Electronics）设备以及其他块设备。

图 6-9：
从此配置窗口设置块设备的选项。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_529_1.png)

第一个选项询问你是否想要软盘驱动器支持。因为大多数 PC 都配备软盘驱动器，你的答案通常是 Yes。选择 Module for the Parallel Port IDE Device Support 选项，如果你有外部 CD-ROM 或磁盘设备通过 PC 的并行端口连接。

如果你在图 6-9 的选项列表中向下滚动，你会找到更多块设备选项。将 Loopback Device Support 选项设置为 Yes 或 Module 可让 Linux 内核在单个大文件中操作整个文件系统。如果你在刻录 CD 之前想检查 CD 映像，这很有用。

RAM Disk Support 选项允许内核使用系统内存的一部分作为能够存储文件系统的磁盘。通常，RAM 磁盘仅在系统启动期间起作用，此时硬盘可能尚未可用。RAM 磁盘是必不可少的，如果你在未将 SCSI 驱动程序编译到内核的情况下启动 SCSI 磁盘。

## 网络选项

此选项集（如图 6-10 所示）涉及网络。你如何设置这些选项取决于你希望如何在网络中使用 Red Hat Linux 系统。始终启用 TCP/IP Networking 选项，因为 X Window System 使用 TCP/IP 网络（即使你的 PC 未连接到任何网络）。

图 6-10：
从此配置窗口配置网络选项。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_530_0.png)

将 Network Packet Filtering（Replaces ipchains）选项设置为 Yes，如果你想将 Red Hat Linux 系统用作防火墙——控制信息在本地局域网（LAN）和互联网之间流动的中间系统。

## 电话支持

借助合适的硬件和软件，电话支持选项可让你使用 Red Hat Linux 系统通过互联网拨打电话（也称为 voiceover IP 或 VoIP）。如果你有电话卡，例如 Internet

PhoneJACK 或由 Quicknet Technologies, Inc. 制造的 Internet LineJACK。如果您没有 Quicknet 电话卡，可以安全地将这些选项设为 No。

## ATA/IDE/MFM/RLL support

当您配置操作系统时，您必须预期会遇到不少缩写——这里有四个缩写：ATA、IDE、MFM 和 RLL。所有这些都与硬盘或将磁盘驱动器连接到 PC 的接口有关。它们的意思如下：

- **ATA** stands for *AT Attachment* and refers to the PC-AT style interface used to connect hard drives and DVD/CD-ROM drives to the PC's motherboard.
- **IDE** stands for *Integrated Drive Electronics* and refers to the original PC hard drives that integrate the disk controller onto the hard drive itself. The IDE interface is more accurately described as *AT Attachment Packet Interface* or ATAPI. You typically see the terms IDE, ATA, and ATAPI used interchangeably.
- **MFM** stands for *Modified Frequency Modulation*, the way data was encoded on older hard drives. These hard drives can work over an IDE interface.
- **RLL** stands for *Run Length Limited*, an old technique for storing data on hard drive from the early days of the PC. RLL disks can work over an IDE interface.

您应将 ATA/IDE/MFM/RLL 支持保持设为 Yes。从此窗口按 Next 时，您会得到另一个配置窗口（Figure 6-11）with many more options involving IDE devices, such as hard drives and ATAPI CD-ROM and DVD-ROM drives.

The first option is for enhanced IDE support, which refers to full-featured IDE controllers that can control up to 10 IDE interfaces. Because each IDE interface can have a master and a slave device, Linux can access a total of up to 20 IDE devices (such as disks or DVD/CD-ROM drives). You should leave this option set to Yes.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_531_0.png)

The second button in Figure 6-11 is a comment that refers you to the file Documentation/ide.txt for help with IDE devices. To read these help files (these are all text files), type the following command to change the directory:

```
cd /usr/src/linux*/Documentation
```

Now you can browse the directory for text files relating to specific devices. You can also use GNOME or KDE file managers to browse the documentation.

Note that IDE/ATAPI FLOPPY refers to IDE floppy drives, such as Iomega Zip drive or Iomega Superdisk LS-120 drive. If you have a IDE ZIP drive, set this option to Module or Yes.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_532_0.png)

Figure 6-11:
Set options for IDE devices from this configuration window.

## SCSI support

SCSI stands for Small Computer Systems Interface — a type of interface through which you can connect multiple devices (such as hard drives and scanners) to the PC. This set of options (shown in Figure 6-12) has to do with SCSI devices. If your system has a SCSI adapter, start by setting the SCSI Support option to Yes. After that, you can set the options relating to the types of devices (disk, tape, CD-ROM) connected to the SCSI adapter. Finally, you must enable support for the specific SCSI adapter model on your system.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_532_1.png)

If your system has a SCSI adapter, always select y for all the needed SCSI options. In particular, select y for the SCSI low-level driver for your specific brand of SCSI adapter.

## IEEE 1394 (FireWire) support (Experimental)

IEEE 1394 is a high-speed serial bus for connecting peripherals to PCs. Apple calls this bus FireWire; Sony calls it i.Link. IEEE 1394 is similar to USB, but it can transfer data at rates up to 400Mbps, which is more than 30 times the data rate of the older USB version 1.1 (note that USB 2.0 is even faster; it can transfer data at rates of up to 480Mbps). Because of its high data-transfer rates, IEEE 1394 is ideal for connecting high-speed peripherals such as digital audio and video devices and external hard drives to the PC.

The Linux kernel includes experimental support for the IEEE 1394 bus. Currently, Linux supports IEEE 1394 chipsets that are compatible with Texas Instruments PCI/Lynx/PCI/Lynx2 and OHCI chipsets. If your PC has an IEEE 1394 adapter, you can build the necessary drivers through these options (as shown in Figure 6-13).

Figure 6-12:
Enable support for various SCSI devices from this window.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_533_0.png)

Figure 6-13:
Configure support for IEEE 1394 (FireWire) devices from this window.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_533_1.png)

![](img/a7eec43a54473e95dc5ea333fecf1bd7_534_0.png)

Because the IEEE 1394 drivers are experimental, you can set these options only if you have said Yes to experimental drivers in the code maturity level options.

To learn more about using IEEE 1394 peripherals in Linux, visit the Web site of the IEEE 1394 for Linux project at www.linux1394.org.

## I2O device support

Pronounced *eye-two-oh*, I2O refers to Intelligent Input/Output — a new device driver architecture independent of the operating system and the controlled device. The basic concept of I2O is to separate the part responsible for managing the device from the part that contains operating system-specific details (it's called the I2O Split Driver model). The two parts of an I2O driver are the OS Services Module (OSM), which works with the operating system, and the Hardware Device Module (HDM) that interfaces with the particular device the driver manages. The OSM and HDM communicate by passing messages to each other. To learn more about I2O, visit the Intelligent I/O.com Web site at www.intelligent-io.com. Linux comes with some I2O drivers for SCSI and PCI devices. You can configure these drivers from this category of options.

## Network device support

This category of options involves the drivers for network interface cards. It includes the configuration of network devices such as Ethernet, Token Ring, ARCnet, and AppleTalk network adapters. If you have an Ethernet card installed on your PC, remember to build the driver for your Ethernet card by selecting Yes or Module for that card.

You can also enable dial-up and wide area network (WAN) support by using SLIP and PPP through options in this category.

## ISDN subsystem

This set of options enables you to include support for ISDN (Integrated Services Digital Network) — a digital telephone line you can use to connect the Linux system to the Internet. These ISDN-related options include the configuration of specific ISDN adapters.

You should build the ISDN driver only if your PC has an ISDN card. If you anticipate adding an ISDN card and purchasing ISDN service from the phone company, you can build the driver as a module. Read the file `/usr/src/linux*/Documentation/isdn/README` for more information on how to set up and use the ISDN driver in Linux.

## Character devices

These options deal with configuring character devices, which include devices connected to the serial and parallel ports. These options also include configuration of multiport serial interface cards that enable you to connect multiple terminals or other devices to your Red Hat Linux system. Answer No if you don't have any such devices on your system.

This list of options includes the Parallel Printer Support option. If you plan to connect a printer to the parallel port, set this option to Yes.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_535_0.png)

A subcategory of the character device options refers to I2C support. I2C — pronounced eye-squared-see — is a protocol Philips has developed for communication over a pair of wires at rates between 10 and 100kHz. System Management Bus (SMBus) is a subset of the I2C protocol. Many modern motherboards have an SMBus meant for connecting devices such as EEPROM (electrically erasable programmable read-only memory) and chips for hardware monitoring. Linux supports the I2C and SMBus protocols. You need this support for Video for Linux. If you have any hardware sensors or video equipment that needs I2C support, set the I2C support option to m (for module) and answer m to the specific driver for your hardware. To learn more about the I2C, read the documentation in the `/usr/src/linux*/Documentation/i2c` directory. In particular, the `summary` file briefly describes the I2C and SMBus protocols.

Other subcategories of character devices include

- **Mice:** You can specify the type of mouse on your PC (what's important is how the mouse is connected to the PC, not the make and model of the mouse). You have choices such as bus mouse, PS/2 mouse, and specialized devices such as digitizer pad and touch screen.
- **Joysticks:** You can set the options for any joysticks or special game controllers (steering wheel, game pad, and so on) on your PC.
- **Watchdog cards:** You can enable support for special watchdog cards that can monitor the PC's status (including the temperature, for instance) and reboot the PC when necessary. This can be helpful if you want to have a networked PC automatically reboot after it hangs up for whatever reason.
- **Ftape or the floppy-tape device driver:** If you have a tape drive connected to your floppy controller, you can configure it through this category of options.
- **PCMCIA character devices:** These options are for configuring PC card modems and serial ports that are meant for laptop or notebook PCs.

## Multimedia devices

This category of options configures support for multimedia devices such as video cameras, television tuners, and FM radio cards. For more information

对于这些设备，请查阅 /usr/src/linux*/Documentation/video4linux 目录中的文档。

## 文件系统

通过此类别的选项（见图 6-14），您可以为特定类型的文件系统打开支持。Linux 内核可以支持的文件系统种类之多会令您惊讶。表 6-1 列出了 Linux 可以支持的一些文件系统。您通常会构建一个内核，支持核心 Linux 文件系统（ext2 和 ext3）、CD-ROM 文件系统（ISO 9660 和 Joliet）以及 DOS/Windows 文件系统（MSDOS、FAT 和 VFAT）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_536_0.png)

图 6-14：从此配置窗口打开特定文件系统的支持。

表 6-1 Linux 内核支持的一些文件系统

| 文件系统 | 描述 |
|---|---|
| Apple Macintosh | Macintosh HFS 文件系统（Linux 可以读取和写入 Macintosh 格式的软盘和硬盘）。 |
| Coda | 一种高级网络文件系统，与 NFS 类似，但更好地支持断开操作（例如笔记本电脑），并且具有更好的安全模型。 |
| Ext2 | 第二代扩展文件系统——Linux 当前的标准文件系统。 |
| Ext3 | 支持日志功能的 Ext2 文件系统——一种设施，可在崩溃后快速恢复磁盘。 |
| FAT | 指任何基于文件分配表（FAT）的文件系统（包括 MS-DOS 和 Windows 95 VFAT 文件系统）。 |
| HPFS | OS/2 HPFS 文件系统（Linux 只能读取 HPFS 文件）。 |
| ISO 9660 | CD-ROM 上使用的标准 ISO 9660 文件系统（这也被称为 High Sierra 文件系统，在某些 UNIX 工作站上称为 hsfs）。 |
| Joliet | Microsoft 对 ISO 9660 CD-ROM 文件系统的 Joliet 扩展，允许使用 Unicode 格式的长文件名。（Unicode 是新的 16 位字符代码，可以编码世界上几乎所有语言的字符。） |
| MSDOS | MS-DOS 文件系统。 |
| NFS | 用于在网络上共享其他系统上的文件和目录的网络文件系统。 |
| NTFS | NT 文件系统（NTFS）——Microsoft Windows NT 使用的文件系统（Linux 只能读取 NTFS 磁盘）。 |
| /proc | 一个虚拟文件系统，可通过它获取有关内核的信息。/proc 文件系统不存在于磁盘上；文件在访问时创建。 |
| ROM | 安装 Red Hat Linux 时在初始 RAM 磁盘（initrd）期间使用的非常小、只读的内存驻留文件系统。 |
| SMB | 使用服务器消息块（SMB）协议访问运行 Windows 95/98/NT/2000 的网络 PC 上的共享目录的文件系统。 |
| System V | SCO、Xenix 和 Coherent 变体 UNIX 在 Intel PC 上使用的文件系统。 |
| UDF | 用于某些 CD-ROM 和 DVD 的新文件系统。（例如，UDF 文件系统用于以数据包模式写入或由 DirectCD 等 UDF 工具写入的可重写 CD。） |
| UFS | BSD（伯克利软件发行版）变体 UNIX（例如 SunOS、FreeBSD、NetBSD 和 NeXTstep）使用的文件系统。 |
| VFAT | 具有长文件名的 Windows 95/98/NT/2000 文件系统。 |

## 声音

使用这组选项配置声卡支持。如果已安装声卡，请先对“声卡支持”选项回答 y 或 m。之后，您必须为 PC 中安装的声卡启用多个选项。您始终可以选择 m 以模块形式构建声音支持，需要时可加载。

## USB 支持

使用此类别的选项（图 6-15）配置通用串行总线（USB）的支持——一种内置于大多数新 PC 中的串行总线。USB 1.1 版本支持高达 12Mbps 的数据传输速率——每秒 1200 万位或每秒 1.5 兆字节——相比之下，标准串行端口（如 COM1）的传输速率为 115Kbps 或 0.115Mbps。您可以在 USB 总线上菊花链连接多达 127 个设备。总线还为设备供电，并且可以在 PC 运行期间连接或移除设备——这种功能通常称为热插拔。USB 2.0 版本（或简称为 USB 2.0 或 USB2）将数据传输速率提高到 480Mbps，略快于竞争的 IEEE 1394（FireWire）总线。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_538_0.png)

图 6-15
通过这些选项配置 USB 支持。

USB 可以取代 PC 的串行和并行端口的功能，以及键盘和鼠标端口的功能。如今，许多 PC 外设——例如鼠标、键盘、打印机、扫描仪、调制解调器、数码相机等——设计为通过 USB 端口连接到 PC。

如果您的 PC 具有 USB 端口，请将 USB 支持选项设置为 y 或 m。然后您必须根据 PC 拥有的 USB 接口类型——UHCI（Intel）或 OHCI（Compaq 等）——对 UHCI 或 OHCI 选项回答 m。要确定 USB 接口的类型，输入 lspci 并在输出中查找 USB 控制器的制造商和型号。如果控制器由 Intel 生产，请使用 UHCI 驱动程序。

对于 USB 2.0 支持，您可以将 EHCI HCD（即主机控制器设备）选项设置为 y 或 m。

在选择 UHCI 或 OHCI 接口支持后，您必须为系统上的特定 USB 设备构建驱动模块。有关 USB 设备的更多信息，请查阅 /usr/src/linux*/Documentation/usb 目录中的文档——尤其是 usb-help.txt 文件中的链接。

## 内核调试

这组选项使您能够使用 SysRq 键（相当于在键盘上按下 Alt+PrintScreen）以在系统崩溃后立即获取重要的状态信息。如果您是期望调试内核的 Linux 开发人员，此信息很有用。大多数用户将这些选项设置为 No（因为大多数用户运行的是稳定的内核版本，并且不期望修复内核错误）。

## 构建内核

配置内核选项后，单击主配置窗口中的“保存并退出”按钮（参见图 6-1）。现在您必须构建内核。这涉及输入三条命令来执行三个任务。

使用单行命令行启动接下来的三个任务（您可以在同一行输入多个用分号分隔的命令），以便您可以输入该行；然后按 Enter，并休息一下。这部分需要一段时间。根据您的系统，制作新内核可能需要几分钟到一个多小时。

在单行输入以下内容以启动该过程：

```
make dep; make clean; make zImage
```

make dep 命令确定哪些文件已更改以及必须重新编译的内容。make clean 命令删除旧的、无用的文件（如旧的内核副本）。最后，make zImage 在名为 zImage 的压缩文件中创建新内核并将其放置在某个目录中。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_539_0.png)

如果您将太多功能链接到内核中（通过对许多配置选项回答 Yes），内核文件大小可能太大，无法在 PC 启动时使用的 640K 内存中容纳。此 640K 限制的存在是因为 Intel x86 处理器以实模式启动，只能访问 1MB 内存，其中 640K 可供程序使用。此限制是旧 MS-DOS 时代的遗留问题，仅在 PC 启动时 Linux 内核初始加载时适用。在这种情况下，make 命令会显示如下错误消息：

```
System is too big. Try using bzImage or modules.
```

如果您收到“System is too big”错误，请输入 make bzImage 以使用可能适合内存限制的另一种类型的压缩内核。否则，请再次进行 make config 步骤，通过为这些配置问题选择 No 来消除不必要的特性。对于您确实需要或可能想尝试的其他功能，请选择 m 以创建模块。虽然内核大小在启动时有限制，但内核在启动过程完成后可以加载所需的任意多个模块。

在构建内核时，您会在屏幕上看到大量消息。全部完成后，/usr/src/linux*/arch/i386/boot 目录中会出现一个名为 zImage 的压缩文件形式的新的内核。

要使用新内核，您必须将内核复制到 /boot 目录下并使用特定名称，并编辑 /etc/grub.conf 文件以设置 GRUB——引导加载程序。但是，在继续进行内核安装之前，您必须构建和安装模块。

## 构建和安装模块

如果在内核配置期间选择了任何模块，您必须构建模块并安装它们。按以下步骤执行这些任务：

- 1. 输入以下命令以构建模块：
  ```
  cd /usr/src/linux*
  make modules
  ```
  目录中当前的一组模块以您系统正在运行的 Linux 内核版本命名。例如，如果您的系统运行内核版本 2.4.20-20.1.2013.nptl，则模块位于以下目录中：
  ```
  /lib/modules/2.4.20-20.1.2013.nptl
  ```
- 2. 按如下方式将模块目录移动到新位置：
  ```
  mv /lib/modules/2.4.20-20.1.2013.nptl
      /lib/modules/2.4.20-20.1.2013.nptl-old
  ```
- 3. 使用以下命令安装新模块：
  ```
  make modules_install
  ```

现在您可以安装内核并使其可供 GRUB 启动。

## 安装新内核并设置 GRUB

Red Hat Linux 使用 GRUB 从磁盘加载 Linux 内核。配置文件 /etc/grub.conf 列出了 GRUB 运行的内核二进制文件。你

可以通过输入以下命令来检查 GRUB 配置文件的内容：

```
cat /etc/grub.conf
```

当我在其中一台系统上尝试此命令时，我看到的内容如下：

```
# grub.conf generated by anaconda
#
# Note that you do not have to rerun grub after making changes to this file
# NOTICE: You have a /boot partition. This means that
# all kernel and initrd paths are relative to /boot/, eg.
# root (hd0,2)
# kernel /vmlinuz-version ro root=/dev/hda5
# initrd /initrd-version.img
#boot=/dev/hda
default=0
timeout=10
splashimage=(hd0,2)/grub/splash.xpm.gz
title Red Hat Linux (2.4.20-20.1.2013.nptl)
root (hd0,2)
kernel /vmlinuz-2.4.20-20.1.2013.nptl ro root=LABEL=/
initrd /initrd-2.4.20-20.1.2013.nptl.img
title Windows XP
rootnoverify (hd0,1)
chainloader +1
```

以下是 /etc/grub.conf 文件中各行的含义（以 # 开头的行是注释）：

- **default=0** — 指定第一个启动项为 GRUB 应启动的默认项。如果将其设置为 1，GRUB 将启动第二个启动项。
- **timeout=10** — 导致 GRUB 在等待 10 秒后自动启动默认项。如果文件中存在其他启动项，用户可以从 GRUB 显示的启动菜单中选择另一个。

- 以 `title Red Hat Linux (2.4.20-20.1.2013.nptl)` 开头的四行构成了第一个启动项——该项定义了 GRUB 可以启动的特定内核文件。你可以通过在配置文件中添加类似的段落来让 GRUB 启动另一个内核。以下是此启动项中各行的含义：
- `root (hd0,2)` — 将 `root` 设备设置为第一块硬盘的第三个分区。Red Hat Linux 就安装在此特定系统的该分区上。
- `kernel /vmlinuz-2.4.20-20.1.2013.nptl ro root=LABEL=/` — 标识 GRUB 加载的内核。在此例中，内核文件为 `vmlinuz-2.4.20-20.1.2013.nptl`，位于 `root` 设备中。在我的系统上，该分区挂载在 `/boot` 目录下。换句话说，GRUB 加载的内核文件为 `/boot/vmlinuz-2.4.20-20.1.2013.nptl`。

- `initrd /initrd-2.4.20-20.1.2013.nptl.img` 行指定了一个文件，该文件包含一个初始 RAM 磁盘（`initrd` 代表 initial RAM disk）映像，在磁盘可用之前充当文件系统。Linux 内核使用 RAM 磁盘——用作磁盘的内存块——来启动；然后它加载其他驱动模块并开始使用硬盘。

- 以 `title Windows XP` 开头的三行是第二个启动项，并引用了该系统上存在的 Windows XP 操作系统。标题行旁边的文本会出现在 GRUB 菜单中。

在具有 Windows 分区的系统上，GRUB 配置文件通常包含另一个段落，其中包含该分区上操作系统的详细信息（可能是 Windows XP 或 Windows 2000）。

要配置 GRUB 启动新的 Linux 内核（你刚刚构建的那个），请按照以下步骤操作：

1. **将新的内核二进制文件复制到 /boot 目录。**

新的压缩内核文件位于 `/usr/src/linux*/arch/i386/boot` 目录中。如果你输入了命令 `make zImage`，内核文件名是 `zImage`；如果你使用 `make bzImage` 命令构建了内核，文件名是 `bzImage`。我只是将该文件以相同名称复制到 `/boot` 目录：

```
cp /usr/src/linux*/arch/i386/boot/zImage /boot
```

如果内核文件名是 `bzImage`，请确保使用 `bzImage` 而不是 `zImage`。你可以使用任何其他文件名，只要你在步骤 3 中在 `/etc/grub.conf` 文件中引用内核时使用相同的名称即可。

2. **保存 /boot 目录中的旧 System.map 文件，并复制新的映射文件。**

我假设你在更改了一些配置选项后重新构建了内核版本 2.4.20-20.1.2013.nptl：

```
mv /boot/System.map-2.4.20-20.1.2013.nptl /boot/System.map-2.4.20-20.1.2013.nptl-old
cp /usr/src/linux*/System.map /boot/System.map-2.4.20-20.1.2013.nptl
cd /boot
ln -s System.map-2.4.20-20.1.2013.nptl System.map
```

3. **使用你喜欢的文本编辑器编辑 /etc/grub.conf 文件，在文件中的 timeout 行之后添加以下行：**

```
title Red Hat Linux (2.4.20-20.1.2013.nptl NEW)
root (hd0,2)
kernel /zImage ro root=LABEL=/
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_543_0.png)

在你的系统上，你应确保 `root` 行正确——不要使用 `(hd0,2)`，而应列出 Linux `root` 目录（`/`）所在的正确磁盘分区。此外，使用内核映像文件的正确文件名（例如，如果内核文件名为此，则为 `/bzImage`）。

请注意，我不再显示 `initrd` 行，因为我假设你不再使用模块化 SCSI 驱动程序，即使你的系统具有 SCSI 适配器。

4. 保存 `grub.conf` 文件并退出编辑器。

现在你可以重新启动系统并尝试新的内核。

## 重启系统

配置完 GRUB 后，你可以重新启动系统。在你仍以 `root` 身份登录时，输入以下命令重新启动系统：

```
reboot
```

当你看到 GRUB 屏幕时，选择你在 `/etc/grub.conf` 文件中为新内核指定的名称。

系统重新启动后，你应该会看到熟悉的图形登录屏幕。要证明你确实运行的是新内核，请以用户身份登录，打开一个终端窗口并输入 `uname -srv`。此命令会显示内核版本以及该内核构建的日期和时间。如果你升级了内核源代码，你应该会看到新内核的版本号。如果你只是为同一旧内核版本重新构建了内核，日期和时间应与你重新构建内核的时间相匹配。这就是系统正在运行新内核的证明。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_543_1.png)

如果系统挂起（似乎什么也没发生——屏幕上没有输出且没有磁盘活动），你可能在内核重建过程中跳过了一步。你可以关闭并打开 PC 电源以重新启动。这次，在 GRUB 屏幕上选择旧工作内核的名称。

如果你也无法启动较旧版本的 Red Hat Linux，请使用紧急启动盘（包含较早但可用的 Linux 版本）启动系统。然后你可以重复内核重建和安装过程，确保正确遵循所有步骤。

## 第七卷

## 安全

## 第五波

Rich Tennant 著

![](img/a7eec43a54473e95dc5ea333fecf1bd7_544_0.png)

> "客房服务？请派人上来补充迷你吧、整理房间并整理碎片化硬盘。"

## 一目了然的内容

- 第 1 章：了解网络和主机安全 ............................................519
- 第 2 章：保护主机 ............................................531
- 第 3 章：保护网络 ............................................551
- 第 4 章：执行安全审计 ............................................571

### 第 1 章：了解网络和主机安全

### 本章内容

- ✓ 建立安全策略和框架
- ✓ 了解主机安全问题
- ✓ 了解网络安全问题
- ✓ 理解计算机安全术语
- ✓ 跟上安全新闻和更新

在本章中，我解释了你为何应担心安全问题，然后给出如何把握安全问题的宏观视角。我解释了整体安全框架的概念，并解释了安全的两个关键方面——主机安全和网络安全。我以向你介绍计算机安全讨论中使用的术语结束本章。

### 为何要担心安全？

在当今的网络世界中，你必须担心你的 Red Hat Linux 系统的安全性。对于独立系统，或用于隔离局域网（LAN）的系统，你必须专注于保护系统免受用户侵害以及用户相互侵害。换句话说，你不希望用户修改或删除系统文件，无论是有意还是无意。此外，你也不希望用户破坏其他用户的文件。

如果你的 Red Hat Linux 系统连接到互联网，你必须保护系统免受互联网上的未经授权访问。这些入侵者——通常被称为黑客——通常冒充用户身份，窃取或破坏信息，甚至拒绝你访问自己的系统（这被称为拒绝服务或 DoS 攻击）。

就其本质而言，互联网连接使你的系统可被互联网上的任何其他系统访问。毕竟，互联网连接了全球大量网络。事实上，互联网服务的客户端/服务器架构，例如 HTTP（Web）和 FTP，依赖于互联网提供的开放网络访问。不幸的是，你的系统上运行的互联网服务的易于访问性也意味着网上的任何人都可以轻松访问你的系统。



如果您运营一台向他人提供信息的 Internet 主机，您当然希望每个人都能访问您系统的 Internet 服务，例如 FTP 和 Web 服务器。然而，这些服务器通常存在漏洞，黑客可能会利用这些漏洞对您的系统造成损害。您需要了解 Internet 服务的潜在安全风险——以及您可以采取的预防措施，以最大程度地降低有人利用您的 FTP 或 Web 服务器弱点进行攻击的风险。

您还希望保护公司的内部网络免受外部人员侵扰，即使您的目标是通过 Web 或 FTP 服务器向外部世界提供信息。您可以通过设置 Internet 防火墙——内部网络的受控访问点——并将 Web 和 FTP 服务器放置在防火墙外的主机上来保护内部网络。

## 建立安全框架

保护您的 Red Hat Linux 系统的第一步是制定安全策略——一套规定您允许用户（以及通过 Internet 访问的人员）在您的 Red Hat Linux 系统上执行的操作的准则。您建立的安全级别取决于您如何使用 Red Hat Linux 系统——以及如果有人未经授权访问您的系统会面临多大的风险。

如果您是某个组织中一个或多个 Red Hat Linux 系统的系统管理员，您可能希望在制定安全策略时让公司管理层以及用户参与其中。显然，您不能制定一个严苛到阻止所有访问的策略（那样会妨碍任何人有效使用系统）。另一方面，如果用户正在创建或使用对组织有价值的数据，您必须制定保护数据不被外部人员泄露的策略。换句话说，安全策略应在用户需求与保护系统的需求之间取得平衡。

对于独立的 Red Hat Linux 系统，或偶尔连接到 Internet 的家庭系统，安全策略可以只是一份列出您希望在系统上运行的 Internet 服务以及计划在系统上设置的<|message|>用户账户的清单。对于任何较大组织，您可能在连接到 Internet 的局域网（LAN）上有一个或多个 Red Hat Linux 系统——最好是通过防火墙连接（再次说明，防火墙是控制局域网与 Internet 之间 Internet 协议——IP——数据包流量的设备）。在这种情况下，最好从整个组织的角度系统地思考计算机安全。图 1-1 显示了组织范围计算机安全框架的关键要素。

图 1-1 中概述的安全框架始于基于业务需求和风险分析制定安全策略。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_548_0.png)

图 1-1：
起始于一个全面的计算机安全框架。

## 确定安全业务需求

业务需求确定了业务的安全需求——您需要保护的计算机资源和信息（包括适用法律所施加的任何要求，例如保护某些类型数据隐私的要求）。典型的安全需求可能包括以下项目：

- 允许授权用户访问信息
- 实施指定谁可以访问何种信息的业务规则
- 采用强大的用户身份验证系统
- 拒绝对数据进行恶意或破坏性操作
- 在数据跨网络移动时从端到端保护数据
- 实施适用法律所施加的所有安全和隐私要求

## 执行风险分析

风险分析就是识别和评估风险——可能损害您的 Red Hat Linux 系统的潜在事件。分析涉及确定以下内容并进行一些分析以确定处理风险的优先级：

- **威胁：** 您所要防范的对象
- **漏洞：** 可能被利用的弱点（这些就是风险）
- **概率：** 漏洞被利用的可能性
- **影响：** 利用特定漏洞所产生的影响
- **缓解：** 为减少漏洞应采取的措施

## 典型威胁

在进一步描述风险分析之前，这里有一些对您的 Red Hat Linux 系统的典型威胁：

- **拒绝服务：** 计算机和网络被占用，使得合法用户无法使用系统。对于企业而言，拒绝服务可能意味着收入损失。
- **未经授权的访问：** 未经授权的用户使用计算机和网络。未经授权的用户可以窃取信息或恶意破坏或销毁数据。一些企业可能仅因未经授权的用户获得系统访问权限这一事实而遭受负面宣传的伤害，即使没有任何数据受到明确损害。
- **向公众披露信息：** 未经授权地向公众发布信息。例如，密码文件的泄露使潜在攻击者能够推断出用于访问系统的用户名和密码组合。其他敏感信息的泄露，例如财务和医疗数据，可能对企业构成潜在责任。

## 典型漏洞

对您系统和网络的威胁来自于对组织资源——计算机和人员——中漏洞的利用。一些常见漏洞如下：

- 人的疏忽（泄露密码、丢失安全卡等）
- 内部网络连接（路由器、交换机）
- 互联点（网关——Internet 与内部网络之间的路由器和防火墙）
- 安全措施较松的第三方网络提供商（ISP、长途运营商）
- 操作系统安全漏洞（Internet 服务器中的潜在漏洞，例如与 `sendmail`、`named`、`bind` 等相关联的漏洞）
- 应用程序安全漏洞（特定应用程序中已知的漏洞）

## 风险分析的 1-2-3（概率和影响）

要执行风险分析，请为每个潜在漏洞的概率和影响分配数值。要制定可行的风险分析，请对每个漏洞或风险执行以下操作：

1. 为概率分配主观评级 Low、低、Medium、中、High、高。正如评级所建议的，Low 概率意味着漏洞被利用的可能性较小；High 概率意味着可能性较大。
2. 为影响分配类似评级。您认为的影响取决于您。如果漏洞的利用会对您的业务产生很大影响，请将其评为 High 影响。
3. 为三个级别分配数值——Low = 1，Medium = 2，High = 3——分别用于概率和影响。
4. 将概率乘以影响——您可以将该乘积视为风险等级。然后做出决定，为超过概率与影响乘积特定阈值的漏洞制定保护措施。例如，您可能选择处理所有概率乘以影响大于 6 的漏洞。

如果您希望以更细的梯度表征概率和影响，请选择 1 到 5（例如）而不是 1 到 3 的量表，并按照之前相同的步骤进行。

## 建立安全策略

以风险分析和您可能需要解决的任何业务需求（无论风险等级如何）为基础，您可以为组织制定安全策略。安全策略通常涉及以下领域：

- **身份验证：** 将使用何种方法确保用户是真实用户？谁可以访问系统？密码的最小长度和复杂度是多少？用户多久更改一次密码？用户在自动注销之前可以空闲多长时间？
- **授权：** 不同类别的用户可以在系统上执行什么操作？谁可以拥有 `root` 密码？



- **数据保护：** 必须保护哪些数据？谁有权访问数据？某些数据是否需要加密？
- **Internet 访问：** 来自局域网的用户访问互联网有哪些限制？用户可以访问哪些互联网服务（如 Web、Internet Relay Chat 等）？传入的电子邮件和附件是否会扫描病毒？是否有网络防火墙？是否使用虚拟专用网络（VPN）通过互联网连接私有网络？
- **互联网服务：** 每个 Linux 系统允许哪些互联网服务？是否有文件服务器？邮件服务器？Web 服务器？每种类型的服务器上运行哪些服务？用作桌面工作站的 Linux 系统上运行哪些服务（如有）？
- **安全审计：** 谁来测试安全性是否足够？安全性多久测试一次？在安全测试中发现问题时如何处理？
- **事件处理：** 处理任何计算机安全事件的程序是什么？必须通知谁？为了帮助调查事件，必须收集哪些信息？
- **责任：** 谁负责维护安全？谁监控日志文件和审计跟踪以寻找未经授权访问的迹象？谁维护安全策略数据库？

## 实现安全解决方案（缓解）

在分析风险——漏洞——并制定安全策略后，您必须选择缓解方法：如何防范特定漏洞。这就是您基于安全策略、业务需求和可用技术制定整体安全解决方案的地方——该解决方案包括以下内容：

- 服务（身份验证、访问控制、加密）
- 机制（用户名/密码、防火墙）
- 对象（硬件、软件）

## 管理安全

除了实施安全解决方案外，您还必须安装安全管理系统，该系统持续监控、检测并响应任何安全事件。

风险分析、安全策略、安全解决方案和安全管理相结合提供了整体安全框架。这样的框架有助于建立对安全问题的共同理解水平——以及安全解决方案设计和实施的共同基础。

## 保护 Red Hat Linux

在定义安全策略后，您可以根据策略继续保护系统。具体步骤取决于您想对系统做什么——它是服务器还是工作站，以及有多少用户必须访问系统。

要保护 Red Hat Linux 系统，您必须处理两大类安全问题：

- **主机安全问题** 与保护操作系统以及系统上的文件和目录有关
- **网络安全问题** 指的是通过网络连接进行的攻击威胁

### 了解主机安全问题

以下是解决主机安全的一些高层次指南（我在本迷你书的第 2 章中详细介绍了其中一些主题）：

- 安装 Red Hat Linux 时，仅选择系统所需的软件包组。不要安装不必要的软件。例如，如果系统用作工作站，则无需安装大多数服务器（Web 服务器、新闻服务器等）。
- 创建初始用户账户并确保所有密码足够强，以至于密码破解程序无法“猜测”它们。Red Hat Linux 包含强制执行强密码的工具。
- 设置文件所有权和权限以保护重要文件和目录。使用新的访问控制列表（ACL）来管理谁可以使用哪些文件和目录。
- 使用 GNU Privacy Guard（GnuPG）加密或解密包含敏感信息的文件，并对从 Red Hat 下载的文件进行身份验证。GnuPG 随 Red Hat Linux 提供，您可以使用 `gpg` 命令执行诸如加密或解密文件以及对文件进行数字签名等任务。
- 使用文件完整性检查工具，例如 Tripwire，来监控关键系统文件和目录的任何更改。
- 定期检查各种日志文件是否有任何入侵或入侵尝试的迹象。这些日志文件位于系统的 `/var/log` 目录中。
- Red Hat 发布安全更新后立即安装。 这些安全更新修复了 Red Hat Linux 中的已知漏洞。

### 了解网络安全问题

一旦将组织的内部网络连接到互联网，安全问题就会出现。即使只将一台计算机连接到互联网也是如此，但当整个内部网络向世界开放时，安全问题会更加紧迫。

如果您是一名经验丰富的系统管理员，您已经知道管理互联网存在所花费的成本并不是让公司管理层担忧的问题；他们主要关心的是安全。为了获得管理层对网站的支持，您必须制定一个计划来保护企业网络免受入侵者侵害。

您可能认为只需将外部服务器（如 Web 和 FTP 服务器）连接到互联网即可避免危及内部网络。然而，采用这种简单的方法并不明智。这就像因为可能发生事故而决定不驾驶汽车一样。Web 服务器与内部网络之间没有网络连接也会带来以下缺点：

- 您无法使用网络文件传输（如 FTP）将文档和数据从内部网络复制到 Web 服务器。
- 内部网络上的用户无法访问企业 Web 服务器。
- 内部网络上的用户无法访问互联网上的 Web 服务器。这种限制使得对组织中的用户来说宝贵的资源——Web——无法访问。

解决此问题的实用方法是在防火墙外设置互联网防火墙并将 Web 服务器放置在高度安全的服务器上。

除了使用防火墙之外，以下是您应采取的其他一些步骤来解决网络安全问题（我在本迷你书的第 3 章中进一步解释了这些内容）：

- 仅在系统上启用您需要的互联网服务。特别是，不要启用未正确配置的服务。
- 使用安全外壳（`ssh`）进行远程登录。不要使用“r”命令，例如 `rlogin` 和 `rsh`。
- 保护您希望在系统上运行的任何互联网服务，例如 FTP 或 TELNET。您可以使用 TCP wrapper 访问控制文件——`/etc/hosts.allow` 和 `/etc/hosts.deny`——来保护其中一些服务。
- 及时修复您选择运行的互联网服务的任何已知漏洞。通常您通过从 Red Hat 下载并安装最新的服务器 RPM 文件来完成此操作。

## 学习计算机安全术语

计算机书籍、杂志文章和计算机安全专家使用许多具有独特含义的术语。您需要了解这些术语才能理解有关计算机安全的讨论（并与安全供应商有效沟通）。表 1-1 描述了一些常用的计算机安全术语。

表 1-1 常用计算机安全术语
| 术语 | 描述 |
|---|---|
| Application gateway | 一个充当应用层协议网关的代理服务，例如 FTP、TELNET 和 HTTP。 |
| Authentication | 确认用户确实是其声称的人的过程。典型的身份验证方法是挑战-响应方法，其中用户输入用户名和秘密密码以确认其身份。 |
| Backdoor | 黑客放置在主机上以绕过安全功能的安全弱点。 |
| Bastion host | 一个高度安全的计算机，作为组织在互联网上的主要存在点。堡垒主机通常位于边界网络上，但双宿主机（一个网络接口连接到互联网，另一个连接到内部网络）也是堡垒主机。 |
| Buffer overflow | 程序中的安全缺陷，使黑客能够向该程序发送过量的数据并用发送的数据中的代码覆盖正在运行程序的部分。结果是黑客可以在系统上执行任意代码并可能以特权用户身份访问系统。Linux 内核的新 exec-shield 功能可防止缓冲区溢出。 |
| Certificate | 一个电子文档，用于标识实体（如个人、组织或计算机）并将公钥与该身份关联。证书包含证书持有人的姓名、序列号、到期日期、证书持有人的公钥副本以及证书颁发机构的数字签名，以便接收方可以验证证书的真实性。 |
| Certificate Authority (CA) | 一个验证身份并颁发证书的组织。 |
| Cracker | 一个入侵（或试图入侵）主机的人，通常出于恶意目的。 |
| Confidentiality of data | 一种状态，即只有您自己可以访问（通常通过加密实现）。 |
| Decryption | 将加密信息转换回其原始可理解形式的过程。 |



## 表 1-1（续）

| 术语 | 描述 |
|---|---|
| 服务拒绝 (DoS) | 一种攻击，使用了计算机和网络上的大量资源，导致合法用户无法访问和使用系统。 |
| 数字签名 | 消息发起者用其私钥加密的消息的单向 MD5 或 SHA-1 哈希值，用于验证消息的完整性并确保不可否认性。 |
| DMZ | 外围网络的另一个名称。（DMZ 最初代表非军事区，即分隔朝鲜和越南交战南北方的缓冲区。） |
| 双宿主主机 | 具有两个网络接口的计算机（把每个网络想成一个家庭）。 |
| 加密 | 将信息转换为除预期接收者之外任何人都无法理解的形式的过程。转换是通过密钥与信息之间的数学运算完成的。 |
| 防火墙 | 组织内部网络与互联网之间的受控访问网关。双宿主主机可以配置为防火墙。 |
| 哈希 | 当数学函数将消息转换为称为消息摘要（或哈希）的固定大小数值时得到的结果。例如，MD5 算法产生 128 位消息摘要；安全哈希算法-1（SHA-1）生成 160 位消息摘要。消息的哈希值用发送者的私钥加密以产生数字签名。 |
| 主机 | 配置为向网络上其他计算机提供服务的网络计算机。 |
| 完整性 | 对于接收到的数据，指与原始发送时相同（即在传输过程中未被更改）的状态。 |
| IPSec（IP 安全协议） | OSI 网络模型网络层的安全协议，旨在为 IP 数据包提供加密安全服务。IPSec 提供基于加密的身份验证、完整性、访问控制和保密性（访问 www.ietf.org/html.charters/ipsec-charter.html 查看与 IPSec 相关的 RFC 列表）。 |
| IP 欺骗 | 一种攻击，黑客弄清受信任主机的 IP 地址，然后发送看起来来自该受信任主机的包。攻击者可以发送包但无法看到响应。然而，攻击者可以预测包的序列，本质上发送命令为未来的入侵设置后门。 |
| 不可否认性 | 一种安全功能，防止数据发送者能够否认曾发送过该数据。 |
| 数据包 | 根据特定协议组装的字节集合，是网络上通信的基本单元。例如，在 TCP/IP 网络上，数据包可能被称为 *IP 数据包* 或 *TCP/IP 数据包*。 |
| 包过滤 | 根据数据包类型（按源和目标 IP 地址或端口指定）选择性地阻止数据包。 |
| 外围网络 | 互联网与受保护的内部网络之间的网络。外围网络（也称为 DMZ）是堡垒主机所在的位置。 |
| 端口扫描 | 发现系统上哪些端口是开放的（换句话说，哪些互联网服务已启用）的方法。通过逐个向端口发送连接请求来执行。此过程通常是进一步攻击的前奏。 |
| 代理服务器 | 堡垒主机上的服务器，使内部客户端能够访问外部服务器（并使外部客户端能够访问受保护网络内部的服务器）。有各种互联网服务的代理服务器，例如 FTP 和 HTTP。 |
| 公钥加密 | 一种加密方法，使用一对密钥——私钥和公钥——来加密和解密信息。用公钥加密的任何内容只能用相应的私钥解密，反之亦然。 |
| 公钥基础设施 (PKI) | 一组标准和服务，使公钥加密和证书在网络环境中使用成为可能。PKI 促进诸如签发、续订和撤销证书，以及生成和分发公钥和私钥对等任务。 |
| 筛选路由器 | 过滤数据包的互联网路由器。 |
| Setuid 程序 | 无论谁运行程序，都以所有者权限运行的程序。例如，如果 setuid 程序归 root 所有，则该程序无论谁启动它都具有 root 权限。黑客经常利用 setuid 程序中的漏洞来获得对系统的特权访问。 |
| 对称密钥加密 | 一种加密方法，其中使用相同的密钥来加密和解密信息。 |
| 威胁 | 一种事件或活动，故意或非故意，有可能对系统或网络造成损害。 |
| 特洛伊木马 | 一种伪装成良性程序的程序，实际上是用于攻击系统的后门。攻击者经常安装一组特洛伊木马程序，使攻击者能够自由地以 root 权限访问系统，同时向系统管理员隐藏这一事实。这类特洛伊木马程序的集合称为 rootkit。 |
| 病毒 | 一种自我复制的程序，通过附加到其他程序从一台计算机传播到另一台计算机。 |
| 漏洞 | 可能对系统或网络造成损害的缺陷或弱点。 |
| 蠕虫 | 一种自我复制的程序，通过网络将自身从一台计算机复制到另一台计算机。 |

*表 1-1（续）*

## 跟上安全新闻和更新

为跟上最新的安全警报，您可能希望每天访问以下一个或多个站点：

- CERT 协调中心，网址为 www.cert.org
- 计算机事件咨询能力 (CIAC)，网址为 www.ciac.org/ciac/
- 国家基础设施保护中心，网址为 www.nipc.gov

如果您能够访问互联网新闻组，您可以定期浏览以下内容：

- comp.security.announce — 一个经过审核的新闻组，包含 CERT 关于安全的公告。
- comp.security.unix — 一个新闻组，包含 UNIX 安全问题的讨论，包括与 Red Hat Linux 相关的项目。

如果您更喜欢通过电子邮件接收定期安全更新，您还可以注册（订阅）各种邮件列表：

- redhat-watch-list — 请按照 www.redhat.com/mailing-lists/ 中的说明订阅此邮件列表。
- linux-security — 请按照 www.redhat.com/mailing-lists/ 中的说明订阅此邮件列表。
- FOCUS-LINUX — 请填写 www.securityfocus.com/cgi-bin/subscribe.pl 中的表格以订阅此专注于 Linux 安全问题的邮件列表。
- Cert Advisory 邮件列表 — 请按照 www.cert.org/contact_cert/certmaillist.html 中的说明订阅此邮件列表。

最后，您应检查 Red Hat 网站 www.redhat.com/apps/support/errata/index.html，以获取可能修复 Red Hat Linux 任何已知安全问题的更新。

### 第 2 章：保护主机

### 本章内容

- ✓ 保护密码
- ✓ 保护文件和目录
- ✓ 使用 GnuPG 加密和签名文件
- ✓ 监控系统安全

Host 是您 Red Hat Linux 系统的专业术语——尤其是在您使用它在网络上提供服务时。但即使您单独考虑计算机时，该术语也有意义；它是其上运行的一切的主机——操作系统和所有应用程序。计算机安全的一个关键方面是保护主机。

在本章中，我将带您了解在保护 Red Hat Linux 主机时应遵循的几个关键步骤。这些步骤包括安装操作系统更新、保护密码、保护文件和目录、必要时使用加密以及监控系统的安全性。您可以通过检查日志文件中的任何可疑活动以及使用 Tripwire 工具查看是否有人篡改了系统上的重要文件来监控主机安全。

### 安装操作系统更新

Red Hat Linux 和相关应用程序更新以 RPM 文件形式提供。要手动下载和安装更新，请按照以下步骤操作：

- 1. 以 root 身份登录并为更新创建目录：
- 2. 使用 wget 命令从 Red Hat 的 FTP 站点下载更新。

```
mkdir /usr/local/updates
cd /usr/local/updates
```

例如，要下载 Red Hat Linux 版本 9 的 i386 版本更新，请输入

```
wget ftp://updates.redhat.com/9/en/os/i386/*.rpm
wget ftp://updates.redhat.com/9/en/os/noarch/*.rpm
```



- 3. **使用以下命令安装所有更新：**
  `rpm -F *`
- 4. **使用以下命令删除更新文件：**
  `rm -fr /usr/local/updates`

## 保护密码

历史上，UNIX 密码存储在 /etc/passwd 文件中，任何用户都可以读取。例如，root 用户在典型的旧式 /etc/passwd 文件中的条目如下所示：

```
root:t6Z7NWDK1K8Su:0:0:root:/root:/bin/bash
```

字段由冒号 (:) 分隔，第二字段包含加密形式的密码。为了检查密码是否有效，login 程序会加密用户输入的明文密码，并将其与 /etc/passwd 文件的内容进行比较。如果匹配，则允许用户登录。

密码破解程序的工作方式与 login 程序类似，只是这些程序一次从字典中选取一个词，加密该词，并将其与 /etc/passwd 文件中的加密密码进行比较以寻找匹配项。要破解密码，入侵者需要 /etc/passwd 文件。通常，破解者利用各种 Internet 服务器（如邮件和 FTP）的弱点来获取 /etc/passwd 文件的副本。

近年来，Red Hat Linux 中对密码的安全性进行了多项改进。其中包括影子密码和可插拔认证模块，并且在安装 Red Hat Linux 时可以轻松安装这些功能。在 Red Hat Linux 安装过程中，有一步涉及在身份验证配置屏幕中进行选择。如果接受默认选择——启用 MD5 密码和启用影子密码——您将自动在 Red Hat Linux 中启用更安全的密码。

### 影子密码

显然，将密码随意放置让任何人都能获取——即使它们是加密的——也是糟糕的安全做法。因此，Red Hat Linux 不再将密码存储在 /etc/passwd 文件中（任何用户都可以读取），而是将其存储在影子密码文件 /etc/shadow 中。只有超级用户（root）可以读取此文件。例如，以下是新式 /etc/passwd 文件中 root 的条目：

```
root:x:0:0:root:/root:/bin/bash
```

在这种情况下，请注意第二字段包含 x 而不是加密密码。x 是影子密码；实际的加密密码现在存储在 /etc/shadow 文件中，其中 root 的条目如下：

```
root:$1$AAAn/yNuESHbZupy9cGfoo1Bf0tS0:1107:0:99999:7:-1:-1:134540356
```

/etc/shadow 条目的格式使用冒号分隔字段，与 /etc/passwd 文件中的条目相似，但大多数字段的含义不同。第一个字段仍然是用户名，第二个字段是加密密码。

/etc/shadow 条目中的剩余字段控制密码何时过期。您无需解释或更改 /etc/shadow 文件中的这些条目。相反，使用 chage 命令来更改密码过期信息。首先，您可以使用 chage 命令配合 -l 选项来检查用户的密码过期信息，如下所示（在这种情况下，您必须以 root 身份登录）：

```
chage -l root
```

此命令显示过期信息，包括密码的有效时长以及可以更改密码的频率。

如果您希望确保用户每 90 天强制更改一次密码，可以使用 -M 选项设置密码保持有效的最大天数。例如，为了确保用户 naba 在 90 天内被提示更改密码，我以 root 身份登录并输入以下命令：

```
chage -M 90 naba
```

您可以对每个用户账户执行此操作，以确保所有密码在适当时过期，并且所有用户都必须选择新密码。

### 可插拔认证模块 (PAMs)

除了通过使用影子密码提高密码文件的安全性外，Red Hat Linux 还使用 RFC 1321 中描述的 MD5 消息摘要算法（www.faqs.org/rfcs/rfc1321.html 或 www.cis.ohio-state.edu/cgi-bin/rfc/rfc1321.html）改进了存储在 /etc/shadow 文件中的密码的实际加密方式。MD5 将任意长度的消息缩减为文档的 128 位消息摘要（或指纹），以便您可以使用私钥对其进行加密以进行数字签名。MD5 对于密码加密也很有效。

MD5 相对于旧式密码加密的另一个优势是，旧密码最多限制为八个字符；而新密码（使用 MD5 加密）可以长得多。即使 /etc/shadow 文件落入错误的人手中，更长的密码也更难猜测。

您可以通过 /etc/shadow 文件判断 MD5 加密是否生效；加密后的密码更长，并且都带有 $1$ 前缀，如以下示例条目的第二字段所示：

```
root:$1$AAAAn1/yNuEShBzUpy9CgfooIBf0fSO:1107:0:99999:7::1::134540356
```

一个名为可插拔认证模块（PAM）的附加程序模块执行实际的 MD5 加密。Red Hat Linux 的 PAM 提供了一种灵活的用户认证方法。通过设置 PAM 的配置文件，您可以在不实际修改验证用户身份的重要程序（如 login 和 passwd）的情况下即时更改认证方法。

Red Hat Linux 大量使用 PAM 功能。PAM 驻留在许多不同的模块中（稍后会详细介绍）；其配置文件位于系统的 /etc/pam.d 目录中。通过输入以下命令查看系统上此目录的内容：

```
ls /etc/pam.d
```

此目录中的每个配置文件都指定了特定实用程序的用户认证方式。例如，有用于 login、passwd 和 su 的文件。在我的系统上输入 cat /etc/pam.d/passwd 文件时，我看到的内容如下：

```
#%PAM-1.0
auth       required     pam_stack.so service=system-auth
account    required     pam_stack.so service=system-auth
password   required     pam_stack.so service=system-auth
```

这些行表示认证、账户管理和密码检查都应使用 pam_stack 模块（/lib/security/pam_stack.so）并使用参数 service=system-auth 来完成。本质上，pam_stack 模块引用了 /etc/pam.d 目录中的另一个配置文件。在这种情况下，配置文件是 /etc/pam.d/system-auth。以下是我的 Red Hat Linux PC 上 /etc/pam.d/system-auth 文件的内容：

```
#%PAM-1.0
# This file is auto-generated.
# User changes will be destroyed the next time authconfig is run.
auth required /lib/security/$ISA/pam_env.so
auth sufficient /lib/security/$ISA/pam_unix.so likeauth nullok
auth required /lib/security/$ISA/pam_deny.so
account required /lib/security/$ISA/pam_unix.so
password required /lib/security/$ISA/pam_cracklib.so retry=3 type=
password sufficient /lib/security/$ISA/pam_unix.so nullok use_authtok md5 shadow
password required /lib/security/$ISA/pam_deny.so
session required /lib/security/$ISA/pam_limits.so
session required /lib/security/$ISA/pam_unix.so
```

以下是配置文件中这些行的简要说明：

- 第一行 `auth` 加载 PAM 模块 `/lib/security/pam_env.so`。该模块可以设置或取消设置环境变量（`/lib/security/$ISA/pam_env.so` 中的 `$ISA` 指的是通常未定义的环境变量，因此 PAM 模块的有效路径名为 `/lib/security/pam_env.so`）。
- 第二行 `auth` 指定了一个认证模块，该模块使用 PAM 模块 `/lib/security/pam_unix.so` 并使用参数字符串 `likeauth nullok` 来检查用户身份。参数字符串中的选项含义如下：
  - `likeauth` — 无论模块用于设置新凭据还是认证现有用户名，都返回相同的值。
  - `nullok` — 允许空白密码。
- `/etc/pam.d/system-auth` 文件中的第三行 `auth` 如果 `pam_unix.so` 模块的认证不成功，则拒绝系统访问。
- `/etc/pam.d/system-auth` 文件中的 `account` 行检查用户账户是否未过期、用户是否允许在一天中的特定时间登录等。
- `/etc/pam.d/system-auth` 文件中的接下来两行 `password` 指定了密码的设置方式：
  - 第一行 password 使用 `/lib/security/pam_cracklib.so` 模块尝试破解新密码（模块名称中的 `cracklib` 即表示此含义）。



retry=3 部分表示用户最多可以尝试输入新密码三次。第二个密码行表示使用 MD5 加密将密码存储在 /etc/shadow 文件中。

当您完成 /etc/pam.d/passwd 配置文件的设置后，您的选择将在使用 passwd 命令更改密码时生效。以下是一个我尝试更改密码的示例（我的注释以斜体显示）：

```
passwd
Changing password for user naba.
Changing password for naba.
(current) UNIX password: I type my current password
New password: I type "xyzz"
BAD PASSWORD: it is too short
New password: I type "transport" as password
BAD PASSWORD: it is based on a dictionary word
New password: I type "naba12" as the new password
BAD PASSWORD: it is based on your username
passwd: Authentication token manipulation error
```

在这种情况下，passwd 程序正在使用 PAM 模块来验证我的身份（当我第一次输入当前密码时），并确保我尝试的每个新密码都足够强。最后，在我三次尝试都未能选择一个好的密码后，PAM 模块会中止 passwd 程序。

## 保护文件和目录

保护主机安全的一个重要方面是保护重要的系统文件——以及包含这些文件的目录。您可以通过文件所有权以及控制谁可以读取、写入或（对于可执行程序）执行文件的权限设置来保护文件。

默认的 Red Hat Linux 文件安全通过每个文件或目录的以下设置进行控制：

- 用户所有权
- 组所有权
- 所有者的读、写、执行权限
- 组的读、写、执行权限
- 其他人（所有其他人）的读、写、执行权限

### 查看所有权和权限

当您使用 ls -l 命令查看详细列表时，可以看到文件的这些设置。例如，输入以下命令以查看 /etc/inittab 文件的详细列表：

```
ls -l /etc/inittab
```

生成的列表应如下所示：

```
-rw-r--r-- 1 root root 1756 Aug 1 17:00 /etc/inittab
```

第一组字符描述了用户、组和其他人的文件权限。第三和第四个字段显示拥有此文件用户和组。在这种情况下，用户和组名相同：root。

### 更改文件所有权

您可以使用 chown 命令设置用户和组所有权。例如，如果文件 /dev/hda 应由用户 root 和组 disk 拥有，那么您将以 root 身份输入以下命令来设置此所有权：

```
chown root.disk /dev/hda
```

若要单独更改组所有权，请使用 chgrp 命令。例如，以下是如何将文件组所有权更改为名为 accounting 的组：

```
chgrp accounting ledger.out
```

### 更改文件权限

使用 chmod 命令设置文件权限。要有效使用 chmod，您必须学习如何指定权限设置。一种方法是按所示顺序（谁/操作/权限）从以下表中每个表中连接一个或多个字母，如表 2-1 所示：

表 2-1 文件权限代码

| 谁 | 操作 | 权限 |
|---|---|---|
| u 用户 | + 添加 | r 读取 |
| g 组 | - 删除 | w 写入 |
| o 其他 | = 分配 | x 执行 |
| a 所有 | s 设置用户 ID |  |

要让每个人对目录中的所有文件具有读写访问权限，请输入 `chmod a+rw *`。另一方面，要允许每个人执行特定文件，请输入 `chmod a+x filename`。

另一种指定权限设置的方法是使用三位数字序列。在详细列表中，用户、组和其他人的读、写、执行权限设置显示为序列

```
rwxrwxrwx
```

对于不允许的操作，用破折号代替字母。考虑 `rwxrwxrwx` 包含三个 `rwx` 字符串。现在分配值 r=4, w=2, x=1。要获得序列 `rwx` 的值，只需将 r、w 和 x 的值相加。因此，`rwx` = 7。使用此公式，您可以为任何权限设置分配三位数值。例如，如果用户可以读取和写入文件但其他人只能读取文件，则权限设置是 `rw-r--r--`（这就是列表中的显示方式），其值为 644。因此，如果您希望目录中的所有文件都可被每个人读取但只能由用户写入，请使用以下命令：

```
chmod 644 *
```

### 设置默认权限

当您（或程序）创建新文件时，文件会获得什么权限设置？答案在于所谓的 user file-creation mask，您可以使用 `umask` 命令查看和设置它。

输入 `umask`，它会打印出一个数字，显示当前的文件创建掩码。默认设置对于 `root` 用户和其他普通用户是不同的。对于 `root` 用户，掩码设置为 022，而普通用户的掩码为 002。要查看此文件创建掩码的效果并解释掩码的含义，请按照以下步骤操作：

1. **以 root 身份登录并输入以下命令：**
   `touch junkfile`
   这将创建一个名为 `junkfile` 且为空的文件。
2. **输入 ls -l junkfile 以查看该文件的权限。**
   您应该会看到类似以下的行：
   `-rw-r--r-- 1 root root 0 Aug 24 10:56 junkfile`
   通过将第一字段中（不包括第一个字母）的每个三字母权限转换为 0 到 7 之间的数字来解释权限设置的数值。对于每个存在的字母，

   第一个字母的值为 4，第二个字母为 2，第三个为 1。例如，r w - 转换为 4+2+0（因为第三个字母缺失）或 6。同样，r - - 为 4+0+0 = 4。因此权限字符串 r w r - r - 成为 644。
3. **从 666 中减去数值权限设置，得到的就是 umask 设置。**

   在这种情况下，666 - 644 给我们 umask 为 022。

   因此，umask 为 022 会导致默认权限设置为 666-022 = 644。当您将 644 用权限字符串重写时，它变为 r w r - r - -。

   要设置新的 umask，请键入 umask 后跟掩码的数值。您应按以下方式进行操作：

1. **确定您希望新文件具有什么权限设置。**
   例如，如果您希望新文件只能由所有者读取和写入，而其他人则不能，则权限设置如下所示：
   `r w - - - - - -`
   
2. **使用将第一个字段分配为 4、第二个为 2、第三个为 1 的转换方法将权限转换为数值。**
   因此，对于只能由其所有者读取和写入的文件，权限设置是 600。
   
3. **从 666 中减去所需的权限设置以获得掩码的值。**
   对于权限设置为 600，掩码则变为 666 - 600 = 066。
   
4. **使用 umask 命令设置文件创建掩码：**
   `umask 066`

![](img/a7eec43a54473e95dc5ea333fecf1bd7_566_0.png)

默认 umask 为 022 对系统安全有益，因为它转换为文件对所有者具有读写权限，对其他人具有读权限。底线是您不希望默认 umask 导致文件可被全世界写入。

### 检查 set user ID 权限

还有另一种权限设置可能成为安全隐患。此权限设置称为 set user ID（或简称为 setuid），适用于可执行文件。当启用 setuid 权限时，文件将在文件所有者的用户 ID 下执行。换句话说，如果可执行程序由 root 拥有并且设置了 setuid 权限，那么无论谁执行该程序，它都将作为 root 执行。这意味着该程序可以做更多的事情（例如，读取所有文件、创建新文件和删除文件），而普通用户程序则不能。另一个风险是，如果 setuid 程序文件存在某些安全漏洞，黑客可以通过此类程序造成比其他漏洞更大的损害。

您可以使用简单的 find 命令找到所有 setuid 程序：

```
find / -type f -perm +4000 -print
```

您应该会看到如下文件列表：

- /usr/bin/chage
- /usr/bin/gpasswd
- /usr/bin/chfn
- /usr/bin/chsh
- /usr/bin/newgrp
- /usr/bin/passwd
- /usr/bin/at
- /usr/bin/rcp
- /usr/bin/rlogin
- /usr/bin/rsh
- /usr/bin/sudo
- /usr/bin/crontab
- ... lines deleted ...

许多程序具有 setuid 权限，因为它们需要它，但请检查完整列表并确保没有奇怪的 setuid 程序（例如，用户主目录中的 setuid 程序）。

如果您想查看 ls 命令如何列出这些权限，请键入 ls -l /usr/bin/passwd，您应该会看到权限设置：

```
-r-s--x--x 1 root root 16128 Jun 5 23:03 /usr/bin/passwd
```

所有者权限设置中的 s（r-s）告诉您已设置 setuid 权限。

## 使用 exec-shield

缓冲区溢出是（如果您允许我这么说的话）许多 Linux 安全漏洞的根本原因。当缓冲区溢出发生时，黑客可以覆盖内存的数据存储区域，并使用旨在执行恶意

命令。但如果 Linux 内核拒绝执行任何数据区域中的指令呢？啪！——再也没有缓冲区溢出了！这正是最新 Linux 内核所做的：它通过使程序内存的许多部分（包括存储临时变量的栈）不可执行，来防止常见的缓冲区溢出类型漏洞。Linux 内核的这个特性称为 exec-shield。

最佳之处在于，使用 exec-shield 你不必修复存在缓冲区溢出问题的应用程序。你所要做的只是打开该功能。为了让过程更简单，Red Hat Linux 默认启用 exec-shield。

某些程序在启用 exec-shield 时可能无法正常工作。如果必须关闭 exec-shield，请以 root 身份登录并从终端窗口输入以下命令：

```
echo 0 > /proc/sys/kernel/exec-shield
```

该命令将 exec-shield 内核选项设置为 0。exec-shield 选项可以取三个值——0、1 和 2。将这些值视为四种不同的安全级别。表 2-2 总结了 exec-shield 四个值的含义。Red Hat Linux 默认将 exec-shield 设置为 1。

表 2-2 使用 Exec Shield 的四级安全

| exec-shield 的此值 | 其含义为 |
|---|---|
| 0 | exec-shield 始终被禁用。 |
| 1 | exec-shield 对使用最新版本 gcc 编译器编译的程序启用。 |
| 2 | exec-shield 始终启用。 |

![](img/a7eec43a54473e95dc5ea333fecf1bd7_568_0.png)

将 exec-shield 设置为默认值，输入：

```
echo 1 > /proc/sys/kernel/exec-shield
```

## 使用 GnuPG 加密和签名文件

Red Hat Linux 附带 GNU Privacy Guard（GnuPG 或简称为 GPG）加密和身份验证实用程序。使用 GPG，你可以创建公钥和私钥对，使用你的密钥加密文件，还可以对消息进行数字签名以验证它确实来自你。如果你向拥有你公钥的人发送数字签名消息，收件人可以验证确实是你签署了该消息。

## 理解公钥加密

公钥加密背后的基本思想是使用一对密钥——一个私钥，另一个公钥——它们相关但不能用来推断彼此。任何用私钥加密的内容只能用相应的公钥解密，反之亦然。公钥用于分发给其他人，而你将私钥保存在安全的地方。

你可以使用公钥加密与其他人安全通信；图 2-1 说明了基本思想。假设 Alice 想向 Bob 发送安全消息。他们各自生成公钥和私钥对，然后交换公钥。然后，当 Alice 想向 Bob 发送消息时，她只需使用 Bob 的公钥加密消息并发送给对方。现在消息免受窃听，因为只有 Bob 的私钥可以解密消息——而只有 Bob 拥有该密钥。当 Bob 收到消息时，他使用自己的私钥解密消息并阅读。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_569_0.png)

图 2-1：Bob 和 Alice 可以通过公钥加密安全地通信。

此时，你应该停下来思考并说“等等！” Bob 如何知道消息确实来自 Alice？如果有人使用 Bob 的公钥发送消息冒充 Alice 怎么办？这就是数字签名发挥作用的地方。

## 理解数字签名

数字或电子签名的目的与笔迹签名相同，但数字签名的方式完全不同。与笔迹签名不同，你的数字签名取决于你要签名的消息。创建数字签名的第一步是对消息应用数学函数并将其简化为固定大小的消息摘要（也称为哈希或指纹）。无论你的消息有多大，消息摘要始终约为 128 或 160 位，具体取决于哈希函数。

下一步是应用公钥加密。只需用你的私钥加密消息摘要，即可得到该消息的数字签名。通常，数字签名附加在消息末尾，瞧！——你就得到了一条电子签名消息。

数字签名有什么用？好吧，任何想要验证消息确实由你签名的人都会取你的公钥并解密数字签名。他们得到的是消息的消息摘要（加密的哈希）。然后他们对消息应用相同的哈希函数并将计算出的哈希与解密后的值进行比较。如果两者匹配，则说明没有人篡改过消息。因为你的公钥用于验证签名，所以消息必须是用只有你知道的私钥签名的。因此消息一定来自你！

在 Alice 向 Bob 发送私人消息的理论场景中，Alice 可以对她的消息进行数字签名，以确保 Bob 能判断出消息确实来自她。图 2-2 说明了数字签名与普通公钥加密的联合使用。

以下是 Alice 如何向 Bob 发送私人消息，同时确保 Bob 真正能判断出它来自她：

- 1. Alice 使用软件计算消息的消息摘要，然后使用她的私钥加密摘要。这就是她对该消息的数字签名。
- 2. Alice 加密消息（再次使用一些方便的软件和 *Bob 的公钥*。
- 3. 她将加密的消息和数字签名都发送给 Bob。
- 4. Bob 使用他的私钥解密消息。
- 5. Bob 使用 Alice 的公钥解密数字签名。这给他提供了消息摘要。

图 2-2：
Alice 可以对她的消息进行数字签名，以便 Bob 能判断出它确实来自她。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_571_0.png)

- 6. Bob 计算消息的消息摘要并将其与通过解密数字签名得到的结果进行比较。
- 7. 如果两个消息摘要匹配，Bob 就能确定消息确实来自 Alice。

## 使用 GPG

GPG 包含使用公钥加密和数字签名所需的工具。你使用的就是 gpg 命令。你可以在开始使用加密时逐步学习使用 GPG。我向你展示使用 GPG 时可能执行的某些典型任务。

## 生成密钥对

你必须做的第一件事是生成自己的私钥-公钥对。在终端窗口中输入以下命令以生成密钥对：

```
gpg --gen-key
```

如果这是你第一次使用 gpg，它会在你的主目录中创建 .gnupg 目录，并在该目录中创建一个名为 options 的文件。然后 gpg 会退出并显示一条消息，提示你再次运行 gpg。现在你可以重新运行该命令。生成密钥对的步骤如下：

- 1. **再次输入 gpg --gen-key 命令。**
- 你应该会看到类似这样的消息：
- 2. **按 Enter 选择默认值，因为它足够好。**
- 然后 GPG 会提示你输入密钥大小（位数）。
- 3. **再次按 Enter 接受默认值为 1024 位。**
- GPG 会询问密钥何时过期。默认是不过期。
- 4. **如果默认值是你想要的（为什么不呢？），按 Enter。**
- 5. **当 GPG 询问你是否真的希望密钥永不过期时，按 y 确认。**
- GPG 会提示你输入姓名，然后是电子邮件地址，最后是注释，以便将密钥对与你的姓名关联。
- 6. **输入每个请求的信息并按 Enter。**
- 7. **当 GPG 给你机会更改信息或按原样确认时，通过输入 o 然后按 Enter 来确认。**
- 接下来 GPG 会提示你输入将用于保护私钥的密码短语。
- 8. **输入一个包含小写字母、大写字母、数字和标点符号的长短语——越长越好——然后按 Enter。**
- 小心选择；选择一个你能轻松记住的密码短语。
- GPG 生成密钥。它可能会要求你在 PC 上执行一些操作，以便随机数生成器为密钥生成过程生成足够的随机数。

```
Please select what kind of key you want:
(1) DSA and ElGamal (default)
(2) DSA (sign only)
(5) RSA (sign only)
Your selection?
```

## 交换密钥

要与其他人通信，你必须将你的公钥交给他们。你还必须从可能向你发送消息的人（或可能签名文件且你想验证签名的人）那里获取公钥。GPG 将公钥保存在你的密钥环中。要列出密钥环中的密钥，输入

```
gpg --list-keys
```



发送你的公钥给他人或将其放置在网站上，你必须将密钥导出到文件。最好的方法是按照 GPG 文档所称的方式将密钥放入 ASCII 护甲格式，使用如下命令：

```
gpg --armor --export naba@comcast.net > nabakey.asc
```

该命令将我的公钥以 ASCII 护甲格式（基本上看起来像乱码）保存到名为 nabakey.asc 的文件中。当然，你应该将电子邮件地址替换为你自己的电子邮件地址（创建密钥时使用的地址），并将输出文件名改为其他名称。

导出公钥到文件后，你可以将其邮件发送给他人或放置在网站上供他人使用。

当你从他人导入密钥时，通常也会以 ASCII 护甲格式提供。例如，如果我有一个名为 redhatkey.asc 的文件，其中包含 Red Hat 的 GPG 公钥，我会使用以下命令将其导入我的密钥环：

```
gpg --import redhatkey.asc
```

使用 gpg --list-keys 验证密钥是否已在你的密钥环中。例如，我在系统上输入 gpg --list-keys 时看到的内容如下：

```
gpg: please see http://www.gnupg.org/faq.html for more information
/home/naba/.gnupg/pubring.gpg
pub 1024D/CF922215 2002-08-23 Naba Barkakati (Author) <naba@comcast.net>
sub 1024g/47FED643 2002-08-23
pub 1024D/0B42460E 1999-09-23 Red Hat, Inc <security@redhat.com>
sub 2048g/961630A2 1999-09-23
```

下一步是检查新密钥的指纹。我输入以下命令来获取 Red Hat 密钥的指纹：

```
gpg --fingerprint security@redhat.com
```

这会使 GPG 打印出指纹：

```
pub 1024D/0B42460E 1999-09-23 Red Hat, Inc <security@redhat.com>
Key fingerprint = CA20 8B86 2BD6 9DFC 65F6 ECC4 2191 B0CD B842 A60E
sub 2048g/961630A2 1999-09-23
```

此时，你应该与 Red Hat 的某人核实密钥指纹。对于 Red Hat 这样的公司，你可以从网页（www.redhat.com/solutions/security/news/publickey.html）核实指纹。如果认为密钥指纹是正确的，你可以对密钥进行签名并验证它。以下是用于签名密钥的命令：

```
gpg --sign-key security@redhat.com
```

GPG 会显示一条消息并提示你已执行的密钥验证级别：

```
gpg: Warning: using insecure memory!
gpg: please see http://www.gnupg.org/faq.html for more information

gpg: checking the trustdb
gpg: checking at depth 0 signed=0 ot=-/q/n/f/u/=0/0/0/0/1
pub 1024D/0B42460E created: 1999-09-23 expires: never trust: -/-
sub 2048g/961630A2 created: 1999-09-23 expires: never
(1). Red Hat, Inc <security@redhat.com>

pub 1024D/0B42460E created: 1999-09-23 expires: never trust: -/-
Fingerprint: CA20 8B86 2BD6 9DFC 65F6 ECC4 2191 B0CD B842 A60E

Red Hat, Inc <security@redhat.com>

How carefully have you verified the key you are about to sign actually belongs to the person named above? If you don't know what to answer, enter "0".

(0) I will not answer. (default)
(1) I have not checked at all.
(2) I have done casual checking.
(3) I have done very careful checking.

Your selection?
```

回答后按 Enter，GPG 会要求确认，然后提示你输入密码短语。之后 GPG 会对密钥进行签名。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_574_0.png)

由于密钥验证和签名是 GPG 中潜在的薄弱环节，请谨慎选择要签名的密钥。通过签名密钥，你基本上表示信任该密钥来自该个人或组织。

## 签名文件

如果你向某人发送文件并希望确保收件人知道文件未被篡改且确实是你发送的，签名文件会很有用。GPG 使签名文件变得非常容易。你可以使用以下命令压缩并签名名为 message 的文件：

```
gpg -o message.sig -s message
```

要验证签名，输入

```
gpg --verify message.sig
```

要恢复原始文档，只需输入

```
gpg -o message --decrypt message.sig
```

有时你并不关心保持消息的保密性，只是想签名以表明消息来自你。在这种情况下，你可以使用以下命令生成并附加一个明文签名：

```
gpg -o message.asc --clearsign message
```

该命令基本上将明文签名附加到文本消息中。下面是一个典型的明文签名块：

```
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v1.0.7 (GNU/Linux)

1D0BD0E93Y...
26A...
-----END PGP SIGNATURE-----
```

当消息附加了明文签名时，你可以使用以下命令用 GPG 验证签名：

```
gpg --verify message.asc
```

输出的最后一行应说明签名是好的。

## 加密和解密文档

要加密发给收件人的消息，你可以使用 --encrypt（或 -e）GPG 命令。以下是如果你有我的 GPG 公钥，如何为我加密消息的方法：

```
gpg -o message.gpg -e -r naba@comcast.net message
```

消息将使用我的公钥加密（不带签名，但你可以用 -s 命令添加签名）。当我收到 message.gpg 文件时，我必须使用我的私钥解密它。以下是我的使用命令：

```
gpg -o message --decrypt message.gpg
```

然后 GPG 提示我输入密码短语以解锁我的私钥，然后解密消息并将输出保存到名为 message 的文件中。如果你只是想加密文件且无需他人解密文件，你可以使用 GPG 执行所谓的对称加密。在这种情况下，你可以使用以下 GPG 命令提供密码短语来加密文件：

```
gpg -o secret.gpg -c somefile
```

GPG 会提示你输入密码短语并要求重复输入（以确保你没有输入错误）。然后 GPG 使用从密码短语生成的密钥加密文件。

要解密使用对称密钥加密的文件，输入

```
gpg -o myfile --decrypt secret.gpg
```

GPG 会提示你输入密码短语。如果输入正确的密码短语，GPG 会解密文件并将输出（在此示例中）保存到名为 myfile 的文件中。

## 监控系统安全

即使你已保护了系统，也必须定期监控日志文件以查找入侵迹象。你可能希望安装 Tripwire 软件来监控关键系统文件和目录的完整性。Red Hat Linux 不附带 Tripwire 包。要使用 Tripwire，首先必须从 www.tripwire.org/downloads/index.php 下载它。你应该下载源代码 tarball（源文件的压缩归档），然后构建 Tripwire。（第六卷第4章提供了有关如何从源文件构建软件包的更多信息。）在构建并安装 Tripwire 后，你可以将其配置为监控系统上指定系统文件和目录的任何更改。

你应定期检查日志文件。许多 Red Hat Linux 应用程序，包括一些服务器，使用 syslogd 的日志功能写入日志信息。在 Red Hat Linux 系统上，由 syslogd 写入的日志文件位于 /var/log 目录中。确保只有 root 用户可以读取和写入这些文件。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_576_0.png)

syslogd 配置文件是 /etc/syslog.conf。syslogd 的默认配置应生成必要的日志文件；然而，如果你想检查并理解配置文件，输入 man syslog.conf 获取更多信息。

你应常规监控以下日志文件：

- `/var/log/messages` 包含各种日志消息，从用户登录到由 TCP wrapper 启动的服务的消息。
- `/var/log/secure` 包含来自服务的报告，例如 `in.telnetd` 和 `in.ftpd`，这些服务由 `xinetd` 通过 TCP wrapper 启动。
- `/var/log/maillog` 包含来自 sendmail 的报告。
- `/var/log/xferlog` 包含所有 FTP 文件传输的日志。

第七卷
第2章
保护主机



Red Hat Linux 附带一个图形化日志文件查看实用程序。要使用此工具，请从 GNOME 面板中选择 主菜单→系统工具→系统日志。图 2-3 显示了系统日志实用程序。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_577_0.png)

图 2-3：
使用 Red Hat 系统日志实用程序查看日志文件。

系统日志实用程序使用简单。单击左侧窗口中的日志文件名，即可在右侧的滚动文本窗口中查看其内容。

由于许多潜在入侵者使用端口扫描工具尝试向系统上的知名端口建立 TCP/IP 连接，因此您应查找表明来自未知主机（以名称或 IP 地址表示）的尝试连接的消息。要进行此类检查，请单击左侧窗口中的安全日志，然后浏览右侧窗口中出现的日志消息。您会看到如下行：

```
Jun 22 19:30:37 dhcpc1 xinetd[1691]: START: telnet pid=15174 from=192.168.0.4
Jun 22 20:23:00 dhcpc1 xinetd[1691]: START: sgi_fam pid=15356 from=<no address>
```

这些行显示了连接的类型（telnet、sgi_fam 等）以及连接的源 IP 地址。如果您想使用文本编辑器浏览这些消息，可以在 /var/log/secure 文件中找到它们。

### 第三章：保护网络

### 本章内容

- 保护 Internet 服务
- 使用安全外壳（SSH）进行安全远程登录
- 设置简单的防火墙
- 在您的 Red Hat Linux 系统上启用数据包过滤

要保护您的 Red Hat Linux 系统，您必须同时关注主机安全和网络安全。这两种安全类型的区别有些任意，因为保护网络涉及在主机上修复与系统提供的 Internet 服务相关的问题。在本章中，我将解释如何保护 Internet 服务（主要是通过不提供不必要的服务），如何使用防火墙阻止不需要的网络数据包到达您的网络，以及如何使用安全外壳进行安全远程登录。

## 保护 Internet 服务

对于连接到 Internet 的 Red Hat Linux 系统（甚至是未连接到 Internet 的 TCP/IP 局域网上的系统），一个重大的威胁是有人可能利用许多 Internet 服务之一来获得对您系统的访问权限。每个服务——例如邮件、Web 或 FTP——都需要运行一个服务器程序，该程序响应通过 TCP/IP 网络到达的客户端请求。其中一些服务器程序存在弱点，可能允许外部人员登录到您的系统——也许是以 root 权限。幸运的是，Red Hat Linux 附带了一些设施，您可以使用它们使 Internet 服务更安全。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_578_0.png)

潜在入侵者可以采用端口扫描工具——一种尝试在端口上建立 TCP/IP 连接并寻找响应的程序——来检查哪些 Internet 服务器正在您的系统上运行。然后，为了获得对您系统的访问权限，入侵者可以利用一个或多个服务的任何已知弱点。

### 使用 chkconfig 禁用独立服务

要提供诸如 Web、邮件和 FTP 等 Internet 服务，您的 Red Hat Linux 系统必须运行侦听传入 TCP/IP 网络请求的服务器程序。其中一些服务器在系统启动时启动，并一直运行。我们称此类服务器为 *独立服务器*。Web 服务器和邮件服务器就是独立服务器的例子。其他服务器则由另一个名为 `xinetd` 的服务器按需启动。

您可以使用 `chkconfig` 命令打开或关闭独立服务器。以下是您应如何使用 `chkconfig` 停止不需要的服务的方法：

- 以 `root` 身份登录并输入 `chkconfig --list` 以查看设置为在运行级别 0 到 6 自动启动的所有服务（有关运行级别的更多信息，请参阅第六册第一章）。
- 运行级别 3 和 5 的服务最重要，因为您的 Red Hat Linux 系统通常处于运行级别 3（文本模式）或 5（图形登录）。输入 `runlevel` 查看当前运行级别。
- 决定您不需要哪些服务。您需要或不需要什么取决于您如何使用 Red Hat Linux 系统。例如，如果它只是一台个人工作站，您不必运行大多数服务。
- 要停止一项服务，请使用 `chkconfig` 命令的以下形式：
```
chkconfig --level 345 service_name off
```
其中 `service_name` 是您想要关闭的服务的名称。例如，要防止 `ypserv` 服务在运行级别 3、4 和 5 自动启动，请输入以下命令：
```
chkconfig --level 345 ypserv off
```

使用这种方法，您可以使用 `chkconfig` 停止所有不需要的服务在启动时启动。

要立即停止一项服务，请使用 `service` 命令，如下所示：

```
service service_name stop
```

其中 `service_name` 是要停止的服务的名称。例如，如果邮件服务器（`sendmail`）已在运行，您可以使用以下命令停止它：

```
service sendmail stop
```

### 配置 xinetd 服务器以禁用服务

除了诸如 Web 服务器（`httpd`）、邮件（`sendmail`）和域名服务器（`named`）等独立服务器外，您还必须单独配置另一台服务器。该服务器 `xinetd`（Internet 超级服务器），每当客户端通过网络发出请求时，就会启动大量其他 Internet 服务，例如 FTP、TELNET 等。`xinetd` 服务器包含一些安全功能，您可以使用它们禁用它可以按需启动的服务。

xinetd 服务器在启动时读取名为 /etc/xinetd.conf 的配置文件。该文件反过来引用存储在 /etc/xinetd.d 目录中的配置文件。/etc/xinetd.d 中的配置文件告诉 xinetd 侦听哪些端口以及为每个端口启动哪个服务器。输入 ls /etc/xinetd.d 以查看系统上 /etc/xinetd.d 目录中的文件列表。在我的系统上，ls /etc/xinetd.d 命令列出如下内容：

```
chargen      daytime-udp  imap   ktalk  rlogin  services  time
chargen-udp  echo         imaps  ntalk  rsh     sgi_fam   time-udp
cups-lpd     echo-udp     pop2   pop3s  rsync   talk
daytime     finger       pop3p  rexec  servers telnet
```

此列表显示了 xinetd 可以启动的所有服务。然而，服务的配置文件也可以通过在文件中包含 disable = yes 行来关闭服务。例如，以下是 telnet 文件的内容：

```
# default: on
# description: The telnet server serves telnet sessions;
# it uses unencrypted username/password pairs for
# authentication.
service telnet
{
    flags       = REUSE
    socket_type = stream
    wait        = no
    user        = root
    server      = /usr/sbin/in.telnetd
    log_on_failure += USERID
    disable     = yes
}
```

请注意配置文件中的最后一行——该行禁用了 TELNET 服务。

我不会解释 xinetd 配置文件的格式，除了重申您可以通过在两个大括号 {...} 之间的配置文件中添加以下行来关闭服务：

```
disable = yes
```

您也可以使用 chkconfig 命令打开或关闭由 xinetd 控制的服务。例如，要允许 TELNET 服务，请输入以下命令：

```
chkconfig telnet on
```

根据您使用系统的方式，您可能能够禁用许多服务。如果您不希望任何人远程登录或从您的系统下载文件，只需禁用 TELNET 和 FTP 服务即可。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_581_0.png)

在对 xinetd 配置文件进行任何更改后，您必须重新启动 xinetd 服务器；否则，更改不会生效。要重新启动 xinetd 服务器，请输入以下命令：

```
service xinetd restart
```

这会停止 xinetd 服务器然后重新启动它。重新启动后，它会读取配置文件，更改将生效。

xinetd 的另一个安全功能是它使用 TCP wrapper 启动各种服务。TCP wrapper 是一段提供 Internet 服务访问控制功能的代码，充当您消息的保护包。TCP wrapper 可以启动其他服务，例如 FTP 和 TELNET，但在启动服务之前，它会咨询 /etc/hosts.allow 文件，查看请求服务的主机是否被允许该服务。如果 /etc/hosts.allow 中没有关于该主机的内容，TCP wrapper 会检查 /etc/hosts.deny 文件，查看是否应拒绝该服务。如果两个文件都为空，TCP wrapper 会提供对所请求服务的访问。

以下是收紧 xinetd 配置为启动的服务访问的步骤：

1. 使用文本编辑器编辑 /etc/hosts.deny 文件，将以下行添加到该文件中：

```
ALL:ALL
```

此设置拒绝所有主机访问系统上的任何 Internet 服务。

2. 编辑 /etc/hosts.allow 文件并向其中添加可以访问系统上服务的用户主机的名称。

例如，要仅允许来自 192.168.1.0 网络的主机和本地主机（IP 地址 127.0.0.1）访问系统上的服务，请将以下行放在 /etc/hosts.allow 文件中：

```
ALL: 192.168.1.0/255.255.255.0 127.0.0.1
```

3. 如果您想允许特定远程主机访问特定的 Internet 服务，可以使用以下语法在 /etc/hosts.allow 中为该行使用：

```
server_program_name: hosts
```

这里 server_program_name 是服务器程序的名称（例如，TELNET 的 in.telnetd），hosts 是可以访问该服务的以逗号分隔的主机列表。您也可以将 hosts 写成

网络地址或整个域名，例如 `.mycompany.com`。例如，以下是如何为 `mycompany.com` 域中的所有系统授予 TELNET 访问权限：

```
in.telnetd: .mycompany.com
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_582_0.png)

编辑 `/etc/xinetd.d` 目录中的配置文件以关闭不需要的服务；使用 `/etc/hosts.deny` 和 `/etc/hosts.allow` 文件来控制允许在系统上运行的服务的访问。编辑完 `/etc/xinetd.d` 目录中的文件后，请记得输入 `service xinetd restart` 以重新启动 xinetd 服务器。

## 使用安全外壳（SSH）进行远程登录

Red Hat Linux 附带 *Open Secure Shell* (*OpenSSH*) 软件，这是一套程序，为 Berkeley r 命令提供了安全替代：`rlogin`（远程登录）、`rsh`（远程 shell）和 `rcp`（远程复制）。OpenSSH 使用公钥密码学对用户进行身份验证并加密两个主机之间的通信，因此用户可以安全地从远程系统登录并安全地复制文件。

在本节中，我简要描述如何在 Red Hat Linux 中使用 OpenSSH 软件。要了解有关 OpenSSH 的更多信息并阅读其最新新闻，请访问 www.openssh.com 或 www.openssh.org。

OpenSSH 软件在 Red Hat Linux 安装期间安装。表 3-1 列出了 OpenSSH 软件的主要组件。

**表 3-1 OpenSSH 软件的组件**

| 组件 | 描述 |
|---|---|
| `/usr/sbin/sshd` | 这是 Secure Shell 守护进程，如果希望远程系统的用户使用 `ssh` 客户端安全登录，则必须在主机上运行。当来自 `ssh` 客户端的连接到达时，`sshd` 使用公钥密码学进行身份验证并与 `ssh` 客户端建立加密通信链路。 |
| `/usr/bin/ssh` | 这是 Secure Shell 客户端，用户可以运行它以登录正在运行 `sshd` 的主机。用户还可以使用 `ssh` 在另一台主机上执行命令。 |
| `/usr/bin/slogin` | `/usr/bin/ssh` 的符号链接。 |
| `/usr/bin/scp` | 安全复制程序，其工作原理类似于 `rcp`，但更安全。`scp` 程序使用 `ssh` 进行数据传输，并提供与 `ssh` 相同的身份验证和安全性。 |

**表 3-1（续）**

| 组件 | 描述 |
|---|---|
| /usr/bin/ssh-keygen | 您使用此程序生成 OpenSSH 中使用的公钥密码术所需的公钥和私钥对。ssh-keygen 程序可以为 RSA 和 DSA（数字签名算法）身份验证生成密钥对。 |
| /etc/ssh/sshd_config | 此 sshd 服务器的配置文件指定了 sshd 的许多参数——包括要监听的端口、要使用的协议（SSH 协议有两个版本，SSH1 和 SSH2，均受 OpenSSH 支持）以及其他文件的位置。 |
| /etc/ssh/ssh_config | 这是 ssh 客户端的配置文件。每个用户还可以在用户主目录的 .ssh 子目录中拥有一个名为 config 的 ssh 配置文件。 |

OpenSSH 使用公钥加密，其中发送方和接收方各有一对密钥——公钥和私钥。公钥可以自由分发，每个方都知道对方的公钥。发送方使用接收方的公钥加密数据。只有接收方的私钥才能解密数据。

要使用 OpenSSH，请执行以下两项操作：

- 如果您希望在主机上支持基于 SSH 的远程登录，请在系统上启动 sshd 服务器。输入 `ps ax | grep sshd` 查看服务器是否已在运行。如果没有，请以 root 身份登录，并在 shell 提示符下输入以下命令以确保 sshd 服务器在系统重启时启动：`chkconfig --level 35 sshd on` 要立即启动 sshd 服务器，请输入以下命令：`service sshd start`
- 使用以下命令生成主机密钥：`ssh-keygen -d -f /etc/ssh/ssh_host_key -N ''`

-d 标志会导致 ssh-keygen 程序生成 DSA 密钥，SSH2 协议使用该密钥。如果您看到一条消息说文件 /etc/ssh/ssh_host_key 已存在，这意味着密钥对是在 Red Hat Linux 安装期间生成的。然后您可以使用现有文件而无需重新生成密钥。

想要使用 ssh 登录的用户还必须生成公钥和私钥对。例如，以下是我所做的事情，以便我可以使用 SSH 从另一台系统登录到我的 Red Hat Linux 系统：

- 1. 我输入以下命令为 SSH2 生成 DSA 密钥：
  `ssh-keygen -d`
  系统会提示我输入密码短语，最后一条消息告知我我的公钥已保存到 `/home/naba/.ssh/id_dsa.pub`
- 2. 我将我的公钥——`/home/naba/.ssh/id_dsa.pub` 文件——复制到远程系统并将其保存为 `~/.ssh/authorized_keys2` 文件（这指的是另一个系统 `.ssh` 子目录中的 `authorized_keys` 文件，假设远程系统也是另一台 Red Hat Linux 系统）。请注意，`authorized_keys2` 文件名中的 2 指的是 SSH2 协议
- 3. 要登录到我的 Red Hat Linux 系统（主机名为 `lnbp200`）上的帐户，我在远程系统上输入以下命令：
  `ssh lnbp200 -l naba`
- 4. 在 `lnbp200` 主机上提示输入密码时，我输入密码。我也可以使用以下等效命令登录此帐户：
  `ssh naba@lnbp200`

如果我只是想从 lnbp200 系统安全地复制一个文件，我可以这样使用 scp：

```
scp lnbp200:/etc/ssh/ssh_config .
```

此命令将 /etc/ssh/ssh_config 文件从 lnbp200 主机安全地复制到我输入命令的系统。

## 设置简单防火墙

Internet 防火墙是内部网络与 Internet 之间的中介。防火墙控制对受保护内部网络的访问。

如果您将内部网络直接连接到 Internet，您必须确保内部网络上的每个系统都得到适当保护——这几乎是不可能的，因为只需要一个粗心的用户就会使整个内部网络变得脆弱。防火墙是连接到 Internet 的单一接入点：您可以将所有精力集中在使该防火墙系统成为未经授权外部用户的强大屏障上。

为了有用，防火墙应具有以下一般特征：

- 它必须控制 Internet 与内部网络之间的数据包流。
- 它不得提供动态路由，因为动态路由表容易受到路由欺骗的影响——入侵者使用虚假路由。相反，防火墙应使用静态路由表（您可以在 Red Hat Linux 系统上使用 route 命令设置）。
- 它不得允许任何外部用户以 root 身份登录。这样，即使防火墙系统被攻破，入侵者也无法通过远程登录使用 root 权限。
- 它必须保存在物理安全的位置。
- 它必须区分来自 Internet 的数据包和来自内部受保护网络的数据包。此功能允许防火墙拒绝来自 Internet 但具有内部网络受信任系统 IP 地址的数据包。
- 它应充当内部网络的 SMTP 邮件网关。应设置 sendmail 软件，使所有传出邮件看起来都来自防火墙系统。
- 它不应有任何用户帐户。但是，防火墙系统可能需要为需要访问外部系统的内部用户设置几个用户帐户。需要访问内部网络的外部用户应使用 SSH 进行远程登录（请参阅本章前面关于 SSH 的讨论）。
- 它应记录所有系统活动，例如成功和不成功的登录尝试。
- 它应向外部世界提供 DNS 名称查找服务，以解析应为外部世界所知的任何主机名。
- 它应提供良好的性能，以便不会妨碍内部用户访问特定的 Internet 服务（例如 HTTP 和 FTP）。

防火墙可以采用多种不同的形式。以下是防火墙的三种常见形式：

- 带数据包过滤的筛选路由器：这种简单的防火墙使用能够根据 IP 地址过滤（阻止）数据包的路由器。



-   **使用代理服务的双宿主主机：** 在这种情况下，具有两个网络接口的主机——一个在互联网上，另一个在内部网络上——运行代理服务，作为 FTP 和 HTTP 等服务的网关。
-   **带堡垒主机的外围网络：** 此防火墙配置在互联网和受保护的内部网络之间包括一个外围网络。安全的堡垒主机驻留在外围网络上并提供各种服务。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_586_0.png)

在大型组织中，你可能还必须将较小的内部网络与企业网络隔离。你可以以设置互联网防火墙相同的方式设置此类内部防火墙。

在接下来的几节中，我将描述防火墙的常见形式：使用包过滤的筛选路由器、双宿主主机、带堡垒主机的外围网络以及应用网关。

## 使用包过滤的筛选路由器

如果你将组织的内部网络直接连接到互联网，你必须使用路由器以确保内部网络与互联网之间正确交换数据包。大多数路由器可以根据数据包的源或目标 IP 地址（以及其试图使用的端口号）来阻止数据包。路由器的包过滤功能可用作简单的防火墙。图 3-1 说明了包过滤的基本概念。

Figure 3-1:
使用筛选路由器进行包过滤可提供简单的防火墙。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_586_1.png)

许多路由器厂商，如 Cisco 和 3Com，提供可编程以执行包过滤的路由器。过滤的确切细节取决于路由器厂商，但所有路由器都根据互联网数据包的基本属性引用规则进行操作：

-   源 IP 地址
-   目标 IP 地址
-   协议（TCP、UDP 或 ICMP）
-   源端口号（如果协议为 TCP 或 UDP）
-   目标端口号（如果协议为 TCP 或 UDP）
-   ICMP 消息类型

此外，路由器知道数据包到达的物理接口以及数据包将要发出的接口（如果未被过滤规则阻止）。

大多数包过滤器按以下顺序操作：

1.  你根据 IP 地址和端口号定义允许或阻止特定类型数据包的规则。这些包过滤规则存储在路由器中。
2.  筛选路由器检查每个到达的数据包的头部，以获取你的规则适用的信息（如 IP 地址和端口号）。
3.  筛选路由器按其存储的顺序应用规则。
4.  如果规则允许数据包转发，路由器将数据包发送到其目的地。
5.  如果规则阻止数据包，路由器会丢弃数据包（停止处理它）。
6.  如果没有任何规则适用，数据包将被阻止。此规则体现了安全理念，即应“默认拒绝，除非明确允许”。

尽管使用筛选路由器的包过滤比没有安全措施更好，但包过滤存在以下缺点：

-   网络管理员很容易无意中在过滤规则中引入错误。
-   数据包是基于 IP 地址进行过滤的，IP 地址代表特定主机。基本上，包过滤要么阻止要么路由来自特定主机的所有数据包。这意味着任何侵入受信任主机的人都可以立即访问你的受保护网络。
-   因为它基于 IP 地址，包过滤可以被一种称为 *IP spoofing* 的技术击败，即黑客发送带有受信任主机 IP 地址的数据包（通过占用受信任主机的 IP 地址并设置适当的路由）；带有这些伪造 IP 地址的数据包随后可以访问你的系统。
-   包过滤容易受到路由攻击程序的影响，这些程序可以创建虚假路由，使入侵者接收所有发往受保护内部网络的数据包。
-   实现包过滤的筛选路由器不保留活动日志。这使得你很难确定是否有人试图入侵受保护的网络。正如你在下一节中看到的，双宿主主机可以提供日志记录。
-   筛选路由器不会隐藏内部网络的主机名和 IP 地址。外部人员可以访问并使用这些暴露的信息来对受保护网络发动攻击。

更复杂的方法是使用应用网关，根据特定应用程序而不是逐个数据包来控制网络流量。你可以用双宿主主机实现应用网关，双宿主主机也称为 *bastion host*。

## 双宿主主机

一个 *dual-homed host* 是一个具有两个网络接口的系统——一个连接到互联网，另一个位于需要保护的内部网络上。术语“双宿主”指的是主机“生活”在两个网络中。

事实上，如果你的操作系统支持 IP 路由——即能够从一个接口转发网络数据包到另一个接口——双宿主主机可以充当路由器。然而，你必须关闭 IP 转发功能才能将双宿主主机用作防火墙系统。

Linux 内核支持 IP 转发功能。如果你计划将双宿主主机用作防火墙，你必须使用 `sysctl` 命令禁用 IP 转发。

关闭 IP 转发后，两个网络上的系统——内部网络以及互联网——都可以访问双宿主主机，但互联网上的任何人无法访问内部网络（内部网络上的任何人也无法访问互联网）。在此配置中，双宿主主机完全隔离了这两个网络。图 3-2 显示了双宿主主机的基本架构。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_589_0.png)

Figure 3-2:
双宿主主机可充当互联网防火墙。

双宿主主机通过在双宿主主机上运行应用网关——代理服务——被转变为防火墙。这些代理服务允许特定应用程序，如 FTP 和 HTTP，在双宿主主机上工作。这意味着你可以配置防火墙，使内部客户端（在内部网络上）能够访问互联网上的 Web 和 FTP 服务器。

你的公共网站也可以在双宿主主机上运行，并可供互联网上的每个人访问。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_589_1.png)

不要在双宿主主机上允许用户登录。任何登录到主机的人都可以访问内部网络和互联网。由于双宿主主机是你互联网与内部网络之间唯一的屏障，最好不要通过允许用户登录防火墙系统来增加被入侵的机会。在那里放置用户账户会增加入侵者通过破解用户密码获得防火墙访问权限的机会。

## 带堡垒主机的外围网络

互联网防火墙通常比单个同时连接到互联网和受保护内部网络的双宿主主机更复杂。特别是，如果你提供多种互联网服务，你可能需要多个系统来承载它们。假设你有两个系统：一个运行 Web 和 FTP 服务器，另一个提供邮件（SMTP）和域名系统（DNS）查询。在这种情况下，你将这两个系统放置在互联网和内部网络之间的网络上。图 3-3 说明了互联网防火墙的这一概念。

Figure 3-3:
更完整的互联网防火墙包括外围网络和堡垒主机。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_590_0.png)

在这种情况下，防火墙包括一个通过外部路由器连接到互联网的外围网络。外围网络反过来通过内部路由器连接到内部网络。外围网络有一个或多个运行互联网服务的主机，包括代理服务器（稍后会详细介绍），这些代理服务器允许内部主机访问互联网上的 Web 服务器。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_590_1.png)

术语堡垒主机指的是外围网络上的任何系统，因为此类系统位于互联网上并且必须得到充分加固。双宿主主机也是堡垒主机，因为双宿主主机也可以从互联网访问并且必须受到保护。

在图 3-3 所示的防火墙配置中，外围网络被称为 DMZ（非军事区）网络，因为该网络充当互联网与内部网络之间的缓冲区（正如现实生活中的 DMZ 是朝鲜半岛南北之间的缓冲区）。

通常，你会将包过滤路由器与堡垒主机结合使用。你的互联网服务提供商通常提供外部路由器，这意味着你对该路由器配置的控制有限。但你提供内部路由器，这意味着你可以选择筛选路由器并采用一些包过滤规则。例如，你可能会采用以下包过滤规则：

-   从内部网络，仅允许发往堡垒主机的包。
-   从 DMZ，仅允许源自堡垒主机的包。
-   阻止所有其他包。



这确保内部网络仅与堡垒主机（或多台主机）通信。

与双宿主机类似，堡垒主机也运行一个应用网关，为各种 Internet 服务提供代理服务，例如 TELNET、FTP、SMTP 和 HTTP。

## Application gateway

堡垒主机或双宿主机是充当 Internet 与受保护内部网络之间中介的系统。因此，该系统充当内部网络通往 Internet 的网关。为此，系统运行软件以转发和过滤各种服务的 TCP/IP 数据包，例如 TELNET、FTP 和 HTTP。用于转发和过滤特定应用 TCP/IP 数据包的软件称为代理服务器。图 3-4 说明了代理服务器在防火墙中的作用。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_591_0.png)

Figure 3-4:
代理服务器让内部主机访问 Internet 服务器。

代理服务器接受特定协议（如 FTP）的连接，并将请求转发到另一台服务器。换句话说，代理服务器充当实际服务器的代理。因为它充当特定应用（如 HTTP 或 FTP）的网关，所以代理服务器也称为应用网关。

与仅根据数据包头信息（如源 IP 地址和目标 IP 地址）阻止数据包的筛选路由器不同，代理服务器使用数据包的数据来决定如何处理。例如，代理服务器不会盲目地将数据包转发到 Internet 服务。代理服务器可以根据特定应用执行站点的安全策略并禁止某些操作。例如，FTP 代理服务器可能阻止内部网络的用户使用 FTP put 命令将文件发送到 Internet。

通过代理服务器访问 Internet 服务比直接访问该服务稍微复杂一些。例如，内部网络上的用户与 Internet 主机建立 TELNET 会话的步骤如下：

- 1. 用户与防火墙主机建立 TELNET 会话——运行 TELNET 代理的系统。为此，用户必须输入用户名和密码，以便防火墙主机验证用户是否有权连接到 Internet。
- 2. 用户输入一条命令（TELNET 代理接受该命令）以连接到 Internet 主机。TELNET 代理随后在自身与 Internet 主机之间建立 TELNET 连接。
- 3. 防火墙上的 TELNET 代理开始在 Internet 主机与用户系统之间来回传递数据包（直到用户结束与 Internet 主机的 TELNET 会话）。

除了充当网关之外，TELNET 代理还会记录用户与 Internet 主机的会话。日志记录是应用网关安全功能的一部分，因为日志文件会跟踪所有防火墙访问（以及可能因用户名或密码错误而失败的尝试访问）。

尽管 TELNET 会话涉及两个步骤——首先 TELNET 到防火墙主机，然后连接到 Internet 主机——通过代理访问服务的流程不必过于繁琐。你通过防火墙访问服务的具体步骤取决于所使用的代理软件和用于访问服务的客户端程序。借助合适的客户端程序，代理可以对用户透明。例如，许多 Web 浏览器使通过 HTTP 代理访问网站变得容易。你只需通过菜单选择指定要使用的 HTTP 代理即可。

## Enabling Packet Filtering on Your Red Hat Linux System

你的 Red Hat Linux 系统内置了数据包过滤软件，形式为 Linux 内核中的 netfilter。你只需使用 `iptables` 命令根据数据包头中的 IP 地址和网络连接类型设置数据包的处理规则即可。

内置的数据包过滤功能在 Red Hat Linux 系统与 Internet 之间没有专用防火墙时非常方便。例如，当你通过 DSL 或有线调制解调器将 Red Hat 系统连接到 Internet 时就是这种情况。你基本上可以在 Red Hat Linux 系统内部拥有一个数据包过滤防火墙，位于内核和应用程序之间。

## Using the security level configuration tool

你可以通过图形化的 Security Level Configuration 工具开启不同级别的数据包过滤。要运行该工具，以 `root` 身份登录并选择 主菜单 → 系统设置 → 安全级别。安全级别配置窗口出现（图 3-5）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_593_0.png)

Figure 3-5:
你可以使用此工具设置预定义的数据包过滤级别。

你可以使用安全级别配置工具选择两种预定义的简单防火墙（更准确地说是数据包过滤）级别：

- **禁用防火墙：** 不执行任何过滤，所有连接都被允许（你仍可通过不运行服务器或在 `xinetd` 配置文件中禁用它们来关闭 Internet 服务）。如果你的 Red Hat Linux 系统位于受保护的局域网内或你拥有独立的防火墙设备，此安全级别是可以的。
- **启用防火墙：** 打开数据包过滤。然后你可以选择要允许的服务和你信任的网络设备。

你可以允许发往特定 Internet 服务（如 SSH、TELNET 和 FTP）的数据包。如果将 eth0（第一块以太网卡）等网络接口设为受信任，则该接口上的所有网络流量都将被允许而不进行过滤。

## Using the iptables command

使用 iptables 命令有些复杂。iptables 使用链的概念，链是一系列规则。每条规则说明如果数据包头包含某些信息（如源或目标 IP 地址）该如何处理。如果一条规则不适用，iptables 会咨询链中的下一条规则。默认情况下有三个链：

- **INPUT 链：** 用于测试数据包的第一组规则。只有当输入链未指定 DROP 或 REJECT 时，数据包才会继续到下一链。
- **FORWARD 链：** 包含适用于尝试通过本系统传递到另一系统的包的规则（例如，当你使用 Red Hat Linux 系统作为 LAN 与 Internet 之间的路由器时）。
- **OUTPUT 链：** 包括在数据包发送出去（到另一个网络或应用程序）之前应用的规则。

你可以使用 iptables 命令向这些链添加规则或创建新的规则链。你也可以查看当前链并将其保存到文件中。例如，如果你没有做其他操作，iptables -L 命令应显示以下内容：

```
Chain INPUT (policy ACCEPT)
target     prot opt source               destination

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
```

在这种情况下，三个链——INPUT、FORWARD 和 OUTPUT——都显示相同的 ACCEPT 策略，这意味着一切都是开放的。

如果你要设置数据包过滤器，第一步是指定要接受的数据包。例如，要接受来自 192.168.0.0 网络的数据包，请向输入链添加以下规则：

```
iptables -A INPUT -s 192.168.0.0/24 -j ACCEPT
```

现在添加规则以丢弃除本地回环（lo 网络接口）流量之外的所有内容并停止所有转发，使用以下命令：

```
iptables -A INPUT -i ! lo -j REJECT
iptables -A FORWARD -j REJECT
```

例如，第一个 iptables 命令将规则追加到输入链（-A INPUT），即如果数据包不是来自 lo 接口（-i ! lo），iptables 应拒绝该数据包（-j REJECT）。

在拒绝所有其他数据包之前，你也可以向每个 INPUT 链添加更多规则以允许特定数据包进入。你可以根据许多不同参数选择要接受或拒绝的数据包，例如 IP 地址、协议类型（TCP、UDP）、网络接口或端口号。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_595_0.png)

不要从远程登录会话输入 iptables 命令。开始拒绝来自所有地址的数据包的规则也可能阻止你输入的内容到达系统；一旦发生这种情况，你可能无法通过网络访问系统。为了避免不愉快的意外，始终在控制台输入 iptables 规则——即直接连接到运行数据包过滤器的 Red Hat Linux PC 的键盘和显示器。如果你想迅速删除所有过滤规则，可以通过输入以下命令将其刷新：

```
iptables -F
```

本节不会提供 iptables 命令的所有细节。简而言之，你可以输入 man iptables 来阅读命令摘要。你也可以在 www.iptables.org 阅读有关 netfilter 和 iptables 的信息。

使用 iptables 命令定义规则后，它们会保存在内存中，并在系统重启时消失。要保存它们，请使用 iptables-save 命令将规则存储到文件中。例如，你可以使用以下命令将规则保存到名为 iptables.rules 的文件中：

```
iptables-save > iptables.rules
```

以下是 iptables.rules 文件的列表，由 Red Hat Linux 系统生成：

```
# Generated by iptables-save v1.2.7a on Sun Jun 22 18:12:40 2003
*filter
:INPUT ACCEPT [976:61298]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [938:131584]
```

```
-A INPUT -s 192.168.0.0/255.255.255.0 -j ACCEPT
-A INPUT -i ! lo -j REJECT --reject-with icmp-port-unreachable
-A FORWARD -j REJECT --reject-with icmp-port-unreachable
COMMIT
# Completed on Sun Jun 22 18:12:40 2003
```

如果你好奇的话，这些规则对应于我用来配置过滤器的以下 iptables 命令：

```
iptables -A INPUT -s 192.168.0.0/24 -j ACCEPT
iptables -A INPUT -i ! lo -j REJECT
iptables -A FORWARD -j REJECT
```

如果你想将这些已保存的规则加载到 iptables 中，请使用以下命令：

```
iptables-restore < iptables.rules
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_596_0.png)

在 Red Hat Linux 系统上，保存和恢复防火墙规则的过程是自动化的，通过将 iptables 规则保存到文件 /etc/sysconfig/iptables 中，并使用以下命令启用 iptables：

```
chkconfig iptables on
```

这应确保在系统启动时执行 /etc/init.d/iptables start 命令。随后 /etc/init.d/iptables 脚本会运行 /sbin/iptables-restore 命令，从 /etc/sysconfig/iptables 文件中恢复 iptables 规则。

### 第 4 章：执行安全审计

### 本章内容

- 了解计算机安全审计
- 学习安全测试方法
- 审查主机和网络安全
- 探索安全测试工具

你看到“审计”这个词就想到税务审计，对吧？嗯，审计的类型有很多，其中一种就是计算机安全审计。计算机安全审计的目的基本上是测试你的系统和网络安全。对于大型组织，安全审计可能由独立审计员执行（就像财务报表审计一样）。如果你只有少数几个 Red Hat Linux 系统或一个小型网络，你可以将其作为自我评估来进行安全审计，只是为了弄清楚你是否一切做得都好。

在本章中，我将解释如何执行计算机安全审计，并向你展示许多免费工具和资源，帮助你测试系统的安全性。

## 了解安全审计

审计只是在审计对象上的独立评估。因此，计算机安全审计是对计算机安全的独立评估。如果有人对你的组织进行计算机安全审计，他或她通常会关注两个方面：

- 独立核实你的组织是否遵守其现有的计算机安全政策和程序。这是安全审计的非技术部分。
- 独立测试你的安全控制措施（用于保护系统的任何硬件和软件机制）的有效性。这是安全审计的技术部分。

为什么我们需要安全审计？我们需要它们的原因与我们需要财务审计的原因相同——主要是为了核实一切是否按应有的方式进行。对于公共组织和私营组织，管理层可能希望进行独立的安全审计，以确保自己的安全万无一失。无论你的组织规模大小，你都可以自行进行安全审计，要么为独立安全审计做准备，要么只是为了知道自己做的一切都是正确的。

无论是独立安全审计还是自我评估，以下是安全审计带来的一些好处：

- 定期进行风险评估，考虑对系统和数据的内部和外部威胁。
- 定期测试安全策略、安全控制措施和技术的有效性。
- 识别系统中任何重大的安全缺陷（以便你知道该修复什么）。
- 在自我评估的情况下，为组织可能面临的任何年度独立安全测试做准备。

### 安全审计的非技术方面

计算机安全审计的非技术方面关注的是你组织范围内的安全框架。审计检查组织在计算机安全政策、计划和程序的制定和实施方面做得如何。需要核实的项目包括

- 风险会定期评估。
- 存在全实体安全计划。
- 建立了安全计划管理结构。
- 计算机安全责任明确分配。
- 制定了有效的安全相关人员政策。
- 安全计划的有效性得到监控，并在需要时进行更改。

正如你所预期的那样，安全审计的非技术方面涉及审查文件和访谈相关人员，以了解组织如何管理计算机安全。当然，对于小型组织或家庭 PC，要求文件中有计划和程序是不现实的。在这些情况下，你只需要确保已实施一些技术控制措施来保护你的系统和网络连接。

## 安全审计的技术方面

计算机安全审计的技术方面侧重于测试保护主机和网络的技术控制措施。测试涉及确定

- **主机是否得到妥善保护。** 是否应用了所有操作系统补丁？文件权限是否设置正确？用户账户是否受保护？文件更改是否被监控？日志文件是否被监控？等等。
- **网络是否得到妥善保护。** 不必要的 Internet 服务是否已关闭？是否安装了防火墙？远程登录是否使用 SSH 等工具进行保护？是否使用 TCP wrapper 访问控制？等等。

通常，安全专家使用自动化工具执行这两个安全审查——主机和网络。

## 学习安全测试方法

计算机安全审计的一个关键要素是对用于保护主机和网络的技术机制进行安全测试。安全测试方法遵循以下高层次步骤：

- 1. 清点组织的网络、主机、网络设备（路由器、交换机、防火墙等），以及网络如何连接到 Internet。
- 2. 如果主机和网络连接很多，确定应测试的重要主机和网络设备。主机的 importance 取决于其运行的应用类型。
- 3. 单独测试主机。通常，这涉及以系统管理员身份登录，然后检查主机安全的各个方面，从密码到系统日志文件。
- 4. 测试网络。这通常是通过从 Internet 上的另一系统尝试突破网络防御来完成的。如果有防火墙，测试会检查防火墙是否确实配置正确。
- 5. 分析主机和网络测试的结果，以确定漏洞和风险。

这两种测试类型——主机和网络——各自关注构成整体计算机安全的三个方面：

- **预防：** 包括有助于防止对系统和网络攻击的机制（非技术性和技术性）。
- **检测：** 指诸如监控日志文件、检查文件完整性以及入侵检测系统等技术，可检测到有人即将或已经入侵你的系统。
- **响应：** 包括在发生计算机安全事件时你所执行的操作，例如向当局报告事件以及从备份中恢复重要文件。

对于主机和网络安全，这些领域各有重叠。例如，主机安全方面的预防机制，如良好的密码或文件权限，也可提供网络安全。尽管如此，以预防、检测和响应三个方面来思考是有帮助的。

然而，在考虑预防之前，你必须了解你试图预防的问题类型。换句话说，常见的网络安全漏洞是什么？预防和检测步骤通常取决于这些漏洞是什么。

### 一些常见的计算机漏洞

主机和网络安全的具体测试取决于常见漏洞。基本上，思路是检查主机或网络是否存在黑客最有可能利用的漏洞。

### 计算机漏洞的在线资源

有几个在线资源可识别和分类计算机安全漏洞：

- **SANS Institute** 在 www.sans.org/top20/ 发布了最关键的 20 项 Internet 安全漏洞清单。
- **CVE（通用漏洞和暴露）** 是漏洞的标准名称列表。有关 CVE 的更多信息，请参阅 cve.mitre.org（该列表包含超过 2,500 个漏洞名称）。使用 CVE 名称描述漏洞是常见做法。
- **ICAT 元数据库** 是由美国政府机构国家标准与技术研究院（NIST）发布的有关计算机漏洞信息的可搜索索引。ICAT 漏洞索引在线位于 icat.nist.gov。ICAT 列出了超过 5,800 个漏洞，并为每个漏洞提供漏洞公告和补丁信息的链接。ICAT 还发布一份 Top 10 列表，列出过去一年中查询次数最多的漏洞。

### 典型的 Top 20 计算机漏洞

SANS Top 20 漏洞列表包括三种类型的漏洞：影响所有系统的通用漏洞、Windows 和 UNIX。其中，通用

并且 UNIX 漏洞与 Red Hat Linux 相关。表 4-1 总结了适用于 Red Hat Linux 的通用和 UNIX 漏洞。您可以在 www.sans.org/top20.htm 上阅读这些漏洞的完整详细信息。

表 4-1 常见计算机漏洞类型

| 漏洞类型 | 描述 |
|---|---|
| *通用漏洞* | |
| 默认安装选项 | 这些是由于默认安装选项引入的漏洞，这些选项通常会安装不必要的软件或以不太安全的方式配置软件。 |
| 弱密码或无密码 | 许多用户账户使用弱密码，容易被密码破解程序破解。此外，一些软件包可能会添加没有密码或使用人人皆知的标准密码的用户账户。 |
| 不完整或无备份 | 如果发生安全事件，文件可能需要从备份中恢复。然而，不定期进行备份或不测试备份的完整性是常见的错误。 |
| 大量开放端口 | 开放端口指的是系统上启用的 Internet 服务。有时系统上运行着许多不必要的 Internet 服务。 |
| 数据包过滤不正确或未过滤 | 基于 IP 地址的数据包过滤器可以减少攻击，但许多系统未启用任何数据包过滤。使用 `iptables`，在 Red Hat Linux 中启用数据包过滤很容易。 |
| 不完整或无日志记录 | 系统日志是弄清导致有人入侵系统的事件序列的唯一方法。不幸的是，有时日志记录未正确设置。 |
| 易受攻击的 CGI 程序 | 此漏洞指的是用于在 Web 服务器上处理交互式网页（例如请求用户输入的表单）的通用网关接口（CGI）。存在漏洞（如缓冲区溢出）的 CGI 程序可为攻击者提供破坏系统的途径。 |
| *UNIX 漏洞* | |
| RPC 缓冲区溢出（NFS、NIS） | 网络文件系统（NFS）和网络信息系统（NIS）等服务使用远程过程调用（RPC），RPC 中存在一些已知漏洞。 |
| Sendmail 漏洞 | Sendmail 是一种用于在系统之间传输邮件消息的复杂程序，部分版本的 Sendmail 存在漏洞。 |
| BIND（DNS）弱点 | 伯克利 Internet 名称域（BIND）是一个实现域名系统（DNS）的软件包，DNS 是将名称转换为 IP 地址的 Internet 名称服务。部分版本的 BIND 存在漏洞。 |
| R 命令（rlogin、rsh、rcp） | 所谓的 R 命令允许攻击者利用漏洞，提供对与其他系统存在隐式信任关系的任何系统的便捷访问（R 命令假定存在信任关系）。 |
| LPD（远程打印）漏洞 | LPD 是打印服务器进程，它在端口 515 上监听远程打印请求。不幸的是，远程打印功能存在缓冲区溢出漏洞。 |
| 默认 SNMP 字符串 | 简单网络管理协议（SNMP）用于远程监控和管理从路由器到计算机的各种网络连接系统。SNMP 缺乏良好的访问控制；如果系统上运行 SNMP，攻击者可能能够重新配置或关闭系统。 |

## 主机安全审查

在审查主机安全时，重点评估以下各方面的安全机制：

- **预防：** 安装操作系统更新，使用安全密码，改进文件权限，为引导加载程序设置密码，并使用加密。
- **检测：** 捕获日志消息并使用 Tripwire 检查文件完整性。
- **响应：** 定期备份并制定事件响应程序。

接下来我将审查其中一些主机安全机制。

## 操作系统更新

Red Hat 在得知任何安全漏洞后会立即发布 Red Hat Linux 更新，但下载和安装更新由您或系统管理员负责。跟上 Red Hat Linux 安全补丁的一种方法是注册 Red Hat Network 服务（单台机器免费，但多台机器需订阅）。

您可以使用 rpm 命令安装补丁。如果将所有当前更新放在单个目录中，可以使用以下命令安装它们：

```
rpm -F *.rpm
```

对于大型组织，应由授权的系统管理员安装操作系统更新。

为了评估操作系统更新是否最新，审计员会获取 Red Hat Linux 关键组件的当前更新列表，然后使用 rpm 命令检查它们是否已安装。例如，如果列表显示系统应具有 glibc 版本 2.3.2，审计员会输入以下命令查看当前 glibc 版本号：

```
rpm -q glibc
```

如果版本号小于 2.3.2，则结论是未安装操作系统更新。

## 文件权限

关键系统文件应使用适当的文件所有权和文件权限进行保护。分配文件系统所有权和权限的关键步骤如下：

- 确定哪些文件包含敏感信息以及原因。一些文件可能包含与您的工作或业务相关的敏感数据，而许多其他文件之所以敏感，是因为它们控制着 Red Hat Linux 系统配置。
- 维护当前授权用户列表以及他们在系统上被授权执行的操作。
- 设置密码、组、文件所有权和文件权限，仅允许授权用户访问文件。

表 4-2 列出了 Red Hat Linux 中一些重要的系统文件，并显示了每个文件的数字权限设置。

表 4-2 重要系统文件及其权限

| 文件路径名 | 权限 | 描述 |
|---|---|---|
| /boot/grub/grub.conf | 600 | GRUB 引导加载程序配置文件 |
| /etc/cron.allow | 400 | 允许使用 cron 提交周期性作业的用户列表 |
| /etc/cron.deny | 400 | 不允许使用 cron 提交周期性作业的用户列表 |
| /etc/crontab | 644 | 全系统周期性作业 |
| /etc/hosts.allow | 644 | 允许使用 TCP wrappers 启动的 Internet 服务的主机列表 |
| /etc/hosts.deny | 644 | 被拒绝访问使用 TCP wrappers 启动的 Internet 服务的主机列表 |
| /etc/logrotate.conf | 644 | 控制日志文件轮转的文件 |
| /etc/pam.d | 755 | 包含可插拔认证模块（PAM）配置文件的目录 |
| /etc/passwd | 644 | 旧式密码文件，包含用户账户信息但不包含密码 |
| /etc/rc.d | 755 | 包含系统启动脚本的目录 |
| /etc/securetty | 600 | root 可以登录的 TTY 接口（终端） |
| /etc/security | 755 | 控制系统访问的策略文件 |
| /etc/shadow | 400 | 包含加密密码和密码过期信息的文件 |
| /etc/shutdown.allow | 400 | 可以通过按 Ctrl+Alt+Delete 关闭或重启的用户 |
| /etc/ssh | 755 | 包含安全外壳（SSH）配置文件的目录 |
| /etc/sysconfig | 755 | 系统配置文件 |
| /etc/sysctl.conf | 644 | 内核配置参数 |
| /etc/syslog.conf | 644 | 记录消息的 syslogd 服务器的配置文件 |
| /etc/vsftpd | 600 | 非常安全的 FTP 服务器的配置文件 |
| /etc/vsftpd/ftpusers | 600 | 不能使用 FTP 传输文件的用户列表 |
| /etc/xinetd.conf | 644 | xinetd 服务器的配置文件 |
| /etc/xinetd.d | 755 | 包含 xinetd 服务器可启动的特定服务配置文件的目录 |
| /var/log | 755 | 包含所有日志文件的目录 |
| /var/log/lastlog | 644 | 所有先前登录的信息 |
| /var/log/messages | 644 | 主系统消息日志文件 |
| /var/log/secure | 400 | 与安全相关的日志文件 |
| /var/log/wtmp | 664 | 当前登录的信息 |

另一个重要检查是查找具有 setuid 权限的可执行程序文件。如果程序具有 setuid 权限并且由 root 所有，则该程序以 root 权限运行，无论实际运行该程序的是谁。您可以使用以下 find 命令找到所有 setuid 程序：

```
find / -perm +4000 -print
```

您可能希望将输出保存到文件中（只需在命令后附加 > filename），然后检查文件中是否存在任何不寻常的 setuid 程序。例如，用户主目录中的 setuid 程序是不寻常的。

## 密码安全

验证密码、组和 shadow 密码文件是否受到保护。特别是，shadow 密码文件应写保护且仅 root 可读。文件名及其推荐权限如表 4-3 所示：

表 4-3 密码文件的所有权和权限

| 文件路径名 | 所有权 | 权限 |
|---|---|---|
| /etc/group | root.root | 644 |
| /etc/passwd | root.root | 644 |
| /etc/shadow | root.root | 400 |

## 事件响应

事件响应是回答系统发生异常情况时该怎么办的策略——它告诉您如果有人入侵系统该如何处理。

您对事件的响应取决于您如何使用系统以及它对您或您业务的重要性。有关全面的事件响应，请记住以下要点：

- 弄清你的计算机和网络有多么关键和重要，并确定谁或哪些资源可以帮助你保护系统。
- 采取措施防止和最大程度地减少潜在的损害和中断。
- 制定并记录一份全面的应急计划。
- 定期测试应急计划并根据需要修订程序。

## 网络安全审查

*网络安全审查侧重于评估以下各方面的安全机制：*

- **预防：** 设置防火墙，启用数据包过滤，禁用不必要的 `xinetd` 服务，关闭不需要的 Internet 服务，使用 TCP wrappers 进行访问控制，并使用 SSH 进行安全远程登录。
- **检测：** 使用网络入侵检测并捕获系统日志。
- **响应：** 制定事件响应程序。

我简要描述评估网络安全时的一些关键步骤。

### 由 xinetd 启动的服务

许多 Internet 服务，例如 TELNET 和 `sgi_fam`（`sgi_fam` 监视文件的更改）都是由 `xinetd` 服务器启动的。是否打开其中某些服务的决定取决于系统如何连接到 Internet 以及系统如何使用等因素。通常可以关闭大多数 `xinetd` 服务。

可通过以下任一方式检查哪些 `xinetd` 服务已打开：

- 检查 `/etc/xinetd.d` 目录中的配置文件，以查看 `xinetd` 可以启动的所有服务。如果某项服务已关闭，配置文件中会有如下一行：
  
  ```
  disable = yes
  ```
  
  请记住，如果在该行的开头放置 `#` 将其注释掉，则 `disable = yes` 行无效。
- 输入以下命令以禁用 `xinetd` 可以启动的服务：
  
  ```
  chkconfig servicename off
  ```
  
  其中 `servicename` 是服务的名称（如 `telnet` 或 `sgi_fam`）。要检查 `xinetd` 可以启动的服务的名称，请输入以下命令：

```
chkconfig --list | more
```

在输出中查找以下行：

```
xinetd based services:
```

这些行列出了 xinetd 可以启动的所有服务以及它们是开启还是关闭。例如，以下是系统上 xinetd 服务状态的几行示例：

```
chargen-udp: off
rsync: off
chargen: off
daytime-udp: off
daytime: off
echo-udp: off
echo: off
services: off
servers: off
time-udp: off
time: off
cups-lpd: off
sgi_fam: on
ktalk: off
imap: off
... lines deleted ...
```

在这种情况下，sgi_fam（报告任何文件更改的服务器）服务处于开启状态，但其他所有服务均已关闭。

还请检查以下文件，以查看与 xinetd 服务一起使用的任何访问控制：

- `/etc/hosts.allow` 列出允许访问特定服务的计算机主机。
- `/etc/hosts.deny` 列出应拒绝访问服务的计算机主机。

### 独立服务

许多服务，例如 httpd（Web 服务器）和 sendmail（邮件服务器），在启动时会自动启动，前提是它们被配置为这样启动。你可以使用 chkconfig 命令检查这些独立服务器在各个运行级别中是否设置为启动（有关运行级别的更多信息，请参阅第 VI 书第 1 章）。通常，你的 Red Hat Linux 系统在运行级别 3（文本登录）或 5（图形登录）下启动。因此，重要的是级别 3 和 5 中服务器的设置。要查看服务器列表，请输入以下命令：

```
chkconfig --list | more
```

这是一个你可能会看到的部分列表：

gpm 0:off 1:off 2:on 3:on 4:on 5:on 6:off
kudzu 0:off 1:off 2:off 3:on 4:on 5:on 6:off
syslog 0:off 1:off 2:on 3:on 4:on 5:on 6:off
rawdevices 0:off 1:off 2:off 3:on 4:on 5:on 6:off
netfs 0:off 1:off 2:on 3:on 4:on 5:on 6:off
network 0:off 1:off 2:on 3:on 4:on 5:on 6:off
random 0:off 1:off 2:on 3:on 4:on 5:on 6:off
saslauthd 0:off 1:off 2:off 3:off 4:off 5:off 6:off
pcmcia 0:off 1:off 2:on 3:on 4:on 5:on 6:off
keytable 0:off 1:on 2:on 3:on 4:on 5:on 6:off
apmd 0:off 1:off 2:on 3:on 4:on 5:on 6:off
atd 0:off 1:off 2:off 3:on 4:on 5:on 6:off
autofs 0:off 1:off 2:off 3:on 4:on 5:on 6:off
iptables 0:off 1:off 2:on 3:on 4:on 5:on 6:off
irda 0:off 1:off 2:off 3:off 4:off 5:off 6:off
isdn 0:off 1:off 2:on 3:on 4:on 5:on 6:off
sshd 0:off 1:off 2:on 3:on 4:on 5:on 6:off
portmap 0:off 1:off 2:off 3:on 4:on 5:on 6:off
nfs 0:off 1:off 2:off 3:off 4:off 5:off 6:off
nfslock 0:off 1:off 2:off 3:on 4:on 5:on 6:off
sendmail 0:off 1:off 2:on 3:on 4:on 5:on 6:off
xfs 0:off 1:off 2:off 3:on 4:on 5:on 6:off
crond 0:off 1:off 2:on 3:on 4:on 5:on 6:off
...lines deleted...

第一列显示服务器的名称。查看以 3: 开头的条目列以及以 5: 开头的条目列。这些显示了服务器在运行级别 3 和 5 中的状态。显示为 on 的服务器会在你的 Red Hat Linux 系统启动时自动启动。

如果你正在进行网络安全自我评估，发现某些服务器不应运行，你可以使用 chkconfig 命令按如下方式将其在运行级别 3 和 5 中关闭：

```
chkconfig --level 35 servicename off
```

将 servicename 替换为你要关闭的服务器的名称。

如果你正在审计网络安全，请记录所有已开启的服务器——然后根据你对系统的了解，尝试确定它们是否真的应该开启。是否开启某项特定服务的决定取决于系统的使用方式（例如作为 Web 服务器或桌面系统）以及它如何连接到 Internet（例如通过防火墙或直接连接）。

### 渗透测试

渗透测试是了解 Red Hat Linux 系统上实际运行哪些服务的最佳方法。渗透测试涉及从攻击者的角度尝试访问你的系统。通常，你从 Internet 上的系统执行此测试，尝试看是否可以入侵，或至少访问 Red Hat Linux 系统上运行的服务。

渗透测试的一个方面是查看 Red Hat Linux 系统上哪些端口是开放的。端口号只是一个标识系统特定 TCP/IP 网络连接的数字。仅当端口上运行着服务器（换句话说，如果服务器“正在监听该端口”）时，连接端口的尝试才会成功。如果在连接请求到达时服务器做出响应，则端口被视为开放。

渗透测试的第一步是执行端口扫描。端口扫描一词用于描述尝试连接到每个端口号以查看是否返回有效响应的自动化过程。许多可用的自动化工具可以执行端口扫描——Red Hat Linux 附带一个流行的端口扫描工具 nmap（我在本章后面描述）。

执行端口扫描后，你就知道可能被利用的潜在漏洞。并非所有服务器都有安全问题，但许多服务器存在众所周知的漏洞，而开放的端口为黑客提供了一种通过其中一个服务器攻击系统的途径。事实上，你可以使用称为漏洞扫描器的自动化工具来识别系统中存在的漏洞。（我接下来描述一些漏洞扫描器。）无论你的 Red Hat Linux 系统是通过 DSL 或电缆调制解调器直接连接到 Internet，还是通过防火墙连接，都应使用端口扫描和漏洞扫描工具来判断你的防御是否存在漏洞。还是你自己发现好！

### 探索安全测试工具

有许多自动化工具可用于执行安全测试。其中一些工具用于查找 IP 地址范围内每个系统的开放端口。其他工具则查找与开放端口相关的漏洞。还有其他工具可以捕获（或嗅探）这些弱点并帮助你分析它们，以便你能从中获取有关网络中正在发生的事情的有用信息。

你可以在 www.insecure.org/tools.html 浏览基于 nmap 用户非正式投票的前 50 名安全工具列表。表 4-4 按类别列出了其中一些工具。我在下一节中描述了一些可自由获取的漏洞扫描器。

表 4-4 一些流行的计算机安全工具

| 类型 | 工具名称 |
|---|---|
| 端口扫描器 | nmap, Strobe |
| 漏洞扫描器 | Nessus Security Scanner, SAINT, SARA, Whisker (CGI scanner), ISS Internet Scanner, CyberCop Scanner, Vetescan, Retina Network Security Scanner |



表 4-4 (续)

| 类型 | 工具名称 |
|---|---|
| 网络实用工具 | Netcat, hping2, Firewalk, Cheops, ntop, ping |
| 主机安全工具 | Tripwire, lsof |
| 数据包嗅探器 | tcpdump, Ethereal, dsniff, sniffit |
| 入侵检测系统 (IDSs) | Snort, Abacus, portsentry, scanlogd, NFR, LIDS |
| 密码检查工具 | John the Ripper, LC4 |
| 日志分析与监控工具 | logcolourise, tcpdstats, nlog, logcheck, Swatch |

## nmap

nmap（network mapper 的缩写）是一种端口扫描工具。它可以快速扫描大型网络，并确定网络上有哪些主机可用、它们提供哪些服务、运行的操作系统（以及操作系统版本）、使用何种类型的数据包过滤器或防火墙，以及数十种其他特征。Red Hat Linux 自带 nmap。你可以在 www.insecure.org/nmap 阅读更多关于 nmap 的信息。

如果你想尝试使用 nmap 扫描你的局域网，只需输入类似以下命令（将 IP 地址范围替换为适合你网络的地址）：

```
nmap -O -sS 192.168.0.2-10
```

这是该命令的典型输出示例：

```
Starting nmap 3.27 ( www.insecure.org/nmap/ ) at 2003-06-22 18:41 EDT
Interesting ports on 192.168.0.2:
(The 1618 ports scanned but not shown below are in state: closed)
Port     State    Service
135/tcp  open     loc-srv
139/tcp  open     netbios-ssn
445/tcp  open     microsoft-ds
1025/tcp open     NFS-or-IIS
5000/tcp open     UPnP
Remote operating system guess: Windows Millennium Edition (Me), Win 2000, or Win XP

Interesting ports on 192.168.0.3:
(The 1618 ports scanned but not shown below are in state: closed)
Port     State    Service
21/tcp   open     ftp
22/tcp   open     ssh
23/tcp   open     telnet
111/tcp   open   sunrpc
6000/tcp  open   X11
Remote operating system guess: Linux Kernel 2.4.0 - 2.5.20
<<Lines deleted...>>
Nmap run completed -- 9 IP addresses (3 hosts up) scanned in 95.420 seconds
```

如你所见，nmap 会显示开放端口的名称，并对操作系统名称和版本号进行推测。

## Nessus

Nessus 安全扫描器是一种模块化安全审计工具，它使用用 Nessus 脚本语言编写的插件来测试各种网络漏洞。Nessus 使用客户端-服务器软件架构，服务器名为 nessusd，客户端名为 nessus。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_612_0.png)

在尝试安装 Nessus 之前，你必须安装 sharutils RPM。该软件包包含 Nessus 安装脚本所需的 uudecode 实用程序。sharutils 软件包未随任何标准软件包组一起安装，因此你必须自行安装。

安装 sharutils，请按以下步骤操作：

- 1. 逐一挂载附带的 CD 并找到名称以 sharutils 开头的软件包。
  在将 CD 挂载到 /mnt/cdrom 后，尝试以下命令序列来找到正确的 CD：
  ```
  cd /mnt/cdrom/RedHat/RPMS
  ls sharutils*
  ```
- 2. 找到 sharutils 软件包后，使用以下命令安装它：
  ```
  rpm -ivh sharutils*.rpm
  ```

下载并安装 Nessus，请按以下步骤操作：

- 1. 阅读 www.nessus.org/download.html 上的说明。然后点击你想要下载的软件包的链接。按照说明下载文件 nessus-installer.sh 和 MD5。
- 2. 输入以下命令安装 Nessus（你必须已安装开发工具，包括 GIMP Toolkit）：
  ```
  sh nessus-installer.sh
  ```

按照安装脚本的提示完成安装。通常可以按 Enter 接受默认选项。

安装完成后，按以下步骤使用 Nessus：

- 1. **以 root 身份登录并输入以下命令，创建 Nessus 客户端与 Nessus 服务器之间安全通信所使用的 Nessus SSL 证书：**
  ```
  nessus-mkcert
  ```
- 2. **提供所需信息以完成证书生成过程。**
- 3. **使用以下命令创建 nessusd 账户：**
  ```
  nessus-adduser
  ```
- 4. **在提示时，输入用户名、密码以及任何规则（如果不知道输入什么规则，请按 Ctrl+D）。然后按 y。**
- 5. **如果你愿意，可以通过编辑配置文件 `/usr/local/etc/nessus/nessusd.conf` 来配置 nessusd。**
  如果你想尝试 Nessus，可以使用默认配置文件继续。
- 6. **使用此命令启动 Nessus 服务器：**
  ```
  nessusd -D
  ```
- 7. **在终端窗口中输入以下命令运行 Nessus 客户端：**
  ```
  nessus
  ```
  Nessus 设置窗口出现（图 4-1）。
- 8. **输入 nessusd 用户名和密码，然后点击 Log In。**
- 9. **当 Nessus 显示用于建立安全连接的证书并询问是否接受时，点击 Yes。**
  客户端连接到服务器后，Log in 按钮变为 Log out，其左侧会出现 Connected 标签。
- 10. **在 Target selection 选项卡上，输入要扫描网络中所有主机的 IP 地址范围。**
  例如，要扫描私有网络 192.168.0.0 中的前八台主机，我输入地址为：
  ```
  192.168.0.0/29
  ```
- 11. **点击 Start the Scan。**
  Nessus 开始扫描 IP 地址并检查许多不同的漏洞。进度条显示扫描状态（图 4-2）。

图 4-1:
用户登录后，Nessus 客户端屏幕如下所示。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_614_0.png)

图 4-2:
Nessus 通过进度条显示扫描状态。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_614_1.png)

Nessus 完成主机漏洞扫描后，会以图形和文本格式的良好组合显示结果（图 4-3）。报告是交互式的：你可以点击主机地址查看该主机的报告，并可以深入查看特定漏洞（包括标识该漏洞的 CVE 编号）。

图 4-3:
Nessus 在交互式报告中显示扫描结果。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_615_0.png)

## SAINT

安全管理员集成网络工具（SAINT）扫描主机是否存在各种安全漏洞。对于发现的漏洞，SAINT 会显示通用漏洞和暴露（CVE）标识符。SAINT 的旧版本是免费的，但最新版本仅提供给购买 SAINTWriter 或 SAINTexpress 的用户。

你可以从 www.saintcorporation.com/products/download.html 下载一个受限的（仅限扫描两台主机）15 天试用版 SAINT，看看它能做什么。你可以决定是否购买完整版。

我不会描述下载和安装试用版的步骤。你可以在下载 SAINT 免费试用版的页面上找到说明。

## SARA

安全审计研究助手（SARA）是一种基于 SAINT 的漏洞扫描工具。SARA 扫描已知漏洞，包括 CVE 列表和 SANS Top 20 列表（www.sans.org/top20/）中的漏洞。

要尝试 SARA，请从 www.arc.com/sara/downloads/ 下载最新版本的 SARA。下载压缩的 tar 文件后，使用以下步骤构建和安装软件：

- 1. **使用以下命令解压 tar 文件**
  `tar zxvf sara*`
- 2. **要配置 SARA，输入以下命令：**
  `cd sara*`
  `./configure`
- 3. **要构建软件，输入**
  `make`

SARA 构建完成后，使用以下命令运行它：
`./sara`

SARA 启动一个 Web 浏览器并在 Web 浏览器中显示其用户界面。

你可以通过点击 Web 浏览器左侧的链接执行各种任务。例如，要执行漏洞扫描，点击 Target Selection 链接。SARA 会弹出一个表单，你可以在其中提供要扫描的主机和网络信息。你还可以指定扫描级别——从轻度到极端。

填写信息后，点击表单底部的 Start the Scan 按钮。SARA 开始执行漏洞扫描。在扫描期间，SARA 显示一个数据收集页面，指示扫描进度。

扫描完成后，你可以进行数据分析和查看漏洞信息。



## 第八卷
## 互联网服务器
### 第五波
作者 Rich Tennant
@RICHTENNANT
![](img/a7eec43a54473e95dc5ea333fecf1bd7_618_0.png)

> 现在也许这些人有一个不错的灾难恢复计划，也许没有……

危险
野犀牛

## 目录一览
- 第 1 章：管理服务器 .........................................................593
- 第 2 章：运行 Apache 服务器 ....................................................611
- 第 3 章：设置 FTP 服务器 ....................................................633
- 第 4 章：提供邮件和新闻服务 ....................................................641
- 第 5 章：设置 DNS 和 NIS .......................................................669
- 第 6 章：运行 Samba 和 NFS .......................................................697

### 第 1 章：管理服务器
### 本章内容
- ✓ 了解互联网服务
- ✓ 通过 xinetd 控制服务器
- ✓ 使用 chkconfig 管理服务器
- ✓ 使用服务配置实用程序

互联网是一个由客户端和服务器组成的世界。客户端向服务器发出请求，服务器对请求做出响应。例如，你的 Web 浏览器是一个客户端，它从 Web 服务器下载信息并显示给你。当然，客户端和服务器是运行在各种各样的计算机上的计算机程序。Red Hat Linux 系统是运行各种服务器的理想系统，从 Web 服务器到 Windows 文件和打印服务器。在本章中，我概述了典型的互联网服务、其客户端/服务器架构以及如何在 Red Hat Linux 中管理服务器。你可以使用本章中的信息来管理在你的 Red Hat Linux 系统上运行的任何服务器。

### 了解互联网服务

*互联网服务* 是设计用于从一个系统向另一个系统传递信息的网络应用程序。按设计，每个互联网服务都实现为两个部分——一个提供信息的 *服务器*，以及一个或多个请求信息的 *客户端*。

这种 *客户端/服务器* 架构是构建分布式信息系统的最常见方式。客户端和服务器是运行在这些计算机上的计算机程序，并通过网络进行通信。妙处在于，你可以在桌面计算机上运行客户端，并从世界上任何地方的计算机上运行的服务器访问信息（只要它在互联网上）。

Web 本身、电子邮件和 FTP（文件传输协议）是使用客户端/服务器模型的互联网服务的例子。例如，当你使用 Web 时，你使用 Web 浏览器客户端从 Web 服务器下载和查看网页。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_621_0.png)

客户端/服务器架构要求客户端与服务器通信。这就是传输控制协议/互联网协议——TCP/IP——发挥作用的地方。TCP/IP 为客户端和服务器交换数据包提供了一种标准方式。在接下来的几节中，我将解释基于 TCP/IP 的服务如何通信。

### TCP/IP 和套接字

客户端/服务器应用程序，例如 Web 和 FTP，使用 TCP/IP 在客户端和服务器之间进行数据传输。这些互联网应用程序通常通过使用 Berkeley 套接字接口来使用 TCP/IP 通信（因此得名，因为套接字接口大约在 1982 年首次在 Berkeley UNIX 中引入）。套接字接口不是物理的——它只是一段计算机代码，计算机程序员可以使用它来创建可以与互联网上其他应用程序通信的应用程序。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_621_1.png)

即使你不使用套接字编写网络应用程序，你也可能需要使用或设置许多网络应用程序。了解套接字可以帮助你理解基于网络的应用程序的工作原理，进而帮助你查找和纠正这些应用程序的任何问题。

### 套接字定义

网络应用程序使用套接字通过 TCP/IP 网络进行通信。套接字代表连接的一端点。由于套接字是双向的，数据可以通过它发送也可以接收。套接字有三个属性：

- 系统的网络地址（IP地址）
- 端口号，标识通过套接字交换数据的进程（进程是运行在计算机上的计算机程序）
- 套接字类型，标识数据交换的协议

本质上，IP地址标识网络上的计算机（主机）；端口号标识节点上的进程（服务器）；而套接字类型决定数据交换的方式——通过面向连接（流）或无连接（数据报）协议。

### 面向连接的协议

套接字类型指示通过套接字通信所使用的协议。面向连接的协议的工作方式类似于正常的电话对话。当你想与朋友交谈时，你必须拨打朋友的电话号码并建立连接后才能进行对话。同样，面向连接的数据交换要求发送方和接收方进程在数据交换开始之前建立连接。

在 TCP/IP 协议族中，TCP——传输控制协议——支持互联网上两台计算机上运行的两个进程之间的面向连接的数据传输。TCP 在进程之间提供可靠的双向数据交换。

正如 TCP/IP 的名称所示，TCP 依赖于 IP——互联网协议——来传输数据包。IP 不保证数据包的交付；也不保证数据包按特定顺序交付。IP 却能有效地将数据包从一个网络移动到另一个网络。TCP 负责将数据包按正确顺序排列，检测是否发生错误，并在发生错误时请求重传数据包。

TCP 对于旨在一次交换大量数据的应用程序很有用。此外，需要可靠数据交换的应用程序也使用 TCP。（例如，FTP 使用 TCP 传输文件。）

在套接字模型中，使用 TCP 的套接字被称为流套接字。

### 无连接协议

无连接数据交换协议不需要发送方和接收方显式建立连接。这就像在拥挤的房间里大声喊叫你的朋友——你不能确定你的朋友是否听见了你。

在 TCP/IP 协议族中，用户数据报协议（UDP）提供无连接服务，用于发送和接收称为数据报的数据包。与 TCP 不同，UDP 不保证数据报是否到达其预期目的地。UDP 也不保证数据报按发送顺序交付。

UDP 由一次交换少量数据的应用程序或不需要数据交付的可靠性和顺序性的应用程序使用。例如，SNMP（简单网络管理协议）使用 UDP 传输数据。

在套接字模型中，使用 UDP 的套接字被称为数据报套接字。

### 套接字与客户端/服务器模型

完成通信路径需要两个套接字。当两个进程通信时，它们使用客户端/服务器模型来建立连接。图 1-1 说明了这一概念。服务器应用程序在系统上的特定端口上监听——服务器完全由其运行的系统的 IP 地址和其监听连接的端口号标识。客户端从任何可用端口发起连接并尝试连接到服务器（由 IP 地址和端口号标识）。连接建立后，客户端和服务器可以根据自己的协议交换数据。

图 1-1：客户端和服务器进程使用两个套接字进行通信。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_623_0.png)

套接字数据交换中的事件序列取决于传输是面向连接的（TCP）还是无连接的（UDP）。

对于使用套接字的面向连接的数据传输，服务器在特定端口上“监听”，等待客户端请求连接。数据传输仅在建立连接后才开始。

对于无连接数据传输，服务器等待数据报到达指定端口。客户端不会等待建立连接；它只是将数据报发送到服务器。

无论是服务器还是客户端，每个应用程序首先创建一个套接字。然后它将套接字与本地计算机的 IP 地址和端口号关联（绑定）。IP地址标识机器（应用程序运行的位置），端口号标识使用套接字的应用程序。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_623_1.png)

服务器通常监听众所周知的端口号，以便客户端可以连接到该端口以访问服务器。对于客户端应用程序，将套接字绑定到 IP 地址和端口的过程与服务器相同，但客户端可以使用 0 作为端口号；套接字库会自动为客户端使用一个未使用的端口号。

对于面向连接的流套接字，通信的客户端和服务器应用程序必须建立连接。建立连接的确切步骤取决于应用程序是服务器还是客户端。



![](img/a7eec43a54473e95dc5ea333fecf1bd7_624_0.png)

在客户端/服务器模型中，服务器必须先启动并运行，客户端才能运行。创建套接字并将套接字绑定到端口后，服务器应用程序会设置一个连接队列，该队列决定有多少客户端可以连接到服务器。通常，服务器监听的连接数在1到5个之间。然而，监听队列的大小是你可调整的参数之一（尤其是对于 Web 服务器），以确保服务器能够响应尽可能多的客户端。设置好监听队列后，服务器等待来自客户端的连接。

从客户端建立连接则相对简单一些。创建套接字并将套接字绑定到 IP 地址后，客户端与服务器建立连接。为了建立连接，客户端必须知道服务器的主机名或 IP 地址，以及服务器接受连接的端口。所有 Internet 服务都有众所周知的标准端口号。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_624_1.png)

客户端通过面向连接的流套接字与服务器建立连接后，客户端和服务器可以通过调用适当的套接字 API 函数交换数据。就像两个人之间的对话一样，服务器和客户端交替发送和接收数据——数据的含义取决于服务器和客户端使用的消息协议。通常，服务器是为特定任务设计的；该设计中固有的就是服务器和客户端用来交换必要数据的消息协议。例如，Web 服务器和 Web 浏览器（客户端）使用 HTTP（超文本传输协议）进行通信。

## Internet 服务和端口号

TCP/IP 协议套件是 Internet 的通用语言，因为 Internet 服务“说”TCP/IP。这些服务使 Internet 运转起来，因为它们使得邮件、新闻和网页的传输成为可能。每个 Internet 服务都有自己的协议，该协议依赖 TCP/IP 来实际传输信息。每个服务还分配有一个或多个端口号，用于执行其设计的功能。以下是一些知名 Internet 服务及其相关协议：

- **DHCP（动态主机配置协议）** 用于动态配置计算机上的 TCP/IP 网络参数。DHCP 主要用于分配动态 IP 地址以及配置 TCP/IP 网络所需的其他网络信息，例如名称服务器、默认网关和域名。DHCP 服务器监听 67 端口。
- **FTP（文件传输协议）** 用于在 Internet 上计算机之间传输文件。FTP 使用两个端口：数据在 20 端口传输，控制信息在 21 端口交换。
- **HTTP（超文本传输协议）** 用于从一个系统向另一个系统发送文档。HTTP 是 Web 的底层协议。默认情况下，Web 服务器和客户端在 80 端口通信。
- **SMTP（简单邮件传输协议）** 用于在系统之间交换电子邮件消息。SMTP 使用 25 端口进行信息交换。
- **NNTP（网络新闻传输协议）** 用于以存储转发方式在 Internet 上分发新闻文章。NNTP 使用 119 端口。
- **TELNET** 使一个系统上的用户能够登录到 Internet 上的另一个系统（用户必须提供有效的用户 ID 和密码才能登录到远程系统）。TELNET 默认使用 23 端口。然而，TELNET 客户端可以连接到任何指定端口。
- **NFS（网络文件系统）** 用于在计算机之间共享文件。NFS 使用 Sun 的远程过程调用（RPC）机制，该机制通过 111 端口交换信息。
- **NTP（网络时间协议）** 由客户端计算机用来将系统时间与服务器（具有更准确时钟的服务器）上的时间同步。NTP 使用 123 端口。
- **SNMP（简单网络管理协议）** 用于管理 Internet 上各种类型的网络设备。与 FTP 类似，SNMP 使用两个端口：161 和 162。
- **TFTP（简单文件传输协议）** 用于从一个系统向另一个系统传输文件（通常由 X 终端和无盘工作站用来从网络上的另一主机下载引导文件）。TFTP 数据传输在 69 端口进行。

每个服务都由一个服务器进程提供——一个在系统上运行的计算机程序，等待到达与其服务相关联的众所周知端口的客户端请求。因此，Web 服务器期望在 80 端口（HTTP 服务的标准端口）接收客户端请求。

/etc/services 文本文件在你的 Red Hat Linux 系统上存储服务名称与端口号（以及协议）之间的关联。以下是来自 Red Hat Linux 系统的 /etc/services 文件中的一个小子集：

```
ftp-data 20/tcp
ftp 21/tcp
ssh 22/tcp # SSH Remote Login Protocol
ssh 22/udp # SSH Remote Login Protocol
telnet 23/tcp
smtp 25/tcp mail
time 37/tcp timserver
time 37/udp timserver
nfs 39/udp resource # resource location
nameserver 42/udp name # IEN 116
whois 43/tcp nicname
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_626_0.png)

快速浏览 /etc/services 文件中的条目即可显示 TCP/IP 下可用的网络服务的广度。

请注意，端口号 80 指定用于 Web 服务。换句话说，如果你在系统上设置 Web 服务器，该服务器会监听 80 端口。顺便说一下，IANA——互联网号码分配机构（www.iana.org）——是负责协调 1,024 以下端口号分配的组织。

## 使用 xinetd 超级服务器

客户端/服务器架构的 Internet 服务要求服务器在客户端请求服务之前必须处于运行状态。一个简单的想法是始终运行所有服务器——这不切实际，因为每个服务器进程都会以内存和处理器时间的形式占用系统资源。此外，你并不需要所有服务始终处于运行和就绪状态。解决此问题的明智方案是运行单个服务器 xinetd，它监听所有端口，并在客户端请求到来时启动适当的服务器。（xinetd 服务器是名为 inetd 的旧服务器的替代品，提供改进的访问控制和日志记录。名称 xinetd 代表 extended inetd，即扩展 inetd。）

例如，当客户端尝试连接到 TELNET 端口时，xinetd 启动 TELNET 服务器并让其直接与客户端通信（并且当客户端断开连接时 TELNET 服务器退出）。

由于它按需启动各种服务器，xinetd 被称为 Internet 超级服务器。通常，UNIX 系统在启动时启动 xinetd。xinetd 服务器在启动时读取名为 /etc/xinetd.conf 的配置文件。该文件告诉 xinetd 监听哪些端口以及为每个端口启动什么服务器。该文件可以包含包含其他配置文件的指令。在 Red Hat Linux 中，/etc/xinetd.conf 文件如下所示：

```
# Simple configuration file for xinetd
#
# Some defaults, and include /etc/xinetd.d/
defaults
{
        instances       = 60
        log_type        = SYSLOG authpriv
        log_on_success  = HOST PID
        log_on_failure  = HOST
        cps             = 25 30
}
includedir /etc/xinetd.d
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_627_0.png)

注释行以井号（#）开头。属性的 defaults 块，由大括号（{...}）括起来，指定某些属性的默认值。这些默认值适用于配置文件中的所有其他服务。instances 属性设置为 60，这意味着对于任何服务，同时活跃的服务器最多为 60 个。

/etc/xinetd.conf 文件中的最后一行使用 includedir 指令包含 /etc/xinetd.d 目录中的所有文件，排除以句点（.）开头的文件。想法是 /etc/xinetd.d 目录将包含所有服务配置文件——为 xinetd 服务器预期管理的每种服务类型一个文件。

以下是我在典型的 Red Hat Linux 系统上输入 ls /etc/xinetd.d 命令时出现的 文件列表：

```
chargen      daytime-udp  imap   ktalk  rlogin  services  time
chargen-udp  echo         imaps  ntalk  rsh     sgi_fam   time-udp
cups-lpd     echo-udp     ipop2  pop3s  rsync   talk
 daytime     finger       ipop3  rexec  servers  telnet
```

这些文件中的每一个都指定一个服务的属性。例如，以下列表显示了 /etc/xinetd.d/telnet 文件的内容，该文件指定了 TELNET 服务的 xinetd 配置：

```
# description: The Telnet server serves Telnet sessions; it uses
# unencrypted username/password pairs for authentication.
service telnet
{
    flags           = REUSE
    socket_type     = stream
    wait            = no
    user            = root
    server          = /usr/sbin/in.telnetd
    log_on_failure  += USERID
    disable         = yes
}
```

文件名（在本例中为 telnet）可以是任意名称；重要的是文件中 service 关键字旁边出现的服务名称。在本例中，行 service telnet 告诉 xinetd 服务的名称。xinetd 使用此名称从 /etc/services 文件中查找端口号。要在 /etc/services 文件中查找 telnet，请键入以下命令：

```
grep "^telnet" /etc/services
```

该命令显示以下行：

```
telnet      23/tcp
telnet      23/udp
telnets     992/tcp
telnets     992/udp
```



列出以 telnet 开头的两行显示 TELNET 服务的端口号为 23。这告诉 xinetd，任何到达 23 端口的连接请求都是针对 TELNET 服务的。配置文件 /etc/xinetd.d/telnet 然后告诉 xinetd 如何处理这些服务请求。

/etc/xinetd.d/telnet 中的属性，用大括号括起来，具有以下含义：

- flags 属性提供了关于如何运行 xinetd 启动的服务器的具体说明。REUSE 标志意味着即使 xinetd 重启，服务也会保持运行。请注意，REUSE 标志现在被隐式假定为所有服务都已设置。
- socket_type 属性设置为 stream，这告诉 xinetd TELNET 服务使用面向连接的 TCP 套接字与客户端通信。对于使用无连接 UDP 套接字的服务，此属性将设置为 dgram。
- wait 属性设置为 no，这告诉 xinetd 为每个请求启动一个新服务器。如果此属性设置为 yes，xinetd 会等待服务器退出后才再次启动服务器。
- user 属性提供了 xinetd 用于运行服务器的用户 ID。在此情况下，服务器以 root 身份运行 TELNET 服务器。
- server 属性指定为此服务运行的程序。在此情况下，xinetd 运行 /usr/sbin/in.telnetd 程序以提供 TELNET 服务。
- disable 属性如果设置为 yes 则关闭服务。默认情况下 disable 属性设置为 yes，TELNET 被关闭。

浏览您 Red Hat Linux 系统上 /etc/xinetd.d 目录中的文件，以了解 xinetd 设置为启动的服务类型。其中一些服务，例如 finger，会提供入侵者可能用来入侵系统的信息。如果它们尚未被禁用，您可能希望通过在包含所有属性的大括号内放置以下行来关闭这些服务：

```
disable      = yes
```

另一方面，如果您似乎无法使用 telnet 连接到 Red Hat Linux 系统，请检查 /etc/xinetd.d 目录中的相应文件，并确保 disable 属性设置为 no，或者该行已被注释掉（通过在行首放置 # 将代码行更改为不运行的注释）。

当您对 xinetd 配置文件进行此类更改时，您必须通过键入以下命令重新启动 xinetd 服务器：

```
/etc/init.d/xinetd restart
```

如果您想输入更少的内容，请使用执行完全相同操作的以下命令：

```
service xinetd restart
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_629_0.png)

您还可以使用 chkconfig 命令禁用和启用由 xinetd 启动的服务。例如，要启用 TELNET 服务，以 root 身份登录并键入以下命令：

```
chkconfig telnet on
```

要再次关闭 TELNET，键入 chkconfig telnet off。

## 运行独立服务器

通过 xinetd 启动服务器是一种明智的方法，但如果服务必须经常启动，则效率不高。如果 Web 服务器由 xinetd 控制，您会遇到服务器经常启动的情况，因为每次用户点击网页时，都会为 Web 服务发出请求。对于此类高需求服务，最好以独立方式启动服务器，作为守护进程运行——一个持续运行且永不终止的进程。这意味着服务器监听分配的端口，每当请求到达时，服务器通过复制自身来处理它。这样，服务器只要机器在运行就会保持运行——理论上是永远。一种更高效的策略，用于 Web 服务器，是运行服务器的多个副本，让每个副本处理部分传入请求。

您可以轻松配置 Red Hat Linux 系统以自动启动各种独立服务器。我将在本节中向您展示如何操作。

## 手动启动和停止服务器

要启动未运行的服务，请使用服务器命令。例如，如果 Web 服务器（httpd）未运行，您可以通过运行以下命令的特殊 shell 脚本来启动它：

```
/etc/init.d/httpd start
```

该命令使用 `start` 作为参数运行 `/etc/init.d/httpd` 脚本。如果 `httpd` 服务器已在运行并且您想停止它，请使用 `stop` 作为参数运行相同的命令，如下所示：

```
/etc/init.d/httpd stop
```

要再次停止并启动服务器，只需使用 `restart` 作为参数：

```
/etc/init.d/httpd restart
```

Red Hat Linux 包含另一个名为 `service` 的脚本，它执行相同的任务，但更容易记住。基本上，您可以去掉 `/etc/init.d` 并将其替换为 `service` 后跟一个空格。因此，要启动 `httpd`，您应键入以下内容：

```
service httpd start
```

您能启动和停止的所有服务是什么？答案在 `/etc/init.d` 目录中的文件里。要查看它，请键入以下命令：

```
ls /etc/init.d
```

通过此命令列出的所有文件都是安装在 Red Hat Linux 系统上的服务——您可以根据需要启动和停止它们。例如，以下是 Red Hat Linux 系统上典型的服务列表：

```
aep1000 functions keytable nfs lock saslauthd tux
anacron gpm killall nscd sendmail vsftpd
apmd halt kudu ntpd single winbind
atd httpd lisa pcmcia smartd xfs
autofs lpd messagebus postgresql smb xinetd
bcm2... iptables named postfix smb xinetd
...
```

这超过 50 个服务！

## 启动时自动启动服务器

您可以使用 `/etc/init.d` 目录中的脚本手动启动、停止和重新启动服务器，但您希望某些服务在启动 Red Hat Linux 系统时立即启动。您可以使用 `chkconfig` 命令或图形服务器配置实用程序配置服务器在启动时自动启动。

## 使用 chkconfig 命令

chkconfig 程序是用于检查和更新 Red Hat Linux 中服务器当前设置的命令行实用程序。各种服务器组合被设置为在不同的运行级别自动启动。每个运行级别代表一种系统配置，其中选定的进程集运行。您通常关心运行级别 3 和 5，因为运行级别 3 用于文本模式登录，运行级别 5 用于通过图形界面登录。

chkconfig 命令使用简单。例如，假设您想在运行级别 3 和 5 自动启动 named 服务器。您所需要做的就是以 root 身份登录并在 shell 提示符下键入以下命令：

```
chkconfig --level 35 named on
```

要查看 named 服务器的状态，请键入以下命令：

```
chkconfig --list named
```

您应该会看到类似以下内容的输出行：

```
named 0:off 1:off 2:off 3:on 4:off 5:on 6:off
```

输出显示了运行级别 0 到 6 下 named 服务器的状态。如您所见，named 被设置为在运行级别 3 和 5 运行。

如果您想关闭 named，可以使用以下命令：

```
chkconfig --level 35 named off
```

您可以使用 chkconfig 查看所有服务的状态，包括通过 xinetd 启动的服务。例如，您可以通过键入以下命令查看所有服务的状态：

```
chkconfig --list | more
```

以下是典型的输出：

```
apm 0:off 1:off 2:on 3:on 4:on 5:on 6:off
kudzu 0:off 1:off 2:off 3:on 4:on 5:on 6:off
syslog 0:off 1:off 2:on 3:on 4:on 5:on 6:off
rawdevices 0:off 1:off 2:off 3:on 4:on 5:on 6:off
netfs 0:off 1:off 2:off 3:on 4:on 5:on 6:off
network 0:off 1:off 2:on 3:on 4:on 5:on 6:off
random 0:off 1:off 2:on 3:on 4:on 5:on 6:off
saslauthd 0:off 1:off 2:off 3:off 4:off 5:off 6:off
microcode_ctl 0:off 1:off 2:on 3:on 4:on 5:on 6:off
keytable 0:off 1:on 2:on 3:on 4:on 5:on 6:off
```

```
anacron    0:off 1:off 2:on 3:on 4:on 5:on 6:off
atd        0:off 1:off 2:off 3:on 4:on 5:on 6:off
irda       0:off 1:off 2:off 3:off 4:off 5:off 6:off
snmpd      0:off 1:off 2:off 3:off 4:off 5:off 6:off
... many lines of output deleted ...
```

输出显示了每个服务在 0 到 6 各运行级别的状态。对于每个运行级别，服务要么是 on 要么是 off。在列表的最后，chkconfig 显示 xinetd 控制的服务列表。每个基于 xinetd 的服务也标记为 on 或 off，具体取决于 xinetd 是否配置为启动该服务。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_632_0.png)

请注意，服务通常可以配置为在 xinetd 下运行或以独立方式运行。例如，在 8.1 版本之前，Red Hat Linux 使用 xinetd 控制启动 FTP 服务。然而，从 8.1 版本开始，非常安全的 FTP 服务器（vsftpd）被设置为独立服务器。如今，如果您必须启动 FTP 服务，请键入 service vsftpd start。要在启动时自动启动 FTP 服务，请键入 chkconfig vsftpd on。

## 使用 Red Hat 服务配置实用程序

如果您不喜欢键入 chkconfig 命令，您可以使用图形服务配置实用程序程序来配置服务。要运行服务配置实用程序，请以 root 身份登录并从 GNOME 或 KDE 桌面选择 主菜单→系统设置→服务器设置→服务。然后您可以从服务配置窗口打开或关闭服务（如图 1-2 所示）。

图 1-2：从服务配置窗口，您可以设置服务在启动时自动启动。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_632_1.png)



服务配置实用程序以滚动列表的形式显示服务名称。列表中的每一行都显示一个服务的名称，并在名称前有一个方框。方框中的复选标记表示该服务已被选中，以便在当前运行级别下启动时启动。首次出现对话框时，许多服务已被选中。

您可以上下滚动列表并单击方框以选择或取消选择服务。如果单击方框，复选标记会交替打开和关闭。要了解有关服务的更多信息，请单击服务名称，简要说明会出现在窗口右侧。例如，图 1-2 显示了 atd 服务的帮助文本。此外，该实用程序还会显示所选服务当前是否正在运行。

在选择系统启动时要启动的所有服务后，单击工具栏上的“保存”以保存更改。然后选择“文件→退出”以退出。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_633_0.png)

默认情况下，服务配置实用程序为当前运行级别配置所选服务。这意味着如果您从图形桌面执行此操作，系统处于运行级别 5，并且您配置的服务将设置为在运行级别 5 启动。如果您想为不同级别设置服务，请从“编辑运行级别”菜单中选择该运行级别。

表 1-1 显示了服务的列表以及每个服务的简要说明。第一列显示服务的名称，该名称与提供该服务所需运行的程序的名称相同。当您在系统上运行服务配置实用程序时，您可能看不到其中所有服务，因为服务的确切列表取决于安装在您的 Red Hat Linux 系统上的内容。

Table 1-1
Red Hat Linux 中的一些常见服务

| 服务名称 | 描述 |
|---|---|
| aep1000 | 加载并卸载名为 AEP1000 的加速加密处理卡的驱动程序，该卡可以快速进行加密（仅在系统已安装该卡时使用）。 |
| anacron | 执行按计划定期运行的命令。 |
| apmd | 监视高级电源管理（APM）BIOS 并记录电力状态（交流电或电池备份）。 |
| atd | 运行由 at 和 cron 命令安排的命令。 |
| autofs | 自动挂载文件系统（例如，当您将 CD-ROM 插入 CD-ROM 驱动器时）。 |

| 服务名称 | 描述 |
|---|---|
| bcm5820 | 加载并卸载 Broadcom 的 BCM5820 Cryptonet SSL（安全套接字层）加速芯片的驱动程序（仅在已安装硬件时使用此服务）。 |
| crond | 根据 crontab 命令设定的周期性计划运行用户指定的程序。 |
| cups | 运行通用 UNIX 打印系统（CUPS）守护进程（cupsd）。 |
| cups-lpd | 使应用程序能够使用旧版 LPD（行式打印机守护进程）协议与 CUPS 通信。 |
| finger | 回答 finger 协议请求（用于用户信息，例如登录名和上次登录时间）。您必须启用 xinetd 才能运行此服务。 |
| firstboot | 首次启动 Red Hat Linux 时运行，并允许您设置日期和时间、创建用户帐户、注册 Red Hat Network 并安装其他 CD-ROM。 |
| gpm | 启用在文本模式屏幕中使用鼠标。 |
| httpd | 这是 Apache 万维网（WWW）服务器。 |
| imap | 允许远程 IMAP（Internet 消息访问协议）客户端下载邮件消息。您必须启用 xinetd 才能运行此服务。 |
| imaps | 允许支持安全套接字层（SSL）的远程 IMAP（Internet 消息访问协议）客户端安全地下载邮件消息。您必须启用 xinetd 才能运行此服务。 |
| innd | 这是 InterNetNews 守护进程——您可用于在系统上支持本地新闻组的 Internet 新闻服务器。 |
| ipop3 | 允许远程 POP3（邮局协议版本 3）客户端下载邮件消息。您必须启用 xinetd 才能运行此服务。 |
| iptables | 使用 iptables 自动化数据包过滤防火墙。 |
| irda | 支持 Linux 中与 IrDA 兼容的红外设备的通信。（IrDA 是红外无线通信的标准，速度范围从 2400bps 到 4Mbps。） |
| irqbalance | 将中断分配给多处理器系统中的处理器，以在处理器之间平衡负载。 |
| isdn | 启动和停止 ISDN（综合业务数字网）服务——通过普通电话线路的数字通信服务（仅在您拥有 ISDN 服务时启用）。 |
| keytable | 按 /etc/sysconfig/keyboard 文件中指定的方式加载所选键盘映射。您应让此服务在系统上保持运行。 |
| kudzu | 探测新硬件并配置已更改的硬件。 |

## 表 1-1（续）

| 服务名称 | 描述 |
|---|---|
| lisa | 启动和停止 LAN 信息服务器（LISa）守护进程，该守护进程可以通过在 TCP 端口 7741 广播来显示局域网（LAN）中主机信息。欲了解有关 LISa 的更多信息，请访问 lisa-home.sourceforge.net。 |
| messagebus | 运行 D-BUS 守护进程，使应用程序能够接收系统事件的通知，例如新硬件设备的添加。欲了解有关 D-BUS 的更多信息，请参阅 www.freedesktop.org/software/dbus/。 |
| named | 这是域名系统（DNS）的服务器，可将主机名转换为 IP 地址。如果您愿意，可以在系统上运行一个副本。 |
| netfs | 使您能够挂载和卸载所有网络文件系统（NFS、Samba 和 Netware）。 |
| network | 使您能够激活或停用配置为在系统启动时启动的所有网络接口。 |
| nfs | 使用网络文件系统（NFS）协议启用在 /etc/exports 文件中指定的文件系统的共享。 |
| nfslock | 为使用网络文件系统（NFS）协议导出的文件系统提供文件锁定功能，以便其他系统（运行 NFS）可以共享您系统上的文件。 |
| ntalk | 提供与不同系统上的用户聊天的支持。 |
| ntpd | 这是网络时间协议版本 4（NTPv4）的服务器，用于同步网络中计算机的时钟。 |
| pcmcia | 提供 PCMCIA 设备的支持。 |
| pop3s | 允许支持 SSL 的远程 POP3（邮局协议版本 3）客户端安全地下载邮件消息。您必须启用 xinetd 才能运行此服务。 |
| portmap | 由依赖远程过程调用（RPC）的任何软件使用的服务器。例如，NFS 需要 portmap 服务。 |
| postgresql | 启动或停止处理数据库请求的 PostgreSQL 服务器。（PostgreSQL 是随 Red Hat Linux 提供的免费数据库。） |
| pxe | 用于通过网络启动其他系统的预启动执行环境（PXE）的服务器。 |
| random | 在 Red Hat Linux 系统上生成高质量随机数所需的服务器。 |
| rawdevices | 将原始设备分配给块设备（例如 Oracle 等应用程序所需）。 |
| rexec | 支持基于用户名和密码身份验证的远程执行。您必须启用 xinetd 才能运行此服务。 |

| 服务名称 | 描述 |
|---|---|
| rhnsd | 定期连接到 Red Hat Network Services 服务器以检查更新和通知。 |
| rlogin | 支持远程登录的服务器。您必须启用 xinetd 才能运行此服务。 |
| rsh | 支持远程执行命令的服务器。您必须启用 xinetd 才能运行此服务。 |
| rsync | 支持远程复制文件的服务器。您必须启用 xinetd 才能运行此服务。 |
| saslauthd | 使用 Cyrus-SASL（简单身份验证和安全层）软件支持身份验证。 |
| sendmail | 将邮件消息从一台机器移动到另一台机器。如果您想从 Red Hat Linux 系统发送邮件，请启动此服务。如果您不打算将 Red Hat Linux 系统用作邮件服务器，请不要启动 sendmail 服务器，因为它会减慢启动过程并消耗不必要的资源。 |
| sgi_fam | 实现文件更改监视器（FAM），可用于在文件更改时获取报告。 |
| smb | 启动和停止 Samba smbd 和 nmbd 服务，这些服务在 Red Hat Linux 系统上支持 LAN Manager 服务。 |
| snmpd | 用于网络管理功能的简单网络管理协议（SNMP）服务。 |
| squid | 用于 Internet 对象的缓存服务器——任何可通过 HTTP 和 FTP 访问的内容。 |
| sshd | OpenSSH（安全 Shell）安全远程登录设施的服务器。 |
| syslog | 由许多其他程序（包括其他服务）使用的服务，用于在日志文件（通常是 /var/log/messages 文件）中记录各种错误和状态消息。您应始终运行此服务。 |
| talk | 支持与其它系统上的用户聊天的服务器。您必须启用 xinetd 才能运行此服务。 |
| telnet | 支持 TELNET 远程登录会话的服务器。您必须启用 xinetd 才能运行此服务。 |
| tux | 这是基于内核的 HTTP 服务器。 |
| vsftpd | 用于通过文件传输协议（FTP）进行文件传输的非常安全的 FTP 守护进程。 |
| winbind | 启动和停止 Samba winbindd 服务器，该服务器提供与 /etc/nsswitch.conf 文件提供的名称切换功能类似的功能。 |
| xfs | 启动和停止 X 字体服务器的服务器。 |



**表 1-1（续）**

| 服务名称 | 描述 |
|---|---|
| xinetd | 这是 Internet 超级服务器，是旧的 inetd 的替代品。它在需要时启动其他 Internet 服务，例如 TELNET 和 FTP。 |
| yppasswdd | 网络信息系统 (NIS) 中密码更改所需的服务。除非使用 NIS，否则无需启动 yppasswdd。 |
| ypserv | 网络信息系统 (NIS) 的服务器。除非使用 NIS，否则无需启动 ypserv。 |
| ypxfrd | 一个帮助 ypserv 的服务器。仅在使用网络信息系统 (NIS) 时才启动此服务。 |

### 第 2 章：运行 Apache Web 服务器

### 本章内容

- 探索 HTTP
- 安装 Apache Web 服务器
- 配置 Apache Web 服务器
- 使用 Apache Web 服务器支持虚拟主机

万维网 (WWW 或 Web) 因 Web 浏览器使用户能够轻松浏览存储在各种 Internet 主机上的文档而使 Internet 进入主流。无论您经营小型企业还是为大型公司管理计算机系统和网络，很可能您需要设置和维护一个 Web 服务器。由于内置网络支持，Red Hat Linux PC 是一款经济实惠的 Web 服务器。本章描述如何在 Red Hat Linux PC 上配置 Apache Web 服务器。

### 探索 HTTP

Web 服务器使用 HTTP 提供信息。Web 服务器也称为 HTTP 守护进程（因为在 UNIX 中连续运行的服务器进程称为守护进程），简称为 HTTPD。Web 服务器程序（例如随 Red Hat Linux 提供的 Apache Web 服务器）通常命名为 httpd。

HTTP 代表 HyperText Transfer Protocol。HyperText 部分指的是 Web 页面包含超文本链接。Transfer Protocol 部分指的是通过网络从一台计算机向另一台计算机传输 Web 页面的标准约定。虽然您实际上不必了解 HTTP 即可设置 Web 服务器或使用 Web 浏览器，但了解其工作原理有助于您理解 Web 的工作方式。

您可以通过使用 TELNET 程序连接到 Web 服务器监听的端口来亲身体验 HTTP。在大多数系统上，Web 服务器监听端口 80 并响应发送到该端口的任何 HTTP 请求。因此，您可以使用 TELNET 程序连接到具有 Web 服务器的系统的端口 80 并尝试一些 HTTP 命令。

### HTTP 是 Internet 标准吗？

尽管自 1990 年以来在 Web 上广泛使用，HTTP 直到最近才成为 Internet 标准。所有 Internet 标准首先以请求评论 (RFC) 的形式发布。第一个与 HTTP 相关的 RFC 是 RFC 1945，“HyperText Transfer Protocol — HTTP/1.0”（T. Berners-Lee、R. Fielding 和 H. Frystyk，1996 年 5 月）。然而，RFC 1945 被视为信息性文件，而不是标准。

RFC 2616，“HyperText Transfer Protocol — HTTP/1.1”（R. Fielding、J. Gettys、J. Mogul、H. Frystyk、L. Masinter、P. Leach、T. Berners-Lee，1999 年 6 月）是 HTTP 的草案 Internet 标准。

要阅读这些 RFC，请将您的 Web 浏览器指向 www.rfc-editor.org/rfc.html 或 www.cis.ohio-state.edu/htbin/rfc/rfc-index.html。

要了解有关 HTTP/1.1 和其他 Web 相关标准的更多信息，请使用 Web 浏览器访问 www.w3.org/pub/WWW/Protocols/。

要查看 HTTP 工作的示例，请按照以下步骤操作：

1. **确保您的 Linux PC 的 Internet 连接已启动并运行。**
   如果您使用 SLIP 或 PPP，例如，请确保您已建立连接。
   
2. **输入以下命令：**
   ```
   telnet www.gao.gov 80
   ```
   
3. **在看到 Connected... 消息后，输入以下 HTTP 命令，然后按两次 Enter：**
   ```
   GET / HTTP/1.0
   ```
   
   作为对该 HTTP 命令的响应，Web 服务器返回一些有用信息，然后是默认 HTML 文件的内容（通常称为 index.html）。

以下是我在美国总审计办公室网站上尝试 GET 命令时得到的结果：

```
Trying 161.203.16.2...
Connected to www.gao.gov.
Escape character is "^]".
Date: Sun, 13 Jul 2003 17:49:23 GMT
Server: Apache
Connection: close
Content-Type: text/html

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN"
"http://www.w3.org
/TR/REC-html40/loose.dtd>
<HTML>
<HEAD>
<TITLE>The United States General Accounting Office</TITLE>
..... (lines deleted)
</HEAD>
.....
(lines deleted)
</BODY>
</html>
```

Connection closed by foreign host.

当您使用 TELNET 尝试此示例时，您会看到 Web 服务器发送回 Web 浏览器的确切内容。前几行是供浏览器使用的管理信息。服务器返回此信息：

- 一行显示服务器使用 HTTP 协议版本 1.1 和表示成功的 200 状态代码：
  `HTTP/1.1 200 OK`
- 当前日期和时间。示例日期和时间字符串如下所示：
  `Date: Sun, 13 Jul 2003 17:49:23 GMT`
- Web 服务器软件的名称。例如，对于运行 Apache Web 服务器的站点，服务器返回以下字符串：
  `Server: Apache`
- Web 服务器返回的文档类型。对于 HTML 文档，内容类型报告如下：
  `Content-type: text/html`

服务器抑制版本号和其他详细信息，以便黑客无法轻易利用 Apache Web 服务器特定版本中已知的漏洞。

文档本身跟在管理信息之后。HTML 文档具有以下一般布局：

```
<title>Document's title goes here</title>
<html>
<body optional attributes go here >
...The rest of the document goes here
</body>
</html>
```

您可以通过查看显示 Web 服务器响应 GET 命令的列表来识别此布局。由于示例使用 telnet 命令获取文档，您会看到 HTML 内容

作为文本行。如果您使用 Web 浏览器（例如 Mozilla）访问同一网站（www.gao.gov），您将以图形形式（见图 2-1）看到该页面。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_641_0.png)

图 2-1：
使用 Mozilla Web 浏览器查看的 www.gao.gov 网站。

HTTP 命令的示例显示了 GET 命令的结果。GET 是最常见的 HTTP 命令；它导致服务器返回指定的 HTML 文档。

另外两个 HTTP 命令是 HEAD 和 POST。HEAD 命令几乎与 GET 相同：它导致服务器返回文档中除正文外的所有内容。POST 命令向服务器发送信息；服务器自行决定如何处理这些信息。

### 探索 Apache Web 服务器

您可能已经知道使用 Web 的感觉，但您可能不知道如何设置 Web 服务器，以便您也可以通过网页向世界提供信息。要成为 Web 上的信息提供者，您必须在 Internet 上的 Red Hat Linux PC 上运行 Web 服务器。您还必须为您的网站准备网页——这项任务可能比 Web 服务器设置更具挑战性。

### 安装 Apache Web 服务器

在可用的 Web 服务器中，Apache Web 服务器是最受欢迎的，并且随 Red Hat Linux 提供。Apache Web 服务器最初是 NCSA HTTPD 服务器的改进版本，但很快发展成为一个独立的开发工作。与 NCSA HTTPD 一样，Apache 服务器由一群协作者开发和维护。Apache 可在 Internet 上免费获得。

根据 Red Hat Linux 安装选项，Apache Web 服务器可能已安装在您的系统上。要查找是否已安装，请输入以下命令：

```
rpm -q httpd
```

如果 Web 服务器已安装，您应该看到如下输出：

```
httpd-2.0.45-14
```

如果您收到 httpd 未安装的消息，则可以使用本书的配套 DVD 轻松安装，按以下步骤操作：

1. 以 root 身份登录并将 DVD 插入 DVD 驱动器。
   如果您使用 GNOME 或 KDE 图形桌面，DVD 应该会自动挂载。如果没有，输入命令 mount /dev/cdrom 来挂载 DVD。
2. 输入以下命令安装 Apache Web 服务器：
   ```
   cd /mnt/cdrom/RedHat/RPMS
   rpm -ivh httpd*
   ```

就这样！您现在可以运行 Apache Web 服务器。

### 启动 Apache Web 服务器

即使 Apache Web 服务器已安装，它可能未设置为在启动时启动。如果您想尝试使用它，您必须启动服务器。为此，以 root 身份登录并输入以下命令：

```
service httpd start
```

要查看 httpd 进程（httpd 是 Apache Web 服务器程序的名称）是否正在运行，请输入以下命令：

```
ps ax | grep httpd
```



## 为什么它叫做 Apache？

根据 www.apache.org/foundation/faq.html 上关于 Apache Web 服务器项目的信息，Apache 组织由一批在 1995 年 3 月提供用于修复 NCSA HTTPd 1.3 错误的补丁文件的人组成。应用补丁到 NCSA HTTPd 后的结果被他们称为 patchy server（这就是 Apache 这个名字来源）。Apache 组织现已发展为 Apache 软件基金会（ASF），这是一个非营利公司，于 1999 年 6 月在美国特拉华州注册成立。ASF 有许多其他正在进行中的项目。你可以在 www.apache.org 上阅读这些项目。特别是，访问 httpd.apache.org 以获取有关 Apache Web 服务器项目的更多信息。

根据 news.netcraft.com/archives/web_server_survey.html 上 2003 年 7 月的 Netcraft Web 服务器调查，Apache Web 服务器是最受欢迎的——据报道有 63.72% 的 42,298,371 个站点使用 Apache 服务器。微软 Internet Information Server（IIS）遥居第二，占 25.95% 的站点。

输出应显示多个 httpd 进程。运行多个 Web 服务器进程是一种常见做法——一个父进程和多个子进程——这样可以通过为每个请求分配一个 httpd 进程来高效处理多个 HTTP 请求。

如果没有 httpd 进程，Apache 配置文件可能潜藏着错误。如果是这种情况，应该会出现一些错误消息，给出错误原因的线索。你必须在配置文件中修复问题并重新启动服务器。

如果 httpd 进程正在运行，你可以使用 TELNET 程序来检查它是否工作，但首先你必须在 /var/www/html 目录中添加一个默认主页。如果你没有时间准备一个，复制在出现错误时应发送的网页。以下是你以 root 登录时输入的命令来获取它：

```
cp /var/www/error/noindex.html /var/www/html/index.html
```

现在你有了默认主页，你可以在终端窗口中输入以下命令来检查 Web 服务器是否工作：

```
telnet localhost 80
```

收到 Connected 消息后，输入

```
HEAD / HTTP/1.0
```

然后按两次 Enter。你应该会得到类似以下的响应（日期和数字当然会不同）：

```
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
HTTP/1.1 200 OK
Date: Sun, 13 Jul 2003 18:11:11 GMT
Server: Apache/2.0.45 (Red Hat Linux)
Last-Modified: Sun, 13 Jul 2003 18:10:15 GMT
ETag: "bdf93-b52-b7b3efc0"
Accept-Ranges: bytes
Content-Length: 2898
Connection: close
Content-Type: text/html; charset=UTF-8

Connection closed by foreign host.
```

响应显示了有关 Web 服务器和默认主页的一些信息。你也可以使用在 Red Hat Linux 系统上运行的 Mozilla 等 Web 浏览器来检查 Web 服务器。例如，如果你的系统 IP 地址是 192.168.0.5，使用 URL http://192.168.0.5/ 看看会发生什么。你应该会看到一个标题为 "Test Page for the Apache Web Server on Red Hat Linux." 的网页。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_644_0.png)

如果你想在启动时自动启动 Apache Web 服务器，输入以下命令进行设置：

```
chkconfig --levels 35 httpd on
```

## 配置 Apache Web 服务器

Red Hat Linux 配置 Apache Web 服务器软件使用以下目录：

- Web 服务器程序 — httpd — 安装在 /usr/sbin 目录中。
- Apache Web 服务器配置文件 — httpd.conf — 位于 /etc/httpd/conf 目录中。配置文件是一个文本文件，其中包含指令指定 Web 服务器的各个方面。/etc/httpd/conf 目录还包含有关安全套接字层（SSL）实现需求的信息。（SSL 实现是 Apache Web 服务器的一部分。）
- Apache Web 服务器设置为从 /var/www/html 目录提供 HTML 文档。因此你应该将你的网页放在此目录中。
- 如果你有任何通用网关接口（CGI）程序——Web 服务器可以调用的程序来访问其他文件和数据库——你应该将它们放在 `/var/www/cgi-bin/` 目录中。
- `/var/log/httpd` 目录用于 Web 服务器日志文件（访问日志和错误日志）。
- `/etc/init.d/httpd` 脚本在你的 Red Hat Linux 系统启动时启动 `httpd` 进程，前提是你已使用 `chkconfig` 命令启用它。

## 使用 Apache 配置工具

Red Hat Linux 附带一个图形配置工具，可用于配置 Apache Web 服务器。要运行此配置工具，以 root 登录并从 GNOME 桌面选择 主菜单→系统设置→服务器设置→HTTP 服务器。Apache 配置对话框出现（如图 2-2 所示）。

Figure 2-2:
你可以从此配置窗口配置 Apache HTTP 服务器。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_645_0.png)

Apache 配置对话框分为四个选项卡。你可以从每个选项卡设置各种选项：

- **Main:** 从此选项卡你可以指定 Apache 应期望 Web 服务请求的 IP 地址和端口号。你还可以设置网站管理员的电子邮件地址。
- **Virtual Hosts:** 在这里你可以设置虚拟主机。我将在本章后面讨论虚拟主机的选项。你还可以编辑适用于所有虚拟主机的默认设置。单击虚拟主机选项卡中的编辑默认设置按钮会弹出另一个对话框（如图 2-3 所示），从中你可以设置许多不同的选项。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_646_0.png)

Figure 2-3: 你可以从此配置窗口配置虚拟主机属性。

- **Server:** 此选项卡具有服务器设置，例如 HTTP 服务器应运行的用户和组名称以及存储进程 ID 的文件位置。
- **Performance Tuning:** 在此选项卡你可以设置控制整体性能的一些参数。你可以设置允许的最大连接数、连接的超时时间以及每个连接的最大请求数。

最初配置窗口显示配置文件 `/etc/httpd/conf/httpd.conf` 中的默认值。进行任何更改后，单击确定按钮。配置工具会提示你是否真的要保存更改并退出。如果是，单击是，你就完成了。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_646_1.png)

当你从此配置工具配置 Apache HTTP 服务器时，你所做的只是更改存储在 `/etc/httpd/conf/httpd.conf` 文件中的选项和属性。你也可以通过编辑配置文件（这是一个纯文本文件）轻松地进行更改。在下一节中，我将向你介绍 Apache 配置文件中的一些常见配置指令。

## Apache 配置文件

Apache 服务器的操作由位于 `/etc/httpd/conf` 目录中的 `httpd.conf` 配置文件控制。此文件控制服务器如何运行、提供哪些文档以及谁可以访问这些文档。

在接下来的几节中，我总结了有关 `httpd.conf` 配置文件的重要信息。通常，你不需要更改配置文件中的任何内容即可运行 Apache Web 服务器。然而，了解

配置文件的格式以及其中使用的各种关键字的含义是有用的。

在研究 `/etc/httpd/conf` 目录中的配置文件时，请记住以下语法规则：

- 每个配置文件都是一个文本文件，你可以用喜欢的文本编辑器编辑并用 `more` 命令查看。
- 所有注释行都以 `#` 开头。
- 每行只能有一个指令。
- 额外的空格和空行会被忽略。
- 除路径名和 URL 外，所有条目都不区分大小写。

## httpd.conf 配置文件

`/etc/httpd/conf/httpd.conf` 文件是主要的 HTTP 守护进程配置文件——它包含控制 Apache Web 服务器如何运行的指令。例如，`httpd.conf` 文件指定服务器使用的端口号、网站名称以及在服务器出现任何问题时发送邮件的电子邮件地址。此外，`httpd.conf` 还包含有关网页位置以及谁可以访问哪些目录的信息。

在以下各节中，我将 Apache 指令分为三个类别呈现：通用 HTTPD 指令、资源配置指令和访问控制指令。最后，我将解释如何在 Apache Web 服务器中设置虚拟主机，以便单个 Web 服务器可以处理发送到多个 IP 地址或主机名的 Web 请求。

## 通用 HTTPD 指令

`httpd.conf` 文件中的一些有趣项目是

- `ServerName` 指定你的网站的主机名（形式为 `www.your.domain`）以及 Web 服务器接受连接的端口号。`ServerName` 仅在将网页重定向到另一个网页时使用。名称应为已注册的域名，其他用户可通过其名称服务器找到。以下是示例：
  
  ```
  ServerName www.myhost.com:80
  ```
  
  如果你没有注册的域名，使用你的 Red Hat Linux 系统的 IP 地址。
- `ServerAdmin` 是 Web 服务器在发生任何错误时提供给客户端的电子邮件地址。`ServerAdmin` 的默认值是 `root@localhost`。你应该将其设置为有效的电子邮件地址，任何互联网用户都可以使用它来报告你的网站中的错误。



Apache Web 服务器的工作方式由更多指令控制。以下列表总结了可在 httpd.conf 文件中使用的一些指令。你可以让大多数这些指令保持默认设置，但如果你在维护 Web 服务器，了解它们是很重要的。

- **Listen IP-Address:Port** — 强制 Web 服务器监听特定的 IP 地址和端口号。默认情况下，Web 服务器响应与主机关联的所有 IP 地址。
- **User name [ #id ]** — 指定 HTTP 守护进程使用的用户名（或 ID）。你可以将此指令保持在默认设置（apache）。如果指定用户 ID，请为数字 ID 使用哈希（#）前缀。
- **Group name [ #id ]** — 指定独立模式下 HTTP 守护进程的组名（或 ID）。默认组名是 apache。
- **ServerRoot pathname** — 指定 Web 服务器所在的目录。默认情况下，配置文件和日志文件预计位于此目录的子目录中。在 Red Hat Linux 中，ServerRoot 设置为 /etc/httpd。
- **ServerName www.company.com:80** — 将服务器的主机名设置为 www.company.com，端口号设置为 80。ServerName 仅在将网页重定向到另一个页面时使用。
- **StartServers num** — 设置 Apache Web 服务器启动时立即启动的子进程数。默认值是 8。
- **MaxSpareServers num** — 设置空闲子服务器进程的期望最大数量（如果子进程未处理 HTTP 请求，则认为其处于空闲状态）。默认值是 20。
- **MinSpareServers num** — 设置空闲子服务器进程的期望最小数量（如果子进程未处理 HTTP 请求，则认为其处于空闲状态）。如果数量低于此阈值，每秒会创建一个新的备用进程。默认值是 5。
- **Timeout numsec** — 设置服务器在客户端建立连接后等待客户端发送查询的秒数。默认超时为 300 秒（五分钟）。
- **ErrorLog filename** — 设置 httpd 记录其遇到的错误的文件。如果文件名不以斜杠（/）开头，则名称被视为相对于 ServerRoot。默认的 ErrorLog 是 /etc/httpd/logs/error_log，但 /etc/httpd/logs 是指向 /var/log/httpd 目录的符号链接。因此日志文件位于 /var/log/httpd 目录中。典型的错误日志条目包括服务器重启等事件以及任何警告消息，例如以下内容：

```
[Sun Jul 13 14:10:34 2003] [notice] Apache/2.0.45 (Red Hat Linux) configured -- resuming normal operations
[Sun Jul 13 15:47:03 2003] [error] [client 192.168.0.2] File does not exist: /var/www/html/sample.html
```

- **TransferLog filename** — 设置 httpd 记录所有客户端访问（包括失败的访问）的文件。默认的 TransferLog 是 `/var/log/httpd/access_log`。以下示例显示了典型访问在此日志文件中的记录方式：

```
192.168.0.2 - - [13/Jul/2003:15:46:56 -0400] "GET / HTTP/1.1" 200 2898
"" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)"
192.168.0.2 - - [13/Jul/2003:15:46:56 -0400] "GET /icons/apache_pb.gif HTTP/1.1" 200 2326 "http://192.168.0.6/" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)"
192.168.0.2 - - [13/Jul/2003:15:46:56 -0400] "GET /icons/powered_by.gif HTTP/1.1" 200 581 "http://192.168.0.6/" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)"
```

- **LogFormat formatstring formatname** — 指定 TransferLog 日志条目的格式。此格式也由 CustomLog 指令用于以特定格式生成日志。
- **CustomLog filename formatname** — 设置自定义日志文件的名称，其中 httpd 以 formatname 指定的格式记录所有客户端访问（包括失败的访问）（你使用 LogFormat 指令定义该格式）。
- **PidFile filename** — 设置 HTTPD 存储其进程 ID 的文件。默认的 PidFile 是 `/var/run/httpd.pid`。你可以使用此信息来终止或重启 HTTP 守护进程。以下示例显示了如何重启 httpd：

```
kill -HUP `cat /var/run/httpd.pid`
```

- **MaxClients num** — 设置可以同时连接到服务器的客户端数量的限制。默认值是 150。MaxClients 的值不能超过 256。
- **LoadModule module modules/modfile.so** — 加载作为动态共享对象（DSO）构建的模块。你必须指定模块名称和模块的对象文件。由于模块加载的顺序很重要，你应将这些指令保持为默认配置文件中的显示方式。注意 mod_ssl 模块提供了使用安全套接字层（SSL）协议进行加密的支持。

## 资源配置指令

资源配置指令指定网页的位置，以及如何指定各种文件的数据类型。入门时，你可以让指令保持默认设置。以下是 Apache Web 服务器的一些资源配置指令：

- **DocumentRoot pathname** — 指定 HTTP 服务器查找网页的目录。在 Red Hat Linux 中，默认的 DocumentRoot 是 `/var/www/html`。如果将 HTML 文档放在另一个目录中，请将 DocumentRoot 设置为该目录。
- **UserDir dirname** — 指定在 URL 中出现用户名时 HTTP 服务器查找网页的用户主目录下的子目录（例如在 URL http://www.psn.net/~naba 中，其中包含带波浪线前缀的用户名）。默认情况下，通过将 dirname 设置为 disable 来关闭 UserDir 功能。如果要启用它，可以将其设置为 public_html，这意味着用户的网页位于该用户主目录的 public_html 子目录中。
- **DirectoryIndex filename1 filename2 ...** — 指示当客户端未指定文档时服务器返回的默认文件或文件。默认的 DirectoryIndex 是 index.html。如果 httpd 未找到此文件，它会返回该目录的索引（基本上是该目录的文件的漂亮列表），前提是允许对该目录进行索引。
- **AccessFileName filename** — 指定可能出现在每个包含文档的目录中的文件名称，并指示谁有权访问该目录的内容。默认的 AccessFileName 是 .htaccess。此文件的语法与 Apache 访问控制指令的语法相同，我将在下一节中讨论这些指令。
- **AddType type/subtype extension** — 将文件扩展名与 MIME 数据类型（形式为 type/subtype，如 text/plain 或 image/gif）关联。因此，要让服务器将 .lst 扩展名的文件视为纯文本文件，请指定以下内容：

```
AddType text/plain .lst
```

默认的 MIME 类型和扩展名列在 /etc/mime.types 文件中。
- **AddEncoding type extension** — 将编码类型与文件扩展名关联。要让服务器将以 .gz 或 .tgz 结尾的文件标记为使用 x-gzip 编码方法编码（GZIP 编码的标准名称），请指定以下内容：

```
AddEncoding x-gzip gz tgz
```

- **DefaultType type/subtype** — 指定服务器在无法从文件扩展名确定类型时应使用的 MIME 类型。如果未指定 DefaultType，HTTPD 会假定 MIME 类型为 text/html。在默认的 httpd.conf 文件中，DefaultType 指定为 text/plain。
- **Redirect requested-file actual-URL** — 指定对 requested-file 的任何请求都应重定向到 actual-URL。
- **Alias requested-dir actual-dir** — 指定服务器使用 actual-dir 来定位 requested-dir 目录中的文件（换句话说，requested-dir 是 actual-dir 的别名）。要让对 /icons 目录的请求转到 /var/www/icons，请指定以下内容：

```
Alias /icons/ /var/www/icons/
```

- **ScriptAlias** `requested-dir actual-dir` — 指定用于通用网关接口（CGI）脚本的目录的实际名称。默认配置文件包含此指令：
```
ScriptAlias /cgi-bin/ "/var/www/cgi-bin/"
```
此指令意味着当 Web 浏览器请求脚本，例如 `/cgi-bin/test-cgi` 时，HTTP 服务器运行脚本 `/var/www/cgi-bin/test-cgi`。
- **DefaultIcon** `iconfile` — 指定服务器应为没有图标信息的文件使用的默认图标的位置。默认情况下，DefaultIcon 为 `/icons/unknown.gif`。
- **ReadmeName** `filename` — 指定 README 文件的名称，其内容会添加到自动生成的目录列表末尾。默认 ReadmeName 为 README。
- **HeaderName** `filename` — 指定头文件名称，其内容会添加到自动生成的目录列表前面。默认 HeaderName 为 HEADER。
- **AddDescription** `"file description" filename` — 指定在目录列表中将文件描述字符串显示在指定文件名旁边。您可以使用通配符，例如 `*.html`，作为文件名。例如，以下指令将以 `.tgz` 结尾的文件描述为 GZIP 压缩的 tar 归档：
```
AddDescription "GZIP compressed tar archive" .tgz
```
- **AddIcon** `iconfile extension1 extension2 ...` — 将图标与一个或多个文件扩展名关联。以下指令将图标文件 `/icons/text.gif` 与文件扩展名 `.txt` 关联：
```
AddIcon /icons/text.gif .txt
```
- **AddIconByType** `iconfile MIME-types` — 将图标与作为 MIME 类型通配符形式指定的文件类型组关联（如 `text/*` 或 `image/*`）。要将图标文件 `/icons/text.gif` 与所有文本类型关联，请指定以下内容：
```
AddIconByType (TXT,/icons/text.gif) text/*
```
此指令还告诉服务器为无法接受图像的客户端使用 TXT 代替图标。（浏览器会告诉服务器它们可以接受的数据类型。）
- **AddIconByEncoding** `iconfile encoding1 encoding2 ...` — 指定为一种或多种编码类型（如 `x-compress` 或 `x-gzip`）显示的图标。
- **IndexIgnore** `filename1 filename2 ...` — 指示服务器在准备目录列表时忽略指定的文件名（它们通常包含通配符）。要排除 README、HEADER 以及名称以句点 (.) 开头、以波浪号 (~) 结尾或以井号 (#) 结尾的所有文件，请指定以下内容：
```
IndexIgnore .??* *~ # HEADER* README* RCS CVS *,v *,.t
```
IndexOptions option1 option2 ... — 表示您希望服务器准备的目录列表中的选项。选项可以包括以下一项或多项：
- FancyIndexing 打开花哨的目录列表，其中包含文件名和表示文件类型、大小和最后修改日期的图标。
- IconHeight=N 指定图标高度为 N 像素。
- IconWidth=N 指定图标宽度为 N 像素。
- NameWidth=N 使文件名列宽为 N 个字符。
- IconsAreLinks 使图标像链接一样工作。
- ScanHTMLTitles 显示 HTML 文件的描述。
- SuppressHTMLPreamble 不向头文件（由 HeaderName 指令指定）添加标准 HTML 前言。
- SuppressLastModified 停止显示最后修改日期。
- SuppressSize 停止显示文件大小。
- SuppressDescription 停止显示任何文件描述。
- SuppressColumnSorting 阻止列标题成为可用于排序列的链接。

ErrorDocument errortype filename — 指定服务器在发生特定类型错误时应发送的文件。您也可以为错误提供文本消息。以下是一些示例：
```
ErrorDocument 403 "Sorry, no access to this directory"
ErrorDocument 403 /error/noindex.html
ErrorDocument 404 /cgi-bin/bad_link.pl
ErrorDocument 401 /new_subscriber.html
```
如果没有 ErrorDocument 指令，服务器会发送内置错误消息。errortype 可以是以下 HTTP/1.1 错误条件之一（有关更多信息，请参阅 RFC 2616 at www.ietf.org/rfc/rfc2616.txt or www.cis.ohio-state.edu/htbin/rfc/rfc2616.html）：
- 400 — Bad Request
- 401 — Unauthorized
- 402 — Payment Required
- 403 — Forbidden
- 404 — Not Found
- 405 — Method Not Allowed
- 406 — Not Acceptable
- 407 — Proxy Authentication Required
- 408 — Request Timeout
- 409 — Conflict
- 410 — Gone
- 411 — Length Required
- 412 — Precondition Failed
- 413 — Request Entity Too Large
- 414 — Request URI Too Long
- 415 — Unsupported Media Type
- 416 — Requested Range Not Satisfiable
- 417 — Expectation Failed
- 500 — Internal Server Error
- 501 — Not Implemented
- 502 — Bad Gateway
- 503 — Service Unavailable
- 504 — Gateway Timeout
- 505 — HTTP Version Not Supported

TypesConfig filename — 指定包含文件扩展名到 MIME 数据类型映射的文件。（MIME 代表 Multipurpose Internet Mail Extensions，即在单个消息文件中打包附件的一种方式。）服务器向客户端报告这些 MIME 类型。如果未指定 TypesConfig 指令，HTTPD 假定 TypesConfig 文件为 /etc/mime.types。以下是默认 /etc/mime.types 文件中的几行选定内容：
```
application/msword          doc
application/pdf             pdf
application/postscript      ai eps ps
application/x-tcl           tcl
audio/mpeg                  mpga mp2 mp3
audio/x-pn-realaudio        ram rm
audio/x-wav                 wav
```

| MIME Type | Extensions |
|---|---|
| image/gif | gif |
| image/jpeg | jpeg jpg jpe |
| image/png | png |
| text/html | html htm |
| text/plain | asc txt |
| video/mpeg | mpeg mpg mpe |

每行显示 MIME 类型（如 text/html），后跟该类型的扩展名（html 或 htm）。

## 访问控制指令

访问控制指令使您能够控制谁可以访问系统中的不同目录。这些是全局访问配置指令。您还可以在 Apache Web 服务器可以提供文档的每个目录中使用 AccessFileName 指令指定的名称的另一个访问配置文件。（该每个目录的访问配置文件默认名为 .htaccess。）

去掉大部分注释行后，访问控制指令的格式如下：
```
# First, we configure the "default" to be a
# very restrictive set of permissions.
<Directory />
    Options FollowSymLinks
    AllowOverride None
</Directory>

# The following directory name should
# match DocumentRoot in httpd.conf
<Directory /var/www/html>
    Options Indexes FollowSymLinks
    AllowOverride None
    order allow,deny
    allow from all
</Directory>

# The directory name should match the
# location of the cgi-bin directory
<Directory "/var/www/cgi-bin">
    AllowOverride None
    Options None
    Order allow,deny
    Allow from all
</Directory>
```

访问控制指令使用与其他 Apache 指令不同的语法。语法类似于 HTML。各种访问控制指令被包含在标签对中，例如 <Directory> ... </Directory>。

以下列表描述了一些访问控制指令。特别是，请注意 AuthUserFile 指令；您可以为特定目录设置基于密码的访问控制。

**Options** `opt1 opt2 ...` — 指定此指令出现的目录部分中的访问控制选项。选项可以是一项或多项：
- `None` 禁用所有访问控制功能。
- `All` 为目录打开所有功能。
- `FollowSymLinks` 使服务器能够跟随符号链接。
- `SymLinksIfOwnerMatch` 仅当目录的同一用户拥有链接的目录时才跟随符号链接。
- `ExecCGI` 启用目录中 CGI 脚本的执行。
- `Includes` 在此目录中启用服务器端 `include` 文件（术语 *server-side include* 指的是放置在 HTML 文件中的指令，Web 服务器在将结果返回给 Web 浏览器之前会处理这些指令）。
- `Indexes` 允许客户端请求目录的索引（目录列表）。
- `IncludesNOEXEC` 禁用服务器端包含中的 `#exec` 命令。

**AllowOverride** `directive1 directive2 ...` — 指定哪些访问控制指令可以在每个目录的基础上被覆盖。指令列表可以包含以下一项或多项：
- `None` 阻止任何指令被覆盖。
- `All` 启用在每个目录的基础上覆盖任何指令。
- `Options` 启用在目录级文件中使用 `Options` 指令。
- `FileInfo` 启用控制文档类型的指令的使用，例如 `AddType` 和 `AddEncoding`。
- `AuthConfig` 启用授权指令的使用，例如 `AuthName`、`AuthType`、`AuthUserFile` 和 `AuthGroupFile`。
- `Limit` 启用在目录的访问配置文件中使用 `Limit` 指令（`allow`、`deny` 和 `order`）。

**AuthName** `name` — 指定目录的授权名称。

**AuthType** `type` — 指定要使用的授权类型。唯一受支持的授权类型是 Basic。



AuthUserFile filename — 指定用于存储授权用户名和密码的文件。例如，以下指令将授权文件设置为 /etc/httpd/conf/passwd：

```
AuthUserFile /etc/httpd/conf/passwd
```

你必须使用 /usr/bin/htpasswd 支持程序创建授权文件。要创建授权文件并为名为 jdoe 的用户添加密码，请指定以下内容：

/usr/bin/htpasswd -c /etc/httpd/conf/passwd jdoe
```

当提示输入密码时，输入密码然后再次输入以确认。

AuthGroupFile filename — 指定用于身份验证时查询用户组列表的文件。

order order — 指定另外两个指令 — allow 和 deny — 的评估顺序。顺序如下之一：

- deny,allow 会导致 Web 服务器先评估 deny 指令再评估 allow。
- allow,deny 会导致 Web 服务器先评估 allow 指令再评估 deny。
- mutual-failure 仅启用 allow 列表中的主机。

deny from host1 host2... — 指定被拒绝访问的主机。

allow from host1 host2... — 指定允许访问的主机。

要使特定域中的所有主机都能访问目录中的 Web 文档，请指定以下内容：

```
order deny,allow
allow from .nws.noaa.gov
```

require entity entity1 entity2... — 此指令指定哪些用户可以访问目录。entity 如下之一：

- user 仅启用命名用户列表。
- group 仅启用命名组列表。
- valid-user 允许 AuthUserFile 中列出的所有用户访问该目录（前提是他们输入正确的密码）。

## 虚拟主机设置

Apache HTTP 服务器的一个有用功能是它可以处理虚拟 Web 服务器。虚拟主机简单地意味着单个 Web 服务器可以响应许多不同的 IP 地址，并根据 IP 地址从不同目录提供网页。这意味着您可以设置单个 Web 服务器同时响应 `www.big.org` 和 `www.tiny.com` 并为每个主机名提供唯一的首页。具有此功能的是 *multi-homed* Web 服务器、*virtual* Web 服务器或具有 *virtual host support* 的服务器。

正如您可能猜到的那样，Internet 服务提供商（ISPs）使用 Apache Web 服务器的虚拟主机功能为其客户提供虚拟网站。您需要以下条件来支持虚拟主机：

- Web 服务器必须能够响应多个 IP 地址（每个都有唯一的域名）并且必须能够为每个 IP 地址指定文档目录、日志文件和其他配置项。
- 主机系统必须能够将多个 IP 地址与单个物理网络接口关联。Red Hat Linux 可以做到这一点。
- 与 IP 地址关联的每个域名必须是唯一的、已注册的域名，并且具有正确的 DNS 条目。

有关如何在 Apache HTTP 服务器中设置虚拟主机的最新信息，请参阅以下 URL：

```
http://httpd.apache.org/docs-2.0/vhosts
```

Apache HTTP 服务器可以对不同的主机名使用不同的首页进行响应。支持虚拟主机时，您有两个选项：

- **Run multiple copies of the `httpd` program, one for each IP address.** 在这种情况下，您为每个主机创建 `httpd.conf` 配置文件的单独副本，并使用 `Listen` 指令使服务器响应特定的 IP 地址。
- **Run a single copy of the `httpd` program with a single `httpd.conf` file.** 在配置文件中，将 `Listen` 设置为仅端口号（以便服务器响应与主机关联的任何 IP 地址），并使用 `VirtualHost` 指令为每个虚拟主机配置服务器。

仅当您不期望系统上有重负载时才运行多个 HTTP 守护进程；由于运行多个守护进程的开销，系统可能无法很好地响应。但是，如果每个虚拟主机对以下指令有独特的配置需求，则可能需要多个 HTTP 守护进程：

- `UserId` 和 `GroupId`（HTTP 守护进程的用户和组 ID）
- `ServerRoot`（服务器的根目录）
- `TypesConfig`（MIME 类型配置文件）

对于负载较重的站点，请配置 Web 服务器，使单个 HTTP 守护进程可以为多个虚拟主机提供服务。当然，这条建议意味着只有一个配置文件。在该配置文件中，使用 VirtualHost 指令配置每个虚拟主机。

大多数 ISP 使用 Apache HTTP 服务器的 VirtualHost 功能为其客户提供虚拟网站。除非您支付专用 Web 主机费用，否则您通常会获得一个虚拟站点，您拥有自己的域名，但与许多其他客户共享服务器和实际主机。

VirtualHost 指令的语法如下：

```
<VirtualHost hostaddr>
... directives that apply to this host
</VirtualHost>
```

使用此语法，您使用 <VirtualHost> 和 </VirtualHost> 将一组指令括起来，这些指令仅适用于由 hostaddr 参数标识的特定虚拟主机。hostaddr 可以是 IP 地址或虚拟主机的完全限定域名。

您可以在 <VirtualHost> 块中放置几乎任何 Apache 指令。至少，网络管理员会在 <VirtualHost> 块中包含以下指令：

- **DocumentRoot**，指定此虚拟主机的文档所在位置
- **Servername**，标识服务器对外部世界（这应该是 DNS 支持的已注册域名）
- **ServerAdmin**，此虚拟主机网络管理员的电子邮件地址
- **Redirect**，指定要重定向到其他 URL 的任何 URL
- **ErrorLog**，指定与此虚拟主机相关的错误应记录到的文件
- **CustomLog**，指定访问此虚拟主机的访问应记录到的文件

当服务器接收到对特定虚拟主机的 DocumentRoot 目录中文档的请求时，它会使用该服务器的 <VirtualHost> 块中的配置参数来处理该请求。

以下是设置虚拟主机 www.lnbsoft.com 的 <VirtualHost> 指令的典型示例：

```
<VirtualHost www.lnbsoft.com>
    DocumentRoot /home/naba/httpd/htdocs
    ServerName www.lnbsoft.com
    ServerAdmin webmaster@lnbsoft.com
    ScriptAlias /cgi-bin/ /home/naba/httpd/cgi-bin/
    ErrorLog /home/naba/httpd/logs/error_log
    CustomLog /home/naba/httpd/logs/access_log common
</VirtualHost>
```

这里 CustomLog 指令中的名称 common 指的是 httpd.conf 文件中由 LogFormat 指令更早定义的一个格式的名称，如下所示：

```
LogFormat "%h %l %u %t \"%r\" %>s %b" common
```

此日志格式字符串产生的日志文件中的行如下所示：

```
dial236.dc.psn.net - - [13/Jul/2003:18:09:00 -0500] "GET / HTTP/1.0" 200 1243
```

格式字符串包含以百分号（%）开头的两个字母标记。这些标记的含义如表 2-1 所示。

表 2-1 LogFormat 标记

| 标记 | 含义 |
|-------|---------|
| %b | 发送到客户端的字节数，不包括头信息 |
| %h | 客户端机器的主机名 |
| %l | 用户的身份，如果可用 |
| %r | 客户端的 HTTP 请求（例如，GET / HTTP/1.0） |
| %s | Web 服务器的服务器响应代码 |
| %t | 当前本地日期和时间 |
| %u | 用户提供的用户名（仅当访问控制规则要求用户名/密码身份验证时） |

### 第三章：设置 FTP 服务器

### 本章内容

- 安装 FTP 服务器
- 配置 FTP 服务器
- 设置匿名 FTP

文件传输协议（FTP）是一种流行的用于在系统之间传输文件的 Internet 服务。匿名 FTP 是另一种用于分发文件的流行 Internet 服务。匿名 FTP 的好处在于，如果远程系统支持匿名 FTP，任何人都可以以匿名用户 ID 使用 FTP 并从该系统下载文件。虽然匿名 FTP 对于分发数据很有用，但如果设置不当会带来安全风险。

Red Hat Linux 附带了多个 FTP 客户端和由 Chris Evans 编写的“非常安全”FTP 守护进程（vsftpd）。Red Hat Linux 还包含一个名为 anonftp 的 RPM，用于设置支持匿名 FTP 所需的文件。在本章中，我将向您展示如何通过文本配置文件配置 FTP 服务器以及如何控制对 FTP 服务器的访问。我还描述了匿名 FTP——它的设置方式以及如何确保其安全。

### 安装 FTP 服务器

在 Red Hat Linux 安装期间，您可以选择安装 FTP 服务器软件。要检查 FTP 服务器是否已安装，请键入以下命令：

```
rpm -q vsftpd
```

如果软件确实已安装，您应该会看到类似以下内容的输出：

```
vsftpd-1.2.0-2.1
```



以 root 身份登录并将 DVD 放入 DVD 驱动器。如果您使用的是 GNOME 或 KDE 桌面，DVD 应该会自动挂载。如果没有，请键入以下命令来挂载 DVD：

```
mount /mnt/cdrom
```

然后键入以下命令来更改目录：

```
cd /mnt/cdrom/RedHat/RPMS
```

这里可以找到 FTP 的 RPM 文件。您可以使用以下 RPM 命令同时安装 FTP 服务器和匿名 FTP 包：

```
rpm -ivh vsftpd*
```

```
rpm -ivh anonftp*
```

## 配置 FTP 服务器

Red Hat Linux 自带非常安全的 FTP 守护进程（vsftpd），由 Chris Evans 编写。vsftpd 的可执行文件为 /usr/sbin/vsftpd，它使用 /etc 和 /etc/vsftpd 目录中的多个配置文件。默认情况下，vsftpd 服务器处于禁用状态；如果您想使用 FTP 服务器，首先必须启用它。本节将向您展示如何操作。

在 Red Hat Linux 的早期版本中，vsftpd 服务器被设置为在 xinetd — 互联网超级服务器 下运行。这需要编辑 /etc/xinetd.d 目录中的配置文件以启用 vsftpd 服务器。然而，从 Red Hat Linux 8.1 开始，vsftpd 服务器被配置为独立运行，并且有一个初始化脚本（或 init 脚本）— /etc/init.d/vsftpd — 用于启动和停止服务器。要启动 vsftpd 服务器，请以 root 身份登录并键入以下命令：

```
service vsftpd start
```

您也可以以 root 身份键入以下命令，使 vsftpd 在系统启动时自动启动：

```
chkconfig --level 35 vsftpd on
```

启动 vsftpd 服务器后，默认设置应该足以开始使用服务器。这是因为其他 FTP 客户端现在可以连接并从您的 FTP 服务器请求文件。然而，您应该了解配置文件，以防以后需要对其进行自定义。

### vsftpd 配置文件

vsftpd 服务器会查阅位于 /etc 和 /etc/vsftpd 目录中的多个配置文件。这些目录控制 FTP 服务器的许多方面，例如它是否以独立模式运行、谁可以下载文件以及是否允许匿名 FTP。vsftpd 的关键配置文件如下：

- `/etc/vsftpd.conf` 控制 `vsftpd` 服务器的工作方式（例如，是否应允许匿名登录、允许文件上传等）。
- `/etc/vsftpd.ftpusers` 列出无法访问 FTP 服务器的用户名称。
- `/etc/vsftpd.user_list` 列出被拒绝访问的用户名称（甚至不会提示输入密码）。然而，如果在 `/etc/vsftpd.conf` 中将 `userlist_deny` 选项设置为 NO，则这些用户将被允许访问 FTP 服务器。

通常您可以将这些配置文件的大部分保持默认设置。然而，以防您需要更改某些内容以使 vsftpd 满足您的需求，我将在接下来的几节中简要介绍配置文件。

### /etc/vsftpd.conf 文件

要了解 /etc/vsftpd.conf 文件中可以包含的内容以及这些行如何影响 vsftpd 服务器的操作，请先查看 Red Hat Linux 默认安装的 /etc/vsftpd.conf 文件。该文件中的注释说明了每个选项的作用。

默认情况下，vsftpd 几乎不允许任何操作。/etc/vsftpd.conf 中的选项会放宽限制，以便用户可以使用 FTP。设置应放宽到何种程度由您决定。请注意，大多数选项设置为 YES。这是因为大多数默认设置都是 NO。要反转某个选项的意图，只需在该行的开头放置一个 # 来注释掉该选项即可。

以下是您可以在 /etc/vsftpd.conf 中设置的一些选项：

- `anon_mkdir_write_enable=YES` 允许匿名 FTP 用户创建新目录。这也是一个有风险的选项，即使您允许匿名用户上传文件，也可能希望将其设置为 NO。
- `anon_upload_enable=YES` 表示匿名 FTP 用户可以上传文件。此选项仅在 `write_enable` 已设置为 YES 且目录对所有人具有写权限时才生效。请记住，允许匿名用户在您的系统上写入是非常危险的，因为有人可能会填满磁盘或将您的磁盘用于个人存储。
- `anonymous_enable=YES` 启用 *匿名 FTP*（用户可以使用用户名 `anonymous` 登录并提供其电子邮件地址作为密码）。如果您不想要匿名 FTP，请注释掉此行。
- `ascii_download_enable=YES` 启用 ASCII 模式下的文件下载。不幸的是，恶意的远程用户可以使用巨大文件的名称发出 SIZE 命令，从本质上导致 FTP 服务器浪费大量资源打开该文件并确定其大小。这是拒绝服务攻击中常用的典型技术（我在本节后面提到过）。
- `ascii_upload_enable=YES` 启用 ASCII 模式下的文件上传（用于文本文件）。
- `async_abor_enable=YES` 使 `vsftpd` 能够识别任何时候到达的 ABOR（中止）请求。您可能需要启用它以允许旧的 FTP 客户端与 `vsftpd` 配合使用。
- `banned_email_file=/etc/vsftpd.banned_emails` 指定包含被禁止电子邮件地址列表的文件（仅在 `deny_email_enable` 设置为 YES 时使用）。
- `chown_uploads=YES` 导致上传的匿名文件归 `chown_username` 选项指定的不同用户所有。除非绝对必要，否则不要启用此选项，并且不要将 `root` 指定为 `chown_username`（那是灾难的开始）。
- `chown_username=name` 指定匿名 FTP 用户上传的文件将拥有的用户名。
- `chroot_list_enable=YES` 使 `vsftpd` 在用户登录 FTP 服务时，将除 `chroot_list_file` 指定的列表上的用户之外的所有用户限制在其主目录中。这可以防止这些用户访问主目录之外的任何其他文件。
- `chroot_list_file=/etc/vsftpd.chroot_list` 是用户列表，具体取决于 `chroot_local_user` 的设置，这些用户要么被限制在其主目录中，要么不被限制。
- `connect_from_port_20=YES` 使 `vsftpd` 确保数据传输通过端口 20（FTP 数据端口）进行。
- `data_connection_timeout=120` 是非活动数据连接在超时之前等待的秒数。
- `deny_email_enable=YES` 使 `vsftpd` 检查被禁止电子邮件地址的列表，并拒绝任何尝试使用被禁止的电子邮件地址作为密码匿名登录的用户访问。
- **dirmessage_enable=YES** 使 `vsftpd` 在 FTP 用户更改到某些目录时显示消息。
- **ftp_banner=Welcome to my FTP service.** 设置 `vsftpd` 在用户登录时显示的横幅。您可以将消息更改为您想要的任何内容。
- **idle_session_timeout=600** 是空闲会话（指有人连接但什么都不做的情况）在超时并由 `vsftpd` 注销用户之前等待的时间（以秒为单位）。
- **listen=YES** 使 `vsftpd` 监听连接请求，从而以独立模式运行。如果您想在 `xinetd` 下运行 `vsftpd`，请将其设置为 NO。
- **local_enable=YES** 使 `vsftpd` 授予本地用户访问 FTP 的权限。
- **local_umask=022** 表示 FTP 写入的任何文件权限都为 644（所有人可读，但只有所有者可写）。您可以将其设置为您想要的任何文件权限掩码设置。例如，如果您希望除所有者外任何人都无权限，请将其更改为 077。
- **ls_recurse_enable=YES** 允许 FTP 用户通过使用 `ls -R` 命令递归遍历目录。
- **nopriv_user=ftp** 标识 FTP 服务器可使用的无特权用户账户。
- **pam_service_name=vsftpd** 是在 `vsftpd` 必须对用户进行身份验证时使用的可插拔身份验证模块（PAM）配置文件名称。默认情况下，PAM 配置文件位于 `/etc/pam.d` 目录中。这意味着 `vsftpd` 的 PAM 配置文件是 `/etc/pam.d/vsftpd`。
- **tcp_wrappers=YES** 启用通过 TCP wrapper 进行访问控制的支持，TCP wrapper 会查阅文件 `/etc/hosts.allow` 和 `/etc/hosts.deny`（有关 TCP wrapper 的更多信息，请参阅第七册第 3 章）。
- **userlist_deny=YES** 使 `vsftpd` 拒绝 `/etc/vsftpd.user_list` 文件中列出的用户的访问。这些用户甚至不会被提示输入密码。
- **write_enable=YES** 使 `vsftpd` 允许向主机上传文件。
- **xferlog_enable=YES** 打开文件下载和上传的日志记录（总是明智之举，但会占用磁盘空间）。
- **xferlog_file=/var/log/vsftpd.log** 指定 `vsftpd` 日志文件的完整路径名。默认值为 `/var/log/vsftpd.log`。
- **xferlog_std_format=YES** 使 `vsftpd` 以其他 FTP 守护进程使用的标准格式生成日志文件。




## /etc/vsftpd.ftusers 文件

The vsftpd server uses the Pluggable Authentication Module (PAM) to authenticate users when they try to log in (just as the normal login process uses PAM to do the job). The PAM configuration file for vsftpd is /etc/pam.d/vsftpd. That PAM configuration file refers to /etc/vsftpd.ftusers like this:

```
auth required /lib/security/pam_listfile.so item=user sense=deny file=/etc/vsftpd.ftusers onerr=succeed
```

This basically says that anyone listed in the /etc/vsftpd.ftusers should be denied login. The default /etc/vsftpd.ftusers file contains the following list of users:

```
root
bin
daemon
adm
lp
sync
shutdown
halt
mail
news
uucp
operator
games
nobody
```

## /etc/vsftpd.user_list 文件

If the userlist_deny option is set to YES, vsftpd does not allow users listed in the /etc/vsftpd.user_list file any access to FTP services. It does not even prompt them for a password. However, if userlist_deny is NO, the meaning is reversed and these users are the only ones allowed access (but the PAM configuration still denies anyone on the /etc/vsftpd.ftusers list).

## 设置安全的匿名 FTP

Anonymous FTP refers to the use of the user name anonymous, which anyone can use with FTP to transfer files from a system. Anonymous FTP is a common way to share files on the Internet.

FTP on your Linux PC and place the software in an appropriate directory. After that, all you have to do is announce to the world (probably through a posting in the comp.os.linux.announce newsgroup) that you have a new program available. Now anyone can get the software from your system at his or her convenience.

Even if you run a for-profit business, you can use anonymous FTP to support your customers. If you sell a hardware or software product, you may want to provide technical information or software “fixes” through anonymous FTP.

Unfortunately, the convenience of anonymous FTP comes at a price. If you don’t configure the anonymous FTP service properly, intruders and pranksters may gain access to your system. Some intruders may simply use your system’s disk as a temporary holding place for various files; others may fill your disk with junk files, effectively making your system inoperable (this sort of attack is called a Denial of Service attack). At the other extreme, an intruder may gain user-level (or, worse, root-level) access to your system and do much more damage. The default anonymous FTP setup in Red Hat Linux employs the necessary security precautions.

## 尝试匿名 FTP

To see anonymous FTP in action, try accessing your system by using an FTP client. For example, in the following sample session, I have accessed the FTP server from a terminal window on the same system (my input appears in boldface):

```
ftp localhost
Connected to localhost (127.0.0.1).
220 (vsFTPd 1.1.3)
Name (localhost:naba): anonymous
331 Please specify the password.
Password: < I can type anything as password
230 Login successful. Have fun.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls -l
227 Entering Passive Mode (127,0,0,1,169,190)
150 Here comes the directory listing.
drwxr-xr-x   2 0       0          4096 Jun 06 04:36 pub
226 Directory send OK.
ftp> bye
221 Goodbye.
```

When you successfully log in for anonymous FTP, you access the home directory of the user named ftp (the default directory is /var/ftp). Place the publicly accessible files — the ones you want to enable others to download from your system — in the /var/ftp/pub directory.

## 匿名 FTP 的关键特性

The key features of an anonymous FTP setup are as follows:

- There is a user named `ftp` whose home directory is `/var/ftp`. The user does not have a shell assigned. Here is what you get when you search for `ftp` in the `/etc/passwd` file: `grep ftp /etc/passwd` The output should be something like this: `ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin` The `x` in the second field means that no one can log in with the user name `ftp`.
- Here is the full permission setting and owner information for the `/var/ftp` directory: `drwxr-xr-x 3 root root 4096 Jun 22 12:10 ftp` As this line shows, the `/var/ftp` directory is owned by `root`, and the permission is set to 755 (only `root` can read, write and execute; everyone else can only read and execute).
- You can view the contents of the `/var/ftp` directory with the `ls -la` command. The result is as follows: `total 12` `drwxr-xr-x 3 root root 4096 Jun 22 12:10 .` `drwxr-xr-x 21 root root 4096 Jun 22 12:10 ..` `drwxr-xr-x 2 root root 4096 Jun 6 00:36 pub`
- The `pub` directory is where you place any files that you want to enable others to download from your system through anonymous FTP.

### 第 4 章：提供邮件和新闻服务

### 本章内容

- ✓ Installing and using `sendmail`
- ✓ Testing mail delivery manually
- ✓ Configuring `sendmail`
- ✓ Installing the InterNetNews (INN) server
- ✓ Configuring and starting INN
- ✓ Setting up local newsgroups

Electronic mail (e-mail) is one of the popular services available on Internet hosts. E-mail software comes in two parts: a mail-transport agent (MTA), which physically sends and receives mail messages; and a mail-user agent (MUA), which reads messages and prepares new messages. In this chapter, I describe the e-mail service and show you how to configure the sendmail server on a Red Hat Linux PC.

Internet newsgroups provide another convenient way, besides e-mail, to discuss various topics and to share your knowledge with others. Red Hat Linux comes with the software you need to read newsgroups and to set up your own system as a news server. In this chapter, I describe how to configure and run the InterNetNews server, a popular news server. I also show you how to set up local newsgroups for your corporate intranet (or even your home network).

### 安装邮件服务器

If you install the mail server software during Red Hat Linux installation, you don't have to do much more to begin using the mail service. To see whether the mail server is already installed, type the following command:

```
rpm -q sendmail
```

You're all set if the response looks like this:

```
sendmail-8.12.9-7
```

This output says that sendmail version 8.12.9 is installed on the system.

If the output message tells you that sendmail isn't installed, you can use the Red Hat Package Manager (RPM) to install the individual packages needed for running and configuring sendmail. To install the RPM files for sendmail, log in as root and insert the second CD-ROM in the CD-ROM drive. If you're using GNOME or KDE, the CD-ROM should be automatically mounted. Otherwise, type the following command to mount the CD-ROM:

```
mount /mnt/cdrom
```

Then type the following commands to install the sendmail files:

```
cd /mnt/cdrom/RedHat/RPMS
rpm -ivh sendmail*
```

This should install two packages:

- ♦ sendmail — A complex mail transport agent (MTA)
- ♦ sendmail-cf — Configuration files for sendmail

### 使用 sendmail

To set up your system as a mail server, you must configure the sendmail mail-transport agent properly. sendmail has the reputation of being a complex but complete mail-delivery system. Just one look at sendmail's configuration file, /etc/mail/sendmail.cf, should convince you that sendmail is indeed complex. Luckily, you don't have to be an expert on the sendmail configuration file. All you need is one of the predefined configuration files — like the one that's installed on your system — to use sendmail.

Your system should already have a working sendmail configuration file — /etc/mail/sendmail.cf. The default file assumes you have an Internet connection and a name server. Provided you have an Internet connection, you should be able to send and receive e-mail from your Red Hat Linux PC.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_669_0.png)

### 邮件投递测试

To try out the sendmail mail-transfer agent, you can use the mail command to compose and send a mail message to yourself at a different address. For example, here's how I send myself a message using the mail command:

```
mail naba@comcast.net
Subject: Testing e-mail
This is from my Red Hat Linux system.
Cc: Press Ctrl+D
```

mail 命令是一个简单的邮件用户代理。在前面的示例中，我在命令行中指定收件人 — naba@comcast.net —。mail 程序会提示输入主题行。主题之后，我输入邮件正文，并用仅包含一个句点的一行结束它。提示输入 Cc: 时，我按下 Ctrl+D。结束邮件后，邮件用户代理会将邮件传递给 sendmail — 邮件传输代理 — 以交付到指定地址。由于我的系统已连接到互联网，sendmail 会立即投递邮件。

为验证邮件是否投递，我从我的 ISP 检查邮件并看到消息已到达。只要我的系统拥有官方的 DNS 主机名并且在 ISP 的 DNS 数据库中，我也可以回复。

因此，只要你的 Red Hat Linux 系统具有互联网连接和已注册的域名，随 Red Hat Linux 提供的初始 sendmail 配置文件就足以发送和接收电子邮件。

## 邮件投递机制

在互联网主机上，sendmail 邮件传输代理使用简单邮件传输协议（SMTP）投递邮件。基于 SMTP 的邮件传输代理监听 TCP 端口 25，并使用一组小的文本命令与其他邮件传输代理交换信息。事实上，SMTP 命令简单到足以让你从终端手动使用它们来发送邮件。以下示例展示了我是如何从同一系统上运行的 telnet 会话，使用 SMTP 命令向 Red Hat Linux PC 上的我的账户发送邮件的：

```
telnet localhost 25
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
220 localhost.localdomain ESMTP Sendmail 8.12.9/8.12.9; Tue, 15 Jul 2003 19:22:24 -0400

help
214-2.0.0 This is sendmail version 8.12.9
214-2.0.0 Topics:
214-2.0.0 HELO EHLO MAIL RCPT DATA
214-2.0.0 RSET NOOP QUIT HELP VRFY
214-2.0.0 EXPN VERB ETRN DSN AUTH
214-2.0.0 STARTTLS
214-2.0.0 For more info use *HELP <topic>*.
214-2.0.0 To report bugs in the Implementation send email to
214-2.0.0 sendmail-bugs@sendmail.org.
214-2.0.0 For local information send email to Postmaster at your site.
214-2.0.0 End of HELP info
HELP DATA
214-2.0.0 DATA
214-2.0.0 Following text is collected as the message.
214-2.0.0 End with a single dot.
214-2.0.0 End of HELP info
HELO localhost
250 localhost.localdomain Hello localhost.localdomain [127.0.0.1], pleased to meet you
MAIL FROM: naba
553 5.5.4 naba... Domain name required for sender address naba
MAIL FROM: naba@localhost
250 2.1.0 naba@localhost... Sender ok
RCPT TO: naba
250 2.1.5 naba... Recipient ok
DATA
354 Enter mail, end with "." on a line by itself
Testing... 1 2 3
Sending mail by telnet to port 25
250 2.0.0 h6FMWLQW020B2 Message accepted for delivery
quit
221 2.0.0 localhost.localdomain closing connection
Connection closed by foreign host.
```

telnet 命令打开到端口 25 的 TELNET 会话 — sendmail 期待 SMTP 命令的端口。Red Hat Linux 系统上的 sendmail 进程会立即用一条公告作出回复。

我输入 HELP 以查看 SMTP 命令列表。要获取特定命令的帮助，我可以输入 HELP commandname。列表显示了帮助信息，sendmail 在我输入 HELP DATA 时打印该信息。

我输入 HELO localhost 以启动与主机的会话。sendmail 进程用问候语回复。要发送邮件，我从 MAIL FROM: 命令开始，该命令指定邮件的发件人（我输入发送邮件的系统的用户名）。sendmail 需要用户名以及域名。

接下来，我使用 RCPT TO: 命令指定邮件的收件人。如果我想向多个收件人发送邮件，只需为每个收件人提供地址并使用 RCPT TO: 命令即可。

要输入邮件正文，我使用 DATA 命令。响应 DATA 命令时，sendmail 会显示一条说明，要求我用单独一行中的句点结束邮件。我输入邮件并用单独一行中的单个句点结束。sendmail 进程显示一条消息，表明邮件已被接受投递。最后，我用 QUIT 命令退出 sendmail 会话。

之后，我登录到我的 Red Hat Linux 系统并使用 mail 命令检查邮件。以下是在我通过示例 SMTP 会话使用 sendmail 发送的邮件时，使用 mail 命令的会话：

```
mail
Mail version 8.1 6/6/93. Type ? for help.
"/var/spool/mail/naba": 1 message 1 new
>N 1 naba@localhost.local Tue Jul 15 19:25 12/479
& 1
Message 1:
From: naba@localhost.localdomain Tue Jul 15 19:25:20 2003
Date: Tue, 15 Jul 2003 19:22:24 -0400
From: Naba Barkakati <naba@localhost.localdomain>

Testing... 1 2 3
Sending mail by telnet to port 25

& q
Saved 1 message in mbox
```

正如本示例所示，SMTP 命令简单到足以理解。本示例应有助于你理解邮件传输代理如何使用 SMTP 在互联网上传输邮件。当然，电子邮件程序通常会自动化整个过程 — sendmail 程序也是如此（通过 sendmail 配置文件 /etc/mail/sendmail.cf 中的设置）。

## sendmail 配置文件

你不必理解 sendmail 配置文件 /etc/mail/sendmail.cf 中的所有内容，但你应该知道该文件是如何创建的。这样，如果必要时，你可以进行小的修改并重新生成 /etc/mail/sendmail.cf 文件。

在重新生成 sendmail.cf 文件之前，你必须安装 sendmail-cf 包。要检查 sendmail-cf 包是否已安装，请输入

```
rpm -q sendmail-cf
```

如果命令没有打印 sendmail-cf 包的名称，你必须安装该包。此 RPM 文件位于本书附带的第二张 CD-ROM 中。要安装该包，以 root 身份登录并将第二张 CD-ROM 插入 CD-ROM 驱动器。在 GNOME 或 KDE 中，CD-ROM 应自动挂载。否则，你可以使用以下命令挂载 CD-ROM：

```
mount /mnt/cdrom
```

然后通过输入以下命令安装包：

```
cd /mnt/cdrom/RedHat/RPMS
rpm -ivh sendmail-cf*
```

sendmail-cf 包在 /usr/share/sendmail-cf 目录中安装生成新的 sendmail.cf 配置文件所需的所有文件。正如我在接下来的几节中解释的，sendmail.cf 文件是由多个 m4 宏文件生成的（文本文件，其中每一行最终会扩展为对某个程序有意义的多行）。这些宏文件被组织在 /usr/share/sendmail-cf 下的多个子目录中。你可以阅读 /usr/share/sendmail-cf 中的 README 文件以了解更多关于 sendmail 配置文件创建的信息。

现在你已经处理了先决条件，你可以学习如何重新生成 sendmail.cf 文件。

## m4 宏处理器

m4 宏处理器用于生成随 Red Hat Linux 中 sendmail 包提供的 sendmail.cf 配置文件。主宏文件 sendmail.mc 包含在 sendmail 包中，但该文件需要 sendmail-cf 包中的其他 m4 宏文件。

那么什么是宏？宏基本上是处理某些操作的代号的符号名称，通常以简写形式替代长字符串。像 m4 这样的宏处理器通常读取其输入文件并将其复制到输出，同时处理宏。宏的处理通常涉及执行某些操作并生成输出。由于宏在输出中生成的文本远多于仅宏的名称，因此宏的处理被称为宏展开。

m4 宏处理器是基于流的。这意味着它在展开任何宏的同时将输入字符复制到输出。m4 宏处理器没有行的概念，因此它会将换行符（标记行尾）复制到输出。这就是为什么你在大多数 m4 宏文件中看到单词 dn1；dn1 是一个 m4 宏，表示“删除至换行”。dn1 宏会删除从 dn1 开始直到下一个换行符（包括换行符）之间的所有字符。输出中的换行符不会造成任何危害；它们只是创建不必要的空行。sendmail 宏包使用 dn1 来避免输出配置文件中的此类空行。由于 dn1 基本上意味着删除到行尾的所有内容，m4 宏文件也使用 dn1 作为注释行的前缀。

要了解 m4 的非常简单的用法，请考虑以下 m4 宏文件，它定义了两个宏 — hello 和 bye — 并在表单信中使用它们：

```
dn1 ##################################################
dn1 # File: ex.m4
dn1 # A simple example of m4 macros
dn1 ##################################################
define(`hello', `Dear Sir/Madam')dn1
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_673_0.png)



```
define(`bye',`Sincerely,
Customer Service')dnl
dnl Now type the letter and use the macros
hello,
This is to inform you that we received your recent inquiry.
We will respond to your question soon.
bye
```

使用你喜欢的文本编辑器输入此文本并将其保存为名为 ex.m4 的文件。你可以为宏文件命名任意名称，但对于 m4 宏文件，使用 .m4 扩展名是惯例。

在使用 m4 处理宏文件之前，请注意示例中的以下关键点：

-   使用 dnl 宏开始所有注释行（例如，示例中的前四行）。
-   使用 dnl 宏结束每个宏定义。否则，当 m4 处理宏文件时，它会为每个宏定义产生一个空行。
-   使用内置的 m4 命令 define 来定义新宏。宏名和值都用一对左引号和右引号（'...'）括起来。请注意，不能使用普通的单引号来括住宏名和定义。

现在通过输入以下命令处理宏文件 ex.m4：

```
m4 ex.m4
```

m4 处理宏并显示以下输出：

```
Dear Sir/Madam,

This is to inform you that we received your recent inquiry.
We will respond to your question soon.

Sincerely,

Customer Service
```

听起来就像典型的客户服务格式信件，不是吗？

如果将输出与 ex.m4 文件进行比较，你会看到 m4 将格式信打印到标准输出，并将宏 hello 和 bye 扩展为其定义的值。如果想将格式信保存到名为 letter 的文件中，请使用 shell 的输出重定向功能，如下所示：

```
m4 ex.m4 > letter
```

如果想在信中使用单词 hello 或 bye 而不展开它们怎么办？你可以通过用一对引号（'...'）括住这些宏来实现。对于其他预定义的 m4 宏，如 define，也必须这样做。要将 define 用作普通单词而不是要展开的宏，请键入 'define'。

## sendmail.mc 文件

前一节中的简单示例应能让你了解 m4 宏是如何定义和使用来创建 sendmail.cf 文件等配置文件。您会在 /usr/share/sendmail-cf 目录中的文件中找到许多复杂的宏。一个顶层宏文件 sendmail.mc，在本节后面描述，使用 include 宏（用于将文件复制到输入流中）引入这些宏文件。

通过在位于 /usr/share/sendmail-cf 目录的文件中定义自己的高级宏集合，sendmail 本质上创建了自己的宏语言。sendmail 宏文件使用 .mc 扩展名。你应配置的主要 sendmail 宏文件是位于 /etc/mail 目录的 sendmail.mc。

与 /etc/mail/sendmail.cf 文件不同，/etc/mail/sendmail.mc 文件很短，应该更容易处理。以下是随 Red Hat Linux 提供的 /etc/mail/sendmail.mc 文件的完整列表：

```
divert(-1)dnl
dnl #
dnl # This is the sendmail macro config file for m4. If you make changes to
dnl # /etc/mail/sendmail.mc, you will need to regenerate the
dnl # /etc/mail/sendmail.cf file by confirming that the sendmail-cf package is
dnl # installed and then performing a
dnl # make -C /etc/mail
dnl #
`include(`/usr/share/sendmail-cf/m4/cf.m4')dnl
VERSIONID(`setup for Red Hat Linux')dnl
OSTYPE(`linux')dnl
dnl #
dnl # Uncomment and edit the following line if your outgoing mail needs to
dnl # be sent out through an external mail server:
dnl # define(`SMART_HOST',`smtp.your.provider')dnl
dnl #
define(`confDEF_USER_ID',``8:12')dnl
define(`confTRUSTED_USER',`smmsp')dnl
dnl define(`confAUTO_REBUILD',`')dnl
define(`confTO_CONNECT',`1m')dnl
define(`confTRY_NULL_MX_LIST',`true')dnl
```

```
define(`confDONT_PROBE_INTERFACES',`true')dnl
define(`PROCMAIL_MAILER_PATH',`/usr/bin/procmail')dnl
define(`ALIASES_FILE',`/etc/aliases')dnl
dnl define(`STATUS_FILE',`/etc/mail/statistics')dnl
define(`UUCP_MAILER_MAX',`2000000')dnl
define(`confUSERDB_SPEC',`/etc/mail/userdb.db')dnl
define(`confPRIVACY_FLAGS',`authwarnings,novrfy,noexpn,restrictqrun')dnl
define(`confAUTH_OPTIONS',`A')dnl
dnl #
dnl # The following allows relaying if the user authenticates, and disallows
dnl # plaintext authentication (PLAIN/LOGIN) on non-TLS links
dnl #
dnl # define(`confAUTH_OPTIONS',`A p')dnl
dnl #
dnl # PLAIN is the preferred plaintext authentication method and used by
dnl # Mozilla Mail and Evolution, though Outlook Express and other MUAs do
dnl # use LOGIN. Other mechanisms should be used if the connection is not
dnl # guaranteed secure.
dnl #
define(`confAUTH_MECH',`EXTERNAL DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')dnl
define(`confAUTH_MECHANISMS',`EXTERNAL GSSAPI DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')dnl
dnl #
dnl # Rudimentary information on creating certificates for sendmail TLS:
dnl #    make -C /usr/share/ssl/certs usage
dnl #
dnl define(`confCACERT_PATH',`/usr/share/ssl/certs')dnl
dnl define(`confCACERT',`/usr/share/ssl/certs/ca-bundle.crt')dnl
dnl define(`confSERVER_CERT',`/usr/share/ssl/certs/sendmail.pem')dnl
dnl define(`confSERVER_KEY',`/usr/share/ssl/certs/sendmail.pem')dnl
dnl #
dnl # This allows sendmail to use a keyfile that is shared with OpenLDAP's
dnl # slapd, which requires the file to be readable by group ldap
dnl #
dnl define(`confDONT_BLAME_SENDMAIL',`groupreadablekeyfile')dnl
dnl
dnl define(`confTO_QUEUEWARN',`4h')dnl
dnl define(`confTO_QUEUERETURN',`5d')dnl
dnl define(`confQUEUE_LA',`12')dnl
dnl define(`confREFUSE_LA',`18')dnl
dnl define(`confTO_IDLE',`0')dnl
dnl FEATURE(`delay_checks')dnl
dnl FEATURE(`no_default_msa',``')dnl
FEATURE(`smrsh',`/usr/sbin/smrsh')dnl
FEATURE(`mailertable',`hash -o /etc/mail/mailertable.db')dnl
FEATURE(`virtusertable',`hash -o /etc/mail/virtusertable.db')dnl
FEATURE(`redirect')dnl
FEATURE(`always_add_domain')dnl
FEATURE(`use_cw_file')dnl
FEATURE(`use_ct_file')dnl
dnl #
dnl # The -t option will retry delivery if e.g. the user runs over his quota.
dnl #
FEATURE(`local_procmail',``procmail -t -Y a $h -d $u`')dnl
FEATURE(`access_db',`hash -T<TMPF> -o /etc/mail/access.db')dnl
FEATURE(`blacklist_recipients')dnl
EXPOSED_USER(`root')dnl
dnl #
dnl # The following causes sendmail to only listen on the IPv4 loopback address
dnl # 127.0.0.1 and not on any other network devices. Remove the loopback
dnl # address restriction to accept email from the Internet or Intranet.
dnl #
```

```
DAEMON_OPTIONS(`Port=smtp,Addr=127.0.0.1, Name=MTA')dnl #
dnl #
dnl # The following causes sendmail to additionally listen to port 587 for
dnl # mail from MUAs that authenticate. Roaming users who can't reach their
dnl # preferred sendmail daemon due to port 25 being blocked or redirected find
dnl # this useful.
dnl #
dnl # DAEMON_OPTIONS(`Port=submission, Name=MSA, M=Ea')dnl #
dnl #
dnl # The following causes sendmail to additionally listen to port 465, but
dnl # starting immediately in TLS mode upon connecting. Port 25 or 587 followed
dnl # by STARTTLS is preferred, but roaming clients using Outlook Express can't
dnl # do STARTTLS on ports other than 25. Mozilla Mail can ONLY use STARTTLS
dnl # and doesn't support the deprecated smtps: Evolution 1.1.1 uses smtps
dnl # when SSL is enabled -- STARTTLS support is available in version 1.1.1.
dnl #
dnl # For this to work your OpenSSL certificates must be configured.
dnl #
dnl # DAEMON_OPTIONS(`Port=smtps, Name=TLSMTA, M=s')dnl #
dnl #
dnl # The following causes sendmail to additionally listen on the IPv6 loopback
dnl # device. Remove the loopback address restriction to listen to the network.
dnl #
dnl # NOTE: binding both IPv4 and IPv6 daemon to the same port requires
dnl #       a kernel patch
dnl #
dnl # DAEMON_OPTIONS(`port=smtp,Addr=::1, Name=MTA-v6, Family=inet6')dnl #
dnl #
dnl # We strongly recommend not accepting unresolvable domains if you want to
dnl # protect yourself from spam. However, the laptop and users on computers
dnl # that do not have 24x7 DNS do need this.
dnl #
dnl # FEATURE(`accept_unresolvable_domains')dnl #
dnl #
dnl # FEATURE(`relay_based_on_MX')dnl #
dnl #
dnl # Also accept email sent to *localhost.localdomain* as local email.
dnl #
dnl # LOCAL_DOMAIN(`localhost.localdomain')dnl #
dnl #
dnl # The following example makes mail from this host and any additional
dnl # specified domains appear to be sent from mydomain.com
dnl #
dnl # MASQUERADE_AS(`mydomain.com')dnl #
dnl #
dnl # masquerade not just the headers, but the envelope as well
dnl #
dnl # FEATURE(masquerade_envelope)dnl #
dnl #
dnl # masquerade not just @mydomainalias.com, but *@mydomainalias.com as well
dnl #
dnl # FEATURE(masquerade_entire_domain)dnl #
dnl #
dnl # MASQUERADE_DOMAIN(localhost)dnl #
dnl # MASQUERADE_DOMAIN(localhost.localdomain)dnl #
dnl # MASQUERADE_DOMAIN(mydomainalias.com)dnl #
dnl # MASQUERADE_DOMAIN(mydomain.lan)dnl #
MAILER(smtp)dnl
MAILER(procmail)dnl
```



![](img/a7eec43a54473e95dc5ea333fecf1bd7_678_0.png)

如果您对 /etc/mail/sendmail.mc 文件进行更改，则必须通过运行 m4 宏处理器并使用以下命令生成 /etc/mail/sendmail.cf 文件（您必须以 root 身份登录）：

```
m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf
```

注释还告诉您需要 sendmail-cf 软件包来处理此文件。

根据上一节对 m4 宏的描述，您可以看到 sendmail.mc 文件使用 define 来创建新宏。您还可以看到 dnl 被大量使用，以避免在输出中插入过多的空行。

其他大写单词（如 OSTYPE、FEATURE 和 MAILER）是 sendmail 宏。这些宏在 /usr/share/sendmail-cf 目录的子目录中的 m4 文件中定义，并通过以下 include 宏合并到 sendmail.mc 文件中：

```
include(`/usr/share/sendmail-cf/m4/cf.m4')dnl
```

/usr/share/sendmail-cf/m4/cf.m4 文件反过来包含 cfhead.m4 文件，后者又包含其他 m4 文件，依此类推。净效果是，随着 m4 宏处理器处理 sendmail.mc 文件，宏处理器会将来自 /usr/share/sendmail-cf 的各个子目录的许多 m4 文件合并进来。

以下是关于 /etc/mail/sendmail.mc 文件的一些关键要点：

![](img/a7eec43a54473e95dc5ea333fecf1bd7_678_1.png)

- VERSIONID('setup for Red Hat Linux') 宏会将引号中包含的版本信息插入到输出中。
- OSTYPE('linux') 指定 Linux 为操作系统。您必须尽早指定它以确保正确配置。通常将此宏放在 VERSIONID 宏之后。
- MAILER(smtp) 描述邮件传输代理。根据 /usr/share/sendmail-cf/README 文件中的说明，MAILER 声明应始终放在 sendmail.mc 文件的末尾，并且 MAILER(smtp) 应始终位于 MAILER(procmail) 之前。邮件传输代理 smtp 指的是 SMTP 邮件传输代理。
- FEATURE 宏请求各种特殊功能。例如，FEATURE('blacklist_recipients') 打开阻止特定用户名、主机或地址的传入邮件的功能。允许或拒绝的邮件规范放在访问数据库（/etc/mail/access.db 文件）中。您还需要 FEATURE('access_db') 宏来启用访问数据库
- MASQUERADE_AS('mydomain.com') 导致 sendmail 将传出邮件标记为来自主机 mydomain.com（用您的域名替换此项）。其思路是大型组织设置一台 sendmail 服务器来处理许多子域的邮件，并使所有邮件看起来都来自单个域（例如，大学许多部门的邮件看起来都来自大学的主域名）。
- MASQUERADE_DOMAIN(subdomain.mydomain.com) 指示 sendmail 将来自 user@subdomain.mydomain.com 等地址的邮件发送为源自 MASQUERADE_AS 宏指定的域中的同一用户名。

诸如 FEATURE 和 MAILER 之类的 sendmail 宏在 /usr/share/sendmail-cf/README 文件中进行了描述。在更改 sendmail.mc 文件之前，请查阅该文件以了解有关 sendmail 宏的更多信息。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_679_0.png)

通常，您必须在 /etc/mail/sendmail.mc 文件的最后一行添加系统的主机名。按照以下步骤添加主机名：

1. 如果主机名为 mycompany.com，请按如下方式编辑 /etc/mail/sendmail.mc 中的 Cw 行：
   `Cwlocal.host.localdomain mycompany.com mycompany`
2. 使用以下命令重建 /etc/mail/sendmail.cf 文件：
   `m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf`
3. 使用以下命令重启 sendmail：
   `service sendmail restart`

## sendmail.cf 文件语法

sendmail.cf 文件的语法设计为便于 sendmail 程序解析，因为 sendmail 在启动时每次都会读取此文件。文件语法设计时，人类可读性并不是主要考虑因素。尽管如此，经过一点解释，您就可以理解 sendmail.cf 中控制行的含义。

每个 sendmail 控制行都以一个单字母操作符开头，该操作符定义了行的其余部分的含义。以空格或制表符开头的行被视为前一行的续行。空行和以井号（#）开头的行是注释。

通常，单字母操作符与其后面的参数之间没有空格。这使得行更难理解。例如，sendmail.cf 使用类的概念——本质上是一组短语。您可以使用以下控制行定义名为 P 的类并将短语 REDIRECT 添加到该类中：

```
CPREDIRECT
```

因为一切都混在一起，所以很难解读。另一方面，要定义名为 Accept 的类并将其设置为值 OK 和 RELAY，请写下以下内容：

```
C(Accept)OK RELAY
```

这可能更容易理解一些，因为分隔符（如类名 Accept）被括在大括号中。

其他——更新的——控制行甚至更容易理解。例如，行

```
O HelpFile=/etc/mail/helpfile
```

定义选项 HelpFile 为文件名 /etc/mail/helpfile。该文件包含 sendmail 在收到 HELP 命令时使用的帮助信息。

表 4-1 总结了 sendmail.cf 中使用的单字母控制操作符。每个条目还显示了该操作符的示例。此表应帮助您理解 sendmail.cf 中的一些行。

表 4-1 sendmail.cf 中使用的控制操作符

| Operator | Description |
|---|---|
| C | Defines a class; a variable (think of it as a set) that can contain several values. For example, Cwlocalhost adds the name localhost to the class w. |
| D | Defines a macro, a name associated with a single value. For example, DnMAILER-DAEMON defines the macro n as MAILER-DAEMON. |
| F | Defines a class that's been read from a file. For example, Fw/etc/mail/local-host-names reads the names of hosts from the file /etc/mail/local-host-names and adds them to the class w. |
| H | Defines the format of header lines that sendmail inserts into a message. For example, H?P?Return-Path: <$g> defines the Return-Path: field of the header. |
| K | Defines a map (a key-value pair database). For example, Karith arith defines the map named arith as the compiled-in map of the same name. |
| M | Specifies a mailer. The following lines define the procmail mailer: Mprocmail, P=/usr/bin/procmail, F=DFMSPhnu9, S=EnvFromSMTP/HdrFromSMTP, R=EnvToSMTP/HdrFromSMTP, T=DNS/RFC822/X-Unix, A=procmail -Y -m $h $f $u |

表 4-1（续）

| Operator | Description |
|---|---|
| O | Assigns a value to an option. For example, `O AliasFile=/etc/aliases` defines the AliasFile option to `/etc/aliases`, which is the name of the sendmail alias file. |
| P | Defines values for the precedence field. For example, `Pjunk=-100` sets to -100 the precedence of messages marked with the header field `Precedence: junk`. |
| R | Defines a rule (a rule has a left-hand side and a right-hand side; if input matches the left-hand side, it's replaced with the right-hand side — this is called rewriting). For example, the rewriting rule `R$* ; $1` strips trailing semicolons. |
| S | Labels a ruleset you can start defining with subsequent R control lines. For example, `Scanonify=3` labels the next ruleset as canonify or ruleset 3. |
| T | Adds a user name to the trusted class (class t). For example, `Troot` adds root to the class of trusted users. |
| V | Defines the major version number of the configuration file. For example, `V10/Berkeley` defines the version number as 10. |

## 其他 sendmail 文件

/etc/mail 目录包含 sendmail 使用的其他文件。这些文件在 sendmail 配置文件 /etc/mail/sendmail.cf 中被引用。例如，以下是如何在 /etc/mail/sendmail.cf 文件中搜索 /etc/mail 字符串：

```
grep "\/etc\/mail" /etc/mail/sendmail.cf
```

在我的 Red Hat Linux 系统上，grep 命令搜索结果显示如下：

```
Fw/etc/mail/local-host-names
FR-o /etc/mail/relay-domains
Kmailertable hash -o /etc/mail/mailertable.db
Kvirtuser hash -o /etc/mail/virtusertable.db
Kaccess hash -T<TMPF> -o /etc/mail/access.db
#O ErrorHeader=/etc/mail/error-header
O HelpFile=/etc/mail/helpfile
O StatusFile=/etc/mail/statistics
O UserDatabaseSpec=/etc/mail/userdb.db
#O ServiceSwitchFile=/etc/mail/service.switch
#O DefaultAuthInfo=/etc/mail/default-auth-info
Ft/etc/mail/trusted-users
```

您可以忽略以井号或数字符号（#）开头的行，因为 sendmail 将这些行视为注释。其他行是 sendmail 控制行，引用 /etc/mail 目录中的其他文件。



以下是这些 sendmail 文件应包含的内容（请注意，并非所有这些文件都必须存在于你的 /etc/mail 目录中，即使存在，其中某些文件也可能为空）：

-   `/etc/mail/access` — 允许发送邮件的主机名称和/或 IP 地址（用于阻止垃圾邮件——不需要的邮件）
-   `/etc/mail/access.db` — 从 `/etc/mail/access` 文件生成的访问数据库
-   `/etc/mail/helpfile` — SMTP 命令的帮助信息
-   `/etc/mail/local-host-names` — 主机所知的名称
-   `/etc/mail/mailertable` — 用于覆盖邮件路由方式的邮件传输代理表
-   `/etc/mail/relay-domains` — 允许中继的主机
-   `/etc/mail/trusted-users` — 允许在未警告的情况下使用其他用户名称发送邮件的用户列表
-   `/etc/mail/userdb.db` — 包含每个用户登录名和真实姓名信息的用户数据库文件
-   `/etc/mail/virtusertable` — 在本系统上托管的具有虚拟域地址的用户数据库

## .forward 文件

用户可以通过在其主目录中放置一个 `.forward` 文件来重定向自己的邮件。`.forward` 文件是一个纯文本文件，其中包含以逗号分隔的邮件地址列表。发送给该用户的任何邮件随后会被转发到这些地址。如果 `.forward` 文件包含单个地址，则该用户的所有电子邮件将被重定向到该单个电子邮件地址。例如，假设包含以下行的 `.forward` 文件被放置在名为 `emily` 的用户的主目录中：

```
ashley
```

这会导致 `sendmail` 自动将所有发往 `emily` 的电子邮件发送到同一系统上的用户名 `ashley`。用户 `emily` 根本收不到邮件。

你也可以通过列出完整的电子邮件地址将邮件转发到另一系统上的用户名。例如，我添加了一个 `.forward` 文件，其中包含以下行，以便将我的邮件（发往我的用户名 `naba`）发送到邮件地址 `naba@comcast.net`：

```
naba@comcast.net
```

现在假设我希望在此系统上保留邮件的副本，同时转发到地址 naba@comcast.net。我可以通过向 .forward 文件添加以下行来实现：

```
naba@comcast.net, naba\
```

我只需在其后附加我的用户名并以反斜杠结束该行。行尾的反斜杠（\ ）会阻止 sendmail 反复转发邮件（因为当副本发送到系统上的我的用户名时，sendmail 会再次处理我的 .forward 文件——反斜杠告诉 sendmail 不要重复转发邮件）。

## 在 .forward 文件中调用 procmail

`.forward` 文件的一个有趣用途是运行 procmail 来自动处理某些邮件。例如，假设你想删除任何来自包含字符串 mailing_list 的地址的电子邮件。实现此目的的方法如下：

-   1. 在你的主目录中创建 .forward 文件并在其中放置以下行：

```
| /usr/bin/procmail
```

这一行会导致 sendmail 运行外部程序 /usr/bin/procmail 并将电子邮件消息发送到该程序的输入流。

-   2. 在你的主目录中创建一个名为 .procmailrc 的文本文件并在其中放置以下行：

```
# Delete mail from an address that contains
mailing_list
:0
* ^From:.*mailing_list
/dev/null
```

-   3. 以 root 身份登录并使用以下命令在 /etc/smrsh 中为 /usr/bin/procmail 程序设置符号链接：

```
ln -s /usr/bin/procmail /etc/smrsh/procmail
```

此步骤是必要的，因为 sendmail 使用 Sendmail 受限 Shell——smrsh——来运行外部程序。smrsh 不是运行 /usr/bin/procmail，而是运行 /etc/smrsh/procmail。这就是为什么你需要符号链接的原因。这是 sendmail 的一项安全功能，用于控制其可以运行的外部程序。

就这样！现在，如果你收到任何来自包含 mailing_list 的地址的消息，该消息将被删除。

使用 procmail，你可以执行其他任务，例如自动将消息存储到文件中或将消息转发给他人。你只需在主目录中创建一个合适的 .procmailrc 文件即可。要了解有关 procmail 的更多信息，请输入 man procmail。要查看 .procmailrc 的示例，请输入 man procmailrex。

## sendmail 别名文件

除了 sendmail.cf 文件外，sendmail 还会查阅名为 /etc/aliases 的别名文件以将名称转换为地址。别名文件的位置显示在 sendmail 配置文件中。

每个别名通常是电子邮件地址的较短名称。系统管理员使用 sendmail 别名文件来转发邮件、创建邮件列表（一个标识多个用户的别名）或通过多个不同名称引用用户。例如，以下是一些典型的别名：

```
barkakati: naba
naba: naba@inbsoft
all: naba, leha, ivy, emily, ashley
```

第一行表示发往 barkakati 的邮件应交付给本地系统上的名为 naba 的用户。第二行表示发往 naba 的邮件实际上应发送到 inbsoft 系统上的用户名 naba。最后一行将 all 定义为 naba、leha、ivy、emily 和 ashley 五个用户的别名。这意味着发送给 all 的邮件将发送给这五个用户。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_684_0.png)

在 /etc/aliases 文件中定义任何新别名后，你必须以 root 身份登录并通过输入以下命令使新别名生效：

```
sendmail -bi
```

## 安装新闻服务器

如果你在安装 Red Hat Linux 时安装了新闻服务器，就无需做太多事情即可开始使用新闻服务。否则，你可以使用 Red Hat 软件包管理器（RPM）安装 InterNetNews（INN）——一个基于 TCP/IP 的新闻服务器。

要检查 INN 是否已安装，请输入以下命令：

```
rpm -q inn
```

如果已安装 INN，你应该会看到类似以下的行：

```
inn-2.3.5-4
```

如果收到软件包未安装的消息，你可以从附带的 CD-ROM 手动安装。 以 root 身份登录并将第一张 CD-ROM 插入 CD-ROM 驱动器。如果你使用的是 GNOME 或 KDE 桌面，CD-ROM 应自动挂载。否则，输入以下命令将其挂载：

```
mount /mnt/cdrom
```

然后输入以下命令安装 INN：

```
cd /mnt/cdrom/RedHat/RPMS
```

```
rpm -ivh inn-*
```

## 配置和启动 INN 服务器

随 Red Hat Linux 捆绑的 InterNetNews（INN）软件的大部分在安装 RPM 后即可使用。你需要做的只是稍微熟悉一下 INN 的各个组件，编辑配置文件，然后启动 innd——INN 服务器。顺便说一下，有时我将 INN 服务器称为新闻服务器。

如果你想支持一些互联网新闻组，你还必须安排新闻源——这是你的新闻服务器获取新闻组文章的来源。通常，你可以从 ISP 获取新闻源，但 ISP 会收取额外的月费以覆盖提供源所需的资源成本。你需要提供新闻源的上游服务器名称，并向该服务器提供你的服务器名称和你想要接收的新闻组。

根据你想要接收的新闻组和你想要保留文章的天数，你必须预留适当的磁盘空间来存放文章。新闻组以基于新闻组名称的目录层次结构存储在系统的 /var/spool/news 目录中。如果你正在设置新闻服务器，你可能希望为 /var/spool/news 目录分配一个较大的磁盘分区。

在你的新闻服务器的配置文件中，输入提供新闻源的服务器名称。同时，将接收来自你的服务器新闻源的任何下游新闻服务器（如果有）的名称添加到配置文件中。然后你可以启动新闻服务器并等待新闻到达。监控日志文件以确保新闻文章在系统的 /var/spool/news 目录中被正确排序和存储。

当新闻运行起来后，你必须运行新闻维护和清理脚本。这些脚本使用 cron 作业运行。在 Red Hat Linux 上，已经设置了一个 cron 作业来运行 /usr/bin/news.daily 脚本来执行新闻维护任务。



在以下章节中，我将向您介绍 INN 的设置，但您也可以从 Internet Software Consortium（ISC）了解更多关于 INN 的信息，ISC 是一个致力于开发和维护开源 Internet 软件的非营利公司，例如 BIND（域名系统的一种实现）、DHCP（动态主机配置协议）和 INN。Rich Salz 最初编写了 INN；ISC 于 1996 年接管了 INN 的开发工作。您可以在 ISC 的 INN 网页 www.isc.org/products/INN 上了解更多关于 INN 的信息并访问其他资源。

## InterNetNews 组件

INN 包含多个用于投递和管理新闻组的程序。它还包含许多控制 INN 程序如何工作的文件。最重要的 INN 程序如下：

- `innd` — 新闻服务器。它作为 `daemon` 运行 — 一个保持运行以提供特定服务的后台进程 — 并监听 NNTP 端口（TCP 端口 119）。`innd` 服务器接受来自其他馈送站点的连接，以及来自本地新闻阅读器客户端的连接，但它会将本地连接交给 `nnrpd`。
- `nnrpd` — 由 `innd` 调用的特殊服务器，用于处理来自本地新闻阅读器客户端的请求。
- `expire` — 根据文本文件 `/etc/news/expire.ctl` 中的规范删除旧文章。
- `nntpsend` — 调用 `innxmit` 程序，使用 NNTP 将新闻文章发送到远程站点。配置文件 `/etc/news/nntpsend.ctl` 控制 `nntpsend` 程序。
- `ctl innd` — 使您能够交互式地控制 `innd` 服务器。`ctl innd` 程序可以向 `innd` 服务器的控制通道发送消息。

INN 的其他重要组件是控制文件。这些文件大多数位于 Red Hat Linux 系统的 `/etc/news` 目录中，尽管其中一些位于 `/var/lib/news` 目录中。在这两个目录之间，您拥有超过 30 个 INN 控制文件。一些重要文件包括以下内容：

- `/etc/news/inn.conf` — 指定 `innd` 服务器的配置数据。（要查看此文件的在线帮助，请输入 `man inn.conf`。）
- `/etc/news/newsfeeds` — 指定要向下馈送到其他新闻服务器的文章。（该文件很复杂，但您可以通过输入 `man newsfeeds` 获得帮助。）
- `/etc/news/incoming.conf` — 列出为此服务器提供新闻馈送的主机的名称和地址。（要查看此文件的在线帮助，请输入 `man incoming.conf`。）
- `/etc/news/storage.conf` — 指定存储新闻文章时使用的存储方法。（要查看此文件的在线帮助，请输入 `man storage.conf`。）
- `/etc/news/expire.ctl` — 按需按新闻组级别控制文章的过期。（要查看此文件的在线帮助，请输入 `man expire.ctl`。）
- `/var/lib/news/active` — 列出所有活动新闻组，显示每个新闻组的最新和最旧文章编号，以及每个新闻组的发帖状态。（要查看此文件的在线帮助，请输入 `man active`。）
- `/var/lib/news/newsgroups` — 列出新闻组，并附带每个新闻组的简要描述。
- `/etc/news/readers.conf` — 指定允许从此新闻服务器读取新闻并向新闻组发帖的主机和用户。默认文件仅允许 `localhost` 读取新闻；如果您希望允许本地局域网中的其他主机读取新闻，则必须对其进行编辑。（要查看此文件的在线帮助，请输入 `man readers.conf`。）

在接下来的几个章节中，我将描述如何设置一些重要的控制文件。

## The inn.conf 文件

此文件保存所有 INN 程序的配置数据 — 这使其成为最重要的文件。文件的每一行都以以下格式给出参数的值：

```
parameter:    value
```

根据参数的不同，值是字符串、数字，或 true 或 false。与许多其他配置文件一样，注释行以井号（#）开头。

/etc/news 目录中默认 inn.conf 文件中的大多数参数不需要更改。您可能希望编辑表 4-2 中显示的一个或多个参数。

**表 4-2 /etc/news/inn.conf 中的配置参数**

| 参数名称 | 描述 |
|---|---|
| mta | 将其设置为 innd 用于传输消息的邮件传输代理。默认使用 sendmail。 |
| organization | 将其设置为您希望出现在系统发布的所有新闻文章的 Organization: 头部中的组织名称。用户可以通过定义 ORGANIZATION 环境变量来覆盖此设置。 |
| ovmethod | 设置概览存储方法类型（概览是新闻组中新闻文章的索引）。默认方法是 tradindexed，读取新闻速度快，但存储新闻项速度慢。 |
| pathhost | 将其设置为您希望出现在通过服务器的所有帖子的 Path 头部中的新闻服务器名称。如果未定义 pathhost，则使用系统的完全限定域名。 |
| pathnews | 将其设置为包含 INN 二进制文件和库的目录的完整路径名。在 Red Hat Linux 中，pathnews 设置为 /usr/lib/news。 |
| domain | 将其设置为服务器的域名。 |
| allownewnews | 如果您希望 INN 支持新闻阅读器的 NEWNEWS 命令，则将其设置为 true。由于此命令会大幅降低服务器性能，INN 文档建议将其设置为 false。 |
| storageapi | 如果您希望使用存储管理器 API（应用程序编程接口）存储文章，则将其设置为 true。默认设置为 false 会导致 INN 使用传统的文章存储方法，即每个文件存储一篇文章。如果将其设置为 true，您必须在存储方法 timehash 和 cnfs 之间进行选择，并且必须创建新的 spool 和数据库文件（输入 man storage.conf 以了解有关 cnfs 和 timehash 存储方法的更多信息）。对于少量新闻组，您可以将此选项保留为默认值 false。 |
| hiscachesize | 将其设置为 INN 用于缓存最近使用的历史文件条目的大小（以千字节为单位）。默认设置为 0 会禁用历史缓存。由于历史缓存可以大幅提高服务器每秒处理的文章数量，您可能希望将其设置为 16384（即 16MB）。 |
| innflags | 将其设置为启动时希望传递给 INN 服务器进程的任何标志。 |

## The newsfeeds 文件

newsfeeds 文件指定传入新闻文章如何重新分发到其他服务器和 INN 进程。如果您向其他服务器提供新闻馈送，则必须在此文件中列出这些新闻馈送。（您还必须有一个标记为 ME 的条目，我将在本节后面解释其特殊用途。）

newsfeeds 文件包含一系列条目，每个馈送一个。每个馈送条目具有以下格式：

```
site[/exclude,exclude...]
:pattern.pattern...[/distrib,distrib...]\
:flag,flag...\
:param
```

每个条目有四个由冒号（:）分隔的字段。通常，条目跨越多行，并且行尾的反斜杠（\ ）用于将行继续到下一行。以下是四个字段的含义：

- 第一个字段 site 是馈送的名称。每个名称必须唯一，对于发送到其他新闻服务器的馈送，名称设置为远程服务器的主机名。名称后面是一个可选的斜杠和一个排除列表（/exclude,exclude...），由一系列名称组成。如果文章的 Path 行中出现此列表中的任何名称，则该文章不会被转发到该馈送。如果您不希望接收来自特定来源的文章，可以使用排除列表。
- 第二个字段由一组以逗号分隔的新闻组模式组成，例如 *@alt.binaries.warez.*,!control*,!local*，后面跟一个可选的分发列表。分发列表是一组以逗号分隔的关键字，每个关键字指定文章将被分发的特定站点集。新闻组模式本质上定义了接收此新闻馈送的站点的订阅列表。星号匹配所有新闻组。以 @ 开头的模式会导致匹配该模式的新闻组被丢弃。以感叹号（!）开头的模式表示匹配的新闻组不发送。顺便说一下，INN 配置文件中使用的一种简单的模式匹配语法称为 wildmat 模式。
- 第三个字段是以逗号分隔的标志列表 — 这些字段确定馈送条目类型并为条目设置某些参数。有许多标志；输入 man newsfeeds 并阅读手册页以了解有关标志的更多信息。
- 第四个字段用于参数，其值取决于第三个字段中的设置。通常，此字段包含 INN 服务器使用的文件名或外部程序的名称。您可以在 newsfeeds 手册页中了解有关此字段的更多信息。

现在您知道了 /etc/news/newsfeeds 文件的布局，您可以将其作为示例进行研究。默认文件包含许多示例馈送条目，但只有两个被注释掉了：

- ME 是一个始终必需的特殊馈送条目。它有两个用途。首先，此条目中列出的新闻组模式会被添加到所有


所有其他条目中的新闻组模式。第二，ME 条目的分发列表决定了你的服务器从远程站点接受的分发内容。

- controlchan feed 条目用于设置 INN，使其使用外部程序来处理控制消息（这些消息用于创建新的新闻组和删除组）。例如，以下 controlchan 条目指定外部程序 /usr/lib/news/bin/controlchan 来处理所有控制消息，除了取消消息（用于取消文章）：

```
controlchan!
:!*!,control.control.*,!control.cancel\
:Tc,WnSm:/usr/lib/news/bin/controlchan
```

除这些 feed 条目外，你还要为新闻服务器提供新闻馈送的任何实际站点添加条目。此类条目的格式为

```
feedme.domain.com
:ljunk,!control/!foo\
:Tm:innfeed!
```

其中 feedme.domain.com 是你的系统向其发送新闻文章的站点的完全限定域名。

## The incoming.conf file

incoming.conf 文件描述哪些主机被允许连接到你的主机以馈送文章。对于单个馈送，你可以添加如下条目

```
peer mybuddy {
  hostname: a-feed-site.domain.com
}
```

其中 mybuddy 是对等体的标签，a-feed-site.domain.com 标识馈送你的站点的站点。

![](img/a7eec43a54473e95dc5ea333fec1bd7_690_0.png)

请记住，仅仅在 incoming.conf 文件中添加站点的名称并不会导致该远程站点开始向你的站点馈送新闻——它只是使你的服务器能够从远程站点接受新闻文章。在远程站点，你的朋友必须配置他的或她的服务器以向你的站点发送文章。

## The readers.conf file

此文件指定新闻阅读器客户端（如 Mozilla）可以从中检索新闻组的的主机名或 IP 地址。例如，以下 readers.conf 文件允许从 localhost 以及网络 192.168.0.0 中的任何主机进行读取访问和发布访问（意味着你可以提交文章）：

```
auth "localhost" {
  hosts: "localhost, 127.0.0.1, stdin"
  default: "<localhost>"
}
access "localhost" {
  users: "<localhost>"
  newsgroups: "**"
  access: RPA
}
auth "localnet" {
  hosts: 192.168.0.0/24
  default: "<localnet>"
}
access "localnet" {
  users: "<localnet>"
  newsgroups: "**"
  access: RPA
}
```

## InterNetNews startup

除了配置文件之外，你还必须启动执行新闻服务器定期维护的 cron 作业。在 Red Hat Linux 中，这些 cron 作业已经设置好。因此，你现在可以启动 INN 服务器——innd。

在启动 innd 之前，你必须运行 makehistory 和 makedbz 以初始化并重建 INN 历史数据库。输入 man makehistory 和 man makedbz 以了解有关这些命令的更多信息。输入以下命令以创建初始历史数据库、相关索引，并设置某些文件的属主和权限：

/usr/lib/news/bin/makehistory -b -f history -0 -l 30000 -I
cd /var/lib/news
/usr/lib/news/bin/makedbz -s 'wc -l < history' -f history
chown news.news *
chown news.news /var/spool/news/overview/group.index
chmod 664 /var/spool/news/overview/group.index

与 Red Hat Linux 中的其他服务器一样，要启动 innd，请以 root 身份登录并输入以下命令：

```
service innd start
```

要确保 inn 在启动时启动，输入以下命令：

```
chkconfig --level 35 inn on
```

![](img/a7eec43a54473e95dc5ea333fec1bd7_692_0.png)

如果更改任何配置文件（如 inn.conf 或 newsfeeds），请使用以下命令重新启动 inn 服务器：

```
service inn restart
```

输入 ps ax 以查看 inn 进程是否正在运行。如果一切顺利，你应该在 ps ax 命令的输出中看到两个类似以下的过程：

```
23789 ? S 0:00 /usr/lib/news/bin/inn -p4
23794 ? S 0:00 /usr/bin/perl /usr/lib/news/bin/controlchan
```

![](img/a7eec43a54473e95dc5ea333fec1bd7_692_1.png)

 /var/log/spooler 文件包含来自 inn 的所有状态和错误消息。输入以下命令以查看该文件中的最后几条消息：

```
tail /var/log/spooler
```

## Setting Up Local Newsgroups

如果你想使用新闻组作为在公司内部共享信息的一种方式，可以设置本地新闻组层次结构。然后你可以使用这些新闻组在公司内部创建虚拟社区，让有共同兴趣的人可以非正式地讨论问题并交流知识。

## Defining a newsgroup hierarchy

第一步是定义新闻组层次结构并决定每个新闻组将讨论什么内容。例如，如果你的公司名称是 XYZ Corporation，以下是你可以定义的新闻组层次结构的局部内容：

- `xyz.general` — 关于 XYZ Corporation 的一般事项
- `xyz.weekly.news` — 每周新闻
- `xyz.weekly.menu` — 每周食堂菜单及相关讨论
- `xyz.forsale` — 员工出售物品的清单
- `xyz.jobs` — XYZ Corporation 的职位空缺
- `xyz.wanted` — 员工发布的求助、求购等信息
- `xyz.technical.hardware` — 关于硬件的技术讨论
- `xyz.technical.software` — 关于软件的技术讨论

## Updating configuration files

以下是更新本地新闻组的配置文件然后重新启动新闻服务器的步骤：

1. 向 /var/lib/news/newsgroups 文件中为每个新闻组添加描述性条目。

以下是默认 /var/lib/news/newsgroups 文件中的条目：

```
control          Various control messages (no posting).
control.cancel   Cancel messages (no posting).
control.checkgroups  Hierarchy check control messages (no posting).
control.newgroup Newsgroup creation control messages (no posting).
control.rmgroup  Newsgroup removal control messages (no posting).
junk             Unfiled articles (no posting).
```

向此文件为每个本地新闻组添加一行——输入其名称，后跟简要描述。例如，你可以为 xyz.general 新闻组添加以下内容：

```
xyz.general   General items about XYZ Corporation
```

2. 编辑 /etc/news/newsfeeds 文件中的 ME 条目，并在新闻组模式的逗号分隔列表中添加短语 !xyz.*。

这可确保你的本地新闻组不会在站点外分发。

3. 添加将用于本地新闻组的存储方法。

例如，你可以在 /etc/news/storage.conf 中添加以下行来定义新的 xyz 新闻组层次结构的存储方法（将 xyz 更改为你为本地新闻组命名的名称）：

```
method tradspool {
    class: 1
    newsgroups: xyz.*
}
```

4. 要使这些更改生效，请使用以下命令重新启动新闻服务器：

```
service inn restart
```

## Adding the newsgroups

最后一步是添加新闻组。在配置文件更新并 `inn` 正在运行后，添加本地新闻组非常容易。以 `root` 身份登录并使用 `ctlinnd` 执行此任务。例如，以下是如何添加名为 `xyz.general` 的新闻组：

/usr/lib/news/bin/ctlinnd newgroup xyz.general

就这样！该命令将 `xyz.general` 新闻组添加到你的站点。如果你使用传统存储方法，`inn` 服务器会创建目录 `/var/spool/news/articles/xyz/general` 并将该新闻组的文章存储在该目录中（这发生在有人首次向该新闻组发布新闻文章时）。

在创建所有本地新闻组后，你的内联网用户应该能够发布新闻文章并在本地新闻组中阅读文章。如果他们访问新闻组时遇到问题，请确保 `/etc/news/readers.conf` 文件包含应能够访问 `inn` 服务器的主机的 IP 地址或名称。

## Testing your newsgroups

例如，我使用上一节中解释的说明，在我的 Red Hat Linux 系统上运行的 INN 服务器上添加了一个名为 `local.news` 的新闻组。然后我在局域网上的另一台 Red Hat Linux 系统上启动 Mozilla，并设置一个新的新闻帐户，将新闻服务器设置为我的 INN 服务器。接下来，我通过输入 `news:local.news` 作为 URL 来访问 `local.news` 新闻组。试试看！我敢打赌你会喜欢的。



### 第5章：设置 DNS 和 NIS
### 本章内容
- ✔ 了解 DNS
- ✔ 了解 BIND
- ✔ 配置 DNS
- ✔ 设置缓存名称服务器
- ✔ 配置主名称服务器
- ✔ 了解 NIS
- ✔ 配置 NIS 服务器和客户端
- ✔ 尝试使用 NIS

域名系统（DNS）是一种 Internet 服务，它将完全限定域名（如 www.redhat.com）转换为对应的 IP 地址（如 216.148.218.195）。你可以将 DNS 视为 Internet 主机的目录——正是因为 DNS，你可以使用易于记忆的主机名，即使 TCP/IP 在数据传输中需要数字 IP 地址。DNS 基本上是一个分布式的 DNS 服务器层级结构。在本章中，我将概述 DNS，并向您展示如何在 Red Hat Linux 系统上设置缓存 DNS 服务器。

网络信息系统（NIS）是另一项客户端/服务器服务，旨在管理网络上多个主机计算机之间共享的信息。通常，NIS 在局域网（LAN）上的一组主机为 UNIX 或 Linux 系统维护一组公共的用户账户和其他系统文件。此服务等使用户能够使用相同的用户名和密码登录所有主机。本章简要介绍了 NIS 客户端和服务器软件，并向您展示如何在 Red Hat Linux 系统上使用它们。

### 了解域名系统（DNS）
在 TCP/IP 网络中，每个网络接口（例如以太网卡或拨号调制解调器连接）都由一个 IP 地址标识。由于 IP 地址难以记忆，因此会为 IP 地址分配一个易于记忆的名称——就像电话号码与姓名相对应一样。例如，您无需记住 Red Hat Web 服务器的 IP 地址为 216.148.218.195，只需通过其名称 www.redhat.com 来引用该主机即可。当您在 Web 浏览器中输入 www.redhat.com 作为 URL 时，该名称必须被翻译成对应的 IP 地址。这就是 DNS 概念发挥作用的地方。

### 什么是 DNS？
域名系统是一个分布式、分层的数据库，用于保存有关 Internet 上计算机的信息。这些信息包括主机名、IP地址和邮件路由规范。由于这些信息存储在 Internet 上的许多 DNS 主机中，因此 DNS 被称为分布式数据库。DNS 的主要任务是将主机名与 IP 地址关联起来，反之亦然。

在 ARPANET——当今 Internet 的前身——主机名及其对应 IP 地址的列表保存在名为 HOSTS.TXT 的文本文件中，该文件由中央管理并定期分发给网络上的每台主机。随着主机数量的增长，维护这张静态主机表很快变得不合理。Paul Mockapetris 提出了 DNS 以缓解静态主机表的问题。正如在请求评论（RFC）882 和 883 中正式记录的那样（1983 年 11 月发布，参见 www.faqs.org/rfcs/rfc882.html 和 www.faqs.org/rfcs/rfc883.html），原始 DNS 引入了两个关键概念：
- 使用分层域名，例如 www.ee.umd.edu 和 www.redhat.com
- 通过在整个 Internet 上使用 DNS 服务器来分担管理主机数据库的责任

我们今天所知的 DNS 是一项在 RFC 1034 和 1035 中记录的 Internet 标准。该标准已被其他多个 RFC 更新和扩展——1101、1183、1348、1876、1982、1996、2065、2181、2136、2137、2308、2535、2845 和 2931。较早的更新定义了数据编码，而较新的更新则侧重于改进 DNS 安全。要在线阅读这些和其他 RFC，请访问俄亥俄州立大学的 Internet RFC 页面，网址为：

```
www.cis.ohio-state.edu/hypertext/information/rfc.html
```

DNS 定义了以下内容：
- 用于主机的分层域名系统。
- 一个将每个域名与 IP 地址关联的分布式数据库。
- 库例程（解析器），网络应用程序可使用它来查询分布式 DNS 数据库。（该库称为 *resolver library*。）
- DNS 客户端和服务器之间交换名称和 IP 地址信息的协议。

如今，Internet 上的所有主机都依赖 DNS 来访问远程主机上的各种 Internet 服务。正如您从个人经验中可能知道的那样，当您从 Internet 服务提供商（ISP）获得 Internet 访问权限时，您的 ISP 会为您提供名称服务器的 IP 地址——每当主机名需要映射到 IP 地址时，您的系统就会访问这些 DNS 服务器。

如果您有一个小型局域网，您可以决定在一台主机上运行 DNS 服务器，或使用 ISP 提供的名称服务器。对于使用多个子网的中型网络，您可以在每个子网上运行 DNS 服务器以提供高效的 DNS 查找。在大型企业网络中，企业域（如 microsoft.com）会进一步细分为子域层级；每个子域中可能会使用多个 DNS 服务器。

在下面的章节中，我将概述分层域名命名约定，并介绍 BIND——在大多数 UNIX 系统（包括 Red Hat Linux）上使用的 DNS 软件。

### 学习分层域名
DNS 使用域的层次树来组织命名空间——整个名称集合。每个更高级别的域对其下级子域具有管理权限。每个域代表命名空间的一个独立块，并由单一的管理机构管理。图 5-1 说明了 DNS 命名空间的层次组织。

Figure 5-1:
The DNS namespace is organized in a hierarchy.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_698_0.png)

树的根称为根域，由一个点（.）表示。接下来是顶级或根级域。顶级域进一步细分为二级域，而二级域又可以细分为更低的子域。

顶级域相对固定，包括众所周知的域，如 COM、NET、ORG、EDU、GOV 和 MIL。这些是美国常用的顶级域。这些顶级域是在 20 世纪 90 年代初 Internet 普及时出现的。

还有一组用于国家的顶级域名。这些域名使用国际标准化组织（缩写为 ISO；参见 www.iso.ch）分配的两字母国家代码。例如，美国的顶级国家代码域是 US。在美国，许多地方政府和组织使用 US 域。例如，mcps.k12.md.us 是美国马里兰州蒙哥马利县公立学校的域名。

完全限定域名（FQDN）是通过将子域名从低级到高级串联起来，使用点（.）作为分隔符构造的。例如，REDHAT.COM 是一个完全限定域名；EE.UMD.EDU 也是如此。请注意，这些也可能指特定的主机计算机。图 5-2 说明了完全限定域名的组成部分。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_699_0.png)

域名不区分大小写。因此，就 DNS 而言，域 UMD.EDU 和 umd.edu 都代表马里兰大学的域。然而，通常的做法是以全小写输入域名。

### 探索伯克利 Internet 域名（BIND）
大多数 UNIX 系统，包括 Red Hat Linux，都附带 BIND 系统——一种众所周知的 DNS 实现。只要在选择安装包时选择 DNS 名称服务器包组，BIND 软件就会在 Red Hat Linux 安装期间安装。

要查看 Red Hat Linux 系统上安装的 BIND 版本，请键入以下命令：

```
rpm -q bind
```

如果安装了 BIND，此命令应显示类似以下的行，其中包含 RPM 文件的版本号：

```
bind-9.2.2-19
```

正如此输出所示，我的系统上安装了 BIND 版本 9.2.2。

BIND 包含三个主要组件：
- The named daemon — the name server — that responds to queries about host names and IP addresses
- A resolver library that applications can use to resolve host names into IP addresses (and vice versa)
- Command line DNS utility programs (DNS clients), such as dig (Domain Internet Groper) and host that users can use to query DNS

我将在接下来的几节中描述 BIND 的这些组件。在后面的章节中，我将解释如何配置解析器和名称服务器。

### named — BIND 名称服务器
named 守护进程是响应主机名和 IP 地址查询的名称服务器。根据配置文件和本地 DNS 数据库，named 要么提供查询的答案，要么向其他服务器查询并缓存其响应。named 服务器还执行称为区域传输的功能，该功能涉及在域中的名称服务器之间复制数据。

名称服务器以三种模式之一运行：
- Primary or Master — In this case, the name server keeps the master copy of the domain's data on disk. There is one primary server for each domain or subdomain.
- Secondary or Slave — A secondary name server copies its domain's data from the primary server using a zone transfer operation. You can have one or more secondary name servers for a domain.
- Caching — A caching name server loads the addresses of a few authoritative servers for the root domain and gets all domain data by caching responses to queries it has resolved by contacting other name servers. Primary and secondary servers also cache responses.



![](img/a7eec43a54473e95dc5ea333fecf1bd7_701_0.png)

名称服务器可以是权威的也可以不是，这取决于它提供的信息。顾名思义，权威名称服务器的响应应该是准确的。主名称服务器和辅助名称服务器对其各自的域是权威的，但对于从缓存信息提供的响应则不是权威的。

缓存名称服务器永远不是权威的，因为它们的所有响应都来自缓存信息。

要在 Red Hat Linux 系统上运行名称服务器，必须使用适当的配置文件运行 named。本章后面将介绍控制名称服务器操作的配置文件和数据文件。

## Resolver library

查找主机名的 IP 地址称为解析主机名。网络感知应用程序，例如 Web 浏览器或 FTP 客户端，使用解析器库来执行从名称到 IP 地址的转换。根据 /etc/host.conf 文件中的设置，解析器库会查阅 /etc/hosts 文件或进行 DNS 查询以将主机名解析为其 IP 地址。解析器库查询 /etc/resolv.conf 文件中列出的名称服务器。

除非您正在编写网络感知应用程序，否则您不需要了解太多关于解析器库的知识。要正确运行 Internet 服务，您只需要知道如何配置解析器。本章后面我将向您展示如何配置此项以及 DNS 的其他方面。

## DNS utility programs

您可以使用 DNS 实用程序 — dig 和 host — 从 shell 提示符交互式地尝试 DNS。这些实用程序是 DNS 客户端。您可以使用它们查询 DNS 数据库并调试系统上可能设置的任何名称服务器。默认情况下，这些程序查询系统 /etc/resolv.conf 文件中列出的名称服务器。

您可以使用 dig，即 Domain Internet Groper 程序，来查找域名对应的 IP 地址或反之。例如，要查找 ftp.redhat.com 的 IP 地址，请输入

```
dig ftp.redhat.com
```

dig 会以大量细节打印 DNS 查询的结果。请查看标记为 ANSWER SECTION: 的输出部分以获取结果。例如，该部分在此示例查询中的显示如下：

```
;; ANSWER SECTION:
ftp.redhat.com. 300 IN A 66.187.232.30
```

使用 dig 进行 *反向查找*（为 IP 地址查找主机名）也很简单。例如，要查找 IP 地址 66.187.232.30 对应的主机名，请输入以下内容：

```
dig -x 66.187.232.30
```

同样，答案出现在输出的 ANSWER SECTION: 中，对于此示例，其显示如下：

```
;; ANSWER SECTION:
30.232.187.66.in-addr.arpa. 539 IN PTR ftp.redhat.com.
```

在这种情况下，IP 地址 66.187.232.30 对应的主机名恰好是 ftp.redhat.com。

您也可以使用 host 程序查询 DNS。host 程序以紧凑的格式生成输出。例如，以下是使用 host 查找主机名 IP 地址的典型用法：

```
host www.gao.gov
```

这会生成以下单行输出：

```
www.gao.gov has address 161.203.16.2
```

默认情况下，host 会打印 IP 地址和任何 MX 记录（这些记录列出主机邮件处理程序的名称）。

对于反向查找，使用 -t ptr 选项，并将 IP 地址作为参数，如下所示：

```
host -t ptr 161.203.16.2
```

以下是 host 的输出：

```
2.16.203.161.in-addr.arpa. domain name pointer www.gao.gov.
```

这表明 www.ee.umd.edu 的规范名称（或别名）是 edison.eng.umd.edu。

## Configuring DNS

您通过使用多个配置文件来配置 DNS。确切的文件集取决于您是否运行名称服务器，以及如果是，则名称服务器的类型 — 缓存或主服务器。无论是否运行名称服务器，一些配置文件都是必需的。

## Configuring the resolver

您无需在系统上运行名称服务器即可使用 DNS 客户端（dig 和 host）。您可以使用它们查询您域的名称服务器。通常，您的 ISP 会为您提供此信息。您必须在 /etc/resolv.conf 文件中列出这些名称服务器的 IP 地址 — 解析器库读取此文件以确定如何解析主机名。此文件的格式为

```
domain your-domain.com
search your-domain.com
nameserver A.B.C.D
nameserver X.Y.Z.W
```

其中 A.B.C.D 和 X.Y.Z.W 是您的 ISP 为您提供的首选和次选名称服务器的 IP 地址（点分隔的数字地址，例如 192.168.0.1）。

domain 行列出本地域名。search 行指定首先搜索主机名的域（通常，您将自己的域放在 search 行中）。在解析器库尝试解析它之前，search 行中列出的域会被附加到任何主机名。例如，如果您查找名为 mailhost 的主机，解析器库首先尝试 mailhost.your-domain.com；如果失败，则尝试 mailhost。search 行适用于您尝试访问的任何主机名。例如，如果您尝试访问 www.redhat.com，解析器首先尝试 www.redhat.com.your-domain.com，然后尝试 www.redhat.com。

另一个重要的配置文件是 /etc/host.conf — 此文件告诉解析器在尝试解析主机名时该怎么做。典型的 /etc/host.conf 文件包含以下行：

```
order hosts,bind
```

这告诉解析器首先查阅 /etc/hosts 文件，如果失败，则查询 /etc/resolv.conf 文件中列出的名称服务器。/etc/hosts 文件通常列出任何本地主机名及其 IP 地址。以下是 /etc/hosts 文件中的典型行：

```
127.0.0.1    lnbp200  localhost.localdomain  localhost
```

此行表示 IP 地址 127.0.0.1 分配给主机名 lnbp200、localhost.localdomain 和 localhost。

在使用 GNU C 库版本 2（glibc 2）或更高版本的最新 Linux 内核版本中，名称服务切换（NSS）文件 /etc/nsswitch.conf 控制解析器库、NIS、NIS+ 以及 /etc/hosts 和 /etc/shadow 等本地文件等服务如何交互。例如，/etc/nsswitch.conf 文件中的以下 hosts 条目指定解析器库应首先尝试 /etc/hosts 文件，然后尝试 NIS+，最后尝试 DNS：

```
hosts:      files nisplus dns
```

要了解有关 /etc/nsswitch.conf 文件及其功能的更多信息，请在终端窗口中输入 info libc "Name Service Switch"。

## Configuring a caching name server

一种简单但有用的名称服务器是使用其他名称服务器找到主机名查询的答案，然后在下次需要时记住答案（通过将其保存在缓存中）的名称服务器。这种缓存名称服务器可以缩短访问最近访问过的主机所需的时间；答案已在缓存中。

当您在 Red Hat Linux 安装期间安装 DNS Name Server 软件包组时，缓存名称服务器的配置文件也会被安装。这意味着您可以在几乎不费力的情况下开始运行缓存名称服务器。本节描述配置文件以及启动缓存名称服务器需要执行的操作。

## The /etc/named.conf file

您需要的第一个配置文件是 /etc/named.conf。named 服务器在启动时读取此配置文件。如果您在 Red Hat Linux 安装期间安装了 DNS Name Server，则您已拥有此文件。以下是默认 /etc/named.conf 文件的内容：

// generated by named-bootconf.pl
options {
    directory "/var/named";
};
* If there is a firewall between you and nameservers you want
* to talk to, you might need to uncomment the query-source
* directive below. Previous versions of BIND always asked
* questions using port 53, but BIND 8.1 uses an unprivileged
* port by default.
// query-source address * port 53;
};
//
// a caching only nameserver config
//
controls {
  inet 127.0.0.1 allow { localhost; } keys { rndckey; };
};
zone "." IN {
  type hint;
  file "named.ca";
};
zone "localhost" IN {
  type master;
  file "localhost.zone";
  allow-update { none; };
};
zone "0.0.127.in-addr.arpa" IN {
  type master;
  file "named.local";
  allow-update { none; };
};
include "/etc/rndc.key";

注释采用 C 风格（/* ... */）或 C++ 风格（以 // 开头）。文件包含用大括号（{ ... }）括起并以分号（；）结尾的块语句。块语句反过来包含其他语句，每个语句以分号结尾。

此 /etc/named.conf 文件以包含多个选项语句的 options 块语句开始。directory 选项语句告诉 named 在配置文件中 file 行出现的所有其他文件的位置。在这种情况下，named 在 /var/named 目录中查找文件。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_705_0.png)

 /etc/named.conf 中的 controls 语句包含安全信息，以便 rndc 命令可以连接到端口 953 上的 named 服务并与 named 交互。在这种情况下，controls 语句包含以下行：

```
inet 127.0.0.1 allow { localhost; } keys { rndckey; };
```

这表示 rndc 可以使用名为 rndckey 的密钥从 localhost 连接；文件 /etc/rndc.key 定义了密钥和要使用的加密算法。



![](img/a7eec43a54473e95dc5ea333fecf1bd7_706_0.png)

rndc（remote name daemon control，远程名称守护进程控制）实用程序是较旧的 ndc（name daemon controller，名称守护进程控制器）实用程序的后继者，用于通过特殊控制通道向 named 服务器发送消息来控制它，该通道是一个 TCP 端口，named 在此端口监听消息。rndc 实用程序使用加密密钥将其自身认证给 named 服务器。named 服务器具有相同的加密密钥，以便它可以解码 rndc 发送的认证信息。

在 options 语句之后，/etc/named.conf 文件包含多个区域语句，每个区域语句都用大括号括起来并以分号结尾。每个区域语句定义一个区域。第一个区域名为 “.”（根区域）；它是一个提示区域，指定根名称服务器。

/etc/named.conf 中的接下来两个区域语句是主区域。对于 Internet 类区域（由 IN 关键字表示）的主区域语句的语法如下：

```
zone "zone-name" IN {
    type master;
    file "zone-file";
    [...other optional statements...]
};
```

zone-name 是区域的名称，zone-file 是包含该区域的资源记录（RR）——数据库条目——的区域文件。我将在接下来的两个部分描述区域文件格式和资源记录格式。

## 区域文件格式

区域文件通常以若干指令开头，每个指令都以美元符号（$）后跟一个关键字开始。两个常用的指令是 $TTL 和 $ORIGIN。

例如，行

```
$TTL  86400
```

使用 $TTL 指令为后续未定义 TTL 的记录设置默认生存时间（TTL）。值以秒为单位，有效 TTL 范围为 0 到 2147483647 秒。在此情况下，该指令将默认 TTL 设置为 86400 秒（或一天）。

$ORIGIN 指令设置将附加到任何未限定记录的域名。例如，以下 $ORIGIN 指令将域名设置为 localhost：

```
$ORIGIN localhost.
```

如果没有 $ORIGIN 指令，初始 $ORIGIN 与 /etc/named.conf 文件中 zone 关键字之后出现的区域名称相同。

在指令之后，区域文件包含一个或多个资源记录。这些记录遵循特定格式，在下一节中概述。

## 资源记录（RR）格式

在你能够理解并智能地处理区域文件之前，你必须了解资源记录的格式。每个资源记录具有以下格式（可选字段用方括号显示）：

```
[domain] [ttl] [class] type data [;comment]
```

字段由制表符或空格分隔，并且可能包含一些特殊字符，例如用于域的 @ 符号和用于指示注释开始的分号（;）。

第一个字段必须从行的第一个字符开始，标识域名。你可以使用 @ 符号使用当前 $ORIGIN 作为此记录的域名。如果同一域名有多个记录，请将第一个字段留空。

可选的 ttl 字段指定生存时间——数据可以被缓存并被视为有效的时间。你可以用以下格式之一指定持续时间：

- N，其中 N 为数字，表示 N 秒
- NW，其中 N 为数字，表示 N 周
- ND，其中 N 为数字，表示 N 天
- NH，其中 N 为数字，表示 N 小时
- NM，其中 N 为数字，表示 N 分钟
- NS，其中 N 为数字，表示 N 秒

字母 W、D、H、M 和 S 也可以小写。因此，你可以写 86400 或 1D（或 1d）来表示一天的持续时间。你还可以组合这些来指定更精确的持续时间，例如 5w6d16h 表示 5 周、6 天和 16 小时。

class 字段指定网络类型。此字段最常用的值是 IN，表示 Internet。

资源记录中接下来是 type 字段，它表示记录的类型（例如 SOA、NS、A 或 PTR）。表 5-1 列出了 DNS 资源记录类型。接下来是 data 字段，它取决于 type 字段。

### 表 5-1 DNS 资源记录类型

| 类型 | 名称 | 描述 |
|------|------|------|
| SOA | Start of Authority | 表示此后所有记录对此区域具有权威性。 |
| NS | Name Server | 标识区域的权威名称服务器。 |
| A | Address | 指定与主机名对应的 IP 地址。 |
| PTR | Pointer | 指定与地址对应的名称（用于反向映射——将 IP 地址转换为主机名）。 |
| MX | Mail Exchanger | 标识接受发往域的邮件的主机（用于路由电子邮件）。 |
| CNAME | Canonical Name | 定义主机名的昵称或别名。 |
| KEY | Public Key | 存储与 DNS 名称关联的公钥。 |
| CERT | Digital Certificate | 持有数字证书。 |
| HINFO | Host Info | 标识主机的硬件和操作系统。 |
| RP | Responsible Person | 提供域的技术联系人姓名。 |
| SRV | Services | 列出域提供的知名网络服务。 |
| TXT | Text | 用于在 DNS 数据库中包含注释和其他信息。 |

你应该学会阅读资源记录，至少是类型为 SOA、NS、A、PTR 和 MX 的记录，它们是最常用的。接下来，我简要描述这些记录，通过示例说明每种记录类型。

典型的 SOA 记录具有以下格式：

```
@  1D  IN  SOA
@  root (
    42          : serial
    3H          : refresh -- 3 hours
    15M         : retry -- 15 minutes
    1W          : expiry -- 1 week
    1D )        : minimum -- 1 day
```

第一个字段将域指定为 @，表示当前域（默认情况下为区域名称，如 /etc/named.conf 文件所示）。下一个字段为此记录指定一天的 TTL。class 字段设置为 IN，表示该记录用于 Internet。type 字段将记录类型指定为 SOA。其余字段构成 SOA 记录的数据。数据包括主名称服务器的名称（本例中为 @ 或当前域）、技术联系人的电子邮件地址以及用括号括起来的五个不同时间。

NS 记录指定区域的权威名称服务器。典型的 NS 记录如下所示：

```
. 3600000 IN NS A.ROOT-SERVERS.NET.
```

在此情况下，NS 记录列出了根区域的权威名称服务器（请注意第一个字段的名称是一个点）。Time-To-Live 字段指定记录有效期为 1,000 小时（3,600,000 秒）。class 为 IN，表示 Internet；记录类型为 NS。最后一个字段列出名称服务器的名称（A.ROOT-SERVERS.NET.），以点结尾。

A 记录指定与名称对应的地址。例如，以下 A 记录显示 A.ROOT-SERVERS.NET. 的地址为 198.41.0.4：

```
A.ROOT-SERVERS.NET. 3600000 A 198.41.0.4
```

在此情况下，未指定网络类，因为该字段是可选的，默认值为 IN。PTR 记录用于反向映射——将地址转换为名称。考虑以下示例：

```
1 IN PTR localhost.
```

此记录来自名为 0.0.127.in-addr.arpa 的区域的文件。因此，此记录表示与地址 127.0.0.1 关联的名称是 localhost。MX 记录指定代表特定域接收邮件的主机的名称。例如，这里有一个典型的 MX 记录：naba IN MX 10 mailhub.lnbsoft.com。这表示应将发往当前域中名为 naba 的主机的邮件发送到 mailhub.lnbsoft.com（该主机称为邮件交换器）。数字 10 是首选项值。对于具有不同首选项值的多个 MX 记录列表，首选项值较低的记录会先尝试。有了关于资源记录的这些信息，你可以浏览缓存名称服务器的区域文件。



## /var/named/named.ca 文件

关于根域名服务器的信息位于 /var/named/named.ca 文件中，如 /etc/named.conf 文件中根区域的区域语句所指定。以下列表显示了来自 Red Hat Linux 系统的 /var/named/named.ca 文件：

```
: This file holds the information on root name servers needed to
: initialize cache of Internet domain name servers
: (e.g. reference this file in the "cache . <file>*"
: configuration file of BIND domain name servers).
:
: This file is made available by InterNIC
: under anonymous FTP as
: file /domain/named.cache
: on server FTP.INTERNIC.NET
:
: last update: Nov 5, 2002
: related version of root zone: 2002110501
:
:
: formerly NS.INTERNIC.NET
:
A.ROOT-SERVERS.NET. 3600000 IN NS A.ROOT-SERVERS.NET.
3600000 IN A 198.41.0.4
: formerly NS1.ISI.EDU
:
B.ROOT-SERVERS.NET. 3600000 IN NS B.ROOT-SERVERS.NET.
3600000 IN A 128.9.0.107
: formerly C.PSI.NET
:
C.ROOT-SERVERS.NET. 3600000 IN NS C.ROOT-SERVERS.NET.
3600000 IN A 192.33.4.12
: formerly TERP.UMD.EDU
:
D.ROOT-SERVERS.NET. 3600000 IN NS D.ROOT-SERVERS.NET.
3600000 IN A 128.8.10.90
: formerly NS.NASA.GOV
:
E.ROOT-SERVERS.NET. 3600000 IN NS E.ROOT-SERVERS.NET.
3600000 IN A 192.203.230.10
: formerly NS.ISC.ORG
:
F.ROOT-SERVERS.NET. 3600000 IN NS F.ROOT-SERVERS.NET.
3600000 IN A 192.5.5.241
: formerly NS.NIC.DDN.MIL
:
G.ROOT-SERVERS.NET. 3600000 IN NS G.ROOT-SERVERS.NET.
3600000 IN A 192.112.36.4
: formerly AOS.ARL.ARMY.MIL
:
H.ROOT-SERVERS.NET. 3600000 IN NS H.ROOT-SERVERS.NET.
3600000 IN A 128.63.2.53
```
```
: formerly NIC.NOROU.NET
:
I.ROOT-SERVERS.NET. 3600000 IN NS I.ROOT-SERVERS.NET.
3600000 IN A 192.36.148.17
: operated by VeriSign, Inc.
:
J.ROOT-SERVERS.NET. 3600000 IN NS J.ROOT-SERVERS.NET.
3600000 IN A 192.58.128.30
: housed in LINX, operated by RIPE NCC
:
K.ROOT-SERVERS.NET. 3600000 IN NS K.ROOT-SERVERS.NET.
3600000 IN A 193.0.14.129
: operated by IANA
:
L.ROOT-SERVERS.NET. 3600000 IN NS L.ROOT-SERVERS.NET.
3600000 IN A 198.32.64.12
: housed in Japan, operated by WIDE
:
M.ROOT-SERVERS.NET. 3600000 IN NS M.ROOT-SERVERS.NET.
3600000 IN A 202.12.27.33
: End of File
```

此文件包含 NS 和 A 资源记录，指定根区域（由每个 NS 记录第一字段中的“.”表示）的授权名称服务器的名称及其地址。

文件中的注释行以分号开头。这些注释为您提供了有关根名称服务器位置的提示。互联网有 13 个根名称服务器；大多数根服务器位于美国。任何名称服务器都需要此文件，因为名称服务器必须能够访问至少一个根名称服务器。

## /var/named/localhost.zone 文件

/etc/named.conf 文件包含一个用于 localhost 区域的区域语句，该语句指定区域文件为 localhost.zone。该文件位于您的 Red Hat Linux 系统的 /var/named 目录中。以下是 /var/named/localhost.zone 文件包含的内容列表：

```
$TTL 86400
$ORIGIN localhost.
@ 1D IN SOA @ root (
42 ; serial (d. adams)
3H ; refresh
15M ; retry
1W ; expiry
1D ) ; minimum

1D IN NS @
1D IN A 127.0.0.1
```

此区域文件以 $TTL 指令开头，将后续未定义 TTL 的记录的默认 TTL 设置为一天（86,400 秒）。接下来，$ORIGIN 指令将域名设置为 localhost。

在这两个指令之后，/var/named/localhost.zone 文件包含三个资源记录（RR）：一个 SOA 记录、一个 NS 记录和一个 A 记录。SOA 和 NS 记录指定 localhost 为该区域的主要授权名称服务器。A 记录指定 localhost 的地址为 127.0.0.1。

## /var/named/named.local 文件

/etc/named.conf 文件中的第三个区域语句指定了一个名为 0.0.127.in-addr.arpa 的反向映射区域。对于此区域，区域文件为 /var/named/named.local，其中包含以下内容：

```
$TTL      86400
@         IN      SOA     localhost.  root.localhost.  (
                                 1997022700  : Serial
                                 28800      : Refresh
                                 14400      : Retry
                                 3600000    : Expire
                                 86400 )    : Minimum
          IN      NS      localhost.
1         IN      PTR     localhost.
```

SOA 和 NS 记录指定 localhost 为主要名称服务器。

SOA 记录还显示 root.localhost. 作为域的技术联系人的电子邮件地址。请注意，DNS 区域文件使用 user.host.（注意末尾的句点）格式作为电子邮件地址。在向联系人发送任何电子邮件时，您必须将第一个点替换为 @ 并删除最后的点。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_712_0.png)

## 缓存名称服务器：启动和测试

现在您已经研究了缓存名称服务器的配置文件，您可以启动名称服务器并查看其运行情况。要启动名称服务器，请以 root 身份登录并在终端窗口中输入以下命令：

```
service named start
```

此命令启动 named — 名称服务器守护进程。

为确保每次重新启动系统时 named 服务器都会启动，请以 root 身份登录时输入以下命令：

```
chkconfig --level 35 named on
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_712_1.png)

![](img/a7eec43a54473e95dc5ea333fecf1bd7_713_0.png)

named 服务器在 /var/log/messages 文件中写入诊断日志消息。启动 named 后，您可以通过在文本编辑器中打开 /var/log/messages 来检查日志消息。如果 named 没有错误消息，您可以继续测试名称服务器。

在尝试缓存名称服务器之前，您必须将其指定为您的主要名称服务器。为此，请确保 /etc/resolv.conf 文件中的第一行如下：

```
nameserver 127.0.0.1
```

现在您可以使用 host 来测试名称服务器。例如，要使用 localhost 上的缓存名称服务器查找 www.gao.gov 的 IP 地址，请输入以下命令：

```
host www.gao.gov localhost
```

以下是 host 命令的输出结果：

```
Using domain server:
Name: localhost
Address: 127.0.0.1#53
Aliases:
www.gao.gov. has address 161.203.16.2
```

如输出所示，host 命令使用 localhost 作为 DNS 服务器并返回 www.gao.gov 的 IP 地址。如果您得到类似的输出，则缓存名称服务器已启动并运行。

## 配置主名称服务器

配置主名称服务器的最佳方法是先配置缓存名称服务器（如前几节所述）。然后，为您希望其成为主名称服务器的域添加主区域。例如，假设我想为 naba.net 域定义一个主名称服务器。以下是我在以 root 身份登录后配置该主名称服务器的步骤：

- 1. 向 /etc/named.conf 文件添加以下区域语句：
```
zone "naba.net" IN {
    type master;
    file "naba.zone";
};
zone "0.168.192.in-addr.arpa" IN {
    type master;
    file "0.168.192.zone";
};
```
- 2. 创建区域文件 /var/named/naba.zone，其中包含以下行：
```
$TTL 86400
$ORIGIN naba.net.
@		IN SOA	@ root.naba.net (
		100		; serial
		3H		; refresh
		15M		; retry
		1W		; expiry
		1D )		; minimum

		IN NS	@
		IN A	192.168.0.7

wxp	IN	A	192.168.0.2
```
- 3. 创建区域文件 /var/named/0.168.192.zone，其中包含以下行：
```
$TTL 86400
; Remember zone name is: 0.168.192.in-addr.arpa
@		IN	SOA	naba.net. root.naba.net (
		1		; Serial
		28800	; Refresh
		14400	; Retry
		3600000	; Expire
		86400 ); Minimum

		IN	NS	naba.net.

7		IN	PTR	naba.net.
2		IN	PTR	wxp.naba.net.
```
- 4. 要测试新配置，请使用以下命令重新启动 named 服务器：
```
service named restart
```
- 5. 使用 dig 或 host 查询 DNS 服务器。

例如，以下是我如何使用 host 检查在 localhost 上运行的 DNS 服务器上主机 wxp.naba.net 的地址：

```
host wxp.naba.net localhost
```

此命令产生以下输出：

```
Using domain server:
Name: localhost
Address: 127.0.0.1#53
Aliases:

wxp.naba.net has address 192.168.0.2
```

如果您想使用 dig 检查 DNS 服务器，请输入以下命令：

```
dig @localhost wxp.naba.net
```

该 @localhost 部分指定 dig 应联系的 DNS 服务器。



当你成功使用 dig 联系到 DNS 服务器后，你可以让向该服务器提出的问题变得更复杂一些。下面例如是我输入的命令，用于尝试使用 IP 地址 192.168.0.2 进行反向查找：

```
host 192.168.0.2 localhost
```

此命令显示以下输出：

```
Using domain server:
Name: localhost
Address: 127.0.0.1#53
Aliases:

2.0.168.192.in-addr.arpa domain name pointer wxp.naba.net
```

## 理解网络信息服务（NIS）

网络信息服务（NIS）由 Sun Microsystems 开发，用作在局域网中的所有计算机之间共享信息的方式。NIS 最常用的信息类型包括以下内容：

- 来自诸如 `/etc/passwd` 和 `/etc/shadow` 等文件中的用户名和密码
- 来自 `/etc/group` 文件的组信息

通常，每个系统都有各自文件中的信息副本，任何更改都需要单独在每个系统上更新文件。使用 NIS，你可以为一组计算机在 NIS 服务器中维护一套配置文件。然后所有运行 NIS 客户端的计算机都可以访问这些文件。例如，如果你的用户名和密码在 NIS 密码数据库中，你将能够登录到网络上运行 NIS 客户端程序的所有计算机。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_715_0.png)

NIS 最初被称为 Sun Yellow Pages（YP），但 Yellow Pages 是英国 British Telecom 在英国注册的商标，因此 Sun Microsystems 必须更改名称。然而时至今日，许多 NIS 命令——以及 NIS 软件包名称——仍然以字母 yp 开头。

### NIS 如何工作

如果要在网络中使用 NIS，必须至少设置一台计算机作为 NIS 服务器。网络中可以有多个 NIS 服务器，每个服务器为不同的计算机集合提供服务。你也可以有一个主 NIS 服务器和一个或多个从 NIS 服务器，从服务器接收主服务器数据库的副本。主 NIS 服务器支持的计算机组称为 NIS 域或 YP 域。

主 NIS 服务器运行 ypserv 守护进程（这是 NIS 服务器守护进程），它在 DBM 数据库中维护共享信息。（DBM 指 Data Base Management，是维护数据库中键值对的函数库。）NIS 数据库称为映射。你可以使用随 NIS 服务器软件提供的 /usr/lib/yp/makedbm 程序，直接从文本配置文件——例如 /etc/passwd 和 /etc/group——创建这些 NIS 映射。更准确地说，ypserv 守护进程使用 /var/yp 目录中的 Makefile 为所有共享配置文件创建映射。

主 NIS 服务器向所有 NIS 客户端计算机提供映射。客户端运行 ypbind 守护进程，通过它各种客户端程序访问主 NIS 服务器。除了主服务器之外，还可以设置一个或多个 NIS 从服务器，以防主服务器不可用或宕机时提供 NIS 映射。NIS 从服务器会定期从主服务器复制 NIS 映射（使用 /usr/lib/yp/ypxfr 命令），并在主服务器宕机时向客户端提供这些映射。

你可以将 NIS 视为在 NIS 域中的所有计算机之间分发同一套配置文件的手段。你可以获得共享相同文件的优势（例如所有机器使用相同的用户名和密码），同时仍然只需编辑和维护一套文件——主 NIS 服务器上的文件。

在接下来的几节中，我将解释如何将你的 Red Hat Linux 系统设置为 NIS 客户端和 NIS 服务器。

### 设置 NIS 客户端

如果你的网络使用 NIS 集中管理用户和密码，你可以将 Red Hat Linux PC 设置为 NIS 客户端。事实上，当你从本书附带的 CD-ROM 安装 Red Hat Linux 时，可以在 GUI 安装程序的身份验证配置屏幕中启用 NIS。

在 Red Hat Linux 安装期间，身份验证配置屏幕会显示多种用于验证用户的选项——默认是 shadow 密码和 MD5 密码。其中一个选项是标记为 Enable NIS 的按钮。你可以点击此按钮将 Red Hat Linux PC 设置为 NIS 客户端。当然，只有在你的网络已设置 NIS 服务器时才应这样做。

如果你选择 Enable NIS 选项，你必须提供以下信息：

- 指定 NIS 域名。域名指的是 NIS 服务器服务的计算机组。
- 指定 NIS 服务器的名称。
- 指示你的 PC 是否要在本地网络中使用 IP 广播来查找 NIS 服务器。

如果你在 Red Hat Linux 安装期间未将系统配置为 NIS 客户端，可以通过执行以下通用步骤来完成：

- 1. 定义你的 NIS 域名。
- 2. 设置 NIS 配置文件（`/etc/yp.conf`）。
  在此文件中，你指定为 Red Hat Linux PC 提供 NIS 映射的主 NIS 和从服务器。
- 3. 配置 NIS 客户端守护进程——`ypbind`——使其在系统启动时启动。

我将在接下来的三个部分中向你展示如何执行这些任务的具体步骤。

### NIS 域名设置

NIS 域名标识特定 NIS 服务器支持的计算机组。你可以使用 `domainname` 命令设置系统的 NIS 域名。例如，要将 NIS 域名设置为 admin，以 `root` 登录并在终端窗口中输入以下命令：

```
domainname admin
```

如果你不带任何参数输入 `domainname`，命令会打印当前的 NIS 域名。

为确保系统启动时立即设置 NIS 域名，应从启动脚本之一运行该命令。你可以通过在 Red Hat Linux 系统的 `/etc/sysconfig/network` 文件中添加以下行来实现：

```
NISDOMAIN="admin"
```

当然，你应使用适合你网络的 NIS 域名。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_718_0.png)

NIS 域与本章前面讨论的 DNS 域名不同。选择一个与 DNS 域名无关的 NIS 域名。这样可以使黑客更难猜出你的 NIS 域名（如果他们知道 NIS 域名，就有风险获取 NIS 密码数据库）。

### NIS 配置文件设置

下一节所述的 ypbind 守护进程需要有关 NIS 域和 NIS 服务器的信息来完成其工作。它在 /etc/yp.conf 配置文件中查找这些信息。ypbind 守护进程在启动时或接收到 SIGHUP 信号时读取 /etc/yp.conf 文件（例如，当你使用 kill -HUP 命令重启 ypbind 时）。

要为本地域（你已使用 domainname 命令设置）指定一个或多个 NIS 服务器，/etc/yp.conf 中只需要如下行：

```
ypserver nisadmin
ypserver 192.168.0.4
```

如果该名称列在 /etc/hosts 文件中，你可以使用诸如 nisadmin 这样的名称（这样 ypbind 可以在不使用 NIS 的情况下将名称解析为 IP 地址）。否则，你应指定 NIS 服务器的 IP 地址。

在 /etc/yp.conf 中，你还可以为特定 NIS 域指定特定的 NIS 服务器，如下所示：

```
domain sales server nissales
domain admin server nisadmin
```

/etc/yp.conf 文件中的第三种条目指定 ypbind 应在本地网络中使用 IP 广播为指定域查找 NIS 服务器。为此，将如下行添加到 /etc/yp.conf：

```
domain admin broadcast
```

### NIS 客户端守护进程设置

NIS 域中的每台计算机，包括服务器，都运行 ypbind 守护进程。各种 NIS 客户端应用程序，例如 ypwhich、ypcat 和 yppoll，需要 ypbind 守护进程从主 NIS 服务器获取信息。更准确地说，C 库联系 ypbind 守护进程以定位域的 NIS 服务器。然后 C 库直接联系服务器以获取管理信息。客户端应用程序通过 C 库中的函数获取信息。




![](img/a7eec43a54473e95dc5ea333fecf1bd7_719_0.png)

要交互式启动 ypbind，请以 root 身份登录并输入以下命令：

```
service ypbind start
```

如果希望 ypbind 在系统启动时启动，请输入以下命令：

```
chkconfig --add ypbind
chkconfig --level 35 ypbind on
```

## 设置 NIS 服务器

将你的 Red Hat Linux 系统设置为 NIS 服务器，首先将其设置为 NIS 客户端——设置 NIS 域名，配置 /etc/yp.conf 文件，并配置 ypbind 守护进程。 （请注意，在你拥有正在运行的 NIS 服务器之前，ypbind 守护进程将无法工作。）客户端配置完成后，你可以配置 NIS 服务器。这需要你执行以下任务：

- 使用 ypinit 创建 NIS 映射。
- 配置主 NIS 服务器 — ypserv。
- 可选地，配置一个或多个从 NIS 服务器。

我将在接下来的两个部分中解释这些步骤。

### NIS 映射创建

创建 NIS 映射涉及使用 makedbm 将文本文件（如 /etc/passwd 和 /etc/group）转换为 DBM 文件。映射的创建由 /var/yp/Makefile 控制，该文件可由 make 命令使用以执行特定任务。

你可以配置 NIS 服务器希望与 NIS 域中的客户端共享的内容。你可以通过编辑 /var/yp 目录中的 Makefile 来实现。 在文本编辑器中打开 /var/yp/Makefile 并找到以 all: 开头的行。以下是 Makefile 的典型摘录，显示了 all: 行之前的注释：

```
# If you don't want some of these maps built, feel free to comment
# them out from this list.
all: passwd group hosts rpc services netid protocols mail \
# netgrp shadow publickey networks ethers bootparams printcap \
# amd_home auto_master auto_home auto_local passwd.adjunct \
# timezone locale netmasks
```

正如注释行（以 # 开头的行）所示，你可以注释掉任何不想构建的映射。在前面的示例中，最后三行中列出的映射将不会被构建。

接下来，编辑 /var/yp/secure nets 文件（如果不存在则创建新文件），以指定可以访问 NIS 映射的客户端计算机的 IP 地址。例如，要允许来自 localhost 和 192.168.0.0 网络中的主机的连接，请使用以下内容作为 /var/yp/secure nets 文件的内容：

```
# Always allow access for localhost
host 127.0.0.1
# allow connections from any host
# on the 192.168.0.0 network
255.255.255.0 192.168.0.0
```

最后一行仅允许 192.168.0.1 到 192.168.0.254 范围内的计算机访问 NIS 映射。

接下来，你应该通过使用 -m 选项运行 /usr/lib/yp/ypinit 程序来生成 NIS 映射数据库。以下是使用该程序的示例会话：

```
/usr/lib/yp/ypinit -m
```

该程序会询问你将运行 NIS 服务器的主机名称。它会自动选择你的主机作为 NIS 服务器，并提示输入任何其他 NIS 服务器的名称。你可以一次添加一个服务器名称，并在完成后按 Ctrl-D。然后你必须验证 NIS 服务器列表是否正确（输入 y）。之后，程序会根据 Makefile 中的 all: 行指定的内容生成 NIS 映射。映射文件存储在 /var/yp 的子目录中，该子目录的名称与你之前为系统设置的 NIS 域名相同。例如，对于 NIS 域 admin，映射文件位于 /var/yp/admin 目录中。

### 主 NIS 服务器配置

要配置 NIS 服务器守护进程 ypserv，你必须准备配置文件 /etc/ypserv.conf。你可以通过输入命令 man ypserv.conf 来了解此文件的语法。

你可以在 /etc/ypserv.conf 中添加指定访问规则的行——哪些主机可以访问哪些映射。访问规则的格式如下：

```
Host : Map : Security : mangle [: field_to_mangle]
```

field_to_mangle 是可选的；它指示映射文件中应被篡改的字段（默认为第二个字段，因为密码在大多数文件（如 /etc/passwd）的第二个字段中）。篡改一个字段是指如果请求来自非特权主机，则将其替换为 x。其余字段的含义如下：

- Host — IP 地址或通配符 (*)，表示规则适用于谁。
- Map — 规则适用的映射名称。（映射的名称与 /var/yp/domainname 目录中的映射文件相同，其中 domainname 是你的 NIS 域名。）
- Security — 以下之一：none（始终允许访问）；port（从小于 1024 的端口访问）；deny（拒绝访问映射）；或 des（需要 DES 身份验证）。
- mangle — 以下之一：yes（如果请求来自未经授权的主机，则应将 field_to_mangle 指定的字段替换为 x）或 no（不篡改）。

例如，/etc/ypserv.conf 文件中的以下行将对密码映射的访问限制为 192.168.0 网络中的系统：

```
192.168.0 : passwd.byname : port : yes
192.168.0 : passwd.byuid : port : yes
```

如果你未指定任何访问规则，ypserv 将允许所有计算机访问所有映射。

在设置好 /etc/ypserv.conf 文件后，你可以使用以下命令启动 NIS 服务器：

```
service ypserv start
```

为确保每次重新启动系统时 ypserv 都会启动，请输入以下命令启用它：

```
chkconfig --level 35 ypserv on
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_721_0.png)

为处理来自客户端的密码更改，你还必须在域的主 NIS 服务器上运行 rpc.yppasswd 服务器。rpc.yppasswd 服务器使客户端系统上的用户能够输入 yppasswd 命令并在 NIS 数据库中更改其密码。如果主 NIS 服务器上未运行 rpc.yppasswd 服务器，用户在输入 yppasswd 命令时将收到以下错误消息：

```
yppasswd: yppasswdd not running on NIS master host
```

为纠正此问题，以 root 身份登录并输入

```
service yppasswdd start
```

要在系统启动时自动启动 rpc.yppasswd，请输入

```
chkconfig --level 35 yppasswdd on
```

在主 NIS 服务器运行后，你可以使用各种 NIS 客户端程序（如 ypwhich、yppoll、ypcat 和 ypmatch）对其进行测试。

## 配置从 NIS 服务器

要将系统设置为从 NIS 服务器，首先将其设置为 NIS 客户端并验证客户端是否正常工作。特别是，输入 ypwhich -m 并查找 NIS 映射列表以及每个映射的主 NIS 服务器名称。（在下一节中，我将向你展示 ypwhich -m 命令的工作原理。）

在确认系统已配置为 NIS 客户端后，输入以下命令将系统设置为从 NIS 服务器：

/usr/lib/yp/ypinit -s nismaster

其中 nismaster 是该域的主 NIS 服务器的名称。

## 尝试使用 NIS

在网络中拥有主 NIS 服务器并且 ypbind 客户端正在运行后，你可以尝试各种 NIS 客户端程序和其他实用程序，以查看一切是否正常工作。

NIS 服务器和客户端使用远程过程调用（RPC）交换信息。RPC 需要 portmap 服务，该服务将 RPC 服务映射到 TCP 和 UDP 端口。当支持 RPC 的服务器启动时，它会向 portmap 注册并列出其支持的服务和使用的端口。你的 Red Hat Linux 系统应该已经运行了 portmap。你可以使用以下命令检查它：

```
ps ax | grep portmap
```

在输出中你应该看到显示 portmap 进程的行。例如，以下是该命令在 Red Hat Linux 系统上的输出：

```
525  ?  S  0:00 portmap
26222 pts/2  S  0:00 grep portmap
```

要查看 ypserv 和 ypbind 进程是否在主 NIS 服务器上运行，请输入以下命令：

```
rpcinfo -p
```

输出应显示 ypserv 和 ypbind 在最后一列中。

要确定系统正在使用哪个 NIS 服务器，请尝试 ypwhich 命令。以下是一个典型示例：

```
ypwhich
```

The output should be the name of the host that runs the NIS master server.

You can also use the ypwhich command to view the master NIS server for all available maps, by typing this command:

```
ypwhich -m
```

The output shows a list of the available NIS maps — and, for each map, the name of its master NIS server.

To view the name of the master NIS server and information about a specific NIS map, use the yppoll command. For example, here is a yppoll query for the passwd.byname map:

```
yppoll passwd.byname
```

The output shows the NIS domain name and the name of the master server.

Use the ypcat command to print the values of the keys in an NIS map. For example, here is a ypcat query for the NIS map group.byname:

```
ypcat group.byname
```

The output is a list of group names and group IDs. Here's a typical output:

```
ivy::1:503:
ashley::1:502:
emily::1:501:
naba::1:500:
```

You can use ypmatch to look at the entries in an NIS map that match a specific key. For example, here is a ypmatch command line that looks for entries that match the key naba in the group.byname map:

```
ypmatch naba group.byname
```

Here's the output that matches the key naba:

```
naba::1:500:
```

If you compare this with the output from ypcat that shows all the group names, you can see that ypmatch shows the line corresponding to the group name naba.

### 第 6 章：运行 Samba 和 NFS

### 本章内容

- ✓ Sharing files with NFS
- ✓ Using the Red Hat NFS Server Configuration tool
- ✓ Installing and configuring Samba
- ✓ Setting up a Windows server using Samba

If your local area network is like many others, it needs the capability to share files between systems that run Linux and other systems that don't. Thus, Red Hat Linux includes two prominent file-sharing services:

- ♦ **Network File System (NFS)** is for sharing files with other UNIX systems (or PCs with NFS client software)
- ♦ **Samba** is for file sharing and print sharing with Windows systems.

In this chapter, I describe how to share files using both NFS and Samba.

### 通过 NFS 共享文件

Sharing files through NFS is simple and involves two basic steps:

- ♦ On the Red Hat Linux system that runs the NFS server, you export (share) one or more directories by listing them in the `/etc/exports` file and by running the `exportfs` command. In addition, you must run the NFS server by logging in as `root` and typing the command `service nfs start`.
- ♦ On each client system, you use the `mount` command to mount the directories that your server has exported.

The only problem in using NFS is that each client system must support it. Microsoft Windows doesn't come with NFS. That means you have to buy NFS software separately if you want to share files by using NFS. However, it makes sense to use NFS if all systems on your LAN run Linux (or other variants of UNIX with built-in NFS support).

![](img/a7eec43a54473e95dc5ea333fecf1bd7_725_0.png)

Note that NFS has security vulnerabilities. You should not set up NFS on systems directly connected to the Internet.

In the next few sections, I walk you through NFS setup, using an example of two Red Hat Linux PCs on a LAN.

### 使用 NFS 导出文件系统

Start with the server system that exports — makes available to the client systems — the contents of a directory. On the server, you must run the NFS service and also designate one or more file systems that are to be exported — made available to the client systems.

To export a file system, you have to add an appropriate entry to the /etc/exports file. For example, suppose you want to export the /home directory and you want to enable the host named LNB P75 to mount this file system for read and write operations. You can do so by adding the following entry to the /etc/exports file:

```
/home LNB P75 (rw,sync)
```

If you want to give access to all hosts on a LAN such as 192.168.0.0, you could change this line to:

```
/home 192.168.0.0/24 (rw,sync)
```

Every line in the /etc/exports file has this general format:

```
directory host1(options) host2(options) ...
```

The first field is the directory being shared via NFS, followed by one or more fields that specify which hosts can mount that directory remotely and a number of options within parentheses. You can specify the hosts with names or IP addresses, including ranges of addresses.

The options within parentheses denote the kind of access each host is granted and how user and group IDs from the server are mapped to IDs on the client. (For example, if a file is owned by root on the server, what should that be on the client?) Within the parentheses, commas separate the options. For example, if a host is allowed both read and write access — and all IDs are to be mapped to the anonymous user (by default this is the user named nobody) — then the options would look like this:

```
(rw,all_squash)
```

Table 6-1 shows the options you can use in the /etc/exports file. There are two types of options — general options and user ID mapping options.

表 6-1 /etc/exports 中的选项

| 此选项 | 执行以下操作 |
|---|---|
| **常规选项** | |
| secure | 仅允许从 1024 或更低端口连接（默认）。 |
| insecure | 允许从 1024 或更高端口连接。 |
| ro | 允许只读访问（默认）。 |
| rw | 允许读写访问。 |
| sync | 在请求时执行写操作（这意味着将信息写入磁盘）（默认）。 |
| async | 在服务器准备好时执行写操作。 |
| no_wdelay | 立即执行写操作。 |
| wdelay | 稍作等待以查看是否到达相关的写请求，然后一起执行它们（默认）。 |
| hide | 隐藏已导出的目录，该目录是另一个已导出目录的子目录（默认）。 |
| no_hide | 行为与 hide 完全相反。 |
| subtree_check | 执行子树检查，即在访问文件时检查已导出子目录的父目录（默认）。 |
| no_subtree_check | 关闭子树检查（与 subtree_check 相反）。 |
| insecure_locks | 允许不安全的文件锁定。 |
| **用户 ID 映射选项** | |
| all_squash | 将所有用户 ID 和组 ID 映射到客户端上的匿名用户。 |
| no_all_squash | 将远程用户和组 ID 映射到客户端上的相似 ID（默认）。 |
| root_squash | 将远程 root 用户映射到客户端上的匿名用户（默认）。 |
| no_root_squash | 将远程 root 用户映射到本地 root 用户。 |
| anonuid=UID | 设置用于 all_squash 和 root_squash 选项的匿名用户的用户 ID。 |
| anongid=GID | 设置用于 all_squash 和 root_squash 选项的匿名用户的组 ID。 |

After adding the entry in the /etc/exports file, manually export the file system by typing the following command in a terminal window:

```
exportfs -a
```

This command exports all file systems defined in the /etc/exports file.

Now you can start the NFS server processes. To do so, log in as root and type the following command in a terminal window:

```
service nfs start
```

If you want the NFS server to start when the system boots, type the following command to turn it on:

```
chkconfig --level 35 nfs on
```

When the NFS service is up, the server side of NFS is ready. Now you can try to mount the exported file system from a client system, and access the exported file system as needed.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_727_0.png)

If you ever make any changes to the exported file systems listed in the /etc/exports file, remember to restart the NFS service. To do so, log in as root and type the following command in a terminal window:

```
service nfs restart
```

### 挂载 NFS 文件系统

To access an exported NFS file system on a client system, you have to mount that file system on a mount point. The mount point is nothing more than a local directory. For example, suppose you want to access the /home directory exported from the server named LNBP200 at the local directory /mnt/lnbp200 on the client system. To do so, follow these steps:

- 1. Log in as root and create the directory with the command

```
mkdir /mnt/lnbp200
```

- 2. Type the following command to mount the directory from the remote system (LNBP200) on the local directory /mnt/lnbp200:

```
mount lnbp200:/home /mnt/lnbp200
```

After these steps, you can view and access exported files from the local directory /mnt/lnbp200.

To confirm that the NFS file system is indeed mounted, log in as root on the client system and type mount in a terminal window. You should see a line similar to the following about the NFS file system:

```
lnbp200:/home/public on /mnt/lnbp200 type nfs (rw,addr=192.168.0.4)
```



## 使用 Red Hat NFS 服务器配置工具

Red Hat Linux 附带了一个图形化的 NFS 服务器配置工具，可轻松配置和启动 NFS 服务器。要使用此工具配置 NFS 服务器，请按照以下步骤操作：

1. **以 root 身份登录并从 GNOME 或 KDE 桌面选择 主菜单：系统设置：服务器设置：NFS 服务器。**
   NFS 服务器配置窗口出现。
2. **在工具栏上单击 添加。**
   添加 NFS 共享 对话框出现。
3. **使用对话框添加您希望通过 NFS 共享的目录。**
   首先指定目录、谁有权访问它（主机或 IP 地址）以及访问类型（只读或读写）。图 6-1 显示了将 /home 目录以读写方式与 192.168.0.0 网络中的所有主机共享的设置。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_728_0.png)

图 6-1：
从此对话框指定共享目录和基本权限。

4. **在 添加 NFS 共享 对话框中单击 常规选项 选项卡并设置您想要的选项（如图 6-2 所示）。**
   这些选项对应于表 6-1 的 常规选项 部分中列出的选项。

图 6-2：
从此对话框指定 NFS 共享的常规选项。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_729_0.png)

5. **在 添加 NFS 共享 对话框中单击 用户访问 选项卡并设置您想要的选项（图 6-3）。**
   这些选项对应于表 6-1 的 用户 ID 映射选项 部分中列出的选项。

6. **在 添加 NFS 共享 对话框中单击 确定。**
   NFS 配置工具将设置保存到 `/etc/exports` 文件中并启动 NFS 服务器。

7. **选择 文件→退出 以退出 NFS 配置工具。**
   完成这些步骤后，您可以在网络中的其他主机上挂载 NFS 共享。

图 6-3：
从此对话框指定 NFS 共享的用户访问选项。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_729_1.png)

## 使用 Samba 设置 Windows 服务器

如果您依赖 Windows 进行文件共享和打印共享，那么您可能在服务器和客户端中使用 Windows。如果是这样，您仍然可以在不丢失 Windows 文件和打印共享功能的情况下将 Red Hat Linux PC 作为服务器使用；Red Hat Linux 可以设置为 Windows 服务器。当您从本书的附带 CD-ROM 安装 Red Hat Linux 时，您也有机会安装 Samba 软件包，该软件包执行此设置。您只需在安装期间选择 Windows 文件服务器 软件包组即可。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_730_0.png)

在 Linux PC 上安装并配置 Samba 后，您的客户端 PC — 即使它们运行的是旧的 Windows for Workgroups 操作系统或更新的 Windows 95/98/NT/2000/XP 版本 — 也可以访问 Red Hat Linux PC 上的共享磁盘和打印机。为此，它们使用 Server Message Block（SMB）协议，即 Windows 文件和打印共享中的底层协议。

安装 Samba 软件包后，您可以将 Red Hat Linux PC 设为 Windows 客户端，这意味着 Red Hat Linux PC 可以访问 Windows 服务器管理的磁盘和打印机。

Samba 软件包具有以下主要组件：

- `/etc/samba/smb.conf`：这是 SMB 服务器使用的 Samba 配置文件。
- `/etc/samba/smbusers`：此 Samba 配置文件显示 Samba 用户名与本地 Red Hat Linux PC 上用户名的对应关系。
- `nmbd`：这是 NetBIOS 名称服务器，客户端使用它查找服务器。（NetBIOS 的全称是 Network Basic Input/Output System — 应用程序用于与网络传输（如 TCP/IP）通信的接口）
- `nmblookup`：此命令返回由其 NetBIOS 名称标识的 Windows PC 的 IP 地址。
- `smbadduser`：此程序将用户添加到 SMB 密码文件。
- `smbcacls`：此程序操作共享文件上的 Windows NT 访问控制列表（ACL）。
- `smbclient`：这是 Windows 客户端，在 Linux 上运行，允许 Linux 访问任何 Windows 服务器上的文件和打印机。
- `smbcontrol`：此程序向 `smbd`、`nmbd` 或 `winbindd` 进程发送消息。
- `smbd`：SMB 服务器，接受 Windows 客户端的连接并提供文件和打印共享服务。
- `smbmount`：此程序在 Red Hat Linux PC 上挂载 Samba 共享目录。
- `smbpasswd`：此程序更改 SMB 用户的密码。
- `smbprint`：此脚本启用在 SMB 服务器上的打印机上打印。
- `smbstatus`：此命令列出本地主机的当前 SMB 连接。
- `smbtar`：此程序直接将 SMB 共享备份到 Red Hat Linux 系统上的磁带驱动器。
- `smbumount`：此程序卸载当前已挂载的 Samba 共享目录。
- `testparm`：此程序确保 Samba 配置文件正确。
- `winbindd`：此服务器解析来自 Windows NT 服务器的名称。

在以下各节中，我将描述如何从附带 CD-ROM 安装 Samba 以及如何从 Red Hat Linux PC 打印到 Windows PC 上的共享打印机。

### 检查 Samba 是否已安装

通过在终端窗口中键入以下命令检查 Samba 是否已安装：

```
rpm -q samba
```

如果您看到类似以下输出，则表示 Samba 已安装在您的系统上：

```
samba-3.0.0-5rc1
```

如果收到软件包未安装的消息，请按照以下步骤从本书的附带 CD-ROM 安装 Samba：

1. **以 root 身份登录并将第一张 DVD 插入驱动器。如果您使用 GNOME 或 KDE，DVD 应该会自动挂载。如果没有，请键入以下命令挂载 DVD：**
   `mount /mnt/cdrom`
2. **使用以下命令更改到 DVD — 具体来说是 Red Hat Package Manager（RPM）软件包所在的目录：**
   `cd /mnt/cdrom/RedHat/RPMS`
3. **使用以下 rpm 命令安装 Samba：**
   `rpm -ivh samba*`
   如果 Samba 已安装，此命令会返回错误消息。否则，rpm 命令通过将各种文件复制到适当位置在您的系统上安装 Samba。

安装 Samba 软件后，您必须在可以使用它之前配置 Samba。

### 配置 Samba

要设置 Windows 文件共享和打印共享服务，请使用图形化 Samba 服务器配置工具按照以下步骤操作：

1. **选择 主菜单→系统设置→服务器设置→Samba。**
   如果您未以 root 身份登录，系统会提示您输入 root 密码。然后 Samba 服务器配置窗口出现。

2. **单击 添加 按钮。**
   创建 Samba 共享 对话框出现。

3. **输入要共享的目录名称或单击 浏览 并选择一个目录（目录必须已存在）。还选择权限 — 只读或读写（见图 6-4）。**
   图 6-4 显示了一个典型的示例，共享 `/home/public` 目录。如果目录不存在，您可以以 root 身份登录并在终端窗口中键入 `mkdir /home/public` 来创建目录。

4. **在 创建 Samba 共享 对话框的 访问 选项卡上，输入应有权访问共享目录的用户或选择 允许所有人访问 单选按钮，然后单击 确定。**

![](img/a7eec43a54473e95dc5ea333fecf1bd7_732_0.png)

图 6-4：输入要共享的目录信息。

Samba 服务器配置工具通过在配置文件 `/etc/samba/smb.conf` 中添加条目来创建 Samba 共享。

5. 要设置 Samba 服务器的工作组名称，请在 Samba 服务器配置工具中选择 首选项→服务器设置。然后在 服务器设置 对话框的 基础 选项卡中输入与您的 Windows 网络相同的 workgroup 名称（见图 6-5）。

图 6-5：
输入工作组名称和描述。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_733_0.png)

6. 在 服务器设置 对话框的 安全 选项卡上，选择来宾用户名称（如果需要）并选择身份验证模式。
   如果您将身份验证模式设置为 用户，用户可以使用用户名和密码登录以访问 Samba 共享。

7. 要添加可以访问 Samba 共享的用户，请在 Samba 服务器配置工具中选择 首选项→Samba 用户；在 Samba 用户 对话框中，单击 添加用户 并在 创建新的 Samba 用户 对话框中填写所需信息 — 用户名和密码。
   首先识别 Unix 用户名，然后为该用户设置 Samba 用户名和 Samba 密码（见图 6-6）。

图 6-6：
添加可以访问 Samba 共享的用户信息。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_733_1.png)

8. 添加完用户后，单击 确定 关闭 Samba 用户 对话框。



这会在 /etc/samba 目录中创建适当的 Samba 配置文件并启动 Samba 服务。特别是，文件 /etc/samba/smb.conf 包含你刚刚创建的 Samba 共享的配置详情。

添加 Samba 共享后，输入以下命令以验证 Samba 配置文件是否正确：

```
testparm
```

如果命令显示文件加载正常，那么一切就绪。testparm 命令还会显示 Samba 配置文件的内容。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_734_0.png)

要在系统重启时自动启动 SMB 服务，输入以下命令：

```
chkconfig --level 35 smb on
```

## 试用 Samba

现在你可以从局域网上的 Windows 系统之一访问 Red Hat Linux 系统上的 Samba 服务器。在 Windows 95/98/Me 桌面上双击“网络邻居”图标。在 Windows XP 上，选择“开始→我的网络位置”，然后单击“查看工作组计算机”。这应该会显示同一工作组中的所有计算机。

如标签（图 6-6）所示，Lnblp1 实际上是运行 Samba 的 Red Hat Linux 系统。

Figure 6-7:
可以从 Windows XP 查看 Fedora Samba 服务器。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_734_1.png)

当你看到 Samba 服务器时，可以通过双击图标打开它。系统会提示你输入 Samba 用户名和 Samba 密码，在正确输入这些信息后，你可以访问 Samba 共享上的文件夹和打印机（如有）。例如，图 6-8 显示了我运行在 Fedora 上的 Samba 服务器上的共享资源。如你所见，有两个共享文件夹——一个是我的主目录，另一个是我使用 Samba 服务器配置工具创建的公共共享。然后你可以打开这些文件夹以进一步探索目录内容。

Figure 6-8:
从 Windows XP 查看时，Fedora Samba 服务器上的共享资源。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_735_0.png)

## 第九册

## 编程

## 第五波

作者 Rich Tennant

![](img/a7eec43a54473e95dc5ea333fecf1bd7_736_0.png)

## 目录概览

- 第1章：Red Hat Linux 编程精要 ...........................................711
- 第2章：在 C 中编程 ...........................................737
- 第3章：编写 Shell 脚本 ...........................................769
- 第4章：在 Perl 中编程 ...........................................781

### 第1章：Red Hat Linux 编程精要

## 本章内容

- ✓ 学习编程
- ✓ 探索 Red Hat Linux 中的软件开发工具
- ✓ 使用 GCC 编译和链接程序
- ✓ 学习使用 `make`
- ✓ 使用 `gdb` 调试程序
- ✓ 理解 GNU GPL 和 LGPL 的含义

你的 Red Hat Linux 系统已预装了开发软件所需的所有工具。特别是，它拥有所有 GNU 软件开发工具，例如 GCC（C 和 C++ 编译器）、GNU make 和 GNU 调试器。在本章中，我将向你介绍编程，描述这些软件开发工具，并展示如何使用它们。尽管我使用 C 和 C++ 编程语言中的示例，但重点不是展示如何在这些语言中编程，而是展示如何使用各种软件开发工具（如编译器、make 和调试器）。

我还简要解释了自由软件基金会的 GNU 公共许可证（GPL）可能会如何影响你开发 Linux 软件的计划。你需要了解这一点，因为你在 Linux 中开发软件时会使用 GNU 工具和 GNU 库。

## 学习编程

如果你曾用任何编程语言编写过计算机程序，你可以很快开始在 Red Hat Linux 系统上编写程序。然而，如果你从未编写过计算机程序，在开始之前你需要两个基本资源：对编程基础的了解，以及对计算机及其主要组成部分的快速回顾。在本节中，我为你概述计算机编程——刚好足够让你入门。

## 计算机的简化视图

在你对计算机编程有所体会之前，你需要了解计算机程序在整台计算机中的位置。图 1-1 显示了计算机的简化视图，突出了对程序员重要的主要部件。

Figure 1-1:
计算机的简化视图及其运行程序的方式。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_739_0.png)

计算机的核心是中央处理器（CPU），它执行计算机程序中包含的指令。执行此任务的具体硬件（制造商称之为微处理器，我们称之为芯片）因系统而异：在 Pentium PC 中，它是 Pentium；在 Sun SPARC 工作站中，它是 SPARC 芯片；在 HP UNIX 工作站中，它是 PA-RISC 芯片。这些微处理器功能各不相同，但使命相同：告诉计算机做什么。

随机存取存储器（RAM），或简称内存，在 CPU 执行时作为计算机程序的存储空间。如果程序处理某些数据，该数据也存储在内存中。内存的内容不是永久的；当计算机关闭或程序不再运行时，它们就会消失（永不返回）。

硬盘，或磁盘，作为计算机程序和数据的永久存储空间。磁盘按文件组织，而文件又按层级目录和子目录组织（有点像把纸质文件夹整理到文件柜的抽屉里）。每个文件本质上是一个存储块，能够容纳各种信息。例如，一个文件可能是人类可读的文本文件——也可能是只有 CPU 才能理解的计算机指令集合。当你创建计算机程序时，你会大量使用文件。

对于程序员来说，另外两个重要项目是输入和输出——程序从用户获取输入并向用户显示输出的方式。用户通过键盘提供输入，输出显示在监视器上。然而，程序也可以从文件接受输入并向文件发送输出。

## 操作系统的角色

操作系统是一组特殊的计算机程序，其主要目的是加载和运行其他程序。所有操作系统都包含一个或多个命令处理器（在 Red Hat Linux 中称为 shell），允许用户键入命令并执行诸如运行程序或打印文件等任务。大多数操作系统还包括图形用户界面（如 Red Hat Linux 中的 GNOME 和 KDE），允许用户通过单击屏幕图标来执行大多数任务。Red Hat Linux、Windows（无论是 NT、2000 还是 XP 版本）以及各种版本的 UNIX 都是操作系统的例子。

正是操作系统赋予了计算机个性。例如，你可以在 PC 上运行 Windows 2000 或 Windows XP。在同一台 PC 上，你也可以安装并运行 Red Hat Linux。这意味着，根据安装在其上的操作系统，同一台 PC 可能是 Windows 2000、Windows XP 或 Red Hat Linux 系统。

计算机程序是“建立在”操作系统之上的。这意味着计算机程序必须利用操作系统包含的功能。例如，计算机程序通过使用操作系统的内置功能来读写文件。（而且如果操作系统不能做咖啡，那么没有任何程序可以命令它去做并期望得到积极的结果。）

尽管细节各不相同，但大多数操作系统都支持一些相似的概念。作为程序员，你需要熟悉以下几个概念：

- 进程是当前在计算机中运行的计算机程序。大多数操作系统允许多个进程同时运行。
- 命令处理器，或 shell，是一个特殊程序，允许用户键入命令并执行各种任务，例如运行任何程序、查看大量文件或打印文件。在 Windows 2000 或 Windows XP 中，你可以在命令提示符窗口中键入命令。
- 术语命令行指的是用户输入给命令处理器的命令。通常命令行包含一个命令和一个或多个选项——命令是该行中的第一个词，其余的是选项（计算机被要求的具体行为）。



环境变量本质上是带有名称的文本字符串。例如，PATH 环境变量指的是包含目录名称的字符串。操作系统使用环境变量为进程提供有用的信息。要查看 Windows 2000 或 Windows XP 系统中的环境变量列表，请在命令提示符窗口中输入 SET。在 Red Hat Linux 中，你可以使用 printenv 命令查看环境变量。

## 计算机编程基础

计算机程序是一系列用于执行特定任务的指令，例如加两个数字或在文件中搜索某些文本。因此，计算机编程涉及创建该指令列表，告诉计算机如何完成特定任务。精确的指令取决于你使用的编程语言。对于大多数编程语言，创建计算机程序需要经过以下步骤：

- 1. 使用文本编辑器输入编程语言中的命令序列。

这是完成任务的命令序列。这种人类可读的程序版本称为源文件或源代码。你可以使用任何能够以纯文本形式保存文档的应用程序（如文字处理器）来创建源文件。

始终将源代码保存为纯文本（文件名取决于编程语言的类型）。文字处理器有时会在文档中加入额外指令，告诉计算机以特定字体或其他格式显示文本。相信我，你的程序最好不要有这些东西。

- 2. 使用编译器程序将该文本文件——源代码——从人类可读形式转换为机器可读的目标代码。

通常，此步骤还会将多个目标代码文件合并成一个机器可读的计算机程序，即计算机实际可以运行的东西。

- 3. 使用名为调试器的特殊程序来追踪任何错误并找出源文件中可能导致错误的几行。

- 4. 返回步骤 1，使用文本编辑器修复错误并重复其余步骤。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_741_0.png)

前三个步骤被称为编程的编辑-编译-调试循环，因为大多数程序员在程序正确工作之前必须重复此序列几次。

除了学习基本的编程步骤之外，你还需要熟悉以下术语和概念：

- *变量* 用于存储不同类型的数据。你可以把每个变量想象成数据的占位符——有点像邮箱，有名称和存储数据的空间。变量的内容就是其值。
- *表达式* 通过使用运算符组合变量。表达式可能会添加多个变量；另一个可能会提取字符串的一部分。
- *语句* 执行某些操作，例如将值赋给变量或打印字符串。
- *流程控制语句* 允许语句根据某个表达式的值以各种顺序执行。通常，流程控制语句包括 `for`、`do while`、`while` 和 `if then else` 语句。
- *函数*（也称为 *子程序* 或 *例程*）允许你将多个语句分组并为其命名。此功能允许你通过调用代表这些语句的函数来执行同一组语句。通常，编程语言提供许多预定义函数来执行诸如打开（并从中读取）文件之类的任务。

## 探索 Red Hat Linux 中的软件开发工具

Red Hat Linux 包含这些传统的 UNIX 软件开发工具：

- 用于编辑源代码的文本编辑器，如 `vi` 和 `emacs`。（要了解有关 `vi` 的更多信息，请参阅第二册，第 6 章。）
- 用于编译和链接用 C 编写的程序的 C 编译器——编写 UNIX 应用程序的首选编程语言（尽管如今许多程序员转向 C++ 和 Java）。Red Hat Linux 包含 GNU C 和 C++ 编译器。最初，GNU C 编译器被称为 GCC——现在代表 *GNU 编译器集合*（请参阅 gcc.gnu.org 中的说明）。
- GNU `make` 实用程序用于自动化软件 *构建过程*——将目标模块组合成可执行文件或库的过程。
- 用于调试程序的调试器。Red Hat Linux 包含 GNU 调试器 `gdb`。
- 版本控制系统用于跟踪源文件的各种修订。Linux 附带 RCS（修订控制系统）和 CVS（并发版本系统）。如今大多数开源项目使用 CVS 作为其版本控制系统。

如果你在从本书附带的 DVD 安装 Red Hat Linux 时选择了开发工具，这些工具将自动安装。在接下来的几个部分中，我将简要描述如何使用这些软件开发工具为 Red Hat Linux 编写应用程序。

## GNU C 和 C++ 编译器

Red Hat Linux 中最重要的软件开发工具是 GCC——GNU C 和 C++ 编译器。事实上，GCC 可以编译三种语言：C、C++ 和 Objective-C（一种为 C 增加面向对象编程能力的语言）。你使用相同的 gcc 命令来编译和链接 C 和 C++ 源文件。GCC 编译器支持 ANSI 标准 C，使得将任何 ANSI C 程序移植到 Linux 变得容易。此外，如果你曾经在其他 UNIX 系统上使用过 C 编译器，你会发现使用 GCC 非常得心应手。

## 使用 GCC

使用 gcc 命令调用 GCC。默认情况下，当你对源文件使用 gcc 命令时，GCC 会预处理、编译并链接以创建可执行文件。然而，你可以使用 GCC 选项在中间阶段停止此过程。例如，你可能会使用 -c 选项调用 gcc 来编译源文件并生成目标文件，但不执行链接步骤。

使用 GCC 编译和链接几个 C 源文件非常简单。假设你想编译和链接一个由两个源文件组成的简单程序。我为此任务使用的程序源如下；它存储在文件 area.c 中，是计算通过命令行指定的圆半径面积的主程序：

```c
#include <stdio.h>
#include <stdlib.h>

/* Function prototype */
double area_of_circle(double r);

int main(int argc, char **argv)
{
    if(argc < 2)
    {
        printf("Usage: %s radius\n", argv[0]);
        exit(1);
    }
    else
    {
        double radius = atof(argv[1]);
        double area = area_of_circle(radius);
        printf("Area of circle with radius %f = %f\n", radius, area);
    }
    return 0;
}
```

我们需要另一个实际计算圆面积的文件。下面是文件 circle.c 的列表，其中我定义了一个计算圆面积的函数：

```c
#include <math.h>

#define SQUARE(x) ((x)*(x))

double area_of_circle(double r)
{
    return 4.0 * M_PI * SQUARE(r);
}
```

对于如此简单的程序，当然我本可以将所有内容放在一个文件中，但我需要这个人为的例子来向你展示如何处理多个文件。

要编译这两个文件并创建名为 area 的可执行文件，你使用以下命令：

```
gcc -o area area.c circle.c
```

此次调用 GCC 使用 -o 选项指定可执行文件的名称。（如果不使用 -o 选项指定输出文件的名称，GCC 会将可执行代码保存在名为 a.out 的文件中。）

如果要编译和链接的源文件太多，你可以单独编译文件并生成目标文件（扩展名为 .o）。这样，当你更改源文件时，只需编译该文件——然后只需将编译后的文件链接到所有目标文件即可。以下命令展示了如何为示例程序分离编译和链接步骤：

```
gcc -c area.c
gcc -c circle.c
gcc -o area area.o circle.o
```

前两个命令使用 -c 选项运行 gcc 编译源文件。第三个 gcc 命令将目标文件链接成名为 area 的可执行文件。



如果你好奇的话，下面是如何运行 area 程序（计算半径为 1 的圆的面积）：

```
./area 1
```

程序生成以下输出：

```
Area of circle with radius 1.000000 = 12.566371
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_745_0.png)

顺便说一下，只有当当前目录不在 PATH 环境变量中时，才需要在程序名称（area）前加上 ./ 前缀。即使 PATH 中包含当前目录，添加前缀也没有害处。

## 编译 C++ 程序

GNU CC 是一个集成的 C 和 C++ 编译器，因此 gcc 命令也可以编译 C++ 源文件。GCC 使用文件扩展名来判断文件是 C 还是 C++。C 文件具有小写的 .c 扩展名，而 C++ 文件以 .C 或 .cpp 结尾。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_745_1.png)

虽然 gcc 命令可以编译 C++ 文件，但该命令不会自动链接 C++ 程序通常所需的各种类库。这就是为什么使用 g++ 命令来编译和链接 C++ 程序更简单的原因，它会以适当的选项运行 gcc。

假设你想编译存储在名为 hello.C 的文件中的以下简单 C++ 程序（对于 C++ 源文件，使用大写 C 扩展名是惯例）：

```
#include <iostream>

int main()
{
    using namespace std;
    cout << "Hello from Red Hat Linux!" << endl;
}
```

要将此程序编译并链接为名为 hello 的可执行程序，请使用以下命令：

```
g++ -o hello hello.C
```

该命令创建 hello 可执行文件，你可以按如下方式运行它：

```
./hello
```

程序显示以下输出：

```
Hello from Red Hat Linux!
```

大量的 GCC 选项控制编译 C 和 C++ 程序的各个方面。

## 探索 GCC 选项

这是 gcc 命令的基本语法：

```
gcc options filenames
```

每个选项都以连字符 (-) 开头，通常具有长名称，例如 -funsigned-char 或 -finline-functions。然而，许多常用选项很短，例如 -c，仅编译，-g，生成调试信息（使用 GNU 调试器 gdb 调试程序时需要）。

你可以通过在终端窗口中输入以下命令来查看所有 GCC 选项的摘要：

```
man gcc
```

然后你可以浏览常用的 GCC 选项。通常，你不需要显式提供 GCC 选项，因为默认设置对大多数应用程序来说已经足够。表 1-1 列出了你可能使用的一些 GCC 选项。

表 1-1 常用 GCC 选项

| 选项 | 含义 |
|---|---|
| -ansi | 仅支持 ANSI 标准 C（ISO C89）语法。（此选项禁用了一些 GNU C 特定功能，例如 asm 和 typeof 关键字。） |
| -c | 编译并仅生成目标文件。 |
| -DMACRO | 定义宏，其值为字符串 "1"。 |
| -DMACRO=DEFN | 将宏定义为 DEFN，其中 DEFN 是某个文本字符串。 |
| -E | 仅运行 C 预处理器。 |
| -fallow-single-precision | 以单精度执行所有数学运算。 |
| -fpcc-struct-return | 将所有 struct 和 union 值返回到内存中，而不是返回到寄存器。（这种方式返回值的效率较低，但至少与其它编译器兼容。） |
| -fPIC | 生成适用于共享库的位置无关代码（PIC）。 |
| -freg-struct-return | 在可能的情况下，将 struct 和 union 值返回到寄存器。 |

**表 1-1（续）**

| 选项 | 含义 |
|---|---|
| -g | 生成调试信息。（GNU 调试器可以使用此信息。） |
| -I DIRECTORY | 搜索指定的目录以查找使用 #include 预处理器指令包含的文件。 |
| -L DIRECTORY | 搜索指定的目录以查找库。 |
| -l LIBRARY | 链接时搜索指定的库。 |
| -mcpu=cputype | 为特定处理器优化代码（cputype 可以取许多不同的值——一些常见的值有 i386、i486、i586 和 i686）。 |
| -o FILE | 生成指定的输出文件（用于指定可执行文件的名称）。 |
| -O0 | 不进行优化。 |
| -O or -O1 | 优化生成的代码。 |
| -O2 | 进一步优化。 |
| -O3 | 执行超出 -O2 的优化。 |
| -Os | 为大小优化（以减少代码总量）。 |
| -pedantic | 如果使用任何非 ANSI 标准扩展，则生成错误。 |
| -pg | 在程序中添加额外代码，以便运行时生成 gprof 程序可用于显示程序各部分计时细节的信息。 |
| -shared | 生成共享对象文件（通常用于创建共享库）。 |
| -UMACRO | 取消定义指定的宏。 |
| -v | 显示 GCC 的版本号。 |
| -w | 不生成任何警告信息。 |
| -Wl,OPTION | 将 OPTION 字符串（包含多个以逗号分隔的选项）传递给链接器。例如，要创建名为 libXXX.so.1 的共享库，请使用以下标志：-Wl,-soname,libXXX.so.1。 |

## GNU make 工具

当应用程序由多个源文件组成时，通过手动输入 gcc 命令来编译和链接文件会非常乏味。此外，你也不希望在单个源文件发生变化时重新编译每个文件。这时 GNU make 工具就能派上用场。

make 工具通过读取和解释 makefile 工作——makefile 是一个文本文件，描述了构建特定程序所需的文件，以及如何编译和链接这些文件来构建程序。每当你更改一个或多个文件时，make 会确定应重新编译哪些文件——并发出编译这些文件和重建程序的适当命令。

### Makefile 名称

默认情况下，GNU make 按所示顺序查找具有以下名称之一的 makefile：

- GNUmakefile
- makefile
- Makefile

在 UNIX 系统中，使用 Makefile 作为 makefile 的名称是惯例，因为它出现在目录列表的开头附近，其中大写名称出现在小写名称之前。

当你从互联网下载软件时，通常会找到一个 Makefile，连同源文件一起。要构建软件，你只需在 shell 提示符下输入 make，make 就会处理构建软件所需的所有步骤。

如果你的 makefile 没有标准名称（如 Makefile），你必须使用 make 的 -f 选项来指定 makefile 的名称。例如，如果你的 makefile 称为 myprogram.mak，你必须使用以下命令行运行 make：

```
make -f myprogram.mak
```

### makefile

对于由多个源文件和头文件组成的程序，makefile 指定以下内容：

- make 将创建的项目——通常是目标文件和可执行文件。常用术语 target 指 make 需要创建的任何项目。
- 创建目标所需的文件或其他操作。
- 应执行哪些命令来创建每个目标。

假设你有一个名为 form.C 的 C++ 源文件，其中包含以下预处理器指令：

```
#include "form.h"  // Include header file
```

目标文件 form.o 显然依赖于源文件 form.c 和头文件 form.h。除了这些依赖关系之外，你还必须指定 make 如何将 form.c 文件转换为目标文件 form.o。假设你希望 make 调用 g++（因为源文件是 C++）并使用以下选项：

- -c（仅编译）
- -g（生成调试信息）
- -O2（优化一些）

在 makefile 中，你可以用以下规则表达这一点：

```
# This is a comment in the makefile
# The following lines indicate how form.o depends
# form.c and form.h and how to create form.o.

form.o: form.c form.h
    g++ -c -g -O2 form.c
```

在此示例中，第一条非注释行显示 form.o 为目标，form.c 和 form.h 为依赖文件。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_749_0.png)

依赖关系之后的下一行指示如何从其依赖项构建目标。此行必须以制表符开头。

使用 make 的好处是它可以防止不必要的编译。毕竟，你可以从 shell 脚本运行 g++（或 gcc）来编译和链接构成应用程序的所有文件，但 shell 脚本会编译所有内容，即使编译是不必要的。另一方面，GNU make 仅在目标的一个或多个依赖项自上次构建目标以来发生变化时才构建目标。make 通过检查目标及其依赖项的最后修改时间来验证此更改。

make 将目标视为要实现的目标的名称；目标不必是文件。你可以有如下规则：

```
clean:
    rm -f *.o
```

此规则指定了一个名为 clean 的抽象目标，它不依赖于任何内容。此依赖语句表示要创建目标 clean，GNU make 应调用命令 rm -f *.o，该命令删除所有具有 .o 扩展名的文件（即目标文件）。因此，创建名为 clean 的目标的净效果是删除目标文件。



## 变量（或宏）

除了从依赖项构建目标的基本功能之外，GNU make 还包含许多很棒的功能，使您可以轻松地表达从其依赖项构建目标的依赖关系和规则。例如，如果您需要使用相同的选项通过 GCC 编译大量 C++ 文件，为每个文件输入选项是乏味的。您可以通过在 make 中按如下方式定义变量或宏来避免这种重复任务：

```make
# Define macros for name of compiler
CXX= g++
# Define a macro for the GCC flags
CXXFLAGS= -O2 -g -mcpu=i686
# A rule for building an object file
form.o: form.c form.h
    $(CXX) -c $(CXXFLAGS) form.c
```

在此示例中，CXX 和 CXXFLAGS 是 make 变量。（GNU make 喜欢称它们为变量，但大多数 UNIX make 实用程序称它们为宏。）

要在 makefile 中的任何位置使用变量，请以美元符号 ($) 开头，后跟括号内的变量。GNU make 用其定义替换变量的所有出现；因此它用字符串 -O2 -g -mcpu=i686 替换 $(CXXFLAGS) 的所有出现。

GNU make 有几个具有特殊含义的预定义变量。表 1-2 列出了这些变量。除了表 1-2 中列出的变量之外，GNU make 还将所有环境变量（例如 PATH 和 HOME）视为预定义变量。

**表 1-2 GNU make 中的一些预定义变量**

| Variable | Meaning |
|---|---|
| $% | 归档目标的成员名。例如，如果目标是 libDisp.a(image.o)，则 $% 为 image.o，而 $@ 为 libDisp.a。 |
| $* | 目标文件不带扩展名的名称。 |
| $+ | 列出所有依赖文件（包含重复依赖），按出现顺序排列的名称。 |
| $< | 第一个依赖文件的名称。 |
| $? | 比目标更新的所有依赖文件的名称（名称之间用空格分隔）。 |
| $@ | 目标的完整名称。 |

表 1-2（续）

| Variable | Meaning |
|---|---|
| $^ | 所有依赖文件的名称，名称之间用空格分隔。依赖文件名中的重复项会被移除。 |
| AR | 维护归档的程序名称（默认值：ar）。 |
| ARFLAGS | 归档维护程序的标志（默认值：r v）。 |
| AS | 将汇编语言转换为目标代码的汇编程序名称（默认值：as）。 |
| ASFLAGS | 汇编器的标志。 |
| CC | C 编译器的名称：（默认值：cc）。 |
| CFLAGS | 传递给 C 编译器的标志。 |
| CO | 从 RCS 中提取文件的程序名称（默认值：co）。 |
| COFLAGS | RCS co 程序的标志。 |
| CPP | C 预处理器的名称（默认值：$(CC) -E）。 |
| CPPFLAGS | C 预处理器的标志。 |
| CXX | C++ 编译器的名称（默认值：g++）。 |
| CXXFLAGS | 传递给 C++ 编译器的标志。 |
| FC | FORTRAN 编译器的名称（默认值：f77）。 |
| FFLAGS | FORTRAN 编译器的标志。 |
| LDFLAGS | 编译器在应调用链接器 ld 时的标志。 |
| RM | 删除文件的命令名称（默认值：rm -f）。 |

## 一个示例 makefile

如果您使用 GNU make 的预定义变量和内置规则，可以轻松编写 makefile。例如，考虑一个 makefile，它从三个 C 源文件（xdraw.c、xviewobj.c 和 shapes.c）和两个头文件（xdraw.h 和 shapes.h）创建可执行文件 xdraw。假设每个源文件都包含其中一个头文件。鉴于这些事实，一个示例 makefile 可能如下所示：

```make
##################################################
# Sample makefile
# Comments start with '#'
#
##################################################

# Use standard variables to define compile and link flags

CFLAGS= -g -O2
# Define the target "all"
all: xdraw
OBJS=xdraw.o xviewobj.o shapes.o
xdraw: $(OBJS)
# Object files
xdraw.o: Makefile xdraw.c xdraw.h
xviewobj.o: Makefile xviewobj.c xdraw.h
shapes.o: Makefile shapes.c shapes.h
```

此 makefile 依赖于 GNU make 隐式规则。.c 文件到 .o 文件的转换使用内置规则。定义变量 CFLAGS 会将标志传递给 C 编译器。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_752_0.png)

目标名为 all 被定义为第一个目标是有原因的——如果您在命令行中不指定任何目标运行 GNU make（请参阅以下部分中描述的 make 语法），则命令会构建 makefile 中找到的第一个目标。通过将第一个目标 all 定义为 xdraw，您可以确保 make 构建此可执行文件，即使您没有明确将其指定为目标。UNIX 程序员传统上使用 all 作为第一个目标的名称，但目标的名称无关紧要；重要的是它是 makefile 中的第一个目标。

## 如何运行 make

通常，您只需在 shell 提示符下键入以下命令即可运行 make：

```
make
```

以这种方式运行，GNU make 会按以下顺序查找名为 GNUmakefile、makefile 或 Makefile 的文件。如果 make 找到其中一个 makefile，它会构建该 makefile 中指定的第一个目标。但是，如果 make 未找到合适的 makefile，它会显示以下错误消息然后退出：

```
make: *** No targets specified and no makefile found.  Stop.
```

如果您的 makefile 恰好具有与默认名称不同的名称，则必须使用 -f 选项指定 makefile。使用此选项的 make 命令的语法如下所示：

```
make -f filename
```

其中 filename 是 makefile 的名称。

即使您有一个具有默认名称（如 `Makefile`）的 makefile，您也可能希望从 makefile 中定义的多个目标中构建特定目标。在这种情况下，您在运行 `make` 时必须使用以下语法：

```
make target
```

例如，如果 makefile 包含名为 `clean` 的目标，您可以使用以下命令构建该目标：

```
make clean
```

另一种特殊语法会覆盖 `make` 变量的值。例如，GNU `make` 使用 `CFLAGS` 变量来保存编译 C 文件时使用的标志。您可以在调用 `make` 时覆盖此变量的值。以下是如何将 `CFLAGS` 定义为选项 `-g -O2` 的示例：

```
make CFLAGS="-g -O2"
```

除了这些选项之外，GNU `make` 还接受其他命令行选项。表 1-3 列出了 GNU `make` 选项。

## 表 1-3 GNU make 的选项

| Option | Meaning |
|---|---|
| `-b` | 忽略但接受，以兼容其他版本的 make。 |
| `-C DIR` | 在读取 makefile 之前切换到指定目录。 |
| `-d` | 打印调试信息。 |
| `-e` | 允许环境变量覆盖 makefile 中同名变量的定义。 |
| `-f FILE` | 将 FILE 作为 makefile 读取。 |
| `-h` | 显示 make 选项列表。 |
| `-i` | 构建目标时忽略命令执行中的所有错误。 |
| `-I DIR` | 在指定目录中搜索包含的 makefile（在 makefile 中包含文件的能力是 GNU make 独有的）。 |
| `-j NUM` | 指定 make 可同时运行的命令数。 |
| `-k` | 即使构建其中一个目标时出错，也继续构建不相关的目标。 |
| `-l LOAD` | 如果负载平均值至少为 LOAD（浮点数），则不启动新作业。 |
| `-m` | 忽略但接受，以兼容其他版本的 make。 |
| `-n` | 打印将要执行的命令，但不执行它们。 |

| Option | Meaning |
|---|---|
| -o FILE | 即使 FILE 比其依赖项旧，也不要重建名为 FILE 的文件。 |
| -p | 显示 make 的变量和隐式规则数据库。 |
| -q | 不运行任何内容，但如果所有目标都是最新的则返回零；如果需要更新则返回 1，如果发生错误则返回 2。 |
| -r | 去除所有内置规则。 |
| -R | 去除所有内置变量和规则。 |
| -s | 静默工作（不显示正在执行的命令）。 |
| -t | 更改文件的时间戳。 |
| -v | 显示 make 的版本号和版权声明。 |
| -w | 在处理 makefile 之前和之后显示工作目录的名称。 |
| -W FILE | 假定指定文件已被修改（与 -n 一起使用以查看修改该文件时会发生什么）。 |

## GNU 调试器

虽然 make 自动化了构建程序的过程，但当程序无法正确工作或程序突然因错误消息而退出时，编程中最不令人担忧的部分就是构建程序。您需要一个调试器来查找程序错误的根本原因。Red Hat Linux 包含 gdb——具有命令行界面的多功能 GNU 调试器。

像任何调试器一样，gdb 允许您执行典型的调试任务，例如以下内容：

- 设置断点，以便程序在指定行停止。
- 监视程序中变量的值。
- 一次一行地逐步执行程序。
- 更改变量以尝试修复错误。

gdb 调试器可以调试 C 和 C++ 程序。

## 准备调试程序

如果您想使用 gdb 调试程序，您必须确保编译器在可执行文件中生成并放置调试信息。调试信息包含程序中变量的名称以及可执行文件中地址到源文件中代码行的映射。gdb 需要此信息来执行其功能，例如在执行源代码的指定行后停止。



![](img/a7eec43a54473e95dc5ea333fecf1bd7_755_0.png)

为确保可执行文件正确准备用于调试，请使用 -g 选项编译 GCC。您可以通过在 makefile 中定义变量 CFLAGS 来实现，如下所示

```
CFLAGS= -g
```

## 运行 gdb

调试程序最常见的方法是使用以下命令运行 gdb：

```
gdb progname
```

progname 是程序可执行文件的名称。运行后，gdb 显示以下消息并提示您输入命令：

```
GNU gdb Red Hat Linux (5.3post-1.20021129-37rh)
Copyright 2003 Free Software Foundation, Inc.
GDB is free software, covered by the GNU General Public License, and you are welcome to change it and/or distribute copies of it under certain conditions.
Type "show copying" to see the conditions.
There is absolutely no warranty for GDB. Type "show warranty" for details.
This GDB was configured as "i386-redhat-linux-gnu".
(gdb)
```

您可以在 (gdb) 提示符下输入 gdb 命令。一个有用的命令是 help — 它显示命令列表，如下所示：

```
(gdb) help
List of classes of commands:
  aliases -- Aliases of other commands
  breakpoints -- Making program stop at certain points
  data -- Examining data
  files -- Specifying and examining files
  internals -- Maintenance commands
  obscure -- Obscure features
  running -- Running the program
  stack -- Examining the stack
  status -- Status inquiries
  support -- Support facilities
  tracepoints -- Tracing program execution without stopping the program
  user-defined -- User-defined commands

Type "help" followed by a class name for a list of commands in that class.
Type "help" followed by command name for full documentation.
Command name abbreviations are allowed if unambiguous.
(gdb)
```

要退出 gdb，请键入 q 然后按 Enter。

gdb 有大量命令，但您只需要其中几个就能快速找到错误的根源。表 1-4 列出了常用的 gdb 命令。

## 表 1-4 常用 gdb 命令

| 此命令 | 执行以下操作 |
|---|---|
| break NUM | 在指定的行号设置断点（调试器会在断点处停止）。 |
| bt | 显示所有栈帧的跟踪。（此命令显示迄今为止的函数调用序列。） |
| clear FILENAME:NUM | 删除源文件中的特定行断点。例如，clear xdraw.c:8 清除文件 xdraw.c 第 8 行的断点。 |
| continue | 继续运行被调试的程序。（在程序因信号或断点而停止后使用此命令。） |
| display EXPR | 每次程序停止时显示表达式（由程序中定义的变量组成）的值。 |
| file FILE | 加载指定的可执行文件进行调试。 |
| help NAME | 显示名为 NAME 的命令的帮助。 |
| info break | 显示当前断点列表，包括每个断点被命中的次数信息。 |
| info files | 显示正在调试的文件的详细信息。 |
| info func | 显示所有函数名。 |
| info local | 显示当前函数的局部变量信息。 |
| info prog | 显示正在调试的程序的执行状态。 |
| info var | 显示所有全局和静态变量名。 |
| kill | 结束您正在调试的程序。 |
| list | 列出源代码的一部分。 |
| make | 运行 make 实用程序重建可执行文件，而无需离开 gdb。 |
| next | 在当前函数中推进一行源代码，而不进入其他函数。 |
| print EXPR | 显示表达式 EXPR 的值。 |
| quit | 退出 gdb。 |
| run | 开始运行当前加载的可执行文件。 |
| set variable VAR=VALUE | 将变量 VAR 的值设置为 VALUE。 |
| shell CMD | 执行 UNIX 命令 CMD，而不离开 gdb。 |
| step | 在当前函数中推进一行，如果有则进入其他函数。 |

表 1-4（续）

| 此命令 | 执行以下操作 |
|---|---|
| watch VAR | 每当变量 VAR 的值发生变化时显示其值。 |
| where | 显示调用序列。使用此命令定位程序崩溃的位置。 |
| x/F ADDR | 以字母 F 指定的格式检查地址 ADDR 处的内存位置内容，F 可以是 o（八进制）；x（十六进制）；d（十进制）；u（无符号十进制）；t（二进制）；f（浮点）；a（地址）；i（指令）；c（字符）；或 s（字符串）。您可以在格式字母后附加一个表示数据类型大小的字母。大小字母为 b（字节）；h（半字，2 字节）；w（字，4 字节）；和 g（巨型，8 字节）。通常，ADDR 是变量或指针的名称。 |

## 使用 gdb 查找错误

要了解如何使用 gdb 查找错误，您需要看一个示例。最容易用简单示例来展示该过程，因此我从一个包含典型错误的人为构造程序开始。

这是人为构造的程序，我将其存储在文件 dbgtst.c 中：

```c
#include <stdio.h>

static char buf[256];
void read_input(char *s);

int main(void)
{
    char *input = NULL; /* Just a pointer, no storage for string */
    read_input(input);
    /* Process command. */
    printf("You typed: %s\n", input);
    /* ... */
    return 0;
}

void read_input(char *s)
{
    printf("Command: ");
    gets(s);
}
```

该程序的 main 函数调用 read_input 函数从用户获取一行输入。read_input 函数期望一个字符数组，在其中返回用户输入的内容。然而，在此示例中，main 使用未初始化的指针调用 read_input —— 这就是这个简单程序中的错误。

使用 -g 选项通过 gcc 构建程序：

```
gcc -g -o dbgtst dbgtst.c
```

忽略关于 gets 函数危险的警告信息；我试图利用该函数的缺陷来展示如何使用 gdb 追踪错误。

要查看此程序的问题，请运行它并在命令提示符下输入 test：

```
./dbgtst
Command: test
Segmentation fault
```

程序在显示 Segmentation fault 消息后终止。对于如此小的程序，您可能可以通过检查源代码找到原因。然而，在实际应用中，您可能无法立即知道错误的原因。这时您必须使用 gdb 来找到问题的根源。

要使用 gdb 定位错误，请按以下步骤操作：

- 1. 在 gdb 下加载程序。要在 gdb 中加载名为 dbgtst 的程序，请键入以下内容：
  
      gdb dbgtst
  
- 2. 通过键入 run 命令在 gdb 下开始执行程序。当程序提示输入时，键入一些输入文本。

程序应像之前一样失败。dbgtst 程序发生的情况如下：

```
(gdb) run
Starting program: /home/naba/rhls4e/dbgtst
Command: test
Program received signal SIGSEGV, Segmentation fault.
0x420632cc in gets () from /lib/tls/libc.so.6
(gdb)
```

### 3. 使用 where 命令确定程序在哪终止。

对于 dbgtst 程序，此命令产生以下输出：

```
(gdb) where
#0  0x420632cc in gets () from /lib/tls/libc.so.6
#1  0x080483bc in read_input (s=0x0) at dbgtst.c:22
#2  0x0804837e in main () at dbgtst.c:10
#3  0x420154a0 in __libc_start_main () from
/lib/tls/libc.so.6
(gdb)
```

输出显示函数调用序列。函数调用 #0 —— 最近的一个 —— 是对 C 库函数 gets 的调用。gets 调用源自 read_input 函数（dbgtst.c 文件第 22 行），而该函数又在 dbgtst.c 文件第 10 行从 main 函数调用。

### 4. 使用 list 命令检查可疑源代码的行。

在 dbgtst 中，您可以从 dbgtst.c 文件的第 22 行开始，如下所示：

```
(gdb) list dbgtst.c:22
17     }
18
19     void read_input(char *s)
20     {
21         printf("Command:");
22         gets(s);
23     }
24
(gdb)
```

查看此列表后，您应该能够判断问题可能出在 read_input 的调用方式上。然后您列出 dbgtst.c 中第 10 行周围的行（read_input 调用由此产生）：

```
(gdb) list dbgtst.c:10
5
6    int main(void)
7    {
8        char *input = NULL; /* Just a pointer, no
   storage for string */
9
10       read_input(input);
11
12       /* Process command. */
13       printf("You typed: %s\n", input);
14
(gdb)
```

此时，您应该能够将问题缩小到名为 input 的变量。该变量应为数组，而不是 NULL（表示零）指针。



## 在 gdb 中修复错误

有时你可以直接在 gdb 中修复一个错误。对于前一节中的示例程序，你可以在程序显示错误信息后崩溃时立即尝试此修复。由于该示例是人为构造的，我在 dbgtst 程序中定义了一个名为 buf 的额外缓冲区，如下所示：

```
static char buf[256];
```

我可以通过将变量 input 设置为 buf 来修复未初始化指针的问题。以下与 gdb 的会话纠正了未初始化指针的问题（此示例在程序因段错误运行并崩溃后立即开始）：

```
(gdb) file dbgtst
A program is being debugged already. Kill it? (y or n) y

Load new symbol table from "dbgtst"? (y or n) y
Reading symbols from dbgtst...
done.
(gdb) list
1 #include <stdio.h>
2
3 static char buf[256];
4 void read_input(char *s);
5
6 int main(void)
7 {
8 char *input = NULL; /* Just a pointer, no storage */
9
10 read_input(input);
(gdb) break 9
Breakpoint 1 at 0x8048373: file dbgtst.c, line 9.
(gdb) run
Starting program: /home/naba/rhls4e/dbgtst

Breakpoint 1, main () at dbgtst.c:10
10 read_input(input);
(gdb) set var input=buf
(gdb) cont
Continuing.
Command: test
You typed: test

Program exited normally.
(gdb) q
```

如前面的列表所示，如果我在调用 `read_input` 之前停止程序并将名为 `input` 的变量设置为 `buf`（它是一个有效的字符数组），程序的其余部分运行正常。

在 `gdb` 中找到可行的修复方法后，你可以对源文件进行必要的更改并使修复永久生效。

## 理解 GNU 许可证的影响

你必须为 Linux 的丰硕成果付出代价——为了保护其开发者和用户，Linux 在 GNU GPL（通用公共许可证）下分发，该许可证规定了源代码的分发。

然而，这并不意味着你不能为 Linux 编写商业软件并仅以二进制形式分发（无论是免费还是收费）。

你可以遵守所有规则，同时仍以二进制形式销售你的 Linux 应用程序。

编写 Linux 应用程序时，请注意两种许可证：

- GNU 通用公共许可证（GPL），它管理着许多 Linux 程序，包括 Linux 内核和 GCC
- GNU 库通用公共许可证（LGPL），它涵盖了许多 Linux 库

![](img/a7eec43a54473e95dc5ea333fecf1bd7_761_0.png)

以下各节提供了这些许可证的概述以及满足其要求的建议。然而，由于我不是律师，请不要将本书中的任何内容视为法律建议。这些许可证的全文位于你的 Red Hat Linux 系统上的文本文件中；请向你的法律顾问展示这些许可证以获得完整的解释并评估其对你业务的适用性。

### GNU 通用公共许可证

GNU 通用公共许可证（GPL）的文本位于 Red Hat Linux 系统中各个目录中名为 `COPYING` 的文件中。例如，输入以下命令以阅读 GPL：

```
cd /usr/share/doc/gdb*
more COPYING
```

GPL 与你是否收费或免费分发软件无关；其核心是让软件对所有用户保持自由。GPL 通过要求软件以源代码形式分发并规定任何用户都可以将软件以源代码形式复制和分发给任何其他人来实现这一点。此外，每个人都被提醒该软件完全没有任何担保。

GPL 涵盖的软件不属于公共领域。受 GPL 涵盖的软件始终受版权保护，并且 GPL 明确规定了软件复制和分发的限制。从用户的角度来看，当然，GPL 的限制实际上不是限制；这些限制实际上是好处，因为用户保证可以访问源代码。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_762_0.png)

如果你的应用程序使用了 GPL 涵盖的任何软件的部分，则你的应用程序被视为衍生作品。这意味着你的应用程序也受 GPL 涵盖，你必须分发你的应用程序的源代码。

尽管 GPL 涵盖了 Linux 内核，但 GPL 不涵盖通过系统调用使用内核服务的应用程序。这些应用程序被视为对内核的正常使用。

如果你计划以二进制形式分发你的应用程序（如大多数商业软件的分发方式），你必须确保你的应用程序不使用 GPL 涵盖的任何软件的任何部分。当你的应用程序调用库中的函数时，它可能会最终使用其他软件的部分。然而，大多数库受不同的 GNU 许可证涵盖，我将在下一节中描述。

你只需注意 GPL 涵盖的少数库和实用程序。GNU dbm（gdbm）数据库库是 GPL 涵盖的知名库之一。GNU bison 解析器生成工具是 GPL 涵盖的另一个实用程序。如果你允许 bison 生成代码，则 GPL 涵盖该代码。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_762_1.png)

GNU dbm 和 GNU bison 的其他替代方案不受 GPL 涵盖。对于数据库库，你可以使用 Berkeley 数据库库 db 代替 gdbm。对于解析器生成器，你可以使用 yacc 代替 bison。

### GNU 库通用公共许可证

GNU 库通用公共许可证（LGPL）的文本位于文件 COPYING.LIB 中。如果你已安装内核源代码，则 COPYING.LIB 文件的副本位于其中一个源代码目录中。要在 Red Hat Linux 系统上定位 COPYING.LIB 文件的副本，请在终端窗口中输入以下命令：

```
find /usr/share/doc -name "COPYING*" -print
```

此命令列出系统中 COPYING 和 COPYING.LIB 的所有出现位置。COPYING 文件包含 GPL，而 COPYING.LIB 包含 LGPL。

LGPL 的目的是允许在你的应用程序中使用库，即使你不分发应用程序的源代码。然而，LGPL 规定用户必须能够访问你使用的库的源代码，并且用户可以使用这些库的修改版本。

LGPL 涵盖了大多数 Linux 库，包括 C 库（libc.a）。因此，当你使用 GCC 编译器在 Red Hat Linux 上构建应用程序时，你的应用程序会与一个或多个受 LGPL 涵盖的库中的代码链接。如果你只想以二进制形式分发你的应用程序，你需要关注 LGPL。

满足 LGPL 目的的一种方法是提供你的应用程序的目标代码以及一个 makefile，该 makefile 可将你的目标文件与 LGPL 涵盖的任何更新的 Linux 库重新链接。

满足 LGPL 的更好方法是使用动态链接，在这种链接方式中，你的应用程序和库是独立的实体，即使你的应用程序在运行时调用库中的函数。通过动态链接，用户可以立即获得库的任何更新的好处，而无需重新链接应用程序。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_763_0.png)

### 第 2 章：C 编程

### 本章内容

- ✓ 学习 C 编程的基础知识
- ✓ 学习 C 编程语言的特性
- ✓ 盘点标准 C 库
- ✓ 在 Red Hat Linux 应用程序中使用共享库

C 编程语言的构成——稀疏的核心加上庞大的支持库——使其成为开发软件的理想语言。核心提供了良好的数据类型和控制结构选择，而所有额外任务，包括输入和输出（I/O）、数学计算以及对外围设备的访问，都被委派给函数库。基本上，C 允许你访问系统中你想要的任何东西。这意味着你可以用 C 编写从设备驱动程序到图形应用程序的任何东西。在本章中，我向你介绍 C 编程。我还简要解释了共享库的重要性以及如何使用 C 编程语言在 Red Hat Linux 中创建共享库。

### C 程序的结构

典型的 C 程序组织成一个或多个源文件，或模块（图 2-1）。每个文件具有相似的结构，包括注释、预处理器指令、变量和函数的声明以及它们的定义。你通常会将每组相关的变量和函数放在单个源文件中。

一些文件只是声明集，通过 C 预处理器的 `#include` 指令在其他文件中使用。这些文件通常称为头文件，其名称以 `.h` 扩展名结尾。在图 2-1 中，文件 `shapes.h` 是一个头文件，声明了程序的通用数据结构和函数。另一个文件 `shapes.c` 定义了函数。第三个文件 `shapetest.c` 实现了 `main` 函数——这是 C 程序执行的开始函数。这些名称以 `.c` 结尾的文件是源文件，你在其中定义程序所需的函数。尽管图 2-1 在每个源文件中只显示一个函数，但在典型程序中源文件中有许多函数。



![](img/a7eec43a54473e95dc5ea333fecf1bd7_765_0.png)

创建可执行程序时，必须编译并链接源文件。从 C 源文件构建程序的确切步骤取决于编译器和操作系统。例如，在 Red Hat Linux 中，可以使用以下命令编译并链接图 2-1 中显示的文件：

```
gcc -o shapetest shapetest.c shapes.c
```

该命令创建名为 shapetest 的可执行文件。然后你可以用以下命令运行该文件

```
./shapetest
```

以下是程序显示的输出：

```
Area of circle = 7853.981634
```

## 声明与定义

声明决定程序如何解释一个符号。而定义则实际创建变量或函数。定义会导致编译器为数据或代码分配存储空间，而声明则不会。例如，

```
int x, y, z;
```

是三个不同整数变量的定义，但

```
extern int x, y, z;
```

是声明，表示这三个整数变量在另一个源文件中定义。

在每个源文件中，程序的组件以标准方式排列。如图 2-1 所示的文件所示，如果你在屏幕上向下滚动，C 源文件的典型组件遵循一定的顺序：

- 1. 文件以一些注释开头，这些注释描述了模块的目的并提供其他相关信息，例如作者姓名和修订日期。在 C 中，注释以 /* 开始，以 */ 结束。
- 2. 用于预处理器的命令，即预处理器指令，跟在注释之后。前几个指令通常用于包含头文件和定义常量。
- 3. 接下来是可在整个文件中可见的变量和函数的声明。换句话说，这些变量和函数的名字可在本文件中的任何函数中使用。在这里，你还定义了文件内部需要的变量。
- 4. 文件的其余部分包含函数的定义。在函数体内部，你可以定义仅在函数代码执行期间存在的局部变量。

## 预处理器指令

预处理是指将 C 文件翻译或编译成机器指令的第一步。预处理器处理源文件并对程序中嵌入的某些命令（称为预处理器指令）执行操作。这些指令以井号（#）开头，后跟关键字。通常编译器在开始编译前会自动调用预处理器，但大多数编译器允许你单独调用预处理器。你可以利用预处理器的三大主要功能使程序更模块化、可读性更强且更易于定制：

- 你可以使用 `#include` 指令将文件的内容插入到程序中。这样，你可以将常用声明放在一个位置，并通过文件包含在所有源文件中使用。结果是减少了不同程序模块中变量和函数声明不匹配的风险。
- 通过 `#define` 指令，你可以定义宏以用另一个字符串替换一个字符串。你可以使用 `#define` 指令为数值常量赋予有意义的名称，从而提高源文件的可读性。
- 使用 `#if`、`#ifdef`、`#else` 和 `#endif` 等指令，你可以仅编译程序的选定部分。你可以利用此功能编写包含两个或多个系统代码的源文件，但仅编译适用于编译程序的计算机系统的部分。通过这种策略，你可以使用同一套源文件维护程序的多个版本。

## 包含文件

你可以通过利用 `#include` 指令编写模块化程序。这是因为 C 预处理器使你能够将常用声明保存在单个文件中，并在需要时将其插入其他源文件。ANSI C 支持 `#include` 指令的三种形式。作为 C 程序员，你应该熟悉前两种形式：

```
#include <stdio.h>
#include "shapes.h"
```

你使用第一种形式的 `#include` 来读取文件的内容——在本例中，从所有头文件所在默认位置读取标准 C 头文件 `stdio.h`。当文件（例如 `shapes.h`）位于当前目录时，将文件名放在双引号内。定位包含文件确切的约定取决于编译器。

## 定义宏

一个 `macro` 本质上是可重用 C 代码块的简短名称。代码可以简单到数值常量，也可以复杂到多行详细的 C 代码。其思想是，定义宏后，你可以在程序中需要使用该代码的任何地方使用该宏。在源文件预处理时，宏名称的每次出现都会被其定义替换。

宏的常见用途是为数值常量定义符号名称，然后在程序中使用该符号代替数字。这提高了源代码的可读性；使用描述性名称，你不必猜测程序中使用特定数字的原因。你可以使用 #define 指令以直接的方式定义此类宏。以下是一些示例：

```
#define PI 3.14159
#define GRAV_ACC 9.80665
#define BUFSIZE 512
```

定义这些符号后，你可以在整个源文件中使用 PI、GRAV_ACC 和 BUFSIZE 代替这些数值常量。

然而，宏的功能远不止简单地用常量或代码块替换符号。宏可以接受参数，并在程序中使用宏时用提供的值替换该参数的每次出现。因此，宏展开后得到代码可能会根据使用宏时使用的参数而改变。例如，这里有一个接受参数并展开为计算该参数平方的表达式的宏：

```
#define square(x) ((x)*(x))
```

如果你在程序中使用 square(z)，源文件预处理后它会变成 ((z)*(z))。实际上，此宏等效于计算其参数平方的函数——只是你不调用函数。相反，由宏生成的表达式直接放置在源文件中。

## 条件指令

你可以使用 #if、#ifdef、#ifndef、#else、#elif 和 #endif 等条件指令来控制源文件的哪些部分在什么条件下被编译。借助此功能，你可以维护一套源文件，可在不同编译器和不同环境中选择性编译。（另一个常见用途是插入仅在名为 DEBUG 的符号被定义时才编译的用于调试的 printf 语句。）条件指令以 #if、#ifdef 或 #ifndef 开头——后面可以跟任意数量的 #elif 指令（或根本不跟）。接下来是可选的 #else，然后是标记该条件块结束的 #endif 指令。以下是使用条件指令的一些常见方法。

为了仅包含一次头文件，你可以使用以下方法：

```
#ifndef __PROJECT_H
#define __PROJECT_H
/* Declarations to be included once */
/* ... */
#endif
```

以下内容在调试期间（当符号 DEBUG 被定义时）打印诊断消息：

```c
#ifdef DEBUG
printf("In read_file: bytes_read = %d\n", bytes_read);
#endif
```

以下示例展示了如何根据程序编译的系统类型包含不同的头文件。要有选择地包含头文件，可以使用以下方法：

```c
#if CPU_TYPE == I386
#include <i386sysdef.h>
#elif CPU_TYPE == M68K
#include <m68ksysdef.h>
#else
#error Unknown CPU type.
#endif
```

#error 指令用于在预处理期间显示错误消息。

## 其他指令

还有一些其他预处理器指令执行各种任务。例如，你可以使用 #undef 指令删除符号的当前定义。#pragma 指令是另一个特殊用途指令，可用于向 C 编译器传达信息。你可以使用 pragma 访问编译器的特殊功能——这些功能因编译器而异。

C 编译器提供多个预定义宏（参见表 2-1）。其中，宏 __FILE__ 和 __LINE__ 分别引用当前源文件名和正在处理的当前行号。你可以使用 #line 指令更改它们。例如，要将 __FILE__ 设置为 "file_io.c" 并将 __LINE__ 设置为 100，你可以这样写：

```c
#line 100 "file_io.c"
```

**表 2-1 C 中的预定义宏**

| 宏 | 定义 |
|---|---|
| `__DATE__` | 这是一个包含调用 C 编译器时日期的字符串。其格式为 MMM DD YYYY（例如，Oct 26 2002）。 |
| `__FILE__` | 这会扩展为包含源文件名称的字符串。 |




| 宏 | 定义 |
|---|---|
| __LINE__ | 这是一个十进制整数，其值等于当前源文件中的行号。 |
| __STDC__ | 该宏展开为十进制常量 1，用以表示 C 编译器符合 ANSI 标准。 |
| __TIME__ | 该字符串显示开始编译源文件的时间。其格式为 HH:MM:SS（例如，21:59:45）。 |

## 变量的声明与定义

在 C 语言中，你必须在使用变量和函数之前先定义或声明它们。变量的定义指定了三件事：

- 其 *visibility*，表示变量可以使用的确切位置（是定义在程序的所有文件中、当前文件，还是仅在某个函数中）。
- 其 *lifetime*，决定变量是临时存在（例如函数中的局部变量）还是永久存在（只要程序在运行）。
- 其 *type*（在某些情况下还有其 *initial value*）。例如，初始化为 1 的整数变量 x 是这样定义的：

```c
int x = 1;
```

如果你使用在另一个源文件中定义的变量，则使用 extern 关键字声明该变量，如下所示：

```c
extern int message_count;
```

你必须在至少一个源文件中不带 extern 限定符地定义此变量。程序构建时，链接器会解析对 message_count 变量的所有引用，并确保它们都使用同一个变量。

## 基本数据类型

C 有四种基本数据类型：char 和 int 用于存储字符和整数，而 float 和 double 用于浮点数。你可以以直接的方式为这些基本数据类型定义变量：

```c
char c;
int i, j, bufsize;
float volts;
double mean, variance;
```

你可以通过使用 long、short 和 unsigned 限定符作为前缀，将基本数据类型扩展为更大的集合。long 和 short 限定符是大小修饰符。例如，long int 至少为 4 字节长，而 short int 的最小大小仅为 2 字节。int 的大小取决于系统，但它肯定至少与 short 一样大。

unsigned 限定符仅保留给 int 和 char 类型。通常，这些类型同时保存负值和正值。这是这些数据类型的默认 signed 形式。当你希望变量仅保存正值时，可以使用 unsigned 限定符。以下是使用 short、long 和 unsigned 限定符的一些示例：

```c
unsigned char mode_select;
unsigned char printer_status;
short record_number; /* Same as "short int" */
long offset; /* Same as "long int" */
unsigned int i, j, msg_id; /* Same as "unsigned int" */
unsigned short width, height; /* Same as "unsigned short int" */
unsigned long file_pos; /* Same as "unsigned long int" */
long double result;
```

当 short、long 和 unsigned 限定符与 int 类型一起使用时，可以在声明中省略 int。你也可以使用 long 前缀扩展 double 数据类型。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_771_0.png)

GCC 附带了预定义的头文件 — limits.h 和 float.h — 它们在这些头文件中定义了各种数据类型的确切大小以及值的范围。你可以在 Red Hat Linux 系统的 /usr/include 目录中检查这些文件，以确定 GCC 编译器支持的基本数据类型的大小。

## 枚举

你可以使用 enum 数据类型定义自己的枚举列表——一组固定的命名整数常量。例如，你可以使用 enum 如下声明一个名为 BOOLEAN 的布尔数据类型：

/* Declare an enumerated type named BOOLEAN */
enum BOOLEAN {false = 0, true = 1, stop = 0, go = 1,
    off = 0, on = 1};

/* Define a BOOLEAN called "status" and initialize it */
enum BOOLEAN status = stop;

此示例首先声明 BOOLEAN 为枚举类型。大括号内的列表显示了 enum BOOLEAN 变量的有效枚举常量。你可以按自己的选择初始化每个常量，并且多个常量可以使用相同的值。在此示例中，常量 false、stop 和 off 被设为 0，而 true、go 和 on 被初始化为 1。该示例随后定义了一个名为 status 的枚举 BOOLEAN 变量，其初始值设为常量 stop。

## 结构体、联合体和位域

使用 struct 将相关的数据项组合在一起，并通过名称引用该组合。例如，用于保存队列变量的结构声明可能如下所示：

/* Declare a structure */
struct QUEUE
{
    int count;    /* Number of items in queue */
    int front;    /* Index of first item in queue */
    int rear;     /* Index of last item in queue */
    int elemsize; /* Size of each element of data */
    int maxsize;  /* Maximum capacity of queue */
    char *data;   /* Pointer to queued data */
};

/* Define two queues */
struct QUEUE rcv_q, xmit_q;

QUEUE 结构内部的元素称为其成员。你可以使用成员选择运算符（.）访问这些成员。例如，rcv_q.count 指的是 rcv_q 结构的 count 成员。

union 类似于 struct，但与 struct 将相关数据项组合在一起不同，union 为多个数据项分配存储空间，使其从同一位置开始。因此，union 的所有成员共享相同的存储位置。你可以使用 union 以不同的方式查看相同的数据项。假设你使用的是支持 4 字节 long 数字的编译器，并且想要访问单个 long 整数的 4 个单独字节。以下 union 让你能够实现这一点：

```c
union
{
    long file_type;
    char bytes[4];
} header_id;
```

使用此定义，header_id.file_type 指的是 long 整数，而 header_id.bytes[0] 是该 long 整数的第一个字节。

## 数组

数组是一组一个或多个相同的数据项。你可以声明任何类型的数据的数组，包括结构体和由 typedef 定义的类型。例如，要定义一个包含 80 个字符的数组，你可以编写如下内容：

```c
char string[80];
```

string 数组中的字符占据连续的存储位置，从位置 0 开始。因此，在此示例中，string[0] 指的是该数组中的第一个字符，而 string[79] 指的是最后一个字符。你可以类似地定义其他数据类型和结构体的数组：

```c
struct Customer   /* Declare a structure */
{
 int id;
 char first_name[40];
 char last_name[40];
};
struct Customer customers[100]; /* Define array of structures */
int index[64];   /* An array of 64 integers */
```

你也可以定义多维数组。例如，要表示一个 80 列乘 25 行的文本显示屏，你可以使用二维数组如下：

```c
unsigned char text_screen[25][80];
```

text_screen 的每个项都是一个包含 80 个 unsigned char 的数组，而 text_screen 包含 25 个这样的数组。换句话说，二维数组是通过在内存中按行顺序排列来存储的。你可以使用表达式 text_screen[0][0] 引用第一行中的第一个字符，并使用 text_screen[24][79] 引用显示屏最后一行的最后一个字符。更高维度的数组以类似方式定义：

```c
float coords[3][2][5];
```

此示例将 coords 定义为包含三个数据项的三维数组：每个项都是一个包含两个数组的数组，每个数组又是一个包含五个 float 变量的数组。因此，你将多维数组解释为“数组的数组”。

## 指针

指针是一个变量，可以保存除位域之外任何类型数据的地址。例如，如果 p_i 是指向整数变量的指针，你可以按如下方式定义和使用它：

```c
/* Define an int pointer and an integer */
int *p_i, count;

/* Set pointer to the address of the integer "count" */
p_i = &count;
```

在这种情况下，编译器将为 int 变量 count 和指向整数的指针 p_i 分配存储空间。表示指针所需的字节数取决于底层系统的寻址方案。



![](img/a7eec43a54473e95dc5ea333fecf1bd7_774_0.png)

不要在指针包含有效对象的地址之前使用指针。

示例显示 p_i 使用 & 运算符初始化为整数变量 count 的地址，该运算符提供变量的地址。p_i 初始化后，你可以使用表达式 *p_i 来引用 count 的值，其读作“地址在 p_i 中的对象的内容。”

指针在许多情况下很有用；其中一个重要用途是动态内存分配。标准 C 库包含 malloc 和 calloc 等函数，可用于为对象数组分配存储空间。分配内存后，这些函数会返回内存块的起始地址。由于该地址是访问该内存的唯一方式，因此必须将其存储在能够保存地址的变量中——即指针。

假设你为 50 个整数的数组分配了内存并将返回的地址保存在 p_i 中。现在你可以将这块内存视为名为 p_i 的 50 个整数的数组。因此，你可以将数组中的最后一个元素引用为 p_i[49]，其等价于 *(p_i + 49)。类似地，C 将数组名视为指向数组第一个元素的指针。数组名与指针变量之间的区别在于，数组名是一个常量，无需显式存储来保存数组第一个元素的地址。另一方面，指针是一个实际的存储位置，能够保存任何数据的地址。

除了存储动态分配内存的地址外，指针还常常用作函数的参数。当调用 C 函数时，其所有参数都是按值传递的——也就是说，函数获取每个参数的副本，而不是函数调用参数列表中出现的原始变量。因此，C 函数无法更改其参数的值。指针提供了一种解决办法。要在函数中更改变量的值，可以传递指向该变量的指针；函数可以通过指针更改该值。

## 类型定义

通过 typedef 关键字，C 为你提供了一种方便的方式为现有数据类型分配新名称。你可以使用 typedef 设施为特定应用程序中使用的数据类型赋予有意义的名称。例如，图形应用程序可能会按如下方式声明名为 Point 的数据类型：

```c
/* Declare a Point data type */
typedef struct Point
{
    short x;
    short y;
} Point;
/* Declare PointPtr to be pointer to Point types */
typedef Point *PointPtr;
/* Define some instances of these types
* and initialize them */
Point a = {0, 0};
PointPtr p_a = &a;
```

如 Point 和 PointPtr 类型所示，你可以使用 typedef 方便地声明复杂数据类型。

## 类型限定符：const 和 volatile

两个类型限定符 const 和 volatile 在声明中这样工作：

- 声明中的 const 限定符告诉编译器特定数据对象不得由程序修改。这意味着编译器不得生成可能更改该数据项存储位置内容的代码。
- volatile 限定符指定变量的值可能因超出程序控制的因素而改变。

你可以在单个数据项上同时使用 const 和 volatile 关键字，表示该项不得由你的程序修改，但可能被其他进程更改。const 和 volatile 关键字始终限定其右侧紧跟的项。const 和 volatile 限定符提供的信息旨在帮助编译器优化其生成的代码。例如，假设变量 block_size 按如下方式声明并初始化：

```
const int block_size = 512;
```

在这种情况下，编译器无需生成从内存加载 block_size 值的代码。相反，它可以在程序中使用 block_size 的任何地方使用值 512。现在假设你在声明中添加了 volatile 并将声明更改为：

```
volatile const int block_size = 512;
```

这表示 block_size 的内容可能被某个外部进程更改。因此，编译器无法优化掉对 block_size 的任何引用。当引用 I/O 端口或视频内存时，你可能需要使用此类声明，因为这些位置可能因超出程序控制的因素而改变。

## 表达式

一个 *表达式* 是变量、函数调用和运算符的组合，结果为单个值。例如，这里有一个表达式，其值是存储 *空终止字符串* `str` 所需的字节数（即末尾有一个零字节的 `char` 数据类型数组）：

```
(strlen(str) * sizeof(char) + 1)
```

该表达式涉及函数调用——`strlen(str)`——以及乘法 (*)、加法 (+) 和 `sizeof` 运算符。

C 有大量运算符，它们是表达式的重要组成部分。表 2-2 提供了 C 运算符的摘要。

表 2-2 C 运算符摘要

| 运算符名称 | 语法 | 结果 |
|---|---|---|
| *算术运算符* | | |
| 加法 | x+y | 将 x 和 y 相加。 |
| 减法 | x - y | 从 x 中减去 y。 |
| 乘法 | x*y | 将 x 和 y 相乘。 |
| 除法 | x / y | 将 x 除以 y。 |
| 余数 | x%y | 计算 x 除以 y 的余数。 |
| 前置递增 | ++x | 使用前递增 x。 |
| 后置递增 | x++ | 使用后递增 x。 |
| 前置递减 | --x | 使用前递减 x。 |
| 后置递减 | x-- | 使用后递减 x。 |
| 负号 | -x | 取 x 值的负值。 |
| 正号 | +x | 保持 x 的值不变。 |
| *关系和逻辑运算符* | | |
| 大于 | x>y | 如果 x 大于 y，则值为 1；否则值为 0。 |
| 大于或等于 | x>=y | 如果 x 大于或等于 y，则值为 1；否则值为 0。 |
| 小于 | x<y | 如果 y 大于 x，则值为 1；否则值为 0。 |
| 小于或等于 | x<=y | 如果 y 大于或等于 x，则值为 1；否则值为 0。 |
| 等于 | x == y | 如果 x 等于 y，则值为 1；否则值为 0。 |
| 不等于 | x != y | 如果 x 和 y 不相等，则值为 1；否则值为 0。 |
| 逻辑非 | ! x | 如果 x 为 0，则值为 1；否则值为 0。 |
| 逻辑与 | x && y | 如果 x 或 y 为 0，则值为 0。 |
| 逻辑或 | x || y | 如果 x 和 y 均为 0，则值为 0。 |
| 赋值运算符 | | |
| 赋值 | x = y | 将 y 的值放入 x。 |
| 复合赋值 | x O = y | 等价于 x = x O y，其中 O 是以下运算符之一：+, -, *, /, %, <<, >>, &, ^, 或 |。 |
| 数据访问和大小运算符 | | |
| 下标 | x[ y ] | 选择数组 x 的第 y 个元素。 |
| 成员选择 | x . y | 选择结构（或联合）x 的成员 y。 |
| 成员选择 | x -> y | 从以 x 为地址的结构或联合中选择名为 y 的成员。 |
| 间接 | * x | 地址为 x 的位置的内容。 |
| 地址 | & x | 名称为 x 的数据对象的地址。 |
| 大小 | sizeof( x ) | 名称为 x 的数据对象的大小（以字节为单位）。 |
| 位运算符 | | |
| 位非 | ~ x | 将所有 1 改为 0，0 改为 1。 |
| 位与 | x & y | 结果是 x 和 y 的按位与。 |
| 位或 | x \| y | 结果是 x 和 y 的按位或。 |
| 位异或 | x ^ y | 结果在 x 和 y 的对应位不同的位置包含 1。 |
| 左移 | x << y | 将 x 的位向左移动 y 个位位置。用 0 填充空出的位位置。 |
| 右移 | x >> y | 将 x 的位向右移动 y 个位位置。用 0 填充空出的位位置。 |
| *杂项运算符* | | |
| 函数调用 | x(y) | 结果是函数 x 返回的值（如果有），该函数以 y 作为参数被调用。 |
| 类型转换 | (type)x | 将 x 的值转换为括号中指定的类型。 |
| 条件 | z?x:y | 如果 z 不为 0，则求值 x；否则求值 y。 |
| 逗号 | x,y | 先求值 x，然后求值 y。 |

## 运算符优先级

典型的 C 表达式由多个操作数和运算符组成。在编写复杂表达式时，你必须注意编译器评估运算符的顺序。例如，假设程序使用如下定义的指向整数的指针数组：

```
typedef int *IntPtr;/* Use typedef to simplify declarations*/
IntPtr iptr[10];   /* An array of 10 pointers to int */
```

现在假设你遇到表达式 *iptr[4]。它是指 iptr[4] 中地址的 int 的值，还是指 iptr 地址位置的第五个元素？你真正需要知道的是编译器是否会先评估下标运算符 ([] ) 再评估间接运算符 (*)——还是反过来？要回答此类问题，你需要知道优先级——程序应用运算符的顺序。

表 2-3 总结了 C 的优先级规则。表格按优先级递减的顺序显示运算符。优先级最高的运算符——最先应用的运算符——显示在最前面。表格还显示了结合性——同一级别运算符的求值顺序。

表 2-3 C 运算符的优先级和结合性

| 运算符组 | 运算符名称 | 表示法 | 结合性 |
|---|---|---|---|
| 后缀 | 下标 | x[y] | 从左到右 |
| | 函数调用 | x(y) | |
| | 成员选择 | x.y | |
| | 成员选择 | x->y | |



## 表 2-3（续）

| 操作符组 | 操作符名称 | 表示法 | 结合性 |
|---|---|---|---|
| 一元 | 后自增 | x++ | 从右到左 |
| 一元 | 后自减 | x-- |  |
| 一元 | 前自增 | ++x |  |
| 一元 | 前自减 | --x |  |
| 一元 | 取地址 | &x |  |
| 一元 | 间接寻址 | *x |  |
| 一元 | 正号 | +x |  |
| 一元 | 负号 | -x |  |
| 一元 | 按位非 | ~x |  |
| 一元 | 逻辑非 | !x |  |
| 一元 | sizeof | sizeof x |  |
| 一元 | 类型转换 | (type)x |  |
| 乘法 | 乘法 | x*y | 从左到右 |
| 乘法 | 除法 | x/y |  |
| 乘法 | 取余 | x%y |  |
| 加法 | 加 | x+y | 从左到右 |
| 加法 | 减 | x-y |  |
| 移位 | 左移 | x<<y | 从左到右 |
| 移位 | 右移 | x>>y |  |
| 关系 | 大于 | x>y | 从左到右 |
| 关系 | 大于等于 | x>=y |  |
| 关系 | 小于 | x<y |  |
| 关系 | 小于等于 | x<=y |  |
| 相等 | 等于 | x==y | 从左到右 |
| 相等 | 不等于 | x!=y |  |
| 按位 | 按位与 | x&y | 从左到右 |
| 按位 | 按位异或 | x^y |  |
| 按位 | 按位或 | x|y |  |
| 逻辑 | 逻辑与 | x&&y | 从左到右 |
| 逻辑 | 逻辑或 | x||y |  |
| 条件 | 条件运算符 | z?x:y | 从右到左 |
| 赋值 | 赋值 | x=y | 从右到左 |
| 赋值 | 乘法赋值 | x *= y |  |
| 赋值 | 除法赋值 | x /= y |  |
| 赋值 | 取余赋值 | x %= y |  |
|  | 加法赋值 | x += y |  |
|  | 减法赋值 | x -= y |  |
|  | 左移赋值 | x <<= y |  |
|  | 右移赋值 | x >>= y |  |
|  | 按位与赋值 | x &= y |  |
|  | 按位异或赋值 | x ^= y |  |
|  | 按位或赋值 | x |= y |  |
| 逗号 | 逗号 | x , y | 从左到右 |

回到解释 *iptr[4] 的问题，快速查看表 2-3 可知 [] 运算符的优先级高于 * 运算符。因此，当编译器处理表达式 *iptr[4] 时，它首先计算 iptr[4]，然后应用间接运算符，从而得到 iptr[4] 中地址的 int 值。

## 语句

你使用语句来表示 C 函数将执行的操作并控制 C 程序中的执行流程。语句由关键字、表达式和其他语句组成。每个语句以分号（;）结束。

特殊类型的语句——复合语句——是一组用一对大括号（{ ... }）括起来的语句。函数的体是一个复合语句。此类复合语句（也称为块）可以包含局部变量。

在以下按字母顺序排列的部分中，我简要描述了 C 中可用的语句类型。

### break 语句

你使用 break 语句跳到最内层的 do、for、switch 或 while 语句之后的语句。它也用于从 switch 语句中退出。以下示例使用 break 退出 for 循环：

```c
for(i = 0; i < ncommands; i++)
{
    if(strcmp(input, commands[i]) == 0) break;
}
```

### case 语句

case 语句在 switch 语句中标记标签。以下是一个示例（此处 interrupt_id 是一个整数变量）：

```c
switch (interrupt_id)
{
    case XMIT_RDY:
        transmit();
        break;
    case RCV_RDY:
        receive();
        break;
}
```

### 复合语句或块

复合语句或块是一组声明后跟语句，全部用一对大括号（{ ... }）括起来。典型的复合语句是函数的体以及 if 语句后面的代码块。在以下示例中，大括号内出现的所有内容——声明和语句——构成一个复合语句：

```c
if(theEvent.xexpose.count == 0)
{
    int i;
    /* Clear the window and draw the figures
     * in the "figures" array
     */
    XClearWindow(theDisplay, dWin);
    if(numfigures > 0)
        for(i=0; i<numfigures; i++)
            draw_figure(theDisplay, dWin, theGC, i);
}
```

### continue 语句

continue 语句开始其所在的最内层 do、for 或 while 语句的下一次迭代。当你想跳过循环的执行时，可以使用 continue。例如，要将 1 到 10 的数字相加，但排除 5，可以使用一个在循环索引（i）为 5 时跳过循环体的 for 循环：

```c
for(i=0, sum=0; i <= 10; i++)
{
    if(i == 5) continue;  /* Exclude 5 */
    sum += i;
}
```

### default 标签

你使用 default 作为 switch 语句中的标签来标记当没有任何 case 标签匹配 switch 表达式时将执行的代码。

### do 语句

do 语句与 while 结合形成具有以下结构的迭代循环：

```
do
  statement
  while(expression);
```

其中 statement（通常是复合语句）执行直到 while 语句中的表达式求值为 0。表达式在每次执行语句后求值——因此 do-while 块至少执行一次。例如，要将 1 到 10 的数字相加，可以使用以下 do 语句：

```c
sum = 0;
do
{
    sum += i;
    i++;
}
while(i <= 10);
```

### 表达式语句

表达式语句根据其副作用进行求值。表达式语句的典型用途包括调用函数、递增变量以及为变量赋值。以下是一些示例：

```c
printf("Hello, World!\n");
i++;
num_bytes = length * sizeof(char);
```

### for 语句

使用 for 语句执行语句任意次数（该次数基于表达式的值）。语法如下：

```
for (expr_1; expr_2; expr_3) statement
```

其中 expr_1 在循环开始时求值一次，并且语句执行直到表达式 expr_2 求值为 0。第三个表达式 expr_3 在每次执行语句后求值。三个表达式都是可选的，如果省略 expr_2，则其值假定为 1。以下示例使用 for 循环将 1 到 10 的数字相加：

```c
for(i=0, sum=0; i <= 10; sum += i, i++);
```

在此示例中，实际的加法工作在第三个表达式中完成，并且由 for 循环控制的语句是一个空语句（单个 ;）。

### goto 语句

goto 语句将控制转移到语句标签。以下示例提示用户输入一个值，如果该值不可接受则重复请求：

```c
ReEnter;
printf("Enter offset: ");
scanf("%d", &offset);
if(offset < 0 || offset > MAX_OFFSET)
{
    printf("Bad offset: %d Please reenter:\n", offset);
    goto ReEnter;
}
```

### if 语句

你可以使用 if 语句测试一个表达式，并且仅当表达式不为零时执行语句。if 语句采用以下形式：

```
if ( expression ) statement
```

if 之后的语句仅在括号中的表达式求值为非零值时执行。该语句通常是复合语句。以下是一个示例：

```c
if(mem_left < threshold)
{
    Message("Low on memory! Close some windows.\n");
}
```

### if-else 语句

if-else 语句是 if 语句与 else 子句结合的一种形式。语句的语法为

```
if ( expression )
    statement_1
else
    statement_2
```

其中如果括号内的表达式不为零，则执行 statement_1。否则，执行 statement_2。以下示例使用 if 和 else 选择两个变量中较小的一个：

```c
if ( a <= b)
    smaller = a;
else
    smaller = b;
```

### 空语句

空语句由单个分号表示，不执行任何操作。当所有处理都在循环表达式中完成而不是在循环体中完成时，你在循环中使用空语句。例如，要定位标记字符串末尾的零字节，可以使用以下语句：

```c
char str[80] = "Test";
int i;

for (i=0; str[i] != '\0'; i++)
    ; /* Null statement */
```

### return 语句

return 语句停止执行当前函数并将控制返回给调用函数。语法是

```
return expression;
```

其中表达式的值作为函数的值返回。对于不返回值 的函数，使用以下方式不带表达式的 return 语句：

```
return;
```

### switch 语句

switch 语句根据表达式的值执行多分支。它具有以下语法：

```
switch (expression)
{
    case value1:
        statement_1
        break;
    case value2:

```
statement_2
break;
.
.
default:
    statement_default
}
```

如果 switch 测试的表达式求值为 value1，则执行 statement_1。如果表达式等于 value2，则执行 statement_2。将值与每个 case 标签进行比较，并执行与匹配标签对应的语句。如果值与任何 case 标签都不匹配，则执行 default 标签后面的块 statement_default。每个语句都以 break 语句结束，将一个 case 标签的代码与另一个 case 标签的代码分隔开。以下是根据名为 command 的整数变量的值调用不同例程的 switch 语句：

```
switch (command)
{
    case 'q':
        quit_app();
    case 'c':
        connect();
        break;
    case 's':
        set_params();
        break;
    case '?':
    case 'H':
        print_help();
        break;
    default:
        printf("Unknown command!\n");
}
```

## while 语句

while 语句用于以下形式

```
while (expression) statement
```

其中语句执行直到表达式求值为 0。while 语句在每次执行语句之前评估表达式。因此，while 循环执行语句零次或多次。以下是用于将一个数组复制到另一个数组的 while 语句：

```
i = length;
while (i >= 0) /* Copy one array to another */
{
    array2[i] = array1[i];
    i--;
}
```

## 函数

函数是一组声明和语句。因此，函数是 C 程序的构建块。每个 C 程序至少有一个函数——main 函数，C 程序的执行从这里开始。C 库主要包含函数，尽管其中也包含相当多的宏。

## 函数原型

在 C 中，你必须在使用函数之前声明它。函数声明告诉编译器函数返回的值的类型以及它接受的参数的数量和类型。将函数声明为完整的函数原型，显示返回类型以及参数列表。C 库中的 calloc 函数返回一个 void 指针并接受两个参数，每个参数的类型都是 size_t，这是一种无符号整数类型，其大小足以容纳 sizeof 运算符的值。因此 calloc 的函数原型如下：

```
void *calloc(size_t, size_t);
```

该原型显示了参数列表中每个参数的类型。你也可以为每个参数包含一个标识符。在这种情况下，你将按如下方式编写原型：

```
void *calloc(size_t num_elements, size_t elem_size);
```

这里原型看起来与函数定义的第一行完全一样，只是你没有定义函数，而是在行尾加上分号结束。参数使用合适的名称时，这种原型的形式可以提供大量关于函数使用的信息。例如，只看一下 calloc 的原型就应该能告诉你它的第一个参数是要分配的元素数量，第二个参数是每个元素的大小。

调用函数时可能犯的错误，例如传递错误数量的参数（当函数接受固定数量的参数时）或向函数传递错误类型的参数。

## void 类型

当一个函数既不返回任何内容也不接受任何参数时该怎么办？为处理这些情况，C 提供了 void 类型，它可用于声明不返回任何内容的函数以及描述可以指向任何类型数据的指针。例如，你可以使用 void 返回类型声明一个不返回任何内容的函数，如 exit：

```
void exit(int status);
```

另一方面，如果一个函数不接受任何形式参数，其参数列表由 void 表示：

```
FILE *tmpfile(void);
```

void 指针对于处理内存块的函数很有用。例如，当你从内存分配例程 malloc 请求一定数量的字节时，你可以使用这些位置存储适合该空间的任何数据。在这种情况下，已分配内存块的第一个位置的地址作为 void 指针返回。因此，malloc 的原型写成如下：

```
void *malloc(size_t numbytes);
```

## 具有可变数量参数的函数

如果一个函数接受可变数量的参数，你可以使用省略号 (...) 代替参数列表来表示这一点；但是，你必须在省略号之前提供至少一个参数。stdio.h 头文件中定义的 printf 系列函数就是此类函数的良好示例。这些函数的原型如下：

```
int fprintf(FILE *stream, const char *format, ...);
int printf(const char *format, ...);
int sprintf(char *buffer, const char *format, ...);
```

## C 库

ANSI 和 ISO 对 C 的标准定义了 C 的所有方面——语言、预处理器和库。库中函数的原型以及所有必要的数据结构和预处理器常量都在一组标准头文件中定义。表 2-4 列出了标准头文件，包括其内容摘要。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_788_0.png)

如果你要在 C 中编写应用程序，你必须熟悉许多标准库，因为 C 的大部分编程能力都在于此。如果你正在编写图形应用程序，你还必须学习其他库，例如 The GIMP 工具包。

## 表 2-4 C 中的标准头文件

| 头文件 | 用途 |
|---|---|
| `<assert.h>` | 定义 `assert` 宏。用于程序诊断。 |
| `<ctype.h>` | 声明用于分类和转换字符的函数。 |
| `<errno.h>` | 定义错误条件的宏、`EDOM` 和 `ERANGE`，以及整数变量 `errno`，库函数在其中返回错误代码。 |
| `<float.h>` | 定义可存储在浮点类型中的值的范围。 |
| `<iso646.h>` | 定义了一些宏，在用非英语语言编写 C 程序时很有帮助，这些语言可能将字符组合如 `&` 和 `~` 用于其他目的。 |
| `<limits.h>` | 定义所有整数数据类型的限制值。 |
| `<locale.h>` | 声明 `lconv` 结构以及使 C 程序适应特定区域设置所需的函数。 |
| `<math.h>` | 声明常见的数学函数和 `HUGE_VAL` 宏。 |
| `<setjmp.h>` | 定义 `setjmp` 和 `longjmp` 函数，可在不依赖正常函数调用和返回的情况下将控制从一个函数转移到另一个函数。也定义了 `setjmp` 和 `longjmp` 使用的 `jmp_buf` 数据类型。 |
| `<signal.h>` | 定义处理异常条件所需的符号和例程。 |
| `<stdarg.h>` | 定义宏，提供对接受可变数量参数的函数中未命名参数的访问。 |
| `<stddef.h>` | 定义标准数据类型 `ptrdiff_t`、`size_t`、`wchar_t`；符号 `NULL`；以及宏 `offsetof`。 |
| `<stdio.h>` | 声明输入和输出操作所需的函数和数据类型。定义诸如 `BUFSIZ`、`EOF`、`SEEK_CUR`、`SEEK_END` 和 `SEEK_SET` 之类的宏。 |
| `<stdlib.h>` | 声明许多实用函数，如字符串转换例程、随机数生成器、内存分配例程和进程控制例程（如 `abort`、`exit` 和 `system`）。 |
| `<string.h>` | 声明字符串操作例程，如 `strcmp` 和 `strcpy`。 |

### 表 2-4（续）

| 头文件 | 用途 |
|---|---|
| `<time.h>` | 定义数据类型并声明操作时间的函数。定义类型 `clock_t` 和 `time_t` 以及 tm 数据结构。 |
| `<wchar.h>` | 定义数据类型并声明用于处理宽字符数据类型（`wchar_t`）的函数。 |
| `<wctype.h>` | 定义数据类型并声明用于分类和转换宽字符数据类型（`wchar_t`）的函数。 |

## Red Hat Linux 应用中的共享库

大多数 Red Hat Linux 程序使用共享库。至少，大多数 C 程序使用 C 共享库 `libc.so.X`，其中 X 是版本号。使用共享库是可取的，因为许多可执行程序可以共享同一个共享库——你只需要将一个共享库副本加载到内存中即可。此外，动态链接（其中程序在运行时加载代码模块并与之链接）变得越来越流行，因为它使应用程序能够仅在需要时加载代码块，从而减少应用程序的内存需求。

当程序使用一个或多个共享库时，你需要程序的可执行文件以及所有共享库才能运行程序。换句话说，如果系统上没有所有共享库，你的程序将无法运行。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_789_0.png)

如果你销售使用共享库的应用程序，请确保所有必要的共享库随软件一起分发。

共享库的主题对 Red Hat Linux 程序员来说很有兴趣，因为使用共享库可以减小可执行文件的大小。在本节中，我简要描述了如何在示例程序中创建和使用共享库。

### 检查程序使用的共享库

使用 `ldd` 实用程序确定可执行程序需要的共享库。键入以下 `ldd` 命令以查看程序使用的共享库（该程序由 GCC 存储在默认文件名为 `a.out` 的文件中）：

```
ldd a.out
```

以下是 ldd 对一个典型 C 程序的报告：

```
libc.so.6 => /lib/tls/libc.so.6 (0x42000000)
/lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x40000000)
```

更复杂的程序，例如 The GIMP（类似 Adobe Photoshop 的程序）会使用更多共享库。要查看其共享库需求，请键入以下命令：

```
ldd /usr/bin/gimp
```

以下是我在 Red Hat Linux 系统上显示的列表：

```
libgtk-1.2.so.0 => /usr/lib/libgtk-1.2.so.0 (0x40025000)
libgdk-1.2.so.0 => /usr/lib/libgdk-1.2.so.0 (0x4016e000)
libgmodule-1.2.so.0 => /usr/lib/libgmodule-1.2.so.0 (0x401a6000)
libglib-1.2.so.0 => /usr/lib/libglib-1.2.so.0 (0x401a9000)
libdl.so.2 => /lib/libdl.so.2 (0x400ce000)
libX11.so.6 => /usr/X11R6/lib/libX11.so.6 (0x401d1000)
libXext.so.6 => /usr/X11R6/lib/libXext.so.6 (0x401d9000)
libX11.so.6 => /usr/X11R6/lib/libX11.so.6 (0x401e8000)
libm.so.6 => /lib/libm.so.6 (0x402c7000)
libc.so.6 => /lib/libc.so.6 (0x402e8000)
/lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x40000000)
```

在这种情况下，程序使用了相当多的共享库，包括 X11 库（libX11.so.6）、GIMP 工具包（libgtk-1.2.so.0）、通用绘图工具包（GDK）库（libgdk-1.2.so.0）、数学库（libm.so.6）以及 C 库（libc.so.6）。

几乎任何 Red Hat Linux 应用程序都需要共享库才能运行。

## 创建共享库

为自己的应用程序创建共享库相当简单。假设你想以共享库的形式实现一个对象（把对象想象成一堆代码和数据）。共享库中的一组函数代表对象的接口。要使用该对象，你需要加载其共享库并调用其接口函数。（我在下一节中向你展示如何做到这一点。）

以下是此简单对象的 C 源代码，以共享库的形式实现（你也可以称之为动态链接库）——将其保存到名为 dynobj.c 的文件中：

/*---------------------------------------------*/
/* File: dynobj.c */
/* Demonstrate use of dynamic linking.
*
* Pretend this is an object that can be created by calling
* init and destroyed by calling destroy.
*/
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

/* Data structure for this object */
typedef struct OBJDATA
{
    char *name;
    int version;
} OBJDATA;

/*-------------------------------------------*/
/* i n i t
*
* Initialize object (allocate storage).
*/
void* init(char *name)
{
    OBJDATA *data = (OBJDATA*)calloc(1, sizeof(OBJDATA));
    if(name)
        data->name = malloc(strlen(name)+1);
        strcpy(data->name, name);

    printf("Created: %s\n", name);

    return data;
}
/*-------------------------------------------*/
/* s h o w
*
* Show the object.
*/
void show(void *data)
{
    OBJDATA *d = (OBJDATA*)data;
    printf("show: %s\n", d->name);
}
/*-------------------------------------------*/
/* d e s t r o y
*
* Destroy the object (free all storage).
*/
void destroy(void *data)
{
    OBJDATA *d = (OBJDATA*)data;
    if(d)
{
    if(d->name)
    {
        printf("Destroying: %s\n", d->name);
        free(d->name);
    }
    free(d);
}
```

该对象提供三个接口函数：

- ♦ init 用于分配必要的存储空间并初始化对象
- ♦ show 用于显示对象（在这里，它只是打印一条消息）
- ♦ destroy 用于释放存储空间

要构建名为 libdobj.so 的共享库，请按以下步骤操作：

- 1. 使用 -fPIC 标志编译所有源文件。在本例中，使用以下命令编译 dynobj.c 文件：
      ```
      gcc -fPIC -c dynobj.c
      ```
- 2. 使用 -shared 标志将对象链接成共享库，并为链接器提供适当的标志。要创建名为 libdobj.so.1 的共享库，请使用以下命令：
      ```
      gcc -shared -Wl,-soname,libdobj.so.1 -o libdobj.so.1.0
      dynobj.o
      ```
- 3. 设置一系列符号链接，以便使用共享库的程序可以用标准名称引用它。
      对于示例库，标准名称为 libdobj.so，符号链接通过以下命令设置：
      ```
      ln -sf libdobj.so.1.0 libdobj.so.1
      ln -sf libdobj.so.1 libdobj.so
      ```
- 4. 当你测试共享库时，使用以下命令定义并导出 LD_LIBRARY_PATH 环境变量：
      ```
      export LD_LIBRARY_PATH=`pwd`:$LD_LIBRARY_PATH
      ```

在你测试共享库并确信库能正常工作后，将其复制到标准位置，例如 /usr/local/lib，并运行 ldconfig 实用程序以更新 libdobj.so.1 与 libdobj.so.1.0 之间的链接。

这些是你用于为所有人安装共享库的命令（你必须以 root 身份执行这些步骤）：

```
cp libdobj.so.1.0 /usr/local/lib
/sbin/ldconfig
cd /usr/local/lib
ln -s libdobj.so.1 libdobj.so
```

## 动态加载共享库

在程序中加载共享库并使用其中的函数非常简单。在本节中，我演示了如何做到这一点。头文件 <dlfcn.h>（这是 Red Hat Linux 中的标准头文件）声明了用于加载和使用共享库的函数。文件 dlfcn.h 中声明了四个用于动态加载的函数：

- ♦ void *dlopen(const char *filename, int flag); — 加载 filename 指定的共享库并返回库的句柄。flag 可以是 RTLD_LAZY（在库代码执行时解析未定义符号），或 RTLD_NOW（在 dlopen 返回之前解析所有未定义符号，如果所有符号未定义则失败）。如果 dlopen 失败，则返回 NULL。
- ♦ const char *dlerror(void); — 如果 dlopen 失败，调用 dlerror 以获取包含错误描述的字符串。
- ♦ void *dlsym(void *handle, char *symbol); — 返回由 handle（由 dlopen 返回）标识的共享库中指定符号（函数名）的地址。
- ♦ int dlclose(void *handle); — 如果没有其他人使用，则卸载共享库。

当你使用这些函数中的任何一个时，使用以下预处理器指令包含头文件 dlfcn.h：

```
#include <dlfcn.h>
```

最后，这里有一个简单的测试程序——dltest.c——它展示了如何加载和使用你在上一节中创建的共享库 libdobj.so 中定义的对象：

/*------------------------------------------------------------*/
/* File: dltest.c
 *
 * Test dynamic linking.
 *
 */
#include <dlfcn.h>  /* For the dynamic loading functions */
#include <stdio.h>

int main(void)
{
    void *dlobj;
    void *(*init_call)(char *name);
    void (*show_call)(void *data);
    void (*destroy_call)(void *data);

    /* Open the shared library and set up the function pointers */
    if(dlobj = dlopen("libdobj.so",RTLD_LAZY))
    {
        void *data;

        init_call= dlsym(dlobj,"init");
        show_call= dlsym(dlobj,"show");
        destroy_call= dlsym(dlobj,"destroy");

        /* Call the object interfaces */
        data = (*init_call)("Test Object");
        (*show_call)(data);
        (*destroy_call)(data);
    }
    return 0;
}
```

该程序很简单：它加载共享库，获取库中函数的指针，并通过指针调用函数。

你可以以通常的方式编译和链接此程序，但必须使用 -ldl 选项链接，以便使用 dlfcn.h 中声明的函数。以下是构建程序 dltest 的方法：

```
gcc -o dltest dltest.c -ldl
```

要查看程序运行情况，通过键入以下命令运行 dltest：

```
./dltest
```

它应显示以下输出行：

```
Created: Test Object
show: Test Object
Destroying: Test Object
```

虽然这个示例程序并不令人兴奋，但你现在拥有了一个使用共享库的示例程序。

要了解使用共享库的好处，请返回上一节并在共享库源文件——`dynobj.c`中进行一些更改。例如，你可以在函数中打印其他消息，以便轻松判断是否已进行更改。单独重建共享库。然后再次运行 `dltest`。结果输出应显示你在共享库中所做的更改的效果，这意味着你可以独立于应用程序更新共享库。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_795_0.png)

请注意，共享库的更改可能会影响系统上安装的许多应用程序。因此，在对任何共享库进行更改时要小心。同样，如果有人设法用恶意代码替换共享库，共享库也可能成为安全风险。




### 第 3 章：编写 Shell 脚本

### 本章内容
- 尝试运行简单的 Shell 脚本
- 学习 Shell 脚本编写的基础知识
- 探索 Bash 的内置命令

Red Hat Linux 提供了许多小而专门的命令，以及将这些命令连接起来所需的管道设施。这里所说的*管道设施*，指的是一种机制，即可以将一个命令的输出作为另一个命令的输入。Bash（Bourne Again SHell 的缩写）—— Linux 的默认 Shell —— 通过 I/O 重定向和管道提供了这种管道设施。Bash 还包含诸如 *if* 语句等特性，你可以在特定条件为真时运行命令；以及 *for* 语句，它可以按指定次数重复执行命令。在编写称为*Shell 脚本*的程序时，你可以使用 Bash 的这些特性。

在本章中，我将向你展示如何编写简单的*Shell 脚本*——即存储在文件中的任务导向型 Shell 命令集合。Shell 脚本用于自动化各种任务。例如，当你的 Red Hat Linux 启动时，存储在 */etc* 目录（例如 */etc/init.d*）各个子目录中的许多 Shell 脚本会执行许多初始化任务。

### 尝试简单的 Shell 脚本

如果你不是程序员，可能会对编程感到有些紧张。但 Shell*脚本编写*（或编程）可以非常简单，只需将几条命令存储在一个文件中即可。事实上，你可以拥有一个只包含一条命令的有用 Shell 程序。

例如，在编写本书时，我从 X Window 系统截取了屏幕截图，并在图表中使用了这些截图。我使用了 X 屏幕捕获程序 *xwd* 将屏幕图像存储在 X Window Dump（XWD）格式中。然而，本书的制作团队希望截图是 TIFF 格式的。因此，我使用 Portable Bitmap（PBM）工具包将 XWD 图像转换为 TIFF 格式。为了转换每个文件，我运行了两个程序并删除了一个临时文件，如下所示：

```
xwdtopnm < file.xwd > file.pnm
pnmtotiff < file.pnm > file.tif
rm file.pnm
```

这些命令假设 xwdtopnm 和 pnmtotiff 程序位于 /usr/bin 目录中——这是 PATH 环境变量中列出的目录之一。顺便说一下，xwdtopnm 和 pnmtotiff 是 PBM 工具包中的两个程序。

在将几个 XWD 文件转换为 TIFF 格式后，我对每个文件都输入相同的命令序列感到厌倦，所以我准备了一个名为 totif 的文件，并在其中保存了以下行：

```
#!/bin/sh
xwdtopnm < $1.xwd > $1.pnm
pnmtotiff < $1.pnm > $1.tif
rm $1.pnm
```

然后，我使用以下命令使该文件可执行：

```
chmod +x totif
```

chmod 命令允许你更改文件的权限设置。其中一个设置决定了文件是否可执行。+x 选项表示你希望将文件标记为可执行文件。你必须这样做，因为 Bash 只运行可执行文件。

现在，当我想把文件 figure1.xwd 转换为 figure1.tif 时，只需输入以下命令即可做到：

```
./totif figure1
```

./ 前缀表示 totif 文件位于当前目录——如果 PATH 环境变量包含当前目录，则不需要 ./ 前缀。totif 文件是一个 Shell 脚本（也称为 Shell 程序）。当你使用命令 totif figure1 运行此 Shell 程序时，Shell 会用 figure1 替换每个 $1 的出现。（请注意，$1 指的是用户在执行脚本时所使用的命令中输入的第一个选项。）

Shell 脚本在系统管理员中很受欢迎。如果你是系统管理员，你可以构建一个自定义 Shell 脚本集合，帮助你自动化经常执行的任务。例如，如果某个磁盘似乎快满了，你可能希望找到所有超过一定大小（例如 1MB）且在过去 30 天内未访问过的文件。此外，你可能还想向拥有大文件的所有用户发送电子邮件消息，要求他们归档并清理这些文件。你可以使用 Shell 脚本执行所有这些任务。你可能从以下 find 命令开始以识别大文件：

```
find / -type f -atime +30 -size +100k -exec ls -l {} \; > /tmp/largefiles
```

此命令创建一个名为 /tmp/largefiles 的文件，其中包含关于占用过多空间的旧文件的详细信息。在获取文件列表后，你可以使用其他几个 Linux 命令——例如 sort、cut 和 sed——来准备并发送电子邮件消息给那些拥有需要清理的大文件的用户。手动输入所有这些命令不如将它们放在一个文件中并创建一个 Shell 脚本。简而言之，Shell 脚本的本质就是将 Shell 命令聚集在一个文件中，以便你可以轻松执行重复的系统管理任务。

就像大多数 Linux 命令接受命令行选项一样，Bash 脚本也接受命令行选项。在脚本内部，你可以使用 $1、$2 等来引用这些选项。特殊名称 $0 指的是脚本本身的名称。

这是一个接受参数的典型 Bash 脚本：

```
#!/bin/sh
echo "This script's name is: $0"
echo Argument 1: $1
echo Argument 2: $2
```

第一行运行 /bin/sh 程序，随后处理脚本中的其余行。名称 /bin/sh 传统上指的是 Bourne Shell——第一个 UNIX Shell。在 Red Hat Linux 中，/bin/sh 是 /bin/bash 的一个符号链接，/bin/bash 是 Bash 的可执行程序。

将此简单脚本保存为名为 simple 的文件，并使用以下命令使该文件可执行：

```
chmod +x simple
```

现在按如下方式运行脚本：

```
./simple
```

它会显示以下输出：

```
This script's name is: ./simple
Argument 1:
Argument 2:
```

第一行显示了脚本的名称。因为你没有参数运行了该脚本，所以脚本没有显示参数的值。

现在尝试带有一些参数运行脚本，如下所示：

```
./simple "This is one argument" second-argument third
```

这次脚本显示了更多输出：

```
This script's name is: ./simple
Argument 1: This is one argument
Argument 2: second-argument
```

如输出所示，Shell 将双引号内的整个字符串视为一个参数。否则，Shell 使用空格作为命令行上参数之间的分隔符。

这个示例脚本忽略了第三个参数，因为该脚本设计为仅打印前两个参数。该脚本忽略前两个之后的所有参数。

## 学习 Shell 脚本编写的基础知识

像任何编程语言一样，Bash Shell 支持以下特性：

- 存储值的变量，包括用于访问传递给 Shell 脚本的命令行参数以及其他特殊值的特殊内置变量。
- 评估表达式的能力。
- 允许你对多个 Shell 命令进行循环或有条件地执行某些命令的控制结构。
- 定义可以在脚本中许多地方调用的函数的能力。Bash 还包含许多你可以任何脚本中使用的内置命令。

在接下来的几个小节中，我将通过简单的例子来说明其中的一些编程特性。（我假设你已经在运行 Bash，在这种情况下，你可以在终端窗口的 Shell 提示符处输入这些示例来尝试。）

### 存储数据

你在 Bash 中定义变量的方式与定义环境变量的方式相同。因此，你可以如下定义一个变量：

```
count=12  # 注意不允许嵌入空格
```

要使用变量的值，请在变量名前加一个美元符号（$）。例如，$PATH 是变量 PATH 的值（这是著名的 PATH 环境变量，它列出了 Bash 在尝试定位可执行文件时搜索的所有目录）。要显示变量 count 的值，请使用以下命令：

```
echo $count
```

Bash 有一些特殊变量用于访问命令行参数。在 Shell 脚本中，$0 指的是 Shell 脚本的名称。变量 $1、$2 等指的是命令行参数。变量 $* 将所有命令行参数存储为单个变量，而 $? 包含 Shell 执行的最后一个命令的退出状态。

在 Bash 脚本中，你可以提示用户输入，并使用 read 命令将输入读取到变量中。以下是一个示例：

```
echo -n "Enter value: "
read value
echo "You entered: $value"
```

当此脚本运行时，read value 命令会让 Bash 读取你在键盘上输入的任何内容。

请注意，-n 选项可防止 echo 命令在显示字符串的末尾自动添加新行。

### 调用 Shell 函数

你可以将一组你经常一致使用的 Shell 命令分组到一个函数中，并为其分配一个名称。之后，你可以使用分配给该函数的单个名称来执行那组命令。以下是一个说明 Shell 函数语法的简单脚本：

```
#!/bin/sh

hello() {
    echo -n "Hello, "
    echo $1 $2
}

hello Jane Doe
```

运行此脚本时，它会显示以下输出：

```
Hello, Jane Doe
```

此脚本定义了一个名为 hello 的 Shell 函数。该函数期望有两个参数。在函数体中，这些参数通过 $1 和 $2 引用。函数定义以 hello() 开始——函数的名称，后跟括号。函数体包含在花括号中：{ ... }。在这种情况下，函数体使用 echo 命令显示一行文本。




示例的最后一行展示了如何使用参数调用 shell 函数。在这种情况下，hello 函数被调用时带有两个参数：Jane 和 Doe。hello 函数接收这两个参数并打印出一条内容为 Hello, Jane Doe 的行。

## 控制流程

在 Bash 脚本中，你可以通过使用 if、case、for 和 while 等特殊命令来控制执行流程——即命令执行的顺序。这些控制语句使用命令的退出状态来决定下一步做什么。当任何命令执行时，它会返回一个退出状态——一个表示命令是否成功执行的数值。按照惯例，退出状态为零表示命令执行成功。（是的，你读对了：零表示成功！）非零退出状态表示命令执行出现问题。

例如，假设你想在用 vi 编辑器编辑文件之前先制作文件的备份副本。更重要的是，如果无法制作备份，你希望避免编辑该文件。下面是一个 Bash 脚本，用于处理此任务：

```
#!/bin/sh
if cp "$1" "#$1"
then
    vi "$1"
else
    echo "Failed to create backup copy"
fi
```

此脚本说明了 if-then-else 结构的语法，并展示了 if 命令如何使用 cp 命令的退出状态来确定下一步操作。如果 cp 返回零，脚本将使用 vi 编辑文件；否则，脚本会显示错误消息并退出。顺便说一下，脚本将备份保存在一个文件中，其名称与原文件相同，只是文件名开头添加了一个井号（#）。

![](img/a7eec43a54473e95dc5ea333fec1bd7_801_0.png)

不要忘记终止 if 命令的最后的 fi。忘记 fi 是 Bash 脚本中常见的错误来源。

你可以使用 test 命令来计算任何表达式，并将表达式的值用作命令的退出状态。假设你想要一个仅在文件已存在时才编辑文件的脚本。使用 test，你可以按如下方式编写这样的脚本：

```
#!/bin/sh
if test -f "$1"
then
    vi "$1"
else
    echo "No such file"
fi
```

test 命令的简写形式是将表达式放在方括号（[ ... ]）中。使用这种简写表示法，你可以按如下方式重写前面的脚本：

```
#!/bin/sh
if [ -f "$1" ]
then
    vi "$1"
else
    echo "No such file"
fi
```

注意：方括号的两侧必须有空格。

另一个常见的控制结构是 for 循环。下面的脚本将 1 到 10 的数字相加：

```
#!/bin/sh
sum=0
for i in 1 2 3 4 5 6 7 8 9 10
do
    sum=`expr $sum + $i`
done
echo "Sum = $sum"
```

此示例还说明了使用 expr 命令计算表达式。

case 语句用于根据变量的值执行一组命令。例如，考虑以下脚本，该脚本基于你的 Red Hat Linux 系统中 /etc/init.d/functions 文件中的 confirm() 函数：

```
#!/bin/sh
echo -n "What should I do -- (Y)es/(N)o/(C)ontinue? [Y] "
read answer
case $answer in
y|Y|*)
    echo "YES"
    ;;
c|C)
    echo "CONTINUE"
    ;;
n|N)
    echo "NO"
    ;;
*) echo "UNKNOWN"
;;
esac
```

将此保存到名为 `confirm` 的文件中并输入 `chmod +x confirm` 使其可执行。然后像这样尝试：

```
./confirm
```

当脚本提示你时，输入字符 y、n 或 c 中的一个，然后按 Enter。脚本应显示 YES、NO 或 CONTINUE。例如，当我输入 c（然后按 Enter）时，会发生以下情况：

```
What should I do -- (Y)es/(N)o/(C)ontinue? [Y] c
CONTINUE
```

脚本显示提示并读取你输入的内容。你输入的内容存储在名为 `answer` 的变量中。然后 `case` 语句根据 `answer` 变量的值执行一段代码。例如，当我输入 c 时，将执行以下命令块：

```
c|C)
  echo "CONTINUE"
;;
```

`echo` 命令导致脚本显示 CONTINUE。

从此示例中，你可以看到 `case` 命令的一般语法如下：

```
case $variable in
  value1 | value2)
    command1
    command2
    ...other commands...
  ;;
  value3)
    command3
    command4
    ...other commands...
  ;;
esac
```

本质上，`case` 命令以单词 `case` 开始，以 `esac` 结束。代码的各个块被变量的值包围，其后跟一个右括号并以一对分号 (;;) 终止。

## 探索 Bash 的内置命令

Bash 有超过 50 个内置命令，包括 cd 和 pwd 等常用命令，以及许多其他不常用的命令。你可以在任何 Bash 脚本或 shell 提示符下使用这些内置命令。表 3-1 描述了大多数 Bash 内置命令及其参数。查看完这些信息后，输入 help cmd 以阅读有关特定内置命令的更多信息。例如，要了解有关内置命令 test 的更多信息，请输入以下内容：

```
help test
```

这样将在我的 Red Hat Linux 系统上显示以下信息：

```
test: test [expr]
Exits with a status of 0 (true) or 1 (false) depending on
the evaluation of EXPR. Expressions may be unary or binary. Unary
expressions are often used to examine the status of a file. There
are string operators as well, and numeric comparison operators.

File operators:
-a FILE True if file exists.
-b FILE True if file is block special.
-c FILE True if file is character special.
-d FILE True if file is a directory.
-e FILE True if file exists.
-f FILE True if file exists and is a regular file.
-g FILE True if file is set-group-id.
-h FILE True if file is a symbolic link.
-L FILE True if file is a symbolic link.
-k FILE True if file has its 'sticky' bit set.
-p FILE True if file is a named pipe.
-r FILE True if file is readable by you.
-s FILE True if file exists and is not empty.
-S FILE True if file is a socket.
-t FD True if FD is opened on a terminal.
-u FILE True if the file is set-user-id.
-w FILE True if the file is writable by you.
-x FILE True if the file is executable by you.
-O FILE True if the file is effectively owned by you.
-G FILE True if the file is effectively owned by your group.
(... Lines deleted ...)
```

必要时，help 命令的在线帮助包含大量详细信息。

某些外部程序可能与 Bash 内置命令同名。如果要运行此类外部程序，必须明确指定该程序的完整路径名。否则，Bash 将执行同名的内置命令。

![](img/a7eec43a54473e95dc5ea333fec1bd7_804_0.png)

### 表 3-1 Bash Shell 中内置命令摘要

| 此功能 | 执行以下操作 |
|---|---|
| `. filename [arguments]` | 从指定的文件读取并执行命令，使用可选参数（与 source 命令的工作方式相同）。 |
| `: [arguments]` | 展开参数但不处理它们。 |
| `[ expr ]` | 计算表达式 expr，如果 expr 为真则返回零状态。 |
| `alias [name=value] ...` | 定义别名。 |
| `bg [job]` | 将指定的作业置于后台。如果未指定作业，则将当前执行的命令置于后台。 |
| `bind [-m keymap] [-lvd] [-q name]` | 将键序列绑定到宏。 |
| `break [n]` | 退出 for、while 或 until 循环。如果指定了 n，则退出第 n 个外层循环。 |
| `builtin builtin_command [arguments]` | 执行 shell 内置命令。 |
| `cd [dir]` | 将当前目录更改为 dir。 |
| `command [-pVv] cmd [arg ...]` | 使用指定的参数运行命令 cmd（忽略任何名为 cmd 的 shell 函数）。 |
| `continue [n]` | 开始 for、while 或 until 循环的下一次迭代。如果指定了 n，则开始第 n 个外层循环的下一次迭代。 |
| `declare [-frxi] [name=value]` | 声明具有指定名称的变量，并可选择为其赋值。 |
| `dirs [-l] [-/+n]` | 显示当前记住的目录列表。 |
| `echo [-neE] [arg ...]` | 在标准输出上显示参数。 |
| `enable [-n] [-all] [name ...]` | 启用或禁用指定的内置命令。 |
| `eval [arg ...]` | 连接参数并作为命令执行。 |
| `exec [command [arguments]]` | 用运行指定命令的新进程替换当前 shell 实例。 |
| `exit [n]` | 以状态码 n 退出 shell。 |
| `export [-nf] [name=word] ...` | 定义指定的环境变量并将其导出到未来进程。 |




| 此函数 | 执行以下操作 |
|---|---|
| fc -s [pat=rep] [cmd] | 在将模式 pat 替换为 rep 后重新执行命令。 |
| fg [jobspec] | 将指定的作业置于前台。如果未指定作业，则将最近的作业置于前台。 |
| getopts optstring name [args] | 获取可选参数（在 shell 脚本中调用以从命令行提取参数）。 |
| hash [-r] [name] | 记住指定命令的完整路径名。 |
| help [cmd ...] | 显示指定内置命令的帮助信息。 |
| history [n] | 显示过去的命令，或如果指定数字 n，则显示过去的 n 条命令。 |
| jobs [-lnp] [ jobspec ... ] | 列出当前活动的作业。 |
| kill [-s sigspec \| -sigspec] [pid \| jobspec] ... | 评估每个参数，如果最后一个参数为 0 则返回 1。 |
| let arg [arg ...] | 创建具有指定名称和值的局部变量（用于 shell 函数）。 |
| local [name=value] ... | 退出登录 shell。 |
| logout | 从目录堆栈中删除条目。 |
| popd [+/-n] | 将指定目录添加到目录堆栈顶部。 |
| pushd [dir] | 打印当前工作目录的完整路径名。 |
| pwd | 从标准输入读取一行并解析它。 |
| read [-r] [name ...] | 将指定变量标记为只读，以便以后无法更改这些变量。 |
| readonly [-f] [name ...] | 使用返回值 n 退出 shell 函数。 |
| return [n] | 设置各种标志。 |
| set [-abefhkmnptuvx] [ -o option] [arg ...] | 使第 n+1 个参数成为 $1，第 n+2 个参数成为 $2，以此类推。 |
| shift [n] | 从文件读取并执行命令。 |
| source filename [arguments] | 直到收到 SIGCONT 信号为止停止执行。 |
| suspend [-f] | 评估表达式 expr，如果 expr 为真则返回零。 |
| test expr | 打印从 shell 运行的进程的累计用户时间和系统时间。 |
| times |  |

表 3-1（续）

| 此函数 | 执行以下操作 |
|---|---|
| `trap [-l] [cmd] [sigspec]` | 当收到信号 `sigspec` 时执行 `cmd`。 |
| `type [-all] [-type \| -path] name [name ...]` | 指示 shell 如何解释每个名称。 |
| `ulimit [-SHacdfmstpnuv] [limit]` | 控制 shell 可用的资源。 |
| `umask [-S] [mode]` | 设置文件创建掩码——文件的默认权限。 |
| `unalias [-a] [name ...]` | 取消定义指定的别名。 |
| `unset [-fv] [name ...]` | 删除指定变量的定义。 |
| `wait [n]` | 等待指定进程终止。 |

### 第 4 章：在 Perl 中编程

### 本章内容

- ✓ 编写你的第一个 Perl 程序
- ✓ 获取 Perl 的概览
- ✓ 理解 Perl 包和模块
- ✓ 在 Perl 中使用对象

在编写脚本方面，Perl 语言在系统管理员中非常流行，尤其是在 UNIX 和 Linux 系统上。系统管理员使用 Perl 来自动化例行系统管理任务，例如查找可以归档并删除以释放磁盘空间的旧文件。

Perl 是一种脚本语言，这意味着你不必编译和链接 Perl 脚本（包含 Perl 命令的文本文件）。相反，解释器执行 Perl 脚本。这使得编写和测试 Perl 脚本变得容易，因为你不必经历典型的编辑-编译-链接周期来编写 Perl 程序。

除了编程的简易性之外，Perl 流行的另一个原因是 Perl 可自由分发，并且可在各种计算机系统上使用，包括 Red Hat Linux 以及许多其他系统，如 UNIX、Windows 95/98/NT/2000/XP 和 Apple Macintosh。

在本章中，我向你介绍 Perl 脚本编程。

### 了解 Perl

正式来说，Perl 代表 Practical Extraction Report Language（实用提取报告语言），但 Perl 的创建者 Larry Wall 说人们经常将 Perl 称为 Pathologically Eclectic Rubbish Lister（病态折衷垃圾列表器）。从这些名称可以看出，Perl 最初是为从文本文件中提取信息并生成报告而设计的。

Perl 于 1986 年诞生，最初是由 Larry Wall 创建的系统管理工具。随着时间的推移，Perl 通过不断增加许多新特性和功能而发展。最新版本——Perl 5.8——支持面向对象编程，并允许任何人通过以指定格式添加新模块来扩展 Perl。

Perl 忠实于其作为系统管理工具的起源，多年来一直深受 UNIX 系统管理员的欢迎。最近，当万维网（或简称为 Web）变得流行并出现对通用网关接口（CGI）程序的需求时，Perl 成为那些已熟悉该语言的人的自然选择。Perl 人气最近的飙升主要归功于在 Web 上编写 CGI 程序中使用 Perl。当然，随着人们对 Perl 的关注度提高，他们发现 Perl 的用途远不止 CGI 编程。这反过来又使 Perl 在用户中变得更加流行。

Perl 可在各种计算机系统上使用，因为与 Linux 操作系统一样，Perl 可以自由分发。

如果你熟悉 shell 编程或 C 编程语言，你可以快速掌握 Perl。如果你从未编程过，熟练掌握 Perl 可能需要一段时间。我鼓励你从 Perl 的一小部分功能开始，并忽略你不立即理解的内容。然后，慢慢将 Perl 功能添加到你的技能库中。

### 确定是否已安装 Perl

在继续 Perl 教程之前，请检查你的 Red Hat Linux 系统上是否已安装 perl 程序。输入以下命令：

```
which perl
```

which 命令会告诉你它是否在 PATH 环境变量列出的目录中找到指定的程序。如果已安装 perl，你应该会看到以下输出：

```
/usr/bin/perl
```

如果 which 命令抱怨在当前 PATH 中不存在此类程序，这并不一定意味着你没有安装 perl；它可能只是意味着你没有在 PATH 中包含 /usr/bin 目录。确保 /usr/bin 在 PATH 中；通过输入以下命令进行检查：

```
echo $PATH
```

查看输出是否列出 /usr/bin 目录。如果 /usr/bin 不在 PATH 中，使用以下命令重新定义 PATH：

```
export PATH=$PATH:/usr/bin
```

现在，再次尝试 which perl 命令。如果仍然出现错误，你可能尚未安装 Perl。你可以从随附的 DVD 中安装 Perl，按以下步骤操作：

- 1. 以 **root** 身份登录。
- 2. 将随附的 DVD-ROM 插入 DVD-ROM 驱动器。如果你正在 GNOME 或 KDE 图形环境中工作，DVD-ROM 应该会自动挂载。否则，通过输入以下命令挂载 DVD-ROM：
```
mount /mnt/cdrom
```
- 3. 输入以下命令将目录更改为 Red Hat 软件包的位置：
```
cd /mnt/cdrom/RedHat/RPMS
```
- 4. 输入以下 **rpm**（Red Hat 软件包管理器）命令来安装 Perl：
```
rpm -ivh perl*
```

在系统上安装 Perl 后，输入以下命令查看其版本号：

```
perl -v
```

这是该命令的典型输出：

```
This is perl, v5.8.1 built for i386-linux-thread-multi
(with 1 registered patch, see perl -V for more detail)

Copyright 1987-2003, Larry Wall

Perl may be copied only under the terms of either the Artistic License or the
GNU General Public License, which may be found in the Perl 5 source kit.

Complete documentation for Perl, including FAQ lists, should be found on
this system using "man perl" or "perldoc perl". If you have access to the
Internet, point your browser at http://www.perl.com/, the Perl Home Page.
```

此输出告诉你你拥有 Perl 版本 5.8，补丁级别 1，并且 Perl 的创始人 Larry Wall 拥有版权。（不过请记住，Perl 是在 GNU 通用公共许可证下自由分发的。）

你可以通过将万维网浏览器指向 Comprehensive Perl Archive Network（CPAN）来获取最新版本的 Perl。以下地址会将你连接到离你最近的 CPAN 站点：
http://www.perl.com/CPAN/

![](img/a7eec43a54473e95dc5ea333fecf1bd7_810_0.png)



## 编写你的第一个 Perl 脚本

Perl 具有 C 的许多特性，而且，正如你可能知道的，大多数关于 C 的书籍都以一个在终端上显示 Hello, World! 的示例程序开始。因为 Perl 是一种解释型语言，你可以直接从命令行完成此任务。如果输入

```
perl -e 'print "Hello, World!\n";'
```

Perl 的响应如下：

```
Hello, World!
```

此命令使用 perl 程序的 -e 选项将 Perl 程序作为命令行参数传递给 Perl 解释器。在这种情况下，以下行构成 Perl 程序：

```
print "Hello, World!\n";
```

要将此行转换为 Perl 脚本，只需将该行放在文件中，并以运行 perl 程序的指令开始该文件（就像你在 shell 脚本中放置类似 #!/bin/sh 的行来运行 shell 处理脚本一样）。

要尝试此 Perl 脚本，请按以下步骤操作：

- 1. **使用文本编辑器输入以下行并保存到名为 hello.pl 的文件中：**
  ```
  #!/usr/bin/perl
  # This is a comment.
  print "Hello, World!\n";
  ```
- 2. **使用以下命令使 hello.pl 文件可执行：**
  ```
  chmod +x hello.pl
  ```
- 3. **在 shell 提示符下输入以下内容运行 Perl 脚本：**
  ```
  ./hello.pl
  ```

它应显示以下输出：

```
Hello, World!
```

就这样！你已经编写并尝试了你的第一个 Perl 脚本。

请注意，Perl 脚本的第一行以 #! 开头，后跟 perl 程序的完整路径名。如果脚本的第一行以 #! 开头，shell 只是去掉 #!，将脚本文件名称附加到末尾，并

![](img/a7eec43a54473e95dc5ea333fecf1bd7_811_0.png)

运行脚本。因此，如果脚本文件名为 hello.pl 且第一行为 #!/usr/bin/perl，shell 会执行以下命令：

/usr/bin/perl hello.pl

## 获取 Perl 概览

大多数编程语言，包括 Perl，都具有一些共同特性：

- **变量** 存储不同类型的数据。你可以将每个变量视为数据的占位符——有点像邮箱，有名称和存储数据的空间。变量的内容是其值。
- **表达式** 通过使用运算符组合变量。一个表达式可能会添加多个变量；另一个可能会提取字符串的一部分。
- **语句** 执行某些操作，例如将值赋给变量或打印字符串。
- **流程控制语句** 使语句能够根据某些表达式的值以不同的顺序执行。通常，流程控制语句包括 `for`、`do-while`、`while` 和 `if-then-else` 语句。
- **函数**（也称为 *子程序* 或 *例程*）使你能够将多个语句分组并赋予名称。使用此功能，你可以通过调用代表这些语句的函数来执行同一组语句。通常，编程语言提供一些预定义函数。
- **包** 和 **模块** 使你能够组织一组相关的 Perl 子程序，这些子程序设计为可重用。（模块是在 Perl 5 中引入的。）

在接下来的几个部分中，我将概述 Perl 的这些主要特性并通过简单示例说明这些特性。

## 基本 Perl 语法

Perl 是自由格式的，像 C 一样。对任何关键字的确切位置没有限制。通常，Perl 程序存储在以 .pl 结尾的文件中，但你使用的文件名没有限制。

与 C 相同，每个 Perl 语句以分号 (;) 结尾。井号或磅符号 (#) 标记注释的开始；perl 程序会忽略从井号开始的行剩余部分。

Perl 语句组用大括号 ({ ... }) 括起来。此特性也与 C 类似。

## 变量

与 C 编程语言不同，你不需要在使用 Perl 变量之前声明它们。你可以很容易地在 Perl 脚本中识别变量，因为每个变量名都以特殊字符开头：at 符号 (@)、美元符号 ($) 或百分号 (%)。这些特殊字符表示变量的类型。三种变量类型如下：

标量变量表示基本数据类型：整数、浮点数和字符串。美元符号 ($) 在标量变量之前。以下是一些示例：

```
$maxlines = 256;
$title = "Red Hat Linux All-in-One Desk Reference";
```

数组变量是标量变量的集合。数组变量以 at 符号 (@) 为前缀。因此，以下是数组：

```
@pages = (62, 26, 22, 24);
@commands = ("start", "stop", "draw", "exit");
```

关联数组是键值对的集合，其中每个键都是字符串，值是任意标量变量。百分号 (%) 表示关联数组。你可以使用关联数组将名称与值关联。你可以将每个用户占用的磁盘空间存储在关联数组中，如下所示：

```
%disk_usage = ("root", 147178, "naba", 28547,
  "emily", 55, "ashley", 40);
```

因为每种变量类型都有特殊字符前缀，所以你可以使用相同的名称用于不同变量类型。因此，$disk_usage、@disk_usage 和 %disk_usage 可以出现在同一个 Perl 程序中。

## 标量

标量变量可以存储单个值，例如数字或文本字符串。标量变量是 Perl 中的基本数据类型。每个标量的名称以美元符号 ($) 开始。通常，你通过初始化它的赋值语句开始使用标量。你甚至可以在不初始化的情况下使用变量；数字的默认值是零，字符串的默认值是空字符串。如果你想查看标量是否已定义，请使用 defined 函数，如下所示：

```
print "Name undefined!\n" if !(defined $name);
```

表达式 (defined $name) 在 $name 已定义时为 1。你可以使用 undef 函数“取消定义”变量。例如，你可以按如下方式取消定义 $name：

```
undef $name;
```

变量根据上下文进行求值。以下是一个初始化并打印几个变量的脚本：

```
#!/usr/bin/perl
$title = "Red Hat Linux All-in-One Desk Reference";
$count1 = 650;
$count2 = 238;

$total = $count1 + $count2;

print "Title: $title -- $total pages\n";
```

当你运行前面的 Perl 程序时，它会产生以下输出：

```
Title: Red Hat Linux All-in-One Desk Reference -- 888 pages
```

正如 Perl 语句所示，当两个数值变量相加时，使用其数值；但当 $total 变量被打印时，显示其字符串表示形式。

Perl 的另一个有趣之处是它会计算双引号 ("...") 内字符串中的所有变量。然而，如果你在单引号 ('...') 内编写字符串，Perl 会保持该字符串不变。如果你写

```
print 'Title: $title -- $total pages\n';
```

使用单引号而不是双引号，Perl 显示

```
Title: $title -- $total pages\n
```

并且不生成新行。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_814_0.png)

一个有用的 Perl 变量是 $_（美元符号后跟下划线字符）。这个特殊变量被称为默认参数。Perl 解释器根据上下文确定 $_ 的值。当 Perl 解释器从标准输入读取输入时，$_ 包含当前输入行；当解释器搜索特定文本模式时，$_ 包含默认搜索模式。

## 数组

在 Perl 中，数组是标量的集合。数组名称以 at 符号 (@) 开始。与 C 相同，数组下标从零开始。你可以使用索引访问数组的元素。Perl 动态分配数组的空间。

考虑以下简单脚本：

```
#!/usr/bin/perl
@commands = ("start", "stop", "draw", "exit");

$numcmd = @commands;
print "There are $numcmd commands.\n";
print "The first command is: $commands[0]\n";
```

当你运行脚本时，它会产生以下输出：

```
There are 4 commands.
The first command is: start
```

正如你所见，将标量等同于数组会将标量设置为数组中元素的数量。@commands 数组的第一个元素引用为 $commands[0]，因为索引从零开始。因此，@commands 数组中的第四个元素是 $commands[3]。

两个特殊标量与数组相关。$[ 变量是其中之一，它是当前基索引（起始索引），默认为零。另一个标量是 $#arrayname（其中 arrayname 是数组变量的名称），其值为最后一个数组索引。因此，对于 @commands 数组，$#commands 为 3。

你可以使用如下简单 print 语句打印整个数组：

```
print "@commands\n";
```

当 Perl 执行此语句时，它显示以下输出：

```
start stop draw exit
```

## 关联数组

关联数组变量（以百分号 (%) 前缀声明）是 Perl 的独特特性。使用关联数组，你可以用字符串（如名称）索引数组。关联数组的一个很好的例子是 Perl 为你自动定义的 %ENV 数组。在 Perl 中，%ENV 是环境变量数组，你可以通过使用环境变量名称作为索引来访问它。以下 Perl 语句打印当前的 PATH 环境变量：

```
print "PATH = $ENV{PATH}\n";
```

当 Perl 执行此语句时，它会打印 PATH 的当前设置。与索引普通数组不同，你必须使用大括号来索引关联数组。



Perl 有许多内置函数——例如 delete、each、keys 和 values——可用于访问和操作关联数组。

## Perl 中的预定义变量

Perl 有几个预定义变量，其中包含在 Perl 脚本中可能需要的有用信息。以下是一些重要的预定义变量：

- @ARGV 是一个字符串数组，包含传递给脚本的命令行选项。第一个选项是 $ARGV[0]，第二个是 $ARGV[1]，以此类推。
- %ENV 是一个关联数组，包含环境变量。您可以使用环境变量名作为键来访问此数组。因此 $ENV{HOME} 是主目录，而 $ENV{PATH} 是 shell 用于定位命令的当前搜索路径。
- $_ 是许多函数的默认参数。如果您看到某个 Perl 函数未带任何参数使用，那么该函数很可能期望其参数包含在 $_ 变量中。
- @_ 是传递给子程序的参数列表。
- $0 是包含 Perl 程序的文件名。
- $^V 是您正在使用的 Perl 的版本号（例如，如果您使用 Perl 5.8.1 版本，$^V 将为 v5.8.1）。
- $< 是运行脚本的用户的用户 ID（一个标识号码）。
- $$ 是脚本的进程 ID。
- $? 是上一次系统调用返回的状态。

## 运算符和表达式

运算符用于组合和比较 Perl 变量。典型的数学运算符有加法 (+) 、减法 (-) 、乘法 (*) 和除法 (/) 。Perl 和 C 提供了几乎相同的运算符集合。当您使用运算符组合变量时，就得到了表达式。每个表达式都有一个值。

以下是一些典型的 Perl 表达式：

```
error < 0
$count == 10
$count + $i
$users[$i]
```

这些表达式是比较运算符（前两行）、算术运算符和数组索引运算符的示例。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_817_0.png)

在 Perl 中，不要使用 == 运算符来判断两个字符串是否匹配；== 运算符仅适用于数字。为了测试字符串的相等性，Perl 包含 FORTRAN 风格的 eq 运算符。如下所示，使用 eq 来查看两个字符串是否相同：

```
if ($input eq "stop") { exit; }
```

其他 FORTRAN 风格的字符串比较运算符包括 ne（不相等）、lt（小于）、gt（大于）、le（小于或等于）和 ge（大于或等于）。此外，您还可以使用 cmp 运算符来比较两个字符串。返回值是 -1、0 或 1，取决于第一个字符串是小于、等于还是大于第二个字符串。

Perl 还提供了以下独特运算符。C 缺少 FORTRAN 包含的指数运算符；Perl 使用 ** 作为指数运算符。因此，您可以在 Perl 中编写以下代码：

```
$x = 2;
$y = 3;
$z = $x**$y;  # z should be 8 (2 raised to the power 3)
$y **= 2; # y is now 9 (3 raised to the power 2)
```

您可以使用 () ——空列表运算符——将数组初始化为空，如下所示：

```
@commands = ();
```

点运算符 (.) 使您能够连接两个字符串，如下所示：

```
$part1 = "Hello.";
$part2 = "World!";
$message = $part1.$part2;  # Now $message = "Hello, World!"
```

重复运算符，用 x= 表示，十分有趣且很有用。您可以使用 x= 运算符重复一个字符串指定的次数。假设您想将一个字符串初始化为 65 个星号 (*)。以下示例展示了如何使用 x= 运算符初始化该字符串：

```
$marker = "*";
$marker x= 65;  # Now $marker is a string of 65 asterisks
```

Perl 中的另一个强大运算符是范围，用两个句点 (..) 表示。您可以使用范围运算符轻松初始化数组。以下是一些示例：

```
@numerals = (0..9); # @numerals = 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
@alphabet = ('A'..'Z'); # @alphabet = capital letters A through Z
```

## 正则表达式

如果您使用过 UNIX 或 Linux 系统一段时间，您可能知道 grep 命令，它使您能够在文件中搜索字符串模式。以下是使用 grep 定位所有文件中出现字符串 blaster 或 Blaster 的典型用法——在所有文件名以 .c 结尾的文件的任意行中：

```
cd /usr/src/linux*/drivers/cdrom
grep "[bB]laster" *.c
```

前面的 grep 命令会在文件名以 .c 结尾的文件中查找 blaster 和 Blaster 的所有出现情况。

grep 命令的 "[bB]laster" 参数被称为正则表达式，一种匹配一组字符串的模式。您可以使用一组小的运算符和规则构造正则表达式，这些规则类似于编写算术表达式的规则。例如，方括号 ([...]) 内的字符列表匹配列表中的任何单个字符。因此，正则表达式 "[bB]laster" 是以下两组字符串：

```
blaster  Blaster
```

Perl 支持正则表达式，就像 grep 命令一样。许多其他 Red Hat Linux 程序，例如 vi 编辑器和 sed（流编辑器），也支持正则表达式。正则表达式的目的是在文件中搜索字符串模式。这就是编辑器支持正则表达式的原因。

您可以在 Perl 中构造和使用复杂的正则表达式。这些正则表达式的规则相当简单。本质上，正则表达式是一串字符，其中某些字符具有特殊含义。表 4-1 总结了解释用于构造正则表达式的字符的基本规则。

表 4-1 正则表达式字符解释规则

| 表达式 | 含义 |
|---|---|
| . | 匹配除换行符外的任何单个字符。 |
| x* | 匹配字符 x 的零次或多次出现。 |
| x+ | 匹配字符 x 的一次或多次出现。 |
| x? | 匹配字符 x 的零次或一次出现。 |
| [...] | 匹配括号内的任意字符。 |
| x{n} | 匹配字符 x 恰好出现 n 次。 |
| x{n,} | 匹配字符 x 出现 n 次或更多。 |

（续）

### 表 4-1（续）

| 表达式 | 含义 |
|---|---|
| x{, m} | 匹配字符 x 出现零次或最多 m 次。 |
| x{n,m} | 匹配字符 x 至少出现 n 次，但不超过 m 次。 |
| $ | 匹配行的结尾。 |
| \0 | 匹配空字符。 |
| \b | 匹配退格。 |
| \B | 匹配不在单词开头或结尾的任意字符。 |
| \b | 匹配单词的开头或结尾 — 当不在括号内时。 |
| \cX | 匹配 Ctrl-X（其中 X 为任意字母字符）。 |
| \d | 匹配单个数字。 |
| \D | 匹配非数字字符。 |
| \f | 匹配换页符。 |
| \n | 匹配换行（换行符）字符。 |
| \ooo | 匹配由数字 ooo 指定的八进制值（其中每个 o 为 0 到 7 之间的数字）。 |
| \r | 匹配回车。 |
| \S | 匹配非空白字符。 |
| \s | 匹配空白字符（空格、制表符或换行符）。 |
| \t | 匹配制表符。 |
| \W | 匹配非字母字符。 |
| \w | 匹配字母数字字符。 |
| \xhh | 匹配由数字 hh 指定的十六进制值（其中每个 h 为 0 到 f 之间的数字）。 |
| ^ | 匹配行的开头。 |

如果您想匹配字符 $、|、*、^、[、]、\ 和 / 中的一个，您必须在要匹配的字符前加上反斜杠。因此，您应将这些字符输入为 \$, \|, \*, \^, \[, \], \\ 和 \/。由于奇怪的字符序列大量存在以及反斜杠的广泛使用，正则表达式看起来常常令人困惑。然而，就像其他任何事物一样，您可以从慢开始，起初只使用其中的几个特性。

到目前为止，我已经总结了正则表达式的语法。但我还没有展示如何在 Perl 中使用正则表达式。通常，您将正则表达式放在一对斜杠内，并使用匹配 (=~) 或不匹配

(=~) 和 (!~) 操作符用于测试字符串。你可以编写一个 Perl 脚本，其执行与本节前面使用 grep 完成的相同搜索。按照以下步骤完成此任务：

1. 使用文本编辑器输入并保存以下脚本到名为 lookup 的文件中：

```
#!/usr/bin/perl

while (<STDIN>)
{
    if ( $_ =~ /[bB]laster/ ) { print $_; }
}
```

2. 使用以下命令使 lookup 文件可执行：

```
chmod +x lookup
```

3. 使用以下命令尝试该脚本：

```
cat /usr/src/linux*/drivers/cdrom/sbpcd.c | ./lookup
```

在此情况下，cat 命令将特定文件的内容（正如你从 grep 示例中知道的，该文件包含一些带有正则表达式的行）馈送给 lookup 脚本。脚本 simply 应用 Perl 的正则表达式匹配操作符 (=~) 并打印任何匹配的行。输出应与使用以下命令显示的 grep 命令类似：

```
grep "[bB]laster" /usr/src/linux*/drivers/cdrom/sbpcd.c
```

lookup 脚本中的 $_ 变量需要一些解释。 <STDIN> 表达式从标准输入获取一行，默认情况下将该行存储在 $_ 变量中。在 while 循环内部，正则表达式与 $_ 字符串进行匹配。以下单个 Perl 语句完成了 lookup 脚本的工作：

```
if ( $_ =~ /[bB]laster/ ) { print $_; }
```

```
while (<STDIN>)
{
    if ( $_ =~ /\\n/ && $_ =~ /^ {7}\S/ ) { print $_; }
}
```

## 流程控制语句

到目前为止，你看到的 Perl 语句旨在按串行方式执行，一个接一个。Perl 还包括能够控制语句执行流程的语句。你已经看到过 if 语句和 while 循环。Perl 包含一套完整的流程控制语句，就像 C 中的一样，但有一些额外的特性。

在 Perl 中，所有条件语句采用以下形式：

```
conditional-statement
{ Perl code to execute if conditional is true }
```

请注意，你必须用大括号 ({...}) 括起条件语句后面的代码。条件语句检查表达式的值以确定是否执行大括号内的代码。在 Perl 中，与 C 相同，任何非零值都被视为逻辑真，而零值则为假。

接下来我简要描述 Perl 中主要条件语句的语法。

### if 和 unless

Perl 的 if 语句类似于 C 的 if 语句。例如，if 语句可以检查计数是否超过阈值，如下所示：

```
if ( $count > 25 ) { print "Too many errors!\n"; }
```

你可以向 if 语句添加 else 子句，如下所示：

```
if ($user eq "root")
{
    print "Starting simulation...\n";
}
else
{
    print "Sorry $user, you must be \"root\" to run this program.\n";
    exit;
}
```

如果你熟悉 C，你可以看到 Perl 的语法与 C 非常相似。if 语句的条件可以有零个或多个 elsif 子句以处理更多备选情况，如下所示：

```
print "Enter version number:"; # prompt user for version number

$os_version = <STDIN>;   # read from standard input
chop $os_version; # get rid of the newline at the end of the line
# Check version number
if ($os_version > 10 ) { print "No upgrade necessary\n";}
elsif ($os_version > 6 && $os_version < 9)
{ print "Standard upgrade\n";}
elsif ($os_version > 3 && $os_version < 6 ) { print "Reinstall\n";}
else { print "Sorry, cannot upgrade\n";}
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_822_0.png)

unless 语句是 Perl 独有的。该语句的形式与 if 相同，包括使用 elsif 和 else 子句。不同之处在于 unless 仅在条件为假时执行其语句块。例如，你可以在以下代码中使用 unless：

```
unless ($user eq "root")
{
    print "You must be \"root\" to run this program.\n";
    exit;
}
```

在这种情况下，除非字符串 user 是 "root"，否则脚本会退出。

### while

使用 Perl 的 while 语句进行循环——在现有条件变为逻辑假之前重复某些处理。要逐行从标准输入读取并处理该行，可以使用以下 while 循环：

```
while ($in = <STDIN>)
{
# Code to process the line
    print $in;
}
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_822_1.png)

如果你在不带任何参数的情况下从标准输入读取，Perl 会将标准输入的当前行分配给 $_ 变量。因此，你可以按如下方式编写前面的 while 循环：

```
while (<STDIN>)
{
# Code to process the line
    print $_;
}
```

Perl 的 while 语句比 C 的更灵活，因为你可以用几乎任何东西作为要测试的条件。例如，如果你使用数组作为条件，while 循环会一直执行直到数组没有元素剩余，如以下示例所示：

```
# Assume @cmd_arg has the current set of command arguments
while (@cmd_arg)
{
$arg = shift @cmd_arg; # this extracts one argument
# Code to process the current argument
print $arg;
}
```

shift 函数移除数组的第一个元素并返回该元素。

你可以使用 next 关键字跳到循环的末尾；last 关键字退出循环。例如，以下 while 循环将 1 到 10 的数字相加，跳过 5：

```
while (1)
{
$i++;
if($i == 5) { next; } # Jump to the next iteration if $i is 5
if($i > 10) { last; } # When $i exceeds 10, end the loop
$sum += $i; # Add the numbers
}
# At this point $sum should be 50
```

### for 和 foreach

Perl 和 C 的 for 语句语法相似。使用 for 语句根据表达式的值执行语句任意次数。语法如下：

```
for (expr_1; expr_2; expr_3) { statement block }
```

expr_1 在循环开始时只评估一次；语句块执行直到表达式 expr_2 评估为零。第三个表达式 expr_3 在每次执行语句块后评估。你可以省略任何表达式，但必须包含分号。此外，语句块周围的大括号是必需的。以下是使用 for 循环将 1 到 10 的数字相加的示例：

```
for($i=0, $sum=0; $i <= 10; $sum += $i, $i++) { }
```

在此示例中，实际的加法工作在第三个表达式中完成，而 for 循环控制的语句是一个空块 ({})。

foreach 语句最适合用于数组。以下是语法：

```
foreach Variable (Array) { statement block }
```

foreach 语句将 Array 中的一个元素分配给 Variable 并执行语句块。foreach 语句重复此过程直到没有数组元素剩余。以下 foreach 语句将 1 到 10 的数字相加：

```
foreach $i (1..10) { $sum += $i; }
```

请注意，我使用范围运算符 (..) 声明数组。你也可以使用逗号分隔的项目列表作为数组。

如果你在 foreach 语句中省略 Variable，Perl 会隐式使用 $_ 变量来保存当前数组元素。因此，你可以使用以下内容：

```
foreach (1..10) { $sum += $_; }
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_824_0.png)

### goto

goto 语句导致 Perl 跳转到由标签标识的语句。以下是提示用户输入值并在值不可接受时重复请求的示例：

```
ReEnter:
print "Enter offset: ";
$offset = <STDIN>;
chop $offset;
unless ($offset > 0 && $offset < 512)
{
    print "Bad offset: $offset\n";
    goto ReEnter;
}
```

### 访问 Linux 命令

你可以通过以下几种方式从 Perl 执行任何 Linux 命令：

- 使用包含要执行的 Linux 命令的字符串调用 system 函数。
- 将 Linux 命令用反引号 (`) 括起来，反引号也称为重音符。你可以通过这种方式运行 Linux 命令并捕获其输出。
- 调用 fork 函数复制当前脚本并在子进程中处理新命令。（如果一个进程启动另一个进程，则新进程称为子进程。）




- 调用 `exec` 函数用新脚本或 Linux 命令覆盖当前脚本。
- 使用 `fork` 和 `exec` 提供类似 shell 的行为。（监控用户输入，并通过子进程处理每个用户输入的命令。）在本节中，我将介绍一个实现此任务的简单示例。

最简单的方式在脚本中执行 Linux 命令是使用 `system` 函数并将命令放在字符串中。`system` 函数返回后，命令的退出代码位于 `$?` 变量中。你可以轻松编写一个简单的 Perl 脚本，从标准输入读取字符串并使用 system 函数处理该字符串。请按照以下步骤操作：

### 1. 使用文本编辑器输入以下脚本并保存到名为 rcmd.pl 的文件中：
```
#!/usr/bin/perl
# Read user input and process command

$prompt = "Command (\"exit\" to quit): ";
print $prompt;

while (<STDIN>)
{
  chop;
  if ($_ eq "exit") { exit 0;}

  # Execute command by calling system
  system $_;
  unless ($? == 0) {print "Error executing: $_\n";}
  print $prompt;
}
```

### 2. 使用以下命令使 rcmd.pl 文件可执行：
```
chmod +x rcmd.pl
```

### 3. 在 shell 提示符下输入 ./rcmd.pl 运行脚本。

以下是 rcmd.pl 脚本的示例输出（输出取决于你输入的命令）：
```
Command ("exit" to quit): ps
PID TTY TIME CMD
767 pts/0 00:00:00 bash
940 pts/0 00:00:00 rcmd.pl
945 pts/0 00:00:00 ps
Command ("exit" to quit): exit
```

你也可以在 Perl 脚本中使用 `fork` 和 `exec` 运行 Linux 命令。以下是示例脚本 — psh.pl — 它使用 `fork` 和 `exec` 执行用户输入的命令：

```
#!/usr/bin/perl

# This is a simple script that uses "fork" and "exec" to
# run a command entered by the user

$prompt = "Command (\"exit\" to quit): ";
print $prompt;

while (<STDIN>)
{
    chop;   # remove trailing newline
    if($_ eq "exit") { exit 0;}

    $status = fork;
    if($status)
    {
        # In parent... wait for child process to finish...
        wait;
        print $prompt;
        next;
    }
    else
    {
        exec $_;
    }
}
```

以下示例输出显示了 psh.pl 脚本如何执行 ps 命令：
```
Command ("exit" to quit): ps
PID TTY          TIME CMD
767 pts/0    00:00:00 bash
949 pts/0    00:00:00 psh.pl
950 pts/0    00:00:00 ps
Command ("exit" to quit): exit
```

Shell（例如 Bash）使用 fork 和 exec 组合来运行命令。

## 文件访问

你可能已经注意到本章各种示例中的 <STDIN> 表达式。那是 Perl 读取文件的方式。在 Perl 中，文件句柄，也称为标识符，在读取时为文件提供独特的身份。通常，文件句柄使用大写字符。STDIN 是一个预定义的文件句柄，表示标准输入——默认情况下为键盘。STDOUT 和 STDERR 是另外两个预定义的文件句柄。STDOUT 用于向终端打印，STDERR 用于打印错误消息。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_827_0.png)

要从文件读取，请将文件句柄写在尖括号（< >）内。因此，<STDIN> 从标准输入读取一行。

你可以使用 open 函数打开其他文件。以下示例展示了如何打开 /etc/passwd 文件进行读取以及如何显示该文件中的行：
```
open (PWDFILE, "/etc/passwd");  # PWDFILE is the file handle
while (<PWDFILE>) { print $_; }  # By default, input line is in $_
close PWDFILE;  # Close the file
```

默认情况下，open 函数以读取方式打开文件。你可以在文件名开头添加特殊字符以指示其他类型的访问。 < 前缀用于打开文件进行写入，而 > 前缀用于打开文件进行追加。以下是读取 /etc/passwd 文件并创建一个名为 output 的新文件，其中列出所有没有 shell 的用户（这些用户的密码条目在每行末尾都有 :）的简短脚本：
```
#!/usr/bin/perl
# Read /etc/passwd and create list of users without any shell
open (PWDFILE, "/etc/passwd");
open (RESULT, ">output");  # open file for writing

while (<PWDFILE>)
{
    if ($_ =~ /:$/) {print RESULT $_;}
}

close PWDFILE;
close RESULT;
```

执行此脚本后，你应该在当前目录中找到一个名为 output 的文件。以下是我在 Red Hat Linux 系统上运行此脚本时输出文件的内容：
```
news:x:9:13:news:/etc/news:
```

## 文件名中的管道前缀

一个有趣的文件名前缀是管道字符——竖线（|）。如果使用以 | 开头的文件名调用 open，则文件名其余部分被视为命令。Perl 解释器执行该命令，你可以使用 print 调用向该命令发送输入。以下 Perl 脚本使用 mail 命令向用户列表发送邮件消息：
```
#!/usr/bin/perl
# Send mail to a list of users
foreach ("root", "naba") {
    open (MAILPIPE, "| mail -s Greetings $_");
    print MAILPIPE "Remember to send in your weekly report today!\n";
    close MAILPIPE;
}
```

如果文件名以管道字符（|）结尾，则该文件名作为命令执行；你可以使用尖括号（<...>）读取该命令的输出，如以下示例所示：
```
open (PSPIPE, "ps ax |");
while (<PSPIPE>)
{
# Process the output of the ps command
# This example simply echoes each line
print $_;
}
```

## 子程序

虽然 Perl 包含大量内置函数，但你也可以以子程序的形式添加自己的代码模块。事实上，Perl 包含大量这些程序中的程序。以下是一个简单的脚本，说明了 Perl 中子程序的语法：
```
#!/usr/bin/perl
sub hello
{
# Make local copies of the arguments from the @_ array
local ($first,$last) = @_;

print "Hello, $first $last\n";
}

$a = Jane;
$b = Doe;

&hello($a, $b);  # Call the subroutine
```

运行上述脚本时，它会显示以下输出：
```
Hello, Jane Doe
```

注意子程序的以下几点：
- 子程序在数组 @_（@ 符号，后跟下划线字符）中接收其参数。
- 子程序中使用的变量默认是全局的。使用 local 函数创建一组局部变量。

通过在其名称前放置一个与号（&）来调用子程序。因此，子程序 hello 通过输入 &hello 调用。

如果愿意，你可以将子程序放在自己的文件中。例如，hello 子程序可以驻留在名为 hello.pl 的文件中。当你将子程序放在文件中时，请记住在文件末尾添加返回值——只需在末尾输入 1; 以返回 1。因此，hello.pl 文件如下所示：
```
sub hello
{
# Make local copies of the arguments from the @_ array
local ($first,$last) = @_;

print "Hello, $first $last\n";
}
1;  # return value
```

然后，你需要编写使用 hello 子程序的脚本，如下所示：
```
#!/usr/bin/perl
require 'hello.pl';  # include the file with the subroutine

$a = Jane;
$b = Doe;

&hello($a, $b);   # Call the subroutine
```

此脚本使用 require 函数包含包含 hello 子程序定义的 hello.pl 文件。

## Perl 中的内置函数

Perl 有近 200 个内置函数（也称为 Perl 函数），包括类似于 C 运行时库中的函数以及访问操作系统的函数。你确实需要浏览函数列表才能欣赏 Perl 可用功能的广度。本书没有足够的空间来介绍这些函数，但你可以通过将 Web 浏览器指向以下地址来了解 Perl 内置函数：http://www.perldoc.com/perl5.8.0/pod/perlf... 该地址会将你连接到 Perl 5.8.0 文档页面，以便你了解 Perl 内置函数的概览。在该页面上，单击函数名称以查看有关该函数的更详细信息。你也可以通过在终端窗口中输入以下命令在 Red Hat Linux 系统上阅读 Perl 函数手册：

```
man perlfunc
```

此命令显示函数的文本手册页。（我认为你会发现基于 Web 的文档更容易使用。）

## 理解 Perl 包和模块

Perl 包是一种将数据和子程序组合在一起的方式。基本上，它是一种使用变量和子程序名称而不与程序其他部分使用的名称冲突的方式。包的概念自 Perl 4 版本以来就存在。

包提供了一种控制命名空间的方式——该术语指的是变量和子程序名称的集合。虽然你可能没有意识到这一点，但当你编写 Perl 程序时，它会自动属于名为 main 的包。除了 main 之外，Perl 库中还有其他 Perl 包（这些包位于你的 Red Hat Linux 系统的 /usr/lib/perl5/X.Y.Z 目录中，其中 X.Y.Z 是 Perl 的版本号，例如 5.8.1），你也可以自行定义包。

Perl 模块是遵循特定准则的包。

### Perl 包

你可以将 Perl 包视为组织一组相关 Perl 子程序的便捷方式。另一个好处是，在包中定义的变量和子程序名称不会与程序其他地方使用的名称冲突。因此，一个包中名为 $count 的变量对该包保持唯一，不会与 Perl 程序其他地方使用的 $count 冲突。

Perl 包位于单个文件中。package 语句用于文件开头，声明该文件为包并为包命名。例如，文件 timelocal.pl 在名为 timelocal 的包中定义了多个子程序和变量。（请注意，timelocal.pl 文件已被 Time::Local 模块取代。）timelocal.pl 文件在多个位置有以下 package 语句：

```
package timelocal;
```

此包声明的效果是，所有后续的变量名和子程序名都被视为在 timelocal 包中。你可以将此类 package 语句放在实现该包的文件开头。

如果你在实现一个包并且需要引用另一个包中的子程序或变量怎么办？正如你可能猜到的那样，你所需要做的就是同时指定包名和变量（或子程序）名。Perl 提供了以下用于引用另一个包中变量的语法：

```
$Package::Variable
```

这里 Package 是包的名称，Variable 是该包中变量的名称。如果省略包名，Perl 假定你指的是 main 包中的变量。

要在程序中使用包，你可以简单地调用 require 函数并将包文件名作为参数。例如，有一个名为 ctime 的包定义在文件 ctime.pl 中。该包包含 ctime 子程序，可将二进制时间转换为字符串。以下简单程序使用来自 ctime.pl 文件的 ctime 包：

```
#!/usr/bin/perl -w

# Use the ctime package defined in ctime.pl file
require 'ctime.pl';

# Call the ctime subroutine
$time = ctime(time());

# Print the time string
print $time;
```

如你所见，此程序使用 require 函数将 ctime.pl 文件引入程序。当你运行此程序时，它应打印格式化的当前日期和时间，如以下示例输出所示：

```
Sat Jul 26 14:54:25 2003
```

请注意，此脚本的第一行使用了 -w 选项。该选项会导致 Perl 解释器打印有关 Perl 脚本中任何不良构造的警告信息。在调用 Perl 解释器的行中包含 -w 选项是个好主意。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_831_0.png)

### Perl 模块

Perl 5 将包的概念更进一步，引入了模块——一种遵循某些准则并设计为可重用的包。每个模块都是一个包，其定义在与包同名但扩展名为 .pm 的文件中。每个 Perl 对象都作为模块实现。例如，用于 Web 服务器的 CGI 对象被实现为 CGI 模块，存储在名为 CGI.pm 的文件中。

如今 Perl 附带了许多模块。你可以在 /usr/lib/perl5/X.Y.Z 目录中找到这些模块，其中 X.Y.Z 是 Perl 版本号。

对于 Perl 5.8.1 版本，Perl 模块位于 /usr/lib/perl5/5.8.1 目录中。查找以 .pm 结尾的文件名（.pm 代表 Perl module）。

### 使用模块

你可以调用 require 函数或 use 函数将 Perl 模块包含在你的程序中。例如，一个名为 Cwd 的 Perl 模块（按预期定义在 Cwd.pm 文件中）提供了一个 getcwd 子程序，用于返回当前目录。你可以调用 require 函数包含 Cwd 模块并按如下方式调用 getcwd：

```perl
require Cwd;  # You do not need the full file name
$curdir = Cwd::getcwd();
print "Current directory = $curdir\n";
```

第一行将 Cwd.pm 文件引入此程序——你不必指定完整文件名；require 函数会自动在模块名称后附加 .pm 以确定要包含哪个文件。第二行展示了如何从 Cwd 模块调用子程序。当你使用 require 包含模块时，必须使用 Module::subroutine 格式调用每个子程序。

如果你用 use 函数替换 require 重写此示例程序，它将采用以下形式：

```perl
use Cwd;
$curdir = getcwd();  # no need for Cwd:: prefix
print "Current directory = $curdir\n";
```

最显著的区别是你不再需要用模块名称前缀（如 Cwd::）限定子程序名。

你可以调用 require 或 use 将模块包含在程序中。只需记住使用这些函数时的以下细微差别：

- 当你通过调用 require 包含模块时，模块仅在程序运行时调用 require 函数时才被包含。你必须使用 Module::subroutine 语法调用通过 require 函数包含的模块中的任何子程序。
- 当你通过调用 use 包含模块时，模块在 use 语句被处理后立即包含在程序中。因此，你可以像它们是程序的一部分一样调用模块中的子程序和变量。你无需用 Module:: 前缀限定子程序和变量名。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_833_0.png)

你可能希望坚持使用 `use Module;` 语法将模块包含在程序中，因为这让你在调用模块中的子程序时使用更简单的语法。

### 在 Perl 中使用对象

对象是数据结构以及操作该数据的函数。每个对象都是类的一个实例，该类定义了对象的类型。例如，矩形类可能将矩形的四个角作为数据；函数例如计算矩形面积的一个；另一个绘制矩形。然后，每个矩形对象可以是矩形类的一个实例，每个角的坐标各不相同。从这个意义上说，对象是类的一个实例。

实现对象数据操作的函数（或子程序）称为方法。这是借用自 Smalltalk 的术语，Smalltalk 是最早的面向对象编程语言之一。

类还暗示了继承的概念。你可以通过扩展现有类的数据或方法（或两者）来定义新类的对象。继承的常见用途是表达对象各类的 IS A 关系。例如，考虑几何形状。因为圆 IS A 形状且矩形 IS A 形状，你可以说圆类和矩形类继承自形状类。在这种情况下，形状类称为父类或基类。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_833_1.png)

面向对象编程背后的基本思想是你可以将对象的数据和相关方法（子程序）打包，使其像黑盒一样工作——输入产生输出，而无需你指定完成任务的每一个细节。程序员只能通过公开的方法访问对象，而无需了解方法的内部工作原理。通常，程序员可以创建对象，调用其方法来获取或设置属性（这是对象数据的另一个名称），并销毁对象。在本节中，我将向你展示如何在 Perl 中使用对象。掌握这些知识后，你将能够利用对象作为 Perl 程序的构建块。

### 理解 Perl 对象

Perl 通过使用模块来实现对象，模块将数据和子程序打包在文件中。Perl 提供了以下简单的对象模型：

- 对象由引用表示（对象被实现为对哈希的引用）。



-   一个类是提供用于操作对象的方法的 Perl 模块。
-   一个方法是以对象引用作为第一个参数的 Perl 子程序。

对象实现者必须遵循某些规则并在代表类的模块中提供某些方法。然而，要在 Perl 程序中使用它，你实际上不需要了解太多关于对象实现的细节。实际使用时，你只需要知道在使用对象时需要遵循的步骤。

## 创建和访问 Perl 对象

特别有用的 Perl 对象是 Shell 对象，它由 Perl 模块 Shell.pm 实现。该模块随 Perl 发行版提供，位于 /usr/lib/perl5/5.8.1 目录中（适用于 Perl 5.8.1 版本）。

顾名思义，Shell 对象用于从 Perl 脚本内部运行 shell 命令。你可以创建一个 Shell 对象并让它执行命令。

使用 Shell 对象，请遵循以下一般步骤：

1.  在程序中加入以下行以包含 Shell 模块：

```
use Shell;
```

你必须在创建 Shell 对象之前包含这一行。

2.  要创建 Shell 对象，请使用以下语法：

```
my $sh = Shell->new;
```

其中 $sh 是对 Shell 对象的引用。

3.  使用 Shell 对象运行 Linux 命令并通过保存到合适的变量来捕获任何输出。例如，要将 /usr/lib/perl5/5.8.0 目录的目录列表保存到名为 @modules 的数组中，写入以下内容：

```
@modules = $sh->ls("/usr/lib/perl5/5.8.0/*.pm");
```

然后你可以按任何方式处理这个 Perl 模块文件名数组（*.pm 文件就是指这些）。例如，要简单地遍历数组并打印出每个字符串，使用以下 while 循环：

```
while(@modules)
{
  $mod = shift @modules;
  # Do whatever you want with the module name
  print $mod;
}
```

你如何知道要调用哪些方法以及按什么顺序调用它们？在使用对象之前，你必须阅读对象的文档。方法名称和方法调用的顺序取决于对象的作用。

## 使用 English 模块

Perl 包含多个具有奇怪名称的特殊变量，例如 $_（用于默认参数）和 $!（用于对应最近错误的错误消息）。阅读程序时，很难猜出特殊变量的含义。结果是你可能会避免使用本可在程序中派上用场的特殊变量。

作为一种便利措施，Perl 5 提供了 English 模块（English.pm），它使你能够为 Perl 中的各种特殊变量使用易于理解的名称。要使用 English 模块，在你的 Perl 程序中包含以下行：

```
use English;
```

之后，你可以将 $_ 称为 $ARG，将 $! 称为 $ERRNO（这些“英文”名称可能仍然有点晦涩，但肯定比标点符号好）。

以下程序使用 English 模块——并打印一些有趣的变量：

```
#!/usr/bin/perl -w
# File: english.pl

use English;
print "Perl executable = $EXECUTABLE_NAME\n";
print "Script name = $PROGRAM_NAME\n";
```

使用以下命令运行此脚本：

```
./english.pl
```

当我在 Red Hat Linux 上运行此脚本时，我得到的输出如下：

```
Perl executable = /usr/bin/perl
Script name = ./english.pl
```

English 模块很方便，因为它让你可以用有意义的名称引用特殊变量来编写 Perl 脚本。要了解更多关于 Perl 特殊变量及其英文名称的信息，在终端窗口中输入 man perlvar——或者，更好的方法是，将你的 Web 浏览器指向

```
http://www.perldoc.com/perl5.8.0/pod/perlvar.html
```

## 附录：关于 DVD

### 本附录内容

-   系统要求
-   DVD 安装说明
-   DVD 上包含的内容
-   故障排除

### 系统要求

请确保你的计算机满足以下列表中显示的最低系统要求。如果你的计算机与其中大多数要求不符，你在使用 DVD 上的软件和文件时可能会遇到问题。

-   配备 133 MHz Pentium 级处理器的 PC（图形模式推荐使用 400 MHz Pentium II 或更高）
-   计算机上至少安装 64MB 总 RAM 用于文本模式，128MB 用于图形模式；为获得最佳性能，我们推荐图形模式至少 256MB
-   DVD-ROM 驱动器（如果只有 CD-ROM 驱动器，请使用随附的优惠券订购 CD-ROM 版 Red Hat Linux）
-   显卡和能够显示至少 256 种颜色的显示器
-   声卡
-   以太网网络接口卡（NIC）或至少 56 Kbps 的调制解调器
-   硬盘上至少有 650MB 的可用空间用于最小安装；工作站级安装推荐 2.6GB

### DVD 安装说明

从 DVD 安装 Red Hat Linux 可能很棘手，因为某些 PC 硬件不受 Red Hat Linux 支持。尽管如此，附带 DVD 上的 Red Hat Linux 已支持各种硬件，因此你的 PC 外设很可能都得到支持的可能性很大。

要从附带 DVD 安装 Red Hat Linux，请遵循以下步骤。（有关最新信息，请参阅位于 DVD-ROM 根目录的 README 文件。）

1.  **在安装 Linux 之前，收集有关你 PC 硬件的信息，例如显卡、网卡和 SCSI 卡。**
2.  **使用 PartitionMagic 或 FIPS 等分区程序在硬盘上为 Red Hat Linux 创建空间。**
    如果你计划将 Red Hat Linux 作为 PC 上唯一的系统使用，或计划将其安装在空的第二块硬盘上，则跳过此步骤。
3.  **如果你的 PC 无法从 DVD 驱动器启动，请创建 Red Hat Linux 启动盘。**
4.  **使用 DVD 或 Red Hat Linux 启动盘启动你的 PC。**
    此步骤会自动运行 Red Hat Linux 安装程序。从现在开始，随着 Red Hat 安装程序引导你完成步骤，请在多个窗口中回答问题和选择。以下是一些关键安装步骤：
    -   识别安装在你 PC 上的任何 SCSI 适配器。
    -   为 Red Hat Linux 准备硬盘分区。如果你通过缩小现有 DOS 分区的大小来创建空间，此步骤可让你为 Red Hat Linux 创建分区。
    -   配置以太网网络（如有）。你可能需要指定参数，例如 Red Hat Linux 系统的 IP 地址和主机名。
    -   指定本地时区并设置 root 密码。
    -   在硬盘上安装引导加载程序，以便在关闭后重新启动 PC 时可以启动 Red Hat Linux。
    -   选择要安装的特定软件包，例如 X Window 系统和 GNOME 或 KDE 图形桌面。
    -   配置 X Window 系统并启用图形登录屏幕，以便在启动 Linux 系统时显示登录对话框，并在成功登录后直接进入 GNOME 或 KDE 图形桌面。

要将 DVD 上的特定软件包安装到你的硬盘，请遵循以下步骤：

1.  **以 root 身份登录。**
2.  **将 DVD 插入计算机的 DVD 驱动器。**
3.  **如果使用 GNOME 或 KDE GUI，请等待 DVD 挂载。否则，打开终端窗口并在命令提示符下输入**

```
mount /mnt/cdrom
```

4.  选择 主菜单：系统设置：添加/删除应用程序。

添加和删除软件实用程序启动并收集有关系统上已安装软件包状态的信息。在它整理完所有已安装软件包的信息后，实用程序会显示所有软件包的列表。窗口左侧有两个大按钮——安装软件和删除软件。默认情况下，安装软件按钮被选中。

5.  要安装任何未安装的软件包，请单击该软件包旁边的安装超链接。

出现一个对话框，显示有关你即将安装的内容以及新软件包所需的磁盘空间的详细信息。

6.  单击安装软件包以安装所选软件包。

7.  要从 DVD 驱动器中取出 DVD，请在命令提示符下输入以下命令：

```
umount /mnt/cdrom
```

### DVD 上包含的内容

本节提供了 DVD 上软件和其他内容的摘要。如果你需要帮助安装 DVD 上提供的项目，请参考前一节的安装说明。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_838_0.png)

Shareware 程序是受版权保护程序的功能齐全、免费的试用版。如果你喜欢某些程序，可以向作者支付少量费用注册并获得许可证、增强版本和技术支持。Freeware 程序是免费的、受版权保护的游戏、应用程序和实用程序。你可以免费将其复制到任意多台 PC 上——但它们不提供技术支持。GNU 软件受其自身许可证管辖，该许可证包含在 GNU 软件的文件夹中。GNU 软件的分发不受任何限制。有关详细信息，请参阅 DVD 根目录中的 GNU 许可证。软件的试用版、演示版或评估版通常在时间和功能上有限制（例如不允许你在创建项目后保存项目）。

你可以在 DVD 上找到以下软件（有关 DVD 目录组织的详细信息，请参阅位于 DVD 根目录的 README 文件）：

-   Linux 内核 2.4.22，包含主要 PC 硬件配置的驱动模块，包括 IDE/EIDE 和 SCSI 驱动器、PCMCIA 设备、CD 驱动器和 DVD 驱动器
-   用于设置设备和服务的完整安装和配置工具集



- 基于 XFree86 4.3.0 包的图形用户界面，配备 GNOME 2.4 和 KDE 3.1 图形桌面
- 用于 Internet、局域网和内联网的完整 TCP/IP 网络
- 用于使用 PPP、DSL 或拨号串行通信程序将您的 PC 连接到 Internet 服务提供商 (ISP) 的工具
- 完整的 Internet 应用套件，包括电子邮件 (sendmail, mail)、新闻 (INN)、TELNET、FTP、DNS 和 NFS
- Evolution 1.4.5 电子邮件和日历应用程序
- OpenOffice.org 1.0 办公套件，包含文字处理器、电子表格、演示软件等
- Apache Web 服务器 2.0.47，可将您的 PC 变成 Web 服务器；以及 Mozilla 1.4，用于上网冲浪
- Samba 3.0 LAN 管理器软件，用于 Microsoft Windows 连接
- 多种文本编辑器（例如 GNU Emacs 21.3；vim）
- 图形和图像处理软件，如 The GIMP、Xfig、Gnuplot、Ghostscript、Ghostview 和 ImageMagick
- 编程语言（GNU C 和 C++ 3.3、Perl 5.8.1、Tcl/Tk 8.3.5、Python 2.2.3、GNU AWK 3.1.3）和软件开发工具（GNU Debugger 5.3、CVS 1.11、RCS 5.7、GNU Bison 1.875、flex 2.5.4a、TIFF 和 JPEG 库）
- 支持行业标准的 Executable and Linking Format (ELF) 和 Intel Binary Compatibility Specification (iBCS)
- 来自 GNU 项目的完整标准 UNIX 工具套件
- 访问和使用 DOS 文件和应用程序的工具 (mtools 3.9.9)
- 文本格式化和排版软件 (groff、TeX 和 LaTeX)

## Troubleshooting

如果您在安装或使用随附 DVD 上的材料时遇到困难，请参阅第一册中的详细安装和故障排除说明。

如果您在从 DVD 安装项目时遇到问题，请致电客户服务 800-762-2974（美国以外：317-572-3993）或发送电子邮件至 techsup@wiley.com。Wiley Publishing Inc. 仅为安装和其他一般质量控制项目提供技术支持；有关应用程序的技术支持，请咨询程序的供应商或作者。

## Index

### Symbols

. (点)
连接运算符，790
cp 命令参数，171
文件系统导航，167
.. (点点)
数组初始化，790
文件系统导航，167
... (省略号)，在 C 函数中，760
; (分号)，注释指示符，680
() (括号)，空列表运算符，790
$0 (美元符号，零)，Perl 变量，789
2> (两个大于号)，I/O 重定向，145
</...> (尖括号，斜杠)，HTML 标签，374
<...> (尖括号)，HTML 标签，374
* (星号)
可执行文件指示符，168
通配符，145–148
@ (at 符号)
链接指示符，167–168
Perl 数组名称，787
Perl 变量，786
在资源记录中，680
@_ (at 符号，下划线)，变量，789
` (反引号)，Perl 语句，797
[...] (方括号)，通配符，147–148
{...} (花括号)
在 C 语句中，754
注释指示符，678
在 Perl 语句中，794
$ (美元符号)
Perl 变量，786
区域文件指令，679
$< (美元符号，小于号)，Perl 变量，789
$? (美元符号，问号)，Perl 变量，789
$_ (美元符号，下划线)，Perl 变量，787, 789
$$ (美元符号)，Perl 变量，789
== (等号)，相等运算符，790
! (感叹号)
模式匹配，662
重复命令，148–149
/ (正斜杠)，根目录指示符，161
> (大于号)，I/O 重定向，145
# (井号)
注释指示符，652
在 C 指令中，739
在 HTML 锚点中，363
- (连字符)，权限指示符，169
< (小于号)，I/O 重定向，145
% (百分号)，Perl 变量，786
? (问号)
在 HTML 锚点中，363
通配符，146–148
/*...*/ (斜杠星号)，注释指示符，678
// (斜杠斜杠)，注释指示符，678
| (竖线)，管道字符，144, 800–801
-= (等号，波浪号)，匹配运算符，792
!~ (感叹号，波浪号)，不匹配运算符，793
~ (波浪号)，主目录指示符，167

### A

- 绝对路径名，166
- accept 命令，490
- 访问控制指令，627-629
- 访问点，324
- AccessFileName 指令，623
- AddDescription 指令，624
- AddEncoding 指令，623
- AddIcon 指令，624
- AddIconByEncoding 指令，624
- AddIconByType 指令，624
- AddType 指令，623
- Ad-Hoc 模式，322
- Adobe Reader，226
- ADSL (Asymmetric DSL)，290
- AIM 服务，357-358
- Alias 指令，623
- 别名。参见链接
- allow from 指令，629
- AllowOverride 指令，628
- 尖括号，斜杠 (</...>)，HTML 标签，374
- 尖括号 (<...>)，HTML 标签，374
- anon_mkdir_write_enable 选项，635
- anon_upload_enable 选项，635-636
- 匿名 FTP，638-640。另请参见 FTP
- anonymous_enable 选项，636
- Anyware Office，16，181-182
- AOL AIM 服务，357-358
- Apache Software Foundation (ASF)，616
- Apache Web 服务器
  - 在 DVD 上，812
  - 历史，616
  - 安装，615
  - 启动，615-617
- Apache Web 服务器，配置
  - 访问控制指令，627-629
  - 配置文件，619-629
  - 配置工具，618-619
  - 目录，617-618
  - 通用 HTTPD 指令，620-622
  - 资源配置指令，622-627
  - 虚拟主机设置，629-632
- 小程序。参见 GNOME 小程序；KDE 小程序
- 应用网关，527，564-565
- 应用层，310
- 应用程序。另请参见数据库；多媒体
  - 计算器，180-181
  - GIMP，205-207
  - 图形和图像，204-208
  - KGhostview，207-208
  - 用于 PDF，207-208
  - 用于 PostScript 文档，207-208
  - 在 Red Hat 网络中注册，476-477
  - 升级，476-478
- 办公应用程序。另请参见 OpenOffice.org
  - Anyware Office，181-182
  - CrossOver Office，183
  - 拼写检查器，183-184
  - StarOffice，182
- Applixware，网站，182
- Applixware Office，16，181-182
- @ARGV 变量，789
- 数组
  - C 语言，745-746
  - Perl，787-788，790
- ascii_download_enable 选项，636
- ascii_upload_enable 选项，636
- ASF (Apache Software Foundation)，616

### B

aspell 实用程序，183–184
关联数组，788–789
结合性，751–753
星号 (*)
  可执行文件指示符，168
  通配符，145–148
Asymmetric DSL (ADSL)，290
async_abor_enable 选项，636
at 命令，421–423
at 符号，下划线 (@_)，变量，789
at 符号 (@)
  链接指示符，167–168
  Perl 数组名称，787
  Perl 变量，786
在资源记录中，680
ATA 支持，503–504
附件，电子邮件，347
audio CDs
  烧录，199–202
  播放，193–194
审计，安全，524
身份验证，523，527
AuthGroupFile 指令，629
AuthName 指令，628
授权，523
AuthType 指令，628
AuthUserFile 指令，629
自动命令补全，146
ax 命令，154–155
back quote (`)，Perl 语句，797
后门，527
background, changing
  GNOME，83–85，116–117
  KDE，90–91，137–139
backing up data
  自动化备份，453–454
  商业实用程序，449
  增量备份，453
媒体，447–448
多卷归档，451–452
单卷归档，449–451
策略，447–448
系统管理，400
磁带归档器，449–454
tar 命令，449–454
banned_email_file 选项，636
Bash shell
  内置 shell 脚本命令，777–780
  命令行，94
  进程管理，154–155
  root 用户，154
  启动，93–94
Bash shell, shell commands
  自动补全，146
  组合，144
  串联，144
  I/O 重定向，144–146
  多行，143
  概述，94
  重复，148–149
  语法，142–144
  通配符，146–148
bastion host，527，559，562–564
Berkeley Internet Domain Name (BIND)，672–676
BIND (Berkeley Internet Domain Name)，672–676
bit bucket，146
位字段，745–748
块设备，481，502–503
BogoMIPS，74
书签，246
boot loader. 另请参见 GRUB (GRand Unified Bootloader)；LILO (Linux Loader)
  定义，73
  安装，46–47
启动消息，74

### C

- booting
  - 安装后，73–78
  - 内核重建后，516
  - 从启动磁盘启动，故障排除，59
  - 定义，73
  - 紧急启动磁盘，494，516
  - /etc/inittab 文件，405–406
  - 从 GNOME 或 KDE 启动，77
  - init 进程，403–405
  - 用于安装，38–39
  - 运行级别，404，406–407
  - 启动/停止服务器，408–409
  - 启动脚本，407–408
  - 系统在启动后挂起，516
- brackets ([...])，通配符，147–148
- break C 语句，753
- 缓冲区溢出，527，540–541
- 错误。参见调试器
- 内置函数，Perl，802–803
- C 编译器，716–720
- C++ 编译器，716–720
- C 库，760–762
- C programming. 另请参见 Perl programming；software development
  - 数组，745–746
  - 结合性，751–753
  - 位字段，745–748
  - 条件指令，741–742
  - 数据类型，743–744
  - 变量的声明和定义，743–744
  - 声明与定义，739
  - 在 DVD 上，812
  - 枚举，744
  - 表达式，749–751
  - 函数原型，759–760
  - 函数，759–760
  - 包含文件，740
  - 宏，740–743
  - 运算符优先级，751–753
  - 指针，746–747
  - 预处理器指令，739–743
  - 程序结构，737–739
  - 标准头文件，761–762
  - 结构体，745–748
  - 类型定义，747–748
  - 类型限定符，748
  - 联合体，745–748
  - 变量，743–744
- C programming, statements
  - for，755–756
  - break，753
  - case，754
  - 复合，754
  - continue，754
  - default 标签，755
  - do，755
  - 表达式，755
  - goto，756
  - if，756
  - if-else，756–757
  - null，757
  - return，757
  - switch，757–758
  - void 类型，760
  - while，758–759
- CA (Certificate Authority)，527
- cable modem，293–298
- Cable Modem Termination System (CMTS)，295
- caching name server，配置，677–686
- cal 命令，155–156
- Calc。参见 OpenOffice.org Calc



## C
- 计算数据，256–259
- 计算器，180–181
- cancel 命令，489
- case C 语句，754
- cat 命令，158
- cd 命令，166–167
- 识别 CD 驱动器，197–198
- CD-ROM，67–69
- 光盘。另见 DVD
- 音频，193–194，199–202
- 书后。另见 DVD，书后
- 数据，202–203
- 烧录光盘
- 音频 CD，199–202
- DAO 方法，201
- 数据 CD，202–203
- 硬件要求，196
- 识别 CD 驱动器，197–198
- ISO 映像，203–204
- 曲目间暂停，201
- 首选项对话框，198–199
- TAO 方法，201
- 证书，527
- 证书颁发机构 (CA)，527
- 挑战握手认证协议 (CHAP)，307
- CHAP（挑战握手认证协议），307
- 字符设备，481，508
- 图表数据，256–259
- chgrp 命令，436–437
- 芯片，定义，712
- chkconfig 命令，552，604–605
- chmod 命令，170–171
- chown 命令，171，437
- chown_uploads 选项，636
- chown_userid 选项，636
- chown_username 选项，636
- chroot_list_enable 选项，636
- chroot_list_file 选项，636
- 类，Perl，807
- CMTS（电缆调制解调器终止系统），295
- 代码成熟度级别选项，499
- CodeWeavers，17，183
- COM 端口，300–310
- 命令行
- Bash shell，94
- 定义，713
- 命令处理器，定义，713
- 命令行 FTP 客户端，392–396
- 命令。另见 Bash shell，shell 命令；Linux 命令；特定命令的条目
- DOS，457–460
- 内核模块管理，482
- RPM，463–464
- 通用 UNIX 打印系统 (CUPS)，487
- 通用漏洞和暴露 (CVE)，574
- 编译器，714
- 复合 C 语句，754
- 计算机程序，定义，714
- 计算机
- 硬件组件，712–713
- 操作系统，713–714
- 连接
- shell 命令，144
- 字符串，790
- 条件指令，741–742
- 数据保密性，527
- 配置文件。另见 TCP/IP，配置文件；特定文件的条目
- Apache Web 服务器，619–629
- Linux，409–411
- 配置工具。另见 内核，配置工具
- Apache Web 服务器，618–619
- 在 DVD 上，811
- 服务配置实用程序，605–606
- 配置。另见 Apache Web 服务器 服务器，配置（DNS 域名系统），配置
- 防火墙，49，292
- FTP 服务器，634–638
- GNOME，115–117
- INN 服务器，658–664
- KDE，137–139
- 内核，496。另见 内核，配置工具
- LANs，317–319
- LANs，TCP/IP，317–319
- LANs，无线以太网，326–332
- 网络，在安装期间，47–49
- 启动时网络，342
- 新闻组，665–666
- NFS，701–702
- 概述，25
- Red Hat Linux，25
- Samba，705–706
- TCP/IP 网络，启动时，342
- 无线以太网，326–332
- connect_from_port_20 选项，636
- 无连接协议，595
- 面向连接的协议，594–595
- 控制台窗口。另见 终端窗口
- 控制台。另见 物理控制台；虚拟控制台
- const 限定符，748
- continue C 语句，754
- COPYING 文件，472
- 复制文件，114，135
- 统计文件中的单词和行数，156–157
- cp 命令，171–172
- CPU
- 定义，712
- 安装 Red Hat Linux，30
- 破解者，527
- 破解密码，532
- 创建
- 数据库，187
- 目录，172–173
- 文件夹，115，136
- 组，433
- 安装启动磁盘，32–33
- makefile，725–727
- crontab 命令，424–426
- CrossOver Office，17，183
- ctlinnd 程序，659
- CUPS（通用 UNIX 打印系统），487
- 大括号（{...}）
- 在 C 语句中，754
- 注释指示符，678
- 在 Perl 语句中，794
- 自定义
- GNOME，83–85
- KDE，90–92
- CustomLog 指令，622
- CVE（通用漏洞和暴露），574
## D
- DAO（一次写入磁盘）方法，201
- 烧录数据 CD，202–203
- 数据保护，524
- 数据类型，743–744
- 数据库
- 构建，185–186
- 创建，187
- 定义表，188
- 描述，185
- 插入记录，188–189
- MySQL 监视器，187
- 查询，189–190
- Red Hat Linux 功能，16
- data_connection 选项，636
- 数据报，595
- 日期和时间
- 日历，打印，155–156
- 显示，155
- GMT，50
- 时区，设置，49–50，75
- UTC，50
- date 命令，155–156
- 调试器，714，727–734
- 变量的声明和定义，743–744
- 声明与定义，739
- 解密，527
- 默认标签，755
- DefaultIcon 指令，624
- DefaultType 指令，623
- 碎片整理硬盘，33–34
- 延迟循环，74
- 删除
- 文件中的字符，157–158
- 目录，173
- 文件和文件夹，114–115
- 文件或文件夹，135–136
- 隐藏文件，34
- 拒绝服务 (DoS)，522，528
- deny 指令，629
- deny_email_enable 选项，636
- 桌面页图标，126
- 桌面弹出菜单
- GNOME，100–102
- KDE，122–124
- 桌面。另见 GNOME；KDE
- 概述，16
- 登录时选择，100，120
- 检测，574
- 设备驱动程序，479–480
- 设备文件，480–481
- 设备
- 块，481
- 字符，481
- /etc/modules.conf 文件，484–485
- 热插拔，485–487
- 钥匙链存储，486–487
- 可加载驱动模块，481–485
- 主设备号，480–481
- 次设备号，480–481
- 在文件系统上挂载，442–445
- 网络，481
- USB，485–487
- df 命令，175，417
- DHCP（动态主机配置协议），312–313，597
- 图表。另见 OpenOffice.org Draw
- 拨号网络，298–308
- 词典小程序，129–131
- dig（域名互联网探测器）程序，674–675
- 数码相机，190–193
- 数字时钟，126
- 数字签名，528，543–544
- 数字用户线路 (DSL)，288–293
- 目录（续）
- 根，161
- 顶级，163–164
- /usr 子目录，164–165
- /var 子目录，165
- DirectoryIndex 指令，623
- dirmessages_enable 选项，637
- 禁用
- 服务，552–555
- 独立服务器，551–552
- 磁盘性能和使用情况，417–418
- 磁盘空间，检查，175–176
- 一次写入磁盘 (DAO) 方法，201
- 磁盘，22
- 发行版，11
- DMZ，528
- DNS（域名系统）
- BIND，672–676
- dig 程序，674–675
- 在 DVD 上，812
- FQDN，672
- 层次域名，671–672
- host 程序，674–676
- named 守护进程，673–674
- 概述，670–671
- 解析器库，674
- 反向查找，675
- 根域，672
- 实用程序，674–676
- DNS（域名系统），配置
- 缓存名称服务器，677–686
- /etc/named.conf 文件，677–679
- 主名称服务器，686–688
- 解析器，676–677
- rndc 实用程序，679
- RR 格式，680–682
- /var/named/localhost.zone 文件，684–685
- /var/named/named.ca 文件，683–684
- /var/named/named.local 文件，685
- 区域文件格式，679–680
- do C 语句，755
- DocumentRoot 指令，622
- 文档，Writer
- 编辑，233–235
- 从他人获取，224–225
- 大型，247–248
- 审阅，233–235
- 美元符号，小于 ($<)，Perl 变量，789
- 美元符号，问号 ($?)，Perl 变量，789
- 美元符号，下划线 ($_)，Perl 变量，787，789
- 美元符号，零 ($0)，Perl 变量，789
- 美元符号 ($)
- Perl 变量，786
- 区域文件指令，679
- 美元符号 ($$) ，Perl 变量，789
- 域名互联网探测器 (dig) 程序，674–675
- 域名系统 (DNS)。另见 DNS（域名系统）
- domainname 命令，690
- DoS（拒绝服务），522，528
- 运行 DOS 命令，457–460
- DOS 文件系统。另见 文件系统，DOS
- 点 (.)
- 连接运算符，790
- cp 命令参数，171
- 文件系统导航，167
- 点点 (..)
- 数组初始化，790
- 文件系统导航，167
- 点分十进制表示法，312
- 下载文件。另见 文件传输
- 绘图。另见 OpenOffice.org Draw
- 驱动器字母，161–162
- du 命令，175-176，418
- 双宿主主机，528
- 转储数据包头，341-342
- DVD，书后
- 内容，811-812
- 安装，809-811
- 系统要求，809
- 故障排除，812
- DVD/CD-ROM，安装 Red Hat Linux，30
- DVD-ROM，22。另见 光盘
- 动态主机配置协议 (DHCP)，312-313，597
## E
- echo 命令，776
- ed，211-214
- 编辑只读文件，210
- 编辑器
- ed，211-214
- vi，214-219
- 802.11x 以太网标准，322
- ELF（可执行和链接格式），在 DVD 上，812
- 省略号 (...) 在 C 函数中，760
- 电子邮件。另见 IM（即时消息）；邮件服务器；sendmail 程序
- 附件，347
- 自动消息处理，656-657
- 传递机制，643-645
- HTML 消息，347-348
- MTA，346-347
- MUA，346-347
- 重定向，655-656
- 测试邮件传递，642-643
- 电子邮件，邮件阅读器
- Mozilla，353-357
- 摘要表，348
- Ximian Evolution，348-353
- 紧急启动磁盘，494，516
- 加密。另见 公钥加密
- 定义，528
- 数字签名，528，543-544
- 指纹，543
- 哈希，543
- 主机安全问题，541-549
- 密码，533-536
- 安全，主机问题，541-549
- 英语模式，808
- enum 数据类型，744
- 枚举，744
- env 命令，434
- %ENV 变量，789
- 环境变量，434-436，714
- Epiphany，365
- 等于，波浪号 (~-) ，匹配运算符，792
- 等号 (==)，相等运算符，790
- 错误消息
- 丢弃，146
- 保存到文件，145
- ErrorDocument 指令，625-626
- ErrorLog 指令，621
- /etc/fstab 文件，444-445
- /etc/host.conf 文件，335
- /etc/hosts 文件，334
- /etc/hosts.allow 文件，336
- /etc/hosts.deny 文件，336-337
- /etc/inittab 文件，405-406
- /etc/modules.conf 文件，484-485
- /etc/named.conf 文件，677-679
- /etc/networks 文件，334
- /etc/nsswitch.conf 文件，337
- /etc/passwd 文件，431-432
- /etc/resolv.conf 文件，335
- /etc/vsftpd.conf 文件，635-637
- /etc/vsftpd.ftusers 文件，638
- /etc/vsftpd.user_list 文件，638



## F
Ethernet。参见 LANs（局域网），Ethernet
Ethernet 电缆，315–316
Evans, Chris，634
Evolution，在 DVD 上，812
感叹号，波浪号 (!~)，不匹配运算符，793
感叹号 (!)
模式匹配，662
重复命令，148–149
exec 函数，798
exec-shield 程序，540–541
可执行和链接格式 (ELF)，在 DVD 上，812
expire 程序，659
导出文件系统，446，698–700
表达式，C 语句，755
表达式
C 编程，749–751
定义，715
Perl，789–794

字段，在文档中，245–247
文件访问，Perl，799–800
文件句柄，799–800
文件管理器。参见 Konqueror；Nautilus shell
文件共享。参见 sharing files
文件大小，内核，512–513
文件系统。另见 directories；files；folders
驱动器号，161–162
文件名扩展名，162
层次结构，440–442
内核配置，509–510
长文件名，162
概述，23–24
路径名，162–163
由 Linux 内核支持，509–510
卸载，175，400，443
文件系统，DOS
命令摘要，459
在 DVD 上，812
格式化软盘，460–461
挂载软盘，455–457
挂载分区，454–455
mtools 软件包，457–460
概述，454
运行 DOS 命令，457–460
通配符，460
文件系统，挂载
定义，22
描述，175
上的设备，442–445
/etc/fstab 文件，444–445
挂载点，443
NFS，447
系统管理，400
文件系统，导航
绝对路径名，166
当前目录，更改，166
当前目录，显示，166
主目录，切换到，167
父目录，切换到，167
相对目录名，166
文件传输
命令行 FTP 客户端，392–396
FTP，313
FTP 命令，394–396
gFTP，390–391
图形 FTP 客户端，389–392
TFTP，313
Web 浏览器，391–392
文件传输协议 (FTP)，597。另见 file transfer
命令行客户端，392–396
命令，394–396
定义，313
在 DVD 上，812
图形客户端，389–392
TFTP，313
文件名扩展名，162
文件名，464–465
文件。另见 ownership
合并，158
复制，114，135，171–172
计数单词和行，156–157
删除，114–115，135–136，172
删除字符，157–158
查找，156，173–174
链接到，167–168
列出，168–169
移动，114，135，172
读取，95
重命名，115，136
搜索内容，156
排序，157
跨软盘分割，158
替换字符，157–158
查看，111–114，132–135
find 命令，173–174。另见 grep command
查找。参见 searching
指纹，543
FIPS（First Nondestructive Interactive Partition Splitting Program）
定义，34
分区硬盘，35–38
防火墙
Bastion 主机，559，562–564
特征，558
配置，49，292
定义，528，557
形式，558–559
包过滤，559–561
带 Bastion 主机的边界网络，559，562–564
筛选路由器，559–561
防火墙，双宿主主机
定义，561
概述，561–562
带代理服务，559
用户登录，562
FireWire 支持，505–507
First Nondestructive Interactive Partition Splitting Program（FIPS）
定义，34
分区硬盘，35–38
firstboot 过程，57–58，77
软盘-磁带设备驱动程序，508
流量控制
C 语言，741
Perl，794–797
流量控制语句，715
弹出工具栏，279–280
文件夹。另见 ownership
创建，115，136
删除，114–115，135–136
重命名，115，136
查看，111–114，132–135
for
C 语句，755–756
Perl 语句，796–797
foreach 语句，796–797
fork 函数，797
格式化 DOS 软盘，460–461
fortune 命令，435
.forward 文件，655–657
正斜杠（/），根目录指示符，161
FQDN（完全限定域名），672
frames。参见 packets
frames，在文档中，241
自由软件基金会 (FSF)，13
FSF（自由软件基金会），13
Ftape，508

## G
FTP（文件传输协议），597。另见 file transfer
命令行客户端，392–396
命令，394–396
定义，313
在 DVD 上，812
图形客户端，389–392
TFTP，313
ftp 命令，393
FTP 命令，394–396
FTP 服务器
匿名 FTP，638–640
配置，634–638
/etc/vsftpd.conf 文件，635–637
/etc/vsftpd.ftusers 文件，638
/etc/vsftpd.user_list 文件，638
安装，633–634
PAMs，638
vsftpd 服务器，635
ftpd_banner 选项，637
完全限定域名 (FQDN)，672
函数原型，759–760
函数
C 编程，759–760
定义，715
Perl，802–803
shell 脚本，773–774

Gaim，357–358
GCC（GNU C 和 C++ 编译器），716–720
gcc 命令，716–720
gdb 调试器
命令，729–730
在 DVD 上，812
查找错误，731–732
修复错误，733–734
准备调试程序，727–728
退出，728
运行，728
通用 HTTPD 指令，620–622
通用公共许可证 (GNU GPL)，472，734–735
通用公共许可证 (GPL)，472，734–735
gFTP，390–391
GIMP（GNU 图像处理程序），205–207
GMT（格林威治标准时间），50
GNOME（Gnu 对象模型环境）。另见 KDE
背景，更改，83–85，116–117
配置，115–117
自定义，83–85
描述，79
桌面弹出菜单，100–102
在 DVD 上，812
帮助，20
图标弹出菜单，102–103
启动器小程序，80
注销，86
主菜单，81–82，105–108
移动和调整窗口大小，80
Pager 小程序，80
面板，80–81，102–105
Red Hat 按钮，81–82，105–108
登录时选择，100
主题，85
用户界面，79–82
虚拟桌面，80
壁纸，84，117
网站，79
GNOME 小程序
添加，108–109
定义，108
列表，110–111
移除，109
启动，80，82
天气，81
GNOME 面板，80–81，102–105
GNOME 系统监视器，414
GnomeToaster，刻录 CD
音频 CD，199–202
DAO 方法，201
数据 CD，202–203
硬件要求，196
识别 CD 驱动器，197–198
ISO 镜像，203–204
曲目间暂停，201
首选项对话框，198–199
TAO 方法，201
GNU C 和 C++ 编译器 (GCC)，716–720
GNU 调试器。参见 gdb debugger
GNU GPL（通用公共许可证），472，734–735
GNU 图像处理程序 (GIMP)，205–207
GNU LGPL（库通用公共许可证），735–735
Gnu 对象模型环境 (GNOME)。参见 GNOME（Gnu 对象模型环境）
GNU Privacy Guard（GPG）。参见 GPG（GNU Privacy Guard）
GNU 软件
常见软件包，14–15
定义，13
概述，13–15
goto
C 语句，756
Perl 语句，797
GPG（GNU Privacy Guard）
加密/解密文档，548–549
交换密钥，545–547
生成密钥对，544–545
签名文件，547–548
gPhoto，190
GPL（通用公共许可证），472，734–735
GRand Unified Bootloader（GRUB），46–47，513–515
图形应用程序，16
图形 FTP 客户端，389–392
图形用户界面 (GUIs)，16–17
图像
应用程序，204–208
在文档中，243–245
Impress，270–273
软件，在 DVD 上，812
大于号（>），I/O 重定向，145
格林威治标准时间 (GMT)，50
grep 命令，156。另见 find command
groff 程序，在 DVD 上，812
Group 指令，621
groupadd 命令，433
groupdel 命令，434
组
添加用户，433
创建，433
文件所有权，更改，436–437
移除，434
GRUB（GRand Unified Bootloader），46–47，513–515
GUIs（图形用户界面），16–17

## H
硬盘
定义，712
碎片整理，33–34
分区，28，34–38，42–45
硬盘驱动器，安装 Red Hat Linux，30–31
硬件
设置，无线 Ethernet，324–325
系统管理，400
硬件，和安装
兼容性，31–32
检测，39，56–57
库存，27–28，29–31
hash，528，543
hash 标记 (#)
在 C 指令中，739
注释指示符，652
在 HTML 锚点中，363
HeaderName 指令，624
帮助
气泡帮助，126
GNOME，20
KDE，20
man 手册页，19–21
Mozilla，376
工具提示，Writer，229
隐藏文件
删除，34
显示，34
层次域名，671–672
主页，更改，369–370
主机连接，检查，339
主机名，77
主机程序，674–676
hosts，528。另见 security，host issues
热插拔，23，485–487
HTML（超文本标记语言），360
HTML 消息，347–348
<HTML> 源视图，378
HTML 标签视图，377
HTTP（超文本传输协议）
定义，313
Internet 标准，612
概述，611–614
端口号，597
httpd 服务器，18
httpd.conf 配置文件
访问控制指令，627–629
通用 HTTPd 指令，620–622
资源配置指令，622–627
超链接，361–363
超文本标记语言 (HTML)，360
超文本传输协议 (HTTP)。参见 HTTP（超文本传输协议）
连字符 (-)，权限指示符，169

## I
iBCS（Intel 二进制兼容规范），在 DVD 上，812
ICAT 元数据，574
图标弹出菜单
GNOME，102–103
KDE，124–125
IDE 支持，503–504
idle-session 选项，637
IDSL（ISDN DSL），290
IEEE 1394 支持，505–507
if
C 语句，756
Perl 语句，794–795
ifconfig 命令，337–338
if-else C 语句，756–757
IM（即时消息），357–358。另见 e-mail



图像，在网页中插入，
375–376
成像应用程序，204–208
Impress。参见 OpenOffice.org Impress
事件处理，524
事件响应，579–580
#include 指令，740
在 C 程序中包含文件，740
incoming.conf 文件，663
IndexIgnore 指令，624–625
IndexOptions 指令，624–625
基础设施模式，322
init 命令，406–407
init 进程，403–405
INN (InterNetNews) 服务器
组件，659
配置，658–664
控制文件，659–664
ctlinnd 程序，659
在 DVD 上，812
expire 程序，659
incoming.conf 文件，663
inn.conf 文件，660–661
innd 程序，659
安装，657–658
newsfeeds 文件，661–663
nnrpd 程序，659
ntpsend 程序，659
readers.conf 文件，663–664
启动，664–665
wildmat 模式，662
inn.conf 文件，660–661
innd 程序，659
innd 服务器，18
创建安装启动盘，32–33
安装工具，在 DVD 上，811
安装
Apache Web 服务器，615
设备，手动，56–57

FTP 服务器，633–634
INN，657–658
内核，513–515
内核模块，513
操作系统更新，531–532
软件包组，52–54
RPM 软件包，69–71，467–468
Samba，702–703
软件，系统管理，400
SRPMS，475
安装 Red Hat Linux
安装引导加载程序，46–47
启动，38–39
创建安装启动盘，32–33
碎片整理硬盘，33–34
防火墙配置，49
硬件，检测，56–57
硬件兼容性，31–32
硬件检测，39
硬件清单，27–28，29–31
选择安装类型，39–42
指定 IP 地址，47–49
键盘，31，39–42
指定语言支持，49
手动安装设备，56–57
鼠标，31，39–42
网络配置，47–49
概述，24–25
安装软件包组，52–54
分区硬盘，28，34–38，42–45
设置 root 密码，50–52
服务器类安装，42
在文本模式下，56
所需时间，38
设置时区，49–50
与 Windows 一起，28
工作站类安装，42

即时消息 (IM)，357–358。另请参阅 e-mail
完整性，528
Intel 二进制兼容规范 (iBCS)，在 DVD 上，812
in.telnetd 服务器，18
Internet。另请参阅 newsgroups；在线资源：Web
概述，285–286
安全，524
服务器，17–18，593–594
Internet，连接
ADSL，290
有线调制解调器，293–298
CHAP，307
COM 端口，300–310
拨号网络，298–308
DSL，288–293
IDSL，290
IRQs，300–310
本地环路，288
环路长度，289
连接调制解调器，299–300
测试调制解调器，302–304
调制解调器，winmodems，301
概述，286–288
PAP，307–308
PPP，299，304–307
SDSL，290
串行端口检测，301–302
串行设备名称，300–310
USB，300–310
Internet，服务
无连接协议，595
面向连接协议，594–595
数据报，595
定义，593
DHCP，597
FTP，597

HTTP，597
LANs，TCP/IP，312–313
NFS，598
NNTP，598
NTP，598
端口号，597–599
安全，524，551–555
SMTP，598
SNMP，598
套接字，594–597
TCP/IP，594–597
TELNET，598
TFTP，598
UDP，595
InterNetNews (INN) 服务器。参见 INN (InterNetNews)
互联网络，311
入侵者保护，292
I2O 设备支持，507
I/O 重定向，144–146
安装期间指定 IP 地址，47–49
IP 地址
点分十进制表示法，312
IPv6，311–312
LANs，TCP/IP，311–312
TCP/IP，311–312
检查 IP 路由表，338
IP 欺骗，528
IPSec 协议，528
iptables 命令，567–569
IPv6，311–312
IRQs，300–310
ISDN DSL (IDSL)，290
ISDN 子系统，507
刻录 ISO 映像，203–204
将 PC 与 Internet 隔离，292–293
ISP 工具，在 DVD 上，812
iwconfig 命令，332

## J
操纵杆，508

## K
- K 按钮，125–129
- K 桌面环境 (KDE)。参见 KDE (K Desktop Environment)
- KDE (K 桌面环境)。另请参阅 GNOME
- 背景，更改，90–91，137–139
- 配置，137–139
- 自定义，90–92
- 描述，86–88
- 桌面页面图标，126
- 桌面弹出菜单，122–124
- 数字时钟，126
- 在 DVD 上，812
- 帮助，20
- 图标弹出菜单，124–125
- K 按钮，125–129
- Kicker 应用程序，126
- 注销，92
- 主菜单，126–129
- 面板，88–89，125–126
- Red Hat 按钮，88–89
- 登录时选择，120
- 主题，91–92
- 用户界面，88–92
- 虚拟桌面，126
- 壁纸，91，138–139
- 网站，86
- KDE 小程序
- 添加，130
- 词典，129–131
- 列表，131–132
- 移除，131
- 启动，129

- KDE 面板，88–89，125–126
- 内核
- 在 DVD 上，811
- 破解，511–512
- 模块管理命令，482
- 重新构建，493–496
- 升级，492–493
- 版本，12，95
- 内核，构建
- 文件大小，512–513
- GRUB，设置，513–515
- 安装，513–515
- 模块，构建和安装，513
- 重启系统，516
- "系统太大" 错误，513
- 内核，配置工具
- ATA 支持，503–504
- 块设备，502–503
- 字符设备，508
- 代码成熟度级别选项，499
- 文件系统，509–510
- FireWire 支持，505–507
- 软盘-磁带设备驱动程序，508
- Ftape，508
- 通用设置，500
- IDE 支持，503–504
- IEEE 1394 支持，505–507
- I2O 设备支持，507
- ISDN 子系统，507
- 操纵杆，508
- 内核破解，511–512
- 可加载模块支持，499
- MFM 支持，503–504
- 鼠标，508
- 多媒体设备，508–509
- 网络设备支持，507
- 网络选项，503
- 选项依赖关系，499
- 并行端口支持，500–501

## L
内核，配置工具（续）
PCMCIA 字符设备，508
即插即用配置，501-502
处理器类型和功能，500
RLL 支持，503-504
SCSI 支持，505
声音，510
启动，497-498
电话支持，503-504
USB 支持，511-512
看门狗卡，508
键盘，31，39-42
钥匙链存储设备，486-487
KGhostview，207-208
Kicker 应用程序，126
kill 命令，155
Kimball, Spencer，205
Konqueror
复制文件，135
创建文件夹，136
删除文件或文件夹，135-136
移动文件，135
重命名文件或文件夹，136
对列表视图排序，135
查看文件和文件夹，132-135
查看网页，136
指定语言支持，49
LANs (局域网)，连接到 Internet，315-316
LANs (局域网)，以太网电缆，315-316
CSMA/CD，314
概述，314-315
数据包，315
设置，313-314
粗缆，315-316
细缆，315-316

LANs (局域网)，TCP/IP
应用层，310
配置，317-319
和 Internet，311
Internet 服务，312-313
互联网络，311
IP 地址，311-312
层，310-311
网络层，310
概述，309-311
物理层，311
端口号，312-313
传输层，310
LANs (局域网)，无线以太网
接入点，324，326
Ad-Hoc 模式，322
配置，326-332
硬件设置，324-325
基础设施模式，322
受管模式，322
移动站，324
检查网络接口状态，332
概述，321-322
标准，321-322
WEP，323-324
LaTeX，在 DVD 上，812
启动器小程序，80
层，268，310-311
ldd 实用程序，762-763
小于号 (<)，I/O 重定向，145
LGPL (库通用公共许可证)，735-735
库
C，760-762
解析器库，674
共享，762-768
库通用公共许可证 (GNU LGPL)，735-735

## M
库通用公共许可证 (LGPL)，735–735
许可
GPL，472，734–735
LGPL，735–735
LILO (Linux Loader)，46–47
链接支持，495–496
链接，361–363
Linux 应用程序。参见 applications
Linux 命令，Bash shell
列表，149–153
概述，94–95
Linux 命令，在 Perl 中执行，797–799
Linux Loader (LILO)，46–47
Linux Online，25
Listen 指令，621
listen 选项，637
可加载驱动模块，481–485
可加载模块支持，499
LoadModule 指令，622
局域网 (LANs)，连接到 Internet，315–316
局域网 (LANs)，以太网。参见 LANs (局域网)
本地环路，288
local_enable 选项，637
local_umask 选项，637
LogFormat 指令，622
注销
GNOME，86
KDE，92
长文件名，162
环路长度，289
循环，C 语言
break 语句，753
continue 语句，754
do 语句，755
null 语句，757

for 语句，755–756
while 语句，758–759
循环，Perl，795–796
lp 命令，488–489
lpc status 命令，490
lpq 命令，489
lpstat 命令，489–490
ls 命令，168–169
lsmod 命令，482–483
ls_recurse_enable 选项，637
m4 宏处理器，646–648
宏
C 编程，740–743
make 实用程序，723–724
Magicdev 实用程序，67
安装邮件服务器。另请参阅 e-mail
.forward 文件，655–657
m4 宏处理器，646–648
邮件投递机制，643–645
sendmail，别名文件，657
sendmail，配置文件，645–652
sendmail，配置，642
sendmail，文件，654–655
sendmail.cf 文件语法，652–654
sendmail.mc 文件，648–652
启动，642
测试邮件投递，642–643
邮件传输代理 (MTA)，346–347
邮件用户代理 (MUA)，346–347
主菜单
GNOME，81–82，105–108
KDE，126–129
主设备号，480–481
make 命令，474
make 实用程序，720–727



- make xconfig 命令，497
- makefiles
- creating，725–727
- example，724–725
- names，721
- overview，721–722
- man 命令，19
- man 手册页，19–21
- 管理模式，322
- 主讲义，268
- 主备注，268
- 主幻灯片，268
- Mattis, Peter，205
- MaxClients 指令，622
- MaxSparesServers 指令，621
- MD5 加密，533–536
- 内存，定义，712
- 菜单，GNOME
- 桌面弹出菜单，100–102
- 图标弹出菜单，102–103
- 主菜单，81–82，105–108
- 菜单，KDE
- 桌面弹出菜单，122–124
- 图标弹出菜单，124–125
- 主菜单，126–129
- 菜单，Mozilla，369
- 方法，Perl，807
- MFM 支持，503–504
- mformat 工具，460–461
- 微处理器，定义，712
- Microsoft Office，在 Linux 上运行。
- 参见 CrossOver Office
- 次要设备号，480–481
- MinSpareServers 指令，621
- 风险缓解，524
- mkbootdisk 命令，494
- mkdir 命令，172–173
- 移动站，324
- 调制解调器
- 有线，293–298
- 连接，299–300
- 安装 Red Hat Linux，31
- 测试，302–304
- winmodems，301
- modprobe 命令，483–484
- 模块化内核，495–496
- 模块，Perl，804–806
- 监视器，安装 Red Hat Linux，31
- 性能监控，参见
- 性能监控
- 单片内核，495–496
- more 命令，95，156
- mount 命令，174，442–445
- 挂载
- DOS 软盘，455–457
- DOS 分区，454–455
- 文件系统 参见 文件系统，
- 挂载
- NFS，700
- 鼠标，31，39–42，508
- 移动文件，114，135
- Mozilla
- 电子邮件，353–357
- 阅读新闻组，383–387
- Mozilla，Web 浏览器
- 自定义，370–372
- 主页，更改，369–370
- 菜单，369
- 启动，365
- 状态栏，368–369
- 冲浪，372
- 主题，370–372
- 工具栏，366–368
- 用户界面，365–369
- Mozilla Composer
- 帮助气球，376
- <HTML> 源视图，378
- HTML 标签视图，377
- 插入图像，375–376
- 普通视图，377
- 预览视图，378
- 示例编辑会话，375–376
- 视图，377–378
- MTA（邮件传输代理），346–347
- mtools 软件包，457–460
- MUA（邮件用户代理），346–347
- 多媒体
- 数字相机，190–193
- 播放音频 CD，193–194
- 播放声音文件，194–196
- 多媒体，刻录 CD
- 音频 CD，199–202
- DAO 方法，201
- 数据 CD，202–203
- 硬件要求，196
- 识别 CD 驱动器，197–198
- ISO 镜像，203–204
- 曲目间暂停，201
- 首选项对话框，198–199
- TAO 方法，201
- 多媒体设备，508–509
- mv 命令，172
- MySQL
- 构建数据库，185–186
- 创建数据库，187
- 定义表，188
- 描述，185
- 设计数据库，186
- 插入记录，188–189
- MySQL 监视器，187
- 查询数据库，189–190
- MySQL AB，185
- MySQL 监视器，187
## N
- 名称守护进程控制器 (ndc)，679
- 名称服务切换 (NSS) 文件，337
- named 守护进程，673–674
- NAT（Natural Address Translation）
- 路由器
- 有线调制解调器，297–298
- DSL，292–293
- Natural Address Translation（NAT）
- 路由器
- 有线调制解调器，297–298
- DSL，292–293
- Nautilus shell
- 复制文件，114
- 创建文件夹，115
- 删除文件和文件夹，114–115
- 移动文件，114
- 重命名文件和文件夹，115
- 对列表视图排序，114
- 查看文件和文件夹，111–114
- ndc（名称守护进程控制器），679
- Nessus 安全扫描器，585–588
- netstat 命令，339–341
- 网卡，31
- 网络设备支持，507
- 网络设备，481
- Network File System（NFS）。参见 NFS（Network File System）
- Network Information Service（NIS）
- 服务器。参见 NIS（Network Information Service）
- 网络层，310
- 网络映射器 (nmap)，584–585
- Network News Transfer Protocol
- (NNTP)，313，598
- 网络协议，17
- Network Time Protocol（NTP），598
- 网络选项，503
- 网络。另请参见 LANs；安全，网络；TCP/IP
- network;
- 安装期间配置，47–49
- 接口，检查，332，337–338
- 概述，17，24
- 状态，检查，339–341
- 系统管理，400
- 新闻源，658
- 新闻服务器。参见 INN（InterNetNews）
- newsfeeds 文件，661–663
- 新闻组。另请参见在线资源
- 添加，667
- 配置，665–666
- 层次结构，定义，665–666
- 层次结构，描述，380–382
- 与 Linux 相关，382–383
- 概述，379–380
- 发布到，386–387
- 搜索，388
- 订阅，386
- 测试，667
- 顶级类别，381–382
- 新闻组，阅读
- 使用 Mozilla，383–387
- 新闻阅读器，383
- 在网站上，388
- 来自您的 ISP，383–387
- 新闻阅读器，383
- NFS（Network File System）
- 配置，701–702
- 定义，313
- 在 DVD 上，812
- 导出文件系统，446，698–700
- 挂载，447，700
- 端口号，598
- 共享文件，697–702
- NFS 服务器配置工具，701–702
- NIS（Network Information Service）
- 服务器
- 客户端，设置，689–692
- 客户端-守护进程设置，691–692
- 配置文件设置，691
- 域名设置，690–691
- 信息类型，688
- 地图创建，692–693
- 主服务器配置，693–695
- 概述，688–689
- 设置，692–695
- 从服务器配置，694
- 测试，695–696
- nmap（网络映射器），584–585
- nnrpd 程序，659
- NNTP（Network News Transfer Protocol），313，598
- ntpsend 程序，659
- 不可否认性，528
- nopriv_user 选项，637
- noprobe 命令，56–57
- 普通视图，377
- NSS（名称服务切换）文件，337
- NTP（Network Time Protocol），598
- null C 语句，757
## O
- 目标代码，714
- 对象，Perl，806–808
- 在线文档，19–21
- Adobe Reader，226
- Anyware Office，182
- Anywhere Desktop for Linux，17
- Apache Web 服务器，616
- Applixware，182
- Applixware Office，16
- Arkeia，449
- 备份实用程序，449
- BrightStor ARCserve Backup，449
- BRU，449
- CodeWeavers，183
- Computer Associates，449
- CrossOver Office，17
- CTAR，449
- CVE，574
- 数字相机，190
- Ethernet，322
- GNOME，79
- Google Groups，59
- gPhoto，190
- 主机安全，588
- ICAT Metabase，574
- INN，659
- IPv6 FAQ，312
- KDE，86
- 内核版本，12
- Knox Software，449
- Linux Online，25
- Lone Star Software Corporation，449
- LONE-TAR，449
- MySQL AB，185
- OpenOffice.org，182
- OpenSSH，555
- PartitionMagic，35
- 公共新闻服务器，383
- SAINT，588
- SANS Institute，574
- 安全监控，549
- 安全新闻和更新，530
- 安全漏洞，574
- StarOffice，17，182
- Tolis Group, Inc，449
- Tripwire 程序，549
- UniTrends Software Corporation，449
- VistaSource，182
- Open Secure Shell（OpenSSH），555–557
- OpenOffice.org
- 在 DVD 上，812
- 网站，182
- OpenOffice.org Calc
- 计算数据，256–259
- 单元格使用，跟踪，258
- 图表数据，256–259
- 输入数据，253–256
- 功能，250
- 格式化数据，253–256
- 函数，自动化，258
- 主窗口，251–252
- 场景，256–259
- 设置，252–253
- OpenOffice.org Draw
- 绘图，280–282
- 功能，275–276
- 弹出工具栏，279–280
- 主窗口，276–278
- 工具提示，280
- OpenOffice.org Impress
- 功能，261–262
- 图形，270–273
- 插入幻灯片，266
- 层，268
- 主窗口，262–265
- 主讲义，268
- 主备注，268
- 主幻灯片，268
- 重新排列幻灯片，267–268
- 设置，265
- 幻灯片版式，选择，266
- 幻灯片排序视图，267–268
- 特殊效果，270–273
- OpenOffice.org Impress，演示文稿
- 交付，273–274
- 准备，267–270
- 打印为 PDF，273
- 保存，266–267
- 类型，选择，266
- 来自 Writer 大纲，267
- OpenOffice.org Writer
- 书签，246
- 文档，编辑，233–235
- 文档，从他人获取，224–225
- 文档，大型，247–248
- 文档，审阅，233–235
- 功能，225–226
- 字段，245–247
- 格式化页面，235–239
- 框架，241
## P
- OpenOffice.org Writer（续）
  - 开始使用，226–227
  - 图形，243–245
  - 主窗口，227–229
  - 页面布局，239–243
  - PDF 格式，226
  - 参考文献，246
  - 设置，229–232
  - 样式，235–239
  - 模板，235–239
  - 工具提示，229
- OpenSSH（Open Secure Shell），555–557
- 操作系统，9–11
- 运算符
- C 语言，751–753
- Perl，789–790
- 选项依赖，499
- Options 指令，628
- order 指令，629
- 所有权
- 更改，170–171，436–437
- 安全问题，537
- 查看，436
- 软件包组，安装，52–54
- 软件包。另请参见 RPM 软件包
- 从源文件构建，470–475
- Perl，803–804
- 源文件，下载和解包，470–472
- SRPMS，安装，475
- 升级，476–478
- 数据包过滤
- 定义，529
- 启用，559–561，565–569
- 数据包
- 定义，315
- 转储头，341–342
- 安全，529
- 嗅探，341–342
- Pager 小程序，80
- PAMs（可插拔认证模块），533–536，638
- pam_service_name 选项，637
- PAP（密码认证协议），307–308
- 并行端口支持，500–501
- 括号 (())，空列表运算符，790
- 分区硬盘，28，34–38，42–45
- PartitionMagic
- 定义，34
- 分区硬盘，35
- Password Authentication Protocol（PAP），307–308
- 密码
- 破解，532
- 加密，533–536
- MD5 加密，533–536
- NIS，694
- PAMs，533–536
- 审查，579
- root 密码，设置，50–52
- 安全，主机问题，532–536
- shadow，532–533
- 有效性检查，532
- 路径名，162–163
- PCMCIA 字符设备，508
- PCs
- 硬件组件，712–713
- 操作系统，713–714
- PDFs
- Impress 演示文稿，273
- 查看和打印，207–208
- Writer 文档，226
- 渗透测试，582–583
- 百分号 (%)，Perl 变量，786



性能监控
df 命令，417
磁盘性能和使用，417–418
du 命令，418
GNOME 系统监视器，414
系统管理，400
系统使用摘要，416–417
top 实用程序，412–414
uptime 命令，414–416
运行时间统计，414–416
vmstat 实用程序，416–417
周界网络，529
带有堡垒主机的周界网络，559, 562–564
句点。见 点
外围设备，23
Perl 程序，检测，782–783
Perl 编程。另见 C 编程；软件开发
数组，787–788, 790
关联数组，788–789
内置函数，802–803
类，807
默认参数，787
English 模式，808
exec 函数，798
表达式，789–790
文件访问，799–800
文件句柄，799–800
流程控制，794–797
foreach 语句，796–797
fork 函数，797
goto 语句，797
if 语句，794–795
Linux 命令执行，797–799
循环，795–796
方法，807
模块，804–806
对象，806–808
运算符，789–790
概述，781–782
包，803–804
管道前缀，800–801
预定义变量，789
正则表达式，791–794
标量，786–787
for 语句，796–797
子程序，801–802
语法，785
system 函数，798
unless 语句，794–795
变量，786–789
变量，别名，808
while 语句，795–796
编写脚本，784–785
权限
更改，170–171, 537–538
显示，169
字母代码，170
列表，577–579
查看，577–579
设置默认值，538–539
setuid，539–540
PHP and MySQL for Dummies，190
物理控制台，141
物理层，311
PidFile 指令，622
ping 命令，339
ping，339
管道前缀，800–801
PKI（公钥基础设施），529
即插即用配置，501–502
可插拔认证模块（PAMs），533–536, 638
指针，C 编程，746–747
点对点协议（PPP），299, 304–307
端口号
Internet 服务，597–599
LANs，TCP/IP，312–313
端口扫描，529, 583–585
可移植性，10
向新闻组发布，386–387
PostScript 文档，查看和打印，207–208
井号（#）。见 hash 标记（#）
PPP（点对点协议），299, 304–307
预处理器指令，739–743
演示软件。见 应用程序，办公
预防，573
预览视图，378
主名称服务器，686–688
打印队列
CUPS，487
启用/禁用，490
打印作业，取消，489
打印作业，定义，487–488
查询，489
排队，487–488
打印系统，管理，400
printenv 命令，434
打印机
名称，显示，490
概述，23
设置，60–64
状态，检查，489–490
打印文件，488–489
探针，39
/proc 文件系统，418–421
进程
定义，713
列出，154–155
停止，155
处理器。见 CPU
处理器类型和功能，500
procmail 程序，656–657
生产力软件，16–17
编程基础，714–715。另见 C 编程；Perl 编程；软件开发
程序。另见 C 编程；Perl 编程；软件开发
查找，782
运行，显示，95
代理服务器，529
ps 命令，95, 157
公钥密码学，529
公钥加密。另见 加密
加密/解密文档，548–549
交换密钥，545–547
生成密钥对，544–545
OpenSSH，556–557
概述，542–543
签名文件，547–548
公钥基础设施（PKI），529
pwd 命令，166

## Q
查询数据库，189–190
问号（?）
在 HTML 锚点中，363
通配符，146–148

## R
RAM
定义，712
安装 Red Hat Linux，30
readers.conf 文件，663–664
ReadmeName 指令，624
重新排列幻灯片，267–268
重启。见 启动
录制 CD。见 CD，刻录
Red Hat 按钮
GNOME，81–82, 105–108
KDE，88–89
Red Hat Linux，概述。另见 安装 Red Hat Linux
配置，25
数据库应用程序，16
桌面，16 另见 GNOME（Gnu Object Model Environment）；KDE（K Desktop Environment）
磁盘，22
发行版，11
DVD-ROM，22
探索，25–26
文件系统，23–24
GNU 软件，13–15
图形应用程序，16
GUI，16–17
热插拔，23
Internet 服务器，17–18
学习，25–26
网络，17, 24
在线文档，19–21
操作系统，9–11
外围设备，23
可移植性，10
打印机，23
生产力软件，16–17
共享文件，23–24
软件开发，18–19
声音卡，23
电子表格，16
系统管理，21–24
USB，23
版本号，11–12
Red Hat 软件包管理器（RPM）。见 RPM（Red Hat 软件包管理器）
Red Hat 设置代理，73–78
Redirect 指令，623
参考文献，在文档中，246
在 Red Hat 网络注册，476–477
正则表达式，791–794
reject 命令，490
相对目录名，166
远程登录，安全，555–557
远程名称守护进程（rndc）实用程序，679
重命名
文件和文件夹，115
文件或文件夹，136
替换文件中的字符，157–158
require 指令，629
解析器，配置，676–677
解析器库，674
资源配置指令，622–627
资源记录（RR）格式，680–682
响应，574
恢复数据
商业实用程序，449
媒体，447–448
多卷归档，451–452
单卷归档，449–451
策略，447–448
系统管理，400
return C 语句，757
反向查找，675
抓取 CD。见 CD，刻录
风险分析，522, 523
RLL 支持，503–504
rm 命令，172
rmdir 命令，173
rndc（远程名称守护进程）实用程序，679
根目录，161, 440
根域，672
root 密码，设置，50–52
root 用户。另见 系统管理
在 Bash shell 中，154
定义，52
用于 GUI 实用程序，401–403
以其身份登录，401
恢复忘记的密码，402–403
route 命令，338
路由器，筛选，559–561
例程，715
rpcinfo 命令，695
rpcwhich 命令，695–696
RPM（Red Hat 软件包管理器）
命令，463–464
文件名，464–465
rpm 命令，463–464
RPM 软件包。另见 软件包
获取有关信息，466–467
已安装，列出，466
安装，69–71, 467–468
移除，468–469
搜索，466
升级，469
验证，469–470
版本号，获取，465
查看其中的文件，466
RR（资源记录）格式，680–682
运行级别，404, 406–407
运行程序，显示，95

## S
SAINT（安全管理员集成网络工具），588
Samba
检查，704
组件，703–704
配置，705–706
在 DVD 上，812
安装，702–703
测试，707
Windows 2000 和 XP，707
SANS Institute，574
SARA（安全审计员研究助手），589
标量，Perl，786–787
场景，256–259
Schaefer, Arno，36
调度作业，421–426
筛选路由器，529
筛选路由器，559–561
ScriptAlias 指令，624
脚本。见 shell 脚本
SCSI 控制器，31
SCSI 支持，505
SDSL（对称 DSL），290
搜索
文件内容，156
文件和目录，156, 173–174
新闻组，388
RPM 软件包，466
安全 Shell（SSH），555–557
安全。另见 防火墙
审计，524, 571–573
身份验证，523, 527
授权，523
后门，527
堡垒主机，527
缓冲区溢出，527
业务需求，521
CA，527
有线调制解调器暴露，296–297
证书，527
常见威胁，522
数据保密性，527
破解者，527
数据保护，524
解密，527
数字签名，528
DMZ，528
DoS，522, 528
DSL 暴露，292
双宿主机，528
加密，323, 528
哈希，528
主机问题，525
主机，528
实施解决方案，524
事件处理，524
完整性，528
Internet 访问，524
Internet 服务，524
入侵者保护，292
IP 欺骗，528
IPSec 协议，528
将 PC 与 Internet 隔离，292–293
缓解，524
监控，549–550
NAT 路由器，292–293, 297–298
网络问题，526
不可否认性，528
在线资源，530
概述，519–520
包过滤，定义，529
包过滤，启用，565–569
数据包，529
周界网络，529
物理，403
PKI，529
端口扫描，529
代理服务器，529
公钥密码学，529
责任，524
风险分析，522, 523
筛选路由器，529
setuid 程序，529
流密码，323
对称密钥加密，529
系统管理，400
威胁，529
特洛伊木马，529
未经授权的访问，522
未经授权的信息披露，522
病毒，530
漏洞，522–523, 530, 574–576
WEP，323–324
蠕虫，530
安全，主机。另见 防火墙
缓冲区溢出，540–541
加密，541–549
GPG，541–549
在线资源，588
操作系统更新，576–577
操作系统更新，安装，531–532
概述，525
所有权，文件和目录，537
PAMs，533–536
密码，532–536
权限，更改，537–538
权限，列表，577–579
权限，查看，577



- 安全，主机（续）
- 权限，设置默认值，538–539
- 权限，setuid，539–540
- 安全审查，576–580
- 影子密码，532–533
- 签名文件，541–549
- 测试工具，588
- 安全，网络。另见 防火墙
- 应用网关，527，564–565
- 禁用服务，552–555
- Internet 服务，551–555
- OpenSSH，555–557
- 概述，526
- 远程登录，555–557
- 安全审查，580–583
- SSH，555–557
- 独立服务器，禁用，551–552
- 独立服务器，审查，581–582
- TCP wrapper，554–555
- 测试工具，585–588
- xinetd 服务器，552–555，580–581
- 安全，测试方法
- 检测，574
- 主机安全审查，576–580
- 事件响应，579–580
- 网络审查，580–583
- 密码，579
- 渗透测试，582–583
- 权限，577–579
- 端口扫描，583
- 预防，573
- 过程描述，573
- 响应，574
- 影子密码，579
- 独立服务器，审查，581–582
- 漏洞，574–576
- 漏洞扫描器，583
- xinetd 服务器，580–581

- 安全，测试工具
- 主机安全，588
- Nessus 安全扫描器，585–588
- 网络安全，585–588
- nmap，584–585
- 端口扫描，584–585
- SAINT，588
- SARA，589
- 漏洞扫描，589
- 安全管理员集成网络工具（SAINT），588
- 安全审计员研究助手（SARA），589
- 安全级别配置工具，566–567
- 安全策略，520–521，523–524
- 段违规，60
- 分号（;），注释指示符，680
- sendmail 程序。另见 e-mail；邮件服务器
- 别名文件，657
- 配置文件，645–652
- 配置，642
- 在 DVD 上，812
- 文件，654–655
- .forward 文件，655–657
- m4 宏处理器，646–648
- 邮件投递机制，643–645
- 测试邮件投递，642–643
- sendmail 服务器，18
- sendmail.cf 文件语法，652–654
- sendmail.mc 文件，648–652
- 串行端口检测，301–302
- 串行设备名称，300–310
- ServerAdmin 指令，620
- Server 类安装，42
- ServerName 指令，620，621
- ServerRoot 指令，621
- 服务器。另见 特定服务器的条目
- 服务配置实用程序，605–606
- setuid 程序，529

设置代理，73–78
影子密码，532–533，579
共享库，762–768
共享文件
NFS，697–702
使用 NFS，445–447，697–702
概述，23–24
shell 命令，94。另见 Bash shell，shell 命令
shell 脚本
Bash 内置命令，777–780
调用函数，773–774
流程控制，774–776
概述，158–160，769–772
Perl，784–785
存储变量，772–773
shells。另见 Bash shell
访问，141–142
定义，13，713
快捷方式。另见 链接
关闭，96，400
signal 11 错误消息，60
签名文件，541–549
SIGSEGV，故障排除，60
简单邮件传输协议（SMTP），313，598
简单网络管理协议（SNMP），313，598
草图。另见 OpenOffice.org Draw
斜杠（/），根目录指示符，161
斜杠星号（/*...*），注释指示符，678
斜杠斜杠（//），注释指示符，678
幻灯片。另见 OpenOffice.org Impress
SMTP（简单邮件传输协议），313，598
嗅探数据包，341–342

SNMP（简单网络管理协议），313，598
套接字，594–597
软件开发。另见 C 编程；Perl 编程
编译器，714
计算机程序，定义，714
调试器，714，727–734
表达式，715
流程控制语句，715
函数，715
链接编译文件 另见 makefiles
宏，723–724
目标代码，714
概述，18–19
编程基础，714–715
例程，715
语句，715
子程序，715
变量，715，723–724
软件开发，makefiles
创建，725–727
示例，724–725
名称，721
概述，721–722
软件开发，工具
C 编译器，716–720
C++ 编译器，716–720
在 DVD 上，812
GCC，716–720
make 实用程序，720–727
摘要，715–716
sort 命令，157
排序文件，157
声音，配置，510
声音卡
安装 Red Hat Linux，31
概述，23
设置，64–65

声音文件，播放，194–196
声音，测试，75
源 RPM（SRPMS），安装，475
特效，Impress，270–273
拼写检查器，183–184
split 命令，158
打印作业排队，487–488
电子表格，16。另见 应用程序，办公；OpenOffice.org Calc
SRPMS（源 RPM），安装，475
SSH（安全 Shell），555–557
Stallman，Richard，13
独立服务器
    常见服务，列表，606–610
    禁用，551–552
    审查，581–582
    启动时自动启动，603–606
    手动启动/停止，602–603
标准头文件，761–762
StarOffice，17，182
Start 按钮。另见 K 按钮；Red Hat 按钮
启动
    Apache Web 服务器，615–617
    Bash shell，93–94
    GNOME 小程序，80，82
    INN，664–665
    KDE 小程序，129
    内核配置工具，497–498
    邮件服务器，642
    Mozilla，Web 浏览器，365
    sendmail，642
    服务器，启动时，408–409
    独立服务器，启动时自动，603–606
    独立服务器，手动，602–603
启动/停止服务器，408–409
StartServers 指令，621
启动，系统管理，400
启动脚本，407–408
语句，定义，715。另见 特定语句的条目
状态栏，Mozilla，368–369
stderr，重定向，145
stdin，重定向，145
stdout，重定向，145
停止
    进程，155
    服务器，408–409
独立服务器，手动，602–603
结构，745–748
样式，文档，235–239
su 命令，154，401
子程序，715，801–802
订阅新闻组，386
文件中替换字符，157–158
Sun Microsystems，17，182
超级用户。另见 root 用户
switch C 语句，757–758
对称 DSL（SDSL），290
对称密钥加密，529
syslogd 配置文件，549
系统活动，显示，95
系统管理。另见 root 用户；特定任务的条目
    常见任务，399–400
    概述，21–24
系统函数，798
系统信息，查看，418–421
"System is too big" 错误，513
系统运行时间，显示，94
系统使用摘要，416–417

## T
- TAO（Track-At-Once）方法，201
- TCP wrapper，554–555
- tcpdump 命令，341–342
- TCP/IP，594–597
- TCP/IP，配置文件
- /etc/host.conf，335
- /etc/hosts，334
- /etc/hosts.allow，336
- /etc/hosts.deny，336–337
- /etc/networks，334
- /etc/nsswitch.conf，337
- /etc/resolv.conf，335
- NSS，337
- 摘要表，333–334
- TCP/IP，局域网。另见 LANs（局域网），TCP/IP
- TCP/IP，网络
- 启动时配置，342
- 转储数据包头，341–342
- 在 DVD 上，812
- 主机连接性，检查，339
- IP 路由表，检查，338
- 网络接口，检查，337–338
- 网络状态，检查，339–341
- 嗅探数据包，341–342
- tcp_wrappers 选项，637
- 电话支持，503–504
- TELNET
- 定义，313
- 在 DVD 上，812
- 端口号，598
- 模板，文档，235–239
- 终端窗口，141–142
- test 命令，774–775
- 测试
- 主机安全，588
- 内核升级，493
- 邮件投递，642–643
- 调制解调器，302–304
- 网络安全，585–588
- 新闻组，667
- NIS，695–696
- Samba，707
- 安全渗透，582–583 另见 security，test methodology；security，test tools
- 声音，75
- TeX，在 DVD 上，812
- 文本编辑器
- 在 DVD 上，812
- ed，211–214
- vi，214–219
- 文本格式化软件，在 DVD 上，812
- 文本模式安装，56
- TFTP（Trivial File Transfer Protocol），313，598
- 主题
- GNOME，85
- KDE，91–92
- Mozilla，370–372
- thickwire，315–316
- thinwire，315–316
- 安全威胁
- 定义，529
- 列表，522
- 波浪号（~），主目录指示符，167
- 时间。另见 日期和时间
- 时区，设置，49–50，75
- Timeout 指令，621
- 工具提示
- Draw，280
- Writer，229
- top 实用程序，412–414
- tr 命令，157–158
- Track-At-Once（TAO）方法，201
- TransferLog 指令，622
- 传输文件。另见 文件传输



## U

传输层, 310
Tripwire 程序, 549
平凡文件传输协议 (TFTP), 313, 598
特洛伊木马, 529
故障排除
黑屏, 57–59, 75
从启动磁盘启动, 59
Calibrating delay loop... 消息, 74
DVD, 812
打印问题, 490
段违规, 60
signal 11 错误消息, 60
SIGSEGV, 60
"System is too big" 错误, 513
无法重新启动, 516
X 环境, 57–59, 75
two greater than (2>)，I/O 重定向, 145
类型定义, 747–748
类型限定符, 748
typedef 关键字, 747–748
TypesConfig 指令, 626–627
排版软件，在 DVD 上, 812

UDP (用户数据报协议), 595
umask 命令, 538–539
umount 命令, 175, 443
uname 命令, 95
未经授权的访问, 522
未经授权的信息披露, 522
统一资源定位符 (URLs), 361–363
联合体, 745–748
协调世界时 (UTC), 50

通用串行总线 (USB), 23, 300–310, 485–487
UNIX 实用程序，在 DVD 上, 812
unless 语句, 794–795
卸载文件系统, 443
升级代理, 476–478
升级
应用程序, 476–478
内核, 492–493
软件包, 469, 476–478
上传文件。参见文件传输
uptime 命令, 94, 414–416
运行时间统计, 414–416
URLs (统一资源定位符), 361–363
USB (通用串行总线), 23, 300–310, 485–487
USB 支持, 511–512
Usenet。参见 INN (InterNetNews)；新闻组
用户账户
列表, 431–432
修改, 431
用户账户，添加/删除
到现有系统, 428–430
在安装时, 65–67
系统管理, 399
使用用户管理器, 428–430
使用 useradd 命令, 430–431
使用 userdel 命令, 431
用户数据报协议 (UDP), 595
User 指令, 621
用户环境，探索, 434–436
用户界面
GNOME, 79–82
KDE, 88–92
用户管理器, 428–430
useradd 命令, 430–431
userdel 命令, 431

`UserDir` 指令, 623
`userlist_deny` 选项, 637
`usermod` 命令, 431
`/usr` 子目录, 164-165
UTC (协调世界时), 50

## V

$^V (美元符号，插入符号)，Perl 变量, 789
Valade, Janet, 190
`/var` 子目录, 165
变量, 715, 723-724
变量，C 编程, 743-744
变量，Perl
别名, 808
概述, 786-789
预定义, 789
`/var/named/localhost.zone` 文件, 684-685
`/var/named/named.ca` 文件, 683-684
`/var/named/named.local` 文件, 685
验证 RPM 软件包, 469-470
版本号
内核, 12, 95
概述, 11-12
获取 RPM 软件包, 465
竖线 (|)，管道字符, 144, 800-801
`vi`, 214-219
显卡, 31
查看
文件和文件夹, 132-135
网页, 136
虚拟控制台, 141-142
虚拟桌面
GNOME, 80
KDE, 126
虚拟主机设置, 629-632
病毒, 530
VistaSource, 182
`vmstat` 实用程序, 416-417
`void` 类型, 760
volatile 限定符, 748
`vsftpd` 服务器, 18, 635
漏洞
在线资源, 574
审查, 574-576
扫描工具, 589
安全, 522-523, 530
漏洞扫描器, 583

## W

壁纸
GNOME, 84, 117
KDE, 91, 138-139
看门狗卡, 508
`wc` 命令, 156-157
天气小程序, 81
Web。另请参见 Internet；新闻组；
在线资源
地址 参见 URLs
超链接, 361-363
链接, 361-363
概述, 359-361
URLs, 361-363
Web 浏览器。另请参见 Konqueror；
Mozilla
Epiphany, 365
文件传输, 391-392
和 Web 服务器, 363-364
创建网页
HTML, 373-375
Mozilla Composer, 375-378
概述, 372-373
查看网页, 136
Web 服务器。另请参见 Apache Web 服务器
定义, 360
和 Web 浏览器, 363–364
WEP (有线等效保密), 323–324
which 命令, 782–783
while
C 语句, 758–759
Perl 语句, 795–796
通配符
DOS 文件系统, 460
shell 命令, 146–148
wildmat 模式, 662
窗口，移动和调整大小, 80
Windows 资源管理器。参见 Konqueror；Nautilus shell
Windows 服务器，设置, 702–707
有线等效保密 (WEP), 323–324
文字处理, 16。另请参见 应用程序，办公
工作站级安装, 42
万维网。参见 Web
蠕虫, 530
write_enable 选项, 637
Writer。参见 OpenOffice.org Writer

Web 服务器。另请参见 Apache Web 服务器
定义, 360
和 Web 浏览器, 363–364
WEP (有线等效保密), 323–324
which 命令, 782–783
while
C 语句, 758–759
Perl 语句, 795–796
通配符
DOS 文件系统, 460
shell 命令, 146–148
wildmat 模式, 662
窗口，移动和调整大小, 80
Windows 资源管理器。参见 Konqueror；Nautilus shell
Windows 服务器，设置, 702–707
有线等效保密 (WEP), 323–324
文字处理, 16。另请参见 应用程序，办公
工作站级安装, 42
万维网。参见 Web
蠕虫, 530
write_enable 选项, 637
Writer。参见 OpenOffice.org Writer

## Χ

x= (x 等于)，字符串复制运算符, 790
X 环境，故障排除, 57–59
x 等于 (x=)，字符串复制运算符, 790
802.11x 以太网标准, 322
X 多媒体系统 (XMMS), 194–196
XF86Config 文件，创建, 58–59
xferlog_enable 选项, 637
xferlog_file 选项, 637
xferlog_std_format 选项, 637
Ximian Evolution, 348–353
xinetd 服务器
禁用服务, 552–555
网络安全, 552–555
概述, 599–602
安全测试方法, 580–581
XMMS (X 多媒体系统), 194–196

## Υ

ypcat 命令, 696
ypmatch 命令, 696
yppasswd 命令, 694
yppoll 命令, 696
ypwhich 命令, 695

## Z

区域文件格式, 679–680

## Notes

## Notes

## Notes

## GNU GENERAL PUBLIC LICENSE

版本 2，1991 年 6 月
版权所有 © 1989, 1991 Free Software Foundation, Inc.
59 Temple Place - Suite 330, Boston, MA 02111-1307, USA

任何人均可复制和分发本许可证文件的逐字副本，但不得更改。

### 前言

大多数软件的许可证旨在剥夺您共享和更改它的自由。相比之下，GNU 通用公共许可证旨在保证您共享和更改自由软件的自由——确保软件对所有用户都是自由的。本通用公共许可证适用于自由软件基金会的大多数软件以及任何作者承诺使用它的其他程序。 （自由软件基金会的某些其他软件受 GNU 库通用公共许可证的约束。）您也可以将其应用于您的程序。

当我们谈论自由软件时，我们指的是自由，而不是价格。我们的通用公共许可证旨在确保您有权分发自由软件的副本（如果您愿意，可以收取此服务的费用），您会收到源代码或如果您想要可以获得它，您可以更改软件或将其部分用于新的自由程序；并且您知道您可以这样做。

为了保护您的权利，我们需要做出限制，禁止任何人剥夺您的这些权利或要求您放弃这些权利。如果您分发软件的副本或对其进行修改，这些限制会转化为您必须承担的某些责任。

例如，如果您分发此类程序的副本，无论是免费还是收费，您必须向收件人提供您所拥有的所有权利。您必须确保他们也收到或可以获得源代码。您还必须向他们展示这些条款，以便他们知道自己的权利。

我们通过两个步骤保护您的权利：（1）对软件进行版权保护，（2）向您提供本许可证，该许可证授予您合法许可复制、分发和/或修改软件。

此外，为了保护每位作者和我们的利益，我们希望确保每个人都理解本自由软件没有任何担保。如果软件被他人修改并传递下去，我们希望其收件人知道他们拥有的不是原件，这样他人引入的任何问题都不会影响原作者的声誉。

最后，任何自由程序都不断受到软件专利的威胁。我们希望避免分发自由程序的人单独获得专利许可，从而使程序成为专有程序的危险。为此，我们已明确表示，任何专利必须对所有人免费使用，或根本不许可。

复制、分发和修改的具体条款和条件如下。



## 复制、分发和修改的条款和条件

0. 本许可证适用于任何包含版权持有者放置的通知的程序或其他作品，该通知声明其可根据本通用公共许可证的条款分发。下文中的“Program”指任何此类程序或作品，而“基于 Program 的作品”指 Program 或根据版权法产生的任何衍生作品：也就是说，包含 Program 或其一部分的作品，无论是逐字复制还是经过修改和/或翻译成另一种语言。（此后，翻译在“修改”一词的范围内不受限制。）每个被许可人都称为“you”。

复制、分发和修改之外的活动不属于本许可证的涵盖范围；它们超出其范围。运行 Program 的行为不受限制，而 Program 的输出仅在其实质构成基于 Program 的作品时才受涵盖（无论该输出是否由运行 Program 产生）。是否如此取决于 Program 的功能。

1. 你可以复制和分发 Program 源代码的逐字副本，就像你收到的那样，任何媒介均可，前提是你显著且恰当地在每份副本上公布适当的版权声明和免责声明；保持所有提及本许可证及无任何担保的声明完整；并向 Program 的任何其他接收者提供本许可证的副本以及 Program。

你可以就转移副本的实际行为收取费用，并且可自行选择提供担保保护并收取费用。

2. 你可以修改你的一份或多份 Program 副本或其任何部分，从而形成基于 Program 的作品，并在上述第 1 节的条款下复制和分发此类修改或作品，前提是你同时满足以下所有条件：

- a) 你必须使修改过的文件带有显著的声明，说明你更改了文件以及任何更改的日期。
- b) 你必须使你分发或出版的任何作品，如果其全部或部分包含或源自 Program 或其任何部分，则必须作为一个整体无偿地以本许可证的条款许可给所有第三方。
- c) 如果修改后的程序在运行时通常以交互方式读取命令，你必须使其在以最普通的方式启动进行此类交互使用时，打印或显示一份公告，其中包括适当的版权声明和声明其无担保的通知（或声明你提供担保），并说明用户可在这些条件下重新分发该程序，以及告知用户如何查看本许可证的副本。（例外：如果 Program 本身是交互式的但通常不打印此类公告，则基于 Program 的你的作品无需打印公告。）

这些要求适用于修改后的作品整体。如果该作品的可识别部分并非源自 Program，并且可以合理地视为独立且分开的作品，则本许可证及其条款在你将这些部分作为独立作品分发时不适用于这些部分。但当你将同一部分作为基于 Program 的整体作品的一部分分发时，整体的分发必须遵守本许可证的条款，其对其他被许可人的许可延伸至整个整体，从而延伸至每个部分，无论谁撰写了它。

因此，本节的意图并非主张权利或质疑你对完全由你撰写的作品的权利；其意图是行使控制基于 Program 的衍生作品或集合作品分发的权利。

此外，将另一部并非基于 Program 的作品与 Program（或基于 Program 的作品）一起聚合在存储或分发介质的卷上，并不使该另一作品落入本许可证的范围。

3. 你可以在对象代码或可执行形式下复制和分发 Program（或根据第 2 节基于它的作品），在上述第 1 节和第 2 节的条款下，前提是你同时执行以下一项：

- a) 连同完整的对应机器可读源代码一起提供，该源代码必须在通常用于软件交换的介质上根据上述第 1 节和第 2 节的条款分发；或，
- b) 连同一份书面要约一起提供，该要约有效期至少为三年，向任何第三方提供一份完整的对应源代码的机器可读副本，费用不超过你实际执行源代码分发所花费的成本，该源代码必须在通常用于软件交换的介质上根据上述第 1 节和第 2 节的条款分发；或，
- c) 连同你收到的关于分发对应源代码的要约的信息一起提供。（此替代方案仅允许非商业分发，并且仅在你以对象代码或可执行形式收到该程序并附带该要约时才允许，符合上述 b 小节。）

作品的源代码是指用于对其进行修改的首选形式。对于可执行作品，完整源代码是指其包含的所有模块的所有源代码，加上任何相关的接口定义文件，加上用于控制可执行文件的编译和安装的脚本。然而，作为特别例外，分发的源代码无需包含通常随可执行文件运行的操作系统的主要组件（编译器、内核等）一起分发（以源代码或二进制形式）的任何内容，除非该组件本身随可执行文件一起提供。

如果通过提供从指定位置复制的访问权限来分发可执行文件或对象代码，则从同一位置提供复制源代码的等效访问权限即视为分发源代码，即使第三方并非必须连同对象代码一起复制源代码。

4. 除本许可证明确规定外，你不得复制、修改、再许可或分发 Program。任何其他复制、修改、再许可或分发 Program 的尝试均属无效，并将自动终止你在本许可证下的权利。然而，只要这些方完全遵守规定，你从你处收到副本或权利的各方不会因此终止其许可证。

5. 你并非必须接受本许可证，因为你并未签署它。然而，除此之外没有任何内容授予你修改或分发 Program 或其衍生作品的许可。如果不接受本许可证，这些行为在法律上被禁止。因此，通过修改或分发 Program（或基于 Program 的任何作品），你表示接受本许可证这样做，并接受复制、分发或修改 Program 或基于它的作品的所有条款和条件。

6. 每次你重新分发 Program（或基于 Program 的作品），接收者自动从原始许可人处获得许可，可根据这些条款和条件复制、分发或修改 Program。你不得对接收者行使本许可授予的权利施加任何进一步限制。你不对第三方遵守本许可证负责。

7. 如果由于法院判决或专利侵权指控或任何其他原因（不限于专利问题）而对你施加的条件（无论是法院命令、协议或其他）与本许可证的条件相矛盾，它们并不能使你免于本许可证的条件。如果你无法同时满足本许可证的义务和任何其他相关义务，则作为后果，你不得分发 Program。例如，如果专利许可不允许所有直接或间接通过你收到副本的人免版税重新分发 Program，则你唯一能同时满足它和本许可证的方法就是完全停止分发 Program。

如果本节的任何部分在特定情况下被认定为无效或不可执行，则该节的其余部分仍应适用，而该节整体仍应在其他情况下适用。

本节的目的并非诱使你侵犯任何专利或其他财产权利主张或质疑任何此类主张的有效性；本节的唯一目的是保护通过公共许可实践实现的自由软件分发系统的完整性。许多人依赖该系统的一致应用，对通过该系统分发的广泛软件作出了慷慨贡献；作者/捐赠者自行决定是否愿意通过任何其他系统分发软件，而被许可人不得强加该选择。

本节旨在彻底阐明据信是本许可证其余部分的后果。

8. 如果 Program 的分发和/或使用在某些国家因专利或受版权保护的接口而受到限制，则将 Program 置于本许可证下的原始版权持有者可以添加明确的地理分发限制，排除这些国家，以便仅在未被如此排除的国家或国家之间允许分发。在这种情况下，本许可证被视为已将该限制纳入许可证正文。

9. 自由软件基金会可以不时发布通用公共许可证的修订版和/或新版本。此类新版本在精神上将与本版本相似，但在细节上可能有所不同，以解决新问题或关切。 Such new versions will be similar in spirit to the present version, but may differ in detail to address new 版本在精神上将与本版本相似，但在细节上可能有所不同，以解决新问题或关切。

每个版本都分配有区别的版本号。如果 Program 指定了适用于它的本许可证的版本号以及“任何后续版本”，则你可以选择遵循该版本的条款和条件，或自由软件基金会发布的任何后续版本的条款和条件。如果 Program 未指定本许可证的版本号，则你可以选择自由软件基金会发布的任何版本。

10. 如果你希望将 Program 的部分纳入分发条件不同的其他自由程序中，请写信给作者请求许可。对于由自由软件基金会版权所有的软件，请写信给自由软件基金会；我们有时会为此作出例外。我们的决定将以保持我们自由软件所有衍生作品的自由状态以及促进软件的共享和再利用为指导目标。




## 无担保

11. 由于程序是免费许可的，在适用法律允许的范围内，程序不提供任何担保。除非另有书面说明，版权持有人和/或其他方按“按原样”提供程序，不提供任何形式的担保，无论是明示还是暗示，包括但不限于适销性和特定用途适用性的暗示担保。程序质量和性能的全部风险由您承担。如果程序被证明有缺陷，您承担所有必要的维护、修理或更正费用。

12. 除非适用法律要求或另有书面约定，任何版权持有人，或任何根据上述规定可修改和/或重新分发程序的其他方，均不对您因使用或无法使用程序而产生的损害承担责任，包括任何一般性、特殊性、偶发性或后果性损害，该等损害源于使用或无法使用程序，包括但不限于数据丢失或数据不准确、您或第三方遭受的损失，或程序无法与其他程序一起运行，即使该持有人或其他方已被告知此类损害的可能性。

## 条款和条件结束

更多信息，请访问 www.gnu.org/copyleft/gpl.html.

## Wiley Publishing, Inc.
### Linux CD 邮寄兑换券

如果您无法使用配备 DVD 驱动器的 PC，我们以少量运费和材料费提供完整套装的 CD-ROM。如果您希望我们将 CD 寄给您，请：

- 1. 填写此优惠券。
- 2. 注明您购买本书的地点和购买日期。
- 3. 附上 $12（美国资金）的支票或汇票，用于在美国境内发货的订单，或 $20（美国资金）用于美国境外订单。
- 4. 将其寄至优惠券底部列出的地址。

姓名 _________________________
公司 _________________________
地址 _________________________
城市 _________________________ 州 ______ 邮政编码 __________
国家 _________________________
电子邮件 _________________________ 电话 __________

**请将此优惠券连同适当的美元资金退回至：**
Attn: Media Development
Red Hat Linux Fedora All-in-One 0764542583 Fulfillment
Wiley Publishing, Inc.
10475 Crosspoint Blvd.
Indianapolis, IN 46256

**条款：** 在法律禁止或限制的地区无效。交付需时 2-4 周。Wiley 对丢失、被盗、迟到或难以辨认的订单不承担责任。有关此履行优惠的任何问题，请通过电子邮件发送至 MediaDev@wiley.com。
