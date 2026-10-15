
# Linux DevOps 实用指南：使用 Linux 命令、Terraform、Docker、Vagrant 和 Kubernetes 构建并部署 DevOps 流水线

![](img/cover.jpg)

![image](img/cover.jpg)

![](img/line.jpg)

![](img/line.jpg)

![](img/logo.jpg)

[www.bpbonline.com](http://www.bpbonline.com)

**2021 年第一版**

Ph: 23254990/23254991

![](img/logo1.jpg)

由 Manish Jain 为 BPB Publications 出版，地址：20 Ansari Road, Darya Ganj, New Delhi-110002，并在 Repro India Ltd, Mumbai 打印。

[www.bpbonline.com](http://www.bpbonline.com/)

# 献给*我的家人和朋友*

# 关于作者

**Alisson Machado de Menezes** 是一位经验丰富的大数据 DevOps 工程师。在过去的十年里，他曾担任不同的职位，如开发人员、运营分析师、支持分析师、DevOps 工程师、IT 经理、技术负责人，现在深耕大数据领域。他在巴西的 Python Brasil、The Developers Conference、自由软件国际展等活动中进行过多次演讲，并为一些私人公司提供服务。他还教授过 Python 编程、敏捷基础设施、MongoDB、Openshift、Kubernetes、DevOps 和 DevSecOps 等课程。他拥有 Linux 系统管理员 (`LPIC-1`)、Linux 工程师 (`LPIC-2`)、Suse 认证 Linux 管理员 (`SUSE CLA`)、`LPIC – OT` DevOps 工具工程师、Exin – DevOps 专业人员认证，并在加拿大学习过英语。

2019 年，Alisson 搬到了德国，在欧洲汽车营销领域开启了新挑战，旨在助力未来的出行，我们正努力成为电动汽车的先驱。

在工作之余，Alisson 尝试维护一个博客，分享他参与过的项目经验；有空时会旅行、徒步并尝试不同类型的啤酒。

# 关于评审员

**Leonardo Mendes** 目前在 Cogna 担任软件可靠性工程师，是技术创新团队的核心成员。他专注于 FOSS（自由和开源软件）项目。他热爱培训，并在教育项目中工作过，协调培训团队交付 Linux、DevOps、云和大数据培训，还参与了实施项目，并教授关于 Linux、DevOps 和云的课程。

他毕业于计算机网络专业，并拥有云计算硕士学位（MBA）。

# 鸣谢

我想感谢几位在撰写本书期间给予我持续和不断支持的人。首先，我想感谢我的家人，他们教育了我，教我如何变得独立和坚强。Leonardo Mendes 是本书的技术审稿人，也是我最好的朋友之一。Gabriela Dias 是这十年 IT 经验中我遇到的最好的领导，也是我心中一个人的榜样。Juergen Bohn 是带我来到德国的老板，为我在欧洲开启了许多大门和数以虚计的机会。如果没有生活中的这些人，我永远无法完成这本书。

如果没有 BPB Publications 的支持，这本书就不可能问世，他们在我写作期间给予了我支持和关注。

最后，我要感谢上帝，他赋予我智慧、力量以及所有的道路，让我处于现在的位置。

# 前言

DevOps 是 2017 年搜索率最高的词。在我看来，当我们停止在 IT 团队之间建立边界，开始协作和共同工作以实现共同目标时，可以认为是 IT 领域的一场革命。此外，我们还拥有 DevOps 思维中包含的所有技术手段，利用自动化来缩短上市时间并更快速地交付高质量的软件和服务。

我进入领域是因为对 IT 的一切都好奇。我还是一个青少年时就开始学习网络安全，因为我想成为一名黑客。随后，我学习了操作系统、计算机编程、数据库、网络、安全等。这些术语为后来 DevOps 的出现做好了准备。

如今，DevOps 工程师必须掌握这些技能。在我的日常工作中，例如，我必须编写脚本自动化云服务器的安装，这可以通过许多方式实现。大多数情况下针对特定需求使用`Python`；对于更通用的场景，我使用`Ansible`。我使用`Jenkins`进行调度自动化、创建流水线。

我在巴西生活期间还编写过其他课程，包括 MongoDB、DevSecOps、Python 开发、Docker 和 OpenShift 以及敏捷基础设施。在过去的十年里，我在不同的公司、不同的场景中工作。

现在我的职位是大数据 DevOps 工程师，我将 DevOps 自动化知识应用于大数据场景，创建流水线并自动化数据湖、数据流水线、治理规则等。

本书的主要目标是为当今市场的 DevOps 工程师提供所需的信息和技能，根据我的十年经验提供最常用技术的基本概述和步骤：

- **第 1 章** 本章介绍了本地机器上的虚拟化概念，旨在让你创建实验室、测试新技术、在不破坏生产环境的情况下模拟环境，并用于学习。

- **第 2 章** 本章向你介绍了一些基础 bash 命令，因为我们知道如今 Linux 已经不再是一个加分项，而是云和高可用性领域人员的必备要求。

- **第 3 章** 在这里，我们设置了一些服务，如数据库和 Web 服务器，搭建最常见的安装，即我们所谓的 Lamp（Linux Apache Mysql PHP）。

- **第 4 章** 反向代理通常在你只有一个公 IP 且有多个站点运行在私有结构之后使用。当你不使用云服务（如 Azure 或 Amazon）时，你可以自己设置 Nginx 并实现负载均衡，或者将连接传递到私有服务器以确保安全。

## 第 5 章 Docker 是 DevOps 工程师栈中领先技术之一。在这里，我们将学习非常基础的知识，但足以让你创建镜像并将其提交到注册表进行部署。

## 第 6 章 Vagrant 对于那些尚未使用 Docker 的人来说也是一个非常有用的工具。我们知道许多公司仍在使用本地基础设施。这些设施也需要自动化。本章旨在教你如何创建自己的自动化脚本。

## 第 7 章 在你的笔记本电脑上完成工作后，本章将教你如何使用云服务和`CLI`（命令行界面）创建实验室和基础设施，重点关注自动化。

## 第 8 章 多云是一个无法避开的话题。在学习了命令行界面以及不同云提供之间的之间的之后，`Terraform`将为你提供一个单一的工作流，可以在任何提供商上创建基础设施。

## 第 9 章 此时，我们已经创建了大量的代码。因此，我们需要使用`Git`来保存它们，并创建文档以及我们基础设施的不同版本。

## 第 10 章 流水线（Pipelines）是在你的自动化上创建工作流的方式，逐步定义依赖关系，`Jenkins`是为此最著名的开源工具，在本章中我们将学习更多关于它的知识。

## 第 11 章 在我看来，`Kubernetes`将成为应用部署的标准方式，如果不给你介绍至少它的基础知识，我就无法写完这本书。

## 第 12 章 一旦你所有的基础设施都准备好进行扩展和自动化，我们需要找到一种集中日志的方法，因为当你只有几台服务器时，你可以逐个检查日志。但当我们有成千上万台服务器时，为了审计和调试目的，我们必须在服务器中集中日志，`Elasticsearch`、`Fluentd`和`Kibana`就是这方面的参考。

# 下载彩色图片

请点击链接下载本书的`彩色图片`：

# [`rebrand.ly/aeb0pwp`](https://rebrand.ly/aeb0pwp)

# 勘误表 (Errata)

我们对 BPB Publications 的工作感到自豪，并遵循最佳实践以确保内容的准确性，为我们的订阅者提供愉快的阅读体验。我们的读者是我们的镜子，我们利用他们的反馈来反映并改进出版过程中可能发生的任何人为错误（如果有的话）。为了让我们保持质量并帮助我们联系可能因不可预见错误而遇到困难的读者，请通过以下邮箱联系我们：errata@bpbonline.com

BPB Publications 家族非常感谢您的支持、建议和反馈。

你知道 BPB 为出版的每本书都提供电子书版本，并提供 PDF 和 ePub 文件吗？你可以在 [www.bpbonline.com](http://www.bpbonline.com) 升级到电子书版本，作为纸质书客户，你有权获得电子书版本的折扣。请通过 business@bpbonline.com 与我们联系获取详情。

在 [www.bpbonline.com](http://www.bpbonline.com)，你还可以阅读免费技术文章集，订阅一系列免费新闻邮件，并接收 BPB 书籍和电子书的独家折扣和优惠。

# BPB 正在寻找你这样的作者

如果你对成为 BPB 的作者感兴趣，请访问 [www.bpbonline.com](http://www.bpbonline.com/) 并于今天申请。我们曾与成千上万像你这样的开发者和技术专业人士合作，帮助他们与全球技术社区分享见解。你可以进行通用申请、申请我们正在招募作者的特定热门话题，或提交你自己的想法。

本书的代码包也托管在 GitHub 上：[`github.com/bpbpublications/Hands-on-DevOps-with-Linux`](https://github.com/bpbpublications/Hands-on-DevOps-with-Linux)。如果代码有更新，将在现有的 GitHub 仓库中更新。

我们从丰富的书籍和视频目录中还有其他代码包，地址为 [`github.com/bpbpublications`](https://github.com/bpbpublications)。快去看看吧！

# 盗版声明

如果你在互联网上发现任何形式的我们作品的非法复制品，如果你能向我们提供地址或网站名称，我们将不胜感激。请通过 business@bpbonline.com 联系我们并提供材料链接。

# 如果你有兴趣成为作者

如果你在某个领域拥有专长，并且对编写或贡献书籍感兴趣，请访问 [www.bpbonline.com.](http://www.bpbonline.com/)。

# 评论

请留下评价。当你阅读并使用这本书后，为什么不在购买它的网站上留个评价呢？潜在读者就可以查看并利用你的无偏意见来做出购买决策，我们 BPB 可以了解你对我们产品的看法，我们的作者也可以看到你对书的反馈。谢谢！

欲了解更多关于 BP 的信息，请访问 [www.bpbonline.com.](http://www.bpbonline.com/)。

# 第 1 章

# 开始使用 Linux

本章将向你介绍 Linux 世界，重点关注服务器。因此，我不会在桌面端进行解释。你将看到关于 Linux 的解释、为什么你应该了解它、它的基本概念以及很多命令。我是一个技术人员，所以做好准备，因为你将看到如何亲手搭建你的实验室！

## 结构

在本章中，我们将讨论以下主题：

*   什么是 Linux

    *   发行版

    *   服务器

*   搭建你的环境

    *   安装`VirtualBox`

    *   安装 Linux 系统

*   通过`SSH`访问

*   `Bash`简介

    *   实用命令

    *   基础文件以及如何编辑它们

    *   自定义你的 shell

    *   安装包

## 目标

学习完本单元后，你应该能够：

*   理解 Linux 的基础知识

*   选择你喜欢的发行版

*   安装你的虚拟机

*   访问任何远程 Linux 服务器

## 什么是 Linux？

在我看来，如果你买了这本书，你可能对 Linux 是什么有了基本概念，并且已经知道为什么要学习它。总结来说，Linux 是一个具有开源代码的操作系统，工作与著名的 Windows 类似，但不属于任何公司。那么，代码是如何开源的？每个人都可以通过这个网站下载 Linux 核心：[`www.kernel.org/`](https://www.kernel.org/)，如果你感兴趣想看看源代码，可以在这个链接找到：[`git.kernel.org/`](https://git.kernel.org/)。

Linux 取这个名字是因为它的创造者 *Linus Torvalds*。前三个字母是 Linus 的首字母，后两个字母来自另一个名为 Minix 的操作系统，它是由一个名叫 *Andrew Tanenbaum* 的人创建的。

你经常会看到 Linux 与其他字母绑定在一起，比如 GNU。这是因为当 Linus Torvalds 创建 Linux 时，他使用了许多由 GNU 项目创建的工具，[`www.gnu.org/home.en.html`](https://www.gnu.org/home.en.html)。GNU 项目始于自由软件会创始人理查德·斯托曼（Richard Stallman），[`www.fsf.org`](https://www.fsf.org)。开源意味着什么？这意味着由 GNU 项目编写的每个软件，其代码对任何想要对其进行开发的人开放。那么，Linus Torvalds 是如何使用 GNU 项目工具的呢？他采用同样的开源哲学，并使用 GNU 项目的工具发布了 Linux 系统。这解释了 GNU/Linux 这个术语的由来。

## 发行版

由于 Linux 是开源的，许多个人和公司创建了他们自己的 Linux 版本，这些被称为“发行版”。任何拥有计算机编程知识的人都可以创建自己的 Linux 发行版。一个例子是由巴西程序员卡洛·莫里托（Carlos Morimoto）创建的 Kurumin Linux，可以在此链接找到：[`distrowatch.com/table.php?distribution=kurumin`](https://distrowatch.com/table.php?distribution=kurumin)。遗憾的是，它已经停止维护了，因为维护自己的发行版并不是一项轻松的任务。你必须担心更新、新版本、新软件、错误修复以及无数可能的事情，对于单个人来说，在没有报酬的情况下投入所有这些精力基本上是不可能的。因此，决定在你的基础设施中安装哪种发行版是一个重要的课题。想象一下这种情况：你开始使用一个发行版，一年后，它停止维护了，你必须重新安装你包含 300 多台服务器的整个基础设施。作为专业人士，我们不能让这种情况发生。

关于我们想为基础设施选择的发行版，有多个选择，但其中一些是最常用的，原因我将在下文中进一步解释：

*   **RedHat Enterprise Linux (红帽企业级 Linux)**：由于红帽公司的存在，它是最著名且最企业化的发行版。它是 Linux 世界最著名的公司之一。它拥有强大的支持、频繁的更新，并且与红帽软件有 100%的兼容性，例如`JBoss`、`OpenStack`、`RedHat Enterprise Virtualization Manager`以及许多其他选项。但是，使用`RHEL`需要向公司购买订阅并付费。否则，你既无法收到任何更新，也无法访问仓库。

*   **Community Enterprise Operating System (社区企业操作系统)**：`CentOS`是`RHEL`的社区版本。在那些选择不使用付费版本并希望使用红帽软件社区版本的公司中，它是最常见的发行版。

*   **SUSE**：它是 Novell（微软）的发行版，是一个不错的选择，因为微软是全球最大的公司之一。因此，它停止维护的概率为零，你将始终获得公司发布的更新和新软件。它还有一个名为`OpenSUSE`的社区版本，其特性与`CentOS`相同。

*   **Debian**：对于那些更深参与社区且不希望绑定到任何公司（如之前提到的发行版）的人来说，这是一个选择。`Debian`100% 由社区维护，是我们拥有的最古老的发行版之一。此外，它运行在许多服务器上，非常稳定可靠，经常被公司和普通用户使用。

*   **Ubuntu**：这个发行版是由`Canonical`公司在非洲制作的，他们曾向全球分发 CD，让人们更多地了解 Linux 并在桌面上运行它。`Canonical`最初的目标用户是终端用户。因此，我认为对于桌面来说，Ubuntu 是最常用的发行版，而对于服务器，则是`CentOS`。`Ubuntu`有一个服务器版本，那是我最喜欢的发行版。这就是为什么我使用`Ubuntu`来写这本书。但你在这里学到的知识可以适用于所有的发行版。

## 服务器

服务器无非是计算机。它们通常比 PC 更强大，是为了特定目的而创建和安装的。例如，我们可以安装一个 Linux 服务器来充当 Web 服务器。换句话说，就是在上面运行网站，比如 Facebook、Amazon 或 Google。它也可以作为数据库服务器，我们可以在上面安装`PostgreSQL`、`SQL Server`、`MySQL`、`Oracle`或其他的；作为文件服务器，公司将所有数据存储在其中，在许多情况下，是将所有数据放在一起。一个例子就是我们所说的`LAMP`，Linux Apache MySQL PHP。通常，当我们有一个 Linux 系统（在这种情况下是 Web 服务器）、`Apache`、一个数据库服务器（`MySQL`）和一个编程语言解释器（在这种情况下是`PHP`）时，我们称之为`LAMP`。我们也可以将其称为“栈”（Stack）。栈意味着一组你可以用来解决问题的工具集。我最喜欢的栈之一是`NPM`、`Nginx`、`Python`和`MongoDB`。我一直用它来解决我工作公司的许多问题。这个栈可以安装在服务器上（虚拟或物理均可），我们将在接下来的章节中介绍。



# On-premise 与云

On-premise（本地化）是一个经常用于安装在公司基础设施内部的服务器术语，很多时候位于数据中心，有时位于系统管理员的桌下。当我们使用`OpenStack`或`oVirt`等工具在物理服务器上创建虚拟机时，`VMs`也可以运行在本地化基础设施中。这是公司为了获得更强的韧性、灵活性并利用资源而采用的策略。一个例子是，如果你必须更换数据中心的一或多台服务器（因为它们太旧了，无法与其它服务器相同的性能），你可以将`VMs`从一台服务器迁移到另一台。更换物理机器，并在安装新机器后，将所有`VMs`迁移回来。

Cloud（云）用于描述虚拟服务器安装在其他东西的基础设施内部。在大多数情况下，像`AWS`、`Azure`和`GCP`这样的公司有自己的本地化基础设施并将其租给我们。因此，我们不需要担心维护，例如在磁盘故障时更换磁盘、在服务器过时时更换服务器，甚至不需要电力和互联网。此外，你可以在工作日结束后关闭它们并在第二天重新启动，从而节省成本。所有这些提供商只根据机器运行的时间收取费用。否则，你只需为存储付费。

# 结论

现在我们已经对服务器、虚拟机、Linux和发行版有了简要的解释，我们准备好开始动手实践了。让我们从设置第一个Linux环境开始，了解基础知识，以及更多内容。

# 设置你的环境

Linux专业人员最重要的任务之一是具备设置不同类型环境的能力，运行Web服务器、数据库、文件系统以及来自不同供应商的各种服务。在本章中，我们将学习从哪里下载Linux发行版、如何安装虚拟化工具来创建测试环境、如何创建基础镜像以便于创建新实验室，以及如果你的测试环境崩溃了（这在我们学习新知识时经常发生），会发生什么。

要在你的笔记本电脑或个人电脑上运行虚拟机（VM），你需要检查你的处理器架构是否为64位。此规格可以在笔记本电脑制造商或处理器制造商处找到。检查完此设置后，你需要在设备的BIOS或UEFI中启用虚拟化。此配置可能因设备而异，但在大多数情况下，可以在`Advanced`或`Security`选项中找到名为Intel Virtualization Technology的项目。

# 安装VirtualBox

现在我们有很多虚拟化工具可以在笔记本电脑上运行，例如VMware Player、KVM、QEMU、HyperV。但在我看来，VirtualBox是最简单的一个，并且包含了我们创建实验室所需的所有功能。

要安装VirtualBox，你需要从官方网站下载最新版本：[`www.virtualbox.org/wiki/Downloads`](https://www.virtualbox.org/wiki/Downloads)

我使用的是Windows系统，所以我将下载Windows版本。但如果你有Linux基础知识或正在使用MacOS，步骤基本上是相同的。

下载文件后，双击它，安装步骤基本上就是`Next`、`Next`和`Finish`。出现的第一个窗口只是解释你正准备安装VirtualBox：

![](img/Figure-1.1.jpg)

**图 1.1**

第二个窗口对于你选择所有资源非常重要，因为很多时候，主要在你需要在PC和虚拟机之间共享文件，甚至配置网络时需要它们：

![](img/Figure-1.2.jpg)

**图 1.2**

以下是关于快捷方式的基本选项，如果你想将它们添加到桌面：

![](img/Figure-1.3.jpg)

**图 1.3**

在这一步，安装程序会要求你提供`Admin Rights`（管理员权限），因为VirtualBox将创建一个`bridge interface`（桥接接口）。该接口负责宿主机与虚拟机之间的通信，没有它，你无法从虚拟机访问互联网：

![](img/Figure-1.4.jpg)

**图 1.4**

![](img/Figure-1.5.jpg)

**图 1.5**

![](img/Figure-1.6.jpg)

**图 1.6**

安装完成后，你就可以打开VirtualBox，主界面将所示：

![](img/Figure-1.7.jpg)

**图 1.7**

现在，我们准备好设置第一个Linux环境了。VirtualBox有很多选项供你配置和探索。但我现在不会关注它，因为我们有一个Linux系统要安装。

# 安装Linux系统

由于我之前提到过我们将使用Ubuntu服务器来完成此书中的所有操作，你可以从此链接下载最新版本：[`ubuntu.com/download/server`](https://ubuntu.com/download/server)

然后，下载此文件：`ubuntu-18.04.3-live-server-amd64.iso`

现在，让我们开始安装。第一步是打开VirtualBox，点击`New`，在新窗口中输入`UbuntuServer`，如下例所示：

![](img/Figure-1.8.jpg)

**图 1.8**

点击`Next`后，你需要定义你想在虚拟机中使用的内存量。Linux系统通常不需要很多内存即可运行，但在你安装服务并测试它们之后，将需要更多内存。目前，1GB就够了。然后点击`Next`：

![](img/Figure-1.9.jpg)

**图 1.9**

在这一部分，创建一个`New Disk`（新磁盘）。该磁盘本质是你硬盘上的一个文件，虚拟机将在其中存储所有数据。点击`Create`，你会看到以下窗口：

![](img/Figure-1.10.jpg)

**图 1.10**

VDI是VirtualBox使用的标准类型。如果你打算将此机器导入其他虚拟化工具，可以更改类型。例如，`VMDK`是VMware使用类型。点击`Next`：

![](img/Figure-1.11.jpg)

**图 1.11**

这个窗口非常重要。在实验室中，你将始终使用`Dynamically allocated`（动态分配）选项，因为VirtualBox会创建一个小文件并根据磁盘使用增加大小。

`Fixed Size`（固定大小）建议用于生产环境，因为虚拟化工具会为你的虚拟机保留该空间。即使你没有使用所有分配的磁盘空间，它也能避免虚拟空间超过`Physical Space`（物理空间）。在某些情况下，当你在生产环境中使用`Dynamically allocated`大小时，你会超过`Storage`（存储）的总空间，但你的虚拟机仍有剩余空间。我以前遇到过这种情况，真的很难处理。选择此选项的另一个原因是，它可以避免虚拟化工具在每次写入后重新计算磁盘空间。当你对每次写入使用`Dynamically allocated`类型时，系统将计算实际大小以及在达到定义限制之前需要增加多少：

![](img/Figure-1.12.jpg)

**图 1.12**

在这里，你可以定义虚拟机数据的存储位置和磁盘大小。对我们来说，10GB足够运行我们的测试：

![](img/Figure-1.13.jpg)

**图 1.13**

现在，你的虚拟机创建好了！

# 安装你的Linux系统

一旦我们准备好了所有前提条件（例如创建虚拟机并定义所有配置），是时候安装系统了。双击你的虚拟机。会出现以下屏幕：

![](img/Figure-1.14.jpg)

**图 1.14**

此虚拟机中尚未安装任何操作系统。你需要通过点击黄色文件夹来从Ubuntu网站下载ISO：

![](img/Figure-1.15.jpg)

**图 1.15**

点击`Add`，并选择你已经下载的ISO文件。选择它，点击choose，然后点击`Start`：

![](img/Figure-1.16.jpg)

**图 1.16**

现在，选择你的语言。即使我曾住在巴西、加拿大，现在住在德国，我也总是选择`English`。选择此选项无疑会避免很多关于排序的问题，例如标点符号、特殊字符等：

![](img/Figure-1.17.jpg)

**图 1.17**

此选项取决于你的键盘布局。你可能需要根据你目前所在的国家对其进行更改。我的键盘布局是美国布局，所以我选择此选项：

![](img/Figure-1.18.jpg)

**图 1.18**

现在，你什么都不需要做。只需按`Done`，因为我们将使用默认配置。这一步非常重要，因为Ubuntu会在安装期间下载一些更新。所以，确保PC和虚拟机都有网络连接是重要的：

![](img/Figure-1.19.jpg)

**图 1.19**

如果你是在工作时间进行此操作，并且你的公司通过代理访问互联网，现在是你配置的时候了。只需输入代理URL并按`Done`：

![](img/Figure-1.20.jpg)

**图 1.20**

在这里，你可以定义Ubuntu下载更新的镜像站（Mirror）。如果你有网络连接，它将选择离你最近的镜像。在我的情况下，我使用的是德国仓库：

![](img/Figure-1.21.jpg)

**图 1.21**

多年前，我会向你详细解释Linux上的重要目录，这是在目录和分区之间划分磁盘的最佳方法。但现如今，当我们与虚拟机一起工作时，这已经不那么重要了。我们可以把Amazon EC2实例作为一个例子。它们甚至没有SWAP分区。如果你缺少空间，只需在根分区中增加空间并清理你的服务器即可。另一个重要的点是`/var`目录。我现在不会深入讨论这个话题，但它是存储Linux系统日志的目录。因此，它们经常占用你大量的空闲空间，我们必须经常清理它。多年前，我会要求你将其划分为不同的分区。但今天，我们有工具将日志发送到`Log Server`，我们可以每天从本地机器上删除日志。不过，请选择`Use An Entire Disk`（使用整个硬盘）：

![](img/Figure-1.22.jpg)

**图 1.22**

现在，选择安装操作系统的物理设备，并按`Enter`：

![](img/Figure-1.23.jpg)

**图 1.23**

接下来的屏幕显示了磁盘是如何分区的。我们可以看到有一个`Physical Device`（物理设备）、`VBOX_HARDDISK`，它被分为两个部分。启动分区是启动系统所必需的，也是引导加载程序安装的地方。

`root`分区，也称为`/`。只需选择`Done`（完成）：

![](img/Figure-1.24.jpg)

**图 1.24**

在这里，我们将创建第一个用户，然后我将定义以下数据：

*   你的名字：`alisson` - 这只是你的真实名字，但不会被用于任何地方。
*   你的服务器名称：`devops` - 这是你机器的主机名
*   选择用户名：`alisson` - 这就是你访问服务器时实际使用的用户
*   选择一个密码：`devops`
*   确认你的密码：`devops`

按`Done`。

## 注意！

接一步非常重要。默认没有安装OpenSSH服务器，所以你必须选择该选项并安装OpenSSH服务器。你可以使用`Tab`键切换选项。否则，你将无法从远程连接访问你的服务器：

![](img/Figure-1.25.jpg)

**图 1.25**

现在你已经选择了正确的选项，按`Done`：

![](img/Figure-1.26.jpg)

**图 1.26**

现在，你需要为你的服务器选择一个安装`Template`（模板），例如Nextcloud服务器。或者，如果你打算运行Kubernetes，可以选择`microk8s`，但这不是我们想要的。所以，按`Tab`将选项更改为`Done`，然后按`Enter`：

![](img/Figure-1.27.jpg)

**图 1.27**

现在，你的安装已经开始。这可能需要一段时间时间，因为Ubuntu将下载更新和一些重要的软件包。你没有义务进行更新。但在我看来，对于学习Linux的人来说，拥有一个更新的系统是很重要的。只需等待安装完成，当Ubuntu询问你`Reboot`（重启）时，执行。重启后，你将看到以下屏幕：

![](img/Figure-1.28.jpg)

**图 1.28**

输入你在安装期间定义的凭据：

```
login: alisson
password: devops
```

现在你已经进入了Linux Shell。从现在开始，你将能够运行命令、安装软件包并对你的服务器做任何你想做的事。这个访问控制台正是你在数据中心内部时会进行的操作。将一个`KVM`（键盘视频显示器鼠标）连接到服务器并运行命令。我在做托管（Colocation）时做过很多次。这是一种业务模式，你可以购买自己的物理服务器并将其安装在别人的数据中心内部。因此，你将使用数据中心的基础，但服务器属于你。

除非你在数据中心内部工作，否则它并不常用用。如果你仍然登录在机器上，请运行以下命令：

```bash
ip a
```

上一个命令将显示你所有的网络接口及其IP地址，如下截图所示：

![](img/Figure-1.29.jpg)

**图 1.29**

我们只有2个IP地址和2个接口：

```
Interface: lo
IP Address: 127.0.0.1
```

这是本地IP地址。它用于在不离开机器的情况下建立TCP/IP连接：

```
Interface: enp0s3
IP Address: 10.0.2.15
```

这是一个NAT接口。我们需要这个接口只是为了建立连接。但我们无法使用此配置从外部访问机器。它仅用于安装目的。我们本可以在之前更改它。然而，我想向你展示如何更改该配置以及为什么我们需要这样做。

要更改此配置，回到VirtualBox的主界面。现在，点击虚拟机，然后点击`Settings`（设置）| `Network`（网络）。在这一部分`Attached`（连接），你会看到值Nat。将其更改为`Bridge Network`（桥接网络），并在`Name`（名称）选项中：选择你具有互联网访问的网络接口。在我的情况下，配置如下所示：

![](img/Figure-1.30.jpg)

**图 1.30**

保存配置后，回到你的虚拟机并再次运行以下命令：

```bash
ip a
```

你将看到一个新的IP地址。在我的情况下，绑定了`192.168.178.62`：

![](img/Figure-1.31.jpg)

**图 1.31**

## 通过SSH访问

我们现在有了从外部的连接。那么，我们如何使用SSH连接到那台机器呢？过去，使用Putty等工具从Windows机器SSH连接到服务器很常见，但在新版本的Windows中，我们有了PowerShell，它是默认安装的，我们可以用它来访问虚拟机。

如果你使用Windows，请打开PowerShell；如果是Linux/MacOS，打开Terminal，运行以下命令：

```bash
ssh alisson@192.168.178.62
```

命令遵循`USER@HOSTNAME`结构。如果你没有配置主机名，可以使用IP地址。之后按`Enter`。它将向你显示以下消息：

```
The authenticity of host '192.168.178.62 (192.168.178.62)' can't be established.
ECDSA key fingerprint is SHA256:GX474/IAL/VeIoiV/r6WoPZHRg3HfFTS3tfvigA9jKM.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.168.178.62' (ECDSA) to the list of known hosts.
```

发生这种情况是因为这是你第一次连接到该服务器。你只需输入`Yes`来确保你想要连接它，然后SSH将向你要密码：

```
alisson@192.168.178.62's password:
```

输入你在安装期间定义的密码。在我的情况下，它是DevOps，你将再次访问Linux Shell：

```
Welcome to Ubuntu 18.04.3 LTS (GNU/Linux 4.15.0-76-generic x86_64)
* Documentation:      https://help.ubuntu.com
* Management:         https://landscape.canonical.com
* Support:            https://ubuntu.com/advantage
System information as of Fri Jan 31 20:04:07 UTC 2020
System load:  0.0                             88
Usage of /:   39.0% of 9.78GB  Users logged in:  1
Memory usage: 15%                            IP address for enp0s3:  192.168.178.62
Swap usage:   0%
61 packages can be updated.
0 updates are security updates.
Last login: Fri Jan 31 19:41:36 2020
To run a command as administrator (user "root"), use `sudo <command>`.
See `man sudo_root` for details.
alisson@devops:~$
```

有很多关于加密SSH连接的理论和概念，我们还有`known_hosts`文件。如果你想成为Linux专家，这很重要，但对我们现在来说并不那么重要。



我们知道使用密码访问服务器并不是最佳实践，因为它们不够可靠且容易泄暴露。因此，我们可以创建一个密钥对来确保访问安全。你可以通过输入以下命令退出 shell：

```
alisson@devops:~$ logout
```

```
Connection to 192.168.178.62 closed.
```

或者按下 `Ctrl` + `D`。在你的 PowerShell 控制台中，输入以下命令：

```
ssh-keygen
```

并对所有选项直接按 `Enter` 键。此命令将为你生成两个文件：

* `id_rsa`：`id_rsa` 是你的私钥。它应该留在你的电脑上，并且只有你才能拥有这个文件。
* `id_rsa.pub`：`id_rsa.pub` 是公钥。你将把此文件复制到每一个你想无密码访问的 Linux 服务器上。

将你的公钥拷贝到我们的服务器，运行以下命令：

```bash
scp .\.ssh\id_rsa.pub alisson@192.168.178.62:/home/alisson/id_rsa.pub
```

```
alisson@192.168.178.62's password:
id_rsa.pub
100%   398   397.4KB/s   00:00
```

文件已拷贝，现在再次访问服务器：

```bash
ssh alisson@192.168.178.62
```

```
alisson@192.168.178.62's password:
```

创建 `.ssh` 目录并创建 `authorized_keys` 文件。该文件将存储所有使用 `alisson` 用户访问服务器的公钥：

```bash
mkdir .ssh
cat id_rsa.pub >> .ssh/authorized_keys
logout
```

现在，如果你尝试再次访问服务器，将不再询问密码，如下例所示：

```bash
ssh alisson@192.168.178.62
```

```
Welcome to Ubuntu 18.04.3 LTS (GNU/Linux 4.15.0-76-generic x86_64)
* Documentation:    https://help.ubuntu.com
* Management:      https://landscape.canonical.com
* Support:          https://ubuntu.com/advantage
System information as of Fri Jan 31 2024:51 UTC 2020
System load:   0.2             Processes:             88
Usage of /:    39.0% of 9.78GB   Users logged in:      1
Memory usage:  15%             IP address for enp0s3:  192.168.178.62
Swap usage:    0%
61 packages can be updated.
0 updates are security updates.
Last login: Fri Jan 31 20:20:28 2020 from 192.168.178.60
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.
alisson@devops:~$
```

任务完成！现在我们准备好学习更多 Bash、目录、文件以及更多内容了。

## 结论

这只是第一章，介绍了如何安装自己的 Linux 服务器以及在 VirtualBox 之上创建实验环境。我强烈建议你使用其他 Linux 发行版再次执行所有步骤，并发现你最喜欢哪一个。当我开始使用 Linux 时，我使用不同的发行版创建了自己的实验环境，包括 Slackware、Gentoo、BigLinux、Mandrake 和 Mandriva。所以，尽管选择你自己的。在我这些年工作的公司里，大多数使用 RedHat 或 CentOS，并且它们运行在本地基础设施上。但自从我开始接触云服务，情况发生了变化。如果你尝试在 Amazon 上创建 Ubuntu 服务器，你会发现它是最常用的发行版之一。

# 第 2 章：使用 Bash

本章将介绍在 Linux 系统内部导航的基础知识、主要目录、最常用的命令、重要文件、用户和组的管理，以及 Linux 权限系统的工作原理！

## 结构

在本章中我们将讨论以下主题：

* 什么是 Bash？
  * 简介
  * 基础命令
* 管理文件和目录
  * 目录结构
  * 重要文件
  * 自定义你的环境
* 管理用户和组
  * 创建和修改用户
  * 创建和修改组
* 权限操作
  * 修改读写权限
  * 修改文件所有者和执行脚本

## 目标

学习完本单元后，你将能够：

* 理解目录基础架构
* 使用重要文件自定义你的环境
* 管理用户和组
* 理解权限和执行脚本

## 什么是 Bash？

Bash 是 Bourne Again Shell 的缩写。它是我们在旧版 Linux/Unix 系统中看到的遗留 Shell 的改进版本。在这个版本中，我们拥有许多功能，如创建函数、控制前台和后台作业、创建别名、自定义你的环境、在终端中添加颜色、新的快捷键、自动补全以及我们将在本章看到的许多其他功能。为了让你有更多背景信息，Shell 是 Linux 上用于管理系统的接口。换句话说，它是我们运行所有命令的地方。

它也是一种编程语言。在 Linux 用户中，我们经常看到 Shell Scripting（Shell 脚本）这个术语。它什么意思？这意味着我们可以获取工作期间所有命令，将它们全部放在同一个文件中，赋予执行权限，并自动化你的日常工作。这就是一个 Shell 脚本。它基本上是 Linux 管理员的瑞士军刀。今天，它经常受到 Python 的挑战，因为 Python 是一种面向对象的语言，与 Shell 脚本相比，它拥有许多非常易用的功能。尽管如此，它将始终是所有 Linux 管理员自动化简单任务的首选工具，在本章结束时，我将教你如何使用之前学过的命令创建一个脚本。

## 简介

在上一章中，我们配置并安装了 Linux 系统，并能够使用 SSH 工具访问它。我们停止的地方如下：

```
ssh alisson@192.168.178.62
```

```
Welcome to Ubuntu 18.04.3 LTS (GNU/Linux 4.15.0-76-generic x86_64)
* Documentation:    https://help.ubuntu.com
* Management:      https://landscape.canonical.com
* Support:          https://ubuntu.com/advantage
System information disabled due to load higher than 1.0
* Multipass 1.0 is out! Get Ubuntu VMs on demand on your Linux, Windows or
Mac. Supports cloud-init for fast, local, cloud devops.
https://multipass.run/
60 packages can be updated.
6 updates are security updates.
Last login: Mon Feb 10 18:59:46 2020
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.
alisson@devops:~$
```

这意味着我们在 Linux Shell 中。现在我们将将其称为 Bash，因为它是命令行解释器。每个操作系统都有自己的命令行解释器，因为它是系统所需的。在旧版本的 Windows 中，我们有 MS-DOS。现在我们有 PowerShell。在旧版本的 Linux 中，我们有 Shell。现在有些用户正从 Bash 迁移到 Z shell。我将在接下来的页面介绍如何更改我们的 `CLI`。

在你的服务器中，最有用的命令叫做 `ls`：

```bash
alisson@devops:~$ ls
id_rsa.pub
```

此命令用于显示 Linux 的文件和目录。它可以配合不同的参数使用。例如，如果我想详细模式显示文件和目录，可以传递参数 `-l`：

```bash
alisson@devops:~$ ls -l
total 4
-rw-rw-r-- 1 alisson alisson 398 Jan 31 20:18 id_rsa.pub
alisson@devops:~$
```

最后的输出按顺序向我们展示更多信息：

`权限 – 硬链接数 – 用户 – 组 – 大小 – 最后修改日期 – 文件名`

这类信息被称为元数据（metadata）。但为什么叫这个名字呢？因为我们有一个文件包含了我们使用的数据，而这些数据是关于操作系统频繁使用的该文件的信息。例如，我们并不总是需要知道文件的大小，但操作系统总是需要这类信息，因为它需要计算磁盘上的可用和已用空间。

如果你想查看更多关于文件的元数据，可以使用以下命令 `stat`：

```
alisson@devops:~$ stat id_rsa.pub
```

`File: id_rsa.pub`

`Size: 398    Blocks: 8     IO Block: 4096    regular file`

`Device: 802h/2050d    Inode: 532800    Links: 1`

`Access: (0664/-rw-rw-r--) Uid: (1000/ alisson) Gid: (1000/ alisson)`

`Access: 2020-01-31 20:20:23.741638861 +0000`

`Modify: 2020-01-31 20:18:39.467733742 +0000`

`Change: 2020-01-31 20:18:39.467733742 +0000`

`Birth: -`

此命令将以详细的形式向你显示文件的所有元数据。

`ls` 有一个非常有趣的参数是 `-a`，它会显示所有文件，包括隐藏文件。在 Linux 中，所有隐藏文件都以 `.`（点）开头。例如：

```
alisson@devops:~$ ls -la
```

total 40

drwxr-xr-x 5 alisson alisson 4096 Jan 31 20:20 .

drwxr-xr-x 3 root root 4096 Jan 31 19:40 ..

-rw------- 1 alisson alisson 113 Jan 31 20:20 .bash_history

-rw-r--r-- 1 alisson alisson 220 Apr 4 2018 .bash_logout

-rw-r--r-- 1 alisson alisson 3771 Apr 4 2018 .bashrc

drwx------ 2 alisson alisson 4096 Jan 31 19:41 .cache

drwx------ 3 alisson alisson 4096 Jan 31 19:41 .gnupg

-rw-rw-r-- 1 alisson alisson 398 Jan 31 20:18 id_rsa.pub

-rw-r--r-- 1 alisson alisson 807 Apr 4 2018 .profile

drwxrwxr-x 2 alisson alisson 4096 Jan 31 20:20 .ssh

我们现在可以看到看到很多文件，比如 `.bashrc` 或 `.bash_history` 或者隐藏目录 `.ssh`，我们在第一章中曾使用它来保存公钥，以便无需密码即可访问服务器。

如果你想查看文件的内容，可以使用命令 `cat`：

```
alisson@devops:~$ cat .bash_logout
```

```# ~/. ~/.bash_logout: executed by bash(1) when login shell exits.
## when leaving the console clear the screen to increase privacy
if ["$SHLVL" = 1]; then
[-x /usr/bin/clear_console] && /usr/bin/clear_console -q
fi
```

通过命令 `cat`，我们看到了 `.bash_logout` 文件的内容。这个文件具有某些性，因为如果我们想在退出服务器之前执行某个命令，应该将它放在这个文件中。

要在屏幕上显示消息，使用命令 `echo`：

```
alisson@devops:~$ echo Message on Terminal
```

Message on Terminal

此命令通常也用于创建文件：

```
alisson@devops:~$ echo Creating a file > message.txt
alisson@devops:~$ ls
```

id_rsa.pub message.txt

```
alisson@devops:~$ cat message.txt
```

Creating a file

我们可以在 Shell 脚本中使用重定向符将命令输出写入文件。存在许多重定向符，但最常用的是 `>` 和 `>>`。

如果你在命令后使用 `>`，命令的标准输出将被重定向到你指定的文件。但如果你选择了一个已存在的文件，重定向符将覆盖它。

如果你在命令后使用 `>>`，命令的标准输出也将被重定向到你指定的指定。但如果你选择了一个已存在的文件，重定向符将追加内容而不是覆盖它。

为了管理文件，大多数命令都使用相同的语法。如果你想复制、移动或重命名文件，可以使用 `COMMAND <SOURCE FILE><DESTINATION FILE>`。

重命名文件：

```
alisson@devops:~$ mv message.txt file.txt
alisson@devops:~$ ls
```

file.txt id_rsa.pub

复制文件：

```
alisson@devops:~$ cp file.txt file2.txt
alisson@devops:~$ ls
```

file2.txt file.txt id_rsa.pub

在第一章中，我们编辑了一个名为 `authorized_keys` 的文件。如果我们想再次检查这个文件，可以使用 `cd` 命令访问目录：

```
alisson@devops:~$ cd .ssh/
alisson@devops:~/.ssh$ ls
```

authorized_keys

并且，我们可以再次检查文件内容：

```
alisson@devops:~/.ssh$ cat authorized_keys
```

这些是你在 Linux 系统中可以找到的最重要的目录，它们将成为你日常工作的一部分。

## 重要文件

既然你已经了解了这些重要目录，让我们进入内部看看对系统运行至关重要的文件。其中一个重要的文件是 `/etc/passwd`。该文件存储所有的 Linux 用户，我们可以使用 `cat` 命令查看其内容：

```bash
alisson@devops:~$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
```

这是前 5 行的示例。它的结构遵循以下序列：

`用户 – 密码 – 用户 ID – 组 ID – 注释 – 主目录 - shell`

数据通过冒号（`:`）分隔。需要注意的是，Linux shell 有许多非常有用的命令来处理这类文件。

例如，我们可以使用 `cut` 命令只查看我们感兴趣的信息：

```bash
alisson@devops:~$ cut -f 1,6,7 -d : /etc/passwd
root:/root:/bin/bash
daemon:/usr/sbin:/usr/sbin/nologin
bin:/bin:/usr/sbin/nologin
sys:/dev:/usr/sbin/nologin
```

因此，在示例中，我只打印了第 1、6、7 列，它们分别对应用户、主目录和 shell。

我没有发布命令的完整输出，是因为我想节省一些空间。但你可能会在自己的虚拟机上运行它。所以，如果你只想显示任何文件的前 3 行，可以使用 `head` 命令。默认情况下，该命令显示文件的前 10 行，但我们有 `-n` 参数，可以在其中定义我们想要看到的行数。

例如：

```bash
alisson@devops:~$ head -n 3 /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
```



在 Linux 上，还可以组合命令。如果你只想看前 3 行，并且像我们之前使用`cut`命令那样只看第 1、6、7 列，可以使用管道（`|`）。该语句的作用是获取上一个命令的输出并将其发送到流水线中的下一个命令。

示例：

```bash
alisson@devops:~$ head -n3 /etc/passwd | cut -f 1,6,7 -d :
root:/root:/bin/bash
daemon:/usr/sbin:/usr/sbin/nologin
bin:/bin:/usr/sbin/nologin
```

因此，每当你想要组合命令时，必须使用管道（`|`）。一个有趣点是`/etc/passwd`文件的第二列。我之前写过它是密码，但我们只能看到一个`x`，这个字符代表加密后的密码。哈希值可以在`/etc/shadow`文件找到：

```bash
alisson@devops:~$ sudo head -n3 /etc/shadow
[sudo] password for alisson:
root:*:18113:0:99999:7:::
daemon:*:18113:0:99999:7:::
bin:*:18113:0:99999:7:::
```

要查看此文件的内容，你需要在执行`head`命令之前运行`sudo`命令。`sudo`命令意味着以替代用户的身份执行操作。简单来说，我们正在以另一个用户的身份运行`head`命令。如果不指定用户，默认用户是 root。密码与我们在安装时设置的相同。如果你设置了和我一样的密码，那就是`devops`。

要查看你用户的密码，我们可以使用`grep`命令。该命令将找到符合我们搜索标准的行。

示例：

```bash
alisson@devops:~$ sudo grep alisson /etc/shadow
alisson:$6$aeR.OxEqoVMnyUuq$eYxtbG6V.156mtlsK9QBZcVOjQZBm7NlcKFn5x1y xF4mffuLYd6Wmz2R9V2iKZvuC7fgp96H7.jlQW/o7OenF/:18292:0:99999:7:::
```

现在你可以清楚地看到第二列中的密码哈希。当然，我们无法将其解密，但如果你想参加 Linux 认证，你需要记录这个文件及其结构。不过，我们也可以删除用户的密码。你只需要编辑此文件并删除哈希值即可。这样，用户就不会有密码，他可以在将来设置一个新密码。

关于用户，Linux 上还有一个文件用于管理用户组。该文件位于`/etc/group`：

```bash
alisson@devops:~$ head -n 3 /etc/group
root:x:0:
daemon:x:1:
bin:x:2:
```

该文件遵循以下序列：

`组名 | 密码 | 组 ID`

如所解释，我们可以使用`grep`来查找组。另一个重要文件是`/etc/fstab`，它用于挂载信息。

...

第二是`/etc/skel`，`adduser`命令会获取该用户`home`文件夹中存在的默认文件。我们可以通过以下命令查看它：

```bash
alisson@devops:~$ ls /etc/skel/ -la
```

```bash
total 20
drwxr-xr-x 2 root root 4096 Aug 5 2019 .
drwxr-xr-x 91 root root 4096 Feb 18 19:25 ..
-rw-r--r-- 1 root root 220 Apr 4 2018 .bash_logout
-rw-r--r-- 1 root root 3771 Apr 4 2018 .bashrc
-rw-r--r-- 1 root root 807 Apr 4 2018 .profile
```

这些文件负责自定义用户的环境。我们将在本章的最后部分编辑它们。但是，如果你想在`home`文件夹中放入更多项目，只需要将它们添加到`/etc/skel`中，它们在下次创建用户时就会包含进去。让我们测试一下。

让我们为托管服务器创建一个骨架。Web 服务器是如何工作的？通常，我们有用户，并且每个用户的`home`文件夹中，你有一些名为`public_html`、`mail`、`conf`、`logs`的文件夹。所有这些文件夹必须在创建用户的同时创建。因此，运行以下命令：

```bash
alisson@devops:~$ sudo mkdir /etc/skel/{public_html, logs, mail, conf}
```

```bash
[sudo] password for alisson:
alisson@devops:~$ ls /etc/skel/
conf logs mail public_html
alisson@devops:~$
```

所以，如你所见，现在`/etc/skel`内部创建了这四个文件夹。现在，让我们创建另一个用户看看效果：

```bash
alisson@devops:~$ sudo adduser customer01
```

```bash
Adding user 'customer01' …
Adding new group 'customer01' (1002) …
Adding new user 'customer01' (1002) with group 'customer01' …
Creating home directory '/home/customer01' …
Copying files from '/etc/skel' …
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
Changing the user information for customer01
Enter the new value, or press ENTER for the default
Full Name []:
Room Number []:
Work Phone []:
Home Phone []:
Other []:
Is the information correct? [Y/n]
```

```bash
alisson@devops:~$ ls /home/customer01/
```

```bash
conf logs mail public_html
```

现在你现在所见，我们在用户的`home`文件夹中创建了这些文件夹。我正为所有用户设置相同的密码。但是，如果你忘记了密码并想更改它，相应的命令如下：

```bash
alisson@devops:~$ sudo passwd elvis
```

```bash
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

现在，输入新密码，密码就更改了。

我们现在讨论的是托管服务器。所以，让我们来看另一个例子。假设你的客户没有给你付钱。因此你需要锁定这个用户。要执行此任务，你可以运行以下命令：

```bash
alisson@devops:~$ sudo passwd -l customer01
```

```bash
passwd: password expiry information changed.
```

Linux 的一个有趣之处是，如果你想知道它是如何锁定用户的，可以查看`/etc/shadow`：

```bash
alisson@devops:~$ sudo getent shadow customer01
```

```bash
customer01:!$6$PExBAe3N$6AxVOOJLi/A5ddWOp2I/ZhvB00mpVwq4KQ78/4.QNNcrz2tsGGFu8XXr/TU7NFA/Hg3T2X9.R5v6cCuzbYF8j.:18310:0:99999:7:::
```

观察输出很容易。为了注意一个区别，让我们与未被锁定的用户进行对比：

```bash
alisson@devops:~$ sudo getent shadow alisson
```

```bash
alisson:$6$aeR.OxEqoVMnyUuq$eYxtbG6V.156mtlsK9QBZcVOjQZBm7NlcKFn5x1 yxF4mffuLYd6Wmz2R9V2iKZvuC7fgp96H7.jlQW/o7OenF/:18292:0:99999:7:::
```

在第二列（存储密码的地方），对于被锁定的用户，你可以看到系统将感叹号（`!`）作为第一个字符。这样，用户输入他的密码，也永远不会与哈值匹配，因为开头有一个感叹号。

要解锁用户，输入以下命令：

```bash
alisson@devops:~$ sudo passwd -u customer01
```

```bash
passwd: password expiry information changed.
alisson@devops:~$ sudo getent shadow customer01
```

```bash
customer01:$6$PExBAe3N$6AxVOOJLi/A5ddWOp2I/ZhvB00mpVwq4KQ78/4.QNNcrz2tsGGFu8XXr/TU7NFA/Hg3T2X9.R5v6cCuzbYF8j.:18310:0:99999:7:::
```

现在，Linux 删除了哈值开头的`!`，用户可以再次访问 shell 了。如果客户取消了与你的服务，可以删除他的用户。要执行此任务，你需要运行以下命令：

```bash
alisson@devops:~$ sudo userdel elvis
alisson@devops:~$ sudo getent passwd elvis
```

需要记住这一点是，删除用户并不意味着`home`目录被删除。如果你也想删除它，可以使用：

```bash
alisson@devops:~$ sudo userdel -r elvis
```

所以，如果你检查输出，可以清楚地看到用户没有 shell 并且被阻止登录。如果我当时执行了`useradd`，情况会简单得多。但当你陷入一个恶性循环时，它是很难避免的。

现在，让我们回到`sudo`组中的用户。删除该用户：

```bash
alisson@devops:~$ sudo userdel -r gabriela
```

```bash
userdel: gabriela mail spool (/var/mail/gabriela) not found
userdel: gabriela home directory (/home/gabriela) not found
```

再次创建用户：

```bash
alisson@devops:~$ sudo adduser gabriela
```

```bash
Adding user 'gabriela' …
Adding new group 'gabriela' (1001) …
Adding new user 'gabriela' (1001) with group 'gabriela' …
Creating home directory '/home/gabriela' …
Copying files from '/etc/skel' …
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
Changing the user information for gabriela
Enter the new value, or press ENTER for the default
Full Name []:
Room Number []:
Work Phone []:
Home Phone []:
Other []:
Is the information correct? [Y/n]
```

将用户添加到组组：

```bash
alisson@devops:~$ sudo gpasswd -a gabriela sudo
```

```bash
Adding user gabriela to group sudo
alisson@devops:~$
```

切换用户：

```bash
alisson@devops:~$ sudo su - gabriela
```

```bash
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.
gabriela@devops:~$
```

现在，你可以看到我的 shell 已经改变了。现在，我是用户`gabriela`。要创建用户或组，我们需要`sudo`权限。让我们尝试创建一个名为`applications`的新组：

```bash
gabriela@devops:~$ sudo addgroup applications
```

```bash
[sudo] password for gabriela:
Adding group 'applications' (GID 1003) …
Done.
```

检查该组是否已创建：

```bash
gabriela@devops:~$ sudo getent group applications
```

```bash
applications:x:1003:
```

将一个新用户添加到此组：

```bash
gabriela@devops:~$ sudo useradd juergen
gabriela@devops:~$ sudo gpasswd -a juergen applications
```

```bash
#Adding user juergen to group applications:
gabriela@devops:~$ getent group applications
```

```bash
applications:x:1003:juergen
```

如果你想删除该组：

```bash
gabriela@devops:~$ sudo delgroup applications
```

```bash
Removing group 'applications' …
Done.
```

切换回我的用户：

```bash
gabriela@devops:~$ exit
```

```bash
logout
alisson@devops:~$
```

就是这样。这就是你管理用户和组的`QuickStart`（快速上手）。当然，我们可以在这些主题上深入得更深，但我还需要解释如何自定义你的环境。

## 权限操作

Linux 权限系统的工作方式与 Windows 不同。我们有一些与权限相关的数字。例如：

- 1 – 执行（Execution）

- 2 - 写入（Writing）

- 4 – 读取（Reading）

所以你总是必须进行一些数学计算来应用权限。如果你想分配执行权限，可以将其设置为`1`，写入权限设置为`2`，读取权限设置为`4`。`写入 + 读取`等于`6`，因此权限是`6`。如果你想要`读取 + 写入 + 执行`则等于`7`。让我们创建一个文件并检查它的权限：

```bash
alisson@devops:~$ touch new_file
alisson@devops:~$ ls -la new_file
```

```bash
-rw-rw-r-- 1 alisson alisson 0 Feb 20 19:21 new_file
```

`touch`命令负责更改任何文件的访问时间。如果文件不存在，它会创建一个。检查输出，你可以看到我们拥有权限：`read+write`、`read+write`、read，但这个序列意味着什么：

`user – group – other`

在同一行中，我们可以看到`alisson alisson`，第一个是该文件的用户所有者，第二个是组。默认情况下，Linux 上创建的所有用户都带有一个与用户名同名的组。

如果你记得代表权限的数字，我们可以进行一个计算，`read+write = 4 + 2 = 6`。然后我们拥有以下权限：

```
664
```

因此，用户可以读取和写入。同一组的用户也可以读取和写入，不属于该组的用户只能读取。现在，我们可以创建一个目录并像刚才那样分析权限：

```bash
alisson@devops:~$ mkdir new_folder
alisson@devops:~$ ls -la | grep new_folder
```

```bash
drwxrwxr-x 2 alisson alisson 4096 Feb 20 19:29 new_folder
```

分析权限，我们可以看到用户和组具有`read + write + execution`权限，而其他人具有`read + execution`权限。如果我们建立如下关联：

```
read + write + execution = 4 + 2 + 1 = 7
read + execution = 4 + 1 = 5
```

我们就得到了`775`。那么我们可以得出什么结论？文件的默认权限是`644`，目录的权限是`775`。

**为什么目录和文件的权限不同？如果我们留意，唯一的区别是执行权限。文件创建时没有这个权限，仅仅是为了安全。所以，我们可以执行错误的文件，而文件夹创建时带有执行权限，因为有了这个权限，我们可以打开文件夹。**

很好，但我们如何更改文件权限呢？

### 修改读取写权限

用于更改这些权限的命令是`chmod`。我将向你展示如何使用数字和字母来更改。丰富的 Linux 用户通常使用数字，但使用数字还是字母并没有区别。让我们以`new_file`为例：

```bash
alisson@devops:~$ ls -la new_file
```

```bash
-rw-rw-r-- 1 alisson alisson 0 Feb 20 19:21 new_file
```

所以权限是`664`，这意味着任何不是我的用户都可以读取文件内容，而我不允许这样做。因此，我将其他用户的权限更改为`0`：

```bash
alisson@devops:~$ chmod 660 new_file
alisson@devops:~$ ls -la new_file
```



```
-rw-rw---- 1 alisson alisson 0 Feb 20 19:21 new_file
```

我刚刚将权限更改为`660`。现在，让我们在这个文件内部创建内容。更改用户并看看它是如何工作的：

```
alisson@devops:~$ echo content not allowed to other > new_file
alisson@devops:~$ cat new_file
```

```
content not allowed to other
```

让我们用户切换为`gabriela`：

```
alisson@devops:~$ sudo su - gabriela
```

```
[sudo] password for alisson:
gabriela@devops:~$ pwd
```

```
/home/gabriela
gabriela@devops:~$ ls -la /home
```

```
total 20
drwxr-xr-x  5  root      root      4096 Feb 20 19:05 .
drwxr-xr-x 24  root      root      4096 Feb 20 19:05 ..
``` （等待，原文的输出行中有拼写错误，我将保留其内容）

```
gabriela@devops:~$ ls -la /home
```

实际上，让我们根据提供的源文本重新对齐：

```
/home/gabriela
gabriela@devops:~$ ls -la /home
total 20
drwxr-xr-x  5  root      root      4096 Feb 20 19:05 .
drwxr-xr-x 24  root      root      4096 Feb 20 19:05 ..
```

并且可以看到文件内容。这就是权限的工作原理。我将展示我们如何使用数字来更改权限。如果你想使用字母来更改，基本上也是那样的。让我们尝试：

```
gabriela@devops:/home/alisson$ cd
gabriela@devops:~$ touch letters_file
gabriela@devops:~$ ls -la letters_file
-rw-rw-r-- 1 gabriela gabriela 0 Feb 20 19:47 letters_file
```

移除其他用户的所有权限：

```bash
gabriela@devops:~$ chmod o= letters_file
gabriela@devops:~$ ls -la letters_file
-rw-rw---- 1 gabriela gabriela 0 Feb 20 19:47 letters_file
```

然后，我们可以看到我只需要输入`o=`，这意味着`other = 无权限`，权限就设置了。我只需要添加执行权限：

```bash
gabriela@devops:~$ chmod o+x letters_file
gabriela@devops:~$ ls -la letters_file
-rw-rw---x 1 gabriela gabriela 0 Feb 20 19:47 letters_file
```

或者，我可以为所有人设置读取权限，仅为所有者设置写入权限：

```bash
gabriela@devops:~$ chmod g=rx,o=rx letters_file
gabriela@devops:~$ ls -la letters_file
-rw-r-xr-x 1 gabriela gabriela 0 Feb 20 19:47 letters_file
```

如果我想给所有人写入权限，我将执行以下操作：

```bash
gabriela@devops:~$ chmod +w letters_file
gabriela@devops:~$ ls -la letters_file
-rw-rwxr-x 1 gabriela gabriela 0 Feb 20 19:47 letters_file
```

相同的命令也适用于目录。

## 修改文件所有者和执行脚本所有者

与`chmod`用于权限一样，`chown`用于所有权。让我使用我们已有的文件：

```bash
gabriela@devops:~$ ls -la letters_file
-rw-rwxr-x 1 gabriela gabriela 0 Feb 20 19:47 letters_file
```

所有者是`gabriela`，组也是`gabriela`。在在上一个示例中，我将用户`gabriela`添加到了组`alisson`中，然后用户就能访问该文件。但这次，我将采取不同的方法：

```bash
gabriela@devops:~$ chown gabriela:alisson letters_file
gabriela@devops:~$ ls -la letters_file
-rw-rwxr-x 1 gabriela alisson 0 Feb 20 19:47 letters_file
```

现在，该文件的组所有是`alisson`。如果我想更改用户，可以运行如下命令：

```bash
gabriela@devops:~$ sudo chown juergen letters_file
[sudo] password for gabriela:
gabriela@devops:~$ ls -la letters_file
-rw-rwxr-x 1 juergen alisson 0 Feb 20 19:47 letters_file
```

`Jurgen`是该文件的所有者。我们可以使用`chown`命令来更改文件或目录的用户和组。但我们也有一个命令可以更改组：

```bash
gabriela@devops:~$ sudo chgrp gabriela letters_file
gabriela@devops:~$ ls -la letters_file
-rw-rwxr-x 1 juergen gabriela 0 Feb 20 19:47 letters_file
```

组现在已经更改。因此，`chgrp`命令仅更改组，而`chown`命令更改所有者，或者所有者和组。因此，为了完成这一章，我们只需要查看如何执行脚本。让我们创建一个简单的脚本：

```bash
gabriela@devops:~$ echo "echo this is a simple script"> simple_script.sh
gabriela@devops:~$ ls -la simple_script.sh
-rw-rw-r-- 1 gabriela gabriela 29 Feb 20 20:05 simple_script.sh
```

在这里，我们创建了脚本。要执行它，请如下运行：

```bash
gabriela@devops:~$ ./simple_script.sh
-su: ./simple_script.sh: Permission denied
```

拒绝拒绝！发生这种情况是因为，如果我们分析之前运行的命令并检查权限，发现没有代表执行权限的`x`。然后，设置以下权限：

```bash
gabriela@devops:~$ chmod +x simple_script.sh
```

再次运行脚本：

```bash
gabriela@devops:~$ ./simple_script.sh
this is a simple script
```

再次检查一次权限：

```bash
gabriela@devops:~$ ls -la simple_script.sh
-rwxrwxr-x 1 gabriela gabriela 29 Feb 20 20:05 simple_script.sh
```

用户、组和其他人的所有权限组中都有`x`。因此，每个人都可以执行它。如果你只想给文件所有者或组提供执行权限，可以使用`chmod`来实现，并使用相同的`math`方法来设置权限。

# 第 3 章

# 设置服务

本章将解释 Linux 软件包系统的工作原理、如何安装软件包、安装服务、配置它，以及在你的第一个 LAMP (Linux Apache MySQL PHP) 服务器上运行你的第一个应用程序。

## 结构

在本章中，我们将讨论以下主题：

*   学习如何安装软件包

    *   APT

*   安装 Apache

    *   配置你的服务

    *   创建虚拟主机 (VHost)

*   安装 MySQL

    *   配置服务

    *   创建数据库和表

*   部署你的应用程序

    *   安装 PHP

    *   部署 WordPress

## 目标

在学习此单元后，你应该能够：

*   理解 Linux 软件包系统

*   使用 APT 安装软件包

*   设置 Web 服务器

*   设置数据库服务器

*   部署应用程序

## 学习如何安装软件包

大多数 Linux 发行版默认都带有一个包管理器。它可以是 YUM、APT、Zypper、pacman、slackapt 等。每个工具都有有其特殊之处，但它们都是为了同一个目的设计的：通过分布在世界各地的中心化仓库安装本质上是 Linux 程序的软件包。

在第一章中，我简要解释了 Linux 发行版以及一些区别。其中一些区别体现在包管理系统中。现在，我将给出两个最著名的包管理器的示例。

基于 Debian 的发行版（如 Ubuntu）拥有`APT`（高级软件包工具）。它连接到这样的中心仓库，例如：`http://de.archive.ubuntu.com/ubuntu`。这仅仅是一个 Apache Web 服务器，其中存储了我们可以选择并安装的多个软件包。

基于 RedHat 的发行版（如 CentOS）拥有`YUM`（黄色狗更新管理器），它很快将由`DNF`（Dandified Yum）取代，这是 YUM 的新替代品。它也使用中心仓库，如`https://dl.fedoraproject.org/pub/epel/7/x86_64/`，并且存储了多个软件包。

现在，让我们关注作为我们目标的 Debian，因为我们正在使用 Ubuntu。

## APT

如果你不带任何参数运行`apt`命令，你将看到以下输出：

```
alisson@devops:~$ apt
apt 1.6.11 (amd64)

Usage: apt [options] command

apt 是命令行包管理器，提供了用于搜索和管理软件包以及查询软件包信息的命令。
它提供了与专门的 APT 工具（如 apt-get 和 apt-cache）相同的功能，但默认启用了更适合交互式使用的选项。

最常用的命令：
list - 根据包名列出软件包
search - 在包描述中搜索
show - 显示包详情
install - 安装软件包
remove - 软件包
autoremove - 自动删除未使用的软件包
update - 更新可用软件包列表
upgrade - 通过安装/升级软件包来升级系统
full-upgrade - 通过删除/安装/升级软件包来升级系统
edit-sources - 编辑源信息文件

访问 apt(8) 获取更多有关可用命令的信息。

配置选项和语法在 apt.conf(5) 中详细介绍。
关于如何配置源的信息可以在 sources.list(5) 中找到。软件包和版本选择可以通过 apt_preferences(5) 表达。
安全详情请参阅 apt-secure(8)。

此 APT 拥有超级牛能力。
```

因此，这些选项是言而自明的。让我们在实践中使用它们吧。一个有趣的命令是`top`：

```text
top - 18:19:11 up 2 days, 2:34, 1 user, load average: 0.04, 0.03, 0.00
Tasks: 92 total, 1 running, 50 sleeping, 0 stopped, 0 zombie
%Cpu(s): 0.0 us, 0.0 sy, 0.0 ni,100.0 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st
KiB Mem : 1008816 total, 133020 free, 126512 used, 749284 buff/cache
KiB Swap: 2017276 total, 2016752 free, 524 used. 716548 avail Mem
PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
28427 alisson 20 0 107988 3460 2448 S 0.3 0.3 0:00.14 sshd
28462 alisson 20 0 42788 3940 3344 R 0.3 0.4 0:00.25 top
1 root   20  0   77992  9104  6680 S 0.0 0.9  0:02.58 systemd
2 root   20  0      0     0     0 S 0.0 0.0  0:00.00 kthreadd
4 root    0 -20     0     0     0 I 0.0 0.0  0:00.00 kworker/0:0H
6 root    0 -20     0     0     0 I 0.0 0.0  0:00.00 mm_percpu_wq
7 root   20  0     0     0     0 S 0.0 0.0  0:00.55 ksoftirqd/0
8 root   20  0     0     0     0 I  0.0  0.0  0:19.94 rcu_sched
```

要退出`top`，按`q`。这个命令基本上显示了你机器当前的状态、内存状态、CPU、运行中的进程等。`top`有另一个版本叫做`htop`。它执行完全相同的操作。不过，它有一个更好的界面，因此，在我们安装该版本之前，运行以下命令：

```bash
alisson@devops:~$ sudo su -
[sudo] password for alisson:
root@devops:~#
```

之前的命令将你的当前用户切换为`root`用户。到目前为止，我们在每个需要更多权限的命令之前都在运行`sudo`。现在，我们不需要每次在命令前输入`sudo`了，因为我们已经是这台服务器的管理员了。或者，你可以说我们`root`用户。

有时，当我们基于镜像创建一个服务器时，`APT`的本地缓存可能是完全过时的。因此，我们需要清理它并使用以下命令进行更新：

```bash
root@devops:~# apt clean
root@devops:~# apt update
Hit:1 http://de.archive.ubuntu.com/ubuntu bionic InRelease
Hit:2 http://de.archive.ubuntu.com/ubuntu bionic-updates InRelease
Hit:3 http://de.archive.ubuntu.com/ubuntu bionic-backports InRelease
Hit:4 http://de.archive.ubuntu.com/ubuntu bionic-security InRelease
Reading package lists… Done
Building dependency tree
Reading state information… Done
65 packages can be upgraded. Run 'apt list --upgradable' to see them.
root@devops:~#
```

现在，你已经更新了本地缓存。我们可以尝试寻找`htop`并查看它是否可以安装：

```bash
root@devops:~# apt search htop
Sorting… Done
Full Text Search… Done
aha/bionic 0.4.10.6-4 amd64
ANSI color to HTML converter
htop/bionic,now 2.1.0-3 amd64 [installed,automatic] interactive viewer
libauthen-oath-perl/bionic 2.0.1-1 all module for Time Passwords
ftools/bionic 3+dfsg1 amd64 search and profiles
```

分析之前的输出，我们可以说`htop`是可用的。因此，要安装该包，我们使用以下命令：

```bash
root@devops:~# apt install htop -y
Reading package lists… Done
Building dependency tree
Reading state information… Done
htop is already the newest version (2.1.0-3).
htop set to manually installed.
0 upgraded, 0 newly installed, 0 to remove and 65 not upgraded.
root@devops:~#
```



以下是排版后的内容：

`CPU[0.0%] Tasks: 29, 28 running`
`Mem[||||||||||||||||||||||||||||||||||||||||128M/985M] Load average: 0.07 0.02 0.00`
`Swap[524K/1.9G] Uptime: 2 days, 02:45:09`
`PID USER PRI NI VIRT RES S CPU% MEM% TIME+ COMMAND`
`28771 root 20 0 32468 4868 3764 R 0.0 0.5 0:00.02 htop`
`1 root   20 0 77992 9104 6680 S 0.0 0.9  0:02.58 /sbin/init maybe-ubiquity`
`394 root 19 -1 100M 17652 16796 S 0.0 1.7 0:00.36 /lib/systemd/systemd-journald`
`420 root 20 0 103M 1852 1664 S 0.0 0.2 0:00.00 /sbin/lvmetad -f`
`421 root 20 0 45836 4476 2888 S 0.0 0.4 0:00.87 /lib/systemd/systemd-udevd`
`496 systemd-t 20 0 138M 3256 2744 S 0.0 0.3 0:00.00 /lib/systemd/systemd-timescd`
`491 systemd-t 20 0 138M 3256 2744 S 0.0 0.3 0:00.20 /lib/systemd/systemd-timescd`
`672 systemd-n 20 0 80048 5076 4484 S 0.0 0.5 0:00.19 /lib/systemd/systemd-networkd`
`696 systemd-r 20 0 70636 4916 4356 S 0.0 0.5 0:00.19 /lib/systemd/systemd-resolved`

在这个简单的输出中，我们能够看到一些改进。例如，我们现在有一个进度条来指示服务器上使用的内存量。它是分析服务器当前状态的好工具，但在生产系统中并不经常使用，因为它比传统的 `top` 消耗了更多的内存。因此，让我们使用以下命令删除此包：

```bash
root@devops:~# apt remove htop
Reading package lists… Done
Building dependency tree
Reading state information… Done
The following packages will be REMOVED:
htop ubuntu-server
0 upgraded, 0 newly installed, 2 to remove and 64 not upgraded.
After this operation, 269 kB disk space will be freed.
Do you want to continue? [Y/n] y
(Reading database … 102467 files and directories currently installed.)
Removing ubuntu-server (1.417.3) …
Removing htop (2.1.0-3) …
Processing triggers for mime-support (3.60ubuntu1) …
Processing triggers for man-db (2.8.3-2) …
```

这些都是你在 Linux 上安装软件包时可能会用到的命令。除了命令，我们还有一些重要的文件，用于安装官方发行版中可能没有的包。

第一个重要文件是`/etc/apt/sources.list`：

```bash
root@devops:~# cat /etc/apt/sources.list

# See http://help.ubuntu.com/community/UpgradeNotes for how to upgrade to
# newer versions of the distribution.

deb http://de.archive.ubuntu.com/ubuntu bionic main restricted
deb http://de.archive.ubuntu.com/ubuntu bionic-updates main
```

上述是`/etc/apt/sources.list`中的示例。这些行代表软件包所在的远程仓库。如果你想添加一个新的仓库，只需要在文件的末尾添加相应的行，例如：

```text
deb http://ppa.launchpad.net/canonical-kernel-team/unstable/ubuntu bionic main
```

`PPA`（**个人包存档**）。这些是不包含在发行版中的但你可以在其中找到需要的仓库。

另一个重要的目录是`/var/cache/apt/`。在开始时我解释过`APT`将缓存存储在系统内部，如果它太旧了，我们需要清理并更新它。此文件夹还会下载系统中安装的软件包，例如：

```bash
root@devops:~# apt install htop --download-only
Reading package lists… Done
Building dependency tree
Reading state information… Done
The following NEW packages will be installed:
htop
0 upgraded, 1 newly installed, 0 to remove and 64 not upgraded.
Need to get 80.0 kB of archives.
After this operation, 221 kB of additional disk space will be used.
Get:1 http://de.archive.ubuntu.com/ubuntu bionic/main amd64 htop amd64 2.1.0-3 [80.0 kB]
Fetched 80.0 kB in 0s (451 kB/s)
Download complete and in download only mode
```

这些都是你在 Linux 上日常工作中安装软件包时可能会用到的命令。

我们安装了一个基础软件包来学习`APT`是如何工作的。现在，让我们安装一个真实的软件包。Apache Web 服务器是目前世界上最广泛使用的 Web 服务器。你可以使用它将其部署为负载均衡器、静态文件缓存、另一个 Web 服务器的代理，以及取决于你用法的许多其他选项。要安装 Apache，请使用以下命令：

```bash
root@devops:~# apt install apache2 -y
```

`Reading package lists… Done`
`Building dependency tree`
`Reading state information… Done`

将安装以下额外的软件包：

`apache2-bin apache2-data apache2-utils libapr1 libaprutil1 libaprutil1-dbd-sqlite3 libaprutil1-ldap liblua5.2-0 ssl-cert`

如果安装顺利，你可以使用以下命令验证 Apache 是否已安装并运行：

```bash
root@devops:~# service apache2 status
```

`apache2.service - The Apache HTTP Server`
`Loaded: loaded (/lib/systemd/system/apache2.service; disabled; vendor preset: enabled)`
`Drop-In: /lib/systemd/system/apache2.service.d`
`└─apache2-systemd.conf`
`Active: active (running) since Mon 2020-07-06 12:56:38 UTC; 11s ago`
`Process: 22810 ExecStart=/usr/sbin/apachectl start (code=exited, status=0/SUCCESS)`

注意显示`Active`(running)的部分，你也可以使用命令`ss -ntpl`：

```bash
root@devops:~# ss -ntpl
```

![](img/p79.jpg)

我们可以看到 Apache 运行在端口`80`上，`PID 22848`。`PID`意味着进程标识。现在服务器已经启动运行。让我们通过浏览器检查一下：

`http://192.168.178.62/`

![](img/Figure-3.1.jpg)

**图 3.1**

这是服务器在 Ubuntu 上运行时时的 Apache 默认页面。通常，此页面会根据你的操作系统而不同。

现在，你可以说你已经设置了一个 Web 服务器。然而，我们知道网站不仅仅是使用 HTML 制作的。有大量的后端处理。通常是`PHP`。当然，你可以使用可用的几十种编程语言之一来开发你的网站。但我仍然非常确定`PHP`是大多数网站常用的语言。

## 安装 PHP

在这一部分中，让我们安装`PHP`并创建一个简单的页面来检查它是否已安装，以及可以使用它的哪些模块：

```bash
root@devops:~# apt install php -y
```

使用`APT`安装非常简单。当我们安装`PHP`和`Apache`时，会一起安装许多 Apache 模块。你可以运行以下命令来检查它们：

```bash
root@devops:~# a2enmod
```

`Your choices are: access_compat actions alias allowmethods asis auth_basic auth_digest auth_form authn_anon authn_core authn_dbd authn_dbm authn_file authn_socache authnz_fcgi authnz_ldap authz_core authz_dbd authz_dbm authz_groupfile authz_host authz_owner authz_user autoindex buffer cache cache_disk cache_socache cern_meta cgi cgid charset_lite data dav dav_fs dav_lock dbd deflate dialup dir dump_io echo env expires ext_filter file_cache filter headers heartbeat heartmonitor http2 ident imagemap include info lbmethod_bybusyness lbmethod_byrequests lbmethod_bytraffic lbmethod_heartbeat ldap log_debug log_forensic lua macro mime mime_magic mpm_event mpm_prefork mpm_worker negotiation php7.2 proxy proxy_ajp proxy_balancer proxy_connect proxy_express proxy_fcgi proxy_fdpass proxy_ftp proxy_hcheck proxy_html proxy_http proxy_http2 proxy_scgi proxy_wstunnel ratelimit reflector remoteip reqtimeout request rewrite sed session session_cookie session_crypto session_dbd setenvif slotmem_plain slotmem_shm socache_dbm socache_memcache socache_shmcb speling ssl status substitute suexec unique_id userdir usertrack vhost_alias xml2enc`

`Which module(s) do you want to enable (wildcards ok)?`

有很多选项，但我们寻找的是`php7.2`：

```bash
root@devops:~# a2enmod php7.2
```

`Considering dependency mpm_prefork for php7.2:`
`Considering conflict mpm_event for mpm_prefork:`
`Considering conflict mpm_worker for mpm_prefork:`
`Module mpm_prefork already enabled`
`Considering conflict php5 for php7.2:`
`Module php7.2 already enabled`

命令`a2enmod`启用了`php7.2`模块，该模块负责集成`Apache`和`PHP`。当我们通过浏览器访问`PHP`页面时，`Apache`将调用该模块，由它调用`PHP`解释器并运行代码。让我们创建一个简单的页面作为示例：

```bash
root@devops:~# vim /var/www/html/info.php
```

```php
<?php
phpinfo();
?>
```

这段代码是你可以在`PHP`上运行的最简单的代码，用于检查一切是否运行正常。当你通过浏览器调用该页面时，你将看到以下内容：

![](img/Figure-3.2.jpg)

**图 3.2**

现在你可以通过浏览器看到你`PHP`安装中安装的所有内容，并确保`PHP`正在运行。当我们在 Web 服务器中运行完整应用程序时，`PHP`和`Apache`就足够发布信息并使其随处可访问了。

然而，完整的系统会存储和管理数据，为了做到这一点，我们需要一个**数据库管理系统**，它可以有很多种。数据库系统和编程语言一样多，并且分为不同的类别：`SQL`、`NoSQL`、`Key Values`等。

运行在 Web 服务器上最流行的`DBMS`是`MySQL/MariaDB`。所以，让我们安装并测试它。

## 安装 MariaDB

运行在 Web 服务器上最流行的`DBMS`是`MySQL/MariaDB`。所以，让我们安装并测试：

```bash
root@devops:~# apt install mariadb-server mariadb-client -y
```

安装后，运行以下命令：

```bash
root@devops:~# mysql
```

`Welcome to the MariaDB monitor. Version 10.3.44-MariaDB on Ubuntu (10.04)`
`Copyright (c) 2000-2018 MariaDB Contributors`
`MariaDB is a fork of MySQL licensed under the GPL General Public License.`
`MariaDB is a compatible drop-in replacement for MySQL.`
`MariaDB is developed by the MariaDB Foundation.`
`MariaDB documentation available at https://wiki.mariadb.org`
`Type "help" for help information.`

`MariaDB [(none)]>`

在过去，我们通常使用`MySQL`。但在 Oracle 购买它之后，创建了一个名为`MariaDB`的分支，并变得越来越受欢迎。它的 API 完全兼容`MySQL`服务器。要创建一个数据库，你需要运行以下命令：

```sql
MariaDB [(none)]> create database chapter03;
```

`Query OK, 1 row affected (0.00 sec)`

`MariaDB [(none)]> use chapter03;`

`Database changed`

你可以看到我们创建了一个名为`chapter03`的数据库，但没有任何表：

```sql
MariaDB [(none)]> show tables;
```

`Empty set (0.00 sec)`

我们可以通过运行以下命令来创建一个表：

```sql
MariaDB [(none)]> create table users(id integer primary key auto_increment, name varchar(50));
```

`Query OK, 0 rows affected (1.77 sec)`

我们刚刚创建了一个包含 2 列的表，一个称为`ID`，将存储数字，另一个称为`name`，将接收字符串。要检查表结构，使用以下命令：

![](img/p83.jpg)

我刚刚输入了 4 个不同的用户`alisson`、`gabriela`、`juergen`和`leonardo`来演示如何查看存储在表中的数据：

```sql
MariaDB [(none)]> select * from users;
```



`+----+----------+`
`| id | name |`
`+----+----------+`
`| 1 | alisson |`
`| 2 | gabriela |`
`| 3 | juergen |`
`| 4 | leonardo |`
`+----+----------+`
`4 rows in set (0.00 sec)`

注意数字是由数据库自动增加的。这在使用自增列时是正常的。我们这样做只是为了确保数据库服务器正在运行。现在，我们有了一个完整的配置，我们称之为 **LAMP**（**Linux Apache MariaDB PHP**），并且准备好部署一个真实的应用程序。

为了实现，我们将使用 WordPress 并看看它是如何工作的。按下 *Ctrl* + *D* 退出 MariaDB 控制台。

## 安装 WordPress

第一个任务是从官方网站下载 WordPress：

```bash
root@devops:~# wget https://wordpress.org/latest.tar.gz
```

```
--2020-07-06 13:51:03-- https://wordpress.org/latest.tar.gz
Resolving wordpress.org (wordpress.org)… 198.143.164.252
Connecting to wordpress.org (wordpress.org)|198.143.164.252|:443… connected.
HTTP request sent, awaiting response… 200 OK
Length: 12238031 (12M) [application/octet-stream]
Saving to: 'latest.tar.gz'

latest.tar.gz      100%[========================================================================================>] 11.67M 359KB/s in 31s

2020-07-06 13:51:35 (380 KB/s) - 'latest.tar.gz' saved [12238031/12238031]
```

现在，你需要在 Apache 文件夹内解压该文件：

```bash
root@devops:~# tar -xf latest.tar.gz -C /var/www/html/
```

```bash
root@devops:~# ls /var/www/html/
```

```
index.html index.nginx-debian.html info.php wordpress
```

现在你可以看到 `/var/www/html` 目录下有一个 `WordPress` 文件夹，包含以下文件：

```bash
root@devops:~# cd /var/www/html/wordpress/
```

```bash
root@devops:/var/www/html/wordpress# ls
```

```
index.php  readme.html  wp-admin          wp-comments-post.php wp-content wp-includes      wp-load.php wp-mail.php    wp-signup.php    xmlrpc.php
license.txt wp-activate.php wp-blog-header.php wp-config-sample.php wp-cron.php wp-links-opml.php wp-login.php wp-settings.php wp-trackback.php
```

重要的文件是 `wp-config-sample.php`。我们将将其重命名为 `wp-config.php` 并通过它设置网站的数据库信息。现在我们开始吧：

```bash
root@devops:/var/www/html/wordpress# mv wp-config-sample.php wp-config.php
```

```bash
root@devops:/var/www/html/wordpress# vim wp-config.php
```

```php
/** The name of the database for WordPress */
define('DB_NAME', 'database_name_here');

/** MySQL database username */
define('DB_USER', 'username_here');

/** MySQL database password */
define('DB_PASSWORD', 'password_here');

/** MySQL hostname */
define('DB_HOST', 'localhost');

/** Database Charset to use in creating database tables. */
define('DB_CHARSET', 'utf8');

/** The Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');
```

此前，你可以看到 WordPress 已经告诉了你需要在哪里替换这些值，然后将文件修改为如下内容：

```php
/** The name of the database for WordPress */
define('DB_NAME', 'chapter03');

/** MySQL database username */
define('DB_USER', 'devops');

/** MySQL database password */
define('DB_PASSWORD', 'devops');

/** MySQL hostname */
define('DB_HOST', 'localhost');
```

设置好所有凭据和配置后，我们在 MariaDB 中创建相同的内容：

```bash
root@devops:/var/www/html/wordpress# mariadb
```

```
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 31
Server version: 10.1.44-MariaDB-0ubuntu0.18.04.1 Ubuntu 18.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```

```sql
MariaDB [(none)]> use chapter03
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed

MariaDB [chapter03]> grant all privileges on chapter03.* to devops@'%' identified by 'devops';
Query OK, 0 rows affected (0.00 sec)
```

我们刚刚创建了一个名为 `devops` 的用户，并授予了对 `chapter03` 数据库所有表的权限。现在，你可以通过浏览器访问了：

`http://192.168.178.62/wordpress`

![](img/Figure-3.3.jpg)

**图 3.3**

你可以使用以下参数填充字段：

- `Site Title: Chapter03`
- `Username: devops`
- `Password: devops`

点击 `Install and finish`（安装并完成），之后你需要点击 `Login`（登录）：

![](img/Figure-3.4.jpg)

**图 3.4**

使用你之前设置的凭据，你将看到 WordPress 管理后台：

![](img/Figure-3.5.jpg)

**图 3.5**

## 结论

我们刚刚使用 PHP、Apache 和 MariaDB 在 Linux 上搭建了最流行的技术栈。如果你正从事 Web 托管工作或作为自由职业 Web 开发人员，这对你将非常有帮助，因为你可以使用 WordPress 创建网站，并且你现在知道如何设置和管理你的服务器。这只是后续章节的准备工作，在后续章节我们将实现自动化。

# 第 4 章：配置 Nginx 反向代理

本章旨在解释 Nginx 是什么以及它的作用。

## 目标

学习本单元后，你应该能够：

- 什么是 Nginx
- 什么是反向代理
- 创建一个简单的页面
- 配置 Nginx

## 安装 Nginx

Nginx 是一个高性能 HTTP 服务器、反向代理、负载均衡器和邮件代理缓存。它因其速度和处理大量并发连接的能力而被广泛使用。

首先，让我们运行以下命令安装 Nginx：

```bash
root@devops:~# apt install nginx -y
```

```
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  nginx nginx-common
The following NEW packages will be installed:
  nginx nginx-common
0 upgraded, 2 newly installed, 0 to remove and 2461 kB of downloaded.
```

安装完成后，你可以通过以下命令检查此文件夹中的所有配置文件：

```bash
root@devops:~# ls /etc/nginx/
```

```
conf.d  fastcgi_params  modules-enabled  nginx.conf  sites-enabled  sites-available
```

你可能看到了它与 Apache 的某些相似之处。例如，这里也有 `sites-enabled` 和 `sites-disable`（应为 available）文件夹。所以你已经知道这些目录的作用了。然而，最重要的是 `nginx.conf`，它存储了 Web 服务器的主配置。我们可以使用 `grep` 来检查启用的行，换之即非注释行：

```bash
root@devops:~# grep -v "#" /etc/nginx/nginx.conf
```

```nginx
user www-data;
worker_processes auto;
pid /run/nginx.pid;
include /etc/nginx/modules-enabled/*.conf;

events {
    worker_connections 768;
}

http {
    sendfile on;
    tcp_nopush on;
    tcp_nodelay on;
    keepalive_timeout 65;
    types_hash_max_size 2048;
    include /etc/nginx/mime.types;
    default_type application/octet-stream;
    ssl_prefer_server_ciphers on;
    access_log /var/log/nginx/access.log;
    error_log /var/log/nginx/error.log;
    gzip on;
    include /etc/nginx/conf.d/*.conf;
}
```

```
include /etc/nginx/sites-enabled/*;
}
```

因此，此文件可以向你显示重要的行，例如每个 worker 的连接数，这样每个 worker 将负责响应 `768` 个连接。默认情况下，该值为 1，但我们可以为每个 CPU 处理器至少设置一个。如果你想检查你的 CPU 中中有多少个处理器，请运行以下命令：

```bash
root@devops:~# cat /proc/cpuinfo | grep processor
```

`processor     : 0`

上一个命令显示你的 CPU 中只有一个处理器。我在我的虚拟机上运行了这条命令。由于我只有一个处理器，如果我在我的物理机上运行，结果如下：

```bash
alisson@avell:~$ cat /proc/cpuinfo | grep processor
```

`processor      : 0`
`processor      : 1`
`processor      : 2`
`processor      : 3`
`processor      : 4`
`processor      : 5`
`processor      : 6`
`processor      : 7 show - show package details`

因此，在这种情况下，我可以配置我的 `Nginx` 使用 8 个 workers。如果你想这样做，只需在 worker connections 下方添加以下行即可：

```bash
Worker_processes 8;
```

重启你的服务器，配置将生效。

我们刚刚看到了一些重要的文件。现在是时候测试我们的 Web 服务器了。在上一章中，我们在虚拟机中安装了 Apache Web 服务器。所以，它可能仍然在运行。让我们检查端口 `80` 上是否有任何运行的进程：

![](img/p93.jpg)

上一个命令的输出打印在屏幕上。在我我的虚拟机中当前监听的所有服务中，如果 Apache 是其中之一，让我们停止它，禁用服务器并启动 `Nginx`：

```bash
root@devops:~# systemctl stop apache2
root@devops:~# systemctl disable apache2
```

`Synchronizing state of apache2.service with SysV service script with /lib/systemd/systemd-sysv-install.`
`Executing: /lib/systemd/systemd-sysv-install disable apache2`

现在，即使你重启虚拟机，Apache 仍然会处于停止状态。要启动并启用 Nginx，请运行以下命令：

```bash
root@devops:~# systemctl start nginx
root@devops:~# systemctl enable nginx
```

`Synchronizing state of nginx.service with SysV service script with /lib/systemd/systemd-sysv-install.`
`Executing: /lib/systemd/systemd-sysv-install enable nginx`

在浏览器中打开 IP 地址以检查首页：`http://192.168.178.62/`：

![](img/Figure-4.1.jpg)

**图 4.1**

有趣的是，它显示的是 Apache 示例页面。发生是因为 Nginx 使用与 Apache 相同的文件夹作为文档根。你可以使用以下命令进行检查：

```bash
root@devops:~# grep -v "#" /etc/nginx/sites-enabled/default
```

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;
    root /var/www/html;
    index index.html index.htm index.nginx-debian.html;
    server_name _;
    location / {
        try_files $uri $uri/ =404;
    }
}
```

`grep` 命令显示文档根被定义为 `/var/www/html`，这与 Apache 相同。如果你想看 Nginx 的默认首页，运行以下命令：

```bash
root@devops:~# cp -v /usr/share/nginx/html/index.html /var/www/html/
```



`'/usr/share/nginx/html/index.html' -> '/var/www/html/index.html'`

`grep`命令显示文档根被定义为`/var/www/html`，这与 Apache 相同。如果你想看 Nginx 的默认首页，运行以下命令：

![](img/Figure-4.2.jpg)

**图 4.2**

现在，你可以看到 Nginx 的默认页面了。

## 安装 Python

Python 如今是最著名的编程语言之一，主要在数据科学和 DevOps 等领域。它经常被用于自动化 Linux 任务以及使用 REST APIs 集成系统。几年前，我在一个名为 BeavOps 的系统中工作过。我负责为我以前工作的咨询公司处理学生入学注册。

该系统从 CRM 接收一个 JSON 文件，包含学生数据、相应的课程以及开始和结束日期。任务是使用这些数据创建一些程序，以集成许多不同的工具，如 Gitlab、Jenkins、Apache、MongoDB 等，目标是为学生创建一个带有 CI/CD 流水线的开发环境。该系统完全使用 Python、Flask 和 MongoDB 来存储数据。

要安装 Python，我们基本上需要两个包：

```bash
root@devops:~# apt install python3 python3-pip -y
```

`Reading package lists… Done`
`Building dependency tree`
`Reading state information… Done`
`python3 is already the newest version (3.6.7-1~18.04).`
`python3 set to manually installed.`

所以，这些选项是不言自明的。因此，让我们在实践中使用它们吧。安装完成后，使用`pip`安装 Flask 框架：

![](img/p95.jpg)

现在，你的环境已经准备好运行 Python 应用程序了。

## 使用 Flask 创建简单的页面

Flask 是一个 Python 的微框架，非常适合你创建 API。现在，你将学习如何使用这个微框架和 Python 创建一个简单的`Hello World`。你还将学习使用 Nginx 和 Gunicorn 部署你的应用程序的所有步骤。

让我们创建一个名为`app.py`的文件，内容如下：

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")

def index():

    return "DevOps with Linux"

if __name__ == "__main__":

    app.run(debug=True,host="0.0.0.0")
```

现在，运行以下命令：

```bash
root@devops:~# python3 app.py
```

`* Serving Flask app "app" (lazy loading)`
`* Environment: production`
`* WARNING: This is a development server. Do not use it in a deployment.`
`Use a production WSGI server instead.`
`* Debug mode: on`
`* Running on http://0.0.0.0:5000 (Press CTRL+C to quit)`
`* Restarting with stat`
`* Debugger is active!`
`* Debugger PIN: 179-281-442`

现在，即使你重启虚拟机，Flask 仍然在运行。为了在生产环境使用 Gunicorn，运行以下命令：

```bash
root@devops:~# gunicorn --chdir /root/ app:app -b "0.0.0.0"
```

`[2020-03-23 18:34:13 +0000] [23783] [INFO] Starting gunicorn 20.0.4`
`[2020-03-23 18:34:13 +0000] [23783] [INFO] Listening at: http://0.0.0.0:8000 (23783)`
`[2020-03-23 18:34:13 +0000] [23783] [INFO] Using worker: sync`
`[2020-03-23 18:34:13 +0000] [23786] [INFO] Booting worker with pid: 23786`

注意端口已经变了。现在，你必须使用端口`8000`：

![](img/Figure-4.4.jpg)

**图 4.4**

就是简单。然而，我们还希望在反向代理之后运行此应用程序。所以，让我们看看如何配置它。

## 配置反向代理

我们已经在虚拟机中安装了 Nginx，并且也知道了配置文件。既然如此，页面的配置可以在虚拟主机中找到，它们位于以下目录：

```bash
root@devops:~# ls /etc/nginx/sites-available/default
```

`/etc/nginx/sites-available/default`

然后，我们可以打开该文件，你的文件内容如下：

```
server {

    listen 80 default_server;

    listen [::]:80 default_server;

    server_name _;

    location / {

}
```

```bash
proxy_pass http://localhost:8000/ ;

}
```

重启服务器以启用配置：

```bash
root@devops:~# systemctl restart nginx

root@devops:~#
```

如果你尝试使用默认端口`80`访问服务器，将看到以下消息：

![](img/Figure-4.5.jpg)

**图 4.5**

发生这种情况是因为我们代理背后的服务器尚未运行。因此，让我们运行它并检查变化：

```bash
root@devops:~# gunicorn --chdir /root/ app:app

[2020-03-23 18:52:26 +0000] [24025] [INFO] Starting gunicorn 20.0.4

[2020-03-23 18:52:26 +0000] [24025] [INFO] Listening at: http://127.0.0.1:8000 (24025)

[2020-03-23 18:52:26 +0000] [24025] [INFO] Using worker: sync

[2020-03-23 18:52:26 +0000] [24028] [INFO] Booting worker with pid: 24028
```

这一次我们不需要传递`bind`选项（`-b`）来让服务器对所有 IP 地址可用。在当前情况下，服务器仅监听`localhost`。因此，Nginx 向世界开放接收连接并将其转发给 Gunicorn。

如果你再次尝试使用默认端口访问，你会发现现在我们能够看到服务正在运行了：

![](img/Figure-4.6.jpg)

**图 4.6**

环境已就绪。反向代理用于许多策略。最常见的策略之一是缓存静态文件，如 JavaScript、CSS 和 HTML。因此，所有进入的连接都由 Nginx 响应，只有动态内容会被转发到 Gunicorn。这种方式对 CPU 处理所有内容来说成本更低。在未来的章节中，我们将看到如何应用相同的逻辑，但是使用目前最常见的云服务。但是，如果你使用的是本地基础设施，这可以是提高性能的良好策略。

# 第 5 章：使用 Docker 部署应用程序

本章旨在解释如何安装 Docker、如何使用它、创建容器、镜像以及部署。

## 结构

在本章中，我们将讨论以下主题：

* Docker 简介
* 安装 Docker 并创建容器
* 使用`Dockerfile`创建镜像
* 部署镜像

## 目标

学习本单元后，你应该能够：

* 理解 Docker 是什么以及如何工作
* 设置 Docker 环境
* 创建容器和镜像
* 部署

## Docker 简介

Docker 是一个用于创建容器和版本的工具。对于具有更多 Linux 经验的人来说，可能已经通过`chroot`命令知道了容器。简单来说，容器是文件系统中的目录，允许你在其中安装另一个操作系统。正如`chroot`命令（更改`root`）所示，`/`将是新的目录。然而，整个操作系统需要更多文件。然后，在网络部分，Docker 底层使用`iptables`规则通过 NAT 重定向来管理一些简单的命令。

## 安装

首先，我们需要在我们的环境中安装 Docker。在官方文档中，你会找到所有步骤。这里有摘要：

```bash
apt-get update

apt-get remove docker-engine docker.io containerd -y
```

现在，我们只需要为 Docker 安装一些依赖项，如`apt-transport-https`：

```bash
apt-get install ca-certificates curl gnupg software-properties-common -y
```

以下命令将从`https`仓库下载 Docker 的某些包：

```bash
curl -fsSL https://download.docker.com/linux/ubuntu | apt-key add -
```

以下命令将添加 GNU 密钥以确保 Docker 仓库的真实性：

```bash
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

之前的命令是为了更新本地列表并安装 Docker 社区版：

```bash
apt-get update

apt-get install docker-ce docker-cli containerd.io -y
```

## 创建容器

环境已就绪。为了确保你的 Docker 运行良好，运行以下命令：

```bash
root@devops:~# systemctl status docker.service
```

现在，你的 Docker 安装已激活并运行。要创建一个容器，你只需要输入以下命令：

```bash
root@devops:~# docker run -ti centos /bin/bash

Unable to find image 'centos:latest' locally

latest: Pulling from library/centos

8a2915cefae: Downloading [=================================>] 72.58MB/73MB
```

之前的命令意味着我们需要运行带有 TTY（终端）的新容器，这由参数`-t`表示，交互式由参数`-i`表示。因此，我们可以在容器终端运行命令并看到它们的输出。当你的容器被创建时，你可以看到以下输出：

```bash
root@devops:~# docker run -ti centos /bin/bash

Unable to find image 'centos:latest' locally

latest: Pulling from library/centos

8a2915cefae: Pull complete

Digest: sha256:fe8d824220415eed5477b63addf0fb06c3b04940242b31982106ac204f6700

Status: Downloaded newer image for centos:latest

[root@595b4fceebc /]#
```

最后一行是重要的：

```
[root@595b4fceebc /]#
```

如果你与运行命令之前的终端进行比较：

```bash
root@devops:~# docker run -ti centos /bin/bash
```

你可以清晰地看到主机名发生了变化，这意味着我们现在处于容器内部，从现在开始运行的所有命令都将在容器内运行，虚拟机环境中不会安装任何内容。给容器的主机名`595b4fceebc`是容器 ID，用于管理你的容器。要退出容器，请输入`exit`或`Ctrl` + `D`：

```bash
[root@595b4fceebc /]#

exit

root@devops:~#
```

查看当前运行的容器，输入以下命令：

![](img/p104.jpg)

我们可以看到零容器在运行。发生这种情况是因为一旦你在容器终端输入`exit`或`Ctrl` + `D`，容器就会停止。要查看这一点，输入以下命令：

![](img/p104a.jpg)

现在，你可以看到你创建的容器。如果你看一眼，会发现`CONTAINER ID`列的值与我们创建它时的容器主机名完全相同。

然而，为什么 Docker 会有这种行为？为什么当我们退出容器时，容器会停止？这是因为在容器的概念中，一个容器是为了特定目的而创建，与虚拟机不同。因此，我们不需要担心容器的运行时间或维护。你可以直接删除它并创建一个新的。如果你想对容器进行更改，必须修改镜像、保存它、删除当前容器，并使用新版本启动新容器。

在我案例中，我创建了一个基于 CentOS 镜像的容器，我只是运行了`/bin/bash`命令，这让我的容器保持运行。一旦该命令停止运行，容器就会变成死亡状态。这同样适用于容器配置。如果你想更改重定向或任何其他参数，必须使用这些新参数创建一个新容器，保存它，然后运行新容器。

现在，我们将基于 CentOS 镜像创建一个新容器，并在这个容器中放入我们在上一节中学到的 Python 应用程序：

```
root@devops:~# docker run -ti --name python_app -p 5000:5000 centos /bin/bash
```

```
[root@ce7f74b0304a /]#
```

现在的创建速度明显比第一次快。这是因为 CentOS 镜像已经存在于我们的本地仓库中了。因此，Docker 不需要重新下载它。

使用以下命令在容器中安装依赖项：

```
[root@ce7f74b0304a /]# yum clean all && yum install python3 python3-pip -y
```

```
Failed to set locale, defaulting to C.UTF-8

0 files removed

Failed to set locale, defaulting to C.UTF-8

CentOS-8 - AppStream 11% [=======] 122 kB/s | 767 kB 00:49 ETA
```

在下载运行期间，我们现在有了一个新命令`yum`。这个命令对应 Ubuntu 上的 APT，你可以用它从远程仓库安装软件包。

下载完成后，为应用程序安装 Python 模块：

```
[root@ce7f74b0304a /]# python3 -m pip install flask
```

```
Successfully installed Jinja2-2.11.1 MarkupSafe-1.1.1 Werkzeug-1.0.1 click-7.1.1 flask-1.1.1 itsdangerous-1.1.0
```

将上一节使用的源代码复制到容器中：

```
[root@ce7f74b0304a /]# cat <<EOF > /srv/app.py
```

```
> from flask import Flask
> app = Flask(__name__)

> @app.route("/")
> def index():
> return "DevOps with Linux"

> if __name__ == "__main__":
> app.run(debug=True,host="0.0.0.0")
> EOF
```

运行应用程序查看它是否工作：

```
[root@ce7f74b0304a /]# python3 /srv/app.py
```

```
* Serving Flask app "app" (lazy loading)
* Environment: production
WARNING: This is a development server. Do not use it in a production deployment.
Use a production WSGI server instead.
* Debug mode: on
* Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
* Restarting with stat
* Debugger is active!
* Debugger PIN: 123-083-749
```

完美！现在，你可以通过浏览器进行测试：

![](img/Figure-5.1.jpg)

**图 5.1**

一切运行正常。现在，我们有一个正在运行的容器，里面有一个应用程序。依赖项已经安装，我们已经知道运行该应用程序的命令。现在，我们需要基于这个容器创建一个新镜像。为了创建镜像，我们需要退出容器。所以，让我们开始吧：

```
[root@ce7f74b0304a /]# python3 /srv/app.py
```



以下是对给定文本的排版处理结果：

---

### Flask 开发服务器启动日志

```
* Serving Flask app "app" (lazy loading)
* Environment: production
WARNING: This is a development server. Do not use it in a production deployment.
Use a production WSGI server instead.
* Debug mode: on
* Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
* Restarting with stat
* Debugger is active!
* Debugger PIN: 123-083-749
192.168.178.60 - - [02/Apr/2020 11:08:54] "GET / HTTP/1.1" 200 -
192.168.178.60 - - [02/Apr/2020 11:08:54] "GET /favicon.ico HTTP/1.1" 404 -
```

```
[root@ce7f74b0304a /]# exit
```

```
root@devops:~#
```

重要的行是最后几行，我输入`Ctrl`+`C`来停止应用程序，并输入`Ctrl`+`D`来退出容器：

![](img/p107.jpg)

我们现在有一个名为`python_app`的容器。如果你检查最后一列，这就是我们想要创建镜像的那个：

```
root@devops:~# docker commit python_app my_first_image
```

```
sha256:866e933c059b90a098cad06a1989d24bf16870caea1d691e2c0d3f4599f1608c
```

参数`commit`接收第一个参数容器；它可以是运行中的容器也可以是停止的容器，这无关；第二个参数是镜像名称。因此，我们正在创建一个名为`my_first_image`的新镜像。

你可以通过以下命令检查正在运行的镜像：

![](img/p108.jpg)

我们可以看到两个镜像；一个是我们从 Docker Hub 下载的 CentOS 镜像，它是官方仓库。另一个是我们刚刚创建的`my_first_image`。你只需要运行以下命令，就可以创建许多你想要的应用程序实例：

```
root@devops:~# docker run -ti -p 5000:5000 my_first_image python3 /srv/app.py
```

```
* Serving Flask app "app" (lazy loading)
* Environment: production
WARNING: This is a development server. Do not use it in a production deployment.
Use a production WSGI server instead.
* Debug mode: on
* Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
* Restarting with stat
```

参数`-p 5000:5000`将我们本地机器的端口`5000`映射到容器的端口`5000`。

如果你想发布你的镜像以便在任何其他服务器下载，你可以在 Docker Hub [`hub.docker.com/`](https://hub.docker.com/) 创建账户，并将你的镜像发送那里。在我案例中，我有一个账户了，所以我将教你如何将自己的镜像发送到 hub：

```
root@devops:~# docker login
```

```
Login with your Docker ID to push and pull images from Docker Hub
```

```
Username:
Password: 
Login Succeeded
```

```
root@devops:~# docker tag my_first_image alissonmenezes/my_first_image
```

```
root@devops:~# docker push alissonmenezes/my_first_image
```

```
Pushing to registry.hub.io/alissonmenezes/my_first_image...
Layer 1: pushed
Layer 2: pushed
Layer 3: pushed
Layer 4: pushed
Layer 5: pushed
Layer 6: pushed
Digest: sha256:866e933c059b90a098cad06a1989d24bf16870caea1d691e2c0d3f4599f1608c
Status: Pushed
```

`Deleted: sha256:fbf13ca6b28b7113d750e70b57c59e2cfc90ae6b3c7436166161c92eef1dc219`

`Untagged: centos:latest`

检查我们是否还有镜像：

![](img/p110a.jpg)

没有镜像。让我们根据推送到 hub 的镜像创建一个容器吧：

```
root@devops:~# docker run -ti -p 5000:5000 alissonmenezes/my_fist_image:latest python3 /srv/app.py
```

```
Unable to find image 'alissonmenezes/my_fist_image:latest' locally
latest: Pulling from alissonmenezes/my_fist_image
8a29a15cefae: Pull complete
f21402989f68: Pull complete
Digest: sha256:3c729fd3e1a595ff2bcf0937611732550ebde0c0d1945a87c01f979ca620b9fa
Status: Downloaded newer image for alissonmenezes/my_fist_image:latest
* Serving Flask app "app" (lazy loading)
* Environment: production
WARNING: This is a development server. Do not use it in a production deployment.
Use a production WSGI server instead.
* Debug mode: on
* Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
* Restarting with stat
* Debugger is active!
* Debugger PIN: 249-372-527
```

你现在可以看到，Docker 的主要目标是使用整个环境为应用程序创建镜像。我们刚刚创建了一个安装了`python3`且包含应用程序的 CentOS 版本。如果你想为应用程序创建一个新版本、更新 CentOS 版本，甚至更改底层操作系统（例如从 CentOS 迁移到 Alpine），你都可以做到。完成所有测试，创建一个相同名称的新镜像版本，将其推送到 hub，并将其下载到你的生产/测试/开发环境中。

## 使用 Dockerfile 创建镜像

现在你已经了解了创建镜像以及将其推送到 hub 的所有步骤，我们可以使用`Dockerfile`来自动化这些步骤。此文件可以帮助你跟踪对镜像所所的修改。当你仅仅创建一个容器、安装所有内容并创建镜像时，跟踪所有安装过的内容是一项艰巨的任务。因此，如果你想为同一个应用程序创建一个新版本，你就必须跟踪所有的依赖项和一切，以确保之前所有的依赖项仍然存在于新镜像中。

现在创建一个名为`Dockerfile`的文件，我们将容器内运行的所有步骤包含在该文件中：

```
root@devops:~# vim Dockerfile
from centos
maintainer alisson.copyleft@gmail.com
run yum clean all
run yum install python3 python3-pip -y
run python3 -m pip install flask
copy app.py /srv/app.py
expose 5000
cmd ["python3","/srv/app.py"]
```

之前，你拥有文件的内容，它完整包含了我们在容器内运行的所有命令。这些语句是自解释的，因此，你可以使用：

* `from`：指定基础镜像。

* `maintainer`：指定维护镜像的人员。

* `run`：在容器内执行命令。

* `copy`：从本地机器将一个文件复制到容器。

* `expose`：发布容器端口。

* `cmd`：确保容器运行的命令。

要根据`Dockerfile`创建镜像，请运行以下命令：

```
root@devops:~# docker build . -t my_new_image
```

```
Sending build context to Docker daemon 735.7kB
Step 1/8 : from centos
latest: Pulling from library/centos
8a29a15cefae: Pulling fs layer
```

Docker build 将在当前目录下查找`Dockerfile`。参数`-t`表示`TAG`（标签），它将定义镜像名称。因此，在命令完成后，你只需要运行以下命令创建一个新容器：

```
Successfully built b1b23966bb89
Successfully tagged my_new_image:latest
```

```
root@devops:~# docker run my_new_image
```

```
* Serving Flask app "app" (lazy loading)
* Environment: production
WARNING: This is a development server. Do not use it in a production deployment.
Use a production WSGI server instead.
* Debug mode: on
* Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
* Restarting with stat
* Debugger is active!
* Debugger PIN: 130-050-890
```

很容易看出，现在我们不需要传递任何额外的参数，因为所有的参数已经通过`Dockerfile`传递过了。`Dockerfile`基本上在创建新容器之前为我们执行了相同的步骤。如果你检查输出，将看到如下：

```
Successfully built b1b23966bb89
```

这是容器 ID，最后容器被标记了`docker build`中指定的名称：

```
Successfully tagged my_new_image:latest
```

你可以直接放入仓库名称并推送到那里。现在，你已经掌握了 Docker 的基础知识，这是你开始将应用程序 Docker 化的最低要求。

## 结论

总之，我们可以看到使用 Docker 进行工作是一项简单的任务。我们只需要将先前的知识应用到工作的不同领域即可。然后，你可以创建一个环境的版本，包括基础设施即代码（Infrastructure as Code），并将其发送到你想去的任何地方，但 Docker 本身对于大型生产环境是不够的。对于这一点，我们有一个关于 Kubernetes 的章节，而 Docker 是我们使用它的前提。

# 第 6 章：自动化你的基础设施即代码

本章旨在解释基础设施即代码如何工作、安装 Vagrant、如何使用它、如何使用 Shell 脚本自动化地创建新的虚拟机，以及设置我们之前完成的所有基础设施。

## 结构

在本章中，我们将讨论以下主题：

* 基础设施即代码简介

* 安装 Vagrant 并创建虚拟机

* 设置 LAMP 服务器

* 设置 Docker 服务器

## 目标

在学习完本单元后，你应该能够：

* 什么是 Vagrant 以及它是如何工作的

* 使用 Vagrant 自动化设置 Docker 环境

* 设置 Apache 服务器

* 自动化的益处

## 基础设施即代码简介

基础设施即代码（Infrastructure as Code）是一种技术，用于以类似于软件开发的方式记录、版本化和维护你基础设施的控制。然后，你可以创建一个描述基础设施所需状态的文件，将其部署到测试环境，验证你的代码，部署到暂存环境，如果一切顺利，你就可以进入生产环境。这可以通过流水线实现；因此，你可以对所有环境使用相同的代码，并使用为每个环境定义的变量更改服务器的大小。

## 什么是 Vagrant 以及它是如何工作的？

在书的开头，你将学习如何设置 VirtualBox、下载 ISO、创建虚拟机、挂载 ISO 并格式化和安装操作系统。然而，这是 DevOps 工程师日常生活中经常重复的任务。你能想象自己每天安装 100 台虚拟机并在工作结束后销毁它们以节省费用吗？这太疯狂了。但是，当我们使用基础设施即代码（IaC）时，这项变得非常简单，因为你只需要点击并运行一些命令来创建和销毁一切。

Vagrant 是可以与 Virtual Box 集成的工具。它负责读取你的代码，将其转换为 VirtualBox 命令，并在虚拟机内运行代码。你不需要执行第一章中学到的所有步骤。HashiCorp 创建了 Vagrant，他们有一个官方镜像仓库，你可以用它来设置环境。所以，你不需要去官方网站、下载 ISO 并设置机器。

## Vagrant 安装

你可以从以下链接下载 Vagrant：

**[`www.vagrantup.com/downloads.html`](https://www.vagrantup.com/downloads.html)**

我使用的是 Windows，所以我将下载 MSI 版本。

![](img/Figure-6.1.jpg)

**图 6.1**

安装过程与其他在 Windows 上安装的任何软件一样简单。你只需要打开 MSI 文件并按照流程点击`Next`、`Next`即可：

![](img/Figure-6.2.jpg)

**图 6.2**

然后在，保持所有默认选项的情况下点击`Finish`：

![](img/Figure-6.3.jpg)

**图 6.3**

现在，安装已经完成，让我们学习基础知识吧。

## 使用方法

首先，像我做的那样创建一个文件夹来存储你的 Vagrant 文件：

![](img/p118.jpg)

我创建了一个名为`VagrantChaper`的文件夹并进入了该文件夹。现在它是空的。要创建你的第一个代码，请输入以下命令：

```
PS C:\Users\1511 MXTI\VagrantChapter> vagrant init
```

```
此目录下已放置一个 'Vagrantfile'。你现在已准备好 'vagrant up' 你的第一个虚拟机环境了！请阅读 Vagrantfile 中的注释以及 'vagrantup.com' 上的文档以获取更多关于使用 Vagrant 的信息。
```

```
PS C:\Users\1511 MXTI\VagrantChapter>
```

命令`vagrant init`会创建一个示例文件，包含大多数虚拟机情况的常用配置。让我们查看文件内容：

```
PS C:\Users\1511 MXTI\VagrantChapter> cat .\Vagrantfile
```

```
# -*- mode: ruby -*-
# vi: set ft=ruby :
# 所有 Vagrant 配置都在下方完成。Vagrant.configure 中的
# "2" 配置了配置版本（为了向后兼容，我们支持旧的样式）。
# 除非你清楚自己在做什么，否则请不要更改它。
Vagrant.configure("2") do |config|
# 最常用的配置选项在下方提供了文档和注释。
# 如需完整参考，请参阅在线文档：
# https://docs.vagrantup.com。
# 每个 Vagrant 开发环境都需要一个 box（镜像）。你可以在
# https://vagrantcloud.com/search  boxes。
config.vm.box = "base"
# 禁用自动 box 更新检查。如果你禁用了此项，则
# 只有在用户运行 'vagrant box outdated' 时才会检查更新。
# 这不建议这样做。
# config.vm.box_check_update = false
# 创建转发端口映射，允许从宿主机的端口
# 访问虚拟机内的特定端口。在下面的示例中，
# 访问 "localhost:8080" 将访问虚拟机上的 80 端口。
# 注意：这将启用对打开端口的公共访问
# config.vm.network "forwarded_port", guest: 80, host: 8080
# 创建转发端口映射，允许从宿主机的端口
# 访问虚拟机内的特定端口，并仅允许通过 127.0.0.1 访问禁用公共访问
# config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
# 创建私有网络，允许使用特定的 IP
# 仅主机访问虚拟机。
```




# `config.vm.network "private_network", ip: "192.168.33.10"`

# 创建公共网络，通常对应于桥接网络。

# 桥接网络使虚拟机看起来像你网络上的另一个物理设备。

# `config.vm.network "public_network"`

# 向虚拟机共享额外的文件夹。第一个参数是

# 宿主机上实际文件夹的路径。第二个参数是

# 虚拟机上挂载文件夹的路径。可选的第三

# 参数是一组非必需选项。

# `config.vm.synced_folder "../data", "/vagrant_data"`

# 特定提供者的配置，允许你对 Vagrant 的各种

# 后端提供者进行微调。这些提供了特定的选项。

# VirtualBox 示例：

#

# # 在启动机器时显示 VirtualBox GUI

# `vb.gui = true`

#

# # 自定义虚拟机的内存量：

# `vb.memory = "1024"`

# end

#

# 查看你正在使用的提供者的文档以获取有关可用选项的更多信息。

# 使用 shell 脚本启用配置（provisioning）。其他可用配置器

# 如 Ansible, Chef, Docker, Puppet 和 Salt。请查看文档

# 获取更多关于其特定语法和使用的信息。

# `config.vm.provision "shell", inline: <<-SHELL`

# `apt-get update`

# `apt-get install -y apache2`

# `SHELL`

`end`

在同一个文件夹中，运行以下命令：

```
PS C:\Users\1511 MXTI\VagrantChapter> vagrant status
```

当前机器状态：
`default` not created (virtualbox)

这意味着我们有一个名为 `default` 的虚拟机（VM），但它还没有被创建。所以，我们将创建一个。

示例文件包含一些配置和许多注释，简要解释了这些命令的作用。该文件使用默认配置允许你只创建一个虚拟机。在本章中，我们将创建两个虚拟机，一个安装了 LAMP 服务器，另一个安装了 Docker。我将修改该文件，并解释示例文件与新文件之间的差异：

```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/focal64"
  config.vm.box_check_update = false

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  config.vm.define "lamp" do |lamp|
    lamp.vm.network "private_network", ip: "192.168.33.10"
    lamp.vm.provision "shell", inline: <<-SHELL
      apt-get clean
      apt update -y
    SHELL
  end

  config.vm.define "docker" do |docker|
    docker.vm.network "private_network", ip: "192.168.33.11"
    docker.vm.provision "shell", inline: <<-SHELL
      apt-get clean
      apt update -y
    SHELL
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get clean
    apt update -y
  SHELL

end
```

前面的文件是我修改后的。它比示例文件更简洁，并且做了更多。让我们运行 `vagrant status` 看看发生了什么：

```
PS C:\Users\1511 MXTI\VagrantChapter> vagrant status
```

当前机器状态：
`lamp` not created (virtualbox)
`docker` not created (virtualbox)

有趣的是，现在我们有两个虚拟机，一个名为 `lamp`，另一个名为 `docker`。它们还没有被创建。在新文件中，我使用了名为 `multi-machine` 的 Vagrant 资源。它允许在一个文件中创建多个机器。

现在，让我们分析文件以及在创建虚拟机之前会发生什么：

```ruby
config.vm.box = "ubuntu/focal64"
config.vm.box_check_update = false

config.vm.provider "virtualbox" do |vb|
  vb.memory = "1024"
end
```

这部分 `config.vm` 是适用于文件中声明的所有虚拟机的通用配置。因此，所有机器将具有 1024 MB 的内存。`config.vm.box` 是将在虚拟机使用的镜像。在我们的案例中，我们将使用 Ubuntu 服务器，版本 20.04：

```ruby
config.vm.define "lamp" do |lamp|
  lamp.vm.network "private_network", ip: "192.168.33.10"
  lamp.vm.provision "shell", inline: <<-SHELL
    apt-get clean
    apt update -y
  SHELL
end
```

在这一部分，我们为 `lamp` 机器提供了本地配置。它是专门为名为 `lamp` 的虚拟机设置的。然后，在这个定义的虚拟机将具有 IP 地址 `192.168.33.10`，以及在配置中运行的命令，即在此部分：`lamp.vm.provision`。它也适用于 Docker 虚拟机：

```ruby
config.vm.provision "shell", inline: <<-SHELL
  apt-get clean
  apt update -y
SHELL
```

在最后一部分，我们有 `config.vm.provision`。在这个块中，你可以定义在所有虚拟机中运行的命令，但 `lamp.vm.provision`（它仅在 `lamp` 虚拟机中运行）和 `docker.vm.provision`（它仅在 Docker 虚拟机中运行）除外。

## 运行

在解释了文件并完成配置以创建虚拟机后，输入以下命令：

```
PS C:\Users\1511 MXTI\VagrantChapter> vagrant up --provider=virtualbox
```

```
Bringing machine 'lamp' up with 'virtualbox' provider…
Bringing machine 'docker' up with 'virtualbox' provider…
==> lamp: Box 'ubuntu/focal64' could not be found. Attempting to find and install…
    lamp: Box Provider: virtualbox
    lamp: Box Version: >= 0
==> lamp: Loading metadata for box 'ubuntu/focal64'
    lamp: URL: https://vagrantcloud.com/ubuntu/focal64
```

这需要一段时间，因为 Vagrant 正在下载 box：

```
==> lamp: Loading metadata for box 'ubuntu/focal64'
    lamp: URL: https://vagrantcloud.com/ubuntu/focal64
==> lamp: Adding box 'ubuntu/focal64' (v20200409.0.0) for provider: virtualbox
    lamp: Downloading: https://vagrantcloud.com/ubuntu/boxes/focal64/versions/20200409.0.0/providers/virtualbox.box
    lamp: Download redirected to host: cloud-images.ubuntu.com
    lamp: Progress: 11% (Rate: 1411k/s, Estimated time remaining: 0:06:09)
```

该 box 是一个云镜像，但针对在 Vagrant 之上运行进行了特定配置。正如你在日志所示，Vagrant 正在为 VirtualBox 下载镜像。你也可以使用 Hyper-V 或 KVM 进行配置。

Vagrant Cloud ([`vagrantcloud.com/`](http://vagrantcloud.com/)) 是下载镜像的官方仓库。当然，它并不是唯一的。你也可以使用 Packer ([`packer.io/`](https://packer.io/)) 创建自己的镜像。然而，如果你没有这样做，你可以在那里搜索有哪些可用镜像供你创建虚拟机。

![](img/Figure-6.4.jpg)

**图 6.4**

配置完成后，如果你想检查本地的 boxes，请使用以下命令：

```
PS C:\Users\1511 MXTI\VagrantChapter> vagrant box list
```

```
centos/7             (virtualbox, 1801.02)
fedora/28-cloud-base  (virtualbox, 20180425)
ubuntu/bionic64      (virtualbox, 20190807.0.0)
ubuntu/focal64       (virtualbox, 20200409.0.0)
ubuntu/xenial64      (virtualbox, 20180413.0.0)
Status: Downloaded newer image for
```

如果是全新的安装，你可能只有我们下载的 `ubuntu/focal64`：

```
PS C:\Users\1511 MXTI\VagrantChapter> vagrant status
Current machine states:
lamp     running (virtualbox)
docker   running (virtualbox)
```

如果配置一切顺利，运行 `vagrant status` 命令，它将向你显示运行中的虚拟机。如果虚拟机尚未创建，你可以尝试重新运行 `vagrant up --provider=virtualbox` 看看是否有效。如果无效，请检查你的安装情况和网络连接。

假设你没有定义任何密码或 SSH Key 来连接这些虚拟机，那么我们如何连接它们呢？Vagrant 也为我们管理这些。通过 `vagrant status`，我们可以看到虚拟机的名称，并使用这些名称通过 `vagrant ssh` 命令进行连接：

```
PS C:\Users\1511 MXTI\VagrantChapter> vagrant ssh docker
Welcome to Ubuntu Focal Fossa (development branch) (GNU/Linux 5.4.0-21-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage
```

虚拟机已成功配置，正如 Ubuntu Focal Fossa 版本所示，Vagrant 还创建了一个名为 `vagrant` 的用户来连接虚拟机，该用户拥有 `sudo` 权限。因此，我们可以切换用户并运行所有命令：

```
vagrant@ubuntu-focal:~$ sudo su -
root@ubuntu-focal:~#
```

现在你可以像我们在之前的章节中那样管理一切了。但是，让我们看看如何以自动方式配置 LAMP。

## 搭建 LAMP 服务器

你已经知道这些命令，那么我们基本上可以将这些命令放在 vagrant 文件的配置部分，并再次配置虚拟机：

```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.box_check_update = false

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  config.vm.define "lamp" do |lamp|
    lamp.vm.network "private_network", ip: "192.168.33.10"
    lamp.vm.hostname = "lamp"
    lamp.vm.provision "shell", inline: <<-SHELL
      sudo apt-get clean
      sudo apt update -y
      sudo apt install apache2 mysql-server php7.4 -y
    SHELL
  end

  config.vm.define "docker" do |docker|
    docker.vm.network "private_network", ip: "192.168.33.11"
    docker.vm.hostname = "docker"
    docker.vm.provision "shell", inline: <<-SHELL
      apt-get clean
      apt update -y
    SHELL
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get clean
    apt update -y
  SHELL
end
```

在这种情况下，我修改了 `lamp.vm.provision`，包含了用于安装 PHP、Apache 和 MySQL 服务器的 Shell 脚本。虚拟机创建后，运行以下命令：

```
PS C:\Users\1511 MXTI\VagrantChapter> vagrant provision lamp
```

```
==> lamp: Running provisioner: shell…
    lamp: Running: inline script
    lamp:
    lamp: WARNING: apt does not have a stable CLI interface. Use with caution in scripts.
    lamp: Get:1 http://archive.ubuntu.com/ubuntu
    lamp: Get:2 http://archive.ubuntu.com/ubuntu-security
    lamp: Get:3 http://archive.ubuntu.com/ubuntu-updates
```

注意，我仅针对 Docker VM 更改了 box，因为在 Docker 仓库中，还没有对 Focal Fossa 的支持。但观察我们如何创建不同操作系统的不同 VM 也很有趣。

现在，在 Docker VM 的配置（provision）部分，我们已经包含了设置服务器的所有安装步骤。然后，你可以再次启动机器：

```
PS C:\Users\1511 MXTI\VagrantChapter> vagrant up docker
Bringing machine 'docker' up with 'virtualbox' provider…
==> docker: Importing base box 'ubuntu/focal64'…
==> docker: Matching MAC address for NAT networking…
==> docker: Setting the name of the VM: VagrantChapter_docker_1586798805547_50415
==> docker: Fixed port collision for 22 => 2222\. Now on port 2200.
```

运行 `provision` 命令：

```
PS C:\Users\1511 MXTI\VagrantChapter> vagrant provision docker
==> docker: Running provisioner: shell…
    docker: Running: inline script
    docker: WARNING:
    docker: apt
    docker: does not have a stable CLI interface.
    docker: Use with caution in scripts.
```



`docker: Get:1 http://archive.ubuntu.com/ubuntu focal InRelease [265 kB]`

让我们检查安装是否成功完成：

```
PS C:\Users\1511 MXTI\VagrantChapter> vagrant ssh docker

Welcome to Ubuntu 18.04.3 LTS (GNU/Linux 4.15.0-55-generic x86_64)

* Documentation:  https://help.ubuntu.com

* Management:      https://landscape.canonical.com

* Support:          https://ubuntu.com/advantageSuccessfully installed Jinja2-2.11.1 MarkupSafe-1.1.1 Werkzeug-1.0.1 click-7.1.1 flask-1.1.1 itsdangerous-1.1.0
```

检查 Docker 是否已启动运行。如果你遇到某些连接问题，检查 VirtualBox 上的主机网络管理器（Host Network Manager）是否启用非常重要。

![](img/Figure-6.6.jpg)

**图 6.6**

检查 DHCP 服务器列是否启用，并确认 IPv4 地址是否存在于网络 `192.168.33.0/24` 中，如下截图所示：

![](img/Figure-6.7.jpg)

**图 6.7**

## 结论

在本章中，我们看到了使用 Vagrant 这种工具的优势，它允许我们编写 VM 配置，如操作系统镜像、IP 地址、主机名、VM 内存等。在配置（provision）部分，我们可以编写 Shell 脚本，脚本将在启动时运行。如果没有运行，或者你想再次运行脚本，可以执行命令`vagrant provision`。Vagrant 允许你使用 Ansible、Puppet 或 Chef 等不同技术来创建配置脚本。我使用了 Shell 脚本作为示例，但欢迎测试并创建你自己的脚本。我们学到的另一个重要点是 Vagrant file。在这个文件中，你定义了一切，并可以与团队共享内容，这样他们就可以参与到你的开发环境中。

# 第 7 章

## 使用云服务创建你的基础设施

本章旨在向你介绍最大的云服务商，以及我们如何利用它们来加速基础设施的配置、扩展性和可靠性。

## 结构

在本章中，我们将讨论以下主题：

* 云和主要参与者
* 使用 AWS 进行配置
* 使用 GCP 进行配置
* 使用 Azure 进行配置

## 目标

学习本单元后，你应该能够：

* 定义什么是云以及如何使用它
* 在每个服务商上设置环境
* 使用命令行创建简单的基础设施
* 在云控制台中检查创建的基础设施

### 云和主要参与者

到目前为止，我们一直使用自己的电脑来创建一切。然而，在生产环境中运行应用程序需要很多支持，例如高可用性、备份、监控、冗余等。在过去，许多公司拥有自己的数据中心或本地服务器，并 24*7 小时运行。因此，管理一切需要耗费大量精力，因为不仅要维护虚拟机或软件，还需要管理网络、存储、能源、不间断运行、互联网连接以及许多涉及 IT 的其他事务。此外，还需要一个拥有不同技能的团队来管理一切，并且需要人员上的冗余，因为如果公司里的某些员工生病了，你必须有其他人可用，以防某些环节停止工作。

当我开始在 IT 行业工作时，我曾就职的一些公司正在使用一种称为 Colocation（托管）的服务，你基本上可以在数据中心内租用一个机架（Rack），并安装你的服务器。因此，你只需要管理自己的服务器。网络、能源和互联网部分都交给了提供服务的公司。过了一段时间，我们开始使用一家名为`SoftLayer`的公司的服务。他们有自己的数据中心，当我们租服务器时，可以付费并使用一段时间物理服务器。

在此之后，我们开始与`AWS`合作，这是一家云公司。在那里，我们可以租用虚拟机，就像我们在前面的章节中创建的 VM 一样。使用此服务有很多好处，例如高可用性。所以，如果他们数据中心里的某个物理服务器故障，你只需要关闭 VM 并在另一台服务器上启动它，甚至可以付费让他们为你进行备份。这样，一个人就可以管理包含数百台服务器的整个基础设施。

### AWS

Amazon Web Services 是目前主要的云服务参与者。他们有几十种服务，可以使用它们来部署应用程序、监控、备份、创建 VM、数据库、队列等。它还允许你使用命令行以自动化方式创建一切，这被称为`AWSCLI`。但当然，使用他们所有的服务并不那么容易。这就是为什么他们创建了许多课程和认证，以便人们获得资质并充分利用他们服务提供的功能。

### GCP

Google Cloud Platform（谷歌云平台）是最新的。他们提供的许多服务与 AWS 类似，但他们还没有拥有所有的服务。尽管如此，他们拥有一些独特的服务，比如`Big Query`，它是查询大型数据集和将数据存储在云端常用的工具之一。此外，如果你从事机器学习，他们提供了可用的集群来配合`TensorFlow`项目发挥最大性能。GCP 通常比其他大竞争对手便宜。我正用它处理我的个人项目。

### Azure

这是微软的云平台。所以，如果你计划将活动目录（Active Directory）导出到云端，这就是你的选择。他们有独特的服务，如`SQL server`、`Azure Active Directory`甚至非常著名的`Azure DevOps`。我过去就职的一些大公司曾使用 Azure 作为他们的主平台，因为微软是一家可靠的公司。但他们也是最贵的。所以，如果钱不是你的问题，而且你在应用程序中使用了微软产品，这就是正确的选择。

### 使用 AWS 进行配置

AWS 有自己的课程来解释如何使用所有服务。那么，我这里的目标是向你展示如何提供与我们使用 VirtualBox 和 Vagrant 时相同的基础设施。因此，我将关注 VM 以及我们如何在上面安装东西。

因此，你的第一个任务是创建你自己的 AWS 账户。你可以访问以下链接进行创建：

`http://console.aws.amazon.com/`

创建账户并登录控制台后，你将看到如图所示的页面：

![](img/Figure-7.1.jpg)

**图 7.1**

该控制台允许你创建任何你的服务。现在，点击`Services`|`EC2`|`Running Instances`。你会看到以下页面：

![](img/Figure-7.2.jpg)

**图 7.2**

我的账户是空的。我过去使用过更多的 AWS，目前在我的工作中使用 Azure，并在个人项目中使用 GCP。然而，这是你用来管理虚拟机（VMs）的控制台。对你来说，知道在控制台中哪里查看你的虚拟机非常重要，因为这样更容易看到你拥有的监控情况。但从现在开始，我们将使用命令行创建一切。所以，现在请安装 Python，然后输入以下 AWS 命令行：

`https://www.python.org/downloads/`

安装 Python 后，运行以下命令行安装 AWS CLI：

```
PS C:\Users\1511 MXTI> python -m pip install awscli --user

Collecting awscli
```

要检查 AWS CLI 是否安装成功，运行以下命令：

```
PS C:\Users\1511 MXTI> aws --version

aws-cli/1.18.42 Python/3.8.2 Windows/10 botocore/1.15.42
```

一切运行正常。现在，为了配置访问权限，你需要创建一个具有程序化访问的 IAM 账户。最简单的方法是点击`Services`并输入`IAM`，如下截图所示：

![](img/Figure-7.3.jpg)

**图 7.3**

`IAM`意味着`Identity Access Management`（身份访问管理）。该服务负责创建和管理用户及组。在仪表板中，点击`Users`|`Add User`:

![](img/Figure-7.4.jpg)

**图 7.4**

我正在创建一个名为 DevOps 的新用户，并开启程序化访问：

![](img/Figure-7.5.jpg)

**图 7.5**

直接选择`Attach existing policies`选项，会出现`AdministratorAccess`策略。此策略将允许我们的用户在 AWS 账户中执行所有操作。此权限不推荐用于生产环境。用户必须仅拥有特定目的所需的权限。

![](img/Figure-7.6.jpg)

**图 7.6**

保存用户后，你将被重定向到带有`Access Key`（访问密钥）和`Secret Key`（秘密密钥）的页面。保存这些值，因为你永远无法再次获得`Secret Key`。唯一的方法是重新创建一个新用户。

![](img/Figure-7.7.jpg)

**图 7.7**

遵循这些步骤后，我们可以配置命令行并测试我们是否能够连接到控制台。第一个任务是将我们的密钥添加到本地环境中：

```
PS C:\Users\1511 MXTI> aws configure

AWS Access Key ID [None]: YOU_ACCESS_KEY

AWS Secret Access Key [None]: YOUR_SECRET_KEY

Default region name [None]: eu-central-1

Default output format [None]:
```

在区域名称中，我设置了`eu-central-1`，它对应`Frankfurt`，因为我住在`Germany`。人们通常将此选项设置为`us-east-1`，它对应美国的弗吉尼亚。所以，这取决于你的决定。

现在，你可以使用以下命令检查是否有任何示例实例：

```
PS C:\Users\1511 MXTI> aws ec2 describe-instances

{
  "Reservations": []
}
```

我没有任何示例实例，但在使用控制台时创建一个是一项简单的任务。只需点击几次，你就可以创建一个。然而，你无法实现自动化。要实现自动化，你需要使用命令行，为此，你应该了解虚拟机所需的每一个对象。

第一个是创建 SSH 密钥。在创建虚拟机后，访问它是必须的。

```
PS C:\Users\1511 MXTI> aws ec2 create-key-pair --key-name DevopsBook --query'KeyMaterial' --output text YOUR_PRIVATE_KEY
```

参数`--query`用于仅以纯文本格式获取私钥。否则，你只会得到一个字符串，这在使用它时会产生文件格式问题。

复制私钥并将其保存到文件中。在我的情况下，我将其保存为`devopbook.pem`，这是 AWS 使用的标准格式。

每个实例都需要 IP 地址。否则，你将无法远程访问它。但是，为了拥有 IP 地址，需要子网（subnet）且需要按顺序。现在，让我们使用以下命令创建一个网络：

```
PS C:\Users\1511 MXTI> aws ec2 create-vpc --cidr-block "192.168.0.0/24"

{
  "Vpc": {
    "CidrBlock": "192.168.0.0/24",
    "DhcpOptionsId": "dopt-891c21e2",
    "State": "pending",
    "VpcId": "vpc-0825b5c6f6a2a2429",
    "OwnerId": "360560397478",
    "InstanceTenancy": "default",
    "Ipv6CidrBlockAssociationSet": [],
    "CidrBlockAssociationSet": [
      {
        "AssociationId": "vpc-cidr-assoc-07b70a566b3a97801",
        "CidrBlock": "192.168.0.0/24",
        "CidrBlockState": {
          "State": "associated"
        }
      }
    ],
    "IsDefault": false,
    "Tags": []
  }
}
```

AWS 上的虚拟网络被称为`VPC`（虚拟私有云）。必须指定 CIDR 块，它代表网络大小，允许我们拥有 254 个可用地址。保存`VpcId`。我们稍后会需要它。

下一步是创建子网。使用以下命令：

```
PS C:\Users\1511 MXTI> aws ec2 create-subnet --cidr-block "192.168.0.0/24" --vpc-id vpc-0825b5c6f6a2a2429

{
  "Vpc": {
    "CidrBlock": "192.168.0.0/24",
    "DhcpOptionsId": "dopt-891c21e2",
    "State": "pending",
    "VpcId": "vpc-0825b5c6f6a2a2429",
    "OwnerId": "360560397478",
    "InstanceTenancy": "default",
    "Ipv6CidrBlockAssociationSet": [],
    "CidrBlockAssociationSet": [
      {
        "AssociationId": "vpc-cidr-assoc-07b70a566b3a97801",
        "CidrBlock": "192.168.0.0/24",
        "CidrBlockState": {
          "State": "associated"
        }
      }
    ],
    "IsDefault": false,
    "Tags": []
  }
}
```

AWS 上的虚拟网络被称为`VPC`（虚拟私有云）。我必须指定 CIDR 块，它代表网络大小，允许我们拥有 254 个可用地址。保存`VpcId`。我们稍后会需要它。

下一步是创建子网。使用以下命令：

```
PS C:\Users\1511 MXTI> aws ec2 create-subnet --cidr-block "192.168.0.0/24" --vpc-id vpc-0825b5c6f6a2a2429
```



AWS 上的虚拟网络被称为 `VPC`（虚拟私有云）。我必须指定 CIDR 块，它代表网络大小，允许我们拥有 254 个可用地址。保存 `VpcId`。我们稍后会需要它。

AWS 上的虚拟网络被称为 `VPC`（虚拟私有云）。我必须指定 CIDR 块，它代表网络大小，允许我们拥有 254 个可用地址。保存 `VpcId`。我们稍后会需要它。该实例没有访问互联网的权限。因此，我们需要使用以下命令为其创建一个互联网网关（Internet Gateway）：

```bash
PS C:\Users\1511 MXTI>aws ec2 create-internet-gateway
```

```json
{
  "InternetGateway": {
    "Attachments": [],
    "InternetGatewayId": "igw-05d94c382dd27185b",
    "Tags": []
  }
}
```

现在，我们需要将互联网网关与 VPC 关联，这样同一个 VPC 内的所有实例都将访问互联网。

```bash
PS C:\Users\1511 MXTI>aws ec2 attach-internet-gateway --internet-gateway-id igw-05d94c382dd27185b --vpc-id vpc-0825b5c6f6a2a2429
```

即使创建了互联网网关和 VPC，仍然需要一个默认路由。默认情况下，所有连接都会尝试首先通过互联网。你可以使用以下命令来检查路由表：

```bash
PS C:\Users\1511 MXTI>aws ec2 describe-route-tables
```

```json
{
  "RouteTables": [
    {
      "Associations": [
        {
          "Main": true,
          "RouteTableAssociationId": "rtbassoc-0388bce2f3bf06f9b",
          "RouteTableId": "rtb-0ba4bf0ea11f024ee",
          "AssociationState": {
            "State": "associated"
          }
        }
      ],
      "PropagatingVgws": [],
      "RouteTableId": "rtb-0ba4bf0ea11f024ee",
      "Routes": [
        {
          "DestinationCidrBlock": "192.168.0.0/24",
          "GatewayId": "local",
          "Origin": "CreateRouteTable",
          "State": "active"
        }
      ],
      "Tags": [],
      "VpcId": "vpc-0825b5c6f6a2a2429",
      "OwnerId": "360560397478"
    }
  ]
}
```

ID 为 `rtb-0ba4bf0ea11f024ee` 的路由与 VPC `vpc-0825b5c6f6a2a2429` 关联，这就是我们创建的 VPC。因此，我们需要分配一条新路由，以便所有目标为 `0.0.0.0/0` 的连接都能通过 ID 为 `igw-05d94c382dd27185b` 的互联网网关。

```bash
PS C:\Users\1511 MXTI>aws ec2 create-route --route-table-id rtb-0ba4bf0ea11f024ee --destination-cidr-block 0.0.0.0/0 --gateway-id igw-05d94c382dd27185b
```

```json
{
  "Return": true
}
```

现在，你可以创建一个公 IP 地址，并使用以下命令检查我们是否可以连接：

```bash
PS C:\Users\1511 MXTI>aws ec2 allocate-address
```

```json
{
  "PublicIp": "18.156.153.94",
  "AllocationId": "eipalloc-04066542351eff3a4",
  "PublicIpv4Pool": "amazon",
  "NetworkBorderGroup": "eu-central-1",
  "Domain": "vpc"
}
```

现在我们已经有了公 IP，并需要将其分配给实例：

```bash
PS C:\Users\1511 MXTI>aws ec2 associate-address --allocation-id eipalloc-04066542351eff3a4 --instance-id i-0d26f9c327b92b630
```

```json
{
  "AssociationId": "eipassoc-07026da6c9093c86a"
}
```

让我们再次检查一次实例：

```bash
PS C:\Users\1511 MXTI> aws ec2 describe-instances --query "Reservations[*].Instances[*].{Instance:InstanceId,State:State,DNS:PublicDnsName, IP:PublicIpAddress}"
```

```json
[
  [
    {
      "Instance": "i-0d26f9c327b92b630",
      "State": {
        "Code": 16,
        "Name": "running"
      },
      "DNS": "",
      "IP": "18.156.153.94"
    }
  ]
]
```

现在我们已经将 IP 地址 `18.156.153.94` 分配给了实例。我们还没有公网 DNS，但可以尝试使用 IP 进行连接。还记得我们在创建 SSH 时保存的私钥（Private Key）吗？你现在需要它：

```bash
PS C:\Users\1511 MXTI>ssh -i devopskey.pem ubuntu@18.156.153.94
```

```text
The authenticity of host '18.156.153.94 (18.156.153.94)' can't be established.
ECDSA key fingerprint is SHA256:N5kMSWQKVwBLycjjUpzJ/AsRnRbBvDVqagBJunxCXyA.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '18.156.153.94' (ECDSA) to the list of known hosts.
```

```text
Welcome to Ubuntu 18.04.3 LTS (GNU/Linux 4.1)
```

![](img/Figure-7.8.jpg)

**图 7.8**

在 Google 上，创建虚拟机（VM）的服务名称为 `Google Compute Engine`。使用此服务，我们将能够像在 Amazon 上完全相同的方式进行创建。

### 激活计费

首先，你需要激活账户中的计费功能。在项目内的 `Dashboard` 中，点击 `Go to Compute Engine`，在那里你有一个名为 `Enable billing` 的按钮，如下图所示：

![](img/Figure-7.9.jpg)

**图 7.9**

点击它并等待几分钟让配置完成。一旦配置完成，你可以使用以下命令找到想要创建实例的镜像：

![](img/p150.jpg)

你将发现很多选项。在我的案例中，我将使用 `ubuntu-1804-xenial-20200407`。你还需要选择要创建 VM 的区域：

![](img/p150a.jpg)

这次，我将使用 `us-east1-b` 区域来创建我的 VM。在 AWS 部分，我们创建了 `t3.micro` 大小的实例。在 Google 上，我们有对应的，但名称不同：

![](img/p150b.jpg)

有很多你可以使用的机器系列类型。不同系列之间的区别在于你使用 VM 的目的。`E2` 家族是为通用型虚拟机制作的。因此，我将只使用它，最小尺寸是 micro，对应于 2 个 CPU 和 1 GB 内存。

### 创建实例

有时，在创建 VM 时仅设置镜像名称可能会导致错误。为了避免出现这种情况，你可以直接放置镜像链接，如下：

```
PS C:\Users\1511 MXTI> gcloud compute images list –uri
```

`https://www.googleapis.com/compute/v1/projects/centos-cloud/global/images/centos-6-v20200402`

`https://www.googleapis.com/compute/v1/projects/centos-cloud/global/images/centos-7-v20200420`

`https://www.googleapis.com/compute/v1/projects/ubuntu-os-cloud/global/images/ubuntu-1804-bionic-v20200414 https://www.googleapis.com/compute/v1/projects/coreos-cloud/global/images/coreos-alpha-2430-0-0-v20200229`

因此，镜像链接如下：

`https://www.googleapis.com/compute/v1/projects/ubuntu-os-cloud/global/images/ubuntu-1804-bionic-v20200414`

要创建你的 VM，运行以下命令：

```
PS C:\Users\1511 MXTI> gcloud compute instances create vm1 --zone=us-east1-b --machine-type=e2-micro --image=https://www.googleapis.com/compute/v1/projects/ubuntu-os-cloud/global/images/ubuntu-1804-bionic-v20200414
```

`Created [https://www.googleapis.com/compute/v1/projects/chapter7-20200423/zones/us-east1-b/instances/vm1].`

![](img/p151.jpg)

该 VM 现在正在运行，外部 IP 为 `25.229.97.23`。你可以用它连接到你的机器。然而，Google Cloud Shell 有特定的命令为你创建 SSH 密钥并自动登录实例：

```
PS C:\Users\1511 MXTI> gcloud compute ssh vm1
```



`WARNING: The PuTTY PPK SSH key file for gcloud does not exist.`
`WARNING: The public SSH key file for gcloud does not exist.`
`WARNING: The private SSH key file for gcloud does not exist.`
`WARNING: you do not have an SSH key for gcloud.`
`WARNING: SSH keygen will be executed to generate a key.`
`WARNING: Invalid characters in local username [1511 MXTI]. Using username corresponding to active account: [alisson_copyleft]`
`No zone specified. Using zone [us-east1-b] for instance: [vm1].`
`Updating project ssh metadata…Updated [https://www.googleapis.com/compute/v1/projects/chapter7-20200423].`
`Updating project ssh metadata…done.`
`Waiting for SSH key to propagate.`
`The server's host key is not cached in the registry. You have no guarantee that the server is the computer you think it is.`
`The server's ssh-ed25519 key fingerprint is:`
`ssh-ed25519 255 9c:f6:6d:58:38:8e:d7:c4:df:63:28:8b:b4:c8:53:24`
`If you trust this host, enter "y" to add the key to PuTTY's cache and carry on connecting.`
`If you want to carry on connecting just once, without adding the key to the cache, enter "n".`
`If you do not trust this host, press Return to abandon the connection.`
`Store key in cache? (y/n)`

之前，你已经有了所有的输出。为了向你展示它是如何工作的，一旦命令完成，将为你打开一个终端，你已经登录了 VM 内部：

![](img/Figure-7.10.jpg)

**图 7.10**

如果你在学习完所有步骤后想删除实例，你需要运行以下命令：

```
PS C:\Users\1511 MXTI> gcloud compute instances delete vm1
```

`No zone specified. Using zone [us-east1-b] for instance: [vm1].`
`The following instances will be deleted. Any attached disks configured to be auto-deleted will be deleted unless they are attached to any other instances or the '--keep-disks' flag is given and specifies them for keeping. Deleting a disk is irreversible and any data on the disk will be lost.`
`- [vm1] in [us-east1-b]`
`Do you want to continue (Y/n)?`

目前，这些足够让你在 GCP 上开始你的基础设施了。

### 使用 Azure 进行配置

正如我们对其他云服务商做的那样，我们将在 Azure 上做同样的事情。以相同的方式提供相同的基础是为了向你展示过程，并让你在选择偏好的平台时感到自在。

### 安装 Azure CLI

第一步是通过以下链接安装 Azure 命令行：

[`docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?view=azure-cli-latest`](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?view=azure-cli-latest)

安装过程与所有 MSI 包完全相同。双击，点击 `Next`、`Next`，然后 `Finish`。安装完成后，你可以运行以下命令检查它是否正常工作：

```
PS C:\Users\1511 MXTI> az --version
```

![](img/p153.jpg)

`Python location 'C:\Program Files (x86)\Microsoft SDKs\Azure\CLI2\python.exe'`
`Extensions directory 'C:\Users\1511 MXTI\.azure\cliextensions'`
`Python (Windows) 3.6.6 (v3.6.6:4cf1f54eb7, Jun 27 2018, 02:47:15) [MSC v.1900 32 bit (Intel)]`

现在，Azure CLI 已成功安装。首先，运行以下命令：

```
PS C:\Users\1511 MXTI> az login
```

`You have logged in. Now let us find all the subscriptions to which you have access…`

```
[
  {
    "cloudName": "AzureCloud",
    "isDefault": true,
    "managedByTenants": [],
    "name": "Pay-As-You-Go",
    "state": "Enabled",
    "user": {
      "name": "alisson_copyleft@gmail.com",
      "type": "user"
    }
  }
]
```

`az login` 命令用你的账户验证命令行身份。

与 Google 类似，我们创建一个项目来分离服务，我们在 Azure 上也将做同样的事，但不是创建项目，而是创建 `ResourceGroups`。

但在创建 `ResourceGroup` 之前，我们需要知道将使用哪个位置。要查看可用位置，请运行：

```
PS C:\Users\1511 MXTI> az account list-locations
```

```
[
  {
    "displayName": "Central US",
    "id": "/subscriptions/55465d5a-355d-43d1-85ce-9e518c81c0c/locations/centralus",
    "latitude": "41.5908",
    "longitude": "-93.6208",
    "name": "centralus",
    "subscriptionId": null
  },
  {
    "displayName": "East US",
    "id": "/subscriptions/55465d5a-355d-43d1-85ce-9e518c81c0c/locations/eastus",
    "latitude": "37.3719",
    "longitude": "-79.8164",
    "name": "eastus",
    "subscriptionId": null
  }
]
```

该命令将显示所有可用位置。在我的案例中，我将使用 East US。现在，我们可以通过命令创建 `ResourceGroup`：

```
PS C:\Users\1511 MXTI> az group create --location eastus --name book
```

```
{
  "id": "/subscriptions/55465d5a-355d-43d1-85ce-9e518c81c0c/resourceGroups/book",
  "location": "eastus",
  "managedBy": null,
  "name": "book",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
```

现在，我们已经创建了一个命名为 `book` 的资源组，并在其中我们将创建实例所需的所有资源。一个有趣的一点是，当你删除资源组时，其底层的所有内容都将被删除：

```
PS C:\Users\1511 MXTI> az vm image list
```

`你正在查看离线镜像列表，使用 --all 获取最新列表`

```json
[
  {
    "offer": "openSUSE-Leap",
    "publisher": "SUSE",
    "sku": "42.3",
    "urn": "SUSE:openSUSE-Leap:42.3:latest",
    "urnAlias": "openSUSE-Leap",
    "version": "latest"
  },
  {
    "offer": "UbuntuServer",
    "publisher": "Canonical",
    "sku": "18.04-LTS",
    "urn": "Canonical:UbuntuServer:18.04-LTS:latest",
    "urnAlias": "UbuntuLTS",
    "version": "latest"
  }
]
```

前面的命令将向你显示用于创建虚拟机的镜像。如既往，我们将选择 `UbuntuServer`。因此，你可以通过运行以下命令创建虚拟机：

```
PS C:\Users\1511 MXTI> az vm create -n vm1 -g book --image Canonical:UbuntuServer:18.04-LTS:latest --admin-username ubuntu
```

```json
{
  "fqdns": "",
  "id": "/subscriptions/55465d5a-355d-43d1-85ce-9e518c812c0c/resourceGroups/book/providers/Microsoft.Compute/virtualMachines/vm1",
  "location": "eastus",
  "macAddress": "00-0D-3A-9A-DF-E9",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.224.120.36",
  "resourceGroup": "book",
  "zones": ""
}
```

对于镜像名称，我们通常引用 `URN`（统一资源名称，Uniform Resource Name），它是镜像的标识。参数 `--admin-username` 是将具有权限运行 `sudo` 并执行管理任务的用户。

Azure 命令行足够智能获取你的默认 SSH 密钥并将其添加到虚拟机中。因此，要连接，你只需要运行默认 SSH 命令并登录：

```
PS C:\Users\1511 MXTI> ssh ubuntu@52.224.120.36
```

`主机 '52.224.120.36 (52.224.120.36)' 的真实性无法确认。`
`ECDSA 密钥指纹是 SHA256:F/Tb2nXVw4B3aertXLsde0wUTzNkBzu+aOwFHEFpl/A.`
`你确定要继续连接吗 (yes/no)? yes`



现在，我们已经创建了一个命名为`book`的资源组，并在其中我们将创建实例所需的所有资源。一个有趣的点是，当你删除资源组时，其底层的所有内容都将被删除：

```bash
PS C:\Users\1511 MXTI> az vm image list
```

你正在查看离线镜像列表，使用`--all`获取最新列表：

```json
[
  {
    "offer": "openSUSE-Leap",
    "publisher": "SUSE",
    "sku": "42.3",
    "urn": "SUSE:openSUSE-Leap:42.3:latest",
    "urnAlias": "openSUSE-Leap",
    "version": "latest"
  },
  {
    "offer": "UbuntuServer",
    "publisher": "Canonical",
    "sku": "18.04-LTS",
    "urn": "Canonical:UbuntuServer:18.04-LTS:latest",
    "urnAlias": "UbuntuLTS",
    "version": "latest"
  }
]
```

前面的命令将向你显示用于创建虚拟机的镜像。如既往，我们将选择`UbuntuServer`。因此，你可以通过运行以下命令创建虚拟机：

```bash
PS C:\Users\1511 MXTI> az vm create -n vm1 -g book --image Canonical:UbuntuServer:18.04-LTS:latest --admin-username ubuntu
```

```json
{
  "fqdns": "",
  "id": "/subscriptions/55465d5a-355d-43d1-85ce-9e518c812c0c/resourceGroups/book/providers/Microsoft.Compute/virtualMachines/vm1",
  "location": "eastus",
  "macAddress": "00-0D-3A-9A-DF-E9",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.224.120.36",
  "resourceGroup": "book",
  "zones": ""
}
```

对于镜像名称，我们通常引用`URN`（统一资源名称，Uniform Resource Name），它是镜像的标识。参数`--admin-username`是将具有权限运行`sudo`并执行管理任务的用户。

Azure 命令行足够智能获取你的默认 SSH 密钥并将其添加到虚拟机中。因此，要连接，你只需要运行默认 SSH 命令并登录：

```bash
PS C:\Users\1511 MXTI> ssh ubuntu@52.224.120.36
```

主机`'52.224.120.36 (52.224.120.36)'`的真实性无法确认。  
ECDSA 密钥指纹是`SHA256:F/Tb2nXVw4B3aertXLsde0wUTzNkBzu+aOwFHEFpl/A`。  
你确定要继续连接吗 (yes/no)? yes



现在，我们已经创建了一个命名为`book`的资源组，并在其中我们将创建实例所需的所有资源。一个有趣的一点是，当你删除资源组时，其底层的所有内容都将被删除：

```bash
PS C:\Users\1511 MXTI> az vm image list
```

`你正在查看离线镜像列表，使用 --all 获取最新列表`

```json
[
  {
    "offer": "openSUSE-Leap",
    "publisher": "SUSE",
    "sku": "42.3",
    "urn": "SUSE:openSUSE-Leap:42.3:latest",
    "urnAlias": "openSUSE-Leap",
    "version": "latest"
  },
  {
    "offer": "UbuntuServer",
    "publisher": "Canonical",
    "sku": "18.04-LTS",
    "urn": "Canonical:UbuntuServer:18.04-LTS:latest",
    "urnAlias": "UbuntuLTS",
    "version": "latest"
  }
]
```

前面的命令将向你显示用于创建虚拟机的镜像。如既往，我们将选择`UbuntuServer`。因此，你可以通过运行以下命令创建虚拟机：

```bash
PS C:\Users\1511 MXTI> az vm create -n vm1 -g book --image Canonical:UbuntuServer:18.04-LTS:latest --admin-username ubuntu
```

```json
{
  "fqdns": "",
  "id": "/subscriptions/55465d5a-355d-43d1-85ce-9e518c812c0c/resourceGroups/book/providers/Microsoft.Compute/virtualMachines/vm1",
  "location": "eastus",
  "macAddress": "00-0D-3A-9A-DF-E9",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.224.120.36",
  "resourceGroup": "book",
  "zones": ""
}
```

对于镜像名称，我们通常引用`URN`（统一资源名称，Uniform Resource Name），它是镜像的标识。参数`--admin-username`是将具有权限运行`sudo`并执行管理任务的用户。

Azure 命令行足够智能获取你的默认 SSH 密钥并将其添加到虚拟机中。因此，要连接，你只需要运行默认 SSH 命令并登录：

```bash
PS C:\Users\1511 MXTI> ssh ubuntu@52.224.120.36
```

`主机 '52.224.120.36 (52.224.120.36)' 的真实性无法确认。`
`ECDSA 密钥指纹是 SHA256:F/Tb2nXVw4B3aertXLsde0wUTzNkBzu+aOwFHEFpl/A.`
`你确定要继续连接吗 (yes/no)? yes`

现在，我们可以使用云提供商创建文件并构建第一个虚拟机（VM）。我将首先使用`GCP`，这是我个人项目使用的云提供商。然后，第一步是创建一个用于存储代码的文件夹。

![](img/p161.jpg)

当然，将代码拆分为多个文件是最佳实践，因为这使得代码具有可复性且易于管理。但在这里，我们只创建一个虚拟机来学习 Terraform 语法并理解它的工作原理。因此，我将所有内容都写在一个单文件中。

## 设置服务账户 (Service Account)

首先，我们需要创建一个服务账户，它相当于用户名和密码，用于代表我创建资源。访问 Google Cloud 控制台 (`https://console.cloud.google.com/`)，进入`IAM & Admin`，并在`Create service account`中创建一个名为`terraform`的账户，如下截图所示：

![](img/Figure-8.1.jpg)

**图 8.1**

点击`Create`，然后选择`Role Compute Admin`。此角色将允许服务账户管理与 Compute Engine 相关的所有资源，这对应于我们的虚拟机。

然后，你必须按照如下所示创建一个 JSON 格式的密钥：

![](img/Figure-8.2.jpg)

**图 8.2**

现在，你已经配置好了服务账户并可以供 Terraform 使用。复制 JSON 文件，并将其放入创建 Terraform 代码的同一个文件夹中。在我们创建的文件夹中，创建一个名为`infrastructure.tf`的新文件，内容如下：

```terraform
provider "google" {
  credentials = file("terraform_sa.json")
  project     = "alisson-187813"
  region      = "us-east1"
}
```

这段代码对于 Terraform 是必须的。在这个文件中，你将使用 Google provider。Provider 是为了在你的 Terraform 代码与你想交互的平台之间建立接口而创建模块。例如，我曾遇到过需要在 Linux 上管理 DNS 服务器（Bind9）的情况。当使用 Terraform 执行的方法是使用`TSIG`协议时，我必须导入 DNS provider。在 Azure 的情况下，我导入了`AzureRM` provider。如果你想了解更多信息，我的个人博客上有两篇文章。

使用 Azure 和 Terraform：[`alissonmachado.com.br/terraform-azure-criando-uma-infraestrutura-basica/`](http://alissonmachado.com.br/terraform-azure-criando-uma-infraestrutura-basica/)

使用 Terraform 和 TSIG 管理 DNS：[`alissonmachado.com.br/terraform-gerenciando-dns-com-tsig/`](http://alissonmachado.com.br/terraform-gerenciando-dns-com-tsig/)

## 初始化 Terraform

回到代码部分，provider 并不随 Terraform 默认提供。你需要下载它们。你可以使用以下命令完成：

```cmd
C:\Users\1511 MXTI\ProductionInfrastructure> terraform init
```

```text
Initializing the backend…

Initializing provider plugins…

- Checking for available provider plugins…

- Downloading plugin for provider "google" (hashicorp/google) 3.20.0…

The following providers do not have any version constraints in configuration, so the latest version was installed. 防止自动升级到可能包含破坏性更改的新主版本，建议在配置中相应的 provider 块中添加 version = "…" 约束，使用下方建议的约束字符串。

* provider.google: version = "~> 3.20"

Terraform has been successfully initialized!
```



你现在可以开始使用 Terraform 了。尝试运行`terraform plan`来查看你的基础设施所需的任何更改。现在所有的 Terraform 命令都应该可以工作。

如果你设置或更改了 Terraform 的模块或后端（`backend`）配置，请重新运行此命令重新初始化工作目录。如果你忘记了，其他命令会检测到并在必要时提醒你这样做。

## 创建基础设施

现在你能够创建基础设施了，因为你已经在本地机器上安装了 provider。因此，包含以下代码来创建我们的第一个实例：

```terraform
provider "google" {
  credentials = file("terraform_sa.json")
  project     = "alisson-187813"
  region      = "us-east1"
}

resource "google_compute_instance" "chapter8" {
  name         = "chapter8-instance"
  machine_type = "g1-small"
  zone         = "us-east1-b"

  boot_disk {
    initialize_params {
      image = "ubuntu-1804-bionic-v20200414"
    }
  }

  network_interface {
    network = "default"
    access_config {
    }
  }
}
```

在前面的代码中，我们定义将使用一个名为`google_compute_instance`的资源，正如我们在上一章中所做的，它对应于虚拟机。但现在，我们使用 Terraform 来。该实例将使用`us-east1-b`区域的 Ubuntu 1804 镜像以及其他细节（如网络配置）。我们将使用 Google 设置的默认值。

使用 Terraform 创建新代码时，第一件事是运行以下命令：

```powershell
PS C:\Users\1511 MXTI\ProductionInfrastructure> terraform plan
```

```text
Refreshing Terraform state in-memory prior to plan…

刷新后的状态将用于用于计算此计划，但不会被持久化到本地或远程状态存储中。

------------------------------------------------------------------------

已生成执行计划，并如下所示。

资源操作将用以下符号表示：

+ create

Terraform will perform the following actions:

# google_compute_instance.chapter8 will be created

+ resource "google_compute_instance" "chapter8" {
+ can_ip_forward           = false
+ cpu_platform             = (known after apply)
+ current_status           = (known after apply)
+ deletion_protection      = false
+ guest_accelerator        = (known after apply)
+ id                       = (known after apply)
+ instance_id              = (known after apply)
+ label_fingerprint        = (known after apply)
+ machine_type             = "g1-small"
+ metadata_fingerprint     = (known after apply)
+ min_cpu_platform         = (known after apply)
+ name                     = "chapter8-instance"
+ project                  = (known after apply)
+ self_link                = (known after apply)
+ tags_fingerprint         = (known after apply)
+ zone                     = "us-east1-b"

+ boot_disk {
+ auto_delete               = true
+ device_name               = (known after apply)
+ disk_encryption_key_sha256 = (known after apply)
+ kms_key_self_link         = (known after apply)
+ mode                      = "READ_WRITE"
+ source                    = (known after apply)

+ initialize_params {
+ image  = "ubuntu/1804-lts"
+ labels = (known after apply)
+ size   = (known after apply)
+ type   = (known after apply)
  }
}

+ network_interface {
+ name               = (known after apply)
+ network            = "default"
+ network_ip         = (known after apply)
+ subnetwork         = (known after apply)
+ subnetwork_project = (known after apply)

+ access_config {
+ nat_ip          = (known after apply)
+ network_tier    = (known after apply)
  }
}

+ scheduling {
+ automatic_restart   = (known after apply)
+ on_host_maintenance = (known after apply)
+ preemptible         = (known after apply)

+ node_affinities {
+ key      = (known after apply)
+ operator = (known after apply)
+ values   = (known after apply)
  }
}
}

Plan: 1 to add, 0 to change, 0 to destroy.

------------------------------------------------------------------------

注意: 你没有指定一个 "-out" 参数来保存此计划，因此当随后运行 "terraform apply" 时，Terraform 无法保证将恰好执行这些操作。
```

`terraform plan` 命令将检查你在 Google 上的项目，并通过差异显示你的代码与 Google 上的项目之间的不同之处。在这种情况下，我们可以看到设置的所有内容都将被创建，因为行前面有加号信号（`+`）。如果某些资源将被删除，你将看到减号（`-`）。此外，在最后一行，你将看到如下：

`Plan: 1 to add, 0 to change, 0 to destroy.`

然后你就会松了一口气，没有任何东西会被删除。Terraform 是一个非常强大的工具，但在运行命令之前你需要小心，否则你可能会用它销毁所有的基础设施。关于这一点有一句名言：

如果你想以自动化的方式在所有的生产服务器上犯错，那就是 DevOps！继续我们的基础设施操作，既然我们确定没有东西会被删除，就可以运行创建实例的`apply`命令了：

```bash
PS C:\Users\1511 MXTI\ProductionInfrastructure> terraform apply
```

```text
已生成执行计划并显示如下。

资源操作由以下符号表示：

+ create

Terraform 将执行以下操作：

# google_compute_instance.chapter8 将被创建

+ resource "google_compute_instance" "chapter8" {
+ can_ip_forward       = false
+ cpu_platform         = (known after apply)
+ current_status       = (known after apply)
+ deletion_protection  = false
+ guest_accelerator    = (known after apply)
+ id                   = (known after apply)
+ instance_id          = (known after apply)
+ label_fingerprint    = (known after apply)
+ machine_type         = "g1-small"
+ metadata_fingerprint = (known after apply)
+ min_cpu_platform     = (known after apply)
+ name                 = "chapter8-instance"
+ project              = (known after apply)
+ self_link            = (known after apply)
+ tags_fingerprint     = (known after apply)
+ zone                 = "us-east1-b"

+ boot_disk {
+ auto_delete           = true
+ device_name           = (known after apply)
+ disk_encryption_key_sha256 = (known after apply)
+ kms_key_self_link     = (known after apply)
+ mode                  = "READ_WRITE"
+ source                = (known after apply)

+ initialize_params {
+ image  = "ubuntu-1804-bionic-v20200414"
+ labels = (known after apply)
+ size   = (known after apply)
+ type   = (known after apply)
  }
}

+ network_interface {
+ name               = (known after apply)
+ network            = "default"
+ network_ip         = (known after apply)
+ subnetwork         = (known after apply)
+ subnetwork_project = (known after apply)

+ access_config {
+ nat_ip          = (known after apply)
+ network_tier    = (known after apply)
  }
}

+ scheduling {
+ automatic_restart   = (known after apply)
+ on_host_maintenance = (known after apply)
+ preemptible         = (known after apply)

+ node_affinities {
+ key       = (known after apply)
+ operator  = (known after apply)
+ values    = (known after apply)
  }
}
}

Plan: 1 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?

Terraform 将执行上述操作。

只有输入 'yes' 才能被接受执行。

Enter a value: yes

google_compute_instance.chapter8: Creating…
google_compute_instance.chapter8: Still creating… [10s elapsed]
google_compute_instance.chapter8: Creation complete after 14s [id=projects/alisson-187813/zones/us-east1-b/instances/chapter8-instance]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```

如你所见，当你运行`apply`命令时，`plan`命令已经执行过了。为了确保你了解基础设施中将发生的变化，你需要输入`yes`，然后实例就会被创建。

实例已成功创建，但我们没有关于用于连接到实例的公 IP 地址的信息。要获取这些信息，我们需要使用名为`output`的 Terraform 语句。这需要在当前代码的末尾包含此部分：

```hcl
output "name" {
  value = google_compute_instance.chapter8.name
}

output "size" {
  value = google_compute_instance.chapter8.machine_type
}

output "public_ip" {
  value = google_compute_instance.chapter8.network_interface[0].access_ip
}
```

```hcl
network_interface {
  network       = "default"
  access_config {
  }
}

metadata = {
  sshKeys = join("",["alisson:",file("id_rsa.pub")])
}

output "name" {
  value = google_compute_instance.chapter8.name
}

output "size" {
  value = google_compute_instance.chapter8.machine_type
}

output "public_ip" {
  value = google_compute_instance.chapter8.network_interface[0].access_config[0].nat_ip
}
```

只要我们不断在代码中包含更多内容，Terraform 就会变得越来越有趣。让我们运行`terraform plan`来查看新的更改：



在 PowerShell 中执行`terraform plan`命令，进入`C:\Users\1511 MXTI\ProductionInfrastructure`目录后，Terraform 会在内存中刷新状态，生成执行计划。以下是`terraform plan`的输出结果：

```bash
PS C:\Users\1511 MXTI\ProductionInfrastructure> terraform plan
Refreshing Terraform state in-memory prior to plan…
The refreshed state will be used to calculate this plan, but will not be persisted to local or remote state storage.
google_compute_instance.chapter8: Refreshing state… [id=projects/alisson-187813/zones/us-east1-b/instances/chapter8-instance]
------------------------------------------------------------------------
An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
~ update in-place
Terraform will perform the following actions:
# google_compute_instance.chapter8 will be updated in-place
resource "google_compute_instance" "chapter8" {
  can_ip_forward       = false
  cpu_platform         = "Intel Haswell"
  current_status      = "RUNNING"
  deletion_protection  = false
  enable_display       = false
  guest_accelerator    = []
  id                  = "projects/alisson-187813/zones/us-east1-b/instances/chapter8-instance"
  instance_id         = "9170008912891805003"
  label_fingerprint    = "42WmSpB8rSM="
  labels               = {}
  machine_type        = "g1-small"
  ~ metadata           = {
  + "sshKeys" = <<~EOT
alisson:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQChi8HX26xv9Rk9gz47Qhb+Tu7MRqGIyPxnheIeEg Fad/dlqG4w4pY7y5dtx5LNGE9C01varco5dZagqsHplI7M+5ECSvjAuS6b5rkYZwZiZru DXxckcQHFpr2yIz3DOzKRTUc5Hg5JHF5aymiqyVfTsxL/aI/LDY8Ikh+INn3S9+b5 bZtU+74tA6y uqth5SCtNSWwMUlv7QL6ONHtQiviAjBe+ksDBBV6thWz2ZIJA/jApSIBJWK9AWmZwq2hFy9sOZArUDB2Kt 6kl3rIZnHpqJ/GMUCxFhtggYamJ5J2H62 77qLFqLZ/8tum9uc5l/lSWYKTDm2+E/prQfmFrxPf9 alisson
EOT
  }
  metadata_fingerprint = "bxkbv_NPHas="
  name                = "chapter8-instance"
  project             = "alisson-187813"
  resource_policies   = []
  self_link           = "https://www.googleapis.com/compute/v1/projects/alisson-187813/zones/us-east1-b/instances/chapter8-instance"
  tags                = []
  tags_fingerprint    = "42WmSpB8rSM="
  zone                = "us-east1-b"
  boot_disk {
    auto_delete = true
    device_name = "persistent-disk-0"
    mode        = "READ_WRITE"
    source  = "https://www.googleapis.com/compute/v1/projects/alisson-187813/zones/us-east1-b/disks/chapter8-instance"
    initialize_params {
      image  = "https://www.googleapis.com/compute/v1/projects/ubuntu-os-cloud/global/images/ubuntu-1804-bionic-v202014"
      labels = {}
      size  = 10
      type  = "pd-standard"
    }
  }
  network_interface {
    name        = "nic0"
    network     = "https://www.googleapis.com/compute/v1/projects/alisson-187813/global/networks/default"
    network_ip  = "10.42.0.3"
    subnetwork  = "https://www.googleapis.com/compute/v1/projects/alisson-187813/regions/us-east1/subnetworks/default"
    subnetwork_project = "alisson-187813"
    access_config {
      nat_ip      = "10.196.24.22"
      network_tier = "PREMIUM"
    }
  }
  scheduling {
    automatic_restart  = true
    on_host_maintenance = "MRATE"
    preemptible        = false
  }
  shielded_instance_config {
    enable_integrity_monitoring = true
    enable_secure_boot           = false
    enable_vtpm                 = true
  }
}
Plan: 0 to add, 1 to change, 0 to destroy.
```

由于没有指定`-out`参数来保存计划，Terraform 在执行`terraform apply`时无法保证执行这些操作。当有一个现有资源并想要修改它时，`metadata`字段增加了。计划为：0 个添加，1 个更改，0 个删除。因此，我们可以运行`terraform apply`：

```bash
PS C:\Users\1511 MXTI\ProductionInfrastructure> terraform apply

google_compute_instance.chapter8: Refreshing state… [id=projects/alisson-187813/zones/us-east1-b/instances/chapter8]

An execution plan has been generated and is shown below.

Resource actions are indicated with the following symbols:

~ update in-place

Terraform will perform the following actions:

# google_compute_instance.chapter8 will be updated in-place

resource "google_compute_instance" "chapter8" {

  can_ip_forward       = false

  cpu_platform         = "Intel Haswell"

  current_status      = "RUNNING"

  deletion_protection  = false

  enable_display       = false

  guest_accelerator    = []

  id                  = "projects/alisson-187813/zones/us-east1-b/instances/chapter8"

  instance_id         = "9170008912891805003"

  label_fingerprint    = "42WmSpB8rSM="

  labels               = {}

  machine_type        = "g1-small"

  ~ metadata           = {

  + "sshKeys" = <<~EOT

alisson:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQChi8HX26xv9Rk9gz47Qhb+Tu7MRqGIyPxnheIeEg Fad/dlqG4w4pY7y5dtx5LNGE9C01varco5dZagqsHplI7M+5ECSvjAuS6b5rkYZwZiZru DXxckcQHFpr2yIz3DOzKRTUc5Hg5JHF5aymiqyVfTsxL/aI/LDY8Ikh+INn3S9+b5 bZtU+74tA6y uqth5SCtNSWwMUlv7QL6ONHtQiviAjBe+ksDBBV6thWz2ZIJA/jApSIBJWK9AWmZwq2hFy9sOZArUDB2Kt 6kl3rIZnHpqJ/GMUCxFhtggYamJ5J2H62 77qLFqLZ/8tum9uc5l/lSWYKTDm2+E/prQfmFrxPf9 alisson

EOT

  }

  metadata_fingerprint = "bxkbv_NPHas="

  name                = "chapter8-instance"

  project             = "alisson-187813"

  resource_policies   = []

  self_link           = "https://www.googleapis.com/compute/v1/projects/alisson-187813/zones/us-east1-b/instances/chapter8-instance"

  tags                = []

  tags_fingerprint    = "42WmSpB8rSM="

  zone                = "us-east1-b"

  boot_disk {

    auto_delete = true

    device_name = "persistent-disk-0"

    mode        = "READ_WRITE"

    source  = "https://www.googleapis.com/compute/v1/projects/alisson-187813/zones/us-east1-b/disks/chapter8-instance"

    initialize_params {

      image  = "https://www.googleapis.com/compute/v1/projects/ubuntu-os-cloud/global/images/ubuntu-1804-bionic-v202014"

      labels = {}

      size  = 10

      type  = "pd-standard"

    }

  }

  network_interface {

    name        = "nic0"

    network     = "https://www.googleapis.com/compute/v1/projects/alisson-187813/global/networks/default"

    network_ip  = "10.42.0.3"

    subnetwork  = "https://www.googleapis.com/compute/v1/projects/alisson-187813/regions/us-east1/subnetworks/default"

    subnetwork_project = "alisson-187813"

    access_config {

      nat_ip      = "10.196.24.22"

      network_tier = "PREMIUM"

    }

  }

  scheduling {

    automatic_restart  = true

    on_host_maintenance = "MRATE"

    preemptible        = false

  }

  shielded_instance_config {

    enable_integrity_monitoring = true

    enable_secure_boot           = false

    enable_vtpm                 = true

  }

}

Plan: 0 to add, 1 to change, 0 to destroy.

Do you want to perform these actions?

Terraform will perform the actions described above.

Only 'yes' will be accepted to approve.

Enter a value: yes

google_compute_instance.chapter8: Modifying… [id=projects/alisson-187813/zones/us-east1-b/instances/chapter8-instance, 10s elapsed]
```

应用完成后，输出如下：
`google_compute_instance.chapter8: Modifications complete after 13s [id=projects/alisson-187813/zones/us-east1-b/instances/chapter8-instance]`
`Apply complete! Resources: 0 added, 1 changed, 0 destroyed.`

### 输出结果：
- `name = chapter8-instance`
- `public_ip = 104.196.24.122`
- `size = g1-small`

更改已成功应用，现在我们可以测试访问是否正常工作：

```bash
PS C:\Users\1511 MXTI\ProductionInfrastructure>ssh alisson@104.196.24.122
```

登录后显示系统信息：
欢迎来到 Ubuntu 18.04.4 LTS (GNU/Linux 5.0.0-1034-gcp x86_64)
- 文档：https://help.ubuntu.com
- 管理：https://landscape.canonical.com
- 支持：https://ubuntu.com/advantage

系统信息（更新至 UTC 2020 年 5 月 11 日 13:21:39）：
- 系统负载：0.0
- 进程：94
- `/`使用率：9.52GB 的 12.8%
- 登录用户：0
- 内存使用率：13%
- `ens4`的 IP 地址：10.142.0.3
- 交换空间使用率：0%

> Ubuntu 20.04 LTS 已发布，提升了 Intel, AMD, Nvidia, ARM64, Z15 以及 AWS, Azure 和 Google Cloud 的性能、安全性和优化标准。
> https://ubuntu.com/blog/ubuntu-20-04-lts-arrives

有 0 个软件包可以更新，0 个更新安全更新。Ubuntu 系统包含的程序是自由软件；每个程序的具体分发条款在`/usr/share/doc/*/copyright`的单独文件中说明。在适用法律允许范围内，Ubuntu **绝对不提供任何保证**。

```bash
alisson@chapter8-instance:~$
```

运行成功！太完美了！我们创建了一切，仅仅管理了几行代码，现在我们就有了一个运行中的实例，只需访问控制台来创建服务帐户。作为最后一步，我想我们可以使用`terraform destroy`命令销毁一切，并看看它是如何工作的：

```bash
PS C:\Users\1511 MXTI\ProductionInfrastructure>terraform destroy
```



`google_compute_instance.chapter8`: Refreshing state… [id=projects/alisson-187813/zones/us-east1-b/instances/chapter8-instance]

已生成执行计划并显示如下。

资源操作用以下符号表示：

- 销

Terraform 将执行以下操作：

```
# google_compute_instance.chapter8 将被销毁

- resource "google_compute_instance" "chapter8" {

- can_ip_forward       = false -> null

- cpu_platform         = "Intel Haswell" -> null

- current_status      = "RUNNING" -> null

- deletion_protection  = false -> null

- enable_display       = false -> null

- guest_accelerator   = [] -> null

- id                   = "projects/alisson-187813/zones/us-east1-b/instances/chapter8-instance" -> null

- instance_id          = "9170008912891805003" -> null

- label_fingerprint    = "42WmSpB8rSM=" -> null

- labels               = {} -> null

- machine_type         = "g1-small" -> null

- metadata             = {

- "sshKeys" = <<~EOT

alisson:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQChi8HX2 6xv9Rk9gz47Qhb+Tu7MRqGIyPxnheIeEgFad/dlqG4w4p Y7y5dtx 5LNGE9C01varco5dZagqsHplI7M +5ECSvjAuS6b5rkYZwZiZruDXxckcQHFpr2yIz3DOzKRTUc5Hg5JHF5aymiqyVfTsxL/aI/LDY8Ikh+INn3S9+b5bZtU+74tA6yuqth5SCtNSWwMUlv7QL6ONHtQiviAj Be+ksDBBV6thWz2ZIJA/jApSIBJWK9AWmZwq2hFy9sOZArUDB2Kt6kl3rIZnHpqJ /GMUCxFhtggYamJ5J2H6277qLFqLZ/8tum9uc5l/lSWYKTDm2+E/prQfmFrxPf9 alisson

EOT

} -> null

- metadata_fingerprint = "lZHcUBfXG-4=" -> null

- name                 = "chapter8-instance" -> null

- project              = "alisson-187813" -> null

- resource_policies    = [] -> null

- self_link           = "https://www.googleapis.com/compute/v1/projects/alisson-187813/zones/us-east1-b/instances/chapter8-instance" -> null

- tags                 = {} -> null

- tags_fingerprint     = "42WmSpB8rSM=" -> null

- zone                 = "us-east1-b" -> null

- boot_disk {

- auto_delete          = false -> null

- device_name          = "0" -> null

- mode                  = "READ" -> null

- source_instance      = "projects/alisson-187813/zones/us-east1-b/instances/chapter8-instance" -> null

- type                  = "DISK" -> null

}

- initialize_disk {

- auto_delete          = false -> null

- image                = "https://www.googleapis.com/compute/v1/projects/global/images/family/ubuntu-1804-" -> null

- mode                  = "READ" -> null

}

- network_interface {

- network_config {

- access_configs {

- name                 = "ONE_TO_NAT"

}

}

- network              = "default" -> null

}

- scheduling {

- auto_delete          = false -> null

- preemptible          = false -> null

- on_host              = "MIG" -> null

}

}
```

太棒了！现在我们的 GCP 账户中没有其他产生费用的项目，如果你想重新创建基础设施，只需运行`terraform apply`命令即可。但是，使用这个名称，你将一次性获得包含 IP 地址和已配置 SSH 密钥的输出。如果你想创建更多实例，只需更改实例名称并复制粘贴代码。所有实例可以使用相同的 SSH 密钥。

## 结论

这一章向我们不需要学习所有云服务提供者的命令行，甚至不需要为每一个都安装 SDK。通过 Terraform，我们能够使用 Terraform 语法对基础设施建模，更改提供程序（providers）来实现不同的集成，并查看哪些内容将被更改、创建或删除。我强烈建议你探索与 Azure、AWS、Digital Ocean 集成的其他提供程序，并尝试其他与云平台不相关的提供程序，它们也可以帮助你提供基础设施，例如 DNS 模块。

# 第 9 章：使用 Git

本章旨在向你介绍`Git`，这是一个帮助你处理同一份代码，并远程与同一项目的其他开发者进行协作的工具。

## 结构

在本章中，我们将讨论以下主题：

* `Git`
* `GitFlow`
* `GitHub`

## 目标

学习完本单元后，你应该能够：

* 安装并使用`Git`配合本地仓库
* 理解`GitFlow`及其如何应用于日常工作
* 使用`GitHub`与他人共享你的代码

## Git

`Git`是由 Linux 系统的创建者`Linus Torvalds`创建的工具。该工具的创建是为了帮助全球许多开发者控制他们之间的开发流程。它可以帮助解决冲突、跟踪修改，甚至撤销在旧版本中运行在新版本中失效的配置。

要安装`Git`，你可以访问以下链接：

[`git-scm.com/download/win`](https://git-scm.com/download/win)

安装过程与我们处理所有 Windows 应用程序相同；只需点击`Next`、`Next`然后`Finish`。安装完成后，你会发现一个名为`Git Bash`的新程序，它允许你创建本地仓库并使用`Git`命令创建应用程序的版本：

![](img/Figure-9.1.jpg)

**图 9.1**

在接下来的步骤中，我将向你展示一些基础命令，这些命令足够你在日常工作中使用`Git`了。当然，完全可以写一整本书来解释`Git`命令以及如何处理冲突和不同的代码版本策略。然而，让我们保持基础吧，因为“完成胜过完美”：

```
1511 MXTI@avell MINGW64 ~

$ mkdir Chapter09

1511 MXTI@avell MINGW64 ~

$ cd Chapter09/
```

如上所述，这是我的`Git Bash`的输出。创建一个名为`Chapter09`的文件夹并进入该文件夹。在这里，我将创建我的第一个仓库：

```
1511 MXTI@avell MINGW64 ~/Chapter09

$ git init

Initialized empty Git repository in C:/Users/1511 MXTI/Chapter09/.git/
```

`git init`命令负责初始化任何文件夹作为`Git`仓库。它本质上会创建一个名为`.git`的文件夹，具有预定义的文件夹结构，用于存储你代码的元数据文件，例如与当前代码版本相比发生了哪些变化、你的修改、你想将哪些文件发送到新版本等。仓库（repository）是你存储和跟踪代码修改的文件夹。

现在，我们可以使用任何文本编辑器创建一些代码并跟踪更改。我将使用 Visual Studio Code，因为我是最喜欢的。但你可以根据喜好使用任何编辑器：

![](img/Figure-9.2.jpg)

**图 9.2**

我在文本编辑器中创建了一个名为`code.txt`的新文件，仅作为带有随机内容的示例。在`Git`仓库中，我们可以跟踪任何类型的文本文件、Python 代码、C++ 代码、Java 或任何内容的修改。

下一步是检查自我创建仓库和文件以来发生了什么，Visual Studio Code 与 PowerShell 集成了，因此我将使用它来运行`Git`命令。

第一个命令是`git status`：

```
PS C:\Users\1511 MXTI\Chapter09> git status

On branch master

No commits yet

Untracked files:

(use "git add <file>…" to include in what will be committed)

code.txt

nothing added to commit but untracked files present (use "git add" to track)
```

在前面的命令中，我们可以看到我们处于`master`分支（branch），并且有一个未跟踪的文件，名为`code.txt`。分支是你对同一个项目可以拥有的版本。你可以按照你想要的方式、使用你想要的名称使用它。然而，创建一个有助于你保持组织标准的流。否则，每个项目将有一套不同的版本策略。

## GitFlow

现在，当我们开始开发一个项目时，我们有已经在生产环境的代码文件，由于 CI/CD 流水线的存在，我们不能在主分支工作。我们需要生成一个包含完整代码的新软件版本。

让我们提交代码的第一版本，将在所有参与同一项目的开发者之间共享：

```
PS C:\Users\1511 MXTI\Chapter09> git add --all

PS C:\Users\1511 MXTI\Chapter09> git commit -m "uploading the scaffold of the project"

[master (root-commit) f6284bf] uploading the scaffold of the project

1 file changed, 3 insertions(+)

create mode 100644 code.txt
```

如果我们再次运行`git status`，将没有任何未跟踪或待提交的内容：

```
PS C:\Users\1511 MXTI\Chapter09> git status

On branch master

nothing to commit, working tree clean
```

要检查你拥有的分支，运行以下命令：

```
PS C:\Users\1511 MXTI\Chapter09> git branch

* master
```

现在，我们需要在不破坏生产环境版本（对应`master`分支）的情况下对代码进行工作。然后，我们将创建一个名为`develop`的新分支，该分支对应我们软件的新版本：

```
PS C:\Users\1511 MXTI\Chapter09> git checkout -b develop

Switched to a new branch 'develop'
```

我们创建了一个新分支。现在，如果我们再次运行`git branch`命令，我们可以看到当前代码的另一个版本，我们可以在不更改当前版本任何内容的情况下修改它：

```
S C:\Users\1511 MXTI\Chapter09> git branch

* develop

master
```

我们创建了一个新分支，然后如果我们再次运行`git branch`命令，我们可以看到当前代码的另一个版本，我们可以在不更改当前版本任何内容的情况下修改它：

![](img/Figure-9.3.jpg)

**图 9.3**

在前面的图中，我在代码中添加了新行。这本书是关于基础设施的。因此，我想展示我们可以包含对应基础设施的新代码，而且我们还有开发基础设施和生产基础设施，无论哪一个拥有自己的配置和代码。

我可以再次运行`git status`命令并查看发生了什么变化：

```
PS C:\Users\1511 MXTI\Chapter09> git status

On branch develop

Changes not staged for commit:

(use "git add <file>…" to update what will be committed)

(use "git restore <file>…" to discard changes in working directory)

modified:   code.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

与第一个文件不同，`code.txt`现在是已修改的（modified），而不是我们在第一个命令中看到的未跟踪状态，这意味着它不是新文件，而是文件被修改了。如果你想检查与旧版本相比发生了哪些变化，可以使用以下命令：

`PS C:\Users\1511 MXTI\Chapter09>` `git diff code.txt`

```diff
diff --git a/code.txt b/code.txt

index 70274ce..9c5fd1c 100644

--- a/code.txt

+++ b/code.txt

@@ -1,3 +1,5 @@

Hello!

-This is my first code!

\ No newline at end of file

+This is my first code!

+

+This is the configuration respective to the VMs size.

\ No newline at end of file
```

在这里，我们可以看到两个版本之间的差异。带有 (`(+)`) 加号的地方意味着这些行被包含在文件中，而带有 (`(-)`) 减号的地方则是我们从旧版本中删除的内容。为了保存这个新版本并与其他开发者共享，我们必须在这个新版本中添加文件并提交更改：

`PS C:\Users\1511 MXTI\Chapter09>` `git add --all`

`PS C:\Users\1511 MXTI\Chapter09>` `git commit -m "adding new configurations"`

```
[develop 806990f] adding new configurations

1 file changed, 3 insertions(+), 1 deletion(-)
```

现在，假设我们已经测试了一切，并且想要将开发版本发布到生产环境。现在，我们需要将开发代码与生产代码合并。为了做到，我们可以使用以下命令：

`PS C:\Users\1511 MXTI\Chapter09>` `git checkout master`

`Switched to branch 'master'`

`PS C:\Users\1511 MXTI\Chapter09>` `git merge develop`

```diff
Updating f6284bf..806990f

Fast-forward

code.txt | 4 +++-

1 file changed, 3 insertions(+), 1 deletion(-)
```



完美！现在我们在生产环境中已经有了开发版本。因此，我们可以部署它，并在另一个版本中开始工作。但是，让我们让事情稍微复杂一点。首先，我们需要回到开发分支：

```
PS C:\Users\1511 MXTI\Chapter09> git checkout develop
Switched to branch 'develop'
```

我们可以假设想要更改基础设施的当前操作系统。假设它是基于 CentOS 的，我们想更改到 `Ubuntu`。然而，我们不能直接在开发环境中更改，因为这可能会停止开发者开发他们自己的项目。因此，我必须基于开发分支创建一个新分支，我们通常称之为 `feature` 分支。

```
PS C:\Users\1511 MXTI\Chapter09> git checkout -b feature-ubuntu
Switched to a new branch 'feature-ubuntu'
```

现在，我将编写新代码：

![](img/Figure-9.4.jpg)

**图 9.4**

在基于开发环境创建的临时环境中测试代码并确保其运行正常后，我们可以提交更改并将其合并到开发环境：

```
PS C:\Users\1511 MXTI\Chapter09> git add --all
PS C:\Users\1511 MXTI\Chapter09> git commit -m "changing the os"
```

```
[feature-ubuntu 5b4ce7a] changing the os
1 file changed, 3 insertions(+), 1 deletion(-)
```

现在，我们可以从特性分支切换到开发分支并合并代码：

```
PS C:\Users\1511 MXTI\Chapter09> git checkout develop
Switched to branch 'develop'
PS C:\Users\1511 MXTI\Chapter09> git merge feature-ubuntu
```

```
Updating 806990f..5b4ce7a
Fast-forward
code.txt | 4 +++-
1 file changed, 3 insertions(+), 1 deletion(-)
```

代码已成功合并。现在假设我们已经在开发环境中测试过，并且一切运行顺畅，现在是时候合并到生产环境了：

```
PS C:\Users\1511 MXTI\Chapter09> git checkout master
Switched to branch 'master'
PS C:\Users\1511 MXTI\Chapter09> git merge develop
```

```
Updating 806990f..5b4ce7a
Fast-forward
code.txt | 4 +++-
1 file changed, 3 insertions(+), 1 deletion(-)
```

## GitHub

这些命令在本地机器和本地环境中运行。这只是基础步骤，但我确信，通过这些命令，你能够完成每天 80% 的工作。如果你不能这样做，有很多工具可以帮助你处理 Git 命令，例如 `git kraken`，或者你甚至可以使用 Visual Studio Code 的插件。我们需要记住，团队规模越大，你遇到的冲突就越多，同时发生的更改也越多。

为了共享我们的代码，我们可以使用 `GitHub`、`GitLab` 或 `Bitbucket`。这些平台允许我们托管仓库、与他人协作并在云环境中管理版本控制。

![](img/Figure-9.8.jpg)

**图 9.8**

现在，我们可以提交并推送到 GitHub 了：

```
PS C:\Users\1511 MXTI\Chapter09> git add –all
PS C:\Users\1511 MXTI\Chapter09> git commit -m "adding new feature"
[new_feature 938b554] adding new feature
1 file changed, 3 insertions(+), 1 deletion(-)
PS C:\Users\1511 MXTI\Chapter09> git push origin new_feature
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 294 bytes | 294.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote:
remote: Create a pull request for 'new_feature' on GitHub by visiting:
remote:      https://github.com/AlissonMMenezes/Chapter09/pull/new/new_feature
remote:
To https://github.com/AlissonMMenezes/Chapter09.git
* [new branch]      new_feature -> new_feature
```

代码已发送，GitHub 命令返回了一个 URL：

[`github.com/AlissonMMenezes/Chapter09/pull/new/new_feature`](https://github.com/AlissonMMenezes/Chapter09/pull/new/new_feature)

该 URL 将根据我们刚刚创建的分支重定向到新的拉请求（pull request）页面。让我们来看：

![](img/Figure-9.9.jpg)

**图 9.9**

我们可以给出一个与我们操作相对应的标题。例如，它可以是你的 Jira 任务名称，类似于 `DASF-158: changing the SSH keys`。如果你愿意，可以描述你所做的工作，或者只为代码审查提供一条信息。例如，请查看一下 `55` 到 `99` 之间的行。我不确定我的逻辑是否正确。现在，你可以创建 `pull request` 了：

![](img/Figure-9.10.jpg)

**图 9.10**

这就是 `PR`（`Pull Request`）的样子。现在，我们可以将其与 `master` 分支或我们想要的另一个分支合并：

![](img/Figure-9.11.jpg)

**图 9.11**

## 总结

这是一个关于 Git 的非常快速且简短的介绍。但我确定这对于你的日常任务已经足够。当然，在现实世界中，我们将面临许多冲突。合作的团队越大，管理代码、分支和审查的挑战就越多，也越复杂。如果你幸运地在初创公司工作，并且你是负责所有云基础设施的 DevOps 人员，这可能能够满足你 100% 的需求。

# 第 10 章

# 使用 Jenkins 进行持续集成和持续交付

本章旨在向你介绍流水线（Pipelines）、`CI`（持续集成）和 `CD`（持续交付）的概念。它还介绍了 Jenkins，这是最著名的开源 CI/CD 平台。

## 结构

在本章中，我们将讨论以下主题：

* 流水线 (Pipelines)
* 持续集成 (Continuous Integration)
* 持续交付 (Continuous Delivery)
* 代码即流水线 (Pipeline as Code) 和 Jenkins

## 目标

学习本单元后，你应该能够：

* 了解 DevOps 流水线
* 区分并实现 CI/CD
* 使用 Groovy 和 Jenkins 使用代码创建流水线
* 使用 Vagrant、Docker 和 Jenkins 部署应用程序

# 流水线 (Pipelines)

我们可以将流水线定义为一系列步骤，按照预定义的路径将事物从起点到终点。在我们的情况下，当代码进入流水线时，我们必须检查许多事情，例如代码质量、最佳实践、运行测试、生成 `ZIP` 文件，并且可以根据需要无限增加。在流水线的末端，你将获得具有质量、遵循最佳实践并准备好以自动化方式部署的一切。它有助于你提高产品或基础设施的质量，并加速过程，因为不需要手动测试流水线的每个部分。对于某些流水线，DevOps 实践定义了特定的名称，例如持续集成和持续交付。

## 持续集成 (Continuous Integration)

通常，当我们开发软件时，应用程序在到达最终客户之前会经过许多阶段。目前，我们有这些常见的阶段：

* **开发 (Development)**：开发者可以在这里测试应用程序、修复错误并验证新请求。在这个环境中，我们可以破坏任何东西。
* **测试 (Staging)**：生产环境的副本，但仅供业务团队验证需求。在这个环境中，可能会出现故障。
* **生产 (Production)**：这是应用程序实际运行的环境，所有内容都经过了验证、测试，并准备好交付最终客户。

目标是尽可能地交付应用程序以避免问题。

持续集成流水线的创建是为了连接所有环境。例如，在开发阶段，我们必须遵循某些测试：

* **单元测试 (Unit tests)**：此测试旨在验证代码中每个部分的业务规则，如类、方法、函数或其他任何。但这些是你可以执行的最简单的测试。例如，你可能会收到创建一个函数的任务，其中需要计算两个数字之和。你的测试将数字传递给该函数并检查它是否返回了预期结果。
* **集成测试 (Integration tests)**：在这里，你必须测试一个业务用例。例如，你创建了一个 `API`。你的最终客户将发送两个参数的请求，并期望得到带有产品数据的 JSON 响应。在这种情况下，我们不需要检查你的 `API` 源码中发生了什么，我们只需要确保当我们接收到这两个参数时，我们会返回带有产品数据的 JSON。
* **端到端测试 (End-to-end)**：这是你应用程序中最困难的测试。它将模拟真实客户，详细测试你的整个系统和每项功能。开发它需要花费大量时间，因此大多数公司到集成测试就停止了。
* **质量测试 (Quality test)**：此测试更多用于检查你的代码质量。如果你遵循了最佳实践，如果你创建了可复用的代码，而不是仅仅在代码中到处复制粘贴（这会使维护变得困难）。

当然，我解释的这些测试只是你将工作的大多数公司会遇到的常见测试。然而，测试应用程序的方法更多。它会因项目和因公司而异。

一旦我们通过了所有这些测试，就必须将应用程序交给其他团队，他们也会对应用程序进行测试（许多时候是手动方式），以确保开发者理解了需求以及我们需要如何编写产品。这就是我们进行持续交付（Continuous Delivery）的地方。

## 持续交付 (Continuous Delivery)

在这个阶段，开发者完成了他们被分配的所有工作。但当然，在客户请求和软件交付之间可能会出现许多沟通问题。

因此，一旦开发者完成了所有测试，我们就可以认为有了一个新版本的应用程序，可以命名为版本 `0.1`。假设它运行正常，我们将为该应用程序创建一个包并将其部署到测试环境（staging environment）。在该环境中，公司业务部门的人员将再次验证功能请求是否按照他们的要求正常工作。此阶段也用于 UX 团队验证您的界面是否易于理解和易用。如果此版本的应用程序没有满足所有要求，或者开发者没有理解新功能应该如何工作，则该版本会被丢弃，他们将在名为 `0.2` 的新版本上工作。例如，它将再次通过所有环境，直到满足最终客户指定的所有要求。

## 代码即流水线 (Pipeline as Code) 与 Jenkins

我们有许多工具可以帮助我们处理流水线以及环境之间的集成，Jenkins 确实是最著名的，因为它的灵活性允许我们安装许多插件以轻松与云提供商集成，而且它是开源的。因此，我们不需要支付许可费用。

本书的重点特别不是软件开发，而是基础设施即代码（Infrastructure as Code）。因此，我将使用的所有示例都将涉及基础设施以及我们如何测试和部署它。

首先，我们需要设置我们的 Jenkins 服务器。我将使用 Vagrant 来设置它。通过创建一个带有 Ubuntu 的虚拟机，安装 Docker，然后 Jenkins 将运行在 Docker 之上：

```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.box_check_update = false
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  config.vm.define "docker" do |docker|
    docker.vm.box = "ubuntu/bionic64"
    docker.vm.network "private_network", ip: "192.168.33.11"
    docker.vm.hostname = "docker"
    docker.vm.provision "shell", inline: <<-SHELL
      apt clean
      apt-get update
      apt-get remove docker docker-engine docker.io containerd runc -y
      apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common -y
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
      add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
      apt-get update -y
      apt-get install docker.io -y
    SHELL
  end
end
```

上述代码只是对 `chapter06` 稍微修改过。然后，我们已经知道如何在 Vagrant 上安装和运行虚拟机。现在，我有一个正在运行的 Docker 环境，在容器中运行 Jenkins 非常简单。只需运行以下命令：

```bash
root@docker:~# docker run -tdi --restart=always --name jenkins -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts
```

容器启动后，您可以通过以下地址访问 Jenkins：

`http://192.168.33.11:8080/login?from=%2F`

它将向您显示以下屏幕，要求输入初始密码：

![](img/Figure-10.1.jpg)

**图 10.1**

您可以通过运行以下命令获取密码：

```bash
docker exec -ti jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```



`a7a1b2c796404bceab99b014f3220a9a`

您可以直接复制密码：

`a7a1b2c796404bceab99b014f3220a9a`

粘贴到屏幕中并继续安装。

![](img/Figure-10.2.jpg)

**图 10.2**

强烈建议安装建议的插件，因为这将安装其中最重要的插件之一，即`git`插件。现在，您只需要按照顺序点击`Next`、`Next`和`Finish`来完成安装。

![](img/Figure-10.3.jpg)

**图 10.3**

安装的最后部分是设置管理员凭据。我将用户和密码都设置为`admin`/`admin`。最后，欢迎来到 Jenkins：

![](img/Figure-10.4.jpg)

**图 10.4**

每个用过 Jenkins 的人都知道，UX 并不是 Jenkins 的强项。为了解决这个问题，有一个非常著名的插件叫做 Blue Ocean，用来改进我们的界面和可用性。

进入`Manage Jenkins` | `Manage Plugins` | `Available`并`Search` Blue Ocean：

![](img/Figure-10.5.jpg)

**图 10.5**

安装插件并重启 Jenkins。一切完成后，您将看到一个新按钮`Open Blue Ocean`可用：

![](img/Figure-10.6.jpg)

**图 10.6**

点击该按钮并检查新界面：

![](img/Figure-10.7.jpg)

**图 10.7**

从初始屏幕来看，我们可以它好得多。当然，并不是强制要求使用这个界面。这只是某种花哨的功能，但我很喜欢它。不仅是因为界面，它还强制要求使用仓库对流水线进行版本控制。您可以点击`Create a new Pipeline`并检查它：

![](img/Figure-10.8.jpg)

**图 10.8**

在我的情况下，我将选择`GitHub`，因为我已经为这一章创建了一个仓库。创建流水线非常简单。您只需要按照屏幕上显示的步骤操作，在 GitHub 上创建一个访问令牌，并将其绑定到您的安装中，如前面的截图所示：

![](img/Figure-10.9.jpg)

**图 10.9**

Jenkins 使用 Groovy 语言来编写流水线。在仓库根目录下，必须有一个名为`Jenkinsfile`的文件，Jenkins 将扫描文件并运行流水线。我已经用以下代码创建了流水线：

```groovy
pipeline {
  agent any;
  stages {
    stage('Code Quality') {
      steps {
        sh 'echo checking quality'
      }
    }
    stage('Unit Tests') {
      steps {
        sh 'echo Testing the Applications'
      }
    }
    stage('Build') {
      steps {
        sh 'echo Creating application'
      }
    }
    stage('Delivery') {
      steps {
        sh 'echo Uploading the artifact to a repository'
      }
    }
    stage('Deploy') {
      steps {
        sh 'echo Deploying the Application'
      }
    }
  }
}
```

这是我们需要的基础骨架。保存一切并检查界面，您将看到流水线自动运行并成功：

![](img/Figure-10.10.jpg)

**图 10.10**

```python
response = {"approved":False,
"newLimit":data.get("limit"),
"reason":"Transaction above the limit"}
return jsonify(response)
return f(*args, **kwargs)
return(validation)
@app.route("/api/transaction",methods=["POST"])
@check_card
def transaction():
card = request.get_json()
new_limit = card.get("limit") - card.get("transaction").get("amount")
response = {"approved":True,"newLimit":new_limit}
return jsonify(response)
if __name__ == '__main__':
app.run(debug=True)
```

看起来好多多了，不是吗？记住我们重构了代码，因此，我们也需要更改测试。在测试源码中，我们只需要更改以下部分：

```python
@pytest.fixture
def client():
    APP.config['TESTING'] = True
    client = APP.test_client()
    yield client
```

我们已经准备好再次运行流水线了。让我们看看新的行为如何：

![](img/Figure-10.13.jpg)

**图 10.13**

现在完美了！我们通过了代码质量检查和功能测试，但在构建步骤处被阻塞了。这是合理的，因为我将代码编写为在执行`exit 1`。对于这一步，我们需要生成一个新的 Docker 镜像。将我们的应用程序部署在运行 Jenkins 容器的同一台服务器上。

为了实现这一点，我们可以将虚拟机设置为 Jenkins 节点。添加新节点时必须访问的地址如下：

`http://192.168.33.11:8080/computer/new`

我将该节点命名为 Docker server。远程根目录必须是`/tmp`，标签（Labels）也必须是`Docker server`。启动方法（Launch method）必须通过 agent 连接到主节点。然后，我们将在虚拟机安装 agent，它将负责运行流水线的后续步骤：

![](img/Figure-10.14.jpg)

**图 10.14**

配置并保存配置后，Jenkins 将为你提供可用 agent：

`http://192.168.33.11:8080/computer/DockerServer/`

![](img/Figure-10.15.jpg)

**图 10.15**

我们可以直接在虚拟机中复制并粘贴该行：

```bash
root@docker:~# apt install openjdk-8-jre-headless -y
root@docker:~# wget http://192.168.33.11:8080/jnlpJars/agent.jar
root@docker:~# java -jar agent.jar -jnlpUrl http://192.168.33.11:8080/computer/DockerServer/slave-agent.jnlp -secret 1309b876151399817cab2ef0da0ea34716ecbc01a44b38a95c93fdd748d72629 -workDir "/tmp"
INFO: Agent discovery successful
Agent address: 192.168.33.11
Agent port:   50000
Identity:     52:84:5b:cb:ed:f7:98:4c:da:b2:64:66:48:de:cf:be
Jun 10, 2020 12:46:41 PM hudson.remoting.jnlp.Main$CuiListener status
INFO: Handshaking
Jun 10, 2020 12:46:41 PM hudson.remoting.jnlp.Main$CuiListener status
INFO: Connecting to 192.168.33.11:50000
Jun 10, 2020 12:46:41 PM hudson.remoting.jnlp.Main$CuiListener status
INFO: Trying protocol: JNLP4-connect
Jun 10, 2020 12:46:42 PM hudson.remoting.jnlp.Main$CuiListener status
INFO: Remote identity confirmed: 52:84:5b:cb:ed:f7:98:4c:da:b2:64:66:48:de:cf:be
Jun 10, 2020 12:46:43 PM hudson.remoting.jnlp.Main$CuiListener status
INFO: Connected
```

agent 已成功连接。现在，我们可以继续编写流水线代码并完成应用程序部署：

```groovy
pipeline {
    agent any;
    stages {
        stage('Preparing the environment') {
            steps {
                sh 'python -m pip install -r requirements.txt'
            }
        }
        stage('Code Quality') {
            steps {
                sh 'python -m pylint app.py'
            }
        }
        stage('Tests') {
            steps {
                sh 'python -m pytest'
            }
        }
        stage('Build') {
            agent {
                node{
                    label "DockerServer";
                }
            }
            steps {
                sh 'docker build https://github.com/AlissonMMenezes/Chapter10.git -t chapter10:latest'
            }
        }
        stage('Deploy') {
            agent {
                node{
                    label "DockerServer";
                }
            }
            steps {
                sh 'docker run -tdi -p 5000:5000 chapter10:latest'
            }
        }
    }
}
```

这是流水线的最新版本。让我们运行它看看它是否可以工作：

![](img/Figure-10.16.jpg)

**图 10.16**

太棒了！现在我们拥有了一个功能完整的流水线，它带有应用版本控制，可以运行测试、代码质量检查，并且实现了 Docker 化。

## 结论

我们刚刚学习了如何使用 Jenkins 创建代码即流水线（pipeline as code）、运行代码质量检查、功能测试、基于功能应用程序创建镜像，并将其部署在 Docker 服务器上。

我们可以看到，这并不是一项极其困难的任务。当然，你的项目越复杂，你的流水线就会越复杂。例如，在初始步骤中，我们能够让 Jenkins 独立运行一切。而在最后步骤中，我们必须添加一个节点并在其上运行。我们还学习了关于 Docker 的新知识，例如每次服务器启动时启动容器的某些参数。我们还可以使用直接托管在远程仓库中的 Dockerfile 来构建镜像。

我深信这段介绍将为你创建完美契合你项目的流水线提供开始。

## 问题

1. 使用流水线有什么好处？
2. 什么是 CI 和 CD？
3. 为什么将流水线作为代码（as code）是一种良好的实践？
4. BlueOcean 插件可以带给我们哪些好处？
5. 什么时候需要 Jenkins 节点？

## 第 11 章

## 使用 Kubernetes 部署和扩展你的应用程序

本旨在向你介绍 Kubernetes，展示如何创建 YAML 文件来使用最流行且可靠的容器编排工具部署并扩展你的应用程序。

## 结构

在本章中，我们将讨论以下主题：

* Kubernetes
* Kubernetes 简介
* 在云端部署

## 目标

学习完本单元后，你应该能够：

* 了解 Kubernetes
* 解释 Kubernetes 的优势
* 创建 YAML 文件来部署你的应用程序
* 测试在集群中运行的应用程序

## Kubernetes

Kubernetes 是一个容器编排工具。在之前的章节中，我们经常使用 Docker 来部署应用程序、创建新镜像等。然而，想象如果你有超过一百个容器需要管理，这对于一个人来说是不可能完成的任务。Docker 本身带有`Docker Swarm`，可以帮助你完成该任务。但它并没有被市场广泛采用，因为缺少了 Kubernetes 中的某些功能和集成。它由 Google 在几年前创建，基于一个名为`Borg`的项目（这也是容器编排工具）。随着 Docker 的发布，该项目进行了适配，现在它已成为管理集群的官方平台。

## Kubernetes 简介

与其他章节一样，我们的重点始终是如何真实环境中实现它。让我们简要介绍如何设置本地环境来学习 Kubernetes，然后我们可以设置真实环境并部署应用程序。你会发现，在本地环境和云端运行时命令是相同的。

首先，我们将安装`minikube`。它是一个在 Virtual Box 之上设置本地 Kubernetes 环境的工具，正如我们随书中做的那样：

```bash
wget https://github.com/kubernetes/minikube/releases/download/v1.11.0/minikube-windows-amd64.exe -O minikube.exe
```

如果你使用的是其他操作系统，可以参考官方文档：[`kubernetes.io/docs/tasks/install-minikube/`](https://kubernetes.io/docs/tasks/install-minikube/)

然后，我们可以启动集群：

```bash
PS C:\Users\1511 MXTI>.\minikube.exe start
* minikube v1.11.0 on Microsoft Windows 10 Pro 10.0.19041 Build 19041
* Automatically selected the virtualbox driver
* Downloading VM boot image …
* Starting control plane node minikube in cluster minikube
* Downloading Kubernetes v1.18.3 preload …
* Creating virtualbox VM (CPUs=2, Memory=6000MB, Disk=20000MB) …
* Preparing Kubernetes v1.18.3 on Docker 19.03.8 …
* Verifying Kubernetes components…
* Enabled addons: default-storageclass, storage-provisioner
* Done! kubectl is now configured to use "minikube"
```

我们还需要安装`kubectl`，这是一个我们将用它来管理`dev`、`stg`和`prd`集群的命令。如果您使用的是其他操作系统，可以遵循官方文档：[`kubernetes.io/docs/tasks/tools/install-minikube/`](https://kubernetes.io/docs/tasks/tools/install-minikube/)

```bash
PS C:\Users\1511 MXTI> wget https://storage.googleapis.com/kubernetes-release/release/v1.18.3/bin/linux/amd64/kubectl -O kubectl.exe
```

首先，我们可以运行一个简单的命令来查看在我们的环境中配置了多少集群：

```bash
PS C:\Users\1511 MXTI> .\kubectl.exe config get-clusters
```
`NAME`
Minikube

目前，只有一个`minikube.`。但我们会有更多，需要了解的一个重要点是`kubectl`是从哪里获取这些信息的：

```bash
PS C:\Users\1511 MXTI> cat 'C:\Users\1511 MXTI\.kube\config'
```



在`minikube`安装`k8s`集群后，它会将配置写入位于您的`home`目录下的`.kube`文件夹中的`config`文件。所有的认证信息都位于该文件中。如果您想了解集群内部运行的所有内容，可以运行以下命令：

![](img/p227.jpg)

我使用了参数来获取`pods`，另一个参数是`–all-namespaces.`。它向我们展示了集群所有命名空间中运行的所有容器。目前，我们只有一个，名为`kube-system`。在继续学习更多命令之前，理解`pod`、namespace（命名空间）以及其他概念是非常重要的。

- **POD**: 它代表运行的一个或多个容器集。
- **NAMESPACE (命名空间)**: 对象之间的逻辑隔离。例如，在同一个集群中，我可以拥有`dev – stg – prd`命名空间，每个空间运行相同应用程序的不同版本，或者可以是`project1`、`project2`和`project3`。您可以根据需要将集群分为任意数量的命名空间。
- **SERVICE (服务)**: 这是您用于连接外部世界与您的`pods`的资源。如果您还记得Docker章节，我们必须将主机端口`8080`映射到容器端口`8080.`。但这仅针对一个容器。在Kubernetes中，我们有一个`POD`，它可以包含一个或多个容器，并可以随时销毁和重建。然而，我们不能丢失端口映射，这就是`SERVICE`的工作，我们在其中配置`NODE`端口，它将重定向到`POD`端口，与我们在Docker中做的方法完全相同。这是服务的用途之一，我们也可以有其他实现，例如负载均衡器，它有一个`clusterIP`，将接收传入的连接并转发到容器。
- **DEPLOYMENT (部署)**: 这是一组规则，确保您有特定数量的运行容器。所有容器都运行相同的镜像，如果任何容器死亡，它将会被重建。换句话说，它会自动创建您的`PODs`，并且`REPLICASET`会确保运行容器的存在。
- **INGRESS (入口)**: 该资源可以比作虚拟主机，就像我们在Apache章节中做的那样。在这里，我们将有一个`NAME`，它将指向`SERVICE`，而`SERVICE`将指向`POD`。如果您没有使用DNS，则`INGRESS`不是强制性的。

上述项目被称为Kubernetes对象。还有许多其他对象可以探索以了解更多关于Kubernetes的知识，但我们可以专门写一本书来解释。现在，我认为最后部署一些微服务足够了。如果您正在部署有状态的应用，您可能需要扩展阅读范围到`VOLUMES`（卷）。

现在，我们可以创建第一个`NAMESPACE`并开始尝试一些对象：

```bash
PS C:\Users\1511 MXTI> .\kubectl.exe create namespace chapter11

namespace/chapter11 created
```

```bash
PS C:\Users\1511 MXTI> .\kubectl.exe get ns

NAME             STATUS    AGE
chapter11        Active    11s
default          Active    38m
kube-node-lease  Active    38m
kube-public      Active    38m
kube-system      Active    38m
```

注意，可以使用参数的全形式，也可以使用短形式，例如当我列出命名空间时，我只使用了`ns`。

`INGRESS`是Kubernetes的一个独立资源。当您在云端使用它时，某些云厂商已经为您安装好了。但在本地环境中，您通常需要安装。对于我们的本地环境，我们必须使用以下命令进行安装：

```bash
PS C:\Users\1511 MXTI> .\minikube.exe addons enable ingress

* The 'ingress' addon is enabled
```

要在集群中运行您的第一个应用程序，请运行以下命令：

```bash
PS C:\Users\1511 MXTI> .\kubectl.exe --namespace=chapter11 run python -dti --port=8080 --image=alissonmenezes/python:latest -l app=python
```

此命令将我的个人仓库`alissonmenezes`下载`python_app:v1`并暴露端口`8080`。如果您想检查`pod`是否正在运行，可以使用以下命令：

```bash
PS C:\Users\1511 MXTI> kubectl get pods --namespace=chapter11

NAME    READY   STATUS    RESTARTS   AGE
python   1/1     Running   1             6m43s
```

现在我们有一个包含一个容器的`pod`在运行。然而，我们想要访问该应用程序，但目前它仅在集群内部可用。集群内部的其他应用程序已经能够访问它，但对我们外部用户来说，必须为它创建一个服务：

```bash
PS C:\Users\1511 MXTI> .\kubectl.exe --namespace=chapter11 create service clusterip python --tcp=80:8080

service/python created
```

我们刚刚创建了`clusterip`类型的`SERVICE`。它不暴露`NODE`端口，我们需要`ingress`来从集群外部到内部的映射。创建一个名为`app.yaml`的文件，内容如下：

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
name: python
namespace: chapter11
annotations:
  nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  backend:
    serviceName: python
    servicePort: 80
```

`INGRESS`由Nginx服务器组成，我们称之为“Ingress Controller”（入口控制器）。它基本上是在将来自任何地址或名称的传入连接通过代理传递转发到名为Python的服务。

要应用该文件，您必须使用以下命令：

```bash
PS C:\Users\1511 MXTI> .\kubectl.exe apply -f .\app.yaml

ingress.extensions/python created
```

获取`minikube`的IP地址，运行以下命令：

```bash
PS C:\Users\1511 MXTI> .\minikube ip

192.168.99.101
```

如果您在网络浏览器中输入此地址，您将看到以下页面：

![](img/Figure-11.1.jpg)

**图 11.1**

应用程序正在运行！

我们通过命令成功创建了一切，并仅使用`YAML`文件创建了`Ingress`。然而，完全可以使用文件来创建一切，这是在Kubernetes上部署一切常用的方法，因为我们可以对文件进行版本控制，并像上一章那样在流水线中运行它们。

我们可以如下所示在一个文件中创建所有内容：

```yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
name: python
namespace: chapter11
labels:
  app: python
spec:
  replicas: 1
  selector:
    matchLabels:
      app: python
  template:
    metadata:
      labels:
        app: python
    spec:
      containers:
      - name: python
        image: alissonmenezes/python:latest
        ports:
        - containerPort: 8080
---
apiVersion: v1
kind: Service
metadata:
  labels:
    app: python
  name: python
namespace: chapter11
spec:
  ports:
  - name: http
    port: 80
    protocol: TCP
    targetPort: 8080
  selector:
    app: python
  type: ClusterIP
---
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  labels:
    app: python
  name: python
namespace: chapter11
annotations:
  nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  backend:
    serviceName: python
    servicePort: 80
```

`backend:`
`serviceName: python`
`servicePort: 80`

为了确保一切运行正常，你可以删除所有内容：

```bash
PS C:\Users\1511 MXTI>
.\kubectl.exe delete all -l app=python --all-namespaces
```

`pod "python-779879dbb6-w57pr" deleted`

使用完整文件内容应用文件：

```bash
PS C:\Users\1511 MXTI>
.\kubectl.exe apply -f .\app.yaml
```

`deployment.apps/python created`
`service/python created`
`ingress.extensions/python unchanged`

现在，你已经掌握了基础知识。让我们来看看它在真实环境中的部署情况。

## 在云端上部署

为了在云端进行部署，我们将使用目前一直以来完全相同的`app.yaml`。但首先，我们需要创建一个Kubernetes集群。我将使用GCP来实现。

我已经创建了一个名为`chapter11`的项目，我将在其中置备集群：

```bash
PS C:\Users\1511 MXTI>
gcloud config set project chapter11-280417
```

`Updated property [core/project].`

定义计算节点创建的位置：

```bash
PS C:\Users\1511 MXTI>
gcloud config set compute/zone us-central1-c
```

`Updated property [compute/zone].`

再次定义计算节点创建的位置：

```bash
PS C:\Users\1511 MXTI>
gcloud container clusters create chapter11 --num-nodes=1
```

```
NAME      LOCATION       MASTER_VERSION  MASTER_IP      MACHINE_TYPE  NODE_VERSION  NUM_NODES  STATUS
chapter11  us-central1-c  1.14.10-gke.36  35.193.191.37  n1-standard-1  1.14.10-gke.36  1           RUNNING
```

一旦集群运行，我们需要使用以下命令登录集群：

```bash
PS C:\Users\1511 MXTI>
gcloud container clusters get-credentials chapter11
```

`Fetching cluster endpoint and auth data.`
`kubeconfig entry generated for chapter11.`

就这样，一切都很完美。现在，我们可以像以前使用`minikube`一样进行工作：

```bash
PS C:\Users\1511 MXTI>
.\kubectl.exe config get-clusters
```

```
NAME
minikube
gke_chapter11-280417_us-central1-c_chapter11
```

通过运行相同的命令，我们可以看到配置了另一个集群，名为`gke_chapter11`。当我们运行`get-credentials`命令时，`gke`被默认设置，现在，我们不需要考虑在一个集群还是另一个集群中运行命令了。

我们还可以通过以下命令检查运行的内容：

```bash
PS C:\Users\1511 MXTI>
.\kubectl.exe get pods --all-namespaces
```

```
NAMESPACE  NAME                           READY  STATUS    RESTARTS  AGE
kube-system  event-exporter-v0.2.5-599d65f456-v2h9f  2/2   Running   0         4m50s
kube-system  fluentd-gcp-scaler-bfd6cf8dd-c4b6c  1/1   Running   0         4m42s
kube-system  fluentd-gcp-v3.1.1-pj6pp        2/2   Running   0         3m51s
kube-system  heapster-gke-7bff5f7474-9vgtb      3/3   Running   0         3m42s
kube-system  kube-dns-5995c95f64-742kn        4/4   Running   0         4m53s
kube-system  kube-dns-autoscaler-8687c64fc-w7w2d  1/1   Running   0         4m41s
kube-system  kube-proxy-gke-chapter11-default-pool-e3952147-h0gc  1/1   Running   0         4m41s
kube-system  l7-default-backend-8f479dd9-tpmk6      1/1   Running   0         4m53s
kube-system  metrics-server-v0.3.1-5c6fbf777-4xmlf  2/2   Running   0         4m50s
```

Elasticsearch、Fluentd和Kibana；这一堆栈在Kubernetes环境中非常有名。通常，我们可以在所有节点上看到运行一个`FluentD`的`DaemonSet`，用于检索日志并将其发送到`Elasticsearch`服务器，该服务器会对日志进行索引和解析，从而能够根据您的标准轻松搜索特定事件。`Kibana`是Web界面，可以连接到`elasticsearch`以实现数据可视化。否则，我们必须向`elasticsearch`的API发起请求。`Kibana`还为我们许多功能，例如基于日志创建图表。因此，我们可以创建过去两个小时内应用程序产生错误数量的可视化。或者在另一个示例中，我们可以统计HTTP状态码并根据请求数进行排序。40个请求返回状态400，500个请求返回状态200，10个请求返回状态500等。

## 安装EFK堆栈

我们将采用以下场景：我们将在使用`Vagrant`在虚拟机中设置`elastsearch`和`Kibana`，`Fluentd`将运行在我们的`minikube`集群中，用于将运行中的应用程序日志推送到远程服务器，并将以中心化的方式进行可视化。

`Vagrant`文件如下：

```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :
# 所有Vagrant配置均在下方。Vagrant.configure中的 "2"
# 配置了配置版本（我们为了向后兼容性支持
# 旧样式）。除非你确定自己在做什么，否则请不要更改它。
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.define "efk" do |efk|
    efk.vm.network "private_network", ip: "192.168.99.50"
    efk.vm.hostname = "efk"
    config.vm.provider "virtualbox" do |v|
      v.memory = 4096
    end
    efk.vm.provision "shell", inline: <<-SHELL
      apt clean
```



使用以下命令置备您的虚拟机：

`vagrant up --provision`

当服务器就绪后，我们必须更改某些配置。首先，通过以下命令启用`elasticsearch`监听所有地址：

`sed -i "s/#network.host: 192.168.0.1/network.host: 0.0.0.0/g" /etc/Elasticsearch/Elasticsearch.yml`

其次，通过以下命令更改种子主机：

`sed -i "s/#discovery.seed_hosts: \[\"host1\", \"host2\"\]/discovery.seed_hosts: \[\]/g" /etc/Elasticsearch/Elasticsearch.yml`

第三，你必须通过以下命令定义为单节点集群：

`echo "discovery.type: single-node">> /etc/Elasticsearch/Elasticsearch.yml`

第四，通过以下命令将`Kibana`配置也监听所有地址：

`sed -i "s/#server.host: \"localhost\"/server.host: \"0.0.0.0\"/g" /etc/kibana/kibana.yml`

然后，你可以通过运行以下命令重启服务：

```bash
root@efk:~# /etc/init.d/kibana restart
d/Elasticsearch start
kibana started
root@efk:~# /etc/init.d/Elasticsearch start
[….] Starting Elasticsearch (via systemctl): Elasticsearch.service
```

如果你正确执行了所有步骤，可以使用命令`ss –ntpl`检查服务端口：

![](img/Figure-12.1.jpg)

**图 12.1**

`Kibana`运行在端口`5601`。现在，你可以使用以下地址检查界面。

`http://192.168.99.50:5601`

![](img/Figure-12.2.jpg)

**图 12.2**

服务器启动需要一段时间。如果花费了大约 10 分钟，请担心。

此时，我们不需要在这台服务器上做任何其他操作了，所以让我们进入`minikube`并运行`FluentD`来推送日志。之后，我们将返回`Kibana`服务器查看日志。

## 运行 Fluentd

首先，让我们使用以下命令设置`minikube`环境：

```bash
PS C:\Users\1511 MXTI\Documents\Blog\EKF> minikube delete
* Deleting "minikube" in virtualbox …
* Removed all traces of the "minikube" cluster.
PS C:\Users\1511 MXTI\Documents\Blog\EKF> minikube start
* minikube v1.11.0 on Microsoft Windows 10 Pro 10.0.19041 Build 19041
* Automatically selected the virtualbox driver
* Starting control plane node minikube in cluster minikube
* Creating virtualbox VM (CPUs=2, Memory=6000MB, Disk=20000MB) …
* Preparing Kubernetes v1.18.3 on Docker 19.03.8 …
* Verifying Kubernetes components…
* Enabled addons: default-storageclass, storage-provisioner
* Done! kubectl is now configured to use "minikube"
```

我删除了现有的环境并启动了一个全新的环境，以确保我们的环境完全相同。在 Kubernetes 环境运行的情况下，我们将使用以下文件设置`DaemonSet`：

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: fluentd
  namespace: kube-system
labels:
  k8s-app: fluentd-logging
  version: v1
spec:
  selector:
    matchLabels:
      name: fluentd
  template:
    metadata:
      labels:
        name: fluentd
        k8s-app: fluentd-logging
        version: v1
        kubernetes.io/cluster-service: "true"
    spec:
      containers:
      - name: fluentd
        image: fluent/fluentd-kubernetes-daemonset:v1-debian-Elasticsearch
        env:
        - name: FLUENT_ELASTICSEARCH_HOST
          value: "192.168.99.50"
        - name: FLUENT_ELASTICSEARCH_SSL_VERIFY
          value: "false"
        - name: FLUENT_ELASTICSEARCH_PORT
          value: "9200"
        - name: FLUENT_ELASTICSEARCH_SCHEME
          value: "http"
        - name: FLUENT_UID
          value: "0"
        - name: FLUENT_LOGSTASH_FORMAT
          value: "true"
        - name: FLUENT_LOGSTASH_PREFIX
          value: "fluentd"
        - name: FLUENT_SYSTEMD_CONF
          value: "disable"
        resources:
          limits:
            memory: 200Mi
          requests:
            cpu: 100m
            memory: 200Mi
        volumeMounts:
        - name: varlog
          mountPath: /var/log
        - name: varlibcontainers
          mountPath: /var/lib/containers
          readOnly: true
      volumes:
      - name: varlog
        hostPath:
          path: /var/log
      - name: varlibcontainers
        hostPath:
          path: /var/lib/containers
```

`DaemonSet`：是一个负责在每个节点上运行相同 pod 的 Kubernetes 对象。普通 pod 与`DaemonSet`的区别在于，`Set`在节点上是强制性的，如果你在部署应用程序，并不非要在所有节点上运行该应用程序：

```bash
kubectl apply -f fluentd.yaml
daemonset.apps/fluentd configured
```

前面的命令将在你的集群中运行`DaemonSet`。要检查它是否运行，你可以运行以下命令：

```bash
PS C:\Users\1511 MXTI\Documents\Blog\EKF> kubectl get daemonset -n kube-system
NAME       DESIRED   CURRENT   READY   UP-DATE   AVAILABLE   NODE SELECTOR   AGE
fluentd    1         1         1         0s        1           <none>          7m26s
kube-proxy  1         1         1         0s        1           kubernetes.io/os=linux  13h
```

检查日志是非常重要的，因为从开始，日志必须发送到 elasticsearch 服务器：

```bash
PS C:\Users\1511 MXTI\Documents\Blog\EKF> kubectl logs daemonset/fluentd -n kube-system
```

现在，我们可以回到 Kibana 仪表板，因为日志应该已经发送到服务器了。下一个目标是将它们可视化。在初始页面上，点击`Explore on my own`（自行探索）选项。然后，点击左上角并发现日志：

![](img/Figure-12.3.jpg)

**图 12.3**

现在，我们可以创建一个匹配所有存储日志的索引。当该集群仅用于此 Kubernetes 环境时，我们就可以这样做。如果你对公司的所有日志使用同一个`elasticsearch`，那么为每种情况创建不同的索引会更好：

![](img/Figure-12.4.jpg)

**图 12.4**

我们必须定义`Index Pattern as *`（索引模式为 *），这将获取所有的日志：

![](img/Figure-12.5.jpg)

**图 12.5**

你可以将时间过滤器选择为时间。如果我们再次回到发现（discovery）部分并选择 3 个月前的日志，我们将能够看到日志已经在`Elasticsearch`中。当然，我们不需要设置 3 个月前，我只是想确保我们能看到所有的当前日志：

![](img/Figure-12.6.jpg)

**图 12.6**

如果你查看左侧，可以找到一些 Kubernetes 元素。你可以尝试操作一下，因为现在我们不需要访问 Kubernetes 集群就可以访问日志。

让我们部署一个应用程序并看看我们如何检查日志：

```bash
kubectl create ns chapter11
```

创建一个名为`Chapter11: Deploying and Scaling your Application using Kubernetes`的命名空间，因为我们将使用上一个章节中的应用程序。应用程序的`yaml`文件如下：

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: python
  namespace: chapter11
  labels:
  app: python
spec:
  replicas: 1
  selector:
    matchLabels:
      app: python
  template:
    metadata:
      labels:
        app: python
    spec:
      containers:
      - name: python
        image: alissonmenezes/python:latest
        ports:
        - containerPort: 8080
---
apiVersion: v1
kind: Service
metadata:
  labels:
  app: python
  name: python
  namespace: chapter11
spec:
  ports:
  - name: http
    port: 80
    protocol: TCP
    targetPort: 8080
  selector:
    app: python
  type: ClusterIP
---
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: python
  labels:
    app: python
  namespace: chapter11
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  backend:
    serviceName: python
    servicePort: 80
```

现在运行以下命令：

```bash
PS C:\Users\1511 MXTI\Documents\Blog\EKF> minikube.exe ip
```

`192.168.99.102`

Kubernetes IP 是`192.168.99.102`。我们将使用它来访问应用程序。确保你已经通过以下命令启用了 ingress：

```bash
PS C:\Users\1511 MXTI\DataLake> minikube.exe addons enable ingress
```

* 'ingress' 插件已启用

如果我们在浏览器中访问应用程序，我们将看到以下页面：

![](img/Figure-12.7.jpg)

**图 12.7**

如果我们查看 Kubernetes 上的应用程序日志，我们可以看到以下：

```bash
PS C:\Users\1511 MXTI\DataLake> kubectl logs deploy/python -n chapter11
```

* Running on http://0.0.0.0:8080/ (Press CTRL+C to quit)
* Restarting with stat
* Debugger is active!
* Debugger PIN: 954-738-244

`172.17.0.6 - - [28/Jun/2020 10:22:16] "GET / HTTP/1.1" 200 -`

`172.17.0.6 - - [28/Jun/2020 10:22:17] "GET /favicon.ico HTTP/1.1" 404 -`

`172.17.0.6 - - [28/Jun/2020 10:22:18] "GET / HTTP/1.1" 200 -`

`172.17.0.6 - - [28/Jun/2020 10:22:18] "GET / HTTP/1.1" 200 -`

这意味着我们已经生成了一些日志，然后我们可以在 Kibana 上看到它们。让我们看一下。首先，我们需要 pod 名称：

```bash
PS C:\Users\1511 MXTI\DataLake> kubectl get pods -n chapter11
```



`NAME                         READY   STATUS    RESTARTS  AGE`
`python-779879dbb6-wrw2g  1/1     Running   0         44m`

在 Kibana 上的查询将如下：

`kubernetes.pod_name:python-779879dbb6-wrw2g`

语法是：`key : value`。然后，第一个参数是你想要过滤的相应元素。冒号 `:` 代表等于，最后是你用作标准的值。

你看到的 Kibana 页面将如截图所示：

![](img/Figure-12.8.jpg)

**图 12.8**

让我们分析日志，因为我们有一个重要信息需要检查：

![](img/Figure-12.9.jpg)

**图 12.9**

注意，`pod_name` 匹配标准，且日志包含了我们在 Kubernetes 上看到的日志行。现在我们确定日志已发送到 elasticsearch。我们可以在 Kibana 上将它们可视化，现在，我们可以创建一个特定的可视化结果来简化日志分析。

## 创建告警

既然 elasticsearch 中有了日志，而且我们知道如何找到它们，让我们创建一些告警，以便它们在事件发生时通知我们。事件可以由你定义，可以返回状态 `404`、状态 `500`，或者例如错误消息的一部分。

在我们的情况下，每当有人尝试访问不存在的页面时，它将返回 `404` 状态并发送通知。为了实现这一点，我们将使用一个名为 `ElastAlert` 的工具。这是一个 Python 工具，它可以连接到我们的 elasticsearch，读取日志并发送通知。

在 EFK 栈中，让我们安装它。

```bash
root@efk:~# apt install python3-pip -y
root@efk:~# python3 -m pip install elastalert
```

有时，我们可能会因为其他模块的版本而遇到问题。`ElastAlert`最重要的模块是 `PyYAML`。所以，让我们升级它以确保我们使用的是最新版本：

```bash
root@efk:~# python3 -m pip install PyYAML --upgrade
```

一旦安装 ElastAlert，我们需要将其与 elasticsearch 连接。要这样做，运行以下命令：

```bash
root@efk:~# elastalert-create-index
```

`Enter Elasticsearch host: 127.0.0.1`
`Enter Elasticsearch port: 9200`
`Use SSL? t/f: f`
`Enter optional basic-auth username:`
`Enter optional basic-auth password:`
`Enter optional Elasticsearch prefix (prepends a string to the URL of request):`
`New index name? (Default elastalert_status)`
`New alias name? (Default elastalert_alerts)`
`Name of existing index to copy? (Default None)`
`Elastic Version: 7.0`
`Reading Elastic 6 mappings:`
`Reading index mapping 'es_mappings/silence.json'`
`Reading index mapping 'es_mappings/elastalert_status.json'`
`Reading index mapping 'es_mappings/elastalert.json'`
`Reading index mapping 'es_mappings/past_elastalert.json'`
`Reading index mapping 'es_mappings/elastalert_error.json'`
`New index elastalert_status created`
`Done!`

所以，下一步是创建 `config.yaml`，这是配置 elasticsearch 服务器的文件：

```bash
root@efk:~# cat config.yaml
```

`rules_folder: rules`
`run_every:`
`minutes: 1`
`buffer_time:`
`minutes: 15`
`es_host: 127.0.0.1`
`es_port: 9200`
`writeback_index: elastalert_status`
`writeback_alias: elastalert_alerts`
`alert_time_limit:`
`days: 2`

现在，我们需要创建一个规则。`ElastAlert` 每分钟运行一次查询，检查我们是否有匹配标准的日志。使用以下命令创建一个名为 rules 的文件夹：

```bash
root@efk:~# ls
```

`config.yaml rules`

```bash
root@efk:~# mkdir rules
root@efk:~# pwd
```

`/root`

在 rules 文件夹中，创建一个名为 `alert_404.yml` 的文件，内容如下：

```yaml
es_host: 192.168.99.50
es_port: 9200
name: Alerting 404
type: frequency
index: "*"
num_events: 1
timeframe:
  hours: 24
filter:
- query:
    wildcard:
      log: "404"
alert:
- slack:
    slack_webhook_url: "https://hooks.slack.com/services/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"
```

我在 Slack 上创建了一个工作区，并在其中创建了一个 web hook。如果你想了解更多关于它的信息，稍后可以查看文档。但现在，最重要的是查看它是否正常工作。因此，让我们使用以下命令运行 `ElastAlert`：

```bash
root@efk:~# elastalert --rule rules/alert_404.yml --verbose
```

```bash
1 rules loaded
INFO:elastalert:Starting up
INFO:elastalert:Disabled rules are: []
INFO:elastalert:Sleeping for 9.999665 seconds
```

现在，你可以尝试访问一个不存在的页面，如下所示所示：

![](img/Figure-12.10.jpg)

**图 12.10**

这次访问应该生成一个带有 `404` 状态的日志。你可能在 `ElastAlert` 上看到了这样的日志：

```bash
INFO:elastalert:Queried rule Alerting 404 from 2020-06-30 18:54 UTC to 2020-06-30 18:57 UTC: 2 / 2 hits
INFO:elastalert:Ran Alerting 404 from 2020-06-30 18:54 UTC to 2020-06-30 18:57 UTC: 2 query hits (2 already seen), 0 matches, 0 alerts sent
INFO:elastalert:Background configuration change check run at 2020-06-30 18:57 UTC
INFO:elastalert:Background alerts thread 0 pending alerts sent at 2020-06-30 18:57 UTC
```

这意味着我们的警告正在工作，我应该在 Slack 上收到了通知：

![](img/Figure-12.11.jpg)

**图 12.11**

正如你在前一张图像中看到的，我在 Slack 上收到了带有日志的通知，通过我可以看到错误并检查应用程序正在发生什么。

当然，你可以探索更多 `ElastAlert` 并配置不同类型的告警，例如使用电子邮件。然而，许多公司现在正在从电子邮件转到 Slack 或类似的工具。这就是为什么我用它作为一个例子的原因。

## 结论

本章简要解释了我们如何使用 EFK 栈和 Kubernetes 设置环境。相同的步骤在云端或本地环境中同样适用。整个章节旨在向你简要介绍使用 DevOps 技术栈（DevOps-ologies）可以实现的一切。对于每一章，我们都可以写一整本书。但在我看来，对不同的主题有一个概览是非常重要的，因为你可以思考可以做什么，以及人们在不同情况下正在使用什么。之后，你可以深入研究这里代表的每种解决方案或寻找它们的替代方案。

# 索引

### A
- 高级包工具 (APT) 58-64
- 亚马逊云服务 (AWS)
  - 关于 120
  - 备 121-132
- Apache
  - 安装 64, 65
- autopep8 模块 203
- Azure
  - 关于 121
  - 备 139-143

### B
- Bash 30-34

### C
- CI, 开发阶段
  - 端到端测试 189
  - 集成测试 188, 189
  - 质量测试 189
  - 单元测试 188
- CI, 阶段
  - 开发 188
  - 生产 188
  - 预发布 188
- 云
  - 关于 120
  - 部署 218-222
- code.txt 文件 174
- 命令行界面 (CLI) 31
- Consul
  - 关于 146
  - 参考链接 146
- 持续交付 (CD) 189
- 持续集成 (CI) 188, 189

### D
- Dandified Yum (DNF) 58
- 数据库管理系统 67
- 部署 214
- 目录
  - 管理 35
  - 结构 35, 36
- 发行版 2, 3
- 发行版, Linux
  - 社区企业版操作系统 (CentOS) 3
  - Debian 3
  - RedHat Enterprise Linux 3
  - SUSE 3
  - Ubuntu 3
- Docker
  - 关于 88
  - 容器创建 89-97
  - 使用 Dockerfile 创建 97-99
  - 安装 88
- Docker 服务器
  - 设置 114-117

### E
- EFK 栈
  - 告警创建 235-239
  - Fluentd 运行 227, 229
  - 日志可视化 230-234
  - 设置 224-226
- ElastAlert 235
- Elasticsearch, Fluentd 和 Kibana (EFK) 224

### F
- 文件 203
- Flask 81, 83

### G
- Git 76-80
  - 关于 88
  - 容器创建 89-97
  - 使用 Dockerfile 创建 97-99
  - 安装 88
- GitHub 172, 174, 178, 185
- GNU 76, 80

### H
- HashiCorp 146

### I
- 代码即代码 (IaC) 102

### K
- Kubernetes 212, 213, 214, 215, 218, 222

### L
- LAMP 108
- Linux 111

### M
- MariaDB 68, 70
- 元数据 32
- Minix 2
- 多云 146

### N
- 命名空间 214
- Nginx 76, 80
- Nomad 146

### P
- 包安装 58
- Packer 146
- URL 110
- PEP 333 83
- 个人包存档 (PPA) 63
- PHP 66, 67
- 代码即流水线 190, 209
- Jenkins 流水线 190, 209
- 定义 188
- Pod 214

### V
- VirtualBox 25

# 拉取请求 (PR) 185

### Python
- 安装 81
- 简单页面，使用 `Flask` 创建 81-83

### R
### 反向代理
- 配置 84, 85

### S
- 服务器 4
- 服务 214
- SoftLayer 120

### T
### Terraform
- 关于 146-160, 163, 166, 167, 170
- 参考链接 146

### Ubuntu 服务器
- 参考链接 9

### 用户
- 管理 44-48

### V
### Vagrant
- 关于 102, 146
- 安装 102-104
- 参考链接 102
- 运行 109-111
- 使用方法 104, 105, 107-109
- 工作原理 102

### Vagrant Cloud
- URL 110

### Vault
- 关于 146
- 参考链接 146

### VirtualBox
- 安装 5-9
- 参考链接 5

### W
### Web 服务器网接口 (WSGI) 83
### WordPress
- 安装 70-73

### Y
### Yellow Dog 更新管理器 (YUM) 58
