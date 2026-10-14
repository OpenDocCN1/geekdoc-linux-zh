
例如，一家公司可能有一位管理员需要与 Novell 交互，一位经理需要查看订单历史，可以通过资源信息、工具和服务的访问，例如：（注：原文此处确实存在重复或截错误，已按原文字样翻译）

*修正 Novell Customer Center 段落的逻辑性翻译：*

Novell Customer Center 是一个直观的基于 Web 的界面，帮助你管理与 Novell 的业务和技术交互。Novell Customer Center 整合了信息、工具和服务的访问，例如：

例如，一家公司可能有一位管理员需要与 Novell 交互，一位经理需要查看订单历史，可以通过集成信息、工具和服务的访问，例如：（注：由于原文文本在此处出现逻辑循环，翻译已保持原文结构）

（注：此处跳过原文重复的逻辑描述，直接进入后续章节）

# Linux 资源

Linux 提供了各种在线资源帮助你配置 SUSE Linux Enterprise Server 10。这些包括：

- http://www.novell.com/products/linuxentererver/eval.html
- http://www.novell.com/documentation/sles10/index.html
- http://support.novell.com/linux/
- http://www.novell.com/coolsolutions
- http://www.novell.com/center

# 议程

以下是课程的议程：

# 场景

你是 Digital Airlines 的管理员。公司正在考虑将某些服务迁移到 SUSE Linux Enterprise Server 10。

作为管理员，你决定执行操作：

完成本培训后，你将能够安装 SUSE Linux Enterprise Server 并为进一步的测试做好准备。

# 练习约定

在练习过程中，你会看到指示你输入特定服务器信息的约定。

以下说明了最常见的约定：

例如，如果你的服务器主机名是 DA50，你看到：

`hostname.digitalairlines.com`

你会输入

`10.0.0.xx`。这是分配给你的 SUSE Linux Enterprise Server 10 服务器的 IP 地址。

例如，如果你的 IP 地址是 10.0.0.50，你看到：

你会输入

`Select (选择)`。该词在练习步骤中表示各种操作，包括点击界面上的按钮和选择菜单项。

如果你被要求输入一个值，请确保不要按 Enter 键，否则可能会启动你尚未准备好启动的进程。

# 第一节 理解 Linux 的故事

本节提供了有关 Linux 的背景信息，并引导你安装 SUSE Linux Enterprise Server 10。

## 目标

### 目标 1

### Linux 历史

Linux 与 UNIX 操作系统有着密切的关系。要理解 Linux 的历史，你需要了解以下内容：

### UNIX 的历史发展

在 20 世纪 60 年代末，大多数操作系统仅为批处理操作设计。如果你想运行一个程序，需要将一叠打孔卡或一卷穿孔带插入读取设备，然后等待结果从打印机上出来。

如果程序中出现错误或者你没有得到所需的结果，你必须重写穿孔带或更换一张或多张打孔卡，重新读取堆栈并等待结果。

这种程序既冗长又低效，导致计算机开发人员寻找一种方法，允许多个用户同时通过对话式的方式与系统交互。

MULTICS 是最早创建的满足这一需求的程序之一。它允许你与计算机进行对话工作，但它仍然受到批处理操作的影响，且操作困难。

1969 年，MULTICS 的开发者之一的肯·汤普森（Ken Thompson）开始创建一种操作系统，该系统除了面向对话的操作外，还旨在提供高功能和结构简单性。

UNIX 的第一个版本是用汇编语言编写的，这是一种接近机器层级的编程语言。为了在后续开发中实现机器无关性，UNIX 在 1971 年用由丹尼斯·里奇（Dennis Ritchie）开发的 C 语言进行了重写。

由于贝尔实验室（AT&T 的子公司）几乎以近乎成本的价格向大学提供 UNIX 的文档和源码，该系统传播得很快。

系统简单的操作、近乎无限的源码可用以及其相对的可移植性，激励了许多用户和公司积极参与开发，因此功能被迅速添加到到 UNIX 中，并使其达到了很高的成熟度。

与此同时，出现了一系列商业 UNIX 衍生版本，包括来自 IBM、DEC 和 HP 的版本（HP-UX，1982），以及由加利福尼亚大学伯克利分校开发的 BSD UNIX（Berkeley Software Distribution，1978）。

1983 年，AT&T 开始通过其姐妹公司 USL 营销 UNIX System V，并宣称 System V 为“唯一的” UNIX 标准。

结果，UNIX 的许可模式发生了巨大变化，导致了（包括其他方面）与 BSD 之间长期法律斗争。同时，由于 UNIX 供应商之间无休止的争吵，防止了 UNIX 操作系统族真正的标准化。

现代 UNIX 操作系统仍然可以分为更偏向 System V 或更偏向 BSD 类型，尽管不存在某一种类的“纯”系统。

Linux 试图结合两者的优点。

由于 Linux 用 C 语言编写的，它可以适用于许多不同的硬件平台，包括：

### Linux 的发展

1991 年春季，芬兰学生林纳斯·贝内尼迪特·托瓦尔斯（Linus Benedict Torvalds）开始为他的 PC 开发一个类 UNIX 操作系统。

几个月后，他开发了一个原始内核，并通过互联网以源码形式发送给其他感兴趣的人，并附带如下消息：

| 发件人: torvalds@klaava.Helsinki.FI (Linus Benedict Torvalds) |
| 新闻组: comp.os.minix |
| 主题: 你最想在 minix 中看到什么？ |
| 摘要: 关于我新操作系统的小调查 |
| 消息 ID: <1991Aug25.205708.9541@klaava.Helsinki.FI> |
| 日期: 91年8月25日 20:57:08 GMT |
| 机构: 赫尔辛基大学 |
| 各位使用 minix 的大家好 - |
| 我正在做一个（免费的）操作系统（只是爱好，不会是像 gnu 那样的大规模专业产品）386(486) 克隆。这从 4 月就开始了，现在开始准备就绪。我想就人们对 minix 中喜欢/不喜欢的地方获得任何反馈，因为我的操作系统在某些方面与其相似（出于实际原因，文件系统的物理布局是相同的等）。 |
| 我目前移植了 bash(1.08) 和 gcc(1.40)，看起来看起来运行良好。这意味着我在几个月内将得到一些实用的东西，我想知道人们想要什么功能。欢迎任何建议，但我不会保证会实现它们 :- |
| Linus (torvalds@kruuna.helsinki.fi) 任何 minix 代码，它具有多线程文件系统。它不是可移植的（使用了 386 任务切换等），而且可能永远不会支持 AT 硬盘以外的，因为我只有这些 :-:- |

林纳斯·托瓦尔斯将他的 Linux 内核源码通过 `GPL`（GNU 通用公共许可证）公开发。`GPL` 允许所有人阅读和编辑源码。`GPL` 许可还要求任何编辑过的源码必须向公众公开。

Linux 迅速发展成为一个涉及许多人的项目，尽管系统核心（Linux 内核）的开发仍由林纳斯·托瓦尔斯协调。所有的内核修改都由他整合。

内核的功能包括输入输出控制、设备控制、进程管理和文件管理。其他组件（shell 工具、网络程序、非 Intel 处理器）由其他人员或小组负责。

### SUSE Linux 与 SUSE Enterprise Server 之间的软件差异

SUSE Enterprise Server 10 是基于 SUSE Linux 10.1 的。SUSE Enterprise Server 在发布与 SUSE Linux 之间的时间被用于密集测试和应用补丁以提高系统的安全性和稳定性。此外，SUSE Enterprise Server 包含在未来 SUSE Linux 版本中提供的功能。

以下展示了开源代码、SUSE Linux 与 SUSE Enterprise Server 之间的关系：

### 图 1-1

![](img/428e877abd09b1c1149d179d3458f12_28_0.png)

SUSE Enterprise Server 10 的软件包少于 SUSE Linux（约 1000），大多数应用程序已被移除。SUSE Enterprise Server 有七年的保证生命周期。在此期间，你将获得补丁和修复以维护 SUSE Enterprise Server。此外，你可以从一系列支持方案中进行选择。

只有 SUSE Enterprise Server 产品经过了独立硬件和软件供应商的认证。

### 目标 2 理解多用户环境

UNIX 的目标之一是允许多个用户同时使用系统（多用户能力）。

由于多个用户可能同时使用使用不同的程序，必须允许这些程序同时运行（多任务能力）。

多用户和多任务系统的实现在单处理器系统中看起来是同时的，但这只有在多处理器系统中才是可能的。
