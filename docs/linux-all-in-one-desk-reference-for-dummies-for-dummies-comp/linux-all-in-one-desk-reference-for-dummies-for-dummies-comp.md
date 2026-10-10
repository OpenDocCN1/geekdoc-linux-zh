# 《Linux 全合一指南 新手入门手册》





![](img/11709a8f88c8cd03868a929dc94c0e2b_3_0.png)

# 作者简介

**Naba Barkakati** 是一位电气工程师，也是一位成功的计算机书籍作者，在从 MS-DOS 和 Windows 到 UNIX 和 Linux 的多种系统中拥有丰富的经验。1984年，他从马里兰大学学院分校（College Park）获得电气工程博士学位后，购买了人生第一台个人电脑——IBM PC-AT。在从事全职工程工作的同时，Naba 梦想为新兴的 PC 软件市场编写软件。幸运的是，他没有像微软那样建立软件帝国，而是最终撰写了成功的计算机书籍。目前，Naba 是美国政府问责办公室（GAO）技术与工程中心的资深技术员。

过去15年里，Naba 撰写了超过25本计算机书籍，主题涵盖从 C++ Windows 编程到 Linux。他著有多部畅销书，如《The Waite Group's Turbo C++ Bible》（威特团 Turbo C++ 圣经）、《Object-Oriented Programming in C++》（C++ 面向对象编程）、《X Window System Programming》（X 窗口系统编程）、《Visual C++ Developer's Guide》（Visual C++ 开发者指南）、《Borland C++ 4 Developer's Guide》（Borland C++ 4 开发者指南）和《Linux Secrets》（Linux 内幕）。他的书被翻译成多种语言，包括西班牙语、法语、波兰语、希腊语、意大利语、中文、日语和韩语。Naba 最新的书是《Red Hat Fedora Linux Secrets》（红帽 Fedora Linux 内幕），同样由威立出版社，股份有限公司出版。

Naba 与妻子 Leha 以及女儿 Ivy、Emily 和 Ashley 住在美国马里兰州的北波托马克（North Potomac）。

# 献词

我想将这本书献给我的妻子 Leha，以及我的女儿 Ivy、Emily 和 Ashley。

# 作者致谢

我要感谢 Terri Varveris 让我启动了这本书——这是一套关于 Linux 的八本快速参考指南，重点介绍了几个主要的 Linux 发行版。作为项目编辑，Christopher Morris 指导我完成了手稿提交流程，并推动各项工作进展。我很感激 Terri 和 Chris 在这个项目中给予我的指导和支持。

我要感谢 Jason Luster 审阅手稿的技术准确性，并提出了许多改进书籍内容的有用建议。

感谢威立出版社的所有人，将我的初稿手稿变成了这本编辑精良、包装精美的书籍。

当然，如果没有 Linux，这本书就没有存在的理由。为此，我们要感谢 Linus Torvalds 和全球无数的 Linux 开发者。最后，一如既往，我最大的感谢献给我的妻子 Leha 和我们的女儿 Ivy、Emily 和 Ashley——是她们对我的爱和支持让我继续前行。谢谢你们一直在那里！

# 出版方致谢

我们为这本书感到自豪；请通过我们在 www.dummies.com/register/ 的在线注册表单向我们发送您的评论。

帮助推出这本书的一些人包括：

## 获取、编辑和媒体开发
- **项目编辑：** Christopher Morris
- **获取编辑：** Terri Varrvers
- **校对编辑：** Heidi Unger
- **技术编辑：** Dan DiNicolo
- **编辑经理：** Kevan Kirschner
- **版权编辑：** Laura Moss
- **媒体开发专员：** Travis Silvers
- **媒体开发经理：** Laura VanWinkle
- **媒体开发主管：** Richard Graves
- **编辑助理：** Amanda Foxworth
- **漫画：** Rich Tennant (www.the5thwave.com)

## 排版服务
- **项目协调员：** Erin Smith
- **版式和图形：** Andrea Dahl, Denny Hager, Melanee Prendergast, Heather Ryan, Erin Zeltner
- **校对人员：** Vicki Broyles, Joe Niesen
- **索引编制者：** Johnna VanHoose

## 技术类“新手版”出版与编辑
- **Richard Swadley**，副总裁兼执行集团出版人
- **Andy Cummins**，副总裁兼出版人
- **Mary Bednarek**，执行获取总监
- **Mary C. Corder**，编辑总监

## 消费者类“新手版”出版
- **Diane Graves Steele**，副总裁兼出版人
- **Joyce Pepple**，获取总监

## 排版服务
- **Jerry Fahey**，生产服务副总裁
- **Debbie Stalley**，排版服务总监




## 引言

当你考虑到 Linux 的起源及其持续演化的方式时，它确实令人惊叹。从作为芬兰人 **Linus Torvalds** 的业余爱好这一谦逊起点开始，Linux 已发展成为一个成熟的操作系统，其特性可与任何商业 UNIX 操作系统相媲美。更棒的是，Linux——包括其所有源代码——对任何人都是免费提供的。你只需要从互联网站点下载它，或者以象征性的费用从众多 Linux CD 供应商那里通过 CD 或 DVD 获取即可。

Linux 确实打破了“一分钱一分货”的规则。尽管 Linux 是免费的，但在性能、特性和可靠性方面，它绝不起眼。Linux 的健壮性与其开发和更新方式有关。世界各地的许多开发人员协作添加特性。用户持续下载增量版本并在各种系统配置中进行测试。Linux 版本经历的 beta 测试比任何商业软件都严格得多。

自 1994 年 3 月 14 日发布 Linux 内核 1.0 以来，全球 Linux 用户数量呈指数级增长。许多 Linux 发行版——操作系统与应用程序及安装工具的组合——已被开发出来，以简化和使用安装过程。一些 Linux 发行版是商业销售并提供支持的，而许多仍保持免费可用。

与许多免费软件不同，Linux 附带了大量在线信息，涉及为各种 PC 和外围设备安装和配置操作系统等主题。一小部分核心 Linux 用户仅凭在线文档就能熟练有效地使用 Linux。然而，绝大多数用户却带着某种特定目的（例如设置 Web 服务器或学习 Linux）转向 Linux。此外，大量的 Linux 用户在家中使用他们的系统。对于这些新用户来说，在线文档并不易用，且文档通常未涵盖用户可能想到的 Linux 的具体用途。

如果你刚开始使用 Linux，你需要一本实用指南，不仅要指导你完成 Linux 的安装和设置，还要展示如何使用 Linux 完成特定任务，例如设置 Web 服务器或开发软件。你可能还想在最终选定一个喜欢的发行版之前，先尝试不同的 Linux 发行版。

## 关于本书

相应地，《Linux 全方位桌面参考傻瓜书》（*Linux All-in-One Desktop Reference For Dummies*）附带一张 DVD，其中包含七个不同的 Linux 发行版——Debian GNU/Linux 3.1r0、Fedora Core 5、Knoppix 4.0.2、MEPIS 3.3.1、SUSE Linux 10.0、Ubuntu 5.04 以及 Xandros 3.02 公开流通版——以及安装和使用其中任何一个发行版的说明。（*提示：* 你可以直接使用本书 DVD 上的 Knoppix Live CD 来快速、无风险地体验 Linux。）

《Linux 全方位桌面参考傻瓜书》（*Linux All-in-One Desk Reference For Dummies*）在一本书中为你提供了八份不同的快速参考指南。综合起来，这八个小册子提供了关于安装、配置和使用 Linux 的详细信息。

你会最喜欢这本书的一点是，你不必按章节顺序阅读，甚至不必按章节中的部分阅读。你完全可以翻到你想看的话题，快速找到关于 Linux 的紧迫问题的答案，无论是关于使用 OpenOffice.org 文字处理软件还是设置 Apache Web 服务器。

以下是你可以使用这本书做的部分事情：

- 从随书附带的 DVD-ROM 安装和配置 Linux——Debian、Fedora Core、Knoppix、MEPIS、SUSE、Ubuntu 或 Xandros。（你只需从 DVD 启动即可使用 Knoppix。）
- 通过 DSL 或电缆调制解调器将 Linux PC 连接到互联网。
- 使用 PPP 设置拨号网络。
- 在你的现有网络中添加无线以太网。
- 获取针对 Linux 特定用途的技巧、技术和快捷方式，例如：
  - 设置和使用互联网服务：Web、邮件、新闻、FTP、NFS 和 DNS。
  - 使用 Samba 设置 Windows 服务器。
  - 使用 Linux 命令。
  - 在 Linux 上使用 Perl、shell 和 C 进行编程。
  - 使用 OpenOffice.org 办公套件及 Linux 附带的其他应用程序。
- 理解系统和网络基础安全。
- 执行系统管理任务。

## 本书使用的约定

我在本书中使用简单的符号风格。所有清单、文件名、函数名、变量名和关键字均以*等宽*字体排版，以便于阅读。我会将新术语和概念的首次出现*斜体*表示，并在那里直接提供定义。我使用**粗体**显示键入的命令。命令的输出和任何文件列表均以等宽字体显示。

## 你不必阅读的部分

每本迷你参考书都专注于特定的任务领域——例如使用互联网或运行互联网服务器——然后提供有关如何执行一系列相关任务的动手指导说明。你可以直接跳转到某一部分，阅读特定任务。你除了阅读与你问题相关的几段文字或步骤列表外，不必阅读其他内容。使用目录或索引来查找与你问题相关的页面。

你可以安全地忽略技术内容图标旁边的文本以及边栏。然而，如果你是那种喜欢了解 Linux 工作原理的一些隐藏细节的人，那就尽去挖掘技术内容图标和边栏吧。

## 你是谁？

我假设你对 PC 有些许熟悉——你知道如何开机和关机，并且已经玩过 Windows。考虑到大多数新的 PC 都预装了 Windows，这个假设应该是安全的，对吧？并且你知道如何使用一些 Windows 应用程序，例如 Microsoft Office。

在 PC 上安装 Linux 时，你可能希望保留你的 Windows 2000 或 Windows XP 安装。我假设你并不介意缩小 Windows 分区以为 Linux 腾出空间。为此，你可以使用本书配套 DVD 上 Knoppix 附带的*分区*实用程序，或者投资购买一个良好的磁盘分区工具，例如 Symantec 的 Norton PartitionMagic，可在 www.powerquest.com/partitionmagic 获取。（不，我与 Symantec 没有任何关系。）

我还假设你愿意接受尝试安装 Linux 时某些事物可能无法正常工作这一风险。如果你有一些不常见的硬件类型，可能会出现问题。如果你担心破坏系统，请尝试找一台稍旧的备用 Pentium PC 进行牺牲，然后在该 PC 上安装 Linux。或者，直接使用随本书附带的 DVD 运行 Knoppix。




## 4. 本书的组织结构

《Linux 一站式桌面参考（Linux All-in-One Desk Reference For Dummies）》包含八本分册（minibooks），每本分册都聚焦于少量相关主题。如果您正在查找特定主题的信息，请查看书脊上的分册名称或查阅目录。

这本桌面参考书从一本解释 Linux 基础知识并指导您完成安装过程的（非常实用，因为通常您购买的电脑不会预装 Linux）分册开始。第二本分册充当 Linux 用户指南——它专注于探索 Linux 工作站的各个方面，包括 GNOME 和 KDE 图形用户界面以及许多与 Linux 捆绑提供的应用程序。第三本分册涵盖网络内容，第四本分册深入介绍互联网的使用。第五本分册介绍系统管理。第六本分册转向保护 Linux 系统及其相关网络这一重要主题。第七本分册展示如何运行各种互联网服务器，从邮件服务器到 Web 服务器。第八本也是最后一本分册，向您介绍编程。

以下是这八本分册及其内容的快速概览：

-   **第一册：Linux 基础：** 什么是 Linux？理解 Linux 2.6 内核中的新特性。安装、配置和故障排除不同的 Linux 发行版（Debian、Fedora Core、Knoppix、MEPIS、SUSE、Ubuntu 和 Xandros）。对 Linux 进行试用。
-   **第二册：Linux 桌面：** 探索 GNOME 和 KDE。使用 shell（到底什么是 shell？）。导航 Linux 文件系统。探索应用程序，如多媒体软件以及文本编辑器（*vi* 和 *emacs*）。
-   **第三册：网络：** 通过拨号连接或高速始终在线连接（如 DSL 或电缆调制解调器）将 Linux PC 连接到互联网。配置和管理 TCP/IP 网络，包括无线网络。
-   **第四册：互联网：** 使用各种互联网服务，如电子邮件、网页浏览和阅读新闻组。使用 FTP 传输文件。
-   **第五册：管理：** 执行基本的系统管理。管理用户账户和文件系统。安装应用程序。使用设备和打印机。使用 USB 设备。升级和定制 Linux 内核。
-   **第六册：安全：** 理解网络和安全主机安全。保护主机和网络。执行安全审计。

### 边栏

有时，我会使用边栏来突出有趣但并非至关重要的信息。边栏解释您可能尚未接触过的概念，或提供相关主题的一些见解。如果您赶时间，可以安全地跳过边栏。

-   **第七册：互联网服务器：** 管理互联网服务。配置 Apache Web 服务器。设置 FTP 服务器。配置邮件和新闻服务器。提供 DNS。使用 NFS 进行文件共享。使用 Samba 设置 Windows 服务器。
-   **第八册：编程：** 了解编程基础。探索 Linux 中的软件开发工具。编写 shell 脚本。学习 C 和 Perl 编程。
-   **附录：关于 DVD：** 总结随书 DVD-ROM 的内容。

### DVD 上有什么？

DVD 包含七个 Linux 发行版——它是一张结合了 Fedora Core 4 和 Knoppix 的 DVD，其中包含一个名为 *distros* 的文件夹，里面有 Debian、Knoppix、MEPIS、SUSE、Ubuntu 和 Xandros 的 ISO 镜像文件，并按独立文件夹分类。您可以按照随软件提供的许可协议使用此 DVD。要了解 DVD 内容的更多信息，请参阅附录。

### 本书中使用的图标

遵循 *All-in-One Desk Reference For Dummies*（一站式桌面参考）系列久负盛名的传统，我使用图标帮助您快速定位有用信息。图标包括以下内容：

![](img/11709a8f88c8cd03868a929dc94c0e2b_30_0.png)

“特定发行版”图标指出适用于特定发行版的信息——即本书涵盖的 Debian、Fedora Core、Knoppix、MEPIS、SUSE、Ubuntu 和 Xandros。

![](img/11709a8f88c8cd03868a929dc94c0e2b_30_1.png)

“记住”图标标记一般性的有趣事实——一些您希望知道并记住的内容。

### 6. 接下来去哪里

![](img/11709a8f88c8cd03868a929dc94c0e2b_31_0.png)

“提示”图标标记您可以执行的操作，以使您的工作更轻松。

![](img/11709a8f88c8cd03868a929dc94c0e2b_31_1.png)

“警告”图标突出显示潜在的陷阱。使用此图标时，我是在告诉您：“小心！这可能会损害您的系统！”

![](img/11709a8f88c8cd03868a929dc94c0e2b_31_2.png)

“技术细节”图标标记可能对高级用户（或 aspire 成为高级用户的人）感兴趣的技术信息。

是时候开始您的 Linux 冒险之旅了。拿出 DVD 并安装 Linux——选择一个发行版，任意一个都行（只要是 Debian、Fedora Core、Knoppix、MEPIS、SUSE、Ubuntu 或 Xandros 即可）。然后，转到相关章节，让乐趣开始。使用目录和索引来确定您想去的地方。不知不觉间，您将成为 Linux 专家！

我希望您在使用本书时能像我撰写它时一样享受！

## 第一册：Linux 基础

《The 5th Wave》作者 Rich Tennant

![](img/11709a8f88c8cd03868a929dc94c0e2b_32_0.png)

#### 内容速览

- 第 1 章：介绍 Linux ................................................9
- 第 2 章：安装 Linux ............................................................31
- 第 3 章：Linux 故障排除与配置 ..................................81
- 第 4 章：试用 Linux ...........................................................111

## 第 1 章：介绍 Linux

###### 本章内容

- 解释什么是 Linux
- 浏览 Linux 发行版通常包含的内容
- 发现 Linux 能帮助您管理什么
- 入门指南

我敢打赌您听说过 Linux。如果您想知道 Linux 到底是什么以及它如何帮助您，本章将回答这些问题。在这里，我提供 Linux 的宏观图景，并告诉您如何立即开始使用它。

顺便说一下，本书涵盖适用于 Intel 80x86 和 Pentium 处理器的 Linux（基本上是可以运行任何版本 Windows 的任何 PC）。

### 什么是 Linux？

您知道您的 PC 是一堆硬件——像机箱、显示器、键盘和鼠标这些您可以触摸的东西。机箱包含最重要的硬件——*中央处理器*（CPU），即运行*软件*（任何告诉计算机如何执行您指令的程序）的微芯片，而这是您实际上无法触摸的。在典型的 Pentium 4 PC 中，Pentium 4 微处理器就是 CPU。机箱中的其他重要硬件包括内存（RAM 芯片）和硬盘——必须有一个程序来运行所有这些并使它们协调工作：即操作系统。

*操作系统*是管理所有硬件并根据您的命令运行其他软件的软件。您作为用户，通过点击菜单和图标或输入一些晦涩的文本来提供这些命令。Linux 是一个操作系统——就像 UNIX、Windows 98、Windows 2000 和 Windows XP 一样。Linux 操作系统以 UNIX 为模型；在其最基础、无装饰的形式下，Linux 操作系统也被称为 *Linux 内核*。

操作系统赋予任何计算机其个性。例如，您可以在 PC 上运行 Windows 98 或 Windows XP——在同样的 PC 上，您也可以安装并运行 Linux。这意味着，取决于任何特定时刻安装并运行的是哪个操作系统，同一台 PC 可以是 Windows 98、Windows XP 或 Linux 系统。

### Linux 真的能在任何计算机上运行吗？

Linux 运行在许多不同类型的计算机系统上——它似乎确实能够在几乎任何类型的计算机上运行。Linus Torvalds 和其他程序员最初是为 Intel 80x86（及兼容）系列处理器开发 Linux 的。如今，Linux 也可用于基于其他处理器的系统——例如带有 AMD 64 位 AMD64 处理器、Motorola 68000 系列、Alpha AXP、Sun SPARC 和 UltraSPARC、Hewlett-Packard HP PA-RISC、PowerPC 和 PowerPC64 处理器以及 MIPS R4x00 和 R5x00 的系统。最近，IBM 已为其 S/390 和 zSeries 大型机发布了其自己的 Linux 版本。本书涵盖适用于 Intel 80x86 和 Pentium 处理器的 Linux。（这些被称为 IA32 架构处理器，或 i386，因为它们支持 80386 处理器的指令集。）

操作系统的主要工作是将软件（计算机程序）从硬盘（或其他永久存储设备）加载到内存中，并使 CPU 运行这些程序。您使用计算机所做的一切都得益于操作系统，因此如果操作系统以某种方式出错，整个系统就会冻结。您知道当您的favorite操作系统——甚至可能是随您 PC 附带的那个操作系统——在您刚刚给好友写完长邮件准备点击发送按钮时突然崩溃是多么令人恼火。您尝试“三指问候”（按 Ctrl+Alt+Delete），但无济于事。然后就该按 Reset 按钮了（如果您的电脑制造商足够明智地包含了一个 Reset 按钮）。幸运的是，在 Linux 上这种情况几乎从不发生——它以非常可靠的操作系统而闻名。

用技术术语来说，Linux 是一个*多用户、多任务操作系统*。这意味着 Linux 允许多个用户登录，并且 Linux 可以同时运行多个程序。如今，几乎所有操作系统都是多用户和多任务的，但当 Linux 在 1994 年刚刚起步时，*多用户*和*多任务*是很大的卖点。

![](img/11709a8f88c8cd03868a929dc94c0e2b_35_0.png)

### Linux 发行版

一个 *Linux 发行版* 由 *Linux 内核*（操作系统）和一组应用程序组成，并附带一个易于使用的安装程序。顺便说一下，大多数人只需说 *Linux* 来指代特定的 Linux 发行版。

您会发现许多 Linux 发行版，每个都包含标准的 Linux 操作系统以及以下主要软件包：


- X 窗口系统：它是图形用户界面。
- 一个或多个图形桌面环境：其中最受欢迎的包括 GNOME 和 KDE。
- 一系列应用程序：Linux 程序以即插即用的软件形式提供，但源代码（即我们人类用来指示计算机执行操作的命令）是包含在内的（或易于获取的），其文档也同样如此。

当前的 Linux 发行版包含了海量的软件选择——多到一些发行版通常需要多张 CD-ROM 或一张 DVD-ROM（本书附带了一张 DVD-ROM）。

![](img/11709a8f88c8cd03868a929dc94c0e2b_36_0.png)

Linux 内核、Linux 发行版中的软件包以及 Linux 发行版本身的开发和维护都是作为开源项目组织的。简而言之，开源意味着有权访问源代码，并有权在任何限制下自由再分发软件。开源的定义远比我简洁的注记所涵盖的要复杂得多。若要了解开源的更多细节以及可接受的开源许可证，您可以访问位于 www.opensource.org 的开源促进组织（Open Source Initiative）网站。

表 1-1 列出了一些主要的 Linux 发行版，并对每个发行版进行了简要描述。除了我在表 1-1 中列出的这些发行版外，还有许多其他的 Linux 发行版。

![](img/11709a8f88c8cd03868a929dc94c0e2b_36_1.png)

若想了解更多关于 Linux 发行版的信息，请访问 Distrowatch.com，网址为 www.distrowatch.com。在该网站上，您可以阅读特定发行版的资料，并找到订购特定发行版 CD 或 DVD 的链接。

**表 1-1 主要 Linux 发行版**

| 发行版 | 描述 |
| :--- | :--- |
| Debian GNU/Linux | 这是一个非商业发行版，始于 1993 年，至今依然是一个广受欢迎的发行版，世界各地有许多志愿者开发者为该项目做出贡献。Debian 是一个庞大的发行版。仅二进制软件包就需要 14 张 CD 或 2 张 DVD。但是，如果您拥有互联网连接，可以使用单张 Debian 网络安装 CD 来安装基础系统，该 CD 可在 www.debian.org/CD/netinst 获取。安装好基础的 Debian 系统后，您可以使用名为 apt-get 的软件包安装工具轻松安装和升级 Debian 软件包，其中 apt 代表 Advanced Package Tool（高级软件包工具）。Debian 可免费下载，网址为 www.debian.org。Debian 是其他几个近期发行版的基础，包括 Knoppix、MEPIS、Ubuntu 和 Xandros。 |
| Fedora Core | 该发行版是 Red Hat Linux（即来自 Red Hat 公司的 Linux 发行版）的继任者。2003 年 11 月发布的 Fedora Core 1 是 Red Hat Linux 9 的继任者。Fedora Core 可免费获取。Fedora Core 使用 Red Hat 软件包管理器（RPM）格式来管理其软件包。您可以从 `http://fedora.redhat.com` 下载 Fedora Core。 |
| Gentoo Linux | 这是一个非商业的、基于源代码的（意味着所有软件均以源代码形式提供）发行版，首次出现在 2002 年。安装程序提供一些二进制软件包以启动 Linux，但其核心理念是在用户的计算机上编译所有源代码软件包。这使得构建一个包含最新图形桌面、多媒体和开发工具的完整 Gentoo 系统耗时较长，因为所有软件包都必须下载并编译。Gentoo Linux 可免费从 `www.gentoo.org` 获取。 |
| Knoppix | 这个 Live CD 发行版基于 Debian，以其开发者、德国人 Klaus Knopper 的名字命名。Knoppix 可以作为恢复工具使用（用于修复已安装的 Linux 系统中的问题），因为您可以直接从 CD 运行 Knoppix，而无需先将其安装到硬盘上。Knoppix CD 以压缩格式存储软件，Knoppix 会在运行时动态解压程序。采用这种方法，Knoppix 可以在一张 CD 上容纳多达 2 GB 的软件。Knoppix 使用 Debian 软件包管理。若想了解如何免费下载 Knoppix，请访问位于 `www.knopper.net/knoppix/index-en.html` 的 Knoppix 网站。 |
| Linspire | 这个商业发行版最初于 2002 年以 LindowsOS 的名称发布。Linspire 使用 Debian 软件包格式，并通过其所谓的 Click-N-Run 基于 Web 的界面提供付费软件下载。您可以通过 BitTorrent（一种点对点文件共享系统）下载名为 LindowsLive! 的 Live CD 版本。若想了解有关 Linspire 的更多信息，请访问 `www.linspire.com`。 |
| Mandriva Linux | 这个流行的发行版最初是 1998 年发布的 Red Hat Linux，带有易于使用的安装程序，并默认使用 KDE 桌面。直到最近，这个发行版还被称为 MandrakeLinux。Mandriva Linux 使用 Red Hat 软件包管理器（RPM）格式来管理其软件包。您可以在 `www.mandrivalinux.com` 获取 Mandriva Linux 下载版（一套 3 张 CD/DVD）。点击 Download（下载）链接以获取更多信息。 |
| MEPIS Linux | 这个基于 Debian 的 Live CD 发行版首次发布于 2003 年 7 月。它还包含一个图形化安装程序，可以从 Live CD 启动以将 MEPIS 安装到硬盘上。MEPIS 具有良好的硬件检测功能，并附带 Java 和多媒体软件，这使其广受欢迎。MEPIS 使用 Debian 软件包格式。您可以从 `www.mepis.org` 免费 SimplyMEPIS Live CD。 |
| Slackware Linux | 这是最古老的发行版之一，最早发布于 1992 年。Slackware 使用压缩 tar 文件作为其软件包，并提供一个基于文本的安装程序，硬件自动检测功能有限。您需要通过编辑文本文件来完成所有软件配置。Slackware 可免费从 www.slackware.com 获取。 |
| SUSE Linux | 这个商业发行版在 2005 年 8 月转变为一个名为 openSUSE 的社区开发项目。SUSE Linux 开源软件（OSS）现在可免费获取，零售版的 SUSE Linux 基于开源版本。SUSE 附带 YaST 安装和配置工具。SUSE Linux 使用 RPM 软件包。openSUSE 项目提供来自各种镜像站的 SUSE Linux OSS 的 ISO 映像文件（参见 www.opensuse.org/Download）。请访问 www.opensuse.org 了解更多关于 SUSE Linux 的信息。 |
| Ubuntu Linux | 这是一个相对较新的基于 Debian 的非商业 Linux 发行版，自 2004 年首次发布以来，在很短的时间内变得非常流行。Ubuntu 既有安装 CD 也有 Live CD 版本。由于它是基于 Debian 的，您可以从安装 CD 安装基本桌面系统，然后使用 apt-get 工具安装其他软件包，并以此保持系统更新。您可以从 www.ubuntu.com 免费下载 Ubuntu。 |
| Xandros Desktop OS | 该发行版是 Corel Linux 的继任者，并基于 Debian。Xandros 面向首次使用 Linux 的用户，其安装程序可以重新分区硬盘。功能强大的 Xandros 文件管理器是 Xandros 的一个主要卖点。然而，Xandros 包含一些专有组件，阻止了再分发。通过 BitTorrent 可以获得一个免费的 Xandros Desktop 受限版本，称为 Open Circulation Edition（开放流通版）。请访问 www.xandros.com 了解更多关于 Xandros 的信息。 |

正如您在表 1-1 的简要描述中看到的，一些 Linux 发行版，如 Knoppix 和 MEPIS，是以 Live CD 的形式存在的。Live CD（或 Live DVD）包含一个 Linux 内核，您可以直接从 CD 或 DVD 启动并运行，而无需先将其安装到硬盘上。如果您想在决定是否安装之前先试用某个发行版，这类 Live CD 发行版会非常方便。

本书附带的配套 DVD 可用作 Knoppix Live DVD。您只需从 DVD 启动 PC 并按 Enter 键即可运行 Knoppix。

许多 Linux 发行版，如 SUSE Linux 和 Xandros Desktop，都是商业产品，您可以在线或在计算机商店和书店购买。如果您听说过开源和 GNU（GNU's Not UNIX）许可证，您可能会认为没有人可以为了利润而销售 Linux。对于销售 Linux 发行版的公司来说，幸运的是，GNU 许可证——也被称为



GNU 通用公共许可证（GPL）允许以营利为目的的商业发行（但要求软件必须以源代码形式分发），并规定任何人可以将软件以源代码形式复制并分发给其他任何人。多个 Linux 发行版可依据 GPL 免费获得，这意味着出版商可以将这些发行版随本书附带在 DVD-ROM 上，并且你可以随意复制该 DVD 而不受数量限制。

#### 解读版本号

Linux 内核和每个 Linux 发行版都有自己的版本号。Linux 发行版中附带的一些附加软件程序（如 GNOME 和 KDE）也拥有各自的版本号。Linux 内核与 Linux 发行版的版本号互不相关，但每个版本号都具有特定的含义。

##### Linux 内核版本号

在 Linux 内核版本 1.0 于 1994 年 3 月 14 日发布后，松散的 Linux 开发社区采用了一套版本号编号方案。其中 x 为偶数的版本号，如 1.x.y 和 2.x.y，被认为是稳定版本。最后一位数字 y 是补丁级别，随着问题被修复，该数字会递增。例如，2.6.14 就是一个典型的 Linux 内核稳定版本。请注意，这些版本号的形式是由句号分隔的三个整数——主版本.次版本.补丁——其中主版本和次版本是表示主要和次要版本号的数字，而补丁则是代表补丁级别的另一个数字。

形如 2.x.y 且 x 为奇数的版本号为开发者提供的测试版（beta）；它们可能不稳定，因此你不应该将此类版本用于日常使用。例如，如果你发现 Linux 内核版本 2.7.5，其中的 7 表明这是一个测试版。开发者会在这些奇数版本号的 Linux 中添加新功能。

你可以在 www.kernel.org 在线查找最新的 Linux 内核版本。

##### 特定发行版的版本号

每个 Linux 发行版也有一个版本号。这些版本号通常遵循 x.y 格式，其中 x 是主要版本，y 是次要版本。如今，如果次要版本号为 0，则直接省略——例如 Fedora Core 4 和 Fedora Core 5。与 Linux 内核版本号不同，奇数和偶数的次要版本号不附有任何特殊含义。每个版本的 Linux 发行版都包含 Linux 内核以及其他主要组件（如 GNOME、KDE 和各类应用程序）的特定版本。

活跃的 Linux 发行版的开发者通常会定期发布新版本——大约每六到九个月发布一次。例如，SUSE Linux 9.0 于 2003 年 10 月发布；9.1 于 2004 年 4 月发布；9.2 于 2004 年 10 月发布；9.3 于 2005 年 4 月发布；SUSE Linux 10.0 则于 2005 年 10 月首次亮相。通常，Linux 发行版的每个新主要版本都会提供显著的新功能。

Debian 在任何时候至少都有三个版本——*稳定版（stable）*、*不稳定版（unstable）*和*测试版（testing）*。

- **稳定版：** 大多数用户更喜欢这种类型的版本，因为它是最新正式发布且稳定的发行版。
- **不稳定版：** 这表明开发者正在处理这个版本。
- **测试版：** 该版本包含经过一些测试但尚未准备好纳入稳定版中的软件包。

##### Linux 标准基础（LSB）

Linux 的重要性已足以形成一个名为 Linux 标准基础（简称 LSB）的标准。LSB 是一组二进制标准，有助于减少 Linux 发行版之间的差异并促进应用程序的可移植性。LSB 背后的理念是提供应用程序二进制接口（ABI），以便软件应用程序能够在任何符合 LSB 标准的 Linux（或其他 UNIX）系统上运行。LSB 规范参考了 POSIX 标准以及许多其他标准，如 C 和 C++ 编程语言标准、X 窗口系统第 11 版第 6 次发布（X11R6）和文件系统层次标准（FHS）。LSB 版本 1.2（通常简称为 *LSB 1.2*）于 2002 年 6 月 28 日发布。LSB 1.3 于 2003 年 1 月发布，LSB 2.0 于 2004 年 8 月 30 日发布，LSB 3.0 于 2005 年 7 月 1 日发布，LSB 3.1 于 2005 年 10 月 31 日发布。

LSB 规范由两部分组成——一个在所有处理器类型之间保持一致的通用规范，以及一组针对每种处理器架构的特定硬件规范。例如，LSB 1.2 针对 Intel 32 位（IA32）和 PowerPC 32 位（PPC32）处理器制定了架构特定规范。LSB 1.3 在 IA32 和 PPC32 规范的基础上，为 Intel 64 位（IA64）架构以及 IBM zSeries 31 位（S390）和 64 位（S390X）处理器增加了规范。LSB 2.0 为 AMD 64 位（AMD64 或 x86_64）处理器增加了规范。当前的 LSB 规范——LSB 3.0——支持七种处理器架构：IA32、IA64、PPC32、PPC64（64 位 PowerPC）、S390、S390X 和 x86_64。

存在一项 LSB 认证计划。截至目前，多个 Linux 发行版——如面向 x86 的 Red Hat Enterprise Linux 3、SUSE Linux 9.1 和 Sun Java Desktop System (JDS) 2——已获认证为符合 LSB 1.3 标准的 IA32 运行环境。还有一些其他发行版——如 SUSE Linux 9.3、MandrakeLinux Corporate Server 3.0、带 Service Pack 1 的面向 x86 的 Novell Linux Desktop 9、SUSE Linux 9.2 以及来自 Sun Wah Linux Limited 的 RAYS LX 1.0——已获认证为符合 LSB 2.0 标准的 IA32 运行环境。SUSE Linux 10.0 是最早的符合 LSB 3.0 标准的 IA32 运行环境之一。预计近期内将有更多发行版通过 LSB 3.0 认证。

要了解有关 LSB 的更多信息，请访问 www.linuxbase.org。最新的 LSB 认证系统列表可在 www.opengroup.org/lsb/cert/cert_prodlist.tpl 获取

### Linux 发行版包含的内容

Linux 发行版包含 Linux 内核以及大量其他软件。这些软件包的内容涵盖了从图形桌面、互联网服务器到创建新软件的编程工具等方方面面。在本节中，我将简要介绍典型 Linux 发行版中捆绑的一些主要软件包。如果没有这些捆绑的软件，Linux 不会像今天这样流行。

#### GNU 项目是什么？

GNU 是一个递归缩写，全称为 GNU’s Not UNIX（GNU 即非 UNIX）。GNU 项目由理查德·斯托曼（Richard Stallman）于 1984 年发起，旨在开发一个完整的类 UNIX 操作系统。GNU 项目开发出了完整操作系统所需的一切，唯独操作系统内核除外。所有 GNU 软件均在 GNU 通用公共许可证（GPL）下分发。GPL 实质上要求软件以源代码形式分发，并规定任何用户都可以以源代码形式复制、修改和分发软件。不过，用户可能需要为其获得的 GNU 软件副本付费。

自由软件基金会（FSF）是一家免税慈善机构，负责为 GNU 项目筹集资金。要了解有关 GNU 项目的更多信息，请访问其主页 www.gnu.org。在那里你可以找到如何联系自由软件基金会以及如何支持 GNU 项目的信息。

#### GNU 软件

Linux 发行版的核心是来自 GNU 项目的一组软件。只有当你通过*文本终端*使用你的 Linux 系统时，才会接触到这些 GNU 实用工具——文本终端是一种基本的命令行接口，屏幕上几乎没有显示什么，只有一个提示符，供你输入命令。（或者你可以使用一个模仿文本终端的图形窗口，仍然可以继续使用 GNU 实用工具。）GNU 软件是任何 Linux 发行版的基本组成部分之一。

作为 Linux 用户，你可能没有意识到所有 Linux 发行版对 GNU 软件的依赖程度之深。你在 Linux 系统中执行的任务几乎都涉及一个或多个 GNU 软件包。例如，GNOME 图形用户界面（GUI）和命令解释器（即 *bash*）都是 GNU 软件程序。顺便说一下，*shell* 是接收你输入的命令并随后运行相应程序来响应的命令解释器应用程序。如果你重建内核或开发软件，你使用的是 GNU C 和 C++*编译器*（这是伴随 Linux 提供的 GNU 软件的一部分）。如果你使用 *ed* 或 *emacs* 编辑器编辑文本文件，你再次使用的是 GNU 软件包。这样的列表可以一直列下去。

![](img/11709a8f88c8cd03868a929dc94c0e2b_42_0.png)

表 1-2 列出了一些随大多数 Linux 发行版附带的知名 GNU 软件包。展示此表只是为了让你感受一下可以使用 GNU 软件进行的各类操作。根据你的兴趣，你可能永远不需要使用其中的许多软件包，但知道它们在必要时是存在的，这总是好的。

**表 1-2** 知名 GNU 软件包

| *软件包* | *描述* |
| --- | --- |
| autoconf | 生成用于自动配置源代码包的 shell 脚本 |
| automake | 生成用于配合 *autoconf* 使用的 *Makefile.in* 文件 |
| bash | Linux 中的默认 shell（命令解释器） |
| bc | 支持任意精度数字的交互式计算器 |
| Binutils | 包含多个用于处理二进制文件的实用工具的软件包：*ar*、*as*、*gasp*、*gprof*、*ld*、*nm*、*objcopy*、*objdump*、*ranlib*、*readelf*、*size*、*strings* 和 *strip* |

*（续）*





# 18 Linux 发行版包含的内容

表 1-2（续）

| 软件包 | 描述 |
| :--- | :--- |
| Coreutils | 一个组合了名为 Fileutils、Shellutils 和 Textutils 的三个独立软件包的软件包，实现了诸如 chgrp、chmod、chown、cp、dd、df、dir、dircolors、du、install、ln、ls、mkdir、mkfifo、mknod、mv、rm、rmdir、sync、touch、vdir、basename、chroot、date、dirname、echo、env、expr、factor、false、groups、hostname、id、logname、nice、nohup、pathchk、printenv、printf、pwd、seq、sleep、stty、su、tee、test、true、tty、uname、uptime、users、who、whoami、yes、cut、join、nl、split、tail、wc 等实用工具 |
| GNUchess | 一款国际象棋游戏 |
| GNU C 库 | 供所有 Linux 程序使用 |
| cpio | 将文件归档复制到磁盘或文件系统的另一部分，或从磁盘/文件系统复制 |
| diff | 比较文件，以几种不同的格式逐行显示更改 |
| ed | 一个面向行的文本编辑器 |
| emacs | 一个可扩展、可定制的全屏文本编辑器及计算环境 |
| Findutils | 一个包含 find、locate 和 xargs 实用工具的软件包 |
| finger | 一个旨在让互联网用户获取彼此信息设计的实用程序 |
| gawk | GNU 项目对 awk 编程语言的实现 |
| gcc | C、C++、Objective C 及其他语言的编译器 |
| gdb | C、C++ 和 Fortran 的源代码级调试器 |
| gdbm | 传统 cfm 和 ndbm 数据库库的替代品 |
| gettext | 一组实用工具，使软件维护人员能够使其软件包的用户消息国际化（即让软件支持英语、法语、西班牙语等不同语言） |
| ghostscript | PostScript 和便携式文档格式（PDF）语言的解释器 |
| ghostview | 一个 X Window 系统应用程序，通过图形用户界面（GUI）使 ghostscript 可被访问，从而让用户能在窗口中查看 PostScript 或 PDF 文件 |
| The GIMP | （GNU 图像操纵程序）：类似于 Adobe Photoshop 的图像处理程序 |
| GNOME | 为 Linux 用户可能执行的广泛任务提供图形用户界面（GUI） |
| gnumeric | 一个在 GNOME 中工作的图形化电子表格（类似于 Microsoft Excel） |
| grep 软件包 | 包含用于查找匹配指定文本模式的行的 grep、egrep 和 fgrep 命令 |
| groff | 类似于 troff 的文档格式化系统 |
| gtk+ | X Window 系统的图形用户界面工具包（用于开发 GNOME 应用程序） |
| gzip | 一个用于压缩和解压文件的 GNU 实用工具 |
| indent | 通过以几种不同风格之一缩进来格式化 C 源代码 |
| less | 一个类似于 more 的逐页显示程序，但具备更多功能 |
| libpng | 用于便携式网络图形（PNG）格式图像文件的库 |
| m4 | 传统 UNIX 宏处理器的实现 |
| make | 一个确定大型软件包中哪些文件需要重新编译，并发出重新编译命令的实用工具 |
| mtools | 一组允许用户读取、写入和操作 DOS 文件系统（通常是软盘）上文件的程序 |
| ncurses | 一个用于在纯文本终端上显示和更新文本的软件包 |
| patch | Larry Wall 程序的 GNU 版本，用于获取 diff 的输出并将这些差异应用于原始文件以生成修改后的版本 |
| rcs | （修订控制系统）：用于软件项目中源文件的版本控制和管理 |
| sed | ed 文本编辑器的面向流的版本 |
| Sharutils | 一个包含 shar（用于将许多文件制作成 shell 归档）和 unshar（用于解压这些 shell 归档）的软件包 |
| tar | 一个磁带归档程序，包含多卷支持；能够归档稀疏文件（包含大量全零数据块的文件）、处理压缩和解压以及创建远程归档；以及其他用于增量和完全备份的特殊功能 |
| texinfo | 一组生成打印手册、纯 ASCII 文本和在线超文本文档（称为 info）的实用工具，并允许用户查看和阅读在线 info 文档 |
| time | 一个报告进程使用的用户时间、系统时间和实际时间的实用工具 |

### 图形用户界面和应用程序

面对现实吧——在终端上输入晦涩难懂的 Linux 命令很无聊。对于普通用户来说，通过图形用户界面（GUI，读作 GOO-ee）使用系统——即提供可点击的图片和小写 w 开始的窗口（windows）来打开的界面——要容易得多。这时，X Window 系统，或简称 X，就派上了用场。

X 有点像 Microsoft Windows，但 X 的工作底层细节与 Windows 完全不同。X 提供了在屏幕上显示窗口的基本功能，但（与 Microsoft Windows 不同）它并不附带任何特定的图形应用程序外观或感觉。那种外观和感觉来自图形用户界面，例如利用 X Window 系统的 GNOME 和 KDE。

大多数 Linux 发行版都包含 X Window 系统，形式为 XFree86 或 X.Org X11 —— 这是针对 80x86 系统的 X Window 系统实现。XFree86 和 X.Org X11 可与当今个人电脑上可用的各种视频卡协同工作。

![](img/11709a8f88c8cd03868a929dc94c0e2b_45_0.png)

直到 2004 年初，XFree86 项目（<http://www.xfree86.org>）的 XFree86 是 x86 系统中最常用的 X Window 系统实现。然而，大约在 4.4 版本时，XFree86 许可条款的一些变更引起了许多 Linux 和 UNIX 供应商的担忧——他们认为许可条款不再与 GNU 通用公共许可证（GPL）兼容。2004 年 1 月，几家供应商成立了 X.Org 基金会（<http://www.x.org>），以促进开源 X Window 系统和图形桌面的持续开发。X.Org X11 的第一个版本使用的是 XFree86 4.4 所使用的相同代码，直到 XFree86 许可变更导致 X.Org 基金会成立的时刻。

至于图形用户界面，Linux 发行版包含两个强大的图形用户界面桌面中的一个或两者：KDE（K 桌面环境）和 GNOME（GNU 对象模型环境）。如果 PC 上同时安装了 GNOME 和 KDE，你可以选择哪个桌面作为默认——或者在两者之间切换。KDE 和 GNOME 提供类似于 Microsoft Windows 和 Mac OS 的桌面。GNOME 还附带 Nautilus 图形外壳，使查找文件、运行应用程序和配置你的 Linux 系统变得容易。使用 GNOME 或 KDE，你无需了解晦涩难懂的 Linux 命令就可以开始使用你的 Linux 工作站。但是，如果你需要直接使用这些命令，你只需打开一个终端窗口并在提示符处输入它们即可。

Linux 还附带许多图形应用程序。最值得注意的程序是 The GIMP（GNU 图像操纵程序），一个用于处理照片和其他图像的程序。The GIMP 的能力与 Adobe Photoshop 不相上下。

提供常见的生产力软件——如文字处理、电子表格和数据库应用程序——曾经是 Linux 缺乏的一个领域。但这种情况已经改变。Linux 附带 OpenOffice.org 办公生产力应用程序。此外，你可能想看看这些未在本书配套 DVD-ROM 中提供的著名商业 Linux 办公生产力应用程序：

-   **Applixware**：此办公套装包是 Linux 生产力软件的一个良好示例。你可以在 `www.vistasource.com` 找到它。
-   **StarOffice**：来自 Sun Microsystems（`www.sun.com/staroffice`），StarOffice 是另一个著名的生产力软件包。
-   **CrossOver Office**：来自 CodeWeavers（`www.codeweavers.com/products/cxoffice`），你可以使用 CrossOver Office 在 Linux 中安装你的 Microsoft Office 应用程序（Office 97、Office 2000 和 Office XP）以及几个其他 Windows 应用程序。

如你所见，兼容 Microsoft Office 的 Linux 办公应用程序并不缺乏。

### 网络

Linux 附带了你所需的一切，以便在网络上使用该系统，使系统能够与其他系统交换数据。在网络中，交换数据的计算机必须遵循定义明确的规则，或**协议**。**网络协议**是发送方和接收方同意的通过网络交换数据的方法。这样的协议类似于你在聚会上与人礼貌交谈时可能遵循的规则。你通常从说你好、交换名字开始，然后轮流说话。网络协议的工作方式大致相同。两台计算机使用相同的协议在网络上相互发送位和字节。

最著名和流行的网络协议之一是传输控制协议/互联网协议（*TCP/IP*）。TCP/IP 是互联网上首选的协议——如今覆盖全球的“网络的网络”。Linux 支持 TCP/IP 协议以及任何利用 TCP/IP 的网络应用程序。

### 互联网服务器

一些流行的网络应用程序专门设计用于将一个系统上的信息传送到另一个系统。当你使用电子邮件（e-mail）发送电子邮件或使用 Web 浏览器访问网站时，你正在使用这些网络应用程序（也称为*互联网服务*）。以下是一些常见的互联网服务：

-   **电子邮件**（e-mail），你使用它通过类似 `joe@someplace.com` 的地址向互联网上的任何其他人员发送消息
-   **万维网**（或简称为 Web），你使用 Web 浏览器浏览它
-   **新闻服务**，你可以阅读新闻组并向名为 `comp.os.linux.networking` 或 `comp.os.linux.setup` 等新闻组发布新闻条目





### Linux 发行版包含的内容

- **文件传输工具**，你可以使用它来上传和下载文件
- **远程登录**，你可以使用它连接到互联网上的另一台计算机（远程计算机）并进行操作——前提是你拥有访问该远程计算机所需的用户名和密码

任何 Linux PC 都可以提供这些互联网服务。为此，该 PC 必须连接到互联网，并且必须运行被称为*互联网服务器*的特殊服务器软件。每个服务器都使用特定的协议来传输信息。例如，以下是 Linux 中常见的一些互联网服务器：

- `sendmail` 是使用 SMTP（简单邮件传输协议）在系统之间交换电子邮件的邮件服务器。
- `Apache httpd` 是使用 HTTP（超文本传输协议）将文档从一个系统发送到另一个系统的 Web 服务器。
- `vsftpd` 是使用 FTP（文件传输协议）在互联网上的计算机之间传输文件的服务器。
- `inn` 是使用 NNTP（网络新闻传输协议）在互联网上以存储转发方式分发新闻文章的新闻服务器。
- `in.telnetd` 允许用户通过 TELNET 协议从一台系统登录到互联网上的另一台系统。
- `sshd` 允许用户通过 SSH（安全外壳）协议从一台系统安全地登录到互联网上的另一台系统。

### 软件开发

Linux 特别适用于软件开发。开箱即用，它内置了丰富的软件开发工具，例如编译器和构建程序所需的代码库。如果你恰好熟悉 UNIX 和 C 编程语言，你会发现在 Linux 中编程如鱼得水。

就开发环境而言，Linux 拥有与其他 UNIX 工作站（例如来自 IBM、Sun Microsystems 和 Hewlett-Packard (HP) 的工作站）中可能使用的基本工具（如编辑器、编译器和调试器）相同的配置。这意味着，如果你白天在其中一个 UNIX 工作站上工作，你可以在晚上使用家里的 Linux PC 以极低的成本复制那个开发环境。然后，你可以在家完成工作项目，或者将时间花在你出于兴趣编写并打算在互联网上分享的软件上。

为了让你对 Linux 的软件开发支持有一个大致的了解，以下是使 Linux 成为高效软件开发环境的各种功能列表：

- GNU C 编译器（*gcc*）：可以编译符合 ANSI 标准的 C 程序。
- GNU C++ 编译器（*g++*）：支持符合 ANSI 标准的 C++ 特性。
- GNU Java 编译器（*gcj*）：可以编译用 Java 编程语言编写的程序。
- GNU make 实用程序：使你可以编译和链接大型程序。
- GNU 调试器（*gdb*）：使你可以单步执行程序以查找问题，并确定程序在何处以及为何失败。（失败程序的内存映像保存在名为 *core* 的文件中；*gdb* 可以检查此文件。）
- GNU 分析实用程序（*gprof*）：使你可以确定软件使用计算机处理器时间的程度。
- 版本控制系统：Subversion、Concurrent Versions System (**CVS**) 和 Revision Control System (**RCS**)：维护版本信息并控制对源文件的访问，以确保两名程序员不会在同一时间无意间修改同一个源文件。
- GNU *emacs* 编辑器：准备源文件，甚至启动编译链接过程以构建程序。
- Perl：是一种脚本语言，你可以使用它来编写脚本以完成特定任务，将许多较小的程序与 Linux 命令连接起来。
- 工具命令语言及其图形工具包（*Tcl*/*Tk*）：使你可以快速构建图形应用程序。
- Python：一种解释型编程语言，可与 Perl 和 Tcl 相媲美。（例如，Fedora Core 安装程序称为 *anaconda*，它是用 Python 编写的。）
- 动态链接共享库：使你的实际程序文件小得多，因为多个程序可能需要的库代码都是共享的——系统中只加载一份副本。

### 在线文档

随着你在使用 Linux 方面变得更加熟练，你可能会想要快速查找信息——例如，而不必翻阅（呃）这本很棒的书。幸运的是，Linux 附带了足够的在线信息，可以在你隐约想起某个命令的名称但记不清应该输入的确切语法的情况下帮你回忆起来。

如果你使用 Linux 命令，可以通过使用 `man` 命令来查看命令的手册页——通常称为*man 页*。（你需要记得该命令才能访问在线帮助。）

你还可以从 GUI 桌面获取帮助。GNOME 和 KDE 桌面都附带了帮助查看器，用于查看在线帮助信息。大多数发行版在桌面菜单中包含一个帮助选项，或者在桌面上有一个帮助图标，你可以选择它以获取在线帮助。然后，你可以通过单击初始帮助窗口上的链接来浏览帮助信息。图 1-1 显示了一个典型的帮助窗口——这是来自 Ubuntu GNOME 桌面的。

![](img/11709a8f88c8cd03868a929dc94c0e2b_49_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_49_1.png)

### Linux 帮助你管理什么

作为操作系统，Linux 充当中介，通过它——作为“系统的主人”——你管理所有硬件。硬件包括系统机箱、显示器、键盘、鼠标以及连接到系统机箱的任何其他设备。*外设*这个总括术语指的是附加到系统的任何设备。如果你使用笔记本电脑，你的所有硬件都封装在笔记本电脑中。

在该系统机箱内部是系统的大脑——微处理器（例如 Intel Pentium 4）或 CPU——它执行计算机程序中包含的指令。当微处理器运行计算机程序时，该程序的指令存储在内存或 *RAM* 中。RAM 代表随机存取存储器。（这意味着内存的任何部分都可以随机访问——以任意顺序。）

系统机箱还有另一个关键组件——硬盘（有时也称为*硬磁盘*）。硬盘是计算机程序和数据的永久存储空间。说是永久，是因为当你关闭 PC 时，其内容不会消失。硬盘组织成文件，这些文件又按层次结构组织成目录和子目录（有点像在文件柜抽屉中的文件夹里整理纸张）。

为了让 Linux 系统正常运行，你或他人必须确保硬件正常工作，并定期备份文件。还有*安全*问题——确保只有合法人员可以访问和使用系统。这些任务被称为*系统管理*。

如果你在拥有许多计算机的大型设施中使用 Linux，全职系统管理员可能会处理所有系统管理任务。另一方面，如果你在家用 PC 上运行 Linux，你就是系统管理员。不要让这个想法吓到你。你不需要知道任何魔法咒语或准备晦涩难懂的配置文件才能成为系统管理员。大多数 Linux 发行版都包含许多图形工具，使系统管理成为*点击*即用的工作，就像运行其他任何应用程序一样。

#### 磁盘、CD-ROM 和 DVD-ROM

一些 Linux 发行版包含在单张 DVD-ROM 上。安装后，Linux 内核和所有应用程序都存储在你的硬盘上——这是当你告诉 PC 做某事时，它首先查看的地方。

通常，硬盘在安装过程中已准备好使用 Linux。之后，你通常不动硬盘，除了备份存储在那里的数据或（偶尔）安装新应用程序。

在 Linux 中使用 CD-ROM 或 DVD-ROM 很容易。当你在 GNOME 或 KDE 桌面登录时，只需将 CD 或 DVD 插入驱动器，系统就应该会自动检测 DVD/CD-ROM。根据 Linux 发行版的不同，桌面上会出现 DVD/CD-ROM 图标，或者文件管理器会自动打开并显示 DVD/CD-ROM 的内容。如果其他方法都失败了，你可以输入一个简单的 `mount` 命令将 DVD/CD-ROM 与系统上的目录关联起来。从 Linux 访问 CD 或 DVD 上文件的整个过程被称为*挂载*该 CD 或 DVD。

除了硬盘和 DVD/CD-ROM 驱动器外，当然，你的 PC 可能还有其他驱动器，例如软盘驱动器或 Zip 驱动器，在 Linux 中使用这些磁盘也很简单：你插入磁盘并双击代表磁盘驱动器的图标，在 GUI 桌面上。这样就会挂载磁盘，使你可以开始使用它。




#### 外围设备

连接到你的 PC 的任何设备都是外围设备，安装在系统机箱内部的某些组件（例如声卡）也是如此。你可以在 Linux 中配置和管理这些外围设备。

打印机是一种常见的外围设备，通常连接到你的 PC 的并口。（许多发行版都附带图形化打印机配置工具，你可以使用它来配置打印机。）

另一种需要配置的外围设备是声卡。大多数 Linux 发行版都能检测并配置声卡，就像 Windows 一样。但是，如果 Linux 无法正确检测声卡，你可能需要运行文本模式或图形工具来配置声卡。

Linux 在安装时就会配置其他外围设备，例如鼠标和键盘。安装完成后，你基本上可以不用管它们。

如今，PC 通常都配备了 USB（通用串行总线）接口；许多设备，包括打印机和扫描仪，都可以插入 PC 的 USB 端口。USB 设备的一个出色特性是，你可以随时将它们插入或拔出 USB 端口——在系统通电启动时，设备不必连接。这些设备被称为*热插拔*设备，因为你可以在系统“热”状态（即正在运行时）插入设备。Linux 支持许多热插拔 USB 设备。当你将设备插入 USB 端口时，Linux 会加载正确的驱动程序并使该设备可供应用程序使用。

#### 文件系统和共享

目录和文件的全部组织结构被称为*文件系统*。当然，你可以使用 Linux 来管理文件系统。当你通过 GNOME 或 KDE 图形桌面浏览文件时，你操作的是熟悉的文件夹图标。

![](img/11709a8f88c8cd03868a929dc94c0e2b_51_0.png)

维护文件系统的各项任务中，备份重要文件是一项关键任务。在 Linux 中，你可以使用 `tar` 程序将软盘或 Zip 驱动器上的一个或多个目录归档。你甚至可以备份磁带上的文件（如果你有一台磁带机）。如果你拥有 CD 或 DVD 刻录机，你还可以将想要备份或永久保存的文件刻录到 CD 或 DVD 上。

Linux 还可以与其他网络系统共享文件系统的一部分。例如，你可以使用网络文件系统（NFS）与其他网络系统共享文件。对于系统上的用户而言，远程系统的文件看起来就像是位于本地系统某个目录中一样。

Linux 还附带 Samba 软件包，该软件包支持与 Microsoft Windows 系统进行文件共享。Samba 使 Linux 系统的工作方式就像 Windows 文件服务器或打印服务器一样。你还可以访问网络上其他 Windows 系统上的共享文件夹。

### 网络

既然现在大多数 PC 要么位于局域网（LAN）中，要么连接到互联网，你就需要管理网络。Linux 附带了一个网络配置工具，用于设置局域网。对于使用调制解调器连接互联网，通常有一个图形界面（GUI）的互联网拨号工具。

如果你使用 DSL（即电话公司提供的高速互联网连接）或有线调制解调器连接互联网，你需要一台带有以太网卡的 PC，该卡连接到有线或 DSL 调制解调器。这也意味着你需要设置一个局域网并配置以太网卡。但幸运的是，这些步骤通常是 Linux 安装过程的一部分。如果你想在以后进行配置，可以使用图形界面网络配置工具来完成。

Linux 还包含用于配置*防火墙*的工具。防火墙是一种保护缓冲层，有助于防止任何人试图通过你的互联网连接窥探，从而让你的系统保持相对安全。你可以通过使用 `iptables` 命令或运行图形界面防火墙配置工具来配置防火墙。

## 入门

根据我在探索新领域的个人经验，我提出了一个四步流程来开始使用 Linux：

1. 在 PC 上安装 Linux
2. 配置 Linux，使一切符合你的喜好
3. 探索图形界面桌面和应用程序
4. 了解诸如互联网服务器等特定主题的详细信息

在接下来的章节中，我将更详细地解释这个处方。

### 安装

Microsoft Windows 通常预装在你的新 PC 上，但 Linux 通常不是。因此，你面临的第一道障碍是将 Linux 安装到你的 PC 上。

克服了对未知事物最初的恐惧之后，我敢打赌你会发现安装 Linux 相当容易——但你首先要从哪里获取 Linux 呢？好消息是它是免费的——只需下载即可。例如，你可以访问 www.linux.org 的 Linux 在线网站，然后点击下载按钮。

由于典型的完整 Linux 发行版非常大——它占用几张 CD 或至少一张 DVD——你最好的选择是购买一本附带 Linux DVD-ROM 的书籍（比如本书）。然后你使用那张 CD 或 DVD 启动 PC，这会启动 Linux 安装过程，创建 Linux 分区并从 DVD 安装 Linux 软件包。在此过程中，你会配置许多项目——从网卡（如果有）到 X 窗口系统。

![](img/11709a8f88c8cd03868a929dc94c0e2b_53_0.png)

### 配置

完成 Linux 安装后，下一步是配置各个系统组件（例如声卡和打印机）并调整所需的设置。

如果你没有看到图形化登录屏幕，可能在安装期间 X 窗口系统未正确配置。你必须修复 X 配置文件才能使图形界面正常工作。

你可能还想配置你选择的图形界面桌面——GNOME 或 KDE 或两者兼有。每个桌面环境都有配置工具。你可以使用这些工具来调整桌面的外观和感觉（背景、标题字体，甚至整个配色方案）。

完成配置步骤后，你系统上的所有硬件和应用程序都应按你的喜好运行。

### 探索

拥有一台配置好的 Linux PC 后，你准备好探索 Linux 本身了。你可以从登录后看到的图形界面桌面开始探索。

探索图形界面桌面——GNOME 和 KDE——以及构成 Linux 文件系统的文件夹和文件。你也可以尝试从桌面运行应用程序。你会发现要探索的办公和多媒体应用程序以及互联网应用程序。

还要尝试*shell*——打开一个终端窗口，并在该窗口中输入一些 Linux 命令。你还可以探索在文本模式下工作的文本编辑器。知道如何在没有图形界面的情况下编辑文本文件是个好主意，以防图形界面不可用。至少你不会再无助。

### 了解更多

在你探索了 Linux 的全貌并了解每个部分的作用后，你可以深入挖掘，了解更多关于特定主题区域的信息。例如，你可能对设置互联网服务器感兴趣。然后你可以学习设置各个服务器的详细信息，例如用于电子邮件的 `sendmail`，用于 Web 服务器的 Apache，以及用于新闻服务器的 INN。

你可以选择了解更多的领域，例如安全性、编程和系统管理。

当然，你可以期待这一步骤会一直持续下去，即使你的系统已经按照你的意愿运行——至少是现在。毕竟，学习是一生的旅程。

*旅途愉快！*

## 第 2 章：安装 Linux

###### 本章内容

- 理解安装步骤
- 制作你的 PC 硬件清单
- 从 DVD 试用 Knoppix
- 为你的发行版刻录 CD 或 DVD
- 为 Linux 预留硬盘空间
- 安装 Debian
- 安装 Fedora Core
- 安装 MEPIS
- 安装 SUSE Linux
- 安装 Ubuntu
- 安装 Xandros Desktop

PC 通常预装了 Microsoft Windows。如果你想使用 Linux，首先必须安装它。

本书附带一张 DVD-ROM，其中包含多个 Linux 发行版——Debian、Fedora、Knoppix、MEPIS、SUSE、Ubuntu 和 Xandros。有些是完整发行版，有些是 Live CD，无需安装到硬盘即可试用。（*完整发行版*意味着包含安装该发行版所需的一切，而 *Live CD* 是指可以直接从中启动 Linux 的光盘。）DVD 上的 Xandros 版本是 Xandros Desktop 的一个有限版本，称为 *Open Circulation Edition*。要安装或试用这些发行版中的任何一个，你只需遵循本章中的步骤即可。

你可能会对在 PC 上安装新的操作系统感到有些担忧，因为这有点像脑部手术——或者更准确地说，有点像嫁接一个新的大脑，因为你可以将 Linux 安装到现有 Microsoft Windows 之上。当你安装两个这样的操作系统时，在启动 PC 时，你可以选择启动其中一个。在装有 Windows 的 PC 上添加 Linux 最大的麻烦是创建一个新的*磁盘分区*——基本上就是预留



Linux 安装的一部分。其余安装步骤相当常规——只需按照说明操作即可。如果你想尝试任何一种*Live CD*，你不需要进行任何磁盘分区，只需从 Live CD 启动你的电脑即可。但最重要的是，深呼吸并缓慢地呼出。你无需担忧，因为本章将解释所有内容。

### 遵循安装步骤

安装任何 Linux 发行版都涉及多个步骤。我想简要带你走过这些步骤，不展开细节。然后你可以按照特定发行版的详细步骤，从本书配套 DVD-ROM 中安装你想要的发行版。

在解释安装 Linux 的细节之前，我想先说明我如何在 DVD 上打包了多个 Linux 发行版。以下是关于配套 DVD 的情况：

- 它是一张包含 Fedora Core 和 Knoppix 的 DVD，这意味着你可以从该 DVD 启动电脑，要么运行 Knoppix Live CD，要么直接从 DVD 安装 Fedora Core。
- 除了 Fedora Core 文件外，DVD 还包含一个*distros*（发行版）文件夹，其中设有多个子文件夹，每个发行版一个——Debian、Knoppix、MEPIS、SUSE、Ubuntu 和 Xandros。在每个文件夹中，你都会找到该发行版的*ISO 映像文件*（ISO 映像文件包含 CD 或 DVD 的完整内容和结构）。在使用这些发行版进行安装之前，你必须将这些 ISO 映像刻录到 CD（或 DVD，如果 ISO 映像是为 DVD 设计的）上。
- SUSE 以 Live DVD ISO 映像文件的形式存在，你可以将其刻录到可刻录 DVD 上，并用于在不将 SUSE Linux 安装到硬盘的情况下，在电脑上运行它。

某些 Linux 发行版要求你在安装前掌握关于电脑硬件的相当多的信息。如果你计划安装 Debian，应当在开始安装之前收集有关电脑及其外设的信息。幸运的是，大多数 Linux 安装程序能够检测并处理大多数电脑外设。尽管如此，弄清楚你的电脑硬件配置仍是个好主意，以便在安装出现问题时能够进行故障排除。

第一步是刻录你所属发行版的 CD 或 DVD，除非你计划安装 Fedora Core 或 Knoppix。你可以在任何带有 CD/DVD 刻录机的系统上刻录 CD。（如果你想刻录 DVD，必须拥有 DVD 刻录机，但 DVD 刻录机既可以刻录 CD 也可以刻录 DVD。）通常，如果你已经拥有一台带有 CD/DVD 刻录机的 Windows 电脑，可以直接使用该系统来刻录 CD。请记住，你还必须拥有 DVD 光驱，因为你需要从本书的配套 DVD-ROM 中刻录 CD。一台配有 DVD 刻录机或组合 DVD-ROM 和 CD 刻录机的电脑即可完成此任务。

![](img/11709a8f88c8cd03868a929dc94c0e2b_57_0.png)

第二步是确保你的电脑可以从 DVD/CD 光驱启动。大多数新电脑可以直接从 DVD/CD 光驱启动，但某些电脑可能需要人工干预。通常，电脑可能被设置为先于 DVD/CD 光驱从硬盘启动，你必须进入 Setup 设置来更改启动设备的顺序。

要将电脑设置为从 DVD 光驱启动，你必须在电脑开机时进入 Setup。进入 Setup 并设置启动设备的具体步骤因电脑而异，但通常涉及按下一个键，例如 F2。当电脑开机时，会显示一条简短的消息，告诉你按哪个键进入 Setup。进入 Setup 后，你可以指定 DVD/CD 光驱为启动设备。一旦你的电脑被设置为从 DVD/CD 光驱启动，只需将 DVD 或 CD 放入光驱，然后重启你的电脑。

![](img/11709a8f88c8cd03868a929dc94c0e2b_58_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_58_1.png)

如果你计划尝试 Live CD 发行版，例如 MEPIS 或 Knoppix，第三步是从 Live CD 或 DVD 启动你的电脑。否则，第三步是在你的电脑硬盘上为 Linux 腾出空间。如果你正在运行 Microsoft Windows，这一步可能简单也可能复杂，取决于你是想用 Linux 替换 Windows，还是希望同时保留 Windows 和 Fedora Core。

如果你想在不移除（或不影响）Windows 的情况下安装 Linux，请记住，你现有的操作系统——我假设是 Windows 95、98、Me、NT、2000 或 XP——使用了整个硬盘。这意味着你必须对硬盘进行分区（划分），以便 Windows 存在于其中一部分，而 Linux 存在于另一部分。这一步可能会令人恐惧，因为你存在损坏硬盘并清除驱动器上所有内容的风险。

要在硬盘上为 Linux 安装程序预留空间，你应该使用分区工具来帮助你创建分区。如果你的电脑运行 Windows NT、2000 或 XP，你可能需要投资一款商业硬盘分区产品，例如 Symantec 的 Norton PartitionMagic（www.powerquest.com/partitionmagic），它也适用于 Windows 95/98/Me 系统。另一方面，你只需启动 Knoppix，然后使用随 Knoppix 附带的一个名为 QTParted 的图形用户界面（GUI）工具，即可重新划分你电脑的硬盘。

![](img/11709a8f88c8cd03868a929dc94c0e2b_58_2.png)

请注意，某些 Linux 发行版的安装程序（例如 SUSE 和 Xandros Desktop）可以通过缩小 Windows 分区的大小来自动为 Linux 创建分区。在这种情况下，你无需使用 PartitionMagic 或 QTParted 等工具来缩小硬盘上现有 Windows 分区的大小。

第一卷  
第二章  
安装 Linux

在你为 Linux 预留硬盘分区后，你可以从所选发行版的 CD 启动电脑并开始安装 Linux。安装过程中会发生很多步骤，且因发行版而异。走到这一步，后续过程应该顺畅无阻。只需依次通过安装界面，一两个小时内即可完成。大多数安装程序会调出 GUI（有些人将其发音为*GOO-ee*），并引导你完成所有步骤。安装过程中的一个关键步骤是再次对硬盘进行分区，但这次你只需使用之前创建的额外分区。在完成一些配置步骤（如设置网络和时区）后，你选择要安装的软件包，然后让安装程序完成剩余的安装工作。有些发行版甚至更简化了这一过程，去掉了软件选择步骤，而是安装一套默认的软件包。

在安装结束时，重启电脑。当 Linux 首次运行时，你有机会执行更多的配置步骤并安装额外的软件包。

#### 检查你的电脑硬件

如果你担心你的电脑可能无法运行 Linux，以下是在开始安装 Linux 之前需要考虑的电脑主要组件：

- **DVD 光驱**：你必须拥有一台 DVD 光驱（DVD-ROM 或 DVD 刻录机均可），且电脑必须能够从此光驱启动。（例外情况：你可以使用书末的优惠券订购 Fedora Core 的安装 CD。）具体的型号不重要，重要的是 DVD 光驱如何连接到电脑。大多数新电脑的 DVD 光驱连接到硬盘控制器（称为*IDE*，即集成驱动电子器件，或*ATA*，即 AT 附件）。如果你添加一个外置 DVD 光驱，它最有可能连接到 USB 端口。任何 IDE/ATA 或 USB DVD 光驱都可以在 Linux 下工作。
- **硬盘**：任何 IDE 磁盘驱动器都可以在 Linux 下工作。另一种硬盘控制器类型是 SCSI（小型计算机系统接口），Linux 也支持它。为了舒适地安装和体验 Linux，你需要大约 5GB 的硬盘空间。另一方面，为了体验 Linux 的 Live CD 版本（如 Knoppix），你不需要占用任何硬盘空间。
- **键盘**：所有键盘都与 Linux 和 X 窗口系统兼容。
- **调制解调器**：如果你计划拨号上网，你需要一个 Linux 支持的调制解调器。对于软件调制解调器（称为*软调制解调器*或*Win-modem*），你可能需要从制造商处下载驱动程序。（它可能免费也可能不免费。）




### 检查您的 PC 硬件

- **显示器**：显示器的类型并不是特别关键，除非它必须能够显示视频卡所使用的屏幕分辨率。屏幕分辨率以水平和垂直方向上的图像元素（*像素*）数量来表示（例如，1024 × 768）。安装程序可以检测大多数现代显示器。如果它未能检测您的显示器，您可以选择具有特定分辨率（如 1024 × 768）的通用显示器类型。您还可以通过其制造商和型号（可在显示器背面找到）来指定显示器。

- **鼠标**：安装程序可以检测鼠标。所有类型的鼠标（如 PS/2 或 USB）都适用于 Linux 和 X 窗口系统。

- **网卡**：并非所有 PC 都有网卡，但如果您有，安装程序通常可以检测并使用它。如果您遇到问题，请尝试查找其制造商和型号（如 Linksys LNE100TX 快速以太网适配器），以便您可以搜索 Linux 是否支持该网卡的信息。

- **处理器**：400 MHz Pentium II 或更高配置最佳。只要速度超过 400 MHz，以 *MHz*（兆赫兹）或 *GHz*（吉赫兹）表示的处理器速度就不那么重要。但越快越好。Linux 可以运行在其他 Intel 兼容处理器上，如 AMD、Cyrix 和 VIA 处理器。

- **内存（RAM）**：*RAM* 是您系统拥有的内存量。与处理速度一样，内存越多越好。您需要 256MB 内存来安装 Linux 和 X 窗口系统，并舒适地运行图形用户界面（GUI）桌面。

- **SCSI 控制器**：一些高性能 PC 拥有 SCSI 控制器，用于将磁盘驱动器和其他外设连接到 PC。如果您的 PC 恰好有 SCSI 控制器，您可能需要查找该控制器的制造商和型号。

- **声卡**：如果您的 PC 有声卡并且您希望在 Linux 中获得声音，必须确保其兼容性。您可以在成功安装 Linux 后配置声卡。

- **视频卡**：Linux 在文本模式下与所有视频卡（也称为 *显示适配器*）配合良好，但如果您想要图形界面，则需要一个能与 X 窗口系统配合工作的视频卡。安装程序可以检测受支持的视频卡并正确配置 X 窗口系统。但是，如果安装程序无法检测视频卡，知道您视频卡的制造商和型号会有所帮助。

- **打印机**：除了这些硬件之外，您还需要查找计划在 Linux 中使用的任何打印机的制造商和型号。

![](img/11709a8f88c8cd03868a929dc94c0e2b_60_0.png)

许多发行版，如 Debian GNU/Linux，运行在与 Linux 内核兼容的任何硬件上。有关 Linux 兼容硬件的信息，请参见 www.tldp.org/HOWTO/Hardware-HOWTO。

要检查您的 PC 硬件是否与 SUSE Linux 兼容，请访问 [SUSE Linux 硬件兼容性列表](http://hardwardedb.suse.de)。对于 MEPIS，请查阅 [MEPIS 硬件数据库](www.mepislovers.org/hwdatabase)。Ubuntu 的硬件兼容性列表位于 [https://wiki.ubuntu.com/HardwareSupport/](https://wiki.ubuntu.com/HardwareSupport/)。对于 Xandros Desktop，您可以在 [www.xandros.com/support/hcl.html](www.xandros.com/support/hcl.html) 找到硬件兼容性列表。

### 试用 Knoppix 启动光盘

在安装任何内容之前，试用随附光盘中的 Knoppix（K 不发音）是值得的。除了体验 Linux 桌面外，您还可以通过 Knoppix 执行一些额外的预安装工作。如果您决定安装除 Fedora 以外的发行版——Debian、MEPIS、SUSE、Ubuntu 或 Xandros——您可以将此书随附光盘上提供的 ISO 镜像文件刻录到 CD 或 DVD 上。您还可以使用 Knoppix 下的 QTParted 工具在硬盘上为 Linux 腾出空间。

要启动 Knoppix，请遵循以下步骤：

1. **从此书随附光盘启动您的 PC。**
   会出现一个 `boot:` 提示符。在此提示符下，您可以输入各种命令来控制启动过程。特别是，您可以输入命令来禁用某些可能导致安装失败的硬件检测类型。
2. **几分钟后，您会看到 Knoppix 使用的 KDE GUI 桌面。**
   现在您可以开始使用 Knoppix。

![](img/11709a8f88c8cd03868a929dc94c0e2b_61_0.png)

如果您在笔记本电脑上尝试 Knoppix 并在显示有关探测 SCSI（这是一种接口类型的名称）消息后挂起，请重新启动。当 `boot:` 提示符出现时，输入 **knoppix noscsi**。告诉 Knoppix 不检查 SCSI 应该能让您通过这个问题。对于在 ACPI（高级配置和电源接口）方面存在问题的 PC，请在启动提示符处输入 **knoppix acpi=off**。在启动提示符处按 F3 查看 Knoppix 启动选项列表。

在获得 Knoppix 桌面后，您可以开始探索 Knoppix。查阅本迷你书的第 4 章以获取更多关于试用 Linux 的信息。如果您想使用 Knoppix 刻录 CD 或调整硬盘分区大小，请参阅本章中“使用 Knoppix 刻录 CD 或 DVD”部分和“在 Knoppix 中使用 QTParted 调整分区大小”部分。

当您结束使用 Knoppix 时，选择 **主菜单::注销**，并从出现的 KDE 结束会话对话框中选择 **重新启动计算机**。在 Knoppix 关机后，移除 DVD 并按 **Enter**。

### 从 ISO 镜像刻录 CD 或 DVD

此书的随附光盘包含 Debian、MEPIS、SUSE、Ubuntu 和 Xandros 发行版，形式为 ISO 镜像，组织在 DVD 的 distros 文件夹内的独立文件夹中。要安装其中任何一个发行版，您必须首先将所选发行版的 ISO 镜像刻录到 CD 或 DVD，视情况而定。通常，您可以使用带有 CD/DVD 刻录机的 PC 执行此步骤，很可能是在使用 Microsoft Windows 的情况下，因为大多数新 PC 都预装了 Windows。另一种选择是从随附光盘启动 Knoppix，然后使用 Knoppix 刻录 CD 或 DVD。我在接下来的两节中描述了这些选项。

#### 使用 CD 刻录应用程序

在 Microsoft Windows 中，您可以使用 CD 刻录应用程序（如 Nero）将 ISO 镜像刻录到可记录 CD 上。如果您没有用于 Microsoft Windows 的 CD 刻录应用程序，请从 DVD 启动 Knoppix，并在图形桌面上选择 主菜单 > 多媒体 > K3b 以启动 CD/DVD 刻录应用程序。从 ISO 镜像刻录 CD 的具体步骤取决于您使用的 CD 刻录应用程序。一般步骤如下。（如果您有 DVD 刻录机，请使用相同的说明来刻录 DVD。）

1. **将随附 DVD-ROM 放入 PC 的 DVD 驱动器中。**
   如果您的 DVD 驱动器是 DVD/CD 组合刻录机，您必须首先将 Linux 发行版的 ISO 镜像文件从 DVD 复制到 PC 的硬盘上，以便您可以使用同一个驱动器刻录 CD。
2. **启动 CD 刻录应用程序。**
3. **从 CD 刻录应用程序打开镜像文件。**
   具体步骤取决于 CD 刻录应用程序。在 Knoppix 下的 K3b 中，从菜单中选择 工具 > CD > 刻录 CD 镜像。在其他 CD 刻录应用程序中，通常通过选择 文件 > 打开来完成此操作。从打开对话框中选择该发行版的 ISO 镜像文件。如果您不确定，请在应用程序的在线帮助中搜索有关从 ISO 镜像刻录 CD 的信息。
4. **将空白可记录 CD 放入 CD 刻录机中。**
5. **将 ISO 镜像刻录到可记录 CD 上。**
   通常，CD 刻录应用程序有一个工具栏按钮，您可以点击它将 ISO 镜像刻录到空白 CD 上。
6. **如果发行版有更多的 ISO 镜像，请对剩余的 ISO 镜像重复步骤 2 到 4。**

> 启动 CD 发行版以单个 ISO 镜像的形式提供，您可以将其刻录到单个 CD 上。其他发行版通常以多个 ISO 镜像的形式提供，您必须将每个镜像文件刻录到单独的 CD 上。




### 使用 Knoppix 烧录 CD 或 DVD

如果你拥有一个 DVD-ROM 光驱和一个独立的 DVD/CD 刻录机，你可以从随书附赠的 DVD 启动 Knoppix，然后使用 Knoppix 来烧录 CD 或 DVD。在这种情况下，Knoppix 将从 DVD-ROM 光驱运行，而你仍然可以在独立的 DVD/CD 刻录机上烧录 CD 或 DVD。

启动 Knoppix 后，通过点击桌面面板上的终端程序图标来打开一个终端窗口。你可以使用 `cdrecord` 命令来烧录 CD，使用 `growisofs` 命令来烧录 DVD。

以下是使用 `cdrecord` 将 ISO 映像烧录到空白可录 CD 上的步骤：

1. **输入 `cdrecord -scanbus`，并查看输出的最后一部分，该部分以 `scsibus0` 开头。**

例如，来自一台配有 DVD 刻录机的 PC 的该命令输出的相关部分如下：

![](img/11709a8f88c8cd03868a929dc94c0e2b_63_0.png)

请注意，在你想要使用的 DVD/CD 刻录机对应的三个由逗号分隔的数字。在此示例中，数字为 `0,0,0`。在第 5 步的 `cdrecord` 命令中，使用这些数字与 `dev` 选项配合使用。

2. **输入 `cd /cdrom/distros` 将目录更改为 ISO 文件在 DVD-ROM 上的位置。**

3. **使用 `cd` 命令更改到你要在 CD 上烧录的发行版 ISO 文件所在的子目录。输入 `ls -l` 以查看 ISO 文件的名称。**

4. **将一张空白可录 CD 放入刻录机。**

5. **输入以下命令来烧录 CD，但请将其中的 `filename.iso` 替换为你的发行版的 ISO 映像文件的名称：**

```
cdrecord -v -pad speed=1 dev=0,0,0 filename.iso
```

如果 `cdrecord` 命令不起作用，请直接从 Knoppix 桌面选择 主菜单→多媒体→K3b。这将启动 K3b CD/DVD 刻录应用程序。然后你可以按照“使用 CD 刻录应用程序”部分中的说明来烧录 CD。

将 DVD ISO 映像烧录到可录 DVD 上也很简单。步骤如下：

1. **输入 `cdrecord -scanbus`，并查看输出的最后一部分，该部分以 `scsibus0` 开头。**

例如，来自一台配有 DVD 刻录机的 PC 的该命令输出的相关部分如下：

```
scsibus0:
    0,0,0   0)  'SONY'      'CD-RW DRU-800A ' 'KY01' Removable
    0,1,0   1)  *   *   *   CD-ROM
    0,2,0   2)  *   *   *
    0,3,0   3)  *   *   *
    0,4,0   4)  *   *   *
    0,5,0   5)  *   *   *
    0,6,0   6)  *   *   *
    0,7,0   7)  *   *   *
```

请注意列表中列出 DVD 刻录机的从 0 到 7 的第二列数字。在此示例中，DVD 刻录机的编号为 0。对于此编号，在第 5 步的 **growisofs** 命令中，使用 `/dev/scd0` 作为设备名称。请记住将设备名称中的 0 更改为 **cdrecord -scanbus** 命令输出中对应你的 DVD 刻录机的数字。

2. **输入 `cd /cdrom/distros` 将目录更改为 ISO 文件在本书随书附赠的 DVD 上的位置。**

因为你从 DVD 启动了 Knoppix，所以 DVD 仍在 DVD-ROM 光驱中。

3. **使用 `cd` 命令更改到你要在 CD 上烧录的发行版 ISO 文件所在的子目录。输入 `ls -l` 以查看 ISO 文件的名称。**

4. **将一张空白可录 DVD 放入刻录机。**

5. **输入以下命令来烧录 DVD，但请将其中的 `filename.iso` 替换为你的发行版的 ISO 映像文件的名称：**

   **growisofs -dvd-compact -Z /dev/scd0=filename.iso**

本书 DVD 中包含的大多数 ISO 映像都小到足以放入 CD。然而，如果你愿意，你可以在 DVD 上烧录任何 CD ISO 映像。SUSE 的 ISO 映像需要 DVD。

### 为 Linux 预留空间

在典型的 Windows PC 中，Windows 位于一个大分区上，占用了整个硬盘。你需要缩小该分区并为 Linux 创建空间。在 Linux 安装期间，安装程序将使用空闲空间用于 Linux 分区。

若要试用任何 Live CD 发行版——Knoppix 或 MEPIS——你无需重新划分硬盘分区。只需从 Live CD 启动你的 PC，就可以开始使用这些发行版。MEPIS、SUSE 和 Xandros 安装程序可以非破坏性地缩小 Windows 分区（执行与 PartitionMagic 等工具相同的任务），因此你不需要预先执行重新分区步骤。如果你计划在硬盘上安装 Fedora Core、Debian 或其他任何 Linux 发行版，则必须重新划分硬盘分区。如果你想在 Windows 下调整磁盘分区大小，可以使用 Norton PartitionMagic（来自 Symantec）在所有 Microsoft 操作系统（从 Windows 95/98/Me 到 Windows NT/2000/XP）中调整大小并拆分磁盘分区。这是一款商业产品，因此你需要购买它才能使用。在我撰写本文时，Norton PartitionMagic 8.0 的标价为 69.95 美元。你可以在 www.powerquest.com/partitionmagic 上阅读关于它的信息并购买它。

![](img/11709a8f88c8cd03868a929dc94c0e2b_65_0.png)

如果你尚未拥有 PartitionMagic，没必要花钱购买。只需从本书随书附赠的 DVD 启动 Knoppix，然后使用 QTParted（一个图形界面工具）来调整 Windows 分区的大小。QTParted 可以调整 Windows 2000 和 XP 使用的 NTFS 分区的大小。

![](img/11709a8f88c8cd03868a929dc94c0e2b_65_1.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_65_2.png)

调整磁盘分区大小总是涉及丢失硬盘上所有数据的风险。因此，在使用诸如 PartitionMagic 等磁盘分区工具调整硬盘分区大小之前，请备份你的硬盘。在完成备份后——并在你对分区进行任何操作之前——请确保你可以从备份中恢复文件。

#### 使用 PartitionMagic 调整 Windows 分区大小

当你运行 PartitionMagic 时，它会在一个窗口中显示当前分区。如果你正在运行 Windows XP，你的硬盘通常有两个分区：一个包含 Windows XP 安装文件的小型隐藏分区，以及一个作为 C: 驱动器的巨大第二 NTFS 分区。你需要减小现有 C: 驱动器的尺寸。这样会在该分区之后创建未使用的空间。然后，在 Linux 安装期间，安装程序可以在未使用的空间中创建新的 Linux 分区。

若要使用 PartitionMagic 减小 Windows 分区的大小，请按照以下步骤操作：

1. 在 PartitionMagic 主窗口的分区映射中，右键单击分区并从上下文菜单中选择 调整大小/移动。

调整分区 对话框出现。

2. 在 调整分区 对话框中，单击并拖动分区的右边缘以将其减小到较小的尺寸。

对于大型硬盘（任何超过 10GB 的硬盘），将 Windows 分区减小到 5GB，并将剩余部分留给 Fedora Core。如果你不得不使用较小的驱动器，请尝试为 Linux 创建至少 4GB 的空间。

3. 单击 确定，然后单击 应用 以应用更改。在 PartitionMagic 完成更改后，单击 确定。

4. 重新启动 PC。

在缩小了原 C: 驱动器所在的分区后，你无需对剩余的硬盘空间做任何处理。在安装期间，Linux 安装程序将使用该空闲空间来安装 Linux。

#### 在 Knoppix 中使用 QTParted 调整分区

在 Knoppix 启动并出现图形桌面后，按照以下步骤操作以减小 Windows 分区的大小：

1. 从 Knoppix 桌面选择 主菜单 → 系统 → QTParted。

QTParted 窗口出现，该工具显示在你的 PC 上找到的驱动器。第一个硬盘以设备名称 /dev/hda 显示，第二个以 /dev/hdb 显示，等等。

2. 在 QTParted 窗口左上角的设备列表中，单击硬盘。

QTParted 在窗口左下角显示驱动器信息，并在右侧显示分区信息，如图 2-1 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_66_0.png)

3. 从右侧的分区列表中，单击你要调整大小的分区。





这通常会是尺寸最大的分区（注意图 2-1 中的 Size 列）。对于 Windows 2000 或 XP，分区类型为 ntfs，如分区列表中的 Type 列所示。在一台典型的新 PC 上，您应该能看到两个分区——一个较小的 fat16 分区和一个较大的 ntfs 分区。

-   4. 从 QTParted 菜单中选择 Operations:Resize（操作:调整大小）。

调整分区大小的对话框将出现（见图 2-2）。

![](img/11709a8f88c8cd03868a929dc94c0e2b_67_0.png)

> 图 2-2：在 QTParted 中通过此对话框调整硬盘分区大小。

-   5. 在 New Size（新大小）文本框中输入分区的新大小（参见图 2-2），以在该分区之后创建空闲空间。

您应选择一个大小，使得在分区之后获得 4000MB 或更多的空闲空间。您将能在对话框中的 Free Space After（分区后的空闲空间）字段中看到空闲空间的大小（见图 2-2）。

-   6. 单击 OK（确定）以关闭对话框。

在通过下一步之前，硬盘分区不会发生改变。

-   7. 从 QTParted 菜单中选择 File: Commit（文件:提交），以使分区更改生效。

现在分区已更改，您在 Windows 分区之后拥有了空闲空间。

在硬盘上为 Linux 创建空闲空间后，您可以使用从配套 DVD 上提供的 ISO 镜像文件刻录的 CD 或 DVD 来继续安装您选择的 Linux 发行版。

### 安装 Debian GNU/Linux

要安装 Debian（发音为 DEB-ee-um）GNU（有些人读作 GUH-new）/Linux，您首先需要从配套 DVD 中的 Debian 文件夹将 ISO 镜像刻录成 CD（参见本章前面的“从 ISO 镜像刻录 CD 或 DVD”部分）。

请注意，Debian 安装程序不会安装 X 窗口系统。您必须在安装完基础操作系统后，将 X 作为单独的包进行安装。

#### 安装概览

当您手头有了 Debian CD 后，您就准备好安装 Debian GNU/Linux 了。在您深入安装过程之前，以下是安装 Debian 主要步骤的概览：

-   1. 在开始安装之前，请记住收集有关您计算机硬件的信息，因为如果 Debian 安装程序无法检测到 PC 上的某些外围设备，您可能需要提供某些详细信息。
-   2. 从 Debian CD 启动 PC。PC 启动后，您会看到一个带有 `boot:` 提示符的启动屏幕。您可以按 Enter 继续，但如果系统挂起，您可能需要再次重新启动，并在 `boot:` 提示符下输入一些启动选项，例如 `linux acpi=off`。然后 Linux 内核启动并启动 Debian 安装程序。
-   3. 选择安装语言。
-   4. 配置网络接口。
-   5. 使用缩小 Windows 分区后释放的空间，创建将由 Debian 使用的硬盘分区。（参见本章中的“为 Linux 预留空间”部分。）至少，您需要创建一个 swap 分区和一个用于根文件系统的分区。
-   6. 安装并配置基础系统，其中包括 Linux 内核和 GNU 实用工具。
-   7. 配置并安装 GRUB 引导加载程序，以便它可以启动 Debian 以及安装在您硬盘上的其他操作系统。
-   8. 重新启动 PC 以启动基础 Debian 系统并完成配置步骤——例如设置时区、设置 root 密码以及创建普通用户账户。
-   9. 配置高级包工具（APT）以便进行进一步的包安装。您必须识别源，例如 CD（如果您有的话）和可以找到 Debian 包的 Internet 站点。安装程序提供了建议；您只需选择这些源即可。
-   10. 选择要安装的软件包，包括桌面环境和各种服务器。
-   11. 安装程序要么从 Internet 下载文件，要么从 CD 获取所需的文件，安装所有选定的软件，然后配置所有包，包括 X 窗口系统。完成配置后，安装程序启动 X 并显示图形登录屏幕。

安装完 Debian GNU/Linux 后，您可以使用 `apt-get` 命令行工具来安装其他包，甚至可以升级整个发行版。

#### 完成 Debian 安装

首先，将第一张 CD 插入您的 PC 的 DVD/CD 驱动器，然后重新启动 PC。PC 从 CD 启动并显示一个说 `Press F1 for help`（按 F1 获取帮助）的屏幕。按 F1 查看帮助索引是个好主意，它告诉您按各个功能键（从 F1 到 F10）可以获取哪些信息。表 2-1 总结了功能键提供的帮助信息。

表 2-1 Debian 安装程序启动屏幕上的功能键

| 功能键 | 显示内容 |
| :--- | :--- |
| F1 | 帮助索引 |
| F2 | 您的 PC 在安装 Debian 方面必须具备的内存和硬盘空间要求（最小安装至少需要 24MB 内存和 256MB 硬盘空间，但这未来可能会改变） |
| F3 | 从 CD 启动 Linux 的方式（例如，通过键入 **linux** 或 **expert** 或 **linux26** 或 **expert26**，每个加载不同的内核） |
| F4 | 您可以输入的启动参数概述，以及按功能键 F5、F6 和 F7 可获取的详细信息 |
| F5 | 用于特殊机器（如某些 IBM ThinkPad 和有显示问题的笔记本电脑）的启动参数 |
| F6 | 用于特殊磁盘控制器（如 Adaptec 151x, 152x, 1542, 274x, 和 284x）的启动参数 |
| F7 | 供安装程序使用的启动参数（例如，如果您不希望安装程序探测 USB，请添加参数 **debian-installer/probe/usb=false**） |
| F8 | 指向 www.debian.org 并告诉您如何获取帮助 |
| F9 | 对 Debian 项目的简要介绍 |
| F10 | 关于适用于 Debian GNU/Linux 的版权和保修信息 |

阅读完帮助信息后，您可以按 Enter 开始，或者键入 **linux** 后跟您 PC 所需的任何启动参数，例如 **acpi=off**。Linux 内核加载后，请按照以下步骤完成 Debian GNU/Linux 的安装。（请确保您的 PC 拥有宽带 Internet 连接，例如 DSL 或电缆调制解调器。）

##### 1. 从初始文本模式屏幕中选择语言、国家/地区和键盘布局。

使用方向键进行选择，每次选择后按 Enter。然后安装程序检测硬件并从 CD-ROM 加载 Debian 安装程序的组件。接着，安装程序使用动态主机配置协议（DHCP）配置网络，并提示输入主机名。

##### 2. 输入您计算机的主机名。

安装程序提示输入您系统的域名，并在文本输入字段中显示默认值。（默认值是安装程序从 DHCP 服务器获取的。）您可以简单地按 Enter 接受默认域名。然后 Debian 安装程序启动磁盘分区工具，该工具显示几个选项，如图 2-3 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_70_0.png)

##### 3. 如果您已为 Debian 创建了空闲空间，请选择默认选项“使用最大连续空闲空间”并按 Enter。

如果您的硬盘上已经有您想用于 Debian 的分区，请选择“手动编辑分区表”选项并按 Enter。安装程序将显示与现有分区列表一起的更多选项，如图 2-4 所示。

**安装 Debian GNU/Linux**

图 2-4：
您可以从此屏幕手动编辑磁盘分区。

![](img/11709a8f88c8cd03868a929dc94c0e2b_71_0.png)

您可以单击其中一个分区，然后编辑其特性——例如使用哪种文件系统——并为该分区选择一个挂载点。完成后，您可以完成分区并将分区表写入硬盘。（见图 2-5。）

图 2-5：
完成后，将分区表写入硬盘。

![](img/11709a8f88c8cd03868a929dc94c0e2b_71_1.png)

安装程序会警告您，所选分区上的数据将被销毁，在您选择“是”之后，它将完成分区并开始安装基础系统。


安装完基础操作系统后，安装程序会检测磁盘分区上是否存在其他操作系统，并建议将 GRUB 引导加载程序安装在硬盘的第一个扇区，即*主引导记录*（MBR）。

4. 安装 GRUB 引导加载程序并重启电脑。

安装程序完成引导加载程序的安装。随后，它会弹出光盘并重启电脑。电脑重启后，Debian 将启动并引导你完成一系列配置步骤。

5. 选择时区，并指示电脑硬件时钟是否设置为格林尼治标准时间（GMT）。

答案通常是否。

6. 输入 root（超级用户）密码。

7. 通过输入所需信息来设置普通用户账户：用户名、全名和密码。

8. 通过指定你希望 Debian 下载软件包的源来配置 APT。

你必须选择一个国家以及该国家内的一个服务器，以标识包含 Debian 软件包的 FTP 和 Web 存储库。如果你的电脑位于 HTTP 代理之后，你也可以指定该代理。（如果没有，则忽略此部分。）稍后，你可以使用 *apt-get* 命令安装或更新各种可用的 Debian 格式软件包。你还可以指定 CD 作为 Debian 软件包的来源，但如果你指定服务器作为来源，始终可以获取最新的软件。

9. 选择要安装的软件包。

使用上、下箭头键移动光标，并按空格键来选择或取消选择软件包。你可以从预配置的包中进行选择，包括：桌面环境、Web 服务器、打印服务器、DNS 服务器、文件服务器、邮件服务器以及 SQL 数据库。你也可以手动选择软件包。

![](img/11709a8f88c8cd03868a929dc94c0e2b_72_0.png)

如果你选择了桌面环境包，你将获得 X 窗口系统和 GNOME 桌面。

完成选择后，按 Tab 键高亮显示 OK，然后按 Enter 键。

随后，安装程序开始下载并安装所选的软件包。如果通过宽带电缆或 DSL 连接互联网，这一步可能需要大约一个小时才能完成。

10. 当安装程序提示信息以配置其已下载和安装的软件包时，回答配置问题。

XFree86 包（X 窗口系统）是安装程序配置的软件包之一。完成所有配置后，安装程序将启动 X，你将看到一个图形登录提示。

11. 在图形登录屏幕上登录。

默认情况下，Debian 安装程序安装 GNOME 桌面管理器（`gdm`），它会启动 GNOME 桌面。

就这样！你现在已经安装好并启动了 Debian。你可以按自己的节奏探索它，并随着对 Debian 了解的深入，根据需要安装更多软件包。

### 安装 Fedora Core

要安装 Fedora Core，请将本书的配套 DVD 插入 DVD 光驱并重启电脑。（在 Windows 中，选择“开始 > 关机”，然后从对话框中选择“重新启动”。）如果你使用 CD，安装步骤与使用 DVD 相同，只是在安装程序提示时需要更换 CD。

如果你的电脑尚未设置为从 DVD 光驱启动，你必须进入 Setup 以更改启动设备的顺序。

电脑开机后，它将从 DVD 加载 Linux 内核，然后 Linux 内核开始运行 Fedora Core 安装程序。在安装的剩余过程中，你将使用安装程序的 GUI 屏幕进行操作。

片刻之后，文本屏幕会显示欢迎消息和一个 `boot:` 提示符。欢迎消息会告诉你，通过按 F1 到 F5 中的一个功能键可以获得帮助。若要立即开始安装 Fedora Core，请按下 Enter 键。你也可以在 `boot:` 提示符下输入其他选项。例如，如果你认为 DVD 可能已损坏，请输入 `linux mediacheck` 并按 Enter 键以测试 DVD 介质是否存在问题。介质检查完成后，你可以继续安装。

在一台速度较快（400 MHz 或更高）的奔腾电脑上，通过配套 DVD-ROM 安装 Fedora Core 大约需要一个小时左右（假设你安装了几乎所有软件包）。

Fedora Core 安装程序会“探测”——尝试确定——特定硬件的存在，并相应地调整安装步骤。例如，如果安装程序检测到网卡，程序会自动显示配置电脑以在 Linux 下连接网络所需的屏幕。你可能会看到与以下章节中展示不同的屏幕序列；确切的序列取决于你电脑的具体硬件配置。

49 安装 Fedora Core
第一卷
第 2 章
安装 Linux

如果在安装过程中遇到任何问题，请查阅这本小册子的第 3 章。该章展示了如何排查常见的安装问题。

#### 选择键盘布局和安装类型

在安装的第一个阶段，在继续创建 Fedora Core 的磁盘分区之前，你需要完成许多步骤。第一个阶段的步骤如下：

1. **从屏幕上的语言列表中选择合适的语言，然后单击“下一步”进入下一步。**

每个屏幕左侧都有可用的在线帮助。你可以阅读帮助消息以了解在特定屏幕中应该做什么。

选择语言后，安装程序会显示键盘布局列表。

2. **选择适合你所在语言字符集的键盘布局（例如，在美国选择美国英语），然后单击“下一步”。**

安装程序会显示一个屏幕，询问你是要安装新系统还是升级旧的 Fedora Core 安装。

3. **对于新的 Fedora Core 安装，单击“安装”并选择安装类型。**

对于新安装，你必须选择以下安装类型之一——个人桌面、工作站、服务器或自定义。个人桌面、工作站和服务器安装通过以预定义的方式划分硬盘来简化安装过程。个人桌面安装会创建一个具有图形环境和生产力应用的 Fedora Core 系统。

工作站级安装还会安装图形环境以及软件开发工具。此类型的安装还会删除所有现有的 Linux 相关分区，为 Linux 创建一组新的分区。

服务器安装会设置所有互联网服务器，例如 Web 服务器、FTP 服务器和邮件服务器。默认情况下，服务器安装不会安装图形环境，但你随时可以添加 GUI 桌面的软件包。

为了获得最大的灵活性，请选择自定义安装。这样你就可以只选择想要尝试的软件包。

安装的下一个主要阶段是为在 Fedora Core 中使用而划分硬盘。

#### 为 Fedora Core 划分硬盘

Fedora Core 安装程序会显示一个屏幕（见图 2-6），在该屏幕上你可以指定如何划分硬盘。如果你单击当前选择（其右侧显示一个上下箭头），安装程序将显示以下关于划分和使用硬盘的选项：

![](img/11709a8f88c8cd03868a929dc94c0e2b_75_0.png)

- **移除所选驱动器上的所有分区并创建默认布局：** 此选项会导致 Fedora Core 安装程序移除所有分区，包括其他操作系统（如 Microsoft Windows）使用的分区。仅当你希望 Fedora Core 作为电脑的*唯一*操作系统时才使用此选项。如果你希望保留任何现有的 Windows 分区，请勿选择此选项。
- **移除所选驱动器上的 Linux 分区并创建默认布局：** 此选项会导致安装程序仅移除现有的 Linux 分区，并为安装 Fedora Core 创建新分区。如果你已在电脑上安装了任何版本的 Linux 并希望将其清除并安装最新版本的 Fedora Core，可以使用此选项。
- **使用所选驱动器上的空闲空间并创建默认布局：** 如果你使用 PartitionMagic 或 QT Parted 工具为 Linux 创建空间，请选择此选项，以使用硬盘上的空闲空间创建 Linux 分区。如果你在调整分区大小后在一台新电脑上安装 Fedora Core，此选项是正确的选择。

![](img/11709a8f88c8cd03868a929dc94c0e2b_75_1.png)

**图 2-6：** 从该屏幕中选择一个自动分区选项。




- **创建自定义布局：** 如果您有一个或多个已存在分区的硬盘，请使用此选项来指定哪些分区将用于安装 Fedora Core。

选择适当的选项，然后单击 *下一步*。例如，如果您选择第二个选项，Fedora Core 安装程序将显示一个对话框以确认您的选择，并指出现有 Linux 分区中的所有数据都将丢失。单击 *是* 以继续。安装程序将显示其已准备好的分区，如图 2-7 所示。此屏幕的具体外观取决于您硬盘当前的分区情况。

![](img/11709a8f88c8cd03868a929dc94c0e2b_76_0.png)

此磁盘设置屏幕显示了一个磁盘驱动器列表以及其中一个驱动器的当前分区信息。如果您希望接受这些分区而无需修改，请单击 *下一步* 继续。

> **警告！** 如果您的计算机内存不足（通常少于 128MB），安装程序会询问是否允许其写入分区表并激活交换分区。执行此操作后，您的硬盘分区将会被更改。只有当您确定要使用新分区并确实要安装 Fedora Core 时，才单击 *是*。

#### 设置关键系统参数

完成磁盘分区设置后，您几乎就可以开始安装软件包了。首先，Fedora Core 安装程序会提示您设置一些关键系统参数。具体来说，您需要执行以下操作：

- 安装引导加载程序
- 配置网络
- 设置时区
- 设置 root 密码

您可以相当快速地完成这些步骤。

##### 安装引导加载程序

安装程序会显示一个屏幕，您可以从中安装 GRUB 引导加载程序。（GRUB 是 GRAnd Unified Bootloader 的缩写。）引导加载程序是一个驻留在硬盘上的小程序，当您给 PC 加电时，它会启动操作系统。如果您的硬盘上有 Microsoft Windows，安装程序应能检测到 Windows 分区，并配置引导加载程序以同时加载 Windows。您可以查看引导加载程序配置并从引导加载程序配置屏幕编辑设置。

![](img/11709a8f88c8cd03868a929dc94c0e2b_77_0.png)

您可以完全跳过引导加载程序的安装。但是，如果您在安装 Linux 时选择不安装任何引导加载程序，即使 Linux 已安装在硬盘上，当重新启动 PC 时您将无法启动 Linux。您只能启动当前引导加载程序设置要加载的内容。

为了更高的安全性（防止任何人在没有密码的情况下启动您的系统），请勾选 **使用引导加载程序密码** 复选框。安装程序会显示一个对话框，您可以在其中为 GRUB 指定密码。

做出选择后，单击 下一步 以继续。

##### 配置网络

假设您的 PC 有网卡并且 Linux 内核检测到了该网卡，Fedora Core 安装程序将显示网络配置屏幕（如图 2-8 所示）。

从这个屏幕，您可以设置网卡的 IP 地址（以便网络中的其他 PC 可以与您的 PC 通信）。此屏幕显示了安装在您的 PC 上的网络设备（例如以太网卡）列表。对于每个网络设备，您可以指示如何设置 IP 地址。单击列表旁边的 编辑 按钮，会出现一个对话框，您可以在其中指定选项。

您可以使用 DHCP 自动指定网卡的 IP（Internet Protocol）地址，其中您的 PC 从 DHCP 服务器获取 IP 地址和其他网络信息。如果您的 PC 连接到 DSL 或电缆调制解调器路由器，通常就是这种情况。

只有当您的局域网中正在运行 DHCP 服务器时，才选择 DHCP。如果选择 DHCP，您的网络配置将自动设置，您可以跳过本节其余部分。

如果不使用 DHCP 配置网络，您必须提供 IP 地址和其他网络信息，例如主 DNS 和辅助 DNS 的 IP 地址（将机器名称（如 `www.amazon.com`）转换为 IP 地址的名称服务器）。输入所需的参数，然后单击 **下一步** 以继续。

##### 设置时区

完成网络配置后，选择时区——本地时间与英国格林威治当前时间之间的时差，这是标准参考时间（也称为格林威治标准时间或 GMT，以及 UTC 或世界协调时间）。安装程序会向您显示一个带有地图的 GUI，您可以从中根据地理位置选择时区。选择时区后，单击 **下一步** 以继续。

##### 设置 root 密码

安装程序显示“设置 Root 密码”屏幕，您可以从中设置 `root` 密码。Fedora Core 安装程序的早期版本允许您在此步骤添加一个或多个用户帐户，但在本版本中，当您首次运行 Fedora Core 时才有机会添加用户帐户。（参见本小册子的第 4 章。）

**图 2-8：** 从此屏幕配置网络选项。

![](img/11709a8f88c8cd03868a929dc94c0e2b_78_0.png)

*root* 用户是 Linux 中的*超级用户*——拥有在系统中执行任何操作的权限。您最好将那个帐户保留为您独占使用。您需要分配一个您能记住但其他人不容易猜到的密码。将密码长度设置为至少八个字符，包含字母和数字的混合，并且（为了保险）加入一些特殊字符，例如 `+` 或 `*`。

在第一行输入密码，然后在下一行重新输入密码。密码中的每个字符在屏幕上显示为星号（`*`）。只有两次输入匹配时，安装程序才会接受您的密码。此功能确保输入错误（或猜测）的密码不起作用。

在您继续安装其余部分之前，必须输入 *root* 密码。完成后，单击 下一步 按钮以继续安装。

#### 选择和安装包组

设置好关键系统参数后，安装程序将显示一个屏幕，您可以从中选择要安装的 Fedora Core 包组。选择包组后，您可以休息一下喝咖啡，让 Fedora Core 安装程序忙于格式化磁盘分区并将所有选定的文件复制到这些分区中。

*包组*由几个 Fedora Core 软件包组成。每个 Fedora Core 软件包又包含许多构成特定软件的文件。

![](img/11709a8f88c8cd03868a929dc94c0e2b_79_0.png)

图 2-9 显示了包含包组列表（实际上是软件组件）的屏幕，您可以选择安装它们。屏幕左侧显示包组类别，右侧显示当前选定类别的包组。一个图标、一个描述标签和一个复选框标识每个包组。

一些包组已经选中，如复选框中的对勾所示。请将选定的包组视为建议安装的最小软件包集合。但是，您可以选择安装任何或所有组件。使用鼠标在滚动列表中上下移动，并单击复选框以选择或取消选择该包组。

![](img/11709a8f88c8cd03868a929dc94c0e2b_79_1.png)

在实际生产环境中安装 Fedora Core 时，您只需安装确切需要的包组。但是，当您试图了解有关 Fedora Core 的所有内容时，您需要许多不同的软件包。如果您的硬盘有足够的空间（至少 6GB）用于 Linux 分区，请选择“Everything”包组以安装所有包组，这样您就可以尝试 Fedora Core 提供的全部内容。

Book I
Chapter 2
Installing Linux

![](img/11709a8f88c8cd03868a929dc94c0e2b_80_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_80_1.png)

除了从图 2-9 所示屏幕选择的包组外，Fedora Core 安装程序会自动安装大量运行 Linux 内核和您选择的应用程序所需的软件包。即使您没有从此屏幕选择任何单个包组，安装程序也会安装大量软件包（它们都仅用于运行核心 Linux 操作系统）以及一组最小工具。

![](img/11709a8f88c8cd03868a929dc94c0e2b_80_2.png)

每个包组都需要特定的软件包才能运行。Fedora Core 安装程序会自动检查任何软件包依赖关系，并显示您尚未选择的任何必需软件包的列表。在这种情况下，请安装必需的软件包。

选择要安装的包组后，单击 下一步 以继续。

然后，安装程序显示一个屏幕，通知您安装即将开始。单击 下一步 以继续安装。Fedora Core 安装程序格式化磁盘分区并安装软件包。在安装软件包时，安装程序显示状态屏幕以显示安装进度，包括需要安装的软件包总数、已安装数量、所需的硬盘空间估计量以及安装完成前的剩余时间估计。

![](img/11709a8f88c8cd03868a929dc94c0e2b_80_3.png)

硬盘格式化和安装可能需要相当长的时间。因此，您可以休息一下，大约 15 分钟后再回来查看。当您回来时，您可以从状态屏幕了解剩余时间，该屏幕会持续更新。





在所有软件包安装完成后，安装程序会显示一条消息，告知您安装已完成。弹出 DVD，然后单击“退出”按钮重启您的电脑。之后，您可以进行更多配置并安装额外的软件。

#### 首次启动后配置防火墙和 SELinux

在首次完成 Fedora Core 安装并重启电脑后，首次配置实用程序将引导您完成多项额外的配置步骤，包括接受许可协议、配置防火墙和 SELinux、选择显示颜色和分辨率、设置用户账户以及检查声卡。在这些步骤中，防火墙和 SELinux 的配置对系统安全至关重要，因此下面简要介绍这些步骤。

在防火墙和 SELinux 配置步骤中，您需要配置 Linux 内置的包过滤器，选择安全增强型 Linux（SELinux）访问控制级别，并根据需求自定义这些安全级别。

请注意，SELinux 是由美国国家安全局（NSA）开发的一个强制访问控制框架，该机构属于美国政府的一部分，SELinux 已集成在 Linux 内核 2.6 中。您可以在 NSA 网站 www.nsa.gov/selinux 上获取更多关于 SELinux 的信息。简而言之，SELinux 的访问控制超越了 Linux 中传统的基于进程或文件所有者的用户和组 ID 的访问控制。SELinux 将系统视为*主体*（用户或进程）和*对象*（文件、设备、任何系统资源）的组合。主体可以扮演不同的角色，例如*普通用户*或*系统管理员*。每个主体都有一个域，每个对象都有一个类型。SELinux 通过定义哪些域可以访问哪些类型以及当程序执行时一个域如何过渡到另一个域，从而提供对 Linux 系统中谁可以访问什么的细粒度控制。这听起来可能有些复杂，但您无需完全理解所有内容，就能享受 SELinux 提供的增强安全性。

对于防火墙，您需要选择以下选项之一：

- **禁用**表示防火墙未激活，您的系统将接受所有类型的连接，而不执行任何安全检查。仅当您的系统运行在可信网络上，或者您计划稍后设置防火墙配置时（越快越好），才使用此选项。
- **启用**表示您希望设置防火墙。这意味着您的系统不接受任何连接，除非您明确启用的连接。默认情况下，系统仅接受 DNS 和 DHCP 请求。然后，您可以选择允许通过防火墙的服务，例如邮件和 FTP。

对于 SELinux 访问控制配置，您可以将其设置为以下选项之一：

- **强制模式**表示 SELinux 执行强制访问控制。
- **宽容模式**表示 SELinux 打印警告消息，但实际上不强制执行访问控制策略。
- **禁用**表示 SELinux 已关闭。

您还可以在配置屏幕上修改 SELinux 策略，但将 SELinux 访问控制保持在其默认设置是安全的。

在您完成首次重启后的所有配置步骤后，单击“完成”即可进入 Fedora Core 的图形登录界面，开始使用 Fedora。

### 安装 ME Pis

随附 DVD 包含一张用于 MEpIS 发行版的单张 CD ISO 镜像——名为 SimplyMEPIS——您可以将其刻录到 CD 上，既可作为 Live CD 使用，也可作为安装 CD 使用。（顺便说一下，MEPIS 的发音是 MEE-pis。）当您从 MEpIS CD 启动时，MEpIS 将直接从 CD 运行，您会看到 MEpIS Live CD 登录界面，可以使用两个预定义的用户名之一（demo 或 root）进行登录。

- **运行 Live CD**：若要试用作为 Live CD 系统的 MEpIS，请在登录窗口中单击 Demo，并输入 demo 作为密码。
- **安装发行版**：若要安装 MEpIS，请在登录窗口中单击 Root 图标，并输入 root 作为密码。

当您以 root 身份登录时，您将看到带有红色背景的 MEpIS 桌面，如图 2-10 所示（相信我，它是红色的：红色背景提醒您当前是以 root 身份登录）。您可以从该桌面启动 MEpIS 硬盘安装。

要在您的电脑硬盘上安装 MEpIS，请遵循以下步骤：

1. 单击 MEpIS 桌面上的 INSTALL ME 图标（见图 2-10）。

MEpIS OS Center 窗口将打开（见图 2-11）。从 MEpIS OS Center，您可以执行多项系统配置和维护任务，包括将 MEpIS 安装到硬盘上。

![](img/11709a8f88c8cd03868a929dc94c0e2b_83_0.png)

2. 从 MEPIS OS Center 窗口左侧显示的任务列表中选择**在硬盘上安装 MEPIS**。

MEPIS OS Center 将在窗口右侧显示版权声明，如图 2-11 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_83_1.png)

3. 阅读版权声明，如果您同意，请单击“下一步”继续。

MEPIS OS Center 将显示安装的第一步，包括三个部分：

- 选择用于安装的硬盘。
- 运行 QTParted 以重新排列分区。此步骤是可选的，但如果您有现有的 Windows 分区并且需要为 MEPIS 创建空间，请单击“运行 QTParted”按钮，使用 QTParted 缩小 Windows 分区。（更多信息，请参阅本章中的“使用 Knoppix 中的 QTParted 调整分区大小”部分。）
- 选择是使用整个磁盘安装还是使用一组现有的硬盘分区。我在创建了一些分区后进行了安装，因此我选择了在现有分区上安装的选项。如果您选择在现有分区上安装，MEPIS OS Center 会提供选择文件系统根分区、/home 目录分区和交换分区的选项。您必须指定一个分区作为根分区，另一个作为交换分区。

4. 指定根分区——用于文件系统根部的分区——和交换分区，然后单击“下一步”。

MEPIS OS Center 将显示一个对话框，询问是否确认真的要格式化并销毁已分配分区中的所有数据。单击“是”以开始 MEPIS 安装。在将文件从 CD 复制到硬盘后，MEPIS OS Center 将继续安装 GRUB 引导加载程序并选择您希望启动的内核。

5. 选择是否将 GRUB 安装到主引导记录（MBR），以及您希望安装的内核版本——2.4 和 2.6。

通常可以接受默认选择，即将 GRUB 安装到 MBR 并启动 2.6 版本的内核。

6. 完成选择后，单击“下一步”继续。

7. 输入 root 密码并定义一个普通用户账户。然后单击“下一步”。

8. 输入计算机的主机名和域名以及 Windows 工作组名称。然后按 Enter。

9. 选择要启动的服务，包括 Guarddog 防火墙服务。同时选择显示驱动程序。然后单击“下一步”。

10. 设置键盘布局和时钟。然后单击“下一步”。

11. 单击“完成”以完成 MEPIS 安装。

最终安装步骤上的消息会告知您，可以在 www.mepis.org 或 www.mepislovers.com 获取 MEPIS 的社区支持。

取出 CD 并重启后，您将看到 GRUB 菜单，从中您可以从硬盘启动 MEPIS。然后，您可以使用安装 MEPIS 时定义的用户名以普通用户身份登录。

### 安装 SUSE Linux

由于 DVD 空间有限，随附 DVD 不包含来自 openSUSE 项目的完整 SUSE（我读作 SOO-za，但许多人发音不同）Linux 发行版。相反，DVD 包含用于 SUSE Live DVD 的 ISO 映像文件，该文件允许您直接从 DVD 运行 SUSE Linux。您可以从 http://ftp.opensuse.org/pub/opensuse/distribution/SL-OSS-stable/ 下载完整的 SUSE Linux 发行版。

![](img/11709a8f88c8cd03868a929dc94c0e2b_85_0.png)

若要试用 SUSE Linux Live DVD 版本，只需使用本书随附 DVD 上的 SUSE Live DVD ISO 镜像刻录一张 DVD，然后从该 DVD 启动您的电脑（您需要 DVD 刻录机将 ISO 文件刻录到 DVD 介质上）。

要安装完整的 SUSE 发行版，您有两种选择：

- 通过高速互联网连接，从镜像 SUSE Linux 发行版的其中一个 FTP 服务器直接安装完整发行版。
- 通过下载并刻录 http://ftp.opensuse.org/pub/opensuse/distribution/SL-OSS-stable/ 上的 SUSE Linux ISO 镜像中的 5 张 CD 来安装完整发行版，然后从第一张 CD 启动您的电脑。（关于刻录 CD 的说明，请参见本章中的“从 ISO 映像刻录 CD 或 DVD”部分。）

在以下几个部分中，我将首先介绍执行 FTP 安装的步骤，然后描述从 CD 安装完整 SUSE 的过程。

#### 执行 FTP 安装

要从镜像 SUSE 发行版的众多 FTP 服务器之一安装 SUSE Linux，您需要执行以下主要步骤：

1. 从 FTP 服务器下载 SUSE 引导映像，并使用该映像刻录一张 CD。
2. 记录 FTP 服务器的 IP 地址以及 SUSE 发行版文件所在的目录。
3. 使用引导 CD 启动电脑。在引导提示符处输入命令，开始从您通过其 IP 地址识别的 FTP 服务器进行 FTP 安装。





如果你拥有一台运行 Windows 且拥有高速互联网连接的 PC，你可以使用该 PC 下载启动映像并刻录启动 CD。你还可以使用 PC 查询 FTP 服务器的 IP 地址。

![](img/11709a8f88c8cd03868a929dc94c0e2b_86_0.png)

你还需要知道安装在你的 PC 上的网卡名称，因为在你开始 SUSE FTP 安装之前，必须手动加载驱动程序。在你下载 SUSE 安装程序的启动映像时，可以同时也找到 FTP 服务器的 IP 地址。我将在本节中解释这些步骤。

通过典型的宽带 DSL 或电缆调制解调器连接到 Internet 时，从 FTP 服务器安装 SUSE 可能需要两个小时或更长时间。请按照以下步骤通过网络从 FTP 服务器执行 FTP 安装：

- 1. 使用 Web 浏览器打开位于 www.suse.com/us/private/download/ftp/int_mirrors.html 的 FTP 服务器列表，并找到标记为 Complete（这意味着该服务器拥有完整的 SUSE 发行版及所有更新）的靠近你所在地的 FTP 服务器。

服务器列表按国家组织，包含 FTP 和 HTTP（Web）服务器。前往离你所在国家最近的章节，并选择标记为 Complete 的最近的服务器。

![](img/11709a8f88c8cd03868a929dc94c0e2b_86_1.png)

如果你在 Microsoft Windows 中执行此步骤，请打开命令提示符窗口（选择“开始 > 运行”，输入 cmd，然后按 Enter 键），输入 ping 后跟 FTP 服务器的名称（例如，mirror.mcs.anl.gov）。然后，你将在下一行看到 FTP 服务器的 IP 地址（例如，140.221.37.130）。记下该 IP 地址以备后用。

- 2. 点击 FTP 服务器链接，找到包含 boot.iso 文件的目录——这就是 SUSE 安装程序的启动映像。

该目录取决于 SUSE 的版本。例如，对于版本 10.0，boot.iso 文件位于 FTP 服务器的 pub/suse/i386/10.0/ 目录中。该文件的大小为几十兆字节。

- 3. 下载 boot.iso 文件并保存它。

- 4. 将 boot.iso 映像刻录到 CD 上。

使用你的 PC 的 CD 刻录应用程序来刻录名为 boot.iso 的 ISO 映像。

- 5. 转到你要执行 SUSE FTP 安装的 PC，插入启动 CD，并重新启动 PC。

如果未设置让你的 PC 从 CD 驱动器启动，你必须进入 Setup（通过在 PC 加电时按诸如 F2 等按键）并更改启动设备的顺序。

PC 重新启动后，经过几秒钟，会显示带有多个选项的 GUI 屏幕。使用方向键在列表项和屏幕上的按钮之间移动。例如，如果你的 PC 在 ACPI 方面存在问题，请选择禁用 ACPI 安装的选项。

- 6. 使用方向键选择安装选项并按 Enter 键。

这会加载 Linux 内核并运行安装程序。在检测和初始化硬件之后，安装程序会显示一条消息，说明它找不到 SUSE Linux 安装源，并且正在激活手动设置程序。这是正常的，你应该按 Enter 键继续。然后安装程序会显示语言列表。

- 7. 使用方向键选择语言并按 Enter 键。

安装程序会显示 *键盘映射* 列表——即依赖于语言的键盘布局。

- 8. 选择键盘语言并按 Enter 键。

安装程序会显示主菜单。

- 9. 使用方向键选择“开始安装”或“系统”并按 Enter 键。在下一个屏幕上，选择“开始安装”或“更新”并按 Enter 键。

安装程序会显示 *源介质* 列表——在这里你指定安装程序在哪里可以找到执行安装所需的文件。

- 10. 选择网络作为源介质并按 Enter 键。

安装程序会提示你选择网络协议。

- 11. 选择 FTP 作为网络协议并按 Enter 键。

一个对话框会提示你确定是否使用动态主机配置协议（DHCP）自动配置网络。如果你的网络使用 DHCP（大多数网络都是如此），请选择“是”并按 Enter 键。否则，你必须在此步骤中输入 IP 地址和名称服务器的 IP 地址。然后安装程序会提示输入 FTP 服务器的 IP 地址。

- 12. 输入你在步骤 1 中找到的 FTP 服务器的 IP 地址（例如，对于 FTP 服务器 *mirror.mcs.anl.gov*，输入 140.221.37.130）。

安装程序会提示你指示是否使用用户名和密码连接到 FTP 服务器。

- 13. 选择“否”并按 Enter 键。

回答“否”，因为 FTP 服务器支持 *匿名 FTP*——这意味着任何人都可以使用用户名 *anonymous* 登录。安装程序还会提示你指示是否使用 HTTP 代理。

- 14. 除非你的 PC 位于代理服务器之后（在某些组织中可能会遇到这种情况），否则选择“否”并按 Enter 键。

然后安装程序会提示输入 SUSE 文件所在目录的名称。

- 15. 输入 FTP 服务器上 SUSE Linux 文件所在目录的名称并按 Enter 键。

目录名称是你所在目录的父目录，该目录是你找到 `boot.iso` 文件的位置（步骤 2 中）。例如，如果 `boot.iso` 文件位于 `pub/suse/i386/10.0/boot/`，则你应该输入 `pub/suse/i386/10.0/` 并按 Enter 键。

安装程序会显示一条消息，告知它正在将数据加载到 RAM 磁盘（指充当硬盘的内存区域）。当安装程序完成数据下载（约 62MB 的数据）后，YaST（这就是 SUSE 安装程序的名字）启动并显示其初始 GUI 屏幕。

从这一点开始，安装步骤与从 CD/DVD 安装相同，我将在下一节中解释。你应该跳转到 YaST 安装程序显示其初始 GUI 屏幕的位置。

##### 从 CD 安装 SUSE Linux

要从本书配套 DVD 上的 ISO 映像刻录的 CD 安装 SUSE Linux，只需将第一张 CD 插入你的 PC 的 CD/DVD 驱动器并重新启动你的 PC。（在 Windows 中，选择“开始 > 关闭”，然后从对话框中选择“重新启动”。）注意，你可能需要进入 Setup 并确保你的 PC 设置为从 CD/DVD 驱动器启动。

当你的 PC 加电后，启动加载程序启动并显示带有项目菜单的初始启动屏幕。表 2-2 列出了每个启动菜单项目及其含义。如你所见，你可以从启动屏幕执行多项任务，包括从硬盘启动现有安装和启动救援系统。

**表 2-2 SUSE 安装程序启动菜单项目**

| 选择此项 | 以执行此操作 |
| :--- | :--- |
| 从硬盘启动 | 从硬盘上先前安装的操作系统的启动 PC |
| 安装 | 自动检测硬件并开始安装 SUSE Linux |
| 安装—禁用 ACPI | 禁用对 ACPI（高级配置和功率接口）的支持，但否则检测硬件并开始 SUSE 安装 |
| 安装 — 安全设置 | 禁用可能引起麻烦的功能，如 ACPI、APM（高级电源管理）和 IDE 接口的 DMA（直接内存访问），并开始安装 SUSE。如果安装在其他任何选项下挂起，请选择此选项。 |
| 救援系统 | 在内存中启动一个小型 Linux 系统，以便你可以登录为 **root** 进行故障排除 |
| 内存测试 | 检查 PC 的内存是否存在任何问题 |

在 SUSE 安装程序启动屏幕的底部，你会看到一些关于使用功能键 F1 到 F6 的信息。表 2-3 解释了这些功能键中的每一个的作用。

你还可以通过启动菜单下方的“Boot Options”文本框提供其他安装程序选项——以及 Linux 内核选项。*安装程序选项* 控制安装程序行为的某些方面，而 *内核选项* 则传递给你开始安装时启动的 Linux 内核。我在这个迷你书的第 3 章中解释了许多这些启动选项。

**表 2-3 在 SUSE 安装程序启动屏幕使用功能键**

| 按此功能键 | 以执行此操作 |
| :--- | :--- |
| F1 | 获取上下文相关的帮助——与当前选中项目相关的帮助信息。使用向上和向下箭头键阅读帮助屏幕，使用向左和向右箭头键在主题之间跳转。你可以通过按 Escape 键关闭帮助屏幕。 |
| F2 | 选择启动加载程序使用的语言和键盘映射。 |
| F3 | 选择你希望 YaST 安装程序用于其 GUI 的屏幕分辨率。如果 GUI 屏幕无法出现，你可以选择文本模式以获得文本模式界面。 |
| F4 | 选择你想要从中安装的源。选项包括：CD 或 DVD；或具有不同协议的网络源，如 FTP、HTTP、NFS 和 SLP（服务定位协议）。 |
| F5 | 更新新硬件的驱动程序模块，其驱动程序可能不在 CD 或 DVD 上。在你开始安装后，你将提示插入更新后的驱动程序模块在软盘或 CD-ROM 磁盘上。 |

![](img/11709a8f88c8cd03868a929dc94c0e2b_89_0.png)

安装程序最初为 GUI 屏幕选择一个相当高的屏幕分辨率（通常是 1280 x 1024 像素）。你应该按 F3，这会弹出一个菜单，你可以从中选择一个更合理的屏幕分辨率，如 1024 x 768 像素。




按下 F2 键设置屏幕分辨率后，从启动菜单中选择“安装”并回车。这将加载 DVD 中的 Linux 内核，Linux 内核随即开始运行 YaST 安装程序。在剩余的 installations 过程中，您将通过 YaST 的图形用户界面屏幕进行操作。

如果在安装过程中遇到任何问题，请查阅本书的小册子第 3 章。该章介绍了如何排查常见的安装故障。

##### 在 YaST 中启动 SUSE 安装

YaST——SUSE 安装程序——会显示一个图形用户界面屏幕（见图 2-12），通过该屏幕您可以将 SUSE Linux 安装到 PC 的硬盘上并进行配置。

YaST 屏幕的左侧显示了安装步骤列表，这些步骤被组织为两大任务类别：**基础安装**（Base Installation）和**配置**（Configuration）。箭头标记当前步骤。例如，在图 2-12 中，箭头标记的是“语言选择”步骤。当步骤完成后，YaST 会在该步骤旁边显示一个对勾标记。

![](img/11709a8f88c8cd03868a929dc94c0e2b_90_0.png)

在 YaST 屏幕的右侧（参见图 2-12），您会看到当前步骤的选项。您需要选择选项并点击 **Accept**（接受）以进入下一个安装步骤。在确认要真正继续安装之前，您随时可以点击 **Abort**（中止）按钮来终止安装过程。

在任何安装步骤中，点击 YaST 屏幕左下角的 **Help**（帮助）按钮（参见图 2-12）可以查看当前步骤的上下文相关帮助信息。帮助区域将显示在 YaST 屏幕的左侧。再次点击该按钮可返回查看安装步骤列表。

![](img/11709a8f88c8cd03868a929dc94c0e2b_91_0.png)

请按照以下步骤完成 YaST 安装程序中的基础安装任务：

1.  **选择安装期间以及已安装的 SUSE Linux 系统中使用的语言。点击 Accept（接受）。**
   - YaST 探测硬件并加载驱动程序模块。YaST 可能会提示您确认是否应加载某些驱动程序模块。随后，YaST 会显示一个**媒体检查**（Media Check）屏幕，让您有机会检查安装介质。点击 **Start Check**（开始检查）执行检查，完成后点击 **Next**（下一步）。YaST 将显示许可协议。

2.  **阅读许可协议，如果同意请点击 Yes（是）按钮。然后点击 Next（下一步）继续。**
   - YaST 会提示您指示这是一次新安装还是一次更新。

3.  **假设您是第一次安装 SUSE，请选择 New Installation（新安装）并点击 Next（下一步）。**
   - YaST 将提示您输入时区。

4.  **选择您的时区并点击 Next（下一步）。**
   - 您还可以点击 **Change**（更改）来修改当前的时间和日期，但通常这些设置是正确的。在此步骤之后，YaST 将提示您（见图 2-13）选择图形用户界面（GUI）桌面环境——GNOME 或 KDE，或其他选项，如最小化图形环境或不使用 GUI 桌面的文本模式系统。您对桌面环境的选择决定了 YaST 将安装哪些软件包。

5.  **选择您想要的桌面并点击 Next（下一步）。**
   - YaST 收集系统信息并准备所有安装设置的列表，初始显示在 **Overview**（概述）选项卡中。点击 **Expert**（专家）选项卡可以按类别查看设置的完整列表，如图 2-14 所示。表 2-4 总结了安装设置类别。请注意，您必须向下滚动才能看到图 2-14 所示屏幕中的所有安装设置。

![](img/11709a8f88c8cd03868a929dc94c0e2b_92_0.png)

### 安装 SUSE Linux

# 67

- 准备
  - 语言
  - 许可协议
  - 系统分析
  - 时区
  - 桌面选择
- 安装
  - 安装摘要
  - 执行安装
- 配置
  - 根密码
  - 网络
  - 在线更新
  - 用户
  - 时钟更新
  - 角色恢复
  - 硬件配置

1.  **KDE**
    KDE 是一个功能强大且直观的桌面环境，使用 Konqueror 作为文件管理器，并使用 Konqueror 作为浏览器和文件管理器。
2.  **GNOME**
    GNOME 是一个功能强大且直观的桌面环境，使用 Evolution 作为邮件客户端，Firefox 作为浏览器，Nautilus 作为文件管理器。
3.  **其他。**

![](img/11709a8f88c8cd03868a929dc94c0e2b_92_1.png)

- 系统：Compaq Presario 9922 · PCI/ISA-ABA DELL (0042 00840) [CPU (Intel(R) PENTIUM(R) D 935 3.4GHz (2 cores 2 units @ 2.50GHz)) 内存：700 MB]
- 键盘/字母
  - English (US)
- 分区
  - 格式化分区 /dev/sda (55290.1 MB) [用于交换分区]
  - 格式化分区 /dev/sda1 (1.32 GB) [用于交换分区]
  - 编辑 /dev/sda1 的挂载点为 /mnt/windowsC
  - 编辑 /dev/sda2 的挂载点为 /mnt/windowsD
  - 编辑 /dev/sda3 的挂载点为 /mnt/windowsE
  - 编辑 /dev/sda4 的挂载点为 /mnt/windowsF
- 软件
  - 标准系统（含 KDE）
  - KDE 桌面环境
  - 帮助和支持文档
  - 待安装的软件包集合 (1.5 GB)
- 启动
  - 引导加载程序类型：GRUB
  - Grub 启动设备：/dev/sda MBR [00480: 537574 (MBR)]
  - Grub 启动设备：/dev/sda1 MBR [00480: 537574 (MBR)]
  - Grub 启动设备：/dev/sda2 MBR [00480: 537574 (MBR)]
  - Grub 启动设备：/dev/sda3 MBR [00480: 537574 (MBR)]
  - Grub 启动设备：/dev/sda4 MBR [00480: 537574 (MBR)]

#### 表 2-4 安装设置类别

| **类别** | **这些设置指定的内容** |
|---|---|
| 系统 | 关于 PC 硬件的信息，包括处理器类型和内存容量 |
| 键盘布局 | 键盘的语言和布局 |
| 鼠标 | 鼠标类型（例如，PS/2 鼠标） |
| 分区 | 关于将被格式化的分区以及将挂载到 Linux 文件系统上的任何分区的信息。您应该检查以确保 YaST 使用您在为 Linux 预留空间时创建的未使用磁盘分区（如本章前面“为 Linux 预留空间”部分所述）。如果您的硬盘仅安装了 Microsoft Windows，YaST 会建议缩小 Windows 分区并创建安装 SUSE Linux 所需的其他分区。如果您除了 Windows 分区外还有其他分区，YaST 将选择适当的分区用于 SUSE Linux。然后，您可以点击“分区”标题，并在后续步骤中接受该建议或创建自定义分区设置。 |
| 软件 | YaST 将安装的软件。这取决于您在早期安装步骤中选择的 GUI 桌面——KDE 或 GNOME。 |
| 启动 | 关于负责在重启 PC 时启动 Linux（以及可能位于硬盘上的其他操作系统，如 Windows XP）的引导加载程序的信息。默认使用安装在硬盘主引导记录 (MBR) 上的 GRUB 引导加载程序。 |
| 时区 | 基于您在早期安装步骤中选择的当前时区以及日期和时间 |
| 语言 | 已安装的 SUSE Linux 系统所使用的语言 |
| 默认运行级别 | Linux 启动后启动的进程。默认运行级别为 5，这将为您提供一个启用网络并提供图形登录界面的完整多用户系统。 |

6.  **向下滚动安装设置列表，点击标题查看设置并进行任何更改。**
   - 您可以直接接受大多数设置。

7.  **检查完所有安装设置后，点击 Next（下一步）。**
   - YaST 将显示您在图 2-15 中看到的警告。它告诉您这是不可逆转的点。您可以点击 **Install**（安装）以确认安装，或者点击 **Back**（返回）回到安装设置。




### 安装 SUSE Linux

![](img/11709a8f88c8cd03868a929dc94c0e2b_94_0.png)

> **图 2-15：** 只有当你确定无疑时，才点击“安装”按钮。

8. 如果你确定要继续安装，请单击**安装**按钮。

YaST 开始安装过程，包括格式化和准备硬盘分区，并将 SUSE Linux 文件复制到硬盘。当 YaST 安装软件包时，它会展示一个幻灯片，介绍 SUSE Linux 的各种功能。完成基础安装后，YaST 会提示输入 root 密码。

9. 输入 root 用户的密码。

root 用户是管理员账户，你可以使用它执行系统上的任何操作——从安装软件到添加新的用户账户。

10. 接受或更改网络配置。

YaST 显示当前设置（参见图 2-16 中的示例）。如果设置正确，你只需单击“下一步”即可继续。

11. 测试互联网连接，并使用 YaST 在线更新服务更新系统。

如果有可用的更新，YaST 会询问你是否现在运行在线更新。单击“确定”以执行此操作，YaST 将自动选择一个镜像站点来下载更新。你只需单击“下一步”，单击“接受”，并按照 YaST 显示的说明进行操作即可。这一步可能需要较长时间才能完成，特别是如果有很多补丁需要下载和安装。在补丁下载和安装的最终步骤中，单击“完成”以继续 SUSE Linux 的其余安装过程。

12. 选择用户身份验证方法，然后单击“下一步”。

如果你没有可用的基于网络的身份验证，请选择本地身份验证。

![](img/11709a8f88c8cd03868a929dc94c0e2b_95_0.png)

图 2-16：在此屏幕上接受或更改网络配置。

对于网络身份验证，你必须从三种网络身份验证方法中选择一种 —— NIS（网络信息系统）、LDAP（轻量级目录访问协议）或 Samba（用于 Windows 网络）。

13. 对于本地身份验证，通过输入用户名、密码和其他设置来添加一个新的本地用户。单击“下一步”继续。

如果你勾选了“自动登录”复选框，SUSE Linux 在启动时将自动登录该用户。如果你的密码存在缺陷（例如使用用户名作为密码的一部分），YaST 会通知你这一问题，并询问你是否确实想要使用一个糟糕的密码。然后 YaST 将显示发行说明。

14. 阅读发行说明，然后单击“下一步”。

发行说明包含关于 SUSE Linux 发行版的最后时刻信息，包括任何已知问题和变通方法。值得浏览一下，以便你了解可能适用于你 PC 硬件配置的内容。

15. 接受或更改显示的你 PC 的硬件配置。

硬件配置包括有关特定硬件的信息（例如你的显卡、显示器、声卡、打印系统等）。通常，显示的配置应该是可接受的，但你应检查每一项。特别是检查显卡配置，看看 YaST 是否正确检测到了显示器和显卡。如果没有，你可以通过单击“显卡”并在后续窗口中更改信息来进行修改。配置步骤完成后，YaST 将通知你安装已完成。

16. 单击“完成”以结束安装。

安装程序重新启动系统。如果你安装了 KDE 图形用户界面（GUI）并在第 5 步中启用了自动登录，SUSE Linux 将重启，自动登录并显示 KDE 桌面。否则，你可以在 GUI 登录屏幕登录并开始使用系统。

#### 安装 Ubuntu

随书附赠的光盘包含用于安装 Ubuntu 的单张 CD ISO 镜像。首先，请按照本章“从 ISO 镜像烧录 CD 或 DVD”部分中概述的步骤，将该 ISO 镜像刻录到 CD-R 上。Ubuntu 基于 Debian，因此安装步骤与 Debian 类似。

要在你的 PC 上安装 Ubuntu，请遵循以下步骤：

1. 从 Ubuntu 安装 CD 启动你的 PC。
   初始启动屏幕提示你按 Enter 开始安装，或按 F1 获取更多帮助。你可以按 F1，查看通过按其他功能键可获得的帮助信息。由于 Ubuntu 基于 Debian，这些选项与你在 Debian 安装程序启动屏幕上获得的类似。若要查看功能键及其功能的摘要，请参阅表 2-1。

2. 按 Enter 或输入启动命令后跟任何选项，然后按 Enter。
   例如，在一条不支持 ACPI 的 PC 上，我输入 `linux acpi=off` 以开始安装 Ubuntu。安装程序提示你选择语言。

3. 选择语言并按 Enter。
   安装程序根据你的语言选择显示你的位置。

4. 选择位置并按 Enter。
   安装程序根据你的语言和位置显示你的键盘布局。

5. 选择键盘布局并按 Enter。
   安装程序检测硬件以找到 CD-ROM 驱动器，并从 CD 加载额外的软件。它检测网络硬件并使用 DHCP 进行配置。然后提示你输入主机名。

6. 输入你系统的主机名并按 Enter。
   安装程序检测硬盘并提示你选择磁盘分区方法。如果你已在硬盘上为 Ubuntu 创建了空间（参见本章中的“为 Linux 预留空间”部分），请选择“使用最大的连续空闲空间进行 Ubuntu 安装”选项。

7. 选择最大的连续空闲空间并按 Enter（或者选择现有分区并将其分配给特定的挂载点，如文件系统 `/root`）。
   安装程序安装 Ubuntu 基础系统，并询问系统时钟是否设置为 GMT（格林尼治标准时间）。答案通常是否。然后安装程序提示你输入时区。

8. 选择你的时区并按 Enter。

9. 创建一个用户账户。
   按照安装程序的提示输入用户的全名、用户名和密码。安装程序配置 APT——高级包工具——用于以后下载和安装包。
   安装程序列出它在你的 PC 硬盘上找到的所有已安装的操作系统，并询问你是否希望在硬盘的主引导记录（MBR）上安装 GRUB 引导加载器。

10. 选择“是”并按 Enter 以安装 GRUB。
    安装程序完成 GRUB 安装，然后卸载并弹出 CD。一条消息告知你安装的第一阶段已完成。移除 CD 并按 Enter 以重新启动 PC。

在 PC 重新启动后，Ubuntu 将从在线仓库下载并安装许多更多的包。（为了使一切正常工作，你的 PC 需要连接到互联网。）

![](img/11709a8f88c8cd03868a929dc94c0e2b_97_0.png)

X 窗口系统和 GNOME GUI 是 Ubuntu 下载和安装的包中的一部分。这些包安装并配置完成后，Ubuntu 将启动一个 GUI 登录屏幕，你可以使用之前定义的用户账户登录。如果由于某种原因 X 窗口系统无法工作，你必须按照本书第 3 章中的建议对 X 进行故障排除。

#### 安装 Xandros Desktop

随书附赠的光盘*不*包含完整的 Xandros Desktop 发行版（你可以将 Xandros 称为 ZAN*drose*，除非有人告诉你其他称呼），因为它是一种商业产品。相反，光盘包含一个名为*Xandros 开放循环版*（OCE）的限制版本的 ISO 镜像。你可以安装 Xandros OCE 来试用 Xandros Desktop，然后再决定是否购买完整发行版。在本节中，我描述了 Xandros OCE 的安装过程，这与完整发行版的安装过程类似，除了完整发行版包含更多的软件包。

要安装 Xandros OCE，请从本书随附光盘中的 Xandros OCE ISO 镜像刻录一张 CD，并从该 CD 启动你的 PC。有关说明，请参阅本章前面“从 ISO 镜像烧录 CD 或 DVD”部分。

![](img/11709a8f88c8cd03868a929dc94c0e2b_98_0.png)

初始 Xandros 启动屏幕显示一个标志和一条消息，内容为“按 Shift 键进入故障排除选项”。如果你什么都不做，Linux 内核将加载并启动一个 GUI 安装程序。但是，如果安装过程似乎挂起，请重新启动 PC，这次在启动屏幕按 Shift。然后你会看到一些用于启动 Linux 内核的选项。默认选项标记为“默认设置”，但你有选项可以尝试各种级别的 APM 和 ACPI 支持。使用上、下箭头键选择这些选项之一，并按 Enter 以解决安装过程中的问题。此外，如果你似乎无法进入 GUI 屏幕，请尝试选择 VESA 模式设置（查看表 2-5 以获取有关此选项的更多信息）。这可能有助于解决启动 X 窗口系统时的任何问题。表 2-5 总结了你可以通过在初始启动屏幕按 Shift 访问的 Xandros 启动选项。

| 选项 | 描述 |
| :--- | :--- |
| 默认设置 | 使用选项 `acpi=on`（启用对 ACPI 的支持）启动 Linux 内核 |
| ACPI 2 设置 | 使用选项 `acpi=on noapic`（启用 ACPI，但禁用 APIC——高级可编程中断控制器）启动 Linux 内核 |
| ACPI 3 设置 | 使用选项 `acpi=on pci=biosirq`（启用 ACPI，但使用 BIOS 设置来路由中断请求或 IRQ）启动 Linux 内核 |
| ACPI 4 设置 | 使用选项 `acpi=on pci=noacpi`（启用 ACPI 且不使用 ACPI 来路由中断请求）启动 Linux 内核 |
| APM 设置 | 使用选项 `acpi=off`（禁用 ACPI）启动 Linux 内核 |




## 74 安装 Xandros 桌面环境

表 2-5（续）

| 此选项 | 执行的操作 |
| :--- | :--- |
| APM 2 设置 | 启动 Linux 内核，选项为 `acpi=off noapic`（禁用 ACPI 和 APIC） |
| APM 3 设置 | 启动 Linux 内核，选项为 `acpi=off pci=biosirq`（禁用 ACPI 并使用 BIOS 设置来路由中断请求） |
| 256 色设置 | 以 256 色模式启动视频卡并运行 X 窗口系统（这应该在几乎所有视频卡上都能正常工作） |
| VESA 模式设置 | 使用 VESA（视频电子标准协会）驱动程序启动 X 窗口系统 |
| 自定义设置 | 启动 Linux 内核，选项为 `vga=normal`（屏幕显示为 80 × 25 文本模式） |
| 恢复 Xandros | 允许你恢复 Xandros 并修复问题 |
| 救援控制台 | 在 80 × 25 文本屏幕中以单用户模式启动 Linux 内核，在此处你可以以 `root` 身份登录并修复问题 |
| 国际选项 | 允许你选择非美国键盘和语言 |

通常情况下，你不需要做任何操作，因为引导加载程序会自动加载 Linux 内核和驱动程序模块。然后它会读取光盘，检测并配置硬件，并启动 X 窗口系统和图形界面安装程序。如果一切顺利，你应该能看到初始图形界面屏幕，如图 2-17 所示。点击**下一步**以继续安装。

下一个屏幕显示的是商业软件界臭名昭著的 EULA（最终用户许可协议）。（猜到了吧——那些喜欢玩弄文字的我们称之为 **YOOLa**。）如果你决定继续，请阅读 EULA，点击**我接受此协议**，然后点击**下一步**。

随后，Xandros 安装程序会显示两种安装选择：

- **快速安装**：以默认设置和你的 PC 上常用软件的选择来安装 Xandros。
- **自定义安装**：允许你控制安装 Xandros 的某些步骤，包括软件选择、Xandros 使用的磁盘分区以及网络配置。

我将在以下章节中介绍这两种安装方法。

![](img/11709a8f88c8cd03868a929dc94c0e2b_100_0.png)

图 2-17：
在此图形界面屏幕开始安装 Xandros。

##### 使用 Xandros 快速安装

Xandros 快速安装非常简单——前提是你希望 Xandros 使用整个硬盘或接管一个未使用的分区。简而言之，你需要输入 root 密码并创建一个普通用户帐户。然后查看安装摘要，点击完成，安装程序将完成其余工作。

![](img/11709a8f88c8cd03868a929dc94c0e2b_100_1.png)

如果你的 PC 上安装了 Windows，Xandros 安装程序将显示一个屏幕，询问你是保留 Windows 还是覆盖它。默认选项是保留 Windows。你可以表示你的选择并点击下一步继续。

下一个屏幕要求输入 root（管理员）密码和计算机名称。输入 root 密码并再次输入以确认。对于计算机名称，你可以接受 Xandros 安装程序生成的名称，或者输入对你来说更有意义的名称。然后点击下一步。

接下来，你有机会创建一个普通用户帐户。输入所需信息，包括用户名和密码，然后点击下一步。此用户名将用于登录 Xandros。

安装程序会显示一个安装摘要屏幕（如图 2-18 所示）供你查看。请仔细检查信息，特别是安装是接管一个分区还是整个硬盘。如果你需要修改，点击上一步。否则，点击完成开始安装。

安装程序完成 Xandros 安装后，会提示你重启 PC。当 Xandros 首次启动时，它会运行首次运行向导图形界面，引导你完成一些配置步骤。这些步骤包括设置日期和时间，以及选择货币和日期的显示方式。你还有机会配置打印机。

##### 使用 Xandros 自定义安装

自定义安装方法让你对安装哪些软件有一定的控制权。它还允许你指定用于安装的特定磁盘分区、配置网络并添加多个用户帐户。要使用自定义安装，请在安装选择屏幕上选择该选项——该屏幕出现在你接受 EULA 协议后立即显示——然后点击下一步，如图 2-19 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_101_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_102_0.png)

图 2-19：
在此屏幕选择自定义安装。

安装程序显示软件选择屏幕，你可以在此选择想要安装的应用程序。你可以从四个预定义的应用程序集中进行选择：

- **最小桌面**：安装一组基本应用程序
- **标准桌面**：安装一组推荐常用应用程序
- **完整桌面**：安装所有标准应用程序以及更多应用程序，例如一些服务器软件
- **自定义桌面**：安装一组基础软件（然后你可以从下方出现的列表中点菜式地选择应用程序）

当你点击选择这些集合中的任意一个时，你可以看到在这些选择下方出现的列表中的详细选择。你还可以从列表中添加或删除任何内容，因此预定义的集合不应限制你的选择。选择完想要安装的软件后，点击下一步。

然后，安装程序将引导你完成磁盘配置步骤。下一个屏幕，如图 2-20 所示，显示了安装程序的建议。如果你有可用的磁盘分区，安装程序建议接管硬盘或分区。（别担心，你会看到安装程序具体打算如何使用磁盘分区，如有必要，你可以进行干预。）

![](img/11709a8f88c8cd03868a929dc94c0e2b_103_0.png)

图 2-20：
Xandros 安装程序建议
其计划如何使用
硬盘。

如果你想管理磁盘分区，请点击“管理磁盘和分区”项，然后点击下一步。安装程序将显示一个编辑器，你可以在此删除和添加分区，并为分区指定挂载点。例如，你可以为 /boot 挂载点分配一个小的 50MB 分区，并为根文件系统（/）分配一个数 GB 的分区。你还可以指定一个大小约为可用内存两倍的交换分区。Linux 使用交换分区作为虚拟内存——基于硬盘的 PC 内存扩展。

表 2-6 总结了磁盘配置屏幕中可用的可能选项。（参见图 2-20。）请注意，只有适用于你 PC 的选项才可供选择。其他选项呈灰色显示。

表 2-6：磁盘配置选项

| 此选项 | 执行的操作 |
| :--- | :--- |
| 使用空闲空间 | 使用硬盘上最大的未分配空间块 |
| 接管磁盘或分区 | 接管整个硬盘、特定分区或旧版本的 Xandros 并擦除所有数据 |
| 调整 Windows 分区大小 | 缩小 Windows 分区的大小，并在腾出的空间中安装 Xandros |
| 替换现有的 Xandros 桌面操作系统 | 升级旧版本的 Xandros（保留用户帐户，为目录重命名添加 _old 后缀，并保留一些默认设置） |
| 管理磁盘和分区 | 允许你创建一个或多个磁盘分区，并为每个分区指定挂载点 |

如果你决定使用默认的“接管磁盘或分区”，点击下一步，Xandros 安装程序将显示它打算接管的分区。如果你同意，点击下一步。然后，安装程序以交换分区和根文件系统的位置形式显示磁盘配置，如图 2-21 所示。复选框显示安装程序将加载第一个 IDE 硬盘主引导记录上的引导管理器。

请注意，Xandros 安装程序使用 ReiserFS 文件系统用于磁盘分区。其他文件系统选择是 Ext2 或 Ext3。你可以选择默认的 ReiserFS。

![](img/11709a8f88c8cd03868a929dc94c0e2b_104_0.png)




#### 安装 Xandros 桌面

  查看磁盘配置后，单击**“下一步”**继续。安装程序将显示网络配置界面。默认情况下，动态配置以太网卡，这意味着使用 DHCP 获取网络接口和名称服务器的 IP 地址。如果这适用于您的网络，请单击**“下一步”**。否则，您需要单击**“编辑”**并输入网络的静态 IP 地址。您也可以选择不配置网络。完成网络配置步骤后，单击**“下一步”**。

  安装程序提示输入 `root` 用户密码。您还可以输入计算机名称。单击**“下一步”**继续后，安装程序将显示用户账户配置屏幕，您可以在此定义多个用户账户。对于每个用户账户，单击**“添加”**并输入所需信息。完成添加用户账户后，单击**“下一步”**。

  安装程序将显示安装摘要屏幕（见图 2-22）。

  仔细查看信息，如有错误请单击**“后退”**进行更正。确认所选内容可接受后，单击**“完成”**。安装程序完成 Xandros 的安装并提示您重启电脑。重启后，Xandros 将运行首次运行向导，引导您完成若干配置步骤。

  恭喜！您现在可以开始使用 Xandros 桌面了。

![](img/11709a8f88c8cd03868a929dc94c0e2b_105_0.png)

**图 2-22：** 自定义安装的摘要。

## 第 3 章：Linux 故障排除与配置

###### 本章内容

- 安装故障排除
- 配置 X 窗口系统
- 设置打印机
- 管理 DVD 和 CD-ROM
- 安装额外的软件包

  在安装 Linux 时，安装程序会尝试检测关键硬件组件，例如 SCSI 控制器和网络卡。根据检测结果，安装程序将引导您执行一系列安装步骤。例如，如果安装程序无法检测到网络卡，它将跳过网络配置步骤。如果您实际上没有网络卡，这完全没问题；但如果您有网络卡，而安装程序错误地坚持认为您没有，那么您就遇到了安装问题。

  另一种可能出现的安装问题是：当您重启电脑时，出现的不是图形登录屏幕，而是文本终端。这意味着 X 窗口系统（或*X*）配置出现了问题。

  此外，通常 Linux 安装并不包含针对您 PC 系统中所有硬件的配置程序。例如，大多数安装在安装过程中不会设置打印机。

  在本章中，我将展示一些排查安装问题的方法。我将向您展示如何配置 *X* 以 GUI 屏幕启动，以及如何配置打印机。

  您可能还需要从配套 DVD-ROM 安装额外的软件包。我将向您展示如何安装不同格式的软件包，例如 Red Hat 软件包管理器（RPM）和 Debian 软件包——这是大多数 Linux 软件发行的两种格式。

### 使用文本模式安装

  大多数 Linux 安装程序试图使用 X 窗口系统来显示图形安装屏幕。例如，如果安装程序未能检测到显卡，X 将无法启动。如果——无论出于此原因还是其他任何原因——安装程序未能启动 X，您始终可以回退到文本模式安装。然后，您可以手动指定显卡，或稍后使用独立的配置程序来配置 X。您还可以通过编辑其文本配置文件来配置 X。

  表 3-1 列出了如何从本书 DVD 中包含的 Linux 发行版初始安装程序屏幕进入文本模式安装。通常，文本模式安装序列与我在本书第 2 章中概述的图形安装类似。您响应提示并完成安装。

| 发行版 | 如何进入文本模式安装程序 |
| :--- | :--- |
| Debian | 在文本模式下工作 |
| Fedora Core | 从 Fedora Core CD 或 DVD 启动电脑后，在 boot: 提示符下输入**text** |
| Knoppix | 在 boot: 提示符下输入 **knoppix 2** 以文本模式启动 Knoppix（因为 Knoppix 是 Live CD 发行版，您无需安装它） |
| SUSE | 在第一个安装屏幕上，按 F3 并使用箭头键选择文本模式选项。按 Enter。 |
| Ubuntu | 基于 Debian 安装程序，并在**文本模式**下工作 |
| Xandros | 启动 CD 时按住 Shift 键并选择 Rescue Console。当出现 `bash-3.00#` 提示符时，输入 **quick_install** 并按照说明操作。 |

### 排查 X 故障

  我在旧电脑上每次安装 Linux 时都遇到过这个问题：安装期间，图形安装工作正常，但安装后首次重启电脑时，图形登录屏幕没有出现。相反，我最终遇到了文本登录屏幕，或者引导过程似乎挂起并显示灰色屏幕。如果您遇到此问题，以下是如何排查故障的方法：

1. 按 Ctrl+Alt+Delete 重启电脑。
   电脑开始引导。您会看到一个屏幕，GRUB 引导加载程序提示您选择要引导的操作系统。（如果发行版使用 Lilo 作为引导加载程序，您会看到一个文本提示符。）

2. **对于 GRUB，按 A 键添加供 Linux 内核使用的选项。对于 LILO，跳过此步骤。**
   然后，GRUB 引导加载程序将显示 Linux 内核的命令提示行，并提示您添加所需内容。

3. **对于 GRUB，输入空格后跟单词 single，然后按 Enter。对于 LILO，输入 linux single 并按 Enter。**
   Linux 内核将以单用户模式启动，并显示如下提示符：
   ```
   sh-3.00#
   ```
   现在您可以准备配置 X 了。

  X 使用配置文件（根据您的发行版不同，该文件名为 `XF86Config-4` 或 `xorg.conf`）来确定显示器类型、监视器以及您想要的屏幕分辨率类型。Linux 安装程序会准备配置文件，但有时配置并不正确。

  要快速创建可用的配置文件，请遵循以下步骤：

4. **输入以下命令：**
   ```
   X -configure
   ```
   这将导致 X 服务器运行并创建一个配置文件。屏幕会变黑，然后 X 服务器在显示一些消息后退出。消息的最后一行在 Fedora Core 中说明如下：
   ```
   To test the server, run 'X -config /etc/xorg.conf.new'
   ```

5. **使用文本编辑器（如 vi）编辑 `/etc/xorg.conf.new` 文件，并在“Files”行后插入以下行：**
   ```
   FontPath "unix/:7100"
   ```
   **在 Fedora Core 上，您还必须将 `/dev/mouse` 更改为 `/dev/input/mice`。**

6. **输入 xfs & 以启动 X 字体服务器。**

7. **在 Debian 和 MEPIS 上，通过输入 `X -xf86config /XF86Config.new` 来试用新的配置文件。在 Fedora Core、SUSE、Ubuntu 和 Xandros 上，通过输入 `X -config /etc/xorg.conf.new` 来试用新的配置文件。**
   如果您看到一个带有 X 形光标的空白屏幕，则配置文件工作正常。

8. **按 Ctrl+Alt+Backspace 终止 X 服务器。**

9. **使用以下命令将新的配置文件复制到 `/etc/X11` 目录（在 Debian 和 MEPIS 上，将第一个文件名更改为 `XF86Config.new`，第二个更改为 `XF86Config-4`）：**
   ```
   cp /etc/xorg.conf.new /etc/X11/xorg.conf
   ```

  现在您有了一个可用的 X 配置文件。

10. **按 Ctrl+Alt+Delete 或输入 reboot 重启电脑。**
    如果一切顺利，您应该会看到图形登录屏幕。

![](img/11709a8f88c8cd03868a929dc94c0e2b_109_0.png)

  使用 X 服务器的 -configure 选项创建的 X 配置文件无法以最佳分辨率显示。要微调配置文件，您必须在重启系统后运行实用程序来调整显示设置。确切的实用程序取决于您的 Linux 发行版，但大多数发行版都包含一个实用程序，允许您通过图形用户界面配置显卡、监视器和显示设置。

### 解决其他安装问题

  我相信我没有穷尽所有潜伏的安装问题。没有人能。Intel x86 电脑中有如此多不同的组件组合，墨菲定律实际上要求存在某种安装程序无法处理的硬件组合。本节列出了几个已知问题。对于其他问题，我建议访问 Google 小组（[http://groups.google.com](http://groups.google.com)）并输入一些故障症状。假设其他人也遇到了类似问题，您可以获得一些关于如何摆脱特定困境的排查方法的指示。

#### 使用 Knoppix 启动命令

  Knoppix Live CD 可以是一个很好的故障排除工具，因为 Knoppix 擅长检测硬件，并且您可以直接从 CD 运行它。当然，有时您可能会在启动 Knoppix 本身时遇到麻烦。如果发生这种情况，您可以尝试在 boot: 提示符下输入 Knoppix 启动命令。例如，如果 Knoppix 在尝试检测 SCSI 卡时似乎挂起，您可以通过在 boot: 提示符下输入 **knoppix noscs** 来禁用 SCSI 探测。或者，如果您希望 X 服务器加载 **nv 模块**（用于基于 NVIDIA 芯片组的显卡），您可以在 boot: 提示符下输入 **knoppix xmodule=nv**。表 3-2 列出了某些常见的 Knoppix 启动命令。

**表 3-2 一些常见的 Knoppix 启动命令**

| 启动命令 | 作用 |
| :--- | :--- |
| *expert* | 以专家模式启动，允许用户交互式设置和配置 Knoppix |
| failsafe | 引导时不尝试检测硬件（除了启动 Linux 所需的最低配置除外） |
| fb1280x1024 | 在指定分辨率下使用固定帧缓冲图形（指定您想要的分辨率，例如 1024 x 768、800 x 600 等） |




### 解决其他安装问题

##### 表 3-2 启动命令

| 启动命令 | 作用 |
| :--- | :--- |
| `knopix 1` | 以运行级别 1（单用户模式）启动 Knopix，可用于执行救援操作 |
| `knopix 2` | 以运行级别 2 启动，仅提供文本模式 shell 提示符 |
| `knopix acpi=off` | 完全禁用 ACPI（高级配置和电源接口） |
| `knopix atapicd` | 使用 ATAPI CD-ROM 接口，而不是为 IDE CD-ROM 驱动器模拟 SCSI 接口 |
| `knopix desktop=<wname>` | 使用指定的窗口管理器代替默认的 KDE（*wname* 可以是以下之一：*fluxbox*、*icewm*、*kde*、*larwm*、*twm*、*wmaker* 或 *xfce*。） |
| `knopix dma` | 为所有 IDE 驱动器启用直接内存访问（DMA） |
| `knopix floppyconfig` | 从软盘运行名为 *knopix.sh* 的 shell 脚本（该 shell 脚本包含您希望运行的 Linux 命令。） |
| `knopix fromhd=/dev/hda1` | 从之前复制到指定硬盘分区中的 Live CD 映像启动 |
| `knopix hsync=80` | 为 X 使用 80 kHz 的水平刷新率（输入您希望 X 使用的水平刷新率） |
| `knopix lang=xx` | 将键盘语言设置为由两位字母代码 *xx* 指定的语言（*xx* 使用以下之一：*cn* = 简体中文，*de* = 德语，*da* = 丹麦语，*es* = 西班牙语，*fr* = 法语，*it* = 意大利语，*nl* = 荷兰语，*pl* = 波兰语，*ru* = 俄语，*sk* = 斯洛伐克语，*tr* = 土耳其语，*tw* = 繁体中文，或 *us* = 美式英语） |
| `knopix mem=256M` | 指定 PC 拥有所述数量的内存（以兆字节为单位） |
| `knopix myconf=/dev/hda1` | 从 */dev/hda1* 分区运行 shell 脚本 *knopix.sh*（输入包含 *knopix.sh* 文件的分区名称。） |
| `knopix myconf=scan` | 使 Knopix 搜索名为 *knopix.sh* 的文件并执行该文件中的命令（如果存在） |
| `knopix noeject` | 在您停止 Knopix 后，不弹出 Live CD |
| `knopix noprompt` | 在您停止 Knopix 后，不提示移除 Live CD |
| `knopix noxwheelmouse` | 强制 PS/2 鼠标或触摸板使用 PS/2 协议（而不是自动检测） |
| `knopix noxxx` | 使 Knopix 跳过硬件检测的特定部分（其中 *xxx* 标识不应探测的硬件或服务器：*apic* = 高级可编程中断控制器，*app* = 加速显卡，*apm* = 高级电源管理，*audio* = 声卡，*d&d* = 显示数据通道，*dhcp* = 动态主机配置协议，*fsstab* = 文件系统表，*firewire* = IEEE 1394 高速串行总线，*pcmcia* = PC 卡，*scsi* = 小型计算机系统接口，*swap* = 用作虚拟内存的硬盘空间，*usb* = 通用串行总线） |
| `knopix pci=bios` | 对于有问题的 PCI 控制器，直接使用 BIOS |
| `knopix pnpbios=off` | 跳过即插即用（PnP）BIOS 初始化 |
| `knopix screen=1280x1024` | 将屏幕分辨率设置为 1280 x 1024 像素（输入您想要的分辨率，例如 1024×768、800×600、640×480 等） |
| `knopix testcd` | 使用 MD5 校验和检查 Live CD 的数据完整性 |
| `knopix tohd=/dev/hda1` | 将 Live CD 复制到指定的硬盘分区并从中运行 |
| `knopix toram` | 将 Live CD 复制到 RAM（内存）并从中运行（需要 1GB 的 RAM） |
| `knopix vga=ext` | 使用 50 行文本模式显示 |
| `knopix vsync=60` | 为 X 使用 60 Hz 的垂直刷新率（输入您希望 X 使用的垂直刷新率） |
| `knopix wheelmouse` | 为滚轮鼠标启用 IMP5/2 协议 |
| `knopix xmodule=modname` | 使 X 服务器加载由 *modname* 指定的模块，以便 X 在您的显卡上正常工作（*modname* 可以是 *ati*、*fbdev*、*i810*、*mga*、*nv*、*radeon*、*savage*、*svga* 或 *s3* 之一。） |
| `knopix xserver=progname` | 启动由 *progname* 指定的 X 服务器（可以是 *XFree86* 或 *XF86\_SVGA* 之一） |

![](img/11709a8f88c8cd03868a929dc94c0e2b_111_0.png)

当拥有多个 Knoppix 启动命令时，只需将它们组合到一行中即可。例如，要指定跳过 SCSI 自动检测、关闭 ACPI、使用美式键盘、滚轮鼠标，并要求 X 服务器加载 *nv* 模块，请在 `boot:` 提示符下输入以下内容：

```
knoppix noscsi acpi=off lang=us wheelmouse xmodule=nv
```

##### 致命的信号 11 错误

一些人在安装过程中遇到致命的信号 11 错误消息——这会彻底停止进程。此错误通常发生在初始启动屏幕之后，安装程序开始其 GUI 或文本界面时。安装过程中发生信号 11 错误的最可能原因是与内存或 CPU（微处理器）相关的缓存有关的硬件错误。

####### 技术细节

信号 11，也称为 SIGSEGV（段错误信号的缩写），可能发生在 Linux 应用程序中。当进程试图访问其不应访问的内存位置时，就会发生*段错误*。操作系统会在问题发生之前捕获它，并通过发送信号 11 来停止违规进程。如果在安装期间发生这种情况，意味着安装程序在访问内存时发生了错误，最可能的原因是硬件问题。针对信号 11 问题的常见建议解决方法是在 BIOS 中关闭 CPU 缓存。为此，您必须在 PC 启动时进入设置界面（通过按功能键，如 F2），并从 BIOS 设置菜单中关闭 CPU 缓存。

如果问题是由内存中的硬件错误引起的（换句话说，是由于内存芯片故障造成的），您可以尝试交换内存模块及其插槽。如果您手边有备用内存模块，也可以考虑用其替换现有的内存模块。

您可以访问 www.bitwizzard.nl/sig11 阅读更多关于信号 11 问题的信息。

##### 绕过 PC 重启问题

在某些 PC 上，当您在启动提示符处按 Enter 键时，初始 Linux 内核会加载并立即重启 PC。这可能是由于 PC BIOS 中 ACPI 实现不良所致。为了绕过此问题，在启动提示符处键入 **linux acpi=off** 以关闭 ACPI；如果不起作用，请查阅表 3-3 以获取您可能希望尝试的其他启动选项。

##### 使用 Linux 内核启动选项

当您将 PC 引导以进行 Linux 安装时，无论是从 DVD 还是第一张 CD-ROM，您都会看到一个带有 **boot:** 提示符的文本屏幕。通常，您在该提示符处按 Enter 键或不进行任何操作，安装程序不久后就会开始。然而，您可以在 **boot:** 提示符处指定相当多种类的选项。这些选项控制 Linux 内核启动的各个方面，例如禁用对问题硬件的支持或使用特定的 X 驱动模块启动 X 服务器。其中一些启动选项可以帮助绕过您在安装过程中可能遇到的问题。

要使用这些启动选项，通常您需要键入 **linux** 后跟启动选项。例如，要执行文本模式安装并告知内核您的 PC 有 512MB 内存，请在 **boot:** 提示符处输入以下内容：

```
linux text mem=512M
```

请查阅表 3-3，其中简要总结了一些 Linux 启动选项。您可以使用这些命令来开启或关闭某些功能。

尽管我在排查安装问题的背景下提到了这些 Linux 内核启动命令，但您可以随时在任何 Linux 发行版启动 PC 时使用其中许多命令，以开启或关闭特定功能。

##### 表 3-3 一些 Linux 启动选项

| 使用此启动选项 | 以执行此操作 |
| :--- | :--- |
| *allowcdma* | 为 CD/DVD 驱动器启用 DMA |
| *apic* | 规避在 Intel 440GX 芯片组 BIOS 中经常遇到的 bug，并且仅在安装程序内核中执行 |
| *acpi=off* | 在存在 ACPI 问题时禁用 ACPI |
| *dd* | 在安装 Red Hat Linux 时提示插入驱动盘 |
| *display=* IP_address:0 | 使安装程序 GUI 出现在由 IP 地址标识的远程系统上。（确保您在远程系统上运行命令 *xhost +hostname*，其中 *hostname* 是您运行安装程序的计算机的主机名。） |
| *driverdisk* | 在安装 Red Hat Linux 时提示插入驱动盘 |
| *enforcing=0* | 关闭增强型 Linux 安全（SELinux）强制访问控制 |
| *expert* | 允许您分区可移动介质，并提示插入驱动盘 |
| *ide=nodma* | 禁用所有 IDE 设备上的 DMA，在遇到 IDE 相关问题时可能很有用 |
| *ks* | 使用 DHCP 配置以太网卡，并通过使用由 DHCP 服务器提供的引导服务器参数标识的 NFS 服务器上的 kickstart 文件运行 kickstart 安装 |
| *ks=kskickstartfile* | 通过由 *kskickstartfile* 指定的 kickstart 文件运行 kickstart 安装。（kickstart 背后的理念是创建一个包含所有安装选项的文本文件，然后通过引导并提供该 kickstart 文件作为输入来启动安装。） |
| *lowres* | 强制安装程序 GUI 以较低的分辨率（640 x 480）运行 |
| *mediacheck* | 提示您检查 CD 映像（也称为 ISO 映像）的完整性。检查映像是通过计算 MD5 校验和并将其与官方 Fedora Core 值进行比较来完成的。检查 CD-ROM 可能需要几分钟时间。 |
| *mem=xxxM* | 覆盖内核在 PC 上检测到的内存数量。（一些旧机器只能检测 16MB 的内存，而在一些新机器上，显卡可能会使用主内存的一部分。）请确保将 *xxx* 替换为表示您 PC 内存兆字节数的数字。 |
| *nmi_watchdog=1* | 启用利用不可屏蔽中断（NMI）的内核内置死锁检测器 |




### 解决其他安装问题

使用以下引导选项可解决特定的安装问题：

| 使用此引导选项 | 用于执行此操作 |
| :--- | :--- |
| noapic | 防止内核使用高级可编程中断控制器 (APIC) 芯片。（对于已知 APIC 存在故障的主板，可以使用此命令。） |
| nofirewire | 不加载 FireWire 支持 |
| noht | 禁用超线程技术，这是一种使单个处理器在硬件级别上表现得如同多个虚拟处理器的功能。 |
| nomce | 禁用通过机器检查异常 (MCE) 对 CPU 执行的自检检查。在某些机器上，这些检查执行过于频繁，需要将其禁用。 |
| nomount | 在救援模式下不自动挂载任何已安装的 Linux 分区 |
| nopass | 不将键盘和鼠标信息传递给安装程序的阶段 2 |
| nopcmcia | 忽略系统中的任何 PCMCIA 控制器 |
| noprobe | 禁用自动硬件检测，转而提示用户输入有关 PC 上安装的 SCSI 和网络硬件的信息。可以使用这种方法向模块传递参数。 |
| noshell | 在安装期间禁用虚拟控制台 2（通过按 Ctrl+Alt+F2 进入的控制台）上的 shell 访问 |
| nousb | 在安装期间禁用 USB 支持的加载。（如果在安装过程早期发生挂起，这可能很有用。） |
| nousbstorage | 在安装程序的加载器中禁用 usbstorage 模块的加载。这可能有助于解决 SCSI 系统中的设备排序问题。 |
| reboot=b | 改变内核尝试重启 PC 的方式，使其即使在内核于系统关机期间挂起时也能重启 |
| pci=noacpi | 导致内核不使用 ACPI 来路由中断请求 |
| pci=biosirq | 导致内核使用 BIOS 设置来路由中断请求 (IRQs) |
| rescue | 以救援模式启动内核，此时你会得到一个 shell 提示符，并可以尝试修复问题 |
| resolution=HHHXVVV | 使安装程序 GUI 在指定的视频模式下运行。（请确保将 HHHH 和 VVVV 替换为标准分辨率数字，如 640x480、800x600、1024x768 等。） |
| selinux=0 | 禁用 SELinux 内核扩展 |
| serial | 在安装期间启用串行控制台支持 |
| skipddc | 跳过对显示器的显示数据通道 (DDC) 探测。（如果探测会导致问题，这很有用。） |
| vnc | 启动 VNC (虚拟网络计算) 服务器，以便你可以从运行 VNC 客户端的另一台联网系统控制 GUI 安装程序 |

### 设置打印机

在大多数 Linux 发行版中，只有在安装完该发行版之后才能设置打印机。以下部分概述了本书 DVD 中每种发行版的打印机配置步骤——Debian、Fedora Core、Knoppix、MEPIS、SUSE、Ubuntu 和 Xandros。

#### 在 Debian 中配置打印机

Debian 附带 foomatic-gui 实用工具，该工具允许你通过图形界面配置打印机，如图 3-1 所示。要配置打印机，请将打印机连接到相应的端口——并口或 USB——并打开电源。然后按照以下步骤操作：

1.  在 GUI 桌面上选择 **应用程序 → 系统工具 → 打印机** 以启动 foomatic-gui。
    - 如果你未以 root 身份登录，对话框将提示你输入 root 密码。
    - 如果你找不到菜单项，请打开一个终端窗口，输入 `su -` 以 root 身份登录，然后输入 `export DISPLAY=:0.0; foomatic-gui`。foomatic-gui 实用工具将显示其主窗口，如图 3-1 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_115_0.png)

**图 3-1：** 使用 foomatic-gui 在 Debian 中配置和管理打印机。

2.  点击工具栏上的 **添加**。 （参考图 3-1。）
    - foomatic-gui 工具将启动添加打印机向导（见图 3-2），该向导将引导你完成向系统添加新打印机的过程。

**图 3-2**：添加打印机向导引导你完成步骤。

![](img/11709a8f88c8cd03868a929dc94c0e2b_116_0.png)

3.  点击“下一步”。
    - 添加打印机向导会显示多种不同的打印机连接类型。
4.  从列表中选中你的打印机连接。
    - 要添加网络连接的打印机，点击“检测网络打印机”，你将看到网络上可用的打印机列表，包括 Windows 打印机。选择打印机连接后，foomatic-gui 会要求为用于保存该打印机打印作业的队列命名。
5.  输入打印机队列的名称以及打印机的标识信息（位置和简要描述），然后点击“下一步”。
    - foomatic-gui 工具将显示打印机制造商和型号列表。
6.  选择打印机的制造商和型号，然后点击“下一步”。
    - foomatic-gui 工具将显示适用于此打印机的驱动程序。
7.  选择你要使用的驱动程序，然后点击“下一步”。
    - 选择标记为“推荐”的驱动程序。foomatic-gui 工具将显示一条消息，告知你可以通过点击“应用”来添加打印机。
8.  点击“应用”以添加打印机。
    - 从 foomatic-gui 窗口（参考图 3-1），你可以选择一台打印机并点击“测试页”按钮来打印测试页。

#### 在 Fedora Core 中配置打印机

Fedora Core 安装程序不包含打印机配置步骤，但你可以通过图形实用程序轻松配置打印机。要设置打印机，请按照以下步骤操作：

1.  从 GNOME 桌面上，选择 系统::管理::打印。
    - 如果你未以 `root` 身份登录，打印机配置工具将提示你输入 `root` 密码。该打印机配置工具称为 `system-config-printer`。图 3-3 显示了其主窗口。

![](img/11709a8f88c8cd03868a929dc94c0e2b_117_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_117_1.png)

2.  点击 **新建** 按钮以配置新打印机。
    - 启动 Fedora Core 的打印机配置向导。初始窗口会显示一条消息，保证你在点击所有步骤结束时的“应用”按钮之前不会有任何更改。
3.  点击 **下一步** 继续。
4.  输入打印队列的名称和打印队列的简短描述。然后点击 **下一步**。
    - 在命名打印队列时使用系统化的方法。例如，如果在 210 房间二层有一台 HP Laserjet 5000 打印机，我可能会将队列命名为 Room210HPLJ5000，因为这个名字使查找打印机更容易。有时系统管理员会选择可爱的名字，如 `kermit`、`piggy`、`elmo`、`cookiemonster` 等，但当你拥有大量打印机时，这种可爱的命名方式并不起作用。在打印队列名称中提供关于打印机位置以及制造商和型号的线索是最好的。
5.  在下一个屏幕（见图 3-4）中，从下拉列表中选择一个队列类型。然后点击 **下一步**。

![](img/11709a8f88c8cd03868a929dc94c0e2b_117_2.png)

-   选择适用于你情况的打印队列类型。例如，如果你想打印到共享的 Windows 打印机，请选择 Networked Windows (SMB)。

![](img/11709a8f88c8cd03868a929dc94c0e2b_118_0.png)

-   要设置连接到 PC 并口的打印机，请选择 Locally-connected。

可用的打印队列类型如下：

-   **Locally-connected**：指直接连接到 PC 的串行、并口或 USB 端口的打印机。
-   **Networked CUPS (IPP)**：指网络中另一台服务器上的通用 UNIX 打印系统 (CUPS) 打印队列（IPP 指用于与远程 CUPS 服务器通信的互联网打印协议）。
-   **Networked UNIX (LPD)**：指由本地网络上另一台 UNIX 系统上的 LPD 服务器管理的打印队列。（LPD 指行打印机守护程序——另一种用于 UNIX 系统的打印假脱机程序。）
-   **Networked Windows (SMB)**：指连接到本地网络上另一台使用 *服务器消息块 (SMB) 协议* 的 PC 的打印机，这是 Windows 文件和打印共享的底层协议。
-   **Networked Novell (NCP)**：指连接到本地网络上 Novell Netware 服务器的打印机。
-   **Networked JetDirect**：指直接连接到本地网络的 HP JetDirect 打印机。

6.   如果你选择 Locally-connected，屏幕下半部分将显示有关检测到的并口的信息。点击端口以选择它，然后点击“下一步”继续。
    - 对于其他选项，屏幕会提示你标识网络打印机。指定网络打印机的方式取决于网络类型。例如，要在局域网中 IP 地址为 192.168.0.8 的主机上使用网络 CUPS 打印机，你必须输入诸如 [http://192.168.0.8:631/printers/HPLaserJetRoom210](http://192.168.0.8:631/printers/HPLaserJetRoom210) 这样的名称，其中 *HPLaserjetRoom210* 是网络打印机的名称。





7. 选择打印机的制造商和型号，然后单击“下一步”。

单击下拉列表（位于滚动列表上方）以显示打印机制造商列表。当您从此列表中选择某个打印机制造商时，滚动列表将显示该制造商提供的不同打印机型号的名称。如果您使用的是 PostScript 打印机，可以直接转到通用列表（通用是制造商列表中的选项之一）并选择 PostScript 打印机。

最后一个屏幕显示新打印队列的相关信息。

8. 复核所有信息以确保其正确，然后单击“完成”以创建打印队列。

9. 当出现询问是否要打印测试页的对话框时，单击“是”。

这样将应用所有更改并重新启动负责打印的打印调度程序。此时打印机将打印一张测试页，随后会弹出一个消息框，提示您检查测试页。

10. 单击“确定”以关闭消息框。

新的打印队列将出现在打印机配置窗口中，您可以向此队列提交打印任务。

11. 选择“操作::退出”以关闭打印机配置工具。

或者，您可以单击窗口边框右上角的 X 按钮来关闭打印机配置窗口。

12. 系统会提示您保存打印机信息。单击“保存”以保存并退出打印机配置工具。

#### 在 Knoppix 和 MEPIS 中配置打印机

在 Knoppix 和 MEPIS 中配置打印机的大多数步骤彼此相似，因此我将在本节中同时介绍两者。要在 Knoppix 或 MEPIS 中添加打印机，请遵循以下步骤：

1.  在 Knoppix 桌面上，选择“主菜单::KNOPPIX::配置::配置打印机(s)”。在 MEPIS 桌面上，选择“主菜单::打印系统::打印管理器”。

    系统将启动一个打印机配置工具。图 3-5 显示了 MEPIS 中的主窗口。在 Knoppix 中，主窗口看起来也很相似。

2.  单击工具栏上的“添加”，并从下拉菜单中选择“添加打印机/类别”。

    打印机配置工具将启动“添加打印机向导”（见图 3-6），引导您完成各个步骤。

![](img/11709a8f88c8cd03868a929dc94c0e2b_120_0.png)

图 3-5：在 Knoppix 和 MEPIS 中，通过此图形用户界面工具配置和管理打印机。

![](img/11709a8f88c8cd03868a929dc94c0e2b_120_1.png)

图 3-6：通过“添加打印机向导”添加新打印机。

3.  单击“下一步”，然后在下一个屏幕中选择打印机连接类型。然后单击“下一步”。

    连接类型可以是本地并口、串口或 USB 端口，也可以是支持不同协议（如 TCP 或 IPP）的网络打印机。

    根据打印机的连接类型，向导会提示您提供更多详细信息。例如，对于本地打印机，您需要从列表中选择并口、串口或 USB 端口。

4.  提供打印机连接信息——即本地端口或标识网络打印机的 URL。然后单击“下一步”。

    向导将显示打印机制造商和型号的列表，如图 3-7 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_121_0.png)

图 3-7：选择打印机的制造商和型号。

5.  选择您的打印机制造商和型号，然后单击“下一步”。

    向导将显示驱动程序列表及其推荐选项。

6.  选择打印机驱动程序，然后单击“下一步”。

    向导将显示一个屏幕（见图 3-8），您可以在此测试打印机设置。

7.  选择是否要在每个打印任务后添加横幅，然后单击“下一步”。

8.  设置任何配额，例如页数限制或发送至打印机的文件大小限制，然后单击“下一步”。

9.  指定用户访问设置，例如哪些用户可以访问打印队列，然后单击“下一步”。

10. 为打印队列命名并添加打印机描述。单击“下一步”。

11. 复核打印机设置，然后单击“完成”以添加打印机。

![](img/11709a8f88c8cd03868a929dc94c0e2b_122_0.png)

图 3-8：在安装打印机之前测试打印机设置。

#### 在 SUSE 中配置打印机

要在 SUSE 中添加打印机，请遵循以下步骤：

1.  选择 **主菜单** > *系统* > *控制中心 (YaST)*，在提示时输入 root 密码，然后单击窗口左侧的 **硬件**。

    YaST 控制中心将显示各种硬件的相关信息，如图 3-9 所示。如您所见，您可以通过 YaST 配置各种硬件。

![](img/11709a8f88c8cd03868a929dc94c0e2b_122_1.png)

图 3-9：若要配置任何项，请从 YaST 控制中心开始。

2.  单击窗口右侧的“打印机”。

    YaST 将打开打印机配置窗口，并显示其检测到的任何打印机的信息，如图 3-10 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_123_0.png)

3.  如果检测到您的打印机，请继续第 4 步。如果未检测到您的打印机，请单击“添加”。

    YaST 将显示打印机类型列表（见图 3-11），您可以从中选择您的打印机。类型取决于您的打印机如何连接到您的 PC（通过并口、串口、USB 或网络）。

4.  选择您的打印机类型，然后单击“下一步”。

    YaST 将根据您选择的打印机类型提示您提供更多详细信息。例如，对于并口打印机，您需要识别打印机所连接的并口。

5.  提供打印机连接信息，然后单击“下一步”。

    YaST 将提示您输入打印队列的名称及其他相关信息。

6.  输入打印队列的名称以及关于打印机的一些描述信息，然后单击“下一步”。

    YaST 将显示打印机制造商和型号的列表。

7.  选择您的打印机制造商和型号。然后单击“下一步”。

    YaST 将显示当前配置信息，以便您测试或编辑配置。

![](img/11709a8f88c8cd03868a929dc94c0e2b_124_0.png)

图 3-11：从此窗口中选择您的打印机类型。

8.  复核配置信息，然后单击“确定”。

    “添加打印机向导”将关闭并返回到 YaST 打印机配置窗口。

9.  单击“确定”以保存设置。

#### 在 Ubuntu 中配置打印机

要在 Ubuntu 中添加打印机，请遵循以下步骤：

1.  选择“系统→系统管理→打印”。

    将显示“打印机”窗口，如图 3-12 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_124_1.png)

图 3-12：在 Ubuntu 中，通过此窗口管理打印机。

2.  单击 **新建打印机**（参见 **图 3-12**）。

    这将启动 **添加打印机** 助手（参见 **图 3-13**），引导您完成打印机安装步骤。

![](img/11709a8f88c8cd03868a929dc94c0e2b_125_0.png)

图 3-13：在此步骤中识别打印机连接。

3.  选择打印机连接（参见 **图 3-13**），然后单击 **继续**。

    您可以选择打印机类型——本地或网络——或者选择已检测到的打印机或打印机端口（USB 或并口）。

4.  选择 **打印机制造商**，并从列表中选择 **型号**（参见 **图 3-14**）。

    对于所选的打印机型号，将显示推荐的驱动程序。

5.  单击 **应用**。

    这将安装打印机并关闭 **添加打印机** 助手。该打印机的图标将显示在 **图 3-12** 所示的打印机窗口中。

#### 在 Xandros 中配置打印机

当您首次运行 Xandros 时，**首次运行向导** 为您提供配置打印机的机会。**图 3-15** 显示了 **首次运行向导** 显示打印机信息以及提供添加新打印机机会的屏幕。

![](img/11709a8f88c8cd03868a929dc94c0e2b_126_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_126_1.png)

如果您在首次重启时跳过了此步骤，始终可以通过选择“主菜单→应用程序→系统→首次运行向导”来启动首次运行向导。

从首次运行向导的打印机屏幕，请遵循以下步骤配置打印机：

1. **单击首次运行向导打印机屏幕中的“添加”按钮**（参见图 3-15）。

    将启动“添加打印机向导”，如图 3-16 所示。





## 102 设置打印机

2.  **选择打印机类型——本地打印机或网络打印机——然后单击“下一步”。**

向导将提示你提供有关打印机连接的更多信息。

3.  **提供打印机连接的信息，然后单击“下一步”。**

例如，对于本地打印机，请指定它是并行端口打印机还是 USB 打印机。向导将显示一个屏幕，你可以在其中选择打印机的制造商、型号和驱动程序。

4.  **选择打印机的制造商、型号和驱动程序，如图 3-17 所示。单击“下一步”。**

![](img/11709a8f88c8cd03868a929dc94c0e2b_127_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_127_1.png)

向导提供打印测试页并完成打印机配置的选项。

5.  单击“完成”以完成打印机配置。

完成打印机配置后，首次运行向导将继续执行其他配置任务。

### 管理 DVD 和 CD-ROM

图形用户界面（GUI）桌面使得在 Linux 中使用 DVD 和 CD-ROM 变得简单。只需将 DVD 或 CD-ROM 放入驱动器，桌面上就会出现一个图标。

然后，你可以通过双击桌面上的图标来访问 CD 或 DVD。

要访问文件和文件夹，只需双击 GUI 文件管理器窗口中显示的图标即可。在某些 Linux 发行版中，当你将 CD 或 DVD 插入驱动器后，GUI 会立即在文件管理器窗口中自动打开 CD 或 DVD 的内容。

如果你看到 DVD/CD-ROM 图标，请右键单击该图标以呼出上下文菜单。通过该菜单，你可以在使用完时弹出 CD 或 DVD。

![](img/11709a8f88c8cd03868a929dc94c0e2b_128_0.png)

Knoppix 和 MEPIS 桌面为每个检测到的驱动器显示图标。要打开 CD 或 DVD，只需单击该驱动器的图标即可。在 SUSE 中，单击“我的计算机”图标，然后单击 DVD/CD 驱动器的图标。Ubuntu 在 Nautilus 窗口中打开 CD/DVD，并在桌面上放置一个图标。Xandros Desktop 在 Xandros 文件管理器窗口中打开 CD/DVD。

### 安装其他软件

安装软件的具体步骤取决于软件分发包的类型。大多数 Linux 软件以 RPM 文件或 Debian 包文件的形式提供。RPM 文件具有 .rpm 扩展名，而 Debian 包具有 .deb 扩展名。

大多数发行版提供 GUI 安装程序以简化安装新软件包的过程。在本节中，我将简要概述在 Debian、Fedora Core、SUSE 和 Xandros 中添加软件的方法。通常，你不会在 Knoppix（或其他任何 Live CD 发行版）中添加软件，因为 Live CD 发行版运行在 CD-ROM 上。

![](img/11709a8f88c8cd03868a929dc94c0e2b_129_0.png)

Fedora Core 和 SUSE 使用 RPM 包。Debian、MEPIS、Ubuntu 和 Xandros 都是基于 Debian 的发行版，并且正如预期的那样，它们通常使用 Debian 包（也称为 DEB）。然而，RPM 和 DEB 包都可以安装在任何 Linux 发行版中。

#### 在 Debian、MEPIS 和 Ubuntu 中安装软件

在 Debian 和基于 Debian 的发行版（如 MEPIS 和 Ubuntu）中管理软件包的最佳方法是使用 APT（Advanced Packaging Tool，高级打包工具），你通常通过 `apt-get` 命令来操作它。

当你安装 Debian 时，最后一步之一是配置 APT 的源。*APT 源* 是 APT 用于查找要下载和安装到系统中的软件包的互联网服务器（包括 FTP 和 Web）。假设 APT 已正确配置且你的系统具有高速互联网连接，你可以通过在终端窗口中输入以下命令开始安装任何软件包：

```
apt-get install pkgname
```

其中 *pkgname* 是你想要安装的软件包的名称。如果你不知道软件包名称，请开始在终端窗口中输入以下命令：

```
apt-cache search keyword
```

其中 *keyword* 与你想要安装的软件包相关。例如，要搜索描述中包含 *screenshot* 一词且包含 *KDE* 一词的软件包，我会输入以下内容。（我使用 *grep* 搜索输出中 *KDE* 文本的出现位置。）

```
apt-cache search screenshot | grep KDE
```

该命令随后打印以下行作为结果：

```
ksnapshot - Screenshot application for KDE
```

这表明 *ksnapshot* 软件包就是我需要的。如果该软件包尚未安装，我可以通过输入以下命令来安装它：

```
apt-get install ksnapshot
```

简而言之，这就是如何使用命令行工具在 Debian 中查找和安装软件包的方法。

### 安装其他软件

![](img/11709a8f88c8cd03868a929dc94c0e2b_130_0.png)

Debian、MEPIS 和 Ubuntu 还附带一个名为 Synaptic Package Manager 的 APT GUI 包安装程序，它非常直观易用。要试用它，请在 Debian 的 GNOME 桌面中选择“应用程序”->“系统工具”->“Synaptic Package Manager”。在 MEPIS 中，选择“主菜单”->“系统”->“Synaptic Package Manager”。在 Ubuntu 中，选择“系统”->“管理”->“Synaptic Package Manager”。（在 Ubuntu 中，当提示输入密码时，请输入你的普通用户密码，因为 Ubuntu 中没有 root 用户。）

Synaptic Package Manager 启动后，它会显示一个“快速入门”对话框，简要告诉你如何标记用于安装、升级或移除的软件包，以及如何进入菜单执行这些操作。阅读完介绍后，单击“关闭”以消除该对话框。

如果你的软件包信息已超过 48 小时，另一个对话框将提示你更新软件包信息。在该对话框中单击“重新加载”。Synaptic Package Manager 将下载最新的软件包信息，关闭对话框，并在主窗口中显示关于软件包的信息，如图 3-18 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_130_1.png)

> **图 3-18：** 你可以使用 Synaptic Package Manager 安装和移除软件包。

通过单击 Synaptic Package Manager 窗口左侧的类别，你可以在窗口右侧查看各种类别的软件包列表。每个软件包左侧的一个框指示该软件包是否已安装。如果你单击软件包名称，Synaptic Package Manager 将在窗口右下角显示所选软件包的信息。

要选择用于安装或移除的软件包，请单击其名称左侧的框，并从出现的弹出菜单中选择“标记为安装”或“标记为移除”。如果安装某软件包需要其他软件包，Synaptic Package Manager 将显示一个包含该信息的对话框，你可以单击“标记”以同时安装所需的软件包。标记尽可能多的软件包，然后单击工具栏上的“应用”以执行所有标记的操作。

#### 在 Fedora Core 中安装软件

大多数 Fedora Core 软件以 RPM 文件的形式提供。*RPM 文件基本上是一个包含安装软件产品所需的所有内容——所有文件和配置信息——的单个软件包。*

从 GNOME 桌面使用“添加或移除软件包”实用工具——这是一个用于安装和卸载 RPM 的图形实用工具。请遵循以下步骤：

1.  **选择“系统”** *应用程序* **“添加/移除软件”。**
    - 如果你没有以 *root* 身份登录，对话框将提示你输入 *root* 密码。添加或移除软件包实用工具启动并收集有关系统上已安装软件包状态的信息。在对所有已安装软件包的信息进行排序后，该实用工具显示“软件包管理”对话框，其中包含所有软件包的列表。（见图 3-19。）

![](img/11709a8f88c8cd03868a929dc94c0e2b_131_0.png)

2.  要安装未安装的软件包组，请选中该软件包组名称左侧的复选框。对于部分未安装的软件包组，请单击软件包名称右侧列中出现的“详细信息”超链接。
    - 将出现一个包含该软件包组中软件包详细信息的对话框。
3.  在对话框中，通过单击名称来选择你想要安装或移除的软件包，然后单击“关闭”以退出对话框。
    - 你将返回到“软件包管理”对话框，如果你添加或移除了任何软件包，“更新”按钮将变为可用。
4.  单击“更新”按钮，根据你在软件包列表中添加或移除的内容来更新软件包。

#### 在 SUSE 中安装软件

在 SUSE 中，请遵循以下步骤来安装或移除软件：

1.  选择 **“主菜单”**：YaST** 以启动如图 3-20 所示的 YaST 控制中心。
    - YaST 控制中心在左侧显示任务类别，在右侧显示该类别下的具体任务。
2.  单击左侧的“软件”类别，以便右侧显示软件选项。
3.  单击右侧的“软件管理”图标（参见图 3-20）。
    - YaST 显示一个新窗口，你可以在其中搜索软件包。

![](img/11709a8f88c8cd03868a929dc94c0e2b_132_0.png)





4. 通过名称搜索软件包，或通过浏览可用软件包来选择软件包。

要通过名称搜索软件包，请在窗口左上角的搜索栏中输入关键词，然后单击“搜索”。YaST 将在窗口右侧显示匹配的软件包，如**图 3-21** 所示。要浏览软件包，请单击左上角的“过滤器”，从下拉列表中选择“软件包组”，然后单击某个组以查看该组中单个软件包的列表。

5. 单击右下角的“接受”按钮，开始安装所选的软件包。

在安装包之前，YaST 会检查*依赖关系*——即如果某个包需要其他包才能正确安装。如果你想查看单击“接受”时会发生哪些更改，请单击“过滤器”并选择“安装摘要”。

#### 在 Xandros 中安装软件

Xandros 桌面操作系统附带了 Xandros 网络功能，它允许你在线购买软件，也可以从 CD 或 DVD 安装软件。要启动 Xandros 网络，请双击 Xandros 桌面上的 Xandros 网络图标。Xandros 网络启动后，会连接到 Xandros 服务器，并显示关于已安装、已更新和新应用程序的信息，如**图 3-22** 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_133_0.png)

**图 3-21：** 在此 YaST 窗口中查找并安装软件。

### 安装其他软件

![](img/11709a8f88c8cd03868a929dc94c0e2b_134_0.png)

**图 3-22：** 使用 Xandros 网络安装或升级软件。

要查看新应用程序列表，请单击 Xandros 网络窗口左侧“新应用程序”标签左边的加号（参见**图 3-23**）。你会看到另一个应用程序类别列表。如果单击某个类别，窗口右侧将显示该类别内软件包的名称。然后你可以选择一个软件包或整个类别进行安装。

要安装任何选中的软件包，请选择“文件：进入管理员模式”。系统会提示你输入管理员（root）密码。输入 root 密码后，你可以选择“文件：安装选定的应用程序”。Xandros 网络会检查依赖关系，如需更多信息会提示你，然后下载并安装新软件。

![](img/11709a8f88c8cd03868a929dc94c0e2b_134_1.png)

如果你下载了一个 Debian 软件包，可以通过从 Xandros 网络菜单中选择“文件：安装 DEB 文件”来安装它。类似地，菜单选项“文件：安装 RPM 文件”用于安装 RPM 软件包。（有关安装 RPM 软件包的更多信息，请参见第五卷，第 4 章。）

![](img/11709a8f88c8cd03868a929dc94c0e2b_135_0.png)

**图 3-23：** 选择要安装的软件包。

## 第 4 章：试用 Linux

###### 本章内容

- 启动 Linux
- 登录
- 体验图形化桌面
- 玩转 Shell
- 关机

![](img/11709a8f88c8cd03868a929dc94c0e2b_136_0.png)

你正坐在你的 PC 前，准备开机。你知道这台 PC 已安装了 Linux。（也许是你自己安装的，但谁知道呢？）你正纳闷开机后会看到什么，以及之后该做什么。不用担心。如果你是第一次使用 Linux，本章将向你展示如何登录、体验图形化桌面、尝试一些晦涩的 Linux 命令，最后是如何关机。

如果你尝试的是 Knoppix 启动光盘，你只需从 Knoppix 启动光盘启动即可（如第一卷第 2 章所述），然后就可以像使用其他 Linux 发行版一样体验它。

对于已经了解一些 Linux 知识的读者，请翻阅本章，看看是否有看似新的内容。你永远不知道自己还不知道什么！

### 启动 Linux

当你打开 PC 电源时，它会经过正常的启动序列并加载引导加载程序——根据你的 Linux 发行版和安装时的选择，可能是 GRUB 或 LILO。引导加载程序（曾被称为自举加载程序）是一个小型计算机程序，它从硬盘将操作系统的其余部分加载到计算机内存中。启动计算机的整个过程被称为引导（booting）。

![](img/11709a8f88c8cd03868a929dc94c0e2b_136_1.png)

对于从 CD 引导的启动光盘（如 Knoppix），引导加载程序通常是 ISOLINUX，它是专为在 ISO 9660 CD-ROM 上工作而设计的引导加载程序。

LILO 和 GRUB 引导加载程序会显示一个图形屏幕，列出引导加载程序可以加载的操作系统名称。例如，如果你的 PC 装有 Windows 和 Linux，你会看到这两个名称都列在那里。然后你可以使用上下箭头键选择要使用的操作系统。如果 PC 设置为默认加载 Linux，等待几秒钟，引导加载程序就会启动 Linux。更准确地说，引导加载程序将*Linux 内核*——Linux 操作系统的核心——加载到 PC 的内存中。

其他引导加载程序，如 ISOLINUX，可能会显示一个文本*boot:* 提示符，你可以在此输入引导命令来加载特定的操作系统并向该操作系统传递选项。

随着 Linux 内核启动，你会看到一长串启动消息，通常被称为*启动消息*。（你可以随时在终端窗口中输入命令 **dmesg** 来查看这些消息。）这些消息包括 Linux 检测到的设备名称。启动消息中的前几行之一内容为

```
Calibrating delay loop... 4997.12 BogoMIPS (lpj=2498560)
```

*BogoMIPS* 是 Linux 术语（本章在一个便捷的小节中进行了说明），用于衡量时间。BogoMIPS 前的数字取决于你 PC 的处理器速度，无论是旧的 200 MHz Pentium 还是新的 4 GHz Pentium 4。当内核需要等待一小段时间让某些事件发生（例如从磁盘控制器获得就绪响应）时，会使用 BogoMIPS 测量值。

#### 什么是 BogoMIPS 和 LPJ？

当 Linux 启动时，你会看到一条消息 `Calibrating delay loop... 4997.12 BogoMIPS (lpj=2498560)`，其中* BogoMIPS* 前有一个数字。BogoMIPS 是那些让新 Linux 用户困惑的术语之一，但它只是一个含义简单的行话。

BogoMIPS 是 Linus 的发明（是的，就是启动 Linux 的那位 Linus Torvalds），意思是虚假的*MIPS*。你可能知道，*MIPS* 是每秒百万条指令的缩写——衡量计算机运行程序速度的指标。不幸的是，MIPS 并不是一个很好的性能衡量标准；不同类型的计算机的 MIPS 测量值很难准确比较。BogoMIPS 基本上是一种独立于确切处理器类型的计算机速度测量方法。Linux 使用 BogoMIPS 数值来校准*延迟循环*，在延迟循环中，计算机持续运行一些无用的指令，直到指定的时间过去。当然，这样消耗宝贵的处理器时间的原因是为了等待某些缓慢的设备准备好工作。

哦……关于 LPJ——它是一个较新的术语，代表每 jiffy 循环数（loops per jiffy），是内核使用的另一种时间延迟衡量标准。Linux 内核以 jiffies 为单位考虑时间，而一个 *jiffy* 被定义为等于 1 秒除以名为 HZ 的内核变量的值的时间段。换句话说，每秒有 HZ 个 jiffies。

在显示启动消息后，某些 Linux 发行版（如 Fedora Core）会切换到图形化启动屏幕，显示系统启动进度的信息。当你第一次安装后启动某些 Linux 发行版（如 Fedora Core 和 Xandros 桌面操作系统）时，你会看到一个首次配置程序，引导你完成一些配置步骤，例如设置日期和时间以及添加用户账户。要完成这些首次配置步骤，你只需输入所需信息即可。

Linux 启动后，你通常会得到一个图形化登录屏幕。对于某些启动光盘发行版（如 Knoppix），你无需作为用户登录即可得到桌面。而在其他启动光盘（如 MEPIS）上，你必须登录。在 MEPIS 中，你可以作为两个预定义用户之一登录——使用密码 demo 的 demo 用户，或使用密码 root 的 root 用户。

![](img/11709a8f88c8cd03868a929dc94c0e2b_138_0.png)

**图 4-1** 显示了从 Knoppix 启动光盘启动 PC 后的 Knoppix 桌面。

对于 SUSE 等发行版，你可能会自动登录。而对于 MEPIS 等其他发行版，典型的图形化登录屏幕看起来类似于**图 4-2** 所示的样子。

![](img/11709a8f88c8cd03868a929dc94c0e2b_138_1.png)

**图 4-1：** 从 Knoppix 启动光盘引导后，你将看到 Knoppix 桌面。





### 启动 Linux

![](img/11709a8f88c8cd03868a929dc94c0e2b_139_0.png)

屏幕中间的登录窗口显示一个对话框，其中包含文本字段，您可以在此输入用户名和密码。

您可以使用在安装过程中或安装后定义的任何账户登录。始终存在 *root* 用户名，它恰好是超级用户（管理员账户）。无论是您自己安装 Linux 还是由他人为您安装，您都需要知道 *root* 密码。没有它，您将无法执行许多了解 Linux 工作原理所必需的任务。

在 Ubuntu 中，您只定义一个普通用户账户；Ubuntu 不给您定义 *root* 用户账户的机会。每当您需要执行任何需要您以 *root* 身份运行的任务时，您都必须使用 *sudo* 命令。

要以用户 **spiderman** 身份登录，请在第一个文本字段中输入 **spiderman**，然后按 Enter 键。（在开始输入之前，请将光标移动到登录对话框中。）然后输入 *spiderman* 的密码并按 Enter 键。然后您会看到初始图形用户界面（GUI — 简称为 GOO-ee）。您看到的内容取决于您对 GUI 的选择 — GNOME 或 KDE。如果别人替您做了选择，请不要担心 — GNOME 和 KDE 都非常优秀且功能强大。

大多数 Linux 发行版都附带两种 GUI 桌面环境中的一种或两种 — GNOME 和 KDE。如果您安装了两者，您可以逐一尝试。每个发行版都有其默认的 GUI。表 4-1 列出了某些 Linux 发行版的默认 GUI 桌面。我在以下部分中概述了两大主要 GUI 桌面环境 — GNOME 和 KDE。

**表 4-1 某些 Linux 发行版的默认 GUI 桌面**

| 发行版 | 默认 GUI 桌面 |
| :----------- | :------------------ |
| Debian       | 通常，Debian 默认安装 GNOME。但用户可以安装任何 GUI 桌面：GNOME、KDE 或 XFCE。（XFCE 是另一个用于 UNIX 系统的 GUI 桌面环境。您可以在 www.xfce.org 上找到有关 XFCE 的更多信息。） |
| Fedora Core  | GNOME，但用户也可以安装 KDE，并轻松在两者之间切换。 |
| Knoppix      | KDE |
| MEPIS        | KDE |
| SUSE         | 默认是 KDE，但用户可以选择在安装过程中安装 GNOME。 |
| Ubuntu       | 默认是 GNOME，但用户可以通过 Synaptic 包管理器安装 KDE。 |
| Xandros      | 经过增强的 KDE。（它被称为 Xandros 桌面。） |

### GNOME

GNOME 代表 GNU 网络对象模型环境（GNU，您可能知道，代表 GNU’s Not UNIX）。GNOME 是一个图形用户界面和一个编程环境。最新的 GNOME 版本是 2.x，也简称为 GNOME 2。从用户的角度来看，GNOME 类似于 Microsoft Windows。在幕后，GNOME 拥有许多功能，允许程序员编写可以良好协作的图形应用程序。在本章中，我只指出 GNOME GUI 的一些关键特性，而将细节留给您在闲暇时自行探索。

如果您感兴趣，您可以通过访问 www.gnome.org 上的 GNOME 主页随时查找有关 GNOME 的最新信息。

如果 GNOME 是默认桌面，登录之后，您会看到 GNOME GUI 桌面。图 4-3 展示了用户典型的初始 GNOME 桌面。

![](img/11709a8f88c8cd03868a929dc94c0e2b_141_0.png)

**图 4-3：登录后初始的 GNOME GUI 桌面。**

**警告！** 通常您不应该以 `root` 身份登录。当您以 `root` 身份登录时，因为您在 `root` 状态下可以执行任何操作，所以可能会意外损坏您的系统。请始终以普通用户身份登录。当您需要以 `root` 身份执行任何任务时，请在终端窗口中输入 `su -` 并输入 `root` 密码。

GNOME 桌面的具体外观取决于*当前会话*（当时运行的一组应用程序）以及您的 Linux 发行版。正如您所见，图 4-3 中显示的初始 GNOME 桌面与 Windows 桌面非常相似，除了它有两个任务栏，一个位于顶部，另一个位于屏幕底部边缘。这些是*GNOME 面板* — 类似于 Windows 任务栏。您可以从顶部 GNOME 面板访问各种菜单并启动应用程序，而状态信息（包括当前运行应用程序的图标）则显示在底部面板中。

您可以像在 Microsoft Windows 中一样移动和调整窗口大小。此外，就像在 Microsoft Windows 的窗口边框中一样，窗口标题栏的右侧角落包括三个按钮。最左边的按钮将窗口缩小为图标，中间的按钮最大化窗口以填充整个屏幕，最右边的按钮关闭窗口。

#### GNOME 面板

注意图 4-3 中沿 GNOME 桌面顶部和底部边缘显示的两个条。这些是 GNOME 面板，或者简称为面板。顶部面板用于启动程序，而底部面板用于状态信息（当前运行应用程序的图标和用于在桌面之间切换的按钮）。顶部面板还为小型面板小部件提供显示区域。每个*面板小部件*都是设计为在面板内运行的小型程序。例如，顶部面板最右侧的时钟小部件显示当前日期和时间。

GNOME 的顶部和底部面板除时钟小部件外还包含其他几个小部件。（具体细节取决于您的 Linux 发行版。）

- **启动器小部件：** 顶部面板上位于“应用程序”、“位置”和“系统”菜单按钮右侧的按钮是启动器小部件。这些每个小部件都显示带有应用程序*图标*的按钮。点击按钮将启动该应用程序。尝试点击这些按钮，看看会发生什么。鼠标和地球按钮启动 Mozilla Firefox Web 浏览器，而点击钢笔和纸张图标打开 OpenOffice.org Writer 文字处理程序。将鼠标悬停在按钮上时，会出现一个包含有关该按钮信息的小型帮助消息。

- **GNOME 分页器小部件：** 位于底部面板的右边缘，此小部件提供一个比系统屏幕物理尺寸更大的虚拟桌面。分页器在一个小的显示区域中显示四个页面。每个页面代表一个与显示屏幕尺寸相等的区域。要转到特定页面，请点击分页器窗口中的该页面。GNOME 分页器小部件显示当前虚拟页面中每个正在显示的窗口的按钮。

- **GNOME 天气小部件：** 显示当地天气。在您启动它之前，您不会看到这个小部件。您可以从在顶部面板空白区域右击时出现的上下文菜单中启动它。

#### GNOME 菜单按钮

在图 4-4 中，顶部面板的左侧以三个菜单按钮开始 — 应用程序、位置和桌面。（在其他发行版的 GNOME 桌面上，这三个菜单按钮可能有不同的名称。）应用程序按钮，我有时称之为主菜单按钮，类似于 Microsoft Windows 中的“开始”按钮。您可以从点击应用程序按钮左键时弹出的菜单中启动应用程序。通常，此菜单列出了启动应用程序的项目。大多数菜单项都有一个*箭头*；当您将鼠标指针放在带有箭头的项上时，会出现另一个弹出菜单。图 4-4 展示了 Fedora Core 系统上典型的 GNOME 应用程序菜单视图。

![](img/11709a8f88c8cd03868a929dc94c0e2b_143_0.png)

在图 4-4 中，菜单选择是 应用程序 > 互联网 > Firefox Web 浏览器。请注意，当您指向某个菜单选择时，会出现一个包含有关该选择信息的气泡帮助。

其他两个 GNOME 菜单 — 位置和桌面 — 使您可以执行以下类别的相关任务：

- **位置**菜单提供选项，用于打开您的主文件夹、查看桌面、浏览计算机、连接到各种服务器（如 FTP 和 Windows 共享）以及搜索文件。

- **系统**菜单用于编辑桌面首选项、配置系统设置、获取在线帮助、锁定屏幕以及注销。系统 > 管理允许您启动 GUI 系统配置实用程序，用于配置用户账户、root 密码、安全级别、显示、网络、打印机以及日期和时间等。要配置各种互联网服务器 — Web、FTP、DNS、Samba 等 — 请转到 系统 > 管理 > 服务器设置。

您可以从“添加到面板”对话框（见图 4-5）中启动小部件，例如天气小部件，当您右击顶部 GNOME 面板并从弹出的菜单中选择“添加到面板”时会出现该对话框。例如，您可以通过在“添加到面板”对话框中选择天气小部件来添加它，并且



点击“Add”后，在“Add to Panel”对话框中，你可以找到许多其他类别的小部件供尝试。

![](img/11709a8f88c8cd03868a929dc94c0e2b_144_0.png)

探索 GNOME 菜单中的所有项目，以了解你可以从此菜单执行的所有任务。特别是，将鼠标指针悬停在 System->Preferences 项上，以查看更改桌面外观的选项。例如，你可以从此菜单更改桌面背景，如图 4-6 所示。

#### 自定义 GNOME 桌面

到现在为止，你可能很想像像装点一番了。没人喜欢一成不变的 GNOME 桌面。毕竟，这是你的桌面。你可以按任何你喜欢的方式设置它。通过选择 System->Preferences，并从各种选项中进行选择，你可以配置 GNOME 桌面外观和大多数方面——即外观和行为。

要查看 Fedora Core 中桌面装饰的工作方式，请从选择 System->Preferences->Desktop Background 开始；会出现一个对话框，如图 4-7 所示。

从该对话框中，你可以选择纯色、颜色渐变或*墙纸*（用作背景的图片）作为背景。颜色渐变背景以某种颜色开始，并逐渐变为另一种颜色。渐变可以是垂直方向（从上到下）或水平方向（从左到右）。

Book I  
Chapter 4  
Trying Out Linux

![](img/11709a8f88c8cd03868a929dc94c0e2b_145_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_145_1.png)

要选择水平颜色渐变，请遵循以下步骤：

1. 从**Desktop Colors**下拉列表（参见图 4-7）中，选择**Horizontal Gradient**选项。
2. 点击下拉列表旁边的“Left Color”按钮。
   会弹出一个颜色选择对话框（如图 4-8 所示）。

   ![](img/11709a8f88c8cd03868a929dc94c0e2b_146_0.png)
3. 选择一种颜色并点击“OK”。
4. 重复相同的过程来选择右侧颜色。

完成这些步骤后，桌面将显示新的背景颜色。

如果你想使用图片作为墙纸，请点击 Desktop Background Preferences 对话框中间的“Add Wallpaper”按钮。将显示 Add Wallpapers 对话框，你可以从中选择用作墙纸的图片。通过点击 Add Wallpapers 对话框中的文件夹名称，你可以进入 `/usr/share/backgrounds/images` 目录。该目录包含 `default.png` 文件，即你在 GNOME 桌面上看到的默认墙纸。要更改墙纸，请选择你想要使用的图片。你可以选择任何联合图像专家组（JPEG）或可移植网络图形（PNG）格式的图片文件作为墙纸。选择图片后，点击“OK”。

新墙纸会立即出现在桌面上。完成更改后，点击“Close”按钮（参见图 4-7）以关闭对话框并应用更改。

#### 注销 GNOME

要在 Fedora Core 中从 GNOME 注销，请选择 System→Log Out。当对话框询问你是否真的想要注销时，点击“OK”。在其他发行版的 GNOME 桌面中，你通常会在顶部面板从左数第二个或第三个菜单按钮中找到注销选项。

### KDE

KDE 代表 K Desktop Environment。KDE 项目始于 1996 年 10 月，旨在为使用 X Window System 的 UNIX 系统开发通用的 GUI。KDE 的第一个测试版于一年后 1997 年 10 月发布。KDE 1.0 版于 1998 年 7 月发布；KDE 2.0 于 2000 年 10 月 23 日发布；KDE 3.0 于 2002 年 4 月 3 日发布；最新版本——KDE 3.4——于 2005 年 3 月 16 日发布。

从用户角度看，KDE 提供了一个图形桌面环境，包括窗口管理器、Konqueror Web 浏览器和文件管理器、启动应用程序的面板、帮助系统、配置工具以及许多应用程序，包括 OpenOffice.org 办公套件、图像查看器、PostScript 查看器以及邮件和新闻程序。

对于开发人员，KDE 拥有用于 C++ 轻松应用程序开发的类库和对象模型，KDE 是一个拥有许多合作者的大型开发项目。

你可以通过访问 www.kde.org 的 KDE 主页随时获取关于 KDE 的最新信息。

如果你的 Linux 系统的默认 GUI 是 KDE，你一登录就会看到 KDE GUI。通常，你会看到初始 KDE 桌面，类似于图 4-9 所示——在这种情况下，是 SUSE Linux 中的 KDE 桌面。

你会发现 KDE 非常容易使用，并且在许多方面与 Windows GUI 相似。你可以从一个类似于 Windows 中“开始”菜单的菜单启动应用程序。与 Windows 一样，你可以将文件夹和应用程序直接放置在 KDE 桌面上。

#### KDE 面板

KDE 面板出现在屏幕底部边缘，旨在用于启动应用程序。面板中最重要的组件是面板最左侧的主菜单按钮。该按钮就像 Windows 中的“开始”按钮。当你点击主菜单按钮时，会出现一个菜单。从这个菜单中，通过将鼠标指针悬停在显示向右箭头的项上，你可以访问其他菜单。例如，图 4-10 显示了配置各种服务的典型菜单选择。

你可以从此菜单启动应用程序。这就是为什么 KDE 文档将主菜单按钮称为*Application Starter*的原因。

在主菜单按钮旁边，面板包含许多其他按钮。如果你不知道某个按钮的作用，只需将鼠标指针悬停在按钮上；一个小弹出窗口会显示关于该按钮的简短消息。

![](img/11709a8f88c8cd03868a929dc94c0e2b_148_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_148_1.png)

#### 探索 GUI 桌面

#### 自定义 KDE 桌面

KDE 使自定义 KDE 桌面的外观和感觉变得简单。你需要用来装饰桌面的所有内容都在一个地方：KDE 控制中心。要启动 KDE 控制中心，请选择 Main Menu > Control Center。

当 KDE 控制中心启动时，它显示主窗口，左侧列有一项列表，右侧工作区显示有关系统的摘要信息，如图 4-11 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_149_0.png)

KDE 控制中心的左侧显示了你可以使用此程序自定义的项。列表组织成类别，如 Appearance & Themes（外观与主题）、Desktop（桌面）、Internet & Network（互联网与网络）、KDE Components（KDE 组件）、Peripherals（外围设备）、Security & Privacy（安全与隐私）、Sound & Multimedia（声音与多媒体）、System Administration（系统管理）等。点击一项以查看该项的子类别。点击其中一个子类别项以更改它。该项的配置选项随后出现在控制中心窗口的右侧。

要更改桌面背景，点击 Appearance & Themes，然后点击 Background。控制中心的右侧（参见图 4-12）显示了自定义桌面背景的选项。

如果你想更改特定桌面的背景，点击 Setting for Desktop 下拉列表。从桌面列表中，你可以选择想要更改哪个桌面背景。

![](img/11709a8f88c8cd03868a929dc94c0e2b_150_0.png)

对于彩色背景，选择 No Picture 单选按钮。从 Colors 下拉列表中，你可以选择单色背景或多种颜色渐变（意味着颜色逐渐从一种颜色变为另一种颜色）或用作背景的模式。然后，你可以点击 Colors 下拉列表下方出现的颜色按钮来选择颜色。完成选择后，点击 Apply 以试用背景。（如果你不喜欢所得结果，点击 Reset 以恢复到上一个背景。）

如果你想使用图片作为背景，选择 Picture 单选按钮，并点击该单选按钮旁边下拉菜单右侧的文件夹图标。会弹出一个对话框，显示 `/usr/share/wallpapers` 目录中的 JPEG 图像。你可以选择这些图像中的任何一个，或从另一个目录选择图片并点击 OK。然后点击 KDE 控制中心中的 Apply 按钮，将此墙纸应用于桌面。如果你不喜欢外观，点击 Reset。

#### 注销 KDE

当你完成对 KDE 的探索后，请注销。要注销 KDE，请选择 Main Menu::Logout。你也可以右键点击桌面的空白区域，然后从出现的上下文菜单中选择 Logout。

### 在 Shell 中玩耍

Linux 基本上是 UNIX，如果你不能在文本终端中输入晦涩难懂的命令，UNIX 就感觉不到像 UNIX。尽管 GNOME 和 KDE 有...



做了很多事情，将我们带入了一个拥有窗口、图标、鼠标和指针的世界——亲切地被称为 WIMP :-)——但有时你只能面对一个纯文本屏幕和一个类似这样的提示符（当你以 naba 身份登录时）：

```
naba@linux:~ /etc>
```

你最常见的文本屏幕出现在 X Window System 出现问题时，该系统本质上是运行你通常看到的窗口和菜单的机制。在这种情况下，你必须使用 shell（shell 环境），并且了解一些晦涩难懂的 Linux 命令。

你可以通过在 GNOME 或 KDE GUI 环境中尝试一些 Linux 命令来为与 shell 的意外遭遇做准备。当你掌握要领后，你甚至可以保持一个终端窗口打开，只是为了使用这些晦涩的命令之一——仅仅因为它比指点点击更快。这些两字母的命令确实很有威力！

#### 启动 bash shell

简单来说，*shell* 是 *Linux 命令解释器*——一个读取你输入的内容、将该文本解释为命令并执行相应操作的程序。

在你开始玩转 shell 之前，请打开一个终端窗口。在 GNOME 或 KDE 中，面板通常包含一个看起来像监视器的图标。当你点击该图标时，会出现一个带有提示符的窗口，如图 4-13 所示。那是一个终端窗口，其工作方式与传统终端完全一样。一个 shell 程序正在运行并准备好接受你输入的任何文本。你输入文本，按 Enter，就会发生某些事情（取决于你输入的内容）。

- **图 4-13：** 你可以在终端窗口的 shell 提示符处输入 Linux 命令。

![](img/11709a8f88c8cd03868a929dc94c0e2b_151_0.png)

#### 玩转 Shell

> **提示**
>
> 如果桌面 GNOME 或 KDE 面板中似乎没有启动终端或 shell 窗口的图标，请在主菜单层次结构中进行搜索，你应该能找到标记为 Console（控制台）或 Terminal（终端）的项。选择该项应该会打开一个终端窗口。

![](img/11709a8f88c8cd03868a929dc94c0e2b_152_0.png)

你看到的提示符取决于在该终端窗口中运行的 shell。默认的 Linux shell 称为 *bash*。

*bash* 可以理解大量的标准 Linux 命令，你可以使用这些命令来查看文件、从一个目录转到另一个目录、查看哪些程序正在运行（以及还有谁登录了系统），以及更多功能。

除了 Linux 命令外，*bash* 还可以运行存储在可执行文件中的任何程序。*bash* 还可以执行 *shell 脚本*——包含 Linux 命令的文本文件。

#### 理解 shell 命令

由于 shell 解释你输入的内容，了解 shell 如何解析你输入的文本非常重要。所有 shell 命令都具有以下通用格式：

```
command option1 option2 ... optionN
```

这样一行命令通常被称为 *命令行*。在命令行中，你输入一个命令，后面跟着一个或多个可选参数（或 *arguments*）。这些命令行选项（或命令行参数）有助于你指定你希望命令执行的操作。

一条基本规则是，你必须使用空格或 Tab 键将命令与选项分开。你还必须使用空格或 Tab 键将选项彼此分开。如果你想使用包含嵌入空格的选项，必须将该选项放在引号内。例如，要在 password 文件中搜索两个单词的文本，我输入以下 grep 命令。（*grep* 是那些用于在文件中搜索文本的晦涩命令之一。）

```
grep "WWW daemon" /etc/passwd
```

当 grep 打印出包含这些单词的行时，看起来像这样。（你在自己系统上看到的内容可能与我展示的不同。）

##### 尝试几个 Linux 命令

当终端窗口打开时，随意尝试几个 Linux 命令玩玩。我会通过一些随机示例指导你，让你对可以在 shell 提示符处做什么有个感觉。

要查看自上次启动以来 Linux PC 已运行了多长时间，请输入以下内容。（注意：我将输入的命令以粗体显示，后跟该命令的输出。）

```
uptime
12:06:34 up 59 days, 16:23, 4 users, load average: 0.56, 0.55, 0.37
```

“up 59 days, 16:23”这部分告诉你，这台特定的 PC 已经运行了将近两个月。嗯... Windows 能做到吗？

要查看你的系统正在运行的 Linux 内核版本，请像这样使用 `uname` 命令：

```
uname -srv
```

这会运行 `uname` 命令并带有三个选项：`-s`、`-r` 和 `-v`（如本例所示，可以组合为 `-srv`）。`-s` 选项使 `uname` 打印内核名称，`-r` 打印内核发行号，`-v` 打印内核版本号。该命令在我的一个 Linux 系统上生成以下输出：

```
Linux 2.6.14-1.1696_PCS #1 Sat Nov 19 19:02:13 EST 2005
```

在这种情况下，系统正在运行 Linux 内核版本 2.6.14。

要读取文件，请使用 `more` 命令。例如，输入 **more /etc/passwd** 来读取 /etc/passwd 文件。生成的输出类似于以下内容：

```
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/bin/bash
daemon:x:2:2:Daemon:/sbin:/bin/bash
lp:x:4:7:Printing daemon:/var/spool/lpd:/bin/bash
mail:x:8:12:Mailer daemon:/var/spool/clientmqueue:/bin/false
news:x:9:13:News system:/etc/news:/bin/bash
uucp:x:10:14:Unix-to-Unix CoPv system:/etc/uucp:/bin/bash
... lines deleted ...
```

要查看当前系统中所有正在运行的程序列表，请使用 `ps` 命令，如下所示：

```
ps ax
```

`ps` 命令接受许多选项，你可以提供这些选项而无需通常的短横线前缀。本例使用了 **a** 和 **x** 选项。**a** 选项列出你正在运行的所有进程，而 **x** 选项显示其余的进程。最终结果是 `ps ax` 打印出系统中所有正在运行的进程列表，如 `ps ax` 命令的以下示例输出所示：

```
PID TTY STAT TIME COMMAND
1 ? S 0:01 init [5]
2 ? SN 0:00 [ksoftirqd/0]
3 ? S< 0:00 [events/0]
4 ? S< 0:00 [khelper]
9 ? S< 0:00 [kthread]
22 ? S< 0:00 [kblockd/0]
58 ? S 0:00 [kapmld]
79 ? S 0:00 [pdflush]
80 ? S 0:00 [pdflush]
82 ? S< 0:00 [aio/0]
... lines deleted ...
5525 ? Ss 0:00 /opt/kde3/bin/kdm
5502 ? S 0:12 /usr/X11R6/bin/X -br -nolisten tcp :0 vt7 -auth /var/lib/xdm/authdir/authfiles/A:0-pIAOrt
5503 ? S 0:00 -:0
6187 ? Ss 0:00 /sbin/portmap
6358 ? Ss 0:00 /bin/sh /usr/X11R6/bin/kde
6566 ? Ss 0:00 /usr/sbin/cupsd
6577 ? Ssl 0:00 /usr/sbin/nscd
... lines deleted ...
```

即使只有你以用户身份登录，系统中可以运行的程序数量之多令人惊叹，不是吗？

你可以猜到，你可以从 shell 提示符处做任何事情，但这确实需要一些时间来适应。

### 关机

当你准备关闭 Linux 时，必须以有序的方式关闭。即使你是 Linux PC 的唯一用户，通常仍有几个其他程序在后台运行。此外，Linux 等操作系统会尝试优化它们向硬盘写入数据的方式。由于硬盘访问相对较慢（与访问内存位置所需的时间相比），数据通常存储在内存中，并以大块形式写入硬盘。因此，如果你只是简单地切断电源，你会有风险导致某些文件没有正确更新。

![](img/11709a8f88c8cd03868a929dc94c0e2b_154_0.png)

任何用户（你甚至不需要登录）都可以从桌面或图形登录屏幕关闭系统，尽管某些发行版（如 Debian）会提示你输入 *root* 密码。选择主菜单 → 注销（或在菜单中查找注销选项）。会出现一个注销对话框，提供重启或停止系统或简单注销的选项。要关闭系统，只需选择 Shutdown（关机）并点击 OK（确定）。然后系统将以有序的方式关闭。

如果注销菜单中没有关机选项，请先注销，然后从图形登录屏幕选择 Shutdown（关机）。

当系统关闭时，你会看到关于进程关闭的消息。你可能会惊讶于即使没有人明确运行任何程序，系统中仍然有多少进程。如果你的系统在关机时没有自动断电，你可以手动关闭电源。

![](img/11709a8f88c8cd03868a929dc94c0e2b_155_0.png)

请注意，关闭或重启系统可能*不*需要 *root* 访问权限。这就是为什么确保对控制台的物理访问得到充分保护非常重要，以便任何想这么做的人不能简单地走到控制台前关闭你的系统。




# 第二卷

## Linux 桌面环境

![](img/11709a8f88c8cd03868a929dc94c0e2b_156_0.png)

“确实，起初听起来很棒——一个‘主动’网络适配器，它通过帮人完成思路来协助撰写备忘录。”

#### 内容概览

- 第1章：介绍图形用户界面（GUI）桌面环境..........................................................133
- 第2章：掌控Shell................................................................161
- 第3章：浏览Linux文件系统...................................................181
- 第4章：介绍Linux应用程序.....................................................207
- 第5章：使用文本编辑器......................................................................239

### 第1章：介绍图形用户界面（GUI）桌面环境

###### 本章内容

- 发现GNOME和KDE图形界面的共同特征
- 介绍Debian的GNOME桌面环境
- 介绍Fedora Core的GNOME桌面环境
- 介绍Knoppix桌面环境
- 介绍MEPIS桌面环境
- 介绍SUSE桌面环境
- 介绍Ubuntu的GNOME桌面环境
- 介绍Xandros桌面环境

Linux发行版通常附带两种流行的图形用户界面（GUI）之一——GNOME和KDE。GNOME和KDE类似于微软Windows，但它们在一个方面很独特。与微软Windows不同，在Linux中你可以选择你的GUI。如果你不喜欢GNOME，只需注销并使用另一种GUI——KDE重新登录即可。试着在微软Windows上这么做看看！

![](img/11709a8f88c8cd03868a929dc94c0e2b_158_0.png)

GNOME和KDE是独立于Linux开发的。事实上，除了Linux之外，GNOME和KDE还可以在其他UNIX操作系统上运行。你也有选择在Linux中安装其他GUI，例如FVWM和Xfce。访问www.freedesktop.org/wiki/Desktops查看其他X桌面（运行在X窗口系统上的桌面）的列表。

本章将探讨GNOME和KDE的主要特性。要弄清这些GUI，最好的方法就是开始使用它们。

![](img/11709a8f88c8cd03868a929dc94c0e2b_158_1.png)

每个Linux发行版通常默认安装一种GUI。Debian、Fedora Core和Ubuntu的默认GUI是GNOME；而Knoppix、MEPIS、SUSE和Xandros的默认GUI是KDE。在Debian中，你可以安装GNOME或KDE中的任意一个。每个发行版还会定制GNOME或KDE，以创建该发行版独有的桌面。因此，我还会概述每个发行版的桌面——包括Debian、Fedora Core和Ubuntu的GNOME，以及Knoppix、MEPIS、SUSE和Xandros的KDE。你可以将其视为简要介绍。你需要自己去探索这些桌面，因为这是熟悉GUI的最佳方式。

#### 了解GUI的共同特征

从用户角度看，GNOME和KDE可能看起来相似，因为许多功能的工作方式类似。熟悉这些共同特征，这样无论你选择哪种GUI作为日常工作环境，都可以依赖它们。

最重要的是，无论你决定使用哪种GUI，所有GUI应用程序——无论基于GNOME还是KDE——都可以在所有GUI桌面上运行。换句话说，你可以在GNOME下运行KDE应用程序，反之亦然。唯一的障碍是，有时GNOME和KDE应用程序可能不会默认安装。

首先，GNOME和KDE的初始桌面看起来与其他流行GUI一样，如微软Windows或Mac OS X桌面。例如，图1-1和图1-2分别展示了典型的GNOME和KDE桌面。

![](img/11709a8f88c8cd03868a929dc94c0e2b_159_0.png)

**图1-1：** 典型的GNOME桌面。

![](img/11709a8f88c8cd03868a929dc94c0e2b_160_0.png)

**图1-2：** 典型的KDE桌面。

这两个桌面（图1-1和图1-2）最初都显示计算机、主文件夹和用于存放已删除文件的回收站图标。GNOME和KDE桌面的另一个主要特征是*面板*——KDE中位于底部的栏和GNOME中位于顶部和底部的栏。每个面板类似于Windows任务栏。左侧有按钮（各种程序的快捷方式），右侧有时钟显示。面板的中间部分显示你已启动的应用程序（或为你自动启动的应用程序）的按钮。

![](img/11709a8f88c8cd03868a929dc94c0e2b_160_1.png)

将鼠标悬停在面板上的任何图标上，一个小弹出窗口会显示该图标的名称。弹出窗口还会提示你可以对该图标执行的操作。

##### 桌面右键菜单

当你在GNOME或KDE桌面的空白区域右键单击时，都会显示右键菜单。该菜单的具体内容取决于桌面，但通常提供菜单选项，使你可以执行以下类型的任务：

- 运行命令。
- 打开终端窗口，在其中输入Linux命令。
- 创建新文件夹。
- 配置桌面背景。
- 重新排列桌面图标。

例如，图1-3和图1-4分别展示了典型GNOME和KDE桌面中的桌面右键菜单。带有向右箭头的桌面菜单选项表示当你将鼠标指针悬停在箭头上时会出现的其他菜单。

![](img/11709a8f88c8cd03868a929dc94c0e2b_161_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_161_1.png)

##### 图标右键菜单

在GNOME或KDE中右键单击任何桌面图标会显示另一个菜单。（参见图1-5和图1-6。）无论单击什么图标，此右键菜单中的许多项目都是相同的，但右键单击某些图标（例如回收站图标）会产生略有不同的菜单。你可以从图标右键菜单执行以下典型任务：

- 在文件管理器中打开文件夹。
- 用你选择的应用程序打开文件。
- 重命名图标。
- 将图标移动到回收站。
- 查看该图标的属性。

![](img/11709a8f88c8cd03868a929dc94c0e2b_162_0.png)

对于回收站图标，图标右键菜单通常提供永久删除回收站内项目的选项。（你有一次选择“是”或“否”的机会。）

![](img/11709a8f88c8cd03868a929dc94c0e2b_162_1.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_162_2.png)

我敢肯定你看到了这里的规律。就是右键单击。无论你在GUI桌面的哪个位置，在选择之前总是先右键单击。当你右键单击时，肯定能找到有用的东西！

##### 面板

面板是横跨桌面顶部或底部的长栏。在GNOME中，有两个面板。图1-7和图1-8分别展示了GNOME上面板和单个KDE面板的典型视图。

![](img/11709a8f88c8cd03868a929dc94c0e2b_163_0.png)

面板是图标的停放处。某些图标在你点击时会启动程序。某些图标显示状态（例如当前正在运行的程序）以及日期和时间等信息。

![](img/11709a8f88c8cd03868a929dc94c0e2b_163_1.png)

从左端开始，第一个图标（无论它显示什么）是主菜单按钮——它类似于微软Windows中的“开始”按钮。然后是几个启动各种程序的图标。

![](img/11709a8f88c8cd03868a929dc94c0e2b_163_2.png)

顺便提一下，如果你将鼠标指针悬停在图标上，会弹出一个帮助气泡，提供有关该图标的有用提示。

在KDE面板最左侧的一组图标右边，工作区切换器图标显示四个矩形区域，每个区域代表一个虚拟桌面。该图标被称为工作区切换器、桌面翻页器，或简称翻页器。你可以点击这些矩形之一来切换到不同的虚拟桌面。此功能就像拥有四个独立的虚拟桌面可供使用。老实说，我最终只使用一个桌面，但我喜欢知道如果我需要时其他桌面在那里。另一方面，如果你正在编写代码并为新程序编写用户指南，你可以使用一个桌面进行所有编码工作，并使用第二个桌面编写用户指南。当然，你可以通过单次鼠标点击在两个桌面之间切换。

桌面翻页器图标右边的区域显示你迄今已启动的程序按钮。如果你尚未启动任何程序，此区域为空。




其他图标可能位于翻页器旁边，但日期和时间始终显示在面板的最右端。

![](img/11709a8f88c8cd03868a929dc94c0e2b_164_0.png)

现在来介绍这些面板图标的一些技术细节。面板本身是一个独立的应用程序；每个图标都是一个按钮或一个称为小程序（applet）的程序。小程序是小型应用程序（也称为插件）。这些面板小程序可以执行各种操作，例如启动其他程序或显示日期和时间。在运行小程序之前，你必须将其添加到面板中。右键单击面板的空白区域，并选择适当的菜单项以将小程序添加到面板。添加小程序后，你可以右键单击该小程序的图标来配置它或执行该小程序支持的某些任务。

如果你右键单击任何图标——或者在面板上的任何位置右键单击——都会弹出一个上下文菜单，允许你执行与该图标相关的操作（例如移动或完全移除它）。你还可以设置一些偏好，并向面板添加更多按钮和小程序。

###### 主菜单

GNOME 顶部面板和 KDE 唯一的 面板中最左侧的图标是主菜单按钮。你通常可以在这里找到所有应用程序，它们被组织成子菜单。在本节中，我提供了主菜单的一些示例，并指出了一些有趣的项目。然后你可以自行进行进一步探索。

在 GNOME 桌面上，顶部面板最左侧的菜单按钮通常标记为“应用程序”，并且顶部面板有一个或多个额外的菜单按钮，例如 Fedora Core GNOME 桌面上的“位置”和“桌面”。

单击主菜单按钮以调出第一级菜单。然后将鼠标悬停在任何带有箭头的菜单项上，以调出下一级菜单，依此类推。你可以遍历菜单层次结构，并从最终菜单中做出选择。图 1-9 和图 1-10 分别显示了典型 GNOME 和 KDE 桌面中的主菜单层次结构。

![](img/11709a8f88c8cd03868a929dc94c0e2b_164_1.png)

关于我如何指称菜单选择，我使用如下表示法：使用 Main Menu::System::Desktop Applet::OpenOffice.Org QuickerStart 来指代图 1-10 中显示的菜单选择。类似地，我说选择 Applications::Internet::Firefox Web Browser 来指代图 1-9 中高亮的菜单序列。你应该明白其中的逻辑。

### 140 了解图形用户界面（GUI）的通用功能

![](img/11709a8f88c8cd03868a929dc94c0e2b_165_0.png)

图 1-9：典型 GNOME 桌面中的主菜单层次结构。

![](img/11709a8f88c8cd03868a929dc94c0e2b_165_1.png)

图 1-10：典型 KDE 桌面中的主菜单层次结构。

在大多数桌面环境中，顶级主菜单包含以下类型的菜单类别：

- **附件**或**实用工具**：大量的实用程序，如科学计算器、字符选择器、软驱格式化程序、词典、Palm Pilot 或 Handspring 同步等。
- **游戏**：一个菜单——还有什么？游戏（而且数量众多——如纸牌、麻将、扫雷、黑白棋等）
- **图形**：诸如 GIMP（一款类似 Adobe Photoshop 的程序）、数码相机接口、扫描仪接口、屏幕截图程序以及 Adobe Acrobat 查看器等程序
- **互联网**：互联网应用程序，如 Web 浏览器、邮件阅读器和即时通讯工具
- **办公**：办公应用程序，如 OpenOffice.org 办公套件（包括 Writer 文字处理器、Calc 电子表格、Impress 幻灯片演示程序、Draw 绘图程序等更多功能）
- **首选项**或**设置**：配置系统许多方面的选项，包括桌面外观和行为
- **多媒体**或**声音与视频**：多媒体应用程序，如 CD 播放器、混音器、录音机和音量控制
- **系统**：用于配置 Linux 系统的系统管理工具

主菜单通常还包含一些用于常见任务的菜单项，例如：

- **主菜单::帮助**：显示在线帮助。
- **主菜单::运行命令**：显示一个对话框，你可以在其中输入程序名称，然后单击“运行”以启动该程序。
- **主菜单::搜索文件（或查找文件）**：运行搜索工具，你可以从中搜索文件。
- **主菜单::锁定屏幕**：启动屏幕保护程序并锁定屏幕。当你想返回桌面时，系统会提示你输入密码。
- **主菜单::注销**：注销你。（你会有一次确认是否真的想要注销的机会。）

每个发行版的主菜单都有不同的类别，但菜单组织方式足够相似，你通常可以找到所需的内容。

好了。关于主菜单，我就说到这里。当你使用 GNOME 或 KDE 桌面时，你会大量使用主菜单。即使一开始似乎信息量过大，随着你在 Linux 上花更多时间，这一切都会变得非常熟悉。

![](img/11709a8f88c8cd03868a929dc94c0e2b_166_0.png)

在接下来的章节中，我将概述具体的桌面环境：Debian 的 GNOME 桌面、Fedora Core 的 GNOME 桌面、Knoppix 桌面、MEPIS 的 KDE 桌面、SUSE 桌面、Ubuntu 的 GNOME 桌面以及 Xandros 桌面。

### 介绍 Debian 的 GNOME 桌面

Debian 默认的 GNOME 桌面具有简单的外观（见图 1-11），桌面上只有三个图标——一个“计算机”图标、你的主文件夹和“回收站”图标。

在图 1-11 中，请注意 Debian GNOME 桌面中的以下主要项目，以及单击它们时会发生什么：

- **桌面图标：** “计算机”图标在 Nautilus 文件管理器中打开你的计算机以便浏览。“主文件夹”图标在 Nautilus 文件管理器中打开你的主文件夹（有关使用 Nautilus 浏览文件夹的更多信息，请参阅本书的小书第 3 章）。
- **回收站（或废纸篓）图标：** 代表一个存储已删除项目的地方，直到你清空回收站。
- **应用程序菜单（主菜单）：** 调出主菜单，你可以从中选择要运行的应用程序。
- **操作菜单：** 提供菜单选项以运行应用程序、搜索文件、截图、锁定屏幕和注销。
- **Nautilus 文件浏览器：** 以文件浏览模式在 Nautilus 文件管理器中打开你的主文件夹（有关使用 Nautilus 浏览文件系统的解释，请参阅本书的小书第 3 章）。
- **终端程序：** 打开一个终端窗口，你可以在其中输入 Linux 命令。
- **工作区切换器：** 每个方框调出不同的桌面。这与 KDE 桌面中的桌面翻页器类似。
- **显示桌面：** 通过最小化所有窗口来显示桌面。
- **音量：** 显示一个音量控制条，你可以拖动滑块来更改声音的音量。
- **窗口选择器：** 显示当前打开的窗口列表，你可以单击并将该窗口置于前台，使其成为当前活动窗口。
- **日期和时间：** 显示当前日期和时间，单击会调出一个显示当前日期的日历。

### 图 1-11：Debian 默认的 GNOME 桌面。

![](img/11709a8f88c8cd03868a929dc94c0e2b_168_0.png)

单击主菜单会调出如图 1-12 所示的主菜单，使你能够访问 Debian 中的大多数应用程序。当然，各种子菜单中应用程序的具体列表取决于你安装了什么，但图 1-12 展示了 Debian 中典型主菜单的视图。要浏览主菜单，鼠标悬停在带有右箭头的项上，并会弹出一个包含更多项目的子菜单。

操作菜单是你可以从面板调用的另一个菜单。通过操作菜单，你可以执行其他任务，如运行任何应用程序、搜索文件、截图和注销。

![](img/11709a8f88c8cd03868a929dc94c0e2b_169_0.png)

图 1-12：从 Debian GNOME 桌面的主菜单启动应用程序。

要探索 Debian 的 GNOME 桌面，尝试单击面板图标以启动应用程序。特别是，你可以单击顶部面板上的 Nautilus 文件浏览器图标，在 Nautilus 文件管理器中打开你的主文件夹。在该窗口打开后，你可以探索其他文件夹以熟悉文件系统。

你也可以单击主菜单，并将鼠标悬停在项目上以查看所有子菜单，了解你可以在 Debian 中运行的应用程序种类。当然，你可以单击某个项目以启动特定应用程序并逐一尝试。

### 介绍 Fedora Core 的 GNOME 桌面

GNOME 是 Fedora Core 的默认图形用户界面。这意味着当你首次在图形登录屏幕上登录时，你会得到 GNOME 桌面，如图 1-13 所示。桌面显示计算机、主文件夹和回收站的图标。

以下列表介绍了 GNOME 桌面的主要部分，并简要描述了每部分的目的：

- **桌面图标：** 双击“计算机”图标以查看计算机的内容，双击“主文件夹”图标在 Nautilus 文件管理器窗口中打开你的主文件夹。“回收站”图标容纳已删除的项目。桌面还显示其他可移动媒体（如 CD 和 DVD）的图标。




#### 应用程序菜单（主菜单）：
调出主菜单，您可以从中选择要运行的应用程序。

#### 位置菜单：
显示一个菜单，您可以从中打开主文件夹、查看桌面、浏览计算机、连接到 FTP 和 Windows 共享等服务器，以及搜索文件。

#### 系统菜单：
调出一个菜单，您可以从中编辑桌面首选项、编辑系统设置、获取在线帮助、锁定屏幕以及注销。`System::Administration::Server Settings` 显示一个菜单，允许您启动用于配置各种互联网服务器（包括 Web、FTP、DNS、Samba 等）的 GUI 系统配置实用程序。

#### Firefox 网络浏览器：
运行 Mozilla Firefox 网络浏览器。

#### Evolution：
启动 Evolution 电子邮件和日历软件。

#### OpenOffice.org 文字处理器：
运行 OpenOffice.org 文字处理器，这是一款类似 Microsoft Word 的文字处理软件。

#### OpenOffice.org 演示文稿：
运行 OpenOffice.org Impress 幻灯片演示程序（类似于 Microsoft PowerPoint）。

#### OpenOffice.org 电子表格：
运行 OpenOffice.org 电子表格程序，这是一款类似 Microsoft Excel 的电子表格程序。

#### 显示桌面：
通过最小化所有窗口来显示桌面。

#### 工作区切换器：
每个方块调出不同的工作区。其功能与 KDE 桌面中的桌面分页器相同。

#### 音量：
显示一个音量控制条，您可以通过拖动滑块来改变声音的音量。

#### 日期和时间：
显示当前日期和时间，点击会调出一个显示当前日期的日历。

点击主菜单（参见图 1-13）以打开主菜单并探索各个类别。从主菜单，您可以访问 Fedora Core 中几乎所有应用程序和实用工具。

### 介绍 Knoppix 桌面

Knoppix 不需要您使用用户名登录。在您通过 Knoppix CD 启动 PC 后，您将看到图 1-15 中显示的初始 Knoppix 桌面。Knoppix 使用 KDE 的定制版本作为其桌面，因此您可能会注意到它与其他基于 KDE 的桌面（如 MEPIS、SUSE 和 Xandros）的相似之处。特别是，MEPIS 桌面看起来与 Knoppix 桌面相似，因为 MEPIS 也包含许多相同的桌面图标和面板项目。

与其他一些发行版相比，Knoppix 有大量的桌面图标和面板项目。这主要是因为它会检测并为所有检测到的硬盘分区、CD/DVD-ROM 驱动器和软盘驱动器添加桌面图标。

在图 1-14 中，请注意 Knoppix 桌面的主要组成部分：

- **桌面图标：** Knoppix 显示所有硬盘分区、CD/DVD 驱动器和软盘驱动器的图标。点击以挂载和打开这些存储设备中的任何一个并访问其内容。此外，还有一个回收站图标和一个指向 Knoppix 手册的快捷方式（Knoppix 启动后会在 Konqueror 窗口中打开该手册）。
- **隐藏面板：** 面板的两个端点作为“隐藏面板”按钮。这意味着如果您点击其中一个，面板将滑动并消失，只留下“隐藏面板”按钮。再次点击，面板将重新出现。您可以隐藏面板以为其他窗口腾出更多空间。
- **主菜单（K 菜单）：** 从这个主菜单（见图 1-15），您可以选择要运行的应用程序、锁定屏幕、获取在线帮助或注销。
- **Knoppix 菜单：** 调出一个菜单，您可以使用它执行诸如配置设备（打印机、声卡）、设置网络、开启或关闭 SSH 和 Samba 等少数服务器，以及打开 root shell 窗口（您可以在此作为超级用户输入命令）等任务。
- **窗口列表：** 点击以查看当前打开的窗口列表，并在桌面上排列这些窗口。
- **显示桌面：** 通过最小化所有窗口来显示桌面。
- **主文件夹：** 在 Konqueror 文件管理器中打开您的主目录。
- **终端程序：** 运行 Konsole，这是一个提供终端窗口以便您输入 Linux 命令的程序。
- **Konqueror 网络浏览器：** 运行 Konqueror 网络浏览器。
- **Firefox 浏览器：** 运行 Firefox 网络浏览器。
- **OpenOffice：** 启动 OpenOffice.org 文字处理器，这是一款类似 Microsoft Word 的文字处理软件。您可以从主菜单启动其他 OpenOffice.org 程序，如 Impress、Calc 和 Draw。
- **桌面分页器：** 每个方块调出不同的桌面。
- **程序图标：** 此区域显示当前运行程序的图标。
- **键盘布局：** 点击以在多种键盘布局之间切换：美国、德国和法国。（图标上的国旗指示当前键盘正在使用哪个国家的布局。）
- **显示配置：** 点击以更改屏幕分辨率或配置显示。
- **音量：** 启动 KMix 实用程序，该程序允许您更改音量并控制声卡的其他方面。
- **日期和时间：** 显示当前日期和时间。点击以调出一个显示当前日期的日历。

![](img/11709a8f88c8cd03868a929dc94c0e2b_170_0.png)

**图 1-14：** Knoppix 桌面基于 KDE。

**已删除项**

**指向 Knoppix 手册的链接**

**存储设备**

**带有 Knoppix 手册的 Konqueror 网络浏览器**

![](img/11709a8f88c8cd03868a929dc94c0e2b_173_0.png)

**图 1-15：** 从 Knoppix 主菜单启动应用程序。

图 1-15 显示了 Knoppix 主菜单，它在您点击面板上的“主菜单”时出现。与所有桌面一样，主菜单是访问 Knoppix 中应用程序的第一步。对于单 CD 发行版，Knoppix 打包了大量应用程序，因此通过查看图 1-15 中主菜单显示的应用程序类别，您可能可以猜到这一点。

Knoppix 菜单（如图 1-16 所示）是您可以从面板打开的另一个重要菜单。此菜单允许您配置设备、设置网络连接、启动服务器、运行一些实用程序，并打开 `root shell`——一个终端窗口，您可以在其中作为 `root`（超级用户）输入 Linux 命令。

要探索 Knoppix 的其他部分，请从点击面板图标开始，以启动网络浏览器和 OpenOffice.org 文字处理器等应用程序。一个好的起点是主图标，它会在 Konqueror 窗口中打开您的主目录。从那个 Konqueror 窗口，您可以探索文件系统的其余部分。

![](img/11709a8f88c8cd03868a929dc94c0e2b_174_0.png)

**提示**

要挂载并访问 Knoppix 检测到的任何硬盘分区上的文件，只需点击桌面上的图标。Knoppix 随后会挂载该分区，并在 Konqueror 窗口中显示其内容。例如，在我的笔记本电脑上，我可以点击桌面上的硬盘分区 [hda2] 图标来访问该分区上的文件。该分区碰巧是一个包含 Windows XP 操作系统的 NTFS 分区。Knoppix 可以挂载并打开该分区，使我能够访问那些分区文件。

您也可以点击主菜单并探索 Knoppix 中海量的应用程序。

**技术内幕**

哦，Knoppix 如何在单个 CD（容量小于 700MB）上打包这么多应用程序的秘密：Knoppix 在 CD 上以压缩格式存储文件，然后根据需要实时解压它们。是不是很令人印象深刻？

### 介绍 MEPIS KDE 桌面

MEPIS 基于 Debian，并使用 KDE 作为其桌面。图 1-17 显示了初始的 MEPIS 桌面。注意，MEPIS 桌面包含所有存储设备的桌面图标，并包含大量用于访问许多应用程序和实用工具的面板图标。

如图 1-17 所示，MEPIS 桌面包含以下关键元素：

- **桌面图标**：MEPIS 显示所有硬盘分区、CD/DVD 驱动器和软盘驱动器的桌面图标。点击以打开并查看这些存储设备中任何一个的内容。桌面还显示一个用于已删除项的回收站图标和一个指向 MEPIS 网站图标链接。
- **主菜单**：调出 MEPIS 主菜单（见图 1-18），您可以从中执行各种任务，如启动应用程序、运行命令、获取帮助、查找文件、访问 MEPIS 操作系统中心、启动新会话或注销。




#### 已删除项
#### 存储设备
#### 链接到 MEPIS 网站

![](img/11709a8f88c8cd03868a929dc94c0e2b_176_0.png)

### 图 1-17：初始的 MEPIS 桌面。

- 主菜单
- 控制中心
- 信息中心
- KDE 系统守护程序
- 终端程序
- Synaptic 包管理器
- 文本编辑器
- 桌面分页器
- 系统性能监视器
- 天气
- CD 和 DVD 刻录
- 挂载 Windows 共享
- OpenOffice.org
- 剪贴板工具
- OpenOffice.org
- Kontact
- 快速启动
- Konqueror 网页浏览器
- 音量
- 日期和时间
- Firefox 网页浏览器
- 主文件夹
- 显示桌面
- MEPIS 系统中心
- 文件管理器
- 浏览 Windows 网络

### 介绍 GUI 桌面

- **信息中心**：运行 KDE 信息中心，您可以在这里查看系统硬件设备和内存的信息。
- **KDE 系统守护程序**：运行 KDE 系统守护程序实用工具，该工具使您能够管理进程并监控系统性能。
- **控制中心**：启动 KDE 控制中心，您可以从这里配置 KDE 桌面的各个方面。
- **终端程序**：打开一个带有 root 登录权限的终端窗口，您可以在其中输入 Linux 命令。
- **MEPIS 系统中心**：启动 MEPIS 系统中心，您可以从中访问 MEPIS 操作系统的安装和配置工具。您可以执行修复分区和更改系统主机名等任务。
- **Synaptic 包管理器**：运行 Synaptic 包管理器——这是 Debian APT（高级包工具）的图形用户界面前端，您可以使用它来安装或删除软件包。
- **文件管理器**：以 root 用户（超级用户）权限启动 Konqueror 文件管理器。
- **浏览 Windows 网络**：打开一个 Konqueror 文件管理器窗口，您可以从中浏览和访问 Windows 共享。
- **显示桌面**：单击可隐藏所有窗口并显示桌面。
- **主文件夹**：在 Konqueror 文件管理器中打开您的主目录。
- **Firefox 网页浏览器**：运行 Mozilla Firefox 网页浏览器。
- **Konqueror 网页浏览器**：运行 Konqueror 网页浏览器。
- **Kontact**：运行 Kontact 个人信息管理器。
- **文本编辑器**：运行 KWrite 文本编辑器。
- **CD/DVD 刻录**：运行 K3B CD/DVD 刻录应用程序。
- **OpenOffice.org 文字处理**：运行 OpenOffice.org 文字处理应用程序。
- **桌面分页器**：单击每个方格以显示不同的桌面。
- **系统性能监视器**：显示当前系统性能（内存和处理器使用率）。
- **音量**：单击以控制声音音量。
- **剪贴板工具**：单击以查看您剪切的内容以及您可以粘贴到其他地方的内容。
- **OpenOffice.org 快速启动**：右键单击以打开新的 OpenOffice.org 文档。
- **挂载 Windows 共享**：单击以打开 Smb4K，它允许浏览和挂载 Windows 共享。
- **天气**：显示所选位置的当前天气（右键单击并选择“配置 KWeather”以更改位置）。
- **日期和时间**：显示当前日期和时间。单击会调出时间和日期实用程序以设置日期和时间。

MEPIS 主菜单（参见图 1-18）具有典型的 KDE 主菜单结构，它将菜单项排列在三个广泛的类别中——“最常用的应用程序”显示您最近使用的应用程序图标，“所有应用程序”包含几个用于访问应用程序的子菜单，“操作”显示用于一些常见任务的菜单，例如访问打印系统、锁定屏幕、运行命令、启动新会话或注销。为了熟悉 MEPIS 作为桌面操作系统提供的功能，请浏览 MEPIS 主菜单“所有应用程序”类别中的菜单。

### 介绍 SUSE 桌面

SUSE Linux 是一种商业产品，它提供了一个定制的桌面。SUSE 会自动登录您在安装过程中定义的本地用户，并调出初始桌面，如图 1-19 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_179_0.png)

### 图 1-19：初始的 SUSE 桌面。

请跟随图 1-19，我将指出 SUSE 桌面上一些值得注意的元素：

- **桌面图标**：SUSE 显示常见的桌面图标——一个用于浏览计算机内容的“我的电脑”图标，一个“回收站”图标，一个用于浏览本地 Windows 网络的图标，以及 Firefox 网页浏览器、打印管理器和 OpenOffice.org 办公套件的图标。
- **主菜单**：调出主菜单（参见图 1-20），您可以从其中启动应用程序、锁定屏幕、获取帮助、切换用户或注销。
- **主文件夹**：在 Konqueror 文件管理器中打开您的主目录。
- **终端程序**：运行 *Konsole*，这是一个提供终端窗口的程序，您可以在其中输入 Linux 命令。
- **SUSE 帮助中心**：启动 SUSE 帮助中心，您可以在这里获取有关 SUSE Linux 各个方面的帮助。
- **Konqueror 网页浏览器**：运行 Konqueror 网页浏览器。
- **Kontact**：启动适用于 KDE 的 Kontact 个人信息管理器。通过 Kontact，您可以阅读邮件、管理联系人、维护日程安排、阅读 RSS 源以及更多。
- **桌面分页器**：单击每个方格以显示不同的桌面。
- **剪贴板工具**：单击以查看已剪切的内容以及您可以粘贴到其他地方的内容。
- **电源节省工具**：右键单击以查看一个菜单，您可以使用它启动 YaST 电源管理模块，从而编辑电源节省设置。
- **音量**：单击以控制声音音量。
- **SUSE 硬件工具**：单击以查看有关 PC 上设备的信息并进行配置。
- **SUSE Watcher**：单击以打开一个窗口，您可以使用它检查在线更新以及启动在线更新。
- **时钟**：显示当前时间。单击会调出显示当前日期的日历。
- **隐藏面板**：面板的端点作为*隐藏面板*按钮，这意味着如果您单击此图标，面板将向右滑动并消失，只剩下端点。再次单击，面板重新出现。您可以隐藏面板以为其他窗口腾出更多空间。

除了您在 SUSE 桌面上看到的内容，当您在面板上单击“主菜单”时出现的主菜单中还有许多其他选择。参见图 1-20。类似于 Windows 的“开始”按钮，主菜单是当您想运行应用程序时的起点。

![](img/11709a8f88c8cd03868a929dc94c0e2b_181_0.png)

SUSE 主菜单（参见图 1-20）有三大类——“最常用的应用程序”显示您最近使用的应用程序图标，“所有应用程序”组织您可以访问的应用程序，“操作”显示用于一些常见日常任务的按钮，例如锁定屏幕、运行命令或注销。您应该浏览“所有应用程序”类别，以熟悉 SUSE 作为桌面操作系统提供的功能。

### 介绍 Ubuntu 的 GNOME 桌面

Ubuntu 使用 GNOME 作为其 GUI 桌面，具有其特有的顶部和底部面板，如图 1-21 所示。与其他发行版的桌面不同，Ubuntu 不使用任何桌面图标，外观简洁。

![](img/11709a8f88c8cd03868a929dc94c0e2b_182_0.png)

### 图 1-21：初始的 Ubuntu 桌面。

- 应用程序菜单（主菜单）
- 系统菜单
- 位置菜单
- Firefox 网页浏览器
- Evolution
- 帮助
- 音量
- 更新
- 日期和时间
- 显示桌面
- 工作区切换器
- 已删除项

如图 1-21 所示，Ubuntu 的 GNOME 桌面具有以下主要功能：

- **应用程序菜单（主菜单）**：调出主菜单，您可以从中选择要运行的应用程序。
- **位置菜单**：显示一个菜单，您可以从中打开主文件夹、浏览计算机、连接到网络服务器以及搜索文件。
- **系统菜单**：调出一个菜单，您可以从中编辑各种应用程序首选项，执行系统管理任务，例如通过 Ubuntu 更新管理器安装和删除软件包、更新软件、获取在线帮助、锁定屏幕以及注销。
- **网页浏览器**：运行 Firefox 网页浏览器。
- **Evolution**：启动 Evolution 电子邮件和日历软件。
- **帮助**：在 Yelp 中显示在线帮助信息——这是 GNOME 的文档查看器。
- **音量**：显示一个音量控制条，您可以拖动滑块来更改声音的音量。
- **更新**：指示是否有可用的更新以安装。单击打开一个窗口，您可以查看可用更新并安装它们。请注意，当提示时，您必须输入您的普通用户密码。
- **日期和时间**：显示当前日期和时间；单击会调出显示当前日期的日历。
- **显示桌面**：单击以隐藏所有窗口并显示桌面。
- **工作区切换器**：每个方格显示不同的工作区。这与 KDE 桌面中的桌面分页器具有相同的功能。

探索三个菜单（应用程序、位置和系统），以查看您可以从这些菜单中的选择执行的任务类别。

### 介绍 Xandros 桌面

商业 Xandros 发行版的官方名称是 Xandros Desktop OS，因此 Xandros 附带一个设计良好的桌面也就不足为奇了。启动时，Xandros 会自动将您登录为用户（它使用您在安装期间定义的用户帐户），您将获得初始桌面，如图 1-22 所示。

Xandros 基于 Debian，它使用 KDE 的定制版本作为其桌面。如图 1-22 所示，您应该注意 Xandros 桌面上的以下关键元素：

- **桌面图标**：Xandros 桌面显示一系列桌面图标：用于已删除项的“回收站”图标，用于浏览主文件夹的图标，代表 Xandros 技术支持和快速入门指南链接的图标，Firefox 网页浏览器的快捷方式，以及用于连接到 Xandros 网络的图标（这是您在 Xandros 中下载和安装更新和新应用程序的方式）。您可以双击打开这些图标。双击的结果取决于图标。例如，如果您双击 Xandros 快速入门指南，该指南将在 Firefox 网页浏览器窗口中打开。另一方面，双击“主”图标会在 Xandros 文件管理器中打开您的主文件夹。





❖ **主菜单**：调出主菜单（见图 1-23），您可以从中启动应用程序、运行命令、获取帮助、切换用户或注销。
❖ **Firefox 网页浏览器**：运行 Mozilla Firefox 网页浏览器。
❖ **Thunderbird 邮件**：启动 Mozilla Thunderbird 邮件程序以访问您的电子邮件。
❖ **Xandros 文件管理器**：启动 Xandros 文件管理器，其布局和导航本地及远程文件系统的功能类似于 Windows 资源管理器。

![](img/11709a8f88c8cd03868a929dc94c0e2b_184_0.png)

## 160 介绍 Xandros 桌面

- **帮助**：单击以打开 Xandros 桌面帮助中心窗口，在那里您可以获取有关 Xandros 和 UNIX 的一些帮助。
- **显示桌面**：单击以隐藏所有窗口并显示桌面。
- **桌面翻页器**：单击每个方块以调出不同的桌面。
- **音量**：单击以通过拖动滑块更改声音音量。
- **更新**：单击以查看 Xandros 更新状态并打开 Xandros Networks 以执行在线更新。
- **锁定桌面**：单击以锁定屏幕，使任何人无法访问它。（您可以通过输入密码再次访问。）
- **注销**：单击以注销。（您必须确认确实想要注销。）
- **时钟**：显示当前时间。单击将调出“时间和日期”实用程序以设置日期和时间。
- **隐藏面板**：单击以隐藏面板。面板向右滑动并消失，只留下按钮。再次单击可查看面板。通过隐藏面板，您的应用程序窗口会有更多空间。

Xandros 使用简化的主菜单，如图 1-23 所示，当您单击面板上的主菜单时会出现该菜单。该菜单将所有应用程序组织在单个“应用程序”类别中。

您可以探索主菜单以了解随 Xandros 附带的应用程序的更多信息。我在本 miniBook 的第 4 章中提供了应用程序概览。

![](img/11709a8f88c8cd03868a929dc94c0e2b_185_0.png)

通过单击面板上的图标来试用 Xandros 文件管理器。从 Xandros 文件管理器中，您可以浏览系统中的各个文件夹，也可以访问局域网上的任何 Windows 共享。您可以执行所有常规操作：通过拖动移动或复制文件，双击文件以打开它们。我发现 Xandros 文件管理器是我 Xandros 会话的良好起点。

### 图 1-23：Xandros 桌面提供简化的主菜单。

![](img/11709a8f88c8cd03868a929dc94c0e2b_185_1.png)

## 第 2 章：命令 Shell

###### 本章内容

- 打开终端窗口和虚拟控制台
- 使用 bash shell
- 发现一些 Linux 命令
- 编写 shell 脚本

有时，事情就是不灵了。如果 GUI 桌面停止响应您的鼠标点击，您该怎么办？如果 GUI 根本没有启动呢？您仍然可以告诉您的 Linux 系统要做什么，但您必须通过在文本屏幕上输入命令来完成。在这些情况下，您将与 shell——Linux 命令解释器——一起工作。本章将介绍 bash shell（大多数 Linux 发行版中的默认 shell）。

当您弄清楚如何使用 shell 后，您甚至可能开始喜欢 Linux 命令的简洁和强大。然后，即使您是 GUI 爱好者，不久的将来您可能会发现自己启动一个终端窗口，并通过用奇怪的标点符号串联起来的两个或三个字母的命令让系统唱歌跳舞。（嘿，我可以做梦，不是吗？）

### 打开终端窗口和虚拟控制台

凡事都有始有终。如果您在 GUI 桌面上工作，例如 GNOME 或 KDE，您在哪里输入 shell 的命令？好问题。

到达 shell 的最简单方法是打开一个终端（也称为控制台）窗口。大多数发行版中的 GNOME 和 KDE GUI 都包含一个图标（或主菜单选项）以打开终端窗口。单击该图标或选择菜单选项以获取终端窗口。现在您可以随心所欲地输入命令了。

如果由于某种原因，GUI 似乎挂起了（您点击并输入但没有反应），您可以转向虚拟控制台。（物理控制台是显示器和键盘的组合。）虚拟控制台的理念是让您有能力在几个文本控制台之间切换，尽管您只有一个物理控制台。无论您是否运行 GUI，您都可以使用不同的文本控制台输入不同的命令。

要从 GNOME 或 KDE 桌面访问第一个虚拟控制台，请按 Ctrl+Alt+F1。按 Ctrl+Alt+F2 访问第二个虚拟控制台，依此类推。每个这些虚拟控制台都是一个文本屏幕，您可以在其中登录并输入 Linux 命令以执行各种任务。完成后，输入 `exit` 以注销。

![](img/11709a8f88c8cd03868a929dc94c0e2b_187_0.png)

您可以使用多达六个虚拟控制台。在大多数发行版中，第七个用于 GUI 桌面。要返回 GUI 桌面，请按 Ctrl+Alt+F7。

#### 使用 *Bash* Shell

如果您使用过 MS-DOS，您可能熟悉 `COMMAND.COM`，即 DOS 命令解释器。该程序显示臭名昭著的 `C:\>` 提示符。在 Windows 中，如果您打开命令窗口，可以看到此提示符。（要在 Microsoft Windows 中打开命令窗口，请选择开始 > 运行，在文本框中输入 **command**，然后单击确定。）

Linux 附带一个类似于 DOS 中 `COMMAND.COM` 的命令解释器，但它能做的事情多得多。Linux 命令解释器称为 *shell*。

许多 Linux 发行版中的默认 shell 是 *bash*。当您打开终端窗口或在文本控制台登录时，*bash* shell 会提示您输入命令。然后，当您输入命令时，shell 执行您的命令。顺便说一下，就像 Linux 有多个 GUI（GNOME 或 KDE）一样，除了 *bash* 之外，您还有其他 shell 的选择。例如，*c* shell 是一些人首选的替代 shell。您可以使用 `chsh` 命令轻松更改您的默认 shell。

除了标准的 Linux 命令外，*bash* 还可以执行任何计算机程序。因此，您可以在 shell 提示符下输入应用程序的名称（该名称通常比您在 GNOME 或 KDE 菜单中看到的名称更晦涩），shell 将启动该应用程序。

##### 理解 shell 命令的 *语法*

由于 shell 解释您输入的内容，了解 shell 如何处理您输入的文本很重要。所有 shell 命令都具有这种通用格式，以命令开头，后跟选项。（某些命令没有选项。）

```
command option1 option2 . . . optionN
```

这种在屏幕上单独一行中给出的命令通常被称为 *命令行*。在命令行上，您输入一个命令，后跟零个或多个选项（*或参数*）。这些选项字符串——*命令行选项*（*或命令行参数*）——修改命令的工作方式，以便您可以执行特定任务。

Shell 使用空格或制表符来区分命令和选项。当然，您通过使用空格或制表符将命令与选项以及选项彼此分隔开来帮助它。

选项可以包含空格——您只需将该选项放在引号内即可包含空格。例如，为了在密码文件中搜索我的名字，我输入以下 `grep` 命令（`grep` 用于在文件中搜索文本）：

```
grep "Naba Barkakati" /etc/passwd
```

当 `grep` 打印带有我名字的那一行时，它是这样的：

```
naba:x:1000:100:Naba Barkakati:/home/naba:/bin/bash
```

如果您创建一个带有您用户名的用户账户，请输入带有用户名作为参数的 `grep` 命令，以在 `/etc/passwd` 文件中查找该用户名。

在 `grep` 命令的输出中，您可以看到最后一个冒号（`:`）后面的 shell 名称（`/bin/bash`）。

当然，命令行选项的数量和格式取决于实际命令。通常，这些选项看起来像 `-X`，其中 X 是一个字符。例如，`ls` 命令列出目录的内容。您可以使用 `-l` 选项来查看更多详细信息。例如，这是在用户主目录中输入 `ls -l` 的结果：

```
total 0
drwxr-xr-x  2 naba users  48 2005-09-08 21:11 bin
drwx------  2 naba users 320 2005-09-08 21:16 Desktop
drwx------  2 naba users  80 2005-09-08 21:11 Documents
drwxr-xr-x  2 naba users  80 2005-09-08 21:11 public_html
drwxr-xr-x  2 naba users 464 2005-09-17 18:21 sdump
```

如果命令太长无法在一行中容纳，您可以按反斜杠键，然后按 Enter。然后，在下一行继续输入命令。例如，输入以下命令。（在每一行之后按 Enter。）

```
cat \
/etc/passwd
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_188_0.png)
![](img/11709a8f88c8cd03868a929dc94c0e2b_188_1.png)
![](img/11709a8f88c8cd03868a929dc94c0e2b_188_2.png)




cat 命令随后会显示 /etc/passwd 文件的内容。

你可以在单行上连接（即串联）几条较短的命令。只需使用分号（;）分隔这些命令即可。例如，以下命令：

```
cd; ls -1; pwd
```

会将当前目录更改为您的主目录，列出该目录的内容，然后显示该目录的名称。

##### 组合 shell 命令

你可以将简单的 shell 命令组合起来，以创建更复杂的命令。例如，假设你想查看名为 sbpcd 的设备文件是否位于系统的 /dev 目录中，因为某些文档指出你需要该设备文件来支持 Sound Blaster Pro CD-ROM 驱动器。你可以使用 `ls /dev` 命令获取 /dev 目录的列表，然后浏览该列表以查看其中是否包含 sbpcd。

不幸的是，/dev 目录中包含大量条目，你可能会发现很难找到名称中包含 sbpcd 的任何项。然而，你可以将 ls 命令与 grep 命令结合起来，构建出一行完全符合你需求的命令行。该命令行如下：

```
ls /dev | grep sbpcd
```

shell 将 ls 命令的输出（即目录列表）发送给 grep 命令，grep 命令则负责搜索字符串 sbpcd。那个垂直线（|）被称为管道，因为它充当两个程序之间的通道（想象一下水管）——第一个命令的输出被作为第二个命令的输入。

##### 控制命令的输入和输出

大多数 Linux 命令都有一个共同特征——它们始终从标准输入（通常是键盘）读取数据，并写入标准输出（通常是屏幕）。错误消息被发送到标准错误（通常也是屏幕）。这三个设备通常被称为 stdin、stdout 和 stderr。

你可以让命令从文件获取输入，然后将输出发送到另一个文件。顺便说一下，这个功能的高深术语叫做输入输出重定向或 I/O 重定向。

表 2-1 展示了常见 I/O 重定向命令的语法，接下来的几个部分将解释如何使用这些命令中的一些。

表 2-1 常见的标准 I/O 重定向

| 任务 | 命令语法 |
| :--- | :--- |
| 将 `stdout` 发送到文件 | `command > file` |
| 将 `stderr` 发送到文件 | `command 2> file` |
| 将 `stdout` 和 `stderr` 发送到文件 | `command > file 2>&1` |
| 从文件读取 `stdin` | `command < file` |
| 从 `file.in` 读取 `stdin` 并将 `stdout` 发送到 `file.out` | `command < file.in > file.out` |
| 将 `stdout` 追加到文件末尾 | `command >> file` |
| 将 `stderr` 追加到文件末尾 | `command 2>> file` |
| 将 `stdout` 和 `stderr` 追加到文件末尾 | `command >> file 2>&1` |
| 从键盘读取 `stdin` 直到输入字符 c | `command <<c` |
| 将 `stdout` 通过管道传输给 `command2` | `command | command2` |
| 将 `stdout` 和 `stderr` 通过管道传输给 `command2` | `command 2>&1 | command2` |

###### 从文件获取命令输入

如果你希望命令从文件读取数据，可以将标准输入重定向，使其来自该文件而不是键盘。例如，键入以下命令：

```
sort < /etc/passwd
```

此命令显示 `/etc/passwd` 文件中所有行的排序列表。在这种情况下，小于号（`<`）重定向了 `stdin`，使得 `sort` 命令从 `/etc/passwd` 文件读取输入。

###### 将命令输出保存到文件

要将命令的输出保存到文件中，请将标准输出重定向到文件。例如，键入 `cd` 切换到你的主目录，然后键入以下命令：

```
grep typedef /usr/include/* > typedef.out
```

此命令在 `/usr/include` 目录中的所有文件中搜索文本 `typedef` 的出现位置——然后将输出保存到名为 typedef.out 的文件中。

![](img/11709a8f88c8cd03868a929dc94c0e2b_191_0.png)

大于号（>）将 stdout 重定向到文件。此命令还展示了 bash 的另一个特性：当你使用星号（*）时，bash 会用指定目录中所有文件名的列表替换该星号。因此，/usr/include/* 表示 /usr/include 目录中的所有文件。

如果你想将命令的输出追加到现有文件的末尾，而不是将输出保存到新文件中，请使用两个大于号（>>），如下所示：

```
command >> filename
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_191_1.png)

将 stdout 发送到文件的另一个有趣用途是利用 cat 命令快速准备小型文本文件。例如，假设你想创建一个新的文本文件，在其中不断保存你键入的文本行，直到你键入 ZZ 并按下 Enter 键。你可以按以下方式完成此任务：

```
cat <<ZZ > input.txt
```

键入此命令后，你可以继续键入各行，并在完成后单独一行键入 ZZ。你键入的所有内容都应保存在 input.txt 文件中。

###### 将错误消息保存到文件

有时你键入一个命令，它会生成大量错误消息，滚动速度之快以至于你无法分辨发生了什么。查看所有错误消息的一种方法是将错误消息保存到文件中，这样你就可以弄清楚到底发生了什么。你可以通过将 stderr 重定向到文件来实现这一点。

例如，键入以下命令：

```
find / -name COPYING -print 2> finderr
```

此命令在整个文件系统查找名为 COPYING 的文件，但将所有错误消息保存在 finderr 文件中。数字 2 后跟大于号（>>，此处指重定向符号，原文语境为 > 但习惯上配合 2 代表 stderr，通常写作 2>）将 stderr 重定向到文件。*注：原文此处写的是 2>，但在前文表格中“Send stderr to file”对应的是 `command 2> file`，而“Append stderr”对应 `2>>`。根据上下文“save ... in a finderr file”，这里是新建或覆盖文件，故通常使用 `2>`。原文此处写的是 `2>`。*

![](img/11709a8f88c8cd03868a929dc94c0e2b_191_2.png)

如果你只是想丢弃错误消息而不是将它们保存到文件中，请使用 /dev/null 作为文件名，如下所示：

```
find / -name COPYING -print 2> /dev/null
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_191_3.png)

那个 /dev/null 是一个特殊文件——常被称为“比特桶”（bit bucket），有时甚至被美化为“天空中的伟大比特桶”（the Great Bit Bucket in the Sky）——它简单地丢弃所接收的一切。所以现在当你听到诸如“你的邮件可能掉进了比特桶”之类的短语时，你就知道他们的意思了。

##### 利用自动命令补全少打字

许多命令接收文件名作为参数。例如，要查看 /etc/modprobe.conf 文本文件的内容，请键入以下命令：

```
cat /etc/modprobe.conf
```

cat 命令显示 /etc/modprobe.conf 文件。对于任何接收文件名作为参数的命令，你都可以使用 bash 的一个功能来避免键入完整的文件名。你只需键入最基本的部分——即足以在目录中唯一标识该文件的前几个字符即可。

要查看示例，请键入 cat /etc/mod，但不要按 Enter；而是按 Tab 键。bash 会自动补全文件名，因此命令变为 cat /etc/modprobe.conf。现在按 Enter 运行该命令。

每当你键入文件名时，在文件名前几个字符之后按 Tab 键。bash 通常可以补全文件名，这样你就不必键入整个名称。如果你输入字符不足以唯一标识文件，bash 会发出哔声。只需再键入几个字符并按一次 Tab 键即可。

![](img/11709a8f88c8cd03868a929dc94c0e2b_192_0.png)

##### 玩转星号和问号

你可以通过另一种方式避免键入长文件名。（毕竟，为用户减少工作量才是计算机的意义所在，不是吗？）

这个特定的技巧涉及使用星号（*）和问号（?）以及一些其他技巧。这些特殊字符被称为通配符，因为它们匹配文本行中零个或多个字符。

如果你熟悉 MS-DOS，可能使用过如 COPY *.* A: 这样的命令来将当前目录中的所有文件复制到 A: 驱动器。bash 也接受文件名中的类似通配符。正如你所预期的，bash 提供的通配符选项比 MS-DOS 命令解释器多得多。

在 bash 中可以使用三种类型的通配符：

- 星号（*）字符匹配文件名中的零个或多个字符。这意味着 * 表示目录中的所有文件。
- 问号（?）匹配任意单个字符。如果你键入 test?，它匹配任何以 test 开头的五个字符的文本。
- 方括号内的一组字符匹配该集合中的任意单个字符。例如，字符串 [aB]* 匹配任何以 a 或 B 开头的文件名。




通配符在你想对大量文件执行操作时非常实用。例如，要将 `/media/cdrom` 目录中的所有文件复制到当前目录，请输入以下命令：

```bash
cp /media/cdrom/* .
```

bash 会用 `/media/cdrom` 目录中所有文件的名称替换通配符 *。命令末尾的句点代表当前目录。

你可以将星号与文件名的其他部分组合使用，以选择更具体的文件组。假设你想使用 `grep` 命令在满足以下条件的 `/usr/include` 目录的所有文件中搜索文本 `typedef struct`：

- **文件名以 s 开头。**
- **文件名以 .h 结尾。**

通配符规范 `s*.h` 表示满足这些条件的所有文件名。因此，你可以使用以下命令执行搜索：

```bash
grep "typedef struct" /usr/include/s*.h
```

该字符串包含一个空格，这是你希望 `grep` 命令查找的内容，因此必须用引号将该字符串括起来。这样，bash 就不会试图将该文本中的每个单词解释为独立的命令行参数。

问号 (?) 匹配单个字符。假设当前目录中有四个文件——image1.pcx、image2.pcx、image3.pcx 和 image4.pcx。要将这些文件复制到 `/mnt/floppy` 目录，请使用以下命令：

```bash
cp image?.pcx /media/floppy
```

bash 会用任意单个字符替换单个问号，并将这四个文件复制到 /mnt。

第三种通配符格式——[ . . . ]——匹配由方括号包围的特定字符集中的单个字符。你可能希望将此格式与其他通配符结合使用，以将匹配的文件名缩小到更小的集合。要查看 `/etc/X11/xdm` 目录中所有以 x 或 X 开头的文件名列表，请输入以下命令：

```bash
ls /etc/X11/xdm/[xX]*
```

##### 重复之前输入的命令

为了让你轻松地重复长命令，*bash* 存储多达 500 条旧命令作为 *命令历史记录*的一部分（基本上只是一个旧命令列表）。要查看命令历史记录，请输入 **history**。*bash* 会显示旧命令的编号列表，包括你在之前登录期间输入的命令。

如果命令列表太长，你可以限制想要查看的旧命令数量。例如，要仅查看最近十条命令，请输入此命令：

```bash
history 10
```

要重复 **history** 命令显示列表中的某个命令，只需输入一个感叹号 (!)，后跟该命令的编号。要重复编号为 3 的命令，请输入 **!3**。

你可以在不知道命令编号的情况下重复命令。假设几分钟前你输入了 **more /usr/lib/X11/xdm/xdm-config**，现在你想再次查看该文件。要重复上一个 **more** 命令，请输入以下内容：

```bash
!more
```

通常，你可能想要重复刚刚输入的最后一条命令，也许稍作修改。例如，你可能已经使用 **ls -l** 命令显示了目录内容。要重复该命令，请按照以下格式输入两个感叹号：

```bash
!!
```

有时，你可能想要重复上一个命令，但为其添加额外参数。假设 **ls -l** 显示了太多文件。只需重复该命令，但通过 **more** 命令将输出管道传输，如下所示：

```bash
!! | more
```

*bash* 将两个感叹号替换为上一个命令，然后将 | **more** 附加到该命令之后。

![](img/11709a8f88c8cd03868a929dc94c0e2b_194_0.png)

> 回想之前命令的最简单方法：只需按向上箭头键，*bash* 就会沿着你之前输入的命令历史向前推进。要在命令历史中向前移动，请按向下箭头键。

##### 发现和使用 Linux 命令

你在 shell 提示符下输入 Linux 命令。这里所说的 *Linux 命令*，是指 `bash` shell 理解的一些命令以及随 Linux 提供的命令行实用程序。在本节中，我将向你介绍几个主要的 Linux 命令类别。

我不可能在本章中涵盖每一个 Linux 命令，但我希望通过展示表 2-2 中常见 Linux 命令的列表，让你对命令的广度有一个初步了解。该表格按类别列出了常见的 Linux 命令。在开始记忆任何 Linux 命令之前，请先浏览此表格。

###### 表 2-2: 常见 Linux 命令概览

| **命令名称** | **操作** |
| :--- | :--- |
| **获取在线帮助** | |
| `apropos` | 查找指定关键字的在线手册页 |
| `info` | 显示关于指定命令的在线帮助信息 |
| `man` | 显示在线帮助信息 |
| `whatis` | 类似于 `apropos`，但仅搜索完整单词 |
| **使命令更易用** | |
| `alias` | 为长命令定义缩写 |
| `type` | 显示命令的类型和位置 |
| `unalias` | 删除使用 `alias` 定义的缩写 |
| **管理文件和目录** | |
| `cd` | 更改当前目录 |
| `chmod` | 更改文件权限 |
| `chown` | 更改文件所有者和组 |
| `cp` | 复制文件 |
| `ln` | 创建指向文件和目录的符号链接 |
| `ls` | 显示目录的内容 |
| `mkdir` | 创建一个目录 |
| `mv` | 重命名文件以及将文件从一个目录移动到另一个目录 |
| `rm` | 删除文件 |
| `rmdir` | 删除目录 |
| `pwd` | 显示当前目录 |
| `touch` | 更新文件的时间戳 |
| **查找文件** | |
| `find` | 根据指定条件（如名称和大小）查找文件 |
| `locate` | 使用定期更新的文件名数据库查找文件。（该数据库由 *updatedb* 程序创建。） |
| `whereis` | 在通常放置 *可执行*（也称为 *二进制*）文件的典型目录中查找文件 |
| `which` | 在 PATH 环境变量列出的目录中查找文件 |
| **处理文件** | |
| `cat` | 在标准输出上显示文件（可用于将几个文件连接成一个大的文件） |
| `cut` | 从文件每行文本中提取指定部分 |
| `dd` | 将数据块从一个文件复制到另一个文件（用于从设备复制数据） |
| `diff` | 比较两个文本文件并找出任何差异 |
| `expand` | 将所有制表符转换为空格 |
| `file` | 显示文件中的数据类型 |
| `fold` | 将每行文本换行以适应指定宽度 |
| `grep` | 在文本文件中搜索正则表达式 |
| `less` | 一次显示一页文本文件（也可以向后翻页） |
| `lpr` | 打印文件 |
| `more` | 一次显示一页文本文件（仅向前翻页） |
| `nl` | 为文本文件中的所有非空行编号并将这些行打印到标准输出 |
| `paste` | 连接几个文件的对应行 |
| `patch` | 使用文件原始版本和修订版本之间的差异更新文本文件 |
| `sed` | 在应用指定编辑命令的同时将文件复制到标准输出 |
| `sort` | 对文本文件中的行进行排序 |
| `split` | 将文件分割成几个具有指定大小的较小文件 |
| `tac` | 反转文件（最后一行首先显示，依此类推） |
| `tail` | 显示文件末尾的几行 |
| `tr` | 在整个文件中将一组字符替换为另一组字符 |
| `uniq` | 从文本文件中消除重复行 |
| `wc` | 统计文本文件中行数、单词数和字符数 |
| `zcat` | 显示压缩文件（解压后） |
| **归档和压缩文件** | |
| `zless` | 一次显示一页压缩文件（也可以向后翻页） |
| `zmore` | 一次显示一页压缩文件 |
| `compress` | 压缩文件 |
| `cpio` | 将文件复制到归档中或从归档中复制 |
| `gunzip` | 解压用 GNU Zip (gzip) 压缩的文件 |
| `gzip` | 使用 GNU Zip 压缩文件 |
| `tar` | 创建一个或多个目录中文件的归档（最初用于磁带归档） |
| `uncompress` | 解压用 compress 压缩的文件 |
| **管理进程** | |
| `bg` | 在后台运行被中断的进程 |
| `fg` | 在前台运行进程 |
| `free` | 显示系统中空闲和已用内存的数量 |
| `halt` | 关闭 Linux 并停止计算机 |
| `kill` | 向进程发送信号（通常用于终止进程） |
| `ldd` | 显示运行程序所需的共享库 |
| `nice` | 以较低优先级运行进程（称为 *nice* 模式） |
| `ps` | 显示当前运行进程列表 |
| `printenv` | 显示当前环境变量 |
| `pstree` | 类似于 *ps*，但清晰地显示父子关系 |
| `reboot` | 停止 Linux 然后重启计算机 |
| `shutdown` | 关闭 Linux |
| `top` | 显示最耗处理器和内存的进程列表 |
| `uname` | 显示系统和 Linux 内核的信息 |
| **管理用户** | |
| `chsh` | 更改 *shell*（命令解释器） |
| `groups` | 打印包含指定用户的组列表 |
| `id` | 显示指定用户名的用户和组 ID |
| `passwd` | 更改密码 |
| `su` | 作为其他用户或 *root*（在不带任何参数调用时）启动新的 shell |




##### 管理文件系统

| 命令名称 | 功能 |
| :--- | :--- |
| `df` | 汇总所有已挂载存储设备上的可用空间 |
| `du` | 显示磁盘使用情况信息 |
| `fdformat` | 格式化软盘 |
| `fdisk` | 对硬盘进行分区 |
| `fsck` | 检查和修复文件系统 |
| `mkfs` | 创建新的文件系统 |
| `mknod` | 创建设备文件 |
| `mkswap` | 在文件或硬盘分区中创建 Linux 交换空间 |
| `mount` | 将设备（例如 CD-ROM）挂载到文件系统中的一个目录 |
| `swapoff` | 停用交换空间 |
| `swapon` | 启用交换空间 |
| `sync` | 将*缓冲区*（保存在内存中）的数据写入文件 |
| `tty` | 显示当前终端的设备名称 |
| `umount` | 从文件系统中卸载设备 |

###### 使用日期和时间

| 命令名称 | 功能 |
| :--- | :--- |
| `cal` | 显示指定月份或年份的日历 |
| `date` | 显示当前日期和时间或设置新的日期和时间 |

##### 成为 root（超级用户）

当你想要执行需要高权限级别的操作（例如管理你的系统）时，你必须变成 `root`。通常，你使用日常用户名以普通用户身份登录。但是，当你需要超级用户权限时，请使用以下命令变成 `root`：

```bash
su -
```

这是 `su` 后面跟一个空格和减号（或连字符）。然后 shell 会提示你输入 `root` 密码。输入密码并按 Enter 键。

![](img/11709a8f88c8cd03868a929dc94c0e2b_198_0.png)

Knoppix 不需要你输入任何密码即可变成 `root`。在你输入 `su -` 并按 Enter 键后，你就变成了 `root`。（提示符会改变以表明身份的变化。）顺便说一下，这并没有听起来那么糟糕，因为 Knoppix 是一个 Live CD 发行版，你直接通过 CD-ROM 运行它，其目的通常是使用 Knoppix 来试用 Linux 或修复现有 Linux 安装中的某些问题。

当你作为 *root* 完成所有你想做的事情后（你具有作为 *root* 执行任何操作的权限），输入 `exit` 返回到你正常的用户名。

除了使用 `su` – 命令变成 *root* 之外，你还可以输入 **sudo** 后跟你想作为 *root* 运行的命令。在 Ubuntu 中，你必须使用 **sudo** 命令，因为安装 Ubuntu 时你无法设置 *root* 用户。如果你列在 `/etc/sudoers` 文件中的授权用户列表中，**sudo** 会执行命令，就好像你是以 *root* 身份登录一样。输入 `man sudoers` 以阅读有关 `/etc/sudoers` 文件的更多信息。

![](img/11709a8f88c8cd03868a929dc94c0e2b_199_0.png)

##### 管理进程

每当 shell 执行你输入的命令时，它都会启动一个进程。Shell 本身是一个进程，shell 运行的任何脚本或程序也是进程。

使用 `ps ax` 命令来查看进程列表。当你输入 **ps ax** 时，`bash` 会显示当前的进程集。以下是我输入 `ps ax -cols 132` 时的几行输出。（我还包括 `--cols 132` 选项，以确保你可以看到每个命令的完整内容。）

```
PID TTY STAT TIME COMMAND
 1 ? S 0:01 init [5]
 2 ? SN 0:00 [ksoftirqd/0]
 3 ? S< 0:00 [events/0]
 4 ? S< 0:00 [khelper]
 9 ? S< 0:00 [kthread]
 19 ? S< 0:00 [kcpid]
 75 ? S< 0:00 [kblockd/0]
 115 ? S 0:00 [pdflush]
 116 ? S 0:01 [pdflush]
 118 ? S< 0:00 [aio/0]
 117 ? S 0:00 [kswapd0]
 711 ? S 0:00 [kseriod]
 1075 ? S< 0:00 [kaiser/0]
 2086 ? S 0:00 [kjournald]
 2239 ? S<s 0:00 /sbin/udev -d
... lines deleted ...
 6374 ? S 1:51 /usr/X11R6/bin/X : 0 -audit 0 -auth
 /var/lib/gdm/:0.Xauth -nolisten tcp vt7
 6460 ? Ss 0:02 /opt/gnome/bin/gdmreorder
 6471 ? Ss 0:00 sshtd: naba [priv]
 6675 ? Ss 0:00 sshd: naba@pts/0
 6676 pts/0 Ss 0:00 -bash
 6712 pts/0 S 0:00 vaftpd
 14752 ? S 0:00 pickup -l -t fifo -u
 14752 pts/0 R+ 0:00 ps ax -cols 132
```

在此列表中，第一列的标题为 **PID**，显示每个进程的一个数字。**PID** 代表*进程 ID*（标识），这是由 Linux 内核分配的顺序号。如果你浏览 `ps ax` 命令的输出，你会看到 `init` 命令是第一个进程，其 PID（进程号）为 1。这就是为什么 `init` 被称为“所有进程之母”的原因。

![](img/11709a8f88c8cd03868a929dc94c0e2b_199_1.png)

`COMMAND` 列显示创建每个进程的命令，`TIME` 列显示进程使用的累计 CPU 时间。`STAT` 列显示进程的状态 —— `S` 表示进程正在睡眠，`R` 表示正在运行。状态字母后面的符号有进一步的含义；例如 `<` 表示高优先级进程，`+` 表示进程在前台运行。`TTY` 列显示与进程关联的终端（如果有）。

进程 ID（或进程号）在你需要强制停止错误进程时很有用。查看 `ps ax` 命令的输出并记下问题进程的 `PID`。然后，使用带有该进程号的 `kill` 命令。例如，要停止进程号 8550，首先输入以下命令：

```
kill 8550
```

如果进程在五秒钟后仍未停止，请重复该命令。停止顽固进程的下一步是输入 `kill -INT pid`，其中 `pid` 是进程号。如果这不起作用，请尝试以下命令作为最后手段：

```
kill -9 8550
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_200_0.png)

-9 选项意味着向进程发送信号号 9。巧合的是，信号号 9 是 `KILL` 信号，这应该会导致进程退出。你也可以将此命令输入为 `kill -KILL pid`，其中 `pid` 是进程 ID。

##### 处理日期和时间

你可以使用 `date` 命令来显示当前日期和时间或设置新的日期和时间。在 shell 提示符处输入 `date`，你会得到类似以下结果：

```
Mon Dec  5 20:51:07 EST 2005
```

如你所见，单独使用 `date` 命令可以显示当前日期和时间。

要设置日期，请以 `root` 身份登录，然后输入 `date` 后跟 `MMDDhhmmYYYY` 格式日期和时间，其中每个字符都是数字。例如，要将日期和时间设置为 2006 年 12 月 31 日下午 9:30，你输入：

```
date 123121302006
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_200_1.png)

MmDDhhmmYYYY 日期和时间格式类似于 24 小时制军用时钟，并具有以下含义：

-   Mm 是月份的双位数（01 到 12）。
-   DD 是月份中天数双位数（01 到 31）。
-   hh 是 24 小时制小时的双位数。（00 是午夜，23 是晚上 11 点。）
-   mm 是分钟的双位数（00 到 59）。
-   YYYY 是四位数的年份（例如 2006）。

另一个有趣的与日期相关的命令是 `cal`。如果你输入 `cal` 没有任何选项，它会打印当前月份的日历。如果你输入 `cal` 后跟一个数字，`cal` 会将该数字视为年份，并打印该年份的日历。要查看特定年份中特定月份的日历，请提供月份号（1 = 一月，2 = 二月，依此类推），后跟年份。因此，要查看 2006 年一月的日历，输入 `cal 1 2006`，你将得到该月份的日历，如下所示：

```
        January 2006
 Su Mo Tu We Th Fr Sa
  1  2  3  4  5  6  7
  8  9 10 11 12 13 14
 15 16 17 18 19 20 21
 22 23 24 25 26 27 28
 29 30 31
```

##### 处理文件

你可以使用 `grep` 在文本文件中搜索，使用 `more` 按屏幕逐屏查看文本文件。例如，要在 `/etc/passwd` 文件中搜索我的用户名，我使用：

```
grep naba /etc/passwd
```

要按屏幕逐屏查看 `/etc/inittab` 文件，我输入：

```
more /etc/inittab
```

当每个屏幕暂停时，我按空格键转到下一页。

许多其他 Linux 命令都在文件上运行——主要是文本文件，但有些命令也适用于任何文件。接下来我将描述一些文件处理工具。




我总是对文件大小感到好奇。对于文本文件，字符数基本上就是文件的字节大小（因为每个字符占用一个字节的存储空间）。那么单词和行数呢？

Linux 的 `wc` 命令派上用场了。`wc` 命令显示文本文件中字符、单词和行的总数。例如，输入 `wc /etc/inittab`，你会看到类似以下的输出：

```
97   395   2926 /etc/inittab
```

在这种情况下，`wc` 报告 `/etc/inittab` 文件中有 97 行、395 个单词和 2,926 个字符。如果你只想查看文件中的行数，请使用 `-l` 选项并输入 `wc -l /etc/inittab`。产生的输出应类似于以下内容：

```
97 /etc/inittab
```

如你所见，使用 `-l` 选项时，`wc` 仅显示行数。

如果不指定文件名，`wc` 命令会等待标准输入。你可以使用 shell 的管道功能（`|`）将其他命令的输出传递给 `wc`，这在某些情况下会非常方便。

![](img/11709a8f88c8cd03868a929dc94c0e2b_202_0.png)

假设你想粗略统计系统中正在运行的进程数量。你可以使用 `ps ax` 命令获取所有进程的列表，但不要手动计算行数，只需将 `ps` 的输出管道到 `wc`，即可自动获得粗略计数：

```
ps ax | wc -l
86
```

这里 `ps` 命令产生了 86 行输出。由于第一行仅显示表格列的标题，因此你可以估计系统中大约有 85 个进程正在运行。（当然，这个计数可能还包括用于运行 `ps` 和 `wc` 命令的进程，但谁在*认真*计数呢？）

##### 排序文本文件

你可以使用 `sort` 命令对文本文件中的行进行排序。要了解 `sort` 命令的工作原理，首先输入 `more /etc/passwd` 以查看 `/etc/passwd` 文件的当前内容。现在输入 `sort /etc/passwd` 以查看按字母顺序排序的行。如果你想要对一个文件进行排序并将排序后的版本保存到另一个文件，你必须使用 `bash` shell 的输出重定向功能，如下所示：

```
sort /etc/passwd > ~/sorted.text
```

此命令对 `/etc/passwd` 文件中的行进行排序，并将输出保存在主目录中名为 `sorted.text` 的文件中。

##### 替换或删除文件中的字符

另一个有趣的命令是 `tr` —— 它在整个文件中将一组字符替换为另一组字符（或删除选定的字符）。假设你偶尔需要在 Linux 系统上使用 MS-DOS 文本文件。尽管你可能期望在任何系统上使用文本文件都没有问题，但你会发现一个陷阱：DOS 使用回车符后跟换行符来标记每行的结束，而 Linux 仅使用换行符。

![](img/11709a8f88c8cd03868a929dc94c0e2b_203_0.png)

在你的 Linux 系统中，你可以使用带有 `-d` 选项的 `tr` 命令来去除 DOS 文本文件中多余的回车符。基本上，要将名为 `filename.dos` 的 DOS 文本文件转换为名为 `filename.linux` 的 Linux 文本文件，请输入以下命令：

```
tr -d '\015' < filename.dos > filename.linux
```

在此命令中，`\015` 表示八进制表示法中的回车符代码。

##### 将文件拆分为多个较小的文件

当你想要将文件复制到软盘但文件太大无法放入单个软盘时，`split` 命令非常实用。你可以使用 `split` 命令将文件拆分为多个较小的文件，每个文件都可以放入软盘中。

默认情况下，`split` 每个文件放入 1,000 行。新的拆分文件由字母组命名，例如 `aa`、`ab`、`ac` 等。你可以指定文件名的前缀。例如，要将一个大文件 `hugefile.tar` 拆分为适合几个高密度 3.5 英寸软盘的小文件，请按以下方式使用 `split`：

```
split -b 1440K hugefile.tar part.
```

此命令将 `hugefile.tar` 文件拆分为 `1440K` 的块，以便每个块都可以放入软盘。该命令创建名为 `part.aa`、`part.ab`、`part.ac` 等文件。

要将拆分后的文件合并回单个文件，请按如下方式使用 **cat** 命令：

```
cat part.?? > hugefile.tar
```

在这种情况下，两个问号（**??**）匹配文件名中的任意两个字符的扩展名。换句话说，文件名 **part.??** 匹配所有诸如 part.12、part.aa、part.ab、part.2b 等文件名。

##### 编写 Shell 脚本

如果你曾经使用过 MS-DOS，你可能还记得 MS-DOS *批处理文件*。这些是包含 MS-DOS 命令的文本文件。类似地，*shell 脚本*也是包含许多 shell 命令的文本文件。

如果你不是程序员，你可能会对编程感到担忧，但 shell 编程可以像将几个命令存储在文件中一样简单。此刻，你可能还无法编写复杂的 shell 脚本，但你完全可以尝试一个简单的 shell 脚本。

要尝试一点 shell 编程，请在 shell 提示符处准确输入以下文本，完成后按下 Ctrl+D：

```
cat > simple
#!/bin/sh
echo "This script's name is: $0"
echo Argument 1: $1
echo Argument 2: $2
```

按下 Ctrl+D。

**cat** 命令将当前目录更改为你的主目录。然后 **cat** 命令显示下一行以及你在按下 Ctrl+D 之前输入的任何其他行。在这种情况下，我使用 **>** simple 将输出发送到名为 simple 的文件。按下 Ctrl+D 后，**cat** 命令结束，你再次看到 shell 提示符。你创建了一个名为 simple 的文件，其中包含以下 shell 脚本：

```
#!/bin/sh
echo "This script's name is: $0"
echo Argument 1: $1
echo Argument 2: $2
```

第一行使 Linux 运行 *bash shell* 程序（名称为 /bin/bash）。然后 shell 读取脚本中的其余行。

# 第二卷

## 第 2 章

掌控 Shell

就像大多数 Linux 命令接受命令行选项一样，**bash** 脚本也接受命令行选项。在脚本内部，你可以将选项称为 **$1**、**$2** 等。特殊名称 **$0** 指代脚本本身的名称。

要运行此 shell 脚本，首先你必须使用以下命令使文件可执行（即将其转换为程序）：

```
chmod +x simple
```

现在输入 **./simple one two** 来运行脚本，它将显示以下输出：

```
This script's name is: ./simple
Argument 1: one
Argument 2: two
```

脚本名称前的 **./** 前缀表示 **simple** 文件位于当前目录中。

该脚本仅打印脚本的名称以及用户在脚本名称后输入的前两个命令行选项。

接下来，尝试使用几个参数运行脚本，如下所示：

```
./simple "This is one argument" second-argument third
This script's name is: ./simple
Argument 1: This is one argument
Argument 2: second-argument
```

Shell 将双引号内的整个字符串视为单个参数。否则，Shell 使用空格作为命令行中参数之间的分隔符。

大多数有用的 shell 脚本比这个简单脚本更复杂，但这个简单练习让你对如何编写 shell 脚本有了一个大致的了解。

将 Linux 命令放在文件中，并使用 **chmod** 命令使文件可执行。就这样！你创建了一个 shell 脚本！

## 第 3 章：浏览 Linux 文件系统

###### 本章内容

- ✓ 理解 Linux 文件系统
- ✓ 使用 Linux 命令浏览文件系统
- ✓ 理解文件权限
- ✓ 使用 Linux 命令操作文件和目录

为了很好地使用文件和目录，你需要理解层次化文件系统的概念。即使你使用图形用户界面（GUI）文件管理器来访问文件和文件夹（文件夹也称为*目录*），了解文件系统的布局也会对你有益。

在本章中，我将向你介绍 Linux 文件系统，并让你发现如何使用几个 Linux 命令来处理文件和目录。

### 理解 Linux 文件系统

与其他操作系统一样，Linux 在文件和目录中组织信息。目录反过来又包含文件。*目录*是一个特殊的文件，可以包含其他文件和目录。由于*目录*可以包含其他目录，这种文件组织方法形成了层次结构。这种文件的层次组织被称为*文件系统*。

Linux 文件系统提供了对 PC 上所有存储的统一视图。文件系统有一个单一的*根*目录，由正斜杠 (/) 表示。在*根*目录内是文件和目录的层次结构。文件系统的部分可以驻留在不同的物理介质上，例如硬盘、软盘和 CD-ROM。图 3-1 说明了 Linux 文件系统的概念（在任何 Linux 系统中都相同）以及它如何跨越多个物理设备。




#### 图 3-1：
Linux 文件系统提供了一种统一的存储视图，该视图可能跨越多个存储设备。

![](img/11709a8f88c8cd03868a929dc94c0e2b_207_0.png)

如果您熟悉 MS-DOS 或 Windows，您可能会发现 Linux 文件系统中缺少某些内容：您在 Linux 中找不到驱动器字母。所有磁盘驱动器和 CD-ROM 驱动器都是单一文件系统的一部分。

在 Linux 中，您可以使用长的文件名（最长 256 个字符），并且文件名是区分大小写的。这些文件名通常具有多个扩展名，例如 `sample.tar.Z`。UNIX 文件名可以采用多种形式，例如：`index.html`、`Makefile`、`binutils-2.15.92.0.2-5.i386.rpm`、`vsftpd_2.0.3-1_i386.deb`、`bash_profile` 和 `httpd_src.tar.gz`。

为了定位文件，您需要不仅仅知道文件名。您还需要关于目录层次结构的信息。显示通往文件的完整目录层次结构扩展文件名被称为 *路径名*。顾名思义，它是通过文件系统迷宫到达文件的路径。图 3-2 展示了 Linux 中文件的典型路径名。

如图 3-2 所示，路径名包含以下部分：

- 根目录，由前斜杠 (/) 字符指示。
- 目录层次结构，每个目录名与前一个目录名之间由前斜杠 (/) 字符分隔。最后一个目录名后会出现一个 /。
- 文件名，包含名称和一个或多个可选的扩展名。（每个扩展名前会出现一个点。）

#### 图 3-2：
文件的路径名显示了通向该文件的目录序列。

![](img/11709a8f88c8cd03868a929dc94c0e2b_208_0.png)

Linux 文件系统有一组定义明确的第一层目录，其中一些目录具有特定用途。如果您知道这些目录的用途，探索文件系统就会更容易。当您面对新情况时，您也更擅长猜测应该在何处寻找特定类型的文件。表 3-1 简要描述了 Linux 文件系统的第一层目录。

##### 表 3-1 Linux 文件系统的第一层目录

| 目录 | 描述 |
| :-- | :-- |
| / | 此 *根* 目录构成了文件系统的基础。所有文件和目录在逻辑上都包含在 *根* 目录中，无论其物理位置在哪里。 |
| /bin | 包含属于 Linux 操作系统一部分的可执行程序。许多 Linux 命令，例如 *cat*、*cp*、*ls*、*more* 和 *tar*，位于 /bin 中。 |
| /boot | 包含 Linux 内核以及 LILO 和 GRUB 启动管理器所需的其他文件。（内核和其他文件可以位于任何位置，但将它们放在 /boot 目录中是惯例。） |
| /dev | 包含代表连接到系统的设备的特殊文件。 |
| /etc | 包含大多数系统配置文件和初始化脚本（在 /etc/rc.d 子目录中） |
| /home | 所有用户主目录的约定位置。例如，用户 naba 的主目录是 /home/naba。 |
| /lib | 包含存储在 /sbin 和 /bin 目录中的程序所需的所有库文件（包括可加载的驱动程序模块），这些是启动 Linux 所必需的 |
| /lost+found | 用于丢失文件的目录。每个磁盘分区都有一个 lost+found 目录。 |
| /media | 用于挂载可移动介质（如 CD/DVD-ROM 驱动器、软盘和 Zip 磁盘）上文件系统的目录。包含用于挂载软盘的 /media/Floppy 目录以及用于挂载 CD/DVD-ROM 驱动器的 /media/cdrom 或 /media/cdrom0 目录。如果您有 CD/DVD 刻录机，您会看到 /media/cdrecorder 目录而不是 /media/cdrom。 |
| /mnt | 用于临时挂载文件系统的目录 |
| /opt | 为大型应用软件包提供存储区域。例如，一些发行版将 OpenOffice.org 办公套件安装在 /opt 目录中。 |
| /proc | 一个特殊目录，包含有关在 Linux 系统中运行的进程的各种信息 |
| /root | root 用户的主目录 |
| /sbin | 包含代表通常用于系统管理任务且由 root 用户使用的命令的可执行文件。例如 *halt* 和 *shutdown* 命令位于 /sbin 目录中。 |
| /srv | 包含由此系统提供的服务（如 Web 和 FTP）的数据 |
| /sys | 一个特殊目录，包含 Linux 内核看到的设备信息 |
| /tmp | 任何用户都可以用作 *scratch* 目录的临时目录，这意味着该目录的内容被认为是不重要的，并且通常在每次系统启动时删除 |
| /usr | 包含许多重要程序的子目录，例如 X Window 系统（位于 */usr/X11R6* 目录中）和在线手册。（表 3-2 展示了 */usr* 中*部分标准的*子目录。） |
| /var | 包含各种系统文件（如日志）以及用于存放其他信息的目录，例如 Web 服务器和匿名 FTP 服务器的文件 |

*/usr* 和 */var* 目录还包含许多标准子目录。表 3-2 列出了 */usr* 中的重要子目录。表 3-3 展示了 */var* 目录的类似细分。

##### 表 3-2 重要的 */usr* 子目录

| 子目录 | 描述 |
| :--- | :--- |
| /usr/X11R6 | 包含 X Window 系统软件 |
| /usr/bin | 包含更多 Linux 命令的可执行文件，包括在 Linux 中常见但不是核心 Linux 操作系统一部分的实用程序 |
| /usr/games | 包含一些旧的 Linux 游戏 |
| /usr/include | 包含 C 和 C++ 编程语言的标题文件（文件名以 .h 结尾）；还包括位于 */usr/include/X11* 目录中的 X11 标题文件和位于 */usr/include/linux* 目录中的 Linux 内核标题文件 |
| /usr/lib | 包含 C 和 C++ 编程语言的库；还包含许多其他库，如数据库库、图形工具包库等 |
| /usr/local | 包含本地文件。例如，`/usr/local/bin` 目录被指定为在任何系统上开发的任何可执行程序的位置。 |
| /usr/sbin | 包含许多管理命令，例如电子邮件和网络命令 |
| /usr/share | 包含共享数据，例如许多应用的默认配置文件和图像。例如，`/usr/share/gnome` 包含 GNOME 桌面的各种共享文件，`/usr/share/doc` 包含许多 Linux 应用（如 `bash` shell、Sawfish 窗口管理器和 GIMP 图像处理程序）的文档文件。 |
| /usr/share/man | 包含在线手册（您可以使用 `man` 命令阅读） |
| /usr/src | 包含 Linux 内核（核心操作系统）的源代码 |

##### 表 3-3 重要的 /var 子目录

| 子目录 | 描述 |
| :--- | :--- |
| /var/cache | 应用程序缓存数据的存储区域 |
| /var/lib | 包含与应用当前状态相关的信息 |
| /var/lock | 包含锁文件，以确保资源只被一个应用程序使用 |
| /var/log | 包含组织成子目录的日志文件。`syslogd` 服务器将其日志文件存储在 `/var/log` 中，文件的具体内容取决于 `syslogd` 配置文件 `/etc/syslog.conf`。例如，`/var/log/messages` 是主系统日志文件；`/var/log/secure` 包含来自安全服务（如 `sshd` 和 `xinetd`）的日志消息；`/var/log/maillog` 包含邮件消息的日志。 |
| /var/mail | 包含用户邮箱文件 |
| /var/opt | 包含存储在 `/opt` 目录中的包的变量数据 |
| /var/run | 包含自系统启动以来描述系统的数据 |
| /var/spool | 包含等待某种处理的数据 |
| /var/tmp | 包含在系统重启之间保留的临时文件 |
| /var/yp | 包含网络信息服务 (NIS) 数据库文件 |

**第二卷**
**第 3 章**
导航 Linux 文件系统





### 使用图形界面文件管理器

GNOME 和 KDE 桌面环境都配备了图形界面文件管理器，它们能让你轻松浏览文件系统并执行复制、移动文件等任务。GNOME 的文件管理器名为 Nautilus，而 KDE 的文件管理器则是 Konqueror。以下部分将简要介绍这些图形界面文件管理器。

#### 使用 Nautilus 外壳

Nautilus 文件管理器（更准确地说是一个图形外壳）随 GNOME 附带提供。Nautilus 易于使用；它类似于 Windows 活动桌面。你可以使用 Nautilus 管理文件和文件夹，还可以管理系统。

![](img/11709a8f88c8cd03868a929dc94c0e2b_211_0.png)

Nautilus 的最新版本与你可能在以前版本的 Red Hat Linux 或 Fedora Core 中了解到的不同。除了你过去熟悉的导航窗口外，Nautilus 现在还提供了一种新的对象窗口视图。当你双击桌面上的任何对象时，Nautilus 会打开一个显示该对象内容的对象窗口。如果你想要带有类似 Web 浏览器用户界面的旧式导航窗口，请右键单击文件夹，并从弹出菜单中选择“打开至：浏览文件夹”（Open→: Browse Folder）。

##### 在对象窗口中查看文件和文件夹

当你双击一个文件或文件夹时，Nautilus 会在其所谓的对象窗口中打开该对象。与过去的 Nautilus 窗口——那些允许你浏览目录层级的窗口——不同，对象窗口没有“后退”和“前进”按钮、工具栏或侧面板。例如，双击 GNOME 桌面左侧的“计算机”图标，Nautilus 会打开一个显示计算机中存储设备（包括文件系统）的对象窗口。然后，如果你在该窗口内双击某个对象，Nautilus 会打开另一个显示该对象内容的对象窗口。图 3-3 展示了在 Nautilus 中双击某些对象的结果。

Nautilus 对象窗口拥有一个极简的用户界面，仅包含菜单栏。你可以从菜单栏执行各种操作，例如使用应用程序打开对象、创建文件夹和文档，以及关闭对象窗口。

##### 从 Nautilus 烧录数据 CD

如果你的系统连接了 CD 刻录机（可以是内置的 ATAPI CD 刻录机，也可以是连接到 USB 端口的独立刻录机），你可以使用 Nautilus 烧录数据 CD。从 Nautilus 对象窗口，你可以访问内置于 Nautilus 中的 CD 创建器。只需遵循以下简单步骤：

- 1. 在任何 Nautilus 对象窗口中，选择 **位置::CD 创建器**。
  Nautilus 会打开一个 CD 创建器窗口。
  *注意：* 如果你没有打开任何 Nautilus 对象窗口，只需双击桌面上的“计算机”图标即可。

- 2. 从其他 Nautilus 窗口中，将你想放入 CD 的文件和文件夹拖放到 CD 创建器窗口中。
  若要获取计算机上的文件，请双击“计算机”图标在 Nautilus 中打开它，并找到你想要的文件。然后将这些文件或文件夹图标拖放到 CD 创建器窗口中。

- 3. 从 CD 创建器窗口中，选择 **文件::写入光盘**。
  Nautilus 会显示一个对话框，你可以在其中选择 CD 刻录机、写入速度以及其他几个选项，例如完成后是否弹出 CD。你还可以指定 CD 标题。

- 4. 点击 **写入** 按钮。
  Nautilus 将烧录 CD。

![](img/11709a8f88c8cd03868a929dc94c0e2b_212_0.png)

**图 3-3：** 默认情况下，Nautilus 为每个对象打开一个新的对象窗口。

##### 在导航窗口中浏览文件夹

如果你更喜欢使用熟悉的导航窗口来浏览文件夹，你需要做一些额外的操作。不要双击图标，而是右键单击图标，并从上下文菜单中选择“浏览文件夹”。Nautilus 随后会打开一个导航窗口，显示该图标所代表对象的内容。例如，右键单击 GNOME 桌面左上角的“主文件夹”图标，并从上下文菜单中选择“浏览文件夹”。Nautilus 会打开一个显示你的主目录内容的导航窗口。（请将目录想象成可以包含其他文件和文件夹的文件夹。）图 3-4 展示了 Nautilus 导航窗口的典型视图。

![](img/11709a8f88c8cd03868a929dc94c0e2b_213_0.png)

导航窗口在垂直方向上分为两部分。左侧面板显示你可以使用 Nautilus 浏览的文件系统的不同视图和其他对象。右侧面板显示左侧面板中当前选中文件夹里的文件和文件夹。Nautilus 为文件和文件夹显示图标。对于图像文件，它显示图像的缩略图。

导航窗口的用户界面类似于 Web 浏览器。窗口的标题栏显示当前选中文件夹的名称。窗口顶部的“位置”文本框显示该目录在 Linux 术语中的完整名称——例如，图 3-4 显示了 /home/naba/photos/April 8, 2005 - Cherry Blossoms 目录的内容。

如果你使用过 Windows 资源管理器，你可以以类似的方式使用 Nautilus 导航窗口。要查看其他目录的内容，请执行以下操作：

- 1. **从“信息”下拉菜单中选择“树”**（位于左侧窗口中）。
  该窗口中会出现一个目录树菜单。最初，树显示你的主文件夹以及作为 *FileSystem* 文件夹显示的文件系统 *根* 目录。

- 2. 点击 *FileSystem* 文件夹旁边的右向箭头；在生成的树状视图中，找到你想要浏览的目录。

- 3. 要查看 *X11* 子目录的内容，点击 X11。

例如，要查看 */etc* 目录，请点击 *etc* 目录旁边的右向箭头。Nautilus 会显示 */etc* 中的子目录，并将右向箭头变为向下箭头。*X11* 是你在下一步中将查看的 */etc* 中的子目录之一。

右侧的 *窗口* 现在显示 */etc/X11* 目录的内容。

Nautilus 通过使用不同类型的图标显示选中目录的内容。每个目录显示为一个文件夹，文件夹图标下方显示目录名称。普通文件，例如 *XP86Config-4*，显示为一张纸。*x* 文件是一个指向可执行文件的链接。

Nautilus 导航窗口具有常规的菜单栏和工具栏。注意图 3-4 中工具栏右侧的 *View as Icons* 按钮。该按钮表明 Nautilus 使用大图标显示目录内容。点击该按钮，会出现一个下拉列表。从列表中选择 *View as List*，Nautilus 将以列表格式使用较小的图标显示内容，并包含详细信息，例如每个文件或目录的大小以及上次修改时间，如图 3-5 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_214_0.png)

如果你点击列表视图顶部沿行的任何列标题——名称、大小、类型或修改日期——Nautilus 将根据该列对列表进行排序。例如，继续点击“修改日期”列标题。Nautilus 现在显示按最后修改时间排序的文件和目录列表。点击“名称”列标题会按字母顺序对文件和文件夹进行排序。

你不仅可以利用 Nautilus 导航窗口在不同的文件夹之间移动，还可以执行诸如将一个文件从一个文件夹移动到另一个文件夹或删除文件等操作。我不逐一列出每个步骤。这些步骤很直观，与你在任何图形界面（如 Windows 或 Mac）中的操作相似。以下是你可以在 Nautilus 中执行的一些操作：

- 要将文件移动到不同的文件夹，请将文件图标拖放到你希望放置文件的文件夹上。
- 要将文件复制到新位置，请选中文件图标，并从 Nautilus 菜单中选择“编辑：复制文件”。（或者，你可以右键单击文件图标，并从上下文菜单中选择“复制文件”。）然后移动到你想复制文件的文件夹，并选择“编辑：粘贴文件”。
- 要删除文件或目录，请右键单击图标，并从上下文菜单中选择“移至回收站”。（只有在你有权删除该文件时才能执行此操作。）要永久删除文件，请右键单击桌面上的回收站图标，并从上下文菜单中选择“清空回收站”。当然，只有在你确实想要删除文件时才这样做。一旦清空回收站，你就再也看不到该文件了。如果你必须从回收站中恢复文件，请双击回收站图标，然后将文件图标拖回到你想保存它的文件夹中。在你清空回收站之前，你可以随时从回收站中恢复文件。
- 要重命名文件或目录，请右键单击图标，并从上下文菜单中选择“重命名”。然后你可以在出现的文本框中输入新名称（或编辑名称）。
- 要创建新文件夹，请右键单击右侧窗口中的空白区域，并从上下文菜单中选择“创建文件夹”。新文件夹图标出现后，你可以右键单击图标，从上下文菜单中选择“重命名”来为其重命名。如果你没有权限创建文件夹，该菜单项将变灰。

#### 使用 Konqueror

Konqueror 是 KDE 自带的文件管理器和 Web 浏览器。它易于使用——有些类似于 Windows 活动桌面。你可以使用 Konqueror 管理文件和文件夹（还可以浏览网页）。




##### 查看文件和文件夹

当你在 KDE 桌面上单击一个文件夹图标时，Konqueror 会自动启动并打开该文件夹。例如，在 SUSE Linux 的 KDE 桌面上，单击左上角的“我的电脑”图标。Konqueror 会运行并显示你计算机的内容。单击 Konqueror 窗口左侧垂直工具栏上的“主文件夹”图标，然后单击中间窗格中的“主文件夹”。Konqueror 将在其主窗口中显示你的主目录内容（可以将目录理解为可以包含其他文件和文件夹的文件夹）。图 3-6 显示了 Konqueror 中一个典型用户的主目录。

![](img/11709a8f88c8cd03868a929dc94c0e2b_216_0.png)

如果你使用过 Windows 资源管理器，你可以以类似的方式使用 Konqueror。

Konqueror 窗口在垂直方向上分为三个部分：

- 一个较窄的左侧窗格，显示你可以单击以在 Konqueror 中执行各种任务的图标。
- 一个较宽的中间窗格（可以切换开启或关闭），显示当前文件夹的树状视图。
- 最宽的窗格（位于右侧），使用图标显示当前文件夹中的文件和文件夹。

Konqueror 为不同类型的文件使用不同类型的图标，并显示每个文件内容的预览。对于图像文件，预览是该图像的缩略图版本。

Konqueror 窗口的标题栏显示当前选中的目录名称。位置文本框（位于窗口顶部）显示该目录的完整名称——在此例中，图 3-6 显示了 `/home/naba` 目录的内容。

使用最左侧的垂直按钮列来选择要浏览的其他内容。当你单击其中一个按钮时，中间窗格会显示一个你可以浏览项目的树状菜单。例如，要浏览文件系统的其他部分，请执行以下操作：

1.  在 Konqueror 窗口最左侧的垂直图标列中（参见图 3-6），单击“根文件夹”图标（从下数第二个图标）。中间窗格会出现一个目录树状菜单。
2.  在树状视图中，找到你要浏览的文件夹。例如，要查看 `/etc` 文件夹，请单击 `/etc` 文件夹旁边的加号。Konqueror 会显示其他文件夹，并将加号变为减号。
3.  要查看 X11 子目录的内容，向下滚动并单击 X11。右侧窗格现在将显示 `/etc/X11` 目录的内容。

Konqueror 使用不同类型的图标来显示文件夹内容。每个目录都显示为一个文件夹，目录名称显示在文件夹图标下方。普通文件显示为一页纸。

Konqueror 窗口具有常见的菜单栏和工具栏。你还可以以其他格式查看文件和文件夹。例如，选择“查看→: 查看模式→: 详细列表视图”，以便以列表格式查看文件夹内容，并使用较小的图标（参见图 3-7），同时显示详细信息（例如每个文件或目录的大小，以及最后一次修改的时间）。

如果你单击列表视图顶部的任何列标题（例如“名称”、“大小”、“文件类型”或“修改时间”等），Konqueror 将按该列对列表进行排序。例如，如果你单击“修改时间”列标题，Konqueror 将显示按最后修改时间排序的文件和文件夹列表。单击“名称”列标题则按名称对文件和目录进行字母排序。

你不仅可以使用 Konqueror 在不同的文件夹之间移动，还可以执行诸如将一个文件从一个文件夹移动到另一个文件夹或删除文件等操作。我不详细列出每一步骤，因为步骤是直观的，且与你在任何 GUI（如 Windows 或 Mac 界面）中执行的操作类似。以下是你可以使用 Konqueror 执行的一些操作：

- **查看文本文件**：单击文件名，Konqueror 将运行 KWrite 文字处理程序，并在一个新窗口中显示该文件。
- **复制或移动文件到不同的文件夹**：将文件图标拖放至你希望文件所在的文件夹。会弹出一个菜单，询问你是要复制、移动，还是仅将文件链接到该目录。
- **删除文件或目录**：右击图标，并从上下文菜单中选择“移至回收站”。要永久删除文件，请右击桌面上的回收站图标，并从上下文菜单中选择“清空回收站”。当然，只有在你确实想要删除该文件时才这样做。当你清空回收站时，被删除的文件将永远消失。如果你想从回收站恢复文件，请双击桌面上的回收站图标，然后从该窗口将文件图标拖放至你希望保存文件的文件夹。当被询问是复制还是移动时，选择“移动”。在你清空回收站之前的任何时候，都可以从回收站恢复文件。
- **重命名文件或目录**：右击图标，并从上下文菜单中选择“重命名”。然后，你可以出现在文本框中输入新名称（或编辑旧名称）。
- **创建新文件夹**：选择“查看•查看模式•图标视图”。然后，右击最右侧窗格的空白区域，并从上下文菜单中选择“创建新•目录”。接着，输入新目录的名称并单击“确定”。（如果你没有权限创建目录，你会收到一条错误消息。）

![](img/11709a8f88c8cd03868a929dc94c0e2b_218_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_218_1.png)

## 194 使用 Linux 命令导航文件系统

##### 查看网页

Konqueror 不仅仅是一个文件管理器。使用它，你可以像查看文件夹一样轻松地查看网页。只需在位置文本框中输入一个 Web 地址，看看会发生什么。例如，图 3-8 显示了当我在工具栏上的位置文本框中输入 www.irs.gov 并按下回车键后的 Konqueror 窗口。

![](img/11709a8f88c8cd03868a929dc94c0e2b_219_0.png)

**图 3-8：** Konqueror 也可以浏览网络。

Konqueror 在右侧窗格中显示该 Web 站点。左侧窗格保持不变。

### 使用 Linux 命令导航文件系统

虽然 Nautilus（在 GNOME 中）或 Konqueror（在 KDE 中）等 GUI 文件管理器使用简单，但你只能在拥有可用的 GUI 桌面的情况下使用它们。有时，你可能没有图形环境来运行图形文件管理器。例如，你可能通过文本终端登录，或者你的系统上 X 没有正常工作。在这些情况下，你必须依赖 Linux 命令来操作文件和目录。当然，你始终可以使用 Linux 命令，即使在图形环境中也一样——你所要做的只是打开一个终端窗口并输入 Linux 命令。

在接下来的章节中，我将简要介绍一些用于在 Linux 文件系统中移动的命令。

#### 目录导航命令

在 Linux 中，当你以 *root* 身份登录时，你的主目录是 `/root`。对于其他用户，主目录通常位于 `/home` 目录中。我的主目录（当我以 *naba* 身份登录时）是 `/home/naba`。这些信息存储在 `/etc/passwd` 文件中。默认情况下，只有你有权在主目录中保存文件，并且只有你可以在主目录中创建子目录以进一步组织你的文件。

Linux 支持*当前*目录的概念，它是所有文件和目录命令操作的对象。例如，登录后，你的当前目录就是主目录。要查看当前目录，请输入 `pwd` 命令。

要更改当前目录，请使用 `cd` 命令。要将当前目录更改为 `/usr/lib`，请输入以下命令：

```
cd /usr/lib
```

然后，要将目录更改为 `/usr/lib` 中的 *cups* 子目录，请输入此命令：

```
cd cups
```

现在，如果你使用 `pwd` 命令，该命令将显示 `/usr/lib/cups` 为当前目录。

这两个例子表明，你可以用两种方式引用目录名称：

- 一个绝对路径名（如 `/usr/lib`），指定目录树中的确切目录
- 一个相对目录名（如 *cups*，代表当前目录的 *cups* 子目录，无论当前目录是什么）

如果你在 `/usr/lib` 中输入 `cd cups`，当前目录将更改为 `/usr/lib/cups`。然而，如果我在 `/home/naba` 中输入相同的命令，shell 会尝试将当前目录更改为 `/home/naba/cups`。

![](img/11709a8f88c8cd03868a929dc94c0e2b_220_0.png)

使用不带任何参数的 `cd` 命令可以将当前目录更改回你的主目录。无论你在哪里，在 shell 提示符下输入 `cd` 都会把你带回主目录！




![](img/11709a8f88c8cd03868a929dc94c0e2b_221_0.png)

顺便提一下，波浪号字符（~）指代您的主目录。因此，命令 `cd ~` 也会将当前目录更改为您的主目录。你还可以通过在波浪号后添加特定用户的姓名来引用该用户的主目录。因此，`cd ~superman` 会将当前目录更改为 superman 的主目录。

![](img/11709a8f88c8cd03868a929dc94c0e2b_221_1.png)

等等，还有更多内容。一个点（.）和两个点（..）——常被巧妙地称为 *dotdot*（点点）——也具有特殊含义。一个点（.）表示当前目录，而两个点（..）表示父目录。例如，如果当前目录是 `/usr/share`，你可以通过输入以下内容上升到上一层目录 `/usr`

```
cd ..
```

#### 目录列表和权限命令

你可以使用 `ls` 命令获取目录列表。默认情况下，不带任何选项的 `ls` 命令会以紧凑的多列格式显示当前目录的内容。例如，输入以下两个命令以查看 `/etc/X11` 目录的内容：

```
cd /etc/X11
ls
```

输出如下所示。（在控制台上，你会看到某些项目以不同颜色显示。）

```
X                    Xsession.d         cursors         rgb.txt        xkb
XF86Config-4         Xsession.options   default-display-manager  rstart       xserver
Xresources           Xwrapper.config    fonts            sysconfig      xsm
Xsession             app-defaults       gdm              xinit
```

从这个列表（没有颜色）中，你无法判断某个条目是文件还是目录。为了区分目录和文件，像这样使用带有 `-F` 选项的 `ls` 命令：

```
ls -F
```

这次，输出为你提供了关于文件类型的一些更多线索：

```
X@                   Xsession.d/        cursors/         rgb.txt        xkb/
XF86Config-4         Xsession.options   default-display-manager  rstart/      xserver/
Xresources/          Xwrapper.config    fonts/           sysconfig/     xsm/
Xsession*            app-defaults/      gdm@             xinit/
```

`ls -F` 的输出显示目录名称末尾附带了一个斜杠（/）。普通文件名原样显示。文件名末尾附加的 at 符号（@）（例如，注意名为 *X* 的文件）表示该文件是另一个文件的链接。（换句话说，这个文件名只是指向另一个文件的引用；它是一个快捷方式。）可执行文件末尾会附加一个星号（*）。（例如，*Xsession* 是一个可执行文件。）Shell 可以运行任何可执行文件。

你可以使用 `-l` 选项查看文件和目录的更详细信息：

```
ls -l
```

对于 `/etc/X11` 目录，`ls -l` 的典型输出如下所示：

```
total 84
lrwxrwxrwx  1 root root    20 Jul 15 20:32 X -> /usr/bin/X11/XFree86
-rw-r-r-r-  1 root root  2878 Jul 16 14:50 XF86Config-4
drwxr-xr-x  2 root root  4096 Jul 15 20:32 Xresources
-rw-r-xr-x  1 root root  3456 Jun  1 01:59 Xsession
drwxr-xr-x  2 root root  4096 Jul 15 20:34 Xsession.d
-rw-r-r-r-  1 root root   217 Jun  1 01:59 Xsession.options
-rw-------  1 root root   771 Jul 15 20:32 Xwrapper.config
drwxr-xr-x  2 root root  4096 Jul 15 20:35 app-defaults
... lines deleted ...
```

这个列表展示了每个目录条目的大量信息——其中每个条目可以是文件，也可以是另一个目录。从右列向左查看，你会看到最右侧的列显示目录条目的名称。名称之前的日期和时间显示该文件最后修改的时间。日期和时间的左侧是文件的大小（以字节为单位）。

文件的组（group）和所有者（owner）显示在文件大小说明的左侧。再往左的下一个数字表示指向该文件的链接数量。（*链接* 类似于 Windows 中的快捷方式。）最后，最左侧的列显示文件的权限设置，这些设置决定了谁可以读取、写入或执行该文件。

最左侧列的第一个字母具有特殊含义，如下列表所示：

- 如果第一个字母是 `l`，则该文件是指向另一个文件的*符号链接*（快捷方式）。
- 如果第一个字母是 `d`，则该文件是一个目录。
- 如果第一个字母是破折号（-），则该文件是普通文件。
- 如果第一个字母是 `b`，则该文件表示块设备，如磁盘驱动器。
- 如果第一个字母是 `c`，则该文件表示字符设备，如串行端口或终端。

![](img/11709a8f88c8cd03868a929dc94c0e2b_222_0.png)

在第一个字母之后，最左侧的列显示由九个字符组成的序列，当每个字母都存在时，它们显示为 `rwxrwxrwx`。每个字母表示一种特定的权限。用连字符（-）代替字母表示对文件特定操作没有权限。将这九个字母视为三组三个字母（`rwx`），解释如下：

- 最左侧的 `rwx` 组控制文件所有者的读取、写入和执行权限。换句话说，如果你在这个位置看到 `rwx`，文件的所有者可以读取（r）、写入（w）和执行（x）该文件。用连字符代替字母表示没有权限。因此，字符串 `rw-` 表示所有者具有读取和写入权限，但没有执行权限。虽然可执行程序（包括 shell 程序）通常具有执行权限，但目录将执行权限视为等同于*使用*权限：用户必须对目录具有执行权限，才能打开并读取目录的内容。
- 中间的三个 `rwx` 字母控制属于该文件组的其他任何用户的读取、写入和执行权限。
- 最右侧的 `rwx` 字母组控制所有其他用户（统称为*世界*）的读取、写入和执行权限。

因此，权限设置为 `rwx------` 的文件仅可被文件所有者访问，而权限设置为 `rwxr--r--` 的文件则可供世界读取。

`ls` 命令的一个有趣特性是，它不列出任何以句点开头的文件。要查看这些文件，你必须使用带有 `-a` 选项的 `ls` 命令，如下所示：

```
ls -a
```

在你的主目录中尝试此命令，然后将结果与不使用 `-a` 选项时看到的内容进行比较：

1.  **输入 `cd` 更改到主目录。**
2.  **输入 `ls -F` 查看主目录中的文件和目录。**
3.  **输入 `ls -aF` 查看*所有内容*，包括隐藏文件。**

![](img/11709a8f88c8cd03868a929dc94c0e2b_223_1.png)

大多数 Linux 命令接受单字符选项，每个选项前面都有一个减号（将此符号视为连字符）。当你要使用多个选项时，输入一个连字符，然后*连接*（串联）选项字母，依次排列。因此，`ls -al` 等同于 `ls -a -l` 以及 `ls -l -a`。

#### 更改权限和所有权的命令

你可能需要更改文件的权限设置以保护它免受他人影响。使用 `chmod` 命令更改文件或目录的权限设置。

要有效使用 `chmod`，你必须指定权限设置。一个好方法是按照表中所示的顺序（谁/操作/权限）连接表 3-4 中各列的字母。

注意：你只使用每列中的单个字符——括号中的文本仅用于解释。

| 谁 | 操作 | 权限 |
| :--- | :--- | :--- |
| u (用户) | + (添加) | r (读取) |
| g (组) | − (移除) | w (写入) |
| o (其他) | = (分配) | x (执行) |
| a (所有) | s (设置用户 ID) | |

例如，要允许所有人读取目录中的所有文件，请从第一列选择 `a`（所有），从第二列选择 `+`（添加），从第三列选择 `r`（读取），以得出权限设置 `a+r`。然后像这样使用 `chmod` 的整套选项：

```
chmod a+r *
```

另一方面，要允许所有人执行某个特定文件，请输入

```
chmod a+x filename
```

假设你有一个名为 `mystuff` 的文件，你想保护它。如果你按以下顺序输入命令，可以使其仅对你可访问：

```
chmod a-rwx mystuff
chmod u+rw mystuff
```

第一个命令关闭所有人的所有权限，第二个命令为所有者（你）开启读取和写入权限。输入 `ls -l` 以验证更改是否已发生。（你会看到权限设置为 `-rw-------`。）以下是 `ls -l` 的示例输出：

```
drwxr-xr-x   2  naba  naba  4096  2005-07-24  16:56  sdump
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_224_0.png)





*注：* 第三个和第四个字段显示为 `naba naba`。这两个字段表示文件的用户和组所有权。在这种情况下，用户名为 `naba`，组名也为 `naba`。在某些发行版中，组 ID 为 `users`。

有时你需要更改文件的用户或组所有权，以便一切正确运行。例如，假设你被指示（根据手册，还能指望什么？）创建一个名为 `cups` 的目录，并赋予其用户 ID `lp` 和组 ID `sys` 的所有权。你该如何操作？

你可以以 root 身份登录，并使用 `mkdir` 命令创建 `cups` 目录：

```text
mkdir cups
```

如果你使用 `ls -l` 命令检查文件详情，你会看到用户和组所有权是 `root root`。

要更改所有者，请使用 `chown` 命令。例如，要将 `cups` 目录的所有权更改为用户 ID `lp` 和组 ID `sys`，请输入：

```text
chown lp.sys cups
```

#### 用于文件操作的命令

要将文件从一个目录复制到另一个目录，请使用 `cp` 命令。例如，要将文件 `/usr/X11R6/lib/X11/xinit/Xclients` 复制到当前目录（如主目录）中的 `Xclients.sample` 文件，请输入以下内容：

```text
cp /usr/X11R6/lib/X11/xinit/xinitrc xinitrc.sample
```

如果你想将文件复制到当前目录但保留原始名称，请使用点号 (.) 作为 `cp` 命令的第二个参数。因此，以下命令将 `/etc/X11` 目录中的 `Xresources` 文件复制到当前目录（由单个点号表示）：

```text
cp /etc/X11/Xresources .
```

`cp` 命令创建文件的新副本，并保留原文件完好无损。

如果你想将整个目录的内容——包括所有子目录及其内容——复制到另一个目录，请使用命令 `cp -ar source_dir dest_dir`。（此命令将 `source_dir` 目录中的*所有内容*复制到 `dest_dir`。）例如，要将 `/etc/X11` 目录中的所有文件复制到当前目录，请输入以下命令：

```text
cp -ar /etc/X11 .
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_225_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_225_1.png)

### 使用 Linux 命令导航文件系统

![](img/11709a8f88c8cd03868a929dc94c0e2b_226_0.png)

要将文件移动到新位置，请使用 **mv** 命令。原始副本消失，新副本出现在目标位置。你可以使用 **mv** 重命名文件。如果你想将 *today.list* 的名称更改为 *old.list*，请使用 **mv** 命令，如下所示：

```text
mv today.list old.list
```

另一方面，如果你想将 *today.list* 文件移动到名为 *saved* 的子目录中，请使用此命令：

```text
mv today.list saved
```

**mv** 的一个有趣特性是，你可以用它将整个目录（包括其所有子目录和文件）移动到新位置。如果你有一个名为 *data* 的目录，其中包含许多文件和子目录，你可以使用以下命令将该整个目录结构移动到 *old_data*：

```text
mv data old_data
```

要删除文件，请使用 **rm** 命令。例如，要删除名为 *old.list* 的文件，请输入以下命令：

```text
rm old.list
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_226_1.png)

使用 **rm** 命令时要小心——尤其是当你以 **root** 身份登录时。你可能会无意中用 **rm** 删除重要文件。

#### 用于目录操作的命令

为了整理主目录中的文件，你必须创建新目录。使用 **mkdir** 命令创建目录。例如，要在当前目录中创建一个名为 *images* 的目录，请输入以下内容：

```text
mkdir images
```

创建目录后，你可以使用 **cd images** 命令切换到该目录。

你可以使用 **mkdir** 命令的 **-p** 选项创建整个目录树。例如，假设你的系统有一个 */usr/src* 目录，你想创建目录树 */usr/src/book/java/examples/applets*。要创建此目录层次结构，请输入以下命令：

```text
mkdir -p /usr/src/book/java/examples/applets
```

当不再需要某个目录时，使用 **rmdir** 命令将其删除。

![](img/11709a8f88c8cd03868a929dc94c0e2b_227_0.png)

只有当目录为空时，你才能删除该目录。

要删除一个空的目录树，你可以像这样使用 -p 选项：

```text
rmdir -p /usr/src/book/java/examples/applets
```

此命令删除 applets 的空父目录。当命令遇到非空目录时停止。

#### 用于查找文件的命令

find 命令对于定位满足搜索标准的文件（和目录）非常有用。

许多年前我开始使用 UNIX（20 世纪 80 年代早期的 Berkeley UNIX）时，find 命令让我感到困惑。在转向更复杂的格式之前，我坚持使用 find 的一种基本语法很长时间。我首先发现的基本语法是用于在文件系统的任何地方查找文件。它是这样运作的：假设你想查找任何名称以 gnome 开头的文件或目录。输入以下 find 命令来查找这些文件：

```text
find / -name "gnome*" -print
```

如果你没有以 root 身份登录，你可能会得到一堆错误消息。如果这些错误消息让你烦心，只需按以下方式修改命令，错误消息就成了历史。（或者，正如 UNIX 爱好者所说，“把它们发送到比特桶。”）

```text
find / -name "gnome*" -print 2> /dev/null
```

此命令告诉 find 从根目录 (/) 开始查找匹配 gnome* 的文件名，并显示任何匹配文件的完整路径名。最后一部分 (2> /dev/null) 只是将错误消息发送到等效于直接忽略它们的特殊文件。

你可以使用这种简单格式的 find 变体来定位任何目录（以及包含在该目录中的任何子目录）中的文件。如果你忘记在主目录中的哪个位置存储了所有名为 report*（以 report 开头的名称）的文件，你可以使用以下命令搜索这些文件：

```text
find ~ -name "report*" -print
```

当你习惯这种 find 语法后，你可以使用 find 的其他选项。例如，要查找特定类型的文件（如目录），请使用 type 选项。以下命令显示你的 Linux 系统中所有顶级目录名称：

```text
find / -type d -maxdepth 1 -print
```

在典型的 Linux 系统中，你通常不需要使用 find 的复杂格式；但如果你需要，可以使用以下命令查找其余的 find 选项：

```text
man find
```

查找所有匹配名称的文件的一个简单方法是使用 locate 命令，它搜索系统中定期更新的数据库中的文件。例如，这里是我在 Debian 系统上输入 locate Xresources 时得到的典型输出：

```text
/etc/X11/Xresources
/etc/X11/Xresources/xbase-clients
/etc/X11/Xresources/xfree86-common
```

SUSE Linux 默认不安装 locate 命令。要安装它，请选择 SUSE 桌面环境中的主菜单：YaST，以启动 YaST2 控制中心。单击窗口左侧的“软件”，然后单击窗口右侧的“安装/删除软件”。在 YaST 软件安装窗口中，搜索 locate。然后从搜索结果中选择该软件包，并单击“接受”以安装它。

#### 用于挂载和卸载的命令

假设你想在登录到文本控制台（没有 GUI 辅助）时访问本书配套 DVD-ROM 上的文件。为此，你必须首先将 DVD-ROM 驱动器的文件系统挂载到 Linux 文件系统中的特定目录。

首先查看 /etc/fstab 文件，以获取 CD-ROM 设备名称的线索。例如，一些 Linux 发行版使用设备名称 /dev/cdrom 来指代 CD/DVD-ROM 驱动器，而其他发行版可能使用诸如 /dev/hdc、/dev/cdroms/cdrom0 或 /dev/cdrecorder（用于 DVD/CD-R 驱动器）等设备名称。/etc/fstab 文件中的条目还告诉该发行版期望将 CD/DVD 挂载到的目录。一些发行版使用 /media/cdrom 作为挂载点，而其他发行版使用 /media/cdrom0 或 /media/cdrecorder。顺便说一下，使用 cdrom 一词来表示 CD-ROM 和 DVD-ROM 是惯例。





## 204 使用 Linux 命令导航文件系统

以 **root** 身份登录（或输入 `su -` 成为 **root**），将 DVD-ROM 插入 DVD 驱动器，然后输入以下命令：

```
mount /dev/hdc /media/cdrom0
```

此命令将名为 `/dev/hdc`（一个 IDE DVD/CD-ROM 驱动器）的设备上的文件系统挂载到 Linux 文件系统中的 `/media/cdrom0` 目录（也称为*挂载点*）。

在 `mount` 命令成功完成任务后，您可以通过将 `/media/cdrom0` 目录作为光盘的顶级目录来访问 DVD-ROM 上的文件。换句话说，要查看 DVD-ROM 的内容，请输入：

```
ls -P /media/cdrom0
```

当您使用完 DVD-ROM——并在从驱动器中弹出之前——您必须使用以下 `umount` 命令卸载光盘驱动器：

```
umount /dev/hdc
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_229_0.png)

您可以将设备挂载到文件系统上的任何空目录。但是，每个发行版都有用于挂载设备的惯例位置目录。例如，一些发行版使用 `/mnt` 中的目录，而另一些发行版使用 `/media` 目录作为挂载点。

#### 检查磁盘空间使用情况的命令

我想向你介绍两个命令——`df` 和 `du`——你可以使用它们来检查系统上的磁盘空间使用情况。这些命令使用起来很简单。`df` 命令显示所有已挂载设备的磁盘空间使用情况摘要。例如，当我在一台挂载了许多存储设备的 PC 上输入 `df` 时，以下是 `df` 命令的输出：

| 文件系统 | 1K-块 | 已用 | 可用 | 使用% | 挂载点 |
|---|---|---|---|---|---|
| /dev/hdb6 | 28243372 | 2377232 | 25872080 | 9% | / |
| tmpfs | 383968 | 12 | 383956 | 1% | /dev/shm |
| /dev/hda5 | 5766924 | 1422232 | 4051744 | 26% | /usr/boot |
| /dev/hda7 | 6258100 | 2989200 | 2951004 | 51% | /debian/boot |
| /dev/hda9 | 5766924 | 1422232 | 4051744 | 26% | /ubuntu |
| /dev/hda10 | 5766924 | 1872992 | 3600984 | 35% | /mepla |
| /dev/hda11 | 6258100 | 2989200 | 2951004 | 51% | /debian |
| /dev/hdb1 | 19585800 | 1370172 | 18188238 | 8% | /android |
| /dev/hdb2 | 16897676 | 10593364 | 5434312 | 66% | /windows/C |
| /dev/hdb1 | 107426620 | 9613028 | 97813592 | 9% | /windows/D |

输出是一个表格，列出了设备、存储总千字节数、已用多少、可用多少、使用百分比以及挂载点。

要以更易读的格式查看 `df` 的输出，请输入 `df -h`。以下是 `df -h` 命令的输出：

| 文件系统 | 大小 | 已用 | 可用 | 使用% | 挂载点 |
|---|---|---|---|---|---|
| /dev/hdb6 | 27G | 2.3G | 25G | 9% | / |
| /tmpfs | 375M | 12K | 375M | 1% | /dev/shm |
| /dev/hda5 | 5.5G | 1.4G | 3.9G | 26% | /ubuntu/boot |
| /dev/hda7 | 6.0G | 2.9G | 2.9G | 51% | /debian/boot |
| /dev/hda9 | 5.5G | 1.4G | 3.9G | 26% | /ubuntu |
| /dev/hda10 | 5.5G | 1.8G | 3.5G | 35% | /mepla |
| /dev/hda11 | 6.0G | 2.9G | 2.9G | 51% | /debian |
| /dev/hdb3 | 19G | 1.4G | 18G | 8% | /xandros |
| /dev/hda2 | 16G | 11G | 5.3G | 66% | /windows/C |
| /dev/hdb1 | 103G | 9.2G | 94G | 9% | /windows/D |

如果你将此输出与纯 `df` 的输出进行比较（参见前面的列表），你会发现 `df -h` 使用 M 表示兆字节、G 表示吉字节等术语打印大小。这些显然比 1K-块更容易理解。

另一个命令——`du`——对于查找目录占用的空间大小非常有用。例如，输入 `du /etc/X11` 以查看 `/etc/X11` 目录中所有目录的内容。（此目录包含 X 窗口系统配置文件。）最终结果如下：

```
12 /etc/X11/Xresources
36 /etc/X11/Xsession.d
272 /etc/X11/app-defaults
20 /etc/X11/cursors
12 /etc/X11/xinit
... 行已删除 ...
12 /etc/X11/fonts/misc
8 /etc/X11/fonts/100dpi
8 /etc/X11/fonts/75dpi
8 /etc/X11/fonts/Speedo
8 /etc/X11/fonts/Type1
48 /etc/X11/fonts
2896 /etc/X11
```

每个目录名前面都有一个数字——它告诉你该目录使用的磁盘空间千字节数。因此，整个 `/etc/X11` 目录使用了 2896KB（或约 2.9MB）的磁盘空间。如果你只想获取目录（包括该目录中包含的所有文件和子目录）使用的总磁盘空间，请使用 `-s` 选项，如下所示：

```
du -s /etc/X11
2896 /etc/X11
```

`-s` 选项使 `du` 仅打印整个目录的摘要信息。

![](img/11709a8f88c8cd03868a929dc94c0e2b_231_0.png)

正如 `df -h` 以兆字节和吉字节打印磁盘空间信息一样，你可以使用 `du -h` 命令以更易读的形式查看 `du` 的输出。例如，以下是我将它与 `-s` 选项结合使用以查看我在家中目录（`/home/naba`）中使用的空间的方法：

```
du -sh /home/naba
645M    /home/naba
```

## 第 4 章：介绍 Linux 应用程序

**本章内容**

- 盘点典型的 Linux 应用程序
- 试用办公应用
- 设置数据库
- 玩多媒体
- 处理图像

每个 Linux 发行版都附带大量应用程序。你只需要看看 GUI 桌面上的菜单，就知道我是什么意思了。通常，同类型的应用程序不止一个。大多数发行版都附带 OpenOffice.org 办公应用程序套件，包括文字处理器、电子表格、演示文稿软件等。你会发现许多 CD 播放器和多媒体播放器的选择，更不用说游戏、实用程序和有用的工具，例如扫描仪和数码相机应用程序。一些商业发行版附带商业办公套件，例如 Sun Microsystems 的 StarOffice。

![](img/11709a8f88c8cd03868a929dc94c0e2b_232_0.png)

说到播放*多媒体*（各种格式的音频和视频，如 MP3、MPEG、QuickTime），免费提供的 Linux 发行版通常不附带合适的解码器，因为某些解码器存在许可限制。最终结果是多媒体应用程序可以运行，但无法播放 MP3 文件或 DVD 电影，因为它缺少解码器。商业发行版，如 Xandros 和 SUSE，通常附带其中一些解码器。

我将为你概述一些这些 Linux 应用程序。阅读关于这些应用程序的信息后，你可以进一步探索它们并在需要时使用它们。

### 盘点 Linux 应用程序

表 4-1 展示了主要 Linux 应用程序的样本，按类别组织。对于主要应用程序，我还显示了一个相关网站，你可以从中获取该应用程序的更多信息。此列表远非全面。每个 Linux 发行版都比此表中显示的应用程序和实用程序拥有更多。

如果你的系统同时安装了 GNOME 和 KDE，那么这些应用程序中的大多数已经可以从任一 GUI 桌面获得。

在本章的后续部分，我将简要介绍表 4-1 中的一些应用程序，每个类别选择一两个。我在第四部分中描述互联网应用程序。

**表 4-1 Linux 应用程序样本**

| 应用程序 | 描述 |
|---|---|
| OpenOffice.org | 免费开源办公套件（与 Microsoft Office 兼容），包括 Writer 文字处理器、Calc 电子表格、Impress 演示应用程序、Draw 绘图程序和 Math 方程编辑器 (www.openoffice.org) |
| StarOffice | OpenOffice.org 衍生而来的商业办公套件 (www.sun.com/staroffice) |
| CrossOver Office | 允许你在 Linux 上安装和运行 Microsoft Office 软件的商业办公套件 (www.codeweavers.com/products/office) |
| AbiWord | 类似于 Microsoft Word 的免费文字处理程序 (www.abisource.com) |
| Dia | 绘图程序，设计类似于名为 Visio 的 Windows 应用程序 (www.gnome.org/projects/dia) |
| GNOME Calculator | GNOME 的简单计算器 |
| KCalc | KDE 的计算器 |
| KOrganizer | KDE 的日历和日程安排程序 (http://korganizer.kde.org) |
| Kontact | KDE 的个人信息管理套件 (www.kde.org/kde/products/konnectivity/kontact/) |
| Aspell | 文本模式拼写检查器 (http://aspell.sourceforge.net) |
| Dictionary | dict.org 字典服务器的图形客户端，你可以用它来查找单词 |
| emacs | 著名的文本编辑器，具有文本和图形界面 (www.gnu.org/software/emacs) |
| KWrite | KDE 的文本编辑器 |
| Kate | KDE 的高级文本编辑器 |
| vim | 具有文本模式界面且与著名的 UNIX 编辑器 vi 兼容的文本编辑器 (www.vim.org) |





## Linux 应用程序盘点

| 应用程序 | 描述 |
| :--- | :--- |
| **数据库** | |
| PostgreSQL | 一个高级对象关系型数据库管理系统 (www.postgresql.org)，支持结构化查询语言 (SQL) |
| MySQL | 一个流行的关系型数据库管理系统，支持 SQL (www.mysql.com) |
| **多媒体** | |
| GNOME CD Player | 音频 CD 播放器（需要可用的声卡） |
| KsCD | KDE 的音频 CD 播放器（需要可用的声卡） |
| Amarok | 一个多媒体音频播放器 (http://amarok.kde.org)，可以播放多种不同的声音格式，如果您安装了 MP3 解码器，还可以播放 MP3 文件 |
| Rhythmbox | 一个多媒体音频播放器 (http://rhythmbox.sourceforge.net)，可以播放多种不同的声音格式，如果您下载了用于此目的的插件，还可以播放 MP3 文件 |
| XMMS | X 多媒体系统：一个多媒体音频播放器 (www.xmms.org)，可以播放许多不同的声音格式，包括 MP3 文件。（对于某些发行版，您需要下载插件来播放 MP3。） |
| xine | 一个自由多媒体播放器 (http://xinehq.de)，可以播放 CD、DVD 和视频 CD (VCD)，并且如果拥有相应的解码器，还可以解码 AVI、MOV、WMV 和 MP3 等多媒体文件 |
| Kaffeine | 基于 xine 的 KDE 媒体播放器，因此 Kaffeine 的功能与 xine 相似 (http://kaffeine.sourceforge.net) |
| Totem | 基于 xine 的 GNOME 电影播放器，因此 Totem 的功能与 xine 相似 (www.gnome.org/projects/totem) |
| cdrao | 一个命令行应用程序，可以根据文本文件中对 CD 内容的描述，以光盘一次性 (DAO) 模式烧录音频或数据 CD-R (http://cdrao.sourceforge.net) |
| cdrecord | 一个命令行应用程序，可以烧录音频和数据 CD-R 以及 DVD-R (http://cdrecord.berlios.de/old/private/cdrecord.html) |
| growisofs | 一个命令行应用程序，使用 mkisofs 命令向用于 CD-R 和 DVD-R 的 ISO 9660 文件系统追加数据 (http://fy.chalmers.se/~appro/linux/DVD+RW) |
| X-CD-Roast | cdrecord 和 cdrao 的图形用户界面前端，使烧录数据和音频 CD-R 变得容易 (www.xcdroast.org) |
| K3b | 基于 KDE 的 cdrecord、cdrao 和 growisofs 的图形用户界面前端，用于烧录 CD-R 和 DVD-R (www.k3b.org) |
| digiKam | 一个数码相机和照片管理应用程序，支持 gPhoto 支持的所有数码相机 (www.digikam.org) |
| **图形与图像** | |
| The GIMP | GNU 图像操作程序：适用于照片修饰、图像合成和图像创作等任务的应用程序 (www.gimp.org) |
| GQview | 功能强大的图像查看器 (http://gqview.sourceforge.net) |
| KFax | KDE 传真查看器 |
| KView | KDE 简单图像查看器 |
| Ggv | GNOME Ghostview (GGv)，一个 PostScript 文档查看器 (www.gnu.org/directory/print/misc/ggv.html) |
| Xpdf | Adobe PDF 文档查看器 (www.foolabs.com/xpdf/) |
| Xsane | 用于通过 SANE（Scanner Access Now Easy）库访问扫描仪的图形前端 (www.xsane.org) |
| KSnapshot | 屏幕捕获程序 |
| Kooka | KDE 扫描仪程序，使用 SANE 库 (www.kde.org/apps/kooka) |
| xscanimage | 用于控制扫描仪的图形前端 |
| **互联网** | |
| Evolution | 个人信息管理应用程序，集成了电子邮件、日历、联系人管理和在线任务列表 (www.novell.com/products/evolution) |
| gFTP | 用于从互联网下载文件的图形 FTP 客户端 |
| Gaim | GNOME 即时消息客户端 (http://gaim.sourceforge.net) |
| Kopete | KDE 即时消息客户端 (http://kopete.kde.org) |
| Mozilla | 著名的开源 Web 浏览器，源自 Netscape 的源代码 (www.mozilla.org) |
| Firefox | 来自 Mozilla 项目的新改进型 Web 浏览器 (www.mozilla.org/products/Firefox) |
| Thunderbird | 来自 Mozilla 项目的电子邮件客户端 (www.mozilla.org/products/thunderbird) |
| Epiphany | 基于 Mozilla 的 GNOME 开源 Web 浏览器 (www.gnome.org/projects/epiphany) |
| Lynx | 文本模式 Web 浏览器 (http://lynx.browser.org) |
| KNode | KDE 的 GUI 新闻阅读器 (http://knode.sourceforge.net) |
| Pan | GNOME 的 GUI 新闻阅读器 (`http://pan.rebelbase.com`) |
| Akregator | KDE 的 RSS 信息源聚合器和阅读器 (`http://akregator.sourceforge.net`) |
| KPhone | 支持会话初始协议 (SIP) 的互联网电话应用程序 (`www.wirlab.net/kphone`) |
| Linphone | 支持会话初始协议 (SIP) 和实时传输协议 (RTP) 的互联网电话应用程序 (`www.linphone.org`) |
| Skype | 使用 IP 语音进行语音电话的互联网电话应用程序 (`www.skype.com`) |
| XChat | 互联网中继聊天 (IRC) 客户端 (`www.xchat.org`) |
| Konqueror | KDE 中的 Web 浏览器和文件管理器 (`www.konqueror.org`) |
| KMail | KDE 的电子邮件客户端 (`http://kmail.kde.org`) |

并非所有 Linux 发行版都包含表 4-1 中列出的所有应用程序，尽管您通常可以在任何发行版中下载并安装所有这些应用程序。表 4-2 列出了本书介绍的每个 Linux 发行版中主要应用程序的默认可用性——Debian GNU/Linux、Fedora Core、Knoppix、SUSE 和 Xandros。勾号表示该应用程序默认可用。

在安装 Linux 发行版时，通常必须选择特定的应用程序组进行安装。您的 Linux 系统上的确切应用程序列表取决于您在安装过程中所做的选择。

只要您拥有宽带（有线或 DSL）互联网连接，在 Debian（以及基于 Debian 的发行版，如 MEPIS 和 Ubuntu）中安装缺失的应用程序是非常容易的。例如，要查看 Debian 是否存在 K3b CD/DVD 烧录工具，我输入 `apt-cache search k3b`。我得到以下输出：

```
k3b - A sophisticated KDE cd burning application
k3b-i18n - Internationalized (i18n) files for k3b
k3blibs - The KDE cd burning application library - runtime files
k3blibs-dev - The KDE cd burning application library - development files
```

接下来，我输入 `apt-get install k3b`，片刻之后我的 Debian 系统上就安装了 K3b。这种安装（或升级）软件的简便性正是 Debian 用户推崇 `apt-get` 的原因（尽管它是一个命令行工具）。

### 表 4-2 某些应用程序的默认可用性

| 应用程序 | Debian | Fedora | Knoppix | MEPIS | SUSE | Ubuntu | Xandros |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 计算器 - GCalc 工具 | | | ✓ | ✓ | ✓ | | |
| 计算器 - KCalc | ✓ | ✓ | ✓ | ✓ | ✓ | | |
| CD/DVD 烧录 - K3b | ✓ | ✓ | ✓ | ✓ | | | |
| CD 播放器 - GNOME | ✓ | ✓ | ✓ | | | | |
| CD 播放器 - KsCD | ✓ | ✓ | ✓ | ✓ | ✓ | | |
| 数据库 - PostgreSQL | ✓ | | | | | | |
| 数据库 - MySQL | ✓ | ✓ | | | | | |
| 词典 - GNOME 词典 | ✓ | ✓ | ✓ | | | | |
| 词典 - Kdict | ✓ | ✓ | ✓ | | | | |
| 数码相机工具 - digiKam | ✓ | ✓ | ✓ | | | | |
| 绘图程序 - Dia | ✓ | ✓ | | | | | |
| 电子邮件 - KMail | ✓ | ✓ | ✓ | ✓ | ✓ | | |
| 电子邮件 - Evolution | ✓ | ✓ | ✓ | | | | |
| 电子邮件 - Thunderbird | ✓ | ✓ | | | | | |
| 文件管理器 - Konqueror | ✓ | ✓ | | | | | |
| 文件管理器 - Nautilus（集成 CD 写入器） | ✓ | ✓ | ✓ | ✓ | | | |
| 文件管理器 - Xandros 文件管理器（集成 CD 写入器） | | | | | | | ✓ |
| 图像处理 - ImageMagick | ✓ | ✓ | ✓ | ✓ | ✓ | | |
| 图像处理 - The GIMP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | |
| 即时消息 - Gaim | ✓ | ✓ | ✓ | ✓ | | | |
| 即时消息 - Kopete | ✓ | ✓ | | | | | |
| 互联网中继聊天 - XChat | ✓ | ✓ | ✓ | ✓ | ✓ | | |
| 互联网电话 - KPhone | ✓ | | | | | | |
| 互联网电话 - Linphone | ✓ | | | | | | |
| 互联网电话 - Skype | ✓ | ✓ | | | | | |
| 音乐播放器 - Amarok | ✓ | | | | | | |
| 音乐播放器 - RealPlayer | | | | ✓ | ✓ | | ✓ |
| 音乐播放器 - Rhythmbox | | ✓* | | | | ✓* | |
| 音乐播放器 - XMMS | ✓ | | ✓ | ✓ | | | ✓ |
| 新闻阅读器 - KNode | ✓ | | ✓ | ✓ | ✓ | | |
| 新闻阅读器 - Pan | | | | ✓ | | | |
| 办公套件 - Open Office.org | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PDF 查看器 - Acrobat Reader | | | ✓ | ✓ | | | ✓ |
| PDF 查看器 - Gpdf | ✓ | | | | | | |
| PDF 查看器 - Kpdf | ✓ | | | | | | |
| PDF 查看器 - Xpdf | | ✓ | | | ✓ | | |
| 个人组织者 - KOrganizer | ✓ | | | ✓ | ✓ | | ✓ |
| 个人组织者 - Kontact | ✓ | | | ✓ | ✓ | | ✓ |
| PostScript 查看器 - GNOME Ghostview (GGv) | ✓ | | | | ✓ | | |
| PostScript/PDF 查看器 - KGhostview | ✓ | | ✓ | | | | ✓ |
| RSS 信息源阅读器 - Akregator | | ✓ | ✓ | ✓ | | | |
| 扫描仪 - Kooka | ✓ | | ✓ | ✓ | | ✓ | ✓ |
| 扫描仪 - Xsane | | | ✓ | | | ✓ | |
| 扫描仪 - xscanimage | | ✓ | ✓ | | | | |
| 屏幕捕获 - KSnapshot | ✓ | | ✓ | ✓ | | ✓ | |
| 录音机 - GNOME 录音机 | ✓ | ✓ | | | | | |
| 录音机 - KDE 录音机 (KRecord) | | | | | | ✓ | ✓ |
| 拼写检查 - Aspell | | ✓ | | | ✓ | ✓ | |
| Web 浏览器 - Epiphany | ✓ | | | | | | |
| Web 浏览器 - Konqueror | | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Web 浏览器 - Lynx 文本模式浏览器 | | | ✓ | | | | |
| Web 浏览器 - Mozilla | ✓ | ✓ | ✓ | ✓ | | ✓ | ✓ |

![](img/11709a8f88c8cd03868a929dc94c0e2b_238_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_238_1.png)




#### 办公应用与工具

文字处理器、电子表格、演示文稿软件、日历、计算器——这些是办公室中一些常用的基础工具。大多数 Linux 发行版都预装了 OpenOffice.org（通常简称为 OO.o 或 Ooo）办公应用套件。你可以逐一尝试这些工具，看看哪一款更符合你的喜好。每个应用程序的使用都非常直观。即使用户界面的一些细节对你来说比较陌生，在使用几次后，你就会习惯了。本部分将简要介绍以下应用程序中的几个：

- **OpenOffice.org 办公套件：** 一个类似于 Microsoft Office 的办公套件，包含 Writer 文字处理器、Calc 电子表格程序、Impress 演示文稿程序、Draw 绘图和插图应用程序，以及 Math（一个数学公式编辑器）
- **Kontakt：** KDE 中的一个个人信息管理应用程序
- **计算器：** GNOME 计算器及 KDE 计算器
- **Aspell：** 拼写检查工具
- **更多：** 可供 Linux 系统商用的办公应用程序

##### OpenOffice.org 办公套件

OpenOffice.org 是由 OpenOffice.org 项目（www.openoffice.org）开发的办公套件。OpenOffice.org 类似于 Microsoft Office 等大型办公套件。其主要组件包括 Writer 文字处理器、Calc 电子表格和 Impress 演示文稿程序。

你可以轻松启动 OpenOffice.org——无论是整个套件还是其中的单个应用程序——在大多数图形桌面环境中，只需点击面板图标或从主菜单中选择即可。例如，在 SUSE 中，你可以点击桌面图标来打开 OpenOffice.org 套件的初始窗口。你可以在 OpenOffice.org 的主窗口中创建新的 OpenOffice 文档或打开现有文档（这些文档也可以是 Microsoft Office 文件）。

以下各部分将简要介绍 Writer、Calc 和 Impress。

###### Writer

在任意 OpenOffice.org 窗口中选择 文件 > 新建 > 文本文档，即可启动带有空白文档的 OpenOffice.org Writer 主窗口。使用 Writer 很简单——它类似于 Microsoft Word 等其他文字处理器。例如，你可以在空白文档中输入文本、格式化文本，并在完成后保存文本。

你也可以在 Windows 机器上用 Microsoft Word 准备好的文档中打开。图 4-1 显示了一个在 OpenOffice.org Writer 中打开的 Microsoft Word 文档。

![](img/11709a8f88c8cd03868a929dc94c0e2b_240_0.png)

当你保存文档时，默认情况下，Writer 会以 OpenDocument 文本格式保存为扩展名为 .odt 的文件。

OpenOffice.org 2.0 及更高版本使用标准的 OASIS Open Document XML 格式作为默认文件格式（文件扩展名为 .odt）。OASIS OpenDocument 格式不绑定任何供应商或特定的办公套件软件。有关 OpenDocument 格式的更多信息，请访问 http://www.oasis-open.org/committees/tc_home.php?wg_abbrev=office

![](img/11709a8f88c8cd03868a929dc94c0e2b_241_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_241_1.png)

如果需要与 Microsoft Word 共享 OpenOffice.org Writer 文档，可以将文档保存为多种格式，包括 Microsoft Word 6.0/95/97/2000/XP 和 富文本格式（.rtf）。Microsoft Word 可以打开 .rtf 文件。如果要与使用 OpenOffice.org 2.0 之前版本的用户交换文件，请将文件保存为带有 .ott 扩展名的 StarOffice 文本文档格式。

我不打算解释如何使用 Writer，因为它使用简单且直观。如有需要，可以使用在线帮助。从 Writer 菜单中选择 帮助 → 内容。这将打开 OpenOffice.org 帮助窗口，其中包含有关 Writer 的帮助信息。然后，你可以点击链接以查看特定的帮助信息。

###### Calc

Calc 是 OpenOffice.org 应用程序套件中的电子表格程序。要启动 Calc，请在主菜单的“Office”类别中选择 电子表格，或在任意 OpenOffice.org 窗口中选择 文件 → 新建 → 电子表格。Calc 会显示其主窗口，该窗口看起来类似于基于 Windows 的电子表格，例如 Microsoft Excel。（事实上，Calc 可以读取和写入 Microsoft Excel 格式的电子表格文件。）

使用 Calc 的方式与使用 Microsoft Excel 相同。你可以在单元格中输入条目、使用公式并对单元格进行格式化。（例如，你可以指定值的类型和小数点后的位数。）图 4-2 显示了 Calc 中的一个典型电子表格。

![](img/11709a8f88c8cd03868a929dc94c0e2b_241_2.png)

**图 4-2：** 使用 OpenOffice.org Calc 准备你的电子表格。

在制作电子表格时，请使用你在 Microsoft Excel 中常用的公式。例如，使用公式 SUM(D2:D6) 来汇总从单元格 D2 到 D6 的条目。要将单元格 D2 设置为条目 A2 和 C2 的乘积，请在单元格 D2 中输入 =A2*C2。要了解有关 OpenOffice.org Calc 中可用函数的更多信息，请从菜单中选择 帮助 → 内容。这将打开 OpenOffice.org 帮助窗口，你可以按类别浏览函数，并点击某个函数以阅读更多相关信息。

要保存电子表格，请选择 文件 → 另存为。会出现一个对话框，你可以从中指定文件格式、目录位置和文件名。OpenOffice.org Calc 可以将文件保存为多种格式，包括 Microsoft Excel 5.0/95/97/2000/XP，以及使用逗号分隔值（CSV）的文本文件。

![](img/11709a8f88c8cd03868a929dc94c0e2b_242_0.png)

如果你想与 Microsoft Excel 交换文件，请将电子表格保存为 Microsoft Excel 格式（选择合适的 Excel 版本）。然后你可以将该文件传输到 Windows 系统并在 Microsoft Excel 中打开它。

###### Impress

Impress 类似于 Microsoft PowerPoint。你可以使用 Impress 制作简报包（幻灯片演示）。要运行 Impress，请在主菜单的“Office”类别中选择 演示文稿，或在任意 OpenOffice.org 窗口中选择 文件 → 新建 → 演示文稿。

首次启动时，Impress 会提示你选择演示文稿样式和模板。若要开始工作，请选择 空白演示文稿 并点击 创建。若要打开现有文档，请从 演示文稿向导 中选择适当的选项并点击 打开。然后选择你要打开的演示文稿文件。你可以在 Impress 中打开 Microsoft PowerPoint 文件。

图 4-3 显示了 Impress 中的一个典型幻灯片演示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_243_0.png)

Impress 窗口显示第一张幻灯片，左侧显示幻灯片的概览视图。具体外观取决于你选择的文档类型和模板。你可以开始在幻灯片中添加文本和其他图形对象，如图像、文本和线条。

若要插入新幻灯片，请从菜单中选择 插入 → 幻灯片。会出现一张空白幻灯片。然后，你可以在该新幻灯片上添加文本和图形。

要保存演示文稿，请选择 文件 → 保存。对于新文档，你需要提供文件名并选择要保存文件的目录。

如果你想将幻灯片分享给使用 Microsoft PowerPoint 的人，请将演示文稿保存为 Microsoft PowerPoint 97/2000/XP 格式。

###### 日历

KDE 附带了 Kontact——一个应用程序，它将现有的 KDE 应用程序（如 Kmail 邮件阅读器和 KOrganizer 日历程序）集成在一个图形化的个人信息管理器中。你可以从面板图标或主菜单启动 Kontact。（菜单项的具体位置取决于 Linux 发行版。）

当 Kontact 启动时，它通常显示 Kmail 应用程序。不过，你可以通过点击 Kontact 窗口左侧面板上的图标切换到其他视图（见图 4-4）。例如，图 4-4 显示了你点击日历图标后的 Kontact 窗口。在这种情况下，Kontact 显示 KOrganizer（KDE 日历程序）的输出。KOrganizer 程序显示一个日历视图，你可以点击日期来设置或查看该天的日程安排。图 4-4 显示了一个典型的日历。





要为特定日期和时间添加事件或预约，请从日历中选择日期，双击时间，然后在出现的新建事件对话框中输入预约的简短描述。完成后单击“确定”。添加完事件和预约后，选择“文件”→“保存”以保存日历。

##### 计算器

你可以选择使用 GNOME 计算器或 KDE 计算器。两者都是科学计算器，你可以执行典型的科学计算，例如平方根和倒数，以及三角函数，例如正弦、余弦和正切。

要使用计算器，请在主菜单的“实用工具”或“附件”类别中查找它。图 4-5 展示了 SUSE 中的 KDE 计算器。

![](img/11709a8f88c8cd03868a929dc94c0e2b_244_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_244_1.png)

通过从“设置”菜单中选择选项，你可以显示额外的按钮。例如，选择“设置”→“三角函数按钮”以显示使你能够使用计算器执行三角函数计算的按钮。

#### Linux 上可商用的办公软件

由于办公软件对许多企业和个人都非常重要，我将简要提及一些在 Linux 上可用的商业办公软件。这些商业产品包括 Applixware Office 和 StarOffice。这些产品需要花费一些金钱，但成本通常低于微软 Office——微软 Office 是 Windows 上领先的办公应用软件套件。（如果你还不知道的话，微软 Office 是几个应用程序的集合：用于文字处理的 Microsoft Word，用于电子表格的 Microsoft Excel，用于演示文稿图形的 Microsoft PowerPoint，以及用于数据库的 Microsoft Access。）

针对 Linux 的另一个商业产品是来自 CodeWeavers 的 CrossOver Office。使用 CrossOver Office，你可以在 Linux 和 X Window System 下运行你现有的 Microsoft Office 应用程序（例如 Word、Excel 和 PowerPoint）。

![](img/11709a8f88c8cd03868a929dc94c0e2b_245_0.png)

本书附带的光盘不包含任何针对 Linux 的这些商业办公软件，但我在接下来的几节中简要描述了它们。你可以访问每家供应商的网站以获取有关这些产品的更多信息。

##### Applixware Office

www.vistasource.com

Applixware 是一套适用于所有 Linux 发行版的办公应用软件套件。2000 年 4 月，Applx, Inc. 成立了一个独立的团队——VistaSource, Inc.——该团队专门专注于 Linux 应用程序。Applxware 是一组集成的模块，包括一个文字处理器、一个能够操作实时数据的电子表格、一个可编程的矢量图形工具以及用于访问数据库的数据库接口。Applxware 模块可以读取和写入 Microsoft Office 格式文档，以及几种其他文件格式。

##### StarOffice

www.sun.com/staroffice

StarOffice 是另一套商业办公应用软件套件；它由德国汉堡的 StarDivision 创建，并于 1999 年被 Sun Microsystems 收购。StarOffice 是一个跨平台解决方案——它运行在 Linux、Windows 95/98/Me/NT/2000/XP、Sun Solaris x86 和 Sun Solaris x86 上。此外，StarOffice 提供多种语言版本：英语、法语、德语、西班牙语、意大利语和瑞典语。

#### 办公应用与工具

以下是 StarOffice 7 包含的内容：

- StarOffice Writer 用于文字处理（兼容 Microsoft Word）
- StarOffice Calc 用于电子表格（兼容 Microsoft Excel）
- StarOffice Impress 用于演示文稿（兼容 Microsoft PowerPoint）
- StarOffice Draw 用于矢量图形绘制
- StarOffice Base 用于数据管理

2000 年 10 月，Sun 在开源许可证下发布了 StarOffice 的源代码。OpenOffice.org，一个 Sun 支持的开源项目，于 2002 年 5 月发布了 OpenOffice.org 1.0 办公生产力套件。当前的 Linux 发行版附带 OpenOffice.org 2.0 或更高版本。欲了解有关 OpenOffice.org 的更多信息，请访问 www.openoffice.org。

Xandros 的商业版本附带 StarOffice 7。寻找桌面上可以点击以启动 StarOffice 的图标。Xandros 还包含 OpenOffice.org。

##### CrossOver Office

www.codeweavers.com/products/cxoffice

你很可能已经在你的 PC 上安装了 Windows 和 Microsoft Office。当你决定在 PC 上运行 Linux 时，你可以继续从 GNOME 或 KDE 桌面运行大多数 Microsoft Office 应用程序。在 Linux 中运行 Microsoft Office 的便利性来自于一个名为 CrossOver Office 的商业产品。

来自 CodeWeavers 的 CrossOver Office 是一个软件包，它使你可以将 Microsoft Office 应用程序（所有版本的 Office，包括 Office 97、Office 2000 和 Office XP）安装在 Linux 中。你不需要 Microsoft Windows 即可在 CrossOver Office 中运行 Office 应用程序。你只需安装 CrossOver Office，然后从 CD-ROM 安装 Microsoft Office（以及许多其他 Windows 应用程序，如 Adobe Photoshop 和 Quicken）。安装 Microsoft Office 后，Office 应用程序可以直接从 GNOME 或 KDE 桌面访问。

CrossOver Office 使用 Wine——这是一个基于 X Window System 实现的 Windows Win32 和 Win16 应用程序编程接口（APIs）的开源实现，旨在 UNIX 和 Linux 系统中运行。Wine 包含 Wine 加载器和 WineLib。Wine 加载器可以加载和运行 Windows 应用程序。WineLib 用于在 Linux 中编译和链接 Windows 应用程序。你可以从 www.winehq.com 免费获得 Wine。

![](img/11709a8f88c8cd03868a929dc94c0e2b_246_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_246_1.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_247_0.png)

CodeWeavers 通过使用定制版本的 Wine 创建了 CrossOver Office，以确保 Microsoft Office 应用程序（特别是 Microsoft Word、Excel 和 PowerPoint）在 Wine 上正常运行。CodeWeavers 对 CrossOver Office 收取名义上的费用——CrossOver Office 标准版的价格为 39.95 美元，CrossOver Office 专业版的价格为 74.95 美元。然而，对 Wine 的所有代码更改和改进都会返还给 Wine 项目。因此，Wine 开源项目从 CrossOver Office 的销售中受益。

Xandros 的商业版本附带 CrossOver Office。在你开始使用 Microsoft Office 应用程序之前，你必须运行 CrossOver Office 设置，然后从原始 CD 安装 Microsoft Office。在安装过程中，你必须输入 Microsoft Office 的产品密钥，就像在 Windows 安装中一样。

#### Aspell 拼写检查器

Aspell 实用工具是一个交互式拼写检查器。你可以使用它来检查文本文件中单词的拼写。为此，只需在终端窗口中输入以下命令：

```
aspell check filename
```

如果你想试用 Aspell，请输入一些笔记并将其保存为名为 notes.txt 的文本文件。（文件名可以是任何东西，但我在本节中使用此文件名。）要对该文件运行拼写检查器，请在终端窗口中输入以下命令：

```
aspell check notes.txt
```

以下是 Aspell 显示的内容：

```
This note describes the *concensus* reached during the August 16 meeting.

1) concensus 6) consensual
2) con census 7) conciences
3) con-census 8) incenses
4) condenses 9) consensues’s
5) concerns 0) consensuses
i) Ignore all I) Ignore all
r) Replace X) Replace all
a) Add x) Exit
?
```

当 Aspell 发现拼写错误的单词（任何不出现在其词典中的单词）时，它会显示包含拼写错误单词（concensus）的句子，并通过在该单词周围加上一对星号来突出显示该单词。在该句子下方，Aspell 列出了可能的更正，并从 1 开始依次编号。在这种情况下，Aspell 将 consenus——正确的选择——列为 concensus 的第一个更正项。

在句子之后，Aspell 显示一个包含 16 个选项的列表——其中十个编号为 0 到 9，六个以单个字母 i, x, a, I, R 和 X 标记——后跟一个问号提示。你必须按下输出中显示的列表中的数字或字母之一，以指示你希望 Aspell 执行的操作。带编号的选项显示了拼写错误单词的十种可能替换词。以下是字母选项的含义：

- 空格表示这次接受该单词。
- i 表示忽略该拼写错误单词。
- I 表示忽略该单词的所有出现。
- x 表示替换此次出现。（按下 x 后，你必须输入一个替换词。）
- R 表示替换所有出现。（按下 R 后，你必须输入一个替换词。）
- a 表示接受该单词并将其添加到你的私人词典中。
- X 表示保存文件的其余部分并退出，忽略拼写错误。

![](img/11709a8f88c8cd03868a929dc94c0e2b_248_0.png)

> 这些选项区分大小写。请确保未开启大写锁定。

### 数据库

Linux 发行版通常附带两种常见关系型数据库之一——PostgreSQL 和 MySQL。

PostgreSQL（发音为 POST-gres cue-ee）是一个强大且流行的关系型数据库（这种类型的数据库作为连接表的集合工作）。你可以使用结构化查询语言（SQL）来处理数据库。PostgreSQL 由一个开发者团队开发，并在 BSD（伯克利软件发行版）开源许可下分发。该许可对 PostgreSQL 源代码的使用方式没有限制。要跟踪 PostgreSQL 的最新发展，请访问 www.postgresql.org。

MySQL（发音为 My-ESS-cue-ee）是另一个流行的关系型数据库。你可以使用 SQL 来处理 MySQL 数据库。一家名为 MySQL AB 的瑞典公司开发 MySQL（www.mysql.com）。





![](img/11709a8f88c8cd03868a929dc94c0e2b_249_0.png)

我简要向您展示如何在 Fedora 上使用 MySQL。顺便提一下，如果您在 Debian 中看不到 MySQL，请以 `root` 身份登录，并在终端窗口中输入 `apt-get install mysql-admin mysql-client mysql-common mysql-server`。

要使用 MySQL，您首先必须以 `root` 身份登录，并使用以下命令启动数据库服务器：

```
/etc/init.d/mysqld start
```

数据库服务器 `mysqld` 是一个守护进程（持续运行的后台进程），它接受来自 MySQL 监控器的数据库查询。

现在，您需要设计一个数据库，在 MySQL 中创建该数据库，并向其中加载数据。

##### 回顾构建数据库的步骤

使用以下基本步骤序列来构建数据库：

- 1. **设计数据库。**
  这包括定义用于存储信息的表和属性。
- 2. **创建一个空数据库。**
  在添加表之前，数据库系统要求您先构建一个空数据库。
- 3. **在数据库中创建表。**
  在此步骤中，您使用 SQL 的 `CREATE TABLE` 语句定义表。
- 4. **向表中加载任何固定数据。**
  例如，如果您有一个制造商名称或出版商名称（在书籍情况下）的表，您希望向该表中加载已知信息。
- 5. **备份初始数据库。**
  如果有必要，此步骤确保您可以从头开始创建数据库。
- 6. **向表中加载数据。**
  您可以从之前数据库的转储文件中加载数据，或者通过表单交互式加载。
- 7. **通过查询数据库来使用它。**
  使用 SQL 命令进行查询、更新记录或插入新记录。

为了说明如何创建和加载数据库，我设置了一个简单的图书目录数据库作为示例。

###### 设计数据库

在我的图书目录示例中，我没有遵循数据库构建的所有步骤。对于示例而言，数据库设计步骤将非常简单，因为我的图书目录数据库将只包含一个表。该表的属性如下：

- 书名，最多 50 个字符
- 第一作者姓名，最多 20 个字符
- 第二作者姓名（如有），最多 20 个字符
- 出版商名称，最多 30 个字符
- 页数，作为数字
- 出版年份，作为数字（例如 2005）
- 国际标准书号（ISBN），作为 10 个字符的文本（例如 0471752622）

我存储的 ISBN 不包含典型 ISBN 中嵌入的破折号。我还使用 ISBN 作为表的主键，因为 ISBN 是书籍的全球识别系统。这意味着每个图书条目必须有一个唯一的 ISBN，因为所有书籍都有唯一的 ISBN。

###### 创建空数据库

要在 MySQL 中创建空数据库，请使用 `mysqladmin` 程序。例如，要创建一个名为 books 的空数据库，我输入以下命令：

```
mysqladmin create books
```

您必须以 root 身份登录才能运行 `mysqladmin` 程序。顾名思义，`mysqladmin` 是 MySQL 的数据库管理程序。

除了创建数据库，您还可以使用 `mysqladmin` 来删除数据库、关闭数据库服务器或检查 MySQL 版本。例如，要查看版本信息，请输入以下命令：

```
mysqladmin version
```

使用 *MySQL* 监控器

创建空数据库后，您与数据库的所有交互都是通过 `mysql` 程序进行的——*MySQL* 监控器充当数据库服务器的客户端。您需要运行 `mysql` 并将数据库名称作为参数。然后 `mysql` 程序会提示您输入。这是我要输入的启动 `mysql` 程序并打开 *books* 数据库的命令：

```
mysql books
```

在显示其版本号和状态信息后，`mysql` 程序提示您输入，如下所示：

```
mysql>
```

然后您可以该提示符下输入 `mysql` 命令。在创建表或向表中加载数据时，一种典型的方法是将 SQL 语句（以及 `mysql` 命令，例如 `\G`）放在一个文件中，然后运行 `mysql`，并将标准输入重定向到该文件。例如，假设有一个名为 `sample.sql` 的文件，其中包含一些您想在一个名为 *books* 的数据库上尝试的 SQL 命令。那么，您应该使用以下命令运行 `mysql`：

```
mysql books < sample.sql
```

我以这种方式使用 `mysql` 来创建数据库表。

###### 定义表

要创建一个名为 *books* 的表，我编辑了一个名为 `makedb.sql` 的文本文件，并在该文件中放置了以下行：

```
#
####### Table structure for table 'books'
#
CREATE TABLE books (
    isbn CHAR(10) NOT NULL PRIMARY KEY,
    title CHAR(50),
    author1 CHAR(20),
    author2 CHAR(20),
    pubname CHAR(30),
    pubyear INT,
    pagecount INT
) \G
```

CREATE TABLE *books* 是一个用于创建名为 *books* 的表的 SQL 语句。语句末尾的 `\G` 是一个 `mysql` 命令。表的属性显示在括号包含的行中。

如果表包含固定数据，您还可以包含其他 SQL 语句（例如 `INSERT INTO`），以便在创建表后立即向表中加载数据。

要执行 `makedb.sql` 文件中的 SQL 语句以创建 `books` 表，我按以下方式运行 `mysql`：

```
mysql books < makedb.sql
```

现在 `books` 数据库有一个名为 `books` 的表。（好吧，也许我应该给它们起不同的名字，但用相同的名字似乎更方便）。现在我可以开始向表中加载数据了。

###### 向表中加载数据

向表中加载数据的一种方式是准备另一个文件中的 SQL 语句，并使用该文件作为输入运行 `mysql`。例如，假设我想将以下书籍信息添加到 `books` 表中：

```sql
isbn = '0764596152'
title = 'SUSE Linux 9.3 For Dummies'
author1 = 'Naba Barkakati'
author2 = NULL
pubname = 'Wiley'
pubyear = 2005
pagecount = 384
```

然后，以下 MySQL 语句将此信息加载到 `books` 表中：

```sql
INSERT INTO books VALUES
('0764596152', 'SUSE Linux 9.3 For Dummies',
'Naba Barkakati', NULL, 'Wiley', 2005, 384)\G
```

另一方面，假设您拥有以不同顺序排列的各种字段——一个与您使用 `CREATE TABLE` 语句定义的顺序不同的顺序。在这种情况下，您可以使用不同形式的 `INSERT INTO` 命令来按正确顺序添加该行，如下例所示：

```sql
INSERT INTO books (pubyear, author1, author2, title,
pagecount, pubname, isbn) values
(2005, 'Naba Barkakati', NULL, 'SUSE Linux 9.3 For
Dummies', 384, 'Wiley', '0764596152')\G
```

基本上，您需要指定属性列表以及值，并确保属性的顺序与值的顺序匹配。

如果我将所有 *INSERT INTO* 命令保存在一个名为 *additems.sql* 的文件中，我可以使用 *source* 命令从 *mysql* 命令行加载数据库，如下所示。（*输入* **mysql** *books 以启动 SQL 客户端。*）

```
mysql> source additems.sql
```

##### 查询数据库

您可以通过 *mysql* 监控器交互式地查询数据库。您确实需要了解 SQL 才能做到这一点。例如，要查询 *books* 数据库，我使用以下命令启动 SQL 客户端：

```
mysql books
```

然后在 *mysql>* 提示符下输入 SQL 命令从数据库中查找项目。完成后，我输入 *quit* 退出 *mysql* 程序。这是一个例子。（*我在终端窗口中键入了所有内容。*）

```
mysql> select title from books where pubyear < 2006 \g

| title |
|SUSE Linux 9.3 For Dummies |
|Linux All-in-One Desk Reference For Dummies |

2 rows in set (0.06 sec)

mysql> quit
Bye
```

#### 多媒体应用程序

大多数 Linux 发行版都包含相当多的多媒体应用程序——主要是多媒体音频播放器和 CD 播放器，但也有用于使用数码相机和烧录 CD-ROM 的应用程序。要播放其他一些多媒体文件（如 MPEG 视频），您可能需要在 Linux 系统上下载并安装额外的软件。以下是几个典型多媒体任务及可用于执行这些任务的应用程序的简要说明：

- **使用数码相机**：使用数码相机工具在 Linux 中从数码相机下载照片（或者简单地将相机作为 USB 大容量存储设备访问）。
- **播放音频 CD**：使用 Linux 自带的众多音频 CD 播放器之一。




##### 播放音频文件
- **播放音频文件：** 使用 Rhythmbox 或 XMMS 多媒体音频播放器。（你需要下载一些额外的软件才能用 Rhythmbox 或 XMMS 播放 MP3 文件。）你也可以从互联网下载其他播放器。
- **刻录光盘：** 使用光驱刻录机，例如 K3b，来刻录音频和数据光盘。

##### 使用数码相机

大多数 Linux 发行版都附带一个数码相机应用程序，你可以用它来从数码相机下载照片。例如，MEPIS、SUSE 和 Xandros 都附带 digiKam，它能与许多不同品牌和型号的数码相机配合使用。根据型号的不同，相机可以连接到串行端口或通用串行总线 (USB) 端口。

要将 digiKam 与你的数码相机配合使用，请按照以下步骤操作：

1. **将你的数码相机连接到串行端口或 USB 端口（取决于相机支持的接口），并打开相机。**
    在主菜单的图形或图像部分找到它。
2. **启动 digiKam。**
3. **从 digiKam 菜单中选择 设置→配置 digiKam。**
    会出现一个配置对话框。
4. **在对话框中点击 相机 选项卡，然后点击 自动检测。**
    如果你的相机受支持且配置为 PTP（图片传输协议）模式，相机将被检测到。如果没有，你可以使用我在这些步骤之后描述的替代方法从相机中获取照片。
5. **从 相机 菜单中选择你的相机型号。**
    会出现一个新窗口，片刻之后，将显示相机中的照片。
6. **点击缩略图以选择要下载的图片；然后选择 相机→下载 以下载图片。**

digiKam 随后将下载这些图片。你可以将文件保存在文件夹中，并使用 The GIMP 或你喜欢的照片编辑器编辑这些照片。

![](img/11709a8f88c8cd03868a929dc94c0e2b_254_0.png)

如果 digiKam 无法识别你的数码相机，请不要灰心。只要你的相机支持 USB 大容量存储，你就可以将数码相机的存储介质（例如紧凑闪存卡）作为 USB 大容量存储设备来访问。要访问 USB 数码相机上的图像，请使用以下步骤。（我在 SUSE Linux 上测试了这些步骤，但它们应该在大多数 Linux 发行版上都能正常工作。）

1. 阅读相机手册并使用相机的菜单选项将 USB 模式设置为大容量存储。
    如果相机不支持 USB 大容量存储，则无法使用此过程访问照片。如果相机支持图片传输协议 (PTP) 模式，你可以使用 digiKam 来下载图片。
2. 使用随相机附带的线缆将数码相机连接到 USB 端口，然后打开相机。
    这将使 Linux 检测到相机，并在文件管理器窗口中打开相机的内容（见图 4-6）。

![](img/11709a8f88c8cd03868a929dc94c0e2b_255_0.png)

3. 点击选择照片，并通过将它们拖放到选定的文件夹中复制到你的硬盘。
4. 关闭文件管理器窗口，从 PC 上断开 USB 线缆，并关闭相机。

当你可以将相机像其他任何存储设备一样访问时，谁还需要数码相机工具呢！

##### 播放音频 CD

所有 Linux 发行版都附带 GNOME 或 KDE 的 CD 播放器应用程序。要播放音频 CD，你需要一张声卡，并且该声卡必须已配置为在 Linux 下工作。

在某些发行版中，将音频 CD 插入驱动器后，会出现一个对话框，询问你是否要播放 CD。例如，图 4-7 展示了在 SUSE Linux 中 KDE CD 播放器 (KsCD) 播放音频 CD 中的音轨。

![](img/11709a8f88c8cd03868a929dc94c0e2b_256_0.png)

KDE CD 播放器显示 CD 的标题和当前音轨的名称。CD 播放器从 http://freedb.org 获取歌曲标题——这是互联网上的一个免费、开源 CD 数据库（freedb.freedb.org，端口 888）。CD 播放器需要从 CD 数据库下载歌曲信息，因此你需要一个活跃的互联网连接。在 CD 播放器下载关于特定 CD 的信息后，它会将该信息缓存在本地数据库中供以后使用。CD 播放器的用户界面直观易懂，你可以轻松掌握。一个不错的功能是你可以通过标题选择音轨。

##### 播放音频文件

你可以使用 Rhythmbox 或 XMMS 打开并播放音频文件（例如 MP3 文件）。拥有大型 MP3 音乐库的用户喜欢 Rhythmbox，因为它可以帮助整理音乐文件。在包括 Debian 和 Fedora Core 在内的多个发行版中，你可以从主菜单中选择音乐播放器应用程序来启动 Rhythmbox。当你首次启动 Rhythmbox 时，它会显示一个向导，提示你（见图 4-8）音乐文件的位置，以便 Rhythmbox 可以管理你的音乐库。

![](img/11709a8f88c8cd03868a929dc94c0e2b_256_1.png)

确定音乐文件位置后，Rhythmbox 启动并以有组织的方式显示库。然后你可以选择音乐并播放，如图 4-9 所示。（这里看到的是在 Debian 上运行的 Rhythmbox。）

# 232 多媒体应用程序

![](img/11709a8f88c8cd03868a929dc94c0e2b_257_0.png)

**图 4-9**：你可以在 Rhythmbox 中播放库中的音乐。

XMMS 是另一种可以播放多种类型音频文件的音乐播放器，包括 Ogg Vorbis、FLAC（自由无损音频编解码器，一种类似于 MP3 的音频文件格式）和 Windows WAV。

你可以从主菜单中选择音频播放器应用程序（在多媒体或声音与视频下查看）来启动 XMMS。XMMS 启动后，你可以选择 窗口菜单->播放文件 或按下 L 键来打开音频文件（例如 MP3 文件）。然后在 加载文件 对话框中选择一个或多个音乐文件。点击 播放 按钮，XMMS 开始播放音频文件。图 4-10 展示了在 SUSE Linux 中播放音频文件时的 XMMS 窗口。

![](img/11709a8f88c8cd03868a929dc94c0e2b_257_1.png)

**图 4-10**：你可以在 XMMS 中播放许多不同类型的音频文件。

##### 刻录光盘

如今，图形用户界面 (GUI) 文件管理器通常具有刻录光盘的功能。例如，Nautilus 和 Xandros 文件管理器内置了刻录光盘的功能。Linux 发行版还附带独立的 GUI 程序，使你能够轻松地刻录 CD 和 DVD。例如，K3b 是 KDE 中一个流行的 CD/DVD 刻录应用程序，可在 Knoppix 和 SUSE 中获取。

大多数光盘刻录应用程序使用简单。你基本上只需收集要刻录到 CD 或 DVD 上的文件，然后开始刻录过程。当然，为了让这行得通，你的 PC 必须安装了 CD 或 DVD 刻录机。

图 4-11 展示了 SUSE Linux 中 K3b CD/DVD 刻录应用程序的初始窗口。K3b 窗口的上半部分用于浏览文件系统，以选择要刻录到 CD 或 DVD 上的内容。左上角显示了安装的光驱设备；在这个例子中，它是一台 DVD/CD-RW 驱动器，因此该驱动器可以读取 DVD 和 CD，但只能刻录 CD。

![](img/11709a8f88c8cd03868a929dc94c0e2b_258_0.png)

**图 4-11：** 你可以使用 K3b 应用程序刻录 CD 和 DVD。

要刻录 CD，你从 K3b 窗口下半部分显示的某个项目开始——例如“新建音频 CD 项目”或“新建数据 DVD 项目”。然后你必须添加文件，最后通过选择 项目->刻录 或按 Ctrl-B 将项目刻录到 CD 或 DVD 上。对于音频 CD，你可以拖放 MP3 文件以及音轨。

![](img/11709a8f88c8cd03868a929dc94c0e2b_259_0.png)

K3b 需要外部命令行程序 cdrecord 和 cdrdao 来刻录 CD。K3b 还需要 growisofs 程序来刻录 DVD。

![](img/11709a8f88c8cd03868a929dc94c0e2b_259_1.png)

如果你在 Debian 中遇到关于缺失 cdrdao 的错误，请确保你的 Debian 系统已连接到互联网，然后输入 `apt-get install cdrdao` 进行安装。

#### 图形与成像

你可以使用图形和成像应用程序来处理图像和图形（线条画和形状）。我讨论了两个应用程序：

- GIMP（GNU 图像操作程序）是一个用于查看和执行图像操作任务的程序，例如照片修饰、图像合成和图像创建。
- Gnome Ghostview (GGV) 是一个能够显示 PostScript 文件的图形应用程序。

##### The GIMP

The GIMP 是由 Peter Mattis 和 Spencer Kimball 编写的图像操作程序，并根据 GNU 通用公共许可证 (GPL) 发布。大多数 Linux 发行版都附带此程序，尽管你可能需要专门选择一个软件包来安装它。The GIMP 与其他图像操作程序（例如 Adobe Photoshop 和 Corel PHOTO-PAINT）相当。

要试用 The GIMP，请在主菜单的 图形 类别中找到它。启动时，The GIMP 会显示一个包含版权和许可证信息的窗口。点击 继续 按钮以继续安装。下一个屏幕显示当你继续进行 The GIMP 个人安装时将创建的目录。

The GIMP 的安装涉及在你的主目录中创建一个目录，并将若干文件放入该目录中。该目录基本上保存了你可能会对 The GIMP 进行的用户偏好设置更改的信息。请继续点击底部的 继续 按钮



窗口。GIMP 会创建必要的目录，将必要的文件复制到这些目录中，并通过一系列对话框引导您完成安装。

安装完成后，点击“继续”按钮。从现在开始，您将不再看到安装窗口：只有在首次运行 GIMP 时，才需要处理安装事宜。

随后，GIMP 会加载任何*插件*——即增强其功能的外部模块。它会显示一个启动窗口，展示每个插件加载时的信息。启动完成后，GIMP 会在一个窗口中显示“每日提示”。您可以浏览这些提示，并点击“关闭”按钮来关闭提示窗口。与此同时，GIMP 会显示多个窗口，如图 4-12 所示。

这些窗口包括一个标题为“GIMP”的主工具箱窗口、一个工具选项窗口、一个笔刷选择窗口，以及一个图层、通道、路径窗口。其中，主工具箱窗口最为重要——事实上，您可以关闭其他窗口，仅使用工具箱中的菜单和按钮进行操作。

![](img/11709a8f88c8cd03868a929dc94c0e2b_260_0.png)
![](img/11709a8f88c8cd03868a929dc94c0e2b_260_1.png)

工具箱菜单栏上有三个菜单：

-   **文件** 菜单提供了创建新图像、打开现有图像、保存和打印图像、通过邮件发送图像以及退出 GIMP 的选项。
-   **扩展**（Xtns）菜单允许您访问 GIMP 的众多扩展功能。Xtns 菜单的具体内容取决于您系统中安装了哪些扩展。
-   **帮助** 菜单是获取帮助和查看提示的地方。例如，选择“帮助::帮助”即可调出带有 GIMP 在线信息的 GIMP 帮助浏览器。

要在 GIMP 中打开图像文件，请选择“文件::打开”。此时会出现“加载图像”对话框，您可以使用它来选择图像文件。您可以更改目录并选择要打开的图像文件。GIMP 可以读取所有常见的图像文件格式，如 GIF、JPEG、TIFF、PCX、BMP、PNG 和 PostScript。选择文件并点击“确定”后，GIMP 会将图像加载到一个新窗口中。（请参阅图 4-12，查看图像在 GIMP 中加载后的样子，以及其他所有 GIMP 窗口。）

工具箱还有许多按钮，代表用于编辑图像和应用特殊效果的工具。将鼠标指针悬停在按钮上，即可获取每个工具按钮的弹出帮助。您可以点击工具按钮来选择工具，并将该工具的效果应用于图像。

为了方便您使用，当您在图像窗口上右键点击时，GIMP 会显示一个弹出菜单。该弹出菜单包含工具箱中“文件”和“扩展”菜单中的大多数选项。您可以从这些菜单中选择具体的操作。

使用 GIMP 所做的远不止加载和查看图像，但本书无法完整讨论其所有功能。如果您想尝试 GIMP 的其他功能，请查阅在线可用的 *《GIMP 用户手册》*（地址为 `http://manual.gimp.org`）。您也可以选择“扩展::Web 浏览器::GIMP.ORG::文档”来访问 GIMP 的在线文档。（当然，执行此命令需要网络连接。）

访问 GIMP 主页 `www.gimp.org`，以查找关于 GIMP 的最新新闻以及其他资源链接。

###### GNOME Ghostview

GNOME Ghostview 是一款图形应用程序，非常适合用于查看和打印 PostScript 或 PDF 文档。对于长篇文档，您可以查看并打印选定页面。您还可以通过放大或缩小来以不同的放大级别查看文档。

在 Fedora Core 中运行 GNOME Ghostview，请在 GUI 桌面上选择“主菜单 $\circled{5}$ 图形 $\circled{5}$ PostScript 查看器”。GNOME Ghostview 应用程序窗口将显示出来。除了顶部的菜单栏和工具栏外，垂直分隔线将窗口的主要显示区域分为两部分。

要在 GNOME Ghostview 中加载并查看 PostScript 文档，请选择“文件 $\circled{+}$ 打开”，或点击工具栏上的“打开”图标。GNOME Ghostview 会显示一个“文件选择”对话框。使用此对话框导航文件系统并选择一个 PostScript 文件。您可以选择随 Ghostscript 附带的一个 PostScript 文件。例如，打开 `/usr/share/ghostscript/7.07/examples` 目录中的 `tiger.ps` 文件。（如果您的系统中的 Ghostscript 版本高于 7.07，您必须使用新的版本号替代 7.07。）

要打开选定的文件，请点击“文件选择”对话框中的“打开文件”按钮。GNOME Ghostview 会打开选定文件，处理其内容，并在窗口中显示输出，如图 4-13 所示。

GNOME Ghostview 适用于查看各种 PostScript 格式的文档。（这些文件的名称通常带有 `.ps` 扩展名。）您还可以在 GNOME Ghostview 中打开 PDF 文件——这些文件通常带有 `.pdf` 扩展名。

> 记住

![](img/11709a8f88c8cd03868a929dc94c0e2b_262_0.png)

图 4-13：您可以在 GNOME Ghostview 中查看 PostScript 文件。

## 第 5 章：使用文本编辑器

###### 本章内容

-   使用 GUI 文本编辑器
-   使用 ed 文本编辑器
-   了解 vi 文本编辑器

在 Linux 中，大多数系统配置文件都是文本文件。如果您编写 shell 脚本或其他计算机程序，它们也是文本文件。有时，您必须使用专为此目的设计的程序——文本编辑器——来编辑这些文件。例如，您可能需要编辑诸如 /etc/hosts、/etc/resolv.conf、/etc/X11/XF86Config-4、/etc/apt/sources.list 以及许多其他文件。

在本章中，我将向您介绍几种文本编辑器——包括 GUI 编辑器和文本模式编辑器。

### 使用 GUI 文本编辑器

每个 GUI 桌面——GNOME 和 KDE——都附带 GUI 文本编辑器（具有图形用户界面的文本编辑器）。

要使用 GUI 文本编辑器，请在主菜单中查找文本编辑器所在的适当类别。例如，在 Debian 和 Fedora Core 中，请在 GNOME 桌面上选择“应用程序>附件>文本编辑器”。当文本编辑器启动并运行后，您可以点击工具栏上的“打开”按钮来打开文件，这会调出“打开文件”对话框。然后，您可以更改目录并通过点击“确定”按钮选择要编辑的文件。

随后，GNOME 文本编辑器会在其窗口中加载该文件。您可以一次打开多个文件，并在编辑文件时在其中进行切换。图 5-1 展示了使用编辑器的典型编辑会话。

在这种情况下，编辑器打开了三个文件以供编辑——hosts、fstab 和 inittab（均来自 /etc 目录）。文件名作为标签显示在编辑器窗口工具栏的下方。您可以通过点击标签在文件之间切换。当前文件名显示在窗口的标题栏中。

如果您打开的文件只有读权限，则窗口标题中显示的文件名后会附加文本 [Read Only]，以指示该文件为只读。在图 5-1 中，所有文件都是只读的，因为此处我是以普通用户身份登录的，且正在打开仅 root 用户可以修改的系统文件。

其余的文本编辑步骤都是直观的。要输入新文本，请点击以定位光标并开始键入。您可以使用文本编辑区域上方的工具栏按钮来选择文本、复制、剪切和粘贴。

从 KDE 桌面，您可以通过选择“主菜单->编辑器->高级文本编辑器”来启动 KDE 高级文本编辑器（Kate）。要打开文本文件，请选择“文件->打开”。Kate 会显示一个对话框。从此对话框中，您可以转到您选择的目录，选择要打开的文件，并点击“确定”。随后，Kate 会打开该文件并在窗口中显示其内容。然后，您可以编辑该文件。

![](img/11709a8f88c8cd03868a929dc94c0e2b_265_0.png)

### 使用 ed 和 vi 进行文本编辑

GUI 文本编辑器使您能够使用鼠标和键盘以与使用任何文字处理软件类似的方式编辑文本文件。文本模式编辑器则完全不同——您仅使用键盘进行操作，并且



必须输入晦涩的命令来执行编辑任务，例如剪切和粘贴文本，或输入和删除文本。Linux 附带两种文本模式编辑器：

- ed：一种面向行的文本编辑器
- vi：一种全屏文本编辑器，支持早期名为 ex 的编辑器所使用的命令集

与图形化文本编辑器相比，ed 和 vi 编辑器显得晦涩难懂。不过，你仍然应该熟悉 ed 和 vi 的基本编辑命令，因为有时这两个可能是唯一可用的编辑器。例如，如果 Linux 拒绝从硬盘启动，你可能不得不从软盘启动。在这种情况下，你必须使用 ed 编辑器来编辑系统文件，因为该编辑器足够小，可以装进软盘。我将向你介绍 ed 和 vi 的基本文本编辑命令——它们并没有那么难。

#### 使用 ed

通常，只有在你启动最小化的 Linux 版本（例如，从已设置为启动软盘的软盘启动），且系统不支持全屏模式时，才需要使用 ed。在其他所有情况下，你可以使用在全屏文本模式下工作的 vi 编辑器。

使用 ed 时，你在命令模式或文本输入模式下操作：

- **命令模式** 是你默认获得的状态。在此模式下，你输入的任何内容都将被解释为命令。ed 文本编辑器拥有一个简单的命令集，其中每个命令由一个或多个字符组成。
- **文本输入模式** 用于输入文本。你可以使用命令 a（追加）、c（更改）或 i（插入）进入输入模式。在输入多行文本后，你可以通过单独输入一个点 (.) 来结束输入模式。

为了练习编辑文件，请通过发出以下命令将 /etc/fstab 文件复制到你的主目录：

```
cd
cp /etc/fstab .
```

现在，你在主目录中有一个名为 fstab 的文件。键入 **ed -p: fstab** 开始使用 ed 编辑文件。编辑器的响应如下：

```
878
:
```

此示例使用 `-p` 选项将提示符设置为冒号字符 (`:`)，并打开 `fstab` 文件（位于当前目录，即你的主目录）进行编辑。`ed` 编辑器打开文件，报告文件中的字符数 (`878`)，显示提示符 (`:`)，并等待命令输入。

![](img/11709a8f88c8cd03868a929dc94c0e2b_267_0.png)

使用 `ed` 进行编辑时，请确保始终开启提示符字符（使用 `-p` 选项）。如果没有提示符，区分 `ed` 处于输入模式还是命令模式会很困难。

当 `ed` 打开文件进行编辑后，当前行是文件的最后一行。若要查看当前行号（当前行是 `ed` 应用你命令的行），请像这样使用 `., =` 命令：

```
:., =
9
```

此输出告诉你 `fstab` 文件有九行。（你系统的 `/etc/fstab` 文件可能有不同数量的行，在这种情况下 `ed` 会显示不同的数字。）

你可以使用 `1,$p` 命令查看文件中的所有行，如下例所示：

```
:1,$p
# This file is edited by fstab-sync - see 'man fstab-sync' for details
/dev/VolGroup00/LogVol00 / ext3 defaults 1 1
LABEL=/boot /boot ext3 defaults 1 2
/dev/depts /dev/gpt5 ext4 gid=5, mode=620 0 0
/dev/shm /dev/shm tmpfs defaults 0 0
/dev/proc /proc proc defaults 0 0
/dev/sys /sys sysfs defaults 0 0
/dev/VolGroup00/LogVol01 / swap defaults 0 0
/dev/scd0 /media/driverom auto
pamconsole, exec, noauto, managed 0 0
/dev/fd0 /media/floppy auto
pamconsole, exec, noauto, managed 0 0
/dev/hdc /media/cdrom auto
pamconsole, exec, noauto, managed 0 0
:
```

若要转到特定行，请输入行号：

```
:2
```

编辑器通过显示该行来响应：

```
/dev/VolGroup00/LogVol00 / ext3 defaults 1 1
:
```

假设你想删除包含 cdrom 的行。要搜索字符串，请输入斜杠 (/) 后跟你要查找的字符串：

```
:/cdrom/
cdrom
dev/hdc /media/cdrom auto
pamconsole,exec,noauto,managed 0 0
:
```

编辑器定位包含该字符串的行，然后显示该行。该行变为当前行。

要删除当前行，请像下面这样使用 d 命令：

```
:d
:
```

要将一个字符串替换为另一个字符串，请使用 s 命令。例如，要将 cdrom 替换为字符串 cd，请使用此命令：

```
:s /cdrom/cd/
:
```

要在当前行之前插入一行，请使用 i 命令：

```
:i
	(输入你想要插入的行)
.	(输入单个点表示完成)
:
```

你可以输入任意数量的行。在最后一行之后，单独输入一个点 (.)。该点标记文本输入模式的结束，编辑器切换到命令模式。在这种情况下，因为你会看到提示符 (:)，所以你可以判断 ed 已切换到命令模式。

当你满意所做的更改时，你可以使用 w 命令将它们写入文件。如果你想保存更改并退出，请输入 wq 同时执行这两个步骤：

```
:wq
857
```

ed 编辑器保存文件中的更改，显示保存的字符数，并退出。如果你想退出编辑器而不保存任何更改，请使用 Q 命令。

这些示例让你对如何使用 ed 命令执行文本文件的基本编辑任务有了了解。表 5-1 列出了一些常用的 ed 命令。

![](img/11709a8f88c8cd03868a929dc94c0e2b_268_0.png)

表 5-1 常用 ed 命令

| 命令 | 执行以下操作 |
| :---- | :---- |
| !command | 执行一个 shell 命令。（例如，`!pwd` 显示当前目录。） |
| $ | 转到缓冲区中的最后一行 |
| % | 将后续命令应用于缓冲区中的所有行。（例如，`%p` 打印所有行。） |
| + | 转到下一行 |
| +n | 转到第 n 行（其中 n 是你指定的数字） |
| ,% | 将后续命令应用于缓冲区中的所有行。（例如，`,p` 打印所有行。）这与 `%` 相似。 |
| - | 转到上一行 |
| -n | 转到第 n 行之前（其中 n 是你指定的数字） |
| . | 引用缓冲区中的当前行 |
| /text/ | 向前搜索指定文本 |
| ; | 引用一行范围——从当前行到缓冲区中的最后一行 |
| = | 打印行号 |
| ?text? | 向后搜索指定文本 |
| ^ | 转到上一行。（另请参阅 `^command`。） |
| ^n | 转到第 n 行之前（其中 n 是你指定的数字）。（另请参阅 `^n` 命令。） |
| a | 在当前行之后追加 |
| c | 更改指定行 |
| d | 删除指定行 |
| i | 在当前行之前插入文本 |
| n | 转到第 n 行 |
| 按 Enter | 显示下一行并使该行成为当前行 |
| q | 退出编辑器 |
| Q | 不保存更改退出编辑器 |
| r file | 读取并插入文件内容到当前行之后 |
| s/old/new/ | 将旧字符串替换为新字符串 |
| u | 撤销上一个命令 |
| W file | 将缓冲区内容追加到指定文件的末尾 |
| w file | 将缓冲区保存到指定文件中。（如果未命名文件，则保存至默认文件——即 `ed` 当前正在编辑其内容的文件。） |

#### 使用 vi

vi 编辑器是一种全屏文本编辑器，因此你可以同时查看多行。大多数 UNIX 系统，包括 Linux，都附带 vi。因此，如果你了解 vi 的基本功能，你就可以在几乎任何 UNIX 系统上编辑文本文件。

![](img/11709a8f88c8cd03868a929dc94c0e2b_270_0.png)

当 vi 编辑文件时，它会将文件读入缓冲区——一块内存——以便你可以更改缓冲区中的文本。vi 编辑器在编辑过程中还会使用临时文件，但在你保存更改之前，原始文件不会被修改。

要启动编辑器，请键入 `vi`，后跟你要编辑的文件名，如下所示：

```
vi /etc/fstab
```

然后，vi 编辑器将文件加载到内存中，在文本屏幕上显示前几行，并将光标定位在第一行，如图 5-2 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_270_1.png)

图 5-2：你可以使用 vi 全屏文本编辑器编辑文本文件。

最后一行显示文件的路径名，以及文件中的行数（11）和字符数（878）。在这种情况下，文件名后出现文本 `[read-only]`，因为我是以普通用户身份登录时打开 `/etc/fstab` 文件（这意味着我没有权限修改该文件）。稍后，vi 显示界面中的最后一行将作为命令输入区域。其余行显示文件内容。如果文件包含的行数少于屏幕行数，vi 会在第一列用波浪号 (`~`) 显示空行。





当前行由光标标记，光标显示为一个小的黑色矩形。光标出现在某个字符的上方。

在使用 `vi` 时，你处于三种模式之一：

- **可视命令模式**是你默认进入的模式。在此模式下，你输入的任何内容都被解释为应用于包含光标所在行的命令。`vi` 的命令类似于 `ed` 的命令。
- **冒号命令模式**用于读取或写入文件、设置 `vi` 选项以及退出 `vi`。所有冒号命令都以冒号（`:`）开头。当你输入冒号时，`vi` 将光标定位在最后一行，并等待你输入命令。当你按下 Enter 键时，命令生效。
- **文本输入模式**用于输入文本。你可以通过命令 `a`（在光标后插入）、`A`（在行尾追加）或 `i`（在光标前插入）进入输入模式。在输入几行文本后，你必须按 Esc 键离开输入模式并重新进入可视命令模式。

这些模式的一个共同问题是，你很难轻易判断 `vi` 当前处于哪种模式。你可能开始打字，然后才意识到 `vi` 并不在输入模式，这可能会让人沮丧。

如果你想确保 `vi` 处于命令模式，只需按几次 Esc 键即可。（多次按 Esc 键不会造成伤害。）

![](img/11709a8f88c8cd03868a929dc94c0e2b_271_0.png)

要在 `vi` 中查看在线帮助，请在冒号命令模式下输入 `:help`。看完帮助后，输入 `:q` 退出帮助屏幕，返回到正在编辑的文件。

`vi` 编辑器初始将光标定位在第一行的第一个字符上——而你能知道的最有用的事情之一就是如何移动光标。为了练习一下，请尝试表 5-2 中所示的命令。

**表 5-2** vi 中的光标移动命令

| 按键 | 执行以下操作 |
| :-- | :-- |
| ↓ | 将光标向下移动一行 |
| ↑ | 将光标向上移动一行 |
| ← | 将光标向左移动一个字符 |
| → | 将光标向右移动一个字符 |
| W | 将光标向前移动一个单词 |
| B | 将光标向后移动一个单词 |
| Ctrl+D | 向下移动半屏 |
| Ctrl+U | 向上滚动半屏 |

你可以随时使用便捷的冒号命令跳转到特定的行号。例如，要跳转到第 6 行，请输入以下内容，然后按 Enter 键：

```
:6
```

当你输入冒号时，vi 在屏幕的最后一行显示冒号。从那时起，vi 将你输入的任何文本作为命令使用。你必须按 Enter 键才能向 vi 提交命令。在冒号命令模式下，vi 接受 ed 编辑器接受的所有命令——以及其他一些命令。

要搜索一个字符串，首先输入一个斜杠（/）。vi 编辑器在屏幕的最后一行显示该斜杠。输入要搜索的字符串，然后按 Enter 键。vi 编辑器定位到该字符串，并将光标定位在该字符串的开头。因此，要在文件 /etc/fstab 中定位字符串 cdrom，请键入：

```
/cdrom
```

要删除包含光标的行，请输入 dd（两个小写 d）。vi 编辑器删除该行文本，并使下一行成为当前行。

要开始在光标前方输入文本，请输入 I（单独的小写 i）。vi 编辑器切换到文本输入模式。现在你可以输入文本。当输入完文本后，按 Esc 键返回可视命令模式。

编辑完文件后，你可以使用 :w 命令保存文件中的更改。要退出不保存任何更改的编辑器，请使用 :q! 命令。如果你想保存更改并退出，可以输入 :wq 同时执行这两个步骤。vi 编辑器保存文件中的更改并退出。你还可以通过按 Shift+ZZ（按住 Shift 键并按两次 Z 键）来保存更改并退出编辑器。

除了上述提到的命令外，vi 还接受大量命令。表 5-3 列出了按任务分类的一些常用 vi 命令。

**表 5-3** 常用 vi 命令

| 命令 | 执行以下操作 |
| :--- | :--- |
| **插入文本** | |
| a | 在光标后插入文本 |
| A | 在当前行末尾插入文本 |
| I | 在当前行开头插入文本 |
| i | 在光标前插入文本 |
| **删除文本** | |
| D | 删除到当前行末尾 |
| dd | 删除当前行 |
| dG | 从当前行删除到文件末尾 |
| dw | 从光标删除到下一个单词的末尾 |
| x | 删除光标所在的字符 |
| **修改文本** | |
| C | 修改到当前行末尾 |
| cc | 修改当前行 |
| J | 将当前行与下一行合并 |
| rx | 用 x 替换光标下的字符（其中 x 是任意字符） |
| **移动光标** | |
| h 或 ← | 向左移动一个字符 |
| j 或 ↓ | 向下移动一行 |
| k 或 ↑ | 向上移动一行 |
| L | 移动到屏幕末尾 |
| l 或 → | 向右移动一个字符 |
| w | 移动到下一个单词的开头 |
| b | 移动到上一个单词的开头 |
| **滚动文本** | |
| Ctrl+D | 向前滚动半屏 |
| Ctrl+U | 向后滚动半屏 |
| **刷新屏幕** | |
| Ctrl+L | 重绘屏幕 |
| **剪切和粘贴文本** | |
| yy | 将当前行复制（Yank）到未命名缓冲区 |
| P | 将复制的行粘贴到当前行上方 |
| p | 将复制的行粘贴到当前行下方 |
| **冒号命令** | |
| : ! 命令 | 执行 shell 命令 |
| :q | 退出编辑器 |
| :q! | 退出不保存更改 |
| :r 文件名 | 读取文件并将其插入到当前行之后 |
| :w 文件名 | 将缓冲区写入文件 |
| :wq | 保存更改并退出 |
| **搜索文本** | |
| /字符串 | 向前搜索字符串 |
| ?字符串 | 向后搜索字符串 |
| **其他** | |
| u | 撤销上一个命令 |
| Esc | 结束输入模式并进入可视命令模式 |
| U | 撤销对当前行的最近更改 |

## 第三部分

### 网络

第五波

作者：Rich Tennant

![](img/11709a8f88c8cd03868a929dc94c0e2b_276_0.png)

“我想你可以说这是我们的网络中心。”

#### 内容概览

- 第 1 章：连接到互联网 ...........................253
- 第 2 章：设置局域网......................275
- 第 3 章：添加无线以太网 LAN..........................287
- 第 4 章：管理网络 ..................................299

##### 第 1 章：连接到互联网

###### 本章内容

- ✔ 理解互联网
- ✔ 决定如何连接到互联网
- ✔ 使用 DSL 连接到互联网
- ✔ 使用电缆调制解调器连接到互联网
- ✔ 设置拨号 PPP 链接

互联网正迅速成为大多数人的生命线。似乎很多人一天都离不开它（我知道如果我写不了这本书的话就写不出来了）。有时候，我会想我们以前是如何在没有互联网的情况下生活的。鉴于互联网的普及和受欢迎程度，我很有把握地假设你想将你的 Linux 系统连接到互联网。在本章中，我将向你展示如何通过几种不同的方式连接到互联网——取决于你拥有 DSL、电缆调制解调器还是拨号网络连接。

连接到互联网的两个选项——DSL 和电缆调制解调器——涉及将一个特殊的调制解调器连接到你的 Linux 系统上的以太网卡。在这些情况下，你必须在你的 Linux 系统上设置以太网网络。（我在这本小书（minibook）的第 2 章中解释了网络知识。）在本章中，我将详细展示如何设置 DSL 或电缆调制解调器连接。

我还向你展示了另一个选项——拨号网络——它涉及从你的 Linux 系统拨号连接到互联网服务提供商（ISP）。

###### 理解互联网

你如何看待互联网取决于你的视角。普通人以他们使用的服务来看待互联网。例如，作为用户，你可能会将互联网视为一种具有如下功能的信息交换媒介：

- **电子邮件**：使用诸如 `mom@home.net` 这样的地址，向互联网上的任何其他用户发送电子邮件。




- **万维网（Web）**：从互联网上数百万台服务器下载并查看文档。
- **新闻组（Newsgroups）**：阅读新闻组并向名为 comp.os.linux.networking 或 comp.os.linux.setup 等新闻组发布新闻条目。
- **信息共享**：下载软件、音乐文件、视频等。反过来，你可以提供文件供其他系统的用户下载。
- **远程访问**：登录互联网上的另一台计算机，前提是你有权访问该远程计算机。

技术人员表示，互联网是一个全球性的*网络的网络*。术语 *internet*（小写形式）是 *internetworking*（网络互联）的缩写形式——即网络的互连。互联网协议（IP）的设计初衷就是连接许多独立的网络。

![](img/11709a8f88c8cd03868a929dc94c0e2b_279_0.png)

就物理连接而言，互联网类似于高速公路和道路组成的网络。这种相似性促使大众媒体将互联网称为“信息高速公路”。正如公路网络包含一些州际高速公路、许多州道以及更多住宅街道一样，互联网也有一些容量非常大的网络（例如，10 Gbps 的主干网可以处理每秒 100 亿比特），还有大量容量较小的网络，范围从 56 Kbps 的拨号连接到 45 Mbps 的 T3 链路不等。（*Kbps* 表示千比特每秒，*Mbps* 表示兆比特每秒。）高容量网络是互联网的骨干。

就管理而言，互联网并非由单一组织运营，也不是由任何中央计算机管理。你可以将物理互联网视为由成千上万的合作组织共同管理的*网络的网络*。是的，由*数千个*组织管理的一个网络集合——听起来很惊人，但它确实有效！

####### 决定如何连接互联网

你想连接互联网，但不知道该怎么办？让我来数一数这些方法。如今，连接家庭和小办公室到互联网有三种流行的选择。（当然，大型公司和政府还有许多其他连接方式。）

- **数字用户线（DSL）**：当地电话公司以及其他电信公司可能提供 DSL 服务。DSL 提供了一种通过普通电话线发送高速数字数据的方式。通常，DSL 提供的数据传输速率在 128 Kbps 到 1.5 Mbps 之间。你从互联网下载数据的速度比从你的 PC 向互联网发送数据（上传）快得多。DSL 的一个注意事项是，你的家必须距离当地的中央办公室（电话公司的设施，你的电话线在此结束）12,000 到 15,000 英尺以内。距离限制因提供商而异。在美国，你可以在 **www.dslreports.com/distance** 查看许多提供商的距离限制。

- **电缆调制解调器**：如果你所在地区的有线电视公司提供通过有线电视访问互联网的服务，你可以使用该服务将你的 Linux 系统连接到互联网。通常，电缆调制解调器提供的数据传输速率比 DSL 高——成本大致相同。通过电缆调制解调器从互联网下载数据比从你的 PC 向互联网发送数据快得多。你可以预期常规下载速度为 1.5 Mbps，上传速度约为 128 Kbps，但有时你可能会获得比这些更高的速度。

- **拨号网络**：在 DSL 和电缆调制解调器出现之前，大多数人使用的就是拨号连接。你将 PC 连接到一个调制解调器，该调制解调器连接到电话线。然后你拨号访问 ISP 以连接互联网。这就是为什么它被称为*拨号网络*——通过拨号调制解调器在你的 Linux PC 和另一个网络（互联网）之间建立网络连接。在这种情况下，最大数据传输速率为 56 Kbps。

DSL 和电缆调制解调器服务不仅将 you 连接到互联网，还充当你的互联网服务提供商（ISP）；除了更快的速度外，你支付的费用还包括 IP 地址和你的电子邮件账户。如果你使用拨号调制解调器连接互联网，首先你必须连接电话线（为此你向电话公司付费），然后选择并支付另一个单独的 ISP 费用——它给你提供一个拨号号码以及所有其他必要的便利设施（如 IP 地址和电子邮件账户）。

表 I-1 总结了所有这些选项。你可以参考该表，选择对你可用且最适合你需求的连接类型。

######## 表 I-1 拨号、DSL 和电缆的比较

| 特性 | 拨号 | DSL | 电缆 |
| --- | --- | --- | --- |
| 设备 | 调制解调器 | DSL 调制解调器，以太网卡 | 电缆调制解调器，以太网卡 |
| 还需要 | 电话服务和互联网服务提供商（ISP） | 电话服务及位于中央办公室 12,000 至 16,000 英尺以内的位置 | 有线电视连接 |
| 连接类型 | 拨号连接 | 始终在线，专用 | 始终在线，共享 |
| **典型速度** | 最大 56 Kbps | 下载 640 Kbps，上传 128 Kbps（更高速度需支付更多费用） | 下载 1.5 Mbps，上传 128 Kbps |
| **一次性成本（估计）** | 无 | 安装 = 100-200 美元（自行安装免费）；设备 = 50-100 美元（可租赁，可能需要激活费用） | 安装 = 100-200 美元（自行安装免费）；设备 = 50-100 美元（可租赁） |
| **典型月费（2005 年）** | 电话费 = 每月 20 美元；ISP 费 = 每月 15-30 美元 | 每月 40-50 美元；可能需要每月调制解调器租赁费 | 每月 40-50 美元；可能需要每月调制解调器租赁费 |

*注：费用因地区和提供商而异。所示费用为美国大都市地区的典型费用。*

![](img/11709a8f88c8cd03868a929dc94c0e2b_281_0.png)

除了表 1-1 中显示的三种选项外，你可能还可以使用一些其他不太常见的选项。这些包括光纤到户（FTTH）、电力线宽带（BPL）、固定无线宽带（称为 FWB 或 WiMax）以及卫星互联网接入（例如，DIREWAY 和 StarBand）。如果你的地理区域提供这些选项中的一种或多种，并且你想使用其中之一进行互联网接入，请按照特定服务提供商的说明设置互联网连接。通常，卫星互联网接入可在广阔的地理区域使用（甚至在没有电话或电缆的地方），但初始设备成本和月费高于 DSL 和电缆。有关卫星互联网接入的更多信息，请访问 www.satellite-internet-access.net。

###### 使用 DSL 连接

DSL 代表数字用户线。DSL 使用现有的电话线除了正常的模拟语音信号（*模拟* 意味着连续变化，而数字数据由 1 和 0 表示）外，还传输数字数据。电话线从你的家延伸到中央办公室，在那里线路连接到电话公司的网络。顺便说一下，从你的家到中央办公室的连接被称为*本地环路*。当你注册 DSL 服务时，电话公司会在中央办公室将你的电话线连接到一些特殊设备。该设备可以将数字数据与语音分离。从此以后，你的电话线可以承载数字数据，然后直接发送到中央办公室的互联网连接。

####### DSL 的工作原理

一个称为 DSL 调制解调器的特殊盒子负责通过你的电话线从你的 PC 向电话公司的中央办公室发送数字数据。你的 PC 可以通过你用于正常电话呼叫的同一部电话线连接互联网——即使线路正在用于 DSL，你仍然可以进行语音通话。图 1-1 显示了典型的 DSL 到互联网的连接。

你的 PC 通过以太网连接与 DSL 调制解调器通信，这意味着你需要在 Linux 系统中有一个以太网卡。

你的 PC 通过以太网连接向 DSL 调制解调器发送数字数据。DSL 调制解调器以不同于模拟语音信号使用的频率发送数字数据。语音信号占据了电话线可承载的所有频率的一小部分。DSL 使用较高的频率来传输数字数据，因此语音和数据可以在同一部电话线上传输。

![](img/11709a8f88c8cd03868a929dc94c0e2b_282_0.png)

**图 1-1：**  
DSL 通过普通电话线提供高速互联网连接。





![](img/11709a8f88c8cd03868a929dc94c0e2b_283_0.png)

你家与中心局之间的距离——即*环路长度*——是影响 DSL 性能的一个因素。不幸的是，电话线只能在有限的距离内可靠地传输 DSL 信号——通常不超过三英里，这意味着只有当你的家（或办公室）位于电话公司中心局大约三英里范围内时，你才能获得 DSL 服务。你的电话公司可以告诉你你的位置是否能接入 DSL。通常，他们有一个网站，你可以在上面输入你的电话号码，获取关于 DSL 可用性的回复。例如，美国地区的用户可以尝试访问 *www.dslavailability.com*。

####### DSL 字母汤：ADSL、IDSL、SDSL

我一直在使用 DSL 这个术语，仿佛只有一种 DSL 似的。正如你可能想象的那样，事情从来没有那么简单。实际上有三种 DSL 变体，每种都有不同的特性。请看以下说明：

- ADSL：非对称 DSL 是最常见的 DSL 形式，其下载速度（从 Internet 到你的 PC）远高于上传速度（从你的 PC 到 Internet）。ADSL 的下载速度最高可达 8 Mbps，上传速度最高可达 1 Mbps。ADSL 在你的位置距离中心局约 ½ 英里（12,000 英尺）以内时效果最佳。ADSL 服务的定价是根据你想要的下载和上传速度来决定的。一种名为 G.lite 的流行 ADSL 形式，专门设计为可以在你用于语音通话的同一条线路上工作。G.lite 的最大下载速度为 1.5 Mbps，最大上传速度为 512 Kbps。

- IDSL：ISDN DSL（ISDN 是一种较旧的技术，称为*综合业务数字网*）是一种特殊类型的 DSL，工作距离可达你的电话与中心局之间的五英里。缺点是 IDSL 仅提供*下行*（从 Internet 到你的 PC）和*上行*（从你的 PC 到 Internet）最高 144 Kbps 的速度。

- SDSL：对称 DSL 提供相等的下载和上传速度，最高可达 1.5 Mbps。SDSL 的定价是根据你想要的速度来决定的，速度越高费用越高。你的位置距离电话公司中心局越近，你能获得的连接速度就越快。

![](img/11709a8f88c8cd03868a929dc94c0e2b_283_1.png)

DSL（以及电缆调制解调器）的速度通常由两个用斜杠分隔的数字来指定，例如：1500/384。这些数字指的是以千位每秒为单位的数据传输速度（即，每秒千位数，缩写为 Kbps）。第一个数字是下载速度，第二个是上传速度。因此，1500/384 意味着你可以以最高 1,500 Kbps（或 1.5 Mbps）的速度从 Internet 下载，并以 384 Kbps 的速度上传到 Internet。如果你的电话线状况不完美，你可能无法达到这些最大速率——ADSL 和 SDSL 都会根据现有线路状况调整速度。

DSL 服务的价格取决于你选择的变体——ADSL、IDSL 还是 SDSL。对于大多数家庭用户来说，主要选择是 ADSL（或者更准确地说，是 ADSL 的 G.lite 形式），传输速度评级为 1500/128。

####### 典型的 DSL 设置

为了为你的家庭或企业获取 DSL，你必须联系一家 DSL 服务提供商。除了你的电话公司，你还可以找到许多其他 DSL 提供商。无论谁提供 DSL 服务，中心局——你的电话线连接到电话网络其余部分的地方——都必须进行一些工作。这项工作包括将你的电话线连接到能够与你家中或办公室的 DSL 调制解调器协同工作的设备。然后，中心局设备和你所在位置的 DSL 调制解调器就可以执行必要的“魔法”操作，通过电话线发送和接收数字数据。

由于需要在中心局设置你的线路，在你下单后需要一段时间才能让你的线路准备好接入 DSL。

你要做的第一步是查看提供服务的 DSL 提供商，看看你是否真的能获得该服务。由于 DSL 只能在特定距离——通常在你的位置和中心局之间小于 2.5 英里——内工作，你必须检查自己是否在该距离限制内。请联系你的电话公司以确认。你也许可以在网上检查这种可用性。尝试在 Google（*www.google.com*）中输入**DSL 可用性**以及你当地电话公司的名称。搜索结果通常包括一个网站，你可以在上面输入你的电话号码，以确定你的家或办公室是否可以接入 DSL。

如果 DSL 可用，你可以查看服务类型——ADSL 与 SDSL——以及定价。价格取决于你想要的下载和上传速度。有时，电话公司提供一种简单的住宅 DSL（基本上是 ADSL 的 G.lite 形式），*速度评级*为 1500/128——这意味着你可以以最高 1,500 Kbps 的速度下载，并以 128 Kbps 的速度上传。当然，这些是*最大值*，具体效果可能因情况而异。

在你选择了想要的 DSL 服务类型和提供商后，你可以下订单，让提供商在你家中或办公室安装必要的设备。图 1-2 展示了典型住宅 DSL 服务的连接示意图。

以下是图 1-2 中需要注意的要点：

- 将你的 DSL 调制解调器的数据连接连接到墙插面板上的电话接口。
- 将 DSL 调制解调器的以太网连接连接到你的 PC 上的以太网卡。
- 当你将其他电话或传真机连接到同一条电话线上时，在墙插面板和这些设备之间安装微滤波器。

![](img/11709a8f88c8cd03868a929dc94c0e2b_284_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_285_0.png)

由于同一条电话线既传输语音信号又传输 DSL 数据，你需要微滤波器来保护 DSL 数据免受可能的干扰。你可以在电子产品商店或从 DSL 提供商处购买。

> **警告！** 当你使用 DSL 将 Linux PC 连接到 Internet 时，连接始终是开启状态，这意味着外部人员入侵 PC 的潜在可能性更大。

你可以保护你的 Linux 系统免受入侵者侵害，此外作为额外的好处，你可以通过使用能够执行网络地址转换（NAT）的路由器，与局域网（LAN）中的其他 PC 共享高速连接。这种 NAT 路由器将内部 LAN 中的多个私有 Internet 协议（IP）地址转换为一个公共 IP 地址，从而允许所有内部 PC 访问 Internet。NAT 路由器充当你的 LAN 和 Internet 之间的网关，并将你的 LAN 与 Internet 隔离开来——这使得入侵者更难以到达你 LAN 上的系统。

如果你还想设置一个局域网，你需要一个以太网集线器将其他 PC 连接到网络。图 1-3 展示了一个典型的设置，通过 NAT 路由器和 DSL 调制解调器将 LAN 连接到 Internet。

![](img/11709a8f88c8cd03868a929dc94c0e2b_286_0.png)

图 1-3：
NAT 路由器将你的 PC 与 Internet 隔离，同时允许你与局域网中的其他 PC 共享 DSL 连接。

在设置如图 1-3 所示的连接时，以下是需要注意的要点：

- 你需要一个具有两个 10BaseT 以太网端口的 NAT 路由器（10BaseT 端口看起来像一个大型电话插孔，也称为 RJ-45 插孔）。通常，一个以太网端口标记为 Internet（或 External 或 WAN，即广域网），另一个标记为 Local 或 LAN（即局域网）。

- 你还需要一个以太网集线器。对于一个小型家庭网络，你可以购买一个 4 口或 8 口的以太网集线器。基本上，你需要的集线器端口数量应等于你打算连接到局域网的 PC 数量。

- 使用 10BaseT 以太网电缆将 DSL 调制解调器的以太网端口连接到 NAT 路由器的 Internet 端口。（这些电缆看起来像带有更大 RJ-45 插头的电话线，通常标记为 5 类线或 Cat 5 线。）

- 使用 10BaseT 以太网电缆将 NAT 路由器的 Local 以太网端口连接到以太网集线器的其中一个端口。

- 然后将每台 PC 连接到以太网集线器。（当然，要做到这一点，你必须首先在每台 PC 中安装并配置好以太网卡。）





您也可以购买内置 4 口或 8 口以太网集线器的 NAT 路由器。使用这种集成了路由器和集线器的设备，您只需一台设备即可组建局域网，并通过 DSL 调制解调器将其连接到互联网。这些设备通常以“有线/DSL 路由器”的名称出售，因为它们既适用于 DSL，也适用于有线调制解调器。

有关如何配置 Linux 系统的网络设置以使系统能够访问互联网的详细信息，请参阅本书第 2 章。

DSL 提供商通常使用一种名为以太网上的点对点协议（PPPoE）的协议，在您的计算机与提供商中心局的设备之间建立连接。PPPoE 要求您提供用户名和密码才能通过以太网建立网络连接。要为系统设置 PPPoE DSL 连接，您只需运行一个配置系统以支持 PPPoE 的工具程序即可。您可以在图形用户界面（GUI）桌面的主菜单中搜索找到该工具。

在 Fedora Core 中，您可以通过选择“系统” > “管理” > “网络”，点击工具栏上的“新建”，然后在弹出的对话框中的设备类型中选择“xDSL 连接”来设置 PPPoE DSL 连接。然后依次浏览各个屏幕并提供所需信息，如登录名和密码。

###### 使用有线调制解调器连接

有线电视公司还通过传输电视信号到您家庭的同一根同轴电缆提供高速互联网接入。在有线电视公司在其设施中安装必要的设备以通过同轴电缆收发数字数据后，客户即可申请有线互联网服务。然后，您就可以通过传输有线电视信号的同一根电缆获得高速互联网接入。

####### 有线调制解调器的工作原理

一个称为有线调制解调器的盒子是电视网络互联网接入的核心。（参见图 1-4。）有线调制解调器从您的 PC 的网卡获取数字数据，并将其放在一个未使用的频段中。（可以将其想象为另一个电视频道，但该频道传输的不是图像和声音，而是数字数据。）

有线调制解调器将上行数据——即从您的 PC 发送到互联网的数据——放在与下行数据——即从互联网传输到您的 PC 的数据——不同的频道上。根据设计，下行数据传输速度远高于上行传输速度。这种设计的假设是人们从互联网下载的内容远远多于上传的内容。（这对我们大多数人来说可能都是真的。）

![](img/11709a8f88c8cd03868a929dc94c0e2b_288_0.png)

**图 1-4：** 有线调制解调器通过电视网络提供高速互联网接入。

![](img/11709a8f88c8cd03868a929dc94c0e2b_288_1.png)

**技术细节**
传输所有这些数百个电视频道到您家中的同轴电缆是一种非常出色的信号载体。特别是，同轴电缆可以承载覆盖巨大频率范围——数百兆赫兹（MHz）——的信号。每个电视频道需要 6 MHz——而同轴电缆可以承载数百个这样的频道。有线调制解调器将上行数据放置在一个小的频段中，并期望在另一个完全独立的频段中接收下行数据。

**技术细节**
在您通往互联网的有线连接的另一端，是您的有线电视公司在其中心设施中安装的*有线电视调制解调器终端系统*（CMTS）——也称为*前端*。（参见图 1-4。）CMTS 将电视网络连接到互联网。它还提取由您的有线调制解调器（以及您邻居的调制解调器）发送的上行数字数据，并将所有这些数据发送到互联网。CMTS 还将数字数据放入上行信道，以便您的有线调制解调器可以提取这些数据并通过网卡将其提供给您的 PC。

有线调制解调器可以以大约 30 Mbps 的速度接收下行数据，并以大约 3 Mbps 的速度发送上行数据。然而，一个社区内所有的有线调制解调器都共享相同的下行容量。每个有线调制解调器都会从 CMTS 发送的数据流中过滤出——分离出——它所需的数据。有线调制解调器遵循一种名为 DOCSIS（有线服务接口数据，Data Over Cable Service Interface Specification）的调制解调器标准。您可以购买任何符合 DOCSIS 标准的调制解调器并与您的有线互联网服务配合使用；您只需致电有线电视公司，提供调制解调器的识别信息，以便 CMTS 能够识别并初始化该调制解调器即可。

![](img/11709a8f88c8cd03868a929dc94c0e2b_289_0.png)

实际上，使用有线调制解调器，您可以获得大约 1.5 Mbps 的下行传输速率和 128 Kbps 的上行速率。这些是最大速率，而您的实际传输速率通常较低，具体取决于同一时间有多少邻居正在使用有线调制解调器。

![](img/11709a8f88c8cd03868a929dc94c0e2b_289_1.png)

如果您想检查下行传输速度，请前往 http://bandwidthplace.com/speedtest 并点击链接开始测试。例如，对于我的有线调制解调器连接，最近的测试报告的下行传输速率约为 2.2 Mbps，但在其他时间，速率最高可达 5.2 Mbps。

####### 典型的有线调制解调器设置

要设置有线调制解调器接入，您的有线电视提供商必须提供高速互联网接入。如果该服务可用，您可以致电申请。有线电视公司通常会有促销活动，例如免安装费或前三个月优惠费率。请留意这些优惠。如果您运气好，当地的有线电视公司可能恰好在您想要申请时有促销活动正在进行。

安装通常由技术人员完成，他们会将传入的电缆分成两部分——一路去往电视，另一路去往有线调制解调器。技术人员会将有线调制解调器的信息提供给有线电视公司的前端，以便在其端进行设置。完成所有步骤后，您只需将 PC 的网卡插入有线调制解调器，即可开始享受高速互联网接入。图 1-5 展示了一种典型的有线调制解调器连接方式。

有线调制解调器连接到 PC 上的网卡。如果您的 PC 没有网卡，有线电视公司的技术人员通常会提供一个。

![](img/11709a8f88c8cd03868a929dc94c0e2b_290_0.png)

**图 1-5：** 有线电视信号在电视和有线调制解调器之间进行分配。

以下是关于图 1-5 中有线调制解调器设置的一些要点：

-   使用双向分配器将传入的有线电视信号分为两部分。（有线电视技术人员会安装分配器。）顺便提一下，双向分配器需要支持 1 GHz 频率；否则，它可能无法让包含互联网下行数据的频率通过。
-   使用同轴电缆将分配器的一个视频输出连接到有线调制解调器的 F 型视频连接器。
-   将有线调制解调器的 10BaseT 以太网连接连接到 PC 上的网卡。
-   将电视连接到双向分配器的另一个视频输出。

**警告！** 当您使用有线调制解调器将您的 Linux PC 直接连接到互联网时，连接始终是开启状态，因此更有可能有人尝试闯入该 PC。Linux 包含 `iptables` 数据包过滤功能，您可能需要使用它来保护您的 PC 免受不需要的互联网连接。

**特定发行版** 在 Fedora Core 中，您可以将防火墙设置设为高安全性。要在 Fedora Core 中配置防火墙设置，请在图形用户界面（GUI）桌面中选择**系统** > **管理** > **安全级别和防火墙**。

为了将您的 Linux PC 或局域网与公共互联网隔离，您可能需要在 PC 和有线调制解调器之间添加一个 NAT 路由器。NAT 路由器的一个网络接口连接到内部网络，另一个接口连接到您的局域网；然后路由器作为您的局域网和互联网之间的网关。作为额外的奖励，通过添加一个以太网集线器，您甚至可以与您自己局域网（LAN）中的所有 PC 共享一个有线调制解调器连接。更好的是，购买一个组合 NAT 路由器和集线器，这样您只需一台设备即可完成所有工作。顺便提一下，NAT 路由器和集线器通常以*有线/DSL 路由器*的名称出售，因为它们既适用于 DSL，也适用于有线调制解调器。

NAT 路由器将私有 IP 地址转换为公共 IP 地址。通过 NAT 路由器连接时，内部局域网中的任何 PC 都可以像拥有自己唯一的 IP 地址一样访问互联网。结果：您可以在多台 PC 之间共享一个互联网连接。（这是对整个“网络冲浪”家庭的理想解决方案！）

图 1-6 展示了一种典型的设置，其中有线调制解调器连接被局域网中的多台 PC 共享。

在设置如图 1-6 所示的连接时，请注意以下要点：

-   您需要一个带有两个 10BaseT 以太网端口的有线/DSL NAT 路由器（10BaseT 端口——也称为 RJ-45 插孔，外观类似于大的电话插孔）。通常，一个以太网端口标记为*互联网*（或*外部*或*WAN*，即广域网），另一个标记为*本地*。
-   如果您计划组建局域网，还需要一个以太网集线器。对于小型家庭网络，您可以购买一个 4 口或 8 口的以太网集线器。基本上，您需要一个具有与您计划连接到局域网的 PC 数量相等的端口的集线器。
-   考虑购买一个同时作为 NAT 路由器和具有多个以太网端口的集线器的单一设备。
-   将视频电缆连接到有线调制解调器的视频输入端口。
-   使用 10BaseT 以太网电缆将有线调制解调器的以太网端口连接到 NAT 路由器的互联网端口。（这些电缆看起来像电话线，只是以太网电缆的 RJ-45 插孔更大，并且通常标记为*Category 5* 或*Cat 5 线*。）
-   使用 10BaseT 以太网电缆将 NAT 路由器的本地以太网端口连接到以太网集线器上的任一端口。
-   现在将每台 PC 连接到以太网集线器。当然，每台 PC 必须有一张网卡。




###### 设置拨号网络

![](img/11709a8f88c8cd03868a929dc94c0e2b_292_0.png)

图 1-6：NAT 路由器将你的计算机与互联网隔离，同时也允许你与其他局域网内的计算机共享宽带调制解调器连接。

在这本小册子的第 2 章中，我将解释如何配置局域网中的计算机，使它们都能通过该路由器访问互联网。

### 拨号网络

*拨号网络* 指的是通过拨号调制解调器将计算机连接到远程网络。如果你足够年长，还记得通过 Procomm 或某些串行通信软件进行拨号上网的日子，请意识到拨号网络与过去的串行通信有显著区别。这两种方法都使用调制解调器拨号连接到远程计算机并建立通信路径，但串行通信软件使你的计算机表现得像是连接到远程计算机的哑终端。串行通信软件独占拨号连接。例如，你无法运行另一个通信软件副本并使用同一调制解调器连接。

在拨号网络中，你的计算机和远程系统都运行网络协议（称为 TCP/IP）软件。当你的计算机拨号并建立通信路径时，网络协议通过该拨号连接交换数据分组。精彩之处在于，任意数量的应用程序都可以使用同一拨号连接来发送和接收数据分组。因此，你的计算机成为远程计算机所属网络的一部分。（如果远程计算机不在网络上，拨号网络将创建一个由远程计算机和你的计算机组成的网络。）

在这本小册子的第 2 章中，我将更多地描述 TCP/IP 协议，但我必须在描述如何设置拨号网络时使用该术语以及几个概念，如互联网协议（IP）地址和域名服务（DNS）。

在拨号链路上设置 TCP/IP 网络涉及指定协议——即用于在通信链路上封装数据分组的约定。点对点协议（PPP）就是一种用于在任何点对点链路（包括拨号电话线）上建立 TCP/IP 连接的协议。Linux 支持 PPP，并附带你可以用来设置 PPP 的配置工具，从而使你的系统能够与你的 ISP 建立 PPP 连接。

![](img/11709a8f88c8cd03868a929dc94c0e2b_293_0.png)

以下是在 Linux 中设置拨号网络所需执行的操作：

1. 在你的计算机中安装内部或外部调制解调器。如果你的计算机没有自带内部调制解调器，你可以购买外部调制解调器并将其连接到计算机的串行端口或 USB 端口。
2. 将调制解调器连接到电话线并给调制解调器通电。
3. 从 ISP 处获取一个账户。每个 ISP 都会提供一个拨号电话号码、一个用户名和一个密码。此外，ISP 还会提供电子邮件和新闻服务器的完整名称。通常，你的系统会自动获取 IP 地址。
4. 运行一个 GUI 工具（如果可用）来设置 PPP 连接。如果你找不到 GUI 工具，请在 shell 提示符下输入 `wvdialconf`。`wvdialconf` 程序会自动检测调制解调器并设置配置文件 `/etc/wvdial.conf`。现在使用文本编辑器编辑文件 `/etc/wvdial.conf`，并输入 ISP 的电话号码以及你在 ISP 处的互联网账户的用户名和密码。（你可以猜到在哪里输入这些项目；只需寻找标有 Username、Password 和 Phone 的字段即可。）
5. 使用 GUI 工具（如果可用）激活 PPP 连接以连接到互联网。如果没有 GUI 工具，请以 `root` 身份登录并输入 `wvdial` 以建立 PPP 连接。

我将在下面几节中简要介绍这些步骤。

####### 连接调制解调器

*modem*（调制解调器）一词是调制器/解调器（modulator/demodulator）的缩写——一种将数字信号（1 和 0 的字符串）转换为通过电话线和无线电波传输的连续变化模拟信号的设备。因此，调制解调器是计算机的数字世界和电话的模拟世界之间的中介。图 1-7 阐明了调制解调器的概念。

![](img/11709a8f88c8cd03868a929dc94c0e2b_294_0.png)

**图 1-7：** 调制解调器连接了计算机的数字世界和电话的模拟世界。

在计算机内部，1 和 0 用电压电平表示，但通过电话线传输的信号通常是不同频率的音调。调制解调器位于计算机和电话线之间，使电话线上的数据通信成为可能。调制解调器在数字电路的有/无电压表示和适合通过电话线传输的不同频率音调之间来回转换信息。

在使用外部调制解调器拨号之前，你必须确保调制解调器已正确连接到计算机的串行端口或 USB 端口之一。

如果你有一个外部调制解调器，请确保你的调制解调器已正确连接到电源，并且调制解调器已连接到电话线。购买正确类型的电缆将调制解调器连接到计算机。你需要一根直通串行电缆将调制解调器连接到计算机。电缆两端的连接器取决于你的计算机上的串行连接器类型。调制解调器一端的电缆需要公头 25 针连接器。计算机一端的电缆通常是母头 9 针连接器。你可以在大多数电脑商店购买到调制解调器电缆。通常，你可以找到标有 *AT Modem Cable* 标签的 9 针母头转 25 针公头调制解调器电缆。使用 USB 电缆连接 USB 调制解调器。

######## Winmodems：只支持 Windows

关于随许多新计算机和笔记本电脑附带的 *Winmodems*，需要稍微提个醒：Winmodems 是基于软件的内部调制解调器——与传统硬件调制解调器完全不同。也被称为 *Windows 调制解调器* 或 *软件调制解调器*（简称 softmodems），它们仅能与特殊的驱动程序软件配合工作（而后者又仅与 Microsoft Windows 配合工作）。对于 Winmodems 和 Linux，你基本上需要自己搞定，但你可以在线 [www.linuxmodems.org](http://www.linuxmodems.org) 的 Linux Winmodem 支持主页上找到一些有用的指导。例如，我发现我笔记本电脑中的 Winmodem 使用 Conexant 芯片组，并且可以从 [www.linuxant.com](http://www.linuxant.com/drivers/hsf/full/11/download.php) 获取 Linux 驱动程序。然后我可以下载适合我发行版的版本——该网站提供了 Debian 包（DPKG）和 RPM 格式文件。顺便说一下，Conexant 驱动的免费版本仅限于 14.4 Kbps。要提升到 56 Kbps，你必须以大约 15 美元的不高价格获取完整版本。不过，免费版本足以用于测试，以确保驱动程序能与你的软件调制解调器配合工作。顺便说一下，通过检查 [www.linuxmodems.org](http://www.linuxmodems.org) 网站，你可以找到许多其他 Winmodem 的 Linux 驱动程序。

![](img/11709a8f88c8cd03868a929dc94c0e2b_295_0.png)

如果你的计算机有内部调制解调器，你只需将电话线连接到内部调制解调器卡背面的电话插孔即可。如果是 Winmodem，你仍然需要连接电话线，但你还需要在互联网上做一点研究并下载一个使 Winmodem 在 Linux 中工作的驱动程序。安装好适用于 Winmodem 的可用 Linux 驱动程序后，它的运作方式与旧的串行端口调制解调器一样。欲了解更多信息，请参阅侧栏“Winmodems：只支持 Windows”。

###### 设置和激活 PPP 连接

大多数 ISP 通过其维护的一个或多个系统提供到互联网的 PPP 拨号访问。如果你注册了此类服务，ISP 将提供你建立到 ISP 系统的 PPP 连接所需的信息。通常，这些信息包括以下内容：

- 连接到远程系统需拨的电话号码。
- 登录远程系统必须使用的用户名和密码。
- ISP 的邮件和新闻服务器名称。
- 你的 PPP 连接的 IP 地址。如果 IP 地址是动态分配的（这意味着每次你的系统建立连接时 IP 地址可能会变化），ISP 不会提供此地址。
- ISP 的 DNS 的 IP 地址。如果 ISP 动态分配 IP 地址，则不会提供这些地址。




在以上信息中，前两项是建立 PPP 连接所需的条件。设置和使用 PPP 连接的具体步骤取决于你所使用的发行版。对于具有图形界面（GUI）互联网连接工具的发行版，你可以轻松找到输入 ISP（互联网服务提供商）账户信息的位置——电话号码、用户名和密码。接下来，我将介绍几种特定发行版配置 PPP 的方法。

Debian 提供了一个用于设置 PPP 连接的图形界面工具，该工具使用 wvdial（默认未安装）。输入 `apt-get install wvdial` 来安装它。之后，你可以使用图形界面工具来配置并激活拨号 PPP 连接。

![](img/11709a8f88c8cd03868a929dc94c0e2b_296_0.png)

在 Fedora Core 中，请从 GNOME 桌面选择 系统->管理->网络。（如果你不是以 `root` 身份登录，系统会提示你输入 `root` 密码。）点击工具栏上的“新建”；然后在第一个对话框中选择调制解调器连接选项（参见图 1-8），并继续进行配置。

![](img/11709a8f88c8cd03868a929dc94c0e2b_296_1.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_296_2.png)

图 1-8：在 Fedora Core 中，通过此对话框配置 PPP 连接。

在 SUSE 中，选择 主菜单->系统->YaST 以打开 YaST 控制中心窗口。点击窗口左侧的“网络设备”，然后点击右侧的“调制解调器”。（参见图 1-9。）YaST 会检测调制解调器，并显示一个包含调制解调器信息的窗口。然后你可以为检测到的调制解调器配置 PPP 连接。你可以从列表中选择你的 ISP，或者输入 ISP 的名称以及接入电话号码和 ISP 账户的用户名和密码。

![](img/11709a8f88c8cd03868a929dc94c0e2b_296_3.png)

# 第三册
## 第 1 章
### 连接互联网

![](img/11709a8f88c8cd03868a929dc94c0e2b_297_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_297_1.png)

在 SUSE 中设置好调制解调器后，Kinternet 工具应当启动，并且面板中应出现一个插头图标，如图 1-10 所示（如果图标未出现，请从 KDE 桌面选择 **主菜单** > **互联网** > **拨号**）。然后你可以点击 Kinternet 工具的图标来激活 PPP 连接。如果连接似乎没有建立，请右键点击 Kinternet 图标，选择 **查看日志**，并寻找可能问题的线索。

![](img/11709a8f88c8cd03868a929dc94c0e2b_297_2.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_297_3.png)

####### 配置 CHAP 和 PAP 认证

系统中的 PPP 服务器必须向 ISP 的 PPP 服务器进行身份验证，PPP 连接才能完全建立并运行。*认证* 要求证明你在 ISP 处拥有有效账户，本质上就是提供用户名和一个 *秘密信息*（即密码）。PPP 规定了在连接两端之间交换认证信息的两种方法：

- **质询握手认证协议（CHAP）** 要求远端发送一个随机生成的质询字符串以及远端服务器的名称。本地系统使用服务器名称查找 *秘密信息*；然后它返回一个响应，该响应包含其名称以及一个结合了 *秘密信息* 和质询的值，使用单向哈希函数计算得出。远端系统随后将其计算出的预期哈希值与该值进行比对。如果值匹配，则认证成功；否则，远端系统将终止连接。在这种情况下，名称和 *秘密信息* 存储在 */etc/ppp/chap-secrets* 文件中。请注意，只要 PPP 链接处于活动状态，远端系统可以随时重复 CHAP 认证。
- **密码认证协议（PAP）** 类似于正常的登录过程。使用 PAP 时，本地系统会反复发送用户名（名称）和密码（*秘密信息*），直到远端系统确认认证或终止连接为止。名称和 *秘密信息* 存储在 */etc/ppp/pap-secrets* 文件中。请注意，用户名和密码是以明文（即未加密）形式发送的。

Linux PPP 服务器支持这两种类型的认证。对于 PAP 和 CHAP，PPP 服务器所需的信息都是名称和一个 *秘密信息*——即用户名和密码对。这些认证信息存储在以下配置文件中：

- */etc/ppp/chap-secrets* 存储 CHAP 的信息。这是一个典型的 chap-secrets 文件的样子：

```
# Secrets for authentication using CHAP
# client      server      secret      IP addresses
"naba"        *          "mypassword"
```

- */etc/ppp/pap-secrets* 存储 PAP 的信息。这是一个典型的 pap-secrets 文件：

```
# Secrets for authentication using PAP
# client      server      secret      IP addresses
"naba"        *          "mypassword"
```

如你所见，chap-secrets 和 pap-secrets 中条目的格式是相同的。每行包含四个字段，顺序如下：

- *client*：此字段包含认证过程中使用的名称。你从 ISP 处获得此名称。
- *server*：此字段包含正在向本地系统进行认证的远端系统的名称。如果你不知道服务器名称，请键入星号以表示任意服务器。
- *secret*：此字段是本地系统的 PPP 服务器必须发送给远端系统以进行自我认证的 *秘密信息*。你从 ISP 处获得此密码。
- *IP addresses*：此可选字段可以包含本地系统连接指定服务器时可能使用的 IP 地址列表。通常此字段留空，因为本地系统通常从服务器获取动态 IP 地址，因此（通常）不知道它使用什么 IP 地址。

##### 第 2 章：设置局域网

###### 本章内容
- 理解 TCP/IP 网络
- 设置以太网局域网
- 配置 TCP/IP 网络
- 将你的局域网连接到互联网

Linux 内置了对传输控制协议/互联网协议（TCP/IP）网络的支持，大多数现代操作系统也是如此，从 Windows 到 Mac OS 皆是如此。你可以通过许多不同的物理接口使用 TCP/IP 网络，例如以太网卡、串行端口和并行端口。

通常，你在办公室甚至家庭中使用以太网作为局域网（LAN）（如果你在家拥有两台或更多系统）。要通过调制解调器连接到远程系统，你使用点对点协议（PPP）上的 TCP/IP 网络。

本章描述如何设置以太网。即使你只有一台 PC，你可能也需要设置以太网网络接口，以便将你的 PC 连接到使用 DSL 或电缆调制解调器的高速互联网访问。（关于 DSL 和电缆调制解调器的内容请参见本小册子的第 1 章。）

###### 理解 TCP/IP

如果你从分层模型的角度思考，将模型分为四层，最好理解 TCP/IP 网络。将每一层视为负责执行特定任务。分层模型描述了数据在网络物理连接和最终用户应用之间的流动。图 2-1 展示了 TCP/IP 的四层网络模型。

![](img/11709a8f88c8cd03868a929dc94c0e2b_301_0.png)

在这个四层模型中，信息总是在层与层之间移动。例如，当一个应用向另一个应用发送数据时，数据按以下顺序通过各层：应用 ➔ 传输 ➔ 网络 ➔ 物理。在接收端，数据从物理 ➔ 网络 ➔ 传输 ➔ 应用 向上移动。

每一层都有自己的 *协议* 集合——约定——用于处理和格式化数据。如果你将发送数据类比为通过邮政服务寄信，典型的协议就是执行任务的优选操作序列，例如在信封上写地址（先是姓名，然后是街道地址，再然后是城市、州名和邮编或其他邮政编码）。

以下是四层从下到上各自的功能：

- **应用层**：运行用户使用的应用程序，如电子邮件阅读器、文件传输和 Web 浏览器。应用层协议包括用于电子邮件的简单邮件传输协议（SMTP）和邮局协议（POP），用于 Web 的超文本传输协议（HTTP），以及用于文件传输的文件传输协议（FTP）。应用层协议还有一个 *端口号*，你可以将其视为特定应用的标识符。例如，端口 80 与 HTTP 或 Web 服务器相关联。
- **传输层**：将数据从一个应用程序发送到另一个应用程序。此层中两个最重要的协议是传输控制协议（TCP）和用户数据报协议（UDP）。TCP 保证数据交付；UDP 只是发送数据，而不确保其实际到达目的地。
- **网络层**：此层负责将数据包从一个网络传递到另一个网络。如果网络相距较远，数据包将从一个网络路由到下一个网络，直到到达目的地。此层的主要协议是互联网协议（IP）。





####### 物理层

指的是承载网络中数据包的物理网络硬件（例如以太网卡或令牌环卡）。

分层模型的美妙之处在于，每一层只负责其特定的任务，其余的交给其他层。各层可以灵活组合——你可以使用任何类型的物理网络介质上的 TCP/IP 网络，从以太网到无线电波（在无线网络中）。软件也是模块化的，因为每一层都可以通过不同的模块来实现。例如，通常传输层和网络层作为操作系统的一部分已经存在，任何应用程序都可以使用这些层。

###### TCP/IP 与互联网

TCP/IP 已成为互联网上首选的协议——互联网是由 ARPANet 演变而来的*网络的网络*。美国政府的高级研究计划局（ARPA）在 20 世纪 70 年代启动了一项关于通过在网络中发送数据包来传递信息的新方式的研究。其结果是 ARPANet：一个由互连计算机组成的国家网络。随后，ARPA 获得了国防前缀并变成了 DARPA。在 DARPA 的推动下，TCP/IP 协议作为用于*网络互联*（即网络间通信）的流行协议集合出现。

TCP/IP 之所以蓬勃发展，是因为该协议是开放的。这意味着协议的技术描述出现在公开文档中，因此任何人都可以在特定的硬件和软件上实现 TCP/IP。

TCP/IP 也取得了巨大进展，因为稳定且可用的软件是可用的。TCP/IP 协议一开始就是可用的软件，而不是网络架构和协议的文字描述——谁能与已经可用的东西争论呢？如今，因此 TCP/IP 统治了互联网。

###### IP 地址

当网络上有很多计算机时，你需要一种方法来唯一地标识每一台。在 TCP/IP 网络中，计算机的地址是 IP 地址。因为 TCP/IP 处理网络互联，所以地址基于网络地址和主机地址的概念。你可以把网络地址和主机地址的想法理解为需要提供两个地址来唯一地标识一台计算机：

-   **网络地址**指示计算机所在的网络。
-   **主机地址**指示该网络中的一台特定计算机。

###### 下一代 IP (IPv6)

当创建 4 字节 IP 地址时，可用地址的数量似乎足够。然而现在，4 字节地址正在耗尽。互联网工程任务组（IETF）在 1991 年认识到 IP 地址可能耗尽的潜力，并开始研究下一代 IP 寻址方案。他们将其称为 IPng（代表互联网协议下一代），并打算最终用旧的 4 字节寻址方案（称为 IPv4，代表 IP 版本 4）替换它。

针对 IPng 提出了几种替代寻址方案并进行讨论。最终的竞争者，具有 128 位（16 字节）地址，被称为 IPv6（代表 IP 版本 6）。1995 年 9 月 18 日，IETF 宣布 IPv6 寻址协议的核心集成为 IETF 提议标准。到目前为止，有许多 RFC 处理 IPv6 的各个方面，从用于通过以太网传输 IPv6 数据包的 IPv6 over PPP。

IPv6 旨在成为从 IPv4 到演进的一步。提议的标准提供了使用旧 IPv4 地址的主机和任何新的 IPv6 主机之间的直接互操作性。其想法是，用户可以在想要时将其系统升级到使用 IPv6，并且网络运营商可以自由地将其网络硬件升级到使用 IPv6 而不影响当前的 IPv4 用户。包括 Linux 在内的许多操作系统的 IPv6 示例实现正在开发中。有关 Linux 中 IPv6 的更多信息，请访问 www.tldp.org/HOWTO/Linux+IPv6-HOWTO 上的 Linux IPv6 HOWTO。有关 IPv6 的一般信息，请访问 www.ipv6.org 上的 IPv6 主页。

IPv6 的 128 位寻址方案允许总共 $2^{128}$ 或 340,282,366,920,938,463,463,374,607,431,768,211,456 个理论上可分配的地址！这应该能让我们用一段时间！

网络地址和主机地址共同构成了*IP 地址*，它是一个 4 字节（32 位）的值。约定是将每个字节写为十进制值，并在每个数字后面加一个点（.）。因此，你会看到诸如 132.250.112.52 这样的网络地址。这种书写 IP 地址的方式被称为*点分十进制*或*点分四元组*表示法。

在十进制表示法中，一个字节（具有 8 位）可以具有 0 到 255 之间的值。因此，有效的 IP 地址在点分十进制表示法中只能使用 0 到 255 之间的数字。

###### 互联网服务和端口号

TCP/IP 协议套件已成为互联网的*通用语言*，因为任何支持 TCP/IP 的系统都提供许多标准服务。这些服务通过促进邮件、新闻和网页的传输使互联网运转。这些服务以众所周知的名称进行，例如：

-   DHCP（动态主机配置协议）用于动态配置计算机上的 TCP/IP 网络参数。DHCP 主要用于分配动态 IP 地址和配置 TCP/IP 网络所需的其他网络信息（如名称服务器、默认网关和域名）。DHCP 服务器监听端口 67。
-   FTP（文件传输协议）用于在互联网上的计算机之间传输文件。FTP 使用两个端口——数据在端口 20 上传输，控制信息在端口 21 上交换。
-   HTTP（超文本传输协议）是一种用于将一个系统中的文档发送到另一个系统的协议。HTTP 是 Web 的基础协议。默认情况下，Web 服务器和客户端在端口 80 上通信。
-   SMTP（简单邮件传输协议）用于在系统之间交换电子邮件。SMTP 使用端口 25 进行信息交换。
-   NNTP（网络新闻传输协议）用于以存储并转发的方式在互联网上分发新闻文章。NNTP 使用端口 119。
-   SSH（安全外壳协议）是一种用于在不安全网络上进行安全远程登录和其他安全网络服务的协议。SSH 使用端口 22。
-   TELNET 用于当用户在互联网上一个系统登录到另一个系统时。（用户必须提供有效的用户 ID 和密码才能登录到远程系统。）TELNET 默认使用端口 23，但 TELNET 客户端可以连接到任何端口。
-   SNMP（简单网络管理协议）用于管理互联网上的所有类型的网络设备。与 FTP 类似，SNMP 使用两个端口：161 和 162。
-   TFTP（简单文件传输协议）用于将一个系统中的文件传输到另一个系统。（它通常由 X 终端和无盘工作站使用，用于从网络上的另一台主机下载引导文件。）TFTP 数据传输发生在端口 69 上。
-   NFS（网络文件系统）用于在计算机之间共享文件。NFS 使用 Sun 的远程过程调用（RPC）设施，该设施通过端口 111 交换信息。

每个此类服务都关联着一个知名端口。TCP 协议使用每个这样的端口来定位任何系统上的服务。（服务器进程——在系统上运行的特殊计算机程序——提供每个服务。）

###### 设置以太网局域网

以太网是在连接到单个集线器的两台或多台计算机之间移动数据包的标准方式。（你可以通过网关连接多个以太网段来创建更大的网络。）要设置以太网局域网，你需要为每台 PC 配备一块以太网卡。Linux 支持 PC 的各种各样的以太网卡。

以太网是物理数据传输机制的良好选择，原因如下：

-   以太网是一项自 20 世纪 80 年代初以来一直在使用的经过验证的技术。
-   以太网提供良好的数据传输速率：通常 10 Mbps（10 Mbps），尽管现在已有 100-Mbps 以太网和千兆以太网（1,000 Mbps）。
-   以太网硬件通常内置于 PC 中，或者可以以相对较低的成本安装。（PC 以太网卡价格约为 10 - 20 美元。）
-   使用无线以太网，你可以轻松地将膝上型 PC 连接到你的以太网局域网，而无需到处拉线。（有关无线以太网的更多信息，请参阅本书第 3 章。）

####### 以太网的工作原理

那么，是什么让以太网运转？本质上，它使任何对话起作用的东西：倾听和轮流发言。

在以太网网络中，段中所有系统都连接到同一根导线。因为使用单根导线，所以使用协议来发送和接收数据，因为在任何时刻电缆上只能存在一个数据包。以太网局域网使用一种称为*载波侦听多路访问/冲突检测*（CSMA/CD）的数据传输协议来在所有计算机之间共享单个传输电缆。计算机中的以太网卡遵循 CSMA/CD 协议来传输和接收以太网数据包。

CSMA/CD 协议背后的想法类似于你在派对上交谈的方式。你倾听停顿（这就是侦听载波），并在没人说话时说话。如果你和另一个人同时开始说话，你们俩都意识到问题（这就是冲突检测）并暂停片刻；然后其中一人再次开始说话。正如你从经验中知道的那样，一切都会解决。

在以太网局域网中，每个以太网卡检查电缆上的信号——这就是载波侦听部分。如果信号电平较低，以太网卡在电缆上发送其数据包；数据包包含关于发送者和预期接收者的信息。局域网上的所有以太网卡都会监听信号，并且接收者接收数据包。如果两个网卡同时发送数据包，


当电缆中的信号电平超过某个阈值时，网卡便会得知发生了冲突（即两个数据包在同一时间被发送出去）。两个网卡都会等待一段随机的时间后，才重新发送它们的数据包。

以太网发明于 20 世纪 70 年代初，由 Robert M. Metcalfe 在施乐帕洛阿尔托研究中心（PARC）设计。到了 20 世纪 80 年代，以太网通过三家公司的合作努力而实现了标准化：数字设备公司（DEC）、英特尔（Intel）和施乐（Xerox）。利用公司名称的首字母，该以太网标准被称为 *DIX* 标准。后来，*DIX* 标准被纳入了由电气和电子工程师学会（IEEE）制定的 802 系列标准。最终的以太网规范正式称为 IEEE *802.3* CSMA/CD，但人们仍然习惯称之为 *Ethernet*。

以太网以*数据包*（离散的块，也称为*帧*）的形式发送数据。你不需要过多关注以太网数据包内部结构，但需注意 6 字节的源地址和目的地址。每个以太网控制器在物理层都有一个唯一的 6 字节（48 位）地址；每个数据包都必须包含该地址。

####### 以太网线缆

任何当你听到专家谈论以太网时，你也会听到一些关于承载数据的线缆的术语让人困惑。以下是简要说明。

![](img/11709a8f88c8cd03868a929dc94c0e2b_306_0.png)

最初的以太网标准使用粗同轴电缆，直径将近半英寸。这种布线被称为*粗缆*或*粗以太网*，尽管 IEEE 802.3 标准称其为 *10Base5*。该命名表示了几个含义：数据传输速率为每秒 10 兆位（10 Mbps）；传输是*基带*的（这仅仅意味着电缆的信号承载能力专用于传输以太网数据包），并且电缆的总长度不得超过 500 米。*粗缆*成本高昂，且电缆相当笨重。除非你是技术历史爱好者，否则你完全不必在意 10Base5 电缆。

![](img/11709a8f88c8cd03868a929dc94c0e2b_306_1.png)

如今，其他几种以太网布线形式更为流行。粗以太网电缆的替代方案是*细缆*，即 10Base2，它使用细而灵活的同轴电缆。细缆以太网段最长可达 185 米。另一种较新的替代方案是通过非屏蔽双绞线（UTP）传输以太网，称为 10BaseT。支持更高传输速率的较新以太网布线选项包括用于 100 Mbps 以太网的 100BaseT4、100BaseT2 和 100BaseTX，以及用于千兆以太网的 1000BaseT。电子工业协会/电信工业协会（EIA/TIA）定义了以下五类屏蔽和非屏蔽双绞线电缆：

- 1 类（Cat 1）：传统电话电缆。
- 2 类（Cat 2）：经认证用于最高 4 Mbps 数据传输的电缆。
- 3 类（Cat 3）：可传输高达 16 MHz 频率信号的电缆。Cat 3 是旧企业网络中最常见的布线类型，通常包含四对线。如今已被视为过时。
- 4 类（Cat 4）：可传输高达 20 MHz 频率信号的电缆。Cat 4 线缆不太常见。如今已被视为过时。
- 5 类（Cat 5）：可传输高达 100 MHz 频率信号的电缆。Cat 5 电缆通常具有四对铜线。Cat 5 UTP 是当今新安装中最流行的电缆。该类别的电缆正在被 5e 类（增强型 Cat 5）取代。
- 5e 类（Cat 5e）：与 Cat 5 类似，但技术参数有所改进，例如近端串扰和衰减。Cat 5e 电缆支持 10BaseT、100BaseT4、100BaseT2、100BaseTX 和 1000BaseT 以太网。如今，Cat 5e 是最低可接受的布线。
- 6 类（Cat 6）：与 Cat 5e 类似，但能够传输高达 250 MHz 频率的信号。Cat 6 电缆支持所有现有以太网标准，并且还支持千兆以太网标准 1000BaseTX，该标准在每个方向上使用两对线，而不是像 Cat 5e 电缆上的 1000BaseT 以太网那样使用所有四对线。

![](img/11709a8f88c8cd03868a929dc94c0e2b_306_2.png)

要设置 10BaseT 或 100BaseT 以太网网络，你需要一个以太网集线器——一个带有 RJ-45 插孔的硬件盒。（这些插孔看起来像大的电话插孔。）你通过从每台 PC 的以太网卡到该集线器铺设双绞线（通常是 5 类电缆）来构建网络。你可以花大约 40 美元购买一个 4 端口的 10BaseT/100BaseT 集线器。图 2.2 展示了一个典型的中小型 10BaseT/100BaseT 以太网局域网，你可能在小办公室或家中设置它。

当你安装本书配套 DVD-ROM 中的任何 Linux 发行版时，如果连接到带有以太网卡的 PC 上，Linux 内核会自动检测以太网卡并安装相应的驱动程序。安装程序还允许你设置 TCP/IP 网络。

Linux 内核每次启动时都会加载以太网卡的驱动程序。要验证以太网驱动程序是否已加载，请在终端窗口中输入以下命令：

```
dmesg | grep eth0
```

图 2-2：
你可以使用以太网集线器来设置 10BaseT/100BaseT 以太网局域网。

![](img/11709a8f88c8cd03868a929dc94c0e2b_308_0.png)

在我的某台 Linux PC 上，当我输入该命令时，我得到以下输出：

```
eth0: RealTek RTL8139 at 0xf0e20000, 00:0c:76:f4:38:i83, IRQ 161
eth0: Identified 8139 chip type 'RTL-8101'
eth0: link up, 100Mbps, full-duplex, lpa 0x45e1
eth0: no IPv6 routers present
```

你应该看到类似的内容，显示你的以太网卡名称及其他相关信息。

####### 配置 TCP/IP 网络

当你在安装 Linux 期间设置 TCP/IP 网络时，安装程序会使用你提供的信息准备所有适当的配置文件。这意味着你通常不需要手动配置网络。然而，大多数 Linux 发行版都附带用于配置网络设备的图形用户界面工具，以防需要更改某些设置。本节中我描述了一些特定发行版的示例。对于所有其他发行版，步骤都类似。

![](img/11709a8f88c8cd03868a929dc94c0e2b_309_0.png)

Fedora Core 附带一个图形网络配置工具，你可以用它来添加新的网络接口或修改名称服务器和主机名等信息。要启动图形网络配置工具，请选择**系统**→**管理**→**网络**。如果你没有以*root*用户登录，系统会提示你输入*root*密码。网络配置工具显示一个带选项卡对话框，如**图 2-3**所示。然后，你可以通过对话框顶部显示的四个选项卡来配置网络。配置好网卡后，你可以选中该设备并点击“激活”按钮来开启以太网。

![](img/11709a8f88c8cd03868a929dc94c0e2b_309_1.png)

在大多数情况下，你可以设置网卡以自动获取 IP 地址（当以太网卡连接到 DSL 或电缆调制解调器时即为这种情况），方法是使用 DHCP。如果你的网络没有 DHCP 服务器（通常内置于路由器中），你必须为网卡指定一个 IP 地址。如果你运行的是私有网络，可以使用 192.168.0.0 到 192.168.255.255 范围内的 IP 地址。（其他地址范围也保留用于私有网络，但对于大多数需求而言，此范围已足够。）

![](img/11709a8f88c8cd03868a929dc94c0e2b_309_2.png)

在**SUSE**中，选择**主菜单**→**系统**→**YaST** 以打开 YaST 控制中心。在提示时输入*root*密码。然后选择窗口左侧的“网络设备”和右侧的“网卡”。YaST 随后会弹出一个窗口（如**图 2-4**所示），其中包含已配置的网卡信息以及它检测到的任何新网卡的信息。然后，你可以配置任何新的网卡。

![](img/11709a8f88c8cd03868a929dc94c0e2b_309_3.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_309_4.png)




![](img/11709a8f88c8cd03868a929dc94c0e2b_310_0.png)

**图 2-4：** 在 SUSE 中，使用 YaST 配置以太网网络。

###### 将局域网连接到互联网

如果你有一个包含多台 PC 的局域网（LAN），你可以使用 DSL 或有线调制解调器将整个局域网连接到互联网。基本上，你可以让局域网中的所有 PC 共享高速 DSL 或有线调制解调器连接。

在本小书的第一章中，我解释了如何设置 DSL 或有线调制解调器。在本节中，我简要说明了如何将局域网连接到互联网，以便所有 PC 都能访问互联网。

通过 DSL 或有线调制解调器将局域网连接到互联网最方便的方法是购买一种名为*DSL/有线调制解调器 NAT 路由器*的硬件设备，它带有 4 口或 8 口以太网集线器。NAT 代表网络地址转换（Network Address Translation），NAT 路由器可以将许多私有 IP 地址转换为一个外部已知的 IP 地址。以太网集线器部分对你来说表现为若干个 RJ-45 以太网端口，你可以将 PC 连接到这些端口以设置局域网。换句话说，除了 DSL 或有线调制解调器之外，你只需要额外购买一个盒子。

图 2-5 展示了如何通过内置以太网集线器的 NAT 路由器将局域网连接到互联网。当然，要使此方案正常工作，你需要 DSL 或有线调制解调器的连接，并且你必须向电话公司注册 DSL 服务，或向有线电视提供商注册有线互联网服务。

当你将局域网连接到互联网时，NAT 路由器充当你局域网的网关。NAT 路由器还动态地为局域网中的 PC 提供 IP 地址。因此，在每台 PC 上，你必须设置网络选项以动态获取 IP 地址。

![](img/11709a8f88c8cd03868a929dc94c0e2b_311_0.png)

你的局域网可以混合使用各种类型的计算机：有些可能运行 Linux，有些可能运行 Microsoft Windows 或其他支持 TCP/IP 的操作系统。在配置网络设置时，请记住选择启用 Linux 通过 DHCP 自动获取 IP 地址设置和 DNS 信息的选项。

![](img/11709a8f88c8cd03868a929dc94c0e2b_311_1.png)

*图 2-5：* 通过内置以太网集线器的 NAT 路由器将局域网连接到互联网。

- 局域网（LAN）中的 PC。每台 PC 必须有一张 10BaseT 以太网卡。
- 以太网线缆（10BaseT）
- 有线或 DSL 调制解调器
- NAT 路由器和以太网集线器
- 以太网线缆（10BaseT）

##### 第 3 章：添加无线以太网局域网

*本章内容*

- 理解无线以太网网络
- 设置无线硬件
- 配置无线网络

如果你的局域网上有笔记本电脑——或者你不希望整理一团乱麻般的线缆来将 PC 连接到局域网——你可以选择使用无线以太网网络。在典型场景中，你有通过有线或 DSL 连接互联网的途径，并希望连接一台或多台带有无线网卡的笔记本电脑，以便通过有线或 DSL 调制解调器访问互联网。本章将向你展示如何设置无线网络以连接到以太网局域网并访问互联网。

###### 理解无线以太网网络

你可能已经听说过 Wi-Fi。Wi-Fi 代表*无线保真*（Wireless Fidelity）网络——一种类似于有线以太网网络的短距离无线网络。一个名为*IEEE*（电气电子工程师学会）的组织制定了一系列标准，定义了 Wi-Fi 网络工作原理的技术细节。制造商使用这些标准制造组件，你可以购买这些组件来设置无线网络，简称 WLAN。

直到 2003 年中，两个流行的 IEEE 标准——802.11a 和 802.11b——用于无线以太网网络。这两个标准在 1999 年最终确定。第三个标准——802.11g——由 IEEE 在 2003 年夏季最终确定。所有这些标准都规定了无线以太网网络在物理层的工作方式。你不需要纠结于设置无线网络的所有标准细节，但了解一些相关细节有助于你为无线网络购买合适的设备。

三种无线以太网标准具有以下主要特征：

- **802.11b**：在 2.4 GHz 频段（2.4 GHz 至 2.4835 GHz）内运行，最多有三个非重叠的频段或信道。支持每信道最大 11 Mbps 的比特率。802.11b 的一个缺点是 2.4 GHz 频段非常拥挤——许多设备（如微波炉、无绳电话、医疗和科学设备，以及蓝牙设备）都在 2.4 GHz 频段内工作。尽管如此，802.11b 在企业网络和家用网络中非常流行。
- **802.11a**：在 5 GHz 频段（5.725 GHz 至 5.850 GHz）内运行，最多有八个非重叠信道。支持每信道最大 54 Mbps 的比特率。5 GHz 频段不像 2.4 GHz 频段那样拥挤，但 5 GHz 频段在欧洲并未获准使用。符合 802.11a 标准的产品已上市，一些无线接入点被设计为同时处理 802.11a 和 802.11b 连接。
- **802.11g**：在 2.4 GHz 频段支持高达 54 Mbps 的数据速率。（这是 802.11b 使用的同一频段。）802.11g 通过使用一种称为*OFDM*（正交频分复用）的技术实现更高的比特率，该技术也用于 802.11a。符合 802.11g 的设备已上市。802.11g 因其工作在 802.11b 相同的频段但承诺提供高得多的数据速率，并且向后兼容 802.11b 设备，从而引发了人们的激动情绪。供应商目前提供可以支持 802.11b 和 802.11g 连接标准的接入点。

在所有情况下，用户实际看到的最大数据吞吐量要低得多，因为使用该无线电频段的所有用户共享该频段的容量。此外，随着用户 PC 与无线接入点之间距离的增加，数据传输率会降低。

正在开发的第三个标准——802.11n——支持在 2.4 GHz 或 5 GHz 频段中达到 100 Mbps 的数据速率，具体取决于这两个提案中哪一个获得所需的成员批准。两个实力相当的公司组——分别被称为 TGn Sync（n 任务组同步）和 WWISE（全球频谱效率）——各自起草了 802.11n 标准的提案。TGn Sync 提议使用 5 GHz 频段，即 802.11a 使用的频段，而 WWiSE 的提案是针对 802.11b 和 g 使用的 2.4 GHz 频段。两个组都同意，需要某种形式的多输入多输出（MIMO，发音为 *MY-mo*）天线技术来实现 100 Mbps 的数据速率。（一些 MIMO 接入点已开始在市场上提供。）在 2005 年 5 月的投票中，TGn Sync 提案获得了多数票，但未获得成为第一版草案基础所需的 75% 票数。你可以在 http://grouper.ieee.org/groups/802/11/Reports/tgn_update.htm 阅读关于 IEEE 802.11n 项目的最新消息。

![](img/11709a8f88c8cd03868a929dc94c0e2b_314_0.png)

如果你正在购买新的无线接入点，请购买一个 802.11g 接入点。802.11g 接入点也可以与较旧（且较慢）的 802.11b 设备通信。你还可以考虑支持多个 802.11 标准并实施技术以获得更高吞吐量和更好范围的 MIMO 接入点。

![](img/11709a8f88c8cd03868a929dc94c0e2b_314_1.png)

要了解有关无线以太网的更多信息，请访问 www.wi-fi.org，这是 Wi-Fi 联盟的主页，该联盟是一个非营利国际协会，成立于 1999 年，旨在基于 IEEE 802.11 标准认证无线局域网产品的互操作性。

###### 理解基础设施模式和临时模式

802.11 标准为无线以太网网络定义了两种操作模式：临时模式（ad hoc）和基础设施模式（infrastructure）。临时模式仅仅是两个或更多无线以太网卡在没有接入点的情况下相互通信。

基础设施模式指的是所有无线以太网卡通过接入点相互通信并与有线局域网通信的方法。在本章的讨论中，我假设你将无线以太网卡设置为基础设施模式。在配置文件中，此模式被称为受管理模式（managed mode）。

###### 理解有线等效保密（WEP）

802.11 标准包括有线等效保密（WEP），用于保护无线通信免受窃听。WEP 依赖于一个在移动站（如带有无线以太网卡的笔记本电脑）和接入点（也称为基站）之间共享的 40 位或 104 位密钥。该密钥用于在传输前加密数据包，并且执行完整性检查以确保数据包在传输过程中未被修改。802.11 标准没有解释共享密钥是如何建立的。在实践中，大多数无线局域网使用所有移动站和接入点共享的一个密钥。然而，这种方法在诸如大学校园这样的环境中扩展性不好，因为密钥与所有用户共享——你知道，如果你与几百人共享秘密会怎样。这就是为什么通常不在大型无线网络（如大学中的那些）上使用 WEP。在这样的无线网络中，你必须使用其他安全措施，如 SSH（安全外壳），来登录远程系统。然而，WEP 在你的家用无线网络上使用是很好的选择。





###### WEP 流密码是否足够安全？

WEP 使用 RC4 加密算法，该算法被称为流密码。此类算法的工作原理是：获取一个短的秘密密钥，并生成一条无限的伪随机位流。在发送数据之前，发送站对伪随机位和代表数据包的位执行异或（exclusive-OR）运算，当两位不同时结果为 1，相同则为 0。接收方拥有相同的秘密密钥副本，生成一条相同的伪随机位流——并对该伪随机流和接收到的位执行相同的异或运算。这样做可以重新生成原始的未加密数据包。

这种流密码方法存在一些问题。如果加密数据流中的某一位被翻转（从 0 变为 1 或反之），解密输出中对应的位也会被翻转，这可能帮助攻击者推导出加密密钥。此外，窃听者如果拦截到两条使用相同流编码的消息，可以生成原始消息的异或值。这一知识足以发起最终能破解加密的攻击。

为了对抗这些弱点，WEP 使用了一些防御措施：

-   **完整性校验（IC）字段**：为了确保数据包在传输过程中不被篡改，WEP 在每个数据包中使用了一个完整性校验字段。
-   **初始化向量（IV）**：为了避免使用相同的密钥流加密两条消息，WEP 使用一个 24 位 IV，该 IV 与共享秘密密钥结合，为每个数据包产生不同的 RC4 密钥。IV 本身也包含在数据包中。

专家认为这两种防御措施都实现得不够好，导致 WEP 无效。IC 和 IV 存在两个主要问题：

-   完整性校验字段通过使用一种名为 32 位循环冗余码（CRC-32）的校验和算法来实现；该校验和随后作为数据包的一部分包含在内。不幸的是，攻击者可以翻转加密消息中的任意位，并正确调整校验和，使得结果消息看起来是有效的。
-   24 位 IV 是明文（未加密）发送的。只有 $2^{24}$ 个可能的初始化向量（对于快速机器来说这并非什么挑战），并且在遍历完所有向量后必须重新使用它们。换句话说，在发送 $2^{24}$ 即 16,777,216 个数据包后，IV 会重复。这个数字听起来很多，但请考虑一个繁忙接入点以 11 Mbps 速率发送 1,500 字节数据包的情况。每个数据包有 8 × 1,500 = 12,000 位。这意味着每秒该接入点发送 11,000,000/12,000 = 916 个数据包。以该速率，接入点在 16,777,216/916 = 18,315 秒或 5 小时内发送 16,777,216 个数据包。这意味着 IV 在 5 小时后重用，而且由于许多消息小于 1,500 字节，时间可能更短。因此，攻击者有充分的机会收集两条使用相同密钥流加密的消息——并执行统计攻击（实际上就是以极快的速度尝试可能的组合）来解密消息。

WEP 有其弱点，但它总比没有好。你可以在较小的无线局域网中使用它，在这些网络中，在所有无线站点间共享相同密钥并非艰巨任务。

> **记住**
>
> 正在开展提供比 WEP 更好的无线网络安全工作。2003 年，Wi-Fi 联盟发布了一项名为*Wi-Fi 保护访问*（WPA）的规范，该规范取代了现有的 WEP 标准，并通过做出一些更改提高了安全性。例如，与使用固定密钥的 WEP 不同，WPA 标准使用*临时密钥完整性协议*（TKIP），它会根据网络上每 10K 传输的数据生成新密钥。这使得 WPA 更难被破解。2004 年，Wi-Fi 联盟推出了 WPA 的后续版本，称为*Wi-Fi 保护访问 2*（WPA2——WPA 安全的第二代）。WPA2 基于最终的 IEEE 802.11i 标准，该标准使用带数字证书的公钥加密以及远程认证拨号用户服务（RADIUS）的身份验证、授权和计费服务器，为无线以太网网络提供更好的安全性。WPA2 使用高级加密标准（AES）进行数据加密。

###### 设置无线硬件

要设置无线连接，你需要一个无线接入点和每个 PC 中的一块无线网络卡。你也可以在两个或更多装有无线网络卡的 PC 之间设置自组网（ad hoc）无线网络，但这仅在这些 PC 之间是一个独立的无线局域网。在本节中，我专注于你想将无线连接到通过电缆调制解调器或 DSL 连接到互联网的一个现有有线局域网的场景。

除了无线接入点外，你还需要连接到互联网的电缆调制解调器或 DSL 连接，以及如本小册子前几章所述的 NAT 路由器和集线器。图 3-1 展示了通过现有电缆调制解调器或 DSL 连接访问无线互联网的典型设置。

如图 3-1 所示，局域网既有有线 PC 也有无线 PC。在此示例中，电缆或 DSL 调制解调器通过 NAT 路由器和集线器将局域网连接到互联网。装有无线网络卡的笔记本电脑通过连接到集线器上其中一个 RJ-45 端口的无线接入点连接到局域网。要将台式机连接到此无线网络，你可以使用 USB 无线网络卡（连接到 USB 端口）。

> **提示**
>
> 如果你尚未为电缆或 DSL 连接购买 NAT 路由器和集线器，可以考虑购买内置无线接入点的路由器和集线器。

![](img/11709a8f88c8cd03868a929dc94c0e2b_316_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_316_1.png)

###### 配置无线接入点

![](img/11709a8f88c8cd03868a929dc94c0e2b_317_0.png)

**图 3-1：** 混合有线和无线以太网局域网连接到互联网的典型连接。

局域网（LAN）中的 PC。每个 PC 必须有一块 10BaseT 以太网卡。

配置无线接入点涉及以下任务：

-   为无线网络设置名称。（技术术语为 ESSID。）
-   设置无线接入点与无线网络卡通信的频率或信道。接入点和卡必须使用相同的信道。
-   决定是否使用加密。
-   如果打算使用加密，设置加密密钥中的位数和加密密钥的值。对于加密密钥，24 位位于接入点内部；你只需指定剩余的位。因此，对于 64 位加密，你需要指定一个 40 位密钥，即 10 个十六进制位。(*十六进制位* 是 0-9 的整数或 A-F 中的字母) 对于 128 位加密密钥，你指定 104 位，即 26 个十六进制位。
-   设置无线网络卡在连接到接入点时必须使用的访问方法。你可以选择开放访问或共享密钥。开放访问方法是典型的（即使在使用加密时也是）。
-   将无线接入点设置为运行在基础设施（管理）模式（因为这是你将无线网络卡连接到现有以太网局域网的方式）。

**记住**

配置无线接入点的具体方法取决于制造商和型号；供应商提供了配置无线接入点的说明。通常，你通过在 Windows PC 上操作图形客户端应用程序来完成配置。如果你启用加密，请记下加密密钥；你需要为笔记本电脑或台式机上的每个无线网络卡指定相同的密钥。

###### 配置无线组网

在你的 Linux 笔记本电脑上，PCMCIA 或 PC 卡管理器识别无线网络卡并为该卡加载相应的驱动程序。Linux 将无线网络卡视为另一个以太网设备，并为其分配诸如 *eth0* 或 *eth1* 的设备名称。如果笔记本电脑中已经有一块以太网卡，该卡将获得 *eth0* 设备名称，而无线 PC 卡将成为 *eth1* 设备。

你确实需要配置某些参数，以便无线网络卡能与无线接入点通信。例如，你必须指定分配给接入点的无线网络名称，并且加密设置必须与接入点上的设置匹配。通常，你可以使用针对你的 Linux 发行版可用的图形网络配置工具来配置所有内容——只需选择无线网络选项并填写所需信息即可。

**发行版特定说明**

例如，在 Fedora Core 中，从 GNOME 桌面选择 系统→管理→网络。然后点击工具栏上的 *New*（新建）以添加网络设备。然后你可以选择无线设备，进入一个窗口，在那里你可以配置无线连接。（见图 3-2。）特别是，将模式设置为*管理*（Managed），指定无线网络的名称（那个



（连接至）目标网络，并设置加密密钥（如果有的话）。您可以将获取 IP 地址的选项设置为 DHCP（一种用于从网络上的服务器获取网络配置参数，包括 IP 地址的协议）。完成设置后，返回到网络配置工具的主窗口，选择新的无线设备并点击“激活”按钮。如果一切顺利，无线网络将在几秒钟内启动并运行。

![](img/11709a8f88c8cd03868a929dc94c0e2b_319_0.png)

**图 3-2：在 Fedora Core 中，从此窗口配置无线连接。**

在 Fedora Core 中，网络配置工具会将您的无线网络设置保存到一个文本文件中。该文本文件的名称取决于无线网络设备名称。如果无线网络设备名称为 `eth0`，则配置存储在文本文件 `/etc/sysconfig/network-scripts/ifcfg-eth0` 中。如果无线设备名称为 `eth1`，则该文件为 `/etc/sysconfig/network-scripts/ifcfg-eth1`。此配置文件包含无线网卡的多种设置。**表 3-1** 解释了这些设置的含义。以下是我运行 Fedora Core 的笔记本电脑中 `/etc/sysconfig/network-scripts/ifcfg-eth1` 文件的一个略作修改的版本：

```
IPV6INIT=no
USERCTL=no
PEERDNS=yes
TYPE=Wireless
DEVICE=eth1
HWADDR=00:02:2d:8c:f9:c4
BOOTPROTO=dhcp
ONBOOT=no
DHCP_HOSTNAME=
NAME=
ESSID='HOME'
CHANNEL=6
MODE=Managed
RATE=auto
```

在 Fedora Core 中，加密密钥是单独存储的。对于设备名称为 `eth1` 的无线以太网卡，加密密钥存储在 `/etc/sysconfig/network-scripts/keys-eth1` 文件中。例如，以下是我示例中该文件包含的内容：

```
KEY=1fdf3fdefe
```

- **技术细节**
  请注意，对于 40 位密钥，密钥包含 10 个十六进制数字（例如，`1fdf-3fde-fe`）；而对于 104 位密钥，则包含 26 个十六进制数字。实际上，密钥长度分别为 64 位和 128 位，但加密算法会自动生成密钥中的 24 位，因此您只需指定其余部分。不用说，密钥越长，加密越安全。

- **请记住**
  如果您在 Fedora Core 中手动编辑无线以太网配置文件中的参数，请在编辑配置文件后输入以下命令以重新激活无线网络接口：

```
/etc/init.d/network restart
```

####### 表 3-1：Fedora Core 中无线以太网网络接口配置文件中的设置

| 此参数 | 含义 |
| :--- | :--- |
| **BOOTPROTO** | 用于获取接口 IP 地址的协议名称。对于以太网接口，它是 `dhcp` 或 `bootp`。 |
| **CHANNEL** | 信道号（在美国和加拿大之间为 1 到 14）。必须与为无线接入点设置的相同。在管理模式下，您无需指定信道。 |
| **DEVICE** | 无线以太网网络接口的设备名称（第一个接口为 `eth0`，第二个为 `eth1`，等等）。 |
| **ESSID** | 扩展服务集（ESS）标识符，也称为无线网络名称。它区分大小写，必须与为无线接入点指定的名称相同。请在单引号内提供该名称（例如，'HOME'）。 |
| **HWADDR** | 无线网卡的硬件地址（也称为 MAC 地址，由六组冒号分隔的十六进制数字组成；例如，00:02:2d:8c:f9:c4）。无线网卡的设备驱动程序会自动检测此地址。 |
| **IPV6INIT** | 当设置为 yes 时，此参数为无线接口初始化 IPv6 配置。如果未使用 IPv6，请将其设置为 no。 |
| **MODE** | 无线网卡的工作模式。对于通过无线接入点连接的典型网络，请设置为 Managed。 |
| **NAME** | 无线网络的昵称。如果未指定，则使用主机名作为昵称。 |
| **ONBOOT** | 设置为 yes 以在启动时激活无线接口；否则，设置为 no。 |
| **PEERDNS** | 设置为 yes 以启用接口修改系统的 `/etc/resolv.conf` 文件，使用从 DHCP 服务器获取的 DNS 服务器（该服务器也提供接口的 IP 地址）。如果将此参数设置为 no，则 `/etc/resolv.conf` 文件保持不变。 |
| **RATE** | 无线连接的比特率（设置为以下选项之一：1M、2M、5.5M、11M 或 auto）。M 表示 Mbps 或每秒百万比特。设置为 auto 以使用最大的可能传输速率。 |
| **TYPE** | 对于无线网络接口，设置为 Wireless。 |
| **USERCTL** | 当设置为 yes 时，非 root 用户可以控制该设备。请将其设置为 no，以便只有 root 可以控制该设备。 |

在 SUSE Linux 中，使用 YaST 配置无线网络。SUSE 将无线配置参数存储在一个以 ifcfg-wlan 开头、后接数字（如 0 或 1，具体取决于无线网络接口的序列号）的文件中。配置文件存储在 /etc/sysconfig/network 目录中。以下是 SUSE Linux 配置文件中典型的无线配置参数列表：

```
WIRELESS_MODE='Managed'
WIRELESS_ESSID='HOME'
WIRELESS_NICK='
WIRELESS_RATE='auto'
WIRELESS_AUTH_MODE='open'
WIRELESS_KEY_0='0123-4567-89'
```

要检查无线网络接口的状态，请输入以下命令：

```
iwconfig
```

以下是来自一台装有无线以太网 PC 卡的 Fedora Core 笔记本电脑的典型输出。（在其他 Linux 发行版中，输出应该类似。）

```
lo no wireless extensions.

eth0 no wireless extensions.

sit0 no wireless extensions.

eth1 IEEE 802.11b ESSID: 'HOME' Nickname: 'localhost.localdomain' Mode:Managed Frequency:2.437 GHz Access Point: 00:30:AB:06:E2:5D Bit Rate:11 Mb/s Sensitivity:1/3 Retry limit:4 RTS thr:off Fragment thr:off Encryption key:1FDF-3FDE-FE Security mode:open Power Management:off Link Quality=51/92 Signal level=-40 dBm Noise level=-91 dBm Rx invalid nwid:0 Rx invalid crypt:0 Rx invalid frag:27 Tx excessive retries:0 Invalid misc:0 Missed beacon:0
```

在这里，`eth1` 接口指的是无线网卡。我编辑了加密密钥和其他一些参数以隐藏这些细节，但示例输出展示了当无线链路正常工作时您通常看到的内容。

##### 第 4 章：管理网络

###### 本章内容

- 学习 TCP/IP 配置文件
- 检查 TCP/IP 网络
- 在启动时配置网络

与 Linux 中的几乎所有其他内容一样，TCP/IP 设置涉及准备大量配置文件（您可以使用任何文本编辑器编辑的文本文件）。其中大多数配置文件位于 /etc 目录中。Linux 安装程序试图通过隐藏 TCP/IP 配置文件的细节来提供帮助。然而，如果您知道这些文件的名称及其用途，那么在必要时手动编辑这些文件会更轻松。

###### 发现 TCP/IP 配置文件

在安装 Linux 时可以配置 TCP/IP 网络。但是，如果您想有效地管理网络，您需要熟悉 TCP/IP 配置文件，以便在必要时编辑这些文件。（例如，如果您想检查名称服务器是否正确指定，您必须了解 /etc/resolv.conf 文件，该文件存储名称服务器的 IP 地址。）

表 4-1 总结了基本的 TCP/IP 配置文件。我将在接下来的几个部分中描述这些配置文件。

####### 表 4-1：基本 TCP/IP 网络配置文件

| 此文件 | 包含以下内容 |
| :--- | :--- |
| /etc/hosts | 本地网络的 IP 地址和主机名，以及您经常访问的其他系统 |
| /etc/networks | 网络的名称和 IP 地址 |
| /etc/host.conf | 如何翻译主机名为 IP 地址的说明 |
| /etc/resolv.conf | 名称服务器的 IP 地址 |
| /etc/hosts.allow | 哪些系统可以访问您系统上 Internet 服务的说明 |
| /etc/hosts.deny | 必须拒绝哪些系统访问您系统上 Internet 服务的说明 |
| /etc/nsswitch.conf | 如何翻译主机名为 IP 地址的说明 |





###### /etc/hosts

*etc/hosts* 文本文件包含本地网络的 IP 地址和主机名列表。在没有名称服务器的情况下，系统中的任何网络程序都会参考此文件来确定与主机名对应的 IP 地址。你可以将 /etc/hosts 视为本地电话簿，你可以在其中查找本地主机的 IP 地址（而非电话号码）。

以下是某个系统的 /etc/hosts 文件，显示了典型局域网中其他主机的 IP 地址和名称：

```
127.0.0.1 localhost localhost.localdomain
# Other hosts on the LAN
192.168.0.100 lnbp933
192.168.0.50 lnbp600
192.168.0.200 lnbp200
192.168.0.233 lnbp233
192.168.0.40 lnbp400
```

如示例所示，文件中的每一行都以 IP 地址开头，后跟该 IP 地址的主机名。（对于给定的 IP 地址，你可以拥有多个主机名。）

###### /etc/networks

/etc/networks 是另一个包含网络名称和 IP 地址的文本文件。这些网络名称通常用于路由命令 (/sbin/route) 中，通过名称而非 IP 地址来指定网络。

如果你的 Linux 电脑没有 /etc/networks 文件，请不要惊慌。没有此文件，你的 TCP/IP 网络也能正常工作。事实上，Linux 安装程序不会创建 /etc/networks 文件。

###### /etc/host.conf

Linux 使用一个名为*解析器库*（resolver library，即一组计算机代码）的特殊*库*来获取与主机名对应的 IP 地址。/etc/host.conf 文件指定名称如何被*解析*（即将名称转换为数字 IP 地址的过程）。典型的 /etc/host.conf 文件可能包含以下行：

```
order hosts, bind
multi on
```

/etc/host.conf 文件中的条目告诉解析器库使用哪些*服务*（以及以何种顺序）来解析名称。

order 选项指示服务的顺序。示例条目告诉解析器库首先参考 /etc/hosts 文件，然后检查名称服务器以解析名称。

![](img/11709a8f88c8cd03868a929dc94c0e2b_326_0.png)

使用 multi 选项指示 /etc/hosts 文件中的主机是否可以拥有多个 IP 地址。拥有多个 IP 地址的主机被称为多宿主（multihomed），因为多个 IP 地址的存在意味着该主机拥有多个网络接口。（实际上，该主机同时位于多个网络中。）

###### /etc/resolv.conf

/etc/resolv.conf 文件是解析器——用于确定主机名 IP 地址的库——使用的另一个文本文件。以下是 /etc/resolv.conf 文件的示例：

```
nameserver 192.168.0.1 # dhcp: eth0
search nrockv01.md.comcast.net
```

nameserver 行提供你域的名称服务器的 IP 地址。如果你有多个名称服务器，请在单独的行上列出它们。它们将按在文件中出现的顺序进行查询。

search 行告诉解析器如何搜索主机名。例如，当试图定位主机名 myhost 时，示例中的 search 指令会使解析器依次尝试 myhost, nrockv01.md.comcast.net, myhost.md.comcast.net, myhost.comcast.net，最后尝试 myhost.md.comcast.net。如果你的网络没有名称服务器，你可以安全地忽略此文件。即使你可能无法通过名称引用主机（除了列在 /etc/hosts 文件中的主机），TCP/IP 仍然可以正常工作。

![](img/11709a8f88c8cd03868a929dc94c0e2b_326_1.png)

第三卷
第四章
管理网络

###### /etc/hosts.allow

/etc/hosts.allow 文件指定哪些主机可以使用你系统上运行的 Internet 服务（如 TELNET 和 FTP）。此文件在特定的 Internet 服务启动之前会被参考。只有当 hosts.allow 文件中的条目表明请求主机被允许使用这些服务时，服务才会启动。

/ hosts.allow 中的条目采用 服务器名:IP地址 的形式，其中“服务器”指的是提供特定 Internet 服务的程序名称，而“IP 地址”识别被允许使用该服务的主机。例如，如果你希望本地网络（网络地址为 192.168.0.0）中的所有主机访问 TELNET 服务（由 in.telnetd 程序提供），请在 /etc/hosts.allow 文件中添加以下行：

```
in.telnetd:192.168.0.
```

如果你希望让所有本地主机访问所有 Internet 服务，可以使用 **ALL** 关键字并将该行重写为：

```
ALL:192.168.0.
```

最后，若要向所有主机开放所有 Internet 服务，你可以将 IP 地址替换为 **ALL**，如下所示：

```
ALL:ALL
```

你也可以使用主机名代替 IP 地址。

![](img/11709a8f88c8cd03868a929dc94c0e2b_327_0.png)

要查找 `/etc/hosts.allow` 文件条目的详细语法，请在终端窗口的 shell 提示符下输入 **man hosts.allow**。

###### /etc/hosts.deny

该文件正好与 `/etc/hosts.allow` 相反。**而** `hosts.allow` 指定哪些主机可以访问你系统上的 Internet 服务（如 TELNET 和 TFTP），`hosts.deny` 文件则识别必须拒绝服务的主机。如果 `/etc/hosts.allow` 文件中没有适用于请求主机的规则，系统会参考 `/etc/hosts.deny` 文件。如果 `hosts.deny` 文件中有适用于该主机的规则，则服务将被拒绝。

`/etc/hosts.deny` 文件中的条目具有与 `/etc/hosts.allow` 文件相同的格式；它们采用 *服务器*:`IP 地址` 的形式，其中 *服务器* 指的是提供特定 Internet 服务的程序名称，而 *IP 地址* 识别不允许使用该服务的主机。

如果你已经在 `/etc/hosts.allow` 文件中设置了条目以允许特定主机访问，你可以将以下行放置在 `/etc/hosts.deny` 文件中，以拒绝其他所有主机访问你系统上的任何服务：

```
ALL:ALL
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_327_1.png)

要查找 `/etc/hosts.deny` 文件条目的详细语法，请在终端窗口的 shell 提示符下输入 **man hosts.deny**。

###### /etc/nsswitch.conf

该文件被称为*名称服务开关*（NSS）文件，它指定解析器库、NIS、NIS+ 和本地配置文件（如 `/etc/hosts` 和 `/etc/shadow`）等服务如何交互。

NIS 和 NIS+ 是*网络信息系统*——另一种类型的名称查找服务。较新版本的 Linux 内核使用 `/etc/nsswitch.conf` 文件来确定优先顺序：是本地配置文件、服务（如 DNS 域名服务）还是 NIS。

作为一个例子，/etc/nsswitch.conf 文件中的以下 hosts 条目表示解析器库首先尝试 /etc/hosts 文件，然后尝试 NIS+，最后尝试 DNS：

hosts: files nisplus dns

![](img/11709a8f88c8cd03868a929dc94c0e2b_328_0.png)

你可以在终端窗口中输入 **man nsswitch.conf** 来了解有关 /etc/nsswitch.conf 文件的更多信息。

###### 检查 TCP/IP 网络

在配置好以太网和 TCP/IP 之后（无论是在安装 Linux 期间，还是之后运行网络配置工具或命令），你可以无障碍地使用各种网络应用程序。万一你遇到问题，Linux 包含一些工具帮助你监控和诊断问题。

####### 检查网络接口

使用 `/sbin/ifconfig` 命令查看当前配置的网络接口。`ifconfig` 命令用于配置网络接口（即将 IP 地址与网络设备关联）。如果你不带任何命令行参数运行 `ifconfig`，该命令将显示当前网络接口的信息。以下是输入 `/sbin/ifconfig` 时的典型输出：

```
eth0      Link encap:Ethernet  HWaddr 00:08:74:85:C1:60
          inet addr:192.168.0.7  Bcast:192.168.0.255  Mask:255.255.255.0
          inet6 addr: fe80::208:74ff:fe85:c160/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:612851 errors:0 dropped:0 overruns:0 frame:0
          TX packets:574197 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:99834031 (95.2 MiB)  TX bytes:76034821 (72.5 MiB)
          Interrupt:10 Base address:0x3000

eth1      Link encap:Ethernet  HWaddr 00:02:2D:8C:F8:C5
          inet addr:192.168.0.9  Bcast:192.168.0.255  Mask:255.255.255.0
          inet6 addr: fe80::202:2dff:fe8c:f8c5/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:0
          RX packets:3833 errors:0 dropped:0 overruns:0 frame:0
          TX packets:1242 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:560194 (547.0 KiB)  TX bytes:250287 (244.4 KiB)
          Interrupt:3 Base address:0x100

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:2456 errors:0 dropped:0 overruns:0 frame:0
          TX packets:2456 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:2891581 (2.7 MiB)  TX bytes:2891581 (2.7 MiB)
```





该输出表明，当前系统上有三个网络接口处于活动状态——即回环接口（*lo*）和两块以太网网卡（*eth0* 和 *eth1*）。对于每个接口，您可以查看其 IP 地址，以及有关已交付和已发送数据包的统计数据。如果 Linux 系统已建立拨号 PPP 链路并正在运行，您还将在输出中看到 *ppp0* 接口的项目。

####### 检查 IP 路由表

另一个网络配置命令 `/sbin/route`，在您不带命令行参数运行它时，也会提供状态信息。如果您在检查与另一台主机（通过 IP 地址指定）的连接时遇到问题，请检查 IP 路由表，查看是否指定了默认网关。然后，检查该网关的路由表，以确保通往外部网络的路径出现在该路由表中。

`/sbin/route` 命令的典型输出如下所示：

```
Kernel IP routing table
Destination    Gateway        Genmask     Flags Metric Ref  Use Iface
               *          0.0.0.0       0.0.0.0     U                   0     0     0 lo
192.168.0.0    *          255.255.255.0 U                   0     0     0 eth0
192.168.0.0    *          255.255.255.0 U                   0     0     0 eth1
169.254.0.0    *          255.255.0.0   U                   0     0     0 eth1
default      192.168.0.1  0.0.0.0       UG                  0     0     0 eth0
```

正如该路由表所示，本地网络使用 *eth0* 和 *eth1* 以太网接口，而默认网关是 *eth0* 以太网接口。默认网关是一种路由设备，它处理发往 Linux 系统所在网络以外的任何网络的数据包。在本例中，发往除以 192.168.0 开头的所有其他网络地址的数据包都会发送到网关——192.168.0.1。该网关将这些数据包转发到其他网络（当然，前提是网关连接到另一个网络，最好是互联网）。

####### 检查与主机的连接

要检查与特定主机的网络连接，请使用 ping 命令。*ping* 是一个广泛使用的 TCP/IP 工具，它使用一系列互联网控制报文协议（ICMP，发音为 *EYE-comp*）消息。ICMP 提供一种回声消息，每台主机都会对此做出响应。通过 ICMP 消息和回复，ping 可以确定另一台系统是否存活，并计算与该系统通信的往返延迟。

以下示例展示了我如何运行 ping 以查看我网络上的某台系统是否存活：

```
ping 192.168.0.1
```

这是该命令在我的家庭网络上显示的内容：

```
PING 192.168.0.1 (192.168.0.1) 56(84) bytes of data.
64 bytes from 192.168.0.1: icmp_seq=1 ttl=63 time=0.256 ms
64 bytes from 192.168.0.1: icmp_seq=2 ttl=63 time=0.267 ms
64 bytes from 192.168.0.1: icmp_seq=3 ttl=63 time=0.272 ms
64 bytes from 192.168.0.1: icmp_seq=4 ttl=63 time=0.267 ms
64 bytes from 192.168.0.1: icmp_seq=5 ttl=63 time=0.275 ms
--- 192.168.0.1 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 3999ms
rtt min/avg/max/mdev = 0.256/0.267/0.275/0.016 ms
```

在 Linux 中，ping 会持续运行，直到您按下 Ctrl+C 停止它；然后它会显示汇总统计信息，表明在两个系统之间发送一个数据包所需的典型时间。在某些系统上，ping 仅报告远程主机处于活动状态。然而，您仍然可以通过使用适当的命令行参数获取计时信息。

![](img/11709a8f88c8cd03868a929dc94c0e2b_330_0.png)

ping 命令依赖于许多防火墙被配置为阻止的 ICMP 消息。因此，ping 并不总是有效，也不再是测试网络连接性的可靠方法。如果针对特定主机的 ping 失败，不要假设该主机已宕机或未连接到网络；通常可以使用 ping 成功检查局域网内的连接性。

####### 检查网络状态

要检查网络状态，请使用 netstat 命令。该命令显示各种类型（如 TCP 和 UDP 连接）的网络连接状态。您可以通过输入 `netstat -i` 快速查看接口的状态，这将产生与以下类似的输出：

```
Kernel Interface table
Iface  MTU Met  RX-ERR RX-DRP RX-OVR  TX-ERR TX-DRP TX-DRP TX-OVR Flg
eth0 1500 0 63175 0 0 1 574695 0 0 0 BMRU
eth1 1500 0 4298 0 0 0 1375 0 0 0 BMRU
lo   16436 0 3255 0 0 0 3255 0 0 0 LRU
```

在此情况下，输出显示回环接口和以太网接口的当前状态。表 4-2 描述了各列的含义。

**第三卷 第4章** 管理网络

| 表 4-2 | 内核接口表中列的含义 |
| --- | --- |
| **列名** | **含义** |
| *Iface* | 接口名称 |
| *MTU* | 最大传输单元——数据包可包含的最大字节数 |
| *Met* | 接口的度量值——路由软件在决定通过哪个接口发送数据包时使用的表示距离（以跳数计）的数字 |
| *RX-OK, TX-OK* | 接收（RX）或传输（TX）的无错误数据包数量 |
| *RX-ERR, TX-ERR* | 包含错误的数据包数量 |
| *RX-DRP, TX-DRP* | 被丢弃的数据包数量 |
| *RX-OVR, TX-OVR* | 因溢出而丢失的数据包数量 |
| *Flg* | A = 接收组播；B = 允许广播；D = 已开启调试；L = 回环接口（注意 lo 上的标志），M = 接收所有数据包，N = 避免尾随头；O = 此接口上没有 ARP；P = 点对点接口；R = 接口正在运行，且 U = 接口已启动 |

*netstat* 选项的另一种有用形式是 `-t`，它显示所有活动的 TCP 连接。以下是在某台 Linux 电脑上键入 *netstat* -t 的典型结果：

```
Active Internet connections (w/o servers)
Proto Recv-Q Send-Q Local Address Foreign Address State
tcp 0 0 localhost:2654 localhost:1024 ESTABLISHED
tcp 0 0 localhost:1024 localhost:2654 ESTABLISHED
tcp 0 0 LMNECXAN.nrokkov01:.ssh 192.168.0.6:1577 ESTABLISHED
```

在此情况下，输出列显示协议（*Proto*）、接收和发送队列中的字节数（*Recv-Q, Send-Q*）、主机名:服务格式下的本地 TCP 端口（*Local Address*）、远程端口（*Foreign Address*）以及连接的状态。

键入 *netstat* -ta 以查看所有 TCP 连接——包括活动的以及您的 Linux 系统正在监听但尚未建立连接的那些。例如，这是 *netstat* -ta 命令的典型输出：

```
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address Foreign Address State
tcp 0 0 *:32769 *:* LISTEN
tcp 0 0 *:mysql *:* LISTEN
tcp 0 0 *:smpnc *:* LISTEN
tcp 0 0 *:ftp *:* LISTEN
tcp 0 0 localhost.localdomain:ipp *:* LISTEN
tcp 0 0 *:telnet *:* LISTEN
tcp 0 0 localhost.localdomain:5335 *:* LISTEN
tcp 0 0 localhost.localdomain:smtop *:* LISTEN
tcp 0 0 192.168.0.9:45876 www.redhat.com:http ESTABLISHED
tcp   0   0 192.168.0.9:45877   www.redhat.com:http
ESTABLISHED
tcp   0   0 192.168.0.9:45875   www.redhat.com:http
ESTABLISHED
tcp   0   0 *:sah   *.*   LISTEN
tcp   0   0 :feff:192.168.0.3:sah :fff:192.168.0.3:4932
ESTABLISHED
```

####### 嗅探网络数据包

嗅探网络数据包——听起来像是某种非法行为，不是吗？并非如此。**嗅探**（Sniffing） simply 指查看 TCP/IP 网络数据包。其概念是捕获所有网络数据包，以便您稍后进行检查。

如果您想嗅探 TCP/IP 数据包，可以使用 **tcpdump**，这是一个随 Linux 提供的命令行实用程序。顾名思义，它**转储**（打印）TCP/IP 网络数据包的头部。

要使用 **tcpdump**，请以 **root** 身份登录，并在终端窗口中输入 **tcpdump** 命令。通常，您希望将输出保存到一个文件中，然后稍后检查该文件。否则，**tcpdump** 会开始吐出结果，这些结果会在窗口上快速闪过。例如，要在名为 **tdout** 的文件中捕获 1,000 个数据包并尝试将 IP 地址转换为名称，请输入以下命令：

```
tcpdump -a -c 1000 > tdout
```

在捕获 1,000 个数据包后，**tcpdump** 退出。然后您可以检查输出文件 **tdout**。它是一个文本文件，因此您可以简单地用文本编辑器打开它，或者键入 **more tdout** 来查看捕获的数据包。

为了激发您的好奇心，以下是 **tcpdump** 典型输出中的几行：

```
20:05:57.723621 arp who-has 192.168.0.1 tell LNR6CXAN.nrcov01.md.comcast.net
20:05:57.723843 arp rep-by 192.168.0.1 ia-at 0:9:5b:64:78:fe
20:06:01.733633 LNR6CXAN.nrcov01.md.comcast.net.1038 > 192.168.0.6.ath: S 53632100:53632100/0 1 win 5840 <mss 1460, sackOK,timestamp 7030060
0,nop,window 0> (DF)
20:06:02.737022 LNR6CXAN.nrcov01.md.comcast.net.ftp > 192.168.0.6.1596: P 1:72 (71) ack 1 win 5840
20:06:02.935335 192.168.0.6.1596 > LNR6CXAN.nrcov01.md.comcast.net.ftp: . ack 72 win 65464 (DF)
20:06:05.462481 192.168.0.6.1596 > LNR6CXAN.nrcov01.md.comcast.net.ftp: P 1:12 (11) ack 72 win 65464 (DF)
20:06:05.462595 LNR6CXAN.nrcov01.md.comcast.net.ftp > 192.168.0.6.1596: . ack 12 win 5840 (DF)
20:06:05.465344 LNR6CXAN.nrcov01.md.comcast.net.ftp > 192.168.0.6.1596: P 72:105(33) ack 12 win 5840 (DF)
. . . lines deleted...
```




输出确实提供了一些关于正在发生的事情的线索：每一行显示关于一个网络数据包的信息。每一行都以时间戳开头，随后是数据包的详细信息（例如来源和去向等信息）。我并没有在此处试图解释这些细节，但你可以通过执行 **man tcpdump** 来了解更多关于部分细节的信息（更重要的是，查看 *tcpdump* 的其他用途）。

![](img/11709a8f88c8cd03868a929dc94c0e2b_333_0.png)

如果在 Debian 中未安装 *tcpdump*，请键入 `apt-get install tcpdump` 进行安装。

在 Linux 中，你可以使用另一种名为 Ethereal 的数据包嗅探器。要了解有关 Ethereal 的更多信息，请访问 `www.ethereal.com`。

###### 在启动时配置网络

每次启动系统时自动启动网络是合乎情理的。要实现这一点，各种启动脚本必须包含相应的命令。除了配置网络（在安装期间或稍后使用网络配置工具）之外，你不需要做其他特殊操作。然而，如果网络在启动时出现异常，你可以通过检查本节中提到的文件来排除故障。

![](img/11709a8f88c8cd03868a929dc94c0e2b_333_1.png)

在 Debian、MEPIS、Ubuntu 和 Xandros 中，`/etc/network/interfaces` 文件描述了系统中可用的网络接口，而 `/sbin/ifup` 命令在系统启动时激活这些接口。以下是来自 Debian 系统的典型 `/etc/network/interfaces` 文件内容：

```bash
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).
# The loopback network interface
auto lo
iface lo inet loopback
# The primary network interface
auto eth0
iface eth0 inet dhcp
```

`auto eth0` 行表示你可以通过使用命令 `ifup -a`（由系统启动脚本调用）在初始化时启用以太网接口。`iface eth0 inet dhcp` 行标识该以太网是一个由动态主机配置协议（DHCP）配置的 TCP/IP 网络接口。

![](img/11709a8f88c8cd03868a929dc94c0e2b_333_2.png)

在 Fedora Core 中，网络激活脚本使用 `/etc/sysconfig` 目录中的一组文本文件来激活网络接口。例如，脚本会检查 `/etc/sysconfig/network` 文件中定义的变量，以决定是否激活网络。在 `/etc/sysconfig/network` 中，你看到 NETWORKING 变量的一行如下所示：

```bash
NETWORKING=yes
```

只有当 **NETWORKING** 变量设置为 *yes* 时，网络才会激活。`/etc/sysconfig/network-scripts` 目录中的许多脚本激活特定的网络接口。例如，激活以太网接口 eth0 的配置文件是 `/etc/sysconfig/network-scripts/ifcfg-eth0`。典型的 `/etc/sysconfig/network-scripts/ifcfg-eth0` 文件包含以下内容：

```bash
DEVICE=eth0
BOOTPROTO=dhcp
HWADDR=00:08:74:E5:C1:06
ONBOOT=yes
TYPE=Ethernet
```

**DEVICE** 行提供网络设备名称。**BOOTPROTO** 变量设置为 *dhcp*，表示 IP 地址是通过使用 DHCP 动态获取的。**ONBOOT** 变量表示此网络接口是否在 Linux 启动时激活。如果你的计算机有以太网卡并且你希望在启动时激活 eth0 接口，**ONBOOT** 必须设置为 *yes*。当然，`/etc/sysconfig/network-scripts` 目录中的配置文件 *ifcfg-eth0* 仅在您的计算机拥有以太网卡且 Linux 内核已检测到并加载了该卡的特定驱动程序的条件下才有效。

在 SUSE 中，网络信息保存在 `/etc/sysconfig/network` 目录中，文件名以 *ifcfg* 开头。对于以太网接口，配置文件名以 *ifcfg-eth*-id- 开头，后跟以太网卡的唯一硬件地址。以下是典型以太网配置文件中的关键行：

```bash
BOOTPROTO='dhcp'
STARTMODE='auto'
```

**BOOTPROTO='dhcp'** 行表示该接口是使用 DHCP 设置的，而 **STARTMODE='auto'** 意味着该接口在系统启动时初始化。

## 第四卷

### 互联网

第五个浪潮
作者：Rich Tennant

![](img/11709a8f88c8cd03868a929dc94c0e2b_336_0.png)

> “在互联网出现之前，我们只是在当地吹牛。但现在，有了我们的网站，我们在全球各地都在吹牛。”

#### 内容概览

- 第 1 章：在 Linux 中发送电子邮件和即时消息 ......313
- 第 2 章：浏览网页 ......333
- 第 3 章：阅读新闻组和 RSS 源 ......345
- 第 4 章：使用 FTP ......361

##### 第 1 章：在 Linux 中发送电子邮件和即时消息

###### 本章内容

- 理解电子邮件
- 盘点邮件阅读器和 IM（即时消息）客户端
- 介绍 Evolution
- 介绍 Thunderbird
- 介绍 KMail
- 使用 Gaim 和 Kopete 进行即时消息

电子邮件（e-mail）是互联网的主要组成部分。电子邮件之所以很棒，是因为你可以与互联网上的任何人交换消息和文档。人们使用互联网的最常见方式之一就是通过电子邮件与朋友、熟人、亲人和陌生人保持联系。你可以向数千英里外的朋友发送消息，并在几分钟内收到回复。基本上，你可以从互联网主机向世界上任何地方发送消息，并且该消息通常会在几分钟内到达目的地——这是传统邮件（也称为*蜗牛邮件*，名副其实）无法做到的。

我热爱电子邮件，因为它让我可以在不进行*电话捉迷藏*游戏的情况下进行沟通，那种游戏中两个人可以无限次地给对方留言，却从未成功取得联系。当我发送电子邮件消息时，它会在收件人的邮箱中等待，以便收件人在方便时阅读。我想我更喜欢相反的情况——当人们给我发邮件时，我可以在*我*方便的时候阅读并回复。

Linux 附带了几个邮件客户端——也称为*邮件阅读器*——可以从你的互联网服务提供商（ISP）下载邮件。你也可以使用这些邮件客户端阅读和发送电子邮件。在本章中，我提到了 Linux 中可用的几个邮件客户端，并简要介绍其中几个。当你熟悉一个后，你就可以轻松使用任何邮件阅读器。

![](img/11709a8f88c8cd03868a929dc94c0e2b_339_0.png)

还有一种*保持联系*的方式，更符合当今年轻一代的需求。我指的是 IM——即时消息。IM 基本上是一对一的聊天，Linux 包含用于 AOL Instant Messenger（或 AIM）的 IM 客户端，以及其他即时消息协议，如 Jabber、ICQ、MSN Messenger、Yahoo!、Gadu-Gadu、IRC（互联网中继聊天）和 SMS（短消息服务或短信）。我在本章中简要描述了一些 IM 客户端。

###### 理解电子邮件

电子邮件消息是发送给*主机*上的用户名的（*主机*只是在线计算机的优雅名称）。这意味着如果 John Doe 以用户名 `jdoe` 登录，发给他的电子邮件地址为 `jdoe`。唯一其他需要的信息是收件人系统的全限定域名，以唯一标识收件人。因此，如果 John Doe 的系统名为 `someplace.com`，他的完整电子邮件地址变为 `jdoe@someplace.com`。有了这个地址，互联网上的任何人都可以向 John Doe 发送电子邮件。

####### MUA 和 MTA 如何工作

两种类型的邮件软件如下：

- **邮件用户代理（MUA）**是邮件阅读器的优雅名称——一个用于读取邮件消息、撰写回复和创建新消息的客户端。通常，邮件用户代理通过使用 POP3 或 IMAP4 协议从邮件服务器检索消息。POP3 是*邮政协议第 3 版*，IMAP4 是*互联网消息访问协议第 4 版*。Linux 附带邮件用户代理，如 Balsa、Thunderbird、KMail 和 Evolution。
- **邮件传输代理（MTA）**是实际发送和接收邮件消息文本的邮件服务器的优雅名称。用于邮件传输的具体方法取决于底层网络。在 TCP/IP 网络中，邮件传输代理使用*简单邮件传输协议*（SMTP）来递送邮件。Linux 包含 `sendmail`，这是 TCP/IP 网络中强大且流行的邮件传输代理。

图 1-1 展示了当 Alice 向 Bob 发送电子邮件消息时 MUA 和 MTA 如何协同工作。（如果你不知道的话，使用 *Alice* 和 *Bob* 来解释电子邮件和加密是惯例——随便拿起一本关于加密的书，你就能看到我的意思。）你可能已经知道这一点，但互联网总是被绘制成云朵——互联网的边界如此模糊，云朵似乎很适合代表它。（或者是因为没人知道它从哪里开始，到哪里结束？）




图 1-1 所示的场景非常典型。爱丽丝（Alice）和鲍勃（Bob）都通过互联网服务提供商（ISP）连接到互联网，并通过他们的 ISP 接收和发送邮件。当爱丽丝输入一条消息并发送时，她的邮件用户代理（MUA）使用简单邮件传输协议（SMTP）将消息发送到她 ISP 的邮件传输代理（MTA）。发送方的 MTA 随后使用 SMTP 将该消息发送到接收方的 MTA——即鲍勃的 ISP 的 MTA。当鲍勃连接到互联网时，他的 MUA 使用 POP3（或 IMAP4）协议从他的 ISP 的 MTA 下载消息。这就是邮件在互联网上的流转方式——从发送方 MUA 到发送方 MTA，再到接收方 MTA，最后到接收方 MUA。

![](img/11709a8f88c8cd03868a929dc94c0e2b_340_0.png)

###### 电子邮件增强功能

过去的电子邮件通常是纯文本（现在大多数邮件仍是如此），但如今许多邮件包含的内容远不止文本。当今电子邮件的两个典型特征是：

- **附件：** 如今的许多邮件都包含附件文件，这些文件可以是文档、图像等任何类型。收件人可以将附件保存到磁盘，或直接通过邮件阅读器打开。不幸的是，黑客尝试将病毒和蠕虫植入你电脑的途径之一，就是将它们放在附件中。（如果这能让你稍感安慰，大多数基于 Windows 的病毒和蠕虫在 Linux 系统中无法运行。）
- **HTML 邮件：** 电子邮件可以是 *HTML*（超文本标记语言）格式，这是一种用于布局网页的语言。当你使用具备相应功能的邮件阅读器阅读 HTML 邮件时，邮件会以华丽的字体和嵌入式图形完整呈现其效果。

![](img/11709a8f88c8cd03868a929dc94c0e2b_341_0.png)

虽然 HTML 邮件看起来不错，但如果你使用的是基于文本的邮件阅读器，它们无法正确显示。在文本邮件阅读器中，HTML 邮件只会显示为一堆乱码（实际上就是原始的 HTML 代码）。

![](img/11709a8f88c8cd03868a929dc94c0e2b_341_1.png)

如果你拥有 ISP 账户，要访问你的电子邮件只需要一个邮件客户端即可。在这种情况下，你的电子邮件驻留在 ISP 的服务器上，当你运行邮件阅读器时，它会下载邮件。在开始从 ISP 的邮件服务器阅读邮件之前，你需要进行一些设置。设置基本上要求你输入从 ISP 获取的信息——邮件服务器名称、服务器类型（例如 POP3）、你的用户名以及你的密码。

####### 盘点 Linux 中的邮件阅读器和 IM 客户端

曾经大多数邮件阅读器都是文本程序，但时移世易。如今，邮件阅读器是图形化应用程序，能够轻松显示 HTML 邮件并处理附件。它们易于使用；如果你能使用其中一个，那么几乎可以肯定你能使用市面上任何图形化的邮件阅读器。（Linux 附带了几个邮件阅读器；不妨尝试几个，看看哪一个最适合你的需求。）

IM（即时消息）是较新出现的现象，但 Linux 努力保持在技术前沿，因此它附带了两个 IM 客户端，可以支持各种 IM 协议。表 1-1 概述了 Linux 中主要的邮件阅读器和 IM 客户端。

**表 1-1 Linux 邮件阅读器和 IM 客户端**

| 软件 | 描述 |
| :--- | :--- |
| KMail | KDE 电子邮件客户端，支持 POP3 和 IMAP4 |
| Thunderbird | Mozilla Mail 客户端的重构版，Mozilla Mail 曾是 Mozilla 开源 Web 浏览器（Netscape Communicator 的开源化身）的一部分 |
| Evolution | 个人信息管理工具（PIM），包含电子邮件、日历、联系人管理和在线任务列表 |
| Gaim | 支持多种即时消息协议的 GNOME IM 客户端，如 AIM、ICQ、Yahoo!、MSN、Gadu-Gadu 和 Jabber |
| Kopete | 支持多种消息协议的 KDE IM 客户端，如 Jabber、ICQ、AIM、MSN、Yahoo!、IRC、Gadu-Gadu 和 SMS |

![](img/11709a8f88c8cd03868a929dc94c0e2b_342_0.png)

如果你的发行版中没有特定的邮件或 IM 客户端，很可能你可以轻松地从互联网下载并安装它。

###### 在 Linux 中发送电子邮件

每个 Linux 发行版的 GUI 桌面都有一个或两个默认的电子邮件客户端。GNOME 桌面通常提供 Evolution，而 KDE 桌面则选择 KMail。GNOME 和 KDE 桌面通常都附带 Mozilla 作为 Web 浏览器，并且 Mozilla 也包含一个邮件客户端。

![](img/11709a8f88c8cd03868a929dc94c0e2b_342_1.png)

Debian 包含 KMail 和 Evolution。Fedora Core 和 Ubuntu 提供 Evolution 作为默认邮件客户端。MEPIS 和 SUSE 使用 KMail 作为默认邮件阅读器，而 Xandros 则同时提供 KMail 和 Thunderbird 邮件客户端。

在接下来的章节中，我将简要介绍 Evolution、Thunderbird 邮件客户端和 KMail。所有邮件客户端都易于使用，因此你只需要一点介绍就能开始有效地使用它们。

####### 介绍 Evolution

我听说过很多关于 Evolution 的好话，所以我想从这里开始。还有什么比直接上手更好的方式呢！

![](img/11709a8f88c8cd03868a929dc94c0e2b_342_2.png)

在 Fedora Core 中，你可以通过在 GNOME 或 KDE 桌面中选择“主菜单†Internet†Evolution Email”来启动 Evolution。（在 Debian 中，我不得不选择“应用程序†Debian Menu†Apps†Net†Evolution”。）

当你第一次启动 Evolution 时，会出现“Evolution 设置向导”窗口，如图 1-2 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_343_0.png)

**图 1-2：** Evolution 设置向导引导你完成初始设置。

在欢迎界面点击“向前”，设置向导将引导你完成以下步骤：

1. **在身份界面上输入你的名字和电子邮件地址，然后点击“向前”按钮。**
   例如，如果你的电子邮件地址是 `jdoe@someplace.com`，那就输入它。
2. **设置接收电子邮件的选项，然后点击“向前”。**
   选择邮件下载协议类型——POP 或 IMAP。然后提供邮件服务器的名称（例如，`mail.comcast.net`）。当 Evolution 首次连接到邮件服务器时，系统会提示你输入密码。
3. **提供有关接收电子邮件的更多信息——多久检查一次邮件以及是否将邮件保留在服务器上——然后点击“向前”。**
   通常，你希望下载邮件并将其从服务器上删除（否则，当邮件堆积时，ISP 会投诉）。
4. 设置以下发送电子邮件的选项，完成后点击**向前**：
   - 将服务器类型选择为 SMTP。
   - 输入服务器名称，例如 `smtp.comcast.net`。
   - 如果服务器要求登录，请选中**服务器需要身份验证**复选框。
   - 输入你的用户名——即你用于登录 ISP 邮件服务器的同一用户名。（通常，发送邮件不需要登录；只有在接收——下载——邮件消息时才需要登录。）
5. 指示是否希望此电子邮件账户成为你的默认账户，并如果愿意，给此电子邮件账户起一个描述性名称；点击**向前**。
6. 通过点击地图来设置你的时区；点击**向前**。
7. 点击**应用**以完成 Evolution 设置。

完成一次性设置后，Evolution 会打开其主窗口，如图 1-3 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_344_0.png)

**图 1-3：** Evolution 负责管理邮件、日历、联系人管理和待办事项列表。

Evolution 的主显示区域垂直分为两个窗口：左侧是一个狭窄的面板，包含一列快捷按钮——邮件、联系人、日历、任务——右侧是一个较大的面板，Evolution 在此显示与当前选中的快捷图标相关的信息。在图 1-3 中，Evolution 显示的是邮件的收件箱。

你可以点击左侧窗口中的快捷按钮来切换到不同的视图。这些按钮提供了访问 PIM 所有必要组件的途径——电子邮件、日历、任务列表和联系人。你会发现所有这些任务在 Evolution 中操作起来都很直观。

要访问你的电子邮件，点击收件箱图标。Evolution 会打开你的收件箱，如图 1-4 所示。如果你启用了自动定期检查邮件的功能，Evolution 会提示你输入邮件密码并下载你的邮件。电子邮件收件箱看起来与其他邮件阅读器的收件箱非常相似，例如 Outlook Express 的收件箱。

要阅读一条消息，点击收件箱上部窗口中的消息，消息文本将显示在下部窗口中。图 1-4 显示了一条带有图像文件附件的消息。

要回复当前消息，点击工具栏上的回复按钮。会弹出一个消息编辑窗口。你可以撰写回复，然后点击工具栏上的发送按钮来发送回复。简单，不是吗？

![](img/11709a8f88c8cd03868a929dc94c0e2b_345_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_345_1.png)





若要发送新邮件，请单击 Evolution 工具栏上的“新建消息”按钮。此时会出现一个新的邮件撰写窗口。您可以在该窗口中输入您的邮件内容，编辑完成后，单击“发送”。

Evolution 附带了详尽的在线帮助。从 Evolution 菜单中选择“帮助→内容”，Evolution 2.0 用户指南将在窗口中显示。您可以随后在该窗口中阅读用户指南。

![](img/11709a8f88c8cd03868a929dc94c0e2b_346_0.png)

####### 简介 Thunderbird

Thunderbird 是 Mozilla Mail 的重新设计版本，它是随 Mozilla Web 浏览器提供的邮件和新闻阅读器——也就是开源的 Netscape Communicator 的继任者。

Xandros 附带 Thunderbird，但某些发行版默认并不安装 Thunderbird。不过，您可以轻松安装 Thunderbird。例如，在 Debian 中，在终端窗口中输入 `su -` 并输入 root 密码，然后输入 `apt-get install mozilla-thunderbird` 来安装 Thunderbird Mail。

![](img/11709a8f88c8cd03868a929dc94c0e2b_346_1.png)

安装完成后，您可以通过在 Debian 的 GNOME 桌面上选择“应用程序→Debian 菜单→应用→网络→Mozilla Thunderbird”来启动 Thunderbird。当 Thunderbird 运行时，它会启动账户向导（如图 1-5 所示）并提示您输入有关您的电子邮件账户的信息。

![](img/11709a8f88c8cd03868a929dc94c0e2b_346_2.png)

图 1-5：在 Thunderbird 的账户向导中输入您的电子邮件账户信息。

选择“电子邮件账户”单选按钮并单击“下一步”。然后，账户向导将引导您完成以下步骤：

- 1. **输入您的身份信息** — 您的姓名和完整的电子邮件地址，例如 `jdoe@someplace.com` — **并单击“下一步”**。
- 2. **提供有关您的 ISP 邮件服务器的信息 — 协议类型（POP 或 IMAP）以及传入和传出服务器名称 — 并单击“下一步”。**
  - 传入服务器是 POP 或 IMAP 服务器，而传出服务器是您发送电子邮件所使用的服务器（即 SMTP 服务器）。
- 3. **输入您的 ISP 分配给您的用户名；单击“下一步”。**
- 4. **输入一个您希望用于标识此账户的名称并单击“下一步”。**
  - 该名称仅供 Thunderbird 使用，因此您可以随意选择，例如“我的家庭账户”。
  - 账户向导会显示您输入的信息摘要。
- 5. **核实信息。如果正确，请单击“完成”。否则，请单击“后退”并更正错误。**

设置好电子邮件账户后，Thunderbird 的主窗口将出现，并显示您收件箱中的内容。很快，一个对话框会弹出，要求您输入电子邮件密码。Thunderbird 需要您的密码来从您的 ISP 下载电子邮件消息。输入您的密码并单击“确定”。

Thunderbird 下载您的消息并以熟悉的格式显示它们。要阅读一条消息，请单击该消息，全文将显示在下方窗口中，如图 1-6 所示。

Thunderbird 的使用很直观。大多数时候，您只需单击工具栏按钮即可执行对电子邮件消息的大多数操作。以下是每个工具栏按钮的功能：

- **获取邮件**：从您的电子邮件账户下载消息。（您可以设置任意数量的账户。）
- **撰写**：打开一个窗口，您可以在其中撰写并发送消息。
- **通讯簿**：打开通讯簿窗口，您可以在其中维护联系人列表。
- **回复**：打开一个窗口，您可以在其中向发送您当前阅读消息的人发送回复。
- **回复全部**：打开一个窗口，用于向您当前阅读消息的所有收件人列表中的每个人发送回复。
- **转发**：在当前窗口中调出当前消息，以便您将其转发给其他人。
- **删除**：删除选定的消息。
- **垃圾邮件**：将选定的消息标记为垃圾邮件。（您可以将选定消息标记为垃圾邮件，并选择“工具→垃圾邮件控制”以阻止类似消息。）
- **打印**：打印选定的消息。
- **停止**：停止与邮件服务器的当前传输。

如果您使用任何 GUI 邮件阅读器——从 Microsoft Outlook Express 到 Novell GroupWise——您都会发现一组类似的工具栏按钮。在以下章节中，我将描述如何执行一些常见的电子邮件相关任务。

![](img/11709a8f88c8cd03868a929dc94c0e2b_348_0.png)

图 1-6：您可以从 Thunderbird 阅读和发送电子邮件消息。

####### 管理您的收件箱

Thunderbird 下载传入邮件并将其存储在收件箱文件夹中。您可以在左侧窄窗口中看到按文件夹组织的结构。（参见图 1-6。）您设置的每个电子邮件账户都有一组文件夹。默认情况下，您拥有以下文件夹：

- **收件箱**：保存此电子邮件账户的所有传入消息。
- **未发送消息**：包含尚未发送到邮件服务器的消息。
- **草稿**：包含您保存为草稿的消息。（在邮件撰写窗口中单击“保存”按钮可将某些内容保存为草稿。）
- **已发送**：保存您成功发送的所有消息。
- **垃圾邮件/废纸篓**：包含您删除的消息。（若要清空废纸篓文件夹，请从 Thunderbird 邮件菜单中选择“文件→清空废纸篓”。）

您可以创建其他文件夹以更好地组织您的邮件。要创建文件夹，请执行以下操作：

- 1. 在 Thunderbird 窗口左侧的“本地文件夹”标签上右键单击，并从出现的菜单中选择“新建文件夹”。
  - 出现“新建文件夹”对话框。
- 2. 填写文件夹名称并选择您希望放置该文件夹的位置。单击“确定”。
  - 新文件夹出现在 Thunderbird 的左侧窗口中。然后，您可以将消息拖放到该文件夹中。

当您在左侧窗口中选择某个文件夹时，Thunderbird 会在右侧上方窗口中显示该文件夹的内容。列表通常按日期排序，最新的消息显示在列表末尾。如果您想按其他方式排序——例如按发件人或主题——只需单击该列标题，Thunderbird 就会根据该列对列表进行排序。

####### 撰写和发送消息

要发送电子邮件，您可以撰写新消息或回复正在阅读的消息。发送电子邮件的一般步骤如下：

- 1. 要回复消息，请在阅读消息时单击工具栏上的“回复”或“回复全部”按钮。要撰写新消息，请单击工具栏上的**撰写**按钮。要转发消息，请单击**转发**按钮。
  - 出现一个消息撰写窗口。
- 2. **在消息撰写窗口中，填写主题行并输入您的消息。**
  - 消息可以包含图像以及指向网站的链接。要插入这些项目中的任意一个，请从菜单中选择 `插入→图像` 或 `插入→链接`。
- 3. **如果您正在创建新消息或转发消息，请输入收件人的电子邮件地址。**
  - 要从通讯簿中选择收件人，请单击工具栏上的**地址**按钮。您的通讯簿将打开，您可以从中选择收件人。
- 4. **完成消息撰写后，单击“发送”按钮。**
  - Thunderbird 会询问您是否希望以 HTML 格式、纯文本格式或两者兼有来发送消息。
- 5. **选择一种格式，然后单击“发送”以发送消息。**
  - 如果您插入了图像和 Web 链接，并且知道收件人可以阅读 HTML 邮件，请务必选择 HTML 格式；否则，请选择纯文本。

![](img/11709a8f88c8cd03868a929dc94c0e2b_350_0.png)

如果您想稍后完成消息，请单击消息撰写窗口中的**保存**，然后关闭窗口。Thunderbird 将消息保存在**草稿**文件夹中。当您准备好再次处理该消息时，请进入**草稿**文件夹，然后双击已保存的消息以打开它。

####### 简介 KMail

KMail 是 KDE 的邮件阅读器。当您首次运行 KMail 时，会出现其主窗口（参见图 1-7），但在配置 KMail 中的邮件账户之前，您无法开始使用它来发送和接收电子邮件。

要配置 KMail，请选择 `设置→配置 KMail`。在**配置 KMail** 窗口（参见图 1-8）中，单击窗口左侧的**账户**并设置有关您的电子邮件账户的信息。KMail 使用此信息来发送和接收邮件。

对于出站邮件，请单击**发送选项卡**上的**添加**按钮（参见图 1-8），然后选择邮件传输代理。通常，对于 ISP 提供的邮件账户，您应该选择 `SMTP` 并输入 ISP 提供给您的邮件服务器名称（例如，`smtp.comcast.net`）。




![](img/11709a8f88c8cd03868a929dc94c0e2b_351_0.png)

图 1-7：KMail 的初始窗口

![](img/11709a8f88c8cd03868a929dc94c0e2b_351_1.png)

图 1-8：在“配置 KMail”窗口中配置电子邮件账户。

要设置 incoming mail information，请在“Receiving”标签页上点击 **Add**（添加），然后选择邮件协议，例如 POP3 或 IMAP。您的 ISP（互联网服务提供商）会告知您使用哪种协议。（通常是 POP3 或 IMAP。）然后输入邮件服务器的名称（例如，mail.concast.net）以及您 ISP 账户的用户名和密码。

设置好电子邮件账户信息后，您可以开始使用 KMail。用户界面直观易用，与 Thunderbird 和 Evolution 等其他邮件阅读器类似。KMail 会定期检查和下载来自您的 incoming mail 账户的邮件。您可以在收件箱（Inbox）中查看到达的邮件。

###### Linux 中的即时通讯

Linux 中有两大主要的即时通讯（IM）客户端。在 GNOME 桌面环境中，您可以使用 Gaim；而 Kopete 则是专为 KDE 桌面环境设计的。我将在下面两个章节中简要介绍这两个即时通讯客户端。

####### 使用 Gaim

您可以使用 Gaim 与众多不同即时通讯服务（如 AIM、ICQ、Yahoo!、MSN、Gadu-Gadu 和 Jabber）上的所有联系人保持联系。如果您使用上述任何一种即时通讯服务，使用 Gaim 会让您感觉如鱼得水。

![](img/11709a8f88c8cd03868a929dc94c0e2b_352_0.png)

在 Fedora Core 中，通过从 GNOME 桌面选择 **Applications → Internet → Messaging Client** 即可启动 Gaim。您可以在其他发行版的 GNOME 桌面中以类似方式启动 Gaim。Gaim 的初始窗口将与账户窗口一起出现，如图 1-9 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_352_1.png)

**图 1-9：** 在此窗口中管理您的所有即时通讯账户。

首先，在“Accounts”（账户）窗口中设置您的消息账户。点击 **Add**（添加）按钮，并在“Add Account”窗口中填入所需信息，如图 1-10 所示。您需要为您的即时通讯服务选择协议。例如，AIM 的协议是 AIM/Icq。其他可选协议包括 Gadu-Gadu、Jabber、MSN 和 Yahoo!。

![](img/11709a8f88c8cd03868a929dc94c0e2b_353_0.png)

图 1-10：输入每个即时通讯账户的信息。

输入账户信息后，“Accounts”窗口将显示所有已定义的账户。然后，您可以从 Gaim 主窗口中选择一个账户并点击 **Sign On**（登录），如图 1-11 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_353_1.png)

图 1-11：使用 Gaim 登录 AIM。

当 Gaim 为您完成登录后，它会打开标准的“Buddy List”（好友列表）窗口。（参见图 1-12。）

![](img/11709a8f88c8cd03868a929dc94c0e2b_354_0.png)

图 1-12：Gaim 中的好友列表窗口。

要添加好友，请选择 **Buddies → Add Buddy**。在出现的“Add Buddy”窗口中，输入好友的屏幕名称并点击 **Add**（添加）。要创建新组，请选择 **Buddies → Add Group**。在出现的“Add Group”窗口中，输入新组的名称，然后点击 **Add**（添加）。

如果您的任何好友在线，他们的名字会显示在“Buddy List”窗口中。要向好友发送消息，请双击其名字，将弹出一个消息窗口。如果有人给您发送消息，也会弹出一个消息窗口显示该消息，您即可在该窗口开始对话。

####### 使用 Kopete

Kopete——KDE 的即时通讯客户端——使您能够连接众多消息服务，包括 AIM、IRC、MSN Messenger、Yahoo!、Gadu-Gadu 和 SMS。

在 Debian、SUSE 和 Xandros 中，您可以通过在应用程序菜单中选择 **Chat** 或 **Instant Messaging** 来启动 Kopete。

首次运行 Kopete 时，您会看到“Configure Kopete”窗口（参见图 1-13），在此您可以输入关于您的即时通讯和其他消息服务账户的信息。

例如，要添加您的 AIM 账户信息，请点击 **New**（新建），然后响应“Account Wizard”（账户向导）中的提示。第一步是选择您的消息服务。（参见图 1-14。）

![](img/11709a8f88c8cd03868a929dc94c0e2b_354_1.png)

## 第四部分

### 第一章

#### 在 Linux 中进行电子邮件和即时通讯

![](img/11709a8f88c8cd03868a929dc94c0e2b_355_0.png)

图 1-13：在此窗口中输入关于您的消息账户的信息。

选择适当的消息服务，例如如果您使用 AOL 的即时通讯服务，则选择 AIM。然后提供 AIM 的屏幕名称和密码。

![](img/11709a8f88c8cd03868a929dc94c0e2b_355_1.png)

图 1-14：在此窗口中选择您的消息服务。

设置好您的消息服务账户后，“Account Wizard”将关闭，您将看到常规的 Kopete 窗口。要通过您的消息服务登录并开始使用 Kopete，请点击 Kopete 窗口中的 **Connect**（连接）按钮——这是工具栏上最左边的按钮。（参见图 1-15。）

![](img/11709a8f88c8cd03868a929dc94c0e2b_356_0.png)

**图 1-15：** 在 Kopete 中查看好友列表。

点击放大镜图标可查看您的好友。在线好友会显示一个实心的笑脸图标。右键点击在线好友，从菜单中选择 **Start Chat**（开始聊天）即可开始交谈。选择 **File ➪ Add Contact** 可添加更多联系人。

好吧，如果您熟悉 AIM，您就知道该怎么做：尽情享受使用 Kopete 进行即时通讯的乐趣吧！

##### 第二章：浏览网络

###### 本章内容

- 探索万维网（World Wide Web）
- 理解 URL
- 了解 Web 服务器和 Web 浏览器
- 盘点 Linux 中的 Web 浏览器
- 使用 Mozilla Firefox 进行 Web 浏览

我猜想您已经了解网络，但您知道网络（或更正式地称为万维网）使互联网变成了今天的样子吗？互联网已经存在相当长的时间，但直到 1993 年网络出现，它才真正大众化。

在网络出现之前，您需要使用晦涩难懂的 UNIX 命令来下载和使用文件，这对我们大多数人来说太复杂了。然而有了网络，任何人都可以通过使用 Web 浏览器——一种下载并显示网络文档的图形应用程序——来享受互联网的好处。只需一次鼠标点击，您就可以从阅读公司网站的文档跳转到下载来自遥远地区的视频剪辑。

在本章中，我将简要介绍网络，并介绍 Mozilla Firefox——大多数 Linux 发行版中的主要 Web 浏览器（顺带一提，它也是主要的邮件和新闻阅读器）。我还会简要讨论如何创建您自己的网页。

> KDE 桌面通常使用 Konqueror 作为 Web 浏览器，但在使用过一款 Web 浏览器后，您可以轻松使用任何其他 Web 浏览器。

###### 探索万维网

如果您在工作中使用过文件服务器，您就知道共享文件的便利性。您可以使用桌面上的文字处理软件来访问共享服务器上的任何文档。

现在想象一下一种文字处理软件，它允许您打开并查看位于互联网上任何计算机上的文档。您可以以完整的形式查看该文档，包括格式化文本和图形。如果文档引用了另一个文档（可能位于另一台计算机上），您可以通过点击该引用来打开链接的文档。这种对分布式文档的轻松访问，本质上万维网就是提供的东西。

当然，文档必须采用标准格式，以便任何计算机（配备适当的 Web 浏览器软件）都能访问和解释该文档。并且，在系统之间传输网络文档也需要一种标准协议。

-   **技术细节**
    标准的网络文档格式是*超文本标记语言*（HTML），而用于交换网络文档的标准协议是*超文本传输协议*（HTTP）。HTML 文档是文本文件，不依赖特定的操作系统，因此它们适用于从 Windows 和 Mac 到任何类型的 UNIX 和 Linux 的任何系统。

-   **记住**
    *Web 服务器*是向发出相应 HTTP 请求的任何客户端提供 HTML 文档的软件。*Web 浏览器*是实际从 Web 服务器下载 HTML 文档并以图形方式显示其内容的客户端软件。

####### 像巨大的蜘蛛网

万维网是 Web 服务器及其提供的 HTML 文档的结合。这样看待网络，网络就像一本巨大的书籍，其页面散布在整个互联网上。您使用计算机上运行的 Web 浏览器来查看这些页面——这些页面像巨大的蜘蛛网一样相互连接，文档无处不在，如图 2-1 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_359_0.png)



想象一下，网页（HTML 文档）通过网络连接相互链接，这些连接形似巨大的蜘蛛网，因此你可以理解为何该网络被称为“*Web*”（万维网）。其中“*World Wide*”（环球/广域）的部分则源于网页遍布世界各地这一事实。

###### 链接和 URL

与实体书的页面类似，网页包含文本和图形。然而与实体书不同的是，网页可以包含多媒体，例如视频片段、声音以及指向其他网页的链接。

网页中的*链接*是指向其他网页的引用，你可以跟随这些链接从一个页面跳转到另一个页面。Web 浏览器通常将这些链接显示为带下划线的文本（不同颜色）或图像。每个链接都如同一条指令——类似于你在实体书中可能找到的“如需更多信息，请参阅第 4 章”。在网页中，你只需点击该链接；Web 浏览器就会调出被引用的页面，即使该文档实际上驻留在互联网上某台远程计算机中。

![](img/11709a8f88c8cd03868a929dc94c0e2b_360_0.png)

网页中的链接被称为*超文本链接*，因为当你点击一个链接时，Web 浏览器会跳转到该链接所引用的网页。

这种结构提出了一个问题。在实体书中，你可能会要求读者前往书中的特定章节或页面。那么超文本链接是如何指示被引用网页位置的？在万维网中，每个网页都有一个特殊的名称，称为*统一资源定位符*（URL）。URL 唯一地指定了计算机上文件的位置。图 2-2 展示了 URL 的组成部分。

![](img/11709a8f88c8cd03868a929dc94c0e2b_360_1.png)
# **第四卷**  
**第 2 章**  
**浏览万维网**

# **336** *发现万维网*

如图 2-2 所示，URL 包含以下部分：

- **协议：** 名称为 Web 浏览器用于访问 URL 指定文件中数据的协议。在图 2-2 中，协议是 http://，这意味着该 URL 指定了一个网页的位置。以下是一些常见的协议类型及其含义：
  - `file://` 表示 URL 指向本地文件。你可以使用此 URL 查看 HTML 文件而无需连接互联网。例如，`file:///var/www/html/index.html` 从你的 Linux 系统打开文件 /var/www/html/index.html。
  - `ftp://` 表示你可以使用文件传输协议（FTP）下载文件。例如，`ftp://ftp.purdue.edu/pub/uns/NASA/nasa.jpg` 指的是 FTP 服务器 ftp.purdue.edu 的 /pub/uns/NASA 目录中的图像文件 nasa.jpg。如果你想通过 FTP 访问特定的用户账户，请使用以下形式的 URL：
    - `ftp://username:password@ftp.somesite.com/`
    - 将用户名和密码嵌入 URL 中。（注意，密码是明文且不安全。）
  - `http://` 表示你使用超文本传输协议（HTTP）下载文件。该协议是所有网站 URL 的通用格式，例如 Fedora 项目主页的 http://fedora.redhat.com。如果 URL 没有文件名，Web 服务器会发送一个名为 index.html 的默认 HTML 文件。（这是流行的基于 UNIX 的 Apache Web 服务器的默认文件名；Microsoft Windows Web 服务器使用不同的默认文件名。）
  - `https://` 指定你通过安全套接层（SSL）连接访问文件——这是由 Netscape 通信公司设计用于加密跨互联网数据传输的协议。通常，这种形式的 URL 用于 Web 浏览器向 Web 服务器发送敏感信息（如信用卡号、用户名和密码）时。例如，像 `https://some.site.com/secure/takeorder.html` 这样的 URL 可能会显示一个请求信用卡信息及其他个人信息（如姓名、地址和电话号码）的 HTML 表单。
  - `mailto:` 指定你可以用来发送电子邮件消息的电子邮件地址。此 URL 会打开你的电子邮件程序，你可以从中发送消息。例如，`mailto:webmaster@someplace.com` 指主机的管理员 someplace.com。
  - `news://` 指定你可以通过网络新闻传输协议（NNTP）读取的新闻组。例如，`news://news.md.comcast.giganews.com/comp.os.linux.setup` 访问新闻服务器 news.md.comcast.giganews.com 上的 comp.os.linux.setup 新闻组。如果你为 Web 浏览器配置了默认新闻服务器，你可以省略新闻服务器名称并使用 URL `news:comp.os.linux.setup` 访问该新闻组。

- **域名：** 包含拥有此 URL 指定文件的计算机的完全限定域名。你也可以在此字段中提供 IP 地址。域名不区分大小写。

- **端口：** 使用 URL 第一部分列出的协议的端口号。URL 的此部分是可选的；所有协议都有默认端口。例如，HTTP 的默认端口是 80。如果站点配置 Web 服务器监听不同的端口，则 URL 必须包含端口号。

- **目录路径：** URL 中引用文件的目录路径。对于网页，此字段是 HTML 文件的目录路径。目录路径区分大小写。

- **文件名：** 文件的名称。对于网页，文件名通常以 *.htm* 或 *.html* 结尾。如果省略文件名，Web 服务器将返回一个默认文件（通常名为 index.html）。文件名区分大小写。

- **HTML 锚点：** URL 的可选部分，使 Web 浏览器跳转到文件中的特定位置。如果此部分以问号 (?) 而不是井号 (#) 开头，浏览器会将问号后面的文本视为查询。Web 服务器会根据此类查询返回信息。

###### Web 服务器和 Web 浏览器

Web 服务器提供网页，Web 浏览器下载它们并向用户显示它们。这就是这两个协作软件包让 Web 正常运作的基本故事。

在典型场景中，用户坐在连接到互联网的计算机前并运行 Web 浏览器。当用户点击一个链接或在 Web 浏览器中输入 URL 时，浏览器连接到 Web 服务器并向服务器请求文档。Web 服务器发送文档（通常为 HTML 格式）并结束连接。Web 浏览器解释并显示 HTML 文档，包括文本、图形和多媒体（如果适用）。图 2-3 说明了用户浏览 Web 的这一典型场景。

![](img/11709a8f88c8cd03868a929dc94c0e2b_362_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_363_0.png)

在服务器发送文档后，Web 浏览器与 Web 服务器的连接即结束。当用户浏览已下载的文档并点击另一个超文本链接时，Web 浏览器再次连接到超文本链接中指定的 Web 服务器，下载文档，结束连接，并显示新文档。这就是用户可以轻松从一个文档移动到另一个文档的方式。

> Web 浏览器不仅仅能与 Web 服务器“交谈” HTTP——事实上，Web 浏览器还可以使用 FTP 下载文档，并且许多浏览器都集成了电子邮件和新闻阅读器。

###### 在 Linux 中浏览 Web

浏览 Web 很有趣，因为如今许多网页都充满了图形和多媒体。此外还有惊喜元素——你可以点击一个链接，最终到达意想不到的网页。链接是 Web 最引人入胜（且有用）的方面。你可以从一个显示今日天气的页面开始，点击几次后，你就可能正在阅读本周的《时代》杂志。

要浏览 Web，你只需要一个 Web 浏览器和一个互联网连接。我假设你已经处理好了互联网连接（如果你尚未设置互联网连接，请参见第三卷第 1 章），所以你只需要了解 Linux 中的 Web 浏览器。

####### 查看 Linux 的 Web 浏览器

许多 Linux 发行版都附带 Mozilla Web 浏览器。Mozilla 是久负盛名的 Netscape Communicator 的开源版本。

Linux 还有其他几种 Web 浏览器。我简要提及其他浏览器，但在其余讨论中主要关注 Firefox。以下是 Linux 的主要 Web 浏览器：

- **Mozilla**：那个老功臣——Netscape Communicator——的再生，但表现更好。包括邮件和新闻阅读器。该 Web 浏览器称为 Mozilla Navigator，或简称为 Navigator（正如在 Netscape Communicator 中那样）。
- **Epiphany**：GNOME Web 浏览器，使用 Mozilla 代码的一部分来绘制网页，但拥有比 Mozilla 更简洁的用户界面。如果未安装 Epiphany，你可以从 www.gnome.org/projects/epiphany 下载。
- **Firefox**：Mozilla 的下一代浏览器，可阻止弹出式广告，提供标签页以便在单个窗口中轻松查看多个网页，并包含一组隐私工具。你可以从 www.mozilla.org/download.html 下载 Firefox。
- **Konqueror**：KDE Web 浏览器，同时兼作文件管理器和通用查看器。

除这些之外，还有许多其他应用程序能够下载和显示网页。

![](img/11709a8f88c8cd03868a929dc94c0e2b_364_0.png)

如今，大多数发行版都包含 Mozilla Firefox Web 浏览器。我在下一节中简要介绍 Firefox Web 浏览器。其他所有 Web 浏览器都具有同样直观的用户界面。

![](img/11709a8f88c8cd03868a929dc94c0e2b_364_1.png)

Debian 默认不安装 Firefox，但你可以通过输入 *su* - 成为 *root*，然后输入 *apt-get install mozilla-firefox* 轻松安装它。安装后，你可以选择 Debian 的 GNOME 桌面上的应用程序‹Debian 菜单‹网络‹Mozilla Firefox 来启动 Firefox。





###### 介绍 Firefox 用户界面

通常，你可以点击面板上的图标或通过从 GUI 桌面菜单中选择来启动 Firefox。

启动 Firefox 时，它会显示一个带有默认主页的浏览器窗口。（Web 服务器上的主 Web 页面被称为*主页*。）你可以配置 Firefox 使用不同的 Web 页面作为默认主页。

图 2-4 显示了一个来自美国政府网站（*www.irs.gov*）的 Web 页面，以及 Firefox 浏览器窗口的主要元素。请注意，Firefox 支持*标签页浏览*，这意味着你可以通过按 Ctrl+T 打开一个新的标签页，并在该标签页中查看 Web 页面。这样，你可以在一个窗口中查看多个 Web 页面。

Firefox Web 浏览器在其用户界面中包含了许多功能，但你很容易掌握它。你可以从基础知识开始使用 Firefox，然后逐渐扩展到尚未探索的领域。

###### Firefox 工具栏

从窗口顶部开始，你会看到一个带有标准菜单（文件、编辑等）的菜单栏，随后是两个工具栏——导航工具栏和书签工具栏。书签工具栏下方的区域是当前 Web 页面显示的位置。

以下是导航工具栏（位于菜单栏下方）上的按钮和文本框（从左到右）的功能：

- 后退：移动到上一个 Web 页面。
- 前进：移动到你之前可能后退过的页面。
- 重新加载：重新加载当前 Web 页面。
- 停止：停止加载当前页面。
- 主页：转到主页。
- 位置：显示当前 Web 页面的 URL。（在此框中输入 URL 并按 Enter 键查看该 Web 页面。）
- 前往：转到在“位置”文本框中输入的 URL。
- Google 搜索：点击可搜索各种网站，如 Google、Yahoo!、Amazon.com、Dictionary.com 和 eBay；输入文本并按 Enter 键搜索当前选定的网站（默认为 Google）。

###### Linux 中的 Web 浏览

341

![](img/11709a8f88c8cd03868a929dc94c0e2b_366_0.png)

图 2-4：正在运行的 Firefox Web 浏览器。

紧接在导航工具栏下方的是书签工具栏，带有可带你到特定 Web 页面的按钮。

####### 状态栏

你可以把 Firefox 窗口底部边缘的栏看作状态栏，因为该区域的中间部分在 Firefox 加载 Web 页面时会显示状态信息。

####### 技术内幕

在 Firefox 状态栏的右侧，当你访问安全的 Web 网站时，会出现一个安全挂锁图标。Firefox 支持使用 SSL 在浏览器和 Web 服务器之间传输加密数据的安全版本 HTTP。当 Firefox 连接到支持安全 HTTP 的 Web 服务器时，状态栏右边缘会出现一个锁定的安全挂锁图标。否则没有安全挂锁图标，表示连接不安全。安全 HTTP 传输的 URL 以 `https://` 开头，而不是通常的 `http://`（注意 `https` 中的额外 `s`）。

####### 提示

Firefox 在状态栏的左侧显示状态消息。你可以观察这个区域的消息以查看发生了什么。如果你将鼠标悬停在 Web 页面上的链接上，状态栏会显示该链接的 URL。

第四卷

第 2 章

浏览 Web

我尚未详细提及 Firefox 菜单。这是因为你通常可以不用它们就完成任务。然而，快速浏览一下 Firefox 菜单是值得的，这样你就知道每个菜单提供的功能。表 2-1 提供了 Firefox 菜单的概述。

| 表 2-1 Firefox 菜单 | |
| :--- | :--- |
| 此菜单 | 允许你执行以下操作 |
| 文件 (File) | 打开文件或 Web 位置，打开或关闭标签页，通过电子邮件发送 Web 页面或链接，编辑 Web 页面，打印当前页面，并退出 Firefox |
| 编辑 (Edit) | 复制和粘贴选区，在当前页面中查找文本，并编辑首选项 |
| 视图 (View) | 显示或隐藏各种工具栏，重新加载当前页面，放大或缩小文本，并查看页面的 HTML 代码 |
| 前往 (Go) | 在你访问过的页面列表中向前和向后移动，或跳转到最近访问的其他 Web 页面 |
| 书签 (Bookmarks) | 为页面添加书签，管理书签，并将链接添加到书签工具栏文件夹。（这些链接随后会出现在书签工具栏中。） |
| 工具 (Tools) | 搜索 Web 并管理 Web 页面的各个方面，如主题，并查看有关当前页面的信息 |
| 帮助 (Help) | 获取 Firefox 的在线帮助 |

你的主页是启动 Firefox 时加载的页面。默认主页取决于发行版。通常主页是系统硬盘上的一个文件。更改主页很容易。

首先，找到你想作为主页的 Web 页面上的页面。你可以用任何方式到达该页面。你可以使用搜索引擎查找你想要的页面，可以在“位置”文本框中输入 URL，甚至可能偶然到达你想要作为主页的页面。这并不重要。

当你在 Firefox 中查看你想作为主页的 Web 页面时，从 Firefox 菜单中选择“编辑”->“首选项”（Edit Preferences）。偏好设置对话框出现，如图 2-5 所示。

在图 2-5 的右侧，注意偏好设置中的“主页”部分。然后你会看到主页的“位置”文本框，地址下方是一个“使用当前页面”按钮。点击该按钮将使当前页面成为你的主页。

![](img/11709a8f88c8cd03868a929dc94c0e2b_368_0.png)

你可以使用偏好设置对话框设置许多其他选项。虽然这里不解释所有选项，但你可以通过点击周围来探索你在此窗口中可以做的所有事情。例如，你可以点击“使用书签”按钮来选择一个保存的 URL 书签作为主页。（你必须从对话框中选择书签。）

###### 使用 Firefox 冲浪网络

你从主页去哪里取决于你。你要做的就是点击并看看你最终到达哪里。移动你的鼠标。当你鼠标指针变成带有伸出食指的手形时，你就知道在一个链接上。点击链接，Firefox 将下载该链接引用的 Web 页面。

你如何使用 Web 取决于你想做什么。刚开始时，你可能会进行大量探索——浏览网站并跟随链接，没有具体目标（你可以称之为 Web 窗口购物）。

另一种更有目的性的 Web 使用方式是从网络查找特定信息。例如，你可能想定位包含指定关键字文档的所有网站。对于这样的搜索，你可以使用网络上可用的许多 Web 搜索工具之一。Firefox 的搜索文本框会将你带到 Google Web 搜索页面（www.google.com）。

第三种使用方式是访问一个具有已知 URL 的特定网站。例如，当你阅读本书中关于特定主题的内容时，你可能会遇到一个特定的 URL。在这种情况下，你想直接转到该 Web 页面。

![](img/11709a8f88c8cd03868a929dc94c0e2b_369_0.png)

如果你想用 Firefox 浏览网络，你只需要一个起始 Web 页面——然后你可以点击任何吸引你的东西。例如，选择 Firefox 导航工具栏中“位置”文本框中的文本，输入 `www.yahoo.com`，然后按 Enter。你到达了 Yahoo! 主页，显示了 Yahoo! Web 目录——按主题组织。这就是你的起点。你要做的就是点击，你就上路了！

##### 第 3 章：阅读新闻组和 RSS 源

**本章内容**

- 理解新闻组
- 从你的 ISP 阅读新闻组
- 在某些网站阅读和搜索新闻组
- 阅读 RSS 源

Internet 新闻组类似于 Web 时代前的公告板系统（BBSs）或 AOL 和 MSN 等在线系统提供的论坛。基本上，新闻组提供了一个全球性的分布式会议系统。你可以发布文章——本质上是一封发给整个群体的一封电子邮件——并回应其他人发布的文章。

把 Internet 新闻组想象成一个聚集地——一个虚拟的会议场所，你可以在那里提问并讨论各种议题。（而且最棒的是，你讨论的一切都被归档以备后患。）

要参与新闻组，你需要访问新闻服务器——你的 Internet 服务提供商（ISP）可以提供这种访问权限。你还需要一个新闻阅读器。幸运的是，Linux 附带了你可以用来阅读新闻组的软件。在本章中，我向你介绍新闻组，并展示如何使用几个新闻阅读器阅读新闻组。我还简要解释了你如何免费从几个网站阅读和搜索新闻组。

如今，阅读网站和网络日志摘要的另一种流行方式是使用可以接受 RSS 源的程序。在章节末尾，我简要描述了什么是 RSS 源，以及如何使用 KDE Aggregator 等程序订阅 RSS 源并在你的 Linux 系统上阅读它们。

###### 理解新闻组

新闻组起源于*Usenet*——一个广泛用于交换电子邮件和新闻项目的存储转发消息网络。Usenet 像电报一样工作，新闻和邮件从一个系统中继到另一个系统。在 Usenet 中，系统不在任何网络上；系统只是互相拨号并使用 UNIX-to-UNIX Copy Protocol (UUCP) 传输文本消息。





####### 了解新闻组

尽管 Usenet 是一个连接非常松散的计算机集合，但由于连接它所花费的费用极低，它运行良好并持续被使用。你只需要一个调制解调器和一个愿意存储并转发你的邮件和新闻的站点。你需要在你的系统上设置 UUCP，但不需要持续的网络连接；只需几通电话即可保持电子邮件和新闻的流动。Usenet 的缺点是你不能通过 UUCP 使用 TCP/IP 服务，如 Web、TELNET 或 FTP。

源自 Usenet 的新闻组现在已经迁移到互联网上（尽管这些新闻组仍被称为 Usenet 新闻组）。目前，网络新闻传输协议（NNTP）取代了 UUCP 来传输新闻。

尽管（对于大多数在线世界而言）新闻传输协议已从 UUCP 更改为 NNTP，但新闻传输的存储转发概念保持不变。因此，如果你想在 Linux 系统上获取新闻，必须找到一个新闻服务器供你的系统从中下载新闻。通常，你可以使用你 ISP 的新闻服务器。

######## 新闻组层级结构

互联网新闻组按照层级结构组织，以便于维护和使用。新闻组名称通过显示层级结构来帮助理清条理。

诚然，这些新闻组名称是用互联网行话编写的，初看可能显得晦涩难懂。但经过一点解释，这种语言其实很容易掌握。例如，典型的新闻组名称如下所示：

```
comp.os.linux.announce
```

这个名称表示 `comp.os.linux.announce` 是一个关于 Linux 操作系统（`os.linux`）公告的新闻组，并且这些主题属于计算机（`comp`）这个大类别。

如你所见，新闻组名称的格式是由点分隔的一系列单词。这些单词表示新闻组的层级。图 3-1 说明了新闻组层级组织的概念。

为了理解新闻组层级结构，请将新闻组名称与 Linux 中文件的路径名（例如，`/usr/lib/X11/xinit/Xclients`）进行比较。正如文件的路径名显示了文件的目录层级一样，新闻组名称也显示了新闻组的层级。在文件名中，斜杠（ / ）用于分隔目录名称；在新闻组名称中，句点（ . ）用于分隔新闻组层级的不同级别。

![](img/11709a8f88c8cd03868a929dc94c0e2b_372_0.png)

在新闻组名称中，第一个词代表新闻组*类别*。例如，`comp.os.linux.announce` 新闻组属于 `comp` 类别，而 `alt.books.technical` 则属于 `alt` 类别。

######## 顶级新闻组类别

表 3-1 列出了一些主要的新闻组类别。你会发现有各种各样的新闻组，涵盖的主题从政治到计算机不等。与 Linux 相关的新闻组位于 `comp.os.linux` 层级中。

| 类别 | 主题 |
| :--- | :--- |
| alt | 替代新闻组（不受任何规则约束），内容从平凡到奇异不等 |
| biomet | 生物学新闻组 |
| bit | Bitnet 新闻组 |
| biz | 商业新闻组 |
| clari | Clarinet 新闻服务（每日新闻） |
| comp | 计算机硬件和软件新闻组（包括 Linux 和 Microsoft Windows 等操作系统） |
| ieee | 电气电子工程师学会（IEEE）新闻组 |
| k12 | 专门针对中小学教育的新闻组 |
| linux | 专门针对 Linux 的新闻组（包括一个 `linux.rechat` 层级） |
| misc | 杂项新闻组 |
| news | 关于互联网新闻管理的新闻组 |
| rec | 娱乐和艺术新闻组 |
| sci | 科学与工程新闻组 |
| soc | 讨论社会问题和各种文化的新闻组 |
| talk | 对当前问题的讨论（想想“谈话广播”） |

这个简短的类别列表具有误导性，因为它并没有真正告诉你每个类别中可用的新闻组的广泛多样性。仅顶级类别就接近一千个，但许多顶级类别仅分布在世界特定地区。由于每个新闻组类别包含多个子类别级别，新闻组的总数可能接近 60,000 或 70,000！仅 `comp` 类别就有接近 1,200 个新闻组。

不幸的是，许多新闻组都被垃圾邮件淹没，这比你的电子邮件收件箱更糟糕，因为任何人都可以在新闻组上发布任何内容。有一些被称为受控新闻组（moderated newsgroups）的新闻组可以提供一些缓解。任何想要在受控新闻组上发帖的人，都必须首先将文章提交给版主——一个人类——版主可以决定是发布该文章还是拒绝它。你可以通过尽可能浏览受控新闻组来减少垃圾邮件的过载。

![](img/11709a8f88c8cd03868a929dc94c0e2b_373_0.png)

若要浏览新闻组类别并了解新闻组所涵盖主题的广度，请访问 Google Groups 网站 http://groups.google.com 并单击 Browse all of Usenet 链接。

######## 与 Linux 相关的新闻组

通常，你根据自己的兴趣缩小新闻组的选择范围。例如，如果你对 Linux 感兴趣，你可以选择以下一个或多个新闻组：

- `comp.os.linux.admin`：关于 Linux 系统管理的信息。
- `comp.os.linux.advocacy`：关于推广 Linux 的讨论。
- `comp.os.linux.announce`：关于 Linux 的重要公告。此新闻组是受控的，这意味着你必须将文章通过电子邮件发送给版主，如果文章适合该新闻组，版主随后会将其发布到新闻组中。（这种方法可以防止杂乱信息堵塞新闻组。）
- `comp.os.linux.answers`：关于 Linux 的问题和答案。所有 Linux HOWTO 都发布在这个受控新闻组中。
- `comp.os.linux.development`：当前的 Linux 开发工作。
- `comp.os.linux.development.apps`：Linux 应用程序开发。
- `comp.os.linux.development.system`：Linux 操作系统开发。
- `comp.os.linux.hardware`：关于 Linux 和各种类型硬件的讨论。
- `comp.os.linux.help`：关于 Linux 各个方面的帮助。
- `comp.os.linux.misc`：各种与 Linux 相关的主题。
- `comp.os.linux.networking`：Linux 下的网络。
- `comp.os.linux.redhat`：Red Hat Linux 相关主题。
- `comp.os.linux.setup`：Linux 设置和安装。
- `comp.os.linux.x`：关于在 Linux 下设置和运行 X 窗口系统的讨论。
- `linux.debian`：关于 Debian GNU/Linux 的受控新闻组。
- `linux.debian.news`：关于 Debian GNU/Linux 新闻条目的受控新闻组。
- `linux.redhat`：关于 Red Hat Linux 的讨论。

![](img/11709a8f88c8cd03868a929dc94c0e2b_374_0.png)

你必须有选择性地决定阅读哪些新闻组，因为跟上所有新闻是不可能的，即使在 Linux 这样一个特定领域也是如此。当你第一次安装和设置 Linux 时，你可能阅读 `comp.os.linux.help`、`comp.os.linux.setup`、`comp.os.linux.hardware` 和 `comp.os.linux.x` 等新闻组（特别是如果你在 X 方面有问题时）。当 Linux 启动并运行后，你可能只想了解 Linux 中发生的新事物。为了获取此类信息，请阅读 `comp.os.linux.announce` 新闻组。

###### 从你的 ISP 阅读新闻组

如果你向 ISP 注册以获得互联网接入，他们可以提供给你访问新闻服务器的权限。这些互联网新闻服务器使用网络新闻传输协议（NNTP）进行通信。你可以使用支持 NNTP 的新闻阅读器（如 KNode）来访问新闻服务器并阅读选定的新闻组。你也可以使用 Thunderbird 阅读新闻。使用新闻阅读器是从你的 ISP 新闻服务器访问新闻的最简单方式。





![](img/11709a8f88c8cd03868a929dc94c0e2b_375_0.png)

关于阅读新闻组（newsgroups）的讨论假设你已从互联网服务提供商（ISP）获取了新闻服务器的访问权限。ISP 会提供新闻服务器的名称，以及在你的新闻阅读器中设置新闻账户所需的用户名和密码。

要阅读新闻，你需要*新闻阅读器*——一个允许你选择新闻组并查看该新闻组中条目的程序。你还必须理解新闻组的层级结构和命名约定（我在本章前面的“新闻组层级结构”一节中对此进行了描述）。现在我将向你展示如何从新闻服务器读取新闻。

![](img/11709a8f88c8cd03868a929dc94c0e2b_375_1.png)

如果你无法通过 ISP 访问新闻组，可以尝试使用现存的许多公共新闻服务器之一。要获取公共新闻服务器的列表，请访问 NewzBot 网站：`www.newzbot.com`。在该网站上，你可以搜索携带特定新闻组的新闻服务器。

####### 盘点新闻阅读器

你可以使用几种软件包之一，在 Linux 中下载和阅读新闻组。以下是一些主要的新闻阅读器：

- **Thunderbird**：Thunderbird 包含从 NNTP 服务器下载新闻的功能。你可以阅读新闻组并将条目发布到新闻组。Xandros 操作系统使用 Thunderbird 处理邮件和新闻。
- **KNode**：这是 KDE 的一个新闻阅读器，你可以从 `knode.sourceforge.net` 下载它。Debian、MEPIS 和 SUSE 将 KNode 作为新闻阅读器提供。
- **Pan**：Pan 是一个基于图形用户界面（GUI）的新闻阅读器。根据开发者的网站（`http://pan.rebelbase.com`）所述：“……试图让新手和有经验的用户都感到满意。”你可以从 `http://pan.rebelbase.com/download` 下载适用于各种 Linux 发行版的 Pan。

![](img/11709a8f88c8cd03868a929dc94c0e2b_375_2.png)

如果在你的 Linux 系统中找不到新闻阅读器，你可以轻松地在任何 Linux 发行版中下载并安装上述任何一个新闻阅读器。通常，你可以通过在搜索引擎中进行简单搜索来找到下载网站——只需搜索单词 *download*（下载）加上新闻阅读器的名称即可。

####### 使用 Thunderbird 阅读新闻组

你可以浏览新闻组并从 Thunderbird 发布文章，Thunderbird 是 Mozilla 项目推出的邮件和新闻阅读器。

![](img/11709a8f88c8cd03868a929dc94c0e2b_375_3.png)

在某些发行版（如 Xandros）中，主菜单中有直接启动 Thunderbird 的选项。在许多 Linux 发行版中，Thunderbird 的邮件和新闻组件可能未安装。在这种情况下，你需要下载并安装 Thunderbird 的邮件和新闻组件，或者使用其他新闻阅读器。

当你第一次使用 Thunderbird 阅读新闻组时，请按照以下步骤设置新闻账户：

1. **从 Thunderbird 菜单中选择 编辑 > 账户设置。** 此时会出现一个对话框。
2. **点击 添加账户。** 账户向导将出现，如图 3-2 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_376_0.png)

图 3-2：Thunderbird 的账户向导引导你完成新闻组账户的设置。

3. **选择 新闻组账户 单选按钮**（参考图 3-2）**并点击 下一步。**
4. **在随后出现的屏幕上，填写你的身份信息——姓名和电子邮件地址——然后点击 下一步** 以进入下一个屏幕。
5. **输入你的新闻服务器名称并点击 下一步。**
6. **输入新闻组账户的描述性名称并点击 下一步。**
7. **点击 完成 以完成新闻组账户设置。**

新的新闻组账户现在出现在 Thunderbird 窗口左侧的账户列表中。点击新闻组账户名称，窗口右侧将显示该新闻组账户的选项。

点击 订阅新闻组 链接。Thunderbird 开始从新闻服务器下载新闻组列表。

![](img/11709a8f88c8cd03868a929dc94c0e2b_377_0.png)

如果你的 ISP 新闻服务器需要用户名和密码，系统会提示你输入这些信息。之后，Thunderbird 将下载新闻组列表并在订阅对话框中显示它们。（你可以在文本框中输入搜索字符串以缩小列表范围。）当你找到想要的新闻组时，勾选复选框以订阅这些新闻组，如图 3-3 所示。然后点击 确定 关闭对话框。

![](img/11709a8f88c8cd03868a929dc94c0e2b_377_1.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_377_2.png)

订阅新闻组后，这些新闻组将出现在 Thunderbird 窗口左侧新闻组账户名称下方。然后你可以按照以下步骤阅读新闻组：

1. **点击新闻组名称**（例如，comp.os.linux.announce）。如果你的新闻服务器需要用户名和密码，对话框将提示你输入此信息。随后，另一个对话框会询问你要下载多少条消息头。
2. **指定你要下载的消息头数量**（例如，500）并点击 下载 以继续。Thunderbird 将从新闻组下载消息头，并在窗口的右上角区域显示列表。
3. **从消息头列表中，点击某一项以阅读该文章，如图 3-4 所示。**

要选择其他已订阅的新闻组，只需点击窗口左侧的新闻组名称即可。

![](img/11709a8f88c8cd03868a929dc94c0e2b_378_0.png)

图 3-4：点击文章以在窗口右下角部分阅读它。

# 新闻组订阅

与杂志或报纸不同，新闻组不需要你进行订阅；你可以阅读新闻服务器上任何可用的新闻组。然而，新闻服务器管理员可能会决定排除某些新闻组；如果未被包含在内，你就无法阅读它们。

唯一可以被称为*订阅*的行为是指定你通常希望阅读的新闻组。新闻服务器不会接收任何此类订阅信息——这些信息仅由新闻阅读器使用，以确定从新闻服务器下载哪些内容。

# 发布新闻

你可以使用任何新闻阅读器将新闻文章（新条目或对旧帖的回复）发布到一个或多个新闻组。发布新闻项的具体命令取决于新闻阅读器。例如，在 Thunderbird 新闻阅读器中，发布文章需遵循以下步骤：

1. 点击工具栏上的**回复**按钮，以发布你所阅读新闻项的后续回复。若要发布新的新闻文章，请点击**撰写**按钮。将出现一个窗口，你可以在其中撰写消息。

第四册
第三章
阅读
新闻组和
RSS 源

## **354 从你的 ISP 阅读新闻组**

2. **输入新闻组的名称，就像发送电子邮件时输入收件人地址一样。输入主题和你的消息。**

   对于这次测试发布，请输入 `ignore`（忽略）作为主题行，并输入 `misc.test` 作为新闻组名称。否则，任何收到你文章的网站都会通过邮件回复以告知你文章已到达该站点；这符合 `misc.test` 新闻组的目的。

3. **完成消息撰写后，点击工具栏上的 发送。**

   Thunderbird 将消息发送到新闻服务器，新闻服务器进而将其发送到其他新闻服务器，很快它就将传遍全世界！

4. **为了验证测试消息是否到达新闻组，请选择 文件 订阅。然后订阅 `misc.test` 新闻组（你最近发布新文章的地方）。查看 `misc.test` 中的最新文章（或其中较新的一篇文章）；它应该就是你最近发布的那篇文章。**

如果你发布了一篇文章并立即阅读该新闻组，你会看到新文章，但这并不意味着文章已经到达互联网上的其他站点。毕竟，由于你是在新闻服务器上发布的文章，你的帖子会立即出现在你的新闻服务器上。由于新闻分发的存储和转发模型，新闻文章会逐渐从你的新闻服务器传播到世界各地的其他服务器。

![](img/11709a8f88c8cd03868a929dc94c0e2b_379_0.png)

`misc.test` 新闻组提供了一种方式来检查你的新闻发布是否真正在传播。如果你在该新闻组发布内容且主题中不包含单词 `ignore`，新闻服务器会通过向文章头部 Reply-To（回复至）字段中列出的地址发送电子邮件消息来确认收到该文章。

# **使用 KNode**

Debian、MEPIS 和 SUSE 提供 KNode 作为默认新闻阅读器。通常，你可以通过从菜单中选择 新闻阅读器 来启动 KNode（查看 Internet 应用程序部分）。如果你在菜单中看不到 新闻阅读器 选项，请在终端窗口中输入 `knode` 以启动 KNode。

当 KNode 首次运行时，它会弹出“配置 KNode”对话框，如图 3-5 所示，通过它可以配置阅读新闻组和向新闻组发布条目所需的一切。

对话框左侧显示所有可配置项，右侧是你为当前在左侧选定的项输入信息的地方。





当首次打开 KNode 配置对话框时，它会提示输入您的个人信息。请输入您的识别信息，如姓名、电子邮件地址和组织名称——当您向新闻组发布新条目时，将使用这些信息。

然后，点击左侧的“账户”（参见图 3-5），并点击右侧的“新闻组服务器”选项卡，以设置有关您将要从中阅读新闻的新闻服务器的信息。点击“新闻组服务器”选项卡中的“新建”，会弹出一个对话框（见图 3-6），您可以在其中输入有关新闻服务器的信息。您的 ISP（互联网服务提供商）应该已提供访问新闻服务器所需的信息。如果新闻服务器需要登录名和密码，您也必须输入这些信息。

设置好新闻账户后，KNode 窗口左侧将显示新闻服务器的名称，如图 3-7 所示。右键单击服务器名称，并从弹出菜单中选择“订阅新闻组”。随后会出现一个对话框，您可以在其中订阅选定的新闻组（例如 `comp.linux.announce`）。

图 3-7 展示了在阅读已订阅新闻组中的某篇文章时，KNode 窗口的典型视图。KNode 的用户界面与其他许多邮件和新闻阅读器类似，包括 Thunderbird。

![](img/11709a8f88c8cd03868a929dc94c0e2b_380_0.png)

## 356 从您的 ISP 阅读新闻组

![](img/11709a8f88c8cd03868a929dc94c0e2b_381_0.png)
![](img/11709a8f88c8cd03868a929dc94c0e2b_381_1.png)

###### 在网站上阅读和搜索新闻组

如果您无法通过 ISP 访问新闻组，您仍然可以在许多网站上阅读新闻组并发布文章。其中一些网站存档了旧的新闻文章，并提供了良好的搜索功能，因此您可以搜索这些网站以查找与您可能提出的问题相关的文章。

通过网站阅读新闻组的最大优点是，您甚至不需要访问新闻服务器，就可以从网页浏览器阅读新闻。

表 3-2 列出了提供免费访问 Usenet 新闻组的网站。一些网站提供收费的 Usenet 新闻组服务。本文未在此列出这些网站，但您可以通过 Google ([www.google.com](https://www.google.com)) 搜索它们——输入搜索词 usenet newsgroup access 即可获得提供新闻组访问服务的所有网站列表（包括收费的网站）。

表 3-2 提供免费访问 Usenet 新闻组的网站

| 网站 | URL |
| --- | --- |
| Google Groups | http://groups.google.com |
| mail2web | http://usenet.mail2web.com |
| InterBulletin | http://news.interbulletin.com |
| Usenet Replayer | www.usenet-replayer.com |
| Mailgate | www.mailgate.org |

阅读新闻组、发布文章以及搜索旧新闻组存档的最佳场所之一是 Google Groups——Google 的 Usenet 讨论论坛——位于网络上的 http://groups.google.com。在该网站上，您可以选择要浏览的新闻组，并可以在各种新闻组上发布的文章回复中发布新回复。

Google Groups 的最佳特性是其搜索功能。您已经知道 Google 的网络搜索有多好；您可以获得同样全面的搜索功能，以查找与您的搜索词相关的新闻组帖子。要搜索新闻组，请填写 http://groups.google.com 上的搜索表单并按 Enter 键。

要在 Google Groups 中浏览新闻组，请忽略搜索框，查看高级别新闻组类别列表，例如 alt、comp 和 soc。点击类别，您可以逐渐深入到具体的新闻组。在 Google Groups 中查看文章时，您可以点击一个链接，该链接允许您发布对该文章的后续回复。

![](img/11709a8f88c8cd03868a929dc94c0e2b_382_0.png)

####### 阅读 RSS 源

RSS 代表 Really Simple Syndication（简易信息聚合）。RSS 是一种用于*聚合*——收集和提供——网站内容的格式，主要用于以新闻为主的网站和博客。*blog* 一词是 weblog 的缩写——一个由博客创建者频繁更新的、包含其想法、评论和观点的日志。RSS 可用于提供可以分解为离散条目并放入 RSS 格式的任何类型的信息。这种 RSS 格式的内容称为 *RSS 源*，具备 RSS 识别能力的程序可以定期检查该源的变化，下载新条目，并将其提供给用户。

RSS 格式是 XML（eXtensible Markup Language，可扩展标记语言）的一种方言。所有 RSS 文件都符合 XML 1.0 规范。

RSS 有许多版本，但三个版本——0.91、1.0 和 2.0——正在广泛使用。Netscape 设计了 RSS 0.90 版本，用于收集和显示新闻网站的标题。一个更简单的版本 0.91 被提出，UserLand Software 采用了该版本用于其博客产品。与此同时，另一个非商业团体已将 RSS 0.90 演变为基于资源描述格式或 RDF（参见 `www.w3.org/rdf`）的 RSS 1.0。UserLand 没有接受 RSS 1.0，而是继续将 RSS 0.91 演变为 0.92、0.93、0.94 版本，并最终定为 RSS 2.0（跳过 1.0，因为该版本号已被占用）。目前，许多博客和网站使用 RSS 0.91 进行基本聚合（标题、URL 和描述）；对使用 RDF 的阅读器使用 RSS 1.0；对具有更多元数据的高级聚合使用 RSS 2.0。（可以将元数据理解为*关于数据的数据*，这就是 RSS 格式所提供的：它提供有关其他信息（如博客和新闻）的数据。）RSS 1.0 文件具有 `.rdf` 扩展名，而 RSS 0.91 和 2.0 文件具有 `.xml` 扩展名。然而，所有 RSS 文件都是使用 XML 标签的文本文件。

![](img/11709a8f88c8cd03868a929dc94c0e2b_383_0.png)

####### 检查 RSS 源

RSS 源是一个包含 XML 标签的文本文件，用于描述网站的内容。通常，您使用自动程序定期生成 RSS 源文件，但您也可以使用文本编辑器准备 RSS 源文件。了解 RSS 源的外观是有益的，这样您就可以调试源的问题。

RSS 源的具体细节取决于 RSS 的版本。最简单的源是 RSS 0.91，以下是一个典型的 RSS 0.91 源：

```xml
<?xml version="1.0" ?>
<!-- A comment line -->
<rss version="0.91">
<channel> <!-- This tag specifies general information about the feed-->
<title>Title of this feed</title>
<link>URL of this feed, for example, http://naba.typepad.com/</link>
<description>Brief description of feed</description>
<language>en-us</language>
<item>
<title>Title of this item</title>
<link>URL for this item</link>
<description>Description of this item</description>
</item>
... more items ...
</channel>
</rss>
```

如您从上述列表所见，RSS 源包含一个频道，具有标题、链接、描述和语言，随后是一系列条目，每个条目都有标题、链接和描述。

![](img/11709a8f88c8cd03868a929dc94c0e2b_384_0.png)

对于使用 RDF 格式的 RSS 1.0，其格式更加冗长。RSS 1.0 本质上提供了 RSS 0.91 中的基本信息，并添加了更多细节，如条目级别的作者、主题和发布日期，而 RSS 0.91 不支持这些。

####### 阅读 RSS 源

有许多 GUI 程序可用于订阅 RSS 源并阅读源中的条目。这些程序被称为 RSS *聚合器*，因为它们可以从许多 RSS 源收集信息，并使所有内容在一个地方可用。

有两种类型的 RSS 聚合器——Web 浏览器插件和独立程序。浏览器插件，如 NewsMonster ([www.newsmonster.org](http://www.newsmonster.org))，在 Web 浏览器中运行，以便源显示在 Web 浏览器中。独立程序，如 GNOME Straw ([www.nongnu.org/straw](http://www.nongnu.org/straw)) 和 KDE Akregator ([http://akregator.sourceforge.net](http://akregator.sourceforge.net))，是完整的 GUI 应用程序，通常与其他邮件和新闻阅读器程序外观相似。

![](img/11709a8f88c8cd03868a929dc94c0e2b_384_1.png)

Fedora、MEPIS 和 SUSE 都配备了 Akregator 程序，这是一个独立的 RSS 源聚合器。要运行它，请在 GUI 桌面的应用程序菜单中寻找链接，但如果您没有看到它列在那里，请在终端窗口中输入 `akregator`。在 Debian 中，您可以通过输入 `apt-get install akregator` 来安装 Akregator（在输入 `su -` 成为 `root` 之后）。





####### Akregator 首次运行

当 Akregator 首次运行时，它会显示主窗口，其中没有任何 RSS 订阅源。要订阅源，请从菜单中选择“Feed▸Add Feed”，或在窗口左侧窗格中右键单击“All Feeds”（见图 3-8），然后从弹出菜单中选择“Add Feed”。接着，在“Add Feed”对话框中输入订阅源的 URL，并单击“OK”。例如，要读取 Slashdot 的 RSS 订阅源，我会输入 `http://slashdot.org/index.rss`。订阅源的标题会显示在窗口的左侧窗格中。单击订阅源标题即可查看该订阅源中的项目。然后，你可以单击右上角窗格中的某个项目，该项目会显示在右下角窗格中，如图 3-8 所示。你可以添加许多不同的 RSS 订阅源，将它们整理到文件夹中，并在 Akregator 中浏览它们。

![](img/11709a8f88c8cd03868a929dc94c0e2b_385_0.png)

##### 第 4 章：使用 FTP

###### 本章内容

-   使用 GNOME FTP 客户端
-   使用任意 Web 浏览器作为 FTP 客户端
-   了解 FTP 命令

顾名思义，*文件传输协议*（FTP）用于在计算机之间传输文件。例如，如果你的互联网服务提供商（ISP）为你提供了一个个人网站空间，你可能已经使用 FTP 上传了构成该网站的文件。使用你电脑上的 FTP 客户端，你可以登录到你的 ISP 账户，提供密码，然后将文件从你的家庭系统复制到 ISP 的服务器。

你还可以使用 FTP 匿名下载其他文件，例如从互联网上其他计算机下载开源软件——在这种情况下，你不需要在远程系统上有账户即可下载文件。你只需使用单词 *anonymous* 作为用户名，并提供你的电子邮件地址作为密码即可登录。（事实上，你的 Web 浏览器可以代表你完成这些操作，因此你可能甚至不知道这个过程正在发生。）这种类型的匿名 FTP 非常适合向任何想要获取文件的人分发文件。例如，硬件供应商可能会使用匿名 FTP 向任何需要的人提供更新后的设备驱动程序。

Linux 附带了多种 FTP 客户端，既有命令行版本的，也有图形界面版本的。在本章中，我将向你介绍几个图形界面 FTP 客户端，并针对命令行 FTP 客户端，描述你操作远程目录时使用的命令。

###### 使用图形界面 FTP 客户端

你可以在 Linux 中使用以下其中一种图形界面 FTP 客户端：

-   gFTP — GNOME 的图形界面 FTP 客户端 (http://gftp.seul.org)
-   KBear — KDE 的图形界面 FTP 客户端 (http://kbear.sourceforge.net)
-   Web 浏览器，如 Firefox，用于匿名 FTP 下载

对于上传文件，你可能希望使用 gFTP，因为此类传输通常需要提供用户名和密码。Web 浏览器非常适合匿名下载，这也是你通常从互联网下载软件的方式。

我将在接下来的两个部分中简要介绍这三个图形界面 FTP 客户端。

####### 使用 gFTP

GNOME 附带了 gFTP，一个图形界面 FTP 客户端。gFTP 默认未安装，但你可以从 [http://gftp.seul.org](http://gftp.seul.org) 下载并轻松安装。在某些发行版中，它可能已包含在某个软件包中，你只需安装该软件包即可。

![](img/11709a8f88c8cd03868a929dc94c0e2b_387_0.png)

在 Debian 中，在终端窗口中输入 `su -` 并输入 root 密码，然后输入 `apt-get install gftp`。

![](img/11709a8f88c8cd03868a929dc94c0e2b_387_1.png)

在 Fedora Core 中，从本书的配套 DVD 安装 gFTP。以 *root* 身份登录，将 DVD 插入 DVD 光驱，并在终端窗口中输入 `mount /mnt/cdrom`。（如果 DVD 光驱是你系统中的第二个 CD/DVD 光驱，你可能需要将 `cdrom` 更改为 `cdrom1`。）然后输入 `cd /mnt/cdrom/Fedora/RPMS`，接着输入 `rpm -ihv gftp`。

在 Fedora Core 中，通过选择主菜单\Internet\gFTP 来启动 gFTP（如果你看不到 gFTP，请以 *root* 身份登录并输入 `yum install gftp`，然后在菜单中寻找它）。在其他发行版中，你应该能在主菜单中找到它。gFTP 窗口将显示，如图 4-1 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_387_2.png)

**图 4-1：** 刚与 FTP 服务器建立连接后的 gFTP 窗口。

![](img/11709a8f88c8cd03868a929dc94c0e2b_387_3.png)

gFTP 窗口有一个菜单栏，包含用于执行各种任务的菜单。菜单栏正下方是一个工具栏，上面有许多按钮和文本字段。在这里，你可以输入远程主机的名称或 IP 地址、登录远程主机所需的用户名和密码。图 4-1 显示了在填入此信息并通过单击工具栏上最左侧显示两台计算机图标的按钮与远程主机建立连接后的 gFTP 窗口。

若要使用 gFTP 上传或下载文件，请遵循以下步骤：

1.  **在 Host 字段中填入远程系统的主机名或 IP 地址。**
    如果你之前使用过该主机，可以在单击 Host 字段旁边的向下箭头时，从出现的下拉列表中选择它。
2.  **在 User 字段中提供用户名，在 Pass 字段中提供密码，并单击带有两台计算机图标的按钮（位于 Host 字段左侧）。**
    此操作将导致 gFTP 连接到你选择的主机，并使用你提供的用户名和密码登录。gFTP 窗口的下半部分显示两个系统之间交换的 FTP 协议消息。
3.  **观察此区域是否有任何错误消息的指示。**
    远程系统的目录列表显示在 gFTP 窗口的右半部分。左半部分显示当前本地目录。
4.  **若要上传一个或多个文件从当前系统到远程系统，请在左侧列表中选择文件，然后单击右箭头按钮。**
5.  **若要下载远程系统的文件，请在右侧列表中选择文件名，并单击左箭头按钮。**
6.  **完成文件传输后，从菜单中选择 FTP:: Quit。**

正如这些步骤所示，使用图形界面 FTP 客户端（如 gFTP）传输文件是一项简单的任务。

> 信不信由你，gFTP 不仅用于 FTP 传输。它还可以使用 HTTP 协议传输文件，并使用 Secure Shell (SSH) 协议进行安全文件传输。

####### 介绍 KBear

KBear 是 KDE 的图形界面 FTP 客户端。在 KDE 桌面上，你可以在主菜单（在 Internet 类别中）找到它。在 Debian 中，输入 `apt-get install kbear` 来安装 KBear（在你输入 `su -` 成为 `root` 之后）。

当你第一次启动 KDE 时，它会运行 KBear 向导，允许你配置 KBear。此配置步骤主要涉及 KBear 窗口的布局，因此你可以直接接受默认设置。

当主 KBear 窗口出现时，它显示你的主文件夹，视图类似于 Windows 资源管理器。若要连接到 FTP 服务器，请选择“FTP Quick Connect”。一个对话框（见图 4-2）会提示你输入 FTP 服务器的主机名以及用户名和密码。

![](img/11709a8f88c8cd03868a929dc94c0e2b_389_0.png)

输入所需信息后，单击“Connect”。KBear 将与远程 FTP 服务器建立连接。在图 4-3 所示的 KBear 主窗口中，你可以看到本地和远程目录并排显示。

现在，你可以通过将文件从一个系统的文件夹拖动到另一个系统的文件夹来传输文件，从而使 FTP 传输变成普通的拖放文件复制。

当你使用完 KBear 时，选择“FTP Quit”或单击工具栏上的电源按钮（最左侧的按钮）。

####### 使用 Web 浏览器作为 FTP 客户端

任何 Web 浏览器都可以充当 FTP 客户端，但此类程序最适合用于匿名 FTP 下载，此时 Web 浏览器可以使用匿名用户名和任意密码登录。

![](img/11709a8f88c8cd03868a929dc94c0e2b_390_0.png)

例如，你可以使用 Firefox Web 浏览器作为 FTP 客户端。你唯一需要知道的是如何编写 URL，以便 Web 浏览器知道你想使用 FTP 下载文件。FTP URL 的语法如下：

```
ftp://hostname/pathname
```

第一部分（`ftp://`）表示你想要进行 FTP 传输。主机名部分是 FTP 服务器的名称（名称通常以 ftp 开头——例如，ftp.netscape.com）。路径名是你想要下载的文件所在的完整目录路径和文件名。

如果你只提供 FTP 服务器的主机名，Web 浏览器将显示匿名 FTP 目录的内容。如果你想访问你 Linux 系统上的匿名 FTP，请启动 Firefox（单击 GNOME 面板上的 Web 浏览器图标），在“Location”文本框中输入 FTP URL，然后按 Enter。例如，在我的系统上，我输入 `ftp://localhost/pub/` 来访问 pub 目录。

图 4-4 展示了 Firefox 中匿名 FTP 目录的典型外观。你可以单击文件夹查看其内容并下载任何文件。虽然我展示了如何使用 Firefox 的 FTP 功能访问本地系统，但 FTP 的目的（当然）是从其他系统下载文件到你的系统。





## 366 使用命令行 FTP 客户端

图 4-4：你可以使用网络浏览器从匿名 FTP 服务器下载文件。

**警告！**

当你使用 `ftp://localhost/` URL 时，如果你没有运行 FTP 服务器，或者你设置了防火墙以禁止 FTP 连接，系统将不会有任何响应。

**特定发行版说明**

在 Debian 和 Fedora Core 中，以 *root* 身份登录并在终端窗口中输入 `etc/init.d/vsftpd start` 以启动 FTP 服务器。在 SUSE 中，`xinetd` 超级服务器控制 FTP 服务器 `vsftpd`。配置文件 `/etc/xinetd.d/vsftpd` 指定了 `vsftpd` 的启动方式。有关 `xinetd` 配置文件的更多信息，请参阅第七卷第一章。

访问匿名 FTP 站点的方法同样适用于输入其他匿名 FTP 服务器主机名的情况。例如，尝试输入以下 URL：

```
http://ftp.netscape.com/
```

你将看到 `ftp.netscape.com` 服务器的目录。

###### 使用命令行 FTP 客户端

了解如何从命令行使用 FTP 是个好主意——以备不时之需。例如，如果你的图形界面桌面无法工作，你可能需要下载一些文件来修复问题。如果你知道如何使用命令行 FTP 客户端，你就可以下载文件并处理这个问题。这并不难，并且所有 Linux 发行版都提供命令行 FTP 客户端。

了解命令行 FTP 客户端的最佳方法是亲自尝试一下。该命令名为 `ftp`，你可以在你的 Linux 系统中运行 `ftp` 命令。你甚至不需要互联网连接，因为你可以使用 `ftp` 命令连接到自己的系统——我会展示给你看。

请注意，`ftp` 命令的具体输出可能有所不同，因为一些发行版（例如 Debian）使用 gFTP 的文本模式版本作为命令行 FTP 客户端。

在以下示例 FTP 会话中，我使用命令行 FTP 客户端通过我的用户名（*naba*）登录，并浏览我的一台 Linux 系统上的目录。当你尝试类似的操作时，请用你的用户名替换该名称，并提供你的密码。以下是展示与典型命令行 FTP 客户端交互的列表（我的评论以*斜体*显示，我输入的文字为**粗体**）：

```
ftp localhost
Connected to localhost.localhost.
220 (vsFTPd 2.0.3)
Name (localhost:naba):   (我按下 Enter。)
331 Please specify the password.
Password:                 (我输入我的密码。)
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> help                (我输入 help 以查看 FTP
命令列表。)
Commands may be abbreviated.  Commands are:
!		debug		mdir		qc				 send
$		dir		mgmt		sendport		site
account	disconnect	mkdir	put			size
append		exit		mls		pwd			status
ascii		form		mode		quit			struct
bell		get		mtime		quote		system
binary		glob		mput		recv			unique
bye		hash		nsnewer		reget			tenex
case		help		map		restart		tick
cd		idle		nlist		rhelp		trace
cdup		image		ntrans		rename		type
chmod		lcd		open		reset		user
close		ls		prompt		restart		umask
cr		mcd		passive		mmkdir		verbose
delete		mdelete		proxy		runique		?
```

```
ftp> help mget            (我可以获取关于特定命令的帮助。)
mget			 get multiple files
ftp> cd /var (这将目录更改为 /var。)
250 Directory successfully changed.
ftp> ls      (此命令列出
目录的内容。)
227 Entering Passive Mode (127,0,0,1,38,142)
150 Here comes the directory listing.
. . . lines deleted . . .
226 Directory send OK.
ftp> bye     (此命令结束会话。)
221 Goodbye.
```

## 368 使用命令行 FTP 客户端

如上所示，通过输入命令 `ftp hostname` 可以启动命令行 FTP 客户端，其中 `hostname` 是你想要访问的系统名称。当 FTP 客户端与远程系统上的 FTP 服务器建立连接时，FTP 服务器会提示你输入用户名和密码。在你提供信息后，FTP 客户端显示 `ftp>` 提示符，你可以开始输入命令来执行特定任务。如果你记不住某个特定的 FTP 命令，请键入 `help` 以查看命令列表。你可以通过键入 `help command` 来获取关于特定命令的额外帮助，其中 `command` 是你需要帮助的内容。

许多 FTP 命令类似于用于浏览文件系统的 Linux 命令。例如，`cd` 更改目录，`pwd` 打印当前工作目录的名称，`ls` 列出当前目录的内容。另外两个常用命令是 `get` 和 `put`；`get` 用于从远程系统下载文件到你的系统，而 `put` 用于上传（发送）文件从你的系统到远程主机。

表 4-1 描述了一些常用的 FTP 命令。你不需要输入完整的 FTP 命令。对于长命令，你只需要输入前几个字符——足以唯一识别该命令。例如，要删除文件，你可以输入 `dele`，要将文件传输模式更改为二进制，你可以输入 `bin`。

从互联网下载文件时，你几乎总是希望以二进制模式传输文件，因为软件通常以二进制形式归档和压缩。（它们的文件不是纯文本文件。）因此，始终使用 `binary` 命令将模式设置为二进制。然后使用 `get` 命令下载文件。

在传输多个名称相似的文件（例如 `image1.jpg`、`image2.jpg`、`image3.jpg` 等）时，键入 `prompt` 以关闭提示。（否则，FTP 客户端将在每次文件传输后询问你是否要传输下一个文件。）然后键入 `mget`，后跟带有通配符的文件名。例如，要下载所有以 `image` 开头且以 `.jpg` 扩展名结尾的文件，键入 `mget image*.jpg`。

**表 4-1：常用 FTP 命令**

| 命令 | 描述 |
| :--- | :--- |
| `!` | 在本地系统上执行 shell 命令。例如，`ls` 列出本地系统当前目录的内容。 |
| `?` | 显示命令列表（与 `help` 相同） |
| `append` | 将本地文件追加到远程文件 |
| `ascii` | 将文件传输类型设置为 ASCII（或纯文本）。此命令是默认的文件传输类型。 |
| `binary` | 将文件传输类型设置为二进制 |
| `bye` | 结束与远程 FTP 服务器的 FTP 会话并退出 FTP 客户端 |
| `cd` | 更改远程系统上的目录。例如，`cd /pub/Linux` 将远程目录更改为 `/pub/Linux`。 |
| `chmod` | 更改远程文件的权限设置。例如，`chmod 644 index.html` 更改远程系统上 `index.html` 文件的权限设置。 |
| `close` | 结束与 FTP 服务器的 FTP 会话并返回到 FTP 客户端的提示符 |
| `delete` | 删除远程文件。例如，`delete bigimage.jpg` 删除远程系统上的该文件。 |
| `dir` | 列出远程系统上当前目录的内容 |
| `disconnect` | 结束 FTP 会话并返回到 FTP 客户端的提示符。（此命令与 `close` 相同。） |
| `get` | 下载远程文件。例如，`get junk.tar.gz` 从远程系统下载文件 `junk.tar.gz` 并将其保存为本地系统上的文件 `junk.tgz`。 |
| `hash` | 开启或关闭显示文件传输进度的哈希标记 (#) 打印。当此功能开启时，每从远程系统传输 1,024 字节，屏幕上就会打印一个哈希标记。（这是进度条的命令行版本。） |
| `help` | 显示命令列表 |
| `image` | 与 `binary` 相同 |
| `lcd` | 更改本地系统上的当前目录。例如，`lcd /var/ftp/pub` 将当前本地目录更改为 `/var/ftp/pub`。 |
| `ls` | 列出当前远程目录的内容 |
| `mdelete` | 删除远程系统上的多个文件。例如，`mdelete * .jpg` 删除当前目录中所有名称以 `.jpg` 结尾的远程文件。 |
| `mdir` | 列出多个远程文件并将列表保存在指定的本地文件中。例如，`mdir /usr/share/doc/w* > wlist` 将列表保存在名为 `wlist` 的本地文件中。 |
| `mget` | 下载多个文件。例如，`mget * .jpg` 下载所有名称以 `.jpg` 结尾的文件。如果提示已开启，FTP 客户端会在下载每个文件前请求确认。 |

第四卷
第 4 章
使用 FTP





###### 表 4-1（续）

| 命令 | 描述 |
|---|---|
| **mkdir** | 在远程系统上创建目录。`mkdir images` 会在远程系统的当前目录下创建一个名为 `images` 的目录。 |
| **mls** | 与 **mdir** 相同 |
| **mput** | 上传多个文件。例如，`mput *.jpg` 会将所有文件名以 `.jpg` 结尾的文件发送到远程系统。如果提示已开启，FTP 客户端会在发送每个文件前要求确认。 |
| **open** | 打开与指定主机上的 FTP 服务器的连接。例如，`open ftp.netscape.com` 将连接到主机 `ftp.netscape.com` 上的 FTP 服务器。 |
| **prompt** | 开启或关闭提示功能。当提示功能开启时，在进行多文件传输期间，FTP 客户端会在下载或上传每个文件前要求您确认。 |
| **put** | 将文件发送到远程系统。例如，`put index.html` 将本地系统中的 `index.html` 文件发送到远程系统。 |
| **pwd** | 显示远程系统当前目录的完整路径名。当您以用户身份登录时，初始当前工作目录是您的主目录。 |
| **quit** | 与 **bye** 相同 |
| **recv** | 与 **get** 相同 |
| **rename** | 重命名远程系统上的文件。例如，`rename old.html new.html` 会在远程系统上将文件 `old.html` 重命名为 `new.html`。 |
| **rmdir** | 删除远程系统上的目录。例如，`rmdir images` 将删除远程系统当前目录下的 `images` 目录。 |
| **send** | 与 **put** 相同 |
| **size** | 显示远程文件的大小。例如，`size bigfile.tar.gz` 显示该远程文件的大小。 |
| **status** | 显示 FTP 客户端的当前状态 |
| **user** | 向 FTP 服务器发送新的用户信息。例如，`user naba` 会发送用户名 `naba`；随后 FTP 服务器会提示输入该用户的密码。 |

## 第五卷

### 系统管理

第五波浪

作者：Rich Tennant

![](img/11709a8f88c8cd03868a929dc94c0e2b_396_0.png)

> “这部分测试旨在告知我们您是否适合从事网络管理工作。”

#### 内容概览

- 第 1 章：介绍基础系统管理... 373
- 第 2 章：管理用户和组 ....... 413
- 第 3 章：管理文件系统 ... 425
- 第 4 章：安装和更新应用程序 ...... 449
- 第 5 章：定制 Linux 内核 ... 473

##### 第 1 章：介绍基础系统管理

###### 本章内容

- 介绍图形化系统管理工具
- 成为 *root*
- 理解系统启动过程
- 盘点系统配置文件
- 通过 /proc 文件系统查看系统信息
- 监控系统性能
- 管理设备
- 调度任务

*系统管理* 或 sysadmin 指为保持计算机系统正常运行所必须执行的任何工作。系统*管理员*（也称为 sysadmin）指负责处理这些任务的人员。

如果您是在家庭或小型办公室运行 Linux，您很可能就是您系统的系统管理员。或者，您可能是一位管理着整个由 Linux 系统组成的局域网（LAN）的系统管理员。无论如何，在本章中，我将向您介绍基础系统管理程序，并展示如何执行一些常见任务。

每个 Linux 发行版都附带了一些图形化工具，用于执行特定的系统管理任务。我将在本章中介绍其中一些图形化工具，并在本书的其他章节中更详细地描述它们。

###### 盘点系统管理任务

那么，系统管理任务包括哪些内容？我随口给出的答案是*任何为了保持系统良好运行而必须做的事情*。更准确地说，系统管理员的职责包括以下内容：

- 添加和删除用户账户。您需要添加新的用户账户并删除不必要的用户账户。如果用户忘记了密码，您需要更改密码。
- **管理打印系统。** 您需要开启或关闭打印队列，检查打印队列的状态，并在必要时删除打印作业。
- **安装、配置和升级操作系统及各种实用工具。** 您需要安装或升级 Linux 操作系统的一部分以及其他属于操作系统的软件。
- **安装新软件。** 您需要安装各种软件包格式（如 RPM 或 DEB）的软件。您还需要下载和解包以源代码形式提供的软件——然后从源代码构建可执行程序。
- **管理硬件。** 有时，您需要添加新硬件并安装驱动程序，以便设备正常工作。
- **进行备份。** 您需要备份文件，无论是通过 Zip 驱动器、USB 记忆棒还是磁带（如果您有磁带驱动器）。
- **挂载和卸载文件系统。** 例如，当您想访问 CD-ROM 上的文件时，您需要将该 CD-ROM 的文件系统挂载到 Linux 文件系统中的一个目录上。您可能还需要挂载软盘，包括 Linux 格式和 DOS 格式。
- **自动化任务。** 您需要安排 Linux 任务自动（在特定时间）或定期（以固定间隔）执行。
- **监控系统性能。** 您可能希望密切关注系统性能，以查看处理器将大部分时间花在哪里，以及系统中空闲和已用内存的量。
- **启动和关闭系统。** 尽管启动系统通常只需给 PC 通电即可，但在关闭 Linux 系统时确实需要小心。如果您的系统设置为图形登录界面，您可以通过选择登录界面上的菜单项来执行关闭操作。否则，请使用 `shutdown` 命令在关闭 PC 电源开关之前停止所有程序。
- **监控网络状态。** 如果您拥有网络连接（无论是局域网、DSL 线路还是电缆调制解调器连接），您可能需要检查各种网络接口的状态，以确保您的网络连接处于正常状态。
- **设置主机和网络安全。** 您需要确保系统文件受到保护，并且您的系统能够防御来自网络的攻击。
- **监控安全性。** 您需要密切关注任何入侵行为，通常通过检查日志文件来实现。

这是一份很长的任务清单！我并未在本章中涵盖所有任务，但这本书的其他部分描述了其中大多数任务。在这里，我将通过介绍一些图形化工具、解释如何成为 root（超级用户）、描述系统配置文件，并展示如何监控系统性能、管理设备以及设置定期任务，来重点介绍一些基础知识。

###### 介绍一些图形化系统管理工具

每个 Linux 发行版都附带用于执行系统管理任务的图形化工具。这些图形化工具会提示您输入信息，然后运行必要的 Linux 命令来执行任务。在以下部分中，我将简要介绍 Debian、Fedora Core、SUSE 和 Xandros 中的图形化系统管理工具。

####### Debian 中的图形化系统管理工具

Debian 默认使用 GNOME 桌面，并提供了一些用于执行系统管理任务的图形化工具。这些工具位于 应用程序 → 系统工具 菜单中。表 1-1 列出了一些常见任务以及启动相应图形化工具的菜单选项。

**表 1-1 在 Debian 中使用图形化工具执行系统管理任务**

| 要执行的操作 | 在 Debian GNOME 桌面中选择以下内容 |
| :--- | :--- |
| 添加或删除软件包 | 应用程序 → 系统工具 → Synaptic 软件包管理器 |
| 更改日期或时间 | 应用程序 → 系统工具 → 时间和日期 |
| 更改密码 | 主菜单 → 设置 → 更改密码 |
| 配置桌面 | 应用程序 → 桌面偏好设置 |
| 配置网络 | 应用程序 → 网络 |
| 格式化软盘 | 应用程序 → 系统工具 → 软盘格式化器 |
| 管理打印机 | 应用程序 → 系统工具 → 打印机 |
| 管理用户账户 | 应用程序 → 系统工具 → 用户和组 |
| 监控系统性能 | 应用程序 → 系统工具 → 系统监视器 |
| 查看系统日志 | 应用程序 → 系统工具 → 系统日志 |

####### Fedora Core 中的图形化系统管理工具

Fedora Core 附带了一套图形化系统配置工具，可以减轻执行典型系统管理杂务的负担。表 1-2 简要总结了启动特定任务图形化工具的菜单选项。





######## 表 1-2 在 Fedora Core 中启动图形界面系统管理工具

| 需要配置或管理的对象 | 选择以下选项启动图形工具 |
| :--- | :--- |
| 日期和时间 | 系统 » 管理 » 日期与时间 |
| 磁盘和 DVD/CD-ROM | 应用程序 » 系统工具 » 磁盘管理 |
| 显示设置 | 系统 » 管理 » 显示 |
| 防火墙设置 | 系统 » 管理 » 安全级别和防火墙 |
| 硬件 | 应用程序 » 系统工具 » 硬件浏览器 |
| 互联网连接 | 系统 » 管理 » 网络 |
| 网络 | 系统 » 管理 » 网络 |
| 偏好设置，如桌面和密码 | 系统 » 偏好设置 |
| 打印机 | 系统 » 管理 » 打印 |
| `root` 密码 | 系统 » 管理 » 根用户密码 |
| 服务器 | 系统 » 管理 » 服务器设置 |
| 软件 | 系统 » 管理 » 添加/删除应用程序 |
| 系统性能 | 应用程序 » 系统工具 » 系统监视器 |
| 用户账户 | 系统 » 管理 » 用户和组 |

####### Knoppix 中的图形界面系统管理工具

Knoppix 是一个 Live CD 发行版，您可以使用它来试用 Linux 或修复现有 Linux 系统中的问题。因此，Knoppix 附带了多个可用于系统管理任务的图形工具。表 1-3 汇总了 Knoppix 中的一些图形工具。

######## 表 1-3 在 Knoppix 中使用图形工具进行系统管理任务

| 要执行的操作 | 在 Knoppix 图形桌面上选择以下选项 |
| :--- | :--- |
| 配置桌面 | 主菜单 » 设置 » 桌面设置向导 |
| 配置 KDE | 主菜单 » 设置 » 控制中心 |
| 配置网络 | 主菜单 » KNOPPIX » 网络/互联网 » 网卡配置 |
| 配置打印机 | 主菜单 » KNOPPIX » 配置 » 配置打印机 |
| 查找文件 | 主菜单 » 查找文件 |
| 管理磁盘分区（用于排查现有 Linux 安装问题） | 主菜单 » 系统 » QTParted |
| 以 `root` 权限打开终端窗口 | 主菜单 » KNOPPIX » Root Shell |
| 启动 Samba 服务器 | 主菜单>KNOPPIX>服务>启动 Samba 服务器 |
| 启动 SSH 服务器 | 主菜单>KNOPPIX>服务>启动 SSH 服务器 |

####### MEPIS 中的图形界面系统管理工具

您可以将 MEPIS 作为 Live CD 运行，也可以将其安装在硬盘上。MEPIS 使用 KDE 桌面，并包含一些用于系统管理任务的图形工具。MEPIS 的独特之处在于 MEPIS OS 中心，它允许您执行系统管理任务。您可以通过选择主菜单>MEPIS OS 中心来启动它。图 1-1 显示了 MEPIS OS 中心的主窗口，您可以通过它安装 MEPIS 到硬盘（当您将 MEPIS 作为 Live CD 运行时）并执行一些系统配置和维护任务。

![](img/11709a8f88c8cd03868a929dc94c0e2b_402_0.png)

除了 MEPIS OS 中心，您还可以使用 KDE 控制中心（选择主菜单>控制中心）进行一些系统管理和配置任务。表 1-4 列出了 MEPIS 中可按特定系统管理任务使用的其他一些图形工具。

######## 表 1-4 MEPIS 中用于系统管理任务的一些图形工具

| 要执行的操作 | 在 MEPIS 图形桌面上选择以下选项 |
| :--- | :--- |
| 配置桌面 | 主菜单>系统>设置>桌面设置向导 |
| 配置 KDE | 主菜单>控制中心 |
| 配置打印机 | 主菜单→系统→设置→打印管理器 |
| 查找文件 | 主菜单→查找文件 |
| 安装软件 | 主菜单→系统→Synaptic 软件包管理器 |
| 管理磁盘分区（用于排查现有 Linux 安装问题） | 主菜单→系统→文件系统→QTParted |
| 管理用户账户 | 主菜单→系统→KUser |
| 以 root 权限打开终端窗口 | 主菜单→系统→终端程序 - 超级用户模式 |

####### SUSE 中的图形界面系统管理工具

在 SUSE 中，选择主菜单→系统→YaST 即可在 YaST 控制中心中开始您的系统管理任务。图 1-2 显示了 YaST 控制中心窗口。

![](img/11709a8f88c8cd03868a929dc94c0e2b_403_0.png)

YaST 控制中心的左侧显示您可以执行的任务类别图标。右侧显示当前选中类别中的具体任务图标。当您点击 YaST 控制中心右侧的某个图标时，会出现一个新的 YaST 窗口，使您能够执行该任务。

####### 介绍一些图形界面系统管理工具

表 1-4 汇总了您在 YaST 控制中心左侧看到的每个类别图标所对应的任务。从表 1-5 第二列的条目中可以看出，YaST 控制中心确实是您处理所有系统管理杂务的一站式购物平台。

######## 表 1-5 YaST 控制中心中按类别划分的任务

| 该类别 | 允许您配置/管理以下内容 |
| :--- | :--- |
| 软件 | 在线更新、安装源、在 Xen 环境中安装、安装到目录、媒体检查、补丁 CD |
| 硬件 | 蓝牙、CD-ROM 驱动器、磁盘控制器、显卡和显示器、硬件信息、IDE DMA 模式、红外设备、游戏杆、键盘布局、鼠标型号、打印机、扫描仪、声音、电视卡 |
| 系统 | `/etc/sysconfig` 编辑器、引导加载程序配置、引导或救援软盘、日期和时间、LVM、语言、PCI 设备驱动程序、分区工具、电源管理、PowerTweak、配置管理器、系统备份、系统恢复、系统服务（运行级别） |
| 网络设备 | DSL、传真、ISDN、调制解调器、网卡、电话应答机 |
| 网络服务 | DHCP 服务器、DNS 服务器、DNS 主机和名称、HTTP 服务器、主机名、Kerberos 客户端、LDAP 客户端、邮件传输代理、NFS 客户端、NIS 客户端、NIS 客户端、NIS 服务器、NTP 客户端、网络服务 (xinetd)、代理、远程管理、路由、SLIP 浏览器、Samba 客户端、Samba 服务器、TFTP 服务器 |
| 安全和用户 | 防火墙、组管理、本地安全、用户管理 |
| 杂项 | 自动安装、提交支持查询、供应商驱动 CD、查看启动日志、查看系统日志 |

####### Ubuntu 中的图形界面系统管理工具

Ubuntu 使用 GNOME 桌面，其菜单组织与 Fedora Core 的 GNOME 桌面类似。您可以在以下菜单中找到 Ubuntu 的图形系统管理工具：**应用程序** → **系统工具**、**系统** → **管理** 以及 **系统** → **偏好设置**。表 1-6 列出了启动某些图形工具的菜单选项。

第四卷
第一章
介绍基础系统管理
379

######## 表 1-6 在 Ubuntu 中启动图形界面系统管理工具

| 需要配置或管理的对象 | 选择以下选项启动图形工具 |
| :--- | :--- |
| 日期和时间 | 系统 » 管理 » 时间和日期 |
| 显示设置 | 系统 » 偏好设置 » 屏幕分辨率 |
| 硬件 | 系统 » 管理 » 设备管理器 |
| 互联网连接 | 系统 » 管理 » 网络连接 |
| 网络 | 系统 » 管理 » 网络连接 |
| 偏好设置，如桌面和默认应用程序 | 系统 » 偏好设置 |
| 打印机 | 系统 » 管理 » 打印 |
| *root* 密码 | 系统 » 管理 » 根用户密码 |
| 服务器 | 系统 » 管理 » 服务器设置 |
| 软件 | 应用程序 » 系统工具 » 添加/删除程序 |
| 系统日志 | 应用程序 » 系统工具 » 系统日志 |
| 系统性能 | 应用程序 » 系统工具 » 系统监视器 |
| 更新 | 系统 » 管理 » Ubuntu 更新管理器 |
| 用户账户 | 系统 » 管理 » 用户和组 |

####### Xandros 中的图形界面系统管理工具

Xandros 被设计为桌面操作系统，因此，您可以轻松地从桌面访问所有功能。对于大多数系统管理任务，您从 Xandros 控制中心开始——选择主菜单 » 控制中心即可到达那里。（图 1-3 展示了您到达那里的样子。）

如您所见，窗口左侧显示了任务类别的树形菜单。您可以点击类别旁边的加号来查看子类别。当您点击某个具体任务时，窗口右侧将显示用于执行该任务的图形界面。

对于某些任务，例如挂载文件系统或添加打印机，您可以通过选择主菜单 » 应用程序 » 系统 » 管理员工具 » Xandros 文件管理器 (管理员) 以系统管理员身份打开 Xandros 文件管理器。系统会提示您输入 `root` 密码。图 1-4 显示了 Xandros 文件管理器窗口，您可以从中执行一些系统管理任务。




###### 如何获取 root 权限

你必须以 *root* 用户登录才能执行系统管理任务。*root* 用户是超级用户，也是系统中唯一拥有执行任何操作所需全部权限的账户。

通常的建议是，你*不要*平时以 *root* 身份登录。当你处于 *root* 状态时，一个小失误就可能让你轻松删除所有文件——尤其是在输入命令时。例如，你可能会输入 `rm *.html` 来删除所有扩展名为 `.html` 的文件。如果不小心在星号（`*`）后面按了空格键会怎样？Shell 会将该命令解析为 `rm *.html` 并——由于 `*` 匹配任何文件名——删除当前目录中的所有内容。这听起来似乎不太可能发生，直到它真的发生在你身上！

####### 使用 `su -` 命令

如果你是以普通用户身份登录的，该如何执行系统管理任务呢？好吧，你可以暂时变成 `root`。如果你正在终端窗口或控制台工作，请输入

```
su -
```

然后根据提示输入 `root` 密码。从这一刻起，你就是 `root` 了。想做什么都行。要恢复到普通用户身份，请输入

```
exit
```

就这么简单！就是这么容易。

顺便说一下，Knoppix 有一个 `root` 用户，但没有 `root` 密码，所以你只需在终端窗口的 Shell 提示符下输入 `su -` 即可变成 `root`。此外，Ubuntu 没有 `root` 用户。要在 Ubuntu 中执行任何需要 `root` 权限的任务，你必须输入 `sudo` 后跟具体命令，并在提示时提供你的普通用户密码。

####### 在 GUI 工具中获取 `root` 权限

大多数 Linux 发行版都包含用于执行系统管理任务的图形界面（GUI）工具。如果你使用这些 GUI 工具来执行需要你是 `root` 的任务，该工具通常会弹出一个对话框，提示你输入 `root` 密码，如图 1-5 所示（Ubuntu 除外，Ubuntu 中的 GUI 工具会提示你输入普通用户密码）。只需输入密码并按下回车键即可。如果你不想使用该工具，请点击取消。

![](img/11709a8f88c8cd03868a929dc94c0e2b_407_1.png)

###### 恢复被遗忘的 root 密码

要执行系统管理任务，你必须知道 `root` 密码。如果忘记了 `root` 密码怎么办？别担心。只需重启电脑，按照以下步骤即可重置 `root` 密码：

- 1. 重启电脑（退出图形界面时选择“重新启动”，或像往常一样开机）。

很快你会看到图形化的 GRUB 引导加载程序界面，其中列出了可启动的操作系统名称。如果你的系统使用 LILO 引导加载程序，请按住 Ctrl+X，并在 `boot:` 提示符下输入 `linux single`，然后按回车。然后继续执行第 4 步。

- 2. 如果你安装了不止一个操作系统，请使用方向键选择 Linux 作为你的操作系统。然后按 A 键。

GRUB 会提示你输入要添加到其默认引导命令中的指令。

- 3. 按下空格键，输入以下内容，然后按回车：

```
single
```

Linux 像往常一样启动，但以单用户模式运行，该模式不需要你登录。Linux 启动后，你会看到以下命令行提示符，末尾带有井号（#），类似于以下示例：

```
sh-3.00#
```

- 4. 输入 `passwd` 命令来更改 `root` 密码，如下所示：

```
sh-3.00# passwd
Changing password for user root.
New password:
```

- 5. 输入你想要使用的新 `root` 密码（屏幕上不会显示该密码），然后按回车。

Linux 会再次要求你输入密码，如下所示：

```
Retype new password:
```

- 6. 再次输入密码并按回车。

如果你在两次输入中输入了相同的密码，`passwd` 命令就会更改 `root` 密码。

- 7. 现在输入 reboot 以重启电脑。

Linux 启动后，会显示熟悉的登录界面。现在你可以使用新密码以 `root` 身份登录了。

![](img/11709a8f88c8cd03868a929dc94c0e2b_409_0.png)

在 SUSE Linux 中，在第 3 步中，输入 **single init=/bin/sh**（而不是 **single**），并且在继续执行第 4 步之前，输入 **mount / -n -o remount,rw**。然后执行第 4 到第 6 步以更改 *root* 密码。更改密码后，输入 **mount / -n -o remount,ro**。然后继续执行第 7 步并重启电脑。

![](img/11709a8f88c8cd03868a929dc94c0e2b_409_1.png)

确保你的 Linux 电脑在*物理*上是安全的。正如这些步骤所示，任何能够物理访问你的 Linux 电脑的人都可以简单地重启，设置新的 *root* 密码，并对系统为所欲为。保护密码不被重置的另一种方法是设置 GRUB 密码，这会导致 GRUB 在引导 Linux 前要求输入有效的密码。当然，你必须在每次启动系统时记得输入 GRUB 密码！

###### 了解 Linux 的启动过程

了解 Linux 在启动时启动进程的顺序非常重要。你可以利用这些知识来启动和停止服务，例如 Web 服务器和网络文件系统（NFS）。接下来的几个部分将概述 Linux 的启动过程以及初始进程集的启动方式。这些部分还将帮助你熟悉启动 Linux 系统中各种服务的 Shell 脚本。

####### 了解 init 进程

当 Linux 启动时，它会从硬盘加载并运行核心操作系统程序。核心操作系统旨在运行其他程序。名为 `init` 的进程启动了你的 Linux 系统中的初始进程集。

要查看当前系统中正在运行的进程，请输入

```
ps ax | more
```

你将得到一个输出列表，开头如下所示：

```
  PID TTY      STAT   TIME COMMAND
    1 ?        S      0:22 init [2]
```

第一列标题为 *PID*，为每个进程显示一个编号。PID 代表进程 ID（identification）——由 Linux 内核分配的序列号。进程列表中的第一个条目，其进程 ID（PID）为 1，就是 `init` 进程。它是第一个进程，启动了你的 Linux 系统中的所有其他进程。这就是为什么 `init` 有时被称为“所有进程的之母”。

init 进程启动的内容取决于以下因素：

- *运行级别*（run level），这是一个标识符，用于识别只允许选定的一组进程存在的系统配置。
- `/etc/inittab` 文件的内容，这是一个文本文件，指定了在不同运行级别下要*启动*哪些进程。
- 在特定运行级别下执行的一组 Shell 脚本。（这些脚本位于 `/etc/init.d` 目录以及 `/etc` 下的几个子目录中——这些子目录的名称以 `rc` 开头。）

大多数 Linux 发行版使用七个运行级别——0 到 6。运行级别的含义因发行版而异。表 1-7 列出了运行级别的含义，并指出了 Fedora Core、Debian、MEPIS、SUSE、Ubuntu 和 Xandros 的一些特定操作。

![](img/11709a8f88c8cd03868a929dc94c0e2b_410_0.png)

| 运行级别 | 含义 |
| :--- | :--- |
| 0 | 关闭系统 |
| 1 | 以单用户独立模式运行（其他人无法登录；你在文本控制台操作） |
| 2 | 以多用户模式运行（Debian、Ubuntu 和 Xandros 使用运行级别 2 作为默认运行级别） |
| 3 | 以完全多用户模式运行（用于 Fedora Core、MEPIS 和 SUSE 中的文本模式登录） |
| 4 | 以完全多用户模式运行（在 Fedora Core、MEPIS 和 SUSE 中未使用） |
| 5 | 以完全多用户模式运行（在 Fedora Core、MEPIS 和 SUSE 中用作图形登录的默认运行级别） |
| 6 | 重启系统 |

![](img/11709a8f88c8cd03868a929dc94c0e2b_410_1.png)

当前的运行级别以及 `/etc/inittab` 文件的内容共同控制在 Linux 中 *init* 启动哪些进程。在 Debian、Ubuntu 和 Xandros 中，默认运行级别是 2。在 Fedora Core、MEPIS 和 SUSE 中，运行级别 3 用于文本模式登录屏幕，而 5 用于图形登录屏幕。你可以通过编辑 `/etc/inittab` 文件中的一行来更改默认运行级别。

要检查当前的运行级别，请在终端窗口中输入以下命令：

```
/sbin/runlevel
```





在 Debian 中，**runlevel** 命令会输出类似下面的结果：

```
N 2
```

输出的第一个字符显示前一个运行级别（N 表示没有前一个运行级别），第二个字符显示当前运行级别（2）。在这种情况下，系统启动于运行级别 2。如果你正在 Fedora Core 或 MEPIS 的图形用户界面（GUI）桌面环境中，**runlevel** 命令应显示 **5** 作为当前运行级别。

######## 检查 /etc/inittab 文件

`/etc/inittab` 文件是理解 `init` 在不同运行级别下启动哪些进程的关键。你可以使用 **more** 命令查看该文件的内容，方法如下：

```
more /etc/inittab
```

要使用 **more** 命令查看 `/etc/inittab` 文件的内容，你无需以 **root** 身份登录。

若要解读 `/etc/inittab` 文件的内容，请遵循以下步骤：

- 1. **查找包含短语 `initdefault` 的那一行。**
   以下是 Debian 系统中 `/etc/inittab` 文件中的那行内容：

   ```
   id:2:initdefault:
   ```

   该行显示了默认运行级别。在本例中，它是 2。

- 2. **查找所有指定 `init` 在运行级别 2 中执行内容的行。寻找一个在前两个冒号 (:) 之间含有数字 2 的行。以下是 Debian 中一个相关的行：**

   ```
   l2:2:wait:/etc/init.d/rc 2
   ```

   这一行指定 `init` 执行文件 `/etc/init.d/rc`，并传入 **2** 作为参数。

如果你在 Debian 系统中查看文件 `/etc/init.d/rc`，会发现它是一个 Shell 脚本。你可以研究该文件，了解它如何为运行级别 **1** 到 **5** 启动各种进程。

`/etc/inittab` 文件中的每个条目都告诉 `init` 在一个或多个运行级别中执行什么操作——你只需列出该进程运行的所有运行级别即可。每个 `inittab` 条目包含四个字段——由冒号分隔——格式如下：

```
id:runlevels:action:process
```

表 1-8 说明了每个字段的含义。

######## 表 1-8: 每个 inittab 条目中字段的含义

| 字段 | 含义 |
| :--- | :--- |
| *id* | 唯一的单字符或双字符标识符。*init* 进程在内部使用此字段。你可以使用任何你想要的标识符，只要不在多行中使用相同的标识符即可。 |
| *runlevels* | 由零个或多个字符组成的序列，每个字符代表一个运行级别。例如，如果 *runlevels* 字段为 12345，则该条目适用于运行级别 1 到 5 中的每一个。如果 *action* 字段设置为 *sysinit*、*boot* 或 *bootwait*，则忽略此字段。 |
| *action* | 告诉 *init* 进程如何处理该条目。例如，如果此字段为 *initdefault*，则 *init* 将 *runlevels* 字段解释为默认运行级别。如果此字段设置为 *wait*，则 *init* 启动 *process* 字段中指定的程序或脚本，并等待该进程退出。 |
| *process* | *init* 启动的脚本或程序的名称。当然，*action* 字段的某些设置不需要 *process* 字段。例如，当 *action* 字段为 *initdefault* 时，不需要 *process* 字段。 |

####### 使用 init 命令尝试新的运行级别

若要尝试新的运行级别，你无需更改 /etc/inittab 文件中的默认运行级别。如果你以 *root* 身份登录，可以通过输入 **init** 后跟运行级别来更改运行级别（以及随之而来的 Linux 中运行的进程）。

例如，要将系统置于单用户模式，请键入以下内容：

```
init 1
```

因此，如果你想在不更改 /etc/inittab 文件中默认运行级别的情况下尝试运行级别 3，请在 Shell 提示符下输入以下命令：

```
init 3
```

系统将终止所有当前进程并进入运行级别 3。默认情况下，*init* 命令会等待 20 秒，然后停止所有当前进程并启动运行级别 3 的新进程。

若要立即切换到运行级别 3，请键入命令 **init -t0 3**。*-t* 选项后的数字表示 *init* 在更改运行级别前等待的秒数。

你还可以使用 `telinit` 命令，它只不过是 `init` 的一个符号链接（快捷方式）。如果你对 `/etc/inittab` 文件进行了更改并希望 `init` 重新加载其配置文件，请使用命令 `telinit q`。

####### 了解 Linux 启动脚本

`init` 进程在系统启动时运行许多脚本。在以下讨论中，我以一个 Debian 系统为例，但其他发行版的基本序列是相似的——只是脚本的名称和位置可能有所不同。

![](img/11709a8f88c8cd03868a929dc94c0e2b_413_0.png)

如果你在 Debian 系统中查看 `/etc/inittab` 文件，你会发现文件开头附近有以下行：

```
# Boot-time system configuration/initialization script.
si::sysinit:/etc/init.d/rcS
```

第一行是一行注释。第二行使 `init` 运行 `/etc/init.d/rcS` 脚本——这是在 Debian 系统中 `init` 运行的第一个 Linux 启动脚本。`rcS` 脚本执行许多初始化任务，如挂载文件系统、设置时钟、配置键盘布局、启动网络以及加载许多其他驱动程序模块。`rcS` 脚本通过调用许多其他脚本并读取位于 `/etc/rcS.d` 目录中的配置文件来执行这些初始化任务。

执行完 `/etc/init.d/rcS` 脚本后，`init` 进程会运行 `/etc/init.d/rc` 脚本，并将运行级别作为参数传入。例如，对于运行级别 2，`/etc/inittab` 中的以下行指定了 `init` 执行的内容：

```
l2:2:wait:/etc/init.d/rc 2
```

此示例说明 `init` 执行命令 `/etc/init.d/rc 2` 并等待该命令完成。

`/etc/init.d/rc` 脚本有点复杂。它是这样工作的：

- 它执行与运行级别对应的目录中的脚本。例如，对于运行级别 2，`/etc/init.d/rc` 脚本运行 `/etc/rc2.d` 目录中的脚本。
- 在与运行级别对应的目录中，`/etc/init.d/rc` 查找所有以 `K` 开头的文件，并用 `stop` 参数执行它们。该参数会终止任何当前运行的进程。然后它查找所有以 `S` 开头的文件，并用 `start` 参数执行每个文件。该参数会启动指定运行级别所需的进程。

若要查看其在运行级别 2 下的执行情况，请键入以下命令：

```
ls -l /etc/rc2.d
```

在生成的列表中，K 脚本——文件名以 K 开头的文件——停止（或终止）服务器，而 S 脚本则启动服务器。/etc/init.d/rc 脚本严格按照它们在目录列表中出现的顺序执行这些文件。

####### 手动启动和停止服务器

在 Linux 中，服务器启动脚本位于 /etc/init.d 目录中。你可以手动调用此目录中的脚本来启动、停止或重启特定进程——通常是服务器。例如，要停止 FTP 服务器（服务器程序名为 vsftpd），请键入以下命令：

```
/etc/init.d/vsftpd stop
```

如果 vsftpd 已经在运行并且你想重启它，请键入以下命令：

```
/etc/init.d/vsftpd restart
```

你可以通过熟悉 /etc/init.d 目录中的脚本来提高你的系统管理技能。要查看其列表，请键入以下命令：

```
ls /etc/init.d
```

脚本名称会给你一些线索，告诉你脚本可以启动和停止哪个服务器。例如，samba 脚本启动和停止 Samba Windows 网络服务所需的进程。你有空的时候，可能想要研究一下这些脚本中的一些，以了解每个脚本的作用。你不必理解所有的 Shell 编程；注释有助于你发现每个脚本的目的。

###### 在系统启动时自动启动服务器

你希望某些服务器在每次启动系统时都自动启动。配置服务器的具体命令因发行版而异。

![](img/11709a8f88c8cd03868a929dc94c0e2b_414_0.png)

在 Fedora Core 和 SUSE 中，使用 chkconfig 命令设置服务器在系统进入特定运行级别时启动。例如，如果你启动了 SSH 服务器，你希望 sshd 服务器在系统启动时始终启动。你可以使用 chkconfig 命令来实现这一点。





若要设置 sshd 在系统启动至运行级别 3、4 或 5 时自动启动，请输入以下命令（此时需以*root*身份登录）：

```
chkconfig --level 345 sshd on
```

在 Fedora Core 和 SUSE 中，你还可以使用*chkconfig*命令来检查哪些服务器处于开启或关闭状态。例如，要查看所有运行级别下所有服务器的完整列表，请输入以下命令：

```
chkconfig --list
```

在 Debian、MEPIS、Ubuntu 和 Xandros 中，你可以使用*update-rc.d*命令来启用服务器在系统启动时自动运行。例如，要将*sshd*设置为在默认运行级别下自动启动，请以*root*身份登录，并在终端窗口中输入*update-rc.d sshd defaults*。你也可以指定确切的运行级别和序列号（即每个服务器启动的顺序）。要了解*update-rc.d*命令的更多信息，请在终端窗口中输入*man update-rc.d*。

![](img/11709a8f88c8cd03868a929dc94c0e2b_415_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_415_1.png)

###### 盘点 Linux 系统配置文件

Linux 包含大量配置文件。所有这些文件都是文本文件，你可以使用任何文本编辑器对其进行编辑。若要编辑这些配置文件，必须以*root*身份登录。我并未逐一讨论这些文件，而是在表 1-9 中展示了一些配置文件的精选列表，并附带对每个文件的简要说明。这份清单让你了解系统管理员需要处理哪些类型的配置文件。在许多情况下，Linux 还包含图形用户界面（GUI）实用程序，用于配置许多此类文件。

####### 表 1-9 部分 Linux 配置文件

| 配置文件 | 描述 |
| :--- | :--- |
| /boot/grub | GRUB 引导加载程序文件的位置 |
| /boot/grub/menu.lst | GRUB 在启动系统前显示的引导菜单的配置文件 |
| /boot/System.map | Linux 内核映射（将内核地址映射为函数和变量的名称） |
| /boot/vmlinuz | Linux 内核（操作系统的核心） |
| /etc/apache2/httpd.conf | Apache Web 服务器的配置文件（Debian 和 MEPIS） |
| /etc/apt/sources.list | 列出高级打包工具（APT）获取包源（FTP 或网站或 CD-ROM）的配置文件（Debian、MEPIS、Ubuntu 和 Xandros） |
| /etc/at.allow | 允许使用 at 命令安排稍后执行任务的用户名列表 |
| /etc/at.deny | 禁止使用 at 命令的用户名列表 |
| /etc/bashrc | bash shell 的系统级函数和别名（Fedora Core） |
| /etc/bash.bashrc | bash shell 的系统级函数和别名（Debian、MEPIS、SUSE、Ubuntu 和 Xandros） |
| /etc/cups/sys.conf | 通用 UNIX 打印系统（CUPS）调度程序的打印机配置文件 |
| /etc/fonts | 包含字体配置文件的目录。（特别是，你可以将本地字体配置设置放入文件 /etc/fonts/local.conf 中。） |
| /etc/fstab | 关于可用于挂载的文件系统及其挂载位置的信息 |
| /etc/group | 关于组的信息 |
| /etc/grub.conf | Fedora Core 和 SUSE 中 GRUB 引导加载程序的配置 |
| /etc/hosts | IP 地址及其对应主机名的列表 |
| /etc/hosts.allow | 允许访问本系统互联网服务的主机 |
| /etc/hosts.deny | 禁止访问本系统互联网服务的主机 |
| /etc/httpd/conf/httpd.conf | Apache Web 服务器的配置文件（Fedora Core） |
| /etc/init.d | 包含用于启动和停止各种服务器的脚本的目录 |
| /etc/inittab | 由 init 进程使用的配置文件，该进程会启动所有其他进程 |
| /etc/issue | 包含在显示文本模式登录提示符之前要打印的消息的文件（通常是发行版名称和版本号） |
| /etc/lilo.conf | Linux 加载器（LILO）的配置——这是一种可以从磁盘加载操作系统的引导加载程序之一（仅当你使用 LILO 引导加载程序时才存在） |
| /etc/login.defs | 用于创建用户账户的默认信息，由 useradd 命令使用 |
| /etc/modprobe.conf | 可加载内核模块的配置文件，由 modprobe 命令使用（Fedora Core 和 SUSE） |
| /etc/modules.conf | 可加载模块的配置文件（Debian、MEPIS 和 Xandros） |
| /etc/mtab | 关于当前已挂载文件系统信息 |
| /etc/passwd | 关于所有用户账户的信息。（实际密码存储在 /etc/shadow 中。） |
| /etc/profile | bash shell 的系统级环境和启动文件 |
| /etc/profile.d | 包含脚本文件（以 .sh 结尾的名称）的目录，由 /etc/profile 脚本执行 |
| /etc/init.d/rcS | Debian、MEPIS、SUSE、Ubuntu 和 Xandros 中的 Linux 初始化脚本 |
| /etc/rc.d/rc.sysinit | Fedora Core 中的 Linux 初始化脚本 |
| /etc/shadow | 包含所有用户账户加密密码的安全文件（只能由 root 读取） |
| /etc/shells | 系统上用户可使用的 shell 列表 |
| /etc/skel | 保存诸如 .bash_profile 等文件初始版本的目录，这些文件会被复制到新用户的 home 目录 |
| /etc/sysconfig | Linux 配置文件（Fedora Core 和 SUSE） |
| /etc/sysctl.conf | 包含内核参数的配置文件，这些参数在系统启动时由 sysctl 读取和设置 |
| /etc/termcap | 终端功能和选项的数据库（Fedora Core 和 SUSE） |
| /etc/udev | 包含 udev 配置文件的目录——udev 是提供动态命名热插拔设备并在 /dev 目录中创建设备文件能力的程序 |
| /etc/X11 | 包含 X 窗口系统（X11）及 gdm 和 xdm 等各种显示管理器配置文件的目录 |
| /etc/X11/XF86Config 或 /etc/X11/xf86config-4 | XFree86 X11 的配置文件（Debian、MEPIS 和 Xandros） |
| /etc/X11/xorg.conf | X.org X11——X 窗口系统的配置文件（Fedora Core、Ubuntu 和 SUSE） |
| /etc/xinetd.conf | xinetd 守护程序的配置，该程序按需启动一系列互联网服务 |
| /etc/yum.conf | yum 包更新器及安装器的配置（Fedora Core） |
| /var/log/apache2 | Web 服务器的访问和错误日志（Debian 和 MEPIS） |
| /var/log/cron | 包含来自运行计划任务进程的 cron 进程的消息的日志文件 |
| /var/log/boot.msg | 包含启动消息的文件（SUSE） |
| /var/log/dmesg | 包含启动消息的文件（Debian、Fedora Core、MEPIS、Ubuntu 和 Xandros） |
| /var/log/httpd | Web 服务器访问和错误日志（Fedora Core） |
| /var/log/messages | 系统日志 |

![](img/11709a8f88c8cd03868a929dc94c0e2b_416_0.png)

###### 监控系统性能

作为系统管理员，你必须密切关注 Linux 系统的运行状况。你可以通过查看诸如以下信息来监控系统的整体性能：

- 中央处理器（CPU）使用率
- 物理内存使用率
- 虚拟内存（交换空间）使用率
- 硬盘使用率

Linux 附带了许多实用程序，你可以使用它们来监控一个或多个此类性能参数。这里我介绍了其中一些实用程序，并展示了如何理解这些实用程序呈现的信息。

####### 使用 top 实用程序

要查看占用 CPU 时间最多的进程——即 CPU 使用率最高的前几个进程——你可以使用文本模式的 top 实用程序。要启动该实用程序，请在终端窗口（或文本控制台）中输入 top。随后，top 实用程序将显示一个文本屏幕，列出当前进程（按 CPU 使用率排序），以及其他各种信息，如内存和交换空间使用情况。图 1-6 显示了 top 实用程序的典型输出。

top 实用程序每五秒更新一次显示。如果你在某个窗口中保持 top 运行，你可以持续监控 Linux 系统的状态。要退出 top，请按 Q 或 Ctrl-C，或关闭终端窗口。

![](img/11709a8f88c8cd03868a929dc94c0e2b_418_0.png)




输出屏幕的前五行（参见图 I-6）提供了有关系统的摘要信息。以下是这五行显示的内容：

- 第一行显示当前时间、系统已启动的时间、当前登录的用户数，以及三个*负载平均值*——即在过去 1、5 和 15 分钟内准备运行的进程的平均数量。
- 第二行列出进程的总数以及这些进程的状态。
- 第三行显示 CPU 使用率——用户*进程*占用了多少百分比的 CPU 时间，系统（内核）*进程*占用了多少百分比，以及 CPU 处于空闲状态的时间百分比。
- 第四行显示物理内存的使用情况——总量、已使用量、可用量，以及分配给*缓冲区*的量（例如用于从硬盘读取数据）。
- 第五行显示虚拟内存（或*交换*空间）的使用情况——交换空间的总量、已使用量、可用量，以及被缓存的量。

摘要信息下方出现的表格（参见图 I-6）列出了关于当前进程的信息，并按照使用的 CPU 时间量降序排列。表 1-10 总结了 `top` 工具显示的表格中各列标题的含义。

**表 1-10 top 工具输出中列标题的含义**

| 标题 | 含义 |
| :--- | :--- |
| PID | 进程 ID |
| USER | 运行该进程的用户名 |
| PR | 进程优先级 |
| NI | 进程的 Nice 值——该值范围从 -20（最高优先级）到 19（最低优先级），默认值为 0。（*nice* 值代表进程的相对优先级：值越高，优先级越低，进程越“体贴”——因为它会让步给其他进程。） |
| VIRT | 进程使用的虚拟内存总量，单位为 KB（千字节） |
| RES | 任务使用的总物理内存（通常以 KiLo-bytes 显示，但如果后缀为 m 则表示兆字节） |
| SHR | 进程使用的共享内存量 |
| S | 进程状态（S 代表休眠，D 代表不可中断休眠，R 代表运行中，Z 代表*僵尸*——本应已终止但仍存在的进程，或者 T 代表已停止） |
| %CPU | 自上次屏幕更新以来占用的 CPU 时间百分比 |
| %MEM | 进程占用的物理内存百分比 |
| TIME+ | 进程自启动以来使用的总 CPU 时间 |
| COMMAND | 启动该进程的命令的缩写形式 |

####### 使用 uptime 命令

你可以使用 `uptime` 命令来获取系统状态的摘要。只需输入如下命令：

```
uptime
```

它会显示类似以下内容的输出：

```
15:03:21 up 32 days, 57 min, 3 users, load average: 0.13, 0.23, 0.27
```

此输出显示当前时间、系统已启动的时间、用户数量，以及（最后）三个负载平均值——即在过去 1、5 和 15 分钟内准备运行的进程的平均数量。负载平均值大于 1 意味着许多进程正在同时竞争 CPU 时间。

负载平均值可以指示系统的繁忙程度。

####### 使用 vmstat 工具

你可以使用 `vmstat` 工具获取关于系统总体使用情况的摘要信息。要查看过去 5 秒间隔内平均的系统使用信息，请键入以下命令（第二个参数表示 `vmstat` 显示输出的总行数）：

```
vmstat 5 8
```

你会看到类似以下列表的输出：

| procs | \ \ \ Memory \ \ | | | | | \ \ \ Swap \ \ | | | | \ \ \ io \ \ | \ \ \ system \ \ | \ \ \ cpu \ \ |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| r | b | swpd | free | buff | cache | si | so | bi | bo | in | cs | us | sy | id | wa |
| 0 | 0 | 31324 | 4016 | 18568 | 136004 | 1 | 1 | 17 | 16 | 8 | 110 | 33 | 4 | 61 | 1 |
| 0 | 0 | 31324 | 2520 | 15348 | 136982 | 0 | 0 | 7798 | 199 | 1157 | 377 | 8 | 8 | 6 | 78 |
| 1 | 0 | 31324 | 1584 | 12936 | 141480 | 0 | 19 | 5784 | 105 | 1099 | 437 | 12 | 5 | 0 | 82 |
| 2 | 0 | 31324 | 1928 | 13004 | 137136 | 7 | 0 | 1586 | 138 | 1104 | 561 | 43 | 6 | 0 | 51 |
| 3 | 1 | 31324 | 1484 | 13348 | 132064 | 0 | 0 | 2620 | 51 | 1080 | 427 | 50 | 5 | 0 | 46 |
| 0 | 0 | 31324 | 1804 | 13240 | 129796 | 0 | 0 | 1126 | 46 | 1082 | 782 | 19 | 5 | 47 | 30 |
| 0 | 0 | 31324 | 1900 | 13240 | 129796 | 0 | 0 | 0 | 1010 | 211 | 3 | 1 | 96 | 0 | |
| 0 | 0 | 31324 | 1916 | 13248 | 129796 | 0 | 0 | 0 | 10 | 1015 | 224 | 3 | 2 | 95 | 0 |

输出的第一行显示了自上次重启以来的平均值。之后，`vmstat` 再显示七次 5 秒的平均数据，覆盖接下来的 35 秒。表格输出被分为六个信息类别，由输出第一行中的字段指示。第二行显示了六个主要字段的进一步详细信息。你可以使用表 1-11 来解释这些字段。

**表 1-11 vmstat 工具输出中字段的含义**

| 字段名称 | 描述 |
| :------------- | :------------- |
| `procs` | 进程数量及其类型：$r =$ 等待运行的进程，$b =$ 处于不可中断休眠的进程，$w =$ 已被交换出但准备运行的进程 |
| `memory` | 关于物理内存和交换空间使用的信息（所有数字单位为 KB）：$swpd =$ 已使用的虚拟内存，$free =$ 可用物理内存，$buff =$ 用作缓冲区的内存，$cache =$ 已缓存的虚拟内存 |
| `swap` | 交换量（数字单位为 KB/秒）：$si =$ 从磁盘交换进来的内存量，$so =$ 交换到磁盘的内存量 |
| `io` | 输入和输出信息。（数字单位为块/秒，块大小取决于磁盘设备。） $bi =$ 发送到磁盘的块速率，$bo =$ 从磁盘接收的块速率 |
| `system` | 关于系统的信息：$in =$ 每秒中断次数（包括时钟中断），$cs =$ 每秒上下文切换次数 $-$ 内核更改正在运行的进程的次数 |
| `cpu` | 占用的 CPU 时间百分比：$us =$ 用户进程占用的 CPU 时间百分比，$sy =$ 系统进程占用的 CPU 时间百分比，$id =$ CPU 空闲时间百分比，$wa =$ 等待输入或输出（I/O）所花费的时间 |

![](img/11709a8f88c8cd03868a929dc94c0e2b_421_0.png)

在 `vmstat` 工具的输出中，$si$ 和 $so$ 字段的高数值表明交换过多。（*Swapping* 指在物理内存和硬盘上的虚拟内存之间复制信息。）$bi$ 和 $bo$ 字段的高数值表明磁盘活动过多。

####### 检查磁盘性能和磁盘使用情况

Linux 自带 `/sbin/hdparm` 程序，用于控制大多数 PC 上常见的 IDE 或 ATAPI 硬盘。`hdparm` 程序的一个功能是，你可以使用 `-t` 选项来确定数据从磁盘读取到内存缓冲区中的速率。例如，在我的系统中键入 `/sbin/hdparm -t /dev/hda` 的结果如下：

```
/dev/hda:
    Timing buffered disk reads: 178 MB in 3.03 seconds = 58.81 MB/sec
```

该命令要求将 IDE 驱动器的设备名称作为参数（第一块硬盘为 `/dev/hda`，第二块硬盘为 `/dev/hdb`）。如果你有 IDE 硬盘，可以尝试此命令，看看数据从系统磁盘驱动器读取的速度有多快。

要显示当前挂载的文件系统中可用的空间，请使用 `df` 命令。如果你希望 `df` 的输出更易读，请键入以下命令：

```
df -h
```

以下是该命令的典型输出：

| Filesystem | Size | Used | Avail | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/hda5 | 7.1G | 3.9G | 2.9G | 59% | / |
| /dev/hda3 | 99M | 18M | 77M | 19% | /boot |
| none | 125M | 0 | 125M | 0% | /dev/shm |
| /dev/sdc0 | 2.6G | 2.6G | 0 | 100% | /media/cârecorder |

如本例所示，`-h` 选项使 `df` 命令以 GB（GB）和 MB（MB）为单位显示大小。

要检查特定目录使用的磁盘空间，请使用 `du` 命令——你可以指定 `-h` 选项以 KB（K）和 MB（M）为单位查看输出，如下例所示：

```
du -h /var/log
```

以下是该命令的典型输出：

```
152K	/var/log/cups
4.0K	/var/log/vbox
4.0K	/var/log/httpd
508K	/var/log/gdm
4.0K	/var/log/samba
8.0K	/var/log/mail
4.0K	/var/log/news/OLD
8.0K	/var/log/news
4.0K	/var/log/squid
2.2M	/var/log
```

`du` 命令显示每个目录使用的磁盘空间，最后一行显示该目录使用的磁盘空间总量。如果你只想查看目录使用的总空间，请使用 `-s` 选项。例如，键入 `du -sh /home` 以查看 `/home` 目录使用的空间。该命令产生的输出如下所示：

```
89M	/home
```





####### 通过 /proc 文件系统查看系统信息

您的 Linux 系统拥有一个特殊的文件系统，称为 /proc 文件系统。您可以通过此文件系统了解系统的许多信息。事实上，您甚至可以通过 /proc 文件系统（只需向该文件系统中的一个文件写入内容）来更改内核参数，从而修改系统行为。

/proc 文件系统并不是硬盘上真正的目录，而是由 Linux 内核管理的一组内存数据结构，它们以目录和文件的形式呈现给您。/proc（也称为进程文件系统）的目的是让您能够访问有关 Linux 内核的信息，并帮助您了解当前正在系统上运行的所有进程。

您可以像访问任何其他目录一样访问 /proc 文件系统，但您需要了解各个文件的含义才能解读其中的信息。通常，您可以使用 `cat` 或 `more` 命令来查看 /proc 中文件的内容。文件的内容提供了有关系统某一方面信息。

与任何目录一样，首先查看 /proc 的详细目录列表。为此，请以 root 身份登录并在终端窗口中输入 `ls -l /proc`。在输出中，第一组目录（由行首的字母 r 表示）代表当前在系统上运行的进程。每个对应进程的目录都以进程 ID（一个数字）作为其名称。

![](img/11709a8f88c8cd03868a929dc94c0e2b_423_0.png)

还要注意，有一个非常大的文件名为 /proc/kcore；该文件代表您系统的整个物理内存。尽管 /proc/kcore 在列表中显示为一个巨大的文件，但并没有单个物理文件占用那么多硬盘空间——因此，不要试图删除该文件来回收磁盘空间。

/proc 中的多个文件和目录包含有关您的 Linux PC 的有趣信息。例如，/proc/cpuinfo 文件列出了系统的关键特性，如处理器类型和浮点处理器信息。您可以通过输入 `cat /proc/cpuinfo` 来查看处理器信息。例如，当我在我的系统上输入 `cat /proc/cpuinfo` 时，得到的结果如下：

```
processor       : 0
vendor_id       : GenuineIntel
cpu family      : 15
model           : 3
model_name      : Intel(R) Celeron(R) CPU 2.53GHz
stepping        : 3
cpu MHz         : 2533.129
cache size      : 256 KB
fdiv_bug        : no
hlt_bug         : no
f00f_bug        : no
coma_bug        : no
fpu             : yes
fpu_exception   : yes
cpuid level     : 5
wp              : yes
flags           : fpu vme de pse tsc msr pae mce cx8 apic
sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx
fxsr sse sse2 ss ht tm pbe pi_ni monitor ds_cpl cid
bogomips        : 4997.12
```

此输出来自一个 2.5 GHz 赛扬系统。列表展示了处理器的许多有趣特性。注意以 `fdiv_bug` 开头的行。还记得臭名昭著的 Pentium 浮点除法错误吗？该错误存在于一条名为 `fdiv`（*用于浮点除法*）的指令中。因此，`fdiv_bug` 行表明此特定的 Pentium 是否存在该错误。（幸运的是，我的 PC 处理器没有该错误。）

`/proc/cpuinfo` 文件的最后一行显示了处理器的 BogoMIPS，这是由 Linux 内核在启动时计算得出的。BogoMIPS 是 Linux 内部用于时间延迟循环的一种机制。

表 1-12 总结了 /proc 文件系统中一些提供有关您的 Linux 系统信息的文件。您可以在系统上查看这些文件以了解其内容，但请注意，表 1-12 中显示的文件并非所有都存在于您的系统中。/proc 文件系统的具体内容取决于内核配置和已加载的驱动程序模块（这反过来又取决于您 PC 的硬件配置）。

您可以像在 Linux 中操作其他目录和文件一样浏览 /proc 文件系统。使用 `more` 或 `cat` 命令查看文件内容。

![](img/11709a8f88c8cd03868a929dc94c0e2b_424_0.png)

######## 表 1-12 /proc 中的一些文件和目录

| 文件名 | 内容 |
| :--- | :--- |
| `/proc/acpi` | 高级配置和电源接口（ACPI）信息——一种行业标准接口，用于笔记本电脑、台式机和服务器的配置和电源管理 |
| `/proc/bus` | 包含每种总线类型（如 PCI）的总线特定信息的目录 |
| `/proc/cmdline` | 用于启动 Linux 内核的命令行（例如，`ro root=LABEL=/ rhgb`） |
| `/proc/cpuinfo` | 有关 CPU（微处理器）的信息 |
| `/proc/devices` | 系统中可用的块设备和字符设备 |
| `/proc/dma` | 有关所使用的 DMA（直接内存访问）通道的信息 |
| `/proc/driver/rtc` | 有关 PC 实时时钟（RTC）的信息 |
| `/proc/filesystems` | 支持的文件系统列表 |
| `/proc/ide` | 包含 IDE 设备信息的目录 |
| `/proc/interrupts` | 有关中断请求（IRQ）号及其用途的信息 |
| `/proc/ioports` | 有关输入/输出（I/O）端口地址及其用途的信息 |
| `/proc/kcore` | 物理内存的映像 |
| `/proc/kmsg` | 内核消息 |
| `/proc/loadavg` | 负载平均值（过去 1、5 和 15 分钟内等待运行的进程的平均数量） |
| `/proc/locks` | 当前内核锁（用于确保多个进程不向同一文件同时写入） |
| `/proc/meminfo` | 有关物理内存和交换空间使用情况的信息 |
| `/proc/misc` | 杂项信息 |
| `/proc/modules` | 已加载驱动程序模块列表 |
| `/proc/mounts` | 已挂载的文件系统列表 |
| `/proc/net` | 包含许多子目录的目录，其中包含有关网络的信息 |
| `/proc/partitions` | Linux 内核已知的分区列表 |
| `/proc/pci` | 有关在系统中找到的 PCI 设备的信息 |
| `/proc/scsi` | 包含有关在系统中找到的 SCSI 设备信息的目录（仅当拥有 SCSI 设备时存在） |
| `/proc/stat` | 关于系统的总体统计数据 |
| `/proc/swaps` | 有关交换空间及其使用情况的信息 |
| `/proc/sys` | 包含系统信息的目录。您可以通过向此目录中的文件写入内容来更改内核参数。（使用这种方法调整系统性能需要专业知识才能正确完成。） |
| `/proc/uptime` | 关于系统运行时间的信息 |
| `/proc/version` | 内核版本号 |

###### 理解 Linux 设备

Linux 将所有设备视为文件，并使用设备的方式就像使用文件一样——打开它、向其中写入数据、从中读取数据，并在完成后关闭它。这种将每个设备视为文件的能力是通过使用设备驱动程序实现的。**设备驱动程序**是一种控制特定类型硬件的特殊程序。当内核向设备写入数据时，设备驱动程序会执行对该设备适当的操作。例如，当内核向软盘驱动器写入数据时，软盘设备驱动程序会将数据写入软盘的物理介质。另一方面，如果内核向并行端口设备写入数据，并行端口驱动程序会将数据发送到连接到并行端口的打印机。

因此，设备驱动程序将特定于设备的代码与内核的其他部分隔离开来，并使设备看起来像文件。任何应用程序都可以通过打开特定于该设备的文件来访问设备。图 1-7 阐明了 Linux 设备驱动程序的概念。

**图 1-7：** 应用程序可以通过一个特殊的文件来访问设备，该文件进而使用设备驱动程序。

![](img/11709a8f88c8cd03868a929dc94c0e2b_426_0.png)

####### 设备文件

如图 1-7 所示，应用程序可以像访问文件一样访问设备。这些文件是称为**设备文件**的特殊文件，它们出现在 Linux 文件系统中的 `/dev` 目录中。





如果使用 `1s` 命令查看 `/dev` 目录下的文件列表，你会看到数千个文件。这些文件并不意味着你的系统拥有数千个设备。`/dev` 目录包含所有可能类型的设备的文件——这就是设备文件数量如此巨大的原因。

那么，当应用程序打开特定的设备文件时，内核是如何知道该使用哪个设备驱动程序的呢？答案在于两个数字，称为 *主要* 和 *次要* 设备号。每个设备文件都通过这些数字映射到特定的设备驱动程序。

要查看主要和次要设备号的示例，请在终端窗口中输入以下命令：

```
ls -l /dev/hda
```

你会看到类似以下输出的一行：

```
brw-rw---- 1 root disk 3, 0 Aug 16 14:50 /dev/hda
```

在这行输出中，主要和次要设备号出现在日期之前。在这种情况下，主要设备号是 3，次要设备号是 0。内核通过使用该 *主要设备号* 来为此设备文件选择设备驱动程序。

实际上，你不需要了解太多关于设备文件和设备号的知识，只需意识到它们的存在即可。

![](img/11709a8f88c8cd03868a929dc94c0e2b_427_0.png)

> 如果你感到好奇，所有设备的主要和次要编号都是根据设备类型分配的。这些编号由 Linux 分配名称和编号机构（LANANA）进行分配。你可以在 www.lanana.org/docs/device-list/devices.txt 查看当前的设备列表。

####### 块设备

设备文件列表中的第一个字母也提供了重要线索。对于 `/dev/hda` 设备，第一个字母是 b，这表明 `/dev/hda` 是一个 *块设备*——它可以按块（通常为 512 字节或 1K）接受或提供数据。顺便说一下，`/dev/hda` 指的是你系统上的第一个 IDE 硬盘（在 Windows 中对应 C: 盘）。硬盘、软盘驱动器和 CD-ROM 驱动器都是块设备的例子。

####### 字符设备

如果设备文件列表中的第一个字母是 c，则该设备是一个 *字符设备*——它一次只能接收和发送一个字符（一个字节）的数据。例如，串行端口和并行端口都是字符设备。

要查看字符设备的具体列表，请在终端窗口中输入以下命令：

```
ls -l /dev/ttyS0
```

该设备的列表类似于以下内容：

```
crw-rw--- 1 root uucp 4, 64 Aug 16 14:50 /dev/ttyS0
```

注意，第一个字母是 c，因为 /dev/ttyS0（第一个串行端口）是一个字符设备。

####### 网络设备

使你的系统能够与网络交互的网络设备——例如以太网和拨号点对点协议（PPP）连接——有些特殊，因为它们不需要文件来对应设备。相反，内核使用特殊的名称来表示设备。例如，以太网设备被命名为 eth0（第一张以太网卡）、eth1（第二张），依此类推。PPP 连接被命名为 ppp0、ppp1 等。

由于网络设备没有映射到设备文件，因此 /dev 目录中不存在对应这些设备的文件。

####### 使用 udev 实现持久设备命名

Linux 内核 2.6 引入了一种处理设备的新方法，基于以下特性：

- **sysfs**：内核 2.6 提供了 sysfs 文件系统，该文件系统挂载在文件系统的 /sys 目录上。sysfs 文件系统显示了系统中的所有设备以及每个设备的许多信息。这些信息包括设备在总线上的位置、名称和序列号等属性，以及设备的主要和次要编号。
- **/sbin/hotplug**：每当有设备添加或移除时，都会调用此程序。然后它可以执行处理该设备所需的操作。
- **/sbin/udev**：此程序负责基于设备特征（如序列号、总线上的设备编号或基于通过文本文件 /etc/udev/udev.rules 设置的一组规则确定的用户分配名称）动态命名设备。

udev 程序的配置文件是 /etc/udev/udev.conf。根据该配置文件中的设置，udev 自动在由 udev_root 参数指定的目录中创建设备节点。例如，为了管理 /dev 目录中的设备节点，应在 /etc/udev/udev.conf 中定义 udev_root，如下所示：

```
udev_root="/dev/"
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_428_0.png)

####### 管理可加载驱动程序模块

要使用任何设备，Linux 内核必须包含其驱动程序。如果驱动代码作为单体程序（一个形式为单一大型文件的程序）链接到内核中，添加新驱动意味着需要用新的驱动代码重建内核。重建内核意味着你必须使用新内核重启 PC，然后才能使用新的设备驱动程序。幸运的是，Linux 内核采用了模块化设计，避免了重启的麻烦。Linux 设备驱动程序可以以模块的形式创建，内核可以加载和卸载这些模块，而无需重启 PC。

![](img/11709a8f88c8cd03868a929dc94c0e2b_429_0.png)

驱动程序模块是可加载内核模块（一种更广泛的软件模块类别）的一种类型。其他类型的内核模块包括支持新型文件系统的代码、网络协议模块以及解释不同格式可执行文件的模块。

######## 加载和卸载模块

你可以使用一组命令来管理可加载的设备驱动程序模块。你需要以 root 身份登录才能使用其中一些命令。在表 3-13 中，我总结了一些常用的模块命令。

**表 3-13 管理内核模块的命令**

| 此命令 | 执行以下操作 |
| :--- | :--- |
| insmod | 将模块插入内核 |
| rmmod | 从内核中移除模块 |
| depmod | 确定模块之间的相互依赖关系 |
| ksyms | 显示符号列表以及定义该符号的模块名称 |
| lsmod | 列出当前加载的所有模块 |
| modinfo | 显示有关内核模块的信息 |
| modprobe | 智能地插入或移除一个模块或一组模块。（例如，如果模块 A 需要 B，那么当要求加载 A 时，modprobe 会自动加载 B。） |

如果你必须使用其中任何一个命令，请以 *root* 身份登录或在终端窗口中输入 **su -** 以成为 *root*。

要查看当前加载的模块，请键入

```
lsmod
```

你会看到一个漫长的模块列表，具体取决于安装在系统中的设备类型。

`lsmod` 显示的列表包括所有类型的 Linux 内核模块，而不仅仅是设备驱动程序。例如，如果你使用 Ext3 文件系统，通常会发现两个模块——jbd 和 *ext3*——它们都是 Ext3 文件系统（Linux 的最新文件系统）的一部分。

![](img/11709a8f88c8cd03868a929dc94c0e2b_430_0.png)

除了 `lsmod` 之外，另一个常用的模块命令是 `modprobe`。当你需要手动加载或移除一个或多个模块时，请使用 *modprobe*。`modprobe` 最好的地方在于你不需要担心模块是否需要其他模块才能工作。`modprobe` 命令会自动加载模块所需的任何其他模块。例如，在我的一个系统中，我使用以下命令手动加载声音驱动程序：

```
modprobe snd-card-0
```

此命令使 *modprobe* 加载使声音工作所需的所有内容。

![](img/11709a8f88c8cd03868a929dc94c0e2b_430_1.png)

你可以使用带有 *-r* 选项的 *modprobe* 来移除模块。例如，要移除声音模块，我使用以下命令：

```
modprobe -r snd-card-0
```

此命令消除了 `modprobe snd-card-0` 命令已加载的所有模块。

######## 使用 /etc/modprobe.conf 文件

当我使用模块名称 `snd-card-0` 时，*modprobe* 命令如何知道它需要加载 `snd-intel8x0` 驱动程序模块？答案在 `/etc/modprobe.conf` 配置文件中。该文件包含一行内容，告诉 *modprobe* 在看到模块名称 `snd-card-0` 时应加载什么。

要查看 `/etc/modprobe.conf` 的内容，请键入

```
cat /etc/modprobe.conf
```





![](img/11709a8f88c8cd03868a929dc94c0e2b_431_0.png)

在一台运行 Linux 2.6 的 Fedora Core 个人电脑上，`/etc/modprobe.conf` 文件包含以下行：

```
alias eth0 3c59x
alias snd-card-0 snd-intel8x0
alias usb-controller uhci-hcd
```

以关键字 `alias` 开头的每一行都为实际的驱动模块定义了一个标准名称。例如，第一行将 `3c59x` 定义为别名 `eth0` 的实际驱动名称，`eth0` 代表第一张以太网卡。类似地，第三行定义了当使用名称 `snd-card-0` 时要加载的模块为 `snd-intel8x0`。

`modprobe` 命令会查阅 `/etc/modprobe.conf` 文件将别名转换为驱动模块的真实名称。它还会查阅 `/etc/modprobe.conf` 文件以完成其他任务，例如获取驱动模块的参数。例如，你可以插入以 `options` 关键字开头的行，以提供驱动模块可能需要的参数值。

例如，要将以太网驱动的 `debug` 级别参数设置为 5（该参数会在 `/var/log/messages` 中生成大量信息），我在 `/etc/modprobe.conf` 文件中添加了以下行：

```
options 3c59x debug=5
```

该行指定 `3c59x` 模块中名为 `debug` 的参数的值为 5。

如果你想知道模块接受的参数名称，请使用 `modinfo` 命令。例如，要查看关于 `3c59x` 驱动模块的信息，我输入：

```
modinfo 3c59x | more
```

从生成的输出中，我可以知道 `debug` 是设置调试级别的参数名称。

不幸的是，`modinfo` 命令显示的信息可能有些晦涩难懂。唯一的安慰是，你通常只需要使用图形实用工具来配置设备，而该工具会自动处理向配置文件（如 `/etc/modprobe.conf`）中添加所需内容的工作。

###### 在 Linux 中安排作业

作为系统管理员，你可能需要在定期时间自动运行某些程序，或者在指定的未来时间执行一个或多个命令。你的 Linux 系统包含了安排作业在任何你想要未来日期或时间运行的设施。你也可以设置系统定期或仅一次执行任务。以下是一些你可以通过在 Linux 系统上安排作业来执行的典型任务：

- 在半夜备份文件。
- 在系统不忙时（例如清晨）下载大文件。
- 发送消息提醒会议。
- 定期分析系统日志并查找任何异常活动。

你可以使用 Linux 的 `at` 命令或 `crontab` 设施来设置这些作业。在接下来的几个部分中，我将介绍 Linux 的这些作业调度功能。

####### 安排一次性作业

如果你想在稍后的时间运行一个或多个命令，可以使用 `at` 命令。`at` `守护进程`——一个专门用于处理使用 `at` 提交的作业的程序——会在指定时间运行你的命令，并将输出邮件发送给你。

![](img/11709a8f88c8cd03868a929dc94c0e2b_432_0.png)

在尝试 `at` 命令之前，你需要知道以下配置文件控制哪些用户可以使用 `at` 命令安排任务：

- `/etc/at.allow` 包含可以使用 `at` 命令提交作业的用户名称。
- `/etc/at.deny` 包含不允许使用 `at` 命令提交作业的用户名称。

如果这些文件不存在，或者你发现空的 `/etc/at.deny` 文件，任何用户都可以使用 `at` 命令提交作业。Linux 的默认设置是一个空的 `/etc/at.deny` 文件；在这种情况下，任何人都可以使用 `at` 命令。如果你不希望某些用户使用 `at`，只需将他们的用户名列在 `/etc/at.deny` 文件中即可。

要使用 `at` 安排稍后执行的一次性作业，请遵循以下步骤：

1. **运行带有你想要执行命令的日期或时间的 `at` 命令。**

按下回车键后，会出现 `at>` 提示符，如下所示：

```
at 21:30
at>
```

这是指示你想要执行一个或多个命令的时间的最简单方法——只需指定 24 小时制的时间即可。在这种情况下，你想要在晚上 9:30 执行命令（如果现在已经过了晚上 9:30，则是在明天）。不过，你可以用许多不同的方式指定执行时间。（参见表 1-14 中的示例。）

2. **在 `at>` 提示符下，输入你想执行的命令，就像在 shell 提示符下输入一样。每个命令之后按下回车键并继续输入下一个命令。当你输入完所有想要执行的命令后，按下 Ctrl+D 表示结束。**

以下是一个示例，展示了如何在未来时间执行 `ps` 命令：

```
at> ps
at> <EOF>
job 1 at 2006-12-28  21:30
```

按下 Ctrl+D 后，`at` 命令会响应一个作业号以及作业将执行的日期和时间。

| **表 1-14** | **at 命令执行时间的格式** |
| :---------------- | :-------------------------------------------------------------- |
| **命令** | **作业运行时间** |
| `at now` | 立即 |
| `at now + 15 minutes` | 从当前时间起 15 分钟后 |
| `at now + 4 hours` | 从当前时间起 4 小时后 |
| `at now + 7 days` | 从当前时间起 7 天后 |
| `at noon` | 今天中午（如果已过中午，则为明天中午） |
| `at now next hour` | 从现在开始正好 60 分钟 |
| `at now next day` | 明天同一时间 |
| `at 17:00 tomorrow` | 明天下午 5:00 |
| `at 4:45pm` | 今天下午 4:45（如果已过下午 4:45，则为明天下午 4:45） |
| `at 3:00 Dec 28, 2006` | 2006 年 12 月 28 日清晨 3:00 |

输入一个或多个作业后，你可以使用 `atq` 命令查看当前安排的作业列表：

```
atq
```

输出看起来类似于以下内容：

```
4    2006-12-28 03:00 a root
5    2006-10-26 21:57 a root
6    2007-10-26 16:45 a root
```

每行的第一个字段显示作业号——即你提交作业时 `at` 命令显示的相同数字。下一个字段显示执行的年、月、日和小时。最后一个字段显示名为 `a` 的队列中挂起的作业。

如果你想取消某个作业，请使用 `atrm` 命令将该作业从队列中移除。在使用 `atrm` 命令移除作业时，请通过作业号引用该作业，如下所示：

```
atrm 4
```

此命令删除了安排在 2006 年 12 月 28 日清晨 3:00 执行的作业 4。

![](img/11709a8f88c8cd03868a929dc94c0e2b_434_0.png)

当作业执行时，输出会邮件发送给你。在终端窗口中输入 `mail` 即可读取你的邮件并查看作业的输出。

####### 安排重复性作业

虽然 `at` 适合在特定时间运行命令，但对于以重复间隔自动运行程序则不太实用。你必须使用 `crontab` 来安排此类重复性作业——例如，如果你想每晚午夜将文件备份到磁带上。

你通过在具有特定格式的文件中放置作业信息，并使用 `crontab` 命令提交该文件来安排重复性作业。`cron` 守护进程——`crond`——每分钟检查一次作业信息，并在指定时间执行重复性作业。由于 `cron` 守护进程处理重复性作业，因此这些作业也被称为 `cron` 作业。

来自 `cron` 作业的任何输出都会邮件发送给提交该作业的用户。（在提交的作业信息文件中，你可以指定邮件输出的不同接收者。）

两个配置文件控制谁可以使用 `crontab` 安排 `cron` 作业：

- `/etc/cron.allow` 包含可以使用 `crontab` 命令提交作业的用户名称。
- `/etc/cron.deny` 包含不允许使用 `crontab` 命令提交作业的用户名称。

如果存在 `/etc/cron.allow` 文件，则只有列在该文件中的用户才能安排 `cron` 作业。如果仅存在 `/etc/cron.deny` 文件，则列在该文件中的用户不能安排 `cron` 作业。如果两个文件都不存在，默认的 Linux 设置允许任何用户提交 `cron` 作业。

要提交一个 `cron` 作业，请遵循以下步骤：

1. **准备一个 shell 脚本（或任何编程语言的可执行程序），能够执行你想要执行的重复任务。**
   如果你想定期执行现有的程序，可以跳过此步骤。

2. **准备一个包含你想要运行 shell 脚本或程序（步骤 1 中的）时间的信息文件，然后使用 `crontab` 提交此文件。**
   你可以用单个文件提交多个重复性作业。每行包含关于作业时间信息的行都有一个标准格式，有六个字段——前五个指定作业运行的时间，第六个及后续字段构成实际运行的命令。例如，下面是一行代码，它每天午夜后 5 分钟在用户主目录中执行 `myjob` shell 脚本：
   `5 0 * * * $HOME/myjob`
   表 1-15 显示了前五个字段的含义。**注意：** 星号 (*) 表示该字段的所有可能值。此外，前五个字段中的任何条目可以是单个数字、逗号分隔的数字列表、用连字符分隔的一对数字（表示数字范围）或星号。

3. **假设当前目录中的文本文件 `jobinfo` 包含作业信息。使用以下命令将此信息提交给 `crontab`：**
   `crontab jobinfo`
   就这样！你的 `cron` 作业已设置完毕。从现在开始，`cron` 作业将按照固定间隔运行（如作业信息文件中指定的那样），你将收到包含作业输出的邮件消息。
   要验证作业确实已安排，请输入以下命令：
   `crontab -l`
   `crontab -l` 命令的输出显示以你的名义当前安装的 `cron` 作业。要移除你的 `cron` 作业，请输入 `crontab -r`。





####### 表 1-15 crontab 文件中执行时间的格式

| 字段编号 | 字段含义 | 可接受的值范围* |
| :--- | :--- | :--- |
| 1 | 分钟 | 0–59 |
| 2 | 小时 | 0–23 |
| 3 | 日期 | 0–31 |
| 4 | 月份 | 1–12（1 代表一月，2 代表二月，依此类推）或月份名称的前三个字母 — Jan、Feb、Mar、Apr、May、Jun、Jul、Aug、Sep、Oct、Nov、Dec |
| 5 | 星期 | 0–6（0 代表周日，1 代表周一，依此类推）或工作日名称的三个字母缩写 — Sun、Mon、Tue、Wed、Thu、Fri、Sat |

*字段中的星号（*）表示该字段的所有可能值。例如，如果第三个字段中是一个星号，则任务将每天执行。

如果你以 root 身份登录，你还可以为任何用户设置、检查和删除 cron 任务。要为某用户设置 cron 任务，请使用以下命令：

```bash
crontab -u username filename
```

这里，`username` 是你安装 cron 任务的目标用户，`filename` 是包含任务信息的文件。

使用以下形式的 crontab 命令来查看某用户的 cron 任务：

```bash
crontab -u username -l
```

要删除某用户的 cron 任务，请使用以下命令：

```bash
crontab -u username -r
```

> **注意：** cron 守护进程还会执行系统全局 cron 任务文件 `/etc/crontab` 中列出的 cron 任务。下面是一个典型的 Linux 系统 `/etc/crontab` 文件（输入 `cat /etc/crontab` 查看文件内容）：

```bash
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/
# run-parts
01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
22 4 * * 0 root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly
```

前四行设置了此文件中列出的任务的几个环境变量。`MAILTO` 环境变量指定接收来自此文件中 cron 任务输出的邮件信息的用户。

以 `#` 开头的行是注释行。`run-parts` 注释后面的四行在不同的时间执行 `run-parts` shell 脚本（位于 `/usr/bin` 目录中），并以特定目录的名称作为参数。`run-parts` 的每个参数 — `/etc/cron.hourly`、`/etc/cron.daily`、`/etc/cron.weekly` 和 `/etc/cron.monthly` — 都是目录。本质上，`run-parts` 执行位于你作为参数提供的目录中的所有脚本。

表 1-16 列出了你可以找到这些脚本的目录以及它们执行的时间。你必须查看这些目录中的脚本，才能知道在这些周期性间隔执行的是什么。

####### 表 1-16 cron 任务的脚本目录

| 目录名称 | 内容 |
| :--- | :--- |
| /etc/cron.hourly | 脚本每小时执行一次 |
| /etc/cron.daily | 脚本每天执行一次 |
| /etc/cron.weekly | 脚本每周执行一次 |
| /etc/cron.monthly | 脚本每月执行一次 |

##### 第 2 章：管理用户和组

###### 本章内容

- 添加用户账户
- 理解密码文件
- 管理组
- 探索用户环境
- 更改文件和目录的用户及组所有权

Linux 是一个多用户系统，因此拥有许多用户账户。即使你是系统上的唯一用户，许多服务器也需要独特的用户名和组名。例如，FTP 服务器在用户名 `ftp` 下运行。一大批系统用户并非供人使用，而是专门用于运行特定程序的。

此外，用户可以属于一个或多个组。通常，每个用户名都有一个对应的私有组名。默认情况下，每个用户都属于那个对应的私有组。但是，你可以定义其他组，以便根据组成员身份提供对特定文件和目录的访问权限。

文件和目录的用户及组所有权是确保只有正确的人（或正确的进程）能访问正确的文件和目录的一种方法。管理用户和组账户是典型的系统管理任务。鉴于 Linux 提供的工具，做这部分工作并不难。我将在本章中向你展示方法。

###### 添加用户账户

在 Linux 安装完成后第一次启动系统时，你会有机会添加用户账户。root 账户是你必须在安装期间设置的唯一账户。如果你没有在第一次启动系统时添加其他用户账户，之后可以使用 GUI 用户账户管理器或 `useradd` 命令在系统上添加新用户。

![创建用户账户](img/11709a8f88c8cd03868a929dc94c0e2b_439_0.png)

除了 root 之外，创建其他用户账户是一个好主意。即使你是系统的唯一用户，以权限较低的用户登录也是良好的实践习惯，因为这样你不会意外损坏重要的系统文件。如有必要，你可以输入 `su -` 以 root 身份登录，然后执行任何系统管理任务。

####### 使用 GUI 用户管理器添加用户账户

大多数 Linux 发行版都附带一个管理用户账户的 GUI 工具。你可以使用该 GUI 工具添加新的用户账户。无论具体的 GUI 工具如何，基本步骤都涉及以下内容：

1. 该工具显示当前用户账户的列表，并有一个“添加”按钮用于添加新用户。
2. 点击“添加”按钮以弹出对话框，提示你输入关于新用户账户的信息。
3. 输入请求的信息 — 用户名、密码（输入两次）以及用户的完整姓名。
4. 点击创建新账户的按钮，GUI 工具将负责添加新的用户账户。

![GUI 用户管理器示例](img/11709a8f88c8cd03868a929dc94c0e2b_439_1.png)

例如，在 SUSE 中，从 YaST 控制中心左侧选择“安全和用户”类别，然后点击窗口右侧的“用户管理”图标。然后 YaST 将显示“用户和组管理”窗格，如图 2-1 所示，你可以在其中定义新的用户账户。

![图 2-1：用户和组管理窗格](img/11709a8f88c8cd03868a929dc94c0e2b_439_2.png)

注意该窗格有两个单选按钮：用户和组（如图 2-1 所示）。选择“用户”单选按钮将显示来自 `/etc/passwd` 文件的当前用户列表。选择“组”单选按钮将列出来自 `/etc/group` 文件的组名。最初，“用户和组管理”工具会过滤掉任何系统用户和组。但是，你可以点击“设置过滤器”并从下拉菜单中选择“系统用户”来查看系统用户。（系统用户指未分配给人工用户的用户账户；相反，这些用户账户用于运行各种服务。）

你可以从图 2-1 所示的窗格中添加新的用户和组，或编辑现有的用户和组。

要添加新的用户账户，请点击“添加”按钮，并在“新本地用户”窗口中输入请求的信息，如图 2-2 所示。

![图 2-2：新本地用户窗口](img/11709a8f88c8cd03868a929dc94c0e2b_440_0.png)

在窗口中填写请求的信息（参见图 2-2），然后点击“接受”按钮。新用户现在出现在“用户和组管理”窗格中的用户列表中。

如果你愿意，可以添加更多用户账户。完成后，点击“用户和组管理”窗格中的“完成”按钮（参见图 2-1）以创建新的用户账户。

默认情况下，YaST 将所有本地用户放在名为 `users` 的组中。有时你希望用户也属于其他组，以便该用户可以访问由该组拥有的文件。将用户添加到其他组很容易。例如，假设我想将用户名 `naba` 添加到名为 `wheel` 的组中。我只需在终端窗口中输入以下命令：

```bash
usermod -G wheel naba
```

![将用户添加到组的示例](img/11709a8f88c8cd03868a929dc94c0e2b_441_0.png)

要在 SUSE 中删除用户账户，请点击用户账户列表中的用户名（参见图 2-1）。然后点击“删除”按钮。

####### 使用命令管理用户账户

如果你正在文本控制台工作，可以使用 `useradd` 命令创建新的用户账户。按照以下步骤为新用户添加账户：

1. **以 `root` 身份登录。**
   如果你尚未以 `root` 身份登录，请输入 `su -` 成为 `root`。
2. **输入带有 `-c` 选项的以下 `useradd` 命令以创建账户：**
   ```bash
   /usr/sbin/useradd -c "Ashley Barkakati" ashley
   ```
3. **使用 `passwd` 命令设置密码，如下所示：**
   ```bash
   passwd ashley
   ```
   你会被提示两次输入密码。如果你输入一个别人容易猜到的密码，`passwd` 程序将拒绝它。

![为新用户设置密码](img/11709a8f88c8cd03868a929dc94c0e2b_441_1.png)

`useradd` 命令会参考以下配置文件以获取关于新用户账户各种参数的默认信息：

- `/etc/default/useradd`：指定默认 shell（`/bin/bash`）和默认主目录位置（`/home`）
- `/etc/login.defs`：提供自动组和用户 ID 以及密码过期参数的系统默认值
- `/etc/skel`：包含 `useradd` 在用户主目录中创建的默认文件

使用 `cat` 或 `more` 命令检查这些文件，以查看它们包含的内容。




# 提醒

你可以使用 `userdel` 命令删除用户账户。只需在命令提示符下输入 `/usr/sbin/userdel username` 即可删除用户账户。若同时希望清除该用户的家目录，请输入 `/usr/sbin/userdel -r username`。

要修改用户账户中的任何信息，请使用 `usermod` 命令。例如，如果我希望我的用户名 `naba` 的主要组为 `root`，我将输入以下命令：

```
usermod -g root naba
```

####### 提示

要了解关于 `useradd`、`userdel` 和 `usermod` 命令的更多信息，请在终端窗口中输入 `man useradd`、`man userdel` 或 `man usermod`。

###### 理解 /etc/passwd 文件

`/etc/passwd` 文件是用户账户的列表。它是一个文本文件，任何用户都可以读取——无需特殊权限。`/etc/passwd` 中的每一行包含七个字段，由冒号（`:`）分隔。

以下是 `/etc/passwd` 文件中的一个典型条目：

```
naba:x:500:10:Naba Barkakati:/home/naba:/bin/bash
```

**图 2-3：** 这个典型的 `/etc/passwd` 条目展示了各个字段的含义。

![](img/11709a8f88c8cd03868a929dc94c0e2b_442_0.png)

正如示例所示，`/etc/passwd` 中每行的格式如下：
`username:password:UID:GID:GECOS:home dir:shell`

表 2-1 解释了 `/etc/passwd` 条目中七个字段的含义。

**表 2-1** */etc/passwd 文件中字段的含义*

| 此字段 | 包含内容 |
| :--- | :--- |
| username | 字母数字用户名，通常为 8 个字符长且唯一（Linux 允许用户名长于 8 个字符，但某些其他操作系统不允许。） |
| password | 若存在，为 13 位加密密码。（空字段表示访问该账户无需密码。若为 x，则表示密码存储在 `/etc/shadow` 文件中，这样更安全。） |
| UID | 用作用户标识符的唯一数字。（`root` 的 UID 为 0，通常 1 到 100 之间的 UID 保留给非人类用户（如服务器服务）；最好将 UID 保持在 32,767 以下。） |
| GID | 用户所属组的默认组 ID（`GID` 0 对应组 `root`，其他组定义在 `/etc/group` 中，用户通常可以同时属于一个或多个组。） |
| GECOS | 关于用户的可选个人信息。（`The finger` 命令使用此字段，GECOS 代表 General Electric Comprehensive Operating System，这是一个早已被遗忘的操作系统，但其名称因 `/etc/passwd` 中该字段而得名而永存。） |
| home dir | 用户家目录的名称 |
| shell | 用户登录时执行的命令解释器（shell），例如 `bash`（`/bin/bash`） |

###### 管理用户组

组是用户所属的集合。组具有名称和标识号（ID）。组定义完成后，用户可以属于这些组中的一个或多个。

你可以在 `/etc/group` 中找到所有现有组的列表。例如，定义名为 `wheel` 的组的那一行如下：
`wheel:x:10:root,naba`

如本例所示，/etc/group 中的每一行具有以下格式，由四个字段组成，以冒号分隔：

```
groupname:password:GID:membership
```

表 2-2 解释了组定义中四个字段的含义。

**表 2-2**

*/etc/group 文件中字段的含义*

| 字段名称 | 含义 |
| :--- | :--- |
| groupname | 组名称（例如，wheel） |
| password | 组密码（x 表示密码存储在 /etc/shadow 文件中） |
| GID | 数字组 ID（例如，10） |
| membership | 属于此组的逗号分隔的用户名列表（例如，root, naba） |

若要创建新组，只需使用 groupadd 命令。例如，若要添加一个名为 class 的新组，并自动选择组 ID，只需在终端窗口中输入以下命令（必须以 root 身份登录）：

```
groupadd class
```

然后，你可以使用 usermod 命令将用户添加到该组。例如，要将用户 naba 和 ashley 添加到名为 class 的组中，请输入以下命令：

```
usermod -G class naba
usermod -G class ashley
```

就这样。现在检查 /etc/group，发现其中包含 class 的以下定义：

```
class:x:502:naba,ashley
```

就是这么简单！

若要删除组，请使用 groupdel 命令。例如，若要删除名为 class 的组，请输入

```
groupdel class
```

###### 探索用户环境

当你以用户身份登录时，你会获得一组控制你在 Linux 系统中所见所做许多方面的环境变量。若想看当前的环境，请在终端窗口中输入以下命令：

```
env
```

（顺便说一句，`printenv` 命令也能显示环境，但 `env` 更简短。）

`env` 命令会打印出一长串行。这一整集合行构成了当前环境，而每一行定义一个环境变量。例如，`env` 命令显示如下典型的一行：

```
HOSTNAME=localhost.localdomain
```

该行定义了环境变量 `HOSTNAME`，其值为 `localhost.localdomain`。

*环境变量* 不过是与字符串关联的名称。例如，名为 `PATH` 的环境变量通常这样为普通用户定义：

```
PATH=/usr/local/bin:/bin:/usr/bin:/usr/X11R6/bin
```

等号（`=`）右侧的字符串是 `PATH` 环境变量的 *值*。按照惯例，`PATH` 环境变量是一系列目录名，每个名称与前一个名称之间用冒号（`:`）分隔。

每个环境变量都有特定用途。例如，当 shell 需要搜索文件时，它只在 `PATH` 环境变量中列出的目录中搜索。shell 按照出现顺序搜索 `PATH` 中的目录。因此，如果两个程序具有相同的名称，shell 将执行它首先找到的那个。

与 shell 使用 `PATH` 环境变量类似，编辑器（如 `vi`）使用 `TERM` 环境变量的值来确定如何显示你用 `vi` 编辑的文件。要在 shell 提示符下查看 `TERM` 的当前设置，请输入以下命令：

```
echo $TERM
```

如果在终端窗口中输入此命令，输出如下：

```
xterm
```

要在 *bash* 中定义环境变量，请使用以下语法：

```
export NAME=Value
```

这里，*NAME* 表示环境变量的名称，*Value* 是代表其值的字符串。因此，使用以下命令可将 *TERM* 设置为值 *xterm*：

```
export TERM=xterm
```

定义环境变量后，你可以通过指定新值来更改其值，语法为 NAME=new-value。例如，要将 *TERM* 的定义更改为 *vt100*，请在 shell 提示符下输入 **TERM=vt100**。

对于 *PATH* 这样的环境变量，你通常希望向现有定义追加新的目录名，而不是从头定义 *PATH*。例如，如果你下载并安装了 Java 2 开发工具包（可从 http://java.sun.com/j2ee/1.5.0/download.jsp 获取），你就必须将 Java 二进制文件的位置添加到 *PATH* 中。以下是完成此任务的方法：

```
export PATH=$PATH:/usr/java/jdk1.5.0/bin
```

该命令将字符串 `:/usr/java/jdk1.5.0/bin` 追加到 *PATH* 环境变量的当前定义中。最终效果是将 `/usr/java/jdk1.5.0/bin` 添加到 *PATH* 的目录列表中。

**注意：** 你也可将这条导出命令写成如下形式：

```
export PATH=$(PATH):/usr/java/jdk1.5.0/bin
```

输入该命令后，你就可以访问 `/usr/java/jdk1.5.0/bin` 目录中的程序，例如 `javac`，这是将 Java 源代码转换为 Java 解释器可执行形式的 Java 编译器。

*PATH* 和 *TERM* 只是少数常见环境变量中的两个。表 2-3 列出了典型 Linux 用户的部分环境变量。




###### 更改文件和目录的用户与组所有权

在 Linux 中，每个文件或目录都有两种所有者——一个用户和一个组。换句话说，每个文件和目录都由一个用户和一个组所有。用户和组的归属权限可以控制谁可以访问文件或目录。

要查看文件或目录的所有者，请使用 `ls -1` 命令来查看目录的详细列表。例如，这是一个典型文件的信息：

```
drwxr-x--- 1 naba naba 40909 Aug 16 20:37 composer.txt
```

在此示例中，第一组字符显示了文件的权限设置——谁可以读取、写入或执行该文件。第三个和第四个字段（在本例中为 `naba naba`）指示了文件的用户和组所有者。每个用户都有一个与用户名同名的私有组。因此，大多数文件的用户和组所有权都会显示用户名两次。

作为系统管理员，你可能会决定将文件的组所有权更改为一个通用组。例如，假设你要将 `composer.txt` 文件的组所有权更改为 `class` 组。为此，请以 `root` 身份登录并输入以下命令：

```
chgrp class composer.txt
```

此 `chgrp` 命令将 `composer.txt` 的组所有权更改为 `class`。在我尝试了此操作后，再次输入 `ls -1` 以验证所有权，以下是我得到的结果：

```
-rw-rw-r-- 1 naba class 40909 Aug 16 20:37 composer.txt
```

你可以使用 `chown` 命令来更改用户所有者。该命令的格式如下：

```
chown username filename
```

例如，要将名为 `sample.jpg` 的文件的所有者更改为 `naba`，我输入：

```
chown naba sample.jpg
```

实际上，`chown` 可以同时将用户和组所有者一起更改。例如，要将用户所有者更改为 `naba`，组所有者更改为 `class`，我输入：

```
chown naba.class composer.txt
```

换句话说，你只需在用户名和组名之间加一个点，然后将它们作为所有者的名称使用即可。

##### 第 3 章：文件系统管理

###### 本章内容

- 浏览 Linux 文件系统
- 使用 NFS 共享文件
- 备份和恢复文件
- 挂载 NFS 文件系统
- 访问 MS-DOS 文件

*文件系统* 指的是文件和目录的组织方式。作为系统管理员，你需要执行某些操作来管理各种存储介质上的文件系统。例如，你必须知道如何*挂载*——通过将存储介质上的文件系统附加到整个 Linux 文件系统来添加文件系统。你还需要备份重要数据并从备份中恢复文件。其他文件系统操作包括通过网络文件系统 (NFS) 共享文件以及访问 MS-DOS 文件。在本章中，我将向你展示如何执行所有文件系统管理任务。

###### 探索 Linux 文件系统

你电脑中的文件和目录以有组织的方式存储信息，就像纸质档案系统一样。当你在纸上存储信息时，你通常会将几页纸放入文件夹，然后将文件夹存放在文件柜中。如果你有很多文件夹，你可能会有某种档案系统。例如，你可能在每个文件夹的标签上贴标签，然后按字母顺序排列在文件柜中。你可能有几个文件柜，每个文件柜都有许多抽屉，而抽屉里又装满了文件夹。

像 Linux 这样的操作系统以类似于纸质档案系统的方式组织计算机中的信息。Linux 使用文件系统来组织计算机中的所有信息。当然，存储介质不是金属文件柜和纸张。相反，Linux 将信息存储在硬盘、软盘驱动器和 CD-ROM 驱动器等设备上。

为了将你的计算机文件系统与纸质档案系统进行类比，请将磁盘驱动器想象为文件柜。文件柜中的抽屉对应于文件系统中的目录。每个抽屉中的文件夹也是目录——因为计算机文件系统中的目录可以包含其他目录。你可以将文件想象为文件夹内的页面——而实际信息就存储在那里。图 3-1 说明了文件柜和 Linux 文件系统之间的类比。

![](img/11709a8f88c8cd03868a929dc94c0e2b_451_0.png)

> **图 3-1:** 这有点牵强，但你可以将 Linux 文件系统想象为类似于文件柜。

Linux 文件系统具有*层次*结构——目录可以包含其他目录，而这些目录又包含单个文件。

你的 Linux 系统中的所有内容都以文件系统中的文件和目录形式组织起来。要访问和使用系统上的文档和程序，你必须熟悉文件系统。

####### 理解文件系统层次结构

Linux 文件系统像树一样组织，有一个 `root`（根）目录，其他所有目录都从该目录分支出来。当你编写完整的路径名时，`root` 目录由单个斜杠 (`/`) 表示。然后是一系列文件和目录的层次结构。文件系统的部分可能位于不同的物理驱动器或不同的硬盘分区上。

Linux 使用标准的目录层次结构。图 3-2 显示了 Linux 文件系统中的一些标准部分。当然，你可以在此结构中的任何位置创建新目录。

通过拼接识别该文件或目录位置的目录名称，并使用正斜杠 (`/`) 作为分隔符，来编写任何文件或目录的名称。例如，在图 3-2 中，顶级 `usr` 目录被写为 `/usr`，因为 `root` 目录 (`/`) 包含 `usr`。另一方面，`X11R6` 目录位于 `usr` 目录内，而 `usr` 目录位于 `root` 目录 (`/`) 内。因此，`X11R6` 目录由名称 `usr/X11R6` 唯一标识。这种完整名称被称为*路径名*，因为该名称标识了你从 `root` 目录到达文件所经过的路径。因此，`/usr/X11R6` 是一个路径名。

![](img/11709a8f88c8cd03868a929dc94c0e2b_452_0.png)

文件系统层次结构标准 (FHS) 规定了类 UNIX 操作系统（如 Linux）中文件和目录的组织方式。FHS 定义了一组标准目录及其预期用途。如果所有 Linux 发行版都忠实采用 FHS，它应有助于提高应用程序、系统管理工具、开发工具和脚本在所有 Linux 发行版之间的互操作性。FHS 甚至有助于系统文档以及像本书这样的书籍，因为对文件系统的相同描述适用于所有 Linux 发行版。FHS 2.3 版于 2004 年 1 月 29 日发布。FHS 2.3 是 Linux 标准基 3.0 版 (LSB 3.0) 的一部分，LSB 3.0 于 2005 年 7 月 1 日发布。LSB 3.0（参见 www.linuxbase.org）是一组旨在减少 Linux 发行版之间差异并促进应用程序可移植性的二进制标准。要了解有关 FHS 的更多信息，请访问 www.pathname.com/fhs 上的 FHS 主页。

Linux 文件系统中的每个标准目录都有特定的用途。表 3-1 总结了这些目录。

**表 3-1 Linux 文件系统中的标准目录**

| 目录 | 用于存储 |
| --- | --- |
| /bin | 用户命令的可执行文件（供所有用户使用） |
| /boot | 引导加载器加载 Linux 内核所需的文件 |
| /dev | 设备文件 |
| /etc | 特定于主机的系统配置文件 |

*（未完待续）*



####### 表 3-1（续）

| 目录 | 用于存储 |
| :--- | :--- |
| /home | 用户主目录 |
| /lib | 共享库和内核模块 |
| /media | 可移动介质的挂载点 |
| /mnt | 临时挂载文件系统的挂载点 |
| /opt | 附加应用程序软件包 |
| /root | 根用户的主目录 |
| /sbin | 系统管理实用工具 |
| /srv | 由该系统提供的服务（如 Web 和 FTP）的数据 |
| /tmp | 临时文件 |

| /usr 层级 | 二级目录层级 |
| :--- | :--- |
| /usr/X11R6 | X Window 系统，第 11 版第 6 次发行 |
| /usr/bin | 大多数用户命令 |
| /usr/include | 头文件目录——这些文件通过各种指令插入到应用程序源代码中——用于开发 Linux 应用程序 |
| /usr/lib | 软件包和编程使用的库 |
| /usr/libexec | 应用程序库 |
| /usr/local | 任何本地软件 |
| /usr/sbin | 非必需的系统管理员实用工具 |
| /usr/share | 不依赖于系统架构（无论是 Intel PC 还是 Sun SPARC 工作站）的共享数据 |
| /usr/src | 源代码 |

| /var 层级 | 可变数据 |
| :--- | :--- |
| /var/cache | 应用程序的缓存数据 |
| /var/lib | 与应用当前状态相关的信息 |
| /var/lock | 锁定文件，以确保资源仅被一个应用程序使用 |
| /var/log | 组织到子目录中的日志文件 |
| /var/mail | 用户邮件箱文件 |
| /var/opt | 存储在 /opt 目录中的软件包的可变数据 |
| /var/run | 描述系统自启动以来的数据 |
| /var/spool | 等待某种处理的数据 |
| /var/tmp | 在系统重启之间保留的临时文件 |
| /var/yp | 网络信息服务 (NIS) 数据库文件 |

###### 在文件系统上挂载设备

  您在 Linux 中使用的存储设备包含 Linux 文件系统。每个设备都有自己本地的文件系统，由目录层级组成。在您能够访问设备上的文件之前，必须将设备的目录层级附加到代表整体 Linux 文件系统的树结构中。

  挂载是执行的操作，目的是使物理存储设备（硬盘分区或 CD-ROM）上的文件系统表现为 Linux 文件系统的一部分。图 3-3 说明了挂载的概念。

![](img/11709a8f88c8cd03868a929dc94c0e2b_454_0.png)

**图 3-3：** 在访问设备之前，必须先在 Linux 文件系统上挂载该设备。

  图 3-3 显示每个设备都有一个以 `/dev` 开头的名称。例如，`/dev/cdrom` 是第一个 DVD/CD-ROM 驱动器，`/dev/fd0` 是软盘驱动器。这些物理设备在 Linux 文件系统的特定挂载点上被挂载。例如，DVD/CD-ROM 驱动器 `/dev/cdrom` 在文件系统上挂载于 `/media/cdrom`。以这种方式挂载 CD-ROM 后，CD-ROM 或 DVD-ROM 上的 Fedora 目录在 Linux 文件系统中表现为 `/media/cdrom/Fedora`。

  您可以使用 `mount` 命令将设备手动挂载到 Linux 文件系统的指定目录上。该目录即为**挂载点**。例如，要将 DVD/CD-ROM 驱动器挂载到 `/media/cdrom` 目录，请键入以下命令（在登录为 `root` 后）：

```
mount /dev/cdrom /media/cdrom
```

  如果 DVD/CD-ROM 设备已经挂载，或者驱动器中没有 CD 或 DVD 介质，`mount` 命令会报告错误。否则，`mount` 操作成功，您可以通过 `/media/cdrom` 目录访问 DVD 或 CD 的内容。

![](img/11709a8f88c8cd03868a929dc94c0e2b_455_0.png)

  您可以使用任何目录作为挂载点。但是，如果您将设备挂载到非空目录上，那么在该目录中，直到您使用 `umount` 命令卸载该设备，您将无法访问其中的文件。因此，始终使用空目录作为挂载点。

![](img/11709a8f88c8cd03868a929dc94c0e2b_455_1.png)

  当不再需要设备时，请使用 `umount` 命令卸载该设备。例如，对于设备名为 `/dev/cdrom` 的 DVD/CD-ROM 设备，请键入以下命令以卸载该设备：

```
umount /dev/cdrom
```

  只要没有人在使用 DVD/CD-ROM，`umount` 命令就会成功。如果您在尝试卸载 DVD/CD-ROM 时遇到错误，请检查当前工作目录是否在 DVD 或 CD 上。如果您当前正在 DVD/CD-ROM 的某个目录中工作，这也算作对 DVD/CD-ROM 的使用。

###### 检查 /etc/fstab 文件

  `mount` 命令的一般格式如下：

```
mount device-name mount-point
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_455_2.png)

  然而，只要 `/etc/fstab` 文件中存在 CD-ROM 挂载点的条目，您就可以通过仅指定 CD-ROM 设备名称或挂载点名称来进行挂载。该条目指定了 CD-ROM 设备名称和文件系统类型。这就是为什么您可以使用更短的 `mount` 命令来挂载 CD-ROM 的原因。

![](img/11709a8f88c8cd03868a929dc94c0e2b_455_3.png)

  例如，在 Debian 中，您可以通过键入以下任一命令来挂载 CD-ROM：

```
mount /dev/cdrom
mount /media/cdrom
```

  `/etc/fstab` 文件是一个*配置文件*——一个包含 `mount` 和 `umount` 命令所用信息的文本文件。`/etc/fstab` 文件中的每一行都提供了有关设备及其在 Linux 文件系统中的挂载点的信息。本质上，`/etc/fstab` 文件将文件系统内的各种挂载点与特定设备关联起来，这使得 `mount` 命令可以在命令行上仅以挂载点或设备作为参数来工作。

  这是一个来自 SUSE 系统的 `/etc/fstab` 文件。（其他 Linux 发行版中的文件格式类似。）

![](img/11709a8f88c8cd03868a929dc94c0e2b_456_0.png)

```
/dev/hda1 / reiserfs acl,user_xattr 1 1
/dev/hda7 /boot ext3 acl,user_xattr 1 2
/dev/hda6 /data1 auto noauto,user 0 0
/dev/hda9 /data2 auto noauto,user 0 0
/dev/hda10 /data3 auto noauto,user 0 0
/dev/hda5 /data4 auto noauto,user 0 0
/dev/hda2 /windows/C ntfs ro,users,gid=users,umask=0002,nls=utf8 0 0
/dev/hda8 swap swap pri=42 0 0
devpts /dev/pts devpts mode=0620,gid=5 0 0
proc /proc proc defaults 0 0
usbfs /proc/bus/usb usbfs noauto 0 0
sysfs /sys sysfs noauto 0 0
/dev/cdrecorder /media/cdrecorder auto fsecdss,ro,procuid,nodev,exec,locharsets=utf8 0 0
/dev/fd0 /media/floppy auto fs=loopppyfs,procuid,nodev,nosuid,sync 0 0
```

  每行的第一个字段显示设备名称，如硬盘分区。第二个字段是挂载点，第三个字段指示设备上的文件系统类型。目前您可以忽略最后三个字段。

  这个 `/etc/fstab` 文件表明 `/dev/hda8` 设备作为虚拟内存的交换设备，这就是为什么挂载点和文件系统类型都设置为 `swap` 的原因。

  Linux 操作系统使用 `/etc/fstab` 文件的内容自动挂载各种文件系统。在 Linux 启动期间，`init` 进程执行一个 shell 脚本，该脚本运行 `mount -a` 命令。该命令读取 `/etc/fstab` 文件并挂载所有列出的文件系统（除了带有 `noauto` 选项的那些）。`/etc/fstab` 每行的第三个字段指定该设备上的文件系统类型，第四个字段显示 `mount` 命令在将设备挂载到文件系统时使用的以逗号分隔的选项列表。通常，您在此字段中发现 `defaults` 选项。`defaults` 选项意味着——除其他事项外——设备在启动时挂载，只有 `root` 用户才能挂载该设备，并且该设备用于读和写。如果选项包含 `noauto`，则设备不会在系统启动时自动挂载。

![](img/11709a8f88c8cd03868a929dc94c0e2b_456_1.png)




###### 使用 NFS 共享文件

在 Fedora Core 中，您经常会在 `/etc/fstab` 条目的第四字段中发现 `managed` 选项。`managed` 选项表示该行是由 **HAL**（硬件抽象层）守护进程添加到 `fstab` 文件中的，该守护进程运行 `fstab-sync` 命令，为检测到的每个可移动驱动器在 `/etc/fstab` 文件中添加条目。您通常会发现 DVD/CD-ROM 驱动器（在大多数系统中为 `/dev/hdc`）和软盘驱动器（`/dev/fd0`）的条目在第四字段中包含 `managed` 选项。

###### 使用 NFS 共享文件

通过 NFS 共享文件很简单，涉及两个基本步骤：

- 在 NFS 服务器上，通过将它们列在 `/etc/exports` 文件中并运行 `/usr/sbin/exportfs` 命令来**导出一个或多个目录**。此外，您必须运行 NFS 服务器。
- 在每个客户端系统上，使用 `mount` 命令挂载服务器已导出的目录。

启动 NFS 服务器的方式取决于 Linux 发行版。如果有 GUI 系统管理工具，您可以从该 GUI 工具启动 NFS 服务器。否则，您可以在终端窗口中输入命令来启动 NFS 服务器。例如，在 Debian 中，您可以输入 `invoke-rc.d nfs-kernel-server start` 和 `invoke-rc.d nfs-common start` 来启动 NFS 服务器。在 Fedora Core 中，输入 `service nfs start`。在 SUSE 中，您可以使用 YaST 控制中心（主菜单 > 系统 > YaST）来启动 NFS 服务器。（它位于网络服务类别中。）在 Xandros 中，您可以从 Xandros 控制中心（主菜单 > 控制中心）启动 NFS 服务器，或者在终端窗口中输入 `invoke-rc.d nfs-user-server start`。

使用 NFS 的唯一问题是每个客户端系统必须支持它。大多数 PC 并不附带 NFS——这意味着如果您想通过 NFS 共享文件，必须单独购买 NFS 软件。然而，如果您局域网上的所有系统都运行 Linux（或其他内置 NFS 支持的 UNIX 变体），那么使用 NFS 是有意义的。

> NFS 存在安全漏洞。因此，请勿在直接连接到 Internet 的系统上设置 NFS。

在下一节中，我将引导您完成一个 NFS 设置，以一个局域网中两台 Linux PC 的示例进行说明。

####### 使用 NFS 导出文件系统

首先从**导出**（即向客户端系统提供目录内容）目录内容的服务器系统开始。在服务器上，您必须运行 NFS 服务，并指定一个或多个要导出到客户端系统的文件系统。

![](img/11709a8f88c8cd03868a929dc94c0e2b_458_0.png)

要导出文件系统，您必须在 `/etc/exports` 文件中添加适当的条目。例如，假设您想导出 `/home` 目录，并希望启用名为 **LNBp75** 的主机对该文件系统进行读写操作挂载。（您可以使用主机的 IP 地址代替主机名。）您可以通过在 `/etc/exports` 文件中添加以下条目来实现：

```
/home  LNBp75 (rw)
```

如果使用主机的 IP 地址，条目可能看起来像这样：

```
/home  192.168.0.2 (rw)
```

这指定 192.168.0.2 是允许对 `/home` 目录具有完全访问权限的主机的 IP 地址。

在 `/etc/exports` 文件中添加条目后，使用适合您的 Linux 发行版的方法启动 NFS 服务器。例如，在 Fedora Core 中，我以 *root* 身份登录，并在终端窗口中输入以下命令：

```
service nfs start
```

当 NFS 服务启动时，NFS 的服务器端准备就绪。现在您可以尝试从客户端系统挂载导出的文件系统并访问该导出的文件系统。

![](img/11709a8f88c8cd03868a929dc94c0e2b_458_1.png)

如果您对 `/etc/exports` 文件中列出的导出文件系统进行了任何更改，请记住重启 NFS 服务。例如，在 Fedora Core 中，我在终端窗口中输入 `service nfs restart`。在 Xandros 中，我输入 `invoke-rc.d nfs-user-server restart`。

####### 挂载 NFS 文件系统

要在客户端系统上访问导出的 NFS 文件系统，您必须将该文件系统挂载到一个*挂载点*——从实际意义上讲，挂载点不过是一个本地目录。例如，假设您想访问由名为 **LNBp200** 的服务器导出的 `/home` 目录，并在客户端系统的本地目录 `/mnt/lnbp200` 上进行访问。为此，请遵循以下步骤：

1. 以 *root* 身份登录并使用以下命令创建目录：
   `mkdir /mnt/lnbp200`
2. 输入以下命令以执行*挂载*操作：
   `mount lnbp200:/home/public /mnt/lnbp200`
3. 如果您只知道服务器的 IP 地址，请将主机名（在此情况下为 lnbp200）替换为 IP 地址。
4. 使用命令 cd /mnt/lnbp200 更改目录到 /mnt/lnbp200。

现在，您可以从该目录查看和访问导出的文件。

要确认 NFS 文件系统确实已挂载，请以 root 身份在客户端系统上登录，并在终端窗口中输入 mount。您会看到类似以下关于 NFS 文件系统的行：

```
lnbp200:/home//public on /mnt/lnbp200 type nfs (rw,addr=192.168.1.200)
```

###### 备份和恢复文件

备份和恢复文件是一项关键的系统管理任务。如果您的系统硬盘发生故障，您必须依靠备份来恢复重要文件。在这里，我介绍了一些备份策略，描述了多种备份介质，并解释了如何使用随 Linux 附带的磁带归档工具（tar）程序来备份和恢复文件。此外，您还将了解如何在磁带上执行增量和自动备份。

如果您有 CD 刻录机，还可以通过将文件刻录到 CD-R 上来备份文件。请参阅第二册第四章，了解可以使用哪些应用程序来刻录数据 CD。

####### 选择备份策略和介质

您的 Linux 系统硬盘包含使系统运行所需的一切——以及其他文件（例如文档和数据库），这些文件使您的业务保持运行。您必须备份这些文件，以便在硬盘崩溃时能够快速恢复并将系统恢复到正常状态。通常，您必须遵循严格的定期备份制度，因为您永远无法预测硬盘何时会失效或文件系统何时会损坏。要实施这样的制度，首先决定您要备份哪些文件、频率如何以及使用什么备份存储介质。这就是我所指的选择备份策略和备份介质的过程。

您对备份策略和备份介质的选择取决于您对因硬盘故障而导致业务中断风险的评估。根据您对 Linux 系统的使用方式，磁盘故障可能对您的影响可大可小。

例如，如果您将 Linux 系统用作学习工具（为了了解更多关于 Linux 或编程的信息），您可能只需要备份一些用于配置 Linux 的系统文件。在这种情况下，您的备份策略可以是每次更改任何系统配置时，将重要的系统配置文件保存在一个或多个软盘上。

另一方面，如果您将 Linux 系统用作提供共享文件存储的办公室服务器，供许多用户使用，那么因磁盘故障导致业务中断的风险要高得多。在这种情况下，您必须每周备份所有文件，并每天备份任何新增或更改的文件。您可以以自动化的方式执行这些备份（使用本小册子第一章中描述的任务调度功能）。此外，您可能需要一个能够存储大量（数 GB）数据的备份存储介质。换句话说，对于高风险情况，您的备份策略更加复杂，并需要额外的设备（例如磁带机）。

您对备份介质的选择取决于您要备份的数据量。对于少量数据（例如系统配置文件），您可以使用软盘或 USB 闪存盘作为备份介质。如果您的 PC 有 Zip 驱动器，您可以使用 Zip 磁盘作为备份介质；这些适合备份单个用户目录。要备份整个服务器，请使用磁带机，通常是连接到 SCSI 控制器的 4mm 或 8mm 磁带机。此类磁带机每条磁带可存储数 GB 的数据，您可以使用它们在一条磁带上备份整个文件系统。

将这些介质上的文件备份时，您必须通过名称引用备份设备。表 3-2 列出了某些常见备份设备的设备名称。

**表 3-2** 常见备份设备的名称

| 备份设备 | Linux 设备名称 |
| :--- | :--- |
| 软盘 | `/dev/fd0` |
| IDE Zip 驱动器 | `/dev/hdc4` 或 `/dev/hdd4` |
| SCSI Zip 驱动器 | `/dev/sda`（假设它是第一个 SCSI 驱动器——否则，设备名称取决于 SCSI ID） |
| SCSI 磁带机 | `/dev/st0` 或 `/dev/nst0`（`n` 前缀表示文件复制到磁带后磁带不会倒带。） |

####### Linux 的商业备份工具

在下一节中，我将解释如何使用随 Linux 附带的磁带归档工具（tar）程序来备份和恢复文件。虽然您可以使用 tar 管理备份，但有许多商业备份工具



通过图形用户界面和其他功能简化备份操作。以下是一些知名的用于 Linux 的商业备份工具：

- BRU：来自 TOLIS Group, Inc. 的备份和恢复工具（www.tolisgroup.com）
- LONE-TAR：来自 Lone Star Software Corp. 的磁带备份软件包（www.cactus.com）
- Arkeia：Arkeia 公司提供的针对异构网络的备份和恢复软件（www.arkeia.com）
- Bare Metal Plus：UniTrends 公司提供的备份和恢复软件（www.unitrends.com）
- Brightstor ARCserve Backup for Linux：Computer Associates 公司提供的 Linux 系统数据保护技术（www3.ca.com/solutions/product.asp?id=3370）

###### 使用磁带归档工具——tar

你可以使用 tar 命令将文件归档到设备，例如软盘或磁带。tar 程序会创建一个归档文件，该文件可以包含其他目录和文件，并且（可选地）对归档进行压缩以进行高效存储。然后，归档会被写入指定的设备或另一个文件。事实上，许多软件包都是以压缩的 tar 文件形式分发的。

tar 程序的命令语法如下：

```
tar options destination source
```

这里，选项通常由一系列单个字母指定，每个字母指定 tar 的操作。destination（目标）是备份设备的设备名称。而 source（源）是一个文件或目录名的列表，表示要备份的文件。

####### 备份和恢复单卷归档

例如，假设你想将 /etc/X11 目录的内容备份到软盘上。登录 root 用户，将软盘放入软驱，并输入以下命令：

```
tar zcvf /dev/fd0 /etc/X11
```

tar 程序会在每个文件复制到软盘上的压缩 tar 归档时显示文件名的列表。在这种情况下，选项是 zcvf，目标是 `/dev/fd0`（软盘），源是 `/etc/X11` 目录（这隐含了其所有子目录及其内容）。你可以使用类似的 `tar` 命令将文件备份到磁带——只需将 `/dev/fd0` 替换为磁带设备——例如 SCSI 磁带驱动器的 `/dev/st0`。

表 3-3 定义了几个常见的 `tar` 选项。

| Table 3-3 | 常见的 tar 选项 |
| :--- | :--- |

要查看你在软盘上创建的 `tar` 归档的内容，请输入以下命令：

```
tar ztf /dev/fd0
```

你会看到一份文件名列表（每个都以 `/etc/X11` 开头），指示备份中包含的内容。在这个 `tar` 命令中，`t` 选项用于列出 `tar` 归档的内容。

要从 `tar` 备份中提取文件，请在登录为 `root` 的状态下执行以下步骤：

1. **输入以下命令将目录更改为 `/tmp`：**

   ```
   cd /tmp
   ```

   这一步是你可以练习从 `tar` 备份中提取文件的地方。对于实际的备份，请将目录更改为适当的位置（通常，你输入 `cd /`）。

2. **输入以下命令：**

   ```
   tar zxvf /dev/fd0
   ```

   这个 `tar` 命令使用 `x` 选项从存储在 `/dev/fd0`（软盘）上的归档中提取文件。

现在，如果你检查 `/tmp` 目录的内容，你会注意到 `tar` 命令在 `/tmp` 中创建了一个 `etc/X11` 目录树，并将 `tar` 归档中的所有文件恢复到该目录中。`tar` 命令会剥离归档中文件名前面的 `/`，并将文件恢复到当前目录中。如果你想从软盘上的归档中恢复 `/etc/X11` 目录，请使用以下命令：

```
tar zxvrf /dev/fd0 -C /
```

命令末尾的 `/` 表示你希望恢复备份文件的目录。

你可以使用 `tar` 命令创建、查看和恢复归档。你可以将归档存储在文件中，或存储在你通过设备名称指定的任何设备中。

## *备份和恢复多卷归档*

有时，单个存储介质的容量小于存储归档所需的总存储空间。在这种情况下，你可以使用 `M` 选项来创建多卷归档——这意味着归档可以跨越多个磁带或软盘。但请注意，你无法创建压缩的多卷归档。这意味着你必须去掉 `z` 选项。要了解多卷归档是如何工作的，请登录 `root`，将一张软盘放入软驱，并输入以下 `tar` 命令：

```
tar cvfM /dev/fd0 /usr/share/doc/ghostscript*
```

**注意：** `M` 选项包含在选项字母中；它告诉 `tar` 创建多卷归档。当第一张软盘填满时，`tar` 命令会提示你准备第二张软盘。当你看到以下提示时，取出第一张软盘并插入另一张软盘：

```
Prepare volume #2 for '/dev/fd0' and hit return:
```

当你按下回车键时，`tar` 程序将继续使用第二张软盘。在这个例子中，你只需要两张软盘来存储归档；对于更大的归档，如果需要更多软盘，`tar` 程序会继续提示你插入软盘。

要从这个多卷归档中恢复，请键入 `cd /tmp` 将目录更改为 `/tmp`。（这里我使用 `/tmp` 目录作为演示目的，但当你从归档中恢复文件时，你必须使用真实的目录。）然后键入

```
tar xvfm /dev/fd0
```

*tar* 程序会在必要时提示你插入软盘。

- **提示**：使用 *du -s* 命令来确定归档一个目录所需的存储空间。例如，输入 *du -s /etc* 即可查看 /etc 目录以千字节为单位的总大小。以下是该命令的典型输出：
  > 35724 /etc
  
  输出的结果表明，备份 /etc 目录至少需要 35,724K 的存储空间。

####### 在磁带上进行备份

虽然在 *tar* 命令中使用正确的设备名称即可在磁带上进行备份，但你需要了解一些磁带设备的细微之处才能很好地使用它。当你使用 *tar* 备份到名为 */dev/st0*（第一个 SCSI 磁带驱动器）的设备时，磁带设备会在 *tar* 程序完成将归档复制到磁带后自动将磁带倒带。*/dev/st0* 设备被称为可倒带磁带设备，因为它默认会倒带。

如果你的磁带可以容纳数 GB 的数据，你可能希望将多个 *tar* 归档——一个接一个地——写入同一盘磁带（否则磁带的很大一部分可能会空着）。如果你打算这样做，你的磁带设备就不能在 *tar* 程序结束后倒带。为了帮助处理这种情况，几个 Linux 磁带设备是不可倒带的。不可倒带的 SCSI 磁带设备被称为 */dev/nst0*。如果你想在磁带上一个接一个地写入归档，请使用此设备名称。

- **提示**：在每个归档之后，不可倒带磁带设备会写入一个文件结束（EOF）标记，以将一个归档与下一个分隔开。使用 *mt* 命令来控制磁带——你可以从一个标记移动到下一个，或将磁带倒带。例如，在你使用 */dev/nst0* 设备名称向磁带写入多个归档后，你可以使用以下命令强制磁带倒带：
  > mt -f /dev/nst0 rewind
  
  倒带后，你可以使用以下命令将文件从第一个归档提取到当前磁盘目录：
  > tar xvrf /dev/nst0
  
  之后，你必须越过 EOF 标记以到达下一个归档。为此，请使用以下 *mt* 命令：
  > mt -f /dev/nst0 ffs 1

这将磁带定位到下一个归档的开头。现在再次使用 `tar xvf` 命令读取此归档。

![](img/11709a8f88c8cd03868a929dc94c0e2b_465_0.png)

如果你在磁带上保存多个归档，你必须自己记录归档的顺序。归档的顺序可能很难记住，所以你最好还是每张磁带上只保存一个归档。

####### 执行增量备份

假设你使用 `tar` 将系统硬盘备份到磁带上。由于这种完整备份可能需要相当长的时间，你不想每晚都重复这项任务。（此外，一天中可能只有少数文件发生了变化。）要定位需要备份的文件，你可以使用 `find` 命令列出过去 24 小时内发生变化的所有文件：

```
find / -mtime -1 -type f -print
```

此命令打印出过去一天内发生变化的文件列表。`-mtime -1` 选项表示你想要最后修改时间少于一天的文件。现在，你可以将此 `find` 命令与 `tar` 命令结合使用，仅备份过去一天内发生变化的那些文件：

```
tar cvf /dev/st0 `find / -mtime -1 -type f -print`
```

当你在单个反引号之间放置一个命令时，shell 会执行该命令并将其输出放在命令行中的该位置。最终结果是 `tar` 程序仅在归档中保存已更改的文件。这个过程为你提供的是自前一天以来仅包含已更改文件的增量备份。

####### 执行自动备份

在本小书的第一章中，我向你展示了如何使用 `crontab` 设置定期任务（称为 `cron 任务`）。Linux 系统会以固定的间隔执行这些任务。备份系统是 `crontab` 功能的良好用途。假设你的备份策略如下：

- ✦ 每周日凌晨 1:15，系统将整个硬盘备份到磁带上。
- ✦ 周一至周六，系统在凌晨 3:10 执行增量备份，仅保存过去 24 小时内发生变化的文件。

要设置此自动备份计划，请登录 `root` 并在名为 `backups` 的文件中输入以下行（此示例假设你使用 SCSI 磁带驱动器）：


tar zcvf /dev/st0 / | find / -mtime -1 -type f -print

接下来，使用以下 crontab 命令提交此作业计划：

```
crontab backups
```

现在，您的自动备份已经配置完成。您只需要每天在磁带驱动器中放入一条新磁带即可。请记住为每条磁带贴上合适的标签。

###### 访问 DOS/Windows 文件系统

如果您的硬盘上安装了 Microsoft Windows 95/98/Me，您可能已经将在 Linux 下挂载了 DOS/Windows 分区。如果没有，您可以在 Linux 中轻松地挂载 DOS/Windows 分区。挂载会使 DOS/Windows 目录层次结构看起来像是 Linux 文件系统的一部分。

####### 挂载 DOS/Windows 磁盘分区

要在 Linux 中挂载 DOS/Windows 硬盘分区或软盘，请使用 mount 命令，但需包含 -t vfat 选项以将文件系统类型指定为 DOS。例如，如果您的 DOS 分区恰好位于您的 IDE（集成驱动电子设备）硬盘的第一个分区，并且您想将其挂载到 /dos，请使用以下 mount 命令：

```
mount -t vfat /dev/hda1 /dos
```

mount 命令中的 -t vfat 部分指定您要挂载的设备——/dev/hda1——具有 MS-DOS 文件系统。图 3-4 展示了此 mount 命令的效果。

图 3-4 显示了 DOS 分区中的目录如何映射到 Linux 文件系统。在 DOS 下为 C:\DOS 的目录在 Linux 下变为 /dos/dos。同样，C:\WINDOWS 现在变为 /dos/windows。您可能已经看出了其中的规律。要将 DOS 文件名转换为 Linux 格式（当您将 DOS 分区挂载到 /dos 时），请执行以下步骤：

- 1. 将 DOS 名称改为小写。
- 2. 将 C:\ 改为 /dos/。
- 3. 将所有反斜杠 (\) 改为斜杠 (/)。

以下是如何将 DOS 分区挂载到 /dos 目录的方法。

![](img/11709a8f88c8cd03868a929dc94c0e2b_467_0.png)

####### 挂载 DOS 软盘

就像将 DOS 硬盘分区挂载到 Linux 文件系统一样，您也可以挂载 DOS 软盘。您必须以 root 身份登录才能挂载软盘，但您可以遵循本节后半部分所示的步骤来设置系统，以便任何用户都可以挂载 DOS 软盘。您还必须知道软盘驱动器的设备名称。默认情况下，Linux 定义了以下两个通用软盘设备名称：

- /dev/fd0 是 A 驱动器（第一个软盘驱动器）
- /dev/fd1 是 B 驱动器（第二个软盘驱动器，如果有的话）

至于挂载点，您可以使用文件系统中的任何空目录作为挂载点，但 Linux 系统自带一个专门用于挂载软盘的目录 /media/floppy。

要将 DOS 软盘挂载到 /media/floppy 目录，请将软盘放入驱动器并键入以下命令：

```
mount -t vfat /dev/fd0 /media/floppy
```

挂载软盘后，您可以使用 Linux 复制命令（*cp*）将文件复制到软盘或从软盘复制文件。要将当前目录中的文件 gnomel.pcx 复制到软盘，请键入以下内容：

```
cp gnomel.pcx /media/floppy
```

同样地，要查看软盘的内容，请键入以下内容：

```
ls /media/floppy
```

如果您想将软盘从驱动器中取出，请先*卸载*软盘驱动器。卸载会移除软盘文件系统与 Linux 文件系统上的挂载点之间的关联。使用 *umount* 命令以如下方式卸载软盘：

```
umount /dev/fd0
```

您可以设置 Linux 系统，使任何用户都可以挂载 DOS 软盘。例如，要允许任何用户在 A 驱动器的 /a 目录上挂载 DOS 软盘，请执行以下步骤：

- 1. **以** *root* **身份登录。**
- 2. **在终端窗口中键入以下命令，创建** `/a` **目录（挂载点）：**

```
mkdir /a
```

- 3. **在文本编辑器（如** *vi* **或** *emacs* **）中编辑** `/etc/fstab` **文件，插入以下行，然后保存文件并退出编辑器：**

```
/dev/fd0 /a vfat noauto,user 0 0
```

该行中的第一个字段是软盘驱动器的设备名称（*\/dev/fd0*）；第二个字段是挂载目录（*\/a*）；第三个字段显示文件系统类型（*vfat*）。*user* 选项（位于 *noauto* 旁边）允许所有用户挂载 DOS 软盘。

- 4. **注销，然后以普通用户身份重新登录。**
- 5. **要确认您可以像普通用户而不是** *root* **那样挂载 DOS 软盘，请在 A 驱动器中插入一张 DOS 软盘并键入以下命令：**

```
mount /a
```

*mount* 操作成功，当您键入命令 *ls /a* 时，您会看到 DOS 软盘的目录列表。

- 6. **要卸载 DOS 软盘，请键入** *umount /a*。

####### 挂载 NTFS 分区

如今，大多数电脑都预装了 Windows XP 或 Windows 2000。Windows XP 和 2000 以及 Windows NT 通常使用 NT 文件系统（NTFS）。Linux 支持对 NTFS 分区的只读访问，许多发行版都包含访问 NTFS 分区所需的 ntfs.ko 内核模块。

如果您在 Windows XP 系统上安装了 Linux，并希望访问 NTFS 分区上的文件，但您的发行版不包含 ntfs.ko 模块，您可以在内核配置步骤中启用 NTFS 模块后重新编译内核。（有关配置、编译和安装内核的详细说明，请参见本书第 5 章。）

在重新编译并从新内核启动后，以 root 身份登录，并键入以下命令为 NTFS 分区创建挂载点。（在这种情况下，我正在 /mnt 目录中创建一个挂载点。）

```
mkdir /mnt/xp
```

现在，您可以使用以下命令挂载 NTFS 分区：

```
mount /dev/hda2 /mnt/xp -t ntfs -r -o umsk=0222
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_469_0.png)

请将 /dev/hda2 替换为您系统中 NTFS 分区的设备名称。在大多数预装 Windows XP 的电脑上，NTFS 分区是第二个分区（/dev/hda2）——第一个分区（/dev/hda1）通常是一个隐藏分区，用于保存 Windows XP 安装所用的文件。

####### 使用 mtools

访问 MS-DOS 文件系统的一种方法是先使用 mount 命令挂载 DOS 硬盘或软盘，然后使用常规 Linux 命令（如 ls 和 cp）来处理已挂载的 DOS 文件系统。这种挂载 DOS 文件系统的方法对于硬盘来说是合适的。Linux 可以在启动时自动挂载 DOS 分区，您可以随时访问硬盘上的 DOS 目录。

然而，如果您想快速列出 DOS 软盘的目录，挂载可能很快就会变得相当繁琐。首先，您必须挂载软盘驱动器。然后，您必须使用 ls 命令。最后，在将软盘弹出驱动器之前，您必须使用 umount 命令。

正是在这种情况下，mtools 软件包派上了用场。mtools 软件包实现了大多数常见的 DOS 命令；这些命令使用与 DOS 中相同的名称，只是您在每个命令前加一个 m 前缀。因此，获取目录列表的命令是 mdir，而 mcopy 用于复制文件。mtools 最棒的一点是，使用 mtools 命令时不需要挂载软盘。

![](img/11709a8f88c8cd03868a929dc94c0e2b_470_0.png)

由于 mtools 命令会向物理设备（软盘）写入和读取，因此您必须以 root 身份登录才能执行这些命令。如果您希望任何用户都能访问 mtools 命令，您必须更改软盘驱动器设备的权限设置。使用以下命令允许任何人读写第一个软盘驱动器：

```
chmod o+rw /dev/fd0
```

######## 试用 mtools

要试用 mtools，请遵循以下步骤：

- 1. 将一张 MS-DOS 软盘放入系统的 A 驱动器中。
- 2. 键入 mdir。

您将看到软盘的目录（采用标准的 DOS 目录列表格式）。

通常，您使用 mtools 实用程序来访问软盘。默认配置文件 /etc/mtools.conf 设置为将软盘驱动器作为 A 驱动器访问。虽然您可以编辑该文件以定义 DOS 硬盘分区的 C 和 D 驱动器，但您也可以通过使用 Linux mount 命令来挂载它们从而访问硬盘分区。因为您可以自动在启动时挂载硬盘分区，所以通过 Linux 命令访问它们通常同样容易。

######## 理解 /etc/mtools.conf 文件

mtools 软件包在默认设置下可以正常工作，但如果您遇到任何错误，请检查 /etc/mtools.conf 文件。该文件包含 mtools 实用程序所看到的驱动器（如 A、B 和 C）的定义。以下是典型的 /etc/mtools.conf 文件中的几行：

```
drive a: file="/dev/fd0" exclusive mformat_only
drive b: file="/dev/fd1" exclusive mformat_only
# First SCSI hard disk partition
#drive c: file="/dev/sda1"
# First IDE hard disk partition on a Windows 98 PC
drive c: file="/dev/hda1"
# Internal IDE Zip drive
drive e: file="/dev/hdd4" exclusive
```

井号 (#) 表示注释的开始。每一行定义一个驱动器盘符、关联的 Linux 设备名称以及指示如何访问该设备的某些关键字。在此示例中，前两行定义了驱动器 A 和 B。第三个非注释行将驱动器 C 定义为第一个分区，位于



第一个 IDE 驱动器（`/dev/hda1`）。如果你有其他的 DOS 驱动器（例如 D），你可以添加另一行，将 D 驱动器定义为相应的磁盘分区。

如果你的系统的 A 驱动器是高密度 3.5 英寸驱动器，你无需更改默认的 `/etc/mtools.conf` 文件中的任何内容即可访问软驱。如果你还想访问硬盘中的任何 DOS 分区，请取消 C 驱动器相应行的注释并进行编辑。

你还可以通过 mtools 访问 Iomega Zip 驱动器。只需指定驱动器字母和相应设备的文件名。对于内置的 IDE（ATAPI）Zip 驱动器，请尝试将 `/dev/hdd4` 作为设备文件，并在 `/etc/mtools.conf` 文件中添加以下行：

```
drive e: file="/dev/hdd4"
```

之后，你可以使用 mtools 命令访问 Zip 驱动器（将其视为 E 驱动器）。例如，要查看目录列表，请将 Zip 盘放入 Zip 驱动器并输入：

```
mdir e:
```

####### 学习 mtools 命令

mtools 包是一组实用工具。到目前为止，我一直在使用 mdir —— 它是 DOS 中 DIR 命令的 mtools 对应版本。其他 mtools 命令也很容易使用。

如果你熟悉 MS-DOS 命令，使用 mtools 命令就很简单了。以小写字母输入 DOS 命令，并记得在每个命令前面加上 m。由于 Linux 命令和文件名是区分大小写的，因此在输入 mtools 命令时必须全部使用小写字母。

表 3-4 总结了 mtools 中可用的命令。

| mtools 工具 | MS-DOS 命令（如果有） | mtools 工具执行以下操作 |
| :--- | :--- | :--- |
| mattrb | ATTRIB | 更改 MS-DOS 文件属性标志 |
| mbadblocks | | 测试软盘并在文件分配表 (FAT) 中标记坏块 |
| mcd | CD | 更改 MS-DOS 目录 |
| mcopy | COPY | 在 MS-DOS 和 Linux 之间复制文件 |
| mdel | DEL 或 ERASE | 删除 MS-DOS 文件 |
| mdeltree | DELTREE | 递归删除 MS-DOS 目录 |
| mdir | DIR | 显示 MS-DOS 目录列表 |
| mdu | | 列出目录及其内容所占用的空间 |
| mformat | FORMAT | 在已低级格式化的软盘上建立 MS-DOS 文件系统（在 Linux 中使用 fdformat 对软盘进行低级格式化。） |
| minfo | | 获取有关 MS-DOS 文件系统的信息 |
| mkmanifest | | 创建短名称等效项列表 |
| mlabel | LABEL | 初始化 MS-DOS 卷标 |
| mmd | MD 或 MKDIR | 创建 MS-DOS 目录 |
| mmovc | | 移动或重命名 MS-DOS 文件或子目录 |
| mmount | | 挂载 MS-DOS 磁盘 |
| mpartition | | 将 MS-DOS 文件系统创建为分区 |
| mrd | RD 或 RMDIR | 删除 MS-DOS 目录 |
| mren | REN 或 RENAME | 重命名现有的 MS-DOS 文件 |
| mshowfat | | 显示 MS-DOS 文件的 FAT 条目 |
| mtooletest | | 测试并显示当前的 mtools 配置 |
| mtype | TYPE | 显示 MS-DOS 文件的内容 |
| mwrite | COPY | 将 Linux 文件复制到 MS-DOS |
| mzip | | 在 SCSI Zip 磁盘上执行某些操作 |

你可以像使用对应的 DOS 命令一样使用 *mtools* 命令。例如，*mdir* 命令的作用与 DOS 中的 *DIR* 命令相同。表 3-4 中显示的所有其他 *mtools* 命令也是如此。

你可以使用通配符（例如 *）配合 *mtools* 命令，但你必须记住 Linux shell 是第一个看到你的命令的程序。如果你不想让 shell 到处展开通配符字符，请在包含任何通配符字符的文件名周围使用引号。例如，要复制 A 驱动器上的所有 *.txt 文件到当前目录，请使用以下命令：

```
mcopy "a:*.txt" .
```

如果你省略了引号，shell 将尝试使用当前 Linux 目录中的文件名展开字符串 a:*.txt。它还会尝试从 DOS 软盘复制这些文件（如果有）。

另一方面，如果你想从 Linux 目录复制文件到 DOS 软盘，你确实希望 shell 展开任何通配符字符。例如，要复制当前 Linux 目录中的所有 *.jpg 文件到 DOS 软盘，请像这样使用 `mcopy`：

```
mcopy *.jpg a:
```

使用 mtools 工具时，你可以使用反斜杠字符（\）作为目录分隔符，正如你在 DOS 中所做的那样。但是，当你输入包含反斜杠字符的文件名时，必须用双引号（" "）将该名称包围起来。例如，下面是一个从 A 驱动器上的子目录复制文件到当前 Linux 目录的命令：

```
mcopy "a:\test\sample.dat" .
```

##### 第 4 章：安装和更新应用程序

###### 本章内容

- 使用 `rpm` 命令处理 **RPM 文件**
- 使用 `dpkg`、`dselect` 和 **APT** 处理 **DEB 文件**
- 从源文件构建应用程序
- 在线更新 Linux 应用程序

大多数为 Linux 制作的软件包都以两种特殊文件格式之一进行分发：Red Hat Package Manager (RPM) 文件或 Debian (DEB) 文件。因此，你必须知道如何安装或删除以 RPM 或 DEB 文件形式提供的软件包。幸运的是，本章将向你展示如何操作 RPM 和 DEB 文件。

![](img/11709a8f88c8cd03868a929dc94c0e2b_474_0.png)

你可以在所有 Linux 发行版中安装 RPM 和 DEB 文件，但每个发行版都有其偏好的分发格式。Fedora Core 凭借其 Red Hat Linux 的血统，倾向于使用 RPM 文件，而大多数基于 Debian 的发行版，如 Knoppix、MEPIS、Ubuntu 和 Xandros，则使用 DEB 文件来分发软件。SUSE Linux 使用 RPM 格式。

许多其他开源软件包以源代码形式提供，通常位于压缩归档文件中。你必须解包、构建并安装软件才能使用它。我将描述你在下载、构建和安装基于源代码的软件包时通常遵循的步骤。

最后，我将简要描述如何在线更新你的 Linux 系统。你会发现，每个发行版都有自己用于在线更新的工具。

###### 处理 RPM 文件

RPM 是一种将软件产品所需的所有必要文件打包到单个文件中的系统——称为 *RPM 文件*，或简称 *RPM*。实际上，整个 Fedora Core 和 SUSE 发行版就是大量的 RPM。操作 RPM 的最佳方式是通过 RPM 命令。你必须在终端窗口或文本控制台的 shell 提示符下输入这些命令。

![](img/11709a8f88c8cd03868a929dc94c0e2b_475_0.png)

在 Fedora Core 中，`rpm` 命令仅适用于你需要安装少量 `rpm` 文件的情况。要安装大量 `rpm` 文件，你应该从桌面选择“应用程序::添加/删除软件”。如果你从 CD 或 DVD 安装 `rpm` 文件，请先挂载 CD/DVD，然后输入 `system-config-packages`（如果你的 CD/DVD 挂载在其他目录，请将 `/media/cdrom` 替换为该目录名称）。这将打开一个包管理窗口，你可以从中选择并安装成组的软件包。

####### 使用 rpm 命令

当你安装基于 `rpm` 的发行版（如 Fedora Core）时，安装程序使用 `rpm` 命令解包软件包（`rpm` 文件）并将内容复制到你的硬盘上。

你不需要理解 `rpm` 文件的内部结构，但你需要了解如何使用 `rpm` 命令来操作 `rpm` 文件。以下是你可以使用 `rpm` 命令执行的一些操作：

- 查找你系统中已安装的 RPM 的版本号和其他信息。
- 从 RPM 安装新的软件包。例如，你可能需要安装初始安装时跳过的某个软件包。
- 删除（卸载）你之前从 RPM 安装的不需要的软件。如果发现你很少（或从未）使用某个软件包，你可以卸载它以回收磁盘空间。
- 用新版本升级旧版本的 RPM。例如，在 Fedora Core 中，在你从 Fedora Core 下载站点（在线列出于 `http://fedora.redhat.com/download/mirrors.html`）下载软件包的新版本后，你可能需要升级。你必须升级 RPM 才能受益于新版本中的修复。
- 验证 RPM 是否处于正常工作状态。你可以验证软件包以检查所有必要文件是否位于正确的位置。

正如你所见，`rpm` 命令功能强大——根据你使用的选项不同，它可以做很多不同的事情。

如果你忘记了 `rpm` 的选项，请输入以下命令以查看列表：

```
rpm --help | more
```

`rpm` 选项的数量会让你惊讶！





####### 了解 RPM 文件名

RPM 包含多个文件，但在你的 Fedora Core 系统上它表现为一个单一文件。按照惯例，RPM 文件名具有特定的格式。典型的 RPM 文件名看起来像这样：

openoffice.org-writer-1.9.104-2.i386.rpm

此文件名由以下部分组成，前三个部分由短横线 (-) 分隔：

- 包名称：openoffice.org-writer
- 版本号：1.9.104
- 发行版本号：2
- 架构：i386（此包适用于 Intel 80x86 或 Pentium 兼容处理器）

通常，包名称的描述性足够强，你可以据此猜测 RPM 可能包含的内容。版本号与软件包当前版本号相同（即使它是以其他形式分发的，例如 tar 文件）。开发人员分配发行版本号以跟踪变更。架构是 i386，或者你可以搜索想要在具有 Intel x86 兼容处理器的 PC 上安装的 RPM。

####### 查询 RPM

在安装软件包时，`rpm` 命令会构建一个已安装 RPM 的数据库。你可以使用 `rpm -q` 命令查询此数据库，以获取有关系统中已安装软件包的信息。

例如，要查找系统中已安装的 Linux 内核的版本号，请键入以下 `rpm -q` 命令：

```
rpm -q cups
```

你会看到类似以下的响应：

```
cups-1.1.23-15
```

响应是内核 RPM 的名称。（此版本是内核的可执行版本，而不是源文件。）该名称与 RPM 文件名相同，只是最后一部分—.i386.rpm—未显示。在这种情况下，RPM 的版本部分告诉你已安装了 cups（Common UNIX Printing System，通用 UNIX 打印系统）版本 1.1.23。

###### 处理 RPM 文件

使用以下命令可以查看所有已安装 RPM 的列表：

`rpm -qa`

你会看到一长串 RPM 列表在屏幕上滚动。若要一次查看一屏列表，请键入：

`rpm -qa | more`

如果你想搜索特定的软件包，将 `rpm -qa` 的输出提供给 `grep` 命令。例如，要查看所有名称中包含 kernel 的软件包，请键入：

`rpm -qa | grep kernel`

结果取决于系统中安装了内核 RPM 的哪些部分。

使用 `rpm -q` 命令可以查询比软件包版本号更多的信息。通过添加单字母选项，你可以获取其他有用的信息。例如，尝试以下命令以查看 cups 软件包中的文件：

`rpm -ql cups`

以下是 `rpm -q` 命令的几个其他有用形式，用于查询有关软件包的信息。（要使用这些 `rpm -q` 命令中的任何一个，请键入该命令，后跟软件包名称。）

- `rpm -qc`：列出软件包中的所有配置文件。
- `rpm -qd`：列出软件包中的所有文档文件。这些通常是在线手册页（也称为 man 页）。
- `rpm -qf`：显示指定文件所属的软件包名称（如果有）。
- `rpm -qi`：显示有关软件包的详细信息，包括版本号、大小、安装日期和简短描述。
- `rpm -ql`：列出软件包中的所有文件。对于某些软件包，你会看到非常长的列表。
- `rpm -qs`：列出软件包中所有文件的状态。（文件的状态可能是以下之一：正常、未安装或已替换。）

![](img/11709a8f88c8cd03868a929dc94c0e2b_477_0.png)

这些 rpm 命令仅提供有关已安装软件包的信息。如果你想查找有关未安装 RPM 文件的信息，请在每个命令的命令行选项后加上字母 p。例如，要查看名为 `xrist-6.1.5-792.i386.rpm` 的 RPM 文件中的文件列表，请进入该文件所在的目录并键入以下命令：

`rpm -qpl rdast-*.rpm`

当然，此命令仅在当前目录包含该 RPM 文件时才有效。

两个便捷的 `rpm -q` 命令可以让你找出哪个 RPM 文件提供特定文件，以及哪些 RPM 需要指定软件包。要找出提供某个文件的 RPM 名称，请使用以下命令：

`rpm -q --whatprovides filename`

例如，要查看哪个 RPM 提供文件 /etc/vsftpd.conf，请键入：

`rpm -q --whatprovides /etc/vsftpd.conf`

RPM 随后会打印提供该文件的软件包名称，如下所示：

vsftpd-2.0.3-1

如果你提供的是软件包名称而不是文件名，RPM 将显示包含指定软件包的 RPM 软件包的名称。

另一方面，要查找需要特定软件包的 RPM 名称，请使用以下命令：

`rpm -q -f`

例如，要查看哪些软件包需要 openssl 软件包，请键入：

`rpm -q -f openssl`

此命令的输出显示所有需要 openssl 软件包的 RPM 软件包。

####### 安装 RPM

要安装 RPM，请使用 `rpm -i` 命令。你必须提供 RPM 文件的名称作为参数。如果你想查看 RPM 安装的进度，请使用 `rpm -ivh`。随着软件包的解包，会显示一系列井号 (#)。

例如，要从配套 DVD-ROM 为 Fedora Core 安装内核-devel RPM（其中包含 Linux 操作系统的头文件），我插入 DVD，挂载后，键入以下命令：

```
cd /media/cdrom/Fedora/RPMS
rpm -ivh kernel-devel*
```

你不必键入完整的 RPM 文件名——你可以使用名称开头的几个字符后跟星号 (*)。确保你键入足够多的名称以唯一识别 RPM 文件。

如果你尝试安装一个已经安装的 RPM，`rpm -i` 命令将显示错误消息。例如，当在我系统上键入以下命令安装 man 软件包时，会发生什么：

```
rpm -i man-2*
```

我从 `rpm -i` 命令获得以下错误消息：

```
package man-2.4.1-221 is already installed
```

要强制 `rpm` 命令在存在错误的情况下安装软件包，只需在 `rpm -i` 命令中添加 `--force`，如下所示：

```
rpm -i --force man-2*
```

####### 删除 RPM

如果你意识到实际上不需要软件，你可能想要删除——卸载——该软件包。例如，如果你已安装 X Window System 开发软件包，但发现你对编写 X 应用程序不感兴趣，你可以使用 `rpm -e` 命令轻松删除该软件包。

在删除之前，你必须知道软件包的名称。查找名称的一个好方法是使用 `rpm -qa` 结合 `grep` 搜索适当的 RPM 文件。

例如，要删除名为 `qt3-devel` 的软件包，请键入：

```
rpm -e qt3-devel
```

删除 RPM 时，你不需要完整的 RPM 文件名；你只需要软件包名称——即文件名中版本号前短横线 (-) 之前的第一部分。

`rpm -e` 命令不会删除其他软件包所需的软件包。

####### 升级 RPM

使用 `rpm -U` 命令升级 RPM。你必须提供包含新软件的 RPM 文件的名称。例如，如果我的系统上安装了 `cups`（打印系统）版本 1.1.20，但我想要升级到版本 1.1.23，我从存储库下载 RPM 文件 `cups-1.1.23-i5.1386.rpm` 并使用以下命令：

```
rpm -U cups-1.1.23-i5.1386.rpm
```

`rpm` 命令通过删除 `cups` 软件包的旧版本并安装新的 RPM 来执行升级。

只要可能，请升级而不是删除旧软件包并安装新软件包。升级会自动保存你的旧配置文件，从而省去在新安装后重新配置软件的麻烦。

当你升级包含即运 Linux 内核的 `kernel` 软件包时，请使用 `rpm -i` 命令（而不是 `rpm -U` 命令）进行安装。这样，你就不会覆盖当前内核。

####### 验证 RPM

你可能不经常这样做，但如果你怀疑软件包未正确安装，请使用 `rpm -V` 命令进行验证。例如，要验证内核软件包，请键入以下内容：

```
rpm -V kernel
```

此命令使 `rpm` 将软件包中每个文件的大小和其他属性与原始文件进行比较。如果一切验证正确，`rpm -V` 命令不会打印任何内容。如果发现任何差异，你会看到一份报告。例如，我修改了 Apache `httpd` Web 服务器的配置文件。以下是我验证 `httpd` 软件包时键入的内容：

```
rpm -V httpd
```

以下是我得到的结果：

```
S,5....T c /etc/httpd/conf/httpd.conf
```

在这种情况下，`rpm -V` 的输出告诉我配置文件已更改。此命令输出的每一行由三部分组成：

- 行以八个字符开头：每个字符表示找到的差异类型。例如，S 表示大小不同，T 表示最后修改时间不同。表 4-1 显示了每个字符及其含义。句点表示该特定属性与原始属性匹配。
- 对于配置文件，会出现一个 c；否则，此字段为空。这就是你如何判断文件是否为配置文件的方法。通常，如果配置文件已更改，你不必担心；你自己可能进行了更改。
- 行的最后一部分是文件的完整路径名。从这部分，你可以确切知道文件的位置。





####### 表 4-1 RPM 验证报告中使用的字符

| 字符 | 含义 |
| :--- | :--- |
| S | 文件大小已变更 |
| M | 权限和文件类型不同 |
| 5 | 使用 MD5 算法计算的校验和不同 |
| D | 设备类型不同 |
| L | 符号链接不同 |
| U | 文件属主不同 |
| G | 文件属组不同 |
| T | 文件修改时间不同 |

###### 处理 DEB 文件

带有 `.deb` 文件扩展名的 Debian 软件包将可执行文件与配置文件、在线文档和其他信息存储在一起。你可以使用 Debian 实用工具 `dpkg` 来解包和操作这些 DEB 文件，这是一个接受许多选项的命令行程序。还有一种名为 dselect 的文本模式菜单驱动程序，可供你管理软件包，而无需输入 `dpkg` 命令。

你通常使用一种名为 APT（高级打包工具，Advanced Packaging Tool）的高级实用工具来处理 Debian 中的软件包。例如，与其下载 DEB 文件并使用 `dpkg` 命令安装，你只需使用 `apt-get` 命令即可安装软件包。`apt-get` 命令甚至可以在线下载软件包并从 Debian 存储库安装到你的系统。当你想要查看从存储库手动下载的 DEB 文件，或可能位于 APT 缓存目录（Debian 中为 `/var/cache/apt/archives`）中的 DEB 文件内容时，`dpkg` 命令仍然很有用。

![](img/11709a8f88c8cd03868a929dc94c0e2b_481_0.png)

我将在以下部分向你介绍 `dpkg`、`dselect` 和 APT。

####### 理解 DEB 文件名

典型的 DEB 软件包文件名采用以下格式：

```
mozilla-firefox_1.0.2-1_i386.deb
```

文件名由下划线 (_) 分隔的三部分组成：

- **软件包名称：** `mozilla-firefox`
- **版本号和修订号：** `1.0.4-2`（版本由连字符分隔的两部分组成。第一部分是软件包维护者的版本号；第二部分是 Debian 修订号。）
- **架构：** `i386.`（该软件包适用于 Intel x86 兼容系统。）

文件名具有 `.deb` 扩展名，表明这是一个 DEB 文件。

####### 使用 `dpkg` 命令

为了熟悉 `dpkg` 命令，请输入 `dpkg -help | more`。输出显示了 `dpkg` 接受的众多选项。你也可以输入 `man dpkg` 来阅读 `dpkg` 的在线 man 页。

你可以使用 `dpkg` 对软件包执行大量操作，但你必须在终端窗口或文本控制台的 shell 提示符下操作。`dpkg` 命令的格式为

```
dpkg [options] action package
```

包含零个或多个 `options`、指示 `dpkg` 需要执行的 `action`，以及 `package`、DEB 文件或目录的名称（取决于 `action` 参数）。有时 `dpkg` 命令不需要任何软件包或文件名称，只需要一个 `action`。

以下是你可以使用 `dpkg` 执行的一些操作示例：

- 使用命令 `dpkg -i` `packagefile` 从 DEB 文件**安装**软件包，其中 `packagefile` 是 DEB 文件的名称（例如，`vsftpd-*.deb`）。
- 使用命令 `dpkg -r` `packagename` **移除**软件包但保留配置文件，其中 `packagename` 是软件包的名称（例如，`vsftpd`）
- 使用命令 `dpkg --configure` `packagename` **配置**软件包，其中 `packagename` 是软件包的名称（例如，`vsftpd`）
- **清除**（删除包括配置文件在内的所有内容）使用命令 `dpkg -P` `packagename`，其中 `packagename` 是软件包的名称（例如，`vsftpd`）
- 使用命令 `dpkg -C` **审计**软件包（并找到系统中部分安装的软件包）（不需要文件名或软件包名称）
- 使用命令 `dpkg -c packagefile` 列出 DEB 文件的**内容**，其中 `packagefile` 是 DEB 文件的名称（例如，`vsftpd-*.deb`）
- 使用命令 `dpkg -I packagefile` **查看**关于 DEB 文件的信息，其中 `packagefile` 是 DEB 文件的名称（例如，`vsftpd-*.deb`）
- 使用命令 `dpkg -l pattern` **列出匹配模式的软件包**，其中 `pattern` 是你想要匹配的软件包名称模式——通常带有通配符——（例如，`kernel*`）
- 使用命令 `dpkg -S pattern` **查找包含文件的软件包**，其中 `pattern` 是软件包包含的文件名模式——通常带有通配符——（例如，`stdio*`）
- 使用命令 `dpkg -L package` **列出从软件包安装的文件**，其中 `package` 是软件包的名称（例如，`vsftpd`）

你可以在 Debian 系统或使用 DEB 软件包的系统中尝试这些命令。例如，要查找所有名称以 *mozilla* 开头的软件包，请在终端窗口中输入 `dpkg -l mozilla*`。以下是我 Debian 系统上该命令输出的相关部分：

```
||/ Name            Version               Description
***===========================================================***
un  mozilla         <none>              (no description available)
un  mozilla-bonobo  <none>              (no description available)
ii  mozilla-browser 1.7.4-1            The Mozilla Internet application suite - core
ii  mozilla-firefox 1.0.4-2            lightweight web browser based on Mozilla
```

第一列中的 `ii` 表示软件包已安装；`un` 表示软件包未安装。

`dpkg -l` 的另一种常见用法是列出所有软件包，并使用 `grep` 查找匹配搜索字符串的行。例如，要查找包含 *kernel* 的任何内容，请输入 `dpkg -l | grep kernel`。如果软件包名称（`dpkg -l` 输出的第二列）被截断，请使用类似这样的命令调整输出行的宽度：

```
COLUMNS=132 dpkg -l | grep kernel
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_483_0.png)

我发现 `dpkg -S` 命令是定位系统中哪个软件包提供了特定文件的一种方便方法。例如，如果我想弄清楚哪个软件包包含 `/etc/host.conf` 文件，我会输入 `dpkg -S /etc/host.conf`，输出显示 `base-files` 软件包包含 `/etc/host.conf`：

```
base-files: /etc/host.conf
```

###### 介绍 dselect

`dselect` 旨在作为 `dpkg` 工具的前端。要试用 `dselect`，请以 **root** 身份登录并在终端窗口（或文本控制台）中输入 `dselect`。当 `dselect` 启动时，你会得到 `dselect` 的文本模式菜单（如图 4-1 所示）。

![](img/11709a8f88c8cd03868a929dc94c0e2b_484_0.png)

**图 4-1：** 你可以使用 `dselect` 来管理 Debian 中的软件包。

我不会详细描述 `dselect`，但以下是你可以从 `dselect` 主菜单执行的一些任务：

- 指定访问方法——如何查找 DEB 软件包
- 更新可用软件包列表
- 查看已安装和可用软件包的状态
- 选择软件包并管理软件包之间的依赖关系
- 安装新软件包或将现有软件包升级到较新版本
- 配置尚未配置的软件包
- 移除软件包

`dselect` 中常见的一个序列是更新可用软件包列表，然后升级所有有可用更新的软件包。当然，你也可以使用简单的 APT 命令执行相同的任务。

###### 使用 APT 管理 DEB 软件包

APT 确实是一个用于保持 Debian 系统最新的先进工具。你可以使用多种 APT 工具来管理 DEB 软件包。两个常用的命令是 `apt-get` 和 `apt-cache`。

# 460 处理 DEB 文件

要使用 `apt-get` 安装软件包，只需输入 `apt-get install packagename`，其中 `packagename` 是你想要安装的软件包的名称。例如，要安装 `vftpd` 软件包，请输入 `apt-get install vftpd`。

移除软件包同样简单。输入 `apt-get remove packagename`，其中 `packagename` 是你想要移除的软件包的名称。

如果你想知道软件包的名称，并且知道与该软件包相关的一些术语，你可以使用 `apt-cache` 工具查找它。例如，要查找 CD/DVD 刻录软件包，我会输入 `apt-cache search burn | more` 来搜索 APT 的软件包缓存（这是 APT 从 `/etc/apt/sources.list` 文件中列出的服务器下载的 Debian 软件包列表）。以下是该命令的一些输出行：

- arson - KDE frontend for burning CDs
- burn - Command line Data-CD, Audio-CD, ISO-CD, Copy-CD writing tool
- caca-utils - text mode graphics utilities
- cdcontrol - A parallel burner that allow you to write to one or more CD-Writers at once
- cdlabelgen - generates front cards and tray cards for CDs and DVDs
- cdrecord - Tcl/Tk frontend for burning cdrom
- cdw - Tool for burning CD’s - console version
- cdc-comman - Tool for burning CD’s - common files
- cpuburn - a collection of programs to put heavy load on CPU
- ccrun - Chez Man CD Ripper
- dvd-rw-tools - DVD+-RW/R tools
- dvdbackup - tool to rip DVD’s from the command line
- ednamath.app - Scientific calculator for GNUstep
- gcd - Tool for burning CD’s - graphical version
- gcombust - GTK+ based CD mastering and burning program
- ... lines deleted ...

输出显示了我可以安装的几个潜在的 CD/DVD 刻录程序。要了解有关任何软件包的更多信息，我会输入 `apt-cache show packagename`，其中 `packagename` 是我想要信息的软件包的名称。例如，要了解有关 `dvd-rw-tools` 软件包的更多详细信息，我会输入 `apt-cache show dvd-rw-tools`，输出将向我显示该软件包的描述。然后我可以使用 `apt-get install` 安装该软件包。

![](img/11709a8f88c8cd03868a929dc94c0e2b_485_0.png)

要搜索仅出现在软件包名称中的关键字，请使用 `--names-only` 选项，如下所示：`apt-cache search --names-only keyword`，其中 `keyword` 是出现在软件包名称中的内容。例如，如果我想要查找名称中包含 `selinux` 的软件包，我会输入 `apt-cache search --names-only selinux`。




定期运行 `apt-get clean` 命令，以清理本地存储库（位于 `/var/cache/apt/archives` 目录）中已安装的 DEB 文件。通过删除这些 DEB 文件，您可以释放一些磁盘空间。

###### 从源文件构建软件包

许多开源软件包以源代码形式分发，不包含可执行二进制文件。在使用此类软件之前，必须通过编译来构建可执行二进制文件，并且您还必须遵循某些说明来安装该软件包。在本节中，我将展示如何从源文件构建软件包。

####### 下载和解包软件

通常，开源软件的源文件以压缩的 `tar` 归档形式分发。这些归档由 `tar` 程序创建，并使用 `gzip` 程序进行压缩。分发的形式是一个大型单文件，扩展名为 `.tar.gz` 或 `.tar.z` — 通常被称为 *压缩的 tarball*。如果您想要该软件，必须下载压缩的 tarball 并将其解包。

使用匿名 FTP 或通过 Web 浏览器下载压缩的 `tar` 文件。通常，除了点击链接并将文件保存到系统上的适当目录外，该过程不需要您做任何努力。

如果您想尝试下载和构建软件包，可以以 X 多媒体系统 (XMMS) 进行练习 — 这是一个用于播放 MP3 和其他多媒体文件的图形 X 应用程序。XMMS 包含在 Fedora Core 中，并且已经安装在您的系统上。但是，再次下载和重新构建 XMMS 软件包不会造成任何伤害。

从 `www.xmms.org/download.php` 下载 XMMS 的源文件。这些文件以压缩的 tar 归档形式打包。点击源文件的 `http` 链接，并将它们保存在 Linux 系统的 `/usr/local/src` 目录中。（请确保以 `root` 用户身份登录；否则无法保存到 `/usr/local/src` 目录。）

下载压缩的 tar 文件后，使用以下 `tar` 命令查看其内容：

```
tar ztf xmms*.gz | more
```

您将看到类似于以下内容的列表：

```
xmms-1.2.10/
xmms-1.2.10/intl/
xmms-1.2.10/intl/ChangeLog
xmms-1.2.10/intl/Makefile.in
xmms-1.2.10/intl/config.charset
xmms-1.2.10/intl/locale.alias
xmms-1.2.10/intl/ref-add.sin
xmms-1.2.10/intl/ref-del.sin
xmms-1.2.10/intl/gmo.h
xmms-1.2.10/intl/gettext.h
xmms-1.2.10/intl/hash-string.h
xmms-1.2.10/intl/loadinfo.h
... lines deleted ...
```

此 `tar` 命令的输出显示了归档中包含的内容，并让您了解解包归档后创建的目录。在这种情况下，会在当前目录（在我的案例中是 `/usr/local/src`）中创建一个名为 `xmms-1.2.10` 的目录。从列表中，您还可以推断出用于编写该包的语言。如果您看到 `.c` 和 `.h` 文件，那么源文件是采用 C 编程语言编写的，许多开源软件包都使用这种语言。

要提取压缩的 `tar` 归档的内容，请输入以下 `tar` 命令：

```
tar zrvf xmms*.gz
```

您会再次看到这些文件从归档中提取并复制到硬盘上的适当目录时的长列表。

现在您可以准备构建软件了。

####### 从源文件构建软件

解包压缩的 `tar` 归档后，所有源文件都位于一个目录中，该目录的名称通常是软件包名称加上版本号后缀。例如，XMMS 1.2.10 版本的源文件会提取到 `xmms-1.2.10` 目录中。要开始构建软件，请使用以下命令更改目录：

```
cd xmms*
```

您无需输入完整的名称 — shell 可以展开目录名称并切换到 `xmms-1.2.10` 目录。

几乎所有的软件包都附带某种 **_README_** 或 **_INSTALL_** 文件 — 一个告诉您如何构建和安装包的文本文本文件。XMMS 也不例外；它附带了一个 **_README_** 文件，您可以输入 **more README** 来浏览。一个 **_INSTALL_** 文件包含构建和安装 XMMS 的说明。

![](img/11709a8f88c8cd03868a929dc94c0e2b_488_0.png)

大多数开源软件包，包括 XMMS，还附带一个名为 **COPYING** 的文件。该文件包含 *GNU 通用公共许可证* (GPL) 的全文，其中阐明了您可以使用和重新分发软件的条件。如果不熟悉 GNU GPL，请阅读此文件，并将许可证出示给您的法律顾问，以获取完整解释和对其业务适用性的评估。

要构建软件包，请遵循 **_README_** 或 **_INSTALL_** 文件中的说明。对于 XMMS 包，**_README_** 文件列出了一些先决条件（如库），并告诉您要输入哪些命令来构建和安装包。就 XMMS 而言，说明告诉您使用以下步骤：

- 1. 输入 **_./configure_** 以运行 shell 脚本，该脚本检查您的系统配置并创建一个名为 **Makefile** 的文件 — 一个由 **make** 命令用于构建和安装包的文件。（您可以输入 **_./configure --help_** 来查看 **_configure_** 接受的一组选项。）
    - 如果遇到关于缺少包的任何错误，您必须安装这些缺失的包。使用您的发行版的软件安装工具来添加缺失的包。例如，在 Debian 中使用 **_apt-get install_** 命令。在 Fedora Core 中，选择 **应用程序 > 添加/移除软件**。在 SUSE 中，使用 YaST GUI 工具。
- 2. 输入 **make** 来构建软件。
    - 此步骤编译所有子目录中的源文件。（编译源代码将每个源文件转换为一个 *目标文件* — 一个包含您的 PC 处理器可以理解的二进制指令的文件。）
- 3. 输入 **make install** 来安装软件。
    - 此步骤将库和可执行二进制文件复制到系统上的适当目录。

虽然这些步骤是针对 XMMS 的，但大多数其他包都遵循这些步骤 — **_configure_**、**_make_** 和 **_install_**。**_configure_** shell 脚本会推测系统相关的变量，并创建一个包含构建和安装软件所需命令的 **Makefile**。

![](img/11709a8f88c8cd03868a929dc94c0e2b_489_0.png)

通常，除了输入构建软件的命令外，您不需要做任何事情，但您必须在系统上安装软件开发工具。在 Fedora Core 中，您必须安装开发工具和 GNOME 软件开发包。在 Debian 中，要构建和运行 XMMS，您还必须安装 X 软件开发包，因为它是一个 X 应用程序。

安装 XMMS 后，尝试在终端窗口中输入 **xmms**，从 GNOME 或 KDE 桌面运行它。在 XMMS 窗口中，按 L 键以获取加载文件对话框。选择一个 MP3 文件进行播放。您的 PC 必须有声卡，并且声卡必须配置正确，XMMS 才能正常工作。

总而言之，这里是下载、解包、构建和安装典型软件包所遵循步骤的概述：

- 1. 使用 Web 浏览器从匿名 FTP 站点或网站下载源代码，通常形式为 .tar.gz 文件。
- 2. 使用 `tar zxvf filename` 命令解包文件。（如果压缩的 tar 文件具有 .bz2 扩展名，这意味着该文件是用 bzip2 压缩的，您可以使用 `tar jxvf filename` 命令解包该文件。）
- 3. 将目录更改到软件解包后的新子目录，使用诸如 `cd software_dir` 这样的命令。
- 4. 阅读任何 README 或 INSTALL 文件，了解构建和安装软件时必须遵循的特定说明。
- 5. 构建软件的细节可能因软件包而异，但通常您输入以下命令来构建和安装软件：

```
./configure
make
make install
```

- 6. 阅读随软件提供的其他任何文档，以了解如何使用该软件以及在使用之前是否必须进一步配置软件。

####### 安装 SRPM

![](img/11709a8f88c8cd03868a929dc94c0e2b_489_1.png)

如果您拥有 Fedora Core 的源光盘（您可以从 `http://fedora.redhat.com/download/mirrors.html` 列出的站点之一下载源 CD 镜像），您可以安装源文件并直接从源文件构建各种应用程序。Fedora Core 源代码 RPM 文件通常被称为 SRPM（source RPMs 的缩写）。




###### 在线更新 Linux 应用程序

若要安装特定的源 RPM 并构建应用程序，请按照以下步骤操作：

1.  **通过键入 `mount /media/cdrom` 来挂载 DVD-ROM，或者等待 GNOME 桌面自动挂载 DVD。**
2.  **通常，源 RPM 位于 SRPMS 目录中。请键入以下命令切换到该目录：**
    ```
    cd /media/cdrom/SRPMS
    ```
3.  **使用 `rpm -i` 命令安装源 RPM 文件。例如，要安装 Web 服务器（httpd）源，请键入：**
    ```
    rpm -ivh httpd*.src.rpm
    ```
4.  **使用 spec 文件和 `rpmbuild` 命令来构建软件。**
    通过使用 `rpmbuild` 命令的不同选项，你可以执行不同的任务，从解包源文件到构建和安装二进制文件。例如，要处理整个 spec 文件，请键入：
    ```
    rpmbuild -ba packagename.spec
    ```

文件将安装在 `/usr/src/redhat/SOURCES` 目录中。带有 _.spec 扩展名的 spec 文件会被放置在 `/usr/src/redhat/SPECS` 目录中。spec 文件描述了软件，并包含用于构建和安装软件的信息。

此处的 `packagename` 是 SRPM 的名称。该命令通常用于构建软件并安装二进制文件。

###### 在线更新 Linux 应用程序

每个 Linux 发行版——Debian、Fedora Core、MEPIS、SUSE、Ubuntu 和 Xandros——都附带了允许你在线更新软件的实用工具。在接下来的部分中，我将概述 Debian、Fedora Core、MEPIS、SUSE、Ubuntu 和 Xandros 中的更新方法。

![](img/11709a8f88c8cd03868a929dc94c0e2b_490_0.png)

你需要一个快速的互联网连接（例如 DSL 或电缆调制解调器），以便轻松地更新你的 Linux 应用程序或下载新的软件包。在尝试在线更新你的 Linux 系统之前，请确保你的互联网连接已正常运行。

####### 使用 APT 保持 Debian、MEPIS 和 Ubuntu 更新

![](img/11709a8f88c8cd03868a929dc94c0e2b_490_1.png)

保持你的 Debian 系统更新的最佳方法是使用 APT。更具体地说，你需要使用带有适当选项的 `apt-get` 命令行实用工具。由于 MEPIS 和 Ubuntu 是基于 Debian 的，你也可以使用 APT 来更新 MEPIS 和 Ubuntu。

简而言之，假设在 Debian 安装期间已配置了 APT 源，你可以按以下顺序键入以下两个命令，来保持当前软件集合的更新：

```
apt-get update
apt-get upgrade
```

`apt-get update` 命令将当前的软件包列表与 `/etc/apt/sources.list` 文件中指定的位置提供的软件包进行对照检查，并收集已安装软件包新版本的信息。

`apt-get upgrade` 命令实际上会安装你的 Debian 系统中已安装的软件包的可用新版本。你必须执行 `apt-get upgrade` 来安装任何可用的升级。

![](img/11709a8f88c8cd03868a929dc94c0e2b_491_0.png)

要在 Debian 中安装新软件包，请使用 `apt-cache search` 在 APT 的软件包缓存中查找软件包名称，然后使用 `apt-get install` 安装该软件包。

####### 更新 Fedora Core 应用程序

![](img/11709a8f88c8cd03868a929dc94c0e2b_491_1.png)

Fedora Core 自带 Up2date——一个图形化更新代理，它可以下载你的系统所需的任何新 RPM 文件并为你安装这些文件。Up2date 也被称为 Red Hat 更新代理，因为 Red Hat 为 Red Hat Network 开发了它，Red Hat 通过该网络为其商业客户提供服务。

若要使用 Up2date 更新 Fedora Core 软件包，请遵循以下步骤：

1. **以 root 身份登录，并选择 应用程序 -> 系统工具 -> Red Hat Network。** 你也可以在终端窗口中键入 `up2date`。

   （如果在菜单中看不到 Red Hat Network，或者键入 `up2date` 时出现错误，请以 `root` 身份登录，在终端窗口中键入 `yum install up2*`，然后在菜单中查找它。）更新代理将启动，如果你是第一次使用 Up2date，Red Hat Network 配置对话框将出现并引导你完成配置步骤。通常，你可以点击**确定**接受默认设置。然后另一个对话框会提示你在你的 GPG 密钥环中安装一个公钥。（GPG 指 GNU 隐私守卫或 GnuPG，一个使用 OpenPGP 互联网标准对电子邮件和其他数据进行加密、解密和签名的程序。）GnuPG 验证软件包开发者已安全地签署了 Up2date 下载的软件包。如果提示这样做，点击**是**以安装公钥。

2. **Up2date 显示一个带有欢迎消息的窗口。点击“下一步”按钮继续。**

3. Up2date 显示一个它称为“通道”的列表——这些是代理下载软件包头信息的仓库。点击“下一步”继续。

默认情况下，Up2date 代理使用一个可与 Yum 一起工作的通道——我在下一节中描述的命令行软件包更新器/安装器。这些通道在文本配置文件 `/etc/sysconfig/rhn/sources` 中识别。除了 Yum，Up2date 还可以访问专为 Debian 使用的 APT（高级打包工具）设计的仓库。

点击“下一步”后，Up2date 会确定需要更新的内容，并从指定通道获取所有头信息的列表。

4. Up2date 下载头信息后，它会显示软件包列表。你可以滚动查看列表并选择要更新的软件包；点击软件包名称左侧的复选框以选择它。

   点击“下一步”继续。

   然后 Up2date 会检查任何软件包依赖项并开始下载软件包。进度条显示下载状态。

5. 下载完成后，点击“下一步”按钮以继续进行安装。

6. Up2date 在安装每个软件包更新时显示进度条。安装完成后，点击“下一步”按钮。

   Up2date 会显示关于成功安装的软件包的消息。

7. 点击“完成”按钮退出 Up2date。

![](img/11709a8f88c8cd03868a929dc94c0e2b_492_0.png)

Fedora Core 5 还附带另一个名为“软件包更新器”（Package Updater）的图形实用工具，你可以使用它来更新安装在你的 Fedora Core 系统上的软件包。若要启动软件包更新器，请选择 应用程序 → 系统工具 → 软件更新器，或者在终端窗口中键入 `su -` 成为 root，然后键入 `pup`。

在 Fedora Core 中，你还可以使用 Yum（顺便说一句，这是 Yellow dog Updater, Modified 的缩写）。Yum 是一个用于更新以及安装和移除 RPM 软件包的命令行实用工具。Yum 从指定的网站下载 RPM 软件包头，并使用 `rpm` 实用工具来确定软件包之间的相互依赖项以及需要在你的系统上安装的内容。然后它下载并使用 `rpm` 安装必要的软件包。Yum 仅下载头信息来完成其工作，而头信息的尺寸远小于完整的 RPM 软件包。Yum 比手动使用 `rpm` 命令下载完整 RPM 软件包的替代方法快得多。

通常，由于图形化更新代理易于使用，你可以通过它来保持系统最新。然而，知道如何从命令行运行 Yum 总是好的，以防更新代理出现问题。

![](img/11709a8f88c8cd03868a929dc94c0e2b_493_0.png)

你可以访问 `http://linux.duke.edu/projects/yum` 处的 Yum 网页，阅读更多关于 Yum 的内容并了解 Yum 的新闻。

Yum 的命令行具有如下语法：

```
yum [options] command [pakages]
```

*options* 是 Yum 选项列表，*command* 指定你希望 Yum 执行的操作，而 *pakages* 是 Yum 执行该操作的软件包名称。你必须提供 *command*，但 *options* 和 *pakages* 是可选的。这就是为什么我在语法中用方括号表示它们。表 4-2 总结了 Yum 命令，表 4-3 列出了一些常见的 Yum 选项。

**表 4-2：Yum 命令**

| 命令 | 此命令对 Yum 的作用 |
| :--- | :--- |
| check-update | 检查你的系统可用的更新 |
| clean | 清理缓存目录 |
| info | 显示指定软件包的摘要信息 |
| install | 安装指定软件包的最新版本，确保满足所有依赖项 |
| list | 列出可用软件包的信息 |
| provides | 提供有关哪个软件包提供某个文件的信息 |
| remove | 移除指定软件包以及依赖于被移除软件包的任何软件包 |
| search | 查找头部包含你指定软件包名称的软件包 |
| update | 更新指定软件包，确保满足所有依赖项 |

**表 4-3：一些常见的 Yum 选项**

| 选项 | 使 Yum 执行以下操作 |
| :--- | :--- |
| --download-only | 下载软件包，但不安装它们 |
| --exclude=pkgname | 排除指定软件包。（你可以在命令行上多次使用此选项。） |
| --help | 显示帮助消息并退出 |
| --installroot=path | 使用指定的路径名作为安装所有软件包的目录 |
| -y | 假设你对任何问题的回答都是 yes |





###### 在线更新 Linux 应用程序

如果你只是想使用 Yum 来更新系统，只需输入以下命令。（你必须以 *root* 身份登录。）

```
yum update
```

Yum 会查阅其配置文件 `/etc/yum.conf`，并执行更新系统上已安装软件包所需的所有操作。

你可以指定软件包名称来仅更新部分软件包。例如，若要更新内核（kernel）和 xorg-x11 软件包，请使用以下 Yum 命令：

```
yum update kernel* xorg-x11*
```

此命令将更新所有名称以 kernel 和 xorg-x11 开头的软件包。

你可以使用选项进一步指示 Yum 如何操作。例如，如果你想下载更新后的软件包但不安装它们，请输入：

```
yum --downloadonly update
```

另一个典型的选项是 `--exclude`，它允许你在更新过程中排除一个或多个软件包。假设你想更新除 GNOME 软件包（其名称以 gnome 开头）和 Rhythmbox 软件包以外的所有内容。那么请输入以下 Yum 命令：

```
yum --exclude=gnome* --exclude=rhythmbox update
```

####### 在线更新 SUSE

SUSE 附带了 YOU —— YaST Online Update（YaST 在线更新），用于在线软件更新。要访问 YOU，请选择主菜单 > 系统 > YaST，然后在 YaST 控制中心的软件类别中，单击在线更新。这将打开 YaST Online Update 窗口，如图 4-2 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_494_0.png)

若要配置 YOU 自动更新，请单击“配置完全自动更新”按钮。然后，你可以指定一天中的某个时间，让 YOU 下载任何可用的补丁并安装它们。如果你愿意，你可以指定 YOU 仅下载补丁而不安装。

要在线更新你的 SUSE 系统，请选择安装源并单击“下一步”。（见图 4-2。）然后，YOU 将下载补丁列表并显示出来，如图 4-3 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_495_0.png)
图 4-2：你可以使用 YaST Online Update 保持 SUSE 系统更新。

![](img/11709a8f88c8cd03868a929dc94c0e2b_495_1.png)
图 4-3：选择 YOU 补丁并单击“接受”以安装它们。

选择补丁（其中一些是推荐项，并已为你预选），然后单击“接受”。接着，YOU 将下载所需的软件包并将它们安装到你的 SUSE 系统上。

####### 使用 Xandros Networks

在 Xandros 中，使用 Xandros Networks 来更新应用程序或安装新的应用程序。选择主菜单 > Xandros Networks（或双击桌面上的 Xandros Networks 图标）以打开 Xandros Networks 窗口，如图 4-4 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_496_0.png)

要安装来自 Xandros 的最新更新，请选择文件 > 安装所有来自 Xandros 的最新更新，或单击“更新”按钮（位于图 4-4 顶部工具栏中键的左侧）。然后，Xandros Networks 将下载有关可用更新的信息，并显示要下载的软件包及安装它们所需的磁盘空间摘要（见图 4-5）。

![](img/11709a8f88c8cd03868a929dc94c0e2b_496_1.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_497_0.png)

单击确定。Xandros Networks 会提示你输入 root 密码，在你输入 root 密码后，它将下载软件更新并安装。

在幕后，Xandros Networks 使用 Debian 的 `apt-get` 命令来下载和安装软件更新。

![](img/11709a8f88c8cd03868a929dc94c0e2b_497_1.png)

Xandros Networks 窗口还提供安装新软件的选项。你甚至可以通过 Xandros Networks 选购新应用程序。如果你有要安装的 RPM 或 DEB 文件，可以在 Xandros Networks 中选择文件 > 安装 RPM 文件或文件 > 安装 DEB 文件来进行安装。

##### 第 5 章：定制 Linux 内核

###### 本章内容

- 配置内核
- 构建新内核及任何模块
- 安装模块
- 构建并安装新的初始 RAM 磁盘文件
- 安装内核并设置 GRUB

Linux 令人兴奋的其中一个原因是许多程序员一直在不断改进它。例如，一些程序员编写驱动程序以增加对新硬件的支持，如新的声卡或新的网卡。所有这些创新都以 Linux 内核新版本的形式的形式呈现给你。

尽管你不需要在每个新版本可用时都升级或修改 Linux 操作系统——内核——但有时你必须升级，仅仅因为新版本修复了一些问题或更好地支持你的硬件。另一方面，如果较早的内核版本已包含你需要的一切，你就不必急着去升级。

有时，即使没有修复或增强，你也可能希望重新构建内核。随附 DVD-ROM 上的 Linux 内核是通用的，使用模块来支持所有类型的硬件。你可能希望构建一个新的内核，该内核将——整合到内核的二进制文件中——仅包含你系统上安装的设备驱动程序。特别是，如果你有一个 SCSI 硬盘，你可能希望创建一个支持你的 SCSI 适配器的内核。根据你的需求，你还可能希望更改某些内核配置选项，例如创建一个针对你的处理器（而不是通用的 Intel 386 处理器）特定的内核。

在本章中，我将解释如何重新构建并安装新的 Linux 内核。

###### 重新构建内核

*重新构建内核* 指的是为 Linux 核心操作系统创建一个新的二进制文件。这个二进制文件是 Linux 启动时运行的那个文件。

你可能会问为什么想要重新构建内核。好吧，以下是几个原因：

- 在安装 Linux 后，你可能希望创建一个新的内核，该内核仅包含支持你系统上安装的硬件的功能。特别是，如果你有一个 SCSI 适配器，你可能希望创建一个链接 SCSI 驱动程序的内核。随附 DVD-ROM 上的内核将 SCSI 驱动程序包含为内核在启动时加载的外部模块。
- 如果你的系统拥有仅提供实验性支持的硬件，你必须重新构建内核以将该支持整合到操作系统中。
- 你可能希望重新编译内核，并生成在你的特定 Pentium 处理器上运行良好的代码（而不是大多数 Linux 发行版中自带的通用 386 处理器代码）。

要重新构建 Linux 内核，你需要内核源文件。通常不安装内核源文件。使用你的发行版的软件安装工具来安装内核源软件包。

Fedora Core 不提供 *kernel-source* 软件包。相反，你必须安装源 RPM (SRPM) 文件 *kernel-version.src.rpm*，其中 *version* 是内核版本编号。你可以在 Fedora Core 在线存储库的 SRPMS 目录中找到内核 SRPM。你必须使用命令 `rpm -Uvh kernel-version.src.rpm` 安装内核 SRPM。然后输入 `cd /usr/src/redhat/SPECS`，接着输入 `rpmbuild -bp --target $arch kernel.spec`。要在 `/usr/src/linux` 目录中使内核源可用，请输入以下命令。（将 *version* 替换为你可以通过 `uname -r` 命令获取的内核版本号。）

```
cd /usr/src/redhat/BUILD/kernel-VERSION/usr/src/
mv linux-VERSION /usr/src/
cd /usr/src/
ln -s ./linux-VERSION linux
```

在 SUSE 中，使用 YaST 的软件管理工具来安装内核源——要找到它，请使用 YaST 软件安装窗口中的搜索功能（搜索 *kernel-source*）。安装 kernel-source 软件包后，源文件将出现在 `/usr/src/linux-version` 目录中，其中 *version* 是内核的版本编号。因此，对于内核版本 2.6.13，源文件位于 `/usr/src/linux-2.6.13` 目录中。某些发行版会自动将 `/usr/src/linux` 设置为指向包含 Linux 内核源文件的特定版本目录的符号链接（快捷方式）。





## 重建内核

![](img/11709a8f88c8cd03868a929dc94c0e2b_500_0.png)

在基于 Debian 的发行版中，内核源代码安装在 `/usr/src/kernel-source-version` 目录中，其中 version 代表内核版本。因此，对于内核版本 2.6.11，源代码位于 `/usr/src/kernel-source-2.6.11`。要在 Debian 中切换到内核源代码目录，请输入 `cd /usr/src/kernel-source*`。

构建内核涉及以下步骤：

- 配置内核
- 构建内核
- 构建并安装模块
- 创建新的初始 RAM 磁盘 (initrd) 文件
- 安装内核并设置 GRUB

我将在接下来的几节中解释这些步骤，但首先你需要了解将驱动链接到内核与将驱动构建为可加载模块之间的区别。

####### 创建单片内核与模块内核

在 Linux 中支持各种硬件设备所需的设备驱动，你有两个选择：

1.  **链接支持：**你可以将系统中所有硬件的驱动直接链接到内核中。随着设备驱动代码被整合进内核，内核的大小会增加。将所有必要代码链接在一起的内核被称为*单片内核*，因为它是一个大文件。
2.  **使用模块：**你可以以可加载内核模块的形式创建设备驱动。*模块*是内核在启动运行后加载的一块代码。模块的典型用途是为新设备添加支持，而无需为每个新设备重新构建内核。模块不一定是设备驱动，它们还可以为内核添加新的功能。使用模块的内核被称为*模块内核*。

你不必创建完全的单片内核或完全的模块内核。实际上，将部分支持直接链接到内核，同时将不常用的设备驱动构建为模块，是一种常见做法。对于 Linux 发行版来说，包含一个主要基于模块的内核是合理的，此外还附带大量模块以支持许多不同类型的硬件。然后，Linux 安装程序会配置系统，使其仅加载支持用户系统中已安装硬件所需的模块。

![](img/11709a8f88c8cd03868a929dc94c0e2b_501_0.png)

当你为你的硬件配置创建定制内核时，你可能希望将所有必需的设备驱动链接到内核中。你仍然可以控制这种单片内核的大小，因为你只链接系统上已安装的特定硬件集的设备驱动。

####### 配置内核

重建内核的第一步是配置它。要配置内核，请以 `root` 身份登录。然后使用 `cd` 命令切换内核源代码目录，如下所示：

```bash
cd /usr/src/linux*
```

要配置内核，你必须指明想要包含在 Linux 内核中的特性和设备驱动。本质上，你构建的是你自己的 Linux 内核版本，只包含你想要的特性。

Linux 提供了几种配置内核的方法：

- 输入 `make menuconfig` 通过类似文本模式 Linux 安装程序使用的基于文本的界面进入内核配置参数。
- 输入 `make xconfig` 使用基于 X 窗口系统的配置程序来配置内核。要使用这个具有图形界面的配置程序，你需要运行 X。你还必须安装 Qt 开发（`qt-devel`）包，并将 `QTDIR` 环境变量设置为 Qt 安装的目录。（如果你已安装 `qt-devel` 包，请输入 `export QTDIR=/usr/lib/qt-3.3` 以正确定义 `QTDIR`。）
- 输入 `make config` 使用 shell 脚本，它会逐一提示你输入每个配置选项。你可以从 Linux 命令提示符使用这个配置程序。使用此选项时，你需要经历漫长的问答过程来指定配置参数。对于每个问题，回答 `y` 表示将支持链接到内核，回答 `m` 表示构建模块，回答 `n` 表示跳过该特定设备的支持。
- 输入 `make oldconfig` 使用 shell 脚本在升级源代码后重新配置内核。此配置脚本保留现有选项，并仅提示输入新的或已更改的选项。

`make menuconfig`、`make xconfig`、`make config` 和 `make oldconfig` 命令达成相同的最终结果——每个命令都将你的选择存储在一个名为 `.config` 的文本文件中，该文件位于 `/usr/src/linux*` 目录中。由于文件名以点开头，如果你单独使用 `ls` 命令列出目录，你就看不到它。相反，输入 `ls -a` 可以在目录列表中查看 `.config` 文件。

内核配置步骤仅仅是将你的选择记录在 `.config` 文件中。（实际上，在首次配置内核之前，`.config` 文件并不存在。）在使用 `make` 命令编译内核之前，内核文件不会改变。这意味着你可以任意多次执行内核配置选项。如果你想从头开始使用默认设置，请在开始配置内核之前输入以下命令：

```
make mrproper
```

若要使用 `make` 命令查看可执行的内核配置构建步骤概览，请在终端窗口中输入以下内容（在你输入 `cd /usr/src/linux*` 将当前目录切换到正确位置之后）：

```
make help | more
```

在开始重新配置内核之前，先看一下典型的 `.config` 文件。例如，以下是我在 Linux 系统上配置内核后输入 `more .config` 时输出的一些行：

```
#
# Automatically generated make config: don't edit
CONFIG_X86=y
CONFIG_MMU=y
CONFIG_UID16=y
CONFIG_GENERIC_ISA_DMA=y
CONFIG_GENERIC_IOMAP=y
#
# Code maturity level options
#
CONFIG_EXPERIMENTAL=y
CONFIG_CLEAN_COMPILE=y
CONFIG_BROKEN_ON_SMP=y
CONFIG_INIT_ENV_ARG_LIMIT=32
#
# General setup

CONFIG_LOCALVERSION=""
CONFIG_SWAP=y
CONFIG_SYSVIPC=y
... lines deleted ...
```

本质上，每个配置选项都有一个名称，并且每个选项都被分配了一个值。名称以 `CONFIG_` 开头，后跟一个标识该选项的单词。每个选中的选项值为 `y`（表示链接该特性的支持）或 `n`（表示为该特性使用模块）。以 `#` 开头的行是注释。注释行列出未选中的特性。

![](img/11709a8f88c8cd03868a929dc94c0e2b_503_0.png)

我将通过 `make config` 命令来描述配置过程。虽然这种方法因为要逐一引导你通过每个选项而有些繁琐，但它是一个理想的学习工具。当你逐步遍历配置选项组时，我会提供注释解释大多数选项的含义。然后你可以使用你最喜欢的任意配置工具（`make config`、`make menuconfig`、`make xconfig` 或 `make oldconfig`）来配置内核。

当你使用 `make config` 命令配置内核时，你需要选择如何包含特定设备的支持。通常，对于每个配置选项，你必须从以下选择中回答：

- y 表示将支持链接到内核
- m 表示使用模块
- n 表示跳过该特定设备或特性的支持
- ? 获取该内核配置选项的帮助

如果设备没有模块化的设备驱动，你将看不到 m 选项。对于某些配置选项，你可能需要从列表中选择一个数字。

####### 开始内核配置

要开始配置内核，请以 *root* 身份登录，切换到 Linux 内核源代码目录（根据你的发行版输入 `cd /usr/src/linux*` 或 `cd /usr/src/kernel-source*`），并在终端窗口中输入 `make menuconfig`。配置工具随后显示第一个提示：

```
.
.
Linux Kernel Configuration
.
.
Code maturity level options
.
Prompt for development and/or incomplete code/drivers (EXPERIMENTAL) [y/n/?]
```

按 Enter 键接受默认的 Yes 回答。这会导致配置过程显示所有实验性的设备驱动。

![](img/11709a8f88c8cd03868a929dc94c0e2b_503_1.png)

每个提示的可能答案显示在方括号中，默认答案为大写。因此，[Y/n/?] 意味着默认答案是 Yes，另外两个可能的答案是 n 和 ?。要接受默认值，按 Enter 键。如需获取该选项的帮助，按 ?。如果你对任何选项有疑问，请按 ? 并在决定做什么之前仔细阅读帮助文本。你可以使用这个一般指南来进行选择。在以下部分中，我只解释所选的内核配置选项组。




####### 常规设置选项

此组选项允许你指示是否希望启用对通用功能的支持，例如 System V 进程间通信（IPC）、基于 BSD（Berkeley Software Distribution）UNIX 的进程核算，以及热插拔设备。你可以按 Enter 键接受默认选择。

####### 可加载模块支持

此组选项询问你关于可加载模块的支持。可加载模块是一块代码，Linux 内核可以加载并执行它，就好像它是操作系统的一部分一样。

- 可加载模块支持
  - 启用可加载模块支持 (MODULES) [Y/n/?]
  - 模块卸载 (MODULE_UNLOAD) [Y/n/?]
  - 强制模块卸载 (MODULE_FORCE_UNLOAD) [N/y/?]
  - 模块版本支持 (EXPERIMENTAL) (MODVERSIONS) [Y/n/?]
  - 所有模块的源校验和 (MODULE_SRCVERSION_ALL) [Y/n/?]
  - 模块签名验证 (EXPERIMENTAL) (MODULE_SIG) [Y/n/?]
  - 必需模块必须有效签名 (EXPERIMENTAL) (MODULE_SIG_FORCE) [N/y/?]
  - 自动内核模块加载 (KMOD) [Y/n/?]

如果你希望包含模块支持，请对第一个问题回答“是”（Yes），并接受其他问题的默认设置。注意，有一些选项标记为 EXPERIMENTAL（实验性）。只有在你配置会话开始时启用了 EXPERIMENTAL 代码支持时，这些问题才会出现。

####### 处理器类型和功能

此组选项用于设置子体系结构类型、处理器家族以及对特定处理器相关功能的支持：

- 处理器类型和功能
- 子体系结构类型
  1. PC 兼容 (X86_PC)
  2. AMD Elan (X86_ELAN)
  3. Voyager (NCR) (X86_VOYAGER)
  4. NUMAQ (IBM/Sequent) (X86_NUMAQ)
  5. SGI 320/540 (Visual Workstation) (X86_VISWS)
  - 选择(1-5):

子体系结构类型选项允许你从使用 Intel x86 处理器家族的不同类型的基本系统设计中进行选择，但这些设计可能与众所周知的 PC 兼容机有根本区别。在版本 2.6 之前，Linux 内核隐式假设系统架构基于旧的 IBM PC-AT 系列。从内核版本 2.6 开始，你可以为其他类型的基于 Intel x86 的架构构建内核，例如 SGI 图形工作站和具有非均匀内存访问（NUMA）的多处理器系统。你可能可以默认选择 PC 兼容子体系结构，但如果你必须为不同类型的基于 x86 的系统构建内核，其他选项是可用的。

下一组选项提示你选择处理器家族：

1. 386 (M386)
2. 486 (M486)
3. 586/ES/5x86/6x86/5x86MX (M586)
4. Pentium-Classic (M586TSC)
5. Pentium-MDX (M586MMX)
6. Pentium-Pro (M686)
7. Pentium-II/Celeron (pre-Coppermine) (MPENTIUMII)
8. Pentium-II/Celeron (Coppermine)/Pentium-III Xeon (MPENTIUMIII)
9. Pentium M (MPENTIUMM)
10. Pentium-4/Celeron (P4-based)/Pentium-4 M/Xeon (MPENTIUM4)
11. K6/K6-II/K6-III (MK6)
12. Athlon/Duron/K7 (MK7)
13. Opteron/Athlon64/Hammer/K8 (MK8)
14. Crusoe (MCRUSOE)
15. Efficeon (MEFFICEON)
16. Winchip-C6 (MWINCHIP6C)
17. Winchip-2 (MWINCHIP2)
18. Winchip-2A/Winchip-3 (MWINCHIP3D)
19. MediaGX/Gesode (MGEODEX)
20. CrixVII/VIA-C3 (MCYRIXIII)
21. VIA C3-2 (Nehemiah) (MVIA_C3_2)
- 选择[1-21]:

如果你选择 386，编译后的内核可以在任何其他处理器（例如 486 或任何类型的 Pentium）上运行。然而，如果你正在为系统特定的处理器创建内核，请从列表中选择你的处理器类型。

后续选项提示你一系列其他与处理器相关的选项，你可以将它们保留在默认设置中。如果有疑问，你可以按 ? 阅读每个选项的帮助，并选择适用于你系统的那些。

####### 电源管理选项

此组选项涉及管理系统电源，包括高级配置和电源接口（ACPI）、高级电源管理（APM）BIOS 支持以及 CPU 频率缩放。你可以简单地接受这些选项的默认设置。如果你不理解某个选项的含义，按 ? 获取该选项的帮助。

####### 总线选项

这些选项询问你对特定总线的支持：PCI、ISA、EISA、MCA 和 PCMCIA。工业标准结构（ISA）总线曾经是最广泛使用的总线（直到 PCI 总线出现之前）；这种总线用于原始的 IBM PC-AT。微通道结构（MCA）总线是 IBM 的专有总线，最早出现在 PS/2 PC 中。IBM 设计这种总线作为高速总线，但其专有性质阻碍了它在 PC 中的广泛使用。扩展工业标准结构（EISA）总线作为 MCA 总线的替代品出现，其性能与 MCA 相当。EISA 总线未得到广泛使用，因为 EISA 总线外设卡比其 ISA 总线对应物更昂贵。外围组件互连（PCI）总线是最新的高速总线；当前的 PC 使用 PCI 总线，但也提供 ISA 总线插槽，以便你可以继续使用 ISA 卡。

PCMCIA 代表个人计算机存储卡国际协会（Personal Computer Memory Card International Association），这是一个非营利组织，标准化了向笔记本电脑添加存储卡的接口。虽然最初是为存储卡构思的，但 PCMCIA 设备对于笔记本电脑的多种外接设备变得很流行。PCMCIA 设备称为 PC 卡，而术语 CardBus 指的是 PC 卡的电气规范。

通常，你需要内置对 PCI 和 ISA 的支持，并为 PCMCIA 支持构建模块。如果你的系统支持在系统加电运行时添加或移除 PCI 卡，你还可以添加对 PCI 热插拔的支持。

####### 可执行文件格式

开启对可执行与可链接格式（ELF）的支持，这是 Linux 中可执行文件和库的标准格式。在 ELF 之前，可执行文件的格式称为 *a.out*（基于 C 编译器生成的可执行文件的默认名称）。在内核版本 2.6 中，你可以构建一个模块以支持旧的 a.out 格式。

####### 内存技术设备

此类别选项为驻留在内存技术设备（如闪存和随机存取存储器）上的文件系统提供支持。这些文件系统通常用于嵌入式设备。此类别包括多个选项，用于构建支持各种内存设备的内核模块。构建这些模块没有害处，因为如果你的电脑没有适当的内存设备，它们不会被加载。

####### 并口支持

如果你使用通过 PC 并口连接的设备（如打印机或并口 Zip 驱动器），这些选项非常重要。对**并口支持**和**PC 风格硬件**选项回答 **m**，以便将驱动程序构建为模块。

####### 即插即用支持

这些选项询问你是否希望在内核中启用即插即用（PnP）支持。如果你启用 PnP 支持，内核会自动配置 PnP 设备（就像 Windows 那样）。启用这些选项。

####### 块设备

块设备（如磁盘驱动器）以块为单位传输数据（与键盘不同，键盘一次传输一个字符）。此组选项涉及连接在 PC 并口上的软盘和 IDE（集成驱动器电子学）设备以及其他块设备。

- 块设备
  - 正常软盘支持 (**BLK_DEV_FD**) [**M/n/y/?**]
  - XT 硬盘支持 (**BLK_DEV_XD**) [**N/m/y/?**]
  - 并口 IDE 设备支持 (**PARIDE**) [**M/n/?**]

第一个问题询问你是否需要软盘驱动器支持。因为大多数 PC 都有软盘驱动器，所以你通常回答“是”（Yes）。如果你有通过 PC 并口连接的外部 CD-ROM 或磁盘设备，你应该按 Enter 接受第三个问题的默认设置。某些 IDE 设备使用并口 IDE 适配器——这就是 **PARIDE** 选项所指的内容。

下一组选项用于各种并行 IDE 驱动程序。你可能希望通过可加载模块内置对并口 IDE 设备的支持。这样，如果你需要它们，模块就在那里，但内核不会因为额外的代码而臃肿。

接下来是另一组块设备选项。**BLK_DEV_LOOP** 选项用于回环设备。启用回环设备让 Linux 内核操作存储在单个大文件中的完整文件系统映像。如果你想要挂载 CD 或 DVD 映像（例如，Linux ISO 文件）并在实际刻录 CD 或 DVD 之前检查它，这个选项很有用。

RAM 磁盘支持允许内核使用系统内存的一部分作为能够存储文件系统的磁盘。通常，RAM 磁盘仅在系统启动期间起作用，此时硬盘可能不可用。


。如果启动的是 SCSI 磁盘，且未将 SCSI 驱动程序编译进内核，则 RAM 磁盘是必需的。

####### ATA/ATAPI/MFM/RLL 支持

下一组问题涉及 IDE 设备，例如硬盘和 ATAPI CD-ROM 驱动器。

- ATA/ATAPI/MFM/RLL 支持

ATA/ATAPI/MFM/RLL 支持 (IDE) [M/n/y/?]  
增强型 IDE/MFM/RLL 磁盘/CD-ROM/磁带/软盘支持 (BLK_DEV_IDE) [M/n/?]

在配置操作系统时，你必须做好遇到大量缩略词的准备——这里就有四个缩略词：ATA、ATAPI、MFM 和 RLL。这些都与硬盘或连接磁盘驱动器与 PC 的接口有关。它们的含义如下：

- **ATA** 代表 AT Attachment（AT 附加），指连接硬盘和 CD-ROM 驱动器到 PC 主板的 PC-AT 风格接口。  
- **ATAPI** 代表 AT Attachment Packet Interface（AT 附加分组接口），指将磁盘控制器集成在硬盘本身上的原始 PC 硬盘。这种接口过去被称为*集成驱动电子学*（Integrated Drive Electronics），或 IDE。你通常看到 IDE、ATA 和 ATAPI 这些术语互换使用。  
- **MFM** 代表修改调频（Modified Frequency Modulation），这是旧式硬盘上编码数据的方式。这些硬盘可以通过 IDE 接口工作。  
- **RLL** 代表有限长游程（Run Length Limited），是 PC 早期将数据存储到硬盘上的旧技术。RLL 磁盘可以通过 IDE 接口工作。

第一个问题询问你是否希望内核支持 IDE 设备。第二个问题询问你是否希望使用功能齐全的 IDE 设备，它可以控制多达十个 IDE 接口。由于每个 IDE 接口可以有一个主设备和一个从设备，这使得 Linux 可以访问总共多达 20 个 IDE 设备，例如磁盘或 CD-ROM 驱动器。你可以按 Enter 键接受这两个选项的默认选择，即都作为模块。

下一组选项涉及各种 IDE 驱动程序。你可以接受这些选项的默认答案。请注意，IDE/ATAPI FLOPPY 指的是 IDE 软盘驱动器，例如 Iomega Zip 驱动器或 Imation SuperDisk LS-120 驱动器。关于 CMD640 和 RZ1000 错误修复的问题涉及特定 IDE 接口中使用的某些已知存在问题的芯片组。

####### SCSI 设备支持

这组选项与 SCSI 设备有关。SCSI 代表 Small Computer Systems Interface（小型计算机系统接口）——这是一种通过它可以连接多个设备（如硬盘和扫描仪）到 PC 的接口类型。如果你的系统有 SCSI 适配器，你应该先对*SCSI* 选项回答**是**。之后，你必须回答关于连接到 SCSI 适配器的设备类型（磁盘、磁带、CD-ROM）的问题。最后，你必须启用对你系统上特定 SCSI 适配器型号的支持。

####### IEEE 1394 (FireWire) 支持

下一组选项用于启用 IEEE 1394 支持，作为模块或链接到内核。IEEE 1394 是用于连接外设到 PC 的高速串行总线。苹果称此总线为*FireWire*（火线）；索尼称其为*i.Link*。IEEE 1394 类似于 USB，但它可以以高达 400 Mbps 的速率传输数据，这比旧版 USB 1.1 的数据速率快 30 多倍。（注意 USB 2.0 快得多；它可以以高达 480 Mbps 的速率传输数据。）由于其高数据传输速率，IEEE 1394 非常适合将高速外设，如数字音频和视频设备以及外部硬盘，连接到 PC。

目前，Linux 支持兼容 Texas Instruments PCILynx/PCILynx2 和 OHCI 芯片组的 IEEE 1394 芯片组。如果你的 PC 有 IEEE 1394 适配器，你可以通过这些选项构建必要的驱动程序。

- IEEE 1394 (FireWire) 支持
- IEEE 1394 (FireWire) 支持 (IEEE1394) (M/n/y/?)

欲了解有关在 Linux 中使用 IEEE 1394 外设的更多信息，请访问 Linux IEEE 1394 项目的网站 www.linux1394.org。

####### I2O 设备支持

发音为*eye-two-OH*，I2O 指智能输入/输出（Intelligent Input/Output）——一种独立于操作系统和被控设备的新设备驱动程序体系结构。I2O 通过逻辑上分离负责管理设备的部分和包含操作系统特定详情的部分来工作。（驱动程序功能的逻辑分离被称为*I2O 分离驱动模型*。）I2O 驱动程序的两个部分是操作系统服务模块（OSM），它与操作系统协同工作，以及硬件设备模块（HDM），它与驱动程序管理的特定设备接口。OSM 和 HDM 通过互相传递消息来通信。

Linux 附带一些用于 SCSI 和 PCI 设备的 I2O 驱动程序。你可以通过以下配置选项构建 I2O 驱动程序：

- I2O 设备支持
- I2O 支持 (I2O) [M/n/y/?]
  - I2O 配置支持 (I2O_CONFIG) [M/n/?]
  - I2O 块 OSM (I2O_BLOCK) [M/n/?]
  - I2O SCSI OSM (I2O_SCSI) [M/n/?]
  - I2O /proc 支持 (I2O_PROC) [M/n/?]

####### 网络支持

这组选项涉及网络。如何设置这些选项取决于你希望如何在网络中使用你的 Linux 系统。始终对 TCP/IP 网络选项回答“是”，因为 X 窗口系统使用 TCP/IP 网络（即使你的 PC 不在任何网络上）。你还可以启用对 IPv6 的实验性支持——下一代互联网协议。

如果你希望使用你的 Linux 系统作为*防火墙*——一个控制局域网（LAN）和互联网之间信息流动的中介系统，请对网络数据包过滤选项回答“是”。

网络支持选项中的其他类别包括无线局域网、以太网（10/100 Mbps 以及千兆位）、ATM（异步传输模式）、令牌环、ARCnet、AppleTalk、广域网（WAN）、PCMCIA 网络设备、业余无线电、红外线和蓝牙。对于以太网，你可以为你的系统安装的以太网卡构建支持。此类还包括对无线网络的驱动无线以太网卡的驱动支持。你还可以启用对 SCTP——流控制传输协议——的实验性支持，该协议旨在通过 IP 网络传输公共电话交换网信令消息（RFC 3758 描述了 SCTP）。

红外线支持用于使用红外数据协会（IrDA）指定的协议进行红外通信。IrDA 通信被许多笔记本电脑和个人数字助理（PDA）使用，例如 Palm 和 Handspring。许多红外接口以*狗*（dongles）的形式出现——通常附加到 PC 串行端口的适配器。你可以使用此部分的选项来启用对几种常见类型狗的支持。

蓝牙是一种低功耗、短距离无线技术，用于在 2.4 GHz 频段连接设备。使用蓝牙的设备通常在彼此 10 米范围内时可以连接。欲了解有关蓝牙的更多信息，请访问 www.bluetooth.com。Linux 通过核心驱动程序和多个其他模块支持蓝牙。你可以回答 y 以启用蓝牙支持，然后选择特定于你的蓝牙设备的其他选项。

####### ISDN 子系统

这组选项允许你包括对*ISDN*（综合业务数字网）的支持——这是一种你可以用来将 Linux 系统连接到互联网的数字电话线。这些与 ISDN 相关的选项包括特定 ISDN 适配器的配置。

仅当你的 PC 有 ISDN 卡时才构建 ISDN 驱动程序。如果你预见到将添加 ISDN 卡并从电话公司购买 ISDN 服务，你可以将驱动程序构建为模块。

####### 电话支持

配合合适的硬件和软件，电话支持选项允许你使用 Linux 系统进行通过互联网的电话（也称为*互联网语音协议*或*VoIP*）。如果你有电话卡，例如由 Quicknet Technologies, Inc. 制造的 Internet PhoneJACK 或 Internet LineJACK，你可以选择构建用于电话支持的驱动程序模块。如果你没有电话卡，可以安全地保持这些选项关闭。

####### 输入设备和字符设备

接下来的几个选项涉及配置键盘、鼠标、摇杆和触摸屏等输入设备，以及连接到串行和并行端口的设备。这些选项还包括多端口串行接口卡的配置，这些卡允许你将多个终端或其他设备连接到你的 Linux 系统。如果你的系统上没有此类设备，请回答*否*。在列表的末尾，你会看到一个关于并行打印机支持（*PRINTER*）的问题。如果你计划将打印机连接到并行端口，请对此选项回答*是*。

####### 看门狗定时器

这些配置选项允许你启用看门狗定时器支持。基本上，这会导致内核创建一个特殊文件；如果未每分钟打开并写入该文件，系统将重新启动。一些看门狗板可以监控 PC 的状态（包括温度）。你还可以从这组选项中启用对特定看门狗卡的支持。

如果你希望访问 PC 的非易失性（电池供电）内存——NVRAM——在实时时钟中，请对*NVRAM*选项回答*是*。你可以通过启用*RTC*选项来访问实时时钟。

####### 软盘磁带驱动器

如果你有连接到软盘控制器的磁带驱动器，请对下一个选项回答*y* 或*m*，并适当选择其他参数（或接受默认选择）：




# 软盘磁带支持

- `Ftape，软盘磁带设备驱动程序`
- `Ftape (I2C-80/Trawian) 支持` `[F_TAPE]` `[N/m/y/?]`

您还可以启用与软盘磁带驱动器相关的若干参数。

####### 高级图形支持

下一组选项配置了对支持硬件加速 3D 图形的高级显卡的支持。您可以启用第一个选项来构建 AGP（加速图形端口）驱动程序，并针对您的特定芯片组选项回答 `Yes`。

`/dev/agpgart` `[AGP 支持]` `[AGP]` `[Y/m/n/?]`

接下来，您需要配置一组 Direct Rendering Manager（`DRM`）的选项——`DRM` 是一个支持 `XFree86 Direct Rendering Infrastructure`（`DRI`）的独立设备驱动程序。`DRI` 旨在直接访问高级显卡中的 3D 图形硬件，例如 `3Dfx Banshee` 和 `Voodoo3+`。要了解有关 `DRI` 的更多信息，请使用 Web 浏览器访问网址 `http://dri.freedesktop.org/wiki`。

如果您有 3D 显卡，您可以对 `DRM` 回答 `Yes`，并为系统中的显卡构建模块。如果您没有列表中的任一显卡，则应该对这些选项回答 `No`。

####### I2C 支持

`I2C（Inter-Integrated Circuit）——发音为 EYE-squared-see——是 Philips 开发的一种协议，用于通过一对电线在 10 到 100 kHz 的速率下在集成电路芯片之间进行通信。系统管理总线 (SMBus) 是 I2C 协议的一个子集。许多现代主板都有一个 SMBus，用于连接 EEPROM（电可擦除可编程只读存储器）和用于硬件监控的芯片等器件。Linux 支持 I2C 和 SMBus 协议。Linux 视频功能需要此支持。如果您有任何需要 I2C 支持的硬件传感器或视频设备，请对 I2C 支持选项回答 `m`（表示模块），并针对您的硬件的具体驱动程序回答 `m`。例如，如果您想使用 BT848 帧采集板（用于捕获视频），则应对 `I2C`、`I2C_ALGOBIT` 和 `VIDEO_BT848` 选项回答 `m`（`I2C_ALGOBIT` 选项启用了对称为 `I2C bit-banging` 接口的支持，该接口由 `BT848 板` 支持）。

####### 多媒体设备

此类别的选项配置了对多媒体设备的支持，例如摄像机、电视调谐器和 FM 收音机卡。

###### 重新构建内核

####### 帧缓冲

通过这些选项，您可以启用对帧缓冲设备的支持。帧缓冲是图形硬件的抽象，使内核和其他软件能够生成图形输出，而无需依赖显卡的低级细节（如硬件寄存器）。许多显卡都支持帧缓冲。

####### 声音

使用这组选项配置声卡支持。如果您安装了声卡，请首先对 Sound Card Support 选项回答 m。然后，对 Advanced Linux Sound Architecture (ALSA) 和声音设备回答 m。您可以始终为所有类型的声卡构建声音模块。这样，系统声卡所需的模块在需要时即可使用。

####### USB 支持

使用此类别的选项配置对通用串行总线（USB）的支持——这是内置于大多数新 PC 中的串行总线。USB 1.1 版本支持高达 12 Mbps 的数据传输速率——即每秒 1200 万位或每秒 1.5MB——相比之下，标准串行端口（如 COM1）的传输速率为 115 Kbps 或 0.115 Mbps。您可以在 USB 总线上级联多达 127 个设备。总线还为设备提供电源，并且您可以在 PC 运行时连接或断开设备——这种功能通常称为热交换或热插拔。USB 2.0 版本（或简称为 USB 2.0 或 USB2）将数据传输速率提升到 480 Mbps，略快于竞争者 IEEE 1394（FireWire）总线。

USB 可以替代 PC 的串行端口和并行端口的功能，以及键盘和鼠标端口。如今，许多 PC 外围设备——如鼠标、键盘、打印机、扫描仪、调制解调器、数码相机等——都设计为通过 USB 端口连接到 PC。

如果您的 PC 有 USB 端口，请对 Support for USB 选项回答 m（以便构建模块）。然后，您必须根据 PC 拥有的 USB 接口类型——EHCI（用于 USB 2.0）、UHCI（Intel）或 OHCI（Compaq 及其他厂商）——对 EHCI_HCD、UHCI_HCD 或 OHCI_HCD 选项回答 n。要确定 USB 接口的类型，请在终端窗口中输入 lspci，并在输出中查找 USB 控制器的制造商和型号。

为了支持 USB 2.0，您可以对 EHCI_HCD（即主机控制器设备）选项回答 m。

选择 UHCI 或 OHCI 接口支持后，您必须构建系统中特定 USB 设备的驱动程序模块。

### 文件系统

通过此类别的选项，您可以启用对特定类型文件系统的支持。您会惊讶于 Linux 内核支持的众多不同的文件系统。（表 5-1 仅列出了其中一部分。）通常，您构建的内核支持核心 Linux 文件系统（Ext2 和 Ext3）、CD-ROM 文件系统（ISO 9660 和 Joliet）以及 DOS/Windows 文件系统（MSDOS、FAT 和 VFAT）。为了与 Windows 2000/XP 系统共享文件，您还需要构建 CIFS 模块。

**表 5-1 Linux 内核支持的某些文件系统**

| 文件系统 | 描述 |
| :--- | :--- |
| Apple Macintosh | Macintosh HFS 文件系统。（Linux 可以读写 Macintosh 格式的软盘和硬盘。） |
| CIFS | 通用互联网文件系统 (CIFS)——服务器消息块 (SMB) 协议的后继者——是 Windows 2000、Windows XP 和 Samba 等 Windows 服务器的新文件系统。 |
| Coda | 一种高级网络文件系统，类似于 NFS，但更好地支持断开连接的操作（例如笔记本电脑），并具有更好的安全模型 |
| Ext2 | 第二扩展文件系统——Linux 的当前标准文件系统 |
| Ext3 | 支持日志记录的文件系统——一种允许在崩溃后快速恢复磁盘的机制 |
| FAT | 指任何基于文件分配表 (FAT) 的文件系统（包括 MS-DOS 和 Windows 95 VFAT 文件系统） |
| HPFS | OS/2 HPFS 文件系统。（Linux 只能读取 HPFS 文件。） |
| ISO 9660 | CD-ROM 上使用的标准 ISO 9660 文件系统。（该系统也被称为 *High Sierra File System*，在某些 UNIX 工作站上称为 `hfs`。） |
| Joliet | Microsoft 为 ISO 9660 CD-ROM 文件系统开发的 Joliet 扩展，允许使用 Unicode 格式的文件名。（Unicode 是一种新的 16 位字符代码，可以编码世界上几乎所有语言的字符。） |
| Minix | Minix 文件系统——Linux 的原始文件系统 |
| MSDOS | MS-DOS 文件系统 |
| NFS | 用于从网络上的其他系统共享文件和目录的网络文件系统 |
| NTFS | NT 文件系统 (NTFS)——Microsoft Windows NT 和 XP 使用的文件系统。（Linux 只能读取 NTFS 磁盘。） |
| /proc | 一个虚拟文件系统，您可以通过它获取有关内核的信息。`/proc` 文件系统不存在于磁盘上；文件是在您访问它们时创建的。 |
| ReiserFS | 一种高效的文件系统，将文件名和文件都存储在平衡树中，并使用日志记录 |
| SMB | 使用服务器消息块 (SMB) 协议从运行 Windows 95/98/NT/2000 的网络 PC 访问共享目录的文件系统 |
| System V | SCO、Xenix 和 Coherent 版 UNIX 在 Intel PC 上使用的文件系统 |
| UDF | 一些 CD-ROM 和 DVD 上使用的新文件系统。（例如，可重写 CD 使用 UDF 文件系统，无论是以分组模式写入的还是由 DirectCD 等 UDF 实用程序写入的。） |
| UFS | BSD（Berkeley Software Distribution）变体 UNIX（如 SunOS、FreeBSD、NetBSD 和 NeXTstep）使用的文件系统。 |
| VFAT | 具有长文件名的 Windows 95/98/NT/2000 文件系统。 |

####### 分区类型

Linux 可以读取和处理由许多不同系统创建的磁盘分区。这些选项允许您包含对特定分区类型的支持：

- 分区类型
    - 高级分区选择 (PARTITION_ADVANCED) [Y/n/?]
    - Acorn 分区支持 (ACORN_PARTITION) [N/y/?]
    - Alpha OSF 分区支持 (OSF_PARTITION) [Y/n/?]
    - Amiga 分区表支持 (AMIGA_PARTITION) [N/y/?]
    - Atari 分区表支持 (ATARI_PARTITION) [N/y/?]
    - Macintosh 分区映射支持 (MAC_PARTITION) [Y/n/?]
    - PC BIOS (MSDOS 分区表) 支持 (MSDOS_PARTITION) [Y/n/?]
    - ... 行已删除 ...

####### 本地语言支持

此组配置选项要求您选择本地语言字符集。Microsoft FAT 文件系统使用这些字符集来存储和显示多种语言之一的文件名。字符集存储在称为 *DOS 代码页* 的文件中。您必须包含适当的代码页，以便 Linux 内核能够正确读取和写入硬盘上任何 DOS 分区中的文件名。请注意，代码页仅适用于文件名；它们与文件的实际内容无关。

您可以包含任意数量的代码页支持。只需对您选择的语言的代码页回答 Yes 即可。





####### 内核调试

这组选项允许你调试内核，并使用 SysRq 键（相当于按下 Alt+Print Screen）在系统崩溃后立即获取重要的状态信息。如果你是期望调试内核的 Linux 开发人员，这些信息会很有用。大多数用户选择“否”以禁用这些选项（因为大多数用户运行的是稳定版本的内核，并且不期望修复内核错误）。

####### 安全选项

通过这些选项，你可以包含对 **Security Enhanced Linux (SELinux)** 的支持，它由美国国家安全局（NSA）开发。SELinux 随 Linux 提供，但你可以在引导时通过提供 `selinux=0` 作为引导选项来关闭它。有关 SELinux 的更多信息，请访问 www.nsa.gov/selinux。

####### 加密支持

这组选项用于在内核中启用加密支持。你可以启用支持，如下面选项的默认选择所示：

- 加密选项

```
Cryptographic API (CRYPTO) [Y/?] Y
HMAC support (CRYPTO_HMAC) [Y/?] Y
Null algorithms (CRYPTO_NULL) [M/n/y/?]!
MD4 digest algorithm (CRYPTO_MD4) [M/n/y/?]
MD5 digest algorithm (CRYPTO_MD5) [Y/m/?]
SHA1 digest algorithm (CRYPTO_SHA1) [M/y/?]
SHA256 digest algorithm (CRYPTO_SHA256) [M/n/y/?]
SHA384 and SHA512 digest algorithms (CRYPTO_SHA512) [M/n/y/?]
... lines deleted ...
```

你还可以启用对某些硬件加密设备的支持，并为几种循环冗余校验（CRC）算法构建模块。

####### 构建内核和模块

配置内核选项后，你必须构建内核。这部分可能需要一段时间。根据你的系统不同，构建新内核可能需要几分钟到一个多小时。

在一行中键入以下内容以启动该过程：

```
make
```

# 492 安装模块

**make** 命令会创建新内核，以及你在配置步骤中指定的任何模块。

![](img/11709a8f88c8cd03868a929dc94c0e2b_517_0.png)

在内核构建过程中，你会在屏幕上看到大量消息。完成后，名为 **bzImage** 的压缩文件形式的新内核位于内核源代码所在位置的 **arch/i386/boot** 子目录中。

要使用新内核，你必须将内核文件和 **System.map** 文件以特定名称复制到 **/boot** 目录，并编辑 **GRUB** 菜单以设置 GRUB——引导加载程序。然而，在进行内核安装之前，你必须安装模块并构建一个新的初始 RAM 磁盘。

###### 安装模块

如果你在内核配置期间选择了任何模块，内核构建步骤也会构建模块。你只需要安装它们即可。使用以下命令执行此任务：

```bash
cd /usr/src/linux*
make modules_install
```

**make modules_install** 命令将所有模块复制到 **/lib/modules** 目录下的新子目录中。子目录的名称应与内核版本号相同。

现在你可以安装内核并使其可用于 GRUB 引导。

####### 创建初始 RAM 磁盘文件

新内核需要一个新的初始 RAM 磁盘文件，你可以使用 **mkinitrd** 命令创建它。通常，初始 RAM 磁盘镜像存储在一个以 **initrd** 开头的文件中。你可能已经猜到，**initrd** 是初始 RAM 磁盘的缩写，而 **mkinitrd** 命令之所以这样命名是因为它创建 **initrd** 文件。

**mkinitrd** 程序位于 **/sbin** 目录中，你必须以 **root** 身份登录，并使用以下形式的命令行来创建 **initrd** 文件：

```bash
/sbin/mkinitrd /boot/initrd-filename.img module-directory
```

**initrd** 文件必须位于内核所在的 **/boot** 目录中。你可以为 *initrd-filename* 使用任何文件名。*module-directory* 是 **/lib/modules** 中包含新内核模块文件的目录的名称。**make modules_install** 步骤将模块放置在一个名称为内核版本号的目录中。例如，如果你的内核版本（由 `uname -r` 命令报告）是 2.6.11，那么在 `make modules_install` 步骤之后，`module-directory` 就是 2.6.11。

另一种常见做法是使用通过将模块目录名称附加到 `initrd-` 前缀而创建的 `initrd` 文件名。因此，对于模块目录 2.6.11，`initrd` 文件将是 `initrd-2.6.11.img`。

要为新构建的内核创建初始 RAM 磁盘镜像，键入以下命令：

```
sbin/mkinitrd /boot/2.6.11.img 2.6.11
```

此命令在 `/boot` 目录中创建文件 `initrd-2.6.11.img`。你必须在 GRUB 菜单文件中引用此 `initrd` 文件（在 Fedora Core 中为 //etc/grub.conf，在 Debian 和 SUSE 中为 /boot/grub/menu.lst）。

####### 安装新内核并设置 GRUB

大多数 Linux 发行版使用 GRUB 从磁盘加载 Linux 内核。你必须将新内核添加到 GRUB 菜单中，以便 GRUB 可以将其显示为可引导的选项。

在 Debian、MEPIS、SUSE 和 Ubuntu 中，GRUB 菜单是 /boot/grub/menu.lst 文件。在 Fedora Core 中，GRUB 菜单由 /etc/grub.conf 文件指定。你应该编辑适用于你的发行版的文件。

这是我系统上典型的 GRUB 菜单文件：

```
default
# Set a timeout, in seconds, before automatically booting the default entry
# (normally the first entry defined).
timeout
5
#### Ubuntu Linux
title
root
kernel
initrd
# The next entry automatically added by the Debian installer for an existing
# linux installation on /dev/hdb3.
title Xandros on /dev/hdb3
root (hd1,2)
chainloader +1
# Windows XP
title Windows XP
root (hd0,1)
chainloader +1
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_518_0.png)

以下是 GRUB 菜单文件中一些行的含义（以 # 开头的行是注释）：

- `default 0:` 指定第一个引导条目为 GRUB 引导的默认条目。如果此行设置为 1，GRUB 将引导第二个条目（2 表示第三个条目，3 表示第四个，等等）。
- `timeout 5:` 使 GRUB 在等待 5 秒后自动引导默认条目。如果文件中还有其他引导条目，用户可以从 GRUB 显示的引导菜单中选择另一个条目。
- 以 `title` 开头的行构成了第一个引导条目或部分（下一个条目以另一个 `title` 行开头），并且此条目定义了 GRUB 可以引导的特定内核文件。你可以通过向配置文件添加类似的部分来让 GRUB 引导另一个内核。此引导条目中各行的含义如下：
- `root (hd0,4):` 将根设备设置为主磁盘的第一个逻辑分区。在这个特定系统上，Ubuntu 的 Linux 内核安装在此分区上。
- `kernel /vmlinuz-2.6.10-5-386 root=/dev/hda9 ro acpi=off quiet splash:` 标识如果用户选择此引导条目则 GRUB 加载的内核。在这种情况下，内核文件是位于根设备中的 `/vmlinuz-2.6.10-5-386`。在 Linux 系统中，该分区通常挂载在 `/boot` 目录上。换句话说，GRUB 加载内核文件 `/boot/vmlinuz-2.6.10-5-386.` 内核名称后面的项目是提供给内核的选项。例如，`root` 选项标识包含根文件系统 `(/)` 的分区。
- `initrd /initrd.img-2.6.10-5-386:` 指定包含初始 RAM 磁盘 (`initrd`) 图像的文件，该图像在磁盘可用之前作为文件系统服务。Linux 内核使用 `RAM disk`——作为磁盘使用的内存块——来启动；然后它加载其他驱动模块并开始使用硬盘。
- 以 `title` 开头的下一部分用于从第二个 IDE 驱动的第三个分区引导 Xandros。Xandros 使用 LILO 引导加载程序，此引导条目使用 GRUB 的 `chainloader` 命令将控制权转移给 LILO 引导加载程序。
- 以 `title Windows XP` 开头的下一部分是第三个引导条目，指的是恰好位于该系统上的 Windows XP 操作系统。标题行旁边的文本出现在 GRUB 菜单中，用户从中选择要引导的操作系统。





要配置 GRUB 以启动新的 Linux 内核（即你刚刚构建的内核），请遵循以下步骤：

- 将新的内核二进制文件复制到 `/boot` 目录。

新的压缩内核文件位于内核源代码所在的 `arch/i386/boot` 子目录中。内核文件名通常是 `bzImage`。我只需将该文件以相同名称复制到 `/boot` 目录即可。

如果内核文件名是 `vmlinux`，请确保使用 `vmlinux` 而不是 `bzImage`。你可以将 `/boot` 中的内核文件名更改为任何名称，只要在步骤 3 中在 GRUB 菜单文件中引用内核时使用相同的文件名即可。

- 将新的 System.map 文件从内核源代码目录复制到 `/boot` 目录。

- 使用你喜欢的文本编辑器编辑 GRUB 菜单文件，在文件中添加以下行：

```
title New Linux kernel (2.6.11)
root (hd0,2)
kernel /bzImage root=/dev/hda10 ro
initrd /initrd-2.6.11.img
```

在你的系统中，请确保 `root` 行是正确的——不要使用 `(hd0, 2)`，而是列出挂载在 `/boot` 上的正确磁盘分区。此外，请使用内核映像文件的正确文件名（例如，如果内核文件名为 `/vmlinux`，则使用 `/vmlinux`）。内核行上的 `root` 选项必须设置为挂载在 Linux 文件系统根目录（`/`）的 `root` 目录的分区设备名称。

注意：initrd 行指的是你在前面步骤中创建的 initrd 文件。

- 保存 GRUB 菜单文件并退出编辑器。

现在你准备好重新启动系统并试用新内核了。

###### 重新启动系统

完成 GRUB 配置后，你可以重启系统。在你仍以 `root` 身份登录时，输入以下命令以重启系统：

```
reboot
```

当你看到 GRUB 屏幕时，选择你在 GRUB 菜单文件中分配给新内核的名称。

系统重启后，你会看到熟悉的图形登录界面。为了证明你确实正在运行新内核，请作为用户登录，打开一个终端窗口，并输入 `uname -srv`。此命令会显示内核版本，以及构建该内核的日期和时间。如果你升级了内核源代码，你将看到新内核的版本号。如果你只是重新构建了相同旧版本的内核，则日期和时间将与你重新构建内核的时间匹配。这就证明系统正在运行新内核。

![](img/11709a8f88c8cd03868a929dc94c0e2b_521_0.png)

如果系统*挂起*（屏幕上没有输出或没有磁盘活动），你可能在内核重新构建过程中跳过了某个步骤。你可以关闭并重新打开 PC 电源以重启。这次，在 GRUB 屏幕上选择旧的内核名称。

## 第六卷

#### 安全性

The 5th Wave By Rich Tennant

![](img/11709a8f88c8cd03868a929dc94c0e2b_522_0.png)

#### 目录概览

第 1 章：介绍 Linux 安全性....499

第 2 章：保护 Linux 主机....513

第 3 章：改进网络安全....529

第 4 章：执行计算机安全审计 .....547

##### 第 1 章：介绍 Linux 安全性

本章内容

- 建立安全策略和框架
- 理解主机安全问题
- 理解网络安全问题
- 翻译计算机安全术语
- 关注安全新闻和更新

在本章中，我将解释为什么你需要担心安全性，并给你提供一个关于如何掌握安全性的高层视图。我将解释整体安全框架的概念，并解释安全性的两个关键方面——主机安全性和网络安全。我将以介绍讨论计算机安全性时使用的术语来结束本章。

###### 为什么要担心安全性？

在当今的网络化世界中，你必须担心你的 Linux 系统的安全性。对于独立系统或在隔离的局域网 (LAN) 中使用的系统，你需要专注于保护系统免受用户侵害，以及保护用户之间互不干扰。换句话说，你不想让用户故意或非故意地修改或删除系统文件。此外，你也不希望用户破坏其他用户的文件。

如果你的 Linux 系统连接到互联网，你必须保护系统免受来自互联网的不需要的访问。这些入侵者——通常被称为*黑客*——通常会冒充用户，窃取或破坏信息，甚至拒绝你访问你自己的系统（这被称为*拒绝服务*或 DoS 攻击）。

就其性质而言，互联网连接使你的系统可被互联网上的任何其他系统访问。毕竟，互联网连接了全球的大量网络。事实上，互联网服务（如 HTTP [Web] 和 FTP）的客户端/服务器架构依赖于互联网提供的广泛开放的网络访问。不幸的是，对运行在你系统上的互联网服务的轻松访问也意味着网络上的任何人都可以轻松访问你的系统。

如果你运营一个向他人提供信息的互联网主机，你当然希望每个人都能访问你系统的互联网服务，如 FTP 和 Web 服务器。然而，这些服务器通常存在漏洞，黑客可能会利用这些漏洞来危害你的系统。你需要了解互联网服务的潜在安全风险——以及你可以采取哪些预防措施来最小化某人利用你的 FTP 或 Web 服务器弱点的风险。

你还希望保护你公司的内部网络免受外部人员的侵害，尽管你的目标是通过 Web 或 FTP 服务器向外部世界提供信息。你可以通过设置互联网*防火墙*来保护你的内部网络——这是内部网络的一个受控访问点——并将 Web 和 FTP 服务器放置在防火墙外部的主机上。

###### 建立安全框架

保护你的 Linux 系统的第一步是建立*安全策略*——一组指导方针，说明你允许用户（以及来自互联网的访客）在你的 Linux 系统上执行哪些操作。你建立的安全级别取决于你如何使用 Linux 系统——以及如果有人获得对你系统的未授权访问，风险有多大。

如果你是组织内一个或多个 Linux 系统的系统管理员，你很可能希望让公司管理层以及用户参与制定安全策略。显然，你不能创建一个阻止所有访问的严苛策略。（那将阻碍任何人有效地在系统上工作。）另一方面，如果用户正在创建或使用对组织有价值的数据，你必须建立一项保护数据不向外部人员披露的政策。换句话说，安全策略应在用户需求与保护系统的需要之间取得平衡。

对于独立的 Linux 系统，或者你偶尔连接到互联网的家庭系统，安全策略可以只是列出你希望在系统上运行的互联网服务以及你计划在系统上设置的用户账户的列表。对于任何大型组织，你可能在连接到互联网（最好通过防火墙）的局域网上有多个 Linux 系统。（再次强调，*防火墙*是控制局域网与互联网之间互联网协议—IP—数据包流动的设备。）在这种情况下，系统地考虑整个组织的计算机安全是最佳做法。图 1-1 展示了组织范围计算机安全框架的关键要素。

图 1-1 中概述的安全框架包括：

- 确定业务对安全性的要求
- 执行风险评估
- 建立安全策略
- 实施包括人员、流程和技术在内的网络安全解决方案，以减轻已识别的安全风险
- 持续监控和管理安全

在以下部分中，我将讨论安全框架的一些关键要素。

![](img/11709a8f88c8cd03868a929dc94c0e2b_526_0.png)

####### 确定业务对安全性的要求

业务要求识别业务的安全需求——你需要保护的计算机资源和信息（包括适用法律规定的要求，如保护某些类型数据隐私的要求）。典型的安全要求可能包括以下各项：

- 允许授权用户访问信息
- 实施规定谁可以访问哪些信息的业务规则
- 采用强大的用户身份验证系统
- 拒绝数据上的恶意或破坏性操作
- 保护数据在跨网络移动时的端到端安全
- 实施适用法律规定的所有安全和隐私要求





####### 执行风险分析

风险分析的核心在于识别和评估风险——即可能危害您 Linux 系统的潜在事件。该分析涉及确定以下内容，并通过分析来确定处理风险的优先级：

- **威胁：** 您所要防范的对象
- **漏洞：** 可能被威胁利用的弱点（这些就是风险）
- **可能性：** 威胁利用该漏洞的概率
- **影响：** 利用特定漏洞所产生的后果
- **缓解措施：** 为降低漏洞风险而采取的行动

####### 典型威胁

在进一步描述风险分析之前，以下是您的 Linux 系统面临的一些典型威胁：

- **拒绝服务（DoS）：** 计算机和网络被占用，导致合法用户无法使用系统。对于企业而言，拒绝服务可能导致收入损失。
- **未授权访问：** 非授权用户使用计算机和网络。未授权用户可能会窃取信息，或恶意破坏、销毁数据。即使数据显示没有明确损坏迹象，仅凭未授权用户获得系统访问权限这一事实带来的负面 publicity 也可能伤害某些企业。
- **信息向公众披露：** 未经授权的信息公开。例如，密码文件的泄露使得潜在攻击者能够推断出访问系统的用户名和密码组合。其他敏感信息（如金融和医疗数据）的泄露可能成为企业的潜在法律责任。

####### 典型漏洞

对系统和网络的威胁来自对您组织资源（包括计算机和人员）中漏洞的利用。一些常见的漏洞包括：

- 人的失误（如泄露密码、丢失安全卡片等）
- 内部网络连接（路由器、交换机）
- 互连点（互联网与内部网络之间的网关——路由器和防火墙）
- 安全性较宽松的第三方网络提供商（ISP、长途运营商）
- 操作系统安全漏洞（如与 `sendmail`、`named`、`bind` 等相关的互联网服务器中可能存在的安全漏洞）
- 应用层安全漏洞（特定应用中已知的安全漏洞）

####### 风险分析的 1-2-3 原则（可能性与影响）

为了执行风险分析，请为每个潜在漏洞的可能性和影响赋予数值。为了建立可行的风险分析，针对每个漏洞或风险，请执行以下操作：

- 为可能性分配主观评级：低、中、高。如评级所示，低可能性意味着漏洞被利用的机会较小；高可能性意味着机会较大。
- 为影响分配类似的评级。您对影响的界定取决于您自己。如果某个漏洞的利用会对您的业务产生重大影响，请将其标记为高影响。
- 为这三个级别赋予数值——低 = 1，中 = 2，高 = 3——适用于可能性和影响。
- 将可能性乘以影响——您可以将此乘积视为风险级别。然后做出决定，为那些可能性与影响乘积超过特定阈值的漏洞开发防护措施。例如，您可以选择处理所有可能性乘以影响大于 6 的漏洞。

如果您希望以更细致的梯度来表征可能性和影响，请选择 1 到 5（例如）的刻度，而不是 1 到 3，并遵循与之前相同的步骤。

###### 建立安全策略

以风险分析以及您可能需要处理的任何业务需求（无论风险级别如何）为基础，您可以为组织制定安全策略。这样的安全策略通常涉及高层目标，例如确保数据和系统的机密性、完整性和可用性。

安全策略通常涉及以下领域：

- **身份验证：** 使用何种方法确保用户是真实用户？谁有权访问系统？密码的最小长度和复杂度是多少？用户多久更换一次密码？用户空闲多长时间后会被自动注销？
- **授权：** 不同类别的用户在系统上能执行什么操作？谁可以拥有 `root` 密码？
- **数据保护：** 哪些数据需要保护？谁有权访问这些数据？某些数据是否需要加密？
- **互联网访问：** 用户（来自局域网）访问互联网受到哪些限制？用户可以访问哪些互联网服务（如 Web、互联网中继聊天等）？是否对传入的电子邮件和附件进行病毒扫描？是否有网络防火墙？是否使用虚拟私有网络（VPN）来通过互联网连接私有网络？
- **互联网服务：** 每个 Linux 系统允许哪些互联网服务？是否有文件服务器？邮件服务器？Web 服务器？每种类型的服务器上运行哪些服务？用作桌面工作站的 Linux 系统是否运行任何服务？
- **安全审计：** 谁负责测试安全性是否充分？多久测试一次安全性？在安全测试中发现的问题如何处理？
- **事件处理：** 处理计算机安全事件的程序是什么？必须通知谁？需要收集哪些信息以帮助调查事件？
- **职责：** 谁负责维护安全？谁监控日志文件和审计追踪以发现未授权访问的迹象？谁维护安全策略？

###### 实施安全解决方案（缓解措施）

在分析了风险——即漏洞——并制定了安全策略之后，您需要选择*缓解方法*：如何防范特定的漏洞。在此处，您将根据安全策略、业务需求和可用技术来开发整体安全解决方案——该解决方案利用人员、流程和技术，并包含以下内容：

- 服务（身份验证、访问控制、加密）
- 机制（用户名/密码、防火墙）
- 对象（硬件、软件）

由于不可能保护计算机系统免受所有攻击，因此通过风险管理过程确定的解决方案必须支持整体安全计划的三个核心概念：

- *保护*：提供对策，如策略、程序和技术解决方案，以防御对受保护资产的攻击。
- *检测*：监测可能导致安全漏洞的保护措施中的潜在失效。
- *反应*或*响应*：通常需要人工参与，对检测到的违规做出反应，以便在造成损害之前挫败攻击。

由于无法实现免受攻击的绝对保护，未纳入检测和反应的安全计划是不完整的。

###### 安全管理

除了实施安全解决方案外，您还必须安装安全管理机制，持续监控、检测和响应任何安全事件。

风险分析、安全策略、安全解决方案和安全管理的结合提供了整体安全框架。这样的框架有助于建立对安全关注点的共同理解水平——以及设计和实施安全解决方案的共同基础。

###### 确保 Linux 安全

在定义了安全策略之后，您可以根据策略着手确保系统的安全。具体步骤取决于您想对系统做什么——它是服务器还是工作站，以及需要多少用户访问该系统。

为了确保 Linux 系统的安全，您必须处理两大类安全问题：

- *主机安全问题*：涉及确保操作系统以及系统上的文件和目录的安全
- *网络安全问题*：指通过网络连接发起攻击的威胁





####### 理解主机安全问题

以下是一些解决主机安全的高层指导原则。（在本小书的第 2 章中，我详细介绍了其中的一些主题。）

-   在安装 Linux 时，仅选择您的系统所需的软件包组。不要安装不必要的软件。例如，如果您的系统用作工作站，则无需安装大多数服务器（Web 服务器、新闻服务器等）。
-   创建初始用户账户，并确保所有密码都足够强大，使密码破解程序无法猜测出来。Linux 包含用于强制执行强密码的工具。
-   设置文件所有权和权限，以保护重要的文件和目录。
-   如果可用，请启用由安全增强型 Linux (SELinux) 提供的强制访问控制功能。Linux 内核 2.6 支持 SELinux。
-   使用 Gnu Privacy Guard (GnuPG) 对包含敏感信息的文件进行加密或解密，并验证从互联网下载的文件。Linux 附带 GnuPG，您可以使用 gpg 命令执行加密或解密文件以及对文件进行数字签名等任务。（有关数字签名的解释，请参阅本小书的第 2 章。）
-   使用文件完整性检查工具（例如 Tripwire）来监视关键系统文件和目录的任何更改。请访问 www.tripwire.com 获取商业版本。
-   定期检查各种日志文件，查看是否存在入侵或试图入侵的迹象。这些日志文件位于您系统的 /var/log 目录中。
-   一旦安全更新可用，请立即安装。这些安全更新修复了 Linux 中已知的漏洞。

####### 理解网络安全问题

只要您将组织的内部网络连接到互联网，安全方面的问题就会出现。即使您只将一台计算机连接到互联网，也需要考虑安全，但当整个内部网络向世界开放时，安全关注点更加紧迫。

如果您是一位经验丰富的系统管理员，您已经知道，管理互联网存在的成本并不让企业管理层担忧；他们的主要关注点是安全。为了获得管理层对网站的支持，您必须制定一个计划，以确保企业网络免受入侵者的侵害。

您可能认为，通过仅将外部服务器（如 Web 服务器和 FTP 服务器）连接到互联网，可以避免危及内部网络。然而，采用这种简单的方法是不明智的。这就像决定因为可能会发生事故而不开车一样。Web 服务器和内部网络之间没有网络连接也存在以下缺点：

-   您无法使用网络文件传输（如 FTP）将文档和数据从内部网络复制到 Web 服务器。
-   内部网络上的用户无法访问公司 Web 服务器。
-   内部网络上的用户无法访问互联网上的 Web 服务器。这种限制使得宝贵的资源——Web——对组织中的用户不可访问。

解决此问题的实用方法是设置互联网防火墙，并将 Web 服务器放在防火墙外的高安全级别主机上。

除了使用防火墙外，以下是应对网络安全的其他一些步骤。（我在本小书的第 3 章中对此进行了更详细的解释。）

-   仅在系统上启用您需要的互联网服务。特别是，不要启用未正确配置的服务。
-   使用 Secure Shell (ssh) 进行远程登录。不要使用 r 命令，如 rlogin 和 rsh。
-   保护您希望在系统上运行的任何互联网服务，如 FTP 或 TELNET。您可以使用 TCP 封装器访问控制文件——/etc/hosts.allow 和 /etc/hosts.deny——来保护其中的一些服务。（有关 TCP 封装器的更多信息，请参阅本小书的第 3 章。）
-   迅速修复您选择运行的互联网服务的任何已知漏洞。通常，您可以从您的 Linux 发行版的在线更新站点下载并安装最新的安全更新。

####### 深入探讨计算机安全术语

计算机书籍、杂志文章和计算机安全专家使用了许多具有独特含义的术语。您需要了解这些术语才能理解关于计算机安全的讨论（并有效地与安全供应商沟通）。表 1-1 描述了一些常用的计算机安全术语。

######## 表 1-1

常用的计算机安全术语

| 术语 | 描述 |
|---|---|
| 应用网关 | 充当应用层协议（如 FTP、HTTP、NNTP 和 SSH）网关的代理服务。 |
| 认证 | 确认用户确实是其声称身份的过程。典型的认证方法是挑战-响应方法，其中用户输入用户名和秘密密码以确认其身份。 |
| 后门 | 黑客放置在主机上的安全弱点，旨在绕过安全功能。 |
| 堡垒主机 | 充当组织在互联网上主要存在点的高安全计算机。堡垒主机通常驻留在边界网络上，但双宿主机（一个网络接口连接到互联网，另一个连接到内部网络）也是堡垒主机。 |
| 缓冲区溢出 | 程序中的安全缺陷，使黑客能够向该程序发送过量数据，并用发送数据中的代码覆盖正在运行的程序的部分。结果是，黑客可以在系统上执行任意代码，并可能以特权用户身份访问系统。Linux 内核的新 exec-shield 功能可防止缓冲区溢出。 |
| 证书 | 识别实体（如个人、组织或计算机）并将公钥与该身份关联的电子文档。证书包含证书持有者的姓名、序列号、到期日期、证书持有者公钥的副本以及证书机构的数字签名，以便接收者可以验证证书是真实的。 |
| 证书机构 (CA) | 验证身份并发放证书的组织。 |
| 保密性 | 数据的状态，即除了您自己（通常通过加密实现）之外，任何人都无法访问。 |
| 黑客 | 入侵（或试图入侵）主机的人，通常带有恶意意图。 |
| 解密 | 将加密信息转换回其原始、可读形式的过程。 |
| 拒绝服务 (DoS) | 一种攻击，它使用了计算机和网络上的这么多资源，以至于合法用户无法访问和使用该系统。来自单一来源的攻击用消息淹没目标计算机并阻止合法流量。它可以阻止一个系统与其他系统交换数据，或阻止系统使用互联网。 |
| 数字签名 | 消息的单向 MD5 或 SHA-1 哈希值，用消息发起者的私钥加密，用于验证消息的完整性并确保不可否认性。 |
| 分布式拒绝服务 (DDoS) | 拒绝服务攻击的一种变体，它使用分布式计算机系统的协调攻击，而不是单一来源。它通常利用蠕虫传播到多台计算机，这些计算机随后可以攻击目标。 |
| DMZ | 边界网络的另一个名称。（DMZ 最初代表非军事区，即分离朝鲜半岛和越南交战南北双方的缓冲区。） |
| 双宿主机 | 具有两个网络接口的计算机（将每个网络想象为一个家庭）。 |
| 加密 | 转换信息的过程，使其对除预期接收者以外的任何人来说都是不可理解的。该转换是通过密钥和信息之间的数学运算完成的。 |
| 利用工具 | 公开可用且复杂的工具，不同技能水平的入侵者可以使用这些工具来确定漏洞并进入目标系统。 |
| 防火墙 | 组织内部网络和互联网之间的受控访问网关。双宿主机可以配置为防火墙。 |
| 哈希 | 数学函数将消息转换为固定大小的数值（称为消息摘要或哈希值）的结果。例如，MD5 算法生成 128 位消息摘要；安全哈希算法-1 (SHA-1) 生成 160 位消息摘要。消息的哈希值用发送者的私钥加密以生成数字签名。 |
| 主机 | 网络上一台配置为向网络上其他计算机提供服务的计算机。 |
| 完整性 | 接收数据的状态，即与最初发送的相同（即传输过程中未被篡改）。 |
| IP 欺骗 | 一种攻击，其中黑客确定受信任主机的 IP 地址，然后发送看似来自受信任主机数据包。攻击者可以发送数据包，但无法看到响应。然而，攻击者可以预测数据包的序列，并基本上发送设置后门的命令，以便未来进行入侵。 |
| IPSec (IP 安全协议) | OSI 网络模型网络层的安全协议，旨在为 IP 数据包提供加密安全服务。IPSec 提供基于加密的认证、完整性、访问控制和保密性。（有关 Linux IPSec 的信息，请访问 www.ipsec-howto.org。） |
| 逻辑炸弹 | 一种破坏形式，程序员插入代码，当某些触发事件发生（如终止程序员雇佣）时，使程序执行破坏性动作。 |
| 不可否认性 | 一种安全功能，防止数据发送者否认曾经发送过数据。 |

![](img/11709a8f88c8cd03868a929dc94c0e2b_534_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_534_1.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_534_2.png)





# 5.1.0 深入探讨计算机安全术语

| 术语 | 描述 |
| --- | --- |
| **数据包** | 一组按照特定协议组装的字节，作为网络通信的基本单位。例如，在 TCP/IP 网络上，数据包有时也被称为 *IP 数据包* 或 *TCP/IP* 数据包。 |
| **数据包过滤** | 根据数据包类型（由源和目标 IP 地址或端口指定）选择性地阻止数据包。 |
| **边界网络** | 位于互联网和受保护的内部网络之间的网络。边界网络（也称为 *DMZ*）是堡垒主机所在的地方。 |
| **端口扫描** | 通过依次向端口发送连接请求来发现系统中哪些端口是开放的（换句话说，哪些 Internet 服务是启用的）的一种方法。此过程通常是进一步攻击的前奏。 |
| **代理服务器** | 位于堡垒主机上的服务器，它允许内部客户端访问外部服务器（并允许外部客户端访问受保护网络内的服务器）。存在用于各种 Internet 服务的代理服务器，例如 FTP 和 HTTP。 |
| **公钥密码学** | 一种使用密钥对——私钥和公钥——来加密和解密信息的加密方法。用公钥加密的信息只能用对应的私钥解密，反之亦然。 |
| **公钥基础设施 (PKI)** | 一套标准和服务，使能在网络环境中使用公钥密码学和证书。PKI 有助于完成诸如颁发、续期和撤销证书，以及生成和分发公钥和私钥对等任务。 |
| **筛选路由器** | 一种过滤数据包的互联网路由器。 |
| **安装程序** | 一种无论由谁运行，都以所有者权限运行的程序。例如，如果 *root* 拥有某个安装程序，则该程序具有 *root* 权限，无论谁启动了该程序。黑客经常利用安装程序中的漏洞来获取系统的特权访问权限。 |
| **嗅探器** | 与 *数据包嗅探器* 同义——一种拦截路由数据并检查每个数据包以寻找特定信息（如以明文传输的密码）的程序。 |
| **间谍软件** | 任何通过用户的 Internet 连接秘密收集用户信息并通常在后台将这些信息传输给其他人的软件。间谍软件还可以收集电子邮件地址甚至密码和信用卡号码的信息。间谍软件类似于木马，因为用户会在安装其他东西时被欺骗而安装间谍软件。 |
| **对称密钥加密** | 一种使用相同密钥来加密和解密信息的加密方法。 |
| **威胁** | 有意或无意的事件或活动，具有对系统或网络造成损害的潜力。 |
| **木马** | 一个伪装成良性程序的程序，但实际上是用于攻击系统的后门。攻击者通常会安装一组木马程序，使攻击者能够以 root 权限自由访问系统，同时向系统管理员隐藏这一事实。这种木马程序集合被称为 rootkit。 |
| **病毒** | 一种自我复制的程序，通过附着到其他程序上从一个计算机传播到另一个计算机。 |
| **漏洞** | 可能对系统或网络造成损害的缺陷或弱点。 |
| **战争拨号** | 拨打连续电话号码寻找调制解调器的简单程序。 |
| **战争驱动** | 使用笔记本电脑、天线和无线网络卡进入无线计算机网络的一种方法，涉及巡逻各个位置以获得未授权访问。 |
| **蠕虫** | 一种通过自身复制从一个计算机通过网络传播到另一个计算机的程序。 |

###### 关注安全新闻和更新

为了了解最新的安全警报，你可能希望每天访问以下一个或多个网站：

- * CERT 协调中心 (CERT/CC)，位于 `www.cert.org`
- * 计算机事件顾问能力 (CIAC)，位于 `www.ciac.org/ciac`
- * 美国计算机应急响应小组 (US-CERT)，位于 `www.us-cert.gov`

如果你可以访问 Internet 新闻组，可以定期浏览以下内容：

- `comp.security.announce`：一个经过审核的新闻组，包含来自 CERT 关于安全的公告
- `comp.security.linux`：一个包含 Linux 安全问题的讨论的新闻组
- `comp.security.unix`：一个包含 UNIX 安全问题的讨论的新闻组，包括与 Linux 相关的条目

如果你更喜欢通过电子邮件定期接收安全更新，你還可以订阅各种邮件列表：

- **FOCUS-LINUX:** 填写 www.securityfocus.com/archive 上的表格以订阅此专注于 Linux 安全问题的邮件列表。
- **US-CERT 国家网络警报系统:** 按照 www.us-cert.gov 上的说明订阅此邮件列表。网络警报系统通过其邮件列表提供四个类别的安全信息：
    - *技术性网络安全警报* 提供关于各种常见软件产品中漏洞的技术信息。
    - *网络安全警报* 在漏洞影响普通公众时发送。它们概述了非技术家庭和企业计算机用户可以采取的防护步骤和措施。
    - *网络安全公告* 是双周的安全问题和新漏洞摘要，以及补丁、变通方法和其他用户可以采取以降低风险的行动。
    - *网络安全提示* 为技术性较弱的计算机用户提供关于常见安全问题的建议。

最后，请检查你的发行版网站，查看是否有可能修复该发行版已知安全问题的更新。在 Debian、MEPIS 和 Ubuntu 中，你可以使用命令 `apt-get update` 然后 `apt-get upgrade` 来更新系统。对于 Fedora Core，网站是 http://fedorahat.net/download/updates.html。在 SUSE 中，使用 YaST Online Update 使系统保持最新。在 Xandros 中，从 Xandros Networks 获取最新更新。

##### 第 2 章：保护 Linux 主机

**本章内容**

- 保护密码
- 保护文件和目录
- 使用 GnuPG 加密和签名文件
- 监控系统安全

*主机* 是用于指代你的 Linux 系统的技术术语——特别是当你使用它在网络上提供服务时。但即使你单独看待这台计算机，这个术语也有道理；它是运行在其上的一切东西的主机：操作系统和所有应用程序。计算机安全的一个重要方面是保护主机。

在本章中，我将带你了解保护你的 Linux 主机时应遵循的几个关键步骤。这些步骤包括安装操作系统更新、保护密码、保护文件和目录、必要时使用加密以及监控系统安全。你可以通过检查日志文件中的任何可疑活动以及使用 Tripwire 工具（一个用于检测系统文件变更的优秀第三方工具）来查看是否有人对你的系统的重要文件进行了修改，从而监控主机安全。

###### 保护密码

从历史上看，UNIX 密码存储在 `/etc/passwd` 文件中，该文件任何用户都可以读取。例如，典型的旧式 *root* 用户的 `/etc/passwd` 文件条目如下所示：

```
root:t627NWDKlR8su:0:0:root:/root::/bin/bash
```

这些字段用冒号 (`:`) 分隔，第二个字段包含加密形式的密码。为了检查密码是否有效，登录程序会加密用户输入的明文密码，并将其与 `/etc/passwd` 文件的内容进行比较。如果匹配，则允许用户登录。





####### 密码破解程序

密码破解程序的工作原理与登录程序类似，不同之处在于，这些程序每次从字典中选择一个单词，对该单词进行加密，并将加密后的单词与 `/etc/passwd` 文件中存储的加密密码进行比对，寻找匹配项。为了破解密码，入侵者需要获取 `/etc/passwd` 文件。通常，破解者会利用各种 Internet 服务器（如邮件和 FTP 服务）的弱点来获取 `/etc/passwd` 文件的一份副本。

Linux 中的一些改进措施使密码变得更加安全。这些措施包括影子密码和可插拔认证模块——将在接下来的两节中描述——并且你可以在安装 Linux 时轻松安装这些功能。在安装 Linux 期间，你通常有机会配置认证方式。如果你启用了 MD5 密码和影子密码，Linux 中的密码会自动变得更加安全。

######## 影子密码

显然，让密码随意存放（即使它们是加密过的）供任何人获取，这是一种糟糕的安全实践。因此，Linux 不再将密码存储在 `/etc/passwd` 文件（该文件任何用户都可以读取）中，而是将其存储在影子密码文件 `/etc/shadow` 中。只有超级用户（*root*）可以读取此文件。例如，以下是新样式 `/etc/passwd` 文件中 *root* 的条目：

```
root::0:0::root:/bin/bash
```

在这种情况下，请注意第二个字段包含的是 `x` 而不是加密密码。`x` 是*影子密码*；实际的加密密码现在存储在 `/etc/shadow` 文件中，其中 *root* 的条目如下所示：

```
root:$1$AAAnl/VM$UESbX0py9Cgf0o1Bf0150::11077:0:99999:7:-1:-1:134540356
```

`/etc/shadow` 条目中冒号分隔字段的格式类似于 `/etc/passwd` 文件中的条目，但大多数字段的含义不同。第一个字段仍然是用户名，第二个字段是加密密码。

每个 `/etc/shadow` 条目中的其余字段控制密码何时过期。你不需要解读或更改 `/etc/shadow` 文件中的这些条目。相反，使用 *chage* 命令来更改密码过期信息。首先，你可以使用带有 `-l` 选项的 *chage* 命令来查看用户的密码过期信息，如下所示。（在这种情况下，你必须以 *root* 身份登录。）

```
chage -l root
```

此命令显示过期信息，包括密码的有效期以及更改密码的频率。

如果你希望确保用户在固定间隔内被强制更改密码，可以使用 `-M` 选项来设置密码保持有效的最大天数。例如，为了确保用户 naba 在 90 天内被提示更改密码，我以 *root* 身份登录并输入以下命令：

```
chage -M 90 naba
```

你可以对每个用户账户使用此命令，以确保所有密码在适当时候过期，并且所有用户必须选择新密码。

######## 可插拔认证模块 (PAMs)

除了使用影子密码来提高密码文件的安全性外，Linux 还通过使用 RFC 1321 (www.ietf.org/rfc/rfc1321.txt 或 www.cse.ohio-state.edu/cgi-bin/rfc/rfc1321.html) 中描述的 MD5 消息摘要算法来改进存储在 `/etc/shadow` 文件中的密码的实际加密。MD5 将任意长度的消息压缩为 128 位消息摘要（或*指纹*），这样你就可以通过使用私钥对其进行加密来对文档进行数字签名。MD5 在密码加密方面也非常好用。

MD5 相对于旧式密码加密的另一个优势是，旧密码最长限制为 8 个字符；而新密码（使用 MD5 加密）可以长得多。更长的密码更难被猜测，即使 `/etc/shadow` 文件落入错误的人手中也是如此。

你可以通过 `/etc/shadow` 文件判断 MD5 加密是否生效。加密后的密码更长，并且它们都以 `$1$` 前缀开头，如下面的示例条目中的第二个字段所示：

```
root:$1$AAAAnI/yNShuShz2Uppy9CgfKoO1BtOtSo:11077:0:99999:7:-1:-1:134540356
```

一个称为*可插拔认证模块* (PAM) 的附加程序模块执行实际的 MD5 加密。Linux PAM 提供了一种灵活的用于认证用户的方法。通过设置 PAM 的配置文件，你可以随时更改认证方法，而无需实际修改用于验证用户身份的关键程序（例如 *login* 和 *passwd*）。

Linux 广泛使用 PAM 功能。PAM 驻留在许多不同的模块中（稍后还会详细介绍）；它们的配置文件位于系统的 `/etc/pam.d` 目录中。输入以下命令即可查看系统中该目录的内容：

```
ls /etc/pam.d
```

此目录中的每个配置文件都指定了针对特定实用程序的用户认证方式。

###### 保护文件和目录

保护主机的重要方面之一是保护重要的系统文件——以及包含这些文件的目录。你可以通过文件所有权以及控制谁可以读取、写入或（对于可执行程序）执行文件的权限设置来保护文件。

默认 Linux 文件安全由每个文件或目录的以下设置控制：

- 用户所有权
- 组所有权
- 所有者的读取、写入、执行权限
- 组的读取、写入、执行权限
- 其他（所有人）的读取、写入、执行权限

####### 查看所有权和权限

当你使用 `ls -l` 命令查看详细列表时，可以看到这些设置。例如，输入以下命令以查看 `/etc/inittab` 文件的详细列表：

```
ls -l /etc/inittab
```

生成的列表看起来像这样：

```
-rw-r--r-- 1 root root 1666 Feb 16 07:57 /etc/inittab
```

第一组字符描述用户、组和其他人的文件权限。第三个和第四个字段显示拥有此文件的用户和组。在这种情况下，用户和组名称都相同：*root*。

####### 更改文件所有权

你可以使用 `chown` 命令设置用户和组的所有权。例如，如果文件 `/dev/hda` 应由用户 *root* 和组 *disk* 拥有，则作为 *root* 输入以下命令来设置此所有权：

```
chown root.disk /dev/hda
```

你也可以使用 `chgrp` 命令仅更改组所有权。例如：

```
chgrp accounting ledger.out
```

####### 更改文件权限

使用 *chmod* 命令设置文件权限。要有效地使用 *chmod*，你必须指定权限设置。一种方法是按表中所示的顺序（*谁*/*动作*/*权限*）拼接表 2-1 中每一列的一个或多个字母。

**表 2-1** | **文件权限代码**
| 谁 | 动作 | 权限 |
| :--- | :--- | :--- |
| u 用户 | + 添加 | r 读取 |
| g 组 | - 移除 | w 写入 |
| o 其他人 | = 分配 | x 执行 |
| a 所有 | s 设置用户 ID | |

若要授予所有人对目录中所有文件的读取和写入权限，请键入 `chmod a+rw *`。另一方面，若要允许所有人执行特定文件，请键入 `chmod a+x filename`。

指定权限设置的另一种方法是使用三位数字序列。在详细列表中，用户、组和其他人的读取、写入和执行权限设置显示为序列

`rw rwx rw x`

其中使用破折号表示不允许的操作。将 `rw xrwx rwx` 视为字符串 `rwx` 的三次出现。现在分配值 r=4，w=2 和 x=1。要获取序列 `rw x` 的值，只需将 r、w 和 x 的值相加。因此，`rw x` = 7。使用此公式，你可以为任何权限设置分配一个三位数值。例如，如果用户可以读取和写入文件，但其他人只能读取文件，那么权限设置是 `rw -r --r --`（这是它在列表中的显示方式），值为 644。因此，如果你希望目录中的所有文件都可以被所有人读取，但只能由用户写入，请使用以下命令：

`chmod 644 *`

###### 设置默认权限

当你（或程序）创建新文件时，文件获得什么权限设置？答案在于所谓的*用户文件创建掩码*，你可以使用 *umask* 命令来查看和设置它。




输入 **umask**，它会打印出一个数字，显示当前的文件创建掩码。*root* 用户和其他普通用户的默认设置不同。对于 *root* 用户，掩码设置为 022，而普通用户的掩码为 002。要查看此文件创建掩码的效果并解读掩码的含义，请按照以下步骤操作：

- 1. 以 *root* 身份登录并输入以下命令：

```
touch junkfile
```

此命令创建一个名为 *junkfile* 的空文件。

- 2. 输入 `ls -l *junkfile*` 以查看该文件的权限。

您会看到类似下面的一行：

```
-rw-r--r-- 1 root root 0 Aug 24 10:56 junkfile
```

通过将第一字段中（除了最开头的字母外）每组三个字母的权限转换为 0 到 7 之间的数字，来解读权限设置的数值。对于存在的每个字母，第一个字母值为 4，第二个字母为 2，第三个为 1。例如，*rw-* 转换为 4+2+0（因为缺少第三个字母），即 6。同样，*r-* 为 4+0+0 = 4。因此，权限字符串 *-rw-r--r-* 变为 644。

- 3. 从 666 中减去数值权限设置，得到的结果就是 *umask* 设置。

在此例中，666 − 644 得出 *umask* 为 022。

因此，*umask* 为 022 会导致默认的权限设置为 666 − 022 = 644。当您将 644 重新写回权限字符串时，它变为 *rw-r--r--*。

要设置新的 *umask*，请输入 **umask** 后跟掩码的数值。以下是操作方法：

- 1. 确定您希望新文件具有什么权限设置。

例如，如果您希望新文件仅允许所有者读写，其他任何人无权访问，权限设置如下所示：

```
rw-------
```

- 2. 使用转换方法将权限转换为数值，该方法将第一个字段赋值为 4，第二个赋值为 2，第三个赋值为 1。

因此，对于仅所有者可读可写的文件，权限设置为 600。

- 3. 从 666 中减去所需的权限设置，以获取掩码的值。

对于 600 的权限设置，掩码变为 666 – 600 = 066。

- 4. 使用 umask 命令设置文件创建掩码：

```bash
umask 066
```

默认的 022 umask 有利于系统安全，因为它转换为所有者拥有读写权限，其他所有人拥有只读权限的文件。归根结底，您不希望默认 umask 导致所有用户都可写的文件。

![](img/11709a8f88c8cd03868a929dc94c0e2b_544_0.png)

###### 检查设置用户 ID 权限

另一种权限设置可能构成安全隐患。这种称为设置用户 ID（简称 setuid）的权限设置适用于可执行文件。当启用 setuid 权限时，文件将以文件所有者的用户 ID 执行。换句话说，如果一个可执行程序由 root 拥有且设置了 setuid 权限，那么无论谁执行该程序，它都如同 root 在执行一样。这意味着该程序可以比普通用户程序做更多事情（例如，读取所有文件、创建新文件和删除文件）。另一个风险是，如果 setuid 程序文件存在安全漏洞，攻击者可以通过此类程序造成比其他漏洞更大的破坏。

您可以使用一个简单的 find 命令找到所有 setuid 程序：

```
find / -type f -perm +4000 -print
```

您会看到类似以下的文件列表：

```
/bin/su
/bin/ping
/bin/eject
/bin/mount
/bin/ping6
/bin/umount
/opt/kde3/bin/fileshareset
/opt/kde3/bin/artswrapper
/opt/kde3/bin/kcheckpass
... 省略的行 ...
```

许多程序拥有 setuid 权限是因为它们需要该权限，但请检查完整列表，确保没有奇怪的 setuid 程序（例如，用户主目录中的 setuid 程序）。

如果您想查看这些权限如何通过 `ls` 命令列出，请输入 `ls -l /bin/su`，您会看到权限设置：

```
-rwxr-xr-x 1 root root 2536 Aug 19 17:06 /bin/su
```

所有者权限设置（`-rwxs`）中的 `s` 告诉您 `/bin/su` 文件设置了 `setuid` 权限，这是您可以用来变为 `root` 或其他用户的 `su` 命令的可执行文件。

###### 使用 GnuPG 加密和签名文件

Linux 附带了 GNU 隐私保护程序（GnuPG 或简称为 GPG）加密和认证工具。使用 GPG，您可以创建公共密钥和私有密钥对，使用密钥加密文件，并对消息进行数字签名以验证该消息确实出自您手。如果您向拥有您公钥的人发送数字签名消息，接收者可以验证该消息确实由您签名。

####### 理解公钥加密

公钥加密的基本思想是使用一对密钥——一个私有密钥和另一个公共密钥——它们相关但不能通过其中一个猜测另一个。任何用私有密钥加密的内容只能用对应的公共密钥解密，反之亦然。公共密钥用于分发给其他人，而您需将私有密钥保存在安全的地方。

您可以使用公钥加密与他人进行安全通信；图 2-1 说明了基本思想。假设 Alice 想要向 Bob 发送安全消息。他们各自生成公钥和私钥对，之后交换他们的公钥。然后，当 Alice 想要向 Bob 发送消息时，她只需使用 Bob 的公钥加密消息并将加密消息发送给他。现在消息对任何窃听都是安全的，因为只有 Bob 的私钥才能解密消息——而只有 Bob 拥有该密钥。当 Bob 收到消息时，他使用他的私钥解密并阅读该消息。

在此时刻，您需要停下来思考并说：“等一下！Bob 如何知道消息确实来自 Alice？如果其他人使用 Bob 的公钥并假装来自 Alice 发送消息怎么办？” 这时就需要数字签名。

![](img/11709a8f88c8cd03868a929dc94c0e2b_546_0.png)

**图 2-1：**
**Bob 和 Alice 可以通过公钥加密安全通信。**

####### 理解数字签名

数字或电子签名的目的与墨笔签名相同，但数字签名的方式完全不同。与墨笔签名不同，您的数字签名取决于您正在签名的消息。创建数字签名的第一步是对消息应用一个数学函数，将其缩减为固定大小的消息摘要（也称为 *哈希* 或 *指纹*）。无论您的消息有多大，消息摘要始终约为 128 或 160 位，具体取决于哈希函数。

下一步是应用公钥加密。只需使用您的私钥加密消息摘要，就得到了该消息的数字签名。通常，数字签名附加在消息末尾，*瞧*——您就获得了一个电子签名消息。

数字签名有什么用呢？任何想要验证消息确实由您签名的人都会使用您的公钥解密数字签名。那个人得到的是消息的消息摘要（加密的哈希值）。然后，他或她对消息应用相同的哈希函数，并将计算出的哈希值与解密值进行比较。如果两者匹配，则没有人篡改过该消息。因为使用了您的公钥来验证签名，所以该消息必定是用只有您知道的私钥签名的。所以消息必定来自您！

在 Alice 向 Bob 发送私密消息的理论场景中，Alice 可以对她的消息进行数字签名，以确保 Bob 可以判断该消息确实来自她。图 2-2 说明了数字签名与普通公钥加密的结合使用。

以下是 Alice 如何向 Bob 发送她的私密消息，并让 Bob 确信该消息确实来自她：

- 1. Alice 使用软件计算消息的摘要，然后使用她的私钥加密该摘要。这是该消息的数字签名。
- 2. Alice 加密该消息（再次，使用一些方便的软件和 Bob 的公钥）。
- 3. 她将加密的消息和数字签名都发送给 Bob。
- 4. Bob 使用他的私钥解密消息。
- 5. Bob 使用 Alice 的公钥解密数字签名。这给他消息摘要。
- 6. Bob 计算消息的摘要，并将其与通过解密数字签名得到的摘要进行比较。
- 7. 如果两个消息摘要匹配，Bob 就可以确信该消息确实来自 Alice。

![](img/11709a8f88c8cd03868a929dc94c0e2b_547_0.png)

**图 2-2: Alice 可以对她的消息进行数字签名，以便 Bob 可以判断该消息确实来自她。**



####### 使用 GPG

GPG 包含了使用公钥加密和数字签名所需的工具。你使用的是 `gpg` 命令。随着你开始使用加密，你会逐渐了解如何 GPG。我将向你展示一些你可能使用 GPG 执行的典型任务。

######## 生成密钥对

生成密钥对的步骤如下：

- 1. **输入 `gpg --gen-key`**
  如果你第一次使用 `gpg`，它会在你的主目录下创建一个 `.gnupg` 目录，并在该目录下创建一个名为 `gpg.conf` 的文件。然后 GPG 会询问你想要什么类型的密钥：
  ```
  Please select what kind of key you want:
   (1) DSA and ElGamal (default)
   (2) RSA (sign only)
   (4) RSA (sign only)
  Your selection?
  ```

- 2. **按下 Enter 键选择默认选项，因为这已经足够好了。**
  然后 GPG 会提示你输入密钥大小（位数）。

- 3. **再次按下 Enter 键以接受默认的 1,024 位值。**
  GPG 会询问密钥何时过期。默认设置为永不过期。

- 4. **如果默认设置是你想要的（为什么不是呢？），按下 Enter 键。**

- 5. **当 GPG 询问你是否确实希望密钥永不过期时，按下 Y 键确认。**
  GPG 会提示你输入你的姓名、电子邮件地址，最后是一个注释，以便将密钥对与你的姓名关联起来。

- 6. **输入所需的每一部分信息并按下 Enter 键。**

- 7. **当 GPG 给你机会修改信息或确认其原样时，输入 o 并按下 Enter 键以确认。**
  接下来 GPG 会提示你输入一个保护你私钥的密码短语。

- 8. **输入一个包含小写字母、大写字母、数字和标点符号的长句——越长越好——然后按下 Enter 键。**
  请小心选择一个你容易记住的密码短语。
  GPG 生成密钥。它可能会要求你在 PC 上执行一些操作，以便随机数生成器能够为密钥生成过程产生足够的随机数。

######## 交换密钥

为了与他人通信，你必须将你的公钥交给他们。你还必须获取那些可能会给你发送消息的人（或者可能签署文件而你希望验证签名的人）的公钥。GPG 将公钥保存在你的密钥环中。（*密钥环* 只是存储在一个文件中的公钥，但把它称为密钥环听起来很好，因为现实世界中的每个人都有钥匙环，而这些在某种程度上也是钥匙，对吧？）要列出你密钥环中的密钥，输入

```
gpg --list-keys
```

要向某人发送你的公钥或将其放置在网站上，你必须将密钥导出到文件。最好的方法是将密钥放在 GPG 文档中称为 `ASCII-armored` 格式中，使用类似这样的命令：

```
gpg --armor --export naba@comcast.net > nabakey.asc
```

此命令将我的公钥以 ASCII-armored 格式（基本上看起来像乱码文本）保存在名为 `nabakey.asc` 的文件中。当然，你将电子邮件地址替换为你自己的电子邮件地址（创建密钥时使用的地址），并将输出文件名替换为其他名称。

将公钥导出到文件后，你可以将该文件邮寄给其他人，或者将其放置在网站上供其他人使用。

当你从其他人处导入密钥时，通常也会以 ASCII-armored 格式获取。例如，如果我在一个名为 `usercertkey.asc` 的文件中有一个 `us-cert@us-cert.gov` GPG 公钥（我从 `www.us-cert.gov/pgp/email.html` 的链接处获得），我使用以下命令将其导入到我的密钥环中：

```
gpg --import usercertkey.asc
```

使用 `gpg --list-keys` 命令来验证密钥是否在您的密钥环中。例如，这是我在我的系统上输入 `gpg --list-keys` 时看到的内容：

```
/home/naba/.gnupg/pubring.gpg
--------------------------------------------------
pub 1024D/7B38A728 2005-08-28
uid 2048g/3BD6D418 2005-08-28 Naba Barkakati (Author) <naba@comcast.net>
sub

pub 2048R/F8D1E87D0 2004-09-08 [expires: 2005-10-01]
uid US-CERT Operations Key <us-cert@us-cert.gov>
```

下一步是检查新密钥的指纹。我输入以下命令以获取 US-CERT 密钥的指纹：

```
gpg --fingerprint us-cert@us-cert.gov
```

GPG 打印指纹：

```
pub   2048R/F8D1E87D0 2004-09-08 [expires: 2005-10-01] 
Key fingerprint = 049F E38A 240B 4CF1 3A76  06DC 1868 F0E1 87D0 
uid     US-CERT Operations Key <us-cert@us-cert.gov>
```

在此时，你需要与 US-CERT 组织的某人核对密钥指纹。对于像 US-CERT 这样的大型组织，你可以从 US-CERT 网页（[www.us-cert.gov/pgp/encryptmail.html](http://www.us-cert.gov/pgp/encryptmail.html)）上验证指纹。我检查过了，指纹与 US-CERT 网站上显示的一致。

如果你认为密钥指纹没问题，你可以签署并验证该密钥。以下是你用来签署密钥的命令：

```
gpg --sign-key us-cert@us-cert.gov
```

GPG 要求确认，然后提示你输入你的密码短语。之后，GPG 签署该密钥。

> 由于密钥验证和签署是 GPG 中潜在的薄弱环节，请小心你要签署的密钥。通过签署密钥，你基本上表示你信任该密钥来自那个人或组织。

######## 签署文件

如果你向某人发送文件并希望确保接收者该文件未被篡改，且确实是你发送的，你可能会发现签署文件很有用。GPG 使签署文件变得非常简单。你可以使用以下命令压缩并签署名为 message 的文件：

```
gpg -o message.sig -s message
```

要验证签名，输入

```
gpg --verify message.sig
```

要获取原始文档，只需输入

```
gpg -o message --decrypt message.sig
```

有时你并不在乎保持消息的秘密，但你只是想签署它以表明消息是你发的。在这种情况下，你可以使用以下命令生成并附加一个明文签名：

```
gpg -o message.asc --clearsign message
```

此命令基本上是在文本消息末尾附加一个明文签名。这是一个典型的明文签名块：

```
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v1.4.2 (GNU/Linux)

iDEBQPDEhAtAHHLHhs4pgyrhAhigAJ3qjJ0PpMKgVfUooKyUJZAV6pERTC4fo8m
$CWkNRQhOo2DXvXK2Si18=
=2uc/
-----END PGP SIGNATURE-----
```

当消息附加了明文签名时，你可以使用 GPG 通过以下命令验证签名：

```
gpg --verify message.asc
```

如果你确实签署了该消息，输出的最后一行会说这是一个有效的签名。

######## 加密和解密文档

要为接收者加密消息，你可以使用 --encrypt（或 -e）GPG 命令。以下是如何使用其 GPG 密钥为 US-CERT 加密消息的方法：

```
gpg -o message.gpg -e -r us-cert@us-cert.gov message
```

该消息使用 US-CERT 公钥加密（没有签名，但你可以通过 -s 命令添加签名）。

当 US-CERT 接收到 message.gpg 文件时，接收者必须使用 US-CERT 的私钥对其进行解密。以下是 US-CERT 的某人可以使用的命令：

```
gpg -o message --decrypt message.gpg
```

然后 GPG 提示输入密码短语以解锁 US-CERT 私钥，解密消息，并将输出保存在名为 message 的文件中。

如果你只是想加密一个文件，而且没有人需要解密该文件，你可以使用 GPG 执行所谓的对称加密。在这种情况下，你使用以下 GPG 命令提供一个密码短语来加密文件：

```
gpg -o secret.gpg -c somefile
```

GPG 提示你输入密码短语并要求你重复密码短语（以确保你没有输错任何内容）。然后 GPG 使用从密码短语生成的密钥加密文件。

要解密使用对称密钥加密的文件，输入

```
gpg -o myfile --decrypt secret.gpg
```

GPG 提示你输入密码短语。如果你输入正确的密码短语，GPG 将解密文件并将输出（在此例中）保存在名为 `myfile` 的文件中。

###### 监控系统安全性

即使你保护了系统，你也必须定期监控日志文件以寻找入侵迹象。你可能想要使用 Tripwire 软件（一个检测系统文件任何更改的好工具），以便你可以监控关键系统文件和目录的完整性。你的 Linux 系统可能不包含 Tripwire 软件包。要使用 Tripwire，你必须从 www.tripwire.com 购买它。购买并安装 Tripwire 后，你可以配置它来监控系统上指定系统文件和目录的任何更改。

定期检查 `/var/log` 目录及其子目录中的日志文件。许多 Linux 应用程序，包括一些服务器，使用 `syslogd` 的日志功能写入日志信息。在 Linux 系统上，由 `syslogd` 写入的日志文件位于 `/var/log` 目录。确保只有 `root` 用户可以读写这些文件。

![](img/11709a8f88c8cd03868a929dc94c0e2b_552_0.png)

`syslogd` 的配置文件是 `/etc/syslog.conf`。`syslogd` 的默认配置生成必要的日志文件；但是，如果你想查看和理解配置文件，请输入 `man syslog.conf` 以获取更多信息。

![](img/11709a8f88c8cd03868a929dc94c0e2b_552_1.png)





##### 第 3 章：改进网络安全

###### 本章要点

- 保护 Internet 服务
- 使用安全外壳（SSH）进行安全的远程登录
- 设置简单的防火墙
- 在您的 Linux 系统上启用数据包过滤

为了保护您的 Linux 系统，您必须同时关注主机安全和网络安全。这两种安全类型之间的区分在某种程度上是武断的，因为保护网络涉及修复主机上与您的系统提供的 Internet 服务相关的各项配置。在本章中，我将解释如何保护 Internet 服务（主要是通过不提供不必要的服务），如何使用防火墙阻止不需要的网络数据包到达您的网络，以及如何使用安全外壳进行安全的远程登录。

###### 保护 Internet 服务

对于连接到 Internet 的 Linux 系统（甚至是位于未连接到 Internet 的 TCP/IP 局域网中的系统），一个重大威胁是有人可能利用一个或多个 Internet 服务来获取您系统的访问权限。每项服务——例如邮件、Web 或 FTP——都需要运行一个响应通过 TCP/IP 网络到达的客户端请求的服务器程序。其中一些服务器程序存在弱点，允许外部人员登录您的系统——甚至可能以 root 权限登录。幸运的是，Linux 提供了一些设施，您可以使用它们使 Internet 服务更加安全。

![](img/11709a8f88c8cd03868a929dc94c0e2b_554_0.png)

潜在的入侵者可以使用*端口扫描工具*——一种尝试在特定端口建立 TCP/IP 连接并寻找响应的程序——来检查您的系统上运行了哪些 Internet 服务器。然后，为了获取对您系统的访问权限，入侵者可能会利用一项或多项服务的已知弱点。

####### 关闭独立服务

为了提供 Web、电子邮件和 FTP 等 Internet 服务，您的 Linux 系统必须运行监听传入 TCP/IP 网络请求的服务器程序。其中一些服务器在系统启动时开始运行，并且始终处于运行状态。这些服务器被称为*独立服务器*。Web 服务器和邮件服务器是独立服务器的例子。

另一个名为 `xinetd` 的服务器会启动配置为在 `xinetd` 下运行的其他服务器。一些 Linux 系统使用 `inetd` 服务器而不是 `xinetd` 来启动其他服务器。

某些服务器可以配置为独立运行，或在 `xinetd` 等超级服务器下运行。例如，`vsftpd` FTP 服务器可以配置为独立运行，或在 `xinetd` 的控制下运行。

- **发行版特定说明：** 在 Debian、MEPIS、Ubuntu 和 Xandros 中，使用 `update-rc.d` 命令关闭独立服务器，并使用 `invoke-rc.d` 命令交互式地启动或停止服务器。要了解可用的服务，输入 `ls /etc/init.d` 并查看所有用于开启或关闭服务的脚本文件。例如，当您希望开启或关闭某个服务时，可以使用这些文件名。例如，要关闭 Samba 服务，请输入 `update-rc.d 4 samba remove`。如果服务已在运行，请输入 `invoke-rc.d samba stop` 来停止该服务。您可以以类似方式使用 `invoke-rc.d` 命令停止任何服务。

- **发行版特定说明：** 在 Fedora Core 和 SUSE 中，您可以使用 `chkconfig` 命令开启或关闭独立服务器。您可以通过输入 `ls /etc/init.d` 获取服务脚本的名称。然后，您可以通过输入 `chkconfig -del smb` 来关闭某个服务（例如 Samba）。如果服务已在运行，请输入 `/etc/init.d/smb stop` 来停止该服务。您可以通过运行 `/etc/init.d` 目录中的脚本并附带 `stop` 参数，以类似方式停止任何服务。

####### 配置 Internet 超级服务器

除了 Web 服务器或邮件服务器等独立服务器外，还有其他服务器——`inetd` 或 `xinetd`——需要单独配置。这些服务器被称为*Internet 超级服务器*，因为它们可以按需启动其他服务器。

输入 `ps ax | grep inetd` 来查看您的系统运行的是哪个 Internet 超级服务器——`inetd` 或 `xinetd`。

Debian、MEPIS、Ubuntu 和 Xandros 使用 **inetd**，而 Fedora Core 和 SUSE 使用 **xinetd**。

**inetd** 服务器通过 `/etc/inetd.conf` 文件进行配置。您可以通过找到该文件中的相应行并在那行开头添加井号（#）将其注释掉来禁用某个服务。保存配置文件后，输入 **/etc/init.d/inetd restart** 以重启 **inetd** 服务器。

配置 **xinetd** 服务器稍微复杂一些。**xinetd** 服务器在启动时读取名为 **/etc/xinetd.conf** 的配置文件。该文件反过来又引用存储在 **/etc/xinetd.d** 目录中的配置文件。**/etc/xinetd.d** 中的配置文件告诉 **xinetd** 监听哪些端口，以及为每个端口启动哪个服务器。输入 **ls /etc/xinetd.d** 以查看您系统上 **/etc/xinetd.d** 目录中文件的列表。每个文件代表 **xinetd** 可以启动的一项服务。要关闭这些服务中的任何一项，请在文本编辑器中编辑该文件，并在文件中添加一行 **disable = yes**。在对 **xinetd** 配置文件进行任何更改后，您必须重启 **xinetd** 服务器；否则，更改不会生效。要重启 **xinetd** 服务器，请输入 **/etc/init.d/xinetd restart**。此命令停止 **xinetd** 服务器，然后再次启动它。当它重启时，它会读取配置文件，并且更改将生效。

####### 配置 TCP Wrapper 安全性

**inetd** 和 **xinetd** 的一个安全特性是它们使用 **TCP wrapper** 来启动各种服务。**TCP wrapper** 是一段代码，它为 Internet 服务提供访问控制设施，就像您的消息的保护包装一样。TCP wrapper 可以启动其他服务，例如 FTP 和 TELNET；但在启动服务之前，它会查阅 **/etc/hosts.allow** 文件，查看请求服务的宿主是否被允许使用该服务。如果 **/etc/hosts.allow** 中没有关于该宿主的信息，TCP wrapper 会检查 **/etc/hosts.deny** 文件，查看是否拒绝该服务。如果两个文件都为空，TCP wrapper 将提供对请求服务的访问。

以下是收紧 **inetd** 或 **xinetd** 配置启动的服务访问权限的步骤：

1. 使用文本编辑器编辑 **/etc/hosts.deny** 文件，向该文件添加以下行：
   ```
   ALL:ALL
   ```
   此设置拒绝所有宿主访问您系统上的任何 Internet 服务。

2. 编辑 /etc/hosts.allow 文件，并添加可以访问您系统上服务的宿主名称。

   例如，要使仅 192.168.1.0 网络的宿主和本地主机（IP 地址 127.0.0.1）能够访问您系统上的服务，请将以下行放在 /etc/hosts.allow 文件中：
   ```
   ALL: 192.168.1.0/255.255.255.0 127.0.0.1
   ```

3. 如果您希望允许特定的远程宿主访问特定的 Internet 服务，您可以使用 /etc/hosts.allow 中某行的以下语法来实现：
   ```
   server_program_name: hosts
   ```
   这里，server_program_name 是服务器程序的名称，而 hosts 是可以访问该服务的宿主列表（以逗号分隔）。

   您也可以将 hosts 写为网络地址或整个域名，例如 .mycompany.com。

###### 使用安全外壳 (SSH) 进行远程登录

Linux 附带 Open Secure Shell (OpenSSH) 软件，这是一组程序，为 Berkeley r 命令提供了安全的替代方案：rlogin（远程登录）、rsh（远程 shell）和 rcp（远程复制）。OpenSSH 使用公钥密码学对用户进行身份验证，并对两台主机之间的通信进行加密，因此用户可以安全地从远程系统登录并安全地复制文件。

在本节中，我将简要描述如何在 Linux 中使用 OpenSSH 软件。要了解有关 OpenSSH 的更多信息并阅读最新新闻，请访问 www.openssh.com 或 www.openssh.org。

OpenSSH 软件在 Linux 安装期间已安装。表 3-1 列出了 OpenSSH 软件的主要组件。

表 3-1 OpenSSH 软件的组件

| 组件 | 描述 |
|---|---|
| /usr/sbin/sshd | 此 Secure Shell 守护程序必须在主机上运行，如果您希望远程系统上的用户能够使用 ssh 客户端安全登录。当来自 ssh 客户端的连接到达时，sshd 使用公钥密码学执行身份验证，并与 ssh 客户端建立加密通信链路。 |
| /usr/bin/ssh | 用户可以运行此 Secure Shell 客户端登录到运行 sshd 的主机。用户也可以使用 ssh 在另一台主机上执行命令。 |




## 使用安全 shell (SSH) 进行远程登录

| 组件 | 描述 |
| :--- | :--- |
| /usr/bin/login | 指向 /usr/bin/ssh 的符号链接 |
| /usr/bin/scp | 安全工作 like `scp` 的 secure-copy 程序。`scp` 程序使用 `ssh` 进行数据传输，并提供与 `ssh` 相同的认证和安全机制。 |
| /usr/bin/ssh-keygen | 使用此程序生成在 OpenSSH 中用于公钥密码术所需的公钥和私钥对。`ssh-keygen` 程序可以为 RSA 和 DSA（数字签名算法）认证生成密钥对。（RSA 算法的名称源自罗恩·李维斯特（Ron Rivest）、阿迪·沙米尔（Adi Shamir）和伦纳德·阿德勒曼（Leonard Adleman）——该算法开发者的姓名首字母。） |
| /etc/ssh/sshd_config | 此 `sshd` 服务器的配置文件指定了 `sshd` 的许多参数——包括监听的端口、使用的协议以及其他文件的位置。（SSH 协议有两个版本，SSH1 和 SSH2，OpenSSH 均支持这两种版本。） |
| /etc/ssh/ssh_config | 此配置文件用于 `ssh` 客户端。每个用户也可以在用户主目录的 `.ssh` 子目录中拥有一个名为 `config` 的 `ssh` 配置文件。 |

OpenSSH 使用公钥加密，其中发送方和接收方都拥有一对密钥——一个公钥和一个私钥。公钥可以自由分发，且各方都知道对方的公钥。发送方使用接收方的公钥加密数据。只有接收方的私钥才能解密该数据。

要使用 OpenSSH，首先需要启动 `sshd` 服务器，然后生成主机密钥。方法如下：

-   如果你想在主机上支持基于 SSH 的远程登录，请在你的系统上启动 `sshd` 服务器。输入 `ps ax | grep sshd` 以查看服务器是否已在运行。如果没有，请以 root 身份登录并启动 SSH 服务。
-   在 Fedora Core 和 SUSE 中，输入 `chkconfig --level 35 sshd on`。在 Debian 和 Xandros 中，输入 `update-rc.d ssh defaults`。若要立即启动 `sshd` 服务器，在 Debian 和 Xandros 中输入 `/etc/init.d/ssh start`，或在 Fedora Core 和 SUSE 中输入 `/etc/init.d/ssh start`。

使用以下命令生成主机密钥：

```
ssh-keygen -d -f /etc/ssh/ssh_host_key -N ''
```

`-d` 标志使 `ssh-keygen` 程序生成 DSA 密钥，这是 SSH2 协议所使用的。如果你看到一条消息说文件 `/etc/ssh/ssh_host_key` 已经存在，这意味着密钥对在 Linux 安装过程中已生成。你可以使用现有文件，而无需重新生成密钥。

![](img/11709a8f88c8cd03868a929dc94c0e2b_558_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_558_1.png)

希望使用 SSH 登录的用户可以简单地使用 ssh 命令。例如，这是我在一个系统上输入以通过 SSH 登录到另一个系统的命令：

```
ssh 192.168.0.4 -l naba
```

其中 192.168.0.4 是另一个 Linux 系统的 IP 地址。然后 SSH 显示一条消息：

> 无法确定主机 '192.168.0.4 (192.168.0.4)' 的真实性。
> RSA 密钥指纹为 7b:79:f2:d3:8c:54:00:a6:94:ec:fa:8e:7f:c9:ad:66。
> 你确定要继续连接吗 (yes/no)？

我输入 yes 并按 Enter。然后 SSH 将该主机添加到其已知主机列表，并提示我输入另一个 Linux 系统的密码：

```
naba@192.168.0.4's password:
```

输入密码后，我即与该系统建立了安全的登录会话。我也可以使用以下等效命令登录到此账户：

```
ssh naba@192.168.0.4
```

如果我只想从局域网（LAN）上的另一个系统（由其 IP 地址 192.168.0.4 标识）安全地复制文件，可以这样使用 scp：

```
scp 192.168.0.4:/etc/X11/xorg.conf .
```

此命令提示输入我的密码，并将 /etc/X11/xorg.conf 文件从 192.168.0.4 主机安全地复制到输入 scp 命令的系统，如下所示：

```
naba@192.168.0.4's password: (我输入密码。)
xorg.conf             100% 2814      2.8KB/s   00:00
```

###### 设置简单防火墙

防火墙是一个具有两个或更多网络接口的网络设备或主机——一个连接到受保护的内部网络，另一个连接到未受保护的网络（如互联网）。防火墙控制对受保护内部网络的访问。

如果你将内部网络直接连接到互联网，你必须确保内部网络上的每个系统都已得到妥善保护——这几乎是不可能做到的，因为一个疏忽的用户就可能导致整个内部网络变得脆弱。防火墙是通往互联网的单点连接：你可以将全部努力集中在使该防火墙系统成为未经授权的外部用户难以逾越的屏障。本质上，防火墙就像一道保护性围栏，阻止不受 want 的外部数据和软件进入，并防止敏感的内部数据和软件流出。（参见图 3-1。）

![](img/11709a8f88c8cd03868a929dc94c0e2b_560_0.png)

防火墙运行软件以检查到达其网络接口的网络数据包，并根据一组规则采取适当的操作。其思想是定义这些规则，以便只允许授权的网络流量在两个接口之间流动。配置防火墙涉及正确设置规则。一种配置策略是拒绝所有网络流量，然后仅允许有限的一组网络数据包通过防火墙。授权的网络流量包括内部用户执行诸如访问网站和接收电子邮件等操作所必需的连接。

要发挥作用，防火墙具有以下一般特征：

-   它必须控制互联网和内部网络之间的数据包流动。
-   它不得提供动态路由，因为动态路由表易受路由欺骗攻击——入侵者使用假路由。相反，防火墙使用静态路由表（你可以在 Linux 系统上使用 route 命令设置）。
-   它必须不允许任何外部用户以 root 身份登录。这样，即使防火墙系统被攻破，入侵者也会被阻止从远程登录使用 root 权限。
-   它必须放置在物理安全的位置。
-   它必须区分来自互联网的数据包和来自受保护内部网络的数据包。此功能允许防火墙拒绝那些来自互联网但具有内部网络上可信系统 IP 地址的数据包。
-   它充当内部网络的 SMTP 邮件网关。设置 sendmail 软件，使所有传出邮件看起来都来自防火墙系统。
-   其用户账户仅限于少数几个账户，供需要访问外部系统的内部用户使用。需要访问内部网络的外部用户应使用 SSH 进行远程登录（参见本章前面关于 SSH 的讨论）。
-   它保留所有系统活动的日志，例如成功和失败的登录尝试。
-   它向外部世界提供 DNS 名称查找服务，以解析外部世界已知的主机名。
-   它提供良好的性能，以免阻碍内部用户访问特定的互联网服务（如 HTTP 和 FTP）。

防火墙可以采取许多不同的形式。以下是防火墙的三种常见形式：

-   **数据包过滤防火墙**：这种简单的防火墙使用能够根据数据包的各种特征进行过滤（阻止或允许）的路由器，这些特征包括源和目的 IP 地址、网络协议（TCP 或 UDP）以及源和目的端口号。数据包过滤防火墙通常放置在不可信网络的最外层边界，并构成第一道防线。数据包过滤防火墙的一个示例是部署过滤规则以筛选网络流量的网络路由器。

数据包过滤防火墙快速且灵活，但它们无法阻止利用特定应用程序漏洞或功能的攻击。它们只能记录最少量信息，如源 IP 地址、目的 IP 地址和流量类型。此外，它们易受利用 TCP/IP 协议内缺陷的攻击和漏洞利用，例如 IP 地址欺骗，即修改网络数据包中的地址信息，以使数据包看起来来自可信的 IP 地址。

-   **状态检测防火墙**：在这种情况下，防火墙跟踪网络应用程序正在使用的网络连接。当内部系统上的应用程序使用网络连接与远程系统建立会话时，内部系统上的一个端口也会打开。此端口接收来自远程系统的网络流量。对于成功的连接，数据包过滤防火墙必须允许来自远程系统的传入数据包。向传入流量开放许多端口会增加未经授权的入侵者滥用诸如 TCP 等网络协议的预期惯例的风险。状态检测防火墙



####### 配置简单防火墙

通过创建一个出站网络连接表来解决此问题，该表包含每个会话对应的内部端口。然后使用此“状态表”来验证任何传入的数据包。这种有状态检查比数据包过滤器更安全，因为它会单独跟踪内部端口，而不是为外部访问打开所有内部端口。

- **应用代理网关防火墙。** 这种防火墙作为内部应用程序（尝试与外部服务器（如 Web 服务器）通信）之间的中介。例如，Web 代理接收来自防火墙内部运行的 Web 浏览器客户端的外部 Web 页面请求，并将它们中继到外部 Web 服务器，就好像防火墙是发起请求的 Web 客户端一样。外部 Web 服务器响应防火墙，然后防火墙将响应转发给内部客户端，就好像防火墙是 Web 服务器一样。内部客户端主机从未与外部 Web 服务器建立直接的网络连接。

应用代理网关防火墙相比数据包过滤器防火墙和有状态检查防火墙有一些优势。首先，应用代理网关防火墙会检查整个网络数据包，而不仅仅检查网络地址和端口。这使得这些防火墙能够提供比数据包过滤器或有状态检查防火墙更广泛的日志记录功能。另一个优势是，应用代理网关防火墙可以直接对用户进行身份验证，而数据包过滤器防火墙和有状态检查防火墙通常基于系统 IP 地址（即源、目的地址和协议类型）对用户进行身份验证。鉴于网络地址很容易被伪造，应用代理网关防火墙的身份验证能力优于数据包过滤器和有状态检查防火墙。

然而，应用代理网关防火墙的高级功能与数据包过滤器或有状态检查防火墙相比，也带来了一些缺点。首先，由于应用代理网关中存在 **完整数据包感知**，防火墙被迫花费大量时间读取和解释每个数据包。因此，应用代理网关防火墙通常不适用于高带宽或实时应用程序。为了减轻防火墙的负载，可以使用专用代理服务器来保护对时间敏感性要求较低的服务，如电子邮件和大多数 Web 流量。另一个缺点是，应用代理网关防火墙在支持新的网络应用程序和协议方面往往受到限制。对于每种需要穿过防火墙的网络流量类型，都需要一个独立的、专门针对该应用的代理代理。大多数应用代理网关供应商提供通用代理代理，以支持未定义的网络协议或应用程序。然而，这些通用代理代理往往会抵消应用代理网关架构的许多优势，并简单允许流量 *隧道* 穿过防火墙。

![](img/11709a8f88c8cd03868a929dc94c0e2b_562_0.png)

大多数防火墙都实现了这些防火墙功能的组合。例如，许多数据包过滤器防火墙或有状态检查防火墙的供应商也实施了基本的应用代理功能，以弥补其防火墙相关的某些弱点。在大多数情况下，这些供应商实施应用代理以提供更好的网络流量日志记录和更强的用户身份验证。几乎所有主要防火墙供应商都以某种方式在其产品中引入了多种防火墙功能。

![](img/11709a8f88c8cd03868a929dc94c0e2b_563_0.png)

在大型组织中，您可能还需要将较小的内部网络与公司网络隔离。您可以按照设置互联网防火墙的方式设置这些内部防火墙。

####### 使用 NAT

网络地址转换（NAT）是一种有效工具，它允许您 *隐藏* 防火墙后内部网络的地址。本质上，NAT 允许组织在防火墙后使用私有网络地址，同时仍然保持通过防火墙连接外部系统的能力。

有三种实现 NAT 的方法：

- **静态：** 在静态 NAT 中，私有网络上的每个内部系统都有一个与之关联的相应外部可路由 IP 地址。这种特定技术很少被使用，因为唯一 IP 地址供应短缺。
- **隐藏：** 通过隐藏 NAT，防火墙后的所有系统共享同一个外部可路由 IP 地址，而内部系统使用私有 IP 地址。因此，使用隐藏 NAT 时，防火墙后的一批系统看起来仍像是单个系统。
- **端口地址转换：** 通过端口地址转换，可以将主机放置在防火墙系统后面，并仍然使外部用户可以选择性地访问它们。

就优缺点而言，每种类型的 NAT —— 静态、隐藏或端口地址转换 —— 都适用于某些特定情况；变量是每种类型提供的设计灵活性程度。静态 NAT 提供最大的灵活性，但由于 IP 地址短缺，它并不总是实用的。隐藏 NAT 技术很少被使用，因为端口地址转换提供了额外的功能。端口地址转换通常是最方便且安全的解决方案。

####### 在 Linux 系统中启用数据包过滤

您的 Linux 系统内置了数据包过滤软件，形式为 Linux 内核中的 netfilter。您只需要使用 iptables 命令来设置规则，根据数据包报头中的 IP 地址和网络连接类型来决定数据包的命运。

![](img/11709a8f88c8cd03868a929dc94c0e2b_564_0.png)

若要了解有关 netfilter 和 iptables 的更多信息，请访问 netfilter 网站（www.netfilter.org/documentation）的文档部分。

当您的 Linux 系统和互联网之间没有专用防火墙时，内置的数据包过滤功能非常方便。例如，当您通过 DSL 或电缆调制解调器将 Linux 系统连接到互联网时，就是这种情况。本质上，您可以在 Linux 系统内部拥有一个数据包过滤防火墙，位于内核和应用之间。

###### 使用安全级别配置工具

一些 Linux 发行版，如 Fedora Core 和 SUSE，包含图形用户界面（GUI）工具，用于启用数据包过滤防火墙。

![](img/11709a8f88c8cd03868a929dc94c0e2b_564_1.png)

在 Fedora Core 中，您可以通过图形化安全级别配置工具来开启不同级别的数据包过滤。要运行该工具，请以 root 用户登录并选择“系统 -> 管理 -> 安全级别和防火墙”。安全级别配置对话框会出现，如图 3-2 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_564_2.png)

在安全级别配置对话框中的“防火墙选项”选项卡（参见图 3-2）中，您可以使用安全级别配置工具选择两个预定义的简单防火墙（更准确地说，是数据包过滤）级别：

- **禁用：** 不执行任何过滤，允许所有连接。（您仍可以通过不运行服务器或在 `xinetd` 配置文件中禁用它们来关闭互联网服务。）如果您的 Linux 系统位于受保护局域网内，或者您有单独的防火墙设备，此安全级别即可满足需求。
- **启用：** 开启数据包过滤。然后您可以选择想要允许的服务以及您信任的网络设备。

您可以允许发给特定互联网服务（如 SSH、TELNET 和 FTP）的传入数据包。如果您选择一个网络接口（如 `eth0`（第一个以太网卡））作为受信任的，则该接口上的所有网络流量都将不受任何过滤而允许通过。

Fedora Core 的安全级别配置工具还有另一个选项卡——SELinux 选项卡（参见图 3-2）——它允许您开启或关闭由 SELinux 提供的强制访问控制。

在 SUSE 中，要设置防火墙，请选择“主菜单 -> 系统 -> 控制中心 (YaST)”。在出现的 YaST 控制中心窗口中，点击窗口左侧的“安全和用户”，然后点击右侧的“防火墙”。YaST 将打开一个窗口（见图 3-3），您可以使用它来配置防火墙。

**特定于发行版**

![](img/11709a8f88c8cd03868a929dc94c0e2b_565_0.png)




###### 安全性：改进网络

####### 使用 iptables 命令

从第一个屏幕（参见图 3-3），你可以指定防火墙是否在系统启动时启动，也可以启动、停止或重启防火墙。要配置防火墙的其他方面（例如允许通过防火墙的服务），请单击左侧的分类，并指定该分类所需的设置。你可以将网络接口（按设备名称，如 eth0、ppp0 等）指定为以下三个区域之一：内部、外部或非军事区。然后，对于该区域，你可以指定允许的服务（例如 HTTP、FTP 和 SSH）。如果你有多个网络接口，并且使用 Linux 系统作为网关（路由器），你可以启用在网络接口之间转发数据包（称为伪装的一项功能）。你还可以开启不同级别的日志记录（例如，记录所有尝试在特定端口连接的被丢弃数据包）。如果你修改了防火墙设置，请单击“Startup”（启动）分类，然后单击“Save Settings and Restart Firewall Now”（保存设置并立即重启防火墙）。

图形用户界面（GUI）防火墙配置工具使用 *iptables* 命令来实现防火墙。如果你的 Linux 系统没有图形工具，你可以直接使用 *iptables* 来配置 Linux 系统的防火墙。本节将向你介绍 *iptables*。

使用 *iptables* 命令有点复杂。*iptables* 使用*链*（chain）的概念，它是一系列规则的序列。每条规则说明如何处理数据包（如果报头包含特定信息（例如源或目标 IP 地址））。如果某条规则不适用，*iptables* 将参考链中的下一条规则。默认情况下，有三条链：

- **INPUT 链：** 数据包被测试的第一组规则。只有当 INPUT 链未指定 DROP（丢弃）或 REJECT（拒绝）时，数据包才会继续到下一条链。
- **FORWARD 链：** 包含适用于试图通过此系统到达另一系统的数据包的规则（例如，当你使用 Linux 系统作为局域网和互联网之间的路由器时）。
- **OUTPUT 链：** 包含在数据包发送前应用的规则（无论是发送到其他网络还是应用程序）。

图 3-4 展示了 IP 数据包如何通过 *iptables* 的这三条链进行处理的高层描述。

当入站数据包到达时，内核使用 *iptables* 基于数据包的目标 IP 地址做出路由决策。如果数据包是发给这台服务器的，内核会将数据包传递给 INPUT 链。如果数据包满足 INPUT 链中的所有规则，则该数据包将由本地进程（例如监听此类型数据包的网络服务器）进行处理。

![](img/11709a8f88c8cd03868a929dc94c0e2b_567_0.png)

> **图 3-4：** *iptables* 处理链的简化视图。

如果内核启用了 IP 转发，且数据包的目标 IP 地址属于另一个网络，内核会将数据包传递给 FORWARD 链。如果数据包满足 FORWARD 链中的规则，它将被发送到其他网络。如果内核未启用 IP 转发且数据包的目标地址不是发给这台服务器，数据包将被丢弃。

如果接收输入数据包的本地处理程序想要发送出站数据包，这些数据包将经过 OUTPUT 链。如果 OUTPUT 链接受这些数据包，它们将被发送到指定的目标网络。

你可以使用 *iptables* 命令查看当前链、向现有链添加规则或创建新的规则链。当你查看当前链时，也可以将它们保存到文件中。例如，如果你没有做其他任何操作，且你的系统没有配置防火墙，输入 **iptables -L** 应该显示以下内容：

```text
Chain INPUT (policy ACCEPT)
target     prot opt source           destination
Chain FORWARD (policy ACCEPT)
target     prot opt source           destination
Chain OUTPUT (policy ACCEPT)
target     prot opt source           destination
```

在这种情况下，所有三条链 —— INPUT、FORWARD 和 OUTPUT —— 都显示相同的 ACCEPT（接受）策略，这意味着一切都是敞开的。

如果你正在设置数据包过滤器，你要做的第一件事是指定你要接受的数据包。例如，要接受来自 192.168.0.0 网络地址的数据包，请向 INPUT 链添加以下规则：

```text
iptables -A INPUT -s 192.168.0.0/24 -j ACCEPT
```

现在添加一条规则，除了本地回环（lo 网络接口）流量外，丢弃一切并停止所有转发，使用以下命令：

```text
iptables -A INPUT -i ! lo -j REJECT
iptables -A FORWARD -j REJECT
```

例如，第一个 iptables 命令向 INPUT 链（-A INPUT）追加一条规则：如果数据包不是来自 lo 接口（-i ! lo），iptables 将拒绝该数据包（-j REJECT）。

在拒绝所有其他数据包之前，你还可以为每个 INPUT 链添加更多规则以允许特定数据包进入。你可以基于许多不同的参数（例如 IP 地址、协议类型（TCP、UDP）、网络接口和端口号）选择要接受或拒绝的数据包。

你可以使用 iptables 进行各种专门的数据包过滤。例如，假设你设置了一个 Web 服务器，并且你只想接受用于 HTTP（端口 80）和安全 Shell（SSH）服务的数据包。安全 Shell 服务（端口 22）用于你安全地登录和管理服务器。假设服务器的 IP 地址是 192.168.0.10。以下是你为此服务器设置规则的方式：

```text
iptables -P INPUT DROP
iptables -A INPUT -s 0/0 -d 192.168.0.10 -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -s 0/0 -d 192.168.0.10 -p tcp --dport 22 -j ACCEPT
```

在这种情况下，第一条规则将 INPUT 链的默认策略设置为 DROP（丢弃），这意味着如果没有特定的规则匹配，数据包将被丢弃。接下来的两条规则说明，地址为 192.168.0.10 且面向端口 80 和 22 的数据包将被接受。

不要从远程登录会话中键入 iptables 命令。一条开始拒绝来自所有地址数据包的规则也可能阻止你键入的内容到达系统；如果发生这种情况，你可能无法通过网络访问系统。为了避免不愉快的意外，始终在控制台键入 iptables 规则——即直接连接到运行数据包过滤器的 Linux PC 的键盘和显示器。如果你希望紧急删除所有过滤规则，请输入 **iptables -F** 以清除它们。要将 INPUT 链（参见图 3-4）的默认策略更改为 **ACCEPT**，请输入 **iptables -I filter -P INPUT ACCEPT**。这会导致 **iptables** 默认接受所有入站数据包。

本节不提供 **iptables** 命令的所有细节。只需知道，你可以输入 *man iptables* 来阅读命令摘要。你也可以在 **www.iptables.org** 上阅读关于 **netfilter** 和 **iptables** 的内容。

在你使用 **iptables** 命令定义规则后，它们位于内存中，并且在系统重启时消失。使用 *iptables-save* 命令将规则存储到文件中。例如，你可以使用以下命令将规则保存到一个名为 *iptables.rules* 的文件中：

```text
iptables-save > iptables.rules
```

以下是 *iptables.rules* 文件的列表，由 Fedora Core 系统生成：

```text
# Generated by iptables-save v1.3.0 on Sun Aug 28 16:10:12 2005
#filter
:FORWARD ACCEPT [0:0]
:INPUT ACCEPT [0:0]
:OUTPUT ACCEPT [6:636]
-A FORWARD -j REJECT --reject-with icmp-port-unreachable
-A INPUT -s 192.168.0.0/255.255.255.0 -j ACCEPT
-A INPUT -i lo -j REJECT --reject-with icmp-port-unreachable
COMMIT
# Completed on Sun Aug 28 16:10:12 2005
```

如果你好奇的话，这些规则对应于我用于配置过滤器的以下 **iptables** 命令：

```text
iptables -A INPUT -s 192.168.0.0/24 -j ACCEPT
iptables -A INPUT -i ! lo -j REJECT
iptables -A FORWARD -j REJECT
```

如果你希望将这些保存的规则加载到 **iptables** 中，请使用以下命令：

```text
iptables-restore < iptables.rules
```

除非你直接使用 **iptables** 命令配置防火墙，否则防火墙配置的具体细节取决于你的 Linux 发行版提供的用于设置防火墙的 GUI 实用程序。例如，SUSE 防火墙实用程序将 INPUT 和 FORWARD 链（参见图 3-4）的默认策略从 **ACCEPT** 更改为 **DROP**，这意味着在该情况下




##### 第四章：执行计算机安全审计

本章内容

- 理解计算机安全审计
- 学习安全测试方法论
- 审查主机和网络安全性
- 探索安全测试工具

看到 *审计* 这个词，你可能会想到税务审计，对吧？其实有很多不同类型的审计，其中一种就是 *计算机安全审计*。计算机安全审计的基本目的，就是测试你的系统和网络安全。对于大型组织而言，独立的审计员（类似于财务报表审计那样）可以执行安全审计。如果你只有几台 Linux 系统或一个小型网络，你可以将安全审计作为自我评估来进行，以确定你是否正确地处理了所有事项。

在本书中，我将解释如何执行计算机安全审计，并展示一些免费工具和资源，帮助你测试系统的安全性。

###### 理解安全审计

*审计* 很简单，就是对所审计对象的独立评估。因此，*计算机安全审计* 就是计算机安全的独立评估。如果有人对你所在组织进行计算机安全审计，他或她通常关注两个领域：

- 独立验证你的组织是否遵守现有的计算机安全政策和程序。这是安全审计的非技术方面。
- 独立测试你的安全控制措施（任何你用来保护系统安全的硬件和软件机制）的有效性。这是安全审计的技术方面。

为什么需要安全审计？原因和你需要财务审计相同——主要是为了核实一切是否按预定方式运行。对于公共和私营组织，管理层可能希望进行独立的安全审计，以确保其安全无虞。无论你的组织规模大小，你都可以自行进行安全审计，要么为接受独立安全审计做准备，要么只是为了确认自己是否正确地处理了所有事项。

无论你是进行独立安全审计还是自我评估，安全审计都能带来以下一些好处：

- 考虑系统和数据面临的内部和外部威胁的定期风险评估
- 对安全政策、安全控制措施和技术的定期测试
- 识别系统安全性中的任何重大缺陷（以便你知道该修复什么）
- 在自我评估的情况下，为组织可能不得不面对的任何年度独立安全测试做准备

####### 安全审计的非技术方面

计算机安全审计的非技术方面关注你组织范围内的安全框架。审计检查组织在制定和实施计算机安全的政策、计划和程序方面做得如何。需要核实的一些项目包括：

- 证明风险经过定期评估。
- 实体范围内的安全项目计划的存在。
- 已经建立了安全项目管理系统结构。
- 计算机安全责任分配清晰。
- 实施了有效的与人员安全相关的政策。
- 监控安全项目的有效性，并在必要时进行调整。

正如你所料，安全审计的非技术方面涉及审查文档以及采访相关人员，以了解组织是如何管理计算机安全的。当然，对于小组织或家庭 PC，期望在文档中看到计划和程序是荒谬的。在这种情况下，你只需要确保已部署某些技术控制措施来保护系统和网络连接即可。

###### 安全审计的技术方面

计算机安全审计的技术方面侧重于测试保护主机和网络的技术控制措施。测试内容包括确定：

- **主机的安全状况如何。** 所有操作系统补丁是否已安装？文件权限设置是否正确？用户账号是否受到保护？是否监控文件变更？是否监控日志文件？等等。
- **网络的安全状况如何。** 不必要的互联网服务是否已关闭？是否安装防火墙？远程登录是否使用 SSH 等工具保护？是否使用 TCP wrapper 访问控制？等等。

通常，安全专家使用自动化工具对单个主机和整个网络执行这两项安全审查。

###### 实施安全测试方法论

计算机安全审计的一个关键要素是安全测试，它检查用于保护主机和网络的技术机制。安全测试方法论遵循以下高层步骤：

1. 清点组织的网络、主机、网络设备（路由器、交换机、防火墙等）和互联网连接。
2. 如果存在许多主机和网络连接，确定哪些是需要测试的重要主机和网络设备。主机的重要性取决于其运行的应用程序类型。例如，运行公司数据库的主机比充当桌面系统的主机更重要。
3. 单独测试每个主机。通常，此步骤涉及以系统管理员身份登录，检查主机安全的各个方面，从密码到系统日志文件。
4. 测试网络。此步骤通常通过尝试从互联网上的另一个系统突破网络防御来完成。如果存在防火墙，测试会检查防火墙是否确实配置正确。
5. 分析主机和网络测试的结果，确定漏洞和风险。

主机和网络这两种测试类型都关注构成整体计算机安全的三个领域：

- **预防：** 包括帮助防止系统或网络遭受攻击的机制（非技术和技术机制）
- **检测：** 指监控日志文件、检查文件完整性以及使用入侵检测系统等技术，这些系统可检测有人即将或已经入侵你的系统
- **响应：** 包括计算机安全事件发生后执行诸如向当局报告事件以及从备份恢复重要文件等任务的步骤

对于主机和网络安全，这三个领域之间存在一定重叠。例如，主机安全的预防措施（如良好的密码或文件权限）也能提供网络安全。尽管如此，这仍然是有用的。

然而，在思考预防措施之前，你必须了解你试图预防的问题类型。换言之，常见的安全漏洞是什么？预防和控制措施通常取决于这些漏洞。

###### 一些常见的计算机漏洞

主机和网络安全的特定测试取决于常见的漏洞。其基本思想是检查主机或网络是否存在黑客利用的漏洞。

###### 关于计算机漏洞的在线资源

多个在线资源识别并分类计算机安全漏洞：

- **SANS 学院** 在 www.sans.org/top20 发布一份互联网安全十大最严重漏洞列表。
- **CVE**（常见漏洞和暴露）是一个标准化的漏洞名称列表。有关 CVE 的更多信息，请参阅 http://cve.mitre.org。（列表包含超过 7,200 个唯一漏洞名称。）使用 CVE 名称描述漏洞是常见做法。
- **国家漏洞数据库（NVD）** 是由美国政府机构美国国家标准与技术研究院（NIST）发布的关于计算机漏洞信息的一个可搜索索引。NVD 在线地址为 http://nvd.nist.gov。截至 2005 年 9 月 28 日，NVD 列出了近 12,700 个漏洞，并为每个漏洞提供了漏洞公告和补丁信息的链接。





###### 典型的 20 大计算机漏洞

SANS Top 20 互联网安全漏洞列表包含几种类型的漏洞，例如 Windows、跨平台以及 UNIX。其中，UNIX 和跨平台漏洞与 Linux 相关。表 4-1 总结了一些适用于 Linux 的常见 UNIX 和跨平台漏洞。你可以在 www.sans.org/top20 阅读关于这些漏洞的完整详细信息。

####### 表 4-1 UNIX 系统的一些常见漏洞

| 漏洞类型 | 描述 |
| --- | --- |
| BIND DNS | 伯克利互联网名称域 (BIND) 是一个实现域名系统 (DNS) 的包，DNS 是将名称转换为 IP 地址的互联网命名服务。某些版本的 BIND 存在漏洞。 |
| Apache Web 服务器 | 某些 Apache Web 服务器模块（例如 mod_ssl）存在已知漏洞。Web 服务器用于处理交互式 Web 页面的通用网关接口 (CGI) 程序中的任何漏洞都可能为攻击者提供访问系统的方式。 |
| 身份验证 | 用户帐户通常没有密码或使用了容易被密码破解程序破解的弱密码。 |
| CVS、Subversion | 并发版本控制系统 (CVS) 是 Linux 系统中流行的源代码控制系统。Subversion 是另一个在 Linux 中日益流行的版本控制系统。这些版本控制系统存在漏洞，可能被攻击者利用在系统上执行任意代码。 |
| sendmail | sendmail 是一个复杂的程序，用于将邮件消息从一个系统传输到另一个系统，某些版本的 sendmail 存在漏洞。 |
| SNMP | 简单网络管理协议 (SNMP) 用于远程监控和管理各种网络连接系统，范围从路由器到计算机。SNMP 缺乏良好的访问控制，因此如果 SNMP 在你的系统上运行，攻击者可能会重新配置或关闭你的系统。 |
| 开放安全套接字层 (OpenSSL) | 许多应用程序（如 Apache Web 服务器）使用 OpenSSL 为网络连接提供加密安全保护。不幸的是，某些版本的 OpenSSL 存在已知漏洞，可被利用。 |
| 网络文件系统 (NFS) 和网络信息服务 (NIS) | NFS 和 NIS 都存在许多安全问题（例如，缓冲区溢出、潜在的拒绝服务攻击风险以及弱身份验证）。此外，NFS 和 NIS 经常被错误配置，这可能允许本地和远程用户利用安全漏洞。 |
| 数据库 | MySQL 和 PostgreSQL 等数据库是复杂的应用程序，难以正确配置和安全加固。这些数据库具有许多功能，可能被误用或利用，以破坏数据的保密性、可用性和完整性。要了解对 MySQL 的一些常见攻击以及如何防御它们，请参考此论文：www.nextgenss.com/papers/HackprooftingMySQL.pdf。 |
| Linux 内核 | Linux 内核容易受到许多漏洞的影响，例如拒绝服务、执行任意代码以及对系统的 root 级别访问。 |

###### 主机安全审查

在审查主机安全时，重点关注评估以下每个领域的安全机制：

- **预防：** 安装操作系统更新，设置安全密码，改进文件权限，为引导加载程序设置密码，并使用加密
- **检测：** 捕获日志消息，并使用 Tripwire（一种可检测系统文件变化的工具）检查文件完整性
- **响应：** 进行例行备份并制定事件响应程序

我将在接下来的章节中介绍其中一些主机安全机制。

####### 操作系统更新

Linux 发行版在发现安全漏洞后会尽快发布更新。许多发行版提供在线更新，你可以启用并使用它们来保持系统最新。更新操作系统的具体细节取决于发行版。有关如何在线更新 Linux 的信息，请参阅第五卷第四章。

####### 文件权限

使用适当的文件所有权和文件权限保护关键系统文件。分配文件系统所有权和权限的关键步骤如下：

- 弄清楚哪些文件包含敏感信息以及原因。某些文件可能包含与你的工作或业务相关的敏感数据，而许多其他文件之所以敏感是因为它们控制 Linux 系统配置。
- 维护一份经过授权的用户列表及其在系统上被授权执行的操作。
- 设置密码、组、文件所有权和文件权限，以允许仅授权用户访问文件。

表 4-2 列出了 Linux 中一些重要的系统文件，显示了每个文件的数字权限设置。（有关数字权限设置的更多信息，请参阅本小书的第二章。）

######## 表 4-2 重要的系统文件及其权限

| 文件路径名 | 权限 | 描述 |
| :--- | :--- | :--- |
| /boot/grub/menu.lst | 600 | GRUB 引导加载程序菜单文件 |
| /etc/cron.allow | 400 | 允许使用 cron 提交定期作业的用户列表 |
| /etc/cron.deny | 400 | 不允许使用 cron 提交定期作业的用户列表 |
| /etc/crontab | 644 | 系统范围的定期作业 |
| /etc/hosts.allow | 644 | 允许使用 TCP wrappers 启动的互联网服务的hosts列表 |
| /etc/hosts.deny | 644 | 拒绝访问使用 TCP wrappers 启动的互联网服务的hosts列表 |
| /etc/logrotate.conf | 644 | 控制日志文件轮转的文件 |
| /etc/pam.d | 755 | 可插拔身份验证模块 (PAM) 的配置文件目录 |
| /etc/passwd | 644 | 旧式密码文件，包含用户帐户信息但不包含密码 |
| /etc/rc.d | 755 | 系统启动脚本目录 |
| /etc/securetty | 600 | root 可以登录的 TTY 接口（终端） |
| /etc/security | 755 | 控制系统访问的策略文件 |
| /etc/shadow | 400 | 包含加密密码和密码过期信息的文件 |
| /etc/shutdown.allow | 400 | 可以通过按 Ctrl+Alt+Delete 关机或重启的用户 |
| /etc/ssh | 755 | 安全外壳 (SSH) 的配置文件目录 |
| /etc/sysconfig | 755 | 系统配置文件 |
| /etc/sysctl.conf | 644 | 内核配置参数 |
| /etc/syslog.conf | 644 | 记录消息的 syslogd 服务器的配置文件 |
| /etc/udev/udev.conf | 644 | udev 的配置文件——一个提供动态命名热插拔设备并在 /dev 目录中创建设备文件能力的程序 |
| /etc/vsftpd | 600 | 非常安全的 FTP 服务器的配置文件 |
| /etc/vsftpd.ftpusers | 600 | 不允许使用 FTP 传输文件的用户列表 |
| /etc/xinetd.conf | 644 | xinetd 服务器的配置文件 |
| /etc/xinetd.d | 755 | 包含 xinetd 服务器可以启动的特定服务配置文件的目录 |
| /var/log | 755 | 包含所有日志文件的目录 |
| /var/log/lastlog | 644 | 关于所有先前登录的信息 |
| /var/log/messages | 644 | 主要系统消息日志文件 |
| /var/log/wtmp | 664 | 关于当前登录的信息 |

另一个重要检查是查找具有 setuid 权限的可执行程序文件。如果一个程序具有 setuid 权限并由 root 拥有，那么无论实际是谁在运行该程序，该程序都以 root 权限运行。你可以使用以下 find 命令找到所有 setuid 程序：

```
find / -perm +4000 -print
```

你可能希望将输出保存到文件中（只需在命令后添加 > *filename*），然后检查文件中是否有不寻常的 setuid 程序。例如，用户主目录中的 setuid 程序是不寻常的。

###### 密码安全

验证密码、组和 shadow 密码文件是否受保护。特别是，shadow 密码文件必须是写保护的，并且只能由 *root* 读取。文件名及其推荐权限如表 4-3 所示。

####### 表 4-3 密码文件的所有权和权限

| 文件路径名 | 所有权 | 权限 |
| :--- | :--- | :--- |
| /etc/group | root.root | 644 |
| /etc/passwd | root.root | 644 |
| /etc/shadow | root.root | 400 |




###### 事件响应

**事件响应**是用于回答“如果系统确实发生了异常情况该怎么办”这一问题的策略；它告诉您如果有人入侵您的系统时应如何操作。

您对事件响应的处理取决于您如何使用该系统，以及该系统对您或您的业务有多重要。为了实现全面的事件响应，请记住以下关键点：

- 查明您的计算机和网络有多关键和重要，并确定哪些人或资源可以帮助您保护您的系统
- 采取措施以预防和最小化潜在的损坏和中断
- 制定并记录一份全面的应急计划
- 定期测试应急计划，并视情况修改程序

###### 网络安全审查

**网络安全审查**专注于评估以下各个领域中的安全机制：

- **预防：** 设置防火墙，启用数据包过滤，禁用不必要的 `inetd` 或 `xinetd` 服务，关闭不需要的 Internet 服务，使用 TCP wrappers 进行访问控制，并使用 SSH 进行安全的远程登录。
- **检测：** 使用网络入侵检测并捕获系统日志。
- **响应：** 制定事件响应程序。

我将在以下三个小节中简要描述评估网络安全的几个关键步骤。

####### 由 inetd 或 xinetd 启动的服务

根据您的发行版，`inetd` 或 `xinetd` 服务器可能被配置为启动某些 Internet 服务，如 TELNET 和 FTP。开启这些服务的决定取决于系统如何连接到 Internet 以及系统的使用方式等因素。通常，您可以关闭大多数 `inetd` 和 `xinetd` 服务。

Debian、MEPIS、Ubuntu 和 Xandros 使用 `inetd` 来启动某些服务。查看 `/etc/inetd.conf` 文件以了解 `inetd` 被配置为启动哪些服务。您可以通过注释掉 `/etc/inetd.conf` 中的行来关闭服务——只需在行首添加一个井号（#）。

![](img/11709a8f88c8cd03868a929dc94c0e2b_580_0.png)

Fedora Core 和 SUSE 使用 xinetd 作为按需启动其他 Internet 服务的服务器。要了解哪些 xinetd 服务已关闭，请检查 `/etc/xinetd.d` 目录中的配置文件，查找所有包含 `disable = yes` 行的配置文件。（如果该行在行首添加了 # 而被注释掉，则该行不算数。）您可以为任何想要关闭的服务的配置文件中添加一行 `disable = yes`。

还要检查以下文件，以查看用于 `inetd` 或 `xinetd` 服务的任何访问控制：

- `/etc/hosts.allow` 列出被允许访问特定服务的主机。
- `/etc/hosts.deny` 列出被拒绝访问服务的主机。

####### 独立服务

许多服务，如 apache 或 httpd（Web 服务器）和 sendmail（邮件服务器），假设它们被配置为在此时启动，则会在启动时自动运行。

在 Fedora Core 和 SUSE 中，您可以使用 `chkconfig` 命令来检查哪些独立服务器被设置为在 various run levels 下启动。（有关 run levels 的更多信息，请参阅第五卷，第一章。）通常，您的 Fedora Core 或 SUSE 系统会在运行级别 3（用于文本登录）或 5（用于图形登录）下启动。因此，重要的是级别 3 和 5 中服务器的设置。要查看服务器列表，请输入 `chkconfig -list | more`。在对您的网络安全进行自我评估时，如果您发现某些服务器不应运行，您可以通过输入 `chkconfig --level 35 servicename off` 来关闭它们在运行级别 3 和 5 下的运行，其中 `servicename` 是您要关闭的服务的名称。

在某些发行版中，您可以使用 GUI 工具来查看在任何运行级别下启用和正在运行的服务。在 Fedora Core 中，选择 系统→管理→服务器设置→服务。在 SUSE 中，选择 主菜单→系统→控制中心 (YaST)，然后单击窗口左侧的 System 和右侧的 Runlevel Editor。

在审核网络安全时，记下所有已开启的服务器——然后根据您对系统的了解，尝试确定它们是否真的应该开启。开启特定服务的决定取决于系统的使用方式（例如，作为 Web 服务器或桌面系统）以及它如何连接到 Internet（例如，通过防火墙或直接连接）。

####### 渗透测试

![](img/11709a8f88c8cd03868a929dc94c0e2b_582_0.png)

渗透测试是确定 Linux 系统上实际运行哪些服务的最佳方式。*渗透测试*涉及从攻击者的角度尝试访问您的系统。通常，您从 Internet 上的某个系统执行此测试，并尝试查看您是否能入侵，或者至少获取对运行在您的 Linux 系统上的服务的访问权限。

在笔记本电脑上运行的 Knoppix 非常适合执行渗透测试，因为 Knoppix 是一个 Live CD 发行版，捆绑了 *nmap* 和 Nessus 等扫描工具。您只需从 Knoppix CD 启动，就可以准备进行渗透测试。

渗透测试的一个方面是查看您的 Linux 系统上哪些端口是开放的。*端口号* 只是一个用于识别与系统的 TCP/IP 网络连接的数字。只有当该端口上运行有服务器（或者换一种说法，如果有一个服务器“正在该端口上监听”）时，尝试连接端口的行为才会成功。如果服务器在收到该端口的连接请求时做出响应，则认为该端口是开放的。

渗透测试的第一步是执行端口扫描。术语 *端口扫描* 描述了一种自动化的过程，即尝试连接每个端口号，以查看是否有有效响应返回。许多可用的自动化工具可以执行端口扫描——您可以安装并使用一种名为 *nmap* 的流行端口扫描工具（我将在本章后面对其进行描述）。

执行端口扫描后，您将知道哪些端口确实是开放的，并且可能被利用。并非所有服务器都有安全问题，但许多服务器存在众所周知的漏洞。开放的端口为黑客提供了一条通过其中一个服务器攻击您系统的途径。事实上，您可以使用称为 *漏洞扫描器* 的自动化工具来识别系统中存在的漏洞。（我将在以下几个部分中介绍一些漏洞扫描器。）无论您的 Linux 系统是直接连接到 Internet（通过 DSL 或电缆调制解调器）还是通过防火墙，请使用端口扫描和漏洞扫描工具来查明您的防御是否有任何漏洞。被您发现总比被他们发现好！

###### 探索安全测试工具

有许多自动化工具可用于执行安全测试。其中一些工具旨在查找 IP 地址范围内每个系统上的开放端口。其他工具查找与开放端口相关的漏洞。还有其他工具可以捕获（或 *嗅探*）这些弱点，并帮助您分析它们，以便您可以获取有关网络中正在发生的事情的有用信息。

您可以在 www.insecure.org/tools.html 浏览前 75 种安全工具的列表（基于对 nmap 用户的一次非正式调查）。表 4-4 按类别列出了这些工具中的一部分。我将在接下来的几个部分中描述一些免费提供的漏洞扫描器。

**表 4-4 一些流行的计算机安全测试工具**

| 类型 | 工具名称 |
| :--- | :--- |
| 端口扫描器 | nmap, Strobe |
| 漏洞扫描器 | Nessus Security Scanner, SAINT, SARA, Whisker (CGI 扫描器), ISS Internet Scanner, CyberCop Scanner, Vetescan, Retina Network Security Scanner |
| 网络工具 | Netcat, hping2, Firewall, Cheops, ntop, ping, ngrep, AirSnort (802.11 WEP 加密破解工具) |
| 主机安全工具 | Tripwire, Isof |
| 数据包嗅探器 | tcpdump, Ethereal, dsniff, sniffit |
| 入侵检测系统 (IDS) | Snort, Abacus portsentry, scanlogd, NFR, LIDS |
| 密码检查工具 | John the Ripper, LC4 |
| 日志分析和监控工具 | logcollector, tcpdstats, nlog, logcheck, LogWatch, Swatch |

####### nmap

**nmap**（**网络映射器** 的缩写）是一种端口扫描工具。它可以快速扫描大型网络，并确定网络上有哪些可用主机，它们提供什么服务，运行什么操作系统（以及操作系统版本），使用什么类型的数据包过滤器或防火墙，以及数十种其他特征。您可以在 www.insecure.org/nmap 阅读更多关于 nmap 的信息。

![](img/11709a8f88c8cd03868a929dc94c0e2b_583_0.png)

如果尚未安装，您可以轻松地在您的发行版上安装 nmap。Fedora Core 和 Knoppix 自带 nmap。在 Debian、MEPIS 和 Ubuntu 中，您可以使用命令 `apt-get install nmap` 安装它。在 SUSE 中，在 YaST 控制中心 — 主菜单 系统 控制 (YaST) 的软件类别中，点击 安装和移除软件 — 并使用 YaST 的软件搜索功能找到并安装 nmap。在 Xandros 中，您可以使用 `apt-get install nmap` 命令；运行 Xandros Networks 后，选择 编辑 设置 应用程序源，并点击 Debian Unsupported Site 链接作为源。




如果你想使用 `nmap` 扫描你的局域网，只需输入类似以下内容的命令（将 IP 地址范围替换为你的网络中合适的地址）：

```
nmap -O -sS 192.168.0.4-8
```

以下是该命令的典型输出列表：

```
Starting nmap 3.81 ( http://www.insecure.org/nmap/ ) at 2005-08-28 16:20 EDT
Interesting ports on 192.168.0.4:
(The 1659 ports scanned but not shown below are in state: closed)
PORT STATE SERVICE
21/tcp open ftp
22/tcp open ssh
111/tcp open rpcbind
631/tcp open ipp
MAC Address: 00:C0:49:63:78:3A (U.S. Robotics)
Device type: general purpose
Running: Linux 2.4.X|2.5.X|2.6.X
OS details: Linux 2.4.18 - 2.6.7
Uptime 9.919 days (since Thu Aug 18 18:18:15 2005)
... Lines deleted ...
Nmap finished: 5 IP addresses (5 hosts up) scanned in 30.846 seconds
```

如你所见，`nmap` 显示了开放端口的名称，并对操作系统名称和版本号进行了猜测。

####### Nessus

Nessus 安全扫描器是一个模块化的安全审计工具，它使用用 Nessus 脚本语言编写的插件来测试各种网络漏洞。Nessus 采用客户端/服务器软件架构，其中服务器称为 nessusd，客户端称为 nessus。

Knoppix 已随系统附带了 Nessus，因此你无需下载或安装任何内容。若要启动 Nessus，请选择 主菜单→系统→安全→NESSUS Security Tool。

要安装 Nessus，首先尝试使用你的 Linux 发行版通常用于安装新软件包的方法。在 Debian、MEPIS 和 Ubuntu 中，输入 `apt-get install nessus` 来安装包。在 SUSE 中，从 YaST 控制中心（主菜单→系统→控制中心（YaST））的软件类别中点击“安装和删除软件”，并使用 YaST 的搜索功能查找 nessus 软件包。选中软件包并点击“接受”以安装它们。在 Xandros 中，选择 编辑→设置应用程序源，并点击“Debian Unsupported Site”链接作为源。然后输入 `apt-get install nessus` nessusd。

![](img/11709a8f88c8cd03868a929dc94c0e2b_584_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_584_1.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_585_0.png)

对于 Fedora Core，你需要从 www.nessus.org/download/ 下载 Nessus 并安装它。在尝试安装 Nessus 之前，你必须安装 sharutils RPM。该软件包包含 Nessus 安装脚本所需的 uudecode 实用工具。sharutils 软件包未随 Fedora Core 的任何标准软件包组一起安装，因此你需要自行安装。要安装 sharutils，请挂载随附的 DVD 并使用以下命令进行安装：

```
cd /media/cdrom/Fedora/RPMS
rpm -ivh sharutils*.rpm
```

要下载并安装 Nessus，请遵循以下步骤。（这些说明适用于所有 Linux 发行版。）

1. 在 www.nessus.org/download 上，选择要下载的 Nessus 版本。对于 Linux 系统，请下载 Nessus 2.2.5 安装程序。
2. 输入以下命令以安装 Nessus。（必须已安装开发工具，包括 The GIMP Toolkit。）

   ```
   sh nessus-installer-2.2.5.sh
   ```

   响应安装脚本的提示以完成安装。通常可以按 Enter 键接受默认选项。

安装完成后，遵循以下步骤使用 Nessus。（在 Knoppix 中，选择 主菜单→系统→安全→NESSUS Security Tool，然后转到步骤 8。）

3. 以 root 身份登录并输入以下命令，以创建用于 Nessus 客户端和 Nessus 服务器之间安全通信的 Nessus SSL 证书：

   ```
   nessus-mkcert
   ```

4. 提供所需的信息以完成证书生成过程。
5. 使用以下命令创建 nessusd 账户：

   ```
   nessusd-adduser
   ```

6. 在提示时，输入你的用户名、密码和任何规则。（如果你不知道要输入什么规则，请按 Ctrl+D。）然后按 Y 键。
7. 如果需要，你可以通过编辑配置文件 `/usr/local/etc/nessus/nessusd.conf` 来配置 nessusd。

   如果你想试用 Nessus，可以使用默认配置文件继续操作。
8. 使用此命令启动 Nessus 服务器：

   ```
   nessusd -D
   ```

9. 在终端窗口中输入以下命令来运行 Nessus 客户端：

   ```
   nessus
   ```

   将出现 Nessus 设置窗口。
10. 输入 nessusd 用户名和密码，并点击“登录”按钮。
11. 当 Nessus 显示用于建立安全连接的证书并询问你是否接受时，点击“是”。

    客户端连接到服务器后，“登录”按钮会变为“登出”，其左侧会出现一个“已连接”标签。

    nessusd 提供了一个选项，用于启用可以扫描特定漏洞的插件，但其中一些可能会使主机崩溃并在扫描期间干扰你的网络。如果你想试用任何插件，请选中并启用它们。如果你希望安全起见，请点击“启用除危险插件外的所有插件”链接。
12. 点击“目标选择”选项卡，并输入一个 IP 地址范围以扫描网络中的所有主机。

    例如，要扫描私有网络 192.168.0.0/24 中的前八台主机，请将该地址输入为：

    ```
    192.168.0.0/29
    ```

    不要使用 Nessus 扫描你不拥有的任何网络。扫描其他网络通常是违法的，如果你违反了适用法律，可能会产生严重后果。
13. 点击“开始扫描”。

    Nessus 开始扫描 IP 地址并检查许多不同的漏洞。进度条显示扫描的状态。

    在 Nessus 完成主机漏洞扫描后，它将以图形和文本格式的良好组合显示结果。该报告是交互式的——你可以选择一个主机地址查看该主机的报告，你可以深入了解特定漏洞以查找详细信息，例如标识该漏洞的 CVE 编号以及该漏洞的描述。

## 第七卷

### 互联网服务器

Rich Tennant 的《第五波》

![](img/11709a8f88c8cd03868a929dc94c0e2b_588_0.png)

> 我马上就到。让我先处理一下这个用户。他正在完成一个 3 小时的下载，进度大概已过半。

#### 内容速览

1. 第 1 章：管理互联网服务...565
2. 第 2 章：运行 Web 服务器 ...583
3. 第 3 章：设置 FTP 服务器 ...607
4. 第 4 章：管理邮件和新闻服务器 ...613
5. 第 5 章：管理 DNS ...639
6. 第 6 章：使用 Samba 和 DNS...661

##### 第 1 章：管理互联网服务

###### 本章内容

- 理解互联网服务
- 通过 inetd 或 xinetd 控制服务器
- 使用 chkconfig 或 update-rc.d 管理服务器
- 使用 GUI 实用工具配置服务在启动时运行

互联网是一个客户端和服务器并存的世界。客户端向服务器发出请求，服务器响应这些请求。例如，你的 Web 浏览器是一个客户端，它从 Web 服务器下载信息并显示给你。当然，客户端和服务器是在各种各样的计算机上运行的计算机程序。Linux 系统是运行各种服务器的理想系统——从 Web 服务器到 Windows 文件和打印服务器。在本章中，我概述了典型的互联网服务、其客户端/服务器架构以及在 Linux 中如何管理服务器。你可以使用本章的信息来管理在你的 Linux 系统上运行的任何服务器。

###### 理解互联网服务

互联网服务是旨在将信息从一个系统传递到另一个系统的网络应用程序。在设计上，每个互联网服务都由两部分组成——一个提供信息的服务器和一个或多个请求信息的客户端。

这种客户端/服务器架构是构建分布式信息系统最常见的方式。客户端和服务器是运行在这些计算机上并通过网络通信的计算机程序。巧妙之处在于，你可以在桌面计算机上运行客户端，并访问世界上任何地方（只要它在互联网上）的服务器上运行的信息。




Web 本身、电子邮件和 FTP（文件传输协议）是采用客户端/服务器模型的 Internet 服务的示例。例如，当您使用 Web 时，您使用 Web 浏览器客户端从 Web 服务器下载并查看 Web 页面。

![](img/11709a8f88c8cd03868a929dc94c0e2b_591_0.png)

客户端/服务器体系结构要求客户端与服务器进行通信。这正是*传输控制协议*/*互联网协议*——TCP/IP——发挥作用的地方。TCP/IP 为客户端和服务器交换数据包提供了一种标准方式。在接下来的几个部分中，我将解释基于 TCP/IP 的服务如何通信。

####### TCP/IP 和套接字

Web 和 FTP 等客户端/服务器应用程序使用 TCP/IP 在客户端和服务器之间进行数据传输。这些 Internet 应用程序通常使用利用*伯克利套接字接口*的 TCP/IP 通信（该名称源于伯克利 UNIX 在 1982 年左右引入的套接字接口）。套接字接口并非物理实体——它只是计算机程序员可用于创建能与 Internet 上其他应用程序通信的应用程序的一些计算机代码。

![](img/11709a8f88c8cd03868a929dc94c0e2b_591_1.png)

即使您不使用套接字编写网络应用程序，您可能也必须使用或配置许多网络应用程序。了解套接字可以帮助您理解基于网络的应用程序如何工作，这反过来有助于您查找并纠正这些应用程序中的任何问题。

######## 套接字定义

网络应用程序使用套接字在 TCP/IP 网络上进行通信。*套接字*表示连接的一个端点。由于套接字是双向的，因此可以通过它发送和接收数据。套接字有三个属性：

- 系统的*网络地址*（IP 地址）
- *端口号*，标识通过套接字交换数据的进程（*进程*是在计算机上运行的计算机程序）
- *套接字类型*，标识用于数据交换的协议

本质上，IP 地址标识网络上的计算机（主机）；端口号标识节点上的进程（服务器）；套接字类型决定了数据交换的方式——通过面向连接（流）或无连接（数据报）协议。

########## 面向连接的协议

套接字类型指示用于通过套接字通信的协议。面向连接的协议就像普通的电话对话。当您想与朋友交谈时，您必须拨打朋友的电话号码并在开始对话之前建立连接。同样，面向连接的数据交换要求发送和接收进程在开始数据交换之前建立连接。

在 TCP/IP 协议族中，TCP——*传输控制协议*——支持 Internet 上两台计算机上运行的两个进程之间的面向连接的数据传输。TCP 提供进程之间可靠的双向数据交换。

正如 TCP/IP 的名称所暗示的那样，TCP 依赖 IP——*互联网协议*——进行数据包传输。IP 不保证数据包被交付，也不保证数据包按特定顺序交付。然而，IP 确实能高效地将数据包从一个网络移动到另一个网络。TCP 负责将数据包按正确顺序排列，检测是否发生错误，并在发生错误时请求重传数据包。

TCP 适用于旨在一次交换大量数据的应用程序。此外，需要可靠数据交换的应用程序使用 TCP。（例如，FTP 使用 TCP 传输文件。）

在套接字模型中，使用 TCP 的套接字被称为*流套接字*。

########## 无连接协议

*无连接*数据交换协议不要求发送方和接收方显式建立连接。这就像在拥挤的房间里朝朋友大喊——您无法确定朋友是否听到了您。

在 TCP/IP 协议族中，*用户数据报协议*（UDP）为发送和接收称为*数据报*的数据包提供无连接服务。与 TCP 不同，UDP 不保证数据报最终到达其预期目的地。UDP 也不保证数据报按发送顺序交付。

UDP 用于一次交换少量数据的应用程序，或者用于不需要数据交付可靠性和顺序性的应用程序。例如，SNMP（简单网络管理协议）使用 UDP 传输数据。

在套接字模型中，使用 UDP 的套接字被称为*数据报套接字*。

####### 套接字和客户端/服务器模型

需要两个套接字来完成通信路径。当两个进程通信时，它们使用客户端/服务器模型建立连接。图 1-1 说明了这一概念。服务器应用程序监听系统上的特定端口——服务器完全由运行它的系统的 IP 地址和它监听连接的端口号标识。客户端从任何可用端口发起连接，并尝试连接服务器（由 IP 地址和端口号标识）。当连接建立后，客户端和服务器可以根据各自的协议交换数据。

![](img/11709a8f88c8cd03868a929dc94c0e2b_593_0.png)

基于套接字的数据交换中的事件序列取决于传输是面向连接的（TCP）还是无连接的（UDP）。

对于使用套接字的面向连接的数据传输，服务器在特定端口上监听，等待客户端请求连接。只有在建立连接后，数据传输才开始。

对于无连接数据传输，服务器等待数据报到达指定端口。客户端不等待建立连接；它只是将数据报发送给服务器。

无论是服务器还是客户端，每个应用程序首先创建一个套接字。然后它将套接字**关联**（绑定）到本地计算机的 IP 地址和一个端口号。IP 地址标识机器（应用程序运行的位置），端口号标识使用套接字的应用程序。

> **请记住**
> 服务器通常监听一个众所周知的端口号，以便客户端可以连接到该端口以访问服务器。对于客户端应用程序，将套接字绑定到 IP 地址和端口的过程与服务器相同，但客户端可以使用 0 作为端口号——套接字库会自动为客户端使用一个未使用的端口号。

对于面向连接的流套接字，通信的客户端和服务器应用程序必须建立连接。建立连接的具体步骤取决于应用程序是服务器还是客户端。

> **请记住**
> 在客户端/服务器模型中，服务器必须在客户端运行之前启动并运行。在创建套接字并将套接字绑定到端口之后，服务器应用程序设置一个连接队列，这决定了有多少客户端可以连接到服务器。通常，服务器监听一到五个连接。然而，监听队列的大小是您可以调整的参数之一（特别是对于 Web 服务器），以确保服务器响应尽可能多的客户端。在设置好监听队列后，服务器等待来自客户端的连接。

从客户端建立连接相对简单。在创建套接字并将套接字绑定到 IP 地址之后，客户端与服务器建立连接。为了建立连接，客户端必须知道服务器的主机名或 IP 地址，以及服务器接受连接的端口。所有 Internet 服务都有众所周知的标准端口号。

> **技术细节**
> 在客户端通过面向连接的流套接字与服务器建立连接之后，客户端和服务器可以通过调用相应的套接字 API 函数交换数据。就像两个人之间的对话一样，服务器和客户端交替发送和接收数据——数据的含义取决于服务器和客户端使用的消息协议。通常，服务器是为特定任务设计的；该设计中固有服务器和客户端用于交换必要数据的消息协议。例如，Web 服务器和 Web 浏览器（客户端）使用 HTTP（超文本传输协议）进行通信。





####### 互联网服务与端口号

TCP/IP 协议套件是互联网的*通用语言*，因为互联网服务*使用* TCP/IP。这些服务通过实现邮件、新闻和网页的传输，驱动着互联网的运转。每种互联网服务都有其自身的协议，这些协议依赖 TCP/IP 来实际传输信息。每种服务还拥有一个或多个分配的端口号，用于执行其设计功能。以下是一些常见的互联网服务及其相关协议：

- **DHCP（动态主机配置协议）** 用于动态配置计算机上的 TCP/IP 网络参数。DHCP 主要用于分配动态 IP 地址以及其他网络信息，如名称服务器、默认网关和用于配置 TCP/IP 网络所需的域名。DHCP 服务器监听 67 端口。
- **FTP（文件传输协议）** 用于在互联网上的计算机之间传输文件。FTP 使用两个端口：数据通过 20 端口传输，控制信息通过 21 端口交换。
- **HTTP（超文本传输协议）** 用于将一个系统的文档发送到另一个系统。HTTP 是万维网（Web）的基础协议。默认情况下，Web 服务器和客户端通过 80 端口进行通信。
- **SMTP（简单邮件传输协议）** 用于在系统之间交换电子邮件。SMTP 使用 25 端口进行信息交换。
- **NNTP（网络新闻传输协议）** 用于以存储转发方式在互联网上分发新闻文章。NNTP 使用 119 端口。
- **SSH（安全外壳协议）** 是一种用于在不安全网络上进行安全远程登录及其他安全网络服务的协议。SSH 使用 22 端口。
- **TELNET** 允许一个系统上的用户登录到互联网上的另一个系统。（用户必须提供有效的用户 ID 和密码才能登录远程系统。）TELNET 默认使用 23 端口。但是，TELNET 客户端可以连接到任何指定的端口。
- **NFS（网络文件系统）** 用于在计算机之间共享文件。NFS 使用 Sun 的远程过程调用（RPC）机制，该机制通过 111 端口交换信息。
- **NTP（网络时间协议）** 用于客户端计算机将系统时间与拥有更精确时钟的服务器进行同步。NTP 使用 123 端口。
- **SNMP（简单网络管理协议）** 用于管理互联网上的所有类型网络设备。与 FTP 一样，SNMP 使用两个端口：161 和 162。
- **TFTP（特快文件传输协议）** 用于将一个系统上的文件传输到另一个系统。（它通常被 X 终端和无盘工作站用于从网络上的另一个主机下载启动文件。）TFTP 数据传输发生在 69 端口。

每种服务都由一个*服务器进程*提供——这是一个运行在系统上的计算机程序，等待到达与其服务相关的知名端口的客户端请求。因此，Web 服务器期望在 80 端口（HTTP 服务的标准端口）接收到客户端请求。

Linux 系统上的 /etc/services 文本文件存储了服务名称与端口号（以及协议）之间的关联。以下是 Linux 系统 /etc/services 文件中条目的一小部分示例：

| 服务 | 端口/协议 | 别名/注释 |
| :--- | :--- | :--- |
| ftp-data | 20/tcp | |
| ftp | 21/tcp | |
| fspd | 21/udp | fspd |
| ssh | 22/tcp | # SSH 远程登录协议 |
| ssh | 22/udp | |
| telnet | 23/tcp | |
| smtp | 25/tcp | mail |
| time | 37/tcp | timeserver |
| time | 37/udp | timeserver |
| rhp | 39/udp | resource # 资源定位 |
| nameserver | 42/tcp | isc # IEN 116 |
| whois | 43/tcp | nicname |
| tacacs | 49/tcp | tacacs # 登录主机协议 (TACACS) |

快速浏览 /etc/services 文件中的条目，即可了解 TCP/IP 下可用网络服务的广度。

> 注意：80 端口被指定用于 Web 服务。换句话说，如果在你的系统上设置了 Web 服务器，该服务器将监听 80 端口。顺便提一下，IANA——互联网号码分配机构（www.iana.org）——是负责协调 1,024 以下端口号分配的组织。

###### 使用互联网超级服务器

互联网服务的客户端/服务器架构要求，在客户端发出服务请求之前，服务器必须已启动并正在运行。让所有服务器始终处于运行状态可能是一个糟糕的主意——因为不切实际，每个服务器进程都会以内存和处理器的时间形式消耗系统资源。此外，你并不真的需要所有服务始终处于就绪状态。解决这个问题的一个聪明方法是运行一个单一服务器，该服务器监听所有端口，当客户端请求到来时再启动相应的服务器。这种服务器被称为*互联网超级服务器*，因为它按需启动各种服务。

![](img/11709a8f88c8cd03868a929dc94c0e2b_596_0.png)

有两种互联网超级服务器——*inetd* 和 *xinetd*。*inetd* 服务器是较旧的一个，仍被某些 Linux 发行版使用，如 Debian、Knoppix、MEPIS、Ubuntu 和 Xandros。*xinetd* 服务器是 *inetd* 的替代品，提供了改进的访问控制和日志记录功能。名称 *xinetd* 代表*扩展的 inetd*。Fedora Core 和 SUSE 等发行版使用 *xinetd*。

####### 使用 inetd

在使用 *inetd* 的 Linux 发行版中，系统会在启动时启动 *inetd*。*inetd* 服务器在启动时读取名为 `/etc/inetd.conf` 的配置文件。此文件告知 *inetd* 监听哪些端口以及为每个端口启动哪个服务器。例如，在我的一个 Linux 系统上，启动 IMAP（互联网消息访问协议）服务器的 `/etc/inetd.conf` 文件条目如下所示：

```
imaps stream tcp nowait root /usr/sbin/tcpd /usr/sbin/imapd
```

此行中的第一项 `imaps` 告诉 *inetd* 服务的名称。*inetd* 使用此名称从 `/etc/services` 文件中查找端口号。如果你输入 `grep imaps /etc/services`，你会发现 IMAP 服务的端口号是 993。这告诉 *inetd* 监听 993 端口以处理 IMAP 服务请求。

IMAP 条目中其余字段的含义如下：

- 条目的第二和第三字段 `stream` 和 `tcp` 告诉 *inetd* 该服务使用面向连接的 TCP 套接字与客户端通信。对于使用无连接 UDP 套接字的服务，这两个字段应写为 `dgram` 和 `udp`。
- 第四个字段 `nowait` 告诉 *inetd* 为每个请求启动一个新的服务器。如果该字段写为 `wait`，*inetd* 将在服务器退出前等待，然后再重新启动服务器。
- 第五个字段提供了 *inetd* 用于运行服务器的用户 ID。在这种情况下，服务器以 `root` 身份运行。
- 第六个字段指定了为该服务运行的程序，最后一个字段是 *inetd* 传递给服务器程序的参数。在这种情况下，`/usr/sbin/imapd` 作为参数提供给 `/usr/sbin/tcpd` 程序。

`/usr/sbin/tcpd` 程序是互联网服务的访问控制机制——称为 **TCP wrapper**。由于不必要的互联网服务往往是安全漏洞的来源，你可能希望关闭任何不需要的服务，或至少控制对这些服务的访问。`tcpd` 程序可以启动其他服务，如 IMAP 和 TELNET，但在启动服务之前，`tcpd` 会查阅 `/etc/hosts.allow` 文件，查看请求服务的宿主是否被允许访问该服务。如果 `/etc/hosts.allow` 中没有关于该宿主的信息，tcpd 会检查 `/etc/hosts.deny` 文件，查看是否应拒绝该服务。如果两个文件都为空，tcpd 将允许宿主访问请求的服务。你可以在 `/etc/hosts.deny` 文件中放置 **ALL:ALL** 这一行，以拒绝所有宿主访问任何互联网服务。

浏览你系统上的 `/etc/inetd.conf` 文件，以了解 inetd 被设置为启动的服务类型。如今，大多数 inetd 服务都被关闭了，而许多其他服务（如 FTP）则由独立服务器启动。无论如何，如果你发现任何想要关闭的服务，只需在启动这些服务的行首添加一个井号（#）。当你对 `/etc/inetd.conf` 文件做出此类更改时，请输入 `/etc/init.d/inetd restart` 以重启 inetd 服务器。

####### 使用 xinetd

使用 xinetd 的 Linux 发行版在系统启动时启动 xinetd。xinetd 服务器在启动时读取名为 `/etc/xinetd.conf` 的配置文件。此文件告知 xinetd 监听哪些端口以及为每个端口启动哪个服务器。该文件可以包含指向其他配置文件的指令。在 Linux 中，`/etc/xinetd.conf` 文件看起来如下：

```
# xinetd 的简单配置文件
# 设置一些默认值并包含 /etc/xinetd.d/defaults
{
        instances            = 30
        log_type             = FILE /var/log/xinetd.log
        log_on_success       = HOST EXIT DURATION
        log_on_failure       = HOST ATTEMPT
        cps                  = 50 10
}
        includedir /etc/xinetd.d
```

注释行以井号（#）开头。用花括号（{ ... }）包围的默认值块指定了某些属性的默认值。这些默认值适用于配置文件中的所有其他服务。instances 属性设置为 30，这意味着对于任何服务，最多可以有 30 个服务器同时处于活动状态。

`/etc/xinetd.conf` 文件中的最后一行使用 includedir 指令包含 `/etc/xinetd.d` 目录中的所有文件，但以点（.）开头的文件除外。其理念是 `/etc/xinetd.d` 目录包含所有服务配置文件——每个服务类型都有一个文件，供 xinetd 服务器管理。输入 `ls /etc/xinetd.d` 以查看你系统上的 xinetd 配置文件。`/etc/xinetd.d` 中的每个文件指定 xinetd 可以启动的一个服务的属性。




# 574 使用互联网超级服务器

![](img/11709a8f88c8cd03868a929dc94c0e2b_599_0.png)

例如，SUSE Linux 使用 `xinetd` 来启动一些服务，包括 `vsftpd` FTP 服务器。输入 `cat /etc/xinetd.d/vsftpd` 可以查看 `vsftpd` 服务的 `xinetd` 配置。以下是 SUSE 系统上该文件的典型列表：

```
# default: off
# description:
# The vsftpd FTP server serves FTP connections. It uses
# normal, unencrypted usernames and passwords for authentication.
# vsftpd is designed to be secure.

service ftp
{
    socket_type       = stream
    protocol          = ftp
    wait              = no
    user              = root
    server            = /usr/sbin/vsftpd
}
```

文件名（在本例中为 `vsftpd`）可以是任意值；重要的是文件中出现在 `service` 关键字旁边的服务名称。在这种情况下，`service ftp` 这一行告诉 `xinetd` 服务的名称。`xinetd` 使用此名称从 `/etc/services` 文件中查找端口号。

`/etc/xinetd.d/vsftpd` 中的属性（由花括号 `{…}` 包围）具有以下含义：

-   `socket_type` 属性设置为 `stream`，这告诉 `xinetd` FTP 服务使用面向连接的 TCP 套接字与客户端通信。对于使用无连接 UDP 套接字的服务，此属性设置为 `dgram`。
-   `wait` 属性设置为 `no`，这告诉 `xinetd` 为每个请求启动一个新的服务器。如果此属性设置为 `yes`，则 `xinetd` 会等待服务器退出，然后再再次启动服务器。
-   `user` 属性提供了 `xinetd` 用于运行服务器的用户 ID。在这种情况下，服务器以 `root` 身份运行 TELNET 服务器。
-   `server` 属性指定了为此服务运行的程序。在这种情况下，`xinetd` 运行 `/usr/sbin/vsftpd` 程序来提供 FTP 服务。

浏览 Linux 系统 `/etc/xinetd.d` 目录中的文件，可以了解 `xinetd` 设置为启动的服务类型。如果你想关闭任何服务（许多服务默认已禁用），你可以通过编辑该服务的配置文件，并在包围所有属性的花括号内添加以下行来实现：

```
disable       = yes
```

当你更改 `xinetd` 配置文件时，必须通过输入以下命令重启 `xinetd` 服务器：

```
/etc/init.d/xinetd restart
```

**注意：** 你通常可以配置服务在 `xinetd` 下运行或作为独立服务运行。例如，SUSE 在 `xinetd` 的控制下启动 Very Secure FTP 服务器（`vsftpd`）。然而，Debian 和 Fedora Core 将 `vsftpd` 作为独立服务器运行。

###### 运行独立服务器

通过 `inetd` 或 `xinetd` 启动服务器是一种明智的方法，但如果服务需要频繁启动，这种方法效率并不高。如果 Web 服务器由 `inetd` 或 `xinetd` 控制，就会出现这样的情况：每当用户点击网页上的链接时，都会收到一个 Web 服务请求，导致服务器频繁启动。对于此类高需求服务，最好以独立方式启动服务器。在独立模式下，服务器可以作为 *守护进程* 运行——这是一个持续运行且永不终止的进程。这意味着服务器监听指定端口，每当有请求到达时，服务器通过复制自身来处理请求。这样，只要机器在运行，服务器就保持运行状态——至少在理论上如此。更高效的策略（常用于 Web 服务器）是运行服务器的多个副本，让每个副本处理部分传入请求。

你可以轻松配置 Linux 系统以自动启动各种独立服务器。本节将向你展示如何操作。

####### 手动启动和停止服务器

要启动未运行的服务，请使用 `server` 命令。例如，如果 Web 服务器（在 Fedora Core 中称为 `httpd`）未运行，你可以通过运行以下命令的特殊 Shell 脚本来启动它：

```
/etc/init.d/httpd start
```

该命令运行 `/etc/init.d/httpd` 脚本，并将 `start` 作为参数。如果 `httpd` 服务器已经运行且你想停止它，请以 `stop` 为参数运行相同命令，如下所示：

```
/etc/init.d/httpd stop
```

若要停止并重新启动服务器，只需使用 `restart` 作为参数：

```
/etc/init.d/httpd restart
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_601_0.png)

在 Debian、MEPIS、Ubuntu 和 SUSE 中，Web 服务器程序称为 `apache2`，请输入 `/etc/init.d/apache2 start` 来启动 Web 服务器。在 Knoppix 和 Xandros 中，请输入 `/etc/init.d/apache start`。使用相同命令并附加参数 `stop` 或 `restart` 来停止或重新启动 Web 服务器。

你可以启动和停止哪些服务？答案在 `/etc/init.d` 目录的文件中。要查看它们，请输入以下命令：

```
ls /etc/init.d
```

该命令响应中列出的所有文件都是你的 Linux 系统上安装的服务——你可以按需启动和停止它们。通常在 `/etc/init.d` 目录中可以看到 65 到 70 个列出的服务。

####### 在启动时自动启动服务器

你可以使用 `/etc/init.d` 目录中的脚本手动启动、停止和重启服务器，但你希望某些服务在 Linux 系统启动时立即运行。你可以使用图形化服务器配置工具或命令来配置服务器在启动时自动启动。

![](img/11709a8f88c8cd03868a929dc94c0e2b_601_1.png)

配置服务自动启动的命令取决于发行版。在 Debian、MEPIS、Knoppix、Ubuntu 和 Xandros 中，使用 `update-rc.d` 命令。在 Fedora Core 和 SUSE 中，使用 `chkconfig` 命令。以下各节将解释这两个命令。

######## 在 Fedora Core 和 SUSE 中使用 chkconfig 命令

`chkconfig` 程序是 Fedora Core 和 SUSE 中用于检查和更新 Linux 中服务器当前设置的命令行工具。各种服务器组合被设置为在不同的运行级别自动启动。每个 *运行级别* 代表一种系统配置，其中运行一组选定的进程。你通常关注运行级别 3 和 5，因为运行级别 3 用于文本模式登录，而运行级别 5 用于通过图形界面登录。

`chkconfig` 命令使用简单。例如，假设你想在运行级别 3 和 5 自动启动 `named` 服务器。你只需以 `root` 身份登录并在 Shell 提示符下输入以下命令：

```
chkconfig --level 35 named on
```

要查看 `named` 服务器的状态，请输入以下命令：

```
chkconfig --list named
```

你会看到类似以下的一行输出：

```
named	0:off	1:off	2:off	3:on	4:off	5:on	6:off
```

输出显示了 named 服务器在运行级别 0 到 6 的状态。如你所见，named 设置为在运行级别 3 和 5 运行。

如果你想关闭 named，可以使用此命令：

```
chkconfig --level 35 named off
```

你可以使用 chkconfig 查看所有服务的状态，包括通过 xinetd 启动的服务。例如，你可以通过输入以下命令查看所有服务的状态：

```
chkconfig --list | more
```

输出显示了每个服务在运行级别 0 到 6 的状态。对于每个运行级别，服务要么开启要么关闭。在列表的末尾，chkconfig 显示由 xinetd 控制的服务列表。每个基于 xinetd 的服务也根据 xinetd 是否配置为启动该服务而标记为开启或关闭。

######## 在 Debian、Knoppix、MEPIS、Ubuntu 和 Xandros 中使用 update-rc.d 命令

在 Debian、Knoppix、MEPIS、Ubuntu 和 Xandros 中，你可以使用 update-rc.d 命令来设置应在系统启动到特定启动级别时启动的服务。最简单的设置方式是使用此形式命令中的 defaults 选项：

```
update-rc.d service defaults
```

其中 *service* 是 /etc/init.d 目录中启动和停止服务的脚本文件的名称，除此之外还有其它功能。

使用 defaults 选项时，update-rc.d 设置符号链接（换句话说就是快捷方式），以便在运行级别 2、3、4 和 5 启动服务，并在运行级别 0、1 和 6 停止服务。一个序列号控制每个服务启动的顺序。（序列号较小的服务先于序列号较大的服务启动，且数字通常从 00 到 99。）如果你没有明确指定序列号，使用 defaults 选项时 update-rc.d 会使用序列号 20。

![](img/11709a8f88c8cd03868a929dc94c0e2b_602_0.png)





## 578 运行独立服务器

你还可以在特定的运行级别以及特定的序列中启动和停止服务。例如，要在运行级别 2 和 5 中以序列号 85 启动服务，并在运行级别 0、1 和 6 中以序列 90 停止该服务，请使用以下命令：

```
update-rc.d service start 85 2 5 . stop 90 0 1 6 .
```

请记住，*service* 必须是 `/etc/init.d` 目录中某个脚本文件的名称。

> **提示**
> 如果你需要阻止服务在系统启动时启动，请在终端窗口中输入 **update-rc.d -f service remove**，其中 *service* 是 `/etc/init.d` 中用于启动或停止该服务的脚本文件的名称。

####### 使用 GUI 服务配置实用程序

如果你不喜欢输入命令，也许可以使用 GUI 工具来配置服务。Fedora Core 和 SUSE 都包含此类工具来管理服务。

在 Fedora Core 中，从 GUI 桌面选择 系统→管理→服务器设置→服务，并在提示时输入 *root* 密码。然后，你可以从服务配置窗口中打开或关闭服务，如图 1-2 所示。

服务配置实用程序在一个滚动列表中显示服务的名称。列表中的每一行都显示服务名称，名称前有一个复选框。复选框中的勾选标记表示该服务已被选中，以便在当前运行级别下于启动时启动。当对话框首次出现时，许多服务已经被选中。

你可以上下滚动列表，并单击复选框来选中或取消选中服务。如果你单击复选框，勾选标记会交替开启和关闭。要了解有关某项服务的更多信息，请单击服务名称，在窗口的右侧会显示简短的描述。例如，图 1-2 显示了 *acpid* 服务的帮助文本。此外，该实用程序还会显示选中的服务当前是否正在运行。

选择好你在系统启动时希望启动的所有服务器后，单击工具栏上的保存按钮以保存更改。然后选择 文件→退出 以退出。

> **警告！**
> 默认情况下，服务配置实用程序为当前运行级别配置所选服务。这意味着，如果你正在从图形桌面选择服务，系统处于运行级别 5，而你配置的服务被设置为在运行级别 5 下启动。如果你想为不同的级别设置服务，请从 编辑运行级别 菜单中选择该运行级别。

![](img/11709a8f88c8cd03868a929dc94c0e2b_604_0.png)

**图 1-2：** 在 Fedora Core 中，这是你设置服务以便在启动时自动启动的地方。

![](img/11709a8f88c8cd03868a929dc94c0e2b_604_1.png)

在 SUSE 中，你可以从 YaST 控制中心 — 主菜单 > 系统 > 控制中心 (YaST) 配置服务。单击左侧窗口中的 系统，然后单击 系统服务 (运行级别)。YaST 会打开 系统服务 (运行级别) 窗口（见图 1-3），在那里你可以启用或禁用服务。要在特定的运行级别下启用或禁用服务，请单击 专家模式 按钮，并在新出现的列表中编辑服务。

![](img/11709a8f88c8cd03868a929dc94c0e2b_604_2.png)

**图 1-3：** 在 SUSE 中，使用此 YaST 窗口来指定在启动时启动的服务。

### 580 运行独立服务器

表 1-1 列出了服务列表以及每个服务的简要描述。第一列显示服务的名称，这与提供该服务所需的运行程序的名称相同。当你在系统上运行 GUI 服务配置实用程序时，可能不会看到所有这些列出的服务，因为具体的服务列表取决于你的 Linux 系统中安装了什么。

**表 1-1** Linux 中的一些常见服务

| 服务名称 | 描述 |
| --- | --- |
| acpid | 监听来自内核的高级配置和电源接口 (ACPI) 事件，并在发生此类事件时通知其他程序。当内核将计算机放入低功耗状态（例如待机模式）以节省能源时，可能会发生 ACPI 事件。 |
| apache, apache2, 或 httpd | Apache 万维网 (WWW) 服务器 |
| apmd | 监控高级电源管理 (APM) BIOS，并记录电力状态（交流电或电池备用） |
| atd | 运行由 at 和 cron 命令调度的命令 |
| autofs | 自动挂载文件系统（例如，当你将 CD-ROM 插入 CD-ROM 驱动器时） |
| cron 或 crond | 根据 crontab 命令设置的周期性计划运行用户指定的程序 |
| gpm | 在文本模式屏幕上启用鼠标使用 |
| innd | InterNetNews 守护进程 — 你可以使用它来支持系统本地新闻组的互联网新闻服务器 |
| isdn | 启动和停止 ISDN（综合业务数字网）服务 — 这是一种通过普通电话线提供的数字通信服务（仅当你有 ISDN 服务时才启用） |
| named | 域名系统 (DNS) 的服务器，用于将主机名转换为 IP 地址。如果你愿意，可以在你的系统上运行一个副本。 |
| network 或 networking | 允许你激活或停用所有配置为在系统启动时启动的网络接口 |
| nfs 或 nfs server | 使用网络文件系统 (NFS) 协议启用 /etc/exports 文件中指定的文件系统共享 |
| nfs lock | 为使用网络文件系统 (NFS) 协议导出的文件系统提供文件锁定功能，以便其他系统（运行 NFS）可以共享你系统中的文件 |
| pcmcia | 为 PCMCIA 设备提供支持 |
| portmap | 任何依赖远程过程调用 (RPC) 的软件使用的服务器。例如，NFS 需要 portmap 服务。 |
| samba, smb, 或 smbf5 | 启动和停止支持 Linux 系统上 LAN Manager 服务的 Samba smbd 和 nmbd 服务 |
| sendmail | 将邮件消息从一台机器移动到另一台机器。如果你希望从 Linux 系统发送邮件，请启动此服务。如果你不打算将 Linux 系统用作邮件服务器，请不要启动 sendmail 服务器，因为它可能会减慢启动过程并消耗不必要的资源。 |
| snmpd | 用于网络管理功能的简单网络管理协议 (SNMP) 服务 |
| spamassassin | 运行 spamd — SpamAssassin 邮件过滤程序 |
| ssh 或 sshd | OpenSSH（安全外壳）安全远程登录设施的服务器 |
| syslog 或 syslogd | 许多其他程序（包括其他服务）使用的服务，用于在日志文件（通常是 /var/log/messages 文件）中记录各种错误和状态消息。始终运行此服务。 |
| vsftpd | 用于使用文件传输协议 (FTP) 进行文件传输的 Very Secure FTP 守护进程 |
| winbind | 启动和停止 Samba winbindd 服务器，该服务器提供类似于 /etc/nsswitch.conf 文件提供的名称切换功能 |
| xfs | 启动和停止 X 字体服务器的服务器 |
| xinetd | Internet 超级服务器，是老式 inetd 的替代品。它会在需要时启动其他 Internet 服务，如 TELNET 和 FTP。 |
| ypbind | 在 Network Information System (NIS) 客户端上运行的服务，将客户端绑定到 NIS 域。除非你正在使用 NIS，否则不需要启动 ypbind。 |

##### 第 2 章：运行 Web 服务器

###### 本章内容

- 理解 HTTP
- 安装 Apache Web 服务器
- 配置 Apache Web 服务器
- 使用 Apache Web 服务器支持虚拟主机

万维网（WWW 或 Web）使 Internet 进入了主流，因为 Web 浏览器使得浏览存储在各种 Internet 主机上的文档变得容易。无论你是经营一家小企业，还是为一家大公司管理计算机系统和网络，你都有可能必须设置和维护 Web 服务器。由于 Linux PC 具有内置的网络支持，它是一款价格合理的 Web 服务器。本章描述如何在 Linux PC 上配置 Apache Web 服务器。

###### 理解 HTTP

Web 服务器使用 HTTP 提供信息。Web 服务器也被称为 *HTTP 守护进程*（因为在 UNIX 中，持续运行的服务器进程被称为守护进程），或者简称为 *HTTPD*。Web 服务器程序通常命名为 apache、apache2 或 httpd，具体取决于你的 Linux 发行版。

HTTP 代表 *HyperText Transfer Protocol*（超文本传输协议）。*HyperText* 部分指的是 Web 页面包含超文本链接的事实。*Transfer Protocol* 部分指的是通过网络从一个计算机传输到另一个计算机 Web 页面的标准约定。虽然你实际上不需要理解 HTTP 来设置 Web 服务器或使用 Web 浏览器，但了解一下其工作原理确实有助于你理解 Web 是如何工作的。

你可以通过使用 TELNET 程序连接到 Web 服务器监听的端口来获得对 HTTP 的第一手体验。在大多数系统上，Web 服务器监听 80 端口，并响应发送到该端口的任何 HTTP 请求。因此，你可以使用 TELNET 程序连接到系统（如果它有 Web 服务器）的 80 端口并尝试一些 HTTP 命令。




####### HTTP 是互联网标准吗？

尽管 HTTP 自 1990 年以来在 Web 中广泛使用，但直到最近它才成为互联网标准。所有互联网标准最初都以请求意见稿（Request for Comment，简称 RFC）的形式分发。第一个与 HTTP 相关的 RFC 是 RFC 1945《超文本传输协议 — HTTP/1.0》（T. Berners-Lee, R. Fielding, and H. Frystyk，1996 年 5 月）。然而，RFC 1945 被视为信息性文档，而非标准。

RFC 2616《超文本传输协议 — HTTP/1.1》（R. Fielding, J. Gettys, J. Mogul, H. Frystyk, L. Masinter, P. Leach, T. Berners-Lee，1999 年 6 月）是 HTTP 的草案互联网标准。

要阅读这些 RFC，请将您的 Web 浏览器指向 www.ietf.org/rfc/ 或 www.faqs.org/rfcs。

要了解有关 HTTP/1.1 及其他与 Web 相关的标准的更多信息，请使用 Web 浏览器访问 www.w3.org/Protocols。

要查看 HTTP 实际工作的示例，请按照以下步骤操作：

1. 确保您的 Linux 计算机与互联网的连接正常运作。
   - 例如，如果您使用 PPP，请确保已建立连接。如果您拥有宽带电缆或 DSL 连接，您的连接很可能始终处于开启状态。
2. 输入以下命令。（我使用美国政府网站 URL 来说明 HTTP 协议的工作原理。）
   - `telnet www.gao.gov 80`
3. 看到 `Connected...` 消息后，输入以下 HTTP 命令并按两次 Enter：
   - `GET / HTTP/1.0`

作为对该 HTTP 命令的响应，Web 服务器返回一些有用信息，随后是默认 HTML 文件的内容（通常称为 `index.html`）。

以下是我在美国政府网站尝试 GET 命令时得到的结果。（在下文中，我展示了你需要输入 GET 命令的位置。）

```
Trying 161.203.16.2...
Connected to www.gao.gov.
Escape character is '^}'.
GET / HTTP/1.0    (输入此行然后按两次 Enter)

HTTP/1.1 200 OK
Date: Wed, 14 Dec 2005 22:53:26 GMT
Server: Apache
Connection: close
Content-Type: text/html; charset=ISO-8859-1

<html>
<head>
<title>The Government Accountability Office</title>
... (省略行) ...
</head>
<body>

... (省略行) ...

</body>
</html>

Connection closed by foreign host.
```

当您尝试这个 TELNET 示例时，您将看到 Web 服务器发送给 Web 浏览器的确切内容。前几行是供浏览器使用的管理信息。服务器返回此信息：

- 一行显示服务器使用 HTTP 协议版本 1.1 以及表示成功的状态码 200：
  ```
  HTTP/1.1 200 OK
  ```
- 当前日期和时间。一个日期和时间字符串的示例如下：
  ```
  Date: Wed, 14 Dec 2005 22:53:26 GMT
  ```
- Web 服务器软件的名称、版本及其他详细信息。如今，常见的做法是仅显示软件的通用名称（例如 *Apache*），而不提供任何其他详细信息，因为有人可能会利用版本信息来攻击该版本的特定漏洞。
- Web 服务器返回的文档类型。对于 HTML 文档，内容类型报告如下：
  ```
  Content-Type: text/html; charset=ISO-8859-1
  ```

文档本身跟随在管理信息之后。HTML 文档具有以下通用布局：

```
<html>
<head>
<title>文档标题在此处</title>
</head>
<body 可选属性在此处>
.... 文档其余部分在此处
</body>
</html>
```

通过查看显示 Web 服务器响应 **GET** 命令所返回内容的列表，您可以识别出此布局。由于示例使用 **telnet** 命令获取文档，您会看到 HTML 内容以文本行的形式显示。如果您使用 Web 浏览器（如 Mozilla Firefox）访问同一网站（**www.gao.gov**），您将以图形形式看到该页面，如 **图 2-1** 所示。

HTTP 命令的示例展示了 **GET** 命令的结果。**GET** 是最常见的 HTTP 命令；它使服务器返回指定的 HTML 文档或图像。

另外两个 HTTP 命令是 **HEAD** 和 **POST**。**HEAD** 命令几乎像 **GET**：它使服务器返回文档中除主体外的所有内容。**POST** 命令向服务器发送信息；至于如何处理这些信息，由服务器自行决定。

![](img/11709a8f88c8cd03868a929dc94c0e2b_611_0.png)

###### 探索 Apache Web 服务器

您可能已经知道如何使用 Web，但您可能不知道如何设置 Web 服务器，以便您也能通过 Web 页面向世界提供信息。要在 Web 上成为信息提供商，您必须在位于互联网上的 Linux 计算机上运行 Web 服务器。您还必须为您的网站准备 Web 页面——这项任务可能比设置 Web 服务器更具挑战性。

在可用的 Web 服务器中，Apache Web 服务器是最受欢迎的，并且适用于所有 Linux 发行版。Apache Web 服务器最初是 NCSA HTTPD 服务器的改进版本，但很快发展为一个独立的项目。与 NCSA HTTPD 一样，Apache 服务器由一个合作团队开发和维护。Apache 在网络上免费提供。

####### 安装 Apache Web 服务器

根据您在安装 Linux 发行版时所做的选择，Apache Web 服务器可能已安装在您的系统中。如果已安装，它可能已在运行，或者您可能需要启动它。例如，Apache Web 服务器安装在 Knoppix 和 Xandros 中，但默认情况下并未开启。

![](img/11709a8f88c8cd03868a929dc94c0e2b_612_0.png)

Apache Web 服务器软件包名称因发行版而异——Fedora Core 称之为 `httpd`，而 Knoppix 和 Xandros 称之为 `apache`。Debian 和 SUSE 将软件包称为 `apache2`。要检查 Apache Web 服务器是否已安装，在 Debian、Knoppix、MEPIS 和 Xandros 中输入 `dpkg -l apache*`，在 Ubuntu 中输入 `sudo dpkg -l apache*`。如果在输出第一列中看到以 `apache` 开头的软件包名称前有 `ii` 或 `pn`，则表示它已完全或部分安装。在 Fedora Core 中，输入 `rpm -q httpd`。在 SUSE 中，输入 `rpm -q apache2`。

![](img/11709a8f88c8cd03868a929dc94c0e2b_612_1.png)

如果 Web 服务器未安装，您可以轻松安装。步骤取决于您的 Linux 发行版。在 Debian 和 MEPIS 中，以 `root` 身份登录并输入 `apt-get install apache2`，在 Ubuntu 中输入 `sudo apt-get install apache2`。在 Fedora Core 中，挂载伴随 DVD，并通过输入以下命令安装 Apache Web 服务器：

```bash
cd /media/cdrom/Fedora/RPMS
rpm -ivh httpd*
```

####### 为什么叫 Apache？

根据 www.apache.org/foundation/faq.html 上关于 Apache Web 服务器项目的信息，Apache 小组于 1995 年 3 月由一批提供补丁文件的人员组成，这些补丁文件旨在修复 NCSA HTTPD 1.3 中的 bug。将补丁应用到 NCSA HTTPD 后的结果是他们所谓的“补丁式”服务器（这就是 Apache 名称的由来）。Apache 小组现已演变为 Apache 软件基金会（ASF），这是一家于 1999 年 6 月在美国特拉华州注册的非营利公司。ASF 拥有其他多个正在进行的项目。您可以访问 www.apache.org 阅读有关这些项目的信息。特别是，请访问 http://httpd.apache.org 以获取更多关于 Apache Web 服务器项目的信息。

根据 2005 年 8 月 Netcraft Web 服务器调查 http://news.netcraft.com/archives/web_server_survey.html，Apache Web 服务器是市面上最流行的 Web 服务器——报告的 70,392,567 个站点中，69.46% 使用了 Apache 服务器。微软 Internet Information Services (IIS) 位居第二，份额为 20.43%。

![](img/11709a8f88c8cd03868a929dc94c0e2b_613_0.png)

在 SUSE 中，从 YaST 控制中心中的 Software 类别点击“安装和移除软件”——主菜单 → 系统 → 控制中心 (YaST)——然后使用 YaST 的搜索功能查找 Apache。找到您想要安装的软件包后，选中它们并点击“接受”以进行安装。

就是这样！安装好 Apache Web 服务器后，您就可以运行它了。

####### 启动 Apache Web 服务器

即使安装了 Apache Web 服务器，它也可能未设置为在启动时自动运行。如果您想尝试使用它，必须手动启动服务器。

![](img/11709a8f88c8cd03868a929dc94c0e2b_613_1.png)

要启动 Apache Web 服务器，请以 root 身份登录并输入 `/etc/init.d/apache2 start`。在 Debian、MEPIS、Ubuntu 和 SUSE 中，输入 `service httpd start` 于 Fedora Core。在 Knoppix 和 Xandros 中，输入 `/etc/init.d/apache2 start`。如果您希望服务器在启动时自动启动 Apache Web 服务器，请在 Debian、MEPIS 和 Ubuntu 中输入 `update-rc.d apache2 defaults`。在 Knoppix 和 Xandros 中，输入 `update-rc.d apache2 defaults`。在 Fedora Core 中，输入 `chkconfig -levels 35 httpd on`。在 SUSE 中，输入 `chkconfig -levels 35 apache2 on`。

要查看服务器是否正在运行，请输入 `ps ax | grep processname`，其中 `processname` 在 Fedora Core 和 SUSE 中是 `httpd`，在 Debian、Knoppix 和 Xandros 中是 `apache`。如果在输出中看到多个 Web 服务器进程，则一切正常。运行多个 Web 服务器进程——一个父进程和若干子进程——是一种常见做法，以便通过为每个请求分配一个 Web 服务器进程来高效处理多个 HTTP 请求。

如果 `ps ax` 的输出没有显示任何 Web 服务器进程，那么错误可能潜伏在 Apache 配置文件中。如果出现这种情况，你必须修复配置文件中的任何问题，并重新启动服务器。

如果 Web 服务器正在运行，你可以使用 TELNET 程序连接到 80 端口，以检查服务器是否正常工作。首先，在终端窗口中输入以下命令：

```
telnet localhost 80
```

当你收到“已连接”（Connected）消息后，输入

```
HEAD / HTTP/1.0
```

然后按两次回车。你会收到一个类似于以下内容的响应，当然日期和数字会有所不同：

```
HTTP/1.1 200 OK
Date: Sat, 17 Dec 2005 20:57:20 GMT
Server: Apache/2.0.54 (Fedora)
Last-Modified: Sat, 17 Dec 2005 20:57:05 GMT
ETag: "156946-25b-8fe6d64a0"
Accept-Ranges: bytes
Content-Length: 603
Connection: close
Content-Type: text/html; charset=UTF-8
```
连接由远程主机关闭。

该响应显示了有关 Web 服务器和默认主页的一些信息。你也可以使用运行在你的 Linux 系统上的 Web 浏览器（如 Firefox）来检查 Web 服务器。使用 URL http://localhost/ 并看看会发生什么。

![](img/11709a8f88c8cd03868a929dc94c0e2b_614_0.png)

如果你在 Web 浏览器中尝试 http://localhost/ URL 时遇到错误消息，这意味着在由 `DocumentRoot` 配置指令指定的目录中没有 `index.html` 文件（默认网页）。要纠正这个问题，只需在适当的目录中创建一个名为 `index.html` 的简单 HTML 文档（在 HTTP 服务器的配置文件中查找由 `DocumentRoot` 指定的目录名称）。我将在下一节中解释诸如 `DocumentRoot` 这样的配置指令。

###### 配置 Apache Web 服务器

Apache Web 服务器程序文件和配置文件在不同的发行版中存储在不同的位置。在 Fedora Core、Knoppix、SUSE 和 Xandros 中，Apache Web 服务器配置文件名为 `httpd.conf`，而在 Debian、MEPIS 和 Ubuntu 中，其名称为 `apache2.conf`。配置文件是一个文本文件，其中包含指定 Web 服务器各个方面的指令。

在 Debian、MEPIS、SUSE 和 Ubuntu 中，配置文件位于 `/etc/apache2` 目录中。在 Fedora Core 中，`httpd.conf` 文件位于 `/etc/httpd/conf` 目录中。在 Knoppix 和 Xandros 中，该文件位于 `/etc/apache` 目录中。

包含 `httpd.conf` 文件的目录还包含有关安全套接字层（SSL）实现需求的信息。（SSL 实现是 Apache Web 服务器的一部分。）

####### 使用 Apache 配置工具

在某些 Linux 发行版中，你可以使用图形界面工具来配置 Apache Web 服务器。特别是，Fedora Core 和 SUSE 都附带了用于配置 Apache Web 服务器的图形界面工具。我将在本节中向你介绍这些图形界面工具。

在 Fedora Core 中，以 `root` 身份登录，并从图形桌面选择 系统 → 管理 → 服务器设置 → HTTP。将出现 HTTP 对话框，如 图 2-2 所示。

![](img/11709a8f88c8cd03868a929dc94c0e2b_615_0.png)

Apache 配置对话框分为四个选项卡。你可以从这些选项卡中设置各种选项：

- **主选项卡（Main）：** 在此选项卡中，你可以指定 Apache 期望接收 Web 服务请求的 IP 地址和端口号。你还可以设置网页管理员的电子邮件地址。
- **虚拟主机（Virtual Hosts）：** 在这里你可以设置虚拟主机。（我将在本章后面讨论虚拟主机的选项。）你还可以编辑适用于所有虚拟主机的默认设置。在虚拟主机选项卡上单击“编辑默认设置”按钮会弹出另一个对话框（如图 2-3 所示），你可以从中设置多种不同的选项。
- **服务器（Server）：** 此选项卡包含服务器设置，例如 HTTP 服务器运行所在的用户和组名称，以及存储进程 ID 的文件位置。
- **性能调优（Performance Tuning）：** 在此选项卡中，你可以设置一些控制整体性能的参数。你可以设置允许的最大连接数、连接超时时间以及每个连接的最大请求数。

最初，配置窗口显示来自配置文件 `/etc/httpd/conf/httpd.conf` 的默认值。在你进行任何更改后，单击“确定”按钮。配置工具会提示你询问是否确实要保存更改并退出。如果是，请单击“是”，你就完成了。

在 SUSE 中，选择 主菜单 → 系统 → 控制中心 (YaST) 以打开 YaST 控制中心。单击窗口左侧的“网络服务”，然后单击右侧的“HTTP 服务器”。YaST 会打开“HTTP 服务器向导”窗口，如 图 2-4 所示，并引导你通过五个步骤来配置 HTTP 服务器。步骤如下：

1.  确定服务器监听的网络接口。
2.  指定加载特定脚本语言（如 Perl、Python、PHP4 或 Ruby）的模块。
3.  指定若干配置指令，例如文档和配置文件的位置。
4.  配置任何虚拟主机。
5.  启动 HTTP 服务器。

YaST 的好处在于，它会自动安装配置和运行 HTTP 服务器所需的任何其他内容（如 Apache 模块）。

图 2-4：在 SUSE 中，YaST 使你能够配置 Apache HTTP 服务器。

![](img/11709a8f88c8cd03868a929dc94c0e2b_617_0.png)

####### 请记住

![](img/11709a8f88c8cd03868a929dc94c0e2b_617_1.png)

当你使用图形界面配置工具配置 Apache HTTP 服务器时，你所做的只是更改存储在 Apache Web 服务器配置文件中的选项和属性（在 Debian、MEPIS 和 Ubuntu 中为 /etc/apache2/apache2.conf；在 Fedora Core 中为 /etc/httpd/conf/httpd.conf；在 Knoppix 和 Xandros 中为 /etc/apache/httpd.conf；在 SUSE 中为 /etc/apache2/httpd.conf 以及 /etc/apache2 目录中的所有 .conf 文件）。你同样可以通过编辑配置文件来轻松进行更改，配置文件是一个纯文本文件。在接下来的章节中，我将向你介绍 Apache 配置文件中一些常见的配置指令。

####### Apache 配置文件的语法

Apache 服务器的操作由位于取决于你的发行版的目录中的 httpd.conf（或在 Debian 和 Ubuntu 中为 apache2.conf）文件控制。配置文件控制服务器如何运行、提供哪些文档以及谁可以访问这些文档。

在接下来的几节中，我将总结有关 Apache Web 服务器配置文件的关键信息。通常，要运行 Apache Web 服务器，你不需要更改配置文件中的任何内容。然而，了解配置文件的格式以及其中使用的各种关键字的含义是很有用的。

在研究 Apache Web 服务器配置文件时，请记住以下语法规则：

-   每个配置文件是一个文本文件，你可以用你喜欢的文本编辑器进行编辑，并使用 `more` 命令查看。
-   所有注释行以 # 开头。
-   每行只能有一个指令。
-   额外的空格和空行会被忽略。
-   通常，主配置文件通过使用 `Include` 指令引入许多其他配置文件。
-   除了路径名和 URL，所有条目均不区分大小写。

####### Apache Web 服务器配置文件

httpd.conf 文件（或在 Debian 中为 apache2.conf）是主要的 HTTP 守护进程配置文件——它包含控制 Apache Web 服务器如何运行的指令。通常，配置文件通过引用一个名为 `Include` 的指令来引入其他几个配置文件。

配置文件指定服务器使用的端口号、网站名称以及如果服务器出现任何问题时发送邮件的电子邮件地址。此外，配置文件还指定了网页的位置以及谁可以访问哪些目录。

在以下几节中，我将把 Apache 指令分为三类进行介绍：通用 HTTPD 指令、资源配置指令和访问控制指令。最后，我将解释如何在 Apache Web 服务器中设置虚拟主机，以便单个 Web 服务器可以处理发送到多个 IP 地址或主机名的 Web 请求。




######## 通用 HTTPD 指令

要在线浏览 Apache HTTPD 文档，请访问 `http://httpd.apache.org/docs/2.0/`。具体而言，您可以在 `http://httpd.apache.org/docs-2.0/mod/directives.html` 上查阅有关配置指令的信息。

以下是 Apache Web 服务器配置文件中的一些有趣内容：

- **ServerAdmin** 是 Web 服务器在发生错误时向客户端提供的电子邮件地址。**ServerAdmin** 的默认值为 `root@localhost`。请将此地址设置为一个有效的电子邮件地址，以便互联网上的任何人使用它来报告您的网站可能包含的任何错误。

- **Include** 从指定文件加载更多的配置指令。例如，在 Fedora Core 中，默认的 `/etc/httpd/conf/httpd.conf` 文件使用以下 **Include** 指令加载 `/etc/httpd/conf.d` 目录中的所有配置文件：

  ```
  Include conf.d/*.conf
  ```

  该命令意味着，只需将一个文件添加到 `/etc/httpd/conf.d` 目录，即可加载另一组配置。实际上，该目录包含各种 Apache HTTPD 模块（如 Perl、PHP 和 SSL）的配置文件。在 Fedora Core 中，研究 `/etc/httpd/conf.d` 目录中的配置文件，以了解影响 Apache Web 服务器行为的指令全集。

许多其他指令控制着 Apache Web 服务器的工作方式。以下列表总结了您可以在 `httpd.conf` 文件中使用的部分指令。您可以保持其中大多数指令的默认设置，但如果您维护 Web 服务器，了解这些指令是很重要的。

- **Listen _IP地址:端口_**：强制 Web 服务器监听特定的 IP 地址和端口号。默认情况下，Web 服务器响应与主机关联的所有 IP 地址。

- **User _名称_ [ _#id_]:** 指定 HTTP 守护程序使用的用户名（或 ID）。您可以将此指令保留为默认设置（**apache**）。如果您指定一个用户 ID，请使用井号（#）前缀表示数字 ID。

- **Group _名称_ [ _#id_]:** 指定 HTTP 守护程序在独立模式下运行时的组名（或 ID）。默认组名为 **apache**。

- **ServerRoot pathname**：指定 Web 服务器的配置和日志文件预期所在的目录。在 Debian、MEPIS、SUSE 和 Ubuntu 中，*ServerRoot* 设置为 `/etc/apache2`。在 Fedora Core 中，*ServerRoot* 设置为 `/etc/httpd`。在 Knoppix 和 Xandros 中，*ServerRoot* 是 `/etc/apache`。

- **ServerName www.company.com:80**：将服务器的主机名设置为 *www.company.com*，并将端口号设置为 80。仅在将 Web 页面重定向到另一处时使用 *ServerName*。

- **ServerTokens Major | Minor | Min | Prod | OS | Full**：控制返回给客户端的 *Server* 头部字段中的信息量。将该指令设置为 *Prod*，以便 *Server* 响应仅标识产品名称（在本例中为 Apache）。

- **StartServers num**：设置 Apache Web 服务器启动时立即启动的子进程数量。默认值为 8。

- **MaxSpareServers num**：设置期望的最大空闲子服务器进程数量。（如果子进程未处理 HTTP 请求，则被视为空闲。）默认值为 20。

- **MinSpareServers num**：设置期望的最小空闲子服务器进程数量。（如果子进程未处理 HTTP 请求，则被视为空闲。）如果数量低于此阈值，则每秒创建一个新的备用进程。默认值为 5。

- **Timeout numsec**：设置服务器等待客户端在建立连接后发送查询的秒数。默认 *Timeout* 为 300 秒（五分钟）。

- **ErrorLog filename**：设置 *httpd* 记录其遇到的错误的文件。如果文件名不以斜杠（/）开头，则名称被视为相对于 *ServerRoot*。在 Fedora Core 中，默认 *ErrorLog* 为 `/var/log/httpd/error_log`，在 SUSE 中为 `/var/log/apache2/error_log`。在 Debian、MEPIS 和 Ubuntu 中，错误日志位于 `/var/log/apache2/error.log`。在 Knoppix 和 Xandros 中，错误日志位于 `/var/log/apache/error.log`。典型的错误日志条目包括事件，如服务器重启和任何警告消息。

- **TransferLog filename**：设置 *httpd* 记录所有客户端访问（包括失败的访问）的文件。

- **LogFormat formatstring formatname**：指定 *TransferLog* 日志文件条目的格式。*CustomLog* 指令也使用此格式以特定格式生成日志。

- **CustomLog filename formatname**：设置自定义日志文件的名称，*httpd* 在该文件中以由 *formatname*（您使用 *LogFormat* 指令定义）指定的格式记录所有客户端访问（包括失败的访问）。

- **PidFile filename**：设置 *httpd* 存储其进程 ID 的文件。

![](img/11709a8f88c8cd03868a929dc94c0e2b_620_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_620_1.png)

- **MaxClients num**：设置可以同时连接到服务器的客户端数量限制。默认值为 150。MaxClients 的值不能超过 256。

- **LoadModule module file.so**：加载构建为动态共享对象（DSO）的模块。您必须指定模块名称和模块的对象文件。由于模块加载顺序很重要，请保留这些指令在默认配置文件中的原样。注意：mod_ssl 模块提供支持使用安全套接字层（SSL）协议进行加密。

######## 资源配置指令

资源配置指令指定 Web 页面的位置，以及如何指定各种文件的数据类型。开始时，您可以将指令保留为默认设置。以下是 Apache Web 服务器的一些资源配置指令：

- **DocumentRoot pathname**：指定 HTTP 服务器查找 Web 页面的目录。在 Debian 中，默认 DocumentRoot 为 /var/www/apache2-default。在 Fedora Core 中，DocumentRoot 为 /var/www/html。在 SUSE 中，DocumentRoot 为 /srv/www/htdocs。在 Knoppix 和 Xandros 中，DocumentRoot 为 /var/www。如果您的 HTML 文档放在其他目录中，请将 DocumentRoot 设置为该目录。

- **UserDir dirname**：指定用户主目录下的子目录，当 URL 中出现用户名时，HTTP 服务器在该子目录中查找 Web 页面（例如在 http://www.xyz.net/~naba 这样的 URL 中，包含带有波浪号前缀的用户名）。默认情况下，通过将 dirname 设置为 disable 来关闭 UserDir 功能。如果您想启用它，可以将其设置为 public_html，这意味着用户的 Web 页面位于该用户主目录的 public_html 子目录中。UserDir 默认被禁用，因为它可能使文件系统向所有人开放。Apache 文档建议在 httpd.conf 文件中添加以下行：

  ```
  UserDir disabled root
  ```

- **DirectoryIndex filename filename2 …**：指示当客户端未指定文档时，服务器返回默认文件。默认的 DirectoryIndex 是 index.html。如果 Apache Web 服务器未找到此文件，只要允许对该目录进行索引，它就会返回该目录的索引（基本上是一个美观的文件列表）。

- **AccessFileName filename**：指定可能出现在每个包含文档目录中的文件名称，该文件指示谁有权访问该目录的内容。默认 *AccessFileName* 为 .htaccess。此文件的语法与 Apache 访问控制指令相同，我将在下一部分讨论。

- **AddType type/subtype extension**：将文件扩展名与 MIME 数据类型（形式为 *type/subtype*，如 *text/plain* 或 *image/gif*）关联起来。因此，要使服务器将具有 *.lst* 扩展名的文件视为 *纯文本* 文件，请指定以下内容：
  `AddType text/plain .lst`
  默认的 MIME 类型和扩展名列在 `/etc/mime.types` 文件中。

- **AddEncoding type extension**：将编码类型与文件扩展名关联。要使服务器将以 *.gz* 或 *.tgz* 结尾的文件标记为使用 *x-gzip* 编码方法（GZIP 编码的标准名称）进行编码，请指定以下内容：
  `AddEncoding x-gzip gz tgz`

- **DefaultType type/subtype**：指定如果服务器无法从文件扩展名确定类型时使用的 MIME 类型。如果您不指定 DefaultType，Apache Web 服务器假设 MIME 类型为 *text/html*。在默认的 *httpd.conf* 文件中，*DefaultType* 指定为 *text/plain*。

- **Redirect requested-file actual-URL**：指定对 *requested-file* 的任何请求重定向到 *actual-URL*。

- **Alias requested-dir actual-dir**：指定服务器使用 *actual-dir* 来定位 *requested-dir* 目录中的文件。（换句话说，*requested-dir* 是 *actual-dir* 的别名。要使对 */icons* 目录的请求转到 */usr/share/apache2/icons/*，请指定以下内容：
  `Alias /icons/ "/usr/share/apache2/icons/"`

- **ScriptAlias requested-dir actual-dir**：指定包含通用网关接口（CGI）脚本的目录的真实名称。例如，如果配置文件中包含此指令
  `ScriptAlias /cgi-bin/ "/srv/www/cgi-bin/"`
  这意味着当 Web 浏览器请求脚本（如 */cgi-bin/test-cgi*）时，HTTP 服务器运行脚本 */srv/www/cgi-bin/test-cgi*。

- **DefaultIcon iconfile**：指定服务器用于没有图标信息的文件的默认图标的存储位置。




########## ReadmeName

**ReadmeName** *filename*：指定一个 README 文件的名称，其内容将添加到自动生成的目录列表末尾。默认的 ReadmeName 是 README。

########## HeaderName

**HeaderName** *filename*：指定一个头文件的名称，其内容将添加到自动生成的目录列表开头。默认的 HeaderName 是 HEADER。

########## AddDescription

**AddDescription** "file description" *filename*：指定在目录列表中指定文件名旁边显示的文件描述字符串。您可以使用通配符，例如 `*.html`，作为文件名。例如，以下指令将扩展名为 `.tgz` 的文件描述为 GZIP 压缩的 tar 归档：

```apache
AddDescription "GZIP compressed tar archive" .tgz
```

########## AddIcon

**AddIcon** *iconfile* *extension1* *extension2* ...：将图标与一个或多个文件扩展名关联。以下指令将图标文件 `/icons/text.gif` 与文件扩展名 `.txt` 关联：

```apache
AddIcon /icons/text.gif .txt
```

########## AddIconByType

**AddIconByType** *iconfile* *MIME-types*：将图标与一组以 MIME 类型通配符形式指定的文件类型（例如 `text/*` 或 `image/*`）关联。要将图标文件 `/icons/text.gif` 与所有文本类型关联，请指定以下内容：

```apache
AddIconByType /icons/text.gif text/*
```

此指令还告知服务器，对于无法接受图像的客户机，使用 `TXT` 代替图标。（浏览器会告知服务器它们可以接受的数据类型。）

########## AddIconByEncoding

**AddIconByEncoding** *iconfile* *encoding1* *encoding2* ...：指定为一个或多个编码类型（例如 `x-compress` 或 `x-gzip`）显示的图标。

########## IndexIgnore

**IndexIgnore** *filename1* *filename2* ...：指示服务器在准备目录列表时忽略指定的文件名（通常包含通配符）。若要排除 README、HEADER 以及所有名称以点 (.)、结尾的波浪号 (`~`) 或结尾的井号 (#) 开头的文件，请指定以下内容：

```apache
IndexIgnore .??* *~ *# HEADER* README* RCS CVS *,v *,t
```

########## IndexOptions

**IndexOptions** *option1* *option2* ...：指示您希望服务器在准备的目录列表中包含哪些选项。选项可以包括以下一项或多项：

- `IconHeight=N` 指定图标的高度为 *N* 像素。
- `IconWidth=N` 指定图标的宽度为 *N* 像素。
- `NameWidth=N` 使文件名列的宽度为 *N* 个字符。
- `IconsAreLinks` 使图标像链接一样工作。
- `ScanHTMLTitles` 显示 HTML 文件的描述。
- `SuppressHTMLEreamble` 不向头文件（由 `HeaderName` 指令指定）添加标准 HTML 前言。
- `SuppressLastModified` 停止显示最后修改日期。
- `SuppressSize` 停止显示文件大小。
- `SuppressDescription` 停止显示任何文件描述。
- `SuppressColumnSorting` 停止列标题作为链接以启用列排序。

########## ErrorDocument

**ErrorDocument** *errortype* *filename*：指定当发生特定类型的错误时服务器发送的文件。您还可以为错误提供文本消息。以下是一些示例：

```apache
ErrorDocument 403 "Sorry, you cannot access this directory"
ErrorDocument 403 /error/noindex.html
ErrorDocument 404 /cgi-bin/bad_link.pl
ErrorDocument 401 /new_subscriber.html
```

如果没有 `ErrorDocument` 指令，服务器将发送内置的错误消息。`errortype` 可以是以下 HTTP/1.1 错误条件之一。（更多信息请参阅 `www.ietf.org/rfc/rfc2616.txt` 或 `www.faqs.org/rfcs/rfc2616.html` 中的 RFC 2616。）

- 400: 错误请求
- 401: 未授权
- 402: 需要支付
- 403: 禁止
- 404: 未找到
- 405: 方法不允许
- 406: 不可接受
- 407: 需要代理身份验证
- 408: 请求超时
- 409: 冲突
- 410: 已删除
- 411: 需要长度
- 412: 先决条件失败
- 413: 请求实体过大
- 414: 请求 URI 过长
- 415: 不支持的媒体类型
- 416: 无法满足请求范围
- 417: 期望失败
- 500: 内部服务器错误
- 501: 未实现
- 502: 错误网关
- 503: 服务不可用
- 504: 网关超时
- 505: 不支持的 HTTP 版本

########## TypesConfig

**TypesConfig** *filename*：指定包含文件扩展名到 MIME 数据类型映射的文件。（MIME 代表 Multipurpose Internet Mail Extensions，一种在单个消息文件中打包附件的方法。）服务器向客户机报告这些 MIME 类型。如果您未指定 TypesConfig 指令，httpd 假定 Types Config 文件是 `/etc/mime.types`。以下是默认 `/etc/mime.types` 文件中的一些选定行：

| MIME 类型 | 扩展名 |
| :--- | :--- |
| application/msword | doc |
| application/pdf | pdf |
| application/postscript | ai eps ps |
| application/x-tcl | tcl |
| audio/mpeg | mpga mp2 mp3 |
| audio/x-pn-realaudio | ram rm |
| audio/x-wav | wav |
| image/gif | gif |
| image/jpeg | jpeg jpg jpe |
| image/png | png |
| text/html | html htm |
| text/plain | asc txt |
| video/mpeg | mpeg mpg mpe |

每一行显示 MIME 类型（例如 `text/html`），后跟该类型的文件扩展名（`html` 或 `htm`）。

######## 访问控制指令

访问控制指令使您可以控制系统中不同目录的访问权限。这些是全局访问配置指令。您也可以拥有另一个访问配置文件，该文件使用 `AccessFileName` 指令指定的名称，位于 Apache Web 服务器可提供文档的每个目录中。（该每目录访问配置文件默认命名为 `.htaccess`。）

去除大部分注释行后，访问控制指令具有此格式：

```apache
# First, we configure the "default" to be a
# very restrictive set of permissions.
<Directory />
    Options FollowSymLinks
    AllowOverride None
</Directory>

# The following directory name should
# match DocumentRoot in httpd.conf
<Directory /srv/www/html>
    Options Indexes FollowSymLinks
    AllowOverride None
    order allow,deny
    allow from all
</Directory>

# The directory name should match the
# location of the cgi-bin directory
<Directory "/srv/www/cgi-bin">
    AllowOverride None
    Options None
    Order allow,deny
    Allow from all
</Directory>
```

访问控制指令使用与其他 Apache 指令不同的语法。该语法类似于 HTML。各种访问控制指令被封闭在成对的标签中，例如 `<Directory> . . . </Directory>`。

以下列表描述了一些访问控制指令。特别注意 `AuthUserFile` 指令；您可以为特定目录设置基于密码的访问控制。

########## Options

**Options** *opt1* *opt2* ...：指定此指令出现的目录部分的访问控制选项。选项可以是以下一项或多项：

- `None` 禁用所有访问控制功能。
- `All` 打开该目录的所有功能。
- `FollowSymLinks` 允许服务器跟随符号链接（换句话说，是快捷方式）。
- `SymLinksIfOwnerMatch` 仅当目录的同一用户拥有链接目录时才跟随符号链接。
- `ExecCGI` 允许在该目录中执行 CGI 脚本。
- `Includes` 允许在此目录中使用服务器端包含文件。（服务器端包含术语指的是放置在 HTML 文件中的指令，Web 服务器会在将结果返回给 Web 浏览器之前处理这些指令。）
- `Indexes` 允许客户机请求该目录的索引（目录列表）。
- `IncludesNOEXEC` 禁用服务器端包含中的 `#exec` 命令。

########## AllowOverride

**AllowOverride** *directive1* *directive2* ...：指定哪些访问控制指令可以在每目录级别上覆盖。指令列表可以包含以下一项或多项：

- `None` 阻止任何指令被覆盖。
- `All` 允许在每目录级别上覆盖任何指令。
- `Options` 允许在目录级文件中使用 `Options` 指令。
- `FileInfo` 允许使用控制文档类型的指令，例如 `AddType` 和 `AddEncoding`。
- `AuthConfig` 允许使用授权指令，例如 `AuthName`、`AuthType`、`AuthUserFile` 和 `AuthGroupFile`。
- `Limit` 允许在目录的访问配置文件中使用了 `Limit` 指令（`allow`、`deny` 和 `order`）。

########## AuthName

**AuthName** *name*：指定目录的授权名称。

########## AuthType

**AuthType** *type*：指定要使用的授权类型。唯一支持的授权类型是 `Basic`。

########## AuthUserFile

**AuthUserFile** *filename*：指定存储用于授权的用户名和密码的文件。例如，以下指令将授权文件设置为 `/etc/httpd/conf/passwd`：

```apache
AuthUserFile /etc/httpd/conf/passwd
```

您必须使用 `/usr/bin/htpasswd` 支持程序创建授权文件。要创建授权文件并为名为 `jdoe` 的用户添加密码，请指定以下内容：

```bash
/usr/bin/htpasswd -c /etc/httpd/conf/passwd jdoe
```





当系统提示输入密码时，请输入密码并通过再次键入来确认。

- **AuthGroupFile *文件名***：指定用于查询认证用户组列表的文件。
- **order *顺序***：指定两个其他指令——*allow* 和 *deny*——的评估顺序。顺序为以下之一：
    - *deny,allow* 使 Web 服务器在 *allow* 之前评估 *deny* 指令。
    - *allow,deny* 使 Web 服务器在 *deny* 之前评估 *allow* 指令。
    - *mutual-failure* 仅启用 *allow* 列表中的主机。
- **deny *from* *主机1* *主机2***…：指定被拒绝访问的主机。
- **allow *from* *主机1* *主机2***…：指定允许访问的主机。要允许特定域中的所有主机访问目录中的 Web 文档，请指定以下内容：

```
order deny,allow
allow from .nws.nooa.gov
```

- **require *实体* *en1* *en2***…：此指令指定哪些用户可以访问目录。*实体* 是以下之一：
    - *user* 仅启用命名列出的用户。
    - *group* 仅启用命名列出的组。
    - *valid-user* 允许列在 *AuthUserFile* 中的所有用户访问该目录（前提是他们输入了正确的密码）。

####### 虚拟主机设置

Apache HTTP 服务器的一个有用功能是它可以处理虚拟 Web 服务器。*虚拟主机* 意味着单个 Web 服务器可以响应许多不同的 IP 地址，并根据 IP 地址从不同的目录提供 Web 页面。这意味着您可以设置单个 Web 服务器来同时响应 *www.big.org* 和 *www.tiny.com*，并为每个主机名提供独特的主页。具备此能力的服务器被称为*多宿主* Web 服务器、*虚拟* Web 服务器或具有*虚拟主机支持*的服务器。

如您所料，互联网服务提供商 (ISP) 使用 Apache Web 服务器的虚拟主机功能向其客户提供虚拟 Web 站点。支持虚拟主机需要以下条件：

- Web 服务器必须能够响应多个 IP 地址（每个都有唯一的域名），并且必须允许您为每个 IP 地址指定文档目录、日志文件和其他配置项。
- 主机系统必须能够将多个 IP 地址与单个物理网络接口关联。Linux 可以做到这一点。
- 与 IP 地址关联的每个域名必须是一个独特的、已注册的域名，并具有正确的 DNS 条目。

有关如何设置 Apache HTTP 服务器中虚拟主机的最新信息，请参考以下 URL：

```
http://httpd.apache.org/docs-2.0/ vhosts
```

Apache HTTP 服务器可以针对不同的主机名响应不同的主页。支持虚拟主机时，您有两个选择：

- **运行多个 httpd 程序副本，每个 IP 地址一个**：在这种情况下，您为每个主机创建一个单独的 httpd.conf 配置文件的副本，并使用 Listen 指令使服务器响应特定的 IP 地址。
- **运行单个 httpd 程序副本和一个 httpd.conf 文件**：在配置文件中，将 Listen 设置为仅端口号（以便服务器响应与主机关联的任何 IP 地址），并使用 VirtualHost 指令为每个虚拟主机配置服务器。

仅当您不预期系统上有大量流量时，才运行多个 HTTP 守护程序；由于运行多个守护程序相关的开销，系统可能无法很好地响应。但是，如果每个虚拟主机对以下指令有独特的配置需求，您可能需要多个 HTTP 守护程序：

- UserlId 和 GroupId（HTTP 守护程序的用户和组 ID）
- ServerRoot（服务器的根目录）
- TypesConfig（MIME 类型配置文件）

对于流量较大的站点，请配置 Web 服务器，使单个 HTTP 守护程序可以服务于多个虚拟主机。当然，此建议意味着只有一个配置文件。在该配置文件中，使用 VirtualHost 指令来配置每个虚拟主机。

大多数 ISP 使用 Apache HTTP 服务器的 VirtualHost 功能向客户提供虚拟 Web 站点。除非您付费获得专用 Web 主机，否则您通常获得的是虚拟站点，在其中您拥有自己的域名，但与许多其他客户共享服务器和实际主机。

VirtualHost 指令的语法如下：

```
<VirtualHost 主机地址>
...
应用于此主机的指令
</VirtualHost>
```

使用此语法，您使用 <VirtualHost> 和 </VirtualHost> 来封闭一组仅应用于由 *主机地址* 参数标识的特定虚拟主机的指令。*主机地址* 可以是 IP 地址或虚拟主机完全限定域名。

您可以在 <VirtualHost> 块内放置几乎任何 Apache 指令。至少，Web 管理员在 <VirtualHost> 块中包含以下指令：

- **DocumentRoot**，指定该虚拟主机的文档驻留位置
- **Servername**，向外部世界标识服务器（此名称是 DNS 支持的已注册域名）
- **ServerAdmin**，该虚拟主机 Web 管理员的电子邮件地址
- **Redirect**，指定要重定向到其他 URL 的 URL
- **ErrorLog**，指定记录与该虚拟主机相关的错误的文件
- **CustomLog**，指定记录对该虚拟主机的访问的文件

当服务器收到针对特定虚拟主机 DocumentRoot 目录中文档的请求时，它会使用该服务器 <VirtualHost> 块内的配置参数来处理该请求。

以下是设置虚拟主机 www.inbsoft.com 的 <VirtualHost> 指令的一个典型示例。

```
<VirtualHost www.inbsoft.com>
    DocumentRoot    /home/naba/httpd/htdocs
    ServerName      www.inbsoft.com
    ServerAdmin     webmaster@inbsoft.com
    ScriptAlias     /cgi-bin/  /home/naba/httpd/cgi-bin/
    ErrorLog        /home/naba/httpd/logs/error_log
    CustomLog       /home/naba/httpd/logs/access_log common
</VirtualHost>
```

这里，CustomLog 指令中的名称 common 指的是 httpd.conf 文件早期由 LogFormat 指令定义的格式名称，如下所示：

```
LogFormat "%h %l %u %t \"%r\" %>s %b" common
```

# 606 配置 Apache Web 服务器

此日志的格式字符串会产生看起来像这样的日志文件行：

```
dial236.dc.psn.net - - [13/Dec/2005:18:09:00 -0500] "GET /
  HTTP/1.0" 200 1243
```

格式字符串包含两个以百分号 (%) 开头的字母令牌。这些令牌的含义如表 2-1 所示。

| 令牌 | 含义 |
| :--- | :--- |
| %b | 发送到客户端的字节数，不包括头部信息 |
| %h | 客户端机器的主机名 |
| %l | 用户身份（如果可用） |
| %r | 来自客户端的 HTTP 请求（例如，GET / HTTP/1.0） |
| %s | 来自 Web 服务器的响应代码 |
| %t | 当前本地日期和时间 |
| %u | 用户提供的用户名（仅在访问控制规则需要用户名/密码认证时）

##### 第 3 章：设置 FTP 服务器

###### 本章内容

- 安装 FTP 服务器
- 配置 FTP 服务器

**文件传输协议 (FTP)** 是一种流行的互联网服务，用于将一个系统的文件传输到另一个系统。*匿名 FTP* 是另一种用于分发文件的流行互联网服务。匿名 FTP 的巧妙之处在于，如果远程系统支持匿名 FTP，任何人可以使用 `anonymous` 用户 ID 使用 FTP，并可以从该系统下载文件。虽然匿名 FTP 对于分发数据很有用，但如果设置不当，它会带来安全风险。

Linux 发行版通常包含几个 FTP 客户端和由 Chris Evans 编写的非常安全的 FTP 守护程序（`vsftpd`）。FTP 服务器通常包含支持匿名 FTP 所需的文件。在本章中，我将展示如何通过文本配置文件配置 `vsftpd` FTP 服务器，以及如何控制对 FTP 服务器的访问。

###### 安装 FTP 服务器

![](img/11709a8f88c8cd03868a929dc94c0e2b_632_0.png)

根据您在 Linux 安装期间所做的选择，FTP 服务器 `vsftpd` 及其配置文件可能已经安装在您的系统上。如果未安装 `vsftpd`，您可以轻松地安装它。

在 Debian 和 Xandros 中，输入 `dpkg -l *ftp*` 以查看是否安装了 FTP 服务器。在 Fedora Core 和 SUSE 中，输入 `rpm -qa | grep vsftp` 并查看是否安装了 `vsftpd` 包。

在 Debian 和 MEPIS 中，输入 `apt-get install vsftpd` 以安装 FTP 服务器。在 Ubuntu 中，输入 `sudo apt-get install vsftpd`。在 Fedora Core 中，以 `root` 身份登录，挂载 DVD，然后输入 `cd /media/cdrom/Fedora/RPMS`，接着输入 `rpm -ivh vsftpd*`。在 SUSE 中，点击 YaST 控制中心软件类别中的软件管理。然后使用 YaST 的搜索功能找到 `vsftpd` 并安装它。在 Xandros 中，首先运行 Xandros Networks，选择编辑->设置应用程序源，并点击 Debian Unsupported Site 链接作为源；然后您可以使用 `apt-get install vsftpd` 命令安装非常安全的 FTP 服务器。




###### 配置 FTP 服务器

Very Secure FTP 守护程序（`vsftpd`）使用 `/etc` 目录（在 Fedora Core 中为 `/etc/vsftpd` 目录）下的多个配置文件。默认情况下，`vsftpd` 服务器是禁用的——如果您想使用 FTP 服务器，首先必须启用它。在本节中，我将向您展示如何操作。

`vsftpd` 服务器可以配置为以独立模式运行，或在 `xinetd` 服务器的控制下运行。在 Debian 和 Fedora Core 中，`vsftpd` 被设置为作为独立进程运行。在 SUSE 中，`vsftpd` 在 `xinetd` 的控制下运行。在 Debian 和 Fedora Core 中，您可以通过输入 `/etc/init.d/vsftpd start` 来启动 `vsftpd`。在 SUSE 中，编辑文件 `/etc/xinetd.d/vsftpd` —— 确保其中没有 `disable = yes` 行 —— 然后输入 `/etc/init.d/xinetd restart` 以重启 `xinetd`。

要在系统启动时启动 `vsftpd`，请在 Debian 中输入 `update-rc.d vsftpd defaults`。在 Fedora Core 中，通过输入 `chkconfig --level 35 vsftpd on` 来启用 `vsftpd` 的自动启动。

启动 `vsftpd` 服务器后，默认设置对于服务器来说已经足够有用。这是因为其他 FTP 客户端现在可以连接并向您的 FTP 服务器请求文件。然而，您需要了解这些配置文件，以防您以后需要对其进行自定义。

####### vsftpd 配置文件

`vsftpd` 服务器会参考 `vsftpd.conf` 文件（在 Debian、SUSE 和 Xandros 中位于 `/etc`，在 Fedora Core 中位于 `/etc/vsftpd` 目录——请记住，您必须在 Xandros 中先安装 `vsftpd`）。该配置文件可能会引用 `/etc` 目录中的其他文件。`vsftpd.conf` 文件控制 FTP 服务器的许多方面，例如它是否以独立模式运行、谁可以下载文件，以及是否允许匿名 FTP。`vsftpd` 的关键配置文件包括：

- `/etc/vsftpd.conf` 或 `/etc/vsftpd/vsftpd.conf` 控制 `vsftpd` 服务器的工作方式（例如，是否允许匿名登录、允许文件上传等）。
- `/etc/vsftpd.ftpusers`（如果存在）列出了无法访问 FTP 服务器的用户名称。
- `/etc/vsftpd.user_list`（如果存在）列出了被拒绝访问的用户名称（甚至不会提示输入密码）。但是，如果在 `/etc/vsftpd/vsftpd.conf` 中将 `userlist_deny` 选项设置为 NO，则允许这些用户访问 FTP 服务器。

![](img/11709a8f88c8cd03868a929dc94c0e2b_633_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_634_0.png)

在 Debian、SUSE 和 Xandros 中，`vsftpd` 使用单个配置文件 —— `/etc/vsftpd.conf`。在 Fedora Core 中，`vsftpd` 的默认安装使用 `/etc/vsftpd/vsftpd.conf` 文件。

通常，您可以保留大多数 `vsftpd` 配置文件的默认设置。但是，万一您需要更改某些内容以使 `vsftpd` 适合您的需求，我将在接下来的几个章节中简要解释这些配置文件。

######## vsftpd.conf 文件

要了解 `vsftpd.conf` 文件中可以包含什么内容，以及这些行如何影响 `vsftpd` 服务器的操作，首先查看默认安装的 `vsftpd.conf` 文件。该文件中的注释告诉您每个选项的作用。

默认情况下，`vsftpd` 几乎不允许任何操作。通过编辑 `vsftpd.conf` 中的选项，您可以放宽限制，以便用户可以使用 FTP。您可以决定设置的宽松程度。

以下是 `vsftpd.conf` 文件中可以设置的一些选项：

- `anon_mkdir_write_enable=YES` 允许匿名 FTP 用户创建新目录。此选项存在风险，因为恶意用户可能会通过创建过多目录来耗尽您的硬盘空间。因此，即使您允许匿名用户上传文件，您可能也想将此选项设置为 `NO`。
- `anon_upload_enable=YES` 意味着匿名 FTP 用户可以上传文件。只有当 `write_enable` 已设置为 `YES` 且目录对所有人具有写权限时，此选项才生效。**请记住：** 允许用户在您的系统上写入数据可能非常危险，因为用户可能会填满磁盘或将您的磁盘用作个人存储。
- `anonymous_enable=YES` 启用*匿名 FTP*（用户可以用户名 `anonymous` 登录，并输入他们的电子邮件地址作为密码。）如果您不想使用匿名 FTP，请注释掉此行。
- `ascii_download_enable=YES` 启用 ASCII 模式下的文件下载。不幸的是，恶意的远程用户可以发出带有巨大文件名的 `SIZE` 命令，从而基本上导致 FTP 服务器在打开该文件并确定其大小时浪费大量资源。这种技术用于拒绝服务攻击。（有关拒绝服务 [DoS] 攻击的更多信息，请参阅第六卷第一章。）
- `ascii_upload_enable=YES` 启用 ASCII 模式下的文件上传（适用于文本文件）。

![](img/11709a8f88c8cd03868a929dc94c0e2b_634_1.png)

- `async_abor_enable=YES` 使 vsftpd 能够识别在任何时间到达的 ABOR（中止）请求。您可能需要启用它，以允许较旧的 FTP 客户端与 vsftpd 配合工作。
- `banned_email_file=/etc/vsftpd.banned_emails` 指定包含被禁用的电子邮件地址列表的文件（仅在 deny_email_enable 设置为 YES 时使用）。
- `chown_uploads=YES` 导致上传的匿名文件的所有者由 chown_username 选项指定的另一个用户拥有。除非绝对必要，否则不要启用此选项——并且不要指定 root 作为 chown_username。（那是一场等待发生的灾难。）如果某个在特定用户名下运行的进程使用上传的文件，这意味着无论谁上传文件，所有者都必须更改为该进程预期的用户名，您可能需要启用此选项。
- `chown_username=name` 指定由匿名 FTP 用户上传的文件的拥有者用户名。
- `chroot_list_enable=YES` 使 vsftpd 在用户登录 FTP 服务时，将除 chroot_list_file 指定列表中的用户外的所有用户限制在其主目录中。此选项可以防止这些用户访问其主目录以外的任何文件。默认情况下，vsftpd 在 /etc/vsftpd.chroot_list 文件中查找 chroot 用户列表，但您可以通过 chroot_list_file 选项指定文件名来覆盖此设置。
- `chroot_list_file=/etc/vsftpd.chroot_list` 是用户列表，根据 chroot_local_user 的设置，这些用户要么被限制在其主目录中，要么不被限制。
- `connect_from_port_20=YES` 使 vsftpd 确保数据传输通过 20 端口（FTP 数据端口）进行。
- `data_connection_timeout=120` 是未活动数据连接超时后的秒数。
- `deny_email_enable=YES` 使 vsftpd 检查被禁用的电子邮件地址列表，并拒绝任何试图使用被禁用的电子邮件地址作为密码匿名登录的人。默认情况下，vsftpd 期望被禁用的电子邮件地址位于 /etc/vsftpd.banned_emails 文件中，但您可以通过 banned_email_file 选项指定另一个文件名。
- `dirmessage_enable=YES` 使 vsftpd 在 FTP 用户切换到某些目录时显示消息。
- `ftpd_banner=Welcome to my FTP service` 设置用户登录时 vsftpd 显示的横幅。您可以将消息更改为任何您想要的内容。
- `idle_session_timeout=600` 是*空闲会话*（指某人连接但不做任何事情的情况）超时并 vsftpd 注销用户的秒数。
- `listen=YES` 使 vsftpd 监听连接请求，并因此以独立模式运行。如果您希望在 xinetd 下运行 vsftpd，请将此选项设置为 NO。
- `local_enable=YES` 使 vsftpd 授予本地用户访问 FTP 的权限。
- `local_umask=022` 意味着 FTP 写入的任何文件具有 644 权限（所有人可读，但仅所有者可写）。您可以将其设置为任何文件权限掩码设置。例如，如果您不想让除所有者以外的任何人拥有权限，请将该选项更改为 077。（要了解有关文件权限掩码的更多信息，请参阅第六卷第二章。）
- `ls_recurse_enable=YES` 允许 FTP 用户通过使用 `ls -R` 命令递归遍历目录。
- `nopriv_user=ftp` 标识 FTP 服务器可以使用的无权限用户账户。
- `pam_service_name=vsftpd` 是可插拔身份验证模块 (PAM) 配置文件的名称，当 vsftpd 必须对用户进行身份验证时使用该文件。默认情况下，PAM 配置文件位于 /etc/pam.d 目录中。这意味着 vsftpd 的 PAM 配置文件是 /etc/pam.d/vsftpd。
- `tcp_wrappers=YES` 启用通过 TCP wrapper 的支持，该 wrapper 参考 /etc/hosts.allow 和 /etc/hosts.deny 文件进行访问控制。（有关 TCP wrapper 的更多信息，请参阅第六卷第三章。）
- `userlist_deny=YES` 使 vsftpd 拒绝访问 /etc/vsftpd.user_list 文件中列出的用户，前提是 userlist_enable 设置为 YES。这些用户甚至不会收到密码提示。另一方面，如果您将 userlist_deny 设置为 NO，除非用户列在 /etc/vsftpd.user_list 文件中，否则他们将无法访问。
- `userlist_enable=YES` 使 vsftpd 从 /etc/vsftpd.user_list 文件读取用户列表，并拒绝这些用户访问 FTP 服务器，甚至不会提示输入密码。默认用户列表是 /etc/vsftpd.user_list，但您可以通过 userlist_file 选项覆盖此设置。
- `write_enable=YES` 使 vsftpd 允许向主机上传文件。
- `xferlog_enable=YES` 开启文件下载和上传的日志记录（通常是个好主意，但占用磁盘空间）。




- `xferlog_file=/var/log/vsftpd.log` 指定了 vsftpd 日志文件的完整路径名。默认值为 `/var/log/vsftpd.log`。
- `xferlog_std_format=YES` 使 vsftpd 以其他 FTP 守护程序使用的标准格式生成日志文件。

######## /etc/vsftpd.ftpusers 文件

当用户尝试登录时，vsftpd 服务器使用 PAM 对用户进行身份验证（正如普通登录过程使用 PAM 来完成此任务一样）。vsftpd 的 PAM 配置文件是 `/etc/pam.d/vsftpd`。该 PAM 配置文件对 `/etc/vsftpd.ftpusers` 的引用如下：

```bash
auth    required     /lib/security/pam_listfile.so item=user sense=deny
              file=/etc/vsftpd.ftpusers sense=succeed
```

该命令基本上表示：任何列在 `/etc/vsftpd.ftpusers` 文件中的用户都将被拒绝登录。

根据发行版的不同，`/etc/pam.d/vsftpd` 文件可能会引用除 `/etc/vsftpd.ftpusers` 之外的其他文件名。例如，在 Fedora Core 中，`/etc/pam.d/vsftpd` 文件指定 `/etc/vsftpd/ftpusers` 为包含拒绝登录用户名的文件，而 SUSE Linux 使用 `/etc/ftpusers` 文件来列出不允许访问 vsftpd 的用户名。通常，该列表被设置为拒绝如 `root`、`news`、`uucp` 等与服务器相关而非真实用户的 FTP 访问。

![](img/11709a8f88c8cd03868a929dc94c0e2b_637_0.png)

######## /etc/vsftpd.user_list 文件

如果 `userlist_enable` 选项设置为 `YES` 且 `userlist_deny` 设置为 `YES`，则 vsftpd 不允许列在 `/etc/vsftpd.user_list` 文件中的用户访问任何 FTP 服务。它甚至不会提示他们输入密码。然而，如果 `userlist_deny` 设置为 `NO`，则含义相反，这些用户是允许访问的唯一用户。（但 PAM 配置仍然会拒绝 `/etc/vsftpd.ftpusers` 列表中的任何人。）如果 `userlist_enable` 设置为 `NO`，则不使用 `/etc/vsftpd.user_list` 文件。

在 Fedora Core 中，vsftpd 使用 `/etc/vsftpd/user_list` 中的用户列表来作为 `userlist_enable` 和 `userlist_deny` 选项的依据。

![](img/11709a8f88c8cd03868a929dc94c0e2b_637_1.png)

##### 第 4 章：管理和新闻服务器

本章内容

- 安装和使用 sendmail
- 手动测试邮件投递
- 配置 sendmail
- 安装 InterNetNews (INN) 服务器
- 配置和启动 INN
- 设置本地新闻组

电子邮件（e-mail）是互联网主机上提供的流行服务之一。电子邮件软件由两部分组成：邮件传输代理（MTA），负责物理发送和接收邮件消息；以及邮件用户代理（MUA），负责读取消息和准备新消息。在本章中，我将描述电子邮件服务并展示如何在 Linux PC 上配置 sendmail 服务器。

互联网新闻组提供了除电子邮件之外另一种方便的方式来讨论各种主题并与他人分享知识。Linux 自带了阅读新闻组以及将您的系统设置为新闻服务器所需的软件。在本章中，我将描述如何配置和运行流行的 InterNetNews 服务器。我还将展示如何为您的公司内联网（甚至您的家庭网络）设置本地新闻组。

###### 安装邮件服务器

根据您在 Linux 安装期间所做的选择，您可能已经安装了系统上的邮件服务器软件。您可以从几种邮件服务器中进行选择，例如 *exim*、*postfix* 和 *sendmail*——我将在本章中简要介绍 *sendmail*。如果 *sendmail* 未安装，您可以轻松安装它。

在 Debian、MEPIS、Ubuntu 和 Xandros 中，输入 `dpkg -i sendmail*` 以查看是否已安装 *sendmail*。在 Fedora Core 和 SUSE 中，输入 `rpm -qa | grep sendmail` 以查看是否已安装 *sendmail* 软件包。

![](img/11709a8f88c8cd03868a929dc94c0e2b_638_0.png)

在 Debian、MEPIS 和 Ubuntu 中，输入 `apt-get install sendmail` 以安装 sendmail 服务器。在 Fedora Core 中，以 *root* 身份登录，挂载 DVD，输入 `cd /media/cdrom/fedora/RPMS` 然后输入 `rpm -ivh sendmail*`。在 SUSE 中，点击 YaST 控制中心的软件类别中的“软件管理”。然后使用 YaST 的搜索功能找到 *sendmail* 软件包并安装它们。

####### 使用 sendmail

要将您的系统设置为邮件服务器，您必须正确配置 *sendmail* 邮件传输代理。*sendmail* 以其复杂但完整的邮件投递系统而闻名。只要看一眼 *sendmail* 的配置文件——Fedora Core 中的 `/etc/mail/sendmail.cf` 和 SUSE 中的 `/etc/sendmail.cf`——就能让您确信 *sendmail* 确实很复杂。幸运的是，您不需要成为 *sendmail* 配置文件的专家。您只需要一个预定义的配置文件——比如安装在您系统上的那个——就可以使用 *sendmail*。

您的系统已经拥有一个可用的 *sendmail* 配置文件——`/etc/mail/sendmail.cf`。默认文件假设您拥有互联网连接和名称服务器。只要您拥有互联网连接，并且您的系统拥有官方域名，您就可以从您的 Linux PC 发送和接收电子邮件。

为了确保邮件投递正常工作，您的系统名称必须与您的 ISP 分配给您的系统名称相匹配。虽然您可以给您的系统任何主机名，但只有当您的系统名称在 ISP 的名称服务器中时，其他系统才能成功地将邮件投递到您的位置。

######## 邮件投递测试

为了试用 *sendmail* 邮件传输代理，您可以使用 *mail* 命令向 Linux 系统上的任何用户账户编写并发送电子邮件。例如，这是我使用 *mail* 命令给自己发送消息的方法。（我的输入以粗体显示。）

```
mail naba
Subject: Testing e-mail
This is from my Linux system.
.
```

*mail* 命令是一个简单的邮件用户代理。在前面的示例中，我在命令行中指定了收件人（*naba*）。*mail* 程序提示输入主题行。在主题之后，我输入我的消息并以包含单个点的行结束。在我结束消息后，邮件用户代理将消息传递给 sendmail（邮件传输代理），以将其投递到指定地址。sendmail 立即投递电子邮件消息。要验证邮件投递，输入 `mail` 以再次运行 mail 命令并读取消息。

因此，初始的 sendmail 配置文件足以发送和接收电子邮件，至少在您的 Linux 系统内部如此。外部邮件投递也能正常工作，前提是您的 Linux 系统拥有互联网连接和已注册的域名。

![](img/11709a8f88c8cd03868a929dc94c0e2b_640_0.png)

如果您有一个为您的 Linux 系统提供动态 IP 地址的 ISP 账户，您必须使用诸如 Evolution 或 Mozilla Mail 等邮件客户端，通过联系您的 ISP 邮件服务器来投递出站电子邮件。

######## 邮件投递机制

在互联网主机上，sendmail 邮件传输代理使用简单邮件传输协议（SMTP）来投递邮件。基于 SMTP 的邮件传输代理监听 TCP 端口 25，并使用一组小的文本命令与其他邮件传输代理交换信息。事实上，SMTP 命令足够简单，您可以从终端手动使用它们来发送电子邮件消息。以下示例展示了如何从在同一系统上运行的 telnet 会话中使用 SMTP 命令向 Linux PC 上的我的账户发送电子邮件消息。（我的输入以粗体显示。）

```
telnet localhost 25
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
220 linux.site ESMTP Sendmail 8.13.4/8.13.4/SUSE Linux 0.9; Sat, 3 Sep 2005
14:10:06-0400
help
214-2.0.0 This is sendmail version 8.13.4
214-2.0.0 Topics:
214-2.0.0        HELO      EHLO      MAIL      RCPT      DATA
214-2.0.0        RSET      NOOP      QUIT      HELP      VRFY
214-2.0.0        EXPN      VERB      ETRN      DSN       AUTH
214-2.0.0        STARTTLS
214-2.0.0 For more info use "HELP <topic>".
214-2.0.0 To report bugs in the implementation send mail to
214-2.0.0        sendmail-bugs@sendmail.org.
214-2.0.0 For local information send email to Postmaster at your site.
214 2.0.0 End of HELP info
help DATA
214-2.0.0 DATA
214-2.0.0        Following text is collected as the message.
214-2.0.0        End with a single dot.
214 2.0.0 End of HELP info
HELO localhost
250 linux.site Hello localhost [127.0.0.1], pleased to meet you
```





######## Telnet 会话

MAIL FROM: naba
553 5.1.4 naba... 发件人地址 naba 需要域名
MAIL FROM: naba@localhost
250 2.1.0 naba@localhost... 发件人 ok
RCPT TO: naba
250 2.1.5 naba... 收件人 ok
DATA
354 输入邮件内容，以单独一行的“.”结束
Testing... 1 2 3
Sending mail by telnet to port 25
.
250 2.0.0 j831a6m0D05251 邮件已接受进行投递
quit
221 2.0.0 linux.site 正在关闭连接
Connection closed by foreign host.

telnet 命令开启了一个连接到端口 25 的 TELNET 会话（即 sendmail 期望接收 SMTP 命令的端口）。Linux 系统上的 sendmail 进程立即以一条通告消息回复。

我输入 HELP 以查看 SMTP 命令列表。若要获取特定命令的帮助信息，我可以输入 `HELP 命令名`。以下列表显示了当我输入 `HELP DATA` 时 sendmail 打印的帮助信息。

我输入 `HELO localhost` 以向主机发起会话。sendmail 进程以问候语回复。要发送邮件消息，我先使用指定消息发件人的 `MAIL FROM:` 命令。（我输入的是我正在发送消息的源系统上的用户名。）sendmail 要求除了用户名外还需要提供域名。

接下来，我使用 `RCPT TO:` 命令来指定消息的收件人。如果我想将消息发送给多个收件人，只需为每个收件人提供地址并使用 `RCPT TO:` 命令即可。

要输入邮件正文，我使用 `DATA` 命令。作为对 `DATA` 命令的响应，sendmail 显示一条指示，要求我必须以一个单独一行的句点结束消息。我输入正文并以单独一行的单个句点结束。sendmail 进程显示一条消息，表明该邮件已被接受进行投递。最后，我使用 `QUIT` 命令退出 sendmail 会话。

之后，我登录到我的 Linux 系统并使用 `mail` 命令检查邮件。以下是当我显示通过 sendmail 示例 SMTP 会话发送的邮件消息时，`mail` 命令的会话内容。（我的输入以粗体显示。）

mail
mailx version mail 11.4 8/29/04. Type ? for help.
"/var/mail/naba": 1 message 1 new

>N 1 naba@linux.site  Sat Sep  3 14:11    14/464
? l
   Message  1:
From naba@linux.site  Sat Sep  3 14:11:57 2005
Date: Sat,  3 Sep 2005 14:10:06 -0400
From: Naba Barkakati <naba@linux.site>
To: undisclosed-recipients:;

Testing... 1 2 3
Sending mail by telnet to port 25
? q
Saved 1 message in mbox

在这里，我输入 **mail** 以启动邮件程序。它显示新邮件的编号列表（在这种情况下，只有一封邮件）和一个提示符（?）。我输入 1（我想阅读的那封邮件的编号）。邮件程序显示该邮件并再次等待我的输入。我输入 **q** 以退出程序。

如图所示例所示，SMTP 命令足够简单，易于人类理解。这个示例有助于理解邮件传输代理如何在 Internet 上使用 SMTP 传输邮件。当然，电子邮件程序通常会自动化整个流程——**sendmail** 程序也是如此（通过 **sendmail** 配置文件 **sendmail.cf** 中的设置）。

######## sendmail 配置文件

你不需要理解 **sendmail** 配置文件 **sendmail.cf** 中的所有内容，但你需要知道该文件是如何创建的。这样，如有必要，你可以进行小的更改并重新生成 **sendmail.cf** 文件。

在 SUSE 中，你可以通过 YaST 控制中心配置 **sendmail**——选择 主菜单 → 系统 → 控制中心 (YaST)——点击窗口左侧的“网络服务”，然后点击窗口右侧的“邮件传输代理”。YaST 显示一个窗口（见图 4-1），你可以用它来配置 **sendmail**。首先你指定一般设置，然后是出站邮件设置，最后是入站邮件设置。当你退出邮件配置实用程序后，YaST 将邮件设置存储在 `*/etc/sysconfig/sendmail*` 和 `*/etc/sysconfig/mail*` 文件中，并通过运行 **SuSEconfig** 更新 **sendmail** 配置文件 `*/etc/sendmail.cf*`。

![](img/11709a8f88c8cd03868a929dc94c0e2b_642_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_642_1.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_643_0.png)

图 4-1：在 SUSE 中，你可以通过 YaST 配置 sendmail。

你也可以从一些 *m4 宏文件*（文本文件，其中每一行最终扩展为对某个程序有意义的多行内容）生成 *sendmail.cf* 文件。这些宏文件组织在 Fedora Core 的 `/usr/share/sendmail-cf` 目录或 SUSE 的 `/usr/share/sendmail` 目录中的若干子目录下。你可以阅读该目录中的 README 文件，以了解更多关于 *sendmail* 配置文件创建的信息。

######## m4 宏处理器

*m4* 宏处理器生成 *sendmail.cf* 配置文件，该文件随 Linux 中的 *sendmail* 软件包提供。主要宏文件，命名为 *sendmail.mc*、*generic_linux.mc* 或 *linux.mc*，包含在 *sendmail* 软件包中。

那么宏是什么？*宏*基本上是一种处理某些操作的代码的符号名称，通常以简写形式代替一长串字符。像 *m4* 这样的*宏处理器*通常读取其输入文件并将其复制到输出，同时沿路处理宏。宏的处理通常涉及执行某些操作并生成一些输出。因为宏在输出中生成的文本远多于仅仅是宏的名称，所以宏的处理被称为*宏扩展*。

![](img/11709a8f88c8cd03868a929dc94c0e2b_643_1.png)

###### 安装邮件服务器

m4 宏处理器是基于流的。这意味着在忙于扩展任何宏的同时，它将输入字符复制到输出。m4 宏处理器没有“行”的概念，因此它将换行符（标记行末尾的字符）复制到输出中。这就是为什么你在大多数 m4 宏文件中看到 `dnl` 这个词；`dnl` 是一个 m4 宏，代表“删除直到换行符”。`dnl` 宏删除从 `dnl` 开始到下一个换行符（包括该换行符）为止的所有字符。输出中的换行符不会造成任何危害；它们只是产生不必要的空行。sendmail 宏包使用 `dnl` 来避免输出配置文件中出现这样的空行。因为 `dnl` 基本上意味着“删除直到行尾的所有内容”，所以 m4 宏文件也将 `dnl` 用作注释行的前缀。

要查看 m4 的一个非常简单的用例，请考虑以下 m4 宏文件，它定义了两个宏 —— `hello` 和 `bye` —— 并在信函格式中使用它们：

dnl ###################################################
dnl # File: ex.m4
dnl # A simple example of m4 macros
dnl #####################################################
define('hello','Dear Sir/Madam')dnl
define('bye',
'Sincerely,
Customer Service')dnl
dnl Now type the letter and use the macros
hello,

This is to inform you that we received your recent
inquiry.
We will respond to your question soon.

bye

使用你喜欢的文本编辑器输入这段文本并将其保存为名为 `ex.m4` 的文件。你可以将宏文件命名为任何你喜欢的名称，但使用 `.m4` 扩展名作为 m4 宏文件的名称是惯例。

在使用 m4 处理宏文件之前，请注意该示例的以下关键点：

- 使用 `dnl` 宏开始所有注释行，如示例中的前四行所示。
- 以 `dnl` 宏结束每个宏定义。否则，当 m4 处理宏文件时，它会为每个宏定义产生一个空行。
- 使用内置的 `m4` 命令 `define` 来定义一个新宏。宏名称和值都用左右引号对 (`('...')`) 包围。注意，你不能使用普通的单引号来包围宏名称和定义。

![](img/11709a8f88c8cd03868a929dc94c0e2b_644_0.png)

现在通过键入以下命令来处理宏文件 `ex.m4`：

m4 ex.m4

`m4` 处理宏并显示以下输出：

Dear Sir/Madam,

This is to inform you that we received your recent
inquiry.
We will respond to your question soon.
Sincerely,

Customer Service

听起来就像典型的客户服务信函格式，不是吗？

如果你将输出与 `ex.m4` 文件进行比较，你会发现 `m4` 在标准输出上打印信函格式，并将宏 `hello` 和 `bye` 扩展为其定义的值。如果你想将信函格式保存为名为 `letter` 的文件，请使用 shell 的输出重定向功能，如下所示：

m4 ex.m4 > letter

如果你想在不扩展单词 *hello* 或 *bye* 的情况下在信函中使用它们怎么办？你可以通过用单引号对 (`('...')`) 包围这些单词来实现。对于其他预定义的 `m4` 宏（例如 *define*），你也必须这样做。要将 *define* 作为普通单词使用，而不是作为要扩展的宏，请键入 `"define"`。

######## sendmail 宏文件

前一节中的简单示例让你对如何定义 `m4` 宏并使用它们创建诸如 `sendmail.cf` 文件之类的配置文件有了一个概念。在 Fedora Core 的 `/usr/share/sendmail-cf` 目录或 SUSE 的 `/usr/share/sendmail` 目录中的文件中存储了许多复杂的宏。本节后半部分描述的一个顶级宏文件——在 Fedora Core 中称为 `sendmail.mc`，在 SUSE 中称为 `linux.mc`——使用 `include` 宏（用于将文件复制到输入流中）引入这些宏文件。




###### 安装邮件服务器

为了避免针对 Fedora Core 和 SUSE 等不同发行版反复提及不同的文件和目录名称，我在以下讨论中使用 Fedora Core 的文件和目录名称。这些通用讨论适用于所有 Linux 发行版中的 sendmail，但你必须将这些文件和目录名称替换为你特定发行版的对应项。

通过在位于 `/usr/share/sendmail-cf` 目录下的文件中定义自己的一组高级宏，sendmail 本质上创建了自己的宏语言。`sendmail` 宏文件使用 `.mc` 扩展名。你配置的主要 sendmail 宏文件是 `sendmail.mc`，它位于 `/etc/mail` 目录中。

与 `/etc/mail/sendmail.cf` 文件相比，`/etc/mail/sendmail.mc` 文件更短，且更易于操作。以下是随 Fedora Core 附带的 `/etc/mail/sendmail.mc` 文件中的几行代码：

```
dnl divert(-1)dnl
dnl #
dnl # This is the sendmail macro config file for m4. If you make changes to
dnl # /etc/mail/sendmail.mc, you will need to regenerate the
dnl # /etc/mail/sendmail.cf file by confirming that the sendmail-cf package is
dnl # installed and then performing a
dnl #
dnl # make -C /etc/mail
dnl #
include `/usr/share/sendmail-cf/m4/cf/'dnl
VERSIONID(`setup for Red Hat Linux')dnl
OSTYPE(`linux')dnl
dnl #
dnl # default logging level is 9, you might want to set it higher to
dnl # debug the configuration
dnl #
dnl define(`confLOG_LEVEL', `9')dnl
dnl #
dnl # Uncomment and edit the following line if your outgoing mail needs to
dnl # be sent out through an external mail server:
dnl #
dnl define(`SMART_HOST', `smtp.comcast.net')
...lines deleted ...
dnl #
dnl MASQUERADE_AS('mydomain.com')dnl
dnl #
dnl # masquerade not just the headers, but the envelope as well
dnl #
dnl FEATURE(masquerade_envelope)dnl
dnl #
dnl # masquerade not just @mydomainalias.com, but *.mydomainalias.com as well
dnl #
dnl FEATURE(masquerade_entire_domain)dnl
dnl MASQUERADE_DOMAIN(localhost.localdomain)dnl
dnl MASQUERADE_DOMAIN(mydomainalias.com)dnl
dnl MASQUERADE_DOMAIN(mydomain.lan)dnl
```

MAILER(smtp)dnl
MAILER(procmail)dnl
dnl MAILER(cyrusv2)dnl

> 如果你修改了 `/etc/mail/sendmail.mc` 文件，你必须通过以下命令将 `sendmail.mc` 文件通过 `m4` 宏处理器生成 `/etc/mail/sendmail.cf` 文件。（你需要以 **root** 身份登录。）

```
m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf
```

注释还告诉你，你需要 `sendmail-cf` 包来处理此文件。

根据前一节对 `m4` 宏的描述，你可以看到 `sendmail.mc` 文件使用 `define` 来创建新宏。你还可以看到大量使用 `dnl` 来避免在输出中插入过多的空行。

其他大写单词（如 `OSTYPE`、`FEATURE` 和 `MAILER`）是 `sendmail` 宏。这些宏定义在位于 `/usr/share/sendmail-cf` 目录子目录中的 `.m4` 文件中，并通过以下 `include` 宏整合到 `sendmail.mc` 文件中：

```
include(`/usr/share/sendmail-cf/m4/cf.m4')dnl
```

反过来，`/usr/share/sendmail-cf/m4/cf.m4` 文件包含 `cfeead.m4` 文件，后者又包含其他 `m4` 文件，依此类推。最终结果是，当 `m4` 宏处理器处理 `sendmail.mc` 文件时，宏处理器会整合来自 `/usr/share/sendmail-cf` 各个子目录中的许多 `m4` 文件。

以下是关于 `/etc/mail/sendmail.mc` 文件的一些要点：

- **VERSIONID**(`setup for Red Hat Linux') 宏将引号内的版本信息插入到输出中。
- **OSTYPE**(`linux') 指定操作系统为 Linux。你必须尽早指定此宏以确保正确的配置。习惯上将此宏放在 **VERSIONID** 宏之后。
- **MAILER**(smtp) 描述邮件服务器。根据 `/usr/share/sendmail-cf/README` 文件中的说明，**MAILER** 声明始终放置在 `sendmail.mc` 文件的末尾，并且 **MAILER**(smtp) 始终位于 **MAILER**(procmail) 之前。邮件服务器 **smtp** 指的是 SMTP 邮件服务器。
- **FEATURE** 宏请求各种特殊功能。例如，FEATURE(`blacklist_recipients') 开启了对特定用户名、主机或地址的传入邮件进行拦截的能力。关于允许或拒绝哪些邮件的规范被放置在访问数据库中（存储于 `/etc/mail/access_db` 文件）。你还需要 FEATURE(`access_db') 宏来开启访问数据库。
- **MASQUERADE_AS**(`mydomain.com`) 使 sendmail 将外发邮件标记为来自主机 `mydomain.com`（替换为你的域名）。其想法是大型组织设置单一的 sendmail 服务器来处理许多子域的邮件，并让所有内容看起来都来自同一个域。（例如，大学内许多部门的邮件看起来都来自大学的主域名。）
- **MASQUERADE_DOMAIN**(subdomain.mydomain.com) 指示 sendmail 将来自如 `user@subdomain.mydomain.com` 这样的地址的邮件，标记为起源于由 **MASQUERADE_AS** 宏指定的域中的相同用户名。

FEATURE 和 MAILER 等 sendmail 宏在 `/usr/share/sendmail-cf/README` 文件中有描述。在修改 `sendmail.mc` 文件之前，请查阅该文件以了解有关 sendmail 宏的更多信息。

######## sendmail.cf 文件语法

`sendmail.cf` 文件的语法设计旨在易于 sendmail 程序解析，因为 sendmail 在每次启动时都会读取此文件。设计该文件语法时，人类可读性并非主要考虑因素。尽管如此，稍加解释，你就能理解 `sendmail.cf` 中控制行的含义。

每个 sendmail 控制行都以一个单字母运算符开头，该运算符定义了该行其余部分的含义。以空格或制表符开头的行被视为上一行的延续。空行和以井号（#）开头的行是注释。

通常，单字母运算符和其后的参数之间没有空格，这使得这些行更难理解。例如，`sendmail.cf` 使用了类的概念——本质上是一个短语集合。你可以定义一个名为 P 的类，并使用以下控制行将该类中添加短语 REDIRECT：

```
CPREDIRECT
```

由于所有字符都挤在一起，该命令很难解读。另一方面，若要定义一个名为 Accept 的类并将其值设置为 OK 和 RELAY，请编写以下内容：

```
C(Accept)OK RELAY
```

这个命令可能更容易理解，因为分隔符（如类名 Accept）被花括号包围。

其他——较新的——控制行甚至更容易理解。例如，该行：

```
O HelpFile=/etc/mail/helpfile
```

定义了选项 HelpFile 为文件名 `/etc/mail/helpfile`。该文件包含 sendmail 在接收到 HELP 命令时使用的帮助信息。

表 4-1 总结了 *sendmail.cf* 中使用的单字母控制运算符。每个条目还显示了该运算符的示例。此表有助于你理解 *sendmail.cf* 中的一些行。

| 运算符 | 描述 |
| :--- | :--- |
| C | 定义一个类；一个变量（可视为一个集合），可以包含多个值。例如，`Cwlocalhost` 将名称 `localhost` 添加到类 `w` 中。 |
| D | 定义一个宏，即与单个值关联的名称。例如，`Dtm` 或 `DtMAILER-DAEMON` 将宏 `m` 定义为 `MAILER-DAEMON`。 |
| F | 定义从文件读取的类。例如，`Fw/etc/mail/local-host-names` 从文件 `/etc/mail/local-host-names` 读取主机名称并将其添加到类 `w` 中。 |
| H | 定义 sendmail 插入到消息中的头部行的格式。例如，`HP??Return-Path: <$g>` 定义了头部的 `Return-Path:` 字段。 |
| K | 定义一个映射（键值对数据库）。例如，`Karith arith` 将名为 `arith` 的映射定义为同名内置映射。 |
| M | 指定一个邮件服务器。以下行定义了 procmail 邮件服务器：`Mp=procmail`, `Pe=/usr/bin/procmail`, `F=DFGSPhnu9`, `S=EnvFromSMTP/HdrFromSMTP`, `R=EnvToSMTP/HdrFromSMTP`, `T=DNS/RFC822/X-Unix`, `A=procmail -Y -m $h $f $u`。 |





| 运算符 | 描述 |
| :--- | :--- |
| O | 将值分配给一个选项。例如，`O AliasFile=/etc/aliases` 将 `AliasFile` 选项定义为 `/etc/aliases`，这是 sendmail 别名文件的名称。 |
| P | 定义优先级字段的值。例如，`P junk=-100` 将标有 `Precedence: junk` 头部字段的消息优先级设置为 -100。 |
| R | 定义一条规则。（规则包含左侧和右侧；如果输入匹配左侧，则用右侧替换它。此规则称为重写。）例如，重写规则 `R $* : $1` 用于去除末尾的分号。 |
| S | 标记一个规则集，您可以从后续的 R 控制行开始定义它。例如，`S canonify=3` 将下一个规则集标记为 `canonify` 或规则集 3。 |
| T | 将用户名添加到受信任类（class t）中。例如，`T root` 将 root 添加到受信任用户类中。 |
| V | 定义配置文件的主版本号。例如，`V 10/Berkeley` 将版本号定义为 10。 |

######## 其他 sendmail 文件

`/etc/mail` 目录包含 sendmail 使用的其他文件。这些文件在 sendmail 配置文件中被引用，在 Fedora Core 中为 `/etc/mail/sendmail.cf`，在 SUSE 中为 `/etc/sendmail.cf`。例如，以下是如何在 Fedora Core 的 `/etc/mail/sendmail.cf` 文件中搜索 `/etc/mail` 字符串的方法：

```
grep "/etc/mail" /etc/mail/sendmail.cf
```

以下是我的 Fedora Core 系统上 grep 命令搜索结果：

```
Pw/etc/mail/local-host-names
PR-o /etc/mail/relay-domains
Kmailer table hash -o /etc/mail/mailertable.db
Kvirth user hash -o /etc/mail/virthuser table.db
Kaccess hash -To<TMPF> -o /etc/mail/access.db
#0 ErrorHeader=/etc/mail/error-header
O HelpFile=/etc/mail/helpfile
O UserDatabaseSpec=/etc/mail/userdb.db
#0 ServiceSwitchFile=/etc/mail/service.switch
#0 DefaultAuthInfo=/etc/mail/default-auth-info
Pt/etc/mail/trusted-users
```

您可以忽略以井号或数字符号 (#) 开头的行，因为 sendmail 将这些行视为注释。其他行是引用 `/etc/mail` 目录中其他文件的 sendmail 控制行。

以下是这些 sendmail 文件中的一些内容示例。（请注意，并非所有这些文件都必须存在于 `/etc/mail` 目录中，即使存在，某些文件也可能是空的。）

- `/etc/mail/access`: 允许发送邮件的主机名称和/或 IP 地址（有助于阻止垃圾邮件 — 不需要的电子邮件）
- `/etc/mail/access.db`: 从 `/etc/mail/access` 文件生成的访问数据库
- `/etc/mail/helpfile`: SMTP 命令的帮助信息
- `/etc/mail/local-host-names`: 本机已知的主机名称
- `/etc/mail/mailertable`: 用于覆盖邮件路由方式的邮件器表（例如，条目 `comcast.net comcast:smtp.comcast.net` 告诉 sendmail，发往 `comcast.net` 的邮件必须发送到 `smtp.comcast.net`。）
- `/etc/mail/relay-domains`: 允许中继的主机
- `/etc/mail/trusted-users`: 允许使用其他用户名发送邮件而不产生警告的用户列表
- `/etc/mail/userdb.db`: 包含每个用户登录名和真实名称信息的用户数据库文件
- `/etc/mail/virtusertable`: 托管在此系统上的虚拟域地址用户数据库

![](img/11709a8f88c8cd03868a929dc94c0e2b_651_0.png)

`/etc/mail` 目录有时还包含其他文件 — `/etc/mail/certs` 和带有 `.pem` 扩展名的文件 — 这些文件旨在通过使用 SMTP 的 STARTTLS 扩展来支持 sendmail 中的隐私增强邮件（PEM）。STARTTLS 扩展使用 TLS（更常被称为 SSL — 安全套接字层）来验证发送者并加密邮件。RFC 2487 描述了 STARTTLS。（此 RFC 在线可用，地址为 http://ietf.org/rfc/rfc2487.txt。）

如果您编辑了 `/etc/mail/mailertable` 文件，在更改生效之前，必须键入以下命令：

```
makemap hash /etc/mail/mailertable < /etc/mail/mailertable
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_651_1.png)

以下是确保在做出任何更改后重建所有必要内容的更简单方法 — 只需以 root 身份登录并键入以下命令：

```
cd /etc/mail
make
```

第一条命令将当前目录更改为 `/etc/mail`，第二条命令运行 make 命令，该命令读取 `/etc/mail` 中名为 Makefile 的文件来执行重建所有内容的必要步骤。（要了解有关 make 和 Makefile 的更多信息，请参阅第八卷，第一章。）

######## .forward 文件

用户可以在其主目录中放置一个 .forward 文件来重定向自己的邮件。.forward 文件是一个纯文本文件，包含以逗号分隔的邮件地址列表。发送给该用户的任何邮件都会转发到这些地址。如果 .forward 文件包含单个地址，则该用户的所有电子邮件都会重定向到该单个电子邮件地址。例如，假设在一个名为 emily 的用户的主目录中放置了一个包含以下行的 .forward 文件：

ashley

该行导致 sendmail 自动将所有发往 emily 的电子邮件发送到同一系统上名为 ashley 的用户。用户 emily 将完全收不到邮件。

您还可以通过列出完整的电子邮件地址将邮件转发到另一个系统上的用户名。例如，我添加了一个包含以下行的 .forward 文件，以便将我的消息（发往我的用户名 naba）发送到邮件地址 naba@comcast.net：

naba@comcast.net

现在假设我希望除了转发到 naba@comcast.net 地址外，还在原始系统上保留消息的副本。我可以通过在 .forward 文件中添加以下行来实现：

naba@comcast.net, naba\

我只需追加我的用户名，并在行尾添加一个反斜杠。行尾的反斜杠 (\) 会阻止 sendmail 反复转发消息（因为当副本发送到系统上我的用户名时，sendmail 通常会再次处理我的 .forward 文件）。反斜杠告诉 sendmail 不要反复转发消息。

![](img/11709a8f88c8cd03868a929dc94c0e2b_652_0.png)

除了 sendmail.cf 文件外，sendmail 还咨询名为 /etc/aliases 的别名文件，以将名称转换为地址。别名文件的位置出现在 sendmail 配置文件中。

每个别名通常是电子邮件地址的较短名称。系统管理员使用 sendmail 别名文件来转发邮件，创建邮件列表（识别多个用户的单个别名），或通过多个不同名称引用用户。例如，以下是一些典型的别名：

barkakati: naba
naba: naba@lnbsoft
all: naba, leha, ivy, emily, ashley

第一行表示发往 barkakati 的邮件将递送给本地系统中名为 naba 的用户。第二行表明 naba 的邮件实际上是发送到 lnbsoft 系统上的用户名 naba。最后一行将 all 定义为 naba、leha、ivy、emily 和 ashley 这五个用户的别名。这意味着发送到 all 的邮件会发送给这五个用户。

在 /etc/aliases 文件中定义任何新别名后，必须以 root 身份登录，并键入以下命令以使新别名生效：

sendmail -bi

###### 安装 INN 服务器

在本节中，我将描述如何配置 InterNetNews（INN），一个基于 TCP/IP 的新闻服务器。首先，您必须安装 INN。

在 Debian、MEPIS、Ubuntu 和 Xandros 中，键入 `dpkg -l inn*` 以查看是否已安装 inn。在 Fedora Core 和 SUSE 中，键入 `rpm -q inn` 以查看是否已安装 inn 软件包。

在 Debian、MEPIS 和 Ubuntu 中，键入 `apt-get install inn` 以安装 INN 服务器。在 Fedora Core 中，以 root 身份登录，挂载 DVD，然后键入 `cd /media/cdrom/Fedora/RPMS`，接着键入 `rpm -vh inn*`。在 SUSE 中，点击 YaST 控制中心“软件”类别中的“软件管理”。然后使用 YaST 的搜索功能查找 inn，从搜索结果中选择相关软件包并安装它们。在 Xandros 中，首先运行 Xandros Networks，选择“编辑”>“设置应用程序源”，并点击“Debian Unsupported Site”链接作为源。然后键入 `apt-get install inn` 以安装 INN 服务器。

![](img/11709a8f88c8cd03868a929dc94c0e2b_653_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_653_1.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_653_2.png)




###### 配置并启动 INN 服务器

安装完成后，大部分 INN 软件即可投入使用。您只需大致了解 INN 的各个组件，编辑配置文件，然后启动 innd（即 INN 服务器）即可。顺便提一下，有时我会将 INN 服务器称为新闻服务器。

如果您希望运行一个支持特定互联网新闻组选择的新式服务器，还需要安排新闻源（Feed）——即您的新闻服务器获取新闻组文章来源。通常，您可以从 ISP（互联网服务提供商）获取新闻源，但 ISP 会收取额外的月费，以覆盖提供该源所需的资源成本。（您正常的 ISP 费用涵盖从 ISP 服务器读取新闻；只有当您希望运行自己的服务器并获取新闻源时，才需要支付额外费用。）您需要提供提供新闻源的上游服务器名称，并向该服务器提供您的服务器名称以及您希望接收的新闻组。

顺带一提，如果您运行新闻服务器是为了支持仅在您组织网络内可用的本地新闻组，则无需外部新闻源。我在本章的“设置本地新闻组”部分中描述了如何设置本地新闻组。

根据您希望接收的新闻组以及您希望保留文章的天数，您必须预留相应的磁盘空间来存储文章。新闻组存储在系统的 /var/spool/news 目录下的目录层次结构中（基于新闻组名称）。如果您正在设置新闻服务器，您可能希望将一个大磁盘分区专门用于 /var/spool/news 目录。

在您的新闻服务器的配置文件中，输入提供新闻源的服务器名称。同时，在配置文件中添加任何从您的服务器接收新闻源的下游新闻服务器（如果有）的名称。然后，您可以启动新闻服务器并等待新闻到达。监控日志文件，以确保新闻文章在系统的 /var/spool/news 目录中正确排序和存储。

在接下来的章节中，我将介绍 INN 的设置，但您可以从互联网系统协会（ISC）那里了解更多关于 INN 的信息。ISC 是一家致力于开发和维护开源互联网软件（如 BIND（域名系统的实现）、DHCPC（动态主机配置协议）和 INN）的非营利公司。Rice Salze 最初编写了 INN；ISC 在 1996 年接管了 INN 的开发工作。您可以在 ISC 的 INN 网页 www.isc.org/sw/inn 上了解有关 INN 的更多信息并访问其他资源。

####### InterNetNews 组件

INN 包含几个用于分发和管理新闻组的程序。它还包含许多控制 INN 程序工作方式的文件。最重要的 INN 程序如下：

- innd：新闻服务器。它作为*守护进程*（一种后台进程，自身保持运行以提供特定服务）运行，并监听 NNTP 端口（TCP 端口 119）。innd 服务器接受来自其他源站点的连接，也接受来自本地新闻阅读器客户端的连接，但它将本地连接交给 nnrpd 处理。
- nnrpd：由 innd 调用的特殊服务器，用于处理来自本地新闻阅读器客户端的请求。
- expire：根据文本文件 /etc/news/expire.ctl 中的规范删除旧文章。
- nntp.send：调用 innewsmit 程序，使用 NNTP 将新闻文章发送到远程站点。配置文件 /etc/news/nntp_send.ctl 控制 nntp.send 程序。
- cti.innd：允许您交互式地控制 innd 服务器。cti.innd 程序可以向 innd 服务器的控制通道发送消息。

INN 的其他关键组件是控制文件。这些文件中的大多数位于您的 Linux 系统的 /etc/news 目录中，但少数位于 /var/lib/news 目录中。在这两个目录之间，您有超过 30 个 INN 控制文件。一些重要的文件包括：

- /etc/news/inn.conf：指定 innd 服务器的配置数据。（要查看此文件的在线帮助，请输入 **man inn.conf**。）
- /etc/news/newsfeeds：指定将哪些文章馈送到下游的其他新闻服务器。（该文件很复杂，但您可以通过输入 **man newsfeeds** 获取帮助。）
- /etc/news/incoming.conf：列出向此服务器提供新闻源的主机名称和地址。（要查看此文件的在线帮助，请输入 **man incoming.conf**。）
- /etc/news/storage.conf：指定存储新闻文章时使用的存储方法。（要查看此文件的在线帮助，请输入 **man storage.conf**。）
- /etc/news/expire.ctl：控制文章的过期，如果希望，可按每个新闻组级别控制。（要查看此文件的在线帮助，请输入 **man expire.ctl**。）
- /var/lib/news/active：列出所有活动的新闻组，显示每个新闻组的最旧和新文章编号，以及每个新闻组的发布状态。（要查看此文件的在线帮助，请输入 **man active**。）
- /var/lib/news/newsgroups：列出新闻组及其简要描述。
- /etc/news/readers.conf：指定允许从此新闻服务器读取新闻并向新闻组发布新闻的主机和用户。默认文件仅允许 **localhost** 读取新闻；如果您希望允许局域网中的其他主机读取新闻，则必须编辑它。（要查看此文件的在线帮助，请输入 **man readers.conf**。）

在接下来的几节中，我将描述如何设置一些重要的控制文件。

####### inn.conf 文件

此文件保存所有 INN 程序的配置数据——这使它成为最重要的文件。该文件的每一行都有参数值，格式如下：

```
parameter:    value
```

根据参数不同，该值可以是字符串、数字，或者是 *true* 或 *false*。与许多其他配置文件一样，注释行以数字或井号（#）开头。

默认 *inn.conf* 文件（位于 */etc/news* 目录中）的大多数参数不需要更改。您可能想要编辑表 4-2 中显示的一个或多个参数。

表 4-2 /etc/news/inn.conf 中的配置参数

| 参数名称 | 描述 |
| :--- | :--- |
| **mta** | 将此参数设置为用于启动邮件传输代理的命令，**innd** 使用该代理来传输消息。默认值是使用 **sendmail**。 |
| **organization** | 将此参数设置为您的组织名称，方式为您希望它在从您的系统发布的所有新闻文章的 *Organization:* 标头中显示的样子。用户可以通过定义 **ORGANIZATION** 环境变量来覆盖此参数。 |
| **ovmethod** | 设置概述存储方法的类型。（*overview* 是新闻组中新闻文章的索引。）默认方法是 **tradindexed**，读取新闻速度快，但存储新闻项目速度慢。 |
| pathhost | 将此参数设置为您的新闻服务器名称，方式为您希望它在通过您服务器的所有发布的 Path 标头中显示的样子。如果未定义 pathhost，则使用您系统的全限定域名。 |
| pathnews | 将此参数设置为包含 INN 二进制文件和库的目录的完整路径名。默认的 pathnews 设置为 `/usr/lib/news`。 |
| domain | 将此参数设置为您服务器的域名。 |
| allownews | 如果您希望 INN 支持来自新阅读器的 NEWNEWS 命令，请将此参数设置为 true。过去，此选项设置为 false，因为 NEWNEWS 命令会降低服务器的性能，但现在默认设置为 true，因为现代服务器可以轻松处理 NEWNEWS 命令。 |
| hiscachesize | 将此参数设置为您希望 INN 用于缓存最近接收的消息 ID 的大小（以千字节为单位），这些消息 ID 保存在内存中以加快历史查找速度。此缓存仅用于传入源，并且小缓存可以保存相当多的历史文件条目。默认设置 0 禁用历史缓存。如果您有多个传入源，您可能希望将此参数设置为 256（即 256KB）的值。 |
| innflags | 将此参数设置为您希望在 INN 服务器进程启动时传递给它的任何标志。 |

####### newsfeeds 文件

newsfeeds 文件指定传入的新闻文章如何重新分发到其他服务器和 INN 进程。如果您向其他服务器提供新闻源，您必须在此文件中列出这些新闻源。（您还必须有一个标记为 *ME* 的条目，它用于我稍后在本节中解释的特殊目的。）

newsfeeds 文件包含一系列条目，每个源对应一个。每个源条目具有以下格式：

```
site{/exclude,exclude...}\
:pattern, pattern...{/distrib, distrib...}\
:flag, flag...\
:param
```





###### 配置并启动 INN 服务器

每个条目由冒号 (:) 分隔的四个字段组成。通常，条目跨越多行，并在行末使用反斜杠 (\) 将行延续到下一行。这四个字段的含义如下：

- ◆ 第一个字段，site，是源（feed）的名称。每个名称必须是唯一的，对于指向其他新闻服务器的源，该名称设置为远程服务器的主机名。名称后面跟随一个可选的斜杠 (/) 和一个排除列表（*exclude_*、*exclude_*…）的名称。如果该列表中的任何名称出现在文章的路径行中，则该文章不会被转发到该源。如果您不想从特定来源接收文章，可以使用排除列表。

- ◆ 第二个字段是用逗号分隔的新闻组模式列表，例如 `*@alt.barnries.warez.*,!control*,!local*`，后面跟随一个可选的发行列表（distribution list）。发行列表是一个由逗号分隔的关键字列表，每个关键字指定文章分发到的特定站点集合。新闻组模式实际上定义了接收此新闻源的站点订阅列表。星号 (*) 匹配所有新闻组。以 ! 开头的模式会导致匹配该模式的新闻组被丢弃。以感叹号 (!) 开头的模式意味着匹配的新闻组不会被发送。顺便一提，INN 配置文件中使用的简单模式匹配语法被称为 wildmat 模式。

- ◆ 第三个字段是用逗号分隔的标志列表——这些字段确定源条目类型并为条目设置某些参数。您会看到许多标志；输入 `man newsfeeds` 并阅读 man 页面以获取有关标志的更多信息。

- ◆ 第四个字段用于值取决于第三个字段设置的参数。通常，此字段包含 INN 服务器使用的文件或外部程序的名称。您可以从 newsfeeds 的 man 页面中找到有关此字段的更多信息。

既然您知道了 `/etc/news/newsfeeds` 文件的布局，就可以将其作为一个示例来研究了。默认文件包含许多示例源条目，但只有两个被注释掉了：

- ◆ `ME` 是一个特殊的源条目，始终需要存在。它有两个用途。首先，在此条目中列出的新闻组模式用作所有其他条目中所有新闻组模式的前缀。其次，`ME` 条目的发行列表决定了您的服务器接受来自远程站点的哪些发行。

- ◆ `controlchan` 源条目用于配置 INN，以便使用外部程序处理控制消息。（这些消息用于创建新新闻组和移除组。）例如，

![](img/11709a8f88c8cd03868a929dc94c0e2b_658_0.png)

以下 `controlchan` 条目指定外部程序 `/usr/lib/news/bin/controlchan` 来处理所有控制消息，除了 `cancel` 消息（用于取消文章）：

```
controlchan	:!* ,control,control.*,!control, cancel	:Tc,Wnsm: /usr/lib/news/bin/controlchan
```

除了这些源条室外，您还需要为您的新闻服务器提供新闻源的任何实际站点添加条目。此类条目的格式如下：

```
feedme.domain.com	:!junk,!control,!foo	:Tm: innfeed!
```

其中 *feedme.domain.com* 是您的系统发送新闻文章的站点的完全限定域名。

####### incoming.conf 文件

*incoming.conf* 文件描述了哪些主机被允许连接到您的主机以发送文章。对于单个源，您可以添加像这样的条目：

```
peer mybuddy {
	hostname: a-feed-site.domain.com
}
```

其中 *mybuddy* 是对等方的标签，而 *a-feed-site.domain.com* 标识了为您站点提供源的站点。

![](img/11709a8f88c8cd03868a929dc94c0e2b_659_0.png)

请记住，仅仅在 *incoming.conf* 文件中添加站点名称并不会导致远程站点开始向您的站点发送新闻——它只是使您的服务器能够接受来自远程站点的新闻文章。在远程站点，您的伙伴必须配置其服务器以将文章发送到您的站点。

####### readers.conf 文件

此文件指定新闻阅读器客户端（如 Mozilla）可以从您的服务器检索新闻组的主机名或 IP 地址。例如，以下 *readers.conf* 文件允许 *localhost* 和 192.168.0.0 网络中任何主机的 *读访问* 和 *发帖访问*（意味着您可以提交文章）：

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

####### InterNetNews 启动

除了配置文件，您还必须启动执行新闻服务器定期维护的 cron 任务。在 Fedora Core 中，这些 cron 任务已经设置好。因此，您现在准备启动 INN 服务器——innd。

在启动 innd 之前，必须运行 makehistory 和 makedbz 来初始化并重建 INN 历史数据库。输入 man makehistory 和 man makedbz 以了解有关这些命令的更多信息。要创建初始历史数据库、关联索引并设置某些文件的所有权和权限，输入以下命令：

```
/usr/lib/news/bin/makehistory -b -f history -O -l 30000 -I cd /var/lib/news
/usr/lib/news/bin/makedbz -s `wc -l < history` -f history chown news.news *
chown news.news /var/spool/news/overview/group.index
chmod 664 /var/spool/news/overview/group.index
```

在 Fedora Core 中，要启动 innd，请以 root 身份登录并输入 /etc/init.d/innd start。（或者，您可以输入 service innd start。）在 Debian、MEPIS、SUSE、Ubuntu 和 Xandros 中，输入 /etc/init.d/inn start。为确保 innd 在启动时运行，在 Fedora Core 中输入 chkconfig --level 35 innd on，在 SUSE 中输入 chkconfig --level 35 inn on。在 Debian 和 Xandros 中，输入 update-rc.d inn defaults。

如果您对 INN 配置文件进行了任何更改，请记住通过调用 /etc/init.d 脚本并将 restart 作为参数来重新启动服务器。

![](img/11709a8f88c8cd03868a929dc94c0e2b_660_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_660_1.png)

####### 设置本地新闻组

如果您想使用新闻组作为在公司内共享信息的方式，您可以设置一个本地新闻组层次结构。然后，您可以使用这些新闻组在公司内创建虚拟社区，具有共同兴趣的人可以非正式地讨论问题并交换知识。

####### 定义新闻组层次结构

第一项任务是定义新闻组层次结构，决定每个新闻组讨论什么。例如，如果您的公司名称是 XYZ Corporation，以下是您可能定义的局部新闻组层次结构：

- ◇ `xyz.general`：关于 XYZ Corporation 的一般事务
- ◇ `xyz.weekly.news`：每周新闻
- ◇ `xyz.weekly.menu`：每周食堂菜单及相关的讨论
- ◇ `xyz.forsale`：员工出售物品的列表
- ◇ `xyz.jobs`：XYZ Corporation 的职位空缺
- ◇ `xyz.wanted`：员工发布的招聘需求（帮助、要购买的物品等）
- ◇ `xyz.technical.hardware`：关于硬件的技术讨论
- ◇ `xyz.technical.software`：关于软件的技术讨论

####### 更新配置文件

以下是更新本地新闻组的配置文件并重新启动新闻服务器的步骤：

1. **为每个这些新闻组在 `/var/lib/news/newsgroups` 文件中添加描述性条目。**
   为此文件中的每个本地新闻组添加一行——输入其名称，后跟简要描述。例如，以下是您为 `xyz.general` 新闻组可能添加的内容：
   ```
   xyz.general		关于 XYZ Corporation 的一般事务
   ```

2. **编辑 `/etc/news/newsfeeds` 文件中的 ME 条目，并在逗号分隔的新闻组模式列表中添加短语 `*\*xyz.*`。**
   此步骤确保您的本地新闻组不会分发到您的站点外部。





3. 添加用于本地新闻组的存储方法。

例如，你可以在 `/etc/news/storage.conf` 中添加以下行，以定义新的 xyz 层次结构新闻组的存储方法（将 xyz 更改为你为本地新闻组起的名称）：

```
method tradspool {
    class: 1
    newsgroups: xyz.*
}
```

4. 为了使这些更改生效，请重新启动新闻服务器（在 Fedora Core 中输入 **service innnd restart**，或在 Debian、MEPIS、SUSE、Ubuntu 和 Xandros 中输入 **/etc/init.d/inn restart**）。

####### 添加新闻组

最后一步是添加新闻组。在更新配置文件并运行 innnd 之后，添加本地新闻组就变得很容易。登录为 **root** 用户，并使用 `ctlinnnd` 来执行此任务。例如，以下是如何添加一个名为 xyz.general 的新闻组：

```
/usr/lib/news/bin/ctlinnnd newgroup xyz.general
```

就这样！该命令将 xyz.general 新闻组添加到你的站点。如果使用传统存储方法，inn 服务器将创建目录 `/var/spool/news/articles/xyz/general`，并将该新闻组的文章存储在该目录中。（这会在第一次有人向该新闻组发布新闻文章时发生。）

创建完所有本地新闻组后，来自你内部网的用户可以发布新闻文章并阅读本地新闻组中的文章。如果他们遇到访问新闻组的问题，请确保 `/etc/news/readers.conf` 文件包含有权限访问 innnd 服务器的主机的 IP 地址或名称。

####### 测试你的新闻组

例如，我按照前面章节中说明的指令，在运行于我的 Linux 系统上的 INN 服务器中添加了一个名为 local.news 的新闻组。然后我启动一个新闻阅读器，设置一个新的新闻账户，并将新闻服务器设置为我所在的 INN 服务器。然后，我访问 local.news 新闻组。试试吧！我敢打赌你会喜欢它的。

##### 第 5 章：管理 DNS

###### 本章内容

- 理解 DNS
- 探索 BIND
- 配置 DNS
- 设置缓存名称服务器
- 配置主要名称服务器

*域名系统*（DNS）是一种将完全限定域名（如 `www.debian.org`）转换为其相应 IP 地址（如 `194.109.137.218`）的 Internet 服务。你可以将 DNS 视为 Internet 主机的目录——尽管 TCP/IP 在数据传输中需要数字 IP 地址，但 DNS 让你可以使用易于记忆的主机名。DNS 基本上是一个分层的分布式 DNS 服务器体系结构。在本章中，我将提供 DNS 的概述，并展示如何在你的 Linux 系统上设置一个缓存 DNS 服务器。

###### 理解域名系统（DNS）

在 TCP/IP 网络中，每个网络接口（例如，以太网卡或拨号调制解调器连接）都由一个 IP 地址标识。由于 IP 地址难以记忆，因此为 IP 地址分配了一个易于记忆的名称——这就像电话号码对应姓名一样。例如，你不必记住 Red Hat Web 服务器的 IP 地址是 `194.109.137.218`，只需通过其名称 `www.debian.org` 来引用该主机即可。当你在 Web 浏览器中输入 `www.debian.org` 作为 URL 时，名称 `www.debian.org` 会被翻译成其相应的 IP 地址。这就是 DNS 概念发挥作用的地方。

####### 什么是 DNS？

域名系统是一个分布式的、层次化的数据库，保存了 Internet 上计算机的信息。这些信息包括主机名、IP 地址和邮件路由规范。由于这些信息驻留在 Internet 上的许多 DNS 主机上，因此 DNS 被称为*分布式*数据库。DNS 的主要任务是将主机名与 IP 地址相互关联。

在 ARPANET——当今 Internet 的前身——中，主机名和相应 IP 地址的列表维护在一个名为 HOSTS.TXT 的文本文件中，该文件由中心管理并定期分发到网络上的每个主机。随着主机数量的增长，这种静态主机表很快变得不合理，难以维护。Paul Mockapetris 提出了 DNS 以缓解静态主机表的问题。正如在请求评议（RFC）882 和 883（1983 年 11 月发布，参见 www.faqs.org/rfcs/rfc882.html 和 www.faqs.org/rfcs/rfc883.html）中正式记录的那样，原始 DNS 引入了两个关键概念：

- 使用层次化域名，如 www.ee.umd.edu 和 www.debian.org
- 在 Internet 上使用 DNS 服务器——一种分布式责任的体现——作为管理主机数据库的手段

如今，DNS 是记录在 RFC 1034 和 1035 中的 Internet 标准。该标准已由其他几个 RFC 更新和扩展——1101、1183、1348、1886、1995、1996、2136、2181、2308、2845、2930、2931、3007、3110、3226、3403、3596、3597、3645、3646、4025、4033、4034 和 4035。早期的更新定义了数据编码，而后期更新则侧重于改进 DNS 安全性。要在线阅读这些及其他 RFC，请访问 Internet 工程任务组（IETF）网站上的 RFC 页面：

www.ietf.org/rfc.html

DNS 定义了以下内容：

- 用于主机的层次化域名系统
- 将每个域名与 IP 地址相关联的分布式数据库
- 网络应用程序可用于查询分布式 DNS 数据库的库例程（解析器）（该库称为解析器库）
- DNS 客户端和服务器交换名称和 IP 地址信息的协议

如今，Internet 上的所有主机都依赖 DNS 来访问远程主机上的各种 Internet 服务。正如你可能从个人经验中知道的那样，当你从 Internet 服务提供商（ISP）获得 Internet 接入时，ISP 会提供名称服务器——即你的系统在将主机名映射到 IP 地址时访问的 DNS 服务器的 IP 地址。

如果你有一个小型局域网，你可能会决定在某台主机上运行 DNS 服务器，或使用 ISP 提供的名称服务器。对于具有几个子网的中型网络，你可以在每个子网上运行一个 DNS 服务器，以提供高效的 DNS 查找。在大型企业网络中，企业域名（如 www.microsoft.com）进一步划分为子域名层次结构；每个子域名中可以使用几个 DNS 服务器。

在接下来的章节中，我将提供层次化域名命名惯例的概述，并描述 BIND——大多数 UNIX 系统（包括 Linux）上使用的 DNS 软件。

####### 发现层次化域名

DNS 使用域的层次化树来组织命名空间——即整个名称集。每个较高层级的域对其较低层级的子域具有管理权限。每个域代表命名空间中一个独立的块，由单个管理权威管理。图 5-1 说明了 DNS 命名空间的层次化组织。

![](img/11709a8f88c8cd03868a929dc94c0e2b_666_0.png)

树的根称为根域，由单个点（.）表示。接下来是顶级或根级域。顶级域进一步划分为二级域，进而可以划分为更深层级的子域。

顶级域相对固定，包括诸如 COM、NET、ORG、EDU、GOV 和 MIL 等众所周知的域。这些是美国常用的顶级域。这些顶级域的出现是因为 Internet 在 20 世纪 90 年代初得到广泛使用。

另一组顶级域名是为国家保留的。这些域名使用国际标准化组织（缩写为 ISO，参见 www.iso.ch）分配的双字母国家代码。例如，美国的顶级国家代码域是 US。在美国，许多地方政府和组织使用 US 域。例如，mcps.k12.md.us 是美国马里兰州蒙哥马利县公立学校的域名。




## 642 理解域名系统 (DNS)

完全限定域名 (FQDN) 是通过使用点 (.) 作为分隔符，将子域名从低级到高级串联起来构建的。例如，`REDHAT.COM` 是一个完全限定域名；`EE.UMD.EDU` 也是。请注意，这些名称中的每一个也可能指代一台特定的主机计算机。图 5-2 展示了完全限定域名的组成部分。

![](img/11709a8f88c8cd03868a929dc94c0e2b_667_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_667_1.png)

域名是不区分大小写的。因此，就 DNS 而言，域名 `UMD.EDU` 和 `umd.edu` 都代表马里兰大学（University of Maryland）的域名。然而，惯例是全部使用小写字母输入域名。

###### 探索 Berkeley Internet Name Domain (BIND)

大多数 UNIX 系统，包括 Linux，都附带了 BIND 系统——这是 DNS 的一个著名实现。只要你选择在安装包时选择名称服务器，BIND 软件就会在 Linux 安装过程中被安装。

在 Debian、MEPIS、Ubuntu 和 Xandros 中，输入 `dpkg -i bind*` 以查看是否安装了 BIND。在 Fedora Core 和 SUSE 中，输入 `rpm -q bind` 以查看是否安装了 bind 软件包。

在 Debian、MEPIS 和 Ubuntu 中，输入 `apt-get install bind9` 以安装 BIND。在 Fedora Core 中，以 `root` 身份登录，挂载 DVD，然后输入 `cd /media/cdrom/Fedora/RPMS`，接着输入 `rpm -ivh bind*`。在 SUSE 中，在 YaST 控制中心的软件类别中点击软件管理。然后使用 YaST 的搜索功能查找 bind，选择相关的软件包并安装它们。在 Xandros 中，首先运行 Xandros Networks，选择编辑:* 设置应用程序源，并将 Debian Unsupported Site 链接作为源点击。然后输入 `apt-get install bind9` 以安装 BIND 服务器。

BIND 包含三个主要组件：

![](img/11709a8f88c8cd03868a929dc94c0e2b_667_2.png)

- named 守护进程——即名称服务器——用于响应关于主机名和 IP 地址的查询
- 一个解析器库，应用程序可以使用它将主机名解析为 IP 地址（反之亦然）
- 命令行 DNS 实用程序（DNS 客户端），例如 dig（Domain Internet Groper）和 host，用户可以用来查询 DNS

我将在接下来的几节中描述这些 BIND 组件。在后续章节中，我将解释如何配置解析器和名称服务器。

####### named — BIND 名称服务器

named 守护进程是响应关于主机名和 IP 地址查询的名称服务器。基于配置文件和本地 DNS 数据库，named 要么提供查询的答案，要么向其他服务器询问并缓存它们的响应。named 服务器还执行一种称为区域传输的功能，这涉及到在域名内的名称服务器之间复制数据。

名称服务器以三种模式之一运行：

- 主或 Master：在这种情况下，名称服务器在磁盘上保存域名数据的主副本。每个域名或子域名有一个主服务器。
- 从或 Slave：辅助名称服务器使用区域传输操作从主服务器复制其域名的数据。一个域名可以有一个或多个辅助名称服务器。
- 缓存：缓存名称服务器加载根域名的少数权威服务器的地址，并通过缓存由联系其他名称服务器已解决的查询响应来获取所有域名数据。主服务器和辅助服务器也缓存响应。

名称服务器可以是权威的，也可以不是，这取决于它提供的信息。顾名思义，权威名称服务器的响应应该是准确的。主名称服务器和辅助名称服务器对其自身的域名是权威的，但对于从缓存信息提供的响应则不是权威的。

![](img/11709a8f88c8cd03868a929dc94c0e2b_668_0.png)

> 缓存名称服务器永远不是权威的，因为它们的所有响应都来自缓存信息。

要在你的 Linux 系统上运行名称服务器，你必须有适当的配置文件运行 named。在本章稍后部分，你会了解到控制名称服务器操作的配置文件和数据文件。

####### 解析器库

查找主机名的 IP 地址被称为*解析主机名*。具有网络感知功能的应用程序，如 Web 浏览器或 FTP 客户端，使用*解析器库*来执行从名称到 IP 地址的转换。根据 `/etc/host.conf` 文件中的设置，解析器库会查阅 `/etc/hosts` 文件或发起 DNS 查询，以将主机名解析为其 IP 地址。解析器库查询 `/etc/resolv.conf` 文件中列出的名称服务器。

除非你正在编写具有网络感知功能的应用程序，否则不需要了解太多关于解析器库的内容。要正确运行互联网服务，你所需要知道的只是如何配置解析器。在本章稍后部分，我将向你展示如何配置服务器和 DNS 的其它方面。

####### DNS 实用程序

你可以使用 DNS 实用程序——`dig` 和 `host`——在 shell 提示符下交互式地测试 DNS。这些实用程序是 DNS 客户端。你可以使用它们查询 DNS 数据库并调试系统中设置的任何名称服务器。默认情况下，这些程序查询系统中 `/etc/resolv.conf` 文件里列出的名称服务器。

你可以使用 `dig`（Domain Internet Groper 程序）来查找域名 IP 地址或反之亦然。例如，要查找 `ftp.redhat.com` 的 IP 地址，输入

```
dig ftp.redhat.com
```

`dig` 会非常详细地打印 DNS 查询结果。请在输出中标记为*ANSWER SECTION*的部分查找结果。例如，此示例查询中该部分看起来像这样：

```
;; ANSWER SECTION:
ftp.redhat.com.           300     IN      A       66.187.224.30
```

此输出意味着名称 `ftp.redhat.com` 指向 IP 地址 66.187.224.30。

使用 `dig` 进行*反向查找*（为 IP 地址查找主机名）也很简单。例如，要找到 IP 地址 209.132.176.30 对应的主机名，输入以下内容：

```
dig -x 66.187.224.30
```

同样，答案出现在输出的 ANSWER SECTION 中，对于此示例，它看起来像这样：

```
;; ANSWER SECTION:
30.224.187.66.in-addr.arpa. 600 IN PTR ftp.redhat.com.
```

在这种情况下，对应于 IP 地址 66.187.224.30 的主机名恰好是 ftp.redhat.com。

你还可以使用 host 程序查询 DNS。host 程序以紧凑格式输出结果。例如，这里展示了一个使用 host 查找主机名 IP 地址的典型用法：

```
host www.gao.gov
```

此命令产生以下输出：

```
www.gao.gov has address 161.203.16.2
www.gao.gov mail is handled by 5 listserv.gao.gov.
```

默认情况下，host 打印 IP 地址和任何 MX 记录。（这些记录列出了该主机的邮件处理器名称。）

对于反向查找，请使用 -t ptr 选项，并将 IP 地址作为参数，如下所示：

```
host -t ptr 161.203.16.2
```

以下是来自 host 的响应：

```
2.16.203.161.in-addr.arpa domain name pointer www.gao.gov.
```

在这种情况下，host 打印出显示与 IP 地址对应的主机名的 PTR 记录（来自 DNS 数据库）。（PTR 代表指针，PTR 记录指定与地址对应的名称。）

你还可以尝试其他类型的记录，例如 CNAME（规范名称），如下所示：

```
host -t cname www.ee.umd.edu
```

来自 host 的响应说

```
www.ee.umd.edu is an alias for edison.eng.umd.edu.
```

此输出表明 www.ee.umd.edu 的规范名称（或别名）是 edison.eng.umd.edu。

###### 配置 DNS

你通过使用多个配置文件来配置 DNS。具体的文件集取决于你是否在运行名称服务器，如果是，则是哪种类型的名称服务器——缓存型或主型。无论你是否运行名称服务器，都需要一些配置文件。

####### 配置解析器

使用 DNS 客户端（*dig* 和 *host*）不需要在你的系统上运行名称服务器。你可以使用它们查询你域名的名称服务器。通常，你的 ISP 会提供此信息。你必须在 */etc/resolv.conf* 文件中列出这些名称服务器的 IP 地址——解析器库读取此文件以确定如何解析主机名。此文件的格式为

```
domain  your-domain.com
search    your-domain.com
nameserver A.B.C.D
nameserver X.Y.Z.W
```

其中 A.B.C.D 和 X.Y.Z.W 是你的 ISP 提供的主名称服务器和辅助名称服务器的 IP 地址（点分隔的数字地址，例如 192.168.0.1）。

*domain* 行列出本地域名。*search* 行指定首先搜索主机名的域名（通常，你将自己的域名放在 search 行中）。*search* 行列出的域名会在解析器库尝试解析任何主机名之前追加到该主机名后面。例如，如果你查找名为 mailhost 的主机，解析器库首先尝试 mailhost.your-domain.com；如果失败，则尝试 mailhost。*search* 行适用于你尝试访问的任何主机名。例如，如果你正在尝试访问 www.redhat.com，解析器首先尝试 www.redhat.com.your-domain.com，然后尝试 www.redhat.com。

另一个重要的配置文件是 */etc/host.conf*——此文件告诉解析器在尝试解析主机名时该做什么。典型的 */etc/host.conf* 文件包含以下行：

```
order  hosts,bind
```

此命令告诉解析器首先查阅 */etc/hosts* 文件，如果失败，则查询 */etc/resolv.conf* 文件中列出的名称服务器。*/etc/hosts* 文件通常列出任何本地主机名及其 IP 地址。以下是 */etc/hosts* 文件中典型的一行：

```
127.0.0.1  lnpb200  localhost.localhost
```




###### 配置 DNS

####### 配置缓存名称服务器

此行表示 IP 地址 127.0.0.1 被分配给了主机名 `lnbp200`、`localhost.localdomain` 和 `localhost`。

在最新的 Linux 内核版本——即使用 GNU C 库版本 2（glibc 2）或更高版本的内核——中，名称服务切换（NSS）文件 `/etc/nsswitch.conf` 控制了解析器库、NIS、NIS+ 以及 `/etc/hosts` 和 `/etc/shadow` 等本地文件等服务的交互方式。例如，`/etc/nsswitch.conf` 文件中的以下 `hosts` 条目指定了解析器库先尝试 `/etc/hosts` 文件，然后尝试 NIS+，最后尝试 DNS：

```
hosts:          files nisplus dns
```

若要了解关于 `/etc/nsswitch.conf` 文件及其功能的更多信息，请在终端窗口中输入 `man nsswitch.conf`。

一个简单但实用的名称服务器，它会通过（使用其他名称服务器）查找主机名查询的答案，然后记住该答案（将其保存在缓存中）以便下次需要时使用。这种缓存名称服务器可以缩短访问最近访问过的主机所需的时间；因为答案已经在缓存中了。

当你安装 BIND 时，缓存名称服务器的配置文件也会随之安装。这意味着你无需太多操作即可开始运行缓存名称服务器。本节介绍配置文件以及启动缓存名称服务器需要执行的操作。

######## /etc/named.conf 文件

你需要第一个配置文件是 `/etc/named.conf`。（实际上，这是 Fedora Core 和 SUSE 中的文件名；在 Debian、MEPIS、Ubuntu 和 Xandros 中，BIND 配置文件被称为 `/etc/bind/named.conf`。）named 服务器在启动时读取此配置文件。如果你安装了 BIND，你应该已经有这个文件。以下是一个来自 Fedora Core 的 `/etc/named.conf` 文件：

```
options {
    directory "/var/named";
    dump-file "/var/named/data/cache_dump.db";
    statistics-file "/var/named/data/named_stats.txt";
    /*
     * If there is a firewall between you and nameservers you want
     * to talk to, you might need to uncomment the query-source
     * directive below.  Previous versions of BIND always asked
     * questions using port 53, but BIND 8.1 uses an unprivileged
     * port by default.
     */
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

zone "localdomain" IN {
    type master;
    file "localdomain.zone";
    allow-update { none; };
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

zone "0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.ip6.arpa" IN {
    type master;
    file "named.ip6.local";
    allow-update { none; };
};

zone "255.in-addr.arpa" IN {
    type master;
    file "named.broadcast";
    allow-update { none; };
};

zone "0.in-addr.arpa" IN {
    type master;
    file "named.zero";
    allow-update { none; };
};

include "/etc/rndc.key";
```

注释可以是 C 风格（`/* . . . */`）或 C++ 风格（以 `//` 开头）。该文件包含由花括号（`{ . . . }`）包围并以分号（`;`）终止的块语句。块语句反过来又包含其他语句，每个语句都以分号结尾。

此 `/etc/named.conf` 文件以一个 options 块语句开头，其中包含多个 option 语句。directory option 语句告诉 named 在配置文件的 file 行中查找所有其他文件的位置。在这种情况下，named 会在 /var/named 目录中查找文件。

![](img/11709a8f88c8cd03868a929dc94c0e2b_674_0.png)

在 SUSE 中，/etc/named.conf 中的 directory option 指向 /var/lib/named 目录，这意味着所有其他 BIND 配置文件都在 /var/lib/named 中。在 Debian 和 Xandros 中，配置文件被明确指定位于 /etc/bind 目录中。

![](img/11709a8f88c8cd03868a929dc94c0e2b_674_1.png)

/etc/named.conf 中的 controls 语句包含安全信息，以便 rndc 命令可以连接到 named 服务的 953 端口并与 named 交互。在这种情况下，controls 语句包含以下行：

```
inet 127.0.0.1 allow { localhost; } keys { rndckey; };
```

此命令表示 rndc 可以使用名为 rndc 的密钥从 localhost 连接。（/etc/rndc.key 文件定义了密钥和使用的加密算法。）

![](img/11709a8f88c8cd03868a929dc94c0e2b_674_2.png)

rndc（远程名称守护进程控制）实用程序是较旧的 ndc（用于名称守护进程控制器）实用程序的后继者，后者用于通过向 named 服务器发送消息来控制它，该消息通过一个特殊控制通道发送，即 named 监听消息的 TCP 端口。rndc 实用程序使用加密密钥向 named 服务器进行身份验证。named 服务器拥有相同的加密密钥，因此可以解码 rndc 发送的身份验证信息。

在 options 语句之后，/etc/named.conf 文件包含多个 zone 语句，每个语句都包含在花括号中并以分号结尾。每个 zone 语句定义一个区域。第一个区域名为 .（根区域）；它是一个提示区域（hint zone），指定了根名称服务器。（当 DNS 服务器启动时，它使用提示区域找到一个根名称服务器，并获取最新的根名称服务器列表。）

/etc/named.conf 中的接下来两个 zone 语句是主区域（master zones）。（主区域仅仅是某个域的数据的主副本。）互联网类区域（由 IN 关键字指示）的主区域语句的语法如下：

```
zone "zone-name" IN {
type master;
file "zone-file";
[...其他可选语句...]
};
```

*zone-name* 是区域的名称，*zone-file* 是包含该区域的资源记录（RR）——即数据库条目——的区域文件。我将在接下来的两节中介绍区域文件格式和资源记录格式。

######## 区域文件格式

区域文件通常以多个指令开头，每个指令都以美元符号（$）开头，后跟一个关键字。两个常用指令是 $TTL 和 $ORIGIN。

例如，这一行

```
$TTL		86400
```

使用 $TTL 指令为后续未定义 TTL 的记录设置默认的生存时间（Time To Live，TTL）。值以秒为单位，有效的 TTL 范围是 0 到 2147483647 秒。在这种情况下，该指令将默认 TTL 设置为 86400 秒（或一天）。

$ORIGIN 指令设置要附加到任何未限定记录上的域名。例如，以下 $ORIGIN 指令将域名设置为 localhost：

```
$ORIGIN localhost.
```

如果没有 $ORIGIN 指令，初始 $ORIGIN 将与 */etc/named.conf* 文件中 zone 关键字后的区域名称相同。

在指令之后，区域文件包含一个或多个资源记录。这些记录遵循特定的格式，我将在下一节中概述。

######## 资源记录（RR）格式

在理解区域文件并智能地操作之前，你必须理解资源记录的格式。每个资源记录具有以下格式。（可选字段用方括号表示。）

```
[domain]  [ttl]  [class] type data [;comment]
```

字段之间用制表符或空格分隔，并且可能包含一些特殊字符，例如用于域名的 @ 符号和用于指示注释开始的分号（;）。

第一个字段必须从行的第一个字符开始，它标识域名。你可以使用 @ 符号为当前记录使用当前的 $ORIGIN 作为域名。如果你为同一个域名有多个记录，请将第一个字段留空。

可选的 ttl 字段指定生存时间——数据可以缓存并被视为有效的时间段。你可以使用以下格式之一指定时间段：

- **N**，其中 *N* 是一个数字，表示 *N* 秒
- **Mw**，其中 *M* 是一个数字，表示 *M* 周
- **Md**，其中 *M* 是一个数字，表示 *M* 天
- **Mh**，其中 *M* 是一个数字，表示 *M* 小时
- **Mm**，其中 *M* 是一个数字，表示 *M* 分钟
- **Ms**，其中 *M* 是一个数字，表示 *M* 秒

字母 **w**、**d**、**h** 和 **s** 也可以是小写的。因此，你可以写 `86400` 或 `1d`（或 `1D`）来表示一天的时间段。你也可以组合这些来指定更精确的时间段，例如 `5w6d1h` 表示 5 周、6 天和 1 小时。

**class** 字段指定网络类型。此字段最常用的值是表示 Internet 的 **IN**。

资源记录中的下一个字段是 *type* 字段，它表示记录的类型（例如 **SOA**、**NS**、**A** 或 **PTR**）。表 5-1 列出了 DNS 资源记录类型。数据字段接下来出现，具体取决于类型字段。

| 类型 | 名称 | 描述 |
| :--- | :--- | :--- |
| **A** | 地址 | 指定与主机名对应的 IPv4 地址 |
| **AAAA** | IPv6 地址 | 指定与名称对应的 IPv6 主机地址 |
| **AS** | (非标准/常见) | *注意：原文列出的 "AS" 为 "Address"，但上下文暗示 "A"。然而，仔细查看标准 DNS 表格，"A" 是 Address。"AAAA" 是 IPv6。"NS" 是 Name Server。让我们仔细重新检查 OCR 文本。* |
| **CERT** | 数字证书 | 保存数字证书 |
| **CNAME** | 规范名称 | 定义主机名的昵称或别名 |
| **DNAME** | 委派名称 | 用另一个名称替换指定的域名以进行查找 |
| **HINFO** | 主机信息 | 标识主机的硬件和操作系统 |
| **KEY** | 公钥 | 保存与 DNS 名称关联的公钥 |

*（待续）*



######## 表 5-1（续）

| 类型 | 名称 | 描述 |
| :--- | :--- | :--- |
| MX | 邮件交换器 | 标识接受发往特定域名的邮件的主机（用于路由电子邮件） |
| NS | 名称服务器 | 标识某个区域（zone）的权威名称服务器 |
| PTR | 指针 | 指定与地址对应的名称（用于*反向映射*——将 IP 地址转换为主机名） |
| RP | 负责人 | 提供域名技术联系人的姓名 |
| SIG | 签名 | 包含在安全 DNS 中经过认证的数据（详情参见 RFC 2535） |
| SOA | 授权起始 | 指示后续的所有记录对此区域均为权威记录 |
| SRV | 服务 | 列出域名提供的知名网络服务 |
| TXT | 文本 | 用于在 DNS 数据库中包含注释和其他信息 |

阅读区域文件中的资源记录，至少包括类型为 **SOA**、**NS**、**A**、**PTR** 和 **MX** 的记录，这些是最常用的类型之一。（你可以在 Debian 和 Xandros 的 `/etc/bind` 目录、Fedora Core 的 `/var/named` 目录以及 SUSE 的 `/var/lib/named` 目录中找到区域文件。）接下来，我将简要描述这些记录，并通过示例说明每种记录类型。

典型的 **SOA** 记录具有以下格式：

```text
@ IN SOA @ root (
    42 ; serial
    3h ; refresh -- 3 hours
    15m ; retry -- 15 minutes
    1w ; expire -- 1 week
    1d ) ; minimum -- 1 day
```

第一个字段将域名指定为 **@**，这意味着当前域名（默认为区域名称，如本 `/etc/named.conf` 文件所示）。下一个字段指定该记录的 TTL（生存时间）为一 day。类字段设置为 **IN**，表示该记录适用于互联网。类型字段将记录类型指定为 **SOA**。其余字段构成 **SOA** 记录的数据。数据包括主名称服务器的名称（在此情况下为 **@**，即当前域名）、技术联系人的电子邮件地址，以及括号内的五个不同时间值。

**NS** 记录指定某个区域的权威名称服务器。典型的 NS 记录如下所示：

```text
. 3600000 IN NS A.ROOT-SERVERS.NET.
```

在此情况下，**NS** 记录列出了根区域的权威名称服务器。（请注意，第一个字段的名称是一个单点。）**生存时间**字段指定该记录有效期限为 1,000 小时（3600000 秒）。类为 **IN**，代表互联网；记录类型为 **NS**。最后一个字段列出名称服务器的名称（A.ROOT-SERVERS.NET.），其末尾带有一个点。

**A** 记录指定与名称对应的地址。例如，以下 **A** 记录显示 A.ROOT-SERVERS.NET. 的地址为 198.41.0.4：

```text
A.ROOT-SERVERS.NET. 3600000 A 198.41.0.4
```

在此情况下，未指定网络类，因为该字段是可选的，默认为 **IN**。

**PTR** 记录用于反向映射——将地址转换为名称。考虑以下示例：

```text
1 IN PTR localhost.
```

此记录来自名为 0.0.127.in-addr.arpa 的区域的文件。因此，该记录说明与地址 127.0.0.1 关联的名称是 localhost。

**MX** 记录指定代表特定域名接受邮件的主机名称。例如，这里是一个典型的 **MX** 记录：

```text
naba IN MX 10 mailhub.lnbsft.com.
```

该记录说明，发往当前域名下名为 naba 的主机的邮件将被发送到 mailhub.lnbsft.com。（该主机被称为*邮件交换器*。）数字 10 是优先级值。对于具有不同优先级值的多个 **MX** 记录列表，优先级值较低的记录会被优先尝试。

掌握了有关资源记录的这些信息后，你可以查看缓存名称服务器的区域文件。

# 根区域文件

有关十三个根名称服务器的信息位于 `/etc/named.conf` 文件中根区域语句所引用的区域文件中。

（在 Fedora Core 中，根区域文件是 /var/named/named.ca；在 Debian、MEPIS、Ubuntu 和 Xandros 中，它是 /etc/bind/db.root；在 SUSE 中，它是 /var/lib/named/root.hint。）以下列表显示了根区域文件：

```text
;
; This file holds the information on root name servers needed to
; initialize cache of Internet domain name servers
; (e.g. reference this file in the "cache . <files>"
; configuration file of BIND domain name servers).
;
; This file is made available by InterNIC
; under anonymous FTP as
;             file        /domain/named.cache
;                 on server    FTP.INTERNIC.NET
;         -OR-
;                 on server    RS.INTERNIC.NET
;
; last update:   Jan 29, 2004
; related version of root zone:  2004012900
;
;
; formerly NS.INTERNIC.NET
;
.                           3600000 IN  NS  A.ROOT-SERVERS.NET.
A.ROOT-SERVERS.NET.         3600000   A   198.41.0.4
;
; formerly NS1.ISI.EDU
;
.                           3600000   NS  B.ROOT-SERVERS.NET.
B.ROOT-SERVERS.NET.         3600000   A   192.228.79.201
;
; formerly C.PSI.NET
;
.                           3600000   NS  C.ROOT-SERVERS.NET.
C.ROOT-SERVERS.NET.         3600000   A   192.33.4.12
;
; formerly TERP.UMD.EDU
;
.                           3600000   NS  D.ROOT-SERVERS.NET.
D.ROOT-SERVERS.NET.         3600000   A   128.8.10.90
;
; formerly NS.NASA.GOV
;
.                           3600000   NS  E.ROOT-SERVERS.NET.
E.ROOT-SERVERS.NET.         3600000   A   192.203.230.10
;
; formerly NS.ISC.ORG
;
.                           3600000   NS  F.ROOT-SERVERS.NET.
F.ROOT-SERVERS.NET.         3600000   A   192.5.5.241
;
; formerly NS.NIC.DDN.MIL
;
.                           3600000   NS  G.ROOT-SERVERS.NET.
G.ROOT-SERVERS.NET.         3600000   A   192.112.36.4
;
; formerly AOS.ARL.ARMY.MIL
;
.                           3600000   NS  H.ROOT-SERVERS.NET.
H.ROOT-SERVERS.NET.         3600000   A   128.63.2.53
;
; formerly NIC.NORDU.NET.
;
;
.                           3600000   NS      I.ROOT-SERVERS.NET.
I.ROOT-SERVERS.NET.         3600000   A       192.36.148.17
; operated by VeriSign, Inc.
;
;
.                           3600000   NS      J.ROOT-SERVERS.NET.
J.ROOT-SERVERS.NET.         3600000   A       192.58.128.30
; operated by RIPE NCC
;
;
.                           3600000   NS      K.ROOT-SERVERS.NET.
K.ROOT-SERVERS.NET.         3600000   A       193.0.14.129
; operated by ICANN
;
;
.                           3600000   NS      L.ROOT-SERVERS.NET.
L.ROOT-SERVERS.NET.         3600000   A       198.32.64.12
; operated by WIDE
;
;
.                           3600000   NS      M.ROOT-SERVERS.NET.
M.ROOT-SERVERS.NET.         3600000   A       202.12.27.33
; End of File
```

此文件包含 NS 和 A 资源记录，指定了根区域的权威名称服务器名称及其地址（由每个 NS 记录第一个字段中的 . 表示）。

文件中的注释行以分号开始。这些注释提供了有关根名称服务器位置的线索。互联网有 13 个根名称服务器；大多数根服务器位于美国。此文件对任何名称服务器都是必需的，因为名称服务器必须能够到达至少一个根名称服务器。

# localhost.zone 文件

/etc/named.conf 文件包含一个用于 localhost 区域的区域语句，该语句指定区域文件为 localhost.zone。该文件位于 Fedora Core 的 /var/named 目录、SUSE 的 /var/local/named 目录，以及 Debian 和 Xandros 的 /etc/bind/db.local。以下是 localhost.zone 文件内容的列表：

```text
TTL 86400
$ORIGIN localhost.
@ ID IN SOA @ root (
    42 ; serial (d. adams)
    3H ; refresh
    15M ; retry
    1W ; expiry
    1D ) ; minimum
    ID IN NS @
    ID IN A 127.0.0.1
```

此区域文件以一个 `$TTL` 指令开始，该指令将后续未定义 TTL 的记录的默认 TTL（生存时间）设置为一天（86400 秒）。接下来，一个 `$ORIGIN` 指令将域名设置为 `localhost`。

在这两条指令之后，`localhost.zone` 文件包含三个资源记录（RR）：一个 `SOA` 记录、一个 `NS` 记录和一个 `A` 记录。`SOA` 和 `NS` 记录将 `localhost` 指定为该区域的主权威名称服务器。`A` 记录将 `localhost` 的地址指定为 `127.0.0.1`。

# 127.0.0.1 反向映射的区域文件

`/etc/named.conf` 文件中的第三个区域语句指定了一个名为 `0.0.127.in-addr.arpa.` 的反向映射区域。对于此区域，在 Fedora Core 中区域文件是 `/var/named/named.localhost`，在 SUSE 中是 `/var/lib/named/127.0.0.zone`，在 Debian、MEPIS、Ubuntu 和 Xandros 中是 `/etc/bind/db.127`。此区域文件包含以下内容：

```text
$TTL        86400
@   IN  SOA     localhost.    root.localhost.   (
                                    1997022700 ; Serial
                                    288000 ; Refresh
                                    14400 ; Retry
                                    3600000 ; Expire
                                    86400 ) ; Minimum
            IN      NS      localhost.
1            IN  PTR     localhost.
```

`SOA` 和 `NS` 记录将 `localhost` 指定为主名称服务器。`PTR` 记录将 `localhost` 指定为地址 `127.0.0.1` 对应的名称。

![](img/11709a8f88c8cd03868a929dc94c0e2b_681_0.png)

`SOA` 记录还显示了 `root.localhost.` 作为该域名技术联系人的电子邮件地址。请注意，DNS 区域文件使用 `user.host.`（注意结尾的点）格式来表示电子邮件地址。在向联系人发送任何电子邮件时，你必须将第一个点替换为 `@`，并去掉最后的点。

# 缓存名称服务器：启动与测试

在研究了缓存名称服务器的配置文件后，你可以启动名称服务器并观察其运行状态。

![](img/11709a8f88c8cd03868a929dc94c0e2b_681_1.png)

要启动名称服务器，请以 `root` 身份登录，并在 Fedora Core 和 SUSE 中键入 `/etc/init.d/named start`。为了确保每次重启系统时 `named` 服务器都能启动，请在 Fedora Core 和 SUSE 中键入 `chkconfig --level 35 named on`。在 Debian、MEPIS、Ubuntu 和 Xandros 中，键入 `/etc/init.d/bind9 start` 来启动 `named` 服务器。





####### 配置缓存名称服务器

named 服务器会在 /var/log/messages 文件中写入诊断日志消息。启动 named 后，你可以打开 /var/log/messages 文本来查看日志消息。如果没有来自 named 的错误消息，你可以继续进行名称服务器的测试。

在尝试使用缓存名称服务器之前，你必须指定该名称服务器作为你的主名称服务器。为此，请确保 /etc/resolv.conf 文件的第一行如下所示：

```
nameserver 127.0.0.1
```

现在，你可以使用 host 命令来测试名称服务器。例如，要通过本地主机（localhost）上的缓存名称服务器查询 www.gao.gov 的 IP 地址，请输入以下命令：

```
host www.gao.gov localhost
```

以下是 host 命令的结果输出：

```
Using domain server:
Name: localhost
Address: 127.0.0.1#53
Aliases:
  www.gao.gov  has address 161.203.16.2
```

输出显示，host 命令使用 localhost 作为 DNS 服务器并返回 www.gao.gov 的 IP 地址。如果你得到类似的输出，说明缓存名称服务器已经启动并正在运行。

####### 配置主名称服务器

配置主名称服务器最好的方法是从配置缓存名称服务器开始（如前几节所述）。然后，添加你希望此名称服务器作为主名称服务器的域的主区域。例如，假设我想为 naba.net 域定义一个主名称服务器。以下是我在 Fedora Core 系统上（登录为 root 后）配置该主名称服务器所经历的步骤：

1. **在 /etc/named.conf 文件中添加以下区域语句：**

   ```text
   zone "naba.net" IN {
     type master;
     file "naba.zone";
   };
   zone "0.168.192.in-addr.arpa" IN {
     type master;
     file "0.168.192.zone";
   };
   ```

2. **创建区域文件** `/var/named/naba.zone`，**包含以下行：**

   ```text
   $TTL	86400
   $ORIGIN naba.net.
   			@		1D	IN	SOA
   						@ root.naba.net (
   						100		; serial
   						3H		; refresh
   						15M		; retry
   						1W		; expiry
   						1D )
   				; minimum
   			
   			1D	IN	NS	@
   			1D	IN	A		192.168.0.7
   wpxp		IN	A	192.168.0.2
   ```

3. **创建区域文件** `/var/named/0.168.192.zone`，**包含以下行：**

   ```text
   $TTL	86400
   ; Remember zone name is: 0.168.192.in-addr.arpa
   @		IN	SOA	wpxp.naba.net.	root.naba.net. (
   			1		; Serial
   			28800	; Refresh
   			14400	; Retry
   			3600000 ; Expire
   			86400 ) ; Minimum
   		
   			IN	NS		wpxp.naba.net.
   7		IN	PTR	wpxp.naba.net.
   2		IN	PTR	wpxp.naba.net.
   ```

4. **要测试新配置，使用以下命令重启** `named` **服务器：**

   ```sh
   /etc/init.d/named restart
   ```

5. **使用** `dig` **或** `host` **查询** DNS **服务器。**

   例如，以下是我如何使用 `host` 在运行于 `localhost` 的 DNS 服务器上检查主机 `wpxp.naba.net` 地址的方法：

   ```sh
   host wpxp.naba.net localhost
   ```

   此命令产生以下输出：

   ```text
   Using domain server:
   Name:	localhost
   Address:	127.0.0.1#53
   Aliases:
   	wpxp.naba.net has address 192.168.0.2
   ```

   如果你想使用 `dig` 检查 DNS 服务器，请输入以下命令：

   ```sh
   dig @localhost wpxp.naba.net
   ```

   `@localhost` 部分指定了 `dig` 要连接的 DNS 服务器。

当你成功使用 `dig` 连接到 DNS 服务器时，你可以向该服务器请求执行一些更高级的操作。例如，以下是我输入的命令，用于尝试针对 IP 地址 192.168.0.2 进行反向查找：

```
host 192.168.0.2 localhost
```

此命令显示以下输出：

```
Using domain server:
Name: localhost
Address: 127.0.0.1#53
Aliases:
2.0.168.192.in-addr.arpa domain name pointer wpxp.naba.net
```

##### 第 6 章：使用 Samba 和 NFS

###### 本章内容

- 使用 NFS 共享文件
- 安装和配置 Samba
- 使用 Samba 设置 Windows 服务器

如果你的局域网像其他大多数网络一样，它需要具备在运行 Linux 的系统与其他未运行 Linux 的系统之间共享文件的能力。因此，Linux 包含两个突出的文件共享服务：

- **网络文件系统（NFS）** 用于与其他 UNIX 系统（或装有 NFS 客户端软件的 PC）共享文件。
- **Samba** 用于与 Windows 系统进行文件共享和打印共享。

在本章中，我将描述如何使用 NFS 和 Samba 共享文件。

###### 使用 NFS 共享文件

通过 NFS 共享文件很简单，涉及两个基本步骤：

- 在运行 NFS 服务器的 Linux 系统上，你通过在 `/etc/exports` 文件中列出并运行 `exports` 命令来导出（共享）一个或多个目录。此外，你必须启动 NFS 服务器。
- 在每个客户端系统上，你使用 `mount` 命令挂载你的服务器已导出的目录。

使用 NFS 的唯一问题是每个客户端系统都必须支持它。Microsoft Windows 并不附带 NFS。这意味着，如果你想使用 NFS 共享文件，你必须单独购买 NFS 软件。然而，如果局域网中的所有系统都运行 Linux（或其他内置 NFS 支持的 UNIX 变种），使用 NFS 是有意义的。

![](img/11709a8f88c8cd03868a929dc94c0e2b_686_0.png)

NFS 存在安全漏洞。因此，你应该避免在未使用 NFS 版本 4（NFSv4）自带的 RPCSEC\_GSS 安全性的情况下，在直接连接到互联网的系统上设置 NFS。

![](img/11709a8f88c8cd03868a929dc94c0e2b_687_0.png)

Linux 2.6 内核内置对 NFSv4 的支持，它是基于早期版本的 NFS 构建的。但与早期版本不同，NFSv4 具有更强的安全性，并旨在互联网环境中运行。（RFC 3510 描述了 NFSv4；参见 `http://www.ietf.org/rfc/rfc3510.txt.`）NFSv4 使用 RPCSEC_GSS（GSS 代表通用安全服务，Generic Security Services）协议进行安全保护。你可以继续使用基于旧的用户 ID 和组 ID 的身份验证来使用 NFSv4，但如果你想使用 RPCSEC_GSS，你必须运行三个附加服务——服务器上的 `rpcsvcgssd`，客户端上的 `rpcgssd`，以及客户端和服务器上的 `rpcidmapd`。有关 Linux 中 NFSv4 实现的更多信息，请访问 `http://www.citi.umich.edu/projects/nfsv4/linux`。

在接下来的几个部分中，我将通过一个局域网中两台 Linux PC 的示例来引导你完成 NFS 设置。

####### 使用 NFS 导出文件系统

从服务器系统开始，该系统通过 `exports`（即将目录内容提供给客户端系统）使目录内容可用。在服务器上，你必须运行 NFS 服务并指定要导出的一个或多个文件系统。

要导出文件系统，你必须将适当的条目添加到 `/etc/exports` 文件中。例如，假设你想导出 `/home` 目录，并希望允许名为 `LNBP75` 的主机以读写操作挂载此文件系统。你可以通过在 `/etc/exports` 文件中添加以下条目来实现：

```
/home  LNBP75 (rw,sync)
```

如果你想让局域网（例如 `192.168.0.0`）上的所有主机都能访问，你可以将此行更改为

```
/home  192.168.0.0/24 (rw,sync)
```

`/etc/exports` 文件中的每一行都具有这种通用格式：

```
directory host1 (options)  host2 (options) ...
```

第一个字段是通过 NFS 共享的目录，后跟一个或多个字段，指定哪些主机可以远程挂载该目录以及括号内的多个选项。你可以使用名称或 IP 地址来指定主机，包括地址范围。

括号内的选项表示授予每个主机的访问类型以及服务器上的用户和组 ID 如何映射到客户端的 ID。（例如，如果一个文件在服务器上由 `root` 拥有，那么在客户端由谁拥有？）在括号内，选项之间用逗号分隔。例如，如果某个主机被允许同时具有读取和写入权限——并且所有 ID 都应映射到 `匿名用户`（默认情况下，这是名为 nobody 的用户）——那么选项看起来像这样：

(`rw,all_squash`)

表 6-1 显示了你可以在 `/etc/exports` 文件中使用的选项。你会发现有两种类型的选项——通用选项和用户 ID 映射选项。

**表 6-1** **`/etc/exports` 中的选项**

| 此选项 | 执行以下操作 |
| :--- | :--- |
| **通用选项** | |
| `secure` | 仅允许来自 1024 或更低端口的连接（默认） |
| `insecure` | 允许来自 1024 或更高端口的连接 |
| `ro` | 允许只读访问（默认） |
| `rw` | 允许读写访问 |
| `sync` | 在请求时执行写入操作（将信息写入磁盘）（默认） |
| `async` | 在服务器准备好时执行写入操作 |
| `no_wdelay` | 立即执行写入操作 |
| `wdelay` | 等待片刻以查看是否到达相关的写入请求，然后一起执行它们（默认） |
| `hide` | 隐藏已导出目录中作为另一个已导出目录子目录的目录（默认） |
| `no_hide` | 行为与 `hide` 完全相反 |
| `subtree_check` | 执行子树检查，即在访问文件时检查已导出子目录的父目录（默认） |
| `no_subtree_check` | 关闭子树检查（与 `subtree_check` 相反） |
| `insecure_locks` | 允许不安全的文件锁定 |
| **用户 ID 映射选项** | |
| `all_squash` | 将所有用户 ID 和组 ID 映射到客户端上的 `匿名用户` |
| `no_all_squash` | 将远程用户和组 ID 映射到客户端上类似的 ID（默认） |
| `root_squash` | 将远程 `root 用户` 映射到客户端上的 `匿名用户`（默认） |
| `no_root_squash` | 将远程 `root 用户` 映射到本地的 `root 用户` |
| `anounid=UID` | 设置 `匿名用户` 的用户 ID，用于 `all_squash` 和 `root_squash` 选项 |
| `anongid=GID` | 设置 `匿名用户` 的组 ID，用于 `all_squash` 和 `root_squash` 选项 |

![](img/11709a8f88c8cd03868a929dc94c0e2b_688_0.png)




####### 挂载 NFS 文件系统

在 `/etc/exports` 文件中添加条目后，在终端窗口中键入以下命令手动导出文件系统：

```
exportfs -a
```

该命令将导出在 `/etc/exports` 文件中定义的所有文件系统。

现在您可以启动 NFS 服务器进程了。

![](img/11709a8f88c8cd03868a929dc94c0e2b_689_0.png)

在 Debian 中，以 `root` 身份登录并在终端窗口中键入 `/etc/init.d/nfs-kernel-server start` 以启动 NFS 服务器。在 Fedora Core 中，键入 `/etc/init.d/nfs start`。在 SUSE 中，键入 `/etc/init.d/nfsserver start`。如果您希望 NFS 服务器在系统启动时自动运行，请在 Debian 中键入 `update-rc.d nfs-kernel-server defaults`。在 Fedora Core 中，键入 `chkconfig -level 35 nfs on`。在 SUSE 中，键入 `chkconfig -level 35 nfsserver on`。在 Xandros 中，键入 `update-rc.d nfs-user-server defaults`。

当 NFS 服务启动后，NFS 的服务器端即准备就绪。现在您可以尝试从客户端系统挂载导出的文件系统，并按需访问该导出文件系统。

![](img/11709a8f88c8cd03868a929dc94c0e2b_689_1.png)

如果您更改了 `/etc/exports` 文件中列出的任何导出文件系统，请记得重启 NFS 服务。要重启服务，请以 `restart` 作为参数调用 `/etc/init.d` 目录中的脚本（而不是用于启动服务的 `start` 参数）。

######## 挂载 NFS 文件系统的步骤

要在客户端系统上访问导出的 NFS 文件系统，您必须将该文件系统挂载到一个挂载点上。**挂载点** 不过是一个本地目录。例如，假设您希望访问名为 `LNBP200` 的服务器导出的 `/home` 目录，并希望在客户端系统的本地目录 `/mnt/lmbp200` 上访问它。要做到这一点，请按照以下步骤操作：

1. **以 `root` 身份登录，并使用此命令创建目录：**
   ```bash
   mkdir /mnt/lmbp200
   ```

2. **键入以下命令，将远程系统（LNBP200）上的目录挂载到本地目录 `/mnt/lmbp200`：**
   ```bash
   mount lmbp200:/home /mnt/lmbp200
   ```

完成这些步骤后，您就可以通过本地目录 `/mnt/lmbp200` 查看和访问导出的文件了。

要确认 NFS 文件系统确实已挂载，请在客户端系统上以 **root** 身份登录，并在终端窗口中键入 **mount**。您会看到关于 NFS 文件系统的一行类似以下内容：

```
lnbp200:/home/public0 on /mnt/lnbp200 type nfs (rw,addr=192.168.0.4)
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_690_0.png)

NFS 支持两种类型的挂载操作——硬挂载和软挂载。默认情况下挂载是硬挂载，这意味着如果 NFS 服务器无响应，客户端会无限期地尝试访问服务器，直到服务器响应为止。您可以将 NFS 卷进行软挂载，方法是向挂载命令添加 -o soft 选项。对于软挂载，如果 NFS 服务器无响应，客户端将返回错误。

###### 使用 Samba 设置 Windows 服务器

如果您依赖 Windows 进行文件共享和打印共享，那么您可能在服务器和客户端中都使用了 Windows。如果是这样，您仍然可以迁移到 Linux PC 作为您的服务器，而不会失去 Windows 文件共享和打印共享功能；您可以将 Linux 设置为 Windows 服务器。当您从本书的配套 DVD-ROM 安装 Linux 时，您还可以有机会安装 Samba 软件包，该软件包执行此设置。您只需在安装期间选择 Windows File Server 包组即可。

![](img/11709a8f88c8cd03868a929dc94c0e2b_690_1.png)

在您的 Linux PC 上安装并配置 Samba 后，您的客户端 PC——即使它们运行的是旧版 Windows for Workgroups 操作系统或较新的 Windows 95/98/NT/2000/XP 版本——也可以访问 Linux PC 上的共享磁盘和打印机。为此，它们使用服务器消息块（SMB）协议，该协议是 Windows 文件和打印共享的底层协议。

安装 Samba 包后，您可以将 Linux PC 设置为 Windows 客户端，这意味着 Linux PC 可以访问由 Windows 服务器管理的磁盘和打印机。同时，您的 Linux PC 也可以是网络上其他 Windows 系统的客户端。

Samba 软件包具有以下主要组件：

- **/etc/samba/smb.conf**：这是 SMB 服务器使用的 Samba 配置文件。
- **/etc/samba/smbusers**：此 Samba 配置文件显示了与本地 Linux PC 上的用户名相对应的 Samba 用户名。
- **nmbd**：这是 NetBIOS 名称服务器，客户端使用它来查找服务器。（NetBIOS 代表 *Network Basic Input/Output System*（网络基本输入/输出系统）——应用程序用于与网络传输（如 TCP/IP）进行通信的接口。）
- **nmblookup**：此命令返回由 NetBIOS 名称标识的 Windows PC 的 IP 地址。
- **smbadduser**：此程序将用户添加到 SMB（服务器消息块）密码文件中。
- **smbcacls**：此程序操作共享文件上的 Windows NT 访问控制列表（ACL）。
- **smbclient**：这是运行在 Linux 上的 Windows 客户端，允许 Linux 访问任何 Windows 服务器上的文件和打印机。
- **smbcontrol**：此程序向 smbd、nmbd 或 winbindd 进程发送消息。
- **smbd**：这是 SMB 服务器，它接受来自 Windows 客户端的连接并提供文件共享和打印共享服务。
- **smbmount**：此程序在 Linux PC 上挂载 Samba 共享目录。
- **smbpasswd**：此程序更改 SMB 用户的密码。
- **smbprint**：此脚本启用 SMB 服务器上打印机的打印功能。
- **smbstatus**：此命令列出主机的当前 SMB 连接。
- **smbta**：此程序将 SMB 共享直接备份到 Linux 系统上的磁带驱动器。
- **smbunmount**：此程序卸载当前挂载的 Samba 共享目录。
- **testparm**：此程序确保 Samba 配置文件是正确的。
- **winbindd**：此服务器解析来自 Windows NT 服务器的名称。

在下面的章节中，我将描述如何配置和使用 Samba。

####### 安装 Samba

您在安装 Linux 时可能已经安装了 Samba。您可以先检查一下，如果系统上没有发现 Samba，可以轻松安装它。

![](img/11709a8f88c8cd03868a929dc94c0e2b_691_0.png)

在 Debian、MEPIS、Ubuntu 和 Xandros 中，键入 `dpkg -l samba*` 以查看是否已安装 Samba。在 Fedora Core 和 SUSE 中，键入 `rpm -q samba` 以查看是否安装了 samba 包。

![](img/11709a8f88c8cd03868a929dc94c0e2b_691_1.png)

在 Debian、MEPIS 和 Ubuntu 中，键入 `apt-get install samba` 以安装 Samba。在 Fedora Core 中，以 root 身份登录，挂载 DVD，并键入 `cd /media/cdrom/Fedora/RPMS` 后跟 `rpm -vh samba*`。在 SUSE 中，点击 YaST 控制中心“软件”类别中的“软件管理”。然后使用 YaST 的搜索功能查找 `samba`，选择相关软件包并安装它们。至于 Xandros，安装 Xandros 时即会安装 Samba。

安装 Samba 软件后，在使用之前必须配置 Samba。

####### 配置 Samba

要设置 Windows 文件共享和打印共享服务，您可以手动编辑配置文件或使用 GUI 工具。当然，使用 GUI 工具比编辑配置文件容易得多。Fedora Core 和 SUSE 都配备了用于配置 Samba 服务器的 GUI 工具。

在 Fedora Core 中，选择 桌面→系统设置→服务器设置→Samba 以打开 Samba 服务器配置窗口。点击“添加”并填入您希望与 Windows 系统共享的目录信息，如图 6-1 所示。点击“访问”选项卡以指定哪些用户可以访问共享目录。Samba 服务器配置工具通过在配置文件 /etc/samba/smb.conf 中添加条目来创建 Samba 共享。

![](img/11709a8f88c8cd03868a929dc94c0e2b_692_0.png)

**图 6-1：** 在 Fedora Core 中添加 Samba 共享。

在 SUSE 中，您可以通过 YaST 控制中心配置 Samba——选择 主菜单→系统→控制中心 (YaST)——点击窗口左侧的“网络服务”，然后点击窗口右侧的“Samba 服务器”。YaST 显示一个窗口（见图 6-2），您可以配置 Samba。首先，您选择一个工作组名称（YaST 显示您局域网中任何现有 Windows 工作组名称）并点击“下一步”。然后您可以选择服务器类型，启用服务器，并选择要共享的内容。退出 Samba 服务器配置实用程序后，YaST 将 Samba 设置存储在 /etc/samba 目录中的配置文件中。





## 668 使用 Samba 配置 Windows 服务器

**图 6-2：** 在 SUSE 中，您可以通过 YaST 配置 Samba 服务器。

![](img/11709a8f88c8cd03868a929dc94c0e2b_693_0.png)

配置好 Samba 后，在终端窗口中输入以下命令，以验证 Samba 配置文件是否正常：

```
testparm
```

如果该命令提示文件加载正常，则您可以开始使用。`testparm` 命令还会显示 Samba 配置文件的内容。

####### 技术细节

Samba 使用 `/etc/samba/smb.conf` 文件作为其配置文件。这是一个文本文件，其语法类似于 Microsoft Windows 3.1 的 INI 文件。您可以在 Linux 系统上通过任何文本编辑器编辑该文件。与旧版 Windows INI 文件一样，`/etc/samba/smb.conf` 文件由多个部分组成，每个部分包含一组参数。`smb.conf` 文件的每个部分以括号内的部分名称开始。该部分一直持续到下一个部分开始或文件结束。每一行使用 `name = value` 语法来指定参数的值。与 Windows INI 文件相同，以分号 (;) 开头的行是注释行。在 `/etc/samba/smb.conf` 文件中，注释行也可以以井号 (#) 开头。

####### 发行版特定操作

若要在系统重启时自动启动 Samba 服务，请在 Debian、MEPIS、Ubuntu 和 Xandros 中运行 `update-rc.d samba defaults`。在 Fedora Core 和 SUSE 中，请运行 `chkconfig --level 35 smb on`。若立即启动 Samba，请在 Fedora Core 和 SUSE 中运行 `/etc/init.d/smb start`。在 Debian、MEPIS、Ubuntu 和 Xandros 中，请运行 `/etc/init.d/samba start`。

####### 试用 Samba

现在，您可以尝试从局域网中的任一 Windows 系统访问 Linux 系统上的 Samba 服务器。在 Windows 95/98/ME 桌面上，双击“网上邻居”图标。在 Windows XP 中，选择“开始 · 网上邻居”，然后点击“查看工作组计算机”。所有位于同一工作组中的计算机都会显示出来。

当您看到 Samba 服务器时，可以通过双击图标打开它。系统会提示您输入 Samba 用户名和密码，输入正确信息后，您就可以访问 Samba 共享上的文件夹和打印机（如果有的话）。

您可以使用 smbclient 程序访问局域网中 Windows 系统上的共享目录和打印机，并检查您的 Linux Samba 服务器是否正常工作。快速检查的方法是，在终端窗口中输入 `smbclient -L`，以查看 Linux Samba 服务器本身提供的服务列表。

####### 进一步了解 Samba

Samba 的内容远不止本章所展示的。若想深入了解 Samba，您可以查阅以下资源：

- 要在线查看 Samba 文档，请访问 www.samba.org/samba/docs/man/Samba-HOWTO-Collection。
- Jay Tis、Robert Eckstein 和 David Collie-Brown 合著的《Using Samba, 2nd Edition》（O’Reilly & Associates，2003 年 2 月出版）

您还应访问 www.samba.org 以了解 Samba 开发的最新动态。该网站还提供了学习 Samba 的相关资源链接。

## 第八卷

#### 编程

Rich Tennant 的《第五波》

> 万达突然感觉到，她丈夫的新软件程序即将变得具有交互性。

![](img/11709a8f88c8cd03868a929dc94c0e2b_696_0.png)

#### 内容概览

- 第 1 章：Linux 中的编程 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 673
- 第 2 章：C 语言编程 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 699
- 第 3 章：编写 Shell 脚本 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 731
- 第 4 章：Perl 编程 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 743

##### 第 1 章：Linux 中的编程

###### 本章内容

- 学习编程
  - 探索 Linux 中的软件开发工具
  - 使用 GCC 编译和链接程序
  - 使用 `make`
  - 使用 `gdb` 调试程序
  - 理解 GNU、GPL 和 LGPL 的影响

*Linux 自带了您开发软件所需的所有工具。（您只需安装它们即可。）特别是，它包含了所有 GNU 软件开发工具，例如 GCC（C 和 C++ 编译器）、GNU make 以及 GNU 调试器。在本章中，我将介绍编程知识，描述这些软件开发工具，并展示如何使用它们。虽然我使用了 C 和 C++ 编程语言的示例，但重点并非展示如何用这些语言编程，而是展示如何使用各种软件开发工具（如编译器、make 和调试器）。*

我还简要说明了自由软件基金会（Free Software Foundation）的 GNU 通用公共许可证（GPL）可能会如何影响您在 Linux 上开发软件的计划。由于您在 Linux 上使用 GNU 工具和 GNU 库开发软件，因此了解这一点非常重要。

###### 编程概述

如果您曾经用任何编程语言编写过计算机程序，您可以很快开始在 Linux 系统上编写程序。然而，如果您从未编写过计算机程序，那么在开始之前，您需要两个基本资源：了解编程基础知识，以及快速回顾计算机及其主要组成部分。在本节中，我将为您提供计算机编程概述——足以让您入门。

###### 计算机的简化视图

在体验计算机编程之前，您需要了解计算机程序在计算机其他部分中的位置。图 1-1 展示了计算机的简化视图，突出了对程序员重要的主要部分。

**674 编程概述**

![](img/11709a8f88c8cd03868a929dc94c0e2b_699_0.png)

图 1-1：计算机的简化视图及其运行程序的方式。

计算机的核心是中央处理单元（CPU），它执行计算机程序中包含的指令。执行此任务的具体硬件（其制造商称之为微处理器，我们其他人称之为芯片）因系统而异：在 Pentium PC 中，它是 Pentium；在 Sun SPARC 工作站中，它是 SPARC 芯片；在 HP UNIX 工作站中，它是 PA-RISC 芯片。这些微处理器具有不同的功能，但使命相同：告诉计算机该做什么。

随机存取内存（RAM），或简称内存，在 CPU 执行计算机程序时充当存储介质。如果程序处理某些数据，这些数据也存储在内存中。内存的内容不是永久的；当计算机关闭或程序不再运行时，它们会消失（永不再回）。

硬盘（也称为磁盘或驱动器）充当计算机程序和数据的永久存储空间。硬盘被组织成文件，文件又组织在层次化的目录和子目录中（有点像将纸质文件夹放在文件柜的抽屉中）。每个文件本质上是一个存储块，可以保存各种信息。例如，文件可以是人类可读的文本文件，也可以是仅对 CPU 有意义的计算机指令集合。当您创建计算机程序时，您需要大量处理文件。

对于程序员来说，另外两个重要项目是输入和输出——程序如何从用户获取输入并向用户显示输出。用户通过键盘和鼠标提供输入，输出则显示在监视器上。然而，程序也可以从文件接受输入并将输出发送到文件。

###### 操作系统的作用

*操作系统* 是一个特殊的计算机程序集合，其主要目的是加载和运行其他程序。操作系统还充当软件和硬件之间的接口。所有操作系统都包含一个或多个命令处理器（在 Linux 中称为 *shell*），允许用户输入命令并执行任务，如运行程序或打印文件。大多数操作系统还包含图形用户界面（如 Linux 中的 GNOME 和 KDE），允许用户通过点击屏幕图标执行大多数任务。Linux、Windows（无论是 NT、2000 还是 XP 版本）以及各种版本的 UNIX（包括 Linux）都是操作系统的例子。

正是操作系统赋予了计算机个性。例如，您可以在 PC 上运行 Windows 2000 或 Windows XP。在同一台 PC 上，您也可以安装并运行 Linux。这意味着，取决于安装在其上的操作系统，同一台 PC 可以是 Windows 2000、Windows XP 或 Linux 系统。

计算机程序是建立在 *操作系统之上* 的。这意味着计算机程序必须利用操作系统所包含的功能。例如，计算机程序通过操作系统的内置功能来读写文件。（如果操作系统不会煮咖啡，任何程序也无法命令它煮咖啡并期望得到积极的结果。）

尽管细节有所不同，大多数操作系统都支持许多相似的概念。作为程序员，您需要熟悉以下少量概念：

- *进程* 是正在计算机中运行的计算机程序。大多数操作系统允许多个进程同时运行。
- *命令处理器* 或 *shell* 是一个特殊程序，允许用户输入命令并执行各种任务，如运行任何程序、查看大量文件或打印文件。在 Windows 2000 或 Windows XP 中，您可以在命令提示符窗口中输入命令。
- 术语 *命令行* 指的是用户输入给命令处理器的命令。通常，命令行包含一个命令和一个或多个 *选项*——命令是行中的第一个词，其余的是选项（要求计算机执行的具体行为）。
- *环境变量* 本质上是有名称的文本字符串。例如，PATH 环境变量指代一个包含目录名称的字符串。操作系统使用环境变量向进程提供有用的信息。要查看 Windows 2000 或 Windows XP 系统中的环境变量列表，请在命令提示符窗口中输入 **set**。在 Linux 中，您可以输入 **printenv** 来查看环境变量。

在 Linux 中编程




###### 计算机编程基础

*计算机程序* 是指为了执行特定任务（例如计算两个数之和或在文件中查找某些文本）而列出的指令序列。因此，计算机编程涉及*创建*该指令列表，以告知计算机如何完成特定任务。具体的指令取决于你所使用的编程语言。对于大多数编程语言而言，你需要遵循以下步骤来创建计算机程序：

1. 使用文本编辑器输入编程语言中的命令序列。
   该命令序列实现了你的任务。这个人类可读的程序版本被称为*源文件*或*源代码*。你可以使用任何能够以纯文本格式保存文档的应用程序（如文字处理器）来创建源文件。

   请始终将你的源代码保存为纯文本。（文件名取决于编程语言的类型。）文字处理器有时会在其文档中加入额外的指令，以告知计算机按特定字体或其他格式显示文本。将文件保存为纯文本会删除所有这些额外指令。相信我，去掉这些多余的内容，你的程序会更好。

2. 使用*编译器*程序将该文本文件——即*源代码*——从人类可读形式转换为机器可读的*目标代码*。
   通常，此步骤还会将多个目标代码文件合并为一个机器可读的计算机程序，即计算机实际可以运行的程序。

3. 使用一种称为*调试器*的特殊程序来追踪错误并找出源文件中可能导致错误的行。

4. 返回步骤 1，使用文本编辑器修复错误，并重复后续步骤。

这些步骤被称为编程的*编辑-编译-调试*循环，因为大多数程序员必须多次重复该序列才能使程序正确运行。

除了了解基本的编程步骤外，你还需要熟悉以下术语和概念：

- *变量* 用于存储不同类型的数据。你可以将每个变量视为数据的占位符——就像一个带有名称和数据存储空间邮箱。变量的内容即其值。
- *表达式* 通过运算符组合变量。一个表达式可以将几个变量相加；另一个表达式可以提取字符串的一部分。
- *语句* 执行某些操作，例如将值分配给变量或打印字符串。
- *流程控制语句* 允许语句根据某些表达式的值以不同顺序执行。通常，流程控制语句包括 *for*、*do-while*、*while* 和 *if-then-else* 语句。
- *函数*（也称为*子例程*或*例程*）允许你将多条语句分组并给该组命名。此功能使你可以通过调用代表这些语句的函数来执行相同的语句集。通常，编程语言提供许多预定义函数来执行诸如打开（并读取）文件等任务。

####### 探索 Linux 中的软件开发工具

Linux 包含以下传统的 UNIX 软件开发工具：

- 用于编辑源代码的文本编辑器，例如 *vi* 和 *emacs*。（要了解有关 *vi* 的更多信息，请参见第二卷第 5 章。）
- 用于编译和链接用 C 编写的程序的 C 编译器——C 是编写 UNIX 应用程序的首选编程语言（尽管如今许多程序员转向 C++ 和 Java）。Linux 包含 GNU C 和 C++ 编译器。最初，GNU C 编译器被称为 *GCC*——现在 *GCC* 代表 *GNU 编译器集合*（请参阅 http://gcc.gnu.org 上的描述）。
- GNU *make* 实用程序，用于自动化软件*构建过程*——即将目标模块组合成可执行文件或库的过程。（操作系统可以加载并运行可执行文件，而*库*是一组可被可执行文件使用的二进制代码。）
- 用于调试程序的调试器。Linux 包含 GNU 调试器 *gdb*。
- 版本控制系统，用于跟踪源文件的各种修订版本。Linux 附带 *RCS*（修订控制系统）和 *CVS*（并发版本控制系统）。如今，大多数开源项目使用 CVS 作为其版本控制系统，但一种名为 *Subversion* 的较新版本控制系统正在开发中，旨在取代 CVS。

你可以在任何 Linux 发行版中安装这些软件开发工具。Xandros 通常已预装这些工具。在 Fedora Core 中，安装期间请选择开发工具包。在 Debian 中，在终端窗口中输入 *apt-get install gcc*，然后点击*安装 libc6-dev*。在 SUSE 中，选择主菜单：系统::YaST，点击窗口左侧的软件，然后点击安装和卸载软件。在 YaST 的搜索框中输入 *gcc*，从搜索结果中选择相关软件包，然后点击接受进行安装。如果你发现缺少任何软件包，可以用类似的方式安装它们。

![](img/11709a8f88c8cd03868a929dc94c0e2b_702_0.png)

在接下来的几个部分中，我将简要描述如何使用这些软件开发工具为 Linux 编写应用程序。

####### GNU C 和 C++ 编译器

Linux 中最重要的软件开发工具是 GCC——GNU C 和 C++ 编译器。事实上，GCC 可以编译三种语言：C、C++ 和 Objective-C（一种为 C 添加面向对象编程能力的语言）。你使用相同的 gcc 命令来编译和链接 C 和 C++ 源文件。GCC 编译器支持 ANSI 标准 C，这使得将任何 ANSI C 程序移植到 Linux 变得很容易。此外，如果你曾在其他 UNIX 系统上使用过 C 编译器，你会觉得使用 GCC 非常亲切。

####### 使用 GCC

使用 gcc 命令来调用 GCC。默认情况下，当你在源文件上使用 gcc 命令时，GCC 会进行预处理、编译和链接以创建可执行文件。但是，你可以使用 GCC 选项在此过程中的某个中间阶段停止。例如，你可以使用 -c 选项调用 gcc 来编译源文件并生成目标文件，但不执行链接步骤。

使用 GCC 编译和链接几个 C 源文件非常简单。假设你想编译和链接一个由两个源文件组成的简单程序。我使用以下程序源代码完成此任务；它存储在文件 area.c 中，是一个通过命令行指定半径来计算圆面积的主程序：

```
#include <stdio.h>
#include <stdlib.h>
/* Function prototype */
double area_of_circle(double r);
int main(int argc, char **argv)
{
    if (argc < 2)
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

你需要另一个文件来实际计算圆的面积。以下是文件 `circle.c` 的列表，其中定义了一个计算圆面积的函数：

```
#include <math.h>
#define SQUARE(x) ((x) * (x))
double area_of_circle(double r)
{
    return 4.0 * M_PI * SQUARE(r);
}
```

对于这样一个简单的程序，我当然可以将所有内容放在单个文件中，但我需要这个虚构的例子来向你展示如何处理多个文件。

要编译这两个文件并创建一个名为 **area** 的可执行文件，你使用此命令：

```
gcc -o area area.c circle.c
```

此次 GCC 调用使用 `-o` 选项来指定可执行文件的名称。（如果你不使用 `-o` 选项指定输出文件的名称，GCC 会将可执行代码保存在名为 `a.out` 的文件中。）

如果你有太多的源文件需要编译和链接，你可以单独编译这些文件并*生成目标文件*（具有 `.o` 扩展名）。这样，当你更改源文件时，你只需要编译该文件——你只需将编译后的文件链接到所有目标文件。以下命令展示了如何为示例程序分离编译和链接步骤：

```
gcc -c area.c
gcc -c circle.c
gcc -o area area.o circle.o
```

前两个命令使用带有 `-c` 选项的 **gcc** 编译源文件。第三个 **gcc** 命令将目标文件链接为名为 **area** 的可执行文件。

如果你好奇的话，以下是如何运行 **area** 程序（计算半径为 1 的圆的面积）：

```
./area 1
```

程序生成以下输出：

```
Area of circle with radius 1.000000 = 12.566371
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_704_0.png)





顺便一提，只有当当前目录不在 PATH 环境变量中时，才需要在程序名称（区域）前添加 `./` 前缀。即使你的 PATH 包含当前目录，添加该前缀也无害。

####### 编译 C++ 程序

GNU CC 是一个集成的 C 和 C++ 编译器，因此 gcc 命令也可以编译 C++ 源文件。GCC 使用文件扩展名来判断文件是 C 还是 C++。C 文件的扩展名为小写的 .c，而 C++ 文件则以 .C 或 .cpp 结尾。

虽然 gcc 命令可以编译 C++ 文件，但该命令不会自动链接 C++ 程序通常所需的各类类库。这就是为什么使用 g++ 命令编译和链接 C++ 程序很轻松，因为它实际上是以适当的选项运行 gcc。

假设你要编译一个存储在名为 hello.C 的文件中的简单 C++ 程序。（使用大写 C 扩展名作为 C++ 源文件的扩展名是惯例。）

```
#include <iostream>
int main()
{
using namespace std;
cout << "Hello from Linux!" << endl;
}
```

要将此程序编译和链接为名为 hello 的可执行程序，请使用以下命令：

g++ -o hello hello.C

该命令会创建 hello 可执行文件，你可以按以下方式运行它：

./hello

程序将显示以下输出：

Hello from Linux!

众多 GCC 选项控制着编译 C 和 C++ 程序的各个方面。

####### 探索 GCC 选项

以下是 gcc 命令的基本语法：

```
gcc options filenames
```

每个选项都以连字符 (-) 开头，通常具有较长的名称，例如 `-funsigned-char` 或 `-ffinite-functions`。然而，许多常用选项较短，例如用于仅编译的 `-c`，以及用于生成调试信息的 `-g`（使用 GNU 调试器 gdb 调试程序时需要这些信息）。

你可以在终端窗口中键入以下命令查看所有 GCC 选项的摘要：

```
man gcc
```

然后你可以浏览常用的 GCC 选项。通常，你不需要显式提供 GCC 选项，因为默认设置对于大多数应用程序都是合适的。表 1-1 列出了你可能使用的一些 GCC 选项。

**表 1-1 常用 GCC 选项**

| 选项 | 含义 |
| :--- | :--- |
| -ansi | 仅支持 ANSI 标准 C 语法。（此选项禁用某些 GNU C 特有的功能，如 `__asm__` 和 `__typeof__` 关键字。）当与 g++ 一起使用时，仅支持 ISO 标准 C++。 |
| -c | 仅编译并生成目标文件 |
| -DMACRO | 定义宏，其值为字符串 "1" |
| -DMACRO=DEFN | 将宏定义为 DEFN，其中 DEFN 是某个文本字符串。 |
| -E | 仅运行 C 预处理器 |
| -fallow-single-precision | 以单精度执行所有数学运算 |
| -fpic-struct-return | 在内存中返回所有结构体和联合体值，而不是在寄存器中返回。（以这种方式返回值效率较低，但至少与其他编译器兼容。） |
| -fPIC | 生成适用于共享库的位置无关代码 (PIC) |
| -freg-struct-return | 在可能时，在寄存器中返回结构体和联合体值 |
| -g | 生成调试信息。（GNU 调试器可以使用这些信息。） |
| -I DIRECTORY | 搜索指定目录中通过使用 #include 预处理器指令包含的文件 |
| -L DIRECTORY | 搜索指定目录中的库 |
| -l LIBRARY | 在链接时搜索指定的库 |
| -mcputype | 针对特定处理器优化代码。（*cpptype* 可以取许多不同的值 - 一些常见的值包括 *i386, i486, i586, i686, pentium, pentiumpro, pentium2, pentium3, pentium4*。） |
| -O FILE | 生成指定的输出文件（用于指定可执行文件的名称） |
| -00 (两个零) | 不进行优化 |
| -O 或 -O1 (字母 O) | 优化生成的代码 |
| -O2 (字母 O) | 进行更多优化 |
| -O3 (字母 O) | 执行超出 `-O2` 范围的优化 |
| -Os (字母 O) | 针对大小进行优化（以减少代码总量） |
| -pedantic | 如果使用了任何非 ANSI 标准扩展，则生成错误 |
| -pg | 向程序添加额外代码，使其在运行时生成 *gprof* 程序可用来显示程序各部分计时详情的信息 |
| -shared | 生成共享对象文件（通常用于创建共享库） |
| -UNMACRO | 取消定义指定的宏 |
| -v | 显示 GCC 的版本号 |
| -w | 不生成任何警告消息 |
| -W1, OPTION | 将 *OPTION* 字符串（包含多个以逗号分隔的选项）传递给链接器。例如，要创建名为 *libXXX.so.1* 的共享库，请使用以下标志：`-W1,-soname,libXXX.so.1`。 |

####### GNU make 实用工具

当应用程序由多个源文件组成时，手动键入 *gcc* 命令来编译和链接这些文件可能会非常繁琐。此外，你也不希望在更改单个源文件时重新编译每个文件。正是在这种情况下，*GNU make* 实用工具可以助你一臂之力。

*make* 实用工具通过读取和解释 *makefile* 来工作——*makefile* 是一个文本文件，描述了构建特定程序所需哪些文件，以及如何编译和链接这些文件来构建程序。每当更改一个或多个文件时，*make* 会确定需要重新编译哪些文件——并发出编译这些文件和重建程序的适当命令。

####### Makefile 名称

默认情况下，GNU make 查找名为以下之一（按所示顺序）的 makefile：

- GNUmakefile
- makefile
- Makefile

在 UNIX 系统中，习惯使用 Makefile 作为 makefile 的名称，因为它出现在目录列表的开头附近，其中大写名称出现在小写名称之前。

当你从互联网下载软件时，你通常会找到 Makefile，以及源文件一起。要构建软件，你只需在 shell 提示符下键入 make，make 就会处理构建软件所需的所有步骤。

如果你的 makefile 没有标准名称（例如 Makefile），你必须使用 make 的 -f 选项来指定 makefile 名称。例如，如果你的 makefile 名为 myprogram.mk，你必须使用以下命令行运行 make：

```
make -f myprogram.mk
```

## The makefile

对于一个由多个源文件和头文件组成的程序，makefile 指定以下内容：

- make 创建的项目——通常是目标文件和可执行文件。常用术语 target 来指代 make 需要创建的任何项目。
- 创建 target 所需的文件或其他操作。
- 创建每个 target 时要执行哪些命令。

假设你有一个名为 form.C 的 C++ 源文件，其中包含以下预处理器指令：

```
#include "form.h"  // 包含头文件
```

目标文件 form.o 显然依赖于源文件 form.C 和头文件 form.h。除了这些依赖项之外，你还必须指定 make 如何将 form.C 文件转换为目标文件 form.o。假设你希望 make 调用 g++（因为源文件是 C++），并使用以下选项：

- -c (仅编译)
- -g (生成调试信息)
- -O2 (进行一些优化)

在 makefile 中，你可以用以下规则来表示这些选项：

```
# 这是 makefile 中的一行注释
# 以下行说明 form.o 如何依赖
# 于 form.C 和 form.h 以及如何创建 form.o。
form.o: form.C form.h
    g++ -c -g -O2 form.C
```

在此示例中，第一个非注释行显示 form.o 为 target，form.C 和 form.h 为依赖文件。

依赖项之后的行说明了如何从依赖项构建 target。此行必须以制表符（Tab）开头。否则，make 命令将退出并显示错误消息，你会抓耳挠腮，因为在文本编辑器中查看 makefile 时，你无法区分制表符和空格。既然你已经知道了这个秘密，解决方法就是用单个制表符替换有问题的行开头的空格。

使用 make 的好处是它可以防止不必要的编译。毕竟，你可以从 shell 脚本运行 g++（或 gcc）来编译和链接组成你应用程序的所有文件，但 shell 脚本会编译所有内容，即使编译是不必要的。另一方面，GNU make 仅在 target 的一个或多个依赖项自上次构建 target 以来发生了变化时才构建 target。make 通过检查 target 和依赖项的最后修改时间验证此更改。

make 将 target 视为要达成的目标名称；target 不必是文件。你可以有这样的规则：

```
clean:
    rm -f *.o
```

此规则指定了一个名为 clean 的抽象 target，它不依赖任何内容。这个依赖声明表示，为了创建 target clean，GNU make 调用命令 rm -f *.o，该命令删除所有具有 .o 扩展名的文件（即目标文件）。因此，创建名为 clean 的 target 的净效果是删除目标文件。

####### 变量（或宏）

除了从依赖项构建 target 的基本功能外，GNU make 还包括许多实用功能，使您能够轻松表达从依赖项构建 target 的依赖项和规则。如果需要



####### 使用 Make 编译多个 C++ 文件

如果要使用 GCC 以相同的选项编译大量的 C++ 文件，例如为每个文件键入选项会非常繁琐。你可以通过在 make 中定义变量或宏来避免这种重复性任务，如下所示：

```
# 定义编译器的名称宏
CXX= g++
# 定义 GCC 标志的宏
CXXFLAGS= -O2 -g -mcpu=i686
# 构建目标文件的规则
form.o: form.C form.h
        $(CXX) -c $(CXXFLAGS) form.C
```

在此示例中，`CXX` 和 `CXXFLAGS` 是 *make* 变量。（*GNU make* 倾向于称它们为变量，但大多数 UNIX make 实用程序称它们为宏。）

要在 makefile 中的任何位置使用变量，请先使用美元符号 ($)，后跟括号内的变量。GNU make 会用定义替换变量的所有出现；因此，它用字符串 `-O2 -g -mcpu=i686` 替换 `$(CXXFLAGS)` 的所有出现。

GNU make 有几个具有特殊含义的预定义变量。表 1-2 列出了这些变量。除了表 1-2 中列出的变量外，GNU make 还将所有环境变量（如 PATH 和 HOME）视为预定义变量。

| 变量 | 含义 |
| :--- | :--- |
| $% | 存档目标中的成员名称。例如，如果目标是 libDisp.a (image.o)，则 $% 是 image.o。 |
| $* | 不含扩展名的目标文件名称 |
| $+ | 所有依赖文件的名称，重复的依赖项按其出现顺序列出 |
| $< | 第一个依赖文件的名称 |
| $? | 所有比目标更新的依赖文件的名称（名称之间用空格分隔） |
| $@ | 目标的完整名称。例如，如果目标是 libDisp.a (image.o)，则 $@ 是 libDisp.a |
| $^ | 所有依赖文件的名称，名称之间用空格分隔。依赖文件名中的重复项会被移除。 |
| AR | 存档维护程序的名称（默认值：ar） |
| ARFLAGS | 存档维护程序的标志（默认值：rv） |
| AS | 将汇编语言转换为目标代码的汇编器程序的名称（默认值：as） |
| ASFLAGS | 汇编器的标志 |
| CC | C 编译器的名称（默认值：cc） |
| CFLAGS | 传递给 C 编译器的标志 |
| CO | 从 RCS 提取文件的程序名称（默认值：co） |
| COFLAGS | RCS co 程序的标志 |
| CPP | C 预处理器的名称（默认值：$(CC) -E） |
| CPPFLAGS | C 预处理器的标志 |
| CXX | C++ 编译器的名称（默认值：g++） |
| CXXFLAGS | 传递给 C++ 编译器的标志 |
| FC | FORTRAN 编译器的名称（默认值：f77） |
| FFLAGS | FORTRAN 编译器的标志 |
| LDFLAGS | 编译器调用链接器 ld 时使用的标志 |
| RM | 删除文件的命令名称（默认值：rm -f） |

####### 示例 makefile

如果你使用 GNU make 的预定义变量及其内置规则，就可以轻松地编写 makefile。例如，考虑一个 makefile，它从三个 C 源文件（xdraw.c、xviewobj.c 和 shapes.c）和两个头文件（xdraw.h 和 shapes.h）创建可执行文件 xdraw。假设每个源文件都包含其中一个头文件。基于这些事实，示例 makefile 可能如下所示：

```
#####################################################################
####### 示例 makefile
# 注释以 '#' 开头
#
#####################################################################
# 使用标准变量定义编译和链接标志
CFLAGS= -g -O2
# 定义目标 "all"
all: xdraw


OBJS=xdraw.o xviewobj.o shapes.o
xdraw: $(OBJS)

# 目标文件
xdraw.o: Makefile xdraw.c xdraw.h
xviewobj.o: Makefile xviewobj.c xdraw.h
shapes.o: Makefile shapes.c shapes.h
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_712_0.png)

此 *makefile* 依赖于 GNU *make* 的隐含规则。将 .c 文件转换为 .o 文件使用内置规则。定义变量 *CFLAGS* 会将标志传递给 C 编译器。

名为 *all* 的目标被定义为第一个目标是有原因的——如果你在命令行中不指定任何目标就运行 GNU *make*（参见下一节中描述的 *make* 语法），该命令将构建 *makefile* 中找到的第一个目标。通过定义第一个目标 *all* 为 *xdraw*，你可以确保 *make* 构建此可执行文件，即使你未明确将其指定为目标。UNIX 程序员传统上使用 *all* 作为第一个目标的名称，但目标名称无关紧要；重要的是它是 *makefile* 中的第一个目标。

####### 如何运行 make

通常，你只需在 shell 提示符下键入以下命令来运行 *make*：

make

以这种方式运行时，GNU *make* 会按以下顺序查找名为 *GNUmakefile*、*makefile* 或 *Makefile* 的文件。如果 *make* 找到这些 *makefile* 之一，它会构建该 *makefile* 中指定的第一个目标。然而，如果 *make* 未找到合适的 *makefile*，它将显示以下错误消息并退出：

make: *** No targets specified and no *makefile* found. Stop.

如果你的 *makefile* 名称恰好不同于默认名称，你必须使用 *-f* 选项来指定 *makefile*。使用此选项时 *make* 命令的语法是

make -f *filename*

其中 *filename* 是 *makefile* 的名称。

即使你有一个默认名称为 *Makefile* 的 *makefile*，你可能也想构建 *makefile* 中定义的多个目标中的特定目标。在这种情况下，你运行 *make* 时必须使用以下语法：

make target

例如，如果 *makefile* 包含名为 *clean* 的目标，你可以使用此命令构建该目标：

make clean

另一种特殊语法可以覆盖 *make* 变量的值。例如，GNU *make* 使用 `CFLAGS` 变量来保存编译 C 文件时使用的标志。你调用 *make* 时可以覆盖此变量的值。以下是如何将 `CFLAGS` 定义为选项 `-g -O2` 的示例：

```
make CFLAGS="-g -O2"
```

除了这些选项外，GNU *make* 还接受其他几个命令行选项。表 1-3 列出了 GNU *make* 选项。

| 选项 | 含义 |
| :--- | :--- |
| -b | 忽略但接受，以与其他版本的 make 兼容 |
| -C DIR | 在读取 makefile 之前更改到指定目录 |
| -d | 打印调试信息 |
| -e | 允许环境变量覆盖 makefile 中同名变量的定义 |
| -f FILE | 将 FILE 读取为 makefile |
| -h | 显示 make 选项列表 |
| -i | 忽略构建目标时执行的命令中的所有错误 |
| -I DIR | 在指定目录中搜索包含的 makefile。（在 makefile 中包含文件的功能是 GNU make 独有的。） |
| -j NUM | 指定 make 可以同时运行的命令数 |
| -k | 即使构建某个目标时发生错误，也继续构建不相关的目标 |
| -l LOAD | 如果负载平均值至少为 LOAD（一个浮点数），则不要启动新任务 |
| -m | 忽略但接受，以与其他版本的 make 兼容 |
| -n | 打印要执行的命令，但不执行它们 |
| -o FILE | 不重建名为 FILE 的文件，即使它比其依赖项旧 |
| -p | 显示 make 的变量和隐含规则数据库 |
| -q | 不运行任何内容，但如果所有目标都是最新的则返回 0（零）；如果需要更新任何内容则返回 1；如果发生错误则返回 2 |
| -r | 消除所有内置规则 |
| -R | 消除所有内置变量和规则 |
| -s | 安静工作（不显示正在执行的命令） |
| -t | 更改文件的时间戳 |
| -v | 显示 **make** 的版本号和版权声明 |
| -w | 在处理 **makefile** 之前和之后显示工作目录的名称 |
| -w FILE | 假设指定文件已被修改（与 **-n** 一起使用，以查看如果修改该文件会发生什么）。 |

#### GNU 调试器

尽管 **make** 自动化了构建程序的过程，但当程序不能正确工作或突然退出并显示错误消息时，编程中这部分是你最不需要担心的。你需要一个调试器来找出程序错误的原因。Linux 包含 **gdb** —— 具有命令行接口的多功能 GNU 调试器。

像任何调试器一样，**gdb** 允许你执行典型的调试任务，例如：

- 设置断点，使程序在指定行停止
- 监视程序中变量的值
- 逐行单步执行程序
- 修改变量以尝试修复错误

**gdb** 调试器可以调试 C 和 C++ 程序。

######## 准备调试程序

如果你想使用 **gdb** 调试程序，你必须确保编译器生成并将调试信息放置在可执行文件中。调试信息包含程序中变量的名称以及可执行文件中地址到源文件中代码行的映射。**gdb** 需要此信息来执行其功能，例如在执行指定的源代码行后停止。

![](img/11709a8f88c8cd03868a929dc94c0e2b_714_0.png)

为了确保可执行文件已正确准备好进行调试，请使用 GCC 的 -g 选项。你可以通过在 **makefile** 中定义变量 **CFLAGS** 来执行此任务：

```
CFLAGS= -g
```

######## 运行 gdb

调试程序最常见的方法是使用以下命令运行 **gdb**：





## 第八卷
## 第 1 章
### 在 Linux 中编程

`gdb progname`

`progname` 是程序可执行文件的名称。运行后，`gdb` 会显示以下信息，并提示输入命令：

```
GNU gdb 6.3
Copyright 2004 Free Software Foundation, Inc.
GDB is free software, covered by the GNU General Public License, and you are
welcome to change it and/or distribute copies of it under certain conditions.
Type "show copying" to see the conditions.
There is absolutely no warranty for GDB.  Type "show warranty" for details.
This GDB was configured as `i586-suse-linux'.
(gdb)
```

你可以在 `(gdb)` 提示符处输入 `gdb` 命令。一个有用的命令是 `help` —— 它会显示命令列表，如下一个列表所示：

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
tracepoints -- Tracing of program execution without stopping the program
user-defined -- User-defined commands

Type "help" followed by a class name for a list of commands in that class.
Type "help" followed by command name for full documentation.
Command name abbreviations are allowed if unambiguous.
(gdb)
```

要退出 `gdb`，请输入 `q` 然后按 Enter 键。

`gdb` 拥有大量命令，但你只需要其中几个就能快速找到错误的原因。表 1-4 列出了常用的 `gdb` 命令。

####### 表 1-4 常用 `gdb` 命令

| **该命令** | **执行的操作** |
| :--- | :--- |
| `break` `NUM` | 在指定的行号设置一个 `断点`。（调试器会在 `断点` 处停止。） |
| `bt` | 显示所有堆栈帧的跟踪。（此命令显示迄今为止的函数调用序列。） |
| `clear FILENAME:NUM` | 删除源文件中特定行的断点。例如，`clear xdraw.c:8` 清除文件 `xdraw.c` 第 8 行的断点。 |
| `continue` | 继续运行正在调试的程序。（在程序因信号或断点停止后使用此命令。） |
| `display EXPR` | 每次程序停止时，显示表达式（由程序中定义的变量组成）的值 |
| `file FILE` | 加载指定的可执行文件以进行调试 |
| `help NAME` | 显示名为 **NAME** 的帮助命令 |
| `info break` | 显示当前断点列表，包括每个断点被触发的次数信息 |
| `info files` | 显示有关正在调试文件的详细信息 |
| `info func` | 显示所有函数名称 |
| `info local` | 显示当前函数的局部变量信息 |
| `info prog` | 显示正在调试程序的执行状态 |
| `info var` | 显示所有全局和静态变量名称 |
| `kill` | 终止你正在调试的程序 |
| `list` | 列出源代码的一部分 |
| `make` | 运行 **make** 实用程序以重新构建可执行文件，而无需离开 **gdb** |
| `next` | 在当前函数中前进一行源代码，不进入其他函数 |
| `print EXPR` | 显示表达式 **EXPR** 的值 |
| `quit` | 退出 **gdb** |
| `run` | 开始运行当前加载的可执行文件 |
| `set variable VAR=VALUE` | 将变量 **VAR** 的值设置为 **VALUE** |
| `shell CMD` | 执行 UNIX 命令 **CMD**，而无需离开 **gdb** |
| `step` | 在当前函数中前进一行，进入其他函数（如果有） |
| `watch VAR` | 每当变量 **VAR** 的值发生变化时，显示该变量的值 |
| `where` | 显示调用序列。使用此命令来定位你的程序在哪里崩溃。 |
| `x / F ADDR` | 以 **F** 字母指定的格式检查地址 **ADDR** 处内存位置的内容，其中 F 可以是 o (八进制)、x (十六进制)、d (十进制)、u (无符号十进制)、t (二进制)、f (浮点数)、a (地址)、i (指令)、c (字符) 或 s (字符串)。你可以在格式字母后附加一个表示数据类型大小的字母。大小字母为 b (字节)、h (半字，2 字节)、w (字，4 字节) 和 g (巨型字，8 字节)。通常，**ADDR** 是变量或指针的名称。 |

####### 使用 gdb 查找错误

为了理解如何使用 gdb 查找错误，你需要查看一个示例。使用简单的例子来说明这个过程最容易，因此我从一个相当人为构造的包含典型错误的程序开始。

以下是该人为构造的程序，我将其保存在文件 `dbg tst.c` 中：

```c
#include <stdio.h>
static char buf[256];
void read_input (char *s);
int main(void)
{
  char *input = NULL; /* Just a pointer, no storage for string */
  read_input (input);
  /* Process command. */
  printf( "You typed: %s\n", input);
  /* ... */
  return 0;
}
void read_input (char *s)
{
  printf ("Command: ");
  gets (s);
}
```

此程序的 main 函数调用 read_input 函数以从用户获取一行输入。read_input 函数期望一个字符数组，在其中返回用户输入的内容。然而，在此示例中，main 调用 read_input 时使用的是一个未初始化的指针——这就是这个简单程序中的错误。

使用 gcc 并带有 -g 选项来构建程序：

```
gcc -g -o dbg tst dbg tst.c
```

忽略关于 gets 函数危险的警告信息；我试图利用该函数的缺点来展示如何使用 gdb 追踪错误。

要查看此程序的问题，请运行它并在 **Command** 提示符处输入 **test**：

```
./dbg tst
Command: test
Segmentation fault
```

程序在显示 **Segmentation fault** 消息后终止。对于这个非常小的程序，你通过检查源代码可能就能找到原因。然而，在实际应用中，你可能不会立即知道导致错误的原因。这时你必须使用 **gdb** 来找出问题的根源。

要使用 **gdb** 定位错误，请遵循以下步骤：

- 1. **在 gdb 中加载程序。要在 gdb 中加载名为 `dbgtst` 的程序，请输入以下内容：**
  
  ```
  gdb dbgtst
  ```

- 2. **通过输入 `run` 命令在 gdb 下开始执行程序。当程序提示输入时，输入一些文本。**
  
  程序如前一样失败。以下是 `dbgtst` 程序发生的情况：

  ```
  (gdb) run
  Starting program: /home/naba/sdewd/dbgtst
  Command: test

  Program received signal SIGSEGV, Segmentation fault.
  0x400802b6 in gets () from /lib/tls/libc.so.6
  (gdb)
  ```

- 3. **使用 `where` 命令确定程序在哪里死亡。**
  
  对于 `dbgtst` 程序，该命令产生以下输出：

  ```
  (gdb) where
  #0  0x400802b6 in gets () from /lib/tls/libc.so.6
  #1  0x08048474 in read_input (s=0x0) at dbgtst.c:16
  #2  0x08048436 in main () at dbgtst.c:7
  (gdb)
  ```

  输出显示了函数调用序列。函数调用 **#0** —— 最近的一次 —— 是调用 C 库函数 `gets`。`gets` 调用源自 `read_input` 函数（在文件 `dbgtst.c` 的第 16 行），而后者又被 `dbgtst.c` 文件第 7 行的 main 函数调用。

- 4. **使用 `list` 命令检查可疑源代码的行。**
  
  在 `dbgtst` 中，你可以从 `dbgtst.c` 文件的第 16 行开始，如下所示：

  ```
  (gdb) list dbgtst.c:16
     11      return 0;
     12    }
     13    void read_input(char *s)
     14    {
     15      printf("Command: ");
     16      gets(s);
     17    }
     18
  (gdb)
  ```

查看此列表后，你可以看出问题可能是 `read_input` 的调用方式。然后你列出 `dbgst.c` 中第 7 行周围的代码（`read_input` 调用的来源）：

```
(gdb) list dbgst.c:7
2         static char buf[256];
3         void read_input(char *s);
4         int main(void)
5        {
6            char *input = NULL; /* Just a pointer, no
          storage for string */
7            read_input(input);
8            /* Process command. */
9            printf("You typed: %s\n", input);
10           /* .... */
11           return 0;
(gdb)
```

此时，你可以将问题缩小到名为 `input` 的变量。该变量是一个数组，而不是一个 NULL（即零）指针。

####### 在 gdb 中修复错误

有时你可以直接在 `gdb` 中修复错误。对于前一部分中的示例程序，你可以尝试在程序显示错误消息后死亡后立即应用此修复。由于该示例是人为构造的，我在 `dbgst` 程序中定义了一个额外的名为 `buf` 的缓冲区，如下所示：

`static char buf[256];`

我可以通过将变量 `input` 设置为 `buf` 来修复未初始化指针的问题。以下与 `gdb` 的会话纠正了未初始化指针的问题。（此示例紧随程序运行并因段错误而死亡之后。）

```
(gdb) file dbgst
A program is being debugged already.  Kill it? (y or n) y
Load new symbol table from "/home/naba/sw/dbgst"? (y or n) y
Reading symbols from /home/naba/sw/dbgst...done.
(gdb) list
1          #include <stdio.h>
2          static char buf[256];
3          void read_input(char *s);
4          int main(void)
5         {
6            char *input = NULL; /* Just a pointer, no
          storage for string */
7            read_input(input);
8            /* Process command. */
```





9           printf("You typed: %s\n", input);
10         /***/
(gdb) break 7
断点 2 位于 0x804842b: 文件 dbgtest.c, 第 7 行。
(gdb) run
正在启动程序：/home/naba/sw/dbgtest
断点 1，main () at dbgtest.c:7
7           set var input=buf read_input(input);
(gdb) cont
继续运行。
命令：test
你输入了：test
程序正常退出。
(gdb) q

正如上述代码清单所示，如果我在调用 read_input 之前暂停程序，并将名为 input 的变量设置为 buf（这是一个有效的字符数组），程序的其余部分都能正常运行。

在 gdb 中找到有效的修复方法后，你可以对源文件进行必要的更改，使修复方案永久生效。

###### 理解 GNU 许可证的影响

享受 Linux 带来的丰富成果需要付出代价——为了保护开发者和用户，Linux 基于 GNU GPL（通用公共许可证）分发，该许可证规定了源代码的分发要求。

不过，GPL 并不意味着你不能为 Linux 编写只以二进制形式分发（无论是免费还是收费）的商业软件。你可以遵守所有规则，仍然以二进制形式销售你的 Linux 应用程序。

在编写 Linux 应用程序时，请务必注意两种许可证：

- GNU 通用公共许可证（GPL），它管辖许多 Linux 程序，包括 Linux 内核和 GCC
- GNU 库通用公共许可证（LGPL），它涵盖许多 Linux 库

以下章节概述了这些许可证，并提出了满足其要求的一些建议。然而，由于我不是律师，请勿将本书中的任何内容视为法律建议。这些许可证的全文位于你 Linux 系统中的文本文件中；请将这些许可证展示给你的法律顾问，以便获得完整的解释以及对其在商业中适用性的评估。

### GNU 通用公共许可证

GNU 通用公共许可证（GPL）的文本位于名为 **COPYING** 的文件中，该文件分布在 Linux 系统的各个目录中。例如，输入以下命令可以在你的 Linux 系统中找到该文件的一个副本：

```
find /usr -name "COPYING" -print
```

找到该文件后，你可以切换到该目录并输入 **more COPYING** 来阅读 GPL。如果找不到 **COPYING** 文件，可以翻阅本书末尾阅读 GPL。

GPL 与软件是收费还是免费分发无关；其核心是确保软件对所有用户保持自由。GPL 要求软件以源代码形式分发，并规定任何用户都可以将软件的源代码形式复制并分发给其他人。此外，该许可证提醒所有人，软件绝对没有任何保修。

GPL 涵盖的软件不属于公有领域。受 GPL 保护的软件始终受版权保护，而 GPL 明确规定了软件复制和分发的限制。从用户的角度来看，GPL 的限制实际上并非真正的限制；这些限制实际上是好处，因为用户保证可以获得源代码。

如果你的应用程序使用了 GPL 涵盖的任何软件的部分，你的应用程序将被视为*衍生作品*，这意味着你的应用程序也受 GPL 覆盖，你必须分发你应用程序的源代码。

![](img/11709a8f88c8cd03868a929dc94c0e2b_721_0.png)

虽然 GPL 涵盖 Linux 内核，但 GPL 并不涵盖那些通过系统调用使用内核服务的应用程序。这些应用程序被视为对内核的正常用途。

如果你计划以二进制形式分发你的应用程序（大多数商业软件都是这样分发的），你必须确保你的应用程序没有使用 GPL 涵盖的任何软件的部分。当应用程序调用库中的函数时，可能会使用其他软件的部分。然而，大多数库受另一种 GNU 许可证覆盖，我将在下一节中介绍。

你只需要留意少数 GPL 涵盖的库和实用程序。GNU **dbm**（**gdbm**）数据库库是 GPL 涵盖的著名库之一。GNU **bison** 解析器生成工具是另一个 GPL 涵盖的实用程序。如果你允许 **bison** 生成代码，那么该代码也受 GPL 覆盖。

GNU dbm 和 GNU bison 的其他替代方案不受 GPL 覆盖。对于数据库库，你可以使用 Berkeley 数据库库 db 来代替 gdbm。对于解析器生成器，你可以使用 yacc 来代替 bison。

####### GNU 较通用公共许可证

GNU 较通用公共许可证（LGPL）的文本位于名为 COPYING.LIB 的文件中。如果你安装了内核源代码，COPYING.LIB 文件的一个副本位于其中一个源目录中。要在你的 Linux 系统中定位 COPYING.LIB 文件的一个副本，请在终端窗口中输入以下命令：

```
find /usr -name "COPYING*" -print
```

该命令列出系统中所有 COPYING 和 COPYING.LIB 的出现位置。COPYING 文件包含 GPL，而 COPYING.LIB 包含 LGPL。

LGPL 旨在允许在你的应用程序中使用库，即使你不分发你应用程序的源代码。然而，LGPL 规定，用户必须能够访问你所使用库的源代码，并且用户可以使用这些库的修改版本。

LGPL 涵盖大多数 Linux 库，包括 C 库（lib c.a）。因此，当你使用 GCC 编译器在 Linux 上构建应用程序时，你的应用程序会链接到 LGPL 涵盖的一个或多个库的代码。如果你只想以二进制形式分发你的应用程序，你需要关注 LGPL。

满足 LGPL 意图的一种方法是提供你应用程序的目标代码以及一个将你的目标文件与 LGPL 涵盖的任何更新的 Linux 库进行链接的 makefile。

满足 LGPL 的更好方式是使用动态链接，在这种方式下，你的应用程序和库是独立的实体，尽管你的应用程序在运行时调用库中的函数。通过动态链接，用户可以立即受益于库的任何更新，而无需重新链接应用程序。

##### 第 2 章：使用 C 语言编程

###### 本章内容

- 理解 C 语言编程的基础知识
- 发现 C 编程语言的特性
- 清点标准 C 库
- 在 Linux 应用程序中使用共享库

C 编程语言的组成——一个稀疏的核心加上一个庞大的支持库——使其成为开发软件的理想语言。核心提供了良好的数据类型和控制结构选择，而所有附加任务，包括输入和输出（I/O）、数学计算以及访问外围设备，都交给函数库处理。基本上，C 允许你访问系统中的任何内容。这意味着你可以用 C 编写任何东西，从设备驱动程序到图形应用程序。在本章中，我将介绍 C 语言编程。我还会简要解释共享库的重要性，以及如何使用 C 编程语言在 Linux 中创建一个共享库。

###### C 程序的结构

典型的 C 程序组织为一个或多个源文件，即模块。（参见图 2-1。）每个文件具有类似的结构，包含注释、预处理器指令、变量和函数的声明以及它们的定义。通常，你将每组相关的变量和函数放在单个源文件中。

有些文件仅仅是一组声明，通过 C 预处理器的 #include 指令在其他文件中使用。这些文件通常被称为*头文件*，名称以 .h 扩展名结尾。在图 2-1 中，文件 *shapes.h* 是一个头文件，声明了程序的公共数据结构和函数。另一个文件，*shapes.c*，定义了函数。第三个文件，*shapetest.c*，实现了 main 函数——C 程序的执行从该函数开始。这些名称以 .c 结尾的文件是源文件，你在那里定义程序所需的函数。尽管图 2-1 只显示每个源文件中的一个函数，但在典型的程序中，一个源文件通常包含许多函数。




## 700 C 程序的结构

```c
/* File: shapes.h */
/* Header file for data structures */

#ifndef _SHAPES_H
#define _SHAPES_H

enum shape_type {T_CIRCLE, T_RECTANGLE};

typedef struct RECTANGLE
{
    double x1, y1, x2, y2;
} RECTANGLE;

typedef struct CIRCLE
{
    double xc, yc, radius;
} CIRCLE;

typedef struct SHAPE
{
    enum shape_type type;
    union
    {
        RECTANGLE r;
        CIRCLE c;
    } u;
} SHAPE;

/* Function prototypes */
double compute_area(SHAPE *p_s);

#endif
```

```c
/* File: shapes.c */
/* Function that computes area of shapes */

#include <math.h>
#include "shapes.h"

double compute_area(SHAPE *p_s)
{
    switch(p_s->type)
    {
        case T_CIRCLE:
        {
            CIRCLE *p_c = &p_s->u.c;
            return M_PI * p_c->radius * p_c->radius;
        }
        case T_RECTANGLE:
        {
            RECTANGLE *p_r = &p_s->u.r;
            return fabs (p_r->x2 - p_r->x1) *
                   fabs(p_r->y2 - p_r->y1);
        }
    }
    return 0.0;
}
```

**图 2-1：** 通常，由多个源文件组成一个 C 程序。

```c
/* File: shapetest.c */
/* Main program to test shapes.c */

#include <stdio.h>
#include "shapes.h"

int main(void)
{
    SHAPE s;
    CIRCLE *p_c = &s.u.c;
    s.type = T_CIRCLE;
    p_c->radius = 50.0;
    p_c->xc = p_c->yc = 100.0;
    printf("Area of circle = %f\n",
           compute_area(&s));
    return 0;
}
```

###### 声明与定义

*声明*决定了程序如何解释一个*符号*。另一方面，*定义*实际上创建了一个变量或函数。定义会促使编译器为数据或代码保留存储空间，但声明不会。例如，

```c
int x, y, z;
```

这是三个不同整数变量的定义，但

```c
extern int x, y, z;
```

是一个声明，表明这三个整数变量在另一个源文件中定义。

为了创建可执行程序，必须编译和链接源文件。从 C 源文件构建程序的具体步骤取决于编译器和操作系统。例如，在 Linux 中，您可以使用以下命令编译和链接图 2-1 中显示的文件：

```bash
gcc -o shapetest shapetest.c shapes.c
```

此命令创建一个名为 *shapetest* 的可执行文件。然后您可以使用以下命令运行该文件：

```bash
./shapetest
```

以下是该程序显示的输出：

```text
Area of circle = 7853.981634
```

在每个源文件中，程序的组成部分都以标准方式排列。如图 2-1 所示，C 源文件的典型组成部分在屏幕上向下滚动时遵循一定的顺序：

1.  文件以一些注释开头，描述模块的目的并提供其他相关信息，例如作者姓名和修订日期。在 C 语言中，注释以 `/*` 开头，以 `*/` 结束。
2.  预处理器的命令，称为*预处理器指令*，紧随注释之后。前几个指令通常用于包含头文件和定义常量。
3.  接下来是在整个文件中可见的变量和函数的声明。换句话说，这些变量和函数的名称可以在该文件中的任何函数中使用。在此处，您还定义在文件内部所需的变量。
4.  文件的其余部分包括函数的定义。在函数体内部，您可以定义局部于该函数的变量，这些变量仅在函数代码执行期间存在。

###### 预处理器指令

预处理是指将 C 文件转换为机器指令或编译的第一步。预处理器处理源文件并对嵌入在程序中的某些命令（称为*预处理器指令*）进行操作。这些指令以井号（`#`）开头，后跟一个关键字。通常，编译器在开始编译之前会自动调用预处理器，但大多数编译器都提供单独调用预处理器的选项。您可以利用预处理器的三个主要功能使您的程序模块化、更易于阅读并更易于定制：

- 您可以使用 `#include` 指令将文件内容插入到您的程序中。通过这个指令，您可以在一个位置放置常见的声明，并通过文件包含在所有源文件中使用它们。结果是降低了不同程序模块中变量和函数声明之间不匹配的风险。
- 通过 `#define` 指令，您可以定义宏，使您能够用一个字符串替换另一个字符串。您可以使用 `#define` 指令为数值常量赋予有意义的名称，从而提高源文件的可读性。
- 通过使用诸如 `#if`、`#ifdef`、`#else` 和 `#endif` 等指令，您可以只编译程序的选定部分。您可以使用此功能来编写包含两个或多个系统代码的源文件，但只编译适用于您正在编译程序的计算机系统的那些部分。使用这种策略，您可以使用一组源文件维护程序的多个版本。

####### 包含文件

通过利用 `#include` 指令，您可以编写模块化程序。之所以能够使用此指令，是因为 C 预处理器允许您将常用声明保存在单个文件中，并根据需要将其插入其他源文件。ANSI C 支持 `#include` 指令的三种形式。作为 C 程序员，您需要熟悉前两种形式：

```c
#include <stdio.h>
#include "shapes.h"
```

使用第一种形式的 `#include` 来读取文件内容——在这种情况下，是从默认位置（所有头文件所在处）读取标准 C 头文件 `stdio.h`。当文件（例如 `shapes.h`）位于当前目录中时，请将文件名放在双引号内。查找被包含文件的确切约定取决于编译器。

####### 定义宏

*宏*本质上是一个可重用 C 代码块的短名称。代码可以简单到是一个数值常量，也可以复杂到包含许多行详细的 C 代码。其思想是，在定义宏之后，您可以在程序中使用该代码的任何地方使用该宏。当源文件被预处理时，宏名称的每次出现都会被其定义所替换。

宏的一个常见用途是为数值常量定义一个符号名称，然后在程序中使用该符号代替数字。宏提高了源代码的可读性；通过描述性名称，您不需要猜测为什么在程序中使用特定的数字。您可以使用 `#define` 指令以简单的方式定义此类宏。以下是一些示例：

```c
#define PI        3.14159
#define GRAV_ACC  9.80665
#define BUFSIZE   512
```

定义这些符号后，您可以在整个源文件中使用 PI、GRAV_ACC 和 BUFSIZE 代替数值常量。

然而，宏的功能远不止于简单地用符号替换常量或某些代码块。宏可以接受参数，并在宏在程序中被使用时，将该参数的每次出现替换为提供的值。因此，宏展开产生的代码可能会根据您运行宏时使用的参数而变化。例如，这里有一个接受参数并展开为旨在计算参数平方的表达式的宏：

```c
#define square(x) ((x) * (x))
```

如果在程序中使用 `square(z)`，在源文件被预处理后，它会变成 `((z) * (z))`。实际上，这个宏等同于一个计算其参数平方的函数——只是你并不调用函数。相反，由宏生成的表达式直接放置在源文件中。

####### 条件指令

您可以使用条件指令，例如 `if`、`ifdef`、`ifndef`、`else`、`elif` 和 `endif`，来控制源文件的哪些部分被编译以及在何种条件下被编译。通过此功能，您维护一组源文件，可以选择使用不同的编译器和在不同环境中进行编译。（另一种常见用途是插入用于调试的 `printf` 语句，这些语句只有在定义了名为 DEBUG 的符号时才会被编译。）条件指令以 `if`、`ifdef` 或 `ifndef` 开头——后面可以跟随任意数量的 `elif` 指令（或者根本不跟随）。接下来是可选的 `else`，最后是一个标记该条件块结束的 `endif` 指令。以下是使用条件指令的一些常见方式。

为了只包含一次头文件，您可以使用以下代码：

```c
#ifndef __PROJECT_H
#define __PROJECT_H
/* Declarations to be included once */
/* ... */
#endif
```




以下代码在调试期间（当定义了符号 DEBUG 时）会打印一条诊断消息：

```c
#ifdef DEBUG
    printf("In read_file: bytes_read = %d\n", bytes_read);
#endif
```

以下示例展示了如何根据正在编译该程序的计算机系统类型，包含不同的头文件。若要选择性地包含头文件，你可以使用以下方法：

```c
#if CPU_TYPE == I386
    #include <i386/sysdef.h>
#elif CPU_TYPE == M68K
    #include <m68k/sysdef.h>
#else
    #error Unknown CPU type.
#endif
```

`#error` 指令用于在预处理期间显示错误消息。

###### 其他指令

其他几种预处理器指令执行一些杂项任务。例如，你可以使用 `#undef` 指令来移除符号的当前定义。`#pragma` 指令是另一种特殊用途指令，可用于向 C 编译器传达信息。你可以使用 `#pragma` 来访问编译器的特殊功能——这些功能因编译器而异。

C 编译器提供了若干预定义宏（参见表 2-1）。其中，宏 `__FILE__` 和 `__LINE__` 分别指代当前正在处理的源文件名和当前行号。你可以使用 `#line` 指令来更改这些值。例如，要将 `__FILE__` 设置为 "file_io.c"，并将 `__LINE__` 设置为 100，你可以这样写：

```c
#line 100 "file_io.c"
```

####### 表 2-1 C 中的预定义宏

| 宏 | 定义 |
| :--- | :--- |
| `__DATE__` | 此字符串包含你调用 C 编译器时的日期。其格式为 MMM DD YYYY（例如，Oct 26 2004）。 |
| `__FILE__` | 此宏展开为一个包含源文件名的字符串。 |
| `__LINE__` | 此宏是一个十进制整数，其值等于当前源文件中的行号。 |
| `__STDC__` | 此宏展开为十进制常量 1，表示 C 编译器符合 ANSI 标准。 |
| `__TIME__` | 此字符串显示你开始编译源文件的时间。其格式为 `HH:MM:SS`（例如，`21:59:45`）。 |

###### 变量的声明与定义

在 C 语言中，在使用所有变量和函数之前，必须对其定义或声明。变量的定义指定了三件事：

- 其**可见性**，指示变量确切的使用范围。（它是为程序中的所有文件定义的，还是仅为当前文件定义，或仅在某个函数内定义？）
- 其*生命周期*，决定变量是临时存在的（例如，函数中的局部变量）还是永久存在的（只要程序在运行）。
- 其**类型**（在某些情况下，还包括其*初始值*）。例如，初始化为 1 的整型变量 x 的定义方式如下：

```c
int x = 1;
```

如果你要使用在其他源文件中定义的变量，你需要使用 `extern` 关键字来声明该变量，如下所示：

```c
extern int message_count;
```

你必须在至少一个源文件中不带 `extern` 限定符定义此变量。当程序构建时，链接器将解析对 `message_count` 变量的所有引用，并确保它们都使用同一个变量。

###### 基本数据类型

C 语言有四种基本数据类型：`char` 和 `int` 用于存储字符和整数，而 `float` 和 `double` 用于存储浮点数。你可以用简单的方式为这些基本数据类型定义变量：

```c
char c;
int i, j, bufsize;
float volts;
double mean, variance;
```

通过使用 `long`、`short` 和 `unsigned` 限定符作为前缀，你可以将基本数据类型扩展为一个更大的集合。`long` 和 `short` 限定符是大小修饰符。例如，`long int` 至少为 4 字节长，而 `short int` 的最小尺寸仅为 2 字节。`int` 的大小取决于系统，但它肯定至少与 `short` 一样大。

`unsigned` 限定符仅保留给 `int` 和 `char` 类型。通常，这些类型的每一种既包含负值也包含正值。这是这些数据类型的默认有符号形式。当你希望变量仅保存正值时，可以使用 `unsigned` 限定符。以下是使用 `short`、`long` 和 `unsigned` 限定符的一些示例：

```c
unsigned char mode_select, printer_status;
short record_number;                 /* Same as 'short int'      */
long  offset;                        /* Same as 'long int'       */
unsigned   i, j, msg_id;            /* Same as 'unsigned int'   */
unsigned short width, height;        /* Same as 'unsigned short int' */
unsigned long file_pos;             /* Same as 'unsigned long int'   */
long double result;
```

当与 `int` 类型一起使用 `short`、`long` 和 `unsigned` 限定符时，你可以省略声明中的 `int`。你还可以使用 `long` 前缀来扩展 `double` 数据类型。

GCC 附带预定义头文件 `limits.h` 和 `float.h`，其中定义了各种数据类型的确切尺寸——以及这些文件中的数值范围。你可以在 Linux 系统的 `/usr/include` 目录中查看这些文件，以确定 GCC 编译器支持的基本数据类型的尺寸。

####### 枚举

你可以使用 `enum` 数据类型来定义自己的枚举列表——一组固定的、有名称的整型常量。例如，你可以使用 `enum` 如下声明一个名为 BOOLEAN 的布尔数据类型：

```c
/* Declare an enumerated type named BOOLEAN */
enum BOOLEAN {false = 0, true = 1, stop = 0, go = 1,
              off = 0, on = 1};
/* Define a BOOLEAN called “status” and initialize it */
enum BOOLEAN status = stop;
```

此示例首先将 BOOLEAN 声明为枚举类型。大括号内的列表展示了 `enum BOOLEAN` 变量的有效值的枚举常量。你可以将每个常量初始化为任意值，并且多个常量可以使用相同的值。在此示例中，常量 `false`、`stop` 和 `off` 被设置为 0，而 `true`、`go` 和 `on` 被初始化为 1。该示例还定义了一个名为 `status` 的枚举 BOOLEAN 变量，最初设置为常量 `stop`。

###### 结构体、联合体和位域

使用 **struct** 将相关的数据项组合在一起，并通过名称引用该组。例如，定义一个用于持有队列变量的结构体声明可能如下所示：

```c
/* Declare a structure */
struct QUEUE
{
    int  count;      /* Number of items in queue   */
    int  front;      /* Index of first item in queue */
    int  rear;       /* Index of last item in queue  */
    int  elemsize;   /* Size of each element of data */
    int  maxsize;    /* Maximum capacity of queue    */
    char *data;      /* Pointer to queued data       */
};
/* Define two queues */
struct QUEUE rcv_q, xmit_q;
```

QUEUE 结构体内部的元素称为其*成员*。你可以使用成员选择运算符（`.`）来访问这些成员。例如，**rcv_q.count** 引用 **rcv_q** 结构体中的 `count` 成员。

联合体（union）类似于结构体，但联合体不会像 **struct** 那样将相关数据项组合在一起，而是为从同一位置开始的多个数据项分配存储空间。因此，联合体的所有成员共享同一存储空间。你可以使用联合体以不同的方式查看同一数据项。假设你使用的编译器支持 4 字节的 **int** 数字，你想访问单个 **long** 整数的 4 个独立字节。以下是一个实现该功能的联合体：

```c
union
{
   long  file_type;
   char  bytes[4];
}  header_id;
```

在此定义中，**header_id.file_type** 指的是那个 **long** 整数，而 **header_id.bytes[0]** 是该 **long** 整数的第一个字节。

######## 数组

*数组* 是一个或多个相同数据项的集合。你可以声明任何类型的数据数组，包括结构体和由 **typedef** 定义的类型。例如，要定义一个 80 个字符的数组，你可以写下以下内容：

```c
char      string[80];
```





字符串数组中的字符占据连续的存储位置，从位置 0 开始。因此，在这个示例中，*string*[0] 指的是该数组中的第一个字符，而 *string*[79] 指的是最后一个字符。你可以类似地定义其他数据类型和结构的数组：

```
struct Customer          /* Declare a structure   */
{
    int id;
    char first_name[40];
    char last_name[40];
};
struct Customer customers[100]; /* Define array of structures */
int                index[64];   /* An array of 64 integers   */
```

你还可以定义多维数组。例如，要表示一个 80 列 x 25 行的文本显示屏幕，你可以使用如下所示的二维数组：

```
unsigned char text_screen[25][80];
```

*text_screen* 的每个元素都是 80 个 *unsigned char* 组成的数组，而 *text_screen* 包含 25 个这样的数组。换句话说，二维数组在内存中是按行依次排布存储的。你可以使用诸如 *text_screen*[0] [0] 这样的表达式来引用第一行的第一个字符，使用 *text_screen*[24] [79] 来引用显示屏幕最后一行的最后一个字符。更高维度的数组也类似定义：

```
float coords[3][2][5];
```

此示例将 *coords* 定义为包含三个数据项的三维数组：每个项是由两个数组组成的数组，而这两个数组中的每一个又是由五个 *float* 变量组成的数组。因此，你可以将多维数组解释为*数组的数组*。

###### 指针

*指针* 是一种可以存储任何类型数据地址（位域除外）的变量。例如，如果 *p_i* 是指向整型变量的指针，你可以按如下方式定义和使用它：

```
/* Define an int pointer and an integer */
int *p_i, count;
/* Set pointer to the address of the integer "count" */
p_i = &count;
```

在这种情况下，编译器为 *int* 变量 *count* 和一个指向整数的指针 *p_i* 分配存储空间。表示指针所需的字节数取决于底层系统的寻址方案。

不要在指针包含有效对象地址之前使用它。

示例展示了如何使用 `&` 运算符将 `p_i` 初始化为整型变量 count 的地址，该运算符提供变量的地址。`p_i` 初始化后，你可以使用表达式 `*p_i` 来引用 `count` 的值，这读作“`p_i` 中存储的地址所指对象的内容”。

指针在许多情况下很有用；其中一个重要用途是内存的动态分配。标准 C 库包含诸如 `malloc` 和 `calloc` 等函数，你可以调用它们来为对象数组分配存储。在分配内存后，这些函数返回内存块的起始地址。由于该地址是访问该内存的唯一方式，你必须将其存储在能够持有地址的变量中——即指针。

假设你为包含 50 个整数的数组分配了内存，并将返回的地址存储在 `p_i` 中。现在你可以将这块内存视为一个名为 `p_i` 的包含 50 个整数的数组。因此，你可以将数组中的最后一个元素引用为 `p_i[49]`，这等价于 `*(p_i+49)`。类似地，C 将数组名视为指向数组第一个元素的指针。数组名与指针变量的区别在于，数组名是一个常量，不需要显式存储来保存数组第一个元素的地址。另一方面，指针是一个实际的存储位置，能够保存任何数据的地址。

除了存储动态分配内存的地址外，指针还常用作函数的参数。当调用 C 函数时，其所有参数都是按值传递的——也就是说，函数获取的是每个参数的副本，而不是函数调用参数列表中出现的原始变量。因此，C 函数无法改变其参数的值。指针提供了解决方案。要在函数中改变变量的值，你可以传递指向该变量的指针；然后函数可以通过该指针改变值。

###### 结构体、联合体和位域

####### 类型定义

通过 `typedef` 关键字，C 为你提供了一种为现有数据类型赋予新名称的便捷方式。你可以使用 `typedef` 功能为特定应用程序中使用的数据类型赋予有意义的名称。例如，一个图形应用程序可以像下面这样声明一个名为 `Point` 的数据类型：

```c
/* Declare a Point data type */
typedef struct Point
{
    short x;
    short y;
} Point;
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_734_0.png)

```
/* Declare PointPtr to be pointer to Point types */
typedef Point *PointPtr;
/* Define some instances of these types
 * and initialize them */
Point      a = {0, 0};
PointPtr   p_a = &a;
```

正如 `Point` 和 `PointPtr` 类型所示，你可以使用 `typedef` 方便地声明复杂的数据类型。

####### 类型限定符：const 和 volatile

两个类型限定符 `const` 和 `volatile` 在声明中工作方式如下：

- 声明中的 `const` 限定符告诉编译器程序必须不修改特定的数据对象。编译器不得生成可能改变存储该数据项位置内容的代码。
- `volatile` 限定符指定超出程序控制范围的因素可能会改变变量的值。

你可以在单个数据项上使用 `const` 和 `volatile` 关键字，这意味着虽然你的程序必须不修改该项，但其他进程可能会修改它。`const` 和 `volatile` 关键字总是修饰紧随其后（右侧）的项目。`const` 和 `volatile` 限定符提供的信息旨在帮助编译器优化其生成的代码。例如，假设变量 `block_size` 按以下方式声明并初始化：

```
const int block_size = 512;
```

在这种情况下，编译器不需要生成代码从内存加载 `block_size` 的值。相反，它可以在程序中任何使用 `block_size` 的地方使用值 512。现在假设你在声明中添加了 `volatile`，并将声明更改为：

```
volatile const int block_size = 512;
```

此声明表示某些外部进程可以更改 `block_size` 的内容。因此，编译器不能优化掉任何对 `block_size` 的引用。当你引用 I/O 端口或视频内存时，可能需要使用此类声明，因为这些位置可能受到超出程序控制范围的因素的影响而改变。

### 表达式

*表达式* 是变量、函数调用和运算符的组合，其结果为一个单一的值。例如，这里有一个表达式，其值存储 *null-terminated string*（以空字符结尾的字符串）`str` 所需的字节数（即末尾有一个零字节的 char 数据类型数组）：

```
(strlen(str) * sizeof(char) + 1)
```

此表达式涉及函数调用—— `strlen(str)` ——以及乘法 (*)、加法 (+) 和 `sizeof` 运算符。

C 拥有大量运算符，它们是表达式的重要组成部分。表 2-2 总结了 C 中的运算符。

**表 2-2 C 运算符摘要**

| 运算符名称 | 语法 | 结果 |
| :--- | :--- | :--- |
| **算术运算符** | | |
| 加法 | x+y | 将 x 和 y 相加 |
| 减法 | x-y | 从 x 中减去 y |
| 乘法 | x*y | 将 x 和 y 相乘 |
| 除法 | x/y | 将 x 除以 y |
| 取余 | x%y | 计算 x 除以 y 所得的余数 |
| 前置自增 | ++x | 在使用 x 之前自增 |
| 后置自增 | x++ | 在使用 x 之后自增 |
| 前置自减 | --x | 在使用 x 之前自减 |
| 后置自减 | x-- | 在使用 x 之后自减 |
| 取负 | -x | 取 x 的值的负值 |
| 取正 | +x | 保持 x 的值不变 |
| **关系和逻辑运算符** | | |
| 大于 | x>y | 如果 x 大于 y，则值为 1；否则，值为 0。 |
| 大于或等于 | x>=y | 如果 x 大于或等于 y，则值为 1；否则，值为 0。 |
| 小于 | x<y | 如果 y 大于 x，则值为 1；否则，值为 0。 |
| 小于或等于 | x<=y | 如果 y 大于或等于 x，则值为 1；否则，值为 0。 |

（接下页）

**表达式** 711

**第八卷**
第 2 章

**C 语言编程**





### 表达式

| **运算符名称** | **语法** | **结果** |
| :--- | :--- | :--- |
| **关系运算符和逻辑运算符** | | |
| 等于 | `x == y` | 如果 x 等于 y，值为 1；否则，值为 0。 |
| 不等于 | `x != y` | 如果 x 和 y 不相等，值为 1；否则，值为 0。 |
| 逻辑非 | `!x` | 如果 x 为 0，值为 1；否则，值为 0。 |
| 逻辑与 | `x && y` | 如果 x 或 y 中有一个为 0，值为 0。 |
| 逻辑或 | `x \|\| y` | 如果 x 和 y 都为 0，值为 0。 |
| **赋值运算符** | | |
| 赋值 | `x = y` | 将 y 的值放入 x 中 |
| 复合赋值 | `x op = y` | 等同于 `x = x op y`，其中 `op` 是以下运算符之一：`+`、`-`、`*`、`/`、`%`、`<`、`>`、`&`、`^` 或 `\|` |
| **数据访问和大小运算符** | | |
| 下标 | `x[y]` | 选择数组 x 的第 y 个元素 |
| 成员选择 | `x.y` | 选择结构体（或联合体）x 的成员 y |
| 成员选择 | `x->y` | 从以 x 为地址的结构体或联合体中选择名为 y 的成员 |
| 解引用 | `*x` | 以 x 为地址的内存位置的内容 |
| 取地址 | `&x` | 名为 x 的数据对象的地址 |
| 大小 | `sizeof(x)` | 名为 x 的数据对象的大小（以字节为单位） |
| **位运算符** | | |
| 位非 | `~x` | 将所有 1 变为 0，所有 0 变为 1 |
| 位与 | `x & y` | 结果是 x 和 y 的按位与。 |
| 位或 | `x \| y` | 结果是 x 和 y 的按位或。 |
| 位异或 | `x ^ y` | 结果在 x 和 y 对应位不同的位置包含 1。 |
| 左移 | `x << y` | 将 x 的位向左移动 y 个位位置。在腾出的位位置填充 0。 |
| 右移 | `x >> y` | 将 x 的位向右移动 y 个位位置。在腾出的位位置填充 0。 |
| **其他运算符** | | |
| 函数调用 | `x(y)` | 结果是由函数 x 返回的值（如果有），该函数以参数 y 调用。 |
| 类型转换 | `(type) x` | 将 x 的值转换为括号中指定的类型 |
| 条件运算符 | `z ? x : y` | 如果 z 不为 0，则计算 x；否则，计算 y |
| 逗号 | `x, y` | 先计算 x，然后计算 y |

####### 运算符优先级

典型的 C 表达式由几个操作数和运算符组成。在编写复杂表达式时，你必须了解编译器评估运算符的顺序。例如，假设一个程序使用一个指向整数的指针数组，定义如下：

```c
typedef int *IntPtr; // 使用 typedef 简化声明
IntPtr iptr[10]; /* 一个包含 10 个指向 int 的指针的数组 */
```

现在假设你遇到表达式 `*iptr[4]`。它是指向存储在 `iptr[4]` 地址中的 int 的值，还是指位于 `iptr` 地址处的第五个元素？你真正需要了解的是，编译器是先评估下标运算符 `[]` 还是先评估解引用运算符 `*` —— 或者相反？要回答这类问题，你需要了解优先级 —— 即程序应用运算符的顺序。

表 2-3 总结了 C 的优先级规则。该表按优先级递减的顺序列出运算符。最高优先级的运算符 —— 首先应用的 —— 列在前面。该表还显示了*结合性* —— 即同一级别运算符的评估顺序。

######## 表 2-3 C 运算符的优先级和结合性

| 运算符组 | 运算符名称 | 符号 | 结合性 |
| :--- | :--- | :--- | :--- |
| 后置 | 下标 | `x [ y ]` | 从左到右 |
| | 函数调用 | `x ( y )` | |
| | 成员选择 | `x . y` | |
| | 成员选择 | `x -> y` | |
| 一元 | 后置递增 | `x ++` | 从右到左 |
| | 后置递减 | `x --` | |
| | 前置递增 | `++ x` | |
| | 前置递减 | `-- x` | |
| | 取地址 | `& x` | |
| | 解引用 | `* x` | |
| | 加 | `+ x` | |
| | 减 | `- x` | |
| | 位非 | `~ x` | |
| | 逻辑非 | `! x` | |
| | sizeof | `sizeof x` | |
| | 类型转换 | `( type ) x` | |
| 乘法 | 乘 | `x * y` | 从左到右 |
| | 除 | `x / y` | |
| | 取模 | `x % y` | |
| 加法 | 加 | `x + y` | 从左到右 |
| | 减 | `x - y` | |
| 移位 | 左移 | `x << y` | 从左到右 |
| | 右移 | `x >> y` | |
| 关系 | 大于 | `x > y` | 从左到右 |
| | 大于或等于 | `x >= y` | |
| | 小于 | `x < y` | |
| | 小于或等于 | `x <= y` | |
| 相等 | 等于 | `x == y` | 从左到右 |
| | 不等于 | `x != y` | |
| 位运算 | 位与 | `x & y` | 从左到右 |
| | 位异或 | `x ^ y` | |
| | 位或 | `x \| y` | |
| 逻辑 | 逻辑与 | `x && y` | 从左到右 |
| | 逻辑或 | `x \|\| y` | |
| 条件 | 条件 | `z ? x : y` | 从右到左 |
| 赋值 | 赋值 | `x = y` | 从右到左 |
| | 乘赋值 | `x *= y` | |
| | 除赋值 | `x /= y` | |
| | 取模赋值 | `x %= y` | |
| | 加赋值 | `x += y` | |
| | 减赋值 | `x -= y` | |
| | 左移赋值 | `x <<= y` | |
| | 右移赋值 | `x >>= y` | |
| | 位与赋值 | `x &= y` | |
| | 位异或赋值 | `x ^= y` | |
| | 位或赋值 | `x \|= y` | |
| 逗号 | 逗号 | `x , y` | 从左到右 |

回到解释 `*iptr[4]` 的问题，快速查看表 2-3 会告诉你 `[]` 运算符的优先级高于 `*` 运算符。因此，当编译器处理表达式 `*iptr[4]` 时，它首先评估 `iptr[4]`，然后应用*解引用*运算符，得到存储在 `iptr[4]` 地址中的 *int* 值。

###### 语句

你使用语句来表示 C 函数执行的操作，并控制 C 程序中的执行流程。语句由关键字、表达式和其他语句组成。每个语句以分号（`;`）结尾。

一种特殊类型的语句 —— *复合语句* —— 是一对花括号（`{...}`）包围的一组语句。函数体是一个复合语句。这样的复合语句（也称为*代码块*）可以包含局部变量。

在以下按字母顺序排列的小节中 —— 我简要描述了 C 中可用的语句类型。

####### break 语句

你使用 `break` 语句跳转到最内层 `do`、`for`、`switch` 或 `while` 语句之后的语句。它也用于从 `switch` 语句中退出。这是一个使用 `break` 从 `for` 循环中退出的示例：

```c
for (i = 0; i < ncommands; i++)
{
    if (strcmp(input, commands[i]) == 0) break;
}
```

####### case 语句

case 语句在 switch 语句中标记标签。这是一个示例。（此处 interrupt_id 是一个整数变量。）

```c
switch (interrupt_id)
{
    case XMUT_RDY:
        transmit();
        break;
    case RCV_RDY:
        receive();
        break;
}
```

####### 复合语句或代码块

复合语句或代码块是由声明后跟语句的一组内容，全部包裹在一对花括号 `{...}` 中。典型的复合语句包括函数体和 if 语句后的代码块。在以下示例中，花括号内出现的所有内容 —— 声明和语句 —— 构成了一个复合语句：

```c
if (theEvent.expose.count == 0)
{
    int i;
    /* 清除窗口并绘制 "figures" 数组中的图形
     */
    XClearWindow (theDisplay, dWin);
    if (numfigures > 0)
        for (i = 0; i < numfigures; i++)
            draw_figure (theDisplay, dWin, theGC, i);
}
```

####### continue 语句

continue 语句开始其所在的最内层 do、for 或 while 语句的下一次迭代。当你想要跳过循环的执行时，可以使用 continue。例如，为了对 1 到 10 的数字求和（排除 5），你可以使用一个 for 循环，当循环索引（i）为 5 时跳过循环体：

```c
for (i = 0, sum = 0; i <= 10; i++)
{
    if (i == 5) continue;  /* 排除 5 */
    sum += i;
}




####### 默认标签

在 `switch` 语句中，使用 *default* 作为标签来标记当没有任何 case 标签匹配 *switch 表达式* 时执行的代码。

####### do 语句

do 语句与 `while` 一起构成迭代循环，其结构如下：

```
do
	statement
	while(*expression*);
```

*statement*（通常是一个复合语句）会一直执行，直到 `while` 语句中的 *expression* 的求值结果为 0。该表达式在每次执行完语句后进行求值——因此，do-while 块 *至少执行一次*。例如，要累加从 1 到 10 的数字，可以使用以下 `do` 语句：

```
sum = 0;
do
{
	sum += i;
	i++;
}
while(i <= 10);
```

####### 表达式语句

表达式语句是为了其副作用而被求值的。表达式语句的一些典型用途包括调用函数、递增变量以及将值赋给变量。以下是一些示例：

```
printf("Hello, World!\n");
i++;
num_bytes = length * sizeof(char);
```

### for 语句

使用 `for` 语句可以执行语句任意次（该次数基于表达式的值）。语法如下：

```
for (*expr_1*; *expr_2*; *expr_3*) statement
```

*expr_1* 在循环开始时求值一次，语句会一直执行，直到表达式 *expr_2* 求值为 0。第三个表达式 *expr_3* 在每次执行完语句后进行求值。这三个表达式都是可选的，如果省略 *expr_2*，则假设其值为 1。以下是一个使用 *for* 循环累加 1 到 10 的示例：

```
for (i = 0, sum = 0; i <= 10; sum += i, i++);
```

在此示例中，实际累加数字的工作是在第三个表达式中完成的，而由 *for* 循环控制的语句是一个 *空* 语句（仅有一个 ;）。

####### goto 语句

*goto* 语句将控制权转移到语句标签处。以下是一个示例，提示用户输入一个值，如果该值不可接受，则重复请求：

```
ReEnter:
printf("Enter offset: ");
scanf(" %d", &offset);
if (offset < 0 || offset > MAX_OFFSET)
{
printf("Bad offset: %d Please reenter:\n", offset);
goto ReEnter;
}
```

####### if 语句

您可以使用 *if* 语句测试表达式，并且仅在表达式不为零时执行语句。*if* 语句具有以下形式：

```
if ( expression ) statement
```

*if* 语句后面的语句仅在括号内的表达式求值为非零值时执行。该语句通常是一个复合语句。以下是一个示例：

```
if (mem_left < threshold)
{
Message("Low on memory! Please close some windows.\n");
}
```

####### if-else 语句

*if-else* 语句是 *if* 语句与 *else* 子句结合的一种形式。该语句的语法如下：

```
if ( expression )
    statement_1
else
    statement_2
```

如果括号内的表达式不为零，则执行 statement_1。否则，执行 statement_2。以下是一个使用 if 和 else 来选取两个变量中较小值的示例：

```
if ( a <= b )
    smaller = a;
else
    smaller = b;
```

####### 空语句

空语句由一个单独的分号表示，它不执行任何操作。当所有处理都在循环表达式中完成，而不是在循环体中完成时，您可以在循环中使用空语句。例如，要定位标记字符串结尾的零字节，可以使用以下代码：

```
char str[80] = "Test";
int i;
for (i=0; str[i] != '\0'; i++)
    ; /* Null statement */
```

####### return 语句

return 语句停止执行当前函数，并将控制权返回给调用函数。语法如下：

```
return expression;
```

其中表达式的值作为函数的值返回。对于不返回值的函数，请按照以下方式使用不带表达式的 return 语句：

```
return;
```

####### switch 语句

switch 语句根据表达式的值执行多重分支。它具有以下语法：

```
switch (expression)
{
    case value1:
        statement_1
        break;

    case value2:
        statement_2
        break;
    ...
    default:
        statement_default
}
```

如果 switch 测试的 *expression* 求值为 value1，则执行 statement_1。如果表达式等于 value2，则执行 statement_2。该值与每个 case 标签进行比较，并执行匹配标签后的语句。如果该值不匹配任何 case 标签，则执行 default 标签后的 *statement_default* 代码块。每个语句以一个 break 语句结束，该语句将一个 case 标签的代码与另一个 case 标签的代码分开。以下是一个 switch 语句，它根据名为 *command* 的整型变量的值调用不同的例程：

```
switch (command)
{
   case 'q':
      quit_app ();
      break;
   case 'c':
      connect ();
      break;
   case 's':
      set_params ();
      break;
   case '?':
   case 'h':
      print_help ();
      break;
   default:
      printf ("Unknown command!\n");
}
```

####### while 语句

while 语句的使用形式如下：

```
while (expression) statement
```

*statement* 会一直执行，直到 *expression* 求值为 0。while 语句在每次执行语句之前都会对表达式进行求值。因此，while 循环执行语句零次或多次。以下是一个用于将一个数组复制到另一个数组的 while 语句：

```
i = length;
while (i >= 0)  /* Copy one array to another */
{
   array2[i] = array1[i];
   i--;
}
```

### 函数

*函数* 是声明和语句的集合。因此，函数是 C 程序的构建模块。每个 C 程序至少有一个函数——*main 函数*，C 程序的执行从该函数开始。C 库主要包含函数，尽管它也包含许多宏。

####### 函数原型

在 C 中，您必须在使用函数之前声明该函数。函数声明告诉编译器该函数返回值的类型以及它接受的参数的数量和类型。将函数声明为完整的 *函数原型*，显示返回类型以及参数列表。C 库中的 *calloc* 函数返回一个 void 指针并接受两个参数，每个参数的类型都是 *size_t*，这是一种无符号整数类型，其大小足以容纳 *sizeof* 运算符的值。因此，*calloc* 的函数原型如下：

```
void *calloc(size_t, size_t);
```

此原型显示参数列表中每个参数的类型。您还可以为每个参数包含一个标识符。在这种情况下，您按以下方式编写原型：

```
void *calloc(size_t num_elements, size_t elem_size);
```

在此，原型看起来与函数定义的第一行完全一样，除了您没有定义函数，并以分号结束该行。如果为参数选择恰当的命名，这种形式的大名原型可以提供大量关于函数用途的信息。例如，只需看一眼 *calloc* 的原型，就可以知道其第一个参数是要分配的元素的个数，第二个参数是每个元素的大小。

原型还有助于编译器检查函数参数并生成可能使用更快的参数传递机制的代码。根据原型，编译器可以确定预期的精确参数数量和类型。因此，原型使编译器能够捕获您在调用函数时可能犯的任何错误，例如传递错误数量的参数（当函数接受固定数量的参数时）或向函数传递错误类型的参数。

####### void 类型

当函数不返回任何内容也不接受任何参数时，您该怎么办？为了处理这些情况，C 提供了 `void` 类型，它对于声明不返回任何内容的函数以及描述可以指向任何类型数据的指针非常有用。例如，您可以使用 `void` 返回类型来声明像 `exit` 这样不返回任何内容的函数：

```
void exit(int status);
```
另一方面，如果函数不接受任何形式参数，其参数列表由 `void` 表示：

```
FILE *tmpfile(void);
```

void 指针对于处理内存块的函数非常有用。例如，当您从内存分配例程 `malloc` 请求一定数量的字节时，您可以使用这些位置存储适合该空间的任何数据。在这种情况下，分配的内存块的第一个位置的地址作为 `void` 指针返回。因此，`malloc` 的原型如下编写：

```
void *malloc(size_t nbytes);
```

####### 具有可变数量参数的函数

如果函数接受可变数量的参数，您可以通过在参数列表中用省略号（`...`）来表示；但是，您必须在省略号之前提供至少一个参数。这类函数的一个很好的示例是在头文件 `stdio.h` 中定义的 `printf` 系列函数。这些函数的原型如下：

```
int printf(const char *format, ...);
int sprintf(char *buffer, const char *format, ...);
```

###### C 库

C 的 ANSI 和 ISO 标准定义了 C 的各个方面——语言、预处理器和库。库中函数的原型，以及所有必要的数据结构和预处理器常量，都在一组标准头文件中定义。表 2-4 列出了标准头文件，包括其内容摘要。

![](img/11709a8f88c8cd03868a929dc94c0e2b_747_0.png)

如果您打算用 C 编写应用程序，您必须熟悉许多标准库，因为 C 的许多编程过程都在那里。如果您正在编写图形应用程序，您还必须熟悉其他库，例如 GIMP 工具包。




###### C 语言标准头文件

| 头文件 | 用途 |
| :--- | :--- |
| <assert.h> | 定义 `assert` 宏。用于程序诊断。 |
| <ctype.h> | 声明用于字符分类和转换的函数 |
| <errno.h> | 定义错误条件的宏 `EDOM` 和 `ERANGE`，以及库函数返回错误码的整型变量 `errno` |
| <float.h> | 定义可存储在浮点类型中的值范围 |
| <iso646.h> | 定义一组宏，有助于使用非英语语言编写 C 程序，这些语言可能将 `&&` 和 `--` 等字符组合用于其他用途 |
| <limits.h> | 定义所有整型数据类型的极限值 |
| <locale.h> | 声明 `locale` 结构体以及将 C 程序定制到特定语言环境所必需的函数 |
| <math.h> | 声明常见的数学函数和 `HUGE_VAL` 宏 |
| <setjmp.h> | 定义 `setjmp` 和 `longjmp` 函数，这些函数可以在不依赖常规函数调用和返回的情况下将一个函数的控制权转移到另一个函数。还定义了 `setjmp` 和 `longjmp` 使用的 `jmp_buf` 数据类型。 |
| <signal.h> | 定义处理异常条件所需的符号和例程 |
| <stdarg.h> | 定义提供对接受可变数量参数的函数中未命名参数访问的宏 |
| <stddef.h> | 定义标准数据类型 `ptrdiff_t`、`size_t`、`wchar_t`；符号 `NULL`；以及 `offsetof` 宏。 |
| <stdio.h> | 声明输入和输出操作所需的函数和数据类型。定义诸如 `BUFSIZ`、`EOF`、`SEEK_CUR`、`SEEK_END` 和 `SEEK_SET` 等宏。 |
| <stdlib.h> | 声明许多实用函数，如字符串转换例程、随机数生成器、内存分配例程和进程控制例程（如 `abort`、`exit` 和 `system`）。 |
| <string.h> | 声明字符串操作例程，如 `strcmp` 和 `strcpy`。 |
| <time.h> | 定义数据类型并声明操作时间的函数。定义类型 `clock_t` 和 `time_t` 以及 `tm` 数据结构 |
| <wchar.h> | 定义数据类型并声明用于处理宽字符数据类型（`wchar_t`）的函数。 |
| <wctype.h> | 定义数据类型并声明用于分类和转换宽字符数据类型（`wchar_t`）的函数。 |

###### Linux 应用程序中的共享库

大多数 Linux 程序都使用共享库。至少，大多数 C 程序都使用 C 共享库 `libc.so.x`，其中 *x* 是版本号。使用共享库是理想的，因为许多可执行程序可以共享同一个共享库——你只需要在内存中加载一个共享库的副本。此外，*动态链接*（程序在运行时加载代码模块并与之链接）变得越来越流行，因为它允许应用程序仅在需要时加载代码块，从而减少应用程序的内存需求。

当程序使用一个或多个共享库时，你需要程序的可执行文件以及所有共享库才能运行该程序。换句话说，如果系统中没有所有共享库，你的程序就无法运行。

![](img/11709a8f88c8cd03868a929dc94c0e2b_749_0.png)

如果你销售的应用程序使用共享库，请确保所有必要的共享库都与你的软件一起分发。

共享库的主题对 Linux 程序员来说很有趣，因为使用共享库可以减小可执行文件的大小。在接下来的部分中，我将简要描述如何在示例程序中创建和使用共享库。

####### 检查程序使用的共享库

使用 `ldd` 工具来确定可执行程序需要哪些共享库。输入以下 `ldd` 命令以查看程序（GCC 默认存储在名为 `a.out` 的文件中）使用的共享库：

```bash
ldd a.out
```

以下是 `ldd` 针对典型 C 程序报告的内容：

```text
        linux-gate.so.1 =>   (0xffffe000)
        libc.so.6 => /lib/tls/libc.so.6 (0x4002a000)
        /lib/ld-linux.so.2 (0x40000000)
```

更复杂的程序，如 The GIMP（类似 Adobe Photoshop 的程序），会使用更多共享库。要查看其共享库需求，请输入以下命令：

```bash
ldd /usr/bin/gimp
```

在这种情况下，你会发现从冗长的输出中该程序使用了很多共享库，包括 X11 库（`libX11.so.6`）、The GIMP 工具包（`libgtk-x11+2.0.so`）、通用绘图工具包（GDK）库（`libgdk-x11*2.0.so.0`）、数学库（`libm.so.6`）和 C 库（`libc.so.6`）。

几乎任何 Linux 应用程序都需要共享库才能运行。

*创建共享库*

为你自己的应用程序创建共享库相当简单。假设你想以共享库的形式实现一个对象。（将*对象*想象为代码和数据的集合。）共享库中的一组函数代表对象的接口。要使用对象，你加载其共享库并调用其接口函数。（我将在下一节中展示如何加载库。）

以下是这个简单对象的 C 源代码，实现为共享库（你也可以称其为*动态链接库*）——将此代码保存为名为 `dynobj.c` 的文件：

```c
/*---------------------------------------------*
 * File: dynobj.c
 *
 * Demonstrate use of dynamic linking.
 * Pretend this is an object that can be created by
 * calling
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
/*---------------------------------------------*/
/* init
 * Initialize object (allocate storage).
 */
void * init(char *name)
{
    OBJDATA *data = (OBJDATA*)calloc(1, sizeof(OBJDATA));
    if(name)
    {
        data->name = malloc(strlen(name)+1);
        strcpy(data->name, name);
    }
    printf("Created: %s\n", name);
    return data;
}
/*---------------------------------------------*/
/* show
 *
 *  Show the object.
 */
void show(void *data)
{
    OBJDATA *d = (OBJDATA*)data;
    printf("show: %s\n", d->name);
}
/*-----------------------------*/
/* destroy
 *
 *  Destroy the object (free all storage).
 */
void destroy(void *data)
{
    OBJDATA *d = (OBJDATA*)data;
    if (d)
    {
        if (d->name)
        {
            printf("Destroying: %s\n", d->name);
            free(d->name);
        }
        free(d);
    }
}
```

该对象提供三个接口函数：

- `init` 用于分配任何必要的存储并初始化对象
- `show` 用于显示对象（这里，它只是打印一条消息。）
- `destroy` 用于释放任何存储

要构建名为 **libdobj.so** 的共享库，请遵循以下步骤：

1. 使用 `-fPIC` 标志编译所有源文件。在这种情况下，使用以下命令编译 `dynobj.c` 文件：

   ```bash
   gcc -fPIC -c dynobj.c
   ```

2. 使用 `-shared` 标志将目标文件链接到共享库中，并为链接器提供适当的标志。要创建名为 `libdobj.so.1` 的共享库，请使用以下内容：

   ```bash
   gcc -shared -Wl,-soname,libdobj.so.1 -o libdobj.so.1.0 dynobj.o
   ```

3. 建立一系列符号链接，以便使用共享库的程序可以用标准名称引用它。

   对于示例库，标准名称是 `libdobj.so`，以下命令设置符号链接：

   ```bash
   ln -sf libdobj.so.1.0 libdobj.so.1
   ln -sf libdobj.so.1 libdobj.so
   ```

4. 当你测试共享库时，使用以下命令定义并导出 `LD_LIBRARY_PATH` 环境变量：

   ```bash
   export LD_LIBRARY_PATH=`pwd`:$LD_LIBRARY_PATH
   ```

   测试共享库并确信该库工作正常后，将其复制到标准位置，如 `/usr/local/lib`，并运行 `ldconfig` 工具以更新 `libdobj.so.1` 和 `libdobj.so.1.0` 之间的链接。这些是你用于安装共享库供所有人使用的命令。（你必须以 `root` 身份执行这些步骤。）

   ```bash
   cp libdobj.so.1.0 /usr/local/lib
   /sbin/ldconfig
   cd /usr/local/lib
   ln -s libdobj.so.1 libdobj.so
   ```

####### 动态加载共享库

在程序中加载共享库并使用共享库中的函数很简单。在本节中，我将演示如何执行此操作。头文件 `<dlfcn.h>`（这是 Linux 中的标准头文件）声明了加载和使用共享库的函数。`dlfcn.h` 文件中声明了四个用于动态加载的函数：

- `void *dlopen(const char *filename, int flag);`：加载由文件名指定的共享库，并返回该库的手柄。标志可以是 `RTLD_LAZY`（在执行库代码时解析未定义的符号）；或者 `RTLD_NOW`（在 `dlopen` 返回之前解析所有未定义的符号，如果并非所有符号都已定义则失败）。如果 `dlopen` 失败，它返回 `NULL`。
- `const char *dlerror (void);`：如果 `dlopen` 失败，调用 `dlerror` 获取包含错误描述字符串。
- `void *dlsym (void *handle, char *symbol);`：返回由句柄（由 `dlopen` 返回）标识的共享库中指定符号（函数名）的地址。
- `int dlclose (void *handle);`：如果没有其他使用者，则卸载共享库。




####### 动态链接测试程序

使用这些函数中的任何一个时，请包含头文件 `dlfcn.h`，并带有以下预处理器指令：

```
#include <dlfcn.h>
```

最后，这是一个简单的测试程序——`dtest.c`——展示了如何加载和使用共享库 `libdobj.so` 中定义的对象，你将在前面部分创建该对象：

```
/*---------------------------------------------------*/

/* File: dtest.c
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

 /* Open the shared library and set up the function
 pointers */
 if (dlobj = dlopen ("libdobj.so.1", RTLD_LAZY))
 {
 void *data;
 init_call=dlsym (dlobj, "init");
 show_call=dlsym (dlobj, "show");
 destroy_call=dlsym (dlobj, "destroy");

 /* Call the object interfaces */
 data = (*init_call)("Test Object");
 (*show_call)(data);
 (*destroy_call)(data);
 }
 return 0;
}
```

该程序很直接：它加载共享库，获取库中函数的指针，并通过指针调用这些函数。

你可以以通常的方式编译和链接此程序，但你必须使用 `-l dl` 选项进行链接，以便能够使用在 `dlfcn.h` 中声明的函数。以下是如何构建程序 `dtest`：

```
gcc -o dtest dtest.c -l dl
```

要查看程序的运行情况，输入以下命令来运行 `dtest`：

```
./dtest
```

它显示以下输出行：

```
Created: Test Object
show: Test Object
Destroying: Test Object
```

虽然这个示例程序并不令人兴奋，但你现在有一个使用共享库的示例程序。

要查看使用共享库的好处，请回到前面部分并对共享库源文件——`dynobj.c`——做一些更改。例如，你可以在某个函数中打印其他消息，以便轻松识别已做的更改。仅重新构建共享库。然后再次运行 `dtest`。产生的输出显示了你在共享库中进行的更改效果，这意味着你可以独立于应用程序更新共享库。

![](img/11709a8f88c8cd03868a929dc94c0e2b_754_0.png)

共享库中的更改可能会影响系统中安装的许多应用程序。因此，在对*任何*共享库进行更改时请务必小心。同样，如果有人设法用一个包含恶意代码的库替换现有库，共享库也可能成为安全风险。

##### 第 3 章：编写 Shell 脚本

###### 本章内容

- 尝试简单的 shell 脚本
- 发现 shell 脚本的基础知识
- 探索 bash 的内置命令

Linux 提供了许多小而专业的命令，以及连接这些命令所需的“管道”设施。*管道*（plumbing）是指将一个命令的输出用作第二个命令输入的方式。*bash*（Bourne-Again Shell 的缩写）——大多数 Linux 系统中的默认 shell——通过 I/O 重定向和管道提供这种管道设施。*bash* 还包括诸如 *if* 语句（仅在特定条件为真时用于运行命令）和 *for* 语句（将命令重复指定次数）等功能。你可以在编写称为 *shell 脚本* 的程序时使用 *bash* 的这些功能。

在本章中，我将向你展示如何编写简单的 *shell 脚本*——存储在文件中的面向任务的 shell 命令集合。Shell 脚本用于自动化各种任务。例如，当你的 Linux 系统启动时，存储在 `/etc` 目录（例如 `/etc/init.d`）中各个子目录里的许多 shell 脚本会执行许多初始化任务。

###### 尝试简单的 Shell 脚本

如果你不是程序员，可能会觉得编程让人紧张。但 *shell 脚本编写*（或编程）可以简单到只需将几条命令存储在一个文件中。事实上，你甚至拥有一个包含单条命令的有用 shell 程序。

例如，在编写本书时，我从 X Window System 捕获屏幕并使用了截图制作插图。我使用 X 屏幕捕获程序 `xwd` 将屏幕图像存储在 X Window Dump (XWD) 格式中。然而，本书的制作团队希望截图像是 TIFF 格式。因此，我使用便携式位图 (PBM) 工具包将 XWD 图像转换为 TIFF 格式。为了转换每个文件，我运行了两个程序并删除了一个临时文件，如下所示：

```
xwdtopnm < file.xwd > file.pnm
pnmtotiff < file.pnm > file.tif
rm file.pnm
```

这些命令假定 `xwdtopnm` 和 `pnmtotiff` 程序位于 `/usr/bin` 目录中——该目录列在 `PATH` 环境变量中。顺便说一下，`xwdtopnm` 和 `pnmtotiff` 是 PBM 工具包中的两个程序。

转换了几个 XWD 文件为 TIFF 格式后，我对为每个文件输入相同的命令序列感到厌倦，所以我准备了一个名为 `totif` 的文件并保存了以下内容。（第一行带有*魔咒* `#!/bin/sh` 开始执行 *bash* 程序，然后执行文件中的剩余行——每个 shell 脚本都需要该行。）

```
#!/bin/sh
xwdtopnm < $1.xwd > $1.pnm
pnmtotiff < $1.pnm > $1.tif
rm $1.pnm
```

然后我使用此命令使 `totif` 文件可执行：

```
chmod +x totif
```

`chmod` 命令允许你更改文件的权限设置。其中一个设置决定文件是否可执行。`+x` 选项标记文件为可执行。你必须以这种方式标记它，因为 *bash* 只运行可执行文件。

现在，当我想要将文件 `figurel.xwd` 转换为 `figurel.tif` 时，我可以通过输入以下命令来完成：

```
./totif figurel
```

`./` 前缀表明 `totif` 文件位于当前目录——如果 `PATH` 环境变量包含当前目录，则不需要 `./` 前缀。`totif` 文件是一个 shell 脚本（也称为 *shell 程序*）。当你使用命令 `totif figurel` 运行此 shell 程序时，shell 会用 `figurel` 替换 `$1` 的每次出现。（注意 `$1` 指的是用户在执行脚本的命令中输入的第一个选项。）

Shell 脚本在系统管理员中很受欢迎。如果你是系统管理员，你可以构建一组自定义的 shell 脚本，帮助你自动化经常执行的任务。例如，如果一个硬盘似乎快满了，你可能想找到所有超过一定大小（比如 1 MB）且在过去 30 天内未被访问的文件。此外，你可能想向拥有大文件的所有用户发送电子邮件，要求他们归档并清理这些文件。你可以使用 shell 脚本执行所有这些任务。你可以从以下 `find` 命令开始，以识别大文件：

```
find / -type f -atime +30 -size +1000k -exec ls -l {} ; > /tmp/largefiles
```

此命令创建一个名为 /tmp/largefiles 的文件，其中包含关于占用过多空间旧文件的详细信息。获得文件列表后，你可以使用其他一些 Linux 命令——如 sort、cut 和 sed——来准备和发送电子邮件给拥有需要清理的大文件的用户。不要手动输入所有这些命令，而是将它们放入文件中并创建一个 shell 脚本。简而言之，这就是 shell 脚本的精髓——将 shell 命令收集到一个文件中，以便你可以轻松执行重复的系统管理任务。

正如大多数 Linux 命令接受命令行选项一样，bash 脚本也接受命令行选项。在脚本内部，你可以将选项引用为 $1、$2，等等。特殊名称 $0 指脚本本身的名称。

这是一个典型的接受参数的 bash 脚本：

```
#!/bin/sh
echo "This script's name is: $0"
echo "Argument 1: $1"
echo "Argument 2: $2"
```

第一行运行 /bin/sh 程序，随后处理脚本中的其余行。名称 /bin/sh 传统上指 Bourne shell——第一个 UNIX shell。在大多数 Linux 系统中，/bin/sh 是 /bin/bash 的符号链接，后者是 bash 的可执行程序。

将此简单脚本保存为名为 simple 的文件，并使用以下命令使该文件可执行：

```
chmod +x simple
```

现在按如下方式运行脚本：

```
./simple
```

它显示以下输出：

```
This script's name is: ./simple
Argument 1:
Argument 2:
```

第一行显示脚本的名称。由于你运行脚本时没有参数，脚本不显示参数的值。

现在尝试使用几个参数运行脚本，如下所示：

```
./simple "This is one argument" second-argument third
```

> **第八卷**
> **第三章**
> 编写 Shell 脚本





这次脚本显示了更多的输出：

```
This script's name is: ./simple
Argument 1: This is one argument
Argument 2: second-argument
```

如输出所示，shell 将双引号内的整个字符串视为单个参数。否则，shell 使用空格作为命令行上参数之间的分隔符。

该示例脚本忽略第三个参数，因为脚本设计为只打印前两个参数。脚本会忽略前两个参数之后的所有参数。

###### 探索 Shell 脚本基础

像任何编程语言一样，`bash` shell 支持以下功能：

- 存储值的变量，包括访问传递给 shell 脚本的命令行参数的特殊内置变量以及其他特殊值。
- 评估表达式的能力。
- 允许对多条 shell 命令进行循环或条件执行某些命令的控制结构。
- 定义可在脚本中许多地方调用的函数的能力。`bash` 还包含许多你可以用于任何脚本的内置命令。

在接下来的几个部分中，我通过简单的示例来说明这些编程功能。（我假设你已经在运行 `bash`，在这种情况下，你可以在终端窗口的 shell 提示符下输入示例来尝试。否则，你只需打开一个终端窗口，`bash` 就会运行并显示其提示符。）

####### 存储数据

你在 `bash` 中定义变量的方式与定义环境变量的方式相同。因此，你可以按以下方式定义变量：

```
count=12 # note no embedded spaces allowed
```

要使用变量的值，请在变量名前加美元符号（$）。例如，$PATH 是变量 PATH 的值。（这个变量是著名的 PATH 环境变量，它列出了 `bash` 在尝试定位可执行文件时搜索的所有目录。）要显示变量 count 的值，请使用以下命令：

```bash
echo $count
```

bash 有一些特殊的变量用于访问命令行参数。在 shell 脚本中，$0 指的是 shell 脚本的名称。变量 $1、$2 等指的是命令行参数。变量 $* 将所有命令行参数存储为单个变量，而 $? 包含 shell 执行的最后一个命令的退出状态。

在 bash 脚本中，你可以提示用户输入并使用 read 命令将输入读取到变量中。以下是一个示例：

```bash
echo -n "Enter value: "
read value
echo "You entered: $value"
```

当此脚本运行时，read value 命令会使 bash 读取你在键盘上输入的任何内容，并将你的输入存储在名为 value 的变量中。

注意：-n 选项可以防止 echo 命令在显示的字符串末尾自动添加新行。

####### 调用 shell 函数

你可以将一组经常使用的 shell 命令分组为一个函数，并为其分配一个名称。稍后，你可以通过使用该函数分配的名称来执行这组命令。以下是一个说明 shell 函数语法的简单脚本：

```bash
#!/bin/sh
hello() {
    echo -n "Hello, 
    echo $1 $2
}
hello Jane Doe
```

当你运行此脚本时，它会显示以下输出：

```text
Hello, Jane Doe
```

此脚本定义了一个名为 hello 的 shell 函数。该函数期望两个参数。在函数主体中，这些参数通过 $1 和 $2 来引用。函数定义以 hello() 开头——即函数名称后跟括号。函数主体用花括号 — { … } 包围。在此情况下，主体使用 echo 命令显示一行文本。

示例的最后一行展示了如何带参数调用 shell 函数。在这种情况下，hello 函数被调用时带有两个参数：Jane 和 Doe。hello 函数获取这两个参数并打印出一行文本，内容为 Hello, Jane Doe。

###### 控制流程

在 bash 脚本中，你可以使用 if、case、for 和 while 等特殊命令来控制执行流程——即命令执行的顺序。这些控制语句使用命令的退出状态来决定下一步做什么。当任何命令执行时，它都会返回一个退出状态——一个指示命令是否成功的数值。按照惯例，退出状态为零表示命令已成功。（是的，你没看错：零表示成功！）非零的退出状态表示命令出现了问题。

例如，假设你想在 vi 编辑器编辑文件之前对该文件进行备份复制。更重要的是，如果无法创建备份，你希望避免编辑该文件。下面是一个处理此任务的 bash 脚本：

```
#!/bin/sh
if cp "$1" "$1"
then
vi "$1"
else
echo "Failed to create backup copy"
fi
```

此脚本说明了 if-then-else 结构的语法，并展示了 if 命令如何使用 cp 命令的退出状态来确定下一步操作。如果 cp 返回零，脚本使用 vi 编辑文件；否则，脚本显示错误消息并退出。顺便说一下，脚本将备份保存到一个文件名与原始文件相同但文件名开头添加了井号（#）的文件中。

别忘了用于终止 if 命令的最终 fi。忘记 fi 是 bash 脚本中常见的错误来源。

你可以使用 test 命令来评估任何表达式，并将该表达式的值用作命令的退出状态。假设你想要一个仅在文件已存在时才编辑该文件的脚本。使用 test，你可以如下编写此脚本：

```
#!/bin/sh
if test -f "$1"
then
vi "$1"
else
echo "No such file"
fi
```

`test` 命令的一种更短形式是将表达式放在方括号中。使用这种简写表示法，你可以像这样重写前面的脚本：

```
#!/bin/sh
if [ -f "$1" ]
then
vi "$1"
else
echo "No such file"
fi
```

**注意：** 两个方括号周围必须有空格。

另一种常见的控制结构是 `for` 循环。以下脚本将 1 到 10 的数字相加：

```
#!/bin/sh
sum=0
for i in 1 2 3 4 5 6 7 8 9 10
do
sum=`expr $sum + $i`
done
echo "Sum = $sum"
```

此示例还说明了如何使用 `expr` 命令来评估表达式。

`case` 语句根据变量的值执行一组命令。例如，考虑以下脚本：

```
#!/bin/sh
echo -n "What should I do -- (Y)es/(N)o/(C)ontinue? [Y] "
read answer
case $answer in
y|Y|"" )
echo "YES"
;;
c|C )
echo "CONTINUE"
;;
n|N )
echo "NO"
;;
* )
echo "UNKNOWN"
esac
```

将此代码保存为一个名为 *confirm* 的文件，并输入 **chmod +x confirm** 使其可执行。然后像这样尝试一下：

```
./confirm
```

当脚本提示你时，输入字符 **y**、**n** 或 **c** 之一，然后按 Enter。脚本将显示 **YES**、**NO** 或 **CONTINUE**。例如，当我输入 **c**（然后按 Enter）时会发生什么：

```
What should I do -- (Y)es/(N)o/(C)ontinue? [Y] c
CONTINUE
```

脚本显示提示并读取你输入的字符。你的输入存储在一个名为 *answer* 的变量中。然后，**case** 语句根据 *answer* 变量的值执行一段代码。例如，当我输入 **c** 时，将执行以下命令块：

```
c|C)
echo "CONTINUE"
;;
```

**echo** 命令使脚本显示 **CONTINUE**。

从这个例子中，你可以看到 **case** 命令的一般语法如下：

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

基本上，**case** 命令以单词 **case** 开头，以 **esac** 结尾。代码块之间由变量的值分隔，后跟右括号并以一对分号（**;;**）终止。




###### 探索 bash 的内置命令

`bash` 拥有超过 50 个内置命令，包括 `cd` 和 `pwd` 等常用命令，以及许多不常用的命令。你可以在任何 `bash` 脚本或 Shell 提示符中使用这些内置命令。表 3-1 描述了大多数 `bash` 内置命令及其参数。浏览这些信息后，键入 `help command` 以阅读有关特定内置命令的更多详细信息。例如，若要了解内置命令 `test` 的更多详细信息，键入以下内容：

```
help test
```

这样做将显示以下信息：

```
test: test [expr]

根据 EXPR 的求值结果，以状态 0（真）或 1（假）退出。表达式可以是单目或二目。单目表达式通常用于检查文件的状态。除了字符串运算符外，还有数值比较运算符。
```

####### 文件运算符：

- `-a FILE`：如果文件存在则为真。
- `-b FILE`：如果文件是块特殊文件则为真。
- `-c FILE`：如果文件是字符特殊文件则为真。
- `-d FILE`：如果文件是目录则为真。
- `-e FILE`：如果文件存在则为真。
- `-f FILE`：如果文件存在且是普通文件则为真。
- `-g FILE`：如果文件设置了 set-group-id 标志则为真。
- `-h FILE`：如果文件是符号链接则为真。
- `-L FILE`：如果文件是符号链接则为真。
- `-k FILE`：如果文件设置了“粘滞”位（'sticky' bit）则为真。
- `-p FILE`：如果文件是命名管道则为真。
- `-r FILE`：如果你可以读取该文件则为真。
- `-s FILE`：如果文件存在且不为空则为真。
- `-S FILE`：如果文件是套接字则为真。
- `-t FD`：如果文件描述符 FD 在终端上打开则为真。
- `-u FILE`：如果文件设置了 set-user-id 标志则为真。
- `-w FILE`：如果你可以写入该文件则为真。
- `-x FILE`：如果你可以执行该文件则为真。
- `-O FILE`：如果你是该文件的有效所有者则为真。
- `-G FILE`：如果你的组是该文件的有效所有者则为真。

*（已删除若干行）*

在必要时，来自 `help` 命令的在线帮助包含大量详细信息。

![](img/11709a8f88c8cd03868a929dc94c0e2b_764_0.png)

某些外部程序可能与 `bash` 内置命令同名。如果你想运行此类外部程序，必须明确指定该程序的完整路径名。否则，`bash` 将执行同名的内置命令。

####### 表 3-1
bash Shell 中内置命令的摘要

| 此功能 | 执行以下操作 |
| :--- | :--- |
| `. filename [arguments]` | 使用可选参数从指定文件读取并执行命令。（工作方式与 *source* 命令相同。） |
| `: [arguments]` | 扩展参数但不处理它们 |
| `[ expr ]` | 评估表达式 *expr*，如果 *expr* 为真则返回零状态 |
| `alias [name[=value] ...]` | 定义一个别名 |
| `bg [job]` | 将指定任务置于后台。如果没有指定任务，则将当前正在执行的命令置于后台。 |
| `bind [-m keymap] [-lvd] [-q name]` | 将按键序列绑定到宏 |
| `break [n]` | 退出 *for*、*while* 或 *until* 循环。如果指定了 *n*，则退出第 *n* 个外层循环。 |
| `builtin builtin_command [arguments]` | 执行 Shell 内置命令 |
| `cd [dir]` | 将当前目录更改为 *dir* |
| `command [-pVv] cmd [arg ...]` | 使用指定参数运行命令 *cmd*（忽略名为 *cmd* 的任何 Shell 函数） |
| `continue [n]` | 开始 *for*、*while* 或 *until* 循环的下一次迭代。如果指定了 *n*，则开始第 *n* 个外层循环的下一次迭代。 |
| `declare [-aiIlnrx] [name=value]` | 声明具有指定名称的变量，并可选地为其分配一个值。 |
| `dirs [-lv] [+/-n]` | 显示当前记住的目录列表 |
| `echo [-nE] [arg ...]` | 在标准输出上显示参数 |
| `enable [-n] [-a] [name ...]` | 启用或禁用指定的内置命令 |
| `eval [arg ...]` | 连接参数并将其作为命令执行 |
| `exec [command [arguments]]` | 用一个运行指定命令的新进程替换当前的 Shell 实例 |
| `exit [n]` | 以状态码 *n* 退出 Shell |
| `export [-nf] [name=[word]] ...` | 定义指定的环境变量并将其导出到后续进程 |
| `fc -s [pat=rep] [cmd]` | 将模式 pat 替换为 rep 后重新执行命令 |
| `fg [jobspec]` | 将指定任务置于前台。如果没有指定任务，则将最近的任务置于前台。 |
| `getopts optstring name [args]` | 获取可选参数（在 Shell 脚本中用于从命令行提取参数时称为此调用） |
| `hash [-r] [name]` | 记住指定命令的完整路径名 |
| `help [cmd ...]` | 显示指定内置命令的帮助信息 |
| `history [n]` | 显示过去命令，或如果指定了数字 n 则显示过去 n 条命令 |
| `jobs [-lnp] [jobspec ...]` | 列出当前活动任务 |
| `kill [-s sigspec \| -SIGSPEC] [pid \| jobspec] ...` | 向指定进程发送信号 |
| `let arg [arg ...]` | 评估每个参数，如果最后一个 arg 为 0 则返回 1 |
| `local [name=value] ...` | 创建具有指定名称和值的局部变量（用于 Shell 函数中） |
| `logout` | 退出登录 Shell |
| `popd [+/−n]` | 从目录栈中移除条目 |
| `pushd [dir]` | 将指定目录添加到目录栈的顶部 |
| `pwd` | 打印当前工作目录的完整路径名 |
| `read [-r] [name ...]` | 从标准输入读取一行并进行解析 |
| `readonly [-f] [name ...]` | 将指定变量标记为只读，以便稍后不能更改这些变量 |
| `return [n]` | 以返回值 n 退出 Shell 函数 |
| `set [-abefhkmnptuvx1LCHP] [-o option] [arg ...]` | 设置各种标志 |
| `shift [n]` | 使第 n+1 个参数变为 $1，第 n+2 个参数变为 $2，依此类推 |
| `source filename [arguments]` | 从文件读取并执行命令 |
| `suspend [-f]` | 停止执行，直到收到 SIGCONT 信号 |
| `test expr` | 评估表达式 expr，如果 expr 为真则返回零 |
| `times` | 打印从 Shell 运行的进程累积的用户和系统时间 |
| `trap [-1] [cmd] [sigspec]` | 当收到信号 sigspec 时执行 cmd |
| `type [-all] [-type \| -path] name [name ...]` | 指示 Shell 如何解释每个名称 |
| `ulimit [-SHacd] [limit]` | 控制可供 Shell 使用的资源 |
| `umask [-S] [mode]` | 设置文件创建掩码——文件的默认权限 |
| `unalias [-a] [name ...]` | 取消定义指定的别名 |
| `unset [-fv] [name ...]` | 删除指定变量的定义 |
| `wait [n]` | 等待指定进程终止 |

##### 第 4 章：使用 Perl 编程

- **本章内容**
  - 编写你的第一个 Perl 程序
  - 概览 Perl
  - 理解 Perl 包和模块
  - 在 Perl 中使用对象

**当**涉及到编写脚本时，Perl 语言在系统管理员中非常流行，尤其是在 UNIX 和 Linux 系统上。系统管理员使用 Perl 来自动执行常规系统管理任务，例如查找可以归档和删除以释放磁盘空间旧文件。

Perl 是一种脚本语言，这意味着你不必编译和链接 Perl 脚本（包含 Perl 命令的文本文件）。相反，由解释器执行 Perl 脚本。这种特性使编写和测试 Perl 脚本变得容易，因为你不需要经历典型的编辑-编译-链接循环来编写 Perl 程序。

除了编程容易之外，Perl 流行的另一个原因是 Perl 是免费分发的，并且可用于各种操作系统，包括 Linux 以及 UNIX、Windows 95/98/NT/2000/XP 和 Apple Mac OS X 等许多其他操作系统。

在本章中，我将向你介绍 Perl 脚本编程。

###### 理解 Perl

正式来说，Perl 代表 *Practical Extraction Report Language*（实用提取报告语言），但 Perl 的创造者 Larry Wall 说，人们常把 Perl 称为 *Pathologically Electic Rubbish Lister*（病态杂烩垃圾列表器）。正如这些名称所暗示的，Perl 最初被设计用于从文本文件中提取信息并生成报告。

Perl 于 1986 年作为由 Larry Wall 创建的系统管理工具而诞生。随着时间的推移，Perl 通过不断累积许多新功能和函数而发展起来。最新版本——Perl 5.8——支持面向对象编程，并允许任何人通过添加指定格式的新模块来扩展 Perl。




作为系统管理工具，Perl 始终名副其实，多年来深受 UNIX 系统管理员的欢迎。近年来，随着万维网（或简称 Web）的普及以及通用网关接口（CGI）程序需求的产生，Perl 成为了熟悉该语言的用户的自然选择。Perl 近期的人气飙升主要源于其在为 Web 编写 CGI 程序中的应用。当然，随着人们更加关注 Perl，他们发现 Perl 的用途远不止 CGI 编程。反过来，这使得 Perl 在用户中变得更加流行。

Perl 可在多种计算机系统上使用，因为与 Linux 操作系统一样，Perl 可以免费分发。

如果你熟悉 shell 编程或 C 编程语言，你可以很快掌握 Perl。如果你从未编写过程序，精通 Perl 可能需要一段时间。我建议你从 Perl 功能的一个小子集开始，并忽略任何你立即无法理解的内容。然后，慢慢将 Perl 功能添加到你的技能库中。

###### 判断是否已安装 Perl

在继续 Perl 教程之前，请检查你的 Linux 系统是否已安装 `perl` 程序。输入以下命令：

```
which perl
```

`which` 命令会告诉你它是否在 `PATH` 环境变量中列出的目录中找到指定的程序。如果已安装 `perl`，你将看到以下输出：

```
/usr/bin/perl
```

你应该能在所有 Linux 发行版中找到预装的 Perl。

检查 Perl 的另一种方法是输入以下命令以查看其版本号：

```
perl -v
```

以下是该命令的典型输出：

```
This is perl, v5.8.7 built for i586-linux-thread-multi
Copyright 1987-2005, Larry Wall
```

完整的 Perl 文档（包括常见问题解答列表）应使用 'man perl' 或 'perldoc perl' 在此系统中找到。如果你可以访问互联网，请将浏览器指向 <http://www.perl.org/>，这是 Perl 主页。

此输出告诉你，你拥有 Perl 版本 5.8，补丁级别 7，并且 Perl 的创始人 Larry Wall 持有版权。（请记住，Perl 是在 GNU 通用公共许可证下免费分发的。）

![](img/11709a8f88c8cd03868a929dc94c0e2b_770_0.png)

你可以通过将万维网浏览器指向综合 Perl 存档网络（CPAN）来获取 Perl 的最新版本。以下地址将连接你到离你最近的 CPAN 站点：

```
www.perl.com/CPAN
```

###### 编写你的第一个 Perl 脚本

Perl 具有 C 的许多特性，正如你可能知道的，大多数关于 C 的书都以一个在终端上显示 Hello, World! 的示例程序开始。由于 Perl 是解释型语言，而 C 和 C++ 是需要在程序运行前进行编译的，因此你可以直接通过命令行完成此任务。如果你输入：

```
perl -e 'print "Hello, World!\n";'
```

Perl 会以以下内容响应：

```
Hello, World!
```

此命令使用 perl 程序的 -e 选项将 Perl 程序作为命令行参数传递给 Perl 解释器。在这种情况下，下面这行构成了 Perl 程序：

```
print "Hello, World!\n";
```

要将这一行转换为 Perl 脚本，只需将该行放在一个文件中，并在文件开头添加一条运行 perl 程序的指令（就像你在 shell 脚本中放置诸如 #!/bin/sh 这样的行来运行 shell 以处理脚本一样）。

要尝试这个 Perl 脚本，请遵循以下步骤：

- 1. **使用文本编辑器将以下各行输入并保存为名为 hello.pl 的文件：**

```perl
#!/usr/bin/perl
# This is a comment.
print "Hello, World!\n";
```

![](img/11709a8f88c8cd03868a929dc94c0e2b_770_1.png)

- 2. 使用以下命令使 hello.pl 文件可执行：

```
chmod +x hello.pl
```

- 3. 通过在 shell 提示符下输入以下内容来运行 Perl 脚本：

```
./hello.pl
```

它将显示以下输出：

```
Hello, World!
```

就是这样！你已经编写并尝试了你的第一个 Perl 脚本。

![](img/11709a8f88c8cd03868a929dc94c0e2b_771_0.png)

请注意，Perl 脚本的第一行以 #! 开头，后跟 perl 程序的完整路径名。如果脚本的第一行以 #! 开头，shell 会简单地去掉 #!，将脚本文件的名称附加到末尾，并运行脚本。因此，如果脚本文件名为 hello.pl，且第一行是 #!/usr/bin/perl，shell 将执行以下命令：

```
/usr/bin/perl hello.pl
```

###### 概览 Perl

大多数编程语言，包括 Perl，都有一些共同特性：

- 变量存储不同种类的数据。你可以将每个变量视为数据的一个占位符——有点像带有名称和存储空间的数据邮箱。变量的内容就是其值。
- 表达式通过运算符组合变量。一个表达式可能添加几个变量；另一个可能提取字符串的一部分。
- 语句执行某些操作，例如将值分配给变量或打印字符串。
- 流程控制语句使语句能够根据某些表达式的值以不同顺序执行。通常，流程控制语句包括 for、do-while、while 和 if-then-else 语句。
- 函数（也称为子程序或例程）使你能够分组多个语句并给它们命名。使用此功能，你可以通过调用表示这些语句的函数来执行同一组语句。通常，编程语言提供一些预定义函数。
- 软件包和模块使你能够组织一组相关的、旨在可重用的 Perl 子程序。（模块是在 Perl 5 中引入的。）

在接下来的几个部分中，我将概述 Perl 的这些主要特性，并通过简单的示例来说明这些特性。

####### 基本 Perl 语法

Perl 是自由格式的，就像 C 一样。关键字的确切位置没有约束。通常，Perl 程序存储在以 .pl 结尾的文件名的文件中，但你使用的文件名没有限制。

与 C 语言一样，每个 Perl 语句以分号 (;) 结尾。井号或英镑符号 (#) 标志着注释的开始：perl 程序会忽略从井号开始的该行剩余部分。

Perl 语句组被花括号 ( { . . . } ) 包围。此特性在 C 中也很相似。

#### 变量

你不必像 C 编程语言中那样在使用前声明 Perl 变量。你可以轻松识别 Perl 脚本中的变量，因为每个变量名都以一个特殊字符开头：at 符号 (@)、美元符号 ($) 或百分号 (%)。这些特殊字符表示变量的类型。三种变量类型如下：

- **标量变量** 表示基本数据类型：整数、浮点数和字符串。美元符号 ($) 位于标量变量之前。以下是一些示例：
  ```
  $maxlines = 256;
  $title = "Linux All-in-One Desk Reference For Dummies";
  ```

- **数组变量** 是标量变量的集合。数组变量带有 at 符号 (@) 前缀。因此，以下是数组：
  ```
  @pages = (62, 26, 22, 24);
  @commands = ("start", "stop", "draw", "exit");
  ```

- **关联数组** 是键值对的集合，其中每个键都是字符串，值可以是任何标量变量。百分号 (%) 前缀表示关联数组。你可以使用关联数组将名称与值关联起来。你可以在关联数组中存储每个用户占据的磁盘空间量，例如：
  ```
  %disk_usage = ("root", 147178, "naba", 28547,
                 "emily", 55, "ashley", 40);
  ```

由于每种变量类型都有一个特殊的字符前缀，你可以为不同的变量类型使用相同的名称。因此，%disk_usage、@disk_usage 和 $disk_usage 可以出现在同一个 Perl 程序中。





######## 标量

*标量变量* 可以存储单个值，例如数字或文本字符串。标量变量是 Perl 中的基本数据类型。每个标量的名称都以美元符号（$）开头。通常，你通过初始化赋值语句开始使用一个标量。你甚至可以未初始化变量就使用它；数字的默认值为零，字符串的默认值为空字符串。如果你想检查一个标量是否已定义，可以如下使用 defined 函数：

```perl
print "Name undefined!\n" if !(defined $name);
```

如果 $name 已定义，表达式 (defined $name) 的值为 1。你可以使用 undef 函数来*取消定义*一个变量。例如，你可以如下取消定义 $name：

```perl
undef $name;
```

变量的求值取决于上下文。下面是一个初始化并打印几个变量的脚本：

```perl
#!/usr/bin/perl
$Title = "Linux All-in-One Desk Reference For Dummies";
$count1 = 650;
$count2 = 166;
$total = $count1 + $count2;
print "Title: $Title -- $total pages\n";
```

当你运行上面的 Perl 程序时，它会产生以下输出：

```
Title: Linux All-in-One Desk Reference For Dummies -- 816 pages
```

正如 Perl 语句所示，当两个数值变量相加时，使用的是它们的数值；但当打印 $total 变量时，显示的是其字符串表示形式。

Perl 的另一个有趣之处在于它会评估双引号（" . . . "）内字符串中的所有变量。但是，如果你在单引号（' . . . '）内编写字符串，Perl 会保持该字符串原样不动。如果你编写

```perl
print 'Title: $Title -- $total pages\n';
```

使用单引号而不是双引号，Perl 将显示

```
Title: $Title -- $total pages\n
```

并且不会生成新行。

![](img/11709a8f88c8cd03868a929dc94c0e2b_774_0.png)

一个有用的 Perl 变量是 $_（美元符号后跟下划线字符）。这个特殊变量被称为默认参数。Perl 解释器根据上下文确定 $_ 的值。当 Perl 解释器从标准输入读取数据时，$_ 持有当前输入行；当解释器正在搜索特定文本模式时，$_ 持有默认搜索字符串。

######## 数组

在 Perl 中，数组是标量的集合。数组名称以 at 符号（@）开头。与 C 语言一样，数组下标从零开始。你可以使用索引访问数组的元素。Perl 动态分配数组的空间。

考虑以下简单脚本：

```perl
#!/usr/bin/perl
@commands = ("start", "stop", "draw", "exit");
$ncmpd = @commands;
print "There are $ncmpd commands.\n";
print "The first command is: $commands[0]\n";
```

当你运行该脚本时，它会产生以下输出：

```
There are 4 commands.
The first command is: start
```

正如你所见，将标量等于数组会将标量设置为数组中的元素数量。@commands 数组的第一个元素引用为 $commands[0]，因为下标从零开始。因此，@commands 数组中的第四个元素是 $commands[3]。

两个特殊的标量与数组相关。其中之一是 $[ 变量，它是当前的基索引（起始索引），默认为零。另一个标量是 $arrayname（其中 arrayname 是数组变量的名称），其值为最后一个数组索引。因此，对于 @commands 数组，$commands 的值为 3。

你可以使用简单的 print 语句打印整个数组，例如：

```perl
print "@commands\n";
```

当 Perl 执行此语句时，它显示以下输出：

```
start stop draw exit
```

######## 关联数组

*关联数组*变量（以百分号 % 前缀声明）是 Perl 的独特特性。使用关联数组，你可以用字符串（例如名称）作为数组的索引。关联数组的一个良好示例是 Perl 自动为你定义的 %ENV 数组。在 Perl 中，%ENV 是环境变量的数组，你可以使用环境变量名作为索引来访问它们。以下 Perl 语句打印当前的 PATH 环境变量：

```perl
print "PATH = $ENV{PATH}\n";
```

当 Perl 执行此语句时，它会打印 PATH 的当前设置。与索引常规数组不同，索引关联数组必须使用大括号。

Perl 有许多内置函数——例如 *delete, each, keys, and values* ——它们使你能够访问和操作关联数组。

####### Perl 中的预定义变量

Perl 有几个包含你可能在 Perl 脚本中需要的有用信息的预定义变量。以下是一些重要的预定义变量：

- **@ARGV** 是一个字符串数组，包含脚本的命令行选项。第一个选项是 $ARGV[0]，第二个是 $ARGV[1]，等等。
- **%ENV** 是一个包含环境变量的关联数组。你可以使用环境变量名作为键来访问此数组。要访问数组中的每个元素，将百分号改为美元符号，并用大括号括起键。例如，$ENV{HOME} 是主目录，$ENV{PATH} 是 shell 用于定位命令的当前搜索路径。
- **$_** 是许多函数的默认参数。如果你看到一个 Perl 函数未使用任何参数，该函数可能期望其参数包含在 $_ 变量中。
- **@_** 是传递给子程序的参数列表。
- **$0** 是包含 Perl 程序的文件的名称。
- **$]** 是你正在使用的 Perl 的版本号（例如，如果你使用 Perl 版本 5.8.7，$] 将为 5.008007）。
- **$<** 是运行该脚本的用户 ID（识别号码）。
- **$$** 是脚本的进程 ID。
- **$?** 是最后系统调用返回的状态。

####### 运算符和表达式

运算符用于结合和比较 Perl 变量。典型的数学运算符包括加法 (+)、减法 (-)、乘法 (*) 和除法 (/)。Perl 和 C 提供几乎相同的运算符集。当你使用运算符结合变量时，最终得到的是表达式。每个表达式都有一个值。

以下是一些典型的 Perl 表达式：

```perl
error < 0
$count == 10
$count + $i
$users{$1}
```

这些表达式是以下运算符的示例：比较运算符（前两行）、算术运算符和数组索引运算符。

> 在 Perl 中，不要使用 == 运算符来确定两个字符串是否匹配；== 运算符仅适用于数字。要测试字符串的相等性，Perl 包含了 FORTRAN 风格的 eq 运算符。使用 eq 来查看两个字符串是否相同，如下所示：

```perl
if ($input eq "stop") { exit; }
```

其他 FORTRAN 风格的字符串比较运算符包括 ne（不等）、lt（小于）、gt（大于）、le（小于或等于）和 ge（大于或等于）。此外，你可以使用 cmp 运算符来比较两个字符串。返回值是 -1、0 或 1，取决于第一个字符串是小于、等于还是大于第二个字符串。

Perl 还提供了一些独特的运算符。C 语言缺少幂运算符，而 FORTRAN 包含该运算符；Perl 使用 ** 作为幂运算符。因此，你可以在 Perl 中编写以下代码：

```perl
$x = 2;
$y = 3;
$z = $x ** $y; # z 应该是 8 (2 的 3 次方)
$y **= 2; # y 现在是 9 (3 的 2 次方)
```

你可以使用空列表运算符 () 将数组初始化为空，如下所示：

```perl
@commands = ();
```

点运算符 (.) 允许你连接两个字符串，如下所示：

```perl
$part1 = "Hello, ";
$part2 = "World!";
```

```perl
$message = $part1 . $part2; # 现在 $message = "Hello, World!"
```

重复运算符（由 `x` 表示）很有趣且非常有用。你可以使用 `x` 运算符将字符串重复指定次数。假设你想将一个字符串初始化为 65 个星号（`*`）。以下示例展示了如何使用 `x` 运算符初始化字符串：

```perl
$marker = "*";
$marker x= 65; # 现在 $marker 是一个由 65 个星号组成的字符串
```

Perl 中另一个强大的运算符是 `range`，它由两个句点（`..`）表示。你可以使用范围运算符轻松地初始化数组。以下是一些示例：

```perl
@numerals = (0..9); # @numerals = 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
@alphabet = ('A'..'Z'); # @alphabet = 大写字母 A 到 Z
```

####### 正则表达式

如果你使用 UNIX 或 Linux 系统有一段时间了，你大概知道 `grep` 命令，它允许你搜索文件中的字符串模式。以下是 `grep` 的典型用法：

```bash
cd /usr/include
grep "[Ll]inux" *.h | more
```

前面的 `grep` 命令查找所有以 `.h` 结尾的文件中 **Linux** 或 **linux** 的所有出现位置。

`grep` 命令的 "[Ll]inux" 参数被称为正则表达式，即匹配一组字符串的模式。你通过一组类似于编写算术表达式的一组运算符和规则来构建正则表达式。例如，方括号（[ ]）内的字符列表匹配列表中的任何单个字符。因此，正则表达式 "[Ll]inux" 是两个字符串的集合，如下所示：

```
Linux
linux
```

Perl 支持正则表达式，就像 `grep` 命令一样。其他许多 Linux 程序，如 `vi` 编辑器和 `sed`（流编辑器），也支持正则表达式。正则表达式的目的是在文件中搜索字符串模式。这就是为什么编辑器支持正则表达式的原因。

你可以在 Perl 中构建和使用复杂的正则表达式。这些正则表达式的规则相当简单。本质上，正则表达式是字符序列，其中某些字符具有特殊含义。表 4-1 总结了用于构建正则表达式的字符解释的基本规则。





######## 表 4-1 解释正则表达式字符的规则

| *表达式* | *含义* |
| :----------- | :-------- |
| .            | 匹配除换行符外的任意单个字符 |
| x*           | 匹配字符 x 出现零次或多次 |
| x+           | 匹配字符 x 出现一次或多次 |
| x?           | 匹配字符 x 出现零次或一次 |
| [ . . . ]   | 匹配括号内的任意一个字符 |
| x{n}         | 匹配字符 x 恰好出现 n 次 |
| x{n,}        | 匹配字符 x 出现 n 次或更多次 |
| x{n,m}       | 匹配字符 x 最多出现 m 次 |
| x{n,m}       | 匹配字符 x 至少出现 n 次，但不超过 m 次 |
| $            | 匹配行尾 |
| \0           | 匹配空字符 |
| \b           | 匹配退格符 |
| \B           | 匹配单词开头或结尾以外的任意字符 |
| \b           | 匹配单词的开头或结尾——当不在括号内部时 |
| \cX          | 匹配 Ctrl-X（其中 X 是任意字母字符） |
| \d           | 匹配单个数字 |
| \D           | 匹配非数字字符 |
| \f           | 匹配换页符 |
| \n           | 匹配换行（行馈）字符 |
| \ooo         | 匹配由数字 ooo 指定的八进制值（其中每个 o 是 0 到 7 之间的数字） |
| \r           | 匹配回车符 |
| \S           | 匹配非空白字符 |
| \s           | 匹配空白字符（空格、制表符或换行符） |
| \t           | 匹配制表符 |
| \W           | 匹配非字母数字字符 |
| \w           | 匹配字母数字字符 |
| \xhh         | 匹配由数字 hh 指定的十六进制值（其中每个 h 是 0 到 f 之间的数字） |
| ^            | 匹配行首 |

如果你想匹配字符 $、!、*、^、[、]、\、/ 中的任意一个，必须在你想匹配的字符前加上一个反斜杠。因此，你需要将这些字符输入为 \$、\!、\*、\^、\[、\]、\\[、\\[ 和 \\[/。由于存在大量奇怪的字符序列和大量使用的反斜杠，正则表达式看起来往往令人困惑。不过，与其他事物一样，你可以慢慢开始，一开始只使用其中的一些功能。

到目前为止，我已经总结了正则表达式的语法。但我还没有展示如何在 Perl 中使用正则表达式。通常，你将正则表达式放置在一对斜杠之间，并使用匹配 (`m=`) 或不匹配 (`!m=`) 运算符来测试字符串。你可以编写一个 Perl 脚本，执行与本节前面使用 grep 进行的相同的搜索。按照以下步骤完成此任务：

1. 使用文本编辑器输入并将以下脚本保存为名为 `lookup` 的文件：

```perl
#!/usr/bin/perl
while (<STDIN>)
{
        if ( $_ =~ /[Ll]inux/ ) { print $_; }
}
```

2. 使用以下命令使 `lookup` 文件可执行：

```
chmod +x lookup
```

3. 使用以下命令尝试该脚本：

```
cat /usr/include/*.h | ./lookup
```

在这种情况下，`cat` 命令将特定文件的内容（正如你在 grep 示例中所知，该文件包含一些带有正则表达式的行）传递给 `lookup` 脚本。该脚本简单地应用 Perl 的正则表达式匹配运算符 (`=~`) 并打印任何匹配的行。其输出与使用以下命令时 `grep` 命令显示的内容相似：

```
grep "[Ll]inux" /usr/include/*.h
```

`lookup` 脚本中的 `$_` 变量需要一些解释。`<STDIN>` 表达式从标准输入获取一行，并默认将该行存储在 `$_` 变量中。在 while 循环内部，正则表达式与 `$_` 字符串进行匹配。以下单条 Perl 语句完成了 `lookup` 脚本的工作：

```
if ( $_ =~ /[Ll]inux/ ) { print $_; }
```

这个例子说明了如何使用正则表达式搜索文件中字符串的出现。

使用正则表达式一段时间后，你会更好地欣赏它们的功能。诀窍在于找到执行你想要任务的正则表达式。例如，这里有一个搜索，它查找所有恰好以七个空格开头并以右括号结尾的行：

```perl
while (<STDIN>)
{
    if ( $_ =~ /^\s{7}\S/ ) { print $_; }
}
```

###### 流程控制语句

到目前为止，你已经看到了旨在按顺序逐个执行的 Perl 语句。Perl 还包括一些允许你控制语句执行流程的语句。你已经看到了 `if` 语句和一个 `while` 循环。Perl 包含了一套完整的流程控制语句，就像 C 语言中的那样，但有一些额外的功能。

在 Perl 中，所有条件语句都采取以下形式：

```
条件语句
{ 如果条件为真则执行的 Perl 代码 }
```

请注意，你必须用大括号 ( ... ) 括住跟在条件语句后面的代码。条件语句检查表达式的值，以确定是否执行大括号内的代码。在 Perl 中，与 C 语言一样，任何非零值都被视为逻辑真，而零值为假。

接下来，我简要描述 Perl 中主要条件语句的语法。

####### if 和 unless

Perl 的 `if` 语句类似于 C 的 `if` 语句。例如，`if` 语句可以检查计数是否超过阈值，如下所示：

```perl
if ( $count > 25 ) { print "Too many errors!\n"; }
```

你可以像这样向 `if` 语句添加一个 `else` 子句：

```perl
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

如果你了解 C，你会发现 Perl 的语法看起来与 C 非常相似。带有 `if` 语句的条件可以有零个或多个 `elsif` 子句，以考虑更多替代方案，如下所示：

```perl
print "Enter version number:"; # 提示用户输入版本号
$os_version = <STDIN>;         # 从标准输入读取
chop $os_version; # 去掉行尾的换行符
# 检查版本号
if ($os_version >= 10 ) { print "No upgrade necessary\n";}
elsif ($os_version >= 6 && $os_version < 5) { print "Standard upgrade\n";}
else { print "Sorry, cannot upgrade!\n";}
```

`unless` 语句是 Perl 独有的。该语句的形式与 `if` 相同，包括使用 `elsif` 和 `else` 子句。区别在于，`unless` 仅在条件为假时执行其语句块。例如，你可以在以下代码中使用 `unless`：

```perl
unless ($user eq "root")
{
       print "You must be \"root\" to run this program.\n";
       exit;
}
```

在这种情况下，如果字符串 `$user` 不是 `root`，脚本就会退出。

####### while

使用 Perl 的 `while` 语句进行*循环*——即重复处理，直到现有条件在逻辑上变为假。要从标准输入逐行读取并处理该行，你可以使用以下 `while` 循环：

```perl
while ($in = <STDIN>)
{
# 处理该行的代码
    print $in;
}
```

如果你不带任何参数从标准输入读取，Perl 会将当前标准输入行赋值给 `$_` 变量。因此，你可以将前面的 `while` 循环写成如下形式：

```perl
while (<STDIN>)
{
# 处理该行的代码
    print $_;
}
```




####### while 语句

Perl 的 while 语句比 C 语言的更通用，因为几乎可以使用任何内容作为要测试的条件。例如，如果使用数组作为条件，while 循环会执行到数组中没有任何元素为止，如下面的示例所示：

```perl
# Assume @cmd_arg has the current set of command arguments
while (@cmd_arg)
{
    $arg = shift @cmd_arg; # this extracts one argument
    # Code to process the current argument
    print $arg;
}
```

shift 函数移除数组的第一个元素并返回该元素。

你可以使用 **next** 关键字跳过循环的当前迭代进入下一次迭代；**last** 关键字则退出循环。例如，下面的 while 循环对 1 到 10 的数字求和，但跳过了 5：

```perl
while (1)
{
    $i++;
    if($i == 5) { next;} # Jump to the next iteration if $i is 5
    if($i > 10) { last;} # When $i exceeds 10, end the loop
    $sum += $i;       # Add the numbers
}
# At this point $sum should be 50
```

####### for 和 foreach

Perl 和 C 的 for 语句语法相似。使用 for 语句可以根据表达式的值执行语句任意次数。语法如下：

```perl
for (expr_1; expr_2; expr_3) { statement block }
```

*expr_1* 在循环开始时评估一次；语句块执行直到 *expr_2* 的值为零。第三个表达式 *expr_3* 在语句块每次执行后评估。你可以省略任何表达式，但必须包含分号。此外，语句块周围的大括号是必需的。下面是一个使用 *for* 循环将 1 到 10 的数字相加的示例：

```perl
for ($i=0, $sum=0; $i <= 10; $sum += $i, $i++) { }
```

在这个示例中，相加数字的实际工作是在第三个表达式中完成的，而 *for* 循环控制的语句是一个空块 ( {})。

`foreach` 语句最适合用于数组。以下是语法：

```perl
foreach Variable (Array) { statement block }
```

`foreach` 语句将 *Array* 中的一个元素赋值给 *Variable* 并执行语句块。`foreach` 语句重复此过程，直到没有数组元素剩余。下面的 `foreach` 语句将 1 到 10 的数字相加：

```perl
foreach $i (1..10) { $sum += $i;}
```

注意，我使用范围运算符 (`..`) 声明数组。你也可以使用逗号分隔的项列表作为数组。

![](img/11709a8f88c8cd03868a929dc94c0e2b_783_0.png)

如果你省略 `foreach` 语句中的 *Variable*，Perl 会隐式使用 `$_` 变量来保存当前数组元素。因此你可以使用以下代码：

```perl
foreach (1..10) { $sum += $_;}
```

####### `goto`

`goto` 语句使 Perl 跳转到由标签标识的语句。这里有一个示例，它提示用户输入值，如果值不可接受则重复请求：

```perl
ReEnter:   print "Enter offset: ";
   $offset = <STDIN>;
   chop $offset;
   unless ($offset > 0 && $offset < 512)
   {
       print "Bad offset: $offset\n";
       goto ReEnter;
   }
```

###### 访问 Linux 命令

你可以以多种方式从 Perl 中执行任何 Linux 命令：

- 调用 `system` 函数，使用包含要执行的 Linux 命令的字符串。
- 将 Linux 命令包含在反引号 (``) 中，这也称为 *grave accents*。你可以通过这种方式运行 Linux 命令并捕获其输出。
- 调用 `fork` 函数以复制当前脚本，并在子进程中处理新命令。（如果一个进程启动了另一个进程，新进程被称为 *child* 进程。）
- 调用 exec 函数用新脚本或 Linux 命令覆盖当前脚本。
- 使用 fork 和 exec 来提供类似 shell 的行为。（监控用户输入并通过子进程处理每个用户输入的命令。）

在本节中，我将展示一个如何实现此任务的简单示例。

在脚本中执行 Linux 命令的最简单方法是使用 system 函数并将命令放在字符串中。在 system 函数返回后，命令的退出代码位于 $? 变量中。你可以轻松编写一个简单的 Perl 脚本，该脚本从标准输入读取字符串并使用 system 函数处理该字符串。请遵循以下步骤：

1. 使用文本编辑器输入并将以下脚本保存为名为 rcmd.pl 的文件：

```perl
#!/usr/bin/perl
# Read user input and process command
$prompt = "Command (\"exit\" to quit)"; 
print $prompt;

while (<STDIN>)
{
        chomp;
        if ($_ eq "exit") { exit 0;}

        # Execute command by calling system
        system $_;
        unless ($? == 0) {print "Error executing: $_\n";}
        print $prompt;
}
```

2. 使用以下命令使 rcmd.pl 文件可执行：
   ```bash
   chmod +x rcmd.pl
   ```

3. 在 shell 提示符下键入 `./rcmd.pl` 来运行脚本。

以下是 rcmd.pl 脚本的一个示例输出。（输出取决于你输入的命令）

```text
Command ("exit" to quit): ps
  PID TTY          TIME CMD
 3128 pts/2    00:00:00 bash
 3314 pts/2    00:00:00 rcmd.pl
 3315 pts/2    00:00:00 ps
Command ("exit" to quit): exit
```

你可以在 Perl 脚本中使用 fork 和 exec 来运行 Linux 命令。以下是一个使用 fork 和 exec 执行用户输入命令的示例脚本 — psh.pl：

```perl
#!/usr/bin/perl
# This is a simple script that uses "fork" and "exec" to
# run a command entered by the user
$prompt = "Command (\"exit\" to quit): ";
print $prompt;

while (<STDIN>)
{
    chomp;     # remove trailing newline
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

以下示例输出展示了 psh.pl 脚本如何执行 ps 命令：

```text
Command ("exit" to quit): ps
    PID TTY          TIME CMD
    3128 pts/2    00:00:00 bash
    3321 pts/2    00:00:00 psh.pl
    3322 pts/2    00:00:00 ps
Command ("exit" to quit): exit
```

Shell（如 bash）使用 fork 和 exec 组合来运行命令。

###### 文件访问

你可能已经注意到本章各个示例中使用的 `<STDIN>` 表达式。这是 Perl 从文件读取的方式。在 Perl 中，*文件句柄*，也称为 *标识符*，在读取文件时赋予文件独特的身份。通常，文件句柄使用大写字母。**STDIN** 是预定义的文件句柄，表示标准输入 — 默认情况下是键盘。**STDOUT** 和 **STDERR** 是另外两个预定义的文件句柄。**STDOUT** 用于打印到终端，而 **STDERR** 用于打印错误消息。

![](img/11709a8f88c8cd03868a929dc94c0e2b_785_0.png)

要从文件读取，请将文件句柄写在尖括号 (< >) 内。因此，`<STDIN>` 从标准输入读取一行。

你可以使用 open 函数打开其他文件。以下示例展示了如何打开 /etc/passwd 文件进行读取以及如何显示该文件中的行：

```perl
open (PWDFILE, "/etc/passwd"); # PWDFILE is the file handle
while (<PWDFILE>) { print $_;} # By default, input line is in $_
close PWDFILE;           # Close the file
```

默认情况下，open 函数以读取模式打开文件。你可以在文件名开头添加特殊字符来指示其他类型的访问。`>` 前缀以写入模式打开文件，而 `>>` 前缀以追加模式打开文件。下面是一个简短的脚本，它读取 /etc/passwd 文件并创建一个名为 output 的新文件，其中列出了所有没有实际 shell 的用户。（这些用户的密码条目在每行末尾都有 :/bin/false。）

```perl
#!/usr/bin/perl
# Read /etc/passwd and create list of users without any
# shell

open (PWDFILE, "/etc/passwd");
open (RESULT, ">output");    # open file for writing
while (<PWDFILE>)
{
	if ($_ =~ /\/bin\/false\n/) {print RESULT $_;}
}
close PWDFILE;
close RESULT;
```

执行此脚本后，你会在当前目录中找到一个名为 output 的文件。

# 带有管道前缀的文件名

一个有趣的文件名前缀是管道字符 — 竖线 (|)。如果你调用 open 并使用以 | 开头的文件名，文件名的其余部分将被视为命令。Perl 解释器执行该命令，你可以使用 print 调用向此命令发送输入。下面的 Perl 脚本使用 mail 命令向用户列表发送电子邮件：

```perl
#!/usr/bin/perl
# Send mail to a list of users
foreach ("root", "naba")
{
    open (MAILPIPE, "| mail -s Greetings");
    print MAILPIPE "Remember to send in your weekly report today!\n";
    close MAILPIPE;
}
```

如果文件名以管道字符 (|) 结尾，该文件名将作为命令执行；你可以使用尖括号 (<...>) 读取该命令的输出，如下面的示例所示：

Book VII  Chapter 4  Programming in Perl


```
open ($PSPIPE, "ps ax | ");
while (<$PSPIPE>)
{
    # Process the output of the ps command
    # This example simply echoes each line
    print $_;
}
```

###### 子例程

虽然 Perl 包含大量内置函数，但你可以通过*子例程*的形式添加自己的代码模块。实际上，Perl 自带了许多这类“程序中的程序”。以下是一个简单的脚本，展示了 Perl 中子例程的语法：

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
&hello($a, $b);    # Call the subroutine
```

当你运行上述脚本时，它会显示以下输出：

```
Hello, Jane Doe
```

请注意关于子例程的以下几点：

- 子例程通过数组 `@_`（@ 符号，后跟一个下划线字符）接收其参数。
- 在子例程中使用的变量默认是全局的。使用 `local` 函数来创建一组局部变量。
- 通过在名称前加 & 符号调用子例程。因此，通过输入 `&hello` 来调用子例程 `hello`。

如果需要，你可以将子例程放入其单独的文件中。例如，`hello` 子例程可以存放在名为 `hello.pl` 的文件中。将子例程放入文件中时，请记得在文件末尾添加一个返回值——只需在末尾*输入* `1;` 以返回 `1`。因此，`hello.pl` 文件看起来如下：

```
sub hello
{
    # Make local copies of the arguments from the @_ array
    local ($first,$last) = @_;
    print "Hello, $first $last\n";
}
1;     # return value
```

然后，你必须编写使用 **hello** 子例程的脚本，如下所示：

```
#!/usr/bin/perl
require 'hello.pl';  # include the file with the subroutine
$a = Jane;
$b = Doe;
&hello($a, $b);     # Call the subroutine
```

该脚本使用 **require** 函数包含包含 **hello** 子例程定义的 *hello.pl* 文件。

###### Perl 中的内置函数

*Perl* 拥有近 200 个内置函数（也称为 *Perl* 函数），包括类似 C 运行时库中的函数，以及访问操作系统的函数。你确实需要浏览函数列表，才能领略 *Perl* 中可用功能的广度。我在这本书中没有足够的空间来涵盖这些函数，但你可以通过将 Web 浏览器指向以下地址来了解 *Perl* 内置函数：

`http://perldoc.perl.org/index-functions.html`

该地址将连接你到 *Perl* 文档站点的 *Perl* 函数页面，使你可以浏览 *Perl* 内置函数的概述。在该页面上，点击函数名称即可查看关于该函数的更详细信息。

###### 理解 Perl 包和模块

*Perl* 包是将数据组合在一起的子例程的一种方法。本质上，它是使用变量和子例程名称而不与程序其他部分使用的名称冲突的一种方式。自 *Perl* 版本 4 起，包的概念就已经存在。

包提供了一种控制**命名空间**的方法——该术语指变量和子例程名称的集合。你可能没有意识到，当你编写 *Perl* 程序时，它自动属于名为 **main** 的包。除了 **main**，其他 *Perl* 包位于 *Perl* 库中（在你的 Linux 系统的 `/usr/lib/perl5` 目录中），你还可以定义自己的包。

*Perl* **模块**是遵循特定准则的包。

####### Perl 包

你可以将 Perl 包视为组织一组相关 Perl 子例程的便捷方式。另一个好处是，在包中定义的变量和子例程名称不会与程序其他地方使用的名称冲突。因此，一个包中名为 `$count` 的变量仅对该包是唯一的，并且不会与 Perl 程序其他地方使用的 `$count` 冲突。

Perl 包在一个单个文件中。包语句在文件开头使用，以将文件声明为包并为包命名。例如，文件 *ctime.pl* 在名为 *ctime* 的包中定义了一系列子例程和变量。*ctime.pl* 文件在多个位置有以下包语句：

```
package ctime;
```

此包声明的效果是，所有后续的变量名称和子例程名称都被视为在 *ctime* 包中。你可以将这样的包语句放在实现该包的文件开头。

如果你实现了一个包，并且需要引用另一个包中的子例程或变量怎么办？正如你可能猜到的，你只需指定包名称和变量（或子例程）名称即可。Perl 提供了以下语法来引用其他包中的变量：

```
$Package::Variable
```

这里 *Package* 是包名称，*Variable* 是该包中变量的名称。如果你省略包名称，Perl 假设你指的是 *main* 包中的变量。请注意 C++ 恰好在引用其他 C++ 类中的变量时使用类似的语法。（类基本上是数据和函数的集合——对象的模板。）

要在程序中使用包，你只需调用 `require` 函数，并将包文件名作为参数。例如，名为 *ctime* 的包在文件 *ctime.pl* 中定义。该包包含 *ctime* 子例程，它将二进制时间转换为字符串。以下简单程序使用 *ctime.pl* 文件中的 *ctime* 包：

```
#!/usr/bin/perl -w
# Use the ctime package defined in ctime.pl file
require 'ctime.pl';
# Call the ctime subroutine
$Time = ctime(ctime());
# Print the time string
print $Time;
```

如你所见，此程序使用 *require* 函数将 *ctime.pl* 文件引入程序。当你运行此程序时，它会打印当前日期和时间，格式如下所示的示例输出：

```
Sat Sep 3 19:04:34 2005
```

请注意此脚本的第一行使用了 *-w* 选项。该选项导致 Perl 解释器打印有关 Perl 脚本中任何不良结构的警告消息。在调用 Perl 解释器的行中包含 *-w* 选项是个好主意。

如果你想在不实际运行程序的情况下检查 Perl 程序的语法，请使用 *-c* 选项运行 Perl 解释器，就像这样。（*filename* 是你想检查其语法的 Perl 程序的名称。）

```
perl -c filename
```

####### Perl 模块

Perl 5 将包的概念向前推进了一步，引入了*模块*，这是一种遵循特定准则并旨在可重用的包。每个模块都是一个包，它定义在与包名称相同但带有 *.pm* 扩展名的文件中。每个 Perl 对象都实现为一个模块。例如，CGI 对象（用于 Web 服务器）实现为 CGI 模块，存储在名为 *CGI.pm* 的文件中。

如今，Perl 附带了许多模块。你会在 */usr/lib/perl5* 目录以及 */usr/share/perl/x.y.z*（其中 *x.y.z* 是 Perl 版本号）中找到这些模块。在这些目录中，查找以 *.pm*（代表*Perl 模块*）结尾的文件名。

####### 使用模块

你可以调用 *require* 函数或 *use* 函数，将 Perl 模块包含到你的程序中。例如，名为 *Cwd* 的 Perl 模块（如预期定义在 *Cwd.pm* 文件中）提供了一个 *getcwd* 子例程，该子例程返回当前目录。你可以调用 *require* 函数来包含 *Cwd* 模块并调用 *getcwd*，如下所示：

```
require Cwd; # You do not need the full filename
$curdir = Cwd::getcwd();
print "Current directory = $curdir\n";
```

第一行将 *Cwd.pm* 文件引入此程序——你不需要指定完整文件名；*require* 函数自动在模块名称后添加 *.pm* 以确定要包含的文件。第二行展示了如何调用 *Cwd* 模块中的子例程。当你使用


# 766

###### 在 Perl 中使用的对象

当你使用 `require` 来包含一个模块时，你必须使用 `Module::subroutine` 格式调用每个子程序。

如果你用 `use` 函数替换 `require` 来重写这个示例程序，它的形式如下：

```perl
use Cwd;
$curdir = getcwd(); # 不需要 Cwd:: 前缀
print "Current directory = $curdir\n";
```

最显著的区别是，你不再需要用模块名前缀（例如 `Cwd::`）来限定子程序名称。

你可以调用 `require` 或 `use` 来在程序中引入一个模块。只是在使用这些函数时，请记住以下几点细微差别：

-   当你通过调用 `require` 来引入模块时，该模块仅在程序运行期间调用 `require` 函数时才会被引入。你必须使用 `Module::subroutine` 语法来调用通过 `require` 函数引入的模块中的任何子程序。
-   当你通过调用 `use` 来引入模块时，该模块在 `use` 语句被处理时就会立即引入到程序中。因此，你可以像调用程序自身的一部分一样调用模块中的子程序和变量。你不需要用 `Module::` 前缀来限定子程序和变量名称。

![](img/11709a8f88c8cd03868a929dc94c0e2b_791_0.png)

你可能希望坚持使用 `use Module;` 语法来在程序中引入模块，因为这种语法在你调用模块中的子程序时允许你使用更简单的语法。

###### 在 Perl 中使用的对象

对象是一个数据结构以及操作该数据的功能的组合。每个对象都是定义对象类型的某个类的一个实例。例如，一个矩形类可能包含矩形的四个角作为数据，具有计算矩形面积的功能，以及另一个绘制矩形的功能。然后，每个矩形对象都可以是矩形类的一个实例，每个角的坐标都不同。从这个意义上说，对象是类的实例。

实现对象数据操作的函数（或子程序）被称为方法。这是借用自 Smalltalk 的术语，Smalltalk 是最早期的面向对象编程语言之一。

类还暗示了继承的概念。你可以通过扩展现有类的数据或方法（或两者兼有）来定义新类的对象。继承的一种常见用途是表达不同对象类之间的“是一种（IS A）”关系。以几何图形为例。因为圆形是一种形状，矩形也是一种形状，你可以说圆形类和矩形类继承自形状类。在这种情况下，形状类被称为*父类或基类*。

![](img/11709a8f88c8cd03868a929dc94c0e2b_792_0.png)

*面向对象编程*的基本思想是，你可以将对象的数据及其相关方法（子程序）封装起来，使其像一个*黑盒*一样工作——输入产生输出，而你无需指定完成工作的每个细节。程序员仅通过公开的方法访问对象，而不必了解方法的内部机制。通常，程序员可以创建一个对象，调用其方法来获取或设置属性（这是对象数据的另一个名称），并销毁对象。在本节中，我将向你展示如何在 Perl 中使用对象。有了这些知识，你可以将对象作为构建 Perl 程序的构建块加以利用。

####### 理解 Perl 对象

Perl 通过使用模块来实现对象，这些模块将数据和子程序封装在一个文件中。Perl 提出了对象的以下简单模型：

-   一个*对象*由一个引用表示。（对象实现为对哈希的引用。）
-   一个*类*是一个 Perl 模块，它提供用于处理对象的方法。
-   一个*方法*是一个 Perl 子程序，它期望第一个参数是对象引用。

对象实现者必须遵循某些规则，并在代表类的模块中提供某些方法。然而，要在 Perl 程序中使用对象，你真的不需要知道太多关于对象实现的信息。从实用角度来看，你只需要知道使用对象时必须遵循的步骤。

####### 创建和访问 Perl 对象

一个特别有用的 Perl 对象是 `Shell` 对象，它由 Perl 模块 `Shell.pm` 实现。该模块随 Perl 发行版提供，并位于 `/usr/share/perl/5.8.6` 目录中（针对 Perl 版本 5.8.6）。

顾名思义，`Shell` 对象旨在从 Perl 脚本内部运行 shell 命令。你可以创建一个 `Shell` 对象并让它执行命令。

要使用 Shell 对象，请遵循以下通用步骤：

1.  **放置以下行以在程序中包含 Shell 模块：**
    ```perl
    use Shell;
    ```
    你必须在创建 Shell 对象之前包含此行。

2.  **要创建一个 Shell 对象，使用以下语法：**
    ```perl
    my $sh = Shell->new;
    ```
    其中 `$sh` 是 Shell 对象的引用。

3.  **使用 Shell 对象运行 Linux 命令，并通过保存到合适的变量来捕获任何输出。例如，要将 `/usr/share/perl/5.8.6` 目录的目录列表保存在名为 @modules 的数组中，请编写以下内容：**
    ```perl
    @modules = $sh->ls("/usr/lib/perl/5.8.6/*\.pm");
    ```
    然后你可以按任何想的方式处理这个 Perl 模块文件名的数组（这就是 *.pm 文件的内容）。例如，要简单地遍历数组并打印每个字符串，使用以下 while 循环：
    ```perl
    while(@modules)
    {
        $mod = shift @modules;
        # 对模块名称执行任何你想做的操作
        print $mod;
    }
    ```

你如何知道调用哪些方法以及以什么顺序调用它们？在使用对象之前，你必须阅读对象的文档。方法名称和方法调用的顺序取决于对象的作用。

###### 使用 English 模块

Perl 包含几个名称奇特的特殊变量，例如 `$_`（用于默认参数）和 `$!`（用于对应最后一个错误的错误消息）。阅读程序时，猜测特殊变量的含义可能很困难。结果是你最终可能会避免使用本可以很有用的特殊变量。

作为一种有益的功能，Perl 5 提供了 English 模块（`English.pm`），它允许你为 Perl 中的各种特殊变量使用可理解的名词。要使用 English 模块，在 Perl 程序中包含以下行：

```perl
use English;
```

之后，你可以将 `$_` 称为 `$ARG`，将 `$!` 称为 `$ERRNO`。（这些*English* 名称可能仍然有点晦涩，但肯定比标点符号好得多。）

以下程序使用了 English 模块——并打印了几个有趣的变量：

```perl
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

当我运行此脚本时，得到的输出如下：

```
Perl executable = /usr/bin/perl
Script name = ./english.pl
```

English 模块很实用，因为它允许你编写 Perl 脚本，其中你可以通过有意义的名词引用特殊变量。要了解有关 Perl 特殊变量及其 English 名称的更多信息，请在终端窗口中输入 **man perlvar**——或者，更好的做法是将 Web 浏览器指向 *perldoc.perl.org/perlvar.html*。

## 附录：关于 DVD

**本附录内容**

-   系统要求
-   DVD 安装说明
-   DVD 上有什么
-   故障排除

本书的配套 DVD 包括七个主要的 Linux 发行版——Debian GNU/Linux、Fedora Core、Knoppix、MEPIS、SUSE、Ubuntu 和 Xandros Desktop OS——让你开始你的 Linux 之旅。本附录简要介绍了 DVD 并告诉你如何开始安装。

### 系统要求

确保你的计算机满足以下列表中的最低系统要求。如果你的计算机不满足这些要求中的大多数，你可能在使用 DVD 上的软件和文件时会遇到问题：

-   一台 PC，处理器运行频率为 400 MHz 或更高，用于图形安装
-   计算机上至少安装 192MB 总内存用于图形安装（推荐 256MB）
-   硬驱上至少 520MB 可用空间用于最小安装；如果你计划安装大多数包，则推荐 5GB 可用空间，以便你可以尝试本书中介绍的所有内容
-   一个 DVD-ROM 驱动器和一个 CD 刻录机（有关刻录安装 CD 的说明，请参见 Book I，Chapter 2）
-   一个图形卡和监视器，能够显示至少 256 种颜色
-   一个声卡
-   以太网网卡（NIC）或速度至少为 56 Kbps 的调制解调器





### DVD 安装说明

要从随书附赠的 DVD 安装 Linux 发行版，请遵循以下步骤。（详情请参阅第一卷第二章。）

- 1. 在安装 Linux 之前，先收集有关你电脑硬件的信息，例如显卡、网卡和 SCSI 卡。

- 2. 使用分区程序（如 PartitionMagic 或 FIPS 程序）在硬盘上为 Linux 腾出空间。

如果你计划将 Linux 作为电脑的唯一操作系统，或者计划将其安装在一个空的第二块硬盘上，则跳过此步骤。

- 3. 为你的发行版刻录 CD。（如果你正在安装 Fedora Core，请跳过此步骤。）

各发行版的具体说明，请参阅第一卷第二章。

- 4. 使用 DVD（适用于 Fedora Core 和 Knoppix）或第一张 CD（适用于 Debian、MEPIS、SUSE、Ubuntu 和 Xandros）启动你的电脑。

Knoppix 是一个 Live CD（即时启动光盘）发行版，因此此步骤应为你呈现 Knoppix 桌面。对于其他发行版，此步骤将运行该发行版的安装程序。从这一点开始，随着安装程序引导你完成各个步骤，请回答出现的问题并做出选择。以下是一些典型的安装步骤：

- 为 Linux 准备硬盘分区。如果你通过缩小现有 Windows 分区的大小来腾出空间，此步骤允许你创建 Linux 分区。
- 配置以太网网络（如果有）。通常，你通过使用 DHCP 自动配置网络。
- 指定本地时区并设置 `root` 密码。
- 在硬盘上安装引导加载程序，以便你在关机后再启动电脑时能够引导 Linux。
- 选择你要安装的具体软件包，例如 X 窗口系统和 GNOME 或 KDE 图形桌面。

#### DVD 中包含的内容

本节概述了你在 DVD 上找到的软件及其他资源。如果你在安装 DVD 上提供的物品时遇到困难，请回顾前一节中的安装说明。

![](img/11709a8f88c8cd03868a929dc94c0e2b_798_0.png)

*共享软件*是受版权保护程序的完全功能、免费试用版本。如果你喜欢某些程序，可以支付少量费用向作者注册，从而获得许可证、增强版本和技术支持。

*免费软件*是免费、受版权保护的游戏、应用程序和实用工具。你可以将它们复制到任意数量的 PC 上——免费——但它们不提供技术支持。

软件的*试用版、演示版或评估版*通常受到时间或功能限制（例如，不允许你在创建项目后保存项目）。

*GNU 软件*由其自身的许可证管理，该许可证包含在 GNU 软件的文件夹中。GNU 软件的分发没有限制。有关详情，请参阅 DVD 根目录或本书封底的 GNU 许可证。根据 GNU 许可证的要求，本书包含 Fedora Core 的源代码。至于 Debian、Knoppix、SUSE 和 Xandros 的源代码，以下是从互联网获取每个应用程序源代码的方法：

- **Debian**：访问 www.debian.org/mirror/list 上的镜像站点列表，并点击离你最近的站点的 URL。站点加载后，进入 pool 目录，然后在 main、contrib 和 non-free 三个目录之一中查找源代码文件。这些文件根据包名称的首字母进一步组织在单独的目录中。例如，sendmail 包的源代码位于 s 目录中。（有关 pool 目录的更多信息，请参阅 www.debian.org/doc/FAQ/ch-ftarchives.en.html#s-pools。）

- **Knoppix**：Knoppix 的许多包来自 Debian 项目，其源代码可从 Debian 网站获取。（有关下载 Debian 源代码的信息，请参阅上一条。）从 www.knopper.net/download/knoppix 下载 Knoppix 特有的源代码。

- **MEPIS**：MEPIS 中的大多数包来自 Debian 项目，其源代码可从 Debian 网站获取。（有关下载 Debian 源代码的信息，请参阅 Debian 的描述。）MEPIS 独有的组件，如 MEPIS OS Center，属于专有软件，其源代码不可公开获取。

- **SUSE**：从 http://ftp.opensuse.org/pub/opensuse/distribution/SL-OSS-stable/inst-source/suse/src/ 服务器下载 SUSE Linux 的源代码包。

- **Ubuntu**：你可以在 http://archive.ubuntu.com/ubuntu/ 找到 Ubuntu 的源代码，其组织方式与 Debian 源代码类似（请参阅 Debian 的描述）。在运行 Ubuntu 时，你可以通过输入以下命令来下载某个包的源代码：先输入 **sudo apt-get build-dep packagename**，然后输入 **sudo apt-get source packagename**，其中 *packagename* 是包的名称。例如，要下载 **samba** 包的源代码，请输入 **sudo apt-get build-dep samba**，然后输入 **sudo apt-get source samba**。

- **Xandros**：按照 www.xandros.com/support/source_code.html 上的说明，下载 Xandros 免费和开源组件的源代码。

如果你希望将源代码邮寄给你，请填写并寄回本书封底附带的优惠券。

DVD 包含多种不同格式的 Linux 发行版：

- **完整发行版**：你可以从 DVD 启动并安装完整发行版。对于完整发行版，除了从 DVD 启动外，你不需要做任何特别的事。然后你可以直接开始安装 Linux 发行版。

- **即插即用 Live CD**：你可以从 DVD 启动电脑来启动 Live CD。启动即插即用 Live CD 后，你应该会得到一个 Linux GUI 桌面，你可以立即开始使用，而无需在硬盘上安装任何内容。

- **ISO 镜像**：你必须从 ISO 镜像刻录 CD，然后从 CD 安装。虽然你可以自己下载 ISO 镜像，但文件非常大——每个 ISO 镜像约为 700MB——而 DVD 上已包含它们，省去了从互联网下载巨大文件的麻烦。部分 ISO 镜像是 Live CD 镜像。从 Live CD ISO 刻录 CD 后，你可以从 CD 启动并获取 Linux 系统，而无需在硬盘上安装任何内容。

以下是 DVD 包含的 Linux 发行版：

- **Debian**：以网络安装 ISO 镜像的形式提供。刻录 CD 后，你就可以准备通过互联网上的服务器通过网络安装 Debian（执行此安装需要互联网连接）。

- **Fedora Core**：作为完整发行版包含在内。只需从 DVD 启动，即可获得安装 Fedora Core 的选项。使用图形安装程序完成安装步骤。

- **Knoppix**：作为即插即用 Live CD 包含在内。从 DVD 启动后，你将获得启动 Knoppix 的选项。启动后，你将获得 Knoppix 桌面，而无需在硬盘上安装任何内容。

- **MEPIS**：以 Live CD ISO 镜像提供，该镜像也可用作安装 CD。刻录 CD 并从中启动以试用 MEPIS。你也可以直接从同一张 CD 继续安装。

- **SUSE**：以单个 Live DVD ISO 镜像文件提供。将 ISO 文件刻录到 DVD，然后从 DVD 启动，即可直接从 DVD 运行 SUSE Linux。（DVD 上的空间有限，无法提供完整的 SUSE Linux 发行版。要下载完整的 SUSE Linux 发行版，请访问 http://ftp.opensuse.org/pub/opensuse/distribution/SLE-OSS-stable/。）

- **Ubuntu**：以单个安装 CD ISO 镜像提供。刻录 CD 并从中启动以开始安装。

- **Xandros Open Circulation Edition**：以单个 CD ISO 镜像提供。刻录 CD，然后安装 Xandros。

每个 Linux 发行版的详细软件列表略有不同，但大多数发行版都包含以下内容（显示典型版本号）：

- 带有主要 PC 硬件配置驱动模块的 Linux 内核 2.6.x，包括 IDE/ATA 和 SCSI 驱动器、PCMCIA 设备、CD 驱动器和 DVD 驱动器
- 用于设置设备和服务的完整安装和配置工具集
- 基于 X 窗口系统的图形用户界面，配有 GNOME 2.12 和 KDE 3.4 图形桌面
- 用于互联网、局域网和内部网的完整 TCP/IP 网络功能
- 用于使用 PPP、DSL 或拨号串行通信程序将你的 PC 连接到你的互联网服务提供商 (ISP) 的工具
- 完整的互联网应用程序套件，包括电子邮件 (sendmail, mail)、新闻组 (INN)、TELNET、FTP、DNS 和 NPS
- Xiaman Evolution 或等效的电子邮件和日历应用程序
- 带有文字处理器、电子表格、演示软件等的 OpenOffice.org 1.9 办公套件
- Apache Web 服务器（将你的 PC 变成 Web 服务器）和 Mozilla Firefox Web 浏览器（用于浏览网络）
- Samba 3.0.20 局域网管理器软件，用于 Microsoft Windows 连接
- 几个文本编辑器（例如，GNU Emacs 21.3；vim）
- 图形和图像处理软件，如 The GIMP、Xfig、Gnuplot、Ghostscript、Ghostview 和 ImageMagick
- 编程语言（GNU C 和 C++ 4.0、Perl 5.8.7、Tcl/Tk 8.4.11、Python 2.4.1、Ruby 1.8.2、GNU AWK 3.1.4）和软件开发工具（GNU Debugger 6.3、CVS 1.12、RCS 5.7、GNU Bison 1.875、flex 2.5.4a、TIFF 和 JPEG 库）





- 支持行业标准可执行与链接格式（ELF）和英特尔二进制兼容性规范（IBCS）
- 一套完整的来自 GNU 项目的标准 UNIX 实用程序
- 访问和使用 DOS 文件及应用程序的工具（mtools 3.9.10）
- 文本格式化和排版软件（groff、TeX 和 LaTeX）

#### 故障排除

如果您在安装或使用随附 DVD 上的材料时遇到困难，请参阅第一卷中详细的安装和故障排除说明。

如果您在使用 DVD-ROM 时仍遇到问题，请致电 Wiley 产品技术支持电话：(800) 762-2974。在美国境外，请拨打 1(317) 572-3994。您也可以通过互联网在 www.wiley.com/techsupport 联系 Wiley 产品技术支持。Wiley 出版公司仅针对安装和其他一般质量控制项目提供技术支持；如需有关应用程序本身的技术支持，请咨询程序供应商或作者。

如需追加订单或获取有关其他 Wiley 产品的信息，请致电 (800) 225-5945。

## 索引

### 符号

- 星号通配符，167–168
- ! FTP 命令，368
- ? FTP 命令，368
- ?（问号）通配符，167–168

### A

- ABI（应用程序二进制接口），LSB 相关，15
- AbiWord，208
- 接入点，无线网络，292–293
- 账户，用户，系统管理，373
- acpid 互联网服务，580
- 操作菜单，Debian GNOME 桌面，142
- ADSL（非对称数字用户线路），258
- alt 新闻组，348
- amarok，209
- apache 互联网服务，580
- Apache Web 服务器
  - 访问控制指令，601–603
  - 计算机漏洞相关，551
  - 配置，589–606
  - 配置文件，593–603
  - 配置工具，590–592
  - 安装，587–588
  - 命名规范，588
  - 资源配置指令，596–600
  - 启动，588–589
  - 虚拟主机设置，603–606
- apache2 互联网服务，580
- apmd 互联网服务，580
- append FTP 命令，368
- 应用网关，508
- 应用层，TCP/IP，276
- 应用代理防火墙，537–538
- 应用程序
  - 数据库，209
  - 默认可用性，212–214
  - 图形和成像，210
  - 图形用户界面，19–21
  - 互联网，210–211
  - 多媒体，209
  - 办公应用程序，208
  - 办公工具，208
  - 文本编辑器，208
- 应用程序菜单
  - Debian GNOME 桌面，142
  - Fedora Core GNOME 桌面，145
  - Ubuntu GNOME 桌面，157
- Appware
  - 描述，21
  - 概述，220
- APT
  - DEB 文件相关，459–461
  - Debian 更新，465–466
  - MEPIS Linux 更新，465–466
  - Ubuntu Linux 更新，465–466
- 归档。另见备份
  - 相关命令，172
  - 多卷归档，438
  - 单卷归档，436–437
  - tar 程序，26, 436–441
- Arkeia 实用程序，436
- 数组变量，Perl，747, 749
- 数组，C 编程，707–708
- ascii FTP 命令，368
- Aspell，208, 222–223
- 关联数组，Perl，747, 750
- 星号 (*) 通配符，167–168
- ATA 支持，内核，483
- ATAPI 支持，内核，483
- at 互联网服务，580
- 电子邮件附件，316
- 音频 CD
  - 多媒体应用程序，228
  - 播放，230–231
- 审计，安全。另见安全审计
- 认证
  - 计算机漏洞，551
  - 安全，504, 508
- 授权，安全，504
- autocanc GNU 软件包，17
- autofs 互联网服务，580
- automake GNU 软件包，17
- 自动备份，440
- 自动化命令补全，167
- 自动化，系统管理，374

### B

- 后门，安全，508
- 备份。另见归档
  - 自动备份，440
  - 商业实用程序，435–436
  - 设备，435
  - 增量备份，440
  - 介质，434–435
  - 多卷归档，438
  - 单卷归档，436–437
  - 策略，434–435
  - 系统管理，374
  - 磁带，439–440
- Bare Metal Plus 实用程序，436
- bash GNU 软件包，17
- bash shell
  - 内置命令，739–742
  - 概述，162
  - 启动，126–127
- 堡垒主机，安全，508
- bc GNU 软件包，17
- /bin 目录，427
- binary FTP 命令，369
- BIND DNS
  - 计算机漏洞相关，551
  - Debian，642
  - Fedora Core，642
  - MEPIS，642
  - named 守护进程，643
  - 解析器库，644
  - Ubuntu，642
  - 实用程序，644–645
  - Xandros，642
- BIND 名称服务器，643
- Binutils GNU 软件包，17
- bionet 新闻组，348
- bit 新闻组，348
- biz 新闻组，348
- 块设备
  - 内核，482–483
  - 概述，402
- 博客，358–360
- BogoMIPS，112
- 启动命令，Knoppix，84–86
- /boot 目录，427
- /boot/grub 配置文件，390
  - /boot/grub/menu.lst
    - 配置文件，390
- 引导加载程序
  - Fedora Core 安装，52
  - 内核相关，112
  - 启动相关，111
  - SUSE Linux 安装，68
- 启动消息，内核启动相关，112
- 启动选项，Linux 内核，87–89
- /boot/System.map 配置文件，390
- /boot/vmlinuz 配置文件，390
- 启动
  - 定义，111
  - 从 DVD 驱动器启动，33
  - /etc/initab 文件，386–387
  - Fedora Core，113–114
  - init 进程，384–386
  - 登录屏幕，113–114
  - 启动时的网络配置，308–309
  - Ubuntu，114
  - Xandros，113–114
- break 语句，C 编程，715
- BrightStore ARcsereve Linux 备份，436
- 浏览 Windows 网络，436
  - MEPIS KDE 桌面，152
- 浏览器。另见 Web 浏览器
- BRU 实用程序，436
- 缓冲区溢出，安全，508
- 构建内核，491–492
- 构建模块，模块化内核，491–492
- 内置函数，Perl，762–763
- 刻录 CD/DVD
  - ISO 镜像相关，37–39
  - Knoppix，38–39
  - 多媒体应用程序，233–234
  - Nautilus，186–187
- 安全业务需求，501

### C

- C++，编译，680
- C 和 C++ 编译器，GCC，678–682
- C 编程
  - 数组，707–708
  - 位域，707–710
  - break 语句，715
  - case 语句，716
  - 复合语句，716
  - continue 语句，716–717
  - 声明，700
  - default 标签，717
  - 定义，700
  - do 语句，717
  - 枚举，706
  - 表达式语句，717
  - 表达式，711–713
  - 函数库，722–723
  - 函数原型，721–722
  - 函数，可变参数数量，722
  - goto 语句，718
  - 头文件，699, 722–723
  - if-else 语句，718–719
  - if 语句，718
  - 宏，704–705
  - 空语句，719
  - 运算符，711–715
  - 指针，708–709
  - 预处理器指令，701–705
  - 程序结构，699–701
  - return 语句，719
  - 共享库，724–729
  - for 语句，717–718
  - 结构体，707–710
  - switch 语句，719–720
  - 类型定义，709–710
  - 类型限定符，710
  - 联合体，707–710
  - 变量，705–706
  - void 类型，722
  - while 语句，720–721
- CA（证书颁发机构），安全，508
- 电缆调制解调器连接
  - CMTS（电缆调制解调器终止系统），263
  - 与其他连接的比较，255–256
  - 连接方法，262–267
  - 概述，255
  - 设置，264–267
  - 上行数据，262
- 布线，以太网，281–283
- 缓存名称服务器
  - /etc/named.conf 文件，647–650
  - 资源记录格式，650–653
  - 区域文件，650
- Calc，OpenOffice.org，216–217
- 计算器
  - GNO ME，219–220
  - KDE，219–220
- 日历，218–219
- case 语句，C 编程，716
- 新闻组类别，347–348
- CD/DVD 刻录选项，MEPIS KDE 桌面，153
- cd FTP 命令，369
- 随书附赠 CD
  - 刻录，32–33
  - 发行版，31–32
  - cdrecord，209
- CD。另见音频 CD
  - 刻录，多媒体应用程序，233–234
  - 刻录，Nautilus，186–187
  - 简介，25
  - 管理，103
  - SUSE Linux 安装，63–65
- 证书，安全，508
- 字符设备支持，内核，486
- 字符设备，402–403
- chkconfig 命令
  - Fedora Core，576–577
  - SUSE Linux，576–577
- chmod FTP 命令，369
- clari 新闻组，348
- 客户端/服务器模型，套接字，568
- 客户端，互联网服务，565
- 剪贴板工具
  - MEPIS KDE 桌面，153
  - SUSE Linux 桌面，155
- 时钟
  - SUSE Linux 桌面，155
  - Xandros 桌面，160
- close FTP 命令，369
- 命令补全，167
- 命令行参数，163
- 命令行选项，163
  - 描述，127
  - 编程相关，675
- 命令行 FTP 客户端，366–370
- 命令处理程序，编程，675
- 命令
  - 归档，172
  - 文件压缩，172
  - 日期和时间，173
  - depmod，404
  - 目录管理，170, 201–202
  - 目录导航，195–196
  - 磁盘空间使用，204–206
  - dmseg，112
  - dpkg，457–459
  - ed 文本编辑器，244
  - 错误消息，保存至文件，166
  - 文件管理，170, 200–201




### 命令（续）
- 文件系统管理, 173
- 查找文件, 171, 202–203
- FTP, 366–370
- grep, 163
- 帮助, 170
- 输入, 165
- insmod, 404
- iptables, 541–545
- Ksyms, 404
- lsmod, 404
- 进程管理, 172
- modinfo, 404
- modprobe, 404
- 挂载/卸载, 203–204
- mtools, 446–447
- 导航, 194–206
- 输出，保存, 165
- 所有权，更改, 199–200
- 权限, 196–198
- 权限，更改, 199–200
- 文件处理, 171
- 重复, 169
- rmmod, 404
- RPM 文件, 450
- shell 命令, 127
- su -, 382
- uptime, 395
- 用户账户
    - 管理, 416–417
- 用户管理, 172
- vi 文本编辑器, 247–249
- 通配符, 167–168
- Yum, 466–469
- 商业备份工具, 435–436
- 商业软件，办公应用, 220–222
- comp 新闻组, 348

#### 编译器
- GCC, 678–682
- 与编程, 676
- 复合语句, C 编程, 716
- 压缩文件，相关命令, 172
- 计算机，与编程, 673–674
- 计算机编程。参见 编程
- 运行 Linux 的计算机系统, 10
- 计算机漏洞
    - Apache Web 服务器, 551
        - 认证, 551
    - BIND DNS, 551
    - CVS, 551
    - 数据库, 552
    - 主机安全, 552
    - Linux 内核, 552
    - NFS（网络文件系统）, 551
    - NIS（网络信息服务）, 551
    - Open SSL（开放安全套接字层）, 551
    - 信息资源, 550
    - sendmail, 551
    - SNMP, 551
    - subversion, 551
- 串联 shell 命令, 164
- 条件指令, C, 703–704
- 机密性, 安全, 508
- 配置。另参见 TCP/IP 配置文件
    - Apache Web 服务器, 589–606
    - Fedora Core, 网络, 52–53
    - FTP 服务器, 608–612
    - INN 服务器, 628–635
    - 引言, 28
    - 内核, 476–491
    - 打印机, Debian, 90–91
    - 打印机, Fedora Core, 92–94
    - 打印机, Knoppix, 94–96
    - 打印机, MEPIS, 94–96
    - 打印机, SUSE, 97–99
    - 打印机, Ubuntu, 99–100
    - 打印机, Xandros, 100–103
    - Samba, 667–669
    - 系统配置文件, 390–392
- 配置文件
    - sendmail, 617–623
    - vsftpd 文件, 608–609
    - vsftpd.conf 文件, 609–612
- 面向连接的
    - 协议，套接字, 567
- 无连接协议，套接字, 567
- 互联网连接
    - 电缆调制解调器, 255
    - 电缆调制解调器设置, 262–267
    - 拨号网络, 255, 267–274
    - DSL（数字用户线）, 254–262
    - LAN（局域网）, 285–286
- 控制台
    - 打开, 161
    - 虚拟, 161
- const 类型限定符, C 编程, 710
- 上下文菜单
    - 桌面上下文菜单, 135–136
    - 图标上下文菜单, 136–137
- continue 语句, C 编程, 716–717

### 控制中心, MEPIS KDE 桌面, 152
### Coreutils GNU 软件包, 18
### cpio GNU 软件包, 18
### CPU（中央处理单元）, 编程, 674
### 破解者, 安全, 499, 508
### cron Internet 服务, 580
### crond Internet 服务, 580
### CrossOver Office, 21, 208, 221–222
### 内核的加密支持, 491
### CSMA/CD（载波侦听多路访问/冲突检测）, 280–281
### CVE（常见漏洞和暴露）, 计算机漏洞, 550
### CVS（并发版本系统）
- 计算机漏洞, 551
- 描述, 23

### 数据保护, 安全, 504
### 数据类型, C 编程, 705–706
### 数据库
- 构建, 224–225
- 创建空的, 225
- 设计, 225
- MySQL, 209, 223
- PostgreSQL, 209, 223
- 查询, 228
- 表，定义, 226–227
- 表，加载数据, 227–228
- 相关漏洞, 552

### 日期和时间命令, 173
### Debian GNOME 桌面, 142
### Fedora Core GNOME 桌面, 146
### Knoppix 桌面, 148
### MEPIS KDE 桌面, 153
### Ubuntu GNOME 桌面, 158
### date 命令, 175–176
### DDoS（分布式拒绝服务）, 安全, 509
### DEB 文件
- 与 APT, 459–461
- dpkg 命令, 457–458
- 文件名, 456–457

### Debian GNU/Linux 描述, 11
### GNOME 桌面, 142–144
### GUI 系统管理工具, 375
### inetd, 531
### 安装, 42–48
#### 打印机配置, 90–91
#### 软件安装, 104–106
### 独立服务器, 530
#### 文本模式安装, 82
### update-r.c_d 命令, 577–578
### 更新, 465–466
### 版本, 15
### 调试
- 与 gdb, 691–695
- 内核, 491
- 与编程, 676

### 声明
- C 编程, 700
- 变量, C 编程, 705–706

### 解密
- GPG, 526–527
- 安全, 508

### default 标签, C 编程, 717
### 定义
- C 编程, 700
- 变量, C 编程, 705–706

### delete FTP 命令, 369
### 拒绝服务, 安全, 502
### depmod 命令, 404
### Desktop Payer
- Knoppix 桌面, 147
- MEPIS KDE 桌面, 153
- SUSE Linux 桌面, 155
- Xandros Desktop, 160

### 检测，主机安全, 552
### /dev 目录, 427
### 开发环境
- CVS（并发版本系统）, 23
- 与 GNU C 编译器, 23
- 与 GNU C++ 编译器, 23
- GNU Java 编译器, 23
- 与 GNU 调试器, 23
- GNU makes 编辑器, 23
- 与 GNU make 实用程序, 23
- GNU 性能分析实用程序, 23
- Perl, 23
- Python, 23
- RCS（修订控制系统）, 23
- 共享库, 23
- Subversion, 23
- Tcl/Tk（工具命令语言和工具包）, 23

### 设备驱动程序, 401

#### 设备
- 块设备, 402
- 块设备，内核, 482–483
- 字符设备, 402–403
- 文件, 401–403
- 在文件系统上挂载, 429–430
- 命名，与 udev, 403–404
- 网络设备, 403

### DHCP（动态主机配置协议）
- 描述, 279
- Internet 服务, 570

### DIA, 208
### 拨号网络
- 连接
    - CHAP 认证, 272–274
    - 与其他连接的比较, 255–256
    - 连接方法, 267–274
    - DNS（域名服务）, 268
    - IP（互联网协议）, 268
    - 调制解调器连接, 269–270
    - 概述, 255
    - PAP 认证, 272–274
    - PPP（点对点协议）, 268
    - PPP（点对点协议）, 连接设置, 270–272
    - Winmodems, 270

### 字典, 208
### diff GNU 软件包, 18
### digiKam
- 描述, 209
- 数码相机, 229–230

### 数码相机
- digiKam, 229–230
- 多媒体应用程序, 229

### 数字签名
- GPG, 525–526
- 安全, 508

### 数字签名, 521–522
### dir FTP 命令, 369
### 目录
- 描述, 181
- 列表，命令, 196–198
- 管理，命令, 170
- 导航，命令, 195–196
- 所有权, 516
- 路径，URL, 337
- 路径名, 182
- 权限，命令, 196–198
- /proc 文件系统, 398–400
- 安全, 516–520
- 顶层, 183–184

#### 目录管理，命令, 201–202
### 禁用选项, SELinux, 57
### 向公众披露信息，安全, 502
### disconnect FTP 命令, 369
### 磁盘分区
- Fedora Core 安装, 50–51
- 安装, 31–32, 33–34
- Live CDs, 40
- SUSE Linux 安装, 68
- Windows, 调整大小, 40–42

### 磁盘性能, 396–397
### 磁盘空间，使用，命令, 204–206
### 磁盘使用, 396–397
### 磁盘, 25

### 显示配置
- 选项, Knoppix
    - 桌面, 147

### 分布式责任, DNS, 640
### 发行版
- 随书附带的 CD, 31–32
- Debian GNU, 11
- Fedora Core, 12
- Gentoo Linux, 12
- GNU 软件, 17–19
- 内核, 10
- Knoppix, 12
- Linux, 12
- LinuxPir, 12
- Live CDs, 13
- Mandriva Linux, 12
- MEPIS Linux, 12
- Slackware Linux, 13
- SUSE Linux, 13
- Ubuntu Linux, 13
- 版本号, 14–15
- Xandros 桌面操作系统, 13

### dmesg 命令, 112
### DMZ, 安全, 509
### DNS（域名系统）
- BIND, 642–645
- 缓存名称服务器配置, 647–657
- 配置，解析器, 646–647
- 分布式责任, 640
- FQDN, 642
- 分层域名, 641–642
- localhost.zone 文件, 655–656
- 名称服务器, 656–657
- 概述, 639–641
- 主名称服务器，配置, 657–659
- 解析器配置, 646–647
- 资源记录, 651–653





## 索引

- 根区域文件，653–655
- 实用程序，644–645
- 区域文件，656

- do 语句，C 语言编程，717
- 文档，在线，23–24

- 域名
  - FQDN，642
  - 层次结构，641–642
  - URL，337

- DoS（拒绝服务）
  - 攻击，499, 508

- DOS/Windows 文件系统
  - 挂载磁盘分区，441–442
  - 挂载软盘，442–443
  - \mntools，444–448

- 下载，软件，461–462
- dpkg 命令，457–459

- 驱动程序模块
  - /etc/modprobe.conf 文件，405–406
  - 加载/卸载，404–405
  - 选择，dpkg 实用程序，459

- DSL（数字用户线）
  - ADSL（非对称 DSL），258
  - 与其他连接方式的比较，255–256
  - 连接方式，256–262
  - DSL（ISDN DSL），258
  - 本地环路，256
  - 概述，254–255
  - SDSL（对称 DSL），258
  - 设置，259–262

- 双宿主主机，安全性，509

- DVD 驱动器
  - 从中启动，33
  - 安装，34

- DVD
  - 刻录，ISO 镜像，37–39
  - 简介，25
  - 管理，103

- 动态链接，共享库，23

### E

- 电子邮件
  - 附件，316
  - 分发列表，21
  - HTML 消息，316
  - 简介，253
  - MTA（邮件传输代理），314
  - MUA（邮件用户代理），314

- ed 文本编辑器
  - 命令模式，241
  - 命令，244
  - 说明，18
  - 文本输入模式，241

- Emacs GNU 软件包，18, 208
- 加密
  - GPG，526–527
  - 公钥，520–521
  - 安全性，509
- Enforcing 选项，SELinux，57
- 枚举，C 语言编程，706
- 环境变量，编程，675
- Ephyx，210, 339
- 错误消息，保存到文件，166
- /etc/apache2/httpd.conf 配置文件，390
- /etc/apt/sources.list 配置文件，390
- /etc/at.allow 配置文件，390
- /etc/at.deny 配置文件，391
- /etc/bash.bashrc 配置文件，391
- /etc/bashrc 配置文件，391
- /etc/cups/cupsd.conf 配置文件，391
- /etc 目录，427
- /etc/fonts 配置文件，391
- /etc/fstab 配置文件，391, 430–432
- /etc/group 配置文件，391, 418–419, 554
- /etc/grub.conf 配置文件，391
- /etc/host.conf 配置文件，300–301
- /etc/hosts 配置文件，300, 391
- /etc/hosts.allow 配置文件，301–302, 391
- /etc/hosts.deny 配置文件，302, 391
- /etc/httpd/conf/httpd.conf 配置文件，391
- /etc/init.d 配置文件，391
- /etc/init.d/rcS 配置文件，392
- /etc/initlab 配置文件，386–387, 391
- /etc/issue 配置文件，391
- /etc/lilo.conf 配置文件，391
- /etc/login.defs 配置文件，391
- /etc/modprobe.conf 配置文件，391, 405–406
- /etc/modules.conf 配置文件，391
- /etc/mtab 配置文件，391
- /etc/named.conf 文件，647–650
- /etc/networks 配置文件，300
- /etc/nsswitch.conf 配置文件，302–303
- /etc/passwd 配置文件，391, 417–418, 513–515, 554
- /etc/profile 配置文件，391
- /etc/profile.d 配置文件，392
- /etc/rc.d/rc.sysinit 配置文件，392
- /etc/resolv.conf 配置文件，301
- /etc/shadow 配置文件，392, 554
- /etc/shells 配置文件，392
- /etc/skel 配置文件，392
- /etc/ssh/ssh_config，OpenSSH 相关，533
- /etc/ssh/sshd_config，OpenSSH 相关，533
- /etc/sysconfig 配置文件，392
- /etc/sysctl.conf 配置文件，392
- /etc/termcap 配置文件，392
- /etc/udev 配置文件，392
- /etc/vsftpd.ftpipusers 文件，612
- /etc/vsftpd.user_list 文件，612
- /etc/X11 配置文件，392
- /etc/X11/XF86Config-4 配置文件，392
- /etc/X11/XF86Config 配置文件，392
- /etc/X11/xorg.conf 配置文件，392
- /etc/xinetd 配置文件，392
- /etc/yum.conf 配置文件，392

### 以太网

- 布线，281–283
- CSMA/CD（载波侦听多路访问/冲突检测），280–281
- 概述，280–281
- 使用原因，280
- 设置，279–283
- 无线网络。*参见* 无线以太网网络

### 进化（Evolution）

- 说明，210
- Fedora Core GNOME 桌面，146
- 概述，317–321
- Ubuntu GNOME 桌面，158
- 漏洞利用工具，安全性，509
- 导出文件系统，NFS 相关，432–433, 662–664
- 表达式语句，C 语言编程，717

### 表达式

- C 语言编程，711–713
- Perl，746, 751–752
- 编程，676
- 正则表达式，Perl，752–755

### F

### Fedora Core

- 引导加载器安装，52
- 启动，113–114
- chkconfig 命令，576–577
- 说明，12
- 磁盘分区，50–51
- 防火墙配置，56–57
- GNOME 桌面，144–146
- GUI 系统管理工具，375–376
- 安装，48–57
- 安装类型，49–50
- 键盘安装，49
- 网络配置，52–53
- 软件包，安装，54–56
- 打印机配置，92–94
- Root 密码，53–54
- Security Level Configuration 工具，540
- SELinux 配置，56–57
- 软件安装，106–107
- 独立服务器，530
- TCP/IP 网络配置，284
- 文本模式安装，82
- 时区，53
- 更新，466–469
- xinetd，531
- 文件格式，可执行文件，内核，481
- 文件管理，命令，200–201
- 文件管理器，MEPIs KDE 桌面，152
- 文件共享，NFS，661–665

### 文件系统

- 相关命令，173
- 说明，181
- 设备，挂载，429–430
- 目录，427–428
- DOS/Windows，441–444
- 导出，NFS，662–664
- 层次结构，426–428
- 简介，26
- 内核相关，489–490
- 挂载，NFS，664–665
- 挂载/卸载，系统管理相关，433–434
- NFS，26, 432–434
- 概述，425–426
- 文件传输实用程序，发行版，22

### 文件名

- DEB 文件，456–457
- 路径名相关，182
- 管道前缀，Perl，761–762
- RPM 文件，451
- URL，337

### 文件

- 设备文件，401–403
- 查找，命令，171, 202–203
- 管理，命令，170
- 所有权，422–423, 516
- 权限，更改，517
- 权限，默认，517–519
- 权限，设置用户 ID，519–520
- /proc 文件系统，398–400
- 处理，命令，171, 176–179
- 安全性，516–520
- 共享，NFS，432–434
- 系统配置文件，390–392
- 查看，Konqueror，191–193
- 过滤器，包过滤防火墙，536
- 查找文件，命令，202–203
- Findutils GNU 软件包，18
- finger GNU 软件包，18
- 指纹，521

### Firefox 网络浏览器

- 说明，210
- Fedora Core GNOME 桌面，146
- 简介，339
- Knoppix 桌面，147
- MEPIs KDE 桌面，153
- 浏览，343–344
- 用户界面，340–342
- Xandros 桌面，159

### 防火墙

- 应用代理网关防火墙，537–538
- 特征，535–536
- Fedora Core 配置，56–57
- iptables 命令，541–543
- NATs（网络地址转换），538
- 网络相关，27
- 包过滤防火墙，536
- 包过滤，启用，539–545
- 安全性，509
- 设置概述，534–536
- 状态检测防火墙，536–537

### 软盘

- 备份相关，435

### 软盘磁带驱动器，内核，486–487

### 流控制，脚本编写，736–739

### 流控制语句

- Perl，746, 755–758
- 编程相关，677

### 文件夹

- Nautilus，浏览，188–190
- 查看，Konqueror，191–193

### for 语句

- C 语言编程，717–718
- Perl，757–758

### foreach 语句，Perl，757–758

### FQDN（完全限定域名），642

### 帧缓冲，内核，488

### FTP（文件传输协议）

- 命令行 FTP 客户端，366–370
- 命令，366–370
- 说明，279
- /etc/vsftpd.ftpusers 文件，612
- /etc/vsftpd.user_list 文件，612
- 图形界面 FTP 客户端，361–366
- 互联网服务，570
- 服务器配置，608–612
- 服务器安装，607
- SUSE Linux 安装，60–63
- vsftpd 配置文件，608–612

### 功能键

- Debian 安装，44
- SUSE Linux 安装程序，64

### 函数库，722–723

### 函数原型，C 语言编程，721–722

### 函数

- 内置函数，Perl，762–763
- C 语言编程，可变数量参数，722
- Perl，746
- 编程相关，677
- Shell，脚本编写，735–736

### G

### Gaim

- 说明，210
- 概述，327–329

### gawk GNU 软件包，18

### GCC 编译器，678–682

### gcc GNU 软件包，18

### gdb GNU 软件包，18

### gdbm GNU 软件包，18

### Gentoo Linux，12

### get FTP 命令，369

### gettext GNU 软件包，18

### gFTP，210, 362–363

### Ggv，210

### ghoscript GNU 软件包，18

### Ghostview，236–237

### ghostview GNU 软件包，18

### The GIMP GNU 软件包，18, 20, 210, 234–236

### GNOME 计算器，208, 219–220

### GNOME CD 播放器，209

### GNOME Ghostview，236–237

### GNOME（GNU 对象模型环境）

- 定制，119–121
- Debian 桌面，142–144
- Fedora Core 桌面，144–146
- 简介，20
- 启动器小部件，117
- 登录，116
- 注销，121
- 菜单按钮，117–119
- 概述，115–116
- 分页小部件，117
- 面板，116–117, 137–139
- 位置菜单，118
- 系统菜单，118
- Ubuntu Linux 桌面，156–158
- 天气小部件，117

### GNU

- 许可证，695–697
- Shell，17
- 文本终端，17

#### GNU C 编译器，23

#### GNU C++，编译器，23

#### GNU C 库 GNU 软件包，18

#### Java 的 GNU C 编译器，23

#### GNU 调试器

- 说明，23
- gdb，使用其进行调试，691–695
- gdb，运行，689–690
- gdb 命令，690–691

#### GNU Emacs 编辑器，23

#### GNU 性能分析实用程序，23

#### GNU 计划，16

#### GNU 软件，软件包，17–19

#### GNUchess GNU 软件包，18

#### gnumeric GNU 软件包，18

### goto 语句，C 语言编程，718

### goto 语句，Perl，758

### GP6

- 解密，526–527
- 加密，526–527
- 密钥交换，524–525
- 密钥对生成，523
- 文件签名，525–526

### GPL（GNU 通用公共许可证），695–697

### Gpm 互联网服务，580

### GoView，210

### 图形界面 FTP 客户端

- gFTP，362–363
- 简介，361–362
- KBear，363–364
- 将网络浏览器作为 FTP 客户端，364–366

### 高级图形，内核支持，487

### 图形和成像应用程序

- Akreagor，211
- GGv，210
- The GIMP，210, 234–236
- GNOME Ghostview，236–237
- GQview，210
- KFax，210
- Kmail，211
- Konqueror，211
- Kooka，210
- KPhone，211
- KSnaphost，211
- Linphone，211
- Skye，211
- XChat，211
- Xpdf，210
- XScan，210
- xscanimage，210

### grep 命令，163

### grep GNU 软件包，19





### G

- groff GNU 软件包，19
- groups
  - 文件所有权，422-423
  - 管理，418-419
- growisofs，209
- GRUB 引导加载程序
  - Fedora Core 安装，52
  - 简介，111-112
  - 设置，493-495
- gtk+ GNU 软件包，19
- GUI 桌面
  - 常见功能，134-142
  - 上下文菜单，135-136
  - 默认，115, 133
  - GNOME，115-121
  - 图标上下文菜单，136-137
  - KDE，122-125
  - 主菜单，139-142
  - 面板，137-139
  - SUSE Linux，153-156
  - Xandros，158-160
- GUI 文件管理器
  - Konqueror，190-194
  - Nautilus 外壳，186-190
- GUI 系统管理工具
  - Debian，375
  - Fedora Core，375-376
  - Knoppix，376-377
  - MEPIS KDE，377-378
  - SUSE Linux，378-379
  - Ubuntu Linux，379-380
  - Xandros，380-381
- GUI 文本编辑器，239-240
- GUI 用户管理器，添加用户账户，414-416
- GUI 实用工具，root，382
- GUIs（图形用户界面），应用程序，19-21
- gzip GNU 软件包，19

### H

- hard drive 硬盘
  - 安装及，34
  - 编程，674
  - 存储，25
- hardware 硬件
  - DVD 驱动器，34
  - 硬盘，34
  - 安装，34-36
  - 键盘，34
  - 调制解调器，34
  - 监视器，35
  - 鼠标，35
  - 网卡，35
  - 打印机，35
  - 处理器，35
  - RAM，35
  - SCSI 控制器，35
  - 声卡，35
  - SUSE Linux，36
  - 系统管理，374
  - 显卡，35
- hash 哈希，安全，509
- hash FTP 命令，369
- hashes 哈希值，521
- header files 头文件，C 语言编程，722-723
- Help 帮助
  - Ubuntu GNOME 桌面，158
  - Xandros Desktop，160
- help 帮助，命令，170
- help FTP 命令，369
- Hide Panel option 隐藏面板选项
  - SUSE Linux 桌面，155
  - Xandros Desktop，160
- Hide panel option 隐藏面板选项，Knoppix 桌面，147
- hiding NAFS 隐藏 NAFS，538
- hierarchy of file system 文件系统层次结构，426-428
- /home 目录，428
- Home Folder 主文件夹
  - Knoppix 桌面，147
  - MEPIS KDE 桌面，152
  - SUSE Linux 桌面，155
- host addresses 主机地址，IP 地址，277
- host connectivity 主机连接，304-305
- host security 主机安全
  - 操作系统，552
  - 权限，552
- host-security tools 主机安全工具，558
- HTML (HyperText Markup Language) 超文本标记语言
  - 锚点 URL，337
  - Web 文档，334
- HTML messages HTML 消息，电子邮件，316
- HTTP (HyperText Transfer Protocol) 超文本传输协议
  - 描述，279
  - HTTP 守护进程，583
  - 互联网服务，570
  - 作为互联网标准，584
  - Web 文档，334
- httpd，22
- httpd directives Apache Web 服务器
  - 配置文件，594-596
- httpd Internet service，580
- hypertext links 超文本链接。参见 links

### I

- I/O redirection 输入/输出重定向，shell 命令，165
- I2O support 内核 I2O 支持，484-485
- I2C support 内核 I2C 支持，487
- icon context menus 图标上下文菜单，136-137
- icons 图标
  - Debian GNOME 桌面，142
  - Fedora Core GNOME 桌面，144
  - Knoppix 桌面，147
  - MEPIS KDE 桌面，150
  - SUSE Linux 桌面，154
  - Xandros Desktop，158
- IDE Zip drives 备份设备 IDE Zip 驱动器，435
- IDSL (ISDN DSL)，258
- IDSS (Intrusion Detection Systems) 入侵检测系统，558
- IEEE 1394 support 内核 IEEE 1394 支持，484
- ieee newsgroups，348
- if-else statement C 语言编程中的 if-else 语句，718–719
- if statement if 语句
  - C 语言编程，718
  - Perl，755–756
- IM clients 即时通讯客户端
  - Gaim，327–329
  - Kopete，329–331
- image FTP 命令，369
- implementation 安全实施，504–505
- Impress OpenOffice.org，217–218
- incident handling 安全事件处理，504
- incident response 事件响应，555
- incremental backups 增量备份，440
- indent GNU 软件包，19
- inetd
  - 互联网超级服务器，572–573
  - 网络安全审查，555–556
- Info Center MEPIS KDE 桌面信息中心，152
- information sharing via Internet 通过互联网共享信息，254
- init command init 命令
  - 运行级别，387–388
  - 启动/停止服务器，389
- init process init 进程
  - 启动，384–386
  - 运行级别，385
- INN server
  - 配置，628–635
  - 安装，628
  - InterNetNews，630–634
  - 启动，628–635
- inn.conf 文件，631–632
- innd，22
- innd Internet 服务，580
- input device support 内核输入设备支持，486
- insmod 命令，404
- installation 安装
  - Apache Web 服务器，587–588
  - Debian 软件，104–106
  - 磁盘分区，31–34
  - Fedora Core，48–57
  - Fedora Core 软件，106–107
  - 硬件及，34–36
  - INN 服务器，628
  - 简介，27–28
  - Live CD 发行版，33
  - 邮件服务器，613–628
  - MEPIS，57–60
  - MEPIS 软件，104–106
  - RPMs，453–454
  - Samba，666–667
  - 软件，103–104
  - SRPMs，464–465
  - SUSE Linux，60–71
  - SUSE Linux 软件，107–108
  - 文本模式，82
  - Ubuntu 软件，104–106
  - Ubuntu Linux，71–72
  - Xandros Desktop 操作系统，73–80
  - Xandros 软件，108–110
- integrity 完整性，安全，509
- in.telnetsd，22
- Internet 互联网
  - 连接，254–256
  - 电子邮件，253
  - 信息共享，254
  - 互联网服务，278–279
  - LAN 连接，285–286
  - 作为网络的网络，254
  - 新闻组，254
  - 端口号，278–279
  - 远程访问，254
  - 服务器，21–22
  - TCP/IP，277
  - Web，254
- Internet access 互联网访问，安全，504
- Internet applications 互联网应用程序
  - Akregator，211
  - Epiphany，210
  - Evolution，210
  - Firefox，210
  - Gaim，210
  - gFTP，210
  - KMail，211
  - KNode，210
  - Konqueror，211
  - Kopete，210
  - KPhone，211
  - Lipihone，211
  - Lynx，210
  - Mozilla，210
  - Pan，211
  - Skype，211
  - Thunderbird，210
  - XChat，211
- Internet servers 互联网服务器
  - httpd，22
  - innd，22
  - in.telnetsd，22
  - sendmail，22
  - sshd，22
  - 超级服务器，530–531
  - vsftpd，22
- Internet services 互联网服务
  - acpid，580
  - apache，580
  - apache2，580
  - apmd，580
  - autd，580
  - autofs，580
  - 客户端，565
  - cron，580
  - 和 DHCP，570
  - 和 FTP，570
  - gpm，580

### I

- IP addresses IP 地址
  - 点分十进制表示法，278
  - 点分四组表示法，278
- ISA bus，481

### J

- job scheduling 任务调度
  - 一次性任务，407–409
  - 定期任务，409–412

### K

- k12 newsgroups，348
- Kalfaine，209
- Kate，208
- K3b，209
- KBear，363–364
- KCalc，208
- KDE (K Desktop Environment)
  - 计算器，219–220
  - 自定义，124–125
  - 简介，20
  - Knopix，146–150
  - 注销，125
  - MEPIS 桌面，150–153
  - 面板，122
- KDE System Guard MEPIS KDE 桌面 KDE 系统护卫，152
- kernel 内核
  - ATA 支持，483
  - ATAPI 支持，483
  - 块设备，482–483
  - 引导加载程序及，112
  - 启动选项，87–89
  - 构建，491–492
  - 总线选项，481
  - 字符设备，486
  - 配置，476–491
  - 加密支持，491
  - 调试，491
  - 发行版，10
  - 可执行文件格式，481
  - 文件系统支持，489–490
  - 软盘磁带驱动器，486–487
  - 帧缓冲，488
  - 高级图形，487
  - I10 支持，484–485
  - I2C 支持，487
  - IEEE 1394 支持，484
  - 输入设备，486
  - 安装，493–495
  - ISDN 子系统支持，486
  - 可加载模块支持，479
  - 内存技术设备，481
  - MFM 支持，483
  - 模块化，475–476
  - 单片式，475–476
  - 多媒体设备支持，487
  - 本地语言支持，490
  - 网络支持，485
  - 分区类型，490
  - 即插即用支持，482
  - 端口支持，482
  - 电源管理选项，480
  - 处理器类型，479–480
  - 创建 RAM 磁盘文件，492–493
  - 重建，474–491
  - RLL 支持，483
  - SCSI 设备，484
  - 安全选项，491
  - 设置选项，479
  - 声音支持，488
  - 电话支持，486
  - USB 支持，488
  - 版本号，14
  - 漏洞，552
  - 看门狗定时器，486
- key pairs 密钥对
  - 交换密钥，524–525
  - 生成，523
- keyboard 键盘
  - Fedora Core 安装，49
  - 安装，34
  - SUSE Linux 安装，68
  - 键盘布局，Knoppix 桌面，147
- KFax，210
- KMail，325–327
- KNode，354–356
  - 描述，210
- Knode 新闻阅读器，350
- Knoqueror Web 浏览器，Knoppix 桌面，147
- Knoppix
  - 启动命令，84–86
  - 刻录 CD/DVD，38–39
  - 描述，12
  - 探索 Live CD，36
  - GUI 系统管理工具，376–377
  - KDE 桌面，146–150
  - Live DVD，13
  - 打印机配置，94–96
  - 文本模式安装，82
  - update-rc.d 命令，577–578
- Knoppix 菜单，Knoppix 桌面，147
- Konqueror Web 浏览器
  - 查看文件，191–193
  - 查看文件夹，191–193
  - MEPIS KDE 桌面，153
  - 概述，339
  - SUSE Linux 桌面，155
  - 查看 Web 页面，194
- Kontact
  - 描述，208
  - MEPIS KDE 桌面，153
  - 概述，218–219
  - SUSE Linux 桌面，155
- Kooka，210
- Kopecte
  - 描述，210
  - 概述，329–331
- KörGanizer，208
- KscD，209
- KSnapshot，210
- ksys 命令，404
- KWrite，208

### L

- LANs (local area networks) 局域网，27
  - 以太网设置，279–283
  - 以太网布线，281–283
  - 互联网连接，285–286
  - TCP/IP，275–279
  - TCP/IP 配置，283–285
- Launcher applets GNOME 启动器小工具，117
- lcd FTP 命令，369
- less GNU 软件包，19
- LGPL (GNU Library General Public License) GNU 库通用公共许可证，695, 697
- /lib 目录，428
- libpng GNU 软件包，19
- licenses 许可证，695–697
- LILO 引导加载程序，111–112
- links 链接，335–337
- Linspire，12
- Linux
  - 命令，170–173
  - 发行版，10–14
  - 简介，9
  - linux 新闻组，348
  - 与 Linux 相关的新闻组，348–349
- Live CDs 活 CD，13
  - 磁盘分区，40
  - 安装，33
  - knoppix，36
- loadable module support 内核可加载模块支持，479
- loading/unloading modules 加载/卸载模块，命令，404–405
- localhost.zone 文件，DNS，655–656
- Lock Xesktop Xandros Desktop 锁定，160
- log analysis and monitoring tools 日志分析和监控工具，558
- log files 日志文件，安全，509
- login 登录
  - GNOME，116
  - root，381–382
- Logout Xandros Desktop 注销，160
- logout 注销
  - GNOME，121
  - KDE，125
- LONE/TAP 实用工具，436
- LPJ (Loops per jiffy) 每 jiffy 循环数，112
- ls 命令，164
- ls FTP 命令，369
- LSB (Linux Standard Base) Linux 标准基础
  - 和 ABI，15
  - 认证计划，16
  - 通用规范，15
  - 硬件特定规范，15
- lsmod 命令，404
- Lynx，210



### M

- md GNU 软件包，19
- md 宏处理器，sedmail，618–620
- 宏，C 编程，702–705
- 邮件阅读器
  - Evolution，317–321
  - KMail，325–327
  - Thunderbird，321–325
- 邮件服务器
  - 安装，613–628
  - sendmail，614–628
- 主菜单
  - 分类，141
  - 简介，139
  - Knoppix 桌面，147
  - MEPIS KDE 桌面，150
  - SUSE Linux 桌面，155
  - Xandros 桌面，159
- 制作文件（make files）的阅读，682
- make 实用程序 (GNU)
  - 说明，19，23
  - Makefile 名称，683
  - Makefile 选项，683–684
  - Makefile 示例，686–687
- Makefiles，682
  - 运行，687–689
  - 变量，684–686
- man 命令，man
  - 页面，24
- man 页面，文档，24
- 管理组，418–419
- 安全管理，505
- Mandriva Linux，12
- MD5 消息摘要算法，345
- delete FTP 命令，369
- mdir FTP 命令，369
- /media 目录，428
- 内存
  - 编程，674
  - 技术设备，内核，481
- 菜单按钮，GNOME 桌面，117–119
- MEPIS Linux
  - 说明，12
  - GUI 系统管理工具，377–378
  - inetd，531
  - 安装，57–60
  - KDE 桌面，150–153
  - 打印机配置，94–96
  - 软件安装，104–106
  - 独立服务器，530
  - update-rc.d 命令，577–578
  - 更新，465–466
  - MEPIS OS Center，MEPIS KDE 桌面，152
- MFM 支持，内核，483
- nget FTP 命令，369
- 微处理器，24
- 杂项新闻组，348
- 迁移，安全，504–505
- mkdir FTP 命令，369
- nls FTP 命令，369
- /mnt 目录，428
- 调制解调器，安装，34
- 受控新闻组，348
- modinfo 命令，404
- modprobe 命令，404
- 模块化内核，475–476，491–492
- 模块，Perl，746，763–769
- 显示器，安装，35
- 整体式内核，475–476
- 挂载 Windows 共享，MEPIS KDE 桌面，153
- 挂载
  - 命令，203–204
  - 文件系统上的设备，429–430
  - 文件系统，NFS，433–434，664–665
  - 软盘，DOS/Windows 系统，442–443
  - NTFS 分区，444
- 鼠标
  - 安装，35
  - SUSE Linux 安装，68
- Mozilla，210，339
- mput FTP 命令，369
- MTA（邮件传输代理），314
- mutt GNU 软件包
  - 命令，446–447
  - 说明，19
  - /etc/mutt.conf 文件，445–446
  - 概述，444–445
- MUA（邮件用户代理），314
- 多媒体应用程序
  - amarok，209
  - 音频 CD，228，230–231
  - CD 刻录，233–234
  - cdda2wav，209
  - decord，209
  - digiKam，209
  - 数码相机，228
  - GNOME CD Player，209
  - growisofs，209
  - Kaffeine，209
  - K3b，209
  - KsCD，209
  - Rhythmbox，209
  - 声音文件，231–233
  - Totem，209
  - X-CD-Roast，209
  - xine，209
  - XMMS，209
- 多媒体设备，内核，487
- MySQL
  - 说明，209
  - MySQL monitor，226
  - 查询数据库，228
  - SQL 和，223
  - 表，定义，226–227
  - 表，加载数据，228

### N

- 名称服务器，DNS，657–659
- named 守护进程，BIND，643
- named Internet 服务，580
- 命名，设备，udev，403–404
- NATs（网络地址转换）的实现，538
- Nautilus 文件浏览器，Debian GNOME 桌面，142
- Nautilus shell
  - 刻录 CD，186–187
  - 文件，查看，186
  - 文件夹，在导航窗口中浏览，188–190
  - 文件夹，查看，186
  - 对象窗口，186
- 导航，Linux 命令和，194–206
- ncurses GNU 软件包，19
- Nessus 安全扫描器，559–561
- netfilter，539–545
- 网络，安全问题，506–507
- 网络地址，IP 地址和，277
- 网卡，安装和，35
- 网络设备，403
- 网络接口，303–304
- 网络 Internet 服务，580
- 网络层，TCP/IP，276
- 网络管理
  - TCP/IP 配置文件，299–303
- 网络数据包，嗅探，307–308
- 网络安全审查
  - inetd 和，555–556
  - xinetd 和，555–556
- 网络状态，305–307
- 网络实用工具，558
- 组网，580
  - 内核支持，485
  - TCP/IP，配置，283–285
  - 无线（参见无线以太网网络）
- 组网 Internet 服务，580
- 网络
  - 配置，在启动时，308–309
  - 配置，Fedora Core 安装，52–53
  - 防火墙，27
  - LAN，27
  - 协议，21
  - 安全，系统管理，374
  - 状态，系统管理，374
- 新新闻组，348
- 新闻服务器，INN 服务器，628–635
- 新闻服务，发行版，21
- 新闻组
  - 添加，637
  - alt，347
  - bionet，347
  - bit，347
  - biz，347
  - 分类，347–348
  - clarinet，347
  - comp，347
  - 配置文件，更新，636–637
  - 层级结构，346–347
  - 层级结构，定义，636
  - ieee，348
  - k12，348
  - linux，348
  - 与 Linux 相关的，348–349
  - misc，348
  - moderated，348
  - news，348
  - 概述，254
  - 发布新闻，353–354
  - 阅读，349–356
  - rec，348
  - sci，348
  - web，348
  - 订阅，353
  - talk，348
  - 测试，637
  - Usenet，345
  - UUCP，345
  - 相关网站，357
- 新闻阅读器
  - 简介，349–350
  - KNode，350，354–356
  - Pan，350
  - Thunderbird，350–353
- nfs Internet 服务，580
- NFS（网络文件系统）
  - 计算机漏洞和，551
  - 说明，279
  - 导出文件系统，432–433，662–664
  - 文件共享，661–665
  - Internet 服务，570
  - 挂载文件系统，433–434，664–665
  - 共享，26
- nfslock Internet 服务，580
- nsserver Internet 服务，580
- NIS（网络信息服务），计算机漏洞，551
- nmap（网络映射器），端口扫描工具，558–559

### O

- NNTP（网络新闻传输协议），279，349，570
- 不可抵赖性，安全，509
- NTFS 分区，挂载，444
- NTP（网络时间协议），Internet 服务，570
- null 语句，C 编程，719
- NVD（国家漏洞数据库），计算机漏洞，550

### P

- 对象，Perl，766–767
- 办公应用程序
  - AbiWord，208
  - Applixware Office，220
  - Aspell 实用工具，222–223
  - 计算器，219–220
  - 日历，218–219
  - 商业版，220–222
  - CrossOver Office，208，221–222
  - Dia，208
  - OpenOffice.org，208，214–218
  - StarOffice，208，220–221
- 办公工具
  - Aspell，208
  - 词典，208
  - GNOME 计算器，208
  - KCalc，208
  - Kontact，208
  - KOrganizer，208
- 一次性任务，调度，407–409
- 在线文档，23–24
- open FTP 命令，369
- OpenOffice
  - 说明，208
  - Knoppix 桌面，147
  - OpenOffice.org Calc，Fedora Core GNOME 桌面，146
  - OpenOffice.org Impress，Fedora Core GNOME 桌面，146
  - OpenOffice.org 办公套件
    - Calc，216–217
    - Impress，217–218
    - 简介，214–215
    - Writer，215–216
  - OpenOffice.org 快速入门，MEPIS KDE 桌面，153
  - OpenOffice.org Writer
    - Fedora Core GNOME 桌面，146
    - MEPIS KDE 桌面，153
- OpenSSH
  - /etc/ssh/sshd_config，533
  - /usr/bin/scp 和，533
  - /usr/bin/slogin，533
  - /usr/bin/ssh-keygen，533
  - /usr/sbin/sshd，532
  - OpenSSH，计算机漏洞，551
- 操作系统
  - 定义，9
  - 主机安全，552
  - 多任务，10
  - 多用户，10
  - 概述，10
  - 编程，675
  - 重置，10
  - 系统管理，374
- 运算符
  - C 编程，711–715
  - Perl，751–752
- /opt 目录，428
- 所有权
  - 命令，更改，199–200
  - 目录，516
  - 文件，516
  - 组，422–423
  - 用户，422–423

### P

- 包
  - 从源文件构建，461–465
  - 组，Fedora Core 安装，54–56
  - Perl，746，763–766
- 数据包，安全，510
- 包过滤防火墙，536
- 包过滤器
  - 启用，539–545
  - 安全，510
  - 安全级别配置工具，539–540
- 数据包嗅探器，558
- Pager applet，GNOME，117
- PAMs（可插拔认证模块），515
- Pan 新闻阅读器，350
- 面板
  - 常见功能，137–139
  - GNOME，116–117
  - KDE，122
- 分区。参见磁盘分区
- 内核，490
- NTFS，挂载，444
- PartitionMagic，调整 Windows 分区大小，40–41



密码检查工具，558
密码
- /etc/group，554
- /etc/passwd，554
- /etc/shadow，554
- PAMs，515
- root，忘记密码，383–384
- root，Fedora Core，53–54
- 保护，513–515
- 安全性，554–555
- 影子密码，514–515

patch GNU 软件包，19

路径名，各部分，182

PCI 总线，481

PCMCIA 总线，481

pcmcia 互联网服务，580

渗透测试，557

性能
- 磁盘性能，396–397
- 磁盘使用情况，396–397
- 系统管理，374
- top 实用程序，393–395
- uptime 命令，395
- vmstat 实用程序，395–396

周边网络，
安全性，510

外设，24, 26

Perl
- 描述，23
- 表达式，746, 751–752
- 正则表达式，752–755
- 文件访问，760–761
- 文件名，管道前缀，761–762
- 流程控制语句，746, 755–758
- foreach 语句，757–758
- 函数，746
- 内置函数，762–763
- goto 语句，758
- if 语句，755–756
- 简介，743–744
- Linux 命令访问，758–760
- 模块，746, 763–766
- 英语模块，766–769
- 对象，766–767
- 对象访问，767–768
- 创建对象，767–768
- 运算符，751–752
- 包，746, 763–766
- 脚本编写，745–746
- 语句，757–758
- 语句，746
- 子程序，762–763
- 语法，747
- unless 语句，755–756
- 变量，746–750
- which 命令，744
- while 语句，756–757

权限
- /boot/grub/menu.lst，553
- 命令，196–198, 199–200
- /etc/cron.allow，553
- /etc/cron.deny，553
- /etc/crontab，553
- /etc/hosts.allow，553
- /etc/hosts.deny，553
- /etc/logrotate.conf，553
- /etc/pam.d，553
- /etc/rc.d，553
- /etc/security，553
- /etc/selinux，553
- /etc/shadow，553
- /etc/sudoers.allow，553
- /etc/sshd，553
- /etc/sysconfig，553
- /etc/sysctl.conf，553
- /etc/syslog.conf，553
- /etc/udev/udev.conf，554
- /etc/vsftpd，554
- /etc/vsftpd.ftppusers，554
- /etc/xinetd，554
- /etc/xinetd.conf，554
- 文件，修改，517
- 文件，默认设置，517–519
- 主机安全性，552
- 设置用户 ID，519–520
- /var/log，554
- /var/log/lastlog，554
- /var/log/messages，554
- /var/log/wtmp，554

SELinux 的 Permissive 选项，57

物理控制台和虚拟控制台，161

TCP/IP 的物理层，277

PKI（公钥基础设施），安全性，510

“位置”菜单
- Fedora Core GNOME 桌面，145
- Ubuntu GNOME 桌面，157

GNOME“位置”菜单，描述，118

即插即用支持，内核，482

指针，C 语言编程，708–709

端口地址转换，NATs，538

端口号，TCP/IP，278–279

端口扫描器，工具名称，558

端口扫描，安全性，510

端口扫描工具，安全性，529

端口支持，内核，482

portmap 互联网服务，580

端口，URLs，337

#### PostgreSQL
- 描述，209
- 关系型数据库，223
- 向新闻组发送新闻，353–354
- 电源管理，内核，480

#### Powersaver 工具，SUSE
- Linux 桌面，155

#### 预定义变量，Perl，750

#### 预处理器指令，C 语言编程
- 条件指令，703–704
- include 指令，702
- 宏定义，702–705
- 概述，701–702
- 预防，主机安全性，552

#### 主要名称服务器，配置，657–659

#### 打印机，安装，35

#### 打印机
- Debian 配置，90–91
- Fedora Core 配置，92–94
- Knoppix 配置，94–96
- MEPIS 配置，94–96
- SUSE 配置，97–99
- Ubuntu 配置，99–100
- Xandros 配置，100–103
- 打印，系统管理，374
- 概率和影响，安全性，503
- /proc 文件系统，398–400

#### 进程
- 相关命令，172
- 编程，675
- Shell 命令，174–175

#### 处理器，安装，35

处理器类型，内核，479–480

#### 编程
- C。参见 C 语言编程
- 命令行，675
- 命令处理器，675
- 编译器，676
- 计算机，673–674
- CPU，674
- 调试，676
- 环境变量，675
- 表达式，676
- 流程控制语句，677
- 函数，677
- 硬盘，674
- 内存，674
- 操作系统，675
- 概述，676–677
- 进程，675
- Shell，675
- 软件开发工具，677–695
- 语句，677
- 文本编辑器，676
- 变量，676

#### prompt FTP 命令，369

#### 协议
- 描述，21
- URLs，336–337

#### 代理服务器，安全性，510

#### 公钥加密，安全性，510

#### 公钥加密，520–521

#### put FTP 命令，369

#### pwd FTP 命令，369

#### Python，23

### Q

#### QTParted，调整 Windows 分区大小，41–42

#### 查询数据库，MySQL，228

查询 RPMs，451–453

#### 问号 (?) 通配符，167–168

#### quit FTP 命令，369

### R

#### RAM（随机存取存储器），24
- 磁盘文件，创建，492–493
- 安装，35
- 编程，674

#### rcs GNU 软件包，19

#### RCS（修订控制系统），23

阅读 RSS 源，358–360

#### 重启问题，故障排除，87

重启，495–496

rec 新闻组，348

重复作业，调度，409–412

recv FTP 命令，369

#### 正则表达式，Perl，752–755

#### 远程访问，互联网使用，254

#### 远程登录
- 发行版相关，22
- SSH，532–534

#### 移除 RPMs，454

#### rename FTP 命令，369

#### 重复命令，169

#### resolver 库，DNS，644

#### 资源记录 (RR) 格式，650–653

#### 响应，主机安全性，552

#### 职责，安全性，504

#### return 语句，C 语言编程，719

#### Rhythmbox，209

#### 风险分析，安全性
- 概率和影响，503
- 线程，502
- 漏洞，502–503

RLL 支持，内核，483

rm dir FTP 命令，369

rmm od 命令，404

#### root
- 获取 root 权限，173–174
- /etc/password 文件条目，513
- GUI 实用程序，382
- 以 root 身份登录，381–382
- 密码，忘记密码，383–384
- /root 目录，428
- root 域，DNS，641–642
- root 密码
    - Fedora Core，53–54
    - GNOME 登录，116
- root 区域文件，DNS，653–655

#### RPM 文件
- 命令，450
- 文件名，451
- 安装，453–454
- 简介，449–450
- 查询，451–453
- 移除，454
- SRPMs（源代码 RPMs），464–465
- 升级，454–455
- 验证，455

#### RSS 源，阅读，358–360

#### 运行级别
- init 命令，387–388
- init 进程，385

### S

#### Samba
- 配置，667–669
- 安装，666–667
- 资源，669
- 软件包
    - 组件，665–666
    - 测试，669
- Windows 服务器设置，665–669

samba 互联网服务，581

SANS 研究所，计算机漏洞，550

- /sbin 目录，428
- /sbin/hotplug，设备命名，403
- /sbin/udev，设备命名，403

#### 标量变量，Perl，747–749

#### 作业调度
- 一次性作业，407–409
- 重复作业，409–412

sci 新闻组，348

筛查路由器，安全性，510

#### 脚本
- bash shell，内置命令，739–742
- 流程控制，736–739
- 简介，731–734
- Perl，745–746
- Shell 函数，735–736
- 存储，734–735

编写脚本，179–180

SCSI 控制器，安装，35

SCSI 设备，内核，484

SCSI 磁带驱动器，备份设备，435

SCSI Zip 驱动器，备份设备，435

DSL（对称 DSL），258

#### 安全性
- 应用网关，508
- 审计，504
- 身份验证，504, 508
- 授权，504
- 后门，508
- 堡垒主机，508
- 缓冲区溢出，508
- 业务需求，501
- CA（证书颁发机构），508
- 证书，508
- 保密性，508
- 破解者，499, 508
- 数据保护，504
- DoS（分布式拒绝服务），509
- 解密，508
- 数字签名，508
- 目录，516–520
- DMZ，509
- DoS（拒绝服务）攻击，499, 508
- 双角主机，509
- 加密，509
- 加密，520–527
- 利用工具，509
- 文件，516–520
- 防火墙，509, 534–545
- 建立框架，500–505
- GPG，523–527
- 哈希，509
- 主机，509
- 主机安全问题，506, 552–555
- 实施，504–505
- 事件处理，504
- 事件响应，555
- 完整性，509
- 互联网访问，504



安全审计
引言，504
必要性，548
非技术方面，548
概述，547–549
技术方面，549

sed GNU 软件包，19

SELinux，Fedora Core 配置，56–57

发送 PTP 命令，369

sendmail
别名文件，628
计算机漏洞，551
配置文件，617–623
描述，22
/etc/mail 目录，625–626
.forward 文件，627
引言，581
ml 宏处理器，618–620
宏文件，620–623
邮件投递，615–617
概述，614
测试，614–615
sendmail.cf 文件，语法，623–625

服务器
Internet 服务器，21–22
Internet 服务，565
独立，运行，575–581
启动/停止，389–390
Windows，Samba，665–669

设置用户 ID 权限，519–520
安装程序，安全性，510
shadow 密码，514–515

共享库
C 语言编程，724–729
描述，23
共享文件，NFS，26，432–434

Sharutils GNU 软件包，19

shell（外壳）。另见 bash shell
bash，内置命令，739–742
空格，163
命令补全，167
命令 I/O 重定向，165
命令输入，164
命令行，163
命令输出，164
命令语法，162–164
命令通配符，167–168
命令，127
命令，组合，164
命令，串联，164
命令，输入，165
命令，重复，169
命令，将输出保存到文件，165
函数，脚本编写，735–736
GNU，17
grep 命令，163
ls 命令，164
概述，125–126
进程管理，174–175
root 用户相关，173–174
脚本编写，179–180
stderr（标准错误输出），164
stdin（标准输入），164
stdout（标准输出），164
终端，打开，161
shell 脚本编写。另见 脚本编写

显示桌面选项
Debian GNOME 桌面，142
Fedora Core GNOME 桌面，146
Knoppix 桌面，147
MEPIS KDE 桌面，152
Ubuntu GNOME 桌面，158
Xandros 桌面，160

关机，129–130
信号 11 错误，86–87

文件签名
数字签名，521–522
GPG，525–526

单卷归档，436–437
size FTP 命令，369
Slackware Linux，13
smb Internet 服务，581
smbfs Internet 服务，581

SMTP（简单邮件传输协议）
描述，279
Internet 服务，570

嗅探器，安全性，510
嗅探网络数据包，307–308

SNMP（简单网络管理协议）
计算机漏洞，551
描述，279
Internet 服务，570
snmpd Internet 服务，581
soc 新闻组，348

套接字
属性，566
客户端/服务器模型，568
面向连接的协议，567
无连接协议，567
Internet 服务，566–569

软件
开发环境，22–23
下载，461–462
安装，103–104
软件包，从源文件构建，461–465
SUSE Linux 安装，68
系统管理，374
解包，461–462

软件开发工具
C 编译器，677
CVS，677
调试器，677
gdb，677
make 工具，677
RCS，677
文本编辑器，677
版本控制系统，677

声音，内核，488
声卡，安装，35
声音文件，播放，231–233
源代码，编程，676

源文件
从中构建软件包，461–465
编程相关，676

spamassassin Internet 服务，581
间谍软件，安全性，510
SRPMS（源 RPM），安装，464–465
/srv 目录，428
ssh Internet 服务，581

SSH（安全外壳）
描述，279
Internet 服务，570
远程登录，532–534
sshd Internet 服务，22，581

独立 Internet 服务
安全性，530
启动时自动运行，576–581
手动启动/停止，575–576

StarOffice，21，208，220–221
启动 INN 服务器，628–635
启动 Linux，引导加载程序，111
启动服务器，389
启动脚本，init 进程，388–389
启动/关机，系统管理，374
有状态检查防火墙，536–537

语句
C 语言编程，715–721
Perl，746
编程，677

静态 NATs，538
status FTP 命令，369

stdc++，shell 命令，164
stdin，shell 命令，164
stdout，shell 命令，164
停止服务器，389
存储，硬盘，25
su - 命令，382

子目录
/usr，184–185
/var，185

子程序，Perl，762–763
订阅新闻组，353
Subversion，23
subversion，计算机漏洞，551
超级服务器，530–531

SUSE 硬件工具，SUSE Linux 桌面，155
SUSE 帮助中心，SUSE Linux 桌面，155

SUSE Linux
chkconfig 命令，576–577
描述，13
桌面，153–156
FTP 安装，60–63
GUI 系统管理工具，378–379
硬件，36
安装，60–71
从 CD 安装，63–65
数据包过滤，540
打印机配置，97–99
软件安装，107–108
独立服务器，530
TCP/IP 网络配置，284
文本模式安装，82
在线更新，469–470
xinetd，531
YaST，65–71

SUSE 监视器，SUSE Linux 桌面，155
switch 语句，C 语言编程，719–720
对称密钥加密，安全性，510
Synaptic 软件包管理器，MEPIS KDE 桌面，152
语法，Perl，747
sysc，设备命名，403
syslogd Internet 服务，581
syslog Internet 服务，581

系统管理
备份，374
Debian GUI 系统管理工具，375
设备文件，401–403
设备命名，403，403–404
驱动模块，加载/卸载，404–405
Fedora Core GUI 系统管理工具，375–376
文件系统挂载/卸载，374
硬件管理，374
引言，25
作业调度，407–412
Knoppix GUI 系统管理工具，376–377
MEPIS GUI 系统管理工具，377–378
网络状态监控，374
操作系统，374
性能监控，393–397
打印系统，374
/proc 文件系统，398–400
root 用户，登录，381–384
安全监控，374
安全设置，374
软件安装，374
SUSE Linux GUI 系统管理工具，378–379
系统信息，查看，398–400
系统性能监控，374
系统启动/关机，374
任务自动化，374
Ubuntu GUI 系统管理工具，379–380
用户账户，添加/删除，373
实用工具，374
Xandros GUI 系统管理工具，380–381

系统配置，文件，390–392

系统文件
/boot/grub/menu.lst，553
/etc/cron.allow，553
/etc/cron.deny，553
/etc/crontab，553
/etc/hosts.allow，553
/etc/hosts.deny，553
/etc/logrotate.conf，553
/etc/pam.d，553
/etc/passwd，553
/etc/rc.d，553
/etc/security，553
/etc/sysconfig.allow，553
/etc/ssh，553
/etc/sysconfig.allow，553




### 《Linux 一本通傻瓜书》

#### 系统文件（续）
- /etc/sysctl.conf，553
- /etc/syslog.conf，553
- /etc/udev/udev.conf，554
- /etc/vsftpd，554
- /etc/vsftpd.ftpusers，554
- /etc/xinetd.conf，554
- /etc/xinetd.d，554
- /var/log，554
- /var/log/lastlog，554
- /var/log/messages，554
- /var/log/wtmp，554

#### 系统信息
- 查看，398–400

#### 系统菜单，Ubuntu
- GNOME 桌面环境，158

#### 系统菜单，GNOME
- 描述，118
- Fedora Core，146

#### 系统性能监视器
- MEPIS KDE 桌面环境，153

#### 系统安全监控
- 527

### T

#### 表格，数据库
- 定义，226–227
- 加载数据，227–228

#### Talk 新闻组
- 348

#### 磁带备份
- 439–440

#### Tar GNU 软件包
- 19

#### Tar 程序
- 归档，26
- 自动备份，440
- 解压缩文件，437–438
- 增量备份，440
- 多卷归档，438
- 选项，437
- 单卷归档，436–437

#### Tcl/Tk（工具命令语言/工具包）
- 23

#### TCP/IP 配置文件
- 基本文件，299
- /etc/hosts，300–301
- /etc/hosts，300
- /etc/hosts.allow，301–302
- /etc/hosts.deny，302
- /etc/networks，300
- /etc/nsswitch.conf，302–303
- /etc/resolve.conf，301

#### TCP/IP（传输控制协议）/互联网协议
- 21
- 应用层，276
- DHCP，279
- FTP，279
- 主机连通性，304–305
- HTTP，279
- 互联网，277
- 互联网服务，566–569
- 引言，275–276
- IP 地址，277–278
- IP 路由表，304
- 网络层，276–277
- 网络接口，303–304
- 网络层，276
- 网络状态，305–307
- 网络配置，283–285
- NFS，279
- NNTP，279
- 物理层，277
- 端口号，278–279
- SMTP，279
- 嗅探网络数据包，307–308
- SNMP，279
- SSH，279
- TELNET，279
- TFTP，279
- 传输层，276

#### TCP 包装器
- inetd，572
- 安全，531–532

#### 电话支持，内核
- 486

#### TELNET
- 描述，279
- 互联网服务，570

#### 10Base2 以太网布线
- 281

#### 10Base5 以太网布线
- 281

#### 终端，打开
- 161

#### 终端程序
- Debian GNOME 桌面环境，142
- Knoppix 桌面环境，147
- MEPIS KDE 桌面环境，152
- SUSE Linux 桌面环境，155

#### 测试方法论
- 计算机漏洞，550–552
- 安全，概述，549–550

#### 测试工具，安全
- 主机安全工具，558
- IDS（入侵检测系统），558
- 引言，557
- 日志分析与监控工具，558
- 网络工具，558
- 数据包嗅探器，558
- 密码检查工具，558
- 端口扫描器，558
- 漏洞扫描器，558

#### Texinfo GNU 软件包
- 19

#### 文本编辑器，编程
- 676

#### 文本编辑器选项，MEPIS KDE 桌面环境
- 153

#### 文本编辑器
- ed，240–244
- emacs，208
- 图形界面文本编辑器，239–240
- Kate，208
- KWrite，208
- vi，240–249
- vim，208

#### 文本模式安装
- 82

#### 文本终端，GNU
- 17

#### TFTP（简单文件传输协议）
- 描述，279
- 互联网服务与，571

#### 粗线以太网布线
- 281

#### 细线以太网布线
- 281

#### 威胁，安全
- 拒绝服务，502
- 向公众泄露信息，502
- 概述，511
- 未授权访问，502

#### Thunderbird
- 邮件按钮，322–323
- 撰写消息，324–325
- 描述，210
- 收件箱，324
- 概述，321–325
- 发送消息，324–325
- Xandros 桌面环境，159
- 新闻简报，350–353

#### Time GNU 软件包
- 19

#### 时区
- Fedora Core，53
- SUSE Linux 安装，68

#### TKIP（时序密钥完整性协议）
- 291

#### /tmp 目录
- 428

#### 顶层目录，列出
- 183–184

#### Top 实用工具
- 引言，393
- 输出屏幕，394–395

#### Totem
- 209

#### 传输层，TCP/IP
- 276

#### 回收站图标，Debian GNOME 桌面环境
- 142

#### 特洛伊木马，安全
- 511

#### 故障排除
- Knoppix 启动命令，84–86
- Linux 内核启动选项与，87–89
- PC 重启问题，87
- 信号 11 错误，86–87
- X 窗口系统，82–84

#### 双绞线布线，定义
- 282

#### 类型定义，C 语言编程
- 709–710

#### 类型限定符，C 语言编程
- 710

### U

#### Ubuntu Linux
- 启动，114
- 描述，13
- GNOME 桌面环境，156–158
- GNU 系统管理工具，379–380
- inetd，531
- 安装，71–72
- 打印机配置，99–100
- 软件安装，104–106
- 独立服务器，530
- 文本模式安装，82
- update-rc.d 命令，577–578
- 更新，465–466

#### Udev，设备命名
- 403–404

#### UDP（用户数据报协议）
- 567

#### 未授权访问，安全
- 502

#### UNIX，Shell 与
- 125–126

#### Unless 语句，Perl
- 755–756

#### 卸载，命令
- 203–204

#### 解包软件
- 461–462

#### Update-rc.d 命令
- Debian，577–578
- Knoppix，577–578
- MEPIS，577–578
- Ubuntu，577–578
- Xandros，577–578

#### 更新
- Debian GNU/Linux，465–466
- Fedora Core，466–469
- MEPIS Linux，465–466
- 在线更新，应用程序，465–472
- 安全，511–512
- Ubuntu GNOME 桌面环境，158
- Ubuntu Linux，465–466
- Xandros 桌面环境，160，471–472

#### 升级，RPM 包
- 454–455

#### Uptime 命令
- 395

#### URL（统一资源定位符）
- 335–337

#### USB 支持，内核
- 488

#### 用户账户
- 添加，413–417
- 管理命令，416–417
- /etc/passwd 文件，417–418
- 图形界面用户管理器，414–416
- 系统管理，373
- 用户环境，420–422
- 用户 FTP 命令，369

#### 用户
- 管理命令，172
- 文件所有权，422–423

#### /usr/bin/scp，OpenSSH
- 533

#### /usr/bin/slogin，OpenSSH
- 533

#### /usr/bin/ssh-keygen，OpenSSH
- 533

#### /usr 层次结构
- 428

#### /usr/sbin/ssh，OpenSSH
- 532

#### /usr/sbin/sshd，OpenSSH
- 532

#### /usr 子目录
- 184–185

#### 实用工具
- 商业备份工具，435–436
- 系统管理，374

#### UUCP（UNIX 对 UNIX 复制协议）
- 345

### V

#### /var 层次结构
- 428

#### /var/log/apache2 配置文件
- 392

#### /var/boot.msg 配置文件
- 392

#### /var/log/cron 配置文件
- 392

#### /var/log/dmesg 配置文件
- 392

#### /var/log/httpd 配置文件
- 392

#### /var/log/messages 配置文件
- 392

#### /var 子目录
- 185

#### 变量
- C 语言编程，705–706
- -makefile，684–686
- Perl，746，747–750
- 编程，676

#### 验证，RPM 包
- 455

#### 版本号
- 特定发行版，14–15
- 内核，14

#### Vi 文本编辑器
- 缓冲区移动，246
- 冒号命令模式，246
- 命令，247–249
- 光标移动命令，246
- 文本输入命令模式，246
- 可视命令模式，246

#### 显卡，安装
- 35

#### Vim
- 208

#### 虚拟控制台，打开
- 161

#### 虚拟主机设置，Apache Web 服务器
- 603–606

#### 病毒，安全
- 511

#### Vstat 实用工具
- 395–396

#### Void 类型，C 语言编程
- 722

#### Volatile 类型限定符，C 语言编程
- 710

#### 音量
- Debian GNOME 桌面环境，142
- Fedora Core GNOME 桌面环境，146
- MEPIS KDE 桌面环境，153
- SUSE Linux 桌面环境，155
- Ubuntu GNOME 桌面环境，158
- Xandros 桌面环境，160

#### 音量，Knoppix 桌面环境
- 148

#### VSFTPD
- 配置文件，608–609
- 描述，22
- 互联网服务，581
- 服务器，安全，530
- .conf 文件，609–612

#### 漏洞，安全
- 502–503，511
- 另见计算机漏洞

#### 漏洞扫描器
- 558

### W

#### 电话拨号扫描，安全
- 511

#### 驾车攻击，安全
- 511

#### 废纸篓图标，Debian GNOME 桌面环境
- 142

#### 看门狗定时器，内核
- 486

#### 天气，MEPIS KDE 桌面环境
- 153

#### 天气小工具，GNOME
- 117

#### Web
- 发行版，21
- HTML，334
- HTTP，334
- 链接，335–337
- 概述，333–335
- URL，335–337
- 用途，254

#### Web 浏览器，Ubuntu GNOME 桌面环境
- 158

#### Web 浏览器
- Epiphany，339
- Firefox，339
- 作为 FTP 客户端，364–366
- 更改主页，342–343
- HTML 文档，334
- 引言，337–338
- Konqueror，339
- Mozilla，339

#### Web 服务器
- HTML 文档，334
- 概述，337–338

#### 网站
- 新闻组，357
- 安全更新，511–512

#### WEP（有线等效隐私），无线网络
- 289–291

#### While 语句
- C 语言编程，720–721
- Perl，756–757

#### Wi-Fi（无线保真）网络
- 287

#### 命令中的通配符
- 167–168

#### Winbind 互联网服务
- 581

#### 窗口列表，Knoppix 桌面环境
- 147

#### 窗口选择器，Debian GNOME 桌面环境
- 142

#### Windows
- 分区，调整大小，40–42
- 服务器设置，Samba，665–669

#### Winmodem
- 270

#### 无线以太网网络
- ad hoc 模式，289
- 配置，293–297
- 硬件设置，291–292
- 基础设施模式，289
- 概述，287–288
- 标准，287–288
- 与 WEP，289–291
- 无线接入点，配置，292–293

#### 工作区切换器
- Debian GNOME 桌面环境，142
- Fedora Core GNOME 桌面环境，146
- Ubuntu GNOME 桌面环境，158

#### 万维网
- 见 Web

#### 蠕虫，安全
- 511

#### Writer，OpenOffice.org
- 215–216

#### 编写脚本，Shell
- 179–180

### X

#### X-CD-Roast
- 209

#### X 窗口系统
- GUI，20
- 故障排除，82–84

#### XFree86
- 20

#### X.Org X11
- 20

#### Xandros 桌面操作系统
- 启动，113–114
- 自定义安装，76–80
- 描述，270
- 快速安装，75–76
- GUI 系统管理工具，380–381
- 图标，158
- inetd，531
- 安装，73–80
- 打印机配置，100–103
- 软件安装，108–110
- 独立服务器，530
- 文本模式安装，82
- 更新，471–472
- update-rc.d 命令，577–578

#### Xandros 文件管理器
- Xandros 桌面环境，159

#### XFree86
- 20

#### Xfs 互联网服务
- 581

#### Xine
- 209

#### Xinetd
- 互联网服务，581
- 互联网超级服务器，573–575
- 网络安全审查，555–556
- 服务器，安全，530

#### XMMS
- 209

#### X.OrgX11
- 20

#### Xpdf
- 210

#### XSanе
- 210

#### xscanimage
- 210

#### XWD（X 窗口转储）
- 与脚本，731

### Y

#### YaST，SUSE 安装
- 65–71

#### Ypbind 互联网服务
- 581

#### Yum
- 466–469





## 说明

### ISO 发行版

本书包含 Red Hat, Inc. 提供的 Red Hat Linux ISO 副本，你可以按照随软件提供的许可协议使用。你从 Red Hat 购买的官方 Red Hat Linux 包含完整的官方 Red Hat Linux 发行版、Red Hat 文档，可能还包含针对官方 Red Hat Linux 的技术支持。你也可以从 Red Hat 购买技术支持。你可以透过公司的网站（`www.redhat.com`）或其免费电话 1.888.REDHAT1 从 Red Hat 购买官方 Red Hat Linux 和技术支持。

### 有限保修

- (a) WPL 保证，在自购买本书之日起六十（60）天的正常使用寿命期间，软件及软件介质在材料和工艺上无缺陷。如果 WPL 在保修期内收到关于材料或工艺缺陷的通知，WPL 将更换有缺陷的软件介质。

- (b) 对于软件、程序、其中包含的源代码以及/或本书中描述的技术，WPL 和本书作者均否认其他所有明示或暗示的保证，包括但不限于关于适销性和特定用途适用性的暗示保证。WPL 不保证软件中包含的功能将满足你的要求，也不保证软件的操作无错误。

- (c) 此有限保修赋予你具体的法律权利，你或许还拥有因司法管辖区而异的其他权利。

### Linux® 全能桌面参考指南 第2版 源代码提供

为了遵守 GNU 通用公共许可证（GNU GPL），我们单独提供 Linux 源代码。任何人都可以使用此履约要约在 DVD 上接收源代码。如果你希望将源代码寄送给你，请按照以下说明通过电话、在线或优惠券进行订购。

对于每种订购方式，请在提示时输入 ISBN：047004988X。费用为 2.04 美元（USD），另加运费。

条款：法律禁止或限制的地区无效。请允许 2-4 周交货时间。

#### 通过电话订购：

- 1. 在美国拨打免费电话：1-877-762-2974。国际客户请拨：1-317-572-3994。
- 2. 向操作员提供相应的 ISBN。请准备好你的信用卡。

#### 通过在线订购：

- 1. 访问 http://www.wiley.com/
- 2. 使用“产品搜索”功能搜索 Linux All-in-One Desk Reference For Dummies 2E Source Code 或 047004988X。
- 3. 将该项目放入购物车。

#### 通过优惠券订购：

- 1. 填写下方的优惠券。
- 2. 附上金额为 2.04 美元（USD）另加运费的支票或汇票。如需了解运费，美国客户请致电 1-877-762-2974，国际客户请致电 1-317-572-3994。
- 3. 将优惠券寄至优惠券底部列出的地址。

**姓名**

![](img/11709a8f88c8cd03868a929dc94c0e2b_831_0.png)

**公司**

![](img/11709a8f88c8cd03868a929dc94c0e2b_831_1.png)

**地址**

![](img/11709a8f88c8cd03868a929dc94c0e2b_831_2.png)

市_______州_______邮政编码_______国家

**电子邮箱**

![](img/11709a8f88c8cd03868a929dc94c0e2b_831_3.png)

**电话**

![](img/11709a8f88c8cd03868a929dc94c0e2b_831_4.png)

**购书地点**

![](img/11709a8f88c8cd03868a929dc94c0e2b_831_5.png)

☐ （在此处勾选以加入我们的电子邮件列表，了解我们的最新动态——这是一种便捷的方式，可以接收关于我们产品和活动以及特别折扣优惠的消息。）

**请将此优惠券连同适当的美元资金寄回至：**

Wiley Publishing, Inc.
客户服务部
Linux All-in-One Desk Reference For Dummies 第2版 – 源代码 [047004988X]
10475 Crosspoint Blvd.
Indianapolis, IN 46256

**条款：** Wiley 对丢失、被盗、延迟或字迹不清的订单概不负责。有关此履约要约的问题，请致电 1-877-762-2974 或 1-317-572-3994。

### GNU 通用公共许可证

版本 2，1991 年 6 月
版权所有 © 1989, 1991 自由软件基金会（Free Software Foundation, Inc.）
美国，马萨诸塞州，波士顿，圣殿广场 59 号 - 330 室，邮编 02111-1307

任何人都可以复制和分发本许可文档的逐字副本，但对其进行修改是不允许的。

#### 序言

大多数软件的许可证旨在剥夺你分享和修改它们的自由。相比之下，GNU 通用公共许可证旨在保证你分享和修改自由软件的自由 - 确保该软件对所有用户都是自由的。该通用公共许可证适用于自由软件基金会的大多数软件，以及任何其他作者承诺使用它的程序。（自由软件基金会的其他一些软件则由 GNU 库通用公共许可证覆盖。）你也可以将其应用于你的程序。

当我们谈论自由软件时，我们指的是自由，而不是价格。我们的通用公共许可证旨在确保你拥有分发自由软件副本的自由（如果你愿意，可以为这项服务收费），获得源代码或在你想要时获取它，修改软件或其部分用于新的自由程序；并且你知道你可以做这些事情。

为了保护你的权利，我们需要做出限制，禁止任何人否认你这些权利或要求你放弃这些权利。这些限制转化为如果你分发软件的副本或修改软件时你所承担的某些责任。

例如，如果你分发此类程序的副本，无论是免费还是收费，你都必须向接收者提供你拥有的所有权利。你必须确保他们也能获得或获取源代码。你必须向他们展示这些条款，以便他们了解其权利。

我们通过两个步骤保护你的权利：(1) 对软件进行版权保护，(2) 向你提供此许可证，赋予你复制、分发和/或修改软件的法律许可。

此外，为了每位作者及我们的保护，我们希望确保每个人都理解，此自由软件没有任何保修。如果软件被他人修改并传递下去，我们希望接收者知道他们拥有的不是原始版本，这样由他人引入的问题就不会反映在原始作者的声誉上。

最后，任何自由程序都不断受到软件专利的威胁。我们希望能够避免自由程序的分发者各自获得专利许可，从而使程序实际上成为专有软件的危险。为防止这种情况，我们已明确表示，任何专利必须供所有人自由使用，或者根本不予授权。

复制、分发和修改的精确条款和条件如下。

#### 复制、分发和修改的条款和条件

- 0. 本许可证适用于任何包含版权持有者放置的通知，声称其可以按照本通用公共许可证的条款分发的程序或其他作品。下文中的“程序”指任何此类程序或作品，“基于程序的作品”指版权法下的程序或任何衍生作品：也就是说，包含程序或其一部分的作品，无论是逐字包含还是经过修改和/或翻译成另一种语言。（下文中，翻译无限制地包含在“修改”一词中。）每个被许可人称为您。

除复制、分发和修改以外的活动不受本许可证覆盖；它们在其范围之外。运行程序的行为不受限制，程序产生的输出仅当其内容构成基于程序的作品时（无论是否由运行程序产生）才受覆盖。这是否属实取决于程序的功能。

- 1. 你可以复制和分发程序的源代码的逐字副本，以你收到的形式，在任何介质上，前提是你显著且适当地在每个副本上发布适当的版权声明和免责声明；保持所有指代本许可证及无保修的通知完整无损；并随程序向程序的其他接收者提供本许可证的副本。

你可以就传输副本的物理行为收取费用，并且你可以选择提供保修保护以换取费用。

- 2. 你可以修改程序或其任何部分的副本，从而形成基于程序的作品，并复制和分发此类修改或作品，前提是符合上述第 1 节的条款，并且你也满足所有这些条件：
  - a) 你必须使修改过的文件带有显著的通知，说明你修改了文件以及任何修改的日期。




##### 2. 你可以修改你持有的本程序或其任何部分的副本，从而形成基于该程序的作品，并可以根据上述许可协议的条款复制或分发这些修改或作品。

- b) 你必须确保你分发或发布的任何作品，无论在整体上或部分包含或派生自该程序或其任何部分，都必须作为一个整体，根据本许可协议的条款，免费许可给所有第三方。

- c) 如果修改后的程序在运行时通常以交互方式读取命令，则你必须确保该程序在以最普通的方式进行此类交互式使用并启动运行时，打印或显示一条公告，其中包含适当的版权声明、无保证声明（或者声明你提供保证），以及告知用户可以在这些条件下重新分发该程序，并告知用户如何查看本许可协议的一份副本。（例外：如果该程序本身是交互式的，但通常不打印此类公告，则基于该程序的你的作品无需打印公告。）

这些要求适用于修改后的作品整体。如果该作品中可以识别的部分未从该程序派生，且可以合理地被视为其本身独立且分开的作品，则当你将这些部分作为独立作品分发时，本许可协议及其条款不适用于这些部分。但是，当你将这些部分作为基于该程序的作品的整体的一部分进行分发时，整个作品的分发必须在本许可协议的条款下进行，该许可协议对其他被许可人的权限扩展到整个作品，因此也扩展到每一部分，无论其作者是谁。

因此，本节的意图并非主张权利或质疑你完全由你编写的作品的权利；其意图在于行使基于该程序的派生作品或集合作品的分发控制权。

此外，将未基于该程序的另一作品与该程序（或基于该程序的作品）单纯聚合在存储或分发介质的一个卷中，并不会使该另一作品落入本许可协议的范围。

##### 3. 你可以按照上述第 1 节和第 2 节的条款，以目标代码或可执行形式复制或分发该程序（或基于它的作品），前提是你同时也做到以下事项之一：

- a) 随附完整的、对应的机器可读源代码，且必须根据上述第 1 节和第 2 节的条款，在惯常用于软件交换的介质上进行分发；或者

- b) 随附一份为期至少三年的书面要约，向任何第三方提供一份完整的、对应的机器可读源代码副本，费用不超过你实际执行源分发工作的成本，且必须根据上述第 1 节和第 2 节的条款，在惯常用于软件交换的介质上进行分发；或者

- c) 随附你收到的关于分发对应源代码要约的信息。（此替代方案仅允许用于非商业性分发，且仅当你收到的是目标代码或可执行形式的程序，并附带此类要约，且符合上述 b 小节的规定时。）

对于一个作品的源代码，指的是为该作品进行修改的首选形式。对于一个可执行作品，完整的源代码意味着其包含的所有模块的所有源代码，加上任何相关的接口定义文件，加上用于控制该可执行文件编译和安装的脚本。然而，作为特殊例外，分发的源代码无需包含任何通常随可执行文件运行的操作系统的主要组件（编译器、内核等，以源代码或二进制形式）分发的内容，除非该组件本身随附可执行文件。

如果通过提供从指定地点复制的访问权限来分发可执行文件或目标代码，则提供从同一地点复制源代码的同等访问权限，即使第三方未被强制要求将源代码与目标代码一起复制，也视为源代码的分发。

##### 4. 除本许可协议明确规定外，你不得复制、修改、再许可或分发该程序。

任何其他企图复制、修改、再许可或分发该程序的行为均无效，并将自动终止你根据本许可协议享有的权利。但是，只要你保留全面遵守，从你处根据本许可协议收到副本或权利的当事方，其许可不会被终止。

##### 5. 你无需接受本许可协议，因为你并未签署它。

然而，其他任何内容均未授予你修改或分发该程序或其衍生作品的许可。如果你不接受本许可协议，这些行为在法律上是禁止的。因此，通过修改或分发该程序（或任何基于该程序的作品），你表明你接受这样做的本许可协议，以及对于复制、分发或修改该程序或基于它的作品的所有条款和条件。

##### 6. 每次你重新分发该程序（或任何基于该程序的作品）时，接收方自动从原始许可方获得一份许可，使其可以复制、分发或修改该程序，但须遵守这些条款和条件。

你不得对接收方行使此处授予的权利施加任何进一步限制。你对第三方遵守本许可协议不负有强制执行的責任。

##### 7. 如果由于法院判决、专利侵权指控或任何其他原因（不限于专利问题），你被强加了条件（无论是通过法院命令、协议还是其他方式），这些条件与本许可协议的条件相矛盾，它们并不豁免你履行本许可协议的条件。

如果你无法同时满足本许可协议下的义务和其他相关义务进行分发，那么后果是你完全不能分发该程序。例如，如果某项专利许可不允许所有直接或通过你间接收到副本的人免费重新分发该程序，那么满足该专利许可和本许可协议的唯一方式就是完全停止分发该程序。

如果本节的任何部分在特定情况下被判定为无效或不可执行，该节的其余部分旨在继续适用，且该节整体旨在在其他情况下适用。

本节的目的是并非诱导你侵犯任何专利或其他财产权主张，或质疑此类主张的有效性；本节的唯一目的是保护自由软件分发系统的完整性，该系统通过公共许可协议实践来实现。许多人通过依赖该系统的一致应用，为通过该系统分发的广泛软件范围做出了慷慨贡献；是否愿意通过其他系统分发软件由作者/捐赠者决定，被许可人不能强加这一选择。

本节旨在彻底明确据信是本许可协议其余部分的一个后果。

##### 8. 如果由于专利或受版权保护的接口限制，该程序在特定国家的分发和使用受到限制，将本程序置于本许可协议之下的原始版权持有人可以添加明确的地理分发限制，排除那些国家，从而允许分发仅在未被排除的国家之间或之内进行。

在这种情况下，本许可协议将此类限制纳入其中，就好像其写在本许可协议正文中一样。

##### 9. 自由软件基金会可能不时发布通用公共许可协议的修订版和/或新版本。

这些新版本将在精神上与当前版本相似，但在细节上可能会有所不同，以解决新的问题或关切。

每个版本都被赋予一个区分版本号。如果该程序指定了适用于它的本许可协议版本号以及“任何后续版本”，你有选择遵守该版本或自由软件基金会发布的任何后续版本的条款和条件的选项。如果该程序未指定本许可协议版本号，你可以选择自由软件基金会发布的任何版本。

##### 10. 如果你希望将该程序的部分内容整合到其他分发条件不同的自由软件中，请写信给作者请求许可。

对于受自由软件基金会版权保护的软件，请写信给自由软件基金会；我们有时会对此做出例外。我们的决定将由两个目标指导：保持我们所有自由软件衍生作品的自由状态，以及促进软件的一般共享和重用。




### 无保证声明

11. 由于该程序是免费授权的，在法律允许的范围内，除非以书面形式另有说明，版权持有者和/或其他方将程序按“原样”提供，不作任何明示或暗示的保证，包括但不限于对适销性和特定用途适用性的暗示保证。关于程序质量和性能的全部风险均由您承担。如果程序被证明存在缺陷，您将承担所有必要的服务、维修或更正费用。

12. 在任何情况下，除非适用法律要求或经书面协议约定，任何版权持有者，或按照上述权限修改和/或重新分发程序的任何其他方，对于因使用或无法使用程序而产生的任何一般性、特殊性、偶然性或后果性损害（包括但不限于数据丢失、数据不准确，或您或第三方遭受的损失，或程序与任何其他程序无法协同运行的故障），均不承担损害赔偿责任，即使该持有者或其他方已被告知此类损害的可能性。

条款和条件结束

## 商业、职业与个人理财

![](img/11709a8f88c8cd03868a929dc94c0e2b_838_0.png)

0-7645-5307-0

![](img/11709a8f88c8cd03868a929dc94c0e2b_838_1.png)

0-7645-5331-3 *

**亦提供：**

- 1. 《会计学傻瓜入门》*
  0-7645-5314-3
- 2. 《商业计划书傻瓜工具包》*
  0-7645-5365-8
- 3. 《求职信傻瓜入门》
  0-7645-5224-4
- 4. 《节俭生活傻瓜入门》
  0-7645-5403-4
- 5. 《领导力傻瓜入门》
  0-7645-5176-0
- 6. 《管理傻瓜入门》
  0-7645-1771-6
- 7. 《市场营销傻瓜入门》
  0-7645-5600-2
- 8. 《个人理财傻瓜入门》*
  0-7645-5290-5
- 9. 《项目管理傻瓜入门》
  0-7645-5283-X
- 10. 《简历傻瓜入门》*
  0-7645-5471-9
- 11. 《销售傻瓜入门》
  0-7645-5363-1
- 12. 《小型企业傻瓜工具包》**
  0-7645-5093-4

## 家庭与办公计算机基础

![](img/11709a8f88c8cd03868a929dc94c0e2b_838_2.png)

0-7645-4074-2

![](img/11709a8f88c8cd03868a929dc94c0e2b_838_3.png)

0-7645-3758-X

**亦提供：**

- 1. 《ACT考试傻瓜入门》
  0-7645-3645-6
- 2. 《Life ’04 计算机全面参考傻瓜手册》
  0-7645-7347-0
- 3. 《iPAQ掌上电脑傻瓜入门》
  0-7645-6769-1
- 4. 《Mac OS X Panther 省时技巧傻瓜手册》
  0-7645-5812-9
- 5. 《Mac电脑傻瓜入门》
  0-7645-5656-8
- 6. 《Microsoft Money 2004 傻瓜入门》
  0-7645-4195-1
- 7. 《Office 2003 全面参考傻瓜手册》
  0-7645-3883-7
- 8. 《Outlook 2003 傻瓜入门》
  0-7645-3759-8
- 9. 《PC电脑傻瓜入门》
  0-7645-4074-2
- 10. 《TiVo录像机傻瓜入门》
  0-7645-6923-6
- 11. 《PC电脑升级与修复傻瓜手册》
  0-7645-1665-X
- 12. 《Windows XP 省时技巧傻瓜手册》
  0-7645-3748-2

## 美食、家居、园艺、爱好、音乐与宠物

![](img/11709a8f88c8cd03868a929dc94c0e2b_838_4.png)

0-7645-5295-3

![](img/11709a8f88c8cd03868a929dc94c0e2b_838_5.png)

0-7645-5232-5

**亦提供：**

- 1. 《贝斯吉他傻瓜入门》
  0-7645-2487-9
- 2. 《糖尿病食谱傻瓜手册》
  0-7645-5230-9
- 3. 《园艺傻瓜入门》*
  0-7645-5130-2
- 4. 《吉他傻瓜入门》
  0-7645-5106-X
- 5. 《节日装饰傻瓜入门》
  0-7645-2570-0
- 6. 《家居装修全能傻瓜手册》
  0-7645-5680-0
- 7. 《编织傻瓜入门》
  0-7645-5395-X
- 8. 《钢琴傻瓜入门》
  0-7645-5105-1
- 9. 《幼犬饲养傻瓜入门》
  0-7645-5255-4
- 10. 《剪贴簿艺术傻瓜入门》
  0-7645-7200-3
- 11. 《老年犬护理傻瓜入门》
  0-7645-5818-8
- 12. 《歌唱傻瓜入门》
  0-7645-2475-5
- 13. 《30分钟速制菜肴傻瓜手册》
  0-7645-2589-1

## 互联网与数字媒体

![](img/11709a8f88c8cd03868a929dc94c0e2b_838_6.png)

0-7645-1664-7

![](img/11709a8f88c8cd03868a929dc94c0e2b_838_7.png)

0-7645-6924-4

**亦提供：**

- 1. 《2005在线购物指南傻瓜手册》
  0-7645-7495-7
- 2. 《CD与DVD刻录傻瓜入门》
  0-7645-8596-7
- 3. 《eBay易趣傻瓜入门》
  0-7645-5654-1
- 4. 《防范垃圾邮件傻瓜手册》
  0-7645-5965-6
- 5. 《在线家谱研究傻瓜入门》
  0-7645-5964-8
- 6. 《Google傻瓜入门》
  0-7645-4420-9
- 7. 《音乐家家庭录音傻瓜入门》
  0-7645-1634-5
- 8. 《互联网傻瓜入门》
  0-7645-4173-0
- 9. 《iPod与iTunes傻瓜入门》
  0-7645-7727-7
- 10. 《防范身份盗窃傻瓜手册》
  0-7645-7336-5
- 11. 《Pro Tools 全面参考傻瓜手册》
  0-7645-5714-9
- 12. 《Roxio Easy Media Creator傻瓜入门》
  0-7645-7131-1

* 另提供加拿大独立版本
** 另提供英国独立版本

凡有书籍出售处均有售。欲了解更多信息或直接订购：美国客户请访问 www.dummies.com 或拨打 1-877-762-2974。英国客户请访问 www.wiley europe.com 或拨打 0800 234307。加拿大客户请访问 www.wiley.ca 或拨打 1-800-567-4797。

## 体育、健身、育儿、宗教与灵性

![](img/11709a8f88c8cd03868a929dc94c0e2b_839_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_839_1.png)

0-7645-5146-9
0-7645-5418-2

亦提供：

- 《养子领养傻瓜手册》 0-7645-5488-3
- 《篮球傻瓜入门》 0-7645-5248-1
- 《圣经傻瓜入门》 0-7645-5296-1
- 《佛教傻瓜入门》 0-7645-5359-3
- 《天主教傻瓜入门》 0-7645-5391-7
- 《曲棍球傻瓜入门》 0-7645-5228-7
- 《犹太教傻瓜入门》 0-7645-5299-6
- 《武术傻瓜入门》 0-7645-5358-5
- 《普拉提傻瓜入门》 0-7645-5397-6
- 《宗教傻瓜入门》 0-7645-5264-3
- 《教孩子阅读傻瓜手册》 0-7645-4043-2
- 《举重训练傻瓜入门》 0-7645-5168-X
- 《瑜伽傻瓜入门》 0-7645-5117-5

## 旅行

![](img/11709a8f88c8cd03868a929dc94c0e2b_839_2.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_839_3.png)

0-7645-5438-7
0-7645-5453-0

亦提供：

- 《阿拉斯加傻瓜旅行指南》 0-7645-1761-9
- 《亚利桑那傻瓜旅行指南》 0-7645-6938-4
- 《坎昆与尤卡坦傻瓜旅行指南》 0-7645-2437-2
- 《邮轮度假傻瓜入门》 0-7645-6941-4
- 《欧洲傻瓜旅行指南》 0-7645-5456-5
- 《爱尔兰傻瓜旅行指南》 0-7645-5455-7
- 《拉斯维加斯傻瓜旅行指南》 0-7645-5448-4
- 《伦敦傻瓜旅行指南》 0-7645-4277-X
- 《纽约市傻瓜旅行指南》 0-7645-6945-7
- 《巴黎傻瓜旅行指南》 0-7645-5494-8
- 《房车度假傻瓜入门》 0-7645-5443-5
- 《沃尔特迪士尼世界与奥兰多傻瓜旅行指南》 0-7645-6943-0

## 图形、设计与Web开发

![](img/11709a8f88c8cd03868a929dc94c0e2b_839_4.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_839_5.png)

0-7645-4345-8
0-7645-5589-8

亦提供：

- 《Adobe Acrobat与PDF傻瓜入门》 0-7645-3760-1
- 《网站构建傻瓜入门》 0-7645-1441-3
- 《Dreamweaver MX 2004傻瓜入门》 0-7645-4242-3
- 《FrontPage 2003傻瓜入门》 0-7645-3882-9
- 《HTML 4傻瓜入门》 0-7645-1995-6
- 《Illustrator x傻瓜入门》 0-7645-4084-X
- 《Macromedia Flash MX 2004傻瓜入门》 0-7645-4358-X
- 《Photoshop 7 全面参考傻瓜手册》 0-7645-1667-1
- 《Photoshop cs 省时技巧傻瓜手册》 0-7645-6782-9
- 《PHP 5傻瓜入门》 0-7645-6166-8
- 《PowerPoint 2003傻瓜入门》 0-7645-3908-6
- 《QuarkXPress 6傻瓜入门》 0-7645-2593-X

## 网络、安全、编程与数据库

![](img/11709a8f88c8cd03868a929dc94c0e2b_839_6.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_839_7.png)

0-7645-6852-3
0-7645-5784-X

亦提供：

- 《A+认证考试傻瓜手册》 0-7645-4187-0
- 《Access 2003 全面参考傻瓜手册》 0-7645-3988-4
- 《编程入门傻瓜手册》 0-7645-4997-9
- 《C语言傻瓜入门》 0-7645-7088-4
- 《防火墙傻瓜入门》 0-7645-4048-3
- 《家庭网络傻瓜入门》 0-7645-42796
- 《网络安全傻瓜入门》 0-7645-1679-5
- 《网络基础傻瓜入门》 0-7645-1677-9
- 《TCP/IP傻瓜入门》 0-7645-1760-2
- 《VBA傻瓜入门》 0-7645-3988-2
- 《无线技术：全能参考傻瓜手册》 0-7645-7496-5
- 《无线家庭网络傻瓜入门》 0-7645-3910-8





## 健康与自助

![](img/11709a8f88c8cd03868a929dc94c0e2b_840_0.png)

- ISBN: 0-7645-6820-5 *†
- ISBN: 0-7645-2556-2

其他可选版本：

- [阿尔茨海默病实用指南](Alzheimer's For Dummies)
  0-7645-3899-3
- [阿斯伯格综合征实用指南](Asperger For Dummies)
  0-7645-4233-8
- [控制胆固醇实用指南](Controlling Cholesterol For Dummies)
  0-7645-5440-9
- [抑郁症实用指南](Depression For Dummies)
  0-7645-3900-0
- [节食实用指南](Dieting For Dummies)
  0-7645-4149-8
- [生育实用指南](Fertility For Dummies)
  0-7645-2549-2
- [纤维肌痛实用指南](Fibromyalgia For Dummies)
  0-7645-5441-7
- [提升记忆力实用指南](Improve Your Memory For Dummies)
  0-7645-5435-2
- [怀孕实用指南 †](Pregnancy For Dummies †)
  0-7645-4483-7
- [戒烟实用指南](Quitting Smoking For Dummies)
  0-7645-2629-4
- [人际关系实用指南](Relationships For Dummies)
  0-7645-5384-4
- [甲状腺实用指南](Thyroid For Dummies)
  0-7645-5385-2

## 教育、历史、参考与备考

![](img/11709a8f88c8cd03868a929dc94c0e2b_840_1.png)

- ISBN: 0-7645-5194-9
- ISBN: 0-7645-4186-2

其他可选版本：

- [代数实用指南](Algebra For Dummies)
  0-7645-5325-9
- [英国历史实用指南](British History For Dummies)
  0-7645-7021-8
- [微积分实用指南](Calculus For Dummies)
  0-7645-2498-4
- [英语语法实用指南](English Grammar For Dummies)
  0-7645-5322-4
- [法医学实用指南](Forensics For Dummies)
  0-7645-5580-4
- [GMAT 实用指南](The GMAT For Dummies)
  0-7645-5251-1
- [西班牙语实用指南](Inglés Para Dummies)
  0-7645-5427-1
- [意大利语实用指南](Italian For Dummies)
  0-7645-5196-5
- [拉丁语实用指南](Latin For Dummies)
  0-7645-5431-X
- [刘易斯与克拉克实用指南](Lewis & Clark For Dummies)
  0-7645-2545-X
- [研究论文写作实用指南](Research Papers For Dummies)
  0-7645-5426-3
- [SAT 实用指南](The SAT For Dummies)
  0-7645-7193-1
- [科学展览项目实用指南](Science Fair Projects For Dummies)
  0-7645-5460-3
- [美国历史实用指南](U.S. History For Dummies)
  0-7645-5249-X

![](img/11709a8f88c8cd03868a929dc94c0e2b_840_2.png)

## 访问 dummies.com® 获取智慧

- 查看 Dummies 全标题列表
- 浏览大量*免费*在线文章
- 注册接收每周发送给您的*免费* eTips 电子邮件
- 了解其他带有 Dummies 名称的产品
- 直接从 Dummies 书店购买
- 每月有机会赢取新奖品！

* 另有单独的加拿大版
† 另有单独的英国版

## 用 Dummies 做更多事情
为大众打造的产品！

从爱好到健康，发现种类繁多的有趣产品

![](img/11709a8f88c8cd03868a929dc94c0e2b_841_0.png)

- DVD/视频 • 音乐 CD • 游戏
- 消费电子产品 • 软件
- 手工套件 • 烹饪套件 • 更多！

