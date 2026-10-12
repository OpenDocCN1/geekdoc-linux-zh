
一种文本分页器，允许你在文档中前后滚动（使用 `less` 命令读取纯文本文件）。你可以通过输入 `less` 命令，后跟文件的完整目录路径规范及文件名，或 *路径名* 来启动该命令，例如：

```
$ less /usr/share/doc/httpd-2.0.50/README
```

若要读取此文件的压缩版本，请同样使用 `zless` 命令：

```
$ zless /usr/share/doc/attr-2.4.1/CHANGES.gz
```

按下回车键后，你可以使用光标键在文档中滚动。按 Q 键退出。

如果 HOWTO 文档为 HTML 格式，你可以简单地使用网络浏览器（如 Firefox）来读取信息。或者，如果你是通过控制台阅读，可以使用 links 或 lynx 等纯文本网络浏览器，例如：

```
$ links /usr/share/doc/stunnel-4.0.5/stunnel.html
```

links 浏览器提供下拉菜单，可通过点击屏幕顶部的区域访问。你也可以按 Q 键退出。

如果文档为 PostScript 格式（文件名以 .ps 结尾），你可以使用 gv 客户端像这样读取或查看文档：

```
$ gv /usr/share/doc/iproute-2.4.7/ip-crefs.ps
```

最后，如果你想阅读便携式文档格式（文件名以 .pdf 结尾）的文档，请使用 xpdf 客户端，例如：

```
$ xpdf /usr/share/doc/xfig/xfig-howto.pdf
```

![](img/774d40fd20903495c5cd00e2efad3f33_59_0.png)

## Fedora 开发者与文档

如果你对协助 Fedora 项目感兴趣，你可以通过测试 beta 版本、编写文档以及为核心或贡献软件仓库提供软件来提供帮助。你应该具备一些安装 Linux 发行版的经验，希望协助将文档翻译成不同语言，或者能够使用各种软件项目管理系统，例如 CVS。

除了 Fedora 的未来版本外，你还可以参与旧版本 Linux 的持续支持工作。Fedora Legacy 项目旨在为已停止支持的 Fedora 版本提供安全更新和关键 bug 修复。Fedora Core 1 是第一个被迁移到 Fedora Legacy 项目的版本，随着其运营生命周期的结束，未来的版本也会被逐步迁移过来。由于 Red Hat 将 Fedora 视为测试新技术以可能纳入 Red Hat Enterprise Linux 的沙盒，因此它经常更新，且版本之间会相互取代。粗略指南是，每个版本大约支持 11 个月，届时它将被迁移至 Fedora Legacy 项目。你可以在 http://fedoralegacy.org 找到该项目——请记住，这是一个社区支持的项目，因此依赖于像你我这样人的贡献。

在 Fedora Core 开发过程中报告问题也是流程的一部分！欢迎提交 bug 报告，并按照 Tammy Fox 和 Havoc Pennington 的《Fedora 项目开发者指南》中概述的准则提交，该指南位于 http://fedoraproject.com/participate/develpers-guide/。

为 Fedora 编写文档需要一定的纪律性以及使用开源文档发布工具的经验。你可以通过浏览 http://fedoraproject.com/participate/documentation-guide/ 来了解有关此流程的更多信息。

邮件列表也是讨论 Fedora 的出口或论坛。这些列表按类别划分。例如，Fedora Core 的普通用户可以在 fedora-list 邮件列表中讨论问题。Beta 测试人员通过 fedora-test-list 交流，开发人员通过 fedora-devel-list 交流，文档贡献者通过 fedora-docs-list 交流。可以通过向 name_of_the_list-request@redhat.com 发送邮件来订阅邮件列表。

### 参考资料

本书每章都包含一个“参考资料”部分，列出指向正文中涵盖的额外或相关信息的链接。你可以使用这些链接来更多了解 Fedora、Linux 和相关技术。你还可以使用“参考资料”部分的材料来构建自定义书签集，以便在浏览或研究更多关于 Linux 的信息时使用。

- http://www-1.ibm.com/linux/—来自 IBM 的信息，关于其在 Linux 硬件、软件和服务方面的努力与产品。
- http://www.dwheeler.com/sloc—David A. Wheeler 关于 GNU/Linux 当前状态、规模、价值、组件及市场渗透率的出色白皮书。
- http://fedoraproject.com—Fedora 项目的主页，由 Red Hat 赞助，是你更多了解 Fedora 的起点。
- http://www.redhat.com/solutions/info/casestudies/—政府和大型企业 Red Hat 客户列表。
- http://fedorah.redhat.com/docs/—包含指向当前 Fedora 文档和发布说明的链接的网页。
- http://www.tldp.org—获取最新通用 Linux FAQ、指南和 HOWTO 文档更新的最权威起点。
- http://www.ciac.org/ciac/—美国能源部计算机事件咨询网站，详细列出了不仅涉及 Red Hat Linux，还涉及许多其他操作系统的安全问题及修复方法。该网站对联邦软件承包商、开发人员和系统管理员非常有用。
- http://www.justlinux.com/—新手 Linux 用户可以浏览此网站以更多了解 Linux。
- http://fedorafaq.org/basics/—另一个提供 Linux 和 Fedora 轻松入门的网站。

# 第 2 章

# 准备安装 Fedora

- 规划你的 Fedora 部署
- 硬件要求
- 为安装过程做准备
- 安装前后及安装期间的分区
- 使用 Fedora 的 kickstart 安装方法
- 参考资料

在安装前进行适当的准备和规划，日后可能会带来巨大的回报。如果你正在使用 Fedora Core 部署 Linux，你需要决定如何将其投入使用。

首次安装 Linux 对于缺乏经验的用户或系统管理员来说可能显得令人望而生畏，但本章将向你展示，如果你做一些简单的安装前规划和决策，安装可以变得多么简单。磁盘分区可能是安装过程中最陌生的部分之一，但它是配置多平台系统的关键步骤。如你将在本章中所学，当你花时间提前规划时，磁盘分区也是一个可管理的过程。

在本章中，你将学习如何为高效、有效的 Fedora Core 安装做准备。本章以一个考虑事项清单开始，帮助你规划安装后如何使用 Linux，以便你可以在安装过程中做出正确的选择。本章还概述了使用 Linux 的一些基本硬件要求（并针对本书 CD-ROM 和 DVD 上的 Fedora Core 发布版本提供了一些具体说明），并突出了一些你可以提前规划并避免的潜在硬件问题。本章还带你浏览安装过程的通用概述，并提供深入的规划建议，用于分区你的硬盘以支持不同的配置。

正如你即将了解到的，Fedora 是一个灵活的 Linux 发行版，可以适应多种硬件配置，并且可以通过多种方式进行安装。

## 规划你的 Fedora 部署

在规划安装的具体步骤之前，你需要决定要执行的部署类型。计算需求决定了成功部署所需的硬件和软件解决方案的类型，但在深入之前，需要提出并回答一些棘手的问题，例如，“你将如何使用 Fedora？” 你会在下面的章节中更详细地了解这些问题。这些章节还包括一个你可以用作部署前规划清单的表格，以及有关规划安装的一些最后建议。

### 商务考量

选择用于商业目的的操作系统是一个重要决定。迁移或采用新的硬件或软件平台可能对组织产生即时的和长期的影响。在考虑搬迁时，决策过程中没有万能公式，自由职业顾问、小企业主、中型企业、公司和其他大型商业组织将拥有不同的计算资源、目标和需求。对许多企业而言，计算机是商业运营的关键，有时甚至是核心组成部分。

> **注意**
> 浏览 Red Hat 迁移中心 http://www.redhat.com/business/utol/success/ 阅读关于使用 Red Hat 企业 Linux 产品开展业务的成功案例、市场分析报告和技术报告。

幸运的是，Linux 足够灵活，可以提供全部或部分迁移，并支持当今商业运营所需的所有主要计算服务。一些更传统的服务包括电子邮件、文件服务器、网络服务（包括防火墙）、打印、网页托管（基于 Internet 和 Intranet）以及数据库服务器。如果你需要商业支持，Red Hat 可以提供其中一项、多项或全部服务。Linux 也可以分阶段投入使用，以缓解迁移问题，例如培训或支持。

围绕 Linux 部署的一些想法、问题和顾虑列在表 2.1“部署 Fedora”中。一个考虑因素是 Fedora 的使用背景。换句话说，新的操作系统将如何与你的现有硬件和软件需求相匹配？另一个考虑因素是管理层在用户愿意更改或采用新软件环境方面的共识水平。然而，如果尽可能让用户对过渡过程不可察觉（例如，当基于 Linux 的网页、文件或打印服务取代现有服务器时），这个问题就可以被绕过。

转换成本是另一个需要考虑的问题。Fedora 提供灵活性和可靠性，但转换到新平台可能产生意外成本。Linux 的批评者有时指出额外的总拥有成本（TCO）因素，如支持和培训，并认为这些问题会显著增加 Linux 迁移的成本。虽然可能存在一些额外的支持成本，但再次强调，培训可能不是问题，特别是如果 Linux 是隐形部署的话。隐性费用可能会通过低许可成本得到抵消，

