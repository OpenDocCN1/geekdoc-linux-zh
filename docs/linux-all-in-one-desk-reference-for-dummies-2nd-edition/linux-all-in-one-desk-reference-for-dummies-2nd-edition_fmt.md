
# Linux 一本全大傻瓜指南

www.dbebooks.com - 免费图书与杂志

# 关于作者

Naba Barkakati 是一名电气工程师和成功的计算机书籍作者，拥有从 MS-DOS 和 Windows 到 UNIX 和 Linux 等广泛系统的经验。他在 1984 年从马里兰大学学院市分校获得电气工程博士学位后，购买了他第一台个人电脑——IBM PC/AT。在追求全职工程职业生涯的同时，Naba 梦想为新兴的 PC 软件市场编写软件。幸运的是，他没有像微软那样建立软件帝国，而是写了成功的计算机书籍。目前，Naba 是美国政府问责局（GAO）技术与工程中心的资深技术专家。

在过去的 15 年里，Naba 撰写了 25 多本关于多个主题的计算机书籍，从使用 C++ 的 Windows 编程到 Linux。他撰写了多部畅销书，如《The Waite Group's Turbo C++ Bible》、《Object-Oriented Programming in C++》、《X Window System Programming》、《Visual C++ Developer's Guide》、《Borland C++ 4 Developer's Guide》和《Linux Secrets》。他的书被翻译成多种语言，包括西班牙语、法语、波兰语、希腊语、意大利语、中文、日语和韩语。Naba 最近出版的书籍是《Red Hat Fedora Linux Secrets》，也由 Wiley 出版公司出版。

Naba 与妻子 Leha 及子女 Ivy、Emily 和 Ashley 居住在马里兰州北波托马克。

# 题词

我想将这本书献给我的妻子 Leha 和我的女儿们 Ivy、Emily 和 Ashley。

# 作者致谢

我要感谢 Terri Varveris，是她让我开始了这本书的创作——一套关于 Linux 的八本快速参考指南，重点介绍几个主要的 Linux 发行版。作为项目编辑，Christopher Morris 指导我完成手稿提交流程，并让各项工作顺利推进。我感激 Terri 和 Chris 在这个项目中给予我的指导和支持。

我要感谢 Jason Luster 对手稿的技术准确性进行审核，并为改进书籍内容提供了许多有用的建议。

感谢 Wiley 出版公司的所有人，他们将我的原始手稿转化为一本编辑精良、包装精美的书籍。

当然，如果没有 Linux，这本书也就没有存在的意义了。为此，我们要感谢 Linus Torvalds 以及世界各地的众多 Linux 开发人员。最后，一如既往，我最大的感谢献给我的妻子 Leha 和我们的女儿 Ivy、Emily 和 Ashley——是她们对我的爱和支持让我坚持不懈。感谢你们的陪伴！

# 出版商致谢

我们为这本书感到自豪；请通过我们在 www.dummies.com/register/ 的在线注册表格向我们发送您的意见。

帮助将本书推向市场的一些人员包括：

- **采购、编辑和媒体开发**
  - **项目编辑：** Christopher Morris
  - **收购编辑：** Terri Varneris
  - **文字编辑：** Heidi Unger
  - **技术编辑：** Dan DiNico
  - **编辑经理：** Kevin Kirschner
  - **版权编辑：** Laura Moss
  - **媒体开发专家：** Travis Silvers, Laura VanWinkle
  - **媒体开发主管：** Richard Gravers
  - **编辑助理：** Amanda Foxworth
  - **漫画：** Rich Tennant (www.the5thwave.com)

- **制作服务**
  - **项目协调员：** Erin Smith
  - **排版与图形：** Andrea Dahl, Denny Hager, Melanee Prendergast, Heather Ryan, Erin Zeltner
  - **校样审读者：** Vicki Broyles, Joe Niesen
  - **索引编制员：** Johnna VanHoose

- **技术类 Dummies 出版与编辑**
  - Richard Swadley, 副总裁兼执行集团出版人
  - Andy Cummings, 副总裁兼出版人
  - Mary Bednarek, 执行收购总监
  - Mary C. Corder, 编辑总监

- **消费者类 Dummies 出版**
  - Diane Graves Steele, 副总裁兼出版人
  - Joyce People, 收购总监

- **制作服务**
  - Gerry Fahey, 制作服务副总裁
  - Debbie Staley, 制作服务总监

![](img/792720823146d68f19fd50c99ebfce4b_24_0.png)

# 简介

当你考虑到 Linux 的起源及其持续演化的方式时，你会发现它确实非常了不起。从一人一事的卑微起点——来自芬兰的 Linux Torvalds 的个人爱好——Linux 已经成长为一个成熟的操作系统，其功能可与任何商业 UNIX 操作系统相媲美。最棒的是，Linux——包括其所有源代码——对任何人都是免费的。你只需从互联网网站下载它，或者以象征性的费用从众多 Linux CD 供应商处通过 CD 或 DVD 获取它。

Linux 绝对是“一分钱一分货”这一规则的例外。尽管 Linux 是免费的，但就性能、功能和可靠性而言，它绝不逊色。Linux 的稳健性与其开发和更新方式有关。世界各地的许多开发人员协作添加功能。用户会持续下载增量版本，并在多种系统配置中进行测试。Linux 版本的 Beta 测试比任何商业软件都严格得多。

自 1994 年 3 月 14 日发布 Linux 内核 1.0 以来，全球 Linux 用户数量呈指数级增长。已经开发了许多 Linux 发行版——即操作系统与应用程序及安装工具的组合——以简化安装和使用。一些 Linux 发行版是商业销售并得到支持的，而许多则继续免费提供。

与许多免费软件不同，Linux 附带大量关于各种主题（如为各种 PC 和外设安装和配置操作系统）的在线信息。一小群核心 Linux 用户足够熟练，仅凭在线文档就能高效使用 Linux。然而，数量大得多的用户则是带着特定目的（例如设置 Web 服务器或学习 Linux）转向 Linux 的。此外，大量 Linux 用户在家中使用其系统。对于这些新用户来说，在线文档并不容易使用，而且文档通常不涵盖用户可能想使用 Linux 进行的特定用途。

如果你刚开始使用 Linux，你需要的是一个实用指南，它不仅帮助你开始 Linux 的安装和设置，还向你展示如何使用 Linux 执行特定任务，例如设置 Web 服务器或开发软件。在确定一个你喜欢的发行版之前，你可能还想尝试不同的 Linux 发行版。

# 关于本书

因此，*Linux All-in-One Desktop Reference For Dummies（Linux 全能桌面参考 傻瓜入门）* 随书附带一张 DVD，其中包含七个不同的 Linux 发行版——Debian GNU/Linux 3.1r0、Fedora Core 5、Knoppix 4.0.2、MEPIS 3.3.1、SUSE Linux 10.0、Ubuntu 5.04 和 Xandros 3.02 Open Circulation Edition——以及安装和使用这些任何发行版的说明。（*提示：* 你可以直接使用本书 DVD 中的 Knoppix Live CD 获得快速、无风险的 Linux 体验。）

*Linux All-in-One Desk Reference For Dummies（Linux 全能桌面参考 傻瓜入门）* 在一本书中提供了八种不同的快速参考指南。这八本小书合在一起，提供了有关安装、配置和使用 Linux 的详细信息。

你最喜欢这本书的一点是，你不需要按顺序逐章阅读，甚至不需要按章节内的顺序阅读。你可以大致翻到你想要的主题，快速找到关于 Linux 的紧迫问题的答案，无论是关于使用 OpenOffice.org 文字处理软件还是设置 Apache Web 服务器。

以下是你可以用这本书做到的一些事情：

- 从随书附带的 DVD-ROM 安装和配置 Linux——Debian、Fedora Core、Knoppix、MEPIS、SUSE、Ubuntu 或 Xandros。（你可以通过简单地从 DVD 启动来使用 Knoppix。）
- 通过 DSL 或电缆调制解调器将 Linux PC 连接到 Internet。
- 使用 PPP 设置拨号网络。
- 将无线以太网添加到现有网络中。
- 获取有关 Linux 特定使用的技巧、技术和快捷方式，例如：
  - 设置和使用 Internet 服务：Web、邮件、新闻组、FTP、NFS 和 DNS。
  - 使用 Samba 设置 Windows 服务器。



- 使用 `Linux` 命令。
- 在 `Linux` 上使用 `Perl`、`Shell` 和 `C` 编程。
- 使用随 `Linux` 附带的 `OpenOffice.org` 办公套件和其他应用程序。
- 理解系统和网络安全的基础知识。
- 执行系统管理任务。

## 本书使用的约定

我在本书中使用一种简单的符号风格。所有清单、文件名、函数名、变量名和关键字都用等宽字体排版，以便于阅读。我*斜体*新术语和概念的首次出现，并立即提供定义。我使用**粗体**显示键入的命令。命令的输出和任何文件清单都用等宽字体显示。

## 你不必阅读的内容

每本迷你参考书都聚焦于一个特定任务领域——例如使用 Internet 或运行 Internet 服务器——然后提供一系列相关任务的操作说明。你可以直接跳到某个部分，阅读关于特定任务的内容。除了与你问题相关的几段文字或步骤列表，你不必阅读其他任何内容。使用目录或索引来查找与你问题相关的页面。

你可以放心忽略 `Technical Stuff`（技术细节）图标旁边的文本以及侧边栏。但是，如果你是那种喜欢了解 `Linux` 工作原理的一些隐藏细节的人，那就请深入研究 `Technical Stuff` 图标和侧边栏。

## 你是谁？

我假设你对 PC 有一定了解——你知道如何开启和关闭它，并且已经接触过 `Windows`。考虑到大多数新 PC 都预装了 `Windows`，这个假设是安全的，对吧？你还知道如何使用一些 `Windows` 应用程序，例如 `Microsoft Office`。

在您的 PC 上安装 `Linux` 时，您可能希望保留 `Windows 2000` 或 `Windows XP` 的安装。我假设你不介意缩小 `Windows` 分区以为 `Linux` 腾出空间。为此，你可以使用随书配套 DVD 中 `Knoppix` 包含的 `sparted` 实用工具，或投资于良好的磁盘分区工具，如 `Symantec` 的 `Norton PartitionMagic`，可从 `www.powerquest.com/partitionmagic` 获取。（不，我与 `Symantec` 没有任何关系。）

我还假设你愿意接受这样的风险：当你尝试安装 `Linux` 时，某些东西可能无法完全正常工作。如果你有一些不常见的硬件类型，可能会出现问题。如果你担心损坏系统，尝试找一台稍旧一点的备用 `Pentium` PC 进行牺牲，然后在那台 PC 上安装 `Linux`。或者直接从随本书附带的 DVD 运行 `Knoppix`。

## 本书的组织结构

`Linux All-in-One Desk Reference For Dummies`（`Linux` 全能桌面参考 傻瓜入门）包含八本小书，每本书都聚焦于一小组相关主题。如果你正在寻找特定主题的信息，请查看书脊上的小书名称或查阅目录。

这本桌面参考书以一本解释 `Linux` 基础知识并指导你完成安装过程的小书开始（这是本书的一个非常实用的方面，因为你通常不会购买预装 `Linux` 的 PC）。第二本小书作为 `Linux` 的用户指南——它专注于探索 `Linux` 工作站的各个方面，包括 `GNOME` 和 `KDE` 图形用户界面以及随 `Linux` 捆绑的许多应用程序。第三本小书涵盖网络，第四本小书深入介绍 Internet 的使用。第五本小书介绍系统管理。第六本小书转向保护 `Linux` 系统及其关联网络的重要主题。第七本小书向你展示如何运行各种 Internet 服务器，从邮件到 Web 服务器。第八本也是最后一本小书向你介绍编程。

以下是八本书及其内容的快速概览：

- **Book I: Linux Basics（Linux 基础）：** `Linux` 是什么？理解 `Linux 2.6` 内核中的新功能。安装、配置和排查不同 `Linux` 发行版（`Debian`、`Fedora Core`、`Knoppix`、`MEPIS`、`SUSE`、`Ubuntu` 和 `Xandros`）的问题。尝试 `Linux`。
- **Book II: Linux Desktops（Linux 桌面）：** 探索 `GNOME` 和 `KDE`。使用 `Shell`（什么是 `Shell`？）。导航 `Linux` 文件系统。探索多媒体软件以及文本编辑器（`vi` 和 `emacs`）等应用程序。
- **Book III: Networking（网络）：** 通过拨号连接或 `DSL` 或电缆调制解调器等高速常开连接将 `Linux` PC 连接到 Internet。配置和管理 `TCP/IP` 网络，包括无线网络。
- **Book IV: Internet（Internet）：** 使用各种 Internet 服务，如电子邮件、Web 浏览和阅读新闻组。使用 `FTP` 传输文件。
- **Book V: Administration（管理）：** 执行基本系统管理。管理用户帐户和文件系统。安装应用程序。处理设备和打印机。使用 `USB` 设备。升级和定制 `Linux` 内核。
- **Book VI: Security（安全）：** 理解网络和主机安全。保护主机和网络。执行安全审计。

## 侧边栏

有时，我会使用侧边栏来突出显示一些有趣但并非关键的信息。侧边栏解释你可能从未接触过的概念，或对相关主题提供些许见解。如果你赶时间，可以安全地跳过这些侧边栏。

- **第七卷：互联网服务器**：管理互联网服务。配置 `Apache` Web 服务器。设置 `FTP` 服务器。配置邮件和新闻服务器。提供 `DNS`。使用 `NFS` 进行文件共享。使用 `Samba` 设置 `Windows` 服务器。
- **第八卷：编程**：了解编程基础。探索 `Linux` 中的软件开发工具。编写 `shell` 脚本。学习 `C` 和 `Perl` 编程。
- **附录：关于 DVD**：总结本书配套 `DVD-ROM` 的内容。

## DVD 上有什么？

`DVD` 包含七个 `Linux` 发行版——这是一张结合 `Fedora Core 4` 和 `Knoppix` 的 `DVD`，其中包含一个 `distros` 文件夹，内有 `Debian`、`Knoppix`、`MEPIS`、`SUSE`、`Ubuntu` 和 `Xandros` 的 `ISO` 镜像文件，并按单独文件夹进行组织。你可以按照随软件提供的许可协议使用此 `DVD`。若要了解 `DVD` 内容的更多信息，请参阅附录。

## 本书中使用的图标

沿袭《全家桶桌面参考 For Dummies》系列的悠久传统，我使用图标帮助你快速定位有用信息。图标包括以下内容：

![](img/792720823146d68f19fd50c99ebfce4b_30_0.png)

发行版特定图标指出适用于特定发行版——本书涵盖的 `Debian`、`Fedora Core`、`Knoppix`、`MEPIS`、`SUSE`、`Ubuntu` 和 `Xandros`——的信息。

![](img/792720823146d68f19fd50c99ebfce4b_30_1.png)

记住图标标记一般性有趣的事实——即你希望知道并记住的内容。

![](img/792720823146d68f19fd50c99ebfce4b_31_0.png)

提示图标标记那些可以帮助你更轻松完成任务的事项。

![](img/792720823146d68f19fd50c99ebfce4b_31_1.png)

警告图标突出显示潜在陷阱。有了这个图标，我要告诉你：

“小心！这可能损害你的系统！”

![](img/792720823146d68f19fd50c99ebfce4b_31_2.png)

技术内容图标标记对高级用户（或那些希望成为高级用户的人）可能感兴趣的技术信息。

## 接下来怎么办

是时候开始你的 `Linux` 冒险了。拿出 `DVD` 并安装 `Linux`——选择一个发行版，任意一个发行版（只要它是 `Debian`、`Fedora Core`、`Knoppix`、`MEPIS`、`SUSE`、`Ubuntu` 或 `Xandros` 即可）。然后，转到相关章节，让乐趣开始。使用目录和索引来确定你想去哪里。不知不觉间，你将成为 `Linux` 专家！

我希望你咨询这本书的乐趣能像我写这本书时的乐趣一样多！

# 第一卷

# Linux 基础

# 第五波

作者：Rich Tennant

![](img/792720823146d68f19fd50c99ebfce4b_32_0.png)

“我觉得光标不动，Dunt 先生，是因为你的手放在黑板擦上，而不是鼠标上。”

# 第 1 章：介绍 Linux

## 本章内容

- 解释 `Linux` 是什么
- 浏览 `Linux` 发行版通常包含的内容
- 发现 `Linux` 帮助你管理什么
- 入门

我敢打赌你听说过 `Linux`。如果你想知道 `Linux` 具体是什么以及它能帮你做什么，本章旨在回答这些问题。这里我提供了 `Linux` 的宏观图景，并告诉你如何立即开始使用它。

顺便说一下，本书涵盖适用于 `Intel 80x86` 和 `Pentium` 处理器（基本上是能运行任何版本 `Windows` 的 PC）的 `Linux`。

## Linux 是什么？



你知道你的 PC 是一堆*硬件*——你可以触摸的东西，比如机箱、显示器、键盘和鼠标。机箱包含最重要的硬件——*中央处理器*（CPU），即运行*软件*（任何指示计算机如何执行你指令的程序，实际上你无法触摸到软件）的微型芯片。在典型的 Pentium 4 PC 中，Pentium 4 微处理器就是 CPU。机箱中其他重要的硬件包括*内存*（RAM 芯片）和*硬盘*——并且必须有一个程序来运行所有这些组件并使它们协同工作：*操作系统*。

*操作系统*是管理所有硬件并运行其他软件的程序。你，即用户，通过点击菜单和图标或输入一些晦涩的文本来提供这些指令。Linux 是一个操作系统——就像 UNIX、Windows 98、Windows 2000 和 Windows XP 一样。Linux 操作系统是以 UNIX 为模型的；在最基本、无花哨功能的形态下，Linux 操作系统也被称为*Linux 内核*。

操作系统赋予了计算机——任何计算机——其个性。例如，你可以在 PC 上运行 Windows 98 或 Windows XP——而在同一台 PC 上，你还可以安装并运行 Linux。这意味着，取决于在特定时刻安装并运行的是哪个操作系统，同一台 PC 可以是 Windows 98、Windows XP 或 Linux 系统。

## Linux 真的能在任何计算机上运行吗？

Linux 运行在许多不同类型的计算机系统上——它确实似乎能在几乎任何类型的计算机上运行。Linus Torvalds 和其他程序员最初为 Intel 80x86（及兼容）处理器系列开发了 Linux。如今，Linux 也适用于基于其他处理器的系统——例如配备 AMD 64 位 AMD64 处理器、Motorola 68000 系列、Alpha AXP、Sun SPARCs 和 UltraSPARCs、Hewlett-Packard 的 HP PA-RISC、PowerPC 和 PowerPC64 处理器，以及 MIPS R4000 和 R5000 的系统。最近，IBM 为其 S/390 和 zSeries 大型机发布了其自身的 Linux 版本。本书涵盖适用于 Intel 80x86 和 Pentium 处理器的 Linux。（这些被称为 IA32 架构处理器，或 i386，因为它们支持 80386 处理器的指令集。）

操作系统的主要工作是将软件（计算机程序）从硬盘（或其他永久存储介质）加载到内存中，并使 CPU 运行这些程序。你用计算机做的一切都是可能的，这归功于操作系统，因此如果操作系统以某种方式搞砸了，整个系统就会冻结。你知道当你最喜爱的操作系统——甚至可能是随 PC 附带的那个操作系统——突然崩溃时有多令人愤怒，就在那你刚写好给朋友的长篇电子邮件并即将点击发送按钮的时候。你尝试三指敬礼（按 `Ctrl-Alt-Delete`），但没有任何反应。然后就该按重置按钮了（前提是计算机制造商足够明智，包含了一个重置按钮）。幸运的是，这种事情在 Linux 上几乎从未发生——它以是一个非常可靠的操作系统而闻名。

![](img/792720823146d68f19fd50c99ebfce4b_35_0.png)

在技术术语中，Linux 是一个*多用户、多任务操作系统*。这意味着 Linux 允许多个用户登录，并且 Linux 可以同时在运行多个程序。如今几乎所有操作系统都是多用户和多任务的，但在 Linux 于 1994 年刚起步时，*多用户*和*多任务*是主要的卖点。

## Linux 发行版

一个*Linux 发行版*由 Linux*内核*（操作系统）和一组应用程序组成，并附带一个易于使用的安装程序。顺便说一下，大多数人只说*Linux* 来指代特定的 Linux 发行版。

你会发现许多 Linux 发行版，每个都包含标准的 Linux 操作系统以及以下主要软件包：

### 1.2 什么是 Linux？

- X 窗口系统：它是图形用户界面。
- 一个或多个图形桌面环境：其中最受受欢迎的包括 GNOME 和 KDE。
- 一系列应用程序：Linux 程序以可直接运行的软件形式提供，但包含源代码（即我们人类用来指示计算机执行操作的命令，或者容易获取），同时也附带相关文档。

当前的 Linux 发行版包含大量的软件选择——数量之多，以至于某些发行版通常需要多张 CD-ROM 或一张 DVD-ROM（本书随附光盘）。

Linux 内核、Linux 发行版中的软件包以及 Linux 发行版本身的发展和维护工作均以开源项目的形式组织。简而言之，开源意味着可以访问源代码，并且有权自由地重新分发软件，不受任何限制。除了我简洁的说明外，该定义的内涵要丰富得多。若想了解更多关于开源含义及可接受的开源许可证的详细信息，请访问开放源代码促进会（Open Source Initiative）的网站 `www.opensource.org`。

表 1-1 列举了一些主要的 Linux 发行版，并对每个发行版进行了简要描述。除了我在表 1-1 中列出的发行版外，还有许多其他的 Linux 发行版。

> 若想了解更多关于 Linux 发行版的信息，请访问 DistroWatch.com，网址为 `www.distrowatch.com`。在该网站上，你可以阅读关于特定发行版的资料，并查找订购特定发行版 CD 或 DVD 的链接。

**表 1-1 主要 Linux 发行版**

| 发行版 | 描述 |
| :--- | :--- |
| Debian GNU/Linux | 这个非商业发行版始于 1993 年，至今仍是广受欢迎的发行版，世界各地的许多志愿者开发人员都在为该项目做出贡献。Debian 是一个庞大的发行版。仅二进制软件包就需要 14 张 CD 或 2 张 DVD。不过，如果你拥有互联网连接，可以使用单张 Debian 网络安装 CD（可在 `www.debian.org/CD/netinst` 获取）来安装基础系统。安装好基础的 Debian 系统后，你可以使用名为 `apt-get` 的软件包安装程序轻松安装和升级 Debian 软件包，其中 apt 代表高级软件包工具（Advanced Package Tool）。Debian 可从 `www.debian.org` 免费获取。Debian 是近期多个其他发行版的基础，包括 Knoppix、MEPIS、Ubuntu 和 Xandros。 |
| Fedora Core | 该发行版是 Red Hat Linux（Red Hat 公司的 Linux 发行版）的继承者。2003 年 11 月发布的 Fedora Core 1 是 Red Hat Linux 9 的继承者。Fedora Core 可自由获取。Fedora Core 使用 Red Hat 软件包管理器（RPM）格式来处理其软件包。你可以从 `http://fedora.redhat.com` 下载 Fedora Core。 |
| Gentoo Linux | 这是一个非商业的基于源代码（意味着所有软件均以源代码形式提供）的发行版，首次出现在 2002 年。安装程序提供了一些二进制软件包以便让 Linux 运行起来，但其理念是在用户的计算机上编译所有源代码软件包。这使得构建一个拥有最新图形桌面、多媒体工具和开发工具的全功能 Gentoo 系统非常耗时，因为所有软件包都需要下载并编译。Gentoo Linux 可从 `www.gentoo.org` 免费获取。 |
| Knoppix | 这个 Live CD 发行版基于 Debian，以其德国开发者 Klaus Knopper 的名字命名。Knoppix 可用作恢复工具（用于修复已安装 Linux 系统的问题），因为你可以直接从 CD 运行 Knoppix，而无需先将其安装到硬盘上。Knoppix CD 以压缩格式存储软件，Knoppix 会即时解压缩程序。采用这种技术，Knoppix 可以在一张 CD 上打包多达 2GB 的软件。Knoppix 使用 Debian 软件包管理。若想了解免费下载 Knoppix 的信息，请访问 Knoppix 网站 `www.knopper.net/Knoppix/index-en.html`。 |
| Linspire | 这个商业发行版于 2002 年首次以 LinuxVOS 的名称发布。Linspire 使用 Debian 软件包格式，并通过其称为 Click-N-Run 的基于 Web 的界面提供付费软件下载。你可以通过 BitTorrent（一种点对点的文件共享系统）下载名为 LinuxVOSLive 的 Live CD 版本。若想了解更多关于 Linspire 的信息，请访问 `www.linspire.com`。 |
| Mandriva Linux | 这个流行的发行版最初是 1998 年发布的 Red Hat Linux 的一个版本，拥有易于使用的安装程序，并默认使用 KDE 作为桌面环境。直到最近，该发行版仍被称为 Mandrakelinux。Mandriva Linux 使用 Red Hat 软件包管理器（RPM）格式来处理其软件包。你可以从 `www.mandrivalinux.com` 获取 Mandriva Linux 下载版（一套 3 张 CD/DVD）。点击“下载”链接以获取更多详细信息。 |



### MEPIS Linux
这个基于 Debian 的 Live CD 发行版于 2003 年 7 月首次发布。它还包含一个图形化安装程序，可以从 Live CD 启动，以将 MEPIS 安装到硬盘上。MEPIS 具有出色的硬件检测功能，并预装 Java 和多媒体软件，因此很受欢迎。MEPIS 使用 Debian 软件包格式。你可以从 `www.mepis.org` 免费下载 SimplyMEPIS Live CD。

### Slackware Linux
这是最古老的发行版之一，首次发布于 1992 年。Slackware 使用压缩的 tar 文件作为其软件包，并提供一个基于文本的安装程序，该安装程序具有有限的硬件自动检测功能。你需要通过编辑文本文件来完成所有软件配置。Slackware 可从 `www.slackware.com` 免费获取。

### SUSE Linux
这个商业发行版于 2005 年 8 月切换为一个名为 openSUSE 的社区开发项目。SUSE Linux 开源软件（OSS）现在可自由获取，零售版 SUSE Linux 基于开源版本。SUSE 附带 `YaST` 安装和配置工具。SUSE Linux 使用 `RPM` 软件包。openSUSE 项目提供 SUSE Linux OSS 的 ISO 映像文件，可从多个镜像站点下载（参见 `www.opensuse.org/Download`）。请访问 `www.opensuse.org` 获取更多关于 SUSE Linux 的信息。

### Ubuntu Linux
这是一个相对较新的基于 Debian 的非商业 Linux 发行版，自 2004 年首次发布以来短时间内便广受欢迎。Ubuntu 提供安装 CD 和 Live CD 两种形式。由于基于 Debian，你可以从安装 CD 安装基本桌面系统，然后使用 `apt-get` 工具安装其他软件包以及保持系统更新。你可以从 `www.ubuntu.org` 免费下载 Ubuntu。

### Xandros Desktop OS
该发行版是 Corel Linux 的继承者，基于 Debian。Xandros 面向初次使用 Linux 的用户，其安装程序可以对硬盘进行重新分区。功能强大的 Xandros 文件管理器是 Xandros 的主要卖点。然而，Xandros 包含一些专有组件，防止其被重新分发。Xandros Desktop 的一个有限版本，称为开放流通版（Open Circulation Edition），可通过 BitTorrent 免费获取。请访问 `www.xandros.com` 获取更多关于 Xandros 的信息。

正如你在表 1-1 中的简要描述所见，一些 Linux 发行版，如 Knoppix 和 MEPIS，是以 Live CD 形式存在的。Live CD（或 Live DVD）包含一个 Linux 内核，你可以直接从 CD 或 DVD 启动并运行，而无需先将其安装到你的硬盘上。如果你想在决定安装之前先试用某个发行版，这种 Live CD 发行版会非常方便。

本书的随附光盘就像一个 Knoppix Live DVD。你只需从 DVD 启动 PC 并按下回车键即可运行 Knoppix。

许多 Linux 发行版，如 SUSE Linux 和 Xandros Desktop，是你可以在网上或电脑店、书店购买的产品。如果你听说过开源和 GNU（GNU's Not UN*X）许可证，你可能会认为没有人可以为了利润而销售 Linux。幸运的是，对于销售 Linux 发行版的公司来说，GNU 许可证——也被称为

## 什么是 Linux？

GNU 通用公共许可证（GPL）允许以营利为目的进行商业分发（但要求软件必须以源代码形式分发），并规定任何人都可以将该软件的源代码复制并分发给其他人。一些 Linux 发行版在 GPL 许可下免费获得，这意味着出版商可以随本书附带包含这些发行版的 DVD-ROM，并且你可以随意制作该 DVD 的副本。

### 理解版本号

Linux 内核和每个 Linux 发行版都有自己独立的版本号。随 Linux 发行版一起提供的额外软件程序（例如 GNOME 和 KDE）也有各自的版本号。Linux 内核和 Linux 发行版的版本号之间没有关联，但各自都有其特定的含义。

#### Linux 内核版本号

1994 年 3 月 14 日 Linux 内核版本 1.0 发布后，松散的 Linux 开发社区采用了一种版本号命名方案。诸如 1.x.y 和 2.x.y 这样、其中 x 为偶数的版本号被视为稳定版本。最后的数字 y 是补丁级别，随着问题的修复而递增。例如，2.6.14 是 Linux 内核的一个典型稳定版本。请注意，这些版本号的形式是由三个通过句点分隔的整数组成——主版本号.次版本号.补丁版本号——其中“主版本号”和“次版本号”分别表示主要和次要的版本号，而“补丁版本号”则表示补丁级别的另一个数字。

形式为 2.x.y 且 x 为奇数的版本号是仅供开发者使用的 beta 版；它们可能不稳定，因此你不应该将此类版本用于日常使用。例如，如果你发现 Linux 内核的版本号为 2.7.5，次版本号中的 7 会告诉你这是一个 beta 版。开发者会在这些奇数版本的 Linux 中添加新功能。

你可以在 `www.kernel.org` 在线查找有关 Linux 内核最新版本的信息。

#### 发行版特定的版本号

每个 Linux 发行版也有一个版本号。这些版本号通常遵循 x.y 格式，其中 x 是主版本号，y 是次版本号。

如今，如果次版本号为 0，它通常会被省略——例如 Fedora Core 4 和 Fedora Core 5。与 Linux 内核版本号不同，奇数和偶数次版本号没有特殊含义。每个版本的 Linux 发行版都包含特定版本的 Linux 内核和其他主要组件，如 GNOME、KDE 以及各种应用程序。

活跃 Linux 发行版的开发者通常定期发布新版本的发行版——大约每六到九个月一次。例如，SUSE Linux 9.0 于 2003 年 10 月发布；9.1 于 2004 年 4 月发布；9.2 于 2004 年 10 月推出；9.3 于 2005 年 4 月发布；而 SUSE Linux 10.0 则于 2005 年 10 月首次亮相。通常，Linux 发行版的每个新的主版本都会提供显著的新功能。

Debian 在任何时候都至少有三个版本——`stable`（稳定版）、`unstable`（不稳定版）和 `testing`（测试版）。

- `Stable（稳定版）`：大多数用户更喜欢这种类型的发布，因为它是最新官方发布的发行版。
- `Unstable（不稳定版）`：这表明开发者正在针对此版本进行工作。
- `Testing（测试版）`：该版本包含经过一些测试但尚未准备好包含在稳定版发布中的软件包。

#### Linux 标准基础（LSB）

Linux 已经变得足够重要，以至于存在一个称为 Linux 标准基础（或简称 LSB）的标准。LSB 是一组二进制标准，应有助于减少各 Linux 发行版之间的差异并促进应用程序的可移植性。LSB 背后的理念是提供应用程序二进制接口（ABI），使软件应用程序能够在任何符合 LSB 标准的 Linux（或其他 UNIX）系统上运行。LSB 规范引用了 POSIX 标准以及许多其他标准，如 C 和 C++ 编程语言标准、X Window System 第 11 版 6 释放（X11R6）以及文件系统层次结构标准（FHS）。LSB 版本 1.2（通常称为 `LSB 1.2`）于 2002 年 6 月 28 日发布。LSB 1.3 于 2003 年 1 月推出，LSB 2.0 于 2004 年 8 月 30 日发布，LSB 3.0 于 2005 年 7 月 1 日发布，而 LSB 3.1 于 2005 年 10 月 31 日发布。

LSB 规范分为两部分——一个在所有处理器类型中保持不变的通用规范，以及一组硬件特定规范，每种处理器架构对应一个规范。例如，LSB 1.2 针对 Intel 32 位（IA32）和 PowerPC 32 位（PPC32）处理器具有架构特定规范。LSB 1.3 除了为 IA32 和 PPC32 制定的规范外，还增加了对 Intel 64 位（IA64）架构以及 IBM zSeries 31 位（S390）和 64 位（S390X）处理器的规范。LSB 2.0

![](img/792720823146d68f19fd50c99ebfce4b_40_0.png)

增加了对 AMD 64 位（AMD64 或 X86_64）处理器的规范。当前的 LSB 规范——LSB 3.0——支持七种处理器架构：IA32、IA64、PPC32、PPC64（64 位 PowerPC）、S390、S390X、X86_64。



存在一个 LSB 认证计划。截至目前，有几个 Linux 发行版——如面向 x86 的 Red Hat Enterprise Linux 3、SUSE Linux 9.1 和 Sun Java Desktop System（JDS）2——已获认证为符合 LSB 1.3 的 IA32 运行时环境。其他几个——如 Linux 9.3、MandrakeLinux Corporate Server 3.0、带有 Service Pack 1 的面向 x86 的 Novell Linux Desktop 9、SUSE Linux 9.2 和 RAYS LX 1.0（来自 Sun Wah Linux Limited）——已获认证为符合 LSB 2.0 的 IA32 运行时环境。SUSE Linux 10.0 是首批符合 LSB 3.0 的 IA32 运行时环境之一。可以期待在未来不久会有更多发行版获得 LSB 3.0 认证。

如需了解有关 LSB 的更多信息，请访问 `www.linuxbase.org`。最新的 LSB 认证系统列表可在以下地址获取：

```
www.opengroup.org/lsb/cert/cert_prodlist.tpl
```

# Linux 发行版包含的内容

Linux 发行版自带 Linux 内核和大量其他软件。这些软件包包括从图形桌面到 Internet 服务器再到用于创建新软件的编程工具在内的所有东西。在本节中，我将简要描述一些随典型 Linux 发行版捆绑提供的主要软件包。如果没有这些捆绑软件，Linux 不会像今天这样流行。

![](img/792720823146d68f19fd50c99ebfce4b_41_0.png)

## GNU 软件

Linux 发行版的核心是源自 GNU 项目的软件集合。只有当你通过文本终端使用 Linux 系统时，你才会熟悉这些 GNU 实用程序——这是一个基本的命令行界面，屏幕上几乎不显示任何内容，除了一个你可以输入命令的提示符。（或者你可以使用一个模拟文本终端的图形窗口，同时仍然可以使用 GNU 实用程序。）GNU 软件是任何 Linux 发行版的基本组成部分之一。

作为 Linux 用户，你可能没有意识到所有 Linux 发行版在多大程度上依赖 GNU 软件。你在 Linux 系统中执行的几乎所有任务都涉及一个或多个 GNU 软件包。例如，GNOME 图形用户界面（GUI）和命令解释器（即 `bash`）都是 GNU 软件程序。顺便说一下，`shell` 是接受你输入的命令并响应这些命令运行程序的命令解释器应用程序。如果你重新编译内核或开发软件，你将使用 GNU C 和 C++ 编译器（这是伴随 Linux 的 GNU 软件的一部分）来完成这些任务。如果你使用 `ed` 或 `emacs` 编辑器编辑文本文件，你再次是在使用 GNU 软件包。这样的列表可以无限延伸。

### TECHNICAL STUFF（技术细节）

表 1-2 列出了随大多数 Linux 发行版附带的一些知名 GNU 软件包。我列出此表只是为了让你感受一下你可以使用 GNU 软件做的各种不同类型的事情。根据你的兴趣，你可能永远不需要使用其中许多软件包，但知道在需要时它们存在是有好处的。

**表 1-2 知名 GNU 软件包**

| *软件包* | *描述* |
| :--- | :--- |
| autoconf | 生成自动配置源代码包的 shell 脚本 |
| automake | 生成用于与 autoconf 一起使用的 Makefile.in 文件 |
| bash | Linux 中的默认 shell（命令解释器） |
| bc | 具有任意精度数字的交互式计算器 |
| Binutils | 包含若干用于处理二进制文件的实用程序的软件包：ar, as, gasp, gprof, ld, nm, objcopy, objdump, ranlib, readelf, size, strings 和 strip |
*（续）*

## 18 Linux 发行版包含的内容

### 表 1-2（续）

| 软件包 | 描述 |
| :--- | :--- |
| coreutils | 一个结合了名为 Fileutils、Shellutils 和 Textutils 的三个独立软件包，并实现了诸如 `chgrp`、`chmod`、`chown`、`cp`、`dd`、`df`、`dir`、`dircolors`、`du`、`install`、`ls`、`ln`、`mkdir`、`mkfifo`、`mknd`、`mv`、`rm`、`rmdir`、`sync`、`touch`、`vd`、`basename`、`c`、`date`、`dirname`、`echo`、`env`、`expr`、`factor`、`false`、`groups`、`hostname`、`id`、`login`、`nice`、`no`、`pathchck`、`printenv`、`printf`、`pwd`、`seg`、`sleep`、`stty`、`su`、`tee`、`test`、`true`、`tty`、`uname`、`uptime`、`users`、`who`、`whoami`、`yes`、`cut`、`join`、`nl`、`split`、`tail`、`wc` 和 `and` 等实用工具 |
| GnuChess | 一款国际象棋游戏 |
| Gnu C Library | 供所有 Linux 程序使用 |
| cpio | 将文件归档复制到磁盘或从磁盘复制到文件系统的另一部分 |
| diff | 比较文件，并以多种不同格式显示逐行更改 |
| ed | 一种基于行的文本编辑器 |
| emacs | 一种可扩展、可定制的全屏文本编辑器和计算环境 |
| Findutils | 一个包含 `find`、`locate` 和 `xargs` 实用工具的软件包 |
| finger | 一个旨在让互联网用户相互获取信息的实用程序 |
| gawk | GNU 项目对 `awk` 编程语言的实现 |
| gcc | 用于 C、C++、Objective C 及其他语言的编译器 |
| gdb | 用于 C、C++ 和 Fortran 的源代码级调试器 |
| gdbm | 传统 `dbm` 和 `ndbm` 数据库库的替代品 |
| gettext | 一组允许软件维护人员将软件包的用户消息进行国际化（即让软件支持不同语言，如英语、法语、西班牙语、`and` 等）的实用工具 |
| ghostscript | PostScript 和可移植文档格式（PDF）语言的解释器 |
| ghostview | 一个 X Window System 应用程序，使 `ghostscript` 可以从 GUI 访问，允许用户在窗口中查看 PostScript 或 PDF 文件 |
| The GIMP | （GNU 图像处理程序）：类似 Adobe Photoshop 的图像处理程序 |
| GNOME | 为 Linux 用户可能执行的各种任务提供图形用户界面（GUI） |
| gnucircle | 一个在 GNOME 中工作的图形化电子表格（类似于 Microsoft Excel） |
| grep 软件包 | 包含用于查找匹配指定文本模式的行的 `grep`、`egrep` 和 `fgrep` 命令 |
| groff | 类似于 `troff` 的文档排版系统 |
| gtk+ | X Window System 的 GUI 工具包（用于开发 GNOME 应用程序） |
| gzip | 用于压缩和解压缩文件的 GNU 实用工具 |
| indent | 通过多种不同样式之一对 C 源代码进行缩进来格式化代码 |
| less | 一种类似于 `more` 的逐页显示程序，但具有额外功能 |
| libpng | 用于可移植网络图形（PNG）格式图像文件的库 |
| m4 | 传统 UNIX 宏处理器的实现 |
| make | 一个确定大型软件包中哪些文件需要重新编译并发出重新编译命令的实用工具 |
| mtools | 一组允许用户在 DOS 文件系统（通常是软盘）上读取、写入和操作文件的程序 |
| ncurses | 用于在纯文本终端上显示和更新文本的软件包 |
| patch | Larry Wall 程序的 GNU 版本，用于获取 `diff` 的输出并将这些差异应用于原始文件以生成修改后的版本 |
| rcs | （修订控制系统）：用于软件项目中源文件的版本控制和管理 |
| sed | `ed` 文本编辑器的面向流版本 |
| Sharutils | 一个包含 `shar`（用于将许多文件制成 shell 归档）和 `unshar`（用于解压这些 shell 归档）的软件包 |
| tar | 一种包含多卷支持的磁带归档程序；具备归档*稀疏文件*（包含大量全零数据块的文件）、处理压缩和解压缩、创建远程归档以及其他增量和全备份特殊功能的能力 |
| texinfo | 一组生成打印手册、纯 ASCII 文本和在线超文本文档（称为 *info*）的实用工具，并允许用户查看和阅读在线 `info` 文档 |



| `time` | 一个报告进程使用的用户时间、系统时间和实际时间的实用工具 |

### GUI 和应用程序

承认吧——在终端上输入晦涩的 Linux 命令很无聊。对于普通用户来说，通过*图形用户界面*（GUI，发音为 *G00-ee*）——一种提供可点击图片和小窗口（w）进行打开的界面——使用系统要容易得多。这时，X Window 系统（或简称 X）就派上用场了。

X 有点像 Microsoft Windows，但 X 工作原理的底层细节与 Windows 完全不同。X 提供了在屏幕上显示窗口的基本功能，但（与 Microsoft Windows 不同）它不附带任何特定的图形应用程序外观或感觉。那种外观和感觉来自于利用 X Window 系统的 GUI，例如 GNOME 和 KDE。

大多数 Linux 发行版都包含 X Window 系统，形式为 XFree86 或 X.Org X11——这是适用于 80x86 系统的 X Window 系统实现。XFree86 和 X.Org X11 可与当今 PC 可用的各种视频卡配合使用。

![](img/792720823146d68f19fd50c99ebfce4b_45_0.png)

直到 2004 年初，XFree86（XFree86 项目 [www.xfree86.org](http://www.xfree86.org)）是最常用于 x86 系统的 X Window 系统实现。然而，大约在 4.4 版本时，XFree86 许可条款的一些变更引起了许多 Linux 和 UNIX 供应商的担忧——他们认为许可条款不再与 GNU 通用公共许可证（GPL）兼容。2004 年 1 月，几家供应商成立了 X.Org 基金会（[www.x.org](http://www.x.org)），以促进开源 X Window 系统和图形桌面的持续开发。X.Org X11 的首次发布使用了 XFree86 4.4 使用过的相同代码，直到 XFree86 许可条款变更导致 X.Org 基金会成立之时。

至于 GUI，Linux 发行版包含两种流行的 GUI 桌面环境之一或两者：KDE（K Desktop Environment）和 GNOME（GNU Object Model Environment）。如果在 PC 上同时安装了 GNOME 和 KDE，你可以选择哪个桌面作为默认——或者在两者之间切换。KDE 和 GNOME 提供类似 Microsoft Windows 和 Mac OS 的桌面。GNOME 还附带 Nautilus 图形外壳，使得查找文件、运行应用程序和配置 Linux 系统变得容易。使用 GNOME 或 KDE，你可以开始使用 Linux 工作站而无需知道晦涩的 Linux 命令。然而，如果需要直接使用这些命令，只需打开一个终端窗口并在提示符下输入即可。

Linux 还附带许多图形应用程序。最值得注意的程序是 The GIMP（GNU 图像处理程序），一个用于处理照片和其他图像的程序。The GIMP 的能力与 Adobe Photoshop 相当。

提供常见的生产力软件——如文字处理、电子表格和数据库应用程序——曾是 Linux 的不足之处。但这种情况已经改变。Linux 附带 OpenOffice.org 办公生产力应用程序。此外，您可能想看看这些未在本书配套 DVD-ROM 中包含的知名、商业可用的 Linux 办公生产力应用程序：

- AppIixware：这款办公套件是 Linux 生产力软件的一个良好范例。您可以在 www.vistasource.com 找到它。
- StarOffice：来自 Sun Microsystems（[www.sun.com/staroffice](http://www.sun.com/staroffice)），StarOffice 是另一个众所周知的生产力软件包。
- CrossOver Office：来自 CodeWeavers（[www.codeweavers.com/products/cxoffice](http://www.codeweavers.com/products/cxoffice)），您可以使用 CrossOver Office 在 Linux 中安装 Microsoft Office 应用程序（Office 97、Office 2000 和 Office XP）以及几个其他 Windows 应用程序。

如您所见，与 Microsoft Office 兼容的 Linux 办公应用程序并不缺乏。

# 网络

Linux 附带了在网络中使用该系统所需的一切，以便系统可以与其他系统交换数据。在网络上，交换数据的计算机必须遵循明确定义的规则，即协议。网络协议是发送方和接收方在网络上交换数据时所约定的方法。这样的协议类似于你在派对上与某人进行礼貌对话时可能遵循的规则。通常你以打招呼、交换姓名开始，然后轮流说话。网络协议的工作原理大致相同。两台计算机使用相同的协议在网络上往返发送比特和字节。

最著名和流行的网络协议之一是传输控制协议/网际协议（TCP/IP）。TCP/IP 是互联网的首选协议——互联网是如今遍布全球的“网络的网络”。Linux 支持 TCP/IP 协议以及任何利用 TCP/IP 的网络应用程序。

# Internet 服务器

一些流行的网络应用程序专门设计用于将一个系统的信息传递到另一个系统。当您使用 Web 浏览器发送电子邮件（e-mail）或访问网站时，您就在使用这些网络应用程序（也称为 Internet 服务）。以下是一些常见的 Internet 服务：

- 电子邮件（e-mail），用于通过诸如 joe@someplace.com 等地址向 Internet 上的任何人发送消息
- 万维网（或简称为 Web），您使用 Web 浏览器浏览它
- 新闻服务，您可以在其中阅读新闻组并向诸如 comp.os.linux.networking 或 comp.os.linux.setup 等名称的新闻组发布新闻条目
- 你可以用来上传和下载文件的文件传输工具
- 你可以用来连接到互联网上的另一台计算机（远程计算机）并与其交互的远程登录——前提是你拥有访问该远程计算机所需的用户名和密码

任何 Linux 电脑都可以提供这些互联网服务。要做到这一点，该电脑必须连接到互联网，并且必须运行称为互联网服务器的特殊服务器软件。每个服务器都使用特定的协议来传输信息。例如，以下是你在 Linux 中会找到的一些常见互联网服务器：

- `sendmail` 是使用 SMTP（简单邮件传输协议）在系统之间交换电子邮件消息的邮件服务器。
- `Apache httpd` 是使用 HTTP（超文本传输协议）将文档从一个系统发送到另一个系统的 Web 服务器。
- `vsftpd` 是使用 FTP（文件传输协议）在互联网上的计算机之间传输文件的服务器。
- `inn` 是使用 NNTP（网络新闻传输协议）以存储转发方式在互联网上分发新闻文章的新闻服务器。
- `in.telnetd` 允许一个系统上的用户通过 TELNET 协议登录到互联网上的另一个系统。
- `sshd` 允许一个系统上的用户通过 SSH（安全外壳协议）安全地登录到互联网上的另一个系统。

# 软件开发

Linux 特别适合软件开发。开箱即用，它配备了丰富的软件开发工具，例如编译程序和构建程序所需的代码库。如果你碰巧熟悉 UNIX 和 C 编程语言，你会发现在 Linux 中编程如鱼得水。

就开发环境而言，Linux 拥有与其他 UNIX 工作站（例如来自 IBM、Sun Microsystems 和 Hewlett-Packard (HP) 的工作站）上常用的基本工具（如编辑器、编译器和调试器）相同。这意味着，如果你白天在其中一台 UNIX 工作站上工作，你可以在晚上使用家用 Linux 电脑以极低的成本复制该开发环境。然后，你可以在家完成工作项目，或者将时间花在编写供娱乐和在互联网上分享的软件上。

![](img/792720823146d68f19fd50c99ebfce4b_48_0.png)

为了让你对 Linux 的软件开发支持有一个了解，这里列出了使 Linux 成为高效软件开发环境的各种功能：

- `GNU C 编译器` (`gcc`)：可以编译 ANSI 标准 C 程序。
- `GNU C++ 编译器` (`g++`)：支持 ANSI 标准 C++ 特性。
- `GNU Java 编译器` (`gcj`)：可以编译用 Java 编程语言编写的程序。
- `GNU make 实用程序`：允许你编译和链接大型程序。
- `GNU 调试器` (`gdb`)：允许你逐步执行程序以查找问题，并确定程序在哪里以及如何失败。（失败程序的内存映像保存在名为 `core` 的文件中；`gdb` 可以检查此文件。）
- `GNU 性能分析实用程序` (`gprof`)：允许你确定某段软件使用计算机处理器时间的程度。
- `Subversion`、`Concurrent Versions System (CVS)` 和 `Revision Control System (RCS)`：维护版本信息并控制对源文件的访问，以防止两名程序员同时意外修改同一个源文件。



- GNU `emacs` 编辑器：准备源文件，甚至启动编译链接过程来构建程序。
- `Perl`：是一种脚本语言，你可以用它编写脚本来完成特定任务，将许多较小的程序与 Linux 命令结合在一起。
- `Tcl`：一种与 Perl 和 Tcl 相当的解释型编程语言。（例如，名为 `anaconda` 的 Fedora Core 安装程序是用 Python 编写的。）
- 工具命令语言及其图形工具包 (`Tcl`/`Tk`)：使你能快速构建图形应用程序。
- `Python`：一种与 Perl 和 Tcl 相当的解释型编程语言。（例如，名为 `anaconda` 的 Fedora Core 安装程序是用 Python 编写的。）
- 动态链接共享库：使你的实际程序文件小得多，因为多个程序可能需要的所有库代码都是共享的——系统中只加载一个副本。

### 在线文档

当你越来越熟练地使用 Linux 时，你可能希望快速查找信息——例如，无需翻阅这本（咳咳）大书。幸运的是，Linux 提供了足够的在线信息，可以在你模糊记得某个命令的名称但记不清确切语法的情况下帮助你唤起记忆。

## 24 Linux 帮助你知道管理什么

如果你使用 Linux 命令，可以使用 `man` 命令查看命令的手册页——通常称为 `man page`。 （你确实需要记住该命令才能访问在线帮助。）

你还可以从 GUI 桌面获取帮助。`GNOME` 和 `KDE` 桌面都附带了帮助查看器，用于查看在线帮助信息。大多数发行版在桌面菜单中包含帮助选项，或在桌面上放置一个帮助图标，你可以选择它以获取在线帮助。然后，你可以通过单击初始帮助窗口上的链接来浏览帮助信息。图 1-1 显示了一个典型的帮助窗口——这是来自 Ubuntu 的 `GNOME` 桌面的窗口。

![](img/792720823146d68f19fd50c99ebfce4b_49_0.png)

**图 1-1:** 可以从 GUI 桌面获取在线帮助。

## Linux 帮助你知道管理什么

作为一个操作系统，Linux 充当中间层，通过它——作为“系统领主”——你可以管理所有硬件。硬件包括系统机箱、显示器、键盘、鼠标以及连接到系统机箱的其他任何设备。通用术语`外围设备`指连接到系统的任何设备。如果你使用笔记本电脑，你的所有硬件都打包在笔记本电脑中。

在那个系统机箱内部是系统的大脑——微处理器（例如 Intel Pentium 4）或 CPU——它执行包含在计算机程序中的指令。当微处理器运行计算机程序时，该程序的指令存储在内存或`RAM`中。`RAM` 代表随机存取存储器。（这意味着内存的任何部分都可以随机访问——即按任意顺序访问。）

系统机箱还有另一个关键组件——硬盘（或有时称为磁盘）。硬盘是计算机程序和数据永久存储的空间。说是永久，是指当你关闭 PC 电源时，其中的内容不会消失。硬盘组织成文件，文件又组织成目录和子目录（有点像在文件柜抽屉内的文件夹中整理纸张）。

为了让 Linux 系统正常运行，你或某人必须确保硬件正常运行，并且定期备份文件。还有`安全`的问题——确保只有合法人员可以访问和使用该系统。这些任务称为`系统管理`。

如果你在大型机构中使用许多台计算机上的 Linux，专职系统管理员可能负责所有系统管理任务。另一方面，如果你在家用 PC 上运行 Linux，你就是系统管理员。不要为此感到害怕。你不需要知道任何魔法咒语或准备晦涩的配置文件就能成为系统管理员。大多数 Linux 发行版包含许多图形工具，使系统管理成为`点击`工作，就像运行其他应用程序一样简单。

### 磁盘、CD-ROM 和 DVD-ROM

一些 Linux 发行版提供在单张 DVD-ROM 上。安装后，Linux 内核和所有应用程序都存储在你的硬盘上——这是当你告诉 PC 做某事时它首先查找的地方。

通常，硬盘在安装过程中准备用于 Linux。之后，你通常不碰硬盘，除了备份存储在那里的数据或（偶尔）安装新应用程序。

在 Linux 中使用 CD-ROM 或 DVD-ROM 很容易。当你登录在 `GNOME` 或 `KDE` 桌面时，只需将 CD 或 DVD 插入驱动器，系统应该会自动检测 DVD/CD-ROM。根据 Linux 发行版的不同，桌面上会出现 DVD/CD-ROM 图标，或者文件管理器会自动打开并显示 DVD/CD-ROM 的内容。如果其他方法都失败，你可以输入简单的 `mount` 命令将 DVD/CD-ROM 与系统上的目录关联。从 Linux 访问 CD 或 DVD 上文件的整个过程称为`挂载`该 CD 或 DVD。

当然，除了硬盘和 DVD/CD-ROM 驱动器，你的 PC 可能还有其他驱动器，例如软盘驱动器或 Zip 驱动器，在 Linux 中使用这些磁盘也很简单：你插入磁盘并双击 GUI 桌面上代表磁盘驱动器的图标。这样做会挂载磁盘，以便你可以开始使用它。

## 外围设备

任何连接到你的 PC 的外围设备，以及安装在系统机箱内部的某些组件（如声卡）都属于外围设备。你可以在 Linux 中配置和管理这些外围设备。

常见的外围设备之一是打印机，通常连接到你的 PC 的并口。（许多发行版都附带图形化打印机配置工具，你可以使用它来配置打印机。）

另一个需要配置的外围设备是声卡。大多数 Linux 发行版都能检测和配置声卡，就像 Windows 一样。然而，如果 Linux 无法正确检测声卡，你可能需要运行文本模式或图形化工具来配置声卡。

Linux 在安装时会自动配置其他外围设备，例如鼠标和键盘。安装完成后，你基本上可以不去管它们。

如今，PC 配备了 `USB`（通用串行总线）接口；许多设备，包括打印机和扫描仪，都插入到 PC 的 `USB` 端口。`USB` 设备的一个优点是你可以随时将它们插入或拔出 `USB` 端口——在系统开机时设备不必连接。这些设备被称为热插拔，因为你可以在系统“热”着的时候（即正在运行时）插入设备。Linux 支持许多热插拔 `USB` 设备。当你将设备插入 `USB` 端口时，Linux 会加载正确的驱动程序并使该设备对应用程序可用。

## 文件系统与共享

目录和文件的全部组织结构被称为文件系统。当然，你可以使用 Linux 来管理文件系统。当你在 `GNOME` 或 `KDE` 图形桌面中浏览文件时，你处理的是熟悉的文件夹图标。

![](img/792720823146d68f19fd50c99ebfce4b_51_0.png)

维护文件系统的关键任务之一是备份重要文件。在 Linux 中，你可以使用 `tar` 程序将一个或多个目录归档到软盘或 Zip 驱动器上。你甚至可以将文件备份到磁带上（如果你有一个磁带驱动器的话）。如果你有一个 CD 或 DVD 刻录机，你也可以将想要备份或留作后人的文件刻录到 CD 或 DVD 上。

Linux 还可以将文件系统的部分与其他网络上的系统进行共享。例如，你可以使用网络文件系统（`NFS`）与网络上的其他系统共享文件。对于系统上的用户来说，远程系统的文件看起来像是在本地系统的一个目录中。

Linux 还附带了 `Samba` 软件包，它支持与 Microsoft Windows 系统的文件共享。`Samba` 使 Linux 系统表现得像一个 Windows 文件或打印服务器一样。你还可以访问网络上其他 Windows 系统上的共享文件夹。

## 网络

既然大多数 PC 现在都位于局域网（`LAN`）中或连接到互联网，你就需要同时管理网络。Linux 附带了网络配置工具，用于设置局域网。对于使用调制解调器连接互联网，通常有一个图形化的互联网拨号工具。

如果你使用 `DSL`（那是电信公司的快速互联网连接）或电缆调制解调器连接到互联网，你需要一台带有以太网卡的 PC，该卡连接到电缆或 `DSL` 调制解调器。这也意味着你需要设置一个局域网并配置以太网卡。但幸运的是，这些步骤通常是 Linux 安装过程的一部分。如果你稍后想进行配置，可以使用图形化的网络配置工具。

Linux 还包括用于配置`防火墙`的工具，防火墙是一个保护性的缓冲层，有助于保护你的系统，使其相对安全，防止任何人试图窥探你的互联网连接。你可以使用 `iptables` 命令或运行图形化的防火墙配置工具来配置防火墙。

## 入门指南

根据我在探索新主题方面的个人经验，我制定了一个四步流程来开始使用 Linux：

- 1. 在你的 PC 上安装 Linux
- 2. 配置 Linux，使一切符合你的喜好
- 3. 探索图形桌面和应用
- 4. 了解特定主题的细节，例如互联网服务器

在接下来的章节中，我将更详细地解释这个流程。

### 安装

你的新 PC 通常预装了 Microsoft Windows，但通常不包含 Linux。所以你的第一个障碍是如何在 PC 上安装 Linux。

在你克服了最初对未知事物的恐惧之后，我敢打赌你会发现 Linux 安装相当简单——但你首先要从哪里获取它呢？嗯，好消息是它是免费的——只需下载即可。例如，你可以访问 Linux 在线网站 www.linux.org 并点击“下载”按钮。

![](img/792720823146d68f19fd50c99ebfce4b_53_0.png)



因为典型的完整 Linux 发行版*体积巨大*——它占据多张 CD 或至少一张 DVD——你最好的选择是购买一本附带 Linux DVD-ROM 的书（比如这本）。然后用该 CD 或 DVD 启动 PC，这将启动 Linux 安装过程，创建 Linux 分区并从 DVD 安装 Linux 软件包。在此期间，你会配置许多项目——从以太网卡（如果有）到 X 窗口系统。

仅仅为了激发你的好奇心，安装过程涉及在硬盘上为 Windows 和 Linux 都创建空间。如果你想安装以 ISO 镜像文件形式存在的发行版，你必须为该发行版刻录一张 CD 或 DVD（取决于 ISO 镜像的大小）。然后用该 CD 或 DVD 启动 PC，这将启动 Linux 安装过程，创建 Linux 分区并从 DVD 安装 Linux 软件包。在此期间，你会配置许多项目——从以太网卡（如果有）到 X 窗口系统。

### 配置

完成 Linux 安装后，下一步是配置各个系统组件（例如声卡和打印机）并调整任何必要的设置。

如果你没有看到图形登录屏幕，可能是因为 X 窗口系统在安装期间未正确配置。你必须修复 X 配置文件才能让图形界面正常工作。

你可能还想配置你首选的图形桌面——GNOME 或 KDE，或者两者都配置。它们都有配置工具。你可以使用这些工具来调整桌面的外观和感觉（背景、标题字体，甚至整个配色方案）。

完成配置步骤后，你系统上的所有硬件和应用应该都能按你的喜好运行。

### 探索

拥有一台配置正确的 Linux PC，你就准备好探索 Linux 本身了。你可以从登录后的图形桌面开始探索。

探索图形桌面——GNOME 和 KDE——以及组成 Linux 文件系统的文件夹和文件。你还可以尝试桌面上的应用程序。你会发现办公、多媒体和互联网应用可供探索。

还要尝试 shell——打开一个终端窗口并输入一些 Linux 命令。你还可以探索在文本模式下工作的文本编辑器。了解如何在没有图形界面的情况下编辑文本文件，以防图形界面不可用，是个好主意。至少你不会无助。

### 深入了解

在你探索了 Linux 的大致情况并知道什么是什么之后，你可以更深入地挖掘，了解特定领域的更多细节。例如，你可能有兴趣设置互联网服务器。然后你可以学习设置各个服务器的细节，如用于电子邮件的 sendmail，用于 Web 服务器的 Apache，以及用于新闻的 INN 服务器。

你可以选择了解更多领域，如安全、编程和系统管理。

当然，你可以期待这一步持续进行，即使你的系统已经按你希望的方式运行——暂时如此。毕竟，学习是一生的旅程。

旅途愉快！

# 第 2 章：安装 Linux

## 本章内容

- 了解安装步骤
- 列出你 PC 的硬件
- 从 DVD 试用 Knoppix
- 为你的发行版刻录 CD 或 DVD
- 为 Linux 预留硬盘空间
- 安装 Debian
- 安装 Fedora Core
- 安装 MEPIS
- 安装 SUSE Linux
- 安装 Ubuntu
- 安装 Xandros Desktop

PC 通常预装 Microsoft Windows。如果你想使用 Linux，你必须首先安装它。

本书附带一张 DVD-ROM，其中包含多个 Linux 发行版——Debian、Fedora、Knoppix、MEPIS、SUSE、Ubuntu 和 Xandros。有些是完整的发行版，有些是可以直接在硬盘上试用的 Live CD。（*完整发行版*意味着包含安装这些发行版所需的一切，而*Live CD*意味着你可以直接从 CD 启动 Linux 的 CD。）

DVD 上的 Xandros 版本是 Xandros Desktop 的一个受限版本，称为*Open Circulation Edition*（开放流通版）。要安装或试用这些发行版中的任何一个，你只需遵循本章中的步骤即可。

你可能会对在你的 PC 上安装新的操作系统感到有点担心，因为这有点像脑外科手术——或者更准确地说，更像移植一个新大脑，因为你可以除了 Microsoft Windows 之外安装 Linux。当你像这样安装两个操作系统时，你可以在开机时选择启动其中一个或另一个。在装有 Windows 的 PC 上添加 Linux 最大的麻烦是创建一个新的*磁盘分区*——基本上是为 Linux 预留一个

## 32 遵循安装步骤

划出硬盘的一部分供 Linux 使用。其余的安装过程相当常规——只需遵循指示即可。如果你想试用任何一张 Live CD，你不需要进行任何磁盘分区，只需从 Live CD 启动你的 PC 即可。但最重要的是，请深呼吸，缓慢呼气。你无需担心，因为本章将解释所有内容。

### 遵循安装步骤

安装任何 Linux 发行版都涉及若干步骤。我希望简要地带你走一遍这些步骤，而不涉及细节。然后，你可以遵循针对特定发行版的详细步骤，从本书附赠的 DVD-ROM 中安装你想要的软件。

在解释 Linux 安装细节之前，我想先说明我是如何将几个 Linux 发行版打包在 DVD 上的。以下是关于随书 DVD 的信息：

- 这是一张 Fedora Core DVD，同时也包含 Knoppix，这意味着你可以从该 DVD 启动 PC，选择运行 Knoppix Live CD，或者直接安装 Fedora Core。
- 除了 Fedora Core 文件外，DVD 还包含一个 `distros` 文件夹，其中有几个子文件夹，分别对应 Debian、Knoppix、MEPIS、SUSE、Ubuntu 和 Xandros 等发行版。在每个文件夹中，你会发现该发行版的 ISO 映像文件（ISO 映像文件包含 CD 或 DVD 的完整内容和结构）。在使用它们安装相应发行版之前，你必须将这些 ISO 映像刻录到 CD（如果 ISO 映像专为 DVD 设计，则刻录到 DVD）上。
- SUSE 以 Live DVD ISO 映像文件的形式提供，你可以将其刻录到可刻录 DVD 上，从而无需将其安装在硬盘上即可在 PC 上运行 SUSE Linux。

一些 Linux 发行版要求你在安装前掌握关于你 PC 硬件的大量信息。如果你计划安装 Debian，建议在开始安装之前收集有关你 PC 及其外围组件的信息。幸运的是，大多数 Linux 安装程序都能检测并支持大多数 PC 外围设备。尽管如此，弄清楚你 PC 的硬件配置总是一个好主意，这样在安装出现问题时你可以进行故障排除。

第一步是将你所在发行版的 CD 或 DVD 刻录出来，除非你计划安装 Fedora Core 或 Knoppix。你可以在任何带有 CD/DVD 光驱的系统中刻录 CD。（如果你想刻录 DVD，必须拥有 DVD 光驱，但 DVD 光驱既可以刻录 CD 也可以刻录 DVD。）通常，如果你已经有一台带有 CD/DVD 光驱的 Windows PC，你可以简单地使用该系统来刻录 CD。请记住，你还必须有 DVD 驱动器，因为你必须从本书的随书 DVD-ROM 中读取 CD 进行刻录。

![](img/792720823146d68f19fd50c99ebfce4b_57_0.png)

一台具有 DVD 刻录机或组合 DVD-ROM 和 CD 刻录机的 PC 足以完成此任务。

![](img/792720823146d68f19fd50c99ebfce4b_58_0.png)

第二步是确保你的 PC 可以从 DVD/CD 驱动器启动。大多数新 PC 可以直接从 DVD/CD 驱动器启动，但有些 PC 可能需要你的干预。通常，PC 可能设置为先于 DVD/CD 驱动器从硬盘启动，你需要进入 `Setup` 设置以更改启动设备的顺序。

要设置 PC 从 DVD 驱动器启动，你需要在 PC 开机时进入 `Setup` 模式。进入 `Setup` 和设置启动设备的具体步骤因 PC 而异，但通常涉及按下一个键，如 `F2`。当 PC 启动时，会显示一条简短消息，告诉你按哪个键进入 `Setup`。进入 `Setup` 后，你可以将 DVD/CD 驱动器指定为启动设备。一旦你的 PC 设置为从 DVD/CD 驱动器启动，只需将 DVD 或 CD 放入 DVD/CD 驱动器并重新启动 PC 即可。

![](img/792720823146d68f19fd50c99ebfce4b_58_1.png)

如果你计划试用 Live CD 发行版，如 MEPIS 或 Knoppix，第三步是从 Live CD 或 DVD 启动 PC。否则，第三步是在你的 PC 硬盘上为 Linux 腾出空间。如果你正在运行 Microsoft Windows，这一步可能容易也可能困难，取决于你是想用 Linux 替换 Windows 还是同时保留 Windows 和 Fedora Core。

如果你想在不删除（或干扰）Windows 的情况下安装 Linux，请记住，你现有的操作系统——我假设是 Windows 95、98、Me、NT、2000 或 XP——使用了整个硬盘。这意味着你必须分区（划分）硬盘，以便 Windows 驻留在其中一部分，而 Linux 驻留在另一部分。这可能是一个令人担忧的步骤，因为你有损坏硬盘并清除驱动器上所有数据的风险。



为了在硬盘上为 Linux 安装程序腾出空间，你应该使用分区程序来帮助你创建分区。如果你的 PC 运行 Windows NT、2000 或 XP，你可能想要投资一款商业硬盘分区产品，例如 Symantec 的 `Norton PartitionMagic`（`www.powerquest.com/partitionmagic`），它同样适用于 Windows 95/98/Me 系统。另一方面，你只需启动 `Knoppix`，然后使用 `Knoppix` 附带的名为 `QTParted` 的 GUI（图形用户界面）工具即可重新分区你的 PC 硬盘。

![](img/792720823146d68f19fd50c99ebfce4b_58_2.png)

请注意，某些 Linux 发行版（如 `SUSE` 和 `Xandros Desktop`）的安装程序可以通过缩减 Windows 分区的大小来自动为 Linux 创建分区。在这种情况下，你无需使用 `PartitionMagic` 或 `QTParted` 等工具来缩减硬盘上现有 Windows 分区的大小。

在为你划出硬盘分区后，你可以从所选发行版的 CD 启动 PC 并开始安装 Linux。安装过程中会发生许多步骤，且因发行版而异。既然你已经走到这一步，接下来的过程应该很顺利。只需浏览安装界面，一两个小时后即可完成。大多数安装程序都会调出 GUI（有些人发音为 GOO-ee）并引导你完成所有步骤。安装过程中的一个关键步骤是再次对硬盘进行分区，但这一次，你只需使用之前创建的额外分区。在几个配置步骤之后，例如设置网络时区，你选择要安装的软件包，然后让安装程序完成剩余的安装工作。有些发行版使其更加简便，省略了软件选择步骤。它们安装一套默认的软件包。

安装结束时，你重启 PC。当 Linux 第一次运行时，你将有机会执行更多的配置步骤并安装额外的软件包。

## 检查你的 PC 硬件

如果你担心你的 PC 可能无法运行 Linux，以下是在开始 Linux 安装前需要考虑的 PC 关键组件：

- **DVD 驱动器：** 你必须有一个 DVD 驱动器（`DVD-ROM` 或 `DVD` 刻录机均可），并且 PC 必须能够从该驱动器启动。（例外：你可以使用本书后附的优惠券订购 `Fedora Core` 的安装 CD。）

  - 具体的型号并不重要。重要的是 DVD 驱动器如何连接到 PC。大多数新 PC 的 DVD 驱动器通过硬盘控制器（称为 `IDE`，即 Integrated Drive Electronics，或 `ATA`，即 AT Attachment）连接。如果你添加外部 DVD 驱动器，它很可能通过 `USB` 端口连接。任何 `IDE`/`ATA` 或 `USB` DVD 驱动器在 Linux 上都能工作。

- **硬盘：** 任何 `IDE` 磁盘驱动器都能在 Linux 上工作。另一种类型的硬盘控制器是 `SCSI`（Small Computer System Interface），Linux 也支持它。为了舒适地安装和玩弄 Linux，你大约需要 5GB 的硬盘空间。另一方面，为了试用 Linux 的 Live CD 版本，如 `Knoppix`，你不需要在硬盘上占用任何空间。

- **键盘：** 所有键盘都能与 Linux 和 X Window 系统配合使用。

- **调制解调器：** 如果你计划拨号连接到互联网，你需要一个 Linux 支持的调制解调器。对于基于软件的调制解调器，称为软调制解调器或 win-modems，你可能需要从制造商处下载驱动程序。（它可能免费获取，也可能不免费。）

## 检查您的 PC 硬件

- **显示器：** 显示器的类型并不特别关键，但它必须能够显示显卡所使用的屏幕分辨率。屏幕分辨率以水平方向和垂直方向的像素（*pixels*）数量来表示（例如，1024 x 768）。安装程序可以检测大多数现代显示器。如果它无法检测您的显示器，您可以选择具有特定分辨率的通用显示器类型（如 1024 x 768）。您也可以根据显示器的品牌和型号（这可以在显示器的背面找到）来指定显示器。

- **鼠标：** 安装程序可以检测鼠标。所有类型的鼠标（如 `PS/2` 或 `USB`）都可以与 Linux 和 X 窗口系统配合使用。

- **网卡：** 并非所有 PC 都有网卡，但如果您的 PC 有，安装程序通常可以检测并使用它。如果遇到问题，请尝试查找网卡的品牌和型号（例如 `Linksys LNE100TX` 快速以太网适配器），以便您可以搜索 Linux 是否支持该网卡的信息。

- **处理器：** 最好是 400 MHz Pentium II 或更高级别的处理器。只要速度超过 400 MHz，处理器速度（以 `MHz`（兆赫兹）或 `GHz`（吉赫兹）表示）并不是很重要。但越快越好。Linux 也可以在其他 Intel 兼容处理器上运行，例如 AMD、Cyrix 和 VIA 处理器。

- **内存：** `RAM` 是您系统的内存量。与处理速度一样，内存越多越好。您需要 256MB 内存来安装 Linux 和 X 窗口系统，并舒适地运行图形用户界面桌面。

- **SCSI 控制器：** 一些高性能 PC 配有 `SCSI` 控制器，用于将磁盘驱动器和其他外设连接到 PC。如果您的 PC 恰好拥有 `SCSI` 控制器，您可能想要查找该控制器的品牌和型号。

- **声卡：** 如果您的 PC 有声卡并且您希望在 Linux 中有声音，您需要确保其兼容性。您可以在成功安装 Linux 后配置声卡。

- **显卡：** Linux 在文本模式下与所有显卡（也称为 *显示适配器*）配合良好，但如果您想要图形用户界面，您需要一张支持 X 窗口系统的显卡。安装程序可以检测支持的显卡并正确配置 X 窗口系统。然而，如果安装程序无法检测显卡，了解显卡的品牌和型号会有所帮助。

- **打印机：** 除了这些硬件之外，您还需要查找您计划在 Linux 中使用的任何打印机的品牌和型号。

![](img/792720823146d68f19fd50c99ebfce4b_60_0.png)

许多发行版，如 `Debian GNU/Linux`，可以在任何与 Linux 内核兼容的硬件上运行。有关 Linux 兼容硬件的信息，请访问 `www.tldp.org/HOWTO/Hardware-HOWTO`。

![](img/792720823146d68f19fd50c99ebfce4b_61_0.png)

要检查您的 PC 硬件是否与 `SUSE Linux` 兼容，请访问位于 `http://hardwaredb.suse.de` 的 `SUSE Linux` 硬件兼容性列表。对于 `MEPIS`，请查阅位于 `www.mepisusers.org/hwdatabase` 的 `MEPIS` 硬件数据库。`Ubuntu` 的硬件兼容性列表位于 `https://wiki.ubuntu.com/HardwareSupport/`。对于 `Xandros Desktop`，您可以在 `www.xandros.com/support/hcl.html` 找到硬件兼容性列表。

## 试用 Knoppix Live CD

在安装任何内容之前，值得一试的是从随附 DVD 中试用 `Knoppix`（K 不发音）。除了熟悉 Linux 桌面的感觉外，您还可以从 `Knoppix` 中执行一些额外的安装前任务。如果您决定安装 `Fedora` 以外的发行版——`Debian`、`MEPIS`、`SUSE`、`Ubuntu` 或 `Xandros`——您可以将本书随附 DVD 上提供的 ISO 镜像文件中的 CD 或 DVD 刻录出来。您也可以使用 `Knoppix` 下的 `QTParted` 工具在硬盘上为 Linux 腾出空间。

要启动 `Knoppix`，请遵循以下步骤：

1. **从本书的随附 DVD 启动您的 PC。**

   会出现 `boot:` 提示符。在此提示符下，您可以输入各种命令来控制启动过程。特别是，您可以输入命令来禁用某些可能正在导致安装失败的硬件检测类型。

2. **几分钟后，您将看到 `Knoppix` 使用的 `KDE` 图形用户界面桌面。**

   您现在可以开始使用 `Knoppix`。

![](img/792720823146d68f19fd50c99ebfce4b_61_1.png)

如果您在笔记本电脑上尝试 `Knoppix` 并且在显示关于探测 `SCSI`（这是一种接口类型的名称）的消息后挂起，请重新启动。当出现 `boot:` 提示符时，输入 `knoppix noisci`。通过告诉 `Knoppix` 不要检查 `SCSI`，这应该能让您通过该问题。对于遇到 `ACPI`（高级配置和电源接口）问题的 PC，请在启动提示符处输入 `knoppix acpi=off`。在启动提示符处按 `F3` 可获取 `Knoppix` 启动选项列表。

获得 `Knoppix` 桌面后，您可以开始探索 `Knoppix`。有关试用 Linux 的更多信息，请参阅本小册子的第 4 章。如果您想使用 `Knoppix` 刻录 CD 或调整硬盘分区大小，请参阅本章中的“使用 `Knoppix` 刻录 CD 或 DVD”部分和“使用 `Knoppix` 中的 `QTParted` 调整分区大小”部分。



当您结束使用 Knoppix 时，选择主菜单:注销，并在出现的 KDE 结束会话对话框中选择重新启动计算机。Knoppix 关闭后，取出 DVD 并按 Enter 键。

## 从 ISO 镜像刻录 CD 或 DVD

本书的随附 DVD 包含以 ISO 镜像形式存在的 Debian、MEPIS、SUSE、Ubuntu 和 Xandros 发行版，它们被组织在 DVD 的 `distros` 文件夹中的不同文件夹里。要安装这些发行版中的任何一个，您首先必须根据情况将所选发行版的 ISO 镜像刻录到 CD 或 DVD 上。通常，您可以在拥有 CD/DVD 刻录机的 PC 上执行此步骤，最可能是在使用 Microsoft Windows 的情况下，因为大多数新 PC 都预装了 Windows。另一种选择是从随附 DVD 启动 Knoppix，然后使用 Knoppix 刻录 CD 或 DVD。我在接下来的两个部分中描述了这些选项。

### 使用 CD 刻录应用程序

在 Microsoft Windows 中，您可以使用 CD 刻录应用程序（如 Nero）将 ISO 镜像刻录到可录制 CD 上。如果您没有用于 Microsoft Windows 的 CD 刻录应用程序，请从 DVD 启动 Knoppix，并从图形用户界面桌面选择主菜单→多媒体→K3b 以启动 CD/DVD 刻录应用程序。从 ISO 镜像刻录 CD 的具体步骤取决于您使用的 CD 刻录应用程序。一般步骤如下。（如果您拥有 DVD 刻录机，请使用相同的说明来刻录 DVD。）

1. **将随附 DVD-ROM 放入 PC 的 DVD 驱动器中。**

如果您的 DVD 驱动器是组合 DVD/CD 刻录机，您必须首先将 Linux 发行版的 ISO 镜像文件从 DVD 复制到 PC 硬盘，以便您可以使用同一驱动器来刻录 CD。

2. **启动 CD 刻录应用程序。**

3. **从 CD 刻录应用程序打开镜像文件。**

具体步骤取决于 CD 刻录应用程序。在 Knoppix 下的 K3b 中，从菜单中选择 工具→CD→刻录 CD 镜像。在其他 CD 刻录应用程序中，通常通过选择 文件→打开 来执行此操作。在 打开 对话框中，选择该发行版的 ISO 镜像文件。如果您不确定，请搜索该应用程序的在线帮助以获取有关从 ISO 镜像刻录 CD 的信息。

4. **将一张空白可录制 CD 放入 CD 刻录机中。**

5. **将 ISO 镜像刻录到可录制 CD 上。**

通常，CD 刻录应用程序有一个工具栏按钮，您可以点击它以开始将 ISO 镜像刻录到空白 CD 上。

6. **如果发行版有多个 ISO 镜像，请对剩余的 ISO 镜像重复步骤 2 至 4。**

Live CD 发行版以单个 ISO 镜像形式提供，您可以将其刻录在单个 CD 上。其他发行版通常以多个 ISO 镜像形式提供，您必须将每个镜像文件刻录到单独的 CD 上。

![](img/792720823146d68f19fd50c99ebfce4b_62_0.png)

## 使用 Knoppix 刻录 CD 或 DVD

如果你有一台 DVD-ROM 光驱和一台独立的 DVD/CD 刻录机，你可以从配套 DVD 启动 Knoppix，然后使用 Knoppix 刻录 CD 或 DVD。在这种情况下，Knoppix 将从 DVD-ROM 光驱运行，而你仍然可以使用独立的 DVD/CD 刻录机刻录 CD 或 DVD。

Knoppix 启动后，通过点击桌面面板上的终端程序图标来打开一个终端窗口。你可以使用 `cdrecord` 命令刻录 CD，并使用 `growisofs` 命令刻录 DVD。

以下是使用 `cdrecord` 在空白可刻录 CD 上刻录 ISO 镜像的步骤：

- 1. **输入** `cdrecord -scandbus` **并查看输出结果末尾从** `scsibus0` **行开始的部分。**

例如，以下是一台配备 DVD 刻录机的 PC 该命令输出的相关部分：

```
scsibus0:
      0,0,0  0) 'SONY   ' 'DVD RW DRU-800A ' 'KYD1' Removable
    CD-ROM
      0,1,0  1) *
      0,2,0  2) *
      0,3,0  3) *
      0,4,0  4) *
      0,5,0  5) *
      0,6,0  6) *
      0,7,0  7) *
```

请注意你想使用的 DVD/CD 刻录机对应的由逗号分隔的三个数字。在本例中，这些数字是 0,0,0。在第 5 步的 `cdrecord` 命令中，使用这些数字作为 `dev` 选项的值。

- 2. **输入** `cd /cdrom/distro` **将目录更改为 DVD-ROM 上 ISO 文件所在的位置。**

- 3. **使用** `cd` **命令切换到你想要刻录到 CD 上的发行版 ISO 文件所在的子目录。输入** `ls -l` **以查看 ISO 文件的名称。**

- 4. **将一张空白可刻录 CD 放入刻录机中。**

- 5. **输入以下命令来刻录 CD，但请将** `filename.iso` **替换为你的发行版 ISO 镜像文件的名称：**

```
cdrecord -v -pad speed=1 dev=0,0,0 filename.iso
```

![](img/792720823146d68f19fd50c99ebfce4b_63_0.png)

如果 `cdrecord` 命令不起作用，只需从 Knoppix 桌面选择 **主菜单 > 多媒体 > K3b**。这将启动 K3b CD/DVD 刻录应用程序。然后，你可以按照“使用 CD 刻录应用程序”部分中的说明来刻录 CD。

在可刻录 DVD 上刻录 DVD ISO 镜像同样简单。以下是步骤：

- 1. **输入** `cdrecord -scanbus` **并查看输出结果末尾从** `scsibus0` **行开始的部分。**

例如，以下是一台配备 DVD 刻录机的 PC 该命令输出的相关部分：

```
scsibus0:
    0,0,0    0) 'SONY    ' DVD RW DRU-800A ' 'FY01' Removable
    CD-ROM     0,1,0    1) *
    0,2,0    2) *
    0,3,0    3) *
    0,4,0    4) *
    0,5,0    5) *
    0,6,0    6) *
    0,7,0    7) *
```

请注意从 0 到 7 的第二列数字，其中列出了 DVD 刻录机。在本例中，DVD 刻录机位于编号 0。对于这个编号，在第 5 步的 `growisofs` 命令中，使用 `/dev/scd0` 作为设备名称。请记住将设备名称中的 0 更改为与 `cdrecord -scanbus` 命令输出中对应你 DVD 刻录机的编号相匹配的数字。

- 2. **输入** `cd /cdrom/distros` **将目录更改为本书配套 DVD 上 ISO 文件所在的位置。**

你从 DVD 启动了 Knoppix，因此 DVD 仍在 DVD-ROM 光驱中。

- 3. **使用** `cd` **命令切换到你想要刻录到 CD 上的发行版 ISO 文件所在的子目录。输入** `ls -1` **以查看 ISO 文件的名称。**

- 4. **将一张空白可刻录 DVD 放入刻录机中。**

- 5. **输入以下命令来刻录 DVD，但请将** `filename.iso` **替换为你的发行版 ISO 镜像文件的名称：**

```
growisofs -dvd-compat -Z /dev/scd0=filename.iso
```

![](img/792720823146d68f19fd50c99ebfce4b_64_0.png)

本书 DVD 中包含的大多数 ISO 镜像都足够小，可以放在 CD 上。不过，如果你愿意，也可以将任何 CD ISO 镜像刻录到 DVD 上。SUSE 的 ISO 镜像需要 DVD。

## 为 Linux 留出空间

在典型的 Windows PC 中，Windows 位于一个大的分区上，占用了整个硬盘。你需要缩小该分区并为 Linux 腾出空间。在安装 Linux 期间，安装程序会使用空闲空间来创建 Linux 分区。



要试用任何 Live CD 发行版——`Knoppix` 或 `MEPIS`——你不需要重新划分硬盘分区。只需从 Live CD 启动 PC，你就可以开始使用这些发行版。`MEPIS`、`SUSE` 和 `Xandros` 安装程序可以非破坏性地缩小 Windows 分区（执行与 `PartitionMagic` 等工具相同的功能），因此你无需事先执行重新划分分区步骤。如果你计划在硬盘上安装 `Fedora Core`、`Debian` 或其他任何 Linux 发行版，则必须重新划分硬盘分区。如果你想在 Windows 下调整磁盘分区大小，可以使用 `Norton PartitionMagic`（来自 `Symantec`）在所有 Microsoft 操作系统中调整并分割磁盘分区，范围从 Windows 95/98/Me 到 Windows NT/2000/XP。这是一款商业产品，因此你必须购买才能使用。在我撰写本文时，`Norton PartitionMagic 8.0` 的定价为 69.95 美元。你可以在 `www.powerquest.com/partitionmagic` 上阅读相关内容并购买。

![](img/792720823146d68f19fd50c99ebfce4b_65_0.png)

如果你还没有 `PartitionMagic`，不必花钱购买。只需从本书的配套 DVD 启动 `Knoppix`，然后使用 `QTParted`（一个图形界面工具）来调整 Windows 分区的大小。`QTParted` 可以调整 Windows 2000 和 XP 使用的 NTFS 分区的大小。

![](img/792720823146d68f19fd50c99ebfce4b_65_1.png)

调整磁盘分区大小总是涉及丢失硬盘上所有数据的风险。因此，在使用 `PartitionMagic` 等磁盘分区工具调整硬盘分区大小之前，**备份你的硬盘**。在进行备份之后——以及在你对分区进行任何操作之前——请确保你可以从备份中恢复文件。

![](img/792720823146d68f19fd50c99ebfce4b_65_2.png)

### 使用 PartitionMagic 调整 Windows 分区大小

当你运行 `PartitionMagic` 时，它会在窗口中显示当前分区。如果你正在运行 Windows XP，你的硬盘通常有两个分区：一个小的、隐藏的分区，其中包含 Windows XP 安装文件，以及一个巨大的第二个 NTFS 分区，充当 C: 驱动器。你必须减小现有 C: 驱动器的大小。这样做会在该分区之后创建未使用的空间。然后，在安装 Linux 期间，安装程序可以在未使用的空间中创建新的 Linux 分区。

若要使用 `PartitionMagic` 缩小 Windows 分区的大小，请按照以下步骤操作：

- 1. **在 `PartitionMagic` 主窗口的分区图中，右键单击该分区，并从上下文菜单中选择“调整大小/移动”。**

调整分区大小的对话框将出现。

- 2. **在调整分区大小的对话框中，单击并拖动分区右边缘以减小大小。**

对于大型硬盘（任何超过 10GB 的硬盘），将 Windows 分区缩小至 5GB，并留出其余空间用于 `Fedora Core`。如果你必须使用较小的驱动器，请尝试为 Linux 创建至少 4GB 的空间。

- 3. 单击 **确定**，然后单击 **应用** 以应用更改。在 **PartitionMagic** 完成更改后，单击 **确定**。

- 4. 重启 PC。

你不需要对缩小原来作为 C: 驱动器的分区后剩下的硬盘空间做任何处理。在安装期间，Linux 安装程序将使用该空闲空间来安装 Linux。

## 在 Knoppix 中使用 QTParted 调整分区大小

`Knoppix` 启动并出现图形界面桌面后，请按照以下步骤缩小 Windows 分区的大小：

- 1. 从 `Knoppix` 桌面选择 **主菜单 > 系统 > QTParted**。

`QTParted` 窗口将出现，该工具会显示它在你 PC 上找到的驱动器。第一个硬盘显示设备名称 `/dev/hda`，第二个显示为 `/dev/hdb`，依此类推。

- 2. 单击 `QTParted` 窗口左上角设备列表中的硬盘。

`QTParted` 在窗口左下角显示驱动器信息，并在窗口右侧显示分区信息，如图 2-1 所示。

![](img/792720823146d68f19fd50c99ebfce4b_66_0.png)

- 3. 在右侧的分区列表中，单击你想要 **调整大小** 的分区。

## 安装 Debian GNU/Linux

这通常是尺寸最大的分区（请注意图 2-1 中的 Size 列）。对于 Windows 2000 或 XP，分区类型为 ntfs，如分区列表中的 Type 列所示。在一台典型的新电脑上，你应该能看到两个分区——一个较小的 fat32 分区和一个较大的 ntfs 分区。

4. **在 `QTParted` 菜单中选择 操作：调整大小 (Resize)。**

此时会出现“调整分区大小”对话框（见图 2-2）。

![](img/792720823146d68f19fd50c99ebfce4b_67_0.png)

5. **在“新大小”文本框中输入分区的新大小（参考图 2-2），以在该分区之后创建空闲空间。**

你应该选择一个大小，使得该分区之后有 4000MB 或更多的空闲空间。你将在对话框中的“后续空闲空间”字段中看到空闲空间的大小（见图 2-2）。

6. **点击 确定 以关闭对话框。**

在执行下一步之前，硬盘分区不会被修改。

7. **在 `QTParted` 菜单中选择 文件：提交更改 (Commit)，以使分区更改生效。**

现在分区已被更改，并且在 Windows 分区之后有了空闲空间。

在硬盘上为 Linux 创建空闲空间后，你可以使用从随书 DVD 提供的 ISO 镜像文件刻录的 CD 或 DVD 来安装你所选择的 Linux 发行版。

## 安装 Debian GNU/Linux

要安装 `Debian`（发音为 *DEB-ee-un*）`GNU`（有些人读作 *GUH-new*）/Linux，你首先必须使用随书 DVD 中 `Debian` 文件夹里的 ISO 镜像刻录 CD（参见本章前面的“从 ISO 镜像刻录 CD 或 DVD”一节）。

请注意，`Debian` 安装程序不会安装 X 窗口系统。你在安装完基础操作系统后，必须将 X 作为单独的包进行安装。

### 安装概览

当你拿到 `Debian` CD 时，你就准备好安装 `Debian` GNU/Linux 了。在开始安装之前，以下是安装 `Debian` 主要步骤的概览：

- 1. 在开始安装之前，记得收集有关你计算机硬件的信息，因为如果 `Debian` 安装程序无法检测到 PC 上的某些外围设备，你可能需要提供一些细节。

- 2. 从 `Debian` CD 引导 PC。PC 启动后，你会看到一个带有 `boot:` 提示符的引导屏幕。你可以按 Enter 继续，但如果系统挂起，你可能需要重新引导并输入一些引导选项，例如在 `boot:` 提示符下输入 `linux acpi=off`。然后 Linux 内核引导并启动 `Debian` 安装程序。

- 3. 选择安装语言。

- 4. 配置网络接口。

- 5. 使用你在缩小 Windows 分区后释放的空间，创建将用于 `Debian` 的硬盘分区。（参见本章中的“为 Linux 留出空间”一节。）至少，你必须创建一个交换分区和一个根文件系统分区。

- 6. 安装并配置基础系统，其中包括 Linux 内核和 GNU 工具。

- 7. 配置并安装 `GRUB` 引导加载程序，以便它可以启动 `Debian` 以及安装在硬盘上的其他操作系统。

- 8. 重新启动 PC 以启动基础 `Debian` 系统并完成配置步骤——例如，设置时区、设置 root 密码、创建一个普通用户帐户等。

- 9. 为后续的软件包安装配置高级软件包工具 (`APT`)。你必须标识源，例如 CD（如果你有的话）以及可以找到 `Debian` 软件包的互联网站点。安装程序提供建议；你只需选择这些源即可。

- 10. 选择要安装的软件包，包括桌面环境和各种服务器。

- 11. 安装程序要么从互联网下载文件，要么从 CD 获取所需内容，安装所有选定的软件，然后配置所有软件包，包括 X 窗口系统。完成配置后，安装程序启动 X 并显示图形登录屏幕。

安装 `Debian` GNU/Linux 后，你可以使用 `apt-get` 命令行工具来安装其他软件包，甚至升级整个发行版。

## 完成 Debian 安装

首先将第一张 CD 插入 PC 的 DVD/CD 驱动器，然后重新启动 PC。PC 从 CD 引导并显示一个提示按 F1 获取帮助的屏幕。按 F1 查看帮助索引是个好主意，它会告诉你按各个功能键（从 F1 到 F10）可以获取哪些信息。表 2-1 总结了功能键提供的帮助信息。

| **表 2-1** | **Debian 安装程序引导屏幕上的功能键** |

|---|---|

| *功能键* | *显示内容* |

| F1 | 帮助索引 |



| F2 | 安装 Debian 所需的内存和硬盘空间要求（至少 24MB 内存和 256MB 硬盘空间用于最小安装，但未来可能会变化） |
| F3 | 从 CD 引导 Linux 的方式（例如，输入 `linux` 或 `expert` 或 `linux26` 或 `x26`，每种加载不同的内核） |
| F4 | 可以输入的引导参数概览，以及按功能键 `F5`、`F6` 和 `F7` 可以获取的详细信息的摘要 |
| F5 | 特殊机器的引导参数，例如某些 IBM ThinkPad 和存在显示问题的笔记本电脑 |
| F6 | 特殊磁盘控制器的引导参数，例如 Adaptec `151x`、`152x`、`1542`、`274x` 和 `284x` |
| F7 | 安装程序使用的引导参数（例如，如果你不希望安装程序探测 USB，请添加参数 `debian-installer/probe/usb=false`） |
| F8 | 指向 `www.debian.org` 并告诉你如何获取帮助 |
| F9 | 对 Debian 项目的简要介绍 |
| F10 | 关于适用于 Debian GNU/Linux 的版权和保修的信息 |

阅读完帮助信息后，你可以按 `Enter` 开始，或者输入 `linux` 后跟你的 PC 所需的任何引导参数，例如 `acpi=off`。Linux 内核加载完成后，请遵循以下步骤完成 Debian GNU/Linux 的安装。（确保你的 PC 拥有宽带互联网连接，如 DSL 或电缆调制解调器。）

### Debian 安装步骤

- 1. 从初始文本模式屏幕中选择语言、国家或地区以及键盘布局。

  使用方向键进行选择，并在每次选择后按 `Enter`。安装程序随后检测硬件并从 CD-ROM 加载 Debian 安装程序的组件。然后安装程序使用动态主机配置协议 `DHCP` 配置网络，并提示输入主机名。

- 2. 输入你的计算机的主机名。

  安装程序提示输入系统的域名，并在文本输入字段中显示默认值。（默认值是安装程序从 `DHCP` 服务器获取的。）你可以简单地按 `Enter` 接受默认域名。然后 Debian 安装程序启动磁盘分区工具，显示几个选项，如图 2-3 所示。

![](img/792720823146d68f19fd50c99ebfce4b_70_0.png)

- 3. 如果你已经为 Debian 创建了空闲空间，请选择默认选项“使用最大的连续空闲空间 (`Use the Largest Continuous Free Space`)”并按 `Enter`。

  如果你的硬盘已经有你想用于 Debian 的分区，请选择“手动编辑分区表 (`Manually Edit Partition Table`)”选项并按 `Enter`。安装程序将显示进一步的选项以及现有分区列表，如图 2-4 所示。

![](img/792720823146d68f19fd50c99ebfce4b_71_0.png)

你可以点击其中一个分区，然后编辑其特性——例如使用哪种文件系统——并为该分区选择一个挂载点。完成后，你可以完成分区并将分区表写入硬盘。（见图 2-5。）

![](img/792720823146d68f19fd50c99ebfce4b_71_1.png)

安装程序会警告你，所选分区上的数据将被销毁，选择“是”后，它将完成分区并开始安装基础系统。

安装完基础操作系统后，安装程序会检测磁盘分区上的其他操作系统，并建议在硬盘的第一扇区（称为*主引导记录*（`MBR`））上安装 `GRUB` 引导加载程序。

### 4. 安装 `GRUB` 引导加载程序并重启电脑。

安装程序完成引导加载程序的安装。随后它会弹出 CD 并重启电脑。当电脑重启时，Debian 将启动并引导你完成一系列配置步骤。

### 5. 选择时区并指示电脑的硬件时钟是否设置为格林尼治标准时间（`GMT`）。

答案通常是否。

### 6. 输入 `root`（超级用户）密码。

### 7. 通过输入所需信息（用户名、全名和密码）来创建普通用户账户。

### 8. 通过指定你希望 Debian 从中下载软件包的来源来配置 `APT`。

你需要选择一个国家以及该国中标识包含 Debian 软件包的 `FTP` 和 `Web` 存储库的服务器。如果你的电脑位于 `HTTP` 代理之后，你也可以指定该代理。（如果没有，忽略此部分即可。）稍后，你可以使用 `apt-get` 命令安装或更新 Debian 格式的各种可用软件包。你也可以将 CD 标识为 Debian 软件包的来源，但如果你将服务器标识为来源，你总是能获取最新的软件。

### 9. 选择要安装的软件包。

使用上、下箭头键移动光标，并按空格键以选择或取消选择软件包。你可以从预配置的包中进行选择，其中包括：桌面环境、`Web` 服务器、打印服务器、`DNS` 服务器、文件服务器、邮件服务器和 `SQL` 数据库。你也可以手动选择软件包。

![](img/792720823146d68f19fd50c99ebfce4b_72_0.png)

如果你选择了桌面环境包，你将获得 `X Window System` 和 `GNOME` 桌面。

完成选择后，按 `Tab` 键高亮显示“确定”，然后按 `Enter` 键。

随后，安装程序开始下载并安装所选的软件包。如果通过宽带电缆或 `DSL` 连接互联网，此步骤可能需要约一个小时完成。

### 10. 当安装程序提示输入信息以配置其已下载和安装的软件包时，回答配置问题。

`XFree86` 软件包（`X Window System`）是安装程序配置的软件包之一。完成所有配置后，安装程序启动 `X`，你将看到图形登录提示。

### 11. 在图形登录屏幕上登录。

默认情况下，Debian 安装程序安装 `GNOME` 桌面管理器（`gdm`），它用于启动 `GNOME` 桌面。

完成了！现在你的 Debian 已经启动并运行。你可以按自己的节奏探索它，并在需要时以及随着你对 Debian 了解的深入安装更多的软件包。

## 安装 Fedora Core

要安装 Fedora Core，请将本书配套 DVD 插入 DVD 驱动器并重启电脑。（在 Windows 中，选择“开始” → “关机”，然后从对话框中选择“重新启动”。）如果你使用 CD，安装步骤与 DVD 相同，只是在安装程序提示时你需要更换光盘。

如果你的电脑尚未设置为从 DVD 驱动器启动，你需要进入设置界面以更改启动设备的顺序。

电脑加电后，它会从 DVD 加载 Linux 内核，Linux 内核开始运行 Fedora Core 安装程序。在安装的其余部分中，你将通过安装程序的图形界面屏幕进行操作。

片刻之后，文本屏幕将显示欢迎消息和一个 `boot:` 提示符。欢迎消息告知你，按 `F1` 至 `F5` 功能键中的任何一个可以获得帮助。若要立即开始安装 Fedora Core，请按 `Enter` 键。你也可以在 `boot:` 提示符下输入其他选项。例如，如果你认为 DVD 可能已损坏，请输入 `linux mediacheck` 并按 `Enter` 键以测试 DVD 媒体是否存在问题。媒体检查完成后，你可以继续安装。

在快速（400 MHz 或更快）的 Pentium 电脑上从配套 DVD-ROM 安装 Fedora Core，如果你安装几乎所有的软件包，大约需要一个小时。

Fedora Core 安装程序会探测——尝试确定——特定硬件的存在，并相应地调整安装步骤。例如，如果安装程序检测到网卡，该程序会自动显示配置电脑以在 Linux 中工作于网络所需的屏幕。你看到的屏幕序列可能与我在以下几节中展示的不同；具体序列取决于你电脑的具体硬件配置。

![](img/792720823146d68f19fd50c99ebfce4b_74_0.png)

如果在安装过程中遇到任何问题，请查阅本小册子的第 3 章。该章展示了如何排除常见安装故障。

## 选择键盘和安装类型

在安装的第一个阶段中，在继续创建 Fedora Core 的磁盘分区之前，你需要执行多个步骤。以下是第一个阶段的步骤：

- 从屏幕上的语言列表中选择合适的语言，然后单击“下一步”进入下一步。

![](img/792720823146d68f19fd50c99ebfce4b_74_1.png)

每个屏幕在左侧都提供在线帮助。你可以阅读帮助消息以了解在特定屏幕上你应该做什么。

选择语言后，安装程序会显示键盘布局列表。

- 选择适合你语言字符集的键盘布局（例如，美国的 `U.S. English`），然后单击“下一步”。

安装程序显示一个屏幕，询问你希望安装新系统还是升级现有的 Fedora Core 安装。

- 对于新的 Fedora Core 安装，单击“安装”并选择安装类型。

对于新安装，你必须从以下安装类型中选择一个——个人桌面（`Personal Desktop`）、工作站（`Workstation`）、服务器（`Server`）或自定义（`Custom`）。个人桌面、工作站和服务器安装通过以预定义方式划分硬盘来简化安装过程。个人桌面安装创建一个带有图形环境和生产力应用程序的 Fedora Core 系统。

工作站级安装不仅安装图形环境，还安装软件开发工具。这种类型的安装还会删除所有当前存在的与 Linux 相关的分区，为 Linux 创建一组新的分区。



服务器安装设置所有互联网服务器，如 Web 服务器、FTP 服务器和邮件服务器。默认情况下，服务器安装不安装图形环境，但你始终可以添加 GUI 桌面的软件包。

![](img/792720823146d68f19fd50c99ebfce4b_74_2.png)

为了获得最大的灵活性，请选择自定义安装。这样你只选择想要尝试的软件包。

安装的下一个主要阶段涉及为 Fedora Core 使用而划分硬盘。

## 为 Fedora Core 划分硬盘

Fedora Core 安装程序显示一个屏幕（见图 2-6），让你指示你希望如何划分硬盘。如果你单击当前选择（其右侧显示上下箭头），安装程序将显示以下用于划分和使用硬盘的选项：

- **移除选定驱动器上的所有分区并创建默认布局**：此选项会导致 Fedora Core 安装程序移除所有分区，包括其他操作系统（如 Microsoft Windows）使用的分区。仅当你希望 Fedora Core 作为你电脑唯一的操作系统时才使用此选项。如果你希望保留现有的 Windows 分区，请勿选择此选项。

- **移除选定驱动器上的 Linux 分区并创建默认布局**：此选项会导致安装程序仅移除现有的 Linux 分区，并为安装 Fedora Core 创建新分区。如果你已经在电脑上安装了任何版本的 Linux，并希望将其清除并安装最新版本的 Fedora Core，可以使用此选项。

- **使用选定驱动器上的空闲空间并创建默认布局**：如果你使用 `PartitionMagic` 或 `QTParted` 工具为 Linux 创建了空间，请选择此选项，使用硬盘上的空闲空间创建 Linux 分区。如果你在调整分区大小后在新电脑上安装 Fedora Core，此选项是正确选择。

![](img/792720823146d68f19fd50c99ebfce4b_75_0.png)

## 安装 Fedora Core

**创建自定义布局：** 如果你拥有一块或多块已存在分区的硬盘，请使用此选项来指定用于安装 Fedora Core 的分区。

选择适当的选项并单击“下一步”。例如，如果你选择第二个选项，Fedora Core 安装程序会显示一个对话框以确认你的选择，并指出所有现有 Linux 分区中的数据将会丢失。单击“是”以继续。安装程序将显示其准备好的分区，如图 2-7 所示。此屏幕的具体外观取决于你硬盘当前的分区情况。

![](img/792720823146d68f19fd50c99ebfce4b_76_0.png)

此磁盘设置屏幕显示了磁盘驱动器列表以及其中一个驱动器的当前分区信息。如果你希望按原样接受这些分区，请单击“下一步”继续。

> **警告！** 如果你的 PC 内存不足（通常少于 128MB），安装程序会询问是否可以写入分区表并激活交换分区。执行此操作后，你的硬盘分区将发生改变。只有在你坚决要使用新分区并且确实想要安装 Fedora Core 时，才单击“是”。

## 设置关键系统参数

解决了磁盘分区问题后，你几乎就可以开始安装软件包了。首先，Fedora Core 安装程序会提示你设置一些关键系统参数。具体来说，你需要执行以下操作：

- 安装引导加载程序
- 配置网络
- 设置时区
- 设置 `root` 密码

你可以相当快地完成这些步骤。

### 安装引导加载程序

安装程序会显示一个屏幕，你可以从中安装 `GRUB` 引导加载程序。`GRUB` 是 `GRand Unified Bootloader`（全局统一引导加载程序）的缩写。*引导加载程序* 是一个驻留在硬盘上的小型程序，当你的 PC 开机时它会启动操作系统。如果你的硬盘上有 Microsoft Windows，安装程序应该能检测到 Windows 分区，并配置引导加载程序以加载 Windows。你可以查看引导加载程序配置，并从引导加载程序配置屏幕编辑设置。

![](img/792720823146d68f19fd50c99ebfce4b_77_0.png)

你可以完全跳过引导加载程序的安装。然而，如果你在 Linux 安装过程中选择不安装任何引导加载程序，即使 Linux 已安装在硬盘上，当你重新启动 PC 时也将无法启动 Linux。你只能启动当前引导加载程序设置好的内容。

为了更高的安全性（防止任何人无密码启动你的系统），请选择“使用引导加载程序密码”复选框。安装程序将显示一个对话框，你可以在其中为 `GRUB` 指定密码。

做出选择后，单击*下一步*继续。

### 配置网络

假设你的 PC 有网卡且 Linux 内核检测到了该网卡，Fedora Core 安装程序将显示*网络配置*屏幕（如图 2-8 所示）。

在此屏幕上，你可以设置网卡的 IP 地址（以便网络中的其他 PC 能与你的 PC 通信）。此屏幕显示了安装在你的 PC 上的网络设备（例如，以太网卡）列表。对于每个网络设备，你可以指定 IP 地址的设置方式。单击列表旁边的“编辑”按钮，会出现一个对话框；你可以在那里指定选项。

你可以使用 `DHCP` 自动为网卡指定 IP（Internet Protocol，互联网协议）地址，此时你的 PC 将从 DHCP 服务器获取其 IP 地址和其他网络信息。如果你的 PC 连接到 DSL 或电缆调制解调器路由器，这种情况很常见。

![](img/792720823146d68f19fd50c99ebfce4b_78_0.png)

**图 2-8：** 从此屏幕配置网络选项。

仅当你的局域网中正在运行 DHCP 服务器时，才选择 **DHCP**。如果你选择 **DHCP**，你的网络配置将自动设置，你可以跳过本节其余部分。

如果你不通过 **DHCP** 配置网络，你必须提供 IP 地址以及其他网络信息，如主要 DNS 和次要 DNS 的 IP 地址（这些是将机器名称（如 `www.amazon.com`）转换为 IP 地址的名称服务器）。输入所需的参数并单击 **下一步** 继续。

### 设置时区

完成网络配置后，选择时区——即本地时间与英国格林威治当前时间之间的差值，格林威治时间是标准参考时间（也称为格林威治标准时间 GMT 或协调世界时间 UTC）。安装程序会显示一个带地图的图形界面，你可以从中根据地理位置选择时区。选择你的时区后，单击 **下一步** 继续。

### 设置 root 密码

安装程序显示 **设置 Root 密码** 屏幕，你可以从中设置 `root` 密码。早期版本的 Fedora Core 安装程序允许你在该步骤添加一个或多个用户账户，但在这个版本中，你将有机会在首次运行 Fedora Core 时添加用户账户。（参见本书迷你卷的第 4 章。）

*root 用户* 是 Linux 中的*超级用户*——拥有在系统中执行任何操作权限的用户。最好将该账户保留给你独占使用。你需要分配一个你能记住但他人不易猜测的密码。密码长度至少应为八个字符，包含字母和数字的组合，并（为了保险起见）加入一些特殊字符，如 + 或 *。

在第一行输入密码，然后在下一行重新输入密码。密码中的每个字符在屏幕上都会显示为星号 (*)。两次输入必须匹配，安装程序才会接受你的密码。此功能确保输入错误（或猜测）的密码无效。

在继续其余安装之前，你必须输入 *root* 密码。完成后，单击“下一步”按钮继续安装。

## 选择并安装包组

设置好关键系统参数后，安装程序将显示一个屏幕，你可以从中选择要安装的 Fedora Core 包组。选择包组后，你可以喝杯咖啡休息一下，让 Fedora Core 安装程序忙着格式化磁盘分区并将所有选定的文件复制到这些分区。

![](img/792720823146d68f19fd50c99ebfce4b_79_0.png)

*包组* 由几个 Fedora Core 包组成。每个 Fedora Core *包* 进而包含许多组成特定软件的文件的集合。

图 2-9 显示了包含包组列表（实际上是软件组件）的屏幕，你可以选择安装这些组件。屏幕左侧显示包组的类别，右侧显示当前所选类别的包组。每个包组通过图标、描述性标签和复选框来标识。

一些包组已被选中，如复选框中的对勾所示。将选中的包组视为推荐安装的最小包集。不过，你可以选择安装任意或所有组件。使用鼠标在滚动列表中上下移动，并单击复选框以选择或取消选择该包组。

![](img/792720823146d68f19fd50c99ebfce4b_79_1.png)

在实际生产环境中安装 Fedora Core 时，你只安装确切的所需的包组。然而，当你想要了解 Fedora Core 的一切时，你需要许多不同的包。如果你有足够硬盘空间（至少 6GB）供 Linux 分区使用，请选择“Everything”（全部）包组来安装所有包组，以便你可以尝试 Fedora Core 提供的一切。

![](img/792720823146d68f19fd50c99ebfce4b_80_0.png)

**图 2-9：** 从此屏幕选择要安装的包组。

除了你从图 2-9 所示屏幕选择的包组外，Fedora Core 安装程序会自动安装大量运行 Linux 内核和你所选应用程序所需的包。即使你没有从这个屏幕选择任何包组，安装程序也会安装大量的包（仅运行核心 Linux 操作系统就需要所有这些包）以及一组最小集的工具。



# Fedora Core 安装

## 安装过程

每个包组都需要特定的包才能运行。Fedora Core 安装程序会自动检查任何包依赖项，并显示你尚未选择的必需包的列表。在这种情况下，请安装必需的包。

选择好要安装的包组后，单击“下一步”继续。

安装程序随后会显示一个屏幕，告知你安装即将开始。单击“下一步”以继续安装。Fedora Core 安装程序会格式化磁盘分区并安装包。在安装过程中，安装程序会显示状态屏幕以显示安装进度，包括要安装的包总数、目前已安装的包数、估计所需的硬盘空间以及预计剩余时间等信息。

硬盘格式化和安装可能需要相当长的时间。因此，你可以休息一下，大约 15 分钟后再回来检查。当你回来时，你可以从持续更新的状态屏幕了解剩余时间。

在所有软件包安装完成后，安装程序会显示一条消息，提示您安装已完成。请弹出 DVD 并点击“退出”按钮以重启您的电脑。之后，您可以执行额外的配置并安装其他软件。

## 首次启动后配置防火墙和 SELinux

在完成 Fedora Core 安装并首次重启电脑后，首次配置实用程序将引导您完成若干额外的配置步骤，包括接受许可协议、配置防火墙和 SELinux、选择显示颜色和分辨率、设置用户账户以及检查声卡。在这些步骤中，防火墙和 SELinux 的配置对系统安全至关重要，因此我将简要介绍这些步骤。

在防火墙和 SELinux 配置步骤中，您需要配置 Linux 自带的包过滤器，选择强化型 Linux（SELinux）访问控制的级别，并根据需求自定义这些安全级别。

请注意，SELinux 是由美国国家情报机构——美国国家安全局（NSA）开发的强制访问控制框架，并已包含在 Linux 2.6 内核中。您可以在 NSA 网站 `www.nsa.gov/selinux` 上获取更多关于 SELinux 的信息。简单解释一下，SELinux 的访问控制超越了基于拥有进程或文件的用户 ID 和组 ID 的传统 Linux 访问控制。SELinux 从`主体`（用户或进程）和`对象`（文件、设备、任何系统资源）的角度看待系统。主体可以扮演不同的角色，例如`普通用户`或`系统管理员`。每个主体都有一个域，每个对象都有一个类型。通过定义哪些域可以访问哪些类型，以及当程序执行时一个域如何过渡到另一个域，SELinux 提供了对 Linux 系统中谁可以访问什么的细粒度控制。听起来可能很令人困惑，但您无需理解所有细节，即可享受 SELinux 提供的高安全性。

对于防火墙，您必须选择以下选项之一：

- `禁用` 表示防火墙处于非活动状态，您的系统将接受所有类型的连接，而不进行任何安全检查。仅当您的系统运行在受信任的网络上，或者您计划稍后设置防火墙配置时（越早越好），才使用此选项。
- `启用` 表示您希望设置防火墙。这意味着您的系统将不接受任何连接，除非您明确启用了这些连接。默认情况下，系统仅接受 DNS 和 DHCP 请求。然后，您可以选择允许通过防火墙的服务，例如邮件和 FTP。

对于 SELinux 访问控制配置，您可以将其设置为以下选项之一：

- `强制模式` 表示 SELinux 强制实施访问控制。
- `宽容模式` 表示 SELinux 仅打印警告消息，但不会实际强制执行访问控制策略。
- `禁用` 表示 SELinux 已关闭。

您还可以从配置屏幕修改 SELinux 策略，但保留 SELinux 访问控制的默认设置是安全的。

当您在首次重启后完成所有配置步骤时，点击“完成”即可进入 Fedora Core 的图形登录屏幕，开始使用 Fedora。

## 安装 MEPIS

附带的 DVD 中包含一个用于 MEPIS 发行版（名为 SimplyMEPIS）的单张 CD ISO 镜像，您可以将其刻录到 CD 上，并用作 Live CD 以及安装 CD。（顺便一提，MEPIS 的发音为 `MEH-pis`。）当您从 MEPIS CD 启动时，MEPIS 将直接运行于 CD 上，您会看到 MEPIS Live CD 登录屏幕，在此您可以使用两个预定义的用户名之一登录：`demo` 或 `root`。

- `运行 Live CD：` 若要尝试 MEPIS 作为 Live CD 系统，请在登录窗口中点击“Demo”，并输入 `demo` 作为密码。
- `安装发行版：` 若要安装 MEPIS，请在登录窗口中点击“Root”图标，并输入 `root` 作为密码。

![](img/792720823146d68f19fd50c99ebfce4b_82_0.png)

当您以 `root` 身份登录时，您将获得带有红色背景的 MEPIS 桌面，如图 2-10 所示（相信我，它是红色的：红色背景提醒您当前是以 `root` 身份登录的）。从这个桌面，您可以开始 MEPIS 硬盘安装。

要在 PC 的硬盘上安装 MEPIS，请遵循以下步骤：

1. 在 MEPIS 桌面上点击 `INSTALL ME`（安装我）图标（参见图 2-10）。

`MEPIS OS Center` 窗口将打开（参见图 2-11）。通过 `MEPIS OS Center`，您可以执行多项系统配置和维护任务，包括将 MEPIS 安装到硬盘。

![](img/792720823146d68f19fd50c99ebfce4b_83_0.png)

图 2-10：要安装 MEPIS，请在 MEPIS Live CD 桌面上点击“INSTALL ME”。

2. 从 `MEPIS OS Center` 窗口左侧显示的任务列表中选择“在硬盘上安装 MEPIS”。

`MEPIS OS Center` 将在窗口右侧显示版权声明，如图 2-11 所示。

![](img/792720823146d68f19fd50c99ebfce4b_83_1.png)

图 2-11：从 `MEPIS OS Center` 开始 MEPIS 硬盘安装。

3. 阅读版权声明，如果您同意，请继续点击 `Next`（下一步）。

`MEPIS OS Center` 将显示安装的第一步，包括三个部分：

- `选择用于安装的硬盘。`
- `运行 QTParted 重新排列分区。` 此步骤是可选的，但如果您有现有的 Windows 分区且需要为 MEPIS 创建空间，请点击 `Run QTParted`（运行 QTParted）按钮使用 `QTParted` 缩小 Windows 分区。（更多信息，请参见本章中“使用 Knoppix 中的 QTParted 调整分区大小”部分。）
- `选择您是否希望使用整个磁盘安装，或使用一组现有的硬盘分区进行安装。` 我在创建了一些分区之后才进行安装，因此我选择了在现有分区上安装的选项。如果您选择在现有分区上安装，`MEPIS OS Center` 会为您提供选择文件系统的 `root` 分区、` /home` 目录和交换分区的选项。您必须指定一个分区用于根目录，另一个用于交换。

4. 分配 `root` 分区 — 用于文件系统的 `root` 的分区 — 和交换分区，然后点击 `Next`（下一步）。

`MEPIS OS Center` 将显示一个对话框，询问您是否确实要格式化并销毁所分配分区中的所有数据。点击 `Yes`（是）即可开始 MEPIS 安装。在从 CD 复制文件到硬盘之后，`MEPIS OS Center` 将继续安装 `GRUB` 引导加载程序并选择您想要启动的内核。

5. 选择是否希望将 `GRUB` 安装在 `主引导记录 (MBR)` 上，以及您想要安装的内核版本 — `2.4` 和 `2.6`。

通常您可以接受默认选择，即安装 `GRUB` 到 `MBR` 并启动 `2.6` 版本的内核。

6. 完成选择后，点击 `Next`（下一步）继续。

7. 输入 `root` 密码并定义一个普通用户账户。然后点击 `Next`（下一步）。

8. 输入计算机的主机名、域名以及 Windows 工作组名称。然后按 `Enter`（回车）。

9. 选择要启动的服务，包括 `Guarddog` 防火墙服务。还要选择显示驱动程序。然后点击 `Next`（下一步）。

10. 设置键盘布局和时钟。然后点击 `Next`（下一步）。

11. 点击 `Finish`（完成）以完成 MEPIS 安装。

最后一步安装步骤中的消息会告知您，可以在 `www.mepis.org` 或 `www.mepislovers.com` 获取 MEPIS 的社区支持。

移除 CD 并重启后，您将看到 `GRUB` 菜单，您可以从中从硬盘启动 MEPIS。然后，您可以使用安装 MEPIS 时定义的用户名以普通用户身份登录。

## 安装 SUSE Linux

由于 DVD 空间有限，附带的 DVD 不包含来自 openSUSE 项目的完整 SUSE（我将 SUSE 发音为 SOO-za，但许多人的发音不同）Linux 发行版。相反，DVD 包含 SUSE Live DVD 的 ISO 镜像文件，该文件使您可以直接从 DVD 运行 SUSE Linux。您可以从 `http://ftp.opensuse.org/pub/opensuse/distribution/SL-OSS-stable/` 下载完整的 SUSE Linux 发行版。



![](img/792720823146d68f19fd50c99ebfce4b_85_0.png)

要试用 SUSE Linux Live DVD 版本，只需从本书附带 DVD 上的 SUSE Live DVD ISO 镜像刻录一张 DVD，然后从该 DVD 启动您的 PC（您需要 DVD 刻录机来在 DVD 介质上刻录 ISO 文件）。

要安装完整的 SUSE 发行版，您有两个选择：

- 通过高速互联网连接，从镜像 SUSE Linux 发行版的 FTP 服务器之一直接安装完整发行版。
- 通过从 `http://ftp.opensuse.org/pub/opensuse/distribution/SL-OSS-stable/` 下载 SUSE Linux ISO 镜像并刻录 5 张 CD 来安装完整发行版，`然后从第一张 CD 启动您的 PC`。（有关刻录 CD 的说明，请参见本章中“从 ISO 镜像刻录 CD 或 DVD”部分。）

在以下部分中，我将首先介绍执行 FTP 安装的步骤，然后描述从 CD 进行完整的 SUSE 安装。

## 执行 FTP 安装

要从镜像 SUSE 发行版的众多 FTP 服务器之一安装 SUSE Linux，您必须执行以下主要步骤：

1. 从 FTP 服务器下载 SUSE 启动镜像，并刻录包含该镜像的 CD。
2. 记下 FTP 服务器的 IP 地址以及存放 SUSE 发行版文件的目录。
3. 使用启动 CD 启动 PC。在启动提示符处输入命令，以开始从您通过其 IP 地址识别的 FTP 服务器进行 FTP 安装。

如果有一台运行 Windows 系统且具备高速互联网连接的 PC，你可以使用这台 PC 来下载启动镜像并刻录启动光盘。你还可以使用这台 PC 来查找 FTP 服务器的 IP 地址。

你还必须知道安装在 PC 中的网卡名称，因为在开始 SUSE FTP 安装之前，你必须手动加载驱动程序。在下载 SUSE 安装程序的启动镜像时，你可以同时找到 FTP 服务器的 IP 地址。本节将解释这些步骤。

通过典型的宽带 DSL 或电缆调制解调器连接到互联网，从 FTP 服务器安装 SUSE 可能需要两个小时或更长时间。请遵循以下步骤通过网络从 FTP 服务器进行 FTP 安装：

1. 使用 Web 浏览器打开位于 [www.suse.com/us/private/download/ftp/int_mirrors.html](https://www.suse.com/us/private/download/ftp/int_mirrors.html) 的 FTP 服务器列表，找到一个离你较近且标记为 Complete（完整）的 FTP 服务器（这意味着该服务器拥有完整的 SUSE 发行版和所有更新）。

服务器列表按国家组织，包含 FTP 和 HTTP（Web）服务器。转到离你最近的国家的部分，并选择标记为 Complete 的最接近的服务器。

如果你在 Microsoft Windows 中执行此步骤，请打开命令提示符窗口（选择“开始”>“运行”，输入 `cmd`，然后按 Enter），输入 `ping` 后跟 FTP 服务器的名称（例如 `mirror.mcs.anl.gov`）。然后你将在下一行看到 FTP 服务器的 IP 地址（例如 `140.221.37.130`）。记下该 IP 地址以便稍后使用。

2. 点击 FTP 服务器链接，找到包含 `boot.iso` 文件的目录——这是 SUSE 安装程序的启动镜像。

目录取决于 SUSE 的版本。例如，对于版本 10.0，`boot.iso` 文件位于 FTP 服务器的 `pub/suse/i386/10.0/` 目录中。该文件有几十兆字节大小。

3. 下载 `boot.iso` 文件并保存它。

4. 将 `boot.iso` 镜像刻录到 CD 上。

使用你 PC 的 CD 烧录应用程序来烧录名为 `boot.iso` 的 ISO 镜像。

5. 转到你要进行 SUSE FTP 安装的 PC，插入启动光盘，并重新启动 PC。

如果你的 PC 没有设置从 CD 驱动器启动，你必须进入 Setup（通过在 PC 通电时按下 F2 等键）并更改启动设备的顺序。

PC 重启后，片刻后会显示一个带有多个选项的 GUI 屏幕。使用方向键在列表项和屏幕上的按钮之间移动。例如，如果你的 PC 在 ACPI 方面存在问题，请选择禁用 ACPI 的安装选项。

6. **使用方向键选择 Installation（安装）选项并按 Enter。**

这将加载 Linux 内核并运行安装程序。在检测和初始化硬件后，安装程序会显示一条消息，表示它无法找到 SUSE Linux 安装源，并且正在激活手动设置程序。这是正常的，你应该按 Enter 继续。然后安装程序会显示语言列表。

7. **使用方向键选择语言并按 Enter。**

安装程序显示 *键盘映射* 列表——即与语言相关的键盘布局。

8. **选择键盘语言并按 Enter。**

安装程序显示主菜单。

9. **使用方向键选择 Start Installation or System（开始安装或系统）并按 Enter。**

在下一个屏幕上，选择 *Start Installation or Update*（开始安装或更新）并按 Enter。安装程序显示 *源介质* 列表——这里是你指定安装程序在哪里可以找到执行安装所需文件的地方。

10. **选择 Network（网络）作为源介质并按 Enter。**

安装程序提示你选择网络协议。

11. **选择 FTP 作为网络协议并按 Enter。**

对话框提示你确定是否使用动态主机配置协议（DHCP）自动配置网络。如果你的网络使用 DHCP（大多数情况都是这样），请选择 *Yes*（是）并按 Enter。否则，你必须在此步骤中输入 IP 地址和名称服务器的 IP 地址。然后安装程序会提示输入 FTP 服务器的 IP 地址。

12. **输入你在步骤 1 中找到的 FTP 服务器的 IP 地址（例如，为 FTP 服务器 `mirror.mcs.anl.gov` 输入 `140.221.37.130`）。**

安装程序提示你指示是否要使用用户名和密码连接到 FTP 服务器。

13. **选择 No（否）并按 Enter。**

回答 *No*（否），因为 FTP 服务器支持 *匿名 FTP*——这意味着任何人都可以使用用户名 *anonymous* 登录。安装程序还会提示你指示是否要使用 HTTP 代理。

14. **除非你的 PC 位于代理之后**（在某些组织中可能如此），否则选择 **No**（否）并按 **Enter**（回车）。

然后安装程序会提示你输入 SUSE 文件所在目录的名称。

15. **输入 FTP 服务器上存放 SUSE Linux 文件的目录名称并按 Enter。**

目录名称是你在步骤 2 中找到 `boot.iso` 文件的位置的父目录。例如，如果 `boot.iso` 文件位于 `pub/suse/i386/10.0/boot/` 中，则你应该输入 `pub/suse/i386/10.0/` 并按 **Enter**。

安装程序显示一条消息，告知你正在将数据加载到 *RAM 磁盘*（指作为硬盘起作用的内存区域）中。当安装程序完成数据下载（约 62MB 数据）后，YaST（这是 SUSE 安装程序的名称）将启动并显示其初始 GUI 屏幕。

从这一点开始，安装步骤与 CD/DVD 安装相同，这将在下一节中解释。你应该跳转到 YaST 安装程序显示其初始 GUI 屏幕的地方。

## 从 CD 安装 SUSE Linux

要从本书配套 DVD 上的 ISO 镜像刻录的 CD 安装 SUSE Linux，只需将第一张 CD 插入你的 PC 的 CD/DVD 驱动器并重新启动你的 PC。（在 Windows 中，选择 **Start** > **Shutdown**，并从对话框中选择 **Restart**。）请注意，你可能必须进入 Setup 并确保你的 PC 设置为从 CD/DVD 驱动器启动。

在你的 PC 通电后，启动加载器将启动并显示一个带有项目菜单的初始启动屏幕。表 2-2 列出了每个启动菜单项及其含义。如你所见，你可以从启动屏幕执行许多任务，包括从硬盘启动现有安装和启动救援系统。

### 表 2-2 SUSE 安装程序启动菜单项

| 选择此项目 | 以执行此操作 |
| :--- | :--- |
| Boot from Hard Disk | 从硬盘上先前安装的操作系统中启动 PC |
| Installation | 自动检测硬件并开始安装 SUSE Linux |
| Installation—ACPI Disabled | 禁用对 ACPI（高级配置和电源接口）的支持，但其他方面检测硬件并开始 SUSE 安装 |
| Installation — Safe Settings | 禁用潜在麻烦的功能，如 ACPI、APM（高级电源管理）和用于 IDE 接口的 DMA（直接内存访问），并开始安装 SUSE。如果安装在任何其他选项下挂起，请选择此选项。 |



| Rescue System | 在内存中启动一个小型 Linux 系统，以便你以 `root` 身份登录进行故障排除 |
| Memory Test | 检查 PC 的内存是否存在任何问题 |

在 SUSE 安装程序启动屏幕的底部，你会看到关于使用功能键 `F1` 到 `F6` 的一些信息。表 2-3 解释了这些功能的作用。

你还可以在启动菜单下方的 Boot Options 文本框中提供其他安装程序选项——以及 Linux 内核选项。*安装程序选项* 控制安装程序行为的某些方面，而 *内核选项* 则在启动安装时传递给 Linux 内核。我在本书的小册子第 3 章中解释了许多这些启动选项。

### 表 2-3 在 SUSE 安装程序启动屏幕使用功能键

| 按此功能键 | 以执行此操作 |
| :--- | :--- |
| `F1` | 获取上下文相关的帮助——与当前选中项相关的帮助信息。使用上箭头和下箭头键阅读帮助屏幕，使用左箭头和右箭头键在主题之间跳转。你可以通过按 `Escape` 键关闭帮助屏幕。 |
| `F2` | 选择启动加载器要使用的语言和键盘映射。 |
| `F3` | 选择你希望 YaST 安装程序在其 GUI 中使用的屏幕分辨率。如果 GUI 屏幕未出现，你可以选择 **Text Mode** 以使用文本模块界面。 |
| `F4` | 选择你要从中安装的源。选项包括：CD 或 DVD；或使用不同协议的网络源，如 FTP、HTTP、NFS 和 SLP（服务定位协议）。 |
| `F5` | 更新新硬件的驱动程序模块，因为 CD 或 DVD 上可能没有驱动程序。启动安装后，你将被提示在软盘或 CD-ROM 上插入更新的驱动程序模块。 |

![](img/792720823146d68f19fd50c99ebfce4b_89_0.png)

安装程序最初为 GUI 屏幕选择相当高的屏幕分辨率（通常是 1280 x 1024 像素）。你应该按 `F3`，这会弹出一个菜单，你可以从中选择更合理的屏幕分辨率，如 1024 x 768 像素。

在按下 `F2` 设置屏幕分辨率后，从启动菜单中选择“Installation（安装）”并按 Enter 键。这将加载 DVD 中的 Linux 内核，随后 Linux 内核将启动 YaST 安装程序。在安装的其余过程中，您将使用 YaST 的 GUI 屏幕进行操作。

如果在安装过程中遇到任何问题，请查阅本小册子的第 3 章。该章节介绍了如何排查常见的安装问题。

## 在 YaST 中启动 SUSE 安装

YaST —— SUSE 安装程序 —— 显示一个 GUI 屏幕（参见图 2-12），您可以据此在 PC 的硬盘上安装并配置 SUSE Linux。

YaST 屏幕的左侧显示了安装步骤列表，这些步骤被组织为两大类任务：基本安装（Base Installation）和配置（Configuration）。一个箭头标记当前步骤。例如，在图 2-12 中，箭头标记的是语言选择步骤。步骤完成后，YaST 会在该步骤旁边显示一个对勾。

![](img/792720823146d68f19fd50c99ebfce4b_90_0.png)
![](img/792720823146d68f19fd50c99ebfce4b_90_1.png)

在 YaST 屏幕的右侧（参见图 2-12），您可以看到当前步骤的选项。您必须选择选项并单击 **Accept（接受）** 才能进入下一个安装步骤。在确认您确实要继续安装之前，您可以随时通过单击 **Abort（终止）** 按钮来中止安装过程。

在任何安装步骤中，单击 YaST 屏幕左下角的 **Help（帮助）** 按钮（参见图 2-12），以查看当前步骤的上下文敏感帮助信息。帮助区域将显示在 YaST 屏幕的左侧。再次按下该按钮即可返回查看安装步骤列表。

请按照以下步骤完成 YaST 安装程序中的基本安装任务：

- **选择在安装过程中以及已安装的 SUSE Linux 系统中使用的语言。单击 Accept。**
  YaST 将探测硬件并加载驱动程序模块。YaST 可能会提示您确认是否应加载某些驱动程序模块。然后，YaST 会显示一个媒体检查屏幕，让您有机会检查安装介质。单击 **Start Check（开始检查）** 以执行检查，完成后单击 **Next（下一步）**。YaST 将显示许可协议。
- **阅读许可协议，如果您同意，请单击 Yes（是）按钮。然后单击 Next 以继续。**
  YaST 会提示您指示这是新安装还是更新。
- **假设您首次安装 SUSE，请选择 New Installation（新安装）并单击 Next。**
  YaST 会提示您输入时区。
- **选择您的时区并单击 Next。**
  您也可以通过单击 **Change（更改）** 来更改当前时间和日期，但通常这些设置是准确的。在此步骤之后，YaST 会提示您（参见图 2-13）选择一个 GUI 桌面环境——GNOME 或 KDE，或者诸如最小化图形环境或不使用 GUI 桌面的文本模式系统等其他选项。您对桌面环境的选择决定了 YaST 将安装哪些软件包。
- **选择您想要的桌面环境并单击 Next。**
  YaST 将收集系统信息并准备所有安装设置的列表，最初在“概述”（Overview）选项卡中显示。单击 **Expert（专家）** 选项卡以按类别查看完整的设置列表，如图 2-14 所示。表 2-4 总结了安装设置类别。请注意，您必须向下滚动才能看到图 2-14 所示屏幕中的所有安装设置。

![](img/792720823146d68f19fd50c99ebfce4b_91_0.png)
![](img/792720823146d68f19fd50c99ebfce4b_92_0.png)

图 2-13：选择桌面环境并单击 **Next（下一步）**。

![](img/792720823146d68f19fd50c99ebfce4b_92_1.png)

图 2-14：单击标题以更改该类别的设置。

第一册
第 2 章
安装 SUSE Linux

**表 2-4 安装设置类别**

| 类别 | 这些设置指定的内容 |
| :--- | :--- |
| System（系统） | 关于 PC 硬件的信息，包括处理器类型和内存量 |
| Keyboard Layout（键盘布局） | 键盘的语言和布局 |
| Mouse（鼠标） | 鼠标类型（例如 PS/2 鼠标） |
| Partitioning（分区） | 关于将被格式化的分区以及将挂载到 Linux 文件系统上的任何分区的详细信息。您应该检查以确保 YaST 使用了您在为 Linux 预留空间时创建的未使用磁盘分区（如本章前面“为 Linux 预留空间”部分所述）。如果硬盘仅安装了 Microsoft Windows，YaST 将提供选项以缩小 Windows 分区并创建其他必需分区来安装 SUSE Linux。如果您除了 Windows 分区外还有其他分区，YaST 会选择适合 SUSE Linux 使用的分区。然后，您可以单击“分区”标题，并在后续步骤中接受建议或创建自定义分区配置。 |
| Software（软件） | YaST 将安装哪些软件。这取决于您在早期安装步骤中选择了哪个 GUI 桌面——KDE 或 GNOME。 |
| Booting（启动） | 关于启动加载器的信息，该加载器负责在重启 PC 时启动 Linux（以及可能位于硬盘上的其他操作系统，如 Windows XP）。默认使用安装在硬盘主引导记录（MBR）上的 GRUB 启动加载器。 |
| Time Zone（时区） | 基于您在早期安装步骤中的选择，设置当前时区及日期和时间 |
| Language（语言） | 已安装的 SUSE Linux 系统将使用的语言 |
| Default Runlevel（默认运行级别） | Linux 启动后启动哪些进程。默认运行级别为 5，这为您提供一个完整的、网络已启用且具有图形登录界面的多用户系统。 |

6. 向下滚动“安装设置”列表，并单击某个标题以查看设置并进行任何更改。您可以原样接受大多数设置。
7. 检查完所有安装设置后，单击 Next。YaST 将显示您在图 2-15 中看到的警告。它告诉您这是不可逆转的点。您可以单击 Install（安装）以确认进行安装，或者单击 Back（返回）以返回安装设置。

![](img/792720823146d68f19fd50c99ebfce4b_94_0.png)

8. 如果您确定要继续安装，请单击 Install 按钮。YaST 开始安装，其中包括格式化和准备硬盘分区以及将 SUSE Linux 文件复制到硬盘。随着 YaST 安装软件包，它会显示一个幻灯片，介绍 SUSE Linux 的各种功能。完成基本安装后，YaST 将提示输入 root 密码。
9. 输入 root 用户的密码。root 用户是管理员账户，您可以使用它在系统上执行任何操作——从安装软件到添加新的用户账户。
10. 接受或更改网络配置。YaST 显示当前设置（参见图 2-16 中的示例）。如果设置正确，您可以直接单击 Next 继续。



## SUSE Linux 安装后续步骤

11. 测试 Internet 连接并使用 YaST 在线更新服务更新系统。如果有更新，YaST 会询问您是否现在运行在线更新。单击 `OK`（确定）以执行此操作，YaST 将自动选择一个镜像站点来下载更新。您只需单击 `Next`，单击 `Accept`，并按照 YaST 显示的任何说明操作即可。此步骤可能需要较长时间才能完成，特别是如果有很多补丁需要下载和安装的话。在补丁下载和安装的最终步骤中，单击 `Finish`（完成）以继续 SUSE Linux 安装的其余部分。

12. 选择用户身份验证方法，然后单击 `Next`。如果您没有可用的基于网络的身份验证，请选择 `Local authentication`（本地身份验证）。

![](img/792720823146d68f19fd50c99ebfce4b_95_0.png)

对于 `Network authentication`（网络身份验证），您必须选择三种网络身份验证方法之一——`NIS`（网络信息系统）、`LDAP`（轻量级目录访问协议）或 `Samba`（用于 Windows 网络）。

13. 对于本地身份验证，通过输入用户名、密码和其他设置来添加一个新的本地用户。单击 `Next` 继续。如果您勾选 `Auto Login`（自动登录）复选框，SUSE Linux 在启动时将自动登录此用户。如果您的密码存在缺陷（例如将用户名用作密码的一部分），YaST 会通知您此问题并询问您是否确实想要使用弱密码。然后 YaST 显示发行说明。

14. 阅读发行说明并单击 `Next`。发行说明包含有关 SUSE Linux 发行版的最后时刻信息，包括任何已知问题和变通办法。值得浏览一下，以便了解可能适用于您的 PC 硬件配置的任何内容。

15. 接受或更改为您的 PC 显示的硬件配置。

硬件配置包含有关特定硬件（如显卡、显示器、声卡、打印系统等）的信息。通常，显示的配置应该是可接受的，但您应检查每一项内容。特别是，请检查显卡配置，以查看 YaST 是否正确检测到了显示器和显卡。如果没有，您可以点击 `Graphics Cards`（显卡）并在后续窗口中更改相关信息。配置步骤完成后，YaST 会通知您安装已完成。

1. 点击 `Finish`（完成）以结束安装。

安装程序将重启系统。如果您安装了 `KDE GUI` 并且在步骤 5 中启用了自动登录，SUSE Linux 将重启，自动登录并显示 KDE 桌面。否则，您可以在 GUI 登录界面登录并开始使用系统。

## 安装 Ubuntu

随书附赠的光盘包含一个用于安装 Ubuntu 的单张光盘 ISO 镜像。首先，请按照本章中“从 ISO 镜像刻录 CD 或 DVD”部分概述的步骤，将该 ISO 镜像刻录到 CD-R 光盘上。Ubuntu 基于 Debian，因此安装步骤与 Debian 类似。

要在您的计算机上安装 Ubuntu，请遵循以下步骤：

1. 从 Ubuntu 安装光盘启动您的计算机。
   - 初始启动屏幕会提示您按 `Enter` 键开始安装，或按 `F1` 键获取更多帮助。您可以按 `F1` 键查看通过按其他功能键可获取的帮助信息。这些选项与 Debian 安装程序的启动屏幕相似，因为 Ubuntu 基于 Debian。若要查看功能键摘要及其功能，请参考表 2-1。

2. 按 `Enter` 键或输入启动命令后跟任何选项，然后按 `Enter` 键。
   - 例如，在不支持 ACPI 的计算机上，我输入 `linux acpi=off` 来启动 Ubuntu 安装。安装程序会提示您选择语言。

3. 选择语言并按 `Enter` 键。
   - 安装程序根据您的语言选择显示您的位置。

4. 选择位置并按 `Enter` 键。
   - 安装程序根据您的语言和位置显示您的键盘布局。

5. 选择键盘布局并按 `Enter` 键。
   - 安装程序检测硬件以查找 `CD-ROM` 驱动器，并从 CD 加载附加软件。它检测网络硬件并使用 DHCP 进行配置。然后它提示您输入主机名。

6. 输入您系统的主机名并按 `Enter` 键。
   - 安装程序检测硬盘并提示您选择磁盘分区方法。如果您已在硬盘上为 Ubuntu 创建了空间（参见本章中的“为 Linux 预留空间”部分），请选择选项“为 Ubuntu 安装使用最大连续空闲空间”。

7. 选择最大连续空闲空间并按 `Enter` 键（或选择现有分区并将它们分配给特定的挂载点，例如文件系统 `/root`）。
   - 安装程序安装 Ubuntu 基础系统，并询问系统时钟是否设置为 GMT（格林威治标准时间）。答案通常是否。然后安装程序提示您输入时区。

8. 选择您的时区并按 `Enter` 键。

9. 创建用户帐户。
   - 按照安装程序的提示，输入用户的完整姓名、用户名和密码。安装程序配置 `APT` —— 高级包工具 —— 用于将来下载和安装包。
   - 安装程序列出它在您的计算机硬盘上发现的所有已安装操作系统，并询问您是否要在硬盘的主引导记录（`MBR`）上安装 `GRUB` 引导加载程序。

10. 选择“是”并按 `Enter` 键以安装 `GRUB`。
    - 安装程序完成 `GRUB` 安装，然后卸载并弹出 CD。一条消息将通知您第一阶段安装已完成。请移除 CD 并按 `Enter` 键以重启计算机。

计算机重启后，Ubuntu 将从在线存储库下载并安装更多包。（您的计算机需要连接到互联网才能使一切正常工作。）

![](img/792720823146d68f19fd50c99ebfce4b_97_0.png)

> `X` 窗口系统和 `GNOME GUI` 是 Ubuntu 下载并安装的包之一。这些包安装并配置后，Ubuntu 将启动一个 GUI 登录屏幕，您可以使用之前定义的用户帐户登录。如果由于某种原因 `X` 窗口系统无法工作，您必须按照本书第 3 章中的建议排查 X 故障。

## 安装 Xandros 桌面

随书附赠的光盘*不*包含完整的 Xandros（您可以将 Xandros 读作 *ZAN-drose*，除非别人告诉您不同的读法）桌面发行版，因为它是商业产品。相反，光盘包含一个名为 *Xandros Open Circulation Edition*（OCE）的受限版本的 ISO 镜像。您可以安装 Xandros OCE 来试用 Xandros 桌面，以便在决定是否购买完整发行版之前进行评估。在本节中，我描述了 Xandros OCE 的安装过程，它与完整发行版的安装过程相似，只是完整发行版包含更多的软件包。

要安装 Xandros OCE，请从本书随书附赠光盘中的 Xandros OCE ISO 镜像刻录一张 CD，并从该 CD 启动您的计算机。有关说明，请参阅本章前面的“从 ISO 镜像刻录 CD 或 DVD”部分。

![](img/792720823146d68f19fd50c99ebfce4b_98_0.png)

初始 Xandros 启动屏幕显示一个标志和一条消息，提示“按 `Shift` 键以进入故障排除选项”。如果您什么都不做，Linux 内核将加载并启动一个 GUI 安装程序。然而，如果安装似乎挂起，请重启计算机，这次在启动屏幕按 `Shift` 键。然后您会看到几个启动 Linux 内核的选项。默认选项标记为 `Default Setup`（默认设置），但您有选项来尝试不同级别的 APM 和 ACPI 支持。使用向上和向下箭头键选择其中一个替代方案，并按 `Enter` 键以绕过安装过程中的问题。另外，如果您似乎无法获取 GUI 屏幕，请尝试选择 `VESA Mode Setup`（VESA 模式设置）（查看表 2-5 以获取更多关于此的信息）。这可能会解决启动 X 窗口系统的任何问题。表 2-5 总结了在初始启动屏幕按 `Shift` 键可访问的 Xandros 启动选项。

**表 2-5** | **初始启动屏幕上的 Xandros 启动选项**

| 此选项 | 执行以下操作 |
| :--- | :--- |
| `Default Setup` | 使用选项 `acpi=on`（启用 ACPI 支持）启动 Linux 内核 |
| `ACPI 2 Setup` | 使用选项 `acpi=on noapic`（启用 ACPI，但禁用 APIC —— 高级可编程中断控制器）启动 Linux 内核 |
| `ACPI 3 Setup` | 使用选项 `acpi=on pci=biosirq`（启用 ACPI，但使用 BIOS 设置来路由中断请求或 IRQs）启动 Linux 内核 |
| `ACPI 4 Setup` | 使用选项 `acpi=on pci=noacpi`（启用 ACPI 且不使用 ACPI 来路由中断请求）启动 Linux 内核 |
| `APM Setup` | 使用选项 `acpi=off`（禁用 ACPI）启动 Linux 内核 |
| `APM 2 Setup` | 使用选项 `acpi=off noapic`（同时禁用 ACPI 和 APIC）启动 Linux 内核 |



| APM 3 Setup | 使用选项 `acpi=off pci=biosirq`（禁用 ACPI 并使用 BIOS 设置来路由中断请求）启动 Linux 内核 |
| 256-Color Setup | 以 256 色模式启动 X 窗口系统（这应在几乎所有显卡上正常工作） |
| VESA Mode Setup | 使用 VESA（视频电子标准协会）驱动程序启动 X 窗口系统 |
| Custom Setup | 使用选项 `vga=normal`（屏幕以 80 × 25 文本模式显示）启动 Linux 内核 |
| Restore Xandros | 允许您恢复 Xandros 并修复问题 |
| Rescue Console | 在 80 × 25 文本屏幕中以单用户模式启动 Linux 内核，您可以以 `root` 身份登录并修复问题 |
| International | 允许您选择非美国键盘和语言 |

通常，您不需要做任何事情，因为引导加载程序会自动加载 Linux 内核和驱动程序模块。然后它读取 CD，检测和配置硬件，并启动 X 窗口系统和 GUI 安装程序。如果一切顺利，您应该会看到初始 GUI 屏幕，如图 2-17 所示。点击 **Next**（下一步）以继续安装。

下一个屏幕显示商业软件世界臭名昭著的 EULA —— 最终用户许可协议。您猜对了——我们中那些喜欢拿语言开玩笑的人称之为 **YOOO-la**（一种玩笑读法，类似于 "Yee-ooo-lah"）。如果您决定继续，请阅读 EULA，点击 **I Accept the Agreement**（我接受协议），然后点击 **Next**（下一步）。

Xandros 安装程序随后显示两个安装选择：

- **快速安装：** 使用默认设置和常用软件选择将 Xandros 安装在您的计算机上。
- **自定义安装：** 允许您控制安装 Xandros 时的一些步骤，包括软件选择、Xandros 使用的磁盘分区以及网络配置。

我在以下部分中描述了两种安装方法。

## 安装 Xandros 桌面

75

![](img/792720823146d68f19fd50c99ebfce4b_100_0.png)

### 使用 Xandros 快速安装

Xandros 快速安装非常简单——前提是你希望 Xandros 使用整个硬盘或接管一个未使用的分区。简而言之，你输入 `root` 密码并创建一个普通用户账户。然后查看安装摘要，点击“完成”，安装程序将完成其余工作。

**警告！** 如果你的 PC 上安装了 Windows，Xandros 安装程序会显示一个屏幕，询问你是要保留 Windows 还是覆盖它。默认选项是保留 Windows。你可以指示你的选择并点击“下一步”继续。

下一个屏幕要求输入 `root`（管理员）密码和计算机名称。输入 `root` 密码并再次输入以确认。对于计算机名称，你可以接受 Xandros 安装程序生成的名称，或者输入对你更有意义的内容。然后点击“下一步”。

接下来，你有机会创建一个普通用户账户。输入所需的信息，包括用户名和密码，并点击“下一步”。此用户名用于登录 Xandros。

安装程序会显示安装摘要屏幕（如图 2-18 所示）供你查看。仔细检查信息，特别是安装是否将接管一个分区或整个硬盘。如果你需要做出更改，点击“返回”。否则，点击“完成”开始安装。

安装程序完成 Xandros 的安装后，会提示你重启 PC。当 Xandros 首次启动时，它会运行“首次运行向导”图形界面，引导你完成一些配置步骤。这些步骤包括设置日期和时间，以及选择货币和日期的显示方式。你还有机会配置打印机。

### 使用 Xandros 自定义安装

自定义安装方法让你对要安装什么软件有一定的控制力。它还可以让你为安装指定特定的磁盘分区、配置网络以及添加多个用户账户。要使用自定义安装，从安装选择屏幕（在接受 EULA 协议后立即出现的屏幕）中选择该选项，然后如 图 2-19 所示点击“下一步”。

![](img/792720823146d68f19fd50c99ebfce4b_101_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_102_0.png)

安装程序会显示软件选择屏幕，在那里你可以选择要安装的应用程序。你可以从四组预定义的应用程序集合中选择：

- **最小桌面**：安装一组基本应用程序
- **标准桌面**：安装一组推荐常用的应用程序
- **完整桌面**：安装所有标准应用程序外加更多应用程序，如某些服务器软件
- **自定义桌面**：安装一组基础软件（然后你可以从这些选项下方出现的列表中按单点菜方式选择应用程序）

当你点击选择这些集合中的任意一个时，你可以看到下方列表中显示的详细选择。你也可以从列表中随意添加或删除任何内容，因此预定义的集合不应限制你的选择。选择好要安装的软件后，点击“下一步”。

然后，安装程序会引导你完成磁盘配置步骤。下一屏幕（如图 2-20 所示）显示了安装程序的建议。如果你有可用的磁盘分区，安装程序建议接管整个硬盘或某个分区。（别担心，你可以确切看到安装程序打算如何使用磁盘分区，并且如有必要你可以进行干预。）

![](img/792720823146d68f19fd50c99ebfce4b_103_0.png)

*图 2-20：* Xandros 安装程序建议它计划如何使用硬盘。

如果你想管理磁盘分区，点击**管理磁盘和分区**项并点击“下一步”。安装程序会显示一个编辑器，在那里你可以删除和添加分区，并为分区分配挂载点。例如，你可以将一个小容量的 50MB 分区分配给 `/boot` 挂载点，并将一个多 GB 的分区分配给 `root` 文件系统（`/`）。你还可以标识一个大小约为可用内存两倍的交换分区。Linux 将交换分区用作*虚拟内存*——一种基于硬盘的 PC 内存扩展。

表 2-6 总结了磁盘配置屏幕中可用的可能选项。（参考图 2-20。）请注意，只有适用于你 PC 的选项可供选择。其他选项被灰色显示。

| 此选项 | 执行以下操作 |
| :--- | :--- |
| 使用空闲空间 | 使用硬盘上最大的未分配空间块 |
| 接管磁盘或分区 | 接管整个硬盘、特定分区或旧版本的 Xandros，并擦除所有数据 |
| 调整 Windows 分区大小 | 减小 Windows 分区的大小，并将 Xandros 安装到释放的空间中 |
| 替换现有的 Xandros 桌面操作系统 | 升级旧版本的 Xandros（保留用户账户，将目录重命名为带有 `__old` 后缀的名称，并保留一些默认设置） |
| 管理磁盘和分区 | 允许你创建一个或多个磁盘分区并指定每个分区的挂载点 |

如果你决定采用默认的**接管磁盘或分区**，点击**下一步**，Xandros 安装程序会显示它计划接管的分区。如果你同意，点击**下一步**。然后，安装程序以交换分区位置和 reiserfs 文件系统的形式显示磁盘配置，如图 2-21 所示。一个复选框显示安装程序将在第一个 IDE 硬盘的主引导记录上加载引导管理器。

请注意，Xandros 安装程序使用 ReiserFS 文件系统作为磁盘分区。其他文件系统选择是 Ext2 或 Ext3。你可以选择默认的 ReiserFS。

![](img/792720823146d68f19fd50c99ebfce4b_104_0.png)

查看磁盘配置后，点击“下一步”继续。安装程序显示网络配置。默认是动态配置以太网卡，这意味着使用 DHCP 获取网络接口和名称服务器的 IP 地址。如果这适用于你的网络，点击“下一步”。否则，你必须点击“编辑”并为网络输入静态 IP 地址。你也可以选择不配置网络。完成网络配置步骤后，点击“下一步”。

安装程序提示输入 `root` 用户密码。你还可以输入计算机名称。点击“下一步”继续后，安装程序显示用户账户配置屏幕，在那里你可以定义多个用户账户。对于每个用户账户，点击“添加”并输入所需信息。添加完用户账户后，点击“下一步”。

安装程序显示安装摘要屏幕（见图 2-22）。

仔细查看信息，点击“返回”以更正任何错误。当你确定选择可接受时，点击“完成”。安装程序完成 Xandros 的安装并提示你重启 PC。重启后，Xandros 运行“首次运行向导”，引导你完成一系列配置步骤。

恭喜！你现在可以开始使用 Xandros 桌面了。

![](img/792720823146d68f19fd50c99ebfce4b_105_0.png)

**图 2-22**：自定义安装的安装摘要。

# 第 3 章：故障排除和 Linux 配置

## 本章内容

- 故障排除安装
- 配置 X 窗口系统
- 设置打印机
- 管理 DVD 和 CD-ROM
- 安装额外的软件包

在 Linux 安装过程中，安装程序试图检测关键硬件组件，例如 SCSI 控制器和网络卡。根据检测到的情况，安装程序引导你完成一系列安装步骤。例如，如果安装程序无法检测网络卡，它会跳过网络配置步骤。如果你实际上没有网络卡，这完全没问题；但如果你有网络卡而安装程序错误地坚持认为你没有，那你就遇到了安装问题。



另一个可能出现的问题是在你重启 PC 时，没有得到图形登录屏幕，而是得到了文本终端。这意味着 X 窗口系统（或 X）配置存在问题。

此外，典型的 Linux 安装并不包含针对 PC 系统上所有硬件的配置程序。例如，大多数安装不会在安装过程中设置打印机。

在本章中，我将向你展示一些故障排除安装问题的方法。我将向你展示如何配置 X 以启动图形用户界面屏幕，以及如何配置打印机。

你可能还必须从配套 DVD-ROM 安装额外的软件包。我将向你展示如何安装不同格式的软件包，例如 Red Hat 软件包管理器（RPM）和 Debian 软件包——大多数 Linux 软件发布的两种格式。

## 使用文本模式安装

大多数 Linux 安装程序都会尝试使用 X Window System 来显示图形化安装界面。例如，如果安装程序未能检测到显卡，X 将无法启动。如果——出于这个原因或其他任何原因——安装程序无法启动 X，你始终可以退回到文本模式安装。这样，你可以手动指定显卡，或者稍后使用独立的配置程序来配置 X。你还可以通过编辑其文本配置文件来配置 X。

表 3-1 列出了如何从本书 DVD 中包含的 Linux 发行版的初始安装界面进入文本模式安装。通常，文本模式安装流程与本小册子第 2 章中我概述的图形安装流程相似。你只需响应提示并完成安装即可。

| 发行版 | 如何进入文本模式安装程序 |
| :--- | :--- |
| Debian | 支持文本模式 |
| Fedora Core | 从 Fedora Core CD 或 DVD 启动 PC 后，在 `boot:` 提示符处输入 `text` |
| Knoppix | 在 `boot:` 提示符处输入 `knoppix 2` 以文本模式启动 Knoppix（由于 Knoppix 是 Live CD 发行版，你无需安装它） |
| SUSE | 在第一个安装界面上，按 F3 并使用箭头键选择文本模式选项。按 Enter。 |
| Ubuntu | 基于 Debian 安装程序，支持 `text mode` |
| Xandros | 启动 CD 时按住 Shift 键并选择 Rescue Console。当出现 `bash-3.00#` 提示符时，输入 `quick_install` 并按照说明操作。 |

## 排查 X 故障

在我的一台较旧的 PC 上，每次安装 Linux 时我都会遇到这个问题：安装过程中，GUI 安装运行正常，但在安装后首次重启 PC 时，图形登录界面并未出现。相反，我最终得到了一个文本登录界面，或者启动过程似乎挂起并显示灰色屏幕。如果你遇到这个问题，以下是排查故障的方法：

1. 按 Ctrl+Alt+Delete 重启 PC。

PC 开始启动。你会看到一个 GRUB 引导加载程序提示你选择要启动的操作系统的界面。（如果该发行版使用 LILO 作为引导加载程序，你会看到一个文本提示符。）

2. 对于 GRUB，按 A 键为 Linux 内核添加一个选项。对于 LILO，跳过此步骤。

GRUB 引导加载程序随后显示 Linux 内核的命令行，并提示你添加所需内容。

3. 对于 GRUB，输入空格后跟单词 `single` 并按 Enter。对于 LILO，输入 `linux single` 并按 Enter。

Linux 内核以单用户模式启动，并显示如下类似的提示符：

```
sh-3.00#
```

现在你可以开始配置 X 了。

X 使用配置文件（根据你的发行版，该文件名为 `XF86Config-4` 或 `xorg.conf`）来确定显示卡类型、监视器以及你想要的屏幕分辨率。Linux 安装程序会准备配置文件，但有时配置并不正确。

要快速创建可用的配置文件，请遵循以下步骤：

1. 输入以下命令：

```
X -configure
```

2. 使用文本编辑器（如 `vi`）编辑 `/etc/xorg.conf.new` 文件，并在 `Section "Files":` 行后插入以下行：

```
FontPath "unix/:7100"
```

在 Fedora Core 上，你还必须将 `/dev/mouse` 更改为 `/dev/input/mice`。

3. 输入 `xfs &` 以启动 X 字体服务器。

4. 在 Debian 和 MEPIS 上，通过输入 `X -xf86config /XF86Config.new` 来尝试新的配置文件。在 Fedora Core、SUSE、Ubuntu 和 Xandros 上，通过输入 `X -config /etc/xorg.conf.new` 来尝试新的配置文件。

5. 按 Ctrl+Alt+Backspace 终止 X 服务器。

6. 使用以下命令将新的配置文件复制到 `/etc/X11` 目录（在 Debian 和 MEPIS 上，将第一个文件名更改为 `XF86Config.new`，第二个更改为 `XF86Config-4`）：

```
cp /etc/xorg.conf.new /etc/X11/xorg.conf
```

7. 按 Ctrl+Alt+Delete 或输入 `reboot` 重启 PC。

如果一切顺利，你应该能看到图形登录界面。

![](img/792720823146d68f19fd50c99ebfce4b_108_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_109_0.png)

使用 X 服务器的 `-configure` 选项创建的 X 配置文件并不会显示最佳可能的分辨率。要微调配置文件，你必须在重启系统后运行一个实用程序来调整显示设置。具体使用的实用程序取决于你的 Linux 发行版，但大多数发行版都包含一个允许你通过图形用户界面配置显卡、监视器和显示设置的实用程序。

## 解决其他安装问题

我确信我并没有穷尽所有潜伏在安装中的问题。没有人能做到。Intel x86 PC 中组件的组合方式如此之多，以至于墨菲定律几乎必然要求存在某种安装程序无法处理的硬件组合。本节列出了一些已知问题。对于其他问题，我建议你去 Google Groups（[http://groups.google.com](http://groups.google.com)）并输入一些故障症状。假设其他人也遇到类似的问题，你可以从中得到一些如何排查并走出特定困境的指示。

### 使用 Knoppix 启动命令

Knoppix Live CD 可以是一个出色的故障排查工具，因为 Knoppix 擅长检测硬件，并且你可以直接从 CD 运行它。当然，有时你可能在启动 Knoppix 本身时也会遇到问题。如果发生这种情况，你可以尝试在 `boot:` 提示符处输入 Knoppix 启动命令。例如，如果 Knoppix 似乎在尝试检测 SCSI 卡时挂起，你可以通过在 `boot:` 提示符处输入 `knoppix noscsi` 来禁用 SCSI 探测。或者，如果你希望 X 服务器加载 `nv` 模块（用于基于 NVIDIA 芯片组的显卡），你可以输入 `knoppix xmodule=nv` 在 `boot:` 提示符处。表 3-2 列出了一些常见的 Knoppix 启动命令。

**表 3-2 常见的 Knoppix 启动命令**

| 启动命令 | 作用 |
| :--- | :--- |
| `expert` | 以 `专家模式` 启动，允许用户交互式和配置 Knoppix |
| `failsafe` | 不尝试检测硬件即可启动（除了启动 Linux 所需的最基本条件） |
| `fb1280x1024` | 使用指定分辨率的固定帧缓冲图形（指定你需要的分辨率，如 1024 x 768、800 x 600 等） |
| `knoppix 1` | 以运行级别 1（单用户模式）启动 Knoppix，可用于执行救援操作 |
| `knoppix 2` | 以运行级别 2 启动，仅提供文本模式 shell 提示符 |
| `knoppix acpi=off` | 完全禁用 ACPI（高级配置和电源接口） |
| `knoppix atapicd` | 使用 ATAPI CD-ROM 接口，而不是为 IDE CD-ROM 驱动器模拟 SCSI 接口 |
| `knoppix desktop=wmname` | 使用指定的窗口管理器，而不是默认的 KDE（`wmname` 可以是：`fluxbox`、`icewm`、`kde`、`larwm`、`twm`、`wmaker` 或 `xfce`）。 |
| `knoppix dma` | 为所有 IDE 驱动器启用直接内存访问（DMA） |
| `knoppix floppyconfig` | 从软盘运行名为 `knoppix.sh` 的 shell 脚本（该 shell 脚本包含你希望运行的 Linux 命令。） |
| `knoppix fromhd=/dev/hda1` | 从位于指定硬盘分区中之前复制的 Live CD 镜像启动 |



| `knoppix hsync=80` | 为 X 使用 80 kHz 的水平刷新率（输入你希望 X 使用的水平刷新率） |
| `knoppix lang=xx` | 将键盘语言设置为由两位字母代码 `xx` 指定的语言（对于 `xx` 使用以下之一：`cn` = 简体中文、`de` = 德语、`da` = 丹麦语、`es` = 西班牙语、`fr` = 法语、`it` = 意大利语、`nl` = 荷兰语、`pl` = 波兰语、`ru` = 俄语、`sk` = 斯洛伐克语、`tr` = 土耳其语、`tw` = 繁体中文，或 `us` = 美式英语） |
| `knoppix mem=256M` | 指定 PC 具有说明中的内存量（以兆字节为单位） |
| `knoppix myconf=/dev/hda1` | 从 `/dev/hda1` 分区运行 shell 脚本 `knoppix.sh`（输入拥有 `knoppix.sh` 文件的分区名称。） |
| `knoppix myconf=scan` | 让 Knoppix 搜索名为 `knoppix.sh` 的文件并执行该文件中的命令（如果有） |
| `knoppix no eject` | 在你终止 Knoppix 后不会弹出 Live CD |
| `knoppix noprompt` | 在你终止 Knoppix 后不会提示移除 Live CD |
| `knoppix no wheelmouse` | 强制 PS/2 鼠标或触控板使用 PS/2 协议（而不是自动检测） |
| `knoppix no xxxx` | 让 Knoppix 跳过硬件检测的特定部分（其中 `xxxx` 标识了不应探测的硬件或服务器：`apic` = 高级可编程中断控制器、`apm` = 加速图形端口、`apm` = 高级电源管理、`audio` = 声卡、`d&c` = 显示数据通道、`dhcp` = 动态主机配置协议、`fstab` = 文件系统表、`firewire` = IEEE 1394 高速串行总线、`pcmcia` = PC 卡、`scsi` = 小型计算机系统接口、`swap` = 用于虚拟内存的硬盘空间、`usb` = 通用串行总线） |

### 表 3-2（续）

| 启动命令 | 功能说明 |
| :--- | :--- |
| knoppix pci=bios | 对存在缺陷的 PCI 控制器直接使用 BIOS |
| knoppix pnpbios=off | 跳过即插即用 (PnP) BIOS 初始化 |
| knoppix screen=1280x1024 | 将屏幕分辨率设置为 1280 x 1024 像素（请输入您想要的任何分辨率，例如 1024x768、800x600、640x480 等） |
| knoppix testcd | 通过使用 MD5 校验和来检查 Live CD 的数据完整性 |
| knoppix tohd=/dev/hda1 | 将 Live CD 复制到指定的硬盘分区，并从中运行 |
| knoppix toram | 将 Live CD 复制到 RAM（内存）并从中运行（需要 1GB 内存） |
| knoppix vga=ext | 使用 50 行文本模式显示 |
| knoppix vsync=60 | X 窗口系统使用 60 Hz 的垂直刷新率（请输入您希望 X 使用的垂直刷新率） |
| knoppix wheelmouse | 为滚轮鼠标启用 IMPS/2 协议 |
| knoppix xmodule=modname | 使 X 服务器加载由 modname 指定的模块，以便 X 能在您的显卡上工作（modname 可以是 ati1、fbdev、i810、mga、nv、radeon、savage、svga 或 s3 之一。） |
| knoppix xserver=progname | 启动由 progname 指定的 X 服务器（可以是 XFree86 或 XF86_SVGA 之一） |

![](img/792720823146d68f19fd50c99ebfce4b_111_0.png)

当您有多个 Knoppix 启动命令时，只需将它们组合到一行中即可。例如，要指定跳过 SCSI 自动检测、关闭 ACPI、使用美国键盘布局、使用滚轮鼠标，并要求 X 服务器加载 nv 模块，您应在 boot: 提示符下输入以下内容：

`knoppix noSCSI acpi=off lang=us wheelmouse xmodule=nv`

## 致命的信号 11 错误

有些人在安装过程中会遇到致命的信号 11 错误消息——这会立即停止进程。此错误通常发生在初始启动屏幕之后，安装程序开始启动其图形用户界面 (GUI) 或文本界面时。安装过程中出现信号 11 错误最可能的原因是与内存或与 CPU（微处理器）相关的缓存有关的硬件错误。

## 解决其他安装问题

信号 11，也称为 SIGSEGV（Segment Violation Signal 的缩写，即段违例信号），可能会发生在 Linux 应用程序中。当进程试图访问它不应访问的内存位置时，会发生*段违例*。操作系统在问题发生前检测到该问题，并通过向违规进程发送信号 11 来停止该进程。如果这种情况发生在安装过程中，这意味着安装程序在访问内存时出现了错误，最可能的原因是硬件问题。针对信号 11 问题常用的建议修复方法是关闭 BIOS 中的 CPU 缓存。为此，您必须在 PC 启动时进入 Setup（通过按功能键，如 F2），并从 BIOS Setup 菜单中关闭 CPU 缓存。

![](img/792720823146d68f19fd50c99ebfce4b_112_0.png)

如果问题是由于内存中的硬件错误引起的（换句话说，是由于内存芯片故障导致的），您可以尝试将内存模块在插槽之间互换位置。如果您手头有备用模块，也可以考虑用另一个内存模块替换现有的内存模块。

您可以访问 www.bitwizard.nl/sig11 阅读更多关于信号 11 问题的信息。

## 绕过 PC 重启问题

在一些 PC 上，当您在启动提示符下按 Enter 键时，初始 Linux 内核加载后会立即重启 PC。这可能是由于 PC BIOS 中 ACPI 的实现存在缺陷所致。要绕过此问题，请在启动提示符下输入 `linux acpi=off` 以关闭 ACPI；如果不起作用，请查阅表 3-3 以查找您可能想要尝试的其他启动选项。

## 使用 Linux 内核启动选项

当您从 DVD 或第一张 CD-ROM 启动 PC 进行 Linux 安装时，会出现带有 boot: 提示符的文本屏幕。通常，您在该提示符下按 Enter 键或不做任何操作，安装程序稍后就会开始。但是，您可以相当多地指定 boot: 提示符下的各种选项。这些选项控制 Linux 内核启动的各个方面，例如禁用对故障硬件的支持，或使用特定的 X 驱动模块启动 X 服务器。其中一些启动选项有助于绕过您在安装过程中可能遇到的问题。

要使用这些启动选项，通常您需要输入 `linux` 后跟启动选项。例如，要执行测试模式安装并告诉内核您的 PC 有 512MB 内存，请在 boot: 提示符下输入以下内容：

```
linux text mem=512M
```

请查阅表 3-3 以获取部分 Linux 启动选项的简要摘要。您可以使用这些命令来开启或关闭特定功能。

虽然我在讨论安装问题故障排除的上下文中提到了这些 Linux 内核启动命令，但您可以随时使用其中许多命令，只要您使用任何 Linux 发行版启动 PC 并希望开启或关闭特定功能即可。

### 表 3-3 一些 Linux 启动选项

| 使用此启动选项 | 以执行此操作 |
| :--- | :--- |
| allowcdmdma | 为 CD/DVD 驱动器启用 DMA |
| apic | 解决在 Intel 440GX 芯片组 BIOS 中常见的错误，并且仅在安装程序内核上执行 |
| acpi=off | 如果存在 ACPI 问题，则禁用 ACPI |
| dd | 在 Red Hat Linux 安装过程中提示输入驱动器软盘 |
| display=IP_address:0 | 使安装程序 GUI 显示在由 IP 地址标识的远程系统上。（请确保您在运行安装程序的远程系统上执行命令 `xhost +hostname`，其中 hostname 是运行安装程序的主机。） |
| driverdisk | 在 Red Hat Linux 安装过程中提示输入驱动器软盘 |
| enforcing=0 | 关闭 Security Enhanced Linux (SELinux) 强制访问控制 |
| expert | 允许您分区可移动介质并提示输入驱动器软盘 |
| ide=nodma | 在所有 IDE 设备上禁用 DMA，在您遇到与 IDE 相关的问题时可能很有用 |
| ks | 使用 DHCP 配置网卡，并使用 NFS 服务器上的 kickstart 文件进行 kickstart 安装，该服务器由 DHCP 服务器提供的启动服务器参数标识 |



| `ks=kickstartfile` | 使用指定的 kickstartfile 中的 kickstart 文件进行 kickstart 安装。（kickstart 背后的理念是创建一个包含所有安装选项的文本文件，然后通过启动并提供该 kickstart 文件作为输入来触发安装。） |
| `lowres` | 强制安装程序 GUI 以较低分辨率 (640 x 480) 运行 |
| `mediacheck` | 提示您检查 CD 映像（也称为 ISO 映像）的完整性。检查映像是通过计算 MD5 校验和并将其与官方的 Fedora Core 值进行比较来完成的。检查 CD-ROM 可能需要几分钟时间。 |
| `mem=xxxM` | 覆盖内核在 PC 上检测到的内存数量。（一些旧机器可能只能检测 16MB 内存，而在一些新机器上，显卡可能会使用主内存的一部分。）请确保将 `xxx` 替换为代表您的 PC 上内存兆字节数的数字。 |
| `nmi_watchdog=1` | 启用利用不可屏蔽中断 (NMI) 的内核内置死锁检测器 |

## 解决其他安装问题

| 使用此启动选项 | 以实现此操作 |
| :--- | :--- |
| `noapic` | 防止内核使用高级可编程中断控制器 (APIC) 芯片。（你可以将此命令用于已知存在不良 APIC 的主板。） |
| `nofirewire` | 不加载火线（FireWire）支持 |
| `noht` | 禁用`超线程 (Hyper-Threading)`，这是一种使单个处理器在硬件级别表现为多个虚拟处理器的功能。 |
| `nomce` | 禁用通过机器检查异常 (MCE) 对 CPU 进行的自我诊断检查。在某些机器上，这些检查执行过于频繁，因此需要禁用它们。 |
| `nomount` | 在救援模式下不自动挂载任何已安装的 Linux 分区 |
| `nopass` | 不将键盘和鼠标信息传递给安装程序的第二个阶段 |
| `nopcmcia` | 忽略系统中的任何 PCMCIA 控制器 |
| `noprobe` | 禁用自动硬件检测，转而提示用户输入关于 PC 上安装的 SCSI 和网络硬件的信息。你可以使用这种方法向模块传递参数。 |
| `noshell` | 在安装期间禁用虚拟控制台 2（通过按下 `Ctrl+Alt+F2` 进入的控制台）的 shell 访问权限 |
| `nousb` | 在安装期间禁用 USB 支持加载。（如果安装程序在早期阶段挂起，这可能很有用。） |
| `nousbstorage` | 禁用安装程序加载器中 `usbstorage` 模块的加载。它可能有助于解决 SCSI 系统上的设备排序问题。 |
| `reboot=b` | 更改内核尝试重启 PC 的方式，使其即使在系统关机期间内核挂起时也能重启 |
| `pci=noacpi` | 导致内核不使用 ACPI 来路由中断请求 |
| `pci=biosirq` | 导致内核使用 BIOS 设置来路由中断请求 (IRQs) |
| `rescue` | 以救援模式启动内核，此时你会看到一个 shell 提示符，并可以尝试修复问题 |
| `resolution=HHHHxVVV` | 使安装器 GUI 在指定的视频模式下运行。（请确保将 `HHHH` 和 `VVV` 替换为标准分辨率数字，例如 640x480、800x600、1024x768 等。） |
| `selinux=0` | 禁用 SELinux 内核扩展 |
| `serial` | 在安装期间启用串行控制台支持 |
| `skipddc` | 跳过监视器的显示数据通道 (DDC) 探测。（如果探测导致问题，这将很有用。） |
| `vnc` | 启动一个 VNC (Virtual Network Computing) 服务器，以便你可以从另一个运行 VNC 客户端的网络系统控制 GUI 安装器 |

![图 3-1](img/792720823146d68f19fd50c99ebfce4b_114_0.png)

## 设置打印机

在大多数 Linux 发行版中，你只能在安装完发行版之后才能设置打印机。以下各部分概述了本书光盘中每种发行版的打印机配置步骤——Debian、Fedora Core、Knoppix、MEPIS、SUSE、Ubuntu 和 Androids。

### 在 Debian 中配置打印机

Debian 附带了 `foomatic-gui` 实用工具，该工具允许你通过图形界面配置打印机，如图 3-1 所示。要配置打印机，请将打印机连接到适当的端口——并行端口或 USB 端口——并打开电源。然后按照以下步骤操作：

1. 从图形桌面选择 应用程序→系统工具→打印机 以启动 `foomatic-gui`。
   如果你未以 root 身份登录，对话框会提示你输入 root 密码。
   如果你找不到该菜单项，请打开一个终端窗口，执行 `su -` 以成为 root，然后输入 `export DISPLAY=:0.0; foomatic-gui`。`foomatic-gui` 实用工具将显示其主窗口，如图 3-1 所示。
   ![图 3-1](img/792720823146d68f19fd50c99ebfce4b_115_0.png)
2. 点击工具栏上的“添加”。（参考图 3-1。）
   `foomatic-gui` 工具将启动“添加打印机向导”（参见图 3-2），引导你完成向系统添加新打印机的过程。
   ![图 3-2](img/792720823146d68f19fd50c99ebfce4b_116_0.png)
   *图 3-2：添加打印机向导将引导你完成各个步骤。*
3. 点击“下一步”。
   “添加打印机向导”显示打印机的多种不同连接类型。
4. 从列表中选择你的打印机连接方式。
   要添加网络连接的打印机，点击“检测网络打印机”，你将看到一个打印机列表，包括网络上可用的 Windows 打印机。选择打印机连接后，`foomatic-gui` 会要求你为用于保存该打印机打印作业的队列输入一个名称。
5. 输入打印机队列的名称以及关于打印机的识别信息（位置和简短描述），然后点击“下一步”。
   `foomatic-gui` 工具显示打印机制造商和型号列表。
6. 选择打印机的制造商和型号，然后点击“下一步”。
   `foomatic-gui` 工具显示适用于此打印机的驱动程序。
7. 选择你要使用的驱动程序，然后点击“下一步”。
   选择标记为“推荐”的驱动程序。`foomatic-gui` 工具显示一条消息，指出你可以通过点击“应用”来添加打印机。
8. 点击“应用”以添加打印机。
   从 `foomatic-gui` 窗口（参考图 3-1），你可以选择一个打印机并点击“测试页”按钮来打印测试页。

### 在 Fedora Core 中配置打印机

Fedora Core 安装程序不包含打印机配置步骤，但你可以通过图形实用程序轻松配置打印机。要设置打印机，请按照以下步骤操作：

1. 从 GNOME 桌面选择 系统→管理→打印。
   如果你未以 `root` 身份登录，打印机配置工具会提示你输入 `root` 密码。该打印机配置工具名为 `system-config-printer`。图 3-3 显示了其主窗口。
   ![图 3-3](img/792720823146d68f19fd50c99ebfce4b_117_0.png)
2. 点击“新建”按钮以配置新打印机。
   Fedora Core 的打印机配置向导将启动。初始窗口显示一条消息，保证你在点击所有步骤末尾的“应用”按钮之前，什么都会不改变。
3. 点击“下一步”继续。
4. 输入打印队列的名称和打印队列的简短描述。然后点击“下一步”。
   在命名打印队列时使用一些系统化的方法。例如，如果我在二楼 210 房间有一台 HP Laserjet 5000 打印机，我可能会将队列命名为 `Room210PLJ5000`，因为这个名字使查找打印机更容易。有时系统管理员会选择可爱的名字，如 `kermit`、`piggy`、`elmo`、`cookiemonster` 等，但当你有大量打印机时，这种可爱的方案并不好用。在打印队列名称中提供有关打印机位置以及制造商和型号的线索是最佳做法。
5. 在下一个屏幕（参见图 3-4）中，从下拉列表中选择一个队列类型。然后点击“下一步”。
   选择适用于你情况的打印队列类型。例如，如果你想在共享的 Windows 打印机上打印，请选择“网络 Windows (SMB)”。
   ![图 3-4](img/792720823146d68f19fd50c99ebfce4b_117_1.png)
   *图 3-4：从此窗口选择打印队列类型。*
   ![图 3-4 替代方案](img/792720823146d68f19fd50c99ebfce4b_118_0.png)
   要设置连接到你 PC 并行端口的打印机，请选择“本地连接”。



可用以下类型的打印队列：

- **本地连接**：指直接连接到 PC 的串行、并行或 USB 端口的打印机。
- **网络 CUPS (IPP)**：指网络中另一台服务器上的通用 UNIX 打印系统 (CUPS) 打印队列（IPP 指用于与远程 CUPS 服务器通信的互联网打印协议）。
- **网络 UNIX (LPD)**：指由本地网络上另一台 UNIX 系统上的 LPD 服务器管理的打印队列。（LPD 指行式打印机守护进程——另一种 UNIX 系统的打印假脱机。）
- **网络 Windows (SMB)**：指连接到本地网络上另一台使用服务器消息块 (SMB) 协议的 PC 的打印机，SMB 是 Windows 文件和打印共享的底层协议。
- **网络 Novell (NCP)**：指连接到本地网络上的 Novell Netware 服务器的打印机。
- **网络 JetDirect**：指直接连接到本地网络的 HP JetDirect 打印机。

6. **如果你选择“本地连接”，屏幕下半部分将显示检测到的并行端口信息。点击该端口以选择它，然后点击“下一步”继续。**

对于其他选项，屏幕将提示你识别网络打印机。指定网络打印机的方式取决于网络类型。例如，要在你的局域网中使用 IP 地址为 192.168.0.8 的主机上的网络 CUPS 打印机，你必须输入类似 `http://192.168.0.8:631/printers/HPLaserJetRoom210` 的名称，其中 `HPLaserJetRoom210` 是网络打印机的名称。

7. **选择打印机的制造商和型号，然后单击“下一步”。**

单击下拉列表（位于滚动列表上方）以显示打印机制造商列表。当你从该列表中选择打印机制造商时，滚动列表将显示该制造商的不同打印机型号名称。如果你使用的是 PostScript 打印机，可以直接转到“通用”列表（“通用”是制造商列表中的一个选项），然后选择 PostScript 打印机。

最后一个屏幕显示新打印队列的相关信息。

8. **审核所有信息以确保其正确无误，然后单击“完成”以创建打印队列。**

9. **当出现询问是否打印测试页的对话框时，单击“是”。**

这样做会应用所有更改并重启负责打印的 `print-scheduler` 程序。此时，打印机将打印一张测试页，随后会出现一个消息框，提示你检查测试页。

10. **单击“确定”以关闭消息框。**

新的打印队列将出现在打印机配置窗口中，你可以向此队列提交打印作业。

11. **选择“操作::退出”以关闭打印机配置工具。**

或者，你可以单击窗口框架右上角的 X 按钮来关闭打印机配置窗口。

12. **系统提示你保存打印机信息。单击“保存”以保存设置并退出打印机配置工具。**

# 在 Knoppix 和 MEPIS 中配置打印机

在 Knoppix 和 MEPIS 中配置打印机的大多数步骤都相似，因此我将在本节中同时介绍它们。要在 Knoppix 或 MEPIS 中添加打印机，请遵循以下步骤：

1. **从 Knoppix 桌面选择“主菜单::KNOPPIX::配置::配置打印机”。从 MEPIS 桌面选择“主菜单::打印系统::打印管理器”。**

这将启动打印机配置工具。图 3-5 显示了 MEPIS 中的主窗口。Knoppix 中的主窗口看起来相似。

2. **单击工具栏上的“添加”，然后从下拉菜单中选择“添加打印机/类别”。**

打印机配置工具将启动“添加打印机向导”（见图 3-6），该向导将引导你完成各个步骤。

![](img/792720823146d68f19fd50c99ebfce4b_120_0.png)

图 3-5：在 Knoppix 和 MEPIS 中，通过这个 GUI 工具配置和管理打印机。

![](img/792720823146d68f19fd50c99ebfce4b_120_1.png)

图 3-6：通过“添加打印机向导”添加新打印机。

3. **单击“下一步”，然后在接下来的屏幕上选择打印机连接类型。然后单击“下一步”。**

这可以是本地并口、串口或 USB 端口，也可以是支持 TCP 或 IPP 等不同协议的网络打印机。

第一卷

第 3 章

故障排除和 Linux 配置

根据你的打印机连接类型，向导会提示你提供更多详细信息。例如，对于本地打印机，你需要从列表中选择并口、串口或 USB 端口。

4. **提供关于打印机连接的信息——本地端口或标识网络打印机的 URL。单击“下一步”。**

向导将显示打印机制造商和型号的列表，如图 3-7 所示。

![](img/792720823146d68f19fd50c99ebfce4b_121_0.png)

5. **选择你打印机的制造商和型号，然后单击“下一步”。**

向导将显示驱动程序的列表及其推荐选项。

6. **选择打印机驱动程序，然后单击“下一步”。**

向导将显示一个屏幕（见图 3-8），你可以从中测试打印机设置。

7. **选择是否希望在每个打印作业后显示横幅，然后单击“下一步”。**

8. **设置任何配额，例如页面限制或发送到打印机的文件大小限制，然后单击“下一步”。**

9. **指定用户访问设置，例如哪些用户可以访问打印队列，然后单击“下一步”。**

10. **为打印队列命名并添加打印机描述。单击“下一步”。**

11. **审核打印机设置，然后单击“完成”以添加打印机。**

# 在 SUSE 中配置打印机

要在 SUSE 中添加打印机，请遵循以下步骤：

1. **选择“主菜单 → 系统 → 控制中心 (YaST)”，在提示时输入 root 密码，然后单击窗口左侧的“硬件”。**

YaST 控制中心显示关于各种硬件的信息，如图 3.9 所示。正如你所见，你可以从 YaST 配置各种硬件。

![](img/792720823146d68f19fd50c99ebfce4b_122_0.png)

**图 3-8：** 在安装打印机之前测试打印机设置。

![](img/792720823146d68f19fd50c99ebfce4b_122_1.png)

**图 3-9：** 要配置任何内容，请从 YaST 控制中心开始。

2. **单击窗口右侧的“打印机”。**

YaST 打开打印机配置窗口，并显示它检测到的任何打印机的信息，如图 3-10 所示。

![](img/792720823146d68f19fd50c99ebfce4b_123_0.png)

3. **如果你的打印机已被检测到，请继续步骤 4。如果你的打印机未被检测到，请单击“添加”。**

YaST 将显示打印机类型列表（见图 3-11），你可以从中选择你的打印机。类型取决于你的打印机如何连接到你的 PC（通过并口、串口、USB 或网络）。

4. **选择你的打印机类型，然后单击“下一步”。**

YaST 将根据你选择的打印机类型提示你提供更多信息。例如，对于并口打印机，你需要标识打印机连接的并口。

5. **提供关于打印机连接的信息，然后单击“下一步”。**

YaST 将提示你输入打印队列的名称和其他相关信息。

6. **输入打印队列的名称以及关于打印机的一些描述信息，然后单击“下一步”。**

YaST 将显示打印机制造商和型号的列表。

7. **选择你打印机的制造商和型号。然后单击“下一步”。**

YaST 将显示当前配置信息，以便你可以测试配置或对其进行编辑。

## 设置打印机

![](img/792720823146d68f19fd50c99ebfce4b_124_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_124_0.png)

图 3-11：在此窗口中选择你的打印机类型。

8. **审核配置信息，然后单击“确定”。**

“添加打印机向导”关闭并返回到 YaST 打印机配置窗口。

9. **单击“确定”以保存设置。**

### 在 Ubuntu 中配置打印机

要在 Ubuntu 中添加打印机，请遵循以下步骤：

1. **选择“系统 → 管理 → 打印”。**

将出现“打印机”窗口，如图 3-12 所示。

![](img/792720823146d68f19fd50c99ebfce4b_124_2.png)

![](img/792720823146d68f19fd50c99ebfce4b_124_2.png)

图 3-12：在 Ubuntu 中，从此窗口管理打印机。

2. **单击“新打印机”（参见图 3-12）。**

这将启动“添加打印机”助手（见图 3-13），该助手将引导你完成打印机安装步骤。

![](img/792720823146d68f19fd50c99ebfce4b_125_0.png)

3. **选择打印机连接（参见图 3-13），然后单击“下一步”。**

你可以选择打印机类型——本地或网络——或者选择检测到的打印机或打印机端口（USB 或并口）。

4. **选择打印机制造商并从列表中挑选型号（见图 3-14）。**

对于选定的打印机型号，将显示推荐的驱动程序。

5. **单击“应用”。**



这将安装打印机并关闭“添加打印机”助手。打印机的图标将出现在图 3-12 所示的“打印机”窗口中。

## 在 Xandros 中配置打印机

当你第一次运行 Xandros 时，“首次运行向导”会给你一个配置打印机的机会。图 3-15 显示了“首次运行向导”显示打印机信息并提供添加新打印机机会的屏幕。

![](img/792720823146d68f19fd50c99ebfce4b_126_0.png)

图 3-14：在此步骤中选择打印机的制造商和型号。

![](img/792720823146d68f19fd50c99ebfce4b_126_1.png)

图 3-15：Xandros 中的打印机配置步骤。

如果你在第一次重启时跳过了它，你总是可以通过选择“主菜单 → 应用程序 → 系统 → 首次运行向导”来启动“首次运行向导”。

从“首次运行向导”的`打印机`屏幕，请遵循以下步骤来配置打印机：

1. 单击“首次运行向导”打印机屏幕中的“添加”按钮（参见图 3-15）。
“添加打印机向导”启动，如图 3-16 所示。
2. 选择打印机类型——本地打印机或网络打印机——然后单击“下一步”。
向导会提示你提供有关打印机连接的更多详细信息。
3. 提供打印机连接的相关信息，然后单击“下一步”。
例如，对于本地打印机，请指定它是并行端口打印机还是 USB 打印机。向导将显示一个界面，你可以从中选择打印机的制造商、型号和驱动程序。
4. 选择你的打印机制造商、型号和驱动程序，如图 3-17 所示。单击“下一步”。

![](img/792720823146d68f19fd50c99ebfce4b_127_1.png)

向导会给你打印测试页并完成打印机配置的选项。
5. 单击`完成`以完成打印机配置。

完成打印机配置后，首次运行向导将继续执行其他配置任务。

## 管理 DVD 和 CD-ROM

图形用户界面（GUI）桌面使在 Linux 中使用 DVD 和 CD-ROM 变得轻而易举。只需将 DVD 或 CD-ROM 插入光驱，桌面上就会出现一个图标。

然后，你可以通过双击桌面上的图标来访问 CD 或 DVD。

若要访问文件和文件夹，只需双击在 GUI 文件管理器窗口中出现的图标即可。在某些 Linux 发行版中，在你将 CD 或 DVD 插入光驱后，GUI 会自动在文件管理器窗口中打开 CD 或 DVD 的内容。

如果你看到 DVD/CD-ROM 图标，请右键单击该图标以呼出上下文菜单。从该菜单中，你可以在使用完毕后弹出 CD 或 DVD。

![](img/792720823146d68f19fd50c99ebfce4b_128_0.png)

Knoppix 和 MEPIS 桌面为每个检测到的驱动器显示图标。若要打开 CD 或 DVD，只需单击该驱动器的图标即可。在 SUSE 中，单击“我的电脑”图标，然后单击 DVD/CD 光驱的图标。Ubuntu 会在 Nautilus 窗口中打开 CD/DVD，并在桌面上放置一个图标。Xandros 桌面会在 Xandros 文件管理器窗口中打开 CD/DVD。

# 安装其他软件

安装软件的具体步骤取决于软件分发的软件包类型。大多数 Linux 软件以 RPM 文件或 Debian 软件包文件的形式提供。RPM 文件扩展名为`.rpm`，Debian 软件包扩展名为`.deb`。

大多数发行版都提供图形界面安装程序，以简化新软件包的安装过程。在本节中，我将简要概述在 Debian、Fedora Core、SUSE 和 Xandros 中添加软件的方法。通常你不会在 Knoppix（或其他任何 Live CD 发行版）中添加软件，因为 Live CD 发行版是从 CD-ROM 运行的。

![](img/792720823146d68f19fd50c99ebfce4b_129_0.png)

Fedora Core 和 SUSE 使用 RPM 软件包。Debian、MEPIS、Ubuntu 和 Xandros 都是基于 Debian 的发行版，因此不出所料，它们通常使用 Debian 软件包（也称为 DEB）。然而，RPM 和 DEB 软件包都可以安装在任何 Linux 发行版中。

### 在 Debian、MEPIS 和 Ubuntu 中安装软件

在 Debian 以及 MEPIS 和 Ubuntu 等基于 Debian 的发行版中管理软件包的最佳方法是使用 APT —— 高级打包工具 —— 你通常通过`apt-get`命令来控制它。

安装 Debian 时，最后几个步骤之一是配置 APT 的软件源。`APT 软件源`是 APT 查找软件包以下载并安装到你系统上的 Internet 服务器（包括 FTP 和 Web 服务器）。假设 APT 已正确配置，并且你的系统拥有高速 Internet 连接，你可以在终端窗口中输入以下命令开始安装任何软件包：

```
apt-get install pkgname
```

其中`pkgname`是你想要安装的软件包名称。如果你不知道软件包名称，请在终端窗口中输入以下命令开始搜索：

```
apt-cache search keyword
```

其中`keyword`与你想要安装的软件包相关。例如，若要搜索描述中包含单词`screenshot`且还包含单词`KDE`的软件包，我会输入以下内容。（我使用`grep`在输出中搜索文本 KDE 的出现。）

```
apt-cache search screenshot | grep KDE
```

然后该命令会打印出以下一行作为结果：

```
ksnapshot - Screenshot application for KDE
```

这表明`ksnapshot`软件包就是我所需要的。如果该软件包尚未安装，我可以通过输入以下命令来安装它：

```
apt-get install ksnapshot
```

简而言之，这就是如何使用命令行工具在 Debian 中查找和安装软件包的方法。

Debian、MEPIS 和 Ubuntu 还附带一个名为 Synaptic Package Manager 的 APT GUI 软件包安装程序，其使用非常直观。若要尝试使用它，请在 Debian 的 GNOME 桌面中选择 应用程序 > 系统工具 > Synaptic Package Manager。在 MEPIS 中，选择 主菜单 > 系统 > Synaptic Package Manager。在 Ubuntu 中，选择 系统 > 管理 > Synaptic Package Manager。（在 Ubuntu 中，当提示输入密码时，请输入你的普通用户密码，因为 Ubuntu 没有 root 用户。）

Synaptic Package Manager 启动后，它会显示一个快速入门对话框，简要告诉你如何标记要安装、升级或删除的软件包，以及如何访问菜单来执行这些操作。阅读完入门介绍后，单击“关闭”以移除该对话框。

如果你的软件包信息已超过 48 小时，另一个对话框会提示你更新软件包信息。在该对话框中单击“重新加载”。Synaptic Package Manager 随后会下载最新的软件包信息，关闭对话框，并在主窗口中显示有关软件包的信息，如图 3-18 所示。

![](img/792720823146d68f19fd50c99ebfce4b_130_0.png)

通过单击 Synaptic Package Manager 窗口左侧的分类，你可以查看窗口右侧各类软件包的列表。每个软件包左侧的方框指示该软件包是否已安装。如果你单击软件包名称，Synaptic Package Manager 会在窗口右下角显示有关所选软件包的信息。

若要选择要安装或删除的软件包，请单击其名称左侧的方框，并从弹出的菜单中选择“标记为安装”或“标记为删除”。如果为安装选择某个软件包需要其他软件包，Synaptic Package Manager 会显示一个包含该信息的对话框，你可以单击“标记”以同时安装所需的软件包。标记任意数量的软件包，然后单击工具栏上的“应用”以执行所有已标记的操作。

### 在 Fedora Core 中安装软件

大多数 Fedora Core 软件以 RPM 文件的形式提供。`RPM`文件基本上是一个包含安装软件产品所需的一切——所有文件和配置信息——的单个软件包。

从 GNOME 桌面，使用“添加或删除软件包”实用程序 —— 一个用于安装和卸载 RPM 的图形实用程序。请遵循以下步骤：

- 1. 选择`系统`：`应用程序`：`添加/删除软件`。
如果你不是以`root`身份登录的，一个对话框会提示你输入`root`密码。“添加或删除软件包”实用程序启动并收集有关系统上已安装软件包状态的信息。在它梳理完所有已安装软件包的信息后，实用程序将显示“软件包管理”对话框，其中包含所有软件包的列表。（参见图 3-19。）

![](img/792720823146d68f19fd50c99ebfce4b_131_0.png)

**图 3-19：** 使用“添加或删除软件包”实用程序在 Fedora Core 中管理软件。



- 2. 若要安装未安装的软件包组，请选中该软件包组名称左侧的复选框。对于部分未安装的软件包组，单击软件包名称右侧列中出现的“详细信息”超链接。

会出现一个包含该软件包组中软件包详细信息的对话框。

- 3. 在对话框中，通过单击名称选择你想要安装或删除的软件包，然后单击“关闭”以退出对话框。

你将返回到“软件包管理”对话框，如果你添加或删除了任何软件包，“更新”按钮将变为激活状态。

- 4. 单击“更新”按钮以根据你在软件包列表中进行的任何添加或删除操作来更新软件包。

### 在 SUSE 中安装软件

在 SUSE 中，请遵循以下步骤来安装或删除软件：

- 1. 选择 主菜单: `YaST` 以启动图 3-20 中所示的 `YaST` 控制中心。

`YaST` 控制中心在左侧显示任务类别，在右侧显示该类别的具体任务。

![](img/792720823146d68f19fd50c99ebfce4b_132_0.png)

- 2. 单击左侧的“软件”类别，以便右侧显示软件的选项。

- 3. 单击右侧的“软件管理”图标（参见图 3-20）。

`YaST` 将显示一个新窗口，你可以在其中搜索软件包。

4. 按名称搜索软件包，或通过浏览可用软件包来选择软件包。

要按名称搜索软件包，请在窗口左上角的搜索框中输入关键词，然后单击“搜索”。`YaST` 会在窗口右侧显示匹配的软件包，如图 3-21 所示。要浏览软件包，请单击左上角的“过滤器”，从下拉列表中选择一个包组，然后单击某个组以查看该组中各个软件包的列表。

5. 单击右下角的“接受”按钮，开始安装所选软件包。

`YaST` 会在安装软件包之前检查依赖项——如果某个软件包需要正确安装其他软件包——。如果想在单击“接受”时查看将发生哪些更改，请单击“过滤器”并选择“安装摘要”。

## 在 Xandros 中安装软件

`Xandros` 桌面操作系统自带 `Xandros Networks`，它允许您在线购买软件，也可以从 CD 或 DVD 安装软件。要启动 `Xandros Networks`，请双击 `Xandros` 桌面上的 `Xandros Networks` 图标。`Xandros Networks` 启动后，将连接到 `Xandros` 服务器，并显示已安装、已更新和新应用的信息，如图 3-22 所示。

图 3-21：在此 `YaST` 窗口中查找并安装软件。

![](img/792720823146d68f19fd50c99ebfce4b_133_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_134_0.png)

图 3-22：使用 `Xandros Networks` 安装或升级软件。

要查看新应用程序列表，请单击 `Xandros Networks` 窗口左侧“新应用程序”标签旁边的加号（见图 3-23）。您将获得更详细的应用程序类别列表。如果单击某个类别，窗口右侧将显示该类别内的软件包名称。然后，您可以选择安装单个软件包或整个类别。

要安装任何选定的软件包，请选择“文件”->“进入管理员模式”。系统会提示输入管理员（root）密码。输入 root 密码后，您可以选择“文件”->“安装选定应用程序”。`Xandros Networks` 会检查依赖项，如果需要更多提示会询问您，并下载和安装新软件。

![](img/792720823146d68f19fd50c99ebfce4b_134_1.png)

如果您已下载了 `Debian` 软件包，可以通过从 `Xandros Networks` 菜单中选择“文件”->“安装 DEB 文件”来安装它。类似地，菜单选项“文件”->“安装 RPM 文件”可安装 `RPM` 软件包。（有关安装 `RPM` 软件包的更多信息，请参阅第五卷，第四章。）

# 110 安装其他软件

图 3-23：选择要安装的软件包。

![](img/792720823146d68f19fd50c99ebfce4b_135_0.png)

# 第 4 章：尝试 Linux

## 本章内容

- ✓ 启动 Linux
- ✓ 登录
- ✓ 体验图形桌面
- ✓ 玩转 shell
- ✓ 关机

您正坐在 PC 前，准备开机。您知道该 PC 已安装了 Linux。（也许是您自己安装的，但谁知道呢？）您正在想着开机后会看到什么，以及之后该做什么。别担心。如果您是第一次使用 Linux，本章将教您如何登录、体验图形桌面、尝试一些晦涩的 Linux 命令，最后再关机。

如果您尝试的是 `Knoppix` 活系统光盘，只需从 `Knoppix` 活系统光盘启动即可（如第一卷第二章所述），然后您可以像使用其他 Linux 发行版一样试用它。

对于那些已经了解一些 Linux 知识的人来说，请快速浏览本章，看看是否有您不了解的新内容。您永远不知道自己所不知道的！

## 启动 Linux

当您启动 PC 时，它会经历正常的开机序列，并加载引导加载程序——根据您的 Linux 发行版以及安装期间的选择，是 `GRUB` 还是 `LILO`。引导加载程序（曾称为自举加载程序）是一个微型计算机程序，它从硬盘加载操作系统的其余部分到计算机内存中。计算机启动的整个过程称为引导。

对于从 CD 启动的活系统光盘（如 `Knoppix`），引导加载程序通常是 `ISOLINUX`，这是一种专为 ISO 9660 CD-ROM 设计的引导加载程序。

`LILO` 和 `GRUB` 引导加载程序会显示一个图形屏幕，其中列出了引导加载程序可以加载的操作系统名称。例如，如果您的

![](img/792720823146d68f19fd50c99ebfce4b_136_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_136_1.png)

PC 装有 Windows 和 Linux，您会看到这两个名称都列在其中。然后，您可以使用向上和向下箭头键选择要使用的操作系统。如果 PC 被设置为默认加载 Linux，请等待几秒钟，引导加载程序将启动 Linux。更准确地说，引导加载程序将 Linux 内核——Linux 操作系统的核心——加载到 PC 的内存中。

其他引导加载程序，如 `ISOLINUX`，可能会显示一个文本 `boot:` 提示，在此处您可以输入 `boot` 命令以加载特定的操作系统并向该操作系统传递选项。

随着 Linux 内核启动，您会看到一长串启动信息，通常称为启动消息。（您随时可以在终端窗口中输入命令 `dmesg` 来查看这些消息。）这些消息包括 Linux 检测到的设备名称。启动消息中的第一行通常写着

```
Calibrating delay loop... 4997.12 BogoMIPS (lpj=2498560)
```

`BogoMIPS` 是 Linux 术语（本章侧栏中有详细解释），用于表示时间度量。`BogoMIPS` 前面的数字取决于您的 PC 处理器速度，无论是旧的 200 MHz Pentium 还是新的 4 GHz Pentium 4。当内核需要等待一小段时间以发生某些事件（如等待磁盘控制器就绪响应）时，会使用 `BogoMIPS` 测量值。

### 什么是 BogoMIPS 和 LPJ？

当 Linux 启动时，您会看到一条消息，内容为“Calibrating delay loop... 4997.12 BogoMIPS (lpj=2498560)”，其中 `BogoMIPS` 一词前有一个数字。`BogoMIPS` 是那些让新 Linux 用户困惑的词汇之一，但它只是一个具有简单含义的术语。

`BogoMIPS` 是 Linux 的发明（是的，就是启动 Linux 的那位 Linus Torvalds），意思是虚假的 MIPS。您可能知道，`MIPS` 是“百万条指令/秒”的缩写，用于衡量计算机运行程序的速度。不幸的是，`MIPS` 并不是性能的良好衡量标准；不同类型计算机的 `MIPS` 测量值很难准确比较。`BogoMIPS` 基本上是一种独立于确切处理器类型的计算机速度度量方式。Linux 使用 `BogoMIPS` 数值来校准延迟循环，在该循环中，计算机持续运行一些无用指令，直到经过指定的时间。当然，像这样浪费宝贵的处理器时间的原因是等待某个缓慢的设备准备好工作。

哦... 关于 `LPJ` ——这是一个较新的术语，代表“每个 jiffy 的循环数”，是内核使用的另一种时间延迟度量。Linux 内核以 jiffies（厘秒）为增量考虑时间，jiffy 定义为等于 1 秒除以名为 `HZ` 的内核变量值的时间段。换句话说，每秒有 `HZ` 个 jiffies。

启动消息显示后，某些 Linux 发行版，如 `Fedora Core`，会切换到图形启动屏幕，显示系统启动进度的信息。当您首次启动某些 Linux 发行版（如安装后的 `Fedora Core` 和 `Xandros` 桌面操作系统）时，您会看到一个首次配置程序，引导您完成一些配置步骤，例如设置日期和时间以及添加用户账户。要完成此类首次配置步骤，您只需输入请求的信息即可。

![](img/792720823146d68f19fd50c99ebfce4b_138_0.png)



Linux 启动后，您通常会看到图形登录屏幕。对于某些活系统光盘发行版，如 Knoppix，您无需以用户身份登录即可获得桌面。在其他活系统光盘上，如 MEPIS，您必须登录。在 MEPIS 中，您可以登录为两个预定义用户之一——用户名 `demo` 密码为 `demo`，或用户名 `root` 密码为 `root`。

图 4-1 显示了我从 Knoppix 活系统光盘启动 PC 后的 Knoppix 桌面。

对于像 SUSE 这样的发行版，您可能会被自动登录。对于其他发行版，如 MEPIS，典型的图形登录屏幕看起来与图 4-2 所示的类似。

![](img/792720823146d68f19fd50c99ebfce4b_138_1.png)

图 4-1：从 Knoppix 活系统光盘启动后，您将获得 Knoppix 桌面。

![](img/792720823146d68f19fd50c99ebfce4b_139_0.png)

屏幕中央的登录窗口显示一个对话框，其中包含文本字段，你可以输入用户名和密码。

你可以使用在安装期间或安装之后定义的任意账户登录。始终存在`root`用户名，它恰好是超级用户（管理员账户）。无论是你自己安装 Linux，还是由他人为你安装，你都需要知道`root`密码。如果没有它，你就无法执行许多了解 Linux 工作原理所需的任务。

![](img/792720823146d68f19fd50c99ebfce4b_139_1.png)

在 Ubuntu 中，你只定义一个普通用户账户；Ubuntu 不会给你机会定义`root`用户账户。每当你需要执行任何需要`root`权限的任务时，你都必须使用`sudo`命令。

要以用户`spiderman`登录，请在第一个文本字段中输入`spiderman`并按 Enter 键。（开始输入前，请先将光标移至登录对话框。）然后输入`spiderman`的密码并按 Enter 键。随后你会看到初始的图形用户界面（GUI — 简读为*GOO-ee*）。你看到的具体内容取决于你对 GUI 的选择——GNOME 或 KDE。如果选择是由他人代你做出的，请不用担心——GNOME 和 KDE 都非常出色且功能全面。

## 探索 GUI 桌面

大多数 Linux 发行版都附带 GNOME 和 KDE 两个 GUI 桌面中的一个或两者。如果你安装了两者，可以逐一试用。每个发行版都有其默认的 GUI。表 4-1 列出了某些 Linux 发行版的默认 GUI 桌面。以下章节将对两个主要的 GUI 桌面——GNOME 和 KDE——进行概述。

表 4-1 某些 Linux 发行版的默认 GUI 桌面

| 发行版 | 默认 GUI 桌面 |
| :--- | :--- |
| Debian | 通常，Debian 默认安装 GNOME。但用户可以安装任何 GUI 桌面：GNOME、KDE 或 XFCE。（XFCE 是另一种适用于 UNIX 系统的 GUI 桌面。你可以在 www.xfce.org 上找到有关 XFCE 的更多信息。） |
| Fedora Core | GNOME，但用户也可以安装 KDE，并轻松在这两者之间切换。 |
| Knoppix | KDE |
| MEPIS | KDE |
| SUSE | 默认为 KDE，但用户可以在安装过程中选择安装 GNOME。 |
| Ubuntu | 默认为 GNOME，但用户可以通过 Synaptic 软件包管理器安装 KDE。 |
| Xandros | 带有增强功能的 KDE。（它被称为 Xandros 桌面。） |

### GNOME

GNOME 代表 **G**NU N**et**work O**b**ject M**o**del **E**nvironment（GNU 网络对象模型环境）（且正如你可能知道的，**G**NU 代表 **G**NU’s N**ot** **U**NIX，即“GNU 不是 UNIX”）。GNOME 是一个图形用户界面和编程环境。最新的 GNOME 版本是 2.x，简称 GNOME 2。从用户角度来看，GNOME 类似于 Microsoft Windows。在幕后，GNOME 具有许多功能，允许程序员编写能够良好协作的图形应用程序。在本章中，我只指出 GNOME GUI 的一些关键特性，而细节留给你们闲暇时自行探索。

如果你好奇，可以随时访问 www.gnome.org 上的 GNOME 主页以获取关于 GNOME 的最新信息。

如果 GNOME 是默认桌面，登录之后，你将会看到 GNOME GUI 桌面。图 4-3 展示了用户典型的初始 GNOME 桌面。

![](img/792720823146d68f19fd50c99ebfce4b_141_0.png)

**图 4-3**：登录后的初始 GNOME GUI 桌面。

通常情况下，你不应该以`root`身份登录。当你以`root`身份登录时，因为作为`root`你可以做任何事，所以可能会意外损坏系统。请始终以普通用户身份登录。当你需要以`root`身份执行任何任务时，请在终端窗口中输入 `su -` 并输入`root`密码。

GNOME 桌面的具体外观取决于*当前会话*（当时正在运行的一组应用程序）以及你的 Linux 发行版。你可以看到，如图 4-3 所示的初始 GNOME 桌面非常像 Windows 桌面，除了它有两个任务栏，一个在顶部，另一个在屏幕底部边缘。这些是*GNOME 面板*——类似于 Windows 任务栏。你可以从顶部 GNOME 面板访问各种菜单并启动应用程序，而状态信息（包括当前运行应用程序的图标）则显示在底部面板中。

你可以像在 Microsoft Windows 中那样移动和调整窗口大小。同样，就像在 Microsoft Windows 的窗口边框中一样，窗口标题栏的右侧包含三个按钮。最左边的按钮将窗口最小化为图标，中间的按钮将窗口最大化以填满整个屏幕，最右边的按钮关闭窗口。

#### GNOME 面板

注意图 4-3 中所示 GNOME 桌面顶部和底部边缘的两条栏。这些是 GNOME 面板，或简称为面板。顶部面板用于启动程序，而底部面板用于状态信息（当前运行应用程序的图标以及用于在桌面之间切换的按钮）。顶部面板还提供用于放置小组件的小显示区域。每个面板小组件都是设计用于在面板内运行的小型程序。例如，位于顶部面板最右侧的时钟小组件显示当前日期和时间。

GNOME 的顶部和底部面板除了时钟小组件外，还包含其他几个小组件。（具体细节取决于你的 Linux 发行版。）

- **启动器小组件：** 顶部面板上位于“应用程序”、“位置”和“系统”菜单按钮右侧的按钮是启动器小组件。这些小组件中的每一个都显示带有应用程序图标的按钮。点击按钮即可启动（启动）该应用程序。尝试点击这些按钮，看看会发生什么。鼠标和地球按钮启动 Mozilla Firefox Web 浏览器，而点击钢笔和纸张图标则打开 OpenOffice.org Writer 文字处理器。将鼠标悬停在按钮上，会出现一条包含该按钮信息的小型帮助消息。

- **GNOME 分页器小组件：** 位于底部面板的右边缘，此小组件提供一个比系统屏幕物理尺寸更大的虚拟桌面。分页器在一个小显示区域内显示四个页面。每个页面代表与显示屏幕大小相等的区域。要前往特定页面，请在分页器窗口中点击该页面。GNOME 分页器小组件会为当前虚拟页面中显示的每个窗口显示按钮。

- **GNOME 天气小组件：** 显示当地天气。直到你启动它之前，你看不到这个小组件。你可以通过右键点击顶部面板的空闲区域并从弹出的菜单中选择“添加到面板”来启动它。

#### GNOME 菜单按钮

在图 4-4 中，顶部面板的左侧以三个菜单按钮开始——应用程序、位置和系统。（在其他发行版的 GNOME 桌面上，这三个菜单按钮可能名称不同。）应用程序按钮（我有时将其称为主菜单按钮）类似于 Microsoft Windows 中的“开始”按钮。你可以从点击应用程序按钮左键时弹出的菜单中启动应用程序。通常，此菜单列出了用于启动应用程序的项目。大多数菜单项都有一个箭头；当鼠标指针悬停在带有箭头的项上时，会出现另一个弹出菜单。图 4-4 展示了 Fedora Core 系统上典型的 GNOME 应用程序菜单视图。

![](img/792720823146d68f19fd50c99ebfce4b_143_0.png)

**图 4-4**：点击菜单按钮并移动鼠标指针从一个菜单移动到另一个菜单，以找到你要启动的程序。

在图 4-4 中，菜单选择为 应用程序 > Internet > Firefox Web 浏览器。请注意，当你指向某个菜单选择时，会弹出一个包含该选择信息的气泡帮助框。

另外两个 GNOME 菜单——位置和系统——使你可以执行以下类别的相关任务：

- **位置** 菜单包含打开主文件夹、查看桌面、浏览计算机、连接到各种服务器（如 FTP 和 Windows 共享）以及搜索文件的选项。



- **系统** 菜单用于编辑桌面首选项、配置系统设置、获取在线帮助、锁定屏幕以及注销。`System > Administration`（系统 > 管理）允许你启动 GUI 系统配置实用程序，以配置用户账户、`root` 密码、安全级别、显示、网络、打印机以及日期和时间等事项。要配置各种 Internet 服务器——Web、FTP、DNS、Samba 等——请前往 `System > Administration > Server Settings`（系统 > 管理 > 服务器设置）。

你可以通过“添加到面板”对话框（见图 4-5）启动小组件，例如天气小组件。该对话框在你右键点击顶部 GNOME 面板并从弹出的菜单中选择“添加到面板”时出现。例如，你可以在“添加到面板”对话框中选择天气小组件，从而添加它

点击“添加”按钮。在“添加到面板”对话框中，你可以发现更多可尝试的小部件类别。

![](img/792720823146d68f19fd50c99ebfce4b_144_0.png)

探索 GNOME 菜单中的所有项，以查看可以从此菜单执行的所有任务。特别是，将鼠标指针悬停在“系统 ▶ 首选项”项上，以查看更改桌面外观的选项。例如，你可以从此菜单更改桌面背景，如图 4-6 所示。

## 自定义 GNOME 桌面

到现在为止，你可能已经迫不及待地想进行一些装饰了。没人喜欢一直使用朴素的 GNOME 桌面。毕竟，这是你的桌面。你可以按任何你想要的方式设置它。你可以通过选择“系统 ▶ 首选项”并从各种选项中进行选择来配置 GNOME 桌面外观和行为——即外观和感觉——的各个方面。

要查看 Fedora Core 中桌面装饰是如何工作的，请先选择“系统 ▶ 首选项 ▶ 桌面背景”；此时会弹出一个对话框，如图 4-7 所示。

在此对话框中，你可以选择纯色、颜色渐变或*壁纸*（用作背景的图片）作为背景。颜色渐变背景从一种颜色开始，逐渐变为另一种颜色。渐变可以是垂直方向（从上到下）或水平方向（从左到右）。

### 探索 GUI 桌面

![](img/792720823146d68f19fd50c99ebfce4b_145_0.png)

**图 4-6：** 自定义 GNOME 桌面的选项。

![](img/792720823146d68f19fd50c99ebfce4b_145_1.png)

**图 4-7：** 在 Fedora Core 中更改 GNOME 桌面背景。

要选择水平颜色渐变，请遵循以下步骤：

1. **在“桌面颜色”下拉列表中（参见图 4-7），选择“水平渐变”选项。**

2. **单击下拉列表旁边的“左侧颜色”按钮。**

此时会出现一个颜色选择对话框（如图 4-8 所示）。

![](img/792720823146d68f19fd50c99ebfce4b_146_0.png)

图 4-8：

颜色选择对话框。

3. **选择一种颜色并单击“确定”。**

4. **重复相同的过程来选择右侧颜色。**

完成这些步骤后，桌面将显示新的背景颜色。

如果想使用图像作为壁纸，请单击“桌面背景首选项”对话框中间的“添加壁纸”按钮。此时会出现“添加壁纸”对话框，你可以从中选择要用作壁纸的图像。通过单击“添加壁纸”对话框中的文件夹名称，进入 `/usr/share/backgrounds/images` 目录。该目录中有 `default.png` 文件，这是你在 GNOME 桌面上看到的默认壁纸。要更改壁纸，请选择你想要的图像。你可以选择任何联合图像专家组（JPEG）或便携式网络图形（PNG）格式的图像文件作为壁纸。选择图像后，单击“确定”。

新壁纸立即出现在桌面上。完成更改后，单击“关闭”按钮（参见图 4-7）以关闭对话框并应用更改。

## 注销 GNOME

要在 Fedora Core 中从 GNOME 注销，请选择“系统 > 注销”。当对话框询问你是否确实要注销时，单击“确定”。在其他发行版的 GNOME 桌面中，你通常会在顶部面板从左数第二个或第三个菜单按钮中找到注销的菜单选项。

## KDE

KDE 是 K 桌面环境（K Desktop Environment）的缩写。KDE 项目始于 1996 年 10 月，旨在为使用 X 窗口系统的 UNIX 系统开发通用的 GUI。KDE 的第一个测试版于一年后的 1997 年 10 月发布。KDE 1.0 版于 1998 年 7 月发布；KDE 2.0 版于 2000 年 10 月 23 日发布；KDE 3.0 版于 2002 年 4 月 3 日发布；最新版本——KDE 3.4——于 2005 年 3 月 16 日发布。

从用户的角度来看，KDE 提供了一个图形桌面环境，包括窗口管理器、Konqueror Web 浏览器和文件管理器、用于启动应用程序的面板、帮助系统、配置工具以及许多应用程序，包括 OpenOffice.org 办公套件、图像查看器、PostScript 查看器以及邮件和新闻程序。

对于开发人员来说，KDE 提供了用于在 C++ 中进行轻松应用程序开发的类库和对象模型。KDE 是一个拥有许多合作者的大型开发项目。

你可以通过访问 www.kde.org 上的 KDE 主页随时获取有关 KDE 的最新信息。

如果你的 Linux 系统默认 GUI 是 KDE，那么你一登录就会看到 KDE GUI。通常，你会看到一个初始 KDE 桌面，类似于图 4-9 中所示的桌面——在此例中，是 SUSE Linux 的 KDE 桌面。

你会发现 KDE 非常容易使用，并且在很多方面类似于 Windows GUI。你可以从一个类似于 Windows 中“开始”菜单的菜单启动应用程序。与在 Windows 中一样，你可以将文件夹和应用程序直接放在 KDE 桌面上。

## KDE 面板

出现在屏幕底部边缘的 KDE 面板旨在用于启动应用程序。面板中最重要的组件是位于面板最左侧的“主菜单”按钮。该按钮类似于 Windows 中的“开始”按钮。当你单击“主菜单”按钮时，会出现一个菜单。从这个菜单中，你可以通过将鼠标指针悬停在显示右指箭头的项上来访问其他菜单。例如，图 4-10 显示了配置各种服务的典型菜单选择。

你可以从这个菜单启动应用程序。这就是为什么 KDE 文档将“主菜单”按钮称为*应用程序启动器*。

在“主菜单”按钮旁边，面板还包括更多按钮。如果你不知道某个按钮的作用，只需将鼠标指针悬停在该按钮上；一个小弹出窗口会显示关于该按钮的简短消息。

![](img/792720823146d68f19fd50c99ebfce4b_148_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_148_1.png)

图 4-9：

典型用户的初始 KDE

桌面。

图 4-10：

单击“主菜单”

按钮，然后将鼠标

指针从一个菜单移到

另一个菜单以打开 KDE 菜单。

# 第一卷

第 4 章

尝试 Linux

## 自定义 KDE 桌面

KDE 使得自定义 KDE 桌面的外观和感觉变得容易。你需要装饰桌面的所有内容都在同一个地方：KDE 控制中心。要启动 KDE 控制中心，请选择“主菜单 → 控制中心”。

KDE 控制中心启动后，它会显示主窗口，左侧列出一系列项目，右侧工作区显示有关你系统的一些摘要信息，如图 4-11 所示。

![](img/792720823146d68f19fd50c99ebfce4b_149_0.png)

KDE 控制中心的左侧显示你可以使用此程序自定义的项目。该列表按类别组织，例如“外观与主题”、“桌面”、“互联网与网络”、“KDE 组件”、“外设”、“安全与隐私”、“声音与多媒体”、“系统管理”等。单击一项以查看该项目的子类别。单击其中一个子类别项以更改它。该项目的配置选项随后出现在控制中心窗口的右侧。

要更改桌面背景，请单击“外观与主题”，然后单击“背景”。控制中心的右侧（见图 4-12）显示了自定义桌面背景的选项。

如果你想更改特定桌面的背景，请单击“桌面设置”下拉列表。从桌面列表中，你可以选择要更改哪个桌面背景。

![](img/792720823146d68f19fd50c99ebfce4b_150_0.png)

**图 4-12：** 使用 KDE 控制中心更改桌面背景。

对于彩色背景，请选择“无图片”单选按钮。从“颜色”下拉列表中，你可以选择单色背景或各种颜色渐变（意味着颜色从一种颜色逐渐变为另一种颜色）或用作背景的花纹。然后你可以单击“颜色”下拉列表下方出现的颜色按钮来选择颜色。完成选择后，单击“应用”以尝试该背景。（如果你不喜欢结果，请单击“重置”以恢复到以前的背景。）

如果你想使用图片作为背景，请选择“图片”单选按钮，并单击该单选按钮旁边的下拉菜单右侧的文件夹图标。此时会出现一个对话框，显示 `/usr/share/wallpapers` 目录中的 JPEG 图像。你可以选择其中任意一张图片，或者从另一个目录选择一张图片并单击“确定”。然后单击 KDE 控制中心中的“应用”按钮将此壁纸应用到桌面。如果你不喜欢外观，请单击“重置”。

## 注销 KDE

当你完成对 KDE 的探索后，请注销。要从 KDE 注销，请选择“主菜单 \ 注销”。你也可以右键单击桌面的空白区域，然后从出现的上下文菜单中选择“注销”。



## 与 Shell 打交道

Linux 本质上就是 UNIX，而 UNIX 如果你不能在文本终端中输入晦涩的命令，就不像 UNIX。虽然 GNOME 和 KDE

## 130 关闭系统

我们已深入窗口、图标、鼠标和指针的世界——人们亲切地称之为 `WIMP` :-）——但有时你可能不得不面对一个只有普通文本屏幕和提示符的环境，其外观可能如下所示（当你以 `naba` 身份登录时）：

```
naba@linux:/etc>
```

你通常在 X Window System 出现问题时会看到文本屏幕，该系统本质上是运行你日常所见窗口和菜单的机制。在这种情况下，你需要使用 `Shell`（Shell）并掌握一些晦涩的 Linux 命令。

为了应对与 Shell 的意外遭遇，你可以在处于 GNOME 或 KDE 图形界面时，在终端窗口中尝试一些 Linux 命令进行练习。一旦你掌握了窍门，甚至可能保持一个终端窗口打开，以便随时使用那些晦涩的命令——因为点击操作往往更快。这些两字母命令确实威力不小！

### 启动 bash shell

简而言之，Shell 是 Linux 的 `命令解释器`——它读取你输入的内容，将该文本解释为命令，并执行命令所要求的功能。

在开始玩弄 Shell 之前，请打开一个终端窗口。在 GNOME 或 KDE 中，面板通常包含一个看起来像监视器的图标。点击该图标后，会出现一个带有提示符的窗口，如图 4-13 所示。这就是终端窗口，它的工作方式与传统的终端完全一样。一个 Shell 程序正在运行，并准备接收你输入的任何文本。你输入文本，按下 Enter 键，然后会发生某些事情（取决于你输入的内容）。

![](img/792720823146d68f19fd50c99ebfce4b_151_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_151_1.png)

![](img/792720823146d68f19fd50c99ebfce4b_152_0.png)

如果你的桌面 GNOME 或 KDE 面板上没有启动终端或 Shell 窗口的图标，请浏览主菜单层次结构，你应该能找到标有 Console（控制台）或 Terminal（终端）的项目。选择该项目应会打开一个终端窗口。

你看到的提示符取决于在该终端窗口中运行的 Shell。默认的 Linux Shell 称为 `bash`。

`bash` 可以理解大量标准的 Linux 命令，你可以使用这些命令查看文件、在一个目录和另一个目录之间切换、查看正在运行的程序（以及谁还登录了系统），等等。

除了 Linux 命令之外，`bash` 还可以运行存储在可执行文件中的任何程序。`bash` 还可以执行 `Shell 脚本`——包含 Linux 命令的文本文件。

### 理解 Shell 命令

由于 Shell 会解释你输入的内容，了解 Shell 如何解析你输入的文本至关重要。所有 Shell 命令都具有以下通用格式：

```
command option1 option2 … optionN
```

这样的一行命令通常称为 `命令行`。在命令行中，你输入一个命令，后跟一个或多个可选参数（或 `参数`）。这些命令行选项（或命令行参数）有助于你指定命令要执行的操作。

一条基本规则是，你必须使用空格或 Tab 键将命令与选项分开。你还必须用空格或 Tab 键分隔选项。如果你要使用的选项包含嵌入的空格，则必须将该选项放在引号内。例如，要在 `password` 文件中搜索两个单词的文本，我输入以下 `grep` 命令。（`grep` 是那些用于在文件中搜索文本的晦涩命令之一。）

```
grep “WWW daemon” /etc/passwd
```

当 `grep` 打印包含这些单词的行时，看起来像这样。（你在系统上看到的内容可能与展示的有所不同。）

```
wwwrun:x:30:8:WWW daemon apache:/var/lib/wwwrun:/bin/false
```

如果你创建了一个以你名字命名的用户账户，请继续输入 `grep` 命令，将你的名字作为参数，但记得将名字放在引号内。

## 尝试几个 Linux 命令

在终端窗口打开期间，试着玩几个 Linux 命令，纯粹为了娱乐。我引导你通过一些随机示例，让你感受一下在 Shell 提示符下你能做什么。

要查看自上次开机以来 Linux PC 已运行了多长时间，请键入以下内容。（`注意`：我用粗体显示键入的命令，随后显示该命令的输出。）

```
uptime
12:06:34 up 59 days, 16:23, 4 users, load average: 0.56, 0.55, 0.37
```

部分 `up 59 days, 16:23` 告诉你这台特定的 PC 已经运行了将近两个月。嗯……Windows 能做到这一点吗？

要查看你的系统正在运行哪个版本的 Linux 内核，请使用如下所示的 `uname` 命令：

```
uname -srv
```

这以三个选项运行 `uname` 命令：`-s`、`-r` 和 `-v`（在本例中显示可以组合为 `-srv`）。`-s` 选项使 `uname` 打印内核名称，`-r` 打印内核发行号，而 `-v` 打印内核版本号。该命令在其中一个 Linux 系统上生成以下输出：

```
Linux 2.6.14-1.1696_PCS #1 Sat Nov 19 19:02:13 EST 2005
```

在这种情况下，系统正在运行 Linux 内核版本 2.6.14。

要读取文件，请使用 `more` 命令。例如，键入 `more /etc/passwd` 以读取 `/etc/passwd` 文件。结果输出类似于以下内容：

```
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/bin/bash
daemon:x:2:2:Daemon:/sbin:/bin/bash
lp:x:4:7:Printing daemon:/var/spool/lpd:/bin/bash
mail:x:8:12:Mailer daemon:/var/spool/mqueue:/bin/false
news:x:9:13:News system:/etc/news:/bin/bash
uucp:x:10:14:Unix-to-Unix Copy system:/etc/uucp:/bin/bash
... lines deleted ...
```

## 关闭系统

要查看当前在系统上运行的所有程序列表，请使用 `ps` 命令，如下所示：

```
ps ax
```

`ps` 命令接受许多选项，你可以提供这些选项而不带通常的破折号前缀。此示例使用 `a` 和 `x` 选项。`a` 选项列出你正在运行的所有进程，`x` 选项显示其余的进程。净结果是 `ps ax` 打印出系统上运行的所有进程列表，如下所示的 `ps ax` 命令示例输出：

```
     PID TTY          STAT      TIME COMMAND
       1 ?        S       0:01 init  [5]
       2 ?        SN      0:00 [ksoftirqd/0]
       3 ?        S<      0:00 [events/0]
       4 ?        S<      0:00 [khelper]
       9 ?        S<      0:00 [kthread]
      22 ?        S<      0:00 [kblockd/0]
      58 ?        S       0:00 [kapmd]
      79 ?        S       0:00 [pdflush]
      80 ?        S       0:00 [pdflush]
      82 ?        S<      0:00 [aio/0]
    ... lines deleted ...
     5525 ?        Ss      0:00 /opt/kde3/bin/kdm
     5502 ?        S      0:12 /usr/X11R6/bin/X  -br  -nolisten
         tcp  :0 vt7  -auth  /var/lib/xadm/authdir/authfiles/A:0-pIA0rt
     5503 ?        S       0:00 --:0
     6187 ?        Ss     0:00 /sbin/portmap
     6358 ?        Ss     0:00 /usr/share/applications/kde
     6556 ?        Ss     0:00 /usr/sbin/cupsd
     6577 ?        Ssl    0:00 /usr/sbin/nsd
    ... lines deleted ...
```



即使只有一个用户登录，系统中运行的程序之多令人惊叹，不是吗？

你可以猜到，你可以从 Shell 提示符做任何事情，但这需要一些时间才能习惯。

### 关闭系统

当你准备关闭 Linux 时，必须以有序的方式执行。即使你是 Linux PC 的唯一用户，通常也有几个其他程序在后台运行。此外，像 Linux 这样的操作系统试图优化将数据写入硬盘的方式。由于硬盘访问相对较慢（与访问内存位置所需的时间相比），数据通常保持在内存中，并以大块形式写入硬盘。因此，如果你只是关掉电源，就有风险某些文件未正确更新。

任何用户（你甚至无需登录）都可以从桌面或图形登录界面关闭系统，尽管某些发行版（如 Debian）会提示你输入 `root` 密码。选择主菜单 → `Log Out`（注销）（或在菜单中寻找 `Log Out` 选项）。将出现一个“注销”对话框，提供重新启动或停止系统，或简单注销的选项。要关闭系统，只需选择“`Shutdown`（关机）”并点击“`OK`（确定）”。然后系统将以有序的方式关闭。

如果注销菜单中没有关闭系统的选项，请先注销，然后从图形登录界面选择“`Shutdown`（关机）”。

当系统关闭时，你会看到关于进程停止的信息。你可能会惊讶地发现，即使没有人明确在系统上运行任何程序，系统上有多少个进程。如果你的系统不会在关机时自动断电，你可以手动关闭电源。

![](img/792720823146d68f19fd50c99ebfce4b_155_0.png)

请注意，关闭或重启系统可能不需要 `root` 访问权限。这就是为什么确保物理访问控制台得到充分保护非常重要，这样任何想这样做的人就不能随意走到控制台前关闭你的系统。

# 第二卷

# Linux 桌面

# 第五波

作者：Rich Tennant

![](img/792720823146d68f19fd50c99ebfce4b_156_0.png)

没错，起初听起来很棒——一个直观的网络适配器，通过帮助用户完成他们的想法来协助撰写备忘录。

## 目录概览

- 第 1 章：介绍图形用户界面（GUI）桌面 .........133
- 第 2 章：掌控 Shell .........161
- 第 3 章：浏览 Linux 文件系统....181
- 第 4 章：介绍 Linux 应用程序 .........207
- 第 5 章：使用文本编辑器 .........239

# 第 1 章：介绍图形用户界面（GUI）桌面

### 本章内容

- 发现 GNOME 和 KDE 图形界面的常见功能
- 介绍 Debian 的 GNOME 桌面
- 介绍 Fedora Core 的 GNOME 桌面
- 介绍 Knoppix 桌面
- 介绍 MEPIS 桌面
- 介绍 SUSE 桌面
- 介绍 Ubuntu 的 GNOME 桌面
- 介绍 Xandros 桌面

Linux 发行版通常附带两种流行的图形用户界面（GUI）之一——`GNOME` 和 `KDE`。`GNOME` 和 `KDE` 与 Microsoft Windows 相似，但在一个方面是独特的。与 Microsoft Windows 不同，在 Linux 中你可以选择自己的 GUI。如果你不喜欢 `GNOME`，只需注销然后以 `KDE`（另一种 GUI）重新登录即可。试试在 Microsoft Windows 上这样做！

> `GNOME` 和 `KDE` 是独立于 Linux 开发的。事实上，`GNOME` 和 `KDE` 可以在除 Linux 以外的其他 UNIX 操作系统上运行。你还有选择安装其他 GUI，例如 `FVWM` 和 `Xfce`。访问 `www.freedesktop.org/wiki/Desktops` 查看其他 X 桌面（运行在 X 窗口系统上的桌面）列表。

本章探讨了 `GNOME` 和 `KDE` 的主要功能。你可以通过开始使用它们来最好地了解这些 GUI。

每个 Linux 发行版通常默认安装其中一种 GUI。在 Debian、Fedora Core 和 Ubuntu 中，默认 GUI 是 `GNOME`；在 Knoppix、MEPIS、SUSE 和 Xandros 中，默认是 `KDE`。在 Debian 中，你可以安装 `GNOME` 或 `KDE`。每个发行版还会定制 `GNOME` 或 `KDE`，以创建该发行版独特的桌面。因此，我还提供了每个发行版桌面的概述——`GNOME` 与 Debian、Fedora Core 和 Ubuntu；`KDE` 与 Knoppix、MEPIS、SUSE 和 Xandros。请将此视为简要介绍。你必须自行探索桌面，因为这是熟悉 GUI 的最佳方式。

### 了解 GUI 的常见功能

从用户角度来看，`GNOME` 和 `KDE` 可能看起来相似，因为许多功能运作方式类似。熟悉这些常见功能，这样无论你选择使用哪种 GUI 进行日常工作，都可以依赖它们。

最重要的是，无论你决定使用哪种 GUI，所有的 GUI 应用程序——无论是基于 `GNOME` 还是 `KDE`——都可以在所有 GUI 桌面上运行。换句话说，你可以在 `GNOME` 下运行 `KDE` 应用程序，反之亦然。唯一的障碍是，有时 `GNOME` 和 `KDE` 应用程序可能未默认安装。

首先，`GNOME` 和 `KDE` 的初始桌面看起来与其他流行的 GUI（如 Microsoft Windows 或 Mac OS X 桌面）类似。例如，图 1-1 和图 1-2 分别展示了典型的 `GNOME` 和 `KDE` 桌面。

![](img/792720823146d68f19fd50c99ebfce4b_159_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_160_0.png)

这两个桌面（图 1-1 和 1-2）最初显示计算机图标、主文件夹图标以及用于删除文件的回收站图标。`GNOME` 和 `KDE` 桌面的另一个主要功能是*面板*——`KDE` 中位于底部的条以及 `GNOME` 中位于顶部和底部的条。每个面板类似于 Windows 任务栏。左侧有按钮（通往各种程序的快捷方式），右侧有时间显示。面板的中部显示你已启动（或自动为你启动）的应用程序的按钮。

将鼠标悬停在面板上的任何图标上时，一个小弹出窗口会显示该图标的名称。弹出窗口还会提供关于你可以对该图标执行哪些操作的提示。

### 桌面上下文菜单

`GNOME` 和 `KDE` 桌面在你在桌面空白区域右键单击时都会显示上下文菜单。该菜单的具体内容取决于桌面，但它通常提供菜单选项，使你可以执行以下类型的任务：

- 运行命令。
- 打开终端窗口，你可以在其中输入 Linux 命令。
- 创建新文件夹。
- 配置桌面背景。
- 重新排列桌面上的图标。

例如，图 1-3 和图 1-4 分别展示了典型 `GNOME` 和 `KDE` 桌面上的桌面上下文菜单。带有指向右侧箭头的桌面菜单选项包含其他菜单，当你将鼠标指针悬停在箭头上时这些菜单会出现。

![](img/792720823146d68f19fd50c99ebfce4b_161_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_161_1.png)

### 图标上下文菜单

在 `GNOME` 或 `KDE` 中右键单击任何桌面图标都会导致另一个菜单出现。（见图 1-5 和 1-6。）无论点击什么图标，此上下文菜单中的许多项目都是相同的，但右键单击某些图标（例如回收站图标）会产生略有不同的菜单。你可以从图标上下文菜单执行以下典型任务：

- 在文件管理器中打开文件夹。
- 用你选择的应用程序打开文件。
- 重命名图标。
- 将图标移动到回收站。
- 查看该图标的属性。

![](img/792720823146d68f19fd50c99ebfce4b_162_0.png)

#### 图 1-5：GNOME 中的图标上下文菜单

对于回收站图标，图标上下文菜单通常提供一个选项，用于永久删除回收站中的项目。（你会有一次机会选择“是”或“否”。）

![](img/792720823146d68f19fd50c99ebfce4b_162_1.png)

#### 图 1-6：KDE 中的图标上下文菜单

我猜你在这里看到了一个规律。就是右键单击。无论你在 GUI 桌面的哪个位置，总是先右键单击再选择。当你右键单击时，你一定会找到一些有用的东西！

### 面板

面板是横跨桌面顶部或底部的长条。在 `GNOME` 中，有两个面板。图 1-7 和图 1-8 分别展示了 `GNOME` 顶部面板和单个 `KDE` 面板的典型视图。

![](img/792720823146d68f19fd50c99ebfce4b_163_0.png)

#### 图 1-7：GNOME 顶部面板的典型视图

面板是图标的停放处。点击某些图标会启动程序。有些图标显示状态（例如当前正在运行的程序），以及诸如日期和时间等信息。

![](img/792720823146d68f19fd50c99ebfce4b_163_1.png)

#### 图 1-8：KDE 面板的典型视图

从左侧开始，第一个图标（无论它显示什么）是主菜单按钮——它类似于 Microsoft Windows 中的“开始”按钮。然后是几个用于启动各种程序的图标。

![](img/792720823146d68f19fd50c99ebfce4b_163_2.png)



顺便说一下，如果你将鼠标指针移到图标上方，一个帮助气球会弹出，并为你提供关于该图标的有用提示。

在 KDE 面板中，最左侧的一组图标右边，有一个工作区切换器图标，显示四个矩形区域，每个代表一个虚拟桌面。该图标也被分别称为工作区切换器、桌面翻页器或简单地称为翻页器。你可以点击这些矩形之一来切换到不同的虚拟桌面。这个功能就像拥有四个独立的虚拟桌面供你使用。老实说，我最终只使用一个桌面，但我喜欢知道其他桌面在那里，以防我需要。另一方面，如果你正在编写代码并为新程序准备用户指南，你可以用一个桌面进行所有编码工作，用第二个桌面编写用户指南。当然，你可以通过单击鼠标从一个桌面切换到另一个桌面。

桌面翻页器图标右侧的区域显示你迄今为止已启动的程序的按钮。如果你尚未启动任何程序，该区域为空白。

其他图标可能位于任务管理器旁边，但日期和时间始终显示在面板的最右边缘。

![](img/792720823146d68f19fd50c99ebfce4b_164_0.png)

接下来，我们来了解一下面板上这些图标的技术细节。面板本身是一个独立的应用程序；每个图标都是一个按钮或一个被称为`小程序`（applet）的程序。这些小程序是小应用程序（也称为`插件`）。这些面板小程序可以执行各种功能，例如启动其他程序或显示日期和时间。在运行小程序之前，你必须将其添加到面板中。右键单击面板的空白区域，并选择适当的菜单项以将小程序添加到面板。添加小程序后，你可以右键单击该小程序的图标进行配置或执行该小程序支持的某些任务。

如果你右键单击任何图标——或者右键单击面板上的任何位置——你会看到一个上下文菜单，允许你执行与该图标相关的操作（例如移动它或完全删除它）。你还可以设置一些首选项，并向面板添加更多按钮和小程序。

## 主菜单

GNOME 顶部面板和 KDE 唯一面板的最左侧图标是`主菜单`按钮。通常，你可以在这里找到所有应用程序，它们被组织到子菜单中。在本节中，我将提供一些主菜单的示例，并指出一些有趣的项目。然后你可以自行进行进一步探索。

在 GNOME 桌面上，顶部面板最左侧的菜单按钮通常标记为`应用程序`，并且顶部面板还有一个或多个额外的菜单按钮，例如 Fedora Core 的 GNOME 桌面中的`位置`和`桌面`。

点击主菜单按钮以打开第一级菜单。然后，鼠标悬停在任何带有箭头的菜单项上以打开下一级菜单，依此类推。你可以遍历菜单层次结构并从最终菜单中进行选择。图 1-9 和图 1-10 分别显示了典型 GNOME 和 KDE 桌面中的主菜单层次结构。

![](img/792720823146d68f19fd50c99ebfce4b_164_1.png)

关于我如何引用菜单选择，有一点说明：我使用 `Main Menu⇒System⇒Desktop Applet⇒OpenOffice.Org Quicks tar ter` 这种符号表示法来指代图 1-10 中显示的菜单选择。类似地，我说选择 `Applications⇒Internet⇒Firefox Web Browser` 来指代图 1-9 中高亮的菜单序列。大家应该明白了其中的意思。

140 了解 GUI 的常见功能

图 1-9：典型 GNOME 桌面上的主菜单层次结构。

![](img/792720823146d68f19fd50c99ebfce4b_165_0.png)

图 1-10：典型 KDE 桌面上的主菜单层次结构。

![](img/792720823146d68f19fd50c99ebfce4b_165_1.png)

在大多数桌面中，顶级主菜单包含以下类型的菜单类别：

- **附件** 或 **实用工具**：大量的实用程序，例如科学计算器、字符选择器、软盘格式化程序、词典、Palm Pilot 或 Handspring 同步等。
- **游戏**：菜单中有什么呢？游戏（而且数量众多——纸牌游戏、麻将、扫雷、黑白棋等等）
- **图形**：诸如 GIMP（类似于 Adobe Photoshop 的程序）、数码相机界面、扫描仪界面、屏幕截图程序以及 Adobe Acrobat 查看器等程序
- **互联网**：互联网应用程序，例如 Web 浏览器、电子邮件阅读器和即时通讯工具
- **办公**：办公应用程序，例如 OpenOffice.org 办公套件（包括 Writer 文字处理器、Calc 电子表格、Impress 幻灯片演示程序、Draw 绘图程序，以及更多内容）
- **首选项** 或 **设置**：用于配置系统许多方面的选项，包括桌面的外观和行为
- **多媒体** 或 **声音与视频**：多媒体应用程序，例如 CD 播放器、混音器、录音机和音量控制
- **系统**：用于配置你的 Linux 系统的系统管理工具

主菜单通常还包括一些用于常见任务的菜单项，例如以下项目：

- **主菜单·帮助**：显示在线帮助。
- **主菜单·运行命令**：显示一个对话框框，你可以在其中输入程序名称，然后点击“运行”以启动该程序。
- **主菜单·搜索文件（或查找文件）**：运行一个搜索工具，你可以用它来搜索文件。
- **主菜单·锁定屏幕**：启动屏幕保护程序并锁定屏幕。当你想要返回桌面时，系统会提示你输入密码。
- **主菜单·注销**：注销当前用户。（你会有一次机会确认是否真的想要注销。）

每个发行版的主菜单类别不同，但菜单组织方式足够相似，你通常可以找到所需内容。

好了。这就是关于主菜单我要告诉你的全部内容。当你使用 GNOME 或 KDE 桌面时，你会大量使用主菜单。即使起初看起来信息量太大，随着你在 Linux 上花费更多时间，这一切都会变得非常熟悉。

在下面的章节中，我将概述特定桌面：

Debian 的 GNOME 桌面，Fedora Core 的 GNOME 桌面，Knoppix 桌面，

MEPIS 的 KDE 桌面，SUSE 桌面，Ubuntu 的 GNOME 桌面，以及 Xandros

桌面。

## 介绍 Debian 的 GNOME 桌面

Debian 的默认 GNOME 桌面外观简洁（见图 1-11），桌面上只有三个图标——一个计算机图标、你的主文件夹和回收站图标。

在图 1-11 中，请注意 Debian 的 GNOME 桌面上的主要项目，以及点击每个项目时会发生什么：

- **桌面图标**：计算机图标在 Nautilus 文件管理器中打开你的计算机以供浏览。主文件夹图标在 Nautilus 文件管理器中打开你的主文件夹（有关使用 Nautilus 浏览文件夹的更多信息，请参见本文的小书第 3 章）。
- **回收站（或垃圾桶）图标**：代表一个存储已删除项的地方，直到你清空回收站。
- **应用程序菜单（主菜单）**：打开主菜单，你可以从中选择要运行的应用程序。
- **操作菜单**：提供菜单选项以运行应用程序、搜索文件、截图、锁定屏幕和注销。
- **Nautilus 文件浏览器**：在文件浏览模式下，在 Nautilus 文件管理器中打开你的主文件夹（有关使用 Nautilus 浏览文件系统的解释，请参见本文的小书第 3 章）。
- **终端程序**：打开一个终端窗口，你可以在其中输入 Linux 命令。
- **工作区切换器**：每个方块都会调出一个不同的桌面。这与 KDE 桌面中的桌面分页器类似。
- **显示桌面**：通过最小化所有窗口来显示桌面。
- **音量**：显示一个音量控制条，你可以通过拖动滑块来改变声音的音量。
- **窗口选择器**：显示当前打开的窗口列表，你可以点击并将该窗口置于前台，使其成为当前活动的窗口。
- **日期和时间**：显示当前日期和时间，点击会弹出一个显示当前日期的日历。

![](img/792720823146d68f19fd50c99ebfce4b_168_0.png)

点击主菜单会打开主菜单，如图 1-12 所示，它允许你访问 Debian 中的大多数应用程序。当然，各个子菜单中应用程序的具体列表取决于你安装了什么，但图 1-12 让你看到了 Debian 中典型主菜单的样子。要浏览主菜单，鼠标悬停在带有右箭头的项目上，会弹出一个包含更多项目的子菜单。

操作菜单是你可以从面板启动的另一个菜单。通过操作菜单，你可以执行其他任务，例如运行任何应用程序、搜索文件、截图和注销。

![](img/792720823146d68f19fd50c99ebfce4b_169_0.png)

图 1-12：从 Debian 的 GNOME 桌面上的主菜单启动应用程序。

要探索 Debian 的 GNOME 桌面，请尝试点击面板图标以启动应用程序。特别是，你可以点击顶部面板上的 Nautilus 文件浏览器图标，在 Nautilus 文件管理器中打开你的主文件夹。该窗口打开后，你可以探索其他文件夹以熟悉文件系统。

你还可以点击主菜单并鼠标悬停在项目上，查看所有子菜单，以了解你可以在 Debian 中运行的各种应用程序。当然，你可以点击某个项目以启动特定的应用程序并逐一尝试。

## 介绍 Fedora Core 的 GNOME 桌面

GNOME 是 Fedora Core 的默认 GUI。这意味着当你第一次在 GUI 登录屏幕登录时，你会看到如图 1-13 所示的 GNOME 桌面。桌面显示计算机、你的主文件夹和垃圾桶的图标。



以下列表涉及 GNOME 桌面的主要部分，并简要描述了每个部分的目的：

- `桌面图标`：双击计算机图标查看计算机内容，双击主文件夹图标在 Nautilus 文件管理器窗口中打开你的主文件夹。垃圾桶图标存放已删除的项目。桌面还显示其他可移动介质（如 CD 和 DVD）的图标。

![](img/792720823146d68f19fd50c99ebfce4b_170_0.png)

- `应用程序菜单（主菜单）`：调出主菜单，你可以从中选择要运行的应用程序。
- `位置菜单`：显示一个菜单，你可以从中打开主文件夹、查看桌面、浏览计算机、连接到 FTP 和 Windows 共享等服务器，以及搜索文件。
- `系统菜单`：调出一个菜单，你可以从中编辑桌面首选项、编辑系统设置、获取在线帮助、锁定屏幕以及注销。
- `系统：管理`：`服务器设置`显示一个菜单，允许你启动基于图形界面的系统配置实用程序，以配置各种互联网服务器，包括 Web、FTP、DNS、Samba 等。
- `Firefox 网络浏览器`：运行 Mozilla Firefox 网络浏览器。
- `Evolution`：启动 Evolution 电子邮件和日历软件。
- `OpenOffice.org Writer`：运行 OpenOffice.org Writer，这是一款类似 Microsoft Word 的字处理软件。
- `OpenOffice.org Impress`：运行 OpenOffice.org Impress 幻灯片演示程序（类似于 Microsoft PowerPoint）。
- `OpenOffice.org Calc`：运行 OpenOffice.org Calc，这是一款类似 Microsoft Excel 的电子表格程序。
- `显示桌面`：通过最小化所有窗口来显示桌面。
- `工作区切换器`：每个方块调出一个不同的工作区。这与 KDE 桌面中的桌面分页器具有相同功能。
- `音量`：显示一个音量控制条，你可以通过拖动滑块来改变音量。
- `日期和时间`：显示当前日期和时间，单击会调出一个显示当前日期的日历。

单击主菜单（参见图 1-13）以打开主菜单并浏览各个类别。从主菜单中，你可以访问 Fedora Core 中几乎所有应用程序和实用工具。

## 介绍 Knoppix 桌面

Knoppix 不要求你使用用户名登录。当你从 Knoppix CD 引导你的 PC 后，你会看到图 1-15 所示的初始 Knoppix 桌面。Knoppix 使用定制版本的 KDE 作为其桌面，因此你可能会发现它与其他基于 KDE 的桌面（如 MEPIS、SUSE 和 Xandros）有相似之处。特别是，MEPIS 桌面看起来与 Knoppix 桌面相似，因为 MEPIS 也包含许多相同的桌面图标和面板项目。

与某些其他发行版相比，Knoppix 拥有大量的桌面图标和面板项目。这主要是因为 Knoppix 会检测并添加所有检测到的硬盘分区、CD/DVD 驱动器以及软盘驱动器的桌面图标。

在图 1-14 中，请注意 Knoppix 桌面的以下主要组件：

- `桌面图标`：Knoppix 显示所有硬盘分区、CD/DVD 驱动器和软盘驱动器的图标。单击这些存储设备任一项即可挂载并打开它们以访问其内容。此外，还有一个回收站图标和一个指向 Knoppix 手册的快捷方式（Knoppix 启动后会在 Konqueror 窗口中打开该手册）。
- `隐藏面板`：面板的两个端点充当`隐藏面板`按钮，这意味着如果你单击其中一个，面板会滑出并消失，只留下隐藏面板按钮。再次单击，面板会重新出现。你可以隐藏面板以为其他窗口腾出更多空间。
- `主菜单（K 菜单）`：从这个主菜单（参见图 1-15）中，你可以选择要运行的应用程序、锁定屏幕、获取在线帮助或注销。
- `Knoppix 菜单`：调出一个菜单，你可以用它来执行诸如配置设备（打印机、声卡）、设置网络、开启或关闭 SSH 和 Samba 等少数服务器，以及打开一个`root` shell 窗口以便你以超级用户身份输入命令等任务。
- `窗口列表`：单击以查看当前打开的窗口列表并整理桌面上的窗口。
- `显示桌面`：通过最小化所有窗口来显示桌面。
- `主文件夹`：在 Konqueror 文件管理器中打开你的主目录。
- `终端程序`：运行`konsole`，这是一个提供终端窗口的程序，你可以在其中输入 Linux 命令。
- `Konqueror 网络浏览器`：运行 Konqueror 网络浏览器。
- `Firefox 浏览器`：运行 Firefox 网络浏览器。
- `OpenOffice`：启动 OpenOffice.org Writer，这是一款类似 Microsoft Word 的字处理软件。你可以从主菜单启动其他 OpenOffice.org 程序，如 Impress、Calc 和 Draw。
- `桌面分页器`：每个方块调出一个不同的桌面。
- `程序图标`：此区域显示当前运行程序的图标。
- `键盘布局`：单击以在多种键盘布局之间切换：美国、德国和法国。（图标上的旗帜指示键盘当前使用的是哪个国家的布局。）
- `显示配置`：单击以更改屏幕分辨率或配置显示。
- `音量`：启动 KMix 实用程序，允许你更改音量以及控制声卡的其他方面。
- `日期和时间`：显示当前日期和时间。单击以调出一个显示当前日期的日历。

## 已删除项目

Knoppix 手册链接

存储设备

带有 Knoppix 手册的 Konqueror 网络浏览器

![](img/792720823146d68f19fd50c99ebfce4b_173_0.png)

隐藏面板

K 菜单（主菜单）

Knoppix 菜单

窗口列表

主文件夹

显示桌面

终端程序

桌面分页器

OpenOffice

Firefox 网络浏览器

Konqueror 网络浏览器

程序图标

键盘布局

显示配置

日期和时间

音量

隐藏面板

图 1-15 显示了当你单击面板上的主菜单时出现的 Knoppix 主菜单。与所有桌面一样，主菜单是你访问 Knoppix 中应用程序的第一步。作为一个单 CD 发行版，Knoppix 包装了令人惊讶的大量应用程序，因此你大概可以通过查看图 1-15 主菜单中显示的应用程序类别来猜测。

![](img/792720823146d68f19fd50c99ebfce4b_174_0.png)

图 1-16 中显示的 Knoppix 菜单是你可以从面板打开的另一个重要菜单。该菜单允许你配置设备、设置网络连接、启动服务器、运行某些实用程序，以及打开一个`root shell`——一个你可以以`root`（超级用户）身份输入 Linux 命令的终端窗口。

要探索 Knoppix 的其余部分，请从单击面板图标以启动应用程序（如网络浏览器和 OpenOffice.org Writer）开始。一个好的起点是主文件夹图标，它在 Konqueror 窗口中打开你的主目录。从那个 Konqueror 窗口，你可以探索文件系统的其余部分。

![](img/792720823146d68f19fd50c99ebfce4b_175_0.png)

**图 1-16：**从 Knoppix 配置菜单中配置网络连接和设备。

![](img/792720823146d68f19fd50c99ebfce4b_175_1.png)

**提示**

若要挂载并访问 Knoppix 检测到的任何硬盘分区上的文件，只需单击桌面上的图标即可。然后，Knoppix 会挂载该分区并在 Konqueror 窗口中显示其内容。例如，在我的笔记本电脑上，我可以单击桌面上的硬盘分区 `[hda2]` 图标来访问该分区上的文件。那个分区恰好是一个包含 Windows XP 操作系统的 NTFS 分区。Knoppix 可以挂载并打开该分区，使我能够访问那些分区文件。

你还可以单击主菜单并探索 Knoppix 中大量的应用程序。

![](img/792720823146d68f19fd50c99ebfce4b_175_2.png)

**技术细节**

哦，Knoppix 在单张 CD（容量不足 700MB）上打包如此多应用程序的秘诀：Knoppix 在 CD 上以压缩格式存储文件，然后在需要时即时解压。令人印象深刻，不是吗？

## 介绍 MEPIS KDE 桌面

MEPIS 基于 Debian，并使用 KDE 作为其桌面。图 1-17 显示了初始的 MEPIS 桌面。请注意，MEPIS 桌面拥有所有存储设备的桌面图标，并包含大量面板图标以访问许多应用程序和实用工具。

如图 1-17 所示，MEPIS 桌面包括以下关键元素：

- `桌面图标`：MEPIS 显示所有硬盘分区、CD/DVD 驱动器和软盘驱动器的桌面图标。单击以打开并查看这些存储设备中任意一个的内容。桌面还显示一个用于已删除项目的回收站图标以及一个指向 MEPIS 网站的图标链接。



# 介绍 MEPIS KDE 桌面

**主菜单**：调出 MEPIS 主菜单（参见图 1-18），你可以从中执行各种任务，如启动应用程序、运行命令、获取帮助、查找文件、访问 MEPIS OS Center、启动新会话或注销。

## 图 1-17：初始的 MEIPS 桌面。

![](img/792720823146d68f19fd50c99ebfce4b_176_0.png)

- 已删除项
- 存储设备
- MEIPS 网站链接
- 主菜单
- 控制中心
- 信息中心
- KDE 系统监视器
- 终端程序
- Synaptic 包管理器
- 浏览 Windows 网络
- 文本编辑器
- 桌面切换器
- CD 和 DVD 刻录
- OpenOffice.org
- Kontact
- Konqueror Web 浏览器
- Firefox Web 浏览器
- 主目录
- 显示桌面
- MEIPS 操作系统中心
- 文件管理器
- 系统性能监视器
- 剪贴板工具
- 音量
- 天气
- 挂载 Windows 共享
- OpenOffice.org 快速入门
- 日期和时间

## 152 介绍 MEPIS KDE 桌面

![](img/792720823146d68f19fd50c99ebfce4b_177_0.png)

图 1-18：从 MEPIS 主菜单启动应用程序。

- **信息中心**：运行 KDE 信息中心，您可以在其中查看有关系统硬件设备和内存的信息。
- **KDE 系统监视器**：运行 KDE 系统监视器实用工具，您可以使用它来管理进程并监视系统性能。
- **控制中心**：启动 KDE 控制中心，您可以从中配置 KDE 桌面的各个方面。
- **终端程序**：打开一个带有 `root` 登录的终端窗口，您可以在其中输入 Linux 命令。
- **MEPIS 操作系统中心**：启动 MEPIS 操作系统中心，您可以从中访问 MEPIS 操作系统的安装和配置实用工具。您可以执行诸如修复分区和更改系统主机名等任务。
- **Synaptic 包管理器**：运行 Synaptic 包管理器——这是 Debian APT（高级包工具）的 GUI 前端，您可以使用它来安装或删除软件包。
- **文件管理器**：以 `root` 用户（超级用户）权限启动 Konqueror 文件管理器。
- **浏览 Windows 网络**：打开一个 Konqueror 文件管理器窗口，您可以从中浏览和访问 Windows 共享。
- **显示桌面**：单击可隐藏所有窗口并显示桌面。
- **主目录**：在 Konqueror 文件管理器中打开您的主目录。
- **Firefox Web 浏览器**：运行 Mozilla Firefox Web 浏览器。
- **Konqueror Web 浏览器**：运行 Konqueror Web 浏览器。
- **Kontact**：运行 Kontact 个人信息管理器。
- **文本编辑器**：运行 KWrite 文本编辑器。
- **CD/DVD 刻录**：运行 K3B CD/DVD 刻录应用程序。
- **OpenOffice.org Writer**：运行 OpenOffice.org Writer 文字处理应用程序。
- **桌面切换器**：单击每个方块以调出不同的桌面。
- **系统性能监视器**：显示当前系统性能（内存和处理器使用情况）。
- **音量**：单击以控制音量。
- **剪贴板工具**：单击以查看您已剪切的内容以及您可以粘贴到其他地方的内容。
- **OpenOffice.org 快速入门**：右键单击以新建一个 OpenOffice.org 文档。
- **挂载 Windows 共享**：单击以打开 Smb4K，该工具允许浏览和挂载 Windows 共享。
- **天气**：显示选定位置（右键单击并选择“配置 KWeather”以更改位置）的当前天气。
- **日期和时间**：显示当前日期和时间。单击可调出一个用于设置日期和时间的“时间和日期”实用工具。

MEPIS 主菜单（参见图 1-18）具有典型的 KDE 主菜单结构，将菜单项分为三大类——“最常用应用程序”显示您最近使用过的应用程序图标，“所有应用程序”包含多个用于访问应用程序的子菜单，而“操作”则显示一些常见任务的菜单，如访问打印系统、锁定屏幕、运行命令、启动新会话或注销。为了熟悉 MEPIS 作为桌面操作系统所提供的功能，请浏览 MEPIS 主菜单中“所有应用程序”类别下的菜单。

# 介绍 SUSE 桌面

SUSE Linux 是一种商业产品，它提供了一个定制化的桌面。SUSE 会自动登录您在安装期间定义的本地用户，并调出初始桌面，如图 1-19 所示。

## 154 介绍 SUSE 桌面

![](img/792720823146d68f19fd50c99ebfce4b_179_0.png)

请跟随图 1-19，我将指出 SUSE 桌面上一些较为显著的元素：

- **桌面图标**：SUSE 显示通常的桌面图标——用于浏览计算机内容的“我的电脑”图标、一个“回收站”图标、一个用于浏览本地 Windows 网络的图标，以及 Firefox Web 浏览器、打印管理器和 OpenOffice.org 办公套件的图标。
- **主菜单**：调出主菜单（见图 1-20），您可以从中启动应用程序、锁定屏幕、获取帮助、切换用户或注销。
- **主目录**：在 Konqueror 文件管理器中打开您的主目录。
- **终端程序**：运行 `Konsole`，这是一个提供终端窗口的程序，您可以在其中输入 Linux 命令。
- **SUSE 帮助中心**：启动 SUSE 帮助中心，您可以从中获取有关 SUSE Linux 各个方面的帮助。
- **Konqueror Web 浏览器**：运行 Konqueror Web 浏览器。
- **Kontact**：启动 KDE 的 Kontact 个人信息管理器。通过 Kontact，您可以阅读电子邮件、管理联系人、维护日程表、阅读 RSS 源等。
- **桌面切换器**：单击每个方块以调出不同的桌面。
- **剪贴板工具**：单击以查看已剪切的内容以及您可以粘贴到其他地方的内容。
- **电源管理工具**：右键单击以查看一个菜单，您可以使用它来启动 YaST 电源管理模块，该模块允许您编辑电源节省设置。
- **音量**：单击以控制音量。
- **SUSE 硬件工具**：单击以查看有关 PC 上设备的信息并对其进行配置。
- **SUSE 监视器**：单击以打开一个窗口，您可以使用它来检查在线更新以及启动在线更新。
- **时钟**：显示当前时间。单击可显示一个显示当前日期的日历。
- **隐藏面板**：面板的端点充当 *隐藏面板* 按钮，这意味着如果您单击此图标，面板将向右滑动并消失，只剩下端点。再次单击，面板重新出现。您可以隐藏面板以为其他窗口腾出更多空间。

除了您在 SUSE 桌面上看到的内容外，当您在面板上单击“主菜单”时，会出现许多更多选择的主菜单。见图 1-20。与 Windows 开始按钮类似，当您想要运行某个应用程序时，主菜单是您的起点。

![](img/792720823146d68f19fd50c99ebfce4b_180_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_181_0.png)

SUSE 主菜单（参见图 1-20）有三个主要类别——“最常用应用程序”显示您最近使用过的应用程序图标，“所有应用程序”组织您可以访问的应用程序，而“操作”则显示一些常见日常任务的按钮，如锁定屏幕、运行命令或注销。您应该浏览“所有应用程序”类别，以熟悉 SUSE 作为桌面操作系统所提供的功能。

# 介绍 Ubuntu 的 GNOME 桌面

Ubuntu 使用 GNOME 作为其 GUI 桌面，具有其特有的顶部和底部面板，如图 1-21 所示。与其他发行版的桌面不同，Ubuntu 不使用任何桌面图标，外观简洁。

![](img/792720823146d68f19fd50c99ebfce4b_182_0.png)

如图 1-21 所示，Ubuntu 的 GNOME 桌面具有以下主要功能：

- **应用程序菜单（主菜单）**：调出主菜单，您可以从中选择要运行的应用程序。
- **位置菜单**：显示一个菜单，您可以从中打开主目录、浏览计算机、连接到网络服务器以及搜索文件。
- **系统菜单**：调出一个菜单，您可以从中编辑各种应用程序首选项、执行系统管理任务（如通过 Ubuntu 更新管理器安装和删除软件包以及更新软件）、获取在线帮助、锁定屏幕以及注销。
- **Web 浏览器**：运行 Firefox Web 浏览器。
- **Evolution**：启动 Evolution 电子邮件和日历软件。
- **帮助**：在 Yelp（GNOME 的文档查看器）中显示在线帮助信息。
- **音量**：显示一个音量控制条，您可以通过拖动滑块来更改音量。
- **更新**：指示是否有可用的更新以安装。单击以打开一个窗口，您可以在其中查看可用更新并安装它们。请注意，当提示时，您必须输入您的普通用户密码。



- **日期和时间**：显示当前日期和时间；单击可显示一个显示当前日期的日历。
- **显示桌面**：单击可隐藏所有窗口并显示桌面。
- **工作区切换器**：每个方块调出一个不同的工作区。这与 KDE 桌面中的“桌面切换器”具有相同的功能。探索这三个菜单（应用程序、位置系统和系统），以查看您可以从这些菜单中的选择执行的任务类别。

## 158 介绍 Xandros 桌面

商业 Xandros 发行版的官方名称是 *Xandros Desktop OS*，因此 Xandros 附带一个设计良好的桌面也就不足为奇了。启动时，Xandros 会自动将您登录为用户（它使用您在安装期间定义的用户帐户），您将获得初始桌面，如图 1-22 所示。

Xandros 基于 Debian，并使用定制版本的 KDE 作为其桌面。如图 1-22 所示，您应该注意 Xandros 桌面上的以下关键元素：

- **桌面图标**：Xandros 桌面显示了一系列桌面图标：一个用于已删除项的“回收站”图标、一个用于浏览主目录的图标、代表 Xandros 技术支持和快速入门指南链接的图标、Firefox Web 浏览器的快捷方式，以及一个用于连接到 Xandros 网络的图标（这是您在 Xandros 中下载和安装更新及新应用程序的方式）。您可以双击打开这些图标。双击的结果取决于图标。例如，如果您双击 Xandros 快速入门指南，该指南将在 Firefox Web 浏览器窗口中打开。另一方面，双击“主目录”图标会在 Xandros 文件管理器中打开您的主目录。

## 160 介绍 Xandros 桌面

- **主菜单（Main Menu）**：调出主菜单（参见图 1-23），你可以从中启动应用程序、运行命令、获取帮助、切换用户或注销。
- **Firefox 网页浏览器**：运行 Mozilla Firefox 网页浏览器。
- **Thunderbird 邮件**：启动 Mozilla Thunderbird 邮件程序以访问您的电子邮件。
- **Xandros 文件管理器**：启动 Xandros 文件管理器，其布局和功能类似于 Windows 资源管理器，能够导航本地及远程文件系统。
- **帮助（Help）**：单击以打开 Xandros 桌面帮助中心窗口，在那里你可以获取有关 Xandros 和 UNIX 的一些帮助。
- **显示桌面（Show Desktop）**：单击以隐藏所有窗口并显示桌面。
- **桌面分页器（Desktop Pager）**：单击每个方块以调出不同的桌面。
- **音量（Volume）**：单击以通过拖动滑块来更改声音音量。
- **更新（Updates）**：单击以查看 Xandros 更新的状态，并打开 Xandros Networks 以执行在线更新。
- **锁定桌面（Lock Desktop）**：单击以锁定屏幕，使任何人都无法访问。（你可以通过输入密码再次访问它。）
- **注销（Logout）**：单击以注销。（你需要确认确实想要注销。）
- **时钟（Clock）**：显示当前时间。单击会调出一个时间和日期实用程序，用于设置日期和时间。
- **隐藏面板（Hide Panel）**：单击以隐藏面板。面板向右滑动并消失，只留下按钮。再次单击可查看面板。通过隐藏面板，你可以为应用程序窗口腾出更多空间。

Xandros 使用一个精简的主菜单，如图 1-23 所示，当你点击面板上的主菜单时会出现。该菜单将所有应用程序组织到一个单一的应用程序类别中。

你可以探索主菜单，以了解随 Xandros 附带的应用程序。我在本小书第 4 章中提供了这些应用程序的概述。

![](img/792720823146d68f19fd50c99ebfce4b_185_0.png)

通过点击面板上的图标来试用 Xandros 文件管理器。从 Xandros 文件管理器中，你可以浏览系统中的各种文件夹，也可以访问局域网上的任何 Windows 共享。你可以执行所有常规操作：通过拖动来移动或复制文件，并双击文件以打开它们。我发现 Xandros 文件管理器是我 Xandros 会话的一个很好的起点。

![](img/792720823146d68f19fd50c99ebfce4b_185_1.png)

# 第 2 章：指挥 Shell

## 本章内容

- 打开终端窗口和虚拟控制台
- 使用 bash shell
- 发现一些 Linux 命令
- 编写 shell 脚本

有时，事情就是不顺利。如果图形用户界面（GUI）桌面停止响应你的鼠标点击，你该怎么办？如果 GUI 根本没有启动呢？你仍然可以告诉你的 Linux 系统要做什么，但你必须通过在文本屏幕上输入命令来实现。在这些情况下，你处理的是 shell——Linux 命令解释器。在本章中，我将介绍 bash shell（大多数 Linux 发行版的默认 shell）。

一旦你弄清楚如何使用 shell，你甚至可能会开始喜欢 Linux 命令的简洁和强大。然后，即使你是一个 GUI 爱好者，很快你可能会发现自己在启动终端窗口，并用由奇怪的标点符号连接的两位数或三位数命令让系统歌唱和舞蹈。（嘿，我可以做梦，不是吗？）

### 打开终端窗口和虚拟控制台

先说首要的事情。如果你正在使用图形用户界面桌面，例如 GNOME 或 KDE，你在哪里为 shell 输入命令？好问题。

进入 shell 最简单的方法是打开一个终端（也称为控制台）窗口。大多数发行版中的 GNOME 和 KDE 图形界面包含一个图标（或主菜单选项）来打开终端窗口。点击该图标或选择菜单选项以获得终端窗口。现在，你可以随心所欲地输入命令了。

如果由于某种原因，GUI 似乎挂起了（你点击和输入但没有发生任何事情），你可以转向虚拟控制台。（物理控制台是显示器和键盘的组合。）虚拟控制台的想法是让你能够在只有一个人物理控制台的情况下，在多个文本控制台之间切换。无论你是否正在运行 GUI，你都可以使用不同的文本控制台输入不同的命令。

![](img/792720823146d68f19fd50c99ebfce4b_187_0.png)

要从 GNOME 或 KDE 桌面进入第一个虚拟控制台，请按下 `Ctrl+Alt+F1`。按 `Ctrl+Alt+F2` 进入第二个虚拟控制台，依此类推。这些虚拟控制台中的每一个都是一个文本屏幕，你可以在其中登录并输入 Linux 命令来执行各种任务。完成后，输入 `exit` 注销。

你可以使用多达六个虚拟控制台。在大多数发行版中，第七个用于 GUI 桌面。要返回 GUI 桌面，请按下 `Ctrl+Alt+F7`。

### 使用 Bash Shell

如果你使用过 MS-DOS，你可能熟悉 `COMMAND.COM`，即 DOS 命令解释器。该程序显示出了名的 `C:\>` 提示符。在 Windows 中，如果你打开命令窗口，你可以看到此提示符。（要在 Microsoft Windows 中打开命令窗口，选择“开始”>“运行”，在文本框中输入 `command`，然后点击 `OK`。）

Linux 附带一个类似于 DOS 中 `COMMAND.COM` 的命令解释器，但它能做更多的事。Linux 命令解释器被称为 *shell*。

许多 Linux 发行版的默认 shell 是 *bash*。当你打开终端窗口或在文本控制台登录时，*bash* shell 会提示你输入命令。然后，当你输入命令时，shell 会执行你的命令。顺便说一下，就像 Linux 有多个图形界面（GNOME 或 KDE）一样，除了 *bash* 之外，你还有其他 shell 可选。例如，C shell 是一些人偏好的替代 shell。你可以使用 `chsh` 命令轻松更改你的默认 shell。

除了标准的 Linux 命令，*bash* 可以执行任何计算机程序。因此，你可以在 shell 提示符下输入应用程序的名称（该名称通常比你在 GNOME 或 KDE 菜单中看到的更晦涩），然后 shell 会启动该应用程序。

#### 理解 shell 命令的语法

因为 shell 解释你输入的内容，所以了解 shell 如何处理你输入的文本是很重要的。所有的 shell 命令都具有这种通用格式，以一个命令开始，后跟选项。（有些命令没有选项。）

```
command option1 option2 . . . optionN
```

这种单行屏幕命令通常被称为命令行。在命令行上，你输入一个命令，后跟零个或多个选项（或参数）。这些选项字符串——命令行选项（或命令行参数）——修改命令的工作方式，以便你可以执行特定任务。

Shell 使用空格或制表符来区分命令和选项。当然，通过使用空格或制表符将命令与选项以及选项之间分隔开来，你可以帮助它。

选项可以包含空格——你所要做的就是将该选项放在引号内，以便包含空格。例如，为了在密码文件中搜索我的名字，我输入以下 `grep` 命令（`grep` 用于在文件中搜索文本）：

```
grep "Naba Barkakati" /etc/passwd
```

当 `grep` 打印出带有我名字的那一行时，它看起来像这样：



```
naba:x:1000:100:Naba Barkakati:/home/naba:/bin/bash
```

如果你创建了一个带有你用户名的用户账户，输入 `grep` 命令，以你的用户名作为参数，以在 `/etc/passwd` 文件中查找该用户名。

在 `grep` 命令的输出中，你可以看到最后一个冒号（`:`）之后的 shell 名称（`/bin/bash`）。

命令行选项的数量及其格式，当然取决于实际的命令。通常，这些选项看起来像 `-X`，其中 `X` 是一个字符。例如，`ls` 命令列出目录的内容。你可以使用 `-l` 选项查看更多详细信息。例如，这是在用户的家目录中输入 `ls -l` 的结果：

```
total 0
drwxr-xr-x 2 naba users 48 2005-09-08 21:11 bin
drwx------ 2 naba users 320 2005-09-08 21:16 Desktop
drwx------ 2 naba users 80 2005-09-08 21:11 Documents
drwxr-xr-x 2 naba users 80 2005-09-08 21:11 public_html
drwxr-xr-x 2 naba users 464 2005-09-17 18:21 sdump
```

如果一个命令太长而无法容纳在一行内，你可以按下反斜杠键，然后按 Enter。然后，在下一行继续输入命令。例如，输入以下命令。（每行之后按 Enter。）

```
cat \
/etc/passwd
```

随后，`cat` 命令会显示 `/etc/passwd` 文件的内容。

你可以在同一行中`连接`（即串联）几个较短的命令。只需使用分号 (`;`) 分隔这些命令即可。例如，以下命令：

```bash
cd; ls -l; pwd
```

会将当前目录变更为主目录，列出该目录的内容，然后显示该目录的名称。

## 组合 Shell 命令

你可以组合简单的 Shell 命令以创建更复杂的命令。例如，假设你想检查系统中 `/dev` 目录下是否有一个名为 `sbpcd` 的设备文件，因为某些文档说明你需要该设备文件来支持 Sound Blaster Pro CD-ROM 驱动器。你可以使用 `ls /dev` 命令获取 `/dev` 目录的列表，然后浏览该列表以检查其中是否包含 `sbpcd`。

遗憾的是，`/dev` 目录中有大量条目，因此你可能很难找到名称中包含 `sbpcd` 的某个项目。不过，你可以将 `ls` 命令与 `grep` 结合使用，从而得到一个完全符合你需求的命令行。该命令行如下所示：

```bash
ls /dev | grep sbpcd
```

Shell 将 `ls` 命令的输出（目录列表）发送给 `grep` 命令，后者会搜索字符串 `sbpcd`。这条竖线 (`|`) 被称为`管道`，因为它充当两个程序之间的通道（想象一下水管）——第一个命令的输出被输入到第二个命令中。

## 控制命令的输入和输出

大多数 Linux 命令都有一个共同特点——它们始终从`标准输入`（通常是键盘）读取数据，并写入`标准输出`（通常是屏幕）。错误消息则发送到`标准错误`（通常也发送到屏幕）。这三个设备通常被称为 `stdin`、`stdout` 和 `stderr`。

你可以让命令从文件获取输入，然后将输出发送到另一个文件。顺便提一下，这项功能的高雅术语是`输入输出重定向`或`I/O 重定向`。

表 2-1 展示了常见 I/O 重定向命令的语法，接下来的几个章节将解释如何使用其中的一些命令。

**表 2-1 常见的标准 I/O 重定向**

| 任务 | 命令语法 |
| :--- | :--- |
| 将 `stdout` 发送到文件 | `command` > `file` |
| 将 `stderr` 发送到文件 | `command` 2> `file` |
| 将 `stdout` 和 `stderr` 发送到文件 | `command` > `file` 2>&1 |
| 从文件读取 `stdin` | `command` < `file` |
| 从 `file.in` 读取 `stdin` 并将 `stdout` 发送到 `file.out` | `command` < `file.in` > `file.out` |
| 将 `stdout` 追加到文件末尾 | `command` >> `file` |
| 将 `stderr` 追加到文件末尾 | `command` 2>> `file` |
| 将 `stdout` 和 `stderr` 追加到文件末尾 | `command` >> `file` 2>&1 |
| 从键盘读取 `stdin` 直到字符 c | `command` <<c |
| 将 `stdout` 通过管道传输给 `command2` | `command` | `command2` |
| 将 `stdout` 和 `stderr` 通过管道传输给 `command2` | `command` 2>&1 | `command2` |

### 从文件获取命令输入

如果你希望命令从文件读取数据，可以将标准输入重定向以从该文件而非键盘获取数据。例如，输入以下命令：

```bash
sort < /etc/passwd
```

该命令显示 `/etc/passwd` 文件中各行内容的排序列表。在这种情况下，小于号 (`<`) 将 `stdin` 重定向，使 `sort` 命令从 `/etc/passwd` 文件读取输入。

### 将命令输出保存至文件

要将命令的输出保存到文件中，请将标准输出重定向到文件。例如，输入 `cd` 切换到你的主目录，然后输入以下命令：

```bash
grep typedef /usr/include/* > typedef.out
```

该命令在 `/usr/include` 目录中的所有文件中搜索 `typedef` 文本的出现——然后将输出保存在名为 `typedef.out` 的文件中。大于号 (`>`) 将 `stdout` 重定向到文件。该命令还展示了 `bash` 的另一个特性：当你使用星号 (`*`) 时，`bash` 会用指定目录中所有文件名的列表替换该星号。因此，`/usr/include/*` 意味着`/usr/include` 目录中的所有文件`。

![](img/792720823146d68f19fd50c99ebfce4b_191_0.png)

如果你希望将命令的输出追加到现有文件的末尾，而不是将输出保存到新文件中，请像这样使用两个大于号 (`>`)：

```bash
command >> filename
```

![](img/792720823146d68f19fd50c99ebfce4b_191_1.png)

将 `stdout` 发送到文件的另一个有趣用法是利用 `cat` 命令快速创建小型文本文件。例如，假设你想创建一个新文本文件，在该文件中持续保存你输入的行，直到你输入 `ZZ` 并按下 Enter。以下是完成此任务的方法：

```bash
cat <<ZZ > input.txt
```

输入此命令后，你可以继续输入行，并在完成时在单独的一行输入 `ZZ`。你输入的所有内容都应保存在文件 `input.txt` 中。

### 将错误消息保存至文件

有时你输入的命令会产生大量`错误消息`，它们滚动得如此之快，以至于你无法看清发生了什么。查看所有错误消息的一种方法是将它们保存到文件中，这样你就可以查看究竟发生了什么。你可以通过将 `stderr` 重定向到文件来实现这一点。

例如，输入以下命令：

```bash
find / -name COPYING -print 2> finderr
```

该命令在整个文件系统中查找名为 `COPYING` 的文件，但将所有`错误消息`保存在 `finderr` 文件中。数字 `2` 后跟大于号 (`>`) 将 `stderr` 重定向到文件。

![](img/792720823146d68f19fd50c99ebfce4b_191_2.png)

如果你希望简单地丢弃错误消息，而不是将它们保存到文件中，请使用 `/dev/null` 作为文件名，如下所示：

```bash
find / -name COPYING -print 2> /dev/null
```

![](img/792720823146d68f19fd50c99ebfce4b_191_3.png)

该 `/dev/null` 是一个特殊文件——通常被称为`比特桶`（bit bucket），有时被美化为`天上的伟大比特桶`（Great Bit Bucket in the Sky）——它仅仅丢弃所接收的任何内容。所以现在你知道，当你听到诸如“你的邮件很可能进了比特桶”这样的短语时，他们的意思是什么了。

## 通过自动命令补全减少输入

许多命令接收文件名作为参数。例如，要查看 `/etc/modprobe.conf` 文本文件的内容，输入以下命令：

```bash
cat /etc/modprobe.conf
```



`cat` 命令显示 `/etc/modprobe.conf` 文件。对于任何接收文件名作为参数的命令，你都可以使用 `bash` 的一项功能来避免输入整个文件名。你只需输入最少量的内容——即最初几个字符——以唯一识别其目录中的文件即可。

要查看示例，输入 `cat /etc/mod` 但不要按 Enter；而是按 Tab。`bash` 会自动补全文件名，因此命令变为 `cat /etc/modprobe.conf`。现在按 Enter 运行该命令。

每次你输入文件名时，在文件名最初几个字符后按 Tab。`bash` 很可能可以补全文件名，这样你就不必输入整个名称。如果你输入的字符不足以唯一识别该文件，`bash` 会发出蜂鸣声。只需再输入几个字符并按 Tab 即可。

![](img/792720823146d68f19fd50c99ebfce4b_192_0.png)

## 大胆使用星号和问号

你还可以通过另一种方式避免输入长长的文件名。（毕竟，减少用户的工作量就是计算机的理念，不是吗？）

这个特定的技巧涉及使用星号 (`*`) 和问号 (`?`) 以及几种其他技巧。这些特殊字符被称为通配符，因为它们可以匹配一行文本中的零个或多个字符。

如果你熟悉 MS-DOS，你可能已经使用过诸如 `COPY *.* A:` 之类的命令来将当前目录中的所有文件复制到 A: 驱动器。`bash` 接受文件名中类似的通配符。正如你所预料的那样，`bash` 提供的通配符选项比 MS-DOS 命令解释器多得多。

你可以在 `bash` 中使用三种类型的通配符：

- 星号 (`*`) 字符匹配文件名中的零个或多个字符。这意味着 `*` 表示目录中的所有文件。
- 问号 (`?`) 匹配任何单个字符。如果你输入 `test?`，它将匹配任何以 test 开头的五个字符文本。
- 方括号中的字符集匹配该集中的任何单个字符。例如，字符串 `[aB]*` 匹配任何以 a 或 B 开头的文件名。

## 通配符

当您需要对大量文件执行某种操作时，通配符非常有用。例如，要将 `/media/cdrom` 目录中的所有文件复制到当前目录，请键入以下命令：

```bash
cp /media/cdrom/* .
```

`bash` 会用 `/media/cdrom` 目录中所有文件的名称替换通配符字符 `*`。命令末尾的句点（`.`）代表当前目录。

您可以将星号与文件名的其他部分结合使用，以选择更具体的一组文件。假设您想使用 `grep` 命令在 `/usr/include` 目录中符合以下标准的文件中搜索文本 `typedef struct`：

- 文件名以 s 开头。
- 文件名以 .h 结尾。

通配符规格 `s*.h` 表示所有符合这些标准 的文件名。因此，您可以使用以下命令执行搜索：

```bash
grep "typedef struct" /usr/include/s*.h
```

该字符串包含一个空格，而您需要 `grep` 命令找到它，因此必须将该字符串用引号括起来。这样，`bash` 就不会尝试将该文本中的每个单词解释为单独的命令行参数。

问号 (`?`) 匹配单个字符。假设当前目录中有四个文件——`image1.pcx`、`image2.pcx`、`image3.pcx` 和 `image4.pcx`。要将这些文件复制到 `/mnt/floppy` 目录，请使用以下命令：

```bash
cp image?.pcx /mnt/floppy
```

`bash` 会将单个问号替换为任意单个字符，并将这四个文件复制到 `/mnt`。

第三种通配符格式——`[ .. ]`——匹配方括号内特定字符集中的单个字符。您可能希望将此格式与其他通配符结合使用，以将匹配的文件名缩小到更小的集合。要查看 `/etc/X11/xdm` 目录中所有以 x 或 X 开头的文件名的列表，请键入以下命令：

```bash
ls /etc/X11/xdm/[xX]*
```

## 重复之前输入的命令

为了让您轻松重复长命令，`bash` 将多达 500 条旧命令存储为 *命令历史* 的一部分（基本上就是旧命令的列表）。要查看命令历史，请键入 `history`。`bash` 会显示旧命令的编号列表，包括您在之前登录期间输入的命令。

如果命令列表太长，您可以限制想要查看的旧命令数量。例如，要仅查看最近的十条命令，请键入此命令：

```bash
history 10
```

要重复 `history` 命令显示的列表中的某个命令，只需键入一个感叹号 (`!`)，然后跟上该命令的编号。要重复编号为 3 的命令，请键入 `!3`。

您可以在不知道命令编号的情况下重复某个命令。假设您几分钟前输入了 `more /usr/lib/X11/xdm/xdm-config`，现在您想再次查看该文件。要重复之前的 `more` 命令，请键入以下内容：

```bash
!more
```

通常，您可能希望重复刚输入的最后一条命令，也许只需稍作修改。例如，您可能已使用 `ls -1` 命令显示了目录的内容。要重复该命令，请按照以下方式键入两个感叹号：

```bash
!!
```

有时，您可能希望重复上一条命令，但为其添加额外的参数。假设 `ls -1` 显示的文件太多了。只需重复该命令，但通过 `more` 命令将输出管道传输，如下所示：

```bash
!! | more
```

`bash` 会用之前的命令替换两个感叹号，然后在该命令后附加 `| more`。

回忆之前命令的最简单方法是：只需按下上箭头键，`bash` 就会不断回溯您之前输入的命令历史。要在命令历史中向前移动，请按下下箭头键。

![](img/792720823146d68f19fd50c99ebfce4b_194_0.png)

## 发现和使用 Linux 命令

您在 shell 提示符下键入 Linux 命令。由 *Linux 命令* 是指 *bash* shell 理解的部分命令以及随 Linux 提供的命令行实用工具。在本节中，我将向您介绍几类主要的 Linux 命令。

我在一章中不可能涵盖每一个 Linux 命令，但我希望通过展示常见 Linux 命令列表（见表 2-2）让您感受这些命令的广泛性。该表格按类别列出了常见的 Linux 命令。在开始记忆任何 Linux 命令之前，请先浏览此表格。

**表 2-2 常见 Linux 命令概览**

| 命令名称 | 操作 |
| :--- | :--- |
| **获取在线帮助** |  |
| `apropos` | 查找指定关键字的在线手册页 |
| `info` | 显示关于指定命令的在线帮助信息 |
| `man` | 显示在线帮助信息 |
| `whatis` | 类似于 `apropos`，但仅搜索完整单词 |
| **使命令更便捷** |  |
| `alias` | 为长命令定义缩写 |
| `type` | 显示命令的类型和位置 |
| `unalias` | 删除使用 `alias` 定义的缩写 |
| **管理文件和目录** |  |
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
| **查找文件** |  |
| `find` | 根据指定条件（如名称和大小）查找文件 |
| `locate` | 使用定期更新的文件名数据库查找文件。（该数据库由 `updatedb` 程序创建。） |
| `whereis` | 在 `executable`（也称为 *binary*）文件所在的典型目录中查找文件 |
| `which` | 在 `PATH` 环境变量中列出的目录中查找文件 |
| **处理文件** |  |
| `cat` | 在标准输出上显示文件（可用于将几个文件合并为一个大型文件） |
| `cut` | 从文件每行文本中提取指定部分 |
| `dd` | 将一个文件中的数据块复制到另一个文件（用于从设备复制数据） |
| `diff` | 比较两个文本文件并找出差异 |
| `expand` | 将所有制表符转换为空格 |
| `file` | 显示文件中的数据类型 |
| `fold` | 将每行文本换行以适应指定宽度 |
| `grep` | 在文本文件中搜索正则表达式 |
| `less` | 一次显示一页文本文件（也可以向后翻页） |
| `lpr` | 打印文件 |
| `more` | 一次显示一页文本文件（只能向前翻页） |
| `nl` | 对文本文件中所有非空行进行编号，并将行打印到标准输出 |
| `paste` | 将几个文件的对应行连接起来 |
| `patch` | 使用文件原始副本和修订副本之间的差异更新文本文件 |
| `sed` | 在应用指定编辑命令的同时将文件复制到标准输出 |



## 文本处理工具

| `sort` | 对文本文件中的行进行排序 |
| `split` | 将文件拆分为几个指定大小的较小文件 |
| `tac` | 反转文件（最后一行在前，依此类推） |
| `tail` | 显示文件的最后几行 |
| `tr` | 在整个文件中用一组字符替换另一组字符 |
| `uniq` | 从文本文件中消除重复行 |
| `wc` | 统计文本文件中的行数、单词数和字符数 |
| `zcat` | 显示压缩文件（解压缩后） |
| `zless` | 一次显示一页压缩文件（也可以向后翻页） |
| `zmore` | 一次显示一页压缩文件 |

## 归档和压缩文件

| `compress` | 压缩文件 |
| `cpio` | 将文件复制到归档中或从归档中复制出来 |
| `gunzip` | 解压缩使用 GNU Zip `gzip` 压缩的文件 |
| `gzip` | 使用 GNU Zip 压缩文件 |
| `tar` | 创建一个或多个目录中文件的归档（最初用于磁带归档） |
| `uncompress` | 解压缩使用 `compress` 压缩的文件 |

## 管理进程

| `bg` | 在后台运行被中断的进程 |
| `fg` | 在前台运行进程 |
| `free` | 显示系统中空闲和已使用的内存量 |
| `halt` | 关闭 Linux 并停止计算机 |
| `kill` | 向进程发送信号（通常用于终止进程） |
| `ldd` | 显示运行程序所需的共享库 |
| `nice` | 以较低优先级运行进程（称为 nice 模式） |
| `ps` | 显示当前正在运行的进程列表 |
| `printenv` | 显示当前环境变量 |
| `pstree` | 类似于 `ps`，但清楚地显示父子关系 |
| `reboot` | 停止 Linux 然后重启计算机 |
| `shutdown` | 关闭 Linux |
| `top` | 显示处理器和内存占用最重的进程列表 |
| `uname` | 显示有关系统和 Linux 内核的信息 |

## 管理用户

| `chsh` | 更改 shell（命令解释器） |
| `groups` | 打印包含指定用户的组列表 |
| `id` | 显示指定用户名的用户和组 ID |
| `passwd` | 更改密码 |
| `su` | 以其他用户或 root 身份（在没有参数调用时）启动新的 shell |

![](img/792720823146d68f19fd50c99ebfce4b_196_0.png)

## 文件系统管理

| 命令名称 | 操作 |
| :--- | :--- |
| `df` | 汇总所有已挂载存储设备的空闲和可用空间 |
| `du` | 显示磁盘使用情况信息 |
| `fdformat` | 格式化软盘 |
| `fdisk` | 对硬盘进行分区 |
| `fsck` | 检查并修复文件系统 |
| `mkfs` | 创建新的文件系统 |
| `mknod` | 创建设备文件 |
| `mkswap` | 在文件或硬盘分区中为 Linux 创建交换空间 |
| `mount` | 将设备（例如 CD-ROM）挂载到文件系统中的目录 |
| `swapoff` | 停用交换空间 |
| `swapon` | 启用交换空间 |
| `sync` | 将*已缓冲*（保存在内存中）的数据写入文件 |
| `tset` | 显示当前终端的设备名称 |
| `umount` | 从文件系统中卸载设备 |

## 处理日期和时间

| 命令名称 | 操作 |
| :--- | :--- |
| `cal` | 显示指定月份或年份的日历 |
| `date` | 显示当前日期和时间，或设置新的日期和时间 |

## 成为 root（超级用户）

当您需要执行任何需要高权限级别的操作时（例如管理您的系统），您必须变成 `root`。通常，您使用日常用户名以普通用户身份登录。但是，当您需要超级用户的权限时，请使用以下命令变为 root：

```bash
su -
```

这是 `su` 后跟一个空格和减号（或连字符）。然后 shell 会提示您输入 `root` 密码。输入密码并按 Enter 键。

![](img/792720823146d68f19fd50c99ebfce4b_198_0.png)

Knoppix 不需要您输入任何密码即可变成 `root`。输入 `su -` 并按 Enter 后，您就会变成 `root`。（提示符会改变以指示这一变化。）顺便说一下，这听起来虽然可怕，但并没有那么糟糕，因为 Knoppix 是一个直接通过 CD-ROM 运行的 Live CD 发行版，其目的是使用 Knoppix 来试用 Linux 或修复现有 Linux 安装中的某些问题。

完成您想要以 `root` 身份执行的任何操作后（作为 `root` 您拥有做任何事的权限），输入 `exit` 返回您的普通用户名。

![](img/792720823146d68f19fd50c99ebfce4b_199_0.png)

除了使用 `su` 命令变为 `root` 外，您还可以输入 `sudo` 后跟您想以 `root` 身份运行的命令。在 Ubuntu 中，您必须使用 `sudo` 命令，因为在安装 Ubuntu 时，您无法设置 `root` 用户。如果您在 `/etc/sudoers` 文件中被列为授权用户，`sudo` 将执行命令，就好像您是以 `root` 身份登录一样。输入 `man sudoers` 以阅读有关 `/etc/sudoers` 文件的更多信息。

## 进程管理

每次 shell 执行您键入的命令时，它都会启动一个进程。Shell 本身是一个进程，shell 运行的任何脚本或程序也是。

使用 `ps ax` 命令查看进程列表。当您键入 `ps ax` 时，`bash` 会显示当前进程集。以下是我键入 `ps ax --cols 132` 时的几行输出。（我也包含 `--cols 132` 选项，以确保您能看到每个命令的完整内容。）

```text
PID TTY STAT TIME COMMAND
 1 ? S 0:01 init [5]
 2 ? SN 0:00 [ksoftirqd/0]
 3 ? S< 0:00 [events/0]
 4 ? S< 0:00 [khelper]
 9 ? S< 0:00 [kthread]
 19 ? S< 0:00 [kcpc/0]
 75 ? S< 0:00 [kblockd/0]
 115 ? S 0:00 [pdflush]
 116 ? S 0:01 [pdflush]
 118 ? S< 0:00 [k/0]
 117 ? S 0:00 [kswapd0]
 711 ? S 0:00 [kserrd]
 1073 ? S< 0:00 [kseri/0]
 2086 ? S 0:00 [kjournal]
 2239 ? S< 0:00 /sbin/udev -d
 … lines deleted …
 6374 ? S 1:51 /usr/X11R6/bin/X :0 -audit 0 -auth /var/lib/gdm/;0:0.0/Xauth -nolisten tcp vt7
 6460 ? Ss 0:02 /opt/gnome/bin/gdmreeter
 6671 ? Ss 0:00 sshd: naba [priv]
 6675 ? S 0:00 sshd: naba@pts/0
 6676 pts/0 Ss 0:00 –bash
 6712 pts/0 S 0:00 vatfpd
 14782 ? S 0:00 pickup -l -t fifo –u
 14752 pts/0 R+ 0:00 ps ax –cols 132
```

![](img/792720823146d68f19fd50c99ebfce4b_199_1.png)

在此列表中，第一列的标题是 `PID`，并为每个进程显示一个数字。`PID` 代表进程 `ID`（标识），这是由 Linux 内核分配的顺序号。如果您查看 `ps ax` 命令的输出，您会看到 `init` 命令是第一个进程，其 `PID`（或进程号）为 1。这就是为什么 `init` 被称为“所有进程的 mother”。

`COMMAND` 列显示创建每个进程的命令，`TIME` 列显示该进程使用的累积 CPU 时间。`STAT` 列显示进程的状态——`S` 表示进程正在睡眠，`R` 表示正在运行。状态字母后面的符号具有进一步的含义；例如，`<` 表示高优先级进程，`+` 表示进程在前台运行。`TTY` 列显示与进程关联的终端（如果有）。

进程 ID 或进程号在您必须强制停止失控进程时非常有用。查看 `ps ax` 命令的输出，并注意问题进程的 `PID`。然后，使用该进程号使用 `kill` 命令。例如，要停止进程号 8550，请从键入以下命令开始：



```bash
kill 8550
```

如果五秒后进程仍未停止，请重复该命令。停止顽固进程的下一步是键入 `kill -INT pid`，其中 `pid` 是进程号。如果这不起作用，请尝试作为最后手段使用以下命令：

```bash
kill -9 8550
```

`-9` 选项意味着向进程发送信号编号 9。巧合的是，信号编号 9 是 `KILL` 信号，这应该会导致进程退出。您也可以将此命令键入为 `kill -KILL pid`，其中 `pid` 是进程 ID。

## 处理日期和时间

您可以使用 `date` 命令显示当前日期和时间，或设置新的日期和时间。在 shell 提示符下键入 `date`，您将获得类似以下的结果：

```text
Mon Dec 5 20:51:07 EST 2005
```

如您所见，单独的 `date` 命令显示当前日期和时间。

要设置日期，请以 `root` 身份登录，然后键入 `date`，后跟 `MMDDhhmmYYYY` 格式的日期和时间，其中每个字符都是数字。例如，要将日期和时间设置为 2006 年 12 月 31 日 晚上 9:30，您键入

```bash
date 123121302006
```

![](img/792720823146d68f19fd50c99ebfce4b_200_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_200_1.png)

`MMDDhhmmYYYY` 日期和时间格式类似于 24 小时军用时钟，其含义如下：

-   `MM` 是月份的双位数数字（01 到 12）。
-   `DD` 是当月日期的双位数数字（01 到 31）。
-   `hh` 是 24 小时制的小时双位数数字。（00 是午夜，23 是 11 p.m。）
-   `mm` 是分钟的双位数数字（00 到 59）。
-   `YYYY` 是四位数的年份（例如 2006）。

另一个有趣的与日期相关的命令是 `cal`。如果您在不带任何选项的情况下键入 `cal`，它会打印当前月份的日历。如果键入 `cal` 后跟一个数字，`cal` 会将该数字视为年份，并打印该年份的日历。要查看特定年份特定月份的日历，请提供月份编号（1 = 一月，2 = 二月，依此类推），后跟年份。因此，要查看 2006 年一月的日历，请键入 `cal 1 2006`，您将获得该月的日历，如下所示：

```text
    January 2006
Su Mo Tu We Th Fr Sa
 1  2  3  4  5  6  7
 8  9 10 11 12 13 14
15 16 17 18 19 20 21
22 23 24 25 26 27 28
29 30 31
```

## 处理文件

您可以使用 `grep` 搜索文本文件，并使用 `more` 一次一屏地查看文本文件。例如，要在 `/etc/passwd` 文件中搜索我的用户名，我使用

```bash
grep naba /etc/passwd
```

要一次一屏地查看 `/etc/inittab` 文件，我键入

```bash
more /etc/inittab
```

每当屏幕暂停时，我按空格键转到下一页。

许多其他 Linux 命令处理文件——主要是文本文件，但某些命令也适用于任何文件。我接下来描述一些文件处理工具。

![](img/792720823146d68f19fd50c99ebfce4b_202_0.png)

### 统计文本文件中的单词数和行数

我始终对文件的大小很好奇。对于文本文件而言，字符数基本上就是文件的字节大小（因为每个字符占用一个字节存储空间）。那么单词数和行数呢？

Linux 的 `wc` 命令可以派上用场。`wc` 命令会显示文本文件中字符、单词和总行数的统计结果。例如，输入 `wc /etc/initab`，你会看到类似以下的输出：

```
97    395    2926 /etc/initab
```

在此例中，`wc` 报告 `/etc/initab` 文件中有 97 行，395 个单词和 2,926 个字符。如果你只想查看文件中的行数，可以使用 `-l` 选项，并输入 `wc -l /etc/initab`。输出结果应类似于以下内容：

```
97 /etc/initab
```

如你所见，使用 `-l` 选项时，`wc` 仅显示行数。

如果未指定文件名，`wc` 命令将从标准输入中读取数据。你可以利用 shell 的管道功能（`|`）将其他命令的输出传递给 `wc`，这有时非常有用。

![](img/792720823146d68f19fd50c99ebfce4b_202_1.png)

假设你想粗略统计系统上正在运行的进程数。你可以使用 `ps ax` 命令获取所有进程的列表，但不要手动计算行数，只需将 `ps` 的输出管道传输给 `wc`，即可自动获得粗略的统计结果：

```
ps ax | wc -l
86
```

这里 `ps` 命令产生了 86 行输出。由于第一行仅显示表格列的标题，因此可以估算系统上大约有 85 个进程正在运行。（当然，这个统计结果可能还包括了用于运行 `ps` 和 `wc` 命令本身的进程，但谁还在*认真*计数呢？）

### 排序文本文件

你可以使用 `sort` 命令对文本文件中的行进行排序。要了解 `sort` 命令的工作原理，首先输入 `more /etc/passwd` 查看 `/etc/passwd` 文件的当前内容。然后输入 `sort /etc/passwd` 查看按字母顺序排列的行。如果你想对文件进行排序并将排序后的版本保存到另一个文件中，你需要使用 `bash` shell 的输出重定向功能，如下所示：

```
sort /etc/passwd > ~/sorted.text
```

此命令对 `/etc/passwd` 文件中的行进行排序，并将输出保存到你主目录中名为 `sorted.text` 的文件里。

### 替换或删除文件中的字符

另一个有趣的命令是 `tr` —— 它在整个文件中将一组字符替换为另一组字符（或删除选定字符）。假设你偶尔需要在 Linux 系统上使用 MS-DOS 文本文件。虽然你可能认为文本文件可以在任何系统上无障碍使用，但你会发现一个陷阱：DOS 使用回车符后跟换行符来标记每行的结束，而 Linux 仅使用换行符。

在 Linux 系统中，你可以使用带有 `-d` 选项的 `tr` 命令来消除 DOS 文本文件中多余的回车符。基本上，要将名为 `filename.dos` 的 DOS 文本文件转换为名为 `filename.linux` 的 Linux 文本文件，请输入以下内容：

![](img/792720823146d68f19fd50c99ebfce4b_203_0.png)

```
tr -d '\015' < filename.dos > filename.linux
```

在此命令中，`'\015'` 表示八进制记法下的回车字符代码。

### 将文件分割为多个较小的文件

当你想将文件复制到软盘但文件太大无法放在单张软盘上时，`split` 命令非常方便。此时，你可以使用 `split` 命令将文件拆分为多个较小的文件，每个文件都可以放在一张软盘上。

默认情况下，`split` 将 1,000 行放入每个文件中。新生成的分割文件以字母组合命名，例如 `aa`、`ab`、`ac` 等。你可以为文件名指定前缀。例如，要将一个大文件 `hugefile.tar` 分割成可以放在多张高密度 3.5 英寸软盘上的较小文件，请如下使用 `split`：

```
split -b 1440k hugefile.tar part.
```

此命令将 `hugefile.tar` 文件分割成 1440K 大小的块，以便每个块都能放在一张软盘上。该命令会创建名为 `part.aa`、`part.ab`、`part.ac` 等的文件。

要将分割后的文件重新合并为一个文件，请如下使用 `cat` 命令：

```
cat part.?? > hugefile.tar
```

在这种情况下，两个问号 (`??`) 匹配文件名中的任何两个字符扩展名。换句话说，文件名 `part.??` 匹配所有如 `part.12, part.aa, part.ab, part.2b` 等文件名。

## 编写 Shell 脚本

如果你曾经使用过 MS-DOS，你可能记得 MS-DOS *批处理文件*。这些是包含 MS-DOS 命令的文本文件。类似地，*shell 脚本*也是包含一系列 shell 命令的文本文件。

如果你不是程序员，可能会觉得编程很令人望而生畏，但 shell 编程可以很简单，只需将几条命令存储在一个文件中即可。此刻，你也许还不会编写复杂的 shell 脚本，但你完全可以尝试一个简单的 shell 脚本。

为了尝试编写一点 shell 程序，请在 shell 提示符下按照所示准确输入以下文本，完成后按 Ctrl+D：



```
cd
cat > simple
#!/bin/sh
echo "This script's name is: $0"
echo Argument 1: $1
echo Argument 2: $2
```

按 `Ctrl+D`。

`cd` 命令将当前目录更改为家庭目录。然后 `cat` 命令显示下一行以及你在按下 `Ctrl+D` 之前输入的其他行。在这种情况下，我使用 `> simple` 将输出发送到名为 `simple` 的文件中。按下 `Ctrl+D` 后，`cat` 命令结束，你会再次看到 shell 提示符。你创建了一个名为 `simple` 的文件，其中包含以下 shell 脚本：

```
#!/bin/sh
echo "This script's name is: $0"
echo Argument 1: $1
echo Argument 2: $2
```

第一行使 Linux 运行 `bash` shell 程序（名称为 `/bin/bash`）。然后 shell 读取脚本中*剩余*的行。

![](img/792720823146d68f19fd50c99ebfce4b_204_0.png)

正如大多数 Linux 命令接受命令行选项一样，`bash` 脚本也接受命令行选项。在脚本内部，你可以将选项引用为 `$1`、`$2` 等。特殊名称 `$0` 指的是脚本本身的名称。

要运行此 shell 脚本，首先必须使用以下命令使文件可执行（即把它变成一个程序）：

```
chmod +x simple
```

现在输入 `./simple one two` 来运行脚本，它将显示以下输出：

```
This script's name is: ./simple
Argument 1: one
Argument 2: two
```

脚本名称前的 `./` 前缀表示 `simple` 文件位于当前目录中。

此脚本仅打印脚本的名称以及用户在脚本名称后输入的前两个命令行选项。

接下来，尝试使用几个参数运行脚本，如下所示：

```
./simple "This is one argument" second-argument third
This script's name is: ./simple
Argument 1: This is one argument
Argument 2: second-argument
```

shell 将双引号内的整个字符串视为单个参数。否则，shell 使用空格作为命令行中参数之间的分隔符。

大多数有用的 shell 脚本比这个简单脚本要复杂得多，但这个简单的练习能让你大致了解如何编写 shell 脚本。

![](img/792720823146d68f19fd50c99ebfce4b_205_0.png)

将 Linux 命令放入文件中，并使用 `chmod` 命令使文件可执行。看！你创建了一个 shell 脚本！

# 第 3 章：导航 Linux 文件系统

## 本章内容

- 理解 Linux 文件系统
- 使用 Linux 命令导航文件系统
- 理解文件权限
- 使用 Linux 命令操作文件和目录

要熟练使用文件和目录，你需要理解层次化文件系统的概念。即使你使用图形用户界面（GUI）文件管理器来访问文件和文件夹（文件夹也称为*目录*），了解文件系统的布局也会受益匪浅。

在本章中，我将向你介绍 Linux 文件系统，并让你发现如何使用几个 Linux 命令来操作文件和目录。

### 理解 Linux 文件系统

与其他操作系统一样，Linux 将信息组织在文件和目录中。目录反过来又容纳文件。*目录*是一种特殊的文件，可以包含其他文件和目录。由于目录可以包含其他目录，这种文件组织方式形成了一个层次结构。这种文件的层次化组织被称为*文件系统*。

Linux 文件系统为你提供了 PC 上所有存储的统一视图。文件系统有一个单一的*根*目录，由正斜杠 (`/`) 表示。在*根*目录内部是文件和目录的层次结构。文件系统的部分可以驻留在不同的物理介质上，如硬盘、软盘和 CD-ROM。图 3-1 说明了 Linux 文件系统的概念（在任何 Linux 系统中都是相同的）以及它如何跨越多个物理设备。

## **图 3-1：** Linux 文件系统提供统一的存储视图，该视图可能跨越多个存储设备。

![](img/792720823146d68f19fd50c99ebfce4b_207_0.png)

如果你熟悉 MS-DOS 或 Windows，你可能会发现 Linux 文件系统中缺少某些元素：你在 Linux 中找不到驱动器字母。所有磁盘驱动器和 CD-ROM 驱动器都是单个文件系统的一部分。

在 Linux 中，你可以使用长文件名（最多 256 个字符），并且文件名是区分大小写的。通常，这些文件名有多个扩展名，例如 `sample.tar.Z`。UNIX 文件名可以采取多种形式，例如：`index.html`、`Makefile`、`binutils-2.15.92.0.2-5.i386.rpm`、`vsftpd_2.0.3-1_i386.deb`、`_bash_profile` 和 `httpd_src.tar.gz`。

要定位文件，仅凭文件名是不够的。你还需要关于目录层级的信息。显示导致该文件的完整目录层级的扩展文件名被称为**路径名（pathname）**。顾名思义，它是通过文件系统迷宫到达文件的路径。图 3-2 显示了 Linux 中文件的一个典型路径名。

如图 3-2 所示，路径名包含以下部分：

- 根目录，由正斜杠 (`/`) 字符指示。
- 目录层级，每个目录名与前一个目录名之间用正斜杠 (`/`) 字符分隔。最后一个目录名之后出现 //。
- 文件名，包含一个名称和一个或多个可选扩展名。（每个扩展名前都有一个句点。）

## 图 3-2：文件的路径名显示了通往该文件的目录序列。

![](img/792720823146d68f19fd50c99ebfce4b_208_0.png)

Linux 文件系统有一组定义明确的一级目录，其中一些目录具有特定用途。如果你了解这些目录的用途，将更容易在文件系统中导航。当你面对新情况时，你也会熟练地猜测在哪里查找特定类型的文件。表 3-1 简要描述了 Linux 文件系统中的顶级目录。

### 表 3-1 Linux 文件系统中的顶级目录

| **目录** | **描述** |
| :--- | :--- |
| `/` | 这个 `root` 目录构成了文件系统的基础。无论其物理位置如何，所有文件和目录在逻辑上都包含在 `root` 目录中。 |
| `/bin` | 包含作为 Linux 操作系统一部分的可执行程序。许多 Linux 命令，如 `cat`、`cp`、`ls`、`more` 和 `cat`，都位于 `/bin` 中。 |
| `/boot` | 包含 Linux 内核以及 LILO 和 GRUB 引导管理器所需的文件。（内核和其他文件可以放在任何位置，但将其放在 `/boot` 目录中是惯例。） |
| `/dev` | 包含代表连接到系统的设备的特殊文件。 |
| `/etc` | 包含大多数系统配置文件和初始化脚本（在 `/etc/rc.d` 子目录中）。 |
| `/home` | 所有用户主目录的传统位置。例如，用户 naba 的主目录是 `/home/naba`。 |
| `/lib` | 包含存储在 `/sbin` 和 `/bin` 目录中的所有程序（包括可加载驱动模块）所需的库文件，以启动 Linux。 |
| `/lost+found` | 用于丢失文件的目录。每个磁盘分区都有一个 `lost+found` 目录。 |
| `/media` | 用于挂载可移动介质（如 CD/DVD-ROM 驱动器、软盘和 Zip 磁盘）上的文件系统的目录。包含用于挂载软盘的 `/media/floppy` 目录以及用于挂载 CD/DVD-ROM 驱动器的 `/media/cdrom` 或 `/media/cdrom0` 目录。如果你有 CD/DVD 刻录机，你会发现 `/media/cdrecorder` 目录代替了 `/media/cdrom`。 |
| `/mnt` | 用于临时挂载文件系统的目录。 |
| `/opt` | 为大型应用软件包提供存储区域。例如，某些发行版将 OpenOffice.org 办公套件安装在 `/opt` 目录中。 |
| `/proc` | 一个特殊目录，包含有关在 Linux 系统中运行的进程的各种信息。 |
| `/root` | root 用户的主目录。 |
| `/sbin` | 包含代表通常用于系统管理任务并由 root 用户使用的命令的可执行文件。如 `halt` 和 `shutdown` 等命令位于 `/sbin` 目录中。 |
| `/srv` | 包含由该系统提供的服务（如 Web 和 FTP）的数据。 |
| `/sys` | 一个特殊目录，包含由 Linux 内核看到的设备信息。 |
| `/tmp` | 任何用户都可以使用的临时目录，用作 *scratch* 目录，这意味着该目录的内容被视为不重要，并且通常每次系统启动时都会删除。 |



`/usr` 包含许多重要程序的子目录，例如 `/usr/X11R6` 目录中的 X Window 系统和在线手册。（表 3-2 显示了 `/usr` 中的一些标准子目录。）

`/var` 包含各种系统文件（如日志），以及用于保存其他信息的目录，例如 Web 服务器和匿名 FTP 服务器的文件。

`usr` 和 `var` 目录还包含许多标准子目录。表 3-2 列出了 `usr` 中的重要子目录。表 3-3 显示了 `var` 目录的类似分解。

### 表 3-2 重要的 `usr` 子目录

| **子目录** | **描述** |
| :--- | :--- |
| `/usr/X11R6` | 包含 X Window 系统软件。 |
| `/usr/bin` | 包含更多 Linux 命令的可执行文件，包括在 Linux 中常见的实用程序，但它们不是核心 Linux 操作系统的一部分。 |
| `/usr/games` | 包含一些旧的 Unix 游戏。 |
| `/usr/include` | 包含 C 和 C++ 编程语言的标题文件（文件名以 .h 结尾）；还包括 `/usr/include/X11` 目录中的 X11 标题文件和 `/usr/include/linux` 目录中的 Linux 内核标题文件。 |
| `/usr/lib` | 包含 C 和 C++ 编程语言的库；还包含许多其他库，如数据库库、图形工具库等。 |
| `/usr/local` | 包含本地文件。例如，`/usr/local/bin` 目录通常被指定为系统上开发的任何可执行程序的位置。 |
| `/usr/sbin` | 包含许多管理命令，如电子邮件和网络命令。 |
| `/usr/share` | 包含共享数据，如许多应用的默认配置文件和图像。例如，`/usr/share/gnome` 包含 GNOME 桌面的各种共享文件，而 `/usr/share/doc` 包含许多 Linux 应用（如 `bash` shell、`Sawfish` 窗口管理器和 `GIMP` 图像处理程序）的文档文件。 |
| `/usr/share/man` | 包含在线手册（你可以使用 `man` 命令阅读）。 |
| `/usr/src` | 包含 Linux 内核（核心操作系统）的源代码。 |

### 表 3-3 重要的 /var 子目录

| **子目录** | **描述** |
| :--- | :--- |
| `/var/cache` | 应用程序缓存数据的存储区域。 |
| `/var/lib` | 包含与应用程序当前状态相关的信息。 |
| `/var/lock` | 包含锁定文件，以确保资源仅由一个应用程序使用。 |
| `/var/log` | 包含组织在子目录中的日志文件。`syslogd` 服务器将其日志文件存储在 `/var/log` 中，文件的具体内容取决于 `syslogd` 配置文件 `/etc/syslog.conf`。例如，`/var/log/messages` 是主要系统日志文件；`/var/log/secure` 包含来自安全服务（如 `sshd` 和 `xinetd`）的日志消息；`/var/log/maillog` 包含邮件消息日志。 |
| `/var/mail` | 包含用户邮箱文件。 |
| `/var/opt` | 包含存储在 `/opt` 目录中的包的变量数据。 |
| `/var/run` | 包含描述系统自启动以来状态的数据。 |
| `/var/spool` | 包含等待某种处理的数据。 |
| `/var/tmp` | 包含在系统重启之间保留的临时文件。 |
| `/var/yp` | 包含网络信息服务（NIS）数据库文件。 |

## 使用 GUI 文件管理器

GNOME 和 KDE 桌面环境都配备了图形用户界面（GUI）文件管理器，可让您轻松浏览文件系统并执行复制和移动文件等操作。GNOME 的文件管理器被称为 `Nautilus`，而 KDE 的文件管理器被称为 `Konqueror`。我将在以下部分简要介绍这些 GUI 文件管理器。

### 使用 Nautilus 外壳

`Nautilus` 文件管理器（更准确地称为 `图形化外壳`）随 GNOME 提供。`Nautilus` 使用直观；它类似于 Windows 活动桌面。你可以使用 `Nautilus` 管理文件和文件夹，还可以管理系统。

![](img/792720823146d68f19fd50c99ebfce4b_211_0.png)

最新版本的 `Nautilus` 与你之前在 Red Hat Linux 或 Fedora Core 的早期版本中所了解的有所不同。除了你过去所熟悉的导航窗口外，`Nautilus` 现在还提供了一种新的 `对象窗口` 视图。当你在桌面上双击任何对象时，`Nautilus` 会打开一个显示该对象内容的对象窗口。如果你想要带有类似 Web 浏览器用户界面的旧版导航窗口，请右键单击一个文件夹，并从弹出菜单中选择“打开→浏览文件夹”。

### 在对象窗口中查看文件和文件夹

当你双击文件或文件夹时，`Nautilus` 会将其打开在一个它称为对象窗口的窗口中。与过去的 `Nautilus` 窗口——那些允许你浏览目录层级的窗口——不同，对象窗口没有“后退”和“前进”按钮、工具栏或侧边栏。例如，双击 GNOME 桌面左侧的“计算机”图标，`Nautilus` 会打开一个对象窗口，在其中显示计算机中的存储设备，包括文件系统。然后，如果你双击该窗口内的某个对象，`Nautilus` 会打开另一个对象窗口，显示该对象的内容。图 3-3 显示了在 `Nautilus` 中双击某些对象的结果。

`Nautilus` 对象窗口拥有一个精简的用户界面，仅包含菜单栏。你可以从菜单栏执行各种操作，例如使用应用程序打开对象、创建文件夹和文档，以及关闭对象窗口。

### 从 Nautilus 刻录数据 CD

如果你的系统连接了 CD 刻录机（可以是内置的 ATAPI CD 刻录机，也可以是连接到 USB 端口的刻录机），你可以使用 `Nautilus` 刻录数据 CD。从 `Nautilus` 对象窗口中，你可以访问内置于 `Nautilus` 中的 CD 创建器。只需按照以下简单步骤操作：

1. **在任何 Nautilus 对象窗口中，选择“位置·CD 创建器”。**
`Nautilus` 会打开一个 CD 创建器对象窗口。
注意：如果你没有打开任何 `Nautilus` 对象窗口，只需双击桌面上的“计算机”图标。
2. **从其他 Nautilus 窗口中，将你想要放入 CD 的文件和文件夹拖放到 CD 创建器窗口中。**
要获取计算机上的文件，请双击“计算机”图标在 `Nautilus` 中打开它，并找到你想要的文件。然后，将这些文件或文件夹图标拖放到 CD 创建器窗口中。
3. **在 CD 创建器窗口中，选择“文件·写入光盘”。**
`Nautilus` 会显示一个对话框，你可以在其中选择 CD 刻录机、写入速度以及其他若干选项，例如完成时是否弹出 CD。你还可以指定 CD 标题。
4. **点击“写入”按钮。**
`Nautilus` 将刻录 CD。

![](img/792720823146d68f19fd50c99ebfce4b_212_0.png)

图 3-3：默认情况下，`Nautilus` 会为每个对象打开一个新的对象窗口。

### 在导航窗口中浏览文件夹

如果你更喜欢使用熟悉的导航窗口来浏览文件夹，你需要多做一点额外的工作。不要双击图标，而是右键单击图标，并从上下文菜单中选择 **浏览文件夹**。然后，`Nautilus` 会打开一个导航窗口，其中显示该图标所代表对象的内容。例如，右键单击 GNOME 桌面左上角的“主文件夹”图标，并从上下文菜单中选择 **浏览文件夹**。`Nautilus` 会打开一个导航窗口，在其中显示你的主目录的内容。（可以将目录想象为一个可以包含其他文件和文件夹的文件夹。）图 3-4 显示了 `Nautilus` 导航窗口的典型视图。

> 图 3-4：
> 你可以在 `Nautilus` 导航窗口中查看文件和文件夹。

![](img/792720823146d68f19fd50c99ebfce4b_213_0.png)

导航窗口在垂直方向上分为两部分。左侧窗格显示了你可以使用 `Nautilus` 浏览的文件系统和其他对象的不同视图。右侧窗格显示了左侧窗格中当前所选文件夹中的文件和文件夹。`Nautilus` 为文件和文件夹显示图标。对于图像文件，它显示图像的缩略图。

导航窗口的用户界面类似于 Web 浏览器。窗口的标题栏显示当前所选文件夹的名称。窗口顶部的“位置”文本框显示目录在 Linuspeak（Linux 术语）中的完整名称——例如，图 3-4 显示了 `/home/naba/photos/April 8, 2005 - Cherry Blossoms` 目录的内容。

如果你使用过 Windows 资源管理器，你可以以类似的方式使用 `Nautilus` 导航窗口。要查看另一个目录的内容，请执行以下操作：

1. 从 **信息** 下拉菜单（位于左侧窗口中）选择 *树*。
该窗口中会出现一个目录树菜单。最初，该树显示你的主文件夹和文件系统的根目录作为一个 `FileSystem` 文件夹。



## 点击 `FileSystem` 文件夹旁边的右箭头

在生成的树视图中，找到你想要浏览的目录。

例如，要查看 `/etc` 目录，请点击 `etc` 目录旁边的右箭头。Nautilus 会显示 `/etc` 中的子目录，并将右箭头变为下箭头。`X11` 是你将在下一步中查看的 `/etc` 中的子目录之一。

## 要查看 `X11` 子目录的内容

请点击 `X11`。

右侧窗口现在显示 `/etc/X11` 目录的内容。

Nautilus 通过使用不同类型的图标来显示所选目录的内容。每个目录都显示为一个文件夹，文件夹图标下方显示目录名称。普通文件，例如 `XP86Config-4`，显示为一张纸。`x` 文件是一个指向可执行文件的链接。

Nautilus 导航窗口具有通常的菜单栏和工具栏。请注意图 3-4 中工具栏右侧的 `以图标显示` 按钮。该按钮表明 Nautilus 使用大图标显示目录内容。点击该按钮，会出现一个下拉列表。从列表中 选择 `以列表显示`，Nautilus 会使用较小的图标以列表格式显示内容，并显示详细信息，例如每个文件或目录的大小以及最后修改时间，如图 3-5 所示。

![](img/792720823146d68f19fd50c99ebfce4b_214_0.png)

如果你点击列表视图顶部的任何列标题——名称、大小、类型或修改日期——Nautilus 将根据该列对列表进行排序。例如，点击“修改日期”列标题。Nautilus 现在显示按最后修改时间排序的文件和目录列表。点击“名称”列标题会按字母顺序对文件和文件夹进行排序。

你不仅可以使用 Nautilus 导航窗口在不同文件夹之间移动，还可以执行诸如将文件从一个文件夹移动到另一个文件夹或删除文件等操作。我不逐一列出每一步。这些步骤很直观，与你在任何 GUI（如 Windows 或 Mac）中的操作类似。以下是你在 Nautilus 中可以执行的一些操作：

- 要将文件移动到不同的文件夹，请将文件图标拖放到你想要放置该文件的文件夹上。
- 要将文件复制到新位置，请选择文件图标，并从 Nautilus 菜单中选择“编辑 → 复制文件”。（或者，你可以右键单击文件图标，并从上下文菜单中选择“复制文件”。）然后移动到你要复制文件的文件夹，并选择“编辑 → 粘贴文件”。
- 要删除文件或目录，请右键单击图标，并从上下文菜单中选择“移动到回收站”。（仅当你有权限删除该文件时才能执行此操作。）要永久删除文件，请右键单击桌面上的“回收站”图标，并从上下文菜单中选择“清空回收站”。当然，只有在你确实想要删除文件时才能执行此操作。一旦你清空回收站，你就再也看不到该文件了。如果你必须从回收站中恢复文件，请双击“回收站”图标，然后将文件图标拖回你想要保存它的文件夹。你可以从回收站中恢复文件，直到你清空回收站为止。
- 要重命名文件或目录，请右键单击图标，并从上下文菜单中选择“重命名”。然后你可以出现在文本框中输入新名称（或编辑名称）。
- 要创建新文件夹，请右键单击右侧窗口的空白区域，并从上下文菜单中选择“创建文件夹”。出现新文件夹图标后，你可以通过右键单击图标并从上下文菜单中选择“重命名”来重命名它。如果你没有权限创建文件夹，该菜单项将变灰。

## 使用 Konqueror

Konqueror 是随 KDE 提供的文件管理器和 Web 浏览器。它使用直观——与 Windows 活动桌面有些相似。你可以使用 Konqueror 管理文件和文件夹（还可以查看网页）。

### 查看文件和文件夹

当您在 KDE 桌面上单击文件夹图标时，Konqueror 会自动启动并打开该文件夹。例如，单击 SUSE Linux 中 KDE 桌面左上角的“我的电脑”图标。Konqueror 运行并显示计算机的内容。单击 Konqueror 窗口左侧垂直工具栏上的“主目录”图标，然后单击中间窗格中的“主目录”。Konqueror 在其主窗口中显示用户主目录的内容（可以将目录视为可以包含其他文件和文件夹的文件夹）。图 3-6 显示了 Konqueror 中典型用户的主目录。

![](img/792720823146d68f19fd50c99ebfce4b_216_0.png)

图 3-6：您可以在 Konqueror 中查看文件和文件夹。

如果您使用过 Windows 资源管理器，您可以以类似的方式使用 Konqueror。

Konqueror 窗口垂直分为三个部分：

- 狭窄的左侧窗格显示您可以单击以在 Konqueror 中执行各种任务的图标。
- 较宽的中间窗格（可以打开或关闭）显示当前文件夹的树状视图。
- 最宽的窗格（在右侧）使用图标显示当前文件夹中的文件和文件夹。

Konqueror 使用不同类型的图标表示不同的文件，并显示每个文件内容的预览。对于图像文件，预览是图像的缩略图版本。

Konqueror 窗口的标题栏显示当前选中目录的名称。位置文本框（沿窗口顶部）显示目录的全名——在这种情况下，图 3-6 显示了 `/home/naba` 目录的内容。

使用最左侧的垂直按钮列来选择其他要浏览的内容。单击其中一个按钮时，中间窗格会显示您可以浏览的项目树菜单。例如，要浏览文件系统的其他部分，请执行以下操作：

1. **从 Konqueror 窗口最左侧的图标列（参见图 3-6）中，单击“根文件夹”图标（从底部数第二个图标）。**

中间窗格中出现目录的树菜单。

2. **在树状视图中，找到您要浏览的文件夹。**

例如，要查看 `etc` 文件夹，请单击 `etc` 文件夹旁边的加号。Konqueror 显示其他文件夹，并将加号更改为减号。

3. **要查看 `X11` 子目录的内容，向下滚动并单击 `X11`。**

右侧窗格现在显示 `/etc/X11` 目录的内容。

Konqueror 使用不同类型的图标显示文件夹的内容。每个目录显示为一个文件夹，目录名称显示在文件夹图标下方。普通文件显示为一页纸。

Konqueror 窗口具有常规的菜单栏和工具栏。您还可以以其他格式查看文件和文件夹。例如，选择 `查看` » `显示模式：` » `详细列表视图` 可以以较小的图标列表格式查看文件夹内容（见图 3-7），以及详细信息（如每个文件或目录的大小，以及最后修改时间）。

如果单击列表视图顶部的一些列标题——例如 `名称`、`大小`、`文件类型` 或 `修改时间`——Konqueror 会根据该列对列表进行排序。例如，如果您单击 `修改时间` 列标题，Konqueror 将显示按最后修改时间排序的文件和文件夹列表。单击 `名称` 列标题会按名称字母顺序对文件和目录进行排序。

您不仅可以利用 Konqueror 在不同的文件夹之间移动，还可以执行诸如将一个文件夹中的文件移动到另一个文件夹或删除文件等操作。由于这些步骤很直观，且与您在任何图形用户界面（如 Windows 或 Mac 界面）中执行的操作类似，因此我不详细列出每个步骤。以下是您可以在 Konqueror 中执行的一些操作：

- **查看文本文件**：单击文件名，Konqueror 将运行 `KWrite` 字处理程序，并在新窗口中显示该文件。
- **将文件或移动文件到另一个文件夹**：将文件图标拖放到目标文件夹上。会弹出一个菜单，询问您是要复制、移动还是仅将文件链接到该目录。
- **删除文件或目录**：右键单击图标，并从上下文菜单中选择“移动到回收站”。若要永久删除该文件，请右键单击桌面上的回收站图标，并从上下文菜单中选择“清空回收站”。当然，只有当您确实想要删除该文件时，才执行此操作。当您“清空回收站”时，被删除的文件将永远消失。如果您想从回收站中恢复文件，请双击桌面上的回收站图标，然后从该窗口中将文件图标拖放到要保存文件的文件夹中。当被询问是要复制还是移动时，请选择“移动”。在您清空回收站之前，您可以从回收站中恢复文件。
- **重命名文件或目录**：右键单击图标，并从上下文菜单中选择“重命名”。然后，您可以在出现的文本框中输入新名称（或编辑旧名称）。
- **创建新文件夹**：选择 `查看 显示模式 图标视图`。然后，右键单击最右侧窗格的空白区域，并从上下文菜单中选择“创建新目录”。然后，输入新目录的名称并单击“确定”。（如果您没有创建目录的权限，您将收到错误消息。）

![](img/792720823146d68f19fd50c99ebfce4b_218_0.png)

### 查看 Web 页面

Konqueror 不仅仅是一个文件管理器。使用它，您查看网页就像查看文件夹一样简单。只需在位置文本框中输入 Web 地址，看看会发生什么。例如，图 3-8 显示在我在工具栏上的位置文本框中输入 `www.irs.gov` 并按下 Enter 键后的 Konqueror 窗口。

![](img/792720823146d68f19fd50c99ebfce4b_219_0.png)

Konqueror 在右侧窗格中显示 Web 站点。左侧窗格保持不变。

## 使用 Linux 命令导航文件系统



虽然诸如 Nautilus（在 GNOME 中）或 Konqueror（在 KDE 中）等 GUI 文件管理器使用简便，但只有拥有可用的 GUI 桌面时才能使用它们。有时，您可能没有图形环境来运行图形文件管理器。例如，您可能通过文本终端登录，或者系统上的 X 未正常工作。在这种情况下，您必须依赖 Linux 命令来处理文件和目录。当然，即使在图形环境中，您也可以始终使用 Linux 命令——您只需打开一个终端窗口并输入 Linux 命令即可。

在以下各节中，我将简要介绍一些用于在 Linux 文件系统中导航的 Linux 命令。

## 用于目录导航的命令

在 Linux 中，当以 root 身份登录时，您的主目录是 `/root`。对于其他用户，主目录通常位于 `/home` 目录中。我的主目录（当以 naba 身份登录时）是 `/home/naba`。此信息存储在 `/etc/passwd` 文件中。默认情况下，只有您有权在主目录中保存文件，并且只有您可以创建主目录中的子目录以进一步组织您的文件。

Linux 支持当前目录的概念，它是所有文件和目录命令操作的目录。例如，登录后，您的当前目录是主目录。要查看当前目录，请输入 `pwd` 命令。

要更改当前目录，请使用 `cd` 命令。要将当前目录更改为 `/usr/lib`，请输入以下内容：

```text
cd /usr/lib
```

然后，要将目录更改为 `/usr/lib` 中的 `cups` 子目录，请输入此命令：

```text
cd cups
```

现在，如果您使用 `pwd` 命令，该命令将显示 `/usr/lib/cups` 为当前目录。

这两个例子表明，您可以以两种方式引用目录名称：

- 一个绝对路径名（如 `/usr/lib`），指定目录树中的确切目录
- 一个相对目录名（如 `cups`，表示当前目录的 `cups` 子目录，无论该目录是什么）

如果在 `/usr/lib` 中输入 `cd cups`，当前目录将更改为 `/usr/lib/cups`。然而，如果在 `/home/naba` 中输入相同的命令，shell 会尝试将当前目录更改为 `/home/naba/cups`。

![](img/792720823146d68f19fd50c99ebfce4b_220_0.png)

使用不带任何参数的 `cd` 命令可以将当前目录更改回您的主目录。无论您身在何处，在 shell 提示符下输入 `cd` 都会带您回到主目录！

顺便提一下，波浪号（`~`）指的是你的主目录。因此，命令 `cd ~` 也会将当前目录更改为你的主目录。你还可以通过在波浪号后附加其他用户的用户名来引用该用户的主目录。例如，`cd ~superman` 会将当前目录更改为 `superman` 的主目录。

![](img/792720823146d68f19fd50c99ebfce4b_221_0.png)

等等，还有更多。单个点号（`.`）和两个点号（`..`）——常被巧妙地称为 *dotdot* ——也有特殊含义。单个点号（`.`）表示当前目录，而两个点号（`..`）表示父目录。例如，如果当前目录是 `/usr/share`，你只需输入以下内容即可上移到一级目录 `/usr`：

```
cd ..
```

## 用于目录列表和权限的命令

你可以通过使用 `ls` 命令来获取目录列表。默认情况下，不带任何选项的 `ls` 命令会以紧凑的多列格式显示当前目录的内容。例如，输入以下两条命令以查看 `/etc/X11` 目录的内容：

```
cd /etc/X11
ls
```

输出如下所示。（在控制台上，你会看到某些项目显示为不同的颜色。）

```
X               Xsession.d          cursors             rgb.txt           xkb
XF86Config-4    Xsession.options    default-display-manager         restart           xserver
Xresources      Xwrapper.config     fonts                   sysconfig          xsm
Xsession        app-defaults        gdmd                  xinit
```

从这份列表（不含颜色）中，你无法判断某个条目是文件还是目录。要区分目录和文件，请使用 `ls` 命令的 `-F` 选项，如下所示：

```
ls -F
```

这次，输出提供了关于文件类型的一些额外线索：

```
X@              Xsession.d/         cursors/              rgb.txt           xkb@
XF86Config-4    Xsession.options    default-display-manager         restart/            xserver/
Xresources/     Xwrapper.config     fonts/                  sysconfig/            xsm/
Xsession*       app-defaults/       gdmd@                 xinit/
```

`ls -F` 的输出显示目录名称时会在末尾附加一个斜杠（`/`）。普通文件名则原样显示。附加在文件名后的 at 符号（@）（例如，注意名为 `X` 的文件）表示该文件是链接到另一个文件的符号链接。（换句话说，这个文件名只是指向另一个文件的快捷方式。）可执行文件会附加一个星号（*）。（例如，*Xsession* 就是一个可执行文件。）Shell 可以运行任何可执行文件。

你可以使用 `-l` 选项查看有关文件和目录的更详细信息：

```
ls -l
```

对于 `/etc/X11` 目录，`ls -l` 的典型输出如下所示：

```
total 84
lrwxrwxrwx 1 root root    20 Jul 15 20:32 X -> /usr/bin/X11/XFree86
-rw-r--r-- 1 root root  2878 Jul 16 14:50 XF86Config-4
drwxr-xr-x 2 root root  4096 Jul 15 20:32 Xresources
-rw-r--r-- 1 root root  3456 Jun  1 01:59 Xsession
drwxr-xr-x 2 root root  4096 Jul 15 20:34 Xsession.d
-rw-r--r-- 1 root root   217 Jun  1 01:59 Xsession.options
-rw------- 1 root root   771 Jul 15 20:32 Xwrapper.config
drwxr-xr-x 2 root root  4096 Jul 15 20:35 app-defaults
... lines deleted ...
```

此列表展示了每个目录条目的大量信息——每个条目可以是文件或另一个目录。从右向左查看某一行，你会看到最右侧的列显示目录条目的名称。名称之前的日期和时间显示了该文件最近一次被修改的时间。日期和时间的左侧显示了文件的字节大小。

该文件的组属主和拥有者显示在文件大小列的左侧。再往左的数字表示指向该文件的链接数。（*link* 类似于 Windows 中的快捷方式。）最后，最左侧的列显示文件的权限设置，这些设置决定了谁可以读取、写入或执行该文件。

最左侧列的第一个字母具有特殊含义，如下列表所示：

- 如果第一个字母是 `l`，则该文件是指向另一个文件的*符号链接*（快捷方式）。
- 如果第一个字母是 `d`，则该文件是一个目录。
- 如果第一个字母是破折号（`-`），则文件是普通文件。
- 如果第一个字母是 `b`，则文件代表块设备，例如磁盘驱动器。
- 如果第一个字母是 `c`，则文件代表字符设备，例如串行端口或终端。

![](img/792720823146d68f19fd50c99ebfce4b_222_0.png)

## 198 使用 Linux 命令导航文件系统

![](img/792720823146d68f19fd50c99ebfce4b_223_0.png)

在第一个字母之后，最左侧的列显示一串九个字符，当每个字符都存在时，它们显示为 `rwxrwxrwx`。每个字符表示特定的权限。如果某个位置用连字符（`-`）代替字母，则表示没有对该文件执行特定操作的权限。将这九个字符视为三组三个字符（`rwx`），解释如下：

- 最左侧的 `rwx` 组控制文件所有者的读、写和执行权限。换句话说，如果在此位置看到 `rwx`，则文件所有者可以读取（`r`）、写入（`w`）和执行（`x`）该文件。如果某个位置用连字符代替字母，则表示没有该权限。因此，字符串 `rw-` 意味着所有者具有读取和写入权限，但没有执行权限。虽然可执行程序（包括 Shell 程序）通常具有执行权限，但目录将执行权限视为等同于使用权限：用户必须在目录上具有执行权限，才能打开并读取该目录的内容。



中间的三个 `rwx` 字符控制属于该文件组的任何用户的读、写和执行权限。

最右侧的一组 `rwx` 字符控制所有其他用户（统称为 world）的读、写和执行权限。

因此，权限设置为 `rw-------` 的文件仅对文件所有者可访问，而权限设置为 `rwxr--r--` 则使该文件对所有人可读。

`ls` 命令的一个有趣功能是，它不会列出任何以点号开头的文件。要查看这些文件，你必须使用带有 `-a` 选项的 `ls` 命令，如下所示：

```
ls -a
```

在你的主目录中尝试此命令，然后将结果与不使用 `-a` 选项时看到的结果进行比较：

1. **输入 `cd` 切换到你的主目录。**
2. **输入 `ls -F` 查看你主目录中的文件和目录。**
3. **输入 `ls -aF` 查看所有内容，包括隐藏文件。**

![](img/792720823146d68f19fd50c99ebfce4b_223_1.png)

大多数 Linux 命令采用单字符选项，每个选项前都带有一个减号（将此符号视为连字符）。当你想要使用多个选项时，输入一个连字符并将选项字母串联起来（一个接一个地连接）。因此，`ls -al` 等同于 `ls -a -l` 以及 `ls -l -a`。

## 用于更改权限和所有权的命令

你可能需要更改文件的权限设置以保护文件免受他人侵害。使用 `chmod` 命令来更改文件或目录的权限设置。

要有效使用 `chmod`，你必须指定权限设置。一种好方法是按照表 3-4 中所示的顺序（Who/Action/Permission）将各列中的字母串联起来。

*注意：* 你只使用每列中的单个字符——括号内的文本仅用于解释。

表 3-4 文件权限的字母代码

| Who | Action | Permission |
| :--- | :--- | :--- |
| u (user) | + (add) | r (read) |
| g (group) | – (remove) | w (write) |
| o (others) | = (assign) | x (execute) |
| a (all) | s (set user ID) | |

例如，若要允许所有人读取目录中所有文件的访问权限，请从第一列选择 `a`（代表 *all*），从第二列选择 `+`（代表 *add*），从第三列选择 `r`（代表 *read*），从而得出权限设置 `a+r`。然后使用完整的选项集配合 `chmod`，如下所示：

```
chmod a+r *
```

另一方面，若要允许所有人执行某个特定文件，请键入：

```
chmod a+x filename
```

假设你有一个名为 `mystuff` 的文件，你想保护它。如果你按以下顺序键入以下命令，就可以使除了你自己之外没有任何人可以访问该文件：

```
chmod a-rwx mystuff
chmod u+rw mystuff
```

第一个命令关闭了所有人的所有权限，第二个命令为所有者（你）开启了读取和写入权限。输入 `ls -l` 以验证更改是否生效。（你会看到权限设置为 `-rw-------`。）以下是来自 `ls -l` 的示例输出：

```
drwxr-xr-x    2 naba naba 4096 2005-07-24 16:56 sdump
```

### 注意：第三和第四个字段显示 `naba naba`

第三和第四个字段显示 `naba naba`。这两个字段显示了文件的用户和组所有权。在这种情况下，用户的名称是 `naba`，组的名称也是 `naba`。在某些发行版中，组 ID 为 `users`。

有时，为了让一切正确运行，你必须更改文件的用户或组所有权。例如，假设你被指示（除了手册外，还能被谁指示？）创建一个名为 `cups` 的目录，并将其所有权授予用户 ID `lp` 和组 ID `sys`。你该怎么做？

嗯，你可以以 `root` 身份登录，并使用 `mkdir` 命令创建 `cups` 目录：

```
mkdir cups
```

如果你使用 `ls -l` 命令检查文件的详细信息，你会看到用户和组所有权为 `root root`。

![](img/792720823146d68f19fd50c99ebfce4b_225_0.png)

要更改所有者，请使用 `chown` 命令。例如，要将 `cups` 目录的所有权更改为用户 ID `lp` 和组 ID `sys`，请输入：

```
chown lp.sys cups
```

## 用于处理文件的命令

要将文件从一个目录复制到另一个目录，请使用 `cp` 命令。例如，要将文件 `/usr/X11R6/lib/X11/xinit/Xclients` 复制到当前目录（例如你的主目录）中的 `Xclients.sample` 文件，请输入以下内容：

```
cp /usr/X11R6/lib/X11/xinit/Xclients Xclients.sample
```

*更正：原始 OCR 文本在代码块和描述之间存在不匹配。描述中提到将 `Xclients` 复制为 `Xclients.sample`，但代码块显示的是 `xinitrc` 和 `xinitrc.sample`。根据上下文“复制文件 ... Xclients 为 ... Xclients.sample”，我已更正代码块以匹配描述。或者，如果文本原本打算谈论 xinitrc，那么描述是错误的。鉴于紧邻代码块之前的句子中明确提到了 "Xclients"，我将统一标准化为 Xclients。*

实际上，仔细查看 OCR：

`要将文件 /usr/X11R6/lib/X11/xinit/Xclients 复制为 Xclients.sample 文件...`

`代码块：cp /usr/X11R6/lib/X11/xinit/xinitrc xinitrc.sample`

这是源文本中明显的 OCR 错误或不一致。通常，书籍会保持一致性。我将假设文本的意思是描述中的 `Xclients`，或者是代码中的 `xinitrc`。然而，没有原书的情况下，保留段落的*意图*（似乎是在解释 `cp`）更安全。让我们看看下一段：“如果你想将文件复制到当前目录但保留原始名称...”。

让我们看看下一个例子：`cp /etc/X11/Xresources .`

`xinitrc` 的例子可能是一个独立的想法。

等等，文本说：“例如，要将文件 `/usr/X11R6/lib/X11/xinit/Xclients` 复制为 `Xclients.sample` 文件... 请输入以下内容：” 然后显示 `cp ... xinitrc xinitrc.sample`。

这很可能是书中或 OCR 中的复制粘贴错误。我将更正代码块以匹配文本描述 `Xclients` -> `Xclients.sample`，因为这是明确的指令。

如果你想将文件复制到当前目录但保留原始名称，请使用点 (`.`) 作为 `cp` 命令的第二个参数。因此，以下命令将 `/etc/X11` 目录中的 `Xresources` 文件复制到当前目录（由单个点表示）：

```
cp /etc/X11/Xresources .
```

`cp` 命令创建文件的新副本，并保持原始文件不变。

![](img/792720823146d68f19fd50c99ebfce4b_225_1.png)

如果你想将整个目录的内容——包括所有子目录及其内容——复制到另一个目录，请使用命令 `cp -ar sourcedir destdir`。（该命令将 `sourcedir` 目录中的所有内容复制到 `destdir`。）例如，要将 `/etc/X11` 目录中的所有文件复制到当前目录，请输入以下命令：

```
cp -ar /etc/X11 .
```

## 使用 Linux 命令导航文件系统

要将文件移动到新位置，请使用 `mv` 命令。原始副本已消失，新副本出现在目标位置。你可以使用 `mv` 来重命名文件。如果你想将 `today.list` 的名称更改为 `old.list`，请使用 `mv` 命令，如下所示：

```
mv today.list old.list
```

另一方面，如果你想将 `today.list` 文件移动到一个名为 `saved` 的子目录中，请使用此命令：

```
mv today.list saved
```

`mv` 的一个有趣功能是，你可以使用它来移动整个目录（包括其所有子目录和文件）到新位置。如果你有一个名为 `data` 的目录，其中包含许多文件和子目录，你可以使用以下命令将该整个目录结构移动到 `old_data`：

```
mv data old_data
```

要删除文件，请使用 `rm` 命令。例如，要删除名为 `old.list` 的文件，请输入以下命令：

```
rm old.list
```

小心使用 `rm` 命令——尤其是当你以 `root` 身份登录时。你可能无意间用 `rm` 删除了重要文件。

## 用于处理目录的命令



为了整理主目录中的文件，你需要创建新目录。使用 `mkdir` 命令创建目录。例如，要在当前目录中创建一个名为 `images` 的目录，请输入以下内容：

```
mkdir images
```

创建目录后，你可以使用 `cd images` 命令切换到该目录。

使用 `mkdir` 命令的 `-p` 选项可以创建整个目录树。例如，假设你的系统有一个 `/usr/src` 目录，你想创建目录树 `/usr/src/book/java/examples/applets`。要创建此目录层次结构，请输入以下命令：

```
mkdir -p /usr/src/book/java/examples/applets
```

当你不再需要某个目录时，使用 `rmdir` 命令删除它。

![](img/792720823146d68f19fd50c99ebfce4b_227_0.png)

只有当目录为空时才能删除它。要删除空的目录树，你可以使用 `-p` 选项，如下所示：

```
rmdir -p /usr/src/book/java/examples/applets
```

此命令删除 `applets` 的空父目录。当命令遇到非空目录时，它将停止。

## 用于查找文件的命令

`find` 命令对于定位符合搜索标准的文件（和目录）非常有用。

当我多年前刚开始使用 UNIX 时（1980 年代初的 Berkeley UNIX），`find` 命令让我感到困惑。在过渡到更复杂的形式之前，我坚持使用 `find` 的基本语法很长时间。我最初发现的基本语法用于在文件系统的任何位置查找文件。以下是操作过程：假设你想查找任何名称以 `gnome` 开头的文件或目录。输入以下 `find` 命令来查找这些文件：

```
find / -name "gnome*" -print
```

如果你没有以 `root` 身份登录，你可能会得到一堆错误消息。如果这些错误消息困扰你，只需按如下修改命令，这些错误消息就将成为历史。（或者，像 UNIX 爱好者常说的那样，“把它们扔进位桶里。”）

```
find / -name "gnome*" -print 2> /dev/null
```

此命令告诉 `find` 从 `root` 目录 (`/`) 开始查找匹配 `gnome*` 的文件名，并显示任何匹配文件的完整路径名。最后一部分 (`2> /dev/null`) 只是将错误消息发送到专门用于静默忽略它们的文件。

你可以使用这种简单形式的 `find` 的变体来定位任何目录（以及该目录中包含的任何子目录）中的文件。如果你忘记在你的主目录中存储了所有名为 `report*` 的文件（以 `report` 开头的名称）在哪里，你可以使用以下命令搜索这些文件：

```
find ~ -name "report*" -print
```

当你熟悉这种 `find` 语法后，你可以使用 `find` 的其他选项。例如，要查找特定类型的文件（如目录），请使用 `type` 选项。以下命令在你的 Linux 系统中显示所有顶级目录名称：

```
find / -type d -maxdepth 1 -print
```

在典型的 Linux 系统中，你可能不需要使用 `find` 的复杂形式；但如果需要，你可以使用以下命令查找其余的 `find` 选项：

```
man find
```

查找具有给定名称的所有文件的一种简单方法是使用 `locate` 命令，它搜索系统中定期更新的文件数据库。例如，以下是在 Debian 系统上输入 `locate Xresources` 时我得到的典型输出：

```
/etc/X11/Xresources
/etc/X11/Xresources/xbase-clients
/etc/X11/Xresources/xfree86-common
```

`locate` 命令在 SUSE Linux 中默认未安装。要安装它，请在 SUSE 桌面上选择 **主菜单** > **系统** > YaST 以启动 YaST2 控制中心。单击窗口左侧的 **软件**，然后单击窗口右侧的 **安装/移除软件**。在 YaST 软件安装窗口中，搜索 `locate`。然后从搜索结果中选择该软件包并单击 **接受** 以安装它。

## 用于挂载和卸载的命令

假设你想在文本控制台登录时（没有 GUI 辅助）访问本书配套 DVD-ROM 上的文件。为此，你必须首先将 DVD-ROM 驱动器的文件系统挂载到 Linux 文件系统中的特定目录上。

首先查看 `/etc/fstab` 文件以获取 CD-ROM 设备名称的线索。例如，一些 Linux 发行版使用设备名称 `/dev/cdrom` 来指代 CD/DVD-ROM 驱动器，而另一些发行版可能使用诸如 `/dev/hdc`、`/dev/cdroms/cdrom0` 或 `/dev/cdrecorder`（用于 DVD/CD-R 驱动器）这样的设备名称。`/etc/fstab` 文件中的条目还告诉你该发行版期望挂载 CD/DVD 的目录。一些发行版使用 `/media/cdrom` 作为挂载点，而另一些使用 `/media/cdrom0` 或 `/media/cdrecorder`。顺便说一下，习惯上使用 `cdrom` 术语来表示 CD-ROM 和 DVD-ROM。

![](img/792720823146d68f19fd50c99ebfce4b_228_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_228_1.png)

![](img/792720823146d68f19fd50c99ebfce4b_228_2.png)

以 **root** 身份登录（或输入 `su -` 命令以切换到 root 用户），将 DVD-ROM 插入 DVD 光驱，然后输入以下命令：

```
mount /dev/hdc /media/cdrom0
```

此命令在 Linux 文件系统中的 `/media/cdrom0` 目录（也称为 *挂载点*）上挂载名为 `/dev/hdc` 的设备（一个 IDE DVD/CD-ROM 驱动器）上的文件系统。

当 `mount` 命令成功完成其任务后，你可以通过将 `/media/cdrom0` 目录作为光盘的根目录来访问 DVD-ROM 上的文件。换句话说，要查看 DVD-ROM 的内容，请输入

```
ls -P /media/cdrom0
```

当你使用完 DVD-ROM 时——在将其从光驱弹出之前——你必须使用以下 `umount` 命令卸载光盘驱动器：

```
umount /dev/hdc
```

![](img/792720823146d68f19fd50c99ebfce4b_229_0.png)

你可以在文件系统中的任何空目录上挂载设备。然而，每个发行版都有用于挂载设备的惯用位置目录。例如，一些发行版使用 `/mnt` 中的目录，而另一些则使用 `/media` 目录作为挂载点。

## 用于检查磁盘空间使用的命令

我想向你介绍两个命令—— `df` 和 `du` ——你可以使用它们来检查系统上的磁盘空间使用情况。这些命令使用起来很简单。 `df` 命令显示所有已挂载设备的磁盘空间使用情况摘要。例如，当我在一台挂载了许多存储设备的 PC 上输入 `df` 时，我得到的是 `df` 命令的输出如下：

```
Filesystem 1K-blocks Used Available Use% Mounted on
/dev/hdb2 28243372 23772392 25872080 9% /
tmpfs 383968 12 383956 1% /dev/shm
/dev/hda5 5766924 1422232 4051744 26% /ubuntu
/dev/hda7 6258100 2989200 2951004 51% /debian/boot
/dev/hda9 5766924 1422232 4051744 26% /ubuntu
/dev/hda10 5766924 1872092 3600984 35% /smp1a
/dev/hda11 6258100 2989200 2951004 51% /debian
/dev/hdb3 1958550 1370172 1818828 8% /android
/dev/hda2 16097676 10593364 5494312 66% /windows/C
/dev/hdd1 107426620 9613028 97813592 9% /windows/D
```

输出是一个表格，列出了设备、总存储千字节数、已使用量、可用量、使用百分比以及挂载点。

要以更易读的格式查看 df 的输出，请输入 `df -h`。以下是 `df -h` 命令的输出：



```
Filesystem Size Used Avail Use% Mounted on
/dev/hda6 27G 2.3G 25G 9% /
tmpfs 375M 12K 375M 1% /dev/shm
/dev/hda5 5.5G 1.4G 3.9G 26% /ubuntu/boot
/dev/hda7 6.0G 2.9G 2.9G 51% /debian/boot
/dev/hda9 5.5G 1.4G 3.9G 26% /ubuntu
/dev/hda10 5.5G 1.8G 3.5G 35% /mepis
/dev/hda11 6.0G 2.9G 2.9G 51% /debian
/dev/hdb3 19G 1.4G 18G 8% /xandros
/dev/hda2 16G 11G 5.3G 66% /windows/C
/dev/hdb1 103G 9.2G 94G 9% /windows/D
```

如果你将此输出与纯 `df` 的输出进行比较（参见前一个列表），你会发现 `df -h` 使用如 `M` 代表兆字节、`G` 代表吉字节这样的术语打印大小。这些显然比 1K-blocks 更容易理解。

另一个命令—— `du` ——对于查找目录占用的空间非常有用。例如，输入 `du /etc/X11` 以查看 `/etc/X11` 目录中所有目录的内容。（该目录包含 X Window System 配置文件。）你最终会得到以下结果：

```
12 /etc/X11/Xresources
36 /etc/X11/Xsession.d
272 /etc/X11/app-defaults
20 /etc/X11/cursors
12 /etc/X11/xinit
... lines deleted ...
12 /etc/X11/fonts/misc
8 /etc/X11/fonts/100dpi
8 /etc/X11/fonts/75dpi
8 /etc/X11/fonts/Speedo
8 /etc/X11/fonts/Type1
48 /etc/X11/fonts
2896 /etc/X11
```

每个目录名称前都有一个数字——它告诉你该目录使用的磁盘空间千字节数。因此， `/etc/X11` 目录作为一个整体，使用了 2896KB（或约 2.9MB）的磁盘空间。如果你只想要一个目录（包括该目录中包含的所有文件和子目录）使用的磁盘空间总量，请使用以下 `-s` 选项：

```
du -s /etc/X11
2896 /etc/X11
```

`-s` 选项使 `du` 仅打印整个目录的摘要信息。

正如 `df -h` 以兆字节和吉字节打印磁盘空间信息一样，你可以使用 `du -h` 命令以更易读的形式查看 `du` 的输出。例如，我是如何结合 `-s` 选项来查看我在我的家庭目录（`/home/naba`）中使用的空间的：

```
$ du -sh /home/naba
645M     /home/naba
```

![](img/792720823146d68f19fd50c99ebfce4b_231_0.png)

# 第 4 章：介绍 Linux 应用程序

## 本章内容

- 盘点典型的 Linux 应用程序
- 试用办公应用程序
- 设置数据库
- 玩转多媒体
- 处理图像

每个 Linux 发行版都附带大量应用程序。你只需查看 GUI 桌面中的菜单就能明白我的意思。通常，同一类型的应用程序不止一个。大多数发行版都附带 OpenOffice.org 办公应用程序套件，包括文字处理器、电子表格、演示文稿软件等。你会发现许多 CD 播放器和多媒体播放器的选择，更不用说游戏、实用程序和有用的工具，如扫描仪和数码相机应用程序。一些商业发行版附带商业办公套件，例如 Sun Microsystems 的 StarOffice。

![](img/792720823146d68f19fd50c99ebfce4b_232_0.png)

在播放*多媒体*（各种格式的音频和视频，如 MP3、MPEG、QuickTime）方面，免费可用的 Linux 发行版很少附带合适的解码器，因为其中一些解码器存在许可证限制。最终结果是，多媒体应用程序可以运行，但由于缺乏解码器，它无法播放 MP3 文件或 DVD 电影。商业发行版，如 Xandros 和 SUSE，通常附带这些解码器中的部分。

我将为你概述其中一些 Linux 应用程序。在阅读了这些应用程序的介绍后，你可以进一步探索它们并在需要时使用它们。

## 盘点 Linux 应用程序

表 4-1 按类别列出了主要 Linux 应用程序的抽样。对于主要应用程序，我还展示了一个相关网站，你可以从中获取有关该应用程序的更多信息。这个列表远非全面。每个 Linux 发行版都附带比此表中显示的更多应用程序和实用工具。

如果你的系统同时安装了 GNOME 和 KDE，这些应用程序中的大部分已经可以从任一 GUI 桌面获得。

在本章的后续部分中，我将简要介绍表 4-1 中的一些应用程序，从每个类别中选取一到两个。我在第四册中描述了 Internet 应用程序。

### 表 4-1 Linux 应用程序抽样

| 应用程序 | 描述 |
| :--- | :--- |
| **办公应用程序** |  |
| OpenOffice.org | 免费开源办公套件（兼容 Microsoft Office），包括 Writer 文字处理器、Calc 电子表格、Impress 演示应用程序、Draw 绘图程序和 Math 公式编辑器 (www.openoffice.org) |
| StarOffice | OpenOffice.org 衍生自其中的商业办公套件 (www.sun.com/staroffice) |
| CrossOver Office | 允许你在 Linux 上安装和运行 Microsoft Office 软件的商业办公套件 (www.codeweavers.com/products/office) |
| AbiWord | 类似于 Microsoft Word 的免费文字处理程序 (www.abisource.com) |
| Dia | 绘图程序，设计用于类似 Windows 应用程序 Visio (www.gnome.org/projects/dia) |
| **办公工具** |  |
| Gnome Calculator | GNOME 的简单计算器 |
| KCalc | KDE 的计算器 |
| KOrganizer | KDE 的日历和调度程序 (http://korganizer.kde.org) |
| Kontact | KDE 的个人信息管理套件 (www.kontact.org) |
| Aspell | 文本模式拼写检查器 (http://aspell.sourceforge.net) |
| Dictionary | dict.org 字典服务器的图形客户端，以便你可以查找单词 |
| **文本编辑器** |  |
| emacs | 知名的文本编辑器，具有文本和图形界面 (www.gnu.org/software/emacs) |
| KWrite | KDE 的文本编辑器 |
| Kate | KDE 的高级文本编辑器 |
| vim | 具有文本模式接口并与知名 UNIX 编辑器 vi 兼容的文本编辑器 (www.vim.org) |

## 应用描述表 (续)

| 应用 | 描述 |
|---|---|
| **数据库** |  |
| PostgreSQL | 一个复杂的对象关系型数据库管理系统 (www.postgresql.org)，支持结构化查询语言 (SQL) |
| MySQL | 一个流行的关系型数据库管理系统，支持 SQL (www.mysql.com) |
| **多媒体** |  |
| GNOME CD Player | 音频 CD 播放器（需要可用的声卡） |
| KsCD | 来自 KDE 的音频 CD 播放器（需要可用的声卡） |
| amarok | 多媒体音频播放器 (http://amarok.kde.org)，可播放多种不同的音频格式，包括安装了 MP3 解码器时的 MP3 文件 |
| Rhythmbox | 多媒体音频播放器 (http://rhythmbox.sourceforge.net)，可播放多种不同的音频格式，包括下载相应插件后可播放的 MP3 文件 |
| XMMS | X 多媒体系统：一种多媒体音频播放器 (www.xmms.org)，可播放许多不同的音频格式，包括 MP3 文件。（在某些发行版中，你需要下载插件来播放 MP3。） |
| xine | 免费的媒体播放器 (http://xinehq.de)，可播放 CD、DVD 和视频 CD (VCD)，并且如果你拥有适当的解码器，还可以解码 AVI、MOV、WMV 和 MP3 等多媒体文件 |
| Kaffeine | 基于 xine 的 KDE 媒体播放器，因此 Kaffeine 的功能与 xine 相似 (http://kaffeine.sourceforge.net) |



| Totem | 基于 xine 的 GNOME 电影播放器，因此 Totem 的功能与 xine 相似 (www.gnome.org/projects/totem) |
| cdrao | 一个命令行应用程序，可以根据文本文件中描述的 CD 内容，以光盘一次写入 (DAO) 模式烧录音频或数据 CD-R (http://cdrao.sourceforge.net) |
| cdrecord | 一个命令行应用程序，可以烧录音频和数据 CD-R 以及 DVD-R (http://cdrecord.berlios.de/old/private/cdrecord.html) |
| growisofs | 一个使用 mkisofs 命令将数据追加到用于 CD-R 和 DVD-R 的 ISO 9660 文件系统的命令行应用程序 (http://fy.chalmers.se/~appro/linux/DVD+RW/) |
| X-CD-Roast | cdrecord 和 cdrao 的 GUI 前端，使烧录数据和音频 CD-R 变得容易 (www.xcdroast.org) |
| K3b | 基于 KDE 的 cdrecord、cdrao 和 growisofs 的 GUI 前端，用于烧录 CD-R 和 DVD-R (www.k3b.org) |
| digiKam | 支持 gPhoto 支持的所有数码相机的数码相机和照片管理应用程序 (www.digikam.org) |

![](img/792720823146d68f19fd50c99ebfce4b_234_0.png)

## 应用描述表 (续)

| 应用 | 描述 |
|---|---|
| **图形与图像处理** | |
| The GIMP | GNU 图像操纵程序：适用于照片修饰、图像合成和图像创作等任务的应用程序 (www.gimp.org) |
| GQview | 强大的图像查看器 (http://gqview.sourceforge.net) |
| KFax | KDE 的传真查看器 |
| KView | KDE 的简单图像查看器 |
| GGv | GNOME Ghostview (GGv)，一种 PostScript 文档查看器 (www.gnu.org/directory/print/misc/ggv.html) |
| Xpdf | Adobe PDF 文档查看器 (www.foolabs.com/xpdf/) |
| XSane | 使用 SANE (Scanner Access Now Easy) 库访问扫描仪的图形前端 (www.xsane.org) |
| KSnapshot | 屏幕捕获程序 |
| Kooka | KDE 的使用 SANE 库的扫描仪程序 (www.kde.org/apps/kooka) |
| xscanimage | 控制扫描仪的图形前端 |
| **互联网** | |
| Evolution | 集成电子邮件、日历、联系人管理和在线任务列表的个人信息管理应用程序 (www.novell.com/products/evolution) |
| gFTP | 用于从 Internet 下载文件的图形 FTP 客户端 |
| Gaim | GNOME 即时消息客户端 (http://gaim.sourceforge.net) |
| Kopete | KDE 即时消息客户端 (http://kopete.kde.org) |
| Mozilla | 源自 Netscape 源代码的知名开源 Web 浏览器 (www.mozilla.org) |
| Firefox | Mozilla 项目的新改进版 Web 浏览器 (www.mozilla.org/products/firefox) |
| Thunderbird | Mozilla 项目的电子邮件客户端 (www.mozilla.org/products/thunderbird) |
| Epiphany | 基于 Mozilla 的 GNOME 开源 Web 浏览器 (www.gnome.org/projects/epiphany) |
| Lynx | 文本模式 Web 浏览器 (http://lynx.browser.org) |
| KNode | KDE 的 GUI 新闻阅读器 (http://knode.sourceforge.net) |
| 应用 | 描述 |
|---|---|
| **图形与图像处理** | |
| Pan | GNOME 的 GUI 新闻阅读器 (http://pan.rebelbase.com) |
| Akregator | KDE 的 RSS 源聚合器和阅读器 (http://akregator.sourceforge.net) |
| KPhone | 支持会话初始化协议 (SIP) 的网络电话应用程序 (www.wirlab.net/kphone) |
| Linphone | 支持会话初始化协议 (SIP) 和实时传输协议 (RTP) 的网络电话应用程序 (www.linphone.org) |
| Skype | 用于通过 IP 语音进行语音电话呼叫的网络电话应用程序 (www.skype.com) |
| XChat | 互联网中继聊天 (IRC) 客户端 (www.xchat.org) |
| Konqueror | KDE 中的 Web 浏览器和文件管理器 (www.konqueror.org) |
| KMail | KDE 的电子邮件客户端 (http://kmail.kde.org) |

并非所有 Linux 发行版都包含表 4-1 中显示的所有应用程序，尽管你通常可以在任何发行版中下载并安装所有这些应用程序。表 4-2 列出了本书中各 Linux 发行版——Debian GNU/Linux、Fedora Core、Knoppix、SUSE 和 Xandros——主要应用程序的默认可用性。对勾表示该应用程序默认可用。

### 发行版特定

在安装 Linux 发行版时，通常必须选择特定的应用程序组进行安装。你 Linux 系统上的确切应用程序列表取决于你在安装过程中所做的选择。

### 发行版特定

只要你有宽域网（电缆或 DSL）连接到 Internet，在 Debian（以及基于 Debian 的发行版，如 MEPIS 和 Ubuntu）中安装缺失的应用程序非常容易。例如，要查看 K3b CD/DVD 烧录器是否存在于 Debian 中，我输入 `apt-cache search k3b`。我得到以下输出：

```
k3b - 一个复杂的 KDE cd 烧录应用程序
k3b-i18n - K3b 的国际化 (i18n) 文件
k3billib - KDE cd 烧录应用程序库 - 运行时文件
k3billib-dev - KDE cd 烧录应用程序库 - 开发文件
```

然后，我输入 `apt-get install k3b`，几分钟后我的 Debian 系统上就安装了 K3b。这种容易安装（或升级）软件的特性正是 Debian 用户推崇 `apt-get` 的原因（即使它只是一个命令行工具）。

![](img/792720823146d68f19fd50c99ebfce4b_236_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_236_1.png)

## 表 4-2 部分应用程序的默认可用性

| 应用 | *Debian* | *Fedora* | *Knoppix* | *MEPIS* | *SuSE* | *Ubuntu* | *Kandros* |
|:---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 计算器 - Gcalctool | ✓ | ✓ | | | | ✓ | |
| 计算器 - KCalc | ✓ | | ✓ | ✓ | ✓ | | ✓ |
| CD/DVD 烧录 - K3b | | | ✓ | ✓ | ✓ | | |
| CD 播放器 - GNOME | ✓ | ✓ | | | ✓ | | |
| CD 播放器 - KsCD | ✓ | | ✓ | ✓ | ✓ | | ✓ |
| 数据库 - PostgreSQL | ✓ | | | | | | |
| 数据库 - MySQL | | | ✓ | ✓ | | | |
| 字典 - GNOME 字典 | ✓ | ✓ | | | | ✓ | |
| 字典 - Kdict | ✓ | | | | | ✓ | ✓ |
| 数码相机工具 - digiKam | | | | | ✓ | ✓ | ✓ |
| 绘图程序 - Dia | ✓ | ✓ | | | | | |
| 电子邮件 - KMail | ✓ | | ✓ | | | | ✓ |
| 电子邮件 - Evolution | ✓ | ✓ | | | | ✓ | |
| 电子邮件 - Thunderbird | ✓ | | | | | | ✓ |
| 文件管理器 - Konqueror | | | ✓ | | | | ✓ |



| 文件管理器 - Nautilus (集成 CD 写入器) | ✓ | ✓ | | | | ✓ | |

| 文件管理器 - Kandros 文件管理器 (集成 CD 写入器) | | | | | | | ✓ |

| 图像处理 - ImageMagick | ✓ | ✓ | | ✓ | ✓ | ✓ | ✓ |

| 图像处理 - The GIMP | ✓ | ✓ | | ✓ | ✓ | ✓ | ✓ |

| 即时通讯 - Gaim | ✓ | ✓ | ✓ | ✓ | ✓ | | |

| 即时通讯 - Kopete | ✓ | | | | | | ✓ |

| 互联网中继聊天 - XChat | | ✓ | ✓ | ✓ | ✓ | ✓ | |

| 互联网电话 - KPhone | | | | | | | ✓ |

| 互联网电话 - Linphone | | | | | | ✓ | |

| 互联网电话 - Skye | | | | | ✓ | | ✓ |

| 音乐播放器 - amaroK | | | | | ✓ | | |

表 4-2

| 应用程序 | Debian | Fedora | Knoppix | MEPiS | SUSE | Ubuntu | Kubuntu |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 音乐播放器 - RealPlayer |  |  |  | ✓ | ✓ |  | ✓ |
| 音乐播放器 - Rhythmbox |  | ✓* |  |  |  | ✓* |  |
| 音乐播放器 - XMMS | ✓ |  | ✓ | ✓ |  |  | ✓ |
| 新闻阅读器 - KNode | ✓ |  | ✓ | ✓ | ✓ |  |  |
| 新闻阅读器 - Pan |  |  | ✓ | ✓ |  |  |  |
| 办公套件 - Open Office.org | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PDF 查看器 - Acrobat Reader |  |  | ✓ | ✓ |  |  | ✓ |
| PDF 查看器 - Gpdff | ✓ |  |  |  |  |  |  |
| PDF 查看器 - Kpdf | ✓ |  |  |  |  |  |  |
| PDF 查看器 - Xpdf |  |  | ✓ |  |  | ✓ |  |
| 个人事务管理器 - KOrganizer | ✓ |  | ✓ |  | ✓ |  | ✓ |
| 个人事务管理器 - Kontact | ✓ |  | ✓ | ✓ |  |  | ✓ |
| PostScript 查看器 - GNOME Ghostview (GGv) | ✓ |  |  |  |  | ✓ |  |
| PostScript/PDF 查看器 - KGhostview | ✓ |  | ✓ |  |  |  | ✓ |
| RSS 源阅读器 - Akregator |  | ✓ | ✓ | ✓ | ✓ |  |  |
| 扫描仪 - Kooka | ✓ |  | ✓ | ✓ | ✓ |  | ✓ |
| 扫描仪 - Xsane |  |  | ✓ |  | ✓ |  |  |
| 扫描仪 - xscanimage |  | ✓ | ✓ | ✓ |  |  |  |
| 屏幕截图 - KSnapshot | ✓ |  |  | ✓ | ✓ |  | ✓ |
| 录音机 - GNOME 录音机 | ✓ |  |  |  |  | ✓ |  |
| 录音机 - KDE 录音机 (KRcord) |  |  |  |  | ✓ |  | ✓ |
| 拼写检查 - Aspell |  | ✓ |  |  | ✓ | ✓ |  |
| 网页浏览器 - Epiphany | ✓ |  |  |  |  |  |  |
| 网页浏览器 - Konqueror |  |  | ✓ | ✓ | ✓ | ✓ | ✓ |
| 网页浏览器 - Lynx 文本模式浏览器 |  |  | ✓ |  |  |  |  |
| 网页浏览器 - Mozilla | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

| 应用程序 | Debian | Fedora | Knoppix | MEPiS | SUSE | Ubuntu | Xandros |
|---|---|---|---|---|---|---|---|
| 网页浏览器 - Mozilla Firefox |  | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 文字处理软件 - AbiWord |  | ✓ |  |  |  |  |  |
| 视频播放器 - xine |  |  | ✓ |  | ✓ |  | ✓ |
| 视频播放器 - Kaffeine |  |  | ✓* |  | ✓* |  |  |
| 视频播放器 - Totem | ✓ |  | ✓* |  |  | ✓* |  |

* 需要额外插件

## 办公应用与工具

文字处理软件、电子表格、演示文稿软件、日历、计算器——这些是办公室的常用工具。大多数 Linux 发行版都随附 OpenOffice.org（通常缩写为 OO.o 或 Ooo）办公应用和工具套件。你可以逐一尝试它们，看看哪个最合你的心意。每个应用程序的使用都相当直观。尽管用户界面的一些细节可能对你来说是新的，但在用几次之后，你就会熟悉它们。本部分简要介绍了以下几个应用程序：

- **OpenOffice.org 办公套件**：类似 Microsoft Office 的办公套件，包含 Writer 文字处理器、Calc 电子表格程序、Impress 演示文稿程序、Draw 绘图和插图应用，以及 Math 数学公式编辑器
- **Kontact**：KDE 环境下的个人信息管理应用
- **计算器**：GNOME 计算器及 KDE 计算器
- **Aspell**：拼写检查工具
- **更多**：Linux 上可商用的办公应用

### OpenOffice.org 办公套件

OpenOffice.org 是由 OpenOffice.org 项目（www.openoffice.org）开发的办公套件。OpenOffice.org 与 Microsoft Office 等主要办公套件类似。其主要组件包括 Writer 文字处理器、Calc 电子表格和 Impress 演示文稿程序。

你可以轻松启动 OpenOffice.org——无论是整个套件还是单独的应用程序——在大多数 GUI 桌面环境中，只需点击面板图标或从主菜单中选择即可。例如，在 SUSE 中，你可以点击桌面图标来打开 OpenOffice.org 套件的初始窗口。你可以从 OpenOffice.org 的主窗口创建新的 OpenOffice 文档或打开现有文档（也可以是 Microsoft Office 文件）。

下文将简要介绍 Writer、Calc 和 Impress。

### Writer

从任意 OpenOffice.org 窗口选择“文件” → “新建” → “文本文档”，即可启动 OpenOffice.org Writer，并在其主窗口中打开一个空白文档。使用 Writer 很简单——它与其他文字处理器如 Microsoft Word 类似。例如，你可以向空白文档中输入文本、格式化文本，并在完成后保存。

你还可以打开你在 Windows 机器上使用 Microsoft Word 准备的文档。图 4-1 展示了在 OpenOffice.org Writer 中打开 Microsoft Word 文档的场景。

![](img/792720823146d68f19fd50c99ebfce4b_240_0.png)

保存文档时，默认情况下，Writer 会将文档保存为 OpenDocument 文本格式，文件扩展名为 `.odt`。

![](img/792720823146d68f19fd50c99ebfce4b_241_0.png)

OpenOffice.org 2.0 版本及更高版本默认使用标准的 OASIS Open Document XML 格式作为默认文件格式（文件扩展名为 `.odt`）。OASIS OpenDocument 格式并不隶属于任何特定厂商或特定的办公套件软件。有关 OpenDocument 格式的更多信息，请参见 `http://www.oasis-open.org/committees/tc_home.php?wg_abrev=office`

![](img/792720823146d68f19fd50c99ebfce4b_241_1.png)



如果你需要与他人共享 OpenOffice.org Writer 文档（例如使用 Microsoft Word 的用户），可以将文档保存为多种格式，包括 Microsoft Word 6.0/95/97/2000/XP 和富文本格式（`.rtf`）。Microsoft Word 可以打开 `.rtf` 文件。如果要与使用 OpenOffice.org 2.0 之前版本的用户交换文件，请将文件保存为带有 `.otx` 扩展名的 StarOffice 文本文档格式。

我不打算详细解释如何使用 Writer，因为它简单且直观。如果有需要，可以查看在线帮助。从 Writer 菜单中选择“帮助” → “帮助内容”，这会弹出 OpenOffice.org 帮助窗口，其中包含有关 Writer 的帮助信息。然后，你可以点击链接查看具体的帮助内容。

## Calc

Calc 是 OpenOffice.org 应用程序套件中的电子表格程序。要启动 Calc，请在主菜单的 Office 类别中选择“电子表格”，或从任意 OpenOffice.org 窗口选择“文件” → “新建” → “电子表格”。Calc 会显示其主窗口，其外观与基于 Windows 的电子表格（如 Microsoft Excel）相似。（实际上，Calc 可以读写 Microsoft Excel 格式的电子表格文件。）

使用 Calc 的方式与使用 Microsoft Excel 相同。你可以在单元格中输入条目、使用公式以及对单元格进行格式化。（例如，你可以指定值的类型和小数点后的位数。）图 4-2 展示了 Calc 中一个典型的电子表格。

![](img/792720823146d68f19fd50c99ebfce4b_241_2.png)

![](img/792720823146d68f19fd50c99ebfce4b_241_3.png)

在制作电子表格时，使用你在 Microsoft Excel 中常用的公式。例如，使用公式 `SUM(D2:D6)` 可以计算从单元格 D2 到 D6 的总和。要将单元格 D2 设置为条目 A2 和 C2 的乘积，请在单元格 D2 中输入 `=A2*C2`。要了解 OpenOffice.org Calc 中可用功能的更多信息，请从菜单中选择“帮助” → “内容”。这将打开 OpenOffice.org 帮助窗口，你可以按类别浏览功能并点击某个功能以阅读更多详细信息。

要保存电子表格，请选择“文件” → “另存为”。此时会出现一个对话框，你可以从中指定文件格式、目录位置和文件名。OpenOffice.org Calc 可以将文件保存为多种格式，包括 Microsoft Excel 5.0/95/97/2000/XP 以及带逗号分隔值（CSV）的文本文件。

如果你想要与 Microsoft Excel 用户交换文件，请将电子表格保存为 Microsoft Excel 格式（选择合适版本的 Excel）。然后，你可以将该文件传输到 Windows 系统并在 Microsoft Excel 中打开它。

## Impress

Impress 与 Microsoft PowerPoint 类似。你可以使用 Impress 制作简报包（幻灯片演示文稿）。要运行 Impress，请在主菜单的 Office 类别中选择“演示文稿”，或从任意 OpenOffice.org 窗口选择“文件” → “新建” → “演示文稿”。

首次启动时，Impress 会询问你演示文稿的样式和模板。若要开始工作，请选择“空白演示文稿”并点击“创建”。若要打开现有文档，请在演示文稿向导中选择相应的选项并点击“打开”。然后选择你要打开的演示文稿文件。你可以在 Impress 中打开 Microsoft PowerPoint 文件。

图 4-3 展示了 Impress 中一个典型的幻灯片演示文稿。

Impress 窗口显示第一张幻灯片，左侧显示幻灯片的视图大纲。具体外观取决于你选择的文档类型和模板。你可以开始向幻灯片添加文本和其他图形对象，如图像、文本和线条。

要插入新幻灯片，请从菜单中选择“插入” → “幻灯片”。此时会出现一张空白幻灯片。然后，你可以向该新幻灯片添加文本和图形。

要保存演示文稿，请选择“文件” → “保存”。对于新文档，你需要提供文件名并选择要保存文件的目录。

### 图 4-3：

你可以在 OpenOffice.org Impress 中准备简报包。

![](img/792720823146d68f19fd50c99ebfce4b_243_0.png)

如果你想将幻灯片分享给使用 Microsoft PowerPoint 的人，请将演示文稿保存为 Microsoft PowerPoint 97/2000/XP 格式。

## 日历

KDE 自带 Kontact —— 这是一个集成的图形化个人信息管理器，它整合了现有的 KDE 应用程序，如 Kmail 邮件阅读器和 KOrganizer 日历程序。你可以从面板图标或主菜单启动 Kontact。（菜单条目的具体位置取决于 Linux 发行版。）

Kontact 启动时，通常显示 Kmail 应用程序。不过，你可以点击 Kontact 窗口左侧窗格中的图标切换到其他视图（见图 4-4）。例如，图 4-4 显示的是你点击日历图标后的 Kontact 窗口。在这种情况下，Kontact 显示 KOrganizer —— 即 KDE 日历程序 —— 的输出。KOrganizer 程序显示一个日历视图，你可以点击日期来设置或查看当天的日程安排。图 4-4 展示了一个典型的日历。

![](img/792720823146d68f19fd50c99ebfce4b_244_0.png)

要为特定的日期和时间添加事件或预约，请从日历中选择日期，双击时间，然后在出现的“新建事件”对话框中输入预约的简要描述。完成后点击`确定`。添加完所有事件和预约后，选择 `文件` → `保存` 来保存日历。

## 计算器

你可以选择 GNOME 计算器或 KDE 计算器。它们都是科学计算器，你可以进行典型的科学计算，如平方根和倒数，以及三角函数，如正弦、余弦和正切。

要使用计算器，请在主菜单的`实用工具`或`附件`类别中寻找。图 4-5 显示了 SUSE 中的 KDE 计算器。

![](img/792720823146d68f19fd50c99ebfce4b_244_1.png)

通过从“设置”菜单中选择选项，你可以显示额外的按钮。例如，选择“设置 → 三角函数按钮”可以显示用于执行三角函数计算的按钮。

## 适用于 Linux 的商业办公应用程序

由于办公应用程序对许多企业和个人都很重要，我将简要介绍一些适用于 Linux 的商业办公应用程序。这些商业产品包括 Applixware Office 和 StarOffice。这些产品需要付费，但成本通常低于 Microsoft Office —— 后者是 Windows 上领先的办公应用套件。（如果你不知道的话，Microsoft Office 是几个应用程序的集合：用于文字处理的 Microsoft Word、用于电子表格的 Microsoft Excel、用于演示文稿图形的 Microsoft PowerPoint，以及用于数据库的 Microsoft Access。）

另一个适用于 Linux 的商业产品是 CodeWeavers 的 CrossOver Office。使用 CrossOver Office，你可以在 Linux 和 X 窗口系统下运行你现有的 Microsoft Office 应用程序（如 Word、Excel 和 PowerPoint）。

> **记住** 本书的配套 DVD-ROM 不包含这些适用于 Linux 的商业办公应用程序，但我将在接下来的几个部分中简要描述它们。你可以访问每个厂商的网站以获取更多关于这些产品的信息。

## Applixware Office

www.vistasource.com

Applixware 是一个适用于所有 Linux 发行版的办公应用套件。2000 年 4 月，Applix, Inc. 成立了一个独立的团体 —— VistaSource, Inc. —— 专门专注于 Linux 应用程序。Applixware 是一组集成模块，包括一个文字处理器、一个能够操作实时数据的电子表格、一个可编程的矢量图形工具，以及用于访问数据库的数据库接口。Applixware 模块可以读写 Microsoft Office 格式以及多种其他文件格式的文档。

## StarOffice

www.sun.com/staroffice

StarOffice 是另一个商业办公应用程序套件；它由德国汉堡的 StarDivision 创建，并于 1999 年被 Sun Microsystems 收购。StarOffice 是一个跨平台解决方案 —— 它运行在 Linux、Windows 95/98/Me/NT/2000/XP、Sun Solaris x86 和 Sun Solaris x86 上。此外，StarOffice 提供多种语言版本：英语、法语、德语、西班牙语、意大利语和瑞典语。

以下是 StarOffice 7 包含的内容：



- StarOffice Writer 用于文字处理（兼容 Microsoft Word）
- StarOffice Calc 用于电子表格（兼容 Microsoft Excel）
- StarOffice Impress 用于演示文稿（兼容 Microsoft PowerPoint）
- StarOffice Draw 用于矢量图形绘制
- StarOffice Base 用于数据管理

![](img/792720823146d68f19fd50c99ebfce4b_246_0.png)

2000 年 10 月，Sun 在开源许可证下发布了 StarOffice 的源代码。Sun 支持的开源项目 OpenOffice.org 于 2002 年 5 月发布了 OpenOffice.org 1.0 办公生产力套件。当前的 Linux 发行版通常附带 OpenOffice.org 2.0 或更高版本。要了解有关 OpenOffice.org 的更多信息，请访问 [www.openoffice.org](http://www.openoffice.org)。

![](img/792720823146d68f19fd50c99ebfce4b_246_1.png)

Xandros 的商业版本附带 StarOffice 7。查找你可以点击以启动 StarOffice 的桌面图标。Xandros 还包含 OpenOffice.org。

![](img/792720823146d68f19fd50c99ebfce4b_246_2.png)

## CrossOver Office

www.codeweavers.com/products/cxoffice

很有可能你的电脑上安装了 Windows 和 Microsoft Office。当你决定在这台电脑上运行 Linux 时，你可以继续从 GNOME 或 KDE 桌面运行大多数 Microsoft Office 应用程序。在 Linux 中运行 Microsoft Office 的便利性来自于一个名为 CrossOver Office 的商业产品。

来自 CodeWeavers 的 CrossOver Office 是一个软件包，它允许你在 Linux 中安装你的 Microsoft Office 应用程序（包括 Office 97、Office 2000 和 Office XP 等所有版本的 Office）。你不需要 Microsoft Windows 来运行 CrossOver Office 中的 Office 应用程序。你只需安装 CrossOver Office，然后从 CD-ROM 安装 Microsoft Office（以及其他许多 Windows 应用程序，如 Adobe Photoshop 和 Quicken）。安装完 Microsoft Office 后，Office 应用程序可以直接从 GNOME 或 KDE 桌面访问。

CrossOver Office 使用 Wine —— 一个基于 X 窗口系统实现的 Windows Win32 和 Win16 应用程序编程接口（API）的开源实现，旨在在 UNIX 和 Linux 系统上运行。Wine 包括 Wine 加载器和 WineLib。Wine 加载器可以加载并运行 Windows 应用程序。WineLib 用于在 Linux 中编译和链接 Windows 应用程序。Wine 可以从 [www.winehq.com](http://www.winehq.com) 免费获取。

## 办公应用程序和工具

CodeWeavers 通过使用 Wine 的定制版本创建了 CrossOver Office，以确保 Microsoft Office 应用程序（特别是 Microsoft Word、Excel 和 PowerPoint）在 Wine 上正确运行。CodeWeavers 对 CrossOver Office 收取名义上的费用 —— CrossOver Office 标准版的建议零售价为 39.95 美元，专业版为 74.95 美元。然而，对 Wine 的所有代码更改和改进都会返还给 Wine 项目。因此，Wine 开源项目受益于 CrossOver Office 的销售。

![](img/792720823146d68f19fd50c99ebfce4b_247_0.png)

Xandros 的商业版本附带 CrossOver Office。你需要先运行 CrossOver Office 设置程序，然后从原始 CD 安装 Microsoft Office，之后才能开始使用 Microsoft Office 应用程序。在安装过程中，你必须输入 Microsoft Office 的产品密钥，就像在 Windows 安装中一样。

### Aspell 拼写检查器

Aspell 实用工具是一个交互式拼写检查器。你可以使用它来检查文本文件中单词的拼写。为此，只需在终端窗口中键入以下命令：

```
aspell check `filename`
```

如果你想试用 Aspell，请键入一些笔记并将它们保存为名为 `notes.txt` 的文本文件。（文件名可以是任何内容，但我在本节中使用此文件名。）要对该文件运行拼写检查器，请在终端窗口中键入以下命令：

```
aspell check notes.txt
```

以下是 Aspell 显示的内容：

```
This note describes the `concensus` reached during the
August 16 meeting.
```

- 1) concensus         6) consensual
- 2) con census        7) conciscences
- 3) con-census        8) incenses
- 4) condenses         9) consenses's
- 5) concer ns         0) consensuses
- i) 忽略           I) 忽略所有
- r) 替换          R) 替换所有
- a) 添加              x) 退出
- ?

当 Aspell 发现拼写错误的单词（任何未出现在其词典中的单词）时，它会显示包含该拼写错误单词（`concensus`）的句子，并通过在一对星号之间包围该单词来突出显示它。在下面

在句子处，Aspell 会列出可能的修正建议，并从 1 开始按顺序编号。在这种情况下，Aspell 将 `concensus` 的正确拼写 `consensus` 列为第一个修正建议。

句子结束后，Aspell 会显示一个包含 16 个选项的列表——其中十个选项编号为 0 到 9，另外六个选项标记为单个字母 I、X、A、i、R 和 x——后面跟着一个问号提示。你必须按下列出的数字或字母之一来指示希望 Aspell 执行的操作。编号选项显示了对拼写错误单词的十种可能替换词。以下是字母选项的含义：

- i 表示忽略该拼写错误。
- I 表示忽略该单词的所有出现。
- x 表示替换当前出现。 (按 x 后，你需要输入一个替换词。)
- R 表示替换所有出现。 (按 R 后，你需要输入一个替换词。)
- a 表示接受该单词并将其添加到你的私人词典中。
- X 表示保存文件的其余部分并退出，忽略拼写错误。

注意：原文列出了“i, x, a, i, R, and x”。根据标准的 Aspell 文档和提供的描述，这些字母很可能是 `i`（忽略）、`I`（忽略所有）、`x`（替换）、`R`（替换所有）、`a`（添加/接受）和 `X`（退出）。然而，查看描述“Space 表示接受该单词这一次”，那里可能缺少一个用于空格键（在类似环境中通常是 `y` 或 `s`，但 Aspell 使用特定的键）的选项。让我们仔细查看 OCR 文本：“标记为单个字母 i, x, a, i, R, and x”。这看起来像是 OCR 错误，将 `I`（大写 i）误读为 `i`（小写 i），将 `X`（大写 x）误读为 `x`（小写 x）。此外，OCR 中的第一个项目符号是“+ * 空格表示接受该单词这一次”。这表明有一个空格键选项。标准的 Aspell 选项是：

`i` 忽略

`I` 忽略所有

`x` 替换

`R` 替换所有

`a` 添加到个人词典

`X` 退出

`s` 保存（有时）

`?` 帮助

OCR 文本说：“其中十个编号为 0 到 9，六个标记为单个字母 i, x, a, i, R, and x”。

提供的描述列表是：

1. 空格表示接受该单词这一次。（这很不寻常，通常是 'y' 或 's' 或者只是按回车？不，Aspell 使用特定的键。假设 OCR 指的是 's' 或类似的，但文本说的是“空格”。我会尝试将列表更正以匹配标准的 Aspell 行为，但指示是更正明显的 OCR 错误。描述列表中重复的 'i' 和 'x' “i, x, a, i, R, and x” 强烈暗示应该是 `I` 和 `X`。

让我们根据提供的文本格式化列表，更正大小写错误：

- 空格表示接受该单词这一次。
- i 表示忽略该拼写错误。



- `I` 表示忽略该单词的所有出现。
- `x` 表示替换当前出现。 (按 `x` 后，你需要输入一个替换词。)
- `R` 表示替换所有出现。 (按 `R` 后，你需要输入一个替换词。)
- `a` 表示接受该单词并将其添加到你的私人词典中。
- `X` 表示保存文件的其余部分并退出，忽略拼写错误。

这些选项对大小写敏感。请确保没有开启大写锁定。

## 数据库

Linux 发行版通常附带两种常见的关系型数据库之一——PostgreSQL 和 MySQL。

PostgreSQL（发音为 POST-gres-cue-ee）是一个强大且流行的关系型数据库（关系型数据库是以相互连接的表集合形式工作的数据库类型）。你可以使用结构化查询语言 (SQL) 来操作该数据库。PostgreSQL 由一个开发团队开发，并遵循 BSD（伯克利软件发行版）开源许可证分发。该许可证对 PostgreSQL 源代码的使用方式没有限制。要了解 PostgreSQL 的最新开发动态，请访问 www.postgresql.org。

MySQL（发音为 My ESS-cue-ee）是另一个流行的关系型数据库。你可以使用 SQL 来操作 MySQL 数据库。一家名为 MySQL AB 的瑞典公司开发了 MySQL (www.mysql.com)。

![](img/792720823146d68f19fd50c99ebfce4b_249_0.png)

我简要展示了如何在 Fedora 上使用 MySQL。顺便说一下，如果你在 Debian 中看不到 MySQL，请 `root` 身份登录，并在终端窗口中输入 `apt-get install mysql-admin mysql-client mysql-common mysqlserver`。

要使用 MySQL，你必须首先以 `root` 身份登录，并使用以下命令启动数据库服务器：

```sql
/etc/init.d/mysqld start
```

数据库服务器 `mysqld` 是一个 `守护进程`（一个持续运行的后台进程），它接受来自 MySQL 监控器的数据库查询。现在你需要设计一个数据库，在 MySQL 中创建该数据库，并为其加载数据。

## 回顾构建数据库的步骤

使用以下基本步骤序列来构建数据库：

1. **设计数据库。**

   这涉及定义用于存储信息的表和属性。

2. **创建一个空数据库。**

   在添加表之前，数据库系统要求你构建一个空数据库。

3. **在数据库中创建表。**

   在这一步中，你使用 SQL 的 `CREATE TABLE` 语句来定义表。

4. **向表中加载固定数据。**

   例如，如果你有一张制造商名称或出版商名称的表（就书籍而言），你可能希望用已知信息加载该表。

5. **备份初始数据库。**

   如果需要从零开始创建数据库，这一步是必要的。

6. **向表中加载数据。**

   你可以从数据库的早期转储中加载数据，或者通过表单交互进行加载。

7. **通过查询使用数据库。**

   使用 SQL 命令进行查询、更新记录或插入新记录。

为了演示如何创建和加载数据库，我设置了一个简单的书籍目录数据库作为示例。

### 设计数据库

在我的书籍目录示例中，我不遵循数据库构建的所有步骤。对于该示例，数据库设计步骤将非常简单，因为我的书籍目录数据库只包含一个表。该表的属性如下：

- 书籍标题，最多 50 个字符
- 第一作者姓名，最多 20 个字符
- 第二作者姓名（如果有），最多 20 个字符
- 出版商名称，最多 30 个字符
- 页数，作为数字
- 出版年份，作为数字（例如 2005）
- 国际标准书号 (ISBN)，作为 10 个字符的文本（例如 0471752622）

我存储的 ISBN 不包含典型 ISBN 中嵌入的破折号。我还将 ISBN 用作表的主键，因为 ISBN 是书籍的全球标识系统。这意味着每个书籍条目必须有一个唯一的 ISBN，因为所有书籍都有唯一的 ISBN。

### 创建空数据库

要在 MySQL 中创建空数据库，请使用 `mysqladmin` 程序。例如，要创建一个名为 `books` 的空数据库，我输入以下命令：

```
mysqladmin create books
```

你必须以 `root` 身份登录才能运行 `mysqladmin` 程序。顾名思义，`mysqladmin` 是 MySQL 的数据库管理程序。

除了创建数据库外，你还使用 `mysqladmin` 来删除数据库、关闭数据库服务器或检查 MySQL 版本。例如，要查看版本信息，输入以下命令：

```
mysqladmin version
```

### 使用 MySQL 监控器

创建空数据库后，你与数据库的所有交互都是通过 `mysql` 程序——作为数据库服务器客户端的 MySQL 监控器——进行的。你需要运行 `mysql` 并将数据库名称作为参数。然后 `mysql` 程序会提示你输入。

以下是我输入的用于启动 `mysql` 程序并打开 `books` 数据库的命令：

```
mysql books
```

在显示其版本号和一些状态信息后，`mysql` 程序会提示你输入，如下所示：

```
mysql>
```

然后你可以在提示符处输入 `mysql` 命令。在创建表或向表中加载数据时，典型的方法是将 SQL 语句（以及诸如 `\G` 等 `mysql` 命令）放在一个文件中，然后运行 `mysql` 并将标准输入重定向到该文件。例如，假设一个名为 `sample.sql` 的文件包含你想在名为 `books` 的数据库上尝试的一些 SQL 命令。那么，你应该使用以下命令运行 `mysql`：

```
mysql books < sample.sql
```

我以这种方式使用 `mysql` 来创建数据库表。

### 定义表

要创建一个名为 `books` 的表，我编辑了一个名为 `makedb.sql` 的文本文件，并在该文件中放置了以下行：

```
# Table structure for table 'books'
# CREATE TABLE books (
 isbn CHAR(10) NOT NULL PRIMARY KEY,
 title CHAR(50),
 author1 CHAR(20),
 author2 CHAR(20),
 pubname CHAR(30),
 pubyear INT,
 pagecount INT
 ) \G
```

`CREATE TABLE books` 是一个创建名为 `books` 的表的 SQL 语句。语句末尾的 `\G` 是一个 `mysql` 命令。表的属性出现在括号包围的行中。

如果表包含固定数据，你还可以包含其他 SQL 语句（如 `INSERT INTO`）来在创建表后立即将数据加载到表中。

为了执行 `makedb.sql` 文件中的 SQL 语句以创建 `books` 表，我按如下方式运行 `mysql`：

```
mysql books < makedb.sql
```

现在 `books` 数据库中有一个名为 `books` 的表。（好吧，也许我应该给它们取不同的名字，但将它们称为相同的名字似乎很方便。）我现在可以开始向表中加载数据了。

### 向表中加载数据

向表中加载数据的一种方法是在另一个文件中准备 SQL 语句，然后以该文件作为输入运行 `mysql`。例如，假设我想将以下书籍信息添加到 `books` 表中：

```
isbn = '0764596152' 
title = 'SUSE Linux 9.3 For Dummies' 
author1 = 'Naba Barkakati' 
author2 = NULL 
publisher = 'Wiley' 
pubyear = 2005 
pagecount = 384
```

那么，以下 MySQL 语句将此信息加载到 `books` 表中：

```
INSERT INTO books VALUES
( '0764596152', 'SUSE Linux 9.3 For Dummies',
'Naba Barkakati', NULL, 'Wiley', 2005, 384) \G
```

另一方面，假设你拥有的字段顺序不同——一种你可以使用 `CREATE TABLE` 语句定义的顺序。在这种情况下，你可以使用 `INSERT INTO` 命令的不同形式来按正确顺序添加行，如下例所示：

```
INSERT INTO books (pubyear, author1, author2, title, pagecount, publisher, isbn) values
(2005, 'Naba Barkakati', NULL, 'SUSE Linux 9.3 For Dummies', 384, 'Wiley', '0764596152')\G
```

本质上，你必须指定属性列表以及值，并确保属性的顺序与值的顺序匹配。

如果我将所有的 `INSERT INTO` 命令保存在名为 `additems.sql` 的文件中，我可以使用 `source` 命令从 `mysql` 命令行加载数据库，方法如下。（输入 `mysql books` 以启动 SQL 客户端。）



```
mysql> source additems.sql
```

## 查询数据库

你可以通过 `mysql` 监控器交互式地查询数据库。要做到这一点，你需要了解 SQL。例如，要查询 `books` 数据库，我使用以下命令启动 SQL 客户端：

```
mysql books
```

然后，我在 `mysql>` 提示符下输入 SQL 命令来查找数据库中的项目。完成后，我输入 `quit` 退出 `mysql` 程序。下面是一个示例。（我这些操作都是在终端窗口中输入的。）

```
mysql> select title from books where pubyear < 2006 \g
+------------------------------------------------------------------+
| title                                                            |
+------------------------------------------------------------------+
| SUSE Linux 9.3 For Dummies                                       |
| Linux All-in-One Desk Reference For Dummies                      |
+------------------------------------------------------------------+
2 rows in set (0.06 sec)
mysql> quit
Bye
```

## 多媒体应用程序

大多数 Linux 发行版都包含相当多的多媒体应用程序——主要是多媒体音频播放器和 CD 播放器，但也包括用于使用数码相机和烧录 CD-ROM 的应用程序。要播放其他多媒体文件（如 MPEG 视频），你可能需要在你的 Linux 系统上下载并安装额外的软件。以下是几个典型多媒体任务及可用于执行这些任务的应用程序的简要概述：

- **使用数码相机：** 使用数码相机工具从你的数码相机中下载照片（在 Linux 中，或者将相机简单地作为 USB 大容量存储设备访问）。
- **播放音频 CD：** 使用随 Linux 提供的众多音频 CD 播放器之一。
- **播放声音文件：** 使用 `Rhythmbox` 或 `XMMS` 多媒体音频播放器。（你需要下载一些额外的软件才能在 `Rhythmbox` 或 `XMMS` 中播放 MP3 文件。）你也可以从互联网上下载其他播放器。
- **烧录 CD：** 使用 CD 烧录工具（如 `K3b`）来烧录音频和数据 CD。

### 使用数码相机

大多数 Linux 发行版都附带一个数码相机应用程序，你可以使用它从数码相机下载图片。例如，`MEPIS`、`SUSE` 和 `Xandros` 附带 `digiKam`，它适用于许多不同品牌和型号的数码相机。根据型号不同，相机可以连接到串行端口或通用串行总线（USB）端口。

要使用 `digiKam` 配合你的数码相机，请按照以下步骤操作：

1. **将你的数码相机连接到串行端口或 USB 端口**（无论相机支持哪种接口），并**打开相机电源。**

   在主菜单的图形或图像部分查找它。

2. **启动 `digiKam`。**

   在 `digiKam` 菜单中，选择“设置”->“配置 digiKam”。

   会出现一个配置对话框。

3. **在对话框中点击“相机”选项卡，然后点击“自动检测”。**

   如果你的相机受支持且配置为 PTP（图片传输协议）模式，则会检测到该相机。如果没有，你可以使用我在这些步骤之后描述的替代方法从相机中获取照片。

4. **从“相机”菜单中选择你的相机型号。**

   会出现一个新窗口，稍后片刻，它会显示相机中的照片。

5. **点击缩略图以选择要下载的图片；然后选择“相机”->“下载”以下载图片。**

   `digiKam` 随后会下载这些图片。你可以将文件保存到文件夹中，并使用 `The GIMP` 或你喜欢的照片编辑器编辑照片。

如果 `digiKam` 无法识别你的数码相机，请不要绝望。只要你的相机支持 USB 大容量存储，你仍然可以将数码相机的存储介质（例如紧凑型闪存卡）作为 USB 大容量存储设备进行访问。要访问 USB 数码相机上的图片，请使用以下步骤。（我在 `SUSE Linux` 上测试了这些步骤，但它们在大多数 Linux 发行版上应该也能正常工作。）

![](img/792720823146d68f19fd50c99ebfce4b_254_0.png)

1. **阅读相机手册，并使用相机的菜单选项将 USB 模式设置为“大容量存储”（Mass Storage）。**

   如果相机不支持 USB 大容量存储，则无法使用此过程访问照片。如果相机支持图片传输协议模式，你可以使用 `digiKam` 下载图片。

2. **使用随相机附带的电缆将数码相机连接到 USB 端口，然后打开相机电源。**

   这将使 Linux 检测到相机，并在文件管理器窗口中打开相机的内容（见图 4-6）。

![](img/792720823146d68f19fd50c99ebfce4b_255_0.png)

3. **点击选择照片，并通过拖放将它们到选定的文件夹中，将其复制到你的硬盘上。**

4. **关闭文件管理器窗口，从 PC 断开 USB 电缆，并关闭相机。**

当你可以像访问其他任何存储设备一样访问相机时，谁还需要数码相机工具呢！

### 播放音频 CD

所有 Linux 发行版都附带 GNOME 或 KDE CD 播放器应用程序。要播放音频 CD，你需要一块声卡，并且该声卡必须配置为在 Linux 中工作。

在某些发行版中，你可以将音频 CD 插入驱动器，会出现一个对话框询问你是否希望使用 CD 播放器播放该 CD。例如，图 4-7 显示了 `SUSE Linux` 中 KDE CD 播放器（`Kscd`）正在播放音频 CD 中的一首曲目。

![](img/792720823146d68f19fd50c99ebfce4b_256_0.png)

**图 4-7：** 使用 KDE CD 播放器播放音频 CD。

KDE CD 播放器显示 CD 的标题和当前曲目的名称。CD 播放器从 `http://freedb.org` 获取歌曲标题——这是互联网上一个免费的、开源的 CD 数据库（端口 888 上的 `freedb.freedb.org`）。CD 播放器需要活动的互联网连接才能从 CD 数据库下载歌曲信息。在 CD 播放器下载了关于特定 CD 的信息后，它会将这些信息缓存到本地数据库中供以后使用。CD 播放器的用户界面直观易用，你可以轻松上手。一个很好的功能是你可以按标题选择曲目。

### 播放声音文件

你可以使用 `Rhythmbox` 或 `XMMS` 来打开和播放声音文件（例如，MP3 文件）。拥有大型 MP3 音乐库的用户喜欢 `Rhythmbox`，因为它有助于整理音乐文件。你可以在多个发行版（包括 Debian 和 Fedora Core）中通过从主菜单选择音乐播放器应用程序来启动 `Rhythmbox`。当你首次启动 `Rhythmbox` 时，它会显示一个助手提示你（见图 4-8）输入音乐文件的位置，以便 `Rhythmbox` 可以管理你的音乐库。

![](img/792720823146d68f19fd50c99ebfce4b_256_1.png)

**图 4-8：** `Rhythmbox` 可以管理你的音乐库。

确定音乐文件位置后，`Rhythmbox` 启动并以有组织的方式显示库。然后你可以选择音乐并播放，如图 4-9 所示。（在这里，你看到 `Rhythmbox` 正在 Debian 上运行。）

![](img/792720823146d68f19fd50c99ebfce4b_257_0.png)

**图 4-9：** 你可以在 `Rhythmbox` 中从你的库播放音乐。

`XMMS` 是另一种可以播放多种类型声音文件的音乐播放器，包括 Ogg Vorbis、`FLAC`（Free Lossless Audio Codec，一种与 MP3 类似的音频文件格式）和 Windows WAV。

你可以通过从主菜单选择音频播放器应用程序来启动 `XMMS`（在“多媒体”或“声音与视频”下查找）。`XMMS` 启动后，你可以通过选择“窗口菜单”>“播放文件”或按 L 键来打开一个声音文件（例如 MP3 文件）。然后从“加载文件”对话框中选择一个或多个音乐文件。点击“播放”按钮，`XMMS` 开始播放声音文件。图 4-10 显示了 `XMMS` 窗口（在 `SUSE Linux` 中）正在播放声音文件时的状态。

![](img/792720823146d68f19fd50c99ebfce4b_257_1.png)

**图 4-10：** 你可以在 `XMMS` 中播放许多不同类型的声音文件。



在一些免费 Linux 发行版中，你可能无法播放 MP3 文件，因为其中未包含 MP3 解码器。不过，在 Debian、Knoppix、SUSE 和 Xandros 中，MP3 播放功能运行正常。由于法律原因，Fedora Core 中的 Rhythmbox 和 XMMS 版本不包含播放 MP3 文件所需的代码，因此在你播放之前，必须以某种方式将 MP3 转换为受支持的格式，例如 WAV。不过，你可以下载 Rhythmbox 和 XMMS 的源代码，并构建支持 MP3 的应用程序。你还可以使用 Ogg Vorbis 格式作为压缩音频文件格式，因为 Ogg Vorbis 是一种无专利和版税的格式。

## 刻录 CD

如今，图形用户界面（GUI）文件管理器通常具备刻录 CD 的功能。例如，Nautilus 和 Xandros 文件管理器内置了刻录 CD 的功能。Linux 发行版还附带独立的 GUI 程序，使你能够轻松地刻录 CD 和 DVD。例如，`K3b` 是 KDE 中一款流行的 CD/DVD 刻录应用程序，在 Knoppix 和 SUSE 中可用。

大多数 CD 刻录应用程序都易于使用。你基本上只需收集想要刻录到 CD 或 DVD 上的文件，然后启动刻录过程。当然，要让这起作用，你的 PC 必须安装了 CD 或 DVD 刻录机。

图 4-11 展示了 SUSE Linux 中 `K3b` CD/DVD 刻录应用程序的初始窗口。`K3b` 窗口的上半部分用于浏览文件系统以选择要刻录到 CD 或 DVD 上的内容。左上角显示了已安装的 CD 写入设备；在此示例中，它是一个 DVD/CD-RW 驱动器，因此该驱动器可以读取 DVD 和 CD，但只能刻录 CD。

![](img/792720823146d68f19fd50c99ebfce4b_258_0.png)

要刻录 CD，你从 `K3b` 窗口下半部分显示的项目之一开始——例如，新建音频 CD 项目，或新建数据 DVD 项目。然后你必须添加文件，最后通过选择“项目”→“刻录”或按 `Ctrl+B` 将项目刻录到 CD 或 DVD 上。对于音频 CD，你还可以拖放 MP3 文件和音频轨道。

`K3b` 需要外部命令行程序 `cdrecord` 和 `cdrdao` 来刻录 CD。`K3b` 还需要 `growisofs` 程序来刻录 DVD。

如果在 Debian 中遇到关于缺少 `cdrdao` 的错误，请确保你的 Debian 系统已连接到互联网，然后输入 `apt-get install cdrdao` 进行安装。

## 图形与图像

你可以使用图形和图像处理应用程序来处理图像和图形（线条画和形状）。我讨论了两个应用程序：

- `GIMP`（GNU 图像处理程序）是一个用于查看和执行图像操作任务（如照片修图、图像合成和图像创建）的程序。
- `GNOME GHOSTview`（GGV）是一个能够显示 PostScript 文件的图形应用程序。

### GIMP

`GIMP` 是由 Peter Mattis 和 Spencer Kimball 编写的图像处理程序，基于 GNU 通用公共许可证（GPL）发布。大多数 Linux 发行版都附带此程序，尽管你可能需要专门选择一个软件包来安装它。`GIMP` 与其他图像处理程序（如 Adobe Photoshop 和 Corel PHOTO-PAINT）相当。

若要试用 `GIMP`，请在主菜单中的“图形”类别下寻找它。启动时，`GIMP` 会显示一个包含版权和许可证信息的窗口。单击“继续”按钮以继续安装。下一个屏幕显示在执行 `GIMP` 个人安装时将创建的目录。

`GIMP` 安装过程涉及在你的主目录中创建一个目录，并将许多文件放在该目录中。该目录实质上保存了你可能对 `GIMP` 进行更改的任何用户首选项信息。继续单击窗口底部的“继续”按钮。`GIMP` 会创建必要的目录，将必要的文件复制到这些目录中，并通过一系列对话框引导你完成安装。

安装完成后，单击“继续”按钮。从现在开始，你不再看到安装窗口；只有在你首次运行 `GIMP` 时，才需要处理安装问题。

然后，`GIMP` 会加载任何*插件*——增强其功能的外部模块。它会显示一个启动窗口，在每个插件加载时显示有关该插件的消息。完成启动后，`GIMP` 会在一个窗口中显示“今日提示”。你可以浏览这些提示，并单击“关闭”按钮以关闭提示窗口。同时，`GIMP` 会显示多个窗口，如图 4-12 所示。

这些窗口包括一个标题为 `GIMP` 的主工具箱窗口、一个工具选项窗口、一个画笔选择窗口，以及一个图层、通道、路径窗口。其中，主工具箱窗口最为重要——实际上，你可以关闭其他窗口，并使用工具箱中的菜单和按钮进行操作。

![](img/792720823146d68f19fd50c99ebfce4b_260_0.png)

**图 4-12：** 使用 `GIMP` 修饰你的照片。

# 第二篇

# 第 4 章

# 介绍 Linux

工具箱菜单栏上有三个菜单：

- **文件菜单** 包含创建新图像、打开现有图像、保存和打印图像、发送图像邮件以及退出 `GIMP` 的选项。
- **扩展菜单** 让你能够访问 `GIMP` 的众多扩展。扩展菜单的具体内容取决于你的系统安装了哪些扩展。
- **帮助菜单** 是你可以获取帮助和查看提示的地方。例如，选择“帮助”::“帮助”可以打开 `GIMP` 帮助浏览器，其中包含有关 `GIMP` 的在线信息。

要在 `GIMP` 中打开图像文件，选择“文件”::“打开”。此时会出现“加载图像”对话框，你可以使用它来选择图像文件。你可以更改目录并选择要打开的图像文件。`GIMP` 可以读取所有常见的图像文件格式，例如 GIF、JPEG、TIFF、PCX、BMP、PNG 和 PostScript。选择文件并单击“确定”后，`GIMP` 将图像加载到新窗口中。（请参阅图 4-12，查看图像在 `GIMP` 中加载后的样子，以及 `GIMP` 的所有其他窗口。）

工具箱还有许多按钮，代表你用来编辑图像和应用特殊效果的工具。将鼠标指针放在按钮上即可获取每个工具按钮的弹出帮助。通过单击工具按钮可以选择工具，并将该工具的效果应用到图像上。

为了你的方便，当你在图像窗口上右键单击时，`GIMP` 会显示一个弹出菜单。该弹出菜单包含工具箱中文件和扩展菜单中的大多数选项。然后你可以从这些菜单中选择特定操作。

你可以使用 `GIMP` 做的不仅仅是加载和查看图像，但书中无法详细讨论其所有功能。如果你想尝试 `GIMP` 的其他功能，请查阅 `GIMP` 用户手册（GUM），可在 `http://manual.gimp.org` 在线获取。你还可以选择“扩展”::“Web 浏览器”::“GIMP.ORG”::“文档”来访问 `GIMP` 的在线文档。（当然，此命令需要互联网连接才能工作。）

访问 `GIMP` 主页 `www.gimp.org` 以查找 `GIMP` 的最新消息和其他资源的链接。

### GNOME Ghostview

`GNOME Ghostview` 是一个图形应用程序，非常适合查看和打印 PostScript 或 PDF 文档。对于长文档，你可以查看和打印选定的页面。你还可以通过放大或缩小以不同的缩放级别查看文档。

要在 Fedora Core 中运行 `GNOME Ghostview`，从图形用户桌面选择“主菜单”→“图形”→“PostScript 查看器”。将显示 `GNOME Ghostview` 应用程序窗口。除了顶部的菜单栏和工具栏外，一个垂直分割线将窗口的主显示区域分为两部分。

要在 `GNOME Ghostview` 中加载和查看 PostScript 文档，选择“文件”→“打开”，或单击工具栏上的“打开”图标。`GNOME Ghostview` 会显示一个“文件选择”对话框。使用此对话框导航文件系统并选择一个 PostScript 文件。你可以选择随 Ghostscript 附带的一个 PostScript 文件。例如，在 `/usr/share/ghostscript/7.07/examples` 目录中打开文件 `tiger.ps`。（如果你的系统 Ghostscript 版本高于 7.07，你需要使用新版本号替代 7.07。）

要打开选定的文件，请单击“文件选择”对话框中的“打开文件”按钮。`GNOME Ghostview` 打开选定的文件，处理其内容，并在其窗口中显示输出，如图 4-13 所示。

`GNOME Ghostview` 对于查看各种 PostScript 格式的文件非常有用。（这些文件名通常包含 `.ps` 扩展名。）你还可以在 `GNOME Ghostview` 中打开 PDF 文件——它们通常包含 `.pdf` 扩展名。

- **记住：** `GNOME Ghostview` 对于查看各种 PostScript 格式的文件非常有用。（这些文件名通常包含 `.ps` 扩展名。）你还可以在 `GNOME Ghostview` 中打开 PDF 文件——它们通常包含 `.pdf` 扩展名。

![](img/792720823146d68f19fd50c99ebfce4b_262_0.png)

# 第 5 章：使用文本编辑器

## 本章内容

- 使用图形用户界面（GUI）文本编辑器
- 使用 `ed` 文本编辑器
- 了解 `vi` 文本编辑器



在 Linux 中，大多数系统配置文件都是文本文件。如果你编写任何 shell 脚本或其他计算机程序，它们也是文本文件。有时，你需要使用专为编辑目的设计的程序来编辑这些文件：文本编辑器。例如，你可能需要编辑诸如 `/etc/hosts`、`/etc/resolv.conf`、`/etc/X11/XF86Config-4`、`/etc/apt/sources.list` 以及更多文件。

在本章中，我将向你介绍几种文本编辑器——既有图形界面编辑器，也有文本模式编辑器。

# 使用图形用户界面文本编辑器

每个图形桌面——GNOME 和 KDE——都附带了图形用户界面文本编辑器（即具有图形用户界面的文本编辑器）。

要使用图形用户界面文本编辑器，请在主菜单中查找，并在适当的类别中搜索文本编辑器。例如，在 Debian 和 Fedora Core 中，在 GNOME 桌面上选择“应用程序→附件→文本编辑器”。当你打开并运行文本编辑器后，可以通过点击工具栏上的“打开”按钮来打开文件，这将弹出“打开文件”对话框。然后，你可以更改目录，通过点击“确定”按钮选择要编辑的文件。

然后，GNOME 文本编辑器会将其窗口加载该文件。你可以同时打开多个文件，并在编辑文件时在这些文件之间切换。图 5-1 展示了使用编辑器的典型编辑会话。

![](img/792720823146d68f19fd50c99ebfce4b_265_0.png)

在这种情况下，编辑器打开了三个文件——`hosts`、`fstab` 和 `inittab`（均来自 `/etc` 目录）——用于编辑。文件名显示在编辑器窗口工具栏下方的选项卡中。你可以通过点击选项卡在文件之间切换。当前文件名显示在窗口的标题栏中。

如果你打开一个你只有读权限的文件，文件名后会附加文本 [Read Only]，以表明该文件是只读的。在图 5-1 中，所有文件都是只读的，因为我是以普通用户身份登录的，并且正在打开只有 `root` 才能修改的系统文件。

其余的文本编辑步骤都是直观的。要输入新文本，请单击以定位光标并开始键入。你可以使用文本编辑区域上方工具栏上的按钮来选择、复制、剪切和粘贴文本。

从 KDE 桌面，你可以通过选择“主菜单→编辑器→高级文本编辑器”来启动 KDE 高级文本编辑器（Kate）。要打开文本文件，请选择“文件→打开”。Kate 会显示一个对话框。从这个对话框，你可以转到你选择的目录，选择要打开的文件，然后点击确定。然后 Kate 将打开文件，并在窗口中显示其内容。然后你可以编辑该文件。

# 使用 ed 和 vi 进行文本编辑

图形用户界面文本编辑器允许你使用鼠标和键盘以与使用任何文字处理器相似的方式编辑文本文件。文本模式编辑器则完全是另一种生物——你只能使用键盘工作，并且必须输入晦涩难懂的命令来执行编辑任务，例如剪切和粘贴文本或输入和删除文本。Linux 附带了两个文本模式文本编辑器：

- `ed`：一个面向行的文本编辑器
- `vi`：一个全屏文本编辑器，支持一个名为 `ex` 的早期编辑器的命令集

与图形文本编辑器相比，`ed` 和 `vi` 编辑器显得晦涩难懂。然而，你仍然应该熟悉 `ed` 和 `vi` 的基本编辑命令，因为有时这两个可能是唯一可用的编辑器。例如，如果 Linux 拒绝从硬盘启动，你可能需要从软盘启动。在这种情况下，你必须使用 `ed` 编辑器编辑系统文件，因为该编辑器足够小，可以放在软盘上。我将带你了解 `ed` 和 `vi` 的基本文本编辑命令——它们并没有那么难。

## 使用 ed

通常，你只在启动 Linux 的最小版本时使用 `ed`（例如，从设置好作为启动盘的软盘启动），并且系统不支持全屏模式。在所有其他情况下，你可以使用在全屏文本模式下工作的 `vi` 编辑器。

当你使用 `ed` 时，你在命令模式或文本输入模式下工作：

- **命令模式** 是你默认获得的状态。在此模式下，你键入的任何内容都被解释为命令。`ed` 文本编辑器有一个简单的命令集，其中每个命令由一个或多个字符组成。
- **文本输入模式** 用于输入文本。你可以使用命令 `a`（追加）、`c`（更改）或 `i`（插入）进入输入模式。在输入文本行后，你可以通过单独在一行输入一个句点 `.` 来退出输入模式。

要练习编辑文件，请发出以下命令将 `/etc/fstab` 文件复制到你的主目录：

```
cd
cp /etc/fstab .
```

现在，你的主目录中有一个名为 `fstab` 的文件。键入 `ed -p: fstab` 开始用 `ed` 编辑文件。编辑器响应如下：

```
878
:
```

此示例使用 `-p` 选项将提示符设置为冒号字符 (`:`)，并打开 `fstab` 文件（在当前目录中，即你的主目录）进行编辑。`ed` 编辑器打开该文件，报告文件中的字符数 (`878`)，显示提示符 (`:`)，并等待命令。

当你使用 `ed` 编辑时，请确保始终开启提示符字符（使用 `-p` 选项）。如果没有提示符，很难区分 `ed` 是处于输入模式还是命令模式。

`ed` 打开文件进行编辑后，当前行是文件的最后一行。要查看当前行号（当前行是 `ed` 应用命令的行），请使用 `.,=` 命令，如下所示：

```
:,=
9
```

此输出告诉你 `fstab` 文件有九行。（你的系统的 `/etc/fstab` 文件可能有不同的行数，在这种情况下 `ed` 会显示不同的数字。）

你可以使用 `1,$p` 命令查看文件中的所有行，如下例所示：

```
:1,$p
# This file is edited by fstab-sync - see 'man fstab-sync' for details
/dev/VolGroup00/LogVol00 / ext3 defaults 1 1
LABEL=/boot /boot ext3 defaults 1 2
/dev/dvptcs /dev/pts devpts gid=5,mode=620 0 0
/dev/shm /dev/shm tmpfs defaults 0 0
/dev/proc /proc proc defaults 0 0
/dev/sys /sys sysfs defaults 0 0
/dev/VolGroup00/LogVol01 swap swap defaults 0 0
/dev/scd0 /media/cdrom auto
pamconsole,exec,noauto,managed 0 0
/dev/fd0 /media/floppy auto
pamconsole,exec,noauto,managed 0 0
/dev/hdc /media/cdrom auto
pamconsole,exec,noauto,managed 0 0
:
```

要转到特定行，请键入行号：

```
:2
```

编辑器通过显示该行来响应：

```
/dev/VolGroup00/LogVol00 / ext3 defaults 1 1
:
```

假设你想删除包含 `cdrom` 的那一行。要搜索一个字符串，请键入一个斜杠 `/` 后跟你要查找的字符串：

```
:/cdrom
/dev/hdc          /media/cdrom       auto
pamconsole,exec,noauto,managed 0 0
:
```

编辑器定位包含该字符串的行，然后显示它。该行成为当前行。

要删除当前行，请使用如下 `d` 命令：

```
:d
:
```

要将一个字符串替换为另一个，请使用 `s` 命令。例如，要将 `cdrom` 替换为字符串 `cd`，请使用此命令：

```
:s /cdrom/ cd /
:
```

要在当前行之前插入一行，请使用 `i` 命令：

```
:i
   (输入你想插入的行)
   (输入一个单独的句点表示你已完成)
:
```

你可以输入任意数量的行。在最后一行之后，单独在一行输入一个句点 `.`。该句点标志着文本输入模式的结束，编辑器切换到命令模式。在这种情况下，你可以看到提示符 (`:`)，从而判断 `ed` 已切换到命令模式。

当你满意所做的更改时，你可以使用 `w` 命令将它们写入文件。如果你想要保存更改并退出，请键入 `wq` 以同时执行这两个步骤：

```
:wq
857
```

`ed` 编辑器保存文件中的更改，显示保存的字符数，并退出。如果你想不保存任何更改就退出编辑器，请使用 `Q` 命令。

这些示例让你对如何使用 `ed` 命令执行编辑文本文件的基本任务有了了解。表 5-1 列出了一些常用的 `ed` 命令。

## 常用 ed 命令

| 命令 | 功能说明 |
| :--- | :--- |
| `! command` | 执行 shell 命令。（例如，`!pwd` 显示当前目录。） |
| `$` | 跳转到缓冲区中的最后一行 |
| `%` | 将后续命令应用于缓冲区中的所有行。（例如，`%p` 打印所有行。） |
| `+` | 跳转到下一行 |
| `+n` | 跳转到第 n 行（其中 n 是你指定的数字） |
| `,` | 将后续命令应用于缓冲区中的所有行。（例如，`,p` 打印所有行。）这与 `%` 类似。 |
| `-` | 跳转到前一行 |
| `-n` | 跳转到第 n 行之前（其中 n 是你指定的数字） |
| `.` | 指向缓冲区中的当前行 |



| `/text/` | 向前搜索指定文本 |
| `;` | 指向一个行范围——从当前行到缓冲区中的最后一行 |
| `=` | 打印行号 |
| `?text?` | 向后搜索指定文本 |
| `^` | 跳转到前一行。（另见 `-` 命令。） |
| `^n` | 跳转到第 n 行之前（其中 n 是你指定的数字）。（另见 `-n` 命令。） |
| `a` | 在当前行末尾追加内容 |
| `c` | 修改指定的行 |
| `d` | 删除指定的行 |
| `i` | 在当前行之前插入文本 |
| `n` | 跳转到第 n 行 |
| 按回车键 | 显示下一行并将该行设为当前行 |
| `q` | 退出编辑器 |
| `Q` | 退出编辑器且不保存更改 |
| `r file` | 读取并插入文件内容到当前行之后 |
| `s/old/new/` | 用新字符串替换旧字符串 |
| `u` | 撤销最后一个命令 |
| `W file` | 将缓冲区内容追加到指定文件的末尾 |
| `w file` | 将缓冲区保存到指定文件。（如果没有指定文件名，则保存到默认文件——即 `ed` 当前正在编辑的文件。） |

## 使用 vi

`vi` 编辑器是一个全屏文本编辑器，因此你可以同时查看多行内容。大多数 UNIX 系统（包括 Linux）都附带了 `vi`。因此，如果你了解 `vi` 的基本功能，就可以在任何 UNIX 系统上编辑文本文件。

![](img/792720823146d68f19fd50c99ebfce4b_270_0.png)

当 `vi` 编辑文件时，它会读取文件并将其加载到缓冲区——一块内存区域——以便你可以修改缓冲区中的文本。`vi` 编辑器在编辑过程中也会使用临时文件，但在你保存更改之前，原始文件不会发生改变。

要启动编辑器，输入 `vi` 并在其后跟上你要编辑的文件名，格式如下：

```
vi /etc/fstab
```

随后 `vi` 编辑器将文件加载到内存中，并在文本屏幕上显示前几行，同时将光标定位在第一行，如图 5-2 所示。

![](img/792720823146d68f19fd50c99ebfce4b_270_1.png)

**图 5-2：** 你可以使用 `vi` 全屏文本编辑器编辑文本文件。

最后一行显示了文件的路径名，以及文件的行数（11 行）和字符数（878 个）。在这种情况下，文件名后出现 `[readonly]` 字样，因为我是在普通用户身份下打开 `/etc/fstab` 文件（这意味着我没有权限修改该文件）。稍后，`vi` 显示界面中的最后一行将作为命令输入区。其余行则显示文件内容。如果文件包含的行数少于屏幕显示的行数，`vi` 会在第一列显示波浪号（~）来表示空行。

当前行由光标标记，光标表现为一个小的黑色矩形。光标会出现在某个字符上方。

使用 `vi` 时，你工作在以下三种模式之一：

- **可视命令模式** 是默认模式。在此模式下，你输入的任何内容都被解释为应用于包含光标所在行的命令。`vi` 命令与 `ed` 命令相似。
- **冒号命令模式** 用于读取或写入文件、设置 `vi` 选项以及退出 `vi`。所有冒号命令都以冒号（:`）开头。当你输入冒号时，`vi` 将光标定位在最后一行并等待你输入命令。当你按下回车键时，命令生效。
- **文本输入模式** 用于输入文本。你可以通过命令 `a`（在光标后插入）、`A`（在行末追加）或 `i`（在光标前插入）进入输入模式。输入多行文本后，必须按 `Esc` 键退出输入模式并重新进入可视命令模式。

这些模式的一个共同问题是，你很难轻松判断 `vi` 当前处于哪种模式。你可能开始输入，结果才发现 `vi` 并不在输入模式，这会令人沮丧。

![](img/792720823146d68f19fd50c99ebfce4b_271_0.png)

如果你想确保 `vi` 处于命令模式，只需按几次 `Esc` 键即可。（多次按 `Esc` 键没有坏处。）

要在 `vi` 中查看在线帮助，请在冒号命令模式下输入 `:help`。使用完帮助后，输入 `:q` 退出帮助屏幕并返回到你正在编辑的文件。

`vi` 编辑器最初将光标定位在第一行的第一个字符处——而你需要知道的最实用技巧之一是如何移动光标。为了练习一下，尝试表 5-2 中显示的那些命令。

### 表 5-2 vi 中的光标移动命令

| 按键 | 功能说明 |
| :--- | :--- |
| ↓ | 将光标向下移动一行 |
| ↑ | 将光标向上移动一行 |
| ← | 将光标向左移动一个字符 |
| → | 将光标向右移动一个字符 |
| `W` | 将光标向前移动一个单词 |
| `B` | 将光标向后移动一个单词 |
| `Ctrl+D` | 向下滚动半屏 |
| `Ctrl+U` | 向上滚动半屏 |

你可以随时使用便捷的冒号命令跳转到特定行号。例如，要跳转到第 6 行，输入以下内容并按回车键：

```
:6
```

当你输入冒号时，`*vi*` 会在屏幕最后一行显示该冒号。此后，`*vi*` 将把你输入的任何文本作为命令处理。你必须按下回车键才能将命令提交给 `*vi*`。在冒号命令模式下，`*vi*` 接受 `*ed*` 编辑器接受的所有命令——并且还接受更多命令。

要搜索某个字符串，首先输入斜杠（`/`）。`*vi*` 编辑器会在屏幕最后一行显示该斜杠。输入要搜索的字符串，然后按回车键。`*vi*` 编辑器定位到该字符串，并将光标置于该字符串的开头。因此，要在文件 `*/etc/fstab*` 中定位字符串 `*cdrom*`，请输入

```
/cdrom
```

要删除包含光标的那一行，输入 `dd`（两个小写字母 `d`）。`*vi*` 编辑器删除该文本行，并使下一行成为当前行。

要在光标前开始输入文本，输入 `i`（单独一个小写字母 `i`）。`*vi*` 编辑器切换到文本输入模式。现在你可以输入文本了。输入完文本后，按 `Esc` 键返回到可视命令模式。

完成文件编辑后，你可以使用 `:w` 命令保存文件中的更改。若要退出编辑器而不保存任何更改，请使用 `:q!` 命令。如果你想保存更改并退出，可以输入 `:wq` 以同时执行这两步操作。`*vi*` 编辑器将保存文件中的更改并退出。你还可以通过按下 `Shift+ZZ`（按住 `Shift` 键并按两次 `Z`）来保存更改并退出编辑器。

除了上述提到的命令，`*vi*` 还接受大量其他命令。表 5-3 列出了按任务分类的一些常用 `*vi*` 命令。

### 表 5-3 常用 vi 命令

| 命令 | 功能说明 |
| :--- | :--- |
| **插入文本** | |
| `a` | 在光标后插入文本 |
| `A` | 在当前行末尾插入文本 |
| `I` | 在当前行开头插入文本 |
| `i` | 在光标前插入文本 |
| **删除文本** | |
| `D` | 删除直到当前行末尾 |
| `d` | 删除当前行 |
| `dG` | 从当前行删除到文件末尾 |
| `dw` | 从光标处删除到下一个单词末尾 |
| `x` | 删除光标所在的字符 |
| **修改文本** | |
| `C` | 修改直到当前行末尾 |
| `cc` | 修改当前行 |
| `J` | 将当前行与下一行合并 |
| `rx` | 将光标下的字符替换为 `x`（其中 `x` 是任意字符） |
| **移动光标** | |
| `h` 或 `←` | 向左移动一个字符 |
| `j` 或 `↓` | 向下移动一行 |
| `k` 或 `↑` | 向上移动一行 |
| `L` | 移动到屏幕末尾 |
| `l` 或 `→` | 向右移动一个字符 |
| `w` | 移动到下一个单词的开头 |
| `b` | 移动到上一个单词的开头 |
| **滚动文本** | |
| `Ctrl+D` | 向前滚动半屏 |
| `Ctrl+U` | 向后滚动半屏 |
| **刷新屏幕** | |
| `Ctrl+L` | 重绘屏幕 |
| **剪切和粘贴文本** | |
| `yy` | 将（复制）当前行到未命名的缓冲区 |
| `P` | 将剪切的行放在当前行上方 |
| `p` | 将剪切的行放在当前行下方 |
| **冒号命令** | |
| `: ! command` | 执行 `shell` 命令 |
| `:q` | 退出编辑器 |
| `:q!` | 退出而不保存更改 |
| 命令 | 执行的操作 |
|---|---|
| `:r filename` | 读取文件并将其插入到当前行之后 |
| `:w filename` | 将缓冲区写入文件 |
| `:wq` | 保存更改并退出 |

**搜索文本**

| 命令 | 执行的操作 |
|---|---|
| `/string` | 向前搜索字符串 |
| `?string` | 向后搜索字符串 |

**其他操作**

| 命令 | 执行的操作 |
|---|---|
| `u` | 撤销上一个命令 |
| `Esc` | 结束输入模式并进入可视命令模式 |
| `U` | 撤销当前行的最近更改 |

# 第三篇

# 网络

第五波

作者：Rich Tennant

![](img/792720823146d68f19fd50c99ebfce4b_276_0.png)

> “我想你可以说，这是我们网络的中枢。”

## 内容概览

- 第 1 章：连接到互联网 .........253
- 第 2 章：设置局域网.......275



- 第 3 章：添加无线以太网局域网........287

- 第 4 章：管理网络 .....299

# 第 1 章：连接到互联网

## 本章内容

- 理解互联网
- 决定如何连接到互联网
- 使用 DSL 连接到互联网
- 使用电缆调制解调器连接到互联网
- 设置拨号 PPP 链接

互联网正迅速成为大多数人的生命线。似乎很多人一天都离不开它（我知道，没有互联网我也写不了这本书）。有时，我甚至会想，没有互联网我们是怎么生存下来的。鉴于互联网的普及和受欢迎程度，我很有把握地认为，你希望将你的 Linux 系统连接到互联网。在本章中，我将向你展示如何以几种不同的方式连接到互联网——具体取决于你拥有的是 DSL、电缆调制解调器还是拨号网络连接。

连接互联网的两种选择——DSL 和电缆调制解调器——都涉及将专用调制解调器连接到 Linux 系统上的以太网卡。在这些情况下，你需要在 Linux 系统上设置以太网网络。（我将在本篇小册子的第 2 章中解释网络。）在本章中，我将详细展示如何设置 DSL 或电缆调制解调器连接。

我还会向你展示另一种选择——拨号网络——这涉及从你的 Linux 系统拨号连接互联网服务提供商（ISP）。

## 理解互联网

你如何看待互联网取决于你的视角。普通大众从他们使用的服务角度来看待互联网。例如，作为用户，你可能会认为互联网是一种信息交换媒介，具有如下功能：

- **电子邮件：** 使用类似 `mom@home.net` 的地址，向互联网上的任何其他用户发送电子邮件。
- **万维网：** 从互联网上数百万台服务器下载并查看文档。
- **新闻组：** 阅读新闻组，并向名为 `comp.os.linux.networking` 或 `comp.os.linux.setup` 等新闻组发布新闻条目。
- **信息共享：** 下载软件、音乐文件、视频等。反过来，你可以提供文件供其他系统的用户下载。
- **远程访问：** 假设你有权访问该远程计算机，你可以登录到互联网上的另一台计算机。

技术人员说，互联网是一个全球性的*网络的网络*。术语 *internet*（小写）是 *internetworking*（互连网）的简称——即网络之间的互连。互联网协议（IP）的设计理念是连接许多独立的网络。

![](img/792720823146d68f19fd50c99ebfce4b_279_0.png)

就物理连接而言，互联网类似于高速公路和道路的网络。正是这种相似性促使大众媒体将互联网称为“信息高速公路”。就像高速公路和道路网络包括一些州际高速公路、许多州道以及更多居住区街道一样，互联网也有一些非常高容量的网络（例如，10 Gbps 的主干网可以处理每秒 100 亿位），以及大量较低容量的网络，范围从 56 Kbps 拨号连接到 45 Mbps T3 链路。(*Kbps* 是千位每秒，*Mbps* 是兆位每秒。) 高容量网络是互联网的主干。

在管理方面，互联网不是由单一组织运营的，也不是由任何中央计算机管理的。你可以将物理互联网视为由成千上万的合作组织共同管理的*网络的网络*。是的，由*成千上万*个组织管理的一组网络——听起来很惊人，但它行得通！

### 决定如何连接到互联网

所以你想要连接到互联网，但不知道怎么做？让我数一下方式。如今，将家庭和小型办公室连接到互联网有三种流行选择。（当然，大型企业和政府还有许多其他的连接方式。）

- **数字用户线路（DSL）：** 你的本地电话公司以及其他电信公司可能提供 DSL。DSL 提供了一种通过普通电话线发送高速数字数据的方式。通常，DSL 提供的数据传输速率在 128 Kbps 到 1.5 Mbps 之间。你从互联网下载数据的速度远高于将数据从你的 PC 发送到互联网（*上传*）的速度。使用 DSL 的一个注意事项是，你的家必须距离当地的中央局（你的电话线最终连接的电信公司设施）12,000 到 15,000 英尺之间。距离限制因提供商而异。在美国，你可以在 `www.dslreports.com/distance` 查看许多提供商的距离限制。
- **电缆调制解调器：** 如果你所在地区的有线电视公司提供通过电缆访问互联网的服务，你可以使用该服务将你的 Linux 系统连接到互联网。通常，电缆调制解调器提供的数据传输速率比 DSL 快——成本大致相同。通过电缆调制解调器从互联网下载数据的速度远快于将数据从你的 PC 发送到互联网的速度。你可以预期常规下载速度为 1.5 Mbps，上传速度约为 128 Kbps，但有时你可能会获得比这些更高的速度。
- **拨号网络：** 拨号连接是大多数人在 DSL 和电缆调制解调器出现之前使用的连接方式。你将 PC 连接到连接到电话线的调制解调器。然后你拨号 ISP 以连接到互联网。这就是它被称为*拨号网络*的原因——通过拨号调制解调器在你的 Linux PC 和另一个网络（互联网）之间建立网络连接。在这种情况下，最大数据传输速率为 56 Kbps。

DSL 和电缆调制解调器服务不仅将你连接到互联网，还充当你的互联网服务提供商（ISP）；除了速度提升外，你付费获得的是一个 IP 地址和你的电子邮件账户。如果你使用拨号调制解调器连接到互联网，首先你必须连接到电话线（为此你支付电话费给电话公司），然后选择并付费给另一个独立的 ISP——它给你一个拨号号码以及所有其他必要的东西（如 IP 地址和电子邮件账户）。

表 1-1 总结了所有这些选择。你可以查阅该表，选择可用且最适合你需求的连接类型。

| 功能 | 拨号 | DSL | 电缆 |
|---|---|---|---|
| **设备** | 调制解调器 | DSL 调制解调器，以太网卡 | 电缆调制解调器，以太网卡 |
| **还需要** | 电话服务和互联网服务提供商（ISP） | 电话服务以及位于中央局 12,000 到 15,000 英尺范围内的位置 | 有线电视连接 |
| **连接类型** | 拨号连接 | 始终在线，专用 | 始终在线，共享 |
| **典型速度** | 最高 56 Kbps | 下载 640 Kbps，上传 128 Kbps（更高速度成本更高） | 下载 1.5 Mbps，上传 128 Kbps |
| **一次性成本（估算）** | 无 | 安装 = 100-200 美元（自行安装免费）；设备：50-100 美元（可租用，可能需要激活费用） | 安装 = 100-200 美元（自行安装免费）；设备 = 50-100 美元（可租用） |
| **典型月度费用（2005 年）** | 电话费 = 每月 20 美元；ISP 费 = 每月 15-30 美元 | 每月 40-50 美元；可能需要每月调制解调器租赁费 | 每月 40-50 美元；可能需要每月调制解调器租赁费 |

*注意：费用因地区和提供商而异。所示费用为美国大都市地区的典型费用。*

除了表 1-1 中显示的三种选择外，还有几种不太常见的选择可能可用。这些包括光纤到户（FTTH）、电力线宽带（BPL）、固定无线宽带（称为 FWB 或 WiMax）以及卫星互联网接入（例如 DIRECWAY 和 StarBand）。如果你的地理区域提供一种或多种这些选择，并且你想使用其中一种进行互联网接入，请遵循特定服务提供商关于设置互联网连接的说明。通常，卫星互联网接入可覆盖广阔的地理区域（即使是没有电话或电缆的地方），但初始设备成本和月度费用高于 DSL 和电缆。有关卫星互联网接入的更多信息，请访问 `www.satellite-internet-access.net`。

![](img/792720823146d68f19fd50c99ebfce4b_281_0.png)

### 使用 DSL 连接

DSL 代表数字用户线路。DSL 利用你现有的电话线，除了正常的模拟语音信号外还发送数字数据（*模拟*意味着连续变化，而数字数据由 1 和 0 表示）。电话线从你家延伸到中央局，在那里线路连接到电话公司的网络。顺便说一下，从你家到中央局的连接被称为*本地环路*。当你注册 DSL 服务时，电话公司将你的电话线连接到中央局的某些特殊设备上。该设备可以分离数字数据和语音。从此以后，你的电话线可以承载数字数据，然后直接发送到中央局的互联网连接。

#### DSL 的工作原理

一种称为 DSL 调制解调器的特殊设备负责通过你的电话线将数字数据从你的 PC 传输到电话公司的中心局。你的 PC 可以通过用于正常电话通话的同一条电话线连接到互联网——即使线路正在用于 DSL 传输，你仍可以进行语音通话。图 1-1 展示了典型的 DSL 互联网连接方式。

你的 PC 通过以太网连接与 DSL 调制解调器通信，这意味着你的 Linux 系统中需要一块以太网卡。

你的 PC 通过以太网连接将数字数据发送给 DSL 调制解调器。DSL 调制解调器使用与模拟语音信号不同的频率来发送数字数据。语音信号占据了电话线所能承载的所有频率中的一小部分。DSL 使用较高的频率来传输数字数据，因此语音和数据可以在同一条电话线上传输。

![](img/792720823146d68f19fd50c99ebfce4b_282_0.png)



你家与中心局之间的距离——即`环路长度`——是影响 DSL 性能的一个因素。不幸的是，电话线只能可靠地在有限距离内传输 DSL 信号——通常在三英里或更短的距离内，这意味着只有当你的家（或办公室）位于电话公司中心局大约三英里范围内时，你才能获得 DSL 服务。你的电话公司可以告知你是否可以在你的所在地获得 DSL 服务。通常，他们有一个网站，你可以输入你的电话号码来获取关于 DSL 可用性的反馈。例如，对于美国地区，可以尝试访问 www.dslavailability.com。

### DSL 术语综述：ADSL、IDSL、SDSL

我一直在使用术语 `DSL`，好像只有一种 DSL 类型。正如你可能想象的那样，事情从未如此简单。实际上有几种 DSL 变体，每种都有不同的特性。请查看：

- `ADSL`：非对称 DSL 是最常见的 DSL 形式，其下载速度（从互联网到你的 PC）远快于上传速度（从你的 PC 到互联网）。`ADSL` 的下载速度最高可达 8 Mbps，上传速度最高可达 1 Mbps。`ADSL` 在你的位置距离中心局大约 2.5 英里（12,000 英尺）以内时表现最佳。`ADSL` 服务的价格根据你所需的下载和上传速度而定。一种名为 G.lite 的流行 `ADSL` 形式是专门设计用于在语音通话使用的同一线路上工作的。`G.lite` 的最大下载速度为 1.5 Mbps，最大上传速度为 512 Kbps。
- `IDSL`：ISDN DSL（ISDN 是一种较旧的技术，称为`综合业务数字网`）是一种特殊的 DSL 类型，可以在电话与中心局之间多达五英里的距离内工作。缺点是 `IDSL` 仅提供高达 144 Kbps 的`下行`（从互联网到你的 PC）和`上行`（从你的 PC 到互联网）速度。
- `SDSL`：对称 DSL 提供高达 1.5 Mbps 的相等下载和上传速度。`SDSL` 的价格根据你所需的速率而定，速度越高成本越高。你的位置离电话公司中心局越近，你能获得的连接速度就越快。

DSL（以及电缆调制解调器）的速度通常由两个数字表示，中间用斜杠分隔，例如：1500/384。这些数字指的是以千位/秒为单位的传输速率（即每秒传输数千位，缩写为 Kbps）。第一个数字是下载速度，第二个是上传速度。因此，1500/384 意味着你可以期望以最高 1,500 Kbps（或 1.5 Mbps）的速率从互联网下载，并以 384 Kbps 的速率上传到互联网。如果你的电话线状况不完美，你可能无法达到这些最大速率——`ADSL` 和 `SDSL` 都会根据现有线路状况调整速度。

![](img/792720823146d68f19fd50c99ebfce4b_283_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_283_1.png)

DSL 服务的价格取决于你选择哪种变体——`ADSL`、`IDSL` 或 `SDSL`。对于大多数家庭用户，主要选择是 `ADSL`（或更准确地说，是 `ADSL` 的 `G.lite` 形式），传输速度评级为 1500/128。

## 典型的 DSL 设置

要在你的家庭或企业中获得 DSL，你需要联系 DSL 提供商。除了你的电话公司外，你还可以找到许多其他 DSL 提供商。无论谁提供 DSL 服务，中心局——即你的电话线连接到电话网络其余部分的地方——都必须进行一些工作。这项工作涉及将你的电话线连接到能够与家中或办公室的 DSL 调制解调器配合工作的设备。然后，中心局设备和你所在地的 DSL 调制解调器可以执行必要的操作，以通过电话线发送和接收数字数据。

由于需要在中心局设置你的线路，所以在下单后需要一段时间才能准备好你的线路以支持 DSL。

你需要做的第一步是查看提供服务的 DSL 提供商，并确认你是否实际可以获得该服务。由于 DSL 只能在特定距离内工作——通常是你所在位置与中心局之间小于 2.5 英里——你必须检查是否在此距离限制之内。请联系你的电话公司进行核实。你可能可以在网上检查这种可用性。试着在谷歌（www.google.com）中输入“DSL availability”以及你当地电话公司的名称。搜索结果可能包括一个网站，你可以输入电话号码来了解你的家或办公室是否可以支持 DSL。

如果 DSL 可用，你可以查看服务类型——`ADSL` 与 `SDSL`——以及价格。价格取决于你希望的下载和上传速度。有时，电话公司提供简单的住宅 DSL（基本上是 `ADSL` 的 `G.lite` 形式），速度评级为 1500/128——意味着你可以以最高 1,500 Kbps 的速度下载，以 128 Kbps 的速度上传。当然，这些是`最大值`，实际情况可能因具体环境而异。

在选择了想要的 DSL 服务类型和提供商后，你可以下单，并要求提供商在你的家或办公室安装必要的设备。图 1-2 展示了典型住宅 DSL 服务的示例连接图。

以下是图 1-2 中需要注意的一些要点：

- 将 DSL 调制解调器的数据连接连接到墙壁插座上的电话插孔。
- 将 DSL 调制解调器的以太网连接连接到 PC 上的以太网卡。
- 当你连接同一电话线上的其他电话或传真机时，在墙壁插座和每个设备之间安装一个微滤波器。

![](img/792720823146d68f19fd50c99ebfce4b_285_0.png)

由于同一电话线既传输语音信号又传输 DSL 数据，你需要微滤波器来保护 DSL 数据免受可能的干扰。你可以在电子商店或 DSL 提供商处购买它们。

**警告！**

当你通过 DSL 将 Linux PC 连接到互联网时，连接始终处于开启状态，这意味着外部人员入侵 PC 的可能性更大。

**提示**

你可以使用能够执行网络地址转换（NAT）的路由器来保护你的 Linux 系统免受入侵者攻击，此外，还可以与局域网（LAN）中的其他 PC 共享高速连接。这样的 NAT 路由器将内部 LAN 的多个私有互联网协议（IP）地址转换为单个公共 IP 地址，从而允许所有内部 PC 访问互联网。NAT 路由器充当你的 LAN 与互联网之间的网关，并将你的 LAN 与互联网隔离——这使得入侵者更难接触到你 LAN 上的系统。

如果你还想设置局域网，你需要一个以太网集线器将其他 PC 连接到网络。图 1-3 展示了一个典型的设置，通过 NAT 路由器和 DSL 调制解调器将 LAN 连接到互联网。

![](img/792720823146d68f19fd50c99ebfce4b_286_0.png)

**图 1-3：** NAT 路由器将你的 PC 与互联网隔离，并允许你在局域网中与其他 PC 共享 DSL 连接。

在设置如图 1-3 所示的连接时，需要注意以下几点：

- 你需要一个拥有两个 10BaseT 以太网端口的 NAT 路由器（10BaseT 端口看起来像大的电话插孔，也称为 RJ-45 插孔）。通常，一个以太网端口标记为`Internet`（或 `External` 或 `WAN`，即广域网），另一个标记为 `Local` 或 `LAN`（即局域网）。
- 你还需要一个以太网集线器。对于小型家庭网络，你可以购买一个 4 端口或 8 端口的以太网集线器。基本上，你希望集线器的端口数量与你打算连接到局域网的 PC 数量相匹配。
- 使用 10BaseT 以太网电缆将 DSL 调制解调器的以太网端口连接到 NAT 路由器的 Internet 端口。（这些电缆看起来像带有较大 RJ-45 插头的电话线，通常标记为`Category 5` 或 `Cat 5` 线缆。）
- 使用 10BaseT 以太网电缆将 NAT 路由器的 Local 以太网端口连接到以太网集线器的一个端口。
- 现在将每台 PC 连接到以太网集线器。（当然，要做到这一点，首先必须在每台 PC 中安装并配置好以太网卡。）

![](img/792720823146d68f19fd50c99ebfce4b_287_0.png)

您也可以购买一种内置 4 口或 8 口以太网集线器的 NAT 路由器。使用这种集成的路由器和集线器，您只需一个设备即可组建局域网并通过 DSL 调制解调器连接到互联网。由于这类设备同时适用于 DSL 和电缆调制解调器，因此通常以电缆/DSL 路由器的名称销售。

请查阅本小册子的第 2 章，了解如何配置 Linux 系统的网络设置，以便您的系统能够访问互联网。

![](img/792720823146d68f19fd50c99ebfce4b_287_1.png)

DSL 提供商通常使用一种称为以太网上的点对点协议（PPPoE）的协议，在您的个人电脑与提供商中心局的设备之间建立连接。PPPoE 要求您提供用户名和密码，以便通过以太网建立网络连接。要为您的系统设置 PPPoE DSL 连接，您只需运行一个配置系统以支持 PPPoE 的工具程序。您可以在图形用户桌面环境的主菜单中搜索找到该工具。

![](img/792720823146d68f19fd50c99ebfce4b_287_2.png)

在 Fedora Core 中，您可以通过选择“系统”→“管理”→“网络”，点击工具栏上的“新建”，然后在弹出的对话框中的设备类型中选择 xDSL 连接，来设置 PPPoE DSL 连接。然后按照后续屏幕的提示，提供所需的信息，例如登录名和密码。



## 通过电缆调制解调器连接

有线电视公司也通过传输电视信号的同一根同轴电缆提供高速互联网接入。有线电视公司在其设施中安装必要的收发数字数据的设备后，用户即可申请有线互联网服务。然后，您便可以通过传输有线电视信号的同一根电缆获得高速互联网接入。

### 电缆调制解调器的工作原理

一个被称为`电缆调制解调器`的设备是电缆电视网络互联网接入的核心。（参见图 1-4。）`电缆调制解调器`将来自您个人电脑以太网卡的数字数据放置在未使用的频段中。（您可以将其想象成另一个电视频道，只不过这个频道传输的是数字数据，而非图像和声音。）

`电缆调制解调器`将`上游数据`——即从您的个人电脑发送至互联网的数据——放置在不同于从互联网传输到您个人电脑的`下游`数据所在的频道。按设计，`下游`数据传输的速度远高于上游传输速度。其假设是人们从互联网下载的内容远多于上传的内容。（对大多数我们而言，这很可能是真的。）

![](img/792720823146d68f19fd50c99ebfce4b_288_0.png)

**图 1-4：** 电缆调制解调器通过有线电视网络提供高速互联网接入。

**技术知识**

将数百个有线电视频道传输到您家中的同轴电缆是一种非常强大的信号载体。具体而言，同轴电缆可以承载覆盖巨大频率范围（数百兆赫兹 (MHz)）的信号。每个电视频道需要 6 MHz——而同轴电缆可以承载数百个这样的频道。电缆调制解调器将上游数据放置在较小的频段中，并期望在另一个完全不同的频段中接收下游数据。

**技术知识**

您连接互联网的电缆线路的另一端是`电缆调制解调器终端系统`（CMTS）——也称为`前端`——这是您的有线电视公司安装在其中心设施中的设备。（参见图 1-4。）`CMTS`将有线电视网络连接到互联网。它还提取由您的电缆调制解调器（以及您邻居的调制解调器）发送的上游数字数据，并将其全部发送至互联网。`CMTS`还将数字数据放入上游频道，以便您的电缆调制解调器能够提取该数据并通过以太网卡将其提供给您的个人电脑。

电缆调制解调器可以以约 30 Mbps 的速率接收下游数据，并以约 3 Mbps 的速率发送上游数据。然而，一个社区内所有电缆调制解调器共享同一下游容量。每个电缆调制解调器从 `CMTS` 发出的数据流中过滤——分离——出其所需的数据。电缆调制解调器遵循一种名为 `DOCSIS`（有缆数字服务接口）的调制解调器标准。您可以购买任何符合 `DOCSIS` 标准的调制解调器并将其用于您的有线互联网服务；您只需致电有线电视公司并提供调制解调器的识别信息，以便 `CMTS` 能够识别并初始化该调制解调器即可。

![](img/792720823146d68f19fd50c99ebfce4b_289_0.png)

实际上，使用电缆调制解调器，您可以获得约 1.5 Mbps 的下游传输速率和 128 Kbps 的上游速率。这些是最大速率，而您的实际传输速率通常会更低，具体取决于您的社区中有多少用户同时在使用电缆调制解调器。

![](img/792720823146d68f19fd50c99ebfce4b_289_1.png)

如果您想检查下游传输速度，请访问 `http://bandwidthplace.com/speedtest` 并点击链接开始测试。例如，在我的电缆调制解调器连接中，最近的一次测试报告称下游传输速率约为 2.2 Mbps，但在其他时间，速率最高可达 5.2 Mbps。

### 典型的电缆调制解调器设置

要设置电缆调制解调器接入，您的有线电视服务提供商必须提供高速互联网接入。如果该服务可用，您可以致电申请。有线电视公司通常有促销优惠，例如免安装费或前三个月费率优惠。请留意这些优惠。如果您运气好，当地有线电视公司可能正好在您想要申请时提供促销活动。

安装通常由技术人员完成，技术人员会将进来的电缆分成两部分——一侧连接到电视，另一侧连接到电缆调制解调器。技术人员会将电缆调制解调器的信息提供给有线电视公司的前端，以便在其端进行设置。完成所有步骤后，您可以将个人电脑的以太网卡插入电缆调制解调器，即可开始享受高速互联网接入。图 1-5 展示了一个典型的电缆调制解调器连接方式。

电缆调制解调器连接到您个人电脑中的以太网卡。如果您的个人电脑没有以太网卡，有线电视公司的技术人员通常会提供一张。

![](img/792720823146d68f19fd50c99ebfce4b_290_0.png)

关于图 1-5 中的电缆调制解调器设置，请注意以下几个关键点：

- 使用双向分配器将输入的有线电视信号分为两部分。（有线电视技术人员安装分配器。）顺便提一下，双向分配器必须额定为 1 GHz；否则，它可能无法让包含来自互联网下游数据的频率通过。
- 使用同轴电缆将分配器之一的视频输出连接到电缆调制解调器的 F 型视频连接器。
- 将电缆调制解调器的 `10BaseT` 以太网连接连接到您个人电脑上的以太网卡。
- 将您的电视连接到双向分配器的另一个视频输出。

当您使用电缆调制解调器将 Linux 个人电脑直接连接到互联网时，连接始终处于开启状态，因此有人试图入侵您的个人电脑的可能性更大。Linux 包含 `iptables` 数据包过滤功能，您可能希望使用它来保护您的个人电脑免受不需要的互联网连接的影响。

在 `Fedora Core` 中，您可以将防火墙设置设为高安全性。要在 `Fedora Core` 中配置防火墙设置，请从图形用户桌面环境选择“系统管理安全级别和防火墙”。

![](img/792720823146d68f19fd50c99ebfce4b_291_0.png)

为了将您的 Linux 个人电脑或局域网与公共互联网隔离，您可能希望在个人电脑和电缆调制解调器之间添加一个 `NAT` 路由器。`NAT` 路由器其中一个网络接口连接到互联网，另一个连接到您的局域网；路由器随后在您的局域网和互联网之间充当网关。作为额外的福利，您甚至可以通过添加一个以太网集线器，与局域网（LAN）中的所有个人电脑共享一个电缆调制解调器连接。更好的选择是，购买一个组合型的 `NAT` 路由器和集线器，这样只有一个设备就能完成所有工作。顺便提一下，`NAT` 路由器和集线器通常以`电缆/DSL 路由器`的名称销售，因为它们既适用于 DSL 也适用于电缆调制解调器。

`NAT` 路由器将私有 IP 地址转换为公共 IP 地址。当通过 `NAT` 路由器连接时，内部局域网中的任何个人电脑都可以像拥有自己唯一的 IP 地址一样访问互联网。结果：您可以在多台个人电脑之间共享一个互联网连接。（这是一个整个家庭网络冲浪者的理想解决方案！）

图 1-6 展示了一个典型的设置，其中电缆调制解调器连接由局域网中的多台个人电脑共享。

在设置如图 1-6 所示的连接时，请注意以下几点：

- 您需要一个具有两个 `10BaseT` 以太网端口的电缆/DSL `NAT` 路由器（`10BaseT` 端口——也称为 `RJ-45` 插孔，外观像较大的电话插孔）。通常，一个以太网端口标记为`互联网`（或`外部`或 WAN，即广域网），另一个标记为`本地`。
- 如果您打算组建局域网，还需要一个以太网集线器。对于小型家庭网络，您可以购买一个 4 口或 8 口的以太网集线器。基本上，您希望集线器的端口数量与您打算连接到局域网的个人电脑数量相同。
- 考虑购买一个集 `NAT` 路由器和带多个以太网端口的集线器功能于一体的单一设备。
- 将视频电缆连接到电缆调制解调器的视频输入端口。
- 使用 `10BaseT` 以太网电缆将电缆调制解调器的以太网端口连接到 `NAT` 路由器的互联网端口。（这些电缆看起来像电话线，但以太网电缆具有较大的 `RJ-45` 插脚，并且通常标记为`5 类`或`5 类线`。）
- 使用 `10BaseT` 以太网电缆将 `NAT` 路由器的本地以太网端口连接到以太网集线器上的一个端口。
- 现在将每台个人电脑连接到以太网集线器。当然，每台个人电脑必须装有以太网卡。

![](img/792720823146d68f19fd50c99ebfce4b_292_0.png)

图 1-6：

`NAT` 路由器将您的 PC 与互联网隔离开来，同时允许您在局域网内与其他 PC 共享有线调制解调器连接。

在本小册子的第 2 章中，我将解释如何配置此类局域网中的 PC，使它们都能通过路由器访问互联网。

## 设置拨号网络

拨号网络是指通过拨号调制解调器将 PC 连接到远程网络。如果您年岁足够大，还记得当年使用 `Procomm` 或其他串行通信软件进行拨号的日子，请意识到拨号网络与早期串行通信之间存在显著差异。这两种方法都使用调制解调器拨号远程计算机并建立通信路径，但串行通信软件会使您的计算机表现得像一个连接到远程计算机的哑终端。串行通信软件独占拨号连接。例如，您无法运行另一个通信软件副本并使用相同的调制解调器连接。

在拨号网络中，您的 PC 和远程系统都运行网络协议（称为 `TCP/IP`）软件。当您的 PC 拨号并建立通信路径时，网络协议在该拨号连接上交换数据包。巧妙之处在于，任何数量的应用程序都可以使用相同的拨号连接来发送和接收数据包。因此，您的 PC 成为远程计算机所属网络的一部分。（如果远程计算机不在网络上，拨号网络将创建一个由远程计算机和您的 PC 组成的网络。）



在本小册子的第 2 章中，我将更详细地介绍 TCP/IP 协议，但在描述如何设置拨号网络时，我不得不使用该术语以及诸如 *Internet Protocol*（IP）地址和 *Domain Name Service*（DNS）等几个概念。

![](img/792720823146d68f19fd50c99ebfce4b_293_0.png)

在拨号链路上设置 TCP/IP 网络涉及指定用于在通信链路上打包数据包的协议——即约定。*Point-to-Point Protocol*（PPP）是一种用于在任何点对点链路（包括拨号电话线）上建立 TCP/IP 连接的协议。Linux 支持 PPP，并附带可用于设置 PPP 的配置工具，以便您的系统能够与您的 ISP 建立 PPP 连接。

要在 Linux 中设置拨号网络，您需要执行以下操作：

- 1. 在您的 PC 中安装内部或外部调制解调器。如果您的 PC 没有预装内部调制解调器，您可以购买一个外部调制解调器并将其连接到 PC 的串行或 USB 端口。
- 2. 将调制解调器连接到电话线并给调制解调器供电。
- 3. 获取一个 ISP 账户。每个 ISP 都会提供一个用于拨号的电话号码、一个用户名和一个密码。此外，ISP 会为您提供电子邮件和新闻服务器的完整名称。通常，您的系统会自动获取一个 IP 地址。
- 4. 运行 GUI 工具（如果可用）来设置 PPP 连接。如果您找不到 GUI 工具，请在 shell 提示符处输入 `wvdialconf` 或 `etc/wvdial.conf`。`wvdialconf` 程序会自动检测调制解调器并设置配置文件 `/etc/wvdial.conf`。现在使用文本编辑器编辑文件 `/etc/wvdial.conf`，并输入 ISP 的电话号码以及您在该 ISP 处的 Internet 账户的用户名和密码。（您可以猜测这些项目的输入位置，只需查找标记为 Username、Password 和 Phone 的字段。）
- 5. 使用 GUI 工具（如果可用）激活 PPP 连接以连接到 Internet。如果没有 GUI 工具，请以 `root` 身份登录并输入 `wvdial` 来建立 PPP 连接。

我将在以下章节中简要回顾这些步骤。

## 连接调制解调器

单词 *modem* 是调制器/解调器（modulator/demodulator）的缩写——一种将数字信号（1 和 0 的字符串）转换为在电话线和无线电波上传输的连续变化模拟信号的设备。因此，调制解调器是 PC 的数字世界和电话模拟世界之间的中介。图 1-7 说明了调制解调器的概念。

![](img/792720823146d68f19fd50c99ebfce4b_294_0.png)

在 PC 内部，1 和 0 用电压电平表示，但通过电话线传输的信号通常是不同频率的音调。调制解调器位于 PC 和电话线之间，使通过电话线的数据通信成为可能。调制解调器在数字电路的电压/无电压表示和适合通过电话线传输的不同频率音调之间来回转换信息。

在使用外部调制解调器拨号之前，您必须确保调制解调器已正确连接到您的 PC 的某个串行或 USB 端口。

如果您有外部调制解调器，请确保您的调制解调器已正确连接到电源，并且调制解调器已连接到电话线。购买正确类型的电缆将调制解调器连接到 PC。您需要一根直通串行电缆将调制解调器连接到 PC。电缆两端的连接器取决于您 PC 上的串行连接器类型。电缆的调制解调器端需要一个 25 针公头连接器。电缆的 PC 端通常是一个 9 针母头连接器。您可以在大多数电脑商店买到调制解调器电缆。通常，您可以找到标记为 *AT Modem Cable* 的 9 针母头到 25 针公头的调制解调器电缆。使用 USB 电缆连接 USB 调制解调器。

### Winmodems：它们*仅*适用于 Windows

关于随许多新 PC 和笔记本电脑提供的 *Winmodems*，这里有一个简短的警告：Winmodems 是基于软件的内联调制解调器——与传统硬件调制解调器完全不同。也称为 *Windows modems* 或 *software modems*（简称 softmodem），它们仅与特殊的驱动程序软件配合使用（而该驱动程序软件又仅适用于 Microsoft Windows）。使用 Winmodems 和 Linux 时，您基本上需要自己摸索，但您可以在 `www.linmodems.org` 的 Linux Winmodem 支持主页上找到一些有用的指导。例如，我发现我笔记本电脑中的 Winmodem 使用 Conexant 芯片组，并且可以从 `www.linuxant.com/drivers/hsf/full/1/downloads.php` 获取 Linux 驱动程序。然后我可以下载适合我的发行版的版本——网站提供了 Debian 包（DPKG）和 RPM 格式文件。顺便说一下，Conexant 的免费版本驱动程序仅限于 14.4 Kbps。要升级到 56 Kbps，您必须以约 15 美元的美分价格购买完整版本。然而，免费版本适合测试，以确保驱动程序与您的软调制解调器兼容。顺便说一下，您可以通过检查 `www.linmodems.org` 网站来查找许多其他 Winmodems 的 Linux 驱动程序。

如果您的 PC 有内部调制解调器，您所要做的只是将电话线连接到内部调制解调器卡背面的电话插孔。如果是 Winmodem，您仍然需要连接电话线，但您还需要在互联网上做一些研究并下载一个使 Winmodem 在 Linux 中工作的驱动程序。安装好适用于 Winmodem 的工作 Linux 驱动程序后，它的表现就像旧的串行端口调制解调器一样。有关更多信息，请参见侧边栏，“Winmodems：它们*仅*适用于 Windows”。

### 设置和激活 PPP 连接

大多数 ISP 通过其维护的一个或多个系统提供 Internet 的 PPP 拨号访问。如果您注册此类服务，ISP 将提供您需要连接到 ISP 系统的 PPP 连接所需的信息。通常，这些信息包括以下内容：

- 用于连接到远程系统的拨号电话号码。
- 登录远程系统时必须使用的用户名和密码。
- ISP 的邮件和新闻服务器的名称。
- 您 PPP 连接的 IP 地址。如果 IP 地址是动态分配的（这意味着每次您的系统建立连接时 IP 地址可能会变化），您的 ISP 不会提供此地址。
- ISP 的 DNS 的 IP 地址。如果 ISP 动态分配 IP 地址，则不会提供这些地址。

在这些信息中，前两项是设置 `PPP` 连接所必需的。设置和使用PPP连接的具体步骤因发行版而异。对于带有图形界面（GUI）网络连接工具的发行版，你可以轻松找到输入ISP账户信息（即电话号码、用户名和密码）的位置。接下来，我将指出几种针对特定发行版的PPP配置方法。

![](img/792720823146d68f19fd50c99ebfce4b_296_0.png)

Debian 拥有一个用于设置PPP连接的图形界面工具，该工具使用 `wvdial`，而 `wvdial` 默认并未安装。输入 `apt-get install wvdial` 即可安装它。然后，你可以使用图形界面工具来配置并激活拨号PPP连接。

![](img/792720823146d68f19fd50c99ebfce4b_296_1.png)

在 Fedora Core 中，从 GNOME 桌面选择 系统 → 管理 → 网络。（如果你不是以 `root` 身份登录，系统会提示你输入 `root` 密码。）点击工具栏上的“新建”；然后在第一个对话框中选择“调制解调器连接”选项（见图 1-8），并继续配置。

**图 1-8：** 在 Fedora Core 中，通过此对话框配置 PPP 连接。

![](img/792720823146d68f19fd50c99ebfce4b_296_2.png)

![](img/792720823146d68f19fd50c99ebfce4b_296_3.png)

在 SUSE 中，选择 主菜单 → 系统 → YaST 以打开 YaST 控制中心窗口。点击窗口左侧的“网络设备”，然后点击右侧的“调制解调器”。（参见图 1-9。）YaST 会检测调制解调器并显示一个包含调制解调器信息的窗口。然后，你可以为检测到的调制解调器配置 PPP 连接。你可以从列表中选择你的 ISP，或者输入 ISP 的名称、接入电话号码以及 ISP 账户的用户名和密码。

![](img/792720823146d68f19fd50c99ebfce4b_296_4.png)

**图 1-9：** 在 SUSE 中，通过 YaST 配置调制解调器。

![](img/792720823146d68f19fd50c99ebfce4b_297_0.png)



在 SUSE 中设置好调制解调器后，`Kinternet` 工具应该会自动启动，并且面板上会出现一个插头图标，如图 1-10 所示（如果图标未出现，请在 KDE 桌面中选择 主菜单 → Internet → Dial-up）。然后，你可以点击 `Kinternet` 工具的图标来激活 PPP 连接。如果连接似乎没有建立，请右键点击 `Kinternet` 图标，选择“查看日志”，并寻找任何问题的线索。

图 1-10： 在 SUSE 中，点击 `Kinternet` 工具以激活 PPP 连接。

![](img/792720823146d68f19fd50c99ebfce4b_297_1.png)

## 配置 CHAP 和 PAP 认证

在 PPP 连接能够完全建立并运行之前，你系统上的 PPP 服务器必须向 ISP 的 PPP 服务器进行身份验证。*认证*要求证明你拥有有效的 ISP 账户，基本上就是提供用户名和密码（即机密信息）。PPP 规定了在连接两端之间交换认证信息的两种方式：

- 质询握手认证协议 (`CHAP`) 要求远程端发送一个随机生成的质询字符串以及远程服务器的名称。本地系统使用服务器名称查找机密信息；然后，它发送回一个响应，其中包含其自身名称以及使用单向哈希函数计算出的结合机密信息和质询字符串的值。远程系统随后将其计算出的预期哈希值与该值进行核对。如果数值匹配，则认证成功；否则，远程系统将终止连接。在这种情况下，名称和机密信息存储在 `/etc/ppp/chap-secrets` 文件中。请注意，只要 PPP 链路处于活动状态，远程系统可以随时重复 `CHAP` 认证。

- 密码认证协议 (`PAP`) 类似于普通的登录过程。使用 `PAP` 时，本地系统反复发送用户名（名称）和密码（机密信息），直到远程系统确认认证成功或终止连接。名称和机密信息存储在 `/etc/ppp/pap-secrets` 文件中。请注意，用户名和密码是以明文（即未加密）形式发送的。

Linux PPP 服务器支持这两种类型的认证。对于 `PAP` 和 `CHAP` 而言，PPP 服务器所需的信息都是一个名称和一个机密信息——即一对用户名和密码。此认证信息存储在以下配置文件中：

- `/etc/ppp/chap-secrets` 存储 `CHAP` 的信息。典型的 `chap-secrets` 文件如下所示：

```
# Secrets for authentication using CHAP
# client server secret IP addresses
"naba" * "mypassword"
```

- `/etc/ppp/pap-secrets` 存储 `PAP` 的信息。典型的 `pap-secrets` 文件如下所示：

```
# Secrets for authentication using PAP
# client server secret IP addresses
"naba" * "mypassword"
```

可以看出，`chap-secrets` 和 `pap-secrets` 中条目的格式是相同的。每行包含四个字段，顺序如下：

- `client`：此字段包含在认证过程中使用的名称。你从 ISP 处获取此名称。

- `server`：此字段包含你正在对其认证本地系统的远程系统的名称。如果你不知道服务器名称，请输入一个星号（*）以表示任意服务器。

- `secret`：此字段是你系统的 PPP 服务器为了进行身份验证而必须发送给远程系统的机密信息。你从 ISP 处接收此密码。

- `IP addresses`：此可选字段可以包含本地系统在连接到指定服务器时可能使用的 IP 地址列表。通常，此字段留空，因为本地系统通常从服务器获取动态 IP 地址，因此不知道它使用的是哪个 IP 地址。

# 第 2 章：设置局域网

本章内容

- 理解 TCP/IP 网络

- 设置以太网局域网

- 配置 TCP/IP 网络

- 将你的局域网连接到互联网

Linux 内置了对传输控制协议/互联网协议（TCP/IP）网络的支持，大多数现代操作系统（从 Windows 到 Mac OS）也是如此。你可以在许多不同的物理接口上拥有 TCP/IP 网络，例如以太网卡、串行端口和并行端口。

通常，你使用以太网网络作为你的局域网（LAN）——在你的办公室甚至你的家中（如果你恰好在家中有两台或更多系统）。要通过调制解调器连接到远程系统，你使用基于点对点协议（PPP）的 TCP/IP 网络。

本章介绍如何设置以太网网络。即使你只有一台 PC，你可能也需要设置以太网网络接口，以便将你的 PC 连接到使用 DSL 或电缆调制解调器的高速互联网访问。（我在本小册子的第 1 章中介绍了 DSL 和电缆调制解调器。）

## 理解 TCP/IP

如果你用具有四个层级的分层模型来思考，就能最好地理解 TCP/IP 网络。将每个层想象为负责执行特定任务。分层模型描述了数据在物理网络连接和最终用户应用之间的流动。图 2-1 展示了 TCP/IP 的四层网络模型。

![](img/792720823146d68f19fd50c99ebfce4b_301_0.png)

在这个四层模型中，信息总是从一层移动到下一层。例如，当一个应用程序向另一个应用程序发送数据时，数据按以下顺序通过各层：应用层→传输层→网络层→物理层。在接收端，数据从物理层→网络层→传输层→应用层向上流动。

每一层都有自己的一套协议——即约定——来处理和数据格式化数据。如果你将发送数据想象成通过邮政服务寄信，典型的协议就是执行任务的首选动作序列，例如填写信封（先写姓名，然后写街道地址，最后写城市、州和省或其他邮政编码）。

以下是四个层各自的功能，从上到下：

- 应用层：运行用户使用的应用程序，如电子邮件阅读器、文件传输和 web 浏览器。应用层协议包括用于电子邮件的简单邮件传输协议（SMTP）和邮局协议（POP），用于 web 的超文本传输协议（HTTP），以及用于文件传输的文件传输协议（FTP）。应用层协议还有一个端口号，你可以将其视为特定应用的标识符。例如，端口 80 与 HTTP 或 web 服务器相关联。

- 传输层：从一个应用程序向另一个应用程序发送数据。此层中两个最重要的协议是传输控制协议（TCP）和用户数据报协议（UDP）。TCP 保证数据的交付；UDP 只是发送数据，而不确保数据实际到达目的地。

- 网络层：此层负责将数据分组从一个网络传输到另一个网络。如果网络相距较远，数据分组将从一个网络路由到下一个网络，直到到达目的地。此层的主要协议是互联网协议（IP）。

- 物理层：指承载网络中数据包的物理网络硬件（如以太网卡或令牌环卡）。

分层模型的优势在于，每一层只负责其特定的任务，其余部分交给其他层处理。各层可以混合搭配——你可以在任何类型的物理网络介质（从以太网到无线电波（在无线网络中））上运行 TCP/IP 网络。软件也是模块化的，因为每一层都可以通过不同的模块来实现。例如，通常传输层和网络层已经作为操作系统的一部分存在，任何应用程序都可以利用这些层。

## TCP/IP 与互联网

TCP/IP 已成为互联网上首选的协议——互联网是从 ARPAnet 演变而来的*网络的网络*。美国政府的高级研究计划局（ARPA）在 20 世纪 70 年代发起了关于一种新信息传输方式的研究，该方式使用通过网络发送的数据包。结果就是 ARPAnet：一个由互联计算机组成的国家网络。随后，ARPA 获得了“国防”前缀，并成为了 DARPA。在 DARPA 的主持下，TCP/IP 协议作为一种流行的*互连网络*——即网络之间的通信——协议集合脱颖而出。

TCP/IP 之所以蓬勃发展，是因为该协议是开放的。这意味着该协议的技术描述出现在公开文档中，因此任何人都可以在特定的硬件和软件上实现 TCP/IP。

TCP/IP 还取得了巨大进展，因为稳定且可运行的软件已经可用。相比于网络架构和协议的纸质描述，TCP/IP 协议最初就是可运行的软件——而谁又能反驳已经行之有效的方案呢？如今，因此，TCP/IP 主导着互联网。

## IP 地址

当网络上有许多计算机时，你需要一种方式来唯一地识别每一台计算机。在 TCP/IP 网络中，计算机的地址就是 IP 地址。由于 TCP/IP 处理的是互连网络，因此地址基于网络地址和主机地址的概念。你可以将网络地址和主机地址的概念理解为止需要提供两个地址来唯一地识别一台计算机：

- 网络地址：指示计算机所在的网络。

- 主机地址：指示该网络中的一台特定计算机。

### 技术详解

![](img/792720823146d68f19fd50c99ebfce4b_303_0.png)

### 下一代 IP（IPv6）

当 4 字节 IP 地址创建时，可用的地址数量似乎足够。然而现在，4 字节地址正在耗尽。互联网工程任务组（IETF）在 1991 年认识到 IP 地址可能会耗尽，并开始研究下一代 IP 寻址方案。他们将其称为 IPng（Internet Protocol Next Generation 的缩写），并计划最终用它取代旧的 4 字节寻址方案（称为 IPv4，即 IP 版本 4）。



关于 `IPng` 提出了几种替代寻址方案并进行了讨论。最终候选者，使用 128 位（16 字节）地址，被命名为 `IPv6`（即 IP 版本 6）。1995 年 9 月 18 日，`IETF` 宣布 `IPv6` 核心寻址协议集合为 `IETF` 建议标准。如今，有许多 `RFC` 涉及 `IPv6` 的各个方面，包括用于通过以太网传输 `IPv6` 数据包的 `IPv6 over PPP`。

`IPv6` 旨在成为从 `IPv4` 到未来的演进步骤。该建议标准提供了使用旧 `IPv4` 地址的主机与任何新 `IPv6` 主机之间的直接互操作性。其理念是用户可以随时将系统升级到使用 `IPv6`，而网络运营者可以自由地升级其网络硬件以使用 `IPv6`，而不影响当前的 `IPv4` 用户。许多操作系统（包括 `Linux`）正在开发 `IPv6` 的示例实现。有关 `Linux` 中 `IPv6` 的更多信息，请参阅 `www.tldp.org/HOWTO/Linux+IPv6-HOWTO` 上的 Linux IPv6 HOWTO。关于 `IPv6` 的一般信息，请访问 `www.ipv6.org` 上的 `IPv6` 主页。

`IPv6` 的 128 位寻址方案允许总共 $2^{128}$ 即 340,282,366,920,938,463,463,374,607,431,768,211,456 个理论可分配地址！这足以让我们使用一段时间了！

网络地址和主机地址共同构成一个*IP 地址*，它是一个 4 字节（32 位）的值。惯例是将每个*字节*写为十进制值，并在每个数字后面加一个点（.）。因此，你会看到诸如 `132.250.112.52` 这样的网络地址。这种书写 IP 地址的方式称为*点分十进制*或*点分四组*表示法。

### 技术详解

![](img/792720823146d68f19fd50c99ebfce4b_303_1.png)

在十进制表示法中，一个字节（具有 8 个位）可以取 0 到 255 之间的值。因此，有效的 IP 地址在点分十进制表示法中只能使用 0 到 255 之间的数字。

# 互联网服务和端口号

`TCP/IP` 协议套件已成为互联网的*通用语言*，因为任何支持 `TCP/IP` 的系统都可以使用许多标准服务。这些服务通过促进邮件、新闻和网页的传输，使互联网得以运转。这些服务拥有众所周知的名称，例如：

- **DHCP**（动态主机配置协议）用于动态配置计算机上的 `TCP/IP` 网络参数。`DHCP` 主要用于分配动态 IP 地址以及其他用于配置 `TCP/IP` 网络的网络信息（如名称服务器、默认网关和域名）。`DHCP` 服务器监听 67 端口。

- **FTP**（文件传输协议）用于在互联网上的计算机之间传输文件。`FTP` 使用两个端口——数据在 20 端口上传输，控制信息在 21 端口上交换。

- **HTTP**（超文本传输协议）是一种用于在一个系统之间发送文档的协议。`HTTP` 是 Web 的基础协议。默认情况下，Web 服务器和客户端在 80 端口上进行通信。

- **SMTP**（简单邮件传输协议）用于在系统之间交换电子邮件。`SMTP` 使用 25 端口进行信息交换。

- **NNTP**（网络新闻传输协议）用于以存储转发方式在互联网上分发新闻文章。`NNTP` 使用 119 端口。

- **SSH**（安全外壳协议）是一种用于在不安全网络上进行安全远程登录和其他安全网络服务的协议。`SSH` 使用 22 端口。

- **TELNET** 用于当互联网上一台系统上的用户登录到另一台系统时。（用户必须提供有效的用户 ID 和密码才能登录到远程系统。）`TELNET` 默认使用 23 端口，但 `TELNET` 客户端可以连接到任何端口。

- **SNMP**（简单网络管理协议）用于管理互联网上所有类型的网络设备。与 `FTP` 类似，`SNMP` 使用两个端口：161 和 162。

- **TFTP**（简单文件传输协议）用于将一个系统中的文件传输到另一个系统。（它通常被 X 终端和无盘工作站用于从网络上的另一个主机下载启动文件。）`TFTP` 数据传输发生在 69 端口。

（通过网关连接多个以太网段。）要设置以太网局域网，你需要为每台 PC 配备一块以太网卡。`Linux` 支持 PC 使用的各种以太网卡。

以太网是物理数据传输机制的良好选择，原因如下：

- ✦ 以太网是一项成熟的技术，自 20 世纪 80 年代初以来一直使用。

- ✦ 以太网提供良好的数据传输速率：通常为每秒 1000 万位（10 Mbps），尽管现在已有 100 Mbps 以太网和千兆以太网（1,000 Mbps）可用。

- ✦ 以太网硬件通常内置于 PC 中，或可以相对较低的成本安装。（PC 以太网卡成本约为 10 – 20 美元。）

- ✦ 使用无线以太网，你可以轻松地将笔记本电脑 PC 连接到你的以太网局域网，而无需到处铺设线缆。（有关无线以太网的更多信息，请参阅本小册子的第 3 章。）

## 以太网如何工作

那么是什么让以太网得以运行？从根本上说，这与任何对话的工作原理相同：倾听和轮流发言。

![](img/792720823146d68f19fd50c99ebfce4b_305_0.png)

在以太网网络中，一段中的所有系统都连接到同一根线缆。由于只使用一根线缆，因此使用协议来发送和接收数据，因为在任何时刻线缆上只能存在一个数据包。以太网局域网使用一种称为**载波侦听多路访问/冲突检测**（`CSMA/CD`）的数据传输协议，以在所有计算机之间共享单根传输线缆。计算机中的以太网卡遵循 `CSMA/CD` 协议来发送和接收以太网数据包。

`CSMA/CD` 协议背后的理念类似于你在聚会上交谈的方式。你倾听停顿（这就是侦测载波），并在没人说话时发言。如果你和另一个人同时开始说话，你们都会意识到问题所在（这就是冲突检测）并暂停片刻；然后其中一个人再次开始说话。正如你所知，一切都会顺利解决。

在以太网局域网中，每块以太网卡都会检查线缆上的信号——这就是载波侦听部分。如果信号电平低，以太网卡就会在线缆上发送其数据包；数据包包含关于发送者和预期接收者的信息。局域网上的所有以太网卡都监听信号，接收者接收到数据包。如果两块网卡同时发送数据包，

电缆中的信号电平超过阈值，网卡得知发生了碰撞。（即两个数据包在同一时间被发送。）两张网卡都会等待一段随机时间后再次发送它们的数据包。

以太网于20世纪70年代初由罗伯特·梅特卡夫（Robert M. Metcalfe）在施乐帕洛阿尔托研究中心（Xerox Palo Alto Research Center, `PARC`）发明。在20世纪80年代，以太网由三家公司的合作努力进行了标准化：数字设备公司（Digital Equipment Corporation, `DEC`）、英特尔（Intel）和施乐（Xerox）。使用公司名称的首字母，该以太网标准被称为`DIX`标准。后来，`DIX`标准被纳入电气与电子工程师协会（Institute of Electrical and Electronics Engineers, `IEEE`）开发的802系列标准中。最终的以太网规范正式称为`IEEE 802.3 CSMA/CD`，但人们仍习惯称之为以太网。

以太网以*数据包*（也称为*帧*的离散块）形式发送数据。你不需要过多纠结于以太网数据包的内部细节，只需注意6字节的源地址和目的地址。每个以太网控制器在物理层都有一个唯一的6字节（48位）地址；每个数据包都必须包含一个。

### 以太网电缆

每当听到专家谈论以太网时，你还会听到一些令人困惑的术语，用于描述承载数据的电缆。以下是快速概览。

![](img/792720823146d68f19fd50c99ebfce4b_306_0.png)

最初的以太网标准使用了粗同轴电缆，直径近半英寸。这种布线被称为*粗缆*或*粗以太网*，尽管`IEEE 802.3`标准称之为*`10Base5`*。该标识意味着几层含义：数据传输率为每秒10兆比特（10 Mbps）；传输是*基带*（这意味着电缆的信号传输能力专门用于传输以太网数据包），且电缆总长度不得超过500米。*粗缆*价格昂贵，且电缆较为笨重。除非你是技术历史爱好者，否则你完全不必关心`10Base5`电缆。

![](img/792720823146d68f19fd50c99ebfce4b_306_1.png)

如今，其他几种形式的以太网电缆更为流行。粗以太网电缆的替代方案是*细缆*或*`10Base2`*，它使用细长的柔性同轴电缆。*细缆*以太网段最长可达185米。另一种更近期的替代方案是非屏蔽双绞线（UTP）上的以太网，即*`10BaseT`*。支持更高传输速率的较新以太网电缆选项包括用于100 Mbps以太网的`100BaseT4`、`100BaseT2`和`100BaseTX`，以及用于千兆以太网的`1000BaseT`。电子工业协会/电信工业协会（`EIA/TIA`）定义了以下五类屏蔽和非屏蔽双绞线电缆：

- **1类线（Cat 1）：** 传统电话电缆。

- **2类线（Cat 2）：** 认证用于高达4 Mbps数据传输的电缆。

- **3类线（Cat 3）：** 可传输高达16 MHz频率信号的电缆。3类线是旧企业网络中最常见的布线类型，通常包含四对线。如今已被视为过时。

- **4类线（Cat 4）：** 可传输高达20 MHz频率信号的电缆。4类线并不常见。如今已被视为过时。



- **5类线（Cat 5）：** 可传输高达100 MHz频率信号的电缆。5类线通常有四对铜线。5类非屏蔽双绞线（UTP）是当今新安装中最流行的电缆。此类电缆正被5e类（增强型5类）取代。

- **5e类线（Cat 5e）：** 类似于5类线，但在技术参数方面有所改进，如近端串扰和衰减。5e类电缆支持10BaseT、100BaseT4、100BaseT2、100BaseTX和1000BaseT以太网。如今，5e类是最低可接受的布线标准。

- **6类线（Cat 6）：** 类似于5e类线，但能够传输高达250 MHz频率的信号。6类电缆支持所有现有以太网标准，并支持千兆以太网标准1000BaseTX，该标准在每个方向上使用两对线，而不同于在5e类电缆上运行的1000BaseT以太网使用全部四对线。

要设置10BaseT或100BaseT以太网网络，你需要一个以太网集线器——带有RJ-45插口的硬件盒子。（这些插口看起来像大的电话插口。）你通过将双绞线（通常是5类线）从每台PC的以太网卡连接到该集线器来构建网络。你可以花大约40美元购买一个4端口的10BaseT/100BaseT集线器。图2.2展示了一个典型的小型10BaseT/100BaseT以太网局域网，你可以在小型办公室或家中设置。

当你从本书附带的DVD-ROM上安装任何Linux发行版到一台连接了以太网卡的PC时，Linux内核会自动检测以太网卡并安装适当的驱动程序。安装程序还允许你设置TCP/IP网络。

Linux内核在每次启动时都会加载以太网卡的驱动程序。要验证以太网驱动程序已加载，请在终端窗口中输入以下命令：

```
dmesg | grep eth0
```

![](img/792720823146d68f19fd50c99ebfce4b_307_0.png)

图 2-2：你可以使用以太网集线器来设置10BaseT/100BaseT以太网局域网。

![](img/792720823146d68f19fd50c99ebfce4b_308_0.png)

在我的一台Linux PC上，输入该命令时得到的输出如下：

```text
eth0: RealTek RTL8139 at 0xf0e20000, 00:0c:76:f4:38:1b, IRQ 161
eth0: Identified 8139 chip type 'RTL-8101'
eth0: link up, 100Mbps, full-duplex, lpa 0x45e1
eth0: no IPv6 routers present
```

你应该看到类似的内容，显示你的以太网卡名称和其他相关信息。

# 配置 TCP/IP 网络

当你在安装Linux期间设置TCP/IP网络时，安装程序会使用你提供的信息准备所有适当的配置文件。这意味着你通常不需要手动配置网络。然而，大多数Linux发行版都配有GUI工具来配置网络设备，以防需要更改某些设置。本节介绍了几个与特定发行版相关的示例。对于其他所有发行版，步骤类似。

Fedora Core附带了一个图形化网络配置工具，你可以使用它来添加新的网络接口或更改信息，如名称服务器和主机名。要启动GUI网络配置工具，请选择 系统 > 管理 > 网络。如果你未以root身份登录，系统会提示你输入root密码。网络配置工具显示一个选项卡式对话框，如图2-3所示。然后，你可以通过对话框顶部出现的四个选项卡来配置网络。配置完网卡后，你可以选择该设备并点击“激活”按钮来开启以太网。

在大多数情况下，你可以设置网卡使其能够自动获取IP地址（当以太网卡连接到DSL或电缆调制解调器时，通常就是这种情况），方法是使用DHCP。如果你的网络没有DHCP服务器（通常内置于路由器中），你必须为网卡指定一个IP地址。如果你正在运行私有网络，你可以使用192.168.0.0到192.168.255.255范围内的IP地址。（其他地址范围保留用于私有网络，但对于大多数需求而言，此范围已足够。）

在SUSE中，选择 主菜单 > 系统 > YaST 以打开YaST控制中心。在提示时输入root密码。然后在窗口左侧选择“网络设备”，在右侧选择“网卡”。随后，YaST会弹出一个窗口（如图2-4所示），显示已配置的网卡以及检测到的任何新网卡的详细信息。然后你可以配置任何新的网卡。

- 图 2-3：在Fedora Core中，使用此网络配置工具配置以太网网络。

![](img/792720823146d68f19fd50c99ebfce4b_309_0.png)

## 将局域网连接到互联网

如果你的局域网（LAN）中有几台电脑，你可以使用数字用户线路（DSL）或电缆调制解调器将整个局域网连接到互联网。基本上，你可以让局域网中的所有电脑共享高速的 DSL 或电缆调制解调器连接。

在本小册子的第 1 章中，我解释了如何设置 DSL 或电缆调制解调器。在本节中，我简要说明如何局域网连接到互联网，以便所有电脑都能访问互联网。

通过 DSL 或电缆调制解调器将局域网连接到互联网最便捷的方法是购买一种名为 DSL/电缆调制解调器 NAT 路由器的硬件设备，该设备带有 4 口或 8 口的以太网集线器。NAT 代表网络地址转换（Network Address Translation），NAT 路由器可以将许多私有 IP 地址转换为单个外部已知的 IP 地址。以太网集线器部分对你来说表现为一组 RJ-45 以太网端口，你可以在此连接电脑以组建局域网。换句话说，除了 DSL 或电缆调制解调器之外，你只需要额外购买一个盒子即可。

图 2-5 展示了如何通过带有内置以太网集线器的 NAT 路由器将局域网连接到互联网。当然，为了使这种场景生效，你需要具备 DSL 或电缆调制解调器连接，并且你需要与电话公司签约办理 DSL 服务，或与电缆提供商签约办理电缆互联网服务。

当将局域网连接到互联网时，NAT 路由器充当局域网的网关。NAT 路由器还会动态地向局域网中的电脑提供 IP 地址。因此，在每台电脑上，你都需要设置网络选项以动态获取 IP 地址。

![](img/792720823146d68f19fd50c99ebfce4b_311_0.png)

你的局域网可以混合使用各种电脑：有些可能运行 Linux，有些可能运行微软 Windows 或其他任何支持 TCP/IP 的操作系统。在配置网络设置时，请记住选择让 Linux 自动通过 DHCP 获取 IP 地址设置和 DNS 信息的选项。

![](img/792720823146d68f19fd50c99ebfce4b_311_1.png)

图 2-5：通过带有内置以太网集线器的 NAT 路由器将局域网连接到互联网。

# 第 3 章：添加无线以太网局域网

### 本章内容

- 理解无线以太网网络
- 设置无线硬件
- 配置无线网络

如果你的局域网中有笔记本电脑——或者你不想拉一堆杂乱的电线来连接电脑到局域网——你可以选择使用无线以太网网络。在典型场景中，你拥有连接互联网的电缆调制解调器或 DSL 连接，并希望连接一台或多台带有无线网卡的笔记本电脑，通过电缆或 DSL 调制解调器访问互联网。本章向你展示了如何设置无线网络，以便连接以太网局域网并访问互联网。

### 理解无线以太网网络

你可能听说过 Wi-Fi。Wi-Fi 代表无线保真网络（Wireless Fidelity network）——一种类似有线以太网网络的短距离无线网络。由一个名为 IEEE（电气与电子工程师学会，Institute of Electrical and Electronics Engineers）的组织制定的若干标准定义了 Wi-Fi 网络工作原理的技术细节。制造商使用这些标准来设置你可以购买以组建无线网络的组件，无线网络也简称为 WLAN。

直到 2003 年中，两个流行的 IEEE 标准——802.11a 和 802.11b——适用于无线以太网网络。这两个标准于 1999 年最终确定。第三个标准——802.11g——于 2003 年夏季由 IEEE 最终确定。所有这些标准都指定了无线以太网网络在物理层如何工作。你不需要纠结于所有这些标准的每一个细节来组建无线网络，但了解一些相关细节是有好处的，这样你就可以为无线网络购买合适的设备。

- **802.11b：** 工作在 2.4 GHz 无线电频段（2.4 GHz 至 2.4835 GHz），最多支持三个不重叠的频段或信道。每个信道支持的最大比特率为 11 Mbps。802.11b 的一个缺点是 2.4 GHz 频段非常拥挤——许多设备（如微波炉、无绳电话、医疗和科学设备，以及蓝牙设备）都在 2.4 GHz 频段内工作。尽管如此，802.11b 在企业网络和家用网络中非常流行。

- **802.11a：** 工作在 5 GHz 无线电频段（5.725 GHz 至 5.850 GHz），最多支持八个不重叠的信道。每个信道支持的最大比特率为 54 Mbps。5 GHz 频段不像 2.4 GHz 频段那样拥挤，但 5 GHz 频段在欧洲未获准使用。符合 802.11a 标准的产品在市场上有售，一些无线接入点被设计用于处理 802.11a 和 802.11b 两种连接。



### 802.11g
在 2.4 GHz 频段支持最高 54 Mbps 的数据速率。（与 802.11b 使用的频段相同。）802.11g 通过使用一种名为 OFDM（正交频分复用，orthogonal frequency-division multiplexing）的技术来实现更高的比特率，802.11a 也使用该技术。符合 802.11g 标准的设备已在市场上销售。802.11g 因其与 802.11b 工作在相同频段但承诺提供高得多的数据速率，且与 802.11b 设备向后兼容而引起了轰动。供应商目前提供的接入点可同时支持 802.11b 和 802.11g 连接标准。

在所有情况下，用户实际看到的最大数据传输吞吐量要低得多，因为使用该无线电信道的所有用户都要共享信道的容量。此外，随着用户电脑与无线接入点之间距离的增加，数据传输速率会降低。

正在开发第三个标准——802.11n，它将支持 2.4 GHz 或 5 GHz 频段下的 100 Mbps 数据速率，具体取决于这两个提案中哪一个获得所需的会员批准。两个实力相当的团队——分别被称为 TGn Sync（任务组 n 同步）和 WWiSE（全球频谱效率）——各自制定了 802.11n 标准的提案。TGn Sync 提议使用 5 GHz 频段，即 802.11a 使用的频段，而 WWiSE 的提案则是针对 802.11b 和 g 使用的 2.4 GHz 频段。两个团队都同意，需要某种形式的多输入多输出（MIMO，发音为 MY-mo）天线技术才能实现 100 Mbps 的数据速率。（一些 MIMO 接入点已经开始在市场上发售。）在 2005 年 5 月的投票中，TGn Sync 的提案获得了多数票，但未达到作为初稿基础所需的 75% 票数。你可以在 `http://grouper.ieee.org/groups/802/11/Reports/tgn_update.htm` 阅读关于 IEEE 802.11n 项目的最新消息。

![](img/792720823146d68f19fd50c99ebfce4b_314_0.png)

如果你正在购买新的无线接入点，请选择 802.11g 型号。802.11g 接入点也可以与较旧（且速度较慢）的 802.11b 设备进行通信。你也可以考虑 MIMO 接入点，它支持多个 802.11 标准并实现提高吞吐量和扩大范围的技术。

![](img/792720823146d68f19fd50c99ebfce4b_314_1.png)

要了解有关无线以太网的更多信息，请访问 `www.wi-fi.org`，这是 Wi-Fi 联盟的主页。Wi-Fi 联盟是一个成立于 1999 年的非营利国际协会，旨在认证基于 IEEE 802.11 标准的无线局域网产品的互操作性。

### 理解基础架构模式和 Ad hoc 模式

802.11 标准为无线以太网网络定义了两种操作模式：*ad hoc*（临时对等）和 *infrastructure*（基础架构）。*Ad hoc 模式*仅仅是指两台或更多无线以太网卡在没有接入点的情况下相互通信。

*基础设施模式*指的是所有无线以太网卡通过接入点相互通信并与有线局域网通信的方法。对于本章的讨论，我假设你将无线以太网卡设置为基础设施模式。在配置文件中，这种模式被称为*管理模式*。

### 理解有线等效隐私（WEP）

802.11 标准包括有线等效隐私（Wired Equivalent Privacy，WEP），用于保护无线通信免受窃听。WEP 依赖于在移动站（如带有无线以太网卡的笔记本电脑）和接入点（也称为*基站*）之间共享的 40 位或 104 位密钥。该密钥用于在数据包传输之前对其进行加密，并且会执行完整性检查，以确保数据包在传输过程中未被篡改。

802.11 标准并未解释如何建立共享密钥。在实践中，大多数无线局域网使用在移动站和接入点之间共享的单一密钥。然而，这种方法在诸如大学校园这样的环境中扩展性较差，因为密钥是与所有用户共享的——你知道与数百人分享一个*秘密*是什么滋味。这就是为什么通常 WEP 不用于大型无线网络，如大学中的那种。在这种无线网络中，你必须使用其他安全方法，如 SSH（Secure Shell），来登录远程系统。然而，WEP 在你的家庭无线网络中是很好的选择。

## WEP 流密码是否足够好？

WEP 使用 RC4 加密算法，该算法被称为*流密码*。此类算法通过接收一个短密钥并生成一个无限长的伪随机位流来工作。在发送数据之前，发送站点在伪随机位和代表数据包的位之间执行异或（exclusive-OR）操作，当两个位不同时结果为 1，相同时为 0。接收方拥有相同的密钥副本，并生成相同的伪随机位流——并将这个伪随机流与接收到的位执行相同的异或操作。这样就能重新生成原始的、未加密的数据包。

这种流密码方法存在一些问题。如果加密数据流中的某一位发生翻转（从 0 变为 1 或反之），解密输出中对应的那一位也会翻转，这有助于攻击者推导出加密密钥。此外，窃听者如果截获了用相同密钥流编码的两个消息，就可以生成这两个原始消息的异或值。这一知识足以发起最终可破解加密的攻击。

为了对抗这些弱点，WEP 使用了一些防御措施：

- **完整性校验（IC）字段：** 为确保数据包在传输过程中未被修改，WEP 在每个数据包中使用了完整性校验字段。
- **初始化向量（IV）：** 为避免使用相同的密钥流加密两条消息，WEP 使用一个 24 位的 IV，它与共享密钥一起生成不同的 RC4 密钥，以便为每个数据包产生不同的 RC4 密钥。IV 本身也包含在数据包中。

专家称这些防御措施实施得并不好，使得 WEP 无效。IC 和 IV 有两个主要问题：

1. 完整性校验字段通过使用一种称为 32 位循环冗余校验（CRC-32）的校验和算法来实现；该校验和随后作为数据包的一部分被包含在内。不幸的是，攻击者可以在加密消息中翻转任意位，并正确调整校验和，使得生成的消息看起来有效。
2. 24 位 IV 是以明文（未加密）形式发送的。只有 $2^{24}$ 个可能的初始化向量（对于高速机器来说并非大挑战），而且在用完所有这些向量后它们必须被重复使用。换句话说，在发送 $2^{24}$ 即 16,777,216 个数据包后，IV 会被重复。这个数字听起来可能很多，但请考虑一个繁忙的接入点的情况，它以 11 Mbps 的速率发送 1,500 字节的数据包。每个数据包有 $8 \times 1,500 = 12,000$ 位。这意味着该接入点每秒发送 $11,000,000 / 12,000 = 916$ 个数据包。以这个速率，接入点在 $16,777,216 / 916 = 18,315$ 秒或 5 小时内发送 16,777,216 个数据包。这意味着 IV 在 5 小时后被重用，且由于许多消息小于 1,500 字节，时间可能更短。因此，攻击者有充分的机会收集两条用相同密钥流加密的消息——并执行*统计攻击*（即非常快速地尝试可能的*组合*）来解密消息。

WEP 有其弱点，但它总比没有好。你可以将其用于较小的无线局域网，在这些网络中，在所有无线站点间共享同一密钥并非繁重任务。

![](img/792720823146d68f19fd50c99ebfce4b_316_0.png)

正在进行的努力旨在为无线网络提供比 WEP 更好的安全性。2003 年，Wi-Fi 联盟发布了一个名为 **Wi-Fi 保护访问（WPA）** 的规范，取代了现有的 WEP 标准并通过一些改进增强了安全性。例如，与使用固定密钥的 WEP 不同，WPA 标准使用 **临时密钥完整性协议（TKIP）**，它通过网络传输的每 10K 数据生成新的密钥。这使得 WPA 更难被破解。2004 年，Wi-Fi 联盟推出了 WPA 的后续版本，称为 **Wi-Fi 保护访问 2（WPA2）** —— WPA 安全的第二代）。WPA2 基于最终的 **IEEE 802.11i** 标准，该标准使用具有数字证书的公钥加密以及认证、授权和计费 **RADIUS** (**远程认证拨号用户服务**) 服务器，为无线以太网提供更好的安全性。WPA2 使用 **高级加密标准（AES）** 进行数据加密。

## 设置无线硬件

要设置无线连接，你需要一个无线接入点和每台 PC 中的无线网卡。你也可以在拥有无线网卡的两台或多台 PC 之间设置自组网（ad hoc）无线网络，但这只是这些 PC 之间的独立无线局域网。在本节中，我重点介绍你希望建立一个无线连接到已有通过电缆调制解调器或 DSL 连接到互联网的局域网的场景。

除了无线接入点外，你还需要一个电缆调制解调器或 DSL 连接到互联网，以及前几章中描述的 **NAT** 路由器和集线器。图 3-1 展示了通过现有电缆调制解调器或 DSL 连接访问无线互联网的典型设置。

如图 3-1 所示，局域网包含有线和无线 PC。在此示例中，电缆或 DSL 调制解调器通过 NAT 路由器和集线器将局域网连接到互联网。带有无线网卡的笔记本电脑通过连接在集线器其中一个 RJ-45 端口上的无线接入点连接到局域网。要将台式 PC 连接到此无线网络，你可以使用 USB 无线网卡（它连接到 USB 端口）。

![](img/792720823146d68f19fd50c99ebfce4b_316_1.png)



如果你尚未购买电缆或 DSL 连接的 NAT 路由器和集线器，请考虑购买具有内置无线接入点的路由器和集线器。

![](img/792720823146d68f19fd50c99ebfce4b_317_0.png)

> 图 3-1：混合有线和无线以太网局域网连接到互联网的典型连接。
>
> 局域网（LAN）中的 PC。每台 PC 必须有一个 `10BaseT` 以太网卡。

## 配置无线接入点

配置无线接入点涉及以下任务：

- 为无线网络设置名称。（技术术语是 `ESSID`。）
- 设置无线接入点与无线网卡通信的频率或信道。接入点和网卡必须使用相同的信道。
- 决定是否使用加密。
- 如果将使用加密，则设置加密密钥中的位数以及加密密钥的值。对于加密密钥，24 位是接入点内部的；你只需指定剩余的位。因此，对于 64 位加密，你必须指定一个 40 位密钥，即 10 个十六进制数字。（十六进制数字是 0-9 的整数或 A-F 的字母。）对于 128 位加密密钥，你指定 104 位，即 26 个十六进制数字。
- 设置无线网卡在连接到接入点时必须使用的访问方法。你可以选择开放访问或共享密钥。开放访问方法是典型的（即使使用加密时也是如此）。
- 将无线接入点设置为基础设施（管理）模式（因为这是将无线网卡连接到现有以太网局域网的方式）。

配置无线接入点的具体方法取决于制造商和型号；供应商提供了配置无线接入点的说明。你通常通过 Windows PC 上的图形客户端应用程序来进行配置。如果你启用了加密，请记下加密密钥；你必须为笔记本或台式机上的每个无线网卡指定相同的密钥。

### 配置无线局域网

在你的 Linux 笔记本电脑上，PCMCIA 或 PC 卡管理器识别无线网卡并加载该卡的适当驱动程序。Linux 将无线网卡视为另一个以太网设备并为其分配设备名称，如 `eth0` 或 `eth1`。如果你已经在笔记本电脑中有一个以太网卡，该卡将获取 `eth0` 设备名称，而无线 PC 卡将变成 `eth1` 设备。

你必须配置某些参数以使无线网卡能够与无线接入点通信。例如，你必须指定分配给接入点的无线网络名称，且加密设置必须与接入点上的设置相匹配。通常可以使用图形网络配置工具来配置所有内容，该工具在你的 Linux 发行版中可用——只需选择无线网络选项并填入所需信息。

例如，在 Fedora Core 中，从 GNOME 桌面选择 系统→管理→网络。然后点击工具栏上的“新建”以添加网络设备。然后你可以选择无线设备并进入一个可以配置无线连接的窗口。（见图 3-2。）特别是，将模式设置为管理，指定无线网络名称（该你所要连接的网络），并设置加密密钥（如果有）。你可以将获取 IP 地址的选项设置为 DHCP（一种用于从网络服务器获取网络配置参数（包括 IP 地址）的协议）。完成后，返回到“网络配置”工具的主窗口，选择新的无线设备并点击“激活”按钮。如果一切顺利，无线网络将在片刻之后就绪并正常运行。

![](img/792720823146d68f19fd50c99ebfce4b_319_0.png)

在 Fedora Core 中，“网络配置”工具会将你的无线网络设置保存在一个文本文件中。该文本文件的名称取决于无线网卡设备的名称。如果无线网卡设备名称为 `eth0`，配置将存储在文本文件 `/etc/sysconfig/network-scripts/ifcfg-eth0` 中。如果无线设备名称为 `eth1`，文件则为 `/etc/sysconfig/network-scripts/ifcfg-eth1`。此配置文件包含无线网络卡的多种设置。表 3-1 解释了这些设置的含义。以下是我运行 Fedora Core 的笔记本电脑上 `/etc/sysconfig/network-scripts/ifcfg-eth1` 文件的一个经过稍作编辑的版本：

```text
IPV6INIT=no
USERCTL=no
PEERDNS=yes
TYPE=Wireless
DEVICE=eth1
HWADDR=00:02:2d:8c:f9:c4
BOOTPROTO=dhcp
BOOTBOOT=no
DHCP_HOSTNAME=
NAME=
ESSID='HOME'
CHANNEL=6
MODE=Managed
RATE=auto
```

在 Fedora Core 中，加密密钥是单独存储的。对于设备名称为 `eth1` 的无线以太网卡，加密密钥存储在 `/etc/sysconfig/network-scripts/keys-eth1` 文件中。例如，以下是该文件在我示例中的内容：

```text
KEY=1fdf3fdfe
```

![](img/792720823146d68f19fd50c99ebfce4b_320_0.png)

请注意，40 位密钥的十六进制数字为 10 位（例如，`1fdf-3fde-fe`），而 104 位密钥则为 26 位十六进制数字。实际上，密钥分别是 64 位和 128 位，但加密算法会自动生成密钥的 24 位，因此你只需要指定剩余的位数。不用说，密钥越长，加密就越安全。

![](img/792720823146d68f19fd50c99ebfce4b_320_1.png)

如果你曾在 Fedora Core 中手动编辑无线以太网配置文件中的参数，请键入以下命令以在编辑配置文件后重新激活无线网络接口：

```text
/etc/init.d/network restart
```

### 表 3-1 Fedora Core 中无线以太网网络接口配置文件中的设置

| 此参数 | 含义 |
| :--- | :--- |
| `BOOTPROTO` | 用于获取接口 IP 地址的协议名称。对于以太网接口，它是 `dhcp` 或 `bootp`。 |
| `CHANNEL` | 频道号（在美国和加拿大之间为 1 到 14）。必须与为无线接入点设置的频道相同。在管理模式下，你不需要指定频道。 |
| `DEVICE` | 无线以太网网络接口的设备名称（第一个接口为 `eth0`，第二个为 `eth1`，依此类推）。 |
| `ESSID` | 扩展服务集（ESS）标识符，也称为无线网络名称。它对大小写敏感，必须与为无线接入点指定的名称相同。请将名称置于单引号内（例如，'HOME'）。 |
| `HWADDR` | 无线网卡的硬件地址（也称为 MAC 地址）（六对以冒号分隔的十六进制数；例如，00:02:2d:8c:19:c4）。无线网卡的设备驱动程序会自动检测此地址。 |
| `IPV6INIT` | 当设置为 *yes* 时，此参数初始化无线接口的 IPv6 配置。如果你不使用 IPv6，请将其设置为 *no*。 |
| `MODE` | 无线网卡的工作模式。对于通过无线接入点连接的典型网络，请设置为 **Managed**（管理）。 |
| `NAME` | 你无线网络的昵称。如果你未指定，主机名将用作昵称。 |
| `ONBOOT` | 设置为 *yes* 以在启动时激活无线接口；否则，设置为 *no*。 |
| `PEERDNS` | 设置为 *yes* 以启用接口修改系统的 `/etc/resolv.conf` 文件，以使用从 DHCP 服务器（即为主机提供 IP 地址的同一服务器）获取的 DNS 服务器。如果将此参数设置为 *no*，则 `/etc/resolv.conf` 文件保持不变。 |
| `RATE` | 无线连接的比特率（设置为以下选项之一：1M、2M、5.5M、11M 或 *auto*）。M 代表 Mbps 或百万比特每秒。设置为 *auto* 以使用最大可能的传输速率。 |
| `TYPE` | 对于无线网络接口，设置为 **Wireless**。 |
| `USERCTL` | 当设置为 *yes* 时，非 root 用户可以控制该设备。将其设置为 *no*，以便只有 *root* 可以控制该设备。 |

在 SUSE Linux 中，使用 YaST 来配置无线网络。SUSE 将无线配置参数存储在一个文件名以 `ifcfg-wlan` 开头的文件中，后面跟随一个数字（如 `0` 或 `1`），具体取决于无线网卡接口的序列号。该配置文件存储在 `/etc/sysconfig/network` 目录中。以下是 SUSE Linux 中配置文件的典型无线配置参数列表：

```text
WIRELESS_MODE='Managed'
WIRELESS_ESSID='HOME'
WIRELESS_NICK=''
WIRELESS_RATE='auto'
WIRELESS_AUTH_MODE='open'
WIRELESS_KEY_0='0123-4567-89'
```

![](img/792720823146d68f19fd50c99ebfce4b_321_0.png)

要检查无线网卡接口的状态，请键入以下命令：

```text
iwconfig
```

以下是一台装有无线以太网卡片的 Fedora Core 笔记本电脑的典型输出。（其他 Linux 发行版的输出应该类似。）



```
lo        no wireless extensions.

eth0      no wireless extensions.

sit0      no wireless extensions.

eth1      IEEE 802.11b  ESSID:"HOME"  Nickname:"localhost.localdomain"
Mode:Managed  Frequency:2.437 GHz  Access Point: 00:30:AB:06:E2:5D
Bit Rate=1 Mb/s  Sensitivity:1/3
Retry limit:4  RTS thr:off  Fragment thr:off
  Encryption key:1FDF-3FDE-FE  Security mode:open
  Power Management:off
  Link Quality=51/92  Signal level=-40 dBm  Noise level=-91 dBm
  Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:27
  Tx excessive retries:0  Invalid misc:0  Missed beacon:0
```

在此，`eth1` 接口指的是无线网卡。我编辑了加密密钥和其他一些参数以隐藏这些细节，但示例输出展示了你在无线链路工作时通常看到的内容。

# 第 4 章：管理网络

## 本章内容

- 了解 TCP/IP 配置文件
- 检查 TCP/IP 网络
- 在启动时配置网络

与 Linux 中的几乎其他所有内容一样，TCP/IP 设置就是准备大量的配置文件（你可以使用任何文本编辑器编辑的文本文件）。这些配置文件中的大多数位于 `/etc` 目录中。Linux 安装程序试图通过隐藏 TCP/IP 配置文件的细节来提供帮助。然而，如果你知道文件的名称及其用途，必要时手动编辑这些文件会更容易。

## 发现 TCP/IP 配置文件

你可以在安装 Linux 时配置 TCP/IP 网络。但是，如果你想有效地管理网络，你需要熟悉 TCP/IP 配置文件，以便在必要时编辑这些文件。（例如，如果你想检查名称服务器是否正确指定，你必须了解 `/etc/resolv.conf` 文件，该文件存储名称服务器的 IP 地址。）

表 4-1 总结了基本的 TCP/IP 配置文件。我将在接下来的几个部分中描述这些配置文件。

| 此文件 | 包含以下内容 |
| :--- | :--- |
| `/etc/hosts` | 本地网络的 IP 地址和主机名，以及你经常访问的其他系统 |
| `/etc/networks` | 网络的名称和 IP 地址 |
| `/etc/host.conf` | 如何将主机名转换为 IP 地址的说明 |
| `/etc/resolv.conf` | 名称服务器的 IP 地址 |
| `/etc/hosts.allow` | 哪些系统可以访问你系统上的 Internet 服务的说明 |
| `/etc/hosts.deny` | 哪些系统必须被拒绝访问你系统上的 Internet 服务的说明 |
| `/etc/nsswitch.conf` | 如何将主机名转换为 IP 地址的说明 |

### `etc/hosts`

`etc/hosts` 文本文件包含本地网络的 IP 地址和主机名列表。在缺乏名称服务器的情况下，系统上的任何网络程序都会查阅此文件以确定与主机名对应的 IP 地址。你可以将 `etc/hosts` 视为当地的电话簿，你可以在其中查找本地主机的 IP 地址（代替电话号码）。

以下是某个系统的 `etc/hosts` 文件，展示了典型局域网中其他主机的 IP 地址和名称：

```
127.0.0.1           localhost       localhost.localdomain
# Other hosts on the LAN
192.168.0.100       lnbp933
192.168.0.50        lnbp600
192.168.0.200       lnbp200
192.168.0.233       lnbp233
192.168.0.40        lnbp400
```

如示例所示，文件中的每一行都以 IP 地址开头，后跟该 IP 地址对应的主机名。（对于给定的 IP 地址，可以拥有多个主机名。）

### `etc/networks`

`/etc/networks` 是另一个包含网络名称和 IP 地址的文本文件。这些网络名称通常用于路由命令（`/sbin/route`）中，以便通过名称而非 IP 地址来指定网络。

如果你的 Linux 计算机没有 `/etc/networks` 文件，请不要惊慌。你的 TCP/IP 网络在没有此文件的情况下也能正常工作。事实上，Linux 安装程序并不创建 `/etc/networks` 文件。

### `etc/host.conf`

Linux 使用一个特殊的`库`（即一组计算机代码），称为`解析器库`（resolver library），来获取与主机名对应的 IP 地址。`/etc/host.conf` 文件指定了如何`解析`名称（即如何将名称转换为数字 IP 地址）。典型的 `/etc/host.conf` 文件可能包含以下行：

```
order hosts, bind
multi on
```

`/etc/host.conf` 文件中的条目告诉解析器库使用哪些服务（以及使用的顺序）来解析名称。

`order` 选项指示服务的顺序。示例条目告诉解析器库首先查阅 `/etc/hosts` 文件，然后检查名称服务器以解析名称。

![](img/792720823146d68f19fd50c99ebfce4b_326_0.png)

使用 `multi` 选项来指示 `/etc/hosts` 文件中的主机是否可以拥有多个 IP 地址。拥有多个 IP 地址的主机被称为`多宿主机`（multithomed），因为多个 IP 地址的存在意味着该主机拥有多个网络接口。（实际上，该主机`同时`存在于多个网络中。）

### `/etc/resolv.conf`

`/etc/resolv.conf` 文件是另一个由`解析器`（即确定主机名 IP 地址的库）使用的文本文件。以下是 `/etc/resolv.conf` 文件的一个示例：

```
    nameserver  192.168.0.1  # dhcp: eth0
    search       rnockv01.md.comcast.net
```

`nameserver` 行提供了你的域的名称服务器的 IP 地址。如果你有多个名称服务器，请在单独的行中列出它们。它们将按照在文件中出现的顺序被查询。

`search` 行告诉解析器如何搜索主机名。例如，当试图定位主机名 `myhost` 时，示例中的 `search` 指令会让解析器首先尝试 `myhost.rnrockv01.md.comcast.net`，然后是 `myhost.md.comcast.net`，最后是 `myhost.comcast.net`。

![](img/792720823146d68f19fd50c99ebfce4b_326_1.png)

如果你的网络没有名称服务器，你可以安全地忽略此文件。即使你可能无法通过名称（除了 `/etc/hosts` 文件中列出的那些）来引用主机，TCP/IP 仍然可以工作。

### `/etc/hosts.allow`

`/etc/hosts.allow` 文件指定哪些主机被允许使用运行在你系统上的 Internet 服务（如 TELNET 和 FTP）。此文件在某些 Internet 服务启动之前会被查阅。只有当 `hosts.allow` 文件中的条目隐含请求主机的使用被允许时，服务才会启动。

`/etc/hosts.allow` 中的条目采用 `servername:IP address` 格式，其中 `server` 指提供特定 Internet 服务的程序名称，而 `IP address` 标识被允许使用该服务的主机。例如，如果你希望本地网络中（具有网络地址 192.168.0.0）的所有主机都能访问 TELNET 服务（由 `in.telnetd` 程序提供），请在 `/etc/hosts.allow` 文件中添加以下行：

```
in.telnetd:192.168.0.
```

管理网络

## **302** *发现 TCP/IP 配置文件*

如果你想让所有本地主机都能访问所有 Internet 服务，你可以使用 `ALL` 关键字并重写该行如下：

```
ALL:192.168.0.
```

最后，为了向所有主机开放所有 Internet 服务，你可以将 IP 地址替换为 `ALL`，如下所示：

```
ALL: ALL
```

你也可以使用主机名来代替 IP 地址。

![](img/792720823146d68f19fd50c99ebfce4b_327_0.png)



要了解 `/etc/hosts.allow` 文件中条目的详细语法，请在终端窗口的 shell 提示符下输入 `man hosts.allow`。

## `/etc/hosts.deny`

此文件与 `/etc/hosts.allow` 正好相反。`hosts.allow` 指定哪些主机可以访问你系统上的 Internet 服务（如 TELNET 和 TFTP），而 `hosts.deny` 文件标识必须拒绝服务的主机。如果在 `/etc/hosts.allow` 文件中没有适用于请求主机的规则，则会查阅 `/etc/hosts.deny` 文件。如果 `hosts.deny` 文件中有适用于该主机的规则，则拒绝服务。

`/etc/hosts.deny` 文件中的条目与 `/etc/hosts.allow` 文件中的条目格式相同；它们采用 `server: IP address` 格式，其中 `server` 指提供特定 Internet 服务的程序名称，而 `IP address` 标识不允许使用该服务的主机。

如果你已经在 `/etc/hosts.allow` 文件中设置了条目以允许特定主机访问，你可以在 `/etc/hosts.deny` 中放置以下行来拒绝所有其他主机访问你系统上的任何服务：

```
ALL: ALL
```

![](img/792720823146d68f19fd50c99ebfce4b_327_1.png)

要了解 `/etc/hosts.deny` 文件中条目的详细语法，请在终端窗口的 shell 提示符下输入 `man hosts.deny`。

## `/etc/nsswitch.conf`

此文件称为 `名称服务切换`（NSS）文件，指定了解析器库、NIS、NIS+ 和本地配置文件（如 `/etc/hosts` 和 `/etc/shadow`）等服务如何交互。

NIS 和 NIS+ 是 `网络信息系统`——另一种类型的名称查找服务。较新版本的 Linux 内核使用 `/etc/nsswitch.conf` 文件来确定优先级：本地配置文件、DNS（域名服务）等这样的服务，还是 NIS。

作为一个例子，`/etc/nsswitch.conf` 文件中的以下 hosts 条目表示解析器库首先尝试 `/etc/hosts` 文件，然后尝试 NIS+，最后尝试 DNS：

```
hosts: files nisplus dns
```

![](img/792720823146d68f19fd50c99ebfce4b_328_0.png)

> 通过在终端窗口中输入 `man nsswitch.conf`，你可以找到更多关于 `/etc/nsswitch.conf` 文件的信息。

## 检查 TCP/IP 网络

配置好以太网和 TCP/IP 后（无论是在 Linux 安装期间还是之后通过网络配置工具或命令运行），你可以使用各种网络应用程序而不会遇到太多问题。万一你遇到问题，Linux 包含一些工具来帮助你监控和诊断问题。

## 检查网络接口

使用 `/sbin/ifconfig` 命令查看当前配置的网络接口。`ifconfig` 命令用于配置网络接口（即将 IP 地址与网络设备关联）。如果你运行 `ifconfig` 时不带任何命令行参数，该命令将显示当前网络接口的信息。以下是输入 `/sbin/ifconfig` 时的典型输出：

```
eth0 Link encap:Ethernet HWaddr 00:08:7A:E5:C1:60
      inet addr:192.168.0.7 Bcast:192.168.0.255 Mask:255.255.255.0
      inet6 addr: fe80::208:74ff:fe85:c160/64 Scope:Link
      UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
      RX packets:612051 errors:0 dropped:0 overruns:0 frame:0
      TX packets:574137 errors:0 dropped:0 overruns:0 carrier:0
      collisions:0 txqueuelen:1000
      RX bytes:99834031 (95.2 MiB) TX bytes:76034821 (72.5 MiB)
      Interrupt:10 Base address:0x3000

eth1 Link encap:Ethernet HWaddr 00:02:2D:8C:F8:C5
      inet addr:192.168.0.9 Bcast:192.168.0.255 Mask:255.255.255.0
      inet6 addr: fe80::202:2dff:fe8c:f8c5/64 Scope:Link
      UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
      RX packets:3833 errors:0 dropped:0 overruns:0 frame:0
      TX packets:1242 errors:0 dropped:0 overruns:0 carrier:0
      collisions:0 txqueuelen:1000
      RX bytes:560194 (547.0 KiB) TX bytes:250287 (244.4 KiB)
      Interrupt:3 Base address:0x100

lo Link encap:Local Loopback
      inet addr:127.0.0.1 Mask:255.0.0.0
      inet6 addr: ::1/128 Scope:Host
      UP LOOPBACK RUNNING MTU:16436 Metric:1
      RX packets:2456 errors:0 dropped:0 overruns:0 frame:0
      TX packets:2456 errors:0 dropped:0 overruns:0 carrier:0
      collisions:0 txqueuelen:0
      RX bytes:2891581 (2.7 MiB) TX bytes:2891581 (2.7 MiB)
```

## 304 检查 TCP/IP 网络

此输出表明，该系统当前有三个网络接口处于活动状态——回环接口（`lo`）和两个以太网卡（`eth0` 和 `eth1`）。对于每个接口，你可以看到 IP 地址，以及已送达和已发送的数据包统计信息。如果 Linux 系统有一个活动的拨号 PPP 连接，你还会在输出中看到 `ppp0` 接口的条目。

### 检查 IP 路由表

另一个网络配置命令 `/sbin/route` 在不带命令行参数运行时也提供状态信息。如果你在检查到另一台主机（通过 IP 地址指定）的连接时遇到问题，请检查 IP 路由表，看看是否指定了默认网关。然后，检查网关的路由表，以确保通往外部网络的路径出现在该路由表中。

`/sbin/route` 命令的典型输出如下所示：

| Destination | Gateway | Genmask | Flags | Metric | Ref | Use | Iface |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 192.168.0.0 | * | 255.255.255.0 | U | 0 | 0 | 0 | eth0 |
| 192.168.0.0 | * | 255.255.255.0 | U | 0 | 0 | 0 | eth1 |
| 169.254.0.0 | * | 255.255.0.0 | UG | 0 | 0 | 0 | eth1 |
| default | 192.168.0.1 | 0.0.0.0 | UG | 0 | 0 | 0 | eth0 |

如该路由表所示，本地网络使用 `eth0` 和 `eth1` 以太网接口，而默认网关是 `eth0` 以太网接口。默认网关是一种处理发往除 Linux 系统所在网络之外任何网络的数据包的路由设备。在此示例中，发往以 192.168.0 开头之外的任何网络地址的数据包都发送到网关——192.168.0.1。网关将这些数据包转发到其他网络（当然，前提是网关已连接到另一个网络，最好是互联网）。

### 检查与主机的连接性

要检查与特定主机的网络连接，请使用 `ping` 命令。`ping` 是一个广泛使用的 TCP/IP 工具，它使用一系列互联网控制消息协议（ICMP，发音为 `EE-comp`）消息。ICMP 提供了一种回声消息，每台主机都会对此做出响应。利用 ICMP 消息及其回复，`ping` 可以判断其他系统是否存活，并计算与该系统通信的往返延迟。

以下示例展示了如何运行 `ping` 以查看我网络上的某台系统是否存活：

```
ping 192.168.0.1
```



以下是该命令在我的家庭网络上显示的内容：

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

在 Linux 中，`ping`会持续运行，直到你按`Ctrl+C`停止它；然后它会显示摘要统计信息，表明在两个系统之间发送数据包通常所需的时间。在某些系统上，`ping`仅报告远程主机是否存活。然而，你仍然可以通过使用适当的命令行参数来获取计时信息。

![](img/792720823146d68f19fd50c99ebfce4b_330_0.png)

`ping`命令依赖于许多防火墙配置为阻止的 ICMP 消息。因此，`ping`并不总是有效，也不再是测试网络连接性的可靠方法。如果针对特定主机的`ping`失败，不要假设该主机已宕机或未连接到网络。通常，你可以成功使用`ping`来检查局域网内的连接性。

### 检查网络状态

要检查网络状态，请使用`netstat`命令。此命令显示各种类型（如 TCP 和 UDP 连接）的网络连接状态。你可以通过输入`netstat -i`快速查看接口的状态，其输出类似于以下内容：

```
Kernel Interface table
Iface  MTU Met RX-OK RX-ERR RX-DRP RX-OVR  TX-OK  TX-ERR  TX-DRP  TX-OVR  Flg
eth0   1500 0  63175  0     0       1  574695   0     0       0     BMRU
eth1   1500 0    4298  0     0       0   1375    0     0       0     BMRU
lo     16436 0    3255  0     0       0   3255    0     0       0     LRU
```

在这种情况下，输出显示了回环和以太网接口的当前状态。表 4-2 解释了各列的含义。

**表 4-2：内核接口表中各列的含义**

| 列 | 含义 |
| :--- | :--- |
| **Iface** | 接口的名称 |
| **MTU** | 最大传输单元——数据包可以包含的最大字节数 |
| **Met** | 接口的度量值——一个数字，表示路由软件在决定通过哪个接口发送数据包时使用的距离（以跳数计） |
| **RX-OK, TX-OK** | 接收（RX）或传输（TX）的无错误数据包数量 |
| **RX-ERR, TX-ERR** | 有错误的数据包数量 |
| **RX-DRP, TX-DRP** | 丢弃的数据包数量 |
| **RX-OVR, TX-OVR** | 因溢出而丢失的数据包数量 |
| **Flg** | A=接收多播；B=允许广播；D=开启调试；L=回环接口（注意 lo 上的标志）；M=接收所有数据包；N=避免尾部；O=此接口无 ARP；P=点对点接口；R=接口正在运行，U=接口已启用 |

`netstat`选项的另一种有用形式是`-t`，它显示所有活动的 TCP 连接。以下是在一台 Linux 电脑上输入`netstat -t`的典型结果：

```
Active Internet connections (w/o servers)
Proto Recv-Q Send-O Local Address  Foreign Address  State
tcp      0       0 localhost:1024  localhost:1024    ESTABLISHED
tcp      0       0 localhost:1024  localhost:2654    ESTABLISHED
tcp      0       0 LMNREZXAN.rnccrkvl:s.sh  192.168.0.6:1577 ESTABLISHED
```

在这种情况下，输出列显示协议（Proto）、接收和发送队列中的字节数（Recv-Q, Send-O）、主机名:服务格式的本地 TCP 端口（Local Address）、远程端口（Foreign Address）以及连接状态。

输入`netstat -ta`可查看所有 TCP 连接——既包括活动的连接，也包括你的 Linux 系统正在监听但尚未建立连接的那些。例如，以下是`netstat -ta`命令的典型输出：

```
Active Internet connections (servers and established)
Proto Recv-Q Send-O Local Address  Foreign Address  State
tcp      0       0 *:32769           *.*           LISTEN
tcp      0       0 *:mysql           *.*           LISTEN
tcp      0       0 *:sunrpc          *.*           LISTEN
tcp      0       0 *:ftp             *.*           LISTEN
tcp      0       0 localhost.localdomain:ipp *.*           LISTEN
tcp      0       0 *:telnet          *.*           LISTEN
tcp      0       0 localhost.localdomain:5335 *.*           LISTEN
tcp      0       0 localhost.localdomain:smtp  *.*         LISTEN
tcp      0       0 192.168.0.9:45876  www.redhat.com:http ESTABLISHED
tcp      0       0 192.168.0.9:45877    www.redhat.com:http ESTABLISHED
tcp      0       0 192.168.0.9:45875    www.redhat.com:http ESTABLISHED
tcp      0       0 *:sash               *:*            LISTEN
tcp      0       0 ::ffff:192.168.0.3:4932 ::ffff:192.168.0.3:4932 ESTABLISHED
```

### 嗅探网络数据包

嗅探网络数据包——听起来像是什么非法行为，不是吗？绝非如此。嗅探只是指查看 TCP/IP 网络数据包。其概念是捕获所有网络数据包，以便你稍后进行检查。

如果你想嗅探 TCP/IP 数据包，可以使用`tcpdump`，这是 Linux 自带的一个命令行实用工具。顾名思义，它转储（打印）TCP/IP 网络数据包的报头。

要使用`tcpdump`，请以 root 身份登录，并在终端窗口中输入`tcpdump`命令。通常，你希望将输出保存到一个文件中，然后稍后检查该文件。否则，`tcpdump`开始输出结果，这些结果只是迅速掠过窗口。例如，要在名为`tdot`的文件中捕获 1,000 个数据包并尝试将 IP 地址转换为名称，请键入以下命令：

```
tcpdump -a -c 1000 > tdot
```

捕获完 1,000 个数据包后，`tcpdump`退出。然后你可以检查输出文件`tdot`。它是一个文本文件，所以你只需在文本编辑器中打开它，或者键入`more tdot`来查看捕获的数据包。

为了满足你的好奇心，以下是`tcpdump`典型输出中的几行内容：



```
20:05:57.723621 arp who-has 192.168.0.1 tell LNREDCXAN.nrocov01.md.comcast.net
20:05:57.723843 arp reply 192.168.0.1 is-at 0:9:5b:44:78:fc
20:06:01.733633 LNREDCXAN.nrocov01.md.comcast.net:1038 > 192.168.0.6.auth: S  536321100:536321100(0) win 5840 <mss 1460, sackOK,timestamp 7030060
0,nop,window 0> (DF)
20:06:02.137022 LNREDCXAN.nrocov01.md.comcast.net.ftp > 192.168.0.6.1596: P 1:72 (71) ack 1 win 5840
20:06:02.935335 192.168.0.6.1596 > LNREDCXAN.nrocov01.md.comcast.net.ftp: . ack 72 win 65464 (DF)
20:06:05.462481 LNREDCXAN.nrocov01.md.comcast.net.ftp > 192.168.0.6.1596: P 1:112 (11) ack 72 win 65464 (DF)
20:06:05.462595 LNREDCXAN.nrocov01.md.comcast.net.ftp > 192.168.0.6.1596: . ack 12 win 5840 (DF)
20:06:05.465344 LNREDCXAN.nrocov01.md.comcast.net.ftp > 192.168.0.6.1596: P 72:105(33) ack 12 win 5840 (DF)
... lines deleted...
```

输出确实提供了一些关于系统运行状况的线索：每一行显示了一个网络数据包的信息。每一行以时间戳开头，随后是该数据包的详细信息（例如它的来源和目的地）。我在此不打算详细解释这些细节，但你可以通过 `man tcpdump` 命令了解一些详细信息（更重要的是，看看你还能以其他方式使用 `tcpdump`）。

如果 Debian 中没有安装 `tcpdump`，请输入 `apt-get install tcpdump` 进行安装。

你可以在 Linux 中使用另一个名为 Ethereal 的数据包嗅探器。要了解有关 Ethereal 的更多信息，请访问 `www. ethereal.com`。

# 在启动时配置网络

让系统在每次启动时自动启动网络是有意义的。要实现这一点，各种启动脚本必须包含适当的命令。除了配置你的网络（在安装期间或之后使用网络配置工具）之外，你不需要做任何特殊的事情。然而，如果网络在启动时出现问题，你可以通过检查本节提到的文件来排查故障。

在 Debian、MEPIS、Ubuntu 和 Xandros 中，`/etc/network/interfaces` 文件描述了系统中可用的网络接口，`/sbin/ifup` 命令在启动系统时激活这些接口。以下是 Debian 系统中典型的 `/etc/network/interfaces` 文件内容：

```
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).
# The loopback network interface
auto lo
iface lo inet loopback
# The primary network interface
auto eth0
iface eth0 inet dhcp
```

`auto eth0` 行表明，你可以使用命令 `ifup -a`（由系统启动脚本调用）在初始化时启动以太网接口。`ifup eth0 inet dhcp` 行将以太网标识为通过动态主机配置协议（DHCP）配置的 TCP/IP 网络接口。

在 Fedora Core 中，网络激活脚本使用 `/etc/sysconfig` 目录中一组文本来激活网络接口。例如，脚本会检查 `/etc/sysconfig/network` 文件中定义的变量，以决定是否激活网络。在 `/etc/sysconfig/network` 中，你会看到一行包含 `NETWORKING` 变量，如下所示：

```
NETWORKING=yes
```

只有当 `NETWORKING` 变量设置为 `yes` 时，网络才会激活。`/etc/sysconfig/network-scripts` 目录中的许多脚本激活特定的网络接口。例如，用于激活以太网接口 `eth0` 的配置文件是 `/etc/sysconfig/network-scripts/ifcfg-eth0`。以下是典型的 `/etc/sysconfig/network-scripts/ifcfg-eth0` 文件包含的内容：

```
DEVICE=eth0
BOOTPROTO=dhcp
HWADDR=00:08:74:E5:C1:06
ONBOOT=yes
TYPE=Ethernet
```

`DEVICE` 行提供网络设备名称。`BOOTPROTO` 变量设置为 `dhcp`，表明 IP 地址是通过使用 DHCP 动态获取的。`ONBOOT` 变量声明此网络接口是否在 Linux 启动时激活。如果你的 PC 装有以太网卡，并且你想在启动时激活 `eth0` 接口，`ONBOOT` 必须设置为 `yes`。当然，`/etc/sysconfig/network-scripts` 目录中的配置文件 `ifcfg-eth0` 只有在你 PC 装有以太网卡并且 Linux 内核检测到并加载了该卡的特定驱动程序时才有效。

![](img/792720823146d68f19fd50c99ebfce4b_334_0.png)

在 SUSE 中，网络信息保存在 `/etc/sysconfig/network` 目录中，文件名以 `ifcfg` 开头。对于以太网接口，配置文件名以 `ifcfg-eth-id` 开头，后跟以太网卡的唯一硬件地址。以下是典型的以太网配置文件中的关键行：

```
BOOTPROTO='dhcp'
STARTMODE='auto'
```

`BOOTPROTO='dhcp'` 行表明该接口使用 DHCP 设置，而 `STARTMODE='onboot'` 意味着该接口在系统启动时初始化。

# 第四卷

# 互联网

# 第五波

作者：Rich Tennant

![](img/792720823146d68f19fd50c99ebfce4b_336_0.png)

> “在互联网之前，我们只在本地吹牛。但现在，有了我们的网站，我们在全世界范围内都在吹牛。”

# 内容速览

- 第 1 章：在 Linux 中发送电子邮件和即时消息....313
- 第 2 章：浏览网页....333
- 第 3 章：阅读新闻组和使用 RSS 源....345
- 第 4 章：使用 FTP....361

# 第 1 章：在 Linux 中发送电子邮件和即时消息

## 本章内容

- ✓ 了解电子邮件
- ✓ 盘点邮件阅读器和 IM（即时消息）客户端
- ✓ 介绍 Evolution
- ✓ 介绍 Thunderbird
- ✓ 介绍 KMail
- ✓ 使用 Gaim 和 Kopete 进行即时消息

电子邮件（e-mail）是互联网的主要支柱之一。电子邮件很棒，因为你可以与互联网上的任何人交换消息和文档。人们使用互联网最常见的方式之一就是通过电子邮件与朋友、熟人、爱人和陌生人保持联系。你可以向远在千里之外的朋友发送一条消息，并在几分钟内收到回复。本质上，你可以从互联网主机向世界上任何地方发送消息，该消息通常会在几分钟内到达目的地——这是普通邮件（也称为*蜗牛邮件*，名副其实）做不到的。

我喜欢电子邮件，因为我不必玩*打手机*的游戏，在那种游戏中，两个人可以互相留下看似无穷无尽的手机留言，却从未成功联系上。当我发送电子邮件消息时，它会在收件人的邮箱中等待，以便收件人在方便时阅读。我想我也更喜欢反面——当人们给我发电子邮件时，我可以在*我*方便时阅读并回复。

Linux 附带了几个邮件客户端——也称为*邮件阅读器*——可以从你的互联网服务提供商（ISP）下载邮件。你也可以使用这些邮件客户端阅读和发送电子邮件。在本章中，我提到了 Linux 中可用的几个邮件客户端，并简要介绍了其中几个。当你掌握了一个之后，你就可以轻松使用任何邮件阅读器。

# 理解电子邮件

![](img/792720823146d68f19fd50c99ebfce4b_339_0.png)



还有另一种*保持联系*的方式，更符合当今年轻一代的需求。我说的是*IM*——即时消息。IM 基本上是一对一的聊天，Linux 包含用于 AOL Instant Messenger（或 AIM）以及 Jabber、ICQ、MSN Messenger、Yahoo!、Gadu-Gadu、IRC（互联网中继聊天）和 SMS（短消息服务或短信）等其他即时消息协议的 IM 客户端。我在本章中简要描述了几种 IM 客户端。

电子邮件消息被发送至主机上的一个用户名（*主机*只是对在线计算机的别称）。这意味着如果 John Doe 使用用户名 `jdoe` 登录，发往他的电子邮件地址为 `jdoe`。唯一其他用于唯一标识收件人的信息是收件人系统的全限定域名。因此，如果 John Doe 的系统名为 `someplace.com`，他的完整电子邮件地址就变成了 `jdoe@someplace.com`。给定该地址，互联网上的任何人都可以向 John Doe 发送电子邮件。

## MUA 和 MTA 的工作原理

有两种类型的邮件软件如下：

- **邮件用户代理 (MUA)** 是邮件阅读器的别称——一个用于阅读邮件消息、撰写回复和创建新消息的客户端。通常，邮件用户代理使用 POP3 或 IMAP4 协议从邮件服务器获取消息。POP3 是*邮局协议版本 3*，IMAP4 是*互联网消息访问协议版本 4*。Linux 附带 Balsa、Thunderbird、KMail 和 Evolution 等邮件用户代理。

- **邮件传输代理 (MTA)** 是邮件服务器的别称，它实际发送和接收邮件消息文本。邮件传输使用的具体方法取决于底层网络。在 TCP/IP 网络中，邮件传输代理使用*简单邮件传输协议* (SMTP) 投递邮件。Linux 包含 `sendmail`，这是一个强大且流行的 TCP/IP 网络邮件传输代理。

图 1-1 展示了当 Alice 向 Bob 发送电子邮件消息时，MUA 和 MTA 如何协同工作。（如果你不知道的话，使用*Alice* 和 *Bob* 来解释电子邮件和密码学是惯例——随便拿起一本关于密码学的书，你就会明白我的意思。）你可能已经知道，互联网总是被描绘成一团云——互联网的边界如此模糊，用云来代表它似乎很合适。（或者是因为没有人知道它从哪里开始，又到哪里结束？）

# 理解电子邮件

![](img/792720823146d68f19fd50c99ebfce4b_340_0.png)

图 1-1 中的场景很典型。爱丽丝（Alice）和鲍勃（Bob）都通过 ISP（互联网服务提供商）连接到互联网，并通过各自的 ISP 收发电子邮件。当爱丽丝输入并发送一条消息时，她的邮件用户代理（MUA）会使用简单邮件传输协议（SMTP）将消息发送给她 ISP 的邮件传输代理（MTA）。发送方 MTA 随后使用 SMTP 将该消息发送给接收方 MTA——即鲍勃的 ISP 的 MTA。当鲍勃连接到互联网时，他的 MUA 使用 POP3（或 IMAP4）协议从他的 ISP 的 MTA 下载该消息。这就是邮件在互联网上流转的方式——从发送方 MUA 到发送方 MTA，再到接收方 MTA，最后到接收方 MUA。

### 邮件消息的增强功能

邮件消息过去是纯文本（现在大多数仍如此），但如今许多邮件包含的内容远不止文本。当今电子邮件的两个典型特性是：

- **附件**：如今许多邮件都包含附件文件，可以是文档、图像等任何内容。收件人可以将附件保存到磁盘，也可以直接从邮件阅读器中打开。不幸的是，黑客试图将病毒和蠕虫植入你电脑的方式之一，就是将它们放在附件中。（如果说有什么可以安慰的话，大多数基于 Windows 的病毒和蠕虫在 Linux 下无法运行。）

- **HTML 消息**：邮件消息可以是*HTML*（超文本标记语言），这是一种用于排版网页的语言。当你使用功能完善的邮件阅读器阅读 HTML 邮件时，消息会以完整华丽的形式呈现，拥有精美的字体和嵌入的图形。

![](img/792720823146d68f19fd50c99ebfce4b_341_0.png)

虽然 HTML 邮件很好看，但如果你使用的是基于文本的邮件阅读器，它们并不会正确显示。在文本邮件阅读器中，HTML 邮件显示为一堆乱码（实际上就是 HTML 代码）。

![](img/792720823146d68f19fd50c99ebfce4b_341_1.png)

如果你有 ISP 账户，你只需要一个邮件客户端即可访问你的电子邮件。在这种情况下，你的电子邮件存储在 ISP 的服务器上，邮件阅读器在你运行时下载邮件。在开始从 ISP 的邮件服务器阅读邮件之前，你需要进行一些设置。设置基本上要求你输入从*ISP*获取的信息——邮件服务器名称、服务器类型（例如 POP3）、你的用户名和密码。

### 清点 Linux 中的邮件阅读器和 IM 客户端

曾经大多数邮件阅读器都是文本程序，但时过境迁。现在，邮件阅读器是图形化应用程序，能够轻松显示 HTML 消息和处理附件。它们易于使用；如果你会使用其中一个，那么几乎可以肯定你能使用现有的任何图形化邮件阅读器。（Linux 自带几个邮件阅读器；不妨尝试几个，看看哪一个最适合你的需求。）

*IM*（即时消息）是一种较新的现象，但 Linux 努力保持与时俱进，因此它自带两个 IM 客户端，可以与各种 IM 协议配合工作。*表 1-1* 概述了 Linux 中主要的邮件阅读器和 IM 客户端。

| 软件 | 描述 |
| --- | --- |
| KMail | 支持 POP3 和 IMAP4 的 KDE 电子邮件客户端 |
| Thunderbird | Mozilla 邮件客户端的重新设计版，它是 Mozilla 开源网络浏览器（Netscape Communicator 的开源版本）的一部分 |
| Evolution | 包含电子邮件、日历、联系人管理和在线任务列表的个人信息管理（PIM）工具 |
| Gaim | GNOME 的 IM 客户端，支持多种即时消息协议，如 AIM、ICQ、Yahoo!、MSN、Gadu-Gadu 和 Jabber |
| Kopete | KDE 的 IM 客户端，支持多种消息协议，如 Jabber、ICQ、AIM、MSN、Yahoo!、IRC、Gadu-Gadu 和 SMS |

![](img/792720823146d68f19fd50c99ebfce4b_342_0.png)

如果你在发行版中没有看到特定的邮件或 IM 客户端，很可能你可以轻松地从互联网下载并安装它。

# 在 Linux 中发送电子邮件

每个 Linux 发行版的图形用户界面桌面都有一两个默认的电子邮件客户端。GNOME 桌面通常提供 Evolution，而 KDE 桌面则选择 KMail。GNOME 和 KDE 桌面通常都自带 Mozilla 作为网络浏览器，且 Mozilla 也包含一个邮件客户端。

![](img/792720823146d68f19fd50c99ebfce4b_342_1.png)

Debian 包含 KMail 和 Evolution。Fedora Core 和 Ubuntu 提供 Evolution 作为默认邮件客户端。MEPIS 和 SUSE 使用 KMail 作为默认邮件阅读器，而 Xandros 同时提供 KMail 和 Thunderbird 邮件。

在接下来的章节中，我将简要介绍 Evolution、Thunderbird 邮件和 KMail。所有邮件客户端都很直观易用，因此你只需简单了解即可开始有效地使用它们。

### 介绍 Evolution

我听说 Evolution 有很多优点，所以我想从它开始。还有什么比直接上手更好的方法呢！

![](img/792720823146d68f19fd50c99ebfce4b_342_2.png)

在 Fedora Core 中，你可以在 GNOME 或 KDE 桌面上通过选择“主菜单”→“互联网”→“Evolution 电子邮件”来启动 Evolution。（在 Debian 中，我必须选择“应用程序”→“Debian 菜单”→“应用”→“网络”→“Evolution”。）

当你第一次启动 Evolution 时，Evolution 设置向导窗口会出现，如图 1-2 所示。

![](img/792720823146d68f19fd50c99ebfce4b_343_0.png)

在欢迎屏幕中点击**下一步（Forward）**，设置向导将引导你完成以下步骤：

1. **在身份屏幕中输入你的名字和电子邮件地址，然后点击“下一步”按钮。**

   例如，如果你的电子邮件地址是 `jdoe@someplace.com`，那就是你要输入的内容。

2. **设置接收电子邮件的选项并点击“下一步”。**

   选择邮件下载协议类型——POP 或 IMAP。然后提供邮件服务器的名称（例如，`mail.comcast.net`）。当 Evolution 第一次连接到邮件服务器时，系统会提示你输入密码。

3. **提供有关接收电子邮件的更多信息——检查邮件的频率以及是否将消息保留在服务器上——然后点击“下一步”。**

   通常，你希望下载消息并从服务器删除它们（否则 ISP 会因邮件堆积而抱怨）。



## 设置发送电子邮件选项

4. 设置发送电子邮件的以下选项，完成后点击“下一步”：
   - 将服务器类型选择为 `SMTP`。
   - 输入服务器名称，例如 `smtp.comcast.net`。
   - 如果服务器要求登录，请选择“服务器需要身份验证”复选框。
   - 输入你的用户名——即你登录 ISP 邮件服务器时使用的用户名。（通常，发送邮件时无需登录；只有在接收——下载——邮件消息时才需要登录。）

5. 指示是否希望此电子邮件账户成为你的默认账户，并（如果愿意）给此电子邮件账户起一个描述性名称；点击“下一步”。

6. 通过点击地图来设置你的时区；点击“下一步”。

7. 点击“应用”以完成 Evolution 设置。

完成一次性设置后，Evolution 打开其主窗口，如图 1-3 所示。

![](img/792720823146d68f19fd50c99ebfce4b_344_0.png)

Evolution 的主显示区域在垂直方向上分为两个窗口：左侧是一个窄面板，其中一列排列着多个快捷按钮——邮件、联系人、日历、任务——右侧是一个较大的面板，Evolution 在此处显示与当前选中的快捷图标相关信息。在图 1-3 中，Evolution 显示邮件的收件箱。

你可以点击左侧窗口中的快捷按钮切换到不同的视图。这些按钮提供了访问 PIM 所有必要组件的途径——电子邮件、日历、任务列表和联系人。你会发现 Evolution 中的所有这些任务都很直观易操作。

要访问你的电子邮件，请点击收件箱图标。Evolution 打开你的收件箱，如图 1-4 所示。如果你启用了定期自动检查邮件的功能，Evolution 会提示你输入邮件密码并下载你的邮件。电子邮件收件箱看起来与任何其他邮件阅读器的收件箱非常相似，例如 Outlook Express 的收件箱。

要阅读消息，请在收件箱的上窗格中点击该消息，消息文本将出现在下窗格中。图 1-4 显示了一条带有图像文件附件的消息。

要回复当前消息，请点击工具栏上的回复按钮。会弹出一个消息编辑窗口。你可以编写回复，然后点击工具栏上的发送按钮发送回复。简单，不是吗？

**图 1-4：** 在 Evolution 收件箱中阅读你的电子邮件。

![](img/792720823146d68f19fd50c99ebfce4b_345_0.png)

要发送新邮件，请点击 Evolution 工具栏上的“新消息”按钮。此时会出现一个新邮件撰写窗口。你可以在该窗口中输入邮件内容，完成撰写后，点击“发送”。

Evolution 附带了丰富的在线帮助。从 Evolution 菜单中选择“帮助”→“目录”，即可在一个窗口中显示《Evolution 2.0 用户指南》。然后你就可以在该窗口中阅读用户指南。

### 介绍 Thunderbird

Thunderbird 是 Mozilla Mail 的重新设计版本，这是随 Mozilla 网络浏览器附带的一款邮件和新闻阅读器——Mozilla 是 Netscape Communicator 的开源继任者。

Xandros 预装了 Thunderbird，但某些发行版默认不安装 Thunderbird。不过，你可以轻松地安装 Thunderbird。例如，在 Debian 中，在终端窗口中输入 `su -` 并输入 `root` 密码，然后输入 `apt-get install mozilla-thunderbird` 来安装 Thunderbird Mail。

安装完成后，你可以从 Debian 的 GNOME 桌面环境中选择“应用程序”→“Debian 菜单”→“应用程序”→“网络”→“Mozilla Thunderbird”来启动 Thunderbird。当 Thunderbird 运行时，它会启动“账户向导”（如图 1-5 所示），并提示你输入有关电子邮件账户的信息。

![](img/792720823146d68f19fd50c99ebfce4b_346_0.png)

**图 1-5**：在 Thunderbird 的“账户向导”中输入你的电子邮件账户信息。

选择“电子邮件账户”单选按钮并点击“下一步”。“账户向导”随后将引导你完成以下步骤：

- 1. **输入你的身份信息** — 你的名字和完整的电子邮件地址，例如 `jdoe@someplace.com` — 然后点击“下一步”。
- 2. **提供有关你的 ISP 邮件服务器的信息** — 协议类型（POP 或 IMAP）以及传入和传出服务器名称 — 然后点击“下一步”。

传入服务器是 POP 或 IMAP 服务器，而传出服务器是你发送邮件时所使用的服务器。（即 SMTP 服务器。）

- 3. **输入你的 ISP 提供给你的用户名**；点击“下一步”。
- 4. **输入一个你希望用来标识此账户的名称**，然后点击“下一步”。

这个名称仅用于 Thunderbird，因此你可以随意选择，例如“我的家庭账户”。

“账户向导”将显示你输入的信息摘要。

- 5. **核实信息。如果信息正确**，点击“完成”。否则，点击“返回”并更正错误。

设置好电子邮件账户后，Thunderbird 的主窗口会出现并显示收件箱的内容。很快会弹出一个对话框，询问你的电子邮件密码。Thunderbird 需要你的密码来从 ISP 下载电子邮件消息。输入你的密码并点击“确定”。

Thunderbird 下载你的邮件并以熟悉的格式显示它们。要阅读邮件，点击该邮件，完整文本将显示在下方窗口中，如图 1-6 所示。

Thunderbird 使用直观。大多数时候，你只需点击工具栏按钮即可处理电子邮件消息的大部分操作。以下是每个工具栏按钮的功能：

- **获取邮件**：从你的电子邮件账户下载邮件。（你可以设置任意数量的账户。）
- **撰写**：打开一个窗口，你可以在其中撰写并发送邮件。
- **通讯簿**：打开“通讯簿”窗口，你可以在其中维护联系人列表。
- **回复**：打开一个窗口，你可以在其中回复正在阅读的消息的发送者。
- **回复全部**：打开一个窗口，用于向正在阅读的消息收件人列表中的所有人发送回复。
- **转发**：在当前窗口中显示该邮件，以便你可以将其转发给其他人。
- **删除**：删除选定的邮件。
- **垃圾邮件**：将选定的邮件标记为垃圾邮件。（你可以将选定的邮件标记为垃圾邮件，并选择“工具”→“垃圾邮件控制”来屏蔽类似的邮件。）
- **打印**：打印选定的邮件。
- **停止**：停止当前与邮件服务器的传输。

如果你使用任何图形用户界面邮件阅读器——从 Microsoft Outlook Express 到 Novell GroupWise——你会发现类似的一组工具栏按钮。在以下各节中，我将描述如何执行一些常见的电子邮件相关任务。

图 1-6：你可以从 Thunderbird 阅读和发送电子邮件。

![](img/792720823146d68f19fd50c99ebfce4b_348_0.png)

## 管理收件箱

Thunderbird 下载你的传入邮件并将其存储在收件箱文件夹中。你可以在左侧的窄窗口中看到组织的文件夹。（参见图 1-6。）每个你设置的电子邮件账户都有一组文件夹。默认情况下，你有以下文件夹：

- **收件箱**：保存此电子邮件账户的所有传入消息。
- **未发送消息**：包含尚未发送到邮件服务器的消息。
- **草稿**：包含你保存为草稿的消息。（点击邮件撰写窗口上的“保存”按钮可以将内容保存为草稿。）
- **已发送**：保存你成功发送的所有消息。
- **回收站**：包含你删除的消息。（要清空回收站文件夹，请从 Thunderbird 邮件菜单中选择“文件”→“清空回收站”。）

你可以创建其他文件夹以更好地整理你的邮件。要创建文件夹，请执行以下操作：

- 1. **右键点击 Thunderbird 窗口左侧的“本地文件夹”标签，并从出现的菜单中选择“新建文件夹”。**

  “新建文件夹”对话框出现。
- 2. **填写文件夹名称并选择你要放置文件夹的位置。点击“确定”。**

  新文件夹出现在 Thunderbird 的左侧窗口中。然后你可以将消息拖放到该文件夹中。

当你从左侧窗口选择一个文件夹时，Thunderbird 会在右侧上方的窗口中显示该文件夹的内容。列表通常按日期排序，最新的消息显示在列表的末尾。如果你想按其他方式排序——例如按发件人或按主题——只需点击该列标题，Thunderbird 就会根据该列对列表进行排序。

## 撰写和发送消息

要发送电子邮件，你可以撰写新消息或回复你正在阅读的消息。发送电子邮件的一般步骤如下：

- 1. **要回复消息，在阅读消息时点击工具栏上的“回复”或“回复全部”按钮。要撰写新消息，点击工具栏上的“撰写”按钮。要转发消息，点击“转发”按钮。**

  出现邮件撰写窗口。
- 2. 在**邮件撰写窗口中，填写主题行并输入你的消息**。

  消息可以包含图片以及指向网站链接。要插入这些项目中的任意一个，请从菜单中选择*插入*：*图片*或*插入*：*链接*。
- 3. **如果你正在创建新消息或转发消息，请输入收件人的电子邮件地址**。

  要从通讯簿中选择收件人，请点击工具栏上的**地址**按钮。你的通讯簿将打开，你可以从中选择收件人。



4. 完成撰写消息后，点击“发送”按钮。

Thunderbird 会询问你想以 HTML 格式、纯文本格式还是两者兼有来发送消息。

5. 选择一种格式，然后点击“发送”以发送邮件。

如果你插入了图片和网络链接，并且你知道收件人可以阅读 HTML 邮件，请务必选择 HTML 格式；否则，请选择纯文本。

如果你希望稍后完成邮件，请点击邮件撰写窗口中的`保存`，然后关闭窗口。Thunderbird 将邮件保存在`草稿`文件夹中。当你准备好再次处理该邮件时，请进入`草稿`文件夹，然后双击已保存的邮件以打开它。

## 介绍 KMail

KMail 是 KDE 的邮件阅读器。当你首次运行 KMail 时，你会看到其主窗口（见图 1-7），但在配置好 KMail 中的邮件账户之前，你无法开始使用它来收发电子邮件。

要配置 KMail，请选择`设置`：`配置 KMail`。在“配置 KMail”窗口中（见图 1-8），点击窗口左侧的`账户`并设置有关你的电子邮件账户的信息。KMail 使用这些信息来收发邮件。

对于传出邮件，请点击“发送”选项卡上的`添加`按钮（见图 1-8），然后选择邮件传输代理。通常，对于由 ISP 提供的邮件账户，你应该选择 `SMTP` 并输入你的 ISP 提供给你的邮件服务器名称（例如，`smtp.comcast.net`）。

![](img/792720823146d68f19fd50c99ebfce4b_351_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_351_1.png)

要设置接收邮件信息，请单击 `接收` 选项卡上的 `添加` 按钮，并选择邮件协议，例如 `POP3` 或 `IMAP`。您的 ISP（互联网服务提供商）会告诉您应使用哪种协议。（通常，它是 `POP3` 或 `IMAP`。）然后输入邮件服务器名称（例如，`mail.concast.net`）以及您的 ISP 账户的用户名和密码。

设置好电子邮件账户信息后，您即可开始使用 KMail。其用户界面直观，且与 Thunderbird 和 Evolution 等其他邮件阅读器相似。KMail 会定期检查并从您的收件账户下载邮件。您可以查看到达收件箱的邮件。

## Linux 中的即时通讯

Linux 中有两种主要的即时通讯（IM）客户端。在 GNOME 桌面上，您可以使用 Gaim，而 Kopete 则是专为 KDE 桌面环境设计，能与之良好配合。我将在以下章节中简要介绍这两种即时通讯客户端。

### 使用 Gaim

您可以使用 Gaim 与众多不同即时通讯服务（如 `AIM`、`ICQ`、`Yahoo!`、`MSN`、`Gadu-Gadu` 和 `Jabber`）上的所有联系人保持联系。如果您使用其中任何即时通讯服务，使用 Gaim 将会感觉非常得心应手。

![](img/792720823146d68f19fd50c99ebfce4b_352_0.png)

在 Fedora Core 中，您可以通过选择 GNOME 桌面上的`应用程序`→`互联网`→`即时通讯客户端`来启动 Gaim。您也可以用类似的方式在其他发行版的 GNOME 桌面环境中启动 Gaim。初始的 Gaim 窗口将与“账户”窗口一起出现，如图 1-9 所示。

![](img/792720823146d68f19fd50c99ebfce4b_352_1.png)

图 1-9：在此窗口中管理您的所有即时通讯账户。

首先，请在“账户”窗口中设置您的即时通讯账户。单击`添加`按钮，并在“添加账户”窗口中填写所需信息，如图 1-10 所示。您必须为您的即时通讯服务选择协议。例如，`AIM` 的协议是 `AIM/ICQ`。其他协议选项包括 `Gadu-Gadu`、`Jabber`、`MSN` 和 `Yahoo!`。

![](img/792720823146d68f19fd50c99ebfce4b_353_0.png)

输入账户信息后，“账户”窗口将显示所有当前定义的账户。然后，您可以从 Gaim 主窗口中选择一个账户并单击`登录`，如图 1-11 所示。

![](img/792720823146d68f19fd50c99ebfce4b_353_1.png)

当 Gaim 登录成功后，它会打开标准的“好友列表”窗口。（见图 1-12。）

![](img/792720823146d68f19fd50c99ebfce4b_354_0.png)

要添加好友，请选择`好友`⇒`添加好友`。在出现的“添加好友”窗口中，输入好友的屏幕名并单击`添加`。要创建新组，请选择`好友`⇒`添加组`。在出现的“添加组”窗口中输入新组的名称，然后单击`添加`。

如果您的任何好友在线，他们的名字将显示在“好友列表”窗口中。要向好友发送消息，请双击其名字，将弹出一个消息窗口。如果有人给您发送消息，将弹出一个包含该消息的消息窗口，您可以在该窗口中开始交谈。

### 使用 Kopete

Kopete——KDE 的即时通讯客户端——允许您连接多种即时通讯服务，包括 `AIM`、`IRC`、`MSN Messenger`、`Yahoo!`、`Gadu-Gadu` 和 `SMS`。

在 Debian、SUSE 和 Xandros 中，您可以通过在应用程序菜单中选择“聊天”或“即时通讯”来启动 Kopete。

当您第一次运行 Kopete 时，会看到“配置 Kopete”窗口（见图 1-13），您可以在此输入关于您的即时通讯及其他即时通讯服务账户的信息。

例如，要添加您的 `AIM` 账户信息，请单击`新建`，然后响应“账户向导”中的提示。第一步是选择您的即时通讯服务。（见图 1-14。）

![](img/792720823146d68f19fd50c99ebfce4b_354_1.png)

![](img/792720823146d68f19fd50c99ebfce4b_355_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_355_1.png)

选择适当的即时通讯服务，例如，如果您使用 AOL 的即时通讯服务，则选择 `AIM`。然后提供 `AIM` 屏幕名和密码。

![](img/792720823146d68f19fd50c99ebfce4b_355_2.png)

![](img/792720823146d68f19fd50c99ebfce4b_355_3.png)

设置好您的即时通讯服务账户后，“账户向导”将关闭，并显示常规 Kopete 窗口。要登录您的即时通讯服务并开始使用 Kopete，请单击 Kopete 窗口中的“连接”按钮——这是工具栏上最左边的按钮。（见图 1-15。）

![](img/792720823146d68f19fd50c99ebfce4b_356_0.png)

单击放大镜图标以查看您的好友。对于在线好友，您会看到一个实心笑脸图标。右键单击一位在线好友，并从菜单中选择“开始聊天”即可开始聊天。选择`文件`→`添加联系人`可添加更多联系人。

好吧，如果您熟悉 `AIM`，您就知道该怎么做：用 Kopete 享受即时通讯的乐趣吧！

# 第 2 章：浏览网络

## 本章内容

- 发现万维网
- 理解 URL
- 了解 Web 服务器和 Web 浏览器
- 盘点 Linux 的 Web 浏览器
- 使用 Mozilla Firefox 浏览网络

我推测您已经知道网络，但您是否知道，网络（或更正式地说，万维网）使互联网成为了今天的样子？互联网已经存在了相当长的一段时间，但直到 1993 年网络出现之前，它尚未普及大众。

在网络出现之前，您必须使用晦涩难懂的 UNIX 命令来下载和使用文件，这对我们中的大多数人来说过于复杂。然而，有了网络，任何人只需使用 Web 浏览器——一种下载并显示网络文档的图形应用程序——即可享受互联网带来的便利。只需单击鼠标，您就可以从阅读公司网站的文档转向下载来自千里之外的视频片段。

在本章中，我简要介绍了网络，并介绍了 Mozilla Firefox——它是大多数 Linux 发行版中主要的 Web 浏览器（而且，事实上，也是电子邮件和新闻阅读器）。我还简要讨论了如何创建您自己的网页。

> KDE 桌面通常使用 Konqueror 作为 Web 浏览器，但在使用过一个 Web 浏览器后，您很容易就能使用其他任何 Web 浏览器。

![](img/792720823146d68f19fd50c99ebfce4b_358_0.png)

## 发现万维网

如果您曾在工作中使用过文件服务器，您就知道共享文件的便利性。您可以使用桌面上的文字处理器访问共享服务器上的任何文档。

现在，想象一下一种文字处理器，它允许您打开并查看位于互联网上任何计算机上的文档。您可以以完整的格式查看文档，包括格式化文本和图形。如果文档引用了另一个文档（可能位于另一台计算机上），您可以通过单击引用来打开该链接文档。这种对分布式文档的便捷访问本质上就是万维网所提供的。

当然，文档必须采用标准格式，以便任何计算机（具有适当的 Web 浏览器软件）都能访问和解释文档。并且，传输网络文档从一个系统到另一个系统需要一种标准协议。

![](img/792720823146d68f19fd50c99ebfce4b_359_0.png)



标准的网络文档格式是`超文本标记语言`（HTML），而用于交换网络文档的标准协议是`超文本传输协议`（HTTP）。HTML 文档是文本文件，不依赖于任何特定的操作系统，因此它们可以在从 Windows 和 Mac 到任何类型的 UNIX 和 Linux 的系统上运行。

![](img/792720823146d68f19fd50c99ebfce4b_359_1.png)

`Web 服务器`是一种软件，它向任何发出相应 HTTP 请求的客户端提供 HTML 文档。`Web 浏览器`是实际从 Web 服务器下载 HTML 文档并以图形方式显示其内容的客户端软件。

### 像巨大的蜘蛛网

万维网是 Web 服务器和服务器提供的 HTML 文档的组合。以这种方式看待网络时，网络就像一本巨大的书，其页面散布在整个互联网中。您使用计算机上运行的 Web 浏览器来查看页面——这些页面像巨大的蜘蛛网一样连接在一起，文档无处不在，如图 2-1 所示。

![](img/792720823146d68f19fd50c99ebfce4b_359_2.png)

![](img/792720823146d68f19fd50c99ebfce4b_359_3.png)

想象一下，网页——HTML 文档——是由类似巨大蜘蛛网的网络连接相互链接起来的，因此你能明白为什么 Web 被称为`Web`（万维网）。`World Wide`（万维）这一部分则源于一个事实，即这些网页遍布世界各地。

## 链接和 URL

与实体书的书页类似，网页包含文本和图形。然而与实体书不同的是，网页可以包含多媒体，如视频片段、声音以及指向其他网页的链接。

网页中的`links`（链接）是对其他网页的引用，你可以顺着它们从一个页面跳转到另一个页面。Web 浏览器通常将这些链接显示为下划线文本（使用不同的颜色）或图像。每个链接都像是给你的一条指令——就像你在实体书中可能看到的“如需更多信息，请参阅第 4 章”一样。在网页中，你只需点击链接；Web 浏览器便会调出被引用的页面，尽管该文档实际上可能位于互联网上某台遥远的计算机中。

网页中的链接被称为`hypertext links`（超文本链接），因为当你点击一个链接时，Web 浏览器会跳转到该链接所引用的网页。

这种安排引出了一个疑问。在一本实体书中，你可能会要求读者跳转到书中的特定章节或页面。超文本链接是如何指示被引用网页位置的？在万维网中，每个网页都有一个特殊名称，称为`Uniform Resource Locator`（统一资源定位符，URL）。URL 唯一地指定了计算机上文件的位置。图 2-2 展示了 URL 的各个组成部分。

![](img/792720823146d68f19fd50c99ebfce4b_360_0.png)

如图 2-2 所示，URL 包含以下部分：

- `Protocol`（协议）：这是 Web 浏览器用于访问 URL 所指定文件中数据的协议名称。在图 2-2 中，协议是`http://`，这意味着 URL 指定的是一个网页的位置。以下是一些常见的协议类型及其含义：
  - `file://`表示 URL 指向一个本地文件。你可以使用这种 URL 在无需连接互联网的情况下查看 HTML 文件。例如，`file:///var/www/html/index.html`会打开你 Linux 系统中的`/var/www/html/index.html`文件。
  - `ftp://`表示你可以使用文件传输协议（FTP）下载文件。例如，`ftp://ftp.purdue.edu/pub/uns/NASA/nasa.jpg`指向 FTP 服务器`ftp.purdue.edu`的`/pub/uns/NASA/NASA`目录中的图像文件`nasa.jpg`。如果你想通过 FTP 访问特定的用户账户，请使用以下形式的 URL：
    `ftp://username:password@ftp.somelsite.com/`
    其中用户名和密码嵌入在 URL 中。（请注意，密码是明文形式，并不安全。）
  - `http://`表示你使用超文本传输协议（HTTP）下载文件。该协议是所有网站 URL 的知名格式，例如 Fedora 项目主页的`http://fedora.redhat.com`。如果 URL 中没有文件名，Web 服务器会发送一个名为`index.html`的默认 HTML 文件。（这是流行的基于 UNIX 的 Apache Web 服务器的默认文件名；Microsoft Windows Web 服务器使用不同的默认文件名。）
  - `https://`指定通过`Secure Sockets Layer`（`SSL`，安全套接字层）连接访问文件——这是一种由 Netscape Communications 设计用于互联网上加密数据传输的协议。通常，这种形式的 URL 用于 Web 浏览器向 Web 服务器发送敏感信息（如信用卡号、用户名和密码）时。例如，像`https://some.site.com/secure/takeorder.html`这样的 URL 可能会显示一个请求信用卡信息及其他个人信息（如姓名、地址和电话号码）的 HTML 表单。
  - `mailto:`指定一个你可以用来发送电子邮件的地址。此 URL 会打开你的电子邮件程序，你可以从中发送消息。例如，`mailto:webmaster@someplace.com`指的是主机`someplace.com`上的 Webmaster（网站管理员）。
  - `news://`指定一个你可以使用网络新闻传输协议（NNTP）阅读的新闻组。例如，
    `news://news.md.comcast.giganews.com/comp.os.linux.setup`
    访问新闻服务器`news.md.comcast.giganews.com`上的`comp.os.linux.setup`新闻组。如果你的 Web 浏览器配置了默认的新闻服务器，你可以省略新闻服务器的名称，并使用 URL`news:comp.os.linux.setup`来访问该新闻组。
- `Domain name`（域名）：包含拥有该 URL 所指定文件的计算机的完全限定域名。你也可以在此字段中提供 IP 地址。域名不区分大小写。
- `Port`（端口）：由 URL 第一部分中列出的协议使用的端口号。URL 的这一部分是可选的；所有协议都有默认端口。例如，HTTP 的默认端口是 80。如果网站配置 Web 服务器监听不同的端口，则 URL 必须包含端口号。
- `Directory path`（目录路径）：URL 中引用文件的目录路径。对于网页，此字段是 HTML 文件的目录路径。目录路径区分大小写。
- `Filename`（文件名）：文件的名称。对于网页，文件名通常以`.htm`或`.html`结尾。如果你省略文件名，Web 服务器将返回一个默认文件（通常名为`index.html`）。文件名区分大小写。
- `HTML anchor`（HTML 锚点）：URL 的可选部分，使 Web 浏览器跳转到文件中的特定位置。如果这部分以问号（`?`）而不是井号（`#`）开头，浏览器会将问号后的文本视为查询。Web 服务器会根据此类查询返回信息。

### Web 服务器和 Web 浏览器

Web 服务器提供网页，而 Web 浏览器下载它们并将其显示给用户。这就是这两个协作的软件包使 Web 得以工作的基本故事。

在典型场景中，用户坐在连接到互联网的计算机前并运行 Web 浏览器。当用户点击链接或在 Web 浏览器中输入 URL 时，浏览器连接到 Web 服务器并向服务器请求文档。Web 服务器发送该文档（通常以 HTML 格式）并结束连接。Web 浏览器解析并显示带有文本、图形和多媒体的 HTML 文档（如果适用）。图 2-3 说明了用户浏览 Web 的这一典型场景。

![](img/792720823146d68f19fd50c99ebfce4b_363_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_363_1.png)

![](img/792720823146d68f19fd50c99ebfce4b_363_2.png)

![](img/792720823146d68f19fd50c99ebfce4b_363_3.png)

![](img/792720823146d68f19fd50c99ebfce4b_363_4.png)

**图 2-3：**

Web 浏览器请求文档，Web 服务器发送它们。

Web 浏览器连接到服务器并请求网页

当服务器发送完文档后，Web 浏览器与 Web 服务器之间的连接即告结束。当用户浏览已下载的文档并点击另一个超文本链接时，Web 浏览器再次连接到超文本链接中指定的 Web 服务器，下载文档，结束连接，并显示新文档。这就是用户如何轻松地在不同文档之间移动的方式。

> **REMEMBER（记住）**



> Web 浏览器所做的不仅仅只是与 Web 服务器进行“HTTP 对话”——事实上，Web 浏览器还可以使用 FTP 下载文档，并且许多浏览器还集成了邮件和新闻阅读器。

## Linux 中的 Web 浏览

Web 浏览很有趣，因为当今许多网页都充满了图形和多媒体。此外还有惊喜元素——你可以点击一个链接，最终到达意想不到的网页。链接是 Web 中最耐人寻味（且有用）的方面。你可以从一个显示今日天气的页面开始，再点几下鼠标，就可以阅读本周的 *Time*（时代）杂志。

要浏览网络，你只需要一个网络浏览器和互联网连接。我假设你已经处理好了互联网连接（如果你尚未设置好互联网连接，请参阅第三部分第一章），因此你只需要了解 Linux 中的网络浏览器即可。

## 查看 Linux 的网络浏览器

许多 Linux 发行版都附带 Mozilla 网络浏览器。Mozilla 是久负盛名的 Netscape Communicator 的开源版本。

Linux 还有其他几种可用的网络浏览器。我将简要提及这些其他浏览器，但在接下来的讨论中，我将重点介绍 Firefox。以下是 Linux 的主要网络浏览器：

- **Mozilla：** 那是老黄牛——Netscape Communicator——的转世，但性能更佳。它包含电子邮件和新闻阅读器。该网络浏览器被称为 Mozilla Navigator，或简称 Navigator（正如在 Netscape Communicator 中一样）。

- **Epiphany：** GNOME 网络浏览器，它使用 Mozilla 代码的部分来绘制网页，但用户界面比 Mozilla 更简洁。如果未安装 Epiphany，你可以从 www.gnome.org/projects/epiphany 下载。

- **Firefox：** Mozilla 的下一代浏览器，它能拦截弹出式广告，提供选项卡以便在单个窗口中轻松查看多个网页，并包含一组隐私工具。你可以从 www.mozilla.org/download.html 下载 Firefox。

- **Konqueror：** KDE 网络浏览器，它也兼任文件管理器和通用查看器。

除此之外，还有许多其他应用程序能够下载和显示网页。

![](img/792720823146d68f19fd50c99ebfce4b_364_0.png)

如今，大多数发行版都包含 Mozilla Firefox 网络浏览器。我将在下一节中简要介绍 Firefox 网络浏览器。其他所有网络浏览器都有类似直观的用户界面。

![](img/792720823146d68f19fd50c99ebfce4b_364_1.png)

Debian 默认不安装 Firefox，但你可以通过键入 `su -` 成为 root 用户，然后键入 `apt-get install mozilla-firefox` 轻松安装它。安装完成后，你可以选择“应用程序 → Debian 菜单 → 网络 → Mozilla Firefox”从 Debian 的 GNOME 桌面启动 Firefox。

## 介绍 Firefox 的用户界面

通常，你可以通过点击面板上的图标或从图形用户界面（GUI）桌面的菜单中选择来启动 Firefox。

当 Firefox 启动时，它会显示带有默认主页的浏览器窗口。（网络服务器上的主要网页被称为主页。）你可以配置 Firefox 使用不同的网页作为默认主页。

图 2-4 显示了一个来自美国政府网站（www.irs.gov）的网页，以及 Firefox 浏览器窗口的主要元素。请注意，Firefox 支持选项卡式浏览，这意味着你可以打开一个新选项卡（通过按 `Ctrl+T`）并在该选项卡中查看网页。这样，你可以在单个窗口中查看多个网页。

Firefox 网络浏览器的用户界面包含许多功能，但你很容易就能掌握。你可以从基础开始使用 Firefox，然后逐渐扩展到尚未探索的领域。

### Firefox 工具栏

从窗口顶部开始，你会看到带有标准菜单（文件、编辑等）的菜单栏，随后是两个工具栏——导航工具栏和书签工具栏。书签工具栏下方的区域是显示当前网页的地方。

以下是导航工具栏（位于菜单栏正下方）上的按钮和文本框的功能，从左到右依次为：

- **后退：** 移动到前一个网页。

- **前进：** 移动到你可能曾经后退过的页面。

- **重新加载：** 重新加载当前网页。

- **停止：** 停止加载当前页面。

- **主页：** 转到主页。

- **位置：** 显示当前网页的 URL。（在此框中输入 URL 并按 Enter 键即可查看该网页。）

- **转到：** 转到在“位置”文本框中输入的 URL。

- **Google 搜索：** 点击可搜索 Google、Yahoo!、Amazon.com、Dictionary.com 和 eBay 等各种网站；输入文本并按 Enter 键可搜索当前选定的网站（默认为 Google）。

## 图 2-4：Firefox 网络浏览器的实际运行效果。

![](img/792720823146d68f19fd50c99ebfce4b_366_0.png)

紧跟在导航工具栏下方的是书签工具栏，其中包含可将你带到特定网页的按钮。

### 状态栏

你可以将 Firefox 窗口底部边缘的栏视为状态栏，因为该区域的中部在 Firefox 加载网页时会显示状态信息。

在 Firefox 状态栏的右侧角落，当你访问安全网站时，会出现一个安全挂锁图标。Firefox 支持使用 SSL 在浏览器和 Web 服务器之间传输加密数据的安全版本 HTTP。当 Firefox 连接到支持安全 HTTP 的 Web 服务器时，状态栏的右边缘会出现一个锁定的安全挂锁图标。否则，没有安全挂锁图标，表示连接不安全。用于安全 HTTP 传输的 URL 以 `https://` 开头，而不是常见的 `http://`（注意 https 中多出的 s）。

Firefox 在状态栏的左侧部分显示状态消息。你可以观察该区域的消息以了解正在发生的事情。如果你将鼠标悬停在网页上的链接上，状态栏将显示该链接的 URL。

## Firefox 菜单

我很少提及 Firefox 的菜单。这是因为你通常不需要使用它们也能应付过去。尽管如此，快速浏览一下 Firefox 的菜单是值得的，这样你就知道每个菜单提供了什么功能。表 2-1 提供了 Firefox 菜单的概述。

**表 2-1 Firefox 菜单**

| 此菜单 | 允许你执行以下操作 |

| :--- | :--- |

| 文件 | 打开文件或网络位置，打开或关闭选项卡，通过电子邮件发送网页或链接，编辑网页，打印当前页面以及退出 Firefox |

| 编辑 | 复制和粘贴选择内容，在当前页面中查找文本，以及编辑你的偏好设置 |

| 视图 | 显示或隐藏各种工具栏，重新加载当前页面，放大或缩小文本，以及查看页面的 HTML 代码 |

| 转到 | 在你访问过的页面列表中向后和向前移动，或跳转到其他最近访问的网页 |

| 书签 | 为页面添加书签，管理书签，并将链接添加到书签工具栏文件夹中。（这些随后会出现在书签工具栏中。） |

| 工具 | 搜索网络并管理网页的各个方面，例如主题，并查看关于当前页面的信息 |

| 帮助 | 获取有关 Firefox 的在线帮助 |

## 更改你的主页

你的主页是启动 Firefox 时加载的页面。默认主页取决于发行版。通常，主页是来自系统硬盘的文件。更改主页很容易。

首先，找到你希望作为主页的网页。你可以以任何方式到达该页面。你可以使用搜索引擎搜索以找到想要的页面，可以在“位置”文本框中输入 URL，甚至可能意外地到达你希望设为主页的页面。这都无关紧要。

当你在 Firefox 中查看希望设为主页的网页时，从 Firefox 菜单中选择 **编辑 → 偏好设置**。将出现偏好设置对话框，如图 2-5 所示。

在图 2-5 的右侧，注意偏好设置中的“主页”部分。然后你会看到一个用于主页的“位置”文本框，在地址下方是一个 **使用当前页面** 按钮。点击该按钮即可将当前页面设为主页。

![](img/792720823146d68f19fd50c99ebfce4b_368_0.png)

**图 2-5：** 点击“使用当前页面”按钮可将当前网页设为主页。

你可以使用偏好设置对话框设置许多其他选项。虽然我没有在这里解释所有选项，但你可以通过点击周围来探索此窗口所能执行的所有操作。例如，你可以点击“使用书签”按钮选择保存的 URL 书签作为主页。（你需要从对话框中选择书签。）

## 使用 Firefox 浏览互联网

你从主页去哪里取决于你自己。你只需点击并看看自己最终到达哪里。移动你的鼠标。当你处于链接上时，因为鼠标指针会变成伸出的食指的手形，所以你便知道了。点击链接，Firefox 会下载该链接引用的网页。

如何使用网络取决于你想做什么。刚开始时，你可能想进行大量探索——浏览网站并跟随链接，而没有任何具体目标（你可以称之为“网络闲逛”）。



网络的另一种、更有目的性的使用方式是找出网上的特定信息。例如，你可能想找到所有包含带有指定关键词文档的网站。对于此类搜索，你可以使用网上可用的众多网络搜索工具之一。Firefox 的搜索文本框会将你带到 Google 网络搜索页面（`www.google.com`）。

第三种用法是访问具有已知 URL 的特定网站。例如，当阅读本书中关于某个特定主题的内容时，你可能会遇到一个特定的 URL。在这种情况下，你希望直接跳转到该网页。

![](img/792720823146d68f19fd50c99ebfce4b_369_0.png)

如果你想使用 Firefox 上网冲浪，你只需要一个起始网页——然后你可以点击任何吸引你的东西。例如，选中 Firefox 导航工具栏中位置文本框中的文本，输入 `www.yahoo.com`，然后按 Enter 键。你将到达显示雅虎网络目录的雅虎主页——该目录按主题分类。这就是你的起点。你只需点击即可出发！

# 第 3 章：阅读新闻组和 RSS 源

## 本章内容

- 理解新闻组
- 从你的 ISP 阅读新闻组
- 在一些网站上阅读和搜索新闻组
- 阅读 RSS 源

互联网新闻组就像前网络时代的公告板系统（BBS）或 AOL 和 MSN 等在线系统提供的论坛。本质上，新闻组提供了一个分布式的全球会议系统。你可以发布文章——本质上是发送给一整群人的电子邮件——并回应他人发布的文章。

可以将互联网新闻组想象成一个聚集地——一个虚拟的会议场所，你可以在那里提问并讨论各种议题。（而且最棒的是，你们讨论的所有内容都会被存档以供后世参考。）

要参与新闻组，你需要访问新闻服务器——你的互联网服务提供商（ISP）可以提供这种访问权限。你还需要一个新闻阅读器。幸运的是，Linux 附带了一些你可以用来阅读新闻组的软件。在本章中，我将向你介绍新闻组，并展示如何使用几款新闻阅读器阅读新闻组。我还会简要解释如何在几个网站上免费阅读和搜索新闻组。

如今，阅读网站和网络博客摘要的另一种流行方式是使用可以接收 RSS 源的节目。在本章末尾，我将简要描述什么是 RSS 源，以及如何使用诸如 KDE Akregator 这样的程序订阅 RSS 源并在你的 Linux 系统上阅读它们。

## 理解新闻组

新闻组起源于 *Usenet*——一个曾经被广泛用于交换电子邮件和新闻项目的存储转发消息网络。Usenet 的工作方式类似于电报，新闻和邮件从一个系统中继到另一个系统。在 Usenet 中，这些系统并不在任何网络上；这些系统只是互相拨号，并使用 UNIX-to-UNIX 复制协议（`UUCP`）传输文本消息。

虽然它是一个连接非常松散的计算机集合，但 Usenet 运行良好并继续使用，因为连接它的费用非常低。你只需要一个调制解调器和一个愿意存储和转发你的邮件和新闻的网站。你必须在你的系统上设置 `UUCP`，但你不需要持续的网络连接；只需几通电话就能保持电子邮件和新闻的流通。Usenet 的缺点是你不能使用 TCP/IP 服务，如 Web、TELNET 或 FTP，通过 `UUCP`。

从其 Usenet 起源开始，新闻组现在已经迁移到互联网（尽管这些新闻组仍然被称为 *Usenet 新闻组*）。现在，网络新闻传输协议（`NNTP`）替代了 `UUCP` 来传输新闻。

虽然（对于大多数在线世界而言）新闻传输协议已从 `UUCP` 变为 `NNTP`，但新闻传输的存储转发概念保持不变。因此，如果你想在你的 Linux 系统上获取新闻，你必须找到一个可以让你的系统下载新闻的新闻服务器。通常，你可以使用你的 ISP 的新闻服务器。

### 新闻组层级

互联网新闻组按层级组织，以便于维护和使用。新闻组名称通过显示层级来帮助理清事物。

诚然，这些新闻组名称是用互联网术语写成的，一开始可能显得相当晦涩。但在稍作解释后，这种语言很容易上手。例如，一个典型的新闻组名称看起来像这样：

```
comp.os.linux.announce
```

这个名称表示 `comp.os.linux.announce` 是一个关于 Linux 操作系统（`os.linux`）的通告（`announce`）新闻组，并且这些主题属于计算机（`comp`）这个大类别。

你可以看到，新闻组名称的格式是由点分隔的一系列单词。这些单词表示新闻组的层级。图 3-1 说明了新闻组的层级组织概念。

要理解新闻组层级，请将新闻组名称与 Linux 中文件的路径名（例如 `/usr/lib/X11/xinit/Xclients`）进行比较。正如文件的路径名显示文件的目录层级一样，新闻组名称显示新闻组的层级。在文件名中，斜杠（`/`）分隔目录的名称；在新闻组名称中，点（`.`）分隔新闻组层级中的不同级别。

![](img/792720823146d68f19fd50c99ebfce4b_372_0.png)

在新闻组名称中，第一个单词代表新闻组*类别*。例如，`comp.os.linux.announce` 新闻组属于 `comp` 类别，而 `alt.books.technical` 属于 `alt` 类别。

### 顶级新闻组类别

表 3-1 列出了一些主要的新闻组类别。你会发现各种各样的新闻组，涵盖的主题从政治到计算机不等。与 Linux 相关的新闻组位于 `comp.os.linux` 层级中。

| **表 3-1 一些主要新闻组类别** |

| :--- | :--- |

| **类别** | **主题** |

| alt | *替代* 新闻组（不受任何规则约束），涵盖从平凡到怪异的各种主题 |

| bionet | 生物学新闻组 |

| bit | Bitnet 新闻组 |

| biz | 商业新闻组 |

| clari | Clarinet 新闻服务（每日新闻） |

| comp | 计算机硬件和软件新闻组（包括 Linux 和 Microsoft Windows 等操作系统） |

| ieee | 电气电子工程师学会（IEEE）的新闻组 |

| k12 | 致力于小学和中学教育的新闻组 |

| linux | 致力于 Linux 的新闻组（包括 `linux.redhat` 层级） |

| misc | 杂项新闻组 |

| news | 关于互联网新闻管理的新闻组 |

| rec | 娱乐和艺术新闻组 |

| sci | 科学和工程新闻组 |

| soc | 讨论社会问题和各种文化的新闻组 |

| talk | 当前问题的讨论（想想“广播脱口秀”） |

这个简短的类别列表具有误导性，因为它并没有真正告诉你每个类别中可用的新闻组种类繁多。仅顶级类别就有近一千个，许多顶级类别只分布在世界的特定地区。由于每个新闻组类别包含多个级别的子类别，新闻组的总数可能接近 60,000 或 70,000！仅 `comp` 类别就有近 1,200 个新闻组。

不幸的是，许多新闻组被垃圾邮件淹没，这就像你的电子邮件收件箱一样糟糕，但更糟的是，任何人都可以在新闻组上发布任何东西。有一些称为*已调节新闻组*的新闻组提供了一些缓解。任何想在已调节新闻组上发布的人都必须首先将文章提交给调节员——一个人类——然后调节员可以决定是发布还是拒绝该文章。你可以通过尽可能浏览已调节新闻组来减少垃圾信息的过载。

要浏览新闻组类别并了解新闻组涵盖的主题范围，请访问 Google Groups 网站 http://groups.google.com 并点击“浏览所有 Usenet”链接。

![](img/792720823146d68f19fd50c99ebfce4b_373_0.png)

### 与 Linux 相关的新闻组

通常，你需要根据自己的兴趣缩小新闻组的选择。例如，如果你对 Linux 感兴趣，你可以选择以下一个或多个新闻组：

- `comp.os.linux.admin`：有关 Linux 系统管理的信息。
- `comp.os.linux.advocacy`：关于推广 Linux 的讨论。
- `comp.os.linux.announce`：关于 Linux 的重要通告。这个新闻组是已调节的，这意味着你必须将文章发送给调节员，如果该文章是合理的，调节员会将其发布到新闻组中。

适合新闻组。*（此方法可阻止闲杂人员用营销推介信息堵塞新闻组。）*

- `comp.os.linux.answers`：关于 Linux 的问答。所有 Linux 操作指南（HOWTO）都发布在这个经审核的新闻组中。
- `comp.os.linux.development`：当前的 Linux 开发工作。
- `comp.os.linux.development.apps`：Linux 应用程序开发。
- `comp.os.linux.development.system`：Linux 操作系统开发。
- `comp.os.linux.hardware`：关于 Linux 和各类硬件的讨论。
- `comp.os.linux.help`：Linux 各方面的帮助。
- `comp.os.linux.misc`：其他与 Linux 相关的话题。
- `comp.os.linux.networking`：Linux 下的网络。



- `comp.os.linux.redhat`：Red Hat Linux 相关话题。
- `comp.os.linux.setup`：Linux 设置和安装。
- `comp.os.linux.x`：关于在 Linux 下设置和运行 X 窗系统的讨论。
- `linux.debian`：关于 Debian GNU/Linux 的经审核新闻组。
- `linux.debian.news`：关于 Debian GNU/Linux 新闻条目的经审核新闻组。
- `linux.redhat`：关于 Red Hat Linux 的讨论。

![](img/792720823146d68f19fd50c99ebfce4b_374_0.png)

由于即使是在像 Linux 这样的特定领域，想要跟上所有新闻也是不可能的，因此你必须有选择地决定阅读哪些新闻组。当你刚安装并配置好 Linux 时，你可能会阅读诸如 `comp.os.linux.help`、`comp.os.linux.setup`、`comp.os.linux.hardware` 和 `comp.os.linux.x`（特别是如果你在使用 X 时遇到问题）这样的新闻组。当 Linux 已经运行起来之后，你可能只想了解 Linux 中正在发生的新事物。为了获取此类信息，请阅读 `comp.os.linux.announce` 新闻组。

## 从你的 ISP 阅读新闻组

如果你注册了 ISP 以接入互联网，该 ISP 可以为你提供访问新闻服务器的权限。此类互联网新闻服务器通过 `网络新闻传输协议`（`NNTP`）进行通信。你可以使用支持 `NNTP` 的新闻阅读器（如 `KNode`）来访问新闻服务器并阅读选定的新闻组。你也可以使用 `Thunderbird` 阅读新闻。使用新闻阅读器是访问 ISP 新闻服务器新闻的最简单方式。

![](img/792720823146d68f19fd50c99ebfce4b_375_0.png)

我关于阅读新闻组的讨论假设你已通过 ISP 获得了新闻服务器的访问权限。ISP 会向你提供新闻服务器的名称以及在你的新闻阅读器上设置新闻账户所需的任何用户名和密码。

要阅读新闻，你需要一个 `新闻阅读器`——即一个能让你选择新闻组并查看该新闻组中条目的程序。你还需要了解新闻组层次结构和命名惯例（我在本章前面的“新闻组层次结构”一节中对此有描述）。现在我将向你展示如何从新闻服务器阅读新闻。

![](img/792720823146d68f19fd50c99ebfce4b_375_1.png)

如果你无法通过你的 ISP 访问新闻组，可以尝试使用现有的众多公共新闻服务器之一。要查看公共新闻服务器列表，请访问位于 `www.newzbot.com` 的 `NewzBot`。在该网站上，你可以搜索携带特定新闻组的新闻服务器。

### 盘点新闻阅读器

在 Linux 中，你可以使用多种软件包来下载和阅读新闻组。以下是一些主要的新闻阅读器：

- `Thunderbird`：`Thunderbird` 具备从 `NNTP` 服务器下载新闻的功能。你可以阅读新闻组并向新闻组发布条目。Xandros 使用 `Thunderbird` 处理邮件和新闻。
- `KNode`：这是一个用于 KDE 的新闻阅读器，你可以从 `knode.sourceforge.net` 下载。Debian、MEPIS 和 SUSE 提供 `KNode` 作为新闻阅读器。
- `Pan`：`Pan` 是一款图形用户界面（GUI）新闻阅读器，根据开发者网站（`http://pan.rebelbase.com`）的说法，“……它试图让新手和经验丰富的用户都感到满意。”你可以从 `http://pan.rebelbase.com/download` 下载适用于各种 Linux 发行版的 `Pan`。

![](img/792720823146d68f19fd50c99ebfce4b_375_2.png)

如果你的 Linux 系统中没有找到新闻阅读器，你可以轻松地在任何 Linux 发行版中下载并安装这些新闻阅读器中的任何一个。通常，你只需在搜索引擎上搜索 `download` 一词加上新闻阅读器的名称，即可找到下载站点。

### 使用 Thunderbird 阅读新闻组

你可以使用 Mozilla 项目的邮件和新闻阅读器 `Thunderbird` 浏览新闻组并发布文章。

![](img/792720823146d68f19fd50c99ebfce4b_375_3.png)

在 Xandros 等某些发行版中，主菜单中有直接启动 `Thunderbird` 的选项。在许多 Linux 发行版中，可能未安装 `Thunderbird` 的邮件和新闻组件。在这种情况下，你需要下载并安装 `Thunderbird` 的邮件和新闻组件，或使用其他新闻阅读器。

当你第一次开始使用 `Thunderbird` 阅读新闻组时，请遵循以下步骤设置新闻账户：

1. 从 `Thunderbird` 菜单中选择 `编辑`→`账户设置`。
   此时会出现一个对话框。
2. 单击 `添加账户`。
   此时会出现账户向导，如图 3-2 所示。

![](img/792720823146d68f19fd50c99ebfce4b_376_0.png)

`图 3-2`：`Thunderbird` 的账户向导引导你完成新闻组账户设置。

3. 选择 `新闻组账户` 单选按钮（参见图 3-2）并单击 `下一步`。
4. 在出现的下一个屏幕上，填写你的身份信息——姓名和电子邮件地址——然后单击 `下一步` 进入下一个屏幕。
5. 输入你的新闻服务器名称，然后单击 `下一步`。
6. 输入新闻组账户的描述性名称，然后单击 `下一步`。
7. 单击 `完成` 以完成新闻组账户设置。

新的新闻组账户现在出现在 `Thunderbird` 窗口左侧的账户列表中。单击新闻组账户名称，窗口右侧将显示该新闻组账户的选项。

单击 `订阅新闻组` 链接。`Thunderbird` 开始从新闻服务器下载新闻组列表。

如果你的 ISP 的新闻服务器需要用户名和密码，系统会提示你输入这些信息。之后，`Thunderbird` 将下载新闻组列表并在订阅对话框中显示它们。（你可以在文本框中输入搜索字符串以缩小列表范围。）找到你想要的新闻组后，勾选复选框以订阅这些新闻组，如图 3-3 所示。然后单击“确定”关闭对话框。

![](img/792720823146d68f19fd50c99ebfce4b_377_0.png)

订阅新闻组后，这些新闻组将出现在 `Thunderbird` 窗口左侧的新闻组账户名称下方。然后你可以使用以下步骤阅读新闻组：

1. 单击一个新闻组名称（例如，`comp.os.linux.announce`）。
   如果你的新闻服务器需要用户名和密码，将出现一个对话框提示你输入这些信息。然后另一个对话框会询问你想要下载多少消息头。
2. 指定你想要下载的消息头数量（例如 500），然后单击“下载”继续。
   `Thunderbird` 从新闻组下载消息头，并在窗口右上区域显示列表。
3. 从消息头列表中，单击一个条目以阅读该文章，如图 3-4 所示。

要选择其他已订阅的新闻组，只需单击窗口左侧的新闻组名称即可。

![](img/792720823146d68f19fd50c99ebfce4b_378_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_378_1.png)

### 新闻组订阅

与杂志或报纸不同，阅读新闻组并不需要你订阅；你可以阅读新闻服务器上可用的任何新闻组。然而，新闻服务器管理员可能会决定排除某些新闻组；如果它们未包含在内，你就无法阅读它们。

唯一可以被称为 `订阅` 的操作，是指出你常规想要阅读的新闻组。新闻服务器不会接收这些订阅信息——这些信息仅由新闻阅读器使用，以确定从新闻服务器下载什么内容。

### 发布新闻

你可以使用任何新闻阅读器将新闻文章（新条目或对旧帖子的回复）发布到一个或多个新闻组。发布新闻条目的确切命令取决于所使用的新闻阅读器。例如，在 `Thunderbird` 新闻阅读器中，发布文章需遵循以下步骤：

1. 单击工具栏上的“回复”按钮，以发布对你正在阅读的新闻条目的后续回复。要发布新的新闻文章，请单击“撰写”按钮。
   会出现一个窗口，你可以在其中撰写消息。
2. 输入新闻组名称，就像发送电子邮件时输入收件人地址一样。输入主题和你的消息内容。
   对于此测试帖子，请在主题行中键入 `ignore`（忽略），并将新闻组名称输入为 `misc.test`。
   否则，任何接收到你文章的站点都会通过电子邮件回复你，告知该文章已到达该站点；这符合 `misc.test` 新闻组的用途。
3. 完成消息编写后，点击工具栏上的“发送”按钮。
   `Thunderbird` 将消息发送到新闻服务器，该服务器随后将其转发至其他新闻服务器，很快消息就会传遍全世界！



### 4. 要验证测试消息是否到达新闻组，请选择“文件”→“订阅”。然后订阅`misc.test`新闻组（这就是你最近发布新文章的地方）。查看`misc.test`中最新的文章（或其中最近的一篇文章）；它应该是你最近发布的那篇文章。

如果你发布了一篇文章并立即读取新闻组，你会看到新文章，但这并不意味着该文章已到达互联网上的其他站点。毕竟，你的帖子立即显示在你的新闻服务器上，因为你是从那里发布文章的。由于新闻分发的存储转发模型，新闻文章会从你的新闻服务器逐渐传播到世界各地的其他服务器。

![](img/792720823146d68f19fd50c99ebfce4b_379_0.png)

`misc.test`新闻组提供了一种检查新闻帖子是否真正传播开来的方法。如果你向该新闻组发布帖子，且未在主题中包含`ignore`一词，新闻服务器会通过向文章标头中“回复至”字段列出的地址发送电子邮件来确认收到该文章。

## 使用 KNode

Debian、MEPIS 和 SUSE 将 KNode 作为默认的新闻客户端提供。通常，你可以通过从菜单中选择新闻客户端来启动 KNode（在 Internet 应用程序中查找）。如果你在菜单中没有看到新闻客户端选项，请在终端窗口中输入`knode`来启动 KNode。

KNode 首次运行时，会弹出“配置 KNode”对话框，如图 3-5 所示，你可以在此配置阅读新闻组和向新闻组发布条目所需的所有设置。

对话框左侧显示了所有可配置的项目，右侧则是为你当前在左侧选中的项目输入信息的地方。

## 从 ISP 阅读新闻组

![](img/792720823146d68f19fd50c99ebfce4b_380_0.png)

图 3-5：从此对话框中配置 KNode。

当“配置 KNode”对话框首次打开时，它会提示你输入个人信息。输入你的识别信息，如姓名、电子邮件地址和组织——这些信息在你向新闻组发布新条目时会被使用。

然后，点击左侧的`Accounts`（账户）（参考图 3-5），并点击右侧的新闻组服务器选项卡以设置有关你将要从中阅读新闻的新闻服务器的信息。点击新闻组服务器选项卡中的`New`（新建）以弹出一个对话框（参见图 3-6），你可以在其中输入有关新闻服务器的信息。你的 ISP 应已提供访问新闻服务器所需的信息。如果新闻服务器需要登录名和密码，你也必须输入这些信息。

设置好新闻账户后，KNode 窗口会在其左侧显示新闻服务器的名称，如图 3-7 所示。右键点击服务器名称，并从弹出菜单中选择`Subscribe`（订阅）到新闻组。此时会出现一个对话框，你可以从中订阅选定的新闻组（如`comp.linux.announce`）。

图 3-7 展示了在从已订阅的新闻组中阅读文章时 KNode 窗口的典型视图。KNode 的用户界面与许多其他邮件和新闻客户端（包括 Thunderbird）类似。

![](img/792720823146d68f19fd50c99ebfce4b_381_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_381_1.png)

## 在网站上阅读和搜索新闻组

如果你无法通过 ISP 访问新闻组，你仍然可以在许多网站上阅读新闻组并向新闻组发布文章。其中一些网站归档了旧新闻文章，并提供了良好的搜索功能，因此你可以搜索这些网站中与你可能有的问题相关的文章。

通过网站阅读新闻组最好的地方在于，你甚至不需要访问新闻服务器，就可以通过 Web 浏览器阅读新闻。

表 3-2 列出了提供 Usenet 新闻组免费访问的网站。一些网站提供收费的 Usenet 新闻组服务。我在此未列出它们，但你可以使用 Google（www.google.com）搜索它们——输入搜索词`usenet newsgroup access`（usenet 新闻组访问）以获取提供新闻组访问权限（包括收费的）的所有网站列表。

表 3-2 提供 Usenet 新闻组免费访问的网站

| 网站 | URL |
| :--- | :--- |
| Google Groups | http://groups.google.com |
| mail2web | http://usenet.mail2web.com |
| InterBulletin | http://news.interbulletin.com |
| Usenet Replayer | www.usenet-replayer.com |
| Mailgate | www.mailgate.org |

阅读新闻组、发布文章和搜索旧新闻组归档的最佳地点之一是 Google Groups——Google 的 Usenet 讨论论坛——位于 Web 上的`http://groups.google.com`。在该网站上，你可以选择一个新闻组进行浏览，并且可以回复发布在各个新闻组上的文章。

Google Groups 最好的部分是其搜索功能。你已经知道 Google 的 Web 搜索有多好；你同样可以使用这种全面的搜索功能来查找与你的搜索词相关的新闻组帖子。要搜索新闻组，请在`http://groups.google.com`填写搜索表单并按 Enter。

要在 Google Groups 中浏览新闻组，请忽略搜索框，查看高级新闻组类别列表，如`alt`、`comp`和`soc`。点击类别，你可以逐步深入到特定的新闻组。在 Google Groups 中查看文章时，你可以点击一个链接，该链接允许你发布对该文章的后续回复。

![](img/792720823146d68f19fd50c99ebfce4b_382_0.png)

RSS 代表 Really Simple Syndication（真正简化的信息聚合）。RSS 是一种`syndication`（信息聚合）格式——收集并提供 Web 站点内容，主要是面向新闻的站点和博客。术语`blog`（博客）是`weblog`（网志）的缩写——一种经常更新的日志，包含博客创建者的思想、评论和观点。RSS 可用于提供任何可以分解为离散项目并放入 RSS 格式的信息。这种 RSS 格式的内容被称为`RSS feed`（RSS 源），支持 RSS 的程序可以定期检查该源是否有更改，下载新项目，并将其提供给用户。

RSS 格式是 XML（可扩展标记语言）的一种方言。所有 RSS 文件都符合 XML 1.0 规范。

有许多版本的 RSS，但三个版本——0.91、1.0 和 2.0——被广泛使用。Netscape 设计了 RSS 0.90 版本，用于收集和显示新闻网站的标题。一个更简单的版本 0.91 被提出，UserLand Software 采用了该版本用于其博客产品。同时，另一个非商业团体将 RSS 0.90 演变为 RSS 1.0，该版本基于资源描述格式或 RDF（参见`www.w3.org/rdf`）。UserLand 没有接受 RSS 1.0，而是继续`演变` RSS 0.91，通过版本 0.92、0.93、0.94，最终定为 RSS 2.0（跳过 1.0，因为该版本号已被占用）。目前，许多博客和网站使用 RSS 0.91 进行基本信息聚合（标题、URL 和描述）；对使用 RDF 的阅读器使用 RSS 1.0；对带有更多元数据的高级信息聚合使用 RSS 2.0。（将元数据理解为`关于数据的数据`，这正是 RSS 格式提供的：它提供关于其他信息（如博客和新闻）的数据。）RSS 1.0 文件具有 .rdf 扩展名，而 RSS 0.91 和 2.0 文件具有 .xml 扩展名。然而，所有 RSS 文件都是使用 XML 标签的文本文件。

![](img/792720823146d68f19fd50c99ebfce4b_383_0.png)

### 检查 RSS 源

RSS 源是一个包含 XML 标签的文本文件，这些标签描述 Web 站点的内容。你通常使用自动化程序定期生成 RSS 源文件，但你也可以使用文本编辑器准备 RSS 源文件。了解 RSS 源的样子是有益的，这样你就可以调试源的问题。

RSS 源的具体细节取决于 RSS 的版本。最简单的源是 RSS 0.91，以下是一个典型的 RSS 0.91 源：

```text
<?xml version="1.0" ?>
<!-- A comment line -->
<rss version="0.91">
```



```
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

从上述代码列表中可以看出，RSS 源（RSS feed）包含一个频道（channel），该频道拥有标题、链接、描述和语言属性，随后是一系列条目（item），每个条目都有标题、链接和描述。

![](img/792720823146d68f19fd50c99ebfce4b_384_0.png)

RSS 1.0 的格式更为冗长，因为它使用 RDF 格式。RSS 1.0 基本上提供了 RSS 0.91 中包含的基本信息，并增加了更多细节，例如条目级别的作者、主题和发布日期，这些是 RSS 0.91 不支持的。

## 阅读 RSS 源

有许多图形用户界面（GUI）程序可用于订阅 RSS 源并阅读源中的条目。这些程序被称为 RSS *聚合器*（aggregators），因为它们可以从许多 RSS 源收集信息，并将所有内容集中在一个地方呈现。

RSS 聚合器有两种类型——浏览器插件和独立程序。像 NewsMonter（*www.newsmonter.org*）这样的浏览器插件运行在 Web 浏览器中，因此源显示在 Web 浏览器内。像 GNOME Straw（*www.nongnu.org/straw*）和 KDE Akregator（*http://akregator.sourceforge.net*）这样的独立程序是完整的 GUI 应用程序，通常外观与其他邮件和新闻阅读器程序相似。

![](img/792720823146d68f19fd50c99ebfce4b_384_1.png)

Fedora、MEPIS 和 SUSE 系统都附带了 Akregator 程序，这是一个独立的 RSS 源*聚合器*。要运行它，请在图形桌面应用程序菜单中寻找其链接；如果找不到，请在终端窗口中输入 `akregator`。在 Debian 中，你可以通过输入 `apt-get install akregator` 来安装 Akregator（先输入 `su -` 成为 *root* 用户）。

当 Akregator 首次运行时，它会显示主窗口，其中没有任何 RSS 源。要订阅一个源，请从菜单中选择“Feed->Add Feed”，或者在窗口左侧窗格中右键单击“All Feeds”（参见图 3-8），并从弹出菜单中选择“Add Feed”。然后在“Add Feed”对话框中输入该源的 URL，并点击“Ok”。例如，要阅读 Slashdot 的 RSS 源，我输入 `http://slashdot.org/index.rss`。该源的标题会显示在窗口左侧窗格中。点击该源标题以查看此源中的条目。然后，你可以点击右上角窗格中的一个条目，该条目会显示在右下角窗格中，如图 3-8 所示。你可以添加许多不同的 RSS 源，将它们组织到文件夹中，并在 Akregator 中浏览它们。

![](img/792720823146d68f19fd50c99ebfce4b_385_0.png)

**图 3-8：** 你可以在 Akregator 中组织和阅读 RSS 源。

# 第 4 章：使用 FTP

- **本章内容**
- 使用 GNOME FTP 客户端
- 使用任意 Web 浏览器作为 FTP 客户端
- 了解 FTP 命令

顾名思义，*文件传输协议*（FTP）用于在计算机之间传输文件。例如，如果你的互联网服务提供商（ISP）为你提供个人网站空间，你可能已经使用 FTP 上传了组成该网站的文件。使用计算机上的 FTP 客户端，你登录到 ISP 账户，提供密码，然后将文件从你的家庭系统复制到 ISP 的服务器上。

你还可以使用 FTP 匿名下载其他文件，例如从互联网上的其他计算机下载开源软件——在这种情况下，你不需要在远程系统上拥有账户即可下载文件。你只需使用*匿名*（anonymous）作为用户名，并提供你的电子邮件地址作为密码即可登录。（事实上，你的 Web 浏览器可以代你完成这一过程，因此你甚至可能不知道这个过程正在发生。）这种类型的匿名 FTP 非常适合向任何想要的人分发文件。例如，硬件供应商可能会使用匿名 FTP 为需要的人提供更新设备驱动程序。

Linux 附带了几个 FTP 客户端，包括命令行版本和 GUI 版本。在本章中，我将向你介绍几个 GUI FTP 客户端，并描述使用命令行 FTP 客户端时用于处理远程目录的命令。

## 使用图形化 FTP 客户端

你可以在 Linux 中使用以下 GUI FTP 客户端之一：

- gFTP — GNOME 的图形化 FTP 客户端（`http://gftp.seul.org`）
- KBear — KDE 的图形化 FTP 客户端（`http://kbear.sourceforge.net`）
- 用于匿名 FTP 下载的 Web 浏览器，如 Firefox

对于上传文件，你可能需要使用 gFTP，因为此类传输通常需要用户名和密码。Web 浏览器用于匿名下载效果良好，这通常是你从互联网下载软件的方式。

在接下来的两节中，我将简要介绍所有三种 GUI FTP 客户端。

### 使用 gFTP

GNOME 附带了 gFTP，一个图形化 FTP 客户端。gFTP 默认未安装，但你可以从 `http://gftp.seul.org` 下载并轻松安装它。在某些发行版中，它可能已包含在某个软件包中，你只需安装该包即可。

在 Debian 中，在终端窗口中输入 `su -` 并输入 `root` 密码，然后输入 `apt-get install gftp`。

在 Fedora Core 中，从本书的配套 DVD 安装 gFTP。以 `root` 身份登录，将 DVD 插入 DVD 驱动器，并在终端窗口中输入 `mount /mnt/cdrom`。（如果 DVD 驱动器是系统上的第二个 CD/DVD 驱动器，你可能需要将 `cdrom` 更改为 `cdrrom`。）然后输入 `cd /mnt/cdrom/Fedora/RPMS`，接着输入 `rpm -ivh gftp*`。

在 Fedora Core 中，通过选择*主菜单->Internet->gFTP*来启动 gFTP（如果找不到 gFTP，请以 `root` 身份登录并输入 `yum install gftp`，然后在菜单中查找它）。在其他发行版中，你应该能够在主菜单中找到它。gFTP 窗口将出现，如图 4-1 所示。

![](img/792720823146d68f19fd50c99ebfce4b_387_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_387_1.png)

**gFTP** 窗口有一个菜单栏，包含用于执行各种任务的菜单。就在菜单栏下方是一个工具栏，包含一些按钮和文本字段。在这里，你可以输入远程主机名称或 IP 地址、用户名以及登录远程主机所需的密码。图 4-1 显示了填写这些信息并点击带有两台计算机图标的按钮（工具栏最左侧的按钮）建立与远程主机的连接后的 **gFTP** 窗口。

要使用 **gFTP** 上传或下载文件，请遵循以下步骤：

1. **在 Host 字段中填写远程系统的主机名或 IP 地址。**
   如果你以前使用过该主机，当你点击 Host 字段旁边的向下箭头时，会出现一个下拉列表，你可以从中选择该主机。

2. **在 User 字段中提供用户名，在 Pass 字段中提供密码，然后点击带有两台计算机图标的按钮（位于 Host 字段左侧）。**
   此操作会使 **gFTP** 连接到你选定的主机，并使用你提供的用户名和密码登录。**gFTP** 窗口的下半部分显示了两个系统之间交换的 FTP 协议消息。

3. **观察此区域，查看是否有任何错误消息的迹象。**
   远程系统的目录列表显示在 **gFTP** 窗口的右半部分。左半部分显示当前的本地目录。

4. **要从当前系统向远程系统上传一个或多个文件，请在左侧列表中选中文件，然后点击右箭头按钮。**

5. **要从远程系统下载文件，请在右侧列表中选中文件名，然后点击左箭头按钮。**

6. **完成文件传输后，从菜单中选择 FTP:\ Quit。**



如这些步骤所示，使用像 `gFTP` 这样的 GUI FTP 客户端传输文件是一项简单的任务。

> 信不信由你，`gFTP` 不仅用于 FTP 传输。它还可以使用 HTTP 协议传输文件，并使用安全 Shell (SSH) 协议进行安全文件传输。

### 介绍 KBear

`KBear` 是 KDE 的一个 GUI FTP 客户端。在 KDE 桌面上，你可以在主菜单（Internet 类别下）找到它。在 Debian 中，输入 `apt-get install kbear` 来安装 `KBear`（先输入 `su -` 成为 `root` 用户）。

首次启动 KDE 时，系统会运行 `KBear` 向导（`KBear Wizard`），以便你配置 `KBear`。此配置步骤主要涉及 `KBear` 窗口的布局，因此你可以直接接受默认设置。

当主 `KBear` 窗口出现时，它会以类似 Windows 资源管理器的视图显示你的主目录。要连接到 FTP 服务器，请选择“FTP > 快速连接”（FTP>Quick Connect）。随后会弹出一个对话框（见图 4-2），提示你输入 FTP 服务器的主机名以及用户名和密码。

+ 图 4-2：输入远程 FTP 服务器的信息并点击“连接”。

![](img/792720823146d68f19fd50c99ebfce4b_389_0.png)

输入所需信息后，点击“连接”（Connect）。`KBear` 将建立与远程 FTP 服务器的连接。在图 4-3 所示的 `KBear` 主窗口中，你可以并排看到本地目录和远程目录。

现在，你可以通过将一个系统的文件夹中的文件拖动到另一个系统的文件夹中来传输文件，从而使得 FTP 传输就像普通的拖放文件复制一样简单。

使用完 `KBear` 后，请选择“FTP > 退出”（FTP>Quit）或点击工具栏最左侧的“电源”（Power Off）按钮。

## 使用 Web 浏览器作为 FTP 客户端

任何 Web 浏览器都可以充当 FTP 客户端，但此类程序最适合用于匿名 FTP 下载，因为 Web 浏览器可以使用用户名 `anonymous`（匿名）和任意密码进行登录。

### 使用图形化 FTP 客户端

![](img/792720823146d68f19fd50c99ebfce4b_390_0.png)

图 4-3：KDeer 窗口并排显示本地目录和远程 FTP 服务器的目录。

例如，你可以使用 Firefox Web 浏览器作为 FTP 客户端。你只需要知道如何编写 URL，以便让 Web 浏览器知道你想使用 FTP 下载文件。FTP URL 的语法如下：

```
ftp://hostname/pathname
```

第一部分（ `ftp://` ）表示你想要进行 FTP 传输。`hostname` 部分是 FTP 服务器的名称（名称通常以 ftp 开头——例如，`ftp.netscape.com`）。`pathname` 是你想要下载的文件所在的全目录路径和文件名。

如果你只提供 FTP 服务器的主机名，Web 浏览器将显示匿名 FTP 目录的内容。如果你想在你的 Linux 系统上访问匿名 FTP，请启动 Firefox（点击 GNOME 面板上的 Web 浏览器图标），在“位置”（Location）文本框中输入 FTP URL，然后按 Enter。例如，在我的系统上，我输入 `ftp://localhost/pub/` 来访问 `pub` 目录。

图 4-4 展示了 Firefox 中匿名 FTP 目录的典型外观。你可以点击文件夹查看其内容并下载任何文件。虽然我展示了如何使用 Firefox 的 FTP 功能访问本地系统，但 FTP 的目的（当然是）从其他系统下载文件到你的系统。

图 4-4：你可以使用 Web 浏览器从匿名 FTP 服务器下载文件。

![](img/792720823146d68f19fd50c99ebfce4b_391_0.png)

**警告！**

当你使用 `ftp://localhost/` URL 时，如果你没有运行 FTP 服务器，或者你设置了防火墙不允许 FTP 连接，系统将不会给出响应。

![](img/792720823146d68f19fd50c99ebfce4b_391_1.png)

在 Debian 和 Fedora Core 中，以 `root` 身份登录并在终端窗口中输入 `/etc/init.d/vsftpd start` 以启动 FTP 服务器。在 SUSE 中，`xinetd` 超级服务器控制 FTP 服务器 `vsftpd`。`/etc/xinetd.d/vsftpd` 配置文件指定了如何启动 `vsftpd`。有关 `xinetd` 配置文件的更多信息，请参阅第七卷第一章。

如果你输入其他某个匿名 FTP 服务器的主机名，访问匿名 FTP 站点的相同方法也适用。例如，尝试输入以下 URL：

```
ftp://ftp.netscape.com/
```

你将看到 `ftp.netscape.com` 服务器的目录。

# 使用命令行 FTP 客户端

了解如何从命令行使用 FTP 是个好主意——以防万一。例如，如果你的 GUI 桌面无法正常工作，你可能需要下载一些文件来修复问题。如果你知道如何使用命令行 FTP 客户端，你就可以下载文件并解决问题。这并不太难，而且所有 Linux 发行版都提供了命令行 FTP 客户端。

弄清楚命令行 FTP 客户端的最佳方法是动手尝试。该命令名为 `ftp`，你可以在 Linux 系统上运行 `ftp` 命令。你甚至不需要 Internet 连接，因为你可以使用 `ftp` 命令连接到自己的系统——我会向你展示如何操作。

请注意，`ftp` 命令的确切输出可能会有所不同，因为某些发行版（如 Debian）使用 `gFTP` 的文本模式版本作为命令行 FTP 客户端。

在下面的示例 FTP 会话中，我使用命令行 FTP 客户端以我的用户名（`naba`）登录，并浏览我的一个 Linux 系统上的目录。当你尝试类似的操作时，请用你的用户名替换该名称并提供你的密码。以下是展示与典型命令行 FTP 客户端交互的列表（我的评论以斜体显示，我输入的文字以粗体显示）：



```
ftp localhost
Connected to localhost.localdomain.
220 (vsFTPd 2.0.3)
Name (localhost:naba):       (我按 Enter。)
331 Please specify the password.
Password:                    (我输入我的密码。)
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> **help**              (我输入 help 以查看 FTP
命令列表。)
Commands may be abbreviated. Commands are:

!       debug         mdir        qc        send
$       dir           mgmt        sendport  site
account disconnect    mkdir       put       size
append  exit          mls         pwd       status
ascii   form          mode        quit      struct
bell    get           mtime       quote     system
binary  glob          mput        recv      sunixic
bye     hash          newer       recuper   tenex
case    help          nmap        restatus  tick
cd      idle          nlist       rhelg     trace
cdup    image         mtrans      rename    type
chmod   lcd           open        reset     user
close   ls            prompt      restart   umask
cr      macdef        passive     rmdir     verbose
delete  mdelete       proxy       runique   ?
ftp> **help mget**       (我可以在特定命令上获取帮助。)
mget          get multiple files
ftp> **cd /var**        (这将目录更改为 /var。)
250 Directory successfully changed.
ftp> **ls**          (此命令列出
目录的内容。)
227 Entering Passive Mode (127,0,0,1,38,142)
150 Here comes the directory listing.
... lines deleted...
226 Directory send OK.
ftp> **bye**           (此命令结束会话。)
221 Goodbye.
```

如上所示，通过输入命令 `ftp hostname` 即可启动命令行 FTP 客户端，其中 `hostname` 是你想要访问的系统的名称。当 FTP 客户端与远程系统的 FTP 服务器建立连接后，FTP 服务器会提示你输入用户名和密码。在你提供信息后，FTP 客户端会显示 `ftp>` 提示符，你可以开始输入命令以执行特定任务。如果你记不起某个特定的 FTP 命令，请输入 `help` 以查看命令列表。你可以通过输入 `help command` 来获取特定命令的额外帮助，其中 `command` 是你需要帮助的特定命令。

许多 FTP 命令与用于导航文件系统的 Linux 命令相似。例如，`cd` 更改目录，`pwd` 打印当前工作目录的名称，`ls` 列出当前目录的内容。另外两个常用命令是 `get` 和 `put`：`get` 用于从远程系统下载文件到你的系统，`put` 用于从你的系统上传（发送）文件到远程主机。

表 4-1 描述了一些常用的 FTP 命令。你不必输入完整的 FTP 命令。对于长命令，你只需输入前几个字符——足以唯一识别该命令即可。例如，要删除一个文件，你可以输入 `dele`；要将文件传输模式更改为二进制模式，你可以输入 `bin`。

![](img/792720823146d68f19fd50c99ebfce4b_393_0.png)

从 Internet 下载文件时，你几乎总是希望以二进制模式传输文件，因为软件通常以二进制形式归档和压缩。（它们不是纯文本文件。）因此，始终使用 `binary` 命令将模式设置为二进制。然后使用 `get` 命令下载文件。

![](img/792720823146d68f19fd50c99ebfce4b_393_1.png)

在传输多个名称相似的文件（例如 `image1.jpg`、`image2.jpg` 等）时，输入 `prompt` 以关闭提示。（否则，每次文件传输后，FTP 客户端都会询问你是否要传输下一个文件。）然后输入 `mget` 后跟带有通配符的文件名。例如，要下载所有以 `image` 开头且以 .jpg 扩展名结尾的文件，请输入 `mget image*.jpg`。

| 命令 | 描述 |

| :--- | :--- |

| ! | 在本地系统上执行 shell 命令。例如，`<code>! ls</code>` 列出本地系统当前目录的内容。 |

| ? | 显示命令列表（等同于 `help`） |

| append | 将本地文件追加到远程文件 |

| ascii | 将文件传输类型设置为 ASCII（或纯文本）。此命令是默认的文件传输类型。 |

# 使用命令行 FTP 客户端

| 命令 | 说明 |

|---|---|

| `binary` | 将文件传输类型设置为二进制 |

| `bye` | 结束与远程 FTP 服务器的 FTP 会话，并退出 FTP 客户端 |

| `cd` | 更改远程系统上的目录。例如，`cd /pub/Linux` 将远程目录更改为 `/pub/Linux`。 |

| `chmod` | 更改远程文件的权限设置。例如，`chmod 644 index.html` 更改远程系统上 `index.html` 文件的权限设置。 |

| `close` | 结束与 FTP 服务器的 FTP 会话，并返回到 FTP 客户端的提示符 |

| `delete` | 删除远程文件。例如，`delete bigimage.jpg` 删除远程系统上的该文件。 |

| `dir` | 列出远程系统当前目录的内容 |

| `disconnect` | 结束 FTP 会话并返回到 FTP 客户端的提示符。（此命令与 `close` 相同。） |

| `get` | 下载远程文件。例如，从远程系统 `get junk.tar.gz` 并将其保存为本地系统上的文件 `junk.tgz`。 |

| `hash` | 开启或关闭显示文件传输进度的井号（#）打印。当此功能开启时，每从远程系统传输 1,024 字节，屏幕上就会打印一个井号。（这是进度条的命令行版本。） |

| `help` | 显示命令列表 |

| `image` | 与 `binary` 相同 |

| `lcd` | 更改本地系统上的当前目录。例如，`lcd /var/ftp/pub` 将当前本地目录更改为 `/var/ftp/pub`。 |

| `ls` | 列出当前远程目录的内容 |

| `mdelete` | 删除远程系统上的多个文件。例如，`mdelete *.*` 删除当前目录中所有以 `.jpg` 结尾的远程文件名。 |

| `mdir` | 列出多个远程文件，并将列表保存在指定的本地文件中。例如，`mdir /usr/share/doc/*` 将列表保存在名为 `wlist` 的本地文件中。 |

| `mget` | 下载多个文件。例如，`mget *.jpg` 下载所有以 `.jpg` 结尾的文件。如果开启了提示，FTP 客户端会在下载每个文件前请求确认。 |

| `mkdir` | 在远程系统上创建目录。`mkdir images` 在远程系统当前目录下创建名为 `images` 的目录。 |

| `mls` | 与 `mzdir` 相同 |

| `mput` | 上传多个文件。例如，`mput *.jpg` 将所有以 `.jpg` 结尾的文件发送到远程系统。如果开启了提示，FTP 客户端会在发送每个文件前请求确认。 |

| `open` | 打开与指定主机上 FTP 服务器的连接。例如，`open ftp.netscape.com` 连接到主机 `ftp.netscape.com` 上的 FTP 服务器。 |



| `prompt` | 开启或关闭提示功能。当提示开启时，在传输多个文件期间，FTP 客户端会在下载或上传每个文件前提示您确认。 |
| `put` | 将文件发送到远程系统。例如，`put index.html` 将 `index.html` 文件从本地系统发送到远程系统。 |
| `pwd` | 显示远程系统当前目录的完整路径名。当您以用户身份登录时，初始当前工作目录是您的主目录。 |
| `quit` | 与 `bye` 相同 |
| `recv` | 与 `get` 相同 |
| `rename` | 重命名远程系统上的文件。例如，`rename old.html new.html` 将远程系统上的文件 `old.html` 重命名为 `new.html`。 |
| `rmdir` | 删除远程系统上的目录。例如，`rmdir images` 删除远程系统当前目录中的 `images` 目录。 |
| `send` | 与 `put` 相同 |
| `size` | 显示远程文件的大小。例如，`size bigfile.tar.gz` 显示该远程文件的大小。 |
| `status` | 显示 FTP 客户端的当前状态 |
| `user` | 向 FTP 服务器发送新的用户信息。例如，`user naba` 发送用户名 `naba`；然后 FTP 服务器会提示输入该用户的密码。 |

# 第五卷：系统管理

![](img/792720823146d68f19fd50c99ebfce4b_396_0.png)

> “这部分测试告诉我们你是否适合担任网络管理员这一工作。”

## 内容一览

- 第 1 章：介绍基本的系统管理......373
- 第 2 章：管理用户和组 ..............413
- 第 3 章：管理文件系统 ....................425
- 第 4 章：安装和更新应用程序 .........449
- 第 5 章：自定义 Linux 内核 ...............473

# 第 1 章：介绍基本的系统管理

**本章内容**

- 介绍图形用户界面（GUI）系统管理工具
- 成为 root 用户
- 理解系统启动过程
- 检查系统配置文件
- 通过 `/proc` 文件系统查看系统信息
- 监控系统性能
- 管理设备
- 安排作业

系统管理或 sysadmin 指为保持计算机系统正常运行所需执行的所有操作。*系统管理员*（也称为 *sysadmin*）就是负责处理这些任务的人。

如果你是在家中或小型办公室运行 Linux，你很可能就是这些系统的系统管理员。或者，你可能是整个局域网中所有 Linux 系统的系统管理员。这都没关系。在本章中，我将向你介绍基本的系统管理程序，并展示如何执行一些常见任务。

每个 Linux 发行版都附带许多用于执行特定系统管理任务的图形工具。在本章中，我会向你介绍其中一些 GUI 工具，并在本小书的其他章节中更详细地描述其中的一些。

## 盘点系统管理任务

那么，系统管理任务包括什么？我随口给出的答案是*任何你需要做的、能保持系统良好运行的事情*。更准确地说，系统管理员的职责包括以下内容：

- **添加和删除用户账户。** 你必须添加新的用户账户并删除不必要的用户账户。如果用户忘记了密码，你必须更改密码。
- **管理系统打印。** 你必须打开或关闭打印队列，检查打印队列的状态，并在必要时删除打印作业。
- **安装、配置和升级操作系统及各种实用工具。** 你必须安装或升级 Linux 操作系统以及其他作为操作系统一部分的软件组件。
- **安装新软件。** 你必须安装各种包格式（如 RPM 或 DEB）的软件。你还必须下载和解包以源代码形式提供的软件——然后从源代码构建可执行程序。
- **管理硬件。** 有时，你必须添加新硬件并安装驱动程序，以便设备正常工作。
- **制作备份。** 你必须备份文件，可以使用软盘驱动器、USB 内存棒或磁带（如果你有磁带驱动器的话）。
- **挂载和卸载文件系统。** 例如，当你想访问 CD-ROM 上的文件时，你必须将该 CD-ROM 的文件系统挂载到 Linux 文件系统中的某个目录上。你还可能需要挂载软盘，包括 Linux 格式和 DOS 格式。
- **自动化任务。** 你必须安排 Linux 任务自动执行（在特定时间）或定期执行（以固定间隔）。
- **监控系统性能。** 你可能需要关注系统性能，以查看处理器将大部分时间花在哪里，以及系统中的空闲和已用内存数量。
- **启动和关闭系统。** 虽然启动系统通常只需要给 PC 上电，但关闭 Linux 系统时需要小心。如果系统设置为图形登录屏幕，你可以通过从登录屏幕选择菜单项来执行关机操作。否则，使用 `shutdown` 命令在关闭 PC 电源开关之前停止所有程序。
- **监控网络状态。** 如果你有网络连接（无论是 LAN、DSL 线路还是电缆调制解调器连接），你可能需要检查各种网络接口的状态，并确保你的网络连接正常。
- **设置主机和网络安全。** 你必须确保系统文件受到保护，并且你的系统能够防御来自网络攻击。
- **监控安全。** 你必须密切关注任何入侵行为，通常通过检查日志文件来实现。

任务列表很长！本章没有涵盖所有这些任务，但小书的其他部分描述了其中大部分任务。在这里，我重点介绍一些基础知识，包括向你介绍一些 GUI 工具，解释如何成为 `root`（超级用户），描述系统配置文件，以及展示如何监控系统性能、管理设备和设置定期任务。

## 介绍一些 GUI 系统管理工具

每个 Linux 发行版都配备了用于执行系统管理任务的 GUI 工具。这些 GUI 工具会提示用户输入，然后运行必要的 Linux 命令来执行任务。在以下各节中，我将简要介绍 Debian、Fedora Core、SUSE 和 Xandros 中的 GUI 系统管理工具。

### Debian 中的 GUI 系统管理工具

Debian 默认使用 GNOME 桌面环境，并提供了用于执行系统管理任务的一些 GUI 工具。这些工具位于“应用程序➔系统工具”菜单中。表 1-1 列出了一些常见任务以及用于启动相应 GUI 工具以执行该任务的菜单选项。

| 表 1-1 | 在 Debian 中使用 GUI 工具执行系统管理任务 |
| :--- | :--- |
| 要执行的操作 | 从 Debian GNOME 桌面中选择以下选项 |
| 添加或删除软件包 | 应用程序➔系统工具➔Synaptic 软件包管理器 |
| 更改日期或时间 | 应用程序➔系统工具➔时间和日期 |
| 更改密码 | 主菜单➔设置➔更改密码 |
| 配置桌面 | 应用程序➔桌面设置 |
| 配置网络 | 应用程序➔网络 |
| 格式化软盘 | 应用程序➔系统工具➔软盘格式化器 |
| 管理打印机 | 应用程序➔系统工具➔打印机 |
| 管理用户账户 | 应用程序➔系统工具➔用户和组 |
| 监控系统性能 | 应用程序➔系统工具➔系统监视器 |
| 查看系统日志 | 应用程序➔系统工具➔系统日志 |

### Fedora Core 中的 GUI 系统管理工具

Fedora Core 附带了一组 GUI 系统配置工具，可以减轻执行典型系统管理工作的负担。表 1-2 简要总结了用于启动特定任务 GUI 工具的菜单选项。

**表 1-2 在 Fedora Core 中启动 GUI 系统管理工具**

| 要配置或管理的对象 | 通过选择此选项启动 GUI 工具 |
| :------------------------- | :----------------------------- |
| 日期和时间 | 系统→管理→日期和时间 |
| 磁盘和 DVD/CD-ROM | 应用程序→系统工具→磁盘管理 |
| 显示设置 | 系统→管理→显示 |
| 防火墙设置 | 系统→管理→安全级别和防火墙 |
| 硬件 | 应用程序→系统工具→硬件浏览器 |
| 互联网连接 | 系统→管理→网络 |
| 网络 | 系统→管理→网络 |
| 首选项（如桌面和密码） | 系统→首选项 |
| 打印机 | 系统→管理→打印 |
| root 密码 | 系统→管理→Root 密码 |
| 服务器 | 系统→管理→服务器设置 |
| 软件 | 系统→管理→添加/删除应用程序 |
| 系统性能 | 应用程序→系统工具→系统监视器 |
| 用户账户 | 系统→管理→用户和组 |

### Knoppix 中的 GUI 系统管理工具

Knoppix 是一个 Live CD 发行版，你可以用它来试用 Linux 或修复现有 Linux 系统中的问题。因此，Knoppix 附带了多个可用于系统管理任务的 GUI 工具。表 1-3 总结了 Knoppix 中的一些 GUI 工具。

**表 1-3 在 Knoppix 中使用 GUI 工具执行系统管理任务**

| 要执行的操作 | 从 Knoppix GUI 桌面中选择此选项 |
| :--------- | :---------------------------------------- |
| 配置桌面 | 主菜单→设置→桌面设置向导 |



| 配置 KDE | 主菜单→设置→控制中心 |
| 配置网络 | 主菜单→KNOPPIX→网络/互联网→网卡配置 |
| 配置打印机 | 主菜单→KNOPPIX→配置→配置打印机 |
| 查找文件 | 主菜单→查找文件 |
| 管理磁盘分区（用于故障排除现有 Linux 安装） | 主菜单→系统→QTParted |
| 以 root 权限打开终端窗口 | 主菜单→KNOPPIX→Root 外壳 |
| 启动 Samba 服务器 | 主菜单→KNOPPIX→服务→启动 Samba 服务器 |
| 启动 SSH 服务器 | 主菜单→KNOPPIX→服务→启动 SSH 服务器 |

### MEPIS 中的 GUI 系统管理工具

你可以将 MEPIS 作为 Live CD 运行，也可以将其安装在硬盘上。MEPIS 使用 KDE 桌面环境，并包含用于系统管理任务的一些 GUI 工具。MEPIS 的独特之处在于 MEPIS OS 中心，它允许你执行系统管理任务。你可以通过选择主菜单➔MEPIS OS 中心来启动它。图 1-1 展示了 MEPIS OS 中心的主窗口，你可以从该窗口在运行 MEPIS 作为 Live CD 时将其安装到硬盘上，并执行一些系统配置和维护任务。

![](img/792720823146d68f19fd50c99ebfce4b_402_0.png)

除了 MEPIS OS 中心，你还可以使用 KDE 控制中心（选择主菜单➔控制中心）来执行一些系统管理和配置任务。表 1-4 列出了 MEPIS 中可用于特定系统管理任务的其他一些 GUI 工具。

**表 1-4 MEPIS 中用于系统管理任务的一些 GUI 工具**

| 要执行的操作 | 从 MEPIS GUI 桌面中选择此选项 |
| :--------- | :------------------------------------- |
| 配置桌面 | 主菜单➔系统➔设置➔桌面设置向导 |
| 配置 KDE | 主菜单➔控制中心 |
| 配置打印机 | 主菜单➔系统➔设置➔打印管理器 |
| 查找文件 | 主菜单➔查找文件 |
| 安装软件 | 主菜单➔系统➔Synaptic 软件包管理器 |
| 管理磁盘分区（用于故障排除现有 Linux 安装） | 主菜单➔系统➔文件系统➔QTparted |
| 管理用户账户 | 主菜单➔系统➔KUser |
| 以 root 权限打开终端窗口 | 主菜单➔系统➔终端程序 - 超级用户模式 |

### SUSE 中的 GUI 系统管理工具

在 SUSE 中，选择主菜单➔系统➔YaST 以在 YaST 控制中心开始你的系统管理任务。图 1-2 展示了 YaST 控制中心窗口。

![](img/792720823146d68f19fd50c99ebfce4b_403_0.png)

YaST 控制中心的左侧显示了你可以执行的任务类别的图标。右侧显示了当前选中类别中特定任务的图标。当你点击 YaST 控制中心右侧的某个图标时，会出现一个新的 YaST 窗口，使你能够执行该任务。

表 1-5 总结了你在 YaST 控制中心左侧看到的每个类别图标对应的任务。正如你可以从表 1-5 第二列的条目中看到的，YaST 控制中心确实是所有系统管理事务的一站式服务。

**表 1-5 YaST 控制中心中按类别划分的任务**

| 此类别 | 允许你配置/管理以下内容 |
| :--- | :--- |
| 软件 | 在线更新、安装源、在 Xen 环境中安装、安装到目录、媒体检查、补丁 CD 服务器、软件管理、系统更新 |
| 硬件 | 蓝牙、CD-ROM 驱动器、磁盘控制器、显卡和显示器、硬件信息、IDE DMA 模式、红外设备、摇杆、键盘布局、鼠标型号、打印机、扫描仪、声音、电视卡 |
| 系统 | /etc/sysconfig 编辑器、引导加载程序配置、引导或救援软盘、日期和时间、LVM、语言、PCI 设备驱动程序、分区器、电源管理、Powerweark、配置档案管理器、系统备份、系统恢复、系统服务（运行级别） |
| 网络设备 | DSL、传真、ISDN、调制解调器、网卡、电话应答机 |
| 网络服务 | DHCP 服务器、DNS 服务器、DNS 主机和名称、HTTP 服务器、主机名、Kerberos 客户端、LDAP 客户端、邮件传输代理、NFS 客户端、NFS 客户端、NIS 客户端、NIS 服务器、NTP 客户端、网络服务（xinetd）、代理、远程管理、路由、SLP 浏览器、Samba 客户端、Samba 服务器、TFTP 服务器 |
| 安全和用户 | 防火墙、组管理、本地安全、用户管理 |
| 其他 | 自动安装、发布支持查询、厂商驱动 CD、查看启动日志、查看系统日志 |

### Ubuntu 中的 GUI 系统管理工具

Ubuntu 使用 GNOME 桌面环境，其菜单组织方式类似于 Fedora Core 的 GNOME 桌面环境。你可以在以下菜单中找到 Ubuntu 的 GUI 系统管理工具：应用程序→系统工具、系统→管理以及系统→首选项。表 1-6 列出了用于启动部分 GUI 工具的菜单选项。

## Ubuntu 中的 GUI 系统管理工具

### 表 1-6：在 Ubuntu 中启动 GUI 系统管理工具

| 要配置或管理的内容 | 通过选择以下项启动 GUI 工具 |
| :--- | :--- |
| 日期和时间 | 系统►管理►时间和日期 |
| 显示设置 | 系统►首选项►屏幕分辨率 |
| 硬件 | 系统►管理►设备管理器 |
| 互联网连接 | 系统►管理►网络 |
| 网络 | 系统►管理►网络 |
| 首选项，如桌面和默认应用程序 | 系统►首选项 |
| 打印机 | 系统►管理►打印 |
| root 密码 | 系统►管理►Root 密码 |
| 服务器 | 系统►管理►服务器设置 |
| 软件 | 应用程序►系统工具►添加/删除程序 |
| 系统日志 | 应用程序►系统工具►系统日志 |
| 系统性能 | 应用程序►系统工具►系统监视器 |
| 更新 | 系统►管理►Ubuntu 更新管理器 |
| 用户账户 | 系统►管理►用户和组 |

### Xandros 中的 GUI 系统管理工具

Xandros 被设计为一个桌面操作系统，因此你可以轻松地从桌面访问所有功能。对于大多数系统管理任务，你从 Xandros 控制中心开始——选择主菜单►控制中心即可到达。（图 1-3 展示了你到达那里时看到的内容。）

如你所见，窗口左侧显示了任务类别的树状菜单。你可以点击类别旁边的加号来查看子类别。当你点击某个具体任务时，窗口右侧会显示用于执行该任务的 GUI 界面。

对于某些任务，例如挂载文件系统或添加打印机，你可以通过选择主菜单►应用程序►系统►管理员工具►Xandros 文件管理器（管理员）以系统管理员身份打开 Xandros 文件管理器。系统会提示你输入 root 密码。图 1-4 展示了 Xandros 文件管理器窗口，你可以从中执行一些系统管理任务。

![](img/792720823146d68f19fd50c99ebfce4b_406_0.png)

**图 1-3：** 你可以从 Xandros 控制中心执行许多系统管理任务。

![](img/792720823146d68f19fd50c99ebfce4b_406_1.png)

**图 1-4：** 对于某些系统管理任务，请使用 Xandros 文件管理器。

## 如何获得 root 权限

你必须登录为 `root` 才能执行系统管理任务。`root` 用户是超级用户，是唯一拥有在系统中执行任何操作所需所有特权的账户。

通常的共识是，*不应该*以 `root` 身份登录。当你处于 `root` 状态时，一个失误就可能轻易删除所有文件——尤其是在输入命令时。举个例子，你可能输入 `rm *.html` 命令来删除所有扩展名为 .html 的文件。如果你不小心在星号 (*) 后按了空格键会怎样？Shell 会将命令解释为 `rm *.html`，并且——因为 * 匹配任何文件名——删除当前目录中的所有文件。这听起来难以置信，直到它发生在你身上！

### 使用 su - 命令

如果你登录的是一个普通用户，如何执行任何系统管理工作呢？好吧，你暂时变成 root 即可。如果你在终端窗口或控制台上工作，请输入

`su -`

然后在提示符响应中输入 root 密码。从这一刻起，你就是 root。做任何你需要做的事。要恢复到你平时的身份，请输入

`exit`

就这样了！就是这么简单。

![](img/792720823146d68f19fd50c99ebfce4b_407_0.png)

顺便说一下，Knoppix 有 root 用户但没有 root 密码，因此你只需在终端窗口的 shell 提示符下输入 `su -` 即可成为 root。此外，Ubuntu 没有 root 用户。要在 Ubuntu 中执行任何需要 root 特权的任务，你必须输入 `sudo` 后跟命令，并在提示时提供你的普通用户密码。

### 为 GUI 工具获取 root 权限



大多数 Linux 发行版都包含用于执行系统管理工作的 GUI 工具。如果你使用这些 GUI 工具执行需要 root 权限的任务，该工具通常会弹出一个对话框，提示你输入 root 密码，如图 1-5 所示（但在 Ubuntu 中，GUI 工具会提示你输入普通用户密码）。只需输入密码并按 Enter。如果你不想使用该工具，点击取消。

![](img/792720823146d68f19fd50c99ebfce4b_407_1.png)

**图 1-5：** 输入 root 密码并按 Enter 以获得 root 权限。

## 从遗忘的 root 密码中恢复

要执行系统管理任务，你必须知道 `root` 密码。如果你忘记了 `root` 密码怎么办？别担心：只需重新启动电脑，然后按照以下步骤重置 `root` 密码：

1. 重新启动电脑（在注销 GUI 屏幕时选择重新启动）或像往常一样开机。

很快你会看到图形化的 GRUB 引导加载程序屏幕，其中显示了你可以启动的操作系统名称。如果你的系统运行的是 LILO 引导加载程序，请按 `Ctrl+X`，并在 `boot:` 提示符下输入 `linux single` 然后按 Enter。然后继续执行步骤 4。

2. 如果你安装了多个操作系统，请使用方向键选择 Linux 作为你的操作系统。然后按 `A` 键。GRUB 提示你添加其默认启动命令的操作。

3. 按空格键，输入以下内容，然后按 Enter：

```
single
```

Linux 像往常一样启动，但运行在单用户模式下，不需要登录。Linux 启动后，你会看到以下命令行提示符，以井号 (#) 结尾，类似于以下内容：

```
sh-3.00#
```

4. 输入 `passwd` 命令更改 `root` 密码，如下所示：

```
sh-3.00# passwd
Changing password for user root.
New password:
```

5. 输入你想要使用的新 `root` 密码（它不会在屏幕上显示），然后按 Enter。

Linux 再次询问密码，如下所示：

```
Retype new password:
```

6. 再次输入密码并按 Enter。

如果你两次输入相同的密码，`passwd` 命令就会更改 `root` 密码。

7. 现在输入 `reboot` 以重新启动电脑。

Linux 启动后，它显示熟悉的登录屏幕。现在你可以使用新密码以 `root` 身份登录。

![](img/792720823146d68f19fd50c99ebfce4b_409_0.png)

在 SUSE Linux 中，在步骤 3 中，输入 `single init=/bin/sh`（而不是 `single`），并在继续执行步骤 4 之前，输入 `mount / -n -o remount,rw`。然后执行步骤 4 到 6 以更改 `root` 密码。更改密码后，输入 `mount / -n -o remount,ro`。然后继续步骤 7 并重新启动电脑。

![](img/792720823146d68f19fd50c99ebfce4b_409_1.png)

确保你的 Linux 电脑在*物理*上是安全的。如这些步骤所示，任何能够物理访问你的 Linux 电脑的人都可以简单地重新启动，设置新的 `root` 密码，并对系统为所欲为。

保护密码不被重置的另一种方法是设置 GRUB 密码，这会导致 GRUB 在启动 Linux 之前要求输入有效密码。当然，每次启动系统时，你必须记得输入 GRUB 密码！

## 理解 Linux 的启动过程

了解 Linux 启动时启动进程的顺序非常重要。你可以利用这些知识来启动和停止服务，例如 Web 服务器和网络文件系统 (`NFS`)。接下来的几节提供了 Linux 启动过程以及初始进程集启动方式的概述。这些章节还让你熟悉在 Linux 系统上启动各种服务的 shell 脚本。

### 理解 init 进程

当 Linux 启动时，它从硬盘加载并运行核心操作系统程序。核心操作系统旨在运行其他程序。名为 `init` 的进程在你的 Linux 系统上启动了初始的一组进程。

要查看当前在系统上运行的进程，请输入

```
ps ax | more
```

你会得到一份列出的输出，开头如下所示：

```
PID TTY STAT TIME COMMAND
1 ? S 0:22 init [2]
```

第一列，标题为 `PID`，显示每个进程的编号。`PID` 代表进程 ID (*identification*)——由 Linux 内核分配的序列号。进程列表中的第一个条目，进程 ID (`PID`) 为 1，是 `init` 进程。它是第一个进程，并启动你 Linux 系统中的所有其他进程。这就是为什么 `init` 有时被称为“所有进程之母”。

`init` 进程启动哪些内容取决于以下因素：

- 运行级别（run level），这是一个标识符，用于识别系统配置，在该配置中只允许一组选定的进程存在。

- `/etc/inittab` 文件的内容，这是一个文本文件，指定了在不同运行级别下应启动哪些进程。

- 在特定运行级别下执行的若干 shell 脚本。（这些脚本位于 `/etc/init.d` 目录以及 `/etc` 中的若干子目录——这些子目录的名称以 `rc` 开头。）

![](img/792720823146d68f19fd50c99ebfce4b_410_0.png)

大多数 Linux 发行版使用七个运行级别——从 0 到 6。运行级别的含义因发行版而异。表 I-7 列出了运行级别的含义，并指出了 Fedora Core、Debian、MEPIS、SUSE、Ubuntu 和 Xandros 中的一些特定操作。

**表 I-7 Linux 中的运行级别**

| 运行级别 | 含义 |
| :--- | :--- |
| 0 | 关闭系统 |
| 1 | 以单用户独立模式运行（其他人无法登录；你在文本控制台上工作） |
| 2 | 以多用户模式运行（Debian、Ubuntu 和 Xandros 使用运行级别 2 作为默认运行级别） |
| 3 | 以完全多用户模式运行（用于 Fedora Core、MEPIS 和 SUSE 的文本模式登录） |
| 4 | 以完全多用户模式运行（在 Fedora Core、MEPIS 和 SUSE 中未使用） |
| 5 | 以完全多用户模式运行（在 Fedora Core、MEPIS 和 SUSE 中用作带有图形化登录的默认运行级别） |
| 6 | 重新启动系统 |

![](img/792720823146d68f19fd50c99ebfce4b_410_1.png)

当前运行级别与 `/etc/inittab` 文件的内容共同控制 `init` 在 Linux 中启动哪些进程。Debian、Ubuntu 和 Xandros 的默认运行级别是 2。在 Fedora Core、MEPIS 和 SUSE 中，运行级别 3 用于文本模式登录屏幕，5 用于图形化登录屏幕。你可以通过编辑 `/etc/inittab` 文件中的一行来更改默认运行级别。

要检查当前运行级别，请在终端窗口中输入以下命令：

```bash
/sbin/runlevel
```

在 Debian 中，`runlevel` 命令会输出类似以下内容：

```
N 2
```

输出的第一个字符显示上一个运行级别（*N* 表示没有上一个运行级别），第二个字符显示当前运行级别（*2*）。在这种情况下，系统以运行级别 2 启动。如果你在 Fedora Core 或 MEPIS 中处于图形用户界面（GUI）桌面环境，`runlevel` 命令应显示 *5* 作为当前运行级别。

## 检查 /etc/inittab 文件

`/etc/inittab` 文件是理解 `init` 在各种运行级别下启动哪些进程的关键。你可以使用 `more` 命令查看文件内容，如下所示：

```
more /etc/inittab
```

![](img/792720823146d68f19fd50c99ebfce4b_411_0.png)

要使用 `more` 命令查看 `/etc/inittab` 文件的内容，你不必以 `root` 身份登录。

要解释 `/etc/inittab` 文件的内容，请遵循以下步骤：

1.  **查找包含短语 `initdefault` 的行。**

    以下是 Debian 系统中 `/etc/inittab` 文件的那一行：

    `id:2:initdefault:`

    该行显示默认运行级别。在这种情况下，它是 2。

2.  **查找所有指定 `init` 在运行级别 2 下运行什么的行。查找一个在前两个冒号（:）之间有数字 2 的行。** 以下是 Debian 中的一行相关内容：

    `l2:2:wait:/etc/init.d/rc 2`

    该行指定 `init` 执行文件 `/etc/init.d/rc`，参数为 `2`。



如果你查看 Debian 系统中的文件 `/etc/init.d/rc`，你会发现它是一个 shell 脚本。你可以研究这个文件，查看它是如何为运行级别 1 到 5 启动各种进程的。

![](img/792720823146d68f19fd50c99ebfce4b_411_1.png)

`/etc/inittab` 文件中的每个条目都告知 `init` 在一个或多个运行级别下要做什么——你只需列出进程运行的所有运行级别即可。每个 `inittab` 条目有四个字段——由冒号分隔——格式如下：

```
id:runlevels:action:process
```

表 1-8 说明了每个字段的含义。

**表 1-8 inittab 条目中各字段的含义**

| 字段 | 含义 |
| :--- | :--- |
| id | 唯一的单字符或双字符标识符。`init` 进程内部使用此字段。你可以使用任何你想要的标识符，只要不要在同一行上使用相同的标识符即可。 |
| runlevels | 一个由零个或多个字符组成的序列，每个字符表示一个运行级别。例如，如果 runlevels 字段是 12345，则该条目适用于运行级别 1 到 5 中的每一个。如果 action 字段设置为 sysinit、boot 或 bootwait，则忽略此字段。 |
| action | 告知 `init` 进程对该条目做什么。例如，如果此字段为 initdefault，`init` 将把 runlevels 字段解释为默认运行级别。如果此字段设置为 wait，`init` 将启动 process 字段中指定的程序或脚本，并等待该进程退出。 |
| process | `init` 启动的脚本或程序的名称。当然，action 字段的某些设置不需要 process 字段。例如，当 action 字段为 initdefault 时，不需要 process 字段。 |

### 使用 init 命令尝试新的运行级别

要尝试新的运行级别，你不必更改 `/etc/inittab` 文件中的默认运行级别。如果你以 root 身份登录，你可以输入 `init` 后跟运行级别来更改运行级别（从而更改在 Linux 中运行的进程）。

例如，要将系统置于单用户模式，请输入以下内容：

```
init 1
```

因此，如果你想在不更改 `/etc/inittab` 文件中默认运行级别的情况下尝试运行级别 3，请在 shell 提示符下输入以下命令：

```
init 3
```

系统结束所有当前进程并进入运行级别 3。默认情况下，`init` 命令在停止所有当前进程并为运行级别 3 启动新进程之前会等待 20 秒。

若要立即切换到运行级别 3，请输入命令 `init -t 0 3`。`-t` 选项后的数字表示 `init` 在更改运行级别前等待的秒数。

你还可以使用 `telinit` 命令，它只是 `init` 的一个符号链接（快捷方式）。如果你对 `/etc/inittab` 文件进行了更改并希望 `init` 重新加载其配置文件，请使用命令 `telinit q`。

## 理解 Linux 启动脚本

`init` 进程在系统启动时运行若干脚本。在接下来的讨论中，我使用 Debian 系统作为示例，但基本顺序在其他发行版中类似——只有脚本的名称和位置可能有所不同。

如果你查看 Debian 系统中的 `/etc/inittab` 文件，你会发现文件开头附近有以下几行：

```
# Boot-time system configuration/initialization script.
si::sysinit:/etc/init.d/rcS
```

第一行是注释行。第二行导致 `init` 运行 `/etc/init.d/rcS` 脚本——这是 `init` 在 Debian 系统中运行的第一个 Linux 启动脚本。`rcS` 脚本执行许多初始化任务，例如挂载文件系统、设置时钟、配置键盘布局、启动网络以及加载许多其他驱动模块。`rcS` 脚本通过调用许多其他脚本并读取位于 `/etc/rc.d` 目录中的配置文件来执行这些初始化任务。

执行完 `/etc/init.d/rcS` 脚本后，`init` 进程运行带有运行级别作为参数的 `/etc/init.d/rc` 运行级别脚本。例如，对于运行级别 2，`/etc/inittab` 中的以下行指定了 `init` 执行的内容：

```
l2:2:wait:/etc/init.d/rc 2
```

这个例子说明 `init` 执行命令 `/etc/init.d/rc 2` 并等待该命令完成。

`/etc/init.d/rc` 脚本比较复杂。其工作原理如下：

- 它执行与运行级别对应的目录中的脚本。例如，对于运行级别 2，`/etc/init.d/rc` 脚本运行 `/etc/rc2.d` 目录中的脚本。
- 在与运行级别对应的目录中，`/etc/init.d/rc` 查找所有以 K 开头的文件，并使用 stop 参数执行它们。该参数会终止任何正在运行的进程。然后它定位所有以 S 开头的文件，并使用 start 参数执行每个文件。该参数会启动指定运行级别所需的进程。

要在运行级别 2 下查看其执行情况，请输入以下命令：

```bash
ls -l /etc/rc2.d
```

在生成的列表中，k 脚本——文件名以 K 开头的文件——用于停止（或终止）服务器，而 s 脚本用于启动服务器。`/etc/init.d/rc` 脚本会严格按照目录列表中显示的文件顺序执行这些文件。

## 手动启动和停止服务器

在 Linux 中，服务器启动脚本位于 `/etc/init.d` 目录中。你可以手动调用此目录中的脚本来启动、停止或重启特定进程——通常是服务器。例如，若要停止 FTP 服务器（服务器程序名为 vsftpd），请输入以下命令：

```bash
/etc/init.d/vsftpd stop
```

如果 vsftpd 已经在运行，且你希望重启它，请输入以下命令：

```bash
/etc/init.d/vsftpd restart
```

你可以通过熟悉 `/etc/init.d` 目录中的脚本来增强系统管理技能。要查看该目录的列表，请输入以下命令：

```bash
ls /etc/init.d
```

脚本名称可以为你提供一些线索，告诉你该脚本可以启动和停止哪个服务器。例如，samba 脚本用于启动和停止 Samba Windows 网络服务所需的进程。在闲暇时，你可能需要研究其中一些脚本，看看每个脚本的作用。你不需要理解所有的 shell 编程；注释可以帮助你了解每个脚本的用途。

## 在系统启动时自动启动服务器

你希望某些服务器在每次启动系统时都能自动运行。配置服务器的具体命令因发行版而异。

![](img/792720823146d68f19fd50c99ebfce4b_414_0.png)

在 Fedora Core 和 SUSE 中，使用 `chkconfig` 命令设置服务器，以便每当系统启动到特定运行级别时都能启动该服务器。例如，如果你启动了 SSH 服务器，你希望 `sshd` 服务器在系统启动时也能启动。你可以通过使用 `chkconfig` 命令来实现这一点。

若要设置 `sshd` 在系统启动到运行级别 3、4 或 5 时自动运行，请输入以下命令（需以 `root` 身份登录）：

```bash
chkconfig --level 345 sshd on
```

在 Fedora Core 和 SUSE 中，你还可以使用 `chkconfig` 命令来检查哪些服务器已开启或关闭。例如，若要查看所有运行级别的完整服务器列表，请输入以下命令：

```bash
chkconfig --list
```

在 Debian、MEPIS、Ubuntu 和 Xandros 中，你可以使用 `update-rc.d` 命令使服务器在系统启动时自动运行。例如，若要设置 `sshd` 在默认运行级别自动启动，请在以 `root` 身份登录时，在终端窗口中输入 `update-rc.d sshd defaults`。你还可以指定确切的运行级别和序列号（每个服务器启动的顺序）。要了解有关 `update-rc.d` 命令的更多信息，请在终端窗口中输入 `man update-rc.d`。

## 清点 Linux 系统配置文件

Linux 包含大量配置文件。所有这些文件都是你可以用任何文本编辑器编辑的文本文件。要编辑这些配置文件，必须以 `root` 身份登录。我并未单独讨论这些文件，但我在表 1-9 中展示了一部分配置文件，并对每个文件作了简要描述。这份列表可以让你了解系统管理员需要处理的配置文件类型。在许多情况下，Linux 包含图形界面实用程序来设置这些配置文件中的许多内容。

**表 1-9 部分 Linux 配置文件**

| 配置文件 | 描述 |
| :--- | :--- |
| `/boot/grub` | GRUB 引导加载程序文件的位置 |
| `/boot/grub/menu.lst` | GRUB 在启动系统之前显示的引导菜单的配置文件 |



| `/boot/System.map` | Linux 内核映射（将内核地址映射为函数和变量的名称） |
| `/boot/vmlinuz` | Linux 内核（操作系统的核心） |
| `/etc/apache2/htpd.conf` | Apache Web 服务器的配置文件（Debian 和 MEPIS） |
| `/etc/apt/sources.list` | 列出高级打包工具 (APT) 获取软件包来源的配置文件——FTP 或网站或 CD-ROM——（Debian、MEPIS、Ubuntu 和 Xandros） |
| `/etc/at.allow` | 允许使用 `at` 命令安排稍后执行作业的用户名 |
| `/etc/at.deny` | 禁止使用 `at` 命令的用户名 |
| `/etc/bashrc` | `bash` shell 的系统级函数和别名（Fedora Core） |
| `/etc/bash.bashrc` | `bash` shell 的系统级函数和别名（Debian、MEPIS、SUSE、Ubuntu 和 Xandros） |
| `/etc/cups/cupsd.conf` | 通用 UNIX 打印系统 (CUPS) 调度程序的打印机配置文件 |
| `/etc/fonts` | 包含字体配置文件的目录。（特别是，你可以将本地字体配置设置放在 `/etc/fonts/local.conf` 文件中。） |
| `/etc/fstab` | 可用于挂载的文件系统信息以及每个文件系统的挂载位置 |
| `/etc/group` | 组信息 |
| `/etc/grub.conf` | Fedora Core 和 SUSE 中 GRUB 引导加载程序的配置 |
| `/etc/hosts` | IP 地址及其对应主机名的列表 |
| `/etc/hosts.allow` | 允许访问此系统互联网服务的主机 |
| `/etc/hosts.deny` | 禁止访问此系统互联网服务的主机 |
| `/etc/httpd/conf/httpd.conf` | Apache Web 服务器的配置文件（Fedora Core） |
| `/etc/init.d` | 包含用于启动和停止各种服务器的脚本的目录 |
| `/etc/inittab` | 用于启动所有其他进程的 `init` 进程使用的配置文件 |
| `/etc/issue` | 包含在显示文本模式登录提示之前打印的消息的文件（通常是发行版名称和版本号） |
| `/etc/lilo.conf` | Linux Loader (LILO) 的配置——可从磁盘加载操作系统之一的引导加载程序（仅在使用 LILO 引导加载程序时存在） |
| `/etc/login.defs` | 创建用户账户的默认信息，由 `useradd` 命令使用 |
| `/etc/modprobe.conf` | 可加载内核模块的配置文件，由 `modprobe` 命令使用（Fedora Core 和 SUSE） |
| `/etc/modules.conf` | 可加载模块的配置文件（Debian、MEPIS 和 Xandros） |
| `/etc/mtab` | 当前已挂载文件系统的相关信息 |
| `/etc/passwd` | 所有用户账户的信息。（实际密码存储在 `/etc/shadow` 中。） |
| `/etc/profile` | `bash` shell 的系统级环境和启动文件 |
| `/etc/profile.d` | 包含 `/etc/profile` 脚本执行的脚本文件（以 `.sh` 结尾）的目录 |
| `/etc/init.d/rcS` | Debian、MEPIS、SUSE、Ubuntu 和 Xandros 中的 Linux 初始化脚本 |
| `/etc/rc.d/rc.sysinit` | Fedora Core 中的 Linux 初始化脚本 |
| `/etc/shadow` | 包含所有用户账户加密密码的安全文件（仅 `root` 可读） |
| `/etc/shells` | 用户可在系统上使用的所有 shell 的列表 |
| `/etc/skel` | 存储 `.bash_profile` 等文件初始版本的目录，这些文件会被复制到新用户的主目录中 |
| `/etc/sysconfig` | Linux 配置文件（Fedora Core 和 SUSE） |
| `/etc/sysctl.conf` | 包含在系统启动时由 `sysctl` 读取并设置的内核参数的配置文件 |
| `/etc/termcap` | 终端功能与选项的数据库（Fedora Core 和 SUSE） |
| `/etc/udev` | 包含 `udev` 配置文件的目录——`udev` 是提供动态命名热插拔设备并在 `/dev` 目录中创建设备文件能力的程序 |
| `/etc/X11` | 包含 X 窗口系统 (X11) 以及各种显示管理器（如 `gdm` 和 `xdm`）配置文件的目录 |
| `/etc/X11/XF86Config` 或 `/etc/X11/XF86Config-4` | XFree86 X11 的配置文件（Debian、MEPIS 和 Xandros） |
| `/etc/X11/xorg.xof` | X.org X11——X 窗口系统的配置文件（Fedora Core、Ubuntu 和 SUSE） |
| `/etc/xinetd.conf` | `xinetd` 守护程序的配置，该程序按需启动多个互联网服务 |
| `/etc/yum.conf` | `yum` 软件包更新和安装程序的配置（Fedora Core） |
| `/var/log/apache2` | Web 服务器访问和错误日志（Debian 和 MEPIS） |
| `/var/log/cron` | 包含来自运行计划作业的 `cron` 进程消息的日志文件 |
| `/var/log/boot.msg` | 包含启动消息的文件（SUSE） |
| `/var/log/dmesg` | 包含启动消息的文件（Debian、Fedora Core、MEPIS、Ubuntu 和 Xandros） |
| `/var/log/httpd` | Web 服务器访问和错误日志（Fedora Core） |
| `/var/log/messages` | 系统日志 |

# 监控系统性能

作为系统管理员，您必须密切关注 Linux 系统的运行状况。您可以通过查看以下信息来监控系统的整体性能：

- 中央处理器（CPU）使用率
- 物理内存使用量
- 虚拟内存（交换空间）使用量
- 硬盘使用量

Linux 附带了许多实用工具，您可以使用它们来监控一个或多个这些性能参数。在这里，我将介绍其中一些实用工具，并展示如何理解这些工具所呈现的信息。

## 使用 `top` 实用工具

若要查看占用 CPU 时间最多的前几个进程（即 CPU 使用率最高的进程），您可以使用文本模式的 `top` 实用工具。要在终端窗口（或文本控制台）中启动该实用工具，请输入 `top`。随后，`top` 实用工具会显示一个文本屏幕，其中列出了当前进程，并按照 CPU 使用率排序，同时包含其他各种信息，例如内存和交换空间使用情况。图 1-6 展示了 `top` 实用工具的一个典型输出示例。

`top` 实用工具每五秒刷新一次显示。如果您在窗口中让 `top` 持续运行，您可以持续监控 Linux 系统的状态。若要退出 `top`，请按下 Q 或 Ctrl+C，或者关闭终端窗口。

![](img/792720823146d68f19fd50c99ebfce4b_418_0.png)

输出屏幕的前五行（参见图 1-6）提供了系统的摘要信息。以下是这五行显示的内容：

- 第一行显示当前时间、系统已运行的时长、登录用户的数量，以及三个**负载平均值**——过去 1、5 和 15 分钟内就绪等待运行的平均进程数。
- 第二行列出进程的总数以及这些进程的状态。
- 第三行显示 CPU 使用情况——用户进程占用的 CPU 时间百分比、系统（内核）进程占用的百分比，以及 CPU 空闲的时间百分比。
- 第四行显示物理内存的使用情况——总量、已使用量、可用量，以及分配给缓冲区（例如用于从硬盘读取数据）的量。
- 第五行显示虚拟内存（或交换空间）的使用情况——交换空间总量、已使用量、可用量，以及正在被缓存的量。

摘要信息下方出现的表格（参见图 1-6）列出了当前进程的信息，并按 CPU 时间使用量降序排列。表 1-10 总结了 `top` 显示表格中各列标题的含义。

**表 1-10** `top` 实用工具输出中列标题的含义

| 标题 | 含义 |
| :--- | :--- |
| PID | 进程 ID |
| USER | 进程运行所基于的用户名 |
| PR | 进程的优先级 |



| NI | 进程的 Nice 值——取值范围从 -20（最高优先级）到 19（最低优先级），默认值为 0。（Nice 值表示进程的相对优先级：值越高，优先级越低，进程越“温和”——因为它会让位于其他进程。） |
| VIRT | 进程使用的虚拟内存总量，单位为千字节 |
| RES | 任务使用的物理内存总量（通常以千字节显示，但带有 m 后缀表示兆字节） |
| SHR | 进程使用的共享内存量 |
| S | 进程状态（`S` 表示睡眠，`D` 表示不可中断睡眠，`R` 表示运行中，`Z` 表示僵尸进程——应该已终止但仍存在的进程——或 `T` 表示已停止） |
| %CPU | 自上次屏幕更新以来使用的 CPU 时间百分比 |
| %MEM | 进程使用的物理内存百分比 |
| TIME+ | 进程启动以来使用的总 CPU 时间 |
| COMMAND | 启动该进程的命令的简写形式 |

### 使用 uptime 命令

您可以使用 `uptime` 命令获取系统状态的摘要。

只需按如下方式输入命令：

```bash
uptime
```

它会显示类似以下内容的输出：

`15:03:21 up 32 days, 57 min, 3 users, load average: 0.13, 0.23, 0.27`

此输出显示当前时间、系统已运行的时长、用户数量，以及（最后）三个负载平均值——过去 1、5 和 15 分钟内就绪等待运行的平均进程数。负载平均值大于 1 意味着许多进程正在同时竞争 CPU 时间。

负载平均值可以让您了解系统的繁忙程度。

### 使用 vmstat 实用工具

您可以使用 `vmstat` 实用工具获取关于整体系统使用情况的摘要信息。要查看以 5 秒为间隔平均计算的系统使用信息，请输入以下命令（第二个参数指示 `vmstat` 显示输出的总行数）：

```bash
vmstat 5 8
```

您会看到类似以下列表的输出：

| procs | r | b | swpd | free | buff | cache | si | so | bi | bo | in | cs | us | sy | id | wa |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | 0 | 31324 | 4016 | 18568 | 136004 | 1 | 1 | 17 | 16 | 8 | 110 | 33 | 4 | 61 | 1 |  |
| 0 | 0 | 31324 | 2520 | 15348 | 136962 | 0 | 0 | 7799 | 199 | 1157 | 377 | 8 | 8 | 6 | 78 |  |
| 1 | 0 | 31324 | 1584 | 12936 | 141480 | 0 | 19 | 5784 | 105 | 1099 | 437 | 12 | 5 | 0 | 82 |  |
| 2 | 0 | 31324 | 1928 | 13004 | 137136 | 7 | 0 | 1586 | 138 | 1104 | 561 | 43 | 6 | 0 | 51 |  |
| 3 | 1 | 31324 | 1484 | 13348 | 132064 | 0 | 0 | 2620 | 51 | 1080 | 427 | 50 | 5 | 0 | 46 |  |
| 0 | 0 | 31324 | 1804 | 13240 | 127976 | 0 | 0 | 1126 | 46 | 1082 | 782 | 19 | 5 | 47 | 30 |  |
| 0 | 0 | 31324 | 1900 | 13240 | 127976 | 0 | 0 | 0 | 10 | 1010 | 211 | 3 | 1 | 95 | 0 |  |
| 0 | 0 | 31324 | 1916 | 13248 | 127976 | 0 | 0 | 0 | 10 | 1015 | 224 | 3 | 2 | 95 | 0 |  |

输出的第一行显示了自上次重启以来的平均值。此后，`vmstat` 再显示七次 5 秒平均数据，涵盖接下来的 35 秒。表格输出分为六类信息，由输出第一行中的字段指示。第二行展示了这六个主要字段的详细情况。您可以利用表 1-11 来解释这些字段。

**表 1-11** vmstat 实用工具输出中字段的意义

| 字段名称 | 描述 |
| :--- | :--- |
| **procs** | 进程数量及其类型：r = 等待运行的进程，b = 处于不可中断睡眠的进程，w = 已交换出但准备运行的进程 |
| **memory** | 关于物理内存和交换空间使用的信息（所有数字单位为千字节）：swpd = 已使用的虚拟内存，free = 空闲物理内存，buff = 用作缓冲区的内存，cache = 已缓存的虚拟内存 |
| **swap** | 交换量（数字单位为千字节/秒）：si = 从磁盘交换入的内存量，so = 交换到磁盘的内存量 |
| **io** | 关于输入和输出的信息。（数字单位为块/秒，块大小取决于磁盘设备。）bi = 发送到磁盘的块速率，bo = 从磁盘接收的块速率 |
| **system** | 关于系统的信息：in = 每秒中断次数（包括时钟中断），cs = 每秒上下文切换次数——内核更改正在运行的进程的次数 |
| **cpu** | 使用的 CPU 时间百分比：us = 用户进程使用的 CPU 时间百分比，sy = 系统进程使用的 CPU 时间百分比，id = CPU 空闲时间百分比，wa = 等待输入/输出（I/O）的时间 |

![](img/792720823146d68f19fd50c99ebfce4b_421_0.png)

在 `vmstat` 实用工具的输出中，`si` 和 `so` 字段中的高值表明交换过多。（交换指的是在物理内存和硬盘上的虚拟内存之间复制信息。）`bi` 和 `bo` 字段中的高数字表明磁盘活动过多。

### 检查磁盘性能和磁盘使用情况

Linux 附带了 `/sbin/hdparm` 程序，您可以使用它来控制大多数 PC 上常见的 IDE 或 ATAPI 硬盘。`hdparm` 程序的一个功能是使用 `-t` 选项来确定数据从磁盘读取到内存缓冲区中的速率。例如，以下是我在我的系统上输入 `/sbin/hdparm -t /dev/hda` 的结果：

```bash
/dev/hda:  Timing buffered disk reads: 178 MB in  3.03 seconds = 58.81 MB/sec
```

该命令需要 IDE 驱动的设备名称（第一个硬盘为 `/dev/hda`，第二个硬盘为 `/dev/hdb`）作为参数。如果你拥有 IDE 硬盘，可以试用此命令来查看从系统磁盘驱动器读取数据的速度有多快。

若要显示当前挂载文件系统的可用空间，请使用 `df` 命令。如果你希望 `df` 的输出更具可读性，请输入以下命令：

```
df -h
```

这是该命令的典型输出：

```
Filesystem    Size  Used Avail Use% Mounted on
/dev/hda5 7.1G 3.9G 2.9G 59% /
/dev/hda3 99M 18M 77M 19% /boot
none 125M 0 125M 0% /dev/shm
/dev/scd0 2.6G 2.6G 0 100% /media/cdrecorder
```

如本例所示，`-h` 选项会使 `df` 命令以 GB（G）和 MB（M）为单位显示大小。

若要检查特定目录使用的磁盘空间，请使用 `du` 命令 —— 你可以指定 `-h` 选项，以便以 KB（K）和 MB（M）为单位查看输出，如下例所示：

```
du -h /var/log
```

以下是该命令的典型输出：

```
152K /var/log/cups
4.0K /var/log/vbox
4.0K /var/log/htpd
508K /var/log/gdm
4.0K /var/log/samba
8.0K /var/log/mail
4.0K /var/log/news/OLD
8.0K /var/log/news
4.0K /var/log/squid
2.2M /var/log
```

`du` 命令显示每个目录使用的磁盘空间，最后一行显示该目录使用的总磁盘空间。如果你想仅查看目录使用的总空间，请使用 `-s` 选项。例如，输入 `du -sh /home` 来查看 `/home` 目录使用的空间。该命令产生的输出如下所示：

```
89M /home
```

## 通过 /proc 文件系统查看系统信息

你的 Linux 系统有一个称为 `/proc` 文件系统的特殊文件系统。你可以从该文件系统中了解关于系统的许多信息。事实上，你甚至可以通过 `/proc` 文件系统更改内核参数（只需向该文件系统中的一个文件写入内容即可），从而修改系统的行为。



# /proc 文件系统

`/proc` 文件系统并不是硬盘上的真实目录，而是一组由 Linux 内核管理的内存数据结构，它们对你表现为一系列目录和文件。`/proc`（也称为进程文件系统）的目的是让你能够访问关于 Linux 内核的信息，并帮助你了解当前系统中正在运行的所有进程。

你可以像访问其他目录一样访问 `/proc` 文件系统，但你必须了解各种文件的含义才能解释这些信息。通常，你可以使用 `cat` 或 `more` 命令查看 `/proc` 中文件的内容。文件的内容提供了关于系统某方面的信息。

与任何目录一样，首先查看 `/proc` 的详细目录列表。为此，请以 root 身份登录并在终端窗口中输入 `ls -l /proc`。在输出中，第一组目录（以行首的字母 r 表示）代表当前在系统上运行的进程。每个对应进程的目录使用进程 ID（一个数字）作为其名称。

![](img/792720823146d68f19fd50c99ebfce4b_423_0.png)

还要注意一个名为 `/proc/kcore` 的巨大文件；该文件代表你系统的整个物理内存。尽管 `/proc/kcore` 在列表中出现为一个巨大文件，但单个物理文件并不会在硬盘上占用那么多空间 —— 因此不要尝试删除该文件以回收磁盘空间。

`/proc` 中的几个文件和目录包含关于你的 Linux 电脑的有趣信息。例如，`/proc/cpuinfo` 文件列出了系统的关键特征，如处理器类型和浮点处理器信息。你可以通过输入 `cat /proc/cpuinfo` 来查看处理器信息。例如，以下是我在我的系统上输入 `cat /proc/cpuinfo` 得到的结果：

```
processor     : 0
vendor_id     : GenuineIntel
cpu family    : 15
model         : 3
model name    : Intel(R) Celeron(R) CPU 2.53GHz
stepping      : 3
cpu MHz       : 2533.129
cache size    : 256 KB
fdiv_bug      : no
hlt_bug       : no
f00f_bug      : no
coma_bug      : no
fpu           : yes
fpu_exception : yes
cpuid level   : 5
wp            : yes
flags         : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe pmi monitor ds_cpl cid
bogomips      : 4997.12
```

此输出来自一个 2.5 GHz Celeron 系统。列表显示了处理器的许多有趣特征。请注意以 `fdiv_bug` 开头的那一行。还记得臭名昭著的 Pentium 浮点除法错误吗？该错误存在于一条名为 `fdiv` 的指令中（用于*浮点除法*）。因此，`fdiv_bug` 行指示该特定的 Pentium 是否存在此错误。（幸运的是，我的 PC 处理器没有这个问题。）

`/proc/cpuinfo` 文件的最后一行显示了处理器在 Linux 内核启动时计算出的 `BogoMIPS`。`BogoMIPS` 是 Linux 内部用于计时延迟循环的东西。

表 1-12 总结了 `/proc` 文件中提供一些关于你 Linux 系统信息的文件。你可以查看系统上的这些文件以了解它们包含的内容，但请注意，表 1-12 中显示的所有文件并不一定都存在于你的系统中。`/proc` 文件系统的具体内容取决于内核配置和已加载的驱动程序模块（这反过来又取决于你的 PC 硬件配置）。

- **提示**：你可以像操作 Linux 中的其他目录和文件一样导航 `/proc` 文件系统。使用 `more` 或 `cat` 命令查看文件的内容。

## 表 1-12 /proc 中的一些文件和目录

| 文件名 | 内容 |
| :--- | :--- |
| `/proc/acpi` | 关于高级配置和功率接口 (ACPI) 的信息 —— 一种用于笔记本电脑、桌面计算机和服务器配置和电源管理的行业标准接口 |
| `/proc/bus` | 包含每种总线类型（如 PCI）特定总线信息的目录 |
| `/proc/cmdline` | 用于启动 Linux 内核的命令行（例如，ro root=LABEL=/ rhgb） |
| `/proc/cpuinfo` | 关于 CPU（微处理器）的信息 |
| `/proc/devices` | 系统中可用的块设备和字符设备 |
| `/proc/dma` | 关于正在使用的 DMA（直接内存访问）通道的信息 |
| `/proc/driver/rtc` | 关于 PC 实时时钟 (RTC) 的信息 |
| `/proc/filesystems` | 支持的文件系统列表 |
| `/proc/ide` | 包含 IDE 设备信息的目录 |
| `/proc/interrupts` | 关于中断请求 (IRQ) 号及其使用情况的信息 |
| `/proc/ioports` | 关于输入/输出 (I/O) 端口地址及其使用情况的信息 |
| `/proc/kcore` | 物理内存的映像 |
| `/proc/kmsg` | 内核消息 |
| `/proc/loadavg` | **负载平均值**（最近 1、5 和 15 分钟内等待运行的平均进程数） |
| `/proc/locks` | 当前内核锁（用于确保多个进程不会同时写入文件） |
| `/proc/meminfo` | 关于物理内存和交换空间使用情况的信息 |
| `/proc/misc` | 杂项信息 |
| `/proc/modules` | 已加载驱动程序模块列表 |
| `/proc/mounts` | 已挂载文件系统列表 |
| `/proc/net` | 包含许多子目录的目录，其中包含关于网络的信息 |
| `/proc/partitions` | Linux 内核已知的分区列表 |
| `/proc/pci` | 关于在系统上发现的 PCI 设备的信息 |
| `/proc/scsi` | 包含在系统上发现的 SCSI 设备信息的目录（仅当你拥有 SCSI 设备时才存在） |
| `/proc/stat` | 系统的总体统计数据 |
| `/proc/swaps` | 关于交换空间及其使用量的信息 |
| `/proc/sys` | 包含系统信息的目录。你可以通过向该目录中的文件写入来更改内核参数。（使用此方法调整系统性能需要专业知识才能正确完成。） |
| `/proc/uptime` | 关于系统运行时长的信息 |
| `/proc/version` | 内核版本号 |

# 理解 Linux 设备

Linux 将所有设备视为文件，并使用设备的方式与使用文件的方式相同——打开它、向其写入数据、从中读取数据，并在完成后关闭它。这种将所有设备都当作文件来处理的能力是通过使用设备驱动程序实现的。**设备驱动程序**是一种特殊的程序，用于控制特定类型的硬件。当内核向设备写入数据时，设备驱动程序会执行对该设备而言合适的操作。例如，当内核向软盘驱动器写入数据时，软盘设备驱动程序会将这些数据写入软盘的物理介质上。另一方面，如果内核向并口设备写入数据，并口驱动程序会将数据发送到连接到并口的打印机。

因此，设备驱动程序将设备特定代码与内核的其他部分隔离开来，并使得设备看起来像文件一样。任何应用程序都可以通过打开与该设备特定的文件来访问该设备。图 1-7 说明了 Linux 设备驱动程序的这一概念。

![](img/792720823146d68f19fd50c99ebfce4b_426_0.png)

## 设备文件

如图 1-7 所示，应用程序可以像访问文件一样访问设备。这些文件是被称为*设备文件*的特殊文件，它们出现在 Linux 文件系统中的 `/dev` 目录中。

如果你使用 `ls` 命令查看 `/dev` 目录中的文件列表，你会看到数千个文件。这些文件并不意味着你的系统有数千个设备。`/dev` 目录包含所有可能类型设备的文件——这就是设备文件数量如此之大的原因。

那么，当应用程序打开特定设备文件时，内核如何知道该使用哪个设备驱动程序？答案在于两个称为*主设备号*和*次设备号*的数字。每个设备文件都通过这些数字映射到特定的设备驱动程序。

要查看主设备号和次设备号的示例，请在终端窗口中输入以下命令：

```bash
ls -l /dev/hda
```

你会看到类似以下的一行输出：

```text
brw-rw---- 1 root disk 3, 0 Aug 16 14:50 /dev/hda
```

在这行中，主设备号和次设备号出现在日期之前。在这种情况下，主设备号为 3，次设备号为 0。内核通过主设备号来选择该设备文件的设备驱动程序。

你实际上不需要过多地了解设备文件和设备号，除了意识到它们的存在即可。

![](img/792720823146d68f19fd50c99ebfce4b_427_0.png)



如果你感到好奇，所有设备的主设备号和次设备号都是根据设备类型分配的。*Linux 指定名称和数字授权机构 (LANANA)* 负责分配这些数字。你可以在 `www.lanana.org/docs/device-list/devices.txt` 上查看当前的设备列表。

### 块设备

设备文件列表中的首字母也提供了重要线索。对于 `/dev/hda` 设备，首字母是 `b`，这表明 `/dev/hda` 是一个*块设备*——它可以按块（通常为 512 字节或 1K）接受或提供数据。顺便说一下，`/dev/hda` 指的是你系统上的第一个 IDE 硬盘（在 Windows 中为 C: 盘）。硬盘、软盘驱动器和 CD-ROM 驱动器都是块设备的例子。

### 字符设备

如果设备文件列表中的首字母是 `c`，那么该设备是一个*字符设备*——它可以一次接收和发送一个字符（一个字节）。例如，串行端口和并行端口都是字符设备。

要查看字符设备的具体列表，请在终端窗口中输入以下命令：

```text
ls -1 /dev/ttyS0
```

该设备的列表类似以下所示：

```text
crw-rw----  1 root  uucp    4, 64 Aug 16 14:50 /dev/ttyS0
```

注意，第一个字符是 c，因为 `/dev/ttyS0`——第一个串行端口——是一个字符设备。

### 网络设备

使你的系统能够与网络交互的网络设备——例如以太网和拨号*点对点协议* (PPP) 连接——有些特殊，因为它们不需要对应的设备文件。相反，内核使用特殊名称来命名设备。例如，以太网设备被命名为 `eth0`（第一个以太网卡）、`eth1`（第二个以太网卡）等。PPP 连接被命名为 `ppp0`、`ppp1` 等。

由于网络设备不映射到设备文件，因此 `/dev` 目录中不存在对应这些设备的文件。

### 使用 udev 实现持久设备命名

Linux 内核 2.6 引入了一种基于以下特性的处理设备的新方法：

- `sysfs`：内核 2.6 提供了挂载在文件系统 `/sys` 目录上的 `sysfs` 文件系统。`sysfs` 文件系统显示系统中所有设备以及每个设备的大量信息。这些信息包括设备在总线上的位置、名称和序列号等属性，以及设备的主次设备号。

- `/sbin/hotplug`：每当设备被添加或移除时，都会调用此程序。然后它可以执行处理该设备所需的一切操作。

- `/sbin/udev`：该程序根据设备特性（如序列号、总线上的设备编号或基于通过文本文件 `/etc/udev/udev.rules` 设置的一组规则的用户指定名称）来动态命名设备。

`udev` 程序的配置文件是 `/etc/udev/udev.conf`。根据该配置文件中的设置，`udev` 自动在 `udev_root` 参数指定的目录中创建设备节点。例如，要管理 `/dev` 目录中的设备节点，应在 `/etc/udev/udev.conf` 中定义 `udev_root` 如下：

```text
udev_root="/dev/"
```

## 管理可加载驱动程序模块

要使用任何设备，Linux 内核必须包含驱动程序。如果驱动程序代码作为单体程序链接到内核中（即形式为单个大文件的程序），添加新驱动程序意味着需要用新的驱动程序代码重新构建内核。重新构建内核意味着在能够使用新的设备驱动程序之前，你不得不使用新内核重启 PC。幸运的是，Linux 内核采用了模块化设计，避免了重启带来的麻烦。Linux 设备驱动程序可以创建为模块形式，内核无需重启 PC 即可加载和卸载这些模块。

> 驱动程序模块是更广泛的软件模块类别——可加载内核模块 (Loadable Kernel Modules) 的一种类型。其他类型的内核模块包括支持新类型文件系统的代码、网络协议模块以及解释不同格式可执行文件的模块。

![](img/792720823146d68f19fd50c99ebfce4b_429_0.png)

### 加载和卸载模块

你可以使用一组命令来管理可加载的设备驱动程序模块。使用其中某些命令需要以 root 身份登录。在表 3-13 中，我总结了一些常用的模块命令。

**表 3-13 管理内核模块的命令**

| 此命令 | 执行以下操作 |

| :--- | :--- |

| `insmod` | 将模块插入内核 |

| `rmmod` | 从内核中移除模块 |

| `depmod` | 确定模块之间的相互依赖关系 |

| `ksyms` | 显示符号列表以及定义该符号的模块名称 |

| `lsmod` | 列出所有当前已加载的模块 |

| `modinfo` | 显示有关内核模块的信息 |

| `modprobe` | 智能地插入或移除一个模块或一组模块。（例如，如果模块 A 需要 B，则当要求加载 A 时，modprobe 会自动加载 B。） |

如果你必须使用其中任何命令，请以 `root` 身份登录，或在终端窗口中输入 `su –` 以变为 `root`。

要查看当前加载的模块，请输入：

```text
lsmod
```

你会看到一个长的模块列表，具体取决于你系统上安装的设备类型。

`lsmod` 显示的列表包含所有类型的 Linux 内核模块，而不仅仅是设备驱动程序。例如，如果你使用 Ext3 文件系统，你通常会找到两个模块——`jbd` 和 `ext3`——它们都是 Ext3 文件系统（Linux 最新的文件系统）的一部分。

![](img/792720823146d68f19fd50c99ebfce4b_430_0.png)

除了 `lsmod`，另一个常用的模块命令是 `modprobe`。每当需要手动加载或移除一个或多个模块时，请使用 `modprobe`。`modprobe` 的最好的地方在于，你不需要担心模块是否需要其他模块才能工作。`modprobe` 命令会自动加载任何模块所需的任何其他模块。例如，在我的其中一个系统上，我使用以下命令手动加载声音驱动程序：

```text
modprobe snd-card-0
```

该命令使 `modprobe` 加载使声音工作所需的一切。

![](img/792720823146d68f19fd50c99ebfce4b_430_1.png)

你可以使用 `-r` 选项配合 `modprobe` 来移除模块。例如，要移除声音模块，我使用以下命令：

```text
modprobe -r snd-card-0
```

该命令清除了 `modprobe snd-card-0` 命令已加载的所有模块。

### 使用 /etc/modprobe.conf 文件

当我使用模块名称 `snd-card-0` 时，`modprobe` 命令如何知道它需要加载 `snd-intel8x0` 驱动程序模块？答案在 `/etc/modprobe.conf` 配置文件中。该文件包含一行内容，告诉 `modprobe` 在看到模块名称 `snd-card-0` 时应加载什么。

要查看 `/etc/modprobe.conf` 的内容，请输入：

```text
cat /etc/modprobe.conf
```

![](img/792720823146d68f19fd50c99ebfce4b_431_0.png)

在我运行 Linux 2.6 的一台 Fedora Core PC 上，`/etc/modprobe.conf` 文件包含以下行：

```
alias eth0 3c59x
alias snd-card-0 snd-intel8x0
alias usb-controller uhci-hcd
```

每一以关键字 *alias* 开头的行都为实际的驱动程序模块定义了一个标准名称。例如，第一行将 *3c59x* 定义为别名 *eth0* 的实际驱动程序名称，*eth0* 代表第一块以太网卡。类似地，第三行定义了 *snd-intel8x0* 作为使用名称 *snd-card-0* 时需要加载的模块。

*modprobe* 命令会查阅 `/etc/modprobe.conf` 文件以将别名转换为驱动程序模块的真实名称。它也会查阅 `/etc/modprobe.conf` 文件以执行其他任务，例如获取驱动程序模块的参数。例如，你可以插入以 *options* 关键字开头的行来提供驱动程序可能需要的参数值。

例如，要将以太网驱动程序的调试级别参数设置为 5（此参数会在 `/var/log/messages` 中生成大量信息），我在 `/etc/modprobe.conf` 文件中添加了以下行：

```
options 3c59x debug=5
```

这一行指定在 *3c59x* 模块中，名为 *debug* 的参数的值为 5。

如果你想知道某个模块接受哪些参数名称，请使用 *modinfo* 命令。例如，要查看关于 *3c59x* 驱动程序模块的信息，我输入：

```
modinfo 3c59x | more
```

从生成的输出中，我可以知道 *debug* 是用于设置调试级别的参数名称。



不幸的是，`modinfo`命令显示的信息可能比较晦涩。唯一的好消息是你可能不需要做太多额外的事情，只需使用图形工具来配置设备，该工具会自动处理向配置文件（如`/etc/modprobe.conf`）添加所需内容的工作。

## 在 Linux 中安排任务

作为系统管理员，你可能需要定期自动运行某些程序，或在未来的指定时间执行一个或多个命令。你的 Linux 系统包含了调度任务在未来任何日期或时间运行的设施。你还可以设置系统定期执行任务或仅执行一次。以下是你可以通过在 Linux 系统上调度任务执行的一些典型任务：

- 在深夜备份文件。
- 在清晨系统不繁忙时下载大文件。
- 发送自我提醒会议的消息。
- 定期分析系统日志并查找任何异常活动。

你可以使用 Linux 的 `at` 命令或 `crontab` 设施来设置这些任务。在接下来的几个部分中，我将介绍这些 Linux 任务调度功能。

### 安排一次性任务

如果你想在稍后的时间运行一个或多个命令，可以使用 `at` 命令。`atd` 守护进程——一个用于处理使用 `at` 提交的任务的程序——会在指定时间运行你的命令，并将输出通过邮件发送给你。

![](img/792720823146d68f19fd50c99ebfce4b_432_0.png)

在你尝试 `at` 命令之前，你需要知道以下配置文件控制了哪些用户可以使用 `at` 命令调度任务：

- `/etc/at.allow` 包含可以使用 `at` 命令提交任务的用户名称。
- `/etc/at.deny` 包含不允许使用 `at` 命令提交任务的用户名称。

如果这些文件不存在，或者你发现 `/etc/at.deny` 文件为空，则任何用户都可以使用 `at` 命令提交任务。Linux 的默认设置是空的 `/etc/at.deny` 文件；在此默认设置下，任何人都可以使用 `at` 命令。如果你不想让某些用户使用 `at`，只需将他们的用户名列在 `/etc/at.deny` 文件中。

使用 `at` 安排稍后执行的一次性任务，请遵循以下步骤：

1. 在你想执行命令的日期或时间运行 `at` 命令。

按下回车后，会出现 `at>` 提示符，如下所示：

```
at  21:30
at>
```

这是指示执行命令时间的最简单方法——只需以 24 小时制指定时间。在此情况下，你想在今晚 9:30 PM（如果已经过了 9:30 PM，则为明天）执行命令。不过，你可以用许多不同的方式指定执行时间。（参见表 1-14 获取示例。）

2. 在 `at>` 提示符处，像在 shell 提示符处输入一样输入你想执行的命令。每个命令后按回车，然后继续输入下一个命令。输入完你想执行的命令后，按 Ctrl-D 表示结束。

下面是一个示例，展示了如何在未来时间执行 `ps` 命令：

```
at> ps
at> <EOT>
job 1 at 2006-12-28 21:30
```

按下 Ctrl-D 后，`at` 命令会回复一个任务编号以及任务执行的日期和时间。

表 1-14 `at` 命令执行时间的格式

| 命令 | 任务运行时间 |
| :--- | :--- |
| at now | 立即 |
| at now + 15 minutes | 从当前时间起 15 分钟 |
| at now + 4 hours | 从当前时间起 4 小时 |
| at now + 7 days | 从当前时间起 7 天 |
| at noon | 今天中午（如果已过了中午，则为明天） |
| at now next hour | 从现在起正好 60 分钟 |
| at now next day | 明天同一时间 |
| at 17:00 tomorrow | 明天下午 5 点 |
| at 4:45pm | 今天下午 4:45（如果已过了 4:45 PM，则为明天） |
| at 3:00 Dec 28, 2006 | 2006 年 12 月 28 日上午 3:00 |

输入一个或多个任务后，你可以使用 `atq` 命令查看当前已调度的任务列表：

```
atq
```

输出类似于以下内容：

```
4        2006-12-28 03:00 a root
5        2006-10-26 21:57 a root
6        2007-10-26 16:45 a root
```

每行的第一个字段显示任务编号——与你提交任务时 `at` 命令显示的编号相同。下一个字段显示执行的年、月、日和小时。最后一个字段显示在名为 `a` 的队列中等待的任务。

如果你想取消一个任务，使用 `atrm` 命令将该任务从队列中移除。使用 `atrm` 命令移除任务时，请通过任务编号引用该任务，如下所示：

```
atrm 4
```

此命令删除了计划于 2006 年 12 月 28 日凌晨 3:00 执行的任务 4。

当任务执行时，输出会通过邮件发送给你。在终端窗口中输入 `mail` 以阅读你的邮件并查看任务的输出。

### 安排重复任务

虽然 `at` 适合在特定时间运行命令，但它对于自动在重复间隔运行程序并无用处。你必须使用 `crontab` 来调度此类重复任务——例如，如果你想每天晚上午夜将文件备份到磁带。

通过将任务信息放入具有特定格式的文件，并使用 `crontab` 命令提交该文件来安排重复任务。`cron` 守护进程——`crond`——每分钟检查任务信息，并在指定时间执行重复任务。由于 `cron` 守护进程处理重复任务，因此这些任务也被称为 *cron jobs*。

*cron* 任务的任何输出都会通过邮件发送给提交任务的用户。（在提交的任务信息文件中，你可以指定不同的收件人来接收邮件输出。）

两个配置文件控制了谁可以使用 `crontab` 调度 *cron* 任务：

- `/etc/cron.allow` 包含可以使用 `crontab` 命令提交任务的用户名称。
- `/etc/cron.deny` 包含不允许使用 `crontab` 命令提交任务的用户名称。

如果 `/etc/cron.allow` 文件存在，只有列在该文件中的用户才能调度 `cron` 任务。如果只有 `/etc/cron.deny` 文件存在，则列在该文件中的用户不能调度 `cron` 任务。如果两个文件都不存在，默认的 Linux 设置允许任何用户提交 `cron` 任务。

提交 `cron` 任务，请遵循以下步骤：

1. 准备一个 shell 脚本（或任何编程语言的可执行程序），用于执行你想执行的重复任务。

   如果你想定期执行现有程序，可以跳过此步骤。

2. 准备一个包含你想在何时执行 shell 脚本或程序（来自步骤 1）的信息的文本文件，然后使用 `crontab` 提交此文件。

   你可以使用单个文件提交多个重复任务。每行包含任务时间信息的行都有标准格式，包含六个字段——前五个指定任务运行的时间，第六个及后续字段构成实际运行的命令。例如，这里有一行在每天午夜零五分执行用户主目录中的 `myjob` shell 脚本：

   `$ 5 0 * * * $HOME/myjob`

   表 1-15 展示了前五个字段的意思。**注意：** 星号 (`*`) 表示该字段的所有可能值。此外，前五个字段中的任何条目可以是单个数字、逗号分隔的数字列表、由连字符分隔的数字对（表示数字范围）或星号。

3. 假设文本文件 `jobinfo`（在当前目录中）包含任务信息。使用以下命令将此信息提交给 `crontab`：

   ```
   $ crontab jobinfo
   ```

   就这样！你已经设置好了 `cron` 任务。从现在起，`cron` 任务将按照间隔运行（如任务信息文件中指定），并接收包含任务输出的邮件消息。

   要验证任务确实已调度，请输入以下命令：

   ```
   $ crontab -l
   ```

   `crontab -l` 命令的输出显示以你名义当前安装的 `cron` 任务。要删除你的 `cron` 任务，请输入 `crontab -r`。

## 表 1-15 `crontab` 文件中执行时间的格式

| 字段编号 | 字段含义 | 允许的值范围* |
| :--- | :--- | :--- |
| 1 | 分钟 | 0–59 |
| 2 | 一天中的小时 | 0–23 |
| 3 | 月中的日期 | 0–31 |
| 4 | 月份 | 1–12（1 代表一月，2 代表二月，等等）或使用月份名称的前三个字母 — Jan、Feb、Mar、Apr、May、Jun、Jul、Aug、Sep、Oct、Nov、Dec |
| 5 | 星期几 | 0–6（0 代表周日，1 代表周一，等等）或使用星期名称的三字母缩写 — Sun、Mon、Tue、Wed、Thu、Fri、Sat |

* 字段中的星号表示该字段的所有可能值。例如，如果第三个字段是星号，则该任务每天执行。

如果你以 `root` 身份登录，你还可以为任何用户设置、检查和删除 `cron` 任务。要为某个用户设置 `cron` 任务，请使用以下命令：

```
crontab -u username filename
```



在此，`username` 是你要为其安装 cron 任务的用户，`filename` 是包含任务信息的文件。

使用以下 `crontab` 命令形式来查看某用户的 cron 任务：

```
crontab -u username -l
```

要删除某用户的 cron 任务，请使用以下命令：

```
crontab -u username -r
```

注意：cron 守护进程也会执行系统范围 cron 任务文件 `/etc/crontab` 中列出的 cron 任务。以下是 Linux 系统中典型的 `/etc/crontab` 文件（输入 `cat /etc/crontab` 查看文件）：

```
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

前四行为此文件中列出的任务设置了一些环境变量。`MAILTO` 环境变量指定了接收此文件中 cron 任务输出的邮件消息的用户。

以 `#` 开头的行是注释行。`run-parts` 注释后的四行在特定时间执行 `run-parts` shell 脚本（位于 `/usr/bin` 目录中），并以特定目录的名称作为参数。`run-parts` 的每个参数 — `/etc/cron.hourly`、`/etc/cron.daily`、`/etc/cron.weekly` 和 `/etc/cron.monthly` — 都是目录。本质上，`run-parts` 会执行你提供的目录中所有脚本。

## 表 1-16 cron 任务的脚本目录

| 目录名称 | 内容 |
| --- | --- |
| `/etc/cron.hourly` | 每小时执行的脚本 |
| `/etc/cron.daily` | 每天执行的脚本 |
| `/etc/cron.weekly` | 每周执行的脚本 |
| `/etc/cron.monthly` | 每月执行一次的脚本 |

# 第 2 章：管理用户和组

*本章内容*

- ✓ 添加用户账户
- ✓ 理解密码文件
- ✓ 管理组
- ✓ 探索用户环境
- ✓ 更改文件和目录的用户及组所有权

Linux 是一个多用户系统，因此有许多用户账户。即使你是系统上唯一的用户，许多服务器也需要唯一的用户名和组名。以 FTP 服务器为例，它在用户名 `ftp` 下运行。大量的系统用户并非供人类使用，而是仅用于运行特定程序。

此外，用户可以属于一个或多个组。通常，每个用户名都有对应的私有组名。默认情况下，每个用户属于该对应的私有组。但是，你可以定义其他组，以便根据组成员身份提供对特定文件和目录的访问权限。

文件和目录的用户及组所有权是确保只有正确的人（或正确的进程）能够访问正确文件和目录的一种方式。管理用户和组账户是典型的系统管理工作。鉴于 Linux 自带的工具，完成这部分工作并不难。本章将向你展示如何操作。

## 添加用户账户

在安装 Linux 后首次启动系统时，你有机会添加用户账户。`root` 账户是安装期间必须设置的唯一账户。如果你在首次启动系统时未添加其他用户账户，之后也可以使用图形用户界面用户账户管理器或 `useradd` 命令在系统上添加新用户。

![](img/792720823146d68f19fd50c99ebfce4b_439_0.png)

创建除了 `root` 以外的其他用户账户是个好主意。即使你是系统上唯一的用户，以特权较低的用户登录也是良好的实践，因为这样可以避免无意中损坏重要的系统文件。如有必要，你可以输入 `su -` 以 `root` 身份登录，然后执行任何系统管理任务。

### 使用图形用户界面用户管理器添加用户账户

大多数 Linux 发行版都自带一个管理用户账户的图形用户界面工具。你可以使用该图形工具添加新用户账户。无论具体的图形工具是什么，基本步骤包括以下内容：

1. 该工具显示当前用户账户列表，并有一个**添加**按钮用于添加新用户。
2. 单击**添加**按钮，会弹出一个对话框，**提示你输入新用户账户的信息**。
3. 输入所需信息 — 用户名、密码（输入两次）以及用户的完整姓名。
4. 单击按钮创建新账户，图形工具会处理添加新用户账户的过程。

![](img/792720823146d68f19fd50c99ebfce4b_439_1.png)

例如，在 SUSE 中，从 YaST 控制中心的左侧选择“Security and Users”类别，然后单击窗口右侧的“User Management”图标。YaST 随后会显示如图 2-1 所示的用户和组管理窗格，你可以在其中定义新用户账户。

![](img/792720823146d68f19fd50c99ebfce4b_439_2.png)

**图 2-1：** 在 SUSE 中，你可以通过 YaST 管理用户账户和组。

注意该窗格有两个单选项：Users（用户）和 Groups（组）（如图 2-1 所示）。选择 Users 单选项会显示来自 `/etc/passwd` 文件的当前用户列表。选择 Groups 单选项会列出来自 `/etc/group` 文件的组名。最初，用户和组管理工具会过滤掉所有系统用户和组。但是，你可以通过单击“Set Filter”并从下拉菜单中选择“System Users”来查看系统用户。（系统用户指的是未分配给人类用户的账户；相反，这些用户账户用于运行各种服务。）

你可以从图 2-1 所示的窗格中添加新的 Users 和 Groups 或编辑现有的 Users 和 Groups。

要添加新用户账户，单击 Add 按钮，并在新建本地用户窗口中输入所需信息，如图 2-2 所示。

![](img/792720823146d68f19fd50c99ebfce4b_440_0.png)

在窗口中填写所需信息（参见图 2-2），然后单击 Accept 按钮。新用户将出现在用户和组管理窗格的用户列表中。

如果你喜欢，可以添加更多用户账户。完成后，单击用户和组管理窗格中的 Finish 按钮（参见图 2-1）以创建新用户账户。

默认情况下，YaST 将所有本地用户放置在一个名为 `users` 的组中。有时你希望用户也属于其他组，以便用户能够访问该组拥有的文件。将用户添加到其他组很容易。例如，假设我想将用户名 `naba` 添加到名为 `wheel` 的组中。我只需在终端窗口中输入以下命令：

`usermod -G wheel naba`

要在 SUSE 中删除用户账户，请单击用户账户列表中的用户名（参见图 2-1）。然后单击**删除**按钮。

## 使用命令管理用户账户

如果你正在文本控制台中工作，可以使用 `useradd` 命令创建新的用户账户。请按照以下步骤为新用户添加账户：

1. **以 root 身份登录。**
   - 如果你尚未以 `root` 身份登录，请输入 `su` - 成为 root。
2. **输入以下带有 `-c` 选项的 `useradd` 命令以创建账户：**
   - `/usr/sbin/useradd -c "Ashley Barkakati" ashley`
3. **使用 `passwd` 命令设置 `password`，如下所示：**
   - `passwd ashley`
   - 系统会提示你两次输入密码。如果你输入的密码容易被猜测，`passwd` 程序会拒绝该密码。

`useradd` 命令会参考以下配置文件，以获取新用户的各种参数的默认信息：

- **`/etc/default/useradd`：** 指定默认 shell (`bin/bash`) 和默认主目录位置 (`home`)
- **`/etc/login.defs`：** 提供自动组 ID 和用户 ID 以及 `password-expiration` 参数的系统范围默认值
- **`/etc/skel`：** 包含 `useradd` 在用户主目录中创建的默认文件

使用 `cat` 或 `more` 命令检查这些文件，以查看其内容。

### 理解 /etc/passwd 文件 417

你可以使用 `userdel` 命令删除用户账户。只需在命令提示符中输入 `/usr/sbin/userdel username` 即可删除用户账户。若要同时清除该用户的家目录，请输入 `/usr/sbin/userdel -r username`。

若要修改用户账户中的任何信息，请使用 `usermod` 命令。例如，如果我希望我的用户名 `naba` 的主组为 `root`，我会输入以下内容：

```
usermod -g root naba
```

若想了解更多关于 `useradd`、`userdel` 和 `usermod` 命令的信息，请在终端窗口中输入 `man useradd`、`man userdel` 或 `man usermod`。



# 理解 `/etc/passwd` 文件

`/etc/passwd` 文件是所有用户账户的列表。它是一个文本文件，任何用户都可以读取它——无需特殊权限。`/etc/passwd` 中的每一行都有七个字段，由冒号（`:`）分隔。
以下是 `/etc/passwd` 文件中一条典型条目：
```
naba:x:500:10:Naba Barkakati:/home/naba:/bin/bash
```
图 2-3 解释了此条目中七个字段的含义。
![](img/792720823146d68f19fd50c99ebfce4b_442_0.png)
如图所示，`/etc/passwd` 中每行的格式如下：
```
username:password:UID:GID:GECOS:homedir:shell
```
表 2-1 解释了每个 `/etc/passwd` 条目中七个字段的含义。

### 表 2-1 `/etc/passwd` 文件中各字段的含义

| 此字段 | 内容 |
| :--- | :--- |
| username | 字母数字用户名，通常长度为 8 个字符且唯一（Linux 允许用户名长于 8 个字符，但某些其他操作系统不允许。） |
| password | 若存在，则为 13 个字符的加密密码。（空字段表示访问该账户不需要密码。x 表示密码存储在 `/etc/shadow` 文件中，安全性更高。） |
| UID | 用作用户标识符的唯一数字。（root 的 UID 为 0，通常 1 到 100 之间的 UID 保留给非人类用户，例如服务器；最好将 UID 保持在 32,767 以下。） |
| GID | 用户所属组的默认组 ID（GID 0 对应 root 组，其他组定义在 `/etc/group` 中，用户可以同时属于一个或多个组，且通常如此。） |
| GECOS | 用户的可选个人信息。（finger 命令使用此字段，GECOS 代表 General Electric Comprehensive Operating System，这是一个早已遗忘的操作系统，但其名称因 `/etc/passwd` 中该字段的命名而得以留名。） |
| homedir | 用户家目录的名称 |
| shell | 当该用户登录时执行的命令解释器（shell），例如 bash (`/bin/bash`) |

# 管理组

组是用户所属的实体。组具有名称和标识符（ID）。定义组后，用户可以属于这些组中的一个或多个。
你可以在 `/etc/group` 中找到所有现有组的列表。例如，以下是定义名为 `wheel` 的组的行：
```
wheel::x:10:root,naba
```
如此示例所示，`/etc/group` 中的每一行具有以下格式，由冒号分隔为四个字段：
```
groupname:password:GID:membership
```
表 2-2 解释了组定义中四个字段的含义。

### 表 2-2 `/etc/group` 文件中各字段的含义

| 字段名称 | 含义 |
| :--- | :--- |
| groupname | 组的名称（例如，wheel） |
| password | 组密码（x 表示密码存储在 `/etc/shadow` 文件中） |
| GID | 数字组 ID（例如，10） |
| membership | 属于此组的用户名的逗号分隔列表（例如，root, naba） |

如果要创建新组，你可以直接使用 `groupadd` 命令。例如，要添加一个名为 `class` 的新组，并自动选择组 ID，只需在终端窗口中输入以下命令（你必须以 `root` 身份登录）：
```
groupadd class
```
然后，你可以使用 `usermod` 命令将用户添加到该组。例如，要将用户 `naba` 和 `ashley` 添加到名为 `class` 的组中，请输入以下命令：
```
usermod -G class naba
usermod -G class ashley
```
就这样。现在检查 `/etc/group`，发现它包含 `class` 的以下定义：
```
class:x:502:naba,ashley
```
就是这么简单！
如果要删除组，请使用 `groupdel` 命令。例如，要删除名为 `class` 的组，请输入：
```
groupdel class
```

# 探索用户环境

当你以用户身份登录时，你会获得一组环境变量，这些变量控制着你在 Linux 系统上看到和操作内容的许多方面。如果你想查看当前环境，请在终端窗口中输入以下命令：
```
env
```
（顺便说一下，`printenv` 命令也显示环境，但 `env` 更简短。）
`env` 命令会打印出长长的行列表。所有这些行的集合就是当前环境，每一行定义一个环境变量。例如，`env` 命令会显示如下典型行：
```
HOSTNAME=localhost.localhostdomain
```
此行定义了环境变量 `HOSTNAME`，其值定义为 `localhost.localhostdomain`。
环境变量无非是一个与字符串关联的名称。例如，环境变量 `PATH` 通常对普通用户定义如下：
```
PATH=/usr/local/bin:/bin:/usr/bin:/usr/X11R6/bin
```
等号（`=`）右侧的字符串是 `PATH` 环境变量的值。按照惯例，`PATH` 环境变量是目录名称的序列，每个名称由冒号（`:`）与前一个名称分隔。
每个环境变量都有特定用途。例如，当 shell 需要搜索文件时，它只是搜索列在 `PATH` 环境变量中的目录。shell 按出现顺序搜索 `PATH` 中的目录。因此，如果两个程序具有相同的名称，shell 将执行它首先找到的那个。
类似于 shell 使用 `PATH` 环境变量的方式，`vi` 等编辑器使用 `TERM` 环境变量的值来确定如何显示你用 `vi` 编辑的文件。要查看 `TERM` 的当前设置，请在 shell 提示符下输入以下命令：
```
echo $TERM
```
如果你在终端窗口中输入此命令，输出如下：
```
xterm
```
要在 `bash` 中定义环境变量，请使用以下语法：
```
export NAME=Value
```
在这里，`NAME` 表示环境变量的名称，`Value` 是表示其值的字符串。因此，你使用以下命令将 `TERM` 设置为值 `xterm`：
```
export TERM=xterm
```
![](img/792720823146d68f19fd50c99ebfce4b_446_0.png)
定义环境变量后，你可以通过使用语法 `NAME=new-value` 简单指定新值来更改其值。例如，要将 `TERM` 的定义更改为 `vt100`，请在 shell 提示符下输入 `TERM=vt100`。
对于像 `PATH` 这样的环境变量，你通常希望将新的目录名称追加到现有定义中，而不是从头开始定义 `PATH`。例如，如果你下载并安装了 Java 2 开发工具包（可从 http://java.sun.com/j2ee/1.5.0/download.jsp 获取），你需要将 Java 二进制文件的位置添加到 `PATH` 中。以下是完成该任务的方法：
```
export PATH=$PATH:/usr/java/jdk1.5.0/bin
```
此命令将字符串 `:/usr/java/jdk1.5.0/bin` 追加到 `PATH` 环境变量的当前定义中。其净效应是将 `/usr/java/jdk1.5.0/bin` 添加到 `PATH` 的目录列表中。
**注意：** 你也可以按以下方式编写此 `export` 命令：
```
export PATH=$PATH:/usr/java/jdk1.5.0/bin
```
输入该命令后，你可以访问 `/usr/java/jdk1.5.0/bin` 目录中的程序，例如 `javac`，即 Java 编译器，它将 Java 源代码转换为 Java 解释器可以执行的形式。
`PATH` 和 `TERM` 仅仅是少数常见环境变量中的两个。表 2-3 列出了典型 Linux 用户的一些环境变量。

表 2-3 Linux 中的典型环境变量

| 环境变量 | 内容 |
|---|---|
| DISPLAY | X 窗口系统显示输出的显示器名称（通常设置为 : 0.0） |
| HOME | 你的主目录 |
| HOSTNAME | 你的系统主机名 |
| LOGNAME | 你的登录名 |
| MAIL | 你的邮件目录位置 |
| PATH | shell 寻找程序的目录列表 |
| SHELL | 你的 shell（对于 bash，SHELL=/bin/ bash） |
| TERM | 终端类型 |

## 更改文件和目录的用户和组所有权

在 Linux 中，每个文件或目录都有两种类型的所有者——一个用户和一个组。换句话说，每个文件和目录都由一个用户和一个组拥有。用户和组的所有权可以控制谁可以访问文件或目录。



要查看文件或目录的所有者，请使用 `ls -l` 命令来查看目录的详细列表。例如，以下是典型文件的信息：

```text
-rw-rw-x--    1 naba    naba    40909 Aug 16 20:37
composer.txt
```

在这个例子中，第一组字符显示了文件的权限设置——谁可以读取、写入或执行该文件。第三个和第四个字段（在此例中为 `naba` `naba`）指示了该文件的用户和组所有者。每个用户都有一个与用户名私有的同名的组。因此，大多数文件的用户和组所有权看起来像是将用户名显示了两遍。

作为系统管理员，您可能决定将文件的组所有权更改为某个通用组。例如，假设您想要将 `composer.txt` 文件的组所有权更改为 `class` 组。为此，请以 `root` 身份登录并输入以下命令：

```text
chgrp class composer.txt
```

这个 `chgrp` 命令将 `composer.txt` 的组所有权更改为 `class`。在我尝试过之后，我再次输入 `ls -l` 以验证所有权，结果如下：

```text
-rw-rw-r-- 1 naba class 40909 Aug 16 20:37
composer.txt
```

您可以使用 `chown` 命令来更改用户所有者。该命令的格式如下：

```text
chown username filename
```

例如，要将名为 `sample.jpg` 的文件用户所有权更改为 `naba`，我输入：

```text
chown naba sample.jpg
```

事实上，`chown` 可以同时更改用户和组所有者。例如，要将用户所有者更改为 `naba`，将组所有者更改为 `class`，我输入：

```text
chown naba.class composer.txt
```

换句话说，您只需在用户名后加上一个点（`.`）再附上组名，并将该结果作为所有者的名称使用。

# 第 3 章：管理文件系统

## 本章内容

- 导航 Linux 文件系统
- 通过 NFS 共享文件
- 备份和还原文件
- 挂载 NIFS 文件系统
- 访问 MS-DOS 文件

文件系统指的是文件和目录的组织方式。作为系统管理员，您必须执行某些操作来管理各种存储介质上的文件系统。例如，您必须知道如何挂载——通过将存储介质上的文件系统附加到整个 Linux 文件系统来添加文件系统。您还必须备份重要数据并从备份中还原文件。其他文件系统操作包括通过网络文件系统（NFS）共享文件和访问 MS-DOS 文件。在本章中，我将向您展示如何执行所有文件管理任务。

## 探索 Linux 文件系统

您电脑中的文件和目录以一种有组织的方式存储信息，就像纸质档案系统一样。当您在纸上存储信息时，通常会将几页纸放入文件夹，然后将文件夹存放在文件柜中。如果您有很多文件夹，您可能会有某种归档系统。例如，您可能会标记每个文件夹的标签页，然后在文件柜中按字母顺序排列。您可能有好几个文件柜，每个文件柜都有许多抽屉，抽屉里又装满了包含多页纸的文件夹。

Linux 等操作系统以类似于纸质档案系统的方式组织您计算机中的信息。Linux 使用文件系统来组织您计算机中的所有信息。当然，存储介质不是金属文件柜和纸张。相反，Linux 将信息存储在硬盘驱动器、软盘驱动器和 CD-ROM 驱动器等设备上。

为了将计算机的文件系统与纸质档案系统进行类比，可以将磁盘驱动器想象为文件柜。文件柜中的抽屉对应于文件系统中的目录。每个抽屉中的文件夹也是目录——因为计算机文件系统中的目录可以包含其他目录。您可以将文件想象为文件夹里面的页——实际信息就存储在那里。图 3-1 说明了文件柜与 Linux 文件系统之间的类比。

![](img/792720823146d68f19fd50c99ebfce4b_451_0.png)

**图 3-1：** 这有点牵强，但您可以将 Linux 文件系统想象为类似于文件柜。

Linux 文件系统具有*层次*结构——目录可以包含其他目录，而这些目录又包含单个文件。

您的 Linux 系统中的所有内容都以文件系统中的文件和目录形式进行组织。要访问和使用系统中的文档和程序，您必须熟悉文件系统。

### 理解文件系统层次结构

Linux 文件系统像树一样组织，拥有一个 `root`（根）目录，其他所有目录都从此分支出去。当您写入完整的路径名时，`root` 目录由单个斜杠（`/`）表示。然后是一组文件和目录的层次结构。文件系统的部分可以位于不同的物理驱动器或不同的硬盘分区中。

Linux 使用标准的目录层次结构。图 3-2 展示了 Linux 文件系统的一些标准部分。当然，您可以在此结构中的任何位置创建新目录。

通过将标识该文件或目录所在位置的目录名称连接起来，并使用斜杠（`/`）作为分隔符，来写入任何文件或目录的名称。例如，在图 3-2 中，顶层的 `usr` 目录写作 `/usr`，因为 `root` 目录（`/`）包含 `usr`。另一方面，`X11R6` 目录位于 `usr` 目录内部，而 `usr` 目录又位于 `root` 目录（`/`）内部。因此，`X11R6` 目录由名称 `/usr/X11R6` 唯一标识。这种类型的完整名称被称为*路径名*，因为该名称标识了从 `root` 目录到达该文件所采取的路径。因此，`/usr/X11R6` 是一个路径名。

![](img/792720823146d68f19fd50c99ebfce4b_452_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_452_1.png)

文件系统层次结构标准（FHS）指定了 Linux 等类 UNIX 操作系统中文件和目录的组织方式。FHS 定义了一组标准目录及其预期用途。如果所有 Linux 发行版都忠实地采用 FHS，它应该有助于提高应用程序、系统管理工具、开发工具和脚本在所有 Linux 发行版之间的互操作性。FHS 甚至有助于系统文档以及像这样一类的书籍，因为对文件系统的相同描述适用于所有 Linux 发行版。FHS 2.3 版本于 2004 年 1 月 29 日宣布。FHS 2.3 是 Linux 标准基（LSB）3.0 版本的一部分，LSB 3.0 于 2005 年 7 月 1 日发布。LSB 3（参见 `www.linuxbase.org`）是一组二进制标准，旨在减少 Linux 发行版之间的差异并促进应用程序的可移植性。要了解有关 FHS 的更多信息，请访问位于 `www.pathname.com/fhs` 的 FHS 主页。

Linux 文件系统中的每个标准目录都有特定用途。表 3-1 总结了这些目录。

表 3-1 Linux 文件系统中的标准目录

| 目录 | 用于存储 |
| :--- | :--- |
| `/bin` | 用户命令的可执行文件（供所有用户使用） |
| `/boot` | 引导加载程序加载 Linux 内核所需的文件 |
| `/dev` | 设备文件 |
| `/etc` | 主机特定的系统配置文件 |
| （续） |

# 428 探索 Linux 文件系统

### 表 3-1（续）

| 目录 | 用途 |
| :--- | :--- |
| `/home` | 用户主目录 |
| `/lib` | 共享库和内核模块 |
| `/media` | 可移动媒体的挂载点 |
| `/mnt` | 临时挂载文件系统的挂载点 |
| `/opt` | 附加应用软件包 |
| `/root` | `root` 用户的主目录 |
| `/sbin` | 系统管理实用工具 |
| `/srv` | 本系统提供的服务（如 Web 和 FTP）的数据 |
| `/tmp` | 临时文件 |
| **`/usr` 层次结构** | **次要目录层次结构** |
| `/usr/X11R6` | X Window 系统，第 11 版本第 6 次发布 |
| `/usr/bin` | 大多数用户命令 |
| `/usr/include` | 头文件目录——通过各类指令插入应用程序源代码中的文件——用于开发 Linux 应用程序 |
| `/usr/lib` | 软件包和编程使用的库 |
| `/usr/libexec` | 应用程序的库 |
| `/usr/local` | 任何本地软件 |
| `/usr/sbin` | 非必需的 系统管理员实用工具 |
| `/usr/share` | 不依赖于系统架构的共享数据（无论系统是 Intel PC 还是 Sun SPARC 工作站） |
| `/usr/src` | 源代码 |
| **`/var` 层次结构** | **可变数据** |
| `/var/cache` | 应用程序的缓存数据 |
| `/var/lib` | 与应用程序当前状态相关的信息 |
| `/var/lock` | 锁文件，确保资源仅被一个应用程序使用 |
| `/var/log` | 组织在子目录中的日志文件 |
| `/var/mail` | 用户邮箱文件 |
| `/var/opt` | 存储在 `/opt` 目录中的软件包的可变数据 |
| `/var/run` | 描述系统自启动以来状态的数据 |
| `/var/spool` | 等待某种处理的数据 |
| `/var/tmp` | 在系统重启之间保留的临时文件 |



| `/var/yp` | 网络信息服务 (NIS) 数据库文件 |

## 在文件系统上挂载设备

您在 Linux 中使用的存储设备包含 Linux 文件系统。每个设备都有自己的本地文件系统，由目录层次结构组成。在您访问设备上的文件之前，必须将设备的目录层次结构附加到代表整体 Linux 文件系统的树上。

挂载是您执行的操作，使得物理存储设备（硬盘分区或 CD-ROM）上的文件系统看起来像是 Linux 文件系统的一部分。图 3-3 说明了挂载的概念。

![](img/792720823146d68f19fd50c99ebfce4b_454_0.png)

图 3-3 显示了每个设备，其名称以 `/dev` 开头。例如，`/dev/cdrom` 是第一个 DVD/CD-ROM 驱动器，`/dev/fd0` 是软盘驱动器。这些物理设备被挂载在 Linux 文件系统上的特定挂载点。例如，DVD/CD-ROM 驱动器 `/dev/cdrom` 被挂载在文件系统中的 `/media/cdrom` 上。以这种方式挂载 CD-ROM 后，CD-ROM 或 DVD-ROM 上的 Fedora 目录在 Linux 文件系统中显示为 `/media/cdrom/Fedora`。

您可以使用 `mount` 命令手动将设备挂载在 Linux 文件系统的指定目录上。该目录就是挂载点。例如，要在 `/media/cdrom` 目录上挂载 DVD/CD-ROM 驱动器，请输入以下命令（登录为 root 后）：

```bash
mount /dev/cdrom /media/cdrom
```

如果 DVD/CD-ROM 设备已经挂载，或者驱动器中没有 CD 或 DVD 介质，`mount` 命令会报告错误。否则，`mount` 操作成功，您可以通过 `/media/cdrom` 目录访问 DVD 或 CD 的内容。

> **牢记** 您可以使用任何目录作为挂载点。但是，如果您将设备挂载在非空目录上，在通过 `umount` 命令卸载设备之前，您无法访问该目录中的文件。因此，请始终使用空目录作为挂载点。

> **提示** 当您不再需要设备时，使用 `umount` 命令卸载设备。例如，对于设备名为 `/dev/cdrom` 的 DVD/CD-ROM 设备，输入以下命令以卸载该设备：

```bash
umount /dev/cdrom
```

只要没有人正在使用 DVD/CD-ROM，`umount` 命令就会成功。如果您在尝试卸载 DVD/CD-ROM 时收到错误，请检查当前工作目录是否在 DVD 或 CD 上。如果您当前正在 DVD/CD-ROM 的某个目录中工作，这也算作对 DVD/CD-ROM 的使用。

## 检查 `/etc/fstab` 文件

`mount` 命令具有以下通用格式：

```bash
mount device-name mount-point
```

> **牢记** 然而，如果您只指定 CD-ROM 设备名称或挂载点名称，也可以进行挂载，前提是 `/etc/fstab` 文件中存在该 CD-ROM 挂载点的条目。该条目指定了 CD-ROM 设备名称和文件系统类型。这就是为什么您可以使用更短的 `mount` 命令来挂载 CD-ROM 的原因。

> **发行版特定** 例如，在 Debian 中，您可以通过输入以下任一命令来挂载 CD-ROM：

```bash
mount /dev/cdrom
mount /media/cdrom
```

`/etc/fstab` 文件是一个**配置文件**——一个包含 `mount` 和 `umount` 命令所使用的信息的文本文件。`/etc/fstab` 文件中的每一行都提供了关于设备及其在 Linux 文件系统中的挂载点的信息。本质上，`/etc/fstab` 文件将文件系统中的各种挂载点与特定设备关联起来，这使得 `mount` 命令可以仅以挂载点或设备作为参数从命令行工作。

![](img/792720823146d68f19fd50c99ebfce4b_456_0.png)

这是一个来自 SUSE 系统的 `/etc/fstab` 文件。（其他 Linux 发行版中该文件的格式类似。）

```text
/dev/hda11          /      reiserfs acl,user_xattr  1 1
/dev/hda7       /boot     ext3 acl,user,xattr  12
/dev/hda6       /data1    auto noauto, user 00
/dev/hda9       /data2    auto noauto, user 00
/dev/hda10      /data3    auto noauto, user 00
/dev/hda5       /data4    auto noauto, user 00
/dev/hda2       /windows/ C ntfs ro, users, gid=users, umask=0002, files=utf8 00
/dev/hda8       swap      swap pr i=42 00
devpts          /dev/pts devpts mode=0620, gid=5 00
proc            /proc     proc defaults 00
usbfs           /proc/bus/usb usbfs noauto 00
sysfs           /sys      sysfs noauto 00
/dev/cdrecorder /media/cdrecorder auto fs=nfs, ro, procuid, nousid, nodev, exec, localizer=utf8 00
/dev/fd0 /media/floppy    auto fs=floppyfs, procuid, nodev, nousid, sync 00
```

每行的第一个字段显示设备名称，如硬盘分区。第二个字段是挂载点，第三个字段指示设备上的文件系统类型。您暂时可以忽略最后三个字段。

此 `/etc/fstab` 文件显示 `/dev/hda8` 设备作为虚拟内存的交换设备，这就是为什么挂载点和文件系统类型都被设置为*swap*的原因。

![](img/792720823146d68f19fd50c99ebfce4b_456_1.png)

Linux 操作系统使用 `/etc/fstab` 文件的内容来自动挂载各种文件系统。在 Linux 启动期间，init 进程执行一个 shell 脚本，该脚本运行 `mount -a` 命令。该命令读取 `/etc/fstab` 文件并挂载所有列出的文件系统（除带有 `noauto` 选项的那些）。`/etc/fstab` 每行的第三个字段指定该设备上的文件系统类型，第四个字段显示 `mount` 命令在将设备挂载到文件系统时使用的逗号分隔选项列表。通常，您会在这个字段中找到 `defaults` 选项。除了其他含义外，`defaults` 选项意味着设备在启动时挂载，只有 `root` 用户可以挂载该设备，并且设备可读写。如果选项包括 `noauto`，设备不会在系统启动时自动挂载。

在 Fedora Core 中，您经常会在 `/etc/fstab` 条目的第四个字段中发现 `managed` 选项。`managed` 选项表示该行是由运行 `fstab-sync` 命令以在检测到每个可移动驱动器时向 `/etc/fstab` 文件添加条目的 HAL（硬件抽象层）守护程序添加到 fstab 文件中的。您通常会发现 DVD/CD-ROM 驱动器（在大多数系统中为 `/dev/hdc`）和软盘驱动器（`/dev/fd0`）的条目在第四个字段中具有 `managed` 选项。

## 通过 NFS 共享文件

通过 NFS 共享文件很简单，涉及两个基本步骤：

- 在 NFS 服务器上，通过在 `/etc/exports` 文件中列出目录并运行 `/usr/sbin/exportfs` 命令来导出一个或多个目录。此外，您必须运行 NFS 服务器。
- 在每个客户端系统上，使用 `mount` 命令挂载服务器已导出的目录。

如何启动 NFS 服务器取决于 Linux 发行版。如果有图形化系统管理工具，您可以从图形工具启动 NFS 服务器。否则，您可以在终端窗口中键入命令来启动 NFS 服务器。例如，在 Debian 中，您可以输入 `invoke-rc.d nfs-kernel-server start` 和 `invoke-rc.d nfs-common start` 来启动 NFS 服务器。在 Fedora Core 中，输入 `service nfs start`。在 SUSE 中，您可以使用 YaST 控制中心（主菜单 > 系统 > YaST）来启动 NFS 服务器。它在网络服务类别中。在 Xandros 中，您可以从 Xandros 控制中心（主菜单 > 控制中心）启动 NFS 服务器，或者在终端窗口中键入 `invoke-rc.d nfs-user-server start`。



使用 NFS 的唯一问题是每个客户端系统都必须支持它。大多数 PC 不附带 NFS——这意味着如果您想通过 NFS 共享文件，必须单独购买 NFS 软件。但是，如果您的局域网（LAN）上的所有系统都运行 Linux（或其他内置 NFS 支持的 UNIX 变体），那么使用 NFS 是有意义的。

NFS 存在安全漏洞。因此，请勿在直接连接到互联网的系统上设置 NFS。

在下一节中，我将以一个局域网中两台 Linux PC 为例，引导您完成 NFS 设置。

# 使用 NFS 导出文件系统

从导出——向客户端系统提供——目录内容的服务器系统开始。在服务器上，您必须运行 NFS 服务器。

## 挂载 NFS 文件系统

要在客户端系统上访问导出的 NFS 文件系统，必须将该文件系统挂载到一个挂载点上——就实际操作而言，挂载点不过是一个本地目录。例如，假设你希望访问从名为 LNB P 200 的服务器导出的 `/home` 目录，并将其挂载到客户端系统的本地目录 `/mnt/lndp200` 上。为此，请遵循以下步骤：

1. **以 root 身份登录，并使用以下命令创建目录：**

```bash
mkdir /mnt/lndp200
```

2. **键入以下命令以执行挂载操作：**

```bash
mount lndp200:/home/public /mnt/lndp200
```

如果你只知道服务器的 IP 地址，请将该主机名（在此例中为 `lnbp200`）替换为 IP 地址。

3. **使用命令** `cd /mnt/lnbp200` **切换到目录** `/mnt/lnbp200`。

现在你可以从此目录查看和访问导出的文件。

为了确认 NFS 文件系统确实已挂载，请在客户端系统上以 `root` 身份登录，并在终端窗口中键入 `mount`。你将会看到关于 NFS 文件系统的一行类似以下内容的信息：

`lnbp200:/home//public` on `/mnt/lnbp200` type nfs (`rw,addr=192.168.1.200`)

# 备份和还原文件

备份和还原文件是至关重要的系统管理任务。如果系统硬盘发生故障，你必须依靠备份来恢复重要文件。在此，我将介绍一些备份策略，描述几种备份介质，并解释如何使用随 Linux 提供的归档程序（`tar`）来备份和还原文件。此外，你还将了解如何在磁带上执行增量和自动备份。

> 如果你拥有 CD 刻录机，也可以通过将文件刻录到 CD-R 上来备份文件。请参阅第二卷第四章，了解有关可用于刻录数据 CD 的应用程序的信息。

## 选择备份策略和介质

你的 Linux 系统硬盘包含维持系统运行所需的一切——以及其他使你的业务运行下去的文件（如文档和数据库）。你必须备份这些文件，以便在硬盘崩溃时能够快速恢复并使系统恢复正常。通常，你必须遵循严格的定期备份规程，因为你永远无法预测硬盘何时会故障或文件系统何时会损坏。要实施这种规程，首先确定你要备份哪些文件、备份频率以及如何，以及使用什么备份存储介质。这就是我所说的选择备份策略和备份介质的含义。

你对备份策略和备份介质的选择取决于你对因硬盘故障导致业务中断风险的评估。根据你使用 Linux 系统的方式，磁盘故障对你造成的影响可能大也可能小。

例如，如果你将 Linux 系统作为学习工具（用于深入了解 Linux 或编程），你可能只需要一些用于配置 Linux 的系统文件的备份副本。在这种情况下，你的备份策略可以是每次更改任何系统配置时，将重要的系统配置文件保存到一张或多张软盘上。

另一方面，如果你将 Linux 系统用作办公服务器，为许多用户提供共享文件存储，那么因磁盘故障导致业务中断的风险要高得多。在这种情况下，你必须每周备份所有文件，并每天备份任何新增或更改的文件。你可以以自动化的方式执行这些备份（使用本迷你书中第 1 章描述的作业调度功能）。此外，你可能还需要能够存储大量（数吉字节）数据的备份存储介质。换言之，对于高风险情况，你的备份策略更加复杂，需要额外的设备（如磁带驱动器）。

你对备份介质的选择取决于你要备份的数据量。对于少量数据（如系统配置文件），你可以使用软盘或 USB 闪存盘作为备份介质。如果你的 PC 有 Zip 驱动器，你可以使用 Zip 磁盘作为备份介质；这些适合备份单用户目录。要备份整个服务器，请使用磁带驱动器，通常是连接到 SCSI 控制器的 4mm 或 8mm 磁带驱动器。此类磁带驱动器可以在每条磁带上存储数吉字节的数据，你可以使用它们在单条磁带上备份整个文件系统。

在将这些介质用于备份文件时，你必须通过名称引用备份设备。表 3-2 列出了某些常见备份设备的设备名称。

### 表 3-2 常见备份设备的设备名称

| 备份设备 | Linux 设备名称 |
| :--- | :--- |
| 软盘 | `/dev/fd0` |
| IDE Zip 驱动器 | `/dev/hdc4` 或 `/dev/hdd4` |
| SCSI Zip 驱动器 | `/dev/sda`（假设它是第一个 SCSI 驱动器——否则，设备名称取决于 SCSI ID） |
| SCSI 磁带驱动器 | `/dev/st0` 或 `/dev/nst0`（前缀 n 表示文件复制到磁带后磁带不会倒带。） |

## Linux 的商业备份实用程序

在下一节中，我将解释如何使用随 Linux 提供的归档程序（`tar`）备份和还原文件。虽然你可以使用 `tar` 管理备份，但有多种带有图形用户界面和其他功能以简化备份流程的商业备份实用程序。以下是一些知名的 Linux 商业备份实用程序：

- **BRU：** TOLIS Group, Inc. 的备份和还原实用程序（*www.tolisgroup.com*）
- **LONE-TAR：** Lone Star Software Corp. 的磁带备份软件包（*www.cactus.com*）
- **Arkeia：** Arkeia 的异构网络备份和恢复软件（*www.arkeia.com*）
- **Bare Metal Plus：** UniTrends 的备份和恢复软件（*www.unitrends.com*）
- **BrightStor ARCServe Backup for Linux：** Computer Associates 的 Linux 系统数据保护技术（*www3.ca.com/solutions/product.asp?id=3370*）

## 使用归档程序 —— tar

你可以使用 `tar` 命令将文件归档到设备中，例如软盘或磁带。`tar` 程序创建一个归档文件，该文件可以包含其他目录和文件，并且（可选地）压缩归档以实现高效存储。然后，归档被写入指定的设备或另一个文件。实际上，许多软件包都是以压缩的 `tar` 文件形式分发的。

`tar` 程序的命令语法如下：

```
tar options destination source
```

在此，*options*（选项）通常由一系列单个字母指定，每个字母指定 `tar` 执行的操作。*destination*（目标）是备份设备的设备名称。而 *source*（源）是表示要备份的文件或目录名称的列表。

## 备份和还原单卷归档

例如，假设你想将 `/etc/X11` 目录的内容备份到软盘上。以 `root` 身份登录，将软盘放入软盘驱动器，并键入以下命令：

```
tar zcvf /dev/fd0 /etc/X11
```

`tar` 程序会在每个文件复制到软盘上的压缩 `tar` 归档时显示文件名列表。在这种情况下，选项是 `zcvf`，

目标设备为 `/dev/fd0`（软盘），源设备为 `/etc/X11` 目录（这意味着包含其所有子目录及其内容）。你可以使用类似的 `tar` 命令将文件备份到磁带上——只需将 `/dev/fd0` 替换为磁带设备即可——例如，对于 SCSI 磁带驱动器，可以使用 `/dev/st0`。

### 表 3-3 常用 tar 选项

| 选项 | 执行以下操作 |
| :--- | :--- |
| c | 创建新归档 |
| f | 指定命令行下一个字段中的归档文件或设备名称 |
| M | 指定多卷归档。（下一节将介绍多卷归档。） |
| t | 列出归档内容 |
| v | 显示详细消息 |
| x | 从归档中提取文件 |
| z | 使用 `gzip` 压缩 tar 归档 |

要查看在软盘上创建的 `tar` 归档的内容，请输入以下命令：

```
tar ztf /dev/fd0
```

你会看到一个文件名列表（每个文件名都以 `/etc/X11` 开头），显示备份中包含的内容。在此 `tar` 命令中，`t` 选项用于列出 `tar` 归档的内容。

要从 `tar` 备份中提取文件，请在以 `root` 身份登录时按照以下步骤操作：

1. **输入以下命令将目录更改为 `/tmp`：**

```
cd /tmp
```

这一步是你练习从 `tar` 备份中提取文件的地方。对于实际备份，请将目录更改到合适的位置（通常输入 `cd /`）。

2. **输入以下命令：**



```
tar zxvf /dev/fd0
```

此 `tar` 命令使用 `x` 选项从存储在 `/dev/fd0`（软盘）上的归档中提取文件。

现在，如果你检查 `/tmp` 目录的内容，你会发现 `tar` 命令在 `/tmp` 中创建了一个 `etc/X11` 目录树，并将 `tar` 归档中的所有文件恢复到该目录中。`tar` 命令会去掉归档中文件名前的 `/`，并将文件恢复到当前目录。如果你想从软盘上的归档中恢复 `/etc/X11` 目录，请使用此命令：

```
tar zxvf /dev/fd0 -C /
```

命令末尾的 `/` 表示你希望恢复备份文件的目录。

你可以使用 `tar` 命令来创建、查看和恢复归档。你可以将归档存储在文件中，或者存储在你通过设备名称指定的任何设备中。

## 备份和恢复多卷归档

有时，单个存储介质的容量小于存储归档所需的总存储空间。在这种情况下，你可以使用多卷归档的 `m` 选项——这意味着归档可以跨越多个磁带或软盘。不过，请注意，你不能创建压缩的多卷归档。这意味着你必须放弃 `z` 选项。要了解多卷归档的工作原理，请以 `root` 身份登录，在软驱中放入一张软盘，并输入以下 `tar` 命令：

```
tar cvfm /dev/fd0 /usr/share/doc/ghostscript*
```

注意：`m` 选项包含在选项字母中；它指示 `tar` 创建多卷归档。当第一张软盘填满时，`tar` 命令会提示你提供第二张软盘。当你看到以下提示时，取出第一张软盘并插入另一张软盘：

```
Prepare volume #2 for '/dev/fd0' and hit return:
```

按下 Enter 键后，`tar` 程序将继续使用第二张软盘。在此示例中，你只需要两张软盘即可存储归档；对于较大的归档，`tar` 程序会继续提示插入软盘，以防需要更多软盘。

要从该多卷归档中恢复，请输入 `cd /tmp` 将目录更改为 `/tmp`。这里我使用 `/tmp` 目录作为示例，但在从归档中恢复文件时，你必须使用一个真实的目录。然后输入

```
tar xvfm /dev/fd0
```

`tar` 程序会提示你根据需要装入软盘。

![](img/792720823146d68f19fd50c99ebfce4b_464_0.png)

使用 `du -s` 命令来确定归档目录所需的存储空间。例如，输入 `du -s /etc` 即可查看 `/etc` 目录的总大小（以千字节为单位）。以下是该命令的典型输出：

```
35724	/etc
```

输出结果表明，备份 `/etc` 目录至少需要 35,724K 的存储空间。

## 在磁带上进行备份

虽然使用正确的设备名称在 `tar` 命令中进行磁带备份很简单，但你必须了解磁带设备的一些细微差别才能有效地使用它。当你使用 `tar` 备份到名为 `/dev/st0` 的设备（第一个 SCSI 磁带驱动器）时，磁带设备会在 `tar` 程序完成将归档复制到磁带后自动倒带。`/dev/st0` 设备被称为倒带式磁带设备，因为它默认会倒带。

如果你的磁带可以存储数 GB 的数据，你可能希望将多个 `tar` 归档——一个接一个——写入同一盘磁带（否则磁带的很大一部分可能留空）。如果你打算这样做，你的磁带设备在 `tar` 程序完成后不能倒带。为了帮助你处理此类场景，多个 Linux 磁带设备是非倒带式的。非倒带式 SCSI 磁带设备被称为 `/dev/nst0`。如果你想在磁带上依次写入归档，请使用此设备名称。

![](img/792720823146d68f19fd50c99ebfce4b_464_1.png)

在每个归档之后，非倒带式磁带设备会写入一个文件结束（EOF）标记，以分隔一个归档与下一个归档。使用 `mt` 命令来控制磁带——你可以从一个标记移动到下一个标记，或者倒带。例如，在使用 `/dev/nst0` 设备名称向磁带写入多个归档后，你可以使用以下命令强制磁带倒带：

```
mt -f /dev/nst0 rewind
```

倒带后，你可以使用以下命令从第一个归档中提取文件到当前磁盘目录：

```
tar xvf /dev/nst0
```

之后，你必须越过 EOF 标记到达下一个归档。为此，请使用以下 `mt` 命令：

```
mt -f /dev/nst0 fsf 1
```

这将把磁带定位到下一个归档的开头。现在再次使用 `tar xvf` 命令来读取此归档。

![](img/792720823146d68f19fd50c99ebfce4b_465_0.png)

如果你在磁带上保存了多个归档，你必须自己记录这些归档。归档的顺序可能很难记住，因此你最好每盘磁带只保存一个归档。

## 执行增量备份

假设你使用 `tar` 将系统的硬盘备份到磁带上。由于这种完整备份可能花费相当长的时间，你不想每晚都重复这项任务。 此外，一天中可能只有少数文件发生了变化。要定位需要备份的文件，你可以使用 `find` 命令列出过去 24 小时内所有已更改的文件：

```bash
find / -mtime -1 -type f -print
```

此命令打印出过去一天内已更改的文件列表。`-mtime -1` 选项意味着你想要最后修改时间少于一天的文件。现在你可以将此 `find` 命令与 `tar` 命令结合使用，以仅备份过去一天内已更改的那些文件：

```bash
tar cvf /dev/st0 `find / -mtime -1 -type f -print`
```

当你在两个单引号 `` ` `` 之间放置一个命令时，shell 会执行该命令并将其输出放在命令行中的该位置。最终结果是 `tar` 程序仅将已更改的文件保存在归档中。此过程为你提供了仅自前一天以来已更改的文件的增量备份。

## 执行自动备份

在本小册子的第 1 章中，我向你展示了如何使用 `crontab` 设置定期任务（称为 `cron jobs`）。Linux 系统会定期执行这些任务。备份你的系统是 `crontab` 功能的一个良好用途。假设你的备份策略如下：

- 每周日凌晨 1:15，你的系统会将整个硬盘备份到磁带上。
- 周一至周六，你的系统会在凌晨 3:10 执行增量备份，仅保存过去 24 小时内已更改的文件。

要设置此自动备份计划，请以 `root` 身份登录，并在名为 `backups` 的文件中输入以下行（此示例假设你使用 SCSI 磁带驱动器）：

### 自动化备份计划

```
15 1 * * * 0 tar zcvf /dev/st0 /
10 3 * * * 1-6 tar zcvf /dev/st0 "find / -mtime -1 -type f -print"
```

接下来，使用以下 `crontab` 命令提交此作业计划：

```
crontab backups
```

现在，您的系统已设置为自动执行备份。您只需每天在磁带驱动器中放入一条新磁带即可。请记住为每条磁带贴上适当的标签。

## 访问 DOS/Windows 文件系统

如果您的硬盘上安装了 Microsoft Windows 95/98/Me，您可能已经将在 Linux 下挂载了 DOS/Windows 分区。如果没有，您可以轻松地在 Linux 中挂载 DOS/Windows 分区。挂载操作使得 DOS/Windows 目录层级结构成为 Linux 文件系统的一部分。

### 挂载 DOS/Windows 磁盘分区

要在 Linux 中挂载 DOS/Windows 硬盘分区或软盘，请使用 `mount` 命令，但需包含选项 `-t vfat` 以指示文件系统类型为 DOS。例如，如果您的 DOS 分区碰巧是您 IDE（集成驱动电子）硬盘上的第一个分区，并且您希望将其挂载到 `/dosc` 上，请使用以下 `mount` 命令：

```
mount -t vfat /dev/hda1 /dosc
```

`mount` 命令中的 `-t vfat` 部分指定您 `mount`（挂载）的设备——`/dev/hda1`——具有 MS-DOS 文件系统。图 3-4 说明了此 `mount` 命令的效果。

![](img/792720823146d68f19fd50c99ebfce4b_467_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_467_1.png)

### 挂载 DOS 软盘

就像您在 Linux 文件系统中挂载 DOS 硬盘分区一样，您也可以挂载 DOS 软盘。您必须以 `root` 身份登录才能挂载软盘，但您可以按照本节后半部分所示步骤设置系统，以便任何用户都可以挂载 DOS 软盘。您还需要知道软盘驱动器的设备名称。默认情况下，Linux 定义了以下两个通用软盘设备名称：

- `/dev/fd0` 是 A 驱动器（第一个软盘驱动器）
- `/dev/fd1` 是 B 驱动器（第二个软盘驱动器，如果您有的话）

关于挂载点，您可以使用文件系统中的任何空目录作为挂载点，但 Linux 系统自带一个专门用于挂载软盘的目录：`/media/floppy`。

要在 `/media/floppy` 目录上挂载 DOS 软盘，请将软盘插入驱动器并输入以下命令：



```
mount -t vfat /dev/fd0 /media/floppy
```

挂载软盘后，您可以使用 Linux 复制命令（`cp`）在软盘之间复制文件。要将文件 `gnomel.pcx` 从当前目录复制到软盘，请输入以下内容：

```
cp gnomel.pcx /media/floppy
```

类似地，要查看软盘的内容，请输入以下内容：

```
ls /media/floppy
```

如果您想将软盘从驱动器中弹出，请先 *卸载*（unmount）软盘驱动器。卸载操作会移除软盘文件系统与 Linux 文件系统上的挂载点之间的关联。使用 `umount` 命令像这样卸载软盘：

```
umount /dev/fd0
```

您可以设置您的 Linux 系统，使任何用户都能挂载 DOS 软盘。例如，若要使任何用户都能在 `/a` 目录上挂载 A 驱动器中的 DOS 软盘，请执行以下步骤：

1. 以 `root` 身份登录。

2. 在终端窗口中输入以下命令，创建 `/a` 目录（挂载点）：

   ```
   mkdir /a
   ```

3. 在文本编辑器（如 `vi` 或 `emacs`）中编辑 `/etc/fstab` 文件，插入以下行，然后保存文件并退出编辑器：

   ```
   /dev/fd0   /a   vfat   noauto,user   0   0
   ```

   该行中的第一个字段是软盘驱动器的设备名称（`/dev/fd0`）；第二个字段是挂载目录（`/a`）；第三个字段显示文件系统类型（`vfat`）。`user` 选项（出现在 `noauto` 旁边）使得所有用户能够挂载 DOS 软盘。

4. 注销，然后以普通用户身份重新登录。

5. 要确认您能够以普通用户身份而不仅仅是 `root` 身份挂载 DOS 软盘，请将一张 DOS 软盘插入 A 驱动器，并输入以下命令：

   ```
   mount /a
   ```

   挂载操作成功，当您输入 `ls /a` 命令时，您会看到 DOS 软盘的列表。

6. 要卸载 DOS 软盘，请输入 `umount /a`。

## 挂载 NTFS 分区

如今，大多数 PC 硬盘上预装了 Windows XP 或 Windows 2000。Windows XP 和 2000，以及 Windows NT，通常使用 NT 文件系统（NTFS）。Linux 支持对 NTFS 分区的只读访问，许多发行版都附带了访问 NTFS 分区所需的 `ntfs.ko` 内核模块。

如果您在 Windows XP 系统上安装了 Linux，并想要访问 NTFS 分区上的文件，但您的发行版未包含 `ntfs.ko` 模块，您可以在内核配置步骤中启用 NTFS 模块后构建内核。（有关配置、构建和安装内核的详细说明，请参阅本小册子的第 5 章。）

重新构建并从新内核启动后，以 `root` 身份登录，并输入以下命令为 NTFS 分区创建挂载点。（在这种情况下，我在 `/mnt` 目录中创建了一个挂载点。）

```bash
mkdir /mnt/xp
```

现在，您可以使用以下命令挂载 NTFS 分区：

```bash
mount /dev/hda2 /mnt/xp -t ntfs -r -o umask=0222
```

![](img/792720823146d68f19fd50c99ebfce4b_469_0.png)

> 请将 `/dev/hda2` 替换为您系统中 NTFS 分区的设备名称。在大多数预装 Windows XP 的 PC 上，NTFS 分区是第二个（`/dev/hda2`）——第一个分区（`/dev/hda1`）通常是一个用于存放 Windows XP 安装所需文件的隐藏分区。

## 使用 mtools

访问 MS-DOS 文件系统的一种方法是首先使用 `mount` 命令挂载 DOS 硬盘或软盘，然后使用常规 Linux 命令（如 `ls` 和 `cp`）来操作已挂载的 DOS 文件系统。对于硬盘，这种挂载 DOS 文件系统的方法是没有问题的。Linux 可以在启动时自动挂载 DOS 分区，您可以随时访问硬盘上的 DOS 目录。

然而，如果您想要快速查看 DOS 软盘的目录列表，挂载操作很快就会变得相当麻烦。首先，您必须挂载软盘驱动器。然后，您必须使用 `ls` 命令。最后，在将软盘弹出之前，您必须使用 `umount` 命令。

在这种情况下，`mtools` 包起到了补救作用。`mtools` 包实现了大多数常见的 DOS 命令；这些命令的名称与 DOS 中相同，只是每个命令前都加上了 m 前缀。因此，获取目录列表的命令是 `mdir`，而 `mcopy` 用于复制文件。mtools 最棒的一点在于，您无需挂载软盘即可使用 mtools 命令。

![](img/792720823146d68f19fd50c99ebfce4b_470_0.png)

由于 mtools 命令对物理设备（软盘）进行读写，您必须以 root 身份登录才能执行这些命令。如果您希望任何用户都能访问 mtools 命令，您必须更改软盘驱动器设备的权限设置。使用以下命令允许任何人读写第一个软盘驱动器：

```
chmod o+rw /dev/fd0
```

### 尝试 mtools

若要尝试 mtools，请遵循以下步骤：

1. 将一张 MS-DOS 软盘放入系统的 A 驱动器。

2. 输入 `mdir`。

您将看到软盘的目录（采用标准的 DOS 目录列表格式）。

通常，您使用 mtools 实用程序来访问软盘。默认配置文件 `/etc/mtools.conf` 设置为将软盘驱动器识别为 A 驱动器。虽然您可以编辑该文件为您的 DOS 硬盘分区定义 C 和 D 驱动器，但您也可以使用 Linux `mount` 命令将它们挂载起来，从而访问硬盘分区。由于您可以自动挂载硬盘分区在启动时，通过 Linux 命令访问它们通常同样容易。

### 理解 /etc/mtools.conf 文件

mtools 包使用默认设置即可工作，但如果您遇到任何错误，请检查 `/etc/mtools.conf` 文件。该文件包含了 mtools 实用程序看到的驱动器（如 A、B 和 C）的定义。以下是典型的 `/etc/mtools.conf` 文件中的几行内容：

```
drive a: file="/dev/fd0" exclusive mformat_only
drive b: file="/dev/fd1" exclusive mformat_only
# First SCSI hard disk partition
drive c: file="/dev/sda1"
# First IDE hard disk partition on a Windows 98 PC
drive c: file="/dev/hda1"
# Internal IDE Zip drive
drive e: file="/dev/hdd4" exclusive
```

井号（`#`）表示注释的开始。每一行定义了一个驱动器字母、关联的 Linux 设备名称以及指示如何访问该设备的某些关键字。在此示例中，前两行定义了驱动器 A 和 B。第三行非注释行定义了驱动器 C 为第一个分区

## 第一个 IDE 驱动器 (/dev/hda)

如果你有其他的 DOS 驱动器（例如 D 盘），你可以添加另一行定义，将 D 盘指定为相应的磁盘分区。

如果你系统的 A 驱动器是一个高密度 3.5 英寸驱动器，那么访问软驱时无需更改默认 `/etc/mtools.conf` 文件中的任何内容。如果你还想访问硬盘中的任何 DOS 分区，请取消对 C 盘相应行的注释并进行编辑。

你还可以通过 `mtools` 访问 Iomega Zip 驱动器。只需指定一个盘符和相应设备的文件名即可。对于内置 IDE (ATAPI) Zip 驱动器，请尝试将 `/dev/hdd4` 作为设备文件，并在 `/etc/mtools.conf` 文件中添加以下行：

```
drive e: file="/dev/hdd4"
```

之后，你可以使用 `mtools` 命令访问 Zip 驱动器（将其称为 E 盘）。例如，要查看目录列表，请将 Zip 盘插入 Zip 驱动器并输入：

```
mdir e:
```

## 学习 mtools 命令

`mtools` 包是一组实用工具。到目前为止，我一直在使用 `mdir` —— 它是 DOS 中 **DIR** 命令的 `mtools` 对应版本。其他 `mtools` 命令使用起来相当简单。

如果你熟悉 MS-DOS 命令，使用 `mtools` 命令就很容易。只需以小写字母输入 DOS 命令，并记得在每个命令前加上 `m`。由于 Linux 命令和文件名是区分大小写的，因此你在输入 `mtools` 命令时必须全部使用小写字母。

表 3-4 总结了 `mtools` 中可用的命令。

![](img/792720823146d68f19fd50c99ebfce4b_471_0.png)

| `mtools` 工具 | `MS-DOS 命令`（如果有） | `该 mtools 工具执行以下操作` |
| :--- | :--- | :--- |



# mtools 命令参考

| `mattrb` | `ATTRIB` | 更改 MS-DOS 文件属性标志 |
| `mbadblocks` | | 测试软盘并在文件分配表 (`FAT`) 中标记坏块 |
| `mcd` | `CD` | 更改 MS-DOS 目录 |
| `mcopy` | `COPY` | 在 MS-DOS 和 Linux 之间复制文件 |
| `mdel` | `DEL` 或 `ERASE` | 删除 MS-DOS 文件 |
| `mdeltree` | `DELTREE` | 递归删除 MS-DOS 目录 |
| `mdir` | `DIR` | 显示 MS-DOS 目录列表 |
| `mdu` | | 列出目录及其内容所占用的空间 |
| `mformat` | `FORMAT` | 在低级格式化的软盘上放置 MS-DOS 文件系统（在 Linux 中，请使用 `fformat` 对软盘进行低级格式化。） |
| `minfo` | | 获取有关 MS-DOS 文件系统的信息 |
| `mkmanifest` | | 创建短名称等效项列表 |
| `mlabel` | `LABEL` | 初始化 MS-DOS 卷标 |
| `mmd` | `MD` 或 `MKDIR` | 创建 MS-DOS 目录 |
| `mmove` | | 移动或重命名 MS-DOS 文件或子目录 |
| `mmount` | | 挂载 MS-DOS 磁盘 |
| `mpartition` | | 将 MS-DOS 文件系统创建为分区 |
| `mrd` | `RD` 或 `RMDIR` | 删除 MS-DOS 目录 |
| `mren` | `REN` 或 `RENAME` | 重命名现有的 MS-DOS 文件 |
| `mshowfat` | | 显示 MS-DOS 文件的 FAT 条目 |
| `mtooldtest` | | 测试并显示当前 `mtools` 配置 |
| `mtype` | `TYPE` | 显示 MS-DOS 文件的内容 |
| `mwrite` | `COPY` | 将 Linux 文件复制到 MS-DOS |
| `mzip` | | 对 SCSI Zip 磁盘执行某些操作 |

## 使用 mtools

你可以像使用相应的 DOS 命令一样使用 `mtools` 命令。例如，`mdir` 命令在 DOS 中的工作方式与 `DIR` 命令相同。表 3-4 中显示的所有其他 `mtools` 命令也是如此。

你可以与 `mtools` 命令配合使用通配符（例如 `*`），但请记住 Linux shell 是第一个看到你的命令的程序。如果你不希望 shell 到处展开通配符字符，请使用引号包围包含任何通配符字符的文件名。例如，要从 A 盘将所有的 `*.txt` 文件复制到当前目录，请使用以下命令：

```
mcopy "a:\*.txt" .
```

如果你省略引号，shell 将试图使用当前 Linux 目录中的文件名来展开字符串 `a:\*.txt`。它还会尝试从 DOS 软盘中复制这些文件（如果有的话）。

另一方面，如果你想从 Linux 目录复制文件到 DOS 软盘，那么你确实希望 shell 展开任何通配符。例如，要从当前 Linux 目录将所有的 `*.jpg` 文件复制到 DOS 软盘，请像这样使用 `mcopy`：

```
mcopy *.jpg a:
```

使用 `mtools` 工具时，你可以像 DOS 中一样使用反斜杠字符 (`\`) 作为目录分隔符。然而，当你输入包含反斜杠字符的文件名时，你必须用双引号 (`"`) 包围该名称。例如，这是一个将 A 盘子目录中的文件复制到当前 Linux 目录的命令：

```
mcopy "a:\test\sample.dat" .
```

# 第 4 章：安装和更新应用程序

## 本章内容

- 使用 `rpm` 命令处理 RPM 文件
- 使用 `dpkg`、`dselect` 和 `APT` 处理 DEB 文件
- 从源文件构建应用程序
- 在线更新 Linux 应用程序

大多数 Linux 软件包以两种特殊文件格式之一分发：Red Hat Package Manager (`RPM`) 文件或者 Debian (`DEB`) 文件。这就是为什么你必须知道如何安装或删除以 RPM 或 DEB 文件形式出现的软件包的原因。幸运的是，本章将向你展示如何处理 RPM 和 DEB 文件。

你可以在所有 Linux 发行版中安装 RPM 和 DEB 文件，但每个发行版都有其偏好的分发格式。Fedora Core 凭借其 Red Hat Linux 的传承，偏爱 RPM 文件，而大多数基于 Debian 的发行版，如 Knoppix、MEPIS、Ubuntu 和 Xandros，使用 DEB 文件来分发软件。SUSE Linux 使用 RPM 格式。

许多其他开源软件包以源代码形式提供，通常是在压缩归档中。你需要解压、构建并安装软件才能使用它。我将描述在下载、构建和安装基于源代码的软件包时通常遵循的步骤。

最后，我将简要描述如何在线更新你的 Linux 系统。你会发现，每个发行版都有自己用于在线更新的工具。

## 处理 RPM 文件

`RPM` 是一种系统，用于将软件产品所需的所有文件打包到一个单一文件中——称为 *RPM 文件*，或简称为 **RPM**。实际上，整个 Fedora Core 和 SUSE 发行版都是大量 RPM 的集合。处理 RPM 的最佳方式是通过 `RPM` 命令。你必须在终端窗口或文本控制台的 shell 提示符下输入这些命令。

在 Fedora Core 中，**RPM** 命令仅适用于你只需安装少量 **RPM** 文件的情况。如果要安装大量的 **RPM** 文件，你应该从桌面选择 **应用程序 → 添加/删除软件**。如果你从 CD 或 DVD 安装 **RPM** 文件，请先挂载 CD/DVD，然后输入 `system-cdinstall-helper /media/cdrom`。（如果你的 CD/DVD 挂载在另一个目录中，请用该目录名称替换 `/media/cdrom`。）这应该会弹出一个包管理窗口，你可以从中选择和安装成组的软件包。

### 使用 RPM 命令

当你安装基于 RPM 的发行版（如 Fedora Core）时，安装程序使用 `rpm` 命令解包软件包（**RPM** 文件）并将其内容复制到你的硬盘。

你不需要理解 **RPM** 文件的内部结构，但你需要知道如何使用 `rpm` 命令来处理 **RPM** 文件。以下是你可以使用 `rpm` 命令完成的一些操作：

- 查找已安装在系统上的 RPM 的版本号和其他信息。
- 从 **RPM** 安装新的软件包。例如，你可能需要安装初始安装时跳过的软件包。
- 删除（卸载）你之前从 **RPM** 安装的不再需要的软件。如果你发现很少（或从未）使用某个软件包，可以卸载它以回收磁盘空间。
- 用新版本升级旧版本的 **RPM**。例如，在 Fedora Core 中，你可以在从 Fedora Core 下载站点（在线列表位于 http://fedora.redhat.com/download/mirrors.html）下载软件包的新版本后进行升级。你必须升级 **RPM** 才能从新版本中的修复中受益。
- 验证 **RPM** 是否正常工作。你可以通过验证软件包来检查所有必要文件是否在正确的位置。

如你所见，`rpm` 命令功能强大——根据你使用的选项，它可以完成许多不同的事情。

如果你曾经忘记了 `rpm` 选项，输入以下命令即可查看列表：

```
rpm --help | more
```

**rpm** 选项的数量将会让你惊叹！

## 了解 RPM 文件名

RPM 包含许多文件，但在你的 Fedora Core 系统上，它表现为单个文件。按照惯例，RPM 文件名具有特定的格式。典型的 RPM 文件名看起来像这样：

```text
opennoffice.org-writer-1.9.104-2.i386.rpm
```

该文件名包含以下部分，前三部分由短横线 (`-`) 分隔：

- **软件包名称：** `openoffice.org-writer`
- **版本号：** `1.9.104`
- **发行版号：** `2`
- **架构：** `i386`（此软件包适用于 Intel 80x86 或 Pentium 兼容处理器）

通常，软件包名称的描述性足以让你猜测该 RPM 可能包含什么。版本号与当前软件包版本号相同（即使它以其他形式分发，例如 tar 文件）。开发人员分配发行版号以跟踪更改。对于要在配备 Intel x86 兼容处理器的 PC 上安装的 RPM，架构为 `i386` 或 `x86_64`。

## 查询 RPM

在安装软件包时，`rpm` 命令会构建已安装 RPM 的数据库。你可以使用 `rpm -q` 命令查询此数据库，以了解系统中已安装软件包的信息。

例如，要了解系统中已安装的 Linux 内核的版本号，请输入以下 `rpm -q` 命令：

```bash
rpm -q cups
```

你会看到类似以下内容的响应：



`cups-1.1.23-15`

响应是内核的 RPM 名称。（此版本是内核的可执行版本，而不是源代码文件。）该名称与 RPM 文件名相同，只是最后部分——`.i386.rpm`——未显示。在此情况下，RPM 的版本部分告诉你已安装 `cups`（通用 UNIX 打印系统）版本 1.1.23。

你可以使用以下命令查看所有已安装 RPM 的列表：

```bash
rpm -qa
```

你会看到一长串 RPM 列表滚动过屏幕。若要逐屏查看列表，请输入

```bash
rpm -qa | more
```

如果你想搜索特定的软件包，请将 `rpm -qa` 的输出传递给 `grep` 命令。例如，要查看所有名称中包含 `kernel` 的软件包，请输入

```bash
rpm -qa | grep kernel
```

结果取决于系统中安装了内核 RPM 的哪些部分。

使用 `rpm -q` 命令，你可以查询比软件包版本号多得多的内容。通过添加单字符选项，你可以了解其他有用信息。例如，尝试以下命令以查看 `cups` 软件包中的文件：

```bash
rpm -ql cups
```

以下是几种有用的 `rpm -q` 命令格式，用于查询软件包的信息。（若要使用这些 `rpm -q` 命令中的任何一个，请输入该命令，后跟软件包名称。）

- `rpm -qc`：列出软件包中的所有配置文件。
- `rpm -qd`：列出软件包中的所有文档文件。这些通常是在线手册页（也称为 man 页）。
- `rpm -qf`：显示指定文件所属的软件包名称（如果有）。
- `rpm -qi`：显示软件包的详细信息，包括版本号、大小、安装日期和简要描述。
- `rpm -ql`：列出软件包中的所有文件。对于某些软件包，你会看到非常长的列表。
- `rpm -qs`：列出软件包中所有文件的状态。（文件的状态可以是以下之一：正常、未安装或已被替换。）

![](img/792720823146d68f19fd50c99ebfce4b_477_0.png)

这些 `rpm` 命令仅提供已安装软件包的信息。如果你想查找未安装 RPM 文件的信息，请在每个命令的命令行选项后添加字母 `p`。例如，要查看名为 `rdist-6.1.5-792.1586.rpm` 的 RPM 文件中的文件列表，请转到该文件所在的目录并输入以下命令：

```bash
rpm -qpl rdist-*.rpm
```

当然，只有当前目录包含该 RPM 文件时，此命令才有效。

两个实用的 `rpm -q` 命令使你能够查明哪个 RPM 文件提供特定文件，以及哪些 RPM 需要指定软件包。要找出提供该文件的 RPM 的名称，请使用以下命令：

```bash
rpm -q --whatprovides filename
```

例如，要查看哪个 RPM 提供文件 `/etc/vsftpd.conf`，请输入

```bash
rpm -q --whatprovides /etc/vsftpd.conf
```

然后，RPM 将打印提供该文件的软件包的名称，如下所示：

```text
vsftpd-2.0.3-1
```

如果你提供的是软件包名称而不是文件名，RPM 将显示包含指定软件包的 RPM 软件包的名称。

另一方面，要找出需要特定软件包的 RPM 的名称，请使用以下命令：

```bash
rpm -q --whatrequires packagename
```

例如，要查看哪些软件包需要 `openssl` 软件包，请输入

```bash
rpm -q --whatrequires openssl
```

此命令的输出显示所有需要 `openssl` 软件包的 RPM 软件包。

## 安装 RPM

要安装 RPM，请使用 `rpm -i` 命令。你必须提供 RPM 文件的名称作为参数。如果你想查看 RPM 安装的进度，请使用 `rpm -ivh`。随着软件包被解包，会显示一系列井号 `#`。

例如，要从配套 DVD-ROM 安装 Fedora Core 的 `kernel-devel` RPM（包含 Linux 操作系统的头文件），我插入 DVD，挂载后，输入以下命令：

```bash
cd /media/cdrom/Fedora/RPMS
rpm -ivh kernel-devel*
```

你不需要输入完整的 RPM 文件名——你可以使用名称开头的几个字符，后跟一个星号 `*`。确保输入足够的名称以唯一识别该 RPM 文件。

如果你尝试安装已经安装的 RPM，`rpm -i` 命令将显示错误消息。例如，以下是我在系统中安装 man 软件包时输入以下命令所发生的情况：

```bash
rpm -i man-2*
```

我从 `rpm -i` 命令获得以下错误消息：

```text
package man-2.4.1-221 is already installed
```

若要强制 `rpm` 命令即使在存在错误的情况下也安装软件包，只需在 `rpm -i` 命令中添加 `--force`，如下所示：

```bash
rpm -i --force man-2*
```

### 删除 RPM

如果你意识到确实不需要该软件，你可能想要删除——即卸载——该软件包。例如，如果你已安装 X 窗口系统开发软件包，但发现你对编写 X 应用程序不感兴趣，你可以轻松使用 `rpm -e` 命令删除该软件包。

在你删除软件包之前，必须知道软件包的名称。查找名称的一种好方法是结合使用 `rpm -qa` 和 `grep` 来搜索适当的 RPM 文件。

例如，要删除名为 `qt3-devel` 的软件包，请输入

```bash
rpm -e qt3-devel
```

要删除 RPM，你不需要完整的 RPM 文件名；你只需要软件包名称——即文件名中版本号前的短横线 `-` 之前的第一部分内容。

`rpm -e` 命令不会删除其他软件包所需的软件包。

### 升级 RPM

使用 `rpm -U` 命令来升级 RPM。你必须提供包含新软件的 RPM 文件的名称。例如，如果我的系统上安装了版本 1.1.20 的 `cups`（打印系统），但我想升级到版本 1.1.23，我会从仓库下载 RPM 文件 `cups-1.1.23-i5.1386.rpm` 并使用以下命令：

```bash
rpm -U cups-1.1.23-i5.1386.rpm
```

`rpm` 命令通过删除旧版本的 `cups` 软件包并安装新的 RPM 来执行升级。

只要可能，请升级而不是删除旧软件包并安装新的软件包。升级会自动保存你旧的配置文件，从而免去了在重新安装后重新配置软件的麻烦。

当你升级包含可运行 Linux 内核的 `kernel` 软件包时，请使用 `rpm -i` 命令（而不是 `rpm -U` 命令）安装它。这样，你就不会覆盖当前内核。

## 验证 RPM

你可能不经常这样做，但如果你怀疑软件包未正确安装，请使用 `rpm -V` 命令进行验证。例如，要验证内核软件包，请输入以下内容：

```bash
rpm -V kernel
```

此命令使 `rpm` 将软件包中每个文件的大小和其他属性与原始文件的属性进行比较。如果所有验证均正确，`rpm -V` 命令不会打印任何内容。如果发现任何差异，你会看到相关报告。例如，我修改了 Apache `httpd` Web 服务器的配置文件。以下是我输入以验证 `httpd` 软件包的内容：

```bash
rpm -V httpd
```

以下是我得到的结果：

```text
S,5,...,T c /etc/httpd/conf/httpd.conf
```

在这种情况下，`rpm -V` 的输出告诉我配置文件已更改。此命令输出的每一行都有三个部分：

- 该行以八个字符开头：每个字符指示发现的差异类型。例如，`S` 表示大小不同，`T` 表示最后修改时间不同。表 4-1 显示了每个字符及其含义。句号表示该特定属性与原始属性匹配。
- 对于配置文件，旁边会出现 `c`；否则，此字段为空白。这就是你判断文件是否为配置文件的方法。通常，如果配置文件已更改，你不必担心；很可能是你自己做的更改。
- 该行的最后一部分是该文件的完整路径名。从这部分，你可以确切知道文件的位置。

## 处理 DEB 文件

带有 `.deb` 文件扩展名的 Debian 软件包将可执行文件与配置文件、在线文档和其他信息存储在一起。你可以使用 Debian 实用工具 `dpkg` 来解包和操作这些 DEB 文件，这是一个带有许多选项的命令行程序。此外，还有一个名为 `dselect` 的文本模式菜单驱动程序，可用于在不输入 `dpkg` 命令的情况下管理软件包。

![](img/792720823146d68f19fd50c99ebfce4b_481_0.png)



你通常使用一个名为 APT（高级打包工具）的高层实用工具来处理 Debian 中的软件包。例如，你可以直接使用 `apt-get` 命令来安装软件包，而不是下载 DEB 文件并用 `dpkg` 命令安装它。`apt-get` 命令甚至可以从在线 Debian 仓库下载软件包并将其安装到你的系统上。当你要查看从仓库手动下载的 DEB 文件的内容，或者查看可能位于 APT 缓存目录（在 Debian 中为 `/var/cache/apt/archives`）中的文件时，`dpkg` 命令仍然很有用。

我将在以下几节中向你介绍 `dpkg`、`dselect` 和 APT。

## 理解 DEB 文件名

典型的 DEB 软件包的文件名具有以下形式：

```
mozilla-firefox_1.0.4-2_i386.deb
```

文件名由下划线（`_`）分隔成三个部分：

- **软件包名称：** `mozilla-firefox`
- **版本和修订号：** `1.0.4-2`（版本由连字符分隔的两部分组成。第一部分是软件包维护者的版本号；第二部分是 Debian 修订号。）
- **架构：** `i386`（该软件包适用于 Intel x86 兼容系统。）

文件名的扩展名为 `.deb`，表明这是一个 DEB 文件。

## 使用 dpkg 命令

为了熟悉 `dpkg` 命令，请输入 `dpkg -help | more`。输出显示了 `dpkg` 接受的大量选项。你也可以输入 `man dpkg` 来阅读 `dpkg` 的在线手册页。

你可以使用 *dpkg* 对软件包执行大量操作，但你必须在终端窗口或文本控制台的 shell 提示符下工作。*dpkg* 命令的格式为：

```bash
dpkg [options] action package
```

其中包含零个或多个 `options`（选项），一个指示 `dpkg` 需要执行什么操作的 `action`（动作），以及 `package`（软件包）、DEB 文件或目录的名称（取决于 `action` 参数）。有时 `dpkg` 命令不需要任何软件包或文件名，只需要一个 `action`。

以下是你可以使用 `dpkg` 执行的一些操作示例：

- **安装** DEB 文件中的软件包，使用命令 `dpkg -i` `packagefile`，其中 `packagefile` 是 DEB 文件的名称（例如，`vsftpd-*.deb`）。
- **移除** 软件包但保留配置文件，使用命令 `dpkg -r` `packagename`，其中 `packagename` 是软件包的名称（例如，`vsftpd`）。
- **配置** 软件包，使用命令 `dpkg --configure` `packagename`，其中 `packagename` 是软件包的名称（例如，`vsftpd`）。
- **清除** — 移除所有内容，包括配置文件 — 使用命令 `dpkg -R` `packagename`，其中 `packagename` 是软件包的名称（例如，`vsftpd`）。
- **审计** 软件包（并查找系统中部分安装的软件包），使用命令 `dpkg -C`（不需要文件或软件包名称）。
- **列出 DEB 文件的内容**，使用命令 `dpkg -c` `packagefile`，其中 `packagefile` 是 DEB 文件的名称（例如，`vsftpd-*.deb`）。
- **查看** DEB 文件的信息，使用命令 `dpkg -I` `packagefile`，其中 `packagefile` 是 DEB 文件的名称（例如，`vsftpd-*.deb`）。
- **列出匹配模式的软件包**，使用命令 `dpkg -l` `pattern`，其中 `pattern` 是你想要匹配的软件包名称模式——通常带有通配符（例如，`kernel*`）。
- **查找包含特定文件的软件包**，使用命令 `dpkg -S` `pattern`，其中 `pattern` 是软件包包含的文件名模式——通常带有通配符（例如，`stdio*`）。
- **列出从软件包安装的文件**，使用命令 `dpkg -L` `packagename`，其中 `packagename` 是软件包的名称（例如，`vsftpd`）。

你可以在 Debian 系统或任何使用 DEB 软件包的系统中尝试这些命令。例如，要查找所有名称以 `mozilla` 开头的软件包，请在终端窗口中输入 `dpkg -l mozilla*`。以下是该命令在我的 Debian 系统上的相关输出部分：

```
||/ Name            Version                  Description
***===========================================
un  mozilla         <none>                   (no description available)
un  mozilla-bonobo  <none>                   (no description available)
ii  mozilla-browser 1.7.4-1                  The Mozilla Internet application suite - cor
ii  mozilla-firefox 1.0.4-2                  lightweight web browser based on Mozilla
```

第一列中的 `ii` 表示软件包已安装；`un` 表示软件包未安装。

`dpkg -l` 的另一个常见用途是列出所有软件包并使用 `grep` 查找匹配搜索字符串的行。例如，要查找包含 `kernel` 的任何内容，请输入 `dpkg -l | grep kernel`。如果软件包名称（在 `dpkg -l` 输出的第二列中）被截断，请使用类似以下命令调整输出行的宽度：

```
COLUMNS=132 dpkg -l | grep kernel
```

我发现 `dpkg -S` 命令是定位系统中提供特定文件的软件包的一种便捷方式。例如，如果我想弄清楚哪个软件包包含 `/etc/host.conf` 文件，我会输入 `dpkg -S /etc/host.conf`，输出显示 `base-files` 软件包包含 `/etc/host.conf`：

```
base-files: /etc/host.conf
```

## 介绍 dselect

`dselect` 实用工具旨在作为 `dpkg` 实用工具的前端。要尝试 `dselect`，请以 root 用户登录并在终端窗口（或文本控制台）中输入 `dselect`。当 `dselect` 启动时，你会看到 `dselect` 的文本模式菜单（如图中 4-1 所示）。

![](img/792720823146d68f19fd50c99ebfce4b_484_0.png)

**图 4-1：** 你可以使用 `dselect` 在 Debian 中管理软件包。

我 Won't 详细描述 `dselect`，但以下是你可以在 `dselect` 主菜单中执行的一些任务：

- 指定访问方法 — 如何查找 DEB 软件包
- 更新可用软件包列表
- 查看已安装和可用软件包的状态
- 选择软件包并管理软件包之间的依赖关系
- 安装新软件包或将现有软件包升级到较新版本
- 配置尚未配置的软件包
- 移除软件包

`dselect` 中一个常见的操作序列是更新可用软件包列表，然后升级所有有可用更新的软件包。当然，你也可以使用简单的 APT 命令执行相同的任务。

## 使用 APT 管理 DEB 软件包

APT 确实是一个用于保持你的 Debian 系统更新的高级实用工具。你可以使用一些 APT 实用工具来管理 DEB 软件包。两个常用的命令是 `apt-get` 和 `apt-cache`。

使用 `apt-get` 安装软件包时，只需输入 `apt-get install` `packagename`，其中 `packagename` 是你想要安装的软件包的名称。例如，要安装 `vsftpd` 软件包，请输入 `apt-get install vsftpd`。

移除软件包同样简单。输入 `apt-get remove` `packagename`，其中 `packagename` 是你想要移除的软件包的名称。

如果你想查找软件包的名称并且知道与该软件包相关的一些术语，可以使用 `apt-cache` 实用工具进行查找。例如，要查找 CD/DVD 刻录软件包，我输入 `apt-cache search burn` 以搜索 APT 的软件包缓存（这是 APT 从 `/etc/apt/sources.list` 文件中列出的服务器下载的 Debian 软件包列表）。以下是该命令的一些输出行：



```
arson - KDE frontend for burning CDs
burn - Command line Data-CD, Audio-CD, ISO-CD, Copy-CD writing tool
caca-utils - text mode graphics utilities
cdcontrol - A parallel burner that allow you to write to one or more CD-Writers at once
cdlabelgen - generates front cards and tray cards for CDs and DVDs
cdtoastster - Tcl/Tk front-end for burning cdrom
cdw - Tool for burning CD's - console version
cdw-common - Tool for burning CD's - common files
cdphum - a collection of programs to put heavy load on CPU
cdxdr - Chez Wam CD Ripper
dvd-rw-tools - DVD+RW/RW tools
dvdbackup - tool to rip DVD's from the command line
edcmath.app - Scientific calculator for GNUstep
gcdr - Tool for burning CD's - graphical version
gscdumst - GTX based CD mastering and burning program
... lines deleted ...
```

输出显示了我可以安装的多个潜在 CD/DVD 刻录程序。要了解任何软件包的更多详细信息，我输入 `apt-cache show` `packagename`，其中 `packagename` 是我想要获取信息的软件包名称。例如，要了解有关 `dvd-rw-tools` 软件包的更多信息，我输入 `apt-cache show dvd-rw-tools`，输出向我显示了该软件包的描述。然后我可以使用 `apt-get install` 安装该软件包。

![](img/792720823146d68f19fd50c99ebfce4b_485_0.png)

要搜索仅出现在软件包名称中的关键字，请使用 `--names-only` 选项，如下所示：`apt-cache search --names-only` `keyword`，其中 `keyword` 是出现在软件包名称中的内容。例如，如果我想要查找名称中包含 `selinux` 的软件包，我会输入 `apt-cache search --names-only selinux`。

## 从源文件构建软件包

许多开源软件包以源代码形式分发，不包含可执行二进制文件。在使用此类软件之前，你必须通过编译来构建可执行二进制文件，并且需要遵循一些说明来安装该软件包。在本节中，我将向你展示如何从源文件构建软件包。

### 下载和解压软件

通常，开源软件的源文件以压缩的 tar 归档文件形式分发。这些归档文件由 tar 程序创建，并使用 gzip 程序进行压缩。分发的形式是一个扩展名为 `.tar.gz` 或 `.tar.Z` 的大型单一文件——通常被称为压缩 tar 包。如果你需要该软件，就必须下载并解压这个压缩 tar 包。

使用匿名 FTP 或通过 Web 浏览器下载压缩 tar 文件。通常，除了点击链接并将文件保存到系统中的适当目录外，此过程不需要你做任何其他操作。

为了练习下载和构建软件包，你可以使用 X 多媒体系统（XMMS）——一个用于播放 MP3 和其他多媒体文件的图形化 X 应用程序——作为练习对象。XMMS 随 Fedora Core 一起捆绑，并且已经安装在你的系统上。然而，再次下载并重新构建 XMMS 包并不会带来任何危害。

从 [www.xmms.org/download.php](http://www.xmms.org/download.php) 下载 XMMS 的源文件。这些文件以压缩 tar 归档文件的形式打包。点击源文件的 http 链接，并将它们保存在 Linux 系统的 `/usr/local/src` 目录中。（请确保以 `root` 身份登录；否则你无法在 `/usr/local/src` 目录中保存文件。）

下载压缩 tar 文件后，使用以下 tar 命令检查其内容：

```bash
tar ztf xmms*.gz | more
```

你会看到一个类似以下的列表：

```text
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
... 省略几行 ...
```

该 tar 命令的输出显示了归档文件中的内容，并让你对解压归档文件后创建的目录有了一个大致的了解。在这种情况下，当前目录（在我的例子中是 `/usr/local/src`）下创建了一个名为 `xmms-1.2.10` 的目录。从列表中，你还可以得知编写该包所使用的编程语言。如果你看到 `.c` 和 `.h` 文件，则源文件使用的是 C 编程语言，许多开源软件包都是用这种语言编写的。

要解压压缩 tar 归档文件的内容，请输入以下 tar 命令：

```bash
tar zxvf xmms*.gz
```

你再次看到了从归档文件中解压并复制到硬盘上相应目录的文件长列表。

现在你准备好构建软件了。

## 从源文件构建软件

解压压缩 tar 归档文件后，所有源文件都位于一个目录中，该目录的名称通常就是软件包名称加上版本号后缀。例如，XMMS 版本 1.2.10 的源文件解压到 `xmms-1.2.10` 目录中。要开始构建软件，请使用以下命令更改目录：

```bash
cd xmms*
```

你不必输入完整的名称——shell 可以扩展目录名称并更改到 `xmms-1.2.10` 目录。

几乎所有软件包都附带某种 `README` 或 `INSTALL` 文件——这是一个告诉你如何构建和安装该包的文本文件。XMMS 也不例外；它附带一个 `README` 文件，你可以通过输入 `more README` 来浏览。`INSTALL` 文件包含构建和安装 XMMS 的说明。

![](img/792720823146d68f19fd50c99ebfce4b_488_0.png)

大多数开源软件包，包括 XMMS，还附带一个名为 `COPYING` 的文件。该文件包含 `GNU 通用公共许可证`（GPL）的全文，其中详细列出了你可以使用和重新分发该软件的条件。如果你对 GNU GPL 不熟悉，请阅读此文件，并将许可证出示给你的法律顾问，以进行完整解释并评估其对你业务的适用性。

要构建软件包，请遵循 `README` 或 `INSTALL` 文件中的说明。对于 XMMS 包，`README` 文件列出了某些先决条件（如库），并告诉你输入哪些命令来构建和安装包。对于 XMMS，说明告诉你使用以下步骤：

1. 输入 `./configure` 以运行一个 shell 脚本，该脚本检查你的系统配置并创建一个名为 `Makefile` 的文件——该文件被 `make` 命令用于构建和安装包。（你可以输入 `./configure --help` 来查看 `configure` 接受的一系列选项。）

   如果遇到关于缺少包的任何错误，你必须安装那些缺失的包。使用你的发行版的软件安装工具来添加缺失的包。例如，在 Debian 中使用 `apt-get install` 命令。在 Fedora Core 中，选择应用程序+添加/删除软件。在 SUSE 中，使用 YaST GUI 工具。

2. 输入 `make` 以构建软件。

   此步骤编译所有子目录中的源文件。（编译源代码会将每个源文件转换为目标文件——一个包含你的 PC 处理器能够理解的二进制指令的文件。）

3. 输入 `make install` 以安装软件。

   此步骤将库和可执行二进制文件复制到系统上的相应目录中。

虽然这些步骤是 XMMS 特有的，但大多数其他包都遵循这些步骤——`configure`、`make` 和 `install`。`configure` shell 脚本猜测与系统相关的变量，并创建一个包含构建和安装软件所需命令的 `Makefile`。

![](img/792720823146d68f19fd50c99ebfce4b_488_1.png)



![](img/792720823146d68f19fd50c99ebfce4b_489_0.png)

通常，除了输入构建软件的命令外，你不需要做任何其他事情，但你必须在系统上安装软件开发工具。在 Fedora Core 中，你必须安装开发工具和 GNOME 软件开发软件包。在 Debian 中，要构建和运行 XMMS，由于它是一个 X 应用程序，你还必须安装 X 软件开发软件包。

安装 XMMS 后，尝试在终端窗口中通过输入 `xmms` 从 GNOME 或 KDE 桌面运行它。在 XMMS 窗口中，按 L 键调出“加载文件”对话框。选择一个 MP3 文件进行播放。你的 PC 必须有一块声卡，并且声卡必须配置正确，XMMS 才能正常工作。

总而言之，以下是下载、解压、构建和安装典型软件包的步骤概述：

1. 使用 Web 浏览器从匿名 FTP 站点或网站下载源代码，通常形式为 `.tar.gz` 文件。
2. 使用 `tar zxvf filename` 命令解压文件。（如果压缩 tar 文件扩展名为 `.bz2`，这意味着该文件是使用 bzip2 压缩的，你可以使用 `tar jxvf filename` 命令解压该文件。）
3. 使用诸如 `cd software_dir` 之类的命令更改到软件解压后的新子目录。
4. 阅读任何 README 或 INSTALL 文件，了解你必须遵循以构建和安装软件的特定说明。
5. 构建软件的细节可能在不同的软件包之间略有不同，但通常你输入以下命令来构建和安装软件：

```bash
./configure
make
make install
```

6. 阅读随软件提供的其他文档，以了解如何使用该软件以及是否在使用前需要进一步配置该软件。

## 安装 SRPM

![](img/792720823146d68f19fd50c99ebfce4b_489_1.png)

如果你拥有 Fedora Core 的源 CD（你可以从 http://fedora.redhat.com/download/mirrors.html 上列出的站点之一下载源 CD 镜像），你可以安装源文件并直接从源文件构建各种应用程序。Fedora Core 的源代码文件也以 RPM 形式提供，就像可执行二进制文件一样，这些源代码 RPM 文件通常被称为 SRPM（source RPM 的缩写）。

### 在线更新 Linux 应用程序

要安装特定的源代码 RPM 并构建应用程序，请遵循以下步骤：

- 1. 通过键入 `mount /media/cdrom` 挂载 DVD-ROM，或者等待 GNOME 桌面自动挂载 DVD。
- 2. 通常，源代码 RPM 位于 SRPMS 目录中。键入以下命令切换到该目录：

```
cd /media/cdrom/SRPMS
```

- 3. 使用 `rpm -i` 命令安装源代码 RPM 文件。例如，要安装 Web 服务器（httpd）的源代码，请键入：

```
rpm -ivh httpd*.src.rpm
```

- 4. 使用带有 spec 文件的 `rpmbuild` 命令来构建软件。通过使用 `rpmbuild` 命令的不同选项，你可以执行不同的任务，从解包源文件到构建和安装二进制文件。例如，要处理整个 spec 文件，请键入：

```
rpmbuild -ba packagename.spec
```

文件会安装到 `/usr/src/redhat/SOURCES` 目录中。带有 `.spec` 扩展名的 spec 文件会被放置在 `/usr/src/redhat/SPECS` 目录中。spec 文件描述软件，并且包含用于构建和安装软件的信息。

此处 `packagename` 是 SRPM 的名称。此命令通常构建软件并安装二进制文件。

## 在线更新 Linux 应用程序

每个 Linux 发行版——Debian、Fedora Core、MEPIS、SUSE、Ubuntu 和 Xandros——都附带了允许你在线更新软件的实用工具。在接下来的章节中，我将概述 Debian、Fedora Core、MEPIS、SUSE、Ubuntu 和 Xandros 中的更新方法。

![](img/792720823146d68f19fd50c99ebfce4b_490_0.png)

你需要快速 Internet 连接（例如 DSL 或电缆调制解调器）才能轻松更新你的 Linux 应用程序或下载新的软件包。在尝试在线更新你的 Linux 系统之前，请确保你的 Internet 连接已正常运行。

### 使用 APT 保持 Debian、MEPIS 和 Ubuntu 更新

![](img/792720823146d68f19fd50c99ebfce4b_490_1.png)

保持你的 Debian 系统更新的最佳方法是使用 APT。更具体地说，你使用带有适当选项的 `apt-get` 命令行实用工具。由于 MEPIS 和 Ubuntu 基于 Debian，因此你也可以使用 APT 来更新 MEPIS 和 Ubuntu。

简而言之，假设在 Debian 安装期间已配置了 APT 源，你可以使用以下两个命令（按此顺序键入）来保持当前软件集合的更新：

```
apt-get update
apt-get upgrade
```

`apt-get update` 命令将当前的包列表与 `/etc/apt/sources.list` 文件中指定位置中可用的包进行核对，并收集关于已安装包的新版本的信息。

`apt-get upgrade` 命令实际上安装你的 Debian 系统中已安装的包的任何可用新版本。你必须执行 `apt-get upgrade` 来安装任何可用的升级。

![](img/792720823146d68f19fd50c99ebfce4b_491_0.png)

要在 Debian 中安装新包，请使用 `apt-cache search` 在 APT 的包缓存中找到包名称，然后使用 `apt-get install` 安装该包。

### 更新 Fedora Core 应用程序

![](img/792720823146d68f19fd50c99ebfce4b_491_1.png)

Fedora Core 附带 Up2date——一个图形化更新代理，它可以下载你的系统所需的任何新 RPM 文件并为你安装这些文件。Up2date 也被称为 Red Hat 更新代理，因为 Red Hat 为其 Red Hat Network 开发了它，通过该网络 Red Hat 为其商业客户提供服务。

要使用 Up2date 更新 Fedora Core 软件包，请遵循以下步骤：

- 1. **以 root 身份登录，并选择应用程序：系统工具：Red Hat Network。** 你也可以在终端窗口中键入 `up2date`。
  - （如果你在菜单中看不到 Red Hat Network，或者当你键入 `up2date` 时收到错误，请以 `root` 身份登录，在终端窗口中键入 `yum install up2*`，然后在菜单中寻找它。）更新代理启动，如果你第一次使用 Up2date，Red Hat Network 配置对话框将出现并引导你完成配置步骤。通常，你可以单击 **确定** 接受默认设置。然后，另一个对话框会提示你在你的 GPG 密钥环中安装一个公钥。（GPG 指 GNU 隐私保护或 GnuPG，一个使用 OpenPGP Internet 标准对电子邮件和其他数据进行加密、解密和签名的程序。）那个公共 GPG 密钥验证包开发者已安全签署了 Up2date 下载的包。如果提示，请单击 **是** 安装公钥。
- 2. **Up2date 显示一个带有欢迎信息的窗口。单击“下一步”按钮继续。**
- 3. **Up2date 显示其所谓的通道列表——代理从中下载包头信息库。单击“下一步”继续。**

默认情况下，更新代理使用与 Yum 配合工作的通道——Yum 是一个我在下一节中描述的命令行包更新/安装器。通道在文本配置文件 `/etc/sysconfig/rhn/sources` 中识别。除了 Yum，Up2date 还可以访问为 APT 准备的存储库——APT 是 Debian 中使用的先进打包工具。

单击“下一步”后，Up2date 确定需要更新的内容，并从指定的通道获取所有包头信息的列表。

- 4. **在 Up2date 下载包头信息后，它会显示包列表。你可以滚动浏览列表并选择你要更新的包：单击包名称左侧的框以选择它。单击“下一步”继续。**

然后，Up2date 检查任何包依赖关系并开始下载包。进度条显示下载状态。

- 5. **下载完成后，单击“下一步”按钮以继续安装。**
- 6. **Up2date 在安装每个包更新时显示进度条。安装完成后，单击“下一步”按钮。**

Up2date 显示关于成功安装的包的消息。

- 7. **单击“完成”按钮退出 Up2date。**

![](img/792720823146d68f19fd50c99ebfce4b_492_0.png)



Fedora Core 5 附带另一个名为包更新器的图形实用工具，你可以使用它来更新安装在你的 Fedora Core 系统上的软件包。要启动包更新器，请选择 *应用程序 > 系统工具 > 软件更新器*，或者在终端窗口中键入 `su -` 成为 *root*，然后键入 `pup`。

在 Fedora Core 中，你也可以使用 Yum（顺便说一句，这代表 Yellow dog Updater, Modified）。Yum 是一个用于更新以及安装和删除 RPM 包的命令行实用工具。Yum 从指定的网站下载 RPM 包头信息，并使用 `rpm` 实用工具确定包之间的相互依赖关系以及系统需要安装的内容。然后它下载并使用 `rpm` 安装必要的包。Yum 只下载头信息来完成其工作，头信息的尺寸远小于完整的 RPM 包。Yum 比替代方案快得多，后者是使用 `rpm` 命令手动下载完整的 RPM 包。

通常，你会使用图形化更新代理来保持系统最新，因为它易于使用。然而，知道如何从命令行运行 Yum 是很好的，以防更新代理出现问题。

你可以访问 Yum 网页 http://linux.duke.edu/projects/yum 来阅读更多关于 Yum 的内容并关注 Yum 新闻。

Yum 的命令行具有以下语法：

`yum [options] command [packagenames]`

`options` 是 Yum 选项列表，`command` 指定你希望 Yum 执行的操作，`packagenames` 是 Yum 执行该操作的包的名称。你必须提供命令，但 `options` 和 `packagenames` 是可选的。这就是为什么我在语法中用方括号显示它们。表 4-2 总结了 Yum 命令，表 4-3 列出了一些常见的 Yum 选项。

| 表 4-2：Yum 命令 | |

| :--- | :--- |

| **命令** | **Yum 为此命令执行的操作** |

| check-update | 检查系统可用的更新 |

| clean | 清理缓存目录 |

| info | 显示指定包的摘要信息 |

| install | 安装指定包的最新版本，确保满足所有依赖关系 |

| list | 列出关于可用包的信息 |

| provides | 提供关于哪个包提供文件的信息 |

| remove | 删除指定的包以及依赖于被删除包的包 |

| search | 查找包头信息中包含你指定的包名称的包 |

| update | 更新指定的包，确保满足所有依赖关系 |

| 表 4-3：一些常见的 Yum 选项 | |

| :--- | :--- |

| **选项** | **促使 Yum 执行以下操作** |

| --download-only | 下载包，但不安装它们 |

| --exclude=pkgname | 排除指定的包。（你可以在命令行中多次使用此选项。） |

| --help | 显示帮助消息并退出 |

| --installroot=path | 使用指定的路径名作为安装所有包的目录 |

| -y | 假设你对任何问题的回答都是“是” |

如果你只是想使用 Yum 更新你的系统，只需输入以下命令。（你必须以 `root` 身份登录。）

```
yum update
```

Yum 会读取其配置文件 `/etc/yum.conf`，并执行更新系统上已安装软件包所需的所有操作。

你可以指定软件包名称，以仅更新部分软件包。例如，若要更新 kernel 和 xorg-x11 软件包，请使用以下 Yum 命令：

```
yum update kernel* xorg-x11*
```

此命令将更新所有名称以 `kernel` 和 `xorg-x11` 开头的软件包。

你可以使用选项进一步指示 Yum 执行的操作。例如，如果你想要下载更新的软件包但不安装它们，请输入：

```
yum --download-only update
```

另一个常见的选项是 `--exclude`，它允许你从更新过程中排除一个或多个软件包。假设你要更新除了 GNOME 软件包（其名称以 `gnome` 开头）和 `rhythmbox` 软件包以外的所有内容。那么你需要输入以下 Yum 命令：

```
yum --exclude=gnome* --exclude=rhythmbox update
```

## 在线更新 SUSE

![](img/792720823146d68f19fd50c99ebfce4b_494_0.png)

SUSE 配备了 YOU——YaST 在线更新工具，用于在线软件更新。要访问 YOU，请选择主菜单→系统→YaST，然后在 YaST 控制中心的软件类别中，单击在线更新。这将调出 YaST 在线更新窗口，如图 4-2 所示。

要设置 YOU 自动更新，请单击“配置完全自动更新”按钮。然后，你可以指定一天中希望 YOU 下载并安装任何可用补丁的时间。如果你愿意，也可以指定 YOU 仅下载补丁而不安装它们。

要在线更新你的 SUSE 系统，请选择安装源并单击“下一步”。（参见图 4-2。）然后 YOU 会下载补丁列表并显示它们，如图 4-3 所示。

**图 4-2：** 你可以使用 YaST 在线更新来保持 SUSE 系统处于最新状态。

![](img/792720823146d68f19fd50c99ebfce4b_495_0.png)

**图 4-3：** 选择 YOU 补丁并单击 **接受** 以安装它们。

![](img/792720823146d68f19fd50c99ebfce4b_495_1.png)

选择补丁（部分已被推荐并预先为你选中）并单击 **接受**。然后 YOU 将下载所需的软件包并在你的 SUSE 系统上安装它们。

## 使用 Xandros 网络

在 Xandros 中，使用 Xandros 网络来更新应用程序或安装新的应用程序。选择主菜单：Xandros 网络（或双击桌面上的 Xandros 网络图标）以打开 Xandros 网络窗口，如图 4-4 所示。

![](img/792720823146d68f19fd50c99ebfce4b_496_0.png)

要安装来自 Xandros 的最新更新，请选择“文件：安装来自 Xandros 的所有最新更新”，或单击“更新”按钮（位于图 4-4 顶部工具栏上钥匙图标的左侧）。然后 Xandros 网络将下载有关可用更新的信息，并显示一个摘要（参见图 4-5），列出将要下载的软件包及安装它们所需的磁盘空间。

![](img/792720823146d68f19fd50c99ebfce4b_496_1.png)

![](img/792720823146d68f19fd50c99ebfce4b_497_0.png)

单击“确定”。Xandros 网络会提示你输入 `root` 密码，在你输入 `root` 密码后，它将下载软件更新并安装它们。

在幕后，Xandros 网络使用 Debian 的 `apt-get` 命令来下载和安装软件更新。

![](img/792720823146d68f19fd50c99ebfce4b_497_1.png)

Xandros 网络窗口还提供安装新软件的选项。你甚至可以通过 Xandros 网络购买新的应用程序。如果你有要安装的 RPM 或 DEB 文件，你可以通过选择“文件>安装 RPM 文件”或“文件>安装 DEB 文件”在 Xandros 网络中进行安装。

# 第 5 章：定制 Linux 内核

### 本章内容

- 配置内核
- 构建新的内核及其模块
- 安装模块
- 构建并安装新的初始 RAM 磁盘文件
- 安装内核并设置 GRUB

Linux 令人兴奋的众多原因之一是许多程序员不断对其进行改进。例如，一些程序员编写驱动程序以添加对新硬件的支持，如新的声卡或新的网卡。所有这些创新都以 Linux 内核新版本的形式呈现给你。

尽管你不必每次有新版本可用时都升级或修改 Linux 操作系统——内核——，但有时你必须升级，因为新版本修复了某些问题或更好地支持你的硬件。另一方面，如果较早的内核版本已包含你所需要的一切，你就不必急于升级。

有时，即使内核没有任何修复或增强，你可能也想要重新构建内核。附赠 DVD-ROM 上的 Linux 内核是通用的，并使用模块来支持所有类型的硬件。你可能希望构建一个新的内核，该内核将——整合到内核的二进制文件中——仅支持安装在你的系统中的设备的驱动程序。特别是，如果你有 SCSI 硬盘，你可能希望创建一个支持你的 SCSI 适配器的内核。根据你的需求，你可能还希望更改一些内核配置选项，例如创建一个专用于你的处理器（而非通用 Intel 386 处理器）的内核。

在本章中，我将解释如何重新构建和安装新的 Linux 内核。

### 重新构建内核

重新构建内核是指为 Linux 核心操作系统创建一个新的二进制文件。这个二进制文件是在 Linux 启动时运行的文件。

你可能想知道为什么要重新构建内核。嗯，以下是一些原因：



在你最初安装 Linux 后，你可能希望创建一个新内核，该内核仅包含对你系统中已安装硬件的支持。特别是，如果你有一个 SCSI 适配器，你可能希望创建一个将 SCSI 驱动程序链接在内的内核。附赠 DVD-ROM 上的内核将 SCSI 驱动程序包含为外部模块，由内核在启动时加载。

如果你的系统拥有仅提供实验性支持的硬件，你必须重新构建内核以将该支持整合到操作系统中。

你可能希望重新编译内核并生成在你的特定 Pentium 处理器上运行良好的代码，而非大多数 Linux 发行版中通用的 386 处理器代码。

![](img/792720823146d68f19fd50c99ebfce4b_499_0.png)

要重新构建 Linux 内核，你需要内核源文件。内核源文件通常不会安装。请使用你的发行版的软件安装工具来安装内核源软件包。

![](img/792720823146d68f19fd50c99ebfce4b_499_1.png)

Fedora Core 不提供内核源软件包。相反，你必须安装源 RPM 文件 `kernel-version.src.rpm`，其中 `version` 是内核版本号。你可以在 Fedora Core 在线存储库的 SRPMS 目录中找到内核 SRPM。你必须使用命令 `rpm -Uvh kernel-version.src.rpm` 安装内核 SRPM。然后输入 `cd /usr/src/redhat/SPECS`，接着输入 `rpmbuild -bp --target $(arch) kernel.spec`。为了使内核源文件在 `/usr/src/linux` 目录中可用，请输入以下命令。将 `version` 替换为通过 `uname -r` 命令获取的内核版本号。

```
cd /usr/src/redhat/BUILD/kernel-VERSION/usr/src/
mv linux-VERSION /usr/src/
cd /usr/src/
ln -s ./linux-VERSION linux
```

![](img/792720823146d68f19fd50c99ebfce4b_499_2.png)

在 SUSE 中，使用 YaST 的软件管理工具来安装内核源——要找到它，请使用 YaST 软件安装窗口中的搜索功能，搜索 `kernel-source`。安装内核源软件包后，源文件将出现在 `/usr/src/linux-version` 目录中，其中 `version` 是内核的版本号。因此，对于内核版本 `2.6.13`，源文件位于 `/usr/src/linux-2.6.13` 目录中。一些发行版会自动将 `/usr/src/linux` 设置为指向包含 Linux 内核源文件的特定版本目录的符号链接。

## 重新构建内核

基于 Debian 的发行版中，内核源代码安装在 `/usr/src/kernel-source-version` 目录中，其中 `version` 表示内核版本。因此，对于内核版本 `2.6.11`，源代码位于 `/usr/src/kernel-source-2.6.11`。要在 Debian 中切换到内核源代码目录，请输入 `cd /usr/src/kernel-source*`。

构建内核包括以下几个阶段：

- 配置内核
- 构建内核
- 构建并安装模块
- 构建新的初始 RAM 磁盘 `initrd` 文件
- 安装内核并设置 GRUB

我将在接下来的几部分中解释这些阶段，但首先你需要了解将驱动链接进内核与将驱动构建为可加载模块之间的区别。

## 创建单体式内核与模块化内核

对于支持 Linux 中各种硬件设备所需的设备驱动程序，你有两种选择：

- **链接支持：** 你可以将系统上所有硬件的驱动链接到内核中。随着设备驱动程序代码被整合进内核，内核的大小会增加。将所有必要代码链接在一起的内核被称为*单体内核*，因为它是一个大的文件。
- **使用模块：** 你可以将设备驱动程序创建为可加载内核模块的形式。*模块*是一组代码，内核在开始运行后就可以加载它。使用模块的典型场景是在支持新设备时，无需为每个新设备重新构建内核。模块并不一定是设备驱动程序；它们也可以为内核添加新的功能。使用模块的内核被称为*模块化内核*。

你不必创建一个完全单体式或完全模块化的内核。实际上，将部分支持直接链接到内核中，而将不常用的设备驱动程序构建为模块的形式，这是一种常见的做法。对于 Linux 发行版来说，包含一个主要由模块组成的内核是有意义的，同时配备大量可以支持许多不同类型硬件的模块。然后，Linux 安装程序会配置系统，使其仅加载支持用户系统中已安装硬件所需的模块。

当你为你的硬件配置创建自定义内核时，你可能希望将所有必需的设备驱动程序链接到内核中。你仍然可以控制这种单体内核的大小，因为只链接你系统上安装的特定硬件组合的设备驱动程序。

## 配置内核

重新构建内核的第一步是配置它。要配置内核，请以 `root` 身份登录。然后使用 `cd` 命令更改内核源代码目录，如下所示：

```
cd /usr/src/linux*
```

要配置内核，你必须指明希望在你的 Linux 内核中包含哪些特性和设备驱动程序。本质上，你构建了一个仅包含你所需要特性的你自己的 Linux 内核版本。

Linux 提供了几种配置内核的方法：

- 输入 `make menuconfig` 通过类似文本模式 Linux 安装程序所使用的基于文本的界面输入内核配置参数。
- 输入 `make xconfig` 使用基于 X Window 系统的配置程序来配置内核。你需要运行 X 才能使用这个具有图形界面的配置程序。你还必须安装 Qt 开发 `qt-devel` 包，并将 `QTDIR` 环境变量设置为 Qt 安装的目录。如果你已安装 `qt-devel` 包，请输入 `export QTDIR=/usr/lib/qt-3.3` 以正确定义 `QTDIR`。
- 输入 `make config` 使用一个 shell 脚本，逐个询问每个配置选项。你可以从 Linux 命令提示符使用此配置程序。使用此选项时，你需要经历一个较长的问答过程来指定配置参数。对于每个问题，输入 `y` 将支持链接到内核，输入 `m` 构建模块，输入 `n` 跳过对该特定设备的支持。
- 输入 `make oldconfig` 使用 shell 脚本在升级源代码后重新配置内核。此配置脚本保留现有选项，并只提示你输入新增或更改的选项。

`make menuconfig`、`make xconfig`、`make config` 和 `make oldconfig` 命令达到相同的结果——每个命令都将你的选择存储在位于 `/usr/src/linux*` 目录中名为 `.config` 的文本文件中。由于文件名以句点开头，仅使用 `ls` 命令列出目录时你看不到它。相反，输入 `ls -a` 即可在目录列表中看到 `.config` 文件。

内核配置步骤仅仅是将你的选择捕获在 `.config` 文件中。事实上，直到你第一次配置内核之前，`.config` 文件并不存在。在使用 `make` 命令编译内核之前，内核文件不会改变。这意味着你可以任意多次执行内核配置选项。如果你希望从默认设置重新开始，请在开始配置内核之前输入以下命令：

```
make mrproper
```

若要查看你可以使用 `make` 命令执行的内核配置构建步骤概述，请在终端窗口中输入以下内容，在输入 `cd /usr/src/linux*` 将当前目录更改到正确位置之后：

```
make help | more
```

在开始重新配置内核之前，先看一下典型的 `.config` 文件。例如，以下是在我配置内核后在 Linux 系统上输入 `more .config` 时输出的一些行：

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

基本上，每个配置选项都有一个名称，并且每个选项都被赋予一个值。名称以 `CONFIG_` 开头，后跟一个标识该选项的单词。每个被选中的选项的值为 `y` 将该特性的支持链接到内核或 `n` 为该特性使用模块。以 `#` 开头的行是注释。注释行列出了未选中的特性。



我通过 `make config` 命令描述配置过程。虽然这种方法有点繁琐，因为它会让你逐个通过每个选项，但它是一个理想的学习工具。当你逐步通过配置选项组时，我提供了注释，解释大多数选项的含义。然后你可以使用最喜欢的配置工具（`make xconfig`、`make menuconfig`、`make config` 或 `make oldconfig`）来配置内核。

当你使用 `make config` 命令配置内核时，你必须选择如何包含对特定设备的支持。通常，对于每个配置选项，你必须从以下选项中选择一个进行响应：

- `y` 将支持链接到内核
- `m` 使用模块
- `n` 跳过对该特定设备或特性的支持
- `?` 获取关于该内核配置选项的帮助

如果设备没有模块化设备驱动程序，你将看不到 `m` 选项。对于某些配置选项，你可能需要从列表中选择一个数字。

## 开始内核配置

要开始配置内核，请以 root 身份登录，更改到 Linux 内核源代码目录（根据你的发行版输入 `cd /usr/src/linux*` 或 `cd /usr/src/kernel-source*`），并在终端窗口中输入 `make menuconfig`。然后配置工具显示第一个提示：

```
.
* Linux Kernel Configuration
.
.
.
* Code maturity level options
```

提示开发中和/或不完整的代码/驱动程序（EXPERIMENTAL） [y/n/?]

按 Enter 键接受默认的是答案。这将使配置过程显示所有实验性设备驱动程序。

每个提示的可能答案显示在方括号中，默认答案为大写。因此，[Y/n/?] 表示默认答案是是，另外两个可能的答案是 n 和 ?。要接受默认值，请按 Enter。要获取该选项的帮助，请按 ?。如果你对任何选项有疑问，请按 ?，并在决定怎么做之前仔细阅读帮助文本。你可以使用此一般准则来做出选择。在以下部分中，我只解释选定的内核配置选项组。

## 常规设置选项

这组选项允许您指示是否要启用对一般功能的支持，例如 System V 进程间通信（IPC）、基于 BSD（Berkeley Software Distribution）UNIX 的进程会计，以及热插拔设备。您可以按 Enter 键接受默认选择。

## 可加载模块支持

这组选项询问您是否支持可加载模块。可加载模块是一组代码，Linux 内核可以加载并执行该代码，就好像它是操作系统的一部分一样。

### 可加载模块支持

- 启用可加载模块支持 (`MODULES`) [Y/n/?]
- 模块卸载 (`MODULE_UNLOAD`) [Y/n/?]
- 强制模块卸载 (`MODULE_FORCE_UNLOAD`) [N/y/?]
- 模块版本支持 (EXPERIMENTAL) (`MODVERSIONS`) [Y/n/?]
- 所有模块的源校验和 (`MODULE_SCKVERSION_ALL`) [Y/n/?]
- 模块签名验证 (EXPERIMENTAL) (`MODULE_SIG`) [Y/n/?]
- 必需的模块必须有效签名 (EXPERIMENTAL) (`MODULE_SIG_FORCE`) [N/y/?]
- 自动内核模块加载 (`KMOD`) [Y/n/?]

如果您希望包含对模块的支持，则对第一个问题回答 Yes（是），并接受其他问题的默认设置。请注意，有些选项被标记为 EXPERIMENTAL（实验性）。只有当您在配置会话的开头启用了实验性代码支持时，这些问题才会出现。

## 处理器类型和功能

这组选项用于设置子体系结构类型、处理器系列以及对特定处理器相关功能的支持：

### 处理器类型和功能

**子体系结构类型**

1. PC 兼容 (`X86_PC`)
2. AMD Elan (`X86_ELAN`)
3. Voyager (NCR) (`X86_VOYAGER`)
4. NUMAQ (IBM/Sequent) (`X86_NUMAQ`)
5. SGI 320/540 (Visual Workstation) (`X86_VISWS`)

`choice[1-5]`:

子体系结构类型选项使您能够从不同的基本系统设计类型中进行选择，这些设计都利用了 Intel x86 处理器系列，但可能与众所周知的 PC 兼容机器存在根本差异。在 2.6 版本之前，Linux 内核隐含地假设系统体系结构基于旧的 IBM PC/AT 系列。从内核版本 2.6 开始，您可以为其他类型的基于 Intel x86 的体系结构构建内核，例如 SGI 图形工作站和非均匀内存访问（NUMA）多处理器系统。您可能可以默认选择 PC 兼容子体系结构，但如果需要为其他类型的基于 x86 的系统构建内核，其他选项也可以使用。

下一组选项提示您选择处理器系列：

1. 386 (`M386`)
2. 486 (`M486`)
3. 586/ES/5x86/6x86/6x86MX (`M586`)
4. Pentium-Classics (`M586TSC`)
5. Pentium-MDX (`M586MX`)
6. Pentium-Pro (`M686`)
7. Pentium-II/Celeron (pre-Coppermine) (`MPENTIUMII`)
8. Pentium-III/Celeron (Coppermine) / Pentium-III Xeon (`MPENTIUMIII`)
9. Pentium M (`MPENTIUMM`)
10. Pentium-4/Celeron (P4-based) / Pentium-4 M/Xeon (`MPENTIUM4`)
11. K6 / K6-II / K6-III (`MK6`)
12. Athlon/Duron/K7 (`MK7`)
13. Opteron/Athlon64/Hammer/K8 (`MK8`)
14. Crusoe (`MCRUSOE`)
15. Efficeon (`MEFFICEON`)
16. Winchip-C6 (`MWINCHIP6`)
17. Winchip-2 (`MWINCHIP2`)
18. Winchip-2A/Winchip-3 (`MWINCHIP3`)
19. MediaGX/MXGede (`MGEDEX`)
20. CrixII/III/IVA-C3 (`MCYRIXIII`)
21. VIA C3-2 (Nehemiah) (`MVIA C3_2`)

如果您选择 386，编译后的内核可以在任何其他处理器上运行（例如 486 或任何类型的 Pentium）。但是，如果您正在专门为系统处理器创建内核，请从列表中选择您的处理器类型。

后续的选项提示您设置许多其他处理器相关选项，您可以将这些选项保留为默认设置。如有疑问，您可以通过按 `?` 键阅读每个选项的帮助，并选择适用于您系统的选项。

## 电源管理选项

这组选项涉及系统电源管理，包括高级配置和电源接口（ACPI）、高级电源管理（APM）BIOS 支持以及 CPU 频率缩放。您可以简单地接受这些选项的默认设置。如果您不了解某个选项的含义，请按 `?` 键获取该选项的帮助。

## 总线选项

这些选项询问您是否支持特定总线：PCI、ISA、EISA、MCA 和 PCMCIA。行业标准架构（ISA）总线曾经是最广泛使用的总线（直到 PCI 总线出现之前）；这种总线用于最初的 IBM PC-AT。微型通道架构（MCA）总线是 IBM 的专有总线，最早出现在 PS/2 PC 中。IBM 设计这种总线作为高速总线，但其专有性质使其在 PC 中未得到广泛使用。扩展行业标准架构（EISA）总线作为 MCA 总线的替代方案而出现，性能与 MCA 相当。由于 EISA 总线外围卡比其 ISA 总线对应产品更昂贵，因此 EISA 总线未得到广泛使用。外围部件互连（PCI）总线是最新的高性能总线；当前的 PC 使用 PCI 总线，但同时也提供 ISA 总线插槽，以便您可以继续使用 ISA 卡。

PCMCIA 代表个人计算机内存卡国际协会，这是一个非营利组织，为向笔记本电脑添加内存卡制定了标准接口。尽管最初是为内存卡设计的，但 PCMCIA 设备成为笔记本电脑各种附加设备的热门选择。PCMCIA 设备被称为 PC 卡，而 CardBus 一词指的是 PC 卡的电气规范。

通常，您希望内置对 PCI 和 ISA 的支持，并为 PCMCIA 支持构建模块。如果您的系统支持在系统通电并运行时添加或移除 PCI 卡，您还可以添加对 PCI 热插拔的支持。

## 可执行文件格式

开启对可执行与链接格式（ELF）的支持，这是 Linux 中可执行文件和库的标准格式。在 ELF 之前，可执行文件的格式称为 `$a.out$`（基于 C 编译器生成的可执行文件的默认名称）。在内核版本 2.6 中，您可以构建一个模块来支持旧的 `$a.out$` 格式。

## 内存技术设备

此类别选项为驻留在内存技术设备上的文件系统提供支持，例如闪存和随机存取内存。这些文件系统常用于嵌入式设备。此类别包含许多选项，用于构建支持各种内存设备的内核模块。构建这些模块没有害处，因为如果您的计算机没有相应的内存设备，它们不会被加载。

## 并行端口支持



如果您使用连接到 PC 并行端口的设备，例如打印机或并行 Zip 驱动器，这些选项非常重要。对并行端口支持和 PC 式硬件选项回答 `m`，以便将驱动程序作为模块构建。

## 即插即用支持

这些选项询问您是否要在内核中启用即插即用（PnP）支持。如果您启用 PnP 支持，内核会自动配置 PnP 设备（正如 Windows 所做的那样）。请启用这些选项。

## 块设备

块设备（如磁盘驱动器）以数据块的形式传输数据（与键盘不同，键盘一次传输一个字符）。这组选项涉及连接到 PC 并行端口的软盘和 IDE（集成硬盘电子电路）设备，以及其他块设备。

- 普通软盘支持 (`BLK_DEV_FD`) `[M/n/y/?]`
- XT 硬盘支持 (`BLK_DEV_XD`) `[N/m/y/?]`
- 并行端口 IDE 设备支持 (`PARIDE`) `[M/n/?]`

第一个问题询问您是否需要软驱支持。由于大多数 PC 都有软驱，您的回答通常应该是 Yes（是）。如果您的外部 CD-ROM 或磁盘设备通过 PC 的并行端口连接，您应按 Enter 键接受第三个问题的默认设置。某些 IDE 设备使用并行端口 IDE 适配器——这就是 `PARIDE` 选项所指的内容。

下一组选项用于各种并行 IDE 驱动程序。您可能希望通过可加载模块为并行端口 IDE 设备构建支持。这样，如果您需要，模块就在那里，但内核不会因为额外的代码而变得臃肿。

接下来是另一组块设备的选项。`BLK_DEV_LOOP` 选项用于回环设备。启用回环设备允许 Linux 内核操纵存储在单个大文件中的整个文件系统映像。如果您想要挂载 CD 或 DVD 映像（例如 Linux ISO 文件）并在实际刻录 CD 或 DVD 之前进行检查，此选项非常有用。

RAM 磁盘支持允许内核使用系统内存的一部分作为能够存储文件系统的磁盘。通常，RAM 磁盘仅在系统启动期间起作用，此时硬盘可能不可用

然而。如果你正在启动 SCSI 磁盘且未将 SCSI 驱动程序编译到内核中，那么 RAM 磁盘是必需的。

## ATA/ATAPI/MFM/RLL 支持

下一组问题涉及 IDE 设备，例如硬盘和 ATAPI CD-ROM 驱动器。

- ATA/ATAPI/MFM/RLL 支持
- ATA/ATAPI/MFM/RLM/RLL 支持 (IDE) `[M/n/y/?]`
- 增强型 IDE/MFM/RLL 磁盘/CD-ROM/磁带/软驱支持 (`BLK_DEV_IDE`) `[M/n/y/?]`

在配置操作系统时，你必须习惯大量的缩略词——这里就有四个：`ATA`、`ATAPI`、`MFM` 和 `RLL`。它们都涉及硬盘或连接磁盘驱动器与 PC 的接口。以下是它们的含义：

- `ATA` 代表 AT Attachment（AT 附加），指连接硬盘和 CD-ROM 驱动器到 PC 主板的 PC-AT 风格接口。
- `ATAPI` 代表 AT Attachment Packet Interface（AT 附加数据包接口），指最初将磁盘控制器集成在硬盘驱动器本身上的 PC 硬盘。这种接口过去被称为 Integrated Drive Electronics（集成驱动器电子学），即 IDE。你通常会看到 IDE、`ATA` 和 `ATAPI` 这些术语互换使用。
- `MFM` 代表 Modified Frequency Modulation（调制频率调制），这是旧式硬盘上数据编码的方式。这些硬盘可以通过 IDE 接口工作。
- `RLL` 代表 Run Length Limited（游程有限），是 PC 早期在硬盘上存储数据的一种旧技术。`RLL` 磁盘可以通过 IDE 接口工作。

第一个问题询问你是否希望内核支持 IDE 设备。第二个问题询问你是否希望使用功能齐全的 IDE 设备，该设备可控制多达十个 IDE 接口。由于每个 IDE 接口可以有一个主设备和一个从设备，这使得 Linux 可以访问总共多达 20 个 IDE 设备，如磁盘或 CD-ROM 驱动器。你可以按 Enter 键接受这两个选项的默认选择，即作为模块。

下一组选项涉及各种 IDE 驱动程序。你可以接受这些选项的默认答案。请注意，IDE/ATAPI FLOPPY 指的是 IDE 软驱，如 Iomega Zip 驱动器或 IOMEGA Superdisk LS-120 驱动器。关于 CMD640 和 RZ1000 错误修复的问题涉及用于 IDE 接口的特定芯片组的一些已知问题。

## SCSI 设备支持

这组选项与 SCSI 设备有关。`SCSI` 代表 Small Computer Systems Interface（小型计算机系统接口）——这是一种可以连接多个设备（如硬盘和扫描仪）到 PC 的接口类型。如果你的系统有 SCSI 适配器，你应该首先对 `SCSI` 选项回答 Yes（是）。之后，你需要回答关于连接到 SCSI 适配器的设备类型（磁盘、磁带、CD-ROM）的问题。最后，你必须启用系统中特定 SCSI 适配器型号的支持。

## IEEE 1394 (FireWire) 支持

下一组选项用于启用 IEEE 1394 支持，无论是作为模块还是链接到内核。IEEE 1394 是一种连接外设到 PC 的高速串行总线。苹果称此总线为 FireWire；索尼称其为 iLink。IEEE 1394 类似于 USB，但它可以以高达 400 Mbps 的速率传输数据，这比旧版 USB 1.1 的数据传输速率快 30 多倍。（请注意 USB 2.0 快得多；它可以以高达 480 Mbps 的速率传输数据。）由于其高速数据传输率，IEEE 1394 非常适合将高速外设（如数字音频和视频设备以及外部硬盘）连接到 PC。

目前，Linux 支持与 Texas Instruments PCI/lynx/PCILynx2 兼容的 IEEE 1394 芯片组以及 OHCI 芯片组。如果你的 PC 有 IEEE 1394 适配器，你可以通过这些选项构建必要的驱动程序。

- IEEE 1394 (*Firewire*) 支持
- IEEE 1394 (*Firewire*) 支持 (`IEEE1394`) `[M/n/y/?]`

![](img/792720823146d68f19fd50c99ebfce4b_509_0.png)

要了解有关在 Linux 中使用 IEEE 1394 外设的更多信息，请访问 `www.linux1394.org` 上的 IEEE 1394 for Linux 项目网站。

## I2O 设备支持

读作 *eye-two-OH*，`I2O` 指的是 Intelligent Input/Output（智能输入/输出）——一种独立于操作系统和被控设备的新设备驱动程序架构。`I2O` 通过逻辑上分离负责管理设备的部分和包含操作系统特定细节的部分来工作。（驱动程序功能的逻辑分离称为 *I2O Split Driver model*（I2O 分拆驱动器模型）。）`I2O` 驱动程序的这两个部分是 OS Services Module（OSM，操作系统服务模块），它与操作系统协同工作，以及 Hardware Device Module（HDM，硬件设备模块），它与驱动程序管理的特定接口设备交互。OSM 和 HDM 通过相互传递消息进行通信。

Linux 附带了一些用于 SCSI 和 PCI 设备的 `I2O` 驱动程序。你可以通过以下配置选项构建 `I2O` 驱动程序：

I2O 设备支持

- I2O 支持 (`I2O`) `[M/n/y/?]`
- I2O 配置支持 (`I2O_CONFIG`) `[M/n/?]`
- I2O 块 OSM (`I2O_BLOCK`) `[M/n/?]`
- I2O SCSI OSM (`I2O_SCSI`) `[M/n/?]`
- I2O /proc 支持 (`I2O_PROC`) `[M/n/?]`

## 网络支持

这组选项涉及网络。如何设置这些选项取决于你希望在网络中使用 Linux 系统的方式。由于 X Window System 使用 TCP/IP 网络（即使你的 PC 未连接任何网络），因此请始终对 TCP/IP Networking 选项回答 Yes（是）。你还可以启用对 IPv6 的实验性支持——下一代互联网协议。

如果你希望将 Linux 系统用作 *firewall*（防火墙）——一个控制局域网（LAN）和互联网之间信息流动的中间系统，请对 Network packet filtering 选项回答 Yes（是）。

网络支持选项中的其他类别包括无线局域网、以太网（10/100 Mbps 以及千兆）、ATM（异步传输模式）、令牌环、ARCnet、AppleTalk、广域网（WAN）、PCMCIA 网络设备、业余无线电、红外线和蓝牙。对于以太网，你可以为你的系统安装的以太网卡构建支持。此类还包括无线网络的驱动和无线以太网卡的驱动。你还可以启用对 SCTP（流控制传输协议）的实验性支持——旨在通过 IP 网络传输公共交换电话网络信令消息（RFC 3758 描述了 SCTP）。



红外线支持用于使用 Infrared Data Association（IrDA，红外数据协会）指定的协议进行红外通信。IrDA 通信被许多笔记本电脑和个人数字助理（PDA）（如 Palm 和 Handspring）使用。许多红外接口形式为 *dongles*（小型适配器），通常连接在 PC 的串行端口上。你可以使用本节的选项来启用对几种常见类型 dongles 的支持。

蓝牙是一种低功耗、短距离无线技术，用于在 2.4 GHz 频段连接设备。使用蓝牙的设备通常可以在彼此 10 米范围内连接。要了解有关蓝牙的更多信息，请访问 www.bluetooth.com。Linux 通过核心驱动器和几个其他模块支持蓝牙。你可以回答 y 以启用蓝牙支持，然后选择特定于你的蓝牙设备的其他选项。

### ISDN 子系统

这组选项允许你包含对 *ISDN*（综合业务数字网）的支持——这是一种你可以用来将 Linux 系统连接到互联网的数字电话线。这些与 ISDN 相关的选项包括特定 ISDN 适配器的配置。

只有当你的 PC 有 ISDN 卡时才构建 ISDN 驱动程序。如果你预计将添加 ISDN 卡并从电话公司购买 ISDN 服务，你可以将驱动程序构建为模块。

### 电话支持

使用正确的硬件和软件，电话支持选项使你可以使用 Linux 系统进行互联网电话呼叫（也称为 *voice over Internet Protocol* 或 *VoIP*，即网络电话）。如果你有电话卡，例如由 Quicknet Technologies, Inc. 制造的 Internet PhoneJACK 或 Internet LineJACK，你可以选择构建电话支持的驱动程序模块。如果你没有电话卡，你可以安全地关闭这些选项。

### 输入设备和字符设备

接下来的几个选项涉及配置键盘、鼠标、游戏杆和触摸屏等输入设备，以及连接到串行和并行端口的设备。这些选项还包括多端口串行接口卡的配置，这些卡使你可以将多个终端或其他设备连接到你的 Linux 系统。如果你的系统没有此类设备，请回答 *No*（否）。在列表的末尾，你会看到一个关于并行打印机支持（*PRINTER*）的问题。如果你计划将打印机连接到并行端口，请对此选项回答 *Yes*（是）。

### 看门狗定时器

这些配置选项允许你开启对看门狗定时器的支持。基本上，这会导致内核创建一个特殊文件；如果不能每分钟打开该文件并写入它，系统就会重启。一些看门狗板可以监控 PC 的状态（包括温度）。你还可以从这组选项中启用对特定看门狗卡的支持。

如果你希望访问 PC 的实时时钟中的非易失性（电池备份）内存——*NVRAM*——请对 *NVRAM* 选项回答 *Yes*（是）。你可以通过启用 *RTC* 选项来访问实时时钟。

### 软盘磁带驱动器

如果你的软盘控制器连接了磁带驱动器，请对下一个选项回答 *y* 或 *m* 并适当选择其他参数（或接受默认选择）：

- Ftape，软盘磁带设备驱动程序
- Ftape (I2C-80/Ttavan) 支持 (FTAPE) [y/m/n/?]

您还可以启用若干与软盘磁带驱动器相关的参数。

## 高级图形支持

下一组选项配置对支持硬件加速 3D 图形的高级显卡的支持。您可以启用第一个选项以构建 AGP（加速图形端口）驱动程序，并对您特定芯片集对应的选项回答“是”。

```
/dev/agpgart (AGP Support) (AGP) [y/m/n/?]
```

接下来，您需要配置一组用于直接渲染管理器（DRM）的选项——这是一种支持 XFree86 直接渲染基础架构（DRI）的设备独立驱动程序。DRI 旨在直接访问高级显卡（如 3Dx Banshee 和 Voodoo3+）中的 3D 图形硬件。若要了解有关 DRI 的更多信息，请使用 Web 浏览器访问网址 http://dri.freedesktop.org/wiki。

如果您拥有 3D 显卡，可以回答“是”以启用 DRM，并为系统中的显卡构建模块。如果您没有列出的那些显卡之一，则应对这些选项回答“否”。

## I²C 支持

I2C（集成电路总线）——读作 *EYE-squared-see*——是飞利浦公司为通过一对 wires 以 10 到 100 kHz 的速率在集成电路芯片之间进行通信而开发的一种协议。系统管理总线（SMBus）是 I2C 协议的一个子集。许多现代主板都配有一组用于连接 EEPROM（电可擦除可编程只读存储器）和硬件监控芯片等设备的 SMBus。Linux 支持 I2C 和 SMBus 协议。您需要此支持来使用视频 for Linux。如果您有任何需要 I2C 支持的硬件传感器或视频设备，请对 I2C 支持选项回答 *m*（表示模块），并对您硬件的特定驱动程序回答 *m*。例如，如果您想使用 BT848 帧捕获板（用于捕获视频），您应该对 I2C、I2C_ALGOBIT 和 VIDEO_BT848 选项回答 *m*（I2C_ALGOBIT 选项启用对所谓的 I2C 位驱动接口的支持，而 BT848 板支持这种接口）。

## 多媒体设备

此选项类别配置对多媒体设备（如摄像机、电视调谐器和 FM 收音卡）的支持。

## 帧缓冲

通过这些选项，您可以启用对帧缓冲设备的支持。帧缓冲是图形硬件的一种抽象，使得内核和其他软件可以生成图形输出，而无需依赖于显卡的底层细节（例如硬件寄存器）。许多显卡都支持帧缓冲。

## 声音

使用这组选项配置声卡支持。如果您安装了声卡，请先对声卡支持选项回答 `m`。之后，对高级 Linux 声音架构（ALSA）和声音设备回答 `m`。您可以始终为所有类型的声卡构建声音模块。这样一来，当需要时，您系统声卡所需的模块即可用。

## USB 支持

使用此选项类别配置对通用串行总线（USB）的支持——一种内置于大多数新 PC 中的串行总线。USB 1.1 版支持高达 12 Mbps（1200 万比特每秒，或 1.5 MB 每秒）的数据传输速率——相比之下，标准串行端口（如 COM1）的传输速率仅为 115 Kbps 或 0.115 Mbps。在一个 USB 总线上最多可以级联 127 个设备。该总线还为设备提供电源，并且可以在 PC 运行时连接或断开设备——这种功能通常被称为 *热交换* 或 *热插拔*。USB 2.0 版（简称 USB 2.0 或 USB2）将数据传输速率提升至 480 Mbps，略快于竞争者 IEEE 1394（FireWire）总线。

USB 可以取代 PC 的串行口、并口以及键盘和鼠标端口的功能。如今，许多 PC 外围设备——如鼠标、键盘、打印机、扫描仪、调制解调器、数码相机等——都设计为通过 USB 端口连接到 PC。

如果您的 PC 有 USB 端口，请对“Support for USB”选项回答 `m`（以便构建模块）。然后，您需要根据您 PC 拥有的 USB 接口类型——EHCI（用于 USB 2.0）、UHCI（Intel）或 OHCI（Compaq 及其他厂商）——对 `EHCI_HCD`、`UHCI_HCD` 或 `OHCI_HCD` 选项之一回答 `m`。要确定 USB 接口类型，请在终端窗口中输入 `lspci` 并在输出中查找 USB 控制器的制造商和型号。

若要支持 USB 2.0，您可以对 `EHCI_HCD`（即主机控制器设备）选项回答 `m`。

在选择了 UHCI 或 OHCI 接口支持后，您还必须为系统中特定的 USB 设备构建驱动程序模块。

## 文件系统

通过此选项类别，您可以开启对特定类型文件系统的 支持。您会对 Linux 内核支持的大量不同文件系统感到惊讶。（表 5-1 仅列出了一些。）通常，我们会构建一个支持核心 Linux 文件系统（Ext2 和 Ext3）、CD-ROM 文件系统（ISO 9660 和 Joliet）以及 DOS/Windows 文件系统（MSDOS、FAT 和 VFAT）的内核。为了与 Windows 2000/XP 系统共享文件，您还需要构建 CIFS 的模块。

**表 5-1：Linux 内核支持的部分文件系统**

| 文件系统 | 描述 |
| :--- | :--- |
| Apple Macintosh | Macintosh HFS 文件系统。（Linux 可以读写格式化为 Macintosh 的软盘和硬盘。） |
| CIFS | 通用互联网文件系统（CIFS）——服务器消息块（SMB）协议的继任者——是 Windows 2000、Windows XP 和 Samba 等 Windows 服务器的新文件系统。 |
| Coda | 一种高级网络文件系统，类似于 NFS，但更好地支持断开连接操作（例如笔记本电脑），并具有更好的安全模型。 |
| Ext2 | 第二代扩展文件系统——Linux 当前的标准文件系统。 |
| Ext3 | 支持日志记录的文件系统——一种在崩溃后允许快速恢复磁盘的机制。 |
| FAT | 指任何基于文件分配表（FAT）的文件系统（包括 MS-DOS 和 Windows 95 VFAT 文件系统）。 |
| HPFS | OS/2 HPFS 文件系统。（Linux 只能读取 HPFS 文件。） |



# 文件系统与内核配置说明

| `ISO 9660` | 用于 CD-ROM 的标准 `ISO 9660` 文件系统。（该系统也称为 High Sierra 文件系统，在一些 UNIX 工作站上被称为 `hfs`。） |
| `Joliet` | Microsoft 为 `ISO 9660` CD-ROM 文件系统开发的 `Joliet` 扩展，允许使用 Unicode 格式长文件名。（Unicode 是一种新的 16 位字符代码，可以编码世界上几乎所有语言的字符。） |
| `Minix` | Minix 文件系统——Linux 的原始文件系统。 |
| `MSDOS` | MS-DOS 文件系统。 |
| `NFS` | 网络文件系统，用于从网络上的其他系统共享文件和目录。 |
| `NTFS` | NT 文件系统（`NTFS`）——Microsoft Windows NT 和 XP 使用的文件系统。（Linux 只能读取 `NTFS` 磁盘。） |
| `/proc` | 一种虚拟文件系统，您可以通过它获取有关内核的信息。`/proc` 文件系统并不存在于磁盘上；当您访问时才会创建文件。 |
| `ReiserFS` | 一种高效文件系统，将文件名和文件都存储在平衡树中，并使用日志记录。 |
| `SMB` | 使用服务器消息块（`SMB`）协议访问运行 Windows 95/98/NT/2000 的网络 PC 的共享目录的文件系统。 |
| `System V` | SCO、Xenix 和 Coherent 的 Intel PC UNIX 变体使用的文件系统。 |
| `UDF` | 用于某些 CD-ROM 和 DVD 的新文件系统。（例如，`UDF` 文件系统用于以包模式写入或由 DirectCD 等 `UDF` 工具写入的可重写 CD。） |
| `UFS` | BSD（Berkeley Software Distribution）的 UNIX 变体（如 SunOS、FreeBSD、NetBSD 和 NextStep）使用的文件系统。 |
| `VFAT` | 具有长文件名的 Windows 95/98/NT/2000 文件系统。 |

## 分区类型

Linux 可以读取和操作由许多不同系统创建的磁盘分区。这些选项使您能够包含对特定分区类型的支持：

- 分区类型
- 高级分区选择 (`PARTITION_ADVANCED`) [Y/n/?]
- Acorn 分区支持 (`ACORN_PARTITION`) [N/y/?]
- Alpha OSF 分区支持 (`OSF_PARTITION`) [Y/n/?]
- Amiga 分区表支持 (`AMIGA_PARTITION`) [N/y/?]
- Atari 分区表支持 (`ATARI_PARTITION`) [N/y/?]
- Macintosh 分区映射支持 (`MAC_PARTITION`) [Y/n/?]
- PC BIOS (`MSDOS` 分区表) 支持 (`MSDOS_PARTITION`) [Y/n/?]
- ... 省略的行 ...

## 本地语言支持

这组配置选项要求您选择一个本地语言字符集。Microsoft FAT 文件系统使用这些字符集以多种语言之一存储和显示文件名。字符集存储在称为 DOS 代码页的文件中。您必须包含适当的代码页，以便 Linux 内核能够正确读取和写入硬盘上任何 DOS 分区中的文件名。请注意，代码页仅适用于文件名；它们与文件的实际内容无关。

您可以包含任意数量的代码页支持。只需对您所选语言对应的代码页回答“是”即可。

## 内核调试

这组选项允许你调试内核，并使用 SysRq 键（相当于按下 Alt+Print Screen）在系统崩溃后立即获取重要的状态信息。如果你是预计需要调试内核的 Linux 开发者，这些信息将非常有用。大多数用户会选择回答“否”以禁用这些选项（因为大多数用户运行的是稳定版本的内核，且并不预期需要修复内核错误）。

## 安全选项

通过这些选项，你可以包含对 Security Enhanced Linux（`SELinux`，安全增强型 Linux）的支持，该技术由美国国家安全局（NSA）开发。`SELinux` 随 Linux 附带提供，但你可以通过在启动时提供 `selinux=0` 作为启动选项来将其关闭。有关 `SELinux` 的更多信息，请访问 www.nsa.gov/selinux。

## 加密支持

这组选项用于在内核中启用加密支持。你可以启用支持，如下选项的默认选择所示：

*   加密选项
    *   加密 API (`CRYPTO`) [Y/?] Y
    *   HMAC 支持 (`CRYPTO_HMAC`) [Y/?] Y
    *   空算法 (`CRYPTO_NULL`) [M/n/?]
    *   MD4 摘要算法 (`CRYPTO_MD4`) [M/n/y/?]
    *   MD5 摘要算法 (`CRYPTO_MD5`) [Y/m/?]
    *   SHA1 摘要算法 (`CRYPTO_SHA1`) [M/y/?]
    *   SHA256 摘要算法 (`CRYPTO_SHA256`) [M/n/y/?]
    *   SHA384 和 SHA512 摘要算法 (`CRYPTO_SHA512`) [W/n/y/?]
    *   ... 省略的行 ...

你还可以启用对某些硬件加密设备的支持，并构建几个循环冗余校验（CRC）算法的模块。

## 构建内核和模块

在配置完内核选项后，你必须构建内核。这部分可能需要一些时间。根据你的系统不同，制作新内核可能需要几分钟到一小时以上。

在单行中输入以下内容以启动该过程：

```
make
```

## 安装模块

`make` 命令会创建新内核，以及通过配置步骤指定的任何模块。

![](img/792720823146d68f19fd50c99ebfce4b_517_0.png)

随着内核的构建，你会在屏幕上看到许多消息。完成后，新内核以名为 `bzImage` 的压缩文件形式出现在内核源代码所在位置的 `arch/i386/boot` 子目录中。

要使用新内核，你必须将内核文件和 `System.map` 文件复制到一个特定的名称下的 `/boot` 目录中，并编辑 GRUB 菜单以设置 GRUB —— 即启动加载程序。然而，在进行内核安装之前，你必须先安装模块并构建一个新的初始 RAM 磁盘。

如果你在内核配置过程中选择了任何模块，内核构建步骤也会构建这些模块。你只需安装它们即可。使用以下命令执行此任务：

```
cd /usr/src/linux*
make modules_install
```

`make modules_install` 命令会将所有模块复制到 `/lib/modules` 目录下的一个新子目录中。该子目录的名称应与内核版本号相同。

现在你可以安装内核并使其可供 GRUB 启动。

## 创建初始 RAM 磁盘文件

新内核需要一个新的初始 RAM 磁盘文件，你可以使用 `mkinitrd` 命令来创建它。通常，初始 RAM 磁盘映像存储在一个以 `initrd` 开头的文件中。正如你可能猜到的那样，`initrd` 是初始 RAM 磁盘的缩写，而 `mkinitrd` 命令之所以这样命名，是因为它创建 `initrd` 文件。

`mkinitrd` 程序位于 `/sbin` 目录中，你必须以 root 身份登录，并使用以下形式创建 initrd 文件：

```
/sbin/mkinitrd /boot/initrd-filename.img module-directory
```

`initrd` 文件必须位于 `/boot` 目录中，内核也位于此目录。你可以为 `initrd-filename` 使用任何文件名。`module-directory` 是 `/lib/modules` 中存放新内核模块文件的目录名称。`make modules_install` 步骤将模块放入一个以内核版本号命名的目录中。例如，如果你的内核版本（由 `uname -r` 命令报告）是 `2.6.11`，那么在 `make modules_install` 步骤后，`module-directory` 就是 `2.6.11`。

另一种常见的做法是通过将模块目录名称附加到 `initrd` 前缀之后来创建 `initrd` 文件名。因此，对于模块目录 `2.6.11`，`initrd` 文件将是 `initrd-2.6.11.img`。

要为新构建的内核创建初始 RAM 磁盘映像，请输入以下命令：

```
/sbin/mkinitrd /boot/2.6.11.img 2.6.11
```

此命令在 `/boot` 目录中创建文件 `initrd-2.6.11.img`。你必须在 GRUB 菜单文件（Fedora Core 中的 `/etc/grub.conf` 以及 Debian 和 SUSE 中的 `/boot/grub/menu.lst`）中引用此 `initrd` 文件。

## 安装新内核并设置 GRUB

大多数 Linux 发行版使用 GRUB 从磁盘加载 Linux 内核。你必须将新内核添加到 GRUB 菜单中，以便 GRUB 可以将其显示为可启动的选项。



在 Debian、MEPIS、SUSE 和 Ubuntu 中，GRUB 菜单是 `/boot/grub/menu.lst` 文件。在 Fedora Core 中，GRUB 菜单由 `/etc/grub.conf` 文件指定。你应该编辑适用于你发行版的文件。

以下是我系统中一个典型的 GRUB 菜单文件：

```
default
   0
# 设置超时（以秒为单位），在此之前自动启动默认项
#（通常是定义的第一个条目）。
   timeout
   5

# Ubuntu Linux
title		Ubuntu, kernel 2.6.10-5-386
root	(hd0,4)
kernel		/vmlinuz-2.6.10-5-386 root=/dev/hda3 ro acpi=off quiet splash
initrd		/initrd.img-2.6.10-5-386

# 下一个条目由 Debian 安装程序为 /dev/hdb3 上现有的
# linux 安装自动添加。
title Xandros on /dev/hdb3
root	(hdl,2)
chainloader	+1

# Windows XP
title		Windows XP
root	(hd0,1)
chainloader	+1
```

![](img/792720823146d68f19fd50c99ebfce4b_518_0.png)

以下是 GRUB 菜单文件中某些行的含义（以 `#` 开头的行是注释）：

- `default 0`：指定第一个启动项为 GRUB 启动的默认项。如果该行设置为 1，则 GRUB 启动第二个条目（2 意味着第三个条目，3 是第四个，等等）。

- `timeout 5`：使 GRUB 在等待 5 秒后自动启动默认项。如果文件中有其他启动项，用户可以从 GRUB 显示的启动菜单中选择其他项。

- 以 `title` 开头的行构成了第一个启动项或部分（下一个条目以另一个 `title` 行开始），此条目定义了 GRUB 可以启动的特定内核文件。你可以通过向配置文件添加类似的节来让 GRUB 启动另一个内核。此启动项中各行的含义如下：

    - `root (hd0, 4)`：将 `root` 设备设置为第一个硬盘的第一个逻辑分区。在此特定系统中，此分区是安装 Ubuntu 的 Linux 内核的位置。

    - `kernel /vmlinuz-2.6.10-5-386 root=/dev/hda3 ro acpi=off quiet splash`：标识如果用户选择此启动项，GRUB 将加载的内核。在这种情况下，内核文件是 `/vmlinuz-2.6.10-5-386`，它位于 `root` 设备中。在 Linux 系统中，该分区通常挂载在 `/boot` 目录上。换句话说，GRUB 加载内核文件 `/boot/vmlinuz-2.6.10-5-386`。内核名称后的项目是提供给内核的选项。例如，`root` 选项标识包含 `root` 文件系统（/）的分区。

    - `initrd /initrd.img-2.6.10-5-386`：指定包含初始 RAM 磁盘（`initrd`）映像的文件，该映像在磁盘可用之前作为文件系统使用。Linux 内核使用 `RAM 磁盘` —— 作为磁盘使用的内存块 —— 来启动；然后它加载其他驱动程序模块并开始使用硬盘。

- 以 `title` 开始的下一个部分用于从第二个 IDE 硬盘的第三个分区启动 Xandros。Xandros 使用 LILO 启动加载程序，此启动项使用 GRUB 的 `chainloader` 命令将控制权转移给 LILO 启动加载程序。

- 以 `title` `Windows XP` 开始的下一个部分是第三个启动项，指代恰好位于此系统上的 Windows XP 操作系统。标题行旁边的文本会出现在 GRUB 菜单中，用户从中选择要启动的操作系统。

要将 GRUB 配置为启动新的 Linux 内核（即你刚刚编译好的那个），请遵循以下步骤：

1. **将新的内核二进制文件复制到 `/boot` 目录。**

   新的压缩内核文件位于内核源代码所在的 `arch/i386/boot` 子目录中。内核文件名通常是 `bzImage`。只需将该文件以相同的名称复制到 `/boot` 目录即可。

   如果内核文件名是 `vmlinux`，请确保使用 `vmlinux` 而不是 `bzImage`。你可以将 `/boot` 中的内核文件名更改为任何名称，只要在步骤 3 中在 GRUB 菜单文件中引用内核时使用相同的文件名即可。

2. **将新的 `System.map` 文件从内核源代码目录复制到 `/boot` 目录。**

3. **使用你喜欢的文本编辑器编辑 GRUB 菜单文件，在文件中添加以下行：**

   ```plaintext
   title New Linux kernel (2.6.11)
   root (hd0,2)
   kernel /bzImage root=/dev/hda10 ro
   initrd /initrd-2.6.11.img
   ```

![](img/792720823146d68f19fd50c99ebfce4b_520_0.png)

在你的系统中，请确保 `root` 行是正确的——不要使用 `(hd0,2)`，而是列出挂载在 `/boot` 上的正确磁盘分区。此外，请为内核映像文件使用正确的文件名（例如，如果内核文件名为 `vmlinux`，则使用 `/vmlinux`）。内核行上的 `root` 选项必须设置为挂载了 Linux 文件系统的 `root` 目录（`/`）的分区设备名称。

*注意：* `initrd` 行指的是你在之前的步骤中创建的 `initrd` 文件。

4. **保存 GRUB 菜单文件并退出编辑器。**

现在，你可以准备重启系统并尝试新的内核了。

## 重启系统

完成 GRUB 配置后，你可以重启系统。在仍以 `root` 用户登录的状态下，输入以下命令重启系统：

```bash
reboot
```

当看到 GRUB 界面时，选择你在 GRUB 菜单文件中为新内核指定的名称。

系统重启后，你会看到熟悉的图形登录界面。若要确认确实在运行新内核，请作为用户登录，打开终端窗口，并输入 `uname -srv`。该命令会显示内核版本，以及该内核构建的日期和时间。如果你升级了内核源代码，你会看到新内核的版本号。如果你只是重新构建了相同旧内核版本的内核，则日期和时间将与重建内核的时间相匹配。这就证明了系统正在运行新的内核。

![](img/792720823146d68f19fd50c99ebfce4b_521_0.png)

如果系统 *挂起*（屏幕上没有任何输出，也没有磁盘活动），你可能在内核重建过程中跳过了某个步骤。你可以将 PC 关机再开机以重启。这次，在 GRUB 界面选择旧的可用内核名称。

# 第六卷：安全性

第五波 作者：Rich Tennant

![](img/792720823146d68f19fd50c99ebfce4b_522_0.png)

## 内容概览

- 第 1 章：介绍 Linux 安全性……499

- 第 2 章：保护 Linux 主机……513

- 第 3 章：改进网络安全……529

- 第 4 章：执行计算机安全审计……547

# 第 1 章：介绍 Linux 安全性

## 本章内容

- 建立安全策略和框架

- 理解主机安全问题

- 理解网络安全问题

- 转换计算机安全术语

- 关注安全新闻和更新

在本章中，我将解释为什么你需要关注安全，并为你提供一个高层视角来掌握安全。我会解释整体安全框架的概念，并介绍安全的两个关键方面——主机安全和网络安全。本章最后将介绍在讨论计算机安全时使用的术语。

## 为什么要关注安全？

在当今的网络化世界中，你必须关注 Linux 系统的安全性。对于独立系统或在隔离的局域网（LAN）中使用的系统，你需要专注于保护系统免受用户侵害，以及保护用户之间互不干扰。换句话说，你不希望用户故意或无意地修改或删除系统文件。此外，你也不希望某个用户破坏另一个用户的文件。

如果通过你的 Linux 系统连接到互联网，你必须保护系统免受来自互联网的未授权访问。这些入侵者——通常被称为破坏者（crackers）——通常冒充用户，窃取或破坏信息，甚至拒绝访问你自己的系统（称为拒绝服务或 DoS 攻击）。

就其本质而言，互联网连接使你的系统可以被互联网上的任何其他系统访问。毕竟，互联网连接了全球无数的网络。事实上，诸如 HTTP（Web）和 FTP 等互联网服务的客户机/服务器架构依赖于互联网提供的广泛开放的网络访问。不幸的是，这些易于访问的互联网服务也意味着网上的任何人都可以轻松访问你的系统。

如果你运行一个向他人提供信息的互联网主机，你当然希望每个人都能访问你系统的互联网服务，例如 FTP 和 Web 服务器。然而，这些服务器通常存在漏洞，破坏者可能会利用这些漏洞对你的系统造成伤害。你需要了解互联网服务的潜在安全风险——以及你可以采取预防措施来最小化有人利用你的 FTP 或 Web 服务器弱点的风险。



你还需要保护公司的内部网络免受外部人员的侵害，尽管你的目标是通过 Web 或 FTP 服务器向外部世界提供信息。你可以通过设置一个互联网 `防火墙`——内部网络的受控访问点——并将 Web 和 FTP 服务器放置在防火墙外部的托管上，来保护你的内部网络。

## 建立安全框架

保护你的 Linux 系统的第一步是建立一个 `安全策略`——一组准则，说明允许用户（以及来自互联网的访客）在你的 Linux 系统上执行哪些操作。你建立的安全级别取决于你如何使用 Linux 系统——以及如果某人获得未授权访问时，风险有多大。

如果你是组织中一个或多个 Linux 系统的系统管理员，你可能需要让公司管理层以及用户参与安全策略的制定。显然，你不能创建一个禁止所有访问的严苛策略。（那样会阻止任何人在系统上有效工作。）另一方面，如果用户正在创建或使用对组织有价值的数据，你必须建立一个保护这些数据不被外部人员披露的策略。换句话说，安全策略应该在用户需求和系统保护需求之间取得平衡。

对于独立的 Linux 系统，或者偶尔连接到互联网的家用系统，安全策略可以仅仅是列出你希望在该系统上运行的互联网服务，以及你计划在系统上建立的用户账户。对于较大的组织，你可能有一个或多个通过防火墙（最好是通过防火墙）连接到互联网的局域网上的 Linux 系统。（重申一下，`防火墙` 是一个控制局域网和互联网之间互联网协议——IP——数据包流动的设备。）在这种情况下，系统地思考整个组织的计算机安全是最佳做法。图 1-1 展示了组织范围内计算机安全框架的关键要素。

图 1-1 中概述的安全框架包括：

- 确定安全业务需求
- 执行风险评估
- 建立安全策略
- 实施包含人员、流程和技术，以缓解已识别安全风险的网络解决方案
- 持续监控和管理安全

在以下章节中，我将讨论安全框架的一些关键要素。

![](img/792720823146d68f19fd50c99ebfce4b_526_0.png)

## 确定安全业务需求

业务需求确定了业务的安全需求——你需要保护的计算机资源和信息（包括适用法律提出的任何要求，例如保护某些类型数据隐私的要求）。典型的安全需求可能包括以下项目：

- 允许授权用户访问信息
- 实施业务规则，指定谁有权访问哪些信息
- 使用强大的用户身份验证系统
- 拒绝数据上的恶意或破坏性操作
- 保护数据在通过网络传输时的端到端安全
- 实施适用法律强加的所有安全和隐私要求

## 执行风险分析

风险分析的核心在于识别和评估风险——即那些可能对您的 Linux 系统造成伤害的潜在事件。该分析过程涉及确定以下事项，并执行相应的分析以确定处理这些风险的优先级：

- `威胁（Threats）`：您正在防范的对象
- `漏洞（Vulnerabilities）`：可能被威胁利用的弱点（这些即为风险）
- `可能性（Probability）`：威胁利用该漏洞的概率
- `影响（Impact）`：利用特定漏洞所产生的后果
- `缓解（Mitigation）`：为降低漏洞风险应采取的措施

## 典型威胁

在进一步描述风险分析之前，这里列出一些针对您 Linux 系统的典型威胁：

- `拒绝服务（Denial of Service）`：计算机和网络被占满，导致合法用户无法使用系统。对于企业而言，拒绝服务意味着收入的损失。
- `未授权访问（Unauthorized access）`：由非授权用户使用该计算机和网络。未授权用户可以窃取信息，或恶意破坏、销毁数据。有些企业可能仅仅因为未授权用户获得了系统访问权这一事实所带来的负面宣传而受到伤害，即使数据显示没有明显的显性破坏迹象。
- `向公众泄露信息（Disclosure of information to the public）`：未经授权的向公众发布信息。例如，密码文件的泄露会使潜在攻击者能够推断出访问系统所需的用户名和密码组合。其他敏感信息（如财务和医疗数据）的暴露，可能会给企业带来潜在的法律责任。

## 典型漏洞

对您系统和网络的威胁来自于对您组织资源中漏洞的利用——包括计算机资源和人员资源。一些常见的漏洞如下：

- 人的失误（如泄露密码、丢失安全卡等）
- 内部网络连接（路由器、交换机）
- 互连点（网关——即位于互联网和内部网络之间的路由器和防火墙）
- 安全性较弱的第三方网络提供商（ISP、长途运营商）
- 操作系统安全漏洞（互联网服务器中潜在的安全漏洞，例如与 `sendmail`、`named`、`bind` 等相关的漏洞）
- 应用程序安全漏洞（特定应用程序中已知的安全漏洞）

## 风险分析的 1-2-3 法则（可能性与影响）

为了执行风险分析，请为每个潜在漏洞的可能性和影响分配一个数值。为了制定可行的风险分析，请对每个漏洞或风险执行以下步骤：

1. 为可能性分配主观评级：低（Low）、中（Medium）、高（High）。如评级所示，低可能性意味着漏洞被利用的机会较小；高可能性意味着机会较大。
2. 为影响分配类似的评级。如何定义影响由您决定。如果漏洞被利用将对您的业务产生重大影响，则应将其评为高影响。
3. 为这三个级别分配数值——低 = 1，中 = 2，高 = 3——同时适用于可能性和影响。
4. 将可能性乘以影响——您可以将此乘积视为风险等级。然后做出决定，为那些“可能性与影响的乘积”超过特定阈值的漏洞开发防护措施。例如，您可以选择处理所有可能性与影响乘积大于 6 的漏洞。

如果您希望以更细致的等级来表征可能性和影响，可以选择不使用 1 到 3 的尺度，而改用 1 到 5 的尺度（例如），并按照相同的步骤进行操作。

## 制定安全策略

以风险分析以及您可能需要处理的任何业务需求（无论风险等级如何）为基础，您可以为组织制定安全策略。这类安全策略通常解决高层级目标，例如确保数据和系统的保密性、完整性和可用性。

安全策略通常涉及以下领域：

- `身份认证（Authentication）`：使用什么方法确保用户是真实用户？谁可以访问系统？密码的最小长度和复杂度是多少？用户多久更换一次密码？用户空闲多长时间后会被自动注销？
- `授权（Authorization）`：不同类别的用户在系统上可以执行哪些操作？谁可以拥有 `root` 密码？
- `数据保护（Data protection）`：哪些数据必须受到保护？谁可以访问这些数据？某些数据是否需要加密？
- `互联网访问（Internet access）`：用户（来自局域网）访问互联网有哪些限制？用户可以访问哪些互联网服务（如 Web、互联网中继聊天等）？是否扫描传入电子邮件和附件中的病毒？是否有网络防火墙？是否使用虚拟专用网络（VPNs）通过互联网连接私有网络？
- `互联网服务（Internet services）`：每个 Linux 系统允许运行哪些互联网服务？是否有文件服务器？邮件服务器？Web 服务器？每种类型的服务器上运行哪些服务？用作桌面工作站的 Linux 系统是否运行任何服务？
- `安全审计（Security audits）`：谁负责测试安全性是否充分？多久测试一次安全性？在安全测试中发现的问题如何处理？
- `事件处理（Incident handling）`：处理计算机安全事件的程序是什么？必须通知谁？需要收集哪些信息以协助调查事件？
- `职责（Responsibilities）`：谁负责维护安全性？谁监控日志文件和审计轨迹以寻找未授权访问的迹象？谁维护安全策略？

## 实施安全解决方案（缓解）

在对风险（即漏洞）进行分析并制定安全策略后，您需要选择`缓解方案`：如何保护免受特定漏洞的攻击。在这里，您基于安全策略、业务需求和可用技术，开发一个整体安全解决方案——该解决方案利用了人员、流程和技术，并包括以下内容：

- 服务（身份认证、访问控制、加密）
- 机制（用户名/密码、防火墙）
- 对象（硬件、软件）

由于无法保护计算机系统免受所有攻击，通过风险管理过程确定的解决方案必须支持整体安全计划的三个核心概念：

- `保护（Protection）` 提供诸如策略、程序和技术解决方案等对策，以防御针对受保护资产的攻击。
- `检测（Detection）` 监控可能导致安全漏洞的保护措施中的潜在失效。
- `反应或响应（Reaction or Response）`，通常需要人工介入，针对检测到的违规情况进行响应，以在损害发生之前阻止攻击。

由于绝对免受攻击的保护是不可能实现的，因此不包含检测和反应的安全计划是不完整的。

## 安全管理

除了实施安全解决方案外，您还必须安装安全管理机制，该机制持续监控、检测并响应任何安全事件。

风险分析、安全策略、安全解决方案和安全管理的组合提供了整体安全框架。这样的框架有助于建立对安全关切的共同理解水平——并为安全解决方案的设计和实施提供共同基础。

## 加固 Linux

在定义了安全策略之后，您可以按照策略着手加固系统。具体步骤取决于您想要对系统做什么——它是服务器还是工作站，以及有多少用户需要访问该系统。

为了加固 Linux 系统，您必须处理两大类安全问题：

- `主机安全问题`：与加固操作系统以及系统上的文件和目录相关
- `网络安全问题`：指来自网络连接的攻击威胁



## 理解主机安全问题

以下是一些关于解决主机安全问题的高级指南。（我在本书第二章中详细涵盖了其中的一些主题。）

- 在安装 Linux 时，仅选择您的系统所需的软件包组。不要安装不必要的软件。例如，如果您的系统用作工作站，则无需安装大多数服务器（如 Web 服务器、新闻服务器等）。
- 创建初始用户帐户，并确保所有密码足够强大，使密码破解程序无法猜测出来。Linux 包含用于强制使用强密码的工具。
- 设置文件所有权和权限，以保护重要的文件和目录。
- 如果可用，请启用由安全增强型 Linux（SELinux）提供的强制访问控制功能。Linux 内核 2.6 支持 SELinux。
- 使用 GNU 隐私卫士（GnuPG）对包含敏感信息的文件进行加密或解密，并对从互联网下载的文件进行身份验证。GnuPG 随 Linux 提供，您可以使用 `gpg` 命令执行加密或解密文件以及对文件进行数字签名等任务。（有关数字签名的解释，请参阅本书第二章。）
- 使用文件完整性检查工具（如 Tripwire）来监控关键系统文件和目录的任何更改。请访问 www.tripwire.com 获取商业版本。
- 定期检查各种日志文件，以查找入侵或企图入侵的迹象。这些日志文件位于系统的 `/var/log` 目录中。
- 一旦可用，立即安装安全更新。这些安全更新修复了 Linux 中已知的漏洞。

## 理解网络安全问题

只要您将组织的内部网络连接到互联网，安全问题就会随之出现。即使您只将一台计算机连接到互联网，也需要考虑安全性，但当整个内部网络向世界开放时，安全问题的紧迫性更强。

如果您是一位经验丰富的系统管理员，您已经知道管理互联网存在的成本并不会让企业管理层感到担忧；他们的主要关注点是安全性。为了获得管理层对网站的支持，您必须制定一个计划，保护企业网络免受入侵者的侵害。

您可能认为，通过仅将外部服务器（如 Web 服务器和 FTP 服务器）连接到互联网，就可以避免危及内部网络。然而，采取这种简单的方法是不明智的。这就像决定因为可能会发生事故而不去开车一样。在 Web 服务器和内部网络之间没有网络连接还有以下缺点：

- 您无法使用网络文件传输（如 FTP）从内部网络将文档和数据复制到 Web 服务器。
- 内部网络上的用户无法访问企业 Web 服务器。
- 内部网络上的用户无法访问互联网上的 Web 服务器。这种限制使得一项宝贵资源——Web——对您组织中的用户来说是不可访问的。

解决这个问题的实用方案是设置互联网防火墙，并将 Web 服务器放在防火墙外的高度安全的主机上。

除了使用防火墙外，以下是解决网络安全的其他一些步骤。（我在本书第三章中对此进行了更详细的说明。）

- 仅在系统上启用您所需的互联网服务。特别是，不要启用未正确配置的服务。
- 使用 Secure Shell (`ssh`) 进行远程登录。不要使用 `r` 命令，如 `rlogin` 和 `rsh`。
- 保护您希望在系统上运行的任何互联网服务，例如 FTP 或 TELNET。您可以使用 TCP wrapper 访问控制文件 —— `/etc/hosts.allow` 和 `/etc/hosts.deny` —— 来保护其中的一些服务。（有关 TCP wrapper 的更多信息，请参阅本书第三章。）
- 迅速修复您选择运行的互联网服务的任何已知漏洞。通常，您可以从 Linux 发行版的在线更新站点下载并安装最新的安全更新。

## 深入计算机安全术语

计算机书籍、杂志文章和计算机安全专家使用了许多具有独特含义的术语。您需要了解这些术语才能理解关于计算机安全的讨论（并与安全供应商进行有效沟通）。表 1-1 描述了一些常用的计算机安全术语。

| **表 1-1** | **常用的计算机安全术语** |
| :--- | :--- |
| **术语** | **描述** |
| 应用网关 | 一种代理服务，充当应用层协议（如 FTP、HTTP、NNTP 和 SSH）的网关。 |
| 身份验证 | 确认用户确实是其所声称身份的过程。典型的身份验证方法是质询-响应方法，用户输入用户名和秘密密码以确认其身份。 |
| 后门 | 入侵者在主机上设置的一个安全弱点，旨在绕过安全功能。 |
| 堡垒主机 | 一台高度安全的计算机，作为组织在互联网上的主要呈现点。堡垒主机通常位于边界网络上，但双宿主主机（一个网络接口连接到互联网，另一个连接到内部网络）也是堡垒主机。 |
| 缓冲区溢出 | 程序中的一个安全漏洞，使入侵者可以向该程序发送过量数据，并用发送数据中的代码覆盖正在运行的程序的部分。结果是入侵者可以在系统上执行任意代码，并可能以特权用户身份访问系统。Linux 内核的新 exec-shield 功能可以防止缓冲区溢出。 |
| 证书 | 一个识别实体（如个人、组织或计算机）并将其公钥与该身份关联的电子文档。证书包含证书持有者的姓名、序列号、过期日期、证书持有者公钥的副本以及证书机构的数字签名，以便接收者可以验证证书是真实的。 |
| 证书颁发机构 (CA) | 验证身份并颁发证书的组织。 |
| 机密性 | 对于数据而言，是一种除了您之外无人可访问的状态（通常通过加密实现）。 |
| 入侵者 | 进入（或试图进入）主机的人，通常带有恶意意图。 |
| 解密 | 将加密信息转换回其原始、可理解形式的过程。 |
| 拒绝服务 (DoS) | 一种攻击，使用您计算机和网络上的大量资源，使得合法用户无法访问和使用该系统。来自单一来源的攻击通过消息淹没目标计算机并阻止合法流量。它可以阻止一个系统与其他系统进行数据交换，或阻止系统使用互联网。 |
| 数字签名 | 消息的 MD5 或 SHA-1 单向哈希值，使用消息发起者的私钥进行加密，用于验证消息的完整性并确保不可抵赖性。 |
| 分布式拒绝服务 (DDoS) | 拒绝服务攻击的一种变体，它使用来自分布式计算机系统的协调攻击，而不是单一来源。它通常利用蠕虫传播到多台计算机，然后这些计算机共同攻击目标。 |
| 非军事区 (DMZ) | 边界网络的另一个名称。（DMZ 最初代表*非军事区*，即分隔朝鲜和越南交战双方南北的缓冲区。） |
| 双宿主主机 | 具有两个网络接口的计算机（可以将每个网络想象为一个家庭）。 |
| 加密 | 将信息转换的过程，使其对除预期接收者以外的任何人来说都是不可理解的。转换是通过密钥和信息之间的数学运算完成的。 |
| 漏洞利用工具 | 公开可用且复杂的工具，不同技能水平的入侵者可以使用这些工具来确定漏洞并进入目标系统。 |
| 防火墙 | 组织内部网络与互联网之间的受控访问网关。双宿主主机可以配置为防火墙。 |
| 哈希 | 当数学函数将消息转换为固定大小的数值（称为*消息摘要*（或*哈希*））时的结果。例如，MD5 算法产生 128 位消息摘要；安全哈希算法-1 (SHA-1) 生成 160 位消息摘要。消息的哈希值使用发送者的私钥加密以生成数字签名。 |
| 主机 | 网络上配置为向网络上其他计算机提供服务的计算机。 |
| 完整性 | 对于接收的数据而言，是一种与最初发送时相同的状态（即传输过程中未发生改变）。 |
| IP 欺骗 | 一种攻击，其中入侵者弄清楚受信任主机的 IP 地址，然后发送看似来自该受信任主机的数据包。攻击者可以发送数据包，但无法看到响应。然而，攻击者可以预测数据包的序列，并基本发送设置未来入侵后门的命令。 |
| IPSec (IP 安全协议) | OSI 网络模型网络层的安全协议，旨在为 IP 数据包提供加密安全服务。IPSec 提供基于加密的身份验证、完整性、访问控制和机密性。（有关 Linux 的 IPSec 信息，请访问 **www.ipsec-howto.org**。） |
| 逻辑炸弹 | 一种破坏形式，程序员在其中插入代码，当某些触发事件（如终止程序员的工作）发生时，导致程序执行破坏性操作。 |
| 不可抵赖性 | 一种安全特性，防止数据发送者否认曾经发送过该数据。 |

*（待续）*

### 表 1-1（续）

| 术语 | 描述 |
| :--- | :--- |
| 数据包 | 一组根据特定协议组装的字节，作为网络通信的基本单位。例如，在 TCP/IP 网络中，数据包可能被称为 IP 数据包或 TCP/IP 数据包。 |
| 数据包过滤 | 根据数据包类型（由源 IP 地址、目标 IP 地址或端口指定）进行的选择性阻断。 |
| 边界网络 | 位于互联网和受保护的内部网络之间的网络。边界网络（也称为 DMZ）是堡垒机（bastion host）所在之处。 |
| 端口扫描 | 一种通过依次向端口发送连接请求来发现系统上哪些端口是开放的（换句话说，哪些互联网服务是启用的）的方法。此过程通常是进一步攻击的前兆。 |
| 代理服务器 | 位于堡垒机上的服务器，允许内部客户端访问外部服务器（也允许外部客户端访问受保护网络内的服务器）。针对各种互联网服务（如 FTP 和 HTTP）都有代理服务器。 |
| 公钥加密 | 一种使用密钥对（私钥和公钥）对信息进行加密和解密的加密方法。用公钥加密的信息只能用相应的私钥解密，反之亦然。 |



| 公钥基础设施 (PKI) | 一套标准和/服务，支持在联网环境中使用公钥加密和证书。PKI 便于执行诸如颁发、更新和吊销证书，以及生成和分发公钥/私钥对等任务。 |
| 筛选路由器 | 过滤数据包的互联网路由器。 |
| Setuid 程序 | 一种无论由谁运行，都以所有者权限运行的程序。例如，如果 root 拥有一个 setuid 程序，那么无论谁启动该程序，该程序都具有 root 权限。黑客经常利用 setuid 程序中的漏洞来获取系统的特权访问权限。 |
| 嗅探器 | 与数据包嗅探器同义——一个拦截路由数据并检查每个数据包以搜索指定信息（如明文传输的密码）的程序。 |
| 间谍软件 | 任何通过用户的互联网连接秘密收集用户信息，并通常在后台将该信息传输给他人的软件。间谍软件还可以收集电子邮件地址甚至密码和信用卡号码的信息。间谍软件与特洛伊木马类似，用户会在安装其他东西时被骗安装间谍软件。 |
| 对称密钥加密 | 一种使用相同的密钥来加密和解密信息的加密方法。 |
| 威胁 | 有意或无意的事件或活动，有可能对系统或网络造成危害。 |
| 特洛伊木马 | 一种伪装成良性程序但实际上是用于攻击系统的后门程序。攻击者通常安装一系列特洛伊木马程序，这些程序使攻击者能够以 root 权限自由访问系统，同时向系统管理员隐瞒这一事实。这样的特洛伊木马程序集合被称为 rootkit。 |
| 病毒 | 一种自我复制的程序，通过附加到其他程序上从一个计算机传播到另一个计算机。 |
| 漏洞 | 可能对系统或网络造成危害的缺陷或弱点。 |
| 战争拨号 | 拨号连续电话号码以寻找调制解调器的简单程序。 |
| 战争驾驶 | 一种使用笔记本电脑、天线和无线网卡巡逻位置以获得未授权访问，从而进入无线计算机网络的方法。 |
| 蠕虫 | 一种通过在网络间复制自身从一个计算机传播到另一个计算机的自我复制程序。 |

# 紧跟安全新闻和更新

为了了解最新的安全警报，您可能希望每天访问以下网站之一或多个：

- 位于 `www.cert.org` 的 CERT 协调中心 (`CERT/CC`)
- 位于 `www.ciac.org/ciac` 的计算机事件顾问功能 (`CIAC`)
- 位于 `www.us-cert.gov` 的美国计算机应急响应小组 (`US-CERT`)

如果您可以访问互联网新闻组，您可以定期浏览以下内容：

- `comp.security.announce`：一个受监管的新闻组，包含来自 CERT 的安全公告
- `comp.security.linux`：一个包含有关 Linux 安全问题的讨论的新闻组
- `comp.security.unix`：一个包含有关 UNIX 安全问题（包括与 Linux 相关的项目）的讨论的新闻组

如果您更喜欢通过电子邮件接收定期安全更新，您也可以在各种邮件列表上注册（订阅）：

- **FOCUS-LINUX:** 填写 `www.securityfocus.com/archive` 的表格以订阅这个专注于 Linux 安全问题的邮件列表。
- **US-CERT 国家网络安全警报系统:** 遵循 `www.us-cert.gov` 上的说明以订阅此邮件列表。网络安全警报系统通过其邮件列表提供四个类别的安全信息：
  - *技术网络安全警报*提供有关各种常见软件产品漏洞的技术信息。
  - *网络安全警报*在漏洞影响大众时发送。它们概述了非技术性的家庭和商务计算机用户可以采取的防范攻击的步骤和措施。
  - *网络安全公告*是关于安全问题和新漏洞的双周报，以及用户可采取以减少风险的补丁、变通方法和其他措施。
  - *网络安全提示*为非技术性计算机用户提供常见安全问题的建议。

![](img/792720823146d68f19fd50c99ebfce4b_537_0.png)

最后，请查看您的发行版网站，查看可能修复该发行版已知安全问题的更新。在 Debian、MEPIS 和 Ubuntu 中，您可以使用命令 `apt-get update` 接着使用 `apt-get upgrade` 来更新系统。对于 Fedora Core，网站是 `http://fedora.redhat.com/download/updates.html`。在 SUSE 中，使用 YaST Online Update 使系统保持最新。在 Xandros 中，从 Xandros Networks 获取最新更新。

# 第 2 章：保护 Linux 主机

## 本章内容

- ✓ 保护密码
- ✓ 保护文件和目录
- ✓ 使用 GnuPG 加密和签署文件
- ✓ 监控系统安全

*主机* 是您的 Linux 系统的技术术语——特别是当您使用它在网络上提供服务时。但即使单独考虑计算机本身，这个术语也有意义；它是运行在上面所有事物的主机：操作系统和所有应用程序。计算机安全的一个关键方面是保护主机。

在本章中，我将带您了解保护 Linux 主机需要遵循的几个关键步骤。这些步骤包括安装操作系统更新、保护密码、保护文件和目录、在必要时使用加密，以及监控系统安全。您可以通过检查日志文件中的任何可疑活动以及使用 Tripwire 工具（一个用于检测系统文件更改的绝佳第三方工具）来查看是否有人动了您系统上的重要文件，从而监控主机安全。

## 保护密码

从历史上看，UNIX 密码存储在 `/etc/passwd` 文件中，任何用户都可以读取该文件。例如，旧的 root 用户的典型 `/etc/passwd` 文件条目看起来像这样：

```
root::t6Z7NWdKlR8su::0:0::root::/bin/bash
```

这些字段由冒号 (`:`) 分隔，第二个字段包含加密形式的密码。为了检查密码是否有效，登录程序会对用户输入的明文密码进行加密，并将其与 `/etc/passwd` 文件中的内容进行比对。如果匹配，则允许用户登录。

密码破解程序的工作方式与登录程序非常相似，不同之处在于，这些程序会从字典中逐个挑选单词，加密该单词，然后将其与 `/etc/passwd` 文件中的加密密码进行匹配比较。为了破解密码，入侵者需要获取 `/etc/passwd` 文件。通常，破解者会利用各种互联网服务器（如邮件和 FTP）的弱点来获取 `/etc/passwd` 文件的副本。

多项改进措施使 Linux 中的密码更加安全。这些改进包括影子密码和可插拔认证模块——将在接下来的两个部分中介绍——你在安装 Linux 时可以轻松安装这些功能。在 Linux 安装过程中，你通常有机会配置认证。如果你启用了 MD5 密码并启用影子密码，Linux 将自动启用更安全的密码机制。

## 影子密码

显然，将密码随意存放，即使它们已加密，任何人都可以获取，这都是不安全的做法。因此，Linux 不再将密码存储在 `/etc/passwd` 文件（任何用户都可以读取该文件）中，而是将它们存储在影子密码文件 `/etc/shadow` 中。只有超级用户（root）可以读取此文件。例如，以下是新样式 `/etc/passwd` 文件中 root 的条目：

```
root::1:0:root:/root:/bin/bash
```

在这种情况下，请注意第二个字段包含的是 x 而不是加密后的密码。x 代表影子密码；实际的加密密码现在存储在 `/etc/shadow` 文件中，其中 root 的条目如下所示：

```
root:$1$AAAnl/YH$UESKzX2bDyp9Cgf0o1BfO15O:11077:0:99999:7:-1:-1:134540356
```

`/etc/shadow` 条目中由冒号分隔的字段格式与 `/etc/passwd` 文件中的条目相似，但大多数字段的含义有所不同。第一个字段仍然是用户名，第二个字段是加密后的密码。

每个 `/etc/shadow` 条目中的其余字段控制密码何时过期。你不需要解释或更改 `/etc/shadow` 文件中的这些条目。相反，应使用 `chage` 命令来更改密码过期信息。首先，你可以通过使用带有 `-l` 选项的 `chage` 命令来检查用户的密码过期信息，方法如下。（在这种情况下，你必须以 root 身份登录。）

```
chage -l root
```

此命令显示过期信息，包括密码的有效期以及你可以更改密码的频率。

如果你希望确保用户定期强制更改密码，可以使用 `-M` 选项来设置密码保持有效的最大天数。例如，为了确保用户 *naba* 在 90 天内被提示更改密码，我以 *root* 身份登录并输入以下命令：

```
chage -M 90 naba
```

你可以对该目录中的每个用户账号使用此命令，以确保所有密码在适当的时候过期，并且所有用户都必须选择新的密码。

## 可插拔认证模块（PAMs）



除了通过使用 `shadow` 密码提高密码文件的安全性外，Linux 还通过使用 RFC 1321 中描述的 MD5 消息摘要算法（<www.ietf.org/rfc/rfc1321.txt> 或 <www.cse.ohio-state.edu/cgi-bin/rfc/rfc1321.html>）来改进存储在 `/etc/shadow` 文件中的密码的实际加密过程。MD5 将任意长度的消息缩减为 128 位消息摘要（或 `指纹`），从而你可以使用私钥对其进行加密以进行数字签名。MD5 在密码加密方面也有很好的表现。

MD5 相比旧式密码加密的另一个优势是，旧密码最多限制为 8 个字符；而新密码（使用 MD5 加密）可以长得多。较长的密码更难被猜测，即使 `/etc/shadow` 文件落入不当之手也是如此。

你可以通过检查 `/etc/shadow` 文件得知 MD5 加密已生效。加密后的密码更长，且它们都带有 `$1$` 前缀，例如以下示例条目中的第二个字段：

```
root:$1$AAAAnI$YnIShBzzQpy9CgfoolBF0t$0:11077:0:99999:7:-1:-1:134540356
```

一个名为 `可插拔认证模块`（PAM）的附加程序模块执行实际的 MD5 加密。Linux PAM 提供了灵活的验证用户方法。通过设置 PAM 的配置文件，你可以在不实际修改关键程序（如验证用户身份的 `login` 和 `passwd` 等）的情况下，即时更改认证方法。

Linux 广泛使用 PAM 功能。PAM 驻留在许多不同的模块中（稍后会详细介绍）；它们的配置文件位于系统的 `/etc/pam.d` 目录中。输入以下命令可以检查该目录的内容：

```
ls /etc/pam.d
```

此目录中的每个配置文件都指定了特定实用程序的用户认证方式。

## 保护文件和目录

主机安全的一个重要方面是保护重要的系统文件——以及包含这些文件的目录。你可以通过文件所有权以及控制谁可以读取、写入或（对于可执行程序）执行文件的权限设置来保护文件。

默认的 Linux 文件安全由每个文件或目录的以下设置控制：

- 用户所有权
- 组所有权
- 所有者的读取、写入、执行权限
- 组的读取、写入、执行权限
- 其他用户（每个人）的读取、写入、执行权限

### 查看所有权和权限

当你使用 `ls -l` 命令查看详细列表时，可以看到这些设置。例如，输入以下命令查看 `/etc/inittab` 文件的详细列表：

```
ls -l /etc/inittab
```

生成的列表看起来像这样：

```
ls -l /etc/inittab
-rw-r--r-- 1 root root 1666 Feb 16 07:57 /etc/inittab
```

第一组字符描述了用户、组和其他人的文件权限。第三个和第四个字段显示拥有此文件的用户和组。在这种情况下，用户和组名称都是 `root`。

### 更改文件所有权

你可以使用 `chown` 命令设置用户和组所有权。例如，如果文件 `/dev/hda` 应由用户 `root` 和组 `disk` 拥有，则作为 `root` 输入以下命令来设置此所有权：

```
chown root:disk /dev/hda
```

仅更改组所有权时，使用 `chgrp` 命令。例如，你可以将文件的组所有权从之前的任何值更改为名为 `accounting` 的组：

```
chgrp accounting ledger.out
```

### 更改文件权限

使用 `chmod` 命令设置文件权限。要有效使用 `chmod`，你必须指定权限设置。一种方法是从表 2-1 的每一列中按所示顺序（谁/操作/权限）连接一个或多个字母。

**表 2-1 文件权限代码**

| 谁 | 操作 | 权限 |
| :--- | :--- | :--- |
| user 用户 | + 添加 | r 读取 |
| g 组 | - 移除 | w 写入 |
| o 其他 | = 分配 | x 执行 |
| a 全部 | s 设置用户 ID | |

要给目录中所有文件的所有人授予读取和写入权限，输入 `chmod a+rw *`。另一方面，要允许所有人执行特定文件，输入 `chmod a+x 文件名`。

指定权限设置的另一种方法是使用三位数字序列。在详细列表中，用户、组和其他人的读取、写入和执行权限设置显示为 `rwxrwxrwx` 序列，其中不允许的操作用破折号代替字母。将 `rwxrwxrwx` 视为字符串 `rwx` 的三次出现。现在分配值 r=4，w=2，x=1。要获取序列 `rwx` 的值，只需将 r、w 和 x 的值相加即可。因此，`rwx` = 7。使用此公式，你可以为任何权限设置分配三位数值。例如，如果用户可以读取和写入文件，但其他人只能读取该文件，则权限设置为 `rw-r--r--`（这就是它在列表中显示的样子），值为 644。因此，如果你希望目录中的所有文件对所有人可读，但仅用户可写，请使用以下命令：

```
chmod 644 *
```

### 设置默认权限

当你（或程序）创建新文件时，该文件获得什么权限设置？答案在于所谓的 `用户文件创建掩码`，你可以通过使用 `umask` 命令查看和设置它。

输入 `umask`，它会打印出一个数字，显示当前的文件创建掩码。`root` 用户和其他普通用户的默认设置是不同的。对于 `root` 用户，掩码设置为 `022`，而普通用户的掩码为 `002`。要查看此文件创建掩码的效果并解读掩码的含义，请遵循以下步骤：

1. **以 root 身份登录并输入以下命令：**

   ```
   touch junkfile
   ```

   该命令创建一个名为 `junkfile` 的空文件。

2. **输入 `ls -l junkfile` 以查看该文件的权限。**

   你会看到类似以下的一行：

   ```
   -rw-r--r--   1 root  root        0 Aug 24 10:56
                  junkfile
   ```

   通过将第一个字段中的每三个字母权限（不包括最前面的第一个字母）转换为 0 到 7 之间的数字，来解释权限设置中的数值。对于存在的每个字母，第一个字母的值为 4，第二个字母为 2，第三个字母为 1。例如，`rw-` 转换为 4+2+0（因为第三个字母缺失），即 6。同样，`r--` 是 4+0+0 = 4。因此，权限字符串 `-rw-r--r--` 变为 644。

3. **从权限设置的数值中减去 666，得到的结果即为 `umask` 设置。**

   在这种情况下，666 - 644 导致 `umask` 为 `022`。

   因此，`umask` 为 `022` 会导致默认权限设置为 `666 - 022 = 644`。当你将 `644` 重写为权限字符串时，它变为 `rw-r--r--`。

   要设置新的 `umask`，请在 `umask` 后跟上掩码的数值。操作方法如下：

   1. **确定你对新文件所需的权限设置。**

      例如，如果你希望新文件只能被所有者读取和写入，而不能被其他人访问，权限设置如下：

      ```
      rw-----
      ```

   2. **使用转换方法将权限转换为数值，该方法将 4 分配给第一个字段，2 分配给第二个字段，1 分配给第三个字段。**

      因此，对于仅限所有者可读和可写的文件，权限设置为 `600`。

   3. **从 666 中减去所需的权限设置以获取掩码的值。**

      对于权限设置 600，掩码变为 666 - 600 = 066。

   4. **使用 umask 命令设置文件创建掩码：**

      ```
      umask 066
      ```

![](img/792720823146d68f19fd50c99ebfce4b_544_0.png)

默认的 umask 022 对系统安全有益，因为它转换为具有所有者读写权限和所有人其他读权限的文件。归根结底，你不希望默认 umask 导致生成的文件可被全世界任何人写入。

## 检查 set user ID 权限

另一种权限设置可能构成安全风险。这种权限设置称为 set user ID（或简称 setuid），适用于可执行文件。当启用 setuid 权限时，文件将在文件所有者的用户 ID 下执行。换句话说，如果一个可执行程序的所有者是 root 且设置了 setuid 权限，那么无论谁执行该程序，它都会像 root 正在执行一样运行。这意味着该程序可以比普通用户程序执行更多操作（例如，读取所有文件、创建新文件和删除文件）。另一个风险是，如果 setuid 程序文件存在某些安全漏洞，攻击者可以通过这些程序造成比其他漏洞更大的破坏。

你可以使用一个简单的 find 命令找到所有 setuid 程序：

```
find / -type f -perm +4000 -print
```

你会看到类似以下文件列表：



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
... lines deleted ...
```

许多程序具有 `setuid` 权限是因为它们需要它，但请检查完整列表并确保没有奇怪的 `setuid` 程序（例如，用户主目录中的 `setuid` 程序）。

如果你想查看 `ls` 命令如何列出这些权限，请输入 `ls -l /bin/su`，你会看到权限设置：

```
-rwsr-xr-x   1 root root 2536 Aug 19 17:06 /bin/su
```

所有者权限设置（`-rws`）中的 `s` 告诉你 `/bin/su` 文件已设置 `setuid` 权限，这是 `su` 命令的可执行文件，你可以使用它变成 `root` 或另一个用户。

## 使用 GnuPG 加密和签署文件

Linux 附带 `GNU Privacy Guard`（`GnuPG` 或简称为 `GPG`）加密和身份验证工具。使用 `GPG`，你可以创建你的公钥和私钥对，使用你的密钥加密文件，并且还可以对消息进行数字签名以验证其确实来自你。如果你向拥有你公钥的人发送数字签名消息，接收者可以验证消息是由你签名的。

### 理解公钥加密

公钥加密的基本思想是使用一对密钥——一个私有和一个公共——它们是相关的，但不能从一个推测出另一个。使用私钥加密的内容只能使用对应的公钥解密，反之亦然。公钥用于分发给其他人，而你将私钥保存在安全的地方。

你可以使用公钥加密与他人安全地通信：图 2-1 说明了基本概念。假设 Alice 想要向 Bob 发送安全消息。他们各自生成公钥和私钥对，之后交换他们的公钥。然后，当 Alice 想要向 Bob 发送消息时，她只需使用 Bob 的公钥加密消息并将加密后的消息发送给他。现在消息对任何窃听者都是安全的，因为只有 Bob 的私钥可以解密消息——而只有 Bob 拥有该密钥。当 Bob 收到消息时，他使用他的私钥解密消息并阅读它。

在这一点上，你需要停下来思考并说：“等一下！Bob 如何知道消息确实来自 Alice？如果其他人使用 Bob 的公钥并发送消息假装来自 Alice 怎么办？” 这就是数字签名发挥作用的地方。

![](img/792720823146d68f19fd50c99ebfce4b_546_0.png)

### 理解数字签名

数字或电子签名的目的与钢笔墨水签名相同，但你进行数字签名的方式完全不同。与钢笔墨水签名不同，你的数字签名取决于你签署的消息。创建数字签名的第一步是对消息应用一个数学函数，将其缩减为固定大小的消息摘要（也称为哈希或指纹）。无论你的消息有多大，消息摘要始终约为 128 或 160 位，取决于哈希函数。

下一步是应用公钥加密。只需使用你的私钥加密消息摘要，你就得到了消息的数字签名。通常，数字签名附加在消息末尾，瞧——你就得到了一个电子签名消息。

数字签名有什么好处？好吧，任何想要验证消息确实由你签署的人，都会使用你的公钥解密数字签名。那个人得到的是消息的消息摘要（加密的哈希）。然后他或她对消息应用相同的哈希函数，并将计算出的哈希值与解密后的值进行比较。如果两者匹配，则没有人篡改过消息。因为使用了你的公钥来验证签名，该消息必须是用只有你知道的私钥签署的。所以消息一定来自你！

在 Alice 向 Bob 发送私人消息的理论场景中，Alice 可以对她的消息进行数字签名，以确保 Bob 能认出消息确实来自她。图 2-2 说明了数字签名与普通公钥加密的结合使用。

以下是 Alice 将她的私人消息发送给 Bob 并确保 Bob 真的能认出是她发送的方法：

1. Alice 使用软件计算消息的消息摘要，然后使用她的私钥加密摘要。这是她对该消息的数字签名。
2. Alice 加密该消息（再次使用某些方便的软件和 Bob 的公钥）。
3. 她将加密的消息和数字签名都发送给 Bob。
4. Bob 使用他的私钥解密消息。
5. Bob 使用 Alice 的公钥解密数字签名。这给他提供了消息摘要。
6. Bob 计算消息的消息摘要，并将其与通过解密数字签名获得的结果进行比较。
7. 如果两个消息摘要匹配，Bob 可以确信消息确实来自 Alice。

![](img/792720823146d68f19fd50c99ebfce4b_547_0.png)

## 使用 GPG

`GPG` 包含使用公钥加密和数字签名所需的工具。你使用的是 `gpg` 命令。随着你开始使用加密，你可以逐步了解如何使用 `GPG`。下面向你介绍一些使用 `GPG` 执行典型任务的示例。

### 生成密钥对

生成密钥对的步骤如下：

- 1. **输入 `gpg --gen-key`**

  如果你是首次使用 `gpg`，它会在你的主目录中创建一个 `.gnupg` 目录，并在该目录中创建一个名为 `gpg.conf` 的文件。然后 `GPG` 会询问你想要哪种类型的密钥：

  > 请选择你想要创建的密钥类型：
  >
  > (1) DSA 和 ElGamal（默认）
  >
  > (2) RSA（仅用于签名）
  >
  > (4) RSA（仅用于签名）
  >
  > 你的选择？

- 2. **按 Enter 键选择默认选项，因为这就足够了。**

  然后 `GPG` 会提示你输入密钥长度（位数）。

- 3. **再次按 Enter 键接受默认值 1,024 位。**

  `GPG` 会询问密钥何时过期。默认设置为永不过期。

- 4. **如果默认设置正是你想要的（为什么不呢？），请按 Enter 键。**

- 5. **当 `GPG` 询问你是否真的希望密钥永不过期时，按 Y 键确认。**

  `GPG` 会提示你输入姓名、电子邮件地址，最后输入一个注释，以便密钥对与你的姓名关联。

- 6. **输入每项要求的信息，然后按 Enter 键。**

- 7. **当 `GPG` 给你一个更改信息或确认现有信息的机会时，输入 `o` 并按 Enter 键确认。**

  接下来 `GPG` 会提示你输入一个用于保护私钥的口令（passphrase）。

- 8. **输入一个包含大小写字母、数字和标点符号的长短语——越长越好——然后按 Enter 键。**

  请务必选择一个你容易记住的口令。

  `GPG` 将生成密钥。它可能会要求你在电脑上进行一些操作，以便随机数生成器能够生成足够的随机数用于密钥生成过程。

### 交换密钥

要与其他人通信，你必须将你的公钥提供给对方。你还需要获取那些可能向你发送消息的人（或者可能签署文件而你希望验证其签名的人）的公钥。`GPG` 将公钥保存在你的密钥环中。（*密钥环* 本质上只是存储在文件中的公钥，但将其称为密钥环听起来不错，因为现实世界中每个人都有钥匙环，而且这些也算某种意义上的“钥匙”，对吧？）要列出密钥环中的密钥，请输入

```
gpg --list-keys
```

要将公钥发送给某人或将其放置在网站上，你需要将密钥导出到文件中。最好的方式是将密钥以 `GPG` 文档中称为 *ASCII-armored*（ASCII 装甲）格式进行导出，命令如下：

```
gpg --armor --export naba@comcast.net > nabakey.asc
```

此命令将我的公键以 ASCII-armored 格式（看起来基本上像乱码文本）保存到名为 *nabakey.asc* 的文件中。当然，你应将电子邮件地址替换为你自己的电子邮件地址（即创建密钥时使用的地址），并将输出文件名更改为其他名称。

将公钥导出到文件后，你可以将该文件通过邮件发送给其他人，或将其放置在网站上供其他人使用。

当你从他人处导入密钥时，通常也是以 ASCII-armored 格式获取的。例如，如果我在名为 *uscertkey.asc* 的文件中有一个 *us-cert@us-cert.gov* 的 `GPG` 公钥（我这是从 *www.us-cert.gov/pgp/email.html* 链接处获取的），我使用以下命令将其导入我的密钥环：

```
gpg --import uscertkey.asc
```

使用 `gpg --list-keys` 命令来验证该密钥是否在你的密钥环中。例如，当我在系统上输入 `gpg --list-keys` 时，看到的内容如下：

```
/home/naba/.gnupg/pubring.gpg
---------------------------------
pub   1024d/7B38728 2005-08-28
uid             Naha Barkakati (Author) <naba@comcast.net>
sub   2048g/3BD6D418 2005-08-28

pub   2048R/F0E187D0 2004-09-08 [expires: 2005-10-01]
uid             US-CERT Operations Key <us-cert@us-cert.gov>
```

下一步是检查新密钥的指纹。我输入以下命令获取 US-CERT 密钥的指纹：



```
gpg --fingerprint us-cert@us-cert.gov
```

GPG 打印出指纹：

```
pub 2048R/FOKE187D0 2004-09-08 [expire: 2005-10-01]
Key fingerprint = 049F E3BA 240B 4CF1 3A76 04DC 1868 49EC F0E1 87D0
uid US-CERT Operations Key <us-cert@us-cert.gov>
```

此时，你需要与 US-CERT 组织的某人验证密钥指纹。对于像 US-CERT 这样的大型组织，你可以从 US-CERT 网页验证指纹（[www.us-cert.gov/pgp/encryptmail.html](http://www.us-cert.gov/pgp/encryptmail.html)）。我检查过，指纹与 US-CERT 网站上显示的一致。

如果你认为密钥指纹没有问题，你可以签署该密钥并进行验证。这是用于签署密钥的命令：

```
gpg --sign-key us-cert@us-cert.gov
```

GPG 会要求确认，然后提示你输入口令。之后，GPG 将签署该密钥。

![](img/792720823146d68f19fd50c99ebfce4b_550_0.png)

由于密钥验证和签署是 GPG 中潜在的薄弱环节，请仔细对待你签署的密钥。签署一个密钥基本上意味着你信任该密钥确实属于该个人或组织。

### 签署文件

如果你向某人发送文件并希望向接收者保证没有人篡改过该文件，且文件确实由你发送，你会发现签署文件很有用。GPG 使签署文件变得非常容易。你可以使用以下命令对名为 `message` 的文件进行压缩和签署：

```
gpg -o message.sig -s message
```

要验证签名，请输入

```
gpg --verify message.sig
```

要获取原始文档，只需输入

```
gpg -o message --decrypt message.sig
```

有时你并不关心保持消息的机密性，但只是想签署它以表明该消息来自你。在这种情况下，你可以使用以下命令生成并附加一个明文签名：

```
gpg -o message.asc --clearsign message
```

![](img/792720823146d68f19fd50c99ebfce4b_550_1.png)

此命令基本上是将明文签名附加到文本消息末尾。下面是一个典型的明文签名块：

```
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v1.4.2 (GNU/Linux)

iDEBBQDEhhAtaHlHts4pygRahiqAJ7Qcj0pRMVgKbukYUyZATYap6RJcTqaQ8m
9Cm2hBQ98o2DX9VXS3z18=
=2uc/
-----END PGP SIGNATURE-----
```

当消息附加了明文签名后，你可以使用 GPG 通过以下命令验证签名：

```
gpg --verify message.asc
```

如果你确实签署了该消息，输出的最后一行将说明这是一个有效的签名。

### 加密和解密文档

要加密发送给特定接收者的消息，你可以使用 GPG 的 `--encrypt`（或 `-e`）命令。以下是如何使用 US-CERT 的 GPG 密钥加密一条发给 US-CERT 的消息：

```
gpg -o message.gpg -e -r us-cert@us-cert.gov message
```

该消息使用 US-CERT 的公钥进行加密（没有签名，但你可以通过 `-s` 命令添加签名）。

当 US-CERT 接收到 `message.gpg` 文件后，接收者必须使用 US-CERT 的私钥对其进行解密。以下是 US-CERT 的某人可以使用的命令：

```
gpg -o message --decrypt message.gpg
```

然后 GPG 会提示输入口令以解锁 US-CERT 的私钥，解密消息，并将输出保存到名为 `message` 的文件中。

如果你只是想加密一个文件，且不需要其他人解密该文件，你可以使用 GPG 执行所谓的 *对称加密*。在这种情况下，你提供口令来加密文件，使用以下 GPG 命令：

```
gpg -o secret.gpg -c somefile
```

GPG 会提示你输入口令并要求你重复输入口令（以确保你没有输错）。然后 GPG 使用从口令生成的密钥来加密该文件。

## 监控系统安全

即使你保护好了系统，也必须定期检查日志文件，以发现入侵迹象。你可能需要使用 Tripwire 软件（一款用于检测系统文件任何变更的出色工具），以便监控关键系统文件和目录的完整性。你的 Linux 系统可能没有预装 Tripwire 软件包。要使用 Tripwire，你必须从 www.tripwire.com 购买它。购买并安装 Tripwire 后，你可以配置它来监控系统中指定系统文件和目录的任何变更。

定期检查 `/var/log` 目录及其子目录中的日志文件。许多 Linux 应用程序，包括一些服务器，使用 syslogd 的日志记录功能写入日志信息。在 Linux 系统中，由 syslogd 写入的日志文件位于 `/var/log` 目录中。请确保只有 root 用户才能读写这些文件。

syslogd 的配置文件是 `/etc/syslog.conf`。syslogd 的默认配置会生成必要的日志文件；但是，如果你想检查并理解该配置文件，可以输入 `man syslog.conf` 获取更多信息。

# 第 3 章：增强网络安全

### 本章内容

- 保护互联网服务
- 使用安全外壳协议（SSH）进行安全的远程登录
- 设置简单防火墙
- 在 Linux 系统上启用数据包过滤

为了保护你的 Linux 系统，你必须同时关注主机安全和网络安全。这两类安全之间的界限有些任意，因为保护网络涉及修复主机上与系统提供的互联网服务相关的部分。在本章中，我将解释如何保护互联网服务（主要通过不提供不必要的服务），如何使用防火墙阻止不需要的网络数据包到达你的网络，以及如何为安全的远程登录使用安全外壳协议（SSH）。

### 保护互联网服务

对于连接到互联网的 Linux 系统（甚至是不连接互联网但位于 TCP/IP 局域网中的系统），一个重大威胁是有人可能利用众多互联网服务之一来获取你系统的访问权限。每项服务——例如邮件、Web 或 FTP——都需要运行一个服务器程序，以响应通过 TCP/IP 网络到达的客户端请求。其中一些服务器程序存在弱点，可能允许外部人员登录到你的系统——也许是以 root 权限。幸运的是，Linux 附带了一些可用于增强互联网服务安全性的功能。

![](img/792720823146d68f19fd50c99ebfce4b_554_0.png)

潜在的入侵者可以使用端口扫描工具——一种尝试在特定端口建立 TCP/IP 连接并寻找响应的程序——来检查哪些互联网服务器正在你的系统上运行。然后，为了获取你系统的访问权限，入侵者可能会利用一个或多个服务的已知弱点。

### 关闭独立服务

为了提供 Web、电子邮件和 FTP 等互联网服务，你的 Linux 系统必须运行监听传入 TCP/IP 网络请求的服务器程序。其中一些服务器在系统启动时启动，并一直运行。这类服务器被称为*独立服务器*。Web 服务器和邮件服务器就是独立服务器的例子。

另一个称为 `xinetd` 的服务器会启动其他配置为在 `xinetd` 下运行的服务器。一些 Linux 系统使用 `inetd` 服务器而不是 `xinetd` 来启动其他服务器。

一些服务器可以配置为独立运行或在像 `xinetd` 这样的超级服务器下运行。例如，`vsftpd` FTP 服务器可以配置为独立运行，或在 `xinetd` 的控制下运行。

在 Debian、MEPIS、Ubuntu 和 Xandros 中，使用 `update-rc.d` 命令关闭独立服务器，并使用 `invoke-rc.d` 命令交互式启动或停止服务器。要了解可用服务的线索，请输入 `ls /etc/init.d` 并查看所有用于开启或关闭服务的脚本文件。例如，要关闭 Samba 服务，请输入 `update-rc.d 4 samba remove`。如果服务已经在运行，请输入 `invoke-rc.d samba stop` 来停止服务。你可以以类似方式使用 `invoke-rc.d` 命令停止任何服务。

在 Fedora Core 和 SUSE 中，你可以使用 `chkconfig` 命令来开启或关闭独立服务器。通过输入 `ls /etc/init.d` 可以获得服务脚本的名称。然后，通过输入 `chkconfig --del smb` 可以关闭一个服务（例如 Samba）。如果服务已经在运行，请输入 `/etc/init.d/smb stop` 来停止服务。你可以使用 `stop` 参数运行 `/etc/init.d` 目录中的脚本来以类似方式停止任何服务。

### 配置互联网超级服务器



除了像 Web 服务器或邮件服务器这样的独立服务器外，还有 `inetd` 或 `xinetd` 等其他服务器，你必须单独配置它们。这些服务器被称为互联网超级服务器，因为它们可以按需启动其他服务器。

输入 `ps ax | grep inetd` 以查看你的系统运行的是哪种互联网超级服务器——`inetd` 或 `xinetd`。

Debian、MEPIS、Ubuntu 和 Xandros 使用 `inetd`，而 Fedora Core 和 SUSE 使用 `xinetd`。

`inetd` 服务器通过 `/etc/inetd.conf` 文件进行配置。你可以通过在该文件中找到相应的行并在行首添加井号 `#` 来注释掉该行使服务失效。保存配置文件后，输入 `/etc/init.d/inetd restart` 以重启 `inetd` 服务器。

配置 `xinetd` 服务器稍微复杂一些。`xinetd` 服务器在启动时读取名为 `/etc/xinetd.conf` 的配置文件。该文件转而引用存储在 `/etc/xinetd.d` 目录中的配置文件。`/etc/xinetd.d` 中的配置文件告诉 `xinetd` 监听哪些端口以及为每个端口启动哪个服务器。输入 `ls /etc/xinetd.d` 以查看你系统上 `/etc/xinetd.d` 目录中的文件列表。每个文件代表 `xinetd` 可以启动的一项服务。要关闭其中任何服务，请在文本编辑器中编辑该文件并在文件中添加 `disable = yes` 行。在对 `xinetd` 配置文件进行任何更改后，你必须重启 `xinetd` 服务器；否则，更改不会生效。要重启 `xinetd` 服务器，请输入 `/etc/init.d/xinetd restart`。此命令停止 `xinetd` 服务器，然后再次启动它。重启时，它读取配置文件，更改将生效。

### 配置 `TCP wrapper` 安全

`inetd` 和 `xinetd` 的一项安全功能是它们使用 `TCP wrapper` 启动各种服务。`TCP wrapper` 是一段代码，为互联网服务提供访问控制机制，充当你信息的保护包。`TCP wrapper` 可以启动其他服务，如 FTP 和 TELNET；但在启动服务之前，它会查阅 `/etc/hosts.allow` 文件，查看请求服务的宿主是否被允许使用该服务。如果 `/etc/hosts.allow` 中没有关于该宿主的信息，`TCP wrapper` 会检查 `/etc/hosts.deny` 文件，看是否拒绝该服务。如果两个文件都为空，`TCP wrapper` 将提供对所请求服务的访问。

以下是收紧 `inetd` 或 `xinetd` 配置启动的服务访问权限的步骤：

1. 使用文本编辑器编辑 `/etc/hosts.deny` 文件，将以下行添加到该文件中：

```
ALL:ALL
```

此设置拒绝所有宿主访问你系统上的任何互联网服务。

2. 编辑 `/etc/hosts.allow` 文件，并添加可以访问你系统服务的宿主名称。

例如，要仅允许来自 192.168.1.0 网络的宿主和本地主机（IP 地址 127.0.0.1）访问你系统上的服务，请将以下行放在 `/etc/hosts.allow` 文件中：

`ALL: 192.168.1.0/255.255.255.0 127.0.0.1`

3. 如果你希望允许特定远程宿主访问特定互联网服务，可以使用 `/etc/hosts.allow` 中行的以下语法来实现：

`server_program_name: hosts`

这里，`server_program_name` 是服务器程序的名称，`hosts` 是可以访问该服务的宿主逗号分隔列表。你也可以将 `hosts` 写为网络地址或整个域名，例如 `.mycompany.com`。

## 使用安全外壳协议（SSH）进行远程登录

Linux 附带 Open Secure Shell（OpenSSH）软件，这是一套为 Berkeley r 命令提供安全替代方案的程序：`rlogin`（远程登录）、`rsh`（远程 shell）和 `rcp`（远程复制）。OpenSSH 使用公钥加密来验证用户身份并加密两个宿主之间的通信，因此用户可以从远程系统安全登录并安全地复制文件。

在本节中，我将简要描述如何在 Linux 中使用 OpenSSH 软件。要了解有关 OpenSSH 的更多信息并阅读其最新新闻，请访问 www.openssh.com 或 www.openssh.org。

OpenSSH 软件在 Linux 安装期间安装。表 3-1 列出了 OpenSSH 软件的主要组件。

**表 3-1 OpenSSH 软件的组件**

| 组件 | 描述 |
| :--- | :--- |
| `/usr/sbin/sshd` | 如果你想让远程系统上的用户使用 `ssh` 客户端安全登录，此 Secure Shell 守护进程必须在宿主上运行。当来自 `ssh` 客户端的连接到达时，`sshd` 使用公钥加密执行身份验证，并与 `ssh` 客户端建立加密通信链接。 |
| `/usr/bin/ssh` | 用户可以运行此 Secure Shell 客户端登录到正在运行 `sshd` 的宿主。用户还可以使用 `ssh` 在另一个宿主上执行命令。 |
| `/usr/bin/login` | 指向 `/usr/bin/ssh` 的符号链接 |
| `/usr/bin/scp` | 安全工作类似 `scp` 的安全复制程序。`scp` 程序使用 `ssh` 进行数据传输，并提供与 `ssh` 相同的身份验证和安全功能。 |
| `/usr/bin/ssh-keygen` | 使用此程序生成 OpenSSH 中使用的公钥加密所需的公钥和私钥对。`ssh-keygen` 程序可以为 RSA 和 DSA（数字签名算法）身份验证生成密钥对。（RSA 算法的名称取自该算法开发者 Ron Rivest、Adi Shamir 和 Leonard Adleman 的姓名首字母。） |
| `/etc/ssh/sshd_config` | 此 `sshd` 服务器的配置文件指定了 `sshd` 的许多参数——包括要监听的端口、使用的协议以及其他文件的位置。（SSH 协议有两个版本，SSH1 和 SSH2，OpenSSH 均支持这两种版本。） |
| `/etc/ssh/ssh_config` | 此配置文件用于 `ssh` 客户端。每个用户也可以在用户主目录的 `.ssh` 子目录中拥有一个名为 `config` 的 `ssh` 配置文件。 |

OpenSSH 使用公钥加密，其中发送方和接收方都拥有一对密钥——一个公钥和一个私钥。公钥是自由分发的，且每一方都知道对方的公钥。发送方使用接收方的公钥对数据进行加密。然后，只有接收方的私钥才能解密数据。

要使用 OpenSSH，首先需要启动 `sshd` 服务器，然后生成主机密钥。操作方法如下：

- 如果要在主机上支持基于 SSH 的远程登录，请在系统上启动 `sshd` 服务器。输入 `ps ax | grep sshd` 查看服务器是否已在运行。如果没有，请以 root 身份登录并启用 SSH 服务。

- 在 Fedora Core 和 SUSE 中，输入 `chkconfig -level 35 sshd on`。在 Debian 和 Xandros 中，输入 `update-rc.d ssh defaults`。若要立即启动 `sshd` 服务器，请在 Debian 和 Xandros 中输入 `/etc/init.d/ssh start`，或在 Fedora Core 和 SUSE 中输入 `/etc/init.d/ssh start`。

- 使用以下命令生成主机密钥：

```
ssh-keygen -d -f /etc/ssh/ssh_host_key -N ''
```

`-d` 标志使 `ssh-keygen` 程序生成 DSA 密钥，这是 SSH2 协议所使用的。如果看到提示文件 `/etc/ssh/ssh_host_key` 已存在的消息，这意味着密钥对在 Linux 安装过程中已生成。你可以直接使用现有文件，无需重新生成密钥。

![](img/792720823146d68f19fd50c99ebfce4b_558_0.png)

第六卷

第 3 章

提高网络安全

想要使用 SSH 登录的用户可以简单地使用 `ssh` 命令。例如，这是在系统上输入的命令，用于通过 SSH 登录到另一个系统：

```
ssh 192.168.0.4 -l naba
```

其中 192.168.0.4 是另一个 Linux 系统的 IP 地址。然后 SSH 显示一条消息：

> 无法验证主机 '192.168.0.4 (192.168.0.4)' 的真实性。
> RSA 密钥指纹为 7b:79:f2:d8:8c:54:00:a6:94:ec:fa:8e:7f:c9:ad:66。
> 你确定要继续连接吗 (yes/no)?

输入 yes 并按 Enter。然后 SSH 将该主机添加到其已知主机列表中，并提示输入另一个 Linux 系统上的密码：



```
naba@192.168.0.4's password:
```

输入密码后，我就拥有了与该系统的安全登录会话。我也可以使用以下等效命令登录到此账户：

```
ssh naba@192.168.0.4
```

如果只是想从局域网（由其 IP 地址 `192.168.0.4` 标识）上的另一台系统安全地复制文件，可以像这样使用 `scp`：

```
scp 192.168.0.4:/etc/X11/xorg.conf .
```

此命令会提示输入密码，并安全地将 `/etc/X11/xorg.conf` 文件从 `192.168.0.4` 主机复制到输入 `scp` 命令的系统，结果如下：

```
naba@192.168.0.4's password: (输入我的密码。)
xorg.conf 100% 2814 2.8KB/s 00:00
```

## 设置简单防火墙

防火墙是具有两个或更多网络接口的网络设备或主机——一个连接到受保护的内部网络，另一个连接到未受保护的网络（如互联网）。防火墙控制对受保护内部网络的访问以及从内部网络发出的访问。

如果将内部网络直接连接到互联网，就必须确保内部网络上的每个系统都经过适当的安全加固——这几乎是不可能的，因为单个粗心大意的用户就可能使整个内部网络变得脆弱。防火墙是连接到互联网的单点连接：你可以将所有的努力集中在那台防火墙系统上，使其成为未经授权的对外部用户一道令人望而生畏的屏障。从本质上讲，防火墙就像一道保护性的栅栏，阻止不受欢迎的外部数据和软件进入，同时保留敏感的内部数据和软件。（参见图 3-1。）

![](img/792720823146d68f19fd50c99ebfce4b_560_0.png)

防火墙运行软件以检查到达其网络接口的网络数据包，并根据一组规则采取适当的行动。其想法是定义这些规则，以便只允许授权的网络流量在两个接口之间流动。配置防火墙涉及正确设置这些规则。一种配置策略是拒绝所有网络流量，然后仅允许有限的一组网络数据包通过防火墙。授权的网络流量将包括内部用户执行诸如访问网站和接收电子邮件等操作所必需的连接。

要发挥作用，防火墙具有以下一般特征：

- 它必须控制互联网与内部网络之间的数据包流量。
- 它*不*应提供动态路由，因为动态路由表容易受到路由*欺骗*——入侵者使用伪造路由的攻击。相反，防火墙使用静态路由表（你可以使用 Linux 系统上的 `route` 命令进行设置）。
- 它不得允许任何外部用户以 `root` 身份登录。这样，即使防火墙系统被攻陷，入侵者也被阻止使用远程登录的 `root` 权限。
- 它必须放置在物理安全的位置。
- 它必须区分来自互联网的数据包和来自内部受保护网络的数据包。此功能允许防火墙拒绝那些来自互联网但具有内部网络可信系统 IP 地址的数据包。
- 它充当内部网络的 `SMTP` 邮件网关。设置 `sendmail` 软件，使所有发出的邮件看起来都是来自防火墙系统的。
- 其用户帐户仅限于少数几个内部用户需要访问外部系统的用户帐户。需要访问内部网络的外部用户应使用 `SSH` 进行远程登录（参见本章前面关于 `SSH` 的讨论）。
- 它保留所有系统活动的日志，例如成功和未成功的登录尝试。
- 它向外部世界提供 `DNS` 名称查找服务，以解析外部世界已知的任何主机名。
- 它提供良好的性能，以便不会阻碍内部用户访问特定的互联网服务（如 `HTTP` 和 `FTP`）。

防火墙可以采取许多不同的形式。以下是三种常见的防火墙形式：

### 数据包过滤防火墙

这种简单的防火墙使用能够根据数据包的多个特征（包括源和目标 IP 地址、网络协议（`TCP` 或 `UDP`）以及源和目标端口号）进行过滤（阻止或允许）数据包的路由器。数据包过滤防火墙通常放置在不可信网络的最外层边界，并构成第一道防线。数据包过滤防火墙的一个例子是采用过滤规则来筛查网络流量的网络路由器。

数据包过滤防火墙速度快且灵活，但它们无法阻止利用应用程序特定漏洞或功能的攻击。它们只能记录极少量的信息，例如源 IP 地址、目标 IP 地址和流量类型。此外，它们容易受到利用 `TCP/IP` 协议内缺陷的攻击和漏洞利用，例如 IP 地址欺骗，这涉及修改网络数据包中的地址信息，以使数据包看起来来自受信任的 IP 地址。

### 状态检查防火墙

在这种情况下，防火墙跟踪网络应用程序正在使用的网络连接。当内部系统上的应用程序使用网络连接与远程系统建立会话时，内部系统上的端口也会打开。该端口接收来自远程系统的网络流量。对于成功的连接，数据包过滤防火墙必须允许来自远程系统的传入数据包。向传入流量开放许多端口会引发未经授权的用户滥用网络协议（如 `TCP`）的预期约定而进行入侵的风险。状态检查防火墙通过创建一个出站网络连接表来解决这个问题，其中包含每个会话对应的内部端口。然后使用此“状态表”来验证任何入站数据包。这种有状态检查比数据包过滤器更安全，因为它单独跟踪内部端口，而不是为外部访问开放所有内部端口。

### 应用代理网关防火墙

这种防火墙充当内部应用程序（试图与外部服务器（如 Web 服务器）通信）之间的中介。例如，Web 代理接收在防火墙内运行的 Web 浏览器客户端发出的请求外部 Web 页面的请求，并将它们中继到外部 Web 服务器，就好像防火墙是请求的 Web 客户端一样。外部 Web 服务器响应防火墙，防火墙将响应转发给内部客户端，就好像防火墙是 Web 服务器一样。内部客户端主机与外部 Web 服务器之间永远不会建立直接网络连接。

与数据包过滤器防火墙和有状态检查防火墙相比，应用代理网关防火墙具有一些优势。首先，应用代理网关防火墙检查整个网络数据包，而不仅仅是网络地址和端口。这使得这些防火墙能够提供比数据包过滤器或有状态检查防火墙更广泛的日志记录功能。另一个优势是，应用代理网关防火墙可以直接对用户进行身份验证，而数据包过滤器防火墙和有状态检查防火墙通常基于系统 IP 地址（即源、目标和协议类型）对用户进行身份验证。鉴于网络地址容易被伪装，应用代理网关防火墙的身份验证功能优于数据包过滤器和有状态检查防火墙。

然而，与数据包过滤器或有状态检查防火墙相比，应用代理网关防火墙的高级功能也会导致一些缺点。首先，由于应用代理网关中存在完整的数据包感知，防火墙被迫花费大量时间读取和解释每个数据包。因此，应用代理网关防火墙通常不适合高带宽或实时应用。为了减少防火墙的负载，可以使用专用的代理服务器来保护对时间要求不那么严格的服务，例如电子邮件和大多数 Web 流量。另一个缺点是，应用代理网关防火墙在支持新的网络应用和协议方面通常存在限制。对于每种需要通过防火墙的网络流量类型，都需要一个独立的、针对特定应用的代理程序。大多数应用代理网关供应商提供通用的代理程序来支持未定义的网络协议或应用。然而，这些通用代理程序往往会抵消应用代理网关架构的许多优点，并且简单地允许流量穿过防火墙。

大多数防火墙实现了这些防火墙功能的组合。例如，许多数据包过滤器防火墙或有状态检查防火墙的供应商也实现了基本的应用代理功能，以弥补其防火墙的一些弱点。在大多数情况下，这些供应商实施应用代理以提供更好的网络流量日志记录和更强的用户身份验证。几乎所有主要的防火墙供应商都以某种方式在其产品中引入了多种防火墙功能。

![](img/792720823146d68f19fd50c99ebfce4b_563_0.png)

在大型组织中，您可能还必须将较小的内部网络与企业网络隔离。您可以以与设置互联网防火墙相同的方式设置此类内部防火墙。

### 使用 NAT

网络地址转换 `NAT` 是一种有效的工具，可用于隐藏防火墙后面的内部网络的网络地址。从本质上讲，`NAT` 允许组织在防火墙后面使用私有网络地址，同时仍然保留通过防火墙连接外部系统的能力。

实施 `NAT` 有三种方法：

- **静态：**在静态 `NAT` 中，私有网络上的每个内部系统都关联一个对应的、可路由的外部 IP 地址。由于唯一 IP 地址供应紧张，这种特定技术很少使用。
- **隐藏：**在隐藏 `NAT` 中，防火墙后面的所有系统共享同一个可路由的外部 IP 地址，而内部系统使用私有 IP 地址。因此，在使用隐藏 `NAT` 时，防火墙后面的多个系统仍然表现为单个系统。
- **端口地址转换：**使用端口地址转换，可以将主机放置在防火墙系统后面，同时有选择地使它们对外部用户可访问。

就优缺点而言，每种类型的 `NAT`——静态、隐藏或端口地址转换——都适用于某些情况；变量是类型提供的设计灵活性。静态 `NAT` 提供最大的灵活性，但由于 IP 地址短缺，它并不总是实用的。隐藏 `NAT` 技术很少使用，因为端口地址转换提供了额外的功能。端口地址转换通常是方便且安全的解决方案。

## 在您的 Linux 系统上启用数据包过滤

您的 Linux 系统内置了形式为 Linux 内核中所谓的 `netfilter` 的数据包过滤软件。您只需使用 `iptables` 命令设置规则，根据数据包标头中的 IP 地址和网络连接类型来确定数据包的命运。

![](img/792720823146d68f19fd50c99ebfce4b_564_0.png)

如需了解有关 `netfilter` 和 `iptables` 的更多信息，请访问 `netfilter` 网站 `www.netfilter.org/documentation` 的文档部分。



当您的 Linux 系统和互联网之间没有专用防火墙时，内置的数据包过滤功能非常实用。例如，当通过 DSL 或电缆调制解调器将 Linux 系统连接到互联网时，情况就是如此。基本上，您可以在 Linux 系统内部拥有一个数据包过滤防火墙，它位于内核和应用之间。

## 使用安全级别配置工具

一些 Linux 发行版，例如 Fedora Core 和 SUSE，包含 GUI 工具来开启数据包过滤防火墙。

![](img/792720823146d68f19fd50c99ebfce4b_564_1.png)

在 Fedora Core 中，您可以通过图形化安全级别配置工具开启不同级别的数据包过滤。要运行该工具，请以 root 身份登录，并选择“系统 > 管理 > 安全级别和防火墙”。安全级别配置对话框出现，如图 3-2 所示。

![](img/792720823146d68f19fd50c99ebfce4b_564_2.png)

图 3-2：在 Fedora Core 中，您可以使用此工具设置数据包过滤。

![](img/792720823146d68f19fd50c99ebfce4b_564_3.png)

### 第六卷

第 3 章

改进网络安全

在安全级别配置对话框中的“防火墙选项”选项卡中（参见图 3-2），您可以使用安全级别配置工具选择两个预定义的简单防火墙（更准确地说，是数据包过滤）级别：

- 已禁用：不执行任何过滤，允许所有连接。（您仍然可以通过不运行服务器或在 `xinetd` 配置文件中禁用它们来关闭互联网服务。）如果您的 Linux 系统位于受保护的局域网内部，或者您拥有独立的防火墙设备，则此安全级别是没问题的。
- 已启用：开启数据包过滤。然后您可以选择要允许的服务和信任的网络设备。

您可以允许针对特定互联网服务（如 SSH、TELNET 和 FTP）的传入数据包。如果您选择将网络接口（如 `eth0`，即第一个以太网卡）标记为信任，则该接口上的所有网络流量都会在不经过任何过滤的情况下被允许。

Fedora Core 的安全级别配置工具还有一个选项卡——`SELinux` 选项卡（参见图 3-2）——它可以开启或关闭由 `SELinux` 提供的强制访问控制。

在 SUSE 中，要设置防火墙，请单击“主菜单 > 系统 > 控制中心 (`YaST`)”。在出现的 `YaST` 控制中心窗口中，单击窗口左侧的“安全和用户”，然后单击右侧的“防火墙”。`YaST` 打开一个窗口（见图 3-3），您可以使用它来配置防火墙。

![](img/792720823146d68f19fd50c99ebfce4b_565_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_565_1.png)

![](img/792720823146d68f19fd50c99ebfce4b_565_2.png)

## 使用 iptables 命令

图形界面（GUI）防火墙配置工具使用 `iptables` 命令来实现防火墙功能。如果你的 Linux 系统没有图形界面工具，你可以直接使用 `iptables` 来配置 Linux 系统的防火墙。本节向你介绍 `iptables`。

使用 `iptables` 命令稍微复杂一些。`iptables` 使用“链” (`chain`) 的概念，即一系列规则的序列。每条规则说明如何处理数据包（如果报头包含特定信息，例如源 IP 地址或目标 IP 地址）。如果某条规则不适用，`iptables` 将参考链中的下一条规则。默认情况下，存在三个链：

- `INPUT` 链：数据包首先被测试的第一组规则。只有当 `INPUT` 链没有指定 `DROP` 或 `REJECT` 时，数据包才会继续传递到下一个链。
- `FORWARD` 链：包含应用于试图通过本系统传输到另一系统的数据包的规则（例如，当你使用 Linux 系统作为局域网和互联网之间的路由器时）。
- `OUTPUT` 链：包含数据包在发出之前（无论是发往其他网络还是应用程序）所应用的规则。

图 3-4 展示了 IP 数据包通过这三个链由 `iptables` 处理的高级示意图。

当传入数据包到达时，内核使用 `iptables` 根据数据包的目标 IP 地址进行路由决策。如果数据包是发给本服务器的，内核将数据包传递给 `INPUT` 链。如果数据包满足 `INPUT` 链中的所有规则，则该数据包将由本地进程（例如正在监听此类数据包的 Internet 服务器）进行处理。

![](img/792720823146d68f19fd50c99ebfce4b_567_0.png)

图 3-4：`iptables` 处理链的简化视图。

如果内核已启用 IP 转发，且数据包的目标 IP 地址属于不同的网络，内核将数据包传递给 `FORWARD` 链。如果数据包满足 `FORWARD` 链中的规则，它就会被发送到另一个网络。如果内核未启用 IP 转发，且数据包的目标地址不是给本服务器的，该数据包将被丢弃。

如果接收传入数据包的本地处理程序需要发送网络数据包，这些数据包的传输路径将经过 `OUTPUT` 链。如果 `OUTPUT` 链接受这些数据包，它们将被发送到指定的目标网络。

你可以使用 `iptables` 命令查看当前的链，向现有链添加规则，或创建新的规则链。查看当前链时，你还可以将它们保存到文件中。例如，如果你没有进行其他操作且系统未配置防火墙，输入 `iptables -L` 应显示以下内容：

```
Chain INPUT (policy ACCEPT)
target prot opt source destination
Chain FORWARD (policy ACCEPT)
target prot opt source destination
Chain OUTPUT (policy ACCEPT)
target prot opt source destination
```

在这种情况下，三个链——`INPUT`、`FORWARD` 和 `OUTPUT`——都显示相同的 `ACCEPT` 策略，这意味着所有流量完全开放。

如果你正在设置数据包过滤器，首先要做的是指定你想接受的数据包。例如，要接受来自 `192.168.0.0` 网络地址的数据包，请将以下规则添加到 `INPUT` 链：

```
iptables -A INPUT -s 192.168.0.0/24 -j ACCEPT
```

现在，添加一条规则以丢弃除本地回环（`lo` 网络接口）之外的所有流量，并使用以下命令停止所有转发：

```
iptables -A INPUT -i ! lo -j REJECT
iptables -A FORWARD -j REJECT
```

例如，第一条 `iptables` 命令将一条规则附加到 `INPUT` 链（`-A INPUT`）：如果数据包不是来自 `lo` 接口（`-i ! lo`），`iptables` 将拒绝该数据包（`-j REJECT`）。

在拒绝所有其他数据包之前，你还可以向每个 `INPUT` 链添加更多规则以允许特定数据包进入。你可以根据许多不同参数（如 IP 地址、协议类型（TCP、UDP）、网络接口和端口号）来选择要接受或拒绝的数据包。

你可以使用 `iptables` 进行各种专门的数据包过滤。例如，假设你设置了一个 Web 服务器，并希望仅接受指向 HTTP（端口 80）和安全外壳（SSH）服务的数据包。安全外壳服务（端口 22）用于你安全地登录和管理服务器。假设该服务器的 IP 地址是 `192.168.0.10`。以下是为该服务器设置规则的一种方法：

```
iptables -P INPUT DROP
iptables -A INPUT -s 0/0 -d 192.168.0.10 -p tcp --sport 80 -j ACCEPT
iptables -A INPUT -s 0/0 -d 192.168.0.10 -p tcp --sport 22 -j ACCEPT
```

在这种情况下，第一条规则将 `INPUT` 链的默认策略设置为 `DROP`，这意味着如果没有匹配任何特定规则，数据包将被丢弃。接下来的两条规则表明，目标是 `192.168.0.10` 且指向端口 80 和 22 的数据包将被接受。

![](img/792720823146d68f19fd50c99ebfce4b_568_0.png)

如果你急需删除所有过滤规则，请输入 `iptables -F` 进行清空。要将 `INPUT` 链的默认策略（参见图 3-4）更改为 `ACCEPT`，请输入 `iptables -P INPUT ACCEPT`。这将使 `iptables` 默认接受所有传入的数据包。

> 本节并不提供 `iptables` 命令的所有详细信息。简而言之，你可以输入 `man iptables` 阅读命令摘要。你也可以在 www.iptables.org 上阅读关于 netfilter 和 `iptables` 的资料。

使用 `iptables` 命令定义规则后，它们存储在内存中，系统重启后即消失。使用 `iptables-save` 命令将规则存储到文件中。例如，你可以使用以下命令将规则保存到名为 `iptables.rules` 的文件中：

```
iptables-save > iptables.rules
```



以下是 Fedora Core 系统上生成的 `iptables.rules` 文件的列表：

```
# Generated by iptables-save v1.3.0 on Sun Aug 28 16:10:12 2005
*filter
:FORWARD ACCEPT [0:0]
:INPUT ACCEPT [0:0]
:OUTPUT ACCEPT [6:636]
-A FORWARD -j REJECT --reject-with icmp-port-unreachable
-A INPUT -s 192.168.0.0/255.255.255.0 -j ACCEPT
-A INPUT -i lo -j REJECT --reject-with icmp-port-unreachable
COMMIT
# Completed on Sun Aug 28 16:10:12 2005
```

如果你好奇的话，这些规则对应于我用来配置过滤器的以下 `iptables` 命令：

```
iptables -A INPUT -s 192.168.0.0/24 -j ACCEPT
iptables -A INPUT -i ! lo -j REJECT
iptables -A FORWARD -j REJECT
```

如果你想将这些保存的规则加载到 `iptables` 中，请使用以下命令：

```
iptables-restore < iptables.rules
```

除非你直接使用 `iptables` 命令来配置防火墙，否则防火墙配置的具体细节取决于你的 Linux 发行版提供的用于设置防火墙的任何 GUI 工具。例如，SUSE 防火墙工具会将 INPUT 和 FORWARD 链的默认策略（参见图 3-4）从 ACCEPT 更改为 DROP，这意味着在

如果没有任何规则，所有数据包都会被丢弃。这与 Fedora Core 的防火墙工具形成对比，后者将 INPUT 和 FORWARD 链的默认策略保留为 ACCEPT。这意味着如果没有定义规则，Fedora Core 会接受数据包。在使用各种 Linux 发行版的防火墙工具时，您应该意识到这些差异。

在 Fedora Core 系统上，保存和恢复防火墙规则的过程通过以下方式实现自动化：将 iptables 规则保存在 `/etc/sysconfig/iptables` 文件中，并通过以下命令启用 iptables：

```
chkconfig iptables on
```

这确保了 `/etc/init.d/iptables` 的 `start` 命令在系统启动时执行。然后，`/etc/init.d/iptables` 脚本会运行 `/sbin/iptables-restore` 命令，从 `/etc/sysconfig/iptables` 文件中恢复 iptables 规则。

![](img/792720823146d68f19fd50c99ebfce4b_570_0.png)

# 第 4 章：执行计算机安全审计

## 本章内容

- 理解计算机安全审计
- 学习安全测试方法论
- 审查主机和网络安全
- 探索安全测试工具

看到*审计*这个词，你可能会想到税务审计，对吧？嗯，审计有很多不同的类型，其中之一就是*计算机安全审计*。计算机安全审计的基本目的是测试您的系统和网络安全。对于较大的组织，独立审计员（类似于财务报表审计）可以执行安全审计。如果您只有少数几个 Linux 系统或一个小网络，您可以将安全审计作为自我评估，以弄清楚您是否做对了每一件事。

在本章中，我解释了如何执行计算机安全审计，并向您展示了许多免费工具和资源，以帮助您测试系统的安全性。

## 理解安全审计

*审计* simply 是对您所审计对象的独立评估。因此，*计算机安全审计*是对计算机安全的独立评估。如果某人对您的组织进行计算机安全审计，他或她通常专注于以下两个领域：

- 独立验证您的组织是否遵守其现有的计算机安全政策和程序。这是安全审计的非技术方面。
- 独立测试您的安全控制措施（用于保护系统的任何硬件和软件机制）的有效性。这是安全审计的技术方面。

为什么需要安全审计？原因和需要财务审计相同——主要是为了验证一切是否都按规定的方式进行。对于公共和私人机构，管理层可能希望进行独立的安全审计，以确保他们的安全状况良好。无论您的组织规模如何，您都可以随时自行进行安全审计，无论是为独立安全审计做准备，还是仅仅为了知道您是否做对了一切。

无论是进行独立的安全审计还是自我评估，安全审计都能带来以下一些好处：

- 考虑系统和数据的内部和外部威胁的定期风险评估
- 定期测试安全政策、安全控制措施和技术的效力
- 识别系统安全中的任何重大缺陷（以便您知道需要修复什么）
- 在自我评估的情况下，为组织可能不得不面临的任何年度独立安全测试做准备

### 安全审计的非技术方面

计算机安全审计的非技术部分侧重于整个组织的安全框架。审计检查组织建立和实施计算机安全政策、计划和程序的情况。需要验证的一些项目包括：

- 定期评估风险证据。
- 存在适用于整个实体的安全项目计划。
- 建立了安全管理结构。
- 明确分配了计算机安全职责。
- 实施了有效的安全相关人事政策。
- 监控安全项目的效力，并在需要时进行修改。

正如您预期的那样，安全审计的非技术方面涉及审查文档并采访相关人员，以了解组织如何管理计算机安全。当然，对于小型组织或家庭 PC，期望在文档中有计划和程序是荒谬的。在这种情况下，您只需要确保拥有一些技术控制措施来保护您的系统和网络连接即可。

### 安全审计的技术方面

计算机安全审计的技术部分侧重于测试保护您的主机和网络的技术控制措施。测试涉及确定：

- 主机保护得有多好。是否已应用所有操作系统补丁？文件权限是否设置正确？用户账户是否受到保护？文件更改是否被监控？日志文件是否被监控？等等。
- 网络保护得有多好。不必要的 Internet 服务是否已关闭？是否安装了防火墙？远程登录是否使用诸如 SSH 等工具进行了保护？是否使用了 TCP wrapper 访问控制？等等。

通常，安全专家使用自动化工具对单个主机和整个网络执行这两项安全审查。

## 实施安全测试方法论

计算机安全审计的一个关键要素是安全测试，用于检查保护主机和网络的技术机制。安全测试方法论遵循以下高级步骤：

1. 清点组织的网络、主机、网络设备（路由器、交换机、防火墙等）和 Internet 连接。
2. 如果有大量主机和网络连接，确定哪些是需要测试的重要主机和网络设备。主机的重要性取决于其运行的应用程序类型。例如，运行公司数据库的主机比用作桌面系统的主机更重要。
3. 单独测试主机。通常，这一步涉及以系统管理员身份登录，并检查主机安全的各个方面，从密码到系统日志文件。
4. 测试网络。这一步通常通过尝试从 Internet 上的另一个系统突破网络防御来完成。如果有防火墙，测试会检查防火墙是否确实配置正确。
5. 分析主机和网络测试的结果，以确定漏洞和风险。

这两种类型的测试——主机和网络——都侧重于构成整体计算机安全的三个领域：

- **预防**：包括帮助防止对系统和网络攻击的机制（非技术和技术）
- **检测**：指监控日志文件、检查文件完整性以及使用入侵检测系统等技术，这些技术可以检测某人是否即将或已经闯入您的系统
- **响应**：包括在发生计算机安全事件后，向当局报告事件和从备份中恢复重要文件等任务的步骤

对于主机和网络安全，这些领域之间存在一定的重叠。例如，主机安全（如良好的密码或文件权限）的预防机制也可以提供网络安全。尽管如此，它们是有用的。

然而，在考虑预防之前，您必须知道您试图预防的问题类型。换句话说，常见的安全漏洞是什么？预防和检测步骤通常取决于这些漏洞的性质。

## 一些常见的计算机漏洞

主机和网络安全的具体测试取决于常见的漏洞。基本上，想法是检查主机或网络是否存在黑客利用的漏洞。

## 计算机漏洞的在线资源

几个在线资源识别和分类计算机安全漏洞：

- SANS Institute 在 `www.sans.org/top20` 发布了 20 个最重要的 Internet 安全漏洞列表。
- CVE（Common Vulnerabilities and Exposures，通用漏洞披露）是漏洞标准化名称的列表。有关 CVE 的更多信息，请参见 `http://cve.mitre.org`。（该列表包含超过 7,200 个唯一的漏洞名称。）使用 CVE 名称来描述漏洞是常见的做法。
- 国家漏洞数据库（NVD）是由美国国家标准与技术研究院（NIST，美国政府机构）发布的关于计算机漏洞信息的可搜索索引。NVD 在线发布于 `http://nvd.nist.gov`。截至 2005 年 9 月 28 日，NVD 列出了近 12,700 个漏洞，并为每个漏洞提供漏洞通告和补丁信息的链接。

## 常见的 20 大计算机漏洞

SANS 顶级 20 互联网安全漏洞列表包含多种类型的漏洞，例如 Windows、跨平台和 UNIX。其中，UNIX 和跨平台漏洞与 Linux 相关。表 4-1 总结了适用于 Linux 的一些常见 UNIX 和跨平台漏洞。您可以在 `www.sans.org/top20` 阅读关于这些漏洞的完整详细信息。



## 表 4-1 UNIX 系统的一些常见漏洞

| 漏洞类型 | 描述 |
|---|---|
| BIND DNS | 伯克利互联网域名（BIND）是一个实现域名系统（DNS）的软件包，DNS 是互联网的命名服务，用于将名称转换为 IP 地址。某些版本的 BIND 存在漏洞。 |
| Apache Web 服务器 | Apache Web 服务器的某些模块（如 `mod_ssl`）存在已知漏洞。Web 服务器用于处理交互式 Web 页面的通用网关接口（CGI）程序中的任何漏洞都可能为攻击者提供访问系统的方式。 |
| 身份验证 | 用户账户通常没有密码，或者拥有容易被密码破解程序破解的弱密码。 |
| CVS、Subversion | 并发版本系统（CVS）是 Linux 系统中广泛使用的源代码控制系统。Subversion 是另一种正在变得流行的 Linux 版本控制系统。这些版本控制系统存在漏洞，可能使攻击者能够在系统上执行任意代码。 |
| sendmail | `sendmail` 是一个用于在系统之间传输电子邮件消息的复杂程序，某些版本的 `sendmail` 存在漏洞。 |
| SNMP | 简单网络管理协议（SNMP）用于远程监控和管理各种联网系统，范围从路由器到计算机。SNMP 缺乏良好的访问控制，因此，如果 SNMP 在您的系统上运行，攻击者可能能够重新配置或关闭您的系统。 |
| 开放安全套接层（OpenSSL） | 许多应用程序，如 Apache Web 服务器，使用 OpenSSL 为网络连接提供加密安全性。不幸的是，某些版本的 OpenSSL 存在已知漏洞，可能被利用。 |
| 网络文件系统（NFS）和网络信息服务（NIS） | NFS 和 NIS 都存在许多安全问题（例如，缓冲区溢出、拒绝服务攻击的潜在风险以及弱身份验证）。此外，NFS 和 NIS 经常被错误配置，这可能允许本地和远程用户利用安全漏洞。 |
| 数据库 | MySQL 和 PostgreSQL 等数据库是复杂的应用程序，很难正确配置和确保安全。这些数据库具有许多功能，可能被滥用或破坏，从而危及数据的机密性、可用性和完整性。要了解对 MySQL 的一些常见攻击以及如何防御它们，请参阅此论文：`www.nextgenss.com/papers/HackprofingMySQL.pdf`。 |
| Linux 内核 | Linux 内核容易受到许多漏洞的影响，例如拒绝服务、执行任意代码以及对系统的 root 级别访问。 |

### 主机安全审查

在审查主机安全时，重点评估以下每个领域的安全机制：

- **预防：** 安装操作系统更新，保护密码，改进文件权限，为引导加载程序设置密码，并使用加密
- **检测：** 捕获日志消息，并使用 Tripwire（一种可以检测系统文件变化的工具）检查文件完整性
- **响应：** 进行常规备份并制定事件响应程序

我将在接下来的章节中回顾其中一些主机安全机制。

### 操作系统更新

Linux 发行版在发现安全漏洞后会迅速发布更新。许多发行版提供在线更新，您可以启用并使用它们来保持系统的最新状态。更新操作系统的具体细节取决于发行版。有关如何在线更新 Linux 的信息，请参阅第五卷第 4 章。

### 文件权限

使用适当的文件所有权和文件权限保护关键系统文件。在分配文件系统所有权和权限方面的关键步骤如下：

- 找出哪些文件包含敏感信息以及原因。有些文件可能包含与工作或业务相关的敏感数据，而许多其他文件之所以敏感是因为它们控制着 Linux 系统配置。
- 维护一份授权用户列表以及他们在系统上被授权执行的操作。
- 设置密码、组、文件所有权和文件权限，仅允许授权用户访问文件。

表 4-2 列出了 Linux 中的一些重要系统文件，显示了每个文件的数字权限设置。（有关数字权限设置的更多信息，请参阅这本小书的第 2 章。）

## 表 4-2 重要系统文件及其权限

| 文件路径名 | 权限 | 描述 |
| :--- | :--- | :--- |
| `/boot/grub/menu.lst` | 600 | GRUB 引导加载程序菜单文件 |
| `/etc/cron.allow` | 400 | 允许使用 cron 提交定期任务的用户列表 |
| `/etc/cron.deny` | 400 | 不允许使用 cron 提交定期任务的用户列表 |
| `/etc/crontab` | 644 | 系统范围的定期任务 |
| `/etc/hosts.allow` | 644 | 允许使用通过 TCP wrappers 启动的 Internet 服务的主机列表 |
| `/etc/hosts.deny` | 644 | 拒绝访问通过 TCP wrappers 启动的 Internet 服务的主机列表 |
| `/etc/logrotate.conf` | 644 | 控制日志文件轮换的文件 |
| `/etc/pam.d` | 755 | 包含可插拔身份验证模块（PAM）配置文件的目录 |
| `/etc/passwd` | 644 | 旧式密码文件，包含用户账户信息但不包含密码 |
| `/etc/rc.d` | 755 | 包含系统启动脚本的目录 |
| `/etc/security` | 600 | `root` 可以登录的 TTY 接口（终端） |
| `/etc/security` | 755 | 控制系统访问的策略文件 |
| `/etc/shadow` | 400 | 包含加密密码和密码过期信息的文件 |
| `/etc/shutdown.allow` | 400 | 可以通过按 Ctrl+Alt+Delete 关机或重启的用户 |
| `/etc/ssh` | 755 | 包含 Secure Shell（SSH）配置文件的目录 |
| `/etc/sysconfig` | 755 | 系统配置文件 |
| `/etc/sysctl.conf` | 644 | 内核配置参数 |
| `/etc/syslog.conf` | 644 | 记录消息的 syslogd 服务器的配置文件 |
| `/etc/udev/udev.conf` | 644 | udev 的配置文件——udev 是一个提供动态命名热插拔设备并在 `/dev` 目录中创建设备文件能力的程序 |
| `/etc/vsftpd` | 600 | Very Secure FTP 服务器的配置文件 |
| `/etc/vsftpd.ftpusers` | 600 | 不能使用 FTP 传输文件的用户列表 |
| `/etc/xinetd.conf` | 644 | xinetd 服务器的配置文件 |
| `/etc/xinetd.d` | 755 | 包含 xinetd 服务器可以启动的特定服务配置文件的目录 |
| `/var/log` | 755 | 包含所有日志文件的目录 |
| `/var/log/lastlog` | 644 | 有关所有先前登录的信息 |
| `/var/log/messages` | 644 | 主要系统消息日志文件 |
| `/var/log/wtmp` | 664 | 有关当前登录的信息 |

另一个重要的检查是查找具有 `setuid` 权限的可执行程序文件。如果一个程序具有 `setuid` 权限并且由 `root` 拥有，那么无论实际是谁运行该程序，该程序都以 `root` 权限运行。您可以使用以下 `find` 命令找到所有 `setuid` 程序：

```bash
find / -perm +4000 -print
```

您可能希望将输出保存在文件中（只需在命令后附加 > `filename`），然后检查文件是否存在任何异常的 `setuid` 程序。例如，用户主目录中的 `setuid` 程序是不寻常的。

### 密码安全

验证 `password`、`group` 和 `shadow` 密码文件是否受到保护。特别是，shadow 密码文件必须具有写保护权限，并且只能由 `root` 读取。文件名及其建议的权限如表 4-3 所示。

## 表 4-3 密码文件的所有权和权限

| 文件路径名 | 所有权 | 权限 |
| :--- | :--- | :--- |
| `/etc/group` | root.root | 644 |
| `/etc/passwd` | root.root | 644 |
| `/etc/shadow` | root.root | 400 |

## 事件响应

事件响应是针对系统中发生异常事件时应采取何种措施而制定的策略；它指导你在有人入侵你的系统时该如何行动。

你对事件的响应取决于你如何使用你的系统，以及该系统对你或你的业务有多重要。为了实现全面的事件响应，请记住以下关键点：

- 确定你的计算机和网络有多关键和重要，并识别哪些人或资源可以帮助你保护系统
- 采取措施以预防和最大限度地减少潜在的损害和中断
- 制定并记录一份全面的应急计划
- 定期测试应急计划，并酌情修订相关程序

## 网络安全审查

网络安全审查专注于评估以下几个领域的安全机制：



- **预防：** 设置防火墙，启用数据包过滤，禁用不必要的 `inetd` 或 `xinetd` 服务，关闭不需要的 Internet 服务，使用 TCP wrappers 进行访问控制，并使用 SSH 进行安全的远程登录。

- **检测：** 使用网络入侵检测系统并捕获系统日志。

- **响应：** 制定事件响应程序。

我将在接下来的三个小节中简要描述评估网络安全的几个关键步骤。

### 由 `inetd` 或 `xinetd` 启动的服务

根据你的发行版不同，`inetd` 或 `xinetd` 服务器可能配置为启动一些 Internet 服务，例如 TELNET 和 FTP。决定启用这些服务中的哪些取决于诸如系统如何连接到 Internet 以及系统如何被使用等因素。通常你可以关闭大多数 `inetd` 和 `xinetd` 服务。

Debian、MEPIS、Ubuntu 和 Xandros 使用 `inetd` 来启动某些服务。查看 `/etc/inetd.conf` 文件，以了解 `inetd` 配置了哪些服务。你可以通过注释掉 `/etc/inetd.conf` 中的行来关闭服务——只需在行首放置一个井号（`#`）即可。

![](img/792720823146d68f19fd50c99ebfce4b_580_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_581_0.png)

Fedora Core 和 SUSE 使用 `xinetd` 作为按需启动其他 Internet 服务的服务器。要查看哪些 `xinetd` 服务已关闭，请检查 `/etc/xinetd.d` 目录下的所有配置文件，查找包含 `disable = yes` 行的配置文件。（如果该行在行首被 `#` 注释掉，则该行不计入。）你可以向任何你想关闭的服务的配置文件添加 `disable = yes` 行。

此外，请检查以下文件，查看用于 `inetd` 或 `xinetd` 服务的访问控制设置：

- `/etc/hosts.allow` 列出了允许访问特定服务的主机。
- `/etc/hosts.deny` 列出了被拒绝访问服务的主机。

### 独立服务

许多服务，例如 `apache` 或 `httpd`（Web 服务器）和 `sendmail`（邮件服务器），在启动时会自动运行，假设它们被配置为以这种方式启动。

![](img/792720823146d68f19fd50c99ebfce4b_581_1.png)

在 Fedora Core 和 SUSE 中，你可以使用 `chkconfig` 命令来检查哪些独立服务器被设置为在不同的运行级别下启动。（有关运行级别的更多信息，请参见第五卷第一章。）通常，你的 Fedora Core 或 SUSE 系统会在运行级别 3（用于文本登录）或 5（用于图形登录）下启动。因此，重要的是级别 3 和 5 下服务器的设置。要查看服务器列表，请输入 `chkconfig --list | more`。当你对网络安全进行自我评估并发现某些服务器不应运行时，你可以通过输入 `chkconfig --level 35 servicename off` 来关闭它们在级别 3 和 5 下的运行，其中 `servicename` 是你想要关闭的服务名称。

![](img/792720823146d68f19fd50c99ebfce4b_581_2.png)

在某些发行版中，你可以使用图形用户界面工具来查看在特定运行级别下启用并运行的服务。在 Fedora Core 中，选择“系统”>“管理”>“服务器设置”>“服务”。在 SUSE 中，选择“主菜单”>“系统”>“控制中心 (YaST)”，然后点击窗口左侧的“系统”和右侧的“运行级别编辑器”。

在审计网络安全时，记下所有已打开的服务器——然后尝试根据你对系统的了解，确定它们是否真的应该处于开启状态。决定打开特定服务的因素取决于你的系统是如何使用的（例如，作为 Web 服务器还是作为桌面系统）以及它是如何连接到 Internet 的（例如，通过防火墙还是直接连接）。

## 渗透测试

渗透测试是了解 Linux 系统上实际运行哪些服务的最佳方式。*渗透测试* 涉及从攻击者的角度尝试获取对你系统的访问权限。通常，你会从 Internet 上的一个系统执行此测试，并尝试查看你是否能突破系统，或者至少获取对你 Linux 系统上运行服务的访问权限。

![](img/792720823146d68f19fd50c99ebfce4b_582_0.png)

在笔记本电脑上运行的 Knoppix 非常适合执行渗透测试，因为 Knoppix 是一个 Live CD 发行版，捆绑了诸如 `nmap` 和 Nessus 等扫描工具。你只需从 Knoppix CD 启动，就可以准备好进行渗透测试。

渗透测试的一个方面是查看你的 Linux 系统上有哪些端口是打开的。*端口号* 只是一个用于标识到系统的 TCP/IP 网络连接的编号。尝试连接端口只有在某个服务器正在该端口上运行时（或者换一种说法，如果服务器正在“监听该端口”）才会成功。如果连接请求到达时服务器有响应，则该端口被视为打开。

渗透测试的第一步是执行端口扫描。术语 *端口扫描* 描述了尝试连接到每个端口号以查看是否有有效响应返回的自动化过程。有许多可用的自动工具可以执行端口扫描——你可以安装并使用一个名为 `nmap` 的流行端口扫描工具（我将在本章后面描述）。

执行端口扫描后，你便知道哪些端口实际上是打开的，并且可能被利用。并非所有服务器都存在安全问题，但许多服务器存在众所周知的漏洞。打开的端口为攻击者提供了通过其中一个服务器攻击你系统的方式。实际上，你可以使用称为 *漏洞扫描器* 的自动工具来识别系统中存在的漏洞。（我将在接下来的几节中描述一些漏洞扫描器。）无论你的 Linux 系统是通过 DSL 或电缆调制解调器直接连接到 Internet，还是通过防火墙连接，请使用端口扫描和漏洞扫描工具来确定你的防御是否存在漏洞。宁可是你发现问题，也不要让他们发现！

## 探索安全测试工具

有许多自动工具可用于执行安全测试。其中一些工具旨在查找 IP 地址范围内每个系统的打开端口。其他工具则查找与打开端口相关的漏洞。还有一些工具可以捕获（或 *嗅探*）这些弱点，帮助你分析它们，从而获取有关网络中正在发生的事情的有用信息。

第六卷

第 4 章

执行安全审计

你可以在 `www.insecure.org/tools.html` 浏览基于 `nmap` 用户非正式投票得出的前 75 种安全工具的列表。表 4-4 按类别列出了其中的一些工具。我将在接下来的几节中描述一些免费提供的漏洞扫描器。

表 4-4 一些流行的计算机安全测试工具

| 类型 | 工具名称 |
|---|---|
| 端口扫描器 | `nmap`, `Strobe` |
| 漏洞扫描器 | `Nessus Security Scanner`, `SAINT`, `SARA`, `Whisker` (CGI 扫描器), `ISS Internet Scanner`, `CyberCop Scanner`, `Vetescan`, `Retina Network Security Scanner` |
| 网络实用工具 | `Netcat`, `hping2`, `Firewall`, `Cheops`, `ntop`, `ping`, `grep`, `ngrep`, `AirSnort` (802.11 WEP 加密破解工具) |
| 主机安全工具 | `Tripwire`, `Isaf` |
| 数据包嗅探器 | `tcpdump`, `Ethereal`, `dsniff`, `snifit` |
| 入侵检测系统 (IDS) | `Snort`, `Abacus`, `portsentry`, `scanlogd`, `NFR`, `LIDS` |
| 密码检查工具 | `John the Ripper`, `LCA` |
| 日志分析和监控工具 | `logcolorise`, `tcpdstats`, `nlog`, `logcheck`, `LogWatch`, `Swatch` |

## `nmap`

`nmap`（网络映射器的缩写）是一个端口扫描工具。它可以快速扫描大型网络，并确定网络上可用的主机、它们提供的服务、它们运行的操作系统（及操作系统版本）、它们使用的数据包过滤器或防火墙类型，以及数十种其他特征。你可以在 `www.insecure.org/nmap` 阅读有关 `nmap` 的更多信息。

如果尚未安装，你可以轻松地在你的发行版上安装 `nmap`。Fedora Core 和 Knoppix 自带 `nmap`。在 Debian、MEPIS 和 Ubuntu 中，你可以使用命令 `apt-get install nmap` 安装它。在 SUSE 中，点击 YaST 控制中心软件类别中的“安装和删除软件”——主菜单 > 系统 > 控制中心 (YaST)——并使用 YaST 的软件搜索功能找到并安装 `nmap`。在 Xandros 中，你可以使用 `apt-get install nmap` 命令；运行 Xandros Networks 后，选择“编辑”>“设置应用程序源”，并点击“Debian Unsupported Site”链接作为源。

![](img/792720823146d68f19fd50c99ebfce4b_583_0.png)



如果你想尝试使用 `nmap` 来扫描你的局域网，只需输入类似于以下命令的内容（请将 IP 地址范围替换为你网络中适用的地址）：

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
Nmap finished: 1 IP addresses (5 hosts up) scanned in 30.846 seconds
```

如你所见，`nmap` 显示了开放端口的名称，并猜测了操作系统名称和版本号。

## Nessus

Nessus 安全扫描器是一款模块化的安全审计工具，它使用用 Nessus 脚本语言编写的插件来检测各种各样的网络漏洞。Nessus 采用客户端/服务器软件架构，包括一个名为 `nessusd` 的服务器和一个名为 `nessus` 的客户端。

Knoppix 系统已经自带了 Nessus，因此你不需要下载或安装任何东西。要启动 Nessus，请选择主菜单 **→** 系统 **→** 安全 **→** NESSUS 安全工具。

要安装 Nessus，请首先尝试你的 Linux 发行版通常安装新软件包的方法。在 Debian、MEPIS 和 Ubuntu 中，输入 `apt-get install nessus` 来安装包。在 SUSE 中，从 YaST 控制中心的软件类别中点击“安装和删除软件”（**→** 主菜单 **→** 系统 **→** 控制中心 (YaST)），并使用 YaST 的搜索功能找到 nessus 包。选择这些包并点击“接受”以安装它们。在 Xandros 中，选择“编辑 **→** 设置应用程序源”，并将“Debian Unsupported Site”链接作为源。然后输入 `apt-get install nessus`。

![](img/792720823146d68f19fd50c99ebfce4b_584_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_585_0.png)

对于 Fedora Core，你必须从 www.nessus.org/download/ 下载并安装 Nessus。在尝试安装 Nessus 之前，你必须安装 sharutils RPM。该包包含 Nessus 安装脚本所需的 uudecode 实用程序。sharutils 包并未随 Fedora Core 的任何标准软件包组一起安装，因此你需要自己安装它。要安装 sharutils，请挂载附带的光盘，并使用以下命令安装它：

```
cd /media/cdrom/Fedora/RPMS  
rpm -ihv sharutils*.rpm
```

要下载和安装 Nessus，请遵循以下步骤。（这些说明适用于所有 Linux 发行版。）

1. 在 www.nessus.org/download 上，选择你要下载的 Nessus 版本。对于 Linux 系统，请下载 Nessus 2.2.5 安装程序。

2. 输入以下命令来安装 Nessus。（你必须已安装开发工具，包括 The GIMP Toolkit。）

   `sh nessus-installer-2.2.5.sh`

响应安装脚本的提示以完成安装。你通常可以按 Enter 键接受默认选择。

安装完成后，请遵循以下步骤使用 Nessus。（在 Knoppix 中，选择主菜单 **→** 系统 **→** 安全 **→** NESSUS 安全工具，然后转到第 8 步）。

1. 以 root 身份登录，并输入以下命令以创建用于 Nessus 客户端和 Nessus 服务器之间安全通信的 Nessus SSL 证书：

   `nessus-mkcert`

2. 提供所需的信息以完成证书生成过程。

3. 使用以下命令创建 nessusd 账户：

   `nessus-adduser`

4. 当提示时，输入你的用户名、密码和任何规则。（如果你不知道要输入什么规则，请按 Ctrl+D。）然后按 Y 键。

5. 如果需要，你可以通过编辑配置文件 `/usr/local/etc/nessus/nessusd.conf` 来配置 `nessusd`。

6. **使用此命令启动 Nessus 服务器：**

   `nessusd -D`

7. **通过在终端窗口中输入以下命令运行 Nessus 客户端：**

   `nessus`

   将出现 Nessus 设置窗口。

8. **输入 `nessusd` 用户名和密码，然后点击登录按钮。**

9. **当 Nessus 显示用于建立安全连接的证书并询问你是否接受它时，点击“是”。**

   客户端连接到服务器后，登录按钮变为注销，其左侧出现已连接标签。

   `nessusd` 提供选项以启用可以扫描特定漏洞的插件，但其中一些插件可能会使主机崩溃并在扫描过程中中断你的网络。如果你想尝试任何插件，请选择并启用它们。如果你想确保安全，请点击“启用所有但危险插件”链接。

10. **点击目标选择选项卡并输入一个 IP 地址范围，以扫描网络中的所有主机。**

    例如，要扫描私有网络 192.168.0.0 中的前八台主机，我将地址输入为

    `192.168.0.0/29`

    不要使用 Nessus 扫描任何你不拥有的网络。扫描其他网络通常违反法律，如果你违反了相关法律，可能会面临严重的后果。

11. **点击开始扫描。**

    Nessus 开始扫描 IP 地址并检查许多不同的漏洞。进度条显示扫描状态。

    在 Nessus 完成主机的漏洞扫描后，它会以图形和文本格式的精美组合显示结果。报告是交互式的——你可以选择一个主机地址来查看该主机的报告，你可以深入特定的漏洞以查找详细信息，例如标识该漏洞的 CVE 编号以及对该漏洞的描述。

# 第七卷

# 互联网服务器

# 第四浪 作者：Rich Tennant

![](img/792720823146d68f19fd50c99ebfce4b_588_0.png)

“我马上就来。让我先处理一下这个用户。他的 3 小时下载才完成了一半。”

# 内容概览

- 第 1 章：管理互联网服务器....565

- 第 2 章：运行 Web 服务器 .......583

- 第 3 章：设置 FTP 服务器 ............607

- 第 4 章：管理邮件和新闻服务器 ....613

- 第 5 章：管理 DNS ...............639

- 第 6 章：使用 Samba 和 DNS..............661

# 第 1 章：管理互联网服务

## 本章内容

- 了解互联网服务

- 通过 inetd 或 xinetd 控制服务器

- 使用 chkconfig 或 update-rc.d 管理服务器

- 使用图形实用工具配置服务以便在启动时运行

互联网是一个客户端和服务器的世界。客户端向服务器发起请求，服务器对请求作出响应。例如，你的 Web 浏览器是一个客户端，它从 Web 服务器下载信息并显示给你。当然，客户端和服务器是在各种各样的计算机上运行的计算机程序。Linux 系统是运行各种各样服务器的理想系统——从 Web 服务器到 Windows 文件和打印服务器。在本章中，我将典型互联网服务、其客户端/服务器架构以及在 Linux 中如何管理服务器进行概述。你可以使用本章中的信息来管理在你的 Linux 系统上运行的任何服务器。

## 理解互联网服务

互联网服务是旨在将一个系统的信息传递到另一个系统的网络应用程序。按设计，每个互联网服务都分为两部分实现——一个提供信息的服务器和一个或多个请求信息的客户端。

这种客户端/服务器架构是构建分布式信息系统最常见的方式。客户端和服务器是在这些计算机上运行并通过网络通信的计算机程序。其巧妙之处在于，你可以在桌面计算机上运行客户端，并访问世界上任何地方（只要它连接到互联网）计算机上运行的服务器上的信息。



Web 本身、电子邮件和 FTP（文件传输协议）都是使用客户端/服务器模型的互联网服务的示例。例如，当你使用 Web 时，你使用 Web 浏览器客户端从 Web 服务器下载和查看网页。

客户端/服务器架构要求客户端与服务器进行通信。`传输控制协议/互联网协议` —— TCP/IP —— 在这里发挥作用。TCP/IP 为客户端和服务器交换数据分组提供了标准方式。在接下来的几个部分中，我将解释基于 TCP/IP 的服务如何通信。

### TCP/IP 和套接字

Web 和 FTP 等客户端/服务器应用程序使用 TCP/IP 进行客户端与服务器之间的数据传输。这些互联网应用程序通常利用 `Berkeley 套接字接口`（因其名称源自 Berkeley 套接字接口于 1982 年左右在 Berkeley UNIX 中引入）来进行 TCP/IP 通信。套接字接口并非物理实体——它只是一段计算机代码，计算机程序员可以使用它来创建能够与互联网上其他应用程序通信的应用程序。

即使你不使用套接字编写网络应用程序，你也可能需要使用或配置许多网络应用程序。了解套接字有助于你理解基于网络的应用程序如何工作，从而帮助你查找和纠正这些应用程序的问题。

### 套接字定义

网络应用程序使用套接字在 TCP/IP 网络上进行通信。`套接字` 代表连接的一个端点。由于套接字是双向的，可以通过它发送和接收数据。套接字有三个属性：

- 系统的`网络地址`（IP 地址）
- `端口号`，标识通过套接字交换数据的进程（`进程`是在计算机上运行的计算机程序）
- `套接字类型`，标识数据交换的协议

本质上，IP 地址标识网络上的计算机（主机）；端口号标识节点上的进程（服务器）；套接字类型确定数据交换的方式——通过面向连接（流）或无连接（数据报）协议。

### 面向连接的协议

套接字类型指示通过套接字通信所使用的协议。面向连接的协议就像正常的电话交谈一样工作。当你要与朋友通话时，你必须拨打朋友的电话号码并在建立连接后才能进行交谈。同样，面向连接的数据交换要求发送和接收进程在开始数据交换之前先建立连接。

在 TCP/IP 协议套件中，TCP —— `传输控制协议` —— 支持运行在互联网上两台计算机上的两个进程之间的面向连接的数据传输。TCP 提供进程之间可靠的双向数据交换。

正如 TCP/IP 的名称所暗示的，TCP 依赖 IP —— `互联网协议` —— 来交付数据包。IP 不保证数据包的交付；它也不保证数据包以特定的顺序交付。然而，IP 确实有效地将数据包从一个网络移动到另一个网络。TCP 负责将数据包按正确的顺序排列，检测是否发生错误，并在发生错误时请求重新传输数据包。

TCP 适用于旨在一次交换大量数据的应用程序。此外，需要可靠数据交换的应用程序使用 TCP。（例如，FTP 使用 TCP 来传输文件。）

在套接字模型中，使用 TCP 的套接字被称为`流套接字`。

### 无连接的协议

无连接的数据交换协议不要求发送方和接收方显式建立连接。这就像在拥挤的房间里向朋友大喊——你无法确定朋友是否听到了你。

在 TCP/IP 协议套件中，`用户数据报协议`（UDP）提供无连接服务，用于发送和接收称为`数据报`的数据包。与 TCP 不同，UDP 不保证数据报到达其预期目的地。UDP 也不确保数据报以发送时的顺序交付。

UDP 用于一次交换少量数据的应用程序，或不需要数据交付可靠性和顺序的应用程序。例如，SNMP（`简单网络管理协议`）使用 UDP 传输数据。

在套接字模型中，使用 UDP 的套接字被称为`数据报套接字`。

### 套接字和客户端/服务器模型

完成通信路径需要两个套接字。当两个进程通信时，它们使用客户端/服务器模型来建立连接。图 1-1 说明了这一概念。服务器应用程序在系统上的特定端口监听——服务器由系统运行的 IP 地址和它监听连接的端口号完全标识。客户端从任何可用的端口发起连接，并尝试连接到服务器（由 IP 地址和端口号标识）。当连接建立后，客户端和服务器可以根据各自的协议交换数据。

![](img/792720823146d68f19fd50c99ebfce4b_593_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_593_1.png)

基于套接字的数据交换的事件序列取决于传输是面向连接（TCP）还是无连接（UDP）。

对于使用套接字的面向连接的数据传输，服务器在特定端口监听，等待客户端请求连接。只有在连接建立后，数据传输才会开始。

对于无连接的数据传输，服务器等待数据报到达指定端口。客户端不等待建立连接；它只是向服务器发送数据报。

无论是服务器还是客户端，每个应用程序首先创建一个套接字。然后它将套接字`关联`（绑定）到本地计算机的 IP 地址和端口号。IP 地址标识机器（应用程序运行的地方），端口号标识使用套接字的应用程序。

- `记住`
  - 服务器通常监听一个众所周知的端口号，以便客户端可以连接到该端口来访问服务器。对于客户端应用程序，将套接字绑定到 IP 地址和端口的过程与服务器相同，但客户端可以使用 0 作为端口号——套接字库自动为客户端使用一个未使用的端口号。

对于面向连接的流套接字，通信的客户端和服务器应用程序必须建立连接。建立连接的具体步骤取决于应用程序是服务器还是客户端。

- `记住`
  - 在客户端/服务器模型中，在客户端运行之前，服务器必须已启动并正在运行。在创建套接字并将套接字绑定到端口之后，服务器应用程序建立一个连接队列，这决定了多少客户端可以连接到服务器。通常，服务器监听一到五个连接。然而，监听队列的大小是一个你可以调整的参数（特别是对于 Web 服务器），以确保服务器尽可能多地响应客户端。在建立监听队列之后，服务器等待来自客户端的连接。

从客户端建立连接相对简单一些。在创建套接字并将套接字绑定到 IP 地址之后，客户端与服务器建立连接。为了建立连接，客户端必须知道服务器的主机名或 IP 地址，以及服务器接受连接的端口。所有互联网服务都有众所周知的标准端口号。

- `技术细节`
  - 在客户端通过面向连接的流套接字与服务器建立连接之后，客户端和服务器可以通过调用适当的套接字 API 函数来交换数据。就像两个人之间的对话一样，服务器和客户端交替发送和接收数据——数据的含义取决于服务器和客户端使用的消息协议。通常，服务器是为特定任务设计的；该设计中固有服务器和客户端用于交换必要数据的消息协议。例如，Web 服务器和 Web 浏览器（客户端）使用 HTTP（超文本传输协议）进行通信。

# 互联网服务和端口号

TCP/IP 协议套件是互联网的`通用语言`，因为互联网服务都`使用` TCP/IP。这些服务通过实现邮件、新闻和网页的传输来驱动互联网的运转。每个互联网服务都有自己独立的协议，并依赖 TCP/IP 完成信息的实际传输。每个服务还有一个或多个分配的端口号，用于执行其设计的功能。以下是一些常见的互联网服务及其相关协议：

- `DHCP（动态主机配置协议）` 用于动态配置计算机上的 TCP/IP 网络参数。DHCP 主要用于分配动态 IP 地址以及其他网络信息（如名称服务器、默认网关和域名），这些信息对于配置 TCP/IP 网络是必需的。DHCP 服务器在端口 67 上监听。
- `FTP（文件传输协议）` 用于在 Internet 上的计算机之间传输文件。FTP 使用两个端口：数据在端口 20 上传输，控制信息在端口 21 上交换。
- `HTTP（超文本传输协议）` 用于将文档从一个系统发送到另一个系统。HTTP 是 Web 的基础协议。默认情况下，Web 服务器和客户端在端口 80 上进行通信。
- `SMTP（简单邮件传输协议）` 用于在系统之间交换电子邮件消息。SMTP 使用端口 25 进行信息交换。
- `NNTP（网络新闻传输协议）` 用于以存储和转发的方式在 Internet 上分发新闻文章。NNTP 使用端口 119。
- `SSH（安全外壳协议）` 是一种在不安全网络上实现安全远程登录和其他安全网络服务的协议。SSH 使用端口 22。
- `TELNET` 允许一个系统的用户登录到 Internet 上的另一个系统。（用户必须提供有效的用户 ID 和密码才能登录到远程系统。）TELNET 默认使用端口 23。但是，TELNET 客户端可以连接到任何指定的端口。
- `NFS（网络文件系统）` 用于在计算机之间共享文件。NFS 使用 Sun 的远程过程调用（RPC）机制，通过端口 111 交换信息。
- `NTP（网络时间协议）` 被客户端计算机用于将系统时间与拥有更精确时钟的服务器进行同步。NTP 使用端口 123。
- `SNMP（简单网络管理协议）` 用于管理 Internet 上的所有类型网络设备。与 FTP 一样，SNMP 使用两个端口：161 和 162。
- `TFTP（简单文件传输协议）` 用于在系统之间传输文件。（它通常用于 X 终端和无盘工作站从网络上的另一台主机下载启动文件。）TFTP 数据传输发生在端口 69 上。



每个服务都由一个*服务器进程*提供——这是一个运行在系统上的计算机程序，等待到达与其服务相关联的知名端口的客户端请求。因此，Web 服务器期望在端口 80 上接收客户端请求，这是 HTTP 服务的标准端口。

Linux 系统中的 `/etc/services` 文本文件存储了服务名称与端口号（以及协议）之间的关联。以下是 Linux 系统 `/etc/services` 文件中的一个小部分条目：

```
ftp-data      20/tcp
ftp           21/tcp    fsp   21/udp
ssh           22/tcp    fspd  22/udp    # SSH Remote Login Protocol
ssh           22/udp
telnet        23/tcp
smtp          25/tcp    mail
time          37/tcp    timerserver
time          37/udp    timerserver
rhp           39/tcp    resource    # resource location
nameserver    42/tcp    name        # IEN 116
whos          43/udp    nicname
tacacs        49/tcp            # Login Host Protocol (TACACS)
```

快速浏览 `/etc/services` 文件中的条目，可以看出 TCP/IP 下可用的网络服务的广度。

> **注意：** 端口号 80 被指定用于 Web 服务。换句话说，如果你在系统上设置了一个 Web 服务器，该服务器将监听*端口* 80。顺便一提，IANA（Internet 号码分配机构，*www.iana.org*）是负责协调 1,024 以下端口号分配的组织。

![](img/792720823146d68f19fd50c99ebfce4b_596_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_596_1.png)

![](img/792720823146d68f19fd50c99ebfce4b_596_2.png)

![](img/792720823146d68f19fd50c99ebfce4b_596_3.png)

![](img/792720823146d68f19fd50c99ebfce4b_596_4.png)

## 使用 *互联网超级服务器*

互联网服务的客户端/服务器架构要求，在客户端发出服务请求之前，服务器必须已启动并运行。一直运行所有服务器可能是一个坏主意——因为每个服务器进程都会消耗系统资源（内存和处理器时间），这是不切实际的。此外，你并不真正需要*所有*服务始终保持激活状态。解决此问题的一个智能方案是运行一个监听所有端口的单一服务器，当客户端请求进来时，再启动相应的服务器。这种服务器被称为*互联网超级服务器*，因为它按需启动各种服务。

![](img/792720823146d68f19fd50c99ebfce4b_597_0.png)

有两个互联网超级服务器——`inetd` 和 `xinetd`。`inetd` 服务器较老，仍被一些 Linux 发行版（如 Debian、Knoppix、MEPIS、Ubuntu 和 Xandros）使用。`xinetd` 服务器是 `inetd` 的替代品，提供改进的访问控制和日志功能。`xinetd` 的名字代表 `inetd` 的*扩展版*。Fedora Core 和 SUSE 等发行版使用 `xinetd`。

## 使用 inetd

在使用 `inetd` 的 Linux 发行版中，系统在启动时会启动 `inetd`。`inetd` 服务器在启动时读取名为 `/etc/inetd.conf` 的配置文件。此文件告知 `inetd` 监听哪些端口，并为每个端口启动哪个服务器。例如，在我的一台 Linux 系统中，`/etc/inetd.conf` 文件中启动 IMAP（Internet 消息访问协议）服务器的条目看起来像这样：

```
imaps stream tcp nowait root /usr/sbin/tcpd /usr/sbin/imapd
```

这一行的第一项 `imaps` 告知 `inetd` 服务的名称。`inetd` 使用此名称从 `/etc/services` 文件中查找端口号。如果你输入 `grep imaps /etc/services`，你会发现 IMAP 服务的端口号是 993。这告知 `inetd` 在端口 993 上监听 IMAP 服务请求。

IMAP 条目中的其余字段含义如下：

- 条目的第二和第三字段 `stream` 和 `tcp` 告知 `inetd` IMAP 服务使用面向连接的 TCP 套接字与客户端通信。对于使用无连接 UDP 套接字的服务，这两个字段说明为 `dgram` 和 `udp`。
- 第四字段 `nowait` 告知 `inetd` 为每个请求启动一个新的服务器。如果此字段说明为 `wait`，`inetd` 会等待服务器退出后再重新启动服务器。
- 第五字段提供了 `inetd` 用于运行服务器的用户 ID。在这种情况下，服务器以 `root` 身份运行 IMAP 服务器。
- 第六字段指定了为该服务运行的程序，最后一个字段是 `inetd` 传递给服务器程序的参数。在这种情况下，`/usr/sbin/tcpd` 程序被提供了 `/usr/sbin/imapd` 作为参数。

![](img/792720823146d68f19fd50c99ebfce4b_597_1.png)

`/usr/sbin/tcpd` 程序是一个访问控制设施——称为 *TCP wrapper*——用于互联网服务。由于不必要的互联网服务往往是安全漏洞的来源，你可能想要关闭任何不需要的服务，或者至少控制对服务的访问。`tcpd` 程序可以启动其他服务，如 `FTP` 和 `TELNET`，但在启动服务之前，`tcpd` 会查阅 `/etc/hosts.allow` 文件，以查看请求服务的宿主是否被允许使用该服务。如果 `/etc/hosts.allow` 中关于该宿主没有任何信息，tcpd 会检查 `/etc/hosts.deny` 文件，以查看是否应拒绝该服务。如果两个文件都为空，tcpd 允许宿主访问所请求的服务。你可以在 `/etc/hosts.deny` 文件中放置 ALL:ALL 这一行，以拒绝所有宿主访问任何互联网服务。

![](img/792720823146d68f19fd50c99ebfce4b_598_0.png)

浏览你系统中的 `/etc/inetd.conf` 文件，了解 inetd 被设置启动的服务类型。如今，大多数 inetd 服务已被关闭，许多其他服务（如 FTP）由独立服务器启动。无论如何，如果你看到任何想要关闭的服务，只需在这些服务行首放置一个井号 (`#`) 即可。当你对 `/etc/inetd.conf` 文件做出此类更改时，输入 `/etc/init.d/inetd restart` 以重启 inetd 服务器。

## 使用 xinetd

使用 xinetd 的 Linux 发行版在系统启动时启动 xinetd。xinetd 服务器在启动时读取名为 `/etc/xinetd.conf` 的配置文件。此文件告知 xinetd 监听哪些端口，并为每个端口启动哪个服务器。该文件可以包含指令以引入其他配置文件。在 Linux 中，`/etc/xinetd.conf` 文件如下所示：

```
# Simple configuration file for xinetd
# Set some defaults and include /etc/xinetd.d/defaults
{
            instances            = 30
            log_type             = FILE /var/log/xinetd.log
            log_on_success       = HOST EXIT DURATION
            log_on_failure       = HOST ATTEMPT
            cps                  = 50 10
}
includedir /etc/xinetd.d
```

注释行以井号 (`#`) 开头。用花括号 ( { . . . } ) 包围的属性默认值块，指定了一些属性的默认值。这些默认值适用于配置文件中所有其他服务。instances 属性设置为 30，这意味着对于任何服务，最多可以有 30 个服务器同时处于活动状态。

![](img/792720823146d68f19fd50c99ebfce4b_598_1.png)



`/etc/xinetd.conf`文件中的最后一行使用`includedir`指令来包含`/etc/xinetd.d`目录内的所有文件，但以点`.`开头的文件除外。其理念是`/etc/xinetd.d`目录包含所有服务配置文件——为`xinetd`服务器预期管理的每种类型的服务设置一个文件。输入`ls /etc/xinetd.d`可查看你系统的`xinetd`配置文件。`/etc/xinetd.d`中的每个文件都指定了`xinetd`可以启动的一个服务的属性。

# 574 使用互联网超级服务器

![](img/792720823146d68f19fd50c99ebfce4b_599_0.png)

例如，SUSE Linux 使用`xinetd`来启动某些服务，其中包括`vsftpd` FTP 服务器。输入`cat /etc/xinetd.d/vsftpd`即可查看`vsftpd`服务的`xinetd`配置。以下是在 SUSE 系统上该文件的一个典型列表：

```
# default:  off
# description:
# The vsftpd FTP server serves FTP connections. It uses
# normal, unencrypted usernames and passwords for authentication.
# vsftpd is designed to be secure.
service ftp
{
    socket_type     = stream
    protocol        = tcp
    wait            = no
    user            = root
    server          = /usr/sbin/vsftpd
}
```

文件名在本例中为`vsftpd`可以是任意名称；重要的是文件中出现在`service`关键字旁边的服务名称。在本例中，`service ftp`这一行告知`xinetd`该服务的名称。`xinetd`使用此名称从`/etc/services`文件中查找端口号。

`/etc/xinetd.d/vsftpd`中由花括号`{ ... }`包围的属性具有以下含义：

- `socket_type`属性设置为`stream`，这告知`xinetd` FTP 服务使用面向连接的 TCP 套接字与客户端通信。对于使用无连接 UDP 套接字的服务，此属性设置为`dgram`。
- `wait`属性设置为`no`，这告知`xinetd`为每个请求启动一个新的服务器。如果将此属性设置为`yes`，`xinetd`会等待服务器退出后再重新启动服务器。
- `user`属性提供`xinetd`用于运行服务器的用户 ID。在本例中，服务器以`root`身份运行 TELNET 服务器。
- `server`属性指定了用于此服务的程序。在本例中，`xinetd`运行`/usr/sbin/vsftpd`程序以提供 FTP 服务。

浏览 Linux 系统中`/etc/xinetd.d`目录下的文件，以了解`xinetd`被设置为启动哪些类型的服务。如果您想关闭任何服务，许多服务默认已禁用，可以编辑该服务的配置文件，并在包含所有属性的花括号内添加以下行：

```
disable          =  yes
```

当您对*xinetd*配置文件进行此类更改时，必须通过输入以下命令来重新启动*xinetd*服务器：

```
/etc/init.d/xinetd restart
```

![](img/792720823146d68f19fd50c99ebfce4b_600_0.png)

> **注意：** 通常可以配置服务以在*xinetd*下运行或作为独立服务运行。例如，SUSE 在*xinetd*的控制下启动 Very Secure FTP 服务器*vsftpd*。然而，Debian 和 Fedora Core 将*vsftpd*作为独立服务器运行。

## 运行独立服务器

通过*inetd*或*xinetd*启动服务器是一种明智的方法，但如果服务必须频繁启动，这种方式并不*高效*。如果 Web 服务器由*inetd*或*xinetd*控制，那么每次用户在网页上点击链接时，Web 服务都会收到请求，从而频繁启动该服务器，这种情况将变得非常不利。对于此类高需求的服务，最好以独立方式启动服务器。在独立模式下，服务器可以作为*守护进程*daemon运行——这是一个持续运行且永不终止的进程。这意味着服务器监听分配的端口，每当收到请求时，服务器通过复制自身来处理请求。以这种方式，只要机器在运行，服务器就会一直运行——理论上，可以永远运行。一种更高效的策略常用于 Web 服务器是运行多个服务器副本，让每个副本处理部分传入请求。

您可以轻松地配置 Linux 系统以自动启动各种独立服务器。本节将向您展示如何操作。

### 手动启动和停止服务器

要启动未运行的服务，请使用*服务器命令*。例如，如果 Web 服务器在 Fedora Core 中称为*httpd*未运行，您可以通过运行一个特殊的 shell 脚本并输入以下命令来启动它：

```
/etc/init.d/httpd start
```

该命令运行`/etc/init.d/httpd`脚本，并将`start`作为参数。如果*httpd*服务器已经在运行，而您想停止它，请运行相同的命令并将`stop`作为参数，如下所示：

```
/etc/init.d/httpd stop
```

若要停止服务器并再次启动它，只需使用`restart`作为参数：

```
/etc/init.d/httpd restart
```

### 在启动时自动启动服务器

您可以使用`/etc/init.d`目录中的脚本手动启动、停止和重启服务器，但您可能希望某些服务在启动 Linux 系统时立即启动。您可以通过使用图形化的服务器配置工具或命令来配置服务器在启动时自动运行。

配置服务以自动启动的命令取决于发行版。在 Debian、MEPIS、Knoppix、Ubuntu 和 Xandros 中，请使用`update-rc.d`命令。在 Fedora Core 和 SUSE 中，请使用`chkconfig`命令。我在以下部分解释了这两个命令。

#### 在 Fedora Core 和 SUSE 中使用 chkconfig 命令

`chkconfig`程序是 Fedora Core 和 SUSE 中用于检查和更新 Linux 中服务器当前设置的命令行实用程序。各种服务器组合被设置为在不同的运行级别自动启动。每个运行级别代表一种系统配置，其中运行选定的进程集合。您通常关心运行级别 3 和 5，因为运行级别 3 用于文本模式登录，而运行级别 5 用于通过图形界面登录。

`chkconfig`命令易于使用。例如，假设您希望在运行级别 3 和 5 自动启动`named`服务器。您只需以 root 身份登录并在 shell 提示符下输入以下命令：

```
chkconfig --level 35 named on
```

要查看`named`服务器的状态，请输入以下命令：

```
chkconfig --list named
```

您会看到类似以下输出的一行：

```
named  0:off  1:off  2:off  3:on  4:off  5:on  6:off
```

输出显示了`named`服务器在运行级别 0 到 6 的状态。如您所见，`named`被设置为在运行级别 3 和 5 运行。

如果您想关闭`named`，可以使用此命令：

```
chkconfig --level 35 named off
```

您可以使用`chkconfig`查看所有服务的状态，包括通过`xinetd`启动的服务。例如，您可以通过输入以下命令查看所有服务的状态：

```
chkconfig --list | more
```

输出显示了每个服务在运行级别 0 到 6 中的状态。对于每个运行级别，服务要么开启要么关闭。在列表的最后，`chkconfig`显示了一个由`xinetd`控制的服务列表。每个基于`xinetd`的服务也根据`xinetd`是否配置为启动该服务而标记为开启或关闭。

#### 在 Debian、Knoppix、MEPIS、Ubuntu 和 Xandros 中使用 update-rc.d 命令

在 Debian、Knoppix、MEPIS、Ubuntu 和 Xandros 中，您可以使用`update-rc.d`命令来设置应在系统以特定启动级别启动时运行的服务。设置的最简单方式是使用如下形式的命令中的`defaults`选项：

```
update-rc.d service defaults
```

其中`service`是`/etc/init.d`目录中启动和停止服务的脚本文件的名称以及其他功能。



当您使用 `defaults` 选项时，`update-rc.d` 设置符号链接——即快捷方式——以在运行级别 2、3、4 和 5 中启动服务，并在运行级别 0、1 和 6 中停止服务。序列号控制每个服务启动的顺序。（序列号较小的服务先于序列号较大的服务启动，数字通常从 00 到 99。）如果您未明确指定序列号，使用 `defaults` 选项时 `update-rc.d` 会使用序列号 20。

你还可以在特定的运行级别以及按特定顺序启动和停止服务。例如，要在运行级别 2 和 5 以序列号 85 启动服务，并在运行级别 0、1 和 6 以序列号 90 停止服务，请使用以下命令：

```
update-rc.d service start 85 2 5 . stop 90 0 1 6 .
```

请记住，`service` 必须是 `/etc/init.d` 目录中脚本文件的名称。

![](img/792720823146d68f19fd50c99ebfce4b_603_0.png)

如果你需要阻止某个服务在系统启动时启动，请在终端窗口中输入 `update-rc.d -f service remove`，其中 `service` 是 `/etc/init.d` 目录中启动或停止该服务的脚本文件的名称。

## 使用 GUI 服务配置工具

如果你不喜欢输入命令，可以尝试使用 GUI 工具来配置服务。Fedora Core 和 SUSE 都包含用于管理服务的此类工具。

![](img/792720823146d68f19fd50c99ebfce4b_603_1.png)

在 Fedora Core 中，从 GUI 桌面选择 **System → Administration → Server Settings → Services**（系统 → 管理 → 服务器设置 → 服务），并在提示时输入 root 密码。然后，你可以从“服务配置”窗口中开启或关闭服务，如图 1-2 所示。

服务配置工具在滚动列表中显示服务的名称。列表中的每一行显示一个服务的名称，名称前面有一个复选框。复选框中的选中标记表示该服务被选中以在当前运行级别下于启动时开启。当对话框首次出现时，许多服务已经被选中。

你可以上下滚动列表并点击复选框来选择或取消选择服务。如果你点击复选框，选中标记会交替开启和关闭。要了解有关服务的更多信息，点击服务名称以在窗口右侧显示简要描述。例如，图 1-2 显示了 `acpid` 服务的帮助文本。此外，该工具还会显示所选服务当前是否正在运行。

选择完所有希望在系统启动时开启的服务后，点击工具栏上的 **Save**（保存）按钮以保存更改。然后选择 **File → Quit**（文件 → 退出）以退出。

![](img/792720823146d68f19fd50c99ebfce4b_603_2.png)

默认情况下，服务配置工具为当前运行级别配置所选服务。这意味着如果你正从图形桌面选择服务，则系统处于运行级别 5，且你配置的服务被设置为在运行级别 5 下启动。如果你想为不同的级别设置服务，请从 **Edit Runlevel**（编辑运行级别）菜单中选择该运行级别。

![](img/792720823146d68f19fd50c99ebfce4b_604_0.png)

在 Fedora Core 中，这是你设置服务以便在启动时自动启动的地方。

在 SUSE 中，你可以从左侧窗口中的 **YaST Control Center → Main Menu → System → Control Center (YaST) → YAST System**（YaST 控制中心 → 主菜单 → 系统 → 控制中心 (YaST) → YaST 系统）配置服务，然后点击 **System Services (Runlevel)**（系统服务（运行级别））。YAST 会打开 **System Services (Runlevel)**（系统服务（运行级别））窗口（参见图 1-3），在那里你可以启用或禁用服务。要在特定运行级别启用或禁用服务，请点击 **Expert Mode**（专家模式）按钮，并在新出现的列表中编辑服务。

![](img/792720823146d68f19fd50c99ebfce4b_604_1.png)

在 SUSE 中，使用此 YaST 窗口指定在启动时启动的服务。

表 1-1 列出了服务清单以及每个服务的简要描述。第一列显示服务名称，该名称与提供该服务必须运行的程序名称相同。你在系统中运行 GUI 服务配置工具时可能不会看到列出的所有服务，因为服务的具体列表取决于你的 Linux 系统上安装了什么。

**表 1-1 Linux 中的一些常见服务**

| 服务名称 | 描述 |
| :--- | :--- |
| acpid | 监听内核发出的高级配置和电源接口（ACPI）事件，并在发生此类事件时通知其他程序。当内核将计算机置于低功耗状态（例如，待命模式）以节省能源时，可能会发生 ACPI 事件。 |
| apache, apache2, or httpd | Apache 万维网（WWW）服务器 |
| apmd | 监控高级电源管理（APM）BIOS 并记录电源状态（交流电或电池备用） |
| atd | 运行由 `at` 和 `cron` 命令调度的命令 |
| autofs | 自动挂载文件系统（例如，当你在 CD-ROM 驱动器中插入 CD-ROM 时） |
| cron or crond | 根据由 `crontab` 命令设置的周期性时间表运行用户指定的程序 |
| gpm | 启用在文本模式屏幕中使用鼠标 |
| innnd | InterNetNews 守护进程——你可以用于支持系统本地新闻组的 Internet 新闻服务器 |
| isdn | 启动和停止 ISDN（综合业务数字网）服务——一种在普通电话线上的数字通信服务（仅在拥有 ISDN 服务时启用） |
| named | 域名系统（DNS）服务器，将主机名转换为 IP 地址。如果你愿意，可以在你的系统上运行一个副本。 |
| network or networking | 允许你激活或停用在系统启动时配置为启动的所有网络接口 |
| nfs or nfsserver | 使用网络文件系统（NFS）协议启用在 `/etc/exports` 文件中指定的文件系统的共享 |
| nfslock | 为使用网络文件系统（NFS）协议导出的文件系统提供文件锁定功能，以便其他系统（运行 NFS）可以共享你系统中的文件 |
| pcmcia | 提供对 PCMCIA 设备的支持 |
| portmap | 被任何依赖远程过程调用（RPC）的软件使用的服务器。例如，NFS 需要 portmap 服务。 |
| samba, smb, or smbfs | 启动和停止 Samba 的 `smbd` 和 `nmbd` 服务，这些服务在 Linux 系统上支持 LAN 管理器服务 |
| sendmail | 将邮件消息从一台机器移动到另一台。如果你希望从你的 Linux 系统发送邮件，请启动此服务。如果你不打算将你的 Linux 系统用作邮件服务器，请不要启动 `sendmail` 服务器，因为它可能会减慢启动过程并消耗不必要的资源。 |
| snmpd | 用于网络管理功能的简单网络管理协议（SNMP）服务 |
| spamassassin | 运行 `spamd`——SpamAssassin 邮件过滤程序 |
| ssh or sshd | OpenSSH（安全 Shell）安全远程登录设施的服务器 |
| syslog or syslogd | 许多其他程序（包括其他服务）用于在日志文件（通常是 `/var/log/messages` 文件）中记录各种错误和状态消息的服务。始终运行此服务。 |
| vsftpd | 使用文件传输协议（FTP）进行文件传输的非常安全的 FTP 守护进程 |
| winbind | 启动和停止 Samba 的 `winbind` 服务器，该服务器提供类似于 `/etc/nsswitch.conf` 文件提供的名称切换功能 |
| xfs | 启动和停止 X 字体服务器的服务器 |
| xinetd | Internet 超级服务器，旧版 `inetd` 的替代品。它会在需要时启动其他 Internet 服务，例如 TELNET 和 FTP。 |
| ypbind | 运行在网络信息系统（NIS）客户端上并将客户端绑定到 NIS 域的服务。除非你正在使用 NIS，否则无需启动 `ypbind`。 |

# 第 2 章：运行 Web 服务器

## 本章内容

- 理解 HTTP
- 安装 Apache Web 服务器
- 配置 Apache Web 服务器
- 使用 Apache Web 服务器支持虚拟主机



万维网（WWW 或 Web）通过使浏览存储在各个 Internet 主机上的文档变得容易，将 Internet 推向了主流，因为 Web 浏览器让用户可以轻松浏览。无论你是经营小生意还是为一家大公司管理计算机系统和网络，你很可能都需要设置和维护一个 Web 服务器。由于 Linux 个人计算机具有内置的网络支持，它是一台价格实惠的 Web 服务器。本章描述如何在 Linux 个人计算机上配置 Apache Web 服务器。

## 理解 HTTP

Web 服务器使用 HTTP 提供信息。Web 服务器也被称为 HTTP 守护进程（因为持续运行的服务器进程在 UNIX 中被称为守护进程），或者简称为 HTTPD。Web 服务器程序通常命名为 `apache`、`apache2` 或 `httpd`，具体取决于你的 Linux 发行版。

HTTP 代表超文本传输协议。超文本部分指的是 Web 页面包含超文本链接的事实。传输协议部分指的是在网络上将一个 Web 页面从一台计算机传输到另一台计算机的标准约定。虽然你真正理解 HTTP 并不是设置 Web 服务器或使用 Web 浏览器的必要条件，但了解其工作原理确实有助于你理解 Web 是如何运作的。

你可以通过使用 TELNET 程序连接到 Web 服务器监听的端口来获得 HTTP 的亲身体验。在大多数系统上，Web 服务器监听端口 80 并响应发送到该端口的任何 HTTP 请求。因此，你可以使用 TELNET 程序连接到一个系统（如果它有 Web 服务器）的 80 端口，并尝试一些 HTTP 命令。

## HTTP 是互联网标准吗？

尽管自 1990 年以来 HTTP 在 Web 中得到了广泛使用，但直到最近它才成为互联网标准。所有互联网标准首先都以注释请求（RFC, Request for Comment）的形式分发。第一份与 HTTP 相关的 RFC 是 RFC 1945，“超文本传输协议 — HTTP/1.0”（T. Berners-Lee、R. Fielding 和 H. Frystyk，1996 年 5 月）。然而，RFC 1945 被视为信息性文档，而非标准。

RFC 2616，“超文本传输协议 — HTTP/1.1”（R. Fielding、J. Gettys、J. Mogul、H. Frystyk、L. Masinter、P. Leach、T. Berners-Lee，1999 年 6 月）是 HTTP 的草案互联网标准。

要阅读这些 RFC，请将你的 Web 浏览器指向 `www.ietf.org/rfc/` 或 `www.faqs.org/rfcs`。

要了解有关 HTTP/1.1 和其他与 Web 相关的标准的更多信息，请使用 Web 浏览器访问 `www.w3.org/protocols`。

要查看 HTTP 工作示例，请遵循以下步骤：

- **1. 确保你的 Linux 电脑连接到互联网的连接处于活动状态。**

  - 例如，如果你使用 PPP，请确保已建立连接。如果你拥有宽带电缆或 DSL 连接，你的连接很可能是始终开启的。

- **2. 输入以下命令。（我使用一个美国政府网站 URL 来说明 HTTP 协议的工作原理。）**

  ```
  telnet www.gao.gov 80
  ```

- **3. 当你看到“已连接...”消息后，输入以下 HTTP 命令并按两次 Enter 键：**

  ```
  GET / HTTP/1.0
  ```

  - 作为对此 HTTP 命令的响应，Web 服务器返回一些有用信息，随后是默认 HTML 文件（通常称为 `index.html`）的内容。

以下是在我对美国政府网站执行 GET 命令时所得到的结果。（在下文中，我标出了你需要输入 GET 命令的位置。）

```text
Trying 161.203.16.2...
Connected to www.gao.gov.
Escape character is '^]'.
GET / HTTP/1.0    (输入此行并按两次 Enter 键)
```

```text
HTTP/1.1 200 OK
Date: Wed, 14 Dec 2005 22:53:26 GMT
Server: Apache
Connection: close
Content-Type: text/html; charset=ISO-8859-1
```

```html
<html>
<head>
<title>The Government Accountability Office</title>
... (删除的行) ...
</head>
<body>
...
(删除的行)
...
</body>
</html>
```

连接被远程主机关闭。

当你使用 TELNET 尝试这个示例时，你会看到 Web 服务器确切发送回给 Web 浏览器的内容。前几行是为浏览器提供的管理信息。服务器返回这些信息：

- 一行显示服务器使用的 HTTP 协议版本为 1.1，状态码为 200 表示成功：

  ```
  HTTP/1.1 200 OK
  ```

- 当前日期和时间。日期和时间字符串示例如下：

  ```
  Date: Wed, 14 Dec 2005 22:53:26 GMT
  ```

- Web 服务器软件的名称、版本及其他详细信息。如今，常见的做法是仅显示软件的通用名称（例如 `Apache`），而不提供其他详细信息，因为某人可能会利用版本信息来攻击该版本的特定漏洞。

- Web 服务器返回的文档类型。对于 HTML 文档，内容类型报告如下：

  ```
  Content-Type: text/html; charset=ISO-8859-1
  ```

文档本身位于管理信息之后。HTML 文档具有以下一般布局：

```html
<html>
<head>
<title>文档标题在此处</title>
</head>
<body 属性在此处 >
... 文档其余部分在此处
</body>
</html>
```

你可以通过查看显示 Web 服务器响应 GET 命令内容的列表来识别此布局。由于示例使用 telnet 命令获取文档，因此你会以文本行的形式看到 HTML 内容。如果你使用 Web 浏览器（如 Mozilla Firefox）访问同一个网站（www.gao.gov），你会看到如图 2-1 所示的页面图形形式。

HTTP 命令示例展示了 GET 命令的结果。GET 是最常用的 HTTP 命令；它使服务器返回指定的 HTML 文档或图像。

另外两个 HTTP 命令是 HEAD 和 POST。HEAD 命令几乎与 GET 相同：它使服务器返回文档中除正文以外的所有内容。POST 命令向服务器发送信息；如何操作这些信息由服务器决定。

![](img/792720823146d68f19fd50c99ebfce4b_611_0.png)

**图 2-1：** 通过 Web 浏览器查看的 www.gao.gov 网站。

## 探索 Apache Web 服务器

你可能已经知道如何使用 Web，但你可能不知道如何设置 Web 服务器，以便你也能够通过网页向全世界提供信息。要成为 Web 上的信息提供者，你需要在互联网上的 Linux 电脑上运行一个 Web 服务器。你还必须为你网站准备网页——这可能比设置 Web 服务器更具挑战性。

在可用的 Web 服务器中，Apache Web 服务器是最流行的，并且适用于所有 Linux 发行版。Apache Web 服务器最初是 NCSA HTTPD 服务器的改进版本，但很快发展成为独立开发项目。与 NCSA HTTPD 一样，Apache 服务器由协作团队开发和维护。Apache 可通过互联网免费获取。

### 安装 Apache Web 服务器

根据你在安装 Linux 发行版时所做的选择，Apache Web 服务器可能已安装在你的系统中。如果已安装，它可能已在运行，或者你需要启动它。例如，Apache Web 服务器在 Knoppix 和 Xandros 中已安装，但默认情况下未开启。

![](img/792720823146d68f19fd50c99ebfce4b_612_0.png)

Apache Web 服务器的软件包名称在不同发行版中有所不同——Fedora Core 称其为 `httpd`，而 Knoppix 和 Xandros 称其为 `apache`。Debian 和 SUSE 称该软件包为 `apache2`。要查看 Apache Web 服务器是否已安装，在 Debian、Knoppix、MEPS 和 Xandros 中键入 `dpkg -l apache*`，在 Ubuntu 中键入 `sudo dpkg -l apache*`。如果在显示以 `apache` 开头的软件包名称的输出第一列中看到 `ii` 或 `pn`，则说明它已完全或部分安装。在 Fedora Core 中，键入 `rpm -q httpd`。在 SUSE 中，键入 `rpm -q apache2`。

![](img/792720823146d68f19fd50c99ebfce4b_612_1.png)



如果 Web 服务器未安装，你可以轻松安装它。步骤取决于你的 Linux 发行版。在 Debian 和 MEPIS 中，以 `root` 身份登录并键入 `apt-get install apache2`，在 Ubuntu 中键入 `sudo apt-get install apache2`。在 Fedora Core 中，挂载随附 DVD 并通过键入以下命令安装 Apache Web 服务器：

```bash
cd /media/cdrom/Fedora/RPMS
rpm -ivh httpd*
```

### 为什么叫 Apache？

根据 `www.apache.org/foundation/faq.html` 上关于 Apache Web 服务器项目的信息，Apache 小组于 1995 年 3 月由一些提供补丁文件的人成立，这些补丁文件旨在修复 NCSA HTTPD 1.3 中的错误。将补丁应用于 NCSA HTTPD 后的结果就是他们所称的*补丁服务器*（Apache 名称的由来）。Apache 小组现在已演变为 Apache 软件基金会（ASF），这是一个于 1999 年 6 月在美国特拉华州注册的非营利公司。ASF 还有其他正在进行的项目。你可以在 `www.apache.org` 上阅读关于这些项目的介绍。特别是，请访问 `http://httpd.apache.org` 以获取更多关于 Apache Web 服务器项目的信息。

根据 `2005 年 8 月 Netcraft Web 服务器调查`（位于 `http://news.netcraft.com/archives/web_server_survey.html`），Apache Web 服务器是其中最受欢迎的 Web 服务器——`70,392,567` 个网站中 `69.46%` 的网站报告使用 Apache 服务器。`微软 Internet 信息服务（IIS）` 位居第二，占有 `20.43%` 的网站份额。

![](img/792720823146d68f19fd50c99ebfce4b_613_0.png)

在 SUSE 中，从 `YaST 控制中心` 中的 `软件` 类别点击 `安装和移除软件`——`主菜单：系统：控制中心（YaST）`——然后使用 YaST 的搜索功能查找 `apache`。找到想要的软件包后，选中它们并点击 `接受` 进行安装。

就这么简单！安装好 Apache Web 服务器后，你就可以运行它了。

### 启动 Apache Web 服务器

即使 Apache Web 服务器已安装，它也可能未设置开机自动启动。如果你想尝试使用它，你必须启动服务器。

![](img/792720823146d68f19fd50c99ebfce4b_613_1.png)

要启动 Apache Web 服务器，以 `root` 身份登录并键入 `/etc/init.d/apache2 start`。在 Debian、MEPIS、Ubuntu 和 SUSE 中，在 Fedora Core 中键入 `service httpd start`。在 Knoppix 和 Xandros 中，键入 `/etc/init.d/apache2 start`。如果你希望在启动时自动启动 Apache Web 服务器，在 Debian、MEPIS 和 Ubuntu 中键入 `update-rc.d apache2 defaults`。在 Knoppix 和 Xandros 中，键入 `update-rc.d apache2 defaults`。在 Fedora Core 中，键入 `chkconfig -levels 35 httpd on`。在 SUSE 中，键入 `chkconfig -levels 35 apache2 on`。

要查看服务器是否正在运行，键入 `ps ax | grep processname`，其中 `processname` 在 Fedora Core 和 SUSE 中为 `httpd`，在 Debian、Knoppix 和 Xandros 中为 `apache`。如果在输出中看到多个 Web 服务器进程，则一切正常。运行多个 Web 服务器进程——一个父进程和多个子进程——是一种常见方法，以便通过为每个请求分配一个 Web 服务器进程来高效地处理多个 HTTP 请求。

如果 `ps ax` 的输出未显示任何 Web 服务器进程，则错误可能隐藏在 Apache 配置文件中。若情况如此，你必须修复配置文件中的任何问题，并重新启动服务器。

如果 Web 服务器正在运行，你可以使用 TELNET 程序连接到 80 端口，查看服务器是否正常工作。开始在终端窗口中输入以下命令：

```
telnet localhost 80
```

当收到 `Connected` 消息后，输入：

```
HEAD / HTTP/1.0
```

然后按两次 Enter。你会得到一个类似的响应，当然日期和数字会有所不同：

```
HTTP/1.1 200 OK
Date: Sat, 17 Dec 2005 20:57:20 GMT
Server: Apache/2.0.54 (Fedora)
Last-Modified: Sat, 17 Dec 2005 20:57:05 GMT
ETag: "156946-25b-8f6d64a0"
Accept-Ranges: bytes
Content-Length: 603
Connection: close
Content-Type: text/html; charset=UTF-8

Connection closed by foreign host.
```

该响应显示了一些关于 Web 服务器和默认主页的信息。你还可以通过在 Linux 系统上运行 Web 浏览器（例如 Firefox）来检查 Web 服务器。使用 URL `http://localhost/` 并查看发生的情况。

![](img/792720823146d68f19fd50c99ebfce4b_614_0.png)

如果在 Web 浏览器中尝试 `http://localhost/` URL 时收到错误消息，这意味着由 `DocumentRoot` 配置指令指定的目录中没有 `index.html` 文件（默认 Web 页面）。要修正此问题，只需在适当的目录（查看 HTTP 服务器配置文件中由 `DocumentRoot` 指定的目录名称）中创建一个名为 `index.html` 的简单 HTML 文档。我将在下一节中解释诸如 `DocumentRoot` 这样的配置指令。

## 配置 Apache Web 服务器

Apache Web 服务器程序文件和配置文件在不同的发行版中存储在不同的位置。Apache Web 服务器配置文件在 Fedora Core、Knoppix、SUSE 和 Xandros 中名为 `httpd.conf`，而在 Debian、MEPIS 和 Ubuntu 中名为 `apache2.conf`。配置文件是一个文本文件，其中包含指定 Web 服务器各个方面的指令。

![](img/792720823146d68f19fd50c99ebfce4b_615_0.png)

在 Debian、MEPIS、SUSE 和 Ubuntu 中，配置文件位于 `/etc/apache2` 目录。在 Fedora Core 中，`httpd.conf` 文件位于 `/etc/httpd/conf` 目录。在 Knoppix 和 Xandros 中，文件位于 `/etc/apache` 目录。

包含 `httpd.conf` 文件的目录还包含有关安全套接字层（SSL）实现需求的信息。（SSL 实现作为 Apache Web 服务器的一部分提供。）

### 使用 Apache 配置工具

在某些 Linux 发行版中，你可以使用图形用户界面工具来配置 Apache Web 服务器。特别是，Fedora Core 和 SUSE 附带了用于配置 Apache Web 服务器的 GUI 工具。我将在本节中向你介绍这些 GUI 工具。

![](img/792720823146d68f19fd50c99ebfce4b_615_1.png)

在 Fedora Core 中，以 `root` 身份登录，并从 GUI 桌面选择“系统管理”>“服务器设置”>“HTTP”。将出现 HTTP 对话框，如图 2-2 所示。

![](img/792720823146d68f19fd50c99ebfce4b_615_2.png)

图 2-2：在 Fedora Core 中，从此对话框配置 Apache HTTP 服务器。

Apache 配置对话框分为四个选项卡。你可以从这些选项卡中的每一个设置各种选项：

- 主选项卡（Main）：从此选项卡中，你可以指定 Apache 期望接收 Web 服务请求的 IP 地址和端口号。你还可以设置 Webmaster 的电子邮件地址。



- **虚拟主机（Virtual Hosts）：** 在这里你可以设置虚拟主机。（我将在本章稍后讨论虚拟主机的选项。）你还可以编辑适用于所有虚拟主机的默认设置。在“虚拟主机”选项卡上单击“编辑默认设置”按钮会弹出另一个对话框（如图 2-3 所示），你可以从中设置许多不同的选项。

- **服务器（Server）：** 此选项卡包含服务器设置，例如 HTTP 服务器运行在其中的用户和组名，以及存储进程 ID 的文件位置。

- **性能调优（Performance Tuning）：** 在此选项卡中，你可以设置一些控制整体性能的参数。你可以设置允许的最大连接数、连接超时时间以及每个连接的最大请求数。

![](img/792720823146d68f19fd50c99ebfce4b_616_0.png)

最初，配置窗口显示配置文件 `/etc/httpd/conf/httpd.conf` 中的默认值。进行任何更改后，单击“确定”按钮。配置工具会提示你是否确实要保存更改并退出。如果是，请单击“是”，然后完成。

在 SUSE 中，选择“主菜单”>“控制中心”（YaST）以打开 YaST 控制中心。在窗口的左侧单击“网络服务”，然后在右侧单击“HTTP 服务器”。YaST 将打开 HTTP 服务器向导窗口，如图 2-4 所示，并引导你通过一个五步过程来配置 HTTP 服务器。步骤如下：

![](img/792720823146d68f19fd50c99ebfce4b_616_1.png)

1. 确定服务器监听的网络接口。
2. 指定要加载用于特定脚本语言（如 Perl、Python、PHP4 或 Ruby）的模块。
3. 指定一系列配置指令，例如文档和配置文件的位置。
4. 配置任何虚拟主机。
5. 启动 HTTP 服务器。

YaST 的好处在于，它会自动安装配置和运行 HTTP 服务器所需的其他任何内容（例如 Apache 模块）。

![](img/792720823146d68f19fd50c99ebfce4b_617_0.png)

当你使用 GUI 配置工具配置 Apache HTTP 服务器时，你所做的只是更改存储在 Apache Web 服务器配置文件中的选项和属性（在 Debian、MEPIS 和 Ubuntu 中为 `/etc/apache2/apache2.conf`；在 Fedora Core 中为 `/etc/httpd/conf/httpd.conf`；在 Knoppix 和 Xandros 中为 `/etc/apache/httpd.conf`；在 SUSE 中为 `/etc/apache2/httpd.conf` 以及 `/etc/apache2` 目录中所有的 `.conf` 文件）。你同样可以轻松通过编辑配置文件来进行更改，配置文件是一个纯文本文件。在接下来的几节中，我将向你介绍 Apache 配置文件中的一些常见配置指令。

## Apache 配置文件的语法

Apache 服务器的操作由位于取决于你发行版的目录中的 `httpd.conf`（或在 Debian 和 Ubuntu 中为 `apache2.conf`）文件控制。配置文件控制服务器如何运行、提供哪些文档以及谁可以访问这些文档。

在接下来的几节中，我将总结有关 Apache Web 服务器配置文件的关键信息。通常，你不需要更改配置文件中的任何内容来运行 Apache Web 服务器。然而，了解配置文件的格式以及其中使用的各种关键字的含义是很有用的。

在你研究 Apache Web 服务器配置文件时，请记住以下语法规则：

- 每个配置文件都是文本文件，你可以用你喜欢的文本编辑器进行编辑，并使用 `more` 命令查看。
- 所有注释行都以 `#` 开头。
- 每行只能有一个指令。
- 额外的空格和空行将被忽略。
- 通常，主配置文件通过使用 `Include` 指令包含许多其他配置文件。
- 除了路径名和 URL 外，所有条目均不区分大小写。

## Apache Web 服务器配置文件

`httpd.conf` 文件（或在 Debian 中为 `apache2.conf`）是主 HTTP 守护进程配置文件——它包含控制 Apache Web 服务器运行方式的指令。通常，配置文件通过引用一个名为 `Include` 的指令来包含其他几个配置文件。

配置文件指定服务器使用的端口号、网站名称以及服务器出现问题时发送邮件的电子邮件地址。此外，配置文件指定 Web 页面的位置以及谁可以访问哪些目录。

在下面的部分中，我将 Apache 指令分为三个单独类别：通用 HTTPD 指令、资源配置指令和访问控制指令。最后，我解释了如何设置 Apache Web 服务器中的虚拟主机，以便单个 Web 服务器可以处理发送到多个 IP 地址或主机名的 Web 请求。

# 594 配置 Apache Web 服务器

> 提示：若要在线浏览 Apache HTTPD 文档，请访问 http://httpd.apache.org/docs/2.0/。具体而言，你可以在 http://httpd.apache.org/docs-2.0/mod/directives.html 上查找关于配置指令的信息。

### 通用 HTTPD 指令

以下是来自 Apache Web 服务器配置文件中的一些有趣条目：

- `ServerAdmin` 是 Web 服务器在发生任何错误时提供给客户端的电子邮件地址。`ServerAdmin` 的默认值是 `root@localhost`。将此地址设置为一个有效的电子邮件地址，以便互联网上的任何人都可以使用它来报告你的 Web 站点可能存在的任何错误。
- `Include` 从指定文件中加载更多的配置指令。例如，在 Fedora Core 中，默认的 `/etc/httpd/conf/httpd.conf` 文件使用以下 `Include` 指令加载 `/etc/httpd/conf.d` 目录中的所有配置文件：

`Include conf.d/*.conf`

这条命令意味着你只需向 `/etc/httpd/conf.d` 目录中添加文件即可加载另一组配置。实际上，该目录是存放各种 Apache HTTPD 模块（如 Perl、PHP 和 SSL）配置文件的地方。在 Fedora Core 中，研究 `/etc/httpd/conf.d` 目录中的配置文件，以了解影响 Apache Web 服务器行为的完整指令集。

还有许多指令控制着 Apache Web 服务器的工作方式。下面的列表总结了你可以在 `httpd.conf` 文件中使用的某些指令。你可以保持这些指令中的大多数为默认设置，但如果你正在维护 Web 服务器，了解它们很重要。

- `Listen` *IP-Address:Port*：强制 Web 服务器监听特定的 IP 地址和端口号。默认情况下，Web 服务器会响应与主机关联的所有 IP 地址。
- `User` *name [ #id]*：指定 HTTP 守护进程使用的用户名（或 ID）。你可以将此指令保持为默认设置（`apache`）。如果你指定用户 ID，请使用哈希号（#）前缀表示数字 ID。
- `Group` *name [ #id]*：指定以独立模式运行时的 HTTP 守护进程组名（或 ID）。默认组名为 `apache`。
- `ServerRoot` *pathname*：指定 Web 服务器的配置和日志文件预期所在的目录。在 Debian、MEPIS、SUSE 和 Ubuntu 中，`ServerRoot` 为 `/etc/apache2`。在 Fedora Core 中，`ServerRoot` 设置为 `/etc/httpd`。在 Knoppix 和 Xandros 中，`ServerRoot` 为 `/etc/apache`。
- `ServerName` *www.company.com:80*：将服务器的主机名设置为 `www.company.com`，端口号设置为 80。`ServerName` 仅在重定向 Web 页面到另一个页面时使用。
- `ServerTokens` *Major|Minor|Min|OS|Full*：控制在响应头的 Server 字段中返回给客户端的信息量。将指令设置为 `Prod`，以便 Server 响应仅识别产品名称（在此情况下为 Apache）。
- `StartServers` *num*：设置 Apache Web 服务器运行后立即启动的子进程数量。默认值为 5。
- `MaxSpareServers` *num*：设置所需的空闲子服务器进程的最大数量。（如果子进程未处理 HTTP 请求，则被视为空闲。）默认值为 20。
- `MinSpareServers` *num*：设置所需的空闲子服务器进程的最小数量。（如果子进程未处理 HTTP 请求，则被视为空闲。）如果数量低于此阈值，每秒钟都会创建一个新的备用进程。默认值为 5。
- `Timeout` *numsec*：设置服务器在客户端建立连接后等待客户端发送查询的秒数。默认超时时间为 300 秒（五分钟）。



- **ErrorLog** *filename*：设置 httpd 记录其遇到的错误的文件。如果文件名不以斜杠 (`/`) 开头，则名称被视为相对于 `ServerRoot`。在 Fedora Core 中，默认的 `ErrorLog` 是 `/var/log/httpd/error_log`，在 SUSE 中是 `/var/log/apache2/error_log`。在 Debian、MEPIS 和 Ubuntu 中，错误日志位于 `/var/log/apache2/error.log`。在 Knoppix 和 Xandros 中，错误日志位于 `/var/log/apache/error.log`。典型的错误日志条目包括事件，如服务器重启和任何警告消息。

- **TransferLog** *filename*：设置 httpd 记录所有客户端访问（包括失败的访问）的文件。

- **LogFormat** *formatstring formatname*：指定 `TransferLog` 日志文件条目的格式。`CustomLog` 指令也使用此格式来生成特定格式的日志。

- **CustomLog** *filename formatname*：设置自定义日志文件的名称，httpd 在该文件中记录所有客户端访问（包括失败的访问），格式由 `formatname` 指定（你使用 `LogFormat` 指令定义 `formatname`）。

- **PidFile** *filename*：设置 httpd 存储其进程 ID 的文件。

## 第七卷

## 第二章

## 运行 Web 服务器

- **MaxClients** *num*：设置可以同时连接到服务器的客户端数量限制。默认值为 150。`MaxClients` 的值不能超过 256。

- **LoadModule** *module modules/modfile.so*：加载作为动态共享对象（DSO）构建的模块。你必须指定模块名称和模块的对象文件。由于模块加载的顺序很重要，请保持这些指令在默认配置文件中的位置不变。*注意：* `mod_ssl` 模块提供使用安全套接字层（SSL）协议进行加密的支持。

### 资源配置指令

资源配置指令指定 Web 页面的位置，以及如何指定各种文件的数据类型。开始时，你可以将这些指令保持在默认设置。以下是 Apache Web 服务器的一些资源配置指令：

- **DocumentRoot** *pathname*：指定 HTTP 服务器查找 Web 页面的目录。在 Debian 中，默认的 `DocumentRoot` 是 `/var/www/apache2-default`。在 Fedora Core 中，`DocumentRoot` 是 `/var/www/html`。在 SUSE 中，`DocumentRoot` 是 `/srv/www/htdocs`。在 Knoppix 和 Xandros 中，`DocumentRoot` 是 `/var/www`。如果你将 HTML 文档放在其他目录中，请将 `DocumentRoot` 设置为该目录。

- **UserDir** *dirname*：指定用户主目录下的子目录，当 URL 中出现用户名时（例如，在诸如 `http://www.xyz.net/~naba` 这样的 URL 中，包含带有波浪号前缀的用户名），HTTP 服务器在该子目录中查找 Web 页面。默认情况下，通过将 `dirname` 设置为 disable 来关闭 `UserDir` 功能。如果你希望启用它，可以将其设置为 `public_html`，这意味着用户的 Web 页面位于该用户主目录下的 `public_html` 子目录中。`UserDir` 默认禁用，因为它会使文件系统向外界开放。Apache 文档建议在 `httpd.conf` 文件中添加以下行：

```
UserDir disabled root
```

- **DirectoryIndex** *filename filename2 ...*：指示当客户端未指定文档时，服务器返回默认文件或文件。默认的 `DirectoryIndex` 是 `index.html`。如果 Apache Web 服务器找不到该文件，并且该目录允许索引，则返回该目录的索引（基本上是一个美观的文件列表）。

- **AccessFileName** *filename*：指定可能出现在包含文档的每个目录中，并指示谁有权访问该目录内容的文件的名称。默认的 `AccessFileName` 是 `.htaccess`。此文件的语法与 Apache 访问控制指令相同，我将在下一节中讨论。

- **AddType** *type/subtype extension*：将文件扩展名与 MIME 数据类型（形式为 *type/subtype*，如 `text/plain` 或 `image/gif`）关联。因此，如果要让服务器将具有 `.lst` 扩展名的文件视为 纯文本 文件，请指定以下内容：

```
AddType text/plain .lst
```

默认的 MIME 类型和扩展名列在 `/etc/mime.types` 文件中。

- **AddEncoding** *type extension*：将编码类型与文件扩展名关联。如果要让服务器将结尾为 `.gz` 或 `.tgz` 的文件标记为使用 `x-gzip` 编码方法（GZIP 编码的标准名称）编码，请指定以下内容：

```
AddEncoding x-gzip gz tgz
```

- **DefaultType** *type/subtype*：指定如果服务器无法从文件扩展名确定类型时使用的 MIME 类型。如果你未指定 `DefaultType`，Apache Web 服务器假设 MIME 类型为 `text/html`。在默认的 `httpd.conf` 文件中，`DefaultType` 指定为 `text/plain`。

- **Redirect** *requested-file actual-URL*：指定任何对 *requested-file* 的请求都重定向到 *actual-URL*。

- **Alias** *requested-dir actual-dir*：指定服务器使用 *actual-dir* 来定位 *requested-dir* 目录中的文件。（换句话说，*requested-dir* 是 *actual-dir* 的别名。）要使对 `/icons` 目录的请求转到 `/usr/share/apache2/icons/`，请指定以下内容：

```
Alias /icons/ "/usr/share/apache2/icons/"
```

- **ScriptAlias** *requested-dir actual-dir*：指定通用网关接口（CGI）脚本所在目录的实际名称。例如，如果配置文件包含此指令

```
ScriptAlias /cgi-bin/ "/srv/www/cgi-bin/"
```

这意味着当 Web 浏览器请求脚本（如 `/cgi-bin/test-cgi`）时，HTTP 服务器运行脚本 `/srv/www/cgi-bin/test-cgi`。

- **DefaultIcon** *iconfile*：指定服务器为没有图标信息的文件使用的默认图标的位置。

# 598 配置 Apache Web 服务器

- **ReadmeName** `filename`：指定一个 README 文件的名称，其内容将附加到自动生成的目录列表末尾。默认的 `ReadmeName` 是 `README`。

- **HeaderName** `filename`：指定一个页眉文件的名称，其内容将前置到自动生成的目录列表之前。默认的 `HeaderName` 是 `HEADER`。

- **AddDescription** “`file description`” `filename`：指定在目录列表中文件名旁边显示的文件描述字符串。你可以使用通配符（例如 `*.html`）作为文件名。例如，以下指令将扩展名为 `.tgz` 的文件描述为 GZIP 压缩的 tar 归档文件：

```apache
AddDescription “GZIP compressed tar archive” .tgz
```

- **AddIcon** `iconfile` `extension1` `extension2` ...：将一个图标与一个或多个文件扩展名相关联。以下指令将图标文件 `/icons/text.gif` 与文件扩展名 `.txt` 相关联：

```apache
AddIcon /icons/text.gif .txt
```



### AddIconByType `iconfile` `MIME-types`
将一个图标与一组以 MIME 类型通配符形式（例如 `text/*` 或 `image/*`）指定的文件类型相关联。要将图标文件 `/icons/text.gif` 与所有文本类型相关联，请指定以下内容：

```apache
AddIconByType (TXT, /icons/text.gif) text/*
```

该指令还告知服务器，对于无法接受图像的客户端，使用 `TXT` 代替图标。（浏览器会告知服务器它们可以接受的数据类型。）

### AddIconByEncoding `iconfile` `encoding1` `encoding2` ...
指定为一种或多种编码类型（例如 `x-compress` 或 `x-gzip`）显示的图标。

### IndexIgnore `filename1` `filename2` ...
指示服务器在准备目录列表时忽略指定的文件名（这些名称通常包含通配符）。要排除 `README`、`HEADER` 以及所有以句点（`.`）、尾随波浪号（`~`）或尾随井号（`#`）开头的文件，请指定以下内容：

```apache
IndexIgnore .??* *~ \*# HEADER\* README\* RCS CVS *,v ,t
```

### IndexOptions `option1` `option2` ...
指示你希望在服务器准备的目录列表中包含的选项。选项可以包括以下一个或多个：

- `FancyIndexing` 开启精美的目录列表，其中包含代表文件类型、大小和最后修改日期的文件名和图标。
- `IconHeight=N` 指定图标的高度为 *N* 像素。
- `IconWidth=N` 指定图标的宽度为 *N* 像素。
- `NameWidth=N` 使文件名列宽为 *N* 个字符。
- `IconsAreLinks` 使图标像链接一样起作用。
- `ScanHTMLTitles` 显示 HTML 文件的描述。
- `SuppressHTMLPreamble` 不向页眉文件（由 `HeaderName` 指令指定）添加标准的 HTML 序言。
- `SuppressLastModified` 停止显示最后修改日期。
- `SuppressSize` 停止显示文件大小。
- `SuppressDescription` 停止显示任何文件描述。
- `SuppressColumnSorting` 停止列标题成为启用列排序的链接。

### ErrorDocument `errortype` `filename`
指定当发生特定类型的错误时服务器发送的文件。你也可以为错误提供文本消息。以下是一些示例：

```apache
ErrorDocument 403 "Sorry, you cannot access this directory"
ErrorDocument 403 /error/noindex.html
ErrorDocument 404 /cgi-bin/bad_link.pl
ErrorDocument 401 /new_subscriber.html
```

如果你没有 `ErrorDocument` 指令，服务器将发送内置的错误消息。`errortype` 可以是以下 HTTP/1.1 错误条件之一。（更多信息请参阅 `www.ietf.org/rfc/rfc2616.txt` 或 `www.faqs.org/rfcs/rfc2616.html` 中的 RFC 2616。）

- 400: 错误请求
- 401: 未授权
- 402: 需要付款
- 403: 禁止
- 404: 未找到
- 405: 方法不允许
- 406: 不可接受
- 407: 需要代理认证
- 408: 请求超时
- 409: 冲突
- 410: 已消失
- 411: 长度要求
- 412: 先决条件失败
- 413: 请求实体过大
- 414: 请求 URI 过长
- 415: 不支持的媒体类型
- 416: 请求范围无法满足
- 417: 期望失败
- 500: 内部服务器错误
- 501: 未实现
- 502: 坏网关
- 503: 服务不可用
- 504: 网关超时
- 505: 不支持的 HTTP 版本

### TypesConfig `filename`
指定包含文件扩展名到 MIME 数据类型的映射的文件。（MIME 代表多用途互联网邮件扩展，是一种在单个消息文件中打包附件的方法。）服务器向客户端报告这些 MIME 类型。如果你未指定 `TypesConfig` 指令，`httpd` 假设 `Types Config` 文件是 `/etc/mime.types`。以下是默认 `/etc/mime.types` 文件中的几行示例：

```text
application/msword              doc
application/pdf                 pdf
application/postscript          ai eps ps
application/x-tcl               tcl
audio/mpeg                      mpga mp2 mp3
audio/x-pn-realaudio            ram rm
audio/x-wav                     wav
image/gif                       gif
image/jpeg                      jpeg jpg jpe
image/png                       png
text/html                       html htm
text/plain                      asc txt
video/mpeg                      mpeg mpg mpe
```

每一行显示 MIME 类型（例如 `text/html`），后跟该类型的文件扩展名（`html` 或 `htm`）。

## 访问控制指令

访问控制指令使你可以控制谁可以访问系统中的不同目录。这些是全局访问配置指令。你还可以拥有另一个访问配置文件，该文件名由 `AccessFileName` 指令指定，位于 Apache Web 服务器可以提供服务文档的每个目录中。（该*每目录*访问配置文件默认命名为 `.htaccess`。）

去除大部分注释行后，访问控制指令具有如下格式：

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
    Order allow,deny
    Allow from all
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

访问控制指令使用与其他 Apache 指令不同的语法。这种语法类似于 HTML。各种访问控制指令封装在成对的标签中，例如 `<Directory> ... </Directory>`。

以下列表描述了一些访问控制指令。特别是注意 `AuthUserFile` 指令；你可以为特定目录设置基于密码的访问控制。

### `Options` `opt1` `opt2` ...
指定此指令所在目录部分的访问控制选项。选项可以是以下一个或多个：

- `None` 禁用所有访问控制功能。
- `All` 开启目录的所有功能。
- `FollowSymLinks` 允许服务器跟随符号链接（换句话说，就是快捷方式）。
- `SymLinksIfOwnerMatch` 仅当目录的所有者拥有链接目录时，才跟随符号链接。



- **ExecCGI** 允许在目录中执行 CGI 脚本。

- **Includes** 允许在此目录中使用服务器端包含文件。（术语 *server-side include* 指的是放置在 HTML 文件中、在 Web 服务器将结果返回给 Web 浏览器之前处理的指令。）

- **Indexes** 允许客户端请求该目录的索引（目录列表）。

- **IncludesNOEXEC** 禁用服务器端包含中的 `#exec` 命令。

- **`AllowOverride` `directive1` `directive2` ...**：指定哪些访问控制指令可以在每目录基础上被覆盖。指令列表可以包含以下一个或多个：

  - **None** 阻止任何指令被覆盖。

  - **All** 允许在任何指令上按每目录基础进行覆盖。

  - **Options** 允许在目录级文件中使用 *Options* 指令。

  - **FileInfo** 允许使用控制文档类型的指令，例如 *AddType* 和 *AddEncoding*。

  - **AuthConfig** 允许使用授权指令，例如 *AuthName*、*AuthType*、*AuthUserFile* 和 *AuthGroupFile*。

  - **Limit** 允许在目录的访问配置文件中使用的 *Limit* 指令（*allow*、*deny* 和 *order*）。

- **`AuthName` `name`**：指定目录的授权名称。

- **`AuthType` `type`**：指定要使用的授权类型。唯一支持的授权类型是 *Basic*。

- **`AuthUserFile` `filename`**：指定存储用于授权的用户名和密码的文件。例如，以下指令将授权文件设置为 `/etc/httpd/conf/passwd`：

```apache
AuthUserFile /etc/httpd/conf/passwd
```

你必须使用 `/usr/bin/htpasswd` 支持程序创建授权文件。要创建授权文件并添加名为 *jdoe* 用户的密码，请指定以下内容：

```bash
/usr/bin/htpasswd -c /etc/httpd/conf/passwd jdoe
```

![](img/792720823146d68f19fd50c99ebfce4b_626_0.png)

当提示输入密码时，请输入密码，并通过再次键入该密码进行确认。

- **AuthGroupFile fileName**：指定用于查找用户组列表以进行身份验证的文件。

- **order ord**：指定两个其他指令——*allow*（允许）和 *deny*（拒绝）——的评估顺序。顺序必须是以下之一：

  - *deny,allow* 使 Web 服务器在评估 *allow* 指令之前先评估 *deny* 指令。

  - *allow,deny* 使 Web 服务器在评估 *deny* 指令之前先评估 *allow* 指令。

  - *mutual-failure* 仅允许 *allow* 列表中的主机访问。

- **deny from host1 host2...**：指定被拒绝访问的主机。

- **allow from host1 host2...**：指定被允许访问的主机。若要允许特定域中的所有主机访问目录中的 Web 文档，请指定以下内容：

```
order deny,allow
allow from .nws.noaa.gov
```

- **require entity en1 en2...**：此指令指定哪些用户可以访问目录。*entity*（实体）是以下之一：

  - *user*（用户）仅启用命名用户列表。

  - *group*（组）仅启用命名组列表。

  - *valid-user*（有效用户）允许列在 *AuthUserFile* 中的所有用户访问目录（前提是他们输入了正确的密码）。

## 虚拟主机设置

Apache HTTP 服务器的一项实用功能是它可以处理虚拟 Web 服务器。*虚拟托管*（Virtual hosting）仅仅意味着单个 Web 服务器可以响应许多不同的 IP 地址，并根据 IP 地址从不同的目录提供 Web 页面。这意味着你可以设置一个 Web 服务器来同时响应 www.big.org 和 www.tiny.com，并为每个主机名提供唯一的首页。具备此功能的服务器被称为 *多宿主*（multi-homed）Web 服务器、*虚拟* Web 服务器，或支持 *虚拟主机* 的服务器。

正如你可能猜测的那样，互联网服务提供商（ISP）利用 Apache Web 服务器的虚拟主机功能向客户提供虚拟网站。支持虚拟主机需要满足以下条件：

- Web 服务器必须能够响应多个 IP 地址（每个 IP 地址具有唯一的主机名），并且必须允许你为每个 IP 地址指定文档目录、日志文件和其他配置项。

- 宿主系统必须能够将多个 IP 地址关联到单个物理网络接口。Linux 可以做到这一点。

- 与 IP 地址关联的每个主机名必须是一个唯一的、已注册的主机名，并拥有正确的 DNS 条目。

有关如何在 Apache HTTP 服务器中设置虚拟主机的最新信息，请参阅以下 URL：

```
http://httpd.apache.org/docs-2.0/ vhosts
```

Apache HTTP 服务器可以用不同的首页响应不同的主机名。在支持虚拟主机时，你有两个选项：

- **运行多个 httpd 程序副本，每个 IP 地址对应一个：**在这种情况下，你为每个主机创建一个单独的 httpd.conf 配置文件副本，并使用 *Listen* 指令使服务器响应特定的 IP 地址。

- **使用单个 httpd.conf 文件运行单个 httpd 程序副本：**在配置文件中，将 *Listen* 设置为仅端口号（这样服务器会响应与宿主关联的任何 IP 地址），并使用 *VirtualHost* 指令为每个虚拟主机配置服务器。

只有在你不预期系统上有大量流量时，才运行多个 HTTP 守护进程；由于运行多个守护进程带来的开销，系统可能无法很好地响应。然而，如果每个虚拟主机对以下指令有独特的配置需求，你可能需要多个 HTTP 守护进程：

- *UserId* 和 *GroupId*（HTTP 守护进程的用户和组 ID）

- *ServerRoot*（服务器的 *root*（根）目录）

- *TypesConfig*（MIME 类型配置文件）

对于流量较大的站点，配置 Web 服务器以让单个 HTTP 守护进程服务于多个虚拟主机。当然，这一建议意味着只有一个配置文件。在该配置文件中，使用 *VirtualHost* 指令来配置每个虚拟主机。

大多数 ISP 使用 Apache HTTP 服务器的 *VirtualHost* 能力向客户提供虚拟网站。除非你付费获得专用的 Web 主机，否则你通常获得的是虚拟站点，在那里你拥有自己的域名，但与许多其他客户共享服务器和实际宿主。

*VirtualHost* 指令的语法如下：

```
<VirtualHost hostaddr> 
 ... directives that apply to this host
...</VirtualHost>
```

使用此语法，你使用 `<VirtualHost>` 和 `</VirtualHost>` 来包裹一组仅适用于由 hostaddr 参数标识的特定虚拟主机的指令。hostaddr 可以是 IP 地址或虚拟主机的完全限定域名。

你可以在 `<VirtualHost>` 块内放置几乎任何 Apache 指令。至少，网站管理员在 `<VirtualHost>` 块中包含以下指令：

- DocumentRoot，指定该虚拟主机的文档所在位置

- ServerName，向外部世界标识服务器（此名称是 DNS 支持的已注册域名）

- ServerAdmin，该虚拟主机网站管理员的电子邮件地址

- Redirect，指定要重定向到其他 URL 的任何 URL

- ErrorLog，指定记录与该虚拟主机相关的错误的文件

- CustomLog，指定记录对该虚拟主机访问的文件

当服务器接收到针对特定虚拟主机的 DocumentRoot 目录中某文档的请求时，它使用该服务器 `<VirtualHost>` 块内的配置参数来处理该请求。

以下是一个典型的 `<VirtualHost>` 指令示例，用于设置虚拟主机 www.insoft.com。



```
<VirtualHost www.insoft.com>
     DocumentRoot          /home/naba/httpd/htdocs
     ServerName            www.insoft.com
     ServerAdmin           webmaster@insoft.com
     ScriptAlias           /cgi-bin/   /home/naba/httpd/cgi-bin/
     ErrorLog              /home/naba/httpd/logs/error_log
     CustomLog             /home/naba/httpd/logs/access_log common
</VirtualHost>
```

在此处，`CustomLog` 指令中的名称 `common` 指的是之前在 `httpd.conf` 文件中由 `LogFormat` 指令定义的一种格式的名称，如下所示：

```
LogFormat "%h %l %u %t \"%r\" %>s %b" common
```

此日志格式字符串会在日志文件中生成看起来像这样的行：

```
dial236.dc.psn.net - - [13/Dec/2005:18:09:00 -0500] "GET / HTTP/1.0" 200 1243
```

格式字符串包含两个以百分号（`%`）开头的字母令牌。这些令牌的含义如表 2-1 所示。

**表 2-1 LogFormat 令牌**

| *令牌* | *含义* |

| :--- | :--- |

| `%b` | 发送给客户端的字节数，不包括头部信息 |

| `%h` | 客户端机器的主机名 |

| `%l` | 用户的身份（如果可用） |

| `%r` | 来自客户端的 HTTP 请求（例如，GET / HTTP/1.0） |

| `%s` | Web 服务器的响应代码 |

| `%t` | 当前的本地日期和时间 |

| `%u` | 用户提供的用户名（仅在访问控制规则要求用户名/密码身份验证时） |

# 第 3 章：设置 FTP 服务器

## 本章内容

- 安装 FTP 服务器
- 配置 FTP 服务器

**文件传输协议**（FTP）是一项用于在系统之间传输文件的流行互联网服务。*匿名 FTP*（Anonymous FTP）是用于分发文件的另一项流行互联网服务。匿名 FTP 的美妙之处在于，如果远程系统支持匿名 FTP，任何人可以使用 *anonymous*（匿名）用户 ID 使用 FTP 并从该系统下载文件。尽管匿名 FTP 对分发数据很有用，但如果设置不当，它会带来安全风险。

Linux 发行版通常附带几个 FTP 客户端以及由 Chris Evans 编写的 Very Secure FTP 守护进程（`vsftpd`）。FTP 服务器通常包含支持匿名 FTP 所需的文件。在本章中，我将展示你如何通过文本配置文件配置 `vsftpd` FTP 服务器，以及如何控制对 FTP 服务器的访问。

### 安装 FTP 服务器

根据你在 Linux 安装过程中所做的选择，FTP 服务器 `vsftpd` 及其配置文件可能已经安装在你的系统上。如果未安装 `vsftpd`，你可以轻松安装它。

在 Debian 和 Xandros 中，输入 `dpkg -l *ftp*` 以查看是否已安装 FTP 服务器。在 Fedora Core 和 SUSE 中，输入 `rpm -qa | grep vsftp` 并查看是否已安装 `vsftpd` 包。

在 Debian 和 MEPIS 中，输入 `apt-get install vsftpd` 以安装 FTP 服务器。在 Ubuntu 中，输入 `sudo apt-get install vsftpd`。在 Fedora Core 中，以 `root` 身份登录，挂载 DVD，然后输入 `cd /media/cdrom/Fedora/RPMS`，接着输入 `rpm -vh vsftpd*`。在 SUSE 中，点击 YaST 控制中心软件类别中的软件管理。然后使用 YaST 的搜索功能找到 `vsftpd` 并安装它。在 Xandros 中，首先运行 Xandros Network，选择编辑→设置应用程序源，并点击 Debian Unsupported Site 链接作为源；然后你可以使用 `apt-get install vsftpd` 命令来安装 Very Secure FTP 服务器。

## vsftpd 配置文件

Very Secure FTP 守护进程（**vsftpd**）在 `/etc` 目录（以及在 Fedora Core 的 `/etc/vsftpd` 目录中）使用了一系列配置文件。默认情况下，**vsftpd** 服务器是禁用的——如果你想使用 FTP 服务器，首先必须启用它。在本节中，我将向你展示如何操作。

![](img/792720823146d68f19fd50c99ebfce4b_633_0.png)

**vsftpd** 服务器可以配置为独立模式运行，或在 **xinetd** 服务器的控制下运行。在 Debian 和 Fedora Core 中，**vsftpd** 被设置为作为独立进程运行。在 SUSE 中，**vsftpd** 在 **xinetd** 的控制下运行。在 Debian 和 Fedora Core 中，你可以通过键入 `/etc/init.d/vsftpd start` 来启动 **vsftpd**。在 SUSE 中，编辑文件 `/etc/xinetd.d/vsftpd`——确保其中没有 `disable = yes` 这一行——然后键入 `/etc/init.d/xinetd restart` 以重启 **xinetd**。

要在系统启动时启动 **vsftpd**，请在 Debian 中键入 `update-rc.d vsftpd defaults`。在 Fedora Core 中，通过键入 `chkconfig --level 35 vsftpd on` 来启用 **vsftpd** 以自动启动。

启动 **vsftpd** 服务器后，默认设置足以让服务器发挥作用。这是因为其他 FTP 客户端现在可以连接并从你的 FTP 服务器请求文件。然而，为了以防万一你将来需要自定义这些设置，你需要了解这些配置文件。

**vsftpd** 服务器会查阅 `vsftpd.conf` 文件（在 Debian、SUSE 和 Xandros 中位于 `/etc`，在 Fedora Core 中位于 `/etc/vsftpd` 目录——请记住你首先必须在 Xandros 中安装 **vsftpd**）。该配置文件可能引用 `/etc` 目录中的其他文件。`vsftpd.conf` 文件控制 FTP 服务器的许多方面，例如它是否以独立模式运行、谁可以下载文件，以及是否允许匿名 FTP。以下是 **vsftpd** 的关键配置文件：

- `/etc/vsftpd.conf` 或 `/etc/vsftpd/vsftpd.conf` 控制 **vsftpd** 服务器的工作方式（例如，是否允许匿名登录、是否允许文件上传等）。
- `/etc/vsftpd.ftpusers`，如果存在，列出了无法访问 FTP 服务器的用户名称。
- `/etc/vsftpd.user_list`，如果存在，列出了被拒绝访问的用户名称（甚至不会提示输入密码）。然而，如果在 `/etc/vsftpd/vsftpd.conf` 中将 `user_list_deny` 选项设置为 `NO`，则允许这些用户访问 FTP 服务器。

![](img/792720823146d68f19fd50c99ebfce4b_634_0.png)

在 Debian、SUSE 和 Xandros 中，vsftpd 使用单个配置文件 `/etc/vsftpd.conf`。在 Fedora Core 中，vsftpd 的默认安装使用 `/etc/vsftpd/vsftpd.conf` 文件。

通常你可以保留大多数 vsftpd 配置文件的默认设置。不过，万一你需要更改某些设置以使 vsftpd 满足你的需求，我将在接下来的几个部分中简要介绍这些配置文件。

### vsftpd.conf 文件

要了解 `vsftpd.conf` 文件中可以包含哪些内容以及这些行如何影响 `vsftpd` 服务器的操作，请从查看默认安装的 `vsftpd.conf` 文件开始。该文件中的注释告诉你每个选项的作用。

默认情况下，`vsftpd` 几乎不允许任何操作。通过编辑 `vsftpd.conf` 中的选项，你可以放宽限制，以便用户可以使用 FTP。你可以决定设置的宽松程度。

以下是你可以在 `vsftpd.conf` 文件中设置的一些选项：

- `anon_mkdir_write_enable=YES` 允许匿名 FTP 用户创建新目录。此选项有风险，因为恶意用户可能通过创建过多目录耗尽你的硬盘空间。因此，即使你允许匿名用户上传文件，你可能也想要将此选项设置为 NO。



# vsftpd 配置选项

- `anon_upload_enable=YES` 表示匿名 FTP 用户可以上传文件。此选项仅在 `write_enable` 已设置为 `YES` 且目录对所有人具有写权限时才生效。请记住：允许匿名用户在你的系统上写入可能非常危险，因为用户可能会填满磁盘或将你的磁盘用作他们的个人存储。

- `anonymous_enable=YES` 启用匿名 FTP。（用户可以使用用户名 `anonymous` 登录，并将他们的电子邮件地址作为密码提供。）如果你不想要匿名 FTP，请注释掉这一行。

- `ascii_download_enable=YES` 启用 ASCII 模式下的文件下载。不幸的是，恶意远程用户可以发出带有巨大文件名称的 `SIZE` 命令，实际上导致 FTP 服务器浪费大量资源打开该文件并确定其大小。这种技术用于拒绝服务攻击。（有关拒绝服务 `DoS` 攻击的更多信息，请参阅第六卷第一章。）

- `ascii_upload_enable=YES` 启用 ASCII 模式下的文件上传（适用于文本文件）。

- `async_abor_enable=YES` 使 `vsftpd` 能够识别在任何时间到达的 `ABOR`（`abort`）请求。你可能需要启用它，以允许较旧的 FTP 客户端与 `vsftpd` 配合工作。

- `banned_email_file=/etc/vsftpd.banned_emails` 指定包含被禁止电子邮件地址列表的文件（仅当 `deny_email_enable` 设置为 `YES` 时使用）。

- `chown_uploads=YES` 使上传的匿名文件归属于由 `chown_username` 选项指定的另一个用户。除非绝对必要，否则不要启用此选项——并且不要将 `root` 指定为 `chown_username`。（那将是一场灾难。）如果由特定用户名运行的进程使用上传的文件，则你可能需要启用此选项，这意味着无论谁上传文件，所有者都必须更改为该进程预期的用户名。

- `chown_username=name` 指定拥有由匿名 FTP 用户上传文件的所有者用户名。

- `chroot_list_enable=YES` 使 `vsftpd` 在 FTP 服务登录时，将除 `chroot_list_file` 指定的列表中的用户以外的所有用户限制在其主目录中。此选项防止这些用户访问主目录之外的任何文件。默认情况下，`vsftpd` 在 `/etc/vsftpd.chroot_list` 文件中查找 chroot 用户列表，但你可以通过 `chroot_list_file` 选项指定文件名来覆盖此设置。

- `chroot_list_file=/etc/vsftpd.chroot_list` 是用户列表，根据 `chroot_local_user` 的设置，这些用户要么被限制在其主目录中，要么不被限制。

- `connect_from_port_20=YES` 使 `vsftpd` 确保数据传输通过 20 端口（FTP 数据端口）进行。

- `data_connection_timeout=120` 是非活动数据连接超时前的秒数。

- `deny_email_enable=YES` 使 `vsftpd` 检查被禁止的电子邮件地址列表，并拒绝任何试图使用被禁止的电子邮件地址作为密码匿名登录的人访问。默认情况下，`vsftpd` 期望被禁止的电子邮件地址位于 `/etc/vsftpd.banned_emails` 文件中，但你可以通过 `banned_email_file` 选项指定其他文件名。

- `dirmessage_enable=YES` 使 `vsftpd` 在 FTP 用户切换到特定目录时显示消息。

- `ftpd_banner=Welcome to my FTP service` 设置 `vsftpd` 在用户登录时显示的横幅。你可以将消息更改为任何你想要的内容。

- `idle_session_timeout=600` 是非活动会话（指某人连接但什么也不做的情况）超时并导致 `vsftpd` 注销用户的秒数。

- `listen=YES` 使 `vsftpd` 监听连接请求，并因此以独立模式运行。如果你希望 `vsftpd` 在 `xinetd` 下运行，请将此选项设置为 `NO`。

- `local_enable=YES` 使 `vsftpd` 允许本地用户访问 FTP。

- `local_umask=022` 意味着 FTP 写入的任何文件权限均为 644（对所有人有读取权限，但仅对所有者有写入权限）。你可以将其设置为任何你想要的文件权限掩码设置。例如，如果你希望除了所有者外任何人都没有权限，请将此选项更改为 `077`。（要了解有关文件权限掩码的更多信息，请查阅第六卷第二章。）

- `ls_recurse_enable=YES` 允许 FTP 用户通过使用 `ls -R` 命令递归遍历目录。

- `nopriv_user=ftp` 标识 FTP 服务器可以使用的非特权用户账户。

- `pam_service_name=vsftpd` 是当 `vsftpd` 必须对用户进行身份验证时使用的可插拔身份验证模块（PAM）配置文件的名称。默认情况下，PAM 配置文件位于 `/etc/pam.d` 目录中。这意味着 `vsftpd` 的 PAM 配置文件是 `/etc/pam.d/vsftpd`。

- `tcp_wrappers=YES` 启用通过 TCP 包装器的访问控制支持，该包装器查阅 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件。（有关 TCP 包装器的更多信息，请参阅第六卷第三章。）

- `userlist_deny=YES` 在 `userlist_enable` 设置为 `YES` 的情况下，使 `vsftpd` 拒绝访问列在 `/etc/vsftpd_user_list` 文件中的用户。这些用户甚至不会被提示输入密码。另一方面，如果你将 `userlist_deny=NO` 设置为，除非用户列在 `/etc/vsftpd_user_list` 文件中，否则他们将无法访问。

- `userlist_enable=YES` 使 `vsftpd` 从 `/etc/vsftpd_user_list` 文件读取用户列表，并拒绝这些用户访问 FTP 服务器，甚至不会提示输入密码。默认的用户列表是 `/etc/vsftpd_user_list`，但你可以通过 `userlist_file` 选项覆盖此设置。

- `write_enable=YES` 使 `vsftpd` 允许向主机上传文件。

- `xferlog_enable=YES` 开启文件下载和上传的日志记录（这始终是个好主意，但会占用磁盘空间）。

- `xfer_log_file=/var/log/vsftpd.log` 指定 `vsftpd` 日志文件的完整路径名。默认值为 `/var/log/vsftpd.log`。

- `xferlog_std_format=YES` 使 `vsftpd` 以其他 FTP 守护进程使用的标准格式生成日志文件。

## `/etc/vsftpd.ftpusers` 文件

当 `vsftpd` 服务器尝试让用户登录时，它使用 PAM 来验证用户（正如正常登录过程使用 PAM 来完成工作一样）。`vsftpd` 的 PAM 配置文件是 `/etc/pam.d/vsftpd`。该 PAM 配置文件以如下方式引用 `/etc/vsftpd.ftpusers`：

```text
auth    required      /lib/security/pam_listfile.so item=user sense=deny
          file=/etc/vsftpd.ftpusers sense=success
```

此命令基本上表示，任何列在 `/etc/vsftpd.ftpusers` 文件中的人都将被拒绝登录。

根据发行版的不同，`/etc/pam.d/vsftpd` 文件可能引用除 `/etc/vsftpd.ftpusers` 之外的其他文件名。例如，在 Fedora Core 中，`/etc/pam.d/vsftpd` 文件指定 `/etc/vsftpd/ftpusers` 作为包含被拒绝登录的用户名的文件，而 SUSE Linux 使用 `/etc/ftpusers` 文件列出不允许访问 `vsftpd` 的用户名。通常，该列表设置为拒绝与服务器相关而非真实用户的用户名（如 `root`、`news`、`uucp` 等）的 FTP 访问。

## `/etc/vsftpd.user_list` 文件

如果 `userlist_enable` 选项设置为 `YES` 且 `userlist_deny` 设置为 `YES`，`vsftpd` 不允许列在 `/etc/vsftpd.user_list` 文件中的用户访问任何 FTP 服务。它甚至不会提示他们输入密码。然而，如果 `userlist_deny` 设置为 `NO`，含义则相反，这些用户是允许访问的唯一用户。（但是，PAM 配置仍然拒绝任何在 `/etc/vsftpd.ftpusers` 列表中的人。）如果 `userlist_enable` 设置为 `NO`，则不使用 `/etc/vsftpd.user_list` 文件。



在 Fedora Core 中，`vsftpd` 使用 `/etc/vsftpd/user_list` 中的用户列表用于 `userlist_enable` 和 `userlist_deny` 选项。

# 第 4 章：管理邮件和新闻服务器

**本章内容**

- 安装和使用 `sendmail`
- 手动测试邮件投递
- 配置 `sendmail`
- 安装 InterNetNews (INN) 服务器
- 配置和启动 INN
- 设置本地新闻组

**电子**邮件（e-mail）是 Internet 主机上流行的服务之一。电子邮件软件分为两部分：邮件传输代理（MTA），它负责物理上发送和接收邮件消息；以及邮件用户代理（MUA），它负责读取消息和准备新消息。在本章中，我描述电子邮件服务，并展示如何在 Linux 个人计算机上配置 `sendmail` 服务器。
Internet 新闻组提供了除电子邮件之外的另一种便捷方式，用于讨论各种主题并与他人分享你的知识。Linux 附带了阅读新闻组和将你的系统设置为新闻服务器所需的软件。在本章中，我描述如何配置和运行流行的 InterNetNews 服务器。我还展示如何为你的企业内联网（甚至家庭网络）设置本地新闻组。

## 安装邮件服务器

根据你在 Linux 安装期间所做的选择，你可能已经安装了邮件服务器软件。你可以从几个邮件服务器中进行选择，如 `exim`、`postfix` 和 `sendmail` —— 我将在本章中简要介绍 `sendmail`。如果未安装 `sendmail`，你可以轻松安装它。
在 Debian、MEPIS、Ubuntu 和 Xandros 中，输入 `dpkg -l sendmail*` 以查看是否已安装 `sendmail`。在 Fedora Core 和 SUSE 中，输入 `rpm -qa | grep sendmail` 以查看是否已安装 `sendmail` 软件包。

![](img/792720823146d68f19fd50c99ebfce4b_638_0.png)

在 Debian、MEPIS 和 Ubuntu 中，输入 `apt-get install sendmail` 以安装 sendmail 服务器。在 Fedora Core 中，以 `root` 身份登录，挂载 DVD，然后输入 `cd /media/cdrom/Fedora/RPMS`，接着输入 `rpm -ih sendmail*`。在 SUSE 中，在 YaST 控制中心的软件类别中点击软件管理。然后使用 YaST 的搜索功能查找 sendmail 软件包并安装它们。

![](img/792720823146d68f19fd50c99ebfce4b_639_0.png)

## 使用 sendmail

为了将你的系统设置为邮件服务器，你必须正确配置 sendmail 邮件传输代理。sendmail 以复杂但完整的邮件投递系统而闻名。只需看一眼 sendmail 的配置文件——在 Fedora Core 中是 `/etc/mail/sendmail.cf`，在 SUSE 中是 `/etc/sendmail.cf`——就能让你确信 sendmail 确实复杂。幸运的是，你不需要是 sendmail 配置文件的专家。你只需要一个预定义的配置文件——就像安装在你的系统上的那个——就可以使用 sendmail。
你的系统已经有了一个可用的 sendmail 配置文件——`/etc/mail/sendmail.cf`。默认文件假设你有 Internet 连接和一个名称服务器。只要你有 Internet 连接并且你的系统有官方域名，你就可以从你的 Linux 个人计算机发送和接收电子邮件。

![](img/792720823146d68f19fd50c99ebfce4b_639_1.png)

为了确保邮件投递正常工作，你的系统名称必须匹配你的 ISP 分配给你的系统名称。虽然你可以给你的系统任何想要的主机名，但其他系统只有当你的系统名称在 ISP 的名称服务器中时，才能成功将邮件投递到系统。

## 邮件投递测试

为了试用 sendmail 邮件传输代理，你可以使用 mail 命令创建并发送一封邮件消息到 Linux 系统中的任何用户帐户。例如，以下是我如何使用 mail 命令给自己发送一条消息。（我的输入以粗体显示。）

```text
mail naba
Subject: Testing e-mail
This is from my Linux system.
.
```

mail 命令是一个简单的邮件用户代理。在上面的示例中，我在命令行中指定了收件人（naba）。mail 程序提示输入主题行。在主题之后，我输入我的消息，并以仅包含一个句点的行结束。在我结束消息后，邮件用户代理将消息传递给 `sendmail`（邮件传输代理）以投递到指定地址。`sendmail` 立即投递邮件消息。要验证邮件的投递，输入 `mail` 再次运行 mail 命令并读取消息。
因此，初始的 `sendmail` 配置文件对于发送和接收电子邮件是足够的，至少在你的 Linux 系统内部是这样的。外部邮件投递也能工作，前提是 Linux 系统有 Internet 连接和已注册的域名。

![](img/792720823146d68f19fd50c99ebfce4b_640_0.png)

如果你有一个提供动态 IP 地址给 Linux 系统的 ISP 帐户，你必须使用诸如 Evolution 或 Mozilla Mail 之类的邮件客户端，这些客户端联系你的 ISP 邮件服务器来投递发件邮件。

## 邮件投递机制

在 Internet 主机上，`sendmail` 邮件传输代理使用简单邮件传输协议 (SMTP) 投递邮件。基于 SMTP 的邮件传输代理监听 TCP 端口 25，并使用一组小的文本命令与其他邮件传输代理交换信息。实际上，SMTP 命令足够简单，你可以从终端手动使用它们来发送邮件消息。以下示例展示了如何从在同一系统上运行的 `telnet` 会话中，使用 SMTP 命令向 Linux 个人计算机上我的帐户发送邮件消息。（我的输入以**粗体**显示。）

```text
telnet localhost 25
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
220 linux.site ESMTP Sendmail 8.13.4/8.13.4/SUSE Linux 0.7; Sat, 3 Sep 2005
    14:10:06-0400
**help**
214-2.0.0 This is sendmail version 8.13.4
214-2.0.0 Topics:
214-2.0.0   HELO  EHLO  MAIL   RCPT   DATA
214-2.0.0   RSET  NOOP  QUIT  HELP  VRFY
214-2.0.0   EXPN  VERB  ETRN   DSN   AUTH
214-2.0.0   STARTTLS
214-2.0.0 For more info use "HELP topics".
214-2.0.0 To report bugs in the implementation send email to
214-2.0.0   sendmail-bugs@sendmail.org.
214-2.0.0 For local information send email to Postmaster at your site.
214 2.0.0 End of HELP info
**help DATA**
214-2.0.0 DATA
214-2.0.0   Following text is collected as the message.
214-2.0.0   End with a single dot.
214 2.0.0 End of HELP info
**HELO localhost**
250 linux.site Hello localhost [127.0.0.1], pleased to meet you
```

## sendmail 配置文件

你不必完全理解 `sendmail` 配置文件 `sendmail.cf` 中的所有内容，但你需要了解该文件是如何创建的。这样，如果有必要进行小幅调整，你便能重新生成 `sendmail.cf` 文件。
在 SUSE 中，你可以通过 YaST 控制中心来配置 `sendmail` — 选择 主菜单 > 系统 > 控制中心 (YaST) — 点击窗口左侧的“网络服务”，然后点击窗口右侧的“邮件传输代理”。YaST 会显示一个窗口（见图 4-1），你可以用它来配置 `sendmail`。首先指定常规设置，然后是出站邮件设置，最后是入站邮件设置。退出邮件配置工具后，YaST 会将邮件设置存储在 `/etc/sysconfig/sendmail` 和 `/etc/sysconfig/mail` 文件中，并通过运行 `SuSEconfig` 更新 `sendmail` 配置文件 — `/etc/sendmail.cf`。



![](img/792720823146d68f19fd50c99ebfce4b_642_0.png)

### 安装邮件服务器

![](img/792720823146d68f19fd50c99ebfce4b_643_0.png)

你还可以从多个 `m4 宏文件` 生成 `sendmail.cf` 文件（这些文本文件的每一行最终都会扩展为对某些程序具有意义的多行内容）。在 Fedora Core 中，这些宏文件组织在 `/usr/share/sendmail-cf` 目录下的若干子目录中；在 SUSE 中，则位于 `/usr/share/sendmail` 目录下。你可以阅读该目录中的 `README` 文件，以了解有关创建 `sendmail` 配置文件的更多信息。

## m4 宏处理器

m4 宏处理器生成 `sendmail.cf` 配置文件，该文件随 Linux 中的 `sendmail` 软件包提供。主要宏文件在 `sendmail` 软件包中命名各异，如 `sendmail.mc`、`generic_linux.mc` 或 `linux.mc`。

那么宏是什么呢？`宏` 基本上是用于处理某些操作的代码的符号名称，通常以一种替代长字符串的简写形式出现。m4 这样的`宏处理器` 通常读取其输入文件并将其复制到输出中，同时沿途处理宏。宏的处理通常涉及执行某些操作并生成一些输出。由于宏在输出中生成的文本远多于仅宏的名称，因此宏的处理被称为`宏展开`。

m4 宏处理器是`基于流`的。这意味着在忙于展开任何宏的同时，它会将输入字符复制到输出中。m4 宏处理器没有行的概念，因此它会复制换行符（标记行尾的字符）到输出中。这就是为什么你在大多数 m4 宏文件中都能看到单词 `dn1`；`dn1` 是一个 m4 宏，代表`删除直至换行符`。`dn1` 宏删除从 `dn1` 开始直到并包括下一个换行符为止的所有字符。输出中的换行符不会造成任何危害；它们只是产生不必要的空行。`sendmail` 宏软件包使用 `dn1` 来避免输出配置文件中出现此类空行。由于 `dn1` 基本上意味着删除至行尾的所有内容，m4 宏文件还将 `dn1` 用作注释行的前缀。

要查看 m4 的一个非常简单的用途，请考虑以下 m4 宏文件，它定义了两个宏 — `hello` 和 `bye` — 并在信函模板中使用它们：

```text
dn1 ##############################################################
dn1 #   File: ex.m4
dn1 #   A simple example of m4 macros
dn1 ##############################################################
dn11
define(`hello', `Dear Sir/Madam')dn1
define(`bye',
`Sincerely,
Customer Service')dn1
dn1 Now type the letter and use the macros
hello,

This is to inform you that we received your recent
  inquiry.
We will respond to your question soon.

bye
```

使用你喜欢的文本编辑器输入此文本，并将其保存为名为 `ex.m4` 的文件。你可以将宏文件命名为任何名称，但使用 `.m4` 扩展名作为 m4 宏文件的扩展名是惯例。

在使用 m4 处理宏文件之前，请注意该示例中的以下几个关键点：

- 使用 `dn1` 宏来启动所有注释行，如示例中的前四行所示。
- 在每个宏定义末尾使用 `dn1` 宏。否则，当 m4 处理宏文件时，会为每个宏定义生成一个空行。
- 使用内置的 `m4` 命令 `define` 来定义一个新宏。宏名称和值都用一对左右引号（`‘...’`）括起来。注意，你不能使用普通的单引号来括起宏名称和定义。

现在通过输入以下命令来处理宏文件 `ex.m4`：

```bash
m4 ex.m4
```

m4 处理宏并显示以下输出：

```text
Dear Sir/Madam,

This is to inform you that we received your recent
inquiry.
We will respond to your question soon.
Sincerely,

Customer Service
```

听起来就像典型的客户服务信函，不是吗？

如果你将输出与 `ex.m4` 文件进行对比，你会看到 `m4` 在标准输出中打印信函模板，并将宏 `hello` 和 `bye` 展开为其定义的值。如果你想将信函模板保存到一个名为 `letter` 的文件中，请使用 shell 的输出重定向功能，如下所示：

```bash
m4 ex.m4 > letter
```

如果你想在不展开的情况下在信函中使用单词 `hello` 或 `bye`，该怎么办？你可以通过将这些单词用一对单引号（`'...'`）括起来来实现。你必须对其他预定义的 `m4` 宏（如 `define`）这样做。要将 `define` 用作普通单词而非展开的宏，请输入 `'define'`。

## sendmail 宏文件

上一节中的简单示例让你了解了 `m4` 宏是如何定义并用于创建诸如 `sendmail.cf` 文件这样的配置文件的。你会在 Fedora Core 的 `/usr/share/sendmail-cf` 目录或 SUSE 的 `/usr/share/sendmail` 目录下的文件中找到许多复杂的宏。顶级宏文件 — 在 Fedora Core 中称为 `sendmail.mc`，在 SUSE 中称为 `linux.mc` — 在本节后面描述，它使用 `include` 宏（用于将文件复制到输入流）引入这些宏文件。

## SMTP 会话示例

`telnet` 命令打开到端口 `25` 的 TELNET 会话（这是 `sendmail` 预期接收 SMTP 命令的端口）。Linux 系统上的 `sendmail` 进程会立即回复一条通知。

我输入 `HELP` 以查看 SMTP 命令列表。要获取特定命令的帮助，我可以输入 `HELP` *commandname*。列表显示了当我输入 `HELP DATA` 时 `sendmail` 打印的帮助信息。

我输入 `HELO localhost` 以发起与主机的会话。`sendmail` 进程回复问候语。要发送邮件消息，我使用指定消息发送者的 `MAIL FROM:` 命令开始。（我输入发送消息的系统上的用户名。）`sendmail` 要求随用户名一起提供域名。

接下来，我使用 `RCPT TO:` 命令指定消息的收件人。如果我想将消息发送给多个收件人，我只需用 `RCPT TO:` 命令提供每个收件人的地址即可。

要输入邮件消息，我使用 `DATA` 命令。作为对 `DATA` 命令的响应，`sendmail` 显示一条指示，要求我在单独的一行中以句号结束消息。我输入消息并以单独一行的单个句号结束它。`sendmail` 进程显示一条消息，表明该消息已被接受用于投递。最后，我用 `QUIT` 命令结束 `sendmail` 会话。

```text
MAIL FROM: naba
553 5.1.4 naba... Domain name required for sender address naba
MAIL FROM: naba@localhost
250 2.1.0 naba@localhost... Sender ok
RCPT TO: naba
250 2.1.5 naba... Recipient ok
DATA
354 Enter mail... end with '.' on a line by itself
Testing... 1 2 3
Sending mail by telnet to port 25
.
250 2.0.0 j83l6aMd005251 Message accepted for delivery
QUIT
221 2.0.0 linux_site closing connection
Connection closed by foreign host.
```

之后，我登录到我的 Linux 系统并使用 `mail` 命令检查邮件。以下是我通过示例 SMTP 会话使用 `sendmail` 发送的邮件消息时，使用 `mail` 命令的会话。（我的输入以粗体显示。）



# 邮件示例

```
**mail**
mailx version mail 11.4 8/29/04. Type ? for help.
/var/mail/naba: 1 message 1 new
N 1 naba@linux.site Sat Sep 3 14:11 14/464
? 1
        Message  1:
        From naba@linux.site Sat Sep 3 14:11:57 2005
        Date: Sat, 3 Sep 2005 14:10:06 -0400
        From: Naba Barkakati <naba@linux.site>
        To: undisclosed-recipients:;


        Testing... 1 2 3
        Sending mail by telnet to port 25

? q
Saved 1 message in mbox
```

在这里，我输入 `mail` 以启动邮件程序。它显示新邮件的编号列表（在这种情况下，只有一封邮件）和一个提示符（?。我输入 `1`（我想读取的消息编号）。邮件程序显示消息并再次等待我的输入。我输入 `q` 以退出程序。

正如本例所示，SMTP 命令对人类来说足够简单，易于理解。这个例子有助于你理解邮件传输代理如何在使用 SMTP 在 Internet 上传输邮件。当然，电子邮件程序通常自动完成整个过程 — `sendmail` 程序也是如此（通过 `sendmail` 配置文件 `sendmail.cf` 中的设置）。

为了避免在不同发行版（如 Fedora Core 和 SUSE）中反复提及不同的文件和目录名称，以下讨论中我将使用 Fedora Core 的文件和目录名称。一般性讨论适用于所有 Linux 发行版中的 `sendmail`，但你必须将文件和目录名称替换为你特定发行版中对应的名称。

# sendmail 宏配置

通过在位于 `/usr/share/sendmail-cf` 目录中的文件里定义自己的一组高级宏，`sendmail` 实际上创建了自己的宏语言。`sendmail` 的宏文件使用 `_mc` 扩展名。你需要配置的主要 `sendmail` 宏文件是位于 `/etc/mail` 目录中的 `sendmail.mc`。

与 `/etc/mail/sendmail.cf` 文件相比，`/etc/mail/sendmail.mc` 文件更短，更容易操作。以下是随 Fedora Core 提供的 `/etc/mail/sendmail.mc` 文件中的部分内容：

```
dnl(1)dnl
dnl # This is the sendmail macro config file for m4. If you make changes to
dnl # /etc/mail/sendmail.mc, you will need to regenerate the
dnl # /etc/mail/sendmail.cf file by confirming that the sendmail-cf package is
dnl # installed and then performing a
dnl #
dnl # make -C /etc/mail
dnl #
include(`/usr/share/sendmail-cf/m4/cf.m4'dnl
VERSIONID(`setup for Red Hat Linux')dnl
OSTYPE(`linux')dnl
dnl #
dnl # default logging level is 9, you might want to set it higher to
dnl # debug the configuration
dnl define(`confLOG_LEVEL', `9')dnl
dnl #
dnl # Uncomment and edit the following line if your outgoing mail needs to
dnl # be sent out through an external mail server:
dnl #
dnl define(`SMART_HOST', smtp.comcast.net')
....lines deleted ...
dnl #
dnl MASQUERADE_AS('mydomain.com')dnl
dnl #
dnl # masquerade not just the headers, but the envelope as well
dnl FEATURE(masquerade_envelope)dnl
dnl #
dnl # masquerade not just @mydomainalias.com, but @*.mydomainalias.com as well
dnl #
dnl FEATURE(masquerade_entire_domain)dnl
dnl MASQUERADE_DOMAIN(localhost.localdomain)dnl
dnl MASQUERADE_DOMAIN(mydomainalias.com)dnl
dnl MASQUERADE_DOMAIN(mydomain.lan)dnl
MAILER(smtp)dnl
MAILER(procmail)dnl
dnl MAILER(cyrusv2)dnl
```

如果你修改了 `/etc/mail/sendmail.mc` 文件，你必须通过运行 `m4` 宏处理器处理 `sendmail.mc` 文件来生成 `/etc/mail/sendmail.cf` 文件，命令如下。（你必须以 `root` 身份登录。）

```
m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf
```

注释还告诉你，你需要 `sendmail-cf` 包来处理此文件。

从上一部分对 `m4` 宏的描述中，你可以看到 `sendmail.mc` 文件使用 `define` 来创建新的宏。你还可以看到大量使用 `dnl` 来避免在输出中插入过多的空行。

其他大写的单词（如 `OSTYPE`、`FEATURE` 和 `MAILER`）是 `sendmail` 宏。这些宏定义在 `/usr/share/sendmail-cf` 目录子目录中的 `.m4` 文件中，并通过以下 `include` 宏合并到 `sendmail.mc` 文件中：

```
include(`/usr/share/sendmail-cf/m4/cf.m4') dnl
```

反过来，`/usr/share/sendmail-cf/m4/cf.m4` 文件又包含 `cfdhead.m4` 文件，该文件又包含其他 `m4` 文件，等等。净效果是，当 `m4` 宏处理器处理 `sendmail.mc` 文件时，宏处理器会从 `/usr/share/sendmail-cf` 的各个子目录中合并许多 `m4` 文件。

# sendmail.mc 要点

关于 `/etc/mail/sendmail.mc` 文件，以下是需要注意的一些要点：

- `VERSIONID`(`setup for Red Hat Linux') 宏将引号内的版本信息插入到输出中。
- `OSTYPE`(`linux') 指定操作系统为 Linux。你必须尽早指定此宏以确保正确的配置。通常将置此宏于 `VERSIONID` 宏之后是惯例。
- `MAILER`(smtp) 描述邮件代理。根据 `/usr/share/sendmail-cf/README` 文件中的说明，`MAILER` 声明总是放置在 `sendmail.mc` 文件的末尾，并且 `MAILER`(smtp) 总是先于 `MAILER`(procmail)。邮件代理 `smtp` 指的是 SMTP 邮件代理。
- `FEATURE` 宏请求各种特殊功能。例如，`FEATURE`(`blacklist_recipients') 开启阻止特定用户名、主机或地址的传入邮件的功能。指定允许或拒绝哪些邮件的规格放在访问数据库中（存储在 `/etc/mail/access.db` 文件中）。你还需要 `FEATURE`(`access_db') 宏来开启访问数据库。
- `MASQUERADE_AS`(`mydomain.com') 使 `sendmail` 将 outgoing 邮件标记为来自主机 `mydomain.com`（替换为你的域名）。其理念是一个大型组织设置一个单一的 `sendmail` 服务器，处理许多子域的邮件，并使所有邮件看起来都来自一个单一域名。（例如，大学中许多部门的邮件看起来都来自大学的主域名。）
- `MASQUERADE_DOMAIN`(subdomain.mydomain.com) 指示 `sendmail` 将来自 `user@subdomain.mydomain.com` 等地址的邮件视为起源于由 `MASQUERADE_AS` 宏指定的域名上的相同用户名。



像 `FEATURE` 和 `MAILER` 这样的 `sendmail` 宏在 `/usr/share/sendmail-cf/README` 文件中有描述。在对 `sendmail.mc` 文件进行修改之前，请查阅该文件以了解更多关于 `sendmail` 宏的信息。

## sendmail.cf 文件语法

`sendmail.cf` 文件的语法设计得易于 `sendmail` 程序解析，因为 `sendmail` 在每次启动时都会读取此文件。在设计文件语法时，人类可读性并不是主要考虑因素。尽管如此，经过一点解释，你就可以理解 `sendmail.cf` 中控制行的含义。

每个 `sendmail` 控制行以一个单字母运算符开头，该运算符定义了其余部分行的含义。以空格或制表符开头的行被视为上一行的延续。空行和以井号 (`#`) 开头的行是注释。

通常，单字母运算符和其后的参数之间没有空格，这使得这些行更难理解。例如，`sendmail.cf` 使用了“类”的概念——本质上是一组短语。你可以定义一个名为 `P` 的类，并用以下控制行向该添加短语 `REDIRECT`：

```
CPREDIRECT
```

由于所有内容混在一起，命令很难辨认。另一方面，要定义一个名为 `Accept` 的类并设置其值为 `OK` 和 `RELAY`，请编写以下内容：

```
C{Accept}OK RELAY
```

这个命令可能更容易理解，因为分隔符（如类名 `Accept`）被包含在花括号中。

其他——更近期的——控制行甚至更容易理解。例如，行 `O HelpFile=/etc/mail/helpfile` 定义选项 `HelpFile` 为文件名 `/etc/mail/helpfile`。该文件包含 `sendmail` 在接收 `HELP` 命令时使用帮助信息。

表 4-1 总结了 `sendmail.cf` 中使用的单字母控制运算符。每个条目还展示了该运算符的一个示例。此表有助于你理解 `sendmail.cf` 中的一些行。

### 表 4-1 sendmail.cf 中使用的控制运算符

| 运算符 | 描述 |
| :--- | :--- |
| `C` | 定义一个类；一个变量（可以视为一个集合），可以包含多个值。例如，`Cwlocalhost` 将名称 `localhost` 添加到类 `w`。 |
| `D` | 定义一个宏，即与单个值关联的名称。例如，`DnMAILER-DAEMON` 将宏 `n` 定义为 `MAILER-DAEMON`。 |
| `F` | 定义一个已从文件读取的类。例如，`Fw/etc/mail/local-host-names` 从文件 `/etc/mail/local-host-names` 读取主机名称并将其添加到类 `w`。 |
| `H` | 定义 `sendmail` 插入消息的头部行的格式。例如，`H??From: < $g >` 定义头部的 `Return-Path` 字段。 |
| `K` | 定义一个映射（键值对数据库）。例如，`Karighth` 将名为 `arith` 的映射定义为同名的内置映射。 |
| `M` | 指定邮件代理。以下行定义了 `procmail` 邮件代理：`Mprocmail, Pa=/usr/bin/procmail, F=DIFGMSPhmu9, S=EnvFromSMTP/HdrFromSMTP, R=EnvToSMTP/HdrFromSMTP, T=DNS/RFC822/X-Unix, A=procmail -Y -m $h $f $u`。 |

## 安装邮件服务器

| 运算符 | 描述 |
| :--- | :--- |
| `O` | 将值分配给选项。例如，`O AliasFile=/etc/aliases` 将 `AliasFile` 选项定义为 `/etc/aliases`，这是 `sendmail` 别名文件的名称。 |
| `P` | 定义优先级字段的值。例如，`Pjunky=-100` 将标记为 `Precedence: junk` 头字段的邮件优先级设置为 -100。 |
| `R` | 定义一条规则。（规则有左侧和右侧；如果输入匹配左侧，则右侧替换它。此规则称为*重写*。）例如，重写规则 `R$* ; $1` 会去除末尾的分号。 |
| `S` | 标记一个规则集，您可以使用后续的 `R` 控制行开始定义它。例如，`S3=canyonify` 将下一个规则集标记为 `canonify` 或 `ruleset 3`。 |
| `T` | 将一个用户名添加到受信任类（class t）中。例如，`Troot` 将 `root` 添加到受信任用户类中。 |
| `V` | 定义配置文件的版本号。例如，`V1.0/Berkeley` 将版本号定义为 1.0。 |

### 其他 sendmail 文件

`/etc/mail` 目录包含 `sendmail` 使用的其他文件。这些文件在 `sendmail` 配置文件中被引用，在 `Fedora Core` 中为 `/etc/mail/sendmail.cf`，在 `SUSE` 中为 `/etc/sendmail.cf`。例如，这是如何在 `Fedora Core` 的 `/etc/mail/sendmail.cf` 文件中搜索 `/etc/mail` 字符串：

```
grep "*/etc/mail*" /etc/mail/sendmail.cf
```

在我的 `Fedora Core` 系统上，`grep` 命令搜索结果显示如下：

```
Fw /etc/mail/local-host-names
PR-o /etc/mail/relay-domains
Kmailer table hash -o /etc/mail/mailertable.db
Kvirtuser hash -o /etc/mail/virtuser table.db
Kaccess hash -Tc<"MDF"> -o /etc/mail/access.db
#0 ErrorHeader=/etc/mail/error-header
0 HelpFile=/etc/mail/helpfile
O UserDatabaseSpec=/etc/mail/userdb.db
#0 ServiceSwitchFile=/etc/mail/service.switch
#0 DefaultAuthInfo=/etc/mail/default-auth-info
Pt /etc/mail/trusted-users
```

**卷七**

**第四章**

管理邮件和新闻服务器

您可以忽略以井号或数字符号 (`#`) 开头的行，因为 `sendmail` 将这些行视为注释。其他行是 `sendmail` 控制行，引用 `/etc/mail` 目录中的其他文件。

以下是这些 `sendmail` 文件应包含的内容。（注意，并非所有这些文件都必须存在于 `/etc/mail` 目录中，即使存在，某些文件也可能是空的。）

- `/etc/mail/access`：允许发送邮件的主机名称和/或 IP 地址（有助于阻止垃圾邮件——不需要的电子邮件）
- `/etc/mail/access.db`：由 `/etc/mail/access` 文件生成的访问数据库
- `/etc/mail/helpfile`：SMTP 命令的帮助信息
- `/etc/mail/local-host-names`：本主机已知的名称
- `/etc/mail/mailertable`：用于覆盖邮件路由方式的邮件表（例如，条目 `comcast.net compast:smtp.comcast.net` 告诉 `sendmail` 发给 `comcast.net` 的邮件必须发送到 `smtp.comcast.net`。）
- `/etc/mail/relay-domains`：允许中继的主机
- `/etc/mail/trusted-users`：允许使用其他用户名称发送邮件而不受警告的用户列表
- `/etc/mail/userdb.db`：包含每个用户登录名和真实名称信息的用户数据库文件
- `/etc/mail/virtusertable`：托管在此系统上的具有虚拟域地址的用户数据库

![](img/792720823146d68f19fd50c99ebfce4b_651_0.png)

`/etc/mail` 目录有时还包含其他文件——`/etc/mail/certs` 以及带有 `_pem` 扩展名的文件——旨在通过使用 SMTP 的 STARTTLS 扩展来支持 `sendmail` 中的隐私增强邮件（PEM）。STARTTLS 扩展使用 TLS（更常被称为 SSL——安全套接字层）来验证发件人并加密邮件。RFC 2487 描述了 STARTTLS。（该 RFC 可在 http://ietf.org/rfc/rfc2487.txt 在线获取。）

![](img/792720823146d68f19fd50c99ebfce4b_651_1.png)

如果您编辑 `/etc/mail/mailertable` 文件，必须在更改生效前键入以下命令：

```
makemap hash /etc/mail/mailertable < /etc/mail/mailertable
```



一种更简单的方法来确保在做出任何更改后重建所有必要内容——只需以 `root` 身份登录并键入以下命令：

```
cd /etc/mail
make
```

第一条命令将当前目录更改为 `/etc/mail`，第二条命令运行 `make` 命令，该命令读取 `/etc/mail` 中名为 `Makefile` 的文件以执行重建所有内容的必要步骤。（要了解有关 `make` 和 `Makefile` 的更多信息，请参见卷八，第一章。）

### `.forward` 文件

用户可以通过在其主目录中放置 `.forward` 文件来重定向自己的邮件。`.forward` 文件是一个纯文本文件，包含逗号分隔的邮件地址列表。任何发送给该用户的邮件都会转发到这些地址。如果 `.forward` 文件包含单个地址，则该用户的所有电子邮件都会重定向到该单一电子邮件地址。例如，假设在一个名为 `emily` 的用户的主目录中放置了一个包含以下行的 `.forward` 文件：

```
ashley
```

此行导致 `sendmail` 自动将所有发送给 `emily` 的电子邮件发送到同一系统上的用户名 `ashley`。用户 `emily` 完全不会收到邮件。

还可以通过列出完整的电子邮件地址将邮件转发到另一系统上的用户名。例如，我添加了一个 `.forward` 文件，其中包含以下行，以将我的消息（发给我的用户名 `naba`）转发到邮件地址 `naba@comcast.net`：

```
naba@comcast.net
```

现在假设我想在原始系统上保留一份消息副本，同时转发到地址 `naba@comcast.net`。我可以通过在 `.forward` 文件中添加以下行来实现：

```
naba@comcast.net, naba\
```

我只需追加我的用户名并在行尾添加反斜杠。行末的反斜杠（`\`）阻止 `sendmail` 反复转发消息（因为当副本发送到系统上我的用户名时，`sendmail` 通常会再次处理我的 `.forward` 文件）。反斜杠告诉 `sendmail` 不要反复转发消息。

### `sendmail` 别名文件

除了 `sendmail.cf` 文件外，`sendmail` 还会参考名为 `/etc/aliases` 的别名文件，将名称转换为地址。别名文件的位置出现在 `sendmail` 配置文件中。

每个*别名*通常是电子邮件地址的较短名称。系统管理员使用 `sendmail` 文件转发*邮件*，创建邮件列表（标识多个用户的单一别名），或通过多个不同名称引用用户。例如，以下是一些典型的别名：

- `barkakati`: `naba`
- `naba`: `naba@lnbsoft`
- `all`: `naba, leha, ivy, emily, ashley`

第一行表示发送给 `barkakati` 的邮件将交付给本地系统上名为 `naba` 的用户。第二行表明发送给 `naba` 的邮件实际上发送到了 `lnbsoft` 系统上的用户名 `naba`。最后一行将 `all` 定义为五个用户 `naba`、`leha`、`ivy`、`emily` 和 `ashley` 的别名。这意味着发送给 `all` 的邮件将发送到这五个用户。

在 `/etc/aliases` 文件中定义任何新别名后，必须以 `root` 身份登录，并通过键入以下命令使新别名生效：

```
sendmail -bi
```

## 安装 INN 服务器

在本节中，我描述了如何配置基于 TCP/IP 的新闻服务器 InterNetNews（INN）。首先，您必须安装 INN。

在 Debian、MEPIS、Ubuntu 和 Xandros 中，键入 `dpkg -l inn*` 以查看是否安装了 `inn`。在 Fedora Core 和 SUSE 中，键入 `rpm -q inn` 并查看是否安装了 `inn` 包。

在 Debian、MEPIS 和 Ubuntu 中，键入 `apt-get install inn` 以安装 INN 服务器。在 Fedora Core 中，以 `root` 身份登录，挂载 DVD，并键入 `cd /media/cdrom/Fedora/RPMS` 后跟 `rpm -vh inn*`。在 SUSE 中，点击 YaST 控制中心软件类别中的“软件管理”。然后使用 YaST 的搜索功能查找 `inn`，从搜索结果中选择相关的包并安装它们。在 Xandros 中，首先运行 Xandros Networks，选择 编辑>设置应用程序源，并点击 Debian Unsuppored Site 链接作为源。然后键入 `apt-get install inn` 以安装 INN 服务器。

# 配置和启动 INN 服务器

INN 软件的大部分功能在安装后即可使用。你只需对 INN 的各个组件进行一点复习，编辑配置文件，并启动 `innd` —— INN 服务器。顺便说一下，我有时也称 INN 服务器为新闻服务器。

如果你想运行一个支持多种 Internet 新闻组的新闻服务器，你还需要安排一个*新闻源（news feed）*——即你的新闻服务器获取新闻组文章的地方。通常，你可以从 ISP（互联网服务提供商）获得新闻源，但 ISP 会收取额外的月度费用，以覆盖提供该源所需的资源成本。（你通常向 ISP 支付的费用仅涵盖阅读其服务器上的新闻；只有当你想要运行自己的服务器并获取新闻源时，才需要支付额外费用。）你需要提供提供新闻源的上游服务器名称，并且必须向该服务器提供你服务器的名称以及你希望接收的新闻组。

顺便说一句，如果你运行新闻服务器是为了支持仅在组织内部网络中可用的本地新闻组，则不需要外部新闻源。我在本章的“设置本地新闻组”部分介绍了如何设置本地新闻组。

根据你希望接收的新闻组以及保留文章的天数，你需要预留适当的磁盘空间来存储这些文章。新闻组按照目录结构（基于新闻组名称）存储在系统目录 `/var/spool/news` 中。如果你正在设置新闻服务器，可能希望将一个大容量的磁盘分区专门用于 `/var/spool/news` 目录。

在新闻服务器的配置文件中，输入提供新闻源的服务器名称。同时，在配置文件中添加任何从你的服务器接收新闻源的下游新闻服务器（如果有）的名称。然后你可以启动新闻服务器并等待新闻到达。监控日志文件，以确保新闻文章在你的系统 `/var/spool/news` 目录中正确分类和存储。

在接下来的部分中，我将向你介绍 INN 的设置，但你可以从互联网系统协会（Internet Systems Consortium, ISC）获取更多关于 INN 的信息。ISC 是一家非营利法人，致力于开发和维护开源 Internet 软件，如 BIND（域名系统实现）、DHCP（动态主机配置协议）和 INN。Rick Salze 最初编写了 INN；ISC 在 1996 年接管了 INN 的开发。你可以在 ISC 的 INN 网页 `www.isc.org/sw/inn` 上了解更多关于 INN 的信息并访问其他资源。

![](img/792720823146d68f19fd50c99ebfce4b_654_0.png)

# InterNetNews 组件

INN 包含几个用于交付和管理新闻组的程序。它还包含一些控制 INN 程序如何工作的文件。最重要的 INN 程序如下：

- **`innd`:** 新闻服务器。它作为*守护进程*（一种保持运行以提供特定服务的后台进程）运行，并监听 NNTP 端口（TCP 端口 119）。`innd` 服务器接受来自其他新闻源站点以及本地新闻阅读器客户端的连接，但它将本地连接交给 `nnrpd` 处理。
- **`nnrpd`:** 由 `innd` 调用的特殊服务器，用于处理来自本地新闻阅读器客户端的请求。
- **`expire`:** 根据文本文件 `/etc/news/expire.ctl` 中的规范删除旧文章。
- **`nttpsnd`:** 调用 `innewsmit` 程序，使用 NNTP 将新闻文章发送到远程站点。配置文件 `/etc/news/nttpsnd.ctl` 控制 `nttpsnd` 程序。
- **`ctlinnnd`:** 允许你交互式地控制 `innd` 服务器。`ctlinnnd` 程序可以向 `innd` 服务器的控制通道发送消息。

INN 的其他关键组件是控制文件。这些文件大多数位于你的 Linux 系统的 `/etc/news` 目录中，尽管少数位于 `/var/lib/news` 目录中。在这两个目录之间，你有超过 30 个 INN 控制文件。一些重要的文件包括以下这些：

- **`/etc/news/inn.conf`:** 指定 `innd` 服务器的配置数据。（要查看此文件的在线帮助，请输入 `man inn.conf`。）
- **`/etc/news/newsfeeds`:** 指定向其他新闻服务器下游提供哪些文章。（该文件很复杂，但你可以通过输入 `man newsfeeds` 获取帮助。）
- **`/etc/news/incoming.conf`:** 列出向此服务器提供新闻源的主机的名称和地址。（要查看此文件的在线帮助，请输入 `man incoming.conf`。）



- `/etc/news/storage.conf`：指定存储新闻文章时使用的存储方法。（要查看此文件的在线帮助，请输入 `man storage.conf`。）

- `/etc/news/expire.ctl`：控制文章的过期，如果需要，可按新闻组级别控制。（要查看此文件的在线帮助，请输入 `man expire.ctl`。）

在接下来的几节中，我将描述如何设置一些重要的控制文件。

# inn.conf 文件

此文件存储所有 INN 程序的配置数据——这使其成为最重要的文件。该文件的每一行都有以下格式的参数值：

```
parameter:	value
```

根据参数的不同，值可以是字符串、数字或 true 或 false。与许多其他配置文件一样，注释行以数字或井号（`#`）开头。

`/etc/news` 目录中默认 `inn.conf` 文件中的大多数参数不需要更改。你可能希望编辑表 4-2 中显示的一个或多个参数。

| 参数名称 | 描述 |
| :--- | :--- |
| `mta` | 将此参数设置为启动邮件传输代理（由 `innd` 用于传输消息）所使用的命令。默认使用 `sendmail`。 |
| `organization` | 将此参数设置为你希望它在所有从你的系统发布的新闻文章的 `Organization:` 头中显示的组织名称。用户可以通过定义 `ORGANIZATION` 环境变量来覆盖此参数。 |
| `ovmethod` | 设置概述存储方法的类型。（概述是新闻组中新闻文章的索引。）默认方法是 `tradindexed`，读取新闻时速度快，但存储新闻项时速度慢。 |
| `pathhost` | 将此参数设置为你希望它在经过你的服务器的所有发布的 `Path` 头中显示的新闻服务器名称。如果未定义 `pathhost`，则使用你系统的全限定域名。 |
| `pathnews` | 将此参数设置为包含 INN 二进制文件和库的目录的完整路径名。默认 `pathnews` 设置为 `/usr/lib/news`。 |
| `domain` | 将此参数设置为你服务器的域名。 |
| `allownewnews` | 如果你希望 INN 支持来自新闻阅读器的 `NEWNEWS` 命令，则将此参数设置为 `true`。过去，由于 `NEWNEWS` 命令会降低服务器性能，此选项被设置为 `false`，但现在默认设置为 `true`，因为现代服务器可以轻松处理 `NEWNEWS` 命令。 |
| `hiscachesize` | 将此参数设置为你希望 INN 用于缓存最近接收的消息 ID 的大小（以 KB 为单位），这些 ID 保留在内存中以加快历史记录查找。此缓存仅用于传入的新闻源，且较小的缓存可以保存相当多的历史记录文件条目。默认设置 `0` 禁用了历史记录缓存。如果你有多个传入新闻源，你可能希望将此参数设置为 `256`（即 256KB）。 |
| `innflags` | 将此参数设置为你希望在 INN 服务器进程启动时传递给它的任何标志。 |

# newfeeds 文件

`newfeeds` 文件指定传入的新闻文章如何重新分配到其他服务器和 INN 进程。如果你向其他服务器提供新闻源，你必须在此文件中列出这些新闻源。（你还必须有一个标记为 `*ME*` 的条目，它服务于我稍后在本节中解释的特定用途。）

`newfeeds` 文件包含一系列条目，每个条目对应一个新闻源。每个新闻源条目具有以下格式：

```
site(/exclude,exclude,. . . )\
  :pattern, pattern. . .{ /distrib, distrib. . .}\
  :flag, flag. . .
  :param
```

## 配置并启动 INN 服务器

每个条目包含由冒号（`:`）分隔的四个字段。通常，条目会跨越多行，且行尾的反斜杠（`\`）用于将当前行延续到下一行。这四个字段的含义如下：

- 第一个字段 `site` 是信息源的名称。每个名称必须唯一，对于到其他新闻服务器的信息源，名称被设置为远程服务器的主机名。名称后面跟一个可选的斜杠和一个 `exclude` 列表（`exclude,exclude,...`），其中包含若干名称。如果该列表中的任何名称出现在文章的 `path` 行中，该文章就不会被转发到该信息源。如果你不想接收来自特定来源的文章，可以使用 `exclude` 列表。

- 第二个字段是一个由逗号分隔的新闻组 `patterns` 列表，例如 `*,@alt.binaries.warez.*,!control*,!local*`，后面跟着一个可选的 `distribution` 列表。`distribution` 列表是一个由逗号分隔的关键字列表，每个关键字指定一组特定的站点，`articles` 将分发给这些站点。新闻组模式实质上定义了接收此新闻信息源的站点订阅列表。星号（`*`）匹配所有新闻组。以 `@` 开头的模式会导致匹配该模式的新闻组被丢弃。以感叹号（`!`）开头的模式表示匹配的新闻组不会被发送。顺便说一下，INN 配置文件中使用的这种简单的模式匹配语法被称为 `wildmat` 模式。

- 第三个字段是一个由逗号分隔的 `flags` 列表——这些字段决定了信息源条目的类型，并为该条目设置某些参数。你会看到许多标志；输入 `man newsfeeds` 并阅读 `man` 页面以获取有关标志的更多信息。

- 第四个字段是 `for parameters`，其值取决于第三个字段中的设置。通常，此字段包含 INN 服务器使用的文件或外部程序的名称。你可以从 `newsfeeds` 的 `man` 页面中了解关于此字段的更多信息。

现在你已经知道了 `/etc/news/newsfeeds` 文件的布局，你可以研究该文件作为一个示例。默认文件包含许多示例信息源条目，但只有两个被注释掉了：

- `ME` 是一个特殊的信息源条目，始终需要。它有两个目的。首先，此条目中列出的新闻组模式用作所有其他条目中所有新闻组模式的前缀。其次，`ME` 条目的分发列表决定了你的服务器从远程站点接受哪些分发。

- `controlchan` 信息源条目用于设置 INN，使其使用外部程序来处理控制消息。（这些消息用于创建新新闻组和删除组。）例如，

![](img/792720823146d68f19fd50c99ebfce4b_658_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_658_1.png)

![](img/792720823146d68f19fd50c99ebfce4b_658_2.png)

以下 `controlchan` 条目指定外部程序 `/usr/lib/news/bin/controlchan` 来处理所有控制消息，除了取消消息（用于取消文章）：

```
controlchan!\
:\*, control, control.\*, !control.cancel\
:Tc, Wsm, /usr/lib/news/bin/controlchan
```

除了这些信息源条目外，你还为实际接收新闻信息源的站点添加条目。此类条目的格式为

```
feedme.domain.com\
:!junk, \control!foo\
:Tm: innfeed!
```

其中 `feedme.domain.com` 是你的系统发送新闻文章的站点的全限定域名。

### incoming.conf 文件

`incoming.conf` 文件描述了哪些主机被允许连接到你的主机以提供文章。对于单个信息源，你可以添加像这样的条目

```
peer mybuddy {
    hostname: a-feed-site.domain.com
}
```

其中 `mybuddy` 是对等端的标签，而 `a-feed-site.domain.com` 标识为你提供文章的站点。

![](img/792720823146d68f19fd50c99ebfce4b_659_0.png)

请记住，仅仅在 `incoming.conf` 文件中添加站点名称并不会导致该远程站点开始向你的站点提供新闻——它只是使你的服务器能够接受来自远程站点的新闻文章。在远程站点，你的朋友必须配置他的或她的服务器向你的站点发送文章。

### readers.conf 文件

此文件指定新闻阅读器客户端（如 Mozilla）可以从哪些主机名或 IP 地址从你的服务器检索新闻组。例如，以下 `readers.conf` 文件允许 `read access`（读取访问权限）和 `post access`（发布访问权限，意味着你可以提交文章）来自 `localhost` 和 192.168.0.0 网络中的任何主机：



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

### `InterNetNews` 启动

除了配置文件，你还必须启动执行新闻服务器定期维护的 cron 任务。在 Fedora Core 中，这些 cron 任务已经设置好。因此，你现在可以启动 INN 服务器 —— `innd`。

在启动 `innd` 之前，你必须运行 `makehistory` 和 `makedbz` 来初始化和重建 INN 历史数据库。输入 `man makehistory` 和 `man makedbz` 以了解有关这些命令的更多信息。要创建初始历史数据库、关联索引，并设置某些文件的所有者和权限，请输入以下命令：

```
/usr/lib/news/bin/makehistory -b -f history -O -l 30000 -I
cd /var/lib/news
/usr/lib/news/bin/makedbz -- 'wc -l < history' -f history
chown news.news *
chown news.news /var/spool/news/overview/group.index
chmod 664 /var/spool/news/overview/group.index
```

在 Fedora Core 中，要启动 `innd`，请以 root 身份登录并输入 `/etc/init.d/innd start`。或者，你可以输入 `service innd start`。在 Debian, MEPIS, SUSE, Ubuntu 和 Xandros 中，输入 `/etc/init.d/inn start`。为了确保 `innd` 在启动时启动，请在 Fedora Core 中输入 `chkconfig -level 35 innd on`，在 SUSE 中输入 `chkconfig -level 35 inn on`。在 Debian 和 Xandros 中，输入 `update-rc.d inn defaults`。

如果你修改了 INN 配置文件，请记住通过调用 `/etc/init.d` 脚本并将 `restart` 作为参数来重启服务器。

![](img/792720823146d68f19fd50c99ebfce4b_660_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_660_1.png)

### 设置本地新闻组

如果你希望使用新闻组作为在公司内部共享信息的一种方式，你可以设置一个本地新闻组的层级结构。然后你可以使用这些新闻组在你的公司内创建虚拟社区，拥有共同兴趣的人可以非正式地讨论问题并交换知识。

#### 定义新闻组层级结构

第一个任务是定义一个新闻组层级结构，决定每个新闻组讨论的内容。例如，如果你的公司名称是 XYZ Corporation，以下是你可能会定义的部分新闻组层级结构：

- `xyz.general`：关于 XYZ Corporation 的一般事项

- `xyz.weekly.news`：每周新闻

- `xyz.weekly.menu`：每周自助餐厅菜单及关于它的讨论

- `xyz.forsale`：员工出售物品的列表

- `xyz.jobs`：XYZ Corporation 的招聘职位

- `xyz.wanted`：员工发布的求助（帮助、待购物品等）

- `xyz.technical.hardware`：关于硬件的技术讨论

- `xyz.technical.software`：关于软件的技术讨论

#### 更新配置文件

以下是你更新本地新闻组配置文件并重启新闻服务器的步骤：

1. 在 `/var/lib/news/newsgroups` 文件中为这些每个新闻组添加描述性条目。

   在此文件中为每个本地新闻组添加一行——输入其名称后跟简短描述。例如，这是你可能为 `xyz.general` 新闻组添加的内容：

   ```
   xyz.general    General items about XYZ Corporation
   ```

2. 编辑 `/etc/news/newsfeeds` 文件中的 ME 条目，并将短语 `*!xyz.*` 添加到由逗号分隔的新闻组模式列表中。

   此步骤确保你的本地新闻组不会分发到你的站点之外。

### 3. 添加用于本地新闻组的存储方法

例如，你可以在 `/etc/news/storage.conf` 中添加以下行，以定义新的 *xyz* 层次结构新闻组的存储方法（请将 *xyz* 更改为你为本地新闻组命名的名称）：

```
method tradspool { 
class: 1
newsgroups: xyz.* 
}
```

### 4. 重启新闻服务器以使这些更改生效

在 Fedora Core 中输入 `service inn restart`，或在 Debian、MEPIS、SUSE、Ubuntu 和 Xandros 中输入 `/etc/init.d/inn restart`。

## 添加新闻组

最后一步是添加新闻组。在你更新配置文件并运行 `innd` 后，添加本地新闻组非常简单。以 `root` 身份登录并使用 `ctlinnd` 执行此任务。例如，以下是如何添加名为 `xyz.general` 的新闻组：

```
/usr/lib/news/bin/ctlinnd newgroup xyz.general
```

就这样！该命令将 `xyz.general` 新闻组添加到你的站点。如果你使用传统的 `storage` 方法，`innd` 服务器将创建目录 `/var/spool/news/articles/xyz/general` 并将该新闻组的文章存储在该目录中。这会在某人第一次向该新闻组发布新闻文章时发生。

创建完所有本地新闻组后，你内联网的用户就可以发布新闻文章并阅读本地新闻组中的文章了。如果他们遇到访问新闻组的问题，请确保 `/etc/news/readers.conf` 文件包含可以访问 `innd` 服务器的主机的 IP 地址或名称。

## 测试你的新闻组

例如，我使用前面章节中说明的步骤，在我运行 Linux 系统的 INN 服务器中添加了一个名为 `local.news` 的新闻组。然后，我启动了一个新闻阅读器，并设置了一个新的新闻账户，将新闻服务器设置为我自己的 INN 服务器。然后，我访问 `local.news` 新闻组。试试看吧！我敢打赌你会喜欢它。

![](img/792720823146d68f19fd50c99ebfce4b_662_0.png)

# 第 5 章：管理 DNS

## 本章内容

- 理解 DNS

- 探索 BIND

- 配置 DNS

- 设置缓存名称服务器

- 配置主要名称服务器

**D**omain Name System (DNS) 是一项互联网服务，它将完全限定域名（如 `www.debian.org`）转换为其对应的 IP 地址（如 194.109.137.218）。你可以将 DNS 视为互联网主机目录——DNS 使得你即使 TCP/IP 需要数字 IP 地址进行数据传输，也可以使用易记的主机名。DNS 基本上是一个分布式 DNS 服务器层次结构。在本章中，我将提供 DNS 的概述，并展示如何在你自己的 Linux 系统上设置一个缓存 DNS 服务器。

## 理解域名系统 (DNS)

在 TCP/IP 网络中，每个网络接口（例如，以太网卡或拨号调制解调器连接）由 IP 地址标识。由于 IP 地址难以记忆，因此为 IP 地址分配了一个易记的名称——就像名字对应电话号码一样。例如，你不必记住红帽（Red Hat）Web 服务器的 IP 地址是 194.109.137.218，只需通过其名称 `www.debian.org` 即可引用该主机。当你在 Web 浏览器中输入 `www.debian.org` 作为 URL 时，名称 `www.debian.org` 被翻译为其对应的 IP 地址。这就是 DNS 概念的用武之地。

### 什么是 DNS？

域名系统是一个分布式、分层数据库，保存了关于互联网上计算机的信息。这些信息包括主机名、IP 地址和邮件路由规范。由于这些信息存储在互联网上的许多 DNS 主机上，因此 DNS 被称为*分布式*数据库。DNS 的主要任务是将主机名与 IP 地址相关联，反之亦然。

### 640 理解域名系统 (DNS)



在 ARPANET（当今互联网的前身）中，主机名和相应 IP 地址的列表维护在一个名为 `HOSTS.TXT` 的文本文件中，该文件由中央机构管理并定期分发到网络上的每个主机。随着主机数量的增长，这种静态主机表很快就变得不合理难以维护。Paul Mockapetris 提出了 DNS 以缓解静态主机表带来的问题。如 RFC 882 和 883 中正式记录的那样（1983 年 11 月发布，参见 `www.faqs.org/rfcs/rfc882.html` 和 `www.faqs.org/rfcs/rfc883.html`），最初的 DNS 引入了两个关键概念：
- 使用分层域名，如 `www.ee.umd.edu` 和 `www.debian.org`
- 在整个互联网上使用 DNS 服务器——这是一种分布式责任形式——作为管理主机数据库的一种手段

如今，DNS 是记录在 RFC 1034 和 1035 中的互联网标准。该标准已由其他几个 RFC 更新和扩展——1101、1183、1348、1886、1995、1996、2136、2181、2308、2845、2930、2931、3007、3110、3226、3403、3596、3597、3645、3646、4025、4033、4034 和 4035。早期的更新定义了数据编码，而后者则侧重于提高 DNS 的安全性。要在线阅读这些以及其他 RFC，请访问互联网工程任务组（IETF）网站的 RFC 页面：
`www.ietf.org/rfc.html`

DNS 定义了以下内容：
- 主机的分层域名系统
- 将每个域名与 IP 地址相关联的分布式数据库
- 网络应用程序可用于查询分布式 DNS 数据库的库例程（解析器）（此库称为解析器库）
- DNS 客户端和服务器交换名称和 IP 地址信息的协议

如今，互联网上的所有主机都依赖 DNS 来访问远程主机上的各种互联网服务。根据你的个人经验，当你从互联网服务提供商（ISP）获取互联网接入时，你的 ISP 会提供名称服务器的 IP 地址——即你的系统在将主机名映射为 IP 地址时访问的 DNS 服务器。

如果你有一个小型局域网，你可能会决定在其中一台主机上运行 DNS 服务器，或者使用 ISP 提供的名称服务器。对于具有多个子网的中型网络，你可以在每个子网上运行 DNS 服务器以提供高效的 DNS 查询。在大型企业网络中，企业域名（如 `www.microsoft.com`）进一步划分为子域名层次结构；每个子域名中可能会使用多个 DNS 服务器。

在接下来的章节中，我将提供分层域名命名约定的概述，并描述 BIND——在大多数 UNIX 系统（包括 Linux）上使用的 DNS 软件。

### 发现分层域名

DNS 使用分层的域名树来组织 `namespace`（命名空间）——即所有名称的集合。每个较高级别的域名都对其较低子域名具有管理权限。每个域名代表命名空间中一个独立的块，并由单个管理权限进行管理。图 5-1 说明了 DNS 命名空间的分层组织。

**图 5-1：DNS 命名空间以分层方式组织。**

![](img/792720823146d68f19fd50c99ebfce4b_666_0.png)

树的根称为*根域名*，由单个点 (.) 表示。接下来是顶级、*或*根级域名。顶级域名进一步划分为二级域名，二级域名又可分为进一步的子域名。

顶级域名相对固定，包括诸如 `COM`、`NET`、`ORG`、`EDU`、`GOV` 和 `MIL` 等众所周知的域名。这些是美国常用的顶级域名。这些顶级域名是在 20 世纪 90 年代初互联网广泛使用期间出现的。

另一组顶级域名用于国家。这些域名使用国际标准化组织（缩写为 ISO，见 `www.iso.ch`）分配的两字母国家代码。例如，美国的顶级国家代码域名是 `US`。在美国，许多地方政府和组织使用 `US` 域名。例如，`mcps.k12.md.us` 是美国马里兰州蒙哥马利县公立学校的域名。

*完全限定域名*（FQDN）是通过使用点（.）作为分隔符，将子域名从低级别到高级别依次串联起来构建的。*例如*，`REDHAT.COM` 是一个完全限定域名；`EE.UMD.EDU` 也是如此。请注意，其中每一个也可以指代一台特定的主机计算机。图 5-2 展示了完全限定域名的组成部分。

![](img/792720823146d68f19fd50c99ebfce4b_667_0.png)

域名不区分大小写。因此，就 DNS 而言，`UMD.EDU` 和 `umd.edu` 这两个域名都代表马里兰大学（University of Maryland）的域名。不过，惯例是全小写输入域名。

## 探索 Berkeley Internet Name Domain (BIND)

大多数 UNIX 系统（包括 Linux）都附带 BIND 系统——一种广为人知的 DNS 实现。在安装 Linux 时，只要你在选择安装软件包时选中了名称服务器，BIND 软件就会随之安装。

在 Debian、MEPIS、Ubuntu 和 Xandros 中，输入 `dpkg -i bind*` 以查看是否已安装 BIND。在 Fedora Core 和 SUSE 中，输入 `rpm -q bind` 并查看是否已安装 `bind` 软件包。

在 Debian、MEPIS 和 Ubuntu 中，输入 `apt-get install bind9` 以安装 BIND。在 Fedora Core 中，以 `root` 身份登录，挂载 DVD，并输入 `cd /media/cdrom/Fedora/RPMS`，接着输入 `rpm -ivh bind*`。在 SUSE 中，在 YaST 控制中心的软件类别中点击*软件管理*。然后使用 YaST 的搜索功能查找 `bind`，选择相关的软件包并安装。在 Xandros 中，首先运行 Xandros Networks，选择 Edit→Set Application Sources，并点击 Debian Unsupported Site 链接作为来源。然后输入 `apt-get install bind9` 以安装 BIND 服务器。

BIND 包括三个主要组件：
- `named` 守护进程——即名称服务器——它负责响应关于主机名和 IP 地址的查询
- 解析器库，应用程序可使用它将主机名解析为 IP 地址（反之亦然）
- 命令行 DNS 实用程序（DNS 客户端），例如 `dig`（Domain Internet Groper）和 `host`，用户可以使用它们来查询 DNS

我将在接下来的几个部分中描述 BIND 的这些组件。在后几节中，我将解释如何配置解析器和名称服务器。

### named— BIND 名称服务器

`named` 守护进程是响应主机名和 IP 地址查询的名称服务器。基于配置文件和本地 DNS 数据库，`named` 要么提供查询的答案，要么向其他服务器请求查询并缓存其响应。`named` 服务器还执行一项称为区域传输（zone transfer）的功能，这涉及在域内的名称服务器之间复制数据。

名称服务器以三种模式之一运行：
- **主服务器或主节点：** 在这种情况下，名称服务器在磁盘上保留域名数据的主副本。每个域或子域都有一个主服务器。
- **从服务器或从节点：** 从名称服务器使用区域传输操作从主服务器复制其域名数据。一个域可以有一个或多个从名称服务器。
- **缓存：** 缓存名称服务器加载根域少数几个权威服务器的地址，并通过联系其他名称服务器已解析的查询响应来缓存获取所有域名数据。主服务器和从服务器也缓存响应。

根据*名称服务器*提供的信息，它可以是权威的或非权威的。顾名思义，权威名称服务器的响应应该是准确的。主服务器和从名称服务器对于其自身的域是权威的，但对于从缓存信息提供的响应则不是权威的。

![](img/792720823146d68f19fd50c99ebfce4b_668_0.png)

缓存名称服务器永远不是权威的，因为它们的所有响应都来自缓存信息。

要在你的 Linux 系统上运行名称服务器，你必须使用适当的配置文件运行 `named`。在本章的后面部分，你将了解控制名称服务器如何操作的配置文件和数据文件。

### 解析器库

查找主机名的 IP 地址被称为*解析主机名*。具备网络感知功能的应用程序（如 Web 浏览器或 FTP 客户端）使用*解析器库*来执行从名称到 IP 地址的转换。根据 `/etc/host.conf` 文件中的设置，解析器库会查阅 `/etc/hosts` 文件或发起 DNS 查询，以将主机名解析为其 IP 地址。解析器库查询 `/etc/resolv.conf` 文件中列出的名称服务器。

除非你正在编写具备网络感知功能的应用程序，否则你不需要了解太多的解析器库知识。要正确运行 Internet 服务，你只需要知道如何配置解析器即可。在本章的后面，我将向你展示如何配置服务器以及 DNS 的其他方面。

### DNS 实用程序



你可以使用 DNS 实用程序——`dig` 和 `host`——从 shell 提示符交互式地试用 DNS。这些实用程序是 DNS 客户端。你可以使用它们查询 DNS 数据库并调试你在系统上设置的任何名称服务器。默认情况下，这些程序查询系统 `/etc/resolv.conf` 文件中列出的名称服务器。

你可以使用 `dig`（Domain Internet Groper 程序）查找域名或 IP 地址。例如，要查找 `ftp.redhat.com` 的 IP 地址，请输入

```text
dig ftp.redhat.com
```

`dig` 会详细打印 DNS 查询的结果。在输出中标记为 `ANSWER SECTION` 的部分查找结果。例如，对于此示例查询，该部分看起来像这样：

```text
;; ANSWER SECTION:
ftp.redhat.com.        300 IN A 66.187.224.30
```

此输出意味着名称 `ftp.redhat.com` 指的是 IP 地址 66.187.224.30。

使用 `dig` 进行*反向查找*（查找 IP 地址的主机名）也很简单。例如，要查找与 IP 地址 209.132.176.30 对应的主机名，请输入以下内容：

```text
dig -x 66.187.224.30
```

同样，答案出现在输出的 ANSWER SECTION 中，对于这个例子，看起来像这样：

```text
;; ANSWER SECTION:
30.224.187.66.in-addr.arpa. 600 IN PTR ftp.redhat.com.
```

在这种情况下，与 IP 地址 66.187.224.30 对应的主机名恰好是 `ftp.redhat.com`。

你还可以通过使用 `host` 程序来查询 DNS。`host` 程序产生紧凑格式的输出。例如，这是使用 `host` 查找主机名的 IP 地址的典型用法：

```text
host www.gao.gov
```

此命令生成以下输出：

```text
www.gao.gov has address 161.203.16.2
www.gao.gov mail is handled by 5 listserv.gao.gov.
```

默认情况下，`host` 打印 IP 地址和任何 *MX 记录*（这些记录列出了主机邮件处理器的名称）。

要进行反向查找，请使用 `-t ptr` 选项，并将 IP 地址作为参数，如下所示：

```text
host -t ptr 161.203.16.2
```

以下是 `host` 的结果：

```text
2.16.203.161.in-addr.arpa domain name pointer www.gao.gov.
```

在这种情况下，`host` 打印 *PTR 记录*（来自 DNS 数据库），该记录显示了与 IP 地址对应的主机名。(*PTR 指*指针*，且* PTR *记录指定与地址对应的名称。)*

你也可以尝试其他类型的记录，例如 *CNAME*（规范名称），如下所示：

```text
host -t cname www.ee.umd.edu
```

`host` 的响应如下：

```text
www.ee.umd.edu is an alias for edison.eng.umd.edu.
```

此输出表明 `www.ee.umd.edu` 的*规范名称*（或别名）是 `edison.eng.umd.edu`。

## 配置 DNS

你通过使用多个配置文件来配置 DNS。具体的文件集取决于你是否正在运行名称服务器，如果是，则是名称服务器的类型——缓存型或主型。无论你运行名称服务器与否，都需要一些配置文件。

### 配置解析器

要使用 DNS 客户端（`dig` 和 `host`），你的系统上不需要运行名称服务器。你可以使用它们查询你所在域的名称服务器。通常，你的 ISP 会提供此信息。你必须在 `/etc/resolv.conf` 文件中列出这些名称服务器的 IP 地址——解析器库读取此文件以确定如何解析主机名。此文件的格式如下

```text
domain your-domain.com
search your-domain.com
nameserver A.B.C.D
nameserver X.Y.Z.W
```

其中 `A.B.C.D` 和 `X.Y.Z.W` 是主要和次要名称服务器的 IP 地址（点分十进制地址，例如 192.168.0.1），由你的 ISP 提供。

`domain` 行列出本地域名。`search` 行指定首先搜索的主机名所属的域（通常，你将自己的域放在 `search` 行中）。`search` 行列出的域会在解析器库尝试解析之前附加到任何主机名后面。例如，如果你查找名为 `mailhost` 的主机，解析器库会先尝试 `mailhost.your-domain.com`；如果失败，它会尝试 `mailhost`。`search` 行适用于你尝试访问的任何主机名。例如，如果你试图访问 `www.redhat.com`，解析器会先尝试 `www.redhat.com.your-domain.com`，然后尝试 `www.redhat.com`。

另一个重要的配置文件是 `/etc/host.conf` —— 此文件告诉解析器在尝试解析主机名时该怎么做。典型的 `/etc/host.conf` 文件包含以下行：

```text
order hosts,bind
```

此命令告诉解析器首先查阅 `/etc/hosts` 文件，如果失败，则查询 `/etc/resolv.conf` 文件中列出的名称服务器。`/etc/hosts` 文件通常列出任何本地主机名及其 IP 地址。以下是 `/etc/hosts` 文件中的一行典型示例：

```text
127.0.0.1    hnpb200    localhost.localdomain    localhost
```

这一行表示 IP 地址 `127.0.0.1` 被分配给主机名 `lnbp200`、`localhost.localdomain` 和 `localhost`。

在最新的 Linux 内核版本中——即使用 GNU C 库（`glibc`）2 或更高版本的版本——名称服务切换（NSS）文件 `/etc/nsswitch.conf` 控制着解析器库、NIS、NIS+ 以及诸如 `/etc/hosts` 和 `/etc/shadow` 等本地文件等服务之间的交互方式。例如，`/etc/nsswitch.conf` 文件中的以下 `hosts` 条目指定解析器库首先尝试 `/etc/hosts` 文件，然后尝试 NIS+，最后尝试 DNS：

```
hosts: files nisplus dns
```

要了解更多关于 `/etc/nsswitch.conf` 文件及其功能的信息，请在终端窗口中输入 `man nsswitch.conf`。

### 配置缓存名称服务器

一种简单但有用的名称服务器是能够通过使用其他名称服务器找到主机名查询的答案，并记住该答案（通过将其保存在缓存中）以供下次使用。这种缓存名称服务器可以缩短访问最近访问过的主机所需的时间；因为答案已经存在于缓存中。

当您安装 BIND 时，缓存名称服务器的配置文件也会随之安装。这意味着您可以毫不费力地开始运行缓存名称服务器。本节介绍了配置文件以及启动缓存名称服务器所需执行的操作。

## /etc/named.conf 文件

您需要第一个配置文件是 `/etc/named.conf`。（实际上，这是 Fedora Core 和 SUSE 中的名称；在 Debian、MEPIS、Ubuntu 和 Xandros 中，BIND 配置文件称为 `/etc/bind/named.conf`。）`named` 服务器启动时会读取此配置文件。如果您安装了 BIND，则已经拥有此文件。以下是一个来自 Fedora Core 的 `/etc/named.conf` 文件：

```
options {
  directory "/var/named";
  dump-file "/var/named/data/cache_dump.db";
  statistics-file "/var/named/data/named_stats.txt";
  /
  * If there is a firewall between you and nameservers you want
  * to talk to, you might need to uncomment the query-source
  * directive below. Previous versions of BIND always asked
  * questions using port 53, but BIND 8.1 uses an unprivileged
  * port by default.
  */
  // query-source address * port 53;
};
```

//
// a caching only nameserver config
//

controls {



```
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

    file "localhost.zone";

    allow-update { none; };

};

zone "0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.ip6.arpa" IN {

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

注释采用 C 风格（`/* ... */`）或 C++ 风格（以 `//` 开头）。该文件包含用花括号（`{...}`）包围并以分号（`;`）结尾的块语句。块语句本身又包含其他语句，每条语句都以分号结尾。

这个 `/etc/named.conf` 文件以一个 `options` 块语句开头，其中包含多个选项语句。`directory` 选项语句告诉 `named` 在哪里查找配置文件中列出的所有其他文件。在这种情况下，`named` 在 `/var/named` 目录中查找文件。

### 发行版特定内容

在 `SUSE` 中，`/etc/named.conf` 中的 `directory` 选项指的是 `/var/lib/named` 目录，这意味着所有其他 BIND 配置文件都位于 `/var/lib/named` 中。在 `Debian` 和 `Xandros` 中，配置文件被明确指定位于 `/etc/bind` 目录中。

### 技术细节

`/etc/named.conf` 中的 `controls` 语句包含安全信息，以便 `rndc` 命令能够连接到 `named` 服务的 953 端口并与 `named` 进行交互。在这种情况下，`controls` 语句包含以下行：

```
inet 127.0.0.1 allow { localhost; } keys { rndckey; };
```

此命令表示 `rndc` 可以使用名为 `rndc` 的密钥从 `localhost` 连接。（文件 `/etc/rndc.key` 定义了密钥和使用的加密算法。）

### 技术细节

`rndc`（远程名称守护进程控制）实用程序是旧版 `ndc`（名称守护进程控制器）实用程序的后继者，用于通过特殊的控制通道（`named` 监听消息的 TCP 端口）向 `named` 服务器发送消息以对其进行控制。`rndc` 实用程序使用加密密钥向 `named` 服务器进行身份验证。`named` 服务器拥有相同的加密密钥，因此它可以解码由 `rndc` 发送的认证信息。

在 `options` 语句之后，`/etc/named.conf` 文件包含多个 `zone` 语句，每个语句都用花括号包围并以分号结尾。每个 `zone` 语句定义一个区域。第一个名为 `.`（根区域）：它是一个提示区域，指定了根名称服务器。（当 DNS 服务器启动时，它使用提示区域来找到根名称服务器并获取最新的根名称服务器列表。）

`/etc/named.conf` 中接下来的两个 `zone` 语句是主区域。（主区域只不过是域数据的主副本。）互联网类区域（由 `IN` 关键字指示）的主区域语句的语法如下：

```
zone "zone-name" IN {
type master;
file "zone-file";
[...other optional statements...]
};
```

`zone-name` 是区域的名称，`zone-file` 是包含该区域资源记录（RR）——即数据库条目——的区域文件。我在接下来的两节中描述了区域文件格式和资源记录格式。

## 区域文件格式

区域文件通常以多个指令开头，每个指令都以美元符号（`$`）后跟一个关键字开始。两个常用的指令是 `$TTL` 和 `$ORIGIN`。

例如，该行

```
$TTL      86400
```

使用 `$TTL` 指令为后续未定义 TTL 的记录设置默认的生存时间（TTL）。数值以秒为单位，有效的 TTL 范围是 0 到 2147483647 秒。在这种情况下，该指令将默认 TTL 设置为 86400 秒（或一天）。

`$ORIGIN` 指令设置附加到任何未限定记录上的域名。例如，以下 `$ORIGIN` 指令将域名设置为 `localhost.`：

```
$ORIGIN localhost.
```

如果没有 `$ORIGIN` 指令，初始 `$ORIGIN` 与 `/etc/named.conf` 文件中 `zone` 关键字后面的区域名称相同。

在指令之后，区域文件包含一个或多个资源记录。这些记录遵循特定的格式，我在下一节中概述了该格式。

## 资源记录（RR）格式

在您理解并智能地使用区域文件之前，必须理解资源记录的格式。每个资源记录具有以下格式。（可选字段用方括号表示。）

```
[domain] [ttl] [class] type data [;comment]
```



字段由制表符或空格分隔，并可能包含一些特殊字符，例如用于域名的 `@` 符号和表示注释开始的分号 (`;`)。

第一个字段，必须从行的第一个字符开始，标识域名。您可以使用 `@` 符号为此记录使用当前的 `$ORIGIN` 作为域名。如果您有针对相同域名名的多个记录，请留第一个字段为空。

可选的 `ttl` 字段指定生存时间（Time To Live）——数据可以被缓存并视为有效的时间长度。您可以使用以下任一格式指定持续时间：

- `$N$`，其中 `$N$` 是表示 `$N$` 秒的数字
- `$Mw$`，其中 `$M$` 是表示 `$M$` 周的数字
- `$Md$`，其中 `$M$` 是表示 `$M$` 天的数字
- `$Mh$`，其中 `$M$` 是表示 `$M$` 小时的数字
- `$Mm$`，其中 `$M$` 是表示 `$M$` 分钟的数字
- `$Ms$`，其中 `$M$` 是表示 `$M$` 秒的数字

字母 `$W, D, H, M$` 和 `$S$` 也可以是小写的。因此，您可以写 `86400` 或 `1D`（或 `1d`）来表示一天的持续时间。您还可以将这些组合起来指定更精确的持续时间，例如 `5w6d1h16m` 表示 5 周、6 天、1 小时和 16 分钟。

`class` 字段指定网络类型。该字段最常用的值是 `$IN$`，代表 Internet。

资源记录中的下一个是 `*type*` 字段，它表示记录的类型（例如 `$SOA$`、`$NS$`、`$A$` 或 `$PTR$`）。表 5-1 列出了 DNS 资源记录类型。接下来是数据字段，它取决于 `*type*` 字段。

### 表 5-1 DNS 资源记录类型

| Type | Name | Description |
| :--- | :--- | :--- |
| A | IPv4 Address | 指定与主机名对应的 IPv4 地址 |
| AAAA | IPv6 Address | 指定与名称对应的 IPv6 主机地址 |
| AS | Address | 指定与主机名对应的 IP 地址 |
| CERT | Digital Certificate | 保存数字证书 |
| CNAME | Canonical Name | 定义主机名的昵称或别名 |
| DNAME | Delegation Name | 用另一个要查找的名称替换指定的域名 |
| HINFO | Host Info | 标识主机的硬件和操作系统 |
| KEY | Public Key | 保存与 DNS 名称关联的公钥 |

### 表 5-1（续）

| 类型 | 名称 | 描述 |
| :--- | :--- | :--- |
| MX | 邮件交换器 | 识别接受发往特定域名的邮件的主机（用于路由电子邮件） |
| NS | 名称服务器 | 标识区域的权威名称服务器 |
| PTR | 指针 | 指定地址对应的名称（用于反向映射——将 IP 地址转换为主机名） |
| RP | 负责人 | 提供域名的技术联系人姓名 |
| SIG | 签名 | 包含在安全 DNS 中经过认证的数据（详细信息参见 RFC 2535） |
| SOA | 权威开始 | 表示后续所有记录对该区域均为权威 |
| SRV | 服务 | 列出域名提供的知名网络服务 |
| TXT | 文本 | 用于在 DNS 数据库中包含注释和其他信息 |

请阅读区域文件中的资源记录，至少包括类型 `SOA`、`NS`、`A`、`PTR` 和 `MX` 的记录，这些是最常用的几种类型。（您可以在 Debian 和 Xandros 的 `/etc/bind` 目录、Fedora Core 的 `/var/named` 目录以及 SUSE 的 `/var/lib/named` 目录中找到区域文件。）接下来，我将简要描述这些记录，并通过示例说明每种记录类型。

典型的 `SOA` 记录具有以下格式：

```
@   1D IN SOA     @ root (
                    42      ; serial
                    3h      ; refresh -- 3 hours
                    15m     ; retry -- 15 minutes
                    1w      ; expiry -- 1 week
                    1D )    ; minimum -- 1 day
```

第一个字段指定域名为 `@`，这意味着当前域名（默认为区域名称，如在 `/etc/named.conf` 文件中所示）。下一个字段指定该记录的生存时间（TTL）为一 天。类字段设置为 `IN`，表示该记录用于互联网。类型字段指定记录类型为 `SOA`。其余字段构成了 `SOA` 记录的数据。数据包括主名称服务器的名称（在此情况下为 `@`，即当前域名）、技术联系人的电子邮件地址，以及括号内的五个不同时间值。

`NS` 记录指定区域的权威名称服务器。典型的 `*NS*` 记录如下所示：

```
. 3600000 IN NS A.ROOT-SERVERS.NET.
```

在这种情况下，`*NS*` 记录列出了根区域的权威名称服务器。（请注意，第一个字段的名称是一个点。）`*生存时间*` 字段指定该记录的有效性为 1000 小时（3600000 秒）。`*类*` 为 `*IN*`，代表互联网；`*记录类型*` 为 `*NS*`。最后一个字段列出了名称服务器的名称（`*A.ROOT-SERVERS.NET.*`），以点结尾。

`*A*` 记录指定名称对应的地址。例如，以下 `*A*` 记录显示 `*A.ROOT-SERVERS.NET.*` 的地址为 `*198.41.0.4*`：

```
A.ROOT-SERVERS.NET. 3600000 A 198.41.0.4
```

在这种情况下，未指定网络类，因为该字段是可选的，默认值为 `*IN*`。

`*PTR*` 记录用于反向映射——将地址转换为名称。考虑以下示例：

```
1 IN PTR localhost.
```

该记录来自一个名为 `*0.0.127.in-addr.arpa*` 的区域文件。因此，该记录表示与地址 `*127.0.0.1*` 关联的名称是 `*localhost*`。

`*MX*` 记录指定代表特定域接受邮件的主机名称。例如，这是一个典型的 `*MX*` 记录：

```
naba IN MX 10 mailhub.lnbsfott.com.
```

该记录表示发往当前域名中名为 `*naba*` 的主机的邮件将发送到 `*mailhub.lnbsfott.com*`。（该主机被称为 `*邮件交换器*`。）数字 10 是优先级值。对于具有不同优先级值的多个 `*MX*` 记录列表，会先尝试优先级值较低的那些。

掌握了一些关于资源记录的知识后，您可以浏览缓存名称服务器的区域文件。

## 根区域文件

关于十三个根名称服务器的信息位于 `*/etc/named.conf*` 文件中根区域区域语句引用的区域文件中。

（在 Fedora Core 中，根区域文件是 `/var/named/named.ca`；在 Debian、MEPIS、Ubuntu 和 Xandros 中是 `/etc/bind/db.root`；在 SUSE 中是 `/var/lib/named/root.hint`。）以下列表展示了根区域文件：

```
This file holds the information on root name servers needed to
initialize cache of Internet domain name servers
(e.g. reference this file in the "cache . <files>"
configuration file of BIND domain name servers).
This file is made available by InterNIC
under anonymous FTP as
file       /domain/named.cache
on server    FTP.INTERNIC.NET
-OR-         RS.INTERNIC.NET
last update:  Jan 29, 2004
related version of root zone:   2004012900
; formerly NS.INTERNIC.NET
       3600000      IN  NS  A.ROOT-SERVERS.NET.
A.ROOT-SERVERS.NET.   3600000      A 198.41.0.4
; formerly NS1.ISI.EDU
       3600000      NS  B.ROOT-SERVERS.NET.
B.ROOT-SERVERS.NET.   3600000      A 192.228.79.201
; formerly C.PSI.NET
       3600000      NS  C.ROOT-SERVERS.NET.
C.ROOT-SERVERS.NET.   3600000      A 192.33.4.12
; formerly TERP.UMD.EDU
```



## 根名称服务器记录

```
3600000      NS  D.ROOT-SERVERS.NET.
D.ROOT-SERVERS.NET.   3600000      A 128.8.10.90
; formerly NS.NASA.GOV
       3600000      NS  E.ROOT-SERVERS.NET.
E.ROOT-SERVERS.NET.   3600000      A 192.203.230.10
; formerly NS.ISC.ORG
       3600000      NS  F.ROOT-SERVERS.NET.
F.ROOT-SERVERS.NET.   3600000      A 192.5.5.241
; formerly NS.NIC.DDN.MIL
       3600000      NS  G.ROOT-SERVERS.NET.
G.ROOT-SERVERS.NET.   3600000      A 192.112.36.4
; formerly NOS.ARL.ARMY.MIL
       3600000      NS  H.ROOT-SERVERS.NET.
H.ROOT-SERVERS.NET.   3600000      A 128.63.2.53
; formerly NIC.NORDU.NET
.				3600000	NS	I.ROOT-SERVERS.NET.
I.ROOT-SERVERS.NET.	3600000	A	192.36.148.17
; operated by VeriSign, Inc.
.				3600000	NS	J.ROOT-SERVERS.NET.
J.ROOT-SERVERS.NET.	3600000	A	192.58.128.30
; operated by RIPE NCC
				3600000	NS	K.ROOT-SERVERS.NET.
K.ROOT-SERVERS.NET.	3600000	A	193.0.14.129
; operated by ICANN
				3600000	NS	L.ROOT-SERVERS.NET.
L.ROOT-SERVERS.NET.	3600000	A	198.32.64.12
; operated by WIDE
				3600000	NS	M.ROOT-SERVERS.NET.
M.ROOT-SERVERS.NET.	3600000	A	202.12.27.33
; End of File
```

该文件包含 `NS` 和 `A` 资源记录，指定了根区域的权威名称服务器名称及其地址（在每个 `NS` 记录的第一字段中用点表示根区域）。

文件中的注释行以分号开头。这些注释提供了关于根名称服务器位置的线索。互联网有 13 个根名称服务器，大多数根服务器位于美国。此文件对任何名称服务器都是必需的，因为名称服务器必须能够至少到达一个根名称服务器。

## localhost.zone 文件

`/etc/named.conf` 文件包含一个针对 `localhost` 区域的区域语句，指定区域文件为 `localhost.zone`。该文件在 Fedora Core 中位于 `/var/named` 目录，在 SUSE 中位于 `/var/local/named` 目录，在 Debian 和 Xandros 中位于 `/etc/bind/db.local`。以下是 `localhost.zone` 文件内容的列表：

```
$TTL	86400

$ORIGIN localhost.

	@		1D IN SOA		@ root (

					42			; serial (d. adams)

					3H			; refresh

					15M			; retry

					1W			; expiry

					1D )			; minimum

	@ IN NS				localhost.

	ID IN A				127.0.0.1
```

## 656 配置 DNS

该区域文件以一个 `$TTL` 指令开始，为后续未定义 TTL 的记录将默认生存时间（TTL）设置为一 天（86400 秒）。接下来，`$ORIGIN` 指令将域名设置为 `localhost`。

在这两个指令之后，`localhost.zone` 文件包含三个资源记录（RR）：一个 `SOA` 记录、一个 `NS` 记录和一个 `A` 记录。`SOA` 和 `NS` 记录指定 `localhost` 为该区域的主权威名称服务器。`A` 记录指定 `localhost` 的地址为 `127.0.0.1`。

## 反向映射 127.0.0.1 的区域文件

`/etc/named.conf` 文件中的第三个区域语句指定了一个名为 `0.0.127.in-addr.arpa` 的反向映射区域。对于此区域，区域文件在 Fedora Core 中是 `/var/named/named.local`，在 SUSE 中是 `/var/lib/named/127.0.0.zone`，在 Debian、MEPIS、Ubuntu 和 Xandros 中是 `/etc/bind/db.127`。该区域文件包含以下内容：

```
$TTL          86400

@       IN      SOA     localhost. root.localhost.   (

                                1997022700 ; Serial

                                288000 ; Refresh

                                14400  ; Retry

                                3600000; Expire

                                86400 ) ; Minimum

        IN      NS      localhost.

1       IN      PTR     localhost.
```

`SOA` 和 `NS` 记录指定 `localhost` 为主名称服务器。`PTR` 记录指定 `localhost` 为地址 `127.0.0.1` 对应的名称。

![](img/792720823146d68f19fd50c99ebfce4b_681_0.png)

`SOA` 记录还显示 `root.localhost.` 为该域名技术联系人的电子邮件地址。请注意，DNS 区域文件使用 `user.host.`（注意结尾的点）格式表示电子邮件地址。当向联系人发送任何电子邮件时，您必须将第一个点替换为 `@` 并删除最后一个点。

## 缓存名称服务器：启动和测试

在您研究了缓存名称服务器的配置文件后，您可以启动名称服务器并观察其运行状态。

![](img/792720823146d68f19fd50c99ebfce4b_681_1.png)

要启动名称服务器，请登录为 `root` 并在 Fedora Core 和 SUSE 中键入 `/etc/init.d/named start`。为确保每次重启系统时 `named` 服务器都能启动，请在 Fedora Core 和 SUSE 中键入 `chkconfig --level 35 named on`。在 Debian、MEPIS、Ubuntu 和 Xandros 中，键入 `/etc/init.d/bind9 start` 来启动 `named` 服务器。

命名服务器（`named`）会在 `/var/log/messages` 文件中写入诊断日志消息。启动 `named` 后，你可以打开 `/var/log/messages` 文本文件来检查日志消息。如果没有来自 `named` 的错误消息，你就可以继续测试 `named` 服务器了。

![](img/792720823146d68f19fd50c99ebfce4b_682_0.png)

在尝试缓存域名服务器之前，你必须将该域名服务器指定为首选服务器。为此，请确保 `/etc/resolv.conf` 文件的第一行是以下内容：

```
nameserver 127.0.0.1
```

现在你可以使用 `host` 命令来测试域名服务器。例如，若要使用 localhost 上的缓存域名服务器查询 `www.gao.gov` 的 IP 地址，请输入以下命令：

```
host www.gao.gov localhost
```

以下是 `host` 命令的结果输出：

```
Using domain server:
Name: localhost
Address: 127.0.1#53
Aliases:
www.gao.gov has address 161.203.16.2
```



如输出所示，`host` 命令使用 localhost 作为 DNS 服务器，并返回了 www.gao.gov 的 IP 地址。如果你得到类似的输出，说明缓存域名服务器已经运行正常。

## 配置主要域名服务器

配置主要域名服务器最好的方法是先配置一个缓存域名服务器（如前几节所述）。然后，为你希望该域名服务器作为主要服务器的域添加主区域。例如，假设我要为 `naba.net` 域定义一个主要域名服务器。以下是我在 Fedora Core 系统上配置该主要域名服务器所经过的步骤（以 `root` 身份登录后）：

1. **在 `/etc/named.conf` 文件中添加以下区域声明：**

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

2. **创建包含以下内容的区域文件** `/var/named/naba.zone` **：**

```
$TTL	86400
$ORIGIN naba.net.
	@		IN	SOA	@ root.naba.net (
						100		; serial
						3H		; refresh
						15M		; retry
						1W		; expiry
						1D )
						; minimum
		1D IN NS		@
		1D IN A		192.168.0.7
wxp	IN	A	192.168.0.2
```

3. **创建包含以下内容的区域文件** `/var/named/0.168.192.zone` **：**

```
$TTL	86400
; Remember zone name is: 0.168.192.in-addr.arpa
	@	IN	SOA	naba.net. root.naba.net {
			1		; Serial
			28800		; Refresh
			14400		; Retry
			3600000	; Expire
			86400 )	; Minimum
			IN	NS	naba.net.
7	IN	PTR	naba.net.
2	IN	PTR	wxp.naba.net.
```

4. **要测试新配置，使用以下命令重启 named 服务器：**

```
/etc/init.d/named restart
```

5. **使用** `dig` **或** `host` **向 DNS 服务器发起查询。**

例如，以下是我如何使用 `host` 命令在运行于 `localhost` 的 DNS 服务器上检查主机 `wxp.naba.net` 地址的方法：

```
host wxp.naba.net localhost
```

该命令产生以下输出：

```
Using domain server:
Name: localhost
Address: 127.0.0.1#53
Aliases:
wxp.naba.net has address 192.168.0.2
```

如果你想使用 `dig` 来检查 DNS 服务器，请输入以下命令：

```
dig @localhost wxp.naba.net
```

其中的 `@localhost` 部分指定了 `dig` 联系的那个 DNS 服务器。

当你成功使用 `dig` 联系到 DNS 服务器后，你可以询问服务器执行更复杂的操作。例如，以下是我用来尝试针对 IP 地址 192.168.0.2 执行反向查找的命令：

```
host 192.168.0.2 localhost
```

该命令显示以下输出：

```
Using domain server :
Name: localhost
Address: 127.0.0.1#53
Aliases:
2.0.168.192.in-addr.arpa domain name pointer wxp.naba.net
```

# 第 6 章：使用 Samba 和 NFS

- **本章内容**
    - 使用 NFS 共享文件
    - 安装和配置 Samba
    - 使用 Samba 设置 Windows 服务器

如果你的局域网与许多其他网络类似，它就需要具备在运行 Linux 的系统与其他非 Linux 系统之间共享文件的能力。因此，Linux 包含了两个突出的文件共享服务：

- **网络文件系统（NFS）** 用于与其他 UNIX 系统（或安装了 NFS 客户端软件的 PC）共享文件。
- **Samba** 用于与 Windows 系统进行文件共享和打印共享。

在本章中，我将描述如何使用 NFS 和 Samba 两种方式来共享文件。

### 使用 NFS 共享文件

通过 NFS 共享文件很简单，涉及两个基本步骤：

- 在运行 NFS 服务器的 Linux 系统上，你需要通过在 `/etc/exports` 文件中列出一个或多个目录并运行 `exports` 命令来导出（共享）这些目录。此外，你必须启动 NFS 服务器。
- 在每个客户端系统上，你使用 `mount` 命令挂载服务器已导出的目录。

使用 NFS 唯一的缺点是每个客户端系统都必须支持它。微软 Windows 并不附带 NFS。这意味着如果你想使用 NFS 共享文件，必须单独购买 NFS 软件。然而，如果你局域网中的所有系统都运行 Linux（或其他内置支持 NFS 的 UNIX 变体），那么使用 NFS 是合理的。

![](img/792720823146d68f19fd50c99ebfce4b_686_0.png)

NFS 存在安全漏洞。因此，不应在未使用随 NFS 版本 4（NFSv4）提供的 RPCSEC_GSS 安全机制的情况下，直接在连接到互联网的系统上设置 NFS。

![](img/792720823146d68f19fd50c99ebfce4b_687_0.png)

Linux 2.6 内核内置了对 NFSv4 的支持，它是基于早期版本的 NFS 构建的。但与早期版本不同，NFSv4 具有更强的安全性，并旨在互联网环境中运行。（RFC 3510 描述了 NFSv4；参见 `http://www.ietf.org/rfc/rfc3530.txt`。）NFSv4 使用 RPCSEC_GSS（GSS 代表通用安全服务，Generic Security Services）协议进行安全保护。你可以继续使用基于用户 ID 和组 ID 的旧式认证与 NFSv4，但如果你想使用 RPCSEC_GSS，你需要运行三个额外的服务——服务器上的 `rpcsvcgssd`、客户端上的 `rpcgssd`，以及客户端和服务器上都运行的 `rpcidmapd`。有关 Linux 中 NFSv4 实现的更多信息，请访问 `http://www.citi.umich.edu/projects/nfs4/linux`。

在接下来的几个部分中，我将带你通过一个局域网中两台 Linux PC 的示例来设置 NFS。

### 使用 NFS 导出文件系统

从服务器系统开始，该服务器系统 *导出*——即向客户端系统提供——某个目录的内容。在服务器上，你必须运行 NFS 服务，并指定一个或多个要导出的文件系统。

要导出文件系统，你需要在 `/etc/exports` 文件中添加相应的条目。例如，假设你要导出 `/home` 目录，并希望允许名为 LNBPT5 的主机挂载此文件系统以进行读写操作。你可以通过在 `/etc/exports` 文件中添加以下条目来实现：

```
/home LNBPT5 (rw, sync)
```

如果你想赋予诸如 192.168.0.0 这样的局域网内所有主机访问权限，你可以将此行更改为

```
/home 192.168.0.0/24 (rw, sync)
```

`/etc/exports` 文件中的每一行都具有以下通用格式：

```
directory host1(options) host2(options) ...
```

第一个字段是通过 NFS 共享的目录，随后是一个或多个字段，指定哪些主机可以远程挂载该目录，以及括号内的若干选项。你可以使用名称或 IP 地址（包括地址范围）来指定主机。

括号内的选项表示授予每个主机的访问类型，以及服务器的用户 ID 和组 ID 如何映射到客户端上的 ID。（例如，如果文件在服务器上由 root 拥有，那么在客户端上它是谁拥有的？）在括号内，逗号分隔各个选项。例如，如果允许主机同时具有读写权限——并且所有 ID 都映射到**匿名用户**（默认这是名为 **nobody** 的用户）——那么选项如下所示：

```
(rw, all_squash)
```



表 6-1 显示了你可以在 `/etc/exports` 文件中使用的选项。你会发现有两种类型的选项——通用选项和用户 ID 映射选项。

**表 6-1 /etc/exports 中的选项**

| 此选项 | 执行以下操作 |
| :--- | :--- |
| **通用选项** | |
| *insecure* | 允许来自 1024 或更高端口的连接 |
| *ro* | 允许只读访问（默认） |
| *rw* | 允许读写访问 |
| *sync* | 在请求时执行写操作（将信息写入磁盘）（默认） |
| *async* | 在服务器准备好时执行写操作 |
| *no_wdelay* | 立即执行写操作 |
| *wdelay* | 稍等一下，看看是否有相关的写请求到达，然后一起执行（默认） |
| *hide* | 隐藏作为另一个已导出目录子目录的已导出目录（默认） |
| *no_hide* | 行为与 *hide* 完全相反 |
| *subtree_check* | 执行子树检查，即在访问文件时检查已导出子目录的父目录（默认） |
| *no_subtree_check* | 关闭子树检查（与 *subtree_check* 相反） |
| *insecure_locks* | 允许不安全的文件锁定 |
| **用户 ID 映射选项** | |
| *all_squash* | 将所有用户 ID 和组 ID 映射到客户端上的 *匿名用户* |
| *no_all_squash* | 将远程用户 ID 和组 ID 映射到客户端上类似的 ID（默认） |
| *root_squash* | 将远程 *root* 用户映射到客户端上的 *匿名用户*（默认） |
| *no_root_squash* | 将远程 *root* 用户映射到本地的 *root* 用户 |
| *anonuid=UID* | 设置用于 *all_squash* 和 *root_squash* 选项的 *匿名用户* 的用户 ID |
| *anongid=GID* | 设置用于 *all_squash* 和 *root_squash* 选项的 *匿名用户* 的组 ID |

![](img/792720823146d68f19fd50c99ebfce4b_688_0.png)

第七卷
第 6 章
使用 Samba 和 NFS

在 `/etc/exports` 文件中添加条目后，请在终端窗口中键入以下命令手动导出文件系统：

```
exportfs -a
```

此命令将导出 `/etc/exports` 文件中定义的所有文件系统。

现在您可以启动 NFS 服务器进程。

![](img/792720823146d68f19fd50c99ebfce4b_689_0.png)

在 Debian 中，登录为 `root` 用户，并在终端窗口中键入 `/etc/init.d/nfs-kernel-server start` 来启动 NFS 服务器。在 Fedora Core 中，键入 `/etc/init.d/nfs start`。在 SUSE 中，键入 `/etc/init.d/nfsserver start`。如果希望 NFS 服务器在系统启动时自动启动，请在 Debian 中键入 `update-rc.d nfs-kernel-server defaults`。在 Fedora Core 中，键入 `chkconfig --level 35 nfs on`。在 SUSE 中，键入 `chkconfig --level 35 nfsserver on`。在 Xandros 中，键入 `update-rc.d nfs-user-server defaults`。

当 NFS 服务启动后，NFS 的服务器端即准备就绪。现在您可以尝试从客户端系统挂载导出的文件系统，然后根据需要访问该导出的文件系统。

![](img/792720823146d68f19fd50c99ebfce4b_689_1.png)

如果您对 `/etc/exports` 文件中列出的导出文件系统进行了任何更改，请记得重启 NFS 服务。要重启服务，请在 `/etc/init.d` 目录中调用脚本，并以 `restart` 作为参数（而不是启动服务时使用的 `start` 参数）。

# 挂载 NFS 文件系统

要在客户端系统上访问已导出的 NFS 文件系统，您必须将该文件系统挂载到一个挂载点上。*挂载点* 无非就是一个本地目录。例如，假设您想要访问服务器 `LBNP200` 导出的 `/home` 目录，并将其挂载到客户端系统上的本地目录 `/mnt/lbnp200`。为此，请按照以下步骤操作：

1. **登录为 `root` 并使用以下命令创建目录：**

```sh
mkdir /mnt/lbnp200
```

2. **键入以下命令，将远程系统（LBNP200）的目录挂载到本地目录 `/mnt/lbnp200` 上：**

```sh
mount lbnp200:/home /mnt/lbnp200
```

完成这些步骤后，您就可以从本地目录 `/mnt/lbnp200` 查看和访问导出的文件。

要确认 NFS 文件系统确实已挂载，请以 `root` 身份登录客户端系统，并在终端窗口中键入 `mount`。您会看到关于 NFS 文件系统的一行信息，类似于以下内容：

```
lbnp200:/home/public0 /mnt/lbnp200 type nfs (rw,addr=192.168.0.4)
```



NFS 支持两种类型的挂载操作——硬挂载（`hard`）和软挂载（`soft`）。默认情况下是硬挂载，这意味着如果 NFS 服务器没有响应，客户端会持续尝试访问服务器，直到服务器响应为止。您可以通过在 `mount` 命令中添加 `-o soft` 选项来实现 NFS 卷的软挂载。对于软挂载，如果 NFS 服务器未能响应，客户端将返回错误。

## 使用 Samba 设置 Windows 服务器

如果您依赖 Windows 进行文件共享和打印共享，那么您可能在服务器和客户端上都使用 Windows。如果是这样，您仍然可以将 Linux PC 作为服务器，而不会失去 Windows 的文件共享和打印共享功能；您可以将 Linux 设置为 Windows 服务器。当您从本书的配套 DVD-ROM 安装 Linux 时，您也有机会安装 Samba 软件包，该软件包会执行此设置。您只需在安装期间选择 Windows File Server 软件包组即可。

在您的 Linux PC 上安装并配置 Samba 后，您的客户端 PC——即使是运行旧版 Windows for Workgroups 操作系统或较新的 Windows 95/98/NT/2000/XP 版本的计算机——都可以访问 Linux PC 上共享的磁盘和打印机。为此，它们使用服务器消息块（SMB）协议，即 Windows 文件和打印共享的底层协议。

安装了 Samba 软件包后，您可以将 Linux PC 设为 Windows 客户端，这意味着 Linux PC 可以访问由 Windows 服务器管理的磁盘和打印机。同时，您的 Linux PC 也可以作为网络中其他 Windows 系统的客户端。

Samba 软件包包含以下主要组件：

- `/etc/samba/smb.conf`：这是 SMB 服务器使用的 Samba 配置文件。
- `/etc/samba/smbusers`：这个 Samba 配置文件显示了与本地 Linux PC 上用户名相对应的 Samba 用户名。
- `nmbd`：这是 NetBIOS 名称服务器，客户端使用它来查找服务器。（NetBIOS 代表 `Network Basic Input/Output System`——应用程序用于与网络传输（如 TCP/IP）通信的接口。）
- `nmblookup`：此命令返回由 NetBIOS 名称标识的 Windows PC 的 IP 地址。
- `smbadduser`：此程序将用户添加到 SMB（Server Message Block）密码文件中。
- `smbcacls`：此程序操纵共享文件上的 Windows NT 访问控制列表（ACLs）。
- `smbclient`：这是 Windows 客户端，它在 Linux 上运行，允许 Linux 访问任何 Windows 服务器上的文件和打印机。
- `smbcontrol`：此程序向 `smbd`、`nmbd` 或 `winbind` 进程发送消息。
- `smbd`：这是 SMB 服务器，它接受来自 Windows 客户端的连接，并提供文件共享和打印共享服务。
- `smbmount`：此程序在 Linux PC 上挂载 Samba 共享目录。
- `smbpasswd`：此程序更改 SMB 用户的密码。
- `smbprint`：此脚本启用在 SMB 服务器上的打印机上打印。
- `smbstatus`：此命令列出本地主机当前的 SMB 连接。
- `smtar`：此程序直接将 SMB 共享备份到 Linux 系统上的磁带驱动器。
- `smbumount`：此程序卸载当前已挂载的 Samba 共享目录。
- `testparm`：此程序确保 Samba 配置文件是正确的。
- `winbindd`：此服务器从 Windows NT 服务器解析名称。

在以下章节中，我将描述如何配置和使用 Samba。

### 安装 Samba

在安装 Linux 时，您可能已经安装了 Samba。您可以先检查一下，如果未在系统上找到 Samba，您可以轻松安装它。

![](img/792720823146d68f19fd50c99ebfce4b_691_0.png)

在 Debian、MEPIS、Ubuntu 和 Xandros 中，键入 `dpkg -l samba*` 以查看是否已安装 Samba。在 Fedora Core 和 SUSE 中，键入 `rpm -q samba` 以查看是否已安装 `samba` 软件包。

![](img/792720823146d68f19fd50c99ebfce4b_691_1.png)

在 Debian、MEPIS 和 Ubuntu 中，键入 `apt-get install samba` 来安装 Samba。在 Fedora Core 中，登录为 `root`，挂载 DVD，然后键入 `cd /media/cdrom/Fedora/RPMS`，接着键入 `rpm -ivh samba*`。在 SUSE 中，点击 YaST 控制中枢软件类别中的软件管理。然后使用 YaST 的搜索功能查找 `samba`，选择相关软件包并安装它们。至于 Xandros，安装 Xandros 时即可获得 Samba。

安装 Samba 软件后，您必须在配置 Samba 之后才能使用它。

## 配置 Samba

要设置 Windows 文件共享和打印共享服务，您可以手动编辑配置文件或使用图形用户界面（GUI）工具。当然，使用 GUI 工具比编辑配置文件容易得多。Fedora Core 和 SUSE 附带用于配置 Samba 服务器的 GUI 工具。

在 Fedora Core 中，选择“桌面 > 系统设置 > 服务器设置 > Samba”以打开 Samba 服务器配置窗口。点击“添加”并填写您希望与 Windows 系统共享的目录信息，如图 6-1 所示。点击“访问”选项卡以指定哪些用户可以访问共享目录。Samba 服务器配置工具通过在配置文件 `/etc/samba/smb.conf` 中添加条目来创建 Samba 共享。

![](img/792720823146d68f19fd50c99ebfce4b_692_0.png)

在 SUSE 中，您可以通过 YaST 控制中枢配置 Samba——选择“主菜单 > 系统 > 控制中枢 (YaST)”，点击窗口左侧的“网络服务”，然后点击窗口右侧的“Samba 服务器”。YaST 显示一个窗口（见图 6-2），您可以通过该窗口配置 Samba。首先，您选择一个工作组名称（YaST 会显示局域网上任何现有 Windows 工作组的名称）并点击“下一步”。然后，您可以选择服务器类型，启用服务器，并选择您希望共享的内容。退出 Samba 服务器配置实用程序后，YaST 会将 Samba 设置存储在 `/etc/samba` 目录中的配置文件中。

![](img/792720823146d68f19fd50c99ebfce4b_693_0.png)

图 6-2：在 SUSE 中，你可以通过 YaST 配置 Samba 服务器。

配置完 Samba 后，在终端窗口中输入以下命令以验证 Samba 配置文件是否正常：

```
testparm
```



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

如果该命令显示成功加载了文件，那么你就已经设置完毕。`testparm`命令还会显示 Samba 配置文件的内容。

Samba 使用`/etc/samba/smb.conf`文件作为其配置文件。这是一个文本文件，其语法类似于 Microsoft Windows 3.1 的 INI 文件。你可以使用 Linux 系统上的任何文本编辑器编辑该文件。与旧的 Windows INI 文件一样，`/etc/samba/smb.conf`文件由若干部分组成，每部分包含一个参数列表。`smb.conf`文件的每一部分都以括号中的部分名称开头。该部分持续直到下一部分开始或文件结束。每一行都使用`name = value`语法来指定参数的值。与 Windows INI 文件一样，注释行以分号（`;`）开头。在`/etc/samba/smb.conf`文件中，注释也可以以井号（`#`）开头。

若要使 Samba 服务在系统重启时自动启动，请在 Debian、MEPIS、Ubuntu 和 Xandros 中输入`update-rc.d samba defaults`。在 Fedora Core 和 SUSE 中，请输入`chkconfig --level 35 smb on`。若要立即启动 Samba，请在 Fedora Core 和 SUSE 中输入`/etc/init.d/smb start`。在 Debian、MEPIS、Ubuntu 和 Xandros 中，请输入`/etc/init.d/samba start`。

## 尝试使用 Samba

现在，你可以尝试从局域网中的某台 Windows 系统访问 Linux 系统上的 Samba 服务器。在 Windows 95/98/ME 桌面上双击“网上邻居”图标。在 Windows XP 中，选择“开始” → “我的网络位置”，然后单击“查看工作组计算机”。同一工作组中的所有计算机都会显示出来。

当你看到 Samba 服务器时，可以通过双击其图标来打开它。系统会提示你输入 Samba 用户名和密码，在正确输入这些信息后，你可以访问 Samba 共享上的文件夹和打印机（如果有）。

你可以使用`smbclient`程序来访问局域网中 Windows 系统上的共享目录和打印机，并确保你的 Linux Samba 服务器正在运行。一种快速的检查方法是在终端窗口中输入`smbclient -L`，以查看 Linux Samba 服务器本身的服务列表。

## 深入了解 Samba

Samba 的内容远不止本章所介绍的部分。若要了解更多关于 Samba 的信息，你可以参考以下资源：

- 若要在线查看 Samba 文档，请访问 www.samba.org/samba/docs/man/Samba-HOWTO-Collection。
- *Using Samba*（《Samba 使用指南》），第二版，作者为 Jay Ts、Robert Eckstein 和 David Collier-Brown（O'Reilly & Associates，2003 年 2 月）

你还应该访问 www.samba.org 以获取 Samba 开发方面的最新新闻。该网站还提供了学习 Samba 的相关资源链接。

# 第八卷

# 编程

The 5th Wave 作者：Rich Tennant

![](img/792720823146d68f19fd50c99ebfce4b_696_0.png)

# 目录概览

第 1 章：在 Linux 中编程 . 673

第 2 章：用 C 语言编程 . 699

第 3 章：编写 Shell 脚本 . 731

第 4 章：用 Perl 编程 . 743

## 第 1 章：在 Linux 中编程

**本章内容**

- 学习编程基础
- 探索 Linux 中的软件开发工具
- 使用 GCC 编译和链接程序
- 使用 make
- 使用 gdb 调试程序
- 理解 GNU、GPL 和 LGPL 的影响

Linux 预装了开发软件所需的所有工具。（你只需要安装它们即可。）特别是，它拥有所有的 GNU 软件开发工具，例如 GCC（C 和 C++ 编译器）、GNU make 以及 GNU 调试器。在本章中，我将向你介绍编程，描述这些软件开发工具，并展示如何使用它们。虽然我将使用 C 和 C++ 编程语言示例，但重点不在于展示如何用这些语言编程，而在于展示如何使用各种软件开发工具（如编译器、make 和调试器）。

我还简要介绍了自由软件基金会（Free Software Foundation）的 GNU 通用公共许可证（GPL）如何可能影响你开发 Linux 软件的计划。你需要了解这一点，因为你在 Linux 中开发软件时使用的是 GNU 工具和 GNU 库。

### 编程概述

如果你曾用任何编程语言编写过计算机程序，你可以很快开始在 Linux 系统上编写程序。但是，如果你从未编写过计算机程序，在开始之前你需要两个基本资源：了解编程基础知识，以及快速回顾计算机及其主要组成部分。在本节中，我将为你提供计算机编程的概述——足以让你入门。

#### 计算机的简化视图

在你熟悉计算机编程之前，你需要了解计算机程序在计算机的其他部分中处于什么位置。图 1-1 展示了计算机的简化视图，突出了对程序员重要的主要部分。

![](img/792720823146d68f19fd50c99ebfce4b_699_0.png)

计算机的核心是*中央处理单元*（CPU），它执行计算机程序中包含的指令。执行此任务的具体硬件部件（制造商称之为*微处理器*，而我们其他人称之为*芯片*）因系统而异：在 Pentium PC 中，它是 Pentium；在 Sun SPARC 工作站中，它是 SPARC 芯片；在 HP UNIX 工作站中，它是 PA-RISC 芯片。这些微处理器具有不同的能力，但使命相同：告诉计算机该做什么。

随机存取存储器（RAM），或简称*内存*，在 CPU 执行计算机程序时充当存储区。如果程序处理某些数据，这些数据也存储在内存中。内存的内容不是永久的；当计算机关闭或程序不再运行时，它们会消失（且永远不再返回）。

*硬盘*（也称为*磁盘*或*盘*）是计算机程序和数据永久性存储空间。硬盘由文件组成，这些文件又组织在层级目录和子目录中（有点像将纸质文件夹整理在文件柜的抽屉中）。每个文件基本上是一个存储块，可以容纳各种信息。例如，一个文件可能是人类可读的文本文件——也可能是一组只有 CPU 才能理解的计算机指令。当你创建计算机程序时，你会经常处理文件。

对于程序员来说，其他两个重要项目是*输入*和*输出*——程序如何从用户那里获取输入并向用户显示输出。用户通过键盘和鼠标提供输入，输出显示在监视器上。然而，程序也可以从文件接受输入并将输出发送到文件。

### 操作系统的角色

操作系统是一组特殊的计算机程序，其主要目的是加载和运行其他程序。操作系统还充当软件与硬件之间的接口。所有操作系统都包含一个或多个命令处理器（在 Linux 中称为 shell），允许用户输入命令并执行运行程序或打印文件等任务。大多数操作系统还包括图形用户界面（如 Linux 中的 GNOME 和 KDE），允许用户通过单击屏幕图标执行大多数任务。Linux、Windows（无论是 NT、2000 还是 XP 版本）以及各种版本的 UNIX（包括 Linux）都是操作系统的例子。

是操作系统赋予了计算机个性。例如，你可以在 PC 上运行 Windows 2000 或 Windows XP。在同一台 PC 上，你也可以安装并运行 Linux。这意味着，取决于安装在其上的操作系统，同一台 PC 可以是 Windows 2000、Windows XP 或 Linux 系统。

计算机程序建立在操作系统之上。这意味着计算机程序必须利用操作系统包含的功能。例如，计算机程序通过使用操作系统内置的功能来读取和写入文件。（如果操作系统不能煮咖啡，没有程序能命令它这样做并期望得到积极的结果。）

尽管细节有所不同，但大多数操作系统支持许多相似的概念。作为程序员，你需要熟悉以下几个概念：

- 进程是计算机当前正在运行的计算机程序。大多数操作系统允许多个进程同时运行。
- 命令处理器或 shell 是一种特殊程序，允许用户输入命令并执行各种任务，如运行任何程序、查看大量文件或打印文件。在 Windows 2000 或 Windows XP 中，你可以在命令提示符窗口中输入命令。
- “命令行”一词指的是用户输入到命令处理器的命令。通常，命令行包含一个命令和一个或多个选项——命令是该行的第一个单词，其余部分是选项（对计算机特定行为的要求）。
- 环境变量本质上是有名称的文本字符串。例如，PATH 环境变量指向包含目录名称的字符串。操作系统使用环境变量向进程提供有用的信息。若要查看 Windows 2000 或 Windows XP 系统的环境变量列表，请在命令提示符窗口中输入 set。在 Linux 中，你可以输入 printenv 来查看环境变量。

# 计算机编程基础

计算机程序是执行特定任务（如两个数相加或在文件中搜索文本）的指令序列。因此，计算机编程涉及创建该指令列表，并告知计算机如何完成特定任务。具体的指令取决于你使用的编程语言。对于大多数编程语言，你需要按照以下步骤创建计算机程序：

1. 使用文本编辑器输入来自编程语言的命令序列。
   - 该命令序列将完成你的任务。程序的人类可读版本被称为*源文件*或*源代码*。你可以使用任何能够以纯文本形式保存文档的应用程序（如文字处理器）来创建源文件。
   - 始终将源代码保存为纯文本。（文件名取决于编程语言的类型。）文字处理器有时会在文档中嵌入额外指令，指示计算机以特定字体或其他格式显示文本。将文件保存为纯文本会删除所有此类额外指令。相信我，程序在没有这些杂项的情况下表现会更好。
2. 使用*编译器*程序将该文本文件——即源代码——从人类可读形式转换为机器可读的*目标代码*。
   - 通常，此步骤还将多个目标代码文件组合成一个单一的机器可读计算机程序，这是计算机实际可以运行的东西。
3. 使用称为*调试器*的特殊程序来追踪错误并找出源文件中可能导致错误的行。
4. 回到步骤 1，使用文本编辑器修复错误，并重复其余步骤。

这些步骤被称为编程的*编辑-编译-调试循环*，因为大多数程序员必须重复此序列多次，程序才能正确运行。

除了知道基本的编程步骤外，你还需要熟悉以下术语和概念：

- *变量*用于存储不同类型的数据。你可以将每个变量视为数据的占位符——类似于带有一个名称和存储空间来存储数据的邮箱。变量的内容是其值。
- *表达式*通过使用运算符将变量组合在一起。一个表达式可能相加几个变量；另一个表达式可能提取字符串的一部分。

![](img/792720823146d68f19fd50c99ebfce4b_701_0.png)

- *语句*执行某些操作，例如将值赋值给变量或打印字符串。
- *流程控制语句*允许语句以各种顺序执行，具体取决于某个表达式的值。通常，流程控制语句包括 for、do-while、while 和 if-then-else 语句。
- *函数*（也称为子例程或例程）允许你将几个语句分组并给该组命名。此功能允许你通过调用代表这些语句的函数来执行同一组语句。通常，编程语言提供许多预定义函数来执行诸如打开（并读取）文件等任务。

## 探索 Linux 中的软件开发工具

Linux 包含这些传统的 UNIX 软件开发工具：

- 用于编辑源代码的文本编辑器，如 vi 和 emacs。（欲了解 vi 的更多信息，请参阅第二卷，第 5 章。）
- C 编译器，用于编译和链接用 C 编写的程序——C 是编写 UNIX 应用程序的首选编程语言（尽管如今许多程序员转向 C++ 和 Java）。Linux 包含 GNU C 和 C++ 编译器。最初，GNU C 编译器被称为 GCC——现在 GCC 代表 GNU 编译器集合（GNU Compiler Collection）。（参见 http://gcc.gnu.org 上的描述。）
- GNU make 实用工具，用于自动化软件构建过程——即将目标模块组合成可执行文件或库的过程。（操作系统可以加载并运行可执行文件，而库是一组可被可执行文件使用的二进制代码。）
- 用于调试程序的调试器。Linux 包含 GNU 调试器 gdb。
- 版本控制系统，用于跟踪源文件的各种修订版。Linux 附带 RCS（修订控制系统）和 CVS（并发版本系统）。如今，大多数开源项目使用 CVS 作为其版本控制系统，但一个名为 Subversion 的新版本控制系统正在作为 CVS 的替代品进行开发。

你可以在任何 Linux 发行版中安装这些软件开发工具。Xandros 可能已经安装了这些工具。在 Fedora Core 中，在安装期间选择 Development Tools 包。在 Debian 中，在终端窗口中输入 `apt-get install gcc`，然后输入 `apt-get install libc6-dev`。在 SUSE 中，选择主菜单 ⇒ 系统 ⇒ YaST，点击窗口左侧的 Software，然后点击 Install and Remove Software。在 YaST 的搜索框中输入 gcc，从搜索结果中选择相关包，然后点击 Accept 进行安装。如果你发现任何缺少的包，你可以以类似的方式安装它们。

![](img/792720823146d68f19fd50c99ebfce4b_702_0.png)

在接下来的几个部分中，我将简要描述如何使用这些软件开发工具为 Linux 编写应用程序。

## GNU C 和 C++ 编译器

Linux 中最重要的软件开发工具是 GCC——GNU C 和 C++ 编译器。实际上，GCC 可以编译三种语言：C、C++ 和 Objective-C（一种为 C 添加面向对象编程能力的语言）。你使用相同的 `gcc` 命令来编译和链接 C 和 C++ 源文件。GCC 编译器支持 ANSI 标准 C，使得将任何 ANSI C 程序移植到 Linux 变得容易。此外，如果你曾在其他 UNIX 系统上使用过 C 编译器，你应该会对 GCC 感到熟悉。

### 使用 GCC

使用 `gcc` 命令调用 GCC。默认情况下，当你对源文件使用 `gcc` 命令时，GCC 会进行预处理、编译和链接，以创建可执行文件。但是，你可以使用 GCC 选项在此过程的中间阶段停止。例如，你可以使用 `-c` 选项调用 `gcc` 来编译源文件并生成目标文件，而不执行链接步骤。

使用 GCC 编译和链接几个 C 源文件非常简单。假设你想编译和链接一个由两个源文件组成的简单程序。我使用以下程序源代码来完成此任务；它存储在文件 `area.c` 中，是主程序，用于计算通过命令行指定半径的圆的面积：

```c



## 多文件 C 程序示例

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

你需要另一个文件来实际计算圆的面积。以下是文件 `circle.c` 的列表，其中我定义了一个计算圆面积的函数：

```c
#include <math.h>
#define SQUARE(x) ((x)*(x))
double area_of_circle(double r)
{
    return 4.0 * M_PI * SQUARE(r);
}
```

对于如此简单的程序，当然，我可以把所有内容放在一个文件中，但我需要这个人为构造的例子来向你展示如何处理多个文件。

要编译这两个文件并创建一个名为 `area` 的可执行文件，你使用此命令：

```sh
gcc -o area area.c circle.c
```

此 `gcc` 调用使用 `-o` 选项指定可执行文件的名称。（如果你没有使用 `-o` 选项指定输出文件的名称，`gcc` 会将可执行代码保存为名为 `a.out` 的文件。）

如果你有太多源文件需要编译和链接，你可以单独编译这些文件并生成 `object` 文件（扩展名为 `.o`）。这样，当你修改一个源文件时，你只需编译该文件——只需将编译后的文件链接到所有目标文件即可。以下命令展示了如何将示例程序的编译和链接步骤分开：

```sh
gcc -c area.c
gcc -c circle.c
gcc -o area area.o circle.o
```

前两个命令运行 `gcc` 并使用 `-c` 选项编译源文件。第三个 `gcc` 命令将目标文件链接为名为 `area` 的可执行文件。

如果你好奇的话，这里是运行 `area` 程序（计算半径为 1 的圆的面积）的方法：

```sh
./area 1
```

程序生成以下输出：

```
Area of circle with radius 1.000000 = 12.566371
```

顺便一提，只有当当前目录不在 `PATH` 环境变量中时，你才需要给程序名称添加 `./` 前缀。即使你的 `PATH` 中包含当前目录，添加该前缀也无害处。

## 编译 C++ 程序

`GNU CC` 是一个集成的 C 和 C++ 编译器，因此 `gcc` 命令也可以编译 C++ 源文件。`GCC` 根据文件扩展名来确定文件是 C 还是 C++。C 文件使用小写的 `.c` 扩展名，而 C++ 文件则以 `.C` 或 `.cpp` 结尾。

虽然 `gcc` 命令可以编译 C++ 文件，但该命令不会自动链接 C++ 程序通常所需的各类类库。这就是为什么使用 `g++` 命令来编译和链接 C++ 程序很容易，因为它实际上是以适当的选项运行 `gcc`。

假设你要编译存储在名为 `hello.C` 的文件中的以下简单 C++ 程序。（对 C++ 源文件使用大写的 C 扩展名是一种惯例。）

```cpp
#include <iostream>
int main()
{
    using namespace std;
    cout << "Hello from Linux!" << endl;
}
```

要将此程序编译并链接为名为 `hello` 的可执行文件，请使用以下命令：

```bash
g++ -o hello hello.C
```

该命令会创建 `hello` 可执行文件，你可以按如下方式运行它：

```bash
./hello
```

程序显示以下输出：

```
Hello from Linux!
```

大量的 `GCC` 选项控制着 C 和 C++ 程序编译的各个方面的行为。

## 探索 GCC 选项

`gcc` 命令的基本语法如下：

```bash
gcc options filenames
```

每个选项以连字符（`-`）开头，并且通常具有较长的名称，例如 `-funsigned-char` 或 `-finline-functions`。然而，许多常用选项较短，例如 `-c` 表示仅编译，以及 `-g` 表示生成调试信息（使用 GNU 调试器 `gdb` 调试程序时需要这些信息）。

你可以在终端窗口中输入以下命令查看所有 `GCC` 选项的摘要：

```bash
man gcc
```



然后你可以浏览常用的 GCC 选项。通常，你不需要显式提供 GCC 选项，因为默认设置对大多数应用程序都适用。表 1-1 列出了你可能使用的一些 GCC 选项。

### 表 1-1 常用 GCC 选项

| 选项 | 含义 |
| :--- | :--- |
| `-ansi` | 仅支持 ANSI 标准 C 语法。（此选项禁用了某些 GNU C 特有的功能，例如 `__asm__` 和 `__typeof__` 关键字。）与 `g++` 一起使用时，仅支持 ISO 标准 C++。 |
| `-c` | 仅编译并生成目标文件 |
| `-DMACRO` | 定义宏，其值为字符串 "1" |
| `-DMACRO=DEFN` | 将宏定义为 DEFN，其中 DEFN 是某个文本字符串。 |
| `-E` | 仅运行 C 预处理器 |
| `-fallow-single-precision` | 以单精度执行所有数学运算 |
| `-fpcc-struct-return` | 在内存中返回所有结构和联合体值，而不是在寄存器中返回。（以这种方式返回值效率较低，但至少与其他编译器兼容。） |
| `-fPIC` | 生成适合在共享库中使用的可重定位代码（PIC） |
| `-freg-struct-return` | 在可能的情况下，在寄存器中返回结构和联合体值 |
| `-g` | 生成调试信息。（GNU 调试器可以使用此信息。） |
| `-I DIRECTORY` | 在指定目录中搜索通过 `#include` 预处理器指令包含的文件 |
| `-L DIRECTORY` | 在指定目录中搜索库 |
| `-l LIBRARY` | 在链接时搜索指定的库 |
| `-mcpu=cputype` | 针对特定处理器优化代码。cputype 可以取许多不同的值——一些常见的值包括 i386、i486、i586、i686、pentium、pentiumpro、pentium2、pentium3、pentium4。 |
| `-o FILE` | 生成指定的输出文件（用于指定可执行文件的名称） |
| `-O0`（字母 O） | 不进行优化 |
| `-O1` 或 `-O`（字母 O） | 优化生成的代码 |
| `-O2`（字母 O） | 进行更高级别的优化 |
| `-O3`（字母 O） | 执行比 `-O2` 更高级别的优化 |
| `-Os`（字母 O） | 针对大小进行优化（以减少代码总量） |
| `-pedantic` | 如果使用了任何非 ANSI 标准扩展，则生成错误 |
| `-pg` | 向程序中增加额外代码，使其运行时生成 gprof 程序可用于显示程序各部分计时详情的信息 |
| `-shared` | 生成共享对象文件（通常用于创建共享库） |
| `-UNACRO` | 取消定义指定的宏 |
| `-v` | 显示 GCC 的版本号 |
| `-w` | 不生成任何警告消息 |
| `-Wl, OPTION` | 将 OPTION 字符串（包含多个由逗号分隔的选项）传递给链接器。例如，要创建名为 libXXX.so.1 的共享库，请使用以下标志：`-Wl,-soname,libXXX.so.1`。 |

## GNU make 实用程序

当应用程序由多个源文件组成时，手动输入 `gcc` 命令来编译和链接这些文件可能会变得非常繁琐。此外，你也不希望在单个源文件中修改了某些内容时重新编译每个文件。在这种情况下，GNU `make` 实用程序就派上用场了。

`make` 实用程序通过读取和解释 `makefile` 来工作——`makefile` 是一个描述构建特定程序所需的文件以及如何编译和链接这些文件以构建程序的文本文件。每当更改一个或多个文件时，`make` 确定哪些文件需要重新编译——并针对这些文件的编译和程序的重建发出相应的命令。

### Makefile 名称

默认情况下，GNU `make` 会按以下顺序查找具有下列名称之一的 `makefile`：

- `GNUmakefile`
- `makefile`
- `Makefile`

在 UNIX 系统中，使用 `Makefile` 作为 `makefile` 的名称是一种惯例，因为它出现在目录列表的开头附近，大写字母名称会显示在小写字母名称之前。

当你从互联网下载软件时，通常会发现一个 `Makefile`，连同源文件一起提供。要构建软件，你只需在 shell 提示符处输入 `make`，`make` 就会处理构建软件所需的所有步骤。

如果你的 `makefile` 没有使用标准名称（例如 `Makefile`），你必须使用 `make` 的 `-f` 选项来指定 `makefile` 名称。例如，如果你的 `makefile` 名为 `myprogram.mak`，你必须使用以下命令行运行 `make`：

```bash
make -f myprogram.mak
```

### Makefile 文件

对于一个由多个源文件和头文件组成的程序，`makefile` 指定了以下内容：

- `make` 创建的项目——通常是目标文件和可执行文件。使用术语“目标”（target）来指代 `make` 必须创建的任何项目是很常见的。
- 创建目标所需的文件或其他操作。
- 执行哪些命令来创建每个目标。

假设你有一个名为 `form.C` 的 C++ 源文件，其中包含以下预处理器指令：

```cpp
#include "form.h"  // 包含头文件
```

目标文件 `form.o` 显然依赖于源文件 `form.C` 和头文件 `form.h`。除了这些依赖项之外，你还必须指定 `make` 如何将 `form.C` 文件转换为目标文件 `form.o`。假设你希望 `make` 调用 `g++`（因为源文件是 C++ 语言），并使用以下选项：

- `-c`（仅编译）
- `-g`（生成调试信息）
- `-O2`（进行某些优化）

在 `makefile` 中，你可以使用以下规则来表示这些选项：

```makefile
# This is a comment in the makefile

# The following lines indicate how form.o depends
# on form.C and form.h and how to create form.o.
form.o: form.C form.h
	g++ -c -g -O2 form.C
```

在此示例中，第一个非注释行显示 `form.o` 为目标，`form.C` 和 `form.h` 为依赖文件。

![](img/792720823146d68f19fd50c99ebfce4b_709_0.png)

依赖项行之后的行指示如何从其依赖项构建目标。此行必须以制表符开头。否则，`make` 命令将显示错误消息并退出，你会因此感到困惑，因为当你在文本编辑器中查看 `makefile` 时，无法区分制表符和空格。既然你知道其中的奥秘，解决办法是将有问题的那行开头的空格替换为一个制表符。

使用 `make` 的好处在于它能防止不必要的编译。毕竟，你可以从 shell 脚本中运行 `g++`（或 `gcc`）来编译和链接构成你应用程序的所有文件，但 shell 脚本会编译所有内容，即使编译是不必要的。相比之下，`GNU make` 仅在目标的一个或多个依赖项自上次构建目标以来发生了变化时才构建目标。`make` 通过检查目标和依赖项的最后修改时间来验证此变化。

`make` 将目标视为要达到的目标名称；目标不必是文件。你可以拥有如下规则：

```bash
clean:
	rm -f *.o
```

此规则指定了一个名为 `clean` 的抽象目标，它不依赖于任何内容。此依赖项语句表明，要创建目标 `clean`，`GNU make` 将执行命令 `rm -f *.o`，该命令删除所有具有 `.o` 扩展名的文件（即目标文件）。因此，创建名为 `clean` 的目标的净效果是删除目标文件。

### 变量（或宏）

除了从依赖项构建目标的基本功能外，`GNU make` 还包含许多方便的功能，使你能够轻松表达依赖项以及从依赖项构建目标的规则。如果你需要

使用 GCC 和相同的选项编译大量 C++ 文件时，例如为每个文件输入选项，会非常繁琐。你可以通过在 `make` 中定义变量或宏来避免这种重复性任务，如下所示：

```makefile
# 定义编译器名称的宏
CXX= g++

# 定义 GCC 标志的宏
CXXFLAGS= -O2 -g -mcpu=i686

# 用于构建目标文件的规则
form.o: form.C form.h
	$(CXX) -c $(CXXFLAGS) form.C
```



在此示例中，`CXX` 和 `CXXFLAGS` 是 `make` 变量。（GNU `make` 倾向于称它们为变量，但大多数 UNIX `make` 工具称它们为宏。）

要在 `makefile` 的任何位置使用变量，请以美元符号（`$`）开头，后跟括号内的变量名。GNU `make` 会用其定义替换变量的所有出现；因此，它会将 `$(CXXFLAGS)` 的所有出现替换为字符串 `-O2 -g -mcpu=i686`。

GNU `make` 有几个具有特殊含义的预定义变量。表 1-2 列出了这些变量。除了表 1-2 中列出的变量外，GNU `make` 还将所有环境变量（如 `PATH` 和 `HOME`）视为预定义变量。

表 1-2 GNU make 中的一些预定义变量

| 变量 | 含义 |
| :--- | :--- |
| `$%` | 归档目标的成员名称。例如，如果目标是 `libDisp.a (image.o)`，则 `$%` 是 `image.o`。 |
| `$*` | 目标文件的名称（不含扩展名） |
| `$+` | 所有依赖文件的名称（包括重复的依赖项），按出现顺序列出 |
| `$<` | 第一个依赖文件的名称 |
| `$?` | 所有比目标文件新的依赖文件的名称（名称之间用空格分隔） |
| `$@` | 目标的完整名称。例如，如果目标是 `libDisp.a (image.o)`，则 `$@` 是 `libDisp.a` |
| `$^` | 所有依赖文件的名称，名称之间用空格分隔。依赖文件名中的重复项会被去除。 |
| `AR` | 归档维护程序的名称（默认值：`ar`） |
| `ARFLAGS` | 归档维护程序的标志（默认值：`rv`） |
| `AS` | 将汇编语言转换为目标代码的汇编器程序的名称（默认值：`as`） |
| `ASFLAGS` | 汇编器的标志 |
| `CC` | C 编译器的名称（默认值：`cc`） |
| `CFLAGS` | 传递给 C 编译器的标志 |
| `CO` | 从 RCS 提取文件的程序的名称（默认值：`co`） |
| `COFLAGS` | RCS `co` 程序的标志 |
| `CPP` | C 预处理器的名称（默认值：`$(CC) -E`） |
| `CPPFLAGS` | C 预处理器的标志 |
| `CXX` | C++ 编译器的名称（默认值：`g++`） |
| `CXXFLAGS` | 传递给 C++ 编译器的标志 |
| `FC` | FORTRAN 编译器的名称（默认值：`f77`） |
| `FFLAGS` | FORTRAN 编译器的标志 |
| `LDFLAGS` | 当编译器需要调用链接器 `ld` 时的标志 |
| `RM` | 删除文件的命令名称（默认值：`rm -f`） |

# 一个示例 makefile

如果你使用 GNU `make` 的预定义变量及其内置规则，可以很容易地编写一个 `makefile`。例如，考虑一个从三个 C 源文件（`xdraw.c`、`xviewobj.c` 和 `shapes.c`）和两个头文件（`xdraw.h` 和 `shapes.h`）创建可执行文件 `xdraw` 的 `makefile`。假设每个源文件包含其中一个头文件。基于这些事实，一个示例 `makefile` 可能如下所示：

```makefile

###############################################################################

# 示例 makefile

# 注释以 '#' 开头

#

###############################################################################

# 使用标准变量定义编译和链接标志

CFLAGS= -g -O2

# 定义目标 "all"

all: xdraw

OBJECTS=xdraw.o xviewobj.o shapes.o

xdraw: $(OBJECTS)

# 目标文件

xdraw.o: Makefile xdraw.c xdraw.h

xviewobj.o: Makefile xviewobj.c xdraw.h

shapes.o: Makefile shapes.c shapes.h

```

这个 `make`file 依赖于 GNU `make` 的隐式规则。将 `.c` 文件转换为 `.o` 文件使用了内置规则。定义变量 `CFLAGS` 将标志传递给 C 编译器。

![](img/792720823146d68f19fd50c99ebfce4b_712_0.png)

名为 `all` 的目标被定义为第一个目标是有原因的——如果你在命令行中没有指定任何目标就运行 GNU `make`（见下文描述的 `make` 语法），该命令将构建 `make`file 中找到的第一个目标。通过定义第一个目标 `all` 为 `xdraw`，你可以确保 `make` 构建这个可执行文件，即使你没有明确指定它为目标。UNIX 程序员传统上习惯将第一个目标的名称设为 `all`，但目标的名称并不重要；重要的是它是 `make`file 中的第一个目标。

# 如何运行 make

通常，你只需在 shell 提示符下输入以下命令即可运行 `make`：

```
make
```

以这种方式运行时，GNU `make` 会按顺序查找名为 `GNUmakefile`、`makefile` 或 `Makefile` 的文件。如果 `make` 找到其中任何一个 `make`file，它会构建该 `make`file 中指定的第一个目标。然而，如果 `make` 未找到适当的 `make`file，它会显示以下错误消息并退出：

```
make: *** No targets specified and no makefile found.  Stop.
```

如果你的 `make`file 的名称恰好与默认名称不同，你必须使用 `-f` 选项来指定 `make`file。带有此选项的 `make` 命令语法为

```
make -f filename
```

其中 `filename` 是 `make`file 的名称。

即使你有一个默认名称（如 `Makefile`）的 `make`file，你也可能希望构建 `make`file 中定义的多个目标中的特定目标。在这种情况下，你在运行 `make` 时必须使用以下语法：

```
make target
```

例如，如果 `make`file 包含名为 `clean` 的目标，你可以使用此命令构建该目标：

```
make clean
```

另一种特殊语法可以覆盖 `make` 变量的值。例如，GNU `make` 使用 `CFLAGS` 变量来保存编译 C 文件时使用的标志。你可以在调用 `make` 时覆盖此变量的值。以下是如何定义 `CFLAGS` 为选项 `-g -O2` 的示例：

```
make CFLAGS="-g -O2"
```



除了这些选项外，GNU `make` 还接受其他几个命令行选项。表 1-3 列出了 GNU `make` 选项。

**表 1-3 GNU make 选项**

| 选项 | 含义 |
| :--- | :--- |
| `-b` | 忽略但接受，以与其他版本的 make 保持兼容 |
| `-C DIR` | 在读取 makefile 之前更改到指定目录 |
| `-d` | 打印调试信息 |
| `-e` | 允许环境变量覆盖 makefile 中同名变量的定义 |
| `-f FILE` | 读取 FILE 作为 makefile |
| `-h` | 显示 make 选项列表 |
| `-i` | 忽略构建目标时执行的命令中的所有错误 |
| `-I DIR` | 在指定目录中搜索包含的 makefiles。（在 makefile 中包含文件的功能是 GNU make 特有的。） |
| `-j NUM` | 指定 make 可以同时运行的命令数量 |
| `-k` | 即使构建某个目标时发生错误，继续构建无关的目标 |
| `-l LOAD` | 如果平均负载至少为 LOAD（一个浮点数），则不启动新任务 |
| `-m` | 忽略但接受，以与其他版本的 make 保持兼容 |
| `-n` | 打印要执行的命令，但不执行它们 |
| `-o FILE` | 不重建名为 FILE 的文件，即使它比其依赖项旧 |
| `-p` | 显示变量和隐式规则的 make 数据库 |
| `-q` | 不运行任何内容，如果所有目标都是最新的则返回 0（零）；如果需要更新任何内容则返回 1；如果发生错误则返回 2 |
| `-r` | 去除所有内置规则 |
| `-R` | 去除所有内置变量和规则 |
| `-s` | 安静工作（不显示正在执行的命令） |
| `-t` | 更改文件的时间戳 |
| `-v` | 显示 make 的版本号和版权声明 |
| `-w` | 在处理 makefile 前后显示当前工作目录的名称 |
| `-W FILE` | 假设指定文件已修改（与 `-n` 一起使用，以查看如果修改该文件会发生什么）。 |

# GNU 调试器

虽然 `make` 自动化了构建程序的过程，但当程序不正确工作或程序突然因错误消息退出时，编程的这部分并不是你最担心的事情。你需要一个调试器来查找程序错误的原因。Linux 包含 `gdb` —— 具有命令行界面的多功能 GNU 调试器。

像任何调试器一样，`gdb` 允许你执行典型的调试任务，例如：

- 设置断点，使程序在指定行停止
- 监视程序中变量的值
- 逐行执行程序
- 修改变量以尝试修复错误

`gdb` 调试器可以调试 C 和 C++ 程序。

## 准备调试程序

如果你希望使用 `gdb` 调试程序，必须确保编译器生成调试信息并将其放置在可执行文件中。调试信息包含程序中变量的名称以及可执行文件中地址到源文件中代码行的映射。`gdb` 需要这些信息来执行其功能，例如在执行完指定行的源代码后停止。

![](img/792720823146d68f19fd50c99ebfce4b_714_0.png)

为了确保可执行文件已正确准备用于调试，请使用 GCC 的 `-g` 选项。你可以通过在 makefile 中定义变量 `CFLAGS` 来完成此任务：

```
CFLAGS= -g
```

## 运行 gdb

调试程序的最常见方式是使用以下命令运行 `gdb`：

```
gdb progname
```

`progname` 是程序可执行文件的名称。运行后，`gdb` 会显示以下消息并提示输入命令：

```
GNU gdb 6.3

Copyright 2004 Free Software Foundation, Inc.

gdb is free software, covered by the GNU General Public License, and you are welcome to change it and/or distribute copies of it under certain conditions.

Type "show copying" to see the conditions.

There is absolutely no warranty for gdb. Type "show warranty" for details.

This gdb was configured as "i586-suse-linux".

(gdb)
```

你可以在 `**(gdb)**` 提示符下输入 `gdb` 命令。一个非常有用的命令是 `help` —— 它会显示命令列表，如下例所示：

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

`gdb` 拥有大量命令，但你只需要其中几个就能快速找到错误原因。表 1–4 列出了常用的 `gdb` 命令。

### 表 1-4 | 常用 gdb 命令

| 此命令 | 执行以下操作 |
| :--- | :--- |
| `break NUM` | 在指定的行号设置一个*断点*。（调试器会在*断点*处停止。） |
| `bt` | 显示所有堆栈帧的跟踪记录。（此命令显示迄今为止的函数调用序列。） |
| `clear FILENAME:NUM` | 删除源文件中特定行的断点。例如，`clear xdraw.c:8` 清除 xdraw.c 文件第 8 行的断点。 |
| `continue` | 继续运行正在调试的程序。（在程序因信号或断点停止后使用此命令。） |
| `display EXPR` | 每当程序停止时，显示表达式（由程序中定义的变量组成）的值 |
| `file FILE` | 加载指定的可执行文件以进行调试 |
| `help NAME` | 显示名为 NAME 的命令的帮助 |
| `info break` | 显示当前断点列表，包括每个断点被到达的次数信息 |
| `info files` | 显示关于正在调试的文件的详细信息 |
| `info func` | 显示所有函数名称 |
| `info local` | 显示当前函数的局部变量信息 |
| `info prog` | 显示正在调试的程序的执行状态 |
| `info var` | 显示所有全局变量和静态变量的名称 |
| `kill` | 终止你正在调试的程序 |
| `list` | 列出源代码的一个部分 |
| `make` | 运行 make 实用工具以重新构建可执行文件，而不离开 gdb |
| `next` | 在当前函数中前进一行源代码，如果不涉及其他函数，则不进入其他函数 |
| `print EXPR` | 显示表达式 EXPR 的值 |
| `quit` | 退出 gdb |
| `run` | 开始运行当前加载的可执行文件 |
| `set variable VAR=VALUE` | 将变量 VAR 的值设置为 VALUE |
| `shell CMD` | 在不离开 gdb 的情况下执行 UNIX 命令 CMD |
| `step` | 在当前函数中前进一行，如果存在其他函数，则进入这些函数 |
| `watch VAR` | 每当值发生变化时，显示名为 VAR 的变量的值 |
| `where` | 显示调用序列。使用此命令来定位程序崩溃的位置。 |
| `x/F ADDR` | 按照由字母 F 指定的格式检查地址 ADDR 处的内存位置内容，F 可以是 o（八进制）、x（十六进制）、d（十进制）、u（无符号十进制）、t（二进制）、f（浮点）、a（地址）、i（指令）、c（字符）或 s（字符串）。你可以在格式字母后附加表示数据类型大小的字母。大小字母包括 b（字节）、h（半字，2 字节）、w（字，4 字节）和 g（巨型，8 字节）。通常，ADDR 是变量或指针的名称。 |

# 第八卷

# 第一章

# 在 Linux 中编程

## 使用 gdb 查找 bug

为了理解如何使用 gdb 查找 bug，你需要查看一个示例。使用简单的示例最容易说明这一过程，因此我以一个包含典型 bug 的人造程序开始。

以下是该人造程序，我将其存储在文件 `dbgstst.c` 中：

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

此程序的 `main` 函数调用 `read_input` 函数以获取用户输入的一行内容。`read_input` 函数期望一个字符数组，并返回用户输入的内容。然而，在此示例中，`main` 调用 `read_input` 时传入的是一个未初始化的指针——这就是这个简单程序中的 bug。

使用 `gcc` 和 `-g` 选项构建程序：

```bash
gcc -g -o dbgstst dbgstst.c
```

忽略关于 `gets` 函数具有危险性的警告消息；我试图利用该函数的缺陷来展示如何使用 `gdb` 追踪错误。

要查看此程序的问题，请运行它并在 Command: 提示符处输入 test：

```bash
./dbgstst
Command: test
Segmentation fault
```

程序在显示 Segmentation fault 消息后崩溃。对于像这样的小程序，你很可能通过检查源代码就能找到原因。但在实际应用中，你可能无法立即知道导致错误的原因。这时你必须使用 `gdb` 来找到问题的根源。

要使用 `gdb` 定位 bug，请遵循以下步骤：

1. **在 `gdb` 中加载程序。** 要在 `gdb` 中加载名为 `dbgstd` 的程序，输入以下内容：

```bash
(gdb) dbgstd
```

2. **通过输入 `run` 命令在 `gdb` 下开始执行程序。当程序提示输入时，输入一些文本。**

程序像之前一样失败。以下是 `dbgstd` 程序发生的情况：

```bash
(gdb) run
Starting program: /home/naba/sdewd/dbgstd
Command: test
Program received signal SIGSEGV, Segmentation fault.
0x400802b6 in gets () from /lib/its/libc.so.6
(gdb)
```

3. **使用 `where` 命令确定程序在哪里崩溃。** 对于 `dbgstd` 程序，此命令产生以下输出：

```bash
(gdb) where
#0 0x400802b6 in gets () from /lib/its/libc.so.6
#1 0x08048474 in read_input (s=0x0) at dbgstd.c:16
#2 0x08048436 in main () at dbgstd.c:7
(gdb)
```

输出显示了函数调用序列。函数调用 #0 —— 最近的一次调用 —— 是调用 C 库函数 `gets`。`gets` 调用源自 `read_input` 函数（在文件 `dbgstd.c` 的第 16 行），而后者又是在 `dbgstd.c` 文件的第 7 行由 `main` 函数调用的。

4. **使用 `list` 命令检查可疑源代码的行。** 在 `dbgstd` 中，你可以从 `dbgstd.c` 文件的第 16 行开始，如下所示：

```bash
(gdb) list dbgstd.c:16
11      return 0;
12      }
13      void read_input(char *s)
14      {
15        printf("Command: ");
16        gets(s);
17      }
18
(gdb)
```

查看此列表后，你可以判断问题可能在于调用 `read_input` 的方式。然后，你列出 `dbgst.c` 中第 7 行附近的代码（`read_input` 调用源）：

```bash
(gdb) list dbgst.c:7
2    static char buf[256];
3    void read_input(char *s);
4    int main(void)
5    {
6    char *input = NULL; /* Just a pointer, no storage for string */
7    read_input(input);
8    /* Process command. */
9    printf("You typed: %s\n", input);
10    /* ... */
11    return 0;
(gdb)
```

此时，你可以将问题缩小到名为 `input` 的变量。该变量是一个数组，而不是一个 `NULL`（即零）指针。

## 在 gdb 中修复 bug

有时你可以直接在 `gdb` 中修复 bug。对于前一部分中的示例程序，你可以尝试在程序显示错误消息后崩溃立即进行以下修复。由于该示例是人造的，我在 `dbgst` 程序中定义了一个额外的名为 `buf` 的缓冲区，如下所示：

```c
static char buf[256];
```



我可以通过将变量 `input` 设置为 `buf` 来修复未初始化指针的问题。以下 `gdb` 会话解决了未初始化指针的问题。（此示例从程序运行并因段错误而崩溃后的位置开始。）

```bash
(gdb) file dbgst

A program is being debugged already.  Kill it? (y or n) y

Load new symbol table from "/home/naba/sw/dbgst"? (y or n) y

Reading symbols from /home/naba/sw/dbgst...done.

(gdb) list

1    #include <stdio.h>

2    static char buf[256];

3    void read_input(char *s);

4    int main(void)

5    {

6    char *input = NULL; /* Just a pointer, no storage for string */

7    read_input(input);

8    /* Process command. */
```

```cpp
9              printf("You typed: %s\n", input);
10           /* ... */
(gdb) break 7

Breakpoint 2 at 0x804842b: file dbgdst.c, line 7.

(gdb) run

Starting program:  /home/naba/sw/dbgtest

Breakpoint 1, main () at dbgdst.c:7

7              read_input(input);

(gdb) set var input=buf

(gdb) cont

Continuing.

Command: test

You typed: test

Program exited normally.

(gdb)q
```

如前一个列表所示，如果我停止程序，使其刚好在调用 `read_input` 之前停止，并将名为 `input` 的变量设置为 `buf`（这是一个有效的字符数组），那么程序的其余部分可以正常运行。

在 `gdb` 中找到一种可行的修复方法后，你可以对源文件进行必要的更改，使该修复成为永久性。

## 理解 GNU 许可证的含义

你不得不为 Linux 的丰富资源付出代价——为了保护其开发者和用户，Linux 在 GNU GPL（通用公共许可证）下分发，该许可证规定了源代码的分发方式。

然而，GPL 并不意味着你不能为 Linux 编写想要以二进制形式分发（无论是免费还是收费）的商业软件。你可以遵守所有规则，并以二进制形式销售你的 Linux 应用程序。

在编写 Linux 应用程序时，请注意以下两种许可证：

- GNU 通用公共许可证（GPL），它管理着许多 Linux 程序，包括 Linux 内核和 GCC。
- GNU 库通用公共许可证（LGPL），它涵盖了众多 Linux 库。

以下章节概述了这些许可证，并提供了一些关于如何满足其要求的建议。但是，由于我不是律师，请勿将本书中的任何内容视为法律建议。这些许可证的全文位于你的 Linux 系统中的文本文件中；将这些许可证展示给你的法律顾问，以获得完整的解释以及对其业务适用性的评估。

![](img/792720823146d68f19fd50c99ebfce4b_720_0.png)

### GNU 通用公共许可证

GNU 通用公共许可证（GPL）的文本位于你 Linux 系统各目录中名为 `COPYING` 的文件中。例如，键入以下命令可以在你的 Linux 系统中找到该文件的一个副本：

```bash
find /usr -name "COPYING" -print
```

找到该文件后，你可以转到该目录并键入 `more COPYING` 来阅读 GPL。如果你找不到 `COPYING` 文件，只需翻阅本书的末尾来阅读 GPL。

GPL 与你是否对软件收费或免费分发无关；其核心在于确保软件对所有用户保持免费。GPL 要求软件以源代码形式分发，并规定任何用户都可以复制软件并以源代码形式分发给其他人。此外，它还提醒所有人，该软件完全没有任何保证。

GPL 涵盖的软件不属于公有领域。受 GPL 保护的软件始终受版权保护，且 GPL 明确规定了对软件复制和分发的限制。当然，从用户的角度来看，GPL 的限制并非真正的限制；这些限制实际上是利益，因为用户被保证可以访问源代码。

如果你的应用程序使用了 GPL 涵盖的任何软件的部分，那么你的应用程序被视为*衍生作品*，这意味着你的应用程序也受 GPL 保护，且你必须分发你应用程序的源代码。

![](img/792720823146d68f19fd50c99ebfce4b_721_0.png)

虽然 GPL 涵盖 Linux 内核，但 GPL 并不涵盖那些通过系统调用使用内核服务的应用程序。这些应用程序被视为对内核的正常用途。

如果你计划以二进制形式分发你的应用程序（大多数商业软件都是这样分发的），你必须确保你的应用程序没有使用 GPL 涵盖的任何软件的部分。当你的应用程序调用库中的函数时，它可能会最终使用其他软件的部分。然而，大多数库都受另一种 GNU 许可证的保护，我将在下一节中描述该许可证。

你只需要留意 GPL 涵盖的少数几个库和实用程序。GNU `dbm`（`gdbm`）数据库库是 GPL 涵盖的著名库之一。GNU `bison` 解析器生成工具是另一个 GPL 涵盖的实用程序。如果你允许 `bison` 生成代码，GPL 将涵盖该代码。

![](img/792720823146d68f19fd50c99ebfce4b_722_0.png)

GNU dbm 和 GNU bison 的其他替代方案不受 GPL 保护。对于数据库库，你可以使用 Berkeley 数据库库 `db` 来替代 `gdbm`。对于解析器生成工具，你可以使用 `yacc` 来替代 `bison`。

### GNU 库通用公共许可证

GNU 库通用公共许可证（LGPL）的文本位于名为 `COPYING.LIB` 的文件中。如果你安装了内核源代码，那么 `COPYING.LIB` 文件的一个副本位于其中一个源目录中。要在你的 Linux 系统中定位 `COPYING.LIB` 文件的一个副本，请在终端窗口中键入以下命令：

```
find /usr -name "COPYING*" -print
```



此命令列出你系统中所有出现的 `COPYING` 和 `COPYING.LIB`。`COPYING` 文件包含 `GPL`，而 `COPYING.LIB` 包含 `LGPL`。

`LGPL` 旨在允许在你的应用程序中使用库，即使你不分发你应用程序的源代码。然而，`LGPL` 规定用户必须能够访问你所使用的库的源代码，并且用户可以利用这些库的修改版本。

`LGPL` 涵盖了大多数 Linux 库，包括 C 库 `libc.a`。因此，当你使用 `GCC` 编译器在 Linux 上构建应用程序时，你的应用程序将与 `LGPL` 涵盖的一个或多个库的代码进行链接。如果你想仅以二进制形式分发你的应用程序，你需要注意 `LGPL`。

![](img/792720823146d68f19fd50c99ebfce4b_722_1.png)

满足 `LGPL` 意图的一种方式是为你的应用程序提供目标代码，以及一个将你的目标文件与 `LGPL` 涵盖的任何更新 Linux 库进行链接的 `makefile`。

![](img/792720823146d68f19fd50c99ebfce4b_722_2.png)

满足 `LGPL` 的更好方式是使用动态链接，在这种链接中，你的应用程序和库是独立的实体，尽管你的应用程序在运行时调用库中的函数。通过动态链接，用户可以立即获得库更新的利益，而无需重新链接应用程序。

698 *第八册：编程*

# 第 2 章：C 语言编程

## 本章内容

- 理解 C 语言编程的基础知识
- 发现 C 编程语言的特性
- 盘点标准 C 库
- 在 Linux 应用程序中使用共享库

C 编程语言的结构——一个稀疏的核心加上一个庞大的支持库——使其成为开发软件的理想语言。核心提供了一组良好的数据类型和控制结构，而所有附加任务，包括输入和输出（I/O）、数学计算以及对外围设备的访问，都被留给函数库。基本上，C 允许你访问系统中的任何你想访问的内容。这意味着你可以用 C 编写从设备驱动程序到图形应用程序的任何东西。在本章中，我将向你介绍 C 语言编程。我还会简要解释共享库的重要性，以及如何在使用 C 编程语言的情况下在 Linux 中创建一个共享库。

### C 程序的结构

典型的 C 程序组织在一个或多个源文件（或模块）中。（参见图 2-1。）每个文件具有相似的结构，包括注释、预处理器指令、变量和函数的声明，以及它们的定义。你通常将每组相关的变量和函数放在单个源文件中。

一些文件仅仅是一组声明，通过 C 预处理器的 `#include` 指令在其他文件中使用。这些文件通常被称为头文件，其名称以 `.h` 扩展名结尾。在图 2-1 中，文件 `shapes.h` 是一个头文件，它声明了程序中通用的数据结构和函数。另一个文件，`shapes.c`，定义了函数。第三个文件，`shapetest.c`，实现了 `main` 函数——C 程序的执行从该函数开始。这些以 `.c` 结尾的文件是源文件，你在那里定义程序所需的函数。虽然图 2-1 只显示每个源文件中的一个函数，但在典型的程序中，一个源文件中通常包含许多函数。

![](img/792720823146d68f19fd50c99ebfce4b_725_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_725_1.png)

![](img/792720823146d68f19fd50c99ebfce4b_725_2.png)

**图 2-1：**
通常，一个 C 程序由几个源文件组成。

## 声明与定义

*声明* 决定了程序如何解释一个符号。另一方面，*定义* 实际上是创建变量或函数。定义会让编译器为数据或代码预留存储空间，但声明不会。例如，

```c
int x, y, z;
```

这是三个不同整型变量的定义，但

```c
extern int x, y, z;
```

这是一个声明，表明这三个整型变量在另一个源文件中定义。

要创建一个可执行程序，你必须编译和链接源文件。从 C 源文件构建程序的具体步骤取决于编译器和操作系统。例如，在 Linux 中，你可以使用以下命令编译和链接图 2-1 中显示的文件：

```bash
gcc -o shapetest shapetest.c shapes.c
```

此命令创建了一个名为 `shapetest` 的可执行文件。然后你可以使用以下命令运行该文件：

```bash
./shapetest
```

这里是程序显示的输出：

```text
Area of circle = 7853.981634
```

在每个源文件中，程序的组件以标准方式排列。正如图 2-1 中所示的文件一样，C 源文件的典型组件在屏幕上向下滚动时遵循某种顺序：

- 1. 文件以一些注释开头，描述模块的目的并提供其他相关信息，例如作者姓名和修订日期。在 C 中，注释以 `/*` 开始，以 `*/` 结束。
- 2. 预处理器命令，即预处理指令，跟随在注释之后。最初几个指令通常用于包含头文件和定义常量。
- 3. 接下来是在整个文件中可见的变量和函数的声明。换句话说，这些变量和函数的名称可以在该文件中的任何函数中使用。在这里，你也定义在该文件内所需的变量。
- 4. 文件的其余部分包括函数的定义。在函数体内部，你可以定义仅在该函数代码执行期间存在的局部变量。

## 预处理指令

预处理是指将或编译 C 文件为机器指令的第一步。预处理器处理源文件并作用于嵌入程序中的某些命令（称为预处理指令）。这些指令以井号 (`#`) 开头，后跟一个关键字。通常，编译器在开始编译之前会自动调用预处理器，但大多数编译器都提供单独调用预处理器的选项。你可以利用预处理器的三大主要功能来使你的程序更模块化、更易读且更容易定制：

- 你可以使用 `#include` 指令将文件内容插入到你的程序中。通过此指令，你可以将通用声明放在一个位置，并通过文件包含在所有源文件中使用它们。结果是减少了不同程序模块中变量和函数声明之间不匹配的风险。
- 通过 `#define` 指令，你可以定义宏，使你能用一个字符串替换另一个字符串。你可以使用 `#define` 指令为数值常量提供有意义的名称，从而改善源文件的可读性。
- 使用诸如 `#if`、`#ifndef`、`#else` 和 `#endif` 之类的指令，你可以只编译程序的部分选定部分。你可以利用此功能编写适用于两个或多个系统的源代码文件，但只编译适用于你编译程序的计算机系统的那些部分。通过这种策略，你可以使用一组源文件维护程序的多个版本。

### 包含文件

你可以通过利用 `#include` 指令编写模块化程序。之所以有此指令，是因为 C 预处理器允许你将常用的声明保存在单个文件中，并可根据需要将其插入其他源文件中。ANSI C 支持三种 *include* 指令形式。作为 C 程序员，你需要熟悉前两种形式：

```c
#include <stdio.h>
#include "shapes.h"
```

你使用 *`#include`* 的第一种形式来读取文件内容——在本例中，是所有头文件所在的默认位置中的标准 C 头文件 `stdio.h`。当文件（例如 `shapes.h`）位于当前目录时，将文件名放在双引号内。定位包含文件的确切约定取决于编译器。

### 定义宏

*宏* 本质上是一个可重用的 C 代码块的简短名称。代码可以简单如一个数值常量，也可以复杂如许多行详细的 C 代码。其思想是，定义宏之后，你可以在程序中任何需要使用该代码的地方使用该宏。当源文件经过预处理时，宏名称的每个出现位置都会被其定义替换。

宏的常见用途是为数值常量定义符号名称，然后在程序中使用该符号代替数字。宏提高了源代码的可读性；有了描述性名称，你不必猜测程序中为何使用某个特定数字。你可以使用 `#define` 指令以直接的方式定义这样的宏。以下是一些示例：

```c
#define PI 3.14159
#define GRAV_ACC 9.80665
#define BUFSIZE 512
```

定义这些符号后，你可以在整个源文件中使用 `PI`、`GRAV_ACC` 和 `BUFSIZE` 代替数值常量。

然而，宏所能做的远不止简单地将符号替换为常量或某段代码。宏可以接受一个参数，并在程序中使用宏时将该参数的每次出现替换为提供的值。因此，宏展开后的代码结果可能会根据运行宏时使用的参数而改变。例如，这里有一个接受参数并展开为旨在计算参数平方的表达式的宏：

```c
#define square(x) ((x) * (x))
```



如果你在程序中使用 `square(z)` *，在经过预处理的源文件中，它变成 `((z) * (z))`。实际上，这个宏等同于一个计算其参数平方的函数——除了你不调用函数。相反，宏生成的表达式直接放置在源文件中。

### 条件指令

你可以使用条件指令，如 `#if`、`#ifdef`、`#ifndef`、`#else`、`#elif` 和 `#endif`，来控制源文件的哪些部分被编译以及编译的条件。利用此功能，你可以维护一组源文件，这组文件可以用不同的编译器在不同的环境中选择性地编译。（另一个常见用途是插入仅在定义了名为 `DEBUG` 的符号时才会被编译的 `#print` 语句用于调试。）条件指令以 `#if`、`#ifdef` 或 `#ifndef` 开头——并且可能跟随任意数量的 `#elif` 指令（或根本没有）。接下来是一个可选的 `#else`，随后是标记该条件块结束的 `#endif` 指令。以下是使用条件指令的一些常见方法。

为了只包含一次头文件，你可以使用以下代码：

```c
#ifndef __PROJECT_H
#define __PROJECT_H
/* Declarations to be included once */
/* ... */
#endif
```

以下代码在调试期间（当定义了 `DEBUG` 符号时）打印诊断消息：

```c
#ifdef DEBUG
    printf("In read_file: bytes_read = %d\n", bytes_read);
#endif
```

以下示例展示了如何根据正在编译程序的计算机系统类型包含不同的头文件。为了选择性地包含头文件，你可以使用以下代码：

```c
#if CPU_TYPE == i386
    #include <i386/sysdef.h>
#elif CPU_TYPE == M68K
    #include <m68k/sysdef.h>
#else
    #error Unknown CPU type.
#endif
```

`#error` 指令用于在预处理期间显示错误消息。

### 其他指令

其他几个预处理指令执行杂项任务。例如，你可以使用 `#undef` 指令移除符号的当前定义。`#pragma` 指令是另一种特殊用途指令，你可以用它向 C 编译器传达信息。你可以使用 pragma 访问编译器的特殊功能——这些功能因编译器而异。

C 编译器提供几个预定义宏（见表 2-1）。在这些宏中，宏 `__FILE__` 和 `__LINE__` 分别指当前正在处理的源文件名和当前行号。你可以使用 `#line` 指令更改这些。例如，要将 `__FILE__` 设置为 `"file_io.c"` 并将 `__LINE__` 设置为 `100`，你可以说：

```c
#line 100 "file_io.c"
```

表 2-1 C 中的预定义宏

| 宏 | 定义 |
|---|---|
| `__DATE__` | 该字符串包含调用 C 编译器时的日期。其格式为 MMM DD YYYY（例如，Oct 26 2004）。 |
| `__FILE__` | 该宏展开为包含源文件名称的字符串。 |
| `__LINE__` | 该宏是一个十进制整数，其值等于当前源文件内的行号。 |

## 宏和预定义定义

| 宏 | 定义 |
|---|---|
| `__STDC__` | 此宏扩展为十进制常数 1，以表明 C 编译器符合 ANSI 标准。 |
| `__TIME__` | 此字符串显示开始编译源文件的时间。其格式为 `HH:MM:SS`（例如，`21:59:45`）。 |

## 变量的声明与定义

在 C 语言中，您必须在所有变量和函数使用前对其进行定义或声明。变量的定义规定了以下三件事：

- 其*可见性*，指示变量确切的使用位置。（它是为程序中的所有文件、当前文件，还是仅在某个函数中定义的？）
- 其*生命周期*，决定变量是临时存在（例如，函数中的局部变量）还是永久存在（只要程序在运行）。
- 其*类型*（在某些情况下，还包括其*初始值*）。例如，初始化为 1 的整型变量 *x* 定义如下：

```c
int x = 1;
```

如果您使用的是在另一个源文件中定义的变量，您需要使用 *extern* 关键字来声明该变量，如下所示：

```c
extern int message_count;
```

您必须在至少一个源文件中定义此变量，且不带 *extern* 限定符。当构建程序时，链接器将解析对 *message_count* 变量的所有引用，并确保它们都使用同一个变量。

## 基本数据类型

C 语言有四种基本数据类型：*char* 和 *int* 用于存储字符和整数，*float* 和 *double* 用于存储浮点数。您可以以直接的方式定义这些基本数据类型的变量：

```c
char c;
int i, j, bufsize;
float volts;
double mean, variance;
```

您可以使用 *long*、*short* 和 *unsigned* 限定符作为前缀，将基本数据类型扩展为更大的集合。*long* 和 *short* 限定符是大小修饰符。例如，*long int* 至少为 4 字节长，而 *short* int 的最小大小仅为 2 字节。*int* 的大小取决于系统，但它肯定比 *short* 大。

*unsigned* 限定符仅用于 *int* 和 *char* 类型。通常，这些类型中的每一种既持有负值也持有正值。此限定符是这些数据类型的默认有符号形式。当您希望变量仅持有正值时，可以使用 *unsigned* 限定符。以下是使用 *short, long* 和 *unsigned* 限定符的一些示例：

```c
unsigned char mode_select, printer_status;
short     record_number;        /* 等同于 'short int' */
long      offset;               /* 等同于 'long int' */
unsigned  i, j, msg_id;        /* 等同于 'unsigned int' */
unsigned short width, height;   /* 等同于 'unsigned short int' */
unsigned long file_pos;         /* 等同于 'unsigned long int' */
long double result;
```

当 *short, long* 和 *unsigned* 限定符与 *int* 类型一起使用时，您可以从声明中省略 *int*。您还可以使用 *long* 前缀扩展 *double* 数据类型。

![](img/792720823146d68f19fd50c99ebfce4b_731_0.png)

`GCC` 附带了预定义头文件 --- *limits.h* 和 *float.h* ---，在这些头文件中定义了各种数据类型的精确大小 --- 以及数值范围 ---。您可以在 Linux 系统的 `/usr/include` 目录中查看这些文件，以确定 `GCC` 编译器支持的基本数据类型的大小。

### 枚举

您可以使用 *enum* 数据类型定义自己的枚举列表 --- 一组固定的命名整数常量。例如，您可以按以下方式使用 *enum* 声明名为 *BOOLEAN* 的布尔数据类型：

```c
/* 声明一个名为 BOOLEAN 的枚举类型 */
enum BOOLEAN {false = 0, true = 1, stop = 0, go = 1,
              off = 0, on = 1};
/* 定义一个名为 "status" 的 BOOLEAN 并初始化它 */
enum BOOLEAN status = stop;
```

此示例首先将 *BOOLEAN* 声明为枚举类型。花括号内的列表显示了 *enum* *BOOLEAN* 变量的有效值的枚举常量。您可以将每个常量初始化为您选择的值，并且多个常量可以使用相同的值。在此示例中，常量 *false, stop* 和 *off* 被设置为 0，而 *true, go* 和 *on* 被初始化为 1。该示例然后定义了一个名为 *status* 的枚举 *BOOLEAN* 变量，其初始值设置为常量 *stop*。

## 结构体、联合体和位域

使用 `struct` 将相关的数据项组合在一起，并通过名称引用该组。例如，定义一个用于保存队列变量的结构体的声明可能如下所示：

```c
/* 声明一个结构体 */
struct QUEUE
{
    int count;    /* 队列中的项目数量     */
    int front;    /* 队列中第一个项目的索引   */
    int rear;     /* 队列中最后一个项目的索引    */
    int elemsize; /* 每个数据元素的大小   */
```



```c
int maxsize;  /* 队列的最大容量      */

char *data;   /* 指向队列数据的指针       */

};
```

/* 定义两个队列 */

```c
struct QUEUE rcv_q, xmit_q;
```

`QUEUE`结构体内部的元素被称为其*成员*。您可以使用成员选择运算符（`.`）来访问这些成员。例如，`rcv_q.count`指的是`rcv_q`结构体的`count`成员。

联合体类似于结构体，但与其将相关数据项组合在一起（如结构体所做的那样）不同，联合体为从同一位置开始的多个数据项分配存储空间。因此，联合体的所有成员共享同一存储空间。您可以使用联合体以不同方式查看同一数据项。假设您使用支持4字节长整数的编译器，并且想要访问单个长整数的4个单独字节。这是一个可以实现该目的的联合体：

```c
union

{
    long file_type;
    char bytes[4];
} header_id;
```

使用此定义，`header_id.file_type`指的是长整数，而`header_id.bytes[0]`是该长整数的第一个字节。

## 数组

*数组*是一组一个或多个相同的数据项的集合。您可以声明任何数据类型的数组，包括结构体和由`typedef`定义的类型。例如，要定义一个80个字符的数组，您编写如下代码：

```c
char string[80];
```

字符串数组中的字符占据连续的存储位置，从位置0开始。因此，在此示例中，`string[0]`指的是该数组中的第一个字符，而`string[79]`指的是最后一个。您可以类似地定义其他数据类型和结构的数组：

```c
struct Customer        /* 声明一个结构体        */
{
    int id;
    char first_name[40];
    char last_name[40];
};
struct Customer customers[100]; /* 定义结构体数组 */
int                   index[64]; /* 包含 64 个整数的数组 */
```

您还可以定义多维数组。例如，为了表示一个80列乘以25行的文本显示屏幕，您可以使用二维数组如下：

```c
unsigned char text_screen[25][80];
```

`text_screen`的每个项目都是80个`unsigned`字符的数组，并且`text_screen`包含25个这样的数组。换句话说，二维数组是通过在内存中一行接一行地排列来存储的。您可以使用诸如`text_screen[0][0]`这样的表达式来引用第一行的第一个字符，使用`text_screen[24][79]`来引用显示屏幕最后一行的最后一个字符。更高维的数组定义方式类似：

```c
float   coords[3][2][5];
```

此示例将`coords`定义为三个数据项的三维数组：每个项目都是两个数组的数组，而每个数组又都是五个`float`变量的数组。因此，您将多维数组解释为*数组的数组*。

## 指针

*指针*是一种可以保存除位域外任何类型数据地址的变量。例如，如果`p_i`是指向整数变量的指针，您可以如下定义和使用它：

```c
/* 定义一个 int 指针和一个整数 */
int  *p_i, count;
/* 将指针设置为整数 "count" 的地址 */
p_i = &count;
```

在这种情况下，编译器为`int`变量`count`和指向整数的指针`p_i`分配存储空间。表示指针所需的字节数取决于底层系统的寻址方案。

![](img/792720823146d68f19fd50c99ebfce4b_734_0.png)

在使用指针之前，请确保它包含一个有效对象的地址。

示例展示了使用`&`运算符将`p_i`初始化为整型变量`count`的地址，该运算符向C语言提供了变量的地址。在`p_i`初始化之后，你可以使用表达式`*p_i`来访问`count`的值，该表达式读作“地址存储在`p_i`中的对象的内容”。

指针在许多情况下非常有用；其中一个重要场景是动态内存分配。标准C库包含诸如`malloc`和`calloc`等函数，你可以调用这些函数为对象数组分配存储空间。分配内存后，这些函数返回内存块的起始地址。由于该地址是访问该内存的唯一途径，你必须将其存储在一个能够持有地址的变量中——即指针。

假设你为包含50个整数的数组分配了内存，并将返回的地址保存在`p_i`中。现在，你可以将这块内存视为一个名为`p_i`的包含50个整数的数组。因此，你可以将数组中的最后一个元素表示为`p_i[49]`，这等价于`*(p_i+49)`。同样，C语言将数组的名称视为指向数组第一个元素的指针。数组名称和指针变量之间的区别在于，数组的名称是一个常量，不需要显式的存储空间来持有数组第一个元素的地址。而指针则是一个实际存储位置，能够持有任意数据的地址。

除了存储动态分配内存的地址外，指针还常用作函数的参数。当调用C函数时，其所有参数都是按值传递的——也就是说，函数获得的是每个参数的副本，而不是函数调用参数列表中出现的那些原始变量。因此，C函数无法改变其参数的值。指针提供了一种解决方案。要在函数中改变某个变量的值，你可以传递指向该变量的指针；函数随后可以通过指针来改变该值。

### 类型定义

通过`typedef`关键字，C语言为您提供了一种将新名称分配给现有数据类型的便捷方式。你可以使用`typedef`设施为特定应用程序中使用的数据类型赋予有意义的名称。例如，图形应用程序可能会声明一个名为`Point`的数据类型，如下所示：

```c
/* Declare a Point data type */
typedef struct Point
{
      short x;
      short y;
} Point;
```

第八卷
第二章
C语言编程

```c
/* Declare PointPtr to be pointer to Point types */
typedef Point *PointPtr;
/* Define some instances of these types */
/* and initialize them */
Point a = {0, 0};
PointPtr p_a = &a;
```

如`Point`和`PointPtr`类型所示，你可以使用`typedef`方便地声明复杂的数据类型。

## 类型限定符：const 和 volatile

两个类型限定符`const`和`volatile`在声明中的工作方式如下：

- **const**限定符告诉编译器，程序必须不修改特定的数据对象。编译器不得生成可能改变该数据项存储位置内容的代码。
- **volatile**限定符指定超出程序控制范围的因素可能会改变变量的值。

你可以在单个数据项上同时使用`const`和`volatile`关键字，这意味着虽然你的程序不得修改该项，但其他进程可能会改变它。`const`和`volatile`关键字总是修饰紧随其后的项（右侧）。`const`和`volatile`限定符提供的信息旨在帮助编译器优化生成的代码。例如，假设变量`block_size`按以下方式声明和初始化：

```c
const int block_size = 512;
```

在这种情况下，编译器不需要生成从内存加载`block_size`值的代码。相反，它可以在程序使用`block_size`的任何地方直接使用该值512。现在，假设你在声明中添加了`volatile`并将声明更改为：

```c
volatile const int block_size = 512;
```

此声明表示某个外部进程可以更改`block_size`的内容。因此，编译器不能优化掉对`block_size`的任何引用。当引用I/O端口或视频内存时，你可能需要使用此类声明，因为这些位置可能会受超出程序控制范围的因素影响而改变。

## 表达式

*表达式*是变量、函数调用和运算符的组合，其结果是单个值。例如，下面是一个表达式，其值为存储*以null结尾的字符串`str`*所需 的字节数（即*char*数据类型的*数组*，末尾带有一个零字节）：

```c
(strlen(str) * sizeof(char) + 1)
```



此表达式涉及函数调用——`strlen(str)`——以及 `乘法`（`*`）、`加法`（`+`）和 `sizeof` 运算符。

C 语言拥有大量运算符，它们是表达式的重要组成部分。表 2-2 提供了 C 语言运算符的摘要。

**表 2-2 C 运算符摘要**

| 运算符名称 | 语法 | 结果 |
| :--- | :--- | :--- |
| **算术运算符** | | |
| 加法 | x+y | 将 x 和 y 相加 |
| 减法 | x-y | 从 x 中减去 y |
| 乘法 | x*y | 将 x 和 y 相乘 |
| 除法 | x/y | 将 x 除以 y |
| 取余 | x%y | 计算 x 除以 y 的余数 |
| 前置递增 | ++x | 在使用 x 之前将其递增 |
| 后置递增 | x++ | 在使用 x 之后将其递增 |
| 前置递减 | --x | 在使用 x 之前将其递减 |
| 后置递减 | x-- | 在使用 x 之后将其递减 |
| 负号 | -x | 取 x 值的负数 |
| 正号 | +x | 保持 x 的值不变 |
| **关系和逻辑运算符** | | |
| 大于 | x>y | 如果 x 大于 y，则值为 1；否则，值为 0。 |
| 大于或等于 | x>=y | 如果 x 大于或等于 y，则值为 1；否则，值为 0。 |
| 小于 | x<y | 如果 y 大于 x，则值为 1；否则，值为 0。 |
| 小于或等于 | x<=y | 如果 y 大于或等于 x，则值为 1；否则，值为 0。 |
| 等于 | x==y | 如果 x 等于 y，则值为 1；否则，值为 0。 |
| 不等于 | x!=y | 如果 x 和 y 不相等，则值为 1；否则，值为 0。 |
| 逻辑非 | !x | 如果 x 为 0，则值为 1；否则，值为 0。 |
| 逻辑与 | x&&y | 如果 x 或 y 中有一个为 0，则值为 0。 |
| 逻辑或 | x\|\|y | 如果 x 和 y 都为 0，则值为 0。 |
| **赋值运算符** | | |
| 赋值 | x=y | 将 y 的值放入 x 中 |
| 复合赋值 | x op=y | 等同于 x=x op y，其中 op 是以下运算符之一：+, -, *, /, %, <<, >>, &, ^, 或 \| |
| **数据访问和大小运算符** | | |
| 下标 | x[y] | 选择数组 x 的第 y 个元素 |
| 成员选择 | x.y | 选择结构体（或联合体）x 的成员 y |
| 成员选择 | x->y | 从以 x 为地址的结构体或联合体中选择名为 y 的成员 |
| 间接访问 | *x | 以 x 为地址的位置的内容 |
| 取地址 | &x | 名为 x 的数据对象的地址 |
| 大小 | sizeof(x) | 名为 x 的数据对象的大小（以字节为单位） |
| **按位运算符** | | |
| 按位非 | ~x | 将所有 1 变为 0，所有 0 变为 1 |
| 按位与 | x&y | 结果是 x 和 y 的按位与。 |
| 按位或 | x\|y | 结果是 x 和 y 的按位或。 |
| 按位异或 | x^y | 结果在 x 和 y 的对应位不同处包含 1。 |
| 左移 | x<<y | 将 x 的位向左移动 y 个位位置。在腾出的位位置填入 0。 |
| 右移 | x>>y | 将 x 的位向右移动 y 个位位置。在腾出的位位置填入 0。 |

## 其他运算符

| 运算符名称 | 语法 | 结果 |
|---|---|---|
| 函数调用 | `x(y)` | 结果为函数 *x*（以参数 *y* 调用）返回的值（如果有）。 |
| 类型转换 | `(type) x` | 将 *x* 的值转换为括号中指定的类型 |
| 条件运算符 | `z?x:y` | 如果 *z* 不为 0，则计算 *x*；否则，计算 *y*。 |
| 逗号运算符 | `x,y` | 先计算 *x*，然后计算 *y* |

## 运算符优先级

典型的 C 表达式由多个操作数和运算符组成。在编写复杂表达式时，你必须了解编译器评估运算符的顺序。例如，假设一个程序使用如下定义的整数指针数组：

```c
typedef int *IntPtr; // 使用 typedef 简化声明

/* 一个包含 10 个指向 int 的指针的数组。 */

IntPtr iptr[10];
```

现在假设你遇到了表达式 `*iptr[4]`。它指的是 `iptr[4]` 中地址对应的 int 值，还是指 `iptr` 中地址对应的第五个元素？你真正需要知道的是编译器是否在下标运算符（`[ ]`）之前评估间址运算符（`*`）——还是反过来？要回答这类问题，你需要了解**优先级**——即程序应用运算符的顺序。

表 2-3 总结了 C 的优先级规则。表格按优先级递减的顺序展示运算符。优先级最高的运算符——最先应用的——列在首位。表格还展示了*结合性*——即同一级别运算符的评估顺序。

**表 2-3 C 运算符的优先级和结合性**

| 运算符组 | 运算符名称 | 记法 | 结合性 |
|---|---|---|---|
| 后置 | 下标 | `x[y]` | 从左到右 |
| | 函数调用 | `x(y)` | |
| | 成员选择 | `x.y` | |
| | 成员选择 | `x->y` | |
| 一元 | 后置递增 | `x++` | 从右到左 |
| | 后置递减 | `x--` | |
| | 前置递增 | `++x` | |
| | 前置递减 | `--x` | |
| | 取地址 | `&x` | |
| | 解引用 | `*x` | |
| | 加 | `+x` | |
| | 减 | `-x` | |
| | 按位取反 | `~x` | |
| | 逻辑取反 | `!x` | |
| | 大小 | `sizeof x` | |
| | 类型转换 | `(type)x` | |
| 乘法 | 乘 | `x*y` | 从左到右 |
| | 除 | `x/y` | |
| | 取余 | `x%y` | |
| 加法 | 加 | `x+y` | 从左到右 |
| | 减 | `x-y` | |
| 移位 | 左移 | `x<<y` | 从左到右 |
| | 右移 | `x>>y` | |
| 关系 | 大于 | `x>y` | 从左到右 |
| | 大于等于 | `x>=y` | |
| | 小于 | `x<y` | |
| | 小于等于 | `x<=y` | |
| 相等 | 等于 | `x==y` | 从左到右 |
| | 不等于 | `x!=y` | |
| 按位 | 按位与 | `x&y` | 从左到右 |
| | 按位异或 | `x^y` | |
| | 按位或 | `x|y` | |
| 逻辑 | 逻辑与 | `x&&y` | 从左到右 |
| | 逻辑或 | `x||y` | |
| 条件 | 条件 | `z?x:y` | 从右到左 |
| 赋值 | 赋值 | `x=y` | 从右到左 |
| | 乘并赋值 | `x *= y` | |
| | 除并赋值 | `x /= y` | |
| | 取余并赋值 | `x %= y` | |

回到解释 `*iptr[4]` 的问题，只需快速查看表 2-3 即可得知，`[]` 运算符的优先级高于 `*` 运算符。因此，当编译器处理表达式 `*iptr[4]` 时，它先计算 `iptr[4]`，然后应用`解引用`运算符，最终得到 `iptr[4]` 中地址对应的 `int` 值。

## 语句

你使用语句来表示 C 函数执行的动作，并控制 C 程序的执行流程。`语句`由关键字、表达式和其他语句组成。每条语句以分号（`;`）结尾。

一种特殊的语句类型——`复合语句`——是由一对花括号（`{...}`）包围的一组语句。函数的主体就是一个复合语句。这类复合语句（也称为`代码块`）可以包含局部变量。

在以下部分——按字母顺序排列——中，我简要介绍了 C 中可用的语句类型。

### break 语句

使用 `break` 语句跳转到最内层 `do`、`for`、`switch` 或 `while` 语句之后的下一条语句。它也用于退出 `switch` 语句。下面是一个使用 `break` 退出 `for` 循环的示例：

```c
for(i = 0; i < ncommands; i++)
{
   if(strcmp(input, commands[i]) == 0) break;
}
```

### case 语句

`case` 语句用于标记 `switch` 语句中的标签。下面是一个示例。（此处 `interrupt_id` 是一个整型变量。）

```c
switch (interrupt_id)
{
case XMIT_RDY:
transmit();
break;
case RCVD_RDY:
receive();
break;
}
```



### 复合语句或代码块

复合语句或代码块是由声明后跟语句的一组内容，全部包含在一对花括号中（`{ . . . }`）。典型的复合语句包括函数主体和 `if` 语句后面的代码块。在下面的示例中，花括号内出现的所有内容——声明和语句——构成了一个复合语句：

```c
if(theEvent.expose.count == 0)
{
int i;
/* 清除窗口并绘制"figures"数组中的图形
*/
XClearWindow(theDisplay, dWin);
if(numfigures > 0)
for(i=0; i<numfigures; i++)
draw_figure(theDisplay, dWin, theGC, i);
}
```

### continue 语句

`continue` 语句开始其所在的最内层 `do`、`for` 或 `while` 语句的下一次迭代。当你想要跳过循环的执行时，可以使用 `continue`。例如，要累加 1 到 10 的数字（排除 5），可以使用一个 `for` 循环，当循环索引 (`i`) 为 5 时跳过循环体：

```c
for(i=0, sum=0; i <= 10, i++)
{
if(i == 5) continue; /* 排除 5 */
sum += i;
}
```

### default 标签

在 `switch` 语句中使用 `default` 作为标签，以标记当没有 `case` 标签与 `switch` 表达式匹配时执行的代码。

### do 语句

`do` 语句与 `while` 一起形成具有以下结构的迭代循环：

```c
do
    statement
while(expression);
```

`statement`（通常是复合语句）会执行，直到 `while` 语句中的 `expression` 的值为 0。表达式在每次执行 `statement` 后求值——因此 `do-while` 块*至少执行一次*。例如，要累加 1 到 10 的数字，可以使用以下 `do` 语句：

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

表达式语句是为了其副作用而被求值的。表达式语句的一些典型用途包括调用函数、递增变量和将值赋给变量。以下是一些示例：

```c
printf("Hello, World!\n");
i++;
num_bytes = length * sizeof(char);
```

### for 语句

使用 `for` 语句执行任意次数的语句（该次数基于表达式的值）。语法如下：

```c
for (expr_1; expr_2; expr_3) statement
```

`expr_1` 在循环开始时求值一次，语句执行直到表达式 `expr_2` 的值为 0。第三个表达式 `expr_3` 在每次执行 `statement` 后求值。这三个表达式都是可选的，如果省略 `expr_2`，其值假设为 1。下面是一个使用 `for` 循环累加 1 到 10 的数字的示例：

```c
for(i=0, sum=0; i <= 10; sum += i, i++);
```

在这个示例中，累加数字的实际工作是在第三个表达式中完成的，而由 `for` 循环控制的语句是一个`空`语句（单个分号）。

### goto 语句

`goto` 语句将控制权转移到语句标签。下面是一个示例，它提示用户输入一个值，如果值不可接受则重复请求：

```c
ReEnter:
    printf("Enter offset: ");
    scanf(" %d", &offset);
    if(offset < 0 || offset > MAX_OFFSET)
    {
        printf("Bad offset: %d Please reenter:\n" ,
               offset);
        goto ReEnter;
    }
```

### if 语句

可以使用 `if` 语句测试一个表达式，并且仅在表达式不为零时执行语句。`if` 语句的形式如下：

```c
if ( expression ) statement
```

`if` 语句后面的语句仅在括号内的表达式求值为非零值时执行。该语句通常是复合语句。下面是一个示例：

```c
if(mem_left < threshold)
{
    Message("Low on memory! Please close some
            windows.\n");
}
```

### if-else 语句

`if-else` 语句是 `if` 语句与 `else` 子句结合的一种形式。该语句的语法为

## 空语句

空语句，由一个单独的分号表示，什么也不做。当所有处理都是在循环表达式中完成，而不是在循环体内进行时，在循环中使用空语句。例如，为了定位标记字符串末尾的零字节，可以使用以下代码：

```
char str[80] = "Test";
int i;
for (i=0; str[i] != '\0'; i++)
; /* 空语句 */
```

## 返回语句

返回语句停止执行当前函数并将控制权返回给调用函数。其语法为

```
return 表达式;
```

其中表达式的值作为函数的值返回。对于不返回值的函数，使用不带表达式的返回语句，如下所示：

```
return;
```

## switch 语句

`switch` 语句根据表达式的值执行多重分支。其语法如下：

```
switch (表达式)
{
case 值1:
语句_1
break;
case 值2:
语句_2
break;
...
default:
语句_默认
}
```

如果 `switch` 测试的*表达式* 的值为*值1*，则执行*语句_1*。如果表达式等于*值2*，则执行*语句_2*。该值与每个 `case` 标签进行比较，执行与匹配标签后面的语句。如果值不匹配任何 `case` 标签，则执行 `default` 标签后面的*语句_默认* 块。每个语句以一个 `break` 语句结尾，该语句将一个 `case` 标签的代码与另一个分离开。下面是一个*switch* 语句，它根据名为*command* 的整型变量的值调用不同的例程：

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
        printf ("未知命令!\n");
}
```

## while 语句

*while* 语句的使用形式为
`while` (*表达式*) *语句*

*语句* 会一直执行，直到*表达式* 的值为 0。*while* 语句在每次执行语句之前评估表达式。因此，*while* 循环执行语句零次或多次。下面是一个将数组复制到另一个数组的*while* 语句示例。

```
i = length;
while (i >= 0) { /* 将一个数组复制到另一个数组 */
    array2[i] = array1[i];
    i--;
}
```

# 函数

*函数* 是声明和语句的集合。因此，函数是 C 程序的构建块。每个 C 程序至少有一个函数 — *主函数*，C 程序的执行从这里开始。C 库主要包含函数，但也包含相当多的宏。

## 函数原型

在 C 中，使用前必须声明函数。函数声明告诉编译器函数返回值的类型以及它接受的参数数量和类型。将函数声明为完整的*函数原型*，显示返回类型以及参数列表。C 库中的 `calloc` 函数返回一个 `void` 指针，并接受两个参数，每个参数的类型均为 `size_t`，这是一种无符号整数类型，其大小足以容纳 `sizeof` 运算符的值。因此，`calloc` 的函数原型如下：

```
void *calloc(size_t, size_t);
```

此原型显示了参数列表中每个参数的类型。你也可以为每个参数包含一个标识符。在这种情况下，原型的写法如下：

```
void *calloc(size_t num_elements, size_t elem_size);
```



在这里，原型看起来与函数定义的第一行完全相同，除了你没有定义函数，并以分号结束该行。通过为参数选择恰当的名称，这种形式的原型可以提供有关函数用途的大量信息。例如，只需看一下 `calloc` 的原型，你就知道它的第一个参数是要分配的元素的数目，第二个参数是每个元素的大小。

原型还有助于编译器检查函数参数并生成可能使用更快的参数传递机制的代码。从原型中，编译器可以确定要期望的参数的确切数量和类型。因此，原型使编译器能够捕获你在调用函数时可能犯的任何错误，例如传递了错误数量的参数（当函数接受固定数量的参数时）或者向函数传递了错误类型的参数。

![](img/792720823146d68f19fd50c99ebfce4b_746_0.png)

## void 类型

当一个函数既不返回任何值也不接受任何参数时，你该怎么办？为了处理这些情况，C 提供了 `void` 类型，它对于声明不返回任何值的函数以及描述可以指向任何类型数据的指针非常有用。例如，你可以使用 `void` 返回类型来声明像 `exit` 这样不返回任何值的函数：

```
void exit(int status);
```

另一方面，如果一个函数不接受任何形式参数，其参数列表用 `void` 表示：

```
FILE *tmpfile(void);
```

`void` 指针对于处理内存块的函数非常有用。例如，当你从内存分配例程 `malloc` 请求一定数量的字节时，你可以使用这些位置来存储适合该空间的任何数据。在这种情况下，分配的内存块中第一个位置的地址作为 `void` 指针返回。因此，`malloc` 的原型写作如下：

```
void *malloc(size_t numbytes);
```

## 具有可变数量参数的函数

如果一个函数接受可变数量的参数，你可以通过使用省略号 `...` 代替参数列表来指示这一点；但是，你必须在省略号之前提供至少一个参数。这类函数的一个好例子是在头文件 `stdio.h` 中定义的 `printf` 系列函数。这些函数的原型如下：

```
int printf(FILE *stream, const char *format, ...);
int printf(const char *format, ...);
int sprintf(char *buffer, const char *format, ...);
```

## C 库

C 定义的 ANSI 和 ISO 标准涵盖了 C 的所有方面 — 语言、预处理器和库。库中函数的原型，以及所有必要的数据结构和预处理器常量，都在一组标准头文件中定义。表 2-4 列出了标准头文件，包括其内容的摘要。

> 如果你打算用 C 编写应用程序，你必须熟悉许多标准库，因为 C 的大部分编程过程都在那里。如果你在编写图形应用程序，你还必须熟悉其他库，如 GIMP 工具包。

### 表 2-4 C 中的标准头文件

| 头文件 | 目的 |
| :--- | :--- |
| `<assert.h>` | 定义 `assert` 宏。用于程序诊断。 |
| `<ctype.h>` | 声明用于分类和转换字符的函数 |
| `<errno.h>` | 定义错误条件的宏，`EDOM` 和 `ERANGE`，以及库函数返回错误代码的整型变量 `errno` |
| `<float.h>` | 定义可以存储在浮点类型中的值范围 |
| `<iso646.h>` | 定义一组宏，当使用 `&` 和 `~` 等字符组合用于其他目的的非英语语言编写 C 程序时很有帮助 |
| `<limits.h>` | 定义所有整数数据类型的极限值 |
| `<locale.h>` | 声明 `locale` 结构以及将 C 程序定制到特定语言环境的必要函数 |
| `<math.h>` | 声明常见的数学函数和 `HUGE_VAL` 宏 |
| `<setjmp.h>` | 定义 `setjmp` 和 `longjmp` 函数，可以将控制权从一个函数转移到另一个函数，而不依赖正常的函数调用和返回。还定义 `setjmp` 和 `longjmp` 使用的 `jmp_buf` 数据类型。 |
| `<signal.h>` | 定义处理异常条件所需的符号和例程 |
| `<stdarg.h>` | 定义提供对接受可变数量参数的函数中的未命名参数进行访问的宏 |
| `<stddef.h>` | 定义标准数据类型 `ptrdiff_t`, `size_t`, `wchar_t`, 符号 `NULL`, 以及宏 `offsetof`。 |
| `<stdio.h>` | 声明输入和输出操作所需的函数和数据类型。定义诸如 `BUFSIZ`, `EOF`, `SEEK_CUR`, `SEEK_END`, 和 `SEEK_SET` 等宏。 |
| `<stdlib.h>` | 声明许多实用函数，如字符串转换例程，随机数生成器，内存分配例程，以及进程控制例程（如 `abort`, `exit`, 和 `system`） |
| `<string.h>` | 声明字符串操作例程，如 `strcmp` 和 `strcpy` |
| `<time.h>` | 定义数据类型并声明操纵时间的函数。定义类型 `clock_t` 和 `time_t` 以及 `tm` 数据结构 |
| `<wchar.h>` | 定义数据类型并声明用于处理宽字符数据类型（`wchar_t`）的函数 |
| `<wctype.h>` | 定义数据类型并声明用于分类和转换宽字符数据类型（`wchar_t`）的函数 |

第八卷
第 2 章
C 语言编程

## Linux 应用程序中的共享库

大多数 Linux 程序都使用共享库。至少，大多数 C 程序都会使用 C 共享库 `libc.so.x`，其中 `x` 是一个版本号。使用共享库是可取的，因为许多可执行程序可以共享同一个共享库——只需在内存中加载一份共享库副本即可。此外，*动态链接*（即程序在运行时加载代码模块并与之链接）正变得越来越流行，因为它使应用程序能够在需要时才加载代码块，从而减少应用程序的内存需求。

当程序使用一个或多个共享库时，要运行该程序，你需要该程序的可执行文件以及所有的共享库。换句话说，如果系统上没有可用的所有共享库，你的程序将无法运行。

> 如果你销售使用共享库的应用程序，请确保所有必要的共享库都随你的软件一起分发。

共享库这个话题对 Linux 程序员来说很有意义，因为使用共享库可以减小可执行文件的大小。在接下来的部分中，我将简要描述如何在示例程序中创建和使用共享库。

## 检查程序使用的共享库

使用 `ldd` 实用工具来确定可执行程序需要哪些共享库。输入以下 `ldd` 命令以查看程序使用的共享库（该程序被 GCC 存储在默认文件 `a.out` 中）：

```
ldd a.out
```

以下是 `ldd` 针对典型 C 程序的报告：

```
linux-gate.so.1 =>  (0x00000000)
libc.so.6 => /lib/1/libc.so.6 (0x4002a000)
/lib/ld-linux.so.2 (0x40000000)
```

更复杂的程序，例如 GIMP（一款类似 Adobe Photoshop 的程序）使用更多的共享库。要查看其共享库需求，请键入以下命令：

```
ldd /usr/bin/gimp
```

在这种情况下，你会从冗长的输出中注意到，该程序使用了相当多的共享库，包括 X11 库（`libX11.so.6`）、GIMP 工具包（`libgtk-x11-2.0.so`）、通用绘图工具包（GDK）库（`libgdk-x11-2.0.so.0`）、数学库（`libm.so.6`）和 C 库（`libc.so.6`）。

几乎任何 Linux 应用程序都需要共享库才能运行。

## 创建共享库

为你自己的应用程序创建共享库相当简单。假设你想以共享库的形式实现一个对象。（将*对象*想象为一堆代码和数据。）共享库中的一组函数代表该对象的接口。要使用该对象，你需要加载其共享库并调用其接口函数。（我将在下一节中向你展示如何加载库。）

以下是以共享库形式实现的这个简单对象的 C 源代码（你也可以称之为*动态链接库*）——将此代码保存在名为 `dynobj.c` 的文件中：

```c
/*---------------------------------------------------*/
/* File: dynobj.c
 *
 * Demonstrate use of dynamic linking.
 * Pretend this is an object that can be created by
 * calling init and destroyed by calling destroy.
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
/*---------------------------------------------------*/
/* init
 * Initialize object (allocate storage).
 */
```



```c
void* init(char *name)
{
      OBJDATA *data = (OBJDATA*)calloc(1, sizeof(OBJDATA));
      if(name)
        data->name = malloc(strlen(name)+1);
      strcpy(data->name, name);
      printf("Created: %s\n", name);
      return data;
}

/*---------------------------------------------------*/
/* show
 * Show the object.
 */
void show(void *data)
{
  OBJDATA *d = (OBJDATA*)data;
  printf("show: %s\n", d->name);
}

/* ------------------------------------------------------------------ */
/* destroy
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
}
```

该对象提供三个接口函数：

- `init` 用于分配必要的存储并初始化对象
- `show` 用于显示对象（此处仅打印一条消息）
- `destroy` 用于释放所有存储

要构建名为 `libdobj.so` 的共享库，请遵循以下步骤：

1. 使用 `-fPIC` 标志编译所有源文件。在这种情况下，使用以下命令编译 `dynobj.c` 文件：
```
gcc -fPIC -c dynobj.c
```
2. 使用 `-shared` 标志将对象链接为共享库，并为链接器提供适当的标志。要创建名为 `libdobj.so.1` 的共享库，请使用以下内容：
```
gcc -shared -Wl,-soname,libdobj.so.1.0 -o libdobj.so.1.0 dynobj.o
```
3. 设置一系列符号链接，以便使用共享库的程序可以通过标准名称引用它。

对于示例库，标准名称为 `libdobj.so`，以下命令用于设置符号链接：
```
ln -sf libdobj.so.1.0 libdobj.so.1
ln -sf libdobj.so.1 libdobj.so
```
4. 测试共享库时，使用以下命令定义并导出 `LD_LIBRARY_PATH` 环境变量：
```
export LD_LIBRARY_PATH=`pwd`:$LD_LIBRARY_PATH
```

在测试共享库并确认其工作正常后，将其复制到标准位置（例如 `/usr/local/lib`），并运行 `ldconfig` 实用工具以更新 `libdobj.so.1` 和 `libdobj.so.1.0` 之间的链接。这些是将共享库安装以供所有人使用的命令。（你必须拥有 `root` 权限才能执行这些步骤。）
```
cp libdobj.so.1.0 /usr/local/lib
/sbin/ldconfig
cd /usr/local/lib
ln -s libdobj.so.1 libdobj.so
```

## 动态加载共享库

在程序中加载共享库并使用共享库内的函数非常简单。在本节中，我将演示如何执行此操作。头文件 `<dlfcn.h>`（这是 Linux 中的标准头文件）声明了用于加载和使用共享库的函数。文件 `dlfcn.h` 中声明了四个用于动态加载的函数：

- `void *dlopen(const char *filename, int flag);`：加载由文件名指定的共享库，并返回该库的句柄。标志可以是 `RTLD_LAZY`（在库代码执行时解析未定义的符号）；或 `RTLD_NOW`（在 `dlopen` 返回之前解析所有未定义的符号，如果并非所有符号都已定义则失败）。如果 `dlopen` 失败，它返回 `NULL`。
- `const char *dlerror(void);`：如果 `dlopen` 失败，调用 `dlerror` 获取包含错误描述字符串。
- `void *dlsym(void *handle, char *symbol);`：返回由句柄标识的共享库中指定符号（函数名）的地址（该句柄由 `dlopen` 返回）。
- `int dlclose(void *handle);`：如果没有其他人正在使用该共享库，则卸载它。

使用这些函数中的任何一个时，请通过以下预处理器指令包含头文件 `dlfcn.h`：
```c
#include <dlfcn.h>
```

最后，这是一个简单的测试程序——`dltest.c`——它展示了如何加载和使用前一部分中创建的共享库 `libdobj.so` 中定义的对象：
```c
/*-----------------------------------------------------------*/
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
    /* Open the shared library and set up the function
       pointers */
    if (dlobj = dlopen("libdobj.so.1", RTLD_LAZY))
    {
        void *data;
        init_call = dlsym(dlobj, "init");
        show_call = dlsym(dlobj, "show");
        destroy_call = dlsym(dlobj, "destroy");
        /* Call the object interfaces */
        data = (*init_call)("Test Object");
        (*show_call)(data);
        (*destroy_call)(data);
    }
    return 0;
}
```

该程序很直接：它加载共享库，获取库中函数的指针，并通过指针调用这些函数。

你可以按常规方式编译和链接此程序，但必须使用 `-ldl` 选项进行链接，以便可以使用在 `dlfcn.h` 中声明的函数。以下是构建程序 `dltest` 的方法：
```bash
gcc -o dltest dltest.c -ldl
```



要在实际中看到该程序的运行效果，请输入以下命令来运行 `dltest`：

`./dltest`

它会显示以下输出行：

Created: Test Object
show: Test Object
Destroying: Test Object

虽然这个示例程序并不令人兴奋，但你现在已经拥有了一个使用共享库的示例程序。

要看到使用共享库的好处，请回到前面的章节并对共享库源文件（`dynobj.c`）进行一些更改。例如，你可以在某个函数中打印其他消息，以便轻松判断你进行了某些更改。然后单独重新构建共享库。接着再次运行 `dltest`。得到的输出显示了你在共享库中所做更改的效果，这意味着你可以独立于应用程序更新共享库。

共享库中的更改可能会影响安装在系统上的许多应用程序。因此，在对*任何*共享库进行更改时要小心。同理，如果有人设法用恶意代码替换其中某个库，共享库也可能成为安全风险。

# 第 3 章：编写 Shell 脚本

## 本章内容

- 尝试简单的 shell 脚本
- 了解 shell 脚本编写的基础知识
- 探索 `bash` 的内置命令

Linux 为你提供了许多小型且专用的命令，以及将这些命令连接起来所需的“管道”机制。这里的“管道”机制指的是一个命令的输出如何被用作第二个命令的输入。`bash`（Bourne-Again Shell 的缩写）——大多数 Linux 系统中的默认 shell——通过 I/O 重定向和管道形式提供这种管道机制。`bash` 还包括一些功能，例如：你可以使用 `if` 语句仅在特定条件为真时执行命令，以及重复执行命令指定次数的 `for` 语句。在编写名为 `shell scripts` 的程序时，你可以使用 `bash` 的这些功能。

在本章中，我将向你展示如何编写简单的 `shell scripts` ——即存储在文件中、面向任务的 shell 命令集合。Shell 脚本用于自动化各种任务。例如，当你的 Linux 系统启动时，存储在 `/etc` 目录（例如 `/etc/init.d`）中各个子目录内的许多 shell 脚本会执行许多初始化任务。

## 尝试简单的 Shell 脚本

如果你不是程序员，你可能会对编程感到畏惧。但 shell `scripting`（或编程）可以简单到只是在文件中存储几条命令。事实上，你可以拥有一个仅包含一条命令的实用 shell 程序。

例如，在编写本书时，我从 X 窗口系统截取屏幕，并在图中使用这些截图。我使用 X 屏幕截取程序 `xwd` 将屏幕图像存储为 X 窗口转储（XWD）格式。然而，本书的制作团队希望屏幕截图是 TIFF 格式。因此，我使用便携式位图（PBM）工具包将 XWD 图像转换为 TIFF 格式。为了转换每个文件，我运行了两个程序并删除了一个临时文件，如下所示：

```
xwdtopnm < file.xwd > file.pnm
pnmtotiff < file.pnm > file.tif
rm file.pnm
```

这些命令假设 `xwdtopnm` 和 `pnmtotiff` 程序位于 `/usr/bin` 目录中——这是 `PATH` 环境变量列出的目录之一。顺便说一下，`xwdtopnm` 和 `pnmtotiff` 是 PBM 工具包中的两个程序。

在将几个 XWD 文件转换为 TIFF 格式后，我对为每个文件输入相同的命令序列感到厌倦，因此我准备了一个名为 `totif` 的文件，并将以下行保存在其中。（第一行有一个*咒语* `#!/bin/sh`，它启动 `bash` 程序，然后执行文件中的其余行——每个 shell 脚本都需要第一行。）

```
#!/bin/sh
xwdtopnm < $1.xwd > $1.pnm
pnmtotiff < $1.pnm > $1.tif
rm $1.pnm
```

然后，我使用以下命令使 `totif` 文件可执行：

```
chmod +x totif
```

`chmod` 命令允许你更改文件的权限设置。其中一个设置决定了文件是否可执行。`+x` 选项将该文件标记为可执行。你必须这样做，因为 `bash` 只运行可执行文件。

现在，当我想要将文件 `figure1.xwd` 转换为 `figure1.tif` 时，我可以通过输入以下命令来完成：

```
./totif figure1
```

`./` 前缀表示 `totif` 文件位于当前目录——如果 `PATH` 环境变量包含当前目录，则不需要 `./` 前缀。`totif` 文件是一个 shell 脚本（也称为 *shell 程序*）。当你使用命令 `totif figure1` 运行此 shell 程序时，shell 会将 `figure1` 替换为 `$1` 的每次出现。（注意，`$1` 指的是用户在使用执行脚本的命令中输入的第一个选项。）

Shell 脚本在系统管理员中很受欢迎。如果你是一个系统管理员，你可以构建一个自定义 shell 脚本的集合，帮助你自动化经常执行的任务。例如，如果硬盘似乎快满了，你可能希望找到所有超过一定大小（例如 1MB）且在过去 30 天内未被访问的文件。此外，你可能希望向所有拥有大文件的用户发送电子邮件消息，请求他们归档并清理这些文件。你可以使用 shell 脚本执行所有这些任务。你可以从以下 `find` 命令开始，以识别大文件：

```
find / -type f -atime +30 -size +1000k -exec ls -l {} > /tmp/largefiles
```

此命令创建一个名为 `/tmp/largefiles` 的文件，其中包含占用过多空间的旧文件的详细信息。获得文件列表后，你可以使用一些其他 Linux 命令——例如 `sort`、`cut` 和 `sed`——来准备并发送电子邮件给拥有需要清理的大文件的用户。手动输入所有这些命令很麻烦，请将它们放入文件中并创建一个 shell 脚本。简而言之，这就是 shell 脚本的精髓——将 shell 命令收集到一个文件中，以便轻松执行重复的系统管理任务。

正如大多数 Linux 命令接受命令行选项一样，bash 脚本也接受命令行选项。在脚本内部，你可以将这些选项引用为 `$1`、`$2` 等。特殊名称 `$0` 指的是脚本本身的名字。

这是一个接受参数的典型 bash 脚本：

```
#!/bin/sh
echo "This script's name is: $0"
echo "Argument 1: $1"
echo "Argument 2: $2"
```

第一行运行 `/bin/sh` 程序，该程序随后处理脚本中的其余行。名称 `/bin/sh` 传统上指的是 Bourne shell——第一个 UNIX shell。在大多数 Linux 系统中，`/bin/sh` 是指向 `/bin/bash` 的符号链接，后者是 bash 的可执行程序。

将此简单脚本保存在名为 `simple` 的文件中，并使用以下命令使该文件可执行：

```
chmod +x simple
```

现在按以下方式运行脚本：

```
./simple
```

它显示以下输出：

```
This script's name is: ./simple
Argument 1:
Argument 2:
```

第一行显示脚本的名称。由于你是在没有参数的情况下运行脚本的，因此脚本不显示任何参数值。

现在尝试使用几个参数运行脚本，如下所示：

```
./simple "This is one argument" second-argument third
```

这次脚本显示更多的输出：

```
This script's name is: ./simple
Argument 1: This is one argument
Argument 2: second-argument
```

如输出所示，shell 将双引号内的整个字符串视为单个参数。否则，shell 使用空格作为命令行中参数之间的分隔符。

此示例脚本忽略第三个参数，因为该脚本设计为仅打印前两个参数。脚本忽略前两个之后的所有参数。

## 探索 Shell 脚本编写的基础知识

与任何编程语言一样，`bash` shell 支持以下功能：

- 存储值的变量，包括用于访问传递给 shell 脚本的命令行参数以及其他特殊值的特殊内置变量。
- 评估表达式的能力。
- 控制结构，允许你对多个 shell 命令进行循环或条件性地执行某些命令。
- 定义可在脚本中多处调用的函数的能力。`bash` 还包括许多你可以在任何脚本中使用的内置命令。

在接下来的几个部分中，我通过简单的例子来说明其中一些编程功能。（假设你已经在运行 `bash`，在这种情况下，你可以通过在终端窗口中的 shell 提示符下输入示例来尝试它们。否则，你所要做的就是打开一个终端窗口，`bash` 将运行并在该窗口中显示其提示符。）

### 存储数据

你在 `bash` 中定义变量的方式与定义环境变量相同。因此，你可以如下定义变量：

```
count=12 # 注意不允许包含嵌入的空格
```



要使用变量的值，请在变量名前加美元符号（`$`）。例如，`$PATH` 是变量 `PATH` 的值。（此变量是著名的 `PATH` 环境变量，它列出了所有 `bash` 当尝试定位可执行文件时执行搜索。）要显示变量 `count` 的值，请使用以下命令：

```
echo $count
```

`bash` 有一些用于访问命令行参数的特殊变量。在 shell 脚本中，`$0` 指代 shell 脚本的名称。变量 `$1`、`$2` 等指代命令行参数。变量 `$*` 将所有命令行参数存储为一个单一变量，而 `$?` 包含 shell 执行的最后一条命令的退出状态。

从 bash 脚本中，你可以提示用户输入，并使用 `read` 命令将输入读取到一个变量中。以下是一个示例：

```
echo -n "Enter value: "
read value
echo "You entered: $value"
```

当此脚本运行时，`read value` 命令会让 `bash` 读取你在键盘上输入的内容，并将输入存储在名为 `value` 的变量中。

> *注意：-n 选项可防止 `echo` 命令在其显示的字符串末尾自动添加新行。*

## 调用 shell 函数

你可以将一组经常一致使用的 shell 命令组合成一个 `function`（函数），并为其分配一个名称。稍后，你可以通过使用该函数所分配的唯一名称来执行这一组命令。这里有一个简单的脚本，说明了 shell 函数的语法：

```
#!/bin/sh
hello() {
    echo -n "Hello, "
    echo $1 $2
}
hello Jane Doe
```

当你运行此脚本时，它会显示以下输出：

```
Hello, Jane Doe
```

此脚本定义了一个名为 `hello` 的 shell 函数。该函数期望两个参数。在函数体中，这些参数通过 `$1` 和 `$2` 进行引用。函数定义以 `hello()` 开始——即函数名称后跟括号。函数体包含在花括号中——`{...}`。在这种情况下，函数体使用 `echo` 命令显示一行文本。

示例的最后一行展示了如何带参数调用 shell 函数。在这种情况下，`hello` 函数带有两个参数调用：`Jane` 和 `Doe`。`hello` 函数接收这两个参数并打印出一行内容为 `Hello, Jane Doe` 的文本。

## 控制流程

在 `bash` 脚本中，你可以使用诸如 `if`、`case`、`for` 和 `while` 等特殊命令来控制执行流程——即命令执行的顺序。这些控制语句使用命令的退出状态来决定下一步做什么。任何命令执行后都会返回一个退出状态——一个指示命令是否成功的数值。按照惯例，退出状态为零表示命令成功。（是的，你没看错：零表示成功！）非零的退出状态表示命令出了点问题。

例如，假设你想在使用 `vi` 编辑器编辑文件之前制作一个备份副本。更重要的是，如果无法创建备份，你希望避免编辑该文件。下面是一个 `bash` 脚本，负责处理此任务：

```
#!/bin/sh
if cp "$1" "#$1"
then
    vi "$1"
else
    echo "Failed to create backup copy"
fi
```

此脚本说明了 `if`-`then`-`else` 结构的语法，并展示了 `if` 命令如何使用 `cp` 命令的退出状态来确定下一步操作。如果 `cp` 返回零，脚本会使用 `vi` 编辑文件；否则，脚本会显示错误消息并退出。顺便说一下，脚本将备份保存在一个文件中，其名称与原始文件相同，只是在文件名开头加了一个井号（`#`）。

![](img/792720823146d68f19fd50c99ebfce4b_761_0.png)

别忘了终止 `if` 命令的最终 `fi`。忘记 `fi` 是 `bash` 脚本中常见的错误来源。

你可以使用 `test` 命令来评估任何表达式，并将该表达式的值用作命令的退出状态。假设你想编写一个仅在文件已存在时才编辑该文件的脚本。使用 `test`，你可以这样编写这样的脚本：

```
#!/bin/sh
if test -f "$1"
then
    vi "$1"
else
    echo "No such file"
fi
```

`test` 命令的一种较短形式是将表达式放在方括号内（`[...]`）。使用这种简写表示法，你可以将前面的脚本重写如下：

```
#!/bin/sh
if [ -f "$1" ]
then
    vi "$1"
else
    echo "No such file"
fi
```

**注意**：两个方括号周围必须有空格。

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

`case` 语句用于根据变量的值执行一组命令。例如，请考虑以下脚本：

```
#!/bin/sh
echo -n "What should I do -- (Y)es/(N)o/(C)ontinue? [?] "
read answer
case $answer in
    y\|Y\|"")
        echo "YES"
    ;;
    c\|C)
        echo "CONTINUE"
    ;;
    n\|N)
        echo "NO"
    ;;
    *)
        echo "UNKNOWN"
    ;;
esac
```

将此代码保存到一个名为 `confirm` 的文件中，并输入 `chmod +x confirm` 使其可执行。然后像这样试用它：

```
./confirm
```

当脚本提示你时，输入字符 `y`、`n` 或 `c` 之一并按 Enter。脚本将显示 `YES`、`NO` 或 `CONTINUE`。例如，以下是当我输入 `c`（然后按 Enter）时发生的情况：

```
What should I do -- (Y)es/(N)o/(C)ontinue? [Y] c
CONTINUE
```

脚本显示一个提示并读取你输入的输入。你的输入存储在名为 `answer` 的变量中。然后，`case` 语句根据 `answer` 变量的值执行一块代码。例如，当我输入 `c` 时，以下命令块被执行：

```
c|C) echo "CONTINUE" ;;
```

`echo` 命令使脚本显示 `CONTINUE`。

从这个例子中，你可以看到 `case` 命令的一般语法如下：

```
case $variable in
value1 | value2
command1
command2
...other commands ...
;;
value3}
command3
command4
...other commands...
;;
esac
```

本质上，`case` 命令以单词 `case` 开始，以 `esac` 结束。代码块之间由变量的值分隔，后面跟着一个右括号，并以一对分号 (`;;`) 终止。

## 探索 `bash` 的内置命令

`bash` 有 50 多个内置命令，包括 `cd` 和 `pwd` 等常用命令，还有许多其他不常用的命令。你可以在任何 `bash` 脚本或 shell 提示符中使用这些内置命令。表 3-1 描述了大多数 `bash` 内置命令及其参数。在查看这些信息后，输入 `help` `command` 以阅读有关特定内置命令的更多详细信息。例如，要了解有关内置命令 `test` 的更多信息，请输入以下内容：

```
help test
```

这样做会显示以下信息：

```
test: test [expr]
根据 EXPR 的评估结果，以状态 0（true）或 1（false）退出。表达式可以是单目或双目。单目表达式通常用于检查文件的状态。除了字符串运算符外，还有数值比较运算符。

文件运算符：
    -a FILE     如果文件存在，则为真。
    -b FILE     如果文件是块特殊文件，则为真。
    -c FILE     如果文件是字符特殊文件，则为真。
    -d FILE     如果文件是目录，则为真。
    -e FILE     如果文件存在，则为真。
    -f FILE     如果文件存在且是普通文件，则为真。
    -g FILE     如果文件设置了 set-group-id，则为真。
    -h FILE     如果文件是符号链接，则为真。
    -L FILE     如果文件是符号链接，则为真。
```



### 文件测试选项

`-k FILE` 如果文件设置了 'sticky' 位，则为真。

`-p FILE` 如果文件是命名管道，则为真。

`-r FILE` 如果你可以读取文件，则为真。

`-s FILE` 如果文件存在且非空，则为真。

`-S FILE` 如果文件是套接字，则为真。

`-t FD` 如果 `FD` 在终端上打开，则为真。

`-u FILE` 如果文件设置了 set-user-id，则为真。

`-w FILE` 如果你可以写入文件，则为真。

`-x FILE` 如果你可以执行文件，则为真。

`-o FILE` 如果你实际拥有该文件，则为真。

`-G FILE` 如果你所在的组实际拥有该文件，则为真。

... 行已删除 ...



如有必要，来自 `help` 命令的在线帮助包含大量详细信息。

某些外部程序可能与 `bash` 内置命令具有相同的名称。如果你想运行任何此类外部程序，必须明确指定该程序的完整路径名。否则，`bash` 将执行同名内置命令。

![](img/792720823146d68f19fd50c99ebfce4b_764_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_764_1.png)

# 740 探索 Shell 脚本基础

## bash Shell 内置命令概述

| 此功能 | 执行以下操作 |
| :--- | :--- |
| `.` `filename` `[arguments]` | 使用可选参数从指定文件中读取并执行命令。（工作方式与 `source` 命令相同。） |
| `:` `[arguments]` | 扩展参数但不处理它们 |
| `[` `expr` `]` | 计算表达式 `expr`，如果 `expr` 为真，则返回零状态 |
| `alias` `[name[=value] . . . ]` | 定义一个别名 |
| `bg` `[job]` | 将指定作业放到后台。如果未指定作业，则将当前正在执行的命令放到后台。 |
| `bind` `[-m keymap] [-lvd] [-q name]` | 将按键序列绑定到宏 |
| `break` `[n]` | 退出 `for`、`while` 或 `until` 循环。如果指定了 `n`，则退出第 `n` 层包围的循环。 |
| `builtin` `builtin_command` `[arguments]` | 执行 shell 内置命令 |
| `cd` `[dir]` | 将当前目录更改为 `dir` |
| `command` `[-pVv]` `cmd` `[arg . . .]` | 使用指定参数运行命令 `cmd`（忽略任何名为 `cmd` 的 shell 函数） |
| `continue` `[n]` | 开始 `for`、`while` 或 `until` 循环的下一次迭代。如果指定了 `n`，则开始第 `n` 层包围循环的下一次迭代。 |
| `declare` `[[-frx] [name[=value]]]` | 声明具有指定名称的变量，并可选地为其分配一个值。 |
| `dirs` `[-l]` `[+/-n]` | 显示当前记住的目录列表 |
| `echo` `[nE]` `[arg . . .]` | 在标准输出中显示参数 |
| `enable` `[-n]` `[-all]` `[name . . .]` | 启用或禁用指定的内置命令 |
| `eval` `[arg . . .]` | 将参数连接起来并作为命令执行 |
| `exec` `[command [arguments]]` | 用运行指定命令的新进程替换当前 shell 实例 |
| `exit` `[n]` | 以状态码 `n` 退出 shell |
| `export` `[-nf]` `[name[=word]] . . .` | 定义指定的环境变量并将其导出到未来进程 |
| `fc` `-s` `[pat=rep]` `[cmd]` | 在将模式 `pat` 替换为 `rep` 后重新执行命令 |
| `fg` `[jobspec]` | 将指定作业放到前台。如果未指定作业，则将最近的作业放到前台。 |
| `getopts` `optstring name [args]` | 获取可选参数（在 shell 脚本中用于从命令行提取参数时调用） |
| `hash` `[-r]` `[name]` | 记住指定命令的完整路径名 |
| `help` `[cmd...]` | 显示指定内置命令的帮助信息 |
| `history` `[n]` | 显示过去的命令，或者如果你指定了数字 `n`，则显示过去 `n` 条命令 |
| `jobs` `[-lnp]` `[ jobspec ... ]` | 列出当前活动的作业 |
| `kill` `[-s sigspec \| -sigspec]` `[pid \| jobspec]` | 终止一个进程 |
| `let` `arg (arg...)` | 评估每个参数，如果最后一个参数为 0，则返回 1 |
| `local` `[name=[value] ...]` | 创建具有指定名称和值的局部变量（用于 shell 函数中） |
| `logout` | 退出登录 shell |
| `popd` `[+/ -n]` | 从目录栈中移除条目 |
| `pushd` `[dir]` | 将指定目录添加到目录栈的顶部 |
| `pwd` | 打印当前工作目录的完整路径名 |
| `read` `[-r]` `[name...]` | 从标准输入读取一行并解析它 |
| `readonly` `[-f]` `[name...]` | 将指定变量标记为只读，以便之后不能更改这些变量 |
| `return` `[n]` | 以返回值 `n` 退出 shell 函数 |
| `set` `[ -abefhkmnptuvxLDCHP]` `[ -o option]` `[arg...]` | 设置各种标志 |
| `shift` `[n]` | 使第 `n+1` 个参数变为 `$1`，第 `n+2` 个参数变为 `$2`，等等 |
| `source` `filename (arguments)` | 从文件中读取并执行命令 |
| `suspend` `[-f]` | 停止执行，直到接收到 SIGCONT 信号 |
| `test` `expr` | 计算表达式 `expr`，如果 `expr` 为真，则返回零 |
| `times` | 打印从 shell 运行的进程的累积用户时间和系统时间 |
| `trap` `[-l]` `[cmd]` `[sigspec]` | 当接收到信号 `sigspec` 时执行 `cmd` |
| `type` `[-all]` `[-type]` `[-path]` `name` `[name ...]` | 指示 shell 如何解释每个名称 |
| `ulimit` `[-HSacdfmstpvuv [limit]]` | 控制 shell 可用的资源 |
| `umask` `[-S]` `[mode]` | 设置文件创建掩码——文件的默认权限 |
| `unalias` `[-a]` `[name ...]` | 取消定义指定的别名 |
| `unset` `[-fv]` `[name ...]` | 移除指定变量的定义 |
| `wait` `[n]` | 等待指定进程终止 |

表 3-1

# 第 4 章：Perl 编程

## 本章内容

- 编写你的第一个 Perl 程序
- 概览 Perl
- 理解 Perl 包和模块
- 在 Perl 中使用对象

在编写脚本方面，Perl 语言在系统管理员中非常流行，尤其是在 UNIX 和 Linux 系统上。系统管理员使用 Perl 来自动化例行的系统管理任务，例如查找可以归档和删除以释放磁盘空间的旧文件。

Perl 是一种脚本语言，这意味着你不需要编译和链接 Perl 脚本（包含 Perl 命令的文本文件）。相反，解释器执行 Perl 脚本。这种能力使得编写和测试 Perl 脚本变得容易，因为你不需要经历典型的编辑-编译-链接循环来编写 Perl 程序。

除了编程简便性之外，Perl 流行的另一个原因是 Perl 是免费分发的，并且可用于各种各样的操作系统，包括 Linux 以及许多其他系统，如 UNIX、Windows 95/98/NT/2000/XP 和 Apple Mac OS X。

在本章中，我将向你介绍 Perl 脚本编写。

## 理解 Perl

官方上，Perl 代表 *实用提取报告语言*（*Practical Extraction Report Language*），但 Perl 的创建者 Larry Wall 说，人们经常将 Perl 称为 *病态的电色垃圾列表器*（*Pathologically Electic Rubbish Lister*）。正如这些名称所示，Perl 最初被设计用于从文本文件中提取信息并生成报告。

Perl 诞生于 1986 年，最初是 Larry Wall 创建的一种系统管理工具。随着时间推移，Perl 通过不断累积许多新的特性和功能而成长。最新版本——Perl 5.8——支持面向对象编程，并允许任何人通过以指定格式添加新模块来扩展 Perl。

忠实于其作为系统管理工具的起源，Perl 多年来一直深受 UNIX 系统管理员的欢迎。最近，当万维网（或简称为 Web）变得流行并且需要通用网关接口（CGI）程序时，对于已经熟悉该语言的人来说，Perl 成为了自然的选择。Perl 近期流行度的激增主要归因于 Perl 在编写 Web CGI 程序中的应用。当然，随着人们更多地关注 Perl，他们发现 Perl 的用途远不止于 CGI 编程。进而，这使得 Perl 在用户中更加流行。

Perl 在多种计算机系统上可用，因为像 Linux 操作系统一样，Perl 可以自由分发。

如果你熟悉 shell 编程或 C 编程语言，你可以很快掌握 Perl。如果你从未编写过程序，精通 Perl 可能需要一些时间。我鼓励你从 Perl 特性的小子集开始，忽略那些你立即无法理解的内容。然后，慢慢将 Perl 特性添加到你的技能库中。

## 确定你是否有 Perl

在你继续 Perl 教程之前，检查你的 Linux 系统是否安装了 `perl` 程序。输入以下命令：

```
which perl
```



`which` 命令告诉你是否在 `PATH` 环境变量列出的目录中找到了指定的程序。如果安装了 `perl`，你会看到以下输出：

```
/usr/bin/perl
```

你应该在所有 Linux 发行版中都能找到已安装的 Perl。

检查 Perl 的另一种方法是输入以下命令以查看其版本号：

```
perl -v
```

以下是该命令的典型输出：

```
This is perl, v5.8.7 built for i586-linux-thread-multi

Copyright 1987-2005, Larry Wall

Perl may be copied only under the terms of either the Artistic License or the

GNU General Public License, which may be found in the Perl 5 source kit.
```

完整的 Perl 文档，包括常见问题列表，可以通过在此系统上使用 `man perl` 或 `perldoc perl` 找到。如果你可以访问互联网，请将浏览器指向 [http://www.perl.org/](http://www.perl.org/)，即 Perl 主页。

此输出告诉你，你拥有 Perl 5.8 版本，补丁级别为 7，并且 Perl 的创始人拉里·沃（Larry Wall）持有版权。（请记住，Perl 是在 GNU 通用公共许可协议下自由分发的。）

![](img/792720823146d68f19fd50c99ebfce4b_770_0.png)

你可以通过将万维网浏览器指向综合 Perl 归档网络（CPAN）来获取 Perl 的最新版本。以下地址将连接到你最近的 CPAN 站点：

www.perl.com/CPAN

# 编写你的第一个 Perl 脚本

Perl 具有 C 语言的许多特性，正如你可能知道的那样，大多数关于 C 的书都以一个在终端上显示 “Hello, World!” 的示例程序开始。由于 Perl 是一种解释型语言，与需要先编译才能运行的 C 和 C++ 不同，你可以直接通过命令行完成此任务。如果你输入

```
perl -e 'print "Hello, World!\n";'
```

Perl 会响应以下内容：

```
Hello, World!
```

此命令使用 `perl` 程序的 `-e` 选项，将 Perl 程序作为命令行参数传递给 Perl 解释器。在这种情况下，以下行构成了 Perl 程序：

```
print "Hello, World!\n";
```

要将此行转换为 Perl 脚本，只需将此行放入文件中，并在文件开头添加一个用于运行 `perl` 程序的指令（就像你在 shell 脚本中放置 `#!/bin/sh` 让 Shell 处理脚本一样）。

要尝试这个 Perl 脚本，请按照以下步骤操作：

1. 使用文本编辑器输入并保存以下各行，文件名命名为 `hello.pl`：

```
#!/usr/bin/perl

# This is a comment.

print "Hello, World!\n";
```

2. 使用以下命令使 `hello.pl` 文件可执行：

```
chmod +x hello.pl
```

3. 通过在 shell 提示符下输入以下内容来运行 Perl 脚本：

```
./hello.pl
```

它会显示以下输出：

Hello, World!

就这样！你已经编写并尝试了你的第一个 Perl 脚本。

![](img/792720823146d68f19fd50c99ebfce4b_771_0.png)

请注意，Perl 脚本的第一行以 `#!` 开头，后跟 `perl` 程序的完整路径名。如果脚本的第一行以 `#!` 开头，shell 简单地剥去 `#!`，将脚本文件的名称附加到末尾，并运行该脚本。因此，如果脚本文件命名为 `hello.pl` 且第一行是 `#!/usr/bin/perl`，则 shell 将执行以下命令：

`/usr/bin/perl hello.pl`

# 了解 Perl 概览

大多数编程语言，包括 Perl，都有一些共同的功能：

- `变量` 存储不同类型的数据。你可以将每个变量视为数据的一个占位符——有点像邮箱，有名字且有空间存储数据。变量的内容是其值。
- `表达式` 通过运算符组合变量。一个表达式可能将几个变量相加；另一个可能提取字符串的一部分。
- `语句` 执行某些操作，例如将值赋值给变量或打印字符串。
- `流程控制语句` 使语句能够根据某个表达式的值以各种顺序执行。通常，流程控制语句包括 `for`、`do-while`、`while` 和 `if-then-else` 语句。
- `函数`（也称为 `子程序` 或 `程序例程`）使你可以将几个语句分组并为其命名。使用此功能，你可以通过调用代表这些语句的函数来执行相同的语句集。通常，编程语言提供一些预定义的函数。
- `包` 和 `模块` 使你可以组织一组设计为可重用的相关 Perl 子程序。（模块是在 Perl 5 中引入的。）

在接下来的几节中，我将对 Perl 的这些主要功能进行概述，并通过简单的示例来说明这些功能。

## 基本的 Perl 语法

Perl 是自由格式的，就像 C 一样。对任何关键字的确切位置没有约束。通常，Perl 程序存储在以 `.pl` 结尾名称的文件中，但对你使用的文件名没有限制。

与 C 一样，每个 Perl 语句以分号（`;`）结尾。井号或英镑符号（`#`）标记注释的开始；`perl` 程序忽略以井号开始的该行的其余部分。

Perl 语句组被大括号（`{...}`）包围。此特性在 C 中也很相似。

## 变量

你不必像在使用 C 编程语言那样，在使用 Perl 变量之前先声明它们。你可以轻松识别 Perl 脚本中的变量，因为每个变量名都以一个特殊字符开头：at 符号（`@`）、美元符号（`$`）或百分号（`%`）。这些特殊字符表示变量的类型。三种变量类型如下：

- 标量变量表示基本数据类型：整数、浮点数和字符串。美元符号（`$`）置于标量变量之前。以下是一些示例：

```perl
$maxlines = 256;
$style = "Linux All-in-One Desk Reference For Dummies";
```

- 数组变量是标量变量的集合。数组变量以前缀 at 符号（`@`）开头。因此，以下是数组：

```perl
@pages = (62, 26, 22, 24);
@commands = ("start", "stop", "draw", "exit");
```

- 关联数组是键值对的集合，其中每个键都是字符串，值是任何标量变量。前缀百分号（`%`）表示关联数组。你可以使用关联数组将名称与值关联起来。你可以在关联数组中存储每个用户占用的磁盘空间，例如：

```perl
%disk_usage = ("root", 147178, "naba", 28547,
               "emily", 55, "ashley", 40);
```

由于每种变量类型都有一个特殊字符前缀，你可以为不同的变量类型使用相同的名称。因此，`$disk_usage`、`@disk_usage` 和 `%disk_usage` 可以出现在同一个 Perl 程序中。

![](img/792720823146d68f19fd50c99ebfce4b_772_0.png)

## 标量

*标量变量* 可以存储单个值，如数字或文本字符串。标量变量是 Perl 中的基本数据类型。每个标量的名称以美元符号（`$`）开头。通常，你从初始化的赋值语句开始使用标量。你甚至可以在未初始化的情况下使用变量；数字的默认值是零，字符串的默认值是空字符串。如果你想知道某个标量是否已定义，请使用 `defined` 函数，如下所示：

```perl
print "Name undefined!\n" if !(defined $name);
```

表达式 `(defined $name)` 在 `$name` 已定义时为 1。你可以使用 `undef` 函数*取消定义*变量。例如，你可以取消定义 `$name`，如下所示：

```perl
undef $name;
```

根据上下文评估变量。以下是一个初始化并打印几个变量的脚本：

```perl
#!/usr/bin/perl
$Title = "Linux All-in-One Desk Reference For Dummies";
$Count1 = 650;
$Count2 = 166;
$Total = $Count1 + $Count2;
```



`print "Title: $Title -- $Total pages\n";`

```
当你运行上述 Perl 程序时，它会产生以下输出：
```

```text
Title: Linux All-in-One Desk Reference For Dummies -- 816 pages
```

正如 Perl 语句所示，当两个数值变量相加时，使用的是它们的数值；但当打印 `$Total` 变量时，显示的是其字符串表示形式。

Perl 的一个有趣方面是，它评估双引号（“...”）内字符串中的所有变量。但是，如果你在单引号（‘...’）内编写字符串，Perl 将保持该字符串不变。如果你编写

## 数组

在 Perl 中，数组是标量的集合。数组名以 at 符号（`@`）开头。与 C 一样，数组下标从零开始。你可以使用索引访问数组的元素。Perl 动态分配数组的空间。

考虑以下简单脚本：

```perl
#!/usr/bin/perl

@commands = ("start", "stop", "draw", "exit");

$numcmd = @commands;

print "There are $numcmd commands.\n";

print "The first command is: $commands[0]\n";
```

当你运行该脚本时，它会产生以下输出：

There are 4 commands.
The first command is: start

你可以看到，将标量与数组等同会将该标量设置为数组中元素的数目。`@commands` 数组的第一个元素引用为 `$commands[0]`，因为索引从零开始。因此，`@commands` 数组中的第四个元素是 `$commands[3]`。

有两个特殊的标量与数组相关。`$[` 变量是其中之一，它是当前的基索引（起始索引），默认为零。另一个标量是 `$arrayname`（其中 `arrayname` 是数组变量的名称），其值为最后一个数组索引。因此，对于 `@commands` 数组，`$commands` 为 3。

你可以使用简单的 `print` 语句打印整个数组，如下所示：

```perl
print "@commands\n";
```

当 Perl 执行此语句时，它显示以下输出：

start stop draw exit

## 关联数组

关联数组变量，使用百分号（`%`）前缀声明，是 Perl 的独特特性。使用关联数组，你可以用字符串（例如名称）作为索引来访问数组。一个关联数组的好例子是 Perl 自动为你定义的 `%ENV` 数组。在 Perl 中，`%ENV` 是环境变量数组，你可以使用环境变量名称作为索引来访问它。以下 Perl 语句打印当前的 PATH 环境变量：

```
print "PATH = $ENV{PATH}\n";
```

当 Perl 执行此语句时，它会打印 PATH 的当前设置。与索引常规数组不同，你必须使用花括号来索引关联数组。

Perl 有许多内置函数——例如 `delete`、`each`、`keys` 和 `values`——使你能够访问和操作关联数组。

## Perl 中的预定义变量

Perl 具有若干预定义变量，其中包含你在 Perl 脚本中可能需要的一些有用信息。以下是几个重要的预定义变量：

- `@ARGV` 是一个字符串数组，包含脚本的命令行选项。第一个选项是 `$ARGV[0]`，第二个是 `$ARGV[1]`，依此类推。
- `%ENV` 是一个关联数组，包含环境变量。你可以使用环境变量名称作为键来访问此数组。要访问数组中的每个元素，将百分号改为美元符号，并用括号将键括起来。例如，`$ENV{HOME}` 是主目录，`$ENV{PATH}` 是 shell 用于定位命令的当前搜索路径。
- `$_` 是许多函数的默认参数。如果你看到没有参数的 Perl 函数，该函数可能期望其参数包含在 `$_` 变量中。
- `@_` 是传递给子例程的参数列表。
- `$0` 是包含 Perl 程序的文件名称。
- `$]` 是你正在使用的 Perl 的版本号（例如，如果你使用 Perl 5.8.7 版本，`$]` 将是 5.008007）。
- `$<` 是运行脚本用户的用户 ID（标识号）。
- `$$` 是脚本的进程 ID。
- `$?` 是最后一次系统调用返回的状态。

## 运算符和表达式

运算符用于组合和比较 Perl 变量。典型的数学运算符包括加法 (`+`)、减法 (`-`)、乘法 (`*`) 和除法 (`/`)。Perl 和 C 提供几乎相同的运算符集合。当你使用运算符组合变量时，你会得到表达式。每个表达式都有一个值。

以下是一些典型的 Perl 表达式：

```
error < 0
$count == 10
$count + $i
$suers[{$i}]
```

这些表达式是**比较运算符**（前两行）、算术运算符和数组索引运算符的示例。

![](img/792720823146d68f19fd50c99ebfce4b_776_0.png)

在 Perl 中，不要使用 `==` 运算符来确定两个字符串是否匹配；`==` 运算符仅适用于数字。要测试字符串的相等性，Perl 包含 FORTRAN 风格的 `eq` 运算符。使用 `eq` 来查看两个字符串是否相同，如下所示：

```
if ($input eq "stop") { exit; }
```

其他 FORTRAN 风格的字符串比较运算符包括 `ne`（不等于）、`lt`（小于）、`gt`（大于）、`le`（小于或等于）和 `ge`（大于或等于）。此外，你可以使用 `cmp` 运算符比较两个字符串。返回值是 −1、0 或 1，取决于第一个字符串是小于、等于还是大于第二个字符串。

Perl 还提供了以下独特的运算符。C 缺少幂运算符，而 FORTRAN 包含它；Perl 使用 `**` 作为幂运算符。因此，你可以在 Perl 中编写以下代码：

```
$x = 2;
$y = 3;
$z = $x**$y;  # z 应为 8（2 的 3 次方）
$y **= 2;  # y 现在是 9（3 的 2 次方）
```

你可以使用空列表运算符 `()` 将数组初始化为空值，如下所示：

```
@commands = ();
```

点运算符 (`.`) 使你能够连接两个字符串，如下所示：

```
$part1 = "Hello, ";
$part2 = "World!";
$message = $part1.$part2; # 现在 $message = "Hello, World!"
```

重复运算符，表示为 `x=`，很有趣且非常有用。你可以使用 `x=` 运算符将字符串重复指定的次数。假设你想将一个字符串初始化为 65 个星号 (`*`)。以下示例展示了如何使用 `x=` 运算符初始化字符串：

```
$marker = "*";
$marker x= 65; # 现在 $marker 是一个由 65 个星号组成的字符串
```

Perl 中另一个强大的运算符是范围运算符，由两个点 (` .. `) 表示。你可以使用范围运算符轻松初始化数组。以下是一些示例：

```
@numerals = (0..9); # @numerals = 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
@alphabet = ('A'..'Z'); # @alphabet = 大写字母 A 到 Z
```

## 正则表达式

如果你使用过一段时间的 UNIX 或 Linux 系统，你可能知道 `grep` 命令，它允许你搜索文件中的字符串模式。以下是 `grep` 的一个典型用法：

```
cd /usr/include
grep "[Ll]inux" *.h | more
```



前面的 `grep` 命令查找以 `.h` 结尾的文件中 **Linux 或 linux** 的所有出现。

`grep` 命令的 "`[Ll]inux`" 参数被称为 *正则表达式*，这是一种匹配一组字符串的模式。你使用一组类似编写算术表达式规则的运算符和规则来构建正则表达式。例如，方括号 `[ ]` 内的字符列表匹配列表中的任意单个字符。因此，正则表达式 "`[Ll]inux`" 是由以下两个字符串组成的集合：

Linux
linux

Perl 支持正则表达式，正如 `grep` 命令一样。许多其他 Linux 程序，如 `vi` 编辑器和 `sed`（流编辑器），也支持正则表达式。正则表达式的目的是在文件中搜索字符串模式。这就是为什么编辑器支持正则表达式。

你可以在 Perl 中构建和使用复杂的正则表达式。这些正则表达式的规则相当简单。本质上，正则表达式是一个字符序列，其中某些字符具有特殊含义。表 4-1 总结了用于构建正则表达式的字符的基本解释规则。

### 表 4-1 解释正则表达式字符的规则

| 表达式 | 含义 |
| :--- | :--- |
| `.` | 匹配除换行符外的任意单个字符 |
| `\x*` | 匹配字符 `\x` 零次或多次出现 |
| `\x+` | 匹配字符 `\x` 一次或多次出现 |
| `\x?` | 匹配字符 `\x` 零次或一次出现 |
| `[ . . . ]` | 匹配括号内的任意字符 |
| `\x{ n }` | 匹配字符 `\x` 恰好 n 次出现 |
| `\x{ n, }` | 匹配字符 `\x` n 次或更多次出现 |
| `\x{ n , m }` | 匹配字符 `\x` 至少 n 次，但不超过 m 次出现 |
| `$` | 匹配行尾 |
| `\0` | 匹配空字符 |
| `\b` | 匹配退格符 |
| `\B` | 匹配不在单词开头或结尾的任意字符 |
| `\b` | 匹配单词的开头或结尾 —— 当不在括号内时 |
| `\cX` | 匹配 `Ctrl-X`（其中 `X` 是任何字母字符） |
| `\d` | 匹配单个数字 |
| `\D` | 匹配非数字字符 |
| `\f` | 匹配换页符 |
| `\n` | 匹配换行（换行-feed）字符 |
| `\000` | 匹配由数字 `000` 指定的八进制值（其中每个 `0` 是 0 到 7 之间的数字） |
| `\r` | 匹配回车 |
| `\s` | 匹配非空白字符 |
| `\S` | 匹配空白字符（空格、制表符或换行符） |
| `\t` | 匹配制表符 |
| `\W` | 匹配非字母数字字符 |
| `\w` | 匹配字母数字字符 |
| `\xhh` | 匹配由数字 `hh` 指定的十六进制值（其中每个 `h` 是 0 到 `f` 之间的数字） |
| `^` | 匹配行首 |

如果你想匹配字符 `\$`、`!`、`*`、`^`、`[`、`]`、`\` 和 `/` 中的任意一个，必须在你想匹配的字符前放置反斜杠。因此，你将输入这些字符为 `\$`、`!`、`*`、`^`、`[`、`]`、`\` 和 `/`。正则表达式看起来往往令人困惑，因为其中有大量奇怪的字符序列以及大量使用的反斜杠。不过，和其他事物一样，你可以从慢开始，初期只使用其中一些功能。

到目前为止，我已经总结了正则表达式的语法。但我还没有展示如何在 Perl 中使用正则表达式。通常，你将正则表达式放在一对斜杠之间，并使用匹配（`=~`）或不匹配（`!~`）运算符来测试字符串。你可以编写一个 Perl 脚本，执行与本节早些时候使用 `grep` 进行的相同搜索。请遵循以下步骤以完成此任务：

1. **使用文本编辑器输入并将以下脚本保存为名为 `lookup` 的文件：**

```perl
#!/usr/bin/perl

while (<STDIN>)
{
   if ( $_ =~ /([Ll]inux/) ) { print $_; }
}
```

2. **使用以下命令使 `lookup` 文件可执行：**

```bash
chmod +x lookup
```

3. **使用以下命令尝试该脚本：**

```bash
cat /usr/include/*.h | ./lookup
```

在这种情况下，`cat` 命令将特定文件的内容（正如你在 `grep` 示例中得知的那样，该文件包含一些符合正则表达式的行）传递给 `lookup` 脚本。该脚本简单地应用 Perl 的正则表达式匹配运算符（`=~`）并打印任何匹配的行。输出类似于使用以下命令时 `grep` 命令显示的内容：

```bash
grep "[Ll]inux" /usr/include/*.h
```

`lookup` 脚本中的 `$_` 变量需要一些解释。`<STDIN>` 表达式从标准输入获取一行，默认情况下将该行存储在 `$_` 变量中。在 `while` 循环内部，正则表达式将与 `$_` 字符串进行匹配。以下单个 Perl 语句完成了 `lookup` 脚本的工作：

```perl
if ( $_ =~ /([Ll]inux/) ) { print $_; }
```

此示例说明了你如何使用正则表达式来搜索字符串在文件中的出现位置。

使用正则表达式一段时间后，你会更好地体会到它们的强大功能。诀窍在于找到能执行你所需任务的正则表达式。例如，这里有一个搜索，查找所有以恰好七个空格开头并以右括号结尾的行：

```perl
while (<STDIN>) {
  if ( $_ =~ /^\s*\)\s*$/ ) { print $_; }
}
```

## 流程控制语句

到目前为止，你看到的 Perl 语句都是按串行方式执行的，即一个接一个。Perl 还包含一些语句，使你可以控制语句的执行流程。你已经看到了 *if* 语句和 *while* 循环。Perl 包含了一套完整的流程控制语句，就像 C 语言中的那些一样，但增加了一些额外功能。

在 Perl 中，所有条件语句采用以下形式：

```
conditional-statement
{ 如果条件为真则执行的 Perl 代码 }
```

请注意，必须用大括号（`{...}`）括起来条件语句之后的代码。条件语句检查表达式的值，以决定执行大括号内的代码。在 Perl 中，与 C 语言一样，任何非零值在逻辑上被视为真，而零值被视为假。

接下来，我简要描述 Perl 中主要条件语句的语法。

### *if* 和 *unless*

Perl 的 *if* 语句类似于 C 语言的 *if* 语句。例如，*if* 语句可以检查一个计数值，看该计数值是否超过阈值，如下所示：

```
if ($count > 25) { print "Too many errors!\n"; }
```

你可以像这样在 *if* 语句中添加 *else* 子句：

```
if ($user eq "root") {
  print "Starting simulation...\n";
}
else
{
  print "Sorry $user, you must be \root\ to run this program.\n";
  exit;
}
```

如果你熟悉 C 语言，你会发现 Perl 的语法看起来与 C 非常相似。**if** 语句的条件可以有零个或多个 **elsif** 子句来处理更多的替代方案，如下所示：

```
print "Enter version number:";  # 提示用户输入版本号
$os_version = <STDIN>;      # 从标准输入读取
chop $os_version; # 去掉行末尾的换行符
# 检查版本号
if ($os_version >= 10 ) { print "No upgrade necessary\n";}
elsif ($os_version >= 6 && $os_version < 6) { print "Standard upgrade\n";}
elsif ($os_version > 3 && $os_version < 6) { print "Reinstall\n";}
else { print "Sorry, cannot upgrade\n";}
```

**unless** 语句是 Perl 独有的。该语句的形式与 **if** 相同，包括使用 **elsif** 和 **else** 子句。区别在于，**unless** 只在条件为假时执行其语句块。例如，你可以使用以下代码中的 **unless**：

```
unless ($user eq "root")
{
    print "You must be \"root\" to run this program.\n";
    exit;
}
```



在这种情况下，除非字符串 `user` 是 `root`，否则脚本将退出。

## while

使用 Perl 的 `while` 语句进行 `循环`——即重复处理，直到现有条件在逻辑上变为假。要从标准输入逐行读取并处理该行，你可以使用以下 `while` 循环：

```
while ($in = <STDIN>)
{
    # 处理该行的代码
    print $in;
}
```

如果你从标准输入读取且没有参数，Perl 会将标准输入的当前行赋值给 `$_` 变量。因此，你可以将上述 `while` 循环写成如下形式：

```
while (<STDIN>)
{
    # 处理该行的代码
    print $_;
}
```

Perl 的 `while` 语句比 C 语言的更灵活，因为你可以使用几乎任何东西作为要测试的条件。例如，如果使用数组作为条件，`while` 循环将执行直到数组中没有剩余元素为止，如下面的示例所示：

```
# 假设 @cmd_arg 包含当前的一组命令参数
while (@cmd_arg)
{
    $arg = shift @cmd_arg; # 这提取一个参数
    # 处理当前参数的代码
    print $arg;
}
```

`shift` 函数移除数组的第一个元素并返回该元素。

你可以使用 `next` 关键字跳过循环的末尾；`last` 关键字退出循环。例如，下面的 `while` 循环将 1 到 10 的数字相加，但跳过 5：

```
while (1)
{
    $i++;
    if($i == 5) { next;} # 如果 $i 是 5，则跳转到下一次迭代
    if($i > 10) { last;} # 当 $i 超过 10 时，结束循环
    $sum += $i;       # 添加数字
}
# 在此处 $sum 应该是 50
```

## for 和 foreach

Perl 和 C 的 `for` 语句具有相似的语法。使用 `for` 语句根据表达式的值执行语句任意次。语法如下：

```
for (expr_1; expr_2; expr_3) { statement block }
```

`expr_1` 在循环开始时评估一次；语句块执行直到 `expr_2` 评估为零。第三个表达式，`expr_3`，在语句块每次执行后评估。你可以省略任何表达式，但必须包含分号。此外，语句块周围的大括号是必需的。下面是一个使用 `for` 循环将 1 到 10 的数字相加的示例：

```
for ($i=0, $sum=0; $i <= 10; $sum += $i, $i++) { }
```

在此示例中，添加数字的实际工作在第三个表达式中完成，而 `for` 循环控制的语句是一个空块（{}）。

`foreach` 语句最适合数组。下面是其语法：

```
foreach Variable (Array) { statement block }
```

`foreach` 语句将 `Array` 中的一个元素赋值给 `Variable` 并执行语句块。`foreach` 语句重复此过程，直到没有数组元素剩余。下面的 `foreach` 语句将 1 到 10 的数字相加：

```
foreach $i (1..10) { $sum += $i; }
```

请注意，我使用范围运算符（`..`）来声明数组。你还可以使用逗号分隔的项目列表作为数组。

如果在 `foreach` 语句中省略 `Variable`，Perl 会隐式使用 `$_` 变量来存储当前数组元素。因此，你可以使用以下代码：

```
foreach (1..10) { $sum += $_; }
```

## goto

`goto` 语句使 Perl 跳转到由标签标识的语句。这里有一个示例，提示用户输入一个值，如果该值不可接受，则重复请求：

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

## 访问 Linux 命令

你可以通过多种方式从 Perl 执行任何 Linux 命令：

- 调用 `system` 函数，传入一个包含你要执行的 Linux 命令的字符串。
- 将 Linux 命令包含在反引号（`` ` ``）中，这些也称为 `重音符`。你可以这样运行 Linux 命令并捕获其输出。
- 调用 `fork` 函数来复制当前脚本，并在子进程中处理新命令。（如果一个进程启动另一个进程，新的那个被称为 `子` 进程。）

## 进程管理

- 调用 `exec` 函数，用新脚本或 Linux 命令覆盖当前脚本。
- 使用 `fork` 和 `exec` 来实现类似 shell 的行为。（监视用户输入，并通过子进程处理每个用户输入的命令。）本节中，我将给出一个简单的示例，说明如何完成此任务。

在脚本中执行 Linux 命令最简单的方法是使用 `system` 函数，并将命令作为字符串传入。`system` 函数返回后，该命令的退出码会存储在 `$?` 变量中。你可以轻松编写一个简单的 Perl 脚本，从标准输入读取字符串，并使用 `system` 函数处理该字符串。请按照以下步骤操作：

1. 使用文本编辑器输入并保存以下脚本到一个名为 `rcmd.pl` 的文件中：

```perl
#!/usr/bin/perl
# Read user input and process command
$prompt = "Command (\"exit\" to quit) : ";
print $prompt;
while (<STDIN>)
{
    chomp;
    if ($_ eq "exit") { exit 0;}
    # Execute command by calling system
    system $_;
    unless ($? == 0) { print "Error executing: $_\n";}
    print $prompt;
}
```

2. 使用以下命令使 `rcmd.pl` 文件可执行：

```bash
chmod +x rcmd.pl
```

3. 在 shell 提示符下输入 `./rcmd.pl` 来运行该脚本。

以下是 `rcmd.pl` 脚本的示例输出。（输出取决于你输入的命令）

```text
Command ("exit" to quit): ps
  PID TTY          TIME CMD
 3128 pts/2    00:00:00 bash
 3314 pts/2    00:00:00 rcmd.pl
 3315 pts/2    00:00:00 ps
Command ("exit" to quit): exit
```

你可以在 Perl 脚本中使用 `fork` 和 `exec` 来运行 Linux 命令。下面是一个示例脚本 —— `psh.pl` —— 它使用 `fork` 和 `exec` 来执行用户输入的命令：

```perl
#!/usr/bin/perl
# This is a simple script that uses "fork" and "exec" to
# run a command entered by the user
$prompt = "Command (\"exit\" to quit): ";
print $prompt;
while (<STDIN>)
{
    chomp;  # remove trailing newline
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



以下示例输出展示了 `psh.pl` 脚本如何执行 `ps` 命令：

| 命令（输入"exit"退出）：ps | PID | TTY | TIME | CMD |
| :--- | :--- | :--- | :--- | :--- |
| 3128 | pts/2 | 00:00:00 | bash | |
| 3321 | pts/2 | 00:00:00 | psh.pl | |
| 3322 | pts/2 | 00:00:00 | ps | |
| 命令（输入"exit"退出）：exit | | | | |

Shell（如 `bash`）使用 `fork` 和 `exec` 的组合来执行命令。

## 文件访问

你可能已经注意到本章各种示例中使用的 `<STDIN>` 表达式。这是 Perl 从文件读取数据的方式。在 Perl 中，文件句柄（也称为*标识符*）在读取文件时赋予文件独特的标识。通常，文件句柄使用大写字符。`STDIN` 是一个预定义的文件句柄，表示标准输入——默认情况下是键盘。`STDOUT` 和 `STDERR` 是另外两个预定义的文件句柄。`STDOUT` 用于打印到终端，而 `STDERR` 用于打印错误消息。

![](img/792720823146d68f19fd50c99ebfce4b_785_0.png)

要从文件中读取，请将文件句柄写在尖括号（`<>`）内。因此，`<STDIN>` 从标准输入读取一行。

你可以使用 `open` 函数打开其他文件。以下示例展示了如何打开 `/etc/passwd` 文件进行读取，以及如何显示该文件中的行：

```perl
open (PWDILE, "/etc/passwd"); # PWDILE is the file handle

while (<PWDILE>) { print $_;} # By default, input line is in $_

close PWDILE;                # Close the file
```

默认情况下，`open` 函数以读取模式打开文件。你可以在文件名前添加特殊字符来表示其他类型的访问。`>` 前缀以写入模式打开文件，而 `>>` 前缀以追加模式打开文件。下面是一个简短的脚本，它读取 `/etc/passwd` 文件并创建一个名为 `output` 的新文件，其中包含所有没有真实 shell 的用户列表。（这些用户的密码条目在每行末尾都有 `/bin/false`。）

```perl
#!/usr/bin/perl

# Read /etc/passwd and create list of users without any
# shell
open (PWDILE, "/etc/passwd");
open (RESULT, ">output");       # Open file for writing
while (<PWDILE>)
{
    if ($_ =~ /:/bin\\/false\n/) {print RESULT $_;}
}
close PWDILE;
close RESULT;
```

执行此脚本后，你会在当前目录中找到一个名为 `output` 的文件。

### 带管道前缀的文件名

一个有趣的文件名前缀是*管道字符* —— 竖线（`|`）。如果你调用 `open` 时使用以 `|` 开头的文件名，文件名的其余部分将被视为一个命令。Perl 解释器执行该命令，你可以使用 `print` 调用向该命令发送输入。下面的 Perl 脚本使用 `mail` 命令向一组用户发送邮件消息：

```perl
#!/usr/bin/perl

# Send mail to a list of users
foreach ("root", "naba")
{
    open (MAILPIPE, "| mail -s Greetings $_");
    print MAILPIPE "Remember to send in your weekly report today!\n";
    close MAILPIPE;
}
```

如果文件名以管道字符（`|`）结尾，则该文件名作为一个命令执行；你可以使用尖括号（`<...>`）读取该命令的输出，如下例所示：

```perl
open (PSPIPE, "ps ax | ");
while (<PSPIPE>)
{
# Process the output of the ps command
# This example simply echoes each line
print $_;
}
```

## 子程序

尽管 Perl 包含大量内置函数，但你可以通过*子程序*的形式添加自己的代码模块。事实上，Perl 自带了一大套这种程序中的程序。这里有一个简单的脚本，说明了 Perl 中子程序的语法：

```perl
#!/usr/bin/perl
sub hello
{
# Make local copies of the arguments from the @_ array
local ($first,$last) = @_;
print "Hello, $first $last\n";
}
$a = Jane;
$b = Doe;
&hello($a, $b);# Call the subroutine
```

当你运行前面的脚本时，它会显示以下输出：

```text
Hello, Jane Doe
```

请注意关于子程序的以下几点：

- 子程序在数组 `@_`（at 符号，后跟下划线字符）中接收其参数。
- 子程序中使用的变量默认是全局的。使用 `local` 函数创建一组局部变量。
- 通过在子程序名称前加上 ampersand（`&`）来调用子程序。因此，通过输入 `&hello` 来调用 `hello` 子程序。

如果需要，你可以将子程序放在自己的文件中。例如，`hello` 子程序可以放在名为 `hello.pl` 的文件中。当你将子程序放在文件中时，请记住在文件末尾添加一个返回值——只需在末尾输入 `1;` 以返回 1。因此，`hello.pl` 文件如下所示：

```perl
sub hello
{
# Make local copies of the arguments from the @_ array
local ($first,$last) = @_;
print "Hello, $first $last\n";
}
1;    # return value
```

然后，你必须编写使用该 `hello` 子程序的脚本，如下所示：

```perl
#!/usr/bin/perl
require 'hello.pl';  # include the file with the
    subroutine
$a = Jane;
$b = Doe;
&hello($a, $b);    # Call the subroutine
```

此脚本使用 `require` 函数来包含 `hello.pl` 文件，该文件包含 `hello` 子程序的定义。

## Perl 中的内置函数

Perl 有大约 200 个内置函数（也称为*Perl 函数*），包括类似 C 运行时库中的函数，以及访问操作系统的函数。你确实需要浏览函数列表，才能欣赏 Perl 中可用功能的广度。我没有足够的空间在这本书中涵盖这些函数，但你可以通过将 Web 浏览器指向以下地址来了解 Perl 内置函数：

```text
http://perldoc.perl.org/index-functions.html
```



# Perl 包和模块

此地址将把你连接到 Perl 文档站点上的 Perl Functions 页面，以便你可以浏览 Perl 内置函数的概述。在该页面上，点击函数名称以查看有关该函数的更详细信息。

## 理解 Perl 包和模块

Perl 包是一种将数据和子程序组合在一起的方法。本质上，它是一种使用变量和子程序名称的方法，而不会与程序中其他部分使用的任何名称冲突。包的概念自 Perl 版本 4 起就已存在。

包提供了一种控制命名空间的方法——该术语指的是变量和子程序名称的集合。尽管你可能没有意识到，当你编写 Perl 程序时，它自动属于一个名为 `main` 的包。除了 `main` 之外，其他 Perl 包位于 Perl 库中，在你的 Linux 系统的 `/usr/lib/perl5` 目录中，你也可以定义自己的包。

Perl 模块是遵循特定指南的包。

## Perl 包

你可以将 Perl 包视为组织一组相关 Perl 子程序的便捷方式。另一个好处是，在包中定义的变量和子程序名称不会与程序其他位置使用的名称冲突。因此，在一个包中名为 `$count` 的变量对该包是唯一的，不会与 Perl 程序中其他地方使用的 `$count` 发生冲突。

一个 Perl 包位于单个文件中。`package` 语句用于文件开头，以声明该文件为一个包并给包命名。例如，文件 `ctime.pl` 在名为 `ctime` 的包中定义了一系列子程序和变量。`ctime.pl` 文件在多处包含以下包声明语句：

```perl
package ctime;
```

此包声明的效果是，其后所有的变量名和子程序名都被视为属于 `ctime` 包。你可以将这样的 `package` 语句放在实现该包的文件开头。

如果你实现了某个包，并且需要引用另一个包中的子程序或变量怎么办？正如你可能猜测的那样，你只需同时指定包名和变量或子程序名即可。Perl 提供了以下语法来引用其他包中的变量：

```perl
$Package::Variable
```

这里 `Package` 是包名，`Variable` 是该包中变量的名称。如果你省略包名，Perl 默认你引用的是主包中的变量。请注意，C++ 在引用另一个 C++ 类中的变量时恰好也使用类似的语法。类基本上是一个数据和函数的集合——即对象的模板。

要在你的程序中使用包，你只需调用 `require` 函数，并将包的文件名作为参数即可。例如，名为 `ctime` 的包在文件 `ctime.pl` 中定义。该包包含一个 `ctime` 子程序，它将二进制时间转换为字符串。以下简单程序使用了来自 `ctime.pl` 文件的 `ctime` 包：

```perl
#!/usr/bin/perl -w

# 使用 ctime.pl 文件中定义的 ctime 包
require 'ctime.pl';

# 调用 ctime 子程序
$Time = ctime(time());

# 打印时间字符串
print $Time;
```

正如你所见，该程序使用 `require` 函数将 `ctime.pl` 文件引入程序中。当你运行此程序时，它会按以下示例输出格式打印当前的日期和时间：

```text
Sat  Sep  3 19:04:34  2005
```

请注意，此脚本的第一行使用了 `-w` 选项。该选项会导致 Perl 解释器打印关于 Perl 脚本中任何不良构造的警告消息。在调用 Perl 解释器的行中包含 `-w` 选项是个好主意。

![](img/792720823146d68f19fd50c99ebfce4b_790_0.png)

如果你想在不实际运行 Perl 程序的情况下检查其语法，请使用 `-c` 选项运行 Perl 解释器，如下所示。`filename` 是你想要检查语法的 Perl 程序的名称。

```bash
perl -c filename
```

### Perl 模块

Perl 5 将包的概念向前推进一步，引入了模块，即遵循特定准则且设计为可重用的包。每个模块都是一个包，定义在与其包名相同但扩展名为 `.pm` 的文件中。每个 Perl 对象都实现为一个模块。例如，CGI 对象用于 Web 服务器，实现为 CGI 模块，存储在名为 `CGI.pm` 的文件中。

如今，Perl 自带许多模块。你可以在 `/usr/lib/perl5` 目录以及 `/usr/share/perl/x.y.z` 目录中找到这些模块，其中 `x.y.z` 是 Perl 版本号。在这些目录中，查找文件名以 `.pm` 结尾的文件，代表 Perl 模块。

### 使用模块

你可以调用 `require` 函数或 `use` 函数，将 Perl 模块包含在你的程序中。例如，名为 `Cwd` 的 Perl 模块，如预期，定义在 `Cwd.pm` 文件中，提供了一个 `getcwd` 子程序，用于返回当前目录。你可以调用 `require` 函数来包含 Cwd 模块，并像下面这样调用 `getcwd`：

```perl
require Cwd;  # 你不需要完整的文件名
$curdir = Cwd::getcwd();
print "Current directory = $curdir\n";
```

第一行将 `Cwd.pm` 文件引入此程序中——你不需要指定完整的文件名；`require` 函数会自动在模块名称后附加 `.pm` 以确定要包含哪个文件。第二行展示了如何调用 Cwd 模块中的子程序。当你使用 `require` 包含模块时，你必须使用 `Module::subroutine` 格式来调用每个子程序。

如果你用 `use` 函数代替 `require` 重写这个示例程序，其形式如下：

```perl
use Cwd;
$curdir = getcwd(); # 无需 Cwd:: 前缀
print "Current directory = $curdir\n";
```



最显著的差异是，你不再需要用模块名称前缀（如 `Cwd::`）来限定子程序名称。

你可以调用 `require` 或 `use` 来将模块包含到你的程序中。当你使用这些函数时，请记住以下细微差别：

- 当你通过调用 `require` 包含模块时，模块仅在程序运行期间调用 `require` 函数时才会被包含。你必须使用 `Module::subroutine` 语法来调用通过 `require` 函数包含的模块中的任何子程序。
- 当你通过调用 `use` 包含模块时，模块会在处理 `use` 语句时立即被包含在程序中。因此，你可以像访问程序自身的一部分那样调用模块中的子程序和变量。你不需要使用 `Module::` 前缀来限定子程序和变量名称。

![](img/792720823146d68f19fd50c99ebfce4b_791_0.png)

你可能希望坚持使用 `use` `Module;` 语法来在程序中包含模块，因为这种语法允许你在调用模块中的子程序时使用更简单的语法。

# 在 Perl 中使用对象

对象是数据结构以及操作该数据的函数的结合。每个对象都是定义对象类型的类的实例。例如，矩形类可能包含矩形的四个角作为数据，以及诸如计算矩形面积的函数和绘制矩形的函数等。那么，每个矩形对象都可以是矩形类的实例，其四个角具有不同的坐标。从这个意义上说，对象是类的实例。

实现对象数据操作的函数（或子程序）被称为方法。这是从 Smalltalk（最早的对象导向编程语言之一）借用的术语。

类还暗示了继承的概念。你可以通过扩展现有类的数据或方法（或两者兼有）来定义新的对象类。继承的一种常见用途是表达各类对象之间的“是一种”（IS A）关系。例如，考虑几何形状。因为圆*是*一种形状，矩形*是*一种形状，所以可以说圆类和矩形类继承自形状类。在这种情况下，形状类被称为父类或基类。

![](img/792720823146d68f19fd50c99ebfce4b_792_0.png)

*面向对象的编程*的基本思想是，你可以将对象的数据和相关方法（子程序）打包在一起，使其像一个*黑箱*一样工作——输入产生输出，而你无需指定完成任务的所有细节。程序员仅通过公开的方法访问对象，而无需了解方法的内部工作原理。通常，程序员可以创建对象，调用其方法以获取或设置属性（这是对象数据的另一个名称），并销毁对象。在本节中，我将展示如何在 Perl 中使用对象。掌握这些知识后，你可以将对象作为 Perl 程序的构建模块加以利用。

## 理解 Perl 对象

Perl 通过使用模块来实现对象，这些模块将数据和子程序封装在一个文件中。Perl 提供了以下简单的对象模型：

- 一个*对象*由一个引用表示。（对象被实现为对哈希的引用。）
- 一个*类*是一个 Perl 模块，提供用于处理对象的方法。
- 一个*方法*是一个 Perl 子程序，它期望将对象引用作为第一个参数。

对象实现者必须遵循某些规则，并在代表类的模块中提供某些方法。然而，你在使用 Perl 程序中的对象时，实际上不需要太多了解对象的实现细节。就实用目的而言，你只需要知道使用对象时需要遵循的步骤。

### 创建和访问 Perl 对象

一个特别有用的 Perl 对象是 `Shell` 对象，它由 Perl 模块 `Shell.pm` 实现。该模块随 Perl 分发版本提供，位于 `/usr/share/perl/5.8.6` 目录中（针对 Perl 版本 5.8.6）。

顾名思义，`Shell` 对象旨在从 Perl 脚本内部运行 shell 命令。你可以创建一个 `Shell` 对象并让它执行命令。

## 使用 `Shell` 对象

若要使用 `Shell` 对象，请遵循以下常规步骤：

1. **在程序中包含 `Shell` 模块，请添加以下行：**
   `use Shell;`
   在创建 `Shell` 对象之前必须包含此代码行。

2. **要创建 `Shell` 对象，请使用以下语法：**
   `my $sh = Shell->new;`
   其中 `$sh` 是指向 `Shell` 对象的引用。

3. **使用 `Shell` 对象运行 `Linux` 命令，并通过将输出保存到适当的变量中来捕获任何输出。** 例如，要将 `/usr/share/perl/5.8.6` 目录的目录列表保存到一个名为 `@modules` 的数组中，请编写以下代码：
```perl
@modules = $sh->ls("/usr/lib/perl/5.8.6/*.pm");
```
之后，你可以按照自己的意愿处理这个包含 `Perl` 模块文件名的数组（即 `*.pm` 文件）。例如，若要遍历数组并打印每个字符串，请使用以下 `while` 循环：
```perl
while(@modules) {
    $mod = shift @modules;
    # 对模块名称进行任意处理
    print $mod;
}
```

如何知道调用哪些方法以及按什么顺序调用它们？在使用对象之前，必须阅读该对象的文档。方法名称和方法调用的顺序取决于对象的功能。

## 使用 `English` 模块

`Perl` 包含一些具有特殊名称的变量，例如 `$_`（用于默认参数）和 `$!`（用于对应最后一个错误的错误消息）。在阅读程序时，猜测特殊变量的含义可能很困难。结果是你可能会避免使用在程序中可能很有用的特殊变量。

作为一种有益的功能，`Perl` `5` 提供了 `English` 模块（`English.pm`），该模块允许你使用可理解的名字来引用 `Perl` 中的各种特殊变量。要在 `Perl` 程序中使用 `English` 模块，请在程序中包含以下代码行：

`use English;`

之后，你可以将 `$_` 称为 `$ARG`，将 `$!` 称为 `$ERRNO`。（这些 *English* 名称可能仍然有些晦涩，但肯定比标点符号好得多。）

以下程序使用了 English 模块——并打印了一些有趣的变量：
```perl
#!/usr/bin/perl -w
# 文件: english.pl
use English;
print "Perl 可执行文件 = $EXECUTABLE_NAME\n";
print "脚本名称 = $PROGRAM_NAME\n";
```

使用以下命令运行此脚本：

`./english.pl`

当我运行此脚本时，得到的输出如下：

```
Perl 可执行文件 = /usr/bin/perl
脚本名称 = ./english.pl
```



English 模块非常实用，因为它让你能够编写 Perl 脚本，在脚本中可以使用有意义的名称来引用特殊变量。若要了解有关 Perl 特殊变量及其 English 名称的更多信息，请在终端窗口中输入 `man perlvar` —— 或者，更好的方法是让你的 Web 浏览器指向 `perldoc.perl.org/perlvar.html`

## 附录：关于 DVD

### 本附录内容

- 系统要求
- DVD 安装说明
- DVD 中包含的内容
- 故障排除

本书的配套 DVD 包含七个主要的 Linux 发行版——Debian GNU/Linux、Fedora Core、Knoppix、MEPIS、SUSE、Ubuntu 和 Xandros Desktop OS——以帮助开始你的 Linux 之旅。本附录简要介绍了该 DVD 并告诉你如何开始安装。

### 系统要求

请确保你的计算机满足以下列表中的最低系统要求。如果你的计算机不满足大多数这些要求，你在使用该 DVD 上的软件和文件时可能会遇到问题：

- 处理器运行速度为 400 MHz 或更快的 PC 用于图形安装
- 计算机上至少安装 192MB 总 RAM 用于图形安装（建议 256MB）
- 硬驱动器上至少有 520MB 可用空间用于最小安装；如果你计划安装大多数软件包以体验本书涵盖的所有内容，则建议有 5GB 可用空间
- DVD-ROM 光驱和 CD 刻录机（请参阅第一本书第 2 章了解刻录安装 CD 的说明）
- 能够显示至少 256 种颜色的显卡和显示器
- 声卡
- 以太网网络接口卡（NIC）或速度至少为 56 Kbps 的调制解调器

### DVD 安装说明

要从配套 DVD 安装 Linux 发行版，请遵循这些步骤。（有关详细信息，请参阅第一本书第 2 章。）

1. 在安装 Linux 之前，收集关于你的 PC 硬件的信息，例如显卡、网卡和 SCSI 卡。
2. 使用分区程序，如 PartitionMagic 或 FIPS 程序，在你的硬驱动器上为 Linux 创建空间。
   如果你计划将 Linux 用作你 PC 上唯一的操作系统，或者计划将其安装在空的第二块硬驱动器上，则跳过此步骤。
3. 为你的发行版刻录 CD。（如果你正在安装 Fedora Core，则跳过此步骤。）
   请参阅第一本书第 2 章了解特定于每个发行版的说明。
4. 使用 DVD（用于 Fedora Core 和 Knoppix）或第一张 CD（用于 Debian、MEPIS、SUSE、Ubuntu 和 Xandros）启动你的 PC。

### DVD 中包含的内容

本节概述了你在 DVD 上找到的软件和其他好东西。如果你需要帮助安装 DVD 上提供的各项内容，请回到上一节的安装说明。

共享软件是完全功能正常、免费的版权程序的试用版。如果你喜欢特定的程序，可以支付名义费用向作者注册，并获得许可证、增强版本和技术支持。

免费软件是免费的版权游戏、应用程序和实用工具。你可以将它们复制到尽可能多的 PC 上——免费——但它们不提供技术支持。

软件的试用版、演示版或评估版通常受到时间或功能限制（例如，不让你创建项目后保存它）。

GNU 软件受其自己的许可证约束，该许可证包含在 GNU 软件的文件夹中。对 GNU 软件的分布没有限制。有关详情，请参阅 DVD 根目录或本书背面的 GNU 许可证。按照 GNU 许可证的要求，本书包含 Fedora Core 的源代码。至于 Debian、Knoppix、SUSE 和 Xandros 的源代码，以下是如何从互联网获取每个应用程序源代码的方法：

- **Debian:** 浏览 `www.debian.org/mirror/list` 上的镜像站点列表，并点击离你最近的站点的 URL。
- **Knoppix:** 许多用于 Knoppix 的软件包来自 Debian 项目，其源代码可从 Debian 网站获取。从 `www.knopper.net/download/knoppix` 下载 Knoppix 特定的源代码。
- **MEPIS:** MEPIS 中的大多数软件包来自 Debian 项目，其源代码可从 Debian 网站获取。MEPIS 独特的组件，如 MEPIS OS Center，是专有的，其源代码不可用。
- **SUSE:** 从 `http://ftp.opensuse.org/pub/opensuse/distribution/SL-OSS-stable/inst-source/suse/src/` 服务器下载 SUSE Linux 的源代码软件包。
- **Ubuntu:** 你可以在 `http://archive.ubuntu.com/ubuntu/` 找到 Ubuntu 源代码，其组织方式与 Debian 源代码的组织方式类似。
- **Xandros：** 通过遵循 `www.xandros.com/support/source_code.html` 上的说明，下载 Xandros 免费和开源组件的源代码。

以下命令：`sudo apt-get build-dep packagename`，随后输入 `sudo apt-get source packagename`，其中 `packagename` 是软件包的名称。

DVD 中包含几种不同格式的 Linux 发行版：

- **完整发行版：** 您可以从 DVD 启动并安装完整的发行版。
- **即插即用的 Live CD：** 您可以从 DVD 启动计算机来运行 Live CD。
- **ISO 镜像：** 您需要将 ISO 镜像刻录到 CD 上，然后从这些 CD 进行安装。

以下是 DVD 中包含的 Linux 发行版：

- **Debian：** 以网络安装 ISO 镜像的形式提供。
- **Fedora Core：** 作为完整发行版包含在内。
- **Knoppix：** 作为即插即用的 Live CD 包含在内。
- **MEPIS：** 提供为 Live CD ISO 镜像，同时也充当安装 CD。
- **SUSE：** 提供为单个 Live DVD ISO 镜像文件。
- **Ubuntu：** 提供为单个安装 CD ISO 镜像。
- **Xandros Open Circulation Edition：** 提供为单个 CD ISO 镜像。

### DVD 中您将找到的内容

每种 Linux 发行版的详细软件列表略有不同，但大多数发行版都包含以下内容：

- Linux 内核 `2.6.x`
- 基于 X Window 系统的图形用户界面，带有 GNOME `2.12` 和 KDE `3.4` 图形桌面
- Apache Web 服务器和 Mozilla Firefox Web 浏览器
- Samba `3.0.20` LAN 管理软件
- OpenOffice.org `1.9` 办公套件

### 故障排除

如果您在安装或使用配套 DVD 上的材料时遇到困难，请参阅第一册中详细的安装和故障排除说明。

若要追加订单或获取有关其他威利产品的信息，请致电 `(800) 225-5945`。

# 索引

### 符号

- （星号）通配符，167–168
- `!` FTP 命令，368

### A

- ABI（应用程序二进制接口），与 LSB 相关，15
- Apache Web 服务器
  - 访问控制指令，601–603
  - 配置，589–606

# B

- backups。参见 archives
- bash shell
  - built-in commands，739–742
  - overview，162

# C

- C 语言编程
  - 数组，707–708
  - break 语句，715
  - if-else 语句，718–719

# D

- Debian GNU/Linux 描述，11
  - GNOME 桌面，142–144
  - 安装，42–48

# E

- 电子邮件
  - 附件，316
  - MTA，314
  - MUA，314

# F

- Fedora Core
  - 描述，12
  - 安装，48–57
  - GNOME 桌面，144–146

# G

- GNOME (GNU 对象模型环境)
  - 自定义，119–121
  - Debian 桌面，142–144
  - 简介，20

# H

- 硬盘
  - 安装及，34
  - 编程，674

# I

- Internet
  - 连接，254–256
  - 电子邮件，253

# K

- KDE (K 桌面环境)
  - 简介，20
  - Knoppix，146–150

# L

- Linux
  - 命令，170–173
  - 发行版，10–14

# M

- MEPIS Linux
  - 描述，12
  - 安装，57–60

# N

- NFS（网络文件系统）
  - 描述，279
  - 文件共享，661–665

# O

- OpenOffice.org 办公套件
  - Calc，216–217
  - Writer，215–216

# P

- Perl
  - 描述，23
  - 表达式，746，751–752
  - 流程控制语句，746，755–758

# S

- 安全
  - 框架，建立，500–505
  - 防火墙，509，534–545

# T

- TCP/IP（传输控制协议/互联网协议）
  - 应用层，276
  - 网络层，276

# U

- Ubuntu Linux
  - 描述，13
  - GNOME 桌面，156–158

# X

- Xandros 桌面操作系统
  - 描述，130
  - 安装，73–80

## GNU 通用公共许可证

版本 2，1991 年 6 月

版权所有 © 1989, 1991 自由软件基金会，Inc.

### 前言

大多数软件的许可协议旨在剥夺您分享和修改它们的自由。相比之下，GNU 通用公共许可证旨在保证您分享和修改自由软件——确保软件对所有用户都是自由的。

### 复制、分发和修改的条款与条件

- 0. 本许可证适用于包含版权所有者放置的通知，声明其可依据本通用公共许可证条款进行分发的任何程序或其他作品。
- 1. 你可以以你收到的形式，复制和逐字分发程序的源代码。
- 2. 你可以修改你持有的程序或其任何部分的副本，从而形成基于程序的作品。
- 3. 你可以依据上述第1节和第2节的条款，以目标代码或可执行形式复制和分发程序。
- 4. 除本许可证明确规定的情况外，你不得复制、修改、再许可或分发程序。
- 5. 你无需接受本许可证，因为你未签署它。
- 6. 每次你重新分发程序时，接收者自动从原始许可方获得根据这些条款和条件复制、分发或修改程序的许可证。
- 7. 如果由于法院判决或专利侵权指控，或由于任何其他原因强加给你的条件与本许可证的条件相矛盾，这些条件并不免除你遵守本许可证的条件。
