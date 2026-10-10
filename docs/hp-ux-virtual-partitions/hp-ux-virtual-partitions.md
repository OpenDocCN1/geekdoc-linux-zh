# HP-UX 虚拟化分区


# 前言

## 关于虚拟分区

通过虚拟分区 (vParS)，您可以将几乎任何 HP 9000 服务器转换为多个“虚拟”计算机。这些虚拟计算机中的每一个都可以运行自己实例的 HP-UX 及相关应用程序。虚拟计算机在软件层面彼此隔离。在一个虚拟分区上运行的软件不会影响任何其他虚拟分区中运行的软件。在虚拟分区中，您可以运行不同版本的 HP-UX、不同补丁级别的 HP-UX、不同的应用程序，或任何您想要的软件，而不会影响其他分区。

为了在系统上运行 vParS，必须满足一些基本要求。在撰写本书时，您的系统上每个 vPar 必须满足以下最低要求：

- 最少一个 CPU，
- 足够的内存以运行 HP-UX 以及 vPar 中存在的任何其他软件。
- 一个启动磁盘，用于启动 HP-UX。在撰写本书时，无法在 vParS 之间共享总线适配器。因此，每个 vPar 都需要单独的总线适配器。在您阅读本书时，这一要求可能已被取消。
- 用于管理系统的控制台。控制台可以是物理的，也可以是虚拟的。我们将在书中详细介绍控制台。
- 由 HP-UX 11i 支持的 HP 9000 系统。在撰写本书时，vPars 仅支持 HP-UX 11i。对于基于 Itanium 处理器系列 (IPF) 处理器的系统，计划在未来在 vPars 中支持多种操作系统。

我们在本书大多数示例中使用的系统是一个 L 类系统，满足上述列表中的所有要求。您可能还希望在每个 vPar 中拥有额外的磁盘和单独的 LAN 卡。我强烈建议使用 LAN 卡，以便您可以建立到 vPars 的 TELNET 或其他会话，而不是仅从控制台连接。LAN 卡也是执行备份和 Ignite-UX 相关工作的必需设备。

如果您的服务器上部署了即时容量按需分配 (iCOD)，所有 CPU 必须激活才能使 vPars 正常工作。在 vPar 中部署处理器集 (psets) 时，仅使用绑定的 CPU。

HP-UX 11i 附带有一个捆绑的 vPars 产品，也有完整或附加产品。附加产品很少有限制。捆绑产品限制为最多两个 vPars，且其中一个 vPar 只能有一个 CPU。

本书编写时，虚拟分区软件尚未发布。自本书编写以来，虚拟分区已经进行了许多增强。目前正在考虑为 vPars 引入图形用户界面，但本书未涵盖。对于新产品，仅使用命令行并执行大量手动操作时，能更好地理解产品功能。此外，附录 B 中介绍的 Superdome vPars 软件刚刚作为早期访问软件可用。Superdome 的 vPars 软件操作与本书前面示例中介绍的 L 类和 N 类系统上的软件完全相同。虽然自本书编写以来虚拟分区产品已经精简，但通过我在此介绍的操作，您将对虚拟分区有很好的理解。

我希望您在阅读本书和学习材料时，能像我写它时一样享受这个过程。

Marty Poniatowski

marty_poniatowski@hp.com

## 虚拟分区 (vPars) 背景

HP-UX 虚拟分区 (vPars) 允许您在同一台 HP 9000 服务器上运行多个 HP-UX 实例。从硬件角度来看，vPar 由 CPU、内存和 I/O 组成，它们是计算机整体硬件的一个子集。从软件角度来看，vPar 由 HP-UX 11i 操作系统环境以及成功运行工作负载所需的所有应用程序相关软件组成。图 P-1 展示了 HP 9000 计算机系统资源如何分配以支持多个 vPars 的概念图。

![](img/eff8b9287a5f38c5adf538f24aacf29e_23_0.png)

图 P-1 使用 vParts 的 HP 系统资源分配示例

组成您的 HP 9000 的组件可以以多种方式分配。可以看到，所示的八路系统为每个 vPar 分配了不同数量的处理器、不同容量的内存和不同数量的 I/O 卡。未使用的组件可以添加到任何 vPar，或作为另一个 vPar 的基础。此外，组件可以从一个 vPar 移动到另一个 vPar（本书后文将描述一些限制）。

## 虚拟分区的用途

我参与过许多 vPars 安装项目，它们将 vPars 用于各种用途。以下是使用 vPars 的一些原因示例：

- **提高系统利用率** - 许多服务器利用率低下。使用 vPars，您可以将系统资源的子集分配给每个 vPar。由于每个 vPar 运行自己的 HP-UX 11i 实例及相关应用程序，您将获得更高的整体系统利用率。

- **灵活性** - 许多应用程序的资源需求会变化。使用 vPars，您可以在应用程序需求较低时分配较少的系统组件，在应用程序需要时分配额外资源。例如，月底增加的工作负载可以分配更多的系统资源以更快完成。

- **服务器整合** - 在一台 HP 服务器上运行多个 HP-UX 11i 实例及其相关应用程序，减少了所需的服务器总数。原本运行在不同服务器上的 Web 服务器现在可以在同一计算机的不同 vPars 中运行。

- **应用程序隔离** - HP vPars 在软件层面完全彼此隔离。一个 vPar 中的软件故障不会影响其他 vPars。

- **混合生产、测试和开发** - 使用 vPars，生产和测试可以在同一台服务器上进行。测试完成后，测试 vPar 可以变为生产 vPar。类似地，开发通常在单独的系统上进行。然而，由于 vPars 的软件隔离，开发可以在同一系统上进行，与其他应用程序共存。





这只是我在 vPars 使用中看到的用例的抽样。随着 vPars 的广泛使用以及系统专家在更多计算环境中实现它们，将还会有许多其他用例出现。

## 本书的组织结构

我并未将本书的内容局限于仅涵盖虚拟分区（vPars）相关素材。我涵盖了 HP-UX 11i 系统管理的许多主题以及 vPars 对其产生的影响。然而，这不是一本完整的 HP-UX 11i 系统管理书籍。*HP-UX 11i 系统管理手册与工具包*是一本完整的系统管理指南，您可以考虑将其作为本书的配套读物。它还包含一个 UNIX® 部分以及一个 HP-UX 和 Windows® 互操作性部分。

每一章都以分区特有的信息开头，章节的后半部分则包含有关该主题的背景信息。例如，在介绍启动分区的章节中，我首先涵盖与启动分区特别相关的主题。在章节的后半部分，我介绍一般的启动内容。在介绍与某个主题相关的分区特有信息之后，再介绍同一主题的背景信息，这为您提供成功处理分区所需的大部分知识。

## 相关网址

有许多网站可以协助您进行虚拟分区相关工作以及一般的 HP-UX 系统管理。以下是截至本书写作时一些比较突出的 HP-UX 相关网站：

- IT 资源中心
  - （这对每位 HP-UX 管理员来说都是必不可少的）：
  - http://www.ire.com
- 技术文档，包括大多数 HP-UX 文档：
  - http://www.docs.hp.com
- 软件仓库主页：
  - http://www.software.hp.com
- vPar 产品信息：
  - http://www.hp.com/go/servicecontrol
- vPar 系统管理员指南：
  - http://docs.hp.com/hpux
- 即时按需容量（iCOD）：
  - http://www.hp.com/go/icod
- HP 计算专业人士国际协会：
  - http://www.interex.org
- 可配置的内核参数：
  - http://docs.hp.com/hpux/onedocs/os/KCparams.Overview.All.html
- HP-UX 在线文档索引：
  - http://docs.hp.com/hpux/onedocs/os
- 关于 HP 新架构 Itanium 处理器系列的信息：
  - http://www.IA64.hp.com
- 注册名称服务器：
  - http://www.icann.org/registrars/accredited-list.html
- 优秀的非支持系统管理脚本：
  - ftp://contrib:9unsupp8@hprc.external.hp.com/sysadmin/
- 用于 UNIX 和 Windows 互操作性的软件：
  - http://www.hummingbird.com/products/evals/index.html
- 关于 Perl 的信息，包括下载 Perl 的网站：
  - http://www.perl.com
- 《Perl 期刊》：
  - http://www.tpj.com
- 关于 Gnome 桌面环境的信息：
  - http://www.gnome.org
- 已移植到 HP-UX 的公共领域软件：
  - http://hpx.connect.org.uk
- 致力于管理和推广开源的网站：
  - http://www.opensource.org
- Linux 文档网站：
  - http://www.linuxdoc.org
- 关于在 HP 上运行 Java 的信息：
  - http://www.hp.com/go/java

## 随书提供的手册页

我非常感谢休利特-帕卡德公司允许我在这本书中包含 vPars 手册页以及其他一些精选的手册页。在我之前的书中包含手册页一事，我收到了大量积极的反馈。许多读者发现，在手边没有系统可用于检查命令时，书中包含手册页非常有帮助（显然，很多人在不在办公室时阅读我的书）。

当使用书中包含在线手册页的命令时，边栏中会出现以下信息：

![](img/eff8b9287a5f38c5adf538f24aacf29e_28_0.png)

这是一个“手册页”块，其中包含手册页图标、命令名称（在本例中为 **vparstatus**）以及在线手册页所在章节的编号（在本例中为附录 A）。

## 致谢

参与协助完成本书的人太多，无法逐一列出。因此，我决定正式感谢撰写了本书部分章节以及花时间审阅本书的人。我仍然不确定，是写某样东西花的时间多，还是为了确保已写内容正确而审阅它花的时间多。

### Duane Zitzner

Duane Zitzner 是计算系统总裁兼休利特-帕卡德公司副总裁。Duane 担任本书的高管倡导者和赞助人。他的支持对于帮助获得完成本书所需的资源至关重要。

### 作者 - Marty Poniatowski

Marty 在纽约地区担任休利特-帕卡德公司系统工程师十五年。他已与众多休利特-帕卡德客户合作，涉及许多行业，包括互联网初创公司、金融服务和制造业。Marty 在计算机行业贸易出版物中广泛发表文章。他已经发表了 50 多篇关于各种计算机相关主题的文章。除了本书之外，他还是普伦蒂斯厅（Prentice Hall）另外九本书的作者：Marty 拥有纽约理工学院（Brooklyn, NY）信息系统硕士学位、布里奇波特大学（Bridgeport, CT）管理工程硕士学位，以及罗杰·威廉姆斯大学（Bristol, RI）电气工程学士学位。

### Francis Huang - vPars 专家与审阅者

我真诚感谢位于加利福尼亚州库珀蒂诺（Cupertino, CA）休利特-帕卡德公司的 Francis Huang。Huang 先生撰写了 vPars 的官方 HP 手册，并慷慨地投入大量时间审阅本书各章节中关于 vPars 的部分。

Francis 以前是 HP-UX 系统管理员和 MPE 应用程序员。他目前是在旧金山湾区休利特-帕卡德公司的一名技术作家。他拥有计算机科学学士学位，是加利福尼亚州的持证美容师，并即将开始他作为专业家庭办公整理师的第一份有偿工作。

### Geff Blaha - vPars 专家与审阅者

Blaha 先生参与了多项与 vPars 软件相关的活动，包括：开发基于 Web 的培训；在早期访问计划中作为产品现场审阅的一部分，当时只有少数 HP 安装点在使用该产品；以及与 Ignite-UX 相关的工作，包括书中出现的关于使用 Ignite-UX 和 vPars 的流程。

Geff 审阅了本书中所有关于 vPars 特定部分，并贡献了 vPars Ignite-UX 流程。Geff 是一位 UNIX 支持知识工程师，负责开发 HP-UX 操作系统和内核子系统的培训。Geff 在 20 多年前的洛杉矶开始了他在休利特-帕卡德的职业生涯，担任客户工程师和高级客户工程师，支持实时系统和 HP-UX 系统。他在支持方面的贡献包括在旧金山湾区担任响应中心工程师和世界范围技术专家中心（WTEC）工程师，为 RTE、HP-RT 和 HP-UX 客户提供解决方案。Geff 拥有加州波莫纳理工学院（California State Polytechnic University, Pomona）工程技术学士学位。

### Hayden Brown - vPars 专家

Hayden Brown 是一位 vPars 专家，在发布产品之前，我在所有与 vPars 相关的工作中都主要与他联系。他帮助我克服了许多在处理新产品时必须面对的初期障碍，他的帮助 invaluable。

Hayden 在十多年前带着他的 UNIX 专业知识来到休利特-帕卡德公司。他担任过多种角色，从支持工程师、技术咨询顾问到客户教育讲师，讲授关于网络、HP-UX 管理和 HP-UX 内部结构的课程。过去四年，他一直是电子商务数据中心实验室先进技术中心的成员。他被指派开发并培训 HP 技术咨询顾问和客户关于系统整合策略。策略的一部分是 HP 分区连续体，包括诸如进程资源管理器、工作负载管理器、处理器集和虚拟分区等技术。在过去几年中，Hayden 在 HPWorld 和 InterWorks 上就这些技术发表过论文。作为 vPar 实验室的支持角色，Hayden 撰写了第一篇技术



cal 关于 vPars 的白皮书。并管理 HP 客户在 vPars 上的早期访问计划。通过他与客户和 HP 技术专家的交流，他正在帮助塑造惠普公司内部分区技术的未来。

# 本书中使用的约定

我在书中没有使用大量复杂的符号。以下是我使用的一些简单约定，旨在使示例清晰且文本易于跟随：

- **$ 和 #**
  **HP-UX** 命令提示符。书中发出的每个命令前都有一个命令提示符。通常会使用这两个符号中的一个，或者系统名称通常被用作提示符。
- ***斜体***
  *斜体*用于变量值，以及当提及系统管理管理器 (SAM) 中的功能区域和菜单选项时。
- **粗体 和 " "**
  **粗体**文本是你将要输入的信息，例如在提示符后发出的命令，或运行脚本时输入的信息。有时在解释性文本中也会提到你将输入的信息，并且输入的信息可能出现在引号中。
- **<---**
  当需要进行选择时，此约定指示为示例目的而选定的选项。
- **[ ]**
  方括号表示可选项和命令描述。
- **{ }**
  花括号表示你必须从中选择一个项的列表。
- **|**
  竖线用于分隔选择列表中的项。
- **<Enter>**
  表示已在键盘上按下 "Enter" 键。有时使用 **<Return>** 来表示已按下回车键。

另一个额外的约定是用于命令格式的约定。除非必要，否则我不使用命令格式，因为我不可能像 HP-UX 手册页那样彻底地描述命令。手册页详细说明了所有 HP-UX 命令。以下是我在涵盖命令时使用的格式：

```
form 1    command [option(s)] [arg(s)]
form 2    command [option(s)] [arg(s)]
form n    command [option(s)] [arg(s)]
```

在介绍一个命令时，我试图不要过度陷入细节，但有时为了理解一个命令，必须涵盖许多组件。以下是上面列出的组件的简要描述：

- **form #** - 有时一个命令有许多形式。如果一个命令有多个需要解释的形式，那么我将展示多个形式。
- **command** - 可执行文件的名称。
- **option(s)** - 命令行中可能出现多个选项。
- **cmd_arg(s)** - 命令参数，例如路径名。

## 第 1 章
## 安装 HP-UX 11i 和虚拟分区软件

### 虚拟分区简介

我本只想在本章中涵盖软件加载，但我做不到。尽管加载软件是创建虚拟分区 (vPars) 的第一步，但为了理解 vPars 的概念并选择 vPars 将自其引导的设备，我们必须回顾一些背景知识。

HP-UX 虚拟分区允许你在同一台 HP 9000 服务器上运行多个 HP-UX 实例。从硬件角度来看，vPar 由 CPU、内存和 I/O 组成，这些是计算机整体硬件的子集。从软件角度来看，vPar 由 HP-UX 11i 操作环境以及成功运行工作负载所需的所有应用程序相关软件组成。图 1-1（在本书的其他地方也会出现）展示了 HP 9000 计算机系统资源可以如何分配以支持多个 vPars 的概念图。

![](img/eff8b9287a5f38c5adf538f24aacf29e_35_0.png)

构成你的 HP 9000 的组件可以以多种方式进行分配。你可以看到，所示的八路系统为每个 vPar 分配的处理器数量、内存量和 I/O 卡数量各不相同。未使用的组件可以添加到任何 vPar 中，或者作为另一个 vPar 的基础。此外，组件可以在不同的 vPar 之间移动，但会受到书中后面描述的一些限制。

在本章中，我们最关注的是包含在每个 vPar 中的软件。我们希望最终在每个托管虚拟分区的磁盘上都拥有 HP-UX 11i 和虚拟分区软件。这意味着，如果你有一个系统想要运行两个 vPars，你就必须加载支持完全独立的 HP-UX 11i 实例所需的所有软件。我们将得到一个如图 1-2 所示的系统。

![](img/eff8b9287a5f38c5adf538f24aacf29e_36_0.png)

图 1-2 虚拟分区软件堆栈

图 1-2 中包含许多组件。从底部开始，我们有硬件、固件和虚拟分区监视器（作为第 3 章中引导过程的一部分涵盖）。接下来，我们向上移动到软件组件，其中包括安装在两个不同磁盘上的 HP-UX 11i。在图 1-2 最左侧的两个堆栈中显示了两个 HP-UX 11i 实例。这些操作系统必须加载在将充当虚拟分区引导磁盘的每个磁盘上。

虚拟分区监视器是虚拟分区应用程序的一个组件。没有这个应用程序，两个 HP-UX 11i 实例无法在此系统上同时运行。我们在本章中涵盖虚拟分区应用程序的加载。

在未创建虚拟分区的状态下，我们可以从 *这两个* 磁盘中的 *任一* 个启动 HP-UX，但无法同时运行两者。创建我们的虚拟分区在第 2 章中涵盖。完成此操作后，我们确实可以同时运行两个 HP-UX 11i 实例。创建虚拟分区后，你可以继续加载图 1-2 中显示在 HP-UX 11i 上方的中间件和应用程序。

尽管我们在创建的虚拟分区中涵盖了运行多个 HP-UX 11i 实例，但未来我们不仅限于 HP-UX 11i。在基于 Itanium 处理器家族 (IPF) CPU 的系统上，我们将能够运行其他操作系统。图 1-2 中最右侧的虚拟分区描绘了这种未来的能力。这种能力在本书撰写时并不存在，因此不予涵盖。请留意未来本书的更新版本以涵盖这种能力（一旦其存在出现），并密切关注 *www.hp.com* 获取有关 IPF 和虚拟分区增强功能的最新信息。

在开始加载软件之前，我们需要选择安装软件的设备。下一节将涵盖此主题。

### 选择加载软件的磁盘

关于可以加载操作系统和其他由虚拟分区使用的软件的设备，有一些限制。当你进入创建和操作 vPars 的阶段时，你希望阅读接下来两章详细涵盖硬件的章节：第 2 章涵盖 vPars 的操作，第 5 章涵盖 vPars 和设备。然而，在本节中，我们需要介绍选择加载软件磁盘的基础知识，以便你满足撰写时的限制，并在符合 vPars 要求的磁盘上加载软件。

让我们看一下一个 **ioscan** 输出，该输出显示了系统上的磁盘（**ioscan** 以及之前提到的硬件和 vPars 相关问题，在第 2 章和第 5 章中详细涵盖。）

在本书撰写时，位于本地总线适配器 (LBA) 级别及以下级别的组件专门用于某个分区。这意味着，如果你要在两个不同的 vPars 上加载软件，这些磁盘必须位于两个不同的 LBA 上。让我们简要查看系统上的 LBA 和磁盘，以便选择我们将加载软件的磁盘。如果你需要比这里涵盖的更详细的细节，请参考详细涵盖此主题的章节。另外，请记住，系统布局因型号而异，你需要熟悉你的系统布局，以便确定你系统中组件相对于 LBA 级别的位置。

让我们看一下 L-Class 系统，以查看系统总线适配器 (SBA) 和多个 LBA。

```bash
cvhdcon3:/ # ioscan -f | grep ba

# L-Class
ica   0  0       sba
ba    0  0/0     l4k     CLAIMED   BUS_NEXUS Local PCI Bus Adapter (783)
ba    1  0/1     lba     CLAIMED   BUS_NEXUS Local PCI Bus Adapter (782)
ba    2  0/2     lba     CLAIMED   BUS_NEXUS Local PCI Bus Adapter (782)
ba    3  0/3     lba     CLAIMED   BUS_NEXUS Local PCI Bus Adapter (782)
ba    4  0/4     lba     CLAIMED   BUS_NEXUS Local PCI Bus Adapter (782)
ba    5  0/5     lba     CLAIMED   BUS_NEXUS Local PCI Bus Adapter (782)
ba    6  0/6     lba     CLAIMED   BUS_NEXUS Local PCI Bus Adapter (782)
ba    7  0/9     lba     CLAIMED   BUS_NEXUS Local PCI Bus Adapter (782)
ba    8  0/10    lba     CLAIMED   BUS_NEXUS Local PCI Bus Adapter (782)
ba    9  0/12    lba     CLAIMED   BUS_NEXUS Local PCI Bus Adapter (782)
cvhdcon3:/ #
```

这个 L-Class 只有一个 SBA，如上述列表中所有总线开头的 0 所示，并且 LBA 0.0 上有两个 SCSI 总线。内部磁盘通常在这两个不同的 SCSI 总线上进行镜像。然后还有许多额外的 LBA。现在让我们看看哪些磁盘连接到这个系统，并确定它们与哪个 LBA 相关联。

```bash
cvhdcon3:/ # ioscan -f | grep disk
disk  0  0.0/1.0.1.0.0      mdisk CLAIMED DEVICE HP DVD-ROM 304
mdisk 1  0.0/1.1.0.0       mdisk CLAIMED DEVICE SEAGATE ST373404LC
mdisk 2  0.0/1.2.0.0       mdisk CLAIMED DEVICE SEAGATE ST373404LC
mdisk 3  0.0/2.0.0.0       mdisk CLAIMED DEVICE SEAGATE ST373404LC
mdisk 4  0.0/2.0.0.0       mdisk CLAIMED DEVICE SEAGATE ST373404LC
disk  7  0.0/0.0.8.0.5.0.0 sdisk CLAIMED DEVICE HP AS277A
disk 10 0.0/0.0.8.0.5.0.0.1 sdisk CLAIMED DEVICE HP AS277A
disk 11 0.0/0.0.8.0.5.0.0.2 sdisk CLAIMED DEVICE HP AS277A
disk 12 0.0/0.0.8.0.5.0.0.3 sdisk CLAIMED DEVICE HP AS277A
disk 15 0.0/0.0.8.0.5.0.0.3 sdisk CLAIMED DEVICE HP AS277A
disk 17 0.0/0.0.8.0.5.0.2.0 sdisk CLAIMED DEVICE HP AS277A
```





## 加载软件

本列表首先显示了 DVD-ROM，然后是四个内部磁盘，最后是我们外部存储设备机箱上配置的 14 个逻辑单元（LUNs）。

所有内部磁盘都位于同一 LBA 上，如开头的 0/0 所示。第一个 0 代表 SBA，第二个 0 代表 LBA 0。由于它们与同一个 LBA 相关联，因此这些磁盘必须都属于同一个 vPar。我们有多个 LUN 连接到另外两个 LBA，即 8 和 9。这意味着该系统可能最多有三个 vPar，因为存在连接到三个不同 LBA 的潜在启动卷。

我们可能会在其上加载操作系统和 vPars 软件的两个设备示例是：路径为 0/0/0/1.2.0 的内部磁盘和路径为 0/8/0/0.8.0.5.0.0.0 的设备。使用这些满足独立 LBA 要求的设备，我们现在可以继续加载软件。

本章中非 vPars 专属的部分详细介绍了加载 HP-UX 11i 的过程。如果您之前没有加载过 HP-UX 11i，该章节的内容将帮助您完成在所有用于 vPars 的磁盘上加载 11i 的任务。基于我们之前对磁盘的讨论，我们可能会在路径为 0/0/0/1.2.0 的内部磁盘和路径为 0/8/0/0.8.0.5.0.0.0 的设备上加载 HP-UX 11i。本章的非 vPars 专属部分将指导您完成在目标设备上选择并加载 HP-UX 11i 以及加载 11i 的过程。以下是要在每个将作为 vPar 启动设备的磁盘上执行的步骤列表：

- 安装 HP-UX 11i *运行环境*。
- 在加载 HP-UX 11i 后的首次启动时，使用 **set\_parms** 设置系统参数。
- 下载并安装系统中的选定补丁（在撰写本文时，支持 vPars 需要许多补丁。）
- 安装 vPars 软件。
- 配置 vPars。
- 安装额外软件。

您通常会按照上述顺序加载软件：安装基础 *运行环境*；启动系统并使用 **set\_parms**；加载补丁；安装 vPars 软件；配置 vPars；然后安装并配置所有其他软件。您可能希望查看第 10 章，其中涵盖了 Ignite-UX。其中包含的内容有由 HP vPars 实验室专家编写的用于通过 Ignite-UX 加载 vPars 的程序。如果您正在设置多个 vPars 系统，此程序可以为您节省一些时间。

由于本章的非 vPars 专属部分有关于加载 HP-UX 11i 的详细背景介绍，让我们直接跳到下一节的 vPars 软件加载部分。

### 加载虚拟分区所需的软件

本节涵盖安装虚拟分区软件。我假设您的系统已安装 HP-UX 11i，或者您知道如何安装。如果您尚未在系统上安装 HP-UX 11i，请跳至非 vPars 专属部分，该部分涵盖了 HP-UX 11i 的安装。我们之前也讨论了如何选择作为 vPars 基础并安装 HP-UX 11i 的设备。

请记住，每个您希望运行的虚拟分区都必须加载 HP-UX。例如，如果您想运行两个虚拟分区，如本书中的示例所示，则需要为这两个虚拟分区都加载 HP-UX 11i。关于加载 HP-UX 11i 的过程需要为您希望运行的每个虚拟分区执行。HP-UX 11i 可以从媒体（如 CD-ROM 上的 HP-UX 11i 发行版）或 Ignite-UX 服务器加载。您可以使用任何方法为希望运行的每个虚拟分区加载 HP-UX 11i 和虚拟分区软件。

在撰写本文时，有两个 vPars 产品：一个具有全书覆盖的全部功能的产品，以及一个具有完整产品子集功能且免费的产品。免费产品限制最多两个 vPars，其中一个 vPar 只能有一个 CPU。

购买完整产品（产品编号 T1335AC）时，会提供一个 CD-ROM，其中包含以下组件：

- vPars 软件
- 补丁
- vPars 管理指南
- 小册子
- 用于启动的 WINSTALL 文件

在某个时间点，完整产品将通过标准发行版提供，而不是单独的 CD-ROM。免费产品（在撰写本文时称为 VPARSBASE）可以从 www.software.hp.com 下载。

图 1-3 展示了完整产品 T1335AC 下方显示的软件组件示例。

![](img/eff8b9287a5f38c5adf538f24aacf29e_42_0.png)

图 1-3 加载 vPars 软件的示例

图 1-3 显示了构成 T1335AC 的三个组件：内核、监控程序和运行环境。前面列出的额外组件，即补丁和 WINSTALL，也必须加载以使 vPars 完全运行。

请记住，由于本章使用的 vPars 软件尚未发布，您可能会看到一些不同的产品编号。

加载此软件后，系统将重新启动以构建内核。这是自动为您完成的；vPars 内核相关背景在第 2 章和第 4 章中均有介绍。

所有 vPars 软件必须加载到将在 vPars 服务器上使用的每个 HP-UX 11i 卷上。此软件的加载将在您希望在 vPars 服务器上同时运行的每个 HP-UX 11i 实例上进行。有两种方法可以将 HP-UX 11i 操作系统和 vPars 软件加载到所有用于 vPars 的卷上。第一种，也是全书使用的方法，是在创建虚拟分区之前将 HP-UX 11i 和 vPars 软件加载到所有 vPars 卷上。第二种是仅将第一个 vPar 的卷加载所有软件，创建任意数量的 vPars，然后使用 `vparboot -v vp_name -l ignore_kernel` 启动并在其他磁盘上加载 HP-UX 11i。在本章中，我在创建 vPars 之前先在所有磁盘上加载 HP-UX 11i 和 vPars 软件。由于加载了 vPars 软件，大量软件已被加载。/sbin 目录中包含我们将在后续章节中使用的 `vpar` 命令。以下是 /sbin 中 `vpar` 命令的长列表。

```
# ll /sbin/vpar*
-rXr-xr-X    1 bin     bin     128760 Oct 18 22:08 /sbin/vparboot
-rXr-xr-X    1 bin     bin     561236 Oct 18 22:07 /sbin/vparcreate
-rXr-xr-X    1 bin     bin     101040 Oct 18 22:04 /sbin/vpard
-rXr-xr-X    1 bin     bin     559592 Oct 18 22:04 /sbin/vpardump
-rXr-xr-X    1 bin     bin     30920 Oct 18 22:04 /sbin/vparesxtract
-rXr-xr-X    1 bin     bin     140072 Oct 18 22:08 /sbin/vparemmodify
-rXr-xr-X    1 bin     bin     47232 Oct 18 22:04 /sbin/vparreloc
-rXr-xr-X    1 bin     bin     127808 Oct 18 22:08 /sbin/vparremove
-rXr-xr-X    1 bin     bin     132008 Oct 18 22:13 /sbin/vparstate
-rXr-xr-X    1 bin     bin     152040 Oct 18 22:13 /sbin/vparstatus
-rXr-xr-X    1 bin     bin     26152 Oct 18 22:14 /sbin/vparutil
#
```

这些是您用于创建、查看、修改以及通常处理 vPars 的命令。第 2 章专门用于描述这些命令并提供使用它们大多数形式的示例。此外，随书附带的撕页卡片总结了这些命令中的许多。

/stand 中有几个与 vPars 内核相关的文件。以下列表显示了其中一些：

```
# ll /stand/vp*
-ww------    1 root    root      8232 Nov  8  7:09 /stand/vpdb
-rXr-xr-X    1 bin     bin       849992 Oct  5 23:18 /stand/vpmon
#
```

**vpmon** 在系统启动时加载，是运行 vPars 的基础。第 3 章详细涵盖了启动过程，包括启动 **vpmon**。**vpdb** 是包含系统中所有运行 vPars 相关信息的 vPars 数据库。此文件由 vPars 应用程序自动同步，以确保所有 vPars 拥有关于系统中所有 vPars 的相同信息。

有几个与启动相关的文件，包括下面显示的文件，它们在涵盖启动过程的第 8 章中有更详细的介绍。





/etc/rc.config.d/vpqstd
/etc/rc.config.d/vparhb
/etc/rc.config.d/vparinit

/sbin/init.d/vpard
/sbin/init.d/vparhb
/sbin/init.d/vparinit

第 8 章详细涵盖了这些文件，该章节也详细说明了 vPar 的启动过程。其中特别值得关注的是 **vparhp**，它是与保持所有 vPar 上的 **vpdh** 同步相关的心跳守护进程。

对于与 vPar 相关的工作，在线手册页（man pages）非常重要。以下列表显示了在撰写本文时我系统上加载的手册页。

```
# man -k vpar
vparboot (1M)           - boot a virtual partition
vparcreate (1M)         - create a virtual partition
vpardump (1M)           - manage monitor dump files
vparextract (1M)        - extract memory images from a running virtual
                          partition system
vparmodify (1M)         - modify the attributes of a virtual partition
vparreloc (1M)          - relocate the load address of a vmunix file,
                          determine if a vmunix file is relocatable,
                          or promote the scope of symbols in a
                          relocatable vmunix file
vparremove (1M)         - remove a virtual partition
vparreset (1M)          - reset a virtual partition
vparresources (5)       - description of virtual partition resources
                          and their requirements
vparstatus (1M)         - display information about one or more
                          virtual partitions
vpartition (1)          - display information about the Virtual
                          Partition Command Line Interface
vparutil (1M)           - get and set SCSI parameters for SCSI
                          controllers from a virtual partition
```

其中许多手册页出现在附录 A 中，因此在本书阅读各章节时可以参考它们。

至此，我们已经在系统上安装了 HP-UX 11i 和虚拟分区软件。在下一章中，我们将配置虚拟分区，这将允许我们在同一台服务器上同时运行多个 HP-UX 11i 实例。

本章的其余部分涵盖了与安装 HP-UX 11i 相关的背景知识。对于您希望同时在 vPar 服务器上运行的每一个 HP-UX 11i，都需要在一个卷上完成此操作。这是一个逐步执行的程序，因此如果您从未安装过 HP-UX 11i，该程序将引导您从头到尾完成整个过程。

## 非 vPar 专属章节 - 安装 HP-UX 11i 操作系统环境

安装 HP-UX 意味着安装 11i 操作系统环境之一，并随后通过安装 HP 和非 HP 应用程序来构建完整的、功能齐全的 HP-UX 系统。初始系统从 11i 介质加载，或者通过网络上的另一台系统使用 Ignite-UX 加载。本章涵盖了从介质安装的内容。Ignite-UX 章节涵盖了从服务器安装的内容。如果您目前系统中尚未加载 HP-UX 11i，请完成此过程，然后加载前文所述的虚拟分区软件。

您的系统可以以即时点火（instant ignition）的形式交付，这意味着 HP-UX 已安装在您的系统上，您只需添加所需的应用软件即可。我涵盖了从介质开始的完整安装过程，以便您可以看到从头到尾的流程。如果您的系统具有即时点火功能，您未来可能需要安装额外的软件，因此可以使用本节描述的一些技术来加载这些软件。

迁移任何版本的 11.x 操作系统（包括 11i）的特性之一是选择利用 64 位计算。以前的 HP-UX 版本仅支持 32 位处理器，而在 11.x 中，您可以选择运行 32 位或 64 位版本。您选择哪个版本的操作系统取决于两件事：您使用的硬件以及您的应用程序需求。64 位版本并不支持某些 700 系列工作站和许多低端 800 系列，但对于 L 类、N 类、V 类和 Superdome 服务器，它是必需的。在其他 800 系列中，最值得注意的是 K 类和 T 类服务器，您可以选择安装 32 位或 64 位版本。但如果您不确定您的硬件是否支持 64 位，也不必过于担心。如果您的硬件不支持 64 位版本，系统不会提示您选择安装哪个版本。32 位版本将自动安装。如果您可以选择安装 32 位或 64 位版本，那么您的硬件支持其中任意一种。

您的应用程序需求也将有助于确定您是安装 32 位还是 64 位操作系统。如果您的应用程序是 32 位的，那么您确实没有理由运行 64 位版本。但是，如果您将运行 64 位应用程序，那么显然您需要安装 64 位操作系统。好消息是，如果您安装了 32 位操作系统，然后发现您想安装的应用程序是 64 位的，您可以升级到 64 位操作系统，当然，前提条件是您的硬件也支持它。

### 启动系统和“高级安装”

为了安装 HP-UX 软件，请将 HP-UX 11i 的核心操作系统介质放入 DVD-ROM 或 CD-ROM 驱动器。在撰写本文时，CD-ROM 上标有 HP-UX Release 11.1。我当时处理的核心操作系统包含两张 CD-ROM，因为我正在安装关键任务操作系统环境（Mission Critical Operating Environment），该环境位于两张 CD-ROM 上（关于操作系统环境的更多信息稍后介绍）。请务必在安装开始前插入 CD-ROM 安装介质。当您的 HP 9000 单元启动时，您会看到各种信息快速滚动，包括有关处理器、总线、启动风扇等的信息。请参阅第 3 章，该章节涵盖了启动过程，以获取更多关于启动的信息。

以下示例显示了执行的几个步骤。示例从早期启动的末尾开始。早期启动是从介质加载过程的第一部分。在我们的示例开始之前，出现了许多与早期启动相关的信息。我们通过按下一个键终止了启动过程。终止启动后，我们运行 SEArCh 来查找可启动设备。在显示的设备中，包含我们操作系统介质的 DVD-ROM 驱动器是其中之一。我们选择 p0 并使用 `bo p0` 命令从中启动。然后我们选择不与 IPL 交互。

```
*****EARLY BOOT VFP *****
End of early boot detected

Firmware Version 39.46
Duplex Console IO Dependent Code (IOCC) revision 1

(C) Copyright 1995-1998, Hewlett-Packard Company, All rights reserved

        Processor        Speed         State
        Number     CoProcessor State Cache Size
               Inst. Data

          0    440 MHz Active    Functional    512 KB 1 MB
          3    440 MHz Idle      Functional    512 KB 1 MB

Central Bus Speed (in MHz)    :      82
Available Memory              : 2097152 KB
Good Memory Required          :  16908 KB

Primary boot path:         0/0/1/1.2
Alternate boot path:      0/0/2/0.2
Console path:             0/0/4/0.0

Keyboard path: 0/0/4/0.0

WARNING: The non-destructive test bit was set, so memory was not tested destructively. Information only, no action required.

Processor is booting from first available device.

To discontinue, press any key within 10 seconds.

Root terminated.

---- Main Menu ----

  Command                  Description
    Boot [P1|ALT] <path>     Boot from specified path
    Path [P1|ALT] <path>     Display or modify a path
    SEArCh [Display|IPL] <path>  Search for boot devices

    Configuration menu     Displays or sets boot values
    Information menu       Displays hardware information
    SERVice menu           Displays service commands

    Display              Redisplay the current menu
    HELP [<menu><command>] Display help for menu or command
    RESET                Restart the system

Main Menu: Enter command or menu > seArCh

Searching for potential boot device(s)
This may take several minutes.

To discontinue search, press any key (termination may not be immediate).

  Path Device Path (dec)  Device Path (sem) Device Type
  P0  0/0/1/0.3          intscsi3.3        Random access media
  P1  0/0/1/1.2          intscsi3.2        Random access media
  P2  0/0/2/2.2          intscsi4.2        Random access media

Main Menu: Enter command or menu > bo P0

Interact with IPL (Y, N, or Cancel)? Y

Booting...
```

上一个列表中的 *SEArCh* 命令向我们展示了可启动设备。有三个可能的启动设备。后两个位于内部硬盘中，其中一个通常是主要启动设备，另一个通常是备用启动设备。这两块硬盘位于 L 类内部的两条不同的 SCSI 总线上。第一个设备是包含 HP-UX 11i CD-ROM 的外部 DVD-ROM，这是我们要从中启动的操作系统介质。

为了从介质启动而不是与 IPL 交互（有关 IPL 的更多信息，请参见第 3 章），我们发出了以下命令：





#### 主菜单：输入命令或菜单

*   `bo p0`
*   是否与 IPL 交互（Y 或 N）?: `N`

从 *P0* 引导后，我们会看到如下示例中所示的 *欢迎使用 HP-UX 安装/恢复流程！* 菜单：

![](img/eff8b9287a5f38c5adf538f24aacf29e_49_0.png)

*欢迎使用 HP-UX 安装/恢复流程！* 菜单是显示的第一个菜单。它提供了系统中硬件的概要。如果您想查看更多详细信息，请选中屏幕右侧的 **H/W Details** 选项。这将带您进入硬件的详细说明列表。其中包括硬件路径、磁盘驱动器容量和 LAN 地址等项目。除了选择 *Install HP-UX*（安装 HP-UX）外，我们在本示例中不会执行其他任何功能。

当我们选择 *Install HP-UX*（安装 HP-UX）时，会看到如下示例中所示的 *用户界面和介质选项* 菜单：

#### 用户界面和介质选项

此屏幕允许您从决定是否使用 Ignite-UX 服务器以及您的用户界面偏好的选项中进行选择。

源位置选项：

- [ *] 仅使用介质安装
- [ ] 启用网络的介质（允许使用 SD 仓库...）
- [ ] 基于 Ignite-UX 服务器的安装

- [ ] [推荐用于基本安装]
- [*] 高级安装（推荐用于磁盘和文件系统管理）

    使用所有默认值并继续

> **提示：** 如果您需要调整逻辑卷大小，或者希望在安装期间设置最终的网络参数，您需要使用高级模式（或远程图形界面）。

[ 确定 ] [ 取消 ] [ 帮助 ]

此菜单为您提供仅从介质安装、从介质结合网络上的软件仓库安装，或使用 Ignite-UX 产品的选项。在我们的示例中，我们将仅从介质进行安装。

接下来我们选择 *Advanced Installation*（高级安装），因为这在安装时提供了最大的灵活性。*Guided Installation*（引导式安装）会引导您完成基本的系统配置设置。它仅允许选择少数系统特定选项。*Advanced Installation*（高级安装）具有更大的灵活性，允许设置广泛的系统特定参数。我们将逐步介绍 *Advanced Installation*（高级安装）步骤。

现在显示的界面与 Ignite-UX 使用的界面类似。实际上，除了 Ignite-UX 使用图形用户界面（GUI）而终端用户界面为 TUI 外，它们是完全相同的。图 1-4 显示了此界面。

#### 高级安装配置

```text
/opt/ignite/bin/itool

    [ Basic ] [ Software ] [ System ] [ File System ] [ Advanced ]

Configurations: [ HP-UX B.11.11 Default. ->] [ Description... ]
Environments: [ Mission Critical OE-64bit ->] (HP-UX B.11.11)
[ Root Disk... ] SEAGATE ST318203LC, 0/0/1/1.2.0, 17366 M
File System: [ Logical Volume Manager (LVM) with VxFS ->]
[ Root Swap (MB)... ] 1024 Physical Memory (RAM) = 2048 MB
[ Languages... ] English [ Keyboards... ] [ Additional... ]

[ Show Summary... ] [ Reset Configuration ]
[ Go! ] [ Cancel ] [ Help ]
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_51_0.png)

*Advanced Installation*（高级安装）菜单允许您从菜单标签区域中进行选择，并且可以在它们之间来回切换，直到您对选择感到满意为止。

在菜单显示的顶部有五个标签区域：*Basic*（基本）、*Software*（软件）、*System*（系统）、*File System*（文件系统）和 *Advanced*（高级）。按 Tab 键可以突出显示每个标签区域。要选中突出显示的标签区域，请按下 Enter/Return 键。这将显示该标签区域的屏幕。在每个区域中，都有几个可以针对您的特定系统进行修改的参数。以下是每个标签区域的主要功能：

### Basic
- 基本 - 配置和环境信息。

### Software
- 软件 - 选择要安装的可选软件的能力。主要是与引导式安装下出现的相同选项。

### System
- 系统 - 网络参数。也可以通过 `set_params` 命令进行配置。

### File System
- 文件系统 - 磁盘空间分配。

### Advanced
- 高级 - 高级磁盘、文件系统、逻辑卷和卷组参数。

我们将从图 1-4 中所示的 *Basic*（基本）屏幕开始配置我们的系统。

以下讨论了几项特别重要的内容：

- **Configuration**（配置）- 我们使用 *HP-UX B.11.11 Default*（HP-UX B.11.11 默认）。在某些情况下，HP-UX 11i 被称为其原始名称 11.11。
- **Environments**（环境）- 在撰写本文时，有四个 11i 环境可供选择。这是 HP-UX 11i 软件分发方法的一项重大变化。运行环境是使安装 11i 更容易的软件包。我们将选择四个中的第一个，即如图 中所示的最高级或最复杂的运行环境：

![](img/eff8b9287a5f38c5adf538f24aacf29e_52_0.png)

- **Root Disk**（根磁盘）- 根磁盘的默认选择是第一个内部磁盘驱动器，在我们的示例中，该磁盘的路径为 0/0/1/2.0。
- **File System**（文件系统）- 我们被赋予选择 `rootdisk`（非 LVM）配合 HFS、逻辑卷管理器配合 HFS 或逻辑卷管理器配合 VxFS 的选项。如果您尚未审阅本章中逻辑卷管理器部分的内容，在做出此选择之前建议您这样做（LVM 是逻辑卷管理器）。我强烈主张尽可能使用逻辑卷管理器配合 VxFS。
- **Root Swap**（根交换区）- 系统自动选择两倍于主内存大小的数量，或最大 1024 MB。您需要非常仔细地考虑您的主要交换空间。我们示例中的 L-Class 系统有 2GB 内存，我们将采用默认的 1GB 交换空间，如所示。
- **Languages**（语言）- 我们将在系统中安装英语；但是，11i 系统有许多语言可供选择。
- **Additional**（附加）- 这是屏幕右下角的选择项，不是标签区域。在这里，您可以配置诸如第二个交换区、向根卷添加第二个磁盘驱动器以及禁用 DHCP 等设置。在 11i 中，DHCP（动态主机配置协议）与 Ignite-UX 服务器协同工作，自动分配系统名称、IP 地址等。

刚才讨论的 11i 与早期 11.x 版本之间的主要区别在于 *Operating Environments*（运行环境）。11i 是第一个提供 *Operating Environments*（运行环境）的 HP-UX 版本。

转到 *Software*（软件）标签区域，我们发现 11i 安装 CD-ROM 上的软件已被标记为待安装。由于我们选择了 *Mission Critical Operating Environment*（关键任务运行环境），因此有大量软件被自动选中作为此安装的一部分。

图 1-5 显示了我们在 *Software*（软件）标签区域中选中的一些软件。我们选择了 *All*（全部），以便可以看到作为 *Mission Critical Operating Environment*（关键任务运行环境）一部分选中的所有软件。我们可以向下滚动以查看其他软件。

```text
/opt/ignite/bin/itool

Basic || Software || System | File System || Advanced |

| Category | Marked? | Product | Description |
| --- | --- | --- | --- |
| All | Yes | GigEther-00 | PCI/HSC/EPP-HSCGigEther |
| HPUXAdditions | Yes | HPUXBaseAux | HP-UX Base OS Auxilary |
| OrderedApps | No | HprFabric-00 | PCI/HSC HyperFabric Driver |
| Uncategorized | No | J4258BA | Netscape Directory Server |
| | No | J4274AA | HP WebQoS Peak Packaged Ed |
| | No | RAID-00 | PCI RAID; Supptd HW=A5856A |
| | No | TermIO-00 | PCI MUX; Suppt HW=J3592A |

[ Change Depot Location... ]

[ Show Summary... ] | [ Reset Configuration ]

[ Go: ] [ Cancel ] (Help)
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_54_0.png)

您可能想要安装的其他软件可以从安装 CD 中选择。在示例中，前两项已作为 *Mission Critical Operating Environment*（关键任务运行环境）的一部分被自动选中。此时，我们可以在此窗口中选择 *Hyperfabric*（超结构）和 *Netscape Directory Server*（Netscape 目录服务器）等附加软件。请记住，此窗口中显示的软件位于 11i 的核心操作系统 CD-ROM 上。您可能稍后希望从 HP-UX 应用程序 CD 集安装应用程序软件。这是使用软件分发器完成的。本章后面将对用于安装所有 HP-UX 11i 软件的软件分发器产品进行概述。您可能需要查看此概述，以了解其大致概念


软件分发程序所提供的功能类型。swinstall 程序是用于安装软件的软件分发程序。如果您有要安装的应用软件，您将使用 swinstall 进行交互，并且可能会被要求输入要安装的部分软件的密钥信息。如果您的软件受到保护，您将必须输入密钥信息。如果您需要密钥，它应该打印在您随软件收到的 CD-ROM 证书上。该密钥与系统中某硬件设备的 ID 编号绑定。

在我们已选定要加载到系统中的软件后，我们可以转到下一个区域。

图 1-6 中所示的系统选项卡区域是查找与系统标识相关的配置信息的地方。由于我们希望在安装完成后配置网络和其他相关信息，因此我们仅更改了此屏幕上的第一项。第一项的选项为：

-   最终系统参数：[立即设置参数]
-   [首次启动时询问]

我们选择了“首次启动时询问”。

![](img/eff8b9287a5f38c5adf538f24aacf29e_56_0.png)

图 1-6 系统选项卡区域

当系统首次启动时，我们将被要求输入与系统标识相关的信息。

图 1-7 中所示的*文件系统*选项卡区域尤为重要。在此处您可以更改文件系统的大小。通常，您不会满足于某些逻辑卷的默认大小。我通常会在该选项卡区域花一些时间来增加某些逻辑卷的大小。图 1-7 还显示了*文件系统*屏幕的布局以及三个逻辑卷的值及其更新后的大小。在此示例中高亮了根分区（Root），因此与其相关的参数显示在*使用情况*、*大小*等项下。

```
/optignite/bin/1tool
--------------------------------------------------------
| Basic || Software|| System || File System || Advanced |
--------------------------------------------------------
Mount Dir Usage Size(MB) % Used Group S
/stand HFS 300 7 vg00 F ^ [ Add ]
primary SWAP+D 1024 0 vg00 R [ Modify ]
/ VxFS 400 9 vg00 F v [ Remove ]

Usage: [ VxFS -> ] Group: [ vg -> ] Mount Dir: /__________
Size: [ Fixed MB ->] 400 Avail: 13360 MB
[ Add/Remove Disks... ] [ ---- Additional Tasks ---- ->]

[ Show Summary... ] [ Reset Configuration ]
[ Go! ] [ Cancel ] [Help] 
```

图 1-7 文件系统选项卡区域

要更改逻辑卷的大小，您选择该逻辑卷的挂载目录，按 Tab 键移动到**大小**，然后输入所需的新大小。除了**大小**之外，还有几个您可以更改的与逻辑卷相关的其他参数。

您会注意到，**可用空间**显示了您的磁盘驱动器上剩余可分配的磁盘空间。留有一部分磁盘空间未分配是完全没问题的。这将为您日后需要增加磁盘空间时提供一个缓冲。

在完成所有与卷大小相关的修改后，我们即可开始安装系统。但是，首先我们希望在屏幕底部选择**显示摘要**选项。该选项将向我们显示所有所做更改的摘要。这让我们有机会确保没有遗漏任何事项。图 1-8 显示了**通用摘要**屏幕。
Summary View
/---\\---
|General Summary|Hardware Inventory|
\---/---
操作系统：HP-UX B.11.11
产品描述
CDE-English 英语 CDE 环境
FDDI-00 PCI FDDI；支持的硬件=A3739A/A3739B
GigEther-00 PCI/HSC/EFF-HSC GigEther，支持硬件= v
卷组 名称 使用情况 大小(MB) 使用% 挂载目录
vg00 HFS 300 7 /stand
vg00 SWAP+D 1024 0 primary
vg00 VxFS 400 9 /
vg00 VxFS 64 0 /tmp
[ 确定 ] [ 帮助 ]

图 1-8 通用摘要屏幕

此屏幕提供了我们选择加载的软件信息以及逻辑卷的信息。
图 1-9 显示了硬件清单摘要屏幕。

![](img/eff8b9287a5f38c5adf538f24aacf29e_59_0.png)

图 1-9 *硬件清单摘要屏幕*

*硬件清单摘要*屏幕的信息提供了系统硬件的简短摘要。

由于我们对所做的所有修改感到满意，我们已准备好加载操作系统。我们选择*确定（Go!）*，它显示在所有选项卡区域屏幕和图 1-10 中的屏幕底部，随后出现了图 1-10 所示的屏幕：

![](img/eff8b9287a5f38c5adf538f24aacf29e_60_0.png)

图 1-10 确定屏幕

此屏幕警告我们目标磁盘上已存在操作系统，但我们仍希望继续进行安装并选择“确定”。此时 HP-UX 的加载是自动进行的，您可以大约一小时后回来检查日志文件，查看操作系统是否加载成功。

您的 HP-UX 11i 操作系统环境可能需要第二张 CD-ROM 才能完成安装，我们的关键任务操作系统环境（Mission Critical Operating Environment）便是这种情况。如下列代码所示，您将收到插入第二张 CD-ROM 的提示：

# 第 1 章 安装 HP-UX 11i 和虚拟分区软件

需要用户交互：

要完成安装，您现在必须插入*关键任务或（MC OR）*CD。

完成后，按<Return>键继续：

+   * 开始安装源（MC OE）的 swinstall。 
+   * 正在运行命令：`/usr/sbin/swinstall -s/tmp/ign_configure/SD_CDROM - /t/tmp/ign_configure/software_file -x CD_release=8.11.12 -x os_name=HP-UX.64`

当操作系统加载完成后，系统会要求我们输入之前未输入的与系统标识相关的信息。以下代码显示的是这些屏幕中的第一个：

欢迎使用 HP-UX！

在使用您的系统之前，您需要回答几个问题。

第一个问题是您是否计划将此系统用于网络。

如果您已将系统连接到网络并准备好连接到网络，请回答“是”。

如果您：
-   计划将此系统设置为独立系统（无网络）。
-   希望现在将系统用作独立系统，以后再接入网络。

请回答上述问题。

准备好将此系统连接到网络了吗？

请回答 [y] 表示是，或 [n] 表示否，然后按 [Enter]

如果您选择将系统连接到网络，您将被问及有关网络配置的各种问题。您现在不必输入这些信息，因为有一个名为**set\_parms**的命令，我们将在下一节中介绍，它是输入与系统标识相关信息的另一种方式。我们将在下一节中介绍该命令。

现在，随着我们的*关键任务操作系统环境*安装完成，我们将使用 **uname -a** 检查操作系统版本，并使用 **swlist** 检查已加载到系统中的软件包，如下列代码所示：

# 非虚拟分区章节特定部分 - 安装 HP-UX 11i 操作系统环境

```
`#   11.11.20A    English CDE Environment`
`#     #   11.11.20A    PCI (FDDI,S)Supported (HWA3739A/A3739B;SW=J3 626AA`
```

该列表显示确实已加载了 HP-UX 11i，在列表中显示为 11.11，并且已加载了多个软件包，其中包括关键任务操作系统环境。

现在让我们进入下一节，在该节中，我们将指定我们在安装期间推迟处理的系统相关信息。

# 启动后设置系统参数

安装完成后系统启动时，会显示一系列窗口，允许您配置系统名称、时区、root 密码、Internet 协议（IP）地址、子网掩码以及其他网络设置（第 13 章介绍的网络章节提供了 IP 地址和子网掩码的背景知识）。您将遇到的第一个问题之一是您是否希望使用 DHCP 获取网络信息。动态主机配置协议与 Ignite-UX 服务器配合工作，自动分配系统名称、IP 地址等。由于我们的安装不使用此功能，我回答了“否”，这意味着我们必须手动输入所有信息。

接下来要输入的系统特定信息也可以在系统启动后，通过运行 **/sbin/set\_parms** 来输入。该程序可用于设置单个系统参数或启动时设置的所有系统参数。**/sbin/set\_parms** 根据您想要配置的内容，使用表 1-1 中的一个参数。

表 1-1 **/sbin/set\_parms** 参数

| **set\_parms 参数** | **注释** |
| :--- | :--- |
| `hostname` | 设置主机名。 |
| `timezone` | 设置时区。 |
| `date_time` | 设置日期和时间。 |
| `root_passwd` | 设置 root 密码。 |
| `ip_address` | 设置 Internet 协议地址（网络背景参见第 2 章）。 |
| `addl_network` | 配置子网掩码、域名系统和网络信息服务。 |
| `initial` | 经历启动时体验到的整个问答过程。 |

如果使用 **initial** 参数，您将使用询问您信息的各种对话框进行交互。图 1-11 显示了系统主机名对话框。




## 系统主机名

为了让系统正确运行，您必须为其分配一个唯一的系统名称或“主机名”。主机名可以是一个简单名称（例如：widget），也可以是一个完整的互联网域名（例如：widget.redrock-cvi.hp.com）。

简单名称或域名中以点(.)分隔的每个组件必须：

- 以字母或数字开头。
- 不超过63个字符。
- 仅包含字母、数字、下划线(_)或短横线(-)。不建议使用下划线(_)。

注意：为了与HP-UX的'uname'命令兼容，主机名的第一个（或唯一）组件应包含8个字符或更少。

在下方字段中输入主机名，然后单击“确定”即可输入主机名。

![](img/eff8b9287a5f38c5adf538f24aacf29e_64_0.png)

接着，系统会要求您输入时区和root密码。图1-12显示了用于输入IP地址的对话框：

![](img/eff8b9287a5f38c5adf538f24aacf29e_65_0.png)

然后，您可以配置子网掩码和其他网络参数。配置包括图1-13中显示的项：

![](img/eff8b9287a5f38c5adf538f24aacf29e_66_0.png)

图1-13 使用set_params setparms3.bmp进行附加配置

运行带有`initial`选项的`set_params`或带有其他选项的`set_params`，允许您指定与系统设置相关的所有初始信息。这为您节省了在所有相关文件中查找需要放置的信息的麻烦。

### 软件分发器示例

![](img/eff8b9287a5f38c5adf538f24aacf29e_67_0.png)

软件分发器（Software Distributor-HP-UX）（在本书中我将简称为软件分发器；HP文档通常使用SD-UX）是在HP-UX 11i中用于执行所有与软件管理相关任务的程序。我们将使用软件分发器的一个示例来安装软件，目标系统即本章前文所述加载了我们操作系统的系统。软件分发器是一种基于标准的软件管理方式。它符合可移植操作系统接口（POSIX）标准，该标准涉及软件打包以及与软件管理相关的实用程序。本节描述的随您的HP-UX系统提供的软件分发器产品可以通过购买OpenView软件分发器（SD-OV）产品来获得附加功能。SD-OV提供对额外平台的支持，允许您将软件推送到目标系统，具备集中监控功能，并提供任务浏览器以协助管理目标系统上的软件。在本节中，我不会详细讨论SD-OV，但会在适当的地方对SD-OV的功能做一些评论。

软件分发器可以通过本节描述的命令、通过SAM（第11章介绍）或如本章前文所述通过首次安装软件来调用。

使用软件分发器进行软件安装的四个阶段如下：

- **选择**(1) - 您可以在此阶段选择要加载的来源和软件。在即将出现的示例中，将使用软件分发器的图形用户界面，您将看到选择这些是多么容易。
- **分析**(2) - 系统将为您执行各种检查，包括磁盘空闲空间；依赖关系；兼容性；已挂载卷；以及其他。此阶段非常有用的一项输出是，您想要加载的软件在每个逻辑卷上将占用的空间量。这将在示例中展示。
- **加载**(3) - 在您对分析结果满意后，可以继续加载软件。
- **配置**(4) - 加载的软件可能需要重新构建内核并重启系统。启动和关闭脚本也可能需要修改。

关于软件分发器有一些我倾向于比较松散地使用的术语。我对软件分发器只有好评，但我本应更多地遵守官方的软件分发器术语。例如，我倾向于频繁使用*系统*一词，而在软件分发器领域中，这个词可能有许多不同的含义。例如，软件分发器使用“*本地主机*”（运行软件分发器的系统，或者是软件安装或由软件分发器管理的目标系统）、“*分发存储库*”（用作软件产品位置的目录）以及“*开发系统*”（准备软件进行分发的位置）。我将使用*系统*一词来指代我们在示例中工作的系统，因为软件是从介质加载到该系统的。

本节中软件分发器的示例描述了从CD-ROM或DVD将软件加载到本地系统的过程。我在此展示的内容只是软件分发器功能表面的开始，但由于我希望您能尽快上手，这个概述应该会很有帮助。您可以从多种介质以及通过网络加载软件。您可以通过贯穿本节的图形界面、字符用户界面或命令行来运行**swinstall**。您可以通过命令行使用**swinstall**命令，指定来源、选项、目标等。我建议使用字符或图形用户界面，因为它们要容易得多。但是，如果您喜欢以“传统UNIX”方式做事，您可以发出带有参数的**swinstall**命令。您可以查看**swinstall**的手册页，以了解其参数和选项，并从命令行使用此命令。软件分发器的图形用户界面与**sd**一起工作（这是一个SD-OV命令，也可以通过**swjob -i**、**swcopy**、**swevmore**、**swlist**和**swinstall**命令调用。如果您没有图形显示器，这些命令也有交互式终端用户界面。

在即将使用的示例中，L-Class系统上，从CD-ROM加载软件并没有太多需要做的操作。我只需物理地将CD-ROM放入DVD光驱，并在命令行中输入**swinstall**。要手动挂载DVD-ROM设备，我发出了命令**mount /dev/dsk/c0t3d0 /cdrom**。要查找系统上的磁盘设备（包括DVD-ROM和CD-ROM），您发出命令**ioscan -funC disk**。

调用swinstall后，我得到了图1-14所示的屏幕，其中显示了软件安装的来源：

![](img/eff8b9287a5f38c5adf538f24aacf29e_69_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_69_1.png)

swinstall填充了对话框中显示的信息。我不必创建目录/cdrom或在命令行发出mount命令，而这在HP-UX的过去版本中我通常需要这样做。swinstall填充了图1-15中显示的所有信息。我们将从中加载应用程序的应用程序CD-ROM标记为HP-UX Release 11.11 and Application Products。

在接受图中显示的信息后，我继续选择（步骤1 - 选择）我想要的软件列表，通过“标记”它来选中要加载的软件。

选择要加载的软件时，您可能在“已标记？”列收到“是”或“部分”。“是”表示与您选择相关的所有文件集都将被加载，而“部分”表示只有部分文件集将被加载。图1-15在已选软件的“已标记？”列中显示“是”。

![](img/eff8b9287a5f38c5adf538f24aacf29e_70_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_70_1.png)

您选择安装的一组软件可能由产品、子产品和文件集组成。您可以选择任何已“标记”为加载的项目，以查看其由哪些文件集组成。我对Java products for II进行了此操作。我选择了这个*束*（bundle），以查看图1-16中其组成的软件：

![](img/eff8b9287a5f38c5adf538f24aacf29e_71_0.png)

图1-16显示Java软件确实由许多组件组成。要返回顶部，我们选择(*向上*)。

选择*安装*会对您选择加载的软件运行*分析*（步骤2 - 分析）。分析完成后，您可以查看日志文件、查看磁盘空间分析，并执行其他任务。我通常会查看磁盘空间分析，以了解正在加载的软件对磁盘空闲空间的影响，如图1-17所示：


## 图 1-17 磁盘空间分析软件分发器界面

![](img/eff8b9287a5f38c5adf538f24aacf29e_72_0.png)

我还查看产品列表，以确保我正在加载预期要加载的软件，如图 1-18 所示，该图显示了之前标记为待安装的产品：

## 图 1-18 产品摘要软件分发器界面

![](img/eff8b9287a5f38c5adf538f24aacf29e_73_0.png)

如果您对分析结果满意，可以继续进行安装（步骤 3 - 加载）。图 1-19 展示了在软件加载到系统过程中提供给您的状态类型：

## 图 1-19 安装窗口软件分发器界面显示状态

![](img/eff8b9287a5f38c5adf538f24aacf29e_74_0.png)

在这种情况下，我们已加载了所选总软件量的约 37%。当前正在加载的软件是 *Netscape 目录服务器*。我们可以查看日志文件，以了解迄今为止已加载的状态。

软件加载完成后，您可以选择退出会话，或者您将收到一条消息，指示需要重启才能完成配置（步骤 4 - 配置）。并非所有软件都需要重启才能进行配置。大多数软件在加载完成后即可运行配置例程，无需重启。如果需要重启，系统会询问您是否希望重启；但此时可能不是重启的好时机，因此您可能希望等待或推迟重启。

使用软件分发器从介质加载软件的过程既简单又全面。软件分发器的用户界面使得从介质中选择和加载软件变得非常容易。

### 加载补丁

HP-UX 补丁可以从多种来源获取。大多数人会从 *IT 资源中心* (*us-support.external.hp.com*) 开始，因为您可以使用浏览器在那里找到各种有用的 HP-UX 信息。

当您在 *IT 资源中心* 初始设置您的账户时，如果您有，请输入您的系统句柄以及您其中一台系统的序列号，以获取该站点所有信息的完整访问权限。

在登录 *IT 资源中心* 查看单个补丁的过程不言自明。选择 *单个补丁* 和 *HP-UX 补丁* 将允许您选择 HP-UX 的特定版本，例如 HP-UX 11i 的 11.11，并选择您希望在系统上加载的补丁。然后，您可以将补丁添加到您的 *购物车* 并下载它们。

当您在 *IT 资源中心* 搜索补丁时，如果补丁已被较新的补丁取代，系统会告知您。选择要查看的补丁后，将提供大量与该补丁相关的有用信息，包括：

- 补丁文件
- 依赖项
- 取代对象
- 大小
- 严重性
- 症状
- 缺陷描述
- 安装说明

我总是在网站上查看补丁的安装说明，以查看加载补丁是否需要任何特殊操作。以下是我们在示例中将下载并安装的补丁的安装说明：

1. 在安装补丁之前备份您的系统。
2. 以 root 身份登录。
3. 将补丁复制到 /tmp 目录。
4. 移动到 /tmp 目录并解压补丁：
   ```
   cd /tmp
   sh PHCO_21187
   ```
5. 运行 swinstall 以安装补丁：
   ```
   swinstall -x autoreboot=true -x patch_match_target=true \
    -s /tmp/PHCO_21187.depot
   ```

默认情况下，swinstall 会将原始软件存档在 /var/adm/sw/save/PHCO_21187。如果您不希望保留原始软件的副本，请使用 patch_save_files 选项：

```
swinstall -x autoreboot=true -x patch_match_target=true \
 -x patch_save_files=false -s /tmp/PHCO_21187.depot
```

> 警告：如果安装补丁时 patch_save_files 为 false，则无法卸载该补丁。使用此功能时请谨慎。

供日后参考，PHCO_21187 文本文件的内容在产品的 readme 中提供：

```
swlist -l product -a readme -d @ /tmp/PHCO_21187.depot
```

要将此补丁放到磁带上并从磁带驱动器安装，请使用以下命令：

```
add -r/tmp/PHCO_21187.depot o=/dev/mt/lm bew=2k
```

特殊安装说明：无

在许多补丁的安装过程中，需要重启。此补丁的 *autoreboot* 选项设置为 *true*，这意味着如果确实需要重启，系统会自动执行重启。在 HP-UX 11i 中，引入了更多 *动态补丁*，这意味着安装补丁时不需要重启。您将看到越来越多的补丁不需要重启。结合 *动态可加载内核模块* 和 *动态可调内核参数*，11i 系统所需的重启次数将越来越少。

审阅与补丁相关的信息后，我们将通过浏览器选择补丁并点击 *添加到购物车* 来下载它。图 1-20 显示了一个已放入 *购物车* 并准备下载的补丁：

![](img/eff8b9287a5f38c5adf538f24aacf29e_77_0.png)

请注意图底部的内容，您可以选择通过 FTP 而不是通过浏览器下载补丁。

图 1-21 显示了一个正在通过浏览器下载的补丁：

## 图 1-21 补丁下载

![](img/eff8b9287a5f38c5adf538f24aacf29e_78_0.png)

补丁下载完成后，只需按照安装补丁的说明操作，例如我们之前示例中所示的补丁说明。通常，您会将补丁下载到 `tmp` 目录，并对下载的文件运行 `sh`，这将生成 `patchname.depot`。然后，您可以按照说明在命令行上运行 *软件分发器* 命令。

对于示例中的补丁，我对下载的文件运行了 `sh`，生成了一个 `.depot` 文件。我们将运行 `swinstall` 以调出用户界面。图 1-22 显示指定源为本地目录，而不是网络目录/CDROM（如本章前面的示例那样），并指定 /tmp 目录中我们的 .depot 文件的源存储库路径：

![](img/eff8b9287a5f38c5adf538f24aacf29e_79_0.png)

然后，我们将按照图 1-23 所示标记补丁以进行安装：

![](img/eff8b9287a5f38c5adf538f24aacf29e_80_0.png)

## 图 1-23 标记为安装的补丁

您可以使用 **swinstall** 以交互方式加载补丁，如本例中我所做的那样，或者按照嵌入在补丁中的说明，从命令行运行 **swinstall**。

### 软件分发器背景

![](img/eff8b9287a5f38c5adf538f24aacf29e_81_0.png)

您需要了解软件在软件分发器中的组织方式的一些背景知识。在软件分发器中，软件被分为以下四种类型的对象：捆绑包（bundle）、产品（product）、子产品（sub-product）和文件集（fileset）。图 1-24 展示了软件分发器对象的层次结构。

![](img/eff8b9287a5f38c5adf538f24aacf29e_81_1.png)

## 图 1-24 软件分发器对象

您可以将图 1-24 中的捆绑包视为一组软件。如图中所示，这可以是产品、子产品和文件集。这里的概念是以易于管理的方式组织软件。图中显示某些文件集在不同捆绑包和产品之间共享。这种层次结构和共享使得使用软件分发器管理软件更加灵活。

接下来，我们将介绍您可以使用软件分发器执行的一些常见软件管理相关任务。

### 安装和更新软件（命令行或 GUI）

**swinstall** 命令用于安装和更新软件。您要加载的软件源可以来自多种地方，包括 CD-ROM、磁带或可以分发软件的“存储库”（depot）目录。使用存储库，您可以将软件加载到目录中，然后从该目录在其他节点上安装和更新软件。使用软件分发器从 CD-ROM 加载的软件必须加载到本地系统；这在接下来的示例中使用了这种技术。在使用 SD-OV 选择要加载软件的目标系统以及加载软件源时，您有很大的灵活性。例如，您可以从网络上另一台系统上的存储库加载软件。该命令可以在命令行上运行，也可以通过图形用户界面运行。

![](img/eff8b9287a5f38c5adf538f24aacf29e_82_0.png)

### 将软件复制到存储库（命令行或 GUI）

**swcopy** 命令用于将软件从一个存储库复制到另一个存储库。接下来的示例中使用的存储库是 CD-ROM。通过设置存储库，您可以使用 SD-OV 同时快速地将软件安装或更新到其他节点。该命令可以在命令行上运行，也可以通过图形用户界面运行。





### 从系统中移除软件（命令行或 GUI）

![](img/eff8b9287a5f38c5adf538f24aacf29e_83_0.png)

**swremove** 命令用于从已通过软件分发器（Software Distributor）加载软件的系统上移除软件。这包括从系统中移除已安装和已配置的软件，或从存储库（depot）中移除软件。此命令可以通过命令行运行，也可以通过图形用户界面运行。

### 列出安装软件的相关信息

**swlist** 命令提供关于系统中存在的存储库、存储库内容或已安装软件的信息。稍后将提供使用该命令的示例。此命令可以通过命令行运行，也可以通过图形用户界面运行。

### 配置已安装软件

**swconfig** 命令用于配置或取消配置已安装软件。软件配置通常作为 **swinstall** 的一部分进行，但配置可以推迟到稍后的时间执行。

### 验证软件

**swverify** 命令用于确认已安装软件或存储在存储库中的软件的完整性。

### 打包稍后可安装的软件（仅限本地系统）

您可能希望使用 **swpackage** 命令生成软件的“包”，以便稍后将其放入磁带或存储库中。此打包软件随后可以用作 **swinstall** 的来源，并由其他软件分发器命令管理。

![](img/eff8b9287a5f38c5adf538f24aacf29e_84_0.png)

### 控制对软件分发器对象的访问

您可能希望对软件分发器对象（如打包软件）施加受限访问。使用 **swacl** 命令，您可以查看和更改对象的访问控制列表（ACL）。

### 修改已加载软件的信息（仅限本地系统）

已安装产品数据库（IPD）及相关文件用于维护有关已加载软件产品的信息。**swmodify** 可以在命令行上运行以修改这些文件。

### 注册或注销存储库

可以使用 **swreg** 注册或注销软件存储库。这意味着您不必移除存储库；如果暂时不想使用它，您可以将其注销。

### 管理作业（命令行或 GUI，仅限 SD-OV）

可以使用 **swjob** 查看和移除软件分发器作业。此命令的图形用户界面版本可以通过 **sd** 或 **swjob -i** 调用。

![](img/eff8b9287a5f38c5adf538f24aacf29e_85_0.png)

### 列出软件

虽然我更喜欢 **swinstall** 的图形用户界面，但您也可以在命令行上发出软件分发器命令。一个例子是 **swlist** 命令。**swlist** 命令对于查看系统上已加载的软件、查看存储库中已加载的软件或生成存储库列表非常有用。可以通过 *-i* 选项调用 **swlist** 命令的图形用户界面，并且 SAM 中也提供此界面。使用 **swlist** 命令，您可以执行许多功能，包括以下内容：

- 使用 *-l* 选项列出指定级别的软件。稍后我将展示几个示例。可以指定的级别包括：
    - root（根）
    - depot（存储库）
    - bundle（捆绑）
    - product（产品）
    - subproduct（子产品）
    - fileset（文件集）
    - file（文件）

级别由 "." 分隔，因此您会看到 *bundle:*[product]*[:* [subproduct]*[:* [fileset] ]。您可以从 **swlist** 中获取各种有用信息，并将其用于其他目的。您可以使用 **swlist** 执行的一些操作包括：

- 显示软件源的目录。
- 指定希望查看的软件级别属性，如名称、大小、修订版等。
- 创建产品列表，可用作其他软件分发器命令（如 **swinstall** 和 **swremove**）的输入。

当您不带任何选项运行 **swlist** 时，会获得系统上已安装软件产品的列表。让我们尝试使用 *-l* 选项运行几个 **swlist** 命令来查看系统中已安装的软件（默认情况下，**swlist** 将列出已安装的产品；您可以使用 *-s* 选项指定软件存储库或其他源）。以下示例展示了在 *bundle* 级别列出软件。

```
$ swlist -l bundle
# various header information
#
# . . .
B249lBA B.11.00 MirrorDisk/UX
B3701AA_TRY B.11.00.31 Trial HP GlancePlus/UX Pak s800
B3929BA B11.00 HP OnLineJFS (Advanced VxFS)
B3947BA B.11.00 HP Process Resource Manager
B5729AA B.1.4 HP-UX Installation Utilities (ignite-UX)
HPUXEng32RT B.11.00 English HP-UX 32-bit Runtime Environment
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_86_0.png)

该系统具有 HP-UX 运行时环境、GlancePlus/UX 试用软件、HP OnLineJFS 和 MirrorDisk/UX。

如果我们在产品级别运行 `swlist`，对于 GlancePlus/UX 试用软件将产生以下内容：

```
$ swlist -l product B3701AA_TRY
# various header information
#
# . . .
#
B3701AA_TRY B.11.00.31 Trial HP GlancePlus/UX Pak for s800 11.00
B3701AA_TRY.MeasurementInt B.11.00.31 HP-UX Measurement Interface for 11.00
B3701AA_TRY.MeasureWare B.11.00.31 MeasureWare Software/UX
B3701AA_TRY.Glance B.11.00.31 HP GlancePlus/UX
(bundle) (product)
```

GlancePlus/UX 由本例中显示的两个产品组成。GlancePlus/UX 是否包含任何子产品？以下示例将帮助我们确定答案。

```
$ swlist -1 subProduct B3701AA_TRY
# various header information
#
# . . .
#
B3701AA_TRY B.11.00.31 Trial HP GlancePlus/UX Pak for s800 11.00
B3701AA_TRY.MeasurementInt B.11.00.31 HP-UX Measurement Interface for 11.00
B3701AA_TRY.MeasureWare B.11.00.31 MeasureWare Software/UX
B3701AA_TRY.Glance B.11.00.31 HP GlancePlus/UX
(bundle) (product)
```

产品级别和子产品级别的输出相同；因此，GlancePlus/UX 中没有子产品。我们可以更进一步，将其推进到文件集级别，如下例所示：

```
$ swlist -l filesent B3701AA.TRY
# various header information
#...
#...
B3701AA.TRY B.11.05.1 Trial HP GlancePlus/UX Pak for s800 11.00
B3701AA.TRY,MeasurementInt B.11.00.1 HP-UX Measurement Interface for 11.00
B3701AA.TRY,MeasurementInt,ARM B.11.00.1 MP-UX Application Response Measurement for 11.00
B3701AA.TRY,MeasurementInt,MI B.11.00.1 HP-UX Measurement Interface for 11.00
B3701AA.TRY,MeasureWare B.11.00.1 MeasureWare Software/UX
B3701AA.TRY,MeasureWare,MWA B.11.00.1 MeasureWare Software files
B3701AA.TRY,MeasureWare,MWANQ B.11.00.1 MeasureWare NQS Connectivity Module
B3701AA.TRY,MeasureWare,Software B.11.00.1 HP PDS Data Source Integration
B3701AA.TRY,MeasureWare,PERFDSC B.11.00.1 HP GlancePlus/UX
B3701AA.TRY,Glance B.11.00.1 HP GlancePlus files
B3701AA.TRY,Glance,GLANC B.11.00.1 HP GlancePlus Motif interface files
B3701AA.TRY,Glance,GPM (bundle) (product) (filesent)
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_87_0.png)

通过 `swlist` 命令和 `-l` 选项，我们深入遍历了 HP GlancePlus/UX 的层次结构。使用 `-l file` 选项深入到此产品的文件级别会生成与此产品关联的文件长列表。表 1-2 显示了我使用的一些 `swlist` 的 `-l` 选项：

# 表 1-2 部分 swlist -l 选项列表

| 命令 | 说明 |
| --- | --- |
| `swlist -l root` | 显示根级别。 |
| `swlist -l sroot` | 显示共享根。 |
| `swlist -l proot` | 显示私有根。 |
| `swlist -l bundle` | 仅显示捆绑。 |
| `swlist -l product` | 仅显示产品。 |
| `swlist -l subproduct` | 显示产品和子产品。 |
| `swlist -l filesent` | 显示产品、子产品和文件集。 |
| `swlist -l file` | 显示产品、子产品、文件集、文件和编号。 |
| `swlist -l category` | 如果补丁的定义中有类别，则显示所有可用补丁的类别。 |
| `swlist -l patch` | 显示所有已应用的补丁。 |
| `swlist -l depot` | 显示本地主机上的所有存储库。 |
| `swlist -l depot @ sys` | 显示 sys 上的所有存储库。 |

软件分发器背景

我也喜欢在使用 **swlist** 时使用 -a 选项。-a 指定您希望查看与所列软件相关的特定属性。您可以查阅 HP-UX 系统上的 sd 手册页以获取完整的属性列表。我经常查看的一个属性是大小。要获取 NETWORKING 中子产品的列表及其 KBytes 大小，您应发出以下命令：

```
$ swlist -l subproduct -a size NETWORKING
```

我经常查看的另一个属性是修订版（revision），您可以通过以下命令查看：

```
$ swlist -l subproduct -a revision NETWORKING
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_88_0.png)

有时，给出的文件集简要描述不足以真正理解该文件集。title 属性提供描述性标题，您可以通过以下命令在文件集级别看到：

```
$ swlist -l fileset -a title NETWORKING
```

表 1-3 是一些您可能感兴趣的属性列表。

# **表 1-3 部分感兴趣属性列表**

| 属性 | 说明 |
|---|---|
| architecture | 显示软件支持的目标系统。 |
| category | 显示软件类型。 |
| description | 显示软件的更详细描述。 |
| title | 显示软件的官方名称。 |


## 属性 | 说明

| 属性 | 说明 |
| :--- | :--- |
| owner | 显示文件的属主。 |
| path | 显示文件的完整路径名。 |
| revision | 显示软件对象的修订号。 |
| size | 显示所有文件集的大小。 |
| state | 显示文件集的状态。 |

前面列出的其他软件分发器命令也可以在命令行中发出。当您准备进行比从 DVD、CD-ROM 或磁带加载软件更高级的软件分发器工作时，可能需要查阅这些命令的手册页。

对于熟悉 HP-UX 9.x 的系统管理员来说，HP-UX 10.x 和 11.x 中的软件组织方式有所不同，但 **swinstall** 的图形用户界面与软件分发器更好的组织方式相结合，使这成为 HP-UX 11.x 的优势。

![](img/eff8b9287a5f38c5adf538f24aacf29e_89_0.png)

### 第 1 章中使用的命令手册页

以下部分包含第 1 章中使用的命令手册页的副本。这为您提供了快速参考，以便在系统管理日常工作中发出常用命令时使用。手册页（更常被称为 man 页）详细列出了所有条目，但软件分发器（SD-UX）除外。由于软件分发器通常通过图形用户界面使用，因此仅给出这些命令的命令行版本摘要。这些命令列在“sw 命令摘要”下。

#### "sw" 命令摘要

- "sw" 命令 - 与软件分发相关的命令摘要。

![](img/eff8b9287a5f38c5adf538f24aacf29e_91_0.png)

swacl(1M) Hewlett-Packard 公司 swacl(1M)

### 名称

swacl - 查看或修改保护软件产品的访问控制列表（ACL）

### 概要

```
swacl -level [-M acl_entry|-D acl_entry|-F acl_file] [-x option=value]  
[-X option_file] [-f software_file] [-t target_file]  
[software_selections] [@ target_selections]
```

swagentd(1M) Hewlett-Packard 公司 swagentd(1M)
swagent(1M) swagent(1M)

### 名称

swagentd - 处理本地或远程 SD 软件管理任务，包括调用 swagent 命令。

swagent - 作为 SD 命令的代理执行 SD 软件管理任务。

SWAGENTD.EXE - 执行 HP OpenView 软件分发器 PC 软件管理任务，或提供本地 PC 软件以供分发。请参阅下面的“备注：”。

### 概要

```
swagent [-k] [-n] [-r] [-x option=value] [-X option_file]
```

SWAGENTD.EXE（仅限 HP OpenView 软件分发器）

#### swcluster(1M)

#### 名称

swcluster - 从无盘服务器安装或删除软件

#### 概要

`swcluster [XToolkit Options] [-v]` `[v] [-i]` `[-p]` `[-f]` `[-r]` `[-b]` `[-l list_class] [-n] [-s source]`
`[-C session_file]` `[-S session_file]` `[x option=value]` `[-X option_file]` `[software_selections] [@ target_selections]`

#### swconfig(1M)

Hewlett-Packard 公司

#### 名称

swconfig - 配置、解除配置或重新配置已安装的软件

#### 概要

`swconfig [-p]` `[-v]` `[-u]` `[-x option=value]` `[-X option_file]` `[-f software_file]` `[-t target_file]`
`[-C session_file]` `[-S session_file]` `[-Q date]` `[-J jobid]` `[software_selections] [@ target_selections]`

#### swgettools(1M)

Hewlett-Packard 公司

#### 名称

swgettools - 用于从新的 SD 介质获取 SD 产品的实用程序

#### 概要

```
swgetools -s <source_media_location> [-t <temp_dir_location>]
```

swinstall(1M) Hewlett-Packard 公司 swinstall(1M)
swcopy(1M) swcopy(1M)

### 名称

swinstall - 安装和配置软件产品
swcopy - 复制软件产品以便后续安装或分发

### 概要

```
swinstall [XToolkit Options] [-i] [-p] [-v] [-r] [-s source] [-x option=value] [-X option_file]
[-f software_file] [-t target_file] [-C session_file] [-S session_file]
[-Q date] [-J jobid]
[software_selections] [@ target_selections]
swcopy [XToolkit Options] [-i] [-p] [-v] [-s source] [-x option=value] [-X option_file]
[-f software_file] [-t target_file] [-C session_file] [-S session_file]
[-Q date] [-J jobid]
[software_selections] [@ target_selections]
```

swjob(1M) Hewlett-Packard 公司 swjob(1M)
sd(1M) sd(1M)

### 名称

swjob - 显示作业信息并删除作业。

sd - 用于创建和监视作业的交互界面。

有关 HP OpenView 软件分发器对象、属性和数据格式的描述，请输入以下命令查看 sd(4) 手册页：

man 4 sd

有关所有 HP OpenView 软件分发器命令的概述，请输入以下命令查看 sd(5) 手册页：

man 5 sd

### 概要

swjob [-i] [-u] [-v] [-R] [-a attribute] [-x option=value] [-X option_file] [-f jobid_file]
[-t target_file] [-C session_file] [-S session_file] [jobid(s)] [@ target_selections]

sd [-x option=value] [-X option_file]

### swlist(1M) Hewlett-Packard 公司 swlist(1M)

#### 名称

swlist - 显示软件产品的信息

#### 概要

swlist [-d|-r] [-1 level] [-v] [-a attribute] [-R] [-s source] [-x option=value] [-X option_file]
[-f software_file] [-t target_file] [-C session_file] [-S session_file]
[software_selections] [@ target_selections]

### swmodify(1M) Hewlett-Packard 公司 swmodify(1M)

#### 名称

swmodify - 修改目标根或仓库中的软件产品

#### 概要

```
swmodify [-d|-r] [-p] [-P pathname_file] [-v[v]] [-V] [-u]
         [-s product_specification_file|-a attribute=[value]] [-x option=value]
         [-X option_file]
         [-f software_file|-C session_file] [-S session_file]
         [software_selections] [@ target_selection]
```

### swpackage(1M) Hewlett-Packard 公司 swpackage(1M)

#### 名称

swpackage - 将软件产品打包到目标仓库或磁带上

有关作为 swpackage 命令输入的产品规范文件的描述，请输入以下命令查看 swpackage(4) 手册页：

```
man 4 swpackage
```

#### 概要

```
swpackage [-p] [-v[v]] [-V] [-s product_specification_file|directory]
          [-d directory|device]
          [-x option=value] [-X option_file] [-f software_file] [-C session_file]
          [-S session_file]
          [software_selections] [@ target_selection]
```

### swreg(1M) Hewlett-Packard 公司 swreg(1M)

#### 名称

swreg - 注册或注销仓库和根

#### 概要

swreg -l level [-u] [-v] [-x option=value] [-X option_file] [-f object_file] [-t target_file] [-C session_file] [-S session_file] [objects_to_(un)register] [@ target_selections]

### swremove(1M) Hewlett-Packard 公司 swremove(1M)

#### 名称

swremove - 解除配置并移除软件产品

#### 概要

swremove [XToolkit Options] [-i] [-p] [-v] [-d|-r] [-x option=value] [-X option_file] [-f software_file] [-t target_file] [-C session_file] [-S session_file] [-Q date] [-J jobid] [software_selections] [@ target_selections]

### swverify(1M) Hewlett-Packard 公司 swverify(1M)

#### 名称

swverify - 验证软件产品

#### 概要

swverify [-v] [-d|-r] [-x option=value] [-X option_file] [-f software_file] [-t target_file] [-C session_file] [-S session_file] [-Q date] [-J jobid] [software_selections] [@ target_selections]

# 第 2 章

# 使用虚拟分区

## 创建虚拟分区的准备

在第 1 章中，我们加载了 HP-UX 11i 和虚拟分区软件。现在，我们准备好创建虚拟分区了。在本章中创建虚拟分区后，我们需要启动我们创建的分区。虽然我们将在本章中启动分区，但启动虚拟分区的细节，以及 HP 9000 启动的一般过程，将在第 3 章中详细涵盖。

既然我们的磁盘上既有 HP-UX 11i 又有虚拟分区软件，我们就能开始创建分区的过程了。我们的目标是拥有一个看起来像图 2-1 那样的系统：

![](img/eff8b9287a5f38c5adf538f24aacf29e_99_0.png)

图 2-1 虚拟分区软件栈

图 2-1 中有许多组件。我们的系统中已经拥有了图中许多组件。从底部开始，我们有硬件、固件、虚拟分区监视器（在第 3 章中作为启动过程的一部分进行介绍），以及安装在两个不同磁盘上的 HP-UX 11i。图 2-1 最左边的两个堆栈中显示了两个 HP-UX 11i 实例。这些是我们已经加载的操作系统。

由于我们尚未创建虚拟分区，因此这两个 HP-UX 11i 实例无法在我们的 L 类系统上同时运行。在没有创建虚拟分区的情况下，我们可以从这两个之一启动 HP-UX

这些磁盘，但我们无法同时运行两者。现在让我们创建虚拟分区（Virtual Partions），这样我们确实可以拥有两个同时运行的 HP-UX 11i 实例。创建虚拟分区后，您可以继续加载图 2-1 中所示的 HP-UX 11i 顶部的中间件和应用。

虽然我们将在创建的虚拟分区中介绍运行多个 HP-UX 11i 实例，但我们将来不会仅限于 HP-UX 11i。在基于安腾处理器家族（IPF）CPU 的系统上，我们将能够运行额外的操作系统。图 2-1 中最右侧的虚拟分区描绘了这种未来的能力。在本书撰写时，此功能尚不存在，因此未在此处详细介绍。请留意本册书未来涵盖此功能的更新版本，并关注 www.hp.com 上关于 IPF 和虚拟分区的增强功能。

尽管本章中的示例发生在四路（四处理器）L 类系统上，但 vPars 可在大多数 HP 服务器上运行。HP 服务器由组件组成的数量越多，服务器上可拥有的 vPar 数量就越多，并且为创建 vPars 提供的选项也越多。图 2-2 展示了一个八路 HP 服务器示例以及 vPars 的配置方式：

![](img/eff8b9287a5f38c5adf538f24aacf29e_101_0.png)

**图 2-2** 使用 vPars 的 HP 服务器资源分配示例

可以看到，所示的八路系统为每个虚拟分区分配了不同数量的处理器、不同容量的内存和不同数量的 I/O 卡。未使用的组件可以添加到任何 vPar 中，或者作为另一个 vPar 的基础。此外，组件可以从一个 vPar 移动到另一个 vPar（有关限制，将在本章稍后部分描述）。

在本章的示例中，最终我们将得到一个拥有两个完全配置的虚拟分区的四路 L 类系统。在继续这些示例之前，让我们先看看下一节中我们将在全章使用的命令。

### 虚拟分区命令摘要

图 2-1 中用于创建和处理虚拟分区还有若干我们尚未涉及的命令。表 2-1 提供了许多常用虚拟分区相关命令的概述。这与可拆卸的 Overture 分区命令摘要中的信息相同。

**表 2-1** 虚拟分区命令摘要

| 命令 | 描述 |
| :--- | :--- |
| **ISL>** | 通过以下方式从 **ISL>** 加载虚拟分区监视器：<br>**ISL>** `hpxux /stand/vpmon`<br>**MON>**<br>要从 **ISL>** 直接加载虚拟分区，请使用：<br>**ISL>** `hpxux /stand/vpmon vparload -p vPar_name`<br>初始系统加载提示符。 |
| **MON>** | 这是通过以下方式从 **ISL** 加载的：<br>**ISL>** `hpxux /stand/vpmon`<br>**MON>**<br>要从 **ISL** 加载备用数据库，请使用：<br>**ISL>** `hpxux /stand/vpmon -D db_file`<br>要从 **MON>** 加载一个 vPar，请使用：<br>**MON>** `vparload vPar_name`<br>可以从 **MON>** 发出许多其他命令。输入 `help` 或 `?` 进行列表查看。（命令包括：`scan`、`vparinfo`、`ls`、`log`、`getauto`、`list`、`cbuf`、`cat`、`?`） |
| | 虚拟分区监视器提示符。（另请参阅 `vparload` 命令。） |
| **vparload**<br>仅从 **MON>** 提示符加载虚拟分区。 | form1: `vparload -all`<br>form2: `vparload -auto`<br>form3: `vparload -p vp_name [-b kernelpath] [-o "boot_options"] [-B hardware_path]`<br><br>要从 **MON>** 启动虚拟分区：<br>**MON>** `vparload -p vPar_name`<br><br>要从 **MON>** 启动所有虚拟分区：<br>**MON>** `vparload -all`<br><br>要从 **MON>** 以单用户模式启动虚拟分区：<br>**MON>** `vparload -p vPar_name -o "-ls"`<br><br>在 **MON>** 处发出的其他一些选项包括：<br>`"-1q"`（低仲裁）、`"-1m"`（维护模式） |
| **vparboot**<br>仅从命令行启动虚拟分区。 | form1: `vparboot -p vp_name [-b kernel_path] [-o boot_opts] [-B boot_addr]`<br>form2: `vparboot -p vp_name -l ignite_kernel`<br><br>要从命令行启动虚拟分区：<br># `vparboot -p vPar_name`<br>要从命令行以单用户模式启动虚拟分区：<br># `vparboot -p vPar_name -o "-ls"` |
| **vparcreate**<br>创建虚拟分区。 | form: `vparcreate -p vp_name [-B boot_attr] [-D db_file] [-S static_attr] [-b kernel_path] [-o boot_opts] [-a rsrc] [...,]`<br><br>创建一个总共有三个处理器（num）、绑定两个（min）、2048MB 内存、/0/0 上的所有组件、位于 0/0/1/2.0 的启动磁盘、内核为 /stand/vmunix、自动加速开启且控制台位于 0/0/4/0 的虚拟分区：<br># `vparcreate -p vPar_name -a cpu::3 -a cpu::2:4 -b mem::2048 -a io::0/0 -a io::0/0/1/2.0:boot -b /stand/vmunix -B auto`<br><br>注意：<br>- 必须在创建虚拟分区之前或之后将 HP-UX 11i 加载到卷上。如果在创建 vPar 之后加载 HP-UX 11i，则使用 `vparboot -p vp_name -I ignite_kernel` 来加载 11i。<br>- /stand/vmunix 是默认值，无需指定。<br>- vPar 未设置为*静态*，这意味着可以稍后修改它。<br>- CPU 总数为三个（num），绑定两个（min），最多两个未绑定（max）。 |
| **vparmodify**<br>修改虚拟分区的属性。（请注意，使用 `-a` 添加 CPU 是相对于当前数量的。`-a cpu::2` 会在当前 CPU 数量的基础上增加两个 CPU。`-m cpu::3` 指定绝对数量为三个 CPU。） | form: `vparmodify -p vp_name [-B boot_attr] [-D db_file] [-S static_attr] [-b kernel_path] [-o boot_opts] [-P new_vp_name] [-a rsrc] [...,] [-m rsrc] [...,] [-d rsrc] [...,]`<br><br>要添加路径 /109 处的处理器（将此处理器添加到已分配的处理器中）：<br># `vparmodify -p vPar_name -a cpu::109`<br>要指定绝对数量为三个处理器：<br># `vparmodify -p vPar_name -m cpu::3` |
| **vparremove**<br>删除虚拟分区。 | form: `vparremove -p vp_name [-D db_file] [-f]`<br><br>要删除当前运行数据库中的虚拟分区：<br># `vparremove -p vPar_name` |
| **vparreset**<br>重置虚拟分区。 | `vparreset -p vp_name [-t\|-l] [-q] [-f]`<br><br>重置虚拟分区，模拟在 `Ctrl-B` 提示符处的 TOC 操作。如果没有 `-h` 选项，默认命令仅模拟 TOC。<br># `vparreset -p vPar_name`<br><br>强制重置虚拟分区：<br># `vparreset -p vPar_name -h -f` |
| `vparresources(5)` man 页<br>提供虚拟分区及其资源的描述。 | 这是一个手册页，总体描述了虚拟分区资源以及资源如何在其他命令（如 `vparmodify`）中指定。 |
| **vparstatus**<br>显示虚拟分区的状态。 | form1: `vparstatus [-v\|-M] [-p vp_name] [-p..\| -D db_file]`<br>form2: `vparstatus -A [ -M]`（可用资源）<br>form3: `vparstatus -w`（当前 vPar 的名称）<br>form4: `vparstatus -e`（虚拟分区监视器的事件日志）<br>form5: `vparstatus -R [ -p vp_name]`（最近重置的 PIM 数据）<br><br>以详细模式显示虚拟分区的状态：<br># `vparstatus -v -p vPar_name`<br><br>以详细模式显示所有虚拟分区的状态：<br># `vparstatus -v`<br><br>显示可用或未使用的资源：<br># `vparstatus -A` |
| `vpartition` man 页<br>显示有关虚拟分区命令行的信息。 | 提供了以下关于虚拟分区命令的简要描述：<br>**vparboot** 启动虚拟分区。<br>**vparcreate** 创建新的虚拟分区。<br>**vparmodify** 修改现有的虚拟分区。<br>**vparremove** 移除（删除）现有的虚拟分区。<br>**vparreset** 模拟对虚拟分区的 TOC 或硬重置。<br>**vparstatus** 显示虚拟分区和可用资源信息。 |





### vPar 资源命令选项

| 命令 | 描述 |
| :--- | :--- |
| **通过以下方式使用 CPU 资源：** | 绑定和非绑定 CPU 的数量：`cpu::num`<br>CPU 硬件路径：`cpu:path`<br>最小值和最大值：`cpu::[min[:max]]` |
| **CPU 类型：**<br>（有关所有资源类型的更多详情，请参见 `vparresources` 手册页。） | **绑定**：当 vPar 处于活动状态时，CPU 绑定到虚拟分区。分配在创建 vPar 时进行。最低的绑定 CPU 编号为 vPar 的 `monarch`。中断由绑定 CPU 处理。<br>**非绑定**：可以动态重新分配的 CPU。不处理中断。 |
| **通过以下方式使用内存资源：** | 大小 `mem::size`<br>基址和范围：`mem::base:range`<br>上述两者的组合。 |
| **指定 I/O：** | 使用路径：`io:path[.attr1\|.attr2[...]]`<br>（有关详情，请参见手册页 `vparresources`）。 |
| **添加资源使用：**<br>（如果正在运行 `vparmodify`，这会将组件相对于已存在的项添加。） | `-a cpu:path`<br>`-a cpu::num`（可在 vPar 运行时进行）<br>`[-a cpu::num -a cpu::min:[max]]`（`:` 仅限 `vparcreate` 使用）<br>`-a io:path[.attr1\|.attr2[...]]`<br>`-a mem::size`<br>`-a mem::base:range` |
| **删除资源使用：**<br>（如果正在运行 `vparmodify`，这会将组件相对于已存在的项删除。） | `-d cpu:path`<br>`-d cpu::num`（可在 vPar 运行时进行）<br>`-d io:path[.attr1\|.attr2[...]]`<br>`-d mem::size`<br>`-d mem::base:range` |
| **修改资源使用：**<br>（这是相对于绝对数值进行修改。） | `-m cpu::num`（可在 vPar 运行时进行）<br>`-m cpu::[min[:max]]`<br>`-m io:path[.attr1\|.attr2[...]]`<br>`-m mem::size` |

### vPars setboot 选项

| 命令 | 描述 |
| :--- | :--- |
| vPars **setboot** 选项：<br>- `-a`<br>- `-b`<br>- `-p`<br>- `-s`<br>- 无选项 | 更改虚拟分区的备用启动路径。<br>设置虚拟分区的自动启动属性。<br>更改虚拟分区的主要启动路径。<br>无效果。<br>显示有关启动属性的信息。 |
| | 要开启自动启动：<br>`# **setboot -b on**`<br>要设置主要启动路径：<br>`# **setboot -p 0/0/1/1.2.0**`<br>要设置备用启动路径：<br>`# **setboot -a 0/8/0/0.8.0.5.0.0.0**` |

### vPars 状态

| 状态 | 描述 |
| :--- | :--- |
| *load* | 虚拟分区的内核映像正在加载到内存中。这是由虚拟分区监视器执行的。 |
| *boot* | 虚拟分区正在启动过程中。内核映像已成功加载到虚拟分区监视器。 |
| *up* | 虚拟分区已成功启动并正在运行。 |
| *shut* | 虚拟分区正在关闭过程中。 |
| *down* | 虚拟分区未运行且处于停止状态。 |
| *crash* | 虚拟分区发生了恐慌并正在崩溃。 |
| *hung* | 虚拟分区无响应并处于挂起状态。 |

我们将使用即将在创建虚拟分区章节中展示的一些命令。附录 A 提供了有关虚拟分区命令的更多详情，其中包含这些命令的在线手册页。

现在，让我们继续创建我们的虚拟分区。

## 创建虚拟分区的步骤

在本节中，我们将介绍创建虚拟分区的步骤。这些是第 1 步，是在处理 vPars 的某些非常早期的安装期间执行的。此列表应作为处理 vPars 的框架。您可能选择不执行某些步骤并添加其他步骤。这只是一个使 vPars 在您的系统上运行的框架。

在我们将要创建虚拟分区的示例中，我们将执行图 2-3 中所示的步骤。

1. 将 HP-UX 11i 加载到您希望运行虚拟分区的磁盘上*（介质或 Ignite/UX 服务器。）
2. 将虚拟分区软件加载到您希望运行虚拟分区的磁盘上。
3. 使用 `ioscan`、`dmesg` 和其他命令收集系统组件和硬件路径的信息。
4. 列出组成虚拟分区的组件。
5. 在所有将运行虚拟分区的卷上使用 **mk_kernel** 和 **knupdate** 构建新的 HP-UX 11i 内核*（自动完成，用于所有将运行 vPars 的 11i 实例。）
6. 使用 `vparcreate` 创建第一个虚拟分区。
7. 在 `MON>` 提示符下使用 `vparload` 启动第一个虚拟分区。使用 `vparstatus -v` 查看正在运行的 vPar，使用 `vparstatus -A` 查看可用组件。
8. 使用 `vparcreate` 创建第二个虚拟分区（也可以在启动任何 vPar 之前完成）。
9. 从第一个 vPar 使用 `vparboot` 启动第二个虚拟分区，并使用 `vparstatus` 监视其启动过程。启动后，使用 `vparstatus -A` 查看剩余的可用组件。
10. 根据需要，使用 `vparmodify` 修改虚拟分区，并使用 `vparstatus -v` 和 `vparstatus -A` 查看修改内容。修改可以是任何类型，例如添加 CPU、更改属性等。

### 其他任务和备注：

- 可以执行许多其他任务。上述步骤中未使用命令 `vparremove` 和 `vparreset`。

- 典型的 vPar 组件列表如下所示：

```text
name          cabled
processors    min of 1 (bound) max of 3 (1 bound 2 unbound) with num equal to 1
memory        1024 MB
LAN           0/0/0/0 (not specified explicitly)
boot disk     0/0/1/1.2.0
kernel        /stand/vmunix
autoboot      off (manual)
console       0/0/4/0 (not specified explicitly)
```

\* 必须在创建虚拟分区之前或之后将 HP-UX 11i 加载到卷上。如果在创建 vPar 之后加载 HP-UX 11i，则使用 `vparboot -p vp_name -i ignite_kernel` 来加载 11i。

![](img/eff8b9287a5f38c5adf538f24aacf29e_109_0.png)

### 1) 加载 HP-UX 11i

必须将 HP-UX 11i 加载到将用于托管所有 vPar\&s 的卷上。您用于安装 11i 的方法，无论是介质、Ignite-UX 还是其他技术，只要 HP-UX 11i 存在于所有磁盘上都是可接受的。在您开始创建 vPar 之前，第一个磁盘上必须存在 HP-UX 11i。您可以在其他磁盘上创建 vPar\&s，而在 HP-UX 11i 加载到它们之前，然后使用 **vparboot -p vp_name -i ignite.kernel** 在其他磁盘上启动并加载 HP-UX 11i。在本章中，我在创建 vPar\&s 之前首先在 11i 上加载了 HP-UX 11i。第 1 章介绍了加载 HP-UX 11i 和 vPar\&s 软件。在我们的即将推出的示例中，第一个虚拟分区将在 L-Class 系统的内部磁盘上创建。第二个虚拟分区将在外部磁盘上创建。在其中一个根卷上加载 HP-UX 11i 后，我发出了 **uname**，结果输出如下：

```bash
# uname -a
HP-UX cvhdccon3 B.11.11 U 9000/800 136414696 unlimited-user license
#
```

显示了主机名 *cvhdccon3* 和 HP-UX 修订版 *11.11*，这是撰写本文时可用的最新 HP-UX 11i。

处理 vPar\&s 的一个有趣细节是主机和 vPar\&s 的命名。第 1 章中有一个主机名部分，您可能需要重新阅读。简而言之，您在安装 11i 时提供主机名，在创建 vPar\&s 时提供虚拟分区名称。如果 HP-UX 11i 实例的主机名和 vPar 名称相同，可以减少混淆。然而，在某些情况下，组织要求主机名符合导致名称难以记忆的约定。在这种情况下，一些系统管理员会选择一个容易记住的 vPar 名称。在即将到来的示例中，我们为 vPar\&s 和主机名使用了不同的名称。

我们即将展示的示例的主机名为 *cvhdccon3* 和 *cvhdccon4*。使用的相应 vPar 名称为 *cable1* 和 *cable2*。

### 2) 加载虚拟分区应用软件

还必须将虚拟分区软件加载到将用于托管所有 vPars 的卷上。在撰写本文时，软件有 *base* 和 *full* 版本。*base* 软件的限制是最大两个 vPars，其中一个 vPar 中最大一个 CPU。在一个根卷上加载 vPars 软件后，我运行了 **swlist**，结果输出如下：

```bash
# swlist
# Initializing ...
# Contacting target "cvh3dcn3" ...
#
# Target:   cvh3dcn3 /
#
# Bundle(el):
#
BUNDLE11
usrv 2001 B.11.11.0202.2  Required  Exxct Bundle for HP-UX 11i. rev
C06-English B.11.11 English TCS Enforcement
FC01-00 B.11.11.01  PCI FDDISuppdrd Hw:A558A559A560A566
AA
FibrChannel-00 B.11.11.36  PCI/HSC FibreChannel/Suppdrd Hw:A56842,A56
85A.AD158A
GLGELther-00 B.11.11.14  PCI/HSC GigELther/Suppdrd Hw:A4926A/A4928A/
A4924A/A4925A/SW=31642A
HECX11-08-MC B.11.11.3136  HP-UX Mission Critical Operating Envirem
ent Component
HEXBase64 B.11.11  HP-UX 64-bit Base OS
HPUXBaseAux B.11.11.1500 HP-UX Base OS Auxiliary
HWEnableB11i B.11.11.324  Hardware Enablement Patches for HP-UX 11i
June 2001 B.11.11.05308 HPDX 11.11 Support Tools Bundle, Jun 2001
OnLineDiag
RAID-00 B.11.11.01  PCI RAID: Suppdrd Hw:A5856A
VPARSBASE A.03.05.01  HP-UX Virtual Partitions
```

*HP-UX Virtual Partitions* 软件是此列表中显示的最后一项。




### 使用 vPars 进行操作

在使用 vPars 时，您将深入了解您的硬件。您不仅需要知道系统由哪些组件构成，还需要知道许多硬件的路径。某些系统组件，如 `System Bus Adapters`（系统总线适配器）和 `memory controller`（内存控制器），在 vPars 之间是共享的，因此您不需要将这些组件作为各个虚拟分区的一部分进行指定。系统中的大多数其他组件，如处理器、I/O 卡、磁盘等，则固定分配到特定的 vPar 中。

为了查看示例系统由哪些组件组成，我们将在下面的列表中运行 `ioscan -f` 和 `dmesg`：

### ioscan -f 输出

```
# ioscan -f

Class	I	H/W Path	Driver	S/W State	H/W Type	Description
-------	-	------	------	--------	------	----------
root		0	root		root	CLAIMED		BUS_NEXUS	System Bus
ioa		0	0		fbaa	CLAIMED		BUS_NEXUS	Local PCI Bus
								Adapter (803)
ba		0	0/0		lba	CLAIMED		BUS_NEXUS	Local PCI Bus
								Adapter (782)
lan		0	0/0/0/0	blan	CLAIMED		INTERFACE	HP PCI 10/100
								Base-Tx Qwe
ext_bus	0	0/0/0		c720	CLAIMED		INTERFACE	SCSI C896
								Ultra Wide Single-Ended
target		0	0/0/1/0.1	tgt	CLAIMED		DEVICE	HP DVD-R30 304
disk		0	0/0/1/0.1.0	sdisk	CLAIMED		DEVICE	HP DVD-R30 304
target		1	0/0/3/0.3	tgt	CLAIMED		DEVICE
								HP C1537A
tape		0	0/0/3/0.3		stape	CLAIMED		DEVICE
								Initiator
c7i		2	0/0/3/0.7		scl1	CLAIMED		DEVICE	SCSI C896
ext_bus	1	0/0/3/1		c720	CLAIMED		INTERFACE	SCSI C896
								Ultra Wide Single-Ended
target		3	0/0/1/0		tgt	CLAIMED		DEVICE	SEAGATE ST17340 4LC
disk		1	0/0/1/0.1.0	sdisk	CLAIMED		DEVICE	SEAGATE ST17340 4LC
target		4	0/0/1/2		tgt	CLAIMED		DEVICE
disk		2	0/0/1/2.0	sdisk	CLAIMED		DEVICE	SEAGATE ST17340 4LC
target		5	0/0/3/0		tgt	CLAIMED		DEVICE
								Initiator
c7i		1	0/0/3/1		scl1	CLAIMED		DEVICE
ext_bus	2	0/0/2/0		c720	CLAIMED		INTERFACE	SCSI C67x
								Ultra Wide Single-Ended
target		6	0/0/3/0		tgt	CLAIMED		DEVICE	SEAGATE ST17340 4LC
disk		3	0/0/3/0.0	sdisk	CLAIMED		DEVICE	SEAGATE ST17340 4LC
target		7	0/0/3/2		tgt	CLAIMED		DEVICE
disk		4	0/0/3/2.0	sdisk	CLAIMED		DEVICE	SEAGATE ST17340 4LC
target		8	0/0/3/3		tgt	CLAIMED		DEVICE
c7i		2	0/0/3/3		scl1	CLAIMED		DEVICE
ext_bus	3	0/0/3/1		c720	CLAIMED		INTERFACE	SCSI C67x
								Ultra Wide Single-Ended
target		9	0/0/3/2/3		tgt	CLAIMED		DEVICE
c7i		3	0/0/2/7.7		scl1	CLAIMED		DEVICE
								Initiator
tty		0	0/0/4/0		aio0	CLAIMED		INTERFACE	PCI Serial
tty		1	0/0/5/0		aio0	CLAIMED		INTERFACE	PCI Serial
ba		1	0/1		lba	CLAIMED		BUS_NEXUS	Local PCI Bus
								Adapter (782)
ba		2	0/2		lba	CLAIMED		BUS_NEXUS	Local PCI Bus
								Adapter (782)
ba		3	0/3		lba	CLAIMED		BUS_NEXUS	Local PCI Bus
ba		4	0/4		lba	CLAIMED		BUS_NEXUS	Local PCI Bus
ba		5	0/5		lba	CLAIMED		BUS_NEXUS	Local PCI Bus
ba		6	0/6		lba	CLAIMED		BUS_NEXUS	Local PCI Bus
fc		0	0/8/0/0		td	CLAIMED		INTERLACE	HP Tachyon TL/TS
								Fibre Channel Mass Storage Adapter
fcp		0	0/8/0/0/0		fcp	CLAIMED		INTERLACE	Fibre Channel Mass Storage Adapter
ext_bus	4	0/8/0/0-0.5.0	ext_claimed_fcparray	CLAIMED		INTERLACE	FCP Protocol Adapter
ext_bus		4	0/8/0/0.8.0.0.0	fcpdev	CLAIMED		Device	Interface
ext_bus		4	0/8/0/0.8.0.255.0	fcpdev	CLAIMED		Device	Interface
target		10	0/8/0/0.0-0.5.0.0	tgt	CLAIMED		DEVICE
disk		11	0/8/0/0.0-0.5.0.0.0	sdisk	CLAIMED		DEVICE	HP AS277A
disk		12	0/8/0/0.0-0.5.0.0.1	sdisk	CLAIMED		DEVICE	HP AS277A
disk		13	0/8/0/0.0-0.5.0.0.2	sdisk	CLAIMED		DEVICE	HP AS277A
disk		14	0/8/0/0.0-0.5.0.0.3	sdisk	CLAIMED		DEVICE	HP AS277A
target		15	0/8/0/0.0-0.5.0.1	tgt	CLAIMED		DEVICE
disk		16	0/8/0/0.0-0.5.0.1.0	sdisk	CLAIMED		DEVICE	HP AS277A
target		17	0/8/0/0.0-0.5.0.2	tgt	CLAIMED		DEVICE
disk		18	0/8/0/0.0-0.5.0.2.0	sdisk	CLAIMED		DEVICE	HP AS277A
target		19	0/8/0/0.0-0.5.0.3	tgt	CLAIMED		DEVICE
disk		20	0/8/0/0.0-0.5.0.3.0	sdisk	CLAIMED		DEVICE	HP AS277A
ext_bus	5	0/8/0/0.0-0.5.0.0	fcpdev	CLAIMED		Device	Interface
target		21	0/8/0/0.0-0.255.0.5	tgt	CLAIMED		DEVICE
c7i		4	0/8/0/0.0-0.255.0.5	scil	CLAIMED		DEVICE	HP AS277A
ba		7	0/9		lba	CLAIMED		BUS_NEXUS	Local PCI
fc		1	0/9/0/0		td	CLAIMED		INTERLACE	HP Tachyon TL/TS Fibre Channel Mass Storage Adapter
fcp		1	0/9/0/0/0.8	fcp	CLAIMED		INTERLACE	FCP Protocol Adapter
ext_bus	6	0/9/0/0.0-0.4.0	ext_claimed_fcparray	CLAIMED		INTERLACE	FCP Protocol Adapter
target		22	0/9/0/0.0-0.4.0.0	tgt	CLAIMED		DEVICE
disk		23	0/9/0/0.0-0.4.0.0.0	sdisk	CLAIMED		DEVICE	HP AS277A
disk		24	0/9/0/0.0-0.4.0.0.1	sdisk	CLAIMED		DEVICE	HP AS277A
disk		25	0/9/0/0.0-0.4.0.0.2	sdisk	CLAIMED		DEVICE	HP AS277A
disk		26	0/9/0/0.0-0.4.0.0.3	sdisk	CLAIMED		DEVICE	HP AS277A
target		27	0/9/0/0.0-0.4.0.1	tgt	CLAIMED		DEVICE
disk		28	0/9/0/0.0-0.4.0.1.0	sdisk	CLAIMED		DEVICE	HP AS277A
target		29	0/9/0/0.0-0.4.0.2	tgt	CLAIMED		DEVICE
disk		30	0/9/0/0.0-0.4.0.2.0	sdisk	CLAIMED		DEVICE	HP AS277A
target		31	0/9/0/0.0-0.4.0.3	tgt	CLAIMED		DEVICE
disk		32	0/9/0/0.0-0.4.0.3.0	sdisk	CLAIMED		DEVICE	HP AS277A
ext_bus	7	0/9/0/0.0-0.255.0	fcpdev	CLAIMED		Device	Interface
target		33	0/9/0/0.0-0.255.0.4	tgt	CLAIMED		DEVICE
c7i		4	0/9/0/0.0-0.255.0.4	scil	CLAIMED		DEVICE	HP AS277A
ba		6	0/10		lba	CLAIMED		BUS_NEXUS	Local PCI
lan		1	0/10/0/0	blan	CLAIMED		INTERLACE	PCI I/O Adapter-TX Add-on
ba		9	0/12		lba	CLAIMED		BUS_NEXUS	Local PCI
lan		2	0/12/0/0	blan	CLAIMED		INTERLACE	PCI I/O Adapter-TX Add-on

pbc		0	pbc		CLAIMED		BUS_NEXUS		Bus Converter
processor	1	pbc		CLAIMED		PROCESSOR		Processor
pbc		2	pbc		CLAIMED		BUS_NEXUS		Bus Converter
processor	3	pbc		CLAIMED		PROCESSOR		Processor
pbc		4	pbc		CLAIMED		BUS_NEXUS		Bus Converter
processor	5	pbc		CLAIMED		PROCESSOR		Processor
pbc		6	pbc		CLAIMED		BUS_NEXUS		Bus Converter
processor	7	pbc		CLAIMED		PROCESSOR		Processor
memory		8	memory	CLAIMED		MEMORY		Memory
```

### dmesg 输出

```
# dmesg

Jul 31 20:03
NOTICE: mwwav vadpr 6 xcc0020000 for 2 pages.
NOTICE: nssl link (): File system was registered at index 3.
NOTICE: autofs. link (): File system was registered at index 6.
NOTICE: cachefs. link (): File system was registered at index 7.
0 lbx
0/0/0/0 blan
0/0/0/0 c720
0/0/1/0.1 tgt
0/0/1/0.1.0 sdisk
0/0/1/0.3 stape
0/0/1/0.3.0 tgt
0/0/1/0.7 scl1
0/0/1/1 c720
0/0/1/1.0 tgt
0/0/1/0.0 sdisk
0/0/1/0.0 tgt
0/0/1/2.0 sdisk
0/0/1/2.0 tgt
0/0/1/2.1 tgt
0/0/1/3.0 sdisk
0/0/1/3.0 tgt
0/0/1/3.1 tgt
0/0/1/4.0 sdisk
0/0/1/4.0 tgt
0/0/1/5.0 c720
0/0/1/5.7 tgt
0/0/1/5.7.0 sdisk
0/0/4/0 aio0
0/0/5/0 aio0
0/1 lba
0/2 lba
0/3 lba
0/4 lba
0/5 lba
0/6 lba
0/7 lba
0/8 td
0/8/0/0 td
0/8/0/0.0 fcp
0/8/0/0.8.0.0.0 tgt
0/8/0/0.8.0.5.0.0.0 sdisk
0/8/0/0.8.0.5.0.0.1 sdisk
0/8/0/0.8.0.5.0.0.3 tgt
0/8/0/0.8.0.5.0.0.3 sdisk
0/8/0/0.8.0.5.0.1 tgt
0/8/0/0.8.0.5.0.2 sdisk
0/8/0/0.8.0.5.0.2 tgt
0/8/0/0.8.0.5.0.2 sdisk
0/8/0/0.8.0.5.7.1 tgt
0/8/0/0.8.0.255.0.2 fcpdev
0/8/0/0.8.0.255.0.5 tgt
0/8/0/0.8.0.255.0.5 scil
0/9 lba
0/9/0/0 td
0/9/0/0 td
td: claimed Tachyon TL/S Fibre Channel Mass Storage card at 0/9/0/0
0/9/0/0.0 fcp
0/9/0/0.8.0.0.0 fcparray
0/9/0/0.8.0.4.0.0 tgt
0/9/0/0.8.0.4.0.0 sdisk
0/9/0/0.8.0.4.0.0.2 sdisk
0/9/0/0.8.0.4.0.0.2 sdisk
0/9/0/0.8.0.4.0.0.3 tgt
0/9/0/0.8.0.4.0.0.3 sdisk
0/9/0/0.8.0.4.0.1 tgt
0/9/0/0.8.0.4.0.2 tgt
0/9/0/0.8.0.4.0.2 sdisk
0/9/0/0.8.0.4.0.3 tgt
0/9/0/0.8.0.4.0.3.0 sdisk
0/9/0/0.8.0.255.0.4 fcpdev
0/9/0/0.8.0.255.0.4 scil
0/10/0 blan
0/12 lba
0/12/0/0 blan
32 pbc
33 processor
36 pbc
37 processor
96 pbc
97 processor
100 pbc
101 processor
192 memory
blan: Initializing 10/100BASE-TX card at 0/0/0/0....

System Console is on the Built-In Serial Interface
blran: Initializing 10/100BASE-TX card at 0/10/0/0....
blran: Initializing 10/100BASE-TX card at 0/12/0/0....
Entering cifs_init....

Initialization finished successfully....sios is 9
Logical volume 64_0x3 configured as ROOT
Logical volume 64_0x2 configured as SWAP
Logical volume 64_0x2 configured as DUMP

Swap device table: (start & size given in 512-byte blocks)

entry 0 - major is 64, minor is 0x2; start = 0, size = 8388608
Dump device table: (start & size given in 1-byte blocks)

entry 0 - major is 33, minor is 0x12200: start = 17550, size = 4193404
Starting the STREAMS daemon-phase 1
Create STCP device files
Starting the STREAMS daemon-phase 2
`\`\$envision; \vmunix; -w; -pro] selectors: CUP180 BL2L000_1108 -c "Vw for CUP180 BL2L000_1108 bl1d" -cupc180_bl2z00_0 L108 -kxj
Nov 8 19:24:56 FST 2000 S
Memory Information:

physical page size = 4096 bytes, logical page size = 4096 bytes
Physical: 4193404 Kbytes, Lockable: 3231756 Rbytes, available: 3711728 Rbytes
```

**ioscan -f** 和 **dmesg** 的输出提供了关于我们的系统的许多有用信息。我们将使用 **ioscan** 输出中的组件和路径以及 **dmesg** 中的内存信息，在下一步中为各自的 vPar 创建组件列表。例如，我们现在知道两块 LAN 卡的路径分别位于 `0/0/0/0` 和 `0/10/0/0`。我们知道所有四个处理器的路径为 `33, 37, 97, and 101`。控制台位于 `0/0/4/0`。从 **dmesg** 输出中我们知道，我们有总计 4 GB 的 RAM 可以分配给各个 vPar。

从这两个输出中，我们获得了在下一步创建虚拟分区所需的信息。



### 4) 列出虚拟分区的组件

从 **ioscan** 和 **dmseg** 消息中，我们可以选择第一个虚拟分区的组件。以下是我们将包含在此分区中的组件列表：

第一个 *vPar* *cable*
- 名称 cable1
- 处理器 最少一个（绑定） 最多三个（两个未绑定），其中 数量（绑定 + 未绑定）等于 一
- 内存 1024 MB
- LBA 核心 I/O 0/0（0/0 上的所有组件均为隐含项）
- LAN 0/0/0/0（未显式指定，位于 0/0 上）
- 引导磁盘 0/0/1/1, 2, 0
- 内核 /stand/vmmunix（这是默认值）
- 自动引导 关闭（手动）
- 控制台 0/0/4/0（未显式指定，位于 0/0 上）

您可能希望在安装过程中将 *autoboot* 设置为 **auto**，并在安装完成后将其设置为 *manual*。这使得安装过程中的引导更加容易。

其中一些组件需要对其在 vPar 中的实现方式提供一些解释。以下是对其中一些组件的更详细讨论，包括 CPU、内存、LAN、bootdisk、setboot、内核和控制台。

### CPU

在此分区（*cable1*）中使用的 CPU 以及我们稍后将定义的分区（*cable2*）中的 CPU，是通过 *min*、*max* 和 *num* 指定的。我们将拥有 *min 绑定* 的 CPU，这些 CPU 被分配了 I/O 中断，因此非常适合 I/O 密集型应用。分配给 vPar 的额外 CPU 是 *未绑定的*，它们不处理 I/O 中断。因此，与 I/O 密集型应用相反，*未绑定* 的 CPU 非常适合处理器密集型应用。*未绑定* 的 CPU 可以在 vPar 运行时从一个 vPar 自由移动到另一个 vPar，因此拥有 *min 绑定* 的 CPU 给了我们移动未绑定 CPU 的自由度。只有当分区关闭时，绑定 CPU 才能被添加或从虚拟分区中删除。

在使用非统一内存访问（NUMA）的机器上，您需要使用硬件路径（path）来指定 CPU。这是为了确保最小化 CPU 和内存之间的距离。在 N-Class 和 L-Class 等不使用 NUMA 的系统上，建议使用 min 来定义绑定 CPU。

第 5 章中包含了关于处理 CPU 的详细信息。对于我们在线缆 1 和线缆 2 上的工作，以及我对 vPar 的总体工作来说，最常见的需求是在所有 vPar 中拥有 min 数量的绑定 CPU，然后根据 vPar 中应用程序的需求移动未绑定的 CPU。例如，当运行 vparcreate 时，我们将指定以下内容：

```
vparcreate -p cable1 -a cpu:::1:3 -a cpu::1
```

在创建时，cable1 将只有一个绑定 CPU，因为我们指定了 min 为 1 且 num 为 1。num 是绑定 + 未绑定 CPU 的总数，由于我们为 num 指定了 1，我们将获得一个绑定 CPU（我见过一些 vPars 资料使用 num，一些使用 total，因此在本书中 num 和 total 是可以互换的。）由于 max 是 3，我们保留了对添加最多两个额外未绑定 CPU 的可能性。如果我们的系统上有两个未绑定 CPU，我们可以根据需要通过 vparmodify 在 vPar 之间移动它们。要从 cable2 中移除两个未绑定 CPU 并将它们添加到 cable1，我们将发出以下两个 vparmodify 命令：

```
vparmodify -p cable2 -m cpu::1		# 将 cable2 从 3 减少到 1
vparmodify -p cable1 -m cpu::3		# 将 cable1 从 1 增加到 3
```

我们首先从 cable2 中移除了两个未绑定 CPU，然后将它们添加到 cable1。如果这两个未绑定 CPU 未分配给任何 vPar，我们在将它们添加到 cable1 之前就不必从 cable2 中移除它们。

处理 CPU 有很多方法，其中一些在第 5 章中有描述，因此通过表征您的应用程序并理解使用绑定和未绑定 CPU 的选项，您可以使用最能满足您需求的处理器组合。

### 内存

我们已为 *cable1* 识别了 1 GB 的内存。内存可以通过 *range* 或 *size* 来指定。

使用 *size* 向 *cable1* 添加 1 GB 内存，我们将使用以下 *vparcreate* 命令：

```
vparcreate -p cable1 -a mem::1024
```

此 *vparcreate* 命令仅指定用于 *cable1* 的内存。用于创建 *cable1* 的完整 **vparcreate** 命令将在接下来的部分中展示。

内存以 MBytes 为单位指定（1024 MBytes = 1 GByte），并且是 64 MBytes 的倍数。截至今日，虚拟分区监视器消耗大约 128 MBytes 的 RAM，因此这部分内存无法分配给虚拟分区。截至今日，修改内存分配要求虚拟分区处于关闭状态。

在使用非统一内存访问（NUMA）的机器上，您应使用 *range*。*Range* 是 *size* 的子集。在 N-Class 和 L-Class 等不使用 NUMA 的系统上，建议使用 *size* 来定义内存。通过 range 指定内存的语法如下：

```
mem:::base::range
```

本书中的示例均不是使用 NUMA 系统准备的，因此您不会看到使用 *range* 语法的示例；所有示例都使用 *size* 语法。

### LAN

用于此第一个虚拟分区的 LAN 接口位于本地总线适配器（LBA）零上。这意味着位于 LBA 零上的任何其他组件也必须在此虚拟分区中。截至今日，LBA 上的组件无法在 vPar 之间共享。

![](img/eff8b9287a5f38c5adf538f24aacf29e_118_0.png)

请注意，我们决定不使用主机名作为虚拟分区名称。如前所述，使用相同的主机名和 vPar 名称是可取的。由于我们的主机名有点难以记忆，系统管理员决定使用简单的 vPar 名称。当我们在系统上加载 HP-UX 11i 时，我们选择了主机名（您也可以在加载 11i 后运行 set_parsns 来设置系统名称和其他参数）cvhdcn3 和 cvhdcn4。然后我们分别选择了简单的 vPar 名称 cable1 和 cable2。

### 引导磁盘

本章早前发出的 ioscan 显示了许多磁盘设备。我们第一个虚拟分区的引导设备是硬件路径为 0/0/1/1/2.0 的内部磁盘。

截至今日，位于本地总线适配器（LBA）级别或更下级（即硬件更底层）的组件将专属于单个虚拟分区。这意味着，尽管我们早前 ioscan 命令的输出显示了四个内部磁盘，但由于它们位于同一个 LBA 上，因此这四个磁盘必须在同一个虚拟分区中。第 5 章更详细地介绍了 LBA 和硬件。

### 内核

![](img/eff8b9287a5f38c5adf538f24aacf29e_119_0.png)

我们将使用默认的 HP-UX 内核 /stand/vmunix 作为此虚拟分区的内核。由于我们使用的是默认内核，因此不必在 vparcreate 命令中将其指定为的一部分，但为了完整性，我们仍将在 vparcreate 命令中包含它。第 4 章介绍了 HP-UX 内核。

### setboot 命令

在我们的示例中，我们为虚拟分区将 autoboot 设置为 off。在非 vPars 系统上，setboot 命令从稳定存储读取并写入。在 vPars 系统上，setboot 命令与虚拟分区数据库进行交互。在我们接下来的示例中，当我们使用 vparcreate 创建 cable1 时，我们将把 autoboot 设置为 off。在 vPars 系统上运行 setboot 的效果如表 2-2 所示：

| vPars setboot 选项 | 描述 |
| :--- | :--- |
| `-a` | 更改虚拟分区的备用引导路径。<br> 要设置备用引导路径：<br> `# setboot -a 0/8/0/0.8.0.5.0.0.0` |
| `-b` | 设置虚拟分区的自动引导属性。<br> 要打开自动引导：<br> `# setboot -b on` |
| `-p` | 更改虚拟分区的主引导路径。<br> 要设置主引导路径：<br> `# setboot -p 0/0/1/1.2.0` |
| `-s` | 没有效果。 |
| `无选项` | 显示有关引导属性的信息。 |

**setboot** 命令是处理 vPars 的方面之一，它与非 vPars 系统不同。

### 控制台

第 5 章包含了对 vPars 中控制台实现方式的描述。在我们的第一个分区中，我们已指定 LBA 0/0 为 vPar cable1 的一个组件。由于位于 0/0/4/0 的物理控制台位于 0/0 的核心 I/O 卡上，它是 cable1 的一个隐含组件，我们不必在此分区中指定物理控制台。此系统上的其他虚拟分区将使用 vPars 的虚拟控制台功能，发出 Ctrl-A 会在虚拟控制台显示之间切换。




## 数据库

包含所有*vPar*相关信息的*虚拟分区*数据库是/stand/vp.db。该数据库已为您管理并同步（如第8章所述），因此如果您不想过多关注，完全可以忽略它。不过，如果您愿意，可以创建一个替代数据库。您可能会希望这样做，以便为您的系统创建完全不同的*虚拟分区*配置，而不影响当前正在运行的数据库。

![](img/eff8b9287a5f38c5adf538f24aacf29e_121_0.png)

在使用**vpcreate**创建*虚拟分区*时，您可以使用*-D*选项并指定一个位于/stand目录下的替代数据库文件名，例如/stand/vpdb.app2。当您从此数据库启动vParS时（通过**ISL>** hpux /stand/vpmon -D db_file），该数据库将成为默认数据库，因此所有对此数据库中定义的*vParS*所做的修改都将应用于该数据库，而不是默认数据库。

## 第二个vPar *cable2*

我们将在下文中为*cable2*列出与*cable1*相同类别的组件：

- 名称：*cable2*
- 处理器：最少1个（绑定），最多3个（其中2个未绑定）
- 内存：绑定和未绑定总数等于1的1024 MB
- 局域网：0/10/0/0
- 引导磁盘：0/8/0/0/0.8.0.5.0.0.0 /stand/vmunix（这是默认值）
- 自动引导：关闭（手动）
- 控制台：将创建虚拟控制台

现在，我们拥有了两个*vParS*的组件列表。其结果是我们的L-Class系统被划分为两个如图2-4所示的*vParS*：

![](img/eff8b9287a5f38c5adf538f24aacf29e_122_0.png)

图 2-4 包含两个vPar的L-Class（未显示的组件未展示）

图2-4反映的是我们在执行即将进行的步骤来创建两个vPar时，系统的最终形态。请注意，两个*未绑定*处理器（在图2-4中显示为2,3）可以根据需要分配给*cable1*和*cable2*。

### 5) 虚拟分区内核相关工作

每个虚拟分区都有自己的HP-UX 11i实例，并且拥有自己的HP-UX内核。您很可能会以多种方式定制这些内核，以适应在相应vPar中运行的应用程序。当您安装vPars软件时，它会自动重新配置内核以包含vPar驱动程序并使内核可重定位。由于在加载vPars软件时已为您执行了这些内核相关步骤，因此您无需手动执行本节中的内核相关步骤。不过，查看本节中手动执行的步骤仍然具有信息价值，有助于更好地理解vPars的工作方式。在这一步中，我们将调查由vPars应用程序更新的构建新内核所需文件。请记住，每个安装了HP-UX 11i并运行vPar的卷上都需要构建新内核。

由于内存由多个vPar共享，内核必须在内存中可重定位。在撰写本文时，存在允许将内核构建为可重定位内核的补丁。我们不会执行与补丁相关的任何检查。

文件/sbin/vrecheck是系统中必需的vPar文件。以下是/usr/conf/gen/config.sys中用于检查/sbin/vrecheck是否已在系统上加载的部分内容：

```
# 确定链接器是否支持内核重定位。
# 使用重定位选项链接内核。
LOADOPTS_ADDL=`
        if [ -f /sbin/vrecheck ]; then  \
            $(WRK)/$(IZ) \
            $(AWK) '$0 == "92453-7 linker" { \
                if ( vers[1] == 9 && \
                    ( vers[2] == 11 || vers[3] >= 25 ) || vers[2] > 11 ) \
                        print "${LOADOPTS_RELOC}"; \
                    else print "${LOADOPTS_STATIC}"; }
            fi;`
```

以下是随vPar软件加载的/sbin/vrecheck的较长列表：

```
# ll /sbin/vrecheck
-r-Xr-Xr-X 1 bin     bin  20533 Mar  5 19:01 /sbin/vrecheck
#
```

接下来让我们查看/stand/system，看看已添加到文件中的vpar驱动程序：

```
# cat /stand/system
****************************************************************
* 源文件: /ux/core/kern/filesets.info/CORE-KRN/generic
* @(#)B.11.11_LR
*
****************************************************************
* 在每种机器类型中创建完整
* 系统文件时所需的其他驱动程序。此列表包括所有
* master.d/ 文件未强制安装到系统或 ioscann 无法识别的驱动程序。
* 可能还存在针对特殊情况的CPU类型特定文件。
* 参见 create_sysfile (1m)。
****************************************************************
*
* 驱动程序/子系统
gba
lba
c720
sctl
tdisk
as100
cdfs
cxperf
clar_psm
clar_psm_if
dev_Clar
diag0
diag1
diag2
Dmem
dev_Config
iomem
nfs_core
nfs_client
nfs_server
htlan
maclan
dlpi
token_arq
inet
uipc
tun
telm
tels
netdiag1
nms
```

```
hpstreams
c1one
strlog
sad
echo
sc
timod

tirdwr
pipede
pipemod
ffs
ldterm
ptem
pts
ptm
pckt
td
tddi4

gelan

gsCtoPCI
iop_drv
bs_Gem
vxfs
vxporta1
lvm
lv
n
tm
xpcmod
auto
fsc
cache
fsc
cifs
prn
vpar

tRMMS
G

str
ptp

在此处添加vpar驱动程序

st

lvol
dump
l
v
o1

maxsw
apchunks

#STRMMS
G
SZ# st
r
pt
p
lvo1dump
maxswap
chunks

#STRMMS
G
SZ# st
r
pt
p
lvo1dump
maxsw
apchunks

655
35

60

2048

#str
p
G

n		
d	ump

l
vol

maxswapchunks


#STRMMS
G
SZ# st
r
pt
p
lvo1dump
maxswapchunks
```

vpar驱动程序是一个主驱动程序，描述在`/usr/conf/master.d`中，如下所示：

```
$ pwd
/usr/conf/master.d
$ cat vpar
$CDIO

vpar

0

$$

$DRIVER
INSTALL
vcl

-1

209
vcs

-1
```

vpar_driver -1 -1
$$$

$DRIVER_DEPENDENCY
vcc vpar
vcs vpar
vpar vcs vcn vpar_driver
vpar_driver vpar
$$$

```
$DRIVER_LIBRARY

* 驱动程序/库表。此表定义了给定驱动程序
* 依赖于哪些库。如果驱动程序包含在dfile中，则
* 该驱动程序所依赖的库将包含在ld(1)命令
* 行中。只有可选库*需要*在此表中指定，
* （但必需库也可以包含在内）。

* 驱动程序句柄 <库>

* 子系统优先。

vcc libvpar-pdk.a
vcs libvpar-pdk.a
vpar libvpar-pdk.a
vpar_driver libvpar-pdk.a ,
$$$
```

```
$LIBRARY

* 库表。库表中的每个元素描述
* 一个唯一的库。标志成员是一个布尔值，如果库应*始终*
* 包含在ld(1)命令行中，则初始化为1；
* 如果是可选库（即只有在
* 一个或多个驱动程序需要时才包含），则初始化为0。
* 库表的顺序决定了ld(1)命令
* 行中库的顺序（即定义了隐式加载顺序）。
* 新库必须添加到该表中。
* 注意：libhp-ux.a必须是最后一个条目，请勿在其后
* 放置任何内容。
* 库 <必需>
libvpar-pdk.a 0
$$$
#
```

您可以在此文件中看到存在多个驱动程序。vcn和vcs驱动程序用于支持vPars环境中的控制台。由于您通常只为多个分区配备一个物理控制台，因此需要一种共享物理设备的方式。第4章介绍了这些驱动程序的使用方法，其中涵盖了内核配置。目前，只需知道这些驱动程序作为vPars安装的一部分存在，并且必须构建到内核中即可。

既然内核已具备构建可重定位内核所需的条件，且vPars所需的驱动程序也已就位，我们就可以运行**mk_kernel**来构建新内核，并运行**kmpudate**将新的内核相关文件放入指定位置。此过程会自动为您完成，但以下命令展示了如何手动执行此过程：

```
# mk_kernel
正在生成模块: krm....
正在编译 /stand/build/conf.c...
正在加载内核...
正在生成内核符号表....
# kmpudate

已安排内核更新请求。

默认内核 /stand/vmunix 将在下一次系统关机或启动时
由新构建的内核 /stand/build/vmunix_test 更新。
#
```

请记住，此过程需要对所有将运行虚拟分区的HP-UX 11i操作系统执行。如第11章所述，内核的创建和修改也可以在SAM中进行。

### 6) 创建第一个虚拟分区

![](img/eff8b9287a5f38c5adf538f24aacf29e_127_0.png)

**vparscreate**命令用于创建vPar。该命令的摘要如表2-1所示，其手册页位于附录A。该命令的一般形式如下：

```
vparscreate -p vp_name [-B boot_attr] [-D db_file] [-S static_attr]
[-b kernel_path][-o boot_opts] [-a xsrc] [-a...]
```



创建此 vPar 时，我将 `vparcreate` 命令放入一个文件中，以便在创建第二个 vPar 时对其进行修改并执行。`vparcreate` 命令如下所示：

```
# cat /tmp/cable1
vparcreate -p cable1 -B manual -b /stand/vmunix -a cpu::1
-a cpu::1:3 -a mem::1024 -a io::0/0 -a io::0/0/1:2.0:boot
#
```

更改该文件权限并运行后，vPar `cable1` 成功创建。接下来，我们将启动刚刚创建的 vPar。

### 7) 启动第一个虚拟分区

既然第一个 vPar 已创建完毕，且内核已自动重建以支持 vPars，我们就可以启动名为 `cable1` 的第一个 vPar 了。

我们将启动第一个 vPar 并检查其状态。启动过程的详细步骤将在第 3 章中介绍；不过，我们需要在 `ISL>` 提示符下加载虚拟分区监视器（`vpmon`）。`vpmon` 是一个类似 `vmunix` 的 *ramdisk*（ ram 磁盘）内核，需要在启动时加载。我们将通过 `ISL>` 提示符运行 `vpmon` 以获取 `MON>` 提示符。然后，在 `MON>` 提示符下使用 `vparload` 启动我们的虚拟分区，如以下示例所示：

```
ISL> hpux /stand/vpmon
Boot
: disk(0/0/1/2,0,0,0,0,0,0)/stand/vpmon
421888 + 142056 + 4247112 start 0x23000
cable1: WARNING: No boot device specified

Welcome to VPMON (type '?' for a list of commands)

MON> vparload -p cable1

[MON] Console client set to cable1
[MON] cable1 loaded
```

在发出 `vparload` 命令后，你可能会看到与示例中不同的信息。无论如何，系统继续完成了剩余的启动过程，并启动了我们创建的那个名为 *cable1* 的虚拟分区。现在，我们已拥有分配给此虚拟分区的系统组件子集。

`vparload` 命令具有以下三种形式：

```
form1: vparload -all
form2: vparload -auto
form3: vparload -p vp_name [-b kernelpath] [-o boot_options]
       [-B hardware_path]
```

我们使用的是上面显示的第三种形式。有关所有 *MON>* 命令的详细说明，请参阅第 3 章。

既然分区已启动，让我们首先获取我们创建并正在运行的那个名为 *cable1* 的虚拟分区的状态：

```
# vparstatus -p cable1 -v

[Virtual Partition Details]
Name:        cable1
State:       Up
Attributes:  Dynamic, Manual
Kernel Path: /stand/vmunix
Boot Options:
	
[CPU Details]
Min/Max:     1/3
Bound by User [Path]:
Bound by Monitor [Path]:  33
Unbound [Path]:

[IO Details]
        0.0
        0.0.1.1.2.0       BOOT

[Memory Details]
Specificified [Base /Range]:
                  (bytes)    (MB)
Total Memory (MB): 1024
#
```

`vparstatus` 的输出显示 `cable1` 处于 `up`（运行）状态。-v 选项用于获取详细输出。从该列表中可以看出，硬件路径 33 上绑定的 CPU（即通过 `min` 指定的 `bound CPU`）是分区的组成部分，分区中有 1 GB 内存，且我们指定的 `I/O` 组件也在分区内。如果配置了其他分区，我们也会看到它们的输出。

请注意，位于 `0/0/4/0` 的控制台是该 `vPar` 的隐含组件。位于 `0/0/0/0` 的 `LAN` 接口也是如此。这两个组件都是我们在 `vparcreate` 命令中通过 `-a io:0/0` 参数指定为 `cable1` 一部分的 `Core I/O` 卡的一部分。

我们现在可以运行 `vparstatus -A` 来查看系统中可用的组件。由于我们创建的第一个分区只有一个 `CPU`，我们应该会看到三个 `CPUs` 和许多其他可用系统组件，如下所示：

```
# vparstatus -A

[Unbound CPUs (path)]: 37
                          97
                         101
[Available CPUs]: 3

[Available I/O devices (path)]: 0.1
                                0.2
                                0.3
                                0.4
                                0.5
                                0.8
                                0.9
                               0.10
                               0.12
                                32
                                36
                                96
                               100

[Unbound memory (Base /Range):   0x0/128
                   (bytes)  (MB)   0x000000/1856
                                  0x18000000/1088
[Available memory (MB)]: 3072
#
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_130_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_130_1.png)

该输出显示有许多组件可供我们的第二个分区使用。根据我们之前的规划练习，我们知道我们希望包含在第二个 vPar 中的组件，并且此 `vparstatus -A` 命令确认这些组件确实可用。

对于 *cable2*，我们最初想要一个 CPU，目前有三个可用。我们希望启动和 LAN 的 I/O 卡分别位于 *0/8* 和 *0/10*。我们希望有 1 GB 内存，目前大约有 3 GB 可用。我们已经具备进入创建 *cable2* 下一步所需的所有组件。

### 8) 创建第二个虚拟分区

![](img/eff8b9287a5f38c5adf538f24aacf29e_131_0.png)

我们之前列出了第二个分区应由哪些组件组成，并使用 `vparstatus -A` 命令确认这些组件仍然可用。HP-UX 11i 已加载在同一系统上用于创建第一个虚拟分区 *cable1* 的第二块磁盘上。我们可以创建第二个虚拟分区，我们将它称为 *cable2*。我们将在第一个分区运行时创建第二个分区，并从第一个分区启动第二个 vPar。

以下是我们之前为第二个 vPar 列出的组件：

```
name:         cable2
processors:   min of one (bound) max of three (two unbound)
              with num (bound + unbound) equal to one
memory:       1024 MB
LAN:          0/10
LBA:          0/8
boot disk:    0/8/0/0.8.0.5.0.0.0
kernel:       /stand/vmunix (this is the default)
auto:         off (manual)
console:      virtual console to be created
```

两个 vPar 的组件列表之间存在几处差异。我们使用了不同的 LAN 卡和启动磁盘。我们在两个 vPar 中以相同方式指定了 CPU，*min*（这将作为 *bound*）为一个，*max* 为三个。*num* 为一个，并让 vPars 软件识别那一个 *bound* 处理器。这两个虚拟分区将使用不同的 I/O 路径用于其设备。

## 创建虚拟分区的步骤

现在让我们运行 **vparcreate** 命令来创建 **cable2**：

我们现在可以执行以下文件中的命令来创建第二个分区：

```
# cat /tmp/cable2
vparcreate -p cable2 -B manual -b /stand/vmunix -a cpu::1
-a cpu::1:3 -a mem::1024 -a io:0/8
-a io:0/8/0/0.8.0.5.0.0.0:boot -a io:0/10
#
```

执行此文件后，我们可以通过运行 **vparstatus** 来确定第二个 vPar 是否已创建以及它由哪些组件组成：

```
# vparstatus -v

[Virtual Partition Details]
Name:    cable1
State:   Up
Attributes: Dynamic, Manual
Kernel Path: /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max: 1/3
Bound by User [Path]:
Bound by Monitor [Path]: 33
Unbound [Path]:

[IO Details]
 0.0
  0.0.1.1.2.0 BOOT

[Memory Details]
Specified [Base /Range]:
           (bytes) (MB)
Total Memory (MB): 1024

[Virtual Partition Details]
Name:    cable2
State:   Down
Attributes: Dynamic, Manual
Kernel Path: /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max: 1/3
Bound by User [Path]:
Bound by Monitor [Path]: 37
Unbound [Path]:

[IO Details]
0.8
0.8.0.0.8.0.5.0.0.0.0, BOOT
0.10

[Memory Details]
Specified [Base /Range]:
(bytes) (MB)
Total Memory (MB): 1024
#
```

此输出显示第一个 vPar 保持完整，且第二个 vPar 已成功创建，包含我们指定的名称、内核文件、CPU、I/O 和内存组件。请注意，每个 vPar 都有一个分配给它的绑定 CPU。分配给 *cable2* 的 LAN 卡出现在输出中，是因为我们指定了 LBA 0/10 作为 *cable2* 的组件之一。位于 0/0/4/0 的控制台和位于 0/0/0/0 的 LAN 接口是 *cable1* 的隐含组件，不会出现在 **vparstatus -v** 输出中。

创建好第二个 vPar 后，我们可以继续下一步并启动它。

![](img/eff8b9287a5f38c5adf538f24aacf29e_133_0.png)

### 9) 启动第二个虚拟分区

既然我们已经有一个名为 *cable1* 的第一个 vPar 在运行，并且已经创建了名为 *cable2* 的第二个 vPar，我们就可以从第一个 vPar 启动第二个 vPar。启动 vPars 有很多选项。由于第一个 vPar 已经在运行，我们将简单地使用 **vparboot** 从第一个 vPar 启动第二个 vPar，然后运行 **vparstatus -v**，如下例所示。如果我们输入后续的 **vparstatus** 命令，我们可以在下一个输出中看到 vPar *cable2* 的状态从 *Down* 变为 *Boot*，最后当 vPar 运行时变为 *Up*，如下所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_133_1.png)





## vparboot -p cable2

vparboot：正在引导 cable2。请稍候...

## vparstatus

**[虚拟分区]**

虚拟分区名称 状态 属性 内核路径 引导选项
cable1 Up Dyn,Mani /stand/vmunix
cable2 Load Dyn,Mani /stand/vmunix

**[虚拟分区资源摘要]**

CPU 轮换- 数量 内存 (MB)
| 虚拟分区名称 | CPU 最小/最大 | 绑定/ 未绑定 | I/O 设备 | # 范围/ 总计 MB | 总计 MB |
|---|---|---|---|---|---|
| cable1 | 1/ 3 | 1 | 0 | 4 | 0/ 0 | 1024 |
| cable2 | 1/ 3 | 1 | 0 | 4 | 0/ 0 | 1024 |

*cable2* 状态的这种演变反映了在此 vPar 所运行的第二个卷上引导操作系统所需的时间。

除了 *load（加载）、boot（引导）和 up（运行）* 之外，你可能会发现虚拟分区处于其他状态。表 2-3 总结了撰写本文时虚拟分区的状态：

### 表 2-3 虚拟分区状态

| vPar 状态 | 描述 |
|---|---|
| load | 正在将虚拟分区内核映像加载到内存中。这是由虚拟分区监视器完成的。 |
| boot | 虚拟分区正在引导过程中。内核映像已由虚拟分区监视器成功加载。 |
| up | 虚拟分区已成功引导并正在运行。 |
| shut | 虚拟分区正在关闭过程中。 |
| down | 虚拟分区未运行且已停止。 |
| crash | 虚拟分区已发生恐慌并正在崩溃。 |
| hung | 虚拟分区无响应且已挂起。 |

当有多个 vPar 同时运行时，你可以使用内置的 vPar 驱动程序通过 Ctrl-A 在任意数量的虚拟分区之间切换控制台。图 2-5 展示了使用控制台查看主机名为 cvhdcon3 的 cable1。发出 Ctrl-A 连接到主机名为 cvhdcon4 的 vPar cable2。当你在控制台中发出 Ctrl-A 切换到下一个 vPar 时，系统会在方括号中提供你所连接的 vPar 的名称，例如 [cable1]。

![](img/eff8b9287a5f38c5adf538f24aacf29e_136_0.png)

**图 2-5 使用 Ctrl-A 在 vPar 之间切换时显示的控制台**

除了使用控制台在 vPar 之间切换外，还可以使用配置到特定 vPar 的 LAN 卡来打开 TELNET 或其他类型的会话到 vPar。这是你可以在网络上连接任何系统所使用过的同一种技术，而且它也是你始终希望在每个 vPar 中配置一个 LAN 卡的主要原因。

在本章中，我们没有涵盖在 vPar 中配置两个 LAN 卡的内容。为了在两个 vPar 中在网络操作中使用网卡，需要对两个 vPar 都完成 LAN 的配置。第 13 章涵盖了许多网络主题，包括 /etc/hosts 文件；/etc/rc.configd/netconf 文件，它必须在每个 vPar 上配置；以及许多其他内容。

### 10) 修改虚拟分区

你很可能会希望以多种方式修改你的虚拟分区。例如，你可能想要添加或移除一个 CPU。让我们来看看向虚拟分区添加 CPU 的一个示例。

在下面的示例中，有一个四处理器系统，其中包含我们刚才创建的两个虚拟分区：cable1 和 cable2。每个 vPar 都有一个绑定 CPU，这是在创建 vPars 时由 min 分配的。让我们运行 vparstatus 来查看这两个虚拟分区由哪些组件组成，并确认每个都有 1 个绑定 CPU：

```
# vparstatus -p cable1 -v

[Virtual Partition Details]
Name:                 cable1
State:                Up
Attributes:           Dynamic,Manual
Kernel Path:          /stand/vmunix
Boot Opts:
[CPU Details]
Min/Max:      1/3
Bound by User [Path]:
Bound by Monitor [Path]: 33      < - one bound CPU @ 33
Unbound [Path]:

[IO Details]
0.0
0.0.1.1.2.0  BOOT

[Memory Details]
Specified [Base  /Range]:
        (Bytes)      (MB)
Total Memory (MB): 1024
#
```

```
# vparstatus -p cable2 -v

[Virtual Partition Details]
Name:                 cable2
State:                Up
Attributes:           Dynamic,Manual
Kernel Path:          /stand/vmunix
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_137_0.png)

## 创建虚拟分区的步骤

```
Boot Opts:  
[CPU Details]  
Min/Max: 1/3  
Bound by User [Path]:  
Bound by Monitor [Path]: 37 <!-- one CPU in use at 37 -->  
Unbound [Path]:  
[IO Details]  
0.8.0.0.8.0.5.0.0.0 BOOT  
3.0.0.0.0  
[Memory Details]  
Specified [Base /Range]:  
(bytes) (MB)  
Total Memory (MB): 1024  
#
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_138_0.png)

这两个 **vparstatus** 命令的输出显示，`cable1` 有一个 *绑定* CPU，`cable2` 也有一个 *绑定* CPU。在这些 vPars 所创建的 L 类系统上，总共有四个 CPU。这意味着应该有两个 CPU 可用。让我们运行 **vparstatus -A** 来查看系统中的可用组件：

```
# vparstatus -A
[Unbound CPUs (path)]: 97 101
[Available CPUs]: 2

[Available I/O devices (path)]: 0.1 0.2 0.3 0.4 0.5 0.9 0.12 32 36 96 100
[Unbound memory (Base /Range)]: 0x0/64 0xC000000/1856 (bytes) (MB)
[Available memory (MB)]: 2048
#
```

此输出确认在硬件路径 97 和 101 处有两个 CPU 可用。我们可以通过多种方式添加这些 CPU。让我们使用 `vparmodify` 命令将 `cable1` 中的 `num` 个 CPU 更改为两个 CPU。我们通过使用 `-a` 在当前 CPU 数量的基础上 *添加* 一个来实现这一点。这是一个相对操作，即将在当前 CPU 数量的基础上添加一个 CPU。如果你希望指定 vPar 的绝对 CPU 数量而不是相对数量，可以使用 `vparmodify -m`。以下是该 `vparmodify` 命令的示例：

![](img/eff8b9287a5f38c5adf538f24aacf29e_139_0.png)

```
# vparmodify -p cable1 -a cpu::1
#
```

我们现在可以运行 `vparstatus -p cable1 -v` 来确认 CPU 已被添加，如下所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_139_1.png)

```
# vparstatus -p cable1 -v

[Virtual Partition Details]
Name:             cable1
State:            Up
Attributes:       Dynamic,Manual
Kernel Path:      /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max:  1/3
Bound by User [Path]:       <-- original CPU @ 33
Bound by Monitor [Path]:  33
Unbound [Path]:   97       <-- unbound CPU @ 97

[IO Details]
    0.0
    0.0.1.1.2.0  BOOT

[Memory Details]
Specified [Base  /Range]:
                (bytes) (MB)
Total Memory (MB):  1024
#
```

`vparstatus` 的输出显示，位于硬件路径 97 的 CPU 确实已通过 `vparmodify` 命令作为 *未绑定* CPU 添加到 `cable1` 中。

此外，我们可以运行 GlancePlus 或 **top** 来确认在 *cable2* 中有两个 CPU 正在使用。以下是在 *cable2* 上运行的 **top** 输出：

```
# top
System: cvhdc0n3
Load averages: 0.19, 0.51, 0.62    Thu Oct 4 15:30:42 2001
124 processors: 110 sleeping, 14 running
CPU states:
    CPU LOAD  USER  NICE  SYS    IDLE BLOCK SWAIT INTR   %VS
      0  0.37  0.0%   0.2%  0.3%  99.4%    . . .   . . .   0.0%   0.0%
      1  0.02  0.0%   0.0%  0.0%  99.2%    . . .   0.0%   0.0%   0.0%

    avg  0.19  . . .  0.2%  0.4%  99.4%    . . .   0.0%   0.0%   0.0%

Meminfo: 9365K (5781K)  real, 32214K (21936K) virtual, 74285K free     Page 1/4

PID    PPID USER NAME PRI  NI  SIZE  RES  STATE   TIME  %CPU  %MEM COMMAND
    0    0    root    -15   2    0K    0K    run    0:00  0.11  0.11 wakef
    1    0    root    150   10   88K   232K sleep   0:10  0.28  0.28 cdcload
    0    1    ---     -15  -20  4644K  7260K run   0:06  0.21  0.21 pwrshd
    0    1    ---     -15  -20   540K   800K sleep   0:06  0.15  0.15 hpgcmon
    1 pty/ttypl 3114 root  184  20   596K   528K run   0:00  0.14  0.15 cgp
    1  ?    1146 root  -15  -20  7768K  7240K run   0:03  0.14  0.13 madcmom
    3  ?    3 root   128   20    OK    32K sleep   0:06  0.11  0.11 atd/dcdaemon
    0  ?    2018 root  150   20   3968K  1908K sleep   0:00  0.05  0.04 alcrmon
    1  ?    1272 root  152   20   856K   960K run   0:70  0.04   0.04 oipmona
    1  ?    1272 root  150   20  1076K  249K run   0:00  0.04   0.04 mand
    ?  ?     0 root   128   20    OK    0K    sleep   0:12  0.02  0.02 wamper
    1  ?    136 root   168   20   448K   249K sleep   0:00  0.02  0.02 inits
    2  ?    128 root   128   20    OK   12K sleep   0:00  0.02  0.02 wanda
    ?  ?     4 root   128   20    OK    32K sleep   0:00  0.02  0.02 unhashd/aemo
    1  ?    147 root   147   20    OK    32K sleep   0:00  0.02  0.02 lvndcd
    ?  ?    22 root   147   20    OK    32K sleep   0:00  0.02  0.02 lvmhd
    ?  ?    24 root   147   20    OK   12K sleep   0:00  0.02  0.02 lvmfsd
    ?  ?    319 root   154   20   352K   248K sleep   0:00  0.02  0.02 ntpcser
    ?  ?    342 root   168   20    76K   192K sleep   0:00  0.02  0.02 xypwd
    ?  ?    345 root   168   20   156K   316K sleep   0:00  0.02  0.02 zparad
    ?  ?    418 root   154   20    80K   224K sleep   0:00  0.02  0.02 avyilqsd
    ?  ?    446 root   127   20   156K   424K sleep   0:00  0.02  0.02 netfmt
    ?  ?    552 root   154   20   740K   819K sleep   0:00  0.02  0.02 zpc_statd
    ?  ?    558 root   154   20   1004K  4079K sleep   0:00  0.02  0.02 rpc.lockd
    ?  ?    584 root   154   20    80K   819K sleep   0:00  0.02  0.02 inited
    ?  ?    861 root   154   20   1064K  432K sleep   0:00  0.02  0.02 semshall:2
    ?  ?    865 root   154   20   772K   712K sleep   0:00  0.02  0.02 dumdmp
    ?  ?    896 root   154   20   620K   652K sleep   0:00  0.02  0.02 mhbsagt
    ?  ?    918 root   154   20   3132K  6448K sleep   0:00  0.02  0.02 zmagnt
    ?  ?    951 root   154   20   4044K  1440K sleep   0:00  0.02  0.02 kpid
    1 pty/ttypl 952 root   158  24   312K   180K sleep   0:00  0.02  0.02 th
    1  ?    974 root   154   20   153K   949K sleep   0:00  0.02  0.02 crtdaemon
    0  ?    996 root   154   20   200K   316K sleep   0:00  0.02  0.02 pgrnd
    ?  ?   1039 root    74   10   380K   428K sleep   0:00  0.02  0.02 dgaesd
    ?  ?   1093 root   154   20  1224K   916K sleep   0:00  0.02  0.02 cid
    1  ?   1139 root   154   20   2588K  1624K sleep   0:00  0.02  0.02 perfld
    0  ?   1156 root   154   20   2552K  1572K sleep   0:00  0.02  0.02 aergentd
    0  ?   1167 root   154   20   224K   292K sleep   0:00  0.02  0.02 emassent
    0  ?   1168 root   127   20  2380K  2204K sleep   0:00  0.02  0.02 ccopuse
```

此输出显示在 *cable1* 中有两个标记为 *0* 和 *1* 的 CPU。输出中显示的系统名称为 *cvhdc0n3*，因为 *cable1* 的主机名是 *cvhdc0n3*。




虽然这是一个展示如何修改虚拟分区（Virtual Partition）的简单示例，但它也展示了 vPars 的强劲能力。当系统上的两个 vPar 都在运行时，可以在不中断 vPar 中正在运行的程序的情况下，向其中一个或两个 vPar 添加处理器。

请注意，**vparmodify** 的 `-a` 选项会根据当前 CPU 数量*相对地*更改 CPU 数量。在我们的案例中，当前的 CPU 数量为 1，使用 `-a cpu:1` 会在当前数量 1 的基础上增加 1 个 CPU，结果变成 2 个 CPU。使用 **vparmodify** 的 `-d` 选项移除处理器时，也是如此。以下示例展示了运行 **vparstatus** 以查看这两个 CPU，使用 **vparmodify** 将 CPU 数量改回 1（这也是相对于当前 CPU 数量而言的，当前数量为 2），以及运行 **vparstatus** 以确认该更改已生效：

```
# vparstatus -p cabiel -v

[Virtual Partition Details]
Name:                  cabiel
State:                 Up
Attributes:            Dynamic,Manual
Kernel Path:           /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max:               1/3
Bound by User [Path]:  33      <-- bound CPU @ 33
Bound by Monitor [Path]:
Unbound [Path]:        97      <-- unbound CPU @ 97

[IO Details]
  0-0
  0.0.0.0
  0.0.1.1.2.0 BOOT
  0.0.4.0  CONSOLE

[Memory Details]
Specified [Base /Range]:
             (bytes) (MB)
Total Memory (MB):  1024

# vparmodify -p cabiel -d cpu:1

# vparstatus -p cabiel -v

[Virtual Partition Details]
Name:                  cabiel
State:                 Up
Attributes:            Dynamic,Manual
Kernel Path:           /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max:               1/3
Bound by User [Path] : 33 <-- original CPU @ 33
Bound by Monitor [Path] :
Unbound [Path] : <-- no unbound CPUs

[IO Details]
0.0
0.0.0.1.2.0 BOOT
0.0.4.0 CONSOLE

[Memory Details]
Specified [Base /Range] :
(bytes) (MB) :
Total Memory (MB) : 1024
#
```

我们可以利用可用的两个未绑定 CPU 对 vPars 进行许多其他修改，例如向其中一个 vPar 添加两个 CPU，或者向每个 vPar 各添加一个 CPU。

在使用 vparmodify 时，请记住组件的相对性质，并且截至本文撰写时，某些更改，如修改内存或添加 I/O 组件，需要 vPar 处于停机状态。第 5 章对此有详细说明。

![](img/eff8b9287a5f38c5adf538f24aacf29e_141_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_141_1.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_142_0.png)

## 虚拟分区转储文件

当虚拟分区崩溃时，会在 /stand/vpmon.dump 中创建一个转储文件。当虚拟分区启动时，文件会在 /var/adm/crash/vpar 中创建。这些文件带有数字扩展名，指示发生转储的次数。例如，vpmon.1、vpmon.dump.1 和 summary.1 指示保存在 /var/adm/crash/vpar 中的第一组文件。

以下清单展示了与转储相关的、您可能会在 /stand 和 /var/adm/crash/vpar 中看到的示例：

```
VPARNAME = extrans1

# ll /stand
total 100400
-rw-r-- 1 root sys 19 Jul 13 25:04 bootconf
drwxr-xr-x 4 root sys 2048 Oct 18 13:43 build
drwxrwxrwx 5 root sys 1024 Oct 18 13:06 dkkm
drwxrwxrwx 5 root root 1024 Oct 18 13:21 dkkm.vmunix.prev
-rw-r-r- 1 root sys 3388 Oct 18 13:16 iootlddfig
-r-r-r-r- 1 root sys 82 Jul 13 15:34 kernel
drwxr-xr-x 2 root sys 1024 Oct 18 13:18 krs
drwxr-xr-x    2 root     root       1024 Oct 18 13:16 krs.1kg
drwxr-xr-x    2 root     root       1024 Oct 18 13:18 krs.tmp
drwxr-xr-x    2 root     root       8192 Jul 13 13:04 test-founds
-rw-------    1 root     root        12 Oct 18 13:16 rootconf
-r--r--r--.   1 root     sys       2035 Oct 18 11:42 systemd
-r-x-r--r--.   1 root     sys        994 Jul 13 15:28 systemd.01
-r--r-x-x-x    1 root     sys       999 Jul 13 15:56 systemd.02
-r-x-r--r--.   1 root     sys       2354 Oct 18 13:28 systemd.base
-r-x-x-x-x-x   2 root     sys       1024 Jul 13 15:37 systemd.02
-r-x-x--x-x    1 root     sys        2035 Oct 18 10:58 systemd
-r-xwr-xr-x    1 root     root      226825568 Oct 18 13:16 vpars.prev
-rwxr-xr-x    1 root     root      226825568 Oct 18 11:04 vmunix
-rw-------    1 root     sys        8232 Oct 18 13:16 vpdx
-rw--------    1 root     root        8232 Jul 17 14:11 vPod.OLD
-T-x-------    1 bin     bin      5078504 Aug 31 18:59 vpson <--- vPar dump
--wx-------    1 root     root      5078504 Oct 10 10:43 vppon

# 11 /var/adm/crash/vpar                    <--- vPar dump directory
total 44644
-rw-r--r--.   1 root     root          2 Oct 10 10:43 count
-rw-f--r--.   1 root     root       16794 Jul 17 13:26 summary.0
-rw-f--r--.   1 root     root       15993 Jul 18 10:15 summary.1
-rw-f--r--.   1 root     root       19318 Jul 18 11:36 summary.2
-rw-f--r--.   1 root     root       10012 Oct 10 10:43 summary.3
-r-x-r-x-x-x    1 root     root      855928 Jul 17 13:26 vpars
-r-x-r-x-x-x    1 root     root      855928 Jul 18 10:15 vpars
-r-x-r-x-x-x    1 root     root      855928 Jul 18 11:36 vpars
-r-x-r-x-x-x    1 root     root       837614 Oct 10 10:43 vpar
-rw-------    1 root     root      5078504 Jul 17 13:26 vpar.tmp
-rw-------    1 root     root      5078504 Jul 18 10:15 vpar.tmp
-rw-------    1 root     root      5078504 Jul 18 11:36 vpar.tmp
-iw-------    1 root     root      5078504 Oct 10 10:43 vpar.tmp
```

**/var/adm/crash/vpar** 目录中包含四次 *(0-3)* 崩溃的 vPar 转储相关文件。

在 **stand** 中创建的转储文件被保存在 **/var/adm/crash/vpar** 中，并带有崩溃编号作为扩展名。每次崩溃时，**stand** 中的转储文件会被覆盖，但您在 **/var/adm/crash/vpar** 中拥有包含所有转储文件和相关信息的完整历史。请保留 **/stand/vpmon.dump** 文件不要移除。

![](img/eff8b9287a5f38c5adf538f24aacf29e_143_0.png)

## 摘要

在表 2-1 中总结的 **vparreset** 和 **vparremove** 命令在此示例中根本未被执行。**vparremove** 命令可以在任何处于*关机状态*的 vPar 上运行。启动并运行 vPars 以及执行某些修改的一般步骤已为您展示，旨在为您提供一个简单的操作框架。还有其他一些未涵盖的命令，附录 A 中也提供了它们的手册页。

![](img/eff8b9287a5f38c5adf538f24aacf29e_143_1.png)

关于特定领域的更多细节出现在本书的其他章节中，我建议您查阅附录 A 中所有 vPar 的在线手册页。

还有一些与服务器技术相关的考虑事项，我们没有涵盖。如果您在服务器上使用了 Instant Capacity on Demand (iCOD)，为了让 vPars 正常工作，必须激活所有 CPU。在 vPar 中使用处理器集（psets）时，请使用已绑定的 CPU。

# 第 3 章

# 启动与 vPars

# vpmon, vparload, vparboot, PDC, ISL, hpux, 安全 Web 控制台, GSP 配置

## 背景

我们在之前的章节中已经在系统上做了大量工作，以加载和配置 HP-UX 11i 和虚拟分区（vPars）。现在让我们退后一步，考察 HP 9000 启动的细节。在系统上加载 vPars 后，启动过程中有一些变化。让我们先讨论带有 vPars 的启动，然后在本章稍后部分考察一般性启动。首先，我们将讨论在系统上安装 vPars 之后的启动，以查看 vPars 对启动过程的影响。然后，在本章中非 vPars 特定的部分，您将得到以下内容的概述：HP 9000 的低级启动和配置；设置 HP 安全 Web 控制台；以及配置 Guardian 服务处理器（GSP）。

本章示例中使用的绝大多数系统，无论是 vPars 特定部分还是非 vPars 特定部分，都是 L 类系统。我特意使用了一个简单的系统，以便我们可以专注于启动过程，同时最大限度地减少与硬件相关的消息。由于启动过程因系统而异，即使在

对于 HP 9000 系列，这并不是一项全面的研究，而只是一个概述。

## 虚拟分区启动过程概述

启动分区与不分区启动类似。主要区别在于*虚拟分区监控器*——在本章中我将称之为 **vpmon**。**vpmon** 在启动时加载，位于 */stand/vpmon*。

**vpmon** 位于 HP 9000 系统上的固件和操作系统之间。图 3-1 展示了 **vpmon** 相对于其他 HP 9000 组件的位置。

![](img/eff8b9287a5f38c5adf538f24aacf29e_148_0.png)

图 3-1 虚拟分区软件堆栈

请注意图中显示，vPars 中可能运行着不同版本和补丁级别的 HP-UX 11i。在 Itanium 处理器系列 (IPF) 系统上，vPars 中可能运行 HP-UX 以外的操作系统。由于本书撰写时此功能尚不可用，因此本书仅涵盖基于 HP-UX 11i 的 vPars。

在创建 vPars 的过程中，会生成一个分区数据库，用于跟踪与 vPars 关联的资源。**vpmon** 管理这些资源，加载内核，并执行其他功能，使其看起来好像每个虚拟分区都是独立的系统。

你不会直接从 ISL 引导内核（关于引导的所有方面（包括 ISL）的详细信息，请参见本章中非 vPars 相关的部分），而是引导 **vpmon**。**vpmon** 随后加载分区数据库 /stand/vpdb，并根据数据库中分配给 vPars 的资源创建 vPars。**vpdb** 是包含分区相关信息的默认数据库。每个分区都在磁盘上保留 **vpdb** 的副本，并自动保持同步。当对任何分区进行修改时，主 **vpdb** 会被更新，然后其他 vPars 上的本地副本会自动更新。这种同步每隔几秒发生一次，确保所有正在运行的分区上的 **vpdb** 保持同步。如果某个分区未运行，其 **vpdb** 无法更新。

如果没有 vPars，你会像下面这样从 ISL 直接引导 HP-UX 内核：

![](img/eff8b9287a5f38c5adf538f24aacf29e_149_0.png)

```
ISL> hpxp /stand/vmunix
```

你可以使用以下命令从 ISL 引导 **vpmon**：

```
ISL> hpxp /stand/vpmon
```

通过此命令调用 **vpmon** 后，会出现 **vpmon** 提示符，你可以从中加载 vPars。

从 **vpmon** 提示符，我们可以发出 **vparload** 命令来加载一个或多个虚拟分区。**vparload** 命令有许多选项。附录 A 中没有 **vparload** 的手册页，因为它是一个 **vpmon** 命令。**vparboot** 是一个 shell 命令，所以附录 A 中有它的手册页。以下是撰写本书时 **vparboot** 的三种形式：

- 形式 1：`vparload -all`
- 形式 2：`vparload -auto`
- 形式 3：`vparload -p vp_name [-b kernelpath] [-o boot_options] [-B hardware_path]`

形式 1 引导所有 vPars。形式 2 引导所有设置了自动引导属性的 vPars。形式 3 允许你指定选项，例如：要引导的 kernelpath；boot_options，例如“is”表示单用户模式；或者 hardware_path，指定用于该 vPar 的引导设备。

在 ISL> 提示符处发出 /stand/vpmon 命令会给我们 MON> 提示符。要使用 vparload 引导服务器上的所有虚拟分区，我们需要发出以下命令：

```
MON> vparload -all
```

要使用 vparload 引导虚拟分区 symbol1，我们需要发出以下命令：

```
MON> vparload -p symbol1
```

你可以在 ISL 提示符处使用以下命令执行加载 vpmon 和虚拟分区 symbol1 的步骤：

```
ISL> hpxp /stand/vpmon vparload -p symbol1
```

此命令引导 vpmon，然后引导 symbol1。你可能会对你的系统中的 vPar 内核进行实验，并可能需要引导不同的内核。以下示例展示了从一个名为 vmunix_test1 的内核引导：

```
MON> vparload -p symbol1 -b /stand/vmunix_test1
```

顺带一提，上述内核路径通过此 **vparload** 加载，但未进行永久性更改。要对 vPar 数据库进行永久性更改，你会发出以下命令：

```
# vparmodify -p symbol1 -b "stand/vmunix_test1"
```

vPar 数据库已修改，默认内核为 */stand/vmunix_test1*。

你可以使用以下命令以单用户模式引导 vPar：

```
MON> vparload -p symbol1 -o "is"
```

你可以使用多种其他选项来引导 vPars。正如从这个讨论中可以看到，这些选项与你在非 vPar 系统上使用的选项类似。

你可以从 *MON>* 发出多种其他命令。以下展示了一些更常见的命令：

| 命令 | 描述 |
| :--- | :--- |
| **help** | 显示 *MON>* 中可用的所有命令，如下所示（? 产生相同结果） |
| `?` | 打印命令列表 |
| `cat` | 将文件内容转储到屏幕 |
| `cbuf` | 转储控制台缓冲区内容 |
| `getauto` | 打印 AUTO 文件 |
| `help` | 打印命令列表 |
| `lifs` | 列出 LIF 目录中的文件 |
| `log` | 查看事件日志 |
| `ls` | 列出目录中的文件 |
| `readbDb` | 读取分区 DB |
| `reboot` | 重启系统 |
| `scan` | 扫描系统 |
| `todrifpreset` | 重置所有 vPars 的 TOD 漂移 |
| `vparload` | 加载 vPar |
| `vparinfo` | 显示 vPar 信息 |

### scan

显示虚拟分区监控器发现的所有硬件，并指示哪个 vPar（如果有）拥有该设备。请注意以下列表中，某些组件，如位于 0 和 1 的系统总线适配器 (SBA) 以及位于 192 的内存控制器，由虚拟分区监控器拥有，因此由 vPAR-ALL 拥有。其他组件由 vPar unhj1vp1/2 拥有。这是所有组件及其所属 vPar 的信息列表，如下所示：

```
MON> scan
    0
    0/0     BUDSCONV    sv_model= 12 HPA-0xFFFFFFFFFFDODO00 VPAR-ALL
    0/1     BUS_BRIDGE  sv_model=  10 HPA-0x00000FFBFF00P1 VPAR-unhjlvpl
    0/2     BUS_BRIDGE  sv_model=  10 HPA-0xFFFFFFFFFFFF0000 VPAR-NONE
    0/3     BUS_BRIDGE  sv_model=  10 HPA-0xFFFFFFFFFFFF0000 VPAR-NONE
    0/4     BUS_BRIDGE  sv_model=  10 HPA-0xFFFFFFFFFFFF0000 VPAR-NONE
    0/5     BUS_BRIDGE  sv_model=  10 HPA-0xFFFFFFFFFFFF0000 VPAR-NONE
    0/6     BUS_BRIDGE  sv_model=  10 HPA-0xFFFFFFFFFFFF0000 VPAR-unhjlvpo
    0/10    BUS_BRIDGE  sv_model=  10 HPA-0xFFFFFFFFFFFF0000 VPAR-NONE
    0/12    BUDSCONV    sv_model=  12 HPA-0xFFFFFFFFFFFF0000 VPAR-ALL
    1/0     BUS_BRIDGE  sv_model=  10 HPA-0xFFFFFFFFFFFF0000 VPAR-NONE
    1/2     BUS_BRIDGE  sv_model=  10 HPA-0xFFFFFFFFFFFF0000 VPAR-NONE
    1/4     BUS_BRIDGE  sv_model=  10 HPA-0xFFFFFFFFFFFF0000 VPAR-NONE
    1/8     BUS_BRIDGE  sv_model=  10 HPA-0xFFFFFFFFFFFF0000 VPAR-NONE
    1/12    BUS_BRIDGE  sv_model=  10 HPA-0xFFFFFFFFFFFF00P0 VPAR-unhjlvpo
    36*     BUDSCONV    sv_model=  12 HPA-0xFFFFFFFFFFFF0000 VPAR-NONE
    37      NPROX       sv_model=   4 HPA-0xFFFFFFFFFFFF0D50 VPAR-unhjlvpl
    44      BUDSCONV    sv_model=  12 HPA-0xFFFFFFFFFFFF0000 VPAR-NONE
    45      NPROX       sv_model=   4 HPA-0xFFFFFFFFFFFF00P0 VPAR-unhjlvpo
    192     MEMORY      sv_model=   9 HPA-0xFFFFFFFFFFFF0000 VPAR-ALL
    MON> vparinfo unhjlvpl
    Resources assigned to partition 0 (unjlvpl)...

    0     0xFFFFFFFFFFFF0000 1     0 TYPE 7 SV_MODEL= 12
    0/0   0xFFFFFBBFFBFF0000 1     0 TYPE 13 SV_MODEL= 10
    0/2   0xFFFFFFFFFFFF0000 1     0 TYPE-13 SV_MODEL= 10
    1     0xfffffffffed40000    1    0    TYPE= 7   SV_MODEL= 12
    37    0xfffffffffed25000    1    0    TYPE= 0   SV_MODEL= 4
    192   0xfffffffffedc0000    1    0    TYPE= 1   SV_MODEL= 9

Effective Size: 1572064 kB
Boot:    0/0/2/0.6.0
Console: 0/0/U/C
Boot Image: (2/0/2/0.6.0)/stand/vmunix
Boot Options:
AUTOSORT:off
DYNAMIC
```

### vparinfo [partition_name]

显示分配给指定 vPar 的资源，或者如果未指定 vPar 名称，则显示未分配的资源。以下列表显示了分配给 vPar whnjlyp2 的资源：

```
MON> vparinfo whnjlyp2

Resources assigned to partition 1 (whnjlyp2):
0     0xfffffffffed00000    1    0    TYPE= 7   SV_MODEL= 12
0/0   0xfffffffffbff0000    1    0    TYPE=13   SV_MODEL= 10
1     0xfffffffffed04000    1    0    TYPE= 7   SV_MODEL= 12
1/12  0xfffffffffee40000    1    0    TYPE=13   SV_MODEL= 10
45    0xfffffffffed2d000    1    0    TYPE= 0   SV_MODEL= 4
192   0xfffffffffedc0000    1    0    TYPE= 1   SV_MODEL= 9

Effective Size:  524288 kB
S^*: 1, 1, 1, 1, 1, 12,
Console:  Default
Boot Image: (1.12/0/0.12.0)/stand/vmunix
Boot Options:
AUTOSORT: off
DYNAMIC
```

### vparload

此命令的三种形式列在下面。这三种形式之后的示例展示了使用 vparload -all 加载所有 vPars 的开始：

- 形式 1：`vparload -all`
- 形式 2：`vparload -auto`
- 形式 3：`vparload -p vp_name [-b kernelpath] [-o boot_options] [-B hardware_path]`





**vparload -all**

```text
MON> vparload -all
[MON] Booting uhnjlvp2...
[MON] Booting uhnjlvp1...
[MON] Console client set to uhnjlvp2

[MON] uhnjlvp2 loaded

[MON] uhnjlvp1 loaded
```

**lilfs**

显示 LIF 区域中的文件，如下所示：

```text
MON> lilfs
volume ISLI0 data size 7802 directory size 8
filename type start size implement created
================================================================================
ODB -12960 584 848
MAPFILE -12277 1432 128
SYSLIB -12280 1560 353
CONFIGDATA -12278 1920 218
SLMOD2 -12276 2144 140
SLDEV2 -12276 2288 134
SLDRV2 -12276 2424 168
SLSCSI2 -12276 2592 116
MAPPER2 -12279 2712 142
IOTEST2 -12279 2856 89
PERFVER2 -12279 2952 125
PVCD -12801 3080 64
SSINFO -12286 3144 2
ISL -12800 3152 306
AUTO -12289 3464 1
HPUX -12928 3472 848
LABEL -23951 4320 8
```

**getauto**

显示 LIF 区域中 auto 文件的内容，如下所示：

```text
MON> getauto
hpux
```

**log**

显示虚拟分区监视器日志中的所有信息。信息按时间顺序显示，如下所示：

```text
MON> log
INFO:CPU0:MON:[20:16:31 10/1/2001 GMT] VPAR Monitor version 0.2 started
INFO:CPU0:MON:Version string: @(#) $Revision: vpmong:
  vw: -- selectors: CUP
  11.11_BL2001_0616            'cup_cvinod_vpar_ncf_trial'
  'cup_Shepf_r11.11'   Tue Sep 25 18:2
  L12 PGT 2001: $INFO:CPU0:MON:Partition uhnj1vp1 monarch set to 37
INFO:CPU0:MON:Partition uhnj1vp2 monarch set to 45
```

## ls directory

类似于 UNIX 的 **ls** 命令，列出一个目录的内容。在撰写本文时，*目录* 必须是 HFS 格式。默认使用 **/stand** 目录。你还可以添加 *-a* 以列出所有条目，*-l* 以显示长格式列表，*-n* 以显示数字条目，*-i* 以显示 inode，以及 *-F* 以在输出末尾添加文件类型，例如在目录后添加斜杠 (/)。以下使用 *-l* 选项的示例：

```text
MON> ls -l /stand
drwxr-xr-x   2 0       8192 lost+found
-rw-rw-rw-   1 0        5416 iconfig
drwxr-xr-x   4 0       2048 build
-rwxr-xr-x   1 0     15273152 vmunix
drwxrwxrwx   5 0        1024 .dkkm
vmunix.prev
-rw-r-r-r---  1 0         19 bootconf
-r-r-r-r-T--- 1 0          82 kernel
-rw----------  1 0         12 rootconf
-r-r-r-rT---  1 0       1040 system
-r-r-r-rT---  1 0       1035 system.prev
drwxr-xr-x   1 0     14488016 vmunix.prev
drwxrwxrwx   5 0        1024 .dkkm
drwxr-xr-x   2 0       1024 system.d
drwxr-xr-x   2 0       1024 krs
drwxr-xr-x   2 0       1024 krs.tmp
drwxr-xr-x   2 0       1024 krs_lkg
-R-XR-XR-X   1  2      2      845680 vpmcon
-rw-------    1  0      0     102640 vpmcon.dmp
-rw-------     2  0      0      8232 vpdb
```

**cbuf** *partition_name*

显示指定虚拟分区的控制台缓冲区中的信息。如果缓冲区中没有信息，你将收到以下消息：

```text
MON> cbuf uhnjlvp1
   Buffer is empty
```

`MON>` 提示符下的许多命令都具有信息展示功能。现在我们继续了解 vPars 的状态。

### 虚拟分区启动状态

在第二章中创建和修改 vPars 时，我们已经看到了许多处于不同启动状态的 vPars 示例。当我们启动虚拟分区时，它会经历 *load*（加载）阶段，然后是 *boot*（启动）阶段，最后进入 *up*（运行）状态。虚拟分区还可能处于其他状态。表 3-1 总结了在撰写本文时虚拟分区的状态：

### 表 3-1 虚拟分区状态

| vPars 状态 | 描述 |
| :--- | :--- |
| load | 虚拟分区的内核映像正在被虚拟分区监视器加载到内存中。 |
| boot | 虚拟分区正在启动过程中。内核映像已成功由虚拟分区监视器加载。 |
| up | 虚拟分区已成功启动并正在运行。 |
| shut | 虚拟分区正在关闭过程中。 |
| down | 虚拟分区未运行，已停止。 |
| crash | 虚拟分区经历了恐慌（panic）并正在崩溃。 |
| hung | 虚拟分区无响应并挂起。 |

在第二章创建虚拟分区并通过连续发出 **vparstatus** 命令观察其启动时，我们已经看到过其中的几种状态。以下示例显示了虚拟分区 *cable2* 的启动过程：

```text
# vparboot -p cable2
# vparstatus
[Virtual Partition]
Virtual Partition Name  State Attributes Kernel Path Boot Opts
------------------------------------------
cable1 Up Dyn.Manl /stand/vmunix
cable2 Load Dyn.Manl /stand/vmunix

[Virtual Partition Resource Summary]
Virtual Partition Name CPU Num Memory (MB)
                        Min/Max Bound/ IC # Ranges/ Total MB
                        Unbound devs /stand/vmunix
cable1 2/4 2 0 4 0/0 2048
cable2 2/2 2 0 4 0/0 1024
# vparstatus
[Virtual Partition]
Virtual Partition Name State Attributes Kernel Path Boot Opts
------------------------------------------
cable1 Up Dyn.Manl /stand/vmunix
cable2 Boot Dyn.Manl /stand/vmunix

[Virtual Partition Resource Summary]
Virtual Partition Name CPU Num Memory (MB)
                        Min/Max Bound/ IC # Ranges/ Total MB
                        Unbound devs /stand/vmunix
cable1 2/4 2 0 4 0/0 2048
cable2 2/2 2 0 4 0/0 1024
# vparstatus
[Virtual Partition]
Virtual Partition Name State Attributes Kernel Path Boot Opts
------------------------------------------
cable1 Up Dyn_Manl /stand/vmunix
cable2 Up Dyn_Manl /stand/vmunix

[Virtual Partition Resource Summary]
Virtual Partition Name CPU Num Memory (MB)
                        Min/Max Bound/ IC # Ranges/ Total MB
                        Unbound devs /stand/vmunix
cable1 2/4 2 0 4 0/0 2048
cable2 2/2 2 0 4 0/0 1024
```

此示例显示 *cable2* 依次进入 *load*，然后 *boot*，最后 *up* 状态。*cable2* 是从运行在同一硬件上的 *cable1* 启动的。当 *cable1* 启动时，系统已经完成了启动过程。由于大部分硬件已在运行，*cable2* 的启动速度非常快。第一个虚拟分区的启动时间与非虚拟分区系统的启动时间相当，但随后的 vPars 启动要快得多。

### setboot 命令和 vPars

在第二章我们的 vPars 示例中，我们将虚拟分区的 autoboot（自动启动）设置为关闭。在非 vPars 系统上，setboot 命令从稳定存储读取并写入数据。在 vPars 系统上，setboot 命令与虚拟分区数据库交互。在 vPars 系统上运行 setboot 的效果如表 3-2 所示：

### 表 3-2 setboot 和虚拟分区

| vPars setboot 选项 | 描述 |
| :--- | :--- |
| -a | 更改虚拟分区的备用启动路径。设置备用启动路径：# setboot -a 0/8/0/0.8,0.5,0.0.0 |
| -b | 设置虚拟分区的 autoBoot（自动启动）属性。设置 AutoBoot 开启：# setboot -b on |
| -p | 更改虚拟分区的主启动路径。设置主启动路径：# setboot -p 0/0/1/1.2.0 |
| -s | 无效果。 |
| 无选项 | 显示有关启动属性的信息。 |

![img/eff8b9287a5f38c5adf538f24aacf29e_159_0.png](img/eff8b9287a5f38c5adf538f24aacf29e_159_0.png)

**setboot** 命令是与 vPars 交互时与非 vPars 系统的一个不同之处。

你还可以通过 **vpar-modify** 设置主启动路径和备用启动路径。

### 其他启动主题

虚拟分区和 HP-UX 的启动在第 8 章 *启动* 中有详细介绍，由于启动与启动密切相关，建议你阅读第 8 章。要了解 LAN 卡如何与 vPars 配置（即 *lam0* 和 *lam1*），请参见第 13 章。本章其余部分提供了关于启动的广泛背景信息。

## 非 vPars 特定章节部分：启动过程概览

HP 9000 系统上的启动过程在其最简形式下可归结为三个步骤。我将简要描述这三个步骤，然后我们将查看一些启动过程示例，以观察这三个步骤的实际运作。以下是这三个步骤的描述：

**PDC**

HP 9000 系统预装有称为处理器依赖代码（Processor Dependent Code，PDC - 参考手册页 pdc）的固件。系统开机或处理器复位后，PDC 运行自检操作并初始化处理器。PDC 还会识别控制台路径，以便提供消息并接受输入。除非你在提供的 10 秒时间间隔内中断它，否则 PDC 将开始“autoboot”（自动启动）过程。如果你中断“autoboot”过程，你可以发出各种命令。与 PDC 命令交互的界面称为启动控制台处理程序（Boot Console Handler，BCH）。这有时会造成混淆；即，我们是在发出 PDC 命令还是 BCH 命令？这些命令通常被描述为 PDC 命令，而执行它们的界面是 BCH。

**ISL**

初始系统加载器（Initial System Loader，ISL - 参考手册页 isl）在 PDC 之后运行。通常你会从 ISL 运行“autoboot”（自动启动）序列；但是，你可以从 ISL 提示符下运行许多命令。




### 引导控制台处理器（BCH）与处理器相关代码（PDC）

`hpx` 实用程序负责加载 HP-UX 内核并将控制权交给内核。ISL（初始系统加载程序）可以运行 `hpx` 的“自动执行”文件，也可以交互地输入命令。在大多数情况下，你只需要自动启动系统；不过，我们将查看一些可以执行的 `hpx` 命令。这有时也称为次级系统加载器（SSL）。

我发现对于新的系统管理员来说，关于引导过程存在许多困惑。首先，随新系统提供的关于 HP 9000 引导的文档并不多。其次，如果对引导过程没有任何背景知识，很难确定系统在给定时间处于引导的哪个阶段。表 3-3 显示了一些系统状态以及你在系统启动时按大致的顺序可能看到的每个状态对应的提示符：

### 表 3-3 /sbin/set_parms 参数

| 系统引导状态 | 提示符 |
| --- | --- |
| 引导控制台处理器（BCH） | 主菜单：输入命令或菜单 > |
| *在引导开始后 10 秒内中断引导时可见。用于执行与 PDC 相关的工作。* | |
| 初始系统加载器（ISL） | ISL> ? |
| *在与 PDC 相关的工作之后可见。* | |
| hpx | 取决于系统状态而有所不同。 |
| *提示符各不相同。你通常在 ISL 提示符处输入 hpx 命令来启动。这有时也称为次级系统加载器（SSL）。* | |
| 监护服务处理器（GSP） | GSP> |
| *在键入 \*b（控制 b）以访问 GSP 时可见* | |

描述引导过程只有一种方式，那就是通过示例。在即将介绍的章节中，我们将涵盖一个硬件配置最简系统的引导过程。我选择硬件配置最简系统的引导过程，是为了避免陷入硬件相关的细节，而是专注于引导过程本身。启动这个简单系统所显示的信息将使我们能够专注于引导过程，而不是众多硬件组件。对于任何 HP 9000 系统，引导过程通常由基本相同的步骤组成，因此你可以将这些信息应用于你的系统。然而，你可能拥有一个包含更多组件的大型系统，它会生成更冗长的引导信息。

### 引导控制台处理器（BCH）与处理器相关代码（PDC）

如前所述，HP 9000 系统预装了称为处理器相关代码（PDC）的固件。在系统通电或处理器复位后，PDC 会运行自检操作并初始化处理器。PDC 还会识别控制台路径，以便提供消息并接受输入。PDC 随后将开始“自动启动”过程，除非你在提供的 10 秒间隔内中断该过程。如果你中断“自动启动”过程，你可以发出各种命令。

下面的示例展示了一个 L 类系统的引导过程以及我们在系统上接收到的与 PDC 相关的消息。你看到的第一组消息是各种自检相关的消息。处理器、内存、I/O 及其他组件会经历一系列测试。我在示例中省略了部分消息列表，凡见到三个省略号之处，是因为完整的测试结果列表过长，无法收录在本书中：

```
Value of TERM has been set to \"vt100\"
WARNING: YOU ARE SUPERUSER [11.00] (see /etc/issue)
Console Login: root
# reboot -h...checking for disk quotas
Shutdown at 27:41 [in 6 minutes] Xcard Co., All Rights Reserved.
(c)Copyright 1979, 1980, 1983, 1985-1993 The Regents of The Univ. of California
(c)(c)** FINAL System shutdown message from root@sp.serviceengines.com **
(c)Copyright 1986-1992 Sun Microsystems, Inc.
System going down IMMEDIATELY Massachusetts Institute of Technology
(c)Copyright 1989-1993 The Open Software Foundation, Inc.
System shutdown time has arrived\n Corp.
(c)Copyright 1990 Motorola, Inc.
(c)Copyright 1990, 1991, 1992 Cornell University
System shutdown time has arrived\n Corp.
(c)Copyright 1989-1991 The University of Maryland
Console reset done\n arnspie Mellon University
(c)Copyright 1991-1997 Mentat, Inc.
Boot device reset done\n ng Star Technologies, Inc.
(c)Copyright 1996 Progressive Systems, Inc.
(c)Copyright 1997 Isogon Corporation

System has halted
OK to turn off power or reset\n\n\n RIGHT
LEGEND
UNLESS *WAIT for UPR to turn off power* message was printed above do not
restrings as set forth in sub-paragraph (c)(i)(1)\n of the Rights in
V VIRTUAL PROM PANEL****\n\n\n****ee in OPARS 252:227-701.\nSystem BOOT detected
Leds: RUN ATTENTION FAILT REMOTE POWER
 ON FLASH OFF U.S
ON A, CA 94104 U.S
platform  62EF
processor   1C1IYS are as set
processor   1I42
test    1100
processor   1100
processor   1100
test    1100
processor   1100
processor   1100
test    1100
processor   1100
processor   1100
processor   1100
PDR     322F
PDR     3149
PDR     3165
platform  616A
processor   1146
processor   INIT   1701
processor   INIT   1701
.
.
.
processor   111C
processor   111D
processor   111D
processor   1111
processor   2111
processor   2111
processor   2112
processor   2112
processor   2113
processor cache test 2113
processor cache test 2121
processor cache test 2121

memory test 7IA4
memory test 7IA5
memory test 7IA5
memory test 7IA6
memory test 7IA6
memory config 7210
:/0 INIT 8701
1/0 test 8118
1/0 test 8118
1/0 INIT 8701
2/0 INIT 8701
1/0 INIT 8701
1/0 INIT 8701
2/0 INIT 8701
2/0 INIT 8701
1/0 INIT 8701
1/0 INIT 8701
memory config 7240
memory INIT 7702
memory config 7241
memory config 7243
memory config 7240
memory test 7JA1
memory test 7IA2

processor test 1120
processor slave rendezvous 1C40
processor test 1142
processor test 1138
platform test 612A
1/0 config 8238

> ******* EARLY BOOT VPF ******
> End of early boot detected
> ******************************

Firmware Version 39.46

DuPlex Console IO Dependent Code (IODC) revision 1

> (c) Copyright 1995-1998, Hewlett-Packard Company. All rights reserved

Processor Speed State CoProcessor State Cache Size
Number

0 440 Mhz Active Functional 512 KB 1 MB
3 440 Mhz Idle Functional 512 KB 1 MB

+   - Central Bus Speed (in Mhz) : 82
+   - Available Memory : 2097152 KB
+   - Good Memory Required : 11468 KB

+   - Primary boot path: 0/0/1/1.2
+   - Alternate boot path: 0/0/2/0.2
+   - Console path: 0/0/4/0.0
+   - Keyboard path: 0/0/4/0.0

Processor is booting from first available device.

To discontinue, press any key within 10 seconds.
```

“早期”引导完成后，我们会得到一份简明的系统摘要，包括我们系统上的固件版本，然后我们有机会选择从主路径自动启动，或者按任意键停止引导过程。在正常的系统操作中，你会选择自动启动；不过，在我们的情况下，我们将中断引导过程，以查看 PDC 中有哪些可用命令。当我们中断引导过程时，会出现以下菜单：

```
Boot terminated.

Main Menu

Command Description
Boot [PRI|ALT] [<path>] Boot from specified path
PATH [PRI|ALT] [<path>] Display or modify a path
SEARCH [Display|PL] [<path>] Search for boot devices

Configuration menu Displays or changes configurations
Information menu Displays system information
Service menu Display service commands

Display Redisplay the current menu
HELP [<menu>|<command>] Display help for menu or command
RESET Restart the system

Main Menu: Enter command or menu >
```

PDC 的接口被称为引导控制台处理器（BCH）。在我们的讨论中，我们发出的命令是 PDC 命令，而用于发出这些命令的接口是 BCH。这个菜单中的许多命令对系统管理员非常有帮助，但有时它们被忽视，因为它们属于操作系统之前的阶段，通常容易被忽略。

我们暂时跳过前三个命令，先通过输入 co 来查看配置菜单（Configuration menu）。配置（Configuration）中的大写 "CO" 意味着你可以仅输入 co 作为 configuration 的缩写：




### 启动控制台处理程序（BCH）与处理器相关代码（PDC）

主菜单：输入命令或菜单 > co
- 配置菜单

| 命令 | 描述 |
| :--- | :--- |
| Auto [iBoot [SSARCH [Start] [ON/OFF] | 显示或设置指定标志 |
| BootID [>proc] [<bootid> | 显示或设置启动标识 |
| BootInfo | 显示启动相关信息 |
| BootTimer [0 - 200] | 允许启动尝试的秒数 |
| PDUconfig [proc] [ON/OFF] | 配置/取消配置处理器 |
| Default | 将系统设置为预定义值 |
| FanSpeed | 显示或更改风扇速度 |
| BootTests | 显示或设置启动测试执行 |
| Path | 显示或修改路径 |
| SEARCH | 搜索启动设备 |
| RTC | 以格林威治时间读取或设置实时时钟 |
| Boot | 从指定路径启动 |
| Display | 重新显示当前菜单 |
| Help | 显示指定命令的帮助 |
| RESET | 重启系统 |
| Main | 返回主菜单 |

配置菜单：输入命令 >

在*配置*菜单下有几个非常有用的命令。

例如，你可以启用*快速启动*，这可以控制启动时运行的测试。我们将发出**快速启动**命令来查看系统当前的设置，但不会更改*快速启动*的值：

配置菜单：输入命令 > FastBoot
Fastboot: OFF
配置菜单：输入命令 >

我们的系统*快速启动已关闭*，这意味着我们将在启动时运行所有可用的测试。如果你想减少系统启动时间并且愿意跳过启动测试，你可以开启*快速启动*。

在*配置*菜单下还有许多其他命令可以根据你的需求发出，例如使用*CPUconfig* 来配置和取消配置处理器。

现在让我们发出*Main* 命令回到*主*菜单，然后使用*IN* 访问*信息*菜单：

配置菜单：输入命令 > main

| 命令 | 描述 |
| :--- | :--- |
| Boot [PRI|ALT]<+path> | 从指定路径启动 |
| Path [PRI|ALT] <+path> | 显示或修改路径 |
| SEARCH [Display|PL] [-path] | 搜索启动设备 |
| Configuration menu | 显示或设置启动值 |
| Information menu | 显示硬件信息 |
| Service menu | 显示服务命令 |
| Display | 重新显示当前菜单 |
| Help <menu>\|<command> | 显示菜单或命令的帮助 |
| RESET | 重启系统 |

主菜单：输入命令或菜单 > IN

信息菜单

| 命令 | 描述 |
| :--- | :--- |
| ALL | 显示所有系统信息 |
| BootInfo | 显示启动相关信息 |
| Cache | 显示缓存信息 |
| ChipRevisions | 显示主要芯片的版本 |
| Processor | 显示处理器信息/状态 |
| FPU | 显示浮点运算单元信息 |
| Firmware | 显示固件版本 |
| I/O | 显示 I/O 接口信息 |
| LanAddress | 显示核心 LAN 站地址 |
| Memory | 显示内存信息 |
| Processor | 显示处理器信息 |
| Warnings | 显示系统警告消息 |

| 命令 | 描述 |
| :--- | :--- |
| Boot [PRI|ALT]<+path> | 从指定路径启动 |
| Display | 重新显示当前菜单 |
| Help <command> | 显示指定命令的帮助 |
| RESET | 重启系统 |
| MAIN | 返回主菜单 |

信息菜单：输入命令 >

*信息*菜单是系统管理员的一颗隐藏宝石。菜单选项中包含显示*全部*系统信息的选项，这会为我们的 L 类系统生成以下报告。我在报告的末尾省略了部分内容（见三个省略号处）：

信息菜单：输入命令 > all

Model: 9000/800/L2000-44

### 处理器信息

| 处理器 | 速度 | HVERSION | SVERSION | CVERSION | 处理器状态 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | 440 MHz | 0x504 | 0x0491 | 2.4 | 活动 |
| 3 | 440 MHz | 0x504 | 0x0491 | 2.4 | 空闲 |

中央总线速度 (MHz) : 82
软件 ID (十进制) : 143901527
软件 ID (十六进制) : 0x089C357
软件能力 : 0x01F0

### 协处理器信息

| 处理器 | 协处理器型号 | 协处理器版本 | 协处理器状态 |
| :--- | :--- | :--- | :--- |
| 0 | 0x0000010 | 1 | 功能正常 |
| 3 | 0x0000010 | 1 | 功能正常 |

### 缓存信息

| 处理器 | 指令缓存大小 | 数据缓存大小 |
| :--- | :--- | :--- |
| 0 | 512 KB | 1 MB |
| 3 | 512 KB | 1 MB |

### 内存信息

### 内存状态表 (MB) (当前启动状态)

- 插槽 0a 512M 活动
- 插槽 0b 512M 活动
- 插槽 1a 512M 活动
- 插槽 1b 512M 活动
- 插槽 2a -
- 插槽 2b -
- 插槽 3a -
- 插槽 3b -
- 插槽 4a -
- 插槽 4b -
- 插槽 5a -
- 插槽 5b -
- 插槽 6a -
- 插槽 6b -
- 插槽 7a -
- 插槽 7b -

小计 2048M
总计 = 2048 MB

### 内存安装指南

- 为了使 DIMM 正常工作，插槽对 (a/b) 中的两个 DIMM 必须是同一类型。(相同部件号 = 相同类型)
- 为了正确散热，请按以下顺序安装 DIMM：0a/b 1a/b 2a/b 3a/b 4a/b 5a/b 6a/b 7a/b。

活动、已安装内存 : 2048 MB SDRAM
未分配页面 : 0 页
可用内存 : 2048 MB
操作系统所需良好内存 : 12 MB

内存
HVERSION 0x0950
SVSERSION 0x00009900

### I/O 模块信息

| 类型 | 路径 (十进制) | 插槽编号 | NVERSION | SVERSION | IOCC 版本 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 系统总线适配器 | - | - | 0x5820 | 0xd10 | 0x0 |
| 本地总线适配器 | 0/0 | 1 | 0x7820 | 0xa00 | 0x0 |
| 本地总线适配器 | 0/1 | 6 | 0x7820 | 0xa00 | 0x0 |
| 本地总线适配器 | 0/2 | 8 | 0x7820 | 0xa00 | 0x0 |
| 本地总线适配器 | 0/3 | 10 | 0x7820 | 0xa00 | 0x0 |
| 本地总线适配器 | 0/4 | 12 | 0x7820 | 0xa00 | 0x0 |
| 本地总线适配器 | 0/5 | 7 | 0x7820 | 0xa00 | 0x0 |
| 本地总线适配器 | 0/6 | 9 | 0x7820 | 0xa00 | 0x0 |
| 本地总线适配器 | 0/7 | 11 | 0x7820 | 0xa00 | 0x0 |

### PCI 设备信息

| 描述 | 路径 (十进制) | 供应商 ID | 设备 ID | 总线 # | 插槽 # |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 以太网控制器 | 0/0/0/0 | 0x1011 | 0x19 | 0 | 1 |
| SCSI 总线控制器 | 0/0/1/0 | 0x1000 | 0xb | 0 | 1 |
| SCSI 总线控制器 | 0/0/1/1 | 0x1000 | 0xb | 0 | 1 |
| SCSI 总线控制器 | 0/0/2/0 | 0x1000 | 0xf | 0 | 1 |
| SCSI 总线控制器 | 0/0/2/1 | 0x1000 | 0xf | 0 | 1 |
| 计算机串口控制器 | 0/0/4/0 | 0x103c | 0x1048 | 0 | 2 |
| 计算机串口控制器 | 0/0/5/0 | 0x103c | 0x1048 | 0 | 2 |
| 以太网控制器 | 0/0/5/0 | 0x1011 | 0x19 | 24 | 10 |
| SCSI 总线控制器 | 0/4/0/0 | 0x1000 | 0xf | 32 | 12 |
| SCSI 总线控制器 | 0/4/0/1 | 0x1000 | 0xf | 32 | 12 |
| SCSI 总线控制器 | 0/7/0/0 | 0x1000 | 0xf | 56 | 11 |
| SCSI 总线控制器 | 0/7/0/1 | 0x1000 | 0xf | 56 | 11 |

### 启动信息

处理器  启动 ID
-- -- --
0    2
3    2

自动启动:      开
自动搜索:     开
自动启动:      开
快速启动:       关

主启动路径:  intacsilb.2
0/0/1/-
0/0/03/01.2  (十六进制)
备用启动路径: intacsil.2
0/0/2/0.2
0/0/02/0.2   (十六进制)
控制台路径:     0/0/4/0.0
0/0/04/0.0   (十六进制)
键盘路径:    0/0/4/0.0
0/0/04/0.0     (十六进制)

LAN 站地址:  001003-fc9288
2000年4月19日 星期三 22:02:46 GMT    (20:00:04.19:22:02:46)

### 固件信息

固件版本: 39.46

| 模块 | 修订版 |
| :--- | :--- |
| 系统板 | A43938 |
| PA 8500 CPU 模块 | 2.4 |
| PA 8500 CPU 模块 | 2.4 |

### FRU 信息

FRU 名称:           SYS_BD
部件号:        AS911-50001
序列号:      A5449582277
物理位置:  00ffE0001ffff669
工程日期代码: 3918
艺术工艺修订版: A4
扫描修订版:
FRU 特定信息: US4D110E

FRU 名称: IC BP
部件号: A5191-60002
序列号: 525CPK23WX
物理位置: 0001ff0002fff169
工程日期代码: 3962
艺术工艺修订版: A2
扫描修订版:
FRU 特定信息:

FRU 名称: LAN_SCB_CORE_IO
部件号: A5191-60011
序列号: 525CPK128DE
物理位置: 0000004fff0fff85
工程日期代码: 3933
艺术工艺修订版: A5
扫描修订版:
FRU 特定信息:

...
.
.
.

FRU 名称: DIMM 512
部件号: A5798-60001
序列号: A56902093896
物理位置: 0000ff0000fbfff74
工程日期代码: 3938
艺术工艺修订版: A4
扫描修订版:
FRU 特定信息:

信息菜单：输入命令 >

这份报告将是非常适合放入系统管理笔记本的内容。了解固件修订版本级别和启动标志设置等信息非常有价值。

在上面的示例中，我们使用 BCH 发出 PDC 命令 *Information* 然后 *ALL*。*Information* 和 *ALL* 都是通过 BCH 接口发出的 PDC 命令。有时在文档中 PDC 和 BCH 可以互换使用，但要知道 BCH 是发出 PDC 命令的接口，这通常会在你查找特定命令的信息时非常有帮助。

现在让我们回到*主*菜单，然后查看*服务*菜单：

服务菜单：输入命令 > Main

--- 主菜单 ----------------------
命令 描述
Boot [Pri|Alt|<path>] 从指定路径启动

![](img/eff8b9287a5f38c5adf538f24aacf29e_170_0.png)




## 138 第 3 章 vpmom, vparload, vparboot, PDC, ISL, hpxuc, 安全 Web 控制台，GSP 配置

```
PAtt [PRI|ALT] [-path]            显示或修改路径
S8Arch [Display|IPt] [-path]       搜索启动设备

配置菜单                 显示或设置启动值
信息菜单                 显示硬件信息
S8Vtice 菜单                     显示服务命令

显示                          重新显示当前菜单
HeEp [-command]                  显示菜单或命令的帮助
RESET                            重启系统

主菜单：输入命令或菜单 >  80t

    ... 服务菜单 ...
    ...
    命令                描述
    ...
    CLEARPIM               清除（置零）PIM 的内容
    SCSt [option] [-path] [-val]   SCSt 选项或设置 SCSt 控制器值
    MenRead <address> [len]     读取内存或 I/O 位置
    PUT [CLEAR]             显示或清除 PUT
    PIM [-proc] [HPMC|PMC|TOC]  显示 PIM 信息
    ProductNum <O|- <number>   显示或设置产品编号
    SelfTest [ON|OFF]       启用/禁用自检执行
    ...
    BOOT [PRI|ALT| -path]      从指定路径启动
    显示                     重新显示当前菜单
    HELP [-command]             显示指定命令的帮助
    RESET                       重启系统
    Main                        返回主菜单

服务菜单：输入命令 >
```

在 *SERVICE* 菜单中的选项包括操作处理器内部内存（PIM）、显示 SCSt 控制器值以及启用和禁用自检。在下面的示例中，我们运行 *SCSt* 以获取有关 SCSt 接口的信息，然后返回到 *Main* 菜单：

```
服务菜单：输入命令 >  BCSt

路径 (dec)  发起方 ID  SCSI 速率  自动终端

0/0/1/0      7              Fast       Unknown
0/0/1/1      7              Ultra      Unknown
0/0/2/0      7              Ultra      Unknown
0/0/2/1      7              Ultra      Unknown

服务菜单：输入命令 >  main

    ... 主菜单 ...
    ...
    命令                描述
    ...
    BOOT [PRI|ALT| -path]      从指定路径启动
    显示                     显示或修改路径
    S8Arch [Display|IPt] [-path]   搜索启动设备
```

配置菜单	显示或设置启动值
信息菜单	显示硬件信息
SERVICE 菜单	显示服务命令

显示	重新显示当前菜单
HELP (<menu>\<command>)	显示菜单或命令的帮助
RESET	重启系统

主菜单：输入命令或菜单 >

既然我们已经查看了一些 PDC 命令，让我们回到启动过程，查看主菜单下的前三个命令。

BOOT 允许你指定启动系统的路径。PATH 允许你显示或修改启动路径。SEARCH 将显示启动路径。在下面的示例中，我们将使用 SEARCH 显示 L-Class 系统上的所有潜在启动设备，运行 PATH 显示现有的启动路径，然后指定我们希望从中启动系统的设备：

```
服务菜单：输入命令 > main

主菜单：
命令 描述
Boot [PRI|ALT] <path> 从指定路径启动
Path [PRI|ALT] [path] 显示或修改路径
SEARCH [Display|FU] <path> 搜索启动设备

配置菜单 显示或设置启动值
信息菜单 显示硬件信息
SERVICE 菜单 显示服务命令
显示 重新显示当前菜单
HELP [<menu>|<command>] 显示菜单或命令的帮助
RESET 重启系统

主菜单：输入命令或菜单 > sea
主菜单：输入命令或菜单 > sea
正在搜索潜在的启动设备
这可能需要几分钟。

要中止搜索，请按任意键（终止可能不是立即发生的）。

路径# 设备路径 (dec) 设备路径 (名称) 设备类型
F0 0/0/1/1.2 IntscsiB.2 随机存取介质
F1 0/0/2/0.2 IntscsiA.2 随机存取介质

主菜单：输入命令或菜单 > pa
主启动路径：IntscsiB.2
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_172_0.png)

0/0/1/1.2
0/0/01.2    (十六进制)

备用启动路径：    intascia.2
0/0/2/0.2
0/0/2.2    (十六进制)

控制台路径：    0/0/4/0.0
0/0/4/0.6    (十六进制)

键盘路径：    0/0/4/0.0
0/0/4.0    (十六进制)

主菜单：输入命令或菜单 -> **bo p0**
与 IPL 交互 (Y, N, 或 Cancel)? **y**

*SEARCH* 命令显示两个潜在的启动设备；在这种情况下，它们是位于两个不同 SCSI 总线上的两个内部磁盘。这两个启动设备的路径由斜杠 (/) 分隔的数字和点 (.) 组成，斜杠表示总线转换器，点表示卡、插槽编号和地址。有时你需要解码这些路径，以确定启动设备映射到系统上的哪些硬件设备。在我们的情况下，我们只有两个内部磁盘，一个在总线 1 上，另一个在总线 2 上。

*PATH* 命令显示主启动设备是内部总线 1 上的磁盘，备用启动设备是内部总线 2 上的磁盘。

当我在前面的示例中发出 *BOOT* 命令时，我指定了 *p0* 设备，它对应于 *SEARCH* 命令结果中显示的内部总线 1 上的磁盘。我回应说确实想与 IPL 交互，这在启动系统时通常不是这种情况；但是，我想在即将出现的 IPL 部分简要查看一下 IPL。

![](img/eff8b9287a5f38c5adf538f24aacf29e_173_0.png)

通过 BCH 发出的 PDC 命令对许多新的系统管理员来说是一个谜。我在这一部分涵盖了足够的内容，让你能够熟悉你的系统，以便查看那些非直观的命令，即那些提供有用信息但不更改系统设置的命令。如果你发出更改配置的命令，请务必小心。例如，你可以配置和重新配置处理器。除非你的系统未使用且你可以自由修改 CPU，否则你不应该试验此命令。

### PDC 命令

以下是在撰写本文时 N-Class 系统上可用的 PDC 命令列表。尽管本章示例中使用了 L-Class 系统，但 L-Class 和 N-Class 的 PDC 是相似的。请记住，你系统的 PDC 命令可能与列出的略有不同。PDC 偶尔会更新，因此 N-Class 的列表也可能与表 3-4 中显示的略有不同。

![](img/eff8b9287a5f38c5adf538f24aacf29e_174_0.png)

#### 表 3-4 N-Class 的 PDC 命令列表

| 命令 | 说明 |
| :--- | :--- |
| ALL | 显示通常驻留在 INFORMATION 菜单中的其他显示命令提供的全部信息集合。 |
| AUTO | 用于显示或设置 AUTOBOOT、AUTOSearch 或 AUTOSTART 标志的状态。 |
| BOOT | 启动引导序列。 |
| BOOTID | 显示或修改现有处理器的引导 ID。 |
| BOOTINFO | 显示用于系统启动的配置参数的 PDC 级信息。 |
| BOOTTIMER | 在系统中设置一个延迟值，以等待外部大容量存储设备上线。 |
| CACHE | 显示所有安装处理器的缓存内存部分的信息。 |
| CHASSISCODES | 显示最近的机箱代码队列。 |
| CHIPREVISIONS | 用于显示系统中主要超大规模集成电路 (VLSI) 的版本。 |
| CLEARRIM | 用于清除（置零）处理器内部内存 (PIM) 的内容。 |
| CONFIGURATION | 用于进入配置子菜单。 |
| COPROCESSOR | 显示所有安装协处理器的信息。 |
| CPUCONFIG | 允许用户配置或取消配置系统中的处理器。 |
| DEFAULT | 用于将系统设置为预定义的默认值。 |
| DISPLAY | 用于重新显示当前菜单。 |
| FAN | 用于显示或设置系统内部风扇的速度。 |
| FASTBOOT | 用于显示或设置 fastboot 标志。 |
| FWREVISION | 显示当前安装固件的版本。 |
| HELP | 返回指定命令、菜单或系统本身的帮助信息。 |
| INFORMATION | 用于访问信息菜单。 |
| I/O | 显示系统中所有 I/O 模块上的 I/O 接口。 |
| LANADDRESS | 允许用户显示站点地址。 |
| LANCONFIG | 用于配置 LAN 卡。 |
| MAIN | PDC 的用户界面。 |
| MEMORY | 显示系统中物理内存总量以及配置内存的内存信息。 |
| MEMREAD | 用于读取内存位置。 |
| MONITOR | 允许用户查看和更改图形卡的监视器类型。 |
| PATH | 用于设置和/或显示来自稳定存储的系统路径。 |
| PDT | 显示或清除页面解除分配表 (PDT)。 |
| PIM | 显示处理器内部内存 (PIM) 信息。 |
| PROCESSOR | 显示系统中处理器(s) 的信息。 |
| RESET | 重置机器状态。 |
| SEARCH | 搜索系统中的启动设备。 |
| SECURE | 用于显示或设置安全模式标志。 |
| SERVICE | 允许用户进入服务菜单。 |
| TIME | 以 GMT 读取或设置实时时钟。 |
| WARNINGS | 显示可能由前一次 PDC selectest 执行导致的警告消息。 |




### 初始系统加载

如前所述，初始系统加载器（ISL）在 PDC 之后运行。通常你只需从 ISL 运行“autoboot”序列，但是，你可以在 ISL 提示符下运行许多命令。

承接前面示例的进展，我们选择从设备 *p0* 进行 *BOOT*（启动），并与 IPL 进行交互，如下例所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_176_0.png)

```text
Main Menu: Enter command or menu > bo p0
Interact with IPL (Y, N, Or Cancel)? > Y

Booting ...
Boot TD Dependent Code (IGDC) revision 1

HARD Booted.

ISL Revision A.00.33 OCT 26, 1994

ISL> ?

HELP      Help Facility
LS        List ISL utilities
AUTOBOOT  Set or clear autoboot flag in stable storage
AUTORESEARCH
SET or clear autoresearch flag in stable storage
PRIMARYBOOT
Modify primary boot path in stable storage
ALTPATH   Modify alternate boot path in stable storage
CONSPATH  Modify system console path in stable storage
DISPLAY   Display boot and console paths in stable storage
LSBUTOPTL List contents of autoboot file
FASTSIZE  Sets or displays FASTSIZE
B00SUPPORT Boots the a800 Support Kernel from the boot device
700SUPPORT Boot the a700 Support Kernel from the boot device
READNV    Displays contents of one word of NVM
REBADRS   Displays contents of one word of stable storage
LSBATCH   List contents of batch file
BATCH     Execute commands in batch file
LREST     List contents of EST (Extended Self Test) file
EST       Execute commands in EST (Extended Self Test) file

Enter 'LS' to see a list of the ISL utilities.

ISL>
```

输入 *?* 会列出我们可以发出的 ISL 命令列表。发出 *DISPLAY* 命令会显示启动和控制台路径，而 *LS* 则列出可用的 ISL 实用程序，如下例所示：

```text
ISL> display
Fastsize value is 0000000F
Autoboot is ON (enabled)
Autosearch is ON (enabled)
Primary boot path is 0/0/1/1.2.0.0.0.0.0
Primary boot path is (hex) 0/0/1/1.2.0.0.0.0.0
Alternate boot path is 0/0/2/0.2.0.0.0.0.0
Alternate boot path is (hex) 0/0/2/0.2.0.0.0.0.0
System console path is 0/0/4/0.0.0.0.0.0
System console path is (hex) 0/0/4/0.0.0.0.0.0

ISL> ls
Utilities on this system are:

| filename | type   | start | size | created       |
| :------- | :----- | :---- | :--- | :------------ |
| ODE      | -12960 | 584   | 1216 | 00/01/23 15:45:48 |
| HPUX     | -12928 | 540   | 800  | 99/10/28 15:23:53 |

ISL>
```

DISPLAY 产生了我们基于前一节中由 PDC 产生的内容所预期的信息。LS 产生了两个可用的实用程序：ODE 和 HPUX。ODE 是离线诊断环境（Offline Diagnostics Environment）。以下示例展示了通过运行 ODE、查看可用命令的 HELP 命令以及列出 ODE 实用程序的 LS 来列出系统上可用的 ODE 实用程序：

```text
ISL> ode

Offline Diagnostic Environment

(C) Copyright Hewlett-Packard Co. 1993-2000
All Rights Reserved

HP shall not be liable for any damages resulting from the
use of this program.

TC  Version A.02.20
SysLib Version A.00.74
Loader Version A.00.52
Mapfile Version A.01.23
```

Type HELP for command information.

```text
ODE> help

ODE Help

Basic Commands

- HELP -- Prints detailed information to the screen, when "help <command>" or "help <var>" is typed
- LS -- List modules available on boot medium
- <Module Name> -- Load and initialize a module by typing its name
  (for more help, type "help module_name")
- MENU -- Launch ODE's ease-of-use interface
- RUN -- Run a module (after setting desired environment variables)
- Control-c (control-C) -- Abort an ODE command; pauses a module run
- RESUME -- Restart a paused module
- DISPLOG -- After running a module, display contents of a log
- EXIT -- Return to next higher level prompt

Environmental Variables

- SHOWSTATE -- Display the value of the following environment variables:
  - LOOP -- Run a test this many times
  - ERRPRINT [ON|OFF] -- Print low-level error messages to console
    (primarily for manufacturing use)
  - ERRNUM [ON|OFF] -- Print one-line, numbered errors to the console

Continue ([y]/n)? y

- ERRPAUSE [ON|OFF] -- Pause module upon error detection
- ERROR101 [ON|OFF] -- Print OMLE error messages; disable non-error and isolation message printing
- INFOPRINT [ON|OFF] -- Print informational messages to the console
- ISOPRINT [ON|OFF] -- Print fault isolation messages to the console
- ISOPAUSE [ON|OFF] -- Pause module when isolation message is generated
- LOGSIZE -- Set the size of a message log
- DEFAULT -- Reset environment variables to default state

ODE> ls

Modules on this boot media are:

| filename | type | size | created  | description                                |
| :------- | :--- | :--- | :------- | :------------------------------------------- |
| MAPPER2  | TM   | 126  | 05/01/21 | 64 bit version of the system mapping ut    |
| JOTEST2  | TM   | 88   | 05/01/21 | 64 bit version that runs ROM-based self    |
| PERFVER2 | TM   | 124  | 05/01/21 | 64 bit version that runs ROM-based self    |

ODE>
```

在此示例中，当我们运行 ODE 并发出 LS 时，示例末尾列出了三个实用程序。我总是在系统安装过程中加载 ODE，以协助诊断可能出现的系统硬件问题，HP CE（客户工程师）可能需要诊断此类问题。

接下来，我们将通过运行 HPUX 实用程序继续进行启动过程：

如前所述，*hpx* 实用程序管理 HP-UX 内核的加载，并将控制权交给内核。ISL 可以运行 hpxux 的“autoexecute”（自动执行）文件，也可以交互式地给出命令。在大多数情况下，你只需要自动启动系统。然而，在我们目前的示例中，为了查看 ISL 中的一些功能，我们决定与 ISL 进行交互。我们只需发出 HPUX 实用程序名称即可继续启动过程，如下例所示：

```text
ISL: hpxux
Boot:
 /disk/0/0/1/2.0.0.0.0.0/stand/vmunix
 7094272 + 849200 + 724128 sttext 0x241068

alloc_pdc_pages: Relocating PDC from 0xf00000000 to 0x7fab000.
gsata4: aycvc_addr = 0x0002000 for 1 pages
NOTICE: nfsa_link( ): File system was registered at index 4.
NOTICE: autofs_link( ): File system was registered at index 6.

    System Console is on the Built-In Serial Interface
    Entering cifs_init... 
    Initialization finished successfully.  slott is 8
    Logical volume 64, 0x3 configured as ROOT
    Logical volume 64, 0x4 configured as SWAP
    Logical volume 64, 0x2 configured as CDMP
    Swap device table: ( start + size given in 512-byte blocks)
    entry 0 - major is 64, minor is 0x2: start = 0, size = 2097152
    Starting the STREAMS daemons-phase 1
    Checking root file system:
    file system is clean - log replay is not required
    Root check done.
    Create SPCP device files
    Starting the STREAMS daemons-phase 2
    B3252B/9245X8 HP-UX (B.11.00) #1: Wed Nov  5 22:38:19 PST 1997

Memory information:
 physical page size = 4096 bytes, logical page size = 4096 bytes
 Physical: 2097152 Kbytes, lockable: 1574352 Kbytes, available: 18155496 Kbytes
```

```text
/sbin/ioinitrc:

/sbin/hcheckrc:
 Checking for LVM volume groups and Activating ( if any exist)
 Volume group `/dev/vg0' has been successfully changed.
 vxfs fsck: sanity check: root file system OK (mounted read/write)
 Checking file file systems
 /sbin/fsclean: /dev/vg00/lvol1 (mounted) OK
 NFS file systems are OK, non running fock
 Checking vxfs file systems
 /dev/vg00/lvol5
 vxfs fsck: sanity check: /dev/vg00/lvol5 OK
 /dev/vg00/lvol3
 vxfs fsck: sanity check: root file system OK (mounted read/write)
 /dev/vg00/lvol4
```

### HPUX 二级系统加载器 (hpx)

![](img/eff8b9287a5f38c5adf538f24aacf29e_179_0.png)

```text
vxfs fsck: sanity check: /dev/vg00/lvol4 OK
/dev/vg00/lvol5
vxfs fsck: sanity check: /dev/vg00/lvol5 OK
/dev/vg00/lvol6
vxfs fsck: sanity check: /dev/vg00/lvol6 OK
/dev/vg00/lvol7
vxfs fsck: sanity check: /dev/vg00/lvol7 OK
```

```text
(c)Copyright 1983-1997 Hewlett-Packard Co. All Rights Reserved.
(c)Copyright 1973, 1980, 1983, 1985-1997 The Regents of the Univ. of California
(c)Copyright 1984, 1984, 1986 Novell, Inc.
(c)Copyright 1986-1992 Sun Microsystems, Inc.
(c)Copyright 1985, 1996, 1998 Massachusetts Institute of Technology
(c)Copyright 1989-1993 The Open Software Foundation, Inc.
(c)Copyright 1986 Digital Equipment Corp.
(c)Copyright 1990 Motorola, Inc.
(c)Copyright 1990, 1991, 1992 Cornell University
(c)Copyright 1989-1991 The University of Maryland
(c)Copyright 1988 Carnegie Mellon University
(c)Copyright 1991-1997 Mentat, Inc.
(c)Copyright 1994 Morning Star Technologies, Inc.
(c)Copyright 1996 Progressive Systems, Inc.
(c)Copyright 1997 Isogon Corporation
```

RESTRICTED RIGHTS LEGEND
Use, duplication, or disclosure by the U.S. Government is subject to restrictions as set forth in sub-paragraph (c)(1)(ii) of the Rights in Technical Data and Computer Software clause in DFARS 252.227-7013.

Hewlett-Packard Company
3000 Hanover Street
Palo Alto, CA 94304 U.S.A.

Rights for non-DOD U.S. Government Departments and Agencies are as set forth in FAR 52.227-19-(1)(1,2).

Console Login:

我在 *Console Login:* 提示符前出现三个地方的地方对清单进行了缩写。

我们可以使用 *HPX* 实用程序发出许多选项。本章末尾的手册页详细描述了几个选项。表 3-5 列出了一些常见 *HPX* 实用程序启动选项的示例，其中一些来自 man 手册页：

![](img/eff8b9287a5f38c5adf538f24aacf29e_180_0.png)

hpx - 3




## 表 3-5 hpxux 示例

| 命令（均在 ISL> 提示符下） | 注释 |
| :--- | :--- |
| **hpxux** | 无交互 - 自动引导序列。 |
| **hpxux -s** | 将系统启动到运行级别 s，进入单用户模式。 |
| **hpxux** | 默认的引导序列通常源自 *autoexecute*，对象文件通常为 /stand/vmunix。 |
| **hpxux vmunix.test** | 引导对象文件 *vmunix.test*。 |
| **hpxux (5.2,5.0.0) /stand/vmunix** | 从路径 5.2.5.0.0 指向的磁盘上的 /stand/vmunix 进行引导。 |
| **hpxux lan(32) /stand/vmunix** | 从 LAN 引导。 |
| **hpxux -v** | 获取 HP-UX 版本号。 |
| **hp-ux ll /stand** | 列出根磁盘上 /stand 的内容。 |

![](img/eff8b9287a5f38c5adf538f24aacf29e_181_0.png)

在发出 **hpxux** 命令后执行的引导过程包括以下四个部分：

- 1. HP-UX 初始化系统硬件和设备 - HP-UX 内核定位并初始化系统硬件，如内存、I/O 总线和设备等。此时，内核设备驱动程序与 I/O 设备关联。在此过程中，您会看到系统控制台快速显示大量信息。
- 2. 创建并初始化 HP-UX 内核数据结构 - 创建了许多用于系统进程和内存、文件系统等表格。您也可以在系统控制台上查看此引导阶段的状态。
- 3. HP-UX 搜索根文件系统 - 基础文件系统包含关键系统文件，通常位于 HP-UX 引导的磁盘上。作为此过程的一部分，会运行许多命令。
- 4. HP-UX 启动名为 /sbin/init 的 init 进程 - 具有 ID 1 的 init 进程启动系统上的所有其他进程。init 进程读取 /etc/inittab 以获取指令。第 7 章中对 /etc/inittab 的内容有详细描述。

我建议您发出前文中介绍的一些 PDC、ISL 和 hpxux 实用命令，特别是那些不以任何方式修改系统、仅提供系统信息的命令。

下一节将介绍如何配置安全 Web 控制台（Secure Web Console）。

![](img/eff8b9287a5f38c5adf538f24aacf29e_182_0.png)

### 安全 Web 控制台（Secure Web Console）

![](img/eff8b9287a5f38c5adf538f24aacf29e_182_1.png)

关于使用哪种类型的控制台来配合您的 HP 9000，您有多种选择。您可以将终端连接到控制台端口，或使用浏览器和安全 Web 控制台（系统上还提供 LAN 控制台端口作为另一种选择）。此外，还有一种控制台整合解决方案，支持多达 224 个控制台，这里我不作详细介绍。安全 Web 控制台是一种连接到 HP 9000 控制台端口的设备，内置 Web 服务器，允许您使用浏览器作为控制台。这意味着，从运行浏览器的一台系统上，您可以打开多个窗口，这些窗口是不同 HP 9000 系统的控制台屏幕。这免除了在想要执行系统管理功能时从一个控制台走到另一个控制台的必要——您可以坐在运行浏览器的一台系统上管理许多系统。

在本节中，我将介绍如何配置安全 Web 控制台，并提供几张屏幕截图，以便您决定是更喜欢使用安全 Web 控制台还是专用终端作为控制台。

在撰写本文时，您可以从 http://docs.hp.com/hplex/content/swc\_inst/config.html 下载描述安装和配置安全 Web 控制台步骤的文档。我将在本节中提供一个配置示例。

### 连接和配置安全 Web 控制台

安全 Web 控制台是一种连接到您 HP 9000 的控制台端口和您的 LAN 的设备。例如，在 L 类系统中，插槽 2 中有一张核心 I/O 卡，其中包含一个 LAN 控制台端口和一个用于 UPS 和控制台的连接器——安全 Web 控制台的串行端口插入此控制台电缆中。安全 Web 控制台还有一个网络端口，以便您可以将其连接到您的 LAN。图 3-2 描绘了安全 Web 控制台的一般设置：

![](img/eff8b9287a5f38c5adf538f24aacf29e_183_0.png)

图 3-2 在即将使用的示例中 L 类系统上的安全 Web 控制台连接

请记住，您系统上的 HP 9000 连接可能与图中所示不同。连接到 UPS/控制台端口的电缆变成了图 1-1 中显示的三个连接。在我的系统中，安全 Web 控制台连接到面向计算机背面时最右侧的三个连接器之一。它的另一个连接是到 LAN 的网络连接。安全 Web 控制台还有自己的电源，因此即使计算机断电，您也可以从浏览器连接到它。

安全 Web 控制台的默认 IP 地址为 192.0.0.192。分配此地址是为了让您在安装后能够连接到安全 Web 控制台并重新配置它。

在硬件连接完成后，我们将执行以下步骤来设置运行浏览器的系统并连接到安全 Web 控制台：

- **禁用代理**
假设您正在运行受支持的浏览器版本，在安全 Web 控制台配置完成之前，您希望“禁用代理”或使用“无代理”。

- **添加路由**
使用以下命令从运行浏览器的计算机向安全 Web 控制台添加路由：
`route add 192.0.192 63.88.95.15`

在此示例中，我运行浏览器的计算机 IP 地址为 63.88.95.15。

- **检查连接**
使用 **ping** 命令检查运行浏览器的计算机与安全 Web 控制台默认 IP 地址之间的连接：
`ping 192.0.0.192`

使用 **arp**

如果使用 **ping** 未收到响应，您可能需要对 PC 和 UNIX 系统使用 **arp**，如下所示：

```
PC:    arp -s 192.0.0.192 00-10-83-fa-3f-11
UNIX:  arp -s 192.0.0.192 00:10:83:fa:3f:11
```

在我的配置中，我还没有需要使用 **arp** 命令，然而，前面提到的文档建议如果确实事 **ping** 失败，则使用 **arp** 命令。在使用 **arp** 后重新发出 **ping** 命令以检查您的连接。-s 选项用于静态 arp。

**Web 浏览器**

随着 **ping** 成功，您现在可以通过浏览器访问安全 Web 控制台。

图 3-3 显示了我执行的步骤。您可以看到在我的 PC 的命令行上使用 **route** 和 **ping** 来获得对安全 Web 控制台的访问权限：

![](img/eff8b9287a5f38c5adf538f24aacf29e_186_0.png)

图 3-3 带有安全 Web 控制台的 **route** 和 **ping**

此屏幕截图未显示我在提示符发出命令之前执行的“禁用代理”步骤。

> **注意：** 有时我通过从安全 Web 控制台直接连接一根交叉 LAN 电缆到我的笔记本电脑来配置安全 Web 控制台。在完成初始配置步骤后，我将安全 Web 控制台连接到 LAN，并使用桌面系统通过浏览器访问它。与我便携机的连接仅是一个临时连接，目的是使用其最终 IP 地址配置安全 Web 控制台。

在建立连接并且我的计算机上的浏览器正确配置后（之前已禁用代理服务器），我可以使用浏览器连接到安全 Web 控制台上的 Web 服务器。在大多数情况下，您必须位于同一子网中才能正常工作。图 3-4 是一个屏幕截图，显示我使用 http://192.0.0.192 指定了安全 Web 控制台的预配置 IP 地址：

![](img/eff8b9287a5f38c5adf538f24aacf29e_187_0.png)

初始安全 Web 控制台屏幕

“欢迎”屏幕确认我们执行了必要的配置以建立与安全 Web 控制台的初始连接。在此屏幕选择“确定”后，您可以继续进行安全 Web 控制台的配置。

下一个屏幕（图 3-5）显示了与安全 Web 控制台相关的初始信息，当您选择“确定”时，系统会提示您输入这些内容。此信息是针对安全 Web 控制台的管理人员，而不是针对 HP 9000 的。在即将到来的示例中，我放大以便您能更清楚地看到安全 Web 控制台的信息。图中未显示浏览器信息，但从这一点开始，浏览器信息与安全 Web 控制台的配置无关紧要。

![](img/eff8b9287a5f38c5adf538f24aacf29e_188_0.png)

图 3-5 第一个管理员账户的安全 Web 控制台屏幕



添加完所有这些信息后，你就配置好了初始管理员账户。正如我们稍后所见，你可以向 Secure Web Console 添加后续的管理员和运维员账户。

下一个屏幕（图 3-6）显示了我们将要对 Secure Web Console 进行的网络相关配置。由于该设备自带预设的 IP 地址，我们现在将为设备分配专用的 IP 地址。

![](img/eff8b9287a5f38c5adf538f24aacf29e_189_0.png)

在图 3-6 中，我展示了你可以选择的两种终端类型。在这个“配置 IP”屏幕中，你将输入 Secure Web Console 的名称以及与其连接的计算机名称。所有与 IP 相关的信息也都在此屏幕中输入。Secure Web Console 需要一个专用 IP 地址，因为你直接连接到它以建立与 HP 9000 的控制台连接。

当所有信息添加完成后，我们在此屏幕上选择“确定”，随后如图 3-7 所示显示以下消息：

![](img/eff8b9287a5f38c5adf538f24aacf29e_190_0.png)

图 3-7 初始 Secure Web Console 设置完成

在图 3-7 中选择“确定”后，我们可以使用配置过程中分配给 Secure Web Console 的 IP 地址重新连接。在我们的案例中，我们将使用 http://15.88.85.14 进行重连，如图 3-8 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_191_0.png)

图 3-8 Secure Web Console 登录屏幕

我们使用之前为 Secure Web Console 管理员定义的用户名和密码登录，随后如图 3-9 所示建立连接：

![](img/eff8b9287a5f38c5adf538f24aacf29e_192_0.png)

图 3-9 Secure Web Console 菜单

此时，你可以从众多与 Secure Web Console 相关的功能中进行选择，例如配置更多用户，或者访问 HP 9000 的控制台，这是连接该设备的主要目的。“访问控制台”选择项会显示 HP 9000 的控制台，如图 3-10 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_193_0.png)

图 3-10 初始 Secure Web Console 屏幕

请注意，当我们选择 *Access console* 时，是以 root 身份登录的。你可以使用 Secure Web Console 菜单来配置额外的管理员和运维员（在我们的示例中，我们只配置了一名管理员，没有配置运维员），以便通过 Secure Web Console 让多个用户访问你的 HP 9000。

Secure Web Console 可以很好地替代在每个 HP 9000 上使用专用控制台。我希望为你提供配置 Secure Web Console 的基本信息、配置文档的 URL 以及产品概述，以帮助你判断它是否适合你的环境。

### 配置 Guardian 服务处理器 (GSP)

Guardian 服务处理器 (GSP) 是大多数 HP 9000 系统（如 L 类和 N 类）内置的处理器，可用于本地或远程系统管理功能。我不会详细介绍 GSP 的用法，但会介绍其初始配置。初始配置非常重要，因为在配置之前第一个访问 GSP 的人默认成为 GSP 管理员。

你可以通过 `^b` (控制 b) 访问 GSP。如果 GSP 尚未配置，任何获得控制台访问权限的人都可以输入 `^b` 并进入系统。我建议你在安装系统后尽快执行 GSP 配置。

以下示例展示了发送 `^b` 指令，结果进入 GSP> 提示符，并发送 `he` 指令以获取帮助：

```text
Service Processor login:
Service Processor password:

          Hewlett-Packard Guardian Service Processor

          9000/800/12000-44 System Name: uninitialized

GSP Host Name:  uninitialized
GSP>
GSP Host Name:  uninitialized
GSP> he


he
HE
AC : Alert Display Configure            PC : Power Control
AR : Config. Automatic System Restart  PS : Power Management Module status
CA : Configure serial port parameters   RP : Reset password configuration
CP : Log repair info in history buffer  RS : System reset through RST signal
CL : Display console history            SUM : Set Display Mode (hex or text)
CC : Return to Console Mode            SS : Activate a system session
C : Default configuration               SL : Display SPU status logs
D1 : Disconnect remote or LAN console   SO : Security options & access control
DR : Disable remote or LAN console      SS : System's processor status
ER : Enable remote or LAN console       TC : System reset through INIT signal
NB : Display the available commands     TS : Sends a message to other terminals
IT : Modify GSP inactivity timeouts     VFF : Activities Alert Log Display
LC : Configure LAN console               WHO : Displays list of GSP connected users
LS : Display LAN console status          XD : GSP Diagnostic and Reset

MR : Modem Reset
MS : Display the status of the Modem

XU : Upgrade the GSP Firmware

GSP Host Name: uninitialized
GSP:
```

可以看到，在发出 `^b` 后，登录既不需要用户名也不需要密码。这是因为尚未配置 GSP 用户，因此任何人都可以通过系统控制台的 `^b` 访问此菜单。

这里有若干命令不应对未授权用户开放，因此我们将采取的第一步是通过 `SO` 设置安全选项：

```text
GSP> so
SO
This command allow you to modify the security options and access control.
GSP wide parameters are:
. Login Timeout: 1 minutes.
. Number of Password Faults allowed: 3
. Flow Control Timeout: 5 minutes.
Do you want to modify the GSP wide parameters? (Y/N)

User number 1 parameters are:
. User's Name:
. User's Login:
. Organization's Name:
. Dial-back configuration: Disabled
. Access Level: Operator
. Mode: Simple
. User's state: Disabled
Do you want to modify the user number 1 parameters? (Y/N/Q to quit) :
```

从这个菜单中，你可以更改 GSP 全局参数并建立 GSP 用户。第一次进入此屏幕时添加的第一个用户将是 GSP 系统管理员。这是你最初需要设置的，以确保系统安全。你可以添加一个管理员和 19 个用户。这是一个重要步骤，因为从现在起用户必须添加用户名和密码才能访问 GSP。你添加的用户信息如前所示，解释起来不言自明。

### 配置 Guardian 服务处理器 (GSP)

除了配置用户，GSP 还有许多有用的功能，因此我鼓励你去尝试。我经常使用的一个功能是发出 **CL** 指令以显示控制台历史，如本章示例中使用的 L 类系统所示：

```text
> cl

1.

Firmware Version 39.46
Duplex Console IO Dependent Code (IODC) revision 1

(C) Copyright 1995-1998, Hewlett-Packard Company, All rights reserved
Processor State CoProcessor State Cache Size
Number Speed Inst Data
0 440 MHz Active, Functional 512 KB 1 MB
1 440 MHz Idle Functional 512 KB 1 MB
Central Bus Speed (in MHz) : 62
Available Memory : 2097152 KB
Good Memory Required : 11468 KB
```

按 Q/q 退出，按 Enter 继续：

```text
Primary boot path: 0/0/1/1.2
Alternate boot path: 0/0/2/0.2
Console path: 0/0/4/0.0
Keypad path: 0/0/4/0.0

WARNING: The non-destructive test bit was set, so memory was not tested
 destructively. Information only, no action required.

Processor is booting from first available device.
To discontinue, press any key within 10 seconds.
10 seconds expired.
Processing...
Trying Primary Boot Path
.
Booting...
Boot IO Dependent Code (IODC) revision 1
```

按 Q/q 退出，按 Enter 继续：

```text
HARD Booted.
ICL Revision A.00.38 OCT 26, 1994
ICL booting hpx
Boot
: disk(0/0/1/1.2.0.0.0.0.0.0;/stand/ovmanix
6340608 + 821576 + 695024 start 0x210ce8

alloc_pdc_pages: Relocating PDC from 0xf0000000 to 0xf7ab000.
gste04: svsev_cd00: 0x00002000 for 1 pages
Unexpected interrupt on EBR bit 32
NOTICE: aoutfs_link(): File system was registered at index 3.
NOTICE: nfsl_link(): File system was registered at index 5.

System Console is on the Built-In Serial Interface
Logical volume 64, 0x3 configured as ROOT
Logical volume 64, 0x2 configured as SWAP
Logical volume 64, 0x2 configured as DUMP
Swap device table: (start & size given in 512-byte blocks)
entry 0 = major is 64, minor is 0x2; start = 0, size = 2097152

Starting the STREAMS daemons-phase 1
Checking root file system.
log replay in progress
replay complete - marking super-block as CLEAN
Root check done.
Create SCSI device files
Starting the STREAMS daemons-phase 2
B2352B/9245XB HP-UX 1B.11.00) #1: Wed Nov 5 22:38:19 PST 1997

Memory information:
  physical page size = 4096 bytes, logical page size = 4096 bytes
  Physical: 2097152 Kbytes, lockable: 1575156 Kbytes, available: 1816368 Kbytes

/sbin/loginctl:
/dev/vg00/lvol0: 34 files, 0 icount, 25716 used, 173665 free (81 frags, 21698 blks, ...)

/sbin/iocheckrc:
Checking for LVM volume groups and Activating (if any exist)
Volume group "/dev/vg00" has been successfully changed.
Activated volume group
Volume group "/dev/vg01" has been successfully changed.
Resynchronized volume group /dev/vg00
Resynchronized volume group /dev/vg01
vxs fsck: sanity check: root file system OK (mounted read/write)
Checking nfs file systems
/sbin/fascienn: /dev/vg00/lvol1 (mounted) ok
NFS file systems are OK, not running fask

Checking vxfs file systems
/dev/vg00/lvol0:
vxfs fsck: sanity check: /dev/vg00/lvol8 needs checking
log replay in progress
replay complete - marking super-block as CLEAN
/dev/vg01/lvol9
vxfs fsck: sanity check: /dev/vg00/lvol9 needs checking
log replay in progress
replay complete - marking super-block as CLEAN
/dev/vg00/lvol3:
vxfs fsck: sanity check: root file system OK (mounted read/write)
/dev/vg00/lvol4:
vxfs fsck: sanity check: /dev/vg00/lvol4 needs checking
log replay in progress
replay complete - marking super-block as CLEAN
/dev/vg00/lvol5:
vxfs fsck: sanity check: /dev/vg00/lvol5 needs checking
log replay in progress
replay complete - marking super-block as CLEAN
/dev/vg00/lvol6:
vxfs fsck: sanity check: /dev/vg00/lvol6 needs checking
log replay in progress
replay complete - marking super-block as CLEAN
/dev/vg00/lvol7:
vxfs fsck: sanity check: /dev/vg00/lvol7 needs checking
log replay in progress
replay complete - marking super-block as CLEAN

(c) Copyright 1983-1997 Hewlett-Packard Co., All Rights Reserved.
(c) Copyright 1979, 1980, 1981, 1985-1993 The Regents of the Univ. of California
(c) Copyright 1980, 1984, 1986 Novell, Inc.
```





(c)版权 1986-1992 Sun Microsystems, Inc.
(c)版权 1985, 1986, 1988 麻省理工学院
(c)版权 1989-1993 开放软件基金会, Inc.
(c)版权 1986 Digital Equipment Corp.
(c)版权 1990 Motorola, Inc.
(c)版权 1990, 1991, 1992 康奈尔大学
(c)版权 1989-1993 马里兰大学
(c)版权 1988 卡内基梅隆大学
(c)版权 1991-1999 Mentor, Inc.
(c)版权 1996 Morning Star Technologies, Inc.
(c)版权 1996 Progressive Systems, Inc.
(c)版权 1997 Isogen Corporation.

### 受限权利声明

美国政府的**使用、复制或披露**均受限于 DFARS 252.227-7013 中技术数据和计算机软件条款子段落 (c)(1)(ii) 的规定。

Hewlett-Packard 公司
3000 Hanover Street
Palo Alto, CA 94304 美国

非美国国防部的美政府部门和机构的权利如 FAR 52.227-19(c)(1,2) 所述。

```
/sbin/autoframe: DHCP access is disabled (see /etc/autoframe.log)

/sbin/rc: failed to read row and column info from screen

HP-UX Start-up in progress.
```

- 配置系统跟踪转储 `OK`
- 挂载文件系统 `OK`
- 更新内核和可加载模块 `N/A`
- 初始化可加载模块 `N/A`
- 设置主机名：`OK`
- 设置特权组 `N/A`
- 晚期启动 `OK`
- 如果需要保存系统崩溃转储 `N/A`
- 启用 (sysctl) 交换空间 `OK`
- 启动同步守护进程 `OK`
- 配置 HP 光纤通道接口 `OK`
- 配置回环接口 (lo0) `OK`
- 启动软件分发代理守护进程 `OK`
- 配置所有未配置的软件文件集 `OK`
- 恢复先前崩溃文件 `N/A`
- 清理 DUMP `OK`
- 列出和/或启动临时文件 `OK`
- 清理旧日志文件 `OK`
- 启动系统消息日志守护进程 `OK`
- 启动物理分配器守护进程 `OK`
- 启动网络跟踪和日志守护进程 `OK`
- 配置 HP 以太网接口 `OK`
- 配置 HP 10/100T 接口 `OK`
- 配置 HP SPP 10/100T 接口 `N/A`
- 配置局域网 (LAN) 接口 `N/A`
- 启动名称服务器守护进程 `OK`
- 启动 NPS 核心子系统 `OK`
- 启动 NIS- 服务器子系统 `OK`
- 启动 NIS- 客户端子系统 `OK`
- 启动 NIS 服务器子系统 `OK`
- 启动 NIS 客户端子系统 `OK`
- 启动 NIS 客户端子系统 `OK`
- 启动带有 Nis- 子系统的可信模式 `N/A`
- 为 MAC/LIA 访问配置伪设备 `OK`
- 启动多播路由守护进程 `N/A`
- 启动互联网服务守护进程 `OK`
- 启动动态路由守护进程 `N/A`
- 启动路由器发现协议守护进程 `N/A`
- 配置 PPP 接口 `OK`
- 启动 SARP 协议守护进程 `OK`
- 启动远程系统状态守护进程 `N/A`

| 为互联网服务配置 man 页面 | CK |
|---|---|
| 启动邮件守护进程 | CK |
| 为 DDP 软件启动出站连接守护进程 | N/A |
| 启动 SNMP 主网络管理守护进程 | OK |
| 启动 SNMP MIB 网络管理子代理 | N/A |
| 启动 SNMP HP-DNIX 网络管理子代理 | N/A |
| 启动 SNMP MIB-2 网络管理子代理 | OK |
| 启动 SNMP 陷阱守护进程 | OK |
| 启动 D/2 损坏 | N/A |
| 如需要启动 FIP 守护进程 | CK |
| 启动 Iacon 许可证服务器守护进程 | N/A |
| 启动远程本地守护进程 | OK |
| 在 TCR 端口 7000 启动 X 字体服务器 | OK |
| 启动 vt 守护进程 | OK |
| 启动时间同步 | N/A |
| 启动记账 | N/A |
| 启动密码/组辅助子系统 | OK |
| 启动 HP 磁盘阵列管理器守护进程。 | OK |
| 启动磁盘阵列监控守护进程。 | OK |
| 启动打印假脱机 | N/A |
| 启动 HP 分布式打印服务 | CK |
| 启动时钟守护进程 | N/A |
| 支持工具信息文件 | OK |
| 启动环境监测守护进程 | OK |
| 启动审计子系统 | N/A |
| 启动音频服务器守护进程 | N/A |
| 启动分布式单一逻辑屏幕守护进程 | OK |
| SAM 系统管理配置 | OK |
| 重新初始化软件分发代理守护进程 | OK |
| 配置 HP 光纤通道大容量存储接口 | OK |
| 启动 NFS 服务器子系统 | N/A |
| 启动 X 打印服务 | N/A |
| 启动 ColoPulsion 应用服务器 | OK |
| 启动 CDE 登录服务器 | CK |

系统已就绪。

```
GenericSysName [HP Release B.11.00] (see /etc/issue)
Console Login:
*****30/100 Mb/s LAN/1000 Networking*****
Fri May 26 EDT 2000 15.43:26 401827 DASTERT Subsys:BASE100 Loc::00000
<<001> HPDCRS 10/100BASE-T driver detected bad cable connection between
the adapter in slot 0 and the hub or switch.
<<001> HPDCRS 10/100BASE-T driver detected bad cable connection between
the adapter in slot 0 and the hub or switch.
```

```
GenericSysName [HP Release B.11.00] (see /etc/issue)
Console Login: root
Password:
```

此列表显示了一次平稳的启动；然而，你可能会遇到一些与启动相关的问题，并且你可以随时通过 ^b 生成此列表以回顾启动时发生的事件序列。

你可以按照以下列表中的所示使用 **ps** 获取电源模块的状态：

```
GSP> **ps**
```

## 配置守护服务处理器 (GSP)

![](img/eff8b9287a5f38c5adf538f24aacf29e_200_0.png)

这显示我们安装了两个电源，第三个未安装。

你可以按照以下列表中的所示使用 `ss` 查看处理器状态：

```
GSP> ss

SS

System Processor Status:
Monarch Processor: 0

Processor 0 is : Installed and Configured
Processor 1 is : Not Installed
Processor 2 is : Not Installed
Processor 3 is : Installed and Configured

GSP Host Name: uninitialized
GSP>
```

完成 GSP 相关工作后，你只需在 GSP 提示符下发出 `co` 即可从 GSP 提示符返回到控制台模式，如下所示：

```
GSP> co

CO
```

正在离开守护服务处理器命令接口并进入控制台模式。按 Ctrl-B 以重新激活 GSP 命令接口。

GenericSysName [HP Release B.11.00] (see /etc/issue)
Console Login:

任何时候你在控制台上，都可以发出 ^b 访问 GSP 发出任何 GSP 命令，然后通过 co 返回控制台模式。

以下是 N-Class 系统在本著作时可用的 GSP 命令列表。虽然本章示例中使用了 L-Class 系统，但 L-Class 和 N-Class 的 GSP 是相似的。请记住，你系统的 GSP 命令可能与此处列出的略有不同。GSP 偶尔会更新，因此 N-Class 的列表也可能与表 3-6 中显示的有所不同。

### 表 3-6 N-Class GSP 命令列表

| 命令 (功能) | 说明 |
| :--- | :--- |
| AR (Config) | 配置自动系统重启。 |
| CA (Config) | 配置异步和调制解调器参数。 |
| CE (Chassis Codes) | 在 SAS 机箱代码历史中记录机箱代码。 |
| CL (Console) | 显示控制台历史。 |
| CO (Console) | 返回控制台模式。 |
| DC (Config) | 默认配置。 |
| DI (Remote) | 断开远程或局域网 (LAN) 控制台。 |
| DR (Remote) | 禁用远程或局域网 (LAN) 控制台访问。 |
| ER (Remote) | 启用远程或局域网 (LAN) 控制台访问。 |
| HE (Help) | 显示可用命令列表。 |
| IT (Admin) | 修改 SAS 无操作超时。 |
| LC (Config) | 配置已连接 LAN 和 PPP 控制台。 |
| LR (Paging) | 为寻呼保留调制解调器。 |
| LS (Console) | 显示已连接 LAN 和 PPP 控制台状态。 |
| MR (Remote) | 调制解调器重置。 |
| MS (Remote) | 显示调制解调器状态。 |
| PC (Remote) | 远程电源控制。 |
| PG (Paging) | 配置寻呼。 |
| PS (Status) | 显示电源状态。 |
| RP (Reset) | 通过 RST 信号进行系统重置。 |
| SE (Session) | 在本地或远程端口激活系统会话。（每个远程和本地控制台一个会话。） |
| SL (Status) | 显示 SPU 状态日志。 |
| SO (Admin) | 配置安全选项和访问控制。 |
| SS (Reset) | 显示系统处理器状态。 |




### 第 3 章中使用的命令的手册页

以下部分包含第 3 章中使用的命令的手册页副本。这为您在进行系统管理日常工作中发出常用命令时提供了快速参考。手册页，更常见的称呼是 man 页，已完整列出。

![image](img/eff8b9287a5f38c5adf538f24aacf29e_205_0.png)

#### boot

**boot** - 引导过程概述。

| boot(1M) | 仅限系列 700/800 | boot(1M) |
| :--- | :--- | :--- |
| NAME | | |

### NAME

boot - 引导过程

### DESCRIPTION

系列 700 和 800 的引导过程涉及执行三个软件组件：

- pdc（参见 pdc(1M)），
- isl（参见 isl(1M)），以及
- hpx（参见 hpx_800(1M)）。

处理器复位（RESET）后，pdc，即处理器相关代码（固件），执行自检并初始化处理器。然后它加载并转移控制权给 isl，即操作系统无关的初始系统加载器。接着，isl 加载并转移控制权给 hpx 实用工具，即 HP-UX 特定的引导加载器。随后 hpx 从 HP-UX 文件系统下载 HP-UX 内核对象文件，并将控制权转移给已加载的内核映像。

### SEE ALSO

hpx(1M), hpx_800(1M), isl(1M), pdc(1M)。

#### hpx

hpx - 引导 HP-UX 操作系统。

hpxux(1M) hpxux(1M)

### NAME

- *hpx* - HP-UX 引导

### SYNOPSIS

```
hpx [-P] [-lm] [-a[C|R|S|D] devicefile] [-fn]umber] [-istring] [boot] [devicefile]
hpx ll [devicefile] (same as hpx ls -aflm)
hpx ls [-a]in] [devicefile]
hpx set autofile devicefile string
hpx show autofile [devicefile]
hpx -v
hpx restore devicefile (Series 700 only; see DEPENDENCIES.)
```

### DESCRIPTION

*hpx* 是 HP-UX 专用的二级系统加载器（SSL）实用工具，用于引导（关于初始系统加载器，参见 isli(M)）。它支持以下摘要中所示的操作，如 SYNOPSIS 中所示，并在本 DESCRIPTION 中详细说明：

- *boot*：从 HP-UX 文件系统或原始设备加载对象文件，并将控制权转移给已加载的映像。（注意：boot 操作是位置相关的。）
- *ll*：以类似于 `ls -aflm` 的格式列出 HP-UX 目录的内容。（参见 `lsli`；`ls` 仅适用于具有 HFS 文件系统的本地磁盘。）
- *ls*：列出 HP-UX 目录的内容。（参见 `lsli`；`ls` 仅适用于具有 HFS 文件系统的本地磁盘。）
- *show autofile*：显示自动执行文件的内容。
- *set autofile*：将自动执行文件的内容更改为 *string* 指定的内容。
- *-v*：显示 hpx 实用工具的版本号和发行号。
- *restore*：从格式正确的可引导磁带恢复系统。（系列 700 专用；参见 DEPENDENCIES。）

hpx 命令可以从键盘交互输入，也可以通过 isil 自动执行文件提供。

hpx 仅限于对由 pdc(1M) 初始化的接口进行操作。在大多数情况下，操作仅限于引导设备接口。

### Notation

hpux 接受许多选项中的数字（数值常量）。数字遵循 C 语言关于十进制、八进制和十六进制常量的表示法。前导 0（零）表示八进制，前导 0x 或 OX 表示十六进制。例如，037、0x1F、0x1F 和 31 都表示同一个数字，即十进制 31。

hpux 的 boot、ll、is、set autofile、show autofile 和 restore 操作接受 devicefile 规范，其格式如下：

manager/w.x.y:z/filename

devicefiles 规范由设备名和文件名组成。设备名（manager/w.x.y:z/n）包含一个 I/O 系统管理器（设备或接口驱动程序）的通用名称（例如 disc）、通往该设备的硬件路径以及次要号。如果使用默认值，可以完全省略 manager 名称。w.x.y.z 是通往设备的物理硬件路径，标识总线转换器、槽号和硬件地址。对于系列 700 机器，有一组助记符可用于替代硬件路径。n 是控制管理器依赖功能的次要号。文件名部分，filename，是标准的 HP-UX 路径名。某些 hpux 操作对特定组件有默认值。仅包含设备部分的 devicefile 规范指定一个原始设备。包含文件名的 devicefile 规范意味着该设备包含一个 HP-UX 文件系统，且该 filename 位于该文件系统中。

典型的 boot devicefile 规范是：

disc(2/4.0.0)/stand/vmunix

其中 manager 是 disc，通往磁盘设备的硬件路径是 2/4.0.0，默认显示的次要号为 0，而 /stand/vmunix 是引导设备的文件名。

hpux 现在支持合并的 manager 列表：disc、tape 和 lan。manager disc 管理所有通过 HP-IB（原为 dsic0）连接的 CS/80 磁盘；通过 HPP111 接口（原为 dsic1）连接的 CS/80 磁盘；所有通过 NIO HP-IB（原为 dsic2）连接的磁盘设备；所有通过 SCSI（原为 dsic3）连接的磁盘设备，以及所有 audiochanger 磁盘设备（原为 dsic3）。manager lan 通过基于 HP26532A NIO 的 LAN 接口（原为 lanll）管理远程引导。目前仅在此卡上支持远程引导，不支持任何基于 CIO 的 LAN 卡。manager tape 通过 HP-IB（原为 tape1）管理 HPP794、HPP797 和 HPP7980 磁带机，通过 SCSI（原为 tape2）管理磁带机。

devicefile 规范中的硬件路径是一串数字，每个数字后跟斜杠 (/)，后跟一串由点 (.) 分隔的数字，每个数字按顺序从总线地址到设备地址标识一个硬件组件。带有斜杠后缀的硬件组件表示总线转换器，在您的机器上可能不需要。例如，在 w.x.y.z 中，w 是总线转换器的地址，x 是 MIO-UBS 模块的地址，y 是 CIO 槽号，z 是 HP-IB 地址或 HPP111 总线地址。

devicefile 规范中的次要号 n 控制驱动程序相关的功能。（参见手册“Configuring HP-UX for Peripherals”中特定驱动程序的次要号位分配）。

文件名是标准的 HP-UX 路径名。不需要前导斜杠 (/)，指定前导斜杠也不会引起问题。

### Defaults

hpx 用于完成命令的默认值通过一系列步骤获取。首先，使用命令中明确指定的任何组件。如果命令不完整，hpx 尝试根据 pdc 维护的信息（参见 pdc(8M)）构建默认值。如果没有足够的信息来完成命令，则搜索自动执行文件。如果搜索失败，命令中剩余未解决的组件将由硬编码默认值满足。

没有针对 manager 的硬编码默认选择；如果无法选择，hpx 将报告错误。

当未指定通往引导设备的硬件路径时，hpx 默认使用 pdc 维护的信息。硬件路径元素没有硬编码默认值。

如果未提供次要号元素，hpx 从自动执行文件中获取默认值。如果失败，则使用硬编码默认值 0。

对于 boot 命令，没有文件名的 devicefile 规范表示引导设备不包含 HP-UX 文件系统。hpx 将此解释为 NULL（而非缺失）文件名，并且不搜索默认值。如果完全缺失 devicefile 规范，hpx 将搜索默认值；选择自动执行文件内容或硬编码默认值。

有两种可能的硬编码默认 devicefile 规范。一个硬编码默认 devicefile 规范是 /vmunix。另一个硬编码默认 devicefile 规范是 /stand/vmunix。

如果您有一个 LVM 系统，其中引导卷和根卷位于不同的逻辑卷上，则内核将是 /vmunix。这是因为系统在启动时引导卷将挂载在 /stand 下。

对于所有其他配置，内核将是 /stand/vmunix。

硬编码默认值的搜索顺序是先 /stand/vmunix，然后 /vmunix。

### boot Operation

boot 操作根据可选的 devicefile 从 HP-UX 文件系统或原始设备加载对象文件。然后它将控制权转移给已加载的映像。

指定 devicefile 中缺失的任何组件都由默认值补充。例如，devicefile 为 vmunix.new 实际上会产生：

```
disc(8.0.0.0)/vmunix.new
```

而对于从 HP-IB 地址 1 的磁盘引导，devicefile 为 (8.0.1)/stand/vmunix 会产生

```
disc(8.0.1.0)/stand/vmunix
```

无论指定的 devicefile 多么不完整，boot 都会宣布用于查找对象文件的完整 devicefile 规范。伴随此信息，boot 在转移控制权之前给出已加载映像的 TEXT、DATA 和 BSS 段的大小以及入口偏移量。

boot 操作接受多个选项。注意，boot 选项必须按照语法声明中所示的位置指定




## 概要

引导操作的选项如下：

-   `-a[c|R|S|D] devicefile`
    接受一个新位置（由 `devicefile` 指定）并将其传递给加载的映像。如果该映像是 HP-UX 内核，内核将擦除其预定义的 I/O 配置，并配置为指定的 `devicefile`。如果指定了 C、R、S 或 D 选项，内核将分别把 `devicefile` 配置为控制台、根、交换或转储设备。请注意，`-a` 可以重复多次使用。

-   `-f number`
    使用指定数字，并将其作为标志字传递给加载的映像。

-   `-i string`
    在启动系统时，设置 init 的初始运行级别（参见 `init(M)`）。指定的运行级别将覆盖 `/etc/inittab` 中 `initdefault` 条目所指定的任何运行级别（参见 `inittab(4)`）。

-   `-lm`
    在 LVM 维护模式下启动系统，仅配置根卷，然后启动单用户模式。

-   `-F`
    与 Switch/UX 软件一起使用。忽略启动盘上的任何锁定。仅当确定持有锁定的处理器不再运行时，才应使用 `-F` 选项。（如果未指定此选项且磁盘被其他处理器锁定，内核将从该磁盘启动以避免损坏，因为如果其他处理器仍在使用该磁盘，会导致损坏！）

`boot` 对其可加载的对象文件施加了一些限制。它仅接受 HP-UX 魔数 `EXECMAGIC` (0407)、`SHAREMAGIC` (0410) 和 `DYNAMICMAGIC` (0413)。参见 `magic(4)`。对象文件必须包含 `HPUX AUX_ID` 类型的辅助标头，并且它必须是第一个辅助标头（参见 `a.out(4)`）。

## ll 和 ls 操作

`ll` 和 `ls` 操作列出由可选 `devicefile` 指定的 HP-UX 目录的内容。输出类似于 `ls -afl` 命令的输出，但不打印日期信息。

默认的 `devicefile` 的生成方式与 `boot` 相同，默认为当前目录。

### set autoofile 操作

`set autoofile` 操作用指定的字符串覆盖自动执行文件 `autoofile` 的内容（参见“示例”部分中的 `autoexecute`）。

### show autoofile 操作

`show autoofile` 操作显示自动执行文件 `autoofile` 的内容（参见“示例”部分中的 `autoexecute`）。

## 诊断信息

如果遇到错误，`hpux` 会打印诊断消息以指示错误原因。这些消息分为通用、引导、复制、配置和系统调用类别。系统调用错误消息在 `errno(2)` 中描述。其余消息列于下方。

### 通用

-   **devicefile 规范中的次要设备号无效**
    `devicefile` 规范中的次要设备号无法识别。

-   **devicefile 规范中的路径无效**
    `devicefile` 规范中的硬件路径无法识别。

-   **命令过于复杂，无法解析**
    命令行包含过多的参数。

-   **devicefile 规范中缺少路径**
    `devicefile` 规范需要（但不包含）硬件路径组件。

-   **panic (in hpxkboot): (display=#number, flags=#number) string**
    发生了严重的内部 `hpx` 错误。请报告给您最近的 HP 现场代表。

### 引导

-   **魔数无效**
    指定的对象文件没有可识别的魔数。

-   **flags 规范中的数字无效**
    无法识别 `-f` 选项中的 flags 规范数字。

-   **Exec failed: Cannot find /stand/venux or /venux**
    找不到 `/stand/venux` 或 `/venux`。

-   **从原始字符设备引导**
    在从原始设备引导时，指定的管理器仅具有字符接口，如果块大小不正确，这可能会导致问题。

-   **is1 不存在，请按系统 RESET 按钮以继续**
    失败的引导操作在内存中覆盖了 `is1`。无法将控制权交还给 `is1`。

-   **短读**
    指定的对象文件内部不一致；长度不足。

-   **将覆盖**
    加载指定的对象文件将覆盖 `hpx`。

### 配置

-   **无法添加路径，错误编号**
    在将硬件路径添加到 I/O 树时发生了未知错误。给出了内部错误编号。请联系您的 HP 现场代表。

-   **设备倒卷错误**
    在尝试倒卷设备时遇到错误。

-   **跳过文件错误**
    在尝试对磁带设备进行向前定位时遇到错误。

-   **跳过计数为负数**
    如果指定了跳过计数，其值必须大于或等于零。

-   **无主要设备号**
    指定的管理器在块设备或字符设备切换表中没有条目。

-   **路径与另一路径不兼容**
    指定了多个不兼容的硬件路径。

-   **路径过长**
    指定的硬件路径对于指定的管理器而言组件过多。

-   **路径过短**
    指定的硬件路径对于指定的管理器而言组件过少。

-   **表已满**
    指定给 `hpux` 的设备过多。

## 示例

作为以下示例的引言，这里简要概述了 HP-UX 系统引导序列。

### 自动引导

各种 HP-UX 系统上的自动引导过程遵循相似的通用序列。当 HP-UX 系统处理器通电或按下系统重置按钮时，将执行处理器相关代码（固件）以验证硬件和系统整体完整性（参见 `pdc(8M)`）。检查硬件后，`pdc` 为用户提供通过按下 Esc 键来覆盖自动序列的选项。此时，控制台上通常会显示类似以下的消息。

```
(c) Copyright. Hewlett-Packard Company. 1994.
All rights reserved.

PDC ROM rev. 130.0
32 MB of memory configured and tested.

Selecting a system to boot.
To stop selection process, press and hold the ESCAPE key...
```

如果未检测到键盘活动，`pdc` 将通过加载 `isl`（参见 `isl(8M)`）并转移控制权给它来启动自动引导序列。由于正在发生自动引导序列，`isl` 找到并执行自动引导文件，该文件在 HP-UX 系统上要求以适当参数运行 `hpux`。`isl` 在控制台上显示类似以下的消息：

```
Booting from: scsi 6 HP 2213A
Hard booted.
Fsi Revision A.02.D9 March 27, 1990
Isl booting hpux boot disk:/0;/stand/vmunix
```

`hpux`，即二级系统加载器，随后宣布其正在执行的操作，在此情况下为 `boot`，加载映像的来源 `devicefile`，以及加载映像的 TEXT 大小、DATA 大小、BSS 大小和起始地址，如下所示，然后将控制权传递给映像。

```
Booting disk(scsi,6:0)/stand/wnunix
96561e+197312+43948a start 0xc6:50
```

加载的映像随后显示大量的配置和状态消息。

### 交互引导

要以交互方式使用 `hpxux`，必须在 `pdc` 允许的间隔内按下 Esc 键以交互模式启动 `is1`。`pdc` 然后搜索并显示所有可引导设备，并提供一组引导选项。如果选择了适当的选项，`pdc` 将加载 `is1`，`is1` 将交互式地提示输入命令。显示类似以下的信息：

```
Selection process stopped.

Searching for Potential Boot Devices.
To terminate search, press and hold the ESCAPE key.

Device Selection    Device Path          Device Type
-------------------------------------------------------------------------------
    p0                  scsi.6.0            QUANTUM PD210S
    p1                  scsi.1.0            NP          2213A
    p2                  lan.ffffff-ffffff.f.f   fhoLBooT

b) Boot from specified device
a) Search for bootable devices
x) Enter Boot Administration Mode
k) Exit and continue boot sequence

Select from menu: b p0 is1

Trying scsi.6.0
Boot path initialized.
Attempting to load p0

Hard booted.
FSL Revision A.00.2G Mar 27, 1994
IS1...
```

尽管 `hpxux` 的所有操作和选项都可以从 `is1` 交互式使用，但也可以从自动执行文件中执行。在下面的示例中，用户输入是显示在每个 `IS1:` 提示后的该行剩余部分。每个示例的其余部分是系统显示的文字。在回顾 `hpxux` 各种选项和操作的具体示例之前，以下是自动引导过程中采取步骤的概述。尽管所示的硬件配置和引导路径针对单台 Series 800 机器，但所有型号的用户界面都是一致的。当按下系统重置按钮时，`pdc` 执行自检，假设硬件测试通过，`pdc` 宣布自身，向控制终端发送 BELL 字符，并给用户 10 秒钟的时间通过输入任何字符来覆盖自动引导序列。控制台上显示类似以下的文本：

```
Processor Dependent Code (PDC) revision 1.2
Duplex Console IO Dependent Code (IODC) revision 3

Console path            = 56.0.0.0.0.0.0.0 (dec)
                          38.0.0.0.0.0.0.0 (hex)

Primary boot path       = 44.3.0.0.0.0.0.0 (dec)
                          2c.00000003.0.0.0.0.0 (hex)
```




## 2. 指示机器从磁带启动到 ISL。这通常通过指定 `sasi.1` 作为启动路径来完成。

## 3. 在 ISL 提示符下输入以下内容：

```
ISL> hpxw restore disk[sasi.1:0]
```

此操作将从磁带将磁盘映像恢复至 `sasi.1` 处的实际磁盘。磁盘上现有的任何数据将会丢失。该命令将销毁 devicefile 指定设备的内容。对于 560 MB 驱动器，恢复过程大约需要一个小时。

注意：恢复数据的量限制为 2 GB。磁带和磁盘必须位于启动设备接口上。

此外，未来可能会由更优越的安装和恢复机制取代此命令。届时，该命令将被移除。

另请参阅
boot(1M), faxk(1M), init(1M), isl(1M), pdc(1M), errno(2), a.out(4), initab(4), magic(4).




## isl - 初始系统加载器 (isl) 概览

**isl(1M)**  
**Series 800 Com**  
**isl(1M)**

### 名称

isl - 初始系统加载器

### 描述

isl 实现了引导过程中与操作系统无关的部分。它在自检和初始化成功完成后被加载并执行。

处理器包含用于维护关键配置相关参数（例如主启动、备用启动和控制台路径）的专用内存。支持两种形式的内存：稳定存储器和非易失性存储器（NVM）。

**通常，当控制权转移到 isl 时，会发生自动引导序列。** 自动引导序列允许在没有操作员干预的情况下完成完整的引导操作。isl 以脚本方式执行自动引导文件中的命令。自动引导通过稳定存储器中的一个标志来启用。

autosearch 是一种自动定位启动和控制台设备的机制。有关更多信息，请参阅 ldc(1M)。

在自动引导序列期间，isl 显示其版本号和任何执行的实用程序名称。但是，如果自动引导被禁用，isl 在显示其版本号后，会提示从控制台设备输入。可接受的输入是任何 isl 命令名称或系统中可用的任何实用程序名称。如果发生非致命错误或者执行的实用程序返回，isl 会再次提示输入。

### 命令

isl 中有几个可用的命令。以下是一个列表及简短描述。参数可以在命令名称后的命令行中输入。它们必须用空格分隔。对于未输入在命令行的必要参数，isl 会进行提示。

1.  **? help** - 列出命令和可用实用程序
2.  **lsrcl** - 列出可用实用程序
3.  **ls** - 列出可用实用程序
4.  **autoboot** - 启用或禁用自动引导序列；参数 - on 或 off
5.  **autosearch** - 启用或禁用 autosearch 序列；参数 - on 或 off
6.  **primpath** - 修改主启动路径；参数 - 十进制的主启动路径
7.  **altPath** - 修改备用启动路径；参数 – 十进制的备用启动路径
8.  **conpath** - 修改控制台路径；参数 – 十进制的控制台路径
9.  **isauto1** - 列出自动执行文件的内容
10. **display** - 显示主启动、备用启动和控制台路径
11. **readnm** - 以十六进制显示 NVM 中一个字的内容；参数 – 十进制或标准十六进制表示法的 NVM 地址
12. **readss** - 以十六进制显示稳定存储器中一个字的内容；参数 – 十进制或标准十六进制表示法的稳定存储器地址

### 诊断

isl 通过写入控制台的错误消息和 LED 显示上的显示代码来显示诊断信息。

对于显示代码，CEQX 仅起信息提示作用。CYKX 和 CY2X 表示错误，其中一些是致命的，会导致系统停止。其他错误仅导致 isl 显示一条消息。

自动引导序列期间的非致命错误会导致自动引导序列中止，并且 isl 提示输入。在交互式 isl 会话期间，发生非致命错误后，isl 仅提示输入。

致命错误会导致系统停止。必须纠正问题并重置系统以恢复。

- **CE00** isl 正在执行。
- **CE01** isl 正在从自动执行文件进行自动引导。
- **CE02** 找不到自动执行文件，自动引导中止。
- **CE03** 未找到控制台，isl 只能进行自动引导。
- **CE05** 实用程序目录太大，isl 只读取 2K 字节。
- **CE06** 自动执行文件不一致，自动引导中止。
- **CE07** 实用程序文件头不一致：COW 值无效。
- **CE08** 自动执行文件输入字符串超过 2048 个字符，自动引导中止。
- **CE09** isl 命令或实用程序名称超过 10 个字符。
- **CE10** isl 已将控制权转移给实用程序。
- **CE11** 内部不一致：卷标签 - 致命错误。
- **CE12** 内部不一致：目录 - 致命错误。
- **CE13** 读取自动执行文件时出错
- **CE14** 从控制台读取时出错 - 致命错误。
- **CE15** 写入控制台时出错 - 致命错误。
- **CE16** 不是 isl 命令或实用程序。
- **CE17** 实用程序文件头不一致：系统 ID 无效。
- **CE18** 实用程序文件头不一致：魔数错误。
- **CE19** 实用程序将在内存中覆盖 isl。
- **CE1A** 实用程序所需的内存超过已配置的内存。
- **CE1B** 将实用程序读取到内存时出错。
- **CE1C** 将实用程序读取到内存时出错。
- **CE1D** 校验和不正确：将实用程序读取到内存。
- **CE1E** 需要控制台 - 致命错误。
- **CE1F** 内部不一致：启动设备类 - 致命错误。
- **CE21** 实用程序的目标内存地址无效。
- **CZ22** 实用程序文件头不一致：pdc 缓存条目。
- **CZ23** 内部不一致：iode_entry_init - 致命错误。
- **CZ24** 内部不一致：iode_entry_init - 控制台 - 致命错误。
- **CZ25** 内部不一致：iode_entry_init - 启动设备 - 致命错误。
- **CZ26** 实用程序文件头不一致：辅助 ID 错误。
- **CZ27** 实用程序文件类型错误。

### 另请参阅

boot(1M), hpx_800(1M), pdc(1M).

#### pdc

![](img/eff8b9287a5f38c5adf538f24aacf29e_221_0.png)

### pdc - 处理器相关代码 (pdc) 概览

**pdc(1M)**

### 名称

pdc - 处理器相关代码（固件）

### 描述

pdc 是实现所有处理器相关功能的固件，包括处理器的初始化和自检。完成后，它会加载并将控制权转移给初始系统加载器（isl(1M)）。固件行为因硬件系列而异，如下所述。

- **Series 800 行为**
  - 要从外部介质加载 isl，pdc 必须知道 isl 所在的特定设备。通常，该设备由 pdc 在稳定存储器中维护的主启动路径来标识。路径规格是一系列以 `/` 结尾的十进制数，表示总线转换器，后跟一系列以 `,` 分隔的十进制数，表示各种卡槽号和地址。第一个不指定总线转换器的数字是 MID-BUS 模块编号（即槽位编号乘以四），后跟 CIO 槽位编号。如果 CIO 槽位包含 EP-TB 卡，则下一个数字是 HP-IB 地址，后跟设备的单元号（如果设备支持单元）。如果 CIO 槽位包含终端卡，则下一个数字是端口号，对于控制台，该值必须为零。
  - 当处理器在初始化和自检完成后重置时，pdc 从稳定存储器读取控制台路径，并尝试初始化控制台设备。如果初始化失败，pdc 尝试查找并初始化一个控制台设备。用于查找控制台设备的算法取决于模型。然后 pdc 宣布主启动、备用启动和控制台路径。
  - 如果启用了自动引导（参见 isl(1M)），pdc 提供 10 秒延迟，在此期间，操作员可以通过在控制台上输入任何字符来覆盖自动引导序列。如果操作员未中断此过程，pdc 从主启动路径初始化和读取 isl。在支持自动引导的模型上，如果该路径无效且启用了 autosearch（参见 isl(1M)），则 pdc 搜索 MID-BUS 模块和 CIO 槽位以找到可启动介质。目前，autosearch 仅在 825 型上实现。
  - 如果自动引导序列不成功、被操作员覆盖或根本未启用，pdc 交互式提示操作员输入要使用的启动路径。未提供的任何必需路径组件默认为零。
  - 主启动、备用启动和控制台路径以及自动引导和 autosearch 的启用状态都可以通过 isl 修改。
- **Series 700 行为**
  - 要从外部介质加载 isl，pdc 必须知道特定的

设备 on which is l resides. 通常，该设备由 pdc 在稳定存储中维护的主启动路径（Primary Boot Path）标识。路径规范是一种 I/O 子系统助记符，根据硬件型号不同而有所变化。

当处理器在初始化和自检完成后复位，pdc 从稳定存储中读取控制台路径（Console Path），并尝试初始化控制台设备。如果初始化失败，pdc 将尝试查找并初始化一个控制台设备。查找控制台设备所使用的算法根据硬件型号不同而有所变化。

-   如果启用了自动启动（autoboot）和自动搜索（autosearch）（参见 `is l (1M)`），pdc 会等待大约 10 秒，在此期间操作员可以通过按下并按住控制台上的 ESC（转义）键来覆盖自动启动序列。

然后，系统开始搜索潜在的启动设备。如果允许搜索完成，系统将显示一个潜在启动设备的列表，并标记为缩写路径标识符（P0、P1 等）。随后显示一个简单菜单，用户在其中可以：

-   使用缩写路径标识符或完整的 Anomic 启动特定设备。
-   启动设备搜索，搜索内容包括 IPL 镜像（请注意，第一次搜索仅识别设备，未检查其内容）。
-   进入启动管理级别。
-   退出菜单并返回自动启动。
-   获取有关选项的帮助。

通过按下并按住转义键可以中止对潜在启动设备的搜索。通过按下并按住转义键也可以中止对设备内容的搜索。

如果操作员没有中断搜索过程，pdc 将从主启动路径（Primary Boot Path）初始化并读取 `is l`。

如果自动启动序列不成功、被操作员覆盖或首先未启用，pdc 将执行设备搜索并进入上述菜单。

主启动（Primary Boot）、备用启动（Alternate Boot）和控制台路径，以及自动启动和自动搜索的启用状态，可以通过 `is l` 或在 pdc 启动管理级别进行修改。

**另请参阅**
`boot(1M)`, `hpxu boot(1M)`, `is l(1M)`。

## 第 4 章

## 构建 HP-UX 内核

## 虚拟分区与内核

如第 3 章所述，使用 vPars 启动与不使用 vPars 启动不同，因为使用 vPars 的启动是通过虚拟分区监视器（**vpmo**）管理的。你仍然像平常不使用 vPars 那样启动一个 HP-UX 内核，但：**vpmo** 管理虚拟分区，允许你在同一台计算机上运行多个 HP-UX 实例。

每个虚拟分区都运行自己的 HP-UX 11i 操作系统，包括一个独特的内核。你可以定制每个虚拟分区中的操作系统和内核，以满足你的需求。

在本书前面的示例中，**vparcreate** 命令指定了内核 */stand/vmunix*，这是默认内核。你可能会以某种方式修改这个内核，以便优化用于你在每个虚拟分区中运行的应用程序。根据每个 vPar 的应用程序和特定需求，你最终可能会为每个虚拟分区拥有截然不同的内核。

在涵盖启动 vPars 的第 3 章中，我们介绍了一个指定内核路径的示例。你在 HP-UX 中的默认内核是 */stand/vmunix*。你可以对你的系统上 vPars 的内核进行实验，并可能需要在 */stand/vmunix* 之外启动这些实验内核。

![](img/eff8b9287a5f38c5adf538f24aacf29e_224_0.png)

以下示例展示了使用 **vparload** 的 *-b* 选项从一个名为 **vunix_test1** 的内核进行启动：

```
MON> vparload -p symboll -b /stand/vunix_test1
```

上述内核路径通过此 **vparload** 加载，但未进行永久更改。要对 vPars 数据库文件进行永久更改以更新内核路径，你需要发出以下命令：

```
# vparmodify -p symboll -b "stand/vunix_test1"
```

此时，vPar 已修改为具有 */stand/vunix_test1* 的默认内核。

我们首先介绍第 2 章中用于执行虚拟分区内核相关工作的流程。接下来，我们将概述设备驱动程序以及在一个虚拟分区中使用磁带设备及其设备驱动程序的示例。本章后面，在提供 HP-UX 内核背景知识时，将详细介绍修改内核参数和 HP-UX Ili 内核参数的详细描述。

### 虚拟分区内核相关工作

每个虚拟分区都有自己 HP-UX Ili 的实例，拥有自己的 HP-UX 内核。你很可能会以各种方式定制这些内核，以适应你在各自 vPars 中运行的应用程序。安装 vPars 软件时会自动为你构建内核。内核中包含了多个驱动程序，并且内核配置为可在内存中重新定位。重新定位是必需的，因为内存中会有多个 HP-UX 内核，它们必须驻留在不同的位置。在本节中，为了使 vPars 运行，你需要重新配置内核以包含 vPar 驱动程序并使内核可重定位。新内核的创建将在每个带有 HP-UX Ili 且将运行 vPar 的卷上自动完成。让我们来看看一些在幕后为你进行内核相关工作的情况。

由于内存由多个 vPar 共享，内核必须在内存中可重定位。在撰写本文时，存在允许内核作为可重定位内核构建的补丁。我们不执行与补丁相关的任何检查。

文件 `/sbin/vecheck` 是系统中需要的 vPar 文件。以下是 `/usr/conf/gen/config.sys` 的一部分列表，用于检查 `/sbin/vecheck` 是否已加载到系统中：

```
#
& if $vparvecheck
"vecheck supports kernel relocation. If it does,"
"enable the relocation options"
then
vrel= : "00 - /92453-07 linker (\\ 
spilt($57, vvers, ":") \
if { vver[1] == "B" && \
     vver[2] == 11 && vver[3] >= 25 } 
    print "${LOADOPTS_6ELOC}"
else print "${LOADOPTS_STATIC}"
fi 
fi
```

以下是随 vPar 软件加载的 `/sbin/vecheck` 的长列表：

```
# ll /sbin/vecheck
# -r-xr-xr-x  1 bin    bin    20533 Mar  5 19:01 /sbin/vecheck
```

接下来，让我们查看 `/stand/system`，看看已添加到文件中的 *vpar* 驱动程序：

```
# cat /stand/system
***************************************
* Source: /usr/core/kern/filesets.info/CORE-KRN/generic
* @(#)B.11.11_LR
* vpar
***************************************
* Additional drivers required in every machine-type to
* create a complete
* system file during cold install. This list is every driver that the
* master.d/ files do not force on the system or is not identifiable by
* ioscan.
* Other CPU-type specific files can exist for their special cases.
* see create_sysfile (lm).
```

- 驱动程序/子系统
- sba
- lba
- c720
- sctl
- sdisk
- aslo0
- cdfs
- cxperf
- dlar_psm
- dlar_psm_if
- dev_olar
- diag0
- diag1
- diag2
- dmem
- dev_config
- iomem
- nfs_core
- nfs_client
- nfs_server
- btilan
- maclan
- dlpi
- token_arq
- inet
- uipc
- tun
- telm
- tels
- netdiag1
- rms
- hpstreams
- cione
- strlog
- sad
- echo
- sc
- timod
- tirdwr
- pipedev
- pipemod
- ffs
- ldterm
- ptem
- pus
- ptm
- pckt
- ld
- fddi4
- elian
- GSCtOPCI
- i6p_drv
- bs_cam
- vxis
- vxportal

```
lvm
lv
nfsm
rpcmod
autofsc
cache5fsc
cifs
prm
vpar     <--- vpar 驱动程序在此处添加
STRMGSQ5Z 65535
nstrpty  60
dump lvol  60
maxswappchunks 2048
#
```

`vpar` 驱动程序是一个主驱动程序，在 `/usr/conf/master.d` 中描述如下所示：

```
# pwd
/usr/conf/master.d
# cat vpar
$CDIO

        vpar                  0


$$$   


$DRIVER_INSTALL

        vcs       -1                 209
        vc$       -1                  -1
        vpar_driver -1                -1


$$



$DRIVER_DEPENDENCY

        vpar
        vcs
        vpar      vpar

        vpar      vcs vcn vpar_driver
        vpar_driver       vpar


$$$

$DRIVER_LIBRARY

* The driver/library table.  This table defines which libraries a given driver depends on.  If the driver is included in the dfile, then the libraries that driver depends on will be included on the ldl(1) command line.  Only optional libraries `need' to be specified in this table. (but required ones can be included, as well). * Driver handle          <libraries> *
* subsystems first
vcs               libvpar-pdk_a
vc$               libvpar-pdk_a
vpar              libvpar-pdk_a
vpar_driver       libvpar-pdk.a
```




```
/*
 * 库表。库表中的每个元素描述
 * 一个唯一的库。flag 成员是一个布尔值，如果库应始终包含在
 * ld(l) 命令行中，则初始化为 1；如果库是可选的（即仅当
 * 一个或多个驱动程序需要它时才包含在内），则初始化为 0。
 * 库表的顺序决定了库在 ld(l) 命令行上的顺序
 * （即定义了隐式的加载顺序）。新
 * 库必须添加到该表中。
 * 注意：libhp-ux.a 必须是最后一项，请勿
 * 在其后放置任何内容。
 *
 * 库 <required>
 *
libvpar-pdk.a 0
 */
```

在这个文件中可以看到存在多个驱动程序。*vcn* 和 *vcs* 驱动程序用于支持 vPars 环境中的控制台。由于多个分区通常只有一个物理控制台，因此您需要一种方式来共享该物理设备。

以下是这两个驱动程序的说明：

-   *vcn*
    这是供 vPars 使用的虚拟控制台。由于系统中只存在一个物理控制台，*vcn* 被用作虚拟控制台。控制台信息由 *vcn* 发送到 **vpm on**，在那里进行缓冲。缓冲的信息被发送到 *vcs* 驱动程序（见下一项），在那里可以查看。
-   *vcs*
    这是虚拟控制台从驱动程序。该驱动程序是所有虚拟控制台的焦点。由 **vpm on** 存储的信息在建立连接时发送到 *vcs*。

图 4-1 展示了 *vcs*、*vcn* 和 **vpm on** 之间的关系。

![](img/eff8b9287a5f38c5adf538f24aacf29e_230_0.png)

图 4-1  使用 $vcn$ 和 $vcs$ 实现的虚拟控制台，第一个 vPar 正在运行

如果拥有物理控制台的分区没有运行，在图 4-1 中这是最左侧的分区，则 **vpm**on 模拟 $vcs$ 驱动程序并管理物理控制台。这确保了即使拥有它的 vPar 没有运行，物理控制台也可用。

我们还可以使用 SAM 来查看内核的各个方面，并为 vPars 修改内核。请记住，在不同的 vPars 中运行 SAM 就像在不同的系统上运行 SAM 一样。图 4-2 显示了 SAM 显示 vPar `cable1`（主机名为 `cvhdc0n4`，显示在所有 SAM 窗口的顶部）的驱动程序的画面：

![](img/eff8b9287a5f38c5adf538f24aacf29e_231_0.png)

注意图 4-2 左下角窗口中，`vcn`、`vcs` 和 `vpar_driver` 的 *Current State* 为 *In*，表明内核中存在这三个驱动程序。

第 11 章介绍了 SAM 和 vPars。就我们的内核讨论而言，足以说明我们在 vPars 命令行上执行的所有工作也可以在 SAM 中完成。

虽然我们不必手动构建内核以包含这些驱动程序，但我们也可以使用命令行上的 `mk_kernel` 来构建新内核，并使用 `kmpdate` 将新的内核相关文件放置到位，如下面的列表所示：

```
# mk_kernel
Generating module: krm...
Compiling /stand/build/conf.c...
Loading the kernel...
Generating kernel symbol table...
# kmpdate

Kernel update request is scheduled.

Default kernel /stand/vmunix will be updated by
newly built kernel /stand/build/vmunix test
at next system shutdown or startup time.
#
```

**kmpdate** 正在将许多新的内核相关文件放置到位，并保存旧文件的副本。虽然 **kmpdate** 为您节省了部分输入，但重要的是要知道它正在为您执行以下移动操作：

```
# mv /stand/vmunix /stand/vmunix.prev
# mv /stand/d1km /stand/d1km.prev
# mv /stand/build/vmunix_test /stand/vmunix
# mv /stand/build/d1km.vmunix_test /stand/d1km
```

请记住，当 vPars 软件被加载和配置时，此重建内核的过程是为您执行的。了解后台正在发生的事情很重要；然而，在您需要排查与更新后的内核相关的问题时尤其重要。内核创建和修改也可以在 SAM 中完成，如第 11 章所述。

由于使用 vPars 时系统中将有一个以上的内核需要维护，您希望熟悉此过程，以便可以为每个 vPar 定制内核，确保其针对在 vPar 中运行的应用程序进行了优化。

如果您在重建内核方面经验不多，可能需要回顾本章中描述重建内核的背景部分。

### 设备与虚拟分区

您可能正在将 HP 9000 上的各种设备从一个虚拟分区移动到另一个虚拟分区。这意味着相应虚拟分区中的内核需要包含将被该虚拟分区使用的硬件设备驱动程序。让我们看一下系统中的所有硬件，然后看看是否有我们希望从一个虚拟分区移动到另一个虚拟分区的组件。

首先，让我们通过以下示例中的 **ioscan -f** 来查看系统中的 *完整* 硬件：

```bash
cvhdcons:/ # ioscan -fm
```

```
class I/H/W Path Driver S/W State I/O-HWType Description

root 0 root CLAIMED BUS NEXUS System Bus Adapter
losa 0 0 sba CLAIMED BUS NEXUS Local PCI Bus Adapter (803)
chapter (782) 0 0/0 bta CLAIMED INTERFACE HP PCI 10/100Bs lan 0 0/0/0/0
se-TX Core 0 0/0/1/0 c720 CLAIMED INTERFACE /dev/land SCSI C896 Ultra
/dev/diag/land /dev/ether0
ext_bus 0 0/0/1/0 wide Single-ended tgot CLAIMED DEVICE
target 0 0/0/1/0.1 disk CLAIMED DEVICE HP DVD-ROM
ta4 sdisk CLAIMED
/dev/dsk/c0t1d0 /dev/dsk/c0t1d0
target 1 0/0/1/0.3 tgt CLAIMED DEVICE
tape 0 0/0/1/0.3.0 stape CLAIMED DEVICE HP C1337A
/dev/rmt/0m
/dev/rmt/0mB /dev/rmt/c0t3d0mBS7B
/dev/rmt/1m /dev/rmt/c0t3d0mB5B
/dev/rmt/1mB /dev/rmt/c0t3d0DDB
/dev/rmt/2m /dev/rmt/c0t3d0DSB
/dev/rmt/2mB /dev/rmt/c0l3d0mDSB
/dev/rmt/c0t3d0BEST /dev/rmt/c0l3d0DENSb

target 2 0/0/1/2 tgt CLAIMED DEVICE
ctl 0 0/0/1/0.7.0 sc11 CLAIMED DEVICE Initiator
/dev/rcse41/c0t7d0

ext_bus 1 0/0/1/2 wide Single-ended c720 CLAIMED INTERFACE SCSI C896 Ultra
target 3 0/0/1/1.0 tgt CLAIMED DEVICE
disk 1 0/0/1/1.0 edisk CLAIMED DEVICE SEAGATE ST17340
dlc /dev/dsk/c0t0d0 /dev/rdsk/c0t0d0
target 4 0/0/1/1 tgt CLAIMED DEVICE SEAGATE ST17340
disk 4 0/0/4/1 sdisk CLAIMED DEVICE

target 5 /dev/dsk /ctzdo /dev/rdsk /ctzdo
disk tgc CLAIMED DEVICE
xtl 1 sctl CLAIMED DEVICE Initiator
/dev/tacc/ct80
ext_bus 2 0/2/2/0 t720 CLAIMED INTERFACE SCSI C07K Ultra
Wide Single Ended
target 6 0/6/2/2. tgt CLAIMED DEVICE
disk 3 0/0/3/0 sdisk CLAIMED DEVICE SEAGATE ST17340
dlc /dev/dsk /ctd0d /dev/rdsk /ctzd0d

target 7 0/0/3/0 - tgt CLAIMED DEVICE
disk 4 0/0/2/8 edisk CLAIMED DEVICE SEAGATE ST17340
41L

target 8 0/0/2/0 /dev/dsk /ctzdo /dev/rdsk /ctzd0
tgt CLAIMED DEVICE
xtl 2 sctl CLAIMED DEVICE Initiator
/dev/rdsk /c17A0
ext_bus 3 0/0/3/0 t720 CLAIMED INTERFACE SCSI C07K Ultra
Wide Single Ended
target 9 0/9/2/1. tgt CLAIMED DEVICE
crl 3 0/0/2/1. sctl CLAIMED DEVICE Initiator
/dev/dsk /ct0o0
tty 0 0/0/4/0 asioO CLAIMED INTERFACE PCI Serial 1103
c1040 /dev/USBdiagI /dev/mxo /dev/ttygpI
tty 1 0/0/5/0 asioO CLAIMED INTERFACE PCI Serial 1103
/dev/USBdiagz /dev/muxl
c1048 /dev/USBmuxl /dev/ttygp2
ha 1 0/1 iba CLAIMED BUS_NEXUS Local PCI Bus Adapter (762)
target 2 0/2 iba CLAIMED BUS_NEXUS Local PCI Bus Adapter (782)
tha 3 0/3 iba CLAIMED BUS_NEXUS Local PCI Bus Adapter (782)
tha 4 0/4 iba CLAIMED BUS_NEXUS Local PCI Bus Adapter (782)
tha 5 0/5 iba CLAIMED BUS_NEXUS Local PCI Bus Adapter (782)
tha 6 0/8 iba CLAIMED BUS_NEXUS Local PCI Bus Adapter (782)

tc 0 0/8/0 0 Fibre Channel Mass Storage Adapter CLAIMED INTERFACE HP Tachyon TL/T
fzp 0 0/8/0/0.8 fcp CLAIMED INTERFACE FCP Protocol Adapter
arget 7 0/8/0.8.5.1.0.0 fcparray CLAIMED INTERFACE FCP Array Interface
target 10 0/8/0.8.5.0.1.0.0 tgt CLAIMED DEVICE
disk 7 0/8/0.8.5.0.0.1 sdisk CLAIMED DEVICE HP
A5277A /dev/dsk /ct0do /dev/rdsk /ct0do
target 10 0/8/0.8.0.5.0.5.0.1 sdisk CLAIMED DEVICE HP
/dev/dsk /ctodl /dev/rdsk /ctodl
disk 11 0/8/0.8.5.0.5.0.2 sdisk CLAIMED DEVICE HP
/dev/dsk /ctod2 /dev/rdsk /ctod2
disk 12 0/8/0.8.5.0.5.0.3 sdisk CLAIMED DEVICE HP
/dev/dsk /ctod3 /dev/rdsk /ctod3
arget 11 0/8/0.8.5.0.5.1 tgt CLAIMED DEVICE
disk 15 0/8/0.8.5.0.5.1.0.0 sdisk CLAIMED DEVICE HP
A5277A /dev/dsk /ctlio0 /dev/rdsk /ct1010
arget 12 0/8/0.8.5.0.5.2 tgt CLAIMED DEVICE
disk 17 0/8/0.8.5.0.5.2.0.0 sdisk CLAIMED DEVICE HP
A5277A
```




target 13 0/8/0/0.8.0.5.0.3 /dev/dsk/c0t240 /dev/rsk/c0t240
 disk 18 0/8/0/0.8.0.5.0.3 /dev/dsk/c1t240 /dev/rsk/c1t240
 AS277A 声称为 HP 设备
 ext_bus 4 0/8/0/0.8.0.255.0 fcpdev 声称为 FCP 设备接口
 target 14 0/8/0/0.8.0.255.0.5 tgt 声称为 HP 设备
 ctl 4 0/8/0/0.8.0.255.0.5 scl1 声称为 HP 设备
 AS277A
 ba 7 0/9 /dev/rscl/c4t5d0 /dev/rscl/c4t5d0
 dapter (782) 1 0/9/0 /ba BUSEXUS 本地 PCI 总线适配器
 fc 1 0/9/0/fcp 声称为 HP Tachyon TL/7
 S Fibre Channel Messe 存储适配器 /dev/tsl
 fcp 1 0/9/0.0.8 fcp 声称为 FCP 协议适配器
 声称为 HP 设备
 ext_bus 6 0/9/0/0.8.0.4.0 fcparray 声称为 FCP 阵列接口
 target 15 0/9/0/0.8.0.4.0.0 tgt 声称为 HP 设备
 disk 5 0/9/0/0.8.0.4.0.1 s1disk 声称为 HP 设备
 AS277A /dev/dsk/c5t040 /dev/rsk/c5t040
 disk 6 0/9/0/0.8.0.4.0.2 /dev/dsk/c6t040 /dev/rsk/c6t040
 AS277A 声称为 HP 设备
 disk 8 0/9/0/0.8.0.4.0.4.0 /dev/dsk/c8t040 /dev/rsk/c8t040
 AS277A 声称为 HP 设备
 disk 9 0/9/0/0.8.0.4.0.3 /dev/dsk/c9t040 /dev/rsk/c9t040
 AS277A 声称为 HP 设备
 target 16 0/9/0/0.8.0.4.0.1 /dev/dsk/c6t043 /dev/rsk/c6t043
 disk 13 0/9/0/0.8.0.4.0.1.0 /dev/dsk/c6t042 /dev/rsk/c6t042
 AS277A 声称为 HP 设备
 target 17 0/9/0/0.8.0.4.0.2 /dev/dsk/c6t1d0 /dev/rsk/c6t1d0
 disk 14 0/9/0/0.8.0.4.0.2.0 /dev/dsk/c6t1d1 /dev/rsk/c6t1d1
 AS277A 声称为 HP 设备
 target 18 0/9/0/0.8.0.4.0.3 /dev/dsk/c6t2d0 /dev/rsk/c6t2d0
 disk 16 0/9/0/0.8.0.4.0.3.0 s1disk 声称为 HP 设备
 AS277A
 ext_bus 5 0/9/0/0.8.0.255.0 fcpdev 声称为 FCP 设备接口
 target 19 0/9/0/0.8.0.255.0.4 tgt 声称为 HP 设备
 ctl 5 0/9/0/0.8.0.255.0.4 scl1 声称为 HP 设备
 AS277A
 ba 8 0/10 /ba /dev/rscl/c5t4d0 /dev/rscl/c5t4d0
 dapter (782) 1 0/10/0 /ba BUSEXUS 本地 PCI 总线适配器
 lan 1 0/10/0.1 blan 声称为 HP AS230A/B5509 BA PCI 7/100Base-TX 附加卡 /dev/diag/lan1 /dev/ether /dev/lan1
 ba 9 0/12 /ba BUSEXUS 本地 PCI 总线适配器
 dapter (782) 1 0/12 /ba BUSEXUS 本地 PCI 总线适配器
 lan 1 0/12/0 blan 声称为 HP AS230A/B5509 BA PCI 7/100Base-TX 附加卡 /dev/diag/lan2 /dev/ether /dev/lan2
 phc 0 32 phc 声称为 BUSEXUS 总线转换器
 processor 1 33 processor 声称为处理器 处理器
 phc 1 36 phc 声称为 BUSEXUS 总线转换器
 processor 1 37 processor 声称为 BUSEXUS 处理器
 phc 2 96 phc 声称为 BUSEXUS 处理器
 processor 2 97 processor 声称为处理器 处理器
 phc 3 100 phc 声称为 BUSEXUS 总线转换器
 processor 3 101 processor 声称为处理器 总线转换器
 memory 0 128 memory 声称为内存 内存
 virtbus 0 s00 声称为 VIRTBUS 增强型-8CS2 vf1vcons0/1

我使用了 *-f* 选项，因为它能生成所有 I/O 的完整列表。我省略了 *-u* 选项，该选项会生成可用 I/O 设备的列表。要使设备可用，内核中必须存在该设备的驱动程序以及一个实例号。我经常会在系统中发现内核中没有驱动程序的设。我喜欢了解这些设备，以便在不存在驱动程序时添加驱动程序并使用它们。

回到我们之前提到的 *ioscan -f* 示例，列表中有一个 DDS 驱动器。磁带驱动器被分配给 vPar *cable1* 但未分配给 *cable2*，如下面的列表所示：

```
# vparstatus -p cable1 -v

[Virtual Partition Details]
Name: cable1
State: Up
Attributes: Dynamic,Manual
Kernel Path: /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max: 2/3
Bound [Path]: 33
Unbound [Path]:

[IO Details]
0.0.1.1.2.0 BOOT
0.0.4.0 CONSOLE
0.0.5.0
0.0.1.0.3.0 <-- cable1 中的磁带驱动器

[Memory Details]
Specified [Base /Range]: (bytes) (MB)
Total Memory (MB): 2048
#
```

```
# vparstatus -p cable2 -v

[Virtual Partition Details]
Name: cable2
State: Up
Attributes: Dynamic,Manual
Kernel Path: /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max: 1/2
Bound [Path]: 97
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_236_0.png)

```
Unbound {Path}: 101

[IO Details]
    0.8.0.0.8.0.5.0.0.0 ROOT
    0.10.0.0                  <-- 无磁带驱动器

[Memory Details]
Specified [Base /Range]:
        (bytes)      (MB)
Total Memory (MB): 1024
#
```

*cable1* 的 *vmunix* 应该包含支持磁带驱动器所需的设备驱动程序，在本例中为 *stape*。我们可以通过执行以下所示的 *ioscan* 来知道 *stape* 是该驱动程序：

```
cvhdccon3:/ # ioscan -fun | grep tape
tape  0  0/0/1/0.3.0 stape   CLAIMED   DEVICE   HP C1537A
cvhdccon3:/ #
```

磁带驱动器的驱动程序应存在于将使用它的每个虚拟分区中。如果你的磁带驱动器接口位于你可以从一个 vPar 移动到另一个 vPar 的 PCI 插槽中，你希望将它的驱动程序放入将使用它的每个虚拟分区的内核中。请记住，为了移动磁带驱动器，其接口必须位于可以在一个 vPar 和另一个 vPar 之间移动的 LBA 上。在本文撰写时，LBA 不能在 vPars 之间共享。在我们的案例中，磁带驱动器连接到核心 I/O 卡，不会从 *cable1* 移动到 *cable2*。

/stand/system 的以下列表显示我们需要用于磁带的 *stape* 驱动程序存在：

```
cvhdccon3:/ # cat /stand/system
* Drivers and Subsystems

D1kmDrv
GSCLoPCI
PCItoPCI
arp
aslo0
asp
autofsc
autox0
bs_0am
btlan
btlan1
c720
cacheisc
cb
cuts
cifs
cione
core
cxperf
dev_config
dev_olart
devkrs
diag0
diag1
diag2
disc3
dikm
dipl
dmem
echo
esci
cdisk
fctl
fctl cntl
fctl fcp
fems
fcp
fcp cdeo
fcparray
fcpdev
fcpmux
fdc
di4
ffa
gelan
hpstreams
i2c cdeo
imeti
loem
iop drv
ip
kepd
kiog
kiro
kra
lasi
iba
ieterm
lv
lvm
maclan
netdiagl
netga
mfg_client
mfg_core
mfs_server
mfsim
mms
muls
clar_psm
cpar_psm_if
pa_generic_psm
pa_psm
pat_psm
pci
pckt
pflop
pipede
pipemod
prm
ptem
ptm
pts
rawip
rpcmod
sad
sagic
sba
sc
schgr
scsil
scsial
sctl
sdisk
sdm
sio
spr
spt0
ssrfc
stape
stcpmap
strlog
strtpty_included
strtelnet_included
target
top
td
telm
tels
timod
tirdwr
tlcits
tlcots
tlcotsod
token_arp
tun
udp
ufs
uipc
ven
vcs
ve_psm
ve_psm_driver
vfs
vxportal
ws10
```

# 设备和虚拟分区

-   -   内核设备信息
        ```
        dump lvol
        ```

-   -   可调参数

    ```
    STRMSGSZ              65535
    chlc_hash_locks       512
    maxdsiz_64bit         0x40000000
    maxssiz_              0x800000
    maxssiz_64bit         0x8000000
    maxswapChunks          2048
    maxtsiz               0x4000000
    maxtsiz_64bit         0x40000000
    nstrply               64
    shmmax                0x4000000
    cvhdcnc3:/ #
    ```

我们现在可以使用磁带驱动器来对 `cable` 进行备份。第 7 章中有关于备份的详细信息，包括使用远程磁带驱动器进行备份。以下示例显示了执行的 **fbbackup** 命令：

```
fbbackup -0u -f /dev/rmt/0m -g /tmp/backupgraph -I /tmp/backupindex.date '+%Y%m%d_%H:%M' 2> /tmp/backup.date '+%Y%m%d_%H:%M'
```

这将生成 `/var` 在 `cable` 上的备份的 *index* 文件，其中包含以下条目：

```
1024                  1 /
1024                  1 /var
1024                  1 /var/tmp/.fmd
200                   1 /var/tmp/aaaa01664
0                     1 /var/tmp/aaaa01745
0                     1 /var/tmp/aaaa01806
0                     1 /var/tmp/aaaa02391
0                     1 /var/tmp/cmd_res3036
0                     1 /var/tmp/cmd_res4403
1560                  1 /var/tmp/disk_em.fmt
324                   1 /var/tmp/dm_TL_adapter.fmt
1392                  1 /var/tmp/dm_stage.fmt
1241                  1 /var/tmp/ems_inittab.old
28                    1 /var/tmp/envd.action2
28                    1 /var/tmp/envd.action5
200                   1 /var/tmp/fc0mon.fmt
4106                  1 /var/tmp/inetd.conf.old
0       1 /var/tmp/lpmc_em.fmt
96      1 /var/tmp/ntp
0       1 /var/tmp/oe.config.4525
0       1 /var/tmp/rdskACAAo1881
0       1 /var/tmp/rdskQBAa01841
0       1 /var/tmp/rdskSDCa06262
0       1 /var/tmp/rdskSJJa01574
0       1 /var/tmp/rdskUBAa01853
7184    1 /var/tmp/sawagent.log
```

如果磁带接口不在分配给 *cable* 1 的核心 I/O 卡上，我们可以将接口从 *cable* 1 移动到 *cable* 2，确认驱动程序在 **/stand/system** 中，然后备份 *cable* 2。

由于你可能想要在系统上运行的 vPars 之间移动许多设备，因此你需要确保内核中拥有支持这些设备所需的所有设备驱动程序。




## 非 vPar 专用章节 - 修改和构建 HP-UX 内核

你可能需要以某种方式修改 HP-UX 11i 内核，例如更改内核参数，然后重新构建内核。你可能需要创建新的 HP-UX 内核，以便添加设备驱动程序或子系统，调整内核以获得更好的性能，更改可配置参数，或更改转储和交换设备。如果你更新或修改了内核的动态元素，如本章示例中所示，则不需要重启。更新或修改静态元素需要重启，可能还需要执行一些额外步骤。

在 HP-UX 11i 中，对于发生在内核上的所有更改，并不总是需要重新构建内核。在 11i 中，有许多*动态可调内核参数*和*动态可加载内核模块*可以修改你的内核，而不需要重启。结合 11i 中可用的许多*动态补丁*，你将更少频繁地重启系统。

在下一节中，我们将修改一个*动态可调内核参数*，从而修改内核，且无需重启系统即可使更改生效。然后，我们将对内核进行更改并完全重新构建它，以便你可以看到完整重建的过程，包括重启。我通常使用第 11 章介绍的*系统管理管理器 (SAM)* 来进行内核修改。然而，理解手动构建 HP-UX 内核的过程是无法替代的，因此当你以后让 SAM 为你执行此操作时，你会更加知情。在本章中，我们讨论与内核生成相关的各种命令，并介绍手动创建内核的过程。

### 动态可加载内核模块

11.0 版本引入了动态可加载内核模块。在 11.x 中，该功能的基础架构已就位，为每个模块提供了独立的系统文件。11.0 版本提供了将特别创建的模块加载或卸载到内核中的功能，只要该模块未被使用，就无需重启系统。HP-UX 11i 继续支持所有这些动态功能。这种新机制提供了极大的灵活性和更好的系统正常运行时间。关于此高级功能的详细信息可以在 HP-UX 11.x 版本说明中查阅。在本文撰写时，大多数可用的动态可加载内核模块都是第三方的。IT 资源中心网站 (itrc.hp.com) 包含有关此主题的信息，包括开发者指南。

# 构建内核

首先，让我们看看在本书许多示例中使用的 HP-UX 11i L-Class 系统上运行的现有内核。`sysdef` 命令用于分析和报告当前运行系统的可调参数。如果不希望使用当前运行的系统，你可以指定要分析的文件。以下是在 11i L-Class 系统上运行 `sysdef` 的*部分*列表：

```bash
$ /usr/sbin/sysdef
NAME              VALUE     BOOT  MIN-MAX   UNITS     FLAGS
acctresum         4         -     -105-100  -         -
acctasuspend      2         -     -100-100  -         -
allocate_fswswmap 0         -     -         -         -
buffers           32074     -     -         0-        Pages   -
create_fastlinks  0         -     -         -         -
dbc_max_pct       50        -     -         -         -
dbc_min_pct       5         -     -         -         -
default_disk_lr  0         -     -         -         -
dakless_mode      0         -     -         0-1       -         -
epsa_io_estimate  768       -     -         -         -         -
egmremize         23        -     -         -         -         -
file_pad          0         -     -         0-        -         -
fs_fsync          0         -     -         0-        -         -
hpxps_ess_override 0        -     -         0-1       -         -
maxdlis           3         -     -         0-1       -         -
maxdlis_64bit     16384     -     -         0-65536   Pages     -
maxfiles          60        -     -         30-2048   -         -
maxfiles_lim      1024      -     -         30-2048   -         -
maxmsg            65536     -     -         0-65536   Pages     -
maxmsg_64bit      262144    -     -         256-1048576 Pages    -
maxswapChunks     512       -     -         1-16384   -         -
maxtsiz           2048      -     -         0-65536   Pages     -
maxtsiz_64bit     2048      -     -         256-1048576 Pages    -
maxxpsrc          75        -     -         3-        -         -
msgmap            10        -     -         -         -         -
nbuf              18720     -     -         0-        -         -
ncallout          512       -     -         6-        -         -
ncnodse           150       -     -         -         -         -
ndlbuffers        30        -     -         -         -         -
netiss_priority   1         -     -         -1-127    -         -
netnemax          0         -     -         -         -         -
file              920       -     -         14-       -         -
nfile             0         -     -         2-        -         -
ninode
no_lvm_disks
nproc
npty
ndratpty
ndevapdev
nwaapsf
public_shlibs
rmcore_str_swap
rtcched_numpti
selmnt
semmap
shmmax
shmmin
shmmin
streampipe
swapwarn_on
tg64
timeslice
unlinkable_mem
```

除了可调参数外，你可能还想查看系统中发现的所有硬件的报告。`ioscan` 命令可以为你完成此操作。使用 `sysdef` 和 `ioscan`，你可以查看可调参数的设置以及系统中存在的硬件。这样你就知道系统是如何设置的，然后可以更改你的内核。以下是与运行 `sysdef` 相同的 HP-UX 11i L-Class 系统的 `ioscan` 输出：

```bash
# /usr/sbin/ioscan -f

Class I H/W Path   Driver  S/W State  H/W Type     Description

root      0         --      CLAIMED    BUS_NEXUS
lca       0  c       --      CLAIMED    BUS_NEXUS    System Bus Adapter (582)
ba        0 0/0/0/0  i40x    CLAIMED    BUS_NEXUS    Local PCI Bus Adapter (782)
lan       0 0/0/0/0  tk     CLAIMED    INTERFACE    HP PCI 10/100Base-TX Core
ext_bus   0 0/0/1/0  msa    CLAIMED    INTERFACE    SCSI C896 Fast Wide LVD
target    0 0/0/1/0/7  tgt  CLAIMED    DEVICE       Initiator
ctrl      0 0/0/1/0/7.7    ascl  CLAIMED    DEVICE       Initiator
ext_bus   1 0/0/1/1  c720  CLAIMED    INTERFACE    SCSI C896 Ultra Wide Single-Ended
target    1 0/0/1/1.1  tgt  CLAIMED    DEVICE
disk      1 0/0/1/1.4.0  aisk  CLAIMED    DEVICE       SEAGATE ST312203LC
target    2 0/0/1/1.7  tgt  CLAIMED    DEVICE
crl       1 0/0/1/1.7.7  ac11  CLAIMED    DEVICE       Initiator
ext_bus   2 0/0/2/1  c720  CLAIMED    INTERFACE    SCSI C875 Ultra Wide Single-Ended
target    3 0/0/2/0.2  tgt  CLAIMED    DEVICE
disk      3 0/0/2/0.2.2  cdsk  CLAIMED    DEVICE       SEAGATE ST318203LC
target    4 0/0/2/0.7  tgt  CLAIMED    DEVICE
crl       2 0/0/2/0.7.0  ac11  CLAIMED    DEVICE       Initiator
ext_bus   3 0/0/2/1  c720  CLAIMED    INTERFACE    SCSI C875 Ultra Wide Single-Ended
target    5 0/0/2/1.4  tgt  CLAIMED    DEVICE
disk      5 0/0/2/1.4.0  adisk  CLAIMED    DEVICE       TOSHIBA CD-ROM XM-6201TA
target    6 0/0/1.7  tgt  CLAIMED    DEVICE
ctrl      3 0/0/1.7.0  ac11  CLAIMED    DEVICE       Initiator
```

```bash
tty        1  0/0/5/0     agio0        CLAIMED      INTERFACE      PCI Serial (103c1048)
ba         2  1/1         1ba          CLAIMED      BUS NEXUS      Local PCI Bus Adapter (782)
ba         2  2/2         1ba          CLAIMED      BUS NEXUS      Local PCI Bus Adapter (782)
ba         3  0/3         1ba          CLAIMED      BUS NEXUS      Local PCI Bus Adapter (782)
ian        1  0/3/3/0     bclan        CLAIMED      INTERFACE      HP ASIO/A65580B PCI 10/100Base-TX Adaptor
ba         4  0/4         1ba          CLAIMED      BUS NEXUS      Local PCI Bus Adapter (782)
ext_bus    4  0/4/0/0     c720         CLAIMED      INTERFACE      SCSI Fast Wide Differential
target     7  0/4/0/0.7   tgt          CLAIMED      DEVICE
ctl        7  0/4/0/0.7   sctl         CLAIMED      DEVICE         Initiator
ext_bus    5  0/4/0/1     c720         CLAIMED      INTERFACE      SCSI CB75 Fast Wide differential
target     8  0/4/0/1.7   tgt          CLAIMED      DEVICE
ctl        5  0/4/0/1.7   sctl         CLAIMED      DEVICE         Initiator
ba         5  0/5         1ba          CLAIMED      BUS NEXUS      Local PCI Bus Adapter (782)
ba         6  0/6         1ba          CLAIMED      BUS NEXUS      Local PCI Bus Adapter (782)
ba         7  0/7         1ba          CLAIMED      BUS NEXUS      Local PCI Bus Adapter (782)
ext_bus    6  0/7/0/1     c720         CLAIMED      INTERFACE      SCSI CB75 Fast Wide Differential
target     9  0/7/0/0.7   tgt  CLAIMED      DEVICE
ctl        6  0/7/0/0.7   sctl         CLAIMED      DEVICE         Initiator
ext_bus    7  0/7/0/1     c720         CLAIMED      INTERFACE      SCSI CB75 Fast Wide Differential
target    10  0/7/0/1    tgt          CLAIMED      DEVICE
ctl        7  0/7/0/1.7   sctl         CLAIMED      DEVICE         Initiator
memory       0  8          memory       CLAIMED      MEMORY         Memory
processor    0  160       processor    CLAIMED      PROCESSOR      Processor
processor    1  166       processor    CLAIMED      PROCESSOR      Processor
```

我通常运行带有 `-f` 选项的 `ioscan`，因为它包含*Driver*（驱动程序）、*S/W State*（软件状态）和*H/W Type*（硬件类型）列。我感兴趣的是 `-f` 选项生成的与系统中硬件关联的驱动程序。

`ioscan` 输出显示了构成系统的所有硬件，包括系统中的两个处理器。

文件 `/stand/vmunix` 是当前正在运行的内核。以下是 L-Class 系统上 `/stand` 目录的长列表，显示了文件 `/stand/vmunix`：

```bash
# ls -l
total 74274
drwxr-xr-x   4 root     sys      2048 Aug 25 11:24 ddtk
lrwxr-xr-x   5 root     sys      1024 Aug 29 14:25 ddsm.vmunix.prev
-rw-r-----   1 root     sys      3024 Aug 4 12:26 iocconf
-r----r----   1 root     sys       82 Aug 4 12:27 kernel
drwxr-xr-x   2 root     root     1024 Aug 29 11:33 krs
drwxr-xr-x   2 root     root     1024 Aug 29 11:33 krs.lkg
drwxr-xr-x   2 root     root     1024 Aug 29 11:39 krs.tmp
drwxr-xr-x   2 root     root     8192 Aug 4 11:36 lost+found
-rw-------   1 root     root       12 Aug 29 11:33 rootconf
lrwxr-xr-x   1 root     sys      1180 Aug 24 12:52 system
drwxr-xr-x   2 root     root     1026 Aug 4 12:21 system.prev
drwxr-xr-x   1 root     sys     14774416 Aug 24 12:53 vmunix
```




-rwxr-xr-x 1 root sys 23184584 Aug 4 12:22 vmlinux.prev
#

请注意，在显示的目录中，有两个与动态可加载内核模块（DLKM）相关的目录。这些内核模块可以在不重启系统的情况下包含在内核中。

为了对内核进行修改，我们需要进入 `/stand/build` 目录，在此目录下执行创建新内核的所有工作，并按照下文所示发出 `system_prep` 命令：

```
# cd /stand/build
# /usr/lib/sysadm/system_prep -s system
```

现在我们可以继续对内核进行所需的更改，包括添加如 cdfs（CD-ROM 文件系统）之类的驱动程序或子系统。随着 1.1i 版本中动态可加载内核模块（DLM）结构的就位，我们必须使用 `knsystem` 和 `knptune` 来修改内核系统文件和系统描述文件。

您可以使用 `knmute` 来查看现有内核参数相关的值和参数，并提出对内核的修改建议。以下列表显示了发出 `knmute`（不带有 `-i` 选项以查看详细信息）以查看当前正在运行的内核摘要：

```
# knmute
```

| 参数 | 当前值 | 动态计划值 | 模块 | 版本 |
|:---|:---|:---|:---|:---|
| NTRLBLKSIGNED | 2 | - | - | - |
| NSTREVENT | 50 | - | 50 | |
| NSTREPGNH | 16 | - | 16 | |
| NSTRCHRGH | 0 | - | 0 | |
| STRCTLRSZ | 1024 | - | 1024 | |
| STRMSGSZ | 65535 | - | 65535 | |
| acct_resume | 4 | - | 4 | |
| acct_suspends | 2 | - | 2 | |
| aio_listio_max | 256 | - | 256 | |
| aio_max_od | 2048 | - | 2048 | |
| aio_physmem_pct | 10 | - | 10 | |
| aio_prio_delta_max | 20 | - | 20 | |
| allocate_fs_swamap | 0 | - | 0 | |
| alwaysdump | 1 | - | 1 | |
| bootapplink | de | - | 256 | |
| bufcache_hash_locks | 128 | - | 128 | |
| bufpages | 0 | - | 0 | |
| chang_hash_locks | 256 | - | 256 | |
| create_fastlinks | 0 | - | 0 | |
| dpc_max_pct | 50 | - | 50 | |
| dpc_min_pct | 5 | - | 5 | |
| default_disk_ir | 0 | - | 0 | |
| destime | - | - | 0 | |
| diskabort_seconds | 0 | - | 0 | |
| dnalt_hash_locks | 512 | - | 512 | |
| dontdump | 0 | - | 0 | |
| dxleaze_node | 0 | - | 0 | |
| dst | 1 | - | 1 | |
| effective_maxpjd | - | - | (NRPROC4=22500) ?330000 : (NRPROC4*5) +1) | |
| eisa_to_estimate | - | - | 0x300 | |
| enable_1dde | 0 | - | 0 | |
| eqonemize | 15 | - | 15 | |
| executable_staxce | 1 | - | 1 | |
| fcp_large_config | 0 | - | 0 | |
| file_pad | - | - | 10 | |
| fs_asyncr | 0 | - | 0 | |
| ftable_hash_locks | 64 | - | 64 | |
| hdpuw_hash_locks | 128 | - | 128 | |
| hfs_max_ra_blocks | 8 | - | 8 | |
| hfs_max_reva_blocks | 8 | - | 8 | |
| hfs_ra_per_disk | 64 | - | 64 | |
| hfs_reva_per_disk | 64 | - | 64 | |
| hp_nfa_mira_enabled | 1 | - | 1 | |
| hpxa_aes_override | - | - | 0 | |
| intcmdmax | 90 | - | 50 | |
| io_porta_hash_locks | 64 | - | 64 | |
| iomemsize | - | - | 40000 | |
| ksl_alloc_max | 2208 | - | 2268 | |
| ksl_memd_max | 32 | - | 32 | |
| lockfree | - | - | 0 | |
| max_syswc_ports | 50 | - | 50 | |
| max_fcp_regs | 512 | - | 512 | |
| max_mem_window | 0 | - | 0 | |
| max_thread_proc | 64 | - | 64 | |
| maxszds | 0x10000000 | - | 0x10000000 | |
| maxszds_64bit | 0x04000000 | - | 0x04000000 | |
| maxfiles | 60 | - | 60 | |
| maxfiles_lim | 1024 | Y | 1024 | |
| maxqueueTime | - | - | 0 | |
| maxsiz | 0x800000 | - | 0x800000 | |
| maxsiz_64bit | 0x800000 | - | 0x800000 | |
| maxswapChunks | 512 | - | 512 | |
| maxswiz | 0x40000000 | Y | 0x4000000 | |
| maxsiz_64bit | 0x40000000 | - | 0x40000000 | |
| maxqsw | 77 Y | - | 77 | |
| maxusr | 32 | - | 32 | |
| maxvg | 10 | - | 10 | |
| memrg | 1 | - | 1 | |
| minfree | - | - | 0 | |
| modstramx | 500 | - | 500 | |
| msqmap | 42 | - | 42 | |
| msqmax | 8192 Y | - | 8192 | |
| msqmin | 16384 | Y | 16384 | |
| msqmin1 | 50 | - | 50 | |
| msqseq | 2048 | - | 2048 | |
| msqsiz | 8 | - | 8 | |
| msgtql | 40 | - | 40 | |
| nbuf | 0 | - | 0 | |
| nr-ij.art | - | - | - | |
| numnode | 150 | - | 150 | |
| nclust | 63 | - | 63 | |
| ncsize | 5596 | - | 5596 | |
| ndbl buffers | - | - | - | |
| netlar_priority | 30 | - | 30 | |
| - | - | - | 1 | |
| netmemmax | - | - | - | |
| nfile | 910 | - | 910 | |
| nlocka | 200 | - | 200 | |
| nobl_scale | 0 | - | 0 | |
| niodn | 476 | - | 476 | |
| nthread | 499 | - | 499 | |
| nl | - | - | 2 | |
| no_lvm_disks | 0 | - | 0 | |

nproc 400 500
npty 60 60
netpty 60 60
netctl 60 60
nmapdev 10 10
nswapfs 10 10
nyswap 800 800
neymap64 800 800
num_tachyon_adapters 0 0
o_sync_is_o_dsync 0 0
page_razt_to_local - -
pfint_hash_locks 128 128
public_shilks 1 1
region_hash_locks 128 128
remote_nfs_swap 0 0
rtached_numpr 32 32
scroll_lines 100 100
srai_maxphys 1048576 1048576
seema - 1
semsem 16384 16384
semmap 66 66
semmsm 64 64
semmsa 128 128
semmni 30 30
semnum 10 10
semvmx 32767 32767
sendfile_max 0 0
shmes 1 1
shmmax 0x40000000 0x50000000
shmni 200 200
shmseg 120 120
st_atm_enabled 1 1
st_fail_overruns 0 0
st_large_recs 0 0
streampipes 0 0
swapmem_on 1 1
swchunk 2048 2048
sysv_hash_locks 128 128
tophasher 0 0
timeslice 10 10
timzone 420 420
unlockable_mem 0 0
vas_hash_locks 128 128
vnodc_od_hash_locks 128 128
vnodc_hash_locks 128 128
vpcs_ceiling 16 16
vpcs_char_ceiling 1048576 1048576
vpcs_pagesize 4 4
vx_fancyra_enable 0 -
vv_maxlink 32767 32767
vv_ncsize 1024 1024
vzfs_max_ra_kbytes 1024 1024
vzfs_ra_per_disk 1024 1024
#

发出带有 *-l* 选项的 **kmtune** 会生成内核的详细列表。以下仅显示其中一个参数的输出：

```
# kmtune -l
Parameter: maxuprc
Current: 77
Planned: 77
Default: 75
Minimum: -
```

```
Module: - 
Version: -- 
Dynamic: Yes 
#
```

该参数是动态的（Yes），这意味着内核可以被动态更新。在查看完此输出后，我们现在可以修改此动态参数的值。以下命令将以下参数的值从 77（现有值）更改为 80：

```
# kmtune -s maxuprc=80
#
```

我们现在可以再次发出 kmtune 以查看 maxuprc 参数的现有值和提议值：

```
# kmtune
Parameter Current Dym Planned Module Version
------------------------------- ------------------------------
NETBLKSZCMD - 7 
NSSTEVENT 50 - 50 
NETRPUSH 16 - 16 
NETRETCHECK 0 - 0 
STRCLSZ 1024 - 1024 
STRMGSZS 65535 - 65535 
acctresume 4 - 4 
Acctrespend 2 - 2 
aio_fisixio_max 256 - 256 
aio_max_cps 2048 - 2048 
aio_sysmax_pct 10 - 10 
aio_pri_delta_max 20 - 20 
allocate_fs_swapmap 0 - 0 
alwaysdump 1 - 1 
bootspinlocks - - 256 
bufferino_hash_nmax 424 - 424 
bufpages 0 - 0 
chang_hash_locks 256 - 256 
creatc_fastlinks 0 - 0 
dbc_max_pgt 50 - 50 
dbc_min_pgt 5 - 5 
default_disk_ir 0 - 0 
dstcache 0 - 0 
diskroot_seconds 0 - 0 
dnclc_hash_locks 512 - 512 
dontdump - 0 
datless_node - 0 
dat - 1 - 1 
effective_maxpid - - (NPROC-32500):30000: (NPROC*$4)}
else_io_estimate - 0x300 
enable_fdda 0 - 0 
execmemsize 15 - 15 
executable_stack 1 - 1 
frq_table_config 0 - 0
```

## 第 X 章非 vPar 特定部分 - 修改和构建 HP-UX 内核

217

file_pad - - 10
fa_synqc 0 - 0
fstable_hash_locks 64 - 64
htcpvcap_basql_locks 128 - 128
htf_qmax_ra_blocks 8 - 8
htfq_rexra_per_blocks 8 - 8
htfq_ra_per_disk 64 - 64
htf_s_rexra_per_disk 64 - 64
htp_fiq_extra_enabled 1 - 1
fpxiq_wess_override - - 0
inintmodax 50 - 50
iq_postiq_hash_loqke 64 - 64
iomemsize - 40000
kai_wiioc_max 2208 - 2208
kel_wend_max 32 - 32
iobjree - - 0
max_aqqyic_popts 50 - 50
max_frp_regs 512 - 512
max_wino_windqw 0 - 0
max_wirod_proo 64 - 64
maxd81z 0x10000000 - 0x10000000
maxd611_64b1t 0x40000000 0x80000000
maxdled 60 - 60
maxfielq_lim 1024 Y 1200
maqxeuentime - - 0
maxsize1 0x800000 - 0x800000
maxsiziz_64bit 0x800000 - 0x800000
maxswapchunka 512 - 512
maxs11z 0x40000000 Y 0x40000000
maxs11z_64b1t 0x40000000 Y 0x40000000
maxproc 77 Y 89
maxusere 32 - 32
maxveps 10 - 10
meag - - 1
mtree - - 0
modlistmax 500 - 500
mqmap 42 - 42
mqmax 8192 Y 8192
mqminb 16384 Y 16384
mqqmi1 50 - 50
mqsseg 2048 - 2048
mqssez 8 - 8
mqtol 40 - 40
nbuf 0 - 0
nclaiout 515 - 515
ncioster 150 - 150
ncliet 612 - 612
nclize 5596 - 5596
ndltbuffers 30 - 39
netier_priority - - 1
netmemmax - - 0
nf11e 910 - 910
nflooxes 200 - 200
nihull_scale 8 - 8
ninode 476 - 476
nikhread 499 - 499
nn1 - - 2
no_lvm_diske 0 - 0
nproc 400 - 400
nproc 60 - 60
netrip1y 60 - 60
nstarcel 60 - 60
nswqpaoy 10 - 10
nswqpe 10 - 10
nswapap 800 - 800
nqy8mspe4 800 - 800
num_tqctiqm_adqptere 0 - 0
o_synq_1a_o_faync 0 - 0
page_text_to_local - - 128
pifat_hash_locks 128 - 128
public_shills 1 - 1
region_hash_locks 128 - 128
resene_nrq_swap 0 - 0
rteeched_numpri 32 - 32
screol1_lines 100 - 100




### 系统参数调整与内核构建

seml_maxphys      1048576 - 1048576
sema                1     -     1
semsm               16384 - 16384
semmap               66  - 66
semmsi               64  - 64
semmns             128  - 128
semmnu               30  - 30
ssmnume             10  - 10
semmnx            32767 - 32767
swpdta_cebx          0   - 0
swpm               1     - 1
swmax       0x40000000 Y 0x40000000
shmmin               200  - 200
shmmeg               120  - 120
st.ats_enabled          1     -     1
st_fail_overrun       0     -     0
st_large_recv         0     -     0
strmipes                0   - 0
swpsm_on                1   - 1
swchnk               2048 - 2048
syv_hash_locks         128  - 128
trplshaz                0   - 0
timeslice             10  - 10
timeszone             420 - 420
unlckbale_mwm         0     -     0
vas_hash_locks        128 - 128
wxde_wd_hash_locks     128  - 128
xnwde_hash_locks       128  - 128
vps_celing              16  - 16
vps_cbar_celing     1048576 - 1048576
vps_pgazer               4    - 4
vv_fancyra_enable        0    - 0
wx_maxlwk             32767 - 32767
wx_ncxize              1024  - 1024
wods_max_ra_kbytes     1024  - 1024
wxfa_ra_per_disk       1024  - 1024

上述输出表明，我们对参数的更改处于待处理状态。

我们可以通过使用带有 `-u` 选项的 `kmtune` 来应用对动态参数 *maxuprc* 的更改，将其从 77 更新为 80：

```shell
# kmtune -u
The kernel's value of maxuprc has been set to 80 (0x50) .
```

此输出表明，我们希望对内核所做的更改已经完成。我们可以通过再次运行 `kmtune` 并搜索 *maxuprc* 来确认这一点：

```shell
# kmtune | grep maxuprc
maxuprc             80 Y 80
```

*Current* 和 *Planned* 值都已更新为 80。这种动态更新可以使用 **kmsystem** 向内核添加动态驱动程序来完成。

还有许多其他过程，你需要执行额外的步骤才能将这些修改包含在内核中并重新构建它。对于这些非动态更改，你需要创建一个新的内核，该内核将生成为 **/stand/build/vmunix_test**，使用以下所示的命令：

```shell
# mk_kernel -s system
Compiling conf.c...
Loading the kernel...
Generating kernel symbol table...
```

此时，新内核位于 /stand/build 目录中。现有内核将使用 **kmupdate** 与新生成的内核一起更新。**kmupdate** 将新的内核文件移动到 /stand 目录。我建议首先将现有的 /stand/system 内核文件移动到一个备份文件，然后更新新内核，如下所示：

```shell
# mv /stand/system /stand/system.prev (可能想要移动图 4-3 中显示的其他文件)
# kmupdate /stand/build/vmunix_test
Kernel update request is scheduled.

Default kernel /stand/vmunix will be updated by newly built kernel /stand/build/vmunix_test at next system shutdown or startup time.
```

**kmupdate** 会自动为你创建 /stand/vmunix 和 /stand/dlkm 的备份副本。这些将分别创建为 **/stand/vmunix.prev** 和 /stand/dlkm.vmunix.prev。

现在你可以关闭系统，如果更新未能动态完成且需要重启，系统将自动从新内核启动。

图 4-3 总结了在 HP-UX 11i 中构建新内核的过程。

| 步骤 | 注释 |
|---|---|
| 1) 运行 `sysdef` 和 `ioscan -f` | 分析并报告当前运行内核的可调参数。 |
| 2) 对 /stand 目录执行长列表 | 文件 `vmunix` 是现有内核，而 `system` 用于构建新内核。 |
| 3) `cd /stand/build` | 这是将构建新内核的目录。 |
| 4) `/usr/bin/sysadm` `system_prep -s system` | 此操作检查当前运行的内核。 |
| 5) 使用 `kmsystem` 和 `kmtune` 进行更改 | 在 `/stand/build` 目录中执行更改。动态更新在此处完成。 |
| 6) `mk_kernel -s system` | 在 `/stand/build` 目录中创建一个新内核，称为 `vmunix_test`。DLKM 文件在 `dlkm_vmunix_test` 中生成。 |
| 7) `mv /stand/system /stand/system.prev`<br>`mv /stand/vmunix /stand/vmunix.prev`<br>`mv /stand/dlkm /stand/dlkmvmunix.prev` | 将现有文件保存为 `.prev`。 |
| 8) `mv /stand/build/system /stand/system`<br>`kmupdate /stand/build/vmunix_test` | 重命名内核和新生成的内核。自动将旧版本保存在 `/stand` 中，如下所示：<br>`vmunix 作为 /stand/vmunix.prev`<br>`dlkm 作为 dlkmvmunix.prev` |
| 9) `cd /`<br>`shutdown -r 0` | 将目录更改为 `/` 并关闭系统，以便系统使用新内核启动。如果您的更改可以动态实施，则可能不需要此步骤。 |

图 4-3 在 HP-UX 11i 中创建内核

实际上存在两种不同的生成内核的过程——一种是针对动态元素，例如前面示例中所示的参数 *maxuprc*；另一种是针对静态元素。静态过程由几个额外的步骤和一次重启组成。在 HP-UX 11i 中，越来越多的内核对象将动态更新，从而减少修改内核时的重启次数。

### 内核参数描述

以下是撰写本文时 HP-UX 11i 中内核参数的描述。第一部分是每个内核参数的列表和描述。第二部分是内核参数的概览。完整且最新的描述可以在以下 URL 中找到：

http://docs.hp.com/hpux/olinedocs/os/KCparams.Overview.All.html

我鼓励你使用 SAM 的在线帮助和上述 URL 来获取有关内核参数的最新和完整信息。由于篇幅限制，我删除了与内核参数相关的许多背景信息，以节省空间。这些信息在撰写本文时可在 SAM 在线帮助和该 URL 中获得。

我对这些资料进行了最少的格式化。它接近我从实验室的 HP 同事那里收到的原始形式。我认为在这种略显“原始”的形式下效果最佳，毕竟，我们在处理的是与内核相关的信息。

### 内核参数

**aio_listio_max** 指定可以在“listio()”调用中指定的 POSIX 异步 I/O 操作的最大数量。

可接受的值：
- 最小值 2
- 最大值 0x10000
- 默认值 256

此参数对系统资源设置了限制，以防大量 POSIX 异步 I/O 操作在单个“listio()”调用中被请求时消耗系统资源。该值应设置得足够大，以满足系统编程需求，同时保护系统免受故障进程发起的过度异步 I/O 操作的影响。

指定的值不得超过 `aio_max_ops` 的值。

**aio_max_ops** 指定在任一给定时间可以同时排队的 POSIX 异步 I/O 操作的全系统最大数量。

可接受的值：
- 最小值 1
- 最大值 0x100000
- 默认值 2048

指定整数值。

#### 描述

此参数对系统资源设置了限制，以防大量 POSIX 异步 I/O 操作同时排队时消耗系统资源。此参数限制了竞争进程通过大量异步 I/O 操作及其所需的内存压倒系统的能力。

每个排队的异步操作都需要分配系统内存用于其内部控制结构，因此必须设置此限制。除了全系统限制外，还有一个由“getrlimit()”和“setrlimit()”调用的参数 "RLIMIT_AIO_OPS" 控制的每进程限制。

**aio_physmem_pct** 指定系统总物理内存中可用于 POSIX 异步 I/O 操作的锁定内存的最大百分比。

可接受的值：
- 最小值 5
- 最大值 50
- 默认值 10

指定整数值。

#### 描述


此参数对任何给定时刻正在进行的 POSIX 异步 I/O 操作的总数可以锁定的系统内存量施加限制。 还要意识到的是，即使操作已完成，只要未通过该操作的 “aio_return()” 调用正确终止，该操作就会保留在活动队列上，内存也不会释放。

使用请求和回调机制进行 I/O 的异步 I/O 操作必须能够锁定其正在使用的内存。 仅当涉及的设备驱动程序支持该机制时，才使用请求和回调机制。 仅在 I/O 传输正在进行期间锁定内存。 在大型服务器上，最好将 “aio_physmem_pct” 增加到更高的值（最高 50）。

“aio_physmem_pct” 对可锁定的物理内存施加系统范围的限制。 通过使用应用程序内的 “setrlimit()” 系统调用，也可以自我施加每进程的可锁定内存限制。

请记住，任何给定时刻因任何原因（而不仅是异步 I/O）可以锁定的内存总量都由系统范围的 “lockable_mem” 限制控制。 其他系统活动，包括使用 mlock() 和/或 mlock() 接口进行显式内存锁定，也可能影响任何给定时刻的可锁定内存量。

没有名为 “lockable_mem” 的内核参数，但有一个名为 “unlockable_mem” 的参数会影响它。 “lockable_mem” 的值是通过从系统启动后可用的系统内存中减去 “unlockable_mem” 的值来确定的。 在启动期间，系统会在系统控制台上显示其可锁定内存的数量（连同可用内存和物理内存一起）。 系统运行时，可以使用 “/sbin/memsg” 命令检索这些值。

aio_prio_delta_max 指定 POSIX 异步 I/O 操作的最大减速因子（优先级偏移量）。 这是异步 I/O 控制块（“aiocb” 结构）中 “aio_reqprio” 字段允许的最大优先级偏移值。

可接受的值：
- 最小值 0
- 最大值 20
- 默认值 20

指定整数值

描述

此参数对 POSIX 异步 I/O 操作的优先级可以降低多少以减速或停止施加限制。 这限制了异步 I/O 控制块结构 `"aiocb"` 中允许用于 `"int aio_reqprio"` 的值。

# acctresume

当足够的文件系统可用空间可用时恢复记账。

可接受的值：
- 最小值 -100
- 最大值 101
- 默认值 4

指定整数值。

描述

仅当系统中使用进程记账时，此参数才值得关注。

`"acctresume"` 指定在系统因可用空间不足而挂起进程记账时，文件系统必须可用的最小可用空间量，以便系统可以恢复进程记账。 挂起记账的阈值由 `"acctsuspend"` 定义。

相关参数

`"acctsuspend"` 和 `"acctresume"` 是相互关联的。 为防止挂起-恢复冲突，`"acctresume"` 的带符号整数值必须始终大于 `"acctsuspend"` 的带符号整数值。

# acctsuspend

当可用的文件系统空间降至指定量以下时挂起记账。

可接受的值：
- 最小值 -100
- 最大值 100
- 默认值 2

指定整数值。

描述

仅当系统中使用进程记账时，此参数才值得关注。

“acctsuspend” 通过指定进程记账运行时必须保留供其他用途的最小可用文件系统空间量，从而防止记账文件侵占文件系统可用空间。 如果可用空间降至该值以下，则挂起记账，直到有足够的文件空间可用，以便恢复记账。

为 “acctsuspend” 选择值

相关参数

“acctsuspend” 和 “acctresume” 是相互关联的。 为防止挂起-恢复冲突，“acctsuspend” 的带符号整数值必须始终小于 “acctresume” 的带符号整数值。

# allocate_fs_swapmap

预分配足够的内核数据结构，用于文件系统交换使用。

可接受的值：
- 最小值 0（按需分配交换数据结构）
- 最大值 1（预分配必要的内核数据结构）
- 默认值 0

指定 “0” 或 “1” 的整数值。

描述

“allocate_fs_swapmap” 决定文件系统交换的内核数据结构是仅在需要时分配还是预先保留（不适用于设备交换）。 仅识别两个有效值：

“allocate_fs_swapmap” = 0（默认值） 系统按需分配数据结构以节省系统内存。 在某些条件下，即使文件系统有用于交换的空间可用，系统也可能因缺少可用数据结构而拒绝交换请求。

“allocate_fs_swapmap” = 1 系统分配足够的数据结构，以容纳由 “swapon(1)” 系统调用或 “swapon” 命令指定的最大文件系统交换限制。 这确保只要文件系统有交换空间可用，内存中的空间就能支持交换请求。 这种模式最常用于高可用性系统，其中防止因资源不可用导致的进程失败比因在需要之前保留资源而导致的系统效率降低更重要。

# alwaysdump

“alwaysdump” 是一个位映射值，它定义如果发生内核恐慌时要转储哪些类的内核内存页。

可接受的值：
- 最小值 0
- 最大值 无
- 默认值 0

指定整数值。

描述

在大型系统中，发生内核恐慌时转储系统内存所需的时间可能过多甚至不可承受，具体取决于系统中安装的物理内存数量。 由 “dontdump” 和 “alwaysdump” 参数控制的快速转储功能提供了一种将内核转储限制于特定类型信息的手段：
- 未使用的物理内存
- 内核静态数据
- 内核动态数据
- 文件系统元数据
- 内核代码
- 缓冲区高速缓存
- 进程堆栈
- 用户进程

存储在 “alwaysdump” 中的位映射值指定在与内核恐慌相关的内存转储中应包括哪些这些内存类。

相关参数

“alwaysdump” 和 “dontdump” 具有相反的效果。 如果特定内存页类对应的位在一个参数中已设置，则不应在另一个参数中设置；否则会发生冲突，并且基于参数值的实际内核行为未定义。 当使用 SAM 设置值时（“Actions” 菜单中的修改页面类配置，内核配置区域中的 SAM “Dump Devices” 子区域），不会发生这些冲突。

# bufpages

定义文件系统缓冲区高速缓存中 4096 字节内存页的数量。

可接受的值：
- 最小值：“0” 或 64（"Nbuf*2” 或 64 页）
- 最大值：受内存限制
- 默认值：“0”

指定整数值或使用整数公式表达式。 仅当未使用动态缓冲区高速缓存时，才使用非零值。

描述

“bufpages” 指定为文件系统缓冲区高速缓存分配了多少 4096 字节内存页。 这些缓冲区用于所有文件系统 I/O 操作，以及系统中的所有其他块 I/O 操作（“exec”、“mount”、inode 读取和一些设备驱动程序。）

为 “bufpages” 指定值

若要启用动态缓冲区高速缓存分配，请将 “bufpages” 设置为零。 否则，请将 “bufpages” 设置为要分配给缓冲区高速缓存的 4-Kbyte 页的期望数量。 如果为 “bufpages” 指定的值非零但小于 64，则启动时会增加该数量并打印一条消息，宣布此更改。 如果 “bufpages” 大于系统支持的最大值，则启动时会减少该数量并打印一条消息。

相关参数和系统值

“bufpages” 控制分配给缓冲池的实际内存量。

如果系统启动时 “bufpages” 为零，则系统为 “nhbuf” 定义的每个缓冲头分配两个页。 如果 “bufpages” 和 “nbuf” 都为零，则系统启用动态缓冲区高速缓存分配并分配可用内存的一定百分比。

可以分配给缓冲池的最大内存量也受分配给系统用于其他目的的内存量的影响。 因此，修改影响系统内存的参数也可能影响可以为缓冲池提供的最大内存量。

# clcrservedmem

“clcrservedmem” 指定为高速分布式服务器环境（例如用于运行大型数据库处理程序的环境）中用户进程的 I/O 映射用途保留的系统内存字节数。

可接受的值：
- 最小值：“0”
- 最大值：无
- 默认值：“0”

指定整数值。

描述

常规 HP-UX 系统保留相对少量的系统内存用于 I/O 映射。 然而，某些专门的应用程序（如大型数据库处理程序）通常运行在由高速宽带通信网络组成的集群上。 由于对系统资源的强烈需求，这些应用程序通常通过内存映射 I/O 进行通信，其中大块的内存由应用程序和相应的 I/O 或网络软件共享。

可配置参数 “clcrservedmem” 提供了一种手段，用于预留多达 15/16（约 93%）的总系统



供执行大批量、内存映射、网络 I/O 的应用程序使用的内存。虽然该值最高可达 512 GB 甚至 1 TB，但更常见的范围大约从 1 GB 到 64 GB。无论 SAM 中选择的值是多少，系统实际保留的内存不能超过系统总内存的 15/16。

## create_fastlinks

使用快速符号链接。

可接受的值：

- 最小值：`"0"`
- 最大值：`"1"`
- 默认值：`"0"`

指定整数值。

### 描述

当 "create_fastlinks" 为非零时，它将导致系统以减少路径名查找中每个符号链接一次磁盘块访问的方式创建 HFS 符号链接。这涉及 HFS 磁盘格式的微小变化，使得为快速符号链接格式化的磁盘在 HP-UX 9.0 之前的 Series 800 系统和 HP-UX 10.0 之前的 Series 800 系统上无法使用（该可配置参数存在于 Series 700 9.0 版本系统中，但不在 Series 800 HP-UX 9.0 系统中）。

为了提供向后兼容性，"create_fastlinks" 的默认设置为零，即不创建更新的、更快的格式。但是，所有 HP-UX 10.0 内核（以及所有 Series 700 HP-UX 9.0 内核）都理解这两种磁盘格式，无论 "create_fastlinks" 设置为零还是非零。

## dbc_max_pct

定义动态缓冲区缓存使用的最大内存百分比。

可接受的值：

- 最小值：`"2"`
- 最大值：`"90"`
- 默认值：`"50"`

指定整数值。

### 描述

当参数 "buffers" 和 "nbuf" 都设置为默认值 0 时，缓冲区缓存的大小将根据系统内存的竞争请求动态增长或缩小。

“dbc_max_pct”的值设置为分配给动态缓冲区缓存的物理内存的最大百分比。

## dbc_min_pct

定义动态缓冲区缓存使用的最小内存百分比。

可接受的值：

- 最小值：“2”
- 最大值：“90”
- 默认值：“5”

指定整数值。

### 描述

在文件系统 I/O 操作期间，数据存储在缓冲区缓存中，其大小可以是固定的或动态分配的。当参数“bufpages”和“buf”都设置为默认值 0 时，缓冲区缓存的大小将根据系统内存的竞争请求动态增长或缩小。

“dbc_min_pct”的值指定为动态缓冲区缓存预留的最小物理内存百分比。

### 选择合适的值

如果“dbc_min_pct”设置得过低，对缓冲区缓存的极高需求可能会有效地挂起系统。当使用固定缓冲区缓存时也是如此。要确定最小缓存大小（以 MB 为单位）的合理（且保守）值，请使用以下公式：

(系统进程数) × (最大文件系统块大小) / 1024

要确定“dbc_min_pct”的值，将结果除以计算机中安装的物理内存的 MB 数，并将该值乘以 100，以获取正确的百分比值。

只有那些积极使用磁盘 I/O 的进程才应包含在计算中。所有其他进程都可以排除。以下是一些应包含在或排除在计算之外的进程的示例：

包含：
- NFS 守护进程，文本格式化程序，如 "troff"。
- 数据库管理应用程序，文本编辑器，
- 访问或使用源文件和/或编译器等
- 存储在系统上一个或多个文件系统中的输出文件，
- 且已挂载到系统上。

排除：
- X 显示应用程序，"ftp"、"term"、"rlogin"。
- 登录 shell、系统守护进程、"telnet"
- 或 "uucp" 连接等。这些进程使用
- 很少或没有磁盘 I/O。

## dst

启用或禁用夏令时转换，并指定转换计划。

可接受的值：

指定以下整数值之一：

- "0": 禁用夏令时
- "1": 将夏令时设置为美国样式（这是默认值）
- "2": 将夏令时设置为澳大利亚样式
- "3": 将夏令时设置为西欧样式
- "4": 将夏令时设置为中欧样式
- "5": 将夏令时设置为东欧样式

### 描述

"dst" 指定是否转换为夏令时，以及在夏令时和标准时间之间转换时使用哪种计划。

零值禁用转换为夏令时。非零值启用转换，并根据文件 `/usr/include/sys/time.h` 中的以下定义选择转换计划：

```c
#define DST_NONE    0    /* not on dst */
#define DST_USA     1    /* USA style dst */
#define DST_AUST    2    /* Australian style dst */
#define DST_WET     3    /* Western European dst */
#define DST_MET     4    /* Middle European dst */
#define DST_EET     5    /* Eastern European dst */
```

## default_disk_ir

启用磁盘 I/O 的即时报告。

可接受的值：

- 最小值：“0”（关闭）
- 最大值：“1”（开启）
- 默认值：“0”（关闭）

设置为“0”（禁用即时报告）或“1”（启用即时报告）。

### 描述

“default_disk_ir”启用或禁用即时报告。

当即时报告开启时，具有数据缓存的磁盘驱动器在数据被缓存时即从 “write()” 系统调用返回，而不是在数据写入介质后才返回。这有时可以提高写入性能，特别是对于顺序传输，但如果设备在将缓存数据写入介质之前发生电源故障或重置，缓存的数据可能会丢失。Series 800 系统上该参数的推荐值为零（关闭）。

虽然这不是 “mount” 命令的一个选项，但可配置参数 “default_disk_ir” 对文件系统（和原始）磁盘性能以及通过重置的数据完整性有深远影响。它可以设置为开启（设为 1）或关闭（设为 0）。

如果该可配置参数在用于创建内核（“/stand/system”）的内核配置文件中被省略，则假设为关闭（0）。因此，即时报告（也称为写入缓存启用，WCE）的默认行为是关闭（禁用）。

“default_disk_ir”还影响延迟写入与写穿文件系统行为。

## dontdump

“dontdump” 是一个位图值，定义如果在内核恐慌发生时，哪些类别的内核内存页将被转储。

可接受的值：

- 最小值：“0”
- 最大值：无
- 默认值：“0”

指定整数值。

### 描述

在大型系统中，内核恐慌发生时转储系统内存所需的时间可能过长甚至无法承受，这取决于系统中安装的物理内存量。由 “dontdump” 和 “alwaysdump” 参数控制的快速转储功能提供了一种将内核转储限制为特定类型信息的机制：

- 未使用的物理内存
- 内核静态数据
- 内核动态数据
- 文件系统元数据
- 内核代码
- 缓冲区缓存
- 进程堆栈
- 用户进程

存储在 “alwaysdump” 中的位图值指定哪些这些内存类别应包含在与内核恐慌相关的内存转储中。

### 相关参数

“alwaysdump” 和 “dontdump” 具有相反的效果。如果某个特定内存页类别对应的位在一个参数中被设置，则不应在另一个参数中设置；否则会发生冲突，并且基于参数值的实际内核行为将是未定义的。当使用 SAM 设置值时（操作菜单中的“修改页类配置”，内核配置区域中的 SAM “转储设备”子区域），这些冲突不会发生。

## enable_idds

enable_idds 保留用于将来使用。

可接受的值：

- 默认值：“0 (关闭)”

指定布尔值。

### 描述

enable_idds 保留用于可选产品的将来使用。
客户不应尝试更改此参数。在没有该可选产品的情况下启用此参数不会提供任何好处，并会使系统性能降低几个百分点。
IDDS = 入侵检测数据源

## egmemsize

指定等价映射内存保留池的大小（以页为单位）。

可接受的值：
- 最小值：“0”
- 最大值：受内存限制
- 默认值：“15”页

指定整数值或整数公式表达式。

### 描述

“egmemsize” 指定以页为单位预留的最少内存空间，作为供需要实际模式和虚拟模式下寻址相同的已分配内存的驱动程序和子系统使用的空间池。在启动时，系统可能会根据安装的物理内存量增加实际保留的空间。

驱动程序使用这些页在硬件接口之间传输信息。驱动程序使用虚拟模式将数据放置在页上。然后硬件使用直接内存访问（DMA）在实际模式下传输数据，绕过寻址转换。由于虚拟地址和实际地址相同，因此不需要特殊的地址处理。该空间也用于支持代表 “EXEC_MAGIC” 进程发出的地址别名请求。

通常，系统通过尝试从全系统内存池获取具有匹配虚拟地址的空闲页来动态处理等价映射内存的请求。如果系统无法动态获取等价映射页，它会求助于其保留池。通常，由于系统通常可以动态分配等价映射页，因此该保留池不应耗尽。然而，负载相对较高和/或...


超过 1 GB 的物理内存配置可能会导致此保留池耗尽。

根据在系统上运行的应用程序的具体性质、系统负载、内存和 I/O 配置以及其他因素，保留池仍有可能耗尽。如果发生这种情况，系统会在控制台上打印一条消息，指示保留池已耗尽，并且“eqmemsize”应该被增加。

## executable_stack

允许或拒绝在堆栈上执行程序（安全特性）。

可接受值：
- 最小值：“0”
- 最大值：“2”
- 默认值：“1”

指定整数值。“0”表示禁用，“1”表示启用，“2”表示带警告地启用。

### 描述

executable_stack 提供针对常见安全入侵行为的保护。它设置了系统范围的默认值，决定是否使用系统内存映射硬件来帮助保护免受最常见的安全入侵类型之一，通常称为“堆栈缓冲区溢出攻击”。

除非您有已证明的需要以其他方式操作，HP 强烈建议您将此参数设置为‘0’（零）。这是最安全的设置，不会带来性能损失，并且极少干扰合法的应用程序。

请注意，出于兼容性原因，此版本中该参数的默认设置为‘1’（一），这是兼容性最高但安全性最低的设置。它等同于 HP-UX 11.00 及更早版本中的系统行为，并且不提供针对此类攻击的保护。

有关此参数影响的详细描述、可能设置的含义、如何识别系统中是否需要不同的设置以及如何结合系统范围和每应用程序设置以获得安全性和兼容性之间最佳折衷方案，请参阅 charr(1) 手册页中关于‘+es’选项的描述。

## fs_async

选择将文件系统数据结构同步或异步写入磁盘。

可接受值：
- 最小值：“0”（仅使用同步磁盘写入）
- 最大值：“1”（允许异步磁盘写入）
- 默认值：“0”

指定“0”或“1”的整数值。

### 描述

“fs_async” 指定是否允许将文件系统数据结构异步写入磁盘。如果未指定“fs_async”的值，则使用同步写入。

同步写入磁盘使得在更新文件系统数据结构期间如果发生系统崩溃，更容易恢复文件系统的完整性。

如果选择异步写入，HP-UX 文件系统在 NFS 集群环境中的语义将得到保留。此外，使用“open()”并带有“O_SYNC”标志（同步写入）打开的文件，即使在配置了内核的异步写入功能后，仍将继续同步写入。

异步写入磁盘可以显著改善文件系统性能。然而，异步写入可能在系统崩溃事件中将文件系统数据结构置于不一致的状态。有关何时选择同步或异步写入的更多信息，请参阅此帮助页面后面部分的说明文本。

### 什么是同步和异步写入？

如果一个文件被打开用于写入并且正在向该文件写入数据，数据会在缓冲区中累积并定期写入磁盘。当发生文件结束条件并且文件准备关闭时，任何剩余的缓冲区内容都会被写入磁盘，模式会更新为文件大小和块指针信息，并且文件系统的空闲磁盘块列表会被更新。为了确保对文件系统完整性的最大保护，这些操作按照特定的顺序处理，该顺序最小化了在写入磁盘期间发生系统崩溃或电源故障时磁盘上文件系统损坏的风险。这种顺序更新过程被称为“同步写入”。

HP-UX 文件系统将空闲空间列表、块、inode 和其他文件组件随机存储在磁盘设备上的广泛分散的位置。这意味着以特定顺序写入文件信息块需要在执行写入操作前移动到磁盘上的所需位置，这需要额外的时间。如果在此序列期间发生电源故障或系统崩溃，一个或多个块可能无法正确更新，留下潜在的不一致文件系统。``fsck'' 命令用于修复此类不一致性。

与 ``fs_async'' 内核参数相关的异步写入允许系统以更便捷（因此更快）的顺序而不是更安全（更安全但更慢）的顺序在磁盘上更新文件系统信息，从而减少写入之间的搜索和移动延迟。然而，如果在执行这些操作时发生系统崩溃，则无法通过 fsck 自动修复的不一致文件系统的风险比同步写入显著更大。

### 崩溃的后果

如果仅使用同步写入，所有对目录、文件 inode、空闲空间列表等的更新都按照已知给 ``fsck'' 的顺序处理。如果在序列中更新任何磁盘块时发生崩溃，``fsck'' 可以轻松确定崩溃发生的位置并修复缺失的更新信息，可能不需要系统管理员的协助。

如果将 ``fs_async'' 设置为允许异步写入并发生崩溃，``fsck'' 不知道该使用哪种顺序，因此在修复不一致的文件系统信息、修复目录和 inode 项等时，可能需要管理员的交互式协助。

### 为什么允许异步写入？

在写入文件后关闭文件时等待同步写入和更新磁盘块会降低需要频繁文件和目录写入和关闭操作的程序和应用的性能。允许异步写入可以显著减少这些延迟，从而产生相应的性能提升。然而，当应用程序是 CPU 密集型且磁盘 I/O 相对较少时，性能提升要小得多。

### 何时应使用异步写入？

如果满足以下条件，异步写入可用于提高系统性能：

- 电源故障风险低（非常可靠的电源和/或不间断电源）。
- 已采取措施增强数据安全（复杂的文件系统备份或冗余策略），或者由于系统崩溃造成的潜在数据丢失比系统性能更重要。
- 用户应用程序需要频繁打开、写入和关闭磁盘文件和目录。
- 消除同步写入足以改善系统性能以抵消相关风险。

要启用异步写入，请将“fs_async”内核参数设置为“1”，而不是默认值“0”。

## hfs_max_ra_blocks

设置内核可以为单个 HFS 文件系统拥有的最大读入块数量。

可接受值：
- 最小值：“0”
- 最大值：“128”
- 默认值：“8”

指定整数值或使用整数公式表达式。

### 描述

当从磁盘驱动器读取数据时，系统可能会读取操作请求的额外数据。这种“读入”通过预期将读取额外数据并在请求之前使它们在系统缓冲区中可用，从而加速顺序磁盘访问。此参数限制内核允许为任何给定 HFS 文件系统拥有的未处理读入块数量。该限制适用于每个单独的 HFS 文件系统，而不是系统范围的总数。

应根据系统上工作负载的特征调整“hfs_max_ra_blocks”和“hfs_ra_per_disk”。

### 注意

要确定包含以下内容的文件系统的块大小

当前目录，请使用以下命令：

```
df -g
```

## 示例一

软件开发环境通常由小型或中型 I/O 组成，并伴有大量的磁盘寻道。因此，`hfs_max_ra_blocks` 应设置为 8 到 16 个块，而 `hfs_ra_per_disk` 应设置为 32 到 64 千字节。

## 示例二

用于 MCAE 应用的非内核算例求解器具有显著的顺序 I/O 组件，因此 `hfs_max_ra_blocks` 应设置为 64 到 128 个块，而 `hfs_ra_per_disk` 应设置为 128 到 256 千字节。

## hfs_ra_per_disk

设置每个磁盘驱动器 HFS 文件系统的预读量，单位为千字节（Kbytes）。

### 可接受值

- 最小值：`0`
- 最大值：`8192`
- 默认值：`64`

指定一个整数值或一个整数公式表达式。

### 描述

当从磁盘驱动器读取数据时，系统可能会读取超出操作请求的数据。这种“预读”通过预测将读取更多数据，并在请求之前将其保留在系统缓冲区中，从而加速顺序磁盘访问。

此参数指定每个磁盘驱动器允许的预读量。

预读的总量是通过将 `hfs_ra_per_disk` 乘以逻辑卷中的驱动器数量来确定的。如果文件系统不驻留在逻辑卷中，则驱动器数量有效地为一。

## hfs_revra_blocks

此参数设置每次 HFS 反向预读操作读取的最大块数。

### 可接受值

- 最小值：`0`
- 最大值：`128`
- 默认值：`8`

指定整数值。

### 描述

此可调参数定义了当按顺序反向读取时，预读操作中要读取的最大千字节数（Kbytes）。

只有 HP 现场工程师才应修改 hfs_revr_per_disk 内核参数。客户不应更改此参数的默认值。

### 目的

当已知工作负载包含频繁的文件反向顺序读取时，应提高此值。如果提高该值并未带来显著的性能提升，则应将此值降低回其默认值。增加此值可能会因过度的预读而导致额外的磁盘争用和性能损失。

### 相互作用

在更改 `hfs_revr_per_disk` 的值时，可能还需要修改以下额外的可调参数：

- `hfs_max_revr_blocks`
- `hfs_ra_per_disk`
- `hfs_max_ra_blocks`

## hfs_revr_per_disk

此参数设置每次反向预读操作读取的最大 HFS 文件系统块数。

### 可接受值

- 最小值：`0`
- 最大值：`8192`
- 默认值：`64`

指定整数值。

### 描述

此可调参数定义了当按顺序反向读取时，预读操作中要读取的最大文件系统块数。

只有 HP 现场工程师才应修改 hfs_revra_per_disk 内核参数。客户不应更改此参数的默认值。

### 目的

当在具有较小文件系统块大小的文件系统上进行大量反向顺序文件 I/O 时，应增加此参数的值。提高此参数的值意味着将在缓冲缓存中使用更多的内存。

当在具有较大文件系统块大小的文件系统上进行少量反向顺序文件 I/O 时，应降低此参数的值。降低此参数的值可能会导致文件吞吐量降低。

### 相互作用

在更改 "hfs_revra_per_disk" 的值时，可能还需要修改以下额外的可调参数：

- hfs_max_revra_blocks
- hfs_ra_per_disk
- hfs_max_ra_blocks

## initmodmax

"initmodmax" 指定当内核恐慌导致系统内存转储时，"savcrash" 命令将处理的最大内核模块数量。

### 可接受值

- 最小值："0"
- 最大值：无
- 默认值："50"

指定整数值。

### 描述

当发生内核恐慌（系统崩溃）时，在系统关闭之前，指定的系统内存区域会被复制到转储设备。然后可以使用 "savcrash" 命令将转储区域复制到文件系统中的目录中（根据系统大小和转储的内存类，需要!大量!空间）。

当内核包含动态可加载内核模块（未静态安装在内核中的驱动程序）时，"savercrash" 必须在其某个结构中分配空间以保存有关这些模块的信息。由于无法预测在任何给定时间可能加载了多少个模块，此参数提供了 "savercrash" 能够处理的上限。

如果 "initmodmax" 设置为小于已加载内核模块的数量，则 "savercrash" 只会处理遇到的前几个模块，直到达到限制。因此，系统管理员跟踪在系统运行期间加载了多少个内核模块至关重要，以确保在发生内核恐慌和转储时，"initmodmax" 具有足够的值来正确处理它们。

请注意，此参数仅影响 "savercrash" 命令的操作。它不会限制在系统正常运行期间可以加载到内核中的模块数量。

## ksi_alloc_max

"ksi_alloc_max" 指定可以分配的全局排队信号的最大数量。

### 可接受值

- 最小值："32"
- 最大值：（受内存限制）
- 默认值："nproc * 8"

指定整数值。

### 描述

内核为支持由使用 "sigqueue()" 系统调用的进程发送的排队信号所需的数据结构分配存储空间。此参数用于确定应分配多少空间。在系统正常运行的任何给定时间，如果现有进程发送的排队信号总数以及在接收方处仍挂起的信号总数足以填满可用的数据结构空间，则无法发送新的排队信号。

请注意，排队信号与传统 HP-UX/UNIX 信号不同。传统信号（如 kill 或 hangup 信号）是发送给接收进程的。如果向单个进程发送多个相同的信号，进程无法确定发送了不止一个信号。排队信号消除了这种模糊性，因为进程可以处理一个排队信号，然后再次检查队列以发现队列上的另一个信号。

"ksi_alloc_max" 通过控制内核中为处理排队信号分配的数据结构空间，指定在任何给定时间可以在系统范围内排队的最大排队信号数量。定义在 "/usr/include/limits.h" 中的 "SIGQUEUE_MAX" 和 "_POSIX_SIGQUEUE_MAX" 的极限值受此参数值的影响。

此参数的默认值设置为 "nproc * 8"，这允许一个足够大的总数，以容纳系统中每个正在运行的进程挂起的八个信号，假设系统以满容量运行。除非系统软件要求表明需要更多信号，否则这对几乎所有系统都应该是足够的。

## ksi_send_max

"ksi_send_max" 指定单个进程可以发送并在一个或多个接收方处挂起的排队信号的最大数量。

### 可接受值

- 最小值："32"
- 最大值：（受内存限制）
- 默认值："32"

指定整数值。

### 描述

内核为支持由使用 "sigqueue()" 系统调用的进程发送的排队信号所需的数据结构分配存储空间。此参数用于确定应分配多少空间。在系统正常运行的任何给定时间，如果现有进程发送的排队信号总数以及在接收方处仍挂起的信号总数足以填满可用的数据结构空间，则无法发送新的排队信号。

请注意，排队信号与传统 HP-UX/UNIX 信号不同。传统信号（如 kill 或 hangup 信号）是发送给接收进程的。如果向单个进程发送多个相同的信号，进程无法确定发送了不止一个信号。排队信号消除了这种模糊性，因为进程可以处理一个排队信号，然后检查队列

再次发现队列中的另一个信号。

“`ksi_send_max`”限制单个进程能够发送和/或在多个接收者处挂起的排队信号数量。它提供了一种机制，防止单个进程通过发出过多信号而独占信号数据结构空间，从而导致其他进程因内核资源不足而无法发送和接收信号。

“`32`”的默认值对于大多数常见的 HP-UX 应用程序来说都是足够的。如果你有专门的应用程序需要超过该数量的信号（`c’sigqueue()”` 返回 “`EAGAIN`”），除非 `sigqueue()”` 返回的 `EAGAIN` 错误是由一个失控的进程在不应生成信号时生成信号导致的，否则应适当增加该数值以避免此错误。

## maxvgs

系统上由逻辑卷管理器配置的最大卷组数量。

## no_lvm_disks

标志，用于在系统上不存在逻辑卷时通知内核。如果设置，所有文件系统都与系统上的物理磁盘及其物理边界一致。唯一的例外是当磁盘配置为分区，或磁盘的一部分保留用于交换及其他非文件系统用途时。

## max_async_ports

指定系统范围内，进程在任意时刻可以打开的异步磁盘 I/O 驱动程序的最大端口数。

可接受的值：

- 最小值： “`1`”
- 最大值： “”
- 默认值： “`50`”

指定整数值。

### 描述

“`max_async_ports`”限制了系统进程在任意时刻可以打开的异步磁盘 I/O 驱动程序的总端口数（这与任何 RS-232 异步数据通信接口无关）。系统在为每个端口打开时分配一个端口结构数组，用于进程和异步磁盘驱动程序之间的所有通信。给定应用程序所需的异步端口数量通常在该应用程序的文档中指定（例如数据库应用软件、视频管理软件等）。

要确定 “max_async_ports” 的合适值：

- 确定每个使用异步磁盘 I/O 的应用程序和/或进程需要多少端口。
- 确定这些应用程序中哪些将作为独立进程同时运行。还确定同一应用程序的多个副本是否会作为独立进程同时运行。
- 根据这些数字，确定所有进程在任意时刻需要打开的异步磁盘驱动程序的最大端口数，以获得一个合理的总数。
- 将 “max_async_ports” 设置为不小于该数值的值。

## maxsiz and maxsiz_64bit

指定执行进程的最大数据段大小（以字节为单位）。

可接受的值：

“maxsiz” 用于 32 位进程：

- 最小值： “0x400000”（4 Mbytes）
- 最大值： “0x7B03A000”（约 2 GBytes）
- 默认值： “0x400000”（64 Mbytes）

“maxsiz_64bit” 用于 64 位进程：

- 最小值： “0x400000”（4 Mbytes）
- 最大值： “4396972769279”
- 默认值： “0x400000”（64 Mbytes）

指定整数值。

### 描述

以字节为单位输入值。

“maxdsiz” 和 “maxdsiz_64bit” 分别定义了 32 位和 64 位执行进程的数据存储段的最大大小。数据存储段包含固定的数据存储（如静态变量和字符串），以及使用 “sbrk()” 和 “malloc()” 分配的动态数据空间。

仅当您有一个或多个进程使用大量数据存储空间时，才增加 “maxdsiz” 或 “maxdsiz_64bit” 的值。

每当系统加载进程，或执行中的进程尝试扩展其数据存储段时，系统都会检查进程数据存储段的大小。

如果进程的需求超过 “maxdsiz” 或 “maxdsiz_64bit”，系统将向调用进程返回错误，可能会导致进程终止。

## max_fcp_reqs

定义允许安装在机器上的任何 FCP 适配器上的并发光纤通道 FCP 请求的最大数量。可接受的值：

- 最小值： “ 0”
- 最大值： “ 1024”
- 默认值： “ 512”

指定整数值或使用整数公式表达式。

### 描述

“max_fcp_reqs” 指定 FCP 适配器上允许的并发 FCP 请求的最大数量。系统出厂时指定的默认值为 512 个请求。要调高或调低此限制，请指定该参数的所需值。并发请求的最佳限制取决于多种不同因素，如配置、设备特性、I/O 负载、主机内存以及 FCP 软件难以轻松确定的其他值。

### 相关参数和系统值

系统根据 "num_tachyon_adapters" 和 "max_fcp_reqs" 指定的值组合，为 Tachyon FCP 适配器分配内存。

## maxssiz and maxssiz_64bit

设置最大动态存储段（DSS）大小（以字节为单位）。可接受的值：

- "maxssiz" 用于 32 位进程：
  - 最小值："0x4000" (16 Kbytes)
  - 最大值："0x17F00000" (约 200 Mbytes)
  - 默认值："0x800000" (8 Mbytes)
- "maxssiz_64bit" 用于 64 位进程：
  - 最小值："0x4000" (16 Kbytes)
  - 最大值："1073741824"
  - 默认值："0x800000" (8 Mbytes)

指定整数值。

### 描述

以字节为单位输入值。

"maxssiz" 和 "maxssiz_64bit" 分别定义了 32 位和 64 位进程的动态存储段（DSS）最大大小，也称为用户栈段，或执行进程的运行时栈。该段包含通常用于局部变量的栈和寄存器存储空间。

默认的 DSS 大小满足大多数进程的需求。仅当您有一个或多个进程需要大量动态存储时，才增加 "maxssiz" 或 "maxssiz_64bit" 的值。

栈是动态增长的。随着其增长，系统检查进程栈段的大小。如果栈大小需求超过 "maxssiz" 或 "maxssiz_64bit"，系统将终止该进程。

## maxswapchunks

设置系统上可配置的最大交换空间量。

### 可接受的值：

- 最小值：" 1"
- 最大值：" 16384"
- 默认值：" 256"

指定整数值。

### 描述

"maxswapchunks" 指定系统上可配置的最大交换空间量。最大交换空间限制计算如下：

- 磁盘块每个包含 "DEV_BSIZE"（1024）字节。"DEV_BSIZE" 是系统范围的块存储大小，不可配置。
- 交换空间从设备到设备按块分配，每块包含 "swchunk" 个块。选择合适的 "swchunk" 值需要对系统内部结构有深入了解。如果没有这样的知识，不应更改 "swchunk" 的值，保持其标准默认值。
- 允许的系统范围内最大交换空间块数为 "maxswapchunks" 块。
- 最大交换空间（以字节为单位）为："maxswapchunks" × "swchunk" × "DEV_BSIZE"
- 例如，使用 "swchunk"（2048）和 "maxswapchunks"（256）的默认值，并假设 "DEV_BSIZE" 为 1024 字节，则可配置的总交换空间等于 537 Mbytes。

### 选择值

系统磁盘设备上可用的交换空间量由文件 "/etc/fstab" 的内容决定，不受内核配置的影响。

在独立系统或具有本地交换空间的集群客户端上，"maxswapchunks" 应设置为支持足够的交换空间，以容纳所有预期的交换量。将该参数设置得足够大，以避免需要重新配置内核。

对于服务器节点，设置该参数不仅要包括服务器本地的交换需求，还要包括每个将使用交换空间的客户端节点所需的足够交换空间。至少分配与以下数量相等的交换空间

每个客户端使用的内存量。

## max_thread_proc

指定单个进程允许拥有的最大线程数。

可接受的值：

- 最小值：`“64”`
- 最大值：`“30000”`
- 默认值：`“64”`

指定整数值。

## 描述

`“max_thread_proc”` 限制了单个进程允许创建的线程数量。如果某个失控进程在正常操作中创建的线程超出预期，此参数可保护系统免受系统资源过度使用的困扰。分配给此参数的值即分配给在 `“/usr/include/limits.h”` 中定义的极限变量 `“PTHREAD_THREADS_MAX”` 和 `“_SC_THREAD_THREADS_MAX”` 的极限值。

当进程被分割为多个线程时，进程空间的某些部分会为每个线程进行复制，这需要额外的内存和其他系统资源。如果失控进程创建了过多的进程，或者用户通过故意创建大量线程来攻击系统，系统性能可能会严重下降，甚至引发其他故障。

`“max_thread_proc”` 的取值应基于对系统将要运行的最复杂多线程应用程序的评估，并确定这些应用程序在最坏情况的正常使用下需要或创建的线程数量。该值至少应达到该数量，但不应大到足以在出现错误时损害其他系统需求。

## maxtsiz

设置最大共享文本段大小（以字节为单位）。

可接受的值：

32位进程的 `“maxtsiz”`：

- 最小值：`"262144"`（256 KB）
- 最大值：`"1073741824"`（1 GB）
- 默认值：`"0x4000000"`（64 MB）

64位进程的 `"maxsiz_64bit"`：

- 最小值：`"262144"`（256 KB）
- 最大值：`"4398046507008"`（约 4 TB）
- 默认值：`"0x4000000"`（64 MB）

指定整数值。

## 描述

`"maxtsiz"` 和 `"maxsiz_64bit"` 分别定义了32位和64位进程执行的进程共享文本段（程序存储空间）的最大尺寸。程序可执行对象代码以只读方式存储，因此，例如当两个或更多进程同时执行同一程序时，它们可以共享。

正常默认值适用于大多数进程的文本段。除非您计划执行文本段大于64 MB的进程，否则不要修改 `"maxtsiz"` 或 `"maxsiz_64bit"`。

每次系统加载具有共享文本的进程时，系统都会检查其共享文本段的大小。如果进程的文本段超出 `"maxtsiz"` 或 `"maxsiz_64bit"`，系统将发出错误消息并中止该进程。

`"maxtsiz"` 和 `"maxsiz_64bit"` 可以通过重新构建内核来设置，也可以在运行中的内核中通过 `"setname()"` 设置。`"SAM"` 和 `"kmtune"` 使用 `"setname()"`。对 `"maxtsiz"` 和 `"maxsiz_64bit"` 的动态更改仅影响未来对 `"exec()"` 的调用。动态降低这些参数不会影响任何正在运行的进程，直到它们调用 `"exec()"` 为止。

## maxuprc

设置最大同时用户进程数。

可接受的值：

- 最小值：`"3"`
- 最大值：`$Nproc-5$`
- 默认值：`"50"`

指定整数值。

## 描述

`“maxuprc”` 建立了系统中每个用户可用的最大同时进程数。用户由用户ID号识别，而不是由登录实例识别。每个用户至少需要一个进程用于登录Shell，以及该进程组中生成的所有其他进程的额外进程。（默认值通常足够）。

超级用户不受此限制。

管道在 `“|”` 的每侧至少需要一个同时进程。某些命令，如 cc、fc 和 pc，每次调用使用多于一个进程。

如果用户尝试启动一个新进程，导致该用户的总进程数超过 `“maxuprc”`，系统向用户发出错误消息：

no more processes

如果用户进程执行 `“fork()”` 系统调用以创建新进程，导致用户的总进程数超过 `“maxuprc”`，则 `“fork()”` 返回 -1 并将 `“errno”` 设置为 `“EAGAIN”`。

`“maxuprc”` 可以通过重新构建内核来设置，也可以在运行中的内核中通过 `“setune1()”` 设置。`“SAM”` 和 `“kmtune”` 使用 `“setune()”`。对 `“maxuprc”` 的动态更改仅影响未来对 `“fork()”` 的调用。将 `“maxuprc”` 降低到低于用户当前进程数量不会影响任何正在运行的进程。用户的过程将无法 `“fork()”`，直到当前进程退出足够多，使该用户的进程数低于新的限制。

## maxusers

根据系统上预期的同时用户数分配系统资源。

可接受的值：

- 最小值：`“0”`
- 最大值：受内存限制
- 默认值：`“32”`

指定整数值。

## 描述

`“maxusers”` 限制系统资源分配，而非系统中的实际用户数。`“maxusers”` 本身并不决定系统中任何结构的大小；相反，其他全局系统参数的默认值取决于 `“maxusers”` 的值。当其他可配置参数值以 `“maxusers”` 定义时，通过最小化因资源分配不当而导致的浪费空间，内核变得更小且更高效。

`“maxusers”` 定义了 C 语言宏 MaxUsers（例如，`“#define MaxUsers 8”`）。它决定了系统表的大小。用户数量的实际限制取决于购买的 HP-UX 许可证版本。要确定实际限制，请使用 `“uname -a”` 命令。

与其单独调整每个可配置参数，不如基于预期最大用户数使用公式来指定某些参数（例如，`“nproc”` (`“(20+8*MaxUsers)”`) 更容易。因此，如果您增加系统中的最大用户数，只需更改 `“maxusers”` 参数即可。

## maxvgs

指定系统上的最大卷组数。

可接受的值：

- 最小值：`“1”`
- 最大值：`“256”`
- 默认值：`“10”`

指定整数值。

## 描述

`“maxvgs”` 指定系统上的最大卷组数。内核为系统中的每个逻辑卷组创建一组数据结构。将此参数设置为与系统中的卷组数量相匹配，通过仅创建满足实际系统需求的数据结构来节省内核存储空间。

`“maxvgs”` 默认设置为十个卷组。要允许更多或更少，请更改 `“maxvgs”` 以反映新的最大数量。

## 相关参数

无。

## maxfiles

设置进程允许同时打开的文件数的软限制。

可接受的值：

- 最小值：`"30"`
- 最大值：`"60000"`
- 默认值：`"60"`

指定整数值。

### 描述

`"maxfiles"` 指定了系统默认的软限制，即进程在任何给定时间允许打开的文件数。进程可以增加其软限制，因此可以打开比 `"maxfiles"` 更多的文件。

非超级用户进程可以增加其软限制，直到达到硬限制 `"maxfiles_lim"`。

## maxfiles_lim

设置进程允许同时打开的文件数的硬限制。

可接受的值：

- 最小值：`"30"`
- 最大值：`"nfile"`
- 默认值：`"1024"`

指定整数值。

### 描述

`"maxfiles_lim"` 指定了进程可能拥有的打开文件数的系统默认硬限制。非超级用户进程可以增加其软限制，直到达到此硬限制。

`"maxfiles_lim"` 可以通过重新构建内核来设置，也可以在运行中的内核中通过 `"setnum()"` 设置。`"SAM"` 和 `"kernsnc"` 使用 `"setnum()"`。

动态更改会影响系统中所有现有进程，但有两类例外：已经超过新限制的进程不受影响。通过调用 `“setrlimit()”`（或 `“ulimit”`）明确设置其限制的进程不受影响。

## msg

在系统启动时启用或禁用内核中的 System V IPC 消息支持（仅限 Series 700）。

可接受的值：

- 最小值：`“0”`（从内核中排除 System V IPC 消息参数）
- 最大值：`“1”`（在内核中包含 System V IPC 消息参数）
- 默认值：`“1”`

指定 `“0”` 或 `“1”` 的整数值。

## 描述

`“msg”` 指定 System V IPC 消息参数的代码是否应在系统启动时包含在内核中（仅限 Series 700 系统）。

`“msg”` = 1 代码包含在内核中（启用 IPC 消息）。

`“msg”` = 0 代码不包含在内核中（禁用 IPC 消息）。

Series 800 系统：IPC 消息始终在内核中启用。

Series 700 系统：如果 `“msg”` 设置为零，则忽略所有其他 IPC 消息参数。

## modstrmax

`“modstrmax”` 指定 `“savecrash”` 内核模块表的最大大小，该表包含模块名称及其在文件系统中的位置。

可接受的值：

- 最小值：`“500”`
- 最大值：无
- 默认值：`“500”`

指定整数值。

## 描述




当发生内核恐慌（系统崩溃）时，系统内存的指定区域会在系统关机前复制到转储设备中。随后，可以使用 `saverash` 命令将转储区域复制到文件系统中的目录里（所需的内存空间量较大，具体取决于系统大小以及转储的内存类别）。

当内核包含可动态加载的内核模块（即未静态安装在内核中的驱动程序）时，`saverash` 会分配空间以跟踪模块名称及其在文件系统上的位置。该空间存储包含模块的目录的完整路径名称，以及模块名称。即使在一个目录中发现多个模块，也仅保留一份目录路径，从而优化了空间使用。

随着系统中添加的模块增多，如果模块名称倾向于较长，或者模块分散在文件系统的各处，则需要增加 `modstrmx` 以容纳额外的数据。

请注意，此参数仅影响 `saverash` 命令的操作。它不会限制正常系统运行期间可以加载到内核中的模块数量。

## **msgmap**

指定用于为共享内存中新消息分配位置的空闲空间资源映射的大小。

- **可接受值：**
  - 最小值：`3`
  - 最大值：受内存限制
  - 默认值：`msgtql+2`

指定整数值或整数公式表达式。

### 描述

消息队列在共享内存中实现为链表，每个消息由消息队列中的一个或多个连续槽位组成。随着消息被分配和释放，为消息保留的共享内存区域可能会出现碎片化。

`msgmap` 指定用于为新消息分配空间资源映射的大小。该映射显示了所有消息队列使用的共享内存消息空间中的空闲空洞。映射中的每个条目都包含指向一组连续未分配槽位的指针，并包含指向该组的指针以及该组的大小（即该组中的段数）。

消息大小的变化越大，空闲空间碎片化程度越高。由于资源映射需要为每个空闲空间片段保留一个条目，过度的碎片化可能导致空闲空间映射数组填满并溢出。如果内核在请求新消息空间或释放已接收消息使用的空间时发生溢出，系统会发出以下消息：

> 危险：mfree 映射溢出

如果发生此错误消息，请使用较大的 `msgmap` 值重新生成内核。

## msgmax

指定允许的最大单个消息大小（以字节为单位）。

- **可接受值：**
  - 最小值：`0`
  - 最大值：`min(msgmnb, msgseg * msgsz, 65535) 字节`
  - 默认值：`8192 字节`

指定整数值。

### 描述

`msgmax` 定义了队列中单个消息允许的最大大小（以字节为单位）。

仅当系统上使用的应用程序需要更大的消息时，才增加 `msgmax` 的值。此参数可防止恶意或编写不当的程序消耗过多的消息缓冲区空间。

## msgmmb

指定可以同时排在消息队列上的所有消息的最大总大小（以字节为单位）。

- **可接受值：**
  - 最小值：`0`
  - 最大值：`min(msgseg * msgsz, 65535) 字节`
  - 默认值：`16384 字节`

指定整数值。

### 描述

`msgmnb` 指定在任意时刻，给定消息队列中排队的消息的合并最大总大小（以字节为单位）。

任何试图超过此限制的 `msgsnd()` 系统调用都会返回以下错误：

- 如果设置了 `IPC_NOWAIT`，则返回 `EAGAIN`。
- 如果未设置 `IPC_NOWAIT`，则返回 `EINTR`。

可以通过重新构建内核设置 `msgmnb`，也可以在正在运行的内核中通过 `setune1()` 进行设置（`SAM` 和 `ktune` 使用 `setune1()`）。动态更改此参数仅影响新创建的消息队列。现有消息队列不受影响。

## **msgmni**

指定系统中可以同时存在的最大消息队列数量。

- **可接受值：**
  - 最小值：`1`
  - 最大值：受内存限制
  - 默认值：`50`

指定整数值。

### 描述

`msgmni` 定义了在任何给定时间系统中允许的最大消息队列标识符数量。

系统中创建的每个消息队列都需要一个消息队列标识符。

## **msgseg**

`msgseg` 指定在任何给定时间所有消息队列中可存在的消息段的最大总数。

- **可接受值：**
  - 最小值：`1`
  - 最大值：`32767`
  - 默认值：`2048`

指定整数值。

### 描述

`msgseg` 乘以 `msgsz`，定义了系统中所有消息队列可存在的共享内存消息空间的总量（不包括消息头空间）。

相关参数 `msgsz`（消息段大小，以字节为单位）定义了在任何队列中为每个消息段保留的字节数。当消息放入队列时，消息的长度决定了该消息使用了多少个 `msgsz` 段。队列中每个消息消耗的空间始终是 `msgsz` 的整数倍。

`msgseg`（消息段）定义了系统中所有队列可用的这些单元的数量。

## `msgssz`

指定在消息队列中分配消息空间时使用的消息段大小。

- **可接受值：**
  - 最小值：`1`
  - 最大值：受内存限制
  - 默认值：`8 字节`

指定整数值。

### 描述

`msgssz` 乘以 `msgseg`，定义了系统中所有消息队列可存在的共享内存消息空间的总量（不包括消息头空间）。

`msgssz` 指定了用于存储 IPC 消息的内存空间段的字节大小。通过分配一个或多个包含 `msgssz` 字节的每个消息段来创建新消息的空间，以容纳整个消息。

## msgtpl

指定在任何给定时间系统中允许存在的最大消息数量。

- **可接受值：**
  - 最小值：`1`
  - 最大值：受内存限制
  - 默认值：`40`

指定整数值。

### 描述

`msgtpl` 划分了一个用于存储消息头的区域。系统中排队的每个消息都会创建一个消息头。因此，消息头空间的大小定义了在任何给定时间系统中可以排队的最大消息总数。消息头存储在共享（可交换）内存中。

如果 `msgsnd()` 系统调用试图超过由 `msgtpl` 施加的限制，它会：

- 如果未设置 `IPC_NOWAIT` 标志，则阻塞等待空闲头；或者
- 如果设置了 `IPC_NOWAIT`，则返回 `EAGAIN`。

## ndilbuffers

设置在任意给定时间可以同时打开的最大设备 I/O 库设备文件数量。

- **可接受值：**
  - 最小值：`1`
  - 最大值：受内存限制
  - 默认值：`30`

指定整数值。

### 描述

`ndilbuffers` 定义了在任何给定时间，系统范围内可以同时打开的设备 I/O 库 (DIL) 设备文件的最大数量。

"ndiobuf" 专用于设备 I/O 库。如果不使用 DIL，则不需要 DIL 缓冲区。

## **nbuf**

设置系统范围内的文件系统缓冲区和缓存缓冲区头数量（决定系统中的最大总缓冲区数量）。请参见以下说明。

- **可接受值：**
  - 最小值：`0` 或 `16`
  - 最大值：受内存限制
  - 默认值：`0`
  - 指定值为零的整数（参见下文）。

### 描述

此参数用于向后兼容，并且应设置为零，因为首选动态缓冲区缓存。

如果设置为非零值，"nbuf" 指定为文件系统缓冲区缓存分配的缓冲区头数量。每个缓冲区分配 4096 字节内存，除非被 "bufpages" 的冲突值覆盖。

如果 "nbuf" 设置为小于 16 或大于系统支持的最大值的非零值，或者设置为与 "bufpages" 值不一致的值，该数值将适当增加或减少，并在启动时打印消息。

### 相关参数

"nbuf" 与 "bufpages" 的交互如下：

- "bufpages" = 0，"nbuf" = 0：启用动态缓冲区缓存。
- "bufpages" 非零，"nbuf" 为零：创建 "BufPages/2" 个缓冲区头，并在系统启动时分配 "bufpages" 倍 4 Kbytes 的缓冲区池空间。
- "bufpages" = 0，"nbuf" 非零：在启动时分配 "Nbuf*2" 页缓冲区池空间并创建 "Nbuf" 个头。
- "bufpages" 非零，"nbuf" 非零：在... 分配 "BufPages" 页缓冲区池空间并创建 "Nbuf" 个缓冲区头




## “ncallout”

指定内核在任何给定时间可排队的最大超时数量。

可接受值：

- 最小值：6
- 最大值：受内存限制
- 默认值：16+nproc

指定整数值或使用整数公式表达式。

### 描述

“ncallout” 指定内核在任何给定时间可排队的最大超时数量。超时被以下项目使用：

- “alarm()” 系统调用，
- “setitimer()” 系统调用，
- “select()” 系统调用，
- 驱动程序，
- “uucp” 进程，
- 进程调度。

当系统超过超时限制时，它会在系统控制台上打印以下致命错误：

panic: timeout table overflow

### 相关参数

如果增加 “nproc” 的值，应按比例增加 “ncallout”。一般规则是，除非你拥有使用多个调用的进程，否则每个进程应允许一个调用。

## ncnode

内存中可容纳的最大打开 CD-ROM 文件系统节点数。

可接受值：

- 最小值：14
- 最大值：受内存限制
- 默认值：150

指定整数值或使用整数公式表达式。

### 描述

“ncnode” 指定在任何给定时间内内存中（在 vnode 表中）可容纳的最大 CD-ROM 文件系统节点数。它在功能上类似于 “minode”，但仅适用于 CD-ROM 文件系统。在 700 系列和 800 系列系统上的行为相同。

每个节点消耗 288 字节，这意味着，例如，如果将 “ncnodes” 设置为 10000，则几乎 3 Mbytes 的内存被专门保留用于 CD-ROM 文件系统节点表。

## nclist

指定用于 tty 和 tty 数据传输的 cblocks 数量。

可接受值：

- 最小值：132
- 最大值：受可用内存限制
- 默认值：(100 + 16 * MAXUSERS)

指定整数值或使用整数公式表达式。

### 描述

“nclist” 指定系统中分配了多少个 cblocks。当数据流量通过 tty 和 tty 设备时，它被存储在 cblocks 中。

“nclist” 的默认值，“(100 + 16 * MAXUSERS)”，基于以下公式：100 个 cblocks 用于系统处理控制台等流量，加上每个用户会话平均 16 个 cblocks。请注意，cblocks 也用于除登录会话以外的串行连接，如 SLIP 连接、UIUCP 传输、终端仿真器等。如果你的系统使用这些其他类型的连接，应相应地增加 “nclist”。

如果 cblock 池耗尽，通过 tty 或 pty 设备传输的数据可能会丢失，因为在其需要时没有可用的 cblock。

## nfile

设置在任何给定时间系统中可同时打开的最大文件数。

可接受值：

- 最小值：14
- 最大值：受内存限制
- 默认值：((16+(NPROC+16+MAXUSERS)/10)+32+2*(NPTY+NSTRPTY+NSTREL))

指定整数值或使用整数公式表达式。

### 描述

“nfile” 定义了在任何时刻系统范围内可同时打开的最大文件数。它是文件描述符表中的槽位数。请 generously 对待这个数值，因为所需的内存非常少，而槽位不足会限制系统处理能力。

## nfilefs

指定在任何给定时间内，系统范围内所有进程可用的文件锁的总最大数量。

可接受值：

- 最小值：2
- 最大值：受内存限制
- 默认值：209

指定整数值或使用整数公式表达式。

### 描述

“nfilefs” 给出系统范围内可用的文件/记录锁的最大数量。在选择此数值时，请注意，一个文件可能有多个锁，而使用 lockf() 的数据库可能需要异常大量的锁。

打开和锁定的文件消耗内存和其他系统资源。这些资源必须与其他系统需求保持平衡，以维持最佳的整体系统性能。由于每个系统上使用的应用程序类型、同时运行的应用程序数量和类型、系统中的本地和/或远程用户数量以及许多其他因素存在巨大差异，特别是在大型系统中，实现最佳平衡可能非常复杂。

## ninode

指定内存中可容纳的最大打开 inode 数。

可接受值：

- 最小值：14
- 最大值：受内存限制
- 默认值：nproc+48+maxusers+(2*"npty")

指定整数值或使用整数公式表达式。

### 描述

“ninode” 定义了 inode 表中的槽位数，从而定义了内存中可容纳的最大打开 inode 数。inode 表用作缓存内存。出于效率原因，最近 “ninode” 个（数量）打开的 inode 保留在主内存中。该表是散列的。

每个唯一的打开文件都有一个相关的打开 inode。因此，唯一打开文件的数量越大，“ninode” 就应越大。

## nkthread

指定在任何给定时间内，所有进程合计在系统范围内可运行的最大线程数。

可接受值：

- 最小值：50
- 最大值：30000
- 默认值：[(nproc*2)+16]

指定整数或公式值。

### 描述

使用线程以提高性能的过程会创建其进程空间的某些部分的多份副本，这需要线程存储的内存空间以及与管理线程相关的处理器和系统开销。在运行大型线程化应用程序的系统上，可能需要大量线程。内核参数 “max_thread_proc” 限制单个进程可创建的线程数，但系统中可能有其他线程化应用程序也使用大量线程或具有更 modest 的需求。

“nkthread” 限制系统中所有进程在任何给定时间可运行的线程总最大数量。此值保护系统，防止被超过正常、合理操作的大量线程压垮。它保护系统免受多个大型应用程序运行时的过载，也保护系统免受恶意用户通过启动大量线程程序来破坏系统运行的行为，导致资源无法用于正常的系统需求。

默认值允许每个进程平均两个线程外加额外的系统允许量。如果你需要使用更大的值：

- 确定系统中每个线程化应用程序所需的线程总数；特别是任何大型应用程序。
- 确定在任何给定时间内这些应用程序中有多少以及哪些会同时运行。
- 将这些加在一起，并为偶尔使用线程的其他用户或进程留出合理的允许量（“nproc*2” 可能是一个有用的数字）。
- 选择一个足够大的 “nkthread” 值以容纳总数，但不要大到损害系统完整性。

## no_lvm_disk

告知内核系统中不存在逻辑卷组（仅限 700 系列）。

可接受值：

- 最小值：0（检查 LVM 磁盘）
- 最大值：1（系统没有 LVM 磁盘）
- 默认值：0

指定 0 或 1 的整数值。

### 描述

默认情况下，在启动时，系统会检查配置的主磁盘、交换和转储磁盘上的 LVM 数据结构。如果系统中不存在 LVM 磁盘，将 “no_lvm_disks” 设置为 1 可通过省略对 LVM 数据结构的检查来加快启动过程。

在使用 LVM 的系统上将此参数设置为非零值会导致内核 panic，因为内核在正常启动过程中无法获取关于系统中逻辑卷的必要信息。

## nproc

进程数量

- 最小值：10
- 最大值：受内存限制
- 默认值：20+(8 * maxusers)

指定整数值或使用整数公式表达式。

### 描述

“nproc” 指定系统中可同时存在的最大进程总数。

始终至少有四个系统开销进程，并且始终为一个条目保留给超级用户。

当系统中的进程总数大于 “nproc” 时，系统会发出以下消息：

在系统控制台上：

proc: table is full

此外，如果用户尝试从 shell 启动新进程，用户的终端上会打印以下消息：

no more processes




如果用户正在执行 `fork()` 以创建新进程，`fork()` 会返回 -1 并将 `errno` 设置为 `EAGAIN`。

## npty

指定系统中可用的伪终端数据结构的最大数量。

可接受的值：
- 最小值：`1`
- 最大值：受内存限制
- 默认值：`60`

指定整数值。

### 描述

`npty` 限制了伪电传终端驱动程序可使用的以下结构数量：

```
struct tty    pt_tty[npty];
struct tty    *pt_line[npty];
struct pty_info pty_info[npty];
```

## NSTREVENT

设置在任何给定时间允许在系统中存在的未决流 bufcall 的最大数量。

可接受的值：
- 最小值：无
- 最大值：无
- 默认值：`50`

指定整数值。

### 描述

此参数限制了在任何给定时间允许在流中存在的未决 bufcall 的最大数量。特定流中存在的 bufcall 数量由推送到该流中的流模块的数量和性质决定。

此参数旨在保护系统免受由所有流中运行的模块组合发出的过多 bufcall 引起的资源过载。所选值应等于或大于在正常运行期间从系统上所有流中合理预期的 bufcall 最大总数。该值取决于每个可用流模块的行为和结构，以及在任何给定时间可推送到系统中所有流的模块数量和组合。

## nstrpty

设置系统范围内允许的最大流基础 PTY 数量。

可接受的值：
- 最小值：`0`
- 最大值：受内存限制
- 默认值：`0`

指定整数值。

### 描述

此参数限制了系统范围内允许的流基础 PTY 数量。当向 PTY 设备（例如窗口）发送数据时，在任何给定时间，每个打开的窗口都必须存在一个 PTY 设备。

此参数应设置为等于或大于系统中将使用流基础 I/O 管道的 PTY 设备数量的值。不建议使用显著大于 PTY 数量的参数值。`nstrpty` 用于在内核中创建数据结构以支持这些流基础 PTY，过大的值会浪费内核内存空间。

## NSTRPUSH

设置在任何给定时间允许在系统中任何单个流中存在的流模块的最大数量。

可接受的值：
- 最小值：无
- 最大值：无
- 默认值：`16`

指定整数值。

### 描述

此参数定义了可以推送到任何特定流中的流模块的最大数量。这提供了一些保护，以防止失控进程自动选择推送到流中的模块，但其目的并非作为防止系统用户恶意使用流模块的防御手段。

大多数系统在任何给定流中不需要超过三或四个模块。然而，可能存在需要更多模块的某些不寻常情况。此参数的默认值允许一个流中有多达 16 个模块，这对于甚至要求最严格的安装也应该是足够的。

如果你的系统需要一个流中超过 16 个模块，应仔细评估这种需求，并且还应仔细评估对未决 bufcall 和其他因素等其他系统资源的需求。

## NSTRSCH

设置在任何给定时间允许在系统中运行的流调度器守护进程 (`smipsched`) 的最大数量。

可接受的值：
- 最小值：`0`
- 最大值：`32`
- 默认值：`0`

指定整数值。

### 描述

此参数定义了在多处理器（MP）系统中运行的多处理器（MP）流调度器守护进程的最大数量。请注意，单处理器（UP）系统不使用 MP 调度器守护进程，但 MP 和 UP 系统始终都有一个 UP 流调度器 (`sopsched`)。

如果参数值设置为零，系统将基于系统中的处理器数量确定运行多少个守护进程。所选值为 2-4 个处理器时为 `1`，5-8 个处理器时为 `2`，9-16 个处理器时为 `3`，超过 16 个处理器时为 `4`。

如果参数值设置为正的、非零值，那么这就是将在 MP 系统上创建的 `smsched` 守护进程的数量。

## nstrtel

指定内核可以支持用于传入 telnet 会话的 telnet 设备文件的数量。

可接受的值：
- 最小值：`60`
- 最大值：`6`
- 默认值：`60`

指定整数值。

### 描述

`nstrtel` 指定在系统启动时创建的内核数据结构数量，这些结构是支持服务器上用于传入 telnet 会话的设备文件所必需的。该数量应与系统中存在的设备文件数量相匹配。

如果使用 `insf` 命令或 SAM 创建更多的 telnet 设备文件，则必须相应增加 `nstrtel` 的值，否则由于没有可用于与系统通信的内核数据结构，设备文件将无法使用。

选择一个等于或大于系统中 telnet 设备文件数量的 `nstrtel` 值。选择一个超过系统中实际存在的设备文件数量的值会浪费由额外数据结构消耗的内存，但如果计划添加更多设备文件，这可能是合理的。

## nswapdev

指定可以启用设备交换的磁盘设备数量。

可接受的值：
- 最小值：`1`
- 最大值：`25`
- 默认值：`10`

指定一个等于为设备交换配置的物理磁盘设备数量的整数值，最大限制为 25。只允许整数值（公式值不适用于此参数）。

### 描述

`nswapdev` 定义了可用于设备交换的最大设备数量。

在系统启动时，内核创建足够的内部数据结构以支持对指定数量的保留系统交换区域的物理设备进行设备交换。如果指定值大于可用设备数量，则额外的数据结构空间永远不会被使用，从而浪费少量内存（每个结构 <50 字节）。如果值小于可用设备数量，则由于内核中缺乏支持数据结构，某些设备无法用于交换。

相关参数

无。

## nswapfs

指定可以启用文件系统交换的文件系统数量。

可接受的值：
- 最小值：`1`
- 最大值：`25`
- 默认值：`10`

指定一个等于可用于文件系统交换的文件系统数量的整数值，最大限制为 25。

### 描述

`nswapfs` 定义了可用于文件系统交换的最大文件系统数量。

在系统启动时，内核创建足够的内部数据结构（每个结构约 300 字节）以支持对指定数量的文件系统进行文件系统交换。如果指定值大于可用文件系统数量，则额外的数据结构空间永远不会被使用，从而浪费相应数量的内存。如果值小于可用文件系统数量，则由于缺乏支持数据结构，某些文件系统无法用于交换。

相关参数

## nssymap

设置内核动态内存虚拟地址空间资源映射中的条目数量。

可接受的值：
- 最小值：`800`
- 最大值：受内存限制
- 默认值：`2 * nproc`

指定整数值。

### 描述

nssymap 及其 64 位等效项 nssymap64 设置了内核动态内存资源映射的大小，这是一个描述内核动态地址空间中空闲虚拟空间的地址/长度对数组。由于 64 位内核具有更多的虚拟地址空间，因此 32 位和 64 位内核有不同的可调参数。

以前，内核动态内存资源映射仅由系统设置，且不易更改。某些严重分散内核地址空间的工作负载导致资源映射中出现过多条目。当发生这种情况时，资源映射中的最后一个条目被丢弃，导致“泄漏”的内核虚拟地址空间。如果此溢出发生得足够频繁，虚拟空间就会被耗尽。

系统在启动时根据系统工作负载使用算法自动缩放映射大小。如果值仍然设置得不够高以避免内存资源映射数组溢出的问题，您可以调整此参数以适合特定工作负载。

请注意，即使覆盖了默认值，内核也可能根据系统大小将值增加到该值以上。

## 目的

此可调参数已添加以解决“kalloc: 虚拟空间不足”系统崩溃的问题。只有经历资源映射溢出的系统才需要修改此可调参数。




当发生资源映射溢出时，控制台将显示以下消息：

sysmap32: rmap ovflo, lost [X,Y] *

或

sysmap64: rmap ovflo, lost [X,Y]

* 其中 X 和 Y 是十六进制数字。

如果这种情况很少发生，则无需采取任何措施。如果这种情况经常发生（例如，在用户不打算长时间（一年或更久）重新启动的系统中，每天发生几次），则应增加该可调参数的值。如果不增加该可调参数，可能会发生以下内核恐慌（panic）：

kalloc: out of kernel virtual space

在增加 nsysmap(32/64) 时，将可调参数值加倍是一个合理的经验法则。如果在从默认值加倍几次后问题仍然存在，则可能存在其他内核问题，客户应通过其正常的 HP 支持渠道进行调查。

## 副作用

如果增加此参数的值，内核内存使用量会非常轻微地增加。根据工作负载，如果该可调参数相当大，内核内存分配的性能可能会受到负面影响。

将此参数的值从默认值降低是有风险的，会增加资源映射溢出的概率，最终导致内核恐慌。在降低 nsysmap 的值之前，请咨询您的 HP 支持代表。

## num_tachyon_adapters

如果系统不支持 I/O 虚拟寻址，则定义系统中光纤通道 Tachyon 适配器的数量。

可接受的值：

- 最小值：`0`
- 最大值：`5`
- 默认值：`0`

指定整数值或整数公式表达式。如果系统不提供 I/O 虚拟寻址，则非零值是`required`（必需的）。选择一个等于系统中安装 Tachyon FCP 适配器数量的值。

## 描述

`"num_tachyon_adapters"` 指定系统中安装了多少个 Tachyon FCP 适配器，以便在系统启动时，如果系统不提供 I/O 虚拟寻址，可以为它们分配适量的内存。

## 为 `"num_tachyon_adapters"` 指定值

如果您的系统不提供 I/O 虚拟寻址，请将 `"num_tachyon_adapters"` 设置为实际安装在机器中的 Tachyon FCP 适配器的数量。在启动期间，系统将为这些适配器保留相应数量的内存，并根据 `"max_fcp_reqs"` 的值调整该数量。

如果系统支持 I/O 虚拟寻址，请将该参数设置为零。然后系统将自动按需分配内存。

如果您不确定系统是否提供 I/O 虚拟寻址，只要该值不超过系统中实际安装的 Tachyon FCP 适配器的数量，将此参数设置为非零值是无害的。如果该值超过已安装适配器的数量，则会浪费相应数量的内存，因为它不能用于其他目的。

## 相关参数和系统值

系统根据为 `"num_tachyon_adapters"` 和 `"max_fcp_reqs"` 指定的值的组合来分配内存以供 Tachyon FCP 适配器使用。

## o_sync_is_o_dsync

`"o_sync_is_o_dsync"` 指定是否允许系统将 `"open()"` 或 `"fcntl()"` 调用中的 `"O_SYNC"` 标志转换为 `"O_DSYNC"` 标志。

可接受的值：

- 最小值：`"0"`
- 最大值：`"1"`
- 默认值：`"0"`

指定整数值。

## 描述

在 `open()` 或 `fcntl()` 调用中，`O_SYNC` 和 `O_DSYNC` 标志用于确保数据在调用返回之前正确写入磁盘。如果没有设置这些标志，函数会在磁盘访问请求发起后立即返回，并假设写入操作将由系统软件和硬件成功完成。

设置 `O_SYNC` 或 `O_DSYNC` 标志可以防止函数返回到调用进程，直到请求的磁盘 I/O 操作完成，并且直到写入操作更改的所有文件属性（包括访问时间、修改时间和状态更改时间）也写入磁盘。只有在那之后，它才会返回到调用进程。

将 `o_sync_is_o_dsync` 设置为 `"1"` 允许系统将任何包含 `O_SYNC` 标志的 `open()` 或 `fcntl()` 调用转换为使用 `O_DSYNC` 标志的相同调用。这意味着该函数会在文件属性在磁盘上更新之前返回到调用进程，从而引入风险，即如果发生系统故障，此信息可能不在磁盘上。

将此参数设置为非零值允许函数在文件时间戳属性更新之前返回，但仍确保实际文件数据在调用进程可以继续之前已提交到磁盘。这在执行大量磁盘 I/O 并要求文件数据完整性的安装环境中很有用，但通过不强制在继续之前更新时间戳，可以获得一些性能优势。当性能提升的好处超过如果系统或磁盘崩溃时拥有错误文件访问时序信息的相关风险时，可以将此参数设置为 `"1"`。如果情况并非如此，则应将其保持为默认值零。

此参数的设置不影响未使用 `O_SYNC` 的磁盘 I/O 操作。

## page_text_to_local

在 NFS 集群客户端上启用或禁用将程序文本段交换到本地交换设备。

可接受的值：

- 最小值：`0` （独立运行，或客户端使用文件系统服务器）
- 最大值：`1` （使用客户端本地交换）
- 默认值：`1` （使用客户端本地交换）

指定 `0` 或 `1` 的整数值。

## 描述

程序通常包含三个段：

- 文本段：程序中不可变的可执行代码部分。
- 数据段：数组和其他固定数据结构。
- DSS 段：动态存储、堆栈空间等。

为了最大限度地减少不必要的网络流量，没有本地交换设备的 NFS 集群客户端在需要交换内存以为另一个程序或应用程序腾出空间时，会丢弃程序的文本段。丢弃文本段是因为，在没有本地磁盘可用的情况下，交换到服务器上的交换空间，然后稍后检索存在于原始程序文件中的相同数据，会浪费服务器磁盘空间并增加网络数据流量。

然而，当连接到客户端机器的本地磁盘设备上有足够的交换空间时，将文本段写入本地交换并稍后检索更有效。这消除了文本段数据到服务器和从服务器传递的两次独立传输，从而提高了集群性能（取决于使用的特定应用程序和程序）。要以这种方式使用本地交换，可用的交换空间必须大于系统中任何时刻运行的所有进程所需的最大总交换空间。如果不满足此条件，当出现空间冲突时，会发生系统内存分配错误。

`page_text_to_local` 是一个可配置的内核参数，决定是丢弃文本段还是将其交换到本地设备以节省网络流量。

- `0`：不使用本地客户端交换设备。客户端要么没有本地交换设备，要么没有足够的空间支持完整的文本交换。如果需要内存空间，则丢弃文本段，然后在准备再次执行时从服务器检索原始文件。
- `1`：当内存空间需要用于其他目的时，将文本页交换到本地交换设备，然后在需要该段时从交换设备检索。这通常可以提高客户端性能并减少集群网络数据流量。如果使用此值，必须启用本地交换，并且客户端本地磁盘上可用的设备交换空间必须足以满足任何给定时间客户端上可能运行的所有程序所需的最大虚拟内存。否则，进程可能因内存不足而失败。

在独立的非集群系统上，将 `“page_text_to_local”` 设置为 `“0”`。

## pfail_enabled

禁用或启用系统电源故障例程（仅限 Series 800）。

可接受的值：

- 最小值：`0`
- 最大值：`1`
- 默认值：`0`

指定整数值。

## 描述

`“pfail_enabled”` 确定 Series 800 系统是否能够识别本地电源故障（这种故障通过影响中央总线使计算机停止运行）。值可以设置为零或 `“1”`，如下所示：

- `0`：禁用 powerfail 检测。这阻止系统运行 `“/sbin/powerfail”` 命令（由 `“/etc/initab”` 启动），以便在发生电源故障时提供恢复措施。发生电源故障时正在运行的程序无法在电源恢复后继续执行。
- `1`：启用 powerfail 检测。这使得系统能够识别电源故障，并采用与 `“/sbin/powerfail”` 命令（由 `“/etc/initab”` 启动）相关的恢复机制，以便在发生电源故障时，正在运行的程序可以在电源恢复后继续执行。

请务必遵循正确的关机




# 内核参数说明

由电源故障（powerfail）触发的系统。相关准则在 `<book>[系统管理任务]` 手册中进行了讨论。

请注意，尽管 powerfail 出现在所有 `/etc/initab` 文件中，但该条目仅由支持 powerfail 的系统识别和使用。

### public_shlibs

为共享库启用“公共”保护 ID。

可接受的值：
- 最小值：`0`
- 最大值：`1`（或非零值）
- 默认值：`1`

指定整数值。

描述

`public_shlibs` 启用共享库使用“公共”保护 ID 的功能。

共享库使用 `mmap()` 实现，并且每个单独的 `mmap()` 都会被赋予一个唯一的保护 ID。进程有四个保护 ID 寄存器，其中两个被硬编码为文本/数据。剩余的两个在用户进程访问的任意共享库/共享内存段之间来回共享。

当引入共享库时，出现了一个性能问题，导致进程 ID (pid) 抖动增加。为了最小化这种影响，为所有共享库映射添加了一个公共保护 ID，从而有效地将共享库从访问这两个保护 ID 寄存器的对象池中移除。

将 `public_shlibs` 设置为 `1` 允许系统为共享库分配公共保护 ID。将其设置为 `0` 会禁用公共访问，并为每个共享库放置一个唯一的保护 ID。默认值为 `1`，任何非零值都被解释为 `1`。

!!仅当!! 存在某些“安全漏洞”或其他不应使用公共值的理由时，才将此参数设置为零值。

### rtsched_numpri

指定可用的、不同的实时进程调度优先级数量。

可接受的值：
- 最小值：`32`
- 最大值：`512`
- 默认值：`32`

指定整数值。

描述

`rtsched_numpri` 指定在实时调度程序（POSIX 标准，P1003.4）下运行的实时进程可以设置的优先级级别的数量。

适当的值

默认值 32 满足大多数配置的需求。在需要进程间更多不同优先级级别的情况下，相应地增加该值。但是，请注意，增加 `rtsched_numpri` 的值以指定更大数量的优先级会导致系统花费更多时间评估符合条件的进程，从而导致整体系统性能可能下降。

### remote_nfs_swap

`remote_nfs_swap` 启用或禁用系统向 NFS 挂载设备或文件系统执行交换（swap）的能力。

可接受的值：
- 最小值：`0`
- 最大值：`1`
- 默认值：`0`

指定整数值。

描述

使用 `remote_nfs_swap` 启用或禁用系统向 NFS 挂载设备或文件系统执行交换的能力。默认值零禁用 NFS 交换。要启用，请将值更改为 `1`。

此参数最初创建是为了允许 NFS 集群中的客户端使用服务器上的磁盘空间进行交换。HP-UX 系统不再支持 NFS 集群，并且此参数默认设置为零（不允许远程 NFS 交换）。除非允许此功能的系统具有极快的 NFS 能力，否则将此参数设置为允许远程 NFS 交换并不是非常有用。

### scsi_maxphys

设置 SCSI I/O 子系统的最大记录大小，以字节为单位。

可接受的值：
- 最小值：`1048576 (1 MB)`
- 最大值：`16777215 (16MB - 1)`
- 默认值：`1048576 (1 MB)`

指定整数值。

描述

此参数与 `st_large_recs` 配合使用，以启用大型磁带记录支持，而无需逻辑记录的拆分和重组。

### scsi_max_qdepth

设置 SCSI 设备队列中 SCSI 命令的最大数量。

可接受的值：
- 最小值：`1`
- 最大值：`255`
- 默认值：`8`

指定整数值。

描述

对于支持大于系统默认值的队列深度的设备，此参数控制驱动程序在任何一次时刻尝试向设备队列中放入多少个 I/O。有效值为 (1-255)。某些磁盘设备不支持通过此命令设置的最大队列深度。将软件队列深度设置为大于磁盘可处理值的值，一旦磁盘存在队列已满（QUEUE FULL）状态，将导致 I/O 被挂起。

### st_fail_overruns

如果设置，导致数据溢出的 SCSI 磁带读取将导致失败。

可接受的值：
- 禁用：`0`
- 启用：`1`
- 默认值：`0`

指定 `0` 或 `1`。

描述

某些技术应用程序依赖于以下事实：读取小于实际磁带记录大小的记录应生成错误。

### st_large_recs

如果设置，为 SCSI 磁带启用大记录支持。

可接受的值：
- 禁用：`0`
- 启用：`1`
- 默认值：`0`

指定 `0` 或 `1`。

描述

此参数与 `scsi_maxphys` 配合使用，以启用大型磁带记录支持，而无需逻辑记录的拆分和重组。

### scroll_lines

指定 ITE 控制台屏幕缓冲区中的显示行数。

可接受的值：
- 最小值：`60`
- 最大值：`999`
- 默认值：`100`

指定整数值。

描述

`scroll_lines` 定义滚动区域（配置到系统中的每个内部终端仿真器 (ITE) 端口上模拟终端屏幕内存的行数）。

### semmsni

指定系统中可以同时存在的 IPC 信号量组的最大数量。

可接受的值：
- 最小值：`2`
- 最大值：内存限制
- 默认值：`64`

指定整数值或使用整数公式表达式。

描述

`semmsni` 定义可供系统用户使用的信号量组（标识符）的数量。

当系统用尽信号量组时，`semget()` 系统调用返回 `ENOSPC` 错误消息。

### semmsns

定义系统范围内可以为用户分配的单个 IPC 信号量的最大数量。

可接受的值：
- 最小值：`2`
- 最大值：内存限制
- 默认值：`128`

指定整数值或使用整数公式表达式。

描述

`semmax` 定义系统范围内可供系统用户使用的单个信号量最大总数。

当空闲空间映射显示共享内存的信号量区域中满足 `semget()` 请求的连续信号量插槽不足时，`semget()` 返回 `ENOSPC` 错误。即使可能有足够的空闲信号量插槽，但如果它们不连续，也会发生此错误。

### semmsu

定义系统中可以在任意给定 IPC 信号量上拥有挂起取消操作的最大进程数量。

可接受的值：
- 最小值：`1`
- 最大值：`nproc*4`
- 默认值：`30`

指定整数值。

描述

!<undo!! 是信号量操作中的一个特殊、可选标志，如果调用该操作的进程终止，则导致该操作被撤销。

`semmsu` 指定在给定信号量上可以拥有挂起取消操作的进程的最大数量。它决定了 `sem_undo` 结构的大小。

使用 `SEM_UNDO` 标志的 `semop()` 系统调用如果超过此限制，将返回 `ENOSPC` 错误。

### semmap

指定用于在共享内存中分配新的 System V IPC 信号量的空闲空间资源映射的大小。

可接受的值：
- 最小值：`4`
- 最大值：内存限制
- 默认值：`SemMIN+2`

指定整数值或使用整数公式表达式。

描述

按标识符分配的每组信号量占据 sem 数组中的一个或多个连续插槽。随着信号量的分配和释放，sem 数组可能会变得碎片化。

`semmap` 维度是显示 sem 数组中空闲孔洞的资源映射。此映射中的一个条目用于指向每套未分配的连续插槽；该条目包括指向该套的指针以及该套的大小。

如果信号量使用率高且无法容纳信号量组的请求，则会出现以下消息：

> danger: mfree map overflow

此时应使用较大的 `semmap` 值配置新的内核。

如果所有信号量标识符具有相同数量的信号量，则 sem 数组的碎片化会减少；此时 `semmap` 可以稍小一些。

四是最小限制：1 个插槽是映射的开销，第二个插槽在系统初始化时始终需要用来显示 sem 数组是空闲的。

### semume

定义给定进程可以拥有挂起取消操作的 IPC 信号量的最大数量。

可接受的值：
- 最小值：`1`
- 最大值：`SemMNS`
- 默认值：`10`

指定整数值。

描述

!!undo!! 是信号量操作中的一个特殊、可选标志，如果调用该操作的进程终止，则导致该操作被撤销。




`“semume”` 指定了任何给定进程上可以挂起的最大半程量（semaphore undo）数量。

`“semmp”` 是可以通过一次系统调用修改的最大信号量数量。该值在文件 `/usr/include/sys/sem.h` 中指定。

使用 `SEM_UNDO` 标志的 `“semop()”` 系统调用如果在超出 `“semume”` 限制时，将返回一个 `“EINVAL”` 错误。

## semvmx

指定信号量值的最大可能值。

可接受值：

- 最小值：`“1”`
- 最大值：`“65535”`
- 默认值：`“32767”`

指定整数值。

### 描述

`“semvmx”` 指定了信号量可以具有的最大值。此限制不得超过能存储在 16 位无符号整数中的最大数值，否则可能会发生未检测到的信号量溢出。

任何试图将信号量值增加到大于 `“semvmx”` 的 `“semop()”` 系统调用都会返回一个 `“ERANGE”` 错误。如果 `“semvmx”` 大于 `65535`，信号量值可能会溢出而未被检测到。

`“semop”` 是可以通过一次系统调用修改的最大信号量数量。该值在文件 `/usr/include/sys/sem.h` 中指定。

## sema

在系统启动时启用或禁用内核中的 System V IPC 信号量支持（仅限 700 系列）。

最大值：`1`（在内核中包含 System V IPC 信号量代码）
默认值：`1`

指定 `0` 或 `1` 的整数值。

### 描述

`sema` 确定 System V IPC 信号量代码是否在系统启动时包含在内核中（仅限 700 系列系统）。

- `sema` = 1 代码包含在内核中（启用 IPC 共享内存）。
- `sema` = 0 代码未包含在内核中（禁用 IPC 共享内存）。

800 系列系统：内核中始终启用 IPC 共享内存。

700 系列系统：如果 `shmrem` 设置为零，则忽略所有其他 IPC 共享内存参数。

Starbase 图形库和其他一些 HP-UX 子系统使用信号量。只有当您确定系统上没有应用程序依赖 System V IPC 信号量时，才应禁用。

如果 `sema` 为零，任何使用 `semget()` 或 `semop()` 系统调用的程序都将返回一个 `SIGSYS` 信号。

## semaem

定义信号量值可以通过信号量 `undo` 操作改变的最大幅度。

可接受值：

- 最小值：`0`
- 最大值：`SEMVMX` 或 32767，取较小者
- 默认值：`16384`

指定整数值或整数公式表达式。

### 描述

`undo` 是信号量操作中的一个可选标志，如果调用该操作的进程终止，该操作将被撤销。

`semadn` 指定信号量的值可以通过 undo 操作改变的最大幅度。

undo 值是按进程累加的，因此如果一个进程对某个信号量有多个 undo 操作，则每个 undo 操作的值会被相加，总和存储在名为 `semadi` 的变量中。`semadi` 随后包含当进程终止时信号量将被递增或递减的数值。

## sendfile_max

`sendfile_max` 定义了在任何给定时间通过 `sendfile()` 系统调用传输的最大缓冲区缓存页数。

可接受值：

- 最小值：`0`
- 最大值：`0x40000`
- 默认值：`0`

指定整数值。

### 描述

`sendfile_max` 限制了在任何给定时间 `sendfile()` 系统调用可以独占的缓冲区缓存页数。`sendfile()` 是 Web 服务器使用的系统调用，用于避免使用 `send()` 系统调用将数据从用户空间复制到内核空间所带来的开销。在网络传输期间，网络软件直接使用缓冲区缓存，当数据在链路上传输时。通常这是一个非常短的时间段，但在通过慢速链路发送数据或因错误而重传时，传输期间的持续时间可能会比平时长得多。

`sendfile_max` 通过限制 sendfile 在任何给定时间可以访问的缓冲区缓存内存量，防止 `sendfile()` 锁定所有可用的缓冲区缓存。

`sendfile_max` 是任何给定时间通过 sendfile 传输的缓冲区缓存页数的上限。最小值零意味着对缓冲区数量没有限制。其他任何值都将缓冲区缓存访问限制为指示的页数。默认值为 0。

将 `sendfile_max` 设置为 `1` 实际上意味着没有可用的缓冲区。每个缓冲区至少是一页，该值防止任何访问，因为第一个缓冲区空间请求将超过上限，迫使 `sendfile()` 回退到使用 `malloc()` 和数据复制操作，这是 `send()` 系统调用的行为。

将 `sendfile_max` 设置为任何小于 0x40000 的其他值，允许管理员保护系统，以防在正常系统操作期间缓冲区可用性成为问题时，`sendfile()` 占用过多的缓冲区。

## shmem

在系统启动时启用或禁用内核中的 System V IPC 共享内存支持（仅限 700 系列）。

可接受值：

- 最小值：`0`（从内核中排除 System V IPC 共享内存代码）
- 最大值：`1`（在内核中包含 System V IPC 共享内存代码）
- 默认值：`1`

指定 `0` 或 `1` 的整数值。

### 描述

`shmem` 确定 System V IPC 共享内存代码是否在系统启动时包含在内核中（仅限 700 系列系统）。

- `shmem` = `1`
代码包含在内核中（启用 IPC 共享内存）。
- `shmem` = `0`
代码未包含在内核中（禁用 IPC 共享内存）。

800 系列系统：内核中始终启用 IPC 共享内存。

700 系列系统：如果 `shmem` 设置为零，则忽略所有其他 IPC 共享内存参数。

何时禁用共享内存

某些子系统，如 Starbase 图形，需要共享内存。其他子系统，如 X Windows，如果可用则使用共享内存（通常大量使用）进行服务器-客户端通信，否则使用套接字。如果内存空间非常紧张，且此类应用程序可以在没有共享内存的情况下运行（尽管速度较慢），您可能更喜欢在没有启用共享内存的情况下运行。

## shmmax

指定系统范围内允许的最大共享内存段大小。

可接受值：

- 最小值：`2048`（2 KB）
- 最大值：32 位系统上的 `1 GB`
- 最大值：64 位系统上的 `4 TB`
- 默认值：`0x04000000`（64 MB）

指定整数值。

### 描述

`“shmmax”` 定义了系统范围内允许的最大共享内存段大小（以字节为单位）。任何请求大于此限制的段的 `“shmidc()”` 系统调用都会返回错误。

使用的值不能超过最大可用交换空间。对于任何给定系统的最小值、最大值和默认值，请参阅 `/etc/conf/master.d/*` 文件中的值。

可以通过重新构建内核来设置 `“shmmax”`，或者通过 `“setnum”` 在运行的内核中设置。`“SAM”` 和 `“kmtune”` 使用 `“setnum()”`。

`“shmmax”` 仅在新的共享内存段创建时进行检查。动态更改此参数只会限制在调用 `“setnum()”` 之后创建的共享内存段的大小。

## shmmni

指定系统范围内允许的最大共享内存段数量（通过限制段标识符的数量）。

可接受值：

- 最小值：`3`
- 最大值：`(受内存限制)`
- 默认值：`200` 个标识符

指定整数值。

### 描述

`shmmin` 指定了允许同时存在的最大共享内存段数量（系统范围）。当已经存在 `shmni` 个段时，任何请求新段的 `shmget()` 系统调用都会返回错误。此参数定义了存储在不可交换内核空间中的共享内存段标识符列表中的条目数量。

将 `shmmin` 设置为任意大的数字会浪费内存并可能降低系统性能。在内存配置较小的系统中，将此值设置得太高可能会消耗足够的内存空间，导致系统无法启动。为了获得最佳内存使用率，请选择尽可能接近实际系统需求的值。除非系统需求另有规定，否则建议选择不超过 1024 的值。

Starbase 图形要求 `shmmin` 设置不得小于 4。

## shmseg

定义可以同时附加到单个进程的最大共享内存段数量。

可接受值：

- 最小值：`1`
- 最大值：`shmmin`
- 默认值：`120`

指定整数值。

### 描述

`shmseg` 指定了在任何给定时间可以附加到进程的共享内存段的最大数量。任何超出此限制的 `shmat()` 调用都会返回错误。

- `shmseg` 可以通过重新构建内核来设置，或者通过 `setune()` 在运行的内核中设置。`SAM` 和 `kmtune` 使用 `setune()`。
- `shmseg` 仅在将段附加到进程时，在 `shmat()` 中进行检查。动态更改此参数只会影响未来对 `shmat()` 的调用。现有的共享内存段将不受影响。

## STRCTL5Z

设置系统上任何流消息控制部分中允许的最大控制字节数。





## STRICTLSZ

设置系统中任意流消息中允许的最大控制数据字节数。

可接受的值：
- 最小值：0
- 最大值：受内存限制
- 默认值：1024 字节

指定整数值。

### 描述

此参数限制了 `putmsg()` 可以在系统中任何流消息的控制部分插入的控制数据字节数。如果该参数设置为零，则对可以放置在消息控制段中的字节数没有限制。

如果发送的缓冲区大于 `STRICTLSZ` 的当前值，`putmsg()` 将返回 `ERANGE`。

## STRMSGSZ

设置系统中任意流消息中允许的最大数据字节数。

可接受的值：
- 最小值：0
- 最大值：受内存限制
- 默认值：8192 字节

指定整数值。

### 描述

此参数限制了 `putmsg()` 或 `write()` 可以在系统中任何流消息的数据部分插入的数据字节数。如果该参数设置为零，则对可以放置在消息数据段中的字节数没有限制。

如果发送的缓冲区大于 `STRMSGSZ` 的当前值，`putmsg()` 将返回 `ERANGE`；`write()` 会将数据分段为多个消息。

## streampipes

强制所有管道基于流。

可接受的值：
- 最小值：0
- 最大值：1
- 默认值：0

指定整数值。

### 描述

此参数确定由 `pipe()` 系统调用创建的管道类型。如果设置为默认值零，则由 `pipe()` 创建的所有管道都是普通的 HP-UX 文件系统管道。如果值为 1，`pipe()` 将创建基于流的管道，并且可以将模块推入结果流中。

如果此参数设置为非零值，则必须在文件 `/stand/system` 中配置 `pipemod` 和 `pipedev` 模块和驱动程序。

## swchunk

指定用于交换的块大小。

可接受的值：
- 最小值：2048
- 最大值：65536
- 默认值：2048

指定整数值。

除非您需要配置超过 32Gb 的交换空间，否则请使用默认的 2048 值。在更改此参数之前，请查看 `maxswapchunks` 的帮助。

### 描述

`swchunk` 定义交换的块大小。此值必须是 2 的整数次幂。

交换空间以块的形式分配，每个块包含 `swchunk` 个大小为 `DEV_BSIZE` 字节的块。当系统需要交换空间时，从一个设备或文件系统中获取一个交换块。当该块被使用且需要另一个块时，从不同的设备或文件系统中获取一个新的块，从而将交换使用分布在几个设备和/或文件系统中，以提高系统效率并最小化交换系统对特定设备的独占。

## swapmen_on

启用伪交换保留。

可接受的值：
- 最小值：0（禁用伪交换保留）
- 最大值：1（启用伪交换保留）
- 默认值：1

指定 0 或 1 的整数值。

### 描述

"swapmen_on" 启用或禁用伪交换保留，伪交换是指除了磁盘上的设备交换空间之外，被视为可用虚拟内存空间的系统内存中的空间。默认情况下，伪交换是启用的。

虚拟内存（交换）空间通常从系统磁盘上的设备交换区域分配。然而，在安装了大量 RAM 和大磁盘或磁盘阵列的系统中，可能存在不受分配的设备交换空间限制更有利的情况。

例如，考虑一个在单用户模式下运行的管理员，该系统安装了 200 Mbytes 的 RAM，其中只有 20 Mbytes 被内核使用，并且根磁盘阵列上有 1 Gbyte 的交换区域。假设有一个正在运行的进程需要 1.1 Gbytes 的交换空间。由于没有其他用户进程在系统上运行，通过交换系统提供对未使用 RAM 的访问将提供足够的交换空间。"swapmen_on" 实现了这一点。

工作站和较小系统的大管理员可能根据系统和用户需求，更喜欢禁用此功能。

## timeslice

调度时间片间隔。

可接受的值：
- 最小值：-1
- 最大值：+2147483647（约 8 个月）
- 默认值：+10（10 个 10 毫秒时钟滴答）

指定整数值或使用整数公式表达式。

### 描述

"timeslice" 间隔是一个进程在 CPU 被给予相同优先级的下一个进程之前被允许运行的时间量。"timeslice" 的值以 (10 毫秒) 时钟滴答为单位指定。有两个特殊值：
- "0"：使用系统默认值（当前为 10 个 10 毫秒时钟滴答，或 100 毫秒）。
- "-1"：完全禁用轮询调度。

### 对系统的影响

"timeslice" 施加时间限制，当该限制到期时，强制进程检查待处理的信号。这保证任何不进行系统调用的进程都可以被终止（例如无限循环中的失控进程）。将 "timeslice" 设置为非常大的值或 -1，允许此类进程在检查信号的情况下继续运行，从而导致系统性能瓶颈或系统死锁。

除非需要具有特定实时需求的系统应用程序使用不同的值，否则请使用 "timeslice" 的默认值。

此参数不涉及内存分配。在每个时间片间隔都会花费一些 CPU 时间，但此时间尚未精确测量。

## timezone

指定从协调世界时向西到当地时区的时间延迟。

可接受的值：
- 最小值：-720
- 最大值：+720
- 默认值：+420

指定整数值。

### 描述

"timezone" 指定从协调世界时向西到系统所在地当地时区的时间延迟（以分钟为单位）。负值解释为从协调世界时向东的分钟数。该值存储在 "/usr/include/sys/time.h" 中定义的结构中，如下所示：

```c
struct timezone tz = { TimeZone, DST };
struct timezone {
int tz_minuteswest;/* minutes west of Greenwich */
int tz_dsttime; /* type of dst correction */
};

#define DST_NONE 0 /* not on dst */
#define DST_USA 1 /* USA style dst */
#define DST_AUST 2 /* Australian style dst */
#define DST_WET 3 /* Western European dst */
#define DST_EET 5 /* Eastern European dst */
```

## ulockable_mem

指定应保留用于系统开销和虚拟内存管理使用的最小内存量。

可接受的值：
- 最小值：0
- 最大值：电源启动时指示的可用内存
- 默认值：0（系统设置为适当的值）

指定整数值。

### 描述

"ulockable_mem" 定义了始终应保留用于虚拟内存管理和系统开销的最小内存量。增加不可锁定内存的量会减少可锁定内存的量。

以 4-Kbyte 页为单位指定 "ulockable_mem"。请注意，当前可用内存和可锁定内存的量与物理页大小一起列在启动消息中，您可以稍后通过运行 "/etc/dmesg" 查看。

如果 "ulockable_mem" 的值超过可用系统内存，则将其设置为等于可用内存（将可锁定内存减少为零）。

如果需要可锁定内存的任何调用，如果可锁定内存不足，可能会失败。请注意，可锁定内存可用于虚拟内存，除非它被锁定。

## vas_hash_locks

vas_hash_locks 保留用于将来使用。

可接受的值：
- 默认值：128

客户不应尝试更改此参数。

## vmepbn_public_pages

"vmepbn_public_pages" 指定为 VME 从站 I/O 内存映射器保留的 4-Kbyte 页数。

可接受的值：
- 最小值：0
- 最大值：32
- 默认值：1

指定整数值。

### 描述

"vmepbn_public_pages" 指定为 VME 从站 I/O 内存映射器保留的 4-Kbyte 页数。

有关设置可选 VME 子系统的内核参数的更多信息，请参阅 VME 文档。

## vmepbn_sockets

"vmepbn_sockets" 指定 VME 套接字域 "AF_VME_LINK" 是否处于活动状态。

可接受的值：




## vmebpn_sockets

指定 `AF_VME_LINK` 套接字域的可用性。

可接受的值：
- 最小值：`0`（`AF_VME_LINK` 未激活）
- 最大值：`1`（`AF_VME_LINK` 已激活）
- 默认值：`1`（`AF_VME_LINK` 已激活）

指定整数值。

描述

`vmebpn_sockets` 用于启用或禁用 VME 套接字域 `AF_VME_LINK`。

有关设置可选 VME 子系统的内核参数的更多信息，请参考 VME 文档。

## vmebpn_tcp_ip

允许的最大 DLPI PPA 数量。

可接受的值：
- 最小值：`0`
- 最大值：`1`
- 默认值：`1`

指定整数值。

描述

`vmebpn_tcp_ip` 指定系统上允许的最大 DLPI PPA 数量。如果设置为零，则禁用 TCP-IP。否则，最大值为 `1`。

有关设置可选 VME 子系统的内核参数的更多信息，请参考 VME 文档。

## vmebpn_tcp_ip_mtu

`vmebpn_tcp_ip_mtu` 指定 PPA 传输单元中允许的最大千字节数。

可接受的值：
- 最小值：`0`
- 最大值：`64`
- 默认值：`8`

指定整数值。

描述

`vmebpn_tcp_ip_mtu` 指定 PPA 传输单元中允许的最大千字节数。

有关设置可选 VME 子系统的内核参数的更多信息，请参考 VME 文档。

## vmebpn_total_jobs

`vmebpn_total_jobs` 指定在任何给定时间可以打开的 VME 端口的系统范围内最大值。

可接受的值：
- 最小值：`0`
- 最大值：`8096`
- 默认值：`16`

指定整数值。

描述

`vmebpn_total_jobs` 指定在任何给定时间可以打开的 VME 端口的系统范围内最大值。

有关设置可选 VME 子系统的内核参数的更多信息，请参考 VME 文档。

## vme_io_estimate

`vme_io_estimate` 指定内核 I/O 空间中供 VME 子系统使用并需为其分配的 4-Kbyte 页面数量。

可接受的值：
- 最小值：`0`
- 最大值：`0x800`
- 默认值：`0x800`

指定整数值。

描述

`vme_io_estimate` 指定内核 I/O 空间中需分配供 VME 子系统使用的 4-Kbyte 页面数量。

有关设置可选 VME 子系统的内核参数的更多信息，请参考 VME 文档。

## vps_ceiling

指定内核在基于系统配置和对象大小选择页面大小时可选择的最大页面大小（以千字节为单位）。

可接受的值：
- 最小值：`4`
- 最大值：`65536`
- 默认值：`16`

指定整数值。

描述

提供此参数是为了提供一种手段，以最小化在使用具有更小 TLB（转换查找旁路缓冲区）且没有硬件 TLB 查找器的较新 PA-RISC 设备（如 PA-8000）的系统上，由 TLB 未命中导致的丢失周期时间。

如果用户应用程序没有使用 `chartr` 命令来指定程序文本和数据段的页面大小，内核会选择一个基于系统配置和对象大小看起来合适的页面大小。这被称为透明选择。所选大小随后会与系统启动时配置的由 `vps_ceiling` 定义的默认最大页面大小值进行比较。如果该值大于 `vps_ceiling`，则使用 `vps_ceiling`。

该值还会与系统启动时配置的由 `vps_pagesize` 定义的默认最小页面大小值进行比较。如果该值小于 `vps_pagesize`，则使用 `vps_pagesize`。

另外请注意，如果 `vps_ceiling` 指定的值不是合法的页面大小，内核将使用下一个较低的合法值。

有关这些参数的使用方式及其对系统操作的影响的更多信息，请参考题为 *Performance Optimized Page Sizing: Getting the Most out of your HP-UX Server* 的白皮书。

此文档可在万维网上获取：
http://www.unixsolutions.hp.com/products/hpux/pop.html

## vps_chartr_ceiling

指定当用户进程使用 `chartr` 命令指定页面大小时可指定的最大页面大小（以千字节为单位）。

可接受的值：
- 最小值：`4` 千字节
- 最大值：`65536` 千字节
- 默认值：`65536` 千字节

指定整数值。

描述

提供此参数是为了提供一种手段，以最小化在使用具有更小 TLB（转换查找旁路缓冲区）且没有硬件 TLB 查找器的较新 PA-RISC 设备（如 PA-8000）的系统上，由 TLB 未命中导致的丢失周期时间。

## vps_pagesize

指定如果用户应用程序未使用 `chartr` 命令指定页面大小，内核所使用的默认用户页面大小（以千字节为单位）。

可接受的值：
- 最小值：`4`
- 最大值：`65536`
- 默认值：`4`

指定整数值。

描述

提供此参数是为了提供一种手段，以最小化在使用具有更小 TLB（转换查找旁路缓冲区）且没有硬件 TLB 查找器的较新 PA-RISC 设备（如 PA-8000）的系统上，由 TLB 未命中导致的丢失周期时间。

## vxs_max_ra_kbytes

设置内核针对单个 VxFS 文件系统可能拥有的预读数据量（以千字节为单位）的最大值。

可接受的值：
- 最小值：`0`
- 最大值：`65536`
- 默认值：`1024`

指定整数值或使用整数公式表达式。

描述

当从磁盘驱动器读取数据时，系统可能会读取超出操作请求的额外数据。这种“预读”通过预期将读取额外数据并使其在请求之前已在系统缓冲区中可用，从而加速顺序磁盘访问。

此参数限制内核允许针对任何特定 VxFS 文件系统拥有的预读块数量。该限制适用于每个单独的 VxFS 文件系统，而不是系统范围的总和。

## vxs_ra_per_disk

设置每个磁盘驱动器允许的 VxFS 文件系统预读量。

可接受的值：
- 最小值：`0`
- 最大值：`8192`
- 默认值：`1024`

指定整数值或使用整数公式表达式。

描述

当从磁盘驱动器读取数据时，系统可能会读取超出操作请求的额外数据。这种“预读”通过预期将读取额外数据并使其在请求之前已在系统缓冲区中可用，从而加速顺序磁盘访问。

此参数指定每个磁盘驱动器允许的预读量。

预读总量是通过将 `vxs_ra_per_disk` 乘以逻辑卷中的驱动器数量来确定的。如果文件系统不驻留在逻辑卷中，则驱动器数量实际上为一。

内核针对单个 VxFS 文件系统可能拥有的预读总量受 `vxs_max_ra_kbytes` 约束。

## vx_nsize

指定为 VxFS 文件系统使用的目录路径名缓存保留的字节数。

可接受的值：
- 最小值：`0`
- 最大值：无
- 默认值：`1024`

指定整数值。

描述

VxFS 文件系统使用名称缓存来存储与文件系统中最近访问的目录相关的目录路径名信息。从名称缓存中检索此信息使系统能够访问目录及其内容，而无需每次需要查找频繁使用的目录时都使用直接磁盘访问来遍历目录树。以这种方式使用名称缓存可以节省大量开销，特别是在数据库等大型应用程序中，系统会反复访问特定目录或目录路径。

`vx_nsize` 指定为 VxFS 文件系统管理器保留多少空间（以字节为单位）用于此目的。默认值对于大多数典型的 HP-UX 系统来说已经足够，但对于较大的系统或使用大量 VxFS 磁盘 I/O 的应用程序的系 统来说，扩大缓存大小可能会带来一些性能提升。然而，获得的效率很大程度上取决于应用程序使用目录路径的多样性，以及在与 VxFS 文件系统交互过程中花费的总进程时间的百分比。




### 选择内核参数概览

#### 异步 I/O 参数

以下内核参数用于管理异步 I/O 操作。前四个与 POSIX 异步 I/O 操作相关；最后一个涉及进程之间的打开端口以及异步磁盘 I/O 驱动程序：

- "aio_listio_max"：指定在单次 "listio()" 调用中允许进行的 POSIX 异步 I/O 操作的数量。
- "aio_max_ops"：在任何给定时间内，系统范围内允许的 POSIX 异步 I/O 操作的最大数量。
- "aio_physmem_pct"：可用于 POSIX 异步 I/O 操作的系统锁定内存的最大总量百分比。
- "aio_prio_delta_max"：允许在 POSIX 异步 I/O 控制块（"aio_cb"）中的最大优先级偏移量。
- "max_async_ports"：在任何给定时间内，进程可保持打开的通往异步磁盘 I/O 驱动程序的最大端口数。

### 内核恐慌转储的可配置参数

以下参数会影响内核恐慌发生时，系统内存部分被转储到磁盘的操作：

- "alwaysdump"：指定如果发生内核恐慌，要转储的系统内存类别。
- "dontdump"：指定如果发生内核恐慌，不要转储的系统内存类别。
- "intmodmax"：在处理系统崩溃转储数据时，"savecrash" 将处理的内核模块的最大数量。
- "modsmax"："savecrash" 内核模块表的最大大小（以字节为单位），该表包含模块名称及其在文件系统中的位置。

#### 光纤通道内核参数概览

两个内核配置参数涉及光纤通道 SCSI 子系统以及系统处理器与使用光纤通道协议 (FCP) 与其交互的任何外围设备之间的通信。这些参数用于调整默认为支持并发 FCP 读、写和/或控制请求所分配的内存数量和类型。

- "num_tachyon_adapters"
  为 FCP 请求分配的某些内存必须满足特定要求。"num_tachyon_adapters" 参数用于不提供 I/O 虚拟寻址的系统，以便可以分配满足这些要求的内存。您指定的值控制分配的内存类型，并指定系统中基于 Tachyon 的光纤通道适配器的数量。

- "max_fcp_req"
  此参数设置了对 FCP 适配器上允许的并发 FCP 请求数量的限制。默认值 512 个请求可以通过为此参数指定不同的值来更改。并发请求的最佳限制取决于许多因素，例如配置、设备特性、I/O 负载、主机内存以及 FCP 软件难以轻松确定的其他值。

#### 可配置文件系统参数

以下参数控制文件系统管理的各个方面：

### 缓冲缓存组

- "bufpages"
  文件系统缓冲缓存中 4-K 字节的页面数量。

- "dbc_min_pct"
  动态缓冲缓存的最小内存百分比。

- "dbc_max_pct"
  动态缓冲缓存的最大内存百分比。

- "nbuf"
  系统范围内的文件系统缓冲头和缓存缓冲头总数。

### 打开/锁定文件组

- "maxfiles"
  单个进程在任何给定时间可以打开或锁定文件数的软限制。

- "maxfiles_lim"
  单个进程在任何给定时间可以打开或锁定文件数的硬限制。

- "nfile"
  在任何给定时间，系统上可以同时打开的文件的最大数量。

- "nflocks"
  在任何给定时间，系统范围内可供所有进程使用的文件锁的最大总数。

- "ninode"
  可以驻留在内存中的打开 inode 的最大数量。

### 异步写入组

- "fs_async"
  指定将文件系统数据结构同步或异步写入磁盘。

### VxFS（日志）文件系统参数

- "vx_ncsize"
  为 VxFS 目录路径名缓存保留的内存空间

#### 大容量存储内核参数概览

与文件系统性能相关的可配置参数分为以下几类：

- **文件系统缓冲区**：为文件系统缓冲区缓存空间分配系统物理内存资源。
- **打开或锁定文件**：可以同时打开或锁定的文件数量。
- **日志文件系统**：为与 VxFS 文件系统 inode 关联的目录名查找缓存 (DNLC) 分配空间。
- **异步写入**：是否允许对文件系统进行异步写入。

#### 逻辑卷管理器 (LVM) 可配置参数

提供了两个与内核同逻辑卷管理器交互相关的可配置内核参数：

- `maxxgs`：逻辑卷管理器在系统上配置的卷组最大数量。
- `no_lvm_disks`：通知内核系统上不存在逻辑卷的标志。如果设置，则所有文件系统都与系统上的物理磁盘以及物理磁盘边界一致。唯一的例外是当磁盘配置为分区，或者磁盘的一部分保留用于交换和其他非文件系统用途时。

## LVM 操作概览

逻辑卷管理器 (LVM) 是一个子系统，用于管理结构化为逻辑卷而非受限于物理磁盘起止点的文件系统和磁盘存储空间。逻辑卷可以小于其所在的磁盘或磁盘阵列，也可以包含几个磁盘或磁盘阵列的全部或部分。当使用多个磁盘或阵列时，逻辑卷边界不需要与物理磁盘边界一致。

逻辑卷的管理由逻辑卷管理器执行，而不是由内核执行。然而，内核包含系统中每个卷组的数据结构，并且为 LVM 数据结构保留的空间必须足以支持系统中存在的卷组数量。这是通过“maxxgs”内核配置参数完成的。第二个参数“no_lvm_disks”用于在启动时通知内核系统上不存在逻辑卷。这节省了系统必须识别并在启动时激活逻辑卷的工作。

### 卷和组边界

逻辑卷组由一个或多个逻辑卷组成。卷组内的逻辑卷边界可以配置在给定磁盘上的任何位置。然而，单个磁盘设备不能在不同卷组之间共享。配置为用于数据保护的数据冗余独立磁盘阵列 (RAID) 的磁盘阵列被视为单个磁盘设备，并且不能在不同卷组之间共享。任何未配置为 RAID 阵列的阵列中的单个磁盘被视为单独的设备，并且单个设备可以根据管理员的需求分配给任何卷组。

#### 内存分页可配置参数

- `allocate_fs_swapmap`：启用或禁用在调用 `swapon()` 时分配文件系统交换空间，而不是在调用 `malloc()` 时分配交换空间。启用分配可以减少交换空间不足的风险，主要用于高可用性重要的场景。
- `maxswapchunks`：此参数乘以 "svchunk" 再乘以系统块大小值 (`DEV_BSIZE`)，决定了系统范围内可以配置的设备交换和文件系统交换空间的最大总量。
- `nswapdev`：系统范围内可用于设备交换的最大设备数量。请设置为与实际系统配置匹配。
- `nswaps`：系统范围内可用于文件系统交换的最大已挂载文件系统数量。请设置为与实际系统配置匹配。
- `page_text_to_local`：启用或禁用集群客户端上程序文本段到本地交换设备的换页。这会增加加载新内容（文本被写入本地磁盘，而不是稍后丢弃并从服务器重新加载）的内存加载时间，但减少了




#### 可变页大小参数

- *vps_ceiling* 定义如果用户未指定页大小，系统选择的最大页大小。
- *vps_chartr_ceiling* 定义用户使用 *chartr* 命令在程序中可指定的最大页大小。
- *page_size* 定义如果未使用 *chartr* 指定页大小，默认的最低用户页大小。

## 内存分页参数概述

内存分页的可配置内核参数执行与虚拟内存（交换空间）相关的操作规则和限制。它们属于以下类别：

- 系统总交换空间  系统范围内可分配的最大交换空间。
- 设备交换空间  分配在硬盘设备上的交换空间。
- 文件系统交换空间  分配在已挂载文件系统上的交换空间。
- 伪交换空间  使用已安装的 RAM 作为伪交换空间，允许在磁盘设备上的交换空间限制之外分配虚拟内存空间。
- 可变页大小  虚拟内存页的大小可以改变，以在特定应用中提高交换操作的效率。

#### 未记录的内核参数

内核主文件中出现的一些可配置参数未被记录，其中一些对于 SAM 而言未知或不受支持，原因可能有几种：

- 该参数已过时。它在当前的 HP-UX 版本中不再使用，但可能出现在现有的内核配置中。如果 SAM 在当前内核配置中遇到过时参数，它不会在可配置参数列表中显示该参数。它还会在创建用于构建待处理内核的新配置文件时移除该参数。
- 该参数不受 SAM 支持。与时过参数一样，它不会显示在可配置参数列表中，但会保留在新的内核配置文件中，以确保不会因缺少参数而导致故障。
- 该参数由内核配置软件赋值，这通常基于外部因素。所赋的值可能在计算一个或多个其他参数的值时使用。
- 该参数仅供 HP 工厂或支持部门使用。除非 HP 官方支持人员具体指示，否则不应更改默认值。
- 该参数支持过时或即将淘汰的软件。有关如何选择合适的非默认值的信息，请查阅支持该参数的软件附带的文档。

# 第 5 章

# 虚拟分区和设备

## 虚拟分区和设备的背景

在处理虚拟分区时，你“划分”系统，使组件专门用于某个虚拟分区。这样做是为了实现虚拟分区之间的最大隔离，从而最大限度地减少一个虚拟分区对另一个虚拟分区的影响。截至本文撰写时，处于或低于本地总线适配器（LBA）级别的组件都专门用于分区。由于系统布局因型号而异，你需要熟悉系统的布局，以便能够确定系统中组件相对于 LBA 级别的位置。我们将在本章中介绍一些如何确定系统级别的示例。但是，请记住，新系统经常推出，因此示例中可能没有涵盖你的特定系统的内容。

在 LBA 级别之上，系统组件可以在一定程度上共享。正如我们在第 2 章中看到的，CPU 可以*绑定*或*解绑*，这与虚拟分区有关，内存被分割为专门用于虚拟分区的区域，并且系统总线适配器（SBA）可以在虚拟分区之间共享。

在下一节中，我们将查看系统组件及其路径。虽然我们在第 2 章中指定了要添加到虚拟分区的组件，但我们没有仔细查看如何确定系统的组成组件，以便你可以选择将哪些组件用于哪些分区。

表 5-1，取自随本书提供的撕下卡片，描述了在处理 vPar 时指定系统组件的方式。

### 表 5-1 在 vPar 中处理 CPU、I/O 和内存

| 命令 | 描述 |
| :--- | :--- |
| 指定 CPU 资源： | 绑定和未绑定 CPU 的数量：cpu:num<br>CPU 硬件路径：cpu:path<br>最小和最大数量：cpu:[min[:[max]]] |
| CPU 类型： | 绑定：CPU 在 vPar 激活时与虚拟分区绑定。分配在创建 vPar 时完成。最低编号的绑定 CPU 是君主（monarch）。中断由绑定 CPU 处理。<br>未绑定：可以动态重新分配的 CPU。不处理中断。 |
| 指定内存： | 大小 mem:size<br>基址和范围：mem::base:range<br>上述两者的组合。 |
| 指定 I/O： | 使用路径：iopath:[attr1:[attr2[...]]]<br>（有关详细信息，请参阅 man page vparresources）。 |
| 要添加资源请使用：（如果在运行 vparmodify，这会将组件相对于现有内容添加。） | -a cpu:path<br>-a cpu:num<br>[-a cpu:num] [-a cpu:[min[:[max]]] -a cpu:path]（仅限 vparcreate）<br>[-a iopath:[attr1[attr2[...]]]<br>-a mem:size<br>-a mem::base:range |
| 要删除资源请使用： | -d cpu:path<br>-d cpu:num<br>-d iopath:[attr1[att2[...]]<br>-d mem:size<br>-d mem::base:range |
| 要修改资源请使用：（这将其修改为绝对值而非相对值。） | -m cpu:path<br>-m cpu:cpu<br>-m cpu:mem<br>[-m cpu:num][-m cpu:min:mem][-m cpu:path]<br>to io:path:attr[;attr2;...]<br>-m mem:size |

我们将在后续章节中使用与这些组件相关的许多命令，并以表 5-1 中所示的方式指定组件。

### 虚拟分区和本地总线适配器

首先，让我们运行 **ioscan -f** 以生成系统中组件的完整列表：

```
# ioscan -f
```

### N 类

| 类 | I | 硬件路径 | 驱动程序 | 软件状态 | 硬件类型 | 描述 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| root | 0 | | root | CLAIMED | BUS.NEXUS | 系统总线适配器 (803) |
| ioc | 0 | 0/0 | sba | CLAIMED | BUS.NEXUS | 本地 PCI 总线适配器 (782) |
| ba | 0 | 0/0 | lba | CLAIMED | BUS.NEXUS | SGI Ethernet (10110019) |
| lan | 0 | 0/0/0/0 | bclan3 | CLAIMED | INTERFACE | Wide Single-Ended |
| ext_bus | 0 | 0/0/1/0 | c720 | CLAIMED | INTERFACE | SCSI C895 Ultra |
| | | | | | | |
| target | 0 | 0/0/2/0/0/1 | tgt | CLAIMED | DEVICE | HP DVD-ROM 305 |
| disk | 0 | 0/0/3/0/1/0 | mdisk | CLAIMED | DEVICE | |
| target | 1 | 0/0/1/0/7 | tgt | CLAIMED | DEVICE | Initiator |
| ctl | 0 | 0/0/1/0/7/0 | sctl | CLAIMED | DEVICE | SCSI C875 Ultra |
| ext_bus | 1 | 0/0/2/0 | c720 | CLAIMED | INTERFACE | Wide Single-Ended |
| | | | | | | |
| target | 2 | 0/0/2/0/0/6 | tgt | CLAIMED | DEVICE | SEAGATE ST336704LC |
| disk | 1 | 0/0/3/0/0/6 | mdisk | CLAIMED | DEVICE | |
| target | 3 | 0/0/2/0/0/7 | tgt | CLAIMED | DEVICE | Initiator |
| ctl | 1 | 0/0/2/0/7/0 | sctl | CLAIMED | DEVICE | SCSI C875 Ultra |
| ext_bus | 1 | 0/0/3/0 | c720 | CLAIMED | INTERFACE | Wide Single-Ended |
| | | | | | | |
| target | 4 | 0/0/2/1/6 | tgt | CLAIMED | DEVICE | SEAGATE ST336704LC |
| disk | 2 | 0/0/3/1/0/6 | mdisk | CLAIMED | DEVICE | Initiator |
| target | 5 | 0/0/2/1/7 | tgt | CLAIMED | DEVICE | PCI Serial (103c1048) |
| ttf | 2 | 0/0/4/1/7/0 | sctl | CLAIMED | DEVICE | PCI Serial (103c1048) |
| ttf | 0 | 0/0/4/0 | asio0 | CLAIMED | INTERFACE | BUS.NEXUS |
| ttf | 1 | 0/0/5/0 | asio0 | CLAIMED | INTERFACE | 本地 PCI 总线适配器 (782) |
| ba | 1 | 0/1 | lba | CLAIMED | BUS.NEXUS | |




## N 类系统硬件清单

ba 3 0/4 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
lan 1 0/0/0/0 blank CLAIMED INTERFACE HP A5230A/B5509A
ha 4 0/5 lba CLAIMED BUS NEXUS PCI 10/100Base-TX Add-on
ha 5 0/5/0/0 pciToPCI CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
lan 3 0/5/0/0/4/0 blank CLAIMED INTERFACE PCI/PCIoPCI Bridge
lan 4 0/5/0/0/1/0 blank CLAIMED INTERFACE HP A55968 PCI
lan 5 0/5/0/0/6/0 blank CLAIMED INTERFACE 10/100Base-TX 4 port
lan 6 0/5/0/0/7/0 blank CLAIMED INTERFACE HP A55068 PCI
lan 5 0/5/0/0/7/0 blank CLAIMED INTERFACE 10/100Base-TX 4 port
ba 6 0/8 lba CLAIMED BUS NEXUS 10/100Base-TX 4 port
ba 7 0/10 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
ba 8 0/12 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
fcp 0 0/12/10/1 tcd CLAIMED INTERFACE HP Tachyon TS/TS Fibre Channel Mass Storage Adapter
fcp 0 0/12/10/0/0 fcp CLAIMED INTERFACE Channel Mass Storage Adapter
ioa 1 1 sba CLAIMED BUS NEXUS System Bus Adapter (803)
ba 9 1/0 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
ba 10 1/2 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
ba 11 1/4 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
ba 12 1/8 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
ba 13 1/10 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
fcp 1 1/10/10 tcd CLAIMED INTERFACE HP Tachyon TS/TS Fibre Channel Mass Storage Adapter
fcp 1 1/10/10/0/0 fcp CLAIMED INTERFACE Channel Mass Storage Adapter
ba 14 1/12 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
lan 2 0/12/0/0 blank CLAIMED INTERFACE HP A5230A/B5509A PCI
pbc 0 36 pbc CLAIMED BUS NEXUS 10/100Base-TX Add-on
processor 0 37 processor CLAIMED PROCESSOR Processor
pbc 1 44 pbc CLAIMED BUS NEXUS Bus Converter
processor 1 45 processor CLAIMED PROCESSOR Processor
pbc 2 100 pbc CLAIMED BUS NEXUS Bus Converter
processor 2 101 processor CLAIMED PROCESSOR Processor
pbc 3 108 pbc CLAIMED BUS NEXUS Bus Converter
processor 4 109 processor CLAIMED PROCESSOR Processor
memory # 0 192 memory CLAIMED MEMORY Memory

通过这个完整清单，我们可以看到组成该 N 类系统的许多组件。所有设备均处于“已声明（CLAIMED）”状态，这意味着这些设备存在软件驱动程序，且软件已绑定。回顾我们之前关于 LBA 的讨论，我们想知道哪些组件位于哪些 LBA 上，以便规划分区布局。执行以下命令将生成 LBA 和 SBA 的列表：

```bash
# ioscan -f | grep ba N-Class
```

ioa 0 0 sba CLAIMED BUS NEXUS System Bus Adapter (803)
ha 0 0/0 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
ba 1 0/1 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
ba 2 0/2 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
ha 3 0/4 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
ha 4 0/5 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
ha 5 0/5/0/0 pciToPCI CLAIMED BUS NEXUS PCI/PCIoPCI Bridge
ba 6 0/8 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
ba 7 0/10 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
ha 8 0/12 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
ioa 1 1 sba CLAIMED BUS NEXUS System Bus Adapter (803)
ba 9 1/0 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
ha 10 1/2 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
ba 11 1/4 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
ba 12 1/8 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
ba 13 1/10 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)
ba 14 1/12 lba CLAIMED BUS NEXUS Local PCI Bus Adapter (782)

在此 N 类系统中，有两个 SBA，分别由前缀 0 表示第一个 SBA，前缀 1 表示第二个 SBA。SBA 位于 LBA 之上的一级，处于系统级别。列表中每个项目的第一位数字是 SBA，第二位数字是 LBA。截至撰写本文时，位于同一 LBA 上的组件不能与多个虚拟分区共享。例如，在第一个 ioscan（ioscan -f）清单中，两个内部磁盘均位于 0/0/2，即 SBA 0、LBA 0 和 SCSI 总线 2。

让我们将此与我们在本书大部分示例中使用的 L 类系统进行对比，该系统只有一个 SBA 和两个内部 SCSI 总线：

```bash
# ioscan -f | grep ba                 L-Class

cvhxcon3:/ # ioscan -f | grep ba
0         0     0ba    CLAIMED    BUS_NEXUS System Bus Adapter  (803)
ba        0  0/0     2ba    CLAIMED    BUS_NEXUS Local PCI Bus Adapter  (782)
ba        1  0/2    1ba    CLAIMED    BUS_NEXUS Local PCI Bus Adapter  (782)
ba        2  0/2    1ba    CLAIMED    BUS_NEXUS Local PCI Bus Adapter  (782)
ba        3  0/3    1ba    CLAIMED    BUS_NEXUS Local PCI Bus Adapter  (782)
ba        4  0/4    1ba    CLAIMED    BUS_NEXUS Local PCI Bus Adapter  (782)
ba        5  0/5    1ba    CLAIMED    BUS_NEXUS Local PCI Bus Adapter  (782)
ba        6  0/6    1ba    CLAIMED    BUS_NEXUS Local PCI Bus Adapter  (782)
ba        7  0/7    1ba    CLAIMED    BUS_NEXUS Local PCI Bus Adapter  (782)
ba        8  0/10   1ba    CLAIMED    BUS_NEXUS Local PCI Bus Adapter  (782)
ba        9  0/12   1ba    CLAIMED    BUS_NEXUS Local PCI Bus Adapter  (782)
cvhxcon3:/ #
```

尽管这个 L 类系统只有一个 SBA，如上清单中所有总线的前缀 0 所示，但在 LBA 0/0 上有两个 SCSI 总线。内部磁盘通常在这两个不同的 SCSI 总线之间进行镜像。以下清单显示了该 L 类系统中位于两个不同 SCSI 总线上的镜像内部磁盘：

```bash
cvhxcon3:/ # ioscan -f | grep SEA
disk     1  0/0/1/1.0.0   sda1k   CLAIMED   DEVICE   SEAGATE   ST373404LC
disk     2  0/0/1/1.2.0   sda2k  CLAIMED   DEVICE   SEAGATE   ST373404LC
disk     3  0/0/2/0.0.0   sdba1k CLAIMED   DEVICE   SEAGATE   ST373404LC
disk     4  0/0/2/0.2.0   sdba2k CLAIMED   DEVICE   SEAGATE   ST373404LC
```

此清单显示，四个内部磁盘分别位于 **SBA 0**、**LBA 0** 以及 SCSI 总线 **1** 和 **2** 上。截至撰写本文时，由于这些磁盘位于同一 LBA，它们必须处于同一个 vPar 中。

为了将 L 类磁盘所连接的 LBA 以及这两个磁盘分配给 vPar，我们将使用完整的硬件路径 `-i **0/0**` 来将 LBA 分配给虚拟分区，并使用 `-i **0/0/1/1.2.0:boot**` 来指定该虚拟分区的引导磁盘。

内部磁盘并非连接到我们 L 类系统的唯一磁盘。还有一个外部磁盘机箱，我们在上面创建了多个逻辑单元（LUN），它们表现为独立的磁盘驱动器。如果我们运行 `ioscan` 并 `grep` disk，我们会看到其中存在多个此类条目：

```bash
cvhbcon3:/ # ioscan -f | grep disk
disk          0    0/0/1/0.0             sda1k    CLAIMED    DEVICE    HP        DVD-ROM 304
disk          2    0/0/1/1.2.0          sda2k    CLAIMED    DEVICE    SEAGATE ST173404LC
disk          3    0/0/2/0.0.0          sdba1k   CLAIMED    DEVICE    SEAGATE ST173404LC
disk          4    0/0/2/0.2.0          sdba2k   CLAIMED    DEVICE    SEAGATE ST173404LC
disk          7    0/0/0/0.0.0.5.0.0    sdisk    CLAIMED    DEVICE    HP        AS577A
disk         10    0/0/0/0.0.0.5.0.1    sdisk    CLAIMED    DEVICE    HP        AS577A
disk         11    0/0/0/0.0.0.5.0.2    sdisk    CLAIMED    DEVICE    HP        AS577A
disk         12    0/0/0/0.0.0.5.0.3    sdisk    CLAIMED    DEVICE    HP        AS577A
disk         15    0/0/0/0.0.0.5.1.0    sdisk    CLAIMED    DEVICE    HP        AS577A
disk         17    0/0/0/0.0.0.5.2.0    sdisk    CLAIMED    DEVICE    HP        AS577A
disk         18    0/0/0/0.0.0.5.3.0    sdisk    CLAIMED    DEVICE    HP        AS577A
disk          5    0/0/0/0.0.0.4.0.1    sdisk    CLAIMED    DEVICE    HP        AS577A
disk          6    0/0/0/0.0.0.4.0.1    sdisk    CLAIMED    DEVICE    HP        AS577A
disk          8    0/0/0/0.0.0.4.0.2    sdisk    CLAIMED    DEVICE    HP        AS577A
disk          9    0/0/0/0.0.0.4.0.3    sdisk    CLAIMED    DEVICE    HP        AS577A
disk         13    0/0/0/0.0.0.4.1.0    sdisk    CLAIMED    DEVICE    HP        AS577A
disk         14    0/0/0/0.0.0.4.2.0    sdisk    CLAIMED    DEVICE    HP        AS577A
disk         16    0/0/0/0.0.0.4.3.0    sdisk    CLAIMED    DEVICE    HP        AS577A
cvhbcon3:/ #
```

此清单首先显示 DVD-ROM，然后是四个内部磁盘，最后是在外部存储机箱上配置的 14 个 LUN。我们使用其中一个作为 `cable2` 的引导卷。以下 `vparstatus -v` 命令显示了 `cable1` 和 `cable2` 各自的引导磁盘：

![](img/eff8b9287a5f38c5adf538f24aacf29e_349_0.png)

```bash
# vparstatus -v

[Virtual Partition Details]
Name:			cable1
State:			Up
Attributes:		Dynamic,Manual
Kernel Path:		/stand/vmunix
Boot Options:

[CPU Details]
```




## 最小/最大：1/3
**受用户[路径]限制：**
**受监控[路径]限制：** 33
**未绑定[路径]：**

**[I/O 详情]**
0.0
0.0.1.1.2.0 BOOT <--- cable1 的启动磁盘

**[内存详情]**
指定[基地址 /范围]：
(字节) (MB)
总内存 (MB)：1024

**[虚拟分区详情]**
名称：cable2
状态：已启动
属性：动态，手动
内核路径：/stand/vmunix
启动选项：

**[CPU 详情]**
最小/最大：1/3
**受用户[路径]限制：**
**受监控[路径]限制：** 37
**未绑定[路径]：**

**[I/O 详情]**
0.8.0.0.8.0.5.0.0.0, BOOT <--- cable2 的启动磁盘
0.10

**[内存详情]**
指定[基地址 /范围]：
(字节) (MB)
总内存 (MB)：1024

*cable1* 从位于 0.0.1.1.2.0 的内部磁盘启动，*cable2* 从位于 0.8.0.0.8.0.5.0.0.0 的外部磁盘启动。

在使用虚拟分区时，你需要对系统的硬件有良好且扎实的了解，包括总线适配器和磁盘。在撰写本文时，所有与 vPar 相关的工作都在命令行中进行。了解构成你系统的硬件以及如何在命令行中查询这些信息至关重要。

如果你以前未接触过相关设备，可能需要回顾本章末尾的备份材料，以便熟悉设备及相关主题。

### 虚拟分区与处理器

在第 2 章中分配处理器时，我们可以选择将其设为*未绑定*或*绑定*。绑定 CPU 专属于某个 vPar，不能动态地从 vPar 中移除或添加。绑定 CPU 处理 I/O 中断，因此应与 I/O 密集型应用程序配合使用。未绑定 CPU 可以从 vPar 中动态添加和移除。未绑定 CPU 不处理 I/O 中断，因此应与 CPU 密集型应用程序配合使用。处理处理器稍显复杂，因为你有很多选项，其中一些只能在创建 vPar 时执行，其他一些则要求在执行前将 vPar 停止，因此让我们看一下 **vpstatus** 手册页（表 5-2）中的一个表格：

![](img/eff8b9287a5f38c5adf538f24aacf29e_351_0.png)

**表 5-2 添加、删除和修改资源**

| 命令 | 描述 | 在 vPar 运行时完成？ |
| :--- | :--- | :--- |
| 添加资源使用：（如果在运行 **vparmodify**，则相对于现有内容添加组件） | *-a* **cpu**:num | 否 |
| | *-a* **cpu**:num | 是 - 相对值 |
| | [-a **cpu**:num [-a **cpu**: [min] [:max]] [-a **cpu**:path]] **vparcreate** 专用 | |
| | [-a **mem**:size | 否 |
| | *-a* **io**:path [:attr] [,attr2,...]] | 否 |
| 删除资源使用： | *-d* **cpu**:path | 否 |
| | *-d* **cpu**:num | 是 - 相对值 |
| | *-d* **io**:path [:attr] [,attr2,...]] | 否 |
| | *-d* **mem**:size | 否 |
| | *-d* **mem**:base:range | 否 |
| 修改资源使用：（这是将修改为绝对数值而非相对值。） | *-m* **cpu**:num | 是 - 绝对值 |
| | *-m* **cpu**: [min [:max] | 否 |
| | *-m* **io**:path [:attr] [,attr2,...]] | 否 |
| | *-m* **mem**:size | 否 |

表 5-2 表明，在添加、删除和修改与虚拟分区相关的资源时，你有很多选项。虚拟分区提供的灵活性是使用该技术时最令人期望的特性之一。然而，它也是最令人困惑的特性之一。

该表格中嵌入了许多选项。让我们谈谈在创建 vPar 时分配 CPU，因为大多数与 CPU 相关的问题都发生在创建 vPar 时。在撰写本文时，*num* 在某些文档中使用，而 *total* 在其他文档中使用，因此就本讨论而言，*num* 和 *total* 是可以互换的。

*path* 允许你指定用于 vPar 的特定处理器。使用 *path* 会自动分配*绑定*处理器。要将硬件路径 45 处的处理器添加到 vPar，你会使用以下命令：

```bash
-a cpu:45
```

*min* 指的是*绑定* CPU 的最小数量。只有在创建 vPar 并指定 *min* 时，你才能获得 *min* 数量的 CPU，系统会分配*绑定* CPU 的硬件路径。以下命令将为你提供两个*绑定* CPU，其硬件路径由系统定义：

```bash
-a cpu:::2
```

*max* 是*绑定* + *未绑定* CPU 的潜在数量。例如，你可以有两个 *min* 和四个 *max* CPU，这将为你提供两个*绑定*（由 *min* 2 指定）和最多两个*未绑定*（由 *max* 4 指定）。如果有未使用的 CPU，它们将被分配给你的 vPar，从而使总数达到四个。以下命令将提供此数量：

```bash
-a cpu::2:4
```

*num* 是当前*绑定* + *未绑定* CPU 的数量。这与 *max* 描述的潜在数量不同。要通过 *num* 指定总共三个 CPU，其中三个通过 *min* *绑定*，一个在硬件路径 45 通过 *path* 指定，你会使用以下命令：

```bash
-a cpu::3 -a cpu::3 -a cpu:45
```

此命令的一个有趣细节是，要删除我们指定的硬件路径，我们需要按相反顺序发出选项。硬件路径将首先出现，然后是 *min*，最后是 *num*。

在我的 vPar 工作中，最常见的愿望是在所有 vPar 中拥有一定数量的*绑定* *min* CPU，然后根据 vPar 中应用程序的需要移动*未绑定* CPU。例如，当运行 `vparcreate` 时，我们将指定以下内容：

```bash
vparcreate -p cable1 -a cpu:::1:3 -a cpu::1
```

在创建时，*cable1* 将只有一个*绑定* CPU，因为我们指定了 *min* 为 1 且 *num* 为 1。*num* 是*绑定* + *未绑定* CPU 的总数，由于我们为 *num* 指定了 1，我们将获得一个*绑定* CPU。由于 *max* 为 3，我们留出了添加最多两个额外*未绑定* CPU 的空间。如果我们系统中有两个*未绑定* CPU，我们可以使用 `vparmodify` 根据需要将其在 vPar 之间移动。要从 *cable2* 移除两个*未绑定* CPU 并将其添加到 *cable1*，我们将发出以下两个 `vparmodify` 命令：

```bash
vparmodify -p cable2 -m cpu::1        # 将 cable2 从 3 减少到 1
vparmodify -p cable1 -m cpu::3        # 将 cable1 从 1 增加到 3
```

我们首先从 *cable2* 移除两个*未绑定* CPU，然后将其添加到 *cable1*。如果两个*未绑定* CPU 未分配给任何 vPar，我们在将其添加到 *cable1* 之前就不必从 *cable2* 中移除它们。在撰写本文时，*未绑定* CPU 可以在 vPar 启动或停止时移动，但*绑定* CPU 只能在 vPar 停止时移动。

尽管你在指定和修改 CPU 方面有很多选择，但你不需要使用所有这些选择。vPars 就像其他任何系统管理任务一样；保持简单。

让我们现在查看系统中的一些处理器。以下列表显示了在本书中一些早期示例中使用的 L-Class 系统在将其分配给任何 vPar 之前的总 CPU 数量：

```bash
evhdcon> # ioscan -f | grep proc
 processor   0   33   processor CLAIMED     PROCESSOR   Processor
 processor   1   37   processor CLAIMED     PROCESSOR   Processor
 processor   2   97   processor CLAIMED     PROCESSOR   Processor
 processor   3  101   processor CLAIMED     PROCESSOR   Processor
```

此列表中的第三个字段显示了在指定硬件路径时将使用的处理器硬件路径。

将处理器分配给 vPar 后，你希望确认每个 vPar 确实包含你指定数量的处理器。如果我们有两个名为 `cable1` 和 `cable2` 的 vPar，每个都分配了两个绑定处理器，我们可以以多种方式验证我们确实为每个 vPar 分配了两个处理器。首先，我们可以仅检查 `dmesg` 中的处理器部分，如下所示为 `cable1`：

```bash
cvhdcôn3:/ # dmesg | grep proc
 33 processor
 101 processor
 cvhdcôn3:/ #
```

此 `dmesg` 输出证实，我们的 vPar `cable1`（主机名为 `cvhdcôn3`）确实只分配了两个处理器，尽管系统中有四个处理器。

我们还可以通过在 GlancePlus 中运行并选择 `Process List` 屏幕来验证 vPar 中的 CPU 数量，正如我们在图 5-1 中对 `cable1` 所做的那样。



# 图 5-1 GlancePlus 中的 CPU 报告，显示两个处理器

![](img/eff8b9287a5f38c5adf538f24aacf29e_355_0.png)

图 5-1 中的屏幕显示，`*CPU Util*`（CPU 使用率）显示的最大值为 200%，而非系统中存在的四个处理器（若为四个则应显示 400%），这证实我们为 `*cable1*`（主机名 `*cvhdcn3*`）分配了两个处理器。你还可以通过运行 `*top*` 命令来确认 `*cable1*` 中的两个处理器，如图 5-2 所示：

# 图 5-2 top 命令截图，显示 cable1 中的两个处理器

![](img/eff8b9287a5f38c5adf538f24aacf29e_356_0.png)

top 命令清晰地显示了分配给 cable1 的两个 CPU（即图 5-2 中的 CPU 0 和 1）。

### 虚拟分区与内存

在第 2 章分配内存时，你使用了 size（大小）。你也可以像将 hopath 作为 CPU 的 min 和 num 的子集那样，将基地址（base address）和范围（range）作为 size 的子集来指定。我们选择使用 size。表 5-1 显示了与分配和修改内存相关的选项。我们需要执行的第一项操作是查找系统的内存量，以便将其中的一部分分配给 vPars。确定系统内存量有多种方法。以下仅显示了以非 vPars 模式启动标准 HP-UX 时 dmesg 命令中与内存相关的输出：

```
# dmesg

Memory Information:
  MBD / - cal page size = 4096 bytes, logical page size = 4096 bytes
  Physical: 4194304 Kbytes, lockable: 3180924 Kbytes, available: 3655192 Kbytes
```

此列表显示 `*Physical*`（物理）内存为 4GB。你还可以运行 GlancePlus 并选择 `*Memory*`（内存）屏幕。

可以使用 `*m::size*` 轻松为 vPar 指定内存，其中 `*size*` 单位为 MB（兆字节）。要在虚拟分区中指定 2 GB 内存，可以使用选项 `*m::2048*`。

将内存分配给 vPars 后，你希望确认每个 vPar 中确实具有你指定的内存量。你可以通过多种方式验证这一点。首先是在启动虚拟分区时执行 **dmesg**。虚拟分区监视器（Virtual Partitions Monitor）仅启动你指定为虚拟分区一部分的设备。以下示例仅显示了 **dmesg** 针对 `*cable1*` 的与内存相关的输出：

```
# Memory Information:
cvhcon3:/ # page size = 4096 bytes, logical page size = 4096 bytes
  Physical: 2096128 Kbytes, lockable: 1576748 Kbytes, available: 1815620 Kbytes
```

请注意，此输出显示 `*cable1*` 拥有 2 GB RAM，正如创建 `*vPar cable1*` 时指定的那样。这与第 2 章中的示例不同，在该示例中 `*cable1*` 只有 1 GB RAM。这是低级别 vPars 工作原理的一个指示，即在启动时将资源分配给 `*cable1*`，确保只有指定的资源被分配给该 vPar。

我们也可以运行 GlancePlus 并选择 `*memory*` 屏幕来查看与内存相关的信息。以下截图显示了启动标准 HP-UX 而非虚拟分区时的系统总内存，如图 5-3 所示：

# 图 5-3 GlancePlus 中的物理内存，显示系统为 4 GB（非 vPars 模式）

![](img/eff8b9287a5f38c5adf538f24aacf29e_358_0.png)

现在让我们在 GlancePlus 中查看 cable1（主机名 cvhdcn3）的内存。图 5-4 是在系统启动时加载 cable1 时获得的：

![](img/eff8b9287a5f38c5adf538f24aacf29e_359_0.png)

屏幕右下角的 Phys Mem（物理内存）显示为 2 GB，正如我们分配给 cable1 那样。这证实了 dmesg 显示的系统为 4 GB 和 cable1 为 2 GB 的结果。

由于你正在运行多个虚拟分区，因此必须运行多个 HP-UX 内核。特定虚拟分区的内核必须位于分配给该虚拟分区的内存范围内。在 HP-UX 11i 中，内核在内存中的位置由 /usr/con/cfg/map-file 文件指定。此文件中的条目包括内核在内存中将被放置的位置。此行以 Text = LOAD 开头。此文件存在于你拥有虚拟分区的每个文件系统上，并包含相应虚拟分区的内核位置以及其他动态信息。在 HP-UX 11i 的非虚拟分区系统上，此文件也存在并包含 11i 使用的其他信息。关于 HP-UX 11i 内核和虚拟分区的工作方式在第 4 章中涵盖。

### 虚拟分区与局域网

你系统中的局域网（LAN）卡也可以很容易地通过 **ioscan** 进行识别。要仅查看系统中的 LAN 卡列表，我们可以发出以下命令：

```
# ioscan -f | grep lan
lan   0  0/0/0/0        btl an5   CLAIMED   INTERFACE   PCI Ethernet (10110019)
      ~ 1                btl an5   CLAIMED   INTERFACE   PCI A5230A/B5559BA
                                  PCI 10/100Base-TX Addon
lan   3  0/5/0/4/0      btl an   CLAIMED   INTERFACE   PCI 10/100Base-TX 4 port
lan   4  0/5/0/5/0      btl an   CLAIMED   INTERFACE   HP A5506B
                                  PCI 10/100Base-TX 4 port
lan   5  0/5/0/6/0      btl an   CLAIMED   INTERFACE   HP A5506B
                                  PCI 10/100Base-TX 4 port
lan   6  0/5/0/7/0      btl an   CLAIMED   INTERFACE   HP A5506B
                                  PCI 10/100Base-TX 4 port
lan   2  1/2/0/0        btl an5   CLAIMED   INTERFACE   PCI A5230A/B5559BA
                                  PCI 10/100Base-TX Addon
#
```

此系统有七个局域网接口。它具有内置局域网接口、两个附加局域网卡和一个四端口卡。虽然此系统未在我们之前的示例中使用，但我想展示一个具有多种局域网接口的系统列表。

回到我们之前的示例，我们的系统有三个局域网接口，如下面的 **ioscan** 列表所示：

```
cvhdcn3:/ # ioscan -f | grep lan
lan   0  0/0/0/0        btl an   CLAIMED   INTERFACE   HP PCI 10/100Base-TX Core
lan   1  0/10/0/0       btl an   CLAIMED   INTERFACE   HP AS230A/B5509BA PCI 10/100Base-TX Addon
lan   2  0/12/0/0       btl an   CLAIMED   INTERFACE   HP AS230A/B5509BA PCI 10/100Base-TX Addon
cvhdcn3:/> #
```

位于 0/0 的局域网卡已分配给 `*cable1*`，位于 0/10 的卡已分配给 `*cable2*`，如下面的 **vparstatus -v** 列表所示：

```
# vparstatus -v

[Virtual Partition Details]
Name:     cable1
State:    Up
Attributes: Dynamic,Manual
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_360_0.png)

```
Kernel Path: /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max: 1/3
Bound by User [Path]:
Bound by Monitor [Path]: 33
Unbound [Path]:

[IO Details]
0.0 <-- cable1 LAN on 0/0 but not shown
0.0.1.1.2.0 BOOT

[Memory Details]
Specified [Base /Range]:
      (bytes) (MB)
Total Memory (MB): 1024

[Virtual Partition Details]
Name:     cable2
State:    Up
Attributes: Dynamic,Manual
Kernel Path: /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max: 1/3
Bound by User [Path]:
Bound by Monitor [Path]: 37
Unbound [Path]:

[IO Details]
0.8,0.0,0.8,0.5,0.0.0, BOOT
0.10 <-- cable2 LAN

[Memory Details]
Specified [Base /Range]:
      (bytes) (MB)
Total Memory (MB): 1024
# 
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_361_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_361_1.png)

Core I/O 卡上 `*0/0/0/0*` 处的局域网接口并未在 **vparstatus** 输出中明确列出。`*0/0/4/0*` 处的控制台也是此 vPar 的一个隐含组件。这两个组件都是 Core I/O 卡的一部分，我们在 `*cable1*` 的 **vpareccreate** 命令中通过 `-a` `*0/0/0/0*` 参数将其指定为该 vPar 的一部分。

未分配的局域网接口可以通过 **vparmodify** 命令添加到 `*cable1*` 或 `*cable2*`。然而，截至本文撰写时，I/O 组件不能动态添加，vPar 必须处于 `*down*`（关闭）状态才能添加局域网或任何其他 I/O 组件。但是，你可以使用组件的在线更换和添加（OLAR）功能来操作 vPars 中的组件。例如，如果你将一个 I/O 路径分配给某个 vPar，然后在该 I/O 插槽中物理添加一个组件，那么该组件将成为 vPar 的一部分。

### 虚拟分区与控制台

你可以为每个虚拟分区设置专用的物理控制台。这意味着要为每个虚拟分区分配一个串行端口。或者，你的虚拟分区可以使用虚拟控制台。虚拟控制台（Virtual CoNsole）驱动程序 vcn 处理与虚拟控制台相关的 I/O。如图 5-5 所示，vcn 与虚拟分区监视器通信。虚拟分区监视器缓冲与虚拟控制台相关的 I/O，直到其可以由虚拟控制台从属设备（Virtual Console Slave, vcs）处理。所有 vPars 都使用虚拟控制台，并且物理控制台作为 I/O 规范的一部分分配给其中一个 vPar。





![](img/eff8b9287a5f38c5adf538f24aacf29e_363_0.png)

**图 5-5 虚拟分区和控制台**

图 5-5 中最左侧的虚拟分区被分配了一个物理端口作为控制台。其他分区使用 $vcn$ 驱动程序。这些虚拟分区中与控制台相关的信息通过 $vcn$ 驱动程序传输到虚拟分区监视器。然后，监视器与最左侧分区上的 $vcs$ 驱动程序进行通信。你可以使用该分区上的控制台来访问其他分区的控制台。

如果未定义硬件控制台端口，*vcn* 驱动程序会自动使用，因此不需要进行配置。在本书各示例中的物理控制台，是在将核心 *I/O* 卡包含在某个 *vPar* 中时指定的。

你无需进行任何控制台设置即可使用虚拟控制台。当你创建一个 *vPar* 并指定将 *0/0* 处的核心 *I/O* 卡添加到该 *vPar* 时，控制台会自动在该 *vPar* 中为你创建。对于内置的核心 *I/O* LAN 卡也是如此。但是，引导设备必须明确指定其路径，并在路径后加上 *:* *BOOT*。

然后你可以使用 *Ctrl-A* 在任意数量的 *Virtual Partitions*（虚拟分区）之间切换。*Virtual Partition Monitor*（虚拟分区监视器）会缓冲所有发送到控制台的数据。当你按下 *Ctrl-A* 切换到下一个 *vPar* 时，已为所切换到的 *vPar* 缓冲的控制台信息会被发送到控制台。

图 5-6 展示了使用控制台查看主机名为 *cvhdccon3* 的 *cable1* 的情况。发出 *Ctrl-A* 连接到主机名为 *cvhdccon4* 的 *vPar cable2*。当你在控制台中发出 *Ctrl-A* 切换到下一个 *vPar* 时，系统会在方括号内提供你已连接到的 *vPar* 的名称，例如 *[cable1]*。

![](img/eff8b9287a5f38c5adf538f24aacf29e_365_0.png)

**图 5-6 使用 $Ctrl$-A 在 vPars 之间切换的控制台显示**

除了使用控制台在 vPar 之间切换外，你还可以使用配置在相应 vPar 中的 $LAN$ 网卡来开启到 vPar 的 $TELNET$ 或其他类型的会话。这是与通过网络连接任何系统相同的技术，也是你始终希望将 $LAN$ 网卡配置为每个 vPar 一部分的主要原因之一。

### 在虚拟分区中添加和删除设备

我们之前关于虚拟分区所做的多数工作都是静态的；也就是说，我们配置了具有特定组件的虚拟分区，并验证了配置。我们也可以在虚拟分区中添加和删除设备。在第 2 章中，我们将一个未绑定的 CPU 分配给 vPar *cable1*。让我们回顾一下这个过程，我们同样可以将其应用于磁带驱动器和其他设备。

在即将给出的示例中，有一个四处理器系统，上面有我们刚刚创建的两个虚拟分区：*cable1* 和 *cable2*。每个 vPar 都有一个在创建 vPar 时由 *min* 分配的已绑定 CPU。让我们运行 **vparstatus** 来查看构成这两个虚拟分区的组件，并确认每个都有一个已绑定 CPU：

```bash
# vparstatus -p cable1 -v

[Virtual Partition Details]
Name:          cable1
State:         Up
Attributes:    Dynamic,Manual
Kernel Path:   /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max:       1/3
Bound by User [Path]:
Bound by Monitor [Path]: 33     <-- one bound CPU @ 33
Unbound [Path]:

[IO Details]
     0.0.0
     0.0.1.1.2.0    BOOT

[Memory Details]
Specified [Base  /Range]:
                (bytes) (MB)
Total Memory (MB): 1024
#
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_366_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_366_1.png)

```bash
# vparstatus -p cable2 -v

[Virtual Partition Details]
Name:	cable2
State:	Up
Attributes:	Dynamic, Manual
Kernel Path:	/stand/vmunix
Boot Opts:

[CPU Details]
Min/Max:	1/3
Bound by User [Path]:
Bound by Monitor [Path]:	37	<-- one CPU in use at 37
Unbound [Path]:

[IO Details]
0.8.0.0.8.0.5.0.0.0	BOOT
0.10

[Memory Details]
Specified [Base	/Range]:
		(bytes)	(MB)
Total Memory (MB):	1024
#
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_367_0.png)

这两个 **vparstatus** 命令的输出显示 *cable1* 有一个已绑定 CPU，*cable2* 也有一个已绑定 CPU。在这些 vPar 被创建的 L-Class 系统上，总共有四个 CPU。这意味着应该有两个 CPU 可用。让我们运行 **vparstatus -A** 来查看系统上的可用组件：

```bash
# vparstatus -A
[Unbound CPUs (path)]:	97
				101
[Available CPUs]:	2

[Available I/O devices (path)]:	0.1
0.2
0.3
0.4
0.5
0.9
0.12
32
36
```

```text
          96
         100

[Unbound memory (Base  /Range)]:  0x0/64
                (bytes) (MB)     0xc000000/1856
                                 0x18000000/128

[Available memory (MB)]:   2048
#
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_368_0.png)

此输出证实有位于硬件路径 97 和 101 的两个 CPU 可用。我们可以通过多种方式来添加这些 CPU。让我们使用 **varmodify** 命令将 *cable1* 中的 *num* CPU 数量更改为两个 CPU。我们通过使用 *-a* 在当前 CPU 数量的基础上 *添加* 一个来实现这一点。这是一个相对操作，即会在当前 CPU 数量的基础上增加一个 CPU。如果你想指定 vPar 的绝对 CPU 数量而不是相对数量，可以使用 **varmodify -m**。以下展示了该 **varmodify** 命令：

```bash
# varmodify -p cable1 -a cpu::1
#
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_368_1.png)

现在我们可以运行 **vparstatus -p cable1 -v** 来确认 CPU 已添加，如下列清单所示：

```bash
# vparstatus -p cable1 -v

[Virtual Partition Details]
Name:          cable1
State:         Up
Attributes:    Dynamic,Manual
Kernel Path:   /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max:   1/3
Bound by User [Path]:
Bound by Monitor [Path]:  33    <-- original CPU @ 33
Unbound [Path]:   97           <-- unbound CPU @ 97
[IO Details]
     0.0
     0.0.1.1.2.0  BOOT
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_369_0.png)

```text
[Memory Details]

    Specified [Base /Range]:
    (bytes)(MB)

Total Memory (MB) : 1024
```

vparstatus 的输出显示，位于硬件路径 97 的 CPU 确实已通过 varmodify 命令添加到 cable1 中。

此外，我们可以运行 GlancePlus 或 top 来确认 cable1 上有两个 CPU 正在使用。以下是在 cable1 上运行的 top 输出：

![](img/eff8b9287a5f38c5adf538f24aacf29e_369_1.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_369_2.png)

```bash
# top

System: cvcub0002                         Thu Oct 4 15:30:42 2001

Load averages: 0.19, 0.51, 0.62
124 processes: 110 sleeping, 14 running

Cpu states:

      CPU LOAD USER NICE SYS IDLE BLOCK SWAIT INTR SSYS
      0  0.37 0.03 0.23 0.01 99.5% 0.0% 0.0% 0.0% 0.0%
      1  0.02 0.0% 0.0% 0.0% 99.9% 0.0% 0.0% 0.0% 0.0%
      avg 0.19 0.0% 0.2% 0.4% 99.4% 0.0% 0.0% 0.0% 0.0%

Memory: 93636K (57E16K) real, 322124K (239363K) virtual, 746264K free PageS 1/4
```

```text
CPU TT% PRID USER   PRI NI  SZ   RSS    STATE   TIME       %CPU COMMAND

C     0   PID   USER    PR  NI VIRT    RES    SHR  S  %CPU  %MEM   TIME+   COMMAND
?     1   root    20   0   152  20  4K     832K   run   8:00  0.33  0.31  vceld
?     1   PID     USER   PRI  NI  SZ     RSS    STATE   TIME      %CPU    COMMAND
?     1   1442    root   150  20  80K    212K   sleep   0:10  0.22  0.22  ccdagd
?     7   522     root   154  24  4464K  7260K  run     0:56  0.21  0.21  promd
?     7   3114    root   146  24  556K   528K   run     0:50  1.17  0.15  lgtmrd
?     1   3114    root   146  24  596K   88K    sleep   0:00  0.00  0.01  lgtmrd
?     1   254     root   146  24  556K   528K   run     0:21  0.17  0.15  lgtmrd
?     1   3172    root   152  20  1476K  2356K  run     0:01  0.10  0.02  smand
?     1   254     root   146  24  44K    42K    sleep   0:11  0.02  0.02  jinitd
?     1   1372    root   152  20  44K    204K   sleep   0:00  0.02  0.02  jinitd
?     1   1372    root   152  20  44K    204K   sleep   0:00  0.02  0.02  jinitd
?     2   32      root   147  20  0K     32K    sleep   0:00  0.02  0.02  uweashtpd
?     2   4       root   154  20  0K     32K    sleep   0:00  0.02  0.02  uweashtpd
?     7   312     root   147  20  152K   204K   sleep   0:00  0.02  0.02  wycd
?     7   342     root   147  20  204K   32K    sleep   0:00  0.02  0.02  wycd
?     7   313     root   154  20  76K    152K   sleep   0:00  0.02  0.02  wpad
?     7   4345    root   154  20  156K   216K   sleep   0:00  0.02  0.02  rpc.statd
?     7   520     root   154  20  80K    224K   sleep   0:00  0.02  0.02  rpc.lockd
?     7   446     root   154  20  166K   216K   sleep   0:00  0.02  0.02  rpc.rquotad
?     7   558     root   154  20  704K   4120K  sleep   0:00  0.02  0.02  rpc.mountd
?     7   18      root   154  20  18K    316K   sleep   0:00  0.02  0.02  intld
?     7   863     root   154  20  72K    712K   sleep   0:00  0.02  0.02  sendmail:
?     7   830     root   154  20  552K   352K   sleep   0:00  0.02  0.02  mib2agt
?     7   91      root   154  24  4444K  1840K  sleep   0:00  0.02  0.02  ccmqsd
?     7   303     root   154  24  512K   180K   sleep   0:00  0.02  0.02  qd
?     7   1199    root   154  20  204K   316K   sleep   0:00  0.02  0.02  gwared
?     7   1149    root   154  20  108K   428K   sleep   0:00  0.02  0.02  digmonsd
?     7   1039    root   154  20  2588K  1624K  sleep   0:00  0.02  0.02  perfld
?     7   1156    root   154  20  2588K  1572K  sleep   0:00  0.02  0.02  perfld
?     7   1167    root   154  20  2588K  1572K  sleep   0:00  0.02  0.02  tids
```




## 在虚拟分区中添加和移除设备

该输出显示 *cable1* 中标记为 0 和 1 的两个 CPU。由于 *cable1* 的主机名是 *cvhdc0n3*，因此输出中显示了 *cvhdc0n3* 的 *System* 名称。

虽然这是一个展示如何修改虚拟分区的简单示例，但它也展示了 vPar 的强大功能。当系统上的两个 vPar 都在运行时，可以在一个或两个 vPar 中添加处理器，而不会中断正在运行的程序。

![](img/eff8b9287a5f38c5adf538f24aacf29e_370_0.png)

请注意，**vpmodify** 的 *-a* 选项将 CPU 数量*相对*于当前数量进行了更改。在我们的例子中，当前的 CPU 数量为 1，使用 *-a cpu:1* 在当前数量 1 的基础上添加了 1 个 CPU，结果得到 2 个 CPU。当我们使用 **vpmodify** 的 *-d* 选项移除处理器时，情况也相同。以下示例展示了运行 **vpstatus** 以查看两个 CPU，使用 **vpmodify** 将 CPU 数量改回 1（这也是相对于当前 CPU 数量 2 的相对值），并通过 **vpstatus** 确认此更改已生效：

![](img/eff8b9287a5f38c5adf538f24aacf29e_370_1.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_370_2.png)

```bash
# vpstatus -p cable1 -v

[Virtual Partition Details]
Name:          cable1
State:         Up
Attributes:    Dynamic, Manual
Kernel Path:   /stand/vmunix
Boot Options:

[CPU Details]
Min/Max:   1/3
Bound by User [Path]:
Bound by Monitor [Path]: 33        <-- bound CPU @ 33
Unbound [Path]:          97       <-- unbound CPU @ 97

[IO Details]
      0.0
      0.0.0.0
      0.0.1.1.2.0     BOOT
      0.0.4.0         CONSOLE

[Memory Details]
Specified [Base /Range]:
Bound  (bytes)         (MB)

Total Memory (MB):  1024
# vpmodify -P cable1 -d cpu:1
# vpstatus -p cable1 -v
```

```
[Virtual Partition Details]
Name:          cable1
State:         Up
Attributes:    Dynamic, Manual
Kernel Path:   /stand/vmunix
Boot Options:

[CPU Details]
Min/Max:   1/3
Bound by User [Path]:
Bound by Monitor [Path]: 33        <-- original CPU @ 33
Unbound [Path]:                   <-- no unbound CPUs

[IO Details]
      0.0
      0.0.0.0
      0.0.1.1.2.0 BOOT
      0.0.4.0 CONSOLE

[Memory Details]
Specified [Base /Range]:
                (bytes) (MB)
Total Memory (MB):   1024
#
```

我们可以利用可用的两个*未绑定* CPU 对 vPar 进行许多其他修改，例如向其中一个 vPar 添加两个 CPU，或者向每个 vPar 各添加一个 CPU。

在使用 *vparmodify* 时，请记住组件的相对特性，并且在撰写本文时，某些更改，例如修改内存或添加 I/O 组件，要求 vPar 处于关闭状态。

以下部分提供了一些关于 HP-UX 11i 中设备文件的一般背景知识。如果你之前很少在 HP 系统上处理设备文件，建议复习一下本章中非 vPar 特定的部分。

![](img/eff8b9287a5f38c5adf538f24aacf29e_371_0.png)

## 章节的非 vPar 特定部分 - 设备文件和外设背景知识

HP-UX 会在系统启动时为其发现的大多数连接设备创建特殊文件。不过，你可能需要自己创建设备文件，或者至少需要理解系统中存在的一些设备文件，因此本章中的信息对于每位系统管理员来说都至关重要。典型的安装将包括终端、打印机、磁带驱动器、DVD 驱动器等。一些设备是“标准的”，意思是它们是 HP 产品或由 HP 官方支持的第三方产品。然而，你必须小心，因为看似应该能工作的设备最终可能无法工作，也可能不受支持。几乎总是可以找到一种方法最终让设备工作，但请留意你添加的不受支持的设备，它们可能会给你带来麻烦。

当你向系统添加额外外设时，你必须手动添加设备文件或使用 SAM 为你创建它们。你添加的大多数设备都可以通过 SAM 添加。我发现添加外设很像设置网络：也就是说，我几乎总是使用 SAM，但我认为了解后台发生了什么也很重要。举个例子，你可以使用 SAM 向系统添加打印机，而永远不知道为了支持新打印机做了什么操作。如果打印机因某种原因无法工作，如果不了解设备文件，你就真的无法开始排查问题。

下一部分是关于设备文件的一般概述。

### HP-UX 11i 中的设备文件

在 UNIX 世界中，还有什么比设备文件更令人困惑的呢？幸运的是，在 HP-UX 中，Series 700 和 Series 800 的设备文件几乎相同，因此如果你学会了其中一种，你的知识也适用于另一种。在本节中，我将涵盖以下内容：

- 设备文件的结构。
- 一些有助于你处理设备文件的命令。
- 一些创建设备文件的示例。

设备文件为 HP-UX 内核提供关于特定设备的重要信息。在执行 I/O 操作之前，HP-UX 内核需要了解关于该设备的许多信息。在 HP-UX 11i 中，工作站和服务器系统的设备文件命名约定是相同的。设备文件位于 /dev 目录中。/dev 下可能还有一个子目录，用于进一步对设备文件进行分类。子目录的一个示例是 /dev/dsk，磁盘设备文件通常位于此处；另一个是 /dev/rmt，磁带驱动器设备文件位于此处。图 5-7 展示了 HP-UX 11i 的设备文件命名约定。

![](img/eff8b9287a5f38c5adf538f24aacf29e_373_0.png)

图 5-7 HP-UX 11i 设备文件命名约定

在创建设备文件的过程中，你可以使用许多命令。ioscan 命令是其中的第一个。本节中的一些示例在第 3 章构建内核时已使用过。以下是与第 4 章中描述如何创建内核时运行 sysdef 的同一台 Series 700 系统的 ioscan 输出。（使用 -f 参数运行 ioscan 将生成完整列表；建议你尝试带和不带 -f 参数的情况。）我包含了四个 ioscan 输出，以便你可以看到来自不同系统的示例。最后一个列表来自第 9 章中磁盘和文件系统部分示例中使用的大型 V-Class 系统。

```
$ /usr/sbin/ioscan

(on Series 700)
H/W Path        Class         Description
==============================
        bc
1         graphics      Graphics
2         ba
2/0       unknown
2/0/1           target      Built-in SCSI
2/0/1.1.0     disk          HP C2247
2/0/1.2       target
2/0/1.2.0     disk          TOSHIBA CD-ROM XM-3301TA
2/0/1.6       target
2/0/1.6.0     disk          HP C2247
2/0/2       lan           Built-in LAN
2/0/4       tty           Built-in RS-232C
2/0/6       ext_bus       Built-in Parallel Interface
2/0/8       audio         Built-in Audio
2/0/10      pc            Built-in Floppy Drive
2/0/10.1    /dev/floppy   HP PC FDC FLOPPY
2/0/11      ps2           Built-in Keyboard
8         processor     Processor
9         memory          Memory
```

以下是来自 Series 800 系统的 ioscan 输出。注意该输出中显示的四个处理器。

```
$ /usr/sbin/ioscan

(on Series 800)
H/W Path        Class         Description
bc              bc            I/O Adapter
bc              I/O Adapter
ext_bus         GSC built-in Fast/Wide SCSI
disk            target        HP C2490WD
disk            target        HP C2490WD
disk            target        HP C2490WD
disk            target        HP C2490WD
bc              Bus Converter
ba              mux           mux
ba              Core I/O Adapter
ext_bus         Built-in Parallel Interface
ext_bus         Built-in SCSI
target          tape          HP HP35480A
target          disk          TOSHIBA CD-ROM XM-4101TA
lan             P82           Built-in Keyboard/Mouse
processor       Processor
processor       Processor
processor       Processor
processor       Processor
memory          Memory
```

最后一个来自 V-Class 服务器的 ioscan 输出。注意该输出中显示的八个处理器。

```
$ /usr/sbin/ioscan

(on V-Class)
H/W Path        Class         Description
bc              bc            PCI Bus Bridge - epic
lan             PCI           (10110019)
unknown         PCI           (107e0008)
```

| H/W Path | Class | Description |
| :--- | :--- | :--- |
| | ba | ext_bus | PCI Bus Bridge - epic |
| 2/0/0 | | target | Ultra Wide SCSI |
| 2/0/0.5 | | disk | SEAGATE ST34371W |
| 2/0/0.5.0 | | target | |
| 2/0/0.6 | | disk | SEAGATE ST34371W |
| 2/0/0.6.0 | | | |
| 2/0/0.7 | | target | |
| 2/0/0.7.0 | | ctl | Initiator |
| 2/1/0 | lan | | PCI (10110019) |
| 4 | ba | | PCI Bus Bridge - epic |
| 4/1/0 | fc | | HP Fibre Channel Mass |
| | | | Storage Adapter |
| 4/1/0.5 | lan | | HP Fibre Channel Mass |
| | | | Storage Ctrl |
| 4/1/0.8 | fcp | | FCP Protocol Adapter |
| 4/2/0 | ext_bus | | Ultra Wide SCSI |
| 4/2/0.0 | Target | | |
| 4/2/0.0.0 | disk | TOSHIBA CD-ROM XM-5701TA |
| 4/2/0.1 | target | |
| 4/2/0.1.0 | tape | HP C1537A |
| 4/2/0.7 | target | |
| 4/2/0.7.0 | , ctl | Initiator |
| 6 | | | PCI Bus Bridge - epic |
| 8 | memory | | |
| 15 | ba | | Core I/O Adapter |
| 15/1 | tty | Built-in Serial Port DUART |
| 15/2 | tty | Built-in Serial Port DUART |
| 15/3 | unknown | Unknown |
| 17 | processor | Processor |
| 19 | processor | Processor |
| 20 | processor | Processor |
| 22 | processor | Processor |
| 25 | processor | Processor |
| 27 | processor | Processor |
| 28 | processor | Processor |
| 30 | processor | Processor |

以下是来自 V-Class 服务器的完整 ioscan 输出。该服务器连接了一个大型磁盘单元（XP 256），这导致了非常长的输出，我在显示三个点的地方进行了缩写。

```
$ ioscan -f

(on V-Class)
Class  I  H/W Path        Driver     S/W State H/W Type        Description
----   -  --------        -----     --------- ------            -----------
bc         0                  root      CLAIMED   BUS_NEXUS     sago Bridge
ba         0   0  0/0   sasa        CLAIMED   BUS_NEXUS
lan        0   0/0/0   btlam6    CLAIMED   INTERFACE  PCI Ethernet (10110019)
...
```





## 344

# 第 5 章 虚拟分区和设备

ba 1 1 s2ga 已申领 总线 NEXUS saga 桥接器
ext_bus 0 0.0 0.0 c720 已申领 接口 Ultra2 Wide LVD SCSI
target 0 0.0 0.0.4 laimdo 设备
disk 0 0.0 0.0.4 edsk 已申领 设备 SEAGATE ST318275SLW
target 1 1.0 0.5.0 tgt 已申领 设备
disk 1 1.0 0.5.0 edsk 已申领 设备
target 2 1.0 0.6 tgt 已申领 设备 SEAGATE ST318275SLW
disk 2 1.0 0.6.0 edsk 已申领 设备 SEAGATE ST318275SLW
target 3 1.0 0.7 tgt 已申领 设备
disk 3 1.0 0.7.0 cttl 已申领 设备 启动器
target 4 1.0 0.8 tgt 已申领 设备
disk 4 1.0 0.8.0 edsk 已申领 设备 SEAGATE ST318275SLW
ext_bus 1 1.0.0 s2ga 已申领 设备
target 3 1.0 0.7 tgt 已申领 接口 Ultra2 Wide LVD SCSI
cd 1 1.0 0.7.0 c720 已申领 设备
target 1 1.0 0.7.0 ctti 已申领 设备
target 6 1.0 0.9 tgt 已申领 设备
disk 4 1.0 0.9.0 edsk 已申领 设备 SEAGATE ST318275SLW
target 7 1.0 0.10 tgt 已申领 设备
disk 5 1.0 0.10 edsk 已申领 设备 SEAGATE ST318275SLW
target 8 1.0 0.11 tgt 已申领 设备 SEAGATE ST318275SLW
disk 6 1.0 0.11 edsk 已申领 设备
target 9 1.0 0.12 tgt 已申领 设备
disk 7 1.0 0.12 edsk 已申领 设备 SEAGATE ST318275SLW
disk 8 1.0 0.12.0 soga 已申领 设备 SEAGATE ST318275SLW
ba 2 2 se2s 桥接器
fc 3 0.0.0 fd 已申领 接口 HP TapeTwo T137 光纤通道海量存储适配器
fcp 0 0.0.0.0 fcp 已申领 接口 FCP 协议适配器
ext_bus 7 2.0.0.8.0.0.0 fcparray 已申领 接口 FCP 阵列接口
target 12 2.0.0.8.0.0.0.0 tgt 已申领 设备
disk 79 2.0.0.8.0.0.0.0.0 sdisk 已申领 设备 HP OPEN-0
disk 79 2.0.0.8.0.0.0.0.1 sdisk 已申领 设备 HP OPEN-8
disk 79 2.0.0.8.0.0.0.0.2 sdisk 已申领 设备 HP OPEN-8
disk 105 2.0.0.8.0.0.0.0.3 sdisk 已申领 设备 HP OPEN-8
disk 105 2.0.0.8.0.0.0.0.4 sdisk 已申领 设备 HP OPEN-8
disk 105 2.0.0.8.0.0.0.0.5 sdisk 已申领 设备 HP OPEN-8
disk 107 2.0.0.8.0.0.0.0.5 sdisk 已申领 设备 HP OPEN-8
disk 108 2.0.0.8.0.0.0.0.7 sdisk 已申领 设备 HP OPEN-8
target 13 2.0.0.8.0.0.0.1 tgt 设备 HP OPEN-0
disk 111 2.0.0.8.0.0.0.1.0 sdisk 设备 HP OPEN-8
disk 109 2.0.0.8.0.0.0.1.1 sdisk 已申领 设备 HP OPEN-8
disk 120 2.0.0.8.0.0.0.1.2 sdisk 设备 HP OPEN-0
disk 11 2.0.0.8.0.0.0.1.3 sdisk 设备 HP OPEN-8
disk 112 2.0.0.8.0.0.0.1.4 sdisk 已申领 设备 HP OPEN-8
disk 113 2.0.0.8.0.0.0.1.5 sdisk 已申领 设备 HP OPEN-8
disk 114 2.0.0.8.0.0.0.1.6 sdisk 已申领 设备 HP OPEN-8
target 14 2.0.0.8.0.0.0.1.7 tgt 已申领 设备
disk 12 2.0.0.8.0.0.0.2 tgt 已申领 设备
disk 12 2.0.0.8.0.0.0.2.0 sdisk 已申领 设备 HP OPEN-8
disk 177 2.0.0.8.0.0.0.0.2.1 sdisk 已申领 设备 HP OPEN-8
target 15 2.0.0.8.0.0.0.3 tgt 已申领 设备
disk 13 2.0.0.8.0.0.0.3.0 sdisk 已申领 设备 HP DISK-SUBSYSTEM
target 16 2.0.0.8.0.0.0.4 tgt 设备 HP DISK-SUBSYSTEM
disk 14 2.0.0.8.0.0.0.4.0 sdisk 已申领 设备 HP DISK-SUBSYSTEM
target 17 2.0.0.8.0.0.0.0.5 tgt 已申领 设备
disk 15 2.0.0.8.0.0.0.5.0 sdisk 已申领 设备 HP DISK-SUBSYSTEM
target 18 2.0.0.8.0.0.0.6 tgt 已申领 设备
disk 16 2.0.0.8.0.0.0.6.0 sdisk 已申领 设备 HP DISK-SUBSYSTEM
disk 17 2.0.0.8.0.0.0.0.7 tgt 已申领 设备
target 20 2.0.0.8.0.0.0.8 tgt 已申领 设备
disk 18 2.0.0.8.0.0.0.8.0 sdisk 已申领 设备 HP OPEN-8
disk 79 2.0.0.8.0.0.0.8.1 sdisk 已申领 设备 HP OPEN-8
disk 80 2.0.0.8.0.0.0.8.2 sdisk 已申领 设备 HP OPEN-8
disk 115 2.0.0.8.0.0.0.8.3 sdisk 已申领 设备 HP OPEN-8
disk 116 2.0.0.8.0.0.0.8.4 sdisk 已申领 设备 HP OPEN-8
disk 11 2.0.0.8.0.0.0.8.5 sdisk 已申领 设备 HP OPEN-8
disk 119 2.0.0.8.0.0.0.8.7 sdisk 已申领 设备 HP OPEN-8
target 21 2.0.0.8.0.0.0.9 tgt 已申领 设备
disk 19 2.0.0.8.0.0.0.9.0 sdisk 已申领 设备 HP OPEN-8
disk 120 2.0.0.8.0.0.0.9.1 sdisk 已申领 设备 HP OPEN-8
disk 121 2.0.0.8.0.0.0.9.2 sdisk 已申领 设备 HP OPEN-8
disk 123 2.0.0.8.0.0.0.9.3 sdisk 已申领 设备 HP OPEN-8
disk 124 2.0.0.8.0.0.0.9.5 sdisk 已申领 设备 HP OPEN-8

| 磁盘 | 125 | 2.0.0.8.0.0.0.9.6 | sdisk | 已申领 | 设备 | HP OPEN-8 |
|---|---|---|---|---|---|---|
| 磁盘 | 178 | 2.0.0.8.0.0.0.9.7 | sdisk | 已申领 | 设备 | HP OPEN-8 |
| 目标 | 22 | 2.0.0.8.0.0.0.10 | tgt | 已申领 | 设备 | HP |
| 磁盘 | 22 | 2.0.0.8.0.0.0.10.0 | sdisk | 已申领 | 设备 | HP OPEN-8 |
| 磁盘 | 179 | 2.0.0.8.0.0.0.11 | sdisk | 已申领 | 设备 | HP OPEN-8 |
| 目标 | 23 | 2.0.0.8.0.0.0.11 | tgt | 已申领 | 设备 | HP DISK-SUBSYSTEM |
| 磁盘 | 23 | 2.0.0.8.0.0.0.11.0 | sdisk | 已申领 | 设备 | HP DISK-SUBSYSTEM |
| 目标 | 24 | 2.0.0.8.0.0.0.12 | tgt | 已申领 | 设备 | HP DISK-SUBSYSTEM |
| 磁盘 | 23 | 2.0.0.8.0.0.0.12.0 | sdisk | 已申领 | 设备 | HP DISK-SUBSYSTEM |
| 目标 | 25 | 2.0.0.8.0.0.0.13 | tgt | 已申领 | 设备 | HP DISK-SUBSYSTEM |
| 磁盘 | 23 | 2.0.0.8.0.0.0.13.0 | sdisk | 已申领 | 设备 | HP DISK-SUBSYSTEM |
| 目标 | 26 | 2.0.0.8.0.0.0.14 | tgt | 已申领 | 设备 | HP DISK-SUBSYSTEM |
| 磁盘 | 24 | 2.0.0.8.0.0.0.14.0 | sdisk | 已申领 | 设备 | HP DISK-SUBSYSTEM |

| 内存 | 0 | 8 | memory | 已申领 | 内存 | 内存 I/O 适配器 |
|---|---|---|---|---|---|---|
| 总线适配器 | 8 | 15 | bus_adapter | 已申领 | 总线_xBus | 核心 I/O 适配器 |
| congap1 | 0 | 15/2 | congap1 | 已申领 | 接口 | 内置串行端口 DUART |
| tty | 1 | 15/2 | congap1 | 已申领 | 接口 | 内置串行端口 DUART |
| 未知 | -1 | 15/3 | unknown | 未申领 | 未知 | 内置以太网 |
| 处理器 | 0 | 16 | processor | 未申领 | 处理器 | 处理器 |
| 处理器 | 1 | 18 | processor | 已申领 | 处理器 | 处理器 |
| 处理器 | 2 | 21 | processor | 已申领 | 处理器 | 处理器 |
| 处理器 | 3 | 23 | processor | 已申领 | 处理器 | 处理器 |
| 处理器 | 4 | 24 | processor | 已申领 | 处理器 | 处理器 |
| 处理器 | 5 | 26 | processor | 已申领 | 处理器 | 处理器 |
| 处理器 | 6 | 29 | processor | 已申领 | 处理器 | 处理器 |
| 处理器 | 7 | 32 | processor | 已申领 | 处理器 | 处理器 |
| 处理器 | 8 | 34 | processor | 已申领 | 处理器 | 处理器 |
| 处理器 | 9 | 37 | processor | 已申领 | 处理器 | 处理器 |
| 处理器 | 10 | 39 | processor | 已申领 | 处理器 | 处理器 |
| 处理器 | 11 | 40 | processor | 已申领 | 处理器 | 处理器 |
| 处理器 | 12 | 42 | processor | 已申领 | 处理器 | 处理器 |
| 处理器 | 13 | 45 | processor | 已申领 | 处理器 | 处理器 |

下一条有助于创建设备文件的命令是 `lsdev`。`lsdev` 会列出已配置到系统中的驱动程序。在添加设备文件时，需要将对应设备的驱动程序配置到系统中。如果该驱动程序未配置到系统中，可以使用 SAM 进行配置，或者使用前面介绍的手动内核配置流程。表中包含字符设备和块设备的主设备号、驱动程序名称以及驱动程序的类别。主设备号、字符设备及其他参数将在后文中定义。以下是在运行了 `ioscan` 的同一台 Series 700 机器上运行 `lsdev` 的示例：

（在 Series 700 上）

```
$ /usr/sbin/lsdev
```

| 字符 | 块 | 驱动程序 | 类别 |
|---|---|---|---|
| 0 | -1 | csn | 伪 |
| 1 | -1 | ansi0 | tty |
| 2 | -1 | mm | 伪 |
| 3 | -1 | ptyM | ptyu |
| 16 | -1 | ptyS | ptyS |
| 24 | -1 | HiL | HiL |
| 27 | -1 | dmEm | 伪 |
| 46 | -1 | netcdiag | 未知 |
| 52 | -1 | Lan2 | lan |
| 64 | 64 | lv | lvm |
| 66 | -1 | audio | audio |
| 69 | -1 | devconfig | 伪 |
| 72 | -1 | CLone | 伪 |
| 73 | -1 | StrLog | 伪 |
| 74 | -1 | sad | 伪 |
| 75 | -1 | teLM | StrteLM |
| 76 | -1 | teLS | StrteLS |
| 77 | -1 | tIcots | 伪 |
| 78 | -1 | tIcots | 伪 |
| 79 | -1 | tIcoTsod | 伪 |
| 114 | -1 | ip | 伪 |
| 115 | -1 | arp | 伪 |
| 116 | -1 | echo | 伪 |
| 119 | -1 | dIpi | 伪 |
| 130 | -1 | rawIP | 伪 |
| 136 | -1 | tcp | 伪 |
| 137 | -1 | udp | 伪 |
| 138 | -1 | StcpmAp | 伪 |
| 139 | -1 | nuIs | 伪 |
| 140 | -1 | netga | 伪 |
| 141 | -1 | tun | 伪 |
| 142 | -1 | bftlan3 | 未知 |
| 143 | -1 | ffdai3 | 未知 |
| 144 | -1 | ffdai0 | 未知 |
| 145 | -1 | fcTL_cntL | 未知 |
| 156 | -1 | ptM | StrptyM |
| 157 | -1 | ptS | StrptyS |
| 159 | -1 | ps2 | ps2 |
| 164 | -1 | pipedEv | 未知 |
| 168 | -1 | beep | graf 伪 |
| 169 | -1 | focse_Lan | Lan |
| 170 | -1 | Ipro | 未知 |
| 174 | -1 | framebuf | graf 伪 |
| 183 | -1 | diagI | diag |
| 188 | 31 | sdisk | disk |
| 189 | -1 | klog | 伪 |
| 196 | -1 | eepr0M | da |
| 203 | -1 | sctl | ctl |
| 205 | -1 | Stape | tape |
| 207 | -1 | Sy | 伪 |
| 216 | -1 | CentIF | ext Bus |
| 227 | -1 | kepd | 伪 |
| 229 | -1 | ite | graf 伪 |
| 232 | -1 | diag2 | diag |




接下来是在同一台已运行过 **ioscan** 的 Series 800 上运行 **lsdev** 的示例：

（在 Series 800 上）

```bash
$ /usr/sbin/lsdev
```

| 字符 | 块 | 驱动 | 类 |
| :--- | :--- | :--- | :--- |
| 0 | -1 | cn | pseudo |
| 1 | -1 | asio0 | tty |
| 3 | -1 | mm | pseudo |
| 16 | -1 | ptym | ptym |
| 17 | -1 | ptys | ptys |
| 28 | -1 | diag0 | diag |
| 46 | -1 | netdiag1 | unknown |
| 52 | -1 | lan2 | lan |
| 64 | 64 | lv | lvm |
| 69 | -1 | dev_config | pseudo |
| 72 | -1 | clone | pseudo |
| 73 | -1 | strlog | pseudo |
| 74 | -1 | sad | pseudo |
| 75 | -1 | telm | strtelm |
| 76 | -1 | tels | strtels |
| 77 | -1 | t1ctl1s | pseudo |
| 78 | -1 | t1cots | pseudo |
| 79 | -1 | t1cotsod | pseudo |
| 114 | -1 | ip | pseudo |
| 116 | -1 | echo | pseudo |
| 119 | -1 | dlpi | pseudo |
| 130 | -1 | rawip | pseudo |
| 136 | -1 | 1pr0 | unknown |
| 137 | -1 | udp | pseudo |
| 138 | -1 | stcpgmap | pseudo |
| 139 | -1 | nuls | pseudo |
| 140 | -1 | netga | pseudo |
| 141 | -1 | tun | pseudo |
| 142 | -1 | btlani3 | unknown |
| 143 | -1 | fddil3 | unknown |
| 144 | -1 | fddi0 | unknown |
| 156 | -1 | pttm | strpttm |
| 157 | -1 | ptm | strptys |
| 159 | -1 | ps2 | ps2 |
| 164 | -1 | pipedev | unknown |
| 168 | -1 | beep | graf_pseudo |
| 174 | -1 | framebuffer | graf_pseudo |
| 188 | 31 | sdisk | disk |
| 189 | -1 | klog | pseudo |
| 193 | -1 | mux2 | tty |
| 203 | -1 | sctl | ctl |
| 205 | -1 | tape | tape |
| 207 | -1 | sy | pseudo |
| 216 | -1 | CentIF | ext_bus |
| 227 | -1 | kept | pseudo |
| 229 | -1 | ite | graf_pseudo |

最后，这里是在同一台已运行过第一个 **ioscan** 的 V-Class 服务器上运行 **lsdev** 的示例：

```bash
$ /usr/sbin/lsdev
                              (在 V-Class 上)
```

| 字符 | 块 | 驱动 | 类 |
| :--- | :--- | :--- | :--- |
| 0 | -1 | cn | pseudo |
| 3 | -1 | mm | pseudo |
| 16 | -1 | pty0m | pty0m |
| 17 | -1 | pty1e | pty1e |
| 27 | -1 | dmem | pseudo |
| 28 | -1 | diag0 | diag |
| 46 | -1 | netdiag1 | unknown |
| 64 | 64 | lv | lvm |
| 69 | -1 | dev_config | pseudo |
| 72 | -1 | clone | pseudo |
| 73 | -1 | strlog | pseudo |
| 74 | -1 | sad | pseudo |
| 75 | -1 | telm | strtelm |
| 76 | -1 | tels | strtels |
| 77 | -1 | ticlts | pseudo |
| 78 | -1 | tlcots | pseudo |
| 79 | -1 | tlcootad | pseudo |
| 114 | -1 | ip | pseudo |
| 115 | -1 | arp | pseudo |
| 116 | -1 | echo | pseudo |
| 119 | -1 | dlpi | pseudo |
| 130 | -1 | rawip | pseudo |
| 136 | -1 | tcp | pseudo |
| 137 | -1 | udp | pseudo |
| 138 | -1 | stopmap | pseudo |
| 139 | -1 | nuls | pseudo |
| 140 | -1 | netgq | pseudo |
| 141 | -1 | tun | pseudo |
| 142 | -1 | fddi4 | unknown |
| 143 | -1 | fc71_ctl | lan |
| 144 | -1 | fcgsc_lan | lan |
| 145 | -1 | lpr0 | unknown |
| 156 | -1 | ptm | strptym |
| 157 | -1 | pts | strptys |
| 164 | -1 | pipedev | unknown |
| 169 | -1 | conspl | tty |
| 170 | -1 | btlam6 | lan |
| 171 | -1 | fcp | fcp |
| 188 | 31 | sdisk | disk |
| 189 | -1 | klog | pseudo |
| 203 | -1 | sctl | ctl |
| 205 | -1 | stape | tape |
| 207 | -1 | sy | pseudo |
| 227 | -1 | kepd | pseudo |
| 232 | -1 | diag2 | diag |

从这三个 **lsdev** 输出中，你可以观察到设备方面的一些细微差异。例如，Series 700 具有音频和软盘等类别，Series 800 具有多路复用器，而 V-Class 具有 BaseTen 网卡。

你可以使用 **ioscan** 来显示特定外设的设备文件。回到那台连接了四个磁盘和一台 CD-ROM 的 Series 800，你可以发出以下 **ioscan** 命令来查看与*磁盘*相关的设备文件：

（在 Series 800 上）

```bash
$ /usr/sbin/ioscan -fn -C disk
```

| 类 | I 硬件路径 | 驱动 | 软件状态 | 硬件类型 | 描述 |
| :---- | :--------- | :----- | :-------- | :------- | :---------- |
| disk | 0 10/0.3.0 | sdisk | CLAIMED | DEVICE | HP C2490WD |
|      |            | /dev/dsk/c0t3d0 | | /dev/rdisk/c0t3d0 | |
| disk | 1 10/0.4.0 | sdisk | CLAIMED | DEVICE | HP C2490WD |
|      |            | /dev/dsk/c0t4d0 | | /dev/rdisk/c0t4d0 |
| disk | 2 10/0.5.0 | sdisk | CLAIMED | DEVICE | HP C2490WD |
|      |            | /dev/dsk/c0t5d0 | | /dev/rdisk/c0t5d0 |
| disk | 3 10/0.6.0 | sdisk | CLAIMED | DEVICE | HP C2490WD |
|      |            | /dev/dsk/c0t6d0 | | /dev/rdisk/c0t6d0 |
| disk | 3 10/12/5/2.0 | sdisk | CLAIMED | DEVICE | CD-ROM |
|      |              | /dev/dsk/c1t2d0 | | /dev/rdisk/c1t2d0 |

从这个 **ioscan** 输出中，你可以看到所有与*磁盘*相关的设备文件，包括 CD-ROM。

你可以使用 **diskinfo** 命令来获取关于这些设备中某一个的更多信息。请指定你想要了解更多信息的字符设备，如下所示（使用 *-v* 选项提供详细信息可以获得更详尽的信息）。

```bash
$ diskinfo /dev/rdsk/c0t5d0
SCSI describe of /dev/rdsk/c0t5d0
    vendor: HP
    product id: C2490WD
    type: direct access
    size: 2082636 bytes
bytes per sector: 512
```

### 添加外设的示例

在本节中，我们将为一个磁带驱动器构建设备文件。第 9 章介绍了使用设备文件以及所有逻辑卷管理器（Logical Volume Manager）命令来添加磁盘设备的流程，你可能也会想看看这部分内容。在构建设备文件之前，让我们先查看 Series 700 上两个现有的设备文件，看看这些信息出现在哪里。第一个长列表是磁带驱动器的，第二个是磁盘的，两者都在前文的 Series 700 列表中出现过。

```bash
$ ll /dev/rmt/0m
(在 Series 700 上)
crw-rw-rw-  2 bin bin  205 0x003000 Feb 12 03:00 /dev/rmt/0m
```

```bash
$ ll /dev/dsk/c0t1d0
(在 Series 700 上)
brw-r-----  1 bin sys  31 0x001000 Feb 12 03:01 /dev/dsk/c0t1d0
```

磁带驱动器设备文件 **/dev/rmt/0m** 显示主设备号为 205，这与 `lsdev` 中字符设备驱动程序 *stape* 所示的主设备号相对应。磁盘驱动器设备文件 **/dev/dsk/c0t6d0** 显示主设备号为 31，这与 `lsdev` 中*块*设备驱动程序 *fsdisk* 相对应。由于磁带驱动器只需要一个字符设备文件，且没有块 *stape* 设备的主设备号（如 `lsdev` 中块列中的 - *I* 所示），因此该文件是磁带驱动器唯一的设备文件。另一方面，磁盘既可以作为块设备使用，也可以作为字符设备使用（也称为*原始设备*）。因此，我们应该看到一个字符设备文件 /dev/rdsk/c0t6d0，其主设备号为 188，如 `lsdev` 中 *fsdisk* 所示。

（在 Series 700 上）

```bash
$ ll /dev/rdsk/c0t6d0

crw-r----- 1 root sys 188 0x001000 Feb 12 03:01 /dev/rdsk/c0t6d0
```

现在，我们可以使用 `mksf` 命令为第二个磁带驱动器（这次位于 SCSI 地址 2）创建一个设备文件，并为位于 SCSI 地址 5 的磁盘驱动器创建一个磁盘设备文件。你可以以两种不同的方式运行 `mksf`。第一种 `mksf` 形式要求你包含较少具体的信息，例如次设备号。第二种形式要求你包含更多这些具体信息。这些参数中有一些仅适用于你使用的特定 `mksf` 形式。

- `-d`
    使用指定的设备驱动程序。可以使用 `lsdev` 命令获取设备驱动程序列表。
- `-C`
    指定的设备属于此类。类也可以通过 `lsdev` 命令获取。
- `-H`
    使用指定的硬件路径。硬件路径可以通过 `ioscan` 命令获取。
- `-m`
    提供设备的次设备号。
- `-r`
    创建字符设备，也称为原始设备文件。默认情况下创建块文件。
- `-v`
    使用详细输出，这会打印出每个创建的特殊文件的名称。

我们将为磁盘驱动器创建设备文件。需要创建块设备和字符设备文件。示例中的 0x005000 对应于磁盘驱动器上地址 5。这个号码用于块设备和字符设备文件中，对于创建的每个磁盘驱动器都是唯一的。

现在，我们可以使用以下 `mksf` 命令为位于 SCSI 地址 5 的磁盘创建一个块设备文件：

（在 Series 700 上）

```bash
$ /sbin/mksf -v -C disk -m 0x005000 /dev/dsk/c0t5d0
making /dev/dsk/c0t5d0 b 31 0x005000
```

类似地，我们现在可以使用 `mksf` 的第二种形式为位于 SCSI 地址 5 的磁盘创建一个字符设备文件：

（在 Series 700 上）

```bash
$ /sbin/mksf -v -r -C disk -m 0x005000 /dev/dsk/c0t5d0
making /dev/rdsk/c0t5d0 c 188 0x005000
```




这些示例中使用的 -v 选项会在每个设备文件创建时打印该文件。如果您希望在系统中除了现有的磁带驱动器 /dev/rmt/0m 之外，再在 SCSI 地址 2 上添加第二个磁带驱动器，您可以使用以下 mkfs 命令：

```text
(on Series 700)

$ /sbin/mkfs -v -C tape -m 0x002000 /dev/rmt/1m

      making /dev/rmt/1m c 205 0x002000
```

由于不需要块设备驱动程序，因此磁带驱动器会自动生成字符设备。这一事实在 lsdev 命令的输出中已获证实，其中“Block”列中标有 -B。

有了这些关于设备文件的基础知识，当您在添加外围设备时，您应该对 SAM 为您构建的设备文件有一个很好的理解。顺便提一下，打印机设备文件与我在此介绍的设备文件大不相同，但所有相同的原理都适用。

### 内存管理 - 与设备文件有些相关

内存相关的话题在系统管理讨论中几乎从未被涉及。这是因为内存的存在形式太多了，影响所需内存量以及所需内存类型的因素也太多了。让我们从高层概述一些内存相关的话题，并查看一些与内存相关的命令。

一开始，大多数关于内存的讨论都会从这个问题开始：什么是交换区（swap），我需要多少？HP-UX 系统管理员花费大量时间担心交换区的问题。它肯定非常重要。交换区是 HP-UX 整体内存管理方案的一部分，确切地说是三部分之一。任何计算机科学学生都会告诉你，计算机有三种类型的内存：缓存内存、随机访问内存（RAM）和磁盘内存。它们按速度排列；也就是说，缓存比 RAM 快得多，而 RAM 又比磁盘快得多。

#### 缓存内存

HP Precision Architecture 芯片组配置了数据缓存和指令缓存，我可能还要补充一点，这些缓存被非常高效地使用。你必须依赖操作系统来高效地使用缓存，因为你对这一过程的控制非常有限。如果你需要的信息已加载到缓存中（这可能是因为您最近访问过该信息，或者访问了与当前所需信息位置相近的其他信息），那么从缓存内存中获取信息将花费极少的时间。这种访问被称为缓存“命中”，在所有实际目的来看都是瞬间完成的。缓存内存之所以如此快的原因之一是它通常物理上位于与处理器相同的芯片上。如果可以在处理器芯片上安装大量缓存，那么就不需要 RAM 和磁盘了。然而，这在当前是不可能的，因此高效使用内存是整体系统良好表现的关键。

### 检查可用 RAM

您的系统会明确告知您有多少可用 RAM。/sbin/dmesg 会给出系统中安装的“物理”内存数量，如下面的 64-MByte 系统所示：

```text
Physical: 65536 Kbytes
```

当您看到这个数字时不要过于兴奋，因为这并不是所有“可用”内存。可用内存是预留了一部分内存用于内核代码和数据结构后剩下的部分。您还将看到可用内存，在本例中约为 54 MBytes，通过 /sbin/dmesg 可以看到：

```text
available: 55336 Kbytes
```

部分可用内存也可以是“可锁定”的。可锁定内存是指可以专门用于频繁访问的.program 和数据。锁定内存以执行的程序和数据将保持内存驻留并运行得更快。您还会在系统启动时看到可锁定内存的数量，在本例中约为 44 MBytes：

```text
lockable: 45228
```

**/sbin/dmesg** 会向您显示这些值以及系统相关消息的摘要。您应该在您的系统上执行此命令，查看它告诉您的内容。以下显示了一个大型 V-Class 系统在附加了 XP 256 磁盘阵列单元后执行 **bdf** 和 **/sbin/dmesg** 命令的输出。

```text
# bdf
Filesystem    kbytes  used     avail %used Mounted on
/dev/vg00/lvol3   524288 40999 483221   8% /
/dev/vg00/lvol1      99669 29984  58710 33% /stand
/dev/vg00/lvol7   1048576 272706 728019 27% /var
/dev/vg00/lvol16  1048576 491445 523318 48% /usr
/dev/vg01/lvol1   35860480 35632 35544976  0% /l/u0
/dev/vg09/lvol1    35860480 4358224 31294152 12% /l/u9
/dev/vg08/lvol1    35860480 21366 35576720  0% /l/u8
/dev/vg07/lvol1    35860480 555444 35302928  2% /l/u7
/dev/vg06/lvol1    35860480 13624 35564816  0% /l/u6
/dev/vg05/lvol1    35860480 560432 35302480  2% /l/u5
/dev/vg04/lvol1    35860480 575152 35300968  2% /l/u4
/dev/vg03/lvol1    35860480 13624 35564816  0% /l/u3
/dev/vg02/lvol1    35860480 13632 35566808  0% /l/u2
/dev/vg01/lvol4     294800 2273 189930  1% /l/u1
/dev/vg00/lvol4    2097152 466924 1529479 33% /opt
/dev/vg00/lvol8     524288 2087 488858  1% /home
/dev/vgsp/lvol1    35860480 64095880 29146160 18% /app

# /sbin/dmesg
Jun 20 16:26
disk
5/0/0.8.0.0.0.9.2 adisk
5/0/0.8.0.0.0.9.3 adisk
5/0/0.8.0.0.0.9.4 adisk
5/0/0.8.0.0.0.9.9 adisk
5/0/0.8.0.0.0.9.6 adisk
5/0/0.8.0.0.0.9.7 adisk
5/0/0.8.0.0.0.10 cgt
5/0/0. . . . .. . s3iex
5/0/0.8.0.0.0.10.1 adisk
5/0/0.8.0.0.0.10.2 adisk
5/0/0.8.0.0.0.10.3 adisk
5/0/0.8.0.0.0.10.4 adisk
5/0/0.8.0.0.0.10.5 adisk
5/0/0.8.0.0.0.11 sgt
5/0/0.8.0.0.0.11.0 adisk
5/0/0.8.0.0.0.12 tgt
5/0/0.8.0.0.0.13 tgt:
5/0/0.8.0.0.0.13.0 adisk
5/0/0.8.0.0.0.14 tgt
5/0/0.8.0.0.0.14.0 adisk
5/0/0.8.0.255.0.0 fdcpue
5/0/0.8.0.255.0.0 sgt:
5/0/0.8.0.255.0.0 sct1
Probing epic6
Probe of epic6 complete
6 miga
```

```text
6/0/0 btlane
Probing eppic7
Probes of epic7 complete
7 saga
7/0/0 td
td: claimed Tachyon TL/TS Fibre Channel Mass Storage card at 7/0/0
7/0/0.8 fcp

+   7/0/0.9.0.0.0.0 [primary] 
+   7/0/0.0.0.0.0.0 fcpa1
+   7/0/0.0.0.0.5.0 sdisk
+   7/0/0.0.0.0.0.1 sdisk
+   7/0/0.0.0.0.0.2 sdisk
+   7/0/0.0.0.0.0.3 sdisk
+   7/0/0.0.0.0.0.4 sdisk
+   7/0/0.0.0.0.0.5 sdisk
+   7/0/0.0.0.0.0.6 sdisk
+   7/0/0.0.0.0.0.7 sdisk
+   7/0/0.0.0.0.1 tgt
+   7/0/0.0.0.0.0.0 sdisk
+   7/0/0.0.0.0.0.11 sdisk
+   7/0/0.0.0.0.0.12 sdisk
+   7/0/0.0.0.0.0.13 sdisk
+   7/0/0.0.0.0.0.14 sdisk
+   7/0/0.0.0.0.0.15 sdisk
+   7/0/0.0.0.0.0.16 sdisk
+   7/0/0.0.0.0.0.17 sdisk
+   7/0/0.0.0.0.2 tgt
+   7/0/0.0.0.0.2.0 sdisk
+   7/0/0.0.0.0.2.1 sdisk
+   7/0/0.0.0.0.2.2 sdisk
+   7/0/0.0.0.0.2.3 sdisk
+   7/0/0.0.0.0.3 sdisk
+   7/0/0.0.0.0.3.0 sdisk
+   7/0/0.0.0.0.3.1 sdisk
+   7/0/0.0.0.0.3.2 sdisk
+   7/0/0.0.0.0.4 tgt
+   7/0/0.0.0.0.4.0 sdisk
+   7/0/0.0.0.0.4.1 sdisk
+   7/0/0.0.0.0.4.2 sdisk
+   7/0/0.0.0.0.4.3 sdisk
+   7/0/0.0.0.0.4.4 sdisk
+   7/0/0.0.0.0.4.5 tgt
+   7/0/0.0.0.0.4.6 tgt
+   7/0/0.0.0.0.4.6.0 sdisk
+   7/0/0.0.0.0.4.7 tgt
+   7/0/0.0.0.0.4.7.0 sdisk
+   7/0/0.0.0.0.4.7.1 sdisk
+   7/0/0.0.0.0.4.7.2 sdisk
+   7/0/0.0.0.0.5 sdisk
+   7/0/0.0.0.0.5.1 sdisk
+   7/0/0.0.0.0.5.2 sdisk
+   7/0/0.0.0.0.5.3 sdisk
+   7/0/0.0.0.0.5.4 sdisk
+   7/0/0.0.0.0.5.5 sdisk
+   7/0/0.0.0.0.5.6 sdisk
+   7/0/0.0.0.0.5.7 sdisk
+   7/0/0.0.0.0.9 tgt
+   7/0/0.0.0.0.9.0 sdisk
+   7/0/0.0.0.0.9.1 sdisk
+   7/0/0.0.0.0.9.2 sdisk
+   7/0/0.0.0.0.9.3 sdisk
+   7/0/0.0.0.0.9.4 sdisk
+   7/0/0.0.0.0.9.5 sdisk
+   7/0/0.0.0.0.9.6 sdisk
+   7/0/0.0.0.0.9.7 sdisk
+   7/0/0.0.0.0.10 tgt
+   7/0/0.0.0.0.0.0 sdisk
+   7/0/0.0.0.0.0.1 sdisk
+   7/0/0.0.0.0.0.2 sdisk
+   7/0/0.0.0.0.0.3 sdisk
+   7/0/0.0.0.0.0.4 sdisk
+   7/0/0.0.0.0.0.5 sdisk
+   7/0/0.0.0.0.0.6 sdisk
+   7/0/0.0.0.0.0.7 sdisk
+   7/0/0.0.0.0.0.8 sdisk
+   7/0/0.0.0.0.0.9 sdisk
+   7/0/0.0.0.0.0.10 sdisk
+   7/0/0.0.0.0.0.11 sdisk
+   7/0/0.0.0.0.0.12 sdisk
+   7/0/0.0.0.0.0.13 tgt
+   7/0/0.0.0.0.0.14 tgt
+   7/0/0.0.0.0.0.15 tgt
+   7/0/0.0.0.0.255.0 fcpdev
+   7/0/0.0.255.0.0 tgt
+   7/0/0.0.255.0.0.0 sctl

8 memory
15 bus_adapter
15/1 conspi
15/2 conspi
```

```text
1: process88
2: processor
3: processor
4: processer
5: processor
6: processor
7: processor
3: processer
39: processer
40: processor
42: processer
45 [CPU] esm:

hileage: Initializing 10/100BASE-TX card at 0/0/0....
t51mo: Initializing 10/100BASE-TX card at 6/0/0....

System Console is on SPP DUART0 Interface
Entering cifs init....
Initialisation finished successfully....slot is B
Logical volume 64, 0X1 configured as SCOT
Logical volume 64, 0X2 configured as SWAP
Logical volume 64, 0X2 configured as SWAP
Swap device table: (start & size given in 512-byte blocks)
entry 0 - major is 64, minor is 0X2; start = 0, size = 2097152
Dump device table: (start & size given in 1-Kbyte blocks)
entry 0 - major is 31, minor is 0xe000; start = 105312, size = 1048576
Starting the STEMM33 daemons-phase 1
hileage: NOTE: NIT Link Status Not OK - Switch Connection to AUI at 0/0/0....
Create STCP device files
Starting the STEMM33 daemons-phase 2
92352B/9245XB NP-UX (8.11.09) #1: Wed Nov 5 22:38:19 PST 1997

Memory Information:
physical page size = 4096 bytes, logical page size = 4096 bytes
Physical: 16777120 Kbytes, lockable: 13909368 Kbytes, available: 15036116 K

hileage: timeout: DMA Timeout occurred at 0/0/0
hileage: reset state is B50 at 0/0/0....
hileage: WARNING: AUI Loopback Failed at 0/0/0....
hileage: timeout: DMA Timeout occurred at 0/0/0
hileage: reset state is 574 at 0/0/0....
hileage: WARNING: BNC Loopback Failed at 0/0/0....
Unable to add all swap for device: /dev/yy0/lvol9. Increase the tunable parame
G
```

如您所见，除了我们之前讨论过的内存相关报告外，**dmesg** 还提供了大量有用的信息。此输出中的内存信息总量约为 1.6 GBytes，可锁定内存约为 1.3 GBytes。

### 管理缓存和 RAM

如果您需要的信息不在缓存内存中，而是在 RAM 中，那么访问将花费更长的时间。所有内存的速度都在增加，而 RAM 的速度增加得特别快。您对 RAM 的使用方式有很大控制权。首先，您可以决定系统中配置了多少 RAM。整个 HP 产品线，无论是工作站还是服务器系统，都支持比系统实际需要的更多的 RAM。





截至本文撰写之时，RAM 价格低廉，且成本还在持续下降。在配置系统时，RAM 不是应该省钱的地方。此外，你可以高效地利用已配置的所有 RAM。一个示例是配置高效的 HP-UX 内核。HP-UX 内核始终加载在 RAM 中。这意味着如果它比你的需求大了 2 或 3 MB，那么你就失去了 2 或 3 MB 用于其他用途的空间。如果你需要访问 RAM 中的某些信息，其访问速度将比在缓存（cache）中慢大约一个数量级。

#### 虚拟内存

如果你的系统只有缓存和，比方说，64 MB 的 RAM，那么你就只能运行消耗约 64 MB 物理内存的用户进程。利用内存管理，你可以使用虚拟内存来运行远超物理内存大小的用户进程。虚拟内存允许你仅将进程的一部分加载到 RAM 中，而将其余部分保留在磁盘上。你在内存和磁盘之间以页（pages）为单位来回移动数据块。

#### 交换区（Swap）

Swap 用于扩展内存大小，即在磁盘上预留一块区域作为 RAM 的扩展。当系统负载较高时，交换区空间用于容纳那些在物理内存中没有可用空间的部分或全部进程。HP-UX 通过 `vhand`、`statddaemon` 和 `svapper` 进程为你处理所有这些交换操作。你需要确保磁盘上预留了足够的交换区空间，以便内存管理能够进行而不会耗尽交换区空间。

存在三种类型的交换区空间：主交换区、次交换区和文件系统交换区。如下所述：

-   **主交换区（Primary swap）**：在启动时可用的交换区。主交换区位于与根文件系统相同的磁盘上。如果这个主交换区出现问题，你可能会很难引导系统。
-   **次交换区（Secondary swap）**：位于根磁盘以外的其他磁盘上的交换区。
-   **文件系统交换区（File system swap）**：这是一种既支持文件和数据结构，又支持交换操作的文件系统。

不要过于纠结于配置交换区的大小。最低限度，交换区应该是物理内存大小的两倍（这是安装过程的默认大小）。此外，我们的主要应用程序将定义所需的交换区数量。我接触过的应用程序大多会明确说明应用程序所需的最大交换区数量。如果你正在运行多个应用程序，并且它们将同时运行，请累加每个应用程序所需的交换区数量。

# 第 6 章

## 用户和组

## 虚拟分区与用户

每个虚拟分区（Virtual Partition）就像一个独立的服务器。这意味着你在各自的虚拟分区中有独立的用户。需要在虚拟分区之间共享的任何用户相关信息，将以与在物理上分离的服务器之间共享相同的方式进行。例如，你可能希望用户有能力从一个虚拟分区远程登录到另一个虚拟分区。你可以通过在每个虚拟分区中设置适当的网络文件来实现这一目标，就像在独立的服务器上那样（有关网络的详细信息，请参见第 13 章）。图 6-1 展示了虚拟分区与用户之间的关系：

![](img/eff8b9287a5f38c5adf538f24aacf29e_395_0.png)

**图 6-1** 虚拟分区和用户

如图 6-1 所示，每个虚拟分区都有自己的操作系统实例和用户集。从软件角度看，vPar 是隔离的，因此用户似乎存在于不同的服务器上。为了在用户之间共享信息，例如用户数据库，你可以实现诸如网络信息系统（NIS）等技术。使用 NIS，你可以创建一个共享于不同系统之间的用户信息数据库，在这种情况下，即不同的 vPar，因为从软件角度来看，它们等同于不同的服务器。

现在让我们在每个 vPar 上创建一个新用户。在 *cable1* 上，我们将创建用户 *cable1us*，并验证该用户不存在于 *cable2* 上。在 *cable2* 上，我们将创建用户 *cable2us*，并验证该用户不存在于 *cable1* 上。有关创建用户的详细信息，请参阅本章的背景部分。

图 6-2 展示了在 vPar *cable1* 中使用系统管理经理（SAM）创建用户 *cable1us* 的屏幕截图：

![](img/eff8b9287a5f38c5adf538f24aacf29e_396_0.png)

**图 6-2** 在 SAM 中创建 *cable1us* 用户

图 6-2 显示了 *cvhdccon3* 的主机名，这是对 vPar *cable1* 服务器名称的对应。

用户 *cable1us* 是在 vPar *cable1* 中创建的，并且仅存在于 *cable1* 中。我们将很快验证这一点。我们使用 SAM 在 vPar *cable2* 中创建用户 *cable2us* 时执行了相同的程序。

现在，*cable1* 中应该有一个用户无法在 *cable2* 中查看，反之亦然。以下显示了连接到 *cable1* 并列出 /etc/passwd 内容的过程。

```bash
cvhdccon3:/ # cat /etc/passwd
root:*:hiIXKsAzUIPy6:0:3:::/sbin/sh      cable1 listing
daemon:*:*:1:5:::/sbin/sh
bin:*:*:2:2::/usr/bin:/sbin/sh
sys:*:*:3:3::/
adm:*:*:4:4::/var/adm:/sbin/sh
uucp:*:*:5:3::/var/spool/uucppublic:/usr/sbin/uucp/uucico
lp:*:*:9:7::/var/spool/lp:/sbin/sh
nuucp:*:*:11:11::/var/spool/uucppublic:/usr/sbin/uucp/uucico
hpdb:*:*:27:1:ALLBASE::/sbin/sh
nobody:*:*:-2:-2::/
www:*:*:30:1::/
webadmin:*:*:40:1::/usr/obam/server/nologindir:/usr/bin/false
snmbull:*:*:101:101:Do not USE or DELETE - needed by Samba:
        /home/snmbull:/sbin/sh
opc_op:*:*:777:777:OPC DEFAULT OPERATOR:/home/opc_op_op:/sbin/sh
Cable2us:*:102:20:::/home/Cable2us:/usr/bin/sh  <-- cable2us
cvhdccon3:/ #
```

`cable1` 的这个列表表明，`cable1us` 存在于 `cable1` 上的 `/etc/passwd` 文件中；然而，此文件中没有 `cable2us`。以下显示了连接到 `cable2` 并列出 `/etc/passwd` 内容的过程。

```bash
# cat /etc/passwd
root: * :X6GAMrnH.aBs:0:3:::/sbin/sh      cable2 listing
daemon: * : * :1:5:::/sbin/sh
bin: * : * :2:2::/usr/bin:/sbin/sh
sys: * : * :3:3::/
adm: * : * :4:4::/var/adm:/sbin/sh
uucp: * : * :5:3::/var/spool/uucppublic:/usr/sbin/uucp/uucico
lp: * : * :9:7::/var/spool/lp:/sbin/sh
nuucp: * : * :11:11::/var/spool/uucppublic:/usr/sbin/uucp/uucico
hpdb: * : * :27:1:ALLBASE::/sbin/sh
nobody: * : * :-2:-2::/
www: * : * :30:1::/
webadmin: * : * :40:1::/usr/obam/server/nologindir:/usr/bin/false
sam_exec: xxx: 0: 1::/home/sam_exec:/usr/bin/sh
Cable2us: * :101: 20::/home/Cable2us:/usr/bin/sh      <-- cable2us
#
```

`cable2` 的这个列表表明，`cable2us` 存在于 `cable2` 上的 `/etc/passwd` 文件中；然而，此文件中没有 `cable1us`。

该列表表明，各自 vPar 的唯一用户仅存在于其创建的 vPar 上。此外，每个 vPar 都有自己的 `root` 和其他系统级用户。

接下来，让我们看看 vPar 中单个用户的设置信息。

### 单个用户设置

就用户设置而言，你在 vPar 环境中执行设置的方式与非 vPar 环境相同。例如，提示符可能包含系统的主机名。在主机名和 vPar 名称不同的系统中，你可能仍然希望提示符中包含主机名。不过，如果你愿意，也可以在提示符中包含 vPar 名称。以下是 `.profile` 中包含对 *root* 用户进行一些轻微自定义的部分：

```bash
# Added for prompt, history etc.

HISTFILE=~/sh_history;                export HISTFILE
EDITOR=v1;                            export EDITOR
PS1="`whoami`@`hostname`\n [${PWD}] > "; export PS1
```

这是我通常为 *root* 添加的信息，以提供历史文件信息和提示符。我在这里包含了主机名，这将产生一个包含用户名、主机名和当前工作目录的提示符，如下所示：

```bash
root@actappd1[/.root] >
```

如果你的用户需要看到 vPar 名称，可以在 `.profile` 中将其添加到或替换掉主机名。这是让主机名和 vPar 名称保持一致的另一个优势。然而，如果你的主机名非常令人困惑，用简单的 vPar 名称替换提示符可能对用户更有益。在两种情况下，你的用户设置都不会因 vPar 而改变，因为从用户角度看，vPar 等同于独立的系统。




特定应用程序所需的用户必须在该应用将运行的所有 vPar 上进行配置。由于 vPar 类似于独立的系统，你需要将用户（包括应用程序用户）放置在需要的 vPar 上，而不是其他的 vPar。例如，在一个运行 Broadvision 和 Oracle 的系统上，你需要设置这些应用程序所需的用户。以下展示了运行这两个应用程序的系统中 `/etc/passwd` 的输出：

```
# cat /etc/passwd
root:9Cbj3CYa98pPo1:0:1:/root:/sbin/sh
daemon:*:1:1:/:/sbin/sh
bin:*:2:2:/:/usr/bin:/sbin/sh
sys:*:3:3:/:/sbin/sh
adm:*:4:4:/var/adm:/sbin/sh
uucp:*:5:5:/:/var/spool/uucppublic:/usr/sbin/uucp/uucico
lp:*:9:7:/:/var/spool/lp:/sbin/sh
nuucp:*:11:11:/:/var/spool/uucppublic:/usr/sbin/uucp/uucico
lpd*:*:27:1:ALLBASE:/:/sbin/sh
nobody:*::2:~2:/:/:
www:*:30:31:/:
webadmin:*:40:1::/usr/obam/server/nologinDir:/usr/bin/false
smbmail:*:101:101:DO NOT USE OR DELETE - needed by samba:/home/smbu1.2:/sbin/sh
opc_op:*:777:77:Opc Default Operator:/home/opc_op:/usr/bin/ksh
stssmrp:HFC7D2Xa92Qp9:1108:20:Martin Paul:/home/stssmrp:/bin/ksh
stsserp:/pughbXhY1ah2I:0:3:Martin Paul:/home/stsserp:/bin/ksh
stssgt1f:VarmvXn1wo/T::1185:20:John Fontanilla:/home/stssgtlf:/usr/bin/ksh
phconbv:UzGNSqDTNGtQM:102:20:PB.COM User:/home/phconbv:/usr/bin/ksh
oracle:1i2/OGg/EH2QoE:1012:111:Oracle User:/home/oracle:/bin/ksh
```

请注意文件中最后两个用户，分别属于 Broadvision（*phconbv*）和 Oracle（*oracle*），以及它们各自的主目录。由于这两个应用程序运行在虚拟分区上，必须设置相应的用户。

本章的剩余部分涵盖与用户相关的背景信息。

### 非 vPar 特定章节 - 设置用户和组

正如你可能已经猜到的，在你的 HP-UX 系统上执行系统管理功能很容易：耗时且费力的是规划。设置用户和组也不例外。多亏了 SAM，处理用户和组的大多数操作都变得简单。

这种简单设置有一个例外：HP（通用桌面环境）CDE 自定义。SAM 对 HP CDE 自定义的帮助不大，手动修改 HP CDE 设置也相当棘手。我有第 13 章来协助你进行 HP CDE 自定义。

你需要就用户做出一些基本决策。用户的数据应位于何处？谁需要访问谁的数据，从而定义用户的“组”？用户和应用程序需要哪种特定的启动方式？你的用户偏好哪种 shell？

你需要仔细思考这些重要的用户相关问题。我花大量时间与我的客户一起重新安排用户数据，原因有几点。它不适合整个磁盘（因此，我强烈建议使用逻辑卷管理器或 Veritas 卷管理器）；用户无法自由访问彼此的数据，或者更糟糕的是，用户可以过于自由地访问彼此的数据。

我们将考虑这些问题，但首先，让我们看看添加用户的基本步骤，无论你是手动操作还是依赖 SAM。以下是活动列表：

- 选择要添加的用户名
- 选择用户 ID 号
- 为用户选择组
- 创建 `/etc/passwd` 条目
- 分配用户密码（包括过期选项）
- 选择并创建用户的主目录
- 选择用户将运行的 shell（我强烈推荐使用默认 POSIX shell）
- 将启动文件放置在用户的主目录中
- 测试用户账户

这个列表看起来可能工作量很大，但如果你运行 SAM 并回答问题，就没有什么难的。你做的很多事情都输入在 `/etc/passwd` 文件中，其中存储了所有用户的信息。你可以使用 `/usr/sbin/vipw` 命令向 `/etc/passwd` 文件添加这些条目。图 6-3 是一个 `/etc/passwd` 条目的示例。

```
marty::155:20:Marty P:/home/marty:/usr/bin/sh
|  |  |  |  |  |
|  > shell
|  |  |  |  |
|  > home directory
|  |  |  |  |
|  > optional user info
|  |  |  > group ID (GID)
|  |  > user ID (UID)
|  > password
> name
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_401_0.png)

以下是这些字段的描述：

*name（名称）。* 你分配的用户名。这个名称应该便于用户和系统中的其他用户记忆。在发送电子邮件或从一个用户复制文件到另一个用户时，用户名越容易记忆越好。如果用户在另一个系统上有用户名，你可能希望在你的 HP-UX 系统上分配相同的用户名。一些系统不允许使用漂亮、简单的用户名，因此你可能希望打破与旧系统的僵局，开始在 HP-UX 系统上使用合理、易于记忆的用户名。请记住，用户名不绑定安全性；安全性通过用户密码和文件权限来处理。

*password（密码）。* 这是加密形式的用户密码。如果此字段中出现星号，该账户无法使用。如果为空，用户没有分配密码，只需输入用户名即可登录。我强烈建议每个用户都有一个定期更改的密码。每个系统都有不同的安全需求，但最起码，每个系统上的每个用户都应该有密码。在设置新用户时，你可以通过在密码字段中放入 `*` 来强制用户在首次登录时创建密码。可以在 SAM 中轻松设置密码老化。

良好密码的一些特性包括：

- 至少六个字符，应包含特殊字符，如斜杠 (/)、点 (.) 或星号 (*)。
- 密码不应使用单词。
- 不要使密码具有个人性质，如姓名、地址、喜爱的运动队等。
- 不要使用易于输入的内容，如 123456 或 qwerty。
- 有些人认为拼写错误的单词是可以接受的，但我不建议使用。用于将拼写错误的单词匹配到正确拼写单词的拼写检查程序可用于猜测可能作为密码的拼写错误单词。
- 生成可理解密码的密码生成器效果最好。

*user ID (UID)（用户 ID）。* 用户的标识号。系统上的每个用户都应该有唯一的 UID。UID 没有约定。当你添加用户时，SAM 会为你分配一个 UID，但你始终可以更改它。我建议将 100 以下的 UID 预留给系统级用户。

*group ID (GID)（组 ID）。* 组的标识号。组的成员及其 GID 在 `/etc/group` 文件中。如果你不喜欢分配的 GID，可以更改它，但你可能还必须更改许多文件的 GID。当用户创建文件时，他的 UID 和 GID 都会分配给该文件。这意味着，如果你在同一组的用户创建了许多文件和目录之后才更改 GID，你可能必须更改所有这些元素的 GID。我通常将 10 以下的 GID 保留给系统组。

*optional user info（可选用户信息）。* 在此空间中，你可以输入条目，如用户的电话号码或全名。创建用户时，SAM 会要求你提供此信息。你可以留空，但如果你管理拥有许多用户或网络的系统，你可能希望添加用户的全名和分机，这样如果需要联系他/她，你就有这些信息。（此字段有时称为 GECOs 字段。）

*home directory（主目录）。* 主目录定义了所有用户文件和目录的默认位置。这是登录时的工作目录。

*shell（Shell）。* 这是用户登录时运行的启动程序。Shell 实际上是用户从命令行发出的命令的命令解释器。我建议使用默认 POSIX shell（`/usr/bin/sh`）；但 HP-UX 环境中还有三种传统且流行的 shell：C shell（`/usr/bin/csh`）；Bourne shell（`/usr/old/bin/sh`）；和 Korn shell（`/usr/bin/ksh`）。系统管理员的 Shell 编程在第 6 章中有介绍。

用户主目录的位置是 `/etc/passwd` 文件中的另一个重要条目。你必须为文件的用户“主”目录选择文件系统中用户文件将存储的位置。借助某些先进的网络技术，如 NFS，用户的主目录甚至不一定在物理连接到他/她正在使用的计算机的磁盘上！在 HP-UX 11.x 中，在 HP-UX 系统上定位用户主目录的传统位置是 `home` 目录。

就增长而言，`home` 目录通常是动态性最大的区域。用户经常在主目录中创建和删除文件。这意味着你必须在用户区域比在更静态的区域（如根文件系统和应用区域）进行更多规划。你通常加载 HP-UX 和你的应用程序，然后对它们进行相对较少的访问，就添加和删除文件和目录而言。用户区域不断更新，使其更难维护。

### 将用户分配给组

在定义所有用户相关信息后，你需要考虑组。在 HP-UX 环境中，组通常被忽视，直到系统管理员发现他/她的所有用户都在同一个组中，甚至



尽管从组织角度来看，它们属于不同的组。

在一般性地介绍组之前，让我们先看看一个属于某个用户的文件以及该文件访问权限的定义方式：

```
$ ls -l
-rwxr-x---x    1    marty     users          120    Jul 26    10:20    sort
```

对于系统中的每个文件，HP-UX 支持三类访问权限：

- 用户访问权限 (u)。授予文件所有者访问权限
- 组访问权限 (g)。授予与文件所有者属于同一组的成员访问权限
- 其他访问权限 (o)。授予其他所有用户

这些访问权限由在发行长目录列表命令时 `r` (读)、`w` (写) 和 `x` (执行) 的位置来定义。对于上述的长目录列表 (`ls -l`)，你可以在表 6-1 中看到相应的权限。

### 表 6-1 长目录列表权限

|  | 访问权限 | 用户访问权限 | 组访问权限 | 其他 |
|---|---|---|---|---|
| 读 | r | r | - | - |
| 写 | w | - | - | - |
| 执行 | x | x | x | x |

可以看出，访问权限是以三组一组的方式排列的。存在三组权限，每组有三个访问级别。在此例中，所有者 *marty* 被允许对该文件具有读、写和执行权限。*users* 组中的任何成员都被允许对该文件具有读和执行访问权限。其他用户仅被允许对该文件具有执行访问权限。

在将用户组织到组时，仔细考虑这些权限非常重要。如果多个用户需要访问相同的文件，那么你可能希望将这些用户放在同一个组中。这里的权衡在于，你可以授予组内所有用户对文件的 `rwx` 访问权限，但这会带来多个用户在其他用户不知情的情况下编辑文件的风险，从而导致混乱。另一方面，你可以创建文件的多个副本，以便每个用户都有他或她的个人副本，但这样就会有文件的多个版本。如果可能，应根据其工作内容将用户分配到不同的组。

当你运行 SAM 并指定每个用户所属的组时，*etc/group* 文件会被更新。*etc/group* 文件包含组名、加密密码（很少使用）、组 ID 以及该组中用户的列表。下面是一个 *etc/group* 文件的示例：

```
root::0:root
other::1:root, hpdh
bin::2:root,bin
sys::3:root,uucp
adm::4:root,adm
daemon::5:root,daemon
mail::6:root
lp::7:root,lp
tty::10:
uucp::11:uuucp
military::25:jhunt,tdolan,vdallesandro
commercial::30:ccascone,jperwinc,devers
nogroup::*:-2:
```

这个 *etc/group* 文件显示了两个不同的用户组。尽管所有用户都运行相同的应用程序——一个桌面发布工具，但一些用户处理“commercial”（商业）产品的文档，而另一些用户只处理“military”（军事）文档。系统管理员创建两个组是有道理的，一个用于商业文档制作，另一个用于军事文档制作。组的所有成员都知道当前有哪些文档，并尊重彼此的工作及其重要性。如果你的组成员彼此了解对方在做什么，你会在组成员之间遇到较少的麻烦，你会发现这些成员不会删除不应被删除的文件。然而，如果你将所有用户放入一个组中，你可能会发现你花费更多的时间来恢复文件，因为在这个更广泛的组中，用户不认为属于其组内其他成员所有的文件很重要。用户可以使用 **newgrp** 命令更改组。

### 用于管理用户的 NIS

在分布式环境中管理用户相关信息最流行的方法之一是网络信息系统 (NIS)。NIS 提供了一种方法，让多个系统共享集中式数据库，包括密码、组以及其他可选数据库，如服务和/或主机。通过这样做，用户账户的管理对于终端用户和系统管理员来说都变得简化了。你也会经常听到 NIS 被称为“黄页”或“YP”；事实上，大多数 NIS 命令都以“yp”开头。

只有在用户需要在许多系统上进行管理的分布式环境中，才需要 NIS 和其他此类技术。这是因为信息变更，如添加和删除用户，必须传播到许多系统。在集中式环境中，通常不需要这样做，因为只需维护此类信息的一小份副本。

HP-UX 上的 NIS 与 Solaris 和 Sun 授权的 NIS 实现（包括 Linux）具有互操作性。与大多数此类实现一样，HP 的 NIS 未在 C2 或可信系统模式下实现。此外，基于 Microsoft 的操作系统，如 Windows，不使用或与 NIS 互操作。

#### NIS 管理什么？

NIS 可以管理许多不同的数据库。我们将重点关注用户密码和组信息。表 6-2 列出了 NIS 可以管理的一些数据库：

| 文件名 | 文件中包含的信息 |
|---|---|
| /etc/passwd | 用户名、用户 ID、主要组和加密密码。 |
| /etc/group | 用户组成员资格。 |
| /etc/hosts | 主机名和 IP 地址。 |
| /etc/services | 网络端口号和服务名称。 |
| /etc/aliases | 邮件系统的别名和邮件列表。 |
| /etc/netgroup | Netgroup 定义。 |
| /etc/rpc | 远程过程调用程序编号。 |
| /etc/protocols | 网络协议名称和编号。以下对于 HP 来说是可选的，但不被 HP-UX NIS 客户端使用。 |
| /etc/bootparms | 关于无盘节点的信息。 |
| /etc/ethers | 以太网数字（MAC 地址）。 |
| /etc/netmasks | 网络掩码。 |

NIS 还将每个这些数据库称为一个*映射* (map)。之所以称为映射，是因为 NIS 允许你将一个键（如用户名）映射到一个值字段，例如 NIS 主服务器上的 **passwd** 映射中用户的 **passwd** 条目。

### 我如何为 NIS 做规划？

NIS 需要一个 NIS 主服务器，以及通常每个 IP 子网至少一个 NIS 从服务器。当用户登录时，NIS 主服务器或从服务器通常会响应来自 NIS 客户端的请求，以获取用户密码信息。NIS 是按照“自上而下”或分层的方式设计的，所有更改都是通过 NIS 主服务器进行的。当对 NIS 主服务器进行修改时，可以通过将更新的数据库“推送”到从服务器，使更改对 NIS 从服务器可见。通常，一个 NIS 服务器应满足 25 到 50 个 NIS 客户端的需求。NIS 主服务器和从服务器通常也是 NIS 客户端。

在 NIS 主服务器上，你需要决定在哪里保存 NIS 数据库的“源”文件。通常，除了密码外，NIS 主服务器上的所有数据库都使用 /etc 文件，密码通常被放入“备用”或“专用”密码文件中，如 /etc/passwd.nis。只在那里放置用户密码数据库，而不放置“系统”用户，如 root、sys、bin 等。“系统”用户在任何 NIS 服务器或客户端上都应始终放在 /etc/passwd 中。

NIS 会在 NIS 从服务器和主服务器上提供少量的额外网络和系统负载。最常见的是，在更新映射或数据库并将更改推送到从服务器时遇到这些额外负载。

NIS 的设计要求你先配置 NIS 主服务器，然后配置 NIS 从服务器，最后配置 NIS 客户端。

### 我如何配置 NIS 主服务器或从服务器？

你可以通过使用 SAM 或手动执行该过程来配置 NIS 主服务器和从服务器。如果你使用 SAM 执行此过程，大部分工作将在后台为你完成。你输入相关信息，SAM 执行配置。你执行手动过程中的步骤。有许多好的文档可以帮助你在这一配置中，包括 HP 的 *Installing and Administering NFS Services* 手册。这本手册涵盖了主服务器和从服务器的配置，可以从 www.dcs.hp.com 获取。HP 支持喜欢当你遵循这些逐步程序，这样如果你遇到问题，他们就可以审查你执行步骤的过程。

要使用 SAM 配置，选择 *Networking/Communications*，然后选择 NIS。首先，系统会提示你指定 NIS 域名。之后，你可以继续进入 *启用 NIS 主服务器* 或 *启用 NIS 从服务器* 菜单。




#### 如何配置 NIS 客户端？

你还可以通过使用 SAM 或手动操作来配置 NIS 客户端。同样，《安装和管理 NFS 服务》手册提供了配置客户端的出色逐步操作指南。

要通过 SAM 进行配置，请选择 *网络/通信*，然后选择 NIS。首先系统会提示你指定 NIS 域名。之后，你可以继续进入 *启用 NIS 客户端* 菜单。

无论哪种方式，我有两点额外的建议。首先，HP 提供了以下 `/etc/nsswitch.compat` 文件作为模板，供你复制到 `/etc/nsswitch.conf`。这允许你在 `/etc/passwd` 和 `/etc/group` 中使用“+”和“-”语法：

```
# /etc/nsswitch.compat:
# An example file that could be copied over to
# /etc/nsswitch.conf; it
# uses NIS (YP) in conjunction with files. #

passwd:		compat
group:		compat
hosts:		nis [NOTFOUND=return] files
networks:		nis [NOTFOUND=return] files
protocols:		nis [NOTFOUND=return] files
rpc:		nis [NOTFOUND=return] files
publickey:		nis [NOTFOUND=return] files
netgroup:		nis [NOTFOUND=return] files
automount:		files nis
aliases:		files nis
services:		files nis
```

其次，你可能更倾向于使用 DNS 而非 NIS 来管理主机数据库，并在 `/etc/nsswitch.conf` 中使用以下“hosts”条目：

```
hosts:		files [NOTFOUND=continue] dns ...
```

或者

```
hosts:		dns	[NOTFOUND=continue,UNAVAILABLE=continue]
			files [NOTFOUND=continue,UNAVAILABLE=continue] nis
```

#### 如何维护我的 NIS 环境？

最常见的用户操作是更改用户密码。用户可以使用 **passwd -r nis** 或 **yppasswd** 命令来执行此操作。这将提示输入旧的 NIS 密码、新密码，在 NIS 服务器上执行更改，并且默认情况下会重新制作 NIS 映射并将其推送到所有从服务器（Slave Servers）。

系统管理员可以通过 SAM、shell 脚本或命令（如 `passwd -r nis <username>` 或 `yppasswd <username>`）来更改用户密码。你还可以使用 SAM 添加新用户，或者通过 shell 脚本或命令来完成此操作。

通常，当用户通过 **vi** 编辑修改数据库文件时，如果需要将更改编译到 NIS 映射中（称为“制作”映射），并且“make”操作未自动完成此任务，则还需将映射推送到从服务器。例如，在修改了 `/etc/passwd.nis` 中某些用户的主目录后，系统管理员需要：

1. `cd /var/yp` # 切换到 NIS Makefile 所在目录
2. `make passwd` # “制作”或编译 passwd 映射
3. `yppush passwd` (如果步骤 #2 未推送到 NIS 从服务器)

这里有一个适用于 HP-UX 及任何 NIS 厂商实现（涉及分组文件）的技巧。有时用户属于多个组，导致 `/etc/group` 中的行长度超过 NIS 每行 1024 个字符的限制。为了绕过此限制，请使用不同的组名来表示相同的 GID，例如：

```
102 support:brian,sam,charlie
102 support1:bill,julie,maria
```

请注意，你不需要在 `/etc/group` 中指定用户的主要组成员资格，因为这在 `/etc/passwd` 中已通过其 GID 指定。如果用户属于多个组，你只需在 `/etc/group` 条目中将其用户名添加到他们的次要组中即可。

NIS 提供了一种集中式数据库方案，用于管理用户密码和组信息。用于 NIS 设置和管理的行政管理技术文档齐全，已集成到 SAM 中，并且通常与其他 NIS 实现具有互操作性。

## 第 7 章

## 备份

## 虚拟分区备份

虚拟分区（Virtual Partitions, vPar）的备份方式与非 vPar 系统几乎相同。主要区别在于，你不需要在物理系统上运行一次备份，而是必须对物理系统上存在的每个虚拟分区运行备份。你还必须对每个虚拟分区运行 **make_net_recovery**。这将为该虚拟分区创建一个可引导的恢复存档。这在 Ignite/UX 第 10 章中进行了介绍。

我们将对系统中第一个 vPar 执行备份，该系统的磁带驱动器已配置为其组件之一（这是备份到本地磁带驱动器）。然后，我们将对同一台计算机上的第二个 vPar 执行备份，目标是配置在第一个 vPar 上的磁带驱动器（这是备份到远程磁带驱动器）。磁带驱动器对于第二个 vPar 来说是远程的，因为它未将磁带驱动器配置为其 I/O 组件之一。由于两个 vPar 是独立且不同的系统，第一个 vPar 上的磁带驱动器对于第二个 vPar 来说是远程的。

![](img/eff8b9287a5f38c5adf538f24aacf29e_412_0.png)

### 备份到本地虚拟分区上的磁带驱动器

现在让我们将名为 *cable1* 的 vPar 备份到位于路径 *0.0.1.0.3.0* 的本地 DDS 驱动器。这是将 vPar 备份到本地磁带驱动器，意味着磁带驱动器资源与执行备份的 vPar 绑定。下面的 **vparstatus** 显示位于 *0.0* 的本地总线适配器（LBA）专门分配给 *cable1*：

```
# vparstatus -p cable1 -v

[Virtual Partition Details]
Name:	cable1
State:		Up
Attributes:	Dynamic,Manual
Kernel Path:	/stand/vmunix
Boot Opts:

[CPU Details]
Min/Max:	1/3
Bound by User [Path]:
Bound by Monitor [Path]:	33
Unbound [Path]:	97

[IO Details]
						<-- path of Core I/O card
0.0.0.0
	0.0.1.2.0	BOOT
0.0.4.0	CONSOLE

[Memory Details]
Specified [Base	/Range]:
		(bytes)	(MB)
Total Memory (MB):	1024
#
```

虽然位于 *0.0.1.0.3.0* 的磁带驱动器未在此 **vparstatus -v** 输出中显示，但磁带驱动器连接到位于 *0.0* 的核心 *I/O* 卡，因此 *cable1* 可以访问它并将其用作备份设备。

顺便提一下，如果磁带接口不在专用于 *cable1* 的核心 *I/O* 卡上，我们可以将接口从 *cable1* 移动到同一台计算机上名为 *cable2* 的第二个 vPar，确认驱动程序在 `/stand/system` 中，然后备份 *cable2*。

由于你可能想要在系统中运行的 vPar 之间移动许多设备，因此务必确保你的内核中包含了支持这些设备所需的所有设备驱动程序。

现在让我们运行 **fbackup**，使用 `-u` 更新备份数据库，`-O` 执行完整备份，`-f` 指定我们要写入备份的目标文件，`-g` 指定我们的图文件，`-I` 指定索引文件的名称，最后，我们将消息重定向到一个包含备份日志的文件。我们将把日期和时间附加到索引文件和备份日志文件的末尾。

以下示例显示了发出的 **fbackup** 命令：

```
fbackup -Ou -f /dev/rmt/0m -g /tmp/backupgraph -I
    /tmp/backupindex.`date '+%y%m%d.%H:%M'` 2>
    /tmp/backuplog.`date '+%y%m%d.%H:%M'`
```

图文件用于指定要包含在备份中的文件。索引文件包含作为备份一部分生成的文件列表。图文件包含我们希望作为备份一部分包含（i）或排除（e）的文件。在我们的情况下，该文件仅包含以下行：

```
i /var/tmp
```

现在让我们看看发出此命令后生成了哪些文件。首先查看备份索引和备份日志文件：

```
# ls -l /tmp/backup*
-rw-rw-rw- 1 root sys   11 Aug 29 14:45 backupgraph
-rw------- 1 root sys  778 Aug 29 15:08 backupindex.010829.15:08
-rw-rw-rw- 1 root sys  521 Aug 29 15:08 backuplog.010829.15:08
#
```

```
# cat /tmp/backupindex.010829.15:08
1024      1 /var
1024      1 /var/tmp
1024      1 /var/tmp/aaaa04686
108       1 /var/tmp/ems_inittab.old
1241      1 /var/tmp/election2
28        1 /var/tmp/envd.action5
4106      1 /var/tmp/inetd.conf.old
96        1 /var/tmp/ntp
0         1 /var/tmp/rdsKUBAA02185
0         1 /var/tmp/rdsKWWAA01840
310       1 /var/tmp/sh1649.1
343       1 /var/tmp/sh1649.2
166       1 /var/tmp/sh1649.3
440       1 /var/tmp/sh1649.4
611       1 /var/tmp/swagent.log
0         1 /var/tmp/sysstat_em.fmt
22734848  1 /var/tmp/vmunix.noreloc
#
```

```
# cat /tmp/backupgraph
i /var/tmp
#
```

```
# cat /tmp/backuplog.010829.15:08
fbackup(1417): cannot open the dates file /var/adm/fbackupfiles/dates
for reading
fbackup(1004): session begins on Wed Aug 29 15:08:10 2001
fbackup(3203): volume 1 has been used 1 time(s)
fbackup(3024): writing volume 1 to the output file /dev/rmt/0m
fbackup(1423): WARNING: could not open the dates file /var/adm/fbackup-
files/dates for writing
fbackup(1030): warnings encountered during backup
fbackup(3055): total file blocks read for backup: 44432
#
```

这两个在文件名末尾附加了日期 *(2001年8月29日 15:08)* 的文件是由之前发出的 **fbackup** 命令生成的。附加在文件末尾的日期有助于备份文件的组织。我们可以使用 **frestore** 恢复其中任意或所有文件。

将 vPar *cable1* 备份到本地磁带驱动器，这是对主机名为 *cvhdcn3* 的系统的备份。在此系统上运行的另一个 vPar *cable2* 未包含在备份中，因为其主机 *cvhdcn4* 被视为一个独立的系统。在下一节中，我们将看到如何备份 *cable2* 到专门分配给 *cable1* 的磁带驱动器。

### 备份到不同本地虚拟分区上的磁带驱动器

上一节中的磁带驱动器连接到 *cable1* 并用于备份 *cable1*。现在让我们使用 *cable1* 虚拟分区中的磁带驱动器来备份 *cable2*。请记住，具有主机名...


## 备份到不同本地虚拟分区中的磁带驱动器

cvhdc4 是一个独立于 cable1 及其主机名 cvhdc3 的系统。因此，我们需要将 vPar cable2 备份到 cable1 上的远程磁带驱动器。

我们将使用 fbackup 备份到连接到 cable1 的远程磁带，指定我们要保存文件的系统名称以及磁带驱动器（或文件）。以下示例使用了本章稍后在非 vPar 特定部分中介绍的 fbackup 选项。我们连接到 cable2，并指定将其备份到 cable1（主机名 cvhdc3）上的磁带驱动器。下面的 fbackup 命令将执行到远程磁带驱动器的备份：

```
# fbackup -f cvhdc3:/dev/rmt/0m -i /var/tmp -v

fbackup(1004): session begins on Wed Aug 29 16:09:28 2001
fbackup(3307): volume 1 has been used 6 time(s) (maximum: 100)
fbackup(3024): writing volume 1 to the output file cvhdc3:/dev/rmt/0m
1:    2: /tmp
3: /tmp/.AgentSockets
4: /tmp/.AgentSockets/A
5: /tmp/X11_newFonts.log
6: /tmp/install.vars
7: /tmp/11database.dat
8: /tmp/2dst#found
9: /tmp/portmap.file
10: /tmp/rpcbind.file
11: /tmp/sd_ipd_acl.1417
12: /tmp/services
13: /tmp/swlist
14: /tmp/typescript
fbackup(1055): run time: 17 seconds
fbackup(3055): total file blocks read for backup: 141
fbackup(3056): total blocks written to output file
cvhdc3:/dev/rmt/0m: 0
#
```

即使设备在物理上连接到您正在使用的计算机，将 fbackup 运行到远程设备也需要一点时间来适应。然而，由于两个 vPar 是不同的主机，因此由另一个 vPar 使用的磁带驱动器确实被视为远程设备是有道理的。

fbackup 通过网络从 cable2 传输到 cable1。这是您希望系统中的每个 vPar 都配备网卡的原因之一。

我们也可以发出其他远程备份命令。以下示例展示了在 cable2 上运行 cpio 并将其发送到 cable1（主机名 cvhdc3）上的磁带驱动器：

```
# find . -print | cpio -oBv | (remsh cvhdcon3 dd of=/dev/rmt/0m)

.
lost+found
.AgentsSockets
Socket <.AgentSockets/A> not backed up
typescript
install.vars
swlist
X11_newfonts.log
sd_ipd_acl.1417
services
rpcbind.file
portmap.file
lldb.base.dat
140 blocks
140+0 records in
140+0 records out
#
```

此命令通过将文件发送到系统 cvhdcon3（vPar cable1）上的磁带驱动器，从而完成对 vPar cable2 上 /tmp 的备份。

### 使用 SAM 备份虚拟分区

我们对 cable1 和 cable2 所做的所有备份工作都可以通过 SAM 完成。这包括将 cable2 备份到 cable1 上的远程磁带驱动器。

让我们首先使用 SAM 中的“备份和恢复 - 交互式备份和恢复”功能对 cable1 执行备份。图 7-1 是 CDE 屏幕截图，展示了与 cable1 交互式备份和恢复相关的部分 SAM 窗口：

![](img/eff8b9287a5f38c5adf538f24aacf29e_418_0.png)

图 7-1 cable1 的交互式备份和恢复

图 7-1 中的所有 SAM 窗口顶部均显示主机名 cvhdcn3，对应于 vPar cable1。左上角的窗口显示，作为 cable1 vPar 配置一部分的 DDS 驱动器被选为备份设备。右下角的窗口是我们可以指定备份范围的地方。

使用 SAM 执行这种 cable1 的交互式备份再简单不过了。现在让我们看看是否可以将 cable2 备份到 cable1 上的远程磁带驱动器。请记住，对于 SAM 而言，这两个是完全不同的系统，即使 vPar cable1 和 cable2 运行在同一台计算机上。这意味着将 cable2 备份到 cable1 上的磁带驱动器是远程操作。

我们可以通过两种不同的方式启动 cable2 的备份。第一种方法是在 cable2 上调用 SAM 并指定所有适当的信息。第二种方法是从 vPar cable1 远程运行 SAM。我们选择后者。我们首先从 cable1 指定我们要在其上运行 SAM 的远程系统的名称，如图 7-2 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_419_0.png)

图 7-2 将 vPar cable2 添加为运行 SAM 的远程系统

指定主机名 cvhdcn4 并记下这是 vPar cable2 后，我们按 OK，SAM 将此配置为远程主机。

现在我们可以选择远程主机并像图 7-3 所示那样在其上运行 SAM：

![](img/eff8b9287a5f38c5adf538f24aacf29e_420_0.png)

图 7-3 配置 cable1 上的远程磁带设备用于备份 cable2

图 7-3 中的所有 SAM 窗口现在都显示主机名 cvhdcn4，即 cable2 的远程主机名。右上角的窗口显示，我们已选择 vPar cable2（主机名 cvhdcn4）作为运行 SAM 的远程系统。右下角的窗口显示，我们已选择 cvhdcn3（vPar cable1 的主机名）上的 /dev/rmt/0m 作为备份发生的设备。

此时，我们已完成所有必需的设置，以继续进行到远程磁带驱动器的备份。选择 /var/tmp 作为要备份的目录后，SAM 打开了如图 7-4 所示的窗口，该窗口指示 /var/tmp 的备份正在进行中：

## 交互式备份文件 (cvhcmdi)

完成所需的步骤，然后选择 [Ok] 以执行备份。

- 1. 指定远程备份设备... cvhcmd3:/dev/rst/0e
- 2. 选择备份范围... 已配置为备份选定的文件。
- 3. 设置附加参数... (可选)
- 4. 正在执行备份操作...

![](img/eff8b9287a5f38c5adf538f24aacf29e_421_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_421_1.png)

图 7-4 cable1 的交互式备份和恢复

此备份顺利完成，没有任何问题。

在同一台计算机上对不同 vPar 进行的这项备份工作展示了 vPar 提供的隔离类型。我们在一个 vPar 中执行的工作不会影响另一个 vPar。如果要使用同一台计算机上但属于不同 vPar 的磁带驱动器，我们需要将该磁带驱动器指定为远程设备。如果您习惯于使用 SAM 执行本地和远程备份，只要从 SAM 的角度将不同的 vPar 视为独立的系统，您就可以继续在 vPar 环境中使用 SAM。

本章其余部分提供关于备份程序的背景信息。

## 章节非 vPar 特定部分 - 内置备份程序

大多数 HP-UX 系统管理员采用双重备份策略。首先是使用 Ignite-UX 的 make_recovery 命令创建根卷的启动备份磁带（make_recovery 在第 10 章中有介绍）。其次，使用备份程序备份系统上剩余的数据。在本章中，我将概述几种备份命令。我不会涵盖任何高级备份程序，如 HP 的 OmniBack。不过，高级备份工具可以使集中式备份和备份的整体管理等工作变得更加容易。

以下是我将在后续章节中介绍的备份程序的简要概述：

- **tar**：tar 被广泛认为是备份和恢复程序中可移植性最强的。tar 是最通用的备份实用程序。您会发现许多应用程序都打包在 tar 磁带上。这是与其他 UNIX 系统交换数据最广泛使用的格式。tar 是最古老的 UNIX 备份方法，因此在所有 UNIX 系统上都可以运行。您可以将文件追加到 tar 磁带的末尾，这是 fbackup 无法做到的。当向另一个 UNIX 用户发送文件时，我强烈建议使用 tar。tar 的速度像糖浆一样慢，因此您不会想将其用于完整备份或增量备份。tar 的一个非常理想的特点是，当您使用 tar 将文件加载到磁带上然后恢复到另一个系统时，原始用户和组会被保留。

- **cpio**：cpio 也像 tar 一样可移植且易于使用。此外，cpio 比 tar 快得多 - 没有 fbackup 那么快，但比 tar 快得多。cpio 适用于复制目录树。

- **fbackup**：fbackup 是 SAM 使用的实用程序。它具有许多功能，例如指定备份是完整备份还是增量备份、不同的备份级别、以及要包含或排除的文件和目录。



支持一种*图（graph）*文件，用于指定要包含和排除的文件，以及其他高级功能。**fbbackup** 是一个仅限 HP-UX 使用的实用工具，而磁带只能在 HP-UX 系统上使用 **frecover** 进行读取。

### dd

这是一种逐位复制。它并不“智能”，即不会复制文件和所有权；它只是复制位。因此，与使用 **frecover**、**tar**、**restore** 或 **cpio** 不同，你无法从 **dd** 磁带上选择单个文件。**dd** 主要用于将 EBCDIC 等数据转换为 ASCII。

### dump

**dump** 类似于 **fbbackup**。如果你在 HP-UX 上使用 **fbbackup**，你会发现在使用 **dump** 时也有许多相似之处。**dump** 提供与 **fbbackup** 相同级别的备份方案，并创建 /var/admin/dumpdates，其中列出了文件系统最后一次备份的时间。**restore** 用于读取通过 **dump** 备份的信息。然而，**dump** 仅适用于 HFS 文件系统，而不适用于 VxFS，并且它假设你使用的是卷轴式磁带。

### tar

**tar** 通常被认为是最*可移植*的备份和恢复程序。你会发现许多应用程序是通过 **tar** 磁带分发的，而从 Internet 下载的许多 UNIX 文件都是 **tar** 格式。这是与其他 UNIX 系统交换数据时最常用的格式。**tar** 是最古老的 UNIX 备份方法，因此在所有 UNIX 系统上都能运行。你可以将文件追加到 **tar** 磁带的末尾，这是许多其他程序无法做到的。在将文件发送给另一个 UNIX 用户时，我强烈推荐使用 **tar**。 **tar** 的速度慢得像摩尔糖一样，因此如果你有大量数据需要备份，就不会想用它来进行完整或增量备份。**tar** 的一个非常 desirable 的特点是，当你使用 **tar** 将文件加载到磁带上，然后将其恢复到另一个系统时，原始的用户和组得以保留。

在接下来的示例中，我们将使用几个 **tar** 命令，包括以下命令：

```bash
# tar cf /dev/rmt/0m /var  # 使用 tar 创建 (c) 目录 /var 的归档并将其放到磁带 /dev/rmt/0m 上。
# tar tvf /dev/rmt/0m  # 从磁带 /dev/rmt/0m 获取目录 (t) 并生成详细 (v) 输出。
# tar xvf /dev/rmt/0m  # 提取 (x) 磁带 /dev/rmt/0m 上归档的全部内容到默认目标位置。
# tar xvf /dev/rmt/0m file1  # 仅从磁带 /dev/rmt/0m 上的归档中提取 file1 到默认目标位置。
```

当你查看 **tar** 的手册页时，你会注意到选项前有一个连字符。该命令在没有连字符的情况下也能工作，因此大多数 **tar** 示例，包括本章中的示例，都省略了连字符。

让我们来看看一些使用 **tar** 的示例。首先，让我们对目录 **/var** 执行 **tar** 备份（通常称为*创建归档*），将其备份到磁带设备 **/dev/rmt/0m**。我们使用 *c* 选项来创建备份，并使用 *f* 选项来指定磁带驱动器 **/dev/rmt/0m** 的文件：

```bash
# tar cf /dev/rmt/0m /var
tar: /var/opt/dce/rpc/local/01060/reaper is not a file. Not dumped
tar: /var/opt/dce/rpc/local/00997/reaper is not a file. Not dumped
tar: /var/opt/dce/rpc/local/00997/-c-3/7000 is not a file. Not dumped
tar: /var/opt/dce/rpc/local/00997/-c-3/shared is not a file. Not dumped
tar: /var/opt/dce/rpc/local/8-3/7002 is not a file. Not dumped
tar: /var/opt/dce/rpc/local/8-0/135 is not a file. Not dumped
tar: /var/opt/dce/rpc/local/8-0/2121 is not a file. Not dumped
tar: /var/opt/dce/rpc/local/8-3/135 is not a file. Not dumped
tar: /var/opt/dce/rpc/local/8-3/2121 is not a file. Not dumped
tar: /var/spool/sockets/pwgr/client933 is not a file. Not dumped
tar: /var/spool/sockets/pwgr/client1028 is not a file. Not dumped
tar: /var/spool/sockets/pwgr/client1152 is not a file. Not dumped
tar: /var/spool/sockets/pwgr/client1172 is not a file. Not dumped
tar: /var/spool/sockets/pwgr/client1173 is not a file. Not dumped
tar: /var/spool/sockets/pwgr/client1193 is not a file. Not dumped
tar: /var/spool/sockets/pwgr/client2500 is not a file. Not dumped
tar: /var/spool/sockets/pwgr/client2592 is not a file. Not dumped
tar: /var/spool/sockets/pwgr/client2490 is not a file. Not dumped
tar: /var/spool/sockets/pwgr/client2593 is not a file. Not dumped
tar: /var/spool/pwgr/daemon is not a file. Not dumped
#
```

此命令的结果仅将问题相关消息打印到*标准输出*。你经常会看到 **tar** 使用 *v* 选项来生成详细输出，这将列出上述消息以及成功写入磁带归档的文件的相关消息。

接下来，让我们只查看磁带上包含字符串 *eaaa* 的文件。为了生成目录，我们将使用 *t* 选项。以下示例还使用 *v* 进行详细输出：

```bash
# tar tvf /dev/rmt/0m | grep eaaa
-rw-rw-rw- 0/3 28 Jul 11 15:37 2000 /var/tmp/eaaa01299
-rw-rw-rw- 0/3 28 Jul 11 15:37 2000 /var/tmp/eaaa01333
-rw-rw-rw- 0/3 28 Jul 11 15:38 2000 /var/tmp/eaaa01354
-rw-rw-rw- 0/3 28 Jul 11 15:40 2000 /var/tmp/eaaa01380
-rw-rw-rw- 0/3 28 Jul 11 15:40 2000 /var/tmp/eaaa01405
-rw-rw-rw- 0/3 28 Jul 11 15:45 2000 /var/tmp/eaaa01487
#
```

此输出显示了磁带上以 *eaaa* 开头的几个文件。我们将使用 *x* 选项从 **tar** 归档中提取文件，从计算机上删除最后一个此类文件，并将其从磁带中恢复。然后，我们将列出系统上的目录，以确认我们从磁带上恢复的已删除文件已回到目录中。

```bash
# rm /var/tmp/eaaa01487
# tar xvf /dev/rmt/0m /var/tmp/eaaa01487
x /var/tmp/eaaa01487, 28 bytes, 1 tape blocks
# ls -l /var/tmp/eaaa*
drw-rw-rw-   1 root     sys       28 Jul 11 15:37 /var/tmp/eaaa01299
-rw-rw-rw-   1 root     sys       28 Jul 11 15:37 /var/tmp/eaaa01333
-rw-rw-rw-   1 root     sys       28 Jul 11 15:38 /var/tmp/eaaa01354
-rw-rw-rw-   1 root     sys       28 Jul 11 15:40 /var/tmp/eaaa01380
-rw-rw-rw-   1 root     sys       28 Jul 11 15:40 /var/tmp/eaaa01405
-rw-rw-rw-   1 root     sys       28 Jul 11 15:45 /var/tmp/eaaa01487
#
```

这种使用 **tar** 进行备份和恢复很简单，并且能够完成工作。

**tar** 的一个常见用途是从一个目录备份文件并恢复到另一个目录。我们将备份 **/var/tmp** 的内容并将其恢复到目录 **/tmp/puttarfilesHere**。在以下示例中，我们将创建一个 **tar** 备份归档到文件，而不是磁带。该文件名为 **tartest**。然后，我们将此文件移动到目标目录并在那里提取它。在这个示例中，我们完全没有使用磁带。

```bash
# cd /var/tmp
# ls -l
total 72
-rw-rw-rw-   1 root     sys      0 Jul 11 15:57 OBAMPEaa01630
-rw-rw-rw-   1 root     sys      0 Jul 11 15:20 OBAMHBAa01020
-rw-rw-rw-   1 root     sys      0 Jul 11 15:50 OBAMHBaa01540
-rw-rw-rw-   1 root     sys     102 Jul 11 15:20 aaaa01112
-rw-rw-rw-   1 root     sys     102 Jul 11 15:37 aaaa01299
-rw-rw-rw-   1 root     sys     102 Jul 11 15:38 aaaa01333
-rw-rw-rw-   1 root     sys     102 Jul 11 15:38 aaaa01354
-rw-rw-rw-   1 root     sys     102 Jul 11 15:40 aaaa01380
-rw-rw-rw-   1 root     sys      99 Jul 11 15:40 aaaa01405
-rw-rw-rw-   1 root     sys      28 Jul 11 15:17 aaaa01333
-rw-rw-rw-   1 root     sys      28 Jul 11 15:38 aaaa01354
-rw-rw-rw-   1 root     sys      28 Jul 11 15:40 aaaa01380
-rw-rw-rw-   1 root     sys      28 Jul 11 15:40 aaaa01405
-rwxr-xr-x   1 root     root      28 Jul 11 15:45 aaaa01487
-rwxr-xr-x   1 root     root      28 Jul 11 16:04 envd.action2
-rwxr-xr-x   1 root     root      28 Jul 11 16:04 envd.action5
-rw-r--r--   1 root     root       96 Jul 11 13:50 ntp
-rw-------   1 root     root      600 Jul 11 15:27 swagent.log
# tar cvf /tmp/tartest .
 a OBAMPEaa01630 0 blocks
 a OBAMHBAa01020 0 blocks
 a OBAMHBaa01540 0 blocks
 a aaaa01112 1 blocks
 a aaaa01299 1 blocks
 a aaaa01333 1 blocks
 a aaaa01354 1 blocks
 a aaaa01380 1 blocks
 a aaaa01405 1 blocks
 a aaaa01487 1 blocks
 a envd.action2 1 blocks
 a envd.action5 1 blocks
 a swagent.log 2 blocks
#
# cd /tmp
# mkdir puttarfilesHere
# cp tartest puttarfilesHere
# cd puttarfilesHere
# ls -l
total 80
-rw-rw-rw- 1 root sys 40960 Jul 11 17:09 tartest
#
# tar xvf tartest
x OBAMPEaa01630, 0 bytes, 0 tape blocks
x OBAMHBAa01020, 0 bytes, 0 tape blocks
x OBAMHBaa01540, 0 bytes, 0 tape blocks
x aaaa01112, 102 bytes, 1 tape blocks
x aaaa01299, 102 bytes, 1 tape blocks
x aaaa01333, 102 bytes, 1 tape blocks
x aaaa01354, 102 bytes, 1 tape blocks
x aaaa01380, 102 bytes, 1 tape blocks
x aaaa01405, 99 bytes, 1 tape blocks
x aaaa01487, 28 bytes, 1 tape blocks
x envd.action2, 28 bytes, 1 tape blocks
x envd.action5, 28 bytes, 1 tape blocks
x swagent.log, 600 bytes, 2 tape blocks
#
```




### cpio

**cpio** 是一款功能强大的实用工具，通常与 **find** 配合使用，以执行完全备份和增量备份。**cpio** 是一个成熟的 UNIX 实用工具，在大多数 UNIX 变体上都能以类似的方式工作。

在下面的示例中，我们将使用几条命令，包括以下内容：

- `# find . -print | cpio -oBv > /dev/rmt/0m` ;; 查找当前目录的内容并将其写入磁带。
- `# cpio -it < /dev/rmt/0m` ;; 读取磁带的内容表 (t)。
- `# cpio -icvBdum < /dev/rmt/0m` ;; 恢复 (i) 磁带的内容，这是最广泛使用的 cpio 命令。
- `# find . -print | cpio -oBv | (remsh tapesys dd of=/dev/rmt/0m)` ;; 查找当前目录的内容并将其写入 (o) 远程机器 tapesys 上的磁带。
- `# remsh tapesys "dd if=/dev/rmt/0m bs=8k" | cpio -icvBdum` ;; 将远程系统 tapesys 上磁带的内容 (i) 恢复到本地系统。

我们将发出的第一条命令是 **find**（查找）/var/tmp 中的内容并将其写入我们的磁带设备 /dev/rmt/0m。以下示例中使用的 **cpio** 选项为：*o* 表示输出模式，*B* 表示块输出，*v* 表示详细报告：

```bash
# cd /var/tmp
# find . -print | cpio -oBv > /dev/rmt/0m
(Using tape drive with immediate report mode enabled (reel #1)).
envd.action2
envd.action5
swagent.log
ntp
OBAMHBAa01020
aaaa01558
aaaa01426
aaaa01112
OBAMHBAa01540
aaaa01299
...
aaaa01487
OBAMFEAa01630
cmd_res8215
tmp_cfg_file
cmd_res8708
exclude.temp
arch.include.1
3570 blocks
#
```

在该示例中，我们首先将目录更改为 `/var/tmp`，然后执行 `find` 命令并将其输出通过管道传递给 `cpio`。`cpio` 几乎总是像示例中那样与 `find` 配合使用。由于我们在发出备份命令之前更改到了目录 `/var/tmp`，因此生成了具有相对路径名称的备份。

接下来，我们将查看磁带的内容，以确认我们使用 `cpio` 写入的文件。`i` 选项用于输入，`t` 选项用于在以下列表获取内容表：

```bash
# cpio -it < /dev/rmt/0m

envd.action2
envd.action5
swagent.log
ntp
OBAMHBAa01020
aaaa01558
aaaa01426
aaaa01112
OBAMHBAa01540
aaaa01299
...
ea_aa01487
OB_AMFE_aa01630
cmd_res8215
tmp_cfg_file
cmd_res8708
excl_ude_temp
arch_incl_ude_l
3570 blocks
#
```

既然我们已将内容写入磁带并查看了其内容表，接下来我们将恢复 /var/tmp 的内容。在以下示例中，我们对 `cpio` 使用了几个选项，包括：`i` 表示输入模式，`c` 表示 ASCII 头部格式，`v` 表示详细模式，`B` 表示块输出，`d` 表示目录，`u` 表示无条件覆盖现有文件，以及 `m` 表示恢复原始修改时间：

```bash
# cpio -icvBdum < /dev/rmt/0m
.
envd_action2
envd_action5
swagent_log
ntp
OB_AMHB_AA01020
aaaa01558
aaaa01426
aaaa01112
OB_AMHB_AA01540
aaaa01299
.
.
.
.
.
ea_aa01487
OB_AMFE_aa01630
cmd_res8215
tmp_cfg_file
cmd_res8708
excl_ude_temp
arch_incl_ude_l
3570 blocks
#
```

**cpio** 命令生成将从磁带读取并恢复到系统的文件列表。由于我们包含了详细选项，我们将看到与恢复相关的所有信息。

既然我们已经了解了如何在本地系统上写入磁带、生成内容表以及读取磁带内容，让我们处理一下远程系统上的磁带驱动器。我们将执行向远程磁带驱动器进行备份，查看磁带上的内容表，然后使用远程磁带驱动器进行恢复。

首先，让我们执行向远程磁带驱动器的备份。本地系统没有连接磁带驱动器，它是 *orl*。远程系统连接了磁带驱动器，它是 *tapesy*。我们将在 *orl* 上运行 **cpio**（使用前面描述的相同的三个选项），并在 *tapesy* 上运行远程 shell 和 **dd**，这将存储备份的内容。在以下示例中，我们将在 *orl* 的 */var/tmp* 中运行这些命令：

```bash
# find . -print | cpio -oBv | (remsh tapesy dd of=/dev/rmt/0m)

. 
envd.action2 
envd.action5 
swagent.log 
ntp 
OBAMHBAA01020 
aaaa01558 
aaaa01426 
aaaa01112 
OBAMHBAA01540 
aaaa01299 
:
:
:
aaa01487 
OBAMPEAA01630 
cmd_res8215 
tmp_cfg_file 
cmd_res8708 
exclude.temp 
arch.include.l 
3570 blocks 
#
```

现在让我们回到没有磁带驱动器的本地系统，恢复我们刚刚生成的 **cpio** 磁带的内容，但让我们将它们恢复到不同的目录。我们将磁带内容（最初在 /var/tmp）恢复到的目录是 /tmp/remoteepiofiles。这类似于本章前面 tar 部分中我们执行的过程，当时我们将 tar 文件恢复到了不同的位置。

在以下示例中，我们在 or1 上发出了一系列命令。这些命令中的最后一条是向系统 tapesys 发出 remsh，该系统上有一个装载了我们刚刚创建的 cpio 磁带的磁带驱动器。我们 dd 信息并通过 cpio 管道传输以恢复磁带的内容。在此示例中，我们对 cpio 使用了相同的恢复选项，包括：i 表示输入模式，c 表示 ASCII 头部格式，v 表示详细模式，B 表示块输出，d 表示目录，u 表示无条件覆盖现有文件，以及 m 表示恢复原始修改时间：

```bash
# hostname
or1
# cd /tmp
# mkdir remoteepiofiles
# cd remoteepiofiles
# pwd
/tmp/remoteepiofiles
# remsh tapesys "dd if=/dev/rmt/0m bs=8k" | cpio -icvBdum
envd.action2
envd.action5
swagent.log
ntp
OBAMHBAA01020
aaaa01558
aaaa01426
aaaa01112
OBAMHBAA01540
aaaa01299
.
.
.
aaaa01487
OBAMPEAA01630
cmd_res8215
tmp_cfg_file
cmd_res8708
exclude.temp
arch.include.1
3570 blocks
#
# pwd
/tmp/remoteepiofiles
# ls
envd.action2
enwd.action5
swagent.log
ntp
OBAMHBaa01020
aaaa01558
aaaa01426
aaaa01112
OBAMHBAA01540
aaaa01299
.
.
.
.
eaaa01487
OBAMFEAa01630
cmd_res8215
tmp_cfg_file
cmd_res8708
exclude.temp
arch.include.l
#
```

我们在该示例末尾发出的 ls 确认我们确实将远程系统上的磁带内容写入到了新目录 /tmp/remotecpiofiles。您可能希望在 ls 选项中添加 -a 命令，以确保文件包含内容。

您可以从本 cpio 部分中的简单示例构建备份和恢复命令，以满足您在适度环境中的需求。

### fbackup 和 frecover

**fbackup** 和 **frecover** 是 HP-UX 上首选的备份和恢复程序。使用 **fbackup** 产生的备份无法移植到其他 UNIX 变体。如果您在异构环境中工作，您将无法在 HP-UX 系统上生成的 **fbackup** 磁带恢复到一个运行不同 UNIX 变体的系统上。

在本节中，我将介绍在命令行上发出 **fbackup** 和 **frecover** 命令。您也可以使用 SAM（在第 3 章中有介绍）使用这些命令来管理备份。SAM 帮助您管理 *自动备份* 和 *交互式备份和恢复*。虽然 **fbackup** 和 **frecover** 是随您的 HP-UX 系统捆绑的最先进的备份和恢复程序，但您的需求可能会超越这些程序。您还可以从 HP 和第三方采购高级备份程序。总体而言，我发现 **fbackup** 和 **frecover** 的功能对于新的 HP-UX 安装已经足够。但是，如果您有一个高度分布的环境，或者需要备份大量数据，需要在运行不同操作系统的系统上执行备份，或者需要同时使用多个备份设备，您可能需要考虑更高级的产品。

**fbackup** 具有执行不同 *级别* 备份的功能。级别定义了要包含在备份中的信息量。完全备份，即本节中介绍的内容，是备份级别 0。其他级别定义了各种程度的增量备份。我是执行完全备份的坚定支持者，然后对自*上次完全备份*以来发生变化的每个文件执行增量备份。这意味着，为了从一个完全“损坏”（这是一个表示*毁坏*的技术术语）的系统恢复，您需要您的完全备份磁带和仅一个增量磁带（您将通过使用 **make_recovery** 生成的可启动 Ignite-UX 磁带恢复根卷，这在第 10 章中有介绍）。例如，如果您在周日执行完全备份，并在周一到周五执行增量备份，那么您需要仅加载周日的完全备份磁带和周五的增量备份磁带即可完全恢复系统。**fbackup** 支持此方案。

请记住，虽然我们将在本章的命令行上发出 **fbackup** 和 **frecover** 命令，但通过 SAM 管理这些命令会更加容易。以下是对 **fbackup** 命令及其*部分*选项的说明：





/usr/sbin/fbackup -f device [-0-9] [-u] [-i path] [-e path] [-g graph]

- `-f device`
  备份使用的磁带驱动器，例如本地磁带驱动器为 `/dev/rmt/0m`。
- `[-0-9]`
  这是备份的级别。如果你在周日执行级别 0 的完全备份，那么在其他工作日你应执行级别 1 的增量备份。增量备份会备份自较低级别备份以来所有更改的信息。你可以在周日执行级别 0，周一执行级别 1，周二执行级别 2，以此类推。然而，为了恢复系统，你需要依次加载周日的磁带，然后周一的磁带，再周二的磁带，等等，才能完全恢复。
- `[-u]`
  此选项更新过去备份的数据库，使其包含诸如备份级别、备份会话的开始和结束时间以及用于备份会话的图形文件（如下所述）等信息。此选项仅在配合 `-g (graph)` 选项时有效。
- `[-i path]`
  指定的路径将包含在备份中。此选项可以指定任意次数。
- `[-e path]`
  指定的路径将从备份中排除。此选项也可以指定任意次数。
- `[-g graph]`
  图形文件包含要包含或排除在备份之外的文件和目录列表。

尽管 fbackup 非常彻底且易于使用，但它并未内置全量备份和增量备份运行的日期和时间。你必须创建一个 cron 条目来自动运行 fbackup。SAM 会为你创建一个 cron 条目，从而让你可以随时运行 fbackup。（cron 在第 11 章中有详细介绍。）

在最简单形式下，我们可以运行 fbackup，并通过 f 选项指定磁带驱动器，通过 i 选项指定要备份的目录，如下例所示：

由于未包含用于详细模式的 v 选项，fbackup 未生成包含在备份中的文件列表。

要查看磁带的内容，我们运行带有 `r`（读取）、`N`（防止磁带内容恢复到系统）和 `v`（详细）选项的 `frecover`，如下面的命令所示：

```bash
# frecover -rNv -f /dev/rmt/0m
drwxr-xr-x    root    root    /
dr-xr-xr-x    bin     bin     /var
drwxrwxrwx    bin     bin     /var
drwxr-xr-x    root    sys     /var/tmp/OBAMFBAa01630
-rw----root    sys     /var/tmp/OBAMHBAa01020
-rw----root    sys     /var/tmp/OBAMHBAa01540
-rw----root    sys     /var/tmp/OBAMHBAa07762
-rw-rw-rw-     root    sys     /var/tmp/aaa01112
...
-rw-rw-rw-     root    sys     /var/tmp/eaa01487
-rwxr-xr-x     root    root    /var/tmp/envd.action2
-rwxr-xr-x     root    root    /var/tmp/envd.action5
-rw-rw-rw-     root    sys     /var/tmp/exclude.temp
dr-xr-xr-x     bin     bin     /var/tmp/ntp
-rw-rr-xr-x     sys     /var/tmp/swagent.log
-rw-rw-rw-     root    sys     /var/tmp/tmf_cfg.file
#
```

现在让我们从系统中删除一个作为备份一部分包含在内的文件。然后我们将只恢复我们删除的那个文件。我们将使用 `x` 选项表示提取，并使用 `i` 选项指定要包含的文件，配合 `frecover` 使用，如下例所示：

```bash
# cd /var/tmp
# ls -1 aa*
-rw-fw-rw- 1 root sys      102 Jul 11 15:20 aaaa01112
-rw-fw-rw- 1 root sys      102 Jul 11 15:37 aaaa01299
-rw-fw-rw- 1 root sys      102 Jul 11 15:37 aaaa01333
-rw-fw-rw- 1 root sys      102 Jul 11 15:38 aaaa01354
-rw-fw-rw- 1 root sys       99 Jul 11 15:40 aaaa01380
-rw-fw-rw- 1 root sys       99 Jul 11 15:40 aaaa01405
-rw-fw-rw- 1 root sys      102 Jul 11 15:47 aaaa01426
-rw-fw-rw- 1 root sys       99 Jul 11 15:45 aaaa01487
-rw-fw-rw- 1 root sys      102 Jul 11 14:24 aaaa01558
# rm aaaa01487
# cd /
# frecover -x -i /var/tmp/aaaa01487 -f /dev/rmt/0m
# cd /var/tmp
# ls -1 aa*
-rw-fw-rw- 1 root sys      102 Jul 11 15:20 aaaa01112
-rw-fw-rw- 1 root sys      102 Jul 11 15:37 aaaa01299
-rw-fw-rw- 1 root sys      102 Jul 11 15:37 aaaa01333
-rw-fw-rw- 1 root sys      102 Jul 11 15:38 aaaa01354
-rw-fw-rw- 1 root sys       99 Jul 11 15:40 aaaa01380
-rw-fw-rw- 1 root sys       99 Jul 11 15:40 aaaa01405
-rw-fw-rw- 1 root sys      102 Jul 11 15:47 aaaa01426
-rw-fw-rw- 1 root sys       99 Jul 11 15:45 aaaa01487
-rw-fw-rw- 1 root sys      102 Jul 11 14:24 aaaa01558
#
```

在上面的示例中，我们使用 frestore 成功地从磁带上恢复了文件 /var/tmp/aaaa01487。

备份有一些强大的功能，我们在示例中并未使用。这些包括备份级别、图形文件和索引文件。backup 支持 0-9 的备份级别，0 用于完全备份，其他数字表示各种增量备份级别。

图形文件用于指定包含在备份中的文件。索引文件包含作为备份一部分生成的文件列表。让我们看一个使用所有这些功能的示例。首先，我们创建一个图形文件，其中包含我们要包含 (i) 或排除 (e) 作为备份一部分的文件。在我们的情况下，该文件将仅包含以下一行：

```text
i /var/tmp
```

现在让我们运行 fbackup，使用 u 更新备份数据库，O 进行完全备份，f 指定我们要写入备份的文件（在此示例中，我们将使用文件而不是磁带），g 指定我们的图形文件，I 指定索引文件的名称，最后，我们将消息重定向到一个包含备份日志的文件。我们还会在索引和备份日志文件的末尾添加日期和时间。

```bash
# fbackup -Ou -f /tmp/testbackup -g /tmp/backupgraph \
-I /tmp/backupindex.`date '+%y%m%d.%H:%M'` 2> /tmp/backuplog.`date '+%y%m%d.%H:%M'`
#
```

现在我们来看看执行此命令后生成了哪些文件。首先让我们查看备份索引和备份日志文件：

```bash
# ls /tmp/backup*
backupgraph
backupindex.000712.15:04
backuplog.000712.15:04
# 
# cat /tmp/backupindex000712.15:04
1024          1 / 
1024          1 /var
2048          1 /var/tmp
0             1 /var/tmp/OBAMFEA01630
0             1 /var/tmp/OBAMHBAO1020
0             1 /var/tmp/OBAMHBAo1540
336           1 /var/tmp/OBAMHBAo7762
102           1 /var/tmp/aaa01112
            .
            .
            .
28            1 /var/tmp/aaaa1487
28            1 /var/tmp/envd.action2
28            1 /var/tmp/envd.action5
4608          1 /var/tmp/exclude.tmp
96            1 /var/tmp/stmp
1595          1 /var/tmp/swagent.log
205           1 /var/tmp/tmp_cfg_file
# 
# cat /tmp/backupgraph000712.15:04
1/var/tmp
# 
# cat /tmp/backuplog000712.15:04

fbackup(1004): session begins on Wed Jul 12 14:56:19 2000
fbackup(3024): writing volume 1 to the output file /tmp/testbackup
fbackup(1030): warnings encountered during backup
fbackup(3055): total file blocks read for backup: 3614
fbackup(3056): total blocks written to output file /tmp/testbackup:3876
#
```

带有日期附加在文件名末尾（7/12/00 时间 15:04）的三个文件是由之前发出的 **fbackup** 命令生成的。附加在文件末尾的日期有助于组织备份文件。我们可以使用 **frestore** 从包含备份信息的文件（*`/tmp/testbackup`*）中恢复其中任意或所有文件，如前所示。

我们并不局限于对连接到本地系统的磁带驱动器进行备份。我们可以通过指定系统名称和磁带驱动器或文件来使用 **fbackup** 备份到远程磁带，将文件存储到我们想要的位置。下面的示例使用了之前介绍的 **fbackup** 选项，并且包含了带有磁带驱动器的系统名称：

```bash
# fbackup -f tapesys:/dev/rmt/0m -i /var/tmp -v
fbackup(1004): session begins on Wed Jul 12 15:56:22 2000
fbackup(3507): volume 1 has been used 1 time(s) (maximum: 100)
fbackup(3024): writing vol 1 to output file tapesys:/dev/rmt/0m
1: /
2: /var
3: /var/tmp
4: /var/tmp/AAAA1812 0
5: /var/tmp/AAAA1992 0
6: /var/tmp/BEQ19522 19
7: /var/tmp/DCB19522 0
8: /var/tmp/DBC19522 0
9: /var/tmp/ISPX19522 0
.
.
.
73: /var/tmp/eaaa13306 1
74: /var/tmp/ems_inittab.old 2
75: /var/tmp/envd.action2 1
76: /var/tmp/envd.action5 1
77: /var/tmp/inet.conf.old 9
78: /var/tmp/net19522 1799
79: /var/tmp/swagent.log 16
fbackup(1005): run time: 43 seconds
fbackup(3055): total file blocks read for backup: 1974
fbackup(3056): total blocks written to output file ori:/dev/rmt/0m: 0
#
```

此命令通过系统将文件发送到系统 *tapesys* 上的磁带驱动器，从而在系统 *or1* 上执行 */var/tmp* 的备份。我们可以使用许多其他选项给 **fbackup**，如前面的示例所示，但我希望保持示例简单，以便容易看出远程磁带驱动器的指定方式。




### dd

**dd** 是一个用于将设备（如磁盘）的内容写入磁带的实用程序。您还可以使用 **dd** 将磁带的映像复制到系统上的文件中，然后查看该文件。

首先，让我们使用 **tar** 将目录的内容写入磁带；然后使用 **dd** 将磁带内容复制为文件。在此示例中，**dd** 唯一需要的选项是 *if*，它指定输入文件为磁带驱动器。

```bash
% cd /var/tmp
# tar cf /dev/rmt/0m ~ `ls`
# cd /tmp
# dd if=/dev/rmt/0m > /tmp/tapecontents
183+0 records in
183+0 records out
# tar tv /tmp/tapecontents
rw-------  0/3      0 Jul 11 15:57 2000 CBAMFEAa01630
rw-------  0/3      0 Jul 11 15:20 2000 CBAMHBAa01020
rw-------  0/3      0 Jul 11 15:50 2000 CBAMHBAa01540
rw-------  0/3    336 Jul 12 13:18 2000 CBAMHBAa07762
rw-------  0/3    102 Jul 12 13:44 2000 CBAMHBAa08333
rw-rw-rw-  0/3    102 Jul 11 15:20 2000 aaaa01112
.
rw-rw-rw-  0/3     28 Jul 11 15:45 2000 esa01487
rwxr-x--  0/0     28 Jul 11 21:53 2000 envd.action2
rwxr-x--  0/0     28 Jul 11 21:53 2000 envd.action5
rw-rw-rw-  0/3    2304 Jul 12 12:42 2000 exclude.temp
r-xr-xr-x  2/2      0 Jul 11 13:50 2000 ntp/
rw-r--r--  0/3    1595 Jul 12 12:23 2000 swagent.log
rw-rw-rw-  0/3     205 Jul 12 12:39 2000 tmp_cfg_file
#
```

现在，我们可以像前面章节所示那样，使用 **tar** 查看文件内容，命令如下：

```bash
# tar tv /tmp/tapecontents
```

**dd** 的另一个常见用途是将远程系统磁带驱动器上的 **cpio** 归档提取到本地系统。在以下示例中，没有磁带驱动器的本地系统是 *orl*，具有磁带驱动器的远程系统是 *tapessys*。我们将使用 **dd** 和 **cpio** 将磁带读取到 *orl* 上的一个目录中（有关选项的解释，请参阅前面的 **cpio** 章节），示例如下：

```bash
# hostname
orl
# pwd
/tmp/remotecpiofiles
# remsh tapessys "dd if=/dev/rmt/0m bs=8k" | cpio -icvBdum
.
envd.action2
envd.action5
swagent.log
ntp
CBAMHBAo01020
aaaa01558
.
.
.
.
aaaa01487
CBAMFEAa01630
cmd_res8215
tmp_cfg_file
cmd_res8708
CBAMHBAb07762
exclude.temp
arch.include.1
3580 blocks
0+358 records in
0+358 records out
#
```

该命令运行远程 shell（**remsh**）以在 *tapessys* 上执行 **dd** 命令。此命令的输出通过管道传输到我们本地系统的 **cpio**，以提取归档。在此示例中，仅使用 *if* 选项来指定输入文件。指定输出文件的 *of* 选项不需要。如果您要对磁盘设备执行 **dd** 操作将其写入磁带驱动器，则 *of* 将是您系统上的磁带驱动器，例如 */dev/rmt/0m*。

### dump 和 restore

**dump** 类似于 **backup**。如果在 HP-UX 上使用 **backup**，您会发现使用 **dump** 时有很多相似之处。**dump** 作为备份方案的一部分提供级别，并创建 **/var/adm/dumpdates**，该文件列出了文件系统最后备份的时间。**restore** 用于读取使用 **dump** 备份的信息。然而，**dump** 仅适用于 HFS 文件系统，不适用于 VxFS，并且假设您使用的是盒式磁带。**vxdump** 和 **vxrestore** 用于 VxFS。一般来说，您不会看到在 HP-UX 上推荐 **dump**（以及 **vxdump**）和 **restore**（以及 **vxrestore**）作为备份和恢复程序。**fbackup** 和 **cpio** 是 HP-UX 上首选的备份程序。然而，只要您牢记文件系统类型的限制，使用 **dump** 和 **restore** 是没有理由不行的。

让我们看看一些使用 **dump** 和 **restore** 的示例。我们的示例实际上将使用 **vxdump** 和 **vxrestore**；然而，HFS 和 VxFS 程序的使用方式几乎相同。我们将在接下来的示例中使用几条命令，包括以下内容：

```bash
# vxdump 0fu /dev/rmt/0m /var  ; dump vxfs file system /var to tape
# /dev/rmt/0m using level 0 and update /var/adm/dumpdates.

# vxrestore tf /dev/rmt/0m | grep eaaa  ; obtain table of contents from

# vxrestore -x -f /dev/rmt/0m ./tmp/eaaa01487  ; restore file to current directory
```

让我们更详细地查看其中一些命令，我将提供关于正在发生的事情的更多解释。

我们的第一个示例运行 **vxdump**，以备份级别 0（完全备份）备份目录 **/var**，使用 *f* 选项指定输出文件 **/dev/rmt/0m**，并使用 *u* 向 **/var/adm/dumpdates** 写入：

```bash
# vxdump 0fu /dev/rmt/0m /var

vxdump: Date of this level 0 dump: Tue Jul 11 16:41:27 2000
vxdump: Date of last level 0 dump: the epoch
vxdump: dumping /dev/vg00/rvol10 to /dev/rmt/0m
vxdump: mapping (Pass I) [regular files]
vxdump: mapping (Pass II) [directories]
vxdump: estimated 428058 blocks (209.01MB).
vxdump: dumping (Pass III) [directories]
vxdump: dumping (Pass IV) [regular files]
vxdump: 214146 tape blocks on 1 volumes(s)
vxdump: level 0 dump on Tue Jul 11 16:41:27 2000
vxdump: closing /dev/rmt/0m
vxdump: vxdump is done
#
```

**vxdump** 会将与备份相关的信息输出到标准输出。

接下来，让我们使用 **vxrestore** 查看磁带上的目录，查找以 *eaaa* 开头的文件。然后，我们将从系统中删除这些文件中的一个，并使用 **vxrestore** 从磁带中恢复它。要生成目录，我们使用 *t* 选项；要从磁带中提取文件，我们使用 **vxrestore** 的 *x* 选项，如下列清单所示：

```bash
# vxrestore tf /dev/rmt/0m | grep eaaa
404 ../tmp/eaaa01299
678 ../tmp/eaaa01333
700 ../tmp/eaaa01354
736 ../tmp/eaaa01380
741 ../tmp/eaaa01405
717 ../tmp/eaaa01487

#
#
# rm /var/tmp/eaaa01487
#
# vxrestore -x -f /dev/rmt/0m ./tmp/eaaa01487
# You have not read any tapes yet.
# Unless you know which volume your file(s) are on you should start
# with the next volume and work towards the first.
# Specify next volume #: 1
# set owner/mode for '..' [yn] y

# cd /var/tmp
# ls -1 eaaa01487
total 2
-rw-rw-rw- 1 root sys 28 Jul 11 15:45 eaaa01487
#
```

请注意，在恢复文件的过程中，我们必须指定卷号 1 以及是否要设置文件的模式。

本节的示例展示了使用 **vxdump** 创建备份磁带、生成目录以及使用 **vxrestore** 进行恢复。虽然 **fbackup** 和 **cpio** 是 HP-UX 上推荐的备份解决方案，但如果您熟悉这些程序并希望使用它们，可以使用 **dump** 和 **restore**。由于 **tar** 的可移植性，它也经常被用于备份和恢复。

## 第 8 章

### 系统启动和关闭脚本

## 虚拟分区中的系统启动和关闭脚本

每个虚拟分区都有独立的启动和关闭脚本，就像在独立系统上一样。由于虚拟分区，在启动和关闭方面没有独特的活动；但是，由于每个 vPar 都在运行自己的 HP-UX，您可以定制启动和关闭以满足您在每个 vPar 中运行的应用程序的需求。此外，还有一个 *heartbeat* 守护进程，用于每隔几秒同步一次虚拟分区数据库。

让我们看看在 vPar 中运行的应用程序以及支持该应用程序所使用的启动和关闭过程。此外，我们还将查看启动和停止 *heartbeat* 守护进程以同步虚拟分区数据库的方式。

### 虚拟分区中的应用启动

每个虚拟分区就像一台独立的服务器。在 vPar 中运行的应用程序独立于其他 vPar 中运行的应用程序和活动。

vPar 中的所有应用程序都需要运行启动脚本，就像在任何系统上一样（如果您需要了解 HP-UX 启动和关闭如何工作，请参阅本章中非 vPar 特定的部分）。

在本示例中使用的 vPar 中，我们运行了多种应用程序，包括 Broadvision。让我们查看 *etc/rc.config.d*，配置变量脚本位于此处，看看存在哪些 *bv* 文件（与 Broadvision 相关的文件）：

```bash
# ll | grep bv
-rwxr-xr-x    1 root        sys          9 Sep 26 09:31 bv
# cat bv
BV_CTL=1
#
```

此清单显示了 *bv* 文件及其内容。*BV_CTL=1* 变量表示当系统启动时应启动 Broadvision。

启动 *bv* 应用程序进程会导致启动多个与 Broadvision 相关的守护进程，包括以下清单中所示的那些：

```bash
# ps -ef | grep bv1
pbcosmb    3111    3096   0 Sep 26 ?        0:04 bvcont_srv_p_1221_3 -f -install_name bv1tol/bvcont_srv...
pbcosv    3404    3096   0 Sep 26 7        1:19 cntcdb_p_1221_5 -install_name bv1tol/cntcdb_1
pbcosbv   3707    3096   0 Sep 26 7        0:20 genericdb_p_1221_6 -install_name bv1tol/genericdb_1
pbcosbv   3479    3096   0 Sep 26 7:05 cntdb_p_1221_7 -install_name bv1tol DiscussionForus_cntdb_1
root        7572    7232   0 13:17:33 pts/0                0:00 grep bv1
#
```

您可以看到，此系统上正在运行许多与 *bv1* 应用程序相关的进程。这些进程作为 HP-UX 启动结构的一部分自动启动。以下清单显示了运行级别一（*/sbin/rc1.d*）和运行级别二（*/sbin/rc2.d*）中 *bv* 的链接。

```bash
# ll /sbin/rc1.d | grep bv
lrwxr-xr-x    1 root        sys          15 Sep 26 10:42 F10sbv -> /sbin/init.d/bv
# ll /sbin/rc2.d | grep bv
lrwxr-xr-x    1 root        sys          15 Sep 26 10:41 S930bv -> /sbin/init.d/bv
#
```




### 虚拟分区中的应用启动

如链接前的“K”所示，`bv_kill` 脚本显示在 `/sbin/rc1.d` 中；如链接前的“S”所示，`start` 脚本显示在 `/sbin/rc2.d` 中。

在链接中显示的脚本 `/sbin/init.d/bv` 会在虚拟分区的启动和关闭时运行各种命令。以下清单展示了 `/sbin/init.d/bv` 脚本：

```bash
#
#
# <在此处插入关于你的脚本的注释>
#
#
# 允许的退出值：
# 0 = 成功；会在检查表中显示“OK”。
# 1 = 失败；会在检查表中显示“FAIL”。
# 2 = 跳过；会在检查表中显示“N/A”。
# 如果此脚本的执行被控制变量的使用所覆盖，
# 或者由于其他原因不适合执行此脚本，则使用此值。
# 3 = 重启；会在执行后重启系统。
# 4 = 后台；会在检查表中显示“BG”；
# 如果此脚本以后台模式启动进程，则使用此值。
#
# 输入和输出：
# stdin 重定向自 /dev/null
#
# 在检查表模式下，stdout 和 stderr 重定向到 /etc/rc.log 文件，
# 在原始模式下则重定向到控制台。
PATH=/usr/sbin:/usr/bin:/sbin
export PATH

# 注意：如果你的脚本在运行状态 0 或状态 1 下执行，则 /usr 可能
# 不可用。除非你的脚本在运行状态 2 或更高状态下执行，否则不要尝试访问
# /usr 中的命令或文件。其他通常在运行状态 2 才挂载的文件系统包括 /var
# 和 /opt。

rval=0
# 检查此脚本运行的命令的退出值。如果非零，则
# 退出码会被回显到日志文件，且此脚本的返回值
# 被设置为指示失败。
set_return() {
   x=$?
   if [ $x -ne 0 ]; then
      echo "EXIT CODE: $x"
      rval=1 # 脚本失败
   fi
}

# 终止命名的进程。
# $1= 用于你的进程的搜索模式
killproc() {
   pid=`ps -ef | awk '{ if ( /"/"$1*"/" && ($4 != mypid) && ($5 != mypid))
      print $4 }' | tr -d ' '`
   if [ "$pid" ]; then
      kill "$pid"&
      echo "$1 stopped"
   else
      echo "Unable to stop $1"
   fi
}

case "$1" in
    'start_msg')
        # 发出与使用
        # "start" 参数运行此脚本相关的简短消息；
        # 此消息作为检查表的一部分显示。
        echo "Starting the BroadVision subsystem"
    ;;
    'stop_msg')
        # 发出与使用
        # "stop" 参数运行此脚本相关的简短消息；
        # 此消息作为检查表的一部分显示。
        echo "Stopping the BroadVision subsystem"
    ;;
    'start')
        # 读取系统配置变量
        if [ -f /etc/rc.config.d/bv ]; then
            . /etc/rc.config.d/bv
        else
            echo "ERROR: /etc/rc.config.d/bv defaults file MISSING"
        fi

        # 检查此脚本是否允许运行...
        if [ "$BV_CTL" != 1 ]; then
            rval=2
        else
            # 执行启动你的子系统的命令
            su - pbcombv -c "/opt/bvit01/bin/bvconf execute"
            set_return
        fi
    ;;
    'stop')
        # 读取系统配置变量
        if [ -f /etc/rc.config.d/bv ]; then
            . /etc/rc.config.d/bv
        else
            echo "ERROR: /etc/rc.config.d/bv defaults file MISSING"
        fi

        # 检查此脚本是否允许运行...
        if [ "$BV_CTL" != 1 ]; then
            rval=2
        else
            # 执行停止你的子系统的命令
            su - pbcombv -c "/opt/bvit01/bin/bvconf shutdown"
            set_return
        fi
    ;;
    *)
        echo "Usage: $0 { start|stop|start_msg|stop_msg}"
        rval=1
    ;;
esac

exit $rval
```

请注意，由于此脚本用于 *kill*（K）和 *start*（S），因此所有与 Broadvision 相关的 *start* 和 *stop* 信息都存在于此文件中。另请注意这一行：

```bash
if [ "$BV_CTL" != 1 ]; then
```

它检查我们之前在 `/etc/rc.config.d/bv` 中查看的变量是否等于我们检查文件时看到的一（1）。

在你想运行此应用的所有虚拟分区中，都需要安装并启动 Broadvision。在此示例中使用的 vPar 发生的情况，就是你在每个运行 Broadvision 的 vPar 中会看到的情况。

### 虚拟分区启动

让我们看一下 `/etc/rc.config.d`，配置变量脚本就位于此处，以查看存在哪些与 vPar 相关的脚本（如果你需要了解 HP-UX 的启动和关闭如何操作的信息，请参阅本章中非 vPar 特定的部分）。我们将对此目录执行长列表显示并搜索 *vpar*：

```bash
# ll /etc/rc.config.d | grep vpar
-r--r--r--   1 bin     bin     291 Aug 21 14:38 vparad
-r--r--r--   1 bin     bin     399 Aug 13 14:33 vparlib
-r--r--r--   1 bin     bin     702 Aug 13 14:30 vparinit
```

此列表显示了三个与 vPar 相关的配置变量脚本。我们将重点讨论 `vparhb`，即 *heartbeat* 守护进程。

*heartbeat* 守护进程用于每几秒钟同步一次在服务器上运行的 vPars 之间的虚拟分区数据库。你对虚拟分区所做的修改会更新虚拟分区数据库 `/stand/vpdb`。以下清单展示了虚拟分区中 `/stand` 的内容：

```bash
# ll /stand
total 143232
-rw-r--r--   1 root      sys         19 Jul 13 15:04 bootconf
drwxr-xr-x   4 root      sys       2048 Sep 17 15:47 build
drwxrwxrwx   5 root      root      1024 Sep 17 15:52 dtkm
drwxrwxrwx   5 root      sys        1024 Sep 17 14:10 /dtkm.vmmix.prev
-rw-r--r--   1 root      sys        3388 Sep 26 13:01 iconfig
-r--r--r--   1 root      sys           82 Jul 13 15:34 kernel
drwxr-xr-x   2 root      sys        1024 Sep 26 13:04 krs
drwxr-xr-x   2 root      root       1024 Sep 26 13:01 krs_lkg
drwxr-xr-x   2 root      root       1024 Sep 26 13:04 krs_tmp
drwxr-xr-x 2 root root 8192 Jul 13 15:04 lost+found
-rw------- 1 root root 12 Sep 26 13:01 rootconf
-r--r--r-- 1 root sys 2035 Sep 17 14:09 system
-r--r--r-- 1 root sys 994 Jul 13 15:28 system.01
-r--r--r-- 1 root sys 992 Jul 13 15:56 system.02
-r--r--r-- 1 root sys 994 Jul 13 15:28 system.base
drwxr-xr-x 2 root sys 1024 Jul 13 15:37 system.d
-rwxr-xr-x 1 root sys 2030 Sep 17 14:07 system.prev
-rwxr-xr-x 1 root sys 22682568 Sep 17 15:52 vmunix
-rwxr-xr-x 1 root sys 21316712 Sep 17 14:10 vmunix.prev
-rw------- 1 root root 8232 Sep 26 13:01 vpd6
-rw------- 1 root root 8232 Jul 17 14:11 vpd6.OLD
-rxr-xr-x 1 root bin 839161 Aug 31 18:59 vpmgr
dr-x------- 1 root root 507854 Jul 18 11:36 vpmgr.dmp
#
#
```

此列表中显示的文件中包括 **vpdb**。如果此 **vpdb** 被修改，或者此服务器上的另一个 **vpdb** 被修改，*heartbeat* 守护进程 **vpd6** 将确保服务器上所有运行中的 vPars 中的所有数据库都被同步。未运行的 vPars 在它们启动之前无法进行同步。

*heartbeat* 守护进程 **vpd6** 显示在以下 `ps -ef` 列表中：

```bash
$ ps -ef | grep vpd6
root 352 1 0 13:01:53 ? 0:00 vpd6 -d 10 -p /var/run/vpd6.pid
root 7289 7232 1 12:18:28 pts/0 0:01 grep vpd6
$
```

**vpd6** 作为 HP-UX 启动结构的一部分自动启动。以下清单显示了运行级别零（run level zero）中 /sbin/rc0.d 的所有链接，包括此列表开头的两个与 vPar 相关的链接：

```bash
# ll /sbin/rc0.d
total 0
lwxr-xr-x 1 bin bin 18 Sep 17 14:11 K425vpar6 -> /sbin/init.d/vpar6
lwxr-xr-x 1 bin bin 10 Sep 17 14:11 K431vpar6b -> /sbin/init.d/vpar6b
lwxr-xr-x 1 root root 19 Jul 13 15:08 K45emvcr -> /sbin/init.d/syncer
lwxr-xr-x 1 root root 15 Jul 13 15:08 K60vdl1 -> /sbin/init.d/vd1
lwxr-xr-x 1 root root 20 Jul 13 15:08 K60killall -> /sbin/init.d/killall
lwxr-xr-x 1 root root 19 Jul 13 15:08 K886knit -> /sbin/init.d/knit
lwxr-xr-x 1 root root 20 Jul 13 15:08 K99nrebuild -> /sbin/init.d/ntrebuild
lwxr-xr-x 1 root root 23 Jul 13 15:08 K99localmount -> /sbin/init.d/localmount
#
```

这些是 *kill* 脚本，如每个链接前的“K”所示。指向 *start* 脚本的链接可以在 /sbin/rc1.d 中找到。




我们将查看心跳链接中所示的文件 `/sbin/init.d/vparhb`，该文件在启动时运行，如下所示：

```bash
# cat /sbin/init.d/vparhb
#!/sbin/sh

# NOTE: This script is not configurable! Any changes made to this
# script will be overwritten when you upgrade to the next
# release of HP-UX.
#
# # vphb3 $Startup: Startup and kill script for the virtual partition
# heartbeat daemon
#
PATH=/sbin:/usr/sbin:/usr/bin
export PATH

if [ -r /etc/rc.config.d/vparhb ]
then . /etc/rc.config.d/vparhb
fi

case "$1" in
        'start_msg') echo "Starting Virtual Partition Heartbeat Daemon" ;
        'start|' vphb -d ${VPHBD_DELAY:-0} -p ${VPHBD_PID_FILE:=/var/run/vphb.pid}
                 exit $?
                ;;
        'stop_msg|' echo "Stopping Virtual Partition Heartbeat Daemon" ;
        'stop|' [ ! -r ${VPHBD_PID_FILE:=/var/run/vphb.pid} ] && exit 2
                 [ ! -s ${VPHBD_PID_FILE} ] && exit 1
                 kill -TERM `cat ${VPHBD_PID_FILE}`
                 rm -f ${VPHBD_PID_FILE}
                 exit 0
                ;;
        * echo "Usage: $0 { start | start_msg | stop | stop_msg }"
              ;;
esac
exit 0
```

请注意，与*心跳*守护进程相关的所有启动和停止信息都包含在此文件中，因为该脚本在*终止 (K)*和*启动 (S)*时都会运行。

当安装 vPar 软件时，vPar 特定的启动和关闭配置（例如我们刚刚介绍的*心跳*守护进程）会自动为您完成。您的应用程序相关启动配置必须在每个 vPar 上执行，就像在独立的服务器上一样。

本章的其余部分介绍了与 vPar 启动和关闭相关的背景信息。

## 非 vPar 特定章节部分 - 简介

本章涵盖了与启动和关闭脚本相关的各种主题，包括：

- HP-UX 中启动和关闭机制的整体组织
- 启动文件的示例
- /etc/inittab 文件
- *shutdown* 命令

### 系统启动和关闭脚本

HP-UX 11.x 的启动和关闭脚本基于一种机制，该机制将实际的启动和关闭脚本与配置信息分离开来。为了修改系统的启动或停止方式，你通常不需要修改脚本（这通常被认为有些风险）；相反，你可以修改配置变量。启动和关闭顺序基于一种行业标准，与许多其他基于 UNIX 的系统相似，因此你对 HP-UX 的知识适用于许多其他系统。

随着你的系统管理工作变得日益复杂，启动和关闭对你将变得越来越重要。当你加载和定制更多的应用程序时，你将需要更多的启动和关闭知识。在本节中，我将为你提供启动和关闭的概述以及你可以用来控制系统的命令。

启动和关闭模型中包含以下组件：

#### 执行脚本

执行脚本从配置变量文件中读取变量，并执行启动或关闭序列。这些脚本位于 /sbin/init.d 中。

#### 配置变量脚本

这些是你需要修改的文件，用于设置在系统启动或关闭时启用或禁用子系统或执行其他功能的变量。这些文件位于 **/etc/rc.config.d** 中。

#### 链接文件

这些文件用于控制脚本的执行顺序。它们实际上是指向执行脚本的链接，当从一个运行级别转换到另一个运行级别时执行这些链接。这些文件位于相应运行级别的目录中，例如运行级别 0 的 **/sbin/rc0.d**，运行级别 1 的 **/sbin/rc1.d**，等等。

#### 排序器脚本

此脚本根据运行级别转换调用执行脚本。此脚本位于 **/sbin/rc** 中。

图 8-1 显示了启动和关闭脚本的目录结构。

![](img/eff8b9287a5f38c5adf538f24aacf29e_457_0.png)

### 图 8-1 启动和关闭文件的组织

执行脚本执行启动和关闭任务。/sbin/rc 使用适当的 start 或 stop 参数调用执行脚本，你可以控制台上查看相应的 start 或 stop 消息。你看到的信息将具有以下三个值之一：

- OK 表示执行脚本正确启动或关闭。
- FAIL 在启动或关闭过程中发生了问题。
- N/A 脚本未配置为启动。

为了启动一个子系统，你只需编辑 /etc/rc.config.d 中相应的配置文件。

### 系统启动和关闭脚本

让我们看一个示例启动和关闭文件，该文件用于一个加载到 HP-UX 系统上的应用程序，该应用程序广泛用于 Internet 应用程序，名为 Cold Fusion。与加载在 HP-UX 系统上的许多应用程序一样，Cold Fusion 将启动和关闭脚本作为产品安装过程的标准部分进行安装。

如前所述，用作启动和关闭过程一部分的脚本位于 /etc/init.d 中。在我们的情况下，该程序的名称是 /etc/init.d/coldfusion，如下所示：

```bash
# cat /sbin/init.d/coldfusion
#!/bin/sh
#
# Start the Cold Fusion servers
#
export CFHOME

#
# Start/stop processes for Cold Fusion
#

rval=0
case "$1" in

        start_msg)
                print "Starting ColdFusion Application Server"
                ;;
        stop_msg)
                print "Stopping ColdFusion Application Server"
                ;;
        start)
                #Start_check "on/off switch", to set CF_AUTOSTART, in config.d file.
                RCFILE=/etc/rc.config.d/coldfusion
                if [ -f $RCFILE ]; then
                        . $RCFILE
                else
                        print "Warning: $RCFILE defaults file missing."
                        print "Starting ColdFusion by default."
                        CF_AUTOSTART=1
                fi
        # Start CP if switch is on.
                if [ "$CF_AUTOSTART" -eq 1 ]; then
                        if [ ! -x $CPBIN/start ]; then
                                rval=$?
                        else
                                print "Error: ColdFusion startup script $CPBIN/start missing."
                                print "      ColdFusion not started."
                                rval=1
                        fi
                else
                        print "Notice: ColdFusion startup disabled in $RCFILE"
                        rval=2
                fi
                ;;
        stop)
                if [ -x $CPBIN/stop ]; then
                        $CPBIN/stop -force
                fi
                ;;

        *)
                echo "Usage: $0 [ start | stop ]"
                rval=1
                ;;
esac
exit $rval
```

`/etc/init.d` 中的启动和关闭脚本通常同时执行启动和关闭功能。启动和关闭脚本（包括我们示例中的那个）识别以下四个参数：

- *start_msg* - 这是传递给脚本的参数，以便脚本可以报告一条消息，指示 "start" 操作将执行什么。
- *stop_msg* - 这是传递给脚本的参数，以便脚本可以报告一条消息，指示 "stop" 操作将执行什么。
- *start* - 脚本将启动应用程序。
- *stop* - 脚本将关闭应用程序。

所有启动和关闭脚本（包括前面列表中的那个）都从 `/etc/rc.config.d` 中的变量获取配置数据。我们的示例脚本检查 `/etc/rc.config.d/coldfusion` 中 "开/关" 开关的值，以判断是否应该启动 Cold Fusion，如下所示：

```bash
# cat /etc/rc.config.d/coldfusion
# ColdFusion Application Server configuration file
#
CF_AUTOSTART=1  #Set to 1 to restart at boot time
```

该文件中的变量被设置为 1，因此应用程序将在系统启动时启动。





### 系统启动和关闭脚本

启动和关闭脚本根据脚本链接所在的目录来运行。我们示例中的脚本应在运行级别三时启动。因此，其脚本链接出现在目录 `/sbin/rc3.d` 中，如下所示列表中的第三个链接：

```
# ls -l /sbin/rc3.d
total
lrwxr-xr-x    1 root     sys        23 Apr 26 14:32 G100nfs.server -> /sbin/init.d/nfs.server
lrwxr-xr-x    1 root     sys        19 Apr 26 14:52 S200tpc.rc -> /sbin/init.d/tps.rc
lrwxrwxrwx    1 root     sys        20 May 16 20:57 S790coldfusion -> ../init.d/coldfusion
lrwxr-xr-x    1 root     sys        23 Apr 26 14:44 S890dologin.rc -> /sbin/init.d/dologin.rc
```

我们稍后会解释链接命名的意义。目前，只需知道名为 `/sbin/rc3.d/S790coldfusion` 的链接指向我们的脚本 `/init.d/coldfusion` 即可。

应用程序的关闭顺序与启动顺序相反。这意味着启动和关闭脚本的链接将出现在用于关闭的较低级别目录中。在我们的示例中，启动链接出现在 `/sbin/rc3.d`，但关闭链接出现在 `/etc/rc1.d`，如下所示列表：

```
# ls -l /sbin/rc1.d
lrwxr-xr-x    1 root     sys         17 Apr 26 14:52 K220slod -> /sbin/init.d/slod
lrwxr-xr-x    1 root     sys         18 Apr 26 14:45 K230audio -> /sbin/init.d/audio
lrwxr-xr-x    1 root     sys         21 Apr 26 14:46 K240auditlog -> /sbin/init.d/auditlog
lrwxr-xr-x    1 root     sys         17 Apr 26 14:43 K250envd -> /sbin/init.d/envd
lrwxr-xr-x    1 root     sys         17 Apr 26 14:43 K270cron -> /sbin/init.d/cron
lrwxr-xr-x    1 root     sys         15 Apr 26 14:45 K270pd -> /sbin/init.d/pd
lrwxr-xr-x    1 root     sys         15 Apr 26 14:45 K280lp -> /sbin/init.d/lp
lrwxr-xr-x    1 root     sys         21 Apr 26 14:49 K290ipamgr -> /sbin/init.d/ipamgr
lrwxr-xr-x    1 root     sys         20 Apr 26 14:41 K290pararray -> /sbin/init.d/pararray
lrwxrwxrwx    1 root     sys         20 May 16 20:57 K300coldfusion -> ../init.d/coldfusion
```

名为 `/sbin/rc1.d/K300coldfusion` 的链接指向我们的脚本 `/init.d/coldfusion`。此应用程序的启动发生在运行级别 3，而关闭发生在运行级别 1。

前述两个列表中显示的链接名称具有特定含义。让我们看一下我们示例中的启动链接：

![](img/eff8b9287a5f38c5adf538f24aacf29e_461_0.png)

此示例适用于我们的 Cold Fusion 启动脚本。启动链接以 "S" 开头，代表 startup（启动）。关闭脚本在 `/sbin/rc1.d` 中有类似的条目，但链接名的第一个字符是 "K"，表示 kill（终止）。脚本按字典顺序执行。在给定的运行级别中，启动脚本之间以及关闭脚本之间留有间隔，因此当添加新脚本时，无需重新编号该运行级别内现有的脚本。

由于应用程序的关闭顺序与启动顺序相反，关闭脚本通常不会与其启动对应项使用相同的编号。两个因依赖关系而按特定顺序启动的应用程序，通常会以相反的顺序关闭。在我们的示例中，启动编号是 S790coldfusion，关闭编号是 K300coldfusion。

当运行级别发生变化时，脚本会执行。`/sbin/rc` 是一个在运行级别变化时运行的程序。以下列表显示了 `/etc/inittab`，它调用在我们示例系统中使用的 `/sbin/rc`：

```
id:1::sysinit:/sbin/initrc ></dev/console 2>&1
tape:1:sysinit:/sbin/stinit ></dev/console 2>&1
moxi:2:sysinit:/sbin/baseupg 1>/dev/console 2>&1 # mux init
stty:1:sysinit:/sbin/stty 9600 clocal -icanon echo opost oxtab ixon icrnl ignpar </dev/eystty
brcl:bootwait:/sbin/boheckrc </dev/console >/dev/console 2>&1 # kick, etc.
link:wait:/sbin/sh -c "/sbin/um -f /dev/syscons; `
/sbin/init /dev/sys/tty /dev/syscons> /dev/console 2>kl
ccprt: bootwait:/sbin/cat /etc/copyright ./dev/syscons # legal req
sysrc: wait:/sbin/rc </dev/console >/dev/console 2>1 # system init
#post: powerwait:/sbin/powerfail /dev/console 2>1 # powerfail
conn: 123456:respawn:/usr/sbin/getty console console # system console
#tp1:234:respawn:/usr/sbin/getty -h ttyOp1 9600
#tp2:234:respawn:/usr/sbin/getty -h ttyOp2 9600
#tp3:234:respawn:/usr/sbin/getty -h ttyOp3 9600
#tp4:234:respawn:/usr/sbin/getty -h ttyOp4 9600
#tp5:234:respawn:/usr/sbin/getty -h ttyOp5 9600
#ups: respawn:/tmp/l 8 /usr/lib/upd_wond -f /etc/ups_conf
```

**/sbin/rc** 行始终存在于 **/etc/inittab** 文件中。关于 **/etc/inittab** 的更多信息稍后会出现。

如果你正在将系统引导到运行级别 3，那么 **/sbin/rc** 将运行存在于 **/sbin/rc1.d**、**/sbin/rc2.d** 和 **/sbin/rc3.d** 中的启动脚本。

我在本次讨论中多次提到了运行级别。这里描述的启动和关闭脚本，以及 **/etc/inittab** 文件，都依赖于运行级别。在 HP-UX 11.x 中，存在以下运行级别：

| 运行级别 | 描述 |
| :--- | :--- |
| 0 | 已停止的运行级别。 |
| s | 运行级别 s，也称为单用户模式，用于确保没有其他用户登录系统，以便你可以执行系统管理任务。 |
| 1 | 运行级别 1 启动各种基本进程。 |
| 2 | 运行级别 2 允许用户访问系统。这也称为多用户模式。 |
| 3 | 运行级别 3 用于导出 NFS 文件系统。 |
| 4 | 运行级别 4 启动图形管理器，包括 HP 通用桌面环境（HP CDE）。 |
| 5 和 6 | 目前未使用。 |

**/etc/inittab** 还用于定义将运行的各种进程，并且由 **/sbin/init** 使用。**/sbin/init** 的进程 ID 为 1。它是系统上启动的第一个进程，并且没有父进程。**init** 进程查看 **/etc/inittab** 以确定系统的运行级别。

**/etc/inittab** 文件中的条目具有如下格式：

```
id:run state:action:process
```

-   **id**
    条目的名称。id 长度最多为四个字符，并且必须在文件中唯一。如果 **/etc/inittab** 中的行以“#”开头，则该条目被视为注释。
-   **run state**
    指定执行命令的运行级别。可以指定多个运行级别。命令将为指定的每个运行级别执行。
-   **action**
    定义对该进程将采取的 11 种操作之一。action 的 11 种选择为：*initdefault*、*sysinit*、*boot*、*bootwait*、*wait*、*respawn*、*once*、*powerfail*、*powerwait*、*ondemand* 和 *off*。
-   **process**
    如果运行级别和/或操作字段指示如此，则将要执行的 shell 命令。

这里是一个 **/etc/inittab** 条目的示例：

```
cons:123456:respawn:/usr/bin/getty    console console

    |  |              |                |-> process
    |  |          |-> action
    |  |-> run state
    |-> id
```

这之所以位于 **/etc/inittab** 文件中，而不是定义为启动脚本，是因为控制台可能会被终止，并且每当它停止运行时都需要重启，即使运行级别没有变化。**respawn** 在进程不存在时启动该进程，并在其停止后重启该进程。此条目显示了所有运行状态，因为你希望控制台始终处于激活状态。

另一个示例是 /etc/inittab 中的第一行：

```
init:3:initdefault:
```

系统的默认运行级别定义为 3。

理解此处描述的系统启动和关闭的基本知识非常重要。你将启动和关闭系统，甚至可能修改此处描述的一些文件。在开始修改之前，请仔细检查启动和关闭文件。

现在让我们看一下你可以发出以关闭系统的命令。

### 系统关闭

关闭系统意味着什么？好吧，以最简单的形式来说，关闭系统仅仅意味着发出 /sbin/shutdown 命令。**shutdown** 命令用于终止所有处理。它有许多选项，包括：

-   `-r` 自动重启系统；即关机后再开机。
-   `-h` 完全停止系统。
-   `-y` 完成关闭操作，而不向你提出通常会询问的问题。
-   `grace` 指定在关闭系统前希望等待的秒数，以便给用户时间保存文件、退出应用程序并注销。

当你发出 **shutdown** 命令时，你的系统会执行以下一些操作：

-   检查执行 **shutdown** 的用户是否确实具有执行该命令的权限。





- 将工作目录更改为根目录（/）。
- 将 PATH 设置为 /usr/bin:/usr/sbin:/sbin。
- 更新所有超级块。
- 通知用户已发出关机指令，并要求他们注销。
- 执行 /sbin/rc，执行诸如通过关机脚本（例如 spooler 和 CDE）关闭子系统、卸载文件系统以及其他此类任务。
- 如果使用 -r 选项，则执行 /sbin/reboot。

若要关机并自动重新启动系统，请输入：

```
shutdown -r
```

若要停止系统，请输入：

```
shutdown -h
```

系统将询问您是否希望输入一条消息给用户，告知他们即将进行的系统关机。在您输入消息后，它会立即发送给所有用户。在指定时间过去之后（默认值为 60 秒），系统将开始关机过程。一旦您收到系统已停止的消息，您就可以关闭所有系统组件的电源。

若要在两分钟内关机且不询问任何问题或发送任何消息，请输入：

```
shutdown -h -y 120
```

有时，您需要使用 shutdown 进入单用户模式以执行某些任务（例如备份或扩展逻辑卷），然后重新启动系统以恢复其原始状态。

若要使系统进入单用户模式关机，请输入：

```
shutdown
```

不带任何选项的 **shutdown** 命令会将您带入单用户模式。在操作系统的旧版本中，您可以使用带 *s* 选项的 **init** 命令（**init s**）进入单用户模式。但是，这种做法强烈不推荐，因为该命令不会终止其他系统活动，也不会注销用户；因此，它不会导致真正的单用户状态。

如果系统已经处于单用户模式，或者您喜欢冒险，您可以执行 /usr/sbin/reboot。我强烈建议您执行 **shutdown**，它将调用 **reboot**。**reboot** 命令会突然终止所有进程，然后停止或重新启动系统。此外，在使用动态加载的内核模块时，**reboot** 不会加载这些模块；只有 **shutdown** 会加载。

再次强调，我推荐使用 **shutdown** 命令，而不是 **reboot**。

## 第 9 章

## 文件系统

## 虚拟分区文件系统

每个虚拟分区都有自己的完整 HP-UX 文件系统，就像在单独的服务器上拥有不同的文件系统一样。这些文件系统完全独立运行。如果您希望共享两个 vPar 之间的文件系统信息，您将使用与在服务器之间共享文件系统信息相同的方法，例如网络文件系统（NFS）。不同 vPar 文件系统之间的这种完全独立性确保了 vPar 的完全软件隔离。

在下一节中，我们将涵盖一些与 vPar 文件系统相关的主题，然后是在本章节非 vPar 特定部分中的文件系统背景知识。

### 独立的 vPar 文件系统

vPar 的文件系统在不同的两个 vPar 上会有所不同，就像在两个不同的服务器上会有所不同一样。这意味着在一台服务器上运行的两个 vPar 所占用的磁盘空间可能正好是同一台服务器上运行一个标准 HP-UX 所占用的磁盘空间的两倍。这两个 vPar 中的每一个都需要自己的操作系统、应用程序、用户主目录等。由于除了通常在网络环境中共享的 NFS 文件系统之外，没有任何文件系统被共享，这可能会使您的存储需求翻倍。让我们看一下在两个不同的 vPar 上运行的文件系统。

以下是在服务器上运行的第一个 vPar（主机名 **actappd1**）上运行的 **bdf** 命令结果：

```
# hostname
actappd1
# bdf
Filesystem             kbytes   used    avail  %used Mounted on
/dev/vg00/lvol3        245760 40769 192184   18% / 
/dev/vg00/lvol1        111637 74350 26123    74% /stand
/dev/vg00/lvol8        1732608 598033 1063751 36% /var
/dev/vg00/lvol7        1732608 755560 915987 45% /usr
/dev/vg00/lvol1        1228800 466678 714321 40% /usr1
/dev/vg00/lvol14       258048 69857 174676   28% /tmp
/dev/vg00/lvol16       1531904 1381306 141226 91% /opt
/dev/vg00/lvol5        819200 176605 603031 23% /home
```

此列表显示了 **vg00**，即系统上配置的唯一一个卷组，以及每个逻辑卷中的容量设置。

**接下来**是在服务器上运行的第二个 vPar（主机名 **ecvpar2**）上运行的 **bdf** 命令结果：

```
# hostname
actappd1
# bdf
Filesystem             kbytes    used     avail  %used Mounted on
/dev/vg00/lvol3        143360   43174   93951  31% / 
/dev/vg00/lvol1        111637   73632   26861  73% /stand
/dev/vg00/lvol8        1536000  965183  535326  64% /var
/dev/vg00/lvol7        1593444  740649  799344  48% /usr
/dev/vg00/lvol14       258048   68619   177641  28% /tmp
/dev/vg00/lvol16       2084864  563709  1426107 28% /opt
/dev/vg00/lvol5        819200   1314    766771 0% /home
```

您可以从这两个列表中看出，这两个 **vg00** 卷组所占用的空间大约是不运行 vPar 时所占用的空间的两倍。通过运行两个 vPar，您在这台服务器上很可能完成两倍的工作量，因此这很可能是值得花费的磁盘空间；但是，您需要将其消耗的空间作为规划的一部分来考虑。

我们前面列出的第一个 vPar 也在其上运行了几个应用程序。其中一个是 **BroadVision**，它需要自己在 **/opt/bs** 下的目录，如下面的列表所示：

```
# hostname
actapp01
# ll /opt
total 32
dr-xr-xr-x 7 bin bin 96 Jul 13 15:27 Migration
dr-xr-xr-x 9 bin bin 1024 Jul 13 15:26 OV
drwxrwxr-x 18 bin bin 1024 Jul 13 15:23 apche
dr-xr-xr-x 6 bin bin 96 Jul 13 15:12 asx
dr-xr-xr-x 6 bin bin 96 Jul 13 15:24 audio
drwxr-xr-x 22 root bin 1024 Sep 21 13:34 bvto1
drwxr-xr-x 8 root users 1024 Jul 13 15:26 cifsclient
dr-xr-xr-x 4 bin bin 96 Jul 13 15:26 cmcluster
dr-xr-xr-x 4 bin bin 96 Jul 13 15:25 cmom
dr-xr-xr-x 10 bin bin 1024 Jul 13 15:10 dce
dr-xr-xr-x 4 bin bin 1024 Jul 13 15:35 dcelocal
dr-xr-xr-x 4 bin bin 96 Jul 13 15:13 dmi
dr-xr-xr-x 4 bin bin 96 Jul 13 15:11 fcmo
dr-xr-xr-x 4 bin bin 96 Jul 13 15:17 graphics
dr-xr-xr-x 3 bin bin 96 Jul 13 15:08 gprarray
dr-xr-xr-x 3 bin bin 96 Jul 13 15:14 ior
dr-xr-xr-x 16 bin bin 1024 Jul 19 15:03 ignite
dr-xr-xr-x 3 bin bin 96 Jul 13 15:14 image
dr-xr-xr-x 4 bin bin 96 Jul 13 15:25 java1.2
drwxrwxrwx 7 bin bin 1024 Aug 24 16:34 java1.3
drwxr-xr-x 2 root root 96 Jul 13 15:04 lost+found
dr-xr-xr-x 7 root sys 96 Aug 27 17:26 make
dr-xr-xr-x 8 root sys 1024 Jul 13 15:27 motd
dr-xr-xr-x 9 bin bin 1024 Jul 13 15:26 netscape
dr-xr-xr-x 7 bin bin 96 Jul 13 15:09 nettladm
dr-xr-xr-x 2 bin bin 96 Jul 13 15:11 networkdocs
dr-xr-xr-x 2 bin bin 96 Jul 13 15:16 pamrg
dr-xr-xr-x 7 bin bin 96 Jul 13 15:15 pd
dr-xr-xr-x 12 root bin 1024 Jul 13 15:25 perf
dr-xr-xr-x 9 bin bin 1024 Jul 13 15:26 prn
dr-xr-xr-x 4 bin bin 96 Jul 13 15:11 rai0d48i
dr-xr-xr-x 6 bin bin 96 Jul 13 15:12 reason
drwxr-xr-x 10 root users 1024 Jul 13 15:25 samba
dr-xr-xr-x 3 root users 96 Jul 13 15:24 samba_sro
dr-xr-xr-x 8 bin bin 1024 Jul 13 15:16 scr
dr-xr-xr-x 3 root bin 96 Aug 24 13:42 tiomli
drwxrwxr-x 11 bin bin 1024 Jul 13 15:24 tocsat
dr-xr-xr-x 5 bin bin 96 Jul 13 15:25 tocmate
dr-xr-xr-x 4 bin bin 96 Jul 13 15:25 videod
dr-xr-xr-x 6 bin bin 96 Jul 13 15:26 webadmin
dr-xr-xr-x 10 bin bin 1024 Jul 13 15:27 wlm
#
```

**/bv1to1** 目录是加载 Broadvision 应用程序的目录。此目录将出现在需要运行 Broadvision 的每个 vPar 上。下面的列表显示了使用 du 命令时 /opt 下每个目录所占用的容量：

```
# hostname
actappdi
# cd /opt
# hostname
actappdi
# pwd
/opt
# du -s *
13842 Migration
80456 OV
57604 apache
250 asx
1912 audio
1402052 bv1to1 <-- Broadvision 目录
5072 cifsclient
2304 cmcluster
4720 cmon
22214 dce
2 dcelocal
446 dmi
296 fcms
620 graphics
44848 gparay
28709 isor
146206 ignite
2064 image
136598 java1.2
136910 java1.3
0 lost+found
2386 make
53634 mx
54444 netscape
2292 netiladm
512 networkdocs
1076 parmgr
35770 pd
216234 perf
112774 pvm
2182 raid4ei
850 resmon
26874 samba
10514 samba_src
8648 scr
87810 tivo1i
8628 tomcat
1998 upgrad
1272 video
28684 webadmin
5908 wlm
#
```




### 独立的 vPar 文件系统

该应用程序将加载到其应运行的每个 vPar 中，并占用与其相关的磁盘空间。这对所有应用程序都是如此。

在此 vPar 上执行 `swlist` 命令会显示已加载到该 vPar 上的所有应用程序，包括 vPars 软件和相关应用程序：

```
# swlist
# Initializing...
# Contacting target "actapppd1"...
# Target: actapppd:/
#
#
# Bundle(s):

B9788AA					1.3.0.01					Java 2 SDK 1.3 for HP-UX (700/800),
FA1-*					PA-1 + DX2.0 Add On

BUNDLIB11					B.11.11.0102.2			Required Patch Bundle for HP-UX 11i
CDS-English				B.11.11
FDDI-00					B.11.11.01				PCI FDDI;Support MWA3739A/A3739B;SW=3626A
FibChani-00					B.11.11.01.16			Support HSC/FibreChannel;
GOLDAPPS11				"B.11.11.0106.9 Gold Application Patches
GLDDABASE11				B.11.11.0106.9 Gold Base Patches for HP-UX 11i, June 2001
GIgChec-00				B.11.11.14				PCI/HSC Gigabit;Support
HW-AS55A					HW-AS42xA/AS439A/AS424A/AS45xA/SW=31642A
HPUXLII-OS-MC				B.11.11.0106				HP-UX Mission Critical
HPUXBase64				B.11.11				HP-UX 64-bit Base OS
HPUXBaseAux				B.11.11.0106				OP-UX Base OS Auxiliary
HW-enable11				B.11.11.0106				Hardware Enablement Patches for
									HP-UX 11i, June 2001
ITX-Recovery				B.3.3.116				Ignite-UX network recovery tool subset
QS235BA					B.04.13				Metascape Directory Server v4 for HP-UX
Onlinedlag				B.11.11.04				HPUX 11.11 Support Tools Bundle, Jun 2001
RAID-00					B.11.11.01				PCI RAID; Support HW-AS55A
#
# Product(s) not contained in a Bundle:
#

BVISION1				6.0				BroadVision One-To-One Enterprise
BVSNC-0AA				6.0.0				BroadVision One-To-One Enterprise 6.0_Patch AA
BVSNCeServerC2BMK7				6.0.0				BroadVision 1.1 Business-To-Business Contract Utility Installation
BVSNTreadingConnector				6.0.0				BroadVision 1.1 Adapter TradingConnector Application Installation
BVSNZbZ				6.0.0				BroadVision 1.1 Commerce Business-To-Business Installation
BVSNZb2AA				6.0.0-AA				BroadVision 1.1 Commerce Business Commerce Patch AA Installation
BVSNcwaa				6.0.0				BroadVision 1.1 Core Commerce Installation
BVSNcwaaa				6.0.0-AA				BroadVision 1.1 Core Commerce Base Commerce Patch AA Installation
BVSNcabv				6.0.0-AB				BroadVision 1.1 Core Commerce Patch AB Installation
BVSNVERITY261				2.6.1.0				Verity V2.6.1 Developer Kit
PHKL_23578				1.0				Software Distributor Cumulative Patch
PHKL_24625				1.0				Virtual Partitions manages cumul patch
PHKL_24546				1.0				vPar enablement patch
PHKL_24547				1.0				vPar enablement patch
PHKL_24548				1.0				vPar enablement patch
PHKL_24549				1.0				vPar enablement patch
PHKL_24550				1.0				Early boot, panic, Paeta & vPar enablement
PHKL_24551				1.0				thread cscop, vPar, Paeta, load averages
PHKL_24552				1.0				vPar enablement patch
PHKL_24553 1.0 console, chassis code, crash/dump, vPar PHKL_24554 1.0 vPar enablement patch PHKL_24555 1.0 PREFSETH LOCK 1/0, PR 8702 2.2, vPar PHKL_24556 1.0 vPar enablement patch PHKL_24557 1.0 vVar enablement patch PHKL_24559 1.0 vVar enablement patch PHKL_24559 1.0 SysLog overflow, high temp alerts, vPar PHKL_24560 1.0 vPar enablement patch PHKL_24561 1.0 Psetc & vVar Enablement PHKL_24562 1.0 vvar enablement patch PHKL_24563 1.0 vPar enablement patch PHKL_24564 1.0 vPar enablement patch PHKL_24565 1.0 vvar enablement patch PHKL_24566 1.0 Kernel Memory allocation, Faets Enablement PHKL_24570 1.0 Boot Bank, Faets & vPar enablement PHKL_24582 1.0 iSCSI Supports, Faets Enablement Patch PHKL_24585 1.0 Paets & vPar enablement patch PHKL_24985 1.0 vPar enablement patch PHKL_25080 1.0 vPar enablement patch FMBS_22535 1.0 Cumulative STRAAMS Patch FMNS_22713 1.0 iDGI) and linker tools cumulative patch Tivem 4.1.2 Tivol) Storage Manager make 3.60 00 06 HP-UX Virtual Partitions Functionality b 3.79.1 make
```

您在系统中看到的 VirtualPartition 软件版本将晚于示例中显示的版本。

维护额外的 HP-UX 文件系统（在运行 vVars 时很可能会发生这种情况）要求您考虑所需的额外磁盘空间，以及确保系统平稳运行的技术，例如恢复和操作系统及应用程序更新。请务必备份您的系统清单，并经常执行备份和创建可引导恢复磁带。

## 章节“简介”中的非 vPar 特定部分

在本章的这一节中，我们将重点关注以下内容：

- Veritas Volume Manager 概述
- 逻辑卷管理器 (LVM) - 您可能正在使用 LVM 来管理系统上的数据。我在本部分提供了 LVM 的背景知识。
- 使用 LVM 向系统添加 XP 256 磁盘的示例。
- 使用 LVM 重新配置磁盘的示例 - 我包含了一个在真实系统上执行的复杂磁盘重新配置示例，以展示使用了多少个 LVM 命令。虽然您的系统可能不需要这种磁盘重新配置，但它是使用 LVM 命令的一个很好的示例。
- 一些额外的文件系统命令。

### Veritas Volume Manager

Veritas Volume Manager 是 HP-UX 11i 的新特性，它随操作系统一起捆绑提供。

与逻辑卷管理器不同，使用 Veritas Volume Manager 执行的大多数工作都是通过基于 Java 的图形界面完成的。本部分的示例都使用图形界面来向您介绍 Veritas Volume Manager。

### 逻辑卷管理器背景

逻辑卷管理器是一个磁盘管理子系统，它允许您以逻辑卷的形式管理物理磁盘。这意味着一个文件系统可以跨越多个物理磁盘。您可以将逻辑卷管理器视为一种灵活的方式，用于定义彼此独立的磁盘空间边界。您不仅可以指定逻辑卷的大小，还可以根据需要更改其大小。与将磁盘专门用于文件系统或拥有固定大小分区的磁盘相比，这一可能性是一个巨大的进步。逻辑卷可以容纳文件系统、原始数据或交换空间。现在您可以指定逻辑卷为任意大小，拥有跨越多个物理磁盘的逻辑卷，并在需要时更改逻辑卷的大小！

那么，为了设置逻辑卷管理器并实现所有这些好处，您需要知道什么？首先，您需要了解术语；其次，您需要了解逻辑卷管理器命令。与许多其他系统管理任务一样，您可以使用 SAM 为您设置逻辑卷管理器。事实上，我建议您使用 SAM 在您的系统上设置逻辑卷管理器。但是，照例，我建议您在使用 SAM 在系统上设置逻辑卷管理器之前，阅读此概述并至少了解逻辑卷管理器的基础知识。SAM 章节（第 11 章）有一个使用 SAM 创建逻辑卷的示例。阅读完本节后，您可能想快速查看一下该示例。

用于日志文件系统 (JFS)，惠普有一款名为 HP OnLineJFS 的附加产品。这个方便的产品允许您在不进入单用户模式的情况下执行许多 LVM 功能。例如，当需要扩展文件系统时，其所驻留的逻辑卷在扩展前需要被卸载。通常，这种卸载意味着将系统关闭到单用户模式，以便没有用户或进程可以访问该卷，然后才能将其卸载。使用 OnLineJFS，逻辑卷和文件系统可以在系统正常运行且无用户或进程中断的情况下简单扩展。

#### 逻辑卷管理器术语

以下术语用于与逻辑卷管理器一起工作。这些仅仅是与逻辑卷管理器相关的一些术语，但足以让您开始使用逻辑卷管理器。如果您使用 SAM，即使不知道所有这些术语，也可以操作逻辑卷管理器。然而，如果您计划使用逻辑卷管理器，阅读以下关于这些术语的简要概述是一个好主意，这样您就可以大致了解 SAM 为您做了什么。




## 卷
卷是用于文件系统、交换分区或原始数据的设备。如果没有逻辑卷管理器，卷要么是磁盘分区，要么是整个磁盘驱动器。

## 物理卷
未初始化为供逻辑卷管理器使用的磁盘。如果要使用逻辑卷管理器，必须初始化整个磁盘；也就是说，不能只初始化磁盘的一部分供逻辑卷管理器使用，而将另一部分用于固定分区。

## 卷组
卷组是由逻辑卷管理器管理的一组逻辑卷。通常，您需要定义系统中哪些磁盘将由逻辑卷管理器使用，然后定义如何将这些磁盘分组为卷组。每个单独的磁盘可以是一个卷组，或者多个磁盘可以组成一个卷组。此时，您已创建了一个称为卷组的磁盘空间池。一个磁盘只能属于一个卷组。一个卷组可以跨越多个物理磁盘。

## 逻辑卷
这是在卷组内定义的空间。卷组被划分为逻辑卷。这类似于固定大小的磁盘分区，但您具有灵活性来更改其大小。逻辑卷包含在卷组中，但卷组可以跨越多个物理磁盘。您可以拥有一个比单个磁盘更大的逻辑卷。

## 物理扩展区
物理卷上的一组连续磁盘块。如果您将磁盘定义为物理卷，其物理扩展区将由该磁盘的块大小决定。如果您将磁盘定义为物理卷，则该磁盘内的连续块构成一个物理扩展区。逻辑卷管理器使用物理扩展区作为将磁盘空间分配给逻辑卷的单位。如果您使用较小的物理扩展区大小（例如 1 MB），则定义逻辑卷时具有较细的粒度。如果您使用较大的物理扩展区大小（例如 256 MB），则定义逻辑卷时具有较粗的粒度。默认大小为 4 MB。

## 逻辑扩展区
逻辑卷是一组逻辑扩展区。在卷组中，逻辑扩展区和物理扩展区的大小相同。尽管逻辑扩展区和物理扩展区的大小相同，但这并不意味着两个逻辑扩展区会映射到两个连续的物理扩展区。可能会出现两个逻辑扩展区映射到不同磁盘上的物理扩展区的情况！

图 9-1 以图形方式展示了我们刚刚介绍的一些逻辑卷术语。在该图中，您可以清楚地看到逻辑扩展区并未映射到连续的物理扩展区，因为某些物理扩展区未被使用。

### 逻辑卷管理器背景

![](img/eff8b9287a5f38c5adf538f24aacf29e_478_0.png)

图 9.1 逻辑卷管理器部分逻辑到物理映射

## 磁盘镜像
逻辑卷可以镜像一次或多次，创建逻辑卷的相同副本。这意味着如果进行镜像，一个逻辑扩展区可以映射到多个物理扩展区。

您可能拥有一个希望镜像部分或所有逻辑卷的环境。可以使用 SAM 为您设置磁盘镜像。但是，您必须首先确定镜像的特性。有一个称为“严格”的镜像策略。在使用以下选项创建逻辑卷时，您定义以下三种严格策略之一：

- **n** 不，这不是严格分配策略，意味着逻辑扩展区的镜像副本可以共享同一个物理卷。这意味着您的原始数据和镜像数据确实可能位于同一个物理磁盘上。如果遇到某种磁盘机械故障，您可能会同时丢失原始数据和镜像数据。

- **y** 是，这是严格分配策略，意味着逻辑扩展区的镜像副本不能共享同一个物理卷。允许数据的镜像副本共享同一个物理卷相比，这样更安全。如果在此场景中磁盘出现问题，您可以保证原始数据位于与镜像数据不同的物理磁盘上。即使您希望它们位于不同的物理卷上，原始数据和镜像数据始终是同一个卷组的一部分。

- **g** 镜像数据不会与原始数据位于同一个物理卷组（PVG）中。此策略称为 PVG-严格分配策略。

严格分配策略取决于您的环境。大多数使用镜像的安装购买了足够的磁盘驱动器来镜像所有数据。在这样的环境中，我会创建两个卷组，一个用于原始数据，一个用于镜像数据，并在创建逻辑卷时使用 "strict -g" 选项，以便原始数据在一个卷组中，而镜像数据在另一个卷组中。

#### 逻辑卷管理器命令

以下是更常见的逻辑卷管理器命令的定义。许多这些命令都在 SAM 为您设置逻辑卷时创建的日志文件中找到。我在这里提供这些命令的描述，以便当您看到它们时，能了解每个命令的用途。虽然这些并非所有逻辑卷管理器命令，但它们是我最常使用的命令，也是您在使用逻辑卷管理器时应了解的那些命令。这些命令分为物理卷（pv）命令、卷组（vg）命令和逻辑卷（lv）命令。这些命令可以在手册页中找到。一些命令，例如 **vgdisplay**、**pvdisplay** 和 **lvdisplay**，已被发出，以便您可以看到这些命令的示例。查看逻辑卷管理器命令的输出时，**bdf** 的以下输出将对您有帮助。**bdf** 的输出显示了几个已挂载的逻辑卷（**lvol1**、**lvol3**、**lvol4**、**lvol5**、**lvol6**、**lvol7**、**lvol8**），它们都属于卷组 **vg00**（参见本章后面的 **bdf** 命令概述）。

$ **bdf**

| 文件系统 | Kbytes | 已用 | 可用 | 使用率 | 挂载于 |
|---|---|---|---|---|---|
| /dev/vg00/lvol3 | 47829 | 18428 | 24618 | 43% | / |
| /dev/vg00/lvol1 | 67733 | 24736 | 36223 | 41% | /stand |
| /dev/vg00/lvol8 | 34541 | 8673 | 22413 | 28% | /var |
| /dev/vg00/lvol7 | 299157 | 149449 | 119792 | 56% | /usr |
| /dev/vg00/lvol4 | 23013 | 48 | 20663 | 0% | /tmp |
| /dev/vg00/lvol6 | 99669 | 32514 | 57188 | 36% | /opt |
| /dev/vg00/lvol5 | 19861 | 9 | 17865 | 0% | /home |
| /dev/dsk/c0t6d0 | 802212 | 552120 | 169870 | 76% | /mnt/9.x |

##### 物理卷命令

**pvchange**

此命令用于以某种方式更改物理卷。例如，如果当前不允许，您希望允许将额外的物理扩展区添加到物理卷中；或者如果确实允许，您希望禁止将额外的物理扩展区添加到物理卷中。

**pvcreate**

此命令用于创建将成为卷组一部分的物理卷。请记住，一个卷组可能由多个物理卷组成。物理卷是您系统上的磁盘。

**pvdisplay**

此命令显示有关您指定的物理卷的信息。如果使用详细（-v）选项，您可以使用此命令获取大量有关逻辑到物理映射的信息。使用 -v **pvdisplay** 将显示指定物理卷的逻辑扩展区到物理扩展区的映射。

您还可以从该命令获取许多其他有用的数据，例如：物理卷的名称；物理卷所属的卷组的名称；物理卷的状态；物理卷上物理扩展区的大小；物理扩展区的总数；以及空闲物理扩展区的数量。
以下是运行 `pvdisplay` 的部分示例：

```
$ pvdisplay -v /dev/dsk/c0t6d0
```

```text
--- Physical volumes ---
PV Name      /dev/dsk/c0t1d0
VG Name      /dev/vg00
PV Status    available
Allocatable  yes
VGDA         2
Cur LV       7
PE Size (Mbytes)   4
Total PE     157
Free PE      8
Allocated PE 149
Stale PE     0

--- Distribution of physical volume ---
LV Name              LE of LV   PE for LV
/dev/vg00/lvol1       12        12
/dev/vg00/lvol2       17        17
/dev/vg00/lvol6       75        75
/dev/vg00/lvol7        9         9
/dev/vg00/lvol4       25        25
/dev/vg00/lvol5        6         6
/dev/vg00/lvol3        5         5

--- Physical extents ---
PE Status  LV                 LE
0000 current /dev/vg00/lvol1  0000
0001 current /dev/vg00/lvol1  0001
0002 current /dev/vg00/lvol1  0002
0003 current /dev/vg00/lvol1  0003
0004 current /dev/vg00/lvol1  0004
0005 current /dev/vg00/lvol1  0005
0006 current /dev/vg00/lvol1  0006
0007 current /dev/vg00/lvol1  0007
0008 current /dev/vg00/lvol1  0008
0009 current /dev/vg00/lvol1  0009
0010 current /dev/vg00/lvol1  0010
0011 current /dev/vg00/lvol1  0011
0012 current /dev/vg00/lvol2  0000
0013 current /dev/vg00/lvol2  0001
0014 current /dev/vg00/lvol2  0002
0015 current /dev/vg00/lvol2  0003
0016 current /dev/vg00/lvol2  0004
```




## PV 移动

0017 current /dev/vg00/lvol2 0005
0018 current /dev/vg00/lvol2 0006
0019 current /dev/vg00/lvol2 0007
0020 current /dev/vg00/lvol2 0008
0021 current /dev/vg00/lvol2 0009
0022 current /dev/vg00/lvol2 0010
0023 current /dev/vg00/lvol2 0011
0024 current /dev/vg00/lvol3 0000
0025 current /dev/vg00/lvol3 0001
0026 current /dev/vg00/lvol3 0002
0027 current /dev/vg00/lvol3 0003
0028 current /dev/vg00/lvol3 0004
0029 current /dev/vg00/lvol4 0000
0030 current /dev/vg00/lvol4 0001
0031 current /dev/vg00/lvol4 0002
0032 current /dev/vg00/lvol4 0003
0033 current /dev/vg00/lvol4 0004
0034 current /dev/vg00/lvol4 0005
0035 current /dev/vg00/lvol4 0006

...

0156 free 0000

从该列表中可以看出，*lvol1* 大约为 48 MBytes，其分配的物理扩展区数量远多于大约 20 MBytes 的 *lvol3*。

### pvmove

您可以使用此命令将物理扩展区从一个物理卷移动到其他的物理卷。通过指定源物理卷和一个或多个目标物理卷，您可以使用此命令将数据分散到您希望的各种物理卷中。

##### 卷组命令

- **vgcfgbackup**
此命令用于保存卷组的配置信息。请记住，卷组由一个或多个物理卷组成。在您做出 LVM 更改后，SAM 会自动运行此命令。

- **vgcfgrestore**
此命令用于恢复卷组的配置信息。

- **vgchange**
此命令使卷组处于活动或非活动状态。使用 *-a* 选项，您可以使卷组失活 (*-an*) 或激活 (*-ay*)。

- **vgcreate**
您可以使用此命令创建卷组并指定其所有参数。创建卷组时，您需要指定卷组名称以及该卷组的所有相关参数。

- **vgdisplay**
如果您使用详细 (-v) 选项，这将显示与卷组相关的所有信息，包括：卷组名称；卷组状态；卷组中的最大、当前和打开的逻辑卷数量；卷组中的最大、当前和活动的物理卷数量；以及物理扩展区相关信息。

以下是使用 **vgdisplay** 查看卷组 *vg00* 的示例：

```
$ vgdisplay /dev/vg00
```

--- 卷组 ---
VG Name            /dev/vg00
VG Write Access    read/write
VG Status          available
Max LV             255
Cur LV             7
Open LV            7
Max PV             16
Cur PV             1
Act PV             1
Max PE per PV      2000
VGDA               2
PE Size (Mbytes)   4
Total PE           157
Alloc PE           149
Free PE            8
Total PVG          0

- **vgexport**
此命令将逻辑卷组从系统中移除，但不会修改物理卷上的逻辑卷信息。然后可以使用 **vgimport** 将这些物理卷导入另一个系统。

- **vgextend**
可以通过此命令指定要添加到卷组的物理卷，从而将物理卷添加到卷组中。

- **vgimport**
此命令可用于将物理卷导入另一个系统。

- **vgreduce**
可以通过此命令缩小卷组的大小，方法是指定要从卷组中移除哪个物理卷。在进行此操作之前，请确保要移除的物理卷上没有数据。

- **vgremove**
可以使用此命令将卷组定义完全从系统中移除。

- **vgscan**
在发生某种灾难的情况下，您可以使用此命令扫描系统，以尝试重建 /etc/lvmtab 文件。

- **vgsync**
有时，卷组中的镜像数据会变得“陈旧”或过时。**vgsync** 用于同步卷组中每个镜像逻辑卷的物理扩展区。

##### 逻辑卷命令

- **lvcreate**
此命令用于创建新的逻辑卷。逻辑卷在卷组内创建。逻辑卷可以跨越多个磁盘，但必须存在于卷组内。当您在 SAM 中创建逻辑卷时，SAM 会为您执行此命令。此命令有许多选项，其中两个常用的选项是 -L 用于定义逻辑卷的大小，-n 用于定义逻辑卷的名称。

- **lvchange**
此命令用于以某种方式更改逻辑卷。例如，您可能希望使用 -p 选项将逻辑卷的权限更改为读写 (w) 或只读 (r)。或者，您可能希望将严格策略（在磁盘镜像下描述）更改为严格 (y)、非严格 (n) 或 PVG 严格 (g)。

- **lvdisplay**
此命令显示您指定的每个逻辑卷的状态和特征。如果使用该命令的详细 (-v) 选项，您将获得许多类别的大量有用数据，包括：

    - 1) 关于逻辑卷设置方式的信息，例如逻辑扩展区所在的物理卷；物理卷上的本地扩展区数量；以及物理卷上的物理扩展区数量。
    - 2) 逻辑扩展区的详细信息，包括逻辑扩展区编号以及关于逻辑扩展区所在的物理卷和物理扩展区的一些信息。

以下是针对之前 **bdf** 示例中显示的第一个逻辑卷 (*vol1*) 使用 **lvdisplay** 的示例：

```
$ lvdisplay -v /dev/vg00/lvol1

--- 逻辑卷 ---
LV Name /dev/vg00/lvol1
VG Name /dev/vg00
LV Permission read/write
LV Status available/syncd
Mirror copies 0
Consistency Recovery MWC
Schedule parallel
LV Size (Mbytes) 48
Current LE 12
Allocated PE 12
Stripes 0
Stripe Size (Kbytes) 0
Bad block off
Allocation strict/contiguous

--- 逻辑卷的分布 ---
PV Name LE on PV PE on PV
/dev/dsk/c0t1d0 12 12

--- 逻辑扩展区 ---
LE PV1 PE1 Status 1
0000 /dev/dsk/c0t1d0 0000 current
```

### 逻辑卷管理器背景

```
0001 /dev/dsk/c0t1d0  0001 current
0002 /dev/dsk/c0t1d0  0002 current
0003 /dev/dsk/c0t1d0  0003 current
0004 /dev/dsk/c0t1d0  0004 current
0005 /dev/dsk/c0t1d0  0005 current
0006 /dev/dsk/c0t1d0  0006 current
0007 /dev/dsk/c0t1d0  0007 current
0008 /dev/dsk/c0t1d0  0008 current
0009 /dev/dsk/c0t1d0  0009 current
0010 /dev/dsk/c0t1d0  0010 current
0011 /dev/dsk/c0t1d0  0011 current
```

尽管此示例中显示的大部分内容不言自明，但有些条目需要解释。逻辑卷的大小为 48 MBytes，由 12 个逻辑扩展区 (LEs) 和 12 个物理扩展区 (PE) 组成。这意味着每个物理扩展区的大小为 4 MBytes (4 MBytes x 12 个扩展区 = 48 MBytes)。我们可以通过运行显示物理卷特征的命令来验证这一点。在该列表的底部，您可以看到逻辑扩展区映射到物理扩展区的情况。在这种情况下，逻辑扩展区 0000 - 0011 与物理扩展区 0000 - 0011 之间存在直接映射。

- **lvextend**

此命令用于增加分配给逻辑卷的物理扩展区数量。我们有时会低估逻辑卷所需的大小，使用此命令可以轻松解决此问题。您可能希望扩展逻辑卷以增加镜像副本数量（使用 -m 选项）、增加逻辑卷的大小（使用 -L 选项）或增加逻辑扩展区数量（使用 -l 选项）。

- **extendfs**

在 **lvextend** 之后使用此命令。虽然 **lvextend** 命令扩展逻辑卷，但 **extendfs** 扩展逻辑卷内的文件系统。如果您忘记发出 **extendfs** 命令，SAM 中的逻辑卷看起来已扩展，但发出 **bdf** 命令不会显示扩展情况。

### lvlnboot

使用此命令将逻辑卷设置为主、引导、主要交换或转储卷（这可以使用 **lvrmbboot** 撤消）。发出带有 -v 选项的 **lvlnboot** 命令可显示当前设置。

### lvsplt 和 lvmerge

这些命令分别用于拆分和合并镜像逻辑卷。如果您有一个镜像逻辑卷，**lvsplt** 将把它拆分为两个逻辑卷。**lvmerge** 合并两个大小相同的逻辑卷，增加镜像副本数量。

### lvmmigrate

此命令为磁盘分区中的根文件系统准备迁移到逻辑卷。如果您有一个需要转换为逻辑卷的分区，就会使用此命令。

### lvreduce

使用此命令减少分配给逻辑卷的物理扩展区数量。在创建逻辑卷时，我们有时会高估逻辑卷的大小。此命令可用于设置镜像副本数量（使用 -m 选项）、减少逻辑扩展区数量（使用 -l 选项）或减少逻辑卷的大小（使用 -L 选项）。在减小逻辑卷大小时请小心。您可能会将其设置得比其中的数据还要小。如果选择这样做，请确保您有良好的数据备份。




清空逻辑卷后，您可以使用此命令从卷组中删除逻辑卷。

如果您不希望某个逻辑卷作为根设备、引导设备、主交换设备或转储设备（这与 **lvlnboot** 命令相反），则使用此命令。但是，除非您有用于引导的磁盘分区，否则请确保使用 **lvlnboot** 命令指定了根设备或引导设备，否则系统将不知道该从哪里引导。

有时，逻辑卷中的镜像数据会变得“陈旧”或过时。**lvsync** 用于同步逻辑卷中的物理区域。

## 添加磁盘

在本节中，我们将对 XP 256 磁盘进行一些操作。我们希望创建十个卷组，每个卷组包含五个主磁盘和五个备用磁盘。

让我们查看包含用于 XP 256 主路径和备用路径的物理磁盘的文件。XP 256 是一种高级存储设备，具备在主控制器故障时故障转移到备用控制器的能力。同一组磁盘连接到主控制器和备用控制器，但这些磁盘被赋予了两个不同的设备文件集。一组是磁盘连接到主控制器时使用的，另一组是同一组磁盘连接到备用控制器时使用的。如果您曾使用过 ServiceGuard，可能会遇到过相同的概念。有一组磁盘通过两条不同的路径连接，因此您必须根据磁盘是通过主路径还是备用路径连接，用不同的名称来定义这些磁盘。以下是文件 *pri* 的内容，其中以每五个为一组列出了主磁盘：

c9t0d0 c9t0d1 c9t0d2 c8t0d0 c8t0d1
c7t0d0 c7t0d1 c7t0d2 c10t0d0 c10t0d1
c9t0d3 c9t0d4 c9t0d5 c8t0d3 c8t0d4
c7t0d3 c7t0d4 c7t0d5 c10t0d3 c10t0d4
c9t0d6 c9t0d7 c9t1d0 c8t0d6 c8t0d7
c7t0d6 c7t0d7 c7t1d0 c10t0d6 c10t0d7
c9t1d1 c9t1d2 c9t1d3 c8t1d1 c8t1d2
c7t1d1 c7t1d2 c7t1d3 c10t1d1 c10t1d2
c9t1d4 c9t1d5 c9t1d6 c8t1d4 c8t1d5
c7t1d4 c7t1d5 c7t1d6 c10t1d4 c10t1d5

请注意，在此列表中，磁盘被分为每五个一组。每五个磁盘将构成一个卷组。总共有 10 组五个磁盘，它们将放入卷组 *vgu01* 到 *vgu10* 中。

还将有一个备用磁盘组，每组五个磁盘。备用磁盘将用于在之前描述的磁盘控制器故障转移情况下使用。以下是文件 *alt* 的内容，其中以每五个为一组列出了备用磁盘：

c8t8d0 c8t8d1 c8t8d2 c9t8d0 c9t8d1
c10t8d0 c10t8d1 c10t8d2 c7t8d0 c7t8d1
c8t8d3 c8t8d4 c8t8d5 c9t8d3 c9t8d4
c10t8d3 c10t8d4 c10t8d5 c7t8d3 c7t8d4
c8t8d6 c8t8d7 c8t9d0 c9t8d6 c9t8d7
c10t8d6 c10t8d7 c10t9d0 c7t8d6 c7t8d7
c8t9d1 c8t9d2 c8t9d3 c9t9d1 c9t9d2
c10t9d1 c10t9d2 c10t9d3 c7t9d1 c7t9d2
c8t9d4 c8t9d5 c8t9d6 c9t9d4 c9t9d5
c10t9d4 c10t9d5 c10t9d6 c7t9d4 c7t9d5

此列表中总共显示了 10 组备用磁盘，它们也将是卷组 *vgu01* 到 *vgu10* 的一部分。使用在 XP 256 上设置好的这些主磁盘和备用磁盘，我们将在主机系统上设置相应的卷。在此示例中，主机系统是 V-Class 系统。

现在，让我们介绍创建其中一个卷组的步骤。首先，我们将使用 pvcreate 命令为卷组中的每个磁盘创建一个物理卷。接下来，我们将使用 mkdir 创建卷组的目录。然后，我们使用 mknod 在该目录内为卷组创建设备特殊文件。这将设置创建 10 个卷组中的第一个所需的目录和特殊文件。然后，我们将使用 vgcreate 创建包含五个主磁盘的卷组。在创建卷组时，我们指定第一个磁盘，然后使用 vgextend 将其他磁盘加入卷组。接着，我们使用 vgextend 扩展卷组以包含五个备用磁盘。最后一步是为整个卷组创建一个单一逻辑卷。您可能希望在一个卷组内创建多个逻辑卷，但在我们的示例中，我们只需要一个消耗卷组全部容量的逻辑卷，即 8755 个物理区域。以下流程列出了创建第一个卷组的手动步骤：

```
# pvcreate /dev/rdsk/c9t0d0 # run for each of the 5 pri disks

# mkdir /dev/vgu01 # make dir for first vol group

# mknod /dev/vgu01/group -c 64 0x01000 # create special file with major
# and minor numbers shown

# vgcreate /dev/vgu01 /dev/dsk/c9t0d0 # place first disk in volume group

# vgextend /dev/vgu01 /dev/dsk/c9t0d1 # extend volume with remaining four
# primary disks

# vgextend /dev/vgu01 /dev/dsk/c8t0d0 # extend volume group to include five
# alternate disks

# lvcreate -l 8755 /dev/vgu01 # creates lv01 (lv011 by default)
# that consumes all 8755 extents
```

我们只完成了一个磁盘的流程，而该卷组中还有九个其他磁盘。此外，还有另外九个卷组需要完成此流程。总共还有 99 个磁盘需要运行各种命令。涉及如此大量的键入操作，错误空间很大，因此这是一个非常适合自动化的过程。

由于有主磁盘集和备用磁盘集，我们将编写一个简短的程序来自动化每个流程。以下程序执行创建每个磁盘的物理卷、创建卷组以及将主磁盘包含在内的所有必需步骤：

```
#!/bin/ksh
set -x            ;set tracing on
vgnum=$1          ;first item on each line is the volume group no.
shift             ;shift to get to first disk

for i in $*       ;run pvcreate for every disk name in first line
do
    pvcreate /dev/rdsk/$i
done

reada             ;pause program to view what has been run

mkdir /dev/vgs$vgnum         ;mkdir for volume group
mknod /dev/vgs$vgnum/c0g5$vgnum 0000 ;mknod for volume group
vgcreate /dev/vgs$vgnum /dev/dsk/$1 ;vgcreate 1st disk in vg

shift             ;shift over to second disk
for i in $*       ;extend volume group to include remaining four disks
do
    vgextend /dev/vgs$vgnum /dev/dsk/$i
done

lvcreate -l 8755 /dev/vgs$vgnum ;create single log vol for entire vg
```

我在该文件中使用 **set -x** 来开启执行跟踪。当我最初调试 shell 程序时，我总是这样做，以便可以看到 shell 程序中的行在何时被执行。正在执行的行前面会有一个 "+"，随后是正常运行程序时通常看到的内容。**The read a** 是一种暂停程序以等待输入的方式，以便我可以回顾到程序该点为止已运行的内容。

为了让此程序运行，我们必须对包含主磁盘设备的文件进行轻微修改，并在每行开头添加卷组编号。此外，我决定从包含主磁盘的文件中调用该程序，并每次只处理一行磁盘。以下列表显示了更新后的文件，其中包含前一个列表中 shell 程序（**vg.sh**）的名称，然后是卷组编号，再然后是卷组中五个主磁盘名称的列表：

```
#vg.sh 01 c9t0d0 c9t0d1 c9t0d2 c8t0d0 c8t0d1
#read a
#vg.sh 02 c7t0d0 c7t0d1 c7t0d2 c10t0d0 c10t0d1
#read a
#vg.sh 03 c9t0d3 c9t0d4 c9t0d5 c8t0d3 c8t0d4
#read a
#vg.sh 04 c7t0d3 c7t0d4 c7t0d5 c10t0d3 c10t0d4
#read a
#vg.sh 05 c9t0d6 c9t0d7 c9t1d0 c8t0d6 c8t0d7
#read a
#vg.sh 06 c7t0d6 c7t0d7 c7t1d0 c10t0d6 c10t0d7
#read a
#vg.sh 07 c9t1d1 c9t1d2 c9t1d3 c8t1d1 c8t1d2
#read a
#vg.sh 08 c7t1d1 c7t1d2 c7t1d3 c10t1d1 c10t1d2
#read a
#vg.sh 09 c9t1d4 c9t1d5 c9t1d6 c8t1d4 c8t1d5
#read a
#vg.sh 10 c7t1d4 c7t1d5 c7t1d6 c10t1d4 c10t1d5
```

该文件中各行之间的 **The read a** 将暂停并等待您输入 **Return** 键，然后下一行才会执行。这样做是因为我可能会决定运行几行，并希望在各行执行之间检查结果。

现在，我们可以取消该文件第一行的注释，并输入文件名 **pri**，这将调用 **vg.sh** 并运行该程序（您必须为文件赋予适当的权限，并确保 **vg.sh** 和 **pri** 均可执行。）





喜欢逐行运行此类文件，并随着卷组的创建检查它们。该脚本编写为逐行执行，但很容易修改为运行所有十行。

我们需要使用备用磁盘名称时做的工作要少得多。物理卷已经创建，卷组和单个逻辑卷已在 `vg.sh` 中设置完毕。我们将创建另一个名为 `vga.sh` 的脚本，“a” 代表“备用”，我们将在其中扩展卷组，以包含每个磁盘的备用名称。该脚本如下所示：

```bash
#!/bin/ksh
set -x    ;set tracing on
vgnum=$1  ;first item on each line is the volume group number
shift     ;shift to get to first disk

for i in $*      ;extend vol group to include all five disks on line
    vgextend /dev/vgs/vg$num /dev/dsk/$i
done
```

此脚本仅执行将卷组 `vgnum` 扩展以包含该行上出现的所有五个磁盘的任务。类似于文件 `pri`，文件 `alt` 将调用脚本 `vga.sh`，如下列列表所示：

```
#vga.sh 01 c8t8d0 c8t8d1 c8t8d2 c9t8d0 c9t8d1
#vga.sh 02 c10t8d0 c10t8d1 c10t8d2 c7t8d0 c7t8d1
#vga.sh 03 c8t8d3 c10t8d4 c8t8d5 c8t8d3 c8t8d4
#vga.sh 04 c10t8d3 c10t8d4 c10t8d5 c7t8d3 c7t8d4
#vga.sh 05 c8t8d6 c8t8d7 c9t8d0 c9t8d6 c9t8d7
#vga.sh 06 c10t8d6 c10t8d7 c10t8d0 c7t8d6 c7t8d7
#vga.sh 07 c8t8d1 c8t8d2 c8t8d3 c7t8d1 c7t8d2
#vga.sh 08 c10t8d1 c10t8d2 c10t8d3 c7t8d1 c7t8d2
#vga.sh 09 c8t8d4 c8t8d5 c8t8d6 c9t8d4 c9t8d5
#vga.sh 10 c10t8d4 c10t8d5 c10t8d6 c7t8d4 c7t8d5
```

你需要取消注释你想要运行脚本的那一行。同样，你可以运行所有十行，但我喜欢检查每行运行后发生的事情。如果你想运行几行并在它们之间暂停以检查结果，可以在此文件的行之间添加 `read a`。

这两个脚本自动化了大量输入工作。有 100 个磁盘需要运行命令，以及其他逻辑卷管理器命令。这是最适合 shell 编程的 HP-UX 系统管理任务类型。

### 自动化流程结束

我完成了为额外磁盘运行必要的步骤，例如为额外四个磁盘执行的 **vgcreate** 和为额外九个磁盘设备执行的 **vgextend**。我在示例中只包含了第一个磁盘，以便你可以看到必须运行的初始步骤。

我们不需要在主要或备用卷中设置任何 RAID 级别，因为这是由 XP 256 内部完成的。

以下 **vgdisplay** 列表显示了我们为卷组 `vgu01` 设置的磁盘，包括五个主要和备用磁盘组：

```
# vgdisplay /dev/vgu01 -v
```

| | |
|---|---|
| VG 名称 | /dev/vgu01 |
| VG 写访问 | 读/写 |
| VG 状态 | available |
| 最大 LV | 255 |
| 当前 LV | 1 |
| 打开的 LV | 1 |
| 最大 PV | 16 |
| 当前 PV | 5 |
| 活动 PV | 5 |
| 每个 PV 的最大 PE | 1751 |
| VGDA | 10 |
| PE 大小 (MB) | 4 |
| 总 PE | 8755 |
| 已分配 PE | 8755 |
| 空闲 PE | 0 |
| 总 PVG | 0 |
| 总备用 PV | 0 |
| 正在使用的备用 PV | 0 |

| | |
|---|---|
| LV 名称 | /dev/vgu01/lvol1 |
| LV 状态 | available/syncd |
| LV 大小 (MB) | 35020 |
| 当前 LE | 8755 |
| 已分配 PE | 8755 |

```
已使用 PV 5

--- 物理卷 ---
PV 名称 /dev/dsk/c9t0d0
PV 名称 /dev/dsk/c8t8d0 备用链接
PV 状态 available
总 PE 1751
空闲 PE 0

PV 名称 /dev/dsk/c9t0d1
PV 名称 /dev/dsk/c8t8d1 备用链接
PV 状态 available
总 PE 1751
空闲 PE 0

PV 名称 /dev/dsk/c9t0d2
PV 名称 /dev/dsk/c8t8d2 备用链接
PV 状态 available
总 PE 1751
空闲 PE 0

PV 名称 /dev/dsk/c8t0d0
PV 名称 /dev/dsk/c9t0d0 备用链接
PV 状态 available
总 PE 1751
空闲 PE 0

PV 名称 /dev/dsk/c8t0d1
PV 名称 /dev/dsk/c9t0d1 备用链接
PV 状态 available
总 PE 1751
空闲 PE 0
```

在这个 **vgdisplay** 中有一些感兴趣的点需要涵盖。第一点是，由于我们之前定义过，到同一磁盘的主路径和备用路径都存在。例如，卷组中的第一个磁盘的主路径名为 *c9t0d0*，备用路径名为 *c8t8d0*。其次，卷组 *vgu01* 和其中唯一的逻辑卷 *lvol1* 总共由 8755 个 PE（物理扩展）组成（在我们的情况下，卷组的大小是 PE x PE 大小，即 8755 x 4MB）。

我们还应该检查 *vgu01* 上的一个逻辑卷，名为 *lvol1*。我们可以使用 **lvdisplay** 命令检查此逻辑卷的参数，如以下示例所示：

```
# lvdisplay -v /dev/vgu01/l*
--- 逻辑卷 ---
```

# 添加磁盘

| LV 名称 | /dev/vgu01/lvol1 |
| :------- | :---------------- |
| VG 名称 | /dev/vgu01 |
| LV 权限 | 读/写 |
| LV 状态 | available/syncd |
| 镜像副本 | 0 |
| 一致性恢复 | MWC |
| 调度 | 并行 |
| LV 大小 (MB) | 35020 |
| 当前 LE | 8755 |
| 已分配 PE | 8755 |
| 条带 | 1 |
| 条带大小 (KB) | 0 |
| 坏块 | 开 |
| 分配 | 严格 |
| IO 超时 (秒) | 默认 |

### --- 逻辑卷分布 ---

| PV 名称 | PV 上的 LE | PV 上的 PE |
| :------ | :------- | :------- |
| /dev/dsk/c9t0d0 | 1751 | 1751 |
| /dev/dsk/c9t0d0 | 1751 | 1751 |
| /dev/dsk/c9t0d2 | 1751 | 1751 |
| /dev/dsk/c8t0d0 | 1751 | 1751 |
| /dev/dsk/c8t0d0 | 1751 | 1751 |

### --- 逻辑扩展 ---

| LE | PV1 | PRI | 状态 1 |
| :--- | :--- | :--- | :------- |
| 00000 | /dev/dsk/c9t0d0 | 00000 | current |
| 00001 | /dev/dsk/c9t0d0 | 00001 | current |
| 00002 | /dev/dsk/c9t0d0 | 00002 | current |
| 00003 | /dev/dsk/c9t0d0 | 00003 | current |
| 00004 | /dev/dsk/c9t0d0 | 00004 | current |
| 00005 | /dev/dsk/c9t0d0 | 00005 | current |
| 00006 | /dev/dsk/c9t0d0 | 00006 | current |
| 00007 | /dev/dsk/c9t0d0 | 00007 | current |
| 00008 | /dev/dsk/c9t0d0 | 00008 | current |
| 00009 | /dev/dsk/c9t0d0 | 00009 | current |
| 00010 | /dev/dsk/c9t0d0 | 00010 | current |
| 00011 | /dev/dsk/c9t0d0 | 00011 | current |
| 00012 | /dev/dsk/c9t0d0 | 00012 | current |
| 00013 | /dev/dsk/c9t0d0 | 00013 | current |
| 00014 | /dev/dsk/c9t0d0 | 00014 | current |
| 00015 | /dev/dsk/c9t0d0 | 00015 | current |
| 00016 | /dev/dsk/c9t0d0 | 00016 | current |
| 00017 | /dev/dsk/c9t0d0 | 00017 | current |
| 00018 | /dev/dsk/c9t0d0 | 00018 | current |
| 00019 | /dev/dsk/c9t0d0 | 00019 | current |
| 00020 | /dev/dsk/c9t0d0 | 00020 | current |
| 00021 | /dev/dsk/c9t0d0 | 00021 | current |
| 00022 | /dev/dsk/c9t0d0 | 00022 | current |
| 00023 | /dev/dsk/c9t0d0 | 00023 | current |
| 00024 | /dev/dsk/c9t0d0 | 00024 | current |
| 00025 | /dev/dsk/c9t0d0 | 00025 | current |
| 00026 | /dev/dsk/c9t0d0 | 00026 | current |
| 00027 | /dev/dsk/c9t0d0 | 00027 | current |
| 00028 | /dev/dsk/c9t0d0 | 00028 | current |
| 00029 | /dev/dsk/c9t0d0 | 00029 | current |
| 00030 | /dev/dsk/c9t0d0 | 00030 | current |
| 00031 | /dev/dsk/c9t0d0 | 00031 | current |

```
00032 /dev/dsk/c9t0d0   00032 current
·
·
·
08733 /dev/dsk/c8t0d1   01729 current
08734 /dev/dsk/c8t0d1   01730 current
08735 /dev/dsk/c8t0d1   01731 current
08736 /dev/dsk/c8t0d1   01732 current
08737 /dev/dsk/c8t0d1   01733 current
08738 /dev/dsk/c8t0d1   01734 current
08739 /dev/dsk/c8t0d1   01735 current
08740 /dev/dsk/c8t0d1   01736 current
08741 /dev/dsk/c8t0d1   01737 current
08742 /dev/dsk/c8t0d1   01738 current
08743 /dev/dsk/c8t0d1   01739 current
08744 /dev/dsk/c8t0d1   01740 current
08745 /dev/dsk/c8t0d1   01741 current
08746 /dev/dsk/c8t0d1   01742 current
08747 /dev/dsk/c8t0d1   01743 current
08748 /dev/dsk/c8t0d1   01744 current
08749 /dev/dsk/c8t0d1   01745 current
08750 /dev/dsk/c8t0d1   01746 current
08751 /dev/dsk/c8t0d1   01747 current
08752 /dev/dsk/c8t0d1   01748 current
08753 /dev/dsk/c8t0d1   01749 current
08754 /dev/dsk/c8t0d1   01750 current
```

此列表在显示三个点的地方进行了缩写。只显示了第一个磁盘的开头和最后一个磁盘的结尾。**lvdisplay** 确实显示了组成该逻辑卷的五个主要磁盘。

最后一步是在我们在 `vgu01` 中设置的逻辑卷上放置文件系统。*SAM* 非常适合这项任务。图 9-2 显示了我们所创建的逻辑卷的 *SAM* 屏幕截图。为十个卷组中的每一个创建了一个逻辑卷。





![](img/eff8b9287a5f38c5adf538f24aacf29e_500_0.png)

图 9-2 vgv01 至 vgv10 上的 lvol1

卷组 vgv01 至 vgv10 中均存在 lvol1。我们希望在每个逻辑卷上创建文件系统，以运行当前应用程序。尽管我们可以在命令行中执行相应的命令，但我们将使用 SAM 来完成此任务。

![](img/eff8b9287a5f38c5adf538f24aacf29e_501_0.png)

图 9-3 在 *vgv01* 的 *lvol1* 上添加文件系统

如图本图所示，我们选择在 *vgv01* 的 *lvol1* 上添加文件系统。

接下来，我们需要修改逻辑卷的默认设置，如本图 9-4 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_502_0.png)

图 9-4 修改文件系统默认设置

在此界面中，我们需要确保*允许大文件*，因为我们将运行会创建许多大文件的数据库应用程序。如果我们在创建文件系统时未包含大文件支持，且正在运行 Online JFS，我们仍可使用 `fsadm` 命令将其转换为支持大文件。我们希望现在挂载此文件系统，并在系统启动时自动挂载，以便在 `/etc/fstab` 中生成相应的条目。

![](img/eff8b9287a5f38c5adf538f24aacf29e_503_0.png)

图 9-5 十个逻辑卷上的十个 VxFS 文件系统

使用 SAM，我们在所有十个 lvol1 上创建了十个 VxFS 文件系统。我们必须在 SAM 中逐个创建这十个文件系统，因此使用 shell 程序进行自动化处理可能更为合适。

SAM 会自动将这些条目添加到 /etc/fstab，因为我们指定了立即挂载并在系统启动时挂载，如下所示：

```text
# System /etc/fstab file. Static information about the file systems
# See fstab(4) and sam(1M) for further details on configuring devices.
/dev/vg00/lvol3 / vxfs delaylog 0 1
/dev/vg00/lvol1 /stand bfs defaults 0 1
/dev/vg00/lvol4 /opt vxfs delaylog 0 2
/dev/vg00/lvol5 /tmp vxfs delaylog 0 2
/dev/vg00/lvol6 /usr vxfs delaylog 0 2
/dev/vg00/lvol7 /var vxfs delaylog 0 2
/dev/vg00/lvol8 /home vxfs delaylog 0 2
/dev/vg00/lvol9 ... swap pri=0 0 0
/dev/vsapp/lvol1 /app vxfs rw, suid, largefiles, delaylog, datainlog 0 2
/dev/vgv01/lvol1 /u01 vxfs rw, suid, largefiles, delaylog, datainlog 0 2
/dev/vgv02/lvol1 /u02 vxfs rw, suid, largefiles, delaylog, datainlog 0 2
/dev/vgv03/lvol1 /u03 vxfs rw, suid, largefiles, delaylog, datainlog 0 2
/dev/vgv04/lvol1 /u04 vxfs rw, suid, largefiles, delaylog, datainlog 0 2
/dev/vgv05/lvol1 /u05 vxfs rw, suid, largefiles, delaylog, datainlog 0 2
/dev/vgv06/lvol1 /u06 vxfs rw, suid, largefiles, delaylog, datainlog 0 2
/dev/vgv07/lvol1 /u07 vxfs rw, suid, largefiles, delaylog, datainlog 0 2
/dev/vgv08/lvol1 /u08 vxfs rw, suid, largefiles, delaylog, datainlog 0 2
/dev/vgv09/lvol1 /u09 vxfs rw, suid, largefiles, delaylog, datainlog 0 2
/dev/vgv10/lvol1 /u10 vxfs rw, suid, largefiles, delaylog, datainlog 0 2
```

此列表显示了我们的十个逻辑卷，其中最后十个条目包含了我们设置的参数，例如 VxFS 和大文件支持。

没有任何理由表明我们不能在命令行中执行文件系统相关命令，例如 **newfs** 和 **fsadm**，就像我们之前执行卷相关命令一样。由于大多数人使用 SAM 执行这些操作，因此我认为使用 SAM 来说明会更为恰当。

下一节将提供一些使用逻辑卷管理器时可能需要执行的各种操作提示。这些都是我多次使用过的操作，当你需要执行类似任务时可能会对你有所帮助。

### 常用 LVM 操作

系统管理员在执行任何侵入性（存在更改 LVM 相关内容的可能性）LVM 命令之前通常都很谨慎。在执行任何侵入性 LVM 命令之前，请务必备份系统，并使用 Ignite-UX 创建可引导的恢复磁带。以下是我常规遇到的一些任务的操作步骤。请根据你的需求进行修改。请勿直接运行所示命令。你需要准备系统，替换卷的名称，并执行额外的步骤。不过，这些命令可以作为展示如何执行上述任务的良好示例。

我们要执行的第一个任务是在未镜像的系统上更换故障磁盘（图 9-6）。

```text
# vgrecreate -a /dev/vgXX /dev/rmdsk/cxtx0d
# vgchange -a y /dev/vgXX
# newfs -F vxfs /dev/vgXX/lvol1
# mount /mountpointname
```

注意事项：
- 确认你拥有 /etc/lvmconf/vgXX.conf
- vgcgbackup 会自动运行
- 故障磁盘在失效前未进行镜像
- 你的系统可能需要额外的步骤

### 图 9-6 更换非镜像磁盘

在此示例中，我们有一块非镜像且非根磁盘出现故障并需要更换。更换磁盘后，使用 **vgrecreate** 恢复该特定磁盘的卷组信息。然后，我们将卷组更改为可用状态，在磁盘上运行 **newfs**，并挂载使用该磁盘的文件系统。

在图 9-7 中，我们将再次更换故障的非根磁盘，但这次磁盘是镜像的。

```text
# vgcfgrestore - /dev/vgXX /dev/rdsk/cxtxdx ; volume group configuration restore
# vgchange -a y /dev/vgXX ; change volume group to available (-a y)
# vgsync /dev/vgXX ; resync logical volumes in volume group
```

注意事项：
- 故障磁盘在失效前是镜像的
- 你的系统可能需要额外的步骤

### 图 9-7 更换镜像磁盘

在此示例中，我们执行了与前两个相同的步骤，即恢复卷组配置并将卷组更改为可用状态。由于磁盘是镜像的，我们只需使用 vgsync 同步新磁盘与其镜像上的数据即可。

在图 9-8 中，我们将再次更换镜像磁盘，但这次磁盘上有引导区域。

```text
# vgcfgrestore - /dev/vgXX /dev/rdsk/ext0xd  ; volume group configuration restore
# vgchange -a y /dev/vgXX                         ; change volume group to available (-a y)
# vgsync /dev/vgXX                                 ; resync logical volumes in volume group
# mkboot /dev/rdsk/ext0xd                          ; create boot area on disk
# mkboot -a "hpux 1q" /dev/rdsk/ext0xd             ; specify low quorum in boot area
# shutdown <desired options>                        ; reboot system to take effect
```

注意事项：
- vgcfgbackup 会自动运行
- 确认你拥有 /etc/lvmconf/vgXX.conf
- 故障磁盘在失效前是镜像的
- 你的系统可能需要额外的步骤

### 图 9-8 更换带有引导区域的镜像磁盘

在此示例中，我们执行了与前一个示例相同的前三个步骤，但还需要在磁盘上创建引导区域。系统必须重新启动才能生效。

在图 9-9 中，我们要将一个卷组迁移到不同的系统上。

在系统 1 上：

```text
# vgchange -a n /dev/vgXX ; change volume group to unavailable (-a n) on 1st system
# vgexport -v -m mapfile -s /dev/vgXX ; make volume group unavailable on 1st system, mapfile will have to be copied to 2nd system, but you don’t have to specify here if standard volume names are used
```

在系统 2 上：

```text
# mkdir /dev/vgXX ; make directory on 2nd system for volume group
# mknod /dev/vgXX/group c 64 0xy0000 ; create special file for vol group (xy=group number such as 00 for vg00, 01 for vg01, and so on)
# vgimport -v -m mapfile -s /dev/vgXX ; import volume group using mapfile copied from 1st system or specify device filenames
# vgchange -a y /dev/vgXX ; make volume group available
```

- 编辑 /etc/fstab 或使用 SAM 以包含新的文件系统

注意事项：
- **vgcfgbackup** 会自动运行
- 你的系统可能需要额外的步骤

### 图 9-9 导出（移除）卷组并将其导入到另一系统

在此示例中，我们在从中迁移卷组的系统上执行了前两个步骤。我们使卷组不可用，然后导出卷组。需要将第一个系统中的 mapfile 复制到第二个系统。如果使用 /dev/vg01 等标准名称，则无需指定 mapfile 名称。无论如何，都必须将 mapfile 复制到卷组正在迁移到的系统。

在第二个系统上，我们为新的卷组创建目录和设备特殊文件。然后导入卷组的 mapfile 并使卷组处于活动状态。最后一步是在 **fstab** 中添加用于挂载文件系统的条目。

图 9-10 显示了将 VxFS 文件系统扩展 800 MBytes。




# lvextend -L 800 /dev/vgXX/rvolY；将逻辑卷 `rvolY` 扩展 800 MB
# fsadm -F vxs -b 800M /mountpointname；使用 **fsadm** 进行扩展，或在非 JFS 文件系统上使用 **extendfs**

注意：

这是 VxFS 文件系统，且系统上已安装 Online JFS

您的系统可能还需要额外的步骤

![](img/eff8b9287a5f38c5adf538f24aacf29e_509_0.png)

首先，我们使用 **lvextend** 指定要扩展的大小和原始逻辑卷。然后，我们使用 **fsadm** 来应用该更改。

图 9-11 展示了将 VxFS 文件系统更改以支持大文件的示例。

# fsadm -F vxfs -o largefiles /dev/vgXN/rlvolY

：使用 fsadm 并指定 largefile 选项

注意：

这是 VxFS 文件系统，对于 hfs 文件系统，您可以在上述示例中用 hfs 替换 vxfs，并用 rlvol1 替换 rlvoyl
在运行之前取消挂载文件系统

您的系统可能还需要额外的步骤

图 9.11 修改逻辑卷以支持大文件

使用 **fsadm**，我们指定希望支持大文件的原始逻辑卷。

如果逻辑卷在创建时已设置为支持大文件，则此更改将无需进行。

### 重新配置部分磁盘：使用部分逻辑卷命令的示例

我在我撰写的书籍和文章中一直建议，在首次为 HP-UX 系统设置磁盘时务必格外小心，确保所选的磁盘布局是能够长期适用的。然而，无论您多么谨慎，通常仍需要执行一些逻辑卷重新配置操作。与系统在首次安装时正确配置相比，修改现有的逻辑卷布局要困难得多。本节描述了在现有系统上对转储（dump）和镜像（mirror）进行一些更改所执行的步骤。

这不是建议您遵循的标准流程，而是一个展示高级逻辑卷管理器（LVM）命令如何用于重新配置特定系统上部分磁盘的示例。它是一个很好的流程，用于说明多个 LVM 命令的使用方式。

### 为什么要更改？

图 9-12 显示了系统的原始磁盘配置以及我们希望实现的更新配置。
此处的总体目标是：将用作根磁盘镜像的 4 GByte 磁盘移动到不同的 SCSI 通道，并在与根磁盘相同的 SCSI 通道上安装 2 GByte 的转储设备。

### 磁盘重新配置示意图

![](img/eff8b9287a5f38c5adf538f24aacf29e_512_0.png)

图 9.12 磁盘重新配置示意图

该流程由几个部分组成。第一部分是获取系统在重新配置前的快照。这有两个目的。首先是提供原始系统配置的文档，可将其纳入系统管理手册中。如果未来对原始配置及其所做的更改有任何疑问，原始配置将记录在系统管理手册中。持有此信息的第二个目的是，在进行重新配置过程时，使所有相关的配置信息可用。

流程的第二部分是关闭系统，安装新的 2 GByte 磁盘，并移动 4 GByte 磁盘。

流程的最后部分是执行转储和镜像的系统管理重新配置。

图 9-13、9-14 和 9-15 展示了一个流程图，描述我们在本节中将遵循的流程。接下来流程中的步骤编号与这些图中显示的步骤编号相对应。现在，让我们从获取系统快照开始。

![](img/eff8b9287a5f38c5adf538f24aacf29e_514_0.png)

获取现有配置的快照并将输出保存到目录。
```shell
# lscan -funC.disk     # hdfl
# vgdisplay -v         # swapinfo
# lvdisplay -v /dev/vg00/lv0* # lvboot, /dev/vg00
# 0 /dev/vg00*         # hdic, -cb, /dev/dsk/c0t0d0
```

将 /dev/vg00 中所有逻辑卷的镜像减少至零。
```shell
# lvreduce -n 0 /dev/vg00/lv0*  至 lv07
```

检查“镜像副本”是否等于零（无需 -v 选项）。
```shell
# lvdisplay /dev/vg00/lv0* -v more
```

从 vg00 中移除 /dev/dsk/c0t5d0，这是 /dev/dsk/c0t6d0 的镜像。
```shell
# vgreduce /dev/vg00 /dev/dsk/c0t5d0
```

使用 vgdisplay -v 验证 c0t5d0 已移除。
PV 名称 /dev/dsk/c0t5d0 不应再出现在列表中，只有 c0t6d0。
```shell
# vgdisplay -v
```

验证 “dump lv0” 是否在 /stand/system 中。如果不在，请添加它，并使用 11.x 系统管理手册中的流程重新配置内核。

执行硬件升级：位于 100.5.0 的 4 GByte 磁盘 /dev/dsk/c0t5d0
变为：/dev/dsk/c11t0 / 10043.5.0；在 100.5.0 处的 /dev/dsk/c0t5d0 添加新的 2 GByte 磁盘
仅用于转储目的。

重新启动后，使用 lscan 验证新磁盘是否在正确的地址就位。
```shell
# lscan -funC.disk
```

使用 vgdisplay 查看 c0t6d0 是 vg00 中唯一的磁盘，且其他卷组保持不变。
```shell
# vgdisplay -v /dev/vg00
# vgdisplay -v /dev/vg-other>
```

# 图 9-13 磁盘重新配置流程图 - 第 1 部分（重新排列磁盘）

# 磁盘重新配置流程图 - 第 2 部分

接续第 1 部分。

- F10
- 使用 vgextend 将 1 GByte 磁盘 /dev/dsk/ct1s00（位于 10/4/4.0）添加到 vg00
- 用于镜像目的。
- # vgextend /dev/vg00 /dev/dsk/ct1s10

- F11
- 为新的 2 GByte 磁盘 /dev/dsk/ct5s00（位于 100.5.0）创建物理卷。
- # pvcreate -f /dev/dsk/ct5s00

- F12
- 使用 vgextend 将 2 GByte 磁盘 /dev/dsk/ct5s00（位于 100.5.0）放入 vg00
- # vgextend /dev/vg00 /dev/dsk/ct5s00

- F13
- 使用 vgdisplay 验证 /dev/vg00 中现在有三个磁盘：ct0s60 -
- 原始磁盘，ct1s00 - 将是镜像，ct5s00 - 将是转储。
- # vgdisplay -v /dev/vg00

- F14
- 在 /dev/vg00 上创建用于转储的逻辑卷，命名为 dump。
- # lvcreate -n dump /dev/vg00

- F15
- 将用于转储的逻辑卷扩展到 2 GBytes：
- 逻辑区 = 508 x 4 MBytes (except)
- # lvextend -L 508 /dev/vg00/dump /dev/dsk/ct5s00

- F16
- 使用 lvdisplay 查看转储逻辑卷。
- # lvdisplay /dev/vg00/dump

- F17
- 使用 lvchange 使转储 lvol 连续，并使用 lvlnboot 添加转储
- # lvchange -cy /dev/vg00/dump
- # lvlnboot -d /dev/vg00/dump

- F18
- 查看转储设备：ct0s60 是主设备 (0)，ct5s00 是次设备 (1)。
- # lvlnboot -v
- 部分输出：Dump lvol2: on: /dev/dsk/ct0s60, 0
- Dump dump: on: /dev/dsk/ct5s00, 1

![](img/eff8b9287a5f38c5adf538f24aacf29e_515_0.png)

# 磁盘重新配置流程图 - 第 3 部分

接续第 2 部分。

使用 `lvextend` 将 `cl060` 上的所有逻辑卷镜像到 `cl030`。  
`# lvextend -m 1 /dev/vg00/lvol1 /dev/disk/cl030`  
lvol2  
lvol3  
lvol4  
lvol5  
lvol6  
lvol7

使用 `lvdisplay` 验证逻辑卷已镜像。  
`# lvdisplay -v /dev/vg00/lvol* | more`

重新启动系统以确认所有更改已生效。将密钥拨到“服务模式”，输入 `tc` 进入命令模式，并使用 `Transfer Control` (`tc`) 命令创建核心转储。  
`CM> tc`

重新启动后，使用 `savecore` 将核心转储保存到磁带中。即使未使用，`/var/adm/crash` 也是该命令的必要部分。  
`# savecore -i /dev/rmt/0m /var/adm/crash`  
将磁带发送给 HP Response Center 以验证核心转储是否可以读取。

可选地，您可以从磁带中提取核心转储并放入 `/var/adm/crash`  
`# savecore -xt /dev/rmt/0m /var/adm/crash`

- F19
- F20
- F21
- F22
- F23

# 图 9-15 磁盘重新配置流程图 - 第 3 部分（恢复镜像）

## F1 - 扫描

首先，让我们运行 **ioscan** 以查看系统中的磁盘。

```
$ /user/sbin/ioscan -func disk
```

| 类 | H | I/N 路径 | 驱动程序 | S/N 状态 H/W 类型 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 磁盘 | 2 | 10/0/5.0 | adisk | CLAIMED DEVICE | SEAGATE ST3150W |
| | /dev/dsk/c0t5d0 | /dev/rdsk/c0t5d0 | | | |
| 磁盘 | 3 | 10/0/6.0 | adisk | CLAIMED DEVICE | SEAGATE ST3150W |
| | /dev/dsk/c0t6d0 | /dev/rdsk/c0t6d0 | | | |
| 磁盘 | 6 | 10/4/4.0 | adisk | CLAIMED DEVICE | SEAGATE ST31510W |
| | /dev/dsk/clt4d0 | /dev/rdsk/clt4d0 | | | |
| 磁盘 | 7 | 10/4/4.5.0 | adisk | CLAIMED DEVICE | SEAGATE ST31510W |
| | /dev/dsk/clt4d5d0 | /dev/rdsk/clt4d5d0 | | | |
| 磁盘 | 8 | 10/4/4.6.0 | sdisk | CLAIMED DEVICE | SEAGATE ST3120W |
| | /dev/dsk/clt6d8 | /dev/rdsk/clt6d8 | | | |
| 磁盘 | 9 | 10/4/12.4.0 | adisk | CLAIMED DEVICE | SEAGATE ST3180W |
| | /dev/dsk/c2t4d0 | /dev/rdsk/c2t4d0 | | | |
| 磁盘 | 10 | 10/4/12.5.0 | adisk | CLAIMED DEVICE | SEAGATE ST3180W |
| | /dev/dsk/c2t5d0 | /dev/rdsk/c2t5d0 | | | |
| 磁盘 | 11 | 10/4/12.6.0 | adisk | CLAIMED DEVICE | SEAGATE ST31510W |
| | /dev/dsk/c2t6d0 | /dev/rdsk/c2t6d0 | | | |
| 磁盘 | 5 | 10/12/5.2.0 | adisk | CLAIMED DEVICE | TOSHIBA CD-ROM XM-5401TA |
| | /dev/dsk/c3t2d0 | /dev/rdsk/c3t2d0 | | | |

请注意，此配置中的磁盘对应于图 9-4 顶部的磁盘。我们尚未查看与这些磁盘相关的逻辑卷信息，只查看了它们的物理地址。

## F1 - vgdisplay

接下来运行 **vgdisplay** 查看卷组。**vg0** 上的 **lv0l2** 是我们将移动到独立 2 GByte 磁盘上的转储逻辑卷。我们尚不确定 **vg0** 上的 **lv0l1-7** 是否都是镜像的。

```
# vgdisplay -v
--- 卷组 ---
VG 名称 /dev/vg00
VG 写访问 读/写
VG 状态 可用
最大 LV 255
当前 LV 7
打开的 LV 7
最大 PV 16
当前 PV 2
活动 PV 2
```




### 重新配置某些磁盘：使用某些逻辑卷命令的示例

```text
Max PE per PV 1023
VDGA 4
PE Size (Mbytes) 4
Current PE 349
Alloc PE 445
Free PE 578
Total PVG 1
--- Logical volumes
LV Name /dev/vg00/1vol1
LV Status available/syncd
LV Size (Mbytes) 48
Current LE 12
Allocated PE 30
Used PV -
LV Name /dev/vg00/1vol2
LV Status available/syncd
LV Size (Mbytes) 53
Current LE 32
Allocated PE 28
Used PV -
LV Name /dev/vg00/1vol3
LV Status available/syncd
LV Size (Mbytes) 20
Current LE 1
Allocated PE 10
Used PV 2
LV Name /dev/vg00/1vol4
LV Status available/syncd
LV Size (Mbytes) 252
Current LE 61
Allocated PE 25
Used PV 2
LV Name /dev/vg00/1vol5
LV Status available/syncd
LV Size (Mbytes) 32
Current LE 8
Allocated PE 16
Used PV 2
LV Name /dev/vg00/1vol6
LV Status available/syncd
LV Size (Mbytes) 320
Current LE 80
Allocated PE 160
Used PV 2
LV Name /dev/vg00/1vol7
LV Status available/syncd
LV Size (Mbytes) 140
Current LE 40
Allocated PE 80
Used PV 2
--- Physical volumes
PV Name /dev/dsk/c0t6d0
PV Status available
Total PE 1024
Free PE 679
PV Name /dev/dsk/c0t5d0
PV Status available
Total PE 1023
Free PE 679
```

### F1 - lvidsplay

使用 lvidsplay 查看详细的逻辑卷信息。请注意，所有这些逻辑卷都是镜像的，并且每个都具有“当前”状态。列表中仅显示了 lv01 和 lv02。lv03 到 lv07 未显示。

```text
# lvidsplay -v /dev/vg00/lvol* 

--- Logical volumes ---
LV Name   /dev/vg00/lvol01
VG Name   /dev/vg00
LV Permission   read/write
LV Status available/syncd
Mirror copies 1
Consistency Recovery MWC
Schedule parallel
LV Size (Mbytes) 92
Current LE 23
Allocated PE 46
Stripes 0
Stripe Size (Kbytes) 0
Bad block off
Allocation strict/contiguous
```

```text
--- Distribution of logical volume ---
PV Name   LE on PV PE on PV
/dev/dsk/c0t0d0   23 23
/dev/dsk/c0t5d0   23 23
```

```text
--- Logical extents ---
LE  PVI  BPI  Status 1  PVS  PE2  Status 2
0000 /dev/dsk/c0t6d0   0000 current /dev/dsk/c0t5d0   0000 current
0001 /dev/dsk/c0t6d0   0001 current /dev/dsk/c0t5d0   0001 current
0002 /dev/dsk/c0t6d0   0002 current /dev/dsk/c0t5d0   0002 current
0003 /dev/dsk/c0t6d0   0003 current /dev/dsk/c0t5d0   0003 current
0004 /dev/dsk/c0t6d0   0004 current /dev/dsk/c0t5d0   0004 current
0005 /dev/dsk/c0t6d0   0005 current /dev/dsk/c0t5d0   0005 current
0006 /dev/dsk/c0t6d0   0006 current /dev/dsk/c0t5d0   0006 current
0007 /dev/dsk/c0t6d0   0007 current /dev/dsk/c0t5d0   0007 current
0008 /dev/dsk/c0t6d0   0008 current /dev/dsk/c0t5d0   0008 current
0009 /dev/dsk/c0t6d0   0009 current /dev/dsk/c0t5d0   0009 current
0010 /dev/dsk/c0t6d0   0010 current /dev/dsk/c0t5d0   0010 current
0011 /dev/dsk/c0t6d0   0011 current /dev/dsk/c0t5d0   0011 current
0012 /dev/dsk/c0t6d0   0012 current /dev/dsk/c0t5d0   0012 current
0013 /dev/dsk/c0t6d0   0013 current /dev/dsk/c0t5d0   0013 current
0014 /dev/dsk/c0t6d0   0014 current /dev/dsk/c0t5d0   0014 current
0015 /dev/dsk/c0t6d0   0015 current /dev/dsk/c0t5d0   0015 current
0016 /dev/dsk/c0t6d0   0016 current /dev/dsk/c0t5d0   0016 current
0017 /dev/dsk/c0t6d0   0017 current /dev/dsk/c0t5d0   0017 current
0018 /dev/dsk/c0t6d0   0018 current /dev/dsk/c0t5d0   0018 current
0019 /dev/dsk/c0t6d0   0019 current /dev/dsk/c0t5d0   0019 current
0020 /dev/dsk/c0t6d0   0020 current /dev/dsk/c0t5d0   0020 current
0021 /dev/dsk/c0t6d0   0021 current /dev/dsk/c0t5d0   0021 current
0022 /dev/dsk/c0t6d0   0022 current /dev/dsk/c0t5d0   0022 current
```

```text
LV Name   /dev/vg00/lvol02
VG Name   /dev/vg00
LV Permission   read/write
LV Status available/syncd
Mirror copies 1
Consistency Recovery MWC
Schedule parallel
LV Size (Mbytes) 50
Current LE 25
Allocated PE 250
Stripes 0
Stripe Size (Kbytes) 0
Bad block Off
Allocation strict/contiguous
```

```text
--- Distribution of logical volume ---

PV Name LE on PV PE on PV
/dev/dsk/c0t6d0 125 125
/dev/dsk/c0t5d0 1 1
```

```text
--- Logical extents ---

LE PV1 PE1 Status 1 PV2 PE2 Status 2

0000 /dev/dsk/c0t6d0 0023 current /dev/dsk/c0t5d0 0023 current
0001 /dev/dsk/c0t6d0 0024 current /dev/dsk/c0t5d0 0024 current
0002 /dev/dsk/c0t6d0 0025 current /dev/dsk/c0t5d0 0025 current
0003 /dev/dsk/c0t6d0 0026 current /dev/dsk/c0t5d0 0026 current
0004 /dev/dsk/c0t6d0 0027 current /dev/dsk/c0t5d0 0027 current
0005 /dev/dsk/c0t6d0 0028 current /dev/dsk/c0t5d0 0028 current
0006 /dev/dsk/c0t6d0 0029 current /dev/dsk/c0t5d0 0029 current
0007 /dev/dsk/c0t6d0 0030 current /dev/dsk/c0t5d0 0030 current
0008 /dev/dsk/c0t6d0 0031 current /dev/dsk/c0t5d0 0031 current
0009 /dev/dsk/c0t6d0 0032 current /dev/dsk/c0t5d0 0032 current
0010 /dev/dsk/c0t6d0 0033 current /dev/dsk/c0t5d0 0033 current
0011 /dev/dsk/c0t6d0 0034 current /dev/dsk/c0t5d0 0034 current
0012 /dev/dsk/c0t6d0 0035 current /dev/dsk/c0t5d0 0035 current
0013 /dev/dsk/c0t6d0 0036 current /dev/dsk/c0t5d0 0036 current
```

```text
0014 /dev/dsk/c0t6d0 0134 current /dev/dsk/c0t5d0 0134 current
0015 /dev/dsk/c0t6d0 0135 current /dev/dsk/c0t5d0 0135 current
0016 /dev/dsk/c0t6d0 0136 current /dev/dsk/c0t5d0 0136 current
0017 /dev/dsk/c0t6d0 0137 current /dev/dsk/c0t5d0 0137 current
0018 /dev/dsk/c0t6d0 0138 current /dev/dsk/c0t5d0 0138 current
0019 /dev/dsk/c0t6d0 0139 current /dev/dsk/c0t5d0 0139 current
0020 /dev/dsk/c0t6d0 0140 current /dev/dsk/c0t5d0 0140 current
0021 /dev/dsk/c0t6d0 0141 current /dev/dsk/c0t5d0 0141 current
0022 /dev/dsk/c0t6d0 0142 current /dev/dsk/c0t5d0 0142 current
0023 /dev/dsk/c0t6d0 0143 current /dev/dsk/c0t5d0 0143 current
0024 /dev/dsk/c0t6d0 0144 current /dev/dsk/c0t5d0 0144 current
0025 /dev/dsk/c0t6d0 0145 current /dev/dsk/c0t5d0 0145 current
0026 /dev/dsk/c0t6d0 0146 current /dev/dsk/c0t5d0 0146 current
0027 /dev/dsk/c0t6d0 0147 current /dev/dsk/c0t5d0 0147 current
```

接下来，查看 /dev/vg00 以记录逻辑卷。

```text
# ll /dev/vg00
/dev/vg00:
total 6
crw-r--- 1 root sys 64 0x000000 May 29 04:44 group
brw-r--- 1 root sys 64 0x000001 May 29 04:44 lv01
brw-r--- 1 root sys 64 0x000002 Jul 9 17:10 lv0l2
brw-r--- 1 root sys 64 0x000003 May 29 04:44 lv0l3
brw-r--- 1 root sys 64 0x000004 May 29 04:44 lv0l4
brw-r--- 1 root sys 64 0x000005 May 29 04:44 lv0l5
brw-r--- 1 root sys 64 0x000006 May 29 04:44 lv0l6
crw-r--- 1 root sys 64 0x000007 May 29 04:44 lv0l7
crw-r--- 1 root sys 64 0x000002 Jul 9 17:10 rlv01l2
crw-r--- 1 root sys 64 0x000003 May 29 04:44 rlv0l3
crw-r--- 1 root sys 64 0x000004 May 29 04:44 rlv0l4
crw-r--- 1 root sys 64 0x000005 May 29 04:44 rlv0l5
```

接下来，查看 /dev/vg_nw 以及其他任何卷组。

```text
$ ll /dev/vg_nw
/dev/vg_nw:
total 0
crw--tw-- 1 root sys  64 0x010000  Jul  9 2:03 group
brw-------  1 root  sys  64  0x010001 Jul  9 3:01  lv_nwbackup
brw-------  1 root  sys  64  0x010004 Jul  9 3:01  lv_mlog
brw-------  1 root  sys  64  0x010052 Jul  9 2:54  lv_nwsys
brw-------  1 root  sys  64  0x010001 Jul  3 2:55 lv_nwnext
brw-------  1 root  sys  64  0x010003 Jul  9  2:03  lv_nwbackup
crw--tw--  1 root  sys  64  0x010004 Jul  9  3:01  rlv_nwlog
crw--tw--  1 root  sys  64  0x010002 Jul  9  2:55  rlv_nwsys
crw--tw--  1 root  sys  64  0x010001 Jul  9  2:54 rlv_nwnext
```

### F1 - bdfl

接下来，使用 bdfl 查看文件系统。请注意，lvol1 未显示，因为它是交换和转储设备。

```text
$ bdfl
FileSystem             kbtes    used    avail   %used  Mounted on
/dev/vg00/ivoll1       31669    ??     56013     ?    /
/dev/vg00/ivol7       155089   81300  59528    58    /opt
/dev/vg00/ivoll6       319135  ?       85300    ?    /
/usr /dev/vg00/ivol5    ?        ?       ?       ?    /tmp
/dev/vg06/ivol4        255285   67854  158302   26    /usr
/dev/vg_nw/lv_nwnext   4090465  207905  163911   ?    /nextext
/dev/vg_nw/lv_nwsys    4099465  1063900  2825839  ?    /nwsys
/dev/vg_nw/lv_mlog    95689    ?     72389      ?    /nwlog
/dev/vg_nw/lv_nwbackup 2552537 373388 1919895   ?    /nwbackup
/dev/vg00/ivol3        15881    ?     2191     15    /home
```

### F1 - swapinfo

接下来，运行 swapinfo 以查看 lvol2 是唯一的交换设备。

```text
$ swapinfo
          Type    AVAIL      USED     FREE     PCT   START/   LIMIT        RESERVE   PRI    NAME
/dev 0         512000    -    512000    0%          -            0          1      /dev/vg00/lvol2
reserve       -    512000    512000
memory     1670828  1474704  196124     88%
```





## F1 - lvlnboot

接下来，使用 `lvlnboot` 查看引导信息。`vg00` 上的 `lvol2` 是转储设备。

```
# lvlnboot -v /dev/vg00
Boot Definitions for Volume Group: /dev/vg00:
Physical Volumes belonging in Root Volume Group:
/dev/dsk/c0t5d0 (10/0.6.0) -- Boot Disk
/dev/dsk/c0t5d0 (10/0.6.0)
Root: lvol1 on: /dev/dsk/c0t5d0
Swap: lvol2 on: /dev/dsk/c0t5d0
Dump: lvol2 on: /dev/dsk/c0t5d0, 0
```

## F1 - lfls

使用 `lfls` 查看引导区。

```
# lfls -Civ /dev/dsk/c0t5d0
volume ISTD data size 7984 directory size 8 94/11/10 14:46:53
filename type start size implement created
CDE -12960 584 496 0 95/05/19 13:10:50
MAPFILE -12277 1080 32 0 95/05/19 13:16:50
SYSID -12280 1112 224 0 95/05/19 13:18:50
CONFINFO -12278 1336 62 0 95/05/19 13:14:50
LVMOD -12278 1400 70 0 95/05/19 13:15:50
SUNWY -12276 1472 68 0 95/05/19 13:16:50
SLUMDB -12276 1544 244 0 95/05/19 13:16:50
MAPPER -12279 1792 91 0 95/05/19 13:14:50
IOTEST -12279 1888 150 0 95/05/19 13:16:51
PERFVER -12279 2040 80 0 95/05/19 13:14:51
TUNT -12901 2120 64 0 95/05/19 13:18:52
SYSNGO -12980 2184 1 0 96/09/16 09:04:01
ZIL -12880 2192 240 0 94/11/04 15:46:52
AUID -12289 2432 1 0 94/11/04 15:44:54
HMIN -12928 2440 800 0 94/11/04 15:44:54
LABEL BIN 3240 8 0 96/05/29 01:43:52
```

## F2

在保存现有配置的所有适当信息后，我们可以开始重新配置。首先，使用 `lvreduce` 和 `-m` 选项打破镜像。

```
# lvreduce -m 0 /dev/vg00/lvol1
Logical volume "/dev/vg00/lvol1" has been successfully reduced.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
# lvreduce -m 0 /dev/vg00/lvol2
Logical volume "/dev/vg00/lvol2" has been successfully reduced.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
# lvreduce -m 0 /dev/vg00/lvol3
Logical volume "/dev/vg00/lvol3" has been successfully reduced.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
# lvreduce -m 0 /dev/vg00/lvol4
Logical volume "/dev/vg00/lvol4" has been successfully reduced.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
# lvreduce -m 0 /dev/vg00/lvol5
Logical volume "/dev/vg00/lvol5" has been successfully reduced.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
# lvreduce -m 0 /dev/vg00/lvol6
Logical volume "/dev/vg00/lvol6" has been successfully reduced.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
# lvreduce -m 0 /dev/vg00/lvol7
Logical volume "/dev/vg00/lvol7" has been successfully reduced.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
```

你可以逐条输入命令，或者创建一个包含这些 `lvreduce` 命令的文件并运行该文件。你可以将文件命名为 `/tmp/reduce`，其中包含以下内容：

```
lvreduce -m 0 /dev/vg00/lvol1
lvreduce -m 0 /dev/vg00/lvol2
lvreduce -m 0 /dev/vg00/lvol3
lvreduce -m 0 /dev/vg00/lvol4
lvreduce -m 0 /dev/vg00/lvol5
lvreduce -m 0 /dev/vg00/lvol6
lvreduce -m 0 /dev/vg00/lvol7
```

创建此文件后，将其更改为可执行文件，然后使用以下两条命令运行。

```
# chmod 555 /tmp/reduce
# /tmp/reduce
```

随后，你将看到运行 `lvreduce` 命令的所有输出。

## F3

使用 `lvdisplay` 检查 `lvol1` 到 `lvol7` 的镜像是否已减少。查看镜像副本是否等于 0。在此列表中仅显示了 `lvol1` 到 `lvol3`。

### 重新配置某些磁盘：使用某些逻辑卷命令的示例

```
# lvdisplay -v /dev/vg00/lvol* | more
--- Logical volumes
LV Name           /dev/vg00/lvol1
VG Name           /dev/vg00
LV Permission     read/write
LV Status         available/syncd
Mirror copies     0
Consistency Recovery MWC
Schedule          parallel
LV Size (Mbytes)  92
Current LE        23
Allocated PE      -
Stripes           0
Stripe Size (Kbytes) 0
Bad block         off
Allocation        strict/contiguous

LV Name           /dev/vg00/lvol2
VG Name           /dev/vg00
LV Permission     read/write
LV Status         available/syncd
Mirror copies     0
Consistency Recovery MWC
Schedule          parallel
LV Size (Mbytes)  500
Current LE        125
Allocated PE      125
Stripes           0
Stripe Size (Kbytes) 0
Bad block         off
Allocation        strict/contiguous

LV Name           /dev/vg00/lvol3
VG Name           /dev/vg00
LV Permission     read/write
LV Status         available/syncd
Mirror copies     0
Consistency Recovery MWC
Schedule          parallel
LV Size (Mbytes)  20
Current LE        5
Allocated PE      5
Stripes           0
Stripe Size (Kbytes) 0
Bad block         on
Allocation        n't't.
```

## F4

现在使用 `vgreduce` 将 `c0t5d0` 从 `vg00` 中移除。由于没有镜像存在，这种方法将有效。该磁盘将被放置在另一个 SCSI 控制器上，并将在后续步骤中再次用于镜像。

```
# vgreduce /dev/vg00 /dev/dsk/c0t5d0
Volume Group /dev/vg00 has been successfully reduced.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
```

## F5

此时，`c0t5d0` 不再位于 `vg00` 中。使用 `vgdisplay` 验证 "PV Name" `c0t5d0` 是否已不在 `vg00` 中。

```
# vgdisplay -v
```

`vg00` 中不应再有 `c0t5d0`。

## F6

验证 "dump lvol" 是否在 /stand/system 中。如果没有，请添加 "dump lvol" 并重新配置内核。请参见第 1 章中的内核重建过程。

## F7

现在进行硬件升级。系统关闭，添加并移动磁盘驱动器，然后系统重新启动。4 GByte 磁盘 `/dev/dsk/c0t5d0` 变为地址 10/4/4,3.0 处的 `/dev/dsk/c1t3d0`，并引入一个新的 2 GByte 磁盘作为 10/0,5.0，设备名称为 `/dev/dsk/c0t5d0`。图 9-4 的第二部分描绘了此变更。

## F8

硬件升级后要执行的第一项活动是使用 `ioscan` 查看新磁盘。现在，10/0,5.0 处有一个 2 GByte 磁盘，10/4/4,3.0 处有一个 4 GByte 磁盘。

```
# iostat -func disk
```

| 类别 | I | H/W 路径 | 驱动程序 | S/W 状态 | H/W 类型 | 描述 |
|---|---|---|---|---|---|---|
| 磁盘 | 2 | 10/0,5.0 | sdisk | CLAIMED | DEVICE | SEAGATE ST332555W |
| 磁盘 | 3 | 10/0,6.0 | sdisk | CLAIMED | DEVICE | SEAGATE ST31550W |
| 磁盘 | 12 | 10/4/4.3.0 | sdisk | CLAIMED | DEVICE | SEAGATE ST15150W |
| 磁盘 | 6 | 10/4/4.4.0 | sdisk | CLAIMED | DEVICE | SEAGATE ST15150W |
| 磁盘 | 7 | 10/4/4.5.0 | sdisk | CLAIMED | DEVICE | SEAGATE ST15150W |
| 磁盘 | 8 | 10/4/4.6.0 | sdisk | CLAIMED | DEVICE | SEAGATE ST15150W |
| 磁盘 | 9 | 10/4/12.4.0 | sdisk | CLAIMED | DEVICE | SEAGATE ST15150W |
| 磁盘 | 10 | 10/4/12.5.0 | sdisk | CLAIMED | DEVICE | SEAGATE ST15150W |
| 磁盘 | 11 | 10/4/12.6.0 | sdisk | CLAIMED | DEVICE | SEAGATE ST15150W |
| 磁盘 | 5 | 10/12/5.2.0 | sdisk | CLAIMED | DEVICE | TOSHIBA CD-ROM XM-5401TA |

## F9

现在我们运行 `vgdisplay` 以查看新的卷组信息。只有 `c0t6d0` 在 `vg00` 中，并且尚未配置镜像。其他卷组保持不变。在我们的示例中，仅显示 `lvol1` 到 `lvol3`。

```
# vgdisplay -v

--- Volume groups ---
VG Name                 /dev/vg00
VG Write Access         read/write
VG Status               available
Max LV                  255
Cur LV                  7
Open LV                 7
Max PV                  16
Cur PV                  1
Act PV                  1
Max PE per VV           1023
VVDA                    2
PE Size (Mbytes)        4
Total PE                1023
Alloc PE                344
Free PE                 679
Total PVG               0

--- Logical volumes ---
LV Name                 /dev/vg00/lvol1
LV Status               available/syncd
LV Size (Mbytes)        92
Current LE              23
Allocated PE            23
Used PV                 1
```




# F9

仅显示 `/dev/vg_nw` 中的前三个逻辑卷。

```
# vgdisplay -v /dev/vg_nw
VG Name /dev/vg_nw
VG Write Access read/write
VG Status available
Max LV 2^5
Cur LV 4
Open LV 4
Max PV 1
Cur PV 6
Act PV 6
Max PE per PV 6 ^2^3
VGDA 12
PE Size (Mbytes) 4
Total PE 6416
Alloc PE 5416
Free PE 722
Total PVs 2
--- Logical volumes ---
LV Name /dev/vg_nw/lv.nwtext
LV Status available/syncd
LV Size (Mbytes) 4092
Current LE 1023
Allocated PE 2046
Used PV 2

LV Name /dev/vg_nw/lv.nwsys
LV Status available/syncd
LV Size (Mbytes) 4092
Current LE 1023
Allocated PE 2046
Used PV 2

LV Name /dev/vg_nw/lv.nwbackup
LV Status available/syncd
LV Size (Mbytes) 2548
Current LE 637
Allocated PE 1274
Used PV 2
```

# F10

使用 `vgextend` 将 4 GByte 的磁盘添加到 `vg00` 以实现镜像（此处可能还需要运行 `pvcreate`）。

```
# vgextend /dev/vg00 /dev/dsk/c1t3d0
Volume group `/dev/vg00' has been successfully extended.
Volume Group configuration for /dev/vg00 has been saved in `/etc/lvmconf/vg00.conf'
```

# F11

现在我们可以创建新的 2 GByte 磁盘并将其添加到 `vg00` 中，使用以下两个命令：`pvcreate` (F11) 用于创建物理卷，`vgextend` (F12) 用于扩展卷组。

```
# pvcreate -f /dev/rdsk/c0t5d0
Physical volume `/dev/rdsk/c0t5d0* has been successfully created.
```

# F12

```
# vgextend /dev/vg00 /dev/dsk/c0t5d0
Volume group `/dev/vg00' has been successfully extended.
Volume Group configuration for /dev/vg00 has been saved in `/etc/lvmconf/vg00.conf'
```

# F13

我们可以使用 `vgdisplay` 检查这两个磁盘是否确实已添加到 `vg00`。在我们的示例中，仅显示 `lvoll` 到 `lv013`。

显示的末尾部分是列表中的重要部分，显示三个物理卷。

```
# vgdisplay -v /dev/vg00

--- Volume groups ---
VG Name /dev/vg00
VG Write Access read/write
VG Status available
Max LV 255
Cur LV 7
Open LV /
Max PV 8
Cur PV 1
Act PV 1
Max PE per PV 1051
VGA
PG Size (Mbytes) 4
Total PE 456
Alloc PE 444
Free PE 12
Total PVs 1

--- Logical volumes ---
LV Name /dev/vg00/lv01
LV Status available/syncd
LV Size (Mbytes) 32
Current LE 33
Allocated PE 32
Used PV 1

LV Name /dev/vg00/lv02
LV Status available/syncd
LV Size (Mbytes) 900
Current LE 125
Allocated PE 125
Used PV 1

LV Name /dev/vg00/lv013
LV Status available/syncd
LV Size (Mbytes) 20
Current LE 5
Allocated PE 5
Used PV 1

--- Physical volumes ---
PV Name /dev/dsk/ct0d10
PV Status available
Total PE 1023
Free PE 679

PV Name /dev/dsk/ct32d0
PV Status available
Total PE 1023
Free PE 1023

PV Name /dev/dsk/ct54d0
PV Status available
Total PE 508
Free PE 508
```

# F14

我们现在可以使用 **lvcreate** (**F14**) 在 **vg00** 中创建 **dump** 逻辑卷，使用 **lvextend** (**F15**) 将其扩展到 **2 GB**，并使用 **lvdisplay** (**F16**) 查看它。

```
# lvcreate -n dump /dev/vg00
Logical volume "/dev/vg00/dump" has been successfully created with character device "/dev/vg00/rdump".
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
```

# F15

```
# lvextend -l 508 /dev/vg00/dump /dev/dsk/c0t5d0
Logical volume "/dev/vg00/dump" has been successfully extended.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
```

# F16

```
# lvdisplay /dev/vg00/dump | more
--- Logical volumes ---
LV Name           /dev/vg00/dump
VG Name           /dev/vg00
LV Permission     read/write
LV Status         available/syncd
Mirror copies     0
Consistency Recovery MWC
Schedule          parallel
LV Size (Mbytes)  2032
Current LE        508
Allocated PE      508
Stripes           0
Stripe Size (Kbytes) 0
Bad Block         on
Allocation        strict

--- Distribution of logical volume ---
PV Name    LE on PV  PE on PV
/dev/dsk/c0t5d0  508  0  508
```

# F17

为了使 **/dev/vg00/dump** 成为 **dump** 设备，我们必须首先使用 **lvchange** 使其连续，然后使用 **lvinboot** 将其设为 **dump** 设备。

```
# lvchange -C y /dev/vg00/dump
```

```
# lvinboot -d /dev/vg00/dump
```

# F18

查看 dump 设备。

```
# lvlnboot -v | more
Boot Definitions for Volume Group /dev/vg00:
Physical Volumes belonging in Root Volume Group:
  /dev/dsk/c0t6d0 (10/0.6.0) -- Boot Disk
  /dev/dsk/c1t3d0 (10/4/4.3.0) -- Boot Disk
  /dev/dsk/c0t5d0 (10/0.5.0)
Root: lvol1  on:  /dev/dsk/c0t6d0
Swap: lvol2  on:  /dev/dsk/c0t6d0
Dump: lvol2 on:  /dev/dsk/c0t6d0, 0
Dump: dump  on:  /dev/dsk/c0t5d0, 1
```

这可能不是你想要的结果。如“0”所示，主 dump 设备是 /dev/dsk/c0t6d0，如“1”所示，次要 dump 设备是 /dev/dsk/c0t5d0。我们可以选择重新执行此操作。让我们先继续对 /dev/vg00 上的 lvol 进行镜像，稍后再处理 dump 设备。

# F19

让我们现在使用 lvextend 扩展 vg00 中所有卷以用于一个镜像。

```
# lvextend -m 1 /dev/vg00/lvol1 /dev/dsk/c1t3d0
The newly allocated mirrors are now being synchronized.
This operation will take some time. Please wait . . .
Logical volume "/dev/vg00/lvol1" has been successfully extended.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
```

将以下内容放入 /tmp/mirror 并运行。lvol1 之前已扩展：lvol2 是交换分区，无需扩展：

```
lvextend -m 1 /dev/vg00/lvol3 /dev/dsk/c1t3d0
lvextend -m 1 /dev/vg00/lvol4 /dev/dsk/c1t3d0
lvextend -m 1 /dev/vg00/lvol5 /dev/dsk/c1t3d0
lvextend -m 1 /dev/vg00/lvol6 /dev/dsk/c1t3d0
lvextend -m 1 /dev/vg00/lvol7 /dev/dsk/c1t3d0
```

```
The newly allocated mirrors are now being synchronized.
This operation will take some time.
Please wait.... Logical volume "/dev/vg00/lvol2" has been successfully extended.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
```

# F20

让我们现在使用 `lvdisplay` 验证镜像是否已到位（仅显示 `lvol1` 和 `lvol2`）。

```
# lvdisplay -v /dev/vg00/lvol* | more

--- Logical volumes ---
LV Name                 /dev/vg00/lvol1
VG Name                 /dev/vg00
LV Permission            read/write
LV Status                available/syncd
Mirror copies            1
Consistency Recovery     mwc
Schedule                 parallel
LV Size [Mbytes]         52
Current LE               23
Allocated PE             46
Stripes                  0
Stripe Size [Kbytes]     0
Bad Block                off
Allocation               strict/contiguous

--- Distribution of logical volume ---
PV Name        LE on PV  PE on PV
/dev/dsk/c0t6d0   23     23
/dev/dsk/c1t3d0   23     23

--- Logical extents ---
LE          PV1            PE1   Status
0000 /dev/dsk/c0t6d0   0000 current   /dev/dsk/c1t3d0 0000 current
0001 /dev/dsk/c0t6d0   0001 current   /dev/dsk/c1t3d0 0001 current
0002 /dev/dsk/c0t6d0   0002 current   /dev/dsk/c1t3d0 0002 current
0003 /dev/dsk/c0t6d0   0003 current   /dev/dsk/c1t3d0 0003 current
```

您可以从此列表中看出，`c0t6d0` 在 `c1t3d0` 上进行了镜像。

# F21

重启系统以确认所有更改已生效。

重启后，执行以下操作以创建转储。对于 ^b 起作用，键必须处于“Service”位置（必须位于服务器上的系统控制台才能使其起作用）。

- 使用 ^b 获取 CM> 提示符。
- 在 CM> 提示符下使用 tc 命令创建核心转储。

# F22

系统在核心转储后会自动重启。使用以下命令将核心转储保存到磁带上。即使核心转储位于转储逻辑卷中而不是 /var/adm/crash 目录中，也需要 /var/adm/crash 文件名。

```
# savecore -t /dev/rmt/0m /var/adm/crash
```

# F23

然后使用 `savecore -xt` 和目录名来提取核心转储。如果您没有足够的空间容纳核心转储，或者想要更彻底的检查，您可以致电要求 HP 响应中心验证保存到磁带是否成功。

```
# savecore -xt /dev/rmt/0m /var/adm/crash
```

核心转储的空间需求是从转储的末尾向前计算的。因此，大约 1.5 GBytes 被写入转储逻辑卷，然后大约 600 MBytes 被写入 lvol2。




### 交换转储优先级的可选步骤

该步骤使用 lvrmb boot 从 /dev/srg00 中移除所有启动定义（包括 swap 和 dump），然后使用 lvrlnboot 重新创建它们。之所以需要这样做，是因为 lv012 是主要转储逻辑卷 (0)，而 dump 是次要转储逻辑卷 (1)。

必须重启系统才能使这些更改生效。图 9-16 展示了完成此可选步骤所需的步骤。

![Figure 9-16 更改转储优先级的步骤（可选）](img/eff8b9287a5f38c5adf538f24aacf29e_535_0.png)

## 图 9-16 更改转储优先级的步骤（可选）

- F24: 使用 lvmboot 完全从 **vg00** 中移除启动区域。

```
# lvmboot -r /dev/vg00
```

- F25: 使用 lvmboot 验证启动区域是否已被移除。

```
# lvmboot -v
```

卷组 /dev/vg00 的启动定义：启动数据区域为空。

- F26: 使用 lvmboot 将根逻辑卷分配给 /dev/vg00 上的 **lv0l1**。

```
# lvmboot -r lv0l1 /dev/vg00
```

- F27: 将交换空间（swap）分配给 /dev/vg00 上的 **lv0l2**。

```
# lvmboot -s lv0l2 /dev/vg00
```

```
# swapinfo
```

```
     Kb        Kb        Kb     PCT START/    Kb
TYPE    AVAIL   USED     FREE    USED LIMIT RESERVE PRI NAME
dev     512000      0    512000   0%    0        -   1 /dev/vg00/lv0l2
reserve -      23144   -23144             -
memory  1671008 27328  1643680  2%
```

- F28: 将转储分配给 /dev/vg00 上的逻辑卷 **dump**。

```
# lvmboot -d dump /dev/vg00
```

- F29: 将次要转储设备指定为 **lv0l2**（主要交换空间），位于 **lv0l2** 上。

```
# lvmboot -d lv0l2 /dev/vg00
```

- F30: 运行 **lvmboot** 以确认转储和交换空间已正确配置，优先级在 2 GByte 磁盘 **c0t5d0** 上为 "0"，在 **c0t6d0** 上为 "1"。

```
# lvmboot -v
# 添加 lv0l2 作为次要转储后
卷组 /dev/vg00 的启动定义：
属于根卷组的物理卷：
/dev/dsk/c0t5d0 (10/4/6.0) -> 启动磁盘
/dev/dsk/c0t6d0 (10/4/3.0) -> 启动磁盘
/dev/dsk/c0t5d0 (10/0.5.0)
根：/dev/dsk/c0t5d0 上的 lv0l1
交换：/dev/dsk/c0t5d0 /dev/dsk/c0t6d0 上的 lv0l2
转储：/dev/dsk/c0t5d0 上的 dump, 0
转储：/dev/dsk/c0t6d0 上的 dump, 1
```

- F31: 重启系统并运行步骤 F21-F23，以确认转储设备的正常运行。

虽然此磁盘重新配置步骤是针对特定系统的，但它对于说明执行此类任务所需的许多 LVM 命令非常有用。在我认为，在成熟的 HP-UX 安装中，LVM 和一般的磁盘管理是消耗系统管理时间的领域。此步骤中使用的许多命令没有“回退”的方法，因此在使用 LVM 命令时请务必谨慎。

![Image](img/eff8b9287a5f38c5adf538f24aacf29e_537_0.png)
![Image](img/eff8b9287a5f38c5adf538f24aacf29e_537_1.png)
![Image](img/eff8b9287a5f38c5adf538f24aacf29e_537_2.png)

### HP VERITAS 卷管理器

在撰写本文时，HP Veritas 卷管理器（本章大部分内容中我将其称为 VxVM）是一个从 HP-UX 11i 应用程序 CD-ROM 加载的软件产品。有一个名为“基础 HP VERITAS 卷管理器”的 VxVM 版本包含在 11i 中，还有一个名为“HP VERITAS 卷管理器”的完整版本。基础产品是完整版本的子集。两个版本的 VxVM 都提供基于 Java 的管理界面、条带化 (RAID 0)、连接、路径故障切换支持、卷在线调整大小以及任务监视器。完整版本执行基础产品中的所有功能，还支持负载均衡、热移动和取消移动、多达 32 个副本的镜像 (RAID 1)、镜像条带、条带镜像、RAID 5、在线迁移和在线重新布局。各版本的功能描述在《HP VERITAS 卷管理器发布说明》中。

在本章 VxVM 部分示例中使用的系统，在最初加载 11i 时，根磁盘设置由逻辑卷管理器 (LVM) 控制。将 HP Veritas 卷管理器作为应用程序加载后，我们可以在系统上的其他磁盘上执行存储管理。根磁盘将保持由 LVM 控制，而不会置于 VxVM 控制之下。

在接下来的章节中，我们将加载 HP Veritas 卷管理器并执行一些基本的存储管理任务，以便您对这款产品有初步的了解。这是一款功能丰富且拥有大量专用手册的产品，因此在本章的这一部分中，我们将介绍一些基础知识。有关 VxVM 手册的完整列表，请参见 docs.hp.com。其中包含有关配置和使用 VxVM 更多详细信息的手册包括《HP VERITAS 卷管理器发布说明》和《HP VERITAS 卷管理器管理员指南》。

#### HP VERITAS 卷管理器设置

从应用程序 CD-ROM 加载 HP Veritas 后，我们必须决定要用 VxVM 控制哪些磁盘。让我们运行 ioscan 来查看我们的 L-Class 系统上的磁盘：

```shell
# ioscan -funC disk
```

| 类别 | I | H/W 路径 | 驱动软件状态 | H/W 类型 | 描述 |
|---|---|---|---|---|---|
| disk | 0 | 0/0/1/2.0 | sdisk CLAIMED | DEVICE | SAMSUNG ST312203LC |
| /dev/disk/c2t0d0 | | /dev/rdisk/c2t0d0 | | | |
| disk | 1 | 0/0/2/0.0 | adisk CLAIMED | DEVICE | SAMSUNG ST312203LC |
| /dev/disk/c2t1d0 | | /dev/rdisk/c2t1d0 | | | |
| disk | 2 | 0/0/2/1.4.0 | sdisk CLAIMED | DEVICE | TOSHIBA CD-ROM XM-6201TA |
| /dev/disk/c3t0d0 | | /dev/rdisk/c3t0d0 | | | |

*注：应用了 OCR 表格修正：根据标准 HP-UX 命名约定和上下文“c<控制器><磁盘><磁盘>”，将 c2td0 修正为 c2t0d0/c2t1d0。原始 OCR 在路径 0/0/1/2.0 和 0/0/2/0.0 下均标记为“c2td0”，这是不正确的。标准 ioscan 输出使用 cXtYdZ 格式。*

此输出显示了两个内部磁盘和一个 CD-ROM 驱动器（我们将稍后添加另外两个磁盘来演示镜像和条带化设置）。由 LVM 控制的根磁盘是 c2t0d0。我们想用 VxVM 在磁盘 c2t1d0 上执行各种存储管理功能。如果该磁盘上有任何 LVM 头信息，必须在执行该磁盘上的任何 VxVM 功能之前将其移除。以下是用于创建和从 LVM 移除该磁盘的两个 LVM 相关命令：

```
# pvcreate -f /dev/rdisk/c2t1d0
物理卷 "/dev/rdisk/c2t1d0" 已成功创建。
# pvremove /dev/rdisk/c2t1d0
与 "/dev/rdisk/c2t1d0" 关联的物理卷已被移除。
#
```

您可能不需要发出 pvcreate 命令；然而，我发现发出这两个命令每次都能生效。此步骤在我之前提到的发布说明中有大纲说明。

接下来，我们运行 vxinstall 来执行 VxVM 的初始设置。在以下步骤中，我们运行 vxinstall 并选择快速安装，它将引导我们评估系统上的磁盘，并允许我们选择要置于 VxVM 控制下的磁盘：

```
# vxinstall

正在填充 VxVM DMP 设备目录 ....
正在生成连接的控制器列表....
卷管理器安装

菜单：VolumeManager/Install
```

卷管理器使用磁盘的控制器和磁盘编号为您系统中的磁盘命名，将它们替换为以下模式：

c<控制器><磁盘><磁盘>

注意：对于 VxVM 的动态多路径 (DMP) 功能，控制器编号代表具有多个访问路径的磁盘设备的多路径伪控制器编号。例如，如果一个磁盘从控制器 c0 和 c1 有 2 条路径，则卷管理器仅显示其中一个（例如 c0）来代表两个控制器。

一些示例如下：

```
c0t0d0- 第一个控制器，第一个目标，第一个磁盘
c1t0d0- 第二个控制器，第一个目标，第一个磁盘
c1t1d0- 第二个控制器，第二个目标，第一个磁盘
```

卷管理器已检测到您系统中的以下控制器：

c1:
c2:

按 RETURN 继续。

```
卷管理器安装
菜单：VolumeManager/Install
```

接下来，系统将询问您是希望使用快速安装还是自定义安装。自定义安装允许您选择卷管理器如何处理系统上连接的每个磁盘的安装。

快速安装会检查系统上连接的每个磁盘，并尝试创建卷以覆盖所有可能用于文件系统或类似目的的磁盘分区。

如果您不希望将某些磁盘用于卷管理器，或者您希望重新初始化某些磁盘，请使用自定义安装




否则，我们建议您使用快速安装选项。

按 RETURN 继续。

#### 卷管理器安装选项
菜单：VolumeManager/Install

- 1 快速安装
- 2 自定义安装
- ? 显示有关菜单的帮助
- ?? 显示有关菜单系统的帮助
- q 退出菜单

选择要执行的操作：1

#### 卷管理器快速安装
菜单：VolumeManager/Install/QuickInstall/c1

正在生成 c1 上连接的磁盘列表....
-排除 c1t2d0>
未在控制器 c1 上找到连接的磁盘！

按 RETURN 继续。

#### 卷管理器快速安装
菜单：VolumeManager/Install/QuickInstall/c2

正在生成 c2 上连接的磁盘列表....
卷管理器在控制器 c2 上检测到以下磁盘：
c2t2d0

按 RETURN 继续。

## 卷管理器针对控制器 c2 的快速安装

菜单：VolumeManager/Install/QuickInstall/c2

初始化此控制器上的所有磁盘？（将销毁这些磁盘上的数据）
[y,n,q,?] .默认：n) y

你确定吗？（将销毁这些磁盘上的数据）
[y,n,q,?] :默认：n) y

卷管理器现在将初始化此控制器上的所有磁盘

按 RETURN 继续。

#### 卷管理器快速安装
菜单：VolumeManager/Install/QuickInstall/c2/Init

是否为这些磁盘使用默认磁盘名称？[y,n,q,?]（默认：y）y

磁盘 c2t2d0 将被分配磁盘名称 disk01

按 RETURN 继续。

#### 卷管理器快速安装
菜单：VolumeManager/Install/QuickInstall

以下是您的选择摘要。
c2t2d0 新磁盘
这是否正确 [y,n,q,?]（默认：y）

卷管理器现在正在重新配置（分区阶段）...
卷管理器：正在将 c2t2d0 初始化为新磁盘。
卷管理器现在正在重新配置（初始化阶段）...
卷管理器：正在将 disk01 (c2t2d0) 添加为新磁盘。

卷守护程序已针对事务启用
正在启动重定位守护程序 vxrelocd。
#

请注意，**vxinstall** 发现了系统中唯一不受 LVM 控制的磁盘，并询问我们是否希望初始化该磁盘。由于我们只有一个潜在的磁盘可以置于 VxVM 控制之下，因此它是 **vxinstall** 找到的唯一磁盘。我们选择的*快速安装*而非*自定义安装*，替我们做出了一些决定，在此情况下，帮助我们快速配置了磁盘。

运行 **vxinstall** 后，我们可以查看已启动以支持 VxVM 的进程：

```
# ps -ef | grep vx
root        34     0  0 12:52:28 ?    0:01 vxfad
root     2978     0  0 12:58:59 ?    0:00 vxiod
root     4170  4156  0 13:07:35 ttyp4 0:00 vxnotify
root     4079     1  0 13:05:51 ?    0:00 vxconfigd -k -m enable
root     4165     1  0 13:07:35 ttyp4 0:00 /sbin/sh -
                     /usr/lib/vxvm/bin/vxrelocd root
root     4173  4165  0 13:07:35 ttyp4 0:00 vxnotify -f -w 15
root     4628  2900  1 13:16:12 ttyp4 0:00 grep vx
#
```

VxVM 的初始加载和设置快速且容易。如果您没有纸质文档，我建议从 *docs.hp.com* 获取文档，以便在需要作为设置的一部分参考时使用。如果没有*发行版说明*，我就不知道如何将第二个磁盘从 LVM 控制中释放出来，以便将其置于 VxVM 控制之下。

#### 卷管理器存储管理员

在 HP Veritas 卷管理器设置完成后，通过 **/opt/HPvmsa/bin/vmsa** 调用其图形界面，用于卷管理器存储管理员（在本节中我偶尔会称之为 vmsa）。图 9-17 显示了我们的 L-Class 系统的界面：

![](img/eff8b9287a5f38c5adf538f24aacf29e_544_0.png)

**图 9-17 卷管理器存储管理员**

图 9-17 展示了在此界面下，在我们的系统名称 13 下可以执行的许多管理区域。我们还可以对额外的系统、主机和集群执行存储管理，这些将显示在左侧窗口中，连同当前显示的系统 13。

现在让我们选择一些管理图标，看看我们的 L-Class 系统报告了什么内容。图 9-18 显示了系统上的控制器：

![](img/eff8b9287a5f38c5adf538f24aacf29e_545_0.png)

**图 9-18 *控制器***

图 9-18 显示了系统上的两个内部控制器 c1 和 c2。所有 L-Class 系统都有两个内部控制器，在我们的情况下，没有额外的控制器。如果我们愿意，也可以单独选择这些控制器以查看连接到它们的磁盘。

现在让我们查看系统中的*磁盘组*，如图 9-19 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_546_0.png)

**图 9.19 磁盘组**

图 9.19 显示了一个名为 rmtog 的磁盘组，它由一个 17 GByte 磁盘驱动器组成。这是我们之前设置的 VxVM 磁盘组。请注意，LVM 磁盘未显示，因为它不受 VxVM 控制。

接下来，我们将在图 9.20 中查看磁盘：

![](img/eff8b9287a5f38c5adf538f24aacf29e_547_0.png)

**图 9-20 磁盘**

图 9-20 显示了 L-Class 系统的两个内部磁盘。第一个由逻辑卷管理器（*root* 磁盘）使用，不受 Veritas 卷管理器控制。因此，与之关联的信息非常少，因为 VxVM 界面不*识别*任何 LVM 信息。第二个是 *rootdg* 中未使用的磁盘，名为 *disk01*。

图 9-21 显示了系统中正在使用的*文件系统*：

![](img/eff8b9287a5f38c5adf538f24aacf29e_548_0.png)

图 9-21 显示了许多正在使用的文件系统。请注意，除了其中一个文件系统外，所有这些都是 Veritas 文件系统，如 **vxfs** 所示。这有时是一个混淆点。有一个 Veritas 文件系统（*vxfs*）定义了文件系统类型，还有一个 Veritas 卷管理器，我们在本节中讨论它，它用于管理文件系统。您还可以使用 LVM 在 HP-UX 上管理 Veritas 文件系统。

我们知道 *rootdg* 中有一个磁盘目前未使用。让我们发出几个 **vx** 命令，并将其与我们在图形界面上看到的内容进行比较。本节末尾的表 9-1 描述了某些 **vx** 命令的使用。

首先，让我们使用 **vxdisk** 获取系统中的磁盘列表：

```
# vxdisk list
DEVICE        TYPE        DISK        GROUP       STATUS
c1t2d0        simple      -                   -           LVM
c2t2d0    simple    disk01    rootdg    online
#
```

**vxdisk** 的输出显示系统中有两个磁盘。第一个是根磁盘，受 LVM 控制，第二个是 *disk01*，受 VxVM 控制。

接下来，让我们使用 **vxprint -ht** 获取一些详细信息：

```
# vxprint -ht
Disk group: rootdg
  DM NAME    DEVICE  RLINK_CNT  MLOG  MINORS  GROUP-ID
  RV NAME     RVG     KSTATE    STATE   PRIMARY   DATAVOLS SRL
  V  NAME     RVG    KSTATE    STATE   REM HOST   REM DG   REM RLINK
  PL NAME     VOLUME  KSTATE    STATE   LENGTH   USRTYPE  PREFLEX RDOP
  SD NAME     PLEX    KSTATE    STATE   LENGTH   LAYOUT   NCOL/NRD MODE
  EV NAME     FLEX    DISK      DIEKSIZE LENGTH   [COL/]-OFF DEVICE MODE
  DG rootdg   FLEX    VOLUME    NVOLLLARS LENGTH   [COL/]OFF AM/BM   MODE
  dg rootdg   DEFAULT   DEFAULT   0      98930419   .1625.13
  dm disk01   c2t2d0   simple   1024     17782088
```

请注意，只有与 *rootdg* 相关的信息，即受 Veritas 卷管理器控制的部分，被生成。*dg* 是与*磁盘组*相关的信息，*dm* 是与*磁盘机制*相关的信息。在稍后的 **vxprint** 中，我们将添加 *-q* 选项以消除与此输出产生的大量标题信息。

接下来让我们使用 **vxdg** 命令查看 *rootdg* 中有哪些空闲空间：

```
# vxdg free
GROUP  DISK    DEVICE    TAG      OFFSET    LENGTH     FLAGS
rootdg  disk01  c2t2d0  c2t2d0  0         17782088  -
```

此输出显示目前我们几乎有整个 18 GBytes 的磁盘空间空闲。

现在我们可以回到图形界面，通过选择 *rootdg* 并输入与新卷相关的信息来创建可用的卷，如图 9-22 所示：




![](img/eff8b9287a5f38c5adf538f24aacf29e_550_0.png)

图 9-22 创建新卷

我们可以为这个卷设置的最大大小是由组成 `rootdg` 的未使用磁盘总大小决定的，即 17781760 字节。我们选择了约 1 GByte，因为没有 RAID 5，这样就不需要另一块磁盘。使用了 `vol01` 的默认名称。此外，从图 9-22 底部选择“添加文件系统...”（Add File System...）后，弹出了图 9-23 所示的窗口：

![](img/eff8b9287a5f38c5adf538f24aacf29e_551_0.png)

图 9-23 指定新卷的文件系统信息

在图 9-23 中，我们选择 `/dataspace` 作为挂载点名称，并选择 `vxfs` 作为文件系统类型。点击“确定”（OK）后，新卷即被创建，如图 9-24 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_552_0.png)

图 9-24 `vol01`

图 9-24 显示了挂载点为 `/dataspace` 的 `vol01`。我们可以使用带有一些实用选项的 `vxprint` 命令来查看卷信息，这包括我们刚刚创建的卷的信息。下面的 `vxprint` 命令展示了以下列表中的一些实用选项：

```bash
$ vxprint -ASteg
Disk group: rootdg

dg  rootdg  default default 0 969390349.1025.13
md  disk01-01  vol01-01  disk01 0 1000000 0 c2t2d0 ENA
$
```

此输出显示我们在 `c2t2d0` 上大约 1 GByte 的区域已就位。我们使用 `-q` 选项执行了这个 `vxprint` 命令，以消除之前示例中显示的头部信息。

这个简单的示例展示了使用 VxVM 添加卷的便捷性。在下一节中，我们将向系统添加两块磁盘并执行一些额外的设置。

### HP VERITAS 卷管理器镜像与条带化

既然我们已经介绍了 VxVM 的基础知识，让我们再进一步，向系统添加两块额外的磁盘并使用镜像和条带化技术。

首先，让我们再次使用 `vxdisk` 命令来查看我们添加到系统中的两块新磁盘：

```bash
# vxdisk list

DEVICE    TYPE    DISK      GROUP     STATUS
c2t0d0    simple  -       -         online invalid
c2t2d0    simple  -       -         LVM
c2t2d0g   simple  -       -         online invalid
c2t2d0    simple  disk01  rootdg    online
```

此时，磁盘已被列出，但尚未进行任何配置。这些磁盘已物理添加到系统中，在执行 `vxdisk` 之前没有发出其他额外命令。

现在让我们进入图形界面来配置这些磁盘。图 9-25 显示了总共四块磁盘，包括我们两块新的未配置磁盘：

![](img/eff8b9287a5f38c5adf538f24aacf29e_554_0.png)

图 9-25 `vmsa` 中的两块新磁盘

图 9-25 显示磁盘 `c1t0d0` 和 `c2t0d0` 已安装且处于 *未初始化* 状态。现在让我们使用图 9-26 所示的图形界面，将这两块磁盘添加到名为 *test* 的新磁盘组中，首先操作其中一块磁盘：

![](img/eff8b9287a5f38c5adf538f24aacf29e_555_0.png)

图 9-26 将新磁盘添加到组 `test`

我们通过 *Add Disk(s)* 窗口在图形界面上将两块磁盘都添加到 *test* 中。结果如图 9-27 所示的屏幕，其中两块新磁盘 *test01* 和 *test02* 均属于 *test*。

![](img/eff8b9287a5f38c5adf538f24aacf29e_556_0.png)

我们可以使用 `vxdisk` 命令确认 *test* 中的磁盘，如下所示：

```bash
# vxdisk list
DEVICE    TYPE      DISK     GROUP     STATUS
c1t0d0    simple    test01   test      online
c1t2d0    simple    -        -         LVM
c2t0d0    simple    test02   test      online
c2t2d0    simple    disk01   rootdg    online
#
```

现在磁盘显示为已配置，名称分别为 *test01* 和 *test02*，且两者都处于 *在线* 状态。这两块磁盘都属于 *Group test*。

接下来，让我们在新的 *磁盘组 test* 中创建一个条带化且镜像的卷。在 *vmsa* 窗口中从项目列表选择 *New*，将弹出图 9-28 所示的对话框。

![](img/eff8b9287a5f38c5adf538f24aacf29e_557_0.png)

图 9-28 创建条带化且镜像的新卷

从图 9-28 中，您可以看到为 *vol02* 指定的所有特性。它的大小约为 5 GBytes，采用条带化，并且有一个镜像副本。它的文件系统类型为 *vfs*，挂载点为 */protected*。

添加此卷后，它将出现在 *vxlist* 窗口中，如图 9-29 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_558_0.png)

图 9-29 卷 *vol02*

我们可以转到命令行，使用不带任何选项的 *vxprint* 来确认 *vol02* 的存在，如下所示：

```bash
$ vxprint
Disk group: rootdg

TY NAME       ASSOC        KSTATE   LENGTH     PLOFFS STATE       TU/TUOLD
-dg rootdg     -            -        -          -      -            -
-dm disk01     c2t2d0     -        17782088   -      -            -
v vol01        fsgen      ENABLED  1000000    -      ACTIVE       -
pl vol01-01    vol01      ENABLED  1000000    -      ACTIVE       -
-md disk01-01  vol01-01   ENABLED  1000000    0       -            -

Disk group: test

TY NAME       ASSOC        KSTATE   LENGTH     PLOFFS STATE       TU/TUOLD
-dg test       test       -        -          -      -            -
-dm test01     c1t0d0     -        17782088   -      -            -
-dm test02     c2t0d0     -        17782088   -      -            -
v vol02        fsgen      ENABLED  5000000    -      ACTIVE       -
pl vol02-03    vol02      ENABLED  5000064    -      ACTIVE       -
sv vol02-801   vol02-03   ENABLED  2500032    0       -            -
```

```
ev vo102-502 		vo102-03 		ENABLED 		2500032 		0 		-		-

v vo102-L01 		fsgen		ENABLED 		2500032 		-		ACTIVE 		-
pl vo102-P01 		vo102-L01		ENABLED 		LOGONLY 		-		ACTIVE 		-
ed test01-03 		vo102-P01 		ENABLED 		33 		LOG 		-		-
pl vo102-P02 		vo102-L01		ENABLED 		2500032 		-		ACTIVE 		-
ed test01-04 		vo102-P02 		ENABLED 		2500032 		0 		-		-

v vo102-L02 		fsgen		ENABLED 		2500032 		-		ACTIVE 		-
pl vo102-P03 		vo102-L02		ENABLED 		2500032 		-		ACTIVE 		-
ed test02-05 		vo102-P03 		ENABLED 		33 		LOG 		-		-
pl vo102-P04 		vo102-L02		ENABLED 		2500032 		-		ACTIVE 		-
ed test02-02 		vo102-P04 		ENABLED 		2500032 		0 		-		-
&
```

此输出显示我们的 5 GByte 卷已配置为镜像。

此外，我们想使用 `df -k` 查看 /protected 作为已挂载的文件系统：

```bash
# df -k

Filesystem          kbytes     used    avail  %used Mounted on
/dev/vg00/lvol13    204800   55509  140002     28% /
/dev/vg00/lvol11   199361   45526  152916     26% /stand
/dev/vg00/lvol18    921600  387319  827033     45% /var
/dev/vg00/lvol17   937984  793162  135806     85% /
/dev/vg00/lvol14    204800    1529  190628      1% /tmp
/dev/vg00/lvol16   835584  722803  105775     87% /opt
/dev/vg00/lvol15    204800    1162  190917      1% /home
/dev/vx/dsk/rootdg/vol01
                      1000000   1349  936243     0% /dataspace
/dev/vx/dsk/test/vol02
                      5000000  2693  4695038    0% /protected
#
```

我们的新卷 `vol02` 已创建，大小为 5 GBytes，挂载点为 /protected。

前面的示例涵盖了使用 VxVM 的几个基础知识。这绝不是对 VxVM 的详尽覆盖，但希望它能作为一个良好的介绍。有关 VxVM 的详细信息，请参阅相关手册。

虽然在本节中我们主要关注 `vmsa`，但有许多您可以运行的 `vx` 命令，它们执行与图形界面相同的功能。我有时喜欢发出命令来查看我在图形界面中执行的卷相关操作，以确认结果。表 9-1 列出了最常用的 `vx` 命令及其功能。

### 表 9-1 VxVM 命令

| 命令 | 描述 |
| :---- | :---- |
| vxsasst | 创建和更改卷。 |
| vxctl | 管理 `vxconfigd` 守护进程。 |
| vxdg | 执行与磁盘组相关的任务。 |
| vxdisk | 执行与磁盘相关的任务。 |
| vxdiskadd | 用于添加磁盘。 |
| vxedit | 更改 VxVM 对象。 |
| vxmake | 创建 VxVM 对象。 |
| vxmend | 纠正配置问题。 |
| vxplex | 执行 plex 相关的任务。 |
| vxprint | 打印配置信息。 |
| vxsd | 在子磁盘上执行任务。 |
| vxstat | 打印卷统计信息。 |
| vxtrace | 跟踪卷任务。 |
| vxunrelocate | 移动已重新定位的子磁盘。 |
| vxvol | 执行卷任务。 |

这些命令在 HP 文档集中有所介绍，也有 man 页面提供这些命令的详细使用信息。




#### 其他文件系统相关命令

##### 使用 bdf 查看文件系统

您可以使用 `bdf` 命令手动查看已挂载的文件系统。`bdf` 提供以下输出：

| 列 | 描述 |
| :--- | :--- |
| **File system** | 块设备文件系统名称。在下述示例中，显示了多个逻辑卷。 |
| **KBytes** | 文件系统的总磁盘空间（以 KB 为单位）。 |
| **used** | 文件系统已使用的 KB 数量。 |
| **avail** | 文件系统可用的 KB 数量。 |
| **%used** | 文件系统中已使用的总可用磁盘空间的百分比。 |
| **Mounted on** | 挂载文件系统所在的目录名称。 |
| **iused** | 正在使用的 inode 数量（仅当使用 `bdf` 的 `-i` 选项时）。 |
| **ifree** | 空闲的 inode 数量（仅当使用 `bdf` 的 `-i` 选项时）。 |
| **%use** | 正在使用的 inode 的百分比（仅当使用 `bdf` 的 `-i` 选项时）。 |

以下是 `bdf` 的一个示例，这也包含在本章前面提到的“逻辑卷管理器背景”部分中：

```bash
$ /usr/bin/df
```

| 文件系统 | kbytes | 已用 | 可用 | %已用 | 挂载点 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/vg00/lvol3 | 47829 | 18428 | 24618 | 43% | / |
| /dev/vg00/lvol1 | 67733 | 24736 | 36223 | 41% | /stand |
| /dev/vg00/lvol8 | 34541 | 8673 | 22413 | 28% | /var |
| /dev/vg00/lvol7 | 299157 | 149449 | 119792 | 56% | /usr |
| /dev/vg00/lvol4 | 23013 | 48 | 20663 | 0% | /tmp |
| /dev/vg00/lvol6 | 99669 | 32514 | 57188 | 36% | /opt |
| /dev/vg00/lvol5 | 19861 | 9 | 17865 | 0% | /home |
| /dev/dsk/c0t6d0 | 802212 | 552120 | 169870 | 76% | /mnt/9.9 |

##### 使用 fsck 进行文件系统维护

**fsck** 是用于 HP-UX 系统文件系统维护的程序。**fsck** 检查文件系统一致性，并可以对损坏的文件系统进行许多“救命”的修复。**fsck** 可以带多个选项运行，包括以下选项：

-   `-F`
    此选项允许您指定文件系统类型。务必指定文件系统类型。在某些 UNIX 变体中，将使用 `/etc/fstab` 来确定文件系统类型；在其他变体中则不会。请参阅本节后面关于 `fstab` 的描述。

-   `-m`
    这是对文件系统的健全性检查。如果运行此选项，系统将告知您的文件系统是否正常。我执行了以下操作来检查挂载为 `/home` 的 `lvol5`：

```bash
$ unmount /home
$ fsck -m /dev/vg00/lvol5
vxfs fsck: sanity check: /dev/vg00/lvol5 OK
```

如果在交互模式下（这是默认模式）运行，`fsck` 会提问。使用 `-y` 选项会使 `fsck` 提出的所有问题的回答均为“是”。不要这样做！如果您的文件系统存在严重问题，可能必须删除数据，而 `-y` 表示对包括删除数据在内的所有问题的回答都是“是”。

对 `fsck` 提出的所有问题的回答均为“否”。这也请不要使用。如果您的文件系统状态不佳，您可能必须对某些问题回答“是”才能修复文件系统。所有“否”的回答无法完成修复工作。

由于您的系统会对那些在关机时未标记为干净状态的文件系统运行 `fsck`，因此您可以放心，当系统启动时，任何未正常关机的磁盘都会被检查。定期以交互方式运行 `fsck` 是个好主意，这样您可以亲眼看到所有文件系统是否都处于良好的工作状态。

如果 `fsck` 发现目录或文件有问题，它会将其放置在 `lost+found` 目录中，该目录位于每个文件系统的顶层。如果文件或目录出现在 `lost+found` 中，您可以通过检查该文件或目录来识别它，并将其移回原始位置。您可以使用 `file`、`what` 和 `strings` 命令获取有关文件的更多信息，以帮助识别其来源。

文件系统问题是如何产生的？文件系统问题最常见的原因是系统未正常关机。写入文件系统的信息首先被写入内存中的缓冲区缓存。随后，通过卸载磁盘或使用 `sync` 命令，或者通过正常填满缓冲区并写入磁盘的操作，这些数据会被写入磁盘。如果您走到一台系统前直接切断电源，您肯定会导致文件系统问题。未同步到磁盘的缓冲区中的数据将丢失，文件系统不会被标记为正常关机，系统启动时会运行 `fsck`。突然断电也可能导致系统未正常关机。

系统的正常关机过程通过 **shutdown** 命令描述。尽管 **fsck** 是一个非常有用的实用程序，偶尔还能创造奇迹，但您不希望给文件系统带来任何不必要的风险。因此，请务必正常关机。

前文提到的 `/etc/fstab` 文件被 **fsck** 用于确定在启动时是否需要检查文件系统及其检查顺序。如果某些条目不存在“通过编号”（pass number），则 `/etc/fstab` 中条目的顺序很重要。以下是 `/etc/fstab` 文件的一个示例：

```text
# System /etc/fstab file. Static information about the file
# systems. See fstab(4) and sam(1m) for further details.

/dev/vg00/lvol3 / vxfs delaylog 0 1
/dev/vg00/lvol1 /stand hfs defaults 0 1
/dev/vg00/lvol4 /tmp vxfs delaylog 0 2
/dev/vg00/lvol6 /opt vxfs delaylog 0 2
/dev/vg00/lvol5 /home vxfs delaylog 0 2
/dev/vg00/lvol7 /usr vxfs delaylog 0 2
/dev/vg00/lvol8 /var vxfs delaylog 0 2
/dev/dsk/c0t6d0 /tmp/mnt9.x hfs rw, suid 0 2
```

| 设备特殊文件 | 目录 | 类型 | 选项 | 备份频率 | 通过编号 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| | | | | | |

**device special file**
这是设备块文件，例如示例中的 `/dev/vg00/lvol1`。

**directory**
挂载该设备特殊文件所在的目录名称。

**type**
可以是多种类型之一，包括：

-   `cdfs`（本地 CD-ROM 文件系统）
-   `hfs`（高性能本地文件系统）
-   `nfs`（网络文件系统）
-   `vxfs`（日志文件系统）
-   `swap` 或 `swapfs`

**options**
有多个可用选项，包括示例中显示的那些。`rw` 是读写；`ro` 是只读。

**backup frequency**
供未来的备份实用程序使用。

**pass #**
由 **fsck** 使用，用于确定文件系统检查（fsck）执行的顺序。

**comment**
任何内容都可以，只要前面有 `#` 号。

##### 使用 mediainit 初始化

这是一个您可能不会使用，但应该了解的命令：**mediainit**。当您使用 SAM 设置磁盘时，可能会运行 **mediainit** 命令来初始化新介质。

以下是 **mediainit** 的一些选项：

-   `-v`
    这是详细模式选项。**mediainit** 通常只是将错误消息打印到屏幕上。使用 `-v` 选项可以获取 **mediainit** 所做操作的连续反馈。

-   `-i` `interleave`
    这允许您指定交织因子，即顺序逻辑记录与物理记录之间的关系。如果未指定，**mediainit** 将提供此值。

-   `-f` `format`
    格式选项允许您为支持不同格式选项的设备（如软盘）指定格式选项。这对硬盘不是必需的。

-   `pathname`
    这是用于 **mediainit** 的字符设备文件。

在前面的一些示例中使用的 **newfs** 用于创建新文件系统。**newfs** 调用前文介绍的 **mkfs** 命令。**newfs** 构建您指定类型的文件系统（这是使用 *-F* 选项的命令之一，因此您可以指定文件系统类型）。

## 第 10 章

## Ignite-UX

## Ignite-UX 用于虚拟分区的可启动恢复档案

使用 Ignite-UX，您可以轻松为所有虚拟分区创建可启动的恢复档案。您可以从 Ignite-UX 服务器或客户端启动创建虚拟分区镜像的过程，该镜像存储在服务器上。如果虚拟分区发生故障，您可以从存储在服务器上的镜像启动客户端，并恢复您的 vPar。与不使用 vPar 的情况相比，使用 vPar 时您需要管理更多的 HP-UX 镜像。例如，在没有 vPar 的情况下运行的 N-Class 系统只有一个 HP-UX 实例，但使用 vPar 时，您可能有四个 HP-UX 实例，每个实例有两个 CPU 需要管理。由于需要管理更多的 HP-UX 镜像，您可能会面临许多额外的系统管理相关挑战；然而，Ignite-UX 将使创建可启动恢复档案变得轻松。

在本章关于虚拟分特的部分中，我们将重点介绍如何使用 Ignite-UX 服务器上的图形用户界面（GUI）创建可启动恢复档案。我们将详细介绍创建可启动恢复档案的过程，并查看后台发生的一些活动。然后，我们将包含一个由 HP 实验室工程师开发的逐步使用 Ignite-UX 和 vPars 的程序。在





在本章中非 vPars 特定的部分，将涵盖大量 Ignite-UX 的背景知识和示例。

请记住，Ignite-UX 用于创建可引导恢复归档时，需结合常规备份使用，以保护您的所有数据。有关备份的信息，请参阅第 7 章。

### 为 vPars 创建可引导恢复归档

在本节中，我们将使用 Ignite-UX 图形用户界面（GUI）为虚拟分区创建可引导恢复归档。此外，我们还将探讨后台发生的一些情况，例如：

- 可引导恢复归档在服务器上占用的磁盘空间。
- 为支持创建客户机归档而创建和修改的服务器文件（`/etc/exports` 及其他）。
- 服务器在客户机上发出的用于生成归档的命令。
- 在下一节中，我们将通过从在服务器上创建的归档引导来恢复客户机（请注意，可重定位内核与标准内核不同。）

### 使用 Ignite-UX GUI 创建 vPar 归档

在 Ignite-UX 工具加载到服务器后，需要进行一些初始的客户机设置，并通过 Ignite-UX 图形用户界面（GUI）进行管理。此外，还会对服务器进行一些修改。其中一项更改是在 `/etc/exports` 中为要管理的客户机添加条目。Ignite-UX 自动为已设置的客户机在 `/etc/exports` 中包含了条目。以下 `/etc/exports` 列表显示了服务器 `chess2` 上两个客户机的条目：

```
root@chess2 > cat /etc/exports
/var/opt/ignite/clients -anon=2
/var/opt/ignite/recovery/archives/actappd1 -anon=2,access=actappd1
/var/opt/ignite/recovery/archives/ecvpard2 -anon=2,access=ecvpard2
root@chess2 >
```

这三个条目包括 Ignite-UX 服务器使用的一般 `clients` 目录，以及在 Ignite-UX 服务器上设置的两个客户机 `actappd1` 和 `ecvpard2` 的 `archives` 目录。这两个主机是运行在同一服务器上的虚拟分区。`chess2` 是 Ignite-UX 服务器，与运行这两个 vPars 的服务器不同。

除了指定客户机时自动进行的 `/etc/exports` 更新外，您可能希望在服务器和客户机上的 `/rhosts` 中手动创建条目，这样在您发起创建可引导恢复归档时，就不需要在服务器上响应客户机密码。服务器在客户机上远程运行程序，为了在不发出密码的情况下执行此操作，`/rhosts` 文件必须包含适当的条目。但是，请记住，在 `/rhosts` 中包含条目会降低系统的整体安全级别。

完成这些设置后，您可以按照图 10-1 所示在我们的服务器 `chess2` 上启动创建可引导恢复归档的过程：

![](img/eff8b9287a5f38c5adf538f24aacf29e_571_0.png)

图 10-1 指定将生成可引导恢复归档的客户机

Ignite-UX GUI 中显示的两个客户机即我们在 `/etc/exports` 中看到条目的客户机。请记住，Ignite-UX GUI 中显示的两个系统是运行在同一服务器上的两个虚拟分区。

选定客户机后，我们可以从几个 *操作* 中进行选择，如图 10-2 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_572_0.png)

图 10-2 选定客户机后的操作菜单

选中 `actappd1` 后，我们将从操作菜单中选择“创建网络恢复归档”。

选择此菜单项后，会弹出一个窗口，其中包含创建归档的一系列默认设置，如图 10-3 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_573_0.png)

图 10-3 创建可引导恢复归档的默认设置

在这些基本屏幕推进之后，Ignite-UX 开始创建归档的过程。

服务器在客户机上发出了 `make_net_recovery` 命令以创建归档。以下是客户机（`actappd1`）上仅针对该命令的 `ps -ef` 输出，该客户机正在生成归档：

```
root@actappd1 > ps -ef | grep make
/opt/ignite/bin/make_net_recovery -i -b -P s -l 0x00306E0981D4
root@actappd1 >
```

此命令现在正在我们的客户机（这是一个虚拟分区）后台运行，并将归档通过网络写入服务器。在我们的客户机上，此过程大约需要三个小时，并生成大小超过 600 MB 的文件。

如果您对 **make_net_recovery** 的许多选项感兴趣，可以查看该命令的在线手册页。在此示例中，`i` 表示*交互式*，`b` 表示*后台*，`-P` 表示*部分*，`s` 表示*服务器*，`-l` 表示客户的机*网卡 ID*。您可以从客户机或服务器发出此命令。一些系统管理员更喜欢从服务器集中管理归档的创建，而另一些人则更喜欢在客户机上创建 cron 条目并从客户机启动此过程。手册页中出现了 **make_net_recovery** 命令的设置和语法（截至本文撰写时，**make_net_recovery** 是最新的命令。）

启动客户机恢复归档创建过程后，会创建许多文件。以下列表显示了一些更有趣的目录和文件。**make_net_recovery** 的手册页提供了为客户端创建的所有重要目录和文件的解释。让我们看一下本章示例中使用的 Ignite-UX 服务器上一些更有趣的文件。

以下是服务器上 `/var/opt/ignite/clients` 目录的长列表：

```
root@chess2[/var/opt/ignite/clients] > ll
total 4
drwxrwxwx    3 bin         bin          1024 Jul 20 12:23 0x001083f7c4fc
drwxr-x-x    3 bin         bin          1024 Jul 19 17:54 0x0019809891d4
drwxr-xr-x    2 root        sys           96 Jul 19 14:13 161.220.212.121
drwxr-xr-x    1 bin         bin          14 Jul 27 14:01 actappd1 -> 0x0010e80981d4
drwxr-xr-x    1 bin         bin          14 Jul 20 09:53 actparad2 -> 0x001083f7c4fc
lrwxrwxrwx    1 root        sys           14 May 25 15:53 sample -> 0x99999999999999
```

请注意，此目录中有我们两个客户机的条目。有一个链接允许您指定客户机名称而不是网卡 ID，因为客户机名称更容易记住和输入。

接下来，让我们切换到正在为其创建归档的客户机目录，并执行长列表：

```
root@chess2[/var/opt/ignite/clients] > cd actappd1
root@chess2[/var/opt/ignite/clients/actappd1] > ll
total 18
-rw-r--r--    1 bin         bin           967 Jul 24 18:33 CDINDEX
-rw-r--r--    1 bin         bin             9 Jul 19 15:15 client_name
-rw-r--r--    1 bin         bin            28 Jul 19 15:15 client_status
-rw-r--r--    1 bin         bin           300 Jul 19 15:15 config.5wg
-rw-r--r--    1 bin         bin           330 Jul 19 15:15 node_info
-rw-r--r--    1 bin         bin           940 Jul 19 15:15 bw.info
-rw-r--r--    1 bin         bin           231 Jul 19 15:15 install.log
-rw-r--r--    1 bin         bin             0 Jul 19 15:20 lockfile
drwxr-xr-x    3 bin         bin          1024 Jul 27 14:01 recovery
-rw-r--r--    1 bin         bin           585 Jul 27 13:39 server.state
```

此目录中有很多与客户机相关的信息。`recovery` 目录包含与我们的客户机最相关的文件，因此让我们切换到该目录并执行长列表：

```
root@chess2(/var/opt/ignite/clients/actappd1) > cd recovery
root@chess2(/var/opt/ignite/clients/actappd1/recovery) > ll
total 8
drwxr-xr-x 2 bin bin 1024 Jul 27 14:05 2001-07-27,13:55
-rw-r--r-- 1 bin bin  252 Jul 27 14:03 archive_content
-rw-r--r-- 1 bin bin  247 Jul 27 14:05 client_status
-rw-r--r-- 1 bin bin  411 Jul 27 14:03 default.log
lrwxr-xr-x 1 bin bin   16 Jul 27 14:01 latest -> 2001-07-27,13:55
```

`archive_content` 文件包含要包含或排除的文件和目录。`client_status` 用于与客户机通信，以提供 `make_net_recovery` 命令的状态。在启动归档创建后，GUI 中会显示一个状态窗口。`latest` 是指向包含最新恢复文件的目录的链接。如果我们切换到该目录并执行长列表，我们将看到以下列表中的文件：

```
root@chess2(/var/opt/ignite/clients/actappd1/recovery) > cd 2001-07-27,13:55
root@chess2(/var/opt/ignite/clients/actappd1/recovery/2001-07-27,13:55) > ll
total 3704
-rw-r--r-- 1 bin bin   3089 Jul 27 14:05 archive.cfg
-rw-r--r-- 1 bin bin    252 Jul 27 14:03 archive_content
-rw-r--r-- 1 bin bin    259 Jul 27 14:03 control.cfg
-rw-r--r-- 1 bin bin 1880616 Jul 27 14:05 filist
-rw-r--r-- 1 bin bin   2510 Jul 27 14:05 recovery.log
-rw-r--r-- 1 root sys  5548 Jul 27 13:58 system.cfg
```

`recovery.log` 文件包含有关我们当前正在创建的归档的信息。以下输出包含该文件的内容：




### 虚拟分区恢复

每个客户端都会生成许多有用的文件；然而，我们最感兴趣的是恢复归档文件。以下列表显示了我们为客户生成的三个归档文件。

```
root@chesus2:/var/opt/ignite/recovery/archives/actapi31: # ls -l
total 1432116
-rw------- 1 bin bin 621280688 Jul 26 20:26 actapi31.vpar
-rw------- 1 bin bin 36192098 Jul 26 20:26 actapi31.vpar
-rw------- 1 bin bin 71928000 Jul 26 20:26 actapi31.vpar
root@chesus2:/var/opt/ignite/recovery/archives/actapi31:
```

第一个是在较早日期创建的完整归档文件，第二个是一个部分归档文件，由于被中止而未完成，第三个是在生成此列表时我们正在创建的归档文件。

这表明我们的虚拟分区消耗的磁盘空间超过 600 MBytes 以用于完整归档。您需要考虑希望在服务器上存储多少客户端的可启动恢复归档文件，并相应地规划您的卷空间。对于我们正在生成的归档文件，目前已有约 73 MBytes 的数据，而最终将是一个超过 600 MByte 的恢复归档文件，我们已在客户端上运行 **make_net_recovery** 大约 20 分钟。

一旦我们的归档文件完全创建，我们就可以将其作为测试进行启动。我通常在虚拟分区生成后立即创建一个归档文件，并在对 vPar 进行大量自定义之前对其进行测试。这将让您放心，知道从恢复归档启动的过程。

![](img/eff8b9287a5f38c5adf538f24aacf29e_577_0.png)

既然我们已经为虚拟分区创建了可启动的恢复归档，我们就可以使用它来恢复我们的 vPar。您可以使用 **vparboot** 命令从一个 vPar 恢复另一个 vPar。这意味着，当其中一个 vPar 正在运行时，您可以使用以下 **vparboot** 命令在同一系统上恢复另一个 vPar：

![](img/eff8b9287a5f38c5adf538f24aacf29e_577_1.png)

```
vparboot -p vp_name -I ignite_kernel
```

这与在第 2 章中我们使用位于同一系统上的内核（而非 Ignite-UX 服务器上的内核）启动 vPar 时使用的 **vparboot** 形式不同。那种形式的 **vparboot** 如下所示：

```
vparboot -p vpar_name [ -b kernel_path ] [ -o boot_opts [ -f boot_addr] ]
```

在前面的章节示例中，我们只需指定我们要启动的虚拟分区的名称，例如 **vparboot -p cable1**。使用这种形式的 **vparboot**，我们通过 *-b* 选项指定本地系统上的启动内核。**vparboot** 和其他 vPar 命令的手页可以在附录 A 中找到。

通常，您会从 PDC 提示符启动恢复归档，也就是说，您的系统已停止并且您正在恢复它。由于我们的系统上有多个 vPar，我们可以使用 **vparboot** 从同一系统上正在运行的 vPar 恢复该系统上的另一个 vPar。

我们将在正在运行的 vPar 中发出以下 **vparboot** 命令，以通过命令行从 Ignite-UX 服务器恢复 vPar *actappd1*：

```
# vparboot -p actappd1 -I 161.228.212.110,/opt/ignite/boot/WINSTALL
```

指定了我们的 Ignite-UX 服务器的 IP 地址。在此 **vparboot** 命令中使用的 **WINSTALL** 文件与用于常规 HP-UX 恢复（没有 vPars）的文件不同。vPars 需要可重定位内核，因此 **vparboot** 命令中使用的 **WINSTALL** 是 vPars 所需的那个。该 **WINSTALL** 随 vPars 提供。

使用 **vparboot** 从正在运行的 vPar 恢复虚拟分区的能力意味着受影响的更少。正在运行的 vPar 中的用户不会受到正在另一个 vPar 上进行的恢复的影响。在根卷组（*vg00*）的恢复完成后，您可以从最新的备份恢复 vPar 上的其余信息。请确保经常创建可启动的恢复归档，以便您的整个根卷组可以使用最新的数据进行恢复。

![](img/eff8b9287a5f38c5adf538f24aacf29e_578_0.png)

## 使用 Ignite-UX 安装虚拟分区

本节包含设置 Ignite-UX 服务器以安装 vPars 的分步程序。该程序由 HP 实验室工程师 Geoff Blaha 提供。由于您将在 vPars 环境中安装许多 HP-UX 11i 和 vPars 软件实例，该程序可以为您节省大量时间。

在前面的章节示例中，我们只需指定我们要启动的虚拟分区的名称，例如 **vparboot -p cable1**。使用这种形式的 **vparboot**，我们通过 *-b* 选项指定本地系统上的启动内核。**vparboot** 和其他 vPar 命令的手页可以在附录 A 中找到。

### Ignite-UX 和 vPars 实用指南

![](img/eff8b9287a5f38c5adf538f24aacf29e_579_0.png)

使用 **vparboot** 命令从虚拟分区安装 HP-UX 和 vPar 软件到目标 vPar。Ignite-UX 服务器用作此安装过程的源仓库。

以下是整体的 vPars 安装过程（假设正在安装新服务器）

- 安装服务器和外围设备
- 安装 vPars 所需的补丁（即，Gold Quality Pack 等）
- 安装 HP-UX 11i（独立安装）
- 安装 vPars 软件。
- 规划所需的 vPars。

![](img/eff8b9287a5f38c5adf538f24aacf29e_579_1.png)

- 使用 **vparcreate** 命令创建 vPars：这将创建 vPars 数据库*/stand/vpdb*。
- 关闭 HP-UX 并将服务器置于 BCH（Boot Console Handler）模式。
- 从 HP-UX/vPars 磁盘启动，并在 ISL 提示符处停止（交互）。
- 加载并运行 vPars 监视器。
- 使用 **vparload** 命令启动第一个 vPar（之前安装的）。
- 使用 **vparboot** 命令安装 HP-UX 和 vPars 软件到所有剩余的 vPars。使用 *Ctrl/A* 命令切换虚拟控制台




在 vPars 和监控器之间。

Ignite-UX 服务器用作 **vparboot** 安装过程的源库。如果尚未存在用于此过程的 Ignite-UX 服务器，请安装并配置一台，最好是在另一台系统上，从以下步骤 1 到 3 开始。如果已经存在 Ignite-UX 服务器，或者其版本早于 B.3.4.115，则需要更新。如果你的 Ignite-UX 服务器已经是 B.3.4.115 版本，请继续执行下面的步骤 4。

## 1) 获取 Ignite-UX 软件。

来源包括 CDROM、*software.hp.com* 和 SD-UX 库文件。

注意：vPars 首个发行版支持的 Ignite-UX 版本为 **B.3.4.115：**

```
= what /opt/ignite/bin/ignite
/opt/ignite/bin/ignite:
ignite user interface $Revision: 10.643 $
Ignite-UX Revision B.3.4.115
install/h $Revision: 10.102 $
```

可以在 2001 年 9 月的应用程序分发中找到此版本。虽然旧版本的 Ignite-UX 可能可以工作，但它们不被支持用于 vPars，并且在使用基于 Ignite-UX B.3.4.115 版本库构建的可重定位 **WINSTALL** 文件时可能会遇到问题。

## 2) 安装或更新 Ignite-UX 软件。

使用 *swinstall* 安装 Ignite-UX。

## 3) 更新 *PATH*。

将以下搜索路径添加到你的登录脚本中：

```bash
export PATH=${PATH}:/opt/ignite/bin
```

如果已经存在 Ignite-UX 服务器（版本 B.3.4.115），请将 HP-UX 11i 服务器 OE 和 vPars 软件添加到 Ignite-UX 服务器中（注意，在 Ignite-UX 服务器上安装和配置软件有多种方法；下面描述的是其中一种方法）：

## 4) 在 Ignite-UX 中设置要安装到目标 vPars 的软件：

- 从 2001 年 9 月的介质创建 HP-UX 11i OE 库（使用 CDROM 设备 `c0t3d0` 的示例）：

```
make_depots -r B.11.11 -s /dev/dsk/c0t3d0
```

- 创建 vPars 应用程序库，以便它在安装期间的 `tool` 的 `Software` 选项卡中显示（使用 tar 格式的库文件，以及另一个使用 Ignite-UX 服务器的示例）：

```
make_depots -r B.11.11 -a 800 -s /tmp/vpar_iC9.tar
```

或者

```
make_depots -r B.11.11 -a 800 -s flatecat.cup.hp.com:/opt/VPAR/ic9/depot
```

> 注意：上述假设 vPars 源作为 tar（库）文件或另一个 Ignite-UX 库位于 `flatcat` 计算机上。CDROM 源也可以工作。上述示例命令将在 `"apps_800"` *库* 中创建并复制 vPars。

- 为上述库（11i OEs 和 vPars）创建 Ignite-UX 配置文件：

```
make_config -r B.11.11
```

上述命令创建 `/var/opt/ignite/data/Rel_B.11.11/apps_800.cfg` 配置文件。

- 管理应用程序的 Ignite-UX 索引文件：

```
# manage_index -a -f /var/opt/ignite/data/Rel_B.11.11/apps_800_cfg
```

- 从 2001 年 9 月的介质创建 HP-UX 11i OE 库：

完成上述步骤后，将用于 vPars 的可重定位 **WINSTALL** 文件复制到 Ignite-UX 引导目录：

```
# cd /opt/ignite/boot
# cp WINSTALL WINSTALL_NoReloc
# cp <source_path>/WINSTALL . (可能还需要执行 chmod 和 chown。)
```

注意，上面的 <source_path> 指的是任何存在 **WINSTALL** 的源。

目前，使用 Ignite-UX 内捆绑的 **WINSTALL** 无法用于 vPars，因为它不是可重定位的。以下命令用于验证是否正在使用正确的 **WINSTALL**：

```
# /usr/ccs/bin/elfdump -r /opt/ignite/boot/WINSTALL | fgrep -i relocation
```

如果上述命令没有输出，则 **WINSTALL** 不是可重定位的。

## 5) 启动 Ignite-UX 服务器管理器：

```
# /opt/ignite/bin/ignite
```

## 6) 完成 Ignite-UX 服务器配置

- 选择：*Options -> Server Configuration...*
- 选择 *Server Options* 选项卡
- 默认配置：*HP-UX B.11.11 Default.*
- 客户端超时：40
- 在 `server` 上运行客户端安装 UI

选择：`Options -> Server Configurations... -> Session Options`

- 验证只设置了以下选项：
  - `Confirm new clients`
  - `Show the welcome screen for the install server`
  - 确保未选中 `Hall the client after installation` 选项。

![](img/eff8b9287a5f38c5adf538f24aacf29e_583_0.png)

一旦 Ignite-UX 服务器安装并配置好以安装 HP-UX OEs 和 vPars，就可以继续使用 `vparsboot` 按需安装所有剩余的 vPars。

有关 Ignite-UX 的更多信息可以在 `Ignite-UX Administration Guide` 中找到。

正如我在本章开头提到的，当你使用 vPars 时，你将拥有更多需要管理的 HP-UX 11i 实例。从 Ignite-UX 服务器安装这些 vPars 将为你节省大量时间，并确保你的安装具有软件的一致性基础。

### 章节非-vPar 特定部分：Ignite-UX 概述

Ignite-UX 是一款功能非常强大的产品。它与许多功能相关联，要全面覆盖这些功能需要一整本书。这个背景部分是根据旧版本的 Ignite-UX 编写的，不包含任何与 vPar 相关的信息。然而，对于从未使用过 Ignite-UX 的人来说，它是一个很好的概览。我将重点介绍我认为 Ignite-UX 的两个主要功能区域。它们是：

- 从拥有软件库的服务器对客户端（或目标）系统进行网络安装。这些库通常通过从介质复制软件到 Ignite-UX 服务器上的库来创建。这与第 2 章中介绍的软件安装有些相似，不同之处在于软件位于服务器上而不是介质上。还有一个图形用户界面，允许你从服务器控制此过程。使用此技术，你可以选择要在每个特定客户端上加载的具体软件。你可以从服务器“推送”软件到客户端，或者从服务器“拉取”软件到客户端。除了从介质创建软件库外，你还可以从“黄金镜像”创建操作系统归档。“黄金镜像”是你希望复制到许多系统的完美运行系统。`make_sys_image` 命令生成“黄金系统”的压缩镜像。在本章中，我们将重点讨论通过从服务器上的介质复制到库来创建的软件库。
- 创建可引导的系统恢复磁带。此功能允许你将根卷的镜像创建到磁带上。之后你可以从此磁带引导并直接从磁带恢复根卷组。

让我们在接下来的部分中看看 Ignite-UX 的这两个方面。请务必检查 www.docs.hp.com 以获取有关 Ignite-UX 的优秀文档，以及 www.software.hp.com 以获取最新的 Ignite-UX 软件。其中一些文档比我在接下来的“如何做”部分中提供的细节更丰富。

我将假设你已经在你的服务器系统上加载了 Ignite-UX 产品。此软件与 HP-UX 11i 和 11.0 捆绑提供，因此只需从介质将其加载到你的服务器系统即可。如果你从 *software.hp.com* 网站下载，可以确保获取最新版本的 Ignite-UX。本章中处理 Ignite-UX 的过程对于 HP-UX 10.20、11.0 和 11i 几乎相同。无论你运行哪个版本的 HP-UX，本章都适用。

安装 Ignite-UX 后，你可能希望更新你的路径，以便无需为每个 Ignite-UX 命令输入完整路径。对于默认的正 POSIX shell，你可以执行以下命令：

```
# export PATH=${PATH}:/opt/ignite/bin
```

此命令更新你的路径以包含大多数 Ignite-UX 可执行文件的目录，**/opt/ignite/bin**。

#### 设置带有库的服务器并安装客户端

你可以使用几乎任何系统作为你的 Ignite-UX 服务器。你可以在你的服务器上为 HP-UX 11i、11.0 和 10.20 设置库。我建议使用 11.00 或 11i 系统作为 Ignite-UX 服务器，因为我曾遇到 10.20 系统作为服务器为 11.00 和 11i 客户端加载软件时的问题。我从未见过 11.0 或 11i 系统作为服务器为任何版本的 HP-UX 客户端加载软件时出现问题。不过，总的来说，服务器作为库的主机，其操作系统不是将软件加载到客户端的组成部分。在我们的示例中，我们将使用运行 11.00 的工作站（型号 J2240）。从我们在此系统上创建的 11.00 库中，我们可以加载各种客户端。就加载客户端而言，重用工作站而不是服务器无关紧要。我发现许多系统管理员使用工作站作为 Ignite-UX 服务器，即使他们主要加载的是服务器，如 N-Class 系统。

你在 Ignite-UX 服务器上创建的软件库会占用大量磁盘空间。包含许多应用程序的核心操作系统可能占用数 GB 的磁盘空间。我喜欢为 Ignite 服务器分配几 GB 的磁盘空间，这样在系统上加载额外库时，我就不必增加 **/var**（软件库的默认位置）的大小。我的经验法则是 **/var** 设为 6 GB，以支持多个库。





为了让您大致了解软件仓库（depots）所消耗的磁盘空间，我在初始系统安装完成时（此时尚未创建任何软件仓库）以及创建核心操作系统和应用仓库之后，分别执行了以下 **bdf** 命令。软件仓库的默认位置是 **/var**；不过，您可以将仓库加载到任何目录中。我建议创建一个文件系统，例如 */var/depots*，作为仓库区域。在下面的示例中，我们将重点关注 **/var** 的容量，因为它在后续示例中用作仓库的目标位置。

```
# bdf
Filesystem      kbytes   used    avail  %used Mounted on
/dev/vg00/lvol3 204800   19830   173464  10%  /
/dev/vg00/lvol1  83733    13654   61705   18%  /stand
/dev/vg00/lvol8  6553600 156292  5998347   3%  /var
/dev/vg00/lvol7  512000   341251  160127   68%  /usr
/dev/vg00/lvol4  102400    1522   94578    2%  /tmp
/dev/vg00/lvol6  602112  186976  389238   32%  /opt
/dev/vg00/lvol5  204800    1157  190923    1%  /home
/dev/dsk/c1t2d0 2457600 2457600      0   100%  /var/tmp/cddirAAAA02574
```

以下是在创建 11.0 核心操作系统仓库后立即执行的 **bdf** 命令输出，显示 **/var** 的可用空间已从 5.998 GBytes 减少到约 5.667 GBytes。这代表了约 330 MBytes 的数据作为核心操作系统的一部分被加载。

```
# bdf
Filesystem      kbytes   used    avail  %used Mounted on
/dev/vg00/lvol3 204800   19943   173357  10%  /
/dev/vg00/lvol1  83733    13654   61705   18%  /stand
/dev/vg00/lvol8  6553600 507000  5668779   8%  /var
/dev/vg00/lvol7  512000   341251  160123   68%  /usr
/dev/vg00/lvol4  102400    3350   92862    3%  /tmp
/dev/vg00/lvol6  602112  186976  389238   32%  /opt
/dev/vg00/lvol5  204800    1157  190923    1%  /home
/dev/dsk/c1t2d0 2457600 2457600      0   100%  /iuxcdrom0
#
```

通过查看仓库位置（如下面列表所示），可以确认核心操作系统仓库所占用的磁盘空间：

```
# cd /var/opt/ignite/depots
# du -s *
688842  Rel_B.11.00
#
```

这个 **du** 命令的输出列表显示，核心操作系统目录中大约有 330 MBytes（688K 个块除以每块 2048 字节）的数据。与我们将要加载到 **depots** 目录中的所有应用程序软件相比，核心操作系统仓库占用的这 330 MBytes 磁盘空间显得微不足道。我们将把核心操作系统和应用程序都放在此目录中，因此将消耗大量更多的空间。

为了进一步强调所消耗的磁盘空间数量，下面的 **du** 命令显示了核心操作系统仓库（仍约为 330 MBytes）和随操作系统发行版附带三张 CD-ROM 中包含的所有应用程序所消耗的磁盘空间总量。/var/opt/ignite/depots/app 目录，它是这三张应用程序 CD-ROM 内容的仓库，大约为 3.7 GBytes！

```
# cd /var/opt/ignite/depots
# du -s *
688874  Rel_B.11.00
3722622 app
#
```

应用程序占用的空间是核心操作系统占用空间的 10 倍多。这 3.7 GBytes 包含了操作系统 11.0 版本中可用的所有应用程序；不过，这能让您了解在使用 Ignite-UX 创建仓库时所需的存储空间。

#### 运行 Ignite-UX GUI

加载 Ignite-UX 工具后，如果您已为 `/opt/ignite/bin/` 设置好路径，可以输入 **ignite**；或者，您可以输入完整路径 `/opt/ignite/bin/ignite` 来调出 Ignite-UX 的图形界面，如图 10-4 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_588_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_589_0.png)

图 10-4 Ignite-UX 欢迎屏幕

在此窗口中，我们可以进行各种选择以配置 Ignite-UX 以适应我们的环境。我们将执行的第一项配置是*服务器设置*（*Server Setup*）。当我们选择*服务器设置*时，会显示图 10-5 中的屏幕，该屏幕允许我们在选项 1 下为希望通过 Ignite-UX 管理的客户端设置 IP 地址。

![](img/eff8b9287a5f38c5adf538f24aacf29e_590_0.png)

我们将为预计通过 Ignite-UX 接口加载的几个客户端设置一组地址，如图 10-6 所示。请务必在您的主机数据库（如 /etc/hosts 文件）中也为这些客户端添加条目。

![](img/eff8b9287a5f38c5adf538f24aacf29e_591_0.png)

图 10-6 一组客户端 IP 地址

我们设置了由 Ignite-UX 管理的七个客户端的一组地址。

接下来，让我们通过图形界面为 HP-UX 11.0 创建一个核心操作系统仓库。我们将从原始 CD-ROM 复制核心操作系统，这是我们将在图 10-7 中做出的选择：

![](img/eff8b9287a5f38c5adf538f24aacf29e_592_0.png)

在做出从 CD-ROM 加载的选择后，会出现另一个窗口，我们的示例中没有显示该窗口。在此，我们指定仓库将加载到的位置。默认情况下，目录是 /var/opt/ignite/depots（例如，对于 HP-UX 11.11 版本，完整路径为 /var/opt/ignite/depots/Rel_B.11.11/core）；但是，我们可以为仓库指定任何目录位置。例如，如果您在 /localapps 中有大量未使用的磁盘空间，可以将完整路径设为 /localapps/depots/Rel_B.11.11/core。接下来，我们会收到一个状态窗口，显示软件复制和仓库创建的进度，如图 10-8 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_593_0.png)

图 10-8 软件仓库创建状态

软件复制和仓库设置完成后，我们会得到如图 10-9 所示的窗口：

![](img/eff8b9287a5f38c5adf538f24aacf29e_594_0.png)

图 10-9 软件仓库已创建完成

核心操作系统的仓库自动创建于 **/var/opt/ignite/depots/Rel_B.11.00** 下。如本章前文所述，该仓库消耗约 330 MBytes 的磁盘空间。

至此，我们仅通过 Ignite-UX 服务器上的图形界面创建了核心操作系统仓库并配置了客户端。在撰写本文时，无法使用图形界面创建应用程序软件仓库。我们将使用三条 Ignite-UX 命令来创建应用程序仓库。首先，我们将为希望制作成仓库的三张应用程序 CD-ROM 运行 **make_depots** 命令。然后，我们将为创建的应用程序仓库运行一次 **make_config** 命令。最后，我们将为创建的应用程序仓库运行一次 **manage_index**。让我们在下面的列表中查看这些命令中的每一个。

```
# /opt/ignite/bin/make_depots -d /var/opt/ignite/depots/app -s /dev/dsk/c1t2d0
# /opt/ignite/bin/make_depots -d /var/opt/ignite/depots/app -s /dev/dsk/c1t2d0
# /opt/ignite/bin/make_depots -d /var/opt/ignite/depots/app -s /dev/dsk/c1t2d0
```

我们添加了 **-d** 选项以指定应用程序媒体内容的目标目录 **app**。我们也可以指定其他目标目录。使用前面的例子，例如，我们可以使用 **-d /localapps/depots/app** 指定目标。在此情况下，我们将加载整个应用程序媒体，即三张 CD-ROM。接下来，我们运行 **make_config**：

```
# /opt/ignite/bin/make_config -s /var/opt/ignite/depots/app
# /opt/ignite/bin/make_config -c /var/opt/ignite/data/Rel_B.11.00/app.cfg
NOTE: make_config can sometimes take a long time to complete. Please be patient!
```

我们将 **app.cfg** 文件放置在特定操作系统版本的目录中。这是一种组织配置文件的方法，使得与特定操作系统版本相关的文件被归为一组。如果我们使用了不同的应用程序目录位置，我们会用 **-s /localapps/depots/app** 指定，但保持 **app.cfg** 文件在同一位置。您可能需要查看 **/var/opt/ignite/data/<yourHP-UXrelease>/** 中的配置文件以



查看其内容。这些文件包含作为您的 Ignite-UX 仓库一部分已加载的所有软件的信息。

`manage_index` 命令用于管理 Ignite-UX 所使用的索引文件，示例如下：

```
# /opt/Ignite/bin/manage_index -a -f /var/opt/Ignite/data/Rel_B.11.00/app.cfg
```

此时，我们已通过 Ignite-UX 图形界面设置了核心操作系统仓库，并通过命令行的三个 Ignite-UX 命令设置了应用程序仓库。现在，在 `/var/opt/Ignite/INDEX` 中也有一个针对您的操作系统版本的条目。您应该查看此文件，以便看到为您的操作系统版本创建的条目。

现在，让我们回到在服务器上使用 Ignite-UX 图形界面。我们可以通过服务器上的 Ignite-UX 界面获取特定客户端的信息。将在服务器上出现的窗口如图 10-10 所示，对应我们要通过 Ignite-UX 启动的客户端：

![](img/eff8b9287a5f38c5adf538f24aacf29e_597_0.png)

*图 10-10* 客户端信息

既然我们已经创建了核心操作系统和应用程序仓库，我们就可以通过服务器上的 Ignite-UX 启动并加载其中一个客户端。

除了像我们在服务器上通过 Ignite-UX 图形界面以“推送”方式控制客户端之外，您还可以在客户端以“拉取”方式进行操作。若要在坐在服务器前时从服务器启动客户端，请在中断启动过程后从 PDC（处理器相关代码；参见第 1 章）发出以下命令：

```
BOOT ADMIN> boot lan 15.32.163.26 install
```

指定的 IP 地址是服务器的地址，即我们设置软件仓库的地方。坐在客户端前时，您将看到字符模式下的 Ignite-UX 界面，并坐在客户端前使用我们在服务器上设置好的软件仓库继续安装过程。

回到 GUI（图形用户界面），我们通过作为初始操作系统加载的一部分的熟悉的 Ignite-UX 界面选择要加载的软件，如图 10-11 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_598_0.png)

图 10-11 在客户端上选择要加载的软件

请注意图 10-11 中我们位于屏幕顶部的“软件”选项卡。我们将在接下来的两幅图中依次浏览“系统”和“文件系统”选项卡。请记住，所有这些操作都是在我们设置的 Ignite-UX 服务器上进行的。

我们在图 10-11 中选择了属于我们创建的应用程序仓库的一部分的 Java 产品。核心操作系统和其他软件的选择也是在软件窗口中完成的。

除了软件加载外，我们还可以在服务器上对要加载的客户端执行额外的配置，例如在“系统”选项卡下提供系统名称，如图 10-12 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_599_0.png)

图 10-12 设置客户端系统

接下来，我们可以在“文件系统”选项卡下执行与文件系统相关的配置，如图 10-13 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_600_0.png)

当我们在服务器上完成针对客户端的 Ignite-UX 所有初始工作后，就可以继续进行客户端加载。图 10-14 显示了我们开始配置和加载客户端时出现在服务器上的两个 Ignite-UX 窗口：

![](img/eff8b9287a5f38c5adf538f24aacf29e_601_0.png)

图 10-14 客户端加载状态

图 10-14 中最左边的窗口显示了我们正在处理的系统的图标，最右边的窗口提供客户端加载的状态。由于我们只处理一个系统，因此最左边的窗口中只显示一个图标。最右边窗口中软件加载的状态表明 *加载软件* 是一个 **活动（ACTIVE）** 进程。一些进程已经 **完成（COMPLETE）**，还有一些其他进程处于 **待处理（PENDING）** 状态。

*虽然您在原始截图中看不到颜色，但状态消息是按颜色编码的。*

使用 Ignite-UX 您还可以完成更多工作，例如将配置文件分组为可在加载客户端时选择的集合，安装补丁仓库，以及其他许多有用的任务。位于 www.docs.hp.com 的 *Ignite-UX 管理员指南* 涵盖了许多其他主题。

然而，从我们在本节中执行的步骤中，您可以看到创建软件仓库和管理客户端是多么简单。

#### 使用 Ignite-UX 进行系统恢复

Ignite-UX 是随 HP-UX 11i 捆绑提供的产品，它提供了一种创建可启动系统恢复磁带的流程。磁带包含一个启动区域和一个操作系统存档。如果您的根磁盘故障或发生损坏，您可以使用可启动系统恢复磁带来恢复。

**make_recovery** 是用于创建可启动系统恢复磁带的 Ignite-UX 工具。在撰写本文时，**make_recovery** 正被 **make_net_recovery** 取代，但本节将使用 **make_recovery**，因为本节介绍的 **check_recovery** 功能尚未在 **make_net_recovery** 中实现。您可以从系统恢复磁带启动并恢复，然后使用您的系统备份完全恢复系统。如果您的根磁盘在非镜像环境中失效，您应执行以下步骤从故障中恢复：

- 更换故障的根磁盘。
- 通过选择磁带设备从恢复磁带启动。
- 监视从恢复磁带恢复操作系统存档的过程。
- 使用备份信息恢复系统上的其余数据。

可启动系统恢复磁带由逻辑交换格式（LIF）卷和操作系统存档组成。LIF 卷包含从磁带启动所需的所有组件。操作系统存档默认仅包含核心操作系统。

如有需要，您可以使用两种不同的技术将额外文件包含在操作系统存档中。第一种是编辑文件 /var/opt/ignite/recovery/makrec.append，并添加您希望包含在操作系统存档中的文件名、目录名或软件分发产品名。第二种技术是以预览模式运行 **make_recovery** 并添加 -p 选项，手动添加要包含和/或排除在存档中的文件，然后使用 -r 选项继续运行 **make_recovery**。HP-UX 系统上的 /opt/ignite/bin/make_recovery 和 /opt/ignite/bin/ignite 的联机手册页提供了相关信息。

您还可以使用 **check_recovery** 命令确定您的恢复磁带是否为最新。使用 -C 选项运行 **make_recovery** 会生成系统恢复状态文件。**check_recovery** 将系统恢复状态文件与系统的当前状态进行比较，并生成差异列表。您可以从此列表确定是否需要生成另一张系统恢复磁带。HP-UX 系统上 **/opt/ignite/bin/check_recovery** 的联机手册页提供了相关信息。

恢复功能只是 Ignite-UX 产品的一个组件。Ignite-UX 提供了一种通过网络安装系统的手段，既可以从 Ignite 服务器向客户端推送安装，也可以从 Ignite 服务器拉取安装到客户端。使用 Ignite-UX，可以创建标准安装设置的“黄金映像”，并通过通过网络从该映像“点燃”系统在几分钟内完成系统设置。更多有关 Ignite-UX 的信息可在 Internet 上的 *http://www.software.hp.com/products/IUX* 上查看，也可以在惠普公司《安装 HP-UX 11.0 并将 10.x 升级到 11.0》手册的“配置 Ignite-UX 服务器”和“从 Ignite-UX 服务器安装”章节以及附录 C：“Ignite-UX 系统管理”中阅读。同一手册中的“HP-UX 系统恢复”章节提供了有关 Ignite-UX 的 **make_recovery** 功能的更多信息。

##### 创建可启动系统恢复磁带的示例

既然我们已经介绍了 Ignite-UX 恢复流程的基本组件和功能，让我们来看一个创建可启动系统恢复磁带的示例。

让我们首先运行带有 *-p* 选项的 **make_recovery**，这样我们可以查看 Ignite-UX 报告磁带中包含信息的方式。我还将使用 *-A* 选项，它指定要包含整个根卷组。我有时使用 **make_recovery** 来克隆相同的系统，方法是通过使用 *-A* 选项生成恢复磁带，然后在希望与原始系统相同的系统上加载该磁带。如果您有大的根卷组，或者执行常规备份并且不需要在恢复磁带上包含所有根卷组信息，则不会使用 *-A* 选项。除了用于预览的 *-p* 和用于全部内容的 *-A* 之外，我还会在以下预览命令示例中使用详细选项 *-v* 和创建系统状态文件的 *-C*：




## make_recovery -p -v -A -C

*** 仅预览模式 ***

指定了选项 -A。整个核心卷组/磁盘将被备份。

HP-UX 系统恢复
正在验证追加文件
完成

核心操作系统磁盘/卷组上的文件系统：

| vg 名称 | PV_名称 |
|---|---|
| vg00 | /dev/dsk/c0t5d0 |

| 卷组 | 逻辑卷 | 挂载点 |
|---|---|---|
| vg00 | /dev/vg00/lvol3 | /home |
| vg00 | /dev/vg00/lvol4 | /opt |
| vg00 | /dev/vg00/lvol5 | |
| vg00 | /dev/vg00/lvol6 | /stand |
| vg00 | /dev/vg00/lvol6 | /tmp |
| vg00 | /dev/vg00/lvol7 | /usr |
| vg00 | /dev/vg00/lvol8 | /var |

创建挂载点：
- /apsk
- /work
- /spill
- /spill2
- /rbdisk01
- /rbdisk02
- /rbdisk03
- /rbdisk04
- /rbdisk05
- /rbdisk06
- /rbdisk07
- /rbdisk08
- /rbdisk09
- /rbdisk10
- /rbdisk11
- /rbdisk12
- /rbdisk13
- /rbdisk14
- /rbdisk15
- /rbdisk16
- /rbdisk17
- /rbdisk18
- /nfs

/cpt 是一个已挂载的目录
- 它位于核心卷组中
- 挂载于 /dev/vg00/lvol5

/var 是一个已挂载的目录
- 它位于核心卷组中
- 挂载于 /dev/vg00/lvol8

目标设备 = /dev/rmt/0m
启动 LIF 位置 = /var/tmp/uxinstlf.recovery

*******************************
仅预览模式。未创建磁带

文件 /var/opt/ignite/recovery/arch.include 已创建。
可以修改该文件以排除已知文件。
仅删除严格由用户创建的文件或目录。
然后可以使用 -r 选项恢复系统恢复磁带的创建过程。
命令将不再执行进一步检查。
清理

此时已生成 **arch.include** 文件。该文件列出了将作为存档一部分的文件，你可以对其进行修改。以下是 **arch.include** 的简略列表，仅显示文件的开头和结尾部分：

```
/lost+found
/etc
/etc/vue
/etc/vue/config
/etc/vue/config/types
/etc/vue/config/types/tools
/etc/vue/config/types/tools/System_Admin
/etc/vue/config/types/tools/System_Admin/FontClientSvr
/etc/vue/config/types/tools/System_Admin/SetNetworking
/etc/vue/config/types/tools/System_Admin/ShutdownSystem
/etc/vue/config/types/tools/System_Admin/VerifyPRX
/etc/vue/config/types/tools/System_Admin/VerifyPRX
/etc/vue/config/types/tools/Media
.
.
.
/spp/scripts/tc_standalone
/spp/scripts/sppconsole.old
/spp/unsupported
/spp/unsupported/chus
/spp/unsupported/clear_pid
/spp/unsupported/ex_shm
/spp/unsupported/rdr_dumper.fw
/spp/unsupported/rdr_formatter
/spp/unsupported/reset_jtag
/spp/unsupported/scan_sram
/users
/users/sppuser
/users/sppuser/.Xdefaults
/users/sppuser/.cshrc
/users/sppuser/.kshrc
/users/sppuser/.login
/users/spuser/.mmwrc
/users/spuser/.profile
/users/spuser/.x11start
/users/spuser/.x11startlog
/users/spuser/.sh_history
/users/spuser/.sw
/users/spuser/.sw/sessions
/users/spuser/.sw/sessions/swlist.last
/users/spuser/.history
.sh_history
.profile
/lib
/bin
/bin
/core
/ignite_10.20.tar
/var/tmp/makrec.lasttmp
/var/opt/ignite/recovery/chkrec.include
/var/opt/ignite/recovery/config.recover
```

在执行此 **make_recovery** 操作的系统中，**arch.include** 文件包含超过 44,000 行，如下所示：

```
# cat /var/opt/ignite/recovery/arch.include | wc
44142 44146 1730818
```

现在让我们恢复 **make_recovery**，它之前是在预览模式下运行的，使用 *-r* 选项进行恢复，*-v* 选项用于详细输出，*-C* 选项用于创建系统状态文件。由于将使用默认磁带设备，因此不会指定 *-d* 选项。之前在预览模式下指定的 *-A* 选项表示要包含整个根卷组。

```
# make_recovery -r -C -v
make_recovery(306). 处于恢复模式。是否继续？y

************************
HP-UX 系统恢复
核心操作系统磁盘/卷组上的文件系统：

  vg 名称 = vg00
  pv_名称 = /dev/dsk/c0t0d0

vg00 /dev/vg00/lvol3 /
vg00 /dev/vg00/lvol5 /home
vg00 /dev/vg00/lvol5 /opt
vg00 /dev/vg00/lvol1 /stand
vg00 /dev/vg00/lvol6 /tmp
vg00 /dev/vg00/lvol7 /usr
vg00 /dev/vg00/lvol8 /var

创建挂载点
/appe
/work
/spill
/spill2
/rbdisk01
/rbdisk02
/rbdisk03
/rbdisk04
/rbdisk05
/rbdisk06
/rbdisk07
/rbdisk09
/rbdisk10
/rbdisk11
/rbdisk12
/rbdisk13
/rbdisk14
/rbdisk15
/rbdisk16
/rbdisk17
/rbdisk18
/nfs

/opt 是一个已挂载的目录
- 它位于核心卷组中
- 挂载于 /dev/vg00/lvol5

/var 是一个已挂载的目录
- 它位于核心卷组中
- 挂载于 /dev/vg00/lvol8

目标设备 = /dev/rmt/0m
启动 LIF 位置 = /var/tmp/uinstlf.recovery

*********************
正在创建配置文件。
完成
正在修改配置文件。
完成
正在备份 vg 配置
卷组 vg00
卷组 vg01
卷组 vg03
卷组 vg02
完成
正在创建 /var/opt/ignite/recovery/makrec.last 文件
完成
即将创建磁带。
正在处理磁带
调用 instal_adm -T
正在创建启动 LIF
完成
正在将启动 LIF 写入磁带 /dev/rmt/0mn

完成
正在创建存档 - 这可能需要大约 30 分钟。
  完成
成功创建系统恢复磁带。
```

现在已生成系统恢复磁带。你可以从该系统恢复磁带启动，并恢复该系统上的整个卷组 **vg00**。

##### 运行 check_recovery 命令

你可以随时运行 **check_recovery** 命令，以查看自上次使用 -C 选项创建系统恢复状态文件以来系统所做的更改。以下示例展示了运行 **check_recovery** 命令的结果：

```
# check_recovery
自上次创建系统恢复映像以来，已检测到以下软件产品更改。
(已添加)    Auxillary-OptB.11.01.01    HP 语言的辅助优化器。
(已添加)    ObjCOBOLB.12.5.0          对象 COBOL 开发工具
自上次创建系统恢复映像以来，以下系统文件（或链接）已添加到当前系统中。
/apps/informix7.3/lib/iosm07a.sl
/apps/informix7.3/lib/ipldd07a.sl
/apps/informix7.3/lib/r1borb_r.sl
/dev/vg13/lvol01
/dev/vg13/r1vol01
/etc/sam/custom/sccjs.cf
/etc/sam/custom/secar.cf
/sbin/init.d.flex
/sbin/rc2.d/S599flex
/usr/lib/iosm07a.sl
/usr/lib/iosm07a.sl.980709
/usr/lib/ipldd07a.sl.980709
/usr/lib/nwst.w.sl
/usr/local/adm/bin/user watch.pl
/usr/local/adm/etl/repf
/usr/local/flexlm/bin/lmcksum
/usr/local/flexlm/bin/lmdtag
/usr/local/flexlm/bin/lmdown
/usr/local/flexlm/bin/lmgrd
/usr/local/flexlm/bin/lmshowi
/usr/local/flexlm/bin/lmremove
/usr/local/flexlm/bin/lmread
/usr/local/flexlm/bin/lmstat
/usr/local/flexlm/bin/lmswitchr
/usr/local/flexlm/bin/lmutil
/usr/local/flexlm/bin/lmwx
/usr/local/flexlm/daemons/HPCUPLANGS
/usr/local/flexlm/liceneses/license.dat
/usr/local/flexlm/licenses/license.log
/usr/share/man/cat1.2/X.1
/usr/share/man/cat1.2/Xserver.1
/usr/share/man/cat1.2/grep.1
/usr/share/man/cat1.2/lmwx.1
/usr/share/man/cat1.2/Imake.1
/usr/share/man/cat1.2/xset.1
/usr/share/man/cat2.2/exec.2
```

自上次创建系统恢复映像以来，以下系统文件（或链接）已从当前系统中删除。

```
/dev/vg1/lvol1
/dev/vg1/lvol1
/stand/build/conf.o
```

自上次创建系统恢复映像以来，当前系统中的以下系统文件（或链接）已被修改。

| 路径 | 属性 | 当前值 | makrec.last |
|---|---|---|---|
| /dev/pty/ptyp2 | 权限 | CRW-RW- | CRW-W--- |
| /dev/pty/ptyp2 | uid | 0 | 102 |
| /dev/pty/ptyp2 | gid | 0 | 10 |
| /dev/pty/ptyp3 | 权限 | CRW-W--- | CRW-RW- |
| /dev/pty/ptyp3 | uid | 102 | 0 |
| /dev/pty/ptyp3 | gid | 10 | 0 |
| /dev/pty/ptyp4 | 权限 | CRW-W--- | CRW-RW- |
| /dev/pty/ptyp4 | uid | 0 | 0 |
| /dev/pty/ptyp4 | gid | 10 | 0 |
| /dev/pty/ptyp5 | 权限 | CRW-RW- | CRW-W--- |
| /dev/pty/ptyp5 | uid | 0 | 102 |
| /dev/pty/ptyp5 | gid | 0 | 10 |
| /dev/pty/ptyp6 | 权限 | CRW-RW- | CRW-W--- |
| /dev/pty/ptyp6 | uid | 0 | 102 |
| /dev/pty/ptyp6 | gid | 0 | 10 |
| /dev/pty/ptyp8 | uid | 0 | 2 |
| /dev/pty/ptyp8 | gid | 0 | 10 |
| /dev/pty/pty2 | 权限 | CRW-RW- | CRW-W--- |
| /dev/pty/pty2 | uid | 0 | 102 |
| /dev/pty/pty2 | gid | 0 | 10 |
| /dev/pty/pty3 | 权限 | CRW-W--- | CRW-RW- |
| /dev/pty/pty3 | uid | 102 | 0 |
| /dev/pty/pty3 | gid | 10 | 0 |
| /dev/pty/pty4 | 权限 | CRW-W--- | CRW-RW- |
| /dev/pty/pty4 | gid | 10 | 0 |
| /dev/pty/pty5 | 权限 | CRW-RW- | CRW-W--- |
| /dev/pty/pty5 | uid | 0 | 102 |
| /dev/pty/pty5 | gid | 0 | 10 |
| /dev/pty/pty6 | 权限 | CRW-RW- | CRW-W--- |
| /dev/pty/pty6 | uid | 0 | 102 |




## 第10章 输出和恢复程序细节

| 路径 | Inode | 大小 | 修改时间 | 权限 |
| :--- | :--- | :--- | :--- | :--- |
| /dev/tty5 | 0 | 0 | 10 | 0 |
| /etc/MANPATH | .checkaun | 1982379524 | 497249200 | 2 |
| /etc/PATH | .checkaun | 562993260 | 2784298760 | |
| /etc/SHLIB_PATH | .checkaun | 2664385509 | 241316845 | |
| /etc/fstab | .checkaun | 3014086519 | 200239819 | |
| /etc/fstab.old | .checkaun | 682979636 | 2528618126 | |
| /etc/group | .checkaun | 368341889 | 127908837 | |
| /etc/lvmonconf/vgl3.conf | .checkaun | 1522028984 | 929609311 | |
| /etc/lvmonconf/vgl3.conf.old | .checkaun | 1839986219 | 3891043243 | |
| /etc/lvmtab | .checkaun | 4147789897 | 3277798772 | |
| /etc/passwd | .checkaun | 1663178396 | 2350540120 | |
| /etc/profile | .checkaun | 510591831 | 2645970599 | |
| /stand/build/conf.SAM.c | .checkaun | 3973853979 | 4022316306 | |
| /stand/build/conf.GAM.c | .checkaun | 4142700410 | 118504999 | |
| /stand/build/conf.o.old | .checkaun | 2526704160 | 1129366190 | |
| /stand/build/config.fam.mk | .checkaun | 2849240259 | 1705279848 | |
| /stand/build/function_names.c | .checkaun | 2434797998 | 12406464943 | |
| | .permissions | rw-rw-rw- | rw-r--rw- | |
| /stand/build/function_names.o | .checkaun | 3857693076 | 1165263911 | |
| | .permissions | rw-rw-rw- | |
| /stand/build/space.h | .permissions | rw-rw-rw- | rw--I--- | |
| /stand/build/tune.h | .checkaun | 2763942582 | 2084825502 | |
| /stand/dhkm,vmunix.prev/symtab | .checkaun | 2086890351 | 1785861028 | |
| | .permissions | rw-r-r-- | rw-rw-rw- | |
| /stand/dhkm,vmunix.prev/system | .checkaun | 3376707916 | 2873910478 | |
| /stand/dhkm/symtab | .checkaun | 2368412414 | 2086890351 | |
| | .permissions | rw-rw-rw- | rw-r--- | |
| /stand/dhkm/system | .checkaun | 2855591959 | 3376707916 | |
| /stand/system | .checkaun | 4141126356 | 1910321628 | |
| | .permissions | rw-rw-rw- | rw-r--r-- | |
| /stand/system.prev | .checkaun | 1910321628 | 253449911 | |
| | .permissions | 1 1 1 | rw-rw-rw- | |
| /stand/vmunix | .checkaun | 2977157561 | 2742478025 | |
| /stand/vmunix.prev | .checkaun | 2742478025 | 3594481120 | |
| /usr/lib/spldda7a.sl | .linkname | /apps/inforix/7.3/lib/spldda7a.sl | | |

/apps/informix/lib/lpldd07a.sl
/usr/local/samba.1.9.18p3/var/locks/browse.dat
    checksum    2594069517     2221092461
/usr/local/samba.1.9.18p3/var/log.nmb
    checksum    4219127043     2190854115
/usr/local/samba.1.9.18p3/var/log.smb
    checksum    2251415300     1791314631
/var/spool/cron/crontabs/root
    checksum    2015828837     1660287231

此输出表明系统发生了许多变化，包括软件添加以及系统文件的添加、删除和修改。如果 **check_recovery** 对系统产生了任何重大变化，你应该重新运行 **make_recovery** 命令，以便系统恢复磁带反映系统的当前状态。完成本节所述的程序后，生成了许多文件。其中一些你可以查看的文件位于 `/var/opt/ignite/recovery` 目录中，如下所示：

```
# cd /var/opt/ignite/recovery
# ll
total 5412
-rw-rw-rw- 1 root sys      1737051 Jul 13 16:17 arch.include
-rw-rw-rw- 1 root sys         250 Jul 13 16:12 chkrec.include
-rw-rw-rw- 1 root sys      4872 Jul 13 16:12 config.recover
-rw-rw-rw- 1 root sys      4872 Jul 13 16:17 config.recover.prev
-rw-rw-rw- 1 root sys       1682 Jul 13 16:12 fstab
-rw-rw-rw- 1 root sys        390 Jul 13 16:29 group.makrec
-rw-rw-rw- 1 root sys       1971 Jun 25 12:27 makrec.append
-rw-rw-rw- 1 bin     1971 Apr 24 00:28 makrec.append.org
-rw-rw-rw- 1 root sys     1010844 Jul 13 16:28 makrec.last
-rw-rw-rw- 1 root sys        2573 Jul 13 16:29 passwd.makrec
```

##### 第10章中使用的命令的手册页

下一节包含 **make_net_recovery** 手册页。

###### make_net_recovery

make_net_recovery - 创建 Ignite-UX 系统恢复归档。

make_net_recovery(1M)

名称

make_net_recovery - 基于网络的系统恢复归档创建

概要

```
/opt/ignite/bin/make_net_recovery -s Ignite-UX_server [-v] [-P partial_inclusion_indicator] [-l|-lb] [-a archive_server:archive_dir] [-d description] [-f content_files] [-i lanic_id] [-n num_archives] [-X content-options] [XToolKit-Options]
```

描述

make_net_recovery 工具创建一个系统恢复归档并将该归档存储到网络上。由 make_net_recovery 创建的归档是针对其创建所在的系统特有的，其标识包括主机名、ip_address、网络信息等。在根磁盘发生故障的情况下，可以通过 Ignite-UX 安装恢复归档以恢复系统。

系统恢复归档的内容始终包含被视为启动功能正常系统所必需的所有文件和目录。这个“必需”列表由 make_net_recovery 预定义。通过以交互模式运行 make_net_recovery，可以显示构成“必需列表”的目录和文件。除了必需列表之外，还可以基于磁盘/卷组、文件或目录基础将数据包含在归档中。还可以排除非必需的文件和目录。

选项

make_net_recovery 识别以下选项：

- **-a** *archive_server:archive_dir*
  指定存储归档的 NFS 服务器和位置。归档目录必须是 NFS 导出的（参见“导出归档目录”部分），并且需要足够的磁盘空间。默认值是 Ignite-UX 服务器的主机名，后跟存放归档的目录，例如，`Serverhost:/var/opt/ignite/recovery/archives/chohostname`（其中 `chohostname` 是被归档系统的主机名）。

![](img/eff8b9287a5f38c5adf538f24aacf29e_614_0.png)

主机名是被归档系统的名称。每个 make_net_recovery 客户端将在指定目录下创建一个以其客户端主机名命名的子目录来存储归档。

- **-t**
  当与 -i 选项组合使用时，它使 make_net_recovery 在交互式用户界面完成后在后台运行。

- **-d** *description*
  系统恢复归档的一行描述。如果描述中包含空格，则必须用引号括起描述。当从 Ignite-UX 图形用户界面中选择归档作为配置时，将显示此描述。默认描述是 Recovery Archive。

- **-f** *content_file*
  标识指定归档包含和排除的关键字的文件的位置。默认值是 `/var/opt/ignite/clients/0x[LLA]/recovery/archive_content`。
  该文件位于 Ignite-UX 服务器上，并由客户端通过 NFS 挂载访问。必须将 archive_content 文件的绝对路径名作为 -f 选项的参数提供。当希望管理指定归档内容的多个文件时，-f 选项可能很有用。使用 -x 选项指定归档内容时，不允许使用 -f 选项。

- **-i**
  使 make_net_recovery 交互式运行，以便你可以选择要包含在恢复归档中的文件和目录。在 Ignite-UX 服务器上运行交互式 make_net_recovery 会话时，最好使用 Ignite GUI 命令。从 Ignite 运行它将会执行任何额外的服务器 NFS 挂载配置。它还提供了更好的进度报告。

- **-l** *lani id*
  被归档系统的 lani id。用于在 Ignite-UX 服务器上创建每个客户端的目录。

- **-n** *num_archives*
  指定在任意给定时间应保留在服务器上的归档数量。默认值是 2。如果 num_archives>2，并且当创建第 3 个归档时已经存在 2 个归档，make_net_recovery 将在成功创建第 3 个归档后删除最旧的归档。

- **-P** *all|w*
  当磁盘或卷组部分包含在系统恢复归档中时，生成 ERROR(e)、WARNING(w) 或 SUPPRESS(s) 任何通常在部分包含发生时生成的警告消息。默认值是 w，因此在检测到磁盘和/或卷组的部分包含时产生警告消息。




当指定 `e` 参数时，错误消息将显示在标准输出和日志文件中，并在显示错误消息后停止 make_net_recovery 的执行。

### -s ignite-UX 服务器
指定 Ignite-UX 服务器的主机名。客户机系统的配置文件、默认值文件和内容文件将从 Ignite-UX 服务器的 /var/opt/ignite/clients/[[ox][LLA]]/recovery 目录中读取。make_net_recovery 工具将通过 NFS 挂载每个客户机的目录来访问此信息。

### -v
在创建系统恢复归档时显示详细进度消息。包括哪些卷组/磁盘将被包含在系统恢复归档中等信息。

### -x include=file|dir
将文件或目录包含在恢复归档中，但不跨越任何挂载点。

### -x inc cross=file|dir
将文件或目录包含在恢复归档中，并跨越挂载点以访问已挂载的目录或包含在已挂载目录中的文件。

### -x inc entree=/dev/dsk/<name> |vg_name
包含指定磁盘或卷组中的所有文件系统。在指定整盘（非 LVM）文件系统时，请使用 /dev/dsk/<name> 格式的设备文件。如果您希望将属于该 LVM 卷组的所有文件系统都包含在归档中，请使用卷组名称（例如 vg01）。

### -x exclude=file|dir
将文件或目录从归档中排除。当指定目录时，该目录下的任何文件都将不会存储在归档中。

## XToolkit 选项

make_net_recovery 命令支持标准 X Toolkit 选项的一个子集，以在指定 -i 选项时控制 GUI 的外观。支持的选项包括：-bg、-background、-fg、-foreground、-display、-name、-xrm 和 -synchronous。有关这些选项的定义，请参阅 X(1) 手册页。

## 归档的包含与排除

归档的内容可以通过内容文件进行控制。内容文件的完整路径为 /var/opt/ignite/clients/[[ox]][[LLA]]/recovery。归档标识符指定了文件、目录、整个磁盘和卷组的包含情况。关键字标识符还指示 make_net_recovery 在创建系统恢复归档时是否遵循挂载点。内容文件包含以下关键字标识符：

- include <文件名 | 目录>
  包含指定的文件名或目录以及所有子目录和关联文件。不会跨越挂载点，也不会跟随符号链接。
- inc_cross <文件名 | 目录>
  包含指定的文件名或目录以及所有子目录和子目录中包含的文件。会跨越本地挂载点，但不会跟随符号链接。
- inc_entire <卷组 | 磁盘>
  包含指定的整个卷组（例如 "vg00"）或磁盘（块设备 - 例如 "/dev/dsk/c1td5D0"）。如果磁盘是卷组的一部分，请勿指定该磁盘。
- exclude <文件名 | 目录>
  排除指定的文件名或目录以及所有子目录和子目录中包含的文件。

make_net_recovery 读取内容文件以生成用于创建系统恢复归档的文件列表。内容文件可以手动修改，也可以通过以交互模式运行 make_net_recovery 来修改。修改内容文件时，请记住以下几点：

- 不能排除任何基本文件或目录。对基本文件或目录的排除将被忽略。
- 排除优先于包含。同时被包含和被排除的任何内容都将从归档中排除。
- 默认文件中包含和排除的顺序并不重要。

## 使用以前归档创建的设置

默认文件存储了通过与 make_net_recovery GUI 交互指定的输入。选项会保留，直到通过与 GUI 交互生成下一个归档为止。命令行选项将覆盖默认文件中的设置。默认文件在 Ignite-UX 服务器上的完整路径为 /var/opt/ignite/clients/xxx/LUA//recovery/defaults。该目录通过 NFS 从客户机访问。

```
##### 默认文件 #####

RECOVERY_MULTI_IN-
RECOVERY_DESCRIPTION="recovery_archive"
SAVE_NUM_ARCHIVES=2
```

## 使用恢复归档

要使用网络恢复归档恢复故障系统：

- 如果正在替换客户机系统，或者自上次使用 make_net_recovery 以来 LAN 卡已更改，您应在开始恢复之前手动重命名旧的客户机目录。不这样做会导致创建新目录，您将无法看到在旧客户机目录下创建的恢复归档。要重命名客户机目录，请获取新的 LIA 地址（您可以在信息菜单中使用 LeadAddress 608-POW 命令），然后使用 mv 命令。例如：
  `mv /cd/L08108305461A XXX006GBCO43AB7`
- 如果您已经启动了新系统，在重命名旧目录之前需要移除新客户机。请小心不要移除包含恢复信息的旧目录。
- 使用网络引导、使用 make_boot_tape 创建的磁带，或者如果系统仍在运行则使用 bootsys 命令来启动系统。
- 不要与 ISL 交互
- 选择：[ 安装 HP-UX ]
- 从 Ignite-UX GUI：选择客户机的图标
- 选择 *安装/新安装*
- 选择要使用的恢复配置

## 导出归档目录

用于存储归档的目录必须从归档服务器导出到每个客户机。从存储归档的系统导出归档目录使 make_net_recovery 能够创建并通过 NFS 访问归档。归档服务器默认为 Ignite-UX 服务器，但可以使用 -a 选项更改为不同的远程服务器，甚至是本地客户机，如果您希望将归档作为客户机常规备份的一部分进行捕获。但是，请注意，如果归档存储在客户机本身，一旦需要使用它们进行恢复，必须将它们放到远程服务器上。

出于安全原因，最好将每个特定于客户机的归档目录仅导出给该单个客户机。如果恢复归档创建是从 Ignite GUI 发起的，无论 Ignite-UX 服务器在何处，且归档服务器与 Ignite-UX 服务器相同，/etc/exports 文件将自动编辑，以便将归档存储在期望的位置。否则，如果在客户机上直接运行 make_net_recovery，则需要在归档服务器上执行以下步骤。

- 在归档服务器上，为每个客户机创建一个目录，用于存放该客户机文件的归档。重要的是该目录的所有者必须是 *bin* 用户。请将以下命令中的 **client** 替换为客户机的主机名。如果使用 make_net_recovery 的 -a 选项来指定归档的替代位置，则需要使用那个路径而不是下面显示的默认路径。

```sh
mkdir -p /var/opt/ignite/recovery/archives/<client>
chown bin:bin /var/opt/ignite/recovery/archives/<client>
```

- 编辑 /etc/exports 为每个客户机添加条目。请将示例中的 <client> 替换为客户机的主机名：

```sh
/var/opt/ignite/recovery/archives/<client> -anow=2,access=<client>
```

- 运行 exportsfs 命令以使对 exports 文件的编辑生效：

```sh
/usr/sbin/exportsfs -av
```

## 网络功能

make_net_recovery 在客户机上建立两个 NFS 挂载点。Ignite-UX 服务器上的 /var/opt/ignite/clients 目录挂载到客户机系统，用于存储描述客户机配置和恢复归档位置配置文件。第二个挂载点指向 archive_server/archive_dir（参见 -a 选项），用于存储客户机系统的恢复归档。在系统恢复归档成功或不成功后，这些 NFS 挂载点将被卸载。

归档目录的 NFS 挂载可以按客户机为基础导出。每个客户机使用单独的归档目录。这允许您仅将每个目录 NFS 导出给拥有该归档的单个客户机，从而提供安全性。

如果客户机系统没有最新版本的 Ignite-UX 工具，Ignite-UX GUI 将使用 suinstall\[M\] 安装“恢复包”，其中包含执行恢复所需的所有必要文件。

## 返回值

make_net_recovery 在成功完成时返回 0。当发生警告时，返回 2。否则，当发生故障时返回 1。

## 示例

通过与 Ignite-UX 服务器上的 Ignite-UX GUI 交互来创建系统恢复归档：

```sh
export DISPLAY=hostname:0
ignite
```

从客户机创建系统恢复归档，使用上次调用 Ignite-UX GUI 时的设置。使用 Ignite-UX 服务器上的选项文件（位于默认位置 /var/opt/ignite/clients/OxDIA/recovery 中的 /server/）。

```sh
make_net_recovery -s myserver
```

创建包含 vg00 卷组中所有文件系统文件的系统恢复归档：



make_net_recovery -s myserver -x inc_entire=vg00

创建一个系统恢复归档，该归档包含 vg00 和 vg01 卷组中的所有文件，但排除 /depots 目录。

make_net_recovery -s myserver -x inc_entire=vg00 -x inc_entire=vg01 -x exclude=/depots

以下是一个示例 shell 脚本，可以在每个客户端上运行。它可以帮助您避免在服务器加载新发行版时，需要在每个客户端上更新 Ignite-UX。如果服务器上有更新的版本，它将自动更新网络恢复软件。这可能适合用于 crontab 条目中。此示例假设已创建 /var/opt/ignite/deposits/recovery_cmds 软件 depot。该 depot 是通过运行 ignite OQI 至少一次来创建系统恢复归档而创建的（另请参阅 pkg_rec_depot(1W)）。一旦创建，每次在服务器上更新 Ignite-UX 时，该 depot 将自动更新。

```bash
myserver=luxserver
/opt/ignite/bin/check_version -s $myserver
if [ $? != 0 ]
then
    swinstall -s
    $myserver:/var/opt/ignite/deposits/recovery_cmds `*`
fi
/opt/ignite/bin/make_net_recovery -s $myserver
```

## 警告

###### 磁盘将被重新格式化

如果恢复归档中包含来自某个磁盘或卷组的任何文件，则该磁盘（或卷组中的所有磁盘）将在恢复期间被重新格式化，且仅恢复包含在内的文件。未包含在归档中的任何文件，都必须从您的常规备份中恢复。

未在任何归档中包含文件的磁盘和卷组在恢复期间不会被重新格式化，而是在恢复结束时重新导入并重新挂载。

###### 逻辑卷物理区分配未保留

make_net_recovery 工具从系统中捕获足够的信息，以便在恢复期间重建先前 LVM 配置的大部分可见方面。这包括逻辑卷和卷组名称、属性，甚至次要号值。该工具还确保新的逻辑卷位于卷组中与之前相同的磁盘上。

然而，make_net_recovery 并不确保逻辑卷按照原始相同的顺序进行扩展。这意味着分配给逻辑卷的 LVM 物理区在磁盘上的位置可能与之前不同。恢复工具使用一种非常具体且复杂的算法来扩展逻辑卷以确保成功（例如在扩展非连续卷之前先扩展连续卷）。此行为的一个示例效果是，即使原始布局可能并非如此，swap/dump 卷仍将位于根磁盘上某些其他卷的前面。

###### 未包含 VxVM 磁盘组

由 VERITAS Volume Manager (VxVM) 管理的磁盘组无法包含在 Ignite-UX 归档中。如果包含它们，make_net_recovery 将报错退出。这些磁盘组将保持原样，并在恢复完成后重新集成到系统中。

###### 未恢复 LVM 磁盘镜像

make_net_recovery 工具会为具有镜像磁盘的系统创建恢复备份，但它不会恢复镜像磁盘配置。如果系统稍后恢复，之前镜像的卷将不再镜像。系统启动后，可以手动重新镜像它们。使用客户端目录中的 config.local 文件，您可以指定在系统恢复后自动执行的 LVM 命令，以恢复镜像磁盘。有关更多细节，请参阅白皮书 /opt/ignite/share/doc/diskmirror.pdf。

## 依赖项

必须从 Ignite-UX 服务器运行 Ignite-UX GUI。参见 Ignite(5)。make_net_recovery 依赖于其他几个 Ignite-UX 工具。当运行 Ignite-UX 服务器 GUI 时，Ignite-UX 会检查 make_net_recovery 在其上运行的客户端系统是否具有相同版本的 Ignite-UX 工具。

如果从未与 Ignite-UX GUI 交互，而是从命令行运行 make_net_recovery，则需要使用 swinstall(1M) 命令从 Ignite-UX 服务器将命令安装到 make_net_recovery 将在其上运行的客户端系统。

## 作者

Ignite-UX 和 make_net_recovery 由 Hewlett-Packard 公司开发。

## 诊断

网络恢复过程中的所有主要步骤都在服务器上记录，并通过 Ignite-UX 服务器 GUI 显示。

## 文件

-   **/opt/ignite/recovery/mr_essentials** 列出被认为必不可少的文件和目录，如果系统中存在这些文件，则它们始终包含在归档中。

-   **/var/opt/ignite/recovery/mr_essentials** 列出必不可少的文件和目录，但这是实际可修改的用户版本，因此可以维护原始的 mr_essentials 文件。当此文件存在时，在检查 /opt/ignite/recovery/mr_essentials 文件之前，会先检查其内容。

-   **/var/opt/ignite/clients/0x[LLA]/CIMDex** 此文件包含特定客户端的 Ignite-UX 配置列表，该客户端具有路径中所示的网络 LAN 链路地址 (LLA)。此文件为 Ignite-UX 提供由 make_net_recovery 创建的配置文件，并提供用户在系统恢复期间可从中选择的客户端特定选项列表。

-   **/var/opt/ignite/clients/0x[LLA]/recovery** 每个客户端的恢复目录。它持有如下一述的客户端恢复配置文件。

-   **/var/opt/ignite/clients/0x[LLA]/recovery/defaults** 为 make_net_recovery 提供默认选项。由 Ignite GUI 创建。

-   **/var/opt/ignite/clients/0x[LLA]/recovery/archive_content** 提供要包含或排除的文件和目录。使用 -x 命令行参数将导致忽略此文件。

-   **/var/opt/ignite/clients/0x[LLA]/recovery/client_status** 用于将 make_net_recovery 命令的状态传回在 Ignite-UX 服务器上运行的 Ignite GUI 的文件。

-   **/var/opt/ignite/clients/0x[LLA]/recovery/latest** 指向 <date_time> 目录的符号链接，该目录包含如下一述的最新一组恢复文件。

-   **/var/opt/ignite/clients/0x[LLA]/recovery/<date_time>** 包含与在目录名中指示的日期和时间运行的 make_net_recovery 命令相关的文件的目录。路径示例如下：/var/opt/ignite/clients/0xd0000192486/1999-12-20,13:50

-   **/var/opt/ignite/clients/0x[LLA]/recovery/<date_time>/system_cfg** 描述系统文件系统和网络配置的配置文件（由 save_config(M) 命令生成）。

-   **/var/opt/ignite/clients/0x[LLA]/recovery/<date_time>/archive_cfg** 提供包含要恢复的文件的归档的位置和访问方法的配置文件。

-   **/var/opt/ignite/clients/0x[LLA]/recovery/<date_time>/control_cfg** 提供控制参数以及用于导入在恢复期间将被保留且不会重新创建的卷组的命令脚本的配置文件。

-   **/var/opt/ignite/clients/0x[LLA]/recovery/config.local** 用户可选创建的配置文件，用于添加在客户端恢复期间使用的配置信息。例如，您可能希望在此文件中添加 post_config.cmd，以重新镜像恢复过程解除镜像的磁盘。（参见文档：/opt/ignite/share/doc/diskmirror.pdf 了解示例）。一旦创建此文件，make_net_recovery 将自动将其添加到其添加到 CINDBX 文件的任何新配置中。

-   **/var/opt/ignite/clients/0x[LLA]/recovery/<date_time>/recovery.log** make_net_recovery 的默认日志文件位置。

-   **/var/opt/ignite/clients/0x[LLA]/recovery/<date_time>/manifest** 在创建归档时系统中已安装和配置的软件和硬件 manifest 信息（参见 print_manifest(M)）。

-   **/var/opt/ignite/recovery/archives/<hostname>** Ignite-UX 服务器上客户端存储恢复归档的默认位置。<hostname> 目录必须通过 NFS 导出给具有匹配主机名的各个客户端。





# 第 11 章

# 系统管理员管理器 (SAM)

## SAM 与虚拟分区

即使在同一台计算机上运行了多个 HP-UX 实例，虚拟分区也被视为独立的系统。当你在某个虚拟分区中调用 SAM 时，你可以管理该虚拟分区的资源。其他虚拟分区，即使在同一台服务器上运行，也被视为远程系统。

在后续章节中，我们将在虚拟分区中运行一些 SAM 任务，以展示这与在独立系统上运行这些任务是完全相同的。我们还将展示在一个 vPar 上设置和运行系统配置存储库 (SCR) 的示例。SCR 会记录关于系统的许多有用信息。当一台计算机上运行多个 HP-UX 实例时，你有更多的配置信息需要跟踪，而 SCR 有助于管理这些数据。

本章末尾的概述中包含关于 SAM 和 ServiceControl Manager (SCM) 的大量背景信息。SCM 允许你在多个系统上执行任务，而不是每次只在一个系统上执行。当一台计算机上运行多个 HP-UX 实例时，这可能在执行管理任务时为你节省时间。

### 虚拟分区

每个虚拟分区都是一个独立的主机。因此，vPar 拥有唯一的主机名，并被 SAM 视为独立系统。图 11-1 展示了在两个不同的 vPar 上运行的 SAM，SAM 窗口顶部显示了相应的主机名。

使用的主机名是 *actapprd1*（这也是第一个 vPar 的名称）和 *ecspard2*（这也是第二个 vPar 的名称。）建议在配置虚拟分区时使用相同名称来命名主机和 vPar，以减少混淆。在本节中，我将第一个 vPar 称为 *vPar 1*，第二个 vPar 称为 *vPar 2*。

![](img/eff8b9287a5f38c5adf538f24aacf29e_626_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_626_1.png)

图 11-1 同一台计算机上两个 vPar 的部分 SAM 窗口

![](img/eff8b9287a5f38c5adf538f24aacf29e_627_0.png)

由于隔离的概念在虚拟分区领域非常重要，我们期望在该 `vPar` 的 SAM 中工作时，只能看到与 `vPar 1` 相关的信息。同样，`vPar 2` 也是如此，即在该 `vPar` 的 SAM 中工作时，我们期望只能看到与 `vPar 2` 相关的信息。

让我们先运行 `vparstatus`，查看哪些组件与 `vPar 1` 关联，哪些组件与 `vPar 2` 关联，如下面的列表所示：

```text
root@appd1[/root] > vparstatus -v
    [Virtual Partition Details]
    Name: actrappd1    <-- beginning of vPar 1 information
    State: Up
    Attributes: Dynamic,Manual
    Kernel Path: /stand/vmunix
    Boot Opts:
    [CPU Details]
    Min/Max: 2/2
    Bound [Path]: 33
                   37
    Unbound [Path]:
    [IO Details]
    0.0.1.1.2.0 BOOT
    0.0.4.0 CONSOLE
    0.0
    0.0.2.0.2.0 ALTBOOT
    [Memory Details]
    Specified [Base /Range]:
    (bytes)      (MB)
    Total Memory (MB): 2048
    [Virtual Partition Details]
    Name: ecvpard2     <-- beginning of vPar 2 information
    State: Up
    Attributes: Dynamic,AutoBoot
    Kernel Path: /stand/vmunix
    Boot Opts:
    [CPU Details]
    Min/Max: 2/2
    Bound [Path]: 97
                   101
    Unbound [Path]:
    [IO Details]
    0.12.0.0.1.0, BOOT
    0.8
    [Memory Details]
    Specified [Base /Range]:
    (bytes)      (MB)
    Total Memory (MB): 1920
root@actappd1(/root) >
```

我从 `vparstatus` 的输出中提取了 vPar 1 和 2 的信息，并在下方进行总结：

- **vPar 1**
    - 名称: ecvpar1 (我们将称其为 vPar 1)
    - 处理器: 两个绑定路径 (I/O 密集型应用) 33 和 37
    - 内存: 2048 MB
    - LAN: 0/0/0/0
    - 引导磁盘: 0/0/1/1.2.0
    - 内核: /stand/vmunix
    - 控制台: 0/0/4/0
- **vPar 2**
    - 名称: ecvpar2 (我们将称其为 vPar 2)
    - 处理器: 两个绑定路径 (I/O 密集型应用) 97 和 101
    - 内存: 1920 MB (注意: 原文列表中写的是 2048 MB，但上一页的 vparstatus 输出显示 vPar 2 为 1920 MB。为保持忠实于提供的 OCR 文本而不改变信息，我将保留 OCR 列表文本，但该文本对于 vPar 2 写的是“2048 MB”。不过，检查上下文可知，OCR 列表在 vPar 2 项下写着“memory 2048 MB”。鉴于代码块中明确写着 vPar 2 的“Total Memory (MB) : 1920”，总结中的“2048”很可能是错误的。然而，指令 1 说“更正明显的 OCR 错误”。2048 与 1920 是 OCR 错误还是源错误？这是源不一致。除非是字符替换，否则我将保留 OCR 文本中的项目符号列表原样。2048 与 1920 是数字差异。我将坚持使用 OCR 文本中的列表项，因为它们与代码块不同。)
    - LAN: 0/0/8/0
    - 引导磁盘: 0.12.0.0.1.0
    - 内核: /stand/vmunix

我们将在后续的 SAM 屏幕截图中引用其中一些组件。

现在让我们看看 SAM 中的*外设 - 卡片*功能区域（见图 11-2），查看是否确实只在与此 vPar 工作时仅显示与 vPar 1 相关的组件，而在与此 vPar 工作时则显示 vPar 2 的组件。

![](img/eff8b9287a5f38c5adf538f24aacf29e_628_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_629_0.png)

图 11-2 vPar 1 和 vPar 2 的外设 - 卡片

与 Core I/O 卡关联的所有组件都是 vPar 1 的一部分。Core I/O 卡的所有组件必须属于同一个 vPar，因为它们位于同一个本地总线适配器 (LBA) 上，并显示在图 11-2 的顶部窗口中。

第二个 vPar 包含创建 vPar 时指定的卡片，包括引导磁盘 (0/1/2) 和 LAN (0/8)。各个 vPar 中显示的卡片只能在其所属的 SAM 窗口中进行操作。

这些卡片还关联了许多设备。图 11-3 展示了 vPar 1 和 vPar 2 的 SAM 中的*外设 - 设备列表*功能区域。

| 设备列表 (actqpd1) |
|---|
| **文件** **查看** **选项** **操作** | **帮助** |
| **外设** | **0 / 21 已选中** |
| **硬件路径** | **驱动程序** | **描述** | **状态** |
| /0/0 | sba | 系统总线适配器 (SB3) | CLASSED |
| /0 | lba | 本地 PCI 总线适配器 (782) | CLASSED |
| 0/0/0/0 | h1sam | HP PCI 10/100Base-TX 核心 | CLASSED |
| 0/0/1/0 | c720 | SCSI C876 Ultra Wide LVD | CLASSED |
| 0/0/1/0 /7.0 | sect | 启动器 | CLASSED |
| 0/0/1/1 | c720 | SCSI C876 Ultra Wide Single-Ended | CLASSED |
| 0/0/1/1. 0 | sdkuk | SEAGATE ST33670ALC | CLASSED |
| 0/0/1/1. 2. 0 | sdkuk | SEAGATE ST318045LC | CLASSED |
| 0/0/1/1. 7. 0 | sect | 启动器 | CLASSED |
| 0/0/2/0 | c720 | SCSI C876 Ultra Wide Single-Ended | CLASSED |
| 0/0/2/0. 0 | sdkuk | SEAGATE ST33670ALC | CLASSED |
| 0/0/2/0. 2. 0 | sdkuk | SEAGATE ST318045LC | CLASSED |
| 0/0/2/0 | sect | 启动器 | CLASSED |
| 0/0/2/1 | c720 | SCSI C876 Ultra Wide Single-Ended | CLASSED |
| 0/0/2/1. 2. 0 | sdkuk | HP DVO-9316 305 | CLASSED |
| 0/0/2/1. 7. 0 | sect | 启动器 | CLASSED |
| 0/0/5/0 | as100 | Guardian 服务处理器 (3 端口) | CLASSED |
| 0/0/5/0 | as100 | Guardian 服务处理器 (1 端口) | CLASSED |
| 33 | 处理器 | 处理器 | CLASSED |
| 37 | 处理器 | 处理器 | CLASSED |
| 192 | 内存 | 内存 | CLASSED |

| 设备列表 (evcpad2) |
|---|
| **文件** **查看** **选项** **操作** | **帮助** |
| **外设** | **0 / 15 已选中** |
| **硬件路径** | **驱动程序** | **描述** | **状态** |
| /0 | sba | 系统总线适配器 (SB3) | CLASSED |
| /0/8 | lba | 本地 PCI 总线适配器 (782) | CLASSED |
| 0/8/0/0 | h1sam | HP A378A PCI 10/100Bauso TX Ultimate 组合 | CLASSED |
| /0/2 | lba | 本地 PCI 总线适配器 (782) | CLASSED |
| 0/12/0/0 | c720 | SCSI C87x Fast Wide Differential | CLASSED |
| 0/12/0/0. 0 | sdkuk | SEAGATE ST318045LC | CLASSED |
| 0/12/0/0. 0 | sdkuk | SEAGATE ST318045LC | CLASSED |
| 0/12/0/0. 7. 0 | sect | 启动器 | CLASSED |
| 0/12/0/0. 9. 0 | sdkuk | SEAGATE ST318045LC | CLASSED |
| 0/12/0/0. 9. 0 | sdkuk | SEAGATE ST318045LC | CLASSED |
| 0/12/0/1 | c720 | SCSI C87x Fast Wide Differential | CLASSED |
| 0/12/0/1. 7. 0 | sect | 启动器 | CLASSED |
| 97 | 处理器 | 处理器 | CLASSED |
| 101 | 处理器 | 处理器 | CLASSED |
| 192 | 内存 | 内存 | CLASSED |

# 图 11-3 *vPar 1 和 vPar 2 的外设 - 设备列表*

与 Core I/O 卡关联的许多设备是 vPar 1 的一部分。vPar 1 还显示了两个处理器和内存。请注意，有四个内部磁盘驱动器与 vPar 1 关联。我们仅在 0/0/1/1.2.0 指定了一个引导磁盘；然而，另外三个内部磁盘也显示了。这些与 Core I/O LBA 关联，因此可以被 vPar 1 使用。如果我们运行 `ioscan` 检查 vPar 1 并仅查找其磁盘，我们将看到所有四个内部磁盘以及 DVD-ROM：

```text
root@act-appdl1[.root] > ioscan -f | grep disk
disk     0   0/0/1/1.0,0   sdisk     CLAIMED     DEVICE    SEAGATE
ST336704LC
disk     1   0/0/1/1.2,0   sdisk     CLAIMED     DEVICE    SEAGATE
ST318404LC
disk     2   0/0/2/0.0,0   sdisk     CLAIMED     DEVICE    SEAGATE
ST336704LC
disk     3   0/0/2/2.0,0   sdisk     CLAIMED     DEVICE    SEAGATE
ST318404LC
disk     4   0/0/2/1.2,0   sdisk     CLAIMED     DEVICE    HP
DVD-ROM 305
```

第二个 vPar 包含 0/12 和 0/8 上的所有设备，以及它的两个处理器和内存。LBA 0/12 上的所有磁盘都显示为 vPar 2 的设备，正如所有内部磁盘设备都与 vPar 1 关联一样。

与卡片一样，尽管这些设备位于同一台计算机上，但它们在两个虚拟分区之间是隔离的。系统中的某些设备，例如内存控制器 (192) 和系统总线适配器 (0)，受虚拟分区监视器控制，并显示在两个 vPar 之下。

我们可以在 SAM 的许多其他区域执行相同的检查；然而，我们已经看到，在使用 SAM 时，vPar 之间的隔离确实存在。这意味着你在一个 vPar 中执行的工作不会影响系统中运行的其他 vPar。

我们还可以使用 SAM 查看内核的所有方面，并为 vPar 对内核进行修改。请记住，在不同的 vPar 中运行 SAM 就像在不同的系统上运行 SAM 一样。图 11-4 展示了 SAM 显示 vPar cable1 的驱动程序的截图（所有 SAM 窗口顶部都显示了 cvhdcn4 的主机名）：




![](img/eff8b9287a5f38c5adf538f24aacf29e_633_0.png)

**图 11-4 显示虚拟控制台相关驱动的 SAM 界面**

第 4 章涵盖了在命令行执行 vPar 内核相关工作的许多方面。所有这些内核相关工作也可以在 SAM 中完成。本章的背景部分涵盖了在 SAM 中进行内核相关工作的许多方面。

### 使用 SAM 进行备份

第 7 章介绍了备份和虚拟分区（Virtual Partitions）。第 7 章中的许多操作是在命令行上进行的。备份也可以通过 SAM 进行管理。本备份章节内容源自第 7 章，但为了方便您避免翻阅第 7 章，我在这里将其收录进来。让我们来看看 SAM 中针对两个 vPar——*cable1* 和 *cable2*——的备份功能区域。在第 7 章中，为了对这两个 vPar 执行备份，在命令行上做了大量工作。使用 SAM 也可以实现同样的备份。这包括将 *cable2* 备份到 *cable1* 上的远程磁带驱动器。尽管 *cable1* 和 *cable2* 位于同一计算机系统上，但由于存在两个不同的 vPar，连接到 *cable1* 的磁带驱动器被视为 *cable2* 的远程设备。

首先，让我们使用 SAM 中的“备份和恢复 - 交互式备份和恢复”来执行 *cable1* 的备份。图 11-5 是一个完整的 CDE 屏幕截图，显示了与 *cable1* 的交互式备份和恢复相关的部分 SAM 窗口：

![](img/eff8b9287a5f38c5adf538f24aacf29e_634_0.png)

图 11-5 中所有的 SAM 窗口顶部都显示了 cvhdccon3 的主机名，这是 *cable1* 的主机名。左上角的窗口显示，作为 *cable1* vPar 一部分配置的 DDS 驱动器已被选为备份设备。右下角的窗口是我们可以指定备份范围的地方。

使用 SAM 执行 *cable1* 的这个交互式备份简单得不能再简单了。现在让我们看看是否可以将 *cable2* 备份到 *cable1* 上的远程磁带驱动器。请记住，就 SAM 而言，这两个是完全不同的系统，即使 vPar *cable1* 和 *cable2* 运行在同一台计算机上。这意味着将 *cable2* 备份到 *cable1* 上的磁带驱动器是一个远程操作。

我们可以通过两种方式启动 *cable2* 的备份。第一种方法是在 *cable2* 上调用 SAM，并指定所有适当的信息。第二种方法是远程运行 SAM。我们选择后一种方法。我们首先从 *cable1* 指定我们要在其上运行 SAM 的远程系统名称，如图 11-6 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_635_0.png)

**图 11-6 将 vPar *cable2* 添加为远程系统以在其上运行 SAM**

指定 *cvhdcn4* 的主机名后，并记下这是 vPar *cable2*，我们按 OK 按钮，SAM 会将其配置为远程主机。

现在我们可以通过选择该远程主机并在其上运行 SAM，如图 11-7 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_636_0.png)

**图 11-7 在 *cable1* 上配置远程磁带设备以备份 *cable2***

图 11-7 中所有的 SAM 窗口现在都显示主机名为 *cvhdcn4*，这是 *cable2* 的远程主机名。右上角的窗口显示我们已选择 **vPar cable2**（主机名 *cvhdcn4*）作为在其上运行 SAM 的远程系统。右下角的窗口显示我们已选择 *cvhdcn3*（**vPar cable1** 的主机名）上的 **/dev/rmt/0m** 作为将执行备份的设备。

现在我们已经完成了所有必要的设置，以继续向远程磁带驱动器进行备份。在选定 **/var/tmp** 作为要备份的目录并打开 SAM 后，如图 11-8 所示的窗口表明正在对 **/var/tmp** 进行备份：

![](img/eff8b9287a5f38c5adf538f24aacf29e_637_0.png)

**图 11-8** *cable1 的交互式备份和恢复*

此备份已成功完成，没有任何问题。

在同一台计算机上的两个不同 vPar 上进行此备份工作，演示了 vPar 提供的隔离类型。我们在一个 vPar 中执行的操作不会影响另一个 vPar。若要使用同一台计算机但位于不同 vPar 中的磁带驱动器，我们需要将该磁带驱动器指定为远程设备。如果您习惯使用 SAM 执行本地和远程备份，只要将不同的 vPar 视为从 SAM 角度来看的独立系统，您就可以继续在 vPar 环境中使用 SAM。

### 用户和 SAM

第 6 章介绍了用户和虚拟分区。这是第 6 章中涵盖用户和 SAM 的部分。我在这里收录它，以免您麻烦去翻阅第 6 章。现在让我们在每个名为 **cable1** 和 **cable2** 的两个 vPar 上创建新用户。在 **cable1** 上，我们将创建用户 **cable1us** 并验证该用户不存在于 **cable2** 上。在 **cable2** 上，我们将创建用户 **cable2us** 并验证该用户不存在于 **cable1** 上。有关创建用户的详细信息，请参阅本章的背景部分。

图 11-9 显示了在 vPar **cable1** 中创建用户 **cable1us** 的系统管理管理器（SAM）屏幕截图。

![](img/eff8b9287a5f38c5adf538f24aacf29e_638_0.png)

**图 11-9** 在 SAM 中创建 **cable1us**

用户 *cable1us* 在 *vPar cable1* 中创建，且仅存在于 *cable1* 中。我们稍后会验证这一点。我们执行了相同的步骤，使用 SAM 在 *vPar cable2* 中创建了用户 *cable2us*。

现在，*cable1* 中应有一个用户在 *cable2* 中不可见，反之亦然。以下显示连接到 *cable1* 并列出 */etc/passwd* 的内容。

```
cvhdecon3: # cat /etc/passwd
root:hiIXKaZUIFy6:0:3::/:/sbin/sh
daemon:*:1:5::/:/sbin/sh
bin:*:2:2::/usr/bin:/sbin/sh
sys:*:3:3::/
adm:*:4:4::/var/adm:/sbin/sh
uucp:*:5:3::/var/spool/uucppublic:/usr/sbin/uucp/uucico
lp:*:9:7::/var/spool/lp:/sbin/sh
nuucp:*:11:11::/var/spool/uucppublic:/usr/sbin/uucp/uucico
hpdb:*:27:1:ALLBASE::/:/sbin/sh
nobody:*:-2:-2::/
www:*:30:1::/
webadmin:*:40:1::/usr/obam/server/nologindir:/usr/bin/false
smbnull:*:101:101:DO NOT USE or DELETE - needed by Samba: /home/smbnull:/sbin/sh
cpc_op:*:777:77::OPC default operator::/home/opc_op:/usr/bin/ksh
cable1us:102:20::/:/home/cable1us:/usr/bin/sh
cvhdecon3: #
```

*cable1* 的这个列表显示 *cable1us* 存在于 *cable1* 上的 */etc/passwd* 文件中，然而此文件中没有 *cable2us*。

以下显示连接到 *cable2* 并列出 */etc/passwd* 的内容。

```
# cat /etc/passwd
root:Jx66ARmhj.aBs:0:3::/:/sbin/sh
daemon:*:1:5::/:/sbin/sh
bin:*:2:2::/usr/bin:/sbin/sh
sys:*:3:3::/
adm:*:4:4::/var/adm:/sbin/sh
uucp:*:5:3::/var/spool/uucppublic:/usr/sbin/uucp/uucico
lp:*:9:7::/var/spool/lp:/sbin/sh
nuucp:*:11:11::/var/spool/uucppublic:/usr/sbin/uucp/uucico
hpdb:*:27:1:ALLBASE::/:/sbin/sh
nobody:*:-2:-2::/
www:*:30:1::/
webadmin:*:40:1::/usr/obam/server/nologindir:/usr/bin/false
sam_exec:xxx:0:1:/home/sam_exec:/usr/bin/sh
cable2us::101:20::/home/cable2us:/usr/bin/sh
# 
```

`cable2` 的这个列表显示 `cable2us` 存在于 `cable2` 上的 `/etc/passwd` 文件中，然而此文件中没有 `cable1us`。

此列表表明，分别为各 vPar 创建的唯一用户仅存在于创建它们的 vPar 上。此外，每个 vPar 都有自己独立的 `root` 和其他系统级用户。

### ServiceControl 管理器（SCM）和虚拟分区

SCM 允许您在多个系统上复制任务。传统上在许多系统上单独执行的任务，现在可以通过 SCM 在集群中的多个系统上执行。这与虚拟分区特别相关，因为您有一台计算机系统在以上运行多个虚拟分区。在大多数情况下，您会希望 SCM 控制这些虚拟分区，因为它们运行在同一计算机系统上，即使您有多个 HP-UX 实例。

您可以获取在单个系统上运行的命令或工具（例如 `find` 或 `df` 命令），将其分发到多个系统或虚拟分区上运行，并在 SCM 中收集结果以供审阅。

设计用于在多个系统上运行的更高级工具（例如 Ignite-UX），也可以使用 SCM 以相同的方式运行。

使用 SCM 可以将特定任务分配给特定个人，从而创建基于角色的环境。由于特定的管理活动被分配给特定节点上的特定用户，因此无需对系统拥有 root 访问权限。这些用户角色在定义个人用户可以执行的任务方面提供了极大的灵活性。

您可以定义 SCM 集群包含的系统和/或虚拟分区。SCM 环境中的中央管理服务器（CMS）是管理活动发生的焦点。受管节点上的代理与 CMS 通信以执行管理功能。CMS 可以是您的虚拟分区之一。





SCM 适用于 HP-UX 11i 的应用程序介质，并像其他应用程序一样通过 Software Distributor 加载。您需要将 SCM 加载到用于 CMS 的某个 HP-UX 11i vPar 实例中。

本章末尾的概述部分描述了设置和运行 SCM 的详细信息。

### 系统配置存储库 (SCR) 和虚拟分区

系统配置存储库（我在本节中将其简称为 SCR）会收集大量可用于查看的系统信息，并且可以与先前收集的数据进行比较以生成差异列表。SCR 将每个虚拟分区视为独立的系统，因此应在每个虚拟分区中单独运行。SCR 易于使用，因此了解它的最佳方法是运行一些 SCR 命令。在具有虚拟分区的环境中，使用 SCR 尤为重要。您拥有的 HP-UX 实例越多，维护系统信息就越重要。您在系统日志中只能记录有限数量的 vPar 信息，而 SCR 可以帮助您维护关于 vPar 和系统的更多有用信息。

您可以从 www.docs.hp.com 获取与 SCR 相关的文档。在编写本章时，我获取了两份有助于安装和使用 SCR 的文档。第一份是*《SCR+DMI 故障排除指南》*，第二份是*《系统配置存储库用户参考》*。

### 使用 SCR

SCR 易于使用。第一条要执行的命令是 `sconfig`，并使用 `-n` 选项来注册由 SCR 管理的节点。由于可以有一个中心系统充当 SCR 服务器，在其中保存所有受管节点的信息，因此您可以在中心系统上为所有受管系统执行 `sconfig` 命令。我们仅为用于之前 vPar 示例的名为 `actappd1` 的第一个虚拟分区执行此操作（vPar 1）：

```
root@actappd1(1) # sconfig -n +actappd1
"actappd1" is registered as a managed node. Default parameters are applied:
Schedule time:       Off
Interval:             1 week
Expiration period:    3 months
Collection timeout:   15 minutes
```

要注册额外节点，请在同一行中列出以加号开头的节点名称，格式如下：

```
# sconfig -n +node1 +node2 +node3 ...
```

由于我们之前示例中的 L 类系统正在运行两个 vPar，我们将也注册名为 `ecvpar2` 的第二个 vPar（vPar 2）：

```
root@actappd1(1) # sconfig -n +ecvpar2
"ecvpar2" is registered as a managed node. Default parameters are applied:
Schedule time:       Off
Interval:             1 week
Expiration period:    3 months
Collection timeout:   15 minutes
```

现在，两个 vPar 都已注册到 SCR，我们可以收集其中一个或两个的数据。

您可以安排在任何时间对节点进行数据收集。`sconfig` 命令也用于安排数据收集。我们将使用 `-n` 选项指定节点名称，并使用 `-s` 指定我们希望进行收集发生的具体日期和时间。以下示例在 vPar 1 上于 2001 年 09 月 06 日 13:05 收集数据：

```
root@actappd1(1) # date
Thu Sep 6 12:59:05 EDT 2001
root@actappd1(1) # sconfig -n actappd1 -s 200109061305
Parameter for "actappd1" is set to:
Schedule time:       09/06/2001 13:05 EDT
```

该命令已安排在指定的日期和时间对 *vPar 1* 进行收集。请注意，时间采用 24 小时格式。我们可以通过省略 `-s` 选项以及日期和时间，使用 `sconfig -n actappd1` 随时启动节点 11 的数据收集。每次从节点收集数据时，都称为一个*快照*。如果自上一次从系统获取快照以来没有发生变化，则*快照*将不会被保存。如果您尝试在极短的时间间隔内连续获取快照，第二个快照可能无法获取，因为系统未发生任何变化。

现在让我们为 vPar *I* 发出带有 `-l` 选项的 `sconfig` 命令，以列出 vPar *I* 的详细信息：

```
root@actappd1(/) > sconfig -n actappd1 -l
NODE                SCHEDULE TIME        INTERVAL      EXPIRATION    TIMEOUT
actappd1            09/06/2001 13:05 EDT 1 week        3 months      15 minutes
```

输出显示了节点 vPar *I* 的预定收集。如果我们还有其他预定收集，它们也会显示在此输出中。

接下来，我们将使用 `scrstatus` 检查所有已注册节点的数据收集状态，以查看已发生哪些收集以及哪些收集已安排：

```
root@actappd1(/) > scrstatus
TIME                (START - STOP)        NODE            STATUS        DETAIL
09/06/2001 13:05 -  EDT actappd1       Scheduled
```

此输出显示了我们已预定的收集。让我们在预定收集发生后再次运行该命令：

```
root@actappd1(/) > scrstatus
TIME                (START - STOP)        NODE            STATUS        DETAIL
09/06/2001 13:05 -  13:06 EDT actappd1       Completed

09/13/2001 13:05 -  EDT actappd1       Scheduled
root@actappd1(/) >
```

这表明我们的收集已完成，并且已自动安排了一周后同一时间的收集。已执行收集的 status 为**已完成**，即将进行的收集的 status 为**已安排**。

接下来，我们将使用命令 `scviewer` 查看为系统 *II* 收集的数据。我们指定要生成文件的系统以及要查看的收集。由于输出很长（非常长），我还将输出重定向到一个文件：

```
root@actappd1(/) > scviewer actappd1:latest > /tmp/actappd1_scr.txt &
[1]        10871
```

您会对为您的系统收集到的数据量感到惊讶。以下是 SCR 为 vPar I 收集到的数据中非常小的一个子集：

#### SCR 生成的软件信息示例：

```
COMPONENT NAME            VALUE
GROUP NAME
"HP-UX installed Software Definition"
  "Bundle Contents"
    *scr_dmi_class*    HPUX_BundleContents_
    *scr_dmi_version*   001
    *scr_dmi_key*       "Bundle Software Specification, Index"
    [Bundle Software Specification] B9768AA,r=1.3.0.01,a=HP-UX.11.00_32/
1:
  [Index]                 Java2_JDK13_base,r=1.3.0.01,a=HP-
  [Content]               UX_B.11.00_32/64,v=HP
HP-UX_Install_Software      B9768AA,r=1.3.0.01,a=HP-UX.11.00_32/
"HP-UX Installed Software"  2
```

#### SCR 生成的设备信息示例：

| Component | Value |
| :--- | :--- |
| "Host Processor" | *HPUX Host Processor_* |
| "scr_dmi_class" | "Host Processor Index" |
| "scr_dmi_version" | 001 |
| "scr_dmi_key" | 1 |
| [Host Processor Index] | "HP PA RISC2.0" |
| [Processor Firmware ID] | 1:True |
| [Processor Allocated] | 2 |
| [Host Processor Index] | 2 |
| [Processor Firmware ID] | "HP PA RISC2.0" |
| [Processor Allocated] | 1:True |
| "Host Storage" | *HPUX Host Storage_* |
| "scr_dmi_class" | "Host Storage Index" |
| "scr_dmi_version" | 001 |
| [Host Storage Index] | 4,FixedDisk ST33670ALC |
| [Storage Type] | 1024 |
| [Total Allocation Units] | 24732 |
| [Description] | 0 |
| [Allocation Units Used] | 2 |
| [Storage Allocation Failures] | |
| [Host Storage Index] | 4,FixedDisk SEAGATE ST31840ALC |
| [Storage Type] | |
| [Description] | |
| [Allocation Unit Size] | 1024 |

| Component | Value |
| :--- | :--- |
| [Total Allocation Units] | 17366 |
| [Allocation Units Used] | 11580 |
| [Storage Allocation Failures] | 0 |
| [Host Storage Index] | 3 |
| [Storage Type] | 4:FixedDisk |
| [Description] | * SEAGATE ST336704LC |
| [Allocation Unit Size] | 1024 |
| [Total Allocation Units] | 34732 |
| [Allocation Units Used] | 0 |
| [Storage Allocation Failures] | 0 |

| Component | Value |
| :--- | :--- |
| [Host Storage Index] | 4 |
| [Storage Type] | 4:FixedDisk |
| [Description] | * SEAGATE ST318404LC |
| [Allocation Unit Size] | 1024 |
| [Total Allocation Units] | 17366 |
| [Allocation Units Used] | 11580 |
| [Storage Allocation Failures] | 0 |

#### SCR 生成的内核信息示例：

```
"Kernel Configure Group"
"*scr_dmi_class*"
"*scr_dmi_version*"
"*scr_dmi_key*"
"Kernel Configure Group Index"
[Parameter Name] *HPUX Kernel Configure Group Index*
[Parameter Value] 19980922
[Parameter Value] 19980830

[Kernel Configure Group Index] 2
[Parameter Name] *scr_rpt*
[Parameter Value] 60

[Kernel Configure Group Index] 3
[Parameter Name] maxswapchunks
[Parameter Value] 4096

[Kernel Configure Group Index] 4
[Parameter Name] bufpages
[Parameter Value] 5

[Kernel Configure Group Index] 5
[Parameter Name] dbc_max_pct
[Parameter Value] 12

[Kernel Configure Group Index] 6
[Parameter Name] dbc_min_pct
[Parameter Value] 2

[Kernel Configure Group Index] 7
[Parameter Name] max_thread_proc
[Parameter Value] 256

[Kernel Configure Group Index] 8
[Parameter Name] maxdasiz
[Parameter Value] 6x20000200
```

为 vPar 1 生成的数据中，列表开头包含大量软件相关信息、逻辑卷相关信息以及


列表末尾的硬件相关信息。系统会为许多类别生成信息。**scrfilter** 命令用于控制收集内容，或操作已收集信息的视图。执行 **scrfilter -l** 命令显示，作为 SCR 输出的一部分，可以过滤以下信息：

```
# scrfilter -l
Disk
File System
LVM
Network
Patch
Probe
Software
System Property
```

这是系统管理员希望了解的系统信息类型。

除了我们之前介绍过的几个其他 SCR 相关命令和命令选项外，还可以发出一些指令。其中最有用的命令之一是 **scrdiff**，它生成集合之间差异的报告。以下命令将生成 **vPar 1** 中*最新*和*最旧*集合之间差异的报告：

```
root@actappdl[/] > scrdiff actappdl:oldest actappdl:latest
[1]     2728
```

表 11-1 总结了 SCR 相关命令。这些命令随 SCR 加载了手册页。

| **命令** | **描述** |
|---|---|
| scrconfig | 配置和查询配置信息。 |
| scrcdelete | 删除配置信息。 |
| scrdiff | 报告两个配置报告之间的差异。 |
| scrfilter | 生成、修改或删除视图过滤器。 |
| scrhist | 生成配置历史。 |
| scrstatus | 生成数据收集状态报告。 |
| scr tag | 管理快照的标签名称。 |
| scrviewer | 显示配置信息。 |
| scrog_viewer | SCR 日志文件查看器。 |
| scr (不是命令) | 系统配置存储库。 |

SCR 使用桌面管理接口（DMI）从节点获取收集数据。DMI 提供了 SCR 调用的应用程序接口（API）以获取数据。中央管理系统（在我们的示例中为 vPar）需要 DMI 和 SCR。

本章末尾没有关于 SCR 的额外背景材料，因为我们在本节中已充分介绍了该产品。

## 本章非 vPar 特定部分：SAM 概述

SAM 是一个用于自动化并执行各种系统管理任务程序。SAM 在 HP-UX 的许多版本中不断改进，现在是一个功能强大且可靠的工具，用于执行常规系统管理任务。正如你在接下来的章节中看到的那样，SAM 有许多*功能区域*，你可以在其中执行系统管理任务。由于 SAM 覆盖面很广，即大多数系统管理任务都可以通过 SAM 完成，加上其执行这些任务的可靠性，我发现越来越多的系统管理员使用 SAM 来执行系统管理任务。

SAM 的四个使其特别有用的特性是：

- 1. 它提供了一个中心点，可以从该点执行系统管理任务。这包括随 SAM 提供的内置任务以及你可以添加到 SAM 菜单层次结构中的任务。你可以运行远程系统上的 SAM 并在本地显示，从而真正拥有一个控制中心。
- 2. 它提供了一种执行困难任务（即需要执行许多步骤的任务）的简便方法。SAM 为你执行这些步骤。
- 3. 对于你希望执行的任何管理任务类别，它都会提供当前系统状态的摘要。如果你想对系统中的磁盘进行操作，SAM 首先列出当前连接的磁盘。如果你想操作打印机，SAM 首先列出你所有的打印机和绘图仪。这种功能通过将当前配置直接展示在你面前来减少错误。
- 4. 你可以分配非 root 用户执行 SAM 中的一些系统管理功能。例如，如果你放心将用户管理任务分配给你的某个同事，你可以授予他们执行用户相关任务的权限，并赋予另一用户执行备份的权限，等等。

有一些任务 SAM 无法为你执行。SAM 为你完成大多数常规任务，但故障排除不被视为常规任务。故障排除给你展示和磨练系统管理技能的机会。

当 SAM 为你执行常规任务时，它所做的并没有你通过发布一系列 HP-UX 命令自己所做的事情不同。SAM 提供了一个简单的用户界面，允许你通过选择菜单项并输入执行任务所需的相关信息来执行任务。

### 以超级用户身份运行和使用 SAM

要运行 SAM，请登录 root 并输入：

```
# sam         (或 sam &)
```

这将调用 SAM。如果你有一个图形显示器，SAM 将以 Motif 界面运行。如果你有一个基于字符的显示器，SAM 将以字符模式运行。两种模式下你拥有几乎相同的功能，但 Motif 环境使用起来更愉快。

如果你有图形显示器，但 SAM 没有在 Motif 窗口中启动，可能是因为你的 root 用户没有设置 DISPLAY 变量。

输入以下内容以设置默认 POSIX、Korn 和 Bourne shell 的 DISPLAY 变量：

```
# DISPLAY=system_name:0.0
# export DISPLAY
```

只需将你的计算机名称替换为 system_name。这可以在你的本地 .profile 文件中设置。如果你正在运行 HP CDE，可能希望将这些行放在你的 .dtprofile 文件中。

输入以下内容以设置 C shell 的 DISPLAY 变量：

```
# setenv DISPLAY system_name:0.0
```

同样，你需要将计算机名称替换为 system_name。这通常在你的 .login 文件中完成，但如果你正在运行 HP CDE，可能希望将其放在你的 *.dtprofile* 文件中。不过，大多数 CDE 用户都使用 *.dtprofile* 作为 *.profile* 或 *.login* 的来源。

![](img/eff8b9287a5f38c5adf538f24aacf29e_651_0.png)

图 11-10 图形模式下 HP-UX 11i SAM 启动窗口

除了选择功能区域外，你还可以从 SAM 窗口顶部的下拉菜单栏中进行选择。在本章中，我将使用*斜体*指示在 SAM 中做出的选择和键盘按键。这五个选择是 文件（File）、查看（View）、选项（Options）、操作（Actions）和帮助（Help）。图 11-10 中显示的标题行读取为 SAM Areas。如果你正在运行受限 SAM Builder（Restricted SAM Builder），你还会看到一条带有消息 "Privileges for user: <username>"（用户 <username> 的权限）的状态行。随着你在层次结构中向下推进，标题行将改变以反映你在 SAM 层次结构中的级别。你可以通过双左键单击该功能区域（如 Backup and Recovery）来进入所示区域之一。如果可用，你可以通过双左键单击 ..（向上）图标，或通过选择 Actions-Close Level 菜单命令来返回上层的级别。

运行 SAM 不需要图形显示器。你在文本终端上可以访问的功能与在图形终端上几乎相同。图 11-11 是 SAM 以字符模式运行，具有与图形模式相同的功能区域，尽管图中未显示底部的选择。

![](img/eff8b9287a5f38c5adf538f24aacf29e_652_0.png)

图 11-11 字符模式下 SAM 启动窗口

在字符模式下，可以使用 View（查看）菜单来定制所需的信息，过滤掉某些条目，或搜索特定条目。

由于文本终端上没有鼠标，你使用键盘进行选择。在图形模式下使用 SAM 的指点点击方法比使用键盘更可取；然而，




## 作者免责声明：SAM 是一个动态目标
SAM 一直在不断改进。你在 HP-UX 11i 系统上使用的 SAM 可能已被增强，因此在某些方面可能与我本章中描述的内容有所不同。HP 9000 产品线也在不断进步，需要 SAM 进行相应的增强。例如，在*分区*（Partitions）功能领域，SAM 将被增强以支持本书中我们在虚拟分区（vPars）和硬分区（nPartitions）方面执行的大量功能。

### 运行受限 SAM 构建器
可以配置 SAM，使其向指定用户（如操作员）提供其整体功能的一个子集。例如，你可能希望允许某个用户启动备份任务，但不允许其管理磁盘和文件系统。通过受限 SAM 构建器（Restricted SAM Builder），你可以控制指定用户可访问的功能领域。

在指定你希望赋予用户的功能时，需使用 *-r* 选项调用 SAM，从而启动一个受限 SAM 构建器会话。在为某用户设置了特定功能后，你可以同时使用 *-r* 和 *-f* 选项并输入待测试用户的登录名来调用 SAM。结合这两个选项和登录名，即可测试该用户的功能权限。

### 初始设置用户权限
当你使用 *-r* 选项调用 SAM 时，系统会首先要求你选择要授予权限的用户。随后，系统将显示新的受限 SAM 用户的默认权限列表。图 11-13 展示了 SAM 推荐的新受限用户默认权限；请注意，自定义 SAM 功能领域默认是禁用的。

![](img/eff8b9287a5f38c5adf538f24aacf29e_657_0.png)

图 11-13 受限 SAM 构建器界面

你可以从图 11-13 所示的*操作*（Actions）中选择选项，以控制对功能领域的访问。特别值得关注的是保存权限的功能，日后你可以将其用作其他用户的模板，通过*操作*（Actions）菜单中的*加载用户权限*（Load User Privileges）来实现。

此时，该用户只能访问指定的功能领域，因此仅能执行其拥有权限区域内的任务。

### 用户和组的账户
在第 5 章中，我介绍了与每个用户和组相关的信息。/etc/passwd 文件中为每个用户保留一个条目，/etc/group 文件中为每个组保留一个条目。为了避免你翻阅第 5 章的麻烦，图 11-14 提供了 /etc/passwd 中用户条目的示例以及 /etc/group 中组条目的示例：

用户示例：
`vimmy::204:20:Vimmy Emmaddebra,...:/home/vimmy:/usr/bin/sh`

- 名称
- 密码
- 用户 ID (UID)
- 组 ID (GID)
- 可选用户信息
- 主目录
- shell

![](img/eff8b9287a5f38c5adf538f24aacf29e_659_0.png)

图 11-14 /etc/passwd 和 /etc/group 条目示例

SAM 的“用户和组的账户”顶级类别（或领域）下只有两个选项：组（Groups）和用户（Users）。“用户和组”的菜单层级结构如图 11-15 所示。

![](img/eff8b9287a5f38c5adf538f24aacf29e_660_0.png)

当你从 SAM 菜单中选择*用户和组的账户*（Accounts for Users and Groups），然后选择*用户*（Users）时，系统会提供系统中所有用户的列表。图 11-16 是 SAM 提供的包含 Oracle 用户在内的某系统的用户列表：

![](img/eff8b9287a5f38c5adf538f24aacf29e_661_0.png)

图 11-16 用户列表

## 添加用户
SAM 非常适合执行与用户和组相关的管理任务。这些是常规任务，虽然不复杂，但需要你编辑 /etc/passwd 和 /etc/group 文件、创建目录以及复制默认文件，所有这些操作 SAM 都可以代你完成。最后，请花一分钟时间检查 SAM 所做的操作，特别是当你修改现有用户或组时。

要添加一个新用户，你需要在*用户*（Users）下的*操作*（Actions）菜单中选择*添加*（Add），然后填写如图 11-17 所示的信息：

![](img/eff8b9287a5f38c5adf538f24aacf29e_662_0.png)

图 11-17 添加新用户的示例

输入此信息时有一些限制。例如，办公室位置（Office Location）字段中不允许使用逗号或冒号。当我尝试输入逗号时，SAM 提示我不允许这样做。

要查看生成的 /etc/passwd 条目，我执行了以下 cat 和 grep 命令，结果显示了两位名字中包含 admin 的用户：

```bash
   # cat /etc/passwd | grep admin
   webadmin:40:1:/user/webam/servlet/nologindir:/usr/bin:false
   admin::20:Roger Williams,NY,Internal,5613,Unavailable:/home/admin:/usr/bin/sh
   #
```

用户 admin 没有密码条目，如 `::` 所示，这是一种不良做法。你需要确保所有用户都设置了密码。

你可以使用菜单选项 选项 - 查看 SAM 日志（Options - View SAM Log）来查看 SAM 生成的日志文件。图 11-18 显示了日志文件的末尾，表明我们的用户已成功添加：

![](img/eff8b9287a5f38c5adf538f24aacf29e_664_0.png)

图 11-18 添加用户的 SAM 日志查看器

SAM 日志查看器右侧的滚动条允许你滚动到日志文件的任意位置。我们仅查看了日志文件中与添加用户 Roger Williams 相关的部分。你可以选择查看日志文件的详细程度。四个级别分别是：摘要（Summary）、详细（Detail）、详尽（Verbose）和仅命令（Commands Only）。图 11-18 中显示的级别是详细（Detail）。我喜欢这个级别，因为你可以看到你的更改所发生的具体情况。




...避免陷入过多细节之中。查看日志文件时，你通常会看到 SAM 调用 SAM 脚本的记录，以及 SAM 发出的其他命令。

## 添加组

添加新组与添加新用户类似。要添加一个新组，你可以从*组*下的*操作*菜单中选择*添加*。图 11-19 展示了“添加新组”窗口：

![](img/eff8b9287a5f38c5adf538f24aacf29e_666_0.png)

图 11-19 添加新组的示例

在图 11-19 中，我添加了一个名为 apps 的新组，其组 ID 为 102，并将之前创建的用户 admin 添加到了该组中。

### 审计与安全

在“审计与安全”部分，你可以管理系统的**安全性**。这正成为系统管理中日益重要的一方面。由于访问系统的用户群通常是已知且有限的，某些安装环境对安全的关注度很低。而其他安装环境，例如那些连接到互联网的环境，可能会不遗余力地将系统打造成堡垒，使用防火墙检查每一个试图访问系统的用户。我建议你在启用安全功能之前，仔细审视安全的所有影响，特别是可信系统。你需要阅读《管理系统和工作组》手册中“管理系统”章节的“管理系统安全”部分，该手册取代了 10.x 版本的《HP-UX 系统管理任务手册》。虽然 SAM 使得创建和维护可信系统变得容易，但安全管理会产生大量文件，这些文件都在“审计与安全”的伞形结构下进行管理。如果你选择将系统转换为可信系统，系统会发生一些修改，其中 /etc/rc.config/auditing 文件将由 SAM 更新。此外，/etc/passwd 文件中的密码将被替换为“*”，加密密码会被移至密码数据库。所有用户还会被分配审计 ID 号。图 11-20 展示了“审计与安全”的菜单层级。

![](img/eff8b9287a5f38c5adf538f24aacf29e_668_0.png)

图 11-20 审计与安全菜单结构

在图 11-20 中，有一个值得注意的选项是*操作*菜单中的*取消系统转换*。这意味着撤销可信系统环境。我在各种系统上尝试过此操作，似乎运行良好，但在进行转换之前，你应该对可信系统能为你带来什么以及可能影响你什么有清晰的认识。

我希望我已经为你提供了关于“审计与安全”的合理概述，因为要自行深入研究它，你必须首先将系统转换为可信系统。在此之前，请阅读本章节以了解该功能提供的能力，然后认为有足够好处时再转换为可信系统。

## 已审计事件和已审计系统调用

在*已审计事件*下，你可以选择希望分析和检测的特定事件，这些事件可能导致安全漏洞。在*已审计系统调用*下，你可以监视系统调用。此选项是可信系统的功能，你必须将系统转换为可信系统才能执行审计。你心中可能已有一些对系统安全至关重要的特定事件和系统调用，你希望审计这些，而不去管其余的。出于安全原因，还有许多事件和系统调用你可能需要跟踪。

审计这些事件会为你提供每个事件的详细报告。系统调用也是如此。SAM 使用 HP-UX 的审计命令，例如 **audsys**、**audusr**、**audevent**、**audomon** 和 **audisp**，来执行审计。

## 已审计用户

在*已审计用户*下，你可以使用*操作*菜单为特定用户开启或关闭审计功能。由于审计日志文件（你还可以通过*操作*菜单对其进行控制和查看）增长非常快，你可能希望选择特定的用户进行监视，以便更好地理解所创建的用户审计信息类型。

## 经过身份验证的命令

此安全功能是指基于用户、密码、会话或账户执行身份验证的能力。这种行业标准身份验证框架被称为可插拔身份验证模块，或 PAM。PAM 框架允许在不修改任何应用程序的情况下实现身份验证模块。目前，身份验证功能已应用于 CDE 组件、HP-UX 标准命令、可信系统以及 DCE（分布式计算环境），以及第三方模块。

## 系统安全策略

HP-UX 安全中最重要的是你实施的策略。例如，如果你选择审计每一个系统调用，但不限制用户密码，那么你很可能会向任何用户开放系统。你最好限制用户权限，而不是过分担心他们的行为。在安全领域，主动防御比被动应对更为重要。

启用**密码老化策略**后，允许你设置：

- 密码更改间隔时间
- 密码过期时间
- 密码过期警告时间
- 密码生存时间
- 立即使所有用户密码过期

启用**常规用户账户策略**后，允许你指定账户变为非活动状态并锁定它的时间。此外，你还可以指定允许的最大登录尝试次数。

**终端安全策略**允许你设置：

- 允许的最大登录尝试次数
- 登录尝试之间的延迟
- 登录超时值（以秒为单位）
- 启动到单用户状态时所需的登录

### 备份和恢复

作为系统管理员，你将执行的最重要的活动是系统备份和恢复。SAM 团队投入了大量心血，为你提供确保系统完整性的所有备份和恢复选项。你可能还想查看第 7 章，该章节涵盖了 HP-UX 上可用的各种备份命令。图 11-21 展示了备份和恢复 SAM 菜单的层级：

![](img/eff8b9287a5f38c5adf538f24aacf29e_672_0.png)

#### 计划备份

第一步是进入*自动备份*子区域。在你指定之前，你不会看到列表中有任何自动备份。使用*操作*菜单并选择*添加自动备份*，你可以指定自动备份的所有信息。当你选择*添加自动备份*时，你必须指定备份是到本地还是远程备份设备。你需要输入有关备份范围、备份设备、备份时间和附加参数的信息。

### 选择备份范围

你可以将备份范围视为包含在备份中以及从备份中排除的文件。这可以包括通过网络文件系统（NFS）挂载的文件系统。图 11-22 展示了用于指定备份中包括和排除的文件窗口：

![](img/eff8b9287a5f38c5adf538f24aacf29e_673_0.png)

图 11-22 选择备份范围

图 11-22 所示的选择中，在“包含的文件”下指定了若干目录。这些是使用“仅本地文件系统（无 NFS）”选项选择的。我们同样可以轻松地将文件和目录从备份范围中排除。

### 选择备份设备

如果你计划备份到本地备份设备，那么连接到系统的设备将被列出，你从列表中选择所需的设备。

如果你计划使用远程备份设备，那么你需要指定远程系统名称和设备文件。

### 选择备份时间

与备份范围一样，你会得到一个窗口，其中可以输入有关全量备份和增量备份的备份时间的全部信息，如图 11-23 所示。如果启用了增量备份，则你必须提供有关全量和增量备份的所有相关信息，如图所示。





![](img/eff8b9287a5f38c5adf538f24aacf29e_675_0.png)

图 11-23 选择备份时间

这里有一个关键点需要记住，即 SAM 为您创建的增量备份包含自上次完整备份以来发生更改的文件。这意味着，若要恢复您的系统，只需要完整备份和最后一次增量备份即可；也就是说，您不需要恢复完整备份以及每一个增量备份。

## 设置额外参数

您还可以指定额外的参数，例如是否创建索引日志（我强烈建议这样做）以及将备份结果邮件发送给谁。在指定备份信息后，您可以查看 SAM 为 root 创建的用于备份的 crontab 条目。*crontab* 文件用于安排由 *cron* 自动执行的任务。*crontab* 文件位于 `/var/spool/cron/crontabs` 目录中。**cron** 是一个在指定时间运行其他程序的程序。*cron* 读取指定要执行的操作及其执行日期和时间的文件。由于我们希望定期执行备份，SAM 将启用 *cron*。

*crontab* 文件条目的格式如下：

minute hour month day month weekday user name command

- *minute* - 小时内的分钟数，范围从 0-59
- *hour* - 一天中的小时数，范围从 0-23
- *monthday* - 月份中的天数，范围从 1-31
- *month* - 一年中的月份，范围从 1-12
- *weekday* - 星期几，范围从 0 (周日) - 6 (周六)
- *user name* - 如果需要，将运行该命令的用户（在示例中未使用）
- *command* - 指定要运行的命令行或脚本文件

在 *crontab* 中，您有许多选项可用于指定执行任务所需的 *minute*（分钟）、*hour*（小时）、*monthday*（日）、*month*（月）和 *weekday*（星期几）。您可以列出字段中的一个条目，然后加一个空格；或在任何字段中用逗号分隔列出多个条目；或用破折号分隔两个条目以指示范围；或者使用星号，它对应于该字段所有可能的条目。

要列出 *crontab* 文件的内容，您只需输入命令 *crontab -l*。SAM 将为您指定的任何备份创建 *crontab* 条目。

当您使用 SAM 的 *Log Viewer*（日志查看器）查看 SAM 为您创建 *crontab* 文件所做的操作时，您会看到各种 *crontab 命令*。例如，如果您更改备份计划，SAM 将使用以下命令移除旧的 *crontab* 文件：

```
$ crontab -r
```

这将移除 `/var/spool/cron/crontabs` 目录中该用户的 **crontab** 文件。

要将文件放入 **crontab** 目录中，您只需输入 **crontab** 命令和 **crontab** 文件的名称：

```
$ crontab crontabfile
```

您可以使用 SAM 安排 cron 任务。本章中关于 *Process Management*（进程管理）的部分有一个名为 *Scheduling Cron Jobs*（安排 Cron 任务）的章节。

## 交互式备份和恢复

*Interactive Backup and Recovery*（交互式备份和恢复）子区域用于交互式执行备份，或恢复先前备份中包含的信息。当您进入此区域时，系统会提示您从生成的列表中选择备份设备，这与您首次进入 *Automated Backups*（自动备份）子区域时被提示选择备份设备的方式相同。

从列表中选择设备后，您可以选择之前提到的 *Actions*（操作）菜单中的某一项。如果您决定使用 *Backup Files Interactively*（交互式备份文件），系统会再次提供一个窗口，您可以从中指定要包含在备份中以及要从备份中排除的文件。系统会要求您 *Select Backup Scope*（选择备份范围）、*Specify Tape Device Options*（指定磁带设备选项）以及 *Set Additional Parameters*（设置额外参数）。但是，由于备份是交互进行的，因此系统不会要求您 *Select Backup Time*（选择备份时间）。

此区域的步骤会根据您选择的磁带设备而有所不同。

索引文件可以从 *Actions*（操作）菜单中查看。这些文件存储在 `/var/sam/log` 目录中。以下显示了一个交互式备份索引文件的最顶部和最底部内容：

```
#1 /
#1 /.profile
#1 /.rhosts
#1 /.sh_history
#1 /.sw
#1 /.sw/sessions
#1 /.sw/sessions/swinstall.last
# 1 /.sw/sessions/swlist.last
# 1 /.sw/sessions/swmodify.last
# 1 /.sw/sessions/swreg.last
# 1 /.dt
# 1 /.dt/Desktop
# 1 /.dt/Desktop/Two TOP
# 1 /.dt/Desktop/Four
# 1 /.dt/Desktop/One
# 1 /.dt/Desktop/Three
# 1 /var/uccp/.Log/uucico
# 1 /var/uccp/.Log/ucup
# 1 /var/uccp/.Log/uuxq
# 1 /var/uccp/.Log/uuxqt
# 1 /var/uccp/.Old
# 1 /var/uccp/.Status
# 1 /var/vrespool/sw
# 1 /var/vrespool/sw/catalog/dfiles
# 1 /var/vrespool/sw/catalog/swlock
# 1 /var/vrespool/sw/swagent.log
# 1 /var/yp
# 1 /var/yp/Makefile BOTTOM
# 1 /var/yp/binding
# 1 /var/yp/securenets
# 1 /var/yp/securereservers
# 1 /var/yp/updaters
# 1 /var/yp/ypmake
# 1 /var/yp/ypxfr_1perday
# 1 /var/yp/ypxfr_1perhour
# 1 /var/yp/ypxfr_2perday
```

## 执行恢复

然而，完整备份或增量备份的价值仅在于它所恢复的文件。要从备份磁带中检索文件，您需要指定一个备份设备，然后指定许多与备份相关的选项。图 11-24 显示了从连接到系统的四个 DLT 单元中选择一个设备：

![](img/eff8b9287a5f38c5adf538f24aacf29e_679_0.png)

图 11-24 从四个 DLT 单元中选择

选择设备后，您可以从许多选项中进行选择，其中包括图 11-25 中所示的选项：

![](img/eff8b9287a5f38c5adf538f24aacf29e_680_0.png)

图 11-25 *Recover Files Interactively*（交互式恢复文件）

在此窗口中，您需要提供三个区域的信息：*Select Recovery Scope*（选择恢复范围）、*Specify Tape Device Options*（指定磁带设备选项）以及 *Set Additional Parameters*（设置额外参数）。您指定的设备选项将取决于您正在使用的磁带设备。

*Select Recovery Scope*（选择恢复范围）允许您输入一个包含要恢复文件的文件名，或者手动列出要包含在恢复中的文件。您还可以选择列出要从恢复中排除的文件。

在 *Specify Tape Device Options*（指定磁带设备选项）中提供了磁带设备文件列表，您可以从中选择磁带设备。在此步骤中，您可以选择磁带设备文件；在其他情况下，您可能需要选择磁光盘表面，或者可能根本不需要选择任何内容。

在 *Set Additional Parameters*（设置额外参数）下，您可以选择以下任一选项：

- 覆盖较新的文件 (Overwrite Newer Files)
- 保留原始文件所有权 (Preserve Original File Ownership)
- 使用完整路径名恢复文件 (Recover Files Using Full Path Name)
- 将文件放入非根目录 (Place Files in Non-Root Directory)

完成所有所需的选择后，恢复操作将开始。如果一个文件被意外删除，您希望从恢复磁带上将其还原，那么您应选择 *Preserve Original File Ownership*（保留原始文件所有权）和 *Recover Files Using Full Path Name*（使用完整路径名恢复文件）选项。在恢复进行时，您将收到恢复状态信息；恢复完成后，您也可以从 *Actions*（操作）菜单中 *View Recovery Log*（查看恢复日志）。如果您选择 *View Recovery Log*（查看恢复日志），您将看到一个窗口，其中提供索引日志的名称以及已恢复文件的名称。

### 集群

可以通过 SAM 管理高可用性集群。诸如添加应用程序和添加应用程序组之类的任务可以使用 SAM 来完成。由于 *高可用性*（high availability）是计算环境中高度定制化的方面，我将不详细涵盖 SAM 的这部分内容。但是，如果您必须管理系统集群，建议您查看此 SAM 区域，看看它是否有助于您的集群相关工作。

### 磁盘和文件系统

*Disks and File Systems*（磁盘和文件系统）帮助您管理磁盘设备、文件系统、逻辑卷、交换区和卷组（如果您的系统中安装了其他 HP 磁盘设备，如 XP 和磁盘阵列，您也可以通过这些设备通过 SAM 进行管理。）没有必要手动操作这些设备，因为 SAM 在管理这些方面做得非常好。图 11-26 和 11-27 显示了 *Disks and File Systems*（磁盘和文件系统）的层次结构：

![](img/eff8b9287a5f38c5adf538f24aacf29e_683_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_683_1.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_683_2.png)

- 操作：（还包括磁盘阵列维护）
    - 配置 (Configure)
        - 使用逻辑卷管理器 (Using Logical Volume Manager)
        - 不使用逻辑卷管理器 (Not Using Logical Volume Manager)
    - 诊断缺失磁盘 (Diagnose Missing Disk)
    - 查看更多信息 (View More Information)
    - 将磁盘标记为已使用 (Mark Disk As Used)
    - 取消配置 (Unconfigure)

![](img/eff8b9287a5f38c5adf538f24aacf29e_683_3.png)

- 操作：
    - 添加本地文件系统 (Add Local File System)
        - 使用逻辑卷管理器 (Using Logical Volume Manager)
        - 不使用逻辑卷管理器 (Not Using Logical Volume Manager)
    - 添加远程文件系统 (Add Remote File System)
        - 使用 NFS (Using NFS)
        - 使用 NFS - 自动挂载器 (Using NFS - Automounter)
        - 使用 NFS - 主机映射 (Using NFS - Hosts Map)
        - 导出自动挂载器 (Export Automounter)
    - 启用 NFS 客户端 (Enable NFS Client)
    - 启用自动挂载器 (Enable Automounter)
    - 查看更多信息 (View More Information)
    - 修改 (Modify)
    - 移除 (Remove)
    - 转换为长文件名 (Convert to Long File Names)
    - VxFS 维护 (VxFS Maintenance)
    - 创建快照 (Create SnapShot)
        - 查看扩展片段报告 (View Extent Fragmentation Report)
        - 查看目录片段报告 (View Directory Fragmentation Report)
        - 重组扩展 (Reorganize Extents)
        - 重组目录 (Reorganize Directories)
        - 从版本 2 升级到版本 3 (Upgrade from Version 2 to Version 3)

![](img/eff8b9287a5f38c5adf538f24aacf29e_683_4.png)

- 操作：（镜像也在这里控制）
    - 创建 (Create)
    - 查看更多信息 (View More Information)
    - 修改 (Modify)
    - 移除 (Remove)
    - 增加大小 (Increase Size)
    - 更改镜像副本数量 (Change Number of Mirror Copies)
    - 将脱机镜像副本合并回联机状态 (Merge Offline Mirror Copy Back Online)

图 11-26 磁盘和文件系统菜单结构





![](img/eff8b9287a5f38c5adf538f24aacf29e_684_0.png)

图 11-27 磁盘和文件系统菜单结构（续）

## 磁盘设备

进入此子区域后，SAM 会显示连接到您系统的磁盘设备。图 11-28 显示了一台 Series 800 单元磁盘的列表：

![](img/eff8b9287a5f38c5adf538f24aacf29e_685_0.png)

图 11-28 磁盘设备窗口

前两条条目指的是 L-Class 系统中的内部磁盘。第三条条目是 CD-ROM 驱动器。让我们将此输出与运行 ioscans 时看到的结果进行比较：

```
$ /usr/sbin/ioscan -func disk
Class I /H/W Path Driver S/W State H/W Type Description
-----------------------------------
disk 1 0/0/1/1.2.0 sdisk CLAIMED DEVICE SEAGATE ST318203LC
/dev/dsk/c1t2d0
/dev/rdsk/c1t2d0
disk 2 0/0/2/0.2.0 sdisk CLAIMED DEVICE SEAGATE ST318203LC
/dev/dsk/c2t2d0
/dev/rdsk/c2t2d0
disk 3 0/0/2/1.4.0 sdisk CLAIMED DEVICE TOSHIBA CD-ROM XM-6201TA
/dev/dsk/c3t4d0
/dev/rdsk/c3t4d0
```

ioscan 的输出与 SAM 生成的磁盘信息相一致。SAM 的输出还表明第一个磁盘已使用，第二个磁盘未使用，而 ioscan 并未显示这一点。

现在我们可以通过在 SAM 中选择“操作”菜单中的“添加”来添加其中一个未使用的磁盘。使用逻辑卷管理器（Logical Volume Manager），我们可以创建一个新的卷组，或者选择希望添加新磁盘的卷组。然后，我们将选择希望在卷组上创建的新逻辑卷，或者扩展现有逻辑卷的大小。其他信息，如挂载目录和逻辑卷的大小，也将被输入。

连接到您系统的大多数磁盘都可以通过 SAM 进行管理。图 11-29 显示了一台 V-Class 系统的 SAM 屏幕截图，该系统连接了一个 XP-256：

![](img/eff8b9287a5f38c5adf538f24aacf29e_687_0.png)

图 11-29 显示 XP-256 磁盘的磁盘设备窗口

截图中显示了所连接磁盘总数的一小部分。前八个磁盘位于 V-Class 内部，其余的是 XP 磁盘。图中显示的所有设备都可以通过 SAM 进行管理。

## 文件系统

*文件系统* 显示挂载目录、文件系统类型以及源设备或远程目录。图 11-30 显示了进入之前示例中使用的 L-Class 系统 *文件系统* 时看到的信息：

![](img/eff8b9287a5f38c5adf538f24aacf29e_688_0.png)

在此级别，您可以执行诸如添加本地文件系统和添加远程文件系统等任务，并且可以从“操作”菜单执行 VxFS 维护。

“类型”列下可能列出几种类型的文件系统。最常见的是：

- **Auto-Indirect**：包含可自动挂载的远程 NFS 文件系统的目录。如果正在运行自动挂载器，您可能会在此处看到 /net 目录。
- **Auto-Mount**：可自动挂载的远程 NFS 文件系统。
- **CDFS**：如果当前已挂载 CD-ROM 文件系统。例如，如果您将 CD-ROM 挂载为 /SD_CDROM，您将在列表中将其视为 CDFS 类型。
- **HFS**：本地 HFS 文件系统。这些是系统的本地 HFS 文件系统。这是 HP 版本的 UNIX 文件系统。这是早期 HP-UX 版本中最常见的文件系统。
- **NFS**：当前已挂载的远程 NFS 文件系统。
- **LOFS**：允许您在多个位置拥有相同文件系统的回环文件系统。
- **VxFS**：本地日志型文件系统（JFS）。这是 HP-UX 对 Veritas 日志型文件系统（VxFS）的实现，支持快速文件系统恢复。JFS 是默认的 HP-UX 文件系统。

*添加本地文件系统* 允许您挂载未挂载的本地文件系统。*添加远程文件系统* 使您可以从另一台主机挂载文件系统。*VxFS 维护* 子区域是可以对您的 JFS 文件系统执行一些文件系统维护任务的地方。在这里，您可以生成关于 extent（区段）和目录碎片的报告。一旦审阅这些报告并发现确实需要进行维护，您可以选择重新整理 extent 或目录的选项。

## 逻辑卷

您可以在 *SAM* 中执行与逻辑卷操作相关的多种功能。诸如 *创建、修改、删除* 和 *增加大小* 之类的任务可以在 SAM 中执行。图 11-31 显示了将 *Ivol5 (home)* 的大小从 52 MBytes 增加到 6 MBytes：

![](img/eff8b9287a5f38c5adf538f24aacf29e_691_0.png)

图 11-31 增加大小窗口

SAM 只有在可以卸载逻辑卷的情况下才会增加其大小。在此任务完成后查看日志文件，显示 SAM 运行了诸如 */sbin/lvextend* 和 */sbin/ext2dfs* 等命令来扩展逻辑卷和文件系统的大小，并运行了 */usr/sbin/umount* 和 */usr/sbin/mount* 来卸载和挂载文件系统。

请参阅第 9 章中关于逻辑卷管理器的详细内容，以了解逻辑卷管理器的术语定义。那里还描述了一些逻辑卷管理器命令。

SAM 可能在尝试增加逻辑卷大小时产生一系列独特的问题。如果逻辑卷无法卸载，在增加其大小时可能会遇到问题。例如，如果您想增加 /opt 逻辑卷的大小，SAM 必须首先将其卸载。如果 SAM 无法卸载 /opt，您将收到 SAM 发出的消息，指示该设备正忙。您可以进入单用户状态，但您必须挂载某些逻辑卷，例如 /usr 和 /var，以便 SAM 能够运行。完成工作后，您需要使用 shutdown -r 重新启动系统。这对于 SAM 运行时不需要的目录（如 /opt）有效。

或者，您可以退出 SAM，终止访问您希望扩展大小的逻辑卷的任何进程，然后手动卸载该逻辑卷。然后您可以使用 SAM 来增加逻辑卷的大小。

HP OnLineJFS 附加产品允许您在单用户模式下执行许多这些 LVM 功能。例如，使用 OnLineJFS，逻辑卷和文件系统可以在系统运行且没有中断用户或进程的情况下简单扩展。

## 交换空间

当您进入 *交换空间* 时，设备交换和文件系统交换都会列出。为您列出的是 设备文件/挂载目录、类型、可用 Mbytes 和 已启用。您可以通过高亮显示某个项目并从 *操作* 菜单中选择“放大”来获取有关该项的更多信息。

## 卷组

当您进入卷组时，为您列出的是 *名称、可用 Mbytes、物理卷 和 逻辑卷*。如果您的系统上有未使用的磁盘，您可以扩展现有卷组或创建新的卷组。此窗口对于查看卷组内尚未分配的磁盘空间量很有用。这里的另一个功能是能够从其他系统导入卷组或将卷组准备好导出到远程系统。当您将包含在整个磁盘驱动器或一组磁盘驱动器上的卷组从一个系统移动到另一个系统时，您会用到这个功能。

### 显示

在此 SAM 区域，您可以执行与系统上图形显示器相关的工作。SAM 中对此工作自我解释，因此我不会详细介绍 SAM 的这个功能区域。

### 内核配置

您的 HP-UX 内核是您 HP-UX 系统中至关重要的一部分，但经常被 HP-UX 管理员忽视。这可能是因为管理员不愿去摆弄系统如此关键和敏感的部分。然而，您的 HP-UX 内核可能会对系统性能产生重大影响，因此您务必了解它是如何配置的。这并不意味着您必须进行大量的实验性更改，但您应该了解当前内核的配置方式，以便评估内核更改可能对系统产生的影响。

SAM 允许您查看和修改 HP-UX 内核的四个基本元素。新的 HP-UX 系统管理员对这些元素存在很大的混淆。在我详细阐述这四个区域的细节之前，我将首先对每个区域进行简要描述。

- **可配置参数** - 这些是与 *值* 相关联的参数。更改值时，您很有可能会影响系统的性能。一个 *可配置参数* 的示例是 *nfile*，即系统中的最大打开文件数。HP-UX 11i 中的许多可配置参数可以在不重启的情况下修改并包含在内核中。我们将在接下来的一个示例中讨论这一点。




-   驱动程序 - 驱动程序用于控制系统上的硬件。您有一个名为 CentIF 的驱动程序，用于并行接口；一个名为 sdisk 的驱动程序，用于 SCSI 磁盘，等等。
-   转储设备 - 转储设备用于在遇到严重内核问题时保存主内存的内容。如果未配置转储设备，则主内存的内容将保存在主交换设备上，并且当系统启动时，此信息会被复制到其中一个目录（通常是 /var/adm/crash）。拥有一个转储设备并非必要，但如果拥有转储设备，系统在崩溃后的启动速度会更快，因为主内存的内容在崩溃后不需要复制到文件中。转储设备与交换设备不同。
-   子系统 - 子系统不同于驱动程序。子系统是系统中的功能区域或支持模块，例如 CD-ROM/9000（CD-ROM 文件系统支持）；LVM（逻辑卷管理器支持）等。

当您进入上述四个子领域之一时，系统将列出您系统针对相应子领域的配置。进入内核配置后的第一件事应该是进入每个子领域，并查看每个领域中关于您系统的信息列表。

内核配置中有一个当前内核和一个待定内核。当前内核是您正在运行的内核，而待定内核是您正在对其做出更改的内核。

图 11-32 显示了 SAM 菜单中内核配置的层级结构。

### 内核配置

![](img/eff8b9287a5f38c5adf538f24aacf29e_695_0.png)

如果您的工作站 RAM 少于 32 MB，您还可能看到“应用精简配置”

图 11-32 内核配置菜单结构

## 可配置参数

选择可配置参数将列出所有您的可配置内核参数。对于每个可配置参数，将列出以下信息：

-   名称 - 参数的名称。
-   当前值 - /stand/vmunix 中该参数的值。
-   待定值 - 待构建内核中该参数的值。
-   类型 - 显示该参数是静态内核的一部分还是可加载模块。
-   关联模块 - 如果类型是可加载的，则列出该参数所属的模块。
-   描述 - 几个词来描述该参数。

然后您可以执行多种操作，包括以下操作：

### 应用调优参数集

已为各种环境调优了多组可配置参数。当您从操作菜单中选中此项时，系统上调优过的参数集（例如数据库服务器系统）将被列出，您可以从中进行选择。

### 模板

您可以选择一个内核模板进行加载，这基本上是与您当前运行的内核配置不同的内核配置。

### 处理新内核

在对可配置参数的*待定值*进行任何更改后，您可以让 SAM 为您创建一个新的内核。

### 修改可配置参数

您可以更改*待定*内核中某个参数的值。您只需高亮显示一个参数，并从*操作*菜单中选择此项。

SAM 使得修改可配置参数变得更加容易。虽然更改参数在操作上更简单，但确定参数的值仍然是此过程中最重要的部分。

许多应用程序建议修改其中一个或多个参数以实现应用程序的最佳性能。但请记住，许多这些参数是相互关联的；修改一个可能会负面影响另一个参数。许多应用程序会要求您更改 *max-uprc* 以支持更多的进程。请记住，如果运行的进程更多，您可能会出现更多打开的文件，并且可能还需要更改每个进程的 *maxfiles*。如果您的系统主要用于单一应用程序，您可以在修改这些参数时更有信心。但如果您运行许多应用程序，请确保不要以提升一个应用程序的性能为代价而损害另一个应用程序的性能。

当您决定修改可配置参数的值时，请务必小心。其中一些值的范围很宽。*maxuprc*（最大用户进程数）可以低至三个进程。我无法想象一个系统在这种低数值下能用于什么用途，但 SAM 确保该参数设置在 HP-UX 支持该参数的范围内：更改这些值时要“管理员谨防”。您可能会发现想要撤销某些更改。以下是一些建议：仔细记录您更改的值，以防需要撤销更改。此外，每次尽可能少地更改值。这样，如果您对结果不满意，您就知道是哪个可配置参数导致了问题。

在第 4 章中，在讲解内核时，我们手动修改了 *maxuprc* 内核参数。由于该参数是动态的，因此无需重启即可使其生效。现在我们使用 SAM 来修改此参数，并再次证明由于它是动态的，如果使用 SAM 进行修改则无需重启。

图 11-33 显示了 SAM 屏幕截图中选中的 *maxuprc*：

![](img/eff8b9287a5f38c5adf538f24aacf29e_699_0.png)

现在让我们将 maxuprc 的值从 80 增加到 100，如图 11-34 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_700_0.png)

图 11-34 maxuprc 从 80 到 100

单击 OK 会立即在系统中将 maxuprc 从 80 更改为 100，无需重启，如图 11-35 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_701_0.png)

图 11-35 _maxuprc：增加立即生效_

图 11-35 显示 _maxuprc_ 的 _当前值_ 和 _待定值_ 均为 100，且无需重启。动态可配置参数和动态可加载内核模块可以以此方式更新而无需重启。

### 驱动程序

当您选择 *驱动程序* 时，将列出您当前内核、您当前内核基于的模板文件以及待定内核的驱动程序。您将通过看到一些列出的驱动程序既不在当前内核中也不在待定内核中，从而知道所显示的驱动程序不仅仅是针对您当前内核的。进入 *驱动程序* 子区域时，会为您列出以下信息：

-   名称 - 驱动程序的名称。
-   当前状态 - 列出驱动程序在 /stand/vmunix 中是 *启用* 还是 *禁用*。
-   待定状态 - 列出驱动程序在待构建的内核中是 *启用* 还是 *禁用*。
-   类别 - 识别该元素是驱动程序还是模块。
-   类型 - 识别驱动程序是静态内核的一部分还是可加载模块。
-   启动时加载模块？ - 如果是可加载模块，列出驱动程序是否在启动时自动加载。
-   描述 - 几个词来描述该驱动程序。

*当前状态* 指示所选驱动程序是否存在于 /stand/vmunix 中。

*待定状态* 指示您是否已选择将该驱动程序添加至内核或从内核中移除。*启用* 表示该驱动程序是内核的一部分或待定为内核的一部分。*禁用* 表示该驱动程序不是内核的一部分或待定为从内核中移除。

通常，驱动程序是静态添加的。也就是说，它们被添加到内核中并留在那里。但是，如果驱动程序是为特定目的特别创建的模块，则它可以被配置为可加载。这意味着可以从内核中加载和卸载它而无需重启系统。此高级功能在 Hewlett-Packard 的 *系统和工作组管理* 一书中的“管理动态可加载内核模块”章节中有详细讨论。

使用 *操作* 菜单，您可以选择其中一个驱动程序并添加或移除它。您也可以从 *操作* 菜单中选择 *查看驱动程序详细信息*。




在您选择其中一个驱动程序后。您可以从“操作”菜单中选择“处理新内核”。如果通过添加或删除驱动程序来索引并修改了此屏幕，您需要重建内核。SAM 会在执行此操作之前询问您是否确定要重建内核。我这里唯一建议的是，在重建内核之前，务必仔细完成您的选择。

## 转储设备

进入此子区域时，系统会向您列出当前的转储设备和待处理的转储设备。当系统发生严重的内核问题时，会使用转储设备将主内存写入磁盘。这些信息即为核心转储（core dump），之后可以从磁盘读取并用于帮助诊断内核问题。

在 HP-UX 11.x 之前，内存转储包含物理内存的完整映像。因此，为了获取完整的内存转储，您需要创建一个至少与主内存一样大的转储区。对于内存容量达到千兆比特的系统来说，仅仅等待系统恐慌发生就浪费了大量的磁盘空间。HP-UX 11.x 引入了新的快速转储功能。这允许您选择需要转储的内容。快速转储功能不仅防止将未使用的内存页和用户文本页进行转储，还允许您配置要转储的内存页类。

系统中转储区的大小可以配置得比主内存稍小。您可以指定磁盘或逻辑卷作为转储设备（您也可以指定磁盘分区，但我完全不建议使用磁盘分区）。随后，整个磁盘或逻辑卷将被保留作为转储设备。

如果没有指定转储设备，或者转储区的大小小于配置要转储的内容大小，则核心转储将被写入主交换区（primary swap）。在系统启动时，核心转储会写入核心文件，通常位于 /var/adm/crash。这是我经手的大多数系统的运行方式；也就是说，没有指定具体的转储设备，核心转储先写入主交换区，然后写入 /var/adm/crash。这种方法有时会造成混淆；即主交换区确实可以作为转储设备使用，但转储设备是专门用于核心转储目的的，而主交换区则是在未指定转储设备的情况下承担此角色。只要您不介意在启动时因将主交换区中的核心转储写入文件而额外花费的时间，您可能就不想为系统添加特定的转储设备。

由于您可能不会将整个磁盘分配为转储设备，所以可能会使用逻辑卷。您必须选择根卷组中未被使用或用于非文件系统交换的逻辑卷。这可以通过从 *Actions* 菜单中选择 *Add* 来添加磁盘或逻辑卷到转储设备列表来实现。

您最好熟悉 *Dump Devices* 中的 *View Dump Configuration Details* 子区域。在这里您可以查看当前的转储配置、当前和待处理的内核转储配置，以及当前的运行时转储配置。

## 子系统

选择 *Subsystems* 会列出您所有的子系统。对于每个子系统，将列出以下信息：

- *Name* - 子系统的名称。
- *Current Value* - 列出子系统是否 *In* 或 *Out of /stand/vmunix*。
- *Pending Value* - 列出子系统在待处理内核中是 *In* 还是 *Out*。
- *Description* - 几个描述该参数的词语。

然后您可以执行许多 *Actions*，包括以下操作：

- *Templates*：您可以选择一个内核模板来加载，这基本上是与您当前正在运行的不同的内核配置。
- *Process New Kernel*：在对子系统的 *Pending State* 进行任何您喜欢的更改后，您可以让 SAM 为您创建一个新的内核。
- *View Subsystem Details*：选择此项时，您将获得关于该子系统的更多详细信息。
- *Add Subsystem to Kernel*：当您突出显示其中一个子系统并从菜单中选择此项时，*Pending State* 将更改为 *In*，并且当您重建内核时，该子系统将被添加到内核中。
- *Remove Subsystem from Kernel*：当您突出显示其中一个子系统并从菜单中选择此项时，*Pending State* 将更改为 *Out*，并且当您重建内核时，该子系统将从内核中移除。

在选择完成后，您可以重建内核以包含您的待处理更改，或者在不应用这些更改的情况下退出。

### 网络与通信

*Networking and Communications* 的菜单层级结构如图 11-36 至 11-38 所示。此区域包含许多高级网络功能。由于 SAM 中需要涵盖的网络区域非常多，我将仅讲解其中几个，以便您对该区域的操作有个大概的了解。气泡图展示了与网络配置相关的许多区域，您可以使用 SAM 进行操作，如果您对于某些特定的网络功能是否可以使用 SAM 进行配置有疑问，可以回头参考该图。

![](img/eff8b9287a5f38c5adf538f24aacf29e_706_0.png)

图 11-36 网络与通信菜单结构

| 网络与通信 |
| :--- |
| **NIS** |
| - 操作： |
  - 设置域名 |
  - 配置主服务器 |
  - 配置从服务器 |
  - 禁用客户端 |
  - 修改 |
  - 移除 |
| **NIS+** |
| - 操作： |
  - NIS+ 组 |
  - NIS+ 表 |
| **名称服务开关** |
| - 操作： |
  - 配置名称服务开关 |
  - 缩放 |
| **网络接口卡** |
| - 操作： |
  - 修改系统名称 |
  - 修改 |
  - 添加 IP 逻辑接口 |
  - 启用/禁用 |
  - 删除 |
| **网络服务** |
| - 操作： |
  - 修改系统名称 |
  - 缩放 |
  - 启用/禁用 |
  - 重启（如果已启用） |

![](img/eff8b9287a5f38c5adf538f24aacf29e_707_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_708_0.png)

图 11-38 网络与通信菜单结构（续）

## 可引导设备

*Bootable Devices* 区域进一步细分为三个子区域：*DHCP Device Groups Booting from this Server*、*Devices for which Boot Requests are Relayed to Remote Servers* 和 *Fixed-Address Devices Booting from this Server*。我将简要描述每个子区域及其用途。动态主机配置协议（DHCP）现已在 HP-UX 上可用，并被许多服务使用。

*DHCP Device Groups Booting from this Server* 子区域是配置设备组的地方。每个组包含一组供该设备组使用的 IP 地址。设备可以是特定类型的打印机或特定类型的终端等。

在 *Devices for which Boot Requests are Relayed to Remote Servers* 子区域中，您可以查看有关从远程 Bootp 或 DHCP 服务器获取引导信息的引导协议（Bootp）客户端设备的信息。显示的信息包括客户端或客户端组，以及远程服务器的 IP 地址，以及来自客户端或客户端组的引导请求可以中继的最大跳数。

在 *Fixed-Address Devices Booting from this Server* 子区域中，您可以指定将使用引导协议（Bootp）或 DHCP 从您的系统引导的系统。Bootp 是一种系统发现网络信息并自动引导的手段。为了使其他设备将其用作引导源，您的系统上必须加载 Bootp 软件（有关如何列出系统上安装的软件，请参见第 2 章中的 *swlist* 命令）。在此子区域中，您可以添加、修改或删除 Bootp 设备。此外，您可以启用或禁用 Bootp 服务器。同样，DHCP 允许客户端使用 IP 地址池中的一个 IP 地址以自动引导。诸如 Ignite-UX 之类的应用程序可以配置为使用此协议。

当您进入 *Fixed-Address Devices Booting from this Server* 子区域时，您会立即收到可以从此系统引导的设备列表。您可以从 *Actions* 菜单中选择 *Add*，然后系统会要求您输入有关您要添加的设备以下信息：


- 主机名
- 互联网地址
- 子网掩码（此项为可选）
- 十六进制站点地址或客户端 ID（此项为可选）
- 引导文件名
- 是否使用以太网或 IEEE 802.3 进行引导
- 是否向客户端或设备发送主机名

你可以根据系统当前是否禁用或启用来支持此功能，从“操作”菜单中选择“启用协议服务器”或“禁用协议服务器”。当你“启用协议服务器”时，同时也会启用简单文件传输协议（TFTP），引导设备使用它来获取引导文件。当你启用或禁用此功能时，/etc/inetd.conf 将被编辑。此文件包含有关系统上运行的网络服务的信息。如果 /etc/inetd.conf 中的某一行前面带有“#”，则该行被视为注释。读取此文件条目的守护进程是 /usr/sbin/inetd。在启用或禁用引导之前，您可能希望查看 /etc/inetd.conf 文件，了解哪些服务已启用。通过 SAM 进行更改后，您可以再次查看 /etc/inetd.conf，查看哪些内容已被修改。有关 /etc/inetd.conf 的安全相关信息，请参阅“系统访问”。以下是来自启用引导和 TFTP 的系统中 /etc/inetd.conf 文件开头的部分。此外，文件开头还提供了此文件中字段的简要说明：

```
# Configured using SAM by root
#
# Inetd reads its configuration information from this file upon ex-
# ecution and at some later time if it is reconfigured.
#
# A line in the configuration file has the following fields separated
# by tabs and/or spaces:
#
# service name          as in /etc/services
# socket type           either "stream" or "dgram"
# protocol              as in /etc/protocols
# wait/nowait           only applies to datagram sockets, stream
#                       sockets should specify nowait
# user                  name of user as whom the server should run
# server program        absolute pathname for the server inetd
#                       will execute
# server program args.  arguments server program uses as they
#               normally are starting with argv[0] which
#               is the name of the server.
#
# See the inetd.conf(4) manual page for more information.
#
#
#
#
# ARPA/Berkeley services
#
ftpd                stream  tcp     nowait  root    /usr/sbin/ftpd      ftpd -l
telnet              stream  tcp     nowait  root    /usr/bin/telnetd   telnetd

# Before uncommenting the "ftpp" entry below, please make sure
# that you have a "ftpp" user in /etc/passwd. If you don't
# have one, please consult the tftpd(8) manual entry for
# information about setting up this service.

tftpd               dgram   udp     wait    root    /usr/sbin/tftpd    tftpd
bootps              dgram   udp     wait    root    /usr/sbin/bootpd   bootpd
#finger             stream  tcp     nowait  bin     /usr/bin/fingerd   fingerd
login               stream  tcp     nowait  bin     /usr/sbin/rlogind  rlogind
shell               stream  tcp     nowait  bin     /usr/sbin/rexecd   rexecd
exec                stream  tcp     nowait  root    /usr/sbin/rexecd   rexecd
#ucp                stream  tcp     nowait  bin     /usr/sbin/ucp     ucp
```

如果您选择*固定地址设备客户端名称*，则可以从*操作*菜单中选择*修改*或*移除*，以更改与客户端相关的某个参数（例如其地址或子网掩码），或完全移除该客户端。

## DNS (BIND)

域名服务（DNS）是一种用于解析主机名到 IP 地址映射的名称服务器。HP-UX 使用 BIND（伯克利互联域），这是可用于实现 DNS 的名称服务之一。DNS 服务器负责解析网络或子网上的所有主机名。每个 DNS 客户端将依赖服务器代表其解决所有 IP 地址到主机名的映射问题。引导文件由服务器用于定位数据库文件。数据库文件将主机名映射到 IP 地址，并将 IP 地址映射到主机名。通过 SAM，可以轻松设置 DNS 服务器。

有关 DNS 及其设置和管理的更多信息，请参阅 HP-UX 手册*《安装和管理互联网服务》*。

## Hosts

*Hosts* 子区域用于维护系统中的默认网关和远程主机。当您进入此子区域时，您将收到系统中指定的主机列表。此信息从系统的*/etc/hosts*文件中检索。

然后您可以从*操作*菜单中*添加*新主机、*指定默认网关*、*修改*其中一个主机，或*移除*其中一个主机。在添加主机时，系统将要求提供与该主机相关的信息，包括其互联网地址、系统名称、系统别名以及注释。

## NIS

网络信息服务（NIS）是一种数据库系统，用于在系统网络中传播公共配置文件。在主服务器上管理诸如*/etc/passwd*、*/etc/hosts*和*/etc/automounter*等文件，这些文件由自动挂载器使用。NIS 以前被称为“黄页”，它将这些文件转换为自己的数据库文件，称为映射（maps），供 NIS 域中的客户端使用。当客户端请求信息时（例如用户登录并输入密码时），信息是从服务器检索的，而不是从客户端系统检索的。因此，此类信息只需在服务器上维护即可。

通过 SAM，可以配置、启用、禁用和移除 NIS 主服务器、从服务器和客户端。一旦建立主服务器、从服务器和客户端，您可以轻松地构建、修改并将各种映射推送到从服务器。

NIS 在可信系统上不可用。

## NIS+

HP-UX 11i 支持 NIS+。这不是 NIS 的增强功能，而是一种新服务，包括标准系统和可信系统以及非 HP-UX 系统。如果您已经使用 NIS，NIS+ 的兼容模式版本允许服务器响应来自 NIS 和 NIS+ 客户端的请求。当在可信系统上配置 NIS+ 时，SAM 的*审计和安全*区域中会显示一个新的子区域，即*受审计的 NIS+ 用户*。

## 名称服务切换

名称服务切换文件*/etc/nsswitch.conf*现在可以通过 SAM 进行配置。此服务允许您确定使用哪个名称服务（FILES、NIS、NIS+、DNS 或 COMPAT）来查找信息的优先级。除非您专门使用这些服务之一，否则应使用默认的 FILES。FILES 指定支持使用本地 /etc 目录来存储诸如*/etc/passwd*、*/etc/hosts*和*/etc/services*等管理文件。（COMPAT 用于 NIS+ 的兼容模式。）

有关名称服务切换文件及其设置的更多信息，请参阅 HP-UX 手册*《安装和管理 NFS 服务》*。

## 网络接口卡

此子区域用于配置系统中的任何网络卡。您可以从操作菜单中*启用*、*禁用*和*修改*网络卡，以及*修改系统名称*。在*添加 IP 逻辑接口*下，您可以为现有的网络卡添加额外的逻辑 IP 地址。

*网络接口卡*屏幕列出了系统中安装的网络卡，包括下面列出的信息。您可能需要扩大窗口或滚动以查看所有此信息。

- 卡类型，例如以太网、IEEE 802.3、令牌环、FDDI 等。
- 卡名称
- 硬件路径
- 状态，例如卡是否已启用
- 互联网地址
- 子网掩码
- 十六进制站点地址

在以太网卡的*配置*部分中包含*高级选项*，它将修改此卡的最大传输单元（MTU）。您系统中的其他卡也可以在此处进行配置，例如 ISDN、X.25、ATM 等。

## 网络服务

此子区域用于启用或禁用系统中的*部分*网络服务。您将在图 11-39 中识别出一些网络服务，这些服务对应于前面显示的 /etc/inetd.conf 文件中的服务。此屏幕有三列，分别是网络服务的名称、状态和*描述*。图 11-39 中*网络服务*子区域显示了一些可以管理的网络服务：





![](img/eff8b9287a5f38c5adf538f24aacf29e_715_0.png)

在选择了图中所示的其中一个网络服务后，你可以根据其当前状态*启用*或*禁用*该服务。如果该服务当前处于启用状态，请*重启*该服务；通过*详细信息*获取有关该服务的更多信息，或者*修改系统名称*，所有这些操作均可从*操作*菜单中执行。

## 网络文件系统

此子区域细分为*导出的本地文件系统*、*挂载的远程文件系统*和*Netgroups*。NFS 被划分为前两个区域，因为你可以导出本地文件系统而无需挂载远程文件系统，反之亦然。这意味着你可以独立管理它们。在你的环境中，可能有一个 NFS 服务器不会挂载远程文件系统，也可能有一个 NFS 客户端只挂载远程文件系统而从不导出其本地文件系统。*Netgroups* 是 NIS 的一部分，允许你将一组系统或用户分组以便一起使用。除其他用途外，netgroup 指定可用于导出文件系统。

在*导出的本地文件系统*下，你可以选择想要导出的文件系统。首次进入此屏幕时，没有列出的导出文件系统。当你从*操作*菜单中选择*添加导出文件系统*时，你将输入如下信息：

- *本地目录名称*
- *用户 ID*
- *是否允许异步写入*
- *权限*

添加此导出文件系统后，你可以选择它并选择多种*操作*，包括*修改*和*删除*。

在*挂载的远程文件系统*下，列出了所有使用 NFS 挂载的目录和文件。这些可以根据需要由自动挂载器进行挂载或卸载。选择其中一个已挂载的文件系统后，你可以执行各种*操作*。对于每个已挂载的远程文件系统，你有以下列：

- *挂载目录*，显示用于挂载远程目录的本地目录名称。
- *类型*，对于标准 NFS 为 *NFS*，对于自动挂载器为 *Auto*（见下文段落）。
- *远程服务器*，显示文件 or 目录所在的远程系统名称。
- *远程目录*，这是远程挂载的目录名称。

你应该考虑是否要使用 NFS 自动挂载器。使用自动挂载器，你按需挂载远程文件或目录，即在你需要时挂载。使用主映射表，你可以指定哪些文件和目录将在需要时被挂载。使用自动挂载器时，文件和目录不会持续挂载，从而在系统资源使用方面提高了效率。然而，与持续挂载相比，按需挂载文件或目录会有一些开销时间。从用户角度来看，这可能稍显不利，但从管理角度来看，使用自动挂载器具有优势。由于自动挂载器是通过 SAM 管理的，你只需进行很少的额外工作即可启用它。

## 系统访问

此子区域细分为*Internet 服务*和*远程登录*。

当你选择*Internet 服务*时，屏幕会列出由 Internet 守护进程 `/usr/sbin/inetd` 启动的网络服务。我之前介绍过 `/etc/inetd.conf`，这是一个配置列表，列出了系统支持的所有网络服务，并被 `inetd` 读取。还有一个安全文件 `/var/adm/inetd.sec`，作为 `inetd` 的安全检查。尽管涉及许多其他组件，你可以将 `inetd`、`/etc/inetd.conf` 和 `/var/adm/inetd.sec` 视为协同工作，以确定支持哪些网络服务以及每个服务的安全级别。

在*系统访问*子区域中列出了*服务名称*、*描述*、*类型*和*系统权限*。图 11-40 显示了我的系统的默认设置：

![](img/eff8b9287a5f38c5adf538f24aacf29e_718_0.png)

图 11-40 系统访问 - Internet 服务窗口

你可以通过选择这些条目中的任何一个，使用*操作*菜单中的*修改*命令，并选择所需的权限，来更改其中任何条目的权限。

*远程登录*用于管理将访问本地系统的远程用户的安全限制。使用两个 HP-UX 文件来管理用户。文件 `/etc/hosts.equiv` 处理用户，而 `/rhosts` 处理超级用户（root）。进入此子区域时，你会看到用户列表及每个用户的限制。然后你可以添加、删除或修改登录安全设置。

## 分区管理器

许多运行 HP-UX 11i 的 HP 9000 系统支持分区。然而，在撰写本文时，分区作为一项先进技术才刚刚出现，我无法访问任何支持分区的系统。在运行 HP-UX 11i 的 HP 9000 系统上支持的两类分区是硬分区（*nPartition*）和虚拟分区（*vPars*），本书对此进行了全面介绍。在撰写本文时，硬分区在 Superdome 和 rp8400 系统上可用，主要由硬件组件组合而成，形成硬分区。我们在本书命令行中一直使用的 vPars，即将在或很快在 HP 9000 所有系统上可用。

### 性能监视器

在*性能监视器*下，你可以查看系统在磁盘和虚拟内存等多个领域的性能。图 11-41 显示了*性能监视器*的菜单层次结构：

![](img/eff8b9287a5f38c5adf538f24aacf29e_720_0.png)

**图 11-41** *性能监视器菜单结构*

*性能监视器* 为你提供了解系统多个方面的窗口。如果你真的想熟悉系统中可用的工具，以帮助理解系统资源的使用情况，你应该仔细阅读第 12 章。第 12 章专门用于掌握系统资源的使用情况，包括许多内置的 HP-UX 命令。你可以在此子区域中选择的一些性能监视器是 **HP-UX 命令**，在使用它们之前，你需要具备一定的背景知识。我将只简要介绍这些领域，因为第 12 章将更详细地讨论这些材料。

## 磁盘和终端活动

选择*磁盘和终端活动*会打开一个窗口，显示 **iostat -t** 的输出。我已包含第 12 章中关于 iostat 的描述，以免你翻阅到后面。当打开显示 **iostat** 输出的*磁盘和终端活动*窗口时，它显示单个 **iostat** 输出。按*Return*键时，窗口会自动为你关闭。

**iostat** 命令指示 CPU 在 I/O 上投入的努力程度以及磁盘和终端之间发生的 I/O 量。以下示例展示了 **iostat -t** 命令，该命令每三秒执行一次，以及来自 HP-UX 11.x 系统的相应输出：

```
# iostat -t 3

    tty                       cpu
    tin tout     us   ni   sy  id
    78   42      2    0   28  70

/dev/dsk/c0t1d0             /dev/dsk/c0t4d0           /dev/dsk/c0t6d0
 bps  sps   msps             bps  sps   msps            bps  sps   msps
  0    0     0               33   8.3    25.2             7    1    19.5

    tty                       cpu
    tin tout     us   ni   sy  id
    66   24      0    0   30  70

/dev/dsk/c0t1d0             /dev/dsk/c0t4d0           /dev/dsk/c0t6d0
 bps  sps   msps             bps  sps   msps            bps  sps   msps
  5   12    15.9             36   9.7    21              7    1.2   13.8

    tty                       cpu
    tin tout     us   ni   sy  id
    90   29      1    0   25  73

/dev/dsk/c0t1d0          /dev/dsk/c0t4d0         /dev/dsk/c0t6d0
bps  sps  msps          bps  sps  msps          bps  sps  msps
 12   1.7   15.5         24    3   19.1          14   2.1  14.6

                 tty
                tin tout
                 48   16

                 cpu
              us   ni  sy  id
               1    0  16  83

/dev/dsk/c0t1d0           /dev/dsk/c0t4d0          /dev/dsk/c0t6d0
bps  sps  msps            bps  sps  msps            bps  sps  msps
0    0*     0              62  9.3  18              12    2   17.2

                 tty
                tin tout
                 32   48

                 cpu
              us   ni  sy  id
               7    0  14  79

/dev/dsk/c0t1d0           /dev/dsk/c0t4d0          /dev/dsk/c0t6d0
bps  sps  msps            bps  sps  msps            bps  sps  msps
1    0.3   14.4            5   .9  16.2           171 29.4  18.2

                 tty
                tin tout
                 2    40

                 cpu
              us   ni  sy  id
              20    1  42  27

/dev/dsk/c0t1d0           /dev/dsk/c0t4d0          /dev/dsk/c0t6d0
bps  sps  msps            bps  sps  msps            bps  sps  msps
248  30.9  20.8           203 29.2  18.8           165 30.6  22.1
```

以下是 iostat 为终端、CPU 和已挂载文件系统提供的报告说明。

对于你连接的每个终端（tty），你会看到“tin”和“tout”，它们分别代表从你的终端读取的字符数和写入你的终端的字符数。-t 选项生成此终端报告。

对于你的 CPU，你会看到用户模式花费时间的百分比（“us”）、以低优先级运行用户进程（称为 nice）所花费时间的百分比（“ni”）、系统模式花费时间的百分比（“sy”）以及 CPU 空闲时间的百分比（“id”）。

对于每个本地挂载的文件系统，你将收到关于每秒传输的千字节数（“bps”）、每秒寻道次数（“sps”）和平均每次寻道的毫秒数（“msps”）的信息。对于 NFS 挂载的磁盘或服务器客户端节点上的磁盘，你将不会收到报告：iostat 仅报告本地挂载的文件系统。





## GlancePlus

如果系统中已安装，GlancePlus 将在此处可用。你可以选择使用 GlancePlus 的 Motif（图形）版本或字符模式版本。GlancePlus 和其他 HP VantagePoint 产品在第 12 章中有详细说明。

## 进程间通信设施状态

进程间通信设施状态显示与进程间通信相关的信息类别。你可以获取消息队列、共享内存和信号量的状态。这只是一个状态窗口，因此再次按下 Return 键时，该窗口会关闭。

## CPU 使用率最高的进程

CPU 使用率最高的进程是一个非常有用的窗口，它列出了系统中消耗 CPU 资源最多的进程。此处列出了有用的信息，如进程 ID、其常驻集大小（RSS）以及所占用的 CPU 百分比。

## 系统活动

系统活动提供了一份 CPU 利用率的报告。你将获得以下列表：

- %usr：用户模式下 CPU 占用的百分比。
- %sys：系统模式下 CPU 占用的百分比。
- %wio：有一些进程正在等待 I/O（如虚拟内存页面换入或换出）时 CPU 空闲的百分比。
- %idle：CPU 完全空闲的百分比。

## 系统属性

*系统属性*提供了系统具体细节的概览。其中包含了那些难以查找的信息，例如处理器信息、CPU 版本、时钟频率、内核支持（32 位或 64 位）、内存信息、操作系统版本以及网络 IP 和 MAC 地址。

## 虚拟内存活动

*虚拟内存活动*运行 **vmstat** 命令。这同样在第 12 章中有涵盖，但我在此处包含了 **vmstat** 的说明，以便你无需翻阅后续章节。当为你打开 *虚拟内存活动* 窗口时，**vmstat** 的一些列会被略微重新排列。

**vmstat** 提供虚拟内存统计信息。它提供有关进程状态、虚拟内存、分页活动、故障以及 CPU 时间占比分解的信息。在以下示例中，输出以五秒间隔产生了十次。**vmstat** 命令的第一个参数是间隔时间；第二个是你希望产生输出的次数。

```bash
# vmstat 5 10
```

| procs | | | memory | | | page | | | | faults | | | cpu | | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| r | b | w | avm | free | re | at | pi | po | fr | de | sr | in | sy | cs | us | sy | id |
| 4 | 0 | 0 | 1161 | 2282 | 6 | 22 | 48 | 0 | 0 | 0 | 0 | 429 | 289 | 65 | 44 | 18 | 38 |
| 9 | 0 | 0 | 1161 | 1422 | 4 | 30 | 59 | 0 | 0 | 0 | 0 | 654 | 264 | 181 | 18 | 20 | 62 |
| 6 | 0 | 0 | 1409 | 1247 | 2 | 19 | 37 | 0 | 0 | 0 | 0 | 505 | 316 | 130 | 47 | 10 | 43 |
| 1 | 0 | 0 | 1409 | 1119 | 1 | 10 | 19 | 0 | 0 | 0 | 0 | 508 | 254 | 180 | 69 | 15 | 16 |
| 2 | 0 | 0 | 1878 | 786 | 0 | 1 | 6 | 0 | 0 | 0 | 0 | 729 | 294 | 217 | 75 | 17 | 8 |
| 2 | 0 | 0 | 1878 | 725 | 0 | 0 | 3 | 0 | 0 | 0 | 0 | 561 | 688 | 435 | 67 | 32 | 1 |
| 2 | 0 | 0 | 2166 | 98 | 0 | 0 | 20 | 0 | 0 | 0 | 66 | 723 | 952 | 145 | 8 | 14 | 78 |
| 1 | 0 | 0 | 2310 | 90 | 0 | 0 | 20 | 0 | 0 | 0 | 171 | 809 | 571 | 159 | 16 | 21 | 63 |
| 1 | 0 | 0 | 2310 | 190 | 0 | 0 | 8 | 1 | 3 | 0 | 335 | 704 | 499 | 176 | 66 | 14 | 20 |
| 1 | 0 | 0 | 2316 | 311 | 0 | 0 | 3 | 1 | 5 | 0 | 376 | 607 | 945 | 222 | 4 | 11 | 85 |

你会从 vmstat 命令中获得比所需更多的信息。下面是 vmstat 产生的信息类别的简要说明。

进程被分为三类：可运行（“r”）、阻塞在 I/O 或短期资源上（“b”）或被换出（“w”）。

接下来你会看到有关内存的信息。“avm”是过去 20 秒内已运行的进程拥有的虚拟内存页面数量。如果这个数字大致等于物理内存大小减去内核大小，那么你就接近分页状态了。“free”列指示系统空闲列表中的页面数量。这并不意味着进程已经结束运行且这些页面不会再被访问；它仅意味着这些页面最近没有被访问过。

接下来是分页活动。第一个字段（re）显示被回收的页面。这些页面曾进入空闲列表，但随后被引用，不得不被挽救。请检查“re”是否为低数值。如果你正在回收系统认为是空闲的页面，那么你正在浪费宝贵的时间来挽救这些页面。回收页面也是内存不足的征兆。

接下来你看到的是故障的三类计数：每秒中断数，通常来自硬件（“in”）；每秒系统调用数（“sy”）；以及每秒上下文切换数（“cs”）。

最后的输出是用户（“us”）、系统（“sy”）和空闲（“id”）的 CPU 使用百分比。这不如 iostat 的输出完整，后者还显示 nice 条目。

### 外围设备

通过外围设备，你可以查看系统中安装的任何 I/O 卡以及连接到系统的周边设备。这些包括正在使用和未使用的设备。你还可以快速配置任何外设，包括打印机、绘图仪、磁带驱动器、终端、调制解调器和磁盘。这是 SAM 中一个特别有用的区域，因为在 HP-UX 中配置外设比较棘手。当使用命令行时，连接打印机执行一种流程，连接磁盘执行另一种流程，等等。在 SAM 中，这些流程是菜单驱动的，因此容易得多。

六个子区域中的两个，磁盘和文件系统以及打印机和绘图仪，在 SAM 中有自己的专用层级，并在本章中涵盖。我不会在本节中再次介绍它们。其他四个子区域，卡、设备列表、磁带驱动器和终端及调制解调器，在本节中涵盖。

我不可能涵盖在 SAM 中可以查看和配置的每种可能设备。我将做的是给你一些服务器上报告为设备的示例，以便你了解在 SAM 的外围设备功能下可以做什么。根据我在这里展示的内容，你应该确信 SAM 可以帮助你配置外设。

图 11-42 显示了外围设备的层级：

![](img/eff8b9287a5f38c5adf538f24aacf29e_727_0.png)

- **操作：**
  - 添加
  - 分析关键资源
  - 诊断缺失卡
  - 放大
  - 移除
  - 显示设备文件
  - 创建设备文件
- **操作：**
  - 放大
  - 显示设备文件

与本章前文涵盖的 *磁盘和文件系统* 完全相同。

与本章后文涵盖的 *打印机和绘图仪* 完全相同。

- **操作：**
  - 添加
  - 移除
  - 诊断缺失磁带驱动器
  - 放大
  - 显示设备文件
  - 创建设备文件（默认或自定义）
- **操作：**
  - 添加终端或调制解调器
  - 移除终端或调制解调器端口
  - 锁定终端或调制解调器
  - 解锁终端或调制解调器
  - 修改终端安全策略
  - 修改终端授权用户

你还会拥有 *仪器和不可中断电源* 作为 *外围设备* 的一部分。

图 11-42 *外围设备菜单结构*

## 卡

当你选择卡时，会向你提供系统中 I/O 卡的列表。你还可以执行添加和移除卡等任务。拥有此 I/O 卡列表非常有用。图 11-43 显示了 L-Class 系统 I/O 卡的列表：

![](img/eff8b9287a5f38c5adf538f24aacf29e_728_0.png)

在卡中，你可以执行以下操作：

- **添加**：你可以在为你打开的窗口中添加一个新的 I/O 卡。
- **诊断缺失卡**：如果你安装的卡未包含在列表中，你可以选择此项以确定原因。
- **放大**：如果你高亮显示一张卡并选择 *放大*，你将获得诸如硬件路径、驱动程序以及卡的描述等信息。
- **移除**：如果你高亮显示一张卡并选择 *移除*，将弹出一个窗口，引导你从系统中移除该卡。
- **显示设备文件**：如果你选择此项，将打开一个窗口，列出与该卡关联的设备文件。
- **创建设备文件**：为选定的卡创建设备文件。此操作无需用户交互即可执行。

## 设备列表

*设备列表*显示配置到系统中的所有外设。图 11-44 显示了 L-Class 系统的设备列表：



![](img/eff8b9287a5f38c5adf538f24aacf29e_730_0.png)

**图 11-44** *外围设备窗口*

这里 *操作* 菜单中的两个选项是 *缩放* 和 *显示设备文件*。选择 *缩放* 会生成一个窗口，其中包含硬件路径、驱动程序、描述和状态等信息。如果您选择“显示设备文件”，将会显示与您高亮选中的项目相关联的设备文件。

磁盘和文件系统在本章前面已经介绍过。

如果您的系统支持 HP-IB 卡，可能会显示仪表。

打印机和绘图仪将在本章后面介绍。

## 磁带驱动器

磁带驱动器列出了连接到您系统的磁带驱动器。您将看到每个磁带驱动器的硬件路径、驱动程序和描述。您可以添加、移除、诊断磁带驱动器，列出磁带驱动器设备文件，以及添加新的磁带驱动器设备文件。图 11-45 显示了连接到系统的四驱动器 DLT 单元：

![](img/eff8b9287a5f38c5adf538f24aacf29e_731_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_732_0.png)

**图 11-45** 磁带驱动器窗口

## 终端和调制解调器

当您进入此子区域时，会列出您系统的终端和调制解调器。您可以从操作菜单执行多种任务，包括以下内容：

- 添加终端或调制解调器
- 移除终端或调制解调器端口
- 锁定终端或调制解调器端口
- 解锁终端或调制解调器端口
- 修改终端安全策略
- 修改终端授权用户
- 附加信息

## 不间断电源

当您进入该区域时，会列出您系统的不间断电源（UPS），包括 UPS 类型、UPS 设备文件、硬件路径、端口号以及是否启用关机功能。您可以选择的 *操作* 包括：*修改全局配置*、添加、缩放、移除和修改。

## 打印机和绘图仪

*打印机和绘图仪* 分为两个子区域：*HP 分布式打印服务* 和 *LP 打印后台*。*HP 分布式打印服务 (HPDPS)* 是分布式计算环境 (DCE) 的一部分。本书未对其内容进行介绍。*LP 打印后台* 在本节中介绍；图 11-46 显示了 *打印机和绘图仪* 的层级结构：

- 打印机和绘图仪
  - HP 分布式打印服务
  - LP 打印后台
  - 打印请求
    - **操作：**
      - 停止或启动打印后台
      - 缩放
      - 取消请求
  - 打印机和绘图仪
    - **操作：**
      - 添加本地打印机/绘图仪
      - 添加远程打印机/绘图仪
      - 添加基于网络的打印机/绘图仪
      - 停止或启动打印后台
      - 显示常见问题
      - 缩放
      - 移除
      - 启用或禁用
      - 接受或拒绝请求
      - 修改围栏优先级
      - 设为系统默认目标
      - 显示类的成员
      - 保存/恢复打印后台配置
    - **操作：**
      - 保存打印后台配置
      - 恢复打印后台配置
      - 缩放

![](img/eff8b9287a5f38c5adf538f24aacf29e_734_0.png)

**图 11-46** *打印机和绘图仪* 菜单结构

### 打印请求

在 *打印请求* 下，您可以管理打印后台和特定的打印任务。您可以启动或停止打印后台，并取消打印任务。关于打印请求，为您列出以下信息：

- **请求 ID：** 每个打印任务都关联一个 ID。这是打印机名称后跟一个数字。
- **所有者：** 请求该打印任务的用户名称。
- **优先级：** 打印任务的优先级在任务提交时分配。可以使用 `lp` 的 *p* 选项为任务分配优先级。每个打印目标都有一个默认优先级，当在 `lp` 命令中不使用 *p* 时，该优先级会分配给任务。
- **文件：** 发送到打印队列的文件名称。
- **大小：** 打印任务的字节大小。

*操作* 菜单允许您通过取消任务来处理打印任务。此外，可以停止和启动打印后台。

您可以在 *打印机和绘图仪* 中配置本地和远程打印机。当您从 *操作* 菜单中选择 *添加本地打印机/绘图仪*，然后选择适当的打印机类型时，会为您打开一个窗口，您可以在其中提供有关打印机的详细信息。然而，在此窗口打开之前，您必须指定要添加的打印机 *类型* 是：并行；串行；HP-IB；非标准设备文件；还是连接到 TSM 终端的打印机，以及将打印机添加到哪个 I/O 卡。使用 SAM 添加打印机的一个巨大优势是，该过程完全由菜单驱动，因此您只需从提供的信息中进行选择。

该窗口出现时会要求您提供以下信息：

- **打印机名称**
  您可以为打印机选择任何名称。我通常喜欢使用具有一定描述性的名称，例如对于 LaserJet 5，使用 *ljet5*。名称限制为 14 个字母数字字符和下划线。
- **打印机型号/接口**
  当此窗口打开时，SAM 为您提供所有接口型号的列表。这些型号位于 `/usr/lib/lp/model` 目录中。每个打印机都有一个接口程序，打印后台使用它向打印机发送打印任务。当选择接口型号时，该型号会被复制到 `/etc/lp/interface/<printername>`，在那里它成为打印机的接口程序。型号可以不加修改地使用，或者您可以创建自定义的接口程序。
- **打印机类**
  您可以定义一组打印机为一个类，这意味着打印请求不会发送到特定的打印机，而是发送到类中第一个可用的打印机。这是可选的。
- **默认请求优先级**
  这定义了发送到此打印机的所有请求的默认优先级级别。
- **默认目标**
  在请求打印任务时未指定打印机的用户，其打印请求将被发送到默认打印机。

您可以使用 SAM 查看打印机，也可以使用显示系统上已配置打印机的 lpstat 命令，如下例所示：

```bash
$ /usr/bin/lpstat -t
scheduler is running
system default destination: ljet5
members of class laserjet:
ljet5
device for ljet5: /dev/cltd0_lq
ljet5 accepting requests since Nov 21 22:45
printer ljet5 is idle, enabled since Nov 21 22:45
fence priority: 0
no entries
```

与 SAM 帮助您的其他所有任务一样，您可以手动管理打印机和绘图仪，也可以使用 SAM。SAM 不仅使这项工作变得更容易，而且我也发现让 SAM 为我执行此任务只有好的结果。当您查看 SAM 日志文件时，您会看到发出的一系列 lp 命令。一些更常用的命令，包括之前发出的 lpstat 命令，列在表 11-2 中：

## 表 11-2 lp 命令

| 命令 | 描述 |
| :--- | :--- |
| `/usr/sbin/accept` | 开始接受排队任务。 |
| `/usr/bin/cancel` | 取消排队的打印任务。 |
| `/usr/bin/disable` | 禁用设备的打印功能。 |
| `/usr/bin/enable` | 启用设备的打印功能。 |
| `/usr/sbin/lpfence` | 设置要打印的后台文件的最低优先级。 |
| `/usr/bin/lp` | 为打印排队任务或作业。 |
| `/usr/sbin/lpadmin` | 使用提供的选项配置打印系统。 |
| `/usr/sbin/lpmove` | 将打印作业从一个设备移动到另一个设备。 |
| `/usr/sbin/lpsched` | 启动 **lp** 调度守护程序。 |
| `/usr/sbin/lpshut` | 停止 **lp** 调度守护程序。 |
| `/usr/sbin/lpstat` | 根据提供的选项显示打印状态。 |
| `/usr/sbin/reject` | 停止接受排队任务。 |

## 保存/恢复打印后台配置

偶尔，打印后台可能会进入不一致的状态（通常，您的系统必须发生其他错误，最终导致某些打印后台配置文件被更改或重命名）。SAM 在每次使用它进行更改时都会保存打印后台配置的副本（只保存最近的一个）。可以恢复此保存的配置，以从打印后台进入不一致的状态中恢复。如果您使用 SAM 创建配置（而不是在命令行上发出 **lp** 命令），SAM 会自动保存您最新的配置，并且可以通过 *保存/恢复打印后台配置* 中的 *恢复打印后台配置* 进行恢复。此屏幕允许您保存当前的打印后台配置或恢复以前保存的打印后台配置信息。





### 进程管理

*进程管理* 分为两个区域，允许你控制和调度进程。*进程控制* 允许你通过执行诸如查看、更改其 *nice* 优先级、终止、停止或继续等任务来控制单个进程。你还可以在*计划任务 Cron 作业*下查看和调度 **cron** 作业。图 11-47 显示了*进程管理*的菜单层级：

![](img/eff8b9287a5f38c5adf538f24aacf29e_739_0.png)

图 11-47 *进程管理* 菜单结构

## 进程控制

当你选择进程控制时，SAM 会列出系统上的进程并允许你执行各种操作。与执行 `ps`、`nice` 等命令相比，使用进程控制是管理系统上进程的更简便方式。图 11-48 显示了部分进程列表：

![](img/eff8b9287a5f38c5adf538f24aacf29e_741_0.png)

列出的信息有四个列：

- *用户* - 拥有该进程的用户名称。
- *优先级* - 进程的优先级决定其由 CPU 进行的调度。数字越低，优先级越高。除非你修改了这些优先级，否则它们将是默认优先级。更改优先级是通过 `nice` 命令完成的，稍后将会介绍。
- *Nice 优先级* - 如果你希望以更低或更高的优先级运行某个进程，你可以更改此值。值越低，CPU 调度优先级越高。
- *命令* - 列出当前在系统上运行或执行的所有命令的名称。

除了这四个列之外，你可以通过从*视图*菜单选择*列*来指定包含在列表中的其他列。你可以包含诸如*进程 ID*、*父进程 ID*、*处理器利用率*、*核心映像大小*等信息。例如，将*处理器利用率*作为一列添加，可以显示所有进程（包括 *SAM*）消耗了多少处理器资源。

现在你可以选择一个进程及其要执行的*操作*。当你选择一个进程进行终止并选择*操作*菜单中的*安全终止*时，你会看到一条消息，指示被终止的进程编号，并说明可能需要几分钟时间才能干净利落地终止它。如果你选择一个进程进行终止并选择*操作*菜单中的*强制终止*，你不会得到任何反馈；SAM 只是终止进程，然后你继续下一步。

第 5 章介绍了 *kill* 命令。为了省去你向前翻页的麻烦，我在这里包含了一些与 *kill* 相关的信息。*kill* 命令可以是 `/usr/bin/kill` 或者属于 POSIX shell 一部分的 *kill*。POSIX shell 是 HP-UX 11i 的默认 shell。其他 shell 也提供了自己的 *kill* 命令。我们在 UNIX 世界中总是使用“终止进程”这个短语。我认为，这是因为它与“杀死”这个强有力的含义相关联。我们真正要说的是我们希望终止一个进程。这种终止是通过信号完成的。最常发送的信号是“SIGKILL”，它会终止进程。你可以向进程发送其他信号，但 SIGKILL 是最常见的。作为发送信号的替代方案，你可以发送相应的信号编号。以下列出了信号编号和相应的信号：

我从 **kill** 手册页获取了这份进程列表。若要终止进程 ID 为 234 的进程，你需要发出以下命令：

```
$ kill -9 234
│
├──────────────> process id (PID)
│
├──────────────> signal number

> kill command to terminate the process
```

从 *操作* 菜单中选择的最后一项是*修改 Nice 优先级*，针对你选择的进程。如果你阅读 *nice* 的手册页，你会很高兴地发现可以使用 SAM 来修改它。在 SAM 中修改 *nice* 值只需选择一个进程，并在允许的范围内指定其新的 *nice* 值。

### 调度 Cron 作业

*计划任务 Cron 作业*菜单选择列出了你安排的所有 **cron** 作业，并允许你通过 *操作* 菜单*添加*、*放大*、*移除*和*修改* **cron** 作业。**cron** 在本章前面的“备份和恢复”中已经描述过。为了省去你向前翻页的麻烦，我包含了一些前面介绍的 **cron** 背景信息。

**crontab** 文件用于调度由 **cron** 自动执行的作业。**crontab** 文件位于 */var/spool/cron/crontabs* 目录中。

**cron** 是一个在指定时间运行其他程序的程序。**cron** 读取指定要执行的操作以及执行日期和时间的文件。

**crontab** 文件中条目的格式如下：

```
minute hour monthday month weekday user name command
```

- *minute* - 一小时的分钟数，从 0-59
- *hour* - 一天的小时数，从 0-23
- *monthday* - 一个月中的日期，从 1-31
- *month* - 一年中的月份，从 1-12
- *weekday* - 一周中的星期几，从 0（周日）- 6（周六）
- *user name* - 如有必要，将运行命令的用户
- *command* - 指定要运行的命令行或脚本文件

你在 **crontab** 文件中有许多选项来指定执行任务的 *minute*、*hour*、*monthday*、*month* 和 *weekday*。你可以在一个字段中列出条目，然后是一个空格，多个由逗号分隔的条目，两个由破折号分隔表示范围的条目，或者星号（对应于该字段的所有可能条目）。

若要列出 **crontab** 文件的内容，你需要发出 **crontab -l** 命令。

## 例常任务

在 SAM 的 *例常任务* 下存在以下子区域：

- 备份和恢复
- 选择性文件移除
- 系统日志文件
- 系统关机

*例常任务*的层级结构如图 11-49 所示。请注意，*备份和恢复* 与本章前面讨论的 SAM 顶级 *备份和恢复* 区域相同。

![](img/eff8b9287a5f38c5adf538f24aacf29e_745_0.png)

图 11.49 例常任务菜单结构

### 备份和恢复

这与此前本章中介绍的备份和恢复区域相同。

## 选择性文件移除

*选择性文件移除* 允许你搜索要移除的文件。你可以指定多种标准来选择要移除的文件，包括以下内容：

**文件类型** 你可以搜索三种不同的文件类型：*大文件*、*无主文件* 和 *核心文件*。弹出菜单允许你选择要搜索哪些文件。对于*大文件*，你正在搜索未在规定时间内修改过的最小大小文件。*无主文件* 是由有效系统用户以外的人拥有的文件。*核心文件* 包含在特定条件下终止进程时的核心映像。核心文件通常与进程问题有关，包含数据、堆栈等信息。

**挂载点** 指定是否要搜索非 NFS 挂载点。如果你选择 *是*，这意味着搜索将包括系统中的挂载点，但不会扩展到 NFS 挂载点。我在示例中没有选择包含其他挂载点。

**起始路径** 你的搜索可以从系统层级中的任意点开始。你可以在此字段中指定搜索的起点。如果你只想搜索 *home* 目录中的文件，则将此条目更改为 */home*，你只会搜索该目录，如我在示例中所做的那样。

**最小大小** 指定你要搜索的最小字节大小的文件。小于此大小的文件不会作为搜索的一部分报告。示例中的最小大小为 500,000 字节。

**最后修改时间** 如果你选择 *大文件*，你可以在此字段中输入条目。你输入自文件最后修改以来的最少天数，并在此时间段内修改过的文件将从搜索中排除。示例中为 30 天。

图 11-50 显示了指定要搜索哪些文件的示例：





![](img/eff8b9287a5f38c5adf538f24aacf29e_748_0.png)

**图 11.50 搜索待删除的文件**

删除文件的方法是从一个异常大的文件大小开始，然后逐渐减小尺寸进行搜索。也许您的系统中有一些“意外”的大文件，您可以将其删除而忽略较小的文件。

### 系统日志文件

*系统日志文件* 用于管理系统日志文件的大小。HP-UX 出于各种原因生成日志文件，包括备份、关闭、*cron* 等。您的应用程序也可能正在生成日志文件。其中一些日志文件的大小可能会无限增长，从而通过增大并崩溃您的系统，在系统中造成潜在的灾难。您可以主动在此子区域管理这些日志文件。

SAM 知道许多由 HP-UX 生成的日志文件。当您进入 *系统日志文件* 子区域时，会列出与这些日志文件相关的信息。您可以补充 SAM 知道的日志文件列表，并在每次进入此子区域时向您显示完整的日志文件列表。每次进入此子区域时，SAM 都会列出与日志文件相关的以下信息。（您可能需要增加窗口大小才能看到所有这些信息。）

**文件名**

日志文件的完整路径名称。

**百分比满**

SAM 拥有其认为的日志文件最大大小。您可以通过从 *Actions* 菜单中选择 *修改推荐大小* 来更改此大小。*百分比满* 是日志文件消耗的推荐大小的百分比。

**当前大小**

列出了文件的字节大小。您可能希望查看一下。日志文件的当前大小可能比您希望的要大得多。然后您可以更改推荐大小，并快速查看哪些文件大于 100%。反之亦然。您可能认为日志文件的推荐大小太小了，并将推荐大小更改为更大的值。无论哪种情况，您都希望快速查看哪些文件远大于推荐值。

**推荐大小**

这是您定义的文件推荐大小。检查以确保您同意此值。

**系统中存在**

如果该文件确实存在于您的系统上，则为“是”；如果不存在，则为“否”。如果文件不存在于您的系统中，并且它根本不适用于您，那么您可以从 *Actions* 菜单中选择 *从列表中移除*。例如，您可能没有运行 UUCP，因此希望删除所有与 UUCP 相关的日志文件。

**文件类型**

列出的文件类型仅有 *ASCII* 和 *非 ASCII*。我发现 */var/sam/log/samlog* 并不是列表中的日志文件之一。这不是一个 ASCII 文件，必须通过 *Actions* 菜单中的 *查看 SAM 日志* 来查看，但它确实是一个我认为应该出现在列表中的日志文件。

您可以使用 *Actions* 菜单中的 *修剪* 命令来修剪日志文件。然后，您有几个与文件大小相关的选项，例如修剪完成时的大小等。

### 系统关闭

SAM 为您提供以下三种关闭系统的方法：

- *停止系统*
- *重启（重新启动）系统*
- *进入单用户状态*

此外，您还可以指定关闭发生前的分钟数。

### 在远程系统上运行 SAM

我认为 SAM 非常棒。如果它在一个系统上运行良好，那么作为系统管理员，您不妨从中央控制点在其他系统上使用它。在远程系统上运行 SAM 允许您设置从中央控制点远程运行 SAM 的系统。

您可以指定任意数量的远程系统由中央系统控制。通过 Actions 菜单，您可以从以下选项中进行选择：

- **添加系统**：打开一个窗口，您可以在其中指定您希望在本地管理的远程系统的名称。
- **运行 SAM**：您可以选择要在其中运行 SAM 的远程系统。
- **移除系统**：可以从将在其上远程运行 SAM 的系统列表中移除远程系统。

### 软件管理

SAM 下的软件管理使用 Software Distributor-HP-UX（我将称之为 Software Distributor），这已在第 1 章中详细介绍。SAM 为您提供了一个 Software Distributor 界面，允许您通过选择要执行的任务来执行软件管理。最终，所有相同的 Software Distributor 命令都会运行，因此我不会在本节中再次介绍它们。SAM 中软件管理下存在以下子区域：

- 复制软件到 Depot
- 安装软件到本地主机
- 列出软件
- 移除软件

*软件管理* 的层次结构如图 11-51 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_753_0.png)

从该图中可以看出，当您选择要执行的任务时，SAM 正在选择要运行的 Software Distributor 命令。第 1 章涵盖了许多此类命令。

### 时间

SAM 的时间区域允许您配置网络时间协议（NTP）并设置系统时钟。NTP 是一项服务，允许您利用世界协调时间服务器同步所有系统的时间。除了说明 NTP 配置可能有些棘手，因此使用 SAM 可以大大简化 NTP 之外，我不打算涵盖 SAM 的此区域。

### NFS 无盘概念

我没有将 NFS 无盘作为管理区域来涵盖，而是偏离了本章贯穿始终的格式，转而提供关于 NFS 无盘的简要描述。

该主题在 HP-UX 10.x 中引入。无盘节点在 HP-UX 9.x 及更早版本中通过分布式 HP-UX（DUX）实现。分布式 HP-UX 首次于 1986 年在 HP-UX 6.0 中引入，并在许多 HP 安装中成功使用。HP-UX 10.x 的无盘节点新实现方式是 NFS 无盘。它具有许多理想的功能，包括以下内容：

- NFS 无盘是当前的事实标准。
- 它不是专有解决方案。
- 高端无盘服务器和客户端可以是对称多处理系统。
- 有许多可用的文件系统类型和功能，例如 UNIX 文件系统、日志文件系统、逻辑卷管理器、磁盘镜像等。
- 全书描述的 System V Release 4 文件系统布局已实现。此文件系统布局有利于广泛的文件共享，这在 NFS 无盘中使用。
- 支持只读 NFS 挂载，例如 **/usr** 和 **/opt/**<i>application</i>**。
- 已移除分布式 HP-UX 功能，例如上下文相关文件。
- 服务器可以是 Series 700 和 Series 800 单元。
- 物理链路无关紧要，因此服务器可以使用许多接口，如 IEEE 802.3 和 FDDI。服务器还可以将一些无盘系统分配给一个网卡，其他系统分配给其他网卡。
- 无盘系统可以通过网关启动，从而允许使用子网。
- 使用标准引导协议（BOOTP）和简单文件传输协议（TFTP）实现启动。
- 客户端可以交换到本地磁盘，或者使用 NFS 交换到远程磁盘。

NFS 无盘还有许多其他功能；然而，由于我们的重点是管理，让我们更仔细地看看。使用 SAM，可以执行所有与 NFS 无盘管理相关的任务。这意味着您拥有集群的单个管理点。您可以管理集群范围内的资源，例如打印机和文件系统，这些资源可以从集群中的任何节点进行管理。如果节点不可达，您可以将某些操作延迟到稍后时间执行。当然，您还可以在 SAM 中添加和删除客户端。

使用 SAM，您可以为多个 NFS 无盘系统获得单个管理点。这意味着在 SAM 中执行的操作会影响集群中的所有系统。SAM 中的单个管理点区域包括：



- 打印机/绘图仪
- 文件系统
- 用户/组
- 主目录
- 电子邮件
- 备份

虽然关于无盘 NFS 以及该领域相对于分布式 HP-UX 的诸多改进可以讨论的内容很多，但从管理角度来看，关键点是 SAM 为无盘 NFS 管理提供了集中管理点。与无盘 NFS 管理相关的所有任务都可以通过 SAM 执行。

### 服务控制管理器（SCM）概述

SCM 允许您在多台系统上复制任务。传统上需要在许多系统上单独执行的任务，现在可以在由 SCM 管理的集群的多台系统上执行。

您可以将在单个系统上运行的命令或工具（如 **find** 或 **df** 命令）分发到多台系统上运行，并在 SCM 中收集结果以供审阅。

设计用于在多台系统上运行的更高级工具，例如 Ignite-UX，也可以使用 SCM 以相同的方式运行。

通过 SCM，可以将特定任务分配给特定个人，从而创建基于角色的环境。这消除了对系统 root 访问的需求，因为特定的管理活动被分配给特定节点上的特定用户。这些用户角色在为定义个人用户可以执行的任务时提供了极大的灵活性。

您可以定义组成 SCM 集群的系统。在 SCM 环境中，中央管理服务器（CMS）是执行管理的焦点。受管节点上的代理与 CMS 通信以执行管理功能。

SCM 包含在 11i 的应用介质中，并像其他应用程序一样通过软件分发器进行加载。

从 HP-UX 11i 应用程序 CD-ROM 加载 SCM 后，我们将运行名为 **mxsetup** 的程序来设置 SCM。与 SCM 相关的大多数程序都以“**mx**”开头，应用程序本身加载在 **/opt/mx** 中，而 SCM 数据仓库保存在 **/var/opt/mx** 中。

```
# mxsetup

Please enter the ServiceControl repository password

Please re-enter the ServiceControl repository password

Please enter a name for your Managed Cluster
(default name: ‘HP Managed Cluster’): servicecluster

Please enter the login name of the initial ServiceControl trusted user
martyp

Would you like mxsetup to backup the ServiceControl repository after
it has initially configured it?(Y/N) [Y]:

Please enter the file path where mxsetup will store the backup data
(default path: /var/opt/mx/data/scm.backup):
```

```
You have entered,

ServiceControl Managed Cluster Name : servicecluster
Initial ServiceControl trusted user : martyp
Backup the ServiceControl repository : Y
Backup file path : /var/opt/mx/data/scm.backup

Would you like to continue? (Y/N) [Y] : 
```

请输入 mxsetup 将备份数据存储的文件路径（默认路径：/var/opt/mx/data/scm.backup）：

```
You have entered,

ServiceControl Managed Cluster Name : servicecluster
Initial ServiceControl trusted user : martyp
Backup the ServiceControl repository : Y
Backup file path : /var/opt/mx/data/scm.backup

Would you like to continue? (Y/N) [Y] : 
```

=====================================================================
ServiceControl Manager 配置有 'B' 个任务，配置可能需要一段时间。

请等待 mxsetup 配置 ServiceControl 管理器...
=====================================================================
1: 创建代理仓库..
2: 将 ServiceControl 受管集群命名为 'servicecluster'........................ 完成
3: 配置 ServiceControl 守护进程............ 完成
4: 启动 ServiceControl 守护进程.............. 完成
5: 安装 AgentConfig....................... 完成
6: 初始化 ServiceControl...................... 完成
7: 添加工具 ..................................... 完成
8: 备份仓库........................ 完成
ServiceControl 管理器配置成功
详情请参阅 /var/opt/mx/logs/scmgr-setup.log。

要启动 ServiceControl 管理器：
- 设置 DISPLAY 环境变量
- 并输入 '/opt/mx/bin/scmgr'
#

设置完成后，您可以运行 **ps** 查看以 *mx* 开头的进程，以查看为运行 SCM 而启动的守护进程。

设置好 SCM 后，我们现在可以运行其图形界面 */opt/mx/bin/scmgr*，如图 11-52 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_759_0.png)

图 11-52 *ServiceControl 管理器 scmgr* 屏幕

显示的四个图标是您在 SCM 中执行的任务的启动点，如下所述：

1. *节点组* 提供受管节点的组视图。显示节点组后，用户可以在选定的节点组上执行任务。
2. *节点视图* 提供所有受管节点的视图。这是您可以执行各种节点相关任务（如添加和删除节点）的起点。
3. *工具视图* 提供 SCM 工具的视图。
4. *用户视图* 提供属于 SCM 的 HP-UX 用户的视图。可信用户可以从该视图执行各种用户相关任务，例如添加或删除用户。

如果您的所有系统都是 11i，则无需在客户端上加载任何软件即可从中央 SCM 系统管理它们。如果您有 11.0 或 10.20 系统，则客户端系统需要额外软件。您可以从 docs.hp.com 获取*ServiceControl 管理器的规划、安装、配置和更新*文档，其中提供了安装所有 SCM 相关软件的程序。

要添加受管节点，您需进入 *操作 - 新建 - 节点...* 菜单项，然后选择要添加的节点。

在此菜单项下还有一个用于*用户和角色*的标签区域。在图 11-53 中，我们添加了具有*操作员*角色的用户 *martyp*：

![](img/eff8b9287a5f38c5adf538f24aacf29e_761_0.png)

图 11-53 为新节点上的用户选择*操作员*角色

在添加节点并将其分组，以及添加用户并定义其角色后，您就设置好了 SCM 管理环境。您可以使用预定义的用户工具，也可以添加自己的自定义工具。

图 11-54 显示了 SCM 中预定义的一些软件管理工具：

![](img/eff8b9287a5f38c5adf538f24aacf29e_762_0.png)

**图 11-54** **SCM 软件管理工具**

图 11-54 中显示的工具是软件管理的默认工具。您也可以定义和添加自己的工具。请注意图左侧显示的工具类别。

从图 11-54 所示的图形环境中，您可以启动 SCM 相关的工作。您也可以从命令行与 SCM 配合使用。表 11-3 列出了您可以在命令行中发出的一些常用 SCM 命令：

## 表 11-3 常用 SCM 命令

| 命令 | 描述 |
| --- | --- |
| mxauth | 在 SCM 中添加、删除或列出授权。 |
| mxexec | 运行 SCM 工具。 |
| mxngroup | 在 SCM 中添加、修改、删除或列出节点组。 |
| mxnode | 在 SCM 中添加、删除或列出节点。 |
| mxrepositoryrestore | 恢复 SCM 仓库。 |
| mxrepositorysave | 备份 SCM 仓库。 |
| mxrole | 列出或修改 SCM 角色。 |
| mxsetup | 设置或卸载 SCM 管理集群的中央管理服务器。 |
| mxtool | 在 SCM 中添加、修改、删除或列出工具。 |
| mxuser | 在 SCM 中添加、修改、删除或列出用户。 |

要查看 SCM 角色，请发出以下命令：

```
# mxrole -1t
```

| 名称 | 启用？ | 描述 |
| --- | --- | --- |
| role16 | true | 供 ServiceControl 管理员使用 |
| role15 | true | 供 ServiceControl 管理员使用 |
| role14 | true | 供 ServiceControl 管理员使用 |
| role13 | true | 供 ServiceControl 管理员使用 |
| role12 | true | 供 ServiceControl 管理员使用 |
| role11 | true | 供 ServiceControl 管理员使用 |
| role10 | true | 供 ServiceControl 管理员使用 |
| role9 | true | 供 ServiceControl 管理员使用 |
| role8 | true | 供 ServiceControl 管理员使用 |
| role7 | true | 供 ServiceControl 管理员使用 |
| role6 | true | 供 ServiceControl 管理员使用 |
| lvmadmin | true | 供 LVM 管理员使用的角色 |
| operator | true | 供操作员使用的只读角色 |
| webadmin | true | 供 WEB 服务器管理员使用的角色 |
| dbadmin | true | 供数据库管理员使用的角色 |
| Master Role | true | ServiceControl 主角色 |

```
#
```




该输出展示了为 SCM 设置的默认角色及其简要描述。由于在 SCM 的图形化版本中，您可以执行大多数想要的功能，因此我不预期您会在命令行上运行许多功能；不过，了解这些命令的存在总是好的。

## 第12章

## 性能主题

## 性能与虚拟分区

在下面的章节中，我们将运行一些与性能分析相关的命令，以查看这些命令的输出与在非 vPars 系统上看到的输出有何不同。由于我们要涵盖的命令是许多与性能分析相关工作的基础，因此了解这些命令输出的差异非常重要。本章中非 vPars 特定部分涵盖了通用的性能分析。在 vPar 上执行的性能分析方式与在非 vPar 系统上执行的性能分析方式相同，除了某些命令的输出不会显示系统上的所有组件。相反，只会显示并分析专门分配给正在执行分析的 vPar 的组件。这是本章第一部分我们将重点关注的领域，即您将看到的某些常用命令的输出。

从纯性能相关的角度来说，您在带有 vPars 的系统上确实运行了额外的软件，即虚拟分区监视器（Virtual Partition Monitor）。vPars 系统中的一些资源是共享的，这意味着它们由虚拟分区监视器拥有，而不是由某个特定的 vPar 拥有，例如系统总线适配器（System Bus Adapters）和内存控制器（Memory Controller）。虚拟分区软件消耗的整体系统资源极少。vPar 中的组件专门用于其所属 vPar 的运作。这意味着当我们在 vPar 上运行性能分析时，我们只分析专门分配给该 vPar 的组件。

在下面的章节中，让我们来看看一些常用的性能分析命令，并查看 vPar 的输出是什么样的。这绝不是一个命令的详尽列表，但它会让你了解在 vPars 上你会看到什么。

### 带磁盘的 sar 和 ioscan

在您的 vPars 系统上运行 **ioscan** 只会显示包含在该 vPar 中的组件。下面的 **ioscan** 命令搜索名为 *cable1* 的 vPar 上的磁盘，并且只显示连接到 *LBA 0/0, 0/0* 的磁盘。当使用 *-a io:io/:* 创建 *cable1* 时，*LBA 0/0, 0/0* 是其唯一的 I/O 组件。

```bash
# ioscan -func C disk
Class  I  H/W Path          Driver  B/W State   H/W Type   Description
------  --------  -----------  -----------  ----------  ---------
disk      0  0/0/1/0.0.0     /dev/dsk/c0t10d0  DEVICE    dr
                                             /dev/rdsk/c0t10d0
disk      1  0/0/1/1.0.0     /dev/dsk/c1t0d0   CLAIMED   DEVICE    SBA LBT 111
                                             /dev/dsk/c1t0d0
disk      2  0/0/1/1.0.0     /dev/dsk/c1t0d0   CLAIMED   DEVICE    SBA LBT 111
                                             /dev/rdsk/c1t0d0
disk      3  0/0/2/0.0.0     /dev/dsk/c2t0d0   CLAIMED   DEVICE    SBA LBT 2
                                             /dev/rdsk/c2t0d0
disk      4  0/0/2/2.0.0     /dev/dsk/c2t2d0   CLAIMED   DEVICE    SEAGATE ST173404LC
                                             /dev/rdsk/c2t2d0
```

此列表显示四个内部磁盘分别位于 SBA 0、LBA 0 以及 SCSI 总线 1 和 2 上。在撰写本文时，这些磁盘必须位于同一个 vPar 中，因为它们位于同一个 LBA 上。

连接到该服务器的磁盘远不止前面列表中显示的这些；但是，那些磁盘连接到不属于 *cable1* 的 LBA，因此不会显示在该列表中。

**sar -d** 的以下输出仅显示配置到 *cable1* 中的那个磁盘的性能数据。该输出产生时，系统中另一个 vPar（*cable2*）正在其上运行的磁盘并未显示在此输出中：

```bash
# sar -d 3

HP-UX cvhdc03  B.11.11 U 9000/800    10/16/01

14:28:42  device     %busy  average  trans/s  blks/s  await    avserv
14:28:46  c1t2d0     0.25    0.50     1        2      0.49     8.29
14:28:50  c1t2d0     0.50    0.50     1        2      1.49     8.77
14:28:54
Average    c1t2d0     0.25    0.50     1        2      0.92     8.50
```

你需要连接到另一个 vPar（在本例中是 cable2），并运行 iostat 和 sar -d，以获取 cable2 正在运行的磁盘的设备列表和性能数据。这是 vPar 在同一个服务器上运行就像独立服务器一样运作的一个清晰例子。所有的 vPar 都运行着各自实例的 HP-UX 11i 和应用程序，必须像独立的服务器一样进行分析。

### uptime

uptime 生成关于系统启动时间以及一些负载数据的信息。让我们对同一服务器上运行的两个不同的 vPar 运行此命令，如下所示：

```bash
# hostname
cvhdc03
### uptime
2:32pm up 3:02, 2 users, load average: 2.26, 1.96, 1.60
# hostname
cvhdc04
### uptime
2:31pm up 2:41, 2 users, load average: 0.25, 0.22, 0.23
#
```

uptime 生成的信息是 vPar 特定的。在此输出中我们看到的第一个输出是第一个 vPar 启动的时间，第二个输出是第二个 vPar 启动的时间。此输出中的其他信息也是针对运行 uptime 的特定 vPar。与你在 vPar 运行时执行的大多数命令一样，你将看到 vPar 特定的信息，而不是系统特定的信息。

接下来，我们将查看 vPar 中的一些网络命令。

### 网络

命令生成的网络信息也取决于你发出命令的 vPar。vPars 的网络配置在第13章中有介绍。让我们看看同一服务器上配置的两个不同 vPars 的网络接口。首先，让我们看看主机名为 cvhdccon3 的 vPar cable1 的输出：

```bash
# hostname
cvhdccon3
# netstat -I lan0
Name   Mtu Network     Address         Ipkts    Ierrs Opkts    Oerrs Coll
lan0   1500 172.16.15.0 cvhdccon3      12785     0   11855    0      3
# 
# netstat -ln
Name   Mtu Network     Address         Ipkts    Ierrs Opkts    Oerrs Coll
lan0   1500 172.16.15.0 172.16.15.36  12990     0    12052    0      3
lo0    4336 127.0.0.0   127.0.0.1       7616     0    7616     0      0
# 
# lanscan
Hardware Station  Crd Rtw  Net-Interface  NM      MAC     HP-DLIP  DLPI
Path     Address   In# State Name       FPA ID     Type     Support M/#
0/0/0/0 0x00306B046F6BA 0    up   lan0     snap0 L       ETHER   Yes    219
# 
```

此输出显示，lan0 是此服务器上专门分配给 vPar cable1 的网络接口。lanscan 输出显示该接口的硬件路径为 0/0/0/0。这是在创建 vPar 时使用 -a io:0/0 配置为该 vPar 组件的核心 I/O 卡。创建 cable1 时没有明确调出核心 I/O 卡上的 LAN 接口，因为 0/0/0/0 是位于 0/0 的核心 I/O 卡的隐含组件。

现在我们来看看在这个服务器上运行的第二个 vPar，称为 cable2，主机名为 cvhdccon4：

```bash
# hostname
cvhdccon4
# netstat -I lan1
Name   Mtu Network     Address         Ipkts    Ierrs Opkts    Oerrs Coll
lan1   1500 172.16.14.0 cvhdccon4     3463      0    1603     0      2
# 
# netstat -ln
Name    Mtu   Network           Address       Ipkts Ierrs Opts  Cerrs Coll
lanl    1500  172.16.14.0       172.16.14.44  3619  0     1545  0     2
lo0     4136  127.0.0.0         127.0.0.1     916   0     916   0     0
# 
# lanscan
Hardware Station     Crd Idw Net-Interface IM      MAC                 HP-DLPI DLPI
Fach  Address        0/0/8 State Name*TPA          ID Type             Support BITS
C/10/0/0  0x0010680053658  1   UP  lanl snapi        1 ETHER          Yes     119
s
```

此输出显示，lan1 是此服务器上专门分配给 vPar cable2 的网络接口。lanscan 输出显示该接口的硬件路径为 0/0/10/0/0。LBA 0/0/10/0/0 在创建 vPar 时使用 -a 10:0/10/0/10 配置为该 vPar 的组件。与作为隐含组件的核心 I/O 卡上的 LAN 接口不同，此 LAN 接口位于单独的 PCI 插槽和 LBA 中，因此在创建 vPar 时必须明确指定。

在 cable1 上运行 lanadmin 会产生更详细的与 lan0 相关的输出，如下所示：

```bash
##### lanadmin

LOCAL AREA NETWORK ONLINE ADMINISTRATION, Version 1.0
          Mon, Oct 15, 2001  14:41:23

     Copyright 1994 Hewlett-Packard Company.
             All rights are reserved.

Test Selection mode.

        lan     = LAN Interface Administration
        menu    = Display this menu
        quit    = Terminate the Administration
        tetera  = Do not display command menu
        verbose = Display command menu

Enter command: lan

LAN Interface test mode. LAN Interface PPA Number = 0

        clear   = Clear statistics registers
        display = Display LAN Interface status and statistics registers
        end     = End LAN Interface Administration, return to Test Selection
        menu    = Display this menu
        ppa     = PPA Number of the LAN Interface
        quit    = Terminate the Administration, return to shell
        reset   = Reset LAN Interface to execute its selftest
        specific = Go to Driver specific menu

Enter command: d

                    LAN INTERFACE STATUS DISPLAY
                    Mon, Oct 15, 2001  14:42:33

PPA Number         =      0
Description        =  lan0  HP PCI 10/100Base-TX Core [100BASE-TX,HD, AUTO, TT=1500
Type (value)       =   ethernet-commacd(6)
MTU Size           =   1500
Speed              =   100000000
Station Address    =   0x360056f8ba
```





管理状态（值）       = 正常(1)
操作状态（值）            = 正常(1)
最后更改                         = 775
入站八位字节                      = 2101014
入站单播数据包             = 2830
入站非单播数据包         = 1692
入站丢弃                    = 0
入站错误                      = 0
入站未知协议           = 72
出站八位字节                     = 1164028
出站单播数据包            = 3613
出站非单播数据包        = 8
出站丢弃                   = 0
出站错误                     = 0
出站队列长度               = 0
特定                            = 655367

按 <Return> 继续

该 `lanadmin` 输出显示 *lan0* 为 *cable1* 上配置的网络接口。现在让我们在 *cable2* 上运行 `lanadmin`，看看它生成了哪个网络接口的输出：

```
##### lanadmin
```

```
         局域网在线管理。版本 1.0
                星期一，2001年10月15日  14:45:23

                        版权所有 1994 年 惠普公司。
                                 保留所有权利。
```

测试选择模式。

```
lan     = 网络接口管理
menu    = 显示此菜单
quit    = 终止管理
terse   = 不显示命令菜单
verbose = 显示命令菜单
```

输入命令：lan

网络接口测试模式。网络接口 PPA 编号 = 1

```
clear   = 清除统计寄存器
display = 显示网络接口状态和统计寄存器
end     = 结束网络接口管理，返回到测试选择
menu    = 显示此菜单
ppa     = 网络接口的 PPA 编号
quit    = 终止管理，返回到 shell
reset   = 重置网络接口以执行其自检
specific= 进入驱动程序特定菜单
```

输入命令：d

```
                  网络接口状态显示
                     星期一，2001年10月15日  14:40:49
```

入站非单播数据包   = 21708
入站丢弃              = 0
入站错误                = 0
入站未知协议     = 20720
出站八位字节               = 401517
出站单播数据包      = 3189
出站非单播数据包  = 7
出站丢弃             = 0
出站错误               = 0
出站队列长度         = 0
特定                      = 655367

按 <Return> 继续

该 `lanadmin` 输出显示 *lan1* 为 *cable2* 上配置的网络接口。

当在 vPar 中发出命令时，产生特定于该 vPar 的信息是您在 vPar 命令行工作时可以预期的结果。

接下来，让我们看一下 GlancePlus/UX 输出的几个例子。

###### HP GlancePlus/UX

在 vPars 中操作 Glance 与在非 vPars 系统上操作 Glance 是相同的，除了使用 vPars 时，您将在 Glance 中看到仅分配给正在分析的 vPar 的组件。这意味着如果您在一个系统上运行两个 vPars，您将在想要执行分析的任意 vPar 中运行 Glance。

图 12-1 显示了 vPar *cable1* 的 Glance 屏幕截图，其主机名为 *cvhdccon3*：

![](img/eff8b9287a5f38c5adf538f24aacf29e_773_0.png)

# **图 12-1** HP GlancePlus/UX 显示 vPar 的两个 CPU

图 12-1 显示该 vPar 中存在两个 CPU。运行此 vPar 的系统是一个四处理器 L 类系统。该 vPar 仅配置了两个 CPU，因此，尽管这是一个四处理器系统，但此 vPar 的 Glance 屏幕截图中只显示了两个。您可能会问其他处理器在哪里？可能是因为配置了其他处理器的 vPart(s) 甚至没有运行，所以此时这些 CPU 可能未被使用。也可能是其他 vPart(s) 正在运行，并且根据额外 vPart(s) 的配置，额外的一或两个 CPU 正在使用。如果其他 vPart(s) 正在运行，在这些 vPars 中调用 Glance 将显示正在使用的额外 CPU(s)。

构成 vPar 的其他组件也将显示在 Glance 中。图 12-2 显示了 vPar *cable1* 的磁盘：

![](img/eff8b9287a5f38c5adf538f24aacf29e_774_0.png)

这与我们在 `ioscan -funcC disk` 输出中看到的 *cable1* 磁盘列表相同。图 12-2 中显示的第一个磁盘已被包含在产生 Glance 屏幕截图的 vPar 中。显示的其他设备也连接到作为在创建 vPar 时包含 -a `io:0:0:0` 的 Core I/O 卡一部分的 SCSI 通道。引导磁盘在创建 vPar 时通过 -a `io:0:0:0.1.1.2:0:BOOT` 明确包含，因此预计它会在 Glance 中显示。其他设备也是 vPar 的一部分，因为它们是 *0:0* LBA 的一部分。该 vPar 还有其他隐含组件，包括位于 *0/0/0/0* 的网络接口和位于 *0/0/4/0* 的 console。有关 vPars 创建方式的更多信息，请参阅第 2 章以及本书中提供的撕裂卡。

本章的其余部分包括用于性能分析的命令和工具的背景信息。

### 章节非 vPar 特定部分：简介

您可以采用多种方法对系统进行性能分析。这些选择从只需几秒钟即可创建的快速快照，到您可能需要运行数周或数月甚至开始分析其产生的数据之前才运行的长期容量规划程序。本章包含来自多种系统的示例，包括 HP-UX 11i 系统。我保留了非 HP-UX 系统的示例，因为我的书的某些读者来自 HP-UX 以外的 UNIX 变体。本章中大多数 HP-UX 示例已更新以反映 11i 系统，然而，我不清楚这些性能示例在 11i 和 11.0 之间有任何差异。

在本章中，我们将重点关注一些常用的 UNIX 命令和几个运行在多种 UNIX 变体上的高级工具。这些绝非与性能管理相关的 UNIX 命令和工具的详尽列表；然而，我提供了足够的良好信息供您概览。您的 UNIX 系统可能支持额外的命令并具有高级性能分析工具。本章将提供性能分析的良好概览，包括最常用的 UNIX 性能相关命令的示例。

#### 标准 UNIX 命令

首先，让我们看看一些您可以从 UNIX 提示符发出的命令，以获取关于系统的一些信息。我要涵盖的命令是：

- `iostat`
- `vmstat`
- `netstat`
- `ps`
- `kill`
- `showmount`
- `swapinfo` 和 `swap`
- `sar`

我们将首先查看这些命令中的每一个，以便您理解它们产生的输出以及如何使用该输出。在您的 HP-UX 系统上，许多涵盖的命令都有联机手册页。

请记住，正如我们涵盖的所有主题一样，这些命令的输出在 UNIX 变体之间可能略有不同。在大多数 UNIX 变体上产生的基本信息是相同的；然而，输出的格式可能略有不同。如果您正在查看输出，这通常并不重要；然而，如果您正在编写接受这些输出并以某种方式操作它们的程序，则输出的格式很重要。

##### 使用 iostat 查看 I/O 和 CPU 统计信息

`iostat` 命令为您提供 CPU 在 I/O 上投入的努力程度以及在磁盘和终端之间发生的 I/O 量的指示。`iostat` 提供许多有用信息；然而，它在不同的 UNIX 变体中表现略有不同。以下示例显示在 Solaris 系统、HP-UX 系统和 AIX 系统上发出 `iostat`。用于本章的 Linux 系统不支持 `iostat`。请注意，在某些系统中，使用 -t 选项获取终端信息仅产生终端信息，而在某些系统中它产生完整输出。当然，您必须根据您的 UNIX 变体确定最适合您需求的选项。以下示例显示 `iostat` 命令：

这是一个在 Solaris 上执行的示例，以五秒间隔执行十次：

```
# iostat 5 10
        tty                 fd0                  fd3                  fd6                  cpu
               kps tps serv        kps tps serv        kps tps serv        kps tps serv       us sy wt id
0       0 0 0 0 0 0        0 0 0 0        3 0 57 0        0 79 0 0          7 49 43
0      49 0 0 0 0 0       14 2 75 0 0 0        0 0 0 0        0 2 0 98
0      16 0 0 0 0 0       0 0 0 0        0 0 0 0        0 0 0 0        0 1 0 99
0      16 0 0 0 0 0       0 0 0 0        0 0 0 0        0 0 0 0        0 1 0 100
0      16 0 0 0 0 0       0 0 0 0        0 0 0 0        0 0 0 0        0 0 0 100
0      16 0 0 0 0 0       0 0 0 0        0 0 0 0        0 0 0 0        0 1 0 99
0      16 0 0 0 0 0       0 0 0 0        6 1 35 0 0        0 0 0 0        0 4 0 96
0      16 0 0 0 0 0       0 0 0 0        0 0 0 0        0 0 0 0        0 0 0 100
```



一个 HP-UX 示例包含以五秒间隔执行五次的 `-t` 选项：

```
# iostat -t 5 5
  tty                     cpu
    tin tout     us  ni  sy  id
      1   58       5   1  10  84

device     bps      sps    msps
c1t2d0      0      0.0     1.0

  tty                     cpu
    tin tout     us  ni  sy  id
      0   30       0   2  26  72

device     bps      sps    msps
c1t2d0    484     249.6    1.0

  tty                     cpu
    tin tout     us  ni  sy  id
      0   31       1   3  23  73

device     bps      sps    msps
c1t2d0    517     256.1    1.0

  tty                     cpu
    tin tout     us  ni  sy  id
      0   35       0   2  23  75

device     bps      sps    msps
c1t2d0    456     254.4    1.0

  tty                     cpu
    tin tout     us  ni  sy  id
      0  444       1   6  38  55

device     bps      sps    msps
c1t2d0    12      6.4     1.4
```

这是一个 AIX 示例，以五秒间隔执行十次：

```
# iostat 5 10

tty:            tin     tout      avg-cpu: %user  %sys   %idle   %iowait
                0.0     0.0                     0.3   1.0    98.4     0.3

Disks:      % tm_act     Kbps     tps   Kb read  Kb writ
hdisk0       0.4        2.7     0.4   2366035  953104
hdisk1       0.0        0.0     0.0      18463  37928
hdisk2       0.3        0.6     0.1    2698903 423284
hdisk3       0.0        0.0     0.0      26875   10000
cd0          0.0        0.0     0.0          0      0

tty:            tout     avg-cpu: %user  %sys   %idle   %iowait
                108.2                      0.0   0.0   99.8     0.2

Disks:      % tm_act     Kbps     tps   Kb_read  Kb_wrt
hdisk0       0.0        0.0     0.0        0      0
hdisk1       0.0        0.0     0.0        0      0
hdisk2       0.0        0.0     0.0        0      0
hdisk3       0.0        0.0     0.0        0      0
cd0          0.0        0.0     0.0        0      0

tty:            tout     avg-cpu: %user  %sys   %idle   %iowait
                108.4                      0.2   0.8   99.6     0.0

Disks:      % tm_act     Kbps     tps   Kb_read  Kb_wrt
hdisk0       0.0        0.0     0.0        0      0
hdisk1       0.0        0.0     0.0        0      0
hdisk2       0.0        0.0     0.0        0      0
hdisk3       0.0        0.0     0.0        0      0
cd0          0.0        0.0     0.0        0      0

tty:            tout     avg-cpu: %user  %sys   %idle   %iowait
                108.4                      0.4   0.2   99.4     0.0

Disks:      % tm_act     Kbps     tps   Kb_read  Kb_wrt
hdisk0       0.0        0.0     0.0        0      0
hdisk1       0.0        0.0     0.0        0      0
hdisk2       0.0        0.0     0.0        0      0
hdisk3       0.0        0.0     0.0        0      0
cd0          0.0        0.0     0.0        0      0

tty:            tout     avg-cpu: %user  %sys   %idle   %iowait
                108.4                      0.0   0.4   99.6     0.0

Disks:      % tm_act     Kbps     tps   Kb_read  Kb_wrt
hdisk0       0.0        0.0     0.0        0      0
hdisk1       0.0        0.0     0.0        0      0
hdisk2       0.0        0.0     0.0        0      0
hdisk3       0.0        0.0     0.0        0      0
cd0          0.0        0.0     0.0        0      0

tty:            tin tout avg-cpu: %user  %sys   %idle   %iowait
                1.0 108.2                   0.0   0.0   99.4     0.0

Disks:      % tm_act     Kbps     tps   Kb_read  Kb_wrt
hdisk0       0.0        0.0     0.0        0      0
hdisk1       0.0        0.0     0.0        0      0
hdisk2       0.0        0.0     0.0        0      0
hdisk3       0.0        0.0     0.0        0      0
cd0          0.0        0.0     0.0        0      0

tty:            tin tout avg-cpu: %user  %sys   %idle   %iowait
                0.0 108.4                   0.0   0.2   99.8     0.0

Disks:      % tm_act     Kbps     tps   Kb_read  Kb_wrt
hdisk0       0.0        0.0     0.0        0      0
hdisk1       0.0        0.0     0.0        0      0
hdisk2       0.0        0.0     0.0        0      0
hdisk3       0.0        0.0     0.0        0      0
cd0          0.0        0.0     0.0        0      0

tty:            tin tout avg-cpu: %user  %sys   %idle   %iowait
                0.0 108.4                   0.0   0.4   99.6     0.0

Disks:      % tm_act     Kbps     tps   Kb_read  Kb_wrt
hdisk0       0.0        0.0     0.0        0      0
hdisk1       0.0        0.0     0.0        0      0
hdisk2       0.0        0.0     0.0        0      0
hdisk3       0.0        0.0     0.0        0      0
cd0          0.0        0.0     0.0        0      0

tty:            tin tout avg-cpu: %user  %sys   %idle   %iowait
                0.0 158.4                   0.0   0.4   99.2     0.0

Disks:      % tm_act     Kbps     tps   Kb_read  Kb_wrt
hdisk0       0.0        0.0     0.0        0      0
hdisk1       0.0        0.0     0.0        0      0
hdisk2       0.0        0.0     0.0        0      0
hdisk3       0.0        0.0     0.0        0      0
cd0          0.0        0.0     0.0        0      0
```

以下是您使用 `iostat` 接收的关于终端、CPU 和已挂载文件系统的报告说明。由于这些报告略有不同，我包含了 HP-UX 输出中的详细信息。这些字段的更详细描述包含在您的 HP-UX 系统上可用的 `iostat` 在线手册页中。大多数字段都会出现在输出中；然而，命令的输出在 UNIX 变体之间略有不同。

对于每个已连接的终端（tty），您会看到“tin”和“tout”，分别代表从终端读取的字符数和写入终端的字符数。

对于 CPU，您会看到用户模式（“us”）所花费时间的百分比、以低优先级运行用户进程（称为 nice，“ni”）所花费时间的百分比、系统模式（“sy”）所花费时间的百分比，以及 CPU 空闲（“id”）时间的百分比。

对于每个本地挂载的文件系统，您会收到关于每秒传输的千字节数（“b/s”）、每秒寻道次数（“sps”）以及每次平均寻道的千字节数（“msps”）的信息。对于通过 NFS 挂载的磁盘或服务器客户端节点上的磁盘，您不会收到报告；`iostat` 仅报告本地挂载的文件系统。

在查看 `iostat` 的输出时，有一些参数需要注意。

首先，注意您的 CPU 在显示的四个类别中花费的时间。CPU 报告是使用 `-t` 选项生成的。我曾在性能不佳的系统上工作，管理员假设这是由于 CPU 缓慢导致的，因为“id”数值非常高，表明 CPU 实际上大部分时间是空闲的。如果 CPU 大部分时间是空闲的，那么瓶颈很可能不是 CPU，而是 I/O、内存或网络。如果 CPU 确实大部分时间都很忙（“id”非常低），请查看是否有进程正在运行“nice”（检查“ni”数值）。可能是一些后台进程消耗了大量的 CPU 时间，可以更改为以“nice”方式运行。

其次，比较正在发生的传输数量。这些通常由诸如每秒块数（b/s）、每秒传输数（t/s）或每秒寻道数（s/s）之类的指标表示。这些数字指示磁盘上正在发生的活动量。如果一个卷持续远高于其他卷，那么它可能执行了不成比例多的工作负载。请注意，在 HP-UX 上，所有磁盘的每次平均寻道毫秒数（ms/s）始终等于一。

##### 使用 vmstat 查看虚拟内存统计信息

**vmstat** 提供虚拟内存统计信息。它提供关于进程状态、虚拟内存、分页活动、缺页中断以及 CPU 时间百分比细分的信息。**vmstat** 在不同 UNIX 变体中的行为略有不同。以下示例展示了在 Solaris 系统、HP-UX 系统、AIX 系统和 Linux 系统上发出 **vmstat** 命令。当然，您必须根据您在特定 UNIX 变体上的需求确定最佳选项。在以下示例中，输出以五秒间隔生成了九次。**vmstat** 命令的第一个参数是间隔；第二个是您希望输出产生次数的参数。

Solaris 示例：

```
$ vmstat 5 9

proc   memory       page        disk       faults        cpu
 r b  w  swap  free re mf pi po fr de aw eo  in sy  cs  us  sy  id
 0 0 0  4480  4896  0 0  1 0  0 0 0 0 0  0  79 864 130 297 0   7 92
 0 0 0 13320  5916  0 3 0 0  0 0 0 0 0  0 102  42  24 0   2 98
 0 0 0 13320  5916  0 0  0 0  0 0 0 0 0  0  78  48 24  0  0 100
 0 0 0 13320  5916  0 0  0 0  0 0 0 0 0  0  74  42 24  0  0 100
 0 0 0 13320  5916  0 0  0 0  0 0 0 0 0  0  35  45 23  0  0 99
 0 0 0 13320  5916  0 0  0 0  0 0 0 0 0  0  52  44 23  0  1 99
 0 0 0 13320  5916  0 0  0 0  0 0 0 0 0  0  53  54 24  0  1 99
 0 0 0 13320  5916  0 0  0 0  0 0 0 0 0  0  60  53 25  0  2 98
```

HP-UX 示例：

```
$ vmstat 5 9

proc    memory       page        faults       cpu
 r  b  w  avm  free  re  at  pl  po  fr  de  aw  eo  in  sy  cs  us  sy  id
 5 240 0 17666  3879  2  0  0  0  0  0  0    0  0  0  778 193 77  3 80
 4 242 0 16722  4106  0  0  0  0  0  0  814 20649 258 89 10  2
 4 240 0 16649  4106  0  0  0  0  0  0  83 18384 213 88  9  8
 4 240 0 16648  4106  0  0  0  0  0  0  782 19552 273 89 11  1
 5 239 0 15630 4012 9 0 0 0 0 0 0 804 18295 270 93 8 1
 5 241 0 16087 3934 6 0 0 0 0 0 0 920 21044 392 89 10 0
 5 241 0 15312 3952 11 0 0 0 0 0 0 868 20239 431 90 10 0
 4 242 0 16577 4043 3 0 0 0 0 0 0 926 19339 409 89 10 0
 6 238 0 17453 4122 0 0 0 0 0 0 0 837 19269 299 89 9 2
```

AIX 示例：

```
martyn $ vmstat 5 9

      kthr  memory          page             faults              cpu
  r  b  swm free re pi po  fr  sr cy in sy cs us sy id wa
  0  0 16604  246  0   0   0   0    2  0 149  79 36  0  0 1  98  0
  0  0 16604  246  0   0   0   0  0.153 126  41  0  0  99  0
  0  0 16604  246  0   0   0   0  0.143  83  33  0  0  99  0
  0  0 16604  246  0   0   0   0  0.140  94  35  0  1  99  0
  0  0 16604  245  0   0   0   0  0.166  62 32  0  0  99  0
  0  0 16604  246  0   0   0   0  0.150 102 38  1  0  99  0
  0  0 16604  246  0   0   0   0  0.183  78 34  0  0  99  0
  0  0 16604  245  0   0   0   0  0.132  87 33  0  1  98  0
  0  0 16604  246  0   0   0   0  0.147  84 38  0  0  99  0
```

Linux 示例：

```
# vmstat 5 5

procs                            memory            swap         io        system      cpu
 r  b   w   swapd  free buff cache si so  bi  bo  in   cs  us sy id
 1  0  0 9432 1160   656 12024  1  2 14   1 138   274  3  1   96
 1  0  0 9684 828    652 12148  0  50  0   14 205 8499  82 18  0
 1  0  0 9684 784    652 11598  0  0   0   1 103  862  81 19  0
 0  0  0 9684 800    652 10996  0  0   0   0  101 8683  80 20  0
 0  0  0 9772 796    652 9824  12 18  3  4 160  6577  66 17 18
```

您当然可以从 `vmstat` 命令中获得大量信息。以下是 vmstat 生成的信息类别的简要说明。由于本章末尾 HP-UX 的手册页，我包含了 HP-UX 示例中字段的描述。但是，您可以看到，输出非常相似。

进程被分类为三种类型之一：可运行（"r"）、因 I/O 或短期资源而阻塞（"b"），或已交换出（"w"）。

接下来您会看到有关内存的信息。"avm" 是过去 20 秒内运行的处理器所拥有的虚拟内存页面数。如果这个数字大致等于物理内存大小减去内核，那么您就接近强制分页了。"free" 列指示系统空闲列表上的页面数。这并不意味着进程已经结束运行且这些页面不会再被访问；它只是意味着这些页面最近没有被访问。我建议忽略这一列。




接下来是页面调度活动。第一个字段（"re"）显示被回收的页面数。这些页面进入了空闲列表，但后来被引用，因此需要重新抢救回来。

接下来你会看到三种类别的缺页中断数量：每秒中断数（通常来自硬件，标记为 "in"），每秒系统调用数（"sy"），以及每秒上下文切换数（"cs"）。

最后的输出是用户（"us"）、系统（"sy"）和空闲（"id"）的 CPU 使用率百分比。这并不如 `iostat` 的输出那么全面，后者还显示了 nice 进程的条目。

如果你正在运行 I/O 密集型工作负载，你确实可能会看到可运行进程（"r"）、阻塞进程（"b"）以及可运行但被换出的（"w"）进程中存在大量活动。如果你有大量可运行但被换出的进程，那么你可能存在 I/O 瓶颈。

##### 使用 netstat 查看网络统计信息

netstat 提供与网络统计相关的信息。因为在某些网络中，网络带宽与 CPU 和内存对性能的影响同样重要，所以你需要了解当前的网络流量水平。

我使用 netstat 的两种形式来获取网络统计信息。第一种是 `netstat -i`，它显示自动配置的接口的状态。虽然 `netstat -i` 提供了主要局域网接口（如所处网络、名称等）的良好概况，但它并不显示有用的统计信息。

以下展示了 `netstat -i` 的输出：

```
# netstat -i
Name Mtu Network Address Ipkts Ierrs Opkts Oerrs Col
lan0 1497 151.150 a4410.e.h.c 242194 120 107665 23 19884
```

netstat 提供了简洁的输出。换句话说，从 netstat 获取的大多数信息都是有用的。以下是对 netstat 示例中九个字段的描述：

-   **Name**：网络接口的名称（Name），在本例中为 "lan0"。
-   **Mtu**："最大传输单元"，即接口卡发送的最大数据包大小。
-   **Network**：接口卡所连接的局域网的网络地址（151.150）。
-   **Address**：主机的名称。如果网络配置使用 /etc/hosts，这是 /etc/hosts 文件中系统的符号名称。

以下是统计信息。根据你使用的系统或操作系统版本，你可能看不到其中一些命令：

-   **Ipkts**：接口卡接收的数据包数量，在本例中为 "lan0"。
-   **Ierrs**：接口卡检测到的入站数据包错误数量。
-   **Opkts**：接口卡传输的数据包数量。
-   **Oerrs**：接口卡在传输数据包过程中检测到的错误数量。
-   **Col**：由数据包流量导致的碰撞次数。

netstat 提供自节点上次启动以来的累积数据；因此，数据可能是在较长的一段时间内累积的。如果你有兴趣查看有用的统计信息，可以使用 netstat 的不同选项。你也可以指定报告统计信息的间隔。我通常忽略第一条记录，因为它显示的是自系统上次启动以来的所有数据。这意味着数据包含了系统空闲的非高峰时段的记录。我更倾向于查看系统处于最高负荷工作时的数据。以下示例展示了在 Solaris、HP-UX 和 AIX 上运行 `netstat -i` 并指定 lan 接口的情况。这些输出几乎相同，尽管网络接口的名称在不同 UNIX 变体中有所不同。netstat 命令以五秒为间隔运行。该命令的 Linux 版本（未显示）不允许我指定间隔。

### Solaris 示例

```
# netstat -I le0 5
```

| | input | | output | | | input (Total) | | output |
|---|---|---|---|---|---|---|---|---|
| | packets | errs | packets | errs | cols | packets | errs | packets |
| (le0) | 18998 | 1189 | 1653100 | 118993180 | 0 | 3474777 | 1189 | 1663100 |
| 12: | 0 | | 0 | 185 | 0 | 1 | 0 | 0 |
| 13: | 0 | | 0 | 273 | 0 | 8 | 0 | 0 |
| 14: | 0 | | 0 | 153 | 0 | 3 | 0 | 0 |
| 15: | 0 | | 0 | 154 | 0 | 3 | 0 | 0 |
| 16: | 0 | | 0 | 124 | 0 | 3 | 0 | 0 |
| 17: | 0 | | 0 | 378 | 0 | 2 | 0 | 0 |
| 18: | 0 | | 0 | 389 | 0 | 4 | 0 | 0 |
| 19: | 0 | | 0 | 286 | 0 | 2 | 0 | 0 |

### HP-UX 示例 (10.x)

```
# netstat -I lan0 5
```

| | output | | | | | (Total)-> input | | output |
|---|---|---|---|---|---|---|---|
| | packets | errs | packets | errs | | packets | errs | packets | errs |
| (lan0)-> | 269841735 | 27 | 256627585 | 1 | 5092223 | 281472199 | 27 |
| 268258048 | 1 | 5092223 | 1602 | 0 | 1238 | 0 | 49 | 1673 | 0 | 1309 | 0 | 49 |
| | | | | | | 1223 | 0 | 1048 | 0 | 25 | 1235 | 0 | 1060 | 0 | 25 |
| | | | | | | 1516 | 0 | 1151 | 0 | 42 | 1560 | 0 | 1195 | 0 | 42 |
| | | | | | | 1553 | 0 | 1188 | 0 | 17 | 1565 | 0 | 1200 | 0 | 17 |
| | | | | | | 2539 | 0 | 2180 | 0 | 44 | 2628 | 0 | 2269 | 0 | 44 |
| | | | | | | 3000 | 0 | 2193 | 0 | 228 | 3000 | 0 | 2193 | 0 | 228 |
| | | | | | | 2959 | 0 | 2213 | 0 | 118 | 3003 | 0 | 2257 | 0 | 118 |
| | | | | | | 2423 | 0 | 1981 | 0 | 75 | 2435 | 0 | 1993 | 0 | 75 |

### AIX 示例

```
# netstat -I en0 5
```

| | input | | output | | | input | | output |
|---|---|---|---|---|---|---|---|
| | packets | errs | packets | errs | cols | packets | errs | packets | errs | cols |
| (eno) | 0 | 1785925 | 0 | 0 | 0 | 47426087 | 0 | 2913405 | 0 | 0 |
| 46333531 | 0 | 1 | 0 | 0 | 0 | 204 | 0 | 2 | 0 | 0 |
| | | 203 | 0 | 1 | 0 | 0 | 298 | 0 | 1 | 0 | 0 |
| | | 288 | 0 | 1 | 0 | 0 | 204 | 0 | 12 | 0 | 0 |
| | | 293 | 0 | 1 | 0 | 0 | 191 | 0 | 1 | 0 | 0 |
| | | 191 | 0 | 1 | 0 | 0 | 191 | 0 | 1 | 0 | 0 |
| | | 150 | 0 | 3 | 0 | 0 | 151 | 0 | 3 | 0 | 0 |
| | | 207 | 0 | 3 | 0 | 0 | 218 | 0 | 15 | 0 | 0 |
| | | 162 | 0 | 3 | 0 | 0 | 162 | 0 | 3 | 0 | 0 |
| | | 120 | 0 | 2 | 0 | 0 | 120 | 0 | 2 | 0 | 0 |

通过这个示例，你可以获得关于 LAN 接口上发生情况的多次输出，包括输出右侧的总数。正如我前面提到的，你可能希望忽略第一个输出，因为它包含了较长时间段的信息。这可能包括网络空闲的时间段，因此这些数据可能对你来说并不重要。

你可以使用 `-I 接口名` 来指定要报告统计信息的网络接口；在示例中，它是 `-I` 加上 `le0`、`lan0` 或 `en0` 中的某一个。本例中还使用了五秒的间隔。

分析 netstat 统计信息很直观。你需要验证碰撞数（Colls）远低于传输的数据包数（Opkts）。碰撞发生在你的 LAN 接口的输出端。你的 LAN 接口遇到的每次碰撞都会拖慢网络速度。关于多少碰撞才算多，你会听到各种各样的意见。如果你的碰撞数少于 "Opkts" 的 5%，那么你的状况可能很好，最好将时间花在其他系统资源的分析上。如果这个数字很高，你可能需要考虑以某种方式对网络进行分段，例如在共享数据不多的网络部分之间安装网络设备等。

作为一条经验法则，如果你减少接收和传输的数据包数量（"Ipkts" 和 "Opkts"），那么整体网络流量就会更少，碰撞也会更少。在规划网络或系统升级时，请牢记这一点。你可能希望在持续通信的系统中配备两个 LAN 卡。这样，这些系统就拥有用于通信的"私有"LAN，而不会对网络上其他系统的性能产生不利影响。每个系统的一个 LAN 接口专门用于系统内部通信。这为通常充当服务器的系统之间提供了一条"紧密"的通信路径。第二个 LAN 接口用于与通常是大型网络中客户端的系统进行通信。

你也可以使用 netstat 获取与路由相关的信息（参见第 13 章）。netstat 的 `-r` 选项显示路由表，这通常是人们需要了解的信息，而 `-n` 选项可用于将网络地址以数字形式而不是名称形式打印出来。在以下示例中，netstat 使用了 `-r` 选项（这将在描述 netstat 输出时使用）以及 `-rn` 选项，以便你可以比较两种输出：



## $ netstat -r

路由表

| 目标 | 网关 | 标志 | 引用 | 使用 | 接口 | Pmtu |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| hp/00 | localhost | UH | 0 | 28 | lo0 | 4608 |
| 默认 | router1 | UG | 0 | 0 | lan0 | 4608 |
| 128.185.61 | system1 | U | 347 | 28668 | lan0 | 1500 |

## $ netstat -rn

路由表

| 目标 | 网关 | 标志 | 引用 | 使用 | 接口 | Pmtu |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 127.0.0.1 | 127.0.0.1 | UH | 0 | 28 | lo0 | 4608 |
| 默认 | 128.185.61.1 | UG | 0 | 0 | lan0 | 4608 |
| 128.185.61 | 128.185.61.2 | U | 347 | 28668 | lan0 | 1500 |

在 **netstat** 中，提供了关于路由器（即中间条目）的一些信息。*-r* 选项显示有关路由的信息，但该命令还有许多其他有用选项。在此输出中，特别值得注意的是“Flags”（标志），它定义了所执行的路由类型。以下是来自我的 HP-UX 系统联机手册页中最常见标志的描述，这些标志在 UNIX 变体之间可能有所不同。

- $U$ = 通过本机本身作为网关路由到一个*网络*。
- $UG$ = 通过远程主机作为网关路由到一个*网络*。
- $UH$ = 通过本机本身作为网关路由到一个*主机*。
- $UGH$ = 通过远程网关（该网关为主机）路由到一个*主机*。

第一行用于本地主机，即称为 *lo0* 的回环接口，其地址为 127.0.0.1（您可以在 **netstat -rn** 示例中看到此地址）。*UH* 标志表明目标地址是本地主机本身。此 A 类地址允许同一主机上的客户端和服务器通过 TCP/IP 相互通信。发送到回环接口的数据报不会发送到网络上，而只会通过回环处理。

第二行用于默认路由。此条目表示，如果找不到更具体的路由，则将数据包发送到 Router 1。在这种情况下，路由器在 Flags 下为 UG。有些路由器配置为 U，而其他路由器（如本例中的路由器）则配置为 UG。我发现我通常需要通过试错法来确定需要 U 还是 UG。如果 Flags 中有 U 且我无法 ping 通路由器另一侧的系统，UG 条目通常能解决这个问题。

第三行用于系统的网络接口 lan0。这意味着对于发送到 128.185.61 的数据包，应使用此网络接口。

##### 使用 ps 检查进程

了解系统上正在运行的进程以及如何停止它们，对系统管理和性能都很重要。

要回答“我的系统在做什么？”这个问题，请使用 ps -ef。此命令提供有关系统上每个运行进程的信息。例如，如果您想知道 NFS 是否正在运行，只需输入 ps -ef 并查找 NFS 守护进程。虽然 ps 告诉您系统上正在运行的每个进程，但它并不提供关于系统资源消耗水平的好总结。我猜测 ps 是最常发出的系统管理命令。ps 有许多可用的选项。我通常使用 e 和 f，它们提供有关所有（“e”）运行进程的信息，并完整列出（“f”）这些信息。不同系统的 ps 输出几乎相同。以下三个示例分别来自 Solaris、AIX 和 HP-UX 系统：

Solaris 示例：

```text
martyn$ ps -ef
UID PR FPID PPID C STIME TTY TIME CMD
root 0 0 0 Feb 18 ? 0:01 sched
root 1 0 0 Feb 18 ? 1:30 /etc/init
root 2 0 0 Feb 18 ? 0:02 pagingd
root 3 0 1 Feb 18 ? 813:44 (aislush)
root 3063 3059 0 Feb 22 ? 0:10 /usr/dt/bin/hsperfclertner - -H r
root 88 1 0 Feb 18 ? 0:02 /usr/bin/in.nutd -g
root 478 0 Feb 18 ? 0:00 /usr/lib/saff/mnc - 300
root 94 0 0 Feb 18 ? 2:50 /usr/sbin/syslogd
root 150 1 0 Feb 18 ? 0:03 /usr/sbin/syslogd
root 96 1 0 Feb 18 ? 0:00 /usr/sbin/keyserv
root 144 Feb 18 ? 50: /usr/lib/autofs/automountd
root 1010 Feb 18 ? /usr/per/bin/mld/daemon
root 106 Feb 18 ? /usr/lib/netcfg/usrp/bpbind -troot
root 156 Feb 18 ? /usr/sbin/cron
root 176 Feb 18 ? /usr/lib/lpschec
root 128 Feb 18 ? /usr/lib/nf/lockd
daemon 130 Feb 18 ? /usr/lib/nf/statd
root 14798 Mar ? 3.8 /usr/sbin/nscd
root 133 Mar ? 1.4 /usr/sbin/smbd -s
root 197 Feb ? 1.2 /usr/lib/powpd/ powerd
root 146 Feb ? .4 /opt/licensed/lgardate. -c /d
root 213 Feb ? 4+03:09 /usr/bin/osvid
root 199 Feb ? .03 suntechd -T 4 -c -qt/optd
root 219 Feb ? .02 /usr/lib/libd/tbd-tsd
root 269 Feb ? /usr/lib/utmpd
root 2335 Feb ? 4+ /usr/openwin/bin/Xenv 10 -nbomanna
root 4728 Feb ? - .
root 2963 Feb ? . /usr/openwin/bin/Xfvconsoldes
root 479 Jun ? 4.80 /usr/lib/afps/g -h -p xunsc
root 10374 Jun ? 0.00 /opt/per/bin/td
root 7468 Feb ? 0.13 /opt/per/bin/pvslard
root 224 Feb ? 0.01 /usr/lib/bin/clogind -daemon
martyP 16763 07:46: ptd4 0.1 .ksh
root 10795 Jun ? 0 /opt/per/bin/periodl
root 484 Feb ? . 30 /usr/lib/aat/ctayson
root 458 Feb ? .24 /usr/lib/anmp/anmpsbd y c <net/f
root 16782 Feb ? .6 /usr/lib/msd/daemon -mode blank
root 471 Feb ? .03 /usr/lib/dm/dmd
root 474 Feb ? .00 /usr/lib/dmir/xmpsDad -a
root 485 Feb ? .4 /usr/lib/bin/dscrecon -y 3974
root 2954 Feb ? 0.2 /bin/ksh /usr/dm/Demo/
root 2936 Feb ? .00 /usr/dt/bin/dtogain -daemon
root 3061 Feb ? . 12 dtwm
root 3058 Feb ? 9.91 /usr/dt/bin/tdsession
root 712 Feb ? .02 pty:tfd/userverd
root 11001 Feb ? 0.01 <defunct
root 2938 Feb ? 0.00 /usr/openwin/bin/fvconsoldes -d 10
root 2939 Feb ptn2 . /usr/dt/birdt/ shell -o ut
root 3059 Feb ptn2 293.15 /usr/dt/bin/DTsession
root 3063 Feb ? .03 /usr/dt/bin/dtclgpreview -help/tegr
root 3099 Feb ? .014 /usr/dt/bin/dtftile -geometry +700
root 11000 Feb ? . 42 /opt/per/bin/agusetserver - t alar/
root 3022 Feb ptn2 . 01 /usr/dt/bin/ unget DT. DIALP2
root 730 Feb ? .17 pty:rstard
root 3062 Feb ? .217 /usr/dt/bin/dfsile -geometry -r 700
root 3067 Feb ? 0.07 /bin/ksh /usr/dt/bin/dtsoldochec
root 3000 Feb ? .00 /usr/dt/bin/tdse
root 3078 Feb ? .0 /bin/cat /tmp/.removeablenotify
root 10396 Jun ? 32.42 /opt/per/kse/p/bin/dsed -b
root 16761 07:46: ? 0.00 telnetd
martyP $
```

AIX 示例：

```text
martyP $ ps -ef
     UID   PID  PPID     C   STIME  TTY TIME CMD
     root    1     0    0 Feb 24     5.07 /init
     root  2208  1521    0 Feb 24     8.22  dcnm
     root  2664  2842    0 Feb 24     0.00 /usr/lib/dm/dloglm -daemon
     root  2882    1    0 Feb 24    158.41 /usr/sbin/syncd 60
     root  3376  2664    5 Feb 24    3594:41 /usr/lib/sxlib/bin/Xs -D /usr/lib/
     root  3624    1    0 Feb 24     0.00 /usr/sbin/sshd -la
     root  3950    1    6 Feb 24     5550:30 /usr/ppc/lfp/bin/libld
     root  4144    1    0 Feb 24     0.00 /usr/ppc/lfp/bin/aidmion
     root  4890    1    0 Feb 24     0.48 /usr/lpp/perf/bin/ptlbod
     root  4996    1    0 Feb 24     0.00 /usr/lfp/arm/daemon
     root  5172    1    0 Feb 24     0.00 /usr/sbin/smartd
     root  5724  5172    0 Feb 24     9.54 /usr/sbin/syslogd
     root  6424  5172    0 Feb 24     0.00 /usr/sbin/biod 6
     root  6450  5172    0 Feb 24     0.32 sendmail: accepting connections
```


## HP-UX 示例（部分列表）

```text
marty% $ ps -ef

    PID    PPID STIME TTY TIME COMMAND
    0      0    Mar 7  ?  107:28 swapper
    1      0    Mar 9  ?  2:27 init
    2      0    Mar 9  ?  14:13 vanda
    3      0    Mar 9  ?  11:43:58 ata/daemon
    4      0    Mar 9  ?  5:57 unhashed
    7      0    Mar 9  ?  154:33 ttsh
```

```text
root 6710 5172 0 Feb 24 - 7.34 /usr/sbin/portmap
root 6956 5172 0 Feb 24 - 0.02 /usr/sbin/initnd
root 7224 5172 0 Feb 24 - 1.08 /usr/sbin/timed -G
root 7842 5172 0 Feb 24 - 11.55 /usr/sbin/smpd
root 8000 1 0 Feb 24 - 0.00 netif
root 8512 8782 1 0 Feb 24 - 9.00 telnet -Cf
root 8782 1 0 Feb 24 - 0.00 /usr/OB/NTU-nti_reader o 1 1 1
root 9036 8000 0 Feb 24 - 10.09 otwdab o -8000
root 9288 8000 0 Feb 24 - 0.44 pcd -A -G -M -Mc -M -M
root 9848 8000 0 Feb 24 - 0.00 trapped -f
root 9804 8000 0 Feb 24 - 0.28 trapd
root 10062 8000 0 Feb 24 - 0.47 orstd
root 10232 8000 0 Feb 24 - 0.31 otwsmd
root 10578 8000 0 Feb 24 - 0.30 otelnd
root 10936 8000 0 Feb 24 - 0.18 otwsmd -O
root 11094 8000 0 Feb 24 - 17.50 netmon -P
root 11852 8000 0 Feb 24 - 0.02 smmpCollect
root 13954 1 0 Feb 24 - 1.22 /usr/sbin/cron
root 12140 5172 0 Feb 24 - 0.01 /usr/lib/tcp/netvcg/ypp/piped
root 12394 5172 0 Feb 24 - 1.28 /usr/sbin/tcp mountd
root 12652 5172 0 Feb 24 - 0.29 /usr/sbin/nfsd 8
root 12908 5172 0 Feb 24 - 0.00 /usr/sbin/rpc.statd
root 13166 5172 0 Feb 24 - 0.53 /usr/sbin/rpc.lockd
root 13428 1 0 Feb 24 - 0.00 /usr/sbin/printfixd
root 14190 5172 0 Feb 24 - 72.59 /usr/sbin/autoconfd
root 14452 5172 0 Feb 24 - 0.17 /usr/sbin/glqademon
root 14714 5172 0 Feb 24 - 0.00 /usr/sbin/rttstatd
root 14992 1 0 Feb 24 - 255.26 /usr/ipp/part/bin/scopeuse
root 15520 3624 1 Feb 24 - 15.29 /usr/df/bin/dtasensorn
root 15998 1 0 Feb 24 1f/0 - 0.00 /usr/bin/diagnostics/bin/diagd
root 16304 18682 0 Feb 24 pte/0 - 0.00 /usr/sbin/getty /dev/console
root 16774 1 Feb 24 pte/0 - 0.00 /bin/ksh
root 17092 4490 0 Feb 24 - 0.00 /usr/ipp/perl/bin/idd
root 27870 18186 1 Mar 25 - 68.54 /usr/ipp/perl/bin/rep_server -t
root 17630 15520 0 Mar 25 - 0.00 <defunct>
root 17898 15520 0 Mar 25 - 0.00 /usr/dt/bin/dtexec -open 0 -ttlp
root 18138 19888 0 Mar 24 pta/1 - 0.00 /usr/dt/bin/dtexec -open 0 -ttlp
root 18166 696 0 Mar 24 - 0.00 /usr/kall
root 18446 15520 0 Mar 15 - 0.00 rpc:ttdserver 100083 1
root 18892 15520 0 Mar 24 - 0.01 /usr/dt/bin/dtexec -open 0 -ttlp
root 19186 16304 0 Feb 24 pts/0 - 3.46 /usr/dt/bin/dtxterm
root 19450 1 0 Feb 24 - 0.01 /usr/XP/11/bin/namixt
root 19864 2208 0 Feb 24 - 0.00 /usr/dt/bin/dtexec -open 0 -ttlp
root 19888 19684 0 Feb 24 - 0.00 /usr/dt/bin/dxserver
root 20104 15520 0 Feb 27 - 0.00 /usr/dt/bin/dtexec -open 0 -ttlp
root 20248 20104 0 Feb 27 - 0.03 /usr/dt/bin/dtexec -open 0 -ttlp
root 20942 29708 0 Mar 14 - 0.03 /usr/dt/bin/dxscreen
root 20912 26306 0 Apr 05 - 0.03 /usr/dt/bin/dxscreen
root 33528 0 May 18 - 3.28 /usr/atria/etc/lockmgr a /var/
root 33834 3666 0 Mar 24 - 0.00 telnetd
root 34072 0 May 18 - 0.00 /usr/atria/etc/sdd_server
marrip 56296 36603 13:07:35.07 pts/2 - 0.00 pss -ef
marrip 36608 33834 1:07:55:50 pts/2 - 0.00 /bin/ksh
root 37220 15520 0 May 28 - 0.00 /usr/dt/bin/dtexec -open 0 -ttlp
INITPID: 1
```

##### 使用 ps 检查进程

```text
root 70 Mar 5 0:04 lvmdk
root 71 Mar 9 0:01 lvmdk
root 72 Mar 9 0:01 lvmdk
root 73 Mar 9 5:54 vx_sch_ed thread
root 74 Mar 9 1:54 vx_iflush_thread
root 75 Mar 9 2:06 vx_free_thread
root 76 Mar 9 2:12 vx_inactive_cache_thread
root 77 Mar 9 0:40 vx_bowril_thread
root 78 Mar 9 ? 0:33 vx_iflush_thread
root 79 Mar 9 ? 0:07 vx_logfsync_thread
root 80 0 0 Mar 9 ? 0:09 vx_inactive_thread
root 81 0 0 Mar 9 ? 0:01 lvmdk
root 82 0 0 Mar 9 ? 0:57 netiser
root 83 0 0 Mar 9 ? 0:18 netiser
root 84 0 0 Mar 9 ? 0:49 netiser
root 85 0 0 Mar 9 ? 0:14 netiser
root 86 0 0 Mar 9 ? 0:48 nvsrler
root 87 0 0 Mar 9 ? 0:00 smpsched
root 88 0 0 Mar 9 ? 0:00 smpsched
root 89 0 0 Mar 9 ? 0:00 smpsched
root 90 0 0 Mar 9 ? 0:00 skbksched
root 91 0 0 Mar 9 ? 0:00 stmmem
root 92 0 0 Mar 9 ? 0:00 strmled
root 100 1 0 1:15:22 console 0:00 /usr/sbin/getty getty console
root 101 1 0 Mar 9 ? 1:57 /usr/sbin/xawgettyd
oracle 102 1 0 5:14:23 ? 0:00 oracle_sprd (LOCAL-NO)
root 103 1 0 Mar 9 ? 78:34 /usr/sbin/rpcd rayer
root 104 1 0 Mar 9 ? 0:10 /usr/sbin/spind -D
root 105 1 0 Mar 9 ? 0:00 /usr/sbin/portmap
root 106 1 0 Mar 9 ? 0:00 /usr/sbin/gsfsdemon
root 107 1 0 Mar 9 ? 0:00 /usr/sbin/blogd 4
root 108 1 0 Mar 9 ? 0:00 /usr/sbin/nkl_daemond 0 0 0 0 0 1 2
oracle 109 1 0 1:13:43 ? 0:00 oracle_sprd (LOCAL-NO)
root 110 1 0 Mar 9 ? 0:00 /usr/sbin/tnsd
root 111 1 0 Mar 9 ? 0:00 /usr/sbin/bload 4
root 112 1 0 Mar 9 ? 0:00 /usr/sbin/bload 4
root 113 1 0 Mar 9 ? 0:00 /usr/sbin/rpc_lockd
root 114 1 0 Mar 9 ? 0:00 /usr/sbin/rpc_atstat
root 115 1 0 Mar 9 ? 0:16 /usr/sbin/automount -f /etc/auto_master
root 116 1 0 Mar 9 ? 0:06 aendmail: accepting connections
root 117 1 0 Mar 9 ? 0:02 /usr/sbin/inetd
root 118 1 0 Mar 9 ? 5:01 /usr/sbin/snmpd
root 119 1 0 Mar 9 ? 11:28 /usr/sbin/ttdbgdapt
root 120 1 0 Mar 9 ? 30:55 lpcp/deco/tpc/rpcd
root 121 1 0 Mar 9 ? 0:00 /usr/sbin/vtfsdemon
root 122 1 0 Mar 9 ? 0:00 <default>
root 123 1 0 Mar 9 ? 0:00 <default>
root 124 1 0 Mar 9 ? 8:55 DIAGMON
root 125 1 0 Mar 9 ? 0:15 /usr/sbin/cron
oracle 126 1 0 1:14:37 ? 0:00 oracle_sprd (LOCAL-NO)
root 127 1 0 Mar 9 ? 0:00 /usr/sbin/dnsmgrd
oracle 128 1 0 07:00:14 ? 0:01 ora_smons_prd
root 129 1 0 Mar 9 ? 0:00 /usr/sbin/envd
root 130 1 0 Mar 9 ? 0:00 DSBLOG; DSBLOG;DNSLOG;0;0
root 131 1 0 Mar 9 ? 0:00 /usr/sbin/nsfd 4
root 132 1 0 Mar 9 ? 0:00 /usr/sbin/nsfs_mount
root 133 1 0 Mar 9 ? 0:00 /usr/sbin/nsfd 4
root 134 1 0 Mar 9 ? 0:00 /usr/sbin/nsfd 4
root 135 1 0 Mar 9 ? 0:13 PSMS;PSM;0;0;1
```

以下是对各表头的简要说明：

- **UID**：进程所有者的用户 ID。
- **PID**：进程 ID（你可以使用此数字来终止进程）。
- **PPID**：父进程的进程 ID。
- **C**：处理器利用率。在多处理器系统上，你可能会看到这个数字超过 100%。它可能会达到每个处理器 100%，因此双处理器系统可能显示 200% 的利用率。这取决于不同的 UNIX 变体。
- **STIME**：进程启动时间。
- **TTY**：进程的控制终端。
- **TIME**：进程的累计执行时间。
- **COMMAND**：命令名称及参数。

`ps` 提供了系统中正在运行的进程的简要概况。要获取更详细的信息，你可以包含 `-f` 选项，其中包含许多有用的额外信息，如下例所示：

```text
martyp $ ps -efl
F S UID PID PPID C PRI NI ADDR SZ WCHAN STIME TTY D
19 S 0 root 0 0 0 0 FY f5e6277f3 0 Feb 18 ? D
6 S 0 root 1 0 0 41 20 f5b96888 175 Feb 18 7 ? D
19 S 0 root 2 0 0 0 SY f5b96008 0 f02f8f3d Feb 18 ? ?
19 S 0 root 3 0 0 0 SY f5b960a8 0 f02f8f3d Feb 18 ? ?
8 S 0 root 1065 3059 0 40 20 f5f6da68 1619 feabaa2d6 Feb 18 ? 6h
8 S 0 root 88 1 0 40 20 f5b6dd706 377 f5b6926f6 Feb 18 ? C
8 S 0 root 478 1 0 41 20 f58bacbc 388 f55b1d2d6 Feb 18 ? Q
8 S 0 root 94 1 0 41 20 f5b6da808 522 f5b63de4c Feb 18 ? D
8 S 0 root 150 1 0 41 20 f5d6da110 808 f5b56500c Feb 18 ? D
8 S 0 root 96 1 0 47 20 f5d6281d 515 f5b584d2e Feb 18 ? V
8 S 0 root 144 1 0 41 20 f5d6da610 2694 ffe8f5361 Feb 18 ? 5d
8 S 0 root 1010 1 0 47 67 f5f6481d0 436 f54bec21c Feb 18 ? S
8 S 0 root 306 1 0 41 20 f5d641310 485 f5b5a6e96 Feb 18 ? N
8 S 0 root 176 1 0 51 20 f5b68ed8 446 f55b1ceb8 Feb 18 ? N
8 S 0 root 136 1 0 53 20 f5d636110 740 f5b958a62 Feb 18 ? D
8 S 0 root 129 1 0 56 20 f5d635110 447 f5b56b231 Feb 18 ? D
R daemon 110 1 0 41 20 f5d635110 584 f5b56997f Feb 18 ? D
R S 0 root 14798 1 0 45 20 f5b5ec50a 616 f5b5c7330 Feb 18 ? D
R S 0 root 129 1 0 51 20 f5e18814 507 f5b596f6c Feb 18 ? D
R S 0 root 137 1 0 63 20 f5e15688 542 f59d051440 Mar 09 ? D
B S 0 root 196 1 0 41 20 f5e146510 429 f596246f6 Feb 18 ? C
B S 0 root 213 1 0 41 20 f5e164316 584 f5b6a2b2e Feb 18 ? C
R S 0 root 199 196 0 41 20 f5e16c18 451 f5b63f816 Feb 18 ? 4d
R S 0 root 219 1 0 41 20 f5e17318 658 f5b59d686 Feb 18 ? M
```




S S root 209 1 0 41 20 fs5e11818 234 f5c0684e 2月 18 7 d
S S root 2935 266 0 49 20 f61db310 2473 fc2a4a56 2月 22 ? 4d
S S root 16806 3059 1 41 30 f636f140 1458 f63b3456 07505480 ?
S S root 2963 2954 0 49 20 f5f52020 513 f61b3116 2月 22 ? e
S S root 479 1 0 55 20 f5se7210 407 f5bdc2e6 2月 15 控制台 g
R 0 root 10976 1 0 65 20 f5158828 4788 f5c907a8 6月 01 ? g
S S root 7468 1 0 46 20 f621da38 2851 83068c 2月 24 ? d
S S root 266 1 0 42 20 f5e65520 1861 f5c8e856 2月 18 ? n
M a r t y p 16763 16761 0 51 20 f6270140 4329 f63d1fac 07:46:45 ?/4
S S root 10995 1 0 41 20 f5baf308 2350 f5fc8e46 6月 01 ? d
R S root 484 478 0 41 20 f5ec4e20 408 f5ee5048 2月 18 ? n
R S root 475 1 0 41 20 f5f54a28 504 f5cc76f0 2月 18 ? 2m
R 0 root 16802 16763 1 61 20 f5e78280 220 08:00:05 ?/4 l
R S root 471 1 0 41 20 f5f55c28 658 f5fd2626 2月 18 ? d
R S root 474 1 0 51 20 f5f53328 604 64145846 2月 18 ? g
R 0 root 485 458 0 49 20 f5f52620 734 f6077d2c 2月 18 ? 74
S S root 2954 2936 0 49 20 f62e5a40 433 f62e5a5d 2月 22 ? n
S S root 2936 266 0 66 20 f5e47120 1637 f5e4718c 2月 22 ? n
S S root 3058 3059 0 49 20 f5e17a18 2041 f613559e 2月 22 ? n
S S root 3058 1 0 49 20 f61daa30 1967 f62aad0c 2月 22 p2/2 m
S R root 712 133 0 41 20 f61d830c 758 fc1b390e 2月 18 ? d
R 2 root 11011 11006 0 0 >
S S root 2938 1 0 59 20 f5ee5320 513 f601fbf6 2月 22 ? >
R 0 root 2999 2954 0 49 20 f621e138 1490 f61631be 2月 22 p2/2 t
S S root 3059 3021 1 51 20 f626de40 4010 f62aaaf6 2月 22 p2/2 2n
S S root 3063 3059 0 59 20 f621e038 1952 f62aa356 2月 22 ?
R S root 3099 3052 0 49 20 f5529728 2275 f6a01d18 2月 22 ?
S S root 11010 10995 0 48 20 f62d74f0 2312 55699a 6月 01 ? e
R S root 3029 2999 0 43 20 f61d8730 427 f61f9879 2月 22 p2/2 -
R S root 730 133 0 49 20 f61985f0 422 f62a83b6 2月 18 ? d
R S root 3062 3059 0 61 20 f621b738 2275 f62aa506 2月 22 ?
R S root 3067 1 0 49 20 f5se5020 424 f5eea506c 2月 22 ? d
R S root 3008 1 0 49 20 f6148030 510 62f4240c 2月 22 ? ?
S S root 3076 3067 0 49 20 f61d9c30 211 f5f512b8 2月 22 ?
S S root 10984 1 0 41 20 f5e45328 2484 e8ee498a 6月 01 ? 1b
S S root 16781 133 0 44 20 f5ee4020 413 f5c8958e 07:46:45 ? d
m a r t y p $

在此示例中，第一列是 F，代表标志（Flags）。F 提供关于进程是否被换出、是否在内核中、是否为系统进程等的八进制信息。八进制值有时会因系统而异，因此请查阅您系统的手册页以查看标志的八进制值。

S 代表状态（State）。状态可以是睡眠，如示例中大多数进程所示的 S，等待、运行、中间状态、终止等。同样，这些值可能会因系统而异，因此请查阅您的手册页。

此输出中还有一些其他有用的信息：NI 代表 nice 值，ADDR 代表进程的内存地址，SZ 代表进程占用的物理页大小，以及 WCHAN，即进程正在等待的事件。

## 终止进程

如果您运行 ps 命令并发现您的某个进程挂起，或者您启动了一个想要停止的大型任务，您可以使用 kill 命令来执行此操作。kill 是一个实用工具，用于向您指定的进程发送信号。您可以终止任何您拥有的进程。此外，超级用户（superuser）可以终止系统上几乎所有的进程。

要终止您拥有的进程，只需发出 kill 命令和进程 ID（PID）。以下示例展示了运行 ps 命令以查找属于用户 martyp 的所有进程，终止一个进程，并检查它是否已消失：

```
martyp $ ps -ef | grep martyp
martyp    19336    19334  0   05:24:32 pts/4      0:01 -ksh
martyp    19426    19336  0   06:01:01 pts/4      0:00 grep martyp
martypl   19424    19336  5   06:00:48 pts/4      0:01 find /-name .login
martypl $ kill 19424
martypl $ ps -ef | grep martyp
martypl   19336    19334  0   05:24:32 pts/4      0:01 -ksh
martypl   19428    19336  1   06:01:17 pts/4      0:00 grep martyp
[1]+    Terminated      find / -name .login &
martypl $
```

该示例展示了终止进程 19424，该进程属于 martyp。通过重新运行 ps 命令，我们可以确认该进程确实已被终止。您也可以使用 ps 的 -u 选项来列出具有您指定登录名的进程。

您可以通过在 kill 后跟一个以空格分隔的进程编号列表来在命令行上终止多个进程。

如果您以超级用户身份登录，终止进程时要格外小心。您可能会以不利的方式影响系统的运行，并可能需要手动重启进程或重启系统。

## 信号

当您发出 kill 命令和进程号时，您也在发送与 kill 关联的信号。我们在 kill 示例中没有指定信号；然而，默认的信号 15，即 *SIGTERM*，被使用了。这些*信号*由系统用于与进程通信。我们用来终止进程的信号 15 是一个软件终止*信号*，通常足以终止用户进程，例如我们启动的 *find*。难以终止的进程可能需要 *SIGKILL*，即 9 号*信号*。此*信号*会导致进程立即终止。我只将其作为最后的手段，因为被 *SIGKILL* 终止的进程并不总是能平稳终止。要终止像 shell 这样的进程，有时不得不使用 *SIGKILL*。

您可以使用*信号*名称或编号。这些信号编号有时因系统而异，因此请查看*信号*的手册页（通常在第 5 节中），以查看您系统中的*信号*列表。以下是一些最常用*信号*编号和对应*信号*的列表：

| 信号编号 | 信号 |
| :--- | :--- |
| 1 | SIGHUP |
| 2 | SIGINT |
| 3 | SIGQUIT |
| 9 | SIGKILL |
| 15 | SIGTERM |
| 24 | SIGSTOP |

要使用 *SIGKILL* 终止 ID 为 234 的进程，您将发出以下命令：

```
$ kill -9 234
> 进程 ID (PID)
> 信号编号
> 用于终止进程的命令
```

##### 使用 showmount 显示远程挂载

**showmount** 用于显示已挂载本地文件系统的所有远程系统（客户端）。**showmount** 对于确定哪些文件系统最常被客户端通过 NFS 挂载非常有用。**showmount** 的输出特别容易阅读，因为它列出了客户端挂载的主机名和目录。

NFS 服务器最终往往服务于许多原本不打算服务的 NFS 客户端。这种情况会导致 NFS 服务器消耗额外的 UNIX 系统资源以及额外的网络带宽。请记住，从 NFS 服务器传输到 NFS 客户端的任何数据都会消耗网络带宽，在某些情况下，如果从 NFS 服务器向客户端传输大文件应用程序，可能会消耗大量带宽。以下示例是从系统中截取的部分 **showmount** 输出。**showmount** 在我本章中使用的 HP-UX、AIX 和 Linux 系统上运行，但在 Solaris 系统上不运行：

```
# showmount -a

sys100.ct.mp.com//applic
sys101.ct.mp.com//applic
sys102.cal.mp.com//applic
sys103.ca.mp.com//applic
sys104.cal.mp.com//applic
sys105.cal.mp.com//applic
sys106.cal.mp.com//applic
sys107.cal.mp.com//applic
sys108.cal.mp.com//applic
sys109.cal.mp.com//applic
sys200.cal.mp.com/usr/users
sys201.cal.mp.com/usr/users
sys202.cal.mp.com/usr/users
sys203.cal.mp.com:/usr/users
sys204.cal.mp.com:/usr/users
sys205.cal.mp.com:/usr/users
sys206.cal.mp.com:/usr/users
sys207.cal.mp.com:/usr/users
sys208.cal.mp.com:/usr/users
sys209.cal.mp.com:/usr/users
```

**showmount** 命令有以下三个可用的选项：

-   **a** 以“名称:目录”的格式打印输出，如上所示。
-   **d** 列出所有被客户端远程挂载的本地目录。
-   **e** 打印导出文件系统的列表。

以下是 **showmount -d** 和 **showmount -e** 的示例：

```
# showmount -d

    /apple
    /usr/users
    /usr/oracle
    /usr/users/emp.data
    /network/database
    /network/users
    /tmp/working
```

```
# showmount -e

    server101.cal.mp.com 的导出列表
```





## 797

```
# showmount -e
/apply
/usr/users
/cdrom
```

##### 显示系统交换区

如果你的系统没有足够的内存来容纳其工作所需的所有信息，它将把信息页移动到交换区，或者将整个进程移动到交换区。最近使用过的页会被保留在主内存中，而最近未使用的页将最先被移出主内存。

系统管理员花大量时间确定系统合适的交换区大小。交换区不足可能会阻止系统启动额外的进程、导致应用程序挂起，或不允许额外用户访问系统。拥有足够的交换区可以防止这些问题发生。系统管理员通常通过考虑许多重要因素来确定合适的交换区大小，包括以下几点：

1.  你运行的应用程序推荐多少交换区？请使用你应用程序推荐的交换区大小。应用程序供应商在推荐交换区空间时通常比较现实。有时，应用程序供应商之间会存在竞争，为了尽可能降低解决方案的总成本而声称最低内存和 CPU 要求，但交换区建议通常是现实的。
2.  你将同时运行多少个应用程序？如果你正在运行多个应用程序，请将对同时运行的每个应用程序推荐的交换区空间相加。例如，如果你有一个数据库应用程序推荐 200 MB 的交换区，以及一个开发工具推荐 100 MB 的交换区，那么至少将系统配置为 300 MB 的交换区。
3.  你是否会在周边功能（如 NFS）上使用大量系统资源？NFS 的本质是提供对文件系统的访问，其中一些文件系统可能非常大，因此这种使用可能会影响你的交换区需求。

交换区在不同的 UNIX 变体中使用不同的命令列出和操作。以下示例展示了在 Solaris 系统上使用 `swap -l` 列出交换区。

```
# swap -l
swapfile dev swaplo blocks free
/dev/dsk/c0t3d0s1 32,25 8 263080 209504
```

这些值均以 512 KByte 块为单位。在这种情况下，空闲块为 209504，这是系统分配的总交换区中相当大的一部分。

你可以使用 `swapinfo` 查看 HP-UX 系统上正在消耗的交换区数量。以下是 `swapinfo` 的一个示例输出：

```
# swapinfo
```

| 类型 | Kb 可用 | Kb 已用 | Kb 空闲 | 使用百分比 | 起始/限制 | 保留 | 优先级 | 名称 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| dev | 49152 | 10532 | 38620 | 21% | 0 | - | 1 | /dev/vg00/lvol2 |
| dev | 86832 | 10888 | 759160 | 1% | 0 | - | 1 | /dev/vg00/lvol8 |
| reserve | 532360 | -532360 | | | | | | |
| memory | 816360 | 469784 | 346576 | 58% | | | | |

以下是 `swapinfo` 提供的简要概述。

在前述示例中，“TYPE”（类型）字段指示交换区是“dev”（设备）、“reserve”（保留页空间）还是“memory”（内存）。内存是一种允许程序保留比系统中设置的硬盘页空间更多的虚拟内存的方式。

“Kb AVAIL”（可用 Kb）是以 1024 字节块为单位的总可用交换区空间。这包括已用和未用的交换区。

“Kb USED”（已用 Kb）是当前正在使用的 1024 字节块数量。

“Kb FREE”（空闲 Kb）是“Kb AVAIL”与“Kb USED”之间的差值。

“PCT USED”（使用百分比）是“Kb USED”除以“Kb AVAIL”。

“START/LIMIT”（起始/限制）是交换区起始位置的块地址。

“Kb RESERVE”（保留 Kb）对于设备交换区为“-”，对于文件系统交换区则是 1024 字节的块数。

“PRI”（优先级）是分配给该交换区的优先级。

“NAME”（名称）是交换设备的设备名称。

你还可以使用一系列选项执行 **swapon** 命令。以下是你可以包含的一些选项：

-   -m 以 MB 为单位显示 **swapinfo** 的输出，而不是以 1024 字节块为单位。
-   -d 仅打印与设备交换区相关的信息。
-   -f 仅打印文件系统交换区的相关信息。

##### sar：系统活动报告器

**sar** 是另一个用于收集系统活动信息的 UNIX 命令。你可以使用 **sar** 在较长的一段时间内收集数据，并根据数据稍后生成报告。由于选项和输出相似，**sar** 在不同的 UNIX 变体中也很相似。我用于示例的 Linux 系统不支持 **sar**，但 Solaris、HP-UX 和 AIX 系统具有相同的选项和几乎相同的输出。以下是一些 **sar** 的有用选项，以及（在适用情况下）使用这些选项生成的报告示例：

-   **sar -o** 将数据保存到由“o”指定的文件中。在文件名之后，通常还会输入样本的时间间隔和样本数量。以下示例展示了以 60 秒间隔保存 300 次二进制数据到文件 /tmp/sar.data：

```
# sar -o /tmp/sar.data 60 300
```

/tmp/sar.data 中的数据可以从文件中提取出来。

-   **sar -f** 指定从中提取数据的文件。

-   **sar -u** 报告 CPU 利用率，标题为 %usr、%sys、%wio、%idle，其中 %idle 包含一些等待块 I/O 的进程。此报告与 iostat 和 vmstat 的 CPU 报告类似。你从保存在文件中的二进制数据中提取 CPU 信息，如下例所示。以下是 **sar -u** 的示例：

```
# sar -u -f /tmp/sar.data

Header Information for your system
12:52:04   %usr   %sys   %wio   %idle
12:53:04      62     4     5      29
12:54:04      88     5     3       4
12:55:04      94     5     1       0
12:56:04      67     4     4      25
12:57:04      59     4     4      32
12:58:04      61     4     3      32
12:59:04      65     4     3      28
13:00:04      62     5    16      17
13:01:04      59     5     9      27
13:02:04      71     4     3      22
13:03:04      60     4     4      32
13:04:04      71     5     4      20
13:05:04      80     6     8       7
13:06:04      56     3     3      37
13:07:04      57     4     4      36
13:08:04      66     4     4      26
13:09:04      80    10     2       8
13:10:04      73    10     2      15
13:11:04      64     6     3      28
13:12:04      56     4     3      38
13:13:04      55     3     3      38
13:14:04      57     4     3      36
13:15:04      70     4     5      21
13:16:04      65     5     9      21
13:17:04      62     6     2      30
13:18:04      60     5     3      33
13:19:04      77     3     4      16
13:20:04      76     5     3      15
14:30:04      50     6     6      38
14:31:04      57    12    19      12
14:32:04      51     8    20      21
14:33:04      41     4     9      46
14:34:04      43     4     9      45
14:35:04      38     4     6      53
14:36:04      38     9     7      46
14:37:04      46     3    11      40
14:38:04      43     4     7      46
14:39:04      37     4     5      54
14:40:04      33     4     5      58
14:41:04      40     3     3      53
14:42:04      44     3     3      50
14:43:04      27     3     7      64
Average        57     5     8      30
```

-   **sar -b** 报告缓冲区缓存活动。Oracle 等数据库应用程序会建议你使用此选项来查看缓冲区缓存使用的有效性。你从保存在文件中的二进制数据中提取 CPU 信息，如下例所示：

```
# sar -b -f /tmp/sar.data
Header information for your system

12:52:04 breads/s freads/s wroache lwrite/s lwrit/s wreache pread/s pwrite/s
12:53:04 5 608 38 1 11 95 0 0
12:54:04 7 759 99 0 14 99 0 0
12:55:04 2 1733 166 4 24 83 0 0
12:56:04 1 836 100 1 18 96 0 0
12:57:04 0 623 100 2 21 92 0 0
12:58:04 0 779 100 1 16 94 0 0
12:59:04 0 1125 100 0 14 98 0 0
13:00:04 2 1144 100 9 89 89 0 0
13:01:04 10 899 99 11 76 86 0 0
13:02:04 0 1156 100 0 14 99 0 0
13:03:04 1 578 100 2 12 88 0 0
13:04:04 5 1251 100 0 12 99 0 0
```

## sar -d

报告磁盘活动。你可以获取设备名称、设备繁忙百分比、设备的平均未完成请求数、设备每秒的数据传输次数以及其它信息。你从保存在文件中的二进制数据中提取 CPU 信息，如下例所示：

```
# sar -d -f /tmp/sar.data
Header information for your system
12:54:04  device  %busy  avgqu   ...  ...  ...  ...  ...  ...
c0t6d0    0.95    1.41   1       ...  ...  4   ...  ...  ...  ...
```

![img/eff8b9287a5f38c5adf538f24aacf29e_802_0.png](img/eff8b9287a5f38c5adf538f24aacf29e_802_0.png)




| | 时间 | 设备 | Trans/s | Bps | Kb/t | tput | W | R |
|---|---|---|---|---|---|---|---|---|
| | | c5t4d2 | 0.72 | 0.50 | 0 | 7 | 4.82 | 15.65 |
| | | c5t6d0 | 1.07 | 21.57 | 1 | 22 | 72.94 | 19.50 |
| 12:56:04 | | c5t4d0 | 100.00 | 0.60 | 16 | 251 | 6.80 | 13.45 |
| | | c4t5d1 | 8.75 | 0.50 | 11 | 377 | 5.05 | 10.61 |
| | | c5t4d2 | 0.62 | 0.50 | 0 | 237 | 7.60 | 23.69 |
| 12:57:04 | | c5t6d0 | 0.78 | 1.16 | 1 | 9 | 13.53 | 14.91 |
| | | c5t4d0 | 100.00 | 0.66 | 15 | 237 | 7.60 | 13.69 |
| | | c4t5d1 | 9.46 | 0.54 | 13 | 210 | 5.19 | 13.33 |
| 12:58:04 | | c5t4d2 | 0.87 | 0.53 | 0 | 10 | 4.86 | 14.09 |
| | | c5t6d0 | 1.12 | 8.29 | 1 | 37 | 54.96 | 14.35 |
| | | c5t4d0 | 100.00 | 0.60 | 11 | 176 | 7.91 | 14.65 |
| | | c5t4d1 | 9.35 | 0.50 | 7 | 37 | 5.23 | 10.35 |
| | | c5t4d2 | 0.92 | 0.50 | 1 | 10 | 4.63 | 16.08 |
| 12:59:04 | | c5t6d0 | 9.87 | 1.51 | 4 | 38 | 18.03 | 16.05 |
| | | c5t4d0 | 99.98 | 0.54 | 11 | 174 | 7.69 | 14.08 |
| | | c4t5d1 | 1.97 | 0.50 | 55 | 83 | 4.82 | 9.54 |
| | | c5t4d2 | 1.06 | 0.50 | 1 | 11 | 4.69 | 16.29 |
| 13:00:04 | | c5t6d0 | 3.22 | 0.67 | 3 | 39 | 8.49 | 16.52 |
| | | c5t4d0 | 100.00 | 0.60 | 65 | 1032 | 8.46 | 14.83 |
| | | c4t5d1 | 21.62 | 0.50 | 31 | 304 | 5.30 | 8.94 |
| | | c5t4d2 | 6.77 | 0.50 | 5 | 78 | 4.86 | 14.09 |
| 13:01:04 | | c5t6d0 | 4.45 | 1.04 | 5 | 59 | 25.83 | 11.49 |
| | | c5t4d0 | 100.00 | 0.65 | 42 | 676 | 7.85 | 14.52 |
| | | c4t5d1 | 21.34 | 0.55 | 30 | 476 | 5.87 | 18.49 |
| | | c5t4d2 | 4.37 | 0.50 | 3 | 51 | 5.32 | 13.50 |
| 14:42:04 | | c5t6d0 | 0.53 | 0.83 | 0 | 7 | 12.21 | 16.33 |
| | | c5t4d0 | 100.00 | 0.56 | 7 | 107 | 6.99 | 14.65 |
| | | c5t4d1 | 6.38 | 0.50 | 7 | 113 | 4.87 | 15.18 |
| 14:43:04 | | c5t4d2 | 0.15 | 0.50 | 2 | 4 | 4.53 | 16.50 |
| | | c5t6d0 | 0.52 | 0.92 | 0 | 7 | 11.50 | 15.86 |
| | | c5t4d0 | 99.98 | 0.92 | 8 | 270 | 8.28 | 13.64 |
| | | c4t5d1 | 10.26 | 0.50 | 9 | 150 | 5.35 | 16.41 |
| | | c5t4d2 | 0.12 | 0.50 | 1 | 1 | 5.25 | 14.45 |
| 平均值 | | c5t6d0 | 1.43 | 108.00 | | 2 | 26 | 0.00 |
| | | c5t4d0 | 100.00 | 0.74 | | 25 | 388 | 7.81 |
| | | c4t5d1 | 19.11 | 0.51 | 25 | 399 | 5.26 | 13.75 |
| | | c5t4d2 | 1.71 | 0.53 | 1 | 21 | 5.29 | 13.46 |

`sar -q` 报告平均队列长度。每当运行队列长度大于系统中的处理器数量时，都可能存在问题：

```
# sar -q -f /tmp/sar.data
```

系统的头部信息

| 时间 | 运行队列大小 | 运行进程数 | 交换队列大小 | 交换压缩率 |
|---|---|---|---|---|
| 12:52:04 | 1.1 | 20 | 0.0 | 0 |
| 12:53:04 | 2.0 | 20 | 0.0 | 0 |
| 12:54:04 | 1.4 | 51 | 0.0 | 0 |
| 12:55:04 | 1.3 | 71 | 0.0 | 0 |
| 12:56:04 | 1.1 | 22 | 0.0 | 0 |
| 12:57:04 | 1.3 | 16 | 0.0 | 0 |
| 12:58:04 | 1.1 | 14 | 0.0 | 0 |
| 12:59:04 | 1.2 | 12 | 0.0 | 0 |
| 13:00:04 | 1.2 | 21 | 0.0 | 0 |
| 13:01:04 | 1.1 | 18 | 0.0 | 0 |
| 13:02:04 | 1.3 | 20 | 0.0 | 0 |
| 13:03:04 | 1.2 | 15 | 0.0 | 0 |
| 13:04:04 | 1.2 | 20 | 0.0 | 0 |
| 13:05:04 | 1.2 | 43 | 0.0 | 0 |
| 13:06:04 | 1.1 | 14 | 0.0 | 0 |
| 13:07:04 | 1.2 | 15 | 0.0 | 0 |
| 13:08:04 | 1.2 | 26 | 0.0 | 0 |
| 13:09:04 | 1.5 | 38 | 0.0 | 0 |
| 13:10:04 | 1.5 | 30 | 0.0 | 0 |
| 13:11:04 | 1.2 | 23 | 0.0 | 0 |
| 13:12:04 | 1.3 | 11 | 0.0 | 0 |
| 13:13:04 | 1.3 | 12 | 0.0 | 0 |
| 13:14:04 | 1.4 | 16 | 0.0 | 0 |
| 13:15:04 | 1.4 | 27 | 0.0 | 0 |
| 13:16:04 | 1.5 | 20 | 0.0 | 0 |
| 13:17:04 | 1.3 | 21 | 0.0 | 0 |
| 13:18:04 | 1.1 | 35 | 0.0 | 0 |
| 13:19:04 | 1.2 | 19 | 0.0 | 0 |
| 13:20:04 | 1.4 | 22 | 0.0 | 0 |
| 14:30:04 | 1.5 | 5 | 0.0 | 0 |
| 14:31:04 | 1.6 | 12 | 0.0 | 0 |
| 14:32:04 | 1.4 | 9 | 0.0 | 0 |
| 14:33:04 | 1.1 | 6 | 0.0 | 0 |
| 14:34:04 | 1.3 | 3 | 0.0 | 0 |
| 14:35:04 | 1.1 | 4 | 0.0 | 0 |
| 14:36:04 | 1.2 | 6 | 0.0 | 0 |
| 14:37:04 | 1.4 | 5 | 0.0 | 0 |
| 14:38:04 | 1.2 | 10 | 0.0 | 0 |
| 14:39:04 | 1.3 | 4 | 0.0 | 0 |
| 14:40:04 | 1.1 | 3 | 0.0 | 0 |
| 14:41:04 | 1.6 | 3 | 0.0 | 0 |
| 14:42:04 | 1.1 | 4 | 0.0 | 0 |
| 14:43:04 | 1.3 | 1 | 0.0 | 0 |
| 平均值 | 1.3 | 17 | 1.2 | 0 |

`sar -w` 报告系统交换活动。

```
# sar -w -f /tmp/sar.data
```

系统的头部信息

| 时间 | 内存百分比 | 处理器百分比 | I/O 百分比 | 交换压缩率 | 页面入交换 |
|---|---|---|---|---|---|
| 12:52:04 | 1.00 | 0.0 | 1.00 | 0.0 | 231 |
| 12:53:04 | 1.00 | 0.0 | 1.00 | 0.0 | 354 |
| 12:54:04 | 1.00 | 0.0 | 1.00 | 0.0 | 348 |
| 12:55:04 | 1.00 | 0.0 | 1.00 | 0.0 | 200 |
| 12:56:04 | 1.00 | 0.0 | 1.00 | 0.0 | 277 |
| 12:57:04 | 1.00 | 0.0 | 1.00 | 0.0 | 277 |
| 12:58:04 | 1.00 | 0.0 | 1.00 | 0.0 | 235 |
| 12:59:04 | 1.02 | 0.0 | 1.02 | 0.0 | 199 |
| 13:00:04 | 0.78 | 0.0 | 0.78 | 0.0 | 456 |
| 13:01:04 | 1.00 | 0.0 | 1.00 | 0.0 | 435 |
| 13:02:04 | 1.02 | 0.0 | 1.02 | 0.0 | 216 |
| 13:03:04 | 0.98 | 0.0 | 0.98 | 0.0 | 204 |
| 13:04:04 | 1.02 | 0.0 | 1.02 | 0.0 | 239 |
| 13:05:04 | 1.00 | 0.0 | 1.00 | 0.0 | 248 |
| 13:06:04 | 0.97 | 0.0 | 0.97 | 0.0 | 170 |
| 13:07:04 | 1.00 | 0.0 | 1.00 | 0.0 | 166 |
| 13:08:04 | 1.02 | 0.0 | 1.02 | 0.0 | 209 |
| 13:09:04 | 0.98 | 0.0 | 0.98 | 0.0 | 377 |
| 13:10:04 | 1.00 | 0.0 | 1.00 | 0.0 | 200 |
| 13:11:04 | 1.00 | 0.0 | 1.00 | 0.0 | 192 |
| 13:12:04 | 0.87 | 0.0 | 0.87 | 0.3 | 187 |
| 13:13:04 | 0.93 | 0.0 | 0.93 | 0.0 | 172 |
| 13:14:04 | 1.00 | 0.0 | 1.00 | 0.0 | 170 |
| 13:15:04 | 1.00 | 0.0 | 1.00 | 0.0 | 382 |
| 13:16:04 | 1.00 | 0.0 | 1.00 | 0.0 | 513 |
| 13:17:04 | 1.00 | 0.0 | 1.00 | 0.0 | 332 |
| 13:18:04 | 1.00 | 0.0 | 1.00 | 0.0 | 265 |
| 13:19:04 | 1.02 | 0.0 | 1.02 | 0.0 | 184 |
| 13:20:04 | 0.98 | 0.0 | 0.98 | 0.0 | 212 |
| 14:30:04 | 0.00 | 0.0 | 0.00 | 0.0 | 301 |
| 14:31:04 | 0.00 | 0.0 | 0.00 | 0.0 | 566 |
| 14:32:04 | 0.00 | 0.0 | 0.00 | 0.0 | 400 |
| 14:33:04 | 0.00 | 0.0 | 0.00 | 0.0 | 282 |
| 14:34:04 | 0.00 | 0.0 | 0.00 | 0.0 | 286 |
| 14:35:04 | 0.00 | 0.0 | 0.00 | 0.0 | 295 |
| 14:36:04 | 0.00 | 0.0 | 0.00 | 0.0 | 249 |
| 14:37:04 | 0.00 | 0.0 | 0.00 | 0.0 | 300 |
| 14:38:04 | 0.00 | 0.0 | 0.00 | 0.0 | 296 |
| 14:39:04 | 0.00 | 0.0 | 0.00 | 0.0 | 419 |
| 14:40:04 | 0.00 | 0.0 | 0.00 | 0.0 | 234 |
| 14:41:04 | 0.00 | 0.0 | 0.00 | 0.0 | 237 |
| 14:42:04 | 0.00 | 0.0 | 0.00 | 0.0 | 208 |
| 14:43:04 | 0.00 | 0.0 | 0.00 | 0.0 | |
| 平均值 | 0.70 | 0.0 | 0.70 | 0.0 | 346 |

##### 使用 `time` 分析命令

如果您有特定的命令想要深入了解，可以使用 `time`，它会报告在执行您指定的任何命令时花费的经过时间、用户时间和系统时间。

**time** 是一个用户友好的命令，因为它能让你了解执行命令时消耗的系统资源。以下两个示例展示了不带选项执行 **time** 以获取已消耗 CPU 量的简短输出；第二个示例展示了在 Solaris 系统上执行 **time -s** 以报告“总”系统活动：

```
marvyp $ time listing

real    0.02
user    0.00
sys     0.02
```

```
marvyp $ time -s listing

real    0.02
user    0.00
sys     0.01
```

```
SunOS 5.7 Generic sun4m       08/21

                avg1  avg5  avg15
07:48:30        dr    pd%   rw    mbufs   mmbufs
07:48:31        dr    pd%   rw    mbufs   mmbufs
07:48:30        bread/s     write/s       swaptch/s   swain/s
07:48:31        bread/s     write/s       swaptch/s   swain/s
Average         3     16    0     1     100

07:48:30        device      %busy   agvm    rw/s    bk/s    await   async
07:48:31        fdo               0     0     0.0       0.0
                        nfsd219   0     0.0   0     0     0.0       0.0
                        sda       0     0.0   0     0     0.0       0.0
                        sdb       0     0.0   0     0     0.0       0.0
                        sdc       0     0.0   0     0     0.0       0.0
                        sdd       0     0.0   0     0     0.0       0.0
                        sde       0     0.0   0     0     0.0       0.0
                        sdf       0     0.0   0     0     0.0       0.0
                        sdg       0     0.0   0     0     0.0       0.0
                        sdh       0     0.0   0     0     0.0       0.0
                        sdi       0     0.0   0     0     0.0       0.0
                        sdj       0     0.0   0     0     0.0       0.0
                        sdk       0     0.0   0     0     0.0       0.0
Average                       0     0.0   0     0     0.0       0.0

07:48:30        rawch/s   canch/s   outhch/s  rwch/s  xmtx/s  mdbmin/s
07:48:31        rawch/s   canch/s   outhch/s  rwch/s  xmtx/s  mdbmin/s
Average                         147     0     0

07:48:30        sall/s    read/s    swir/s    fork/s    exec/s    rchar/s   swchar/s
07:48:31        sall/s    read/s    swir/s    fork/s    exec/s    rchar/s   swchar/s
Average                                             2637    0     95    15.79   0     19216
```




##### 更高级的图形化性能工具

在使用 UNIX 时，命令行是一种生活方式。UNIX 源自命令行，并且至今仍主要以命令行为基础。虽然在下达命令时需要了解许多知识，尤其是在系统性能方面，但通过我刚才提到的许多命令，你可以快速深入挖掘信息。

在大多数 UNIX 变体中，你可以选择购买图形化性能工具。一些系统自带基本的图形化性能分析工具，如果你想要执行高级性能分析，可以使用这些工具。我们将在接下来的章节中快速浏览一些性能工具。

图 12-3 展示了三个随 Red Hat Linux 系统提供的性能工具，我本章中的许多示例都使用了该系统：

*系统监视器 (gtop)* 窗口，显示了 *CPU*、*MEM*、*SW* 和 *LA* 的柱状图，单个进程信息以及其他有用的性能数据。

![](img/eff8b9287a5f38c5adf538f24aacf29e_809_0.png)

top 窗口，显示了负载平均值、处于每种状态的进程数、处理器状态的时间百分比、单个进程相关信息以及其他有用的性能数据。

xosview 窗口，显示 *CPU0* 和 *CPU1* 的利用率均为 100%。

# 图 12-3. Red Hat Linux *性能工具* 屏幕截图

更高级的图形化性能工具

图中展示的三种性能工具分别是：右下角的 **xosview**，屏幕顶部的 *系统监视器*，以及左下角的 **top**。*系统监视器* 在屏幕顶部提供柱状图，指示 CPU、内存、交换空间和局域网的使用量。随后，它为系统中的每个进程提供表格数据。*系统监视器* 是 **top** 的图形化版本，我通过命令 **gtop**（*图形化 top*）调用了它。**xosview** 是一个小型负载监视器，你可以让它持续运行，它在右下角窗口中提供系统活动的柱状图。这是 X Windows 的 *操作系统视图* 程序，因此名为 **xosview**。由于这是一个基于颜色的应用程序，而书本仅以黑白印刷，因此无法在图中清晰看到柱状图。但是，在电脑屏幕上柱状图非常清晰。UNIX 系统上最后一种，也是最常用的工具，是在左下角 **xterm** 中运行的字符版 **top**。许多 UNIX 变体都包含 **top**，它提供了大量有用的系统信息。

**top** 显示的有用系统数据包括以下内容：

- 过去一分钟、五分钟和十五分钟的负载平均值。
- 存在的进程数量以及处于每种状态的进程数量。
- 系统中每个处理器在每种处理器状态下花费的时间百分比。

*系统监视器* 窗口的底部也包含相同的信息，只是该区域被 **top** 和 **xosview** 窗口覆盖了。

接下来，**top** 窗口显示内存数据，包括已用、空闲和共享内存。

还以类似于 **ps** 的格式提供单个进程的数据，包括以下内容：

- *PID* - 进程 ID 号。
- *USER* - 进程所有者的名称。
- *PRI* - 进程的当前优先级。
- *NI* - Nice 值，范围从 -20 到 +20。
- *SIZE* - 进程的总大小（以千字节为单位）。
- *RSS* - 进程的驻留大小（以千字节为单位）。
- *STATE* - 进程的当前状态。
- *TIME* - 进程消耗的系统秒数和 CPU 秒数。
- *%CPU* - CPU 百分比。
- *%MEM* - 内存百分比。
- *COMMAND* - 进程当前运行的命令名称。

与我们涵盖的大多数命令一样，**top** 在 UNIX 变体之间也有所不同。在不同的 UNIX 变体上，你可能会看到一些不同的字段。当坐在任何 UNIX 系统前时，我通常很有信心，我可以运行 **top** 并快速查看系统的运行情况。我运行过的大多数 **top** 版本都是基于字符的应用程序，因此甚至不需要图形终端即可运行。我在本示例中以字符模式在 X 终端中运行了 **top**。

本示例中使用的系统有两个 CPU。如果仔细查看 **xosview** 窗口，你会发现 *CPU0* 和 *CPU1* 的使用率均为 100%。在获取该屏幕截图时，我正在该系统上编译 Linux 内核，这在短时间内消耗了系统所有的 CPU 资源。你可以从 **top** 和 *系统监视器* 窗口中看到，用于编译内核的程序 **cc1** 消耗了系统大量的 CPU 资源。

图 12-3 有助于说明不同的工具如何帮助查看系统资源的消耗情况。**xosview** 提供了关于多少系统资源正在被消耗的图形化快速参考和概述。**top** 和 *系统监视器* 可用于确定消耗最多系统资源的具体进程。

###### HP GlancePlus/UX

使用 UNIX 命令来更好地理解系统正在做什么需要大量工作。首先，下达 UNIX 命令的优势在于能够获得关于系统当前正在发生什么的数据。不幸的是，你并不总能额外下达命令来深入探究某个领域（例如某个进程）以获取更多信息。

现在我将描述另一种技术，一种工具，它可以帮助你实时获取有用数据，调查特定进程，且不会让你淹没在报告中。该工具是 HP GlancePlus/UX（GlancePlus）。该工具可在多种 UNIX 变体上运行，包括 Solaris、HP-UX 和 AIX。

GlancePlus 可以以字符模式或图形模式运行。我选择使用基于字符的 GlancePlus 版本，因为它可以在任何显示终端上运行，无论是图形终端还是字符终端，而 GlancePlus 的 Motif 版本使用的许多颜色在书中显示效果不佳。使用字符模式时，我的示例在书中显示得清晰得多。我建议你尝试 GlancePlus 的两个版本，看看你更喜欢哪一个。

示例中使用的系统有八个处理器，4 GB 内存，以及连接的大量 EMC Symmetrix 磁盘。图 12-4 显示了 GlancePlus 的几个交互屏幕之一。这是 *进程列表* 屏幕，也称为 *全局* 屏幕。这是启动 GlancePlus 时的默认屏幕。

图 12-4 中所示屏幕的两个特点值得立即注意：

1. 屏幕上方的四个直方图以比数字列表更易于理解的形式，图形化地表示 CPU、磁盘、内存和交换空间的使用情况。
2. “进程摘要”具有与 `ps -ef` 类似的列，许多系统管理员对此非常熟悉和习惯。然而，GlancePlus 提供了额外的功能，可以通过指定阈值来过滤掉使用资源很少的进程。

使用 GlancePlus，你可以仔细查看系统的许多领域，包括以下内容：

- 进程列表
- CPU 报告
- 内存报告
- 交换空间
- 磁盘报告
- 局域网详情
- 按系统的 NFS
- PRM 摘要（进程资源管理器）
- 按文件系统的 I/O
- 按磁盘的 I/O
- 按逻辑卷的 I/O
- 系统表

图 12-4 是 GlancePlus 的屏幕截图。




![](img/eff8b9287a5f38c5adf538f24aacf29e_814_0.png)

## 图 12-4 HP GlancePlus/UX 进程列表屏幕截图

由于示例中显示的 *进程列表* 在最高层级上告诉您系统资源的去向，因此我将从这里开始描述。我正在使用便携式电脑上的终端模拟器来显示 GlancePlus。我发现许多系统管理员使用 PC 和终端模拟器来执行 UNIX 管理功能。请记住，此屏幕上显示的信息可以以您选择的任何间隔进行更新。如果您的系统处于稳定状态运行，您可能希望设置较长的间隔，因为您不预期有太多变化。另一方面，如果您处于动态环境中，并希望看到直方图和其他信息每几秒钟更新一次。无论哪种情况，您都可以更改更新间隔以满足您的需求。您可以使用屏幕底部的功能键进入其他功能区域。

## 进程列表说明

*进程列表* 屏幕提供了系统资源状态和活动进程概览。

屏幕的顶部部分（直方图部分）是 GlancePlus 众多屏幕中通用的部分。屏幕的下部显示活动进程的摘要。

第 1 行提供 GlancePlus 的产品和版本号、时间、您的系统名称以及系统类型。在这种情况下，我们运行的是 GlancePlus 11.01 版本。

第 3 行提供关于 CPU 整体状态的信息。这通常是管理员最想知道的系统信息之一——我的 CPU 是否过载？

CPU 利用率条分为以下几部分：

1. “S” 表示用于“系统”活动（如上下文切换和系统调用）的时间。
2. “N” 表示运行“nice”用户进程（以低优先级运行的进程）的时间。
3. “U” 表示运行用户进程的时间。
4. “R” 表示实时进程。
5. “A” 表示运行负“nice”优先级进程的时间。

第 3 行的最右侧显示 CPU 利用率的百分比。如果您的系统是“CPU 受限”的，您将一致看到这个数值接近 100%。您可以获取当前、平均（自开始分析以来）和最高值的统计数据。

第 4 行显示最繁忙的已挂载磁盘的磁盘利用率。此条表示在更新间隔内文件系统和虚拟内存磁盘 I/O 的百分比。此条分为两部分：

1. “F” 表示用户读写及其他非分页活动的文件系统活动量。
2. “V” 表示用于分页虚拟内存的磁盘 I/O 百分比。

当前、平均和最高统计数据的含义与 CPU 利用率描述中的含义相同。

第 5 行显示系统内存利用率。此条分为三部分：

1. “S” 表示用于系统使用的内存量。
2. “U” 表示用于用户程序和数据内存量。
3. “B” 表示用于缓冲缓存的内存量。

当前、平均和最高统计数据的含义与 CPU 利用率描述中的含义相同。

第 6 行显示 Swap Util（交换利用率）信息，分为两部分：

1. “R” 表示已保留但未使用的部分。
2. “U” 表示正在使用的交换空间。

这三个区域（CPU、内存和磁盘）可以分别使用 F2、F3 和 F4 功能键进行更深入的分析。再次提醒，根据您运行的 GlancePlus 版本，您可能会看到不同的功能键。当您选择其中一个键时，您将从进程列表屏幕转到一个在所选区域提供更深入功能的屏幕。此外，许多其他系统区域还有更详细的屏幕。由于对进程列表屏幕之外的大部分调查都在 CPU、内存和磁盘屏幕上完成，我稍后将更详细地描述这些内容。

进程列表屏幕的底部显示在您的系统上运行的活动进程。由于 UNIX 系统上通常运行许多进程，您可能需要考虑使用 o 命令设置 CPU 利用率的阈值。例如，如果您设置 5% 的阈值，则只有在该间隔内平均 CPU 利用率超过 5% 的进程才会显示。还有其他类型的阈值可以指定，例如使用的 RAM 数量（Resident Size）。如果指定阈值，您只会看到您最感兴趣的进程，即那些消耗最多系统资源的进程。

对于满足您定义的阈值要求的每个活动进程都有一行。可能要显示多页进程。屏幕右下角的消息指示您所在的页码。您可以向前滚动查看下一页使用 f，向后滚动使用 b。通常，只有少数进程消耗了您大部分系统资源，因此我建议设置阈值，使得只显示一页进程。在 GlancePlus 中有一系列您可以发出的命令。本节中的最后一幅图显示了 GlancePlus 识别的命令。

以下是进程标题的简要摘要：

- **进程名称** 用于加载可执行程序的名称或缩写。
- *PID* 进程标识号。
- *PPID* 父进程的 PID。
- *Pri* 进程的优先级。数字越低，优先级越高。系统级进程通常在 0 到 127 之间运行。其他进程通常在 128 到 255 之间运行。“Nice”进程是优先级最低的进程，它们的数字最大。
- *用户名* 启动该进程的用户名称。
- *CPU Util* 第一个数字是该进程在更新间隔内消耗的 CPU 利用率百分比。请注意，对于我们的八处理器系统，最大值为 800%。第二个数字是自调用 GlancePlus 以来该进程消耗的 CPU 利用率百分比。大多数系统管理员让他们系统中的 GlancePlus 以较低的更新间隔持续运行。由于 GlancePlus 使用的系统开销极小，因此这样做几乎没有代价。
- *Cum CPU* 该进程使用的总 CPU 时间。GlancePlus 使用“midacmon”来收集信息。如果 **midacmon** 在进程启动前启动，您将得到进程使用的累积 CPU 时间的准确测量值。
- *Disk I/O Rate* 第一个数字是上一个更新间隔内的平均磁盘 I/O 速率（每秒）。第二个数字是自 GlancePlus 启动或自进程启动以来的平均磁盘 I/O 速率。磁盘 I/O 可以指代很多东西。磁盘 I/O 可以指第一次从磁盘获取数据块并将其放入 RAM，或者它可以完全是分页和交换。有些进程只需要比其他进程多得多得多的磁盘 I/O。然而，当这个数字非常高时，请仔细查看是否有足够的 RAM。请记住，如停用和交换等 pageout 活动归属于 *vhand* 进程。

### RSS 大小

进程消耗的 RAM 量（以 KB 为单位）。这称为常驻大小（Resident Size）。与进程相关且在 RAM 中的所有内容都包含在此列中，例如进程的数据、栈、文本和共享内存段。这是一个很好的检查列。由于慢速系统通常被错误地假设为受 CPU 限制，我总会特意查看此列，以识别主要应用程序使用的 RAM 量。这通常很有启示意义。有些应用程序使用少量的 RAM，但使用大型数据集，这一点在计算 RAM 时经常被忽视。此列显示了您的进程当前使用的所有 RAM。

### 阻塞原因

进程被阻塞（无法运行）的原因。如果进程当前被阻塞，您将看到原因。如果进程正在运行，您将看到它上次被阻塞的原因。进程被阻塞的原因有很多。在 *Thd Cnt* 之后列出了进程被阻塞的最常见原因。

### Thd Cnt

当前进程的线程总数。





| 缩写 | 进程被阻塞的原因 |
|---|---|
| CACHE | 等待缓存缓冲区可用 |
| DISK | 等待磁盘操作完成 |
| INODE | 等待 inode 操作完成 |
| IO | 等待非磁盘 I/O 完成 |
| IPC | 等待共享内存操作完成 |
| LAN | 等待局域网（LAN）操作完成 |
| MSG | 等待消息队列操作完成 |
| NFS | 等待 NFS 请求完成 |
| PIPE | 等待管道中的数据传递（输入或输出） |
| PRI | 因为正在运行更高优先级的进程而等待 |
| RFA | 等待远程文件访问（RFA）完成 |
| SEM | 等待信号量可用 |
| SLEEP | 因为进程调用了 **sleep** 或 **wait** 而等待 |
| SOCKT | 等待套接字操作完成 |
| SYS | 等待系统资源 |
| TERM | 等待终端传输 |
| VM | 等待虚拟内存操作完成 |
| OTHER | 等待原因 GlancePlus 无法确定 |

## CPU 报告屏幕说明

如果*进程列表*屏幕指示 CPU 过载，您需要参考图 12-5 中所示的*CPU 报告*屏幕。它可以提供关于 GlancePlus 报告的七种状态类型的有用信息。

![](img/eff8b9287a5f38c5adf538f24aacf29e_820_0.png)

对于七种状态类型中的每一种，都有提供额外信息的列。以下是这些列的说明：

- **Current**：显示在过去时间间隔内分配给此状态的 CPU 时间百分比。
- **Average**：显示自 GlancePlus 启动以来在此状态上花费的平均 CPU 时间百分比。
- **High**：显示自 GlancePlus 启动以来分配给此状态的最高 CPU 时间百分比。
- **Time**：显示在上一个间隔内在此状态上花费的 CPU 时间。
- **Cum Time**：显示自 GlancePlus 启动以来在此状态上花费的总 CPU 时间。

以下是七种状态的描述：

| 状态 | 描述 |
| :--- | :--- |
| User | 在普通优先级下执行用户活动所花费的 CPU 时间。 |
| Nice | 在 nice 模式下运行用户代码所花费的 CPU 时间。 |
| Negative Nice | 以高优先级运行代码所花费的 CPU 时间。 |
| Realtime | 执行以高优先级运行的实时进程所花费的 CPU 时间。 |
| System | 执行系统调用和程序所花费的 CPU 时间。 |
| Interrupt | 执行系统中断所花费的 CPU 时间。此处的高值可能表明存在大量的 I/O，例如分页和交换。 |
| ContSwitch | 在进程之间进行上下文切换所花费的 CPU 时间。 |
| Traps | 处理陷阱（traps）所花费的 CPU 时间。 |
| Vfaults | 处理页面错误（page faults）所花费的 CPU 时间。 |
| Idle | 处于空闲状态所花费的 CPU 时间。 |

###### HP GlancePlus/UX

CPU 报告屏幕还显示系统的运行队列长度或负载平均值。这显示在 CPU 报告屏幕的第二页。等待 CPU 的可运行进程数量的 Current、Average 和 High 值会被显示出来。您可能需要在系统大部分时间处于空闲时了解运行队列长度，并将这些数值与系统在正常使用情况下看到的数值进行对比。

CPU 报告屏幕上报告的最后一个区域是负载平均值、系统调用、中断和上下文切换。我不会过于仔细地检查这些数值，因为如果其中某项数值较高，它通常是问题的症状而非原因。如果您解决了问题，您会看到这些数值降低。

您可以使用 GlancePlus 查看系统中的所有 CPU，如图 12-6 所示。这是一个八处理器系统。

![](img/eff8b9287a5f38c5adf538f24aacf29e_822_0.png)

图 12-6 GlancePlus 中的“所有 CPU”屏幕

## 内存报告屏幕说明

图 12-7 中所示的*内存报告屏幕*提供了关于几种内存管理事件的信息。显示的统计数据是计数形式，而非百分比。您可能需要查看这些在系统大部分时间处于空闲时的计数，然后观察当系统负载逐渐增加时会发生什么。根据我的经验，内存瓶颈发生的次数远多于 CPU 瓶颈，因此您可能会发现此屏幕非常有用。

![](img/eff8b9287a5f38c5adf538f24aacf29e_823_0.png)

图 12-7 HP GlancePlus/UX *内存报告*屏幕截图

对于每个内存管理事件，显示以下五项统计数据：

- **Current**：过去间隔内事件发生的次数。如果您更新间隔，计数会发生变化，因此您可能需要选择一个您满意的间隔并坚持使用它。
- **Cumulative**：自 GlancePlus 启动以来该事件所有计数的总和。
- **Current Rate**：每秒的事件数。
- **Cum Rate**：在累计收集间隔内的平均速率。
- **High Rate**：记录到的最高速率。

以下是提供统计数据的内存管理事件的简要描述：

- **Page Faults**：任何地址转换错误，例如重新回收（reclaims）、进程 ID 错误（pid faults）等。
- **Page In/Page Out**：从虚拟内存（磁盘）移动到物理内存（页面调入）或相反方向（页面调出）的数据页。
- **KB Paged In**：因页面错误而调入的数据量。
- **KB Paged Out**：调出到磁盘的数据量。
- **Reactivations/Deactivations**：换入和换出内存的进程数量。内存不足的系统会花费大量时间进行进程的换入换出。如果大量进行此类交换，您可能会看到较高的 CPU 利用率，其他一些统计数据也可能随之增加。这些可能只是大量交换正在发生的症状。
- **KB Reactivated**：由于之前因 RAM 不足而换出的进程，结果换入 RAM 的信息量。
- **KB Deactivated**：进程移动到磁盘时换出的信息量。
- **VM Reads**：对磁盘进行虚拟内存读取的总次数。此数值越高，您的系统访问磁盘的频率就越高。
- **VM Writes**：内存管理 I/O 的总计数。

内存屏幕上还显示以下数值：

- **Total VM**：所有进程使用的虚拟内存总量。
- **Active VM**：所有活动进程使用的虚拟内存量。
- **Sys Mem**：分配给系统使用内存量。
- **Buf Cache Size**：缓冲区缓存的当前大小。
- **User Mem**：分配给用户使用的内存量。
- **Free Memory**：当前未分配使用的 RAM 量。
- **Phys Memory**：系统中的总 RAM 量。

此屏幕为您提供有关内存子系统使用情况的许多信息。您可能需要在系统大部分时间处于空闲和重度使用时查看一些统计数据，并对比这两者。一些值得记录的良好数值是“Free Memory”（查看在任何情况下是否都有空闲 RAM）和“Total VM”（查看为所有进程分配了多少虚拟内存）。内存充足的系统会有可用内存；而内存不足的系统会分配大量的虚拟内存。

## 磁盘报告屏幕说明

*磁盘报告*屏幕如图 12-8 所示。您可能会看到“本地”和“远程”信息的分组。

![](img/eff8b9287a5f38c5adf538f24aacf29e_826_0.png)

图 12-8 HP GlancePlus/UX *磁盘报告*屏幕截图

对于本地系统上挂载的所有磁盘的逻辑和物理访问相关的八种事件，提供了八项磁盘统计数据。这些事件代表了系统中发生的所有磁盘活动。

以下是提供的八项磁盘统计数据的描述：

- **Requests**：过去间隔内该类型请求的总数。
- **Percentage**：相对于其他类型，此类磁盘事件的百分比。
- **Average**：此类请求每秒的平均数量。
- **Total Bytes**：过去间隔内为该事件传输的字节总数。
- **Cumulative Requests**：自 GlancePlus 启动以来的累计请求数。
- **Cumulative Percentage**：自 GlancePlus 启动以来此类磁盘事件的相对百分比。
- **Cumulative Rate**：在累计收集间隔内的平均速率。
- **Cumulative Bytes**：自 GlancePlus 启动以来为此类事件传输的字节总数。

以下是提供这些统计数据的磁盘事件的描述，这些事件在您的系统中可能列在“Local”（本地）下：

- **Logical I/O**：磁盘的逻辑读写次数。由于磁盘通常使用内存缓冲区缓存，逻辑读取可能不需要物理访问磁盘。
- **Physical Reads**：磁盘的物理读取次数。这些物理读取可能是由于文件系统逻辑读取或虚拟内存管理导致的。
- **Physical Writes**：磁盘的物理写入次数。这可能是由文件系统活动或虚拟内存管理导致的。
- **File I/O**：由于用户文件 I/O 操作而产生的物理磁盘 I/O 量。
- **VM I/O**：由于虚拟内存管理活动而产生的物理磁盘 I/O 量。




## GlancePlus 概览

除了前面描述的进程列表、全局、屏幕以及 CPU、内存和磁盘屏幕外，还有许多其他有用的屏幕，包括以下内容：

- **交换空间（Swap Space）**：显示所有交换区域的详细信息。在其他版本中可能有不同的名称。
- **按接口查看网络（Netwk By Interface）**：提供有关系统中配置的每个局域网卡的详细信息。该屏幕在其他版本中可能有不同的名称。
- **NFS 全局（NFS Global）**：提供有关入站和出站 NFS 挂载文件系统的详细信息。在其他版本中可能有不同的名称。
- **选择进程（Select Process）**：允许你选择一个要调查的单个进程。在其他版本中可能有不同的名称。
- **按文件系统查看 I/O（I/O By File Sys）**：显示每个挂载磁盘分区的 I/O 详细信息。
- **按磁盘查看 I/O（I/O By Disk）**：显示每个挂载磁盘的 I/O 详细信息。
- **按逻辑卷查看 I/O（I/O By Logl Vol）**：显示每个挂载逻辑卷的 I/O 详细信息。
- **系统表（System Tables）**：显示内部系统表的详细信息。
- **进程阈值（Process Threshold）**：定义哪些进程将显示在进程列表屏幕上。在其他版本中可能有不同的名称，例如全局屏幕。

如你所见，虽然我已经详细描述了最常用的四个屏幕，但你还可以使用许多其他屏幕来进一步调查你的系统。

此外，你还可以在 GlancePlus 中发出许多命令。图 12-9 和 12-10 显示了 GlancePlus 中的*命令列表*屏幕。

![](img/eff8b9287a5f38c5adf538f24aacf29e_829_0.png)
图 12-9 HP GlancePlus/UX *命令列表* 屏幕 1

![](img/eff8b9287a5f38c5adf538f24aacf29e_830_0.png)
图 12-10 HP GlancePlus/UX 命令列表 屏幕 2

## 使用 VantagePoint 性能代理识别瓶颈

VantagePoint 性能代理允许你查看许多与系统性能相关的指标，这些指标可以帮助你识别系统中的瓶颈来源。你可以使用 GlancePlus 的图形版本（称为 gpm）来指定你要跟踪的指标。然后，你可以在 gpm 界面中查看它们，并以多种不同方式进行排序。

以下是在系统中可能遇到的最重要类型的瓶颈以及与每种瓶颈相关的指标。这些信息由 Hewlett-Packard 的两位性能专家 Doug Grumann 和 Stephen Ciullo 提供。

1.  **CPU 瓶颈** 使用 VantagePoint 性能代理：
    -   全局 CPU 利用率持续高企，且 `GBL_CPU_TOTAL_UTIL` > 90%，以及下一项。
    -   由 `GBL_PRI_QUEUE` 或 `GBL_RUN_QUEUE` > 3 指示的显著*运行队列*或*平均负载*。
    -   查找因优先级而阻塞的进程，其 `PROC_STOP_REASON` = PRI。

2.  **系统 CPU 瓶颈** 使用 VantagePoint 性能代理（与第 1 项相同，外加第一项）：
    -   大部分 CPU 时间花费在内核模式下，且 `GBL_CPU_SYS_MODE_UTIL` > 50%。
    -   全局 CPU 利用率持续高企，且 `GBL_CPU_TOTAL_UTIL` > 90%，以及下一项。
    -   由 `GBL_PRI_QUEUE` 或 `GBL_RUN_QUEUE` > 3 指示的显著*运行队列*或*平均负载*。
    -   查找因优先级而阻塞的进程，其 `PROC_STOP_REASON` = PRI。

3.  **上下文切换瓶颈** 使用 VantagePoint 性能代理（与第 2 项相同，外加第一项）：
    -   大量 CPU 时间花费在切换上，且 `GBL_CPU_CSWITCH` > 30%。
    -   大部分 CPU 时间花费在内核模式下，且 `GBL_CPU_SYS_MODE_UTIL` > 50%。
    -   全局 CPU 利用率持续高企，且 `GBL_CPU_TOTAL_UTIL` > 90%，以及下一项。
    -   由 `GBL_PRI_QUEUE` 或 `GBL_RUN_QUEUE` > 3 指示的显著*运行队列*或*平均负载*。
    -   查找因优先级而阻塞的进程，其 `PROC_STOP_REASON` = PRI。

4.  **用户 CPU 瓶颈** 使用 VantagePoint 性能代理（与第 1 项相同，外加第一项）：
    -   大部分 CPU 时间花费在用户模式下，且 `GBL_CPU_USER_MODE_UTIL` > 50%。
    -   全局 CPU 利用率持续高企，且 `GBL_CPU_TOTAL_UTIL` > 90%，以及下一项。
    -   由 `GBL_PRI_QUEUE` 或 `GBL_RUN_QUEUE` > 3 指示的显著*运行队列*或*平均负载*。
    -   查找因优先级而阻塞的进程，其 `PROC_STOP_REASON` = PRI。

5.  **磁盘瓶颈** 使用 VantagePoint 性能代理：
    -   至少一个磁盘设备利用率持续高企，且 `BYDSK_UTIL` > 50%。
    -   队列长度大于零，且 `BYDSK_QUEUE` > 0。
    -   进程或线程因多种原因在 I/O 上阻塞，其 `PROC_STOP_REASON` = `CACHE`、`DISK` 或 `IO`。
    -   查找因优先级而阻塞的进程，其 `PROC_STOP_REASON` = `PRI`。

6.  **缓冲池瓶颈** 使用 VantagePoint 性能代理：
    -   至少一个磁盘的中等利用率，且 `BYDSK_UTIL` > 25%。
    -   队列长度大于零，且 `BYDSK_QUEUE` > 0。
    -   低缓冲池读取命中率，且 `GLB_MEM_CACHE_HIT_PCT` < 90%。
    -   进程或线程在缓存上阻塞，其 `PROC_STOP_REASON` = `CACHE`。

7.  **内存瓶颈** 使用 VantagePoint 性能代理：
    -   高物理内存利用率，且 `GLB_MEM_UTIL` > 95%。
    -   显著的页面交换出或任何非活动化，且 `GLB_MEM_PAGEOUT_RATE` > 1 或 `GLB_MEM_SWAPOUT_RATE` > 0。
    -   vhand 进程持续活跃，且 vhand 的 `PROC_CPU_TOTAL_UTIL` > 5%。
    -   进程或线程在虚拟内存上阻塞，其 `PROC_STOP_REASON` = `VM`。

8.  **网络瓶颈** 使用 VantagePoint 性能代理：
    -   高网络数据包速率，且 `GLB_NET_PACKET_RATE` 平均值 > 2。请记住，这会根据配置有很大差异。
    -   正在发生任何输出排队，且 `GLB_NET_OUT_QUEUE` > 0。
    -   在网络上阻塞的进程或线程数量高于正常水平，其 `PROC_STOP_REASON` = `NFS`、`LAN`、`RPC` 或 `SOCKET`。
    -   `GLB_NETWORK_SUBSYSTEM_QUEUE` > 平均值。
    -   一个 CPU 的内核模式 CPU 利用率较高，而其他 CPU 大多处于空闲状态，且 `BYCPU_CPU_INTERRUPT_UTIL` > 30。
    -   使用 *tandadmin* 检查是否经常递增*出站丢弃（Out-bound Discards）*或存在过多的*冲突（Collisions）*。

为了识别你系统上的问题，你首先需要在系统运行顺畅且没有问题时对其进行特征描述。如果系统在某个方面开始表现不佳，你可以将运行顺畅系统的性能数据与可能存在问题的系统进行对比。

###### HP VantagePoint 性能代理和 HP VantagePoint 性能分析器/UX

有一些性能工具可以长时间跟踪和绘制数据图表。系统管理员通常将这一练习称为“容量规划”。容量规划的目标是查看长时间段内消耗了哪些系统资源，并确定可以对系统做出哪些调整或添加以改进性能并为未来做规划。我们将使用 HP VantagePoint 性能代理（即以前的 MeasureWare Agent）和 HP VantagePoint 性能分析器/UX（即以前的 PerfView Analyzer）一起查看系统的性能。这些工具在 HP-UX 上运行，与其他 UNIX 变体上运行的许多高级工具类似。

VantagePoint 性能代理安装在分布式环境中的各个单个系统上。它在单个系统上收集资源和性能测量数据。VantagePoint 性能分析器/UX 管理控制台，通常安装在管理系统的上，随后用于显示历史 VantagePoint 性能代理数据。你还可以使用 VantagePoint 性能代理设置由异常条件触发的警报。例如，如果 VantagePoint 性能代理检测到异常条件，如 CPU 利用率大于 90%，它会生成一条警报消息。然后，警报消息将通过 VantagePoint 性能分析器/UX 显示。我们将在接下来的示例中使用 VantagePoint 性能分析器/UX；然而，实际上 VantagePoint 性能组件有三个：




| | |
| --- | --- |
| *Monitor* | 通过接受来自 VantagePoint Performance 的警报来提供警报监控功能，并显示警报。 |
| *Planner* | 通过外推 VantagePoint Performance 数据进行预测，从而提供预测功能。 |
| *Analyzer* | 分析来自多个系统的 VantagePoint Performance 数据并显示数据。您可以同时查看来自多个系统的数据。 |

在我们的示例中，我们将针对单个系统进行操作。我们将获取在大约一周时间内收集的 VantagePoint Performance 数据，并展示其中的一部分。在这个示例中，我们不会从多个分布式系统获取数据，并且在该示例中仅使用一台服务器。

HP VantagePoint Performance 代理程序生成包含系统资源消耗信息的日志文件。HP VantagePoint Performance 代理程序运行时间越长，它在日志文件中记录的数据就越长。我经常被要求审查运行状况不佳的系统，并提出系统升级建议。我通常运行 HP VantagePoint Performance 代理程序至少一周，以便在足够长的时间段内获取日志信息，从而获得有用的数据。对于一些系统而言，这段时间可能是数月。对于负载规律的其他系统，一周可能已经足够。

在运行 VantagePoint Performance 一周后，我调用了 VantagePoint Performance Analyzer/UX 来查看这一周内发生的系统资源利用率水平。我们将查看的图表包括 CPU、内存和磁盘。图 12-11 显示了一周的全球 CPU 摘要：

![](img/eff8b9287a5f38c5adf538f24aacf29e_836_0.png)

图 12-11 全球 CPU 摘要界面

您可以使用 VantagePoint Performance Analyzer/UX 调整该图表的几乎所有可想象的特征。不幸的是，书中的这张图表丢失了颜色。所使用的颜色使您在计算机屏幕上查看图表时能够识别参数。总 CPU 利用率始终是图表中的最高点，它是系统模式和用户模式利用率的总和。

图 12-11 展示了经典的 CPU 利用率，主要时段反映了高 CPU 利用率，非主要时段反映了低 CPU 利用率。然而，在某些方面，这个图表可能会产生误导。由于每三个小时会出现一个数据点，因此每个 24 小时周期有八个小刻度，您无法看到在更短时间窗口内的实际 CPU 利用率。例如，我们无法准确看到 CPU 在早上何时变得负载严重。我们可以看到它是在第二个和第三个刻度之间，但这是一段很长的时间 - 在上午 6:00 到 9:00 之间。在一天结束时也存在同样的缺乏细粒度的问题。我们可以看到 CPU 利用率在第五和第七个刻度之间明显下降，但这并没有给我们一个清晰的视图。

图 12-12 显示了在更短时间窗口内的 CPU 利用率。

![](img/eff8b9287a5f38c5adf538f24aacf29e_837_0.png)

图 12-12 全球 CPU 摘要 - 短时间周期

图 12-12 显示了在更短时间窗口内更细粒度的 CPU 利用率。这种更细粒度的窗口使人们清楚地看到全天发生的活动高峰。例如，在上午 8:30 出现了一个明显的登录高峰。

内存利用率也可以在整周期间以图表形式显示，如图 12-13 所示。

![](img/eff8b9287a5f38c5adf538f24aacf29e_838_0.png)

用户内存利用率是图表的底线，大致对应于前面显示的 CPU 利用率。在非主要时段，用户内存利用率较低，而在主要时段较高。

系统内存利用率是图表的中间线，在一周内保持相对稳定。

总内存利用率始终是图表的顶线，它是系统利用率和用户利用率的总和。由于系统内存利用率大致保持不变，它随用户利用率的升降而升降。

此图表上数据点之间三个小时的间隔可能无法提供我们所需的细粒度。图 12-14 显示了在更短时间窗口内的内存利用率。

![](img/eff8b9287a5f38c5adf538f24aacf29e_839_0.png)

图 12-14 全球内存摘要 - 短时间周期

图 12-14 显示了在更短时间窗口内更细粒度的内存利用率。现在您可以精确地看到内存利用率在大约一天的时间内是如何变化的。

磁盘利用率也可以在整周期间以图表形式显示，如图 12-15 所示。

![](img/eff8b9287a5f38c5adf538f24aacf29e_840_0.png)

图 12-15 全球磁盘摘要

与 CPU 和内存图表一样，这是一整周的磁盘使用情况。由于该图表上出现了许多峰值，我们肯定希望查看和分析更短的时间窗口。

图 12-16 显示了在更短时间窗口内的磁盘利用率。

![](img/eff8b9287a5f38c5adf538f24aacf29e_841_0.png)

图 12-16 全球磁盘摘要 - 短时间周期

这个大约三小时的更短时间窗口显示了更多的细节。在深夜出现了巨大的磁盘活动峰值。这些可能由多种原因引起，包括批处理作业处理或系统备份。

您不仅可以一次查看与单个系统资源相关的参数。您还可以同时查看许多系统资源的使用方式，如图 12-17 所示。

![](img/eff8b9287a5f38c5adf538f24aacf29e_842_0.png)

图 12-17 全球摘要历史界面

该图表包含许多系统资源，包括 CPU、磁盘和内存。当同时显示如此多的系统资源时，您肯定希望查看更短的时间段。

图 12-18 显示了在更短时间窗口内的相同参数。

![](img/eff8b9287a5f38c5adf538f24aacf29e_843_0.png)

图 12-18 全球摘要 - 短时间周期

图 12-18 显示了在更短时间窗口内许多系统资源利用率的更细粒度。现在您可以查看各种系统资源与其他系统资源之间的关系。

您可以通过一个名为 **perfstat** 的实用命令找到在您的系统上运行的 VantagePoint Performance Analyzer/UX 的状态。以下示例展示了使用“-?”选项发出 **perfstat** 命令以查看所有 **perfstat** 选项：

```
# perfstat -?

usage: perfstat [options]

Unix option Function
-? List all perfstat options.
-c Show system configuration information.
-e Search for warnings and errors from
   performance tool status files.
-f List size of performance tool status files.
-p List active performance tool processes.
-t Display last few lines of performance tool
status files.
-v List version strings for performance tool files.
-Z Dump perfstat info to a file and tar tape.
```

使用 `-c` 选项，您可以获取有关系统配置的信息，如下面的列表所示：

```
# perfstat -c

********************************************************************
** perfstat for rp ux6 on Fri May 15 12:20:06 EDT
********************************************************************

system configuration information:

uname -a: HP-UX ux6 B.11.00 E 9000/800 71763 8-user license

mounted file systems with disk space shown:
Filesystem          kbytes    used    avail %used Mounted on
/dev/vg00/lvol3     85016    27675  54736  34% /
/dev/vg00/lvol1     67733   44928  16031  74% /stand
/dev/vg00/lvol8    163840   56995  90927  42% /var
/dev/vg00/lvol7    497712  358775 132155  73% /usr
/dev/rp06vg tmp /tmp       4319777 1093927 3134084 26% /tmp
/dev/vg00/lvol6     270336  188902  76405  71% /opt
/dev/vg root1/ var   640691   15636  605834   3% /newvar
/dev/vgroot1/usr    486677  356866 115210  76% /newusr
/dev/vgroot1/stand  677733   45109  58580  74% /newstand
/dev/vgroot1/root    83733   21181  54178  28% /newroot
/dev/vgroot1/opt     263253  188109  67246  74% /newopt
/dev/vg00/lvol15     20480     119   8168   6% /home

LAN interfaces:
Name           Mtu        Network       Address       Ipkts     Opkts
lo0            4136      127.0.0.0     localhost     77442     77442
lan0           1500      192.60.11.0   rp-ux6       7847831   12939169

********************************************************************
           (end of perfstat -c output)  *************
```

使用 `-f` 选项显示性能工具状态文件的大小，如下面的列表所示：



## perfstat -f

# perfstat -f

```
*************************************************************
***  perfstat for ux6 on Fri May 15 12:20:08 EDT
*************************************************************
```

位于 /var/opt/perf 目录下的性能工具状态文件的 ls -l 列表：

```
-rw-rw-rw-    1 root     root      7812 May 10 19:35 status_alarmgen
-rw-r-r--     1 root     root         0 May 10 02:40 status.mi
-rw-rw-rw-    1 root     root      3100 May 10 02:40 status_perfIbd
-rw-rw-rw-    1 root     root      3978 May 10 02:40 status_rep_server
-rw-r-r-----    1 root     root      6079 May 11 23:30 status.scope
-rw-r-r-----    1 root     root         0 Mar 31 07:26 status.ttd
```
`**** (end of perfstat -f output) ****`

使用 -v 选项可以显示正在运行的性能工具的版本字符串，如下面的列表所示：

# perfstat -v

```
*************************************************************
***  perfstat for ux6 on Fri May 15 12:20:08 EDT
*************************************************************

listing version strings for performance tool files:

NOTE: The following software version information can be compared with the version information shown in the /opt/perf/ReleaseNotes file(s).
```

| /opt/perf/bin 目录中的 MeasureWare 可执行文件 | 版本 | 日期/操作系统 |
| :--- | :--- | :--- |
| scopeux | C.01.00 | 12/17/97 HP-UX 11.0+ |
| ttd | A.11.00.15 | 12/15/97 HP-UX 11.0+ |
| perflbd | C.01.00 | 12/17/97 HP-UX 11.0+ |
| alarmgen | C.01.00 | 12/17/97 HP-UX 11.0+ |
| agdbserver | C.01.00 | 12/17/97 HP-UX 11.0+ |
| agsysdb | C.01.00 | 12/17/97 HP-UX 11.0+ |
| rep_server | C.01.00 | 12/17/97 HP-UX 11.0+ |
| extract | C.01.00 | 12/17/97 HP-UX 11.0+ |
| utility | C.01.00 | 12/17/97 HP-UX 11.0+ |
| mwa | A.10.52 | 12/05/97 |
| perfstat | A.11.01 | 11/19/97 |
| dlslog | C.01.00 | 12/17/97 HP-UX 11.0+ |
| sdilcomp | C.01.00 | 12/17/97 HP-UX 11.0+ |
| sdi1expt | C.01.00 | 12/17/97 HP-UX 11.0+ |
| sdigendata | C.01.00 | 12/17/97 HP-UX 11.0+ |
| sdiltil | C.01.00 | 12/17/97 HP-UX 11.0+ |

| /opt/perf/lib 目录中的 Measureware 库 | 版本 | 日期/操作系统 |
| :--- | :--- | :--- |
| libmwa.sl | C.01.00 | 12/17/97 HP-UX 11.0+ |
| libmwa.a | A.11.00.15 | 12/15/97 HP-UX 11.0 |
| libarm.sl | A.11.00.15 | 12/15/97 HP-UX 11.00 |

| /var/opt/perf 目录中的 Measureware 指标描述文件 | 版本 | 日期 |
| :--- | :--- | :--- |
| metdesc | C.01.00 | 12/17/97 |

所有关键的 MeasureWare 文件均可访问

```
  libnnums.sl   B.11.00.15 12/15/97 HP-UX 11.00
  midaemon      B.11.00.15 12/15/97 HP-UX 11.00
  g1ance        B.11.01    12/16/97 HP-UX 11.00
  gpm           B.11.01    12/16/97 HP-UX 11.00
```

`************ (end of perfstat -v output) *************`

## 第 13 章

### 网络

## 虚拟分区与网络

每个虚拟分区至少应配备一张专用网络卡。vPar 将通过网络卡与其他 vPar 及其他系统进行通信。与所有组件一样，不同虚拟分区中的网络卡是相互独立管理的，并且与其所附着的虚拟分区也是独立管理的。在接下来的章节中，我们将对虚拟分区的网络卡和整体网络进行一些基本操作。我们将查看网络卡的配置，以及虚拟分区如何通过网络相互通信——即使这些 vPar 运行在同一系统上也是如此。

要在同一系统上运行的两个虚拟分区之间执行如 **telnet** 或*文件传输协议*等基本任务，您需要使用它们的网络卡。没有允许 vPar 之间通过背板而非通过各自 vPar 的网络卡进行通信的低级 vPar 专用功能。

![](img/eff8b9287a5f38c5adf538f24aacf29e_849_0.png)

### 虚拟分区的主机相关信息

虚拟分区的一个方面可能会让人困惑，即与每个虚拟分区相关的主机信息。虚拟分区从所有实际用途上来说都是不同的主机。这意味着，连接到某个虚拟分区的系统认为它与运行在同一服务器上的任何其他虚拟分区都是完全独立的主机。因此，对于每个虚拟分区，您既有定义该虚拟分区的信息，也有定义主机的信息。从网络角度来看，例如使用 telnet 连接到虚拟分区时，您会使用主机名。从虚拟分区角度来看，例如执行 **vparstatus** 等 VPar 命令时，您会使用 VPar 名称。最好让这两个名称保持一致，这样您就可以使用同时定义 VPar 和主机名的一个名称来执行任何命令。

在我们第 2 章的早期示例中，我们在两个单独的磁盘上加载了 HP-UX 11i，每个磁盘将用于一个单独的虚拟分区。在为各自的虚拟分区加载操作系统时，您可以在加载操作系统时指定主机相关信息。例如，在加载 HP-UX 11i 时，您可以输入主机名和其他系统相关信息。每个 HP-UX 11i 实例的此信息是不同的，因为即使虚拟分区运行在同一物理服务器上，11i 的实例用于不同的虚拟分区。虚拟分区实际上是不同的主机，因此将具有不同的系统相关参数。在 HP-UX 11i 安装完成后，或者在虚拟分区启动并运行后，可以使用 **set_params** 更改每个虚拟分区的主机相关信息。

![](img/eff8b9287a5f38c5adf538f24aacf29e_849_1.png)

对于习惯只使用一个 HP-UX 实例和因此只有一组主机相关信息的服务器 Unix 用户来说，一台物理计算机上有多个主机的概念可能需要一点时间才能适应。

虚拟分区相关信息，如名称，可以使用 **vparmmodify** 进行修改。主机相关信息使用 **set_params** 进行更新（或通过手动更新相应的文件）。因此，对于每个虚拟分区，您既有定义该虚拟分区的信息，也有定义主机的信息。

让我们使用 **vparstatus** 查看两个虚拟分区，以查看这两个 VPar 的 LAN 接口对应的 I/O 地址：

```
# vparstatus -v

[Virtual Partition Details]
Name:  cable1
State:  Up
Attributes:  Dynamic,Manual
Kernnel Path:  /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max:  2/3
Bound [Path]:  33
        37
Unbound [Path]:

[IO Details]
    2.9.2.1.2.0  BOOT
    2.5.4.0  CONSOLE
    0.0.0.0                <-- LAN for cable1
    0.7.1.0.3.0

[Memory Details]         *
Specified [Base  /Range]:
        (bytes) (MB)
Total Memory (MB):  2048

[Virtual Partition Details]
Name:  cable2
State:  Up
Attributes:  Dynamic,Manual
Kernnel Path:  /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max:  1/2
Bound [Path]:  97
Unbound [Path]:  101

[IO Details]
    0.8.0.0.0.0.5.0.0.0, BOOT
    0.10.0.0          <-- LAN for cable2

[Memory Details]
Specified [Base  /Range]:
        (bytes) (MB)
Total Memory (MB): 1024
```

这两个硬件路径对应于不同的本地总线适配器（LBA），这是撰写本文时的要求。第一个 vPar 使用 LBA 0 上的 Core I/O 卡，第二个 vPar 使用 LBA 10。现在让我们继续查看这两张卡的软件配置。

我们在第 2 章的许多示例中大量使用了名为 *cable1* 的 vPar。以下内容显示了 vPar *cable1* 上 /etc/hosts 文件的内容：

```
# cat /etc/hosts
# @(B)B,i1.i1_LRhosts $Revision: 1.9.214.1 $ $Date: 96/10/08
13:20:01 $
#
# The form for each entry is:
# <internet address>	<official hostname>	<aliases>
#
# For example:
# 192.1.2.34	hpcrm loghost
#
# See the hosts(4) manual page for more information.
# Note: The entries cannot be preceded by a space.
#	The format described in this file is the correct format.
# The original Berkeley manual page contains an error in
# the format description.
#
172.16.15.36	cvhdccon3
172.16.14.44	cvhdccon4
127.0.0.1	localhost	loopback
#
```

此文件中未提及 vPar 名称 *cable1*。就 HP-UX 而言，*cvhdccon3* 的主机名是该主机和此虚拟分区所需的全部信息。该系统上运行的第二个 vPar 的主机名是 *cvhdccon4*。这两个主机之间的通信是通过网络电缆使用 /etc/hosts 中显示的两个主机名进行的。/etc/hosts 文件中不存在 vPar 名称。所有与 vPar 相关的信息都在 /etc/vpdb 中。如果您的*主机名*和虚拟分区名称确实不同，您可能希望添加 vPar 名称的别名。您可以为 *cable1* 在 /etc/hosts 文件中添加 *cvhdccon3* 的别名，并为 *cable2* 添加 *cvhdccon4* 的别名。

现在让我们在两个主机上运行 **iconfig**，以查看网络接口是如何设置的：




请注意，第一个 vPar 的 LAN 接口为 *lan0*，第二个为 *lan1*。该服务器有两个 LAN 接口，尽管它们属于不同的 vPar 和 HP-UX 实例，但为了让服务器能够区分这两个接口，需要使用两个不同的 LAN 接口名称；我们将在接下来的 `netconf` 文件中看到这一点。

与主机相关的信息存储在 `/etc/rc.config.d/netconf` 中。以下列表显示了与 *cvhdcn3* 相关的信息，同样没有提及 vPar 名称 *cable1*：

# 主机 cvhdcn3 (vPar cable1) 上的 netconf

```bash
# cat /etc/rc.config.d/netconf
#
# netconf: 核心网络子系统的配置值
#
# @(#)B.11.11_LR $Revision: 1.6:119.6 $ Date: 97/09/10 15:56:01 $
#
# HOSTNAME:              用于 uname -s 和 hostname 的系统名称
# OPERATING_SYSTEM:       uname -s 返回的操作系统名称
#                        ---- 请勿更改此值 ----
#
# LOOPBACK_ADDRESS:      回环地址
#                        ---- 请勿更改此值 ----
#
# 重要提示：在 9.x 到 10.0 的迁移过程中，不要在
# 下一组语句之间插入空行

HOSTNAME="cvhdcn3"
OPERATING_SYSTEM=HP-UX
LOOPBACK_ADDRESS=127.0.0.1

# 互联网配置参数。参见 ifconfig(Im), autopush(IIm)
#
# INTERFACE_NAME:  网络接口名称（参见 lanscan(lm)）
# IP_ADDRESS:      主机名（在 /etc/hosts 中）或点分十进制 IP 地址
#     点分十进制表示的子网掩码（如果与默认值不同）
#
# BROADCAST_ADDRESS:
#     点分十进制表示的广播地址（如果与默认值不同）
#
# INTERFACE_STATE:
#     启动时所需的接口状态。
#         可以是 up 或 down；默认为 up。
#
# DHCP_ENABLE:
#     决定是否在网络接口上启用 DHCP 客户端功能
#     （参见 auto_parms(8M), dhclient(8M)）。DHCP 客户端
#     从 DHCP 服务器获取 IP 地址分配。
#         1 启用 DHCP 客户端功能；0 禁用它。
#
# 对于每个额外的网络接口，添加一组类似下面的变量赋值，
# 将索引更改为 "[1]"、"[2]" 等。
#
# 重要提示：在 9.x 到 10.0 的迁移过程中，不要在
# 下一组语句之间插入空行
#
INTERFACE_NAME[0]=lan0            <--  lan0
IP_ADDRESS[0]=172.16.15.34
SUBNET_MASK[0]=255.255.255.0
BROADCAST_ADDRESS[0]=255.255.255.255
INTERFACE_STATE[0]=""
DHCP_ENABLE[0]=0

# 互联网路由配置。参见 route(1M), routing(7M)
#
# ROUTE_DESTINATION:
#     目标主机名（在 /etc/hosts 中）或主机或网络
#     点分十进制 IP 地址，前面加上单词
#     "host" 或 "net"；或者简单地使用单词 "default"。
#
# ROUTE_MASK:
#     点分十进制表示的子网掩码，或 C 语言
#     十六进制表示。这是一个可选字段。
#     如果地址和子网掩码对能唯一标识
#     要到达的子网，如果未给出子网掩码，
#     则系统将为该路由分配已配置网络接口中
#     最长的子网掩码。
#     如果没有匹配的子网掩码，则系统
#     将分配默认网络掩码作为该路由的
#     子网掩码。
#
# ROUTE_GATEWAY:
#     网关主机名（在 /etc/hosts 中）或点分
#     十进制 IP 地址。如果是本地接口，必须使用
#     上述 IP 地址所使用的相同格式（主机名或
#     点分十进制表示）。如果是回环接口，即
#     127.0.0.1，则必须将 ROUTE_COUNT 设置为零。
#
# ROUTE_COUNT:
#     一个整数，表示网关是
#     远程接口（1）还是本地接口（0）
#     或回环接口（例如 127.*）。
#
# ROUTE_ARGS:
#     路由命令的参数和选项。此变量
#     可以包含以下参数的组合：
#     "-X", "-n" 和 "-p geiu"。
#
# 对于每条额外的路由，添加一组类似下面的变量赋值，
# 将索引更改为 "[1]"、"[2]" 等。
#
# 重要提示：在 9.x 到 10.0 的迁移过程中，不要在
# 下一组语句之间插入空行
#
ROUTE_DESTINATION[0]=default
ROUTE_MASK[0]=0.0.0.0
ROUTE_GATEWAY[0]=172.16.15.1
ROUTE_COUNT[0]=1
ROUTE_ARGS[0]=""

# 动态路由守护程序配置。参见 gated(1M)
#
# GATED:
#     设置为 1 以启动 gated 守护程序。
#
# GATED_ARGS: gated 守护程序的参数。
GATED=0
GATED_ARGS=""

#
# 路由器发现协议守护程序配置。参见 rdpd(1m)
# # RDPD: 设置为 1 以启动 rdpd 守护程序
#
RDPD=0

#
# 反向 ARP 守护程序配置。参见 rarpd(1m)
# # RARP: 设置为 1 以启动 rarpd 守护程序
#
RARP=0

ROUTE_GATEWAY[0]=172.16.15.1
ROUTE_COUNT[0]=1
ROUTE_DESTINATION[0]=default
#
```

尽管该文件包含大量信息，如主机名、IP 地址、子网掩码和网关，但没有关于任何 vPar 特定信息的条目。

cvhdcn4 的 /etc/rc.config.d/netconf 指定 lan1 作为此 vPar 的网络接口，如下列列表所示。这两个独立的主机必须通过它们各自的网络接口进行通信。系统中有一个专门用于 cvhdcn3 (vPar cable1) 的 lan 接口 (lan0)，以及第二个专门用于 cvhdcn4 (vPar cable2) 的 lan 接口 (lan1)。各自 netconf 文件中的 lan0 和 lan1 引用是必需的，以便将两张 lan 卡分配给它们各自的 vPar。

# 主机 cvhdcn4 (vPar cable2) 上的 netconf

```bash
# cat /etc/rc.config.d/netconf
# netconf: 核心网络子系统的配置值

# @(#)B.11.11_LR $Revision: 1.6.119.6 $ $Date: 97/09/10 15:56:01 $

# HOSTNAME: 用于 uname -s 和 hostname 的系统名称
# OPERATING_SYSTEM: uname -s 返回的操作系统名称
# ---- 请勿更改此值 ----
# LOOPBACK_ADDRESS: 回环地址
# ---- 请勿更改此值 ----
#
# 重要提示：在 9.x 到 10.0 的迁移过程中，不要在
# 下一组语句之间插入空行

HOSTNAME="cvhdcn4"
OPERATING_SYSTEM=HP-UX
LOOPBACK_ADDRESS=127.0.0.1

# 互联网配置参数。参见 ifconfig(1m), autopush(1m)
#
#INTERFACE_NAME:  网络接口名称（参见 lanscan(1m)）
#
#IP_ADDRESS:
       主机名（在 /etc/hosts 中）或点分十进制
       表示的 IP 地址（例如，192.1.2.3）
#
#SUBNET_MASK:     点分十进制表示的子网掩码，如果与默认值不同
                  则使用此值
#
#BROADCAST_ADDRESS: 点分十进制表示的广播地址，如果
                    与默认值不同则使用此值
#
#INTERFACE_STATE: 启动时所需的接口状态。
                  可以是 up 或 down，默认为 up。
#
#DHCP_ENABLE:
       决定是否在网络接口上启用 DHCP 客户端功能
       （参见 auto_parms(1M), dhclient(1M)）。DHCP 客户端
       从 DHCP 服务器获取 IP 地址分配。
       1 启用 DHCP 客户端功能，0 禁用它。
#
# 对于每个额外的网络接口，添加一组类似下面的变量赋值，
# 将索引更改为 [1]、[2] 等。
#
# 重要提示：在 9.x 到 10.0 的迁移过程中，不要在
# 下一组语句之间插入空行

INTERFACE_NAME[0]=lan1                <--  lan1
IP_ADDRESS[0]=172.16.14.44
SUBNET_MASK[0]=255.255.255.0
BROADCAST_ADDRESS[0]=255.255.255.255
INTERFACE_STATE[0]=""
DHCP_ENABLE[0]=0

# 互联网路由配置。参见 route(1m), routing(7)
#
#ROUTE_DESTINATION: 目标主机名（在 /etc/hosts 中）或主机或网络
                   点分十进制 IP 地址，前面加上单词
                   "host" 或 "net"，或者简单地使用单词 "default"。
#
#ROUTE_MASK:      点分十进制表示的子网掩码，或 0（C 语言
                  十六进制表示）。这是一个可选字段。
                  IP 地址和子网掩码对能唯一标识
                  要到达的子网。如果未给出子网掩码，
                  则系统将为该路由分配已配置网络接口中
                  最长的子网掩码。
                  如果没有匹配的子网掩码，则系统
                  将分配默认网络掩码作为该路由的
                  子网掩码。
#
#ROUTE_GATEWAY:   网关主机名（在 /etc/hosts 中）或点分
                  十进制 IP 地址。本地接口必须使用
                  上述 IP 地址所使用的相同格式（localhost 或
                  点分十进制表示）。如果是回环接口，即
                  127.0.0.1，则必须将 ROUTE_COUNT 设置为零。
#
#ROUTE_COUNT:     一个整数，表示网关是
                  远程接口（1）还是本地接口（0）
                  或回环接口（例如 127.*）。
#
#ROUTE_ARGS:      路由命令的参数和选项。此变量
                  可以包含以下参数的组合：
                  "-r", "-n" 和 "-p "per"。
#
# 对于每条额外的路由，添加一组类似下面的变量赋值，
# 将索引更改为 [1]、[2] 等。
#
# 重要提示：在 9.x 到 10.0 的迁移过程中，不要在
# 下一组语句之间插入空行

# ROUTE_DESTINATION[0]=default
# ROUTE_MASK[0]=0.0.0.0
# ROUTE_GATEWAY[0]="172.16.14.1"
# ROUTE_COUNT[0]="1"
```





# 虚拟分区主机相关信息

```
# ROUTE_ARGS[0]=""

# 动态路由守护进程配置。参见 gated(1m)
# GATED: 设置为 1 以启动 gated 守护进程。
# GATED_ARGS: 传递给 gated 守护进程的参数。

GATED=0
GATED_ARGS=""

# 路由器发现协议守护进程配置。参见 rdpd(1m)
# RDPD: 设置为 1 以启动 rdpd 守护进程

RDPD=0

# 逆 ARP 守护进程配置。参见 rarpd(1m)
# RARP: 设置为 1 以启动 rarpd 守护进程

RARP=0

ROUTE_GATEWAY[0]=172.16.14.1
ROUTE_COUNT[0]=1
ROUTE_DESTINATION[0]=default
```

我们也可以在 SAM 中查看和配置与网络相关的信息。图 13-1 展示了 SAM 中第二个 vPar（*cable2*）上 *lan1* 的与网络相关的信息：

![](img/eff8b9287a5f38c5adf538f24aacf29e_857_0.png)

这些窗口显示了我们之前在各个文件和命令行中查看到的信息。一些系统管理员更喜欢在 SAM 中修改和查看信息，而另一些则更喜欢在命令行中操作。

### 使用两张网卡配合 Telnet

分配给虚拟分区的局域网卡可以像在非 vPar 系统上那样用于多种用途。当两个不同 vPar 中的用户或应用程序进行通信时，它们是通过局域网进行的。在正常操作中，vPar 并没有为通信提供任何特殊的机制。（然而，vPar 之间确实存在特殊的系统管理通信，例如虚拟分区数据库的同步，这是以特殊方式进行的。）当在两个 vPar 之间建立通信会话时，即使它们位于同一台服务器上，也会使用两个 vPar 上的局域网接口。这包括 `telnet`、`ftp` 以及 Berkeley 的“r”命令，如 `rlogin`。以下示例展示了书中许多示例中使用的两个 vPar 之间的 `telnet` 会话。在此示例中，vPar `cable1`（主机名 `cvhdcon3`）发起与 vPar `cable2`（主机名 `cvhdcon4`）的 `telnet` 会话：

```
# hostname cvhdcon3
# telnet cvhdcon4
Telnet3 - <--- 在 cable1 上开始
已连接到 cvhdcon4。 <--- telnet 到 cable2
转义字符是 `^]'.
本地流量控制已开启
Telnet TERMINAL-SPEED 选项已开启
HP-UX cvhdcon4 B.11.11 U 9000/800 (tc)

login: root
Password:
请稍候...正在检查磁盘配额
(c) Copyright 1983-2000 Hewlett-Packard Co., All Rights Reserved.
(c) Copyright 1973, 1980, 1983, 1985-1993 The Regents of the Univ. of California
(c) Copyright 1980, 1984, 1986 Novell, Inc.
(c) Copyright 1986-1992 Sun Microsystems, Inc.
(c) Copyright 1985, 1986, 1988 Massachusetts Institute of Technology
(c) Copyright 1989-1993 The Open Software Foundation, Inc.
(c) Copyright 1986 Digital Equipment Corp.
(c) Copyright 1990 Motorola, Inc.
(c) Copyright 1990, 1991, 1992 Cornell University
(c) Copyright 1989-1991 The University of Maryland
(c) Copyright 1998 Carnegie Mellon University
(c) Copyright 1991-2000 Mentor Inc.
(c) Copyright 1996 Morning Star Technologies, Inc.
(c) Copyright 1996 Progressive Systems, Inc.
(c) Copyright 1991-2000 Isoftex Corporation, All Rights Reserved.

RESTRICTED RIGHTS LEGEND
美国政府的使用、复制或披露受 DFARS 252.227-7013 中技术数据和计算机软件权利条款子段 (c)(1)(ii) 中规定的限制。

Hewlett-Packard Company
3000 Hanover Street
Palo Alto, CA 94304 U.S.A.

非国防部的美国政府部门和机构的权利如 FAR 52.227-19(c)(1,2) 中所述。

TERM 的值已设置为 "hp"。
警告：您是超级用户 !!

# hostname
cvhdcon4    <--- 已连接到 cable2
#
```

只有当您的系统中有两张网络卡——每个 vPar 一张——时，您才能使用 **telnet**、**rlogin** 或其他类似的连接方法。对于其他功能也是如此，例如从 vPar 备份到另一个具有本地磁带驱动器的 vPar 或系统，这要求两个系统都必须有网卡。我认为为每个 vPar 配备一张专用网卡是必要的。

本章剩余部分包含大量的网络背景信息。

网络配置因安装环境而异。一些安装环境，例如高度集中且隔离的系统，仅连接 ASCII 终端，系统管理员只需很少关注网络。而其他安装环境，例如高度分布式的环境，其中成千上万台系统连接到可能跨越多个地理位置的网络，系统管理员可能需要大量关注网络。在后一种场景中，系统管理员用于网络的时间可能超过用于所有其他系统管理功能时间的总和！而不是像第一位系统管理员那样完全忽略网络，或像第二位系统管理员那样可能需要涵盖网络管理的所有方面，我将在本章中介绍适用于大多数 UNIX 系统的网络方面。这些内容基于我在各种新的 UNIX 安装环境中工作的经验。如果您需要的网络背景知识超出了本章涵盖的范围，我推荐以下书籍作为出色的网络信息来源：Bruce H. Hunter 和 Karen Bradford Hunter 著的 *UNIX Networks*（Prentice Hall，ISBN 0-13-08987-1）。

在本章中，我主要提供许多网络主题的背景知识，而非设置信息，因为设置工作主要由系统管理员执行。我所涵盖的大部分内容有时被称为“互联网服务”。总的来说，我将在本章中介绍网络的基础知识。这包括 ARPA 和 Berkeley 服务。以下是我涵盖的主题列表：

-   通用 UNIX 网络背景
-   互联网协议 (IP) 寻址（A、B 和 C 类）
-   子网掩码
-   ARPA 服务
-   Berkeley 命令
-   主机名映射
-   网络文件系统 (NFS) 背景
-   UNIX 网络命令

我在本章中提供了许多 UNIX 命令的摘要和示例。关于这些命令的更多详细信息可以在您的 HP-UX 系统的联机手册页中找到。虽然 vPars 仅运行在 HP-UX 上，但我在本章的示例中使用了多种系统，包括 Solaris、AIX 和 HP-UX。由于 HP-UX 系统管理员通常管理许多 UNIX 变体，因此我希望提供尽可能全面的示例集。

### UNIX 网络

连接到其他机器是每个 UNIX 网络的重要组成部分。这意味着既连接其他 UNIX 机器，也连接非 UNIX 机器。机器必须在物理上相互连接，并在功能上相互连接，以便您可以执行诸如传输文件和登录其他系统之类的任务。您的 UNIX 系统上存在许多命令，为您提供在系统之间登录和传输文件的功能。这些被称为 ARPA 命令，即 telnet 和 ftp。

telnet 命令允许在异构环境中进行远程登录。例如，从您的 UNIX 系统，您可以 telnet 到非 UNIX 系统并登录。在远程系统上登录后，您需要了解正在该系统上运行的操作系统。如果您需要连接另一台计算机只是为了在系统之间传输文件，那么您可以使用 ftp。此命令允许您在任意两个系统之间传输文件，而无需了解远程系统上运行的操作系统。

与可以在 UNIX 系统之间发出的命令相比，这些命令相对原始。对于 UNIX 系统而言，网络不是事后需要添加到系统中的附加部分。ftp 和 telnet 命令随您的 UNIX 系统提供，以及您可以用来在您的 UNIX 系统和其他 UNIX 系统之间通信的更高级命令和功能。这些更高级的命令被称为 Berkeley 命令，允许您远程执行许多命令，例如复制文件和目录以及登录。这种功能-



……性持续增加，直到你处理存储在网络上任意系统上的文件，且通过**网络文件系统 (NFS)**，你对这些文件的访问对你来说是透明的。

让我们来看看 UNIX 网络的一些基础知识。

#### IEEE 802.3 和 TCP/IP 概述

为了理解 UNIX 系统上的网络是如何工作的，你首先需要理解存在于 UNIX 系统上的网络组件。UNIX 系统上存在七层网络功能，如图 13-2 所示。我将简要介绍底部四层，以便你了解每一层如何参与网络的运行，从而在你配置和排除 UNIX 系统网络故障时更加知情。大多数 UNIX 系统管理员花在顶层的时间最多，因为顶层最接近你可以理解的功能。然而，底部几层在某些层面上也很重要，这样你就可以执行必要的配置来改进系统的网络性能，这对系统的整体性能有重大影响。

| 层号 | 层名称 | 数据形式 | 注释 |
| :--- | :--- | :--- | :--- |
| 7 | 应用层 | | 用户应用程序位于此层。 |
| 6 | 表示层 | | 应用程序准备。 |
| 5 | 会话层 | | 应用程序准备。 |
| 4 | 传输层 | 数据包 (Packet) | 由 **TCP** 处理的端口到端口的传输。 |
| 3 | 网络层 | 数据报 (Datagram) | **互联网协议 (IP)** 通过直接前往目的地或默认路由器来处理路由。 |
| 2 | 链路层 | 帧 (Frame) | 数据封装在 **Ethernet** 或 **IEEE 802.3** 中，带有源地址和目的地址。 |
| 1 | 物理层 | | 系统间的物理连接。通常是细缆线或双绞线。 |

![](img/eff8b9287a5f38c5adf538f24aacf29e_863_0.png)

我从底部开始审查图 13-2，从第 1 层开始，然后描述底部四层的每一层。这是**国际标准化组织开放系统互连 (ISO/OSI)** 模型。可视化网络层相互作用的方式是很有帮助的。

### 物理层

起点是网络上系统之间的物理互连。如果没有**物理层**，你无法在系统之间通信，你想要实现的所有强大功能都不可能实现。物理层将你想要传输的数据转换为沿导线传输的模拟信号（目前我将假设你现有的任何物理层都使用导线）。进入网络接口的信息从导线上剥离，并准备供下一层使用。

### 链路层

为了连接到本地系统中的其他系统，你使用链路层，该层能够建立与你本地段上所有其他系统的连接。这是你拥有 **IEEE 802.3** 或 **Ethernet** 的层。你的 UNIX 系统支持这两种“封装”方法。之所以称为封装，是因为你的数据被放入这两种形式之一（**IEEE 802.3** 或 **Ethernet**）。数据在链路层中以帧（数据的一种别名）传输，并附带源地址、目的地址和一些其他信息。你可能认为，由于存在两种不同的封装方法，它们必须非常不同。然而，这种假设并不成立。**IEEE 802.3** 和 **Ethernet** 几乎相同。因此，许多 UNIX 系统可以处理这两种类型的封装。所以，通过底部两层，你的系统之间有物理连接，数据被封装成两种格式之一，并附带源地址和目的地址。图 13-3 列出了**以太网**封装的组件，并在适当的地方对 **IEEE 802.3** 封装进行了注释：

| 组件 | 大小 | 描述 |
| :--- | :--- | :--- |
| 目的地址 | 6 字节 | 数据发送到的地址 |
| 源地址 | 6 字节 | 数据发送自的地址 |
| 类型 | 2 字节 | 这是 802.3 中的“长度计数” |
| 数据 | 46–1500 字节 | 802.3 为 38–1492 字节；这两种数据大小（**MTU**）的差异可以通过 **ifconfig** 命令看到 |
| 循环冗余校验 (CRC) | 4 字节 | 用于检测错误的校验和 |

![](img/eff8b9287a5f38c5adf538f24aacf29e_864_0.png)

有一个有趣的细节需要注意，即 **IEEE 802.3** 和 **以太网** 最大数据大小之间的差异，分别为 1492 和 1500 字节。这就是最大传输单元（**MTU**）。稍后将介绍的 **ifconfig** 命令显示了你的接口的 **MTU**。以太网中的数据称为*帧*（在上一层重新封装数据在 IP 中称为*数据报*，在再上一层封装在 TCP 中称为*数据包*）。

请记住，以太网和 IEEE 802.3 可以在相同的物理连接上运行，但两种封装方法确实存在差异。在你的 UNIX 系统中，你不需要花费多少（如果有的话）时间来设置网络接口进行封装。

### 网络层

接下来我们上升到第三层，即网络层。在 UNIX 系统上，这一层与**互联网协议 (IP)** 是同义词。此层的数据以*数据报*形式传输。这是处理网络中数据路由的层。使用 IP 路由的数据有时会遇到某种错误，这通过**互联网控制消息协议 (ICMP)** 消息报告回源系统。我们稍后会看到一些 ICMP 消息。**ifconfig** 和 **netstat** 是两个常用于配置此路由的 UNIX 命令。

不幸的是，IP 使用的信息不能方便地装入以太网帧中，因此你会得到碎片化的数据。这实际上是数据的重新封装，因此当你向上移动各层时，会出现很多低效性。

IP 以简单的方式处理路由。如果数据发送到直接连接到你的系统目的地，那么数据直接发送到该系统。如果目的地没有直接连接到你的系统，数据则发送到默认路由器。默认路由器随后负责将数据传递到其目的地。这种路由可能有点难理解，所以我稍后会详细介绍。

### 传输层

*传输层*是网络层之上的下一层。它与*端口*通信。**TCP** 是在此层找到的最常见协议，它形成从端口到端口发送的数据包。程序使用的端口通常定义在 */etc/services* 中，连同协议（如 **TCP**）。这些端口被网络程序使用，例如 **telnet**、**rlogin**、**ftp** 等。你可以看到，这些与端口相关的程序是我们分析层图时覆盖的最高层。

#### 互联网协议 (IP) 寻址

互联网协议地址（IP 地址）要么是 A 类、B 类或 C 类地址（还有 D 类和 E 类地址，这里不涵盖）。A 类网络支持的每网络节点数远多于 B 类或 C 类网络。IP 地址由四个字段组成。将 IP 地址分解为四个字段的目的是定义节点（或主机）地址和网络地址。图 13-4 总结了类别和地址之间的关系。

| 地址类别 | 网络数量 | 每网络节点数 | 定义网络的位数 | 定义每网络节点数的位数 |
| :--- | :--- | :--- | :--- | :--- |
| A | 少数 | 最多 | 8 位 | 24 位 |
| B | 许多 | 许多 | 16 位 | 16 位 |
| C | 最多 | 少数 | 24 位 | 8 位 |
| 保留 | - | - | - | - |

**图 13-4 互联网协议 (IP) 地址比较**

这些位模式意义重大，因为位数定义了每个类别中网络和节点的范围。例如，A 类地址使用 8 位来定义网络，而 C 类地址使用 24 位来定义网络。因此，A 类地址支持的网络少于 C 类地址。然而，A 类地址每网络支持的节点数远多于 C 类地址。将这些关系更进一步，我们现在可以在图 13-5 中看到与这些地址类别相关的具体参数。

**图 13-5 地址类别**

| 地址类别 | 支持的网络数 | 每网络节点数 | 地址范围 |
| :--- | :--- | :--- | :--- |
| A | 127 | 16777215 | 0.0.0.1 - 127.255.255.254 |
| B | 16533 | 65535 | 128.0.0.1 - 191.255.255.254 |
| C | 2097157 | 255 | 192.0.0.1 - 223.255.254.254 |
| 保留 | - | - | 224.0.0.1 - 255.255.255.255 |

查看二进制形式的 32 位地址，你可以看到如何确定地址的类别：




## 图 13-5 地址类别（续）

![](img/eff8b9287a5f38c5adf538f24aacf29e_867_0.png)

A 类地址的最高位设为 0。你可以看到，由于所有位都用于节点或主机地址，因此单个网络可以支持如此多的节点。A 类地址的第一位是 0，网络部分剩余的 7 位用于定义网络。然后，总共 3 个字节用于定义网络内的节点。

![](img/eff8b9287a5f38c5adf538f24aacf29e_867_1.png)

B 类地址的最高位设为 1，次高位设为 0。与 A 类地址相比，这里支持更多的网络，但每个网络的节点数较少。在 B 类地址中，2 个字节用于地址的网络部分，2 个字节用于地址的节点部分。

![](img/eff8b9287a5f38c5adf538f24aacf29e_868_0.png)

C 类地址的最高位和次高位均设为 1，第三位为 0。C 类地址支持最多的网络数量，但每个网络的节点数最少。在 C 类地址中，3 个字节用于网络部分，1 个字节用于网络内的节点部分。

这些地址用于各种设置文件中，这些文件将在后面描述 /etc/hosts 文件时进行介绍。你网络中的每个接口必须具有唯一的 IP 地址。拥有两个网络接口的系统必须有两个唯一的 IP 地址。

#### 子网掩码

你的 UNIX 系统使用子网掩码来确定 IP 数据报是发往其自身子网上的主机、同一网络上但不同子网的主机，还是不同网络上的主机。通过划分子网，你可以让一些主机位于一个子网，而其他主机位于另一个子网。子网之间可以通过路由器或其他连接子网的网络电子元件进行隔离。

为了执行路由，路由器使用的地址中仅包括网络（net）和子网（subnet）部分。子网掩码用于屏蔽地址中的主机部分。由于你可以设置网络地址的方式使得只有你知道地址的哪部分是主机、哪部分是子网、哪部分是网络，因此你使用子网掩码来让系统识别 IP 地址中哪些位是用于主机的，哪些是用于子网的。

就其最简单的形式而言，使用子网掩码实际上是在指定 IP 地址中哪一部分定义主机，哪一部分定义网络。使用子网掩码时最令人困惑的一个方面是，大多数书籍将图 13-6 中的子网掩码显示为最常见的情况。

| 地址类别 | 十进制 | 十六进制 |
|---|---|---|
| A | 255.0.0.0 | 0xff000000 |
| B | 255.255.0.0 | 0xffff0000 |
| C | 255.255.255.0 | 0xffffff00 |

图 13-6 子网掩码

然而，这种思维方式假设你将尽可能多的位分配给网络，将尽可能多的位分配给主机，并且不使用子网。图 13-7 展示了使用 B 类地址进行子网划分的示例。

| 地址类别 | B 类 |
|---|---|
| 主机 IP 地址 | 152.128. 12. 1 |
| 分解 | 网络 | 子网 | 主机 ID |
| 位数 | 16 位 | 8 位 | 8 位 |
| 子网掩码（十进制） | 255.255. 255. 0 |
| 子网掩码（十六进制） | 0xfffff00 |
| 同一子网上不同主机的示例 | 152.128. 12. 2 |
| 不同子网上主机的示例 | 152.128. 13. 1 |

图 13-7 B 类 IP 地址和子网掩码示例

在图 13-7 中，子网掩码的前两个字节（255.255）定义网络，第三个字节（255）定义子网，第四个字节（0）用于主机 ID。虽然该 B 类地址的子网掩码未出现在之前提到的默认子网掩码图中，但 255.255.255.0 的子网掩码在 B 类网络中广泛使用以支持子网划分。

你的 UNIX 系统如何使用 255.255.255.0 的子网掩码执行比较，以确定 152.128.12.1 和 152.128.13.1 位于不同的子网？图 13-8 展示了这种比较。

![](img/eff8b9287a5f38c5adf538f24aacf29e_870_0.png)

图 13-8 使用子网掩码比较地址的示例

图 13-9 展示了这两个位于不同子网中的系统：

![](img/eff8b9287a5f38c5adf538f24aacf29e_871_0.png)

你不必使用 8 位边界来划分网络、子网和主机 ID 字段。例如，如果你希望将子网字段的一部分用于主机 ID，你可以这样做。这种做法的一个良好理由是为了适应未来的扩展性。你可能希望子网 12、13、14 和 15 今天属于同一个子网，并在未来将它们变成独立的子网。图 13-10 展示了这种设置：

![](img/eff8b9287a5f38c5adf538f24aacf29e_872_0.png)

这些系统连接到同一个子网，尽管第三字节中通常与子网相关联的一部分被用于主机 ID。在未来，可以将子网掩码更改为 255.255.252.0，从而拥有 12、13、14 和 15 四个独立的子网。这种安排需要部署路由器来路由到这些独立的子网。

让我们现在切换到 ISO/OSI 模型的更高层次，看看一些网络功能。

#### 使用网络

ISO/OSI 模型有助于可视化网络层相互作用的方式。然而，该模型并没有告诉你如何使用网络。两个广泛使用且值得查看的网络服务可能正在你的系统上运行，它们是 ARPA 和 NFS。

你要在你的系统上尝试的第一个网络产品通常被称为 ARPA 服务——我将其称为 ARPA。ARPA 是“ARPA Services”和“Berkeley Services”的组合。ARPA 服务支持运行不同操作系统的系统之间的通信，而 Berkeley 服务支持 UNIX 系统。以下部分列出了最常用的 ARPA 和 Berkeley 命令。虽然可以在这些服务中的每一个下运行许多程序，但以下是 UNIX 领域中最常用的程序。在某些情况下，会有示例展示如何使用这些命令。在大多数示例中，本地主机为 **system1**，远程主机为 **system2**。

##### ARPA 服务（不同操作系统系统间的通信）

**文件传输协议 (ftp)**  
将一个或多个文件从一个系统传输到另一个系统。这通常在 UNIX 工作站和 Windows PC、VAX 等之间传输文件时使用。以下示例展示了将文件 /tmp/krsort.c 从 system2（远程主机）复制到 system1（本地主机）上的本地目录：

```
$ **ftp** system2		注释
Connected to system2.		发出 ftp 命令
system2 FTP server (Version 4.1) ready.
Name (system2:root): root		登录到 system2
Password required for root.
Password:		输入密码
User root logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> **cd** /tmp		cd 到 system2 上的 /tmp
CWD command successful
ftp> **get** ksort.c		获取 ksort.c 文件
PORT command successful
Opening BINARY mode data connection for **krsort.c**
Transfer complete.
2896 bytes received in 0.08 seconds
ftp> **bye**		退出 ftp
Goodbye.
$
```

在这个示例中，两个系统都运行 UNIX；然而，你通过 **ftp** 发出的命令是与操作系统无关的。上面使用的 **cd**（更改目录）和 **get** 命令适用于任何运行 **ftp** 的操作系统。如果你熟悉几个 **ftp** 命令，你可能会发现在异构网络环境中传输信息并不难。

很可能你正在异构环境中使用你的 UNIX 系统，因此你可能使用 **ftp** 将文件和目录从一个系统复制到另一个系统。由于 **ftp** 使用非常广泛，我将描述一些常用的 **ftp** 命令：

- **ascii**
  - 将传输的文件类型设置为 ASCII。这意味着你正在将一个 ASCII 文件从一个系统传输到另一个系统。这通常是默认设置，因此你不需要设置它。
  - 示例：**ascii**

- **binary**
  - 将传输的文件类型设置为二进制。这意味着你正在将一个二进制文件从一个系统传输到另一个系统。例如，如果你希望在 UNIX 系统上拥有一个存放应用程序的目录，并将这些应用程序复制到非 UNIX 系统，那么你需要使用二进制传输。
  - 示例：**binary**

- **cd**
  - 更改到远程主机上的指定目录。
  - 示例：**cd /tmp**





## dir

将远程系统上目录的内容列出到屏幕，或者如果你指定了本地文件名，则列到本地系统的文件中。

## get

将指定的远程文件复制到指定的本地文件。如果你没有指定本地文件名，则将使用远程文件名。

## lcd

更改到本地主机上的指定目录。
示例：**lcd /tmp**

## ls

将远程系统上目录的内容列出到屏幕，或者如果你指定了本地文件名，则列到本地系统的文件中。

## mget

从远程主机复制多个文件到本地主机。
示例：**mget *.c**

## put

将指定的本地文件复制到指定的远程文件。如果你没有指定远程文件名，则将使用本地文件名。
示例：**put test.c**

## mput

从本地主机复制多个文件到远程主机。
示例：**mput *.c**

## bye/quit

关闭到远程主机的连接。
示例：**bye**

除了这里介绍的内容，还有其他可用的 **ftp** 命令。如果你需要关于这些命令的更多信息，或者希望查看其他 **ftp** 命令，UNIX 手册中关于 **ftp** 的页面很有帮助。

## telnet

用于使用 telnet 协议与其他主机进行通信。Telnet 是使用 **rlogin** 的一种替代方法，将在后文介绍。以下示例展示了如何建立与远程主机 system2 的 telnet 连接：

| 命令/输出 | 注释 |
| :--- | :--- |
| $ telnet system2 | Telnet 连接到 system2 |
| Connected to system2. AIX version 4 system2 | |
| login: **root**<br/>password: | 以 root 身份登录到 system2<br/>输入密码 |
| Welcome to system2. - rs6000 aix 4.3.1.0 | |
| $ | system2 上的 AIX 提示符 |

## Berkeley 命令 (*UNIX 系统间的通信*)

###### 远程复制 (rcp)

此程序用于在两个 UNIX 系统之间复制文件和目录。要从 system1 将 /tmp/krsort.c 复制到 system2，你可以执行以下操作：

```
$ rcp system2:/tmp/krsort.c /tmp/krsort.c
```

需要对文件进行一些网络配置才能实现这种级别的功能。在本例中，发出该命令的用户在两个系统中都被视为“等效”用户，并且拥有权限使用 rcp 将文件从一个系统复制到另一个系统（这些术语稍后会描述）。

###### 远程登录 (rlogin)

支持登录到远程 UNIX 系统。要从 system1 远程登录到 system2，你需要执行以下操作：

```
$ rlogin system2
password:
Welcome to system2
$
```

如果用户发出 rlogin 命令时要求输入密码，则用户在两个系统中不是等效的。如果未要求输入密码，则用户确实是等效的。你还可以发出 rlogin system1-user 命令，将系统和用户作为命令的一部分指定。

###### 远程 shell (remsh)

使用 remsh 命令，你可以坐在一个 UNIX 系统上，发出一个要在另一个不同的 UNIX 系统上远程运行的命令，并在本地显示结果。在这种情况下，发出一个 remsh 命令以显示 /tmp/krsort.c 的长列表。命令在 system2 上运行，但结果在输入命令的 system1 上显示：

```
$ remsh system2 ll /tmp/krsort.c
-rw-rw-rw- 1 root sys 2896 Sept 1 10:54 /tmp/krsort.c
$ 
```

在这种情况下，system1 和 system2 上的用户必须是等效的，否则将拒绝执行此命令。

### 远程 who (*rwho*)

查找谁登录在远程 UNIX 系统上。以下是发出 **rwho** 的输出：

```
$ rwho
root system1:ttyu0 Sept 1 19:21
root system2:console Sept 1 13:17
tomd system2:tty22 Sept 1 13:05
```

*   用户名
*   机器名
*   终端行
*   登录日期
*   登录时间

要使 **rwho** 正常工作，必须运行 **rwho** 守护进程 (**rwhod**)。
除了这里介绍的之外，还有其他“r”命令可用。此外，从一个 UNIX 变体到另一个变体，这些命令会有所不同，因此你可能无法在 UNIX 系统上运行完全相同的“r”命令。

#### 主机名映射

与网络相关的最重要决策是在你的 ARPA 系统上如何实现主机名映射。可用于主机名映射的技术有三种：

-   Berkeley 互联网命名域 (BIND)
-   网络信息服务 (NIS)
-   UNIX 文件 /etc/hosts

实现主机名映射最常见且最简单的方法是 /etc/hosts，因此我在下一节中介绍这种技术。请记住，针对你的 UNIX 变体的网络手册可能涵盖了众多网络主题，包括 NFS、ARPA 等。如果你需要了解这里未涵盖的更多网络知识，这些手册是很好的参考资料。

使用 /etc/hosts 文件，正如你即将看到的，在部署了许多系统的环境中变得非常困难。使用这种解决方案，必须保持最新的单个 /etc/hosts 文件，并将其传播到所有其他系统。

域名系统 (DNS) 在大型环境中被广泛使用。DNS 使用 Berkeley 互联网命名域服务 (BIND) 将名称解析为地址。有名称服务器填充对名称数据的请求。这是 BIND 的服务端。BIND 还有一个客户端，称为解析器，它访问名称服务器来解析名称。使用这种客户端/服务器模型，维护命名信息变得更加容易，因为它只需要保存在少数几个地方，而不是保存在每个系统上。

客户端使用名为 /etc/resolv.conf 的文件来配置解析器。名称服务器及其对应的地址是解析信息的关键。

这种解决方案使在大型环境中维护系统名称和地址变得更加容易。DNS 和 BIND 主要是一个系统管理设置过程。从用户的角度来看，你不需要了解太多关于它们的内容。相反，我将在接下来的部分中关注一些用户更感兴趣的程序。我将提供一些背景知识，以便程序的使用方式更有意义。不过，总的来说，我将专注于这些网络主题的用户方面，而不是系统管理方面。

##### /etc/hosts

此文件包含有关你连接的其他系统的信息。它包含每个系统的互联网地址、系统名称以及系统名称的任何别名。如果修改 /etc/hosts 文件以包含网络中系统的名称，它们就为登录到另一个系统提供了基础。虽然你现在可以登录到其他 UNIX 系统，但你尚不能 rcp 或 remsh 到另一个系统。虽然添加 remsh 和 rcp 功能很容易，但这确实会损害安全性，因此并不总是在所有系统上设置。以下是 /etc/hosts 文件的示例：

```
127.0.0.1	localhost	loopback
15.32.199.42	a4410827	
15.32.199.28	a4410tu8	
15.32.199.7	a4410922	
15.32.199.21	a44410tu1	
15.32.199.22	a4410tu2	
15.32.199.62	a4410730	
15.32.199.63	hpxterm1	
15.32.199.64	a4410rd1	
15.32.199.62	a4410750	hp1
```

此文件采用以下格式：

```
<互联网地址>          <官方主机名>  <别名>
```

互联网协议地址 (IP 地址) 是“A”类、“B”类或“C”类地址。“A”类网络比“B”类或“C”类网络支持更多的每个网络节点。将 IP 地址分解为四个字段的目的是定义节点（或主机）地址和网络地址。图 9-3 到 9-6 详细描述了这些类。

假设上述 /etc/hosts 文件包含“C”类地址，最右边的字段是主机或节点地址，其他三个字段组成网络地址。

在发出前面描述的 ARPA 或 Berkeley 命令之一时，你可以使用 /etc/hosts 文件中的官方主机名或别名。例如，以下任意一个 ARPA 命令都可以工作：

```
$ telnet a4410750
```

或者

```
$ telnet hp1
```

类似地，以下任意一个 Berkeley 命令都可以工作：

```
$ rlogin a4410750
```

或者

```
$ rlogin hp1
```

##### /etc/hosts.equiv

你的系统可能已设置为用户 **rlogin** 到远程系统时无需输入密码。他们可以通过编辑此文件来设置等效主机。正如我前面提到的，这种技术有时被认为是一种安全风险，因此并不总是使用。对于 /etc/hosts.equiv 允许用户绕过输入密码，登录名称必须在本地和远程系统上相同。你可以在 /etc/hosts.equiv 中列出所有等效主机，或者列出希望等效的主机和用户名。现在用户可以使用 **rcp** 和 **remsh**，因为他们在这些系统中是等效用户。我通常只是输入网络上的所有主机名。以下是 /etc/hosts.equiv 的示例：

```
a4410730
a4410tu1
a4410tu2
hpnterm1
a4410827
a4410750
```

请记住使用 /etc/hosts.equiv 的潜在安全风险。如果用户可以登录到远程系统而无需密码，你降低了整个网络的整体安全级别。尽管



用户可能会发现，在登录远程系统时不需要输入密码非常方便。你已经为 `/etc/hosts.equiv` 中的所有用户授予了整个网络的访问权限。如果你能确保所有系统上所有文件和目录的权限都设置得当，那么你就不会在意谁有权访问哪个系统。然而，在现实的 UNIX 世界中，权限有时并不符合预期。用户有很强的“四处浏览”的倾向，常常会发现一些他们想要复制的文件，但实际上他们并不应该拥有访问权限。

##### /.rhosts

此文件是超级用户的 `/etc/hosts.equiv`。如果你以 root 身份登录，你希望此文件包含与 `/etc/hosts.equiv` 完全相同的信息。然而，如果你这样做，就会通过允许任何系统上的超级用户无需 root 密码即可登录远程系统，从而增加你的网络安全风险。如果你是你网络中无可争议的管理者，并且 100% 确定不存在任何安全漏洞，那么你可能希望设置 `/.rhosts`，以便在远程以超级用户身份登录系统时无需输入密码。然而，从安全角度来看，你应该知道这种设置是不被推荐的。

如果对 `/etc/hosts`、`/etc/hosts.equiv` 和 `/.rhosts` 中的相应条目进行了适当的修改，你可以使用 ARPA 服务命令 `ftp` 和 `telnet`，以及 Berkeley 命令 `rcp`、`rologin`、`rmesh` 和 `rwho`。

我描述了设置适当文件以启动和运行最常用 ARPA 服务的过程。有时甚至需要更高级的功能，例如 DNS/BIND。你的系统可能已设置 DNS/BIND 或类似功能，使你能够访问本节中涵盖的部分或所有命令。

##### 网络文件系统（NFS）

NFS 允许你挂载远程系统上的磁盘，使其看起来像是你系统的本地磁盘。同样，NFS 允许远程系统挂载你的本地磁盘，使其看起来像是远程系统的本地磁盘。配置 NFS 以实现此功能非常简单。以下是配置 NFS 的步骤：

1. 启动 NFS。
2. 指定你的系统是 NFS 客户端、NFS 服务器，还是两者兼有。
3. 指定哪些本地文件系统可以被远程系统挂载。
4. 指定你想要挂载并视为你系统本地磁盘的远程磁盘。

与 ARPA 一样，你可以启用 NFS 的其他方面，但同样，我介绍的是几乎每个 UNIX 安装都使用的 NFS 功能。

由于 NFS 可能在你的系统上设置为满足众多用户的需求，你可能需要了解与 NFS 相关的术语。以下是常用的 NFS 术语：

| 术语 | 描述 |
| :----- | :----- |
| 节点（Node） | 连接到计算机网络或作为其一部分的计算机系统。 |
| 客户端（Client） | 向其他节点（服务器）请求数据或服务的节点。 |
| 服务器（Server） | 向网络上的其他节点（客户端）提供数据或服务的节点。 |
| 文件系统（File System） | 磁盘分区或逻辑卷。 |
| 导出（Export） | 使文件系统可通过 NFS 在远程节点上挂载。 |
| 挂载（Mount） | 使用 NFS 访问远程文件系统。 |
| 挂载点（Mount Point） | 挂载 NFS 文件系统的目录名称。 |
| 导入（Import） | 挂载远程文件系统。 |

某些具体的配置任务和相关文件在不同 UNIX 变体之间有所不同。以下是一些与配置 NFS 相关的通用任务示例。当然，你的系统管理员必须处理不同 UNIX 变体上配置的具体细节。

你的系统必须是 NFS 客户端、NFS 服务器或两者兼有。此外，必须有守护进程正在运行以支持 NFS。这两种任务在不同 UNIX 变体中的执行方式略有不同。

然后，你的系统导入你拥有本地访问权限的远程文件系统，并导出被其他系统访问的本地文件系统。

你在本地挂载的远程文件系统在 `/etc/fstab`、`/etc/vfstab`、`/etc/filesystems` 或用于挂载文件系统的任何文件中都有一个类似以下内容的条目：

```
system2:/opt/app3    /opt/app3    nfs    rw,suid    0 0
```

在这种情况下，我们将 `system2` 上的 `/opt/app3` 本地挂载为 `/opt/app3`。这是一个带有所示权限的 NFS 挂载。

你可以使用 `showmount` 命令显示所有已挂载本地文件系统的远程系统（客户端）。大多数 UNIX 变体都支持此命令。`showmount` 对于确定客户端最经常使用 NFS 挂载的文件系统非常有用。`showmount` 的输出特别易于阅读，因为它列出了客户端挂载的主机名和目录。`showmount` 命令有以下三个选项：

- `-a` 以“名称:目录”格式打印输出
- `-d` 列出被客户端远程挂载的所有本地目录
- `-e` 打印导出文件系统的列表

#### 在 HP-UX 11.0 和 11i 上使用 BIND 8.1.2 设置 DNS 服务器

本程序记录了如何在 HP-UX 11.0/11i 平台上使用最新支持的 BIND 版本 8.1.2 设置主（Primary）、从（Slave）和仅缓存 DNS 服务器。BIND 8.1.2 在 11.0 上通过 http://software.hp.com 的补丁加载，并在 11i 发布媒体中提供。关于 BIND 8.1.2 的更详细讨论，请参阅 Albitz 和 Liu 所著的 O'Reilly 和 Associates 第三版书籍 *DNS and BIND*。BIND 8.1.2 仅在 11.0/11i 平台上可用，而在 10.20 上不可用。10.20 使用旧版 4.9.7 版本。重要的是要知道，旧版 BIND 4.9.X 具有不同的配置文件（boot 文件）格式。还有一些术语差异。“boot” 文件现在被称为 “config” 或 “conf” 文件。HP 主名称服务器现在称为主名称服务器；次要名称服务器现在称为从服务器。

在大多数情况下，DNS 实施相当直接，即资源记录、数据库文件等。真正的考验在于规划。必须考虑诸如 DNS 系统是否受防火墙保护、是否希望你的解析器在 Internet 上进行“对等”连接，以及 `nslookup` 远程域和地址等问题。一些管理员选择关闭对 Internet 的访问以减少由此产生的网络流量。如果你直接连接到 Internet，你需要向授权 Internet 域名服务提供商注册至少两个名称服务器。这些提供商的列表可在 http://www.icann.org/registrar/accredited-list.html 找到。如果你没有直接连接，即位于防火墙后面，ISP 是 DNS 服务的良好选择，并将为你完成大部分工作。

完成规划后，你需要配置 DNS 服务器。你应该使用哪些名称？有些人使用名称、位置参考，有时人们使用名称作为网络计算机和打印机的名称。决定权在于你，但不要在主机名中使用下划线（参见 “check-names” boot 文件选项），并使名称易于记忆。以下是为你的网络创建主（Primary）DNS 服务器的步骤：

1. 在 `/etc/hosts` 中填入你想要管理的所有主机，按网段和域分隔，并以有序的方式保留所有内容，以便诸如 `hosts_to_named` 之类的工具可以安全高效地为你管理数据库文件，如下例所示：

```
/etc/hosts
15.17.186.159 wtec712-rtx

127.0.0.1 localhost loopback
# 812 无效域 BASEBALL.HP.COM

# NL~ 东区
10.1.1.1 atlantabraves.baseball.hp.com
10.1.1.2 newyorkmets.baseball.hp.com
# NL- 中区
10.1.2.1 houstonastros.baseball.hp.com
10.1.2.2 chicagocubs.baseball.hp.com
10.1.2.3 stlouiscardinals.baseball.hp.com
```

2. 为你的域创建一个包含 `param` 文件的参数，如下例所示，用于 `/tmp/param`：

```
/tmp/param
-d baseball.hp.com <---------- 你的域。
-n 10.1.1
-n 10.1.2
-n 10.1.3
-n 15.17.186
-H /etc/hosts.dnctest <---------- 你将使用的 hosts 文件。
-r <---------- 如果此名称服务器是
根 NS。我们下面的例子
不是针对根 NS。
```

3. 在你想放置数据库的目录中运行带有新建 `param` 文件的 `hosts_to_named`。注意 `param` 文件并非必要，但这是一个好主意；选项可以通过命令行运行而不是包含在文件中。使用 `hosts_to_named` 的另一个常见错误是没有在“干净”目录中运行它。如果你需要在运行前保留结果，请使用 `mkdir /etc/named.data.old; mv /etc/named.data/* /etc/named.data.old` 来保留先前的配置。

```
# cd /etc/named.data
# hosts_to_named -f /tmp/param
```





4. `hosts_to_named` 将同时生成一个 BIND 4.X 的 `named.boot` 文件和一个 BIND 8.X 的 `named.conf` 文件。请将 `/etc/named.data` 中创建的数据库文件与 `/etc/named.data/named.conf` 中找到的文件进行匹配。以下是一个非根域名服务器的示例：

```
// generated by named-bootconf.pl

options {
    check-names response fail;    // do not change this
    check-names slave warn;
    directory "/etc/named.data"; // running directory for named
    /*
     * If there is a firewall between you and nameservers you want
     * to talk to, you might need to uncomment the query-source
     * directive below.  Previous versions of BIND always asked
     * questions using port 53, but BIND 8.1 uses an unprivileged
     * port by default.
     */
    // query-source address * port 53;

    // type domain source file
    //

    zone "0.0.127.IN-ADDR.ARPA" {
        type master;
        file "db.127.0.0";
    };

    zone "baseball.hp.com" {
        type master;
        file "db.baseball";
    };

    zone "1.1.10.IN-ADDR.ARPA" {
        type master;
        file "db.10.1.1";
    };

    zone "2.1.10.IN-ADDR.ARPA" {
        type master;
        file "db.10.1.2";
    };

    zone "3.1.10.IN-ADDR.ARPA" {
        type master;
        file "db.10.1.3";
    };

    zone "186.17.15.IN-ADDR.ARPA" {
        type master;
        file "db.15.17.186";
    };

    zone "." {
        type hint;
        file "db.cache";
    };

    (wtec712-rtr)named.data-1s

    boot.cacheonly db.10.1.2 db.15.17.186 named.boot
    conf.cacheonly db.10.1.3 db.baseball named.conf
    db.10.1.1 db.127.0.0 db.cache params-file
```

如图所示，**hosts_to_named** 创建了带有单个父域名 **baseball.hp.com** 的反向查找（从 IP 地址到名称）数据库文件。我们网络中的每个节点都将拥有全限定名称 **shortname.baseball.hp.com**。

5. 由于许多安装环境仍然在主机名中使用下划线，我们强烈建议通过修改 **hosts_to_named** 生成的 **named.conf** 文件中的 *check-names* 选项列表来允许这种情况。例如，您可能需要更改以下行：

```
options {
    check-names response fail   // do not change this
    check-names slave warn
    .
    .
    .
```

为：

```
options {
    check-names response ignore   //change "fail" to "ignore"
    check-names slave ignore      //change "warn" to "ignore"
    check-names master ignore     //add this whole new line
    .
    .
    .
```

6. 用根域名服务器的地址填充 db.cache。如果您直接连接到互联网并查询 NIC 的根域名服务器，请从站点 ftp://internic.net/domain/named.cache 获取更新的列表。

下载后，将文件复制到 db.cache。如果您没有直接连接到互联网，必须通过防火墙查询根域名服务器，请将防火墙配置为您的根域名服务器，并以指定根域名服务器相同的方式将您的 db.cache 条目指向防火墙。正确配置 db.cache 非常重要，否则会影响邮件和名称解析等服务。以下是其中一个示例：

```
; FILL IN THE NAMES AND ADDRESSES OF THE ROOT SERVERS
;
; . 99999999 IN NS root.server.
;
; root.server. 99999999 IN A ??.?? .?? . ??
;
; 99999999 IN NS firewall.baseball.hp.com.
firewall.baseball.hp.com. 99999999 IN A 15.17.186.99
```

在这种情况下，firewall.baseball.hp.com. 是我的防火墙，由于我的域名服务器无法直接查询根域名服务器，db.cache 被导向我的防火墙。

7. 如果您打算拥有一个不会以任何方式与互联网通信的主（主）域名服务器，则需要通过执行几项操作将您的域名服务器设置为根域名服务器。或者使用您的 **params** 文件中的 *-r* 选项配合 **hosts_to_named**，或者进行以下更改：

在您的 **named.conf** 文件中，将：

```
zone "." {
    type hint;
    file "db.cache";
}
```

更改为：

```
zone "." {
    type master;
    file "db.root";
}
```

根域名服务器数据库文件 **db.root** 将包含以下内容：

```
. IN SOA m3107ced.baseball.hp.com. root.m3107ced.baseball.hp.com.
{
    ; Serial
    10800 ; Refresh every 3 hours
    3600 ; Retry every hour
    604800 ; Expire after a week
    86400 ; Minimum ttl of 1 day
}
IN NS m3107ced.baseball.hp.com.
m3107ced.baseball.hp.com. IN A 15.50.73.92
```

我们做的是设置了一个内部根域名服务器。**db.root** 包含一条记录：**m3107ced.baseball.hp.com**。

8. 下一个需要考虑的问题是将非权威域名的查询发送到哪里。如果您的域名是 **baseball.hp.com**，而有人请求 **jughhead.ibm.com**，会发生什么？如果您配置了一个没有转发器语句的根域名服务器，答案是什么也不会发生。查询将因找不到主机而失败。如果您不希望内部系统查询互联网域名，这通常是件好事。安全和网络拥塞通常是原因。但是，如果您希望解析互联网名称和地址怎么办？很简单，在您的 */etc/named.conf* 中配置转发器语句，指向防火墙或直接与根域名服务器通信的系统，如以下示例所示：

```
options {
    check-names response ignore;    // change fail to ignore
    check-names slave ignore;       // change warn to ignore
    check-names master ignore;      // add this line
}

forwarders 15.253.24.10 15.253.32.10 15.253.24.10 15.253.32.10
directory "/etc/named.data"; // running directory for named

/**
 * If there is a firewall between you and nameservers you want
 * to talk to, you might need to uncomment the query-source
 * directive below.  Previous versions of BIND always asked
 * questions using port 53, but BIND 8.1 uses an unprivileged
 * port by default.
 */
// query-source address * port 53;
**/;
```

这里发生的情况是，对于我们没有权限的域名（基本上是 **baseball.hp.com** 以外的任何东西），我们将查询发送给转发器，让它们来处理。如图所示，有两个转发器，每个都列出了两次。这样做的原因是转发器通常很忙，指定两个可以防止查询超时。请务必将 */etc/named.data/named.conf* 复制到 */etc/named.conf*。所有版本的 BIND 默认都会在 */etc/* 中查找启动文件，因此准备好后不要忘记将其复制到 */etc*。

9. 在您的域名服务器以及所有指向该域名服务器的客户端上配置 */etc/resolv.conf* 和 */etc/nsswitch.conf*：

/etc/resolv.conf

```
domain baseball.hp.com
search baseball.hp.com atl.hp.com hp.com rose.hp.com cup.hp.com external.hp.com
nameserver 15.50.73.92 # authoritative name server 4.atl.hp.com
nameserver 15.51.240.8 # non-authoritative cache only servers
```

/etc/resolv.conf 非常简单：domain 语句标识系统所属的域名；search 语句用于在存在多个域名时简化输入。当您发起查询，例如查询 jugshead 时，它会先在 baseball.hp.com 中查找 jugshead，然后是 atl.hp.com、rose.hp.com，最后是 cup.hp.com。/etc/nsswitch.conf 修改了查找主机和 IP 地址时使用的开关顺序。此信息有四种可能的来源：1) /etc/hosts，2) nis，3) nisplus，4) 和 dns。默认情况下，硬编码的顺序是 dns nis files。要修改开关顺序，您需要从 /usr/newconf/etc/nsswitch.hp_defaults 复制一个新的 /etc/nsswitch.conf 文件，并修改 hosts 条目：

```
# /etc/nsswitch.hp_defaults:
#
# An example file that could be copied over to /etc/nsswitch.conf; it
# uses NIS (YP) in conjunction with files.
#
passwd: compat
group: compat

hosts: files [NOTFOUND=return] dns
networks: nis [NOTFOUND=return] files
protocols: nis [NOTFOUND=return] files
rpc: nis [NOTFOUND=return] files
publickey: nis [NOTFOUND=return] files
netgroup: nis [NOTFOUND=return] files
autmount: files nis
```





别名：files nis
服务：nis [NOTFOUND=return] files

如您所见，*hosts* 行已被修改，以便我们首先查询 /etc/hosts 文件，如果查询不成功，则继续转向 *dns*。更改开关顺序的方式有很多种，还有很多其他方法可能会把事情搞乱。更改开关顺序时请谨慎行事，并查阅 *switch* 的手册页以获取更多相关信息。

- 10. 按如下步骤启动 DNS 名称服务器进程：

```
# /usr/sbin/named
# ps -eaf|grep named

root 8074 1 0 08:42 0:08 ? 0:00 /usr/sbin/named <--- 检查以确保它正在运行..
root 8077 8072 2 08:42 0:00 grep named
```

启动名称服务器后，您可以使用 *sig_named* 执行各种功能。修改任何 *db* 文件或 /etc/named.boot 后，您需要告知 named 刷新其数据库。您可以使用以下两个命令中的任意一个来实现：

```
# sig_named restart
# kill -HUP /var/run/named.pid
```

这将重新加载数据库，您可以通过查看 /var/adm/syslog/syslog.log 文件的末尾来验证，如下所示：

```
Oct 12 08:49:13 m3107ced named[8074]: primary zone "0.0.127.IN-ADDR.ARPA" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: primary zone "baseball.hp.com" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: primary zone "1.1.10.IN-ADDR.ARPA" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: primary zone "2.1.10.IN-ADDR.ARPA" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: primary zone "3.1.10.IN-ADDR.ARPA" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: primary zone "1.168.192.IN-ADDR.ARPA" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: primary zone "2.168.192.IN-ADDR.ARPA" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: primary zone "3.168.192.IN-ADDR.ARPA" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: Ready to answer queries.
```

如您所见，named 加载了我们的每个数据库（或区域），并准备就绪以回答查询。

- 11. 测试通过名称和 IP 地址进行的查询。

```
# nslookup atlantabraves
Using /etc/hosts on: wt ec712-rtr
Looking up FILES
Trying DNS
Name: atlantabraves.baseball.hp.com
Address: 10.1.1.1
```

```
# nslookup 10.1.1.1
Using /etc/hosts on: wt ec712-rtr
Looking up FILES
Trying DNS
Name: atlantabraves.baseball.hp.com
Address: 10.1.1.1
```

通过名称和 IP 地址查找 atlantabraves 均成功，通常此时我们就完成了。

我们总是检查 /var/adm/syslog/syslog.log 以查找来自 named 的消息。named 记录了很多看似不重要的聊天内容，但至少值得稍作浏览。

##### 关于从（二级）名称服务器

一旦您创建了主（一级）DNS 服务器，最艰巨的工作就完成了。创建从服务器和仅缓存服务器很简单。让我们一步步 walkthrough 这个过程：

- 1. 使用 **ftp** 从主（一级）服务器复制 named.conf 文件和 **db.cache**。

- 2. 按如下方式编辑 named.conf 文件：
  - 将每个“master”实例更改为“slave”，回环域 db.127.0.0 和缓存条目除外。
  - 为每个区域添加一个“masters”条目，其中包含主 DNS 服务器的 IP 地址。

我们将使用上面的示例：

```
# cat /etc/named.conf
// generated by named-bootconf.pl
options {
    check-names response fail; // do not change this
    check-names slave warn;
    directory "/etc/named.data"; // running directory for named
};
/*
 * If there is a firewall between you and nameservers you want
 * to talk to, you might need to uncomment the query-source
 * directive below.  Previous versions of BIND always asked
 * questions using port 53, but BIND 8.1 uses an unprivileged
 * port by default.
 */
// query-source address * port 53;
//
// type domain source file
//
zone "0.127.IN-ADDR.ARPA" {
    type master;
    file "db.127.0.0";
};

zone "baseball.hp.com" {
    type slave;
    file "db.baseball";
    masters ( 15.17.186.159);
};

zone "1.1.10.IN-ADDR.ARPA" {
    type slave;
    file "db.10.1.1";
    masters ( 15.17.186.159 );
};

zone "2.1.10.IN-ADDR.ARPA" {
    type slave;
    file "db.10.1.2";
    masters ( 15.17.186.159 );
};

zone "3.1.10.IN-ADDR.ARPA" {
    type slave;
    file "db.10.1.3";
    masters ( 15.17.186.159 );
};

zone "186.17.15.IN-ADDR.ARPA" {
    type slave;
    file "db.15.17.186";
    masters ( 15.17.186.159 );
};

zone "" {
    type hint;
    file "db.cache";
};
```

- 3. 现在，一旦您的 named.boot 已复制到 /etc/named.boot 且您的 /etc/named.data 目录已创建，您所需要做的就是启动区域传输。要启动区域传输，您只需要使用以下命令杀死 named：

```
# sig_named restart
```

或

```
# kill -HUP /var/run/named.pid
```

以开始传输。查看 /etc/named.data，您应该会看到所有数据库文件都在那里。此外，检查 /var/adm/syslog/syslog.log，以确保区域正确加载，如下例所示：

```
Oct 12 09:21:34 stimpv named[1893]: secondary zone "1.1.10.IN-ADDR.ARPA" loaded (serial 1)
Oct 12 09:21:35 stimpv named[1893]: secondary zone "baseball.hp.com" loaded (serial 1)
Oct 12 09:21:35 stimpv named[1893]: secondary zone "2.1.10.IN-ADDR.ARPA" loaded (serial 1)
Oct 12 09:21:35 stimpv named[1893]: secondary zone "1.168.192.IN-ADDR.ARPA" loaded (serial 1)
Oct 12 09:21:35 stimpv named[1893]: secondary zone "3.1.10.IN-ADDR.ARPA" loaded (serial 1)
Oct 12 09:21:36 stimpv named[1893]: secondary zone "2.168.192.IN-ADDR.ARPA" loaded (serial 1)
Oct 12 09:21:36 stimpv named[1893]: secondary zone "3.168.192.IN-ADDR.ARPA" loaded (serial 1)
```

注意串行号条目。它们应在主（一级）服务器和从（二级）服务器上保持一致。

##### 关于仅缓存名称服务器

天底下为什么要使用仅缓存的名称服务器？简而言之，为了性能。如果您希望维护本地缓存但不希望管理数据库文件，那么这是正确的方法。它将像其他名称服务器一样工作，以相同的方式响应查询，除了缓存中构建的查询将是非权威的。任何以非权威回复返回的查询都是来自缓存的查询。这是坏事吗？不，但请注意，主（一级）服务器上的数据可能已更改，缓存的回复可能已过时。每个查询的生存时间 (TTL) 标志是操作名称服务器缓存查询答案时间（以秒为单位）的一种方式，而不是必须联系权威名称服务器。记录的默认 TTL 通常为 86400 秒，即 24 小时。根据记录更新的频率，您可能希望调整此值。一个好的经验法则是每个子网至少有一个名称服务器，而仅缓存名称服务器是一个绝佳的选择。

要配置仅缓存名称服务器，请从主（一级）名称服务器复制 `conf.cacheonly` 文件和 `db.cache`。

```
// generated by named-bootconf.pl

options {
    check-names response fail; // do not change this
    check-names slave warn;
    directory "/tmp/testhack"; // running directory for named
};

/* If there is a firewall between you and nameservers you want
 * to talk to, you might need to uncomment the query-source
 * directive below. Previous versions of BIND always asked
 * questions using port 53, but BIND 8.1 uses an unprivileged
 * port by default.
 */

// query-source address * port 53;

zone "0.0.127.IN-ADDR.ARPA" {
    type master;
    file "db.127.0.0";
};

zone "." {
    type hint;
    file "db.cache";
};
```

请记住，不要忘记将您将要缓存数据的名称服务器填入 `db.cache`。

##### 关于名称服务器设置的最后几句话

本节并不提供有关设置 DNS 的全面讨论。最终，它只旨在作为完成所有规划后的食谱。请参阅位于 `http://docs.hp.com` 的书籍《HP 安装和管理互联网服务》。DNS 相当直接，但 `/etc/named.boot` 中的任何语法错误或问题都可能产生戏剧性的后果。当区域未传输或数据存在问题时，`syslog` 可以是您最好的朋友。




#### 其他网络命令和配置

网络配置对于网络管理员和系统管理员来说是一项需要周密规划的工作。没有两个网络环境是完全相同的。通常，您的系统连接着大量的网络设备。有许多有用的命令可用于测试与其他系统的连接性以及进行网络配置。如果您遇到问题，最好了解一些关键的救命网络命令。此外，如果您的 UNIX 系统需要与某些网络硬件（如路由器、网关、网桥等）进行接口，那么在网络设置过程中可能会遇到一些棘手的问题。我将举例说明这种情况：将 UNIX 系统连接到路由器。同时，作为描述的一部分，我会介绍一些最实用的网络命令。

请参见图 13-11，其中显示了一个 UNIX 系统直接连接到路由器。

![](img/eff8b9287a5f38c5adf538f24aacf29e_899_0.png)

这里，一个 UNIX 系统连接到网段 128.185.61。这是一个启用子网划分的 B 类互联网地址。

/etc/hosts 文件需要包含节点 ID 为 2 的 UNIX 系统、路由器以及该网段或路由器另一侧网段上的其他系统。

如果路由器配置正确，我们应该能够无缝地从 61 网段连接到 60、62 和 63 网段上的系统。路由器应配置为允许我们的系统通过路由器连接到其他网段（60、62 和 63）上的系统。为了使这个简单的网络无缝运行，需要一些未预见到的配置。在这种情况下，在尝试让 system1 连接到路由器另一侧 60、62 和 63 网段上的系统时出现了问题。在讨论所需的额外配置之前，我先展示 /etc/hosts 文件，然后使用一些非常有用的 UNIX 命令来显示网络状态。以下是仅显示 UNIX 系统和路由器的 /etc/hosts 文件：

```
$ cat /etc/hosts
127.0.0.1	localhost loopback
128.185.61.1	router1# router
128.185.61.2	system1# UNIX system on 61
128.185.62.1	system2# UNIX system on 62
```

这个 hosts 文件很简单，允许 system1 连接到 router1 和 system2。system1 到 system2 的连接是通过路由器完成的。

##### ping

让我们来看看最常用的一位网络命令 - ping。该命令用于确定两个网络组件之间是否存在连接。ping 是一个简单的命令，每秒向您指定的主机发送一个 ICMP 回声包。您可能会记得，ICMP 之前在网络或第三层部分中已经介绍过。ping 是 Packet InterNet Groper 的缩写。不同的 UNIX 变种在 ping 上没有选项时的报告方式略有不同。

某些系统在没有选项的情况下发出 ping 时提供性能信息；其他系统则报告系统“存活”。以下是检查本地系统与网络上另一台名为 austin 的系统之间连接的示例：

```
martyp $ ping austin
austin is alive
martyp $
```

在大多数 UNIX 变种中，您可以像下面 HP-UX 示例那样调整数据包大小和迭代次数，其中指定数据包大小为 *4096*，间隔为 *5*：

```
# ping 12 4096 5
PING 12: 4096 byte packets
4096 bytes from 10.1.1.12: icmp_seq=0. time=2. ms
4096 bytes from 10.1.1.12: icmp_seq=1. time=2. ms
4096 bytes from 10.1.1.12: icmp_seq=2. time=2. ms
4096 bytes from 10.1.1.12: icmp_seq=3. time=2. ms
4096 bytes from 10.1.1.12: icmp_seq=4. time=2. ms

---12 PING Statistics---
5 packets transmitted, 5 packets received, 0% packet loss
round-trip (ms)  min/avg/max = 2/2/2
#
```

AIX 允许使用 *-I* 指定间隔，以及其他选项，包括数据包大小和迭代次数。以下示例展示了 AIX 系统中的这些选项：

```
martyp $ ping -I 5 austin 4096 10
PING austin: 4096 data bytes
4104 bytes from austin (128.185.61.5): icmp_seq=0. time=8. ms
4104 bytes from austin (128.185.61.5): icmp_seq=1. time=9. ms
4104 bytes from austin (128.185.61.5): icmp_seq=2. time=9. ms
4104 bytes from austin (128.185.61.5): icmp_seq=3. time=9. ms
4104 bytes from austin (128.185.61.5): icmp_seq=4. time=8. ms
4104 bytes from austin (128.185.61.5): icmp_seq=5. time=9. ms
4104 bytes from austin (128.185.61.5): icmp_seq=6. time=9. ms
4104 bytes from austin (128.185.61.5): icmp_seq=7. time=9. ms
4104 bytes from austin (128.185.61.5): icmp_seq=8. time=9. ms
4104 bytes from austin (128.185.61.5): icmp_seq=9. time=9. ms

----austin PING Statistics----

10 packets transmitted, 10 packets received, 0% packet loss
round-trip (ms) min/avg/max = 9/9/15
martyp $
```

在这个示例中，我们每五秒 **ping** 一次 austin，数据包大小为 4096 字节，总共十次。

让我们回到之前的示例。

我如何知道 system1 与路由器以及路由器另一侧的其他系统之间存在连接？我使用 **ping** 命令。以下是我如何知道 system1 已连接到 router1 的方法：

```
$ ping router1
PING router1: 64 byte packets
64 bytes from 128.185.61.2: icmp_seq=0. time=0. ms
64 bytes from 128.185.61.2: icmp_seq=1. time=0. ms
64 bytes from 128.185.61.2: icmp_seq=2. time=0. ms
```

这里的每一行输出代表从被 ping 的设备返回的一个响应。这意味着设备做出了响应。您将无限期地收到此响应，并必须输入 ^c（Ctrl C）来终止 **ping**。如果没有产生输出，如下所示，则未收到响应，您的系统与您正在检查连接的设备之间可能存在问题：

```
$ ping system2
PING router1: 64 byte packets
```

在这种情形下，您会看到这条消息，并且只能到此为止。^c 会终止 **ping**，您会看到发送了若干数据包但未收到任何数据包。我确实在发出 **ping** 命令时得到了此响应，因此我知道 system1 和 router1 之间的连接存在问题。

*ping* 仅应用于测试目的，例如手动故障隔离，因为它会产生大量的网络流量。您不希望持续使用 ping，例如在持续运行的脚本中。

我使用的一个不错的 **ping** 变体是，指定数据包大小为 4096 字节，而不是前几个示例中显示的默认 64 字节，并统计 *ping* 终止前的传输次数，而不必输入 ^c 来终止 **ping**。以下示例展示了这一点：

```
$ ping router1 4096 5
PING router1: 64 byte packets
4096 bytes from 128.185.61.2: icmp_seq=0. time=8. ms
4096 bytes from 128.185.61.2: icmp_seq=1. time=8. ms
4096 bytes from 128.185.61.2: icmp_seq=2. time=9. ms
4096 bytes from 128.185.61.2: icmp_seq=3. time=9. ms
4096 bytes from 128.185.61.2: icmp_seq=4. time=8. ms
```

请注意，传输和接收响应所需的时间（往返时间）比仅传输 64 字节时要长得多。通常我发现 64 字节的往返时间为 0 毫秒，但这取决于多种因素，包括网络拓扑结构和网络流量。

##### netstat

从之前对子网掩码的描述中，您可以看出从一台主机到另一台主机的路由可以通过多种方式配置。信息从一台主机到达另一台主机所经过的路径取决于路由。

您可以使用 **netstat** 命令获取与路由相关的信息。**netstat** 的 **-r** 选项显示路由表，这通常是您想知道的，而 **-n** 选项可用于以数字形式而非名称形式打印网络地址。使用 **-v** 选项，您可以获得与路由相关的其他信息，例如子网掩码。在以下示例中，**netstat** 使用 **-r** 选项（这是在描述 **netstat** 输出时使用的）、**-n** 选项和 **-mv** 选项，以便您可以比较输出：

```
# netstat -r
Routing tables
Dest/Netsmask             Gateway           Flags  Refs     Use    Interface    Metric
0.0.0.0                   0.0.0.0          UH      0  1890555    lo0     4136
0.0.0.0                   0.0.0.0          UH      0     343    lan1    4136
10.1.1.0                  0.0.0.0          U       2       0   lan0    1500
10.1.1.0                  0.0.0.0          U       2       0   lan1    1500
127.0.0.0                 0.0.0.0          U       2       0    lo0     4136
default                    10.1.1.1            UG       0       0   lan1    1500
```

```
# netstat -rn
Routing tables
Dest/Netsmask             Gateway           Flags  Refs     Use    Interface    Metric
127.0.0.1               127.0.0.1          UH      0  1891036    lo0     4136
10.1.1.10                10.1.1.10         UH      0     343   lan1    4136
10.1.1.110               10.1.1.110        UH      0       0   lan0    4136
10.1.1.0                 10.1.1.110        U       2       0   lan0    1500
10.1.1.0                 10.1.1.10         U       2       0   lan1    1500
127.0.0.0                127.0.0.1         U       0       0    lo0     4136
default                    10.1.1.1                UG      0       0   lan1    1500
```

```
# netstat -rnv
Routing tables
Dest/Netsmask             Gateway           Flags  Refs     Use    Interface    Metric
127.0.0.1/255.255.255.255    127.0.0.1      UH      0  1891036    lo0     4136
10.1.1.10/255.255.255.255    10.1.1.10       UH      0     343   lan1    4136
```




第一个和第二个输出表明，我们的系统 o2 有三个接口：第一个是名为 lo0 的本地回环接口。第二个位于 .10，第三个位于 .110（我们可以从 -rn 的输出中看到）。接下来的两行显示，目标地址 10.1.1.10（这是一个网络地址）可以通过 .10 或 .110 处的网卡访问。第三个输出提供了详细信息。最后一行是默认路由。该条目表示，如果找不到更直接的路由，则将数据包发送到 10.1.1.1。

使用 netstat，可以提供一些关于路由器的信息。-r 选项显示有关路由的信息，但该命令还有许多其他有用的选项可用。此输出中特别值得关注的是“Flags”，它定义了发生何种类型的路由。以下是 UNIX 手册页中最常见标志的描述：

- 1=U 通过作为本地主机自身的路由网关到达网络。
- 3=UG 通过作为远程主机的路由网关到达网络。
- 5=UH 通过作为本地主机自身的路由网关到达主机。
- 7=UGH 通过作为主机的远程路由网关到达主机。

此外，我使用 netstat 的两种形式来获取网络统计数据，而不是路由信息。第一种是 netstat -i，它显示自动配置接口的状态。因为我通常最感兴趣的是获取 lan0 的摘要，所以我发出此命令。netstat -i 可以很好地概览 lan0，例如它所在的网络、名称等。

以下示例分别展示了 Solaris 和 HP-UX 系统上 netstat -i 的输出：

```
# netstat -i
Name Mtu Network Address Ipkts Ierrs Opkts Oerrs Coll
n10* 0 none none 0 0 0 0 0
n1* 0 none none 0 0 0 0 0
lo0 4608 loopback 127.0.0.1 232 0 232 0 0
lan0 1500 169.200.112 169.200.112.2 3599766 2 45630 0 104
```

```
# netstat -i
Name Mtu Network Address Ipkts Opkts
lan1 1500 10.1.1.0 c2 59935480 163641547
lan2 1500 10.1.1.0 c2 1383373 12893358
lo0 4136 127.0.0.0 c2 1992333 1892345
#
```

以下是 **netstat** 示例中各字段的说明：

- *Name*：你的网络接口名称（Name），在此例中为 *lan0*。
- *MTU*：“最大传输单元”，即接口卡发送的最大数据包大小。
- *Network*：接口卡所连接的 LAN 的网络地址（169.200）。
- *Address*：你系统的主机名。这是你在文件 */etc/hosts* 中看到的系统的符号名称。

统计信息包括：

- *Ipkts*：接口卡接收的数据包数量，在此例中为 **lan0**。
- *Ierrs*：接口卡检测到的传入数据包错误数量（在某些 UNIX 变体中）。
- *Opkts*：接口卡发送的数据包数量。
- *Errors*：接口卡发送数据包时检测到的错误数量（在某些 UNIX 变体中）。
- *Colls*：由数据包流量导致的冲突数量（在某些 UNIX 变体中）。

**netstat** 提供自节点上次开机以来的累积数据：你可能已经过了很长时间，数据是在此期间累积的。如果你希望看到有用的统计信息，可以使用 **netstat** 配合不同的选项。你还可以指定报告统计数据的间隔。我通常忽略第一个条目，因为它显示了自系统上次开机以来的所有数据。因此，这些数据包括系统空闲的非高峰时段。我更喜欢在系统工作最繁忙时查看数据。以下 **netstat** 示例每五秒提供一次 Solaris 系统上的网络接口信息：

```
# netstat -i lan0 5
(lan0)-> input                 (Total)-> input         output
       packets  errs   packets  errs colls   packets  errs  packets  errs colls
3590505  2  45734    0  104  3590773  2  45946    0  104
134   0  5   0  0 134  0  5  0  0
174   0  0  0  0 174  0  0  0  0
210   0  13  0  0 210  0  13  0  0
169   0  0   0  0 169  0  0  0  0
169   0  0   0  0 169  0  0  0  0
193   0  7   0  0 193  0  7  0  0
261   0  7   0  0 261  0  7  0  0
142   0  8   0  0 142  0  8  0  0
118   0  0   0  0 118  0  0  0  0
143   0  0   0  0 143  0  0  0  0
149   0  0   0  0 149  0  0  0  0
```

通过这个示例，你可以获得 LAN 接口上发生情况的多次输出。如前所述，你可能希望忽略第一个输出，因为它包含很长一段时间的信息。这可能包括你的网络空闲的时间，因此这些数据对你来说并不重要。

以下 **netstat** 示例每五秒提供一次 HP-UX 11i 系统上的网络接口信息：

```
# netstat -i lan0 5
(lan0)-> input               (Total)-> input        output
      packets      packets      packets      packets
     139185      12841621      61980331      378375605
```

| 139185 | 12841714 | 61968172 | 178375698 |
|---|---|---|---|
| 139185 | 12841810 | 61968213 | 178375794 |
| 139185 | 12841877 | 61968247 | 178375861 |
| 139185 | 12841912 | 61968265 | 178375898 |
| 139185 | 12841925 | 61968359 | 178376079 |
| 139187 | 12842244 | 61968413 | 178376240 |
| 139189 | 12842352 | 61968470 | 178376362 |
| 139189 | 12842453 | 61968525 | 178376441 |
| 139190 | 12842482 | 61968565 | 178376498 |
| 139190 | 12842519 | 61968594 | 178376555 |
| 139190 | 12842671 | 61968667 | 178376667 |

你可以使用 **-I interface** 来指定想要报告统计数据的网络接口。在该示例中，使用的是 *-I lo0*。该示例中还使用了五秒的间隔。

netstat 的另一个用途是显示网络套接字的状态。**netstat -a** 生成协议、队列、本地和远程地址以及协议状态的列表。所有这些都有助于显示活动的通信，如下例所示：

```
# netstat -a
Active Internet connections (including servers)
Proto Recv-Q Send-Q Local Address Foreign Address (state)
tcp 0 0 z.system.telnet atm103@l.atl.hp: .1319 ESTABLISHED
tcp 0 0 .1095 * . * LISTEN
tcp 0 0 .demoond * . * LISTEN
tcp 0 0 .mesoom * . * LISTEN
tcp 0 0 localhost.8846 localhost.1052 ESTABLISHED
tcp 0 0 localhost.1062 localhost.8886 LISTEN
tcp 0 0 .8886 * . * LISTEN
tcp 0 0 .8887 * . * LISTEN
tcp 0 0 .1006 * . * LISTEN
tcp 0 0 .978 * . * LISTEN
tcp 0 0 .22370 * . * LISTEN
tcp 0 0 .389 * . * LISTEN
tcp 0 0 .9181 * . * LISTEN
tcp 0 0 .1054 * . * LISTEN
tcp 0 0 .1051 * . * LISTEN
tcp 0 0 .diagmond * . * LISTEN
tcp 0 0 .1045 * . * LISTEN
tcp 0 0 .1038 * . * LISTEN
tcp 0 0 .135 * . * LISTEN
tcp 0 0 .ueog * . * LISTEN
tcp 0 0 .1036 * . * LISTEN
tcp 0 0 .dpsconn * . * LISTEN
tcp 0 0 .egc * . * LISTEN
tcp 0 0 .dpsccn * . * LISTEN
tcp 0 0 .rcserv * . * LISTEN
tcp 0 0 .kiogin * . * LISTEN
tcp 0 0 .kahuell * . * LISTEN
tcp 0 0 .changen * . * LISTEN
tcp 0 0 .discard * . * LISTEN
tcp 0 0 .echo * . * LISTEN
tcp 0 0 .time * . * LISTEN
tcp 0 0 .daytime * . * LISTEN
tcp 0 0 .printer * . * LISTEN
tcp 0 0 .auth * . * LISTEN
tcp 0 0 .exec * . * LISTEN
tcp 0 0 .shell * . * LISTEN
tcp 0 0 .login * . * LISTEN
tcp 0 0 .telnet * . * LISTEN
tcp 0 0 .ftp * . * LISTEN
tcp 0 0 792 ** LISTEN
tcp 0 0 ** CLOSED
tcp 0 0 * 787 * ** LISTEN
tcp 0 0 * ** LISTEN
tcp 0 0 78 * ** LISTEN
tcp 0 0 * portmap ** LISTEN
udp 0 0 * hci * ** LISTEN
udp 0 0 * 112 * **
udp 0 0 * 177 * **
udp 0 0 1903 * **
udp 0 0 * * * **
udp 0 0 D **
udp 0 0 D * * **
udp 0 0 D * 1f44 * **
udp 0 0 0 79 **
udp 0 0 D D224 * **
udp 0 0 D 198 * **
udp 0 0 D 1070 * **
udp 0 0 D 1070 * **
udp 0 0 D 475 * **
udp 0 0 D 0 * **
udp 0 0 D 1045 * **
udp 0 0 D snmp * **
udp 0 0 D 1940 * **
udp 0 0 D 1f40 * **
udp 0 0 D cchargen * **
udp 0 0 D discard * **
udp 0 0 D echo * **
udp 0 0 D time * **
udp 0 0 D daytime * **
udp 0 0 D ntalk * **
udp 0 0 D bootps * **
udp 0 0 D 1025 * **
udp 0 0 D 787 * **
udp 0 0 D 798 * **
udp 0 0 D 497 * **
udp 0 0 D 1037 * **
udp 0 0 D 0 * **
udp 0 0 D 1036 * **
udp 0 0 D 1035 * **
udp 0 0 D 177 * **
udp 0 0 D portmap * **
udp 0 0 D 1034 * **
udp 0 0 D syslog * **
udp 0 0 D D221 * **
```

#### 其他网络命令和配置

活动的 UNIX 域套接字

```
Address Type Recv-Q Send-Q Inode Conn Refs Nexthref Addr
b8be00 stream 0 0 a19000 0 0 0 /tmp/.AgentSo*
red000 dgram 0 0 c99000 0 0 0 /opt/dcelocal
cebe00 dgram 0 0 d21000 0 0 0 /opt/dcelocal
bd2020 dgram 0 0 b87000 0 0 0 /opt/dcelocal
bd3700 dgram 0 0 b84800 0 0 0 /opt/dcelocal
b24e00 dgram 0 0 b84000 0 0 0 /opt/dcelocal
d54400 dgram 0 0 b84000 0 0 0 /var/tmp/gph_
d85c00 dgram 0 0 be7000 0 0 0 /var/tmp/gph_1
c8b200 dgram 0 0 b21000 0 0 0 /opt/dcelocal
c8c440 stream 0 0 b78400 0 0 0 /opt/dcelocal
b80300 dgram 0 0 b78000 0 0 0 /opt/dcelocal1
b5c090 dgram 0 0 d22400 0 0 0 /opt/dcelocal
cc8c00 dgram 0 0 ba1000 c4a180 c32e80 0 /opt/dcelocal
tbe190 dgram 0 0 9a4400 0 0 0 /opt/dcelocal
d6a100 stream 0 0 9a4800 0 0 0 /opt/dcelocal
bc5600 dgram 0 0 cc0000 d4d940 0 0 /opt/dcelocal1
c44200 dgram 0 0 cf8000 c32c80 0 0 /opt/dcelocal1
cfd800 dgram 0 0 d24000 c12000 0 0 /opt/dcelocal1
CE5e00 stream 0 0 c1b000 0 0 0 /opt/dcelocal
D1dd00 dgram 0 0 ca8400 0 0 0 /opt/dcelocal1
cf8c00 dgram 0 0 a92800 a15bc0 0 /opt/dcelocal7
d2d600 dgram 0 0 a93800 c13200 0 ddbb80 /opt/dcelocal
c98e00 dgram 0 0 a93800 0 0 0 /opt/dcelocal
06a800 stream 0 0 ba3000 0 0 0 /var/opt/GW/SI
```



此输出包含大量信息。你可以参考 HP-UX 系统上的在线手册页。

第一行显示 Proto 为 tcp，Local Address 为 system1.telnet，状态为 ESTABLISHED。这是我们要对该系统发起的连接。我们位于 system1 上，并且有一个到运行 netstat 命令的系统的 telnet 会话处于打开状态。

其余大部分 tcp 协议条目均处于监听状态。这意味着它们正在监听传入连接，如 LISTEN 所示。它们在 Foreign Address 字段中有一个通配符，一旦连接建立，该字段将包含对应的地址。如 ESTABLISHED 所示，我们是少数已建立连接的其中之一。

所有发送和接收队列（显示为 Recv-Q 和 Send-Q）均为空，如 0 所示。

输出末尾的 UNIX 域套接字是 NFS 等多种服务的流和报文连接。

此输出让你能够了解你的 UNIX 系统在网络视角下正在发生的巨大活动量。自 UNIX 诞生以来，网络与连接一直是其最先进的方面之一。

##### route

netstat 显示的信息是你系统的路由表。其中一些是在系统启动或网络接口初始化时，通过 ifconfig 命令自动创建的。到未直接连接到你的系统的网络和主机的路由，是通过 route 命令输入的。

可以即时进行路由更改，就像我将标志从 U 更改为 UG 那样：

```
% /usr/sbin/route add default 128.185.61.1 3
```

首先是 route 命令。其次，我们指定要添加一条路由；另一个选项是删除一条路由。第三，我们指定目标，在此例中是默认目标。这可能是一个特定的主机名、网络名、IP 地址，或者表示通配网关路由的 default（如我们的示例所示）。第四是到达目标所使用的网关。在上述示例中，使用的是 IP 地址，但也可以使用主机名。3 对应于用于指定网关是本地主机还是远程网关的计数。如果网关是本地主机，则使用计数 0。如果网关是远程主机（如示例中的情况），则使用计数 >0。这对应于 Flags 中的 UG。这通过添加具有适当 Flags 的默认路由，手动更改了网络路由表。执行此命令解决了我遇到的问题，即让 system1 与路由器另一侧的系统进行通信（回想图 13-11）。

在执行带有 add 选项的 /usr/sbin/route 之前，你可以先使用 delete 选项来移除现有的不工作的默认路由。

route 命令通常出现在系统的某个启动文件中，以便每次系统启动时都会发出 route 命令。这确保了每次系统启动时都有正确的连接信息就位。

##### ifconfig

ifconfig 命令提供有关 LAN 接口的额外信息。
以下示例提供了网络接口的配置：

```
$ /etc/ifconfig lan0
lan0:	flags=863<UP,BROADCAST,NOTRAILERS,RUNNING>
	inet 128.185.61.2 netmask ffff0000 broadcast 128.185.61.255
```

从这个例子中，我们可以快速看出接口已启用，地址为 128.185.61.2，并且网掩码为 ffff0000。再次请注意，你的网络接口可能有不同的名称，例如 leo。
你可以使用 ifconfig 获取网络接口的状态，就像我在这里所做的那样，为网络接口分配地址，或配置网络接口参数。你拥有的网络地址属于“ A ”、“ B ”或“ C ”类，如前所述。在开始配置你的 LAN 接口之前，务必确定你的网络类别。此示例是一个“ B ”类网络，因此网掩码定义为 ffff0000（这是“ B ”类地址的典型值），而不是 ffff00（这是“ C ”类网络的典型值）。网掩码用于确定保留多少地址来将网络细分为较小的网络。网掩码可以表示为十六进制（如上所示）或十进制格式（如 /etc/hosts 文件中所示）。以下是我发出的用于配置接口的 ifconfig 命令：

```
$ /etc/ifconfig lan0 inet 128.185.61.2 netmask 255.255.0.0
```

-   255.255.0.0 对应于前面针对“ B ”类子网掩码显示的十六进制 ffff0000。
-   lan0 是正在配置的接口。
-   inet 是地址族，目前是该系统唯一支持的地址族。
-   128.185.61.2 是系统 1 的 LAN 接口地址。
-   netmask 显示如何细分网络。
-   255.255.0.0 等同于 ffff0000，这是“ B ”类地址的网掩码。

我很好地利用了 netstat、ping 和 ifconfig 来帮助获取网络状态。如果你需要识别任何需要进行的更改，可以使用 ifconfig、route 和 /etc/hosts 来配置网络。子网示例展示了在配置网络以满足当前和未来需求时，你可以多么灵活。在简单网络中，你可能不需要使用这些命令中的许多或复杂的子网划分。在复杂网络中，或者在遇到配置困难时，你可能必须广泛使用这些命令。在任何情况下，网络规划都是设置 UNIX 系统的重要组成部分。

本章中使用的大多数命令是每个系统管理员工具箱的一部分。然而，网络对于 UNIX 系统的使用至关重要，因此在该领域拥有背景知识有助于你更全面地理解系统以及如何更有效地使用它。

##### rpcinfo

作为用户，你可能需要在另一系统上挂载 NFS 目录，或执行一些你以前未在你的系统上执行过的其他功能。你可以通过评估系统中正在运行的守护进程来确定各种功能是否已启用。rpcinfo 允许你通过在系统上（包括本地系统）发出命令 rpc -p system_name 来生成远程过程调用 (RPC)。

以下示例显示在我们的本地系统上发出 rpcinfo -p：

```
# rpcinfo -p
program vers proto  port service
100000 2 tcp 111 portmapper
100000 2 udp 111 portmapper
100024 1 udp 777 status
100024 1 tcp 779 status
100021 1 tcp 783 nlockmgr
100021 1 udp 1035 nlockmgr
100021 3 tcp 787 nlockmgr
100021 3 udp 1036 nlockmgr
100020 1 udp 1037 flockmgr
100020 1 tcp 792 flockmgr
100021 2 tcp 795 nlockmgr
100068 2 udp 1040 cmsd
100068 3 udp 1040 cmsd
100068 4 udp 1040 cmsd
100068 5 udp 1040 cmsd
100083 1 tcp 1036 ttdbserver
100005 1 udp 976 mountd
100005 1 tcp 978 mountd
100003 1 udp 2049 nfs
150001 1 udp 1003 pnfssd
150001 2 udp 1003 pnfssd
150001 1 tcp 1006 pnfssd
150001 2 tcp 1006 pnfssd
#
```

系统中正在运行许多对我喜欢使用的功能很重要的守护进程。mountd 正在运行，这表明服务器可以在此计算机上挂载 NFS 文件系统。挂载发生还需要其他设置，但至少支持此功能的守护进程正在运行。此外，pnfssd 正在运行，意味着我们支持基于 Windows 的 NFS 访问。

##### arp

用于维护 IP 地址及其对应 MAC 地址列表的机制是 ARP 缓存。映射的地址仅在缓存中保留几分钟，因此如果你想查看最近映射的地址，可以使用 arp 命令，如下面的示例所示：

```
# arp -a
o2 (10.1.1.10) at 0:10:83:f7:a2:f8 ether
l1 (10.1.1.11) at 0:10:83:f7:2e:d0 ether
63.88.85.1 (63.88.85.1) at 0:30:94:b0:b8:a0 ether
l3 (10.1.1.200) at 0:10:83:fc:52:88 ether
tapel (10.1.1.14) at 0:10:83:f7:ae:32 ether
tapel (10.1.1.14) at 0:10:83:f7:ae:32 ether
tapel (10.1.1.14) at 0:10:83:f7:ae:32 ether
tapel (10.1.1.14) at 0:10:83:f7:ae:32 ether
63.88.85.18 (63.88.85.18) -- no entry
```

当前的 arp 条目通过 -a 命令显示。你可以使用 -s 选项创建条目。

##### lanadmin

lanadmin 用于查看和管理网络卡。不带选项发出 lanadmin 会进入交互界面，如下面的示例所示：

```
##### lanadmin
LOCAL AREA NETWORK ONLINE ADMINISTRATION, Version 1.0
Copyright 1994 Hewlett Packard Company.
All rights are reserved.
Test Selection mode.
```





# 局域网接口管理

## lan
- `lan` = 局域网接口管理
- `menu` = 显示此菜单
- `quit` = 终止管理
- `terse` = 不显示命令菜单
- `verbose` = 显示命令菜单

输入命令：lan
局域网接口测试模式：局域网接口 FPA 编号 = 0

## 局域网接口命令
- `clear` = 清除统计寄存器
- `display` = 显示局域网接口状态和统计寄存器
- `end` = 结束局域网接口管理，返回测试选择
- `menu` = 显示此菜单
- `fpa` = 局域网接口的 FPA 编号
- `quit` = 终止管理，返回 shell
- `reset` = 重置局域网接口以执行自检
- `specific` = 进入驱动程序特定菜单

输入命令：d

### 局域网接口状态显示
- FPA 编号 = 0
- 描述 = Land Hewlett-Packard 10/100 TX 半双工 TT - 1500
- 类型 (值) = ethernet-csmacd(6)
- MTU 大小 = 1500
- Bwcd = 100000000
- 站点地址 = 0x10831ffcaae
- 管理状态 (值) = up(1)
- 操作状态 (值) = down(2)
- 最后更改 = 237321866
- 入站八位位组 = 0
- 入站单播数据包 = 0
- 入站非单播数据包 = 0
- 入站丢弃 = 0
- 入站错误 = 0
- 入站未知协议 = 0
- 出站八位位组 = 820
- 出站单播数据包 = 28
- 出站非单播数据包 = 0
- 出站丢弃 = 1
- 出站错误 = 0
- 出站队列长度 = 0
- 特定值 = 65536?

按 <Return> 继续

在此示例中，我们执行了 **lanadmin**，并指定我们要进入 *lan* 接口管理，且希望显示关于该接口的信息。

**lanadmin** 也可以用于执行诸如使用 -M 和 -S 选项分别更改局域网接口的 MTU 或速度等任务。

##### ndd

**n**d 用于执行网络调优并查看有关网络参数的信息。要使用 **ndd** 查看有关所有受支持可调节参数的信息，您需要执行 **ndd -h supported**。您可以使用 -get 选项获取参数的值；您可以使用 -set 选项设置参数的值。

##### nslookup

**nslookup** 用于将主机名解析为 IP 地址。您执行 **nslookup hostname**，**nslookup** 将访问 /etc/resolv.conf 文件或 /etc/hosts 来解析主机名。以下示例显示一个使用 /etc/hosts 生成系统 12 的 IP 地址的系统：

```
# nslookup 12
Using /etc/hosts on:	13

looking up FILES
Name:	12
Address:	10.1.1.12
#
```

您还可以通过在不带任何命令行参数的情况下发出命令来运行 **nslookup** 的交互模式。以下示例显示在不带任何命令行参数的情况下发出命令以进入交互模式，然后输入 help 以获取有关您可以发出的命令的信息：

```
# nslookup 12
> help
NAME		-	print address information about NAME
IP-ADDRESS	-	print hostname information about IP-ADDRESS
policy		-	print switch policy information
server NAME	-	set default server to NAME, using current default server
lserver NAME	-	set default server to NAME, using initial server
```

其他网络命令和设置

- `set OPTION` - 设置 **OPTION**
- `all` - 打印选项、当前服务器和主机
- `[no]swtrace` - 打印查找结果和查找开关消息

# 第 14 章

# 通用桌面环境

## CDE 和虚拟分区

在同一台计算机上运行多个 HP-UX 实例就像拥有多个系统一样。这意味着您在不同 vPar 中为用户配置的通用桌面环境 (CDE) 与在不同系统上配置的方式完全相同。有一些配置文件会在系统范围内影响 CDE。您需要在每个 vPar 上设置这些系统范围的配置文件，以满足在相应 vPar 中工作的特定人员的特定需求。

在接下来的部分中，我们将在虚拟分区中修改 CDE，以在登录屏幕上包含自定义的 CDE 问候语，并自定义菜单以包含一些特定于虚拟分区的命令。

用户在 vPar 系统上第一次接触 CDE 时看到的是登录屏幕。让我们自定义登录屏幕，使其显示主机名（这很可能已经在您的 CDE 登录屏幕上配置好了），以及作为问候语的一部分的 vPar 名称。如果您的主机名和 vPar 名称相同，则您不需要在登录屏幕上提供 vPar 名称。这是对 CDE 的一个有趣自定义，因此我将提供登录屏幕更改作为自定义示例。

登录屏幕的默认信息包含在 /usr/dt/config/C/Xresources 中。我们将把这个文件复制到 /etc/dt/config/C/Xresources，然后将 vPar 名称添加到文件中。该文件中包含 GREETING 的部分如下所示：

```
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!!
!!  GREETING
!!
!! Dlogin*greeting.foreground:          black
!! Dlogin*greeting.background:          #a8a8a8
!! Dlogin*greeting.labelString:         Welcome to $LocalHost$
!! Dlogin*greeting.persLabelString:     Welcome $s
!! Dlogin*greeting.alignment:           ALIGNMENT_CENTER
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!!
```

该文件中的 `//` 表示注释（与我们在 shell 程序中习惯使用的 # 不同。）我们可以取消注释显示 `$LocalHost$` 的那一行，并添加虚拟分区名称，如下所示：

从：

```
!! Dlogin*greeting.labelString:  Welcome to $LocalHost$
```

到：

```
Dlogin*greeting.labelString:     Welcome to $LocalHost% \n
```

这是 *Virtual Partition vPar Name*

如果 vPar 名称和主机名确实不同，您会用您的虚拟分区名称替换 *vPar Name*。图 14-1 显示了我们创建的修改后的问候语：

![](img/eff8b9287a5f38c5adf538f24aacf29e_920_0.png)

此屏幕显示了我们在登录屏幕上更新的问候语，包括主机名 *actappd1* 以及我们将放置 vPar 名称的行。

### 虚拟分区的菜单选择

在本节中，我们将向我们的 CDE 菜单添加一些与虚拟分区相关的命令。由于大多数虚拟分区工作都是由系统管理员执行的，因此我们将在接下来的示例中仅更新 *root* 的菜单选择。登录屏幕的默认信息包含在 `/usr/dt/config/C/Xresources` 中。我们将此文件复制到 root 的主目录和 `.dt` 目录，在此 `vPar` 中，即 `/root/.dt`。复制后，我们将文件重命名为 `dtwmrc`。在更新之前，`/root/.dt/dtwmrc` 的菜单部分如下所示：

```
Menu DtRootMenu
{
   "Workspace Menu"                       f.title
   "Shuffle Up"                           f.circle_up
   "Shuffle Down"                         f.circle_down
   "Refresh"                              f.refresh
   "Minimize/Restore Front Panel"         f.toggle frontpanel
   no-label                               f.separator
   "Restart Workspace Manager..."         f.restart
   no-label                               f.separator
   "Log out..."                           f.action ExitSession
}
```

我们将把新的菜单选择添加在 `DtRootMenu` 条目之后，我们在系统中看到这是鼠标左键的“工作区菜单”。添加菜单选择后，文件如下所示：

```
Menu DtRootMenu
{
   "Workspace Menu"                       f.title
   "Shuffle Up"                           f.circle_up
   "Shuffle Down"                         f.circle_down
   "Refresh"                              f.refresh
   "Minimize/Restore Front Panel"         f.toggle frontpanel
   no-label                               f.separator
   "Restart Workspace Manager..."         f.restart
   no-label                               f.separator
   "Log out..."                           f.action ExitSession

Menu vParMenu
   "vPar Menu"                            f.title
   "vparstatus"                           f.exec "xterm -T vparstatus -e
                                               /usr/bin/sh -c `vparstatus; read xxx"`
   "vparstatus -v"                        f.exec "xterm -geometry 80x50-55+0
                                               -sl 200 -bg white -T vparstatus_verbose
                                               -e /usr/bin/sh -c `vparstatus -v;more; read xxx"`
   "Login vPar2"                          f.exec "xterm -geometry 80x50-55+0 -sl 200 -bg white
                                               -T vPar2 -e remsh vpcvarpd 2 &"
}
```




### 虚拟分区菜单选项

**l.title** 函数表明这是菜单标题。**f.exec** 表示执行后续字符串。在第一个菜单选项 *vparstatus* 中，我们简单地打开一个 *term* 窗口，运行 **vparstatus** 命令，并在关闭窗口前使用 **read** 等待用户输入。下一条命令使用 **vparstatus -v**，其输出更为详尽。对于此命令，我打开一个更大的 *view* 窗口并运行 **vparstatus -vmore**，以便当命令结果超过一屏输出时，用户可以按下空格键。（**vparstatus** 和 **read** 命令周围有单引号。）我在 *term* 上为登录到第二个 vPar 的远程连接增加了更多选项，使终端窗口非常大，拥有大量终端内存并使用特定颜色。我们的新菜单现在看起来就像图 14-2 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_922_0.png)

图 14-2 vPars 菜单选项

这些菜单选项提供了 vPar 状态、带有详细输出的状态以及到我们第二个 vPar 的远程登录。执行这些命令会打开窗口并执行菜单选项中显示的命令。

图 14-3 展示了一个屏幕截图，其中从菜单中选择了两个 **vparstatus** 命令后，打开了两个 **vparstatus** 窗口：

![](img/eff8b9287a5f38c5adf538f24aacf29e_923_0.png)

图 14-3 显示两个 **vparstatus** 窗口的屏幕截图

左上角的窗口包含 **vparstatus** 的输出，而右侧的窗口包含 **vparstatus -v** 的输出。更新后的菜单显示在屏幕左下角。

我们可以进行额外的 CDE 自定义，例如为我们的 VPar 创建工作空间，这样当选择某个工作空间时，我们就会打开指向该工作空间命名的 VPar 的窗口。

本章剩余部分提供了 CDE 的背景知识。我们仅针对 VPar 环境对 CDE 进行了基本自定义。你可以在 CDE 中进行广泛的自定义。本章剩余部分提供的背景知识可以为你进行额外自定义提供帮助。

### 本章非 vPars 特定部分：简介

通用桌面环境（CDE）代表了主要 UNIX 厂商在桌面层统一 UNIX 的努力。CDE 被许多 UNIX 系统上的 X 终端和工作站用户广泛使用。由于你可能管理着许多运行 CDE 的 UNIX 变体，我将介绍 IBM 的 AIX 系统、惠普的 HP-UX 系统和 Sun Microsystems 的 Solaris 系统上的 CDE。本章提供了 CDE 的简介；它涉及 CDE 外观和感觉的基础知识，描述了对 CDE 环境进行修改的方法，并包含了一些关于 X、Motif 和 CDE 之间关系的背景知识。本章编写所使用的 CDE 版本为：AIX CDE 1.0、HP-UX CDE 2.1.0 和 Solaris CDE 1.3。较新的版本将具有增强的功能，但通常它们仍应保持相同的运行方式。

CDE 的多个功能使其易于自定义。每个用户都可以访问的样式管理器（Style Manager）使基于单个用户自定义 CDE 变得容易。然而，迟早你会希望为用户提供一些 CDE 功能的共同基础。例如，如果你有一个大多数用户都会运行的应用程序，你可以设置环境变量、准备下拉菜单、提供合适的字体等，从而提高用户的生产力。用户随后可以执行额外的自定义，如定义文件管理器特征和选择背景。

为了帮助你彻底理解 CDE，我将涵盖以下主题：

- 1. 为什么需要图形用户界面（GUI）？
- 2. CDE 基础知识
- 3. 自定义 CDE
- 4. CDE：高级主题
  - X、Motif 和 CDE 之间的关系
  - X、Motif 和 CDE 配置文件
  - CDE 启动时的事件序列
  - CDE 与性能

首先，我将向你解释提供图形界面而不是更常见但更笨拙的逐行终端界面的原因。接下来是对 CDE 桌面工作空间的概述。这部分分为两节：AIX 和 HP-UX（因为它们非常相似）以及 Solaris。每一部分都将概述前置面板（front panel）的功能。接下来，我将指导你进行一些 CDE 自定义。这些自定义将为自行进行更高级更改提供工作基础。我将展示如何进行一些基本的简单更改，然后进行更复杂的更改，最后以修改带有新标志和新欢迎信息的登录屏幕结束。最后，我将深入探讨 X、Motif 和 CDE 关系、配置文件的使用和位置、CDE 启动时内部发生的事情以及 CDE 性能提示等更高级的主题。

#### 为什么需要图形用户界面（GUI）？

为了让计算机能够放置在每个桌面上使用，必须使其更容易使用。需要一种访问计算机能力的新方法，这种方法避免使用命令行提示符，不要求用户记忆复杂的命令，也不要求用户具备网络技术等技术基础设施的实际知识。这并不意味着这些信息不重要；恰恰相反。这些信息既太重要又太专业化，对普通的“工蜂”计算机用户来说没有用处。对于这些用户来说，了解他们的应用程序才是唯一重要的事。毕竟，按照这种推理，驾驶汽车的人不需要是机械师，那么为什么计算机用户必须理解计算机技术呢？图形用户界面（GUI）使计算机对应用程序终端用户可访问。

图 14-4 说明了计算机硬件、操作系统和图形用户界面之间的关系。计算机是底部的硬件平台。操作系统是上一层，代表基于字符的用户界面。要在这个层级控制计算机，用户必须在键盘上输入命令。接下来的几层，从 X 窗口系统开始，代表图形用户界面。要在这些层级控制计算机，用户必须使用鼠标操作图形控件。

![](img/eff8b9287a5f38c5adf538f24aacf29e_926_0.png)

图 14-4 用户界面组件

GUI 用探索取代了记忆。用户现在可以使用下拉菜单、按钮、滑动滚动条以及其他直接操作方式来使用计算机。输入操作系统命令以执行功能的需求大大减少。有了 GUI，使用计算机既更容易学习，也更容易使用。

虽然在美元成本方面相对便宜（CDE 随操作系统“免费”捆绑提供），但 GUI 在 RAM 使用率和性能方面并非没有成本。尽管存在这种性能开销，GUI 已成为计算环境永久的组成部分。其效用带来的好处值得这种成本。

除了减少培训、使常规任务更简单执行并普遍减轻使用计算机压力的图形控件外，GUI 还有两个值得提及的好处：每个显示器的多窗口和客户端-服务器拓扑。

GUI 提供的多窗口好处在于，每个窗口（字面意义上是由窗口框架包围的矩形区域）包含一个独立的应用程序。用户可以同时处理多个打开的窗口。CDE 更进一步；其多工作空间允许用户按任务将应用程序窗口分离到特定的工作空间中。例如，在一个名为“邮件”的工作空间中，用户可能有显示传入电子邮件列表、当前正在阅读的邮件消息以及稍后发送的正在撰写的消息的应用程序窗口。在另一个名为“财务”的工作空间中，他们可能在处理几个电子表格，每个电子表格都在自己的窗口中。

客户端-服务器拓扑使得网络中分散的计算资源能够被高效访问以满足计算需求。在客户端-服务器拓扑中，网络上强大的计算机专门用于特定目的（文件服务器上的文件管理和应用程序服务器上的运行应用程序）。在其他地方使用较弱客户端计算机工作的用户远程访问文件或应用程序。文件服务器通过集中文件备份来减少系统管理，使系统管理员只需备份文件服务器，而无需备份每个单独的客户端计算机。这种设置还确保文件将在定期间隔进行备份。应用程序服务器通过减少所需存储磁盘的数量和大小以及每个客户端计算机所需的 RAM 大小来降低运营成本。应用程序的单个版本驻留在应用程序服务器上并运行，通过网络中的多个用户访问。

虽然这种拓扑听起来很复杂，但 CDE GUI 使其变得容易。要访问文件，用户从文件管理器窗口“拖放”文件图标。要启动应用程序，用户双击应用程序图标。要打印文件，用户将文件拖到前置面板中相应打印机的图标上并在那里放下。用户不需要知道这些文件和应用程序在哪里，它们在什么目录中，它们在什么计算机上，或者如何访问它们。你部署的基础设施和控制，加上 GUI 的强大功能，使用户能够专注于他们的工作，而不是计算机的机械操作。

#### CDE 基础知识

由于大多数系统都附带了一套 CDE 用户指南，我将只概述 CDE 的外观以及我们在进行一些自定义时将涉及的主要领域。在此过程中，我将指出不同 CDE 版本之间的相似之处和差异。

CDE 登录屏幕在你登录之前提供几个选择。在输入用户名的区域下方有四个按钮：**OK**、**Start Over**、**Options** 和 **Help**。**OK** 与输入登录名和密码后按下 *Enter* 相同。**Start Over** 按钮清除你的用户登录并允许你重新开始。**Options** 为你提供在登录前需要进行的初始会话配置。**Language** 允许你更改默认语言。假设你需要用另一种语言测试你公司的软件。假设该




#### CDE 登录及桌面概述

如果系统中预装了合适的语言环境，您只需选择以不同语言显示 CDE，即可在测试时轻松切换语言。会话允许您选择进入 CDE 桌面会话，或者进入一个**故障安全**会话，该会话是一个 X 会话，但不包含 CDE 桌面。Solaris 还提供了登录到**OpenWindows 桌面**或**用户上次使用的桌面**的选项。**命令行登录**允许您在不调用 CDE 的情况下登录，这将只是一个常规的终端模式会话。**重置登录屏幕**的功能如其名称所示。最后，**帮助**功能列出了所有这些功能，并附有每项功能的简要说明。

登录屏幕本身会显示 CDE 标志、操作系统标志（如 AIX），或者可能是您公司的标志。屏幕上方会出现一条欢迎信息以及一个用于输入用户登录名的位置。输入用户名后，系统会提示您输入密码。一旦输入并验证密码正确，CDE 就会启动并显示桌面。在 Solaris 系统上，首次登录时，系统会让您选择是登录到 CDE 还是 OpenWindows 桌面。

CDE 桌面由四个桌面工作区和一个每个工作区共用的前面板组成。前面板是一个易于使用的界面，可访问各种应用程序、命令和工具。各种组件可以通过简单的单击方式轻松访问。前面板组件是一组对象、子面板和桌面工作区访问入口的集合。一些对象仅用于显示项目，例如时钟；而另一些对象在被点击时，要么启动一个应用程序（如日历或 dmail），要么执行某个操作（如锁定或退出操作图标）。子面板会弹出一个对象菜单，供用户访问。这些对象也可以仅用于显示项目或启动应用程序。默认情况下，在 AIX 和 HP-UX 上，您会看到个人打印机子面板、个人应用程序子面板和帮助子面板。在 Solaris 上，所有面板都包含子面板。正如您在下一节“自定义 CDE”中将会看到的，AIX 和 HP-UX 上的其他面板也可以添加子面板。您可以通过观察每个面板上方的小箭头来识别它们，点击该箭头即可弹出子面板。在前面板的中央是四个工作区。这些工作区提供了执行相关任务的空间，使用户能够区分工作，避免桌面杂乱无章。

AIX 和 HP-UX 上的 CDE 非常相似，通常，一个系统前面板上显示的内容与另一个系统是相同的。然而，Solaris 在保留基本 CDE 外观和感觉的同时，大大扩展了默认前面板及其背后子面板所包含的内容。我将首先概述在 HP-UX 和 AIX 上找到的 CDE。然后，我将指出 Solaris 对 CDE 的增强功能。

### AIX 和 HP-UX 上的 CDE

前面板分为 11 个主要区域：5 个面板、1 个工作区区域和另外 5 个面板。我将按照从左到右的顺序概述每个区域，从时钟开始，以垃圾桶结束，如 图 14-5 所示。

![](img/eff8b9287a5f38c5adf538f24aacf29e_929_0.png)

- **时钟** - 顾名思义，它显示当前时间。

- **日历** - 日历图标显示当前日期，点击后弹出预约日历。该日历允许您设置预约和提醒，并创建任务列表。预约可以设置为单次事件或重复事件。您可以通过蜂鸣声、弹出消息或电子邮件收到预约通知。日历及其相关预约可以按天、按周或按月显示。也可以显示年度日历，但不包含预约。

- **文件管理器** - 文件管理器打开一个窗口，显示您的主目录及相关文件。从这里，您可以执行多种基本文件操作，例如复制文件、移动文件、删除文件或执行程序或脚本。不常用的操作，如创建符号链接或更改文件权限或所有权，也可以在此完成。从文件管理器中移除文件会将其移动到垃圾桶，而不是永久删除文件。这样，如果您决定需要找回该文件，只需从垃圾桶中恢复即可，而无需从备份中恢复——这是一种更耗时的操作。但请注意，每次会话结束时会自动“清空”垃圾桶。因此，当您注销时，文件将被永久删除。

- **个人应用程序** - 个人应用程序子面板包含 CDE 的文本编辑器 **dtpad** 和终端模拟器 **dterm**。它还包含图标编辑器。**dtpad** 是一个易于使用的全屏文本编辑器。与基于 PC 的 word 处理软件类似，**dtpad** 允许您将光标移动到任意位置以添加、更改或删除文本。**vi** 是一种流行的逐行文本编辑器。CDE 的 **dterm** 是一个不错的终端模拟器。图标编辑器可以打开位图（.bm）或像素图（.pm）文件并允许您对其进行编辑。

个人应用程序子面板是我们第一次找到安装图标应用程序的地方。这就是将新图标添加到子面板的位置。这使得与图标关联的应用程序在图标被双击时得以执行。我们在“自定义 CDE”中修改桌面时将使用此功能。

- **邮件** - 当点击此图标时，会调用 CDE 邮件程序 **dmail**。从这里，您可以撰写邮件消息、回复消息和转发消息。您通常认为是基本功能的大多数高级邮件功能都包含在内：例如为消息添加附件、仅回复发件人或所有收件人、以及设置自动回复消息表明您正在休假。另一个功能是当新消息到达时，**dmail** 图标会发生变化，显示一封信装入信箱。

- **工作区区域** - 接下来的四个项目组成了工作区区域。

    - **锁定按钮** - 锁定按钮允许您在离开座位时锁定您的会话。此安全功能可防止他人在您不在时查看或访问您的工作。它免去了每次暂时离开时都要注销并重新登录的麻烦。再次解锁时，必须输入您的登录密码或 root 密码。

    - **工作区切换** - 共有四个，这些是默认创建的独立工作区。它们允许您组织工作，以免工作区变得杂乱无章。通过使用工作区，您可以将不同任务、应用程序或系统的工作彼此分开。您只需点击工作区编号：一、二、三或四，即可从一个工作区切换到另一个。您会发现，无论您处于哪个工作区，前面板都会跟随您。在“自定义 CDE”中，您将看到如何轻松增加工作区数量并更改名称。

    - **活动指示灯** - 活动指示灯简单地表示当系统忙于工作时会闪烁。

    - **退出按钮** - 退出按钮是注销 CDE 并终止 CDE 会话的地方。退出时，根据 CDE 的配置，系统会提示您恢复当前会话或返回主会话。如果您选择恢复当前会话，下次登录时，桌面的外观将与注销时几乎完全相同。某些事情（如远程登录）是不可能的，但其他事情（如自动执行应用程序）是可能的。如果您选择返回主会话，下次登录时，您将返回到已知的预配置状态。此配置在风格管理器面板中设置，稍后讨论。

- **个人打印机** - 此子面板包含您在系统上配置的打印机，包括指定为默认打印机的默认打印机和打印管理器。前面板图标是默认打印机的图标。要打印您的文档之一，只需从文件管理器中将其拖动并放置到打印机图标上即可。打印管理器允许您查看排队中的打印文件，并在打印之前将其移除。但是，这只适用于由您的系统直接管理的打印机。在今天的网络化办公室中，打印机通常是共享的，打印管理功能位于服务器上，很可能在隔壁大楼。

- **风格管理器** - 风格管理器是那些您可以发挥极大的创造力使桌面看起来完全符合您心意，或者浪费大量时间的地方——这取决于您的观点。在这里，您可以按照自己的偏好个性化定制登录到系统的内容。您可以更改字体大小、背景、鼠标速度，以及会话在一定非活动或空闲时间后是否自动锁定。在这里，您可以将前面提到的主会话设置为每次登录时返回的会话，或者将系统设置为返回当前会话，或者选择每次注销时询问的选项。您可以在此配置的另一个选项是窗口焦点是否跟随鼠标，或者您是否必须在窗口成为活动窗口之前先点击它。在 AIX 系统上，您可以切换开关，决定是否在前面板上显示工作区。

- **应用程序管理器** - 打开应用程序管理器时，会显示包含实用应用程序和操作的文件夹。尽管它们不同





在制造商中，甚至在操作系统方面，AIX、HP-UX 和 Solaris 都具有一些基本功能：桌面应用程序、桌面工具、信息和系统管理。桌面应用程序包含计算器、手册页查看器、图标编辑器和创建操作等应用程序和工具。桌面工具包括 sterm、xcwd capture、文件压缩和资源重载等工具。系统管理包含操作系统特定的应用程序，例如 HP-UX 中的 SAM、AIX 中的 SMT 和 Solaris 中的 AdminTool，以及更改密码等更通用的操作。花点时间在这里四处看看。你会发现许多你可能想要集成到你定制的前面板上的项目。就我而言，我发现手册页查看器是一个宝贵的资源，并已将其移动到前面板上，以便于访问。

**帮助** - 帮助子面板是帮助管理器、桌面简介、前面板帮助以及基于项目的前面板帮助机制的汇编。帮助管理器是 CDE 的主要在线帮助设施。这是一个综合帮助系统，具有主题树，可以使用关键字或模式匹配搜索索引，回溯帮助管理器中你去过的地方，并查看你请求帮助的项目历史。桌面简介是 CDE 及其工作原理的概述。前面板帮助设施提供有关如何使用前面板图标、子面板和工作区的信息。基于项目的前面板帮助机制允许你点击你希望获得帮助的前面板项目。除了帮助子面板，你还可以按 F1 功能键请求帮助。如果在你的系统上安装了，AIX 可能还包括基本桌面定制帮助和基础库。

**回收站** - 回收站与文件管理器一起使用，保存你在当前会话中删除的文件和文件夹。使用该设施可以让你快速检索你不应该移除的文件。可以随时“清空”回收站以永久删除项目。此外，当你注销会话时，回收站也会“清空”。

## Solaris 上的 CDE

如前所述，Solaris 已经美化了 CDE，向子面板添加了许多更多的子面板和项目，如图 14-6 所示。Solaris 对面板和子面板进行了大幅更改。我将概述你将找到的内容，就像我在前面关于 AIX 和 HP-UX 部分所做的那样。如果它们相同，我只会注明它们相同。

![](img/eff8b9287a5f38c5adf538f24aacf29e_933_0.png)

**图 14-6 前面板**

与 AIX 和 HP-UX 一样，Solaris 的前面板分为 11 个主要区域：5 个面板、1 个工作区区域和另外 5 个面板。我将从左到右概述每个区域，从世界开始，到回收站结束。

- **链接** - 正如你可能通过世界图标猜到的一样，这是你访问世界的地方。Solaris 的 Web 浏览器 Hotjava 位于此处。这里还包括访问 Web 浏览器个人书签的操作，以及查找网页搜索引擎。正如前面板图标所示，世界上也有一个时钟。

- **卡片** - 日历与 AIX 和 HP-UX 上的相同。然而，子面板中包含查找卡片，这是一个 Rolodex 类型的地址管理器。

- **文件** - 尽管标题略有不同，但这是文件管理器所在的地方。子面板中包含执行与属性、加密、压缩文件、归档和查找文件相关的文件操作的专用图标。Solaris 还包含了管理软盘驱动器和 CD-ROM 的操作。

- **应用程序** - 简单重命名为应用程序，这里不仅包含文本编辑器，还包含文本笔记和语音笔记。对于启用音频的环境，语音笔记允许你播放、录制或保存 WAV、AU 和 AIFF 格式的音频文件。在这个子面板上，你还会找到在 AIX 和 HP-UX 系统的应用程序管理器下找到的应用程序子面板。与其他系统一样，这包括桌面应用程序、桌面工具、信息和系统管理。这些在所有系统上基本上是一样的。

- **邮件** - 此子面板除了 dtmail 外，还增加了建议箱。这是一个非常巧妙的想法，它会自动打开一封预填好地址发给 Sun Microsystems, Inc. 的电子邮件，以便你可以向他们发送你的建议。

- **工作区区域** - 接下来的五个项目组成了工作区区域：
  - **锁定按钮** - 与 AIX 和 HP-UX 上的相同。
  - **工作区切换** - 与 AIX 和 HP-UX 上的相同。
  - **进度指示器** - 这与 AIX 和 HP-UX 上的忙碌指示器相同。
  - **退出按钮** - 与 AIX 和 HP-UX 上的相同。
  - **个人打印机** - 与 AIX 和 HP-UX 上的相同。

- **工具** - 样式管理器位于此处，并显示在前面板上。你还可以轻松访问 CDE 错误日志，查找进程允许你查看系统中正在运行的所有进程并杀死选定的进程。自定义工作区菜单和将项目添加到菜单的操作允许你轻松修改工作区菜单。通过将鼠标移到桌面的空白区域并按住鼠标右键来访问工作区菜单。AIX 和 HP-UX 带有通用菜单，而 Solaris 将前面板和子面板操作纳入工作区菜单，作为访问这些操作的另一种方式。

- **主机** - 在此，Solaris 与 AIX 和 HP-UX 有很大不同。主机子面板包含与系统相关的操作。在前面板上，你会发现性能监视器图标，指示你的 CPU 和磁盘驱动器有多忙。从子面板，这个主机打开 dterm 终端模拟器，而控制台打开专门用于显示控制台消息的 dterm。系统信息提供系统信息，包括系统名称、硬件型号、网络 IP 地址和域名、物理和虚拟内存、操作系统版本以及上次重启的日期和时间。查找主机与卡子面板中的查找卡片相同。

- **帮助** - 这与 AIX 和 HP-UX 上的相同。

- **回收站** - 回收站相同，只是增加了一个“清空”回收站的子面板图标。

这就结束了对 CDE 外观和感觉的概述。掌握了这些知识，你可以轻松自信地在你的桌面环境中导航。接下来，你将学习如何更改该外观和感觉以符合你的工作环境。

#### 定制 CDE

在修改任何 CDE 配置文件之前，首先制定策略。我知道我之前提过这一点，但这足够重要，值得再次提及。

以下问题可以帮助你开始：

1. 你的用户需求是什么？
2. 这些需求中哪些可以通过重新配置 CDE 来满足？
3. 应在什么级别进行这些更改（全系统、用户组、仅单个用户）？
4. 你需要修改哪些 CDE 文件（名称和位置）？
5. 更改是什么，以及它们在文件中的顺序是什么？

随身携带一本包含每个 CDE 组件的手册页（用于查找资源及其值）以及每个 CDE 配置文件的副本也是一个好主意。

现在你对 CDE 的工作方式有了很好的理解，我将指导你进行更改并定制系统，以适合整个用户社区或每个个人用户。

我将在每个更改之前讨论涉及该更改的内容。我将进行一些基本的简单更改以及一些更高级的更改，以展示 CDE 的多功能性。

我需要提到的一件事是，所有这些更改都可以在任何系统上进行。并且知道如何“以艰难的方式”执行这些任务会增加你对这些工具在后台为你做什么的理解。所以务必尝试每一个。

##### 使用样式管理器进行更改

#### 字体大小

当我们最初登录 CDE 且工作区出现时，如图 14-7 所示，许多用户更改的第一件事之一就是字体大小。初始设置为 4，大多数用户希望字体更大。这种更改很容易。

![](img/eff8b9287a5f38c5adf538f24aacf29e_936_0.png)

**图 14-7 样式管理器**

1. 点击前面板上的**样式管理器**图标。此操作会打开样式管理器。
2. 点击**字体**。
3. **高亮显示 5**。
4. 点击**确定**。

#### 背景颜色和色彩

样式管理器也是我们更改背景颜色和色彩的地方：





1.  单击“背景”（Backdrop），我们将看到各种背景选择。
2.  当我们看到喜欢的背景（如 Pebbles）时，可以单击“应用”（apply），然后单击“关闭”（close）来更改背景。但请注意，此操作仅更改当前所处工作区的背景。

若要更改其他工作区，我们可以转到相应工作区并在那里调出样式管理器（Style Manager）；或者，由于样式管理器已经打开，我们可以单击窗口右上角（“File”上方）的小“*”号，访问下拉菜单。在此处，我们可以选择“占据所有工作区”（Occupy All Workspaces）。然后我们只需转到其他工作区，样式管理器就已经在那里准备好了。背景区域是唯一需要注意移动到“其他工作区”的地方。

3.  若要更改颜色，请单击颜色（Color）图标。我们会得到一份不同的颜色方案列表供选择。如果某个方案不完全符合喜好，我们可以轻松修改颜色、色调、亮度和对比度。我们甚至可以从其他位置（例如网络上的图片）提取颜色，将其纳入颜色方案。一旦确定了喜欢的颜色，我们即可使用自定义名称保存该方案。

##### 在前面板中添加或移除对象

通过在前面板中包含常用项，前面板可以让我们的工作稍微轻松一些。最频繁的操作之一是打开终端窗口。虽然 CDE 默认使用 xterm 作为终端窗口，但我们有时可能希望使用另一个 xterm 窗口（注：原文此处逻辑略显矛盾，可能指特定环境的 xterm 或指代不同终端，按原文直译）。我们将把它添加到“个人应用程序”（Personal Applications）子面板中，因为 xterm 存在于 AIX 和 HP-UX 系统上。Solaris 用户可以通过将 xterm 放在“主机”（Hosts）子面板中实现相同效果，该子面板容纳“本机”（This Host）终端仿真器。

添加对象到 CDE 前面板有两种方式：

-   将它们拖放到滑出式子面板中，然后将其设为该子面板的默认项。
-   修改 `/etc/dt/appconfig/types/C/dtwm.fp` 配置文件。此方法将在我们稍后创建操作和文件类型时使用。

通过拖放添加控制按钮的基本操作如下：

-   从应用程序管理器视图中，将您希望作为前面板按钮的应用程序图标拖出，并将其放置到相应子面板的安装区（顶部区域）。
-   将鼠标指针悬停在图标上，按下鼠标按钮 3 以显示子面板菜单。
-   选择“复制到主面板”（Copy to Main Panel）。

1.  **单击** AIX 或 HP-UX 上“个人应用程序”子面板（或 Solaris 上“主机”子面板）的**向上箭头**，使其弹出。
2.  **单击应用程序管理器**（Application Manager）图标，桌面应用程序和桌面工具位于此处。
3.  **双击 Desktop_Tools**。您会在这里找到 **Xterm**。
4.  **将 Xterm** 图标从 Desktop_Tools 拖放到 HP-UX 和 AIX 上“个人应用程序”子面板顶部的“安装图标”（Install Icon）框中，或 Solaris 上的“主机”（Hosts）子面板中。

现在，如果我们想在前面板中包含 **xterm**：

1.  在“个人应用程序”或“主机”子面板中，**右键单击 Xterm** 图标。
2.  根据您使用的 CDE 版本，选择 **Copy to Main Panel**（复制到主面板）或 **Promote to Front Panel**（提升到前面板）。

##### 添加另一个工作区

对前面的另一个简单更改是添加另一个工作区。CDE 默认提供四个工作区，但这很容易更改。我们将再添加一个并将其命名为“Web View”（网络视图）。这可以作为我们访问互联网的窗口。

1.  将鼠标放在前面板的工作区（Workspace）区域，按下鼠标右键。
2.  从下拉菜单中选择“添加工作区”（Add Workspace）。工作区“New”（新建）已被添加。
3.  右键单击标记为“New”的新工作区，选择“重命名”（Rename）。输入 Web View 并按下 Return（回车）键。

如果我们想删除某个工作区，只需右键单击要移除的工作区，然后选择“删除”（delete）。

进行这类更改非常简单，它们有助于为个别用户个性化工作区。

## 以其他方式更改前面板

除了添加和移除按钮，您还可以以其他方式塑造前面板。这些其他方式使用工作区管理器（Workspace Manager）资源来修改默认值。以下资源与前面板相关：

-   **clientTimeoutInterval** - 从前面板启动客户端时，忙碌指示灯闪烁且指针保持为沙漏状的持续时间。
-   **geometry** - 前面板的 x 和 y 坐标位置。
-   **highResFontList** - 在高分辨率显示器上使用的字体。
-   **lowResFontList** - 在低分辨率显示器上使用的字体。
-   **mediumResFontList** - 在中等分辨率显示器上使用的字体。
-   **name** - 当 dtwm.fp 中存在多个前面板时，所使用的某个前面板的名称。
-   `pushButtonClickTime` - 区分两次单击和一次双击的时间间隔（以避免意外双击启动应用程序）。
-   `waitingBlinkRate` - 前面板忙碌指示灯的闪烁频率。
-   `workspaceList` - 工作区名称列表。
-   `title` - 显示在工作区按钮上的标题。

与其他所有工作区管理器资源一样，这些前面板资源具有以下语法：

```
Dtwm*screen*resource: value
```

例如，假设除了默认的四个工作区外，用户只需一个具有六个名为 Mail、Reports、Travel、Financials、Projects 和 Studio 的工作区的前面板。此外，他们更喜欢大字体，并决定使用 10 号粗体 New Century Schoolbook。作为系统管理员，您可以使用以下资源规范让所有用户满意：

```
Dtwm*0*workspaceList: One Two Three Four Five Six
Dtwm*0*One*title: Mail
Dtwm*0*Two*title: Reports
Dtwm*0*Three*title: Travel
Dtwm*0*Four*title: Financials
Dtwm*0*Five*title: Projects
Dtwm*0*Six*title: Studio
Dtwm*0*highResFontList:
 -adobe-new century schoolbook-bold-r-normal\n -10-100-75-75-p-66-iso8859-1
```

屏幕标识通常为 0，除非显示器同时具备图像平面和叠加平面能力。X*screens* 文件中屏幕的顺序决定了屏幕编号；第一个屏幕（通常是图像平面）标识为 0。请注意，在六个标题资源规范中包含了工作区名称（One, Two, Three, Four, Five 和 Six）。

这些更改可以添加到 `sys.resources` 文件中，该文件在本章后面的“高级 CDE 主题”中详细讨论。这些更改也可以通过使用 `EditResources` 操作将新的资源行插入每个用户的 `RESOURCE_MANAGER` 属性中，然后重启工作区管理器来实现。

显而易见的缺点是，您需要物理前往每个用户的工作区域，并接管机器几分钟。然而，好处是更改是即时的，并且会自动保存到恢复当前会话的用户的正确的 **dt.resources** 中。您还可以避免更改被覆盖，这种情况可能发生在用户仍在线时修改了错误的 **dt.resources** 文件的时候。

## 修改滑出式子面板中的内容

子面板在 **dtwm.fp** 中定义于前面板及前面板控件定义之后。要将子面板与前面板控件按钮关联，需将前面板控件名称列在子面板定义中的容器名称（container name）位置。

注意：全局更改在 **/etc/dt** 中进行。**$HOME/dt** 中进行本地或个别用户的更改。

要将滑出式子面板添加到前面板，请遵循以下步骤：

1.  将文件 **/usr/dt/appconfig/types/C/dtwm.fp** 复制到 **/etc/dt/appconfig/types/C/dtwm.fp** 或 **$HOME/dt/types/dtwm.fp**。
2.  确定滑出式面板要与之关联的控件按钮。
3.  在 **dtwm.fp** 中创建子面板定义文件。其形式如下：

```
SUBPANEL  SubPanelName
{
 CONTAINER_NAME AssociatedFrontPanelControlButton
 TITLE  SubPanelTitle
}
```

4.  为子面板创建子面板控件定义。其形式如下：

```
CONTROL  ControlName
{
 TYPE icon
 CONTAINER_NAME SubPanelName
 CONTAINER_TYPE SUBPANEL
 ICON  BitmapName
 PUSH_ACTION  ActionName
}
```





与前面板控制按钮一样，复制并修改现有的子面板文件比从头开始创建要容易得多。

##### 更改默认打印机名称显示

我们现在将对一个弹出子面板进行简单的更改。如果我们调出“个人打印机”（Personal Printers）子面板，它会显示我们已配置了默认打印机，但未显示其名称。让我们回到前面板文件 `dtwm.fp`，并进行更改：

1.  启动您喜欢的编辑器（例如 *dtpad* 或 *vi*），并编辑文件 `$/HOME/di/types/dtwm.fp`。
2.  向下滚动到 **CONTROL Printer**。您将看到 **LABEL** 为 **Default**。请修改或补充该名称为您默认打印机的名称。我的打印机名为 a464。
   ```
   LABEL     Default - a464
   ```
3.  保存文件并重启工作区管理器（Workspace Manager）。将鼠标定位到工作区的空白区域，然后按下鼠标右键。选择“重启工作区管理器”（Restart Workspace Manager）。在 Solaris 上，按下鼠标右键以调出“定制工作区菜单”（Customized Workspace Menu）。在此处，选择“窗口”（Windows），您将在其中找到“重启工作区管理器”选项。

调出“个人打印机”子面板，以查看默认打印机究竟是什么。当然，如果我们更改了默认设置，我们将不得不再次修改前面板。但既然我们现在知道该怎么做，对吧！图 14-8 展示了包含更改后的前面板。

![](img/eff8b9287a5f38c5adf538f24aacf29e_943_0.png)

图 14-8 包含更改的前面板

## 前面板动画

前面板或弹出子面板拖放区域（drop zones）的动画是通过显示一系列位图来创建的。按照惯例，这些位图位于 `*/usr/dd/appconfig/icons*` 中。要显示的位图列表包含在 `*dftwm.fp*` 文件末尾的动画定义中。

要为拖放区域创建动画序列：

1.  创建一系列连续变化的位图。
2.  使用以下语法将这些位图文件的列表添加到相应的配置文件中：
   ```
   ANIMATION AnimationName
   {
       bitmap0
       bitmap1
       bitmap2
       bitmap3
       bitmap4
       bitmap5
   }
   ```
3.  使用以下语法在相应的控制定义中添加一行：
   ```
   DROP_ANIMATION AnimationName
   ```

##### 向工作区菜单添加项

工作区菜单定义在 **sys.dtwmrc** 文件中。如 Solaris 前面板概述中所述，通过鼠标悬停在桌面的空白区域并右键单击可以访问工作区菜单。AIX 和 HP-UX 提供的是通用菜单，而 Solaris 则将前面板和子面板的操作整合到了工作区菜单中，作为访问这些操作的另一种方式。然而，我们可以使用鼠标左键访问，为所有这三个系统创建定制的工作区菜单。我们将接下来执行这项任务。

定制的工作区菜单可以包含常用命令和应用。通常通过按下鼠标左键访问该定制菜单，这会弹出菜单供查看和选择。对于那些定期执行固定数量任务的人来说，工作区菜单非常实用。例如，使用 **C++**、**vi** 和 **isql** 的程序员可以创建一个包含这些项目的菜单，或者系统管理员可以创建一个包含 **df**、**ps -ef** 和 **netstat** 的菜单。或者，在大型网络上的用户可能想要一个系统登录菜单。

对于一两项更改，您可以修改现有的工作区菜单。对于主要更改，在 **sys.dtwmrc** 中插入一个完全新的菜单定义可能更容易。

菜单定义具有以下语法：

```text
Menu MenuName
{
   "Menu Name"     f.title
   "Frame"         f.exec /nfs/system1/usr/frame/bin/maker
   "Second Item"   action
   "Third Item"    action
}
```

第一行指定菜单名称，位于关键字 Menu 之后。大括号之间的行列出了菜单中按出现顺序显示的项目；因此，第一行是由函数 f.title 指定的标题。第二行是一个示例定义，它将在分布式环境中的远程应用服务器上启动 **FrameMaker**。还有其他许多函数，总共约有 45 个。完整列表请参见 **dtwmrc(4)** man 手册页。

为了让用户显示菜单，您需要使用操作 **f.menu MenuName** 将菜单定义绑定到鼠标按钮和屏幕位置。例如，如果用户希望在指针位于工作区背景上时按下鼠标按钮 3 来显示菜单，您将在 **sys.dtwmrc** 末尾的“鼠标按钮绑定\说明”部分插入以下行：

```
<Btn3Down> root f.menu MenuName
```

（实际上，修改已经存在的行会更简单，只需在第二行中将 **MenuName** 替换为 **DtRootMenu** 即可。）

现在，我们将创建一个简单的菜单。我们的菜单将包括运行 **FrameMaker**、运行 **vi** 编辑器以及登录远程系统。

1.  首先，我们需要将 **/usr/dt/config/C/sys.dtwmrc** 文件复制到 **/etc/dt/config/C** 中：`cp /usr/dt/config/C/sys.dtwmrc /etc/dt/config/C/sys.dtwmrc` 如果我们只想为单个用户做本地更改，则将其复制到 **$HOME/.dt** 并重命名为 **dtwmrc**。对于 admin1 用户，即 **/home/admin1/.dt/dtwmrc** 或在 Solaris 上的 **/home/admin1/.Dt/C/dtwmrc**。
2.  进入我们喜欢的编辑器并**修改该文件**。我们将在 DtRootMenu 条目之后立即添加新菜单，在我们系统中，DtRootMenu 显示为鼠标左键的“工作区菜单”。添加以下内容：
   ```
   Menu AdminMenu
   {
       "Admin1's Menu"         f.title
       "Frame Maker"           f.exec "/nfs/system1/usr/frame/bin/maker"
       "VI Editor"             f.exec "xterm -e /usr/bin/vi"
       "Login systemA"         f.exec "xterm -geometry 80x50+830+-0 -sl 200 -bg DarkOrchid4 -fg white -n SYSTEMA -T SYSTEMA -c remsh systemA &"
   }
   ```
3.  **f.title** 函数表明这是菜单标题。**f.exec** 表示执行后面的字符串。请注意，FrameMaker 不需要终端窗口，因为它使用自己的窗口，而 **vi** 和 **login** 都需要一个终端窗口来运行。此外，我在 **xterm** 登录命令上进行了一些修饰，使终端窗口非常大，具有大量的终端内存，并使用特定的颜色。

现在，让我们重启工作区管理器并试用我们的新菜单：

4.  将鼠标定位到工作区的空白区域，并按下鼠标左键。选择**重启工作区管理器**。

创建下拉菜单很容易，并且可以通过向菜单添加子菜单轻松扩展。只需使用函数 **f.menu** 后跟菜单名称即可。在 "Admin1's Menu" 之后立即添加以下内容：

```
"Work Menu"         f.menu  WorkMenu
```

然后在 Menu AdminMenu 部分的大括号 } 之后，添加：

```
Menu WorkMenu
{
    .
}
```

执行这些高级功能其实并不难。最难的部分是记住将文件放在哪些目录中：**/etc/dt** 用于全局更改，或 **$HOME/.dt** 用于个人更改。

## 创建控制按钮、操作和文件类型

一个操作（action）启动一个进程，例如 shell 脚本或应用程序。操作可以连接到前面板按钮，以便在点击该按钮时启动。操作可以连接到前面板拖放区域，以便在数据文件被拖放到该区域时执行。操作可以与文件管理器窗口中的图标相关联，从而通过双击图标来启动该操作。操作可以与特定的数据类型相关联，使得双击数据文件图标时启动该操作并打开该数据文件。

除了设置前面板和默认会话以满足用户需求外，您能为依赖您的用户简化计算生活所做的最重要的一件事就是创建操作和数据类型。

CDE 操作和数据类型定义在扩展名为 .dt 的文件中。与大多数其他 CDE 配置文件类似，*.dt 文件有一个系统范围版本，可以复制到用户的个人目录并进行自定义。大多数系统范围的 *.dt 文件位于 /usr/dt/appconfig/types/C；个人 *.dt 文件是通过从 /usr/dt/appconfig/types/C 复制 user-prefs.dt 到 $HOME/dt/types 创建的。

CDE 用于查找操作和文件类型的默认搜索路径包括以下主要目录，顺序如下：

- \$HOME/dt/types
- /etc/dt/appconfig/types
- /usr/dt/appconfig/types

您可以使用 DTDATABASESEARCHPATH 环境变量向搜索路径添加更多目录。将该环境变量和新的搜索路径插入 /etc/dt/config/Xsession 可产生系统范围的影响。将环境变量和搜索路径插入 $HOME/.dtprofile 可针对个人用户生效。

基本控制定义包含六个部分：

- **CONTROL** _name_ - 定义名称。这是定义中在大括号外的唯一部分。
- **TYPE** - 控制类型。存在多种类型。对于自定义前面板最有用的类型可能是 blank 和


图标。空白项可用作占位符。图标可以启动操作或应用程序，或者充当放置区。

- **图标（ICON）** - 显示在前面板上的位图。前面板位图位于 `/usr/dt/appconfig/icons` 目录中。
- **容器名称（CONTAINER_NAME）** - 包含该控件的容器的名称。这必须与 `dtwm.fp` 中列出的某个实际容器的名称相对应。
- **容器类型（CONTAINER_TYPE）** - 包含该控件的容器类型。可以是 **BOX**、**SWITCH** 或 **SUBPANEL**，但必须与容器名称的类型一致。
- **按动操作（PUSH_ACTION）** - 这是按下控件按钮时发生的事件。**PUSH_ACTION** 只是几种可能操作中的一种。有关更多信息，请参阅 `dtwm` 手册页。

要从前面板移除控件按钮，请在 **CONTROL** 定义行的最左侧列中输入井号（#）。（#）会将控件规范转换为注释行。

通过编辑 `dtwm.fp` 文件来添加控件按钮：

1. 将 `dtwm.fp` 从 `/usr/dt/appconfig/types/C` 复制到 `/etc/dt/appconfig/types/C`。
2. 使用以下格式添加新的控件定义：

```
CONTROL  NewControl
{
TYPE            icon
CONTAINER_NAME Top
CONTAINER_TYPE  BOX
ICON        NewControlBitmap
PUSH_ACTION NewControlExecutable
}
```

操作（Action）和文件类型（File Types）有其特殊性，因为每种都有两部分组成，且每个都必须位于其自己的目录位置中。当我们在子面板上创建一个操作时，这些特殊性将变得清晰。以下是创建操作或文件类型定义的建议位置：

- 在 /etc/dt/appconfig/types 目录中创建一个全新的文件。该文件具有系统范围的影响。请记住，该文件必须以 .dt 扩展名结尾。
- 将 user-prefs.dt 从 /usr/dt/appconfig/types 复制到 /etc/dt/appconfig/types 目录，并在那里插入定义以用于系统范围。
- 将 user-prefs.vf 复制到 $HOME/dt/types 并在那里插入定义以用于单个用户。

典型的具有如下语法的操作：

```
ACTION    ActionName
{
   TYPE    type
   keyword value
   keyword value
}
```

例如，这里有一个 FrameMaker 操作：

```
ACTION    FRAME
{
   TYPE        COMMAND
   WINDOW-TYPE NO-STDIO
   EXEC-STRING /nfs/hpcvxmk6/usr/frame/bin/maker
}
```

典型的数据类型具有如下语法：

```
DATA_ATTRIBUTES       AttributesName
{
   keyword      value
   keyword      value
   ACTIONS      action, action
}
DATA_CRITERIA
{
   DATA_ATTRIBUTES AttributesName
   keyword        value
keyword value
}
```

请注意，所有定义都具有以下通用语法：
`KEYWORD value`

请注意，数据类型定义实际上分为两部分：属性部分和条件部分。数据类型定义的属性部分指定了数据类型的视觉外观；条件部分指定了数据类型的行为。

例如，这里有一个使用 FRAME 操作的 FrameMaker 文件的文件类型：

```
DATA_ATTRIBUTES       FRAME_Docs
                    {
                        DESCRIPTION This file type is for FrameMaker documents
                        ICON        makerIcon
                        ACTIONS     FRAME
                    }

DATA_CRITERIA         {
                        DATA_ATTRIBUTES_NAME FRAME_Docs
                        NAME_PATTERM      *.fm
                        MODE      f
                    }
```

你可以使用这些格式从头创建操作和文件类型。但是，创建操作的最简单方法是使用 **CreateAction** 工具。*CreateAction* 位于应用程序管理器（Applications Manager）中的桌面应用程序（Desktop Applications）文件夹中，它会向你展示一个填空对话框，引导你创建包含操作定义的 *action.dt* 文件。然后你可以将此文件移动到适当的目录中，以便你希望该操作具有的影响范围：*system-wide* 影响使用 */etc/dt/appconfig/types*；*individual users* 使用 *$HOME/.dt/types*。

##### 创建新图标和操作

创建图标是一项具有挑战性的任务。我们可以使用 Desktop_Apps 中的图标编辑器（Icon Editor）创建新图标，或者找一个我们喜欢的图片并使用它。在引入图片时需要注意的一点是，为了在面板上正确显示，它的大小不得超过 32x32 像素，否则只显示图标的一部分。在图标编辑器中查看图片可以显示图片的大小。你可能想搜索应用程序目录以查找有用的图标，或者从互联网上下载一个。

在整个示例中，我将使用随 HP-UX 一起提供的即时信息（Instant Information）软件。这是 CD 上的用户手册。其他应用程序软件也完全适用；只需确保你的路径与你使用的软件相对应。此外，我将使用一个虚构用户的家目录：/home/admin1。

1. 从 Desktop_Apps（HP-UX）、Desktoptools（AIX）或 Solaris 上的 Desktop_Tools 中调用图标编辑器，这些都在应用程序管理器中。
2. 选择 文件 -> 打开。
3. 输入路径或文件夹名称：/opt/dynatext/data/bitmaps。
4. 输入文件名称：logoicon.bm。
5. 选择 打开。

我们将看到图标，并且它确实为 32x32。现在我们需要将图标保存到我们自己的 .dt 目录中。

6. 选择 文件 -> 另存为。
7. 输入路径或文件夹名称：$HOME/.dt/icons。对于 admin1 用户，这将是 /home/admin1/.dt/icons。

如果我们全局执行此任务，我们会将此放在 /etc/.dt/app-config/types/C。

8. 保留文件名称不变。
9. 保存。

现在我们有图标了，我们需要创建一个操作文件和一个说明文件与之配套。

1. **使用你喜欢的文本编辑器**，输入以下内容：

```
 ACTION instinfo 
 {
 LABEL instinfo 
 TYPE COMMAND 
 WINDOW_TYPE NO_STDIO 
 EXEC_STRING /opt/dynatext/bin/dynatext 
 DESCRIPTION This action starts Instant Information 
 }
```

LABEL 是操作的名称，TYPE 是命令，WINDOW_TYPE 是 none（无标准输入/输出，即 NO_STDIO），因为该应用程序有自己的窗口；EXEC_STRING 是要执行的命令，而 DESCRIPTION 只是描述该操作的作用。确保 NO_STDIO 使用下划线而不是连字符，并且不要忘记最后的 }。我犯过这两个错误，然后花了大量时间试图弄清楚为什么操作看起来不存在，或者如果它出现了，为什么它不起作用。

2. **将此文件保存为** `$HOME/.dt/types/instinfo.dt`。对于 admin1 用户，这将是 `/home/admin1/.dt/types/instinfo.dt`。如果是全局配置，我们将文件保存为 `/etc/dt/appconfig/types/C/instinfo.dt`。

现在我们有一个操作了，我们需要创建一个说明文件。请注意，这是一个只包含这两行的新文件。此文件的内容无关紧要，但权限 *必须* 包含可执行权限。

3. 再次，**使用你喜欢的编辑器**，输入：

```
 ACTION instinfo 
 DESCRIPTION This action starts Instant Information 
 ```

4. **将此文件保存为** `$HOME/.dt/appmanager/instinfo`。对于 admin1 用户，这将是 `/home/admin1/.dt/appmanager/instinfo`。如果是全局配置，我们将文件保存为 **/etc/dt/appconfig/appmanager/instinfo**。

5. 按以下方式更改权限以包含执行权限：

   `chmod 555 $HOME/.dt/appmanager/instinfo`

现在是时候修改前面板以包含我们刚刚创建的图标和操作了。前面板文件 **dtwm.fp** 位于 **/usr/dt/appconfig/types/C** 目录中。由于我们不希望覆盖系统文件，我们需要将其本地复制，然后为我们自己修改它。

1. 将此文件复制到 **/$HOME/.dt/types/dtwm.fp**（针对 AIX 和 HP-UX）以及 **/$HOME/.dt/types/fp-dynamic/dtwm.fp**（针对 Solaris）。对于 admin 用户，这将是：
   `cp /usr/dt/appconfig/types/C/dtwm.fp /home/admin1/.dt/types/fp-dynamic/dtwm.fp`
   
   或者对于 Solaris：
   `cp /usr/dt/appconfig/types/C/dtwm.fp /home/admin1/.dt/types/fp-dynamic/dtwm.fp`

2. **使用你喜欢的编辑器**，修改本地的 **dtwm.fp** 文件。

   当我们查看该文件时，我们注意到它的顺序与前面板的显示顺序相同。时钟是文件中的第一个 CONTROL，也是前面板上的第一项。还注意到 POSITION_HINTS 是 1。日期是下一个，POSITION_HINTS 也是 2。我们要做的是将我们的新图标和操作放在 POSITION_HINTS 4，即 TextEditor CONTROL 之后。

3. 向下移动，越过以 ] 结尾的 CONTROL TextEditor，并在 CONTROL Mail 之前。此时，**请严格按照下方所示插入以下内容**。确保大写字母大写，小写字母不大写。

```
CONTROL Info
{
    TYPE            icon
    CONTAINER_NAME  Top
    CONTAINER_TYPE  BOX
```





```
POSITION_HINTS  5
ICON    logoicon.bm
LABEL   Instant Info
PUSH_ACTION    instinfo
}
```

4. 现在请小心：这部分比较棘手。接下来的项目需要重新编号它们的 `POSITION_HINTS`。但我们只重新编号接下来的八个项目，从“Mail”开始，到“Trash”结束。这些项目将从 5 到 12 变为 6 到 13。

5. 保存文件。

现在，让我们重启 Workspace Manager。如果我们做的一切都是正确的，我们将拥有一个新图标，点击该图标将显示即时信息，如图 14-9 所示。

6. 将鼠标放置在工作区的空白区域并按下鼠标右键。选择重启 Workspace Manager。

![](img/eff8b9287a5f38c5adf538f24aacf29e_955_0.png)

图 14-9 工作区菜单和新子面板及操作

在创建操作时要记住几件事：首先也是最重要的是，确保 `PUSH_ACTION` 和文件名相同。这种相似性是它们彼此发现对方的方式。确保该操作文件以 .dt 结尾，并确保该描述文件具有可执行权限。如果其中任何一项出错，该操作要么不起作用，要么不会显示。

为了避免大量输入，最简单的方法有时是复制一个现有的定义并将其插入到你希望新控件所在的位置，然后修改它。当你在控件定义列表中向下移动时，你实际上是在前面板从左向右移动（注意每个定义中的 `POSITION_HINTS` 值都在增加）。所以，如果你希望新控件位于前面板上日期的右侧，就在“date”下面的那一行插入控件，并在你的定义中添加一行 `POSITION_HINTS 3`；如果你希望新控件位于“date”的左侧，就在“date”上面的那一行插入控件，并将 `POSITION_HINTS` 设为 1。

新的控件定义可以位于控件定义列表中的任何位置。`POSITION_HINTS` 行可以防止它意外被移动到新的位置。仍然建议复制一个现有定义以避免额外输入；这降低了输入错误的几率。并且别忘了包含大括号。

### 使用不同的字体

虽然 CDE 字体是为可读性精心挑选的，但你可能有正当理由偏好其他字体。为了让你的字体在 CDE 环境中全局可用，请将其放入 `/etc/dt/app-defaults/Dstyle`，这样它们就会出现在样式管理器的字体对话框中。为了仅针对特定的 X 客户端应用程序使字体可用，请在该应用程序的 `app-defaults` 文件中指定字体。请记住，这会覆盖样式管理器中的字体。

字体对话框最多可以包含七种字体大小。你可以通过重置 `/etc/dt/app-defaults/Dstyle` 中 `Dstyle*NumFonts` 的值来减少这个数字；然而，你不能将其增加到七以上。

`Dstyle` 配置文件的字体对话框部分有七个 `SystemFont` 资源和七个 `UserFont` 资源。同样，你可以少于七种系统字体和七种用户字体，但不能超过这个数量。

要为特定应用程序指定字体，请使用该应用程序 `app-defaults` 文件中的 `*FontList` 资源。

要从个人用户层面修改字体资源，你可以使用前面“以其他方式更改前面板”部分中描述的 `EditResources` 操作。

### 更改登录消息

CDE 的一个优点是能够修改许多部分。你可以定制单独的登录账户或整个系统。通过定制登录屏幕，你可以向即将登录的用户显示他们正在访问的系统名称、公司标志以及个性化问候。这些修改发生在 `Xresources` 文件中：

1. 就像我们已经对 `dtwm.fp` 和 `dtwmrc` 文件所做的那样，我们需要将系统文件从 `/usr/dt/config/C` 复制到 `/etc/dt/config/C`，如下所示：

   `cp /usr/dt/config/C/Xresources /etc/dt/config/C/Xresources`

2. 进入你喜欢的编辑器并打开 Xresources 文件以便编辑。

3. 转到 GREETING 区域。在这里我们会找到以下行：

   `!!Dtlogin*greeting.labelString:    Welcome to %LocalHost%`
   `!!Dtlogin*greetingpersLabelString:  Welcome %s`

   第一行是初始登录屏幕上的消息。让我们修改它，使其欢迎我们来到我们的公司，ABC 公司：

   1. 移除注释符号。与我们大多数人习惯的 shell 脚本不同，Xresources 文件使用两个感叹号作为注释符号。移除 `!!`。
   2. 接下来，修改“`Welcome to %LocalHost%`”。`%LocalHost%` 变量会在登录屏幕上被替换为我们的系统名称。这一行应该如下所示：

      `Dtlogin*greeting.labelString:    ABC, Inc. Welcomes You to %LocalHost%`

   3. 接下来让我们更改第二行，以包含该系统专门服务于的部门：财务部。第二行显示的是当我们被提示输入密码时显示的内容。`%s` 变量是我们的用户名。这一行现在应该如下所示：

      `Dtlogin*greetingpersLabelString:    The Finance Department Welcomes %s`

   4. 保存文件。

4. 现在注销然后重新登录。我们应该能在登录屏幕上看到更改。我们不需要“重新加载”文件，因为注销并重新登录执行了这个操作。

#### 更改登录图片

如果你知道一件事，向登录屏幕添加新图片就很容易。文件必须是位图（.bm）或 pixmap（.pm）文件。位图文件是黑白的，而 pixmap 文件是彩色的。我尝试使用其他类型的图片（.gif 和 .jpg 格式），但它们只是不显示。好消息是，这些可以从其他系统或互联网导入供我们使用。为了简单起见，我们将使用系统上已有的一个。在 HP-UX 工作站上的 /usr/lib/X11/bitmaps 中找到了一个显示生日蛋糕的位图。但是，我也成功从互联网下载了花朵、大峡谷和乡村音乐歌手（注：Donna 写了这一章，而不是 Marty）的图片，并将它们放在了我的系统登录屏幕上。

1. 再次，让我们进入喜欢的编辑器并修改 `/etc/dt/config/C/Xresources`。

2. 转到 MISC 区域。在这里我们会找到以下行：
   ```
   !!Dtlogin*logo*bitmapFile:      < bitmap or pixmap file >
   ```

3. 删除前面的 !!，它们是注释标识符。

4. 用完整的文件路径位置将 < bitmap or pixmap file > 替换为位图文件的名称。这一行应该如下所示：
   ```
   Dtlogin*logo*bitmapFile:       /usr/lib/X11/bitmap/cake.bm
   ```

5. 保存文件。

6. 现在注销然后重新登录。我们应该能在登录屏幕上看到生日蛋糕。同样，我们不需要“重新加载”文件，因为注销并重新登录执行了这个任务。

既然我们已经看到如何轻松地在 CDE 中为最终用户进行一些简单的定制，我们应该能够利用这些知识，真正使他们的 CDE 环境成为一个高效且友好的工作场所。

### CDE - 高级主题

X、Motif 和 CDE 之间的关系

X、OSF/Motif 和 CDE 是使能框架技术。综合起来，X、Motif 和 CDE 构成了操作系统和硬件平台之上的三个图形层。

这些 GUI 层提供了一系列逐渐增加的易用性功能，这些功能作为缓冲层，将最终用户与操作系统层中“对用户不友好”的基于字符的界面隔离开来。

#### X Window 系统

X Window 系统由以下部分组成：

- **Xlib** - 用于编程窗口操作的低级库；图形的功能，如线条绘制和文本放置；控制显示输出、鼠标和键盘输入；以及应用程序的网络透明性。
- **X11 Intrinsics** - 用于编程小部件和设备（图形控制组件，如菜单、滚动条和按钮）的更高级库。
- **显示服务器** - 硬件特定的程序，每个显示一个，管理图形输入和输出。
- **客户端间通信约定 (ICCC)** - 规定 X 客户端程序如何相互通信的标准手册。
- **配置文件** - 一个指定启动的默认会话的配置文件（``sys.x11start``）以及另一个指定用于塑造 X 环境资源值的配置文件（``sys.Xdefaults``）。

通过这些机制，X 提供了基于网络导向、客户端/服务器、分布式计算范式的图形部分的标准。对 **Xlib** 和 **X11 Intrinsics** 的了解对于在 X 中编程以及在 Motif 级别编程很重要。然而，对于系统管理员来说，只要显示服务器正常工作且 X 客户端应用程序符合 ICC 标准，你就无需深入研究 X 层。CDE 使你可以将 X 视为“底层所有





#### Motif

Motif 由以下部分组成：

- mwm 窗口管理器 - 一个可执行程序，在 X 环境中提供基于 Motif 的窗口边框、窗口管理以及工作区菜单。
- Motif 小部件工具包 - 一组更高层的小部件和控件库，用于控制用户界面的图形组件。
- Motif 风格指南 - 一份定义 Motif 外观和行为的程序员手册。
- 配置文件 - 包含工作区菜单配置信息以及按键和按钮绑定的 system.mwmrc 文件。窗口管理器的资源位于 /usr/lib/X11/app-defaults 目录下的 mwm 中。

Motif 为最终用户提供了窗口管理器，为应用开发者提供了小部件工具包，并通过风格指南帮助开发者设计和构建符合 Motif 规范的应用程序。与 X 一样，系统管理员主要可以将 Motif 视为“程序员的东西”，即底层基础设施的一部分，并专注于开发适当的 CDE 配置文件。

#### CDE

如前所述，CDE 由以下部分组成：

- 工作区管理器 - 一个可执行程序，提供基于 Motif 的窗口边框、窗口管理、工作区菜单以及前面板。
- 文件管理器 - 一个通过直接操作图标化管理文件和目录的程序。
- 样式管理器 - 包含控制 CDE 环境元素（如工作区颜色和字体）对话框的容器。
- 帮助管理器 - 此程序提供关于 CDE 组件的上下文敏感帮助文本。
- 登录管理器 - 类似守护进程的应用程序，处理登录和密码验证。
- 会话管理器 - 处理保存和恢复用户会话的管理器。
- 应用程序管理器 - 在 CDE 环境中注册并跟踪应用程序的管理器。
- 配置文件 - 一大堆文件，其中大多数你可以避免处理（见下一节）。

CDE 还提供了许多基本的、增强最终用户生产力的应用程序。通常，CDE 提供一个图形环境，用户或作为系统管理员的你可以在其中整合完成工作所需的软件工具。

### X、Motif 和 CDE 配置文件

X、Motif 和 CDE 都使用配置文件来塑造其外观和行为。外观和行为的元素（如前景色、键盘焦点策略和客户端装饰）是资源，可以通过适当配置文件中的值进行控制。在 X、Motif 和 CDE 中，“资源”一词具有特殊含义。它指的既不是模糊的自然资源，也不是通用的系统资源，而是外观和行为中较为具体的元素。例如，前景色资源、keyboardFocusPolicy 资源和 clientDecoration 资源。例如，前景色可以是黑色，键盘焦点策略可以是显式的，客户端装饰可以是 plus-title（仅标题栏）。这些将在某个适当的配置文件中显示如下：

```
*foreground: black
*keyboardFocusPolicy:explicit
*clientDecoration: +title
```

这些资源出现在哪个配置文件中，取决于期望影响范围（系统级还是单个用户）以及正在使用的图形界面层级（X、Motif 或 CDE）。

#### X 配置文件

X 窗口系统具有以下配置文件：

- sys.X11start
- sys.Xdefaults
- system.mwmrc
- X*screens
- X*devices
- X*pointerkey

按照惯例，这些文件位于 /usr/lib/X11 目录中；不过，我注意到许多系统已移除了此目录，并将许多与 X 相关的文件移至系统的其他位置。此外，每个 X 客户端应用程序都有自己的 app-defaults 配置文件，同样按照惯例，位于 /usr/lib/X11/app-defaults 目录中。尽管上面列出了六个文件，但除非你正在为多显示器屏幕（X*screens）、多输入设备（X*devices）或仅键盘指针导航（X*pointerkey）配置工作站，否则通常只需处理 sys.x11start、sys.Xdefaults 和 system.mwmrc 即可。

sys.x11start 文件是在 CDE 出现之前用于启动 X 和 X 客户端的脚本。系统管理员或熟练用户会修改 sys.x11start，以便适当混合的 X 客户端能够“自动”启动。sys.Xdefaults 文件在 X 启动时被读取，以获取各种外观和行为资源的值。对 sys.Xdefaults 的修改确保了 X 环境和客户端具有适当的外观和行为。system.mwmrc 包含工作区菜单以及按钮和按键绑定的配置。system.mwmrc 也被 Motif 版本 system.mwmrc 所取代。

#### Motif 配置文件

Motif 仅向 X 的列表中添加了一个新的配置文件：system.mwmrc。

按照惯例，此文件保存在 /usr/lib/X11 中的 X 配置文件目录中。实际上，这个文件并不是新的；它是 system.mwmrc 的 Motif 版本，在 Motif 环境中简单地取代了 system.mwmrc。

如果说 X 将网络和客户端间通信标准引入图形用户界面，那么 Motif 则带来了外观和行为标准，该标准最初定义在 IBM 的系统应用程序架构通用用户访问（SAACUA）中，构成了大多数基于 PC 的 GUI 的基础。因此，按钮和滚动条具有定义的外观和行为，双击始终触发默认操作。

从程序员的角度来看，Motif 小部件工具包相比在“原始” X 中进行编程是一个巨大的进步。从用户或系统管理员的角度来看，Motif 用户环境与 X 环境大致相同，只是 mwm 窗口管理器被 Motif 窗口管理器所取代。

#### CDE 配置文件

可以指出超过 80 个文件，它们以某种方式有助于配置 CDE 的某个方面。按照惯例，这些文件位于 /usr/dt 目录中。然而，如果你从这个列表中移除以下文件：

- 配置 CDE 应用程序而非环境本身的文件
- 建立默认操作和数据类型定义的文件（尽管你在单独的文件中创建自己的定义，但你从不修改它们）
- CDE 工作文件，不应进行自定义
- 更适当地与配置 CDE 底层 UNIX、X 和 Motif 环境（包括各种 shell 环境）相关的文件

那么 CDE 大约有 19 个配置文件，如表 14-1 所示。

### 表 14-1 CDE 配置文件

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| *.Xauthority | *.Xdefaults | *.dprofile | dtwm.fp | dt.wmrc | sys.dprofile | sys.dwmc | sys.font | sys.resources | sys.sessions | Xaccess | Xconfig | Xfailsafe | Xreset | Xresources | Xservers | Xsession | Xsetup | Xstartup |

### 表 14-2 CDE 配置文件的影响范围

表 14-2 根据 CDE 配置文件的内容及其影响范围进行了组织：

| 配置文件的性质 | 系统级影响 | 用户个人影响 |
|---|---|---|
| 环境变量 | sys.dprofile | .dprofile |
| | Xconfig | |
| | Xsession | |
| 外观和行为资源 | sys.resources | .Xdefaults |
| | Xconfig | |
| | Xresources | |
| | sys.fonts | |

尽管如此，配置 CDE 并不是你可以在没有一些准备工作和明确目标的情况下就随便动手的事情。所有 CDE 配置文件都有相当完善的注释，因此一个好的第一步是打印出你想要修改的那些文件。

虽然 19 个配置文件仍然很多，但不要被这个数字吓到。你不需要修改其中许多，并且可以忽略你只需修改一次然后遗忘的几个。你只需要深入理解以进行定期修改的一两个文件，也许是一个用于自定义操作和数据类型的系统级 *.dt 文件，或者如果你的工作需要经常修改前面板，可能是 dtwm.fp。





##### 配置文件特性

| 配置文件特性 | 系统级影响 | 用户个人影响 |
|---|---|---|
| 文件类型与操作定义 | misc\*.dt 文件 | user-prefs.dt |
| 登录时客户端启动 | sys.sessions | .Xsession |
|  | Xstartup | sessionetc |
|  | Xsession |  |
|  | Xreset |  |
|  | Xfailsafe |  |
| 工作区管理器与前面板 | sys.dtwmrc | dtwmrc |
|  | dtwm.fp | user-prefs.fp |
| 客户端/服务器与访问 | Xaccess | .Xauthority |
|  | Xservers |  |

文件 **sys.dtwmrc** 控制工作区管理器的系统级配置。这包括以下所有内容：

- **工作区菜单**：当鼠标指针位于工作区背景上并按下鼠标按钮 3 时显示的菜单。
- **按钮绑定**：定义当鼠标指针位于特定区域（框架、图标、窗口或根）上时，按下或释放特定鼠标按钮所执行的操作。
- **键盘绑定**：定义当鼠标指针位于特定区域（框架、图标、窗口或根）上时，按下特定按键或按键序列所执行的操作。

与 X 或 Motif 的配置文件不同，**sys.dtwmrc** 不控制以下配置元素：

- **前面板**：通常位于工作区底部的方框，包含常用指示器和常用图形控件，包括一个六按钮工作区切换器。
- **Slidewp 子面板**：从前面板各种位置滑出的菜单，用于在不占用更多屏幕空间的情况下提供更多功能。

相反，为了避免配置文件过大和过于复杂，这些元素在 CDE 中被分离到自己的配置文件中，即 dtwm.fp。

一些前面板配置元素，如工作区数量及其在工作区切换器中的排列，通过 **sys.resources**、**dt.resources** 或 **.Xdefaults** 文件中的资源进行控制。与其他工作区管理器配置文件类似，**sys.dtwmrc** 可以复制到用户的家目录，实际上是 $HOME/.dt 中的 **dtwmrc**，并对其进行修改，以便在 **sys.dtwmrc** 的系统级配置之外个性化用户的环境。

**sys.resources** 文件是你可能只需修改一次就再也不会修改的文件之一。**dt.resources** 文件是你永远不需要修改且可以忽略的文件。**\.Xdefaults** 文件是你或你的用户可能偶尔会修改的文件。

**sys.resources** 文件放置了你希望在全新首次登录 CDE 的用户登录时生效的任何非默认资源的位置。例如，作为系统管理员，你可能希望你的用户拥有带有预命名工作区、特殊颜色、特定字体或特定位置应用程序窗口的 CDE 前面板。首次登录后，**sys.resources** 将被忽略，转而采用 **dt.resources**。该文件 **dt.resources** 位于 $HOME/.dt/sessions/current（当恢复主会话时位于 $HOME/.dt/sessions/home），并由 CDE 自动创建。你可以将其视为 CDE 的工作文件并忘记它。**\.Xdefaults** 是你或终端用户列出特定于用户个人 CDE 环境的 X 资源的地方。**sys.resources**、**dt.resources** 和 **\.Xdefaults** 包含资源及其值的列表。

**sys.sessions** 文件控制新用户首次登录 CDE 时启动哪些客户端。**dt.sessions** 文件对于 **sys.sessions** 的作用类似于 **dt.resources** 对于 **sys.resources** 的作用。

配置 CDE 为用户启动特定应用程序可能是高效的。你会在 **sys.sessions** 中指定这些应用程序。当新用户首次登录时，CDE 环境将包含指定的客户端。在通过注销结束此首次会话时，剩余的客户端将被记录在 $HOME/.dt/sessions/current（当恢复主会话时位于 $HOME/.dt/sessions/home）中，供 CDE 使用。

`sys.dttprofile` 文件是一个模板，在首次登录时自动复制到每个新用户的家目录中，命名为 `.dttprofile`。在 CDE 环境中，`sys.dttprofile` 取代了 `.profile` 或 `.login`（尽管通过在 DTSOURCEPROFILE=true 前面删除 # 注释符号，可以在 `.dttprofile` 中源加载 `.profile` 或 `.login`）。`.dttprofile` 文件保存了个人环境变量，这些变量在基于字符的环境中通常位于 `.profile` 或 `.login` 中。使用 `.dttprofile` 可以避免终端 I/O 命令对 CDE 图形环境造成的干扰。

CDE 登录管理器 `dttlogin` 将以下环境变量预设为默认值：

| 变量 | 描述 |
| :--- | :--- |
| DISPLAY | 本地显示器的名称 |
| EDITOR | 默认文本编辑器 |
| HOME | 用户在 `/etc/passwd` 中指定的家目录 |
| KBD_LANG | 键盘的当前语言 |
| LANG | 当前 NLS 语言 |
| LC_ALL | LANG 的值 |
| LC_MESSAGES | LANG 的值 |
| LOGNAME | 用户在 `/etc/passwd` 中指定的登录名 |
| MAIL | 邮件的默认文件（通常是 /var/mail/$USER） |
| PATH | 搜索文件和应用程序的默认目录 |
| USER | 用户名 |
| SHELL | 在 `/etc/passwd` 中指定的默认 shell |
| TERM | 默认终端仿真 |
| TZ | 生效的时区 |

对这些默认值的修改应位于每个用户的 `.dttprofile` 中。可以根据工作场景的需要添加额外的环境变量来塑造用户环境。只要注意不要使用引起任何终端 I/O 的命令即可。

与 `.dttprofile` 类似，`$Xsession` 是一个设置用户环境变量的 shell 脚本。`Xsession` 中的环境变量适用于整个系统。`.dttprofile` 中的环境变量仅适用于用户的个人环境。此外，由于登录管理器在 X 服务器启动后运行 `Xsession`，**Xsession** 中的变量对 X 服务器不可用。**Xsession** 中通常设置的变量包括以下内容：

| 项目 | 描述 |
| :--- | :--- |
| **EDITOR** | 默认文本编辑器。 |
| **KBD_LANG** | 键盘的语言（通常设置为 `LANG` 的值）。 |
| **TERM** | 默认终端仿真。 |
| **MAIL** | 邮件的默认文件，通常是 `/var/mail`$USER。 |
| **DTHELPISEARCHPATH** | 搜索 CDE 帮助文件的位置。 |
| **DTAPPSEARCHPATH** | 搜索与 CDE 应用程序管理器注册的应用程序的位置。 |
| **DTDATABASESEARCHPATH** | 搜索额外操作和数据类型定义的位置。 |
| **XMICONSEARCHPATH** | 搜索额外图标的位置。 |
| **XMICONBMSEARCHPATH** | 同上。 |

作为一个例子，假设你是位于单一站点的几个混合工作站和 X 终端集群的系统管理员。像往常一样，大多数用户已经习惯使用某些文本编辑器。有些人喜欢 `vi`，另一些人偏爱 `emacs`，还有两三个人在没有 `dmx` 的情况下寸步难行。为每个用户提供其喜欢的文本编辑器的简单方法是在个人的 **.cprofile** 文件中将 **EDITOR** 变量重置为相应的值。

**Xconfig** 包含控制 **dtlogin** 行为的资源，并且它还提供了一个位置来指定你创建的其他 **dtlogin** 配置文件的位置。**Xconfig** 文件在系统范围内工作，因此它是你只需修改一次然后就可以忘记的文件之一。登录期间运行 **Xconfig** 时，会引用多个 CDE 配置文件：**Xaccess**、**Xservers**、**Xresources**、**Xstartup**、**Xsession**、**Xreset** 和 **Xfailsafe**。与 **Xconfig** 本身一样，这些文件中的大多数都是你在安装 CDE 时修改一次，除非网络拓扑发生变化，否则你永远不会再处理它们。

**Xaccess**，顾名思义，是一个远程显示访问控制文件。**Xaccess** 包含允许或拒绝 XDMCP 连接到本地计算机的主机名列表。例如，当 X 终端请求登录服务时，dtlogin 会参考 **Xaccess** 文件来确定是否应授予服务。

**Xservers** 文件的主要用途是列出 dtlogin 负责管理的本地系统上的显示屏幕。dtlogin 读取 **Xservers** 文件并为其中列出的每个显示启动一个 X 服务器。然后它启动一个子 dtlogin 进程来管理该服务器并显示登录屏幕。请注意，dtlogin 仅在本地工作；dtlogin 无法在远程系统或 X 终端上启动 X 服务器。对于远程显示服务器，必须使用其他机制来启动服务器，该服务器随后使用 X 显示管理控制协议（XDMCP）向 dtlogin 请求登录屏幕。

**Xservers** 文件是另一种你可能最初会花些时间处理，但除非你的网络拓扑发生变化，否则再也不会处理的文件。你何时使用 **Xservers**？当显示不匹配默认配置时。默认配置假设每个系统都有一个位图显示并且是系统控制台。X 终端、多个显示器（头）、多个屏幕和 Starbase 应用程序都需要在 **Xservers** 文件中配置相应的行。

**Xresources** 文件包含控制登录屏幕外观和行为的资源列表。在你用公司的徽标替换 CDE 徽标并更改字体和颜色后，你很可能再也不会处理 **Xresources**（除非你的公司更改其徽标）。

**Xstartup** 是由登录管理器执行的全系统配置文件，登录管理器从中接收多个环境变量：

| 变量 | 描述 |
| :--- | :--- |
| DISPLAY | 本地显示器的名称。 |
| USER | 用户的登录名。 |
| HOME | 用户的家目录。 |
| PATH | Xconfig 中 systemPath 资源的值。 |
| SHELL | Xconfig 中 systemShell 资源的值。 |
| XAUTHORITY | 用于访问权限的文件。 |
| TZ | 本地时区。 |




由于 **Xstartup** 可以在系统范围内执行脚本并启动客户端，因此它与 `sys.sessions` 类似。区别在于 **Xstartup** 是以 root 身份运行的。因此，对 **Xstartup** 的修改应仅限于挂载文件系统之类的操作。

**Xreset** 是 **Xstartup** 的系统级配套脚本。它以 root 身份运行，并基本上撤销了 **Xstartup** 所做的更改。

`Xfailsafe` 文件包含对标准故障排除会话的定制。故障排除会话提供了一种方式来纠正因登录和会话配置文件中的错误而导致的 CDE 会话不当问题。因此，`Xfailsafe` 是用户永远不会使用的东西，但您可以进行一些明智的定制，让事情变得更容易。

`.sessionetc` 文件位于用户的 `.dt/sessions` 目录中，并个性化该用户的 CDE 会话。`.sessionetc` 处理启动额外的 X 客户端（如 `sys.session`），但它是针对每个用户而非系统范围的。虽然 `dl.session` 也是按用户启动客户端，但这些客户端属于默认或当前会话。`dl.session` 位于 `.dt/session/current .sessionetc`，而 `.sessionetc` 位于 `.dt/session`，并且应只包含那些不会被自动恢复的客户端。通常，这些是未正确设置 `WM_COMMAND` 的客户端，因此会话管理器无法保存或恢复它们；因此，需要在 `.sessionetc` 中重启它们。

`sys.font` 文件包含系统范围的默认会话字体配置。这些默认字体基于可用性研究，因此 `sys.font` 是一个您可能永远不会修改的文件。但是，如果您遇到需要系统范围的不同字体组合的情况，这就是您更改它们的地方。请注意，`sys.font` 中提到的字体资源和值必须与 `/usr/dt/app-defaults/C/Dtstyle` 文件中指定的默认字体资源完全匹配。

CDE 有许多指定 CDE 动作和数据类型定义的文件。所有这些文件都以文件扩展名 `*.dt` 结尾（`A *.dt` (“desk top”) 包含数据类型和动作定义。默认的 `*.dt` 文件位于 `/usr/dt/appconfig/types/C`，并在系统范围内起作用。类似地，`user-prefs.dt`（其主副本也位于 `/usr/dt/appconfig/types/C`）用于个人用户级别。

`.Xauthority` 文件是包含需要授权机制才能连接到服务器的客户端所需的授权信息的用户特定配置文件。

##### CDE 配置文件位置

CDE 查找特定配置文件的位置取决于配置文件的性质，主要是这些文件配置的内容及其影响范围。表 13-3 根据文件内容的性质显示了系统和用户配置文件的位置。

对于表 14-3 中列出的每个默认系统范围文件位置，都存在一个对应的自定义系统范围配置文件位置。这些自定义文件应位于 /etc/dt 下的适当子目录中。基本过程是将您需要定制的文件从 /usr/dt/something 复制到 /etc/dt/something，然后在那里进行修改。例如，若要更改 Xresources 中的默认徽标，请将 /usr/dt/config/C/Xresources 复制到 /etc/dt/config/C/Xresources，打开 /etc/dt/config/C/Xresources，并进行您的更改。

**表 14-3 CDE 系统和用户配置文件**

| 配置文件性质 | 系统范围影响 | 用户个人影响 |
| :--- | :--- | :--- |
| 环境变量 | /usr/dt/config/ | $HOME/ |
| 外观和行为资源 | /usr/dt/config/C /usr/dt/app-defaults/C | $HOME/dt/ $HOME/dt/sessions/current/ $HOME/dt/sessions/home/ |
| 文件类型与动作定义 | /usr/dt/config/types/C | $HOME/dt/types |
| 登录时的客户端启动 | /usr/dt/config/ /usr/dt/config/C | $HOME/dt/session/ $HOME/dt/session/current/ $HOME/dt/session/home/ |
| 工作区管理器 | /usr/dt/config | $HOME/dt/ |

这是一个重要的点。位于 /usr/dt 下的文件被视为 CDE 系统文件，并将在更新期间被覆盖。因此，您在那里所做的任何定制都将丢失。请在 /etc/dt 及其子目录中对系统范围配置文件进行所有修改。

##### 配置文件如何协同工作

根据到目前为止所涵盖的内容，您可能已经正确地得出结论，即 CDE 配置文件不是在没有计划的情况下随意修改的东西——而是一个深思熟虑的计划。您可能已经弄清楚，您想要配置的元素及其影响范围决定了您修改哪个配置文件。

例如，如果您想设置环境变量，您可以选择四个配置文件：sys.d/profile、Xconfig、Xsession 和 .d/profile。但如果您只想设置影响特定用户的环境变量，您的选择立即缩小到单个文件，即 .d/profile。

现在，剩下的谜题部分就是理解 CDE 读取其配置文件的顺序。当某个配置元素（环境变量、资源、动作或数据类型）被指定两次但值不同时，您显然希望使用正确的值，忽略错误的值。

适用以下规则：

-   对于环境变量，使用最后指定的值。
-   对于资源，使用最后指定的值。然而，这受具体性影响。因此，*emacs*f*oreground 优先于仅为 *emacs* 客户端的 *f*oreground，无论资源的出现顺序如何。
-   对于动作，使用第一个指定的。
-   对于数据类型，使用第一个指定的。

表 14-4 说明了当 CDE 在其配置文件中读取多个配置元素规范时使用哪个规范：

**表 14-4 CDE 用于配置的内容**

| 配置元素 | 使用的元素 |
| :--- | :--- |
| 资源 | 最后遇到的或最具体的 |
| 环境 | 最后遇到的 |
| 动作 | 首先遇到的 |
| 文件类型 | 首先遇到的 |

用范围术语来说，用户配置文件覆盖系统范围配置文件。仅查看系统范围配置文件的优先顺序，**/etc/dt** 中的文件优先于 **/usr/dt** 中的文件，因此全局自定义配置优先于 CDE 默认配置。并且 **$HOME/.dt** 文件优先于 **/etc/dt** 中的文件。

对于资源（用于指定 GUI 的外观和行为），CDE 根据以下优先级设置值：

1.  **命令行** - 当您从命令行启动客户端时，命令行上列出的选项具有最高优先级。
2.  **Xresources**、**.Xdefaults**、**dt.resources**、**sys.resources** - 当 CDE 启动时，它读取这些资源配置以确定用于会话的 X 资源的值。
3.  **资源管理器** - 属性 **RESOURCE_MANAGER** 中已有的资源可能会影响刚刚启动的应用程序。
4.  **app-defaults** - 指定与内置资源值不同的“默认”资源值。
5.  **内置默认值** - “硬编码”的默认资源具有最低优先级。

特定的资源规范优先于一般的资源规范。例如，假设您希望在文本输入区域使用某种字体。您可以在个人的 **.Xdefaults** 文件中正确指定一个 *FontList* 资源，结果却被 **app-defaults** 文件中的 **XmText**FontList 覆盖。虽然 **app-defaults** 的优先级低于 **.Xdefaults**，但那里设置的具体资源规范更具体，因此它具有优先级。

对于环境变量，CDE 根据以下优先级设置值：

1.  **$HOME/.dtdprofile** - 用户特定变量具有最高优先级。
2.  **/etc/dt/config/C/Xsession** - 未被 X 服务器读取的自定义系统范围变量。
3.  **/etc/dt/config/C/Xconfig** - 被 X 服务器读取的自定义系统范围变量。


### 优先级说明

- 4. /usr/dt/config/C/Xsession - 默认系统级变量，X 服务器不读取。
- 5. /usr/dt/config/C/Xconfig - 默认系统级变量，由 X 服务器读取。
- 6. /usr/dt/bin/tdlogin - 内置默认变量具有最低优先级。

对于数据类型和动作定义，CDE 按照以下优先级查找 `.dt` 文件：

- 1. $HOME/.dt/types
- 2. /etc/dt/appconfig/types/C
- 3. /usr/dt/appconfig/types/C

请记住，对于数据类型或动作，CDE 使用的是它找到的第一个值。如果你无法让文件类型或动作正常工作，请检查文件中是否有更高优先级的重复条目。还要注意，环境变量 `DTDATABASESEARCHPATH` 可以设置在 `/etc/dt/config/Xsession` 或 `$HOME/.dt/profile` 中，以添加 CDE 可以搜索文件类型和动作定义信息的目录。

##### 指定外观和行为

你只需要知道两个技巧来在配置文件中指定外观和行为资源。第一个是正确指定资源及其值。第二个是在正确的配置文件中指定资源和值。

两个注意事项涉及颜色和字体。CDE 样式管理器提供了修改颜色和字体的图形界面。但是，如果你直接指定应用程序的颜色或字体，该指定将覆盖样式管理器管理该资源的能力。直接指定颜色或字体的典型方式包括：

- 在命令行上输入指定作为启动选项。
- 在应用程序的 app-defaults 文件中包含指定。
- 使用 **xrdb** 实用工具将资源添加到应用程序的资源数据库中。

##### CDE 启动时的事件序列

以下部分详细描述了用户登录 CDE 时发生的事情。在这个特定的描述中，假设一个分布式拓扑，如无盘集群。描述从启动主机系统和节点开始（步骤 1）。到步骤 4，每个节点上的 X 服务器正在运行，并显示登录屏幕。到步骤 6，用户已登录。到步骤 11，会话管理器正忙于重建用户会话。

1. **dtlogin** 可执行文件作为 **init** 进程的一部分启动，该进程发生在主机机器和每个集群节点的系统启动序列期间。
2. **dtlogin** 读取 **/usr/dt/config/Xconfig** 以获取配置登录进程所需的资源列表。这是 **dtlogin** 首次了解 **Xaccess**、**Xservers**、**Xresources**、**Xstartup**、**Xsession** 和 **Xreset** 等文件的地方，并获取一些外观和行为资源的值。
3. **dtlogin** 读取 **/usr/dt/config** 中的两个文件：
    - **Xservers** 或由 **Xconfig** 中的 **Dtlogin\*servers** 资源设置标识的文件。
    - **Xresources** 或由 **Xconfig** 中的 **Dtlogin\*resources** 资源设置标识的文件。
4. **dtlogin** 为每个本地显示启动一个 X 服务器和一个子 **dtlogin**。
5. 每个子 **dtlogin** 调用 **dtgreet**（登录屏幕）。
6. 当登录名和密码通过验证后，子 **dtlogin** 将某些环境变量设置为默认值。
7. 子 **dtlogin** 运行 **/usr/dt/config/Xstartup**。
8. 子 **dtlogin** 运行 **/usr/dt/config/Xsession**。
9. Xsession 运行 dthello（版权屏幕）。
10. Xsession 读取 $HOME/.dtprofile，设置任何额外的环境变量或覆盖之前由 dtlogin 设置的变量。
11. 子 dtlogin 调用会话管理器 dtsession。
12. dtsession 恢复相应的会话。例如，要恢复当前会话，dtsession 读取 $HOME/.dt/sessions/current 中的 dtresources 和 dt.session。

退出登录时，过程相反。会话被保存，dtlogin 运行 /usr/dt/config/Xreset。在 Xreset 完成后，dtlogin 再次显示登录屏幕，如步骤 4 所示。

##### CDE 与性能

CDE 不是一个单体应用程序：它是分层在操作系统、X 窗口系统和 Motif 之上的一组组件。每个底层在进入 CDE 或其他客户端之前都会占用一部分 RAM。由于这些层的底层性质，它们使用的 RAM 几乎永远无法通过交换到磁盘来回收。

在某些情况下，操作系统开销和用户应用程序需求限制了对图形用户界面可用的 RAM 数量，仅略多到足以运行 Motif 等窗口管理器。由于 CDE 工作区管理器和 Motif 窗口管理器消耗的 RAM 大致相同，用户可以在基本上不增加额外 RAM 成本的情况下，享受带有 CDE 多个工作区附加值的丰富图形环境。

##### 提高性能的策略

除非你的所有用户都拥有 RAM 加载的强劲系统，否则你需要花时间制定性能策略。如果你将性能视为钟形曲线，满足感位于前缘。你的性能策略应尽可能让所有用户保持在边缘。

可能最合乎逻辑的方法是从最小开始并逐渐扩展。换句话说，在所有系统上从最小的用户环境开始。逐渐添加软件组件，直到你或你的用户开始注意到性能下降。然后稍微后退一点。这种可能需要数周甚至更长时间来评估，因为你在添加组件时，你的用户需要花几天时间实际在该环境中工作，以确定你的更改对系统性能和他们的挫折感的影响。

CDE 中最消耗 RAM 的部分是工作区管理器、会话管理器和文件管理器。工作区管理器开销大，因为它的一部分始终在 RAM 中（假设你在移动窗口并切换工作区）。CDE 工作区管理器并不比 Motif 窗口管理器更昂贵；如果你想要 GUI，这只是你必须支付的价格。会话管理器仅在退出和登录时开销大，因为它保存和恢复会话。其余时间，会话管理器处于休眠状态并被交换出 RAM。在一天结束时保存当前的工作会话是很好的，但如果你想提高登录和退出的性能，这是可以考虑放弃的功能。文件管理器开销大，因为它定期唤醒并跳入 RAM 以检查文件系统状态并更新其文件管理器窗口。当它跳入 RAM 时，它将其他内容推出，例如，也许是你正在使用的桌面出版程序。

这里有一些其他你可能觉得有用的想法：

- **终端模拟器** **xterms** 比 **dtterms** 稍少消耗 RAM。除非你需要 **dterm** 的块模式功能，否则 **xterm** 可能是终端模拟器的更好选择。
- **自动保存** 一些应用程序会自动在定期间隔保存数据。虽然此功能可能有益，但你需要考虑其对性能的影响。如果应用程序对你的用户工作至关重要，那么没问题，但如果不是，你可能想要禁用自动保存功能。

##### 滚动缓冲区

终端模拟器中的大滚动缓冲区可以带来极大的便利，但它们也会占用大量 RAM。即使中等大小的滚动缓冲区，当乘以三到四个终端模拟器时，也会消耗大量 RAM。

##### 背景位图

避免使用大位图；它们会增加 X 服务器的大小。特别避免在会话内频繁切换大位图。如果你正在寻找新的背景，确保在你找到想要的并将其包含在正确的 **sessionetc** 文件后，重启 X 服务器。最有效的位图是可以重复平铺背景的小位图。

##### 前面板

重新配置前面板以最小化按钮数量。仅保留满足用户需求的数量。此策略减少了 RAM 中工作区管理器的大小，并加快登录和退出的速度。

##### 路径名

只要可能，请使用绝对路径名进行位图指定。虽然这种方法降低了系统的灵活性，但它加快了访问时间。

##### 结论

默认的 CDE 即可使用，但鉴于其强大的功能和灵活性，你最终会想要针对用户的工作环境和最佳性能自定义 CDE 环境。花时间去制定你需要进行更改的好主意，更改的顺序，以及确切在哪里进行更改。通过这样做，CDE 的所有强大功能和灵活性将向你敞开。





## 附录 A
### 虚拟分区在线手册页

本书的每一章都包含了用于操作虚拟分区的命令。各章节中提供了许多示例。此外，快速参考撕下卡上列出了所有命令的摘要和示例。然而，没有任何内容能像命令手册页中那样提供详尽的命令细节。虚拟分区命令的手册页编写得非常规范且详尽。本附录仅包含虚拟分区命令的手册页。以下是命令列表：

- **vparboot** - 引导（启动）虚拟分区。
- **vparcreate** - 创建新的虚拟分区。
- **vparmodify** - 修改现有的虚拟分区。
- **vparremove** - 移除（删除）现有的虚拟分区。
- **vparreset** - 向虚拟分区发送 TOC 或硬复位。
- **vparresources** - 提供关于虚拟分区及其资源的描述。
- **vparstatus** - 显示虚拟分区和可用资源信息。
- **vpartition** - 显示关于 vPar 命令行的信息。
- **vparutil** - 处理 vPar 中磁盘的 SCSI 信息。

## vparboot

vparboot - 引导（启动）虚拟分区。

**vparboot (1M)**

### 名称
vparboot - 引导虚拟分区

### 概要
```
vparboot -p vp_name [-b kernel_path] [-o boot_opts] [-B boot_addr]
vparboot -p vp_name -i ignite_kernel
```

### 描述
vparboot 命令使虚拟分区监视器引导指定的虚拟分区。监视器必须处于运行状态。该虚拟分区必须存在于监视器配置中，并且处于 Down（关闭）状态。例如，未运行状态。因此，无法使用此命令引导当前分区。执行该命令的分区称为当前分区。

只有超级用户才能执行 vparboot 命令。

### 选项
'vparboot' 识别以下命令行选项和参数：

- **-p vp_name**  
  指定要引导的虚拟分区的唯一名称。该虚拟分区必须存在于监视器的数据库中，必须处于 Down 状态，并且必须已配置引导设备。必需。

- **-b kernel_path**  
  指定虚拟分区可引导内核的绝对路径。例如，如果在 ISL 提示符下的非分区系统启动字符串为：
  `ISL> hpx -is /stand/vmunix`
  
  则 kernel-path 是该字符串中的 `/stand/vmunix` 部分。

  如果省略此选项，则值取自虚拟分区创建或最近修改期间指定的任何 `-b kernel_path`，或者如果从未指定 `-b kernel_path`，则默认为 `/stand/vmunix`。

- **-o boot_opts**  
  指定引导虚拟分区时应用的命令行选项。例如，如果在 ISL 提示符下的非分区系统启动字符串为：
  `ISL> hpxx -15 /stand/vmunix`
  
  在这种情况下，boot_opts 字符串将为 `-15`。
  
  请注意，如果字符串中包含任何空白字符，则必须引用该字符串。

  有关受支持引导选项字符串的完整列表，请参阅虚拟分区管理指南以及标题为“监视器 Shell 命令”的章节。

  如果省略 `-o` 选项，则值取自虚拟分区创建或最近修改期间指定的任何 `-o boot_opts`，或者如果从未指定 `-o boot_opts`，则为空字符串。

- **-B boot_addr**  
  指定读取虚拟分区内核镜像的设备。它必须是以下三种形式之一：

  - `bct[0] | pri(mary)` （不区分大小写）。如果省略 -B 选项，这是默认值。vparboot 尝试从之前使用 BOOT 属性配置的设备引导 vp_name。如果没有设备以这种方式配置，则视为错误。
  - `alt[ernate][boot]` （不区分大小写）。vparboot 尝试从之前使用 ALTBOOT 属性配置的设备引导 vp_name。如果没有设备以这种方式配置，则视为错误。
  - **从硬件路径引导：** 假设任何其他字符串都是期望的引导设备的硬件路径（例如，10/0）。vparboot 不检查此类规范的任何部分。如果它不是正确的路径，路径不存在，虚拟分区不拥有该路径处的设备，或者该路径处没有可引导设备，则命令会以错误失败，或者引导尝试失败而没有错误指示。

- **-I ignite_kernel**  
  指定冷安装内核的路径，例如 `/opt/ignite/boot/WINSTALL`。此命令形式用于在虚拟分区上冷安装 HP-UX 实例。通常，这是在新创建的虚拟分区上完成的，该分区拥有完全未写入的磁盘。但是，它也可以用于在现有实例上冷安装 HP-UX。

  ignite_kernel 可以位于当前虚拟分区（运行 vpboot 的分区）或任何其他可从该分区访问的网络化系统或虚拟分区上。ignite_kernel 的语法为：
  `[Server name or IP addr,]cold-install_kernel`

  如果 cold-install_kernel 以斜杠“/”开头，则表示指定了绝对路径，vpboot 将在那里查找它。如果 cold-install_kernel 不以“/”开头，则默认路径 `/opt/ignite/boot/` 会前置到 cold-install_kernel 之前。

  如果没有指定服务器名称或 IP 地址，vpboot 将从当前虚拟分区的文件空间加载冷安装内核。否则，命令将从指定服务器的文件空间加载。逗号是服务器名称语法的一部分，必须使用。

### 返回值
vpboot 命令以以下值之一退出：
- 0 成功完成。
- 1 发生了一个或多个错误条件。

### 示例

引导名为 Oslo 的虚拟分区
```
vpboot -p Oslo
```

引导虚拟分区 Bergen，指定备用内核
```
vpboot -p Bergen -b /stand/vmunix_debug
```

从远程服务器上的文件冷安装虚拟分区 Trondheim
```
vpboot -p Trondheim -i mysys.myserver.mysdomain.com:/mypath/mysinst
```

从当前虚拟分区上的默认路径 /opt/ignite/boot 的文件冷安装虚拟分区 Sandefjord
```
vpboot -p Sandefjord -I MINSTALL
```

### 错误
vpboot 在出现以下任何情况时都会在 stderr 上显示错误消息：
- VP_name 在监视器中不存在。
- VP_name 处于 Down 以外的其他状态，因此无法引导。请改用 vpareset(1M) 命令。
- 在尝试访问 Ignite 服务器或冷安装文件时发生错误。
- 您指定了 BOOT 或 ALTBOOT 设备，但对应的设备未在 vp_name 中配置。

注意：如果引导设备未正确配置，vpboot 命令将无错误地完成，但虚拟分区不会引导。可能的原因有两个：
- BOOT 或 ALTBOOT 属性被分配给了磁盘或磁带以外的设备。
- 默认或已配置内核路径处的文件不存在或不是可引导镜像。

### 作者
vpboot 由惠普公司开发。

### 另请参阅
vpcreate(1M), vpmodify(1M), vpremove(1M), vpreset(1M), vpstatus(1M), vpreources(5), vpartition(5).

## vparcreate

vparcreate - 创建新的虚拟分区。

**vparcreate[1M]**

### 名称
vparcreate - 创建虚拟分区

### 概要
```
vparcreate -p vp_name [-B boot_attr] [-D db_file] [-S static_ctrl]
        [-b kernel_path] [-O boot_opts] [-a rsrc]...
```

### 描述
**vparcreate** 命令使用指定的硬件资源创建新的虚拟分区 (vPar)。**vp_name** 是虚拟分区的符号名称，必须在所有引用中使用。如果指定了 *-D* 选项，**虚拟分区将在 db_file 中创建**。否则，它将在虚拟分区监视器数据库中创建。在任一情况下，数据库中已存在名为 **vp_name** 的虚拟分区时是不允许的。任何错误都会终止命令而不创建虚拟分区。

只有超级用户才能执行 **vparcreate** 命令。

### 选项
除 *-a*（添加资源）外，任何选项均不能指定多次。使用 *-a* 选项分配的资源必须可用，即未分配给虚拟分区，且不超过资源的总体限制。使用多个 *-a* 选项分配的资源必须不冲突。违反任何条件均为命令错误。

**vparcreate** 命令识别以下命令行选项和参数：

| 选项 | 描述 |
| :--- | :--- |
| -p vp_name | 指定虚拟分区的符号名称。名称可以由字母数字字符 A-Z、a-z、0-9、下划线字符 (_) 和句点 (.) 组成。名称的最大长度为 259 个字符。必需。 |
| -B boot_attr | 指定虚拟分区的自动引导属性。**boot_attr** 可以具有以下（不区分大小写）值： |
| &nbsp;&nbsp;&nbsp;&nbsp;auto | 设置自动引导属性。 |
| &nbsp;&nbsp;&nbsp;&nbsp;manual | 清除自动引导属性。 |
| | 如果自动引导属性设置为 **auto**，则虚拟分区在成功的 **vparreset** 命令之后或虚拟分区监视器首次加载时重新引导，前提是已指定适当的监视器选项。 |




## -B boot_attr

指定虚拟分区的自动引导属性。`boot_attr` 可以具有以下值（不区分大小写）：

- `auto` 设置自动引导属性。
- `manual` 清除自动引导属性。

如果属性设置为 `manual`，虚拟分区在执行 `vparreset` 后将停止运行，并且在加载监视器时不会引导。此时必须使用 `vparboot` 命令手动引导。

如果省略 `-B` 选项，属性默认为 `auto`。

## -d db_file

在包含于 *db_file* 中的虚拟分区数据库中创建虚拟分区。如果 *db_file* 不存在，该命令将创建它。在创建新的虚拟分区数据库时应使用此选项。

无需运行虚拟分区监视器。如果它正在运行，它不会收到有关新虚拟分区的通知。

尽管作为备用数据库访问时 *db_file* 可以位于任何路径，但在虚拟分区监视器将其作为活动数据库加载之前，必须将其放置在 `/stand` 目录中。

如果省略 `-D` 选项且虚拟分区监视器正在运行，虚拟分区将在虚拟分区监视器的活动数据库中创建。如果监视器未运行，虚拟分区将在默认数据库文件 `/stand/vpdb` 中创建，如果该文件不存在，则会自动创建。

## -s static_attr

指定静态 vPar 属性。*static_attr* 可以具有以下值（不区分大小写）：

- `static` 设置静态属性。
- `dynamic` 重置静态属性。

设置为 *static* 的虚拟分区不支持任何动态资源迁移，也不能使用 `vparmodify` 添加/删除/修改资源属性。此属性在任何初始资源分配后生效，因此在创建新虚拟分区时分配资源并指定结果虚拟分区为 *static* 是可行的。

如果省略 `-S` 选项，属性默认为 `dynamic`。

## -b kernel_path

指定分区可引导内核的绝对路径。例如，如果在 ISL 提示符下非分区系统的启动字符串为：

```
ISL> hpxx -1S /stand/vmunix
```

内核路径就是该字符串中的 `/stand/vmunix` 部分。如果省略此选项，虚拟分区将使用默认内核路径 `/stand/vmunix` 创建。

## -O boot_opts

指定虚拟分区引导时应用的命令行字符串（不包括内核路径）。例如，如果在 ISL 提示符下非分区系统的启动字符串为：

```
ISL> hpxx -1S /stand/vmunix
```

`boot_opts` 字符串就是该字符串中的 `-1S` 部分。请注意，如果字符串包含任何空白字符，则必须对字符串加引号。

支持的引导选项字符串完整列表，请参阅虚拟分区管理指南和题为“监视器和 Shell 命令”的章节。

默认值为空字符串。

## -a rsrc

向虚拟分区添加资源。`rsrc` 是硬件资源规格，如 `vparresources(5)` man 页中所述。资源语法的摘要形式如下表 1 所示。在同一命令中允许有多个 `-a rsrc` 规格，但某些语法形式只允许使用一次。这一点在下表 1 中有说明。在所有情况下，多个规格中的资源不得重复或相互冲突。

### 表 1. 资源语法摘要

某些任务可能会影响其他任务的结果。为避免错误，请参阅 `vparresources(5)` man 页中有关依赖项的详细说明。

## 返回值

`vparcreate` 命令以以下值之一退出：

- 0：成功完成。
- 1：发生了一个或多个错误条件。

## 示例

在虚拟分区监视器数据库中创建名为 Gelo 的虚拟分区，但不分配任何资源：

```bash
vparcreate -p Gelo
```

在虚拟分区监视器数据库中创建名为 Bergen 的虚拟分区，设置 `autoboot` 属性，并指定 5 个处理器（其中 2 个绑定）、2 Gb 物理内存和一个引导磁盘：

```bash
vparcreate -p Bergen -a cpu::5 -a cpu:::2:6 \\
        -a mem::2048 -a io::/0/2/0.6:0:boot -B auto
```

由于未指定 `-b` 选项，引导时将使用默认内核路径 `/stand/vmunix`。

## 错误

在以下任何情况下，`vparcreate` 都会在 `stderr` 上显示错误消息：

- 指定了无效选项。
- 选项指定了无效值或遗漏了值。
- `vp_name` 已存在于监视器数据库或指定的 `db_file` 中。请改用 `vparmodify` 命令。
- 除了 `-a` 以外的一个或多个选项被指定了多次，或同一资源被分配了多次。
- 指定了不可用的资源（已分配给其他虚拟分区或超过可用资源限制）。
- 需要值的参数遗漏了值，或为不接受值的参数提供了值。

## 作者

`vparcreate` 由 Hewlett-Packard 公司开发。

## 另见

`vpartboot(1M)`, `vpartmodify(1M)`, `vpartreserve(1M)`, `vpartreset(1M)`, `vpartstatus(1M)`, `vpartresources(5)`, `vpartition(5)`.

# Man 页

# vpmodify - 修改现有虚拟分区。

vpmodify(1M)                             vpmodify(1M)

## 名称

vpmodify - 修改虚拟分区的属性

## 概要

```
vpmodify -p vp_name [-B boot_attr] [-D db_file] [-S static_attr]
[-b kernel_path] [-o boot_opts] [-P new_vp_name] [-a rescl...
= swpc!... | -d res] ...
```

## 描述

`vpmodify` 命令修改指定虚拟分区的属性和资源。该命令还可以重命名虚拟分区。`vp_name` 是现有虚拟分区的符号名称，必须在所有引用中使用。`vpmodify` 不能创建虚拟分区。请为此目的使用 `vparcreate` 命令。

只有超级用户才能执行 `vpmodify` 命令。

如果指定了 `-D` 选项，则修改 `db_file` 中的 `vp_name`；否则，修改虚拟分区监视器数据库中的 `vp_name`。

如果已在 `vp_name` 中配置了静态属性，则其资源均不得添加、修改或删除。可以修改属性（除 `-a`、`-m` 和 `-d` 以外的所有选项）。请参阅 `-S` 选项说明。

## 选项

在命令中，只有 `-B`、`-a`、`-m` 和/或 `-d` 选项可以指定多次。使用 `-a` 选项分配的资源必须可用，即未分配给虚拟分区。它们还必须不超过资源的总体限制。要修改（`-m`）或删除（`-d`）的资源必须属于 `vp_name`。违反任何条件均为命令错误。

`vpmodify` 识别以下命令行选项和参数。选项从左到右处理。

### -P vp_name

指定要修改的现有虚拟分区的符号名称。

必需。

### -B boot_attr

指定虚拟分区的自动引导属性。`boot_attr` 可以具有以下不区分大小写的值：

- `auto` 设置自动引导属性。
- `manual` 清除自动引导属性。

如果自动引导属性设置为 `auto`，则在成功执行 `vpartreset` 命令后，或者在适当指定了监视器选项时首次加载虚拟分区监视器，虚拟分区将被重新引导。

如果属性设置为 `manual`，虚拟分区在执行 `vpartreset` 后将停止运行，并且在加载监视器时不会引导。此时必须使用 `vpartboot` 命令手动引导。

如果省略 `-B` 选项，属性将不改变。

### -D db_file

对 `db_file` 中包含的 `vp_name` 应用更改。无需运行虚拟分区监视器。如果它正在运行，它不会收到有关修改的通知。

尽管作为备用数据库访问时 `db_file` 可以位于任何路径，但在虚拟分区监视器将其作为活动数据库加载之前，必须将其放置在 `/stand` 目录中。

如果省略 `-D` 选项，虚拟分区监视器必须正在运行。更改将应用于监视器数据库中的 `vp_name`。监视器数据库中的 `vp_name` 必须处于 Down 状态，只有一个例外：未绑定的 CPU 资源可以添加到或从正在运行的虚拟分区中删除。此限制可能会在将来的版本中对其他类型的资源管理放宽。

### -S attr

指定静态虚拟分区属性。`static_attr` 可以具有以下值：

- `static` 设置静态属性。
- `dynamic` 重置静态属性。

如果省略 `-S` 选项，属性将不改变。

不能对静态虚拟分区进行任何硬件资源更改，即不允许使用 `-a`、`-m` 和 `-d` 选项。此限制适用于所有虚拟分区，无论是在备用数据库文件中，还是在监视器的数据库中。





## vparmodify

由于命令行选项是按从左到右的顺序处理的，您可以通过在命令行上先指定 `-S dynamic` 再指定任何资源选项来修改静态分区中的资源，然后在所有资源选项之后指定 `-S static` 以防止进一步修改资源。

`-b kernel_path`
指定用于该分区的可启动内核的绝对路径。如果省略此选项，内核路径将保持不变。

`-o boot_opts`
指定在虚拟分区启动时应用的命令行字符串（内核路径除外）。例如，如果在 ISL 提示符下，未分区的系统启动字符串为：

```
ISL> hpxx -lS /stand/vmunix
```

那么 `boot_opts` 字符串就是该字符串中的 `-lS` 部分。请注意，如果字符串中包含任何空白字符，则必须对该字符串进行引用。

有关支持的各种启动选项字符串的完整列表，请参阅虚拟分区管理指南以及标题为“Monitor and Shell Commands”的章节。

如果省略 `-o` 选项，`boot_opts` 将保持不变。

`-P new_vp_name`
指定正在修改的虚拟分区的新名称。也就是说，在所有修改成功应用于 `vp_name` 后，它会重命名为 `new_vp_name`，前提是该名称在监视器数据库或指定的备用数据库文件中尚不存在。名称可以由字母数字字符 A-Z、a-z、0-9、下划线字符（`_`）和点号（`.`）组成。名称的最大长度为 239 个字符。

- `-a rsrc`：向虚拟分区添加资源。
- `-d rsrc`：从虚拟分区删除资源。
- `-m rsrc`：修改虚拟分区中的现有资源。

`rsrc` 是硬件资源规范，其在 `vparresources(5)` 手册页中有详细描述。下表 1 列出了资源语法形式的摘要。同一命令中允许使用多个资源规范，但某些语法形式仅限于特定选项使用，且某些形式仅允许使用一次。这两种情况均在表 1 中加以说明。在任何情况下，多个规范中的资源不得相互重复或冲突。

### 表 1. 资源语法摘要

| 资源 | 形式 | 选项 | 每次命令次数 |
|----------|-------|---------|-----------------|
| CPU | `cpu:path` | `-a`, `-d` | 多次 |
| | `cpu:num` | `-a`, `-d`, `-m` | 一次 |
| | `cpu::[min:]max` | `-m` | 一次 |
| I/O | `io:path(:attr[;attr2])` | `-a`, `-m`, `-d` | 多次 |
| 内存 | `mem:size` | `-a`, `-m`, `-d` | 一次 |
| | `mem::base:range` | `-a`, `-d` | 多次 |

某些任务可能会影响其他任务的结果。为避免错误，请参阅 `vpresources(5)` 手册页中关于依赖关系的详细说明。

### 返回值

`vparmodify` 命令以以下值之一退出：

- 0：成功完成。
- 1：发生一个或多个错误条件。

### 示例

将名为 Oslo 的虚拟分区更名为 Bergen：

```
vparmodify -p Oslo -P Bergen
```

关闭虚拟分区 Oslo 的自动加速（autoboost）属性：

```
vparmodify -p Oslo -B manual
```

在备用数据库文件 /stand/Norway 中为虚拟分区 Bergen 添加两个处理器：

```
vparmodify -p Bergen -D /stand/Norway -a cpu:2
```

### 错误

在以下任一情况下，`vparmodify` 会在 stderr 上显示错误消息：

- 指定了无效选项。
- 选项指定了无效值，或者省略了值。
- 指定的 `db_file` 不存在、无法访问或已损坏。
- `vp_name` 在指定的 `db_file` 或监视器数据库中不存在。
- `new_vp_name` 已存在于监视器数据库或指定的 `db_file` 中。
- `vp_name` 是静态的，且您尝试更改资源。
- 除 `-S`、`-a`、`-m`、`-d` 以外的一个或多个选项被指定了多次。
- 对于 `-a` 或 `-m` 选项，指定了不可用的资源（已分配给其他虚拟分区或超过可用资源限制）。
- 对于 `-m` 或 `-d` 选项，指定的资源当前未分配给 `vp_name`。

错误发生后，已修改的 vPar 的状态取决于以下因素：

- 如果错误在命令行的语法和语义检查过程中检测到，则 vPar 不会被修改。
- 如果错误在实际修改 vPar 过程中检测到，且您正在修改备用数据库，则 vPar 不会被修改。这是因为更改不会在命令结束前提交。
- 如果在修改 vPar 过程中检测到错误，且您正在修改当前加载到监视器中的数据库，则直到错误发生点所做的任何更改（在命令行上从左到右处理）都将保留。这是因为对实时数据库的更改是增量进行的，即在请求时进行。

### 作者

vparmodify 由 Hewlett-Packard 公司开发。

### 参见

vparboot(1M), vparcreate(1M), vparremove(1M), vparreset(1M), vparstatus(1M), vparresources(5), vpartition(5).

## vparremove - 移除（删除）现有虚拟分区。

vparremove(1M)

### 名称

vparremove - 移除虚拟分区

## 摘要

`vparremove -p vp_name [-D db_file [-f]]`

### 描述

`vparremove` 命令删除之前使用 `vpcreate(1M)` 命令创建的虚拟分区。与虚拟分区关联的所有资源将可供分配给其他分区。

只有超级用户才能执行 `vparremove` 命令。

此命令的非故意使用会带来严重后果；因此，除非指定了 `-f`（强制）选项，否则系统会提示用户确认该操作。

### 选项

`vparremove` 识别以下命令行选项和参数：

- `-p vp_name`：指定要移除的虚拟分区的唯一名称。必填项。
- `-D db_file`：从包含在 `db_file` 中的分区数据库移除虚拟分区。如果省略此选项，虚拟分区将从监视器的数据库中移除。在这种情况下，分区必须处于 Down 状态才能被移除。因此，尝试移除当前虚拟分区（即命令正在执行的那个分区）是一个错误。
- `-f`：指定强制选项。在移除虚拟分区前省略确认对话框。此选项旨在供脚本和其他非交互式应用程序使用。

### 返回值

`vparremove` 命令以以下值之一退出：

- 0：成功完成。
- 1：发生一个或多个错误条件。

### 示例

销毁当前在监视器上运行的分区数据库中的虚拟分区 Oslo：

```
vparremove -p Oslo
Remove virtual partition Oslo? [n]: y
```

使用强制选项销毁当前在监视器中运行的分区数据库中的虚拟分区 Oslo：

```
vparremove -f -p Oslo
```

从分区数据库文件 Norway 中删除分区 Bergen：

```
vparremove -f -D /stand/Norway -p Bergen
```

### 错误

在以下任一情况下，`vparremove` 会在 stderr 上显示错误消息：

- `db_file` 不存在、无法访问、不是虚拟分区数据库文件或已损坏。
- `vp_name` 在监视器的数据库或 `db_file` 中不存在。
- 监视器数据库中的 `vp_name` 处于除 Down 之外的某种状态。

### 作者

vparremove 由 Hewlett-Packard 公司开发。

### 参见

vparboot(1M), vparcreate(1M), vparmodify(1M), vparreset(1M), vparstatus(1M), vparresources(5), vpartition(5).

## vparreset - 向虚拟分区发送 TOC 或硬复位

vparreset(1M)

### 名称

vparreset - 重置虚拟分区

## 摘要

`vparreset -p vp_name [-h|-t] [-q] [-f]`

### 描述

`vparreset` 命令在虚拟分区级别模拟系统控制台上 Control-B 提示符处的 RS 和 TOC 操作。

只有超级用户才能执行 `vparreset` 命令。

`vparreset` 使虚拟分区监视器模拟指定虚拟分区的硬（RS）复位或软（TOC）复位。这两种操作都会收集新的处理器信息模块（PIM）数据，除非同时指定了 `-q`（静默）选项，否则这些数据将显示出来。

此命令的非故意使用会带来严重后果；因此，除非指定了 `-f`（强制）选项，否则系统会提示用户确认该操作。

### 选项

`vparreset` 识别以下命令行选项和参数：

- `-p vp_name`：指定要重置的虚拟分区的唯一名称。虚拟分区必须处于除 Down 或 Crashing 之外的状态。必填项。
- `-t`：模拟 TOC 复位。除非同时指定了 `-q` 选项，否则在重置前会显示当前 PIM 数据。
  
  TOC 复位也是该命令的默认操作，如果在未指定 `-h` 或 `-t` 选项的情况下应用。
  
  同一命令中不能同时指定 `-t` 和 `-h` 选项。
- `-h`：模拟硬（RS）复位而不是 TOC。除非同时指定了 `-q` 选项，否则在重置前会显示当前 PIM 数据。
- `-q`：在重置虚拟分区时，绕过当前 PIM 数据的显示。
- `-f`：强制选项。省略确认对话框

![](img/eff8b9287a5f38c5adf538f24aacf29e_997_0.png)


在重置虚拟分区之前。此选项旨在供脚本和其他非交互式应用程序使用。

## 返回值

vparrset 命令以以下其中一个值退出：

- 0 成功完成。
- 1 发生了一个或多个错误条件。

## 示例

在名为 Oslo 的虚拟分区上执行 TOC 重置，并转储 FIM 数据：

```
vparrset -p Oslo -t
```

重置虚拟分区 Oslo？ [n] y

在虚拟分区 Bergen 上执行硬重置，跳过确认对话框：

```
vparrset -p Bergen -h -f
```

## 错误

vparrset 在以下任一情况下都会在标准错误输出（stderr）上显示错误消息：

- 省略了必需的选项。
- 指定了未知的选项。
- 对于需要值的参数省略了值，或者对于不接受值的参数指定了值。
- vp_name 不存在于监视器数据库中，或者处于错误的状态。
- 同时指定了 -h 和 -t 选项。

## 作者

vparrset 由惠普公司（Hewlett-Packard Company）开发。

## 另请参阅

vparkboot(1M), vparkcreate(1M), vparkmodify(1M), vparkremove(1M), vpartstatus(1M), vparresources(5), vpartition(5)。

## Vparesources

## 名称

vparesources - 虚拟分区资源及其要求的描述

## 描述

硬件资源是虚拟分区（vPar）最重要的属性。这些资源分为三个主要类别：

- CPU，即处理器
- 内存
- I/O 设备，例如磁盘、终端和打印机。

CPU 进一步细分为绑定处理器和非绑定处理器。绑定处理器启用中断，并且在初始发布中，当 vPar 正在运行时不能取消配置。非绑定（或浮动）处理器无法处理中断，但可以从正在运行的 vPar 中取消配置，并分配给另一个正在运行的 vPar。

每个 vPar 可以配置系统总硬件资源的子集，使得给定的物理资源最多分配给一个 vPar。这项工作由六个虚拟分区命令中的两个管理：

- vparcreate(1M)，用于创建新 vPar 时。只能添加资源。
- vparmodify(1M)，用于修改现有 vPar 配置时。可以添加、修改或删除资源。

每个命令都有特定的资源语法和语义要求。例如，某些资源更改只能针对未运行的目标 vPar 进行。某些语法形式可以在一个命令中多次指定。其他形式只能指定一次。所有这些条件都在下表中描述。

资源规范的一般形式是多达五个位置字段，由冒号 (":") 分隔。任何字段内均不允许有空格。

表 I 总结了三个类别以及每个类别的所有允许形式。

表 II 指定了三种任务（添加、修改或删除）中允许的形式。

表 III 是对每种语法形式及其使用条件的详细描述。

## 表 I. 资源语法摘要

| 资源 | 形式 | 每次命令次数 |
| :------- | :--- | :------------ |
| CPU | cpu:path | 多次 |
| | cpu:num | 一次 |
| | cpu::[min[{:max}]] | 一次 |
| I/O | io:path[·attr1[·attr2]] | 多次 |
| 内存 | mem:size | 一次 |
| | mem::base:range | 多次 |

第一个字段始终是（不区分大小写的）字符串 cpu、io 或 mem 之一。

第二个字段，如果使用时，是硬件路径，例如 10/12/6。num、min 和 max 都是正整数。

size 和 range 是以兆字节为单位的正 64 位整数。base 是以字节为单位的无符号 64 位整数。命令会根据需要将它们分别向上舍入到 64 兆字节边界。size、range 和 base 都可以用十进制或十六进制表示。十六进制规范前应以 0x 开头，如 0x80000000。

I/O 规范的属性是以下（不区分大小写的）字符串中的零个、一个或全部：ALTBOOT 和 BOOT。如果同时指定，请用逗号分隔。

每个属性最多可分配给一个 I/O 设备。如果它已分配给某个设备，新分配会静默地解除与其当前设备的分配。然而，一个设备可以关联两个属性。这意味着一个设备可以拥有 ALTBOOT 和 BOOT 两个属性，但不可能两个或更多设备拥有 BOOT。

用户必须注意防止将属性分配给不合适的设备，例如将 BOOT 分配给 tty。命令不会检查这一点，也不会阻止它。

## 表 II. 每种任务允许的形式

| 任务 | 形式 | vPar 运行时允许 |
| :--- | :--- | :------------: |
| -a (添加) | cpu:path | 否 |
| | cpu:num | 是 |
| | cpu::[min[{:max}]] | 不适用 |
| | (仅限 Vpar/create) | |
| | io:path[·attr1[·attr2]] | 否 |
| | mem:size | 否 |
| | mem::base:range | 否 |
| -m (修改) | cpu:num | 是 |
| | cpu::[min[{:max}]] | 否 |
| | io:path[·attr1[·attr2]] | 否 |
| | mem:size | 否 |
| | cpu:path | 否 |

上述形式受命令执行的以下语义规则约束。请注意，根据表 II，除了 cpu::num 形式外，vPar 必须处于关闭状态（或在备用数据库中）才能应用下面描述的任何更改。这一要求可能会在未来的版本中放宽或移除。

### CPU

- 分配给 vPar 的 CPU 总数，由 cpu:num 指定，必须始终在 cpu::min/max 规范指定的范围内。min 或零是绑定的；num=min 是非绑定的。
- 任何或所有绑定 CPU 都可以通过显式路径指定。cpu:path 形式。未如此指定的任何 CPU 都从可用池中分配并绑定到 vPar 监视器。

由此推导出的结果是，你不能通过显式路径指定超过 min 数量的 CPU。如果你希望指定更多，你必须先增加 min，而这反过来可能要求你增加 max、num 或两者。

当你使用 + cpu:path 或 - d cpu:path 时，你并没有改变 vPar 中 CPU 的总数；相反，你用你指定的 CPU 替换监视器分配的绑定 CPU (-a)，或者用监视器分配的 CPU 替换你指定的 CPU (-d)。

惠普建议用户仅在出于性能原因需要时才配置特定的 CPU。在其他情况下，仅指定 CPU 总数 (num) 和其中应该绑定多少 (min)，并允许监视器管理实际分配的 CPU。

- 由于在备用数据库中配置 vPar 时不会咨询监视器（它甚至不必运行），在这种情况下你可以为 min 指定任何值（但不能指定 max）。当此数据库加载到监视器时，如果指定数量的 CPU 不可用，监视器会将 min 向下调整。
- 默认值：创建 vPar 时，以下默认值生效。

使用 mem::base:range 规范指定的范围必须小于或等于使用 mem::size 规范分配给 VPar 的总内存。

当你指定特定范围的内存（无论是添加还是删除）时，你并没有改变分配给 VPar 的内存总量。添加时，你只是指定你给出的特定范围应为分配给你的 VPar 的总量的一部分。删除时，特定范围将返回到分配给 VPar 的未指定总内存池。

惠普建议用户仅在出于性能原因需要时才配置特定的内存范围。在其他情况下，仅指定总内存并允许监视器管理实际分配的范围。

- 示例。

如果在命令中指定了多个任务，它们将按照在命令行中遇到的顺序（从左到右）进行处理。某些任务会影响其他任务的结果。以下是正确使用示例，以及描述中的反例。

```
vparcreate -p winona2 -a cpu::2 -a cpu::2:4 -a cpu:41 -a cpu:45 -a mem::1280 -a mem::0x040000000:128 -a io::0 -a io::1/10 -a 0/8/0/0.5.0:boot
```

在创建时，在处理任何选项之前，min 等于 1，num 也是。假设默认 max 足够高，且指定资源可用于分配。

- -a cpu::2 成功，因为 num(2) 在 min 和 max 的范围内。
- 然后 -a cpu::2:4 成功，因为 num(2) 仍然在所需范围内。注意，如果反转这两个选项，由于从左到右的选项处理，命令将返回错误，因为所需的 min 将超过默认的 num。
- 最后，显式路径 41 和 45 上两个 CPU 的规范成功，因为此类分配创建绑定 CPU。由于我们将 min 设置为 2，它们可以容纳。注意，如果没有前两个 -a 选项，-a cpu:45 选项将失败，因为只能容纳一个（默认的）绑定 CPU。
- 在地址 0x4000000 分配 128 MB 特定内存之所以成功，是因为首先将分配的总内存设置为 1280 MB。这 128 MB 取自那 1280 MB；-a mem::0x40000000:128 选项不会导致增加新的内存。
- 以下 vparmodify(1M) 命令向设置了静态属性的 VPar 添加两个（非绑定）CPU。然后恢复静态属性。

```
vparmodify -p winona2 -S dynamic -a cpu::2 -S static
```





## 表 III. 详细资源规范

### 任务：-a cpu:path

| 项目 | 详情 |
| :--- | :--- |
| **说明** | 将特定路径下的 CPU 资源（绑定 CPU）分配给 vPar 配置。该 CPU 替换监视器分配的绑定 CPU。绑定 CPU 能够处理中断。 |
| **值** | `ioscan(1M)` 命令返回形式的文本字符串，例如“10/12/6” |
| **使用限制** | vPar 必须未运行。此限制可能在将来的版本中移除。<br>特定路径下的 CPU 总数必须 <= min<br>此外，如果 vPar 在监视器数据库中：<br>- 路径处必须存在 CPU，<br>- 它必须可用（未分配给任何 vPar，包括目标 vPar）。 |
| **使用指南** | 此操作不会增加分配给 vPar 的 CPU 总数或绑定 CPU 数。相反，它替换了之前由监视器选择路径的绑定 CPU。要增加 CPU 总分配量，请指定适当的 `num`。要增加绑定 CPU 数量，请指定新的 `min`。<br><br>惠普（Hewlett-Packard）建议用户仅在性能原因需要时配置特定 CPU。在其他情况下，仅指定 CPU 总数（`num`）和其中应绑定的数量（`min`），并允许监视器管理实际分配的 CPU。 |

### 任务：-a cpu:num

| 项目 | 详情 |
| :--- | :--- |
| **说明** | 将 `num` 个未绑定 CPU 添加到 vPar 配置中。这些 CPU 取自系统范围的可用 CPU 池。 |
| **值** | 正整数 |
| **使用限制** | 如果 vPar 在备用数据库文件中，或在实时监视器数据库中但未运行：<br>- CPU 总数 <= max<br>此外，如果 vPar 正在运行：<br>- 系统中必须存在 `num` 个 CPU，<br>- 在 vPar 启动时，它们必须可用（未绑定给任何 vPar）。<br>如果使用 `vparremove` 命令删除另一个 vPar，其绑定 CPU 不能作为浮动者添加到正在运行的 vPar 中。 |

### 任务：-a cpu:: [min] [:: [max]]

| 项目 | 详情 |
| :--- | :--- |
| **说明** | 指定 vPar 允许的最小和最大 CPU 数量。此操作不分配任何 CPU，但指定其他分配任务的限制。 |
| **详情** | `min` 和 `max` 均为可选。默认 `min` 取决于平台，但目前 = 1。如果在备用数据库中创建 vPar，默认 `max` 为 32767。如果在监视器数据库中创建 vPar，默认 `max` 为整个硬件系统的 CPU 总数。 |
| **值** | 如果指定，`min` 和 `max` 必须是正整数，且 `min` < `max`。 |
| **使用限制** | 此选项仅允许在 `vparcreate` 命令中使用。<br><br>`min` 不能超过 CPU 总数。创建 vPar 时的默认总数为 1。使用 `-a cpu::num` 选项在设置除 1 以外的 `min` 之前更改总数。<br><br>`max` 不能小于总数。<br><br>`min` 不能小于通过明确路径配置的 CPU 总数。 |

### 任务：-a iopath: [attr1] [,attr2]

| 项目 | 详情 |
| :--- | :--- |
| **说明** | 将 `path` 处的 I/O 资源添加到 vPar。<br><br>如果指定了属性，它们将与该资源关联。如果 vPar 已经拥有该资源，则指定的属性将添加到其配置中。<br><br>此选项仅添加指定的属性。未指定属性的状态不会更改。 |
| **值** | `path`：`ioscan(1M)` 命令返回形式的文本字符串，例如 "10/12/5"<br><br>`attr`：ALTBOOT 和 BOOT 这两个不区分大小写的属性字符串之一或两者。如果同时指定，它们用逗号 (",") 分隔， |
| **使用限制** | vPar 必须未运行。<br><br>I/O 资源必须未分配，或者（当向已分配的资源添加属性时）分配给目标 vPar。 |
| **使用指南** | 最多只能为一个设备分配 ALTBOOT 和 BOOT 属性。如果将其中一个属性分配给设备，会静默地从其前一个设备（如果有）中删除该属性。<br><br>注意：您应该将属性分配给合适的设备，但系统不会检查这一点。例如，应将 ALTBOOT 和 ROOT 分配给磁盘或磁带。未这样做可能会导致分区无法启动。 |

### 任务：-a mem::size

| 项目 | 详情 |
| :--- | :--- |
| **说明** | 指定分配给 VPar 的内存总量的增加量（以兆字节为单位，向上舍入到 64 兆字节边界）。该内存取自系统启动时可用的未指定内存范围。 |
| **值** | 正 64 位整数 <= 175921860444152 |
| **使用限制** | vPar 必须未运行。<br><br>如果 vPar 在监视器数据库中，此内存必须物理存在，并且在满足所有其他 vPar 的内存需求后必须可用。<br><br>如果 vPar 在备用数据库文件中，分配总是成功的。数据库实际分配的内存量加载到监视器中可能更少，如果其中部分或全部内存被其他 vPar 需要。 |

### 任务：-a mem::base-range

| 项目 | 详情 |
| :--- | :--- |
| **说明** | 指定从 `base` 字节开始并扩展 `range` 兆字节的显式内存地址空间。这两个量均按要求向上舍入以对齐到 64 兆字节边界。 |
| **值** | `Base`：无符号 64 位整数 <= 0xffffffffffffffff<br>`Range`：正 64 位整数 <= 175921860444152 |
| **使用限制** | vPar 必须未运行。<br><br>该范围的任何部分都不得已被此 vPar 或其他 vPar 拥有。<br><br>如果 vPar 在监视器数据库中，整个范围必须存在于系统中。<br><br>在特定范围内分配的总内存不得超过 vPar 的内存大小规范。 |
| **使用指南** | 添加特定内存范围不会增加分配给 vPar 的总内存量。此类内存是该总量的一部分。<br><br>注意：指定内存范围和大小可能会导致没有任何 vPar 能够启动的情况。惠普（Hewlett-Packard）建议用户仅在性能原因需要时配置特定内存范围。在其他情况下，仅指定总内存量并允许监视器管理实际分配的范围。 |

### 任务：-m cpu::num

| 项目 | 详情 |
| :--- | :--- |
| **说明** | 将 CPU 总数（绑定和未绑定）设置为 `num`。 |
| **值** | 正整数 |
| **使用限制** | 如果 vPar 在备用数据库文件中，或在实时监视器数据库中但未运行：<br>- `num` 必须在 `min` 和 `max` 之间。<br><br>此外，如果 vPar 在实时监视器数据库中且 `num` 增加了总数：<br>- 系统中必须存在 `num` 个 CPU。<br>- 在 vPar 启动时，它们必须可用（未绑定给任何 vPar）。<br>如果使用 `vparremove` 命令删除另一个 vPar，其绑定 CPU 不能作为浮动者添加到正在运行的 vPar 中。 |

### 任务：-m cpu::[min] [; [max]]

| 项目 | 详情 |
| :--- | :--- |
| **说明** | 指定 vPar 允许的最小和最大 CPU 数量。此操作不分配任何 CPU，但指定其他分配任务的限制。<br><br>通过不指定另一个字段，您可以只更改 `min` 或 `max`。 |
| **值** | 如果指定，`min` 和 `max` 必须是正整数，且 `min` <= `max`。 |
| **使用限制** | vPar 必须未运行。<br><br>`min` 不能超过 CPU 总数。<br><br>`max` 不能小于总数。<br><br>`min` 不能小于通过明确路径配置的 CPU 总数。 |

### 任务：-m iopath[:attr1[,attr2]]

| 项目 | 详情 |
| :--- | :--- |
| **说明** | 将资源属性更改为选项中指定的属性。省略的属性将从属性集中移除。要保留某项属性，必须指定它。 |
| **值** | `path`：`ioscan(1M)` 命令返回形式的文本字符串，例如 "/0/12/6"<br><br>`attr`：ALTROOT 和 ROOT 这两个不区分大小写的属性字符串之一或两者。如果同时指定，它们用逗号 "," 分隔。 |





## 使用限制
vPar 必须未处于运行状态。
I/O 资源必须已分配给目标 vPar。
仅可以修改属性。

## 使用指南
最多只能为一个设备分配 ALTBOOT 和 ROOT 属性。如果将这些属性之一分配给某个设备，则它会静默地从其原设备（如果存在）中删除。

**注意：** 应将属性分配给合适的设备，但系统不会对此进行检查。例如，ALTBOOT 和 ROOT 应分配给磁盘或磁带。否则可能会导致分区无法启动。

### 任务：-m mem=size

**说明**
指定分配给该 vPar 的内存总量（以兆字节为单位，向上取整到 64 兆字节的边界）。超出由 base 和 range 具体分配的内存部分，将从分区启动时系统可用的未指定内存范围中获取。

**取值**
小于 17592186044352 的正 64 位整数

**使用限制**
- vPar 必须未处于运行状态。
- 内存分配总量的减少不得导致总内存少于所有在特定内存范围中已分配的内存之和。
- 如果该 vPar 位于监视器数据库中，且配置结果导致内存分配增加，则物理上必须存在该内存，并且在满足所有其他 vPar 的内存需求后，该内存必须可用。
- 如果该 vPar 位于备用数据库文件中且总内存增加，则分配操作总是成功。如果在监视器加载该数据库时部分或全部内存被其他 vPar 所需，实际分配的内存量可能会更少。

### 任务：-d cpu:path

**说明**
从 vPar 中解除指定硬件路径上的绑定 CPU 的分配，并用监视器选定的一个绑定 CPU 替换它。取决于可用性，这可能与被解除分配的 CPU 相同。

**取值**
由 toscan(1M) 命令返回的格式形式的文本字符串，例如 “10/12/6”

**使用限制**
- vPar 必须未处于运行状态。
- 指定路径处的资源必须是 CPU 资源。
- vPar 必须拥有该资源。

**使用指南**
- 删除操作不会减少分配给 vPar 的 CPU 总数或绑定 CPU 数量。相反，它会用监视器选定的一个绑定 CPU 替换明确指定的 CPU。若要减少总 CPU 分配量，请指定新的合适 num 值。若要减少绑定 CPU 的数量，请指定新的 min 值。
- 惠普建议用户仅在出于性能原因需要时才配置特定 CPU。在其他情况下，只需指定 CPU 总数 (num) 以及其中应绑定的数量 (min)，并允许监视器管理实际分配的 CPU。

### 任务：-d cpu:num

**说明**
从 vPar 的总配置中删除 num 个 CPU。

**取值**
一个正整数。

**使用限制**
- vPar 必须至少拥有 num 个 CPU。
- 新的 CPU 总数 >= min

### 任务：-d io:path[:attr1[,attr2]]

**说明**
移除资源的指定属性，保持先前分配的属性不变，并且资源本身仍分配给 vPar。如果未指定属性，则移除该资源及其所有属性。

**取值**
- path：由 ioscan(1M) 命令返回的格式形式的文本字符串，例如 “10/12/6”
- attr：大小写不敏感的属性字符串 ALTBOOT 和 BOOT 中的一个或两者。如果同时指定两者，它们由逗号 [“,”] 分隔。

**使用限制**
- vPar 必须未处于运行状态。
- I/O 资源必须已分配给目标 vPar。

**使用指南**
- 从 I/O 设备中删除属性并不会导致该属性被分配给其他设备。您必须在单独的选项或命令中执行此操作。
- 最多只能为一个设备分配 ALTBOOT 和 BOOT 属性。
- **注意：** 应将属性分配给合适的设备，但系统不会对此进行检查。例如，ALTBOOT 和 BOOT 应分配给磁盘或磁带。否则可能会导致分区无法启动。

### 任务：-d mem::size

**说明**
指定分配给该 vPar 的内存总量的减少量（以兆字节为单位，向上取整到 64 兆字节的边界）。

**取值**
小于或等于 175921860444152 的正 64 位整数

**使用限制**
- vPar 必须未处于运行状态。
- vPar 必须至少拥有指定量（取整后）的非特定内存。
- 减少量不得导致总内存少于所有在特定内存范围中已分配的内存之和。

### 任务：-d mem::base::range

**说明**
解除分配从 base 字节开始并延伸 range 兆字节的显式内存地址空间。这两个量都会按需要向上取整，以对齐到 64 兆字节的边界。

**取值**
- Base：小于或等于 0xffffffffc00000 的无符号 64 位整数
- Range：小于或等于 17592186044352 的正 64 位整数

**使用限制**
- vPar 必须未处于运行状态。
- vPar 必须拥有整个范围。
- 指定范围的起点或终点必须与现有范围的起点或终点相匹配。

**使用指南**
- 解除分配特定内存范围不会减少分配给 vPar 的内存总量。
- **注意：** 有可能指定内存范围和大小，导致没有任何 vPar 能够启动。惠普建议用户仅在出于性能原因需要时才配置特定内存范围。在其他情况下，只需指定总内存量并允许监视器管理实际分配的范围。

### 参见

vparboot(1M), vparcreate(1M), vparcmd(1f)(1M), vparremove(1M), vparreset(1M), vparstatus(1M), partition(5).

# vpstatus - 显示虚拟分区和可用资源信息

![](img/eff8b9287a5f38c5adf538f24aacf29e_1010_0.png)

vpstatus(1M)                                    vpstatus(M)

## 名称

vpstatus - 显示一个或多个虚拟分区的信息。

## 概要

vpstatus [-v | -M] [-p vp_name]... [-D db_file]
vpstatus -A [-M]
vpstatus -w
vpstatus -e
vpstatus -R [-p vp_name]

## 描述

*vpstatus* 命令的各种形式显示：

-   * 一个或多个虚拟分区 (vPar) 相关的属性和硬件资源，采用摘要（默认）或详细格式。-w 选项以机器可读格式显示相同的数据。
-   * 当前可用的资源，即未分配给任何虚拟分区的资源。-M 选项以机器可读格式显示相同的数据。
-   * 当前虚拟分区的名称，即运行该命令的虚拟分区。
-   * 虚拟分区监视器的事件日志。
-   * 最近一次虚拟分区重置的处理器信息模块 (PIM) 数据。

只有超级用户才能执行 *vpstatus* 命令。

如果未提供参数，*vpstatus* 将以摘要格式显示监视器数据库中所有虚拟分区的所有属性和资源。可以显式指定一个或多个虚拟分区，以便将输出限制为关于选定虚拟分区的信息。-D 选项列出备用数据库文件中的类似信息，但有一个主要区别。有关详细信息，请参阅 -D 选项的描述。

有三种主要的列表格式。所选格式取决于命令选项和形式：

-   * 摘要格式列出名称、属性和资源总计。如果不使用 -v 或 -M 选项，则显示此格式。
-   * 详细格式列出名称、属性和详细的资源分配，每行一项，带有注释性标题。-v 选项产生此格式。
-   * 机器可读格式显示与详细格式相同的信息，只是省略了字段描述性标题，且所有信息都在同一行上。各个字段之间由四个分隔符分隔。以下均对这些分隔符进行了描述。

针对 -w、-e 和 -R 选项提供了另外三种格式。

vpstatus 显示的信息包括以下内容：

-   * 虚拟分区的名称（在摘要格式中限制为 30 个字符）
-   * 虚拟分区的状态，来自以下列表：
    -   Up：虚拟分区已通知监视器其已启动。这是正在运行的虚拟分区的正常状态，但这并不意味着虚拟分区已完成初始化并完全处于操作状态。
    -   Down：虚拟分区已完全停止。这可能是正常的 /etc/shutdown -h 命令的结果，或者是将自动启动属性设置为手动 (manual) 的分区重置 (paraphereset) 的结果。这也是虚拟分区监视器启动后立即进入的初始状态。
    -   Load：监视器正在加载虚拟分区的内核映像。此状态位于 boot 状态之前。
    -   Boot：虚拟分区已启动，但尚未完全引导。
    -   Crash：虚拟分区正在非优雅地关闭（要么 panic 要么重置）
    -   Shut：虚拟分区正在优雅地关闭
    -   Hung：虚拟分区已停止向监视器发送心跳消息。
    -   N/A：虚拟分区位于备用数据库文件中，因此没有状态。
-   * 静态/动态资源属性
-   * 自动/手动启动属性
-   * 内核路径（在摘要格式中限制为 25 个字符）
-   * 启动选项（在摘要格式中限制为 5 个字符）
-   * CPU、I/O 和内存资源分配的摘要或详细信息

## 选项

vpstatus 识别以下命令行选项和参数：

```
-P vp_name    将命令显示限制为 vp_name 的信息。默认情况下，显示监视器数据库中或指定备用分区数据库中所有虚拟分区的信息。可以指定多个 vp_names，但在显示 PIM 数据时除外。
```

```
-D db_file   显示来自备用分区数据库文件 db_file 的信息，而不是来自监视器
```


交替数据库文件中 vVar 的属性和资源是在 vpcreate 或 vpmmodify 命令中指定的，但未必在运行系统上检查过其存在性。这些信息被称为“请求的”信息。监视器实时数据库中 vVar 的属性和资源的存在性已得到验证；这些信息被称为“有效的”信息。

-   -v - 显示详细展示。每行一个属性或资源。每个属性和资源类型均会被标识。当路径信息可用时，CPU 资源通过路径进行标识。在显示交替数据库中的 vVars 或处于 Down 状态的 vVars 的状态时，某些 CPU 资源可能未知。在这种情况下，将显示“no path”。
-   -A - 显示关于可用资源（即未分配给任何虚拟分区的资源）在虚拟分区监视器数据库中的信息。监视器必须正在运行。资源每行显示一个。
-   -M - 以机器可读格式显示信息。各字段由以下四种分隔符之一分隔：
    -   分号 (;) 分隔每个字段和资源类型。例如，状态、属性信息和内核路径将显示为：
        `Up;Static,Auto:/stand/vmunix`
    -   冒号 (:) 分隔资源类型的子字段。例如，CPU 资源显示为：
        `5/10;33,37;51,53,55;<,>,<`

在上述示例中，第一个子字段显示为虚拟分区配置的最小和最大 CPU 数量；第二个子字段列出由用户特定配置的绑定（指定）CPU；第三个子字段列出剩余的绑定 CPU，这些 CPU 由监视器分配；最后一个子字段列出未绑定（浮动）CPU。

在上面的示例中，未绑定 CPU 的路径是未知的。这种情况可能是因为示例中的 vVar 位于交替数据库中，或者 vVar 处于 Down 状态而未分配未绑定 CPU。在这种情况下，路径位置将显示为“<>”。这也适用于对应的非机器可读显示（-v 或 -A）。

-   -w - 显示当前虚拟分区的名称（即执行该命令的分区）。监视器必须正在运行。
-   -e - 显示监视器的事件日志，这是一个大约 4K 字节长的循环文件。一旦文件填满，新条目将覆盖旧条目至最近的字符。因此，显示的第一个条目可能会缺少一些开头字符。监视器必须正在运行。
-   -P - 显示指定虚拟分区最近一次重置的处理程序信息模块（PIM）数据。如果未指定虚拟分区，则显示当前虚拟分区（即执行该命令的分区）的 PIM 数据。

如果虚拟分区未被重置，或者自上次重置以来 PIM 数据已被清除，则没有可用的 PIM 数据，将显示相应消息。监视器必须正在运行。

### 返回值

vparstatus 命令以以下值之一退出：

-   0: 成功完成。
-   1: 语法错误或无效选项。

### 示例

以下示例假设存在一个 N 类硬件系统 Europe，虚拟分区监视器中当前加载了虚拟分区数据库 Norway。Norway 有两个已配置的虚拟分区：Oslo 和 Bergen。vparstatus 命令从 Gslo 中运行。

Europe 有八个 CPU，两个系统总线适配器（SBA），每个有六个本地总线适配器（LBA），以及 2 Gbytes 主内存。这些资源按如下方式分配给 Oslo 和 Bergen：

-   Gslo:
    -   两个位于硬件路径 33 和 37 的绑定 CPU。位于 33 的 CPU 是用户通过 -a cpupath 资源指定指定的。位于 37 的 CPU 是监视器在 Oslo 启动时从可用 CPU 池中分配的。
    -   一个位于硬件路径 41 的浮动（未绑定）CPU。
    -   一个位于 SBA/LBA/路径 0/0/2/0.6.0 的 SCSI 引导磁盘。
    -   一个位于 0/0/4/0 的终端。
    -   一个连接了多个 LAN 适配器的 LBA (0/4)。
    -   特定内存地址 0x0000000 到 0xC000000（范围 = 64 MB）和 0x2000000 到 0x60000000（范围 = 128 MB）。这些特定范围是总共 768 MB 内存分配的一部分。
-   Bergen:
    -   两个位于硬件路径 97 和 101 的绑定 CPU，均由监视器分配。
    -   两个位于硬件路径 93 和 99 的未绑定 CPU。
    -   一个位于 1/4/0/0.5.0 的 SCSI 引导磁盘。
    -   一个连接了多个 LAN 适配器的 LBA (1/10)。
    -   特定内存 0x64000000 到 0x50000000（范围 = 192 MB）和 0x60000000 到 0x80000000（范围 = 512 MB）。这些特定范围是总共 768 MB 内存分配的一部分。

显示所有虚拟分区中所有属性和资源的摘要格式：

```
# vparstatus
[Virtual Partition]
    Root
Virtual Partition Name/State Attributes Kernel Path Opts
——————————————————————————————————————————————————
Oslo      Up      Static,Auto /stand/vmunix
Bergen    Up      Dyn,Manl    /stand/vmunix

(Virtual Partition Resource Summary)
    CPU    Num    Memory (MB)
CPU    Bound    IO # Ranges/
Virtual Partition Name Min/Max    Unbound devs Total MB   Total MB
———————————————————————————————————————
Oslo     2/      4        21         3        2/640     704
Bergen   2/      4        22           2        2/704    768
```

显示分区 Oslo 的详细属性和资源：

```
# vparstatus -p Oslo -v
[Virtual Partition Details]
Name:         Oslo
State:        Up
Attributes:   Static,Auto,root
Kernel Path:  /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max:      2/4
Bound by User [Path]:33
Bound by Monitor [Path]: 37
Unbound [Path]: 41

[IO Details]
0.0:2.0.6.0 BOOT
        10000
        0.4

[Memory Details]
Specified (Base [Range]:      0x40000000/64
Bytes) (MB):                  0x20000000/128
Total Memory (MB):    704
```

以机器可读格式显示 Bergen 的 CPU 资源：

```
# vparstatus -p Bergen -M
Bergen:Up;Dynamic,Manual;/stand/vmunix::2/4;/97,101,93,99;1.4.0.0.5.0 BOOT;1.10
:0x44000000/192,0x40000000/512;768
```

显示当前虚拟分区的名称：

```
# vparstatus -w
The current virtual partition is Oslo.
```

### 作者

vparstatus 由惠普（Hewlett-Packard）公司开发。

### 另请参阅

-   vparboot(1M), vparcreate(1M), vparmodify(1M), vparremove(1M),
-   vparreset(1M), vparresources(5), vpartition(5).

## vpartition - 显示 vPar 命令行接口的信息。

vpartition(5)			vpartition(5)

### 名称

vpartition - 显示虚拟分区命令行的信息

### 概要

vpartition

### 描述

本手册页列出了用于管理虚拟分区的命令及其简要描述。

| 命令 | 描述 |
| :--- | :--- |
| **vparboot** | 启动虚拟分区。 |
| **vparcreate** | 创建新的虚拟分区。 |
| **vparstatus** | 管理监视器转储文件。 |
| **vparxtract** | 从运行中的虚拟分区系统提取内存映像。 |
| **vparmodify** | 修改现有的虚拟分区。 |
| **vparreloc** | 重新定位 vmutex 文件的加载地址，确定 vmutex 文件是否可重定位，或提升可重定位 vmutex 文件中符号的作用域。 |
| **vparremove** | 移除（删除）现有的虚拟分区。 |
| **vparreset** | 向虚拟分区发送 TOC 或硬重置。 |
| **vparresources** | 描述虚拟分区资源及其要求。 |
| **vparstatus** | 显示虚拟分区和可用资源信息。 |
| **vparutil** | 从虚拟分区获取和设置磁盘设备的 SCSI 参数。 |

### 作者

vpartition 由惠普（Hewlett-Packard）公司开发。

### 另请参阅

vparboot(1M), vparcreate(1M), vparstatus(1M), vparxtract(1M),
vparmodify(1M), vparreloc(1M), vparremove(1M), vparreset(1M),
vparstatus(1M), vparutil(1M), vparresources(5).

## vparutil - 处理 vPar 中磁盘的 SCSI 相关信息。

vparutil(1M)

### 名称

vparutil - 从虚拟分区获取和设置磁盘设备的 SCSI 参数

### 概要

vparutil -g dev_path
vparutil -s dev_path [id] [rate]

### 描述

vparutil 命令用于从运行中的虚拟分区系统获取和设置指定 SCSI 设备的 SCSI 参数。
只有超级用户可以执行 vparutil 命令。

选项

vparutil 识别以下命令行选项：
-   -g
    获取指定 SCSI 磁盘设备 dev_path 的 SCSI 参数。
-   -s
    设置指定 SCSI 磁盘设备 dev_path 的 SCSI 参数。

vparutil 识别以下命令行操作数：
-   dev_path
    SCSI 磁盘设备的设备路径。
-   id
    指定磁盘设备的 SCSI ID。
-   rate
    指定磁盘设备的 SCSI 速率。

### 示例

将位于 0/0/2/0.6.0 的磁盘的 SCSI ID 设置为 3：
# vparutil -s 0/0/2/0.6.0 3

### 返回值

-   0: 成功。
-   1: 无法与虚拟分区监视器通信。
-   >1: 其他错误。

### 作者

vparutil 由惠普（Hewlett-Packard）公司开发。




## 附录 B

### Superdome 虚拟分区

## Superdome vPars

截至本书付梓时，我已经在针对 Superdome 的最初版预发布 vPars 软件上进行工作。本附录包含了我基于初步工作整理的与 Superdome 上的 vPars 相关的重要信息。本书中涵盖的所有内容均适用于 Superdome 上的 vPars。Superdome 的硬件路径与本书示例中使用的 L-Class 和 N-Class 系统的硬件路径有显著不同。因此，我将简要介绍一些 Superdome 上 vPars 的示例，其中包含路径相关信息。

每个 Superdome 硬分区（nPartition）都等同于一个独立的服务器。本书中使用的 L-Class 和 N-Class 系统的示例类似于 Superdome 的 nPartition。因此，只要满足截至撰写时 vPars 的所有要求，我们可以在每个 nPartition 上加载多个 vPars，例如：
- 每个 vPar 拥有独立的启动设备；
- 每个本地总线适配器（LBA）仅分配给一个 vPar；
- 每个 vPar 至少有一个 CPU；等等。

对于接下来的示例，我们确实已满足这些要求。

Superdome 上的守护者服务处理器（GSP）用于为 Superdome 复合系统提供控制台控制。通过连接到 GSP，您可以选择具有控制台控制权的 nPartition。您可以将控制台控制权切换到 Superdome 复合系统中的任意 nPartition。这与我们用于在 vPars 之间切换控制台的 Ctrl-A 功能不同。当我们通过 GSP 上的控制台连接到我们的 nPartition 时，我们连接的是 nPartition，而不是 nPartition 内的某个 vPar。作为在 nPartition 中配置 vPars 的一部分，我们将把核心 I/O 卡分配给我们 nPartition 中的四个 vPars 之一。

让我们通过查看一个完整的 Superdome 复合系统，然后聚焦于将用于支持多个 vPars 的一个 nPartition，来开始我们的 Superdome vPar 工作。

### 分区的层次结构

图 B-1 展示了我们 Superdome 复合系统中分区的层次结构：

![](img/eff8b9287a5f38c5adf538f24aacf29e_1019_0.png)

**图 B-1 Superdome 复合系统中 nPartitions 内的多个 vPars**

每个 nPartition 可以包含多个 vPars。图 B-1 中的 nPartitions 中的 nPar3 被展开，以显示在我们的即将到来的示例中它将运行四个虚拟分区。

现在让我们继续查看我们将创建 vPars 的 nPartition 中的硬件。

### nPartition 和 Superdome 背景知识

nPartitions 是 Superdome 平台内的硬分区。Superdome 服务器可以支持从 1 到 16 个 nPartitions，每个 nPartition 都支持其自身的操作系统、应用程序、外围设备和网络。目前，每个 nPartition 可以托管 HP-UX 操作系统环境。当 Superdome 的 Intel IPF 版本可用时，nPartitions 也将支持 Linux 和 Windows 环境。目前，rp8400 上支持两个 nPartitions。

Superdome 基于模块化组件组。系统建立在基于单元的高带宽、低延迟交叉开关架构之上，可以配置为一个大型对称多处理器（SMP）或几个独立分区。单元或单元板是 Superdome 系统的基本构建模块；它是一个对称多处理器（SMP），包含最多四个处理器和最多 16 GB 的主内存。

在核心层面，nPartitions 支持用户定义的资源分区，并隔离硬件和软件错误。Superdome nPartition 由一个或多个通过高带宽、低延迟交叉开关fabric通信的单元组成。单元被分组为称为*机柜*或*节点*的物理结构。单元中的特殊可编程硬件以强制隔离其他分区操作的方式定义分区的边界。每个分区运行其独立的操作系统。不同的分区可能正在执行不同版本的操作系统。在未来，当支持 Itanium 处理器族（IPF）CPU 时，不同的操作系统，如 HP-UX、Linux 和 Windows，将能够在不同分区中同时得到支持。

每个分区都有其自身的 CPU、内存和 I/O 资源，这些资源由组成该分区的单元的资源构成。可以使用系统管理界面的一部分命令，将一个分区中的资源移除并添加到另一个分区中，而无需物理操作硬件。此外，还支持动态添加新的 nPartitions。向现有 nPartitions 添加或移除单元板不会影响其他分区。

### 处理 nPartitions 和 vPars

为了分配将被分配给 nPartition 内 vPars 的组件，您必须在创建 vPars 的 nPartition 中运行 ioscans。这提供了 nPartition 中可用于 vPars 的所有 I/O 组件、CPU 等的列表。ioscans 不显示其他 nPartitions 中的组件。以下完整的 ioscans 列表显示了我们将创建四个 vPars 的 nPartition 中的所有组件：

```
# ioscans -f

Class I H/W Path Driver S/W State H/W Type Description
-----------------------------------------
root 0 root CLAIMED BUS_NEXUS
cell 0 5 cell CLAIMED BUS_NEXUS
10a 0 5/0 sba CLAIMED sba System
Bus Adapter (804) 0 5/0/0 iba CLAIMED BUS_NEXUS Local PCI
ba 0 5/0/0 iba CLAIMED BUS_NEXUS Local PCI
Bus Adapter (782) 0 5/0/0/0 abso0 CLAIMED INTERFACE PCI
c1 0 5/0/0/0/0 abso0 CLAIMED INTERFACE PCI
Serial (102c1c843) 0 5/0/0/1/0 btlam CLAIMED INTERFACE HP PCI
lan 0 5/0/0/1/0 btlam CLAIMED INTERFACE HP PCI
10/100Base-TX Core 1 5/0/1 iba CLAIMED BUS_NEXUS Local PCI
ba 1 5/0/1 iba CLAIMED BUS_NEXUS Local PCI
Bus Adapter (782) 0 5/0/1/0/0 c720 CLAIMED INTERFACE SCSI C695
ext_bus 0 5/0/1/0/0 c720 CLAIMED INTERFACE SCSI C695
Fast Wide LVD 0 5/0/1/0/0 tgt CLAIMED DEVICE
larget 0 5/0/1/0/0 tgt CLAIMED DEVICE SEAGATE
disk 0 5/0/1/0/0 tgt CLAIMED DEVICE SEAGATE
ST318404LC 1 5/0/1/0/1 tgt CLAIMED DEVICE
target 1 5/0/1/0/1.0 tgt CLAIMED DEVICE
disk 1 5/0/1/0/1.0 dsdsk CLAIMED DEVICE HP
73_4G013734G5JC 1 5/0/1/0/2 acll CLAIMED DEVICE
targets 2 5/0/1/0/2 tgt CLAIMED DEVICE
targets 2 5/0/1/0/2 tgt CLAIMED DEVICE
ctl1 0 5/0/1/0/0.7.0 act1 CLAIMED DEVICE Initiator
targets 3 5/0/1/0/0.15.0 tgt CLAIMED DEVICE
ctl1 1 5/0/1/0/0.15.0 accl1 CLAIMED DEVICE HP
AS4Z72A 2 5/0/2 lba CLAIMED BUS_NEXUS Local PCI
ba 2 5/0/2 lba CLAIMED BUS_NEXUS Local PCI
Bus Adapter (782) 1 5/0/2/0/0 PcltoPcl CLAIMED BUS_NEXUS PCltoPcl
ba 1 5/0/2/0/0 PcltoPcl CLAIMED BUS_NEXUS PCltoPcl
Bridge 1 5/0/2/0/0/4/0 btlam CLAIMED INTERFACE HP AS5506B
lan 1 5/0/2/0/0/4/0 btlam CLAIMED INTERFACE HP AS5506B
PCI 10/100Base-TX 4 Port 2 5/0/2/0/0/5/0 btlm CLAIMED INTERFACE HP A5506B
PCI 10/100Base-TX 4 Port 3 5/0/2/0/0/5/0 btlm CLAIMED INTERFACE HP A5506B
lan 3 5/0/2/0/0/5/0 btlm CLAIMED INTERFACE HP A5506B
PCI 10/100Base-TX 4 Port 4 5/0/2/0/0/5/0 btlm CLAIMED INTERFACE HP A5506B
PCI 10/100Base-TX 4 Port 4 5/0/2 lba CLAIMED BUS_NEXUS Local PCI
Bus Adapter (782) 5 5/0/3/0/0 PcItoPcI CLAIMED BUS_NEXUS PcItoPcI
Bridge 5 5/0/3/0/0 btlm CLAIMED INTERFACE HP A5506B
lan 5 5/0/3/0/0/4/0 btlm CLAIMED INTERFACE HP A5506B
PCI 10/100Base-TX 4 Port lan 6 5/0/3/0/0/5/0 btlm CLAIMED INTERFACE HP A5506B
PCI 10/100Base-TX 4 Port lan 7 5/0/3/0/0/6/0 btlm CLAIMED INTERFACE HP A5506B
PCI 10/100Base-TX 4 Port lan 8 5/0/3/0/0/7/0 btlm CLAIMED INTERFACE HP A5506B
PCI 10/100Base-TX 4 Port lan 8 5/0/4 lba CLAIMED BUS_NEXUS Local PCI
Bus Adapter (782) 6 5/0/4 c720 CLAIMED INTERFACE SCSI C895
ext_bus Fast Wide LVD target disk 5/0/4/0/0.0 5/0/4/0/0.1 c720 CLAIMED DEVICE
sdaa
ST18144LC target disk 5/0/4/0/1.1 sdisk CLAIMED DEVICE HP
73.4G5T5334GSLC 5/0/4/0/0.7 tgct CLAIMED DEVICE
ctel 2 5/0/4/0/0.7.0 accl CLAIMED DEVICE Initiator
target 7 5/0/4/0/0.15 tgct CLAIMED DEVICE
ctel 3 5/0/4/0/0.15.0 accl CLAIMED DEVICE HP
A5272A ba 7 5/6 lba CLAIMED BUS_NEXUS Local PCI
Bus Adapter (781) ext_bus 2 5/6/0/0.0 c720 CLAIMED INTERFACE SCSI C895
Fast Wide LVD target 8 5/6/0/0.0 tgct CLAIMED DEVICE
disk 8 5/6/0/0.0 sdaak CLAIMED DEVICE SEAGATE
ST131844LC target disk 9 5/6/0/1.0 tgct CLAIMED DEVICE
sdial 5/6/0/0.1.0 73.4G5T5334GSLC target disk 10 5/6/0/0.2 sdaik CLAIMED DEVICE HP
73.4G5T5374GSLC 5/6/0/0.2.0 target 11 5/6/0/0.7 tgct CLAIMED DEVICE
ctel 4 5/6/0/0.7.0 accl CLAIMED DEVICE Initiator
target 12 5/6/0/0.15 tgct CLAIMED DEVICE
ctel 5 5/6/0/0.15.0 accl CLAIMED DEVICE HP
A5272A ba 8 5/0/8 lba CLAIMED BUS_NEXUS Local PCI
Bus Adapter (782) fc 9 5/0/9/0/0.0 td CLAIMED INTERFACE HP
Tachyon TL/TS Fibre Channel Mass Storage Adapter 11 5/0/9/0/0.8 fcpp CLAIMED INTERFACE FCP
Protocol Adapter ba 9 5/0/9 lba CLAIMED BUS_NEXUS Local PCI
Bus Adapter (781) ba 10 5/0/9/0/0 PcItoPcI CLAIMED BUS_NEXUS PcItoPcI
Bridge lan 9 5/0/9/0/4/0 btlm CLAIMED INTERFACE HP A5506B
PCI 10/100Base-TX 4 Port lan 10 5/0/9/0/4/0/5/0 btlm CLAIMED INTERFACE HP A5506B
PCI 10/100Base-TX 4 Port lan 11 5/0/9/0/0/6/0 btlm CLAIMED INTERFACE HP A5506B
PCI 10/100Base-TX 4 Port lan 12 5/0/9/0/0/7/0 btlm CLAIMED INTERFACE HP A5506B
PCI 10/100Base-TX 4 Port ba 11 5/0/10 lba CLAIMED BUS_NEXUS Local PCI
Bus Adapter (782) fc 11 5/0/10/0.0 td CLAIMED INTERFACE HP
Tachyon TL/TS Fibre Channel Mass Storage Adapter fcpp 1 5/0/10/0.0.8 fcpp CLAIMED INTERFACE FCP
```




协议适配器

ba 12 5/0/11 lba CLAIMED BUS_NEXUS 本地 PCI 总线适配器 (782)
ext_bus 3 5/0/11/0/0 c720 CLAIMED INTERFACE SCSI 控制器 快速宽差分
target 13 5/0/11/0/0.1 tgt CLAIMED 设备
disk 7 5/0/11/0/0.1.0 sdisk CLAIMED 设备 HP DVD-ROM 3514K
target 14 5/0/11/0/0.3 tgt CLAIMED 设备
tape 0 5/0/11/0/0.3.0 stape CLAIMED 设备 HP C1537A
target 15 5/0/11/0/0.7.0 tgt CLAIMED 设备
ctl 6 5/0/11/0/0.7.0 sctl CLAIMED 设备 启动器
ba 13 5/0/12 lba CLAIMED BUS_NEXUS 本地 PCI 总线适配器 (782)
ext_bus 4 5/0/12/0/0.0 c720 CLAIMED INTERFACE SCSI CB95 快速宽 LVD
target 16 5/0/12/0/0.0 tgt CLAIMED 设备
disk 8 5/0/12/0/0.0.0 sdisk CLAIMED 设备 SEAGATE ST318404LC
target 17 5/0/12/0/0.1 tgt CLAIMED 设备
disk 9 5/0/12/0/0.1.0 sdisk CLAIMED 设备 HP 73.4GST373400SLC
target 18 5/0/12/0/0.2 tgt CLAIMED 设备
disk 10 5/0/12/0/0.2.0 sdisk CLAIMED 设备 HP 73.4GST373400SLC
target 19 5/0/12/0/0.7 tgt CLAIMED 设备
ctl 7 5/0/12/0/0.7.0 sctl CLAIMED 设备 启动器
target 20 5/0/12/0/0.15 tgt CLAIMED 设备
ctl 8 5/0/12/0/0.15.0 sctl CLAIMED 设备 HP AS572A
ba 14 5/0/14 lba CLAIMED BUS_NEXUS 本地 PCI 总线适配器 (782)
ba 15 5/0/14/0/0 cPCItoPCI CLAIMED BUS_NEXUS cPCItoGBT 桥接器
lan 13 5/0/14/0/0/0.0 btlan CLAIMED INTERFACE HP AS5068 PCI 10/100Base-TX 4 端口
lan 14 5/0/14/0/0/0/5.0 btlan CLAIMED INTERFACE HP AS5068 PCI 10/100Base-TX 4 端口
lan 15 5/0/14/0/0/6/0 btlan CLAIMED INTERFACE HP AS5068 PCI 10/100Base-TX 4 端口
lan 16 5/0/14/0/0/7/0 btlan CLAIMED INTERFACE HP AS5068 PCI 10/100Base-TX 4 端口
memory 0 5/5 memory CLAIMED MEMORY 内存
processor 0 5/10 processor CLAIMED PROCESSOR 处理器
processor 1 5/11 processor CLAIMED PROCESSOR 处理器
processor 2 5/12 processor CLAIMED PROCESSOR 处理器
processor 3 5/13 processor CLAIMED PROCESSOR 处理器

请注意，ctl1 本身，就所有目的而言是一个独立的服务器，位于地址 5。有四个处理器，显示在列表末尾，分别位于 5/10、5/11、5/12 和 5/13。我们将把此列表中的许多 I/O 组件分配给我们的四个 vPar，因此您可能会回过头参考该图表。

### 定义和配置四个 vPar

在 Superdome 的 nPartition 中运行 **ioscan** 后，我们确定四个 vPar 中 sẽ 存在以下配置：

#### vPar bvvpard1

- name: bvvpard1
- processors: 最小一个 (绑定) 最大三个 (两个未绑定)
- memory: 2048 MB
- LBA Core I/O: 5/0/0 (0/0 上的所有组件都隐含在内)
- LAN: 5/0/9
- boot disk: 5/0/12/0/0.0.0
- kernel: /stand/vmunix (这是默认值)
- autoboot: off (手动)
- console: 在 5/0/0 的核心 I/O 上

#### vPar bvvpard2

- name: bvvpard2
- processors: 最小一个 (绑定) 最大四个 (两个未绑定)
- memory: 2048 MB
- LAN: 5/0/14
- boot disk: 5/0/6/0/0.0.0
- kernel: /stand/vmunix (这是默认值)
- autoboot: off (手动)
- console: 虚拟

#### vPar extappd2

- name: extappd2
- processors: 最小一个 (绑定) 最大四个 (两个未绑定)
- memory: 2048 MB
- LAN: 5/0/3
- boot disk: 5/0/4/0/0.0.0
- kernel: /stand/vmunix (这是默认值)
- autoboot: off (手动)
- console: 虚拟

#### vPar intappd2

- name: intappd2
- processors: 最小一个 (绑定) 最大四个 (两个未绑定)
- memory: 2048 MB
- LAN: 5/0/2
- boot disk: 5/0/1/0/0.0.0
- kernel: /stand/vmunix (这是默认值)
- autoboot: off (手动)
- console: 虚拟

我们的 vPar 磁盘上拥有所需的所有软件，包括 HP-UX、vPars 软件、补丁等。

既然我们已经获取了 nPartition 中所有组件的完整 ioscans，并规划了我们希望在四个 vPar 中使用的组件，那么我们可以发出 vpcreate 命令来创建这四个 vPar。

```bash
vpcreate -p bvvpard1 -B manual -b /stand/vmunix -a cpu:::1:3 \
-a mem::2048 -a io:5:0/9 -a io:5:0/12 -a io:5:0/12/0.0.0:boot \
-a io:5:0/0 -a io:5:0/11
```

```bash
vpcreate -p bvvpard2 -B manual -b /stand/vmunix -a cpu:::1:4 \
-a mem::2048 -a io:5:0/6 -a io:5:0/14 -a io:5:0/6/0.0.0:boot
```

```bash
vpcreate -p extappd2 -B manual -b /stand/vmunix -a cpu:::1:4 \
-a mem::2048 -a io:5:0/4 -a io:5:0/3 -a io:5:0/4/0.0.0:boot
```

```bash
vpcreate -p intappd2 -B manual -b /stand/vmunix -a cpu:::1:4 \
-a mem::2048 -a io:5:0/1 -a io:5:0/2 -a io:5:0/1/0.0.0:boot
```

这些命令使用本书前面章节中涵盖的相同形式。第 2 章介绍了使用 vpcreate 及其选项的几个示例。请注意，vPar bvvpard1 包含位于 5/0/0 的核心 I/O 卡，这赋予了它控制台访问权限，以及位于 5/0/11 的磁带和 DVD-ROM 接口，因为该 vPar 将用作 Ignite-UX 服务器。

在创建并引导所有四个 vPar 后，我们可以使用 vparstatus -v 检查每个 vPar 的状态并查看其相应组件，如下所示：

```text
# vparstatus -v
[virtual Partition Details]
Name: bvvpard2 <-- vPar bvvpard2
State: Up
Attributes: Dynamic, Manual
Kernel Path: /stand/vmunix
Boot Opts:
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_1025_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_1025_1.png)

```text
[CPU Details]
Min/Max: 1/4
Bound by User [Path]:
Bound by Monitor [Path]: 5.10
Unbound [Path]:

[IO Details]
5.0.6
5.0.12
5.0.0.1.0.0.0 BOOT

[Memory Details]
Specified [Base /Range]:
       (bytes) (MB)
Total Memory (MB): 2048
```

```text
[Virtual Partition Details] <<- vPar bvvpard1
Name:        bvvpard1
State:       Up
Attributes:  Dynamic, Manual
Kernel Path: /stand/vmunix
Boot Opts:
```

```text
[CPU Details]
Min/Max: 1/3
Bound by User [Path]:
Bound by Monitor [Path]: 5.11
Unbound [Path]:

[IO Details]
5.0.9
5.0.12
5.0.12.0.0.0.0 BOOT
5.0.0

[Memory Details]
Specified [Base /Range]:
       (bytes) (MB)
Total Memory (MB): 2048
```

```text
[Virtual Partition Details] <<- vPar extappd2
Name:        extappd2
State:       Up
Attributes:  Dynamic, Manual
Kernel Path: /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max: 1/4
Bound by User [Path]:
Bound by Monitor [Path]: 5.12
Unbound [Path]:

[IO Details]
5.0.4
5.0.3
5.0.4.0.0.0.0 BOOT

[Memory Details]
Specified [Base /Range]:
(bytes) (MB):
Total Memory (MB) : 2048
```

```text
[Virtual Partition Details]
Name: intappd2 -- vPar intappd2
State: Up
Attributes: Dynamic, Manual
Kernel Path: /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max: 1/4
Bound by User [Path]:
Bound by Monitor [Path]: 5.13
Unbound [Path]:

[IO Details]
5.0.1
5.0.2
5.0.1.0.0.0.0 BOOT

[Memory Details]
Specified [Base /Range]:
(bytes) (MB):
Total Memory (MB) : 2048
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_1027_0.png)

我们现在已经配置好四个 vPar，包含我们指定的组件。此 vparstatus 命令的输出与我们在本书中查看的 L 类和 N 类示例的输出相同，只是所使用路径来自 Superdome。

### 控制台

我们可以使用 Ctrl-A 在当前正在工作的 nPartition 的控制台之间切换四个 vPar。我们 nPartition 中位于 5.0/0 的核心 I/O 卡上的控制台被配置为 vPar bvvpard1 的一部分。图 B-2 展示了使用 Ctrl-A 通过控制台在 vPar 之间切换：

![](img/eff8b9287a5f38c5adf538f24aacf29e_1028_0.png)

图 B-2 展示了连续按下 Ctrl-A 四次，以便在名为 intappd2、bvvpard2、bvvpard1 和 extappd2 的四个 vPar 之间切换 vPar 虚拟控制台。正如本书前面所述，当您使用 Ctrl-A 在 vPar 之间切换时，会在括号中提供与控制台连接的 vPar 的名称。

由于每个 vPar 都关联了一张 LAN 卡，我们除了使用图 B-2 中的控制台外，还可以通过网络使用 Telnet 连接到任何 vPar。

请记住，我们使用的控制台是针对整个 Superdome 复合体的。我们选择了配置有四个 vPar 的 nPartition，然后通过 Ctrl-A 在 vPar 之间切换。

我们使用 GSP 的 IP 地址连接到 Superdome 复合体的 GSP。当我们登录到 GSP 时，图 B-3 顶部的屏幕出现。然后我们发出 CO，这会产生 Superdome 中 nPartitions 的控制台列表，如图 B-3 底部所示：




当我们选择配置了 vPar 的 nPartition 时，系统会提供对该 nPartition 的控制台访问权限，我们可以像图 B-2 中那样在 vPar 之间进行切换。在 Superdome 中进行与控制台相关的操作时，您需要先选择要操作的 nPartition，然后按 `Ctrl-I-A` 在 vPar 之间切换。在使用控制台时，按 `Ctrl-B` 会进入 GSP 主菜单。

配置完四个 vPar 后，最终的环境状态如图 B-4 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_1030_0.png)

图 B-4 Superdome nPartition 中的多个 vPar

尽管本附录中使用的 Superdome vPar 软件是新的预发布软件，但其在 Superdome 环境中的运行方式与其他系统中的运行方式相同。这些命令在所有系统中都以相同方式工作，且 vPar 的操作保持一致。

# 索引

## 符号

- `/bin/ksh`, 460
- `"is" (single user)`, 70
- `HOME/dt/ypes/dtwn.fp`, 908, 909
- `HOME/dtprofile`, 940
- `_dt`, 888
- `.dtprofile`, 617, 934
- `.login`, 617
- `.profile`, 365, 617
- `.Xdefaults`, 940
- `l`, 427, 912
- `l/profile`, 365
- `.rhosts`, 537, 685, 849
- `.sh_history`, 365
- `/dev`, 340
- `/dev/mmt/0m`, 392, 399, 400, 404, 410, 411
- `/dev/mmt/0m (for vPars backup)`, 603
- `/dev/vg00`, 487, 498, 503
- `/dev/vg01`, 475
- `/etc/dt/appconfig/types/C/ctwm.fp`, 908
- `/etc/dt/config/C`, 912
- `/etc/dt/config/C/Xconfig`, 940
- `/etc/dt/config/C/Xresources`, 886
- `/etc/dt/config/C/Xsession`, 940
- `/etc/exports`, 536, 537, 538
- `/etc/filesystems`, 851
- `/etc/fstab`, 469, 470, 529, 531, 851
- `/etc/group`, 369, 372, 377, 625
  - `NIS`, 376
- `/etc/hosts`, 557, 818, 835, 846, 847, 866, 867
- `/etc/hosts.equiv`, 685, 848, 849
- `/etc/ifconfig`, 877
- `/etc/inetd.conf`, 677, 681
- `/etc/init.d`, 425, 426
- `/etc/init.d/coldfusion`, 425
- `/etc/inittab`, 148, 428, 429, 430, 431
- `/etc/nsswitch.compat`, 376
- `/etc/nsswitch.conf`, 376, 680, 858
- `/etc/passwd`, 363, 364, 366, 367, 370, 375, 377, 606, 625, 634
  - `description of fields`, 368
  - `NIS`, 376
- `/etc/passwd.nis`, 375
- `/etc/rc.conf.d/coldfusion`, 426
- `/etc/rc.config.d`, 419, 423, 424
- `/etc/rc.config.d/auditing`, 634
- `/etc/rc.config.d/bv`, 419
- `/etc/rc.config.d/coldfusion`, 426
- `/etc/rc.config.d/netconf`, 819, 821
- `/etc/rcl.d`, 427
- `/etc/resolv.conf`, 846, 858
- `/etc/rstab`, 851
- `/etc/vdmp`, 818
- `/home`, 370
- `/init.d/coldfusion`, 427
- `/opt`, 438, 659
- `/opt/HpVmsa/bin/vmsa`, 510
- `/opt/ignite/bin`, 552, 555
- `/opt/ignite/bin/gnite`, 547
- `/opt/mx/bin/smgr`, 726
- `/sbin/dmesg`, 354, 355
- `/sbin/ext2ndfs`, 658
- `/sbin/init`, 148, 429
- `/sbin/init.d`, 422
- `/sbin/init.d/bv`, 417
- `/sbin/init.d/varfb`, 421
- `/sbin/lxextend`, 658
- `/sbin/mksf`, 352
- `/sbin/rc`, 423, 424, 428, 432
- `/sbin/rc0.d`, 420, 423
- `/sbin/rc1.d`, 416, 417, 420, 423, 428, 429
- `/sbin/rc2.d`, 416, 417, 429
- `/sbin/rc3.d`, 427, 429
- `/sbin/rc3.d/K300coldfusion`, 427
- `/sbin/rc3.d/S790coldfusion`, 427
- `/sbin/reboot`, 432
- `/sbin/set_parms arguments`, 128
- `/sbin/shutdown`, 431
- `/sbin/vecheck`, 90, 193
- `/stand`, 109, 110, 212
- `/stand/build`, 213, 219
- `/stand/build/dlkm.vmunix.test`, 199
- `/stand/build/vmunix.test`, 199, 219
- `/stand/dlkm`, 199, 219
- `/stand/dlkm.vmunix.prev`, 219
- `/stand/system`, 91, 193, 204, 219, 380, 492
- `/stand/vmpon.dmp`, 109
- `/stand/vmunix`, 71, 86, 191, 199, 212, 219, 669
  - `defining alternate /Par kernel`, 192
- `/stand/vmunix.prev`, 219
- `/stand/vpdb`, 88, 116, 419
- `/stand/vpmon`, 69, 88, 95, 114
- `/usr/bin/cancel`, 705
- `/usr/bin/disable`, 705
- `/usr/bin/enable`, 705
- `/usr/bin/lp`, 705
- `/usr/bin/lpstat`, 704, 705
- `/usr/conf/gen/config.sys`, 90, 193
- `/usr/conf/gen/mappfile`, 326
- `/usr/conf/master.d`, 195
- `/usr/df/appconf/icons`, 910, 915
- `/usr/df/appconf/types/C/dtwm.fp`, 908
- `/usr/dt/config/Dlogo`, 941
- `/usr/dt/config/C/sys.dtwmrc`, 912
- `/usr/dt/config/C/Xconfig`, 941
- `/usr/dt/config/C/Xresources`, 886, 888
- `/usr/dt/config/C/Xsession`, 941
- `/usr/sbin/sadm/system_prep`, 213
- `/usr/sbin/accept`, 705
- `/usr/sbin/backup`, 404
- `/usr/sbin/inetd`, 684
- `/usr/sbin/oscan`, 342, 652
- `/usr/sbin/padmin`, 705
- `/usr/sbin/lpence`, 705
- `/usr/sbin/pmove`, 705
- `/usr/sbin/psched`, 705
- `/usr/sbin/pshtut`, 705
- `/usr/sbin/pmount`, 658
- `/usr/sbin/reboot`, 433
- `/usr/sbin/route`, 876
- `/usr/sbin/umount`, 658
- `/var/adm/crash.500`, 661, 670
- `/var/adm/rash/var`, 109, 110
- `/var/adm/inetd.sec`, 684
- `/var/opt/lgnite/clients`, 541
- `/var/opt/lgnite/depts`, 559
- `/var/spool/cron/crontabs`, 644, 710
- `*b`, 500
- `*b (in GSP)`, 161

## A

- `absolute (vs. relative CPUs)`, 313
- `Access rights of files`, 371
- `Accounts for Users and Groups in SAM`, 625
- `Add resources to vPars`, 318
- `Adding a Group`, 632
- `Adding a User`, 628
- `Application Startup`, 415
- `Application Users`, 366
- `ARPA Services`, 840
- `Audited Events and Audited System Calls`, 636
- `Audited Users`, 636
- `Auditing and Security in SAM`, 634
- `Authenticated Commands`, 636

## C

- `Cards`, 695
- `Cards in SAM`, 599
- `cbuf command at MON>`, 123
- `cd`, 401, 409, 438, 554
- `CDE`, 885, 887, 927
  - `Activity Light`, 898
  - `Adding Objects to or Removing Objects from the Front Panel`, 904
  - `Advanced Topics`, 926
  - `Application Manager`, 898
  - `Backdrop and Colors`, 903
  - `background`, 891
  - `Calendar`, 896
  - `CDE Basics`, 894
  - `CDE on Solaris`, 899
  - `Changing the Front Panel in Other Ways`, 906
  - `Clock`, 896
  - `Creating Control Buttons, Actions, and File Types`, 914
  - `Customizing`, 902
  - `dterm`, 897
  - `Exit button`, 898
  - `File Manager`, 896
  - `Front Panel Animation`, 910
  - `GREETING`, 886
  - `Help`, 899
  - `Lock Button`, 897
  - `Mail`, 897
  - `Menu Picks for Virtual Partitions`, 887
  - `Modifying Things in Slide-up Subpanels`, 908
  - `on AIX`, 895
  - `on Solaris`, 895
  - `Performance`, 943
  - `Personal Printers`, 898
  - `Sequence of Events When CDE Starts`, 942
- `Backup of vPars`, 379
- `Backup and Recovery in SAM`, 638
- `Backup Using SAM`, 600
- `Base and range (memory on NUMA)`, 85
- `BCH`, 132, 137, 140
- `bdf`, 355, 436, 447, 454, 488, 526, 528, 529, 553
- `Berkeley Commands`, 843
- `BIND`, 852
- `block device`, 351
- `boot`, 172
- `boot boot state of vPars`, 124
- `Boot Console Handler (BCH)`, 129
- `Boot disk`, 86
- `boot disk`, 317
- `Boot in single user`, 70
- `boot state`, 101
- `Boot States`, 123
- `Bootable Devices`, 676
- `Bound`, 105
- `bound`, 83, 84, 98, 311, 319
- `Broadvision`, 366, 416, 437, 438

### Cache

- `Cache Memory`, 354
- `Style Manager`, 898
- `Trash Can`, 899
- `Using Different Fonts`, 923
- `vPar Name`, 887
- `Workspace Area`, 897
- `Workspace Menu`, 888
- `Workspace Switch`, 897
- `xterm`, 889, 899
- `CDE Configuration File Locations`, 938
- `CDE Configuration Files`, 930
- `Central Management Server (in SCM)`, 607
- `character device`, 351
- `chmod`, 490
- `claimed (as part of ioscan)`, 314
- `CM>`, 500

### CO

- `with Superdome`, 995
- `Commands of vPars (table)`, 69
- `Common Desktop Environment (see CDE)`, 885
- `Configurable Parameters`, 660
- `Configuration Variable Scripts`, 423
- `Console`, 87
- `with Superdome`, 994
- `Console and vPars`
- `Ctrl-A`, 331
- `vcn`, 329
- `vcs`, 329
- `control b (in GSP)`, 161
- `Core I/O`, 97
  - `and networking`, 817
- `Core I/O in SAMI`, 597
- `cpio`, 390, 397, 398, 399, 400, 401, 402, 409, 410
- `of vPars`, 383
- `CPU`, 83, 740
- `CPU (in GlancePlus/UX)`, 787, 788
- `CPU in vPars`, 312
- `CPU Report`, 787
- `CPU resources`, 73
- `crash boot state of vPars`, 124
- `Create vPars`, 74
- `Creating Bootable Recovery Archives for vPars`, 536
- `cron`, 710
- `with fbackup`, 404
- `cron (as part of backup)`, 643
- `Cron Jobs`, 710
- `crontab`, 643, 644, 710, 711
- `crontab (as part of backup)`, 643
- `Ctrl A`, 546
- `Ctrl-A`, 102, 103, 331
- `with Superdome`, 994, 995, 997
- `Ctrl-A (and console)`, 87

## D

- `daemon of vPars`, 419
- `Database`, 88
- `dd`, 391, 400, 401, 409, 410
- `Delete resources from vPars`, 318
- `Description of Kernel Parameters`, 222
- `Desktop Management Interface`, 614
- `Device File Naming Convention`, 340
- `Device files background`, 339
- `Device List`, 696
- `Devices in SAM`, 599
- `df (in SCM)`, 607
- `Disk and Terminal Activity`, 688
- `Disk Devices`, 651
- `Disk Mirroring`, 446
- `diskinfo`, 350
- `Disks and File Systems in SAM`, 649
- `Display`, 660
- `dmesg`, 79, 82, 83, 321, 323, 357
- `DMI`, 614
- `DNS`, 852
- `DNS (BIND)`, 678





## D

- vPars 的 down boot 状态，124
- 驱动程序，661
- dt.resources，908
- dtmail，897
- DtRootMenu，912
- dtterm，897
- dtwn.fp，908, 909, 910
- dtwmrc，888, 912
- du，554
- dump，391, 411
- 转储设备，661, 670
- 转储文件，109
- 动态可加载内核模块，209
- 动态可调内核参数，209
- 动态可调内核参数，209

## E

- eight，67
- 八路系统示例，68
- 以太网封装，831
- vPars 系统示例，67
- 执行脚本，422
- extendfs，455

## F

- FAIL（启动和关闭消息），424
- FastBoot，133
- fbakup，207, 390, 403, 404, 405, 406, 407, 408, 411
  - alloptions，404
  - -f 选项，381
  - -g 选项，381
  - 图形文件，381
  - 图形文件排除，381
  - 图形文件包含，381
  - -l 选项，381
  - -O 选项，381
  - vPars 的，381, 382
  - SAM 中 vPars 的，385, 386, 387, 388
  - 向远程设备的 vPars，383
  - -u 选项，381
  - 使用远程磁带驱动器，408
- fbakup 和 ftrecover，403
- file，530
- 文件系统交换，359
- 文件系统，655
- vPars 的文件系统，435
- 文件传输协议，815
- 文件传输协议，840
- find，384, 397, 761
  - 使用 cpio，397, 398, 400
- find（在 SCM 中），607
- ftrecover，403, 405
  - 示例，405, 406
- frecovery，403
- ftrestore，406
  - vPars 的，382
- fsadm，469, 471, 476, 477
- fsck，529, 530, 532
- fstab，475, 529
- ftp，825, 828, 840, 841, 843

## G

- 在 MON> 处获取 auto 命令，121
- GlancePlus，690
- GlancePlus/UX
  - CPU 报告，789
  - CPU 报告，787
  - 磁盘报告，793
  - 内存报告，790
  - mideamon，784
  - 进程列表，782
  - 摘要，795
- grep，510
- GSP，161

## H

- H 类，163
- H-co，168
- H 类命令用于 N 类，168
- H-he，161
- H-ps，166
- H-ss，167
- H 配合 Superdome 使用，995
- H 的 GSP 命令用于 N 类，168
- H-gtop（在 Linux 中），776, 777
- H-Guardian 服务处理器
  - 配合 Superdome 使用，985
- H-Guardian 服务处理器 (GSP)
  - 参见 GSP，161

## I

- vPars 中的 I/O，312
- I/O 中断，83
- iCOD，111
- IEEE802.3，829
- ifconfig，818, 819, 877
- Ignite-UX，535, 538, 540, 547, 557, 558, 567
- Ignite-UX & vPars 烹饪书，546
- 用于虚拟分区的 Ignite-UX 可引导恢复归档，535
- Ignite-UX 图形用户界面，536
- 使用 Ignite-UX 图形用户界面创建 vPar 归档，536
- inetd，684
- init，433
- 初始系统加载 (ISL)，143
- 互联网协议 (IP) 编址，832
- 进程间通信设施状态，690
- ioscan，79, 82, 83, 86, 204, 211, 212, 327, 341, 345, 348, 349, 350, 492, 505, 599, 652, 653, 734, 735, 741
  - 配合 SuperDome 使用，988, 991
- ioscan -f，200, 203, 313, 315, 316, 320
- ioscan -fn，200
- iostat，689, 743, 744, 746, 749
- iostat（在 AIX 中），744
- IP 编址，832
- IPF，115
- IPL，143, 146
- ISL，88, 95, 116, 127, 143, 146, 149, 185
- Itanium 处理器系列，4, 67, 115

## J

- JFS，442
- 日志文件系统 (JFS)，442

## K

- K300coldfusion，428
- 内核，86, 90
- kernel
  - 所有参数的说明，222
  - 构建过程，220
- 内核配置，660
- kill，760, 761
- kill (K)，421
- 终止进程，760
- kmsystem，213, 219
- kmtime，213, 215, 216, 218
  - -1 选项，215
- kmupdate，94, 199, 219

## L

- 1 CPU，740
- LAN，85, 98, 327, 332, 817, 824
  - 同一服务器上不同 vPar 的，819
- LAN 和 vPar，327
- 局域网网卡，82
- lan1，822
  - 系统中第二个 vPar 中的，821
- lanadmin，737, 738, 739
- lanscan，737
- lanscan（vPar 的），736
- LBA，85, 86, 87, 100, 311, 315, 316, 734
  - 网络网卡，817
- 带有两个 vPar 的 L 类，89
- 级别（运行级别），429
- 在 MON> 处使用 lifls 命令，121
- 链接文件，423
- Linux 性能工具，776
- 加载，101
- 加载 vPar 的启动状态，124
- 加载状态，101
- 局域网和 vPar，327
- 局部总线适配器，85, 311
- 在 MON> 处使用 log 命令，122
- 逻辑扩展，444
- 逻辑卷，443, 657
- 逻辑卷管理器背景，441
- 逻辑卷管理术语，442
- lost+found，530
- 低仲裁，70
- lp，704
- 1p 命令，705
- 1pstat，704
- ls，402
  - 在 MON> 处使用 is 命令，122
- 1sdev，345, 347, 348, 349, 351
- 1vchange，453, 497, 498
- 1vcreate，453, 459, 497
- 1vdisplay，447, 453, 454, 464, 466, 486, 490, 497, 499
- 1vextend，455, 476, 497, 498
- 1vlboot，456, 497, 498, 501, 503, 504
- LVM，441
- 1vmerge，456
- 1vmigrate，456
- 1vol，447
- 1vol1，468
- lvreduce，456
- lvremove，457
- lvrmboot，457, 501, 503
- 1vsplit，456
- 1vsync，457

## M

- vPar 的 make_net_recovery，379
- make_config，548, 562
- make_deposits，548, 562
- make_net_recovery，540, 541, 542, 544, 580
- make_recovery，390
- 手册页
  - boot，172
  - hpux，173
  - isl，185
  - make_net_recovery，581
  - pdc，188
- manage_index，549, 562, 563
- 最大（CPU 的），319
- maxuprc，667
- mediainit，532, 533
- 内存，85
- 内存和 vPars，323
- 内存控制器，79
- vPars 中的内存，312
- 内存范围（在 NUMA 上），85
- 内存资源，73
- miidaemon，784
- 中间件，4, 67
- 最小（CPU 的），319
- mk_kernel，94, 199, 219
- mkdir，459
- mkmod，459
- mkst，352, 533
- 修改 vPar，104
- MON，95, 96
- MON>，118, 119
- Motif，927
  - /usr/lib/X11/app-defaults，927
  - system.mmwrc，927
- Motif 配置文件，929
- mxsetup，724

## N

- 名称服务切换，680
- named.conf，857
- netconf，819
- netstat，749, 752, 870, 871, 872, 873, 874, 876, 911
  - netstat 中的常用标志，753
  - netstat 中各字段的说明，749
  - netstat -a，874
  - netstat -l，750, 751
  - netstat -i，749, 871
  - netstat -1（在 AIX 中），751
  - netstat -l（在 Solaris 中），751
  - netstat -n，736
  - netstat -r，753
  - netstat -rn，753
- 网络 netstat，870
- 网络和 vPars，327
- 网络文件系统 (NFS)，849
- 网络文件系统，682
- 网络接口卡，680
- 网络层，831
- 网络服务，681
- 网络
  - /.rhosts，849
  - /etc/hosts，847
  - /etc/hosts.equiv，848
  - 地址类别，833
  - ARPA 服务，840
  - Berkeley 命令，843
  - BIND，852
  - A 类，833
  - B 类，833
  - C 类，833
  - DNS，852
  - 文件传输协议，840
  - ftp，840
  - 主机名映射，846
  - ifconfig，877
  - IP 编址，832
  - ISO/OSI 网络层功能，830
  - landmark，880
  - 链路层，830
  - ndd，882
  - 网络文件系统，849
  - 网络层，831
  - NFS，849
  - nlookup，882
  - 物理层，830
  - ping，867
  - rcp，843
  - 远程复制，843
  - 远程登录，844
  - 远程 shell，844
  - 远程 who，845
  - remsh，844
  - rlogin，844
  - route，876
  - rcpinfo，878
  - rwho，845
  - 子网掩码，835
  - telnet，843
  - 传输层，832
- SAM 中的网络和通信，672
- 网络和 vPars，815
- 网络背景，827
- newfs，471, 472, 533
- newgrp，372
- NFS，435, 849, 850
- SAM 中的无磁盘 NFS 概念，721
- nice，749
- NIS，373, 374, 375, 679
- NIS+，679
- nPartition，985
- nPartitions，987
- nlookup，861
- 数量（CPU 的），319
- NUMA，84, 85

## O

- ODE，144, 145
- 离线诊断环境，144
- OLAR，328
- 操作系统环境，7
- Oracle，366

## P

- 分区管理器，686
- passwd -r nis，377
- 密码
  - 特性，369
  - 密码，368
- PATH，432, 547, 552
- 路径（CPU 的），319
- PDC，127, 132, 137, 139, 140, 141, 149, 564
- pdc，188
- PDC 命令，141
- 性能和虚拟分区，733
- 性能背景，742
- SAM 中的性能监视器，686
- 执行恢复，645
- SAM 中的外围设备，595, 693
- 权限，371
  - 执行，371
  - 读取，371
  - 写入，371
- 物理内存，326
- 物理扩展，443
- 物理卷，443
- ping，868, 869
- POSIX shell，367
- 主交换，358
- 进程控制，707
- 进程列表（在 GlancePlus/UX 中），782
- SAM 中的进程管理，706
- CPU 使用率最高的进程，690
- 处理器相关代码 (PDC)，129
- 处理器硬件路径，82
- 处理器集，111
- 处理器和 vPars，318
- 提示符
  - PS1，365





## P

- ps, 754, 758
- ps 中的标题，758
- ps-et, 420, 510, 540, 754, 756
- ps-et (在 AIX 中), 755
- ps-et (在 Solaris 中), 754
- ps-etl, 758

- rpicnf, 879
- 运行级别，429
- 在远程系统上运行 SAM，718
- rwho, 845
- rwhod, 845

- ADDR, 759
- NI, 759
- SZ, 759
- WCHAN, 759
- PSI, 365
- psets, 111
- pvchange, 448
- pvccreate, 448, 459, 460, 495, 506
- pvdisplay, 447, 448, 449
- pvmove, 450
- pvremove, 506
- pwd, 401, 438

## S

- S790coldfusion, 428
- SAM, 367
- SAM 与虚拟分区，591
- vPar 中的 SAM，593
- sar, 766
- -b-f 示例，768
- -b 选项，768
- -d-f 示例，769
- -d 选项，769
- -f 选项，767
- -o 选项，766
- 选项，766
- -q-f 示例，770
- -q 选项，770
- -u-f 示例，767
- -u 选项，767
- -w-f 示例，771
- -w 选项，771
- sar 和 ioscann 与磁盘（在 vPar 中），734
- sar -b-f, 768
- sar -d-f, 734, 735
- sar -d, 769
- sar -f-l, 770
- sar 系统活动报告器，766
- sar -u -f, 767
- sar -w -f, 771
- SBA, 311, 315, 734
- SBA (系统总线适配器), 79
- MON> 处的 scan 命令，119
- 安排备份，639
- 安排 Cron 任务，710
- SCM 和 vPar，607

## R

- RAM, 82
- RAM (在 GlancePlus 中), 791
- NUMA 上的范围 (内存)，85
- rc1.d, 416, 417
- rc2.d, 416, 417
- rcp, 848, 849
- reboot, 433
- 相对 (对比绝对 CPU)，313, 337
- 远程系统 (用于备份)，602
- remsh, 397, 410, 848
- 与 cpio 一起使用，397, 400, 401
- 与 cpio 和 vPar 一起使用，384
- 与 dd 和 cpio 一起使用，410
- 重新生成，430
- 恢复，411
- 受限 SAM 生成器，623
- root, 365
- route, 876
- SAM 中的例常任务，711

## S

- SCM 命令，730
- SCR, 608
- SCR 命令，614
- scrconfig, 608, 609, 610
- scrlifter, 613
- scstatus, 610
- serviewer, 610
- 次要交换空间，359
- 安全 Web 控制台，149, 153, 154, 155, 156, 157, 160
- 连接，150
- IP 地址，151
- 登录屏幕，158
- 菜单，159
- 选择性文件删除，713
- Sequenizer 脚本，423
- 服务控制管理器 (SCM) 和 vPar，607
- 服务控制管理器 (SCM) 概述，724
- ServiceGuard, 457
- set_params, 86, 816
- setboot, 74, 86, 87, 125
- setboot 命令和 vPar，125
- setboot 表，87
- setenv, 616
- showmount, 762, 851
- -a, 763
- -a 选项，851
- -d, 763
- -d 示例，763
- -d 选项，851
- -e, 763
- -e 示例，763
- -e 选项，851
- 选项，763
- vPar 的 shut 启动状态，124
- shutdown, 431, 432, 433, 531
- 关机脚本，415
- SIGKILL, 761

- 信号，760
- 编号，761
- SIGHUP, 761
- SIGINT, 761
- SIGKILL, 761
- SIGQUIT, 761
- SIGSTOP, 761
- SIGTERM, 761
- 单用户模式，70
- 大小 (内存)，85
- SAM 中的软件管理，718
- software.hp.com, 547
- 假脱机配置，705
- stand/system, 208
- stape, 351
- start, 421, 426
- 作为启动的一部分，418
- start (S), 421
- start_msg, 426
- 启动和关机文件 (组织结构图)，424
- 启动和关机消息，424
- FAIL, 424
- N/A, 424
- OK, 424
- 启动和关机脚本，422
- 应用程序的启动，415
- vPar 的启动，419
- 启动脚本，415
- statdaemon, 358
- vPar 的状态，74
- vPar 状态表，102
- 创建虚拟分区的步骤，76
- 创建 vPar 的步骤，74
- stop, 421, 426
- 作为启动的一部分，418
- stop_msg, 426
- 严格分配策略，446
- strings, 530
- 子网掩码，835

## S

- 子系统，671
- 摘要，1, 109
- Superdome, 985
- Superdome vPar，985
- 交换空间，358, 659, 764
- 交换空间，359
- swap -l, 765
- swapinfo, 488, 765, 766
- swapper, 358
- swinstall, 547
- swlist, 439
- 同步，530
- vpd 的同步，116
- sys.dtwmrc, 911
- sys.resources, 907, 933
- sys.x11start, 929
- sys.Xdefaults, 929
- sysdef, 210, 211
- 系统访问，684
- 系统活动，690
- 系统总线适配器，79
- 系统配置存储库 (SCR) 和 vPar，608
- 系统配置存储库命令，614
- 系统日志文件，715
- 系统属性，691
- 系统安全策略，637
- 系统关机，717
- system.wmwrc, 929
- system_prep, 213

## T

- vPar 命令表，69
- 磁带驱动器，698
- tar, 390, 392, 393, 394, 395, 396, 409
- 创建和归档，392
- 提取内容，392
- 获取目录，392
- TCP/IP, 829

- 拆卸卡，69
- Telnet 和 vPar，825
- telnet, 815, 816, 825, 826, 828
- 终端和调制解调器，699
- SAM 中的时间，721
- timex, 772, 773
- top, 107, 322, 323, 336
- top (在 Linux 中), 776, 777
- 总计 (或 CPU 数量), 319

## U

- umount, 530, 659
- uname, 77
- 未绑定，83, 84, 89, 311, 319, 320
- 不间断电源，700
- 唯一的主机名 (主机名 vs. vPar 名称), 592
- UNIX 网络，828
- 未使用的组件，68
- vPar 的 up 启动状态，124
- up 状态，101
- uptime, 735
- SAM 中的用户，363
- user /etc/passwd, 363
- 设置，365
- 用户，361, 362
- users 应用程序，366
- SAM, 367
- 用户和 SAM (在 vPar 中), 605

## V

- vcn, 196, 198, 329, 330
- vcs, 196, 198, 329, 330
- Veritas 卷管理器，441
- vg00, 436, 484, 492, 493, 495, 497, 503

- vgcfbackup, 451
- vgcfrestore, 451, 472
- vgchange, 451
- vgcreate, 451, 459, 460, 463
- vgdisplay, 447, 451, 452, 463, 464, 484, 492, 493, 495
- vgexport, 452
- vgextend, 452, 459, 463, 495
- vgimport, 452
- vgreduce, 452
- vgremove, 453
- vgscan, 453
- vgsync, 453, 473
- vhand, 358
- 虚拟内存，358
- 虚拟内存活动，691
- 虚拟分区文件系统，435
- 虚拟分区监视器，3, 66, 733
- 虚拟分区启动，419
- 虚拟分区和设备，311
- 虚拟内存 (在 GlancePlus 中), 792
- vmsa, 521
- vmstat, 692, 747, 748
- vmstat (在 AIX 中), 748
- vmstat (在 Linux 中), 748
- vmstat (在 Solaris 中), 747
- vmunix, 204
- 卷，443
- 卷组，443
- 卷组，659
- vpar 驱动程序，92
- vPar 名称，88
- vpar_driver, 198
- vparboot, 70, 100, 101, 116, 544, 545, 546, 547, 550
- vparcreate, 71, 84, 85, 86, 88, 94, 95, 97, 99, 191, 312, 320, 546
- 与 Superdome 一起使用，992
- vparcreate (与 setboot 一起使用), 86
- vparhb (vPar 心跳守护进程), 419

- MON> 处的 vparinfo 命令，119, 120
- vparload, 69, 70, 95, 96, 116, 117, 118, 546
- 从备用内核引导，192
- vparload -all, 117
- MON> 处的 vparload 命令，120
- vparload 表单，117
- vparload -p, 117, 118
- vparmodifier, 71, 73, 84, 106, 108, 109, 118, 320, 328, 335, 337, 816
- 永久修改 vPar 内核，192
- vparremove, 71, 110
- vparreset, 72, 110
- vparresources, 72, 312
- vPar 命令，69
- vPar 心跳守护进程，415
- vPar 名称，592
- vPar 状态，74
- vparstatus, 72, 96, 97, 98, 99, 100, 104, 105, 106, 108, 203, 316, 318, 327, 328, 333, 334, 335, 336, 337, 380, 594, 595, 816, 889
- vpartition, 72
- vpdb, 116, 420
- vpdb 同步，116
- vpdb, 420
- vphb (vPar 心跳守护进程), 420
- vpmon, 95, 114, 115, 116, 117, 191, 196, 197
- vpmon.1, 109
- vpmon.imp.1, 109
- vassist, 527
- vxdef, 527
- vxdg, 516, 527
- vxdisk, 515, 516, 520, 523, 527
- vxdiskd, 527
- vxdump, 411, 412, 413

- 示例，411

- vxedit, 527

- vxinstall, 506, 507, 509, 510

- vxmake, 527

- vxmend, 527

- vplex, 527

- vxprint, 516, 519, 520, 525, 527

- vxrestore, 411, 412, 413

- 示例，411, 412

- vxsd, 527

- vxstat, 527

- vxtrace, 527

- vxrelocate, 527

- VxVM, 510, 513, 514

- VxVM 命令，527

- vxfol, 527

## W

- what, 530

- WINSTALL, 545, 547, 549

- 与 cpio 一起使用，397

- www.docs.hp.com, 551, 569

- www.hp.com, 4, 67

- www.software.hp.com, 551

## X

- X 窗口系统，926

- sys.x11start, 926

- Xlib, 926

- Xt, 926

- X*devices, 929

- X*pointerkey, 929

- X*screens, 907, 929

- Xaccess, 935

- Xconfig, 935

- Xfailsafe, 935

- xosview (在 Linux 中), 776, 777

- XP 256, 441, 457

- Xreset, 935

- Xresources, 923, 935

- Xservers, 935

- Xsession, 934, 935

- Xstartup, 935, 936

- xterm, 899, 913

- xwd, 899

## Y

- yppasswd, 377

2002 年 5 月 2 日 1 号收到

图书馆研究所财产  
636 US 一号公路  
北布鲁斯威克, NJ 08902

| 日期 | 到期日 |
| :--- | :--- |
| | |
| | |
| | |
| | |
| | |
| | |
| | |
| | |
| | |
| | |
| | |
| | |
| | |
| | |





## www.informit.com

- 免费、深入的文章和补充资料
- 在您需要的时候，掌握所需技能
- 从行业领先的书籍、电子书和培训产品中自由选择
- 在您需要时获取答案——来自现场专家或 InformIT 的综合资源库
- 获取行业认证，提升您的职业生涯

![](img/eff8b9287a5f38c5adf538f24aacf29e_1054_0.png)

今日访问 *InformIT*，获取来自 PHP TR 的优质内容

## HP 电脑新闻

![](img/eff8b9287a5f38c5adf538f24aacf29e_1055_0.png)

想第一时间了解惠普公司（Hewlett-Packard Company）发明的新产品、服务和解决方案吗？

需要有关新 HP 服务的信息，以帮助您实施新产品或现有产品吗？

正在寻找 HP 针对您业务中特定挑战的最新解决方案吗？

HP 电脑新闻为您呈现 HP 的最新动态！

![](img/eff8b9287a5f38c5adf538f24aacf29e_1055_1.png)

订阅的 4 种简便方式，且**免费**：

1. **传真** 填写并传真下方表格至 (651) 430-3388，或
2. **在线** 在 www.hp.com/go/compnews 进行在线注册，或
3. **电子邮件** 填写下方信息并发送至 horders@earthlink.net，或
4. **邮寄** 填写并邮寄下方表格至：
   - Twin Cities Fulfillment Center
   - Hewlett-Packard Company
   - P.O. Box 408
   - St. Paul, MN 55082

![](img/eff8b9287a5f38c5adf538f24aacf29e_1055_2.png)

### 立即回复，第一年**免费**！

姓名  
职位

公司  
部门/邮寄代码

地址

城市  
州  
邮政编码

电子邮件  
签名  
日期

- 请在下方注明您的行业：
  
  - [ ] 会计
  - [ ] 教育
  - [ ] 金融服务
  - [ ] 政府
  - [ ] 医疗/医学
  - [ ] 法律
  - [ ] 制造业
  - [ ] 出版/印刷
  - [ ] 在线服务
  - [ ] 房地产
  - [ ] 零售/批发分销
  - [ ] 技术
  - [ ] 电信
  - [ ] 交通和旅游
  - [ ] 公用事业
  - [ ] 其他：

![](img/eff8b9287a5f38c5adf538f24aacf29e_1056_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_1056_1.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_1056_2.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_1056_3.png)

HP 的世界级教育和培训提供包括以下内容的实战教育解决方案：

- Linux
- HP-UX 系统和网络管理
- 高级 HP-UX 系统管理
- 利用先进互联网技术的 IT 服务管理
- Microsoft Windows NT/2000
- Internet/Intranet
- MPE/IX
- 数据库管理
- 软件开发

HP 新的 IT 专业人员认证计划为特定的 IT 职位提供严格的技术资质认证，包括 HP-UX 系统管理、网络管理、Unix/NT 服务器和应用管理以及 IT 服务管理。

![](img/eff8b9287a5f38c5adf538f24aacf29e_1056_4.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_1056_5.png)

## 保持与 PHP TR 在线的最新动态同步！

我们努力保持对专业计算机科学和工程领域最新发展的前沿把握。以下是您访问 **www.phptr.com** 时会发现的一些内容。

- **重点领域** 提供我们最新的书籍、丛书、软件、月度特色、相关链接以及其他有助于您完成工作的有用信息。
- **优惠、优惠、优惠！** 来我们的促销版块看看零售商为您独家提供的最新特价。
- **需要找书店吗？** 很可能：附近有出售大量 PTR 书籍的书店。在 **www.phptr.com** 上寻找附近的 Magnet 书店。
- **PHP TR 有什么新动态？** 我们不仅为专业社区出版书籍，我们也是其中的一部分。查看我们的会议日程，加入作者聊天，获取您感兴趣主题的最新评论和新闻稿。
- **今日订阅！** 加入 **PHP TR 的每月电子邮件新闻通讯！**

希望了解您感兴趣领域的最新动态？在我们的网站上选择一个目标类别，我们将为您通报该领域内最新的 PHP TR 产品、作者活动、评论和会议。

访问我们的邮件室，今日订阅！**http://www.phptr.com/mail_lists**

### 虚拟分区命令摘要

| 命令 | 描述 |
| :--- | :--- |
| `ISL>` | 从 `ISL` 加载虚拟分区监视器：`ISL> hpxuc /stand/vpmon` |
| 初始系统加载提示 `MON>` | 若要直接从 `ISL>` 加载虚拟分区，使用：`ISL> hpxuc /stand/vpmon vparload -p vPar_name` |
| `MON>` | 这是从 `ISL` 加载的：`ISL> hpxuc /stand/vpmon` |
| 虚拟分区监视器提示（另见 `vparload` 命令。） | 要从 `ISL` 加载备用数据库，使用：`ISL> hpxuc /stand/vpmon -D db_file`<br>要从 `MON` 加载一个 vPar，使用：<br>`MON> vparload vPar_name`<br><br>许多其他命令可以从 `MON` 发出。键入 `help` 或 `?` 以列出。<br>（命令包括：`scan`、`vparinfo`、`ls`、`log`、`getauto`、`lifls`、`cbuf`、`cat`。） |
| `vparload`<br>仅从 `MON>` 提示加载虚拟分区。 | 形式 1: `vparload -all`<br>形式 2: `vparload -auto`<br>形式 3: `vparload -p vp_name [-b kernelpath] [-o "boot_options"] [-B hardware_path]`<br><br>要从 `MON>` 启动虚拟分区：<br>`MON> vparload -p vPar_name`<br><br>要从 `MON>` 启动所有虚拟分区：<br>`MON> vparload -all`<br><br>要从 `MON>` 以单用户模式启动虚拟分区：<br>`MON> vparload -p vPar_name -o "-1s"`<br><br>在 `MON>` 中可发出的其他选项包括：<br>`-1q` (低仲裁), `-1m` (维护模式) |
| `vparboot`<br>仅从命令行启动虚拟分区。 | 形式 1: `vparboot -p vp_name [-b kernel_path] [-o boot_opts]`<br>          `[-B boot_addr]`<br>形式 2: `vparboot -p vp_name -1ignite_kernel`<br><br>要从命令行启动虚拟分区：<br>`# vparboot -p vPar_name`<br><br>要从命令行以单用户模式启动虚拟分区：<br>`# vparboot -p vPar_name -o "-1s"` |

| 命令 | 描述 |
| :--- | :--- |
| **vparcreate** | 形式: `vparcreate -p vp_name [-B boot_attr] [-D db_file]`<br>`[-S static_attr]`<br>`[-b kernel_path] [-o boot_opts] [-a src] [-a...]` |
| 创建虚拟分区。 | 创建一个总共有三个处理器（`num`）、两个绑定（`min`）、2048MB RAM、所有组件在 0/0 上、启动磁盘在 0/0/1/1.2.0、内核为 `/stand/vmunix`、autolinux、磁盘和控制器在 0/0/4/0 的虚拟分区：<br><br>```<br># vparcreate -p vpR_name -a cpu::3 -a cpu::2:4<br>-a mem::2048MB -a io::0/0 -a io::0/0/1/1.2.0:boot<br>-b /stand/vmunix -B auto<br>```<br>注意：<br>- 必须在创建虚拟分区之前或之后在卷上加载 `HP-UX 11i`。如果在创建 `vPar` 之后加载 `HP-UX 11i`，则使用 `vparboot -p vp_name -I ignite_kernel` 来加载 11i。<br>- `/stand/vmunix` 是默认值，无需指定。<br>- 未将 `vPar` 设置为 `static`，意味着其可以稍后修改。<br>- `CPUs` 总数为三个（`num`），两个绑定（`min`），最多两个未绑定（`max`）。 |

| 命令 | 描述 |
| :--- | :--- |
| **vparmodify** | `vparmodify -p vp_name [-B boot_attr] [-D db_file] [-S static_attr]`<br>`[-b kernel_path] [-o boot_opts] [-P new_vp_name]` |
| 修改虚拟分区的属性。<br><br>（注意 `CPUs` 是相对于当前数量添加的，`-a, -a cpu::2` 在当前 `CPUs` 数量基础上添加两个 `CPUs`。`-m cpu::3` 指定 `CPUs` 的绝对数量为三个。） | `[-a src] [-a...]`<br>`[-m src] [-m...]`<br>`[-d src] [-d...]`<br><br>要在路径 `1/09` 添加处理器（将此处理器添加到已分配的处理器中）：<br>``` # vparmodify -p vPar_name -a cpu::1/09 ```<br>要指定三个处理器的绝对数量：<br>``` # vparmodify -p vPar_name -m cpu::3 ``` |

| 命令 | 描述 |
| :--- | :--- |
| **vparremove** | `vparremove -p vp_name [-D db_file] [-f]` |
| 删除虚拟分区。 | 要删除当前运行数据库中的虚拟分区：<br>``` # vparremove -p vPar_name ``` |

| 命令 | 描述 |
| :--- | :--- |
| **vparreset** | `vparreset -p vp_name [-h|-q] [-q] [-f]` |
| 重置虚拟分区。 | 模拟在 Crl+B 提示下的 TOC 操作来重置虚拟分区。如果没有 `-h` 选项，默认命令仅模拟 TOC。<br><br>``` # vparreset -p vPar_name ```<br><br>要强制对虚拟分区执行硬重置：<br><br>``` # vparreset -p vPar_name -h -f ``` |





# UNIX/HP-UX 虚拟分区

## hp-ux 虚拟分区

马蒂·波尼亚托夫斯基

**vPars：最大化 HP 9000 利用率、灵活性和可管理性的突破性解决方案**

使用虚拟分区（vPars），您可以将几乎任何 HP 9000 系统转变为多个“虚拟”计算机，每台计算机运行自己的 HP-UX 实例及相关应用程序——从而在任何企业环境中显著提高效率、灵活性、可用性和可管理性。现在，全球领先的 HP-UX 专家兼畅销书作者马蒂·波尼亚托夫斯基提供了一份关于 vPars 的全面指南，涵盖了您成功使用这项突破性技术所需的一切。本书通过实际示例，涵盖了所有必要的 vPars 命令和管理技术。

- 分析您的系统以确定 vPars 中使用的组件
- 加载 HP-UX 和 vPars 软件
- 使用 **vparcreate** 创建 vPars
- 使用 **vparboot** 和 **vparload** 启动 vPars
- 使用 **vparmodify** 修改 vPars
- 使用 **vparstatus** 查看 vPars 详细信息
- 使用 **vparremove** 移除 vPars
- 使用 Ignite-UX、备份、用户、启动选项等定制 vPars 环境
- 汇总所有 vPars 命令的可拆卸卡片

无论您是想整合服务器、提高利用率、快速响应负载变化、防范软件故障，还是在同一台服务器上运行生产和测试系统，vPars 都能实现这些目标——而马蒂·波尼亚托夫斯基的逐步说明让这一切变得简单。

**马蒂·波尼亚托夫斯基** 自 1981 年起就开始接触 UNIX。在过去十五年中，他一直在纽约地区的惠普担任系统工程师，与众多行业的客户合作。他撰写了十二本由 Prentice Hall 出版的与 UNIX 相关的书籍，均由 Prentice Hall PTR 出版，其中包括 *HP-UX 11i 系统管理手册和工具包*。

$49.99 美元 $77.99 加元
Prentice Hall
Upper Saddle River, NJ 07458
www.phptr.com
Hewlett-Packard® 专业书籍
Prentice Hall 系列
www.hp.com/hpbooks

![](img/eff8b9287a5f38c5adf538f24aacf29e_1061_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_1061_1.png)

ISBN 0-13-035826-9
90000

DEVY 理工学院
新泽西州北布鲁斯维克
Hp Ux 虚拟分区

36107000490319

