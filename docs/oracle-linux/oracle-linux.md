
# Oracle Linux 入门指南

![](img/110fa0d6324f0893fff03cee6394144d_0_0.png)

*Robert G. Shimp 序言，*

*Oracle 基础设施软件产品管理高级副总裁*

![](img/110fa0d6324f0893fff03cee6394144d_1_0.png)

献给 Wim Coekaerts、Robert Shimp、Jim Wright 以及 Oracle 产品管理团队，他们致力于让 Oracle Linux 免费下载、免费分发和免费使用。

# 序言

本书旨在对 Oracle Linux 感兴趣、寻求切换到或已选择其作为 IT 基础设施的系统管理员准备的。欢迎！

《Oracle Linux 实战指南》汇集了两位优秀的技术专家（Erik Benner 和 Erik Thomsen），他们提供了丰富的 Linux 诀窍，让你意欲未尽。作者们通过易于遵循的步骤、故障排除技巧和经过测试的最佳实践，分享了他们的共同知识和经验，这些内容可以帮助你采用和管理你的 Oracle Linux 系统。

我有幸认识了 Erik Benner 多年，因为我们都从 20 世纪 90 年代中期起就在 Oracle 工作（我是在 Oracle 工作）。Erik 精通 Oracle 核心技术，包括 Oracle Linux、Oracle Cloud 和 Oracle Database。他在创建、交付和管理基于 Oracle 的解决方案方面的横跨各种规模的政府和商业客户，这意味着在技术实施方面，他处理过几乎能想象的一切——从那些值得米其林星评级的项目，到那些需要拯救的“煮过头”的灾难。

Oracle Linux 团队的成员 Erik B. Thomsen 在美国空军服役期间开始了他的软件职业。在那里，他寻求使用数据库技术来开箱即用的解决问题的方法在全球航空航天公司磨练了自己的技能，他对 Linux 和开源的热情带他到了那里。他曾担任 DBA、产品经理和 DevOps 工程师等职位。Erik 热衷于交付精良的技术解决方案，并通过程序化的文档进行写作，这类似于大师级的食谱。他已在帮助客户简化流程并取得卓越成果方面证明了自己的能力。

Jonathan Spindel 是一位资深的技术专家，他们分享的知识和经验通过易于遵循的步骤、故障排除技巧和经过测试的最佳实践，帮助你采用和管理你的 Oracle Linux 系统。

献给我了不起的父母，你们的爱与牺牲是我生命的基石。你们对我坚定不移的支持和信任激发了我的抱负。我亲爱的妻子，你始终如一的陪伴、爱与鼓励是我在生活风暴之洋中的锚点。我那出色的孩子们，你们是我最大的快乐和灵感。我写下的每一个字、取得的每一项成就，都是献给你们。这本书是为了致敬我心中对你们每一个人无法衡量的爱与感激。感谢你们成为我的坚石、我的光芒以及我梦想的理由。

# 关于评审员

在近十十年里，Avi Miller 曾是 Oracle Linux 的产品经理之一。他的经验涵盖了操作系统、虚拟化和应用栈，曾在小型开发公司和大型企业级硬件及软件供应商商处工作过。如今，他负责 Oracle 云基础设施（OCI）的开源事务工作。在晚上和周末，他对技术的热忱会延伸到通过智能家居升级来烦扰他的丈夫，以及参与社区组织的志愿者服务等更有用的事情。

Satishbabu Gunukula 在广泛的技术领域拥有超过23 年的经验，专长高可用解决方案，例如数据库（Oracle、MS SQL Server、SAP HANA、MySQL 等）、数据分析与可视化（Tableau、SAP、Microsoft 等）、中间件、云（OCI、AWS、Azure）、业务应用（ERP、Hyperion、Agile 等）以及系统管理。他曾为世界500强企业实现过关键业务系统。他荣获了著名的 Oracle ACE Pro 奖以及 2023 世界创新日 Hack 荣誉奖和决赛导师奖。他拥有计算机应用硕士学位，在主要出版物上发表过文章，在 Oracle 相关活动中演讲，并为 PACKT Publishing 出版的五本书进行技术评审。

感谢我的全家人对我提供支持，包容我忙碌的日程，并始终守在我身边。

- 运行原理……
- 准备工作
- 实例文件系统
- 监控
- 运行原理……
- 准备工作
- 运行原理……
- 如何操作……
- 准备工作
- 从基础开始配置和管理 OLAM
- 准备工作
- Ansible 角色创建
- 如何操作……
- Ansible Vault 密钥管理
- 如何操作……
- 使用 Vagrant 搭建完美实验
- 如何操作……
- 容器栈管理
- 如何操作……

# 你可能感兴趣的其他书籍

# 前言

对于寻求稳健、安全且可靠操作系统的组织而言，企业级 Linux 是脱颖出的首选。在 Linux 发行版领域，以 Oracle Linux 和 Rocky Linux 等发行版为代表的企业级 Linux 已赢得了全球企业首选解决方案的声誉。本书探讨了为什么 Oracle Linux 被认为是企业级环境最佳发行版的关键原因，并通过一系列易于遵循、循序渐进的示例（称为“食谱”/recipes）探索了包括 Oracle 发行版在内的多项技术。这些食谱将教你如何在关键领域使用这些技术。

在企业环境中，安全至关重要，Oracle Linux 为强大的安全功能设定了标准。增强型 Linux 安全 (`SELinux`)、强制访问控制以及用于无停机补丁的主动安全补丁系统，共同构建了安全环境。定期的安全审计和及时的停机补丁有助于缓解漏洞，使 Oracle Linux 成为处理敏感和关键任务数据的受信赖选择。

企业级 Linux 发行版的设计旨在实现无缝扩展，无论是在单台服务器还是在大规模集群环境中。集成在这些发行版中的性能优化确保了它们能够处理现代企业应用的需求。Oracle Linux 是性能领域的领导者，提供了使用不可破坏企业内核 (`UEK`) 的选项。本书涵盖了如何安装此选项，并展示了它带来的几项关键功能，例如 `Btrfs` 文件系统。我们还涵盖了可用性，提供了更多关于高可用存储和应用集群的易于的食谱。

Oracle Linux 得益于巨大的软件和应用程序生态系统，这些软件经过了认证并针对性进行了优化。该生态系统包含了数据库管理系统、开发工具、中间件和企业级应用，使得组织更容易构建、部署和管理其软件栈。本书强调了某些支持 DevOps 和 DevSec 团队的技术，例如 `Ansible` 和 `Podman`。

由于其坚如磐石的稳定性、强大的安全功能、可扩展性、全面的支持、对行业标准的遵循以及丰富的生态系统，Oracle Linux 成为企业级环境的最佳发行版。无论是管理关键工作负载、保护敏感数据还是确保高性能计算，企业级 Linux 始终是追求可靠安全操作系统的组织的首选。

# 本书目标读者

本书面向企业级 Linux 管理员，特别是管理 Oracle 企业级 Linux 的管理员。无论你是在从 CentOS 迁移，还是在构建新系统，这本书都充满了实用的技巧和提示。作者的目标是帮助你成为一名更高效的管理员，在你的技能包中增加新的技术，使你能够脱颖而出。

本书也适用于运行在 Oracle Linux 8 上的 Linux 系统管理员和应用程序开发者，因此你应该对 Linux 管理有基础了解，并能够熟练编辑配置文件。

# 如何上手

许多食谱都假设你熟悉 `VirtualBox`。如果你使用的是本书的电子版，请检查链接。为了充分利用本书，请遵循以下步骤。

| 本书涵盖的软件/硬件 | OS |
|---|---|
| Oracle Linux 8 | Oracle Linux |

# 下载示例

你可以从 GitHub 下载示例文件：`https://github.com/PacktPublishing/Oracle-Linux-Cookbook`。如有更新，请查看。

# 约定

书中使用了多种文本约定。

**粗体文本：** 表示代码词、数据库表名、文件夹名、文件名、扩展名、路径名、虚拟 URL。例如：“使用 `.efi` 文件可以获得更多控制。”

代码块格式如下：

```
[ req ]ndef_bits = 4096
distinguished_name = req_distinguished_name
prompt = no
string_mask = utfonly
x509_extensions = extensions
```

当我们需要引起你对代码块某部分的注意时，相关的行或项目将加粗：

```
<Directory>
RewriteEngine %{REQUEST_URI} !=/.well-known/acme-challenge [NC]
RewriteCond %{HTTPS} off
RewriteRule (.*) https://%{HTTP_HOST}/%{REQUEST_URI} [R=301,L]
</VirtualHost>
```

任何命令行输入或输出如下：

```bash
[root@ol18 # grubby --input=/boot/mlinux-0-rescue-c32316cc4b5241b8adb312707ae4644]
```



表示新术语、重要词汇或屏幕上显示的文字。例如，菜单或对话框中的文字在文中显示所示。这是一个例子：`“从菜单中选择 MOK。”`

# 提示或注意事项

显示如下。

# 章节

在书中你会经常遇到几个标题（*准备工作、如何操作...、工作原理、更多...以及另参见*）。

为了清晰地说明如何完成食谱，请如下所示使用这些章节：

## 准备工作

此部分将告诉你食谱的预期内容，以及如何设置食谱所需的任何软件或预备设置。

## 如何操作...

此部分包含遵循食谱所需的步骤。

## 工作原理

此部分通常由对前部分的详细解释组成。

# 更多...

本节包含有关本教程的额外信息，帮助您更深入地了解该教程。

## 另见

本节提供了指向本教程的其他有用信息的链接。

## 联系我们

我们随时欢迎读者的反馈。

**一般反馈：** 如果您对本书的任何方面有任何疑问，请在邮件主题中注明书名，并将邮件发送至 `customercare@packtpub.com`。

**勘误：** 尽管我们尽力确保内容的准确性，但错误在所难免。如果您在书中发现错误，我们将不胜感激地向我们报告。请访问 `www.packt.com/support/errata`，选择您的书籍，点击勘误提交表链接并输入详细信息。

**盗版：** 如果您在互联网上发现任何形式的我们作品的非法副本，如果您能提供位置地址或网站名称，我们将不胜感激。请通过材料链接与 `copyright@packt.com` 联系我们。

**如果您对成为作者感兴趣：** 如果您在某个领域专长，并对编写或为书籍贡献感兴趣，请访问 `authors.packtpub.com`。

## 评论

请留下您的评论。在阅读并使用此书后，为什么不在您购买它的网站上发表评论呢？潜在读者可以参考无偏见的意见做出购买决策，我们 Packt 可以了解您对我们产品的看法，我们的作者也可以看到您对书的反馈。感谢！

有关关于 Packt 的更多信息，请访问 `packt.com`。

## 分享您的想法

一旦您读完《Oracle Linux Cookbook》，我们想听听您的想法！请点击此处直接进入该书的 Amazon 评论页面并分享您的反馈。

您的评论对我们和技术社区都非常重要，并将帮助我们确保交付高质量的内容。

## 下载本书的免费 PDF 副本

感谢购买此书！

您是否喜欢在旅途中阅读，但无法随身携带纸质书？

您的电子书购买是否与您选择的设备不兼容？

别担心，购买每本 Packt 书籍，您都可以免费获得该书的无 DRM PDF 版本。

在任何时间、任何地点、任何任何设备上阅读。直接从您喜欢的技术书中搜索、复制并粘贴代码到您的应用程序中。

优惠不仅于此，您每天可以在收件箱中获得专属折扣、时通讯和精彩内容。

遵循以下简单步骤获取福利：

+ 1. 扫描二维码或访问下方的链接

![](img/110fa0d6324f0893fff03cee6394144d_26_0.png)

`https://packt.link/free-ebook/978-1803249285`

+ 2. 提交您的购买证明

+ 3. 搞定！我们将免费 PDF 和其他福利发送到您的邮箱

# Oracle Linux 8 – 想要就拥有！您终于选择了升级到最安全、最可靠的 Linux 发行版，现在需要学习一些技巧。下一步是什么？如何开始？是时候回到基础并回答一个问题了：如何安装 Oracle Linux？

在过去，安装 Linux 发行版是一项简单任务；只需订购 CD-ROM，插入计算机并从磁盘启动即可。简单……有效……但对许多管理员来说却很痛苦。谁想要买 CD-ROM 呢，或者说，谁还在用 DVD 甚至蓝光光？难道不能直接从网络启动让它变得更复杂吗？当你在云端时会发生什么？CPU 类型（如 Arm 或 x86）又是如何？如何自动化任务？

本章将提供这些问题的见解，并帮助您学习一些自动化 Oracle Linux 的技巧，如果安装未按计划进行，一些故障排除提示。我们将涵盖本章的主要教程：

- Oracle Linux 8 – 哪个 ISO 是正确的？还有人使用 DVD 吗？

- 刻录 ISO 以使其启动

- 一份的价格——在 Windows 的 Linux 子系统 (WSL) 上运行 Oracle Linux

- Arm 拥有未来——不仅仅是树莓派

- 从 Oracle Linux 7 迁移到 8

## 技术要求

书中许多教程的相关配置文件可以在 GitHub 上找到：

`https://github.com/PacktPublishing/Oracle-Linux-Cookbook`.

。

# Oracle Linux 8 – 哪个 ISO 是正确的？还有人使用 DVD 吗？

## 准备工作

在安装 Oracle Linux 时，您必须首先决定如何安装。有多种选择：启动新电脑并加载可安装镜像、从另一个系统克隆驱动器，甚至从网络启动。对于所有这些操作，您都需要正确的介质。尝试使用红帽软件包管理器 (`RPM`) 或错误的架构进行安装是不可行的。在进行任何操作之前，您需要接入互联网以及足够的可用空间来保存 ISO。通常建议至少下载 10 GB 的 ISO。如果您打算使用 `VirtualBox` 运行基于 ISO 的虚拟机，还需要额外的空间。为每个虚拟机分配 100 GB 或更多空间是常见做法，因为这允许您快速扩展文件系统，而无需向卷组添加另一块磁盘。尽管如此，Oracle 的云镜像默认大小为 50 GB，可以适用于许多用户。在云端，使用较小磁盘的优势是降低成本。

> 注意

`RPM` 也被定义为软件包管理器（Package Manager），但这让许多人感到困惑。

## 如何操作

您还需要了解用于安装的硬件设备。将 ISO 刻录到 DVD（或其他光光格式）对于带有这些驱动器的旧系统可能很棒；但现代系统大多数情况下都使用 USB 启动。企业级服务器将此推向了更高级别，允许您从通过网络或虚拟控制台挂载的 ISO 文件进行启动。您还可以从预启动执行环境 (`PXE`) 服务器启动系统，以实现更自动化的网络安装。使用何种方法实际上取决于您的硬件以及您对自动化的需求程度。

> 注意

警惕自动化陷阱。通常，您在自动化安装上花费的时间比手动操作要多得多。在较小的环境中，虽然自动化很美好，但与每年 3-4 次手动构建相比，构建和维护自动化的时间可能需要显著增加。

> 注意

虽然磁盘通常被称为 ISO，但 ISO 文件的实际格式是 ISO 9660 Joliet，这是一种光光介质的格式。ISO 是 [国际标准化组织](https://www.iso.org/home.html) 的实际缩写。ISO 组织成立于 1947 年，拥有各项标准。

获取介质最简单的方法是从 [`https://yum.oracle.com/linux-isos.html`] 下载 ISO。

这里有四种类型的 ISO：

- **Full ISO**：这是 Oracle Linux 的完整安装。该 ISO 包含了安装所需的所有文件，并且可以启动。您可以通过将其刻录到 U 盘或 DVD 来使用它。在许多服务器上，您可以通过管理软件挂载 ISO 进行启动。系统有许多远程控制选项，包括基础功能的智能平台管理接口 (`IPMI`) 以及开源的基板控制器 (`BMC`)。大多数硬件供应商还提供特定技术，例如集成光路 (`ILOM`)、Dell 的集成远程访问 (`iDRAC`) 以及 HP 的集成光路。

- **Boot ISO**：此 ISO 使用红帽兼容内核进行安装并可以启动。它不包含安装所需的所有文件。虽然这个文件小得多，但您需要在网络或本地设备上准备剩余的软件包。您可以通过 HTTP 访问文件，从 `https://yum.oracle.com/` 或本地 HTTP 服务器获取。

> 注意

Oracle Linux 的**不可破坏企业内核 (`UEK`)** 有许多优势，例如启用了 BTFS 文件系统以及与主内核匹配的现代内核，对现代设备的支持更好。

- **uek ISO**：此 ISO 可以启动更现代的 UEK，就像 Boot ISO 一样，它不包含安装所需的文件。安装更现代的 UEK 有帮助，特别是对于那些无法在旧红帽兼容内核 (`RHCK`) 上正确安装的系统。UEK 仅适用于 Arm 架构。

- **Source ISO**：此 ISO 无法启动，但它有用，因为它包含了所有的软件包，允许您审核源代码。

> 注意

对于两种 ISO 选项，介质必须位于网络上的 FTP 服务器、HTTP/HTTPS 服务器或 NFS 服务器上。

此外，有两种 CPU 架构可用。请确保为安装选择正确的架构。让我们来看看它们：

- **x86_64**：这是最常见的架构，适用于 Intel 和 AMD 系统。这包括 Intel X 系列处理器以及 i9、i7、i5 和 i3 处理器。对于 AMD 系统，这包括 AMD EPYC 处理器、Ryzen 处理器，

以及 Athlon 系列。这是最常见的选项，但它在行业内正面临 Arm 选项的挑战。x86 下载站完整选项列表所示：

| 版本 | 完整 ISO | 启动 ISO | UEK 启动 ISO | 源码 ISO |
| --- | --- | --- | --- | --- | ---



| 8.5 | `Oracle_Linux-R8-U5-x86_64.dvd` | `OLU85_x86-64-boot.iso` | `OLU85_x86-64-uek-boot.iso` | `OracleLinux-R8-U5-src-dvd` |

| 8.4 | `Oracle_linux-R8-U4-x86_64.dvd` | `OLU84_x86-64-boot.iso` | `OLU84_x86-64-uek-boot.iso` | `OracleLinux-R8-U4-src-dvd` |

| 8.3 | `Oracle_linux-R8-U3-x86_64.dvd` | `OLU83_x86-64-boot.iso` | `OLU83_x86-64-uek-boot.iso` | `OracleLinux-R8-U3-src-dvd` |

| 7.9 | `Oracle_linux-R7-U9-Server-x86_64.dvd` | `OLU79_x86-64-boot.iso` | `OLU79_x86-64-uek-boot.iso` | `OracleLinux-R7-U9-src-dvd` / `OracleLinux-R7-U9-server-dvd` |

| 7.8 | `Oracle_linux-R7-U8-Server-x86_64.dvd` | `OLU78_x86-64-boot.iso` | `OLU78_x86-64-uek-boot.iso` | `OracleLinux-R7-U8-src-dvd` / `OracleLinux-R7-U8-server-dvd` |

| 7.7 | `Oracle_linux-R7-U7-Server-x86_64.dvd` | `OLU77_x86-64-boot.iso` | `OLU77_x86-64-uek-boot.iso` | `OracleLinux-R7-U7-src-dvd` / `OracleLinux-R7-U7-server-dvd` |

| 6.10 | `Oracle_linux-R6-U10-Server-x86_64.dvd` | `OLU60_x86-64-boot.iso` | `OLU60_x86-64-uek-boot.iso` | `OracleLinux-R6-U10-src-dvd` / `OracleLinux-R6-U10-server-dvd` |

| 6.9 | `Oracle_linux-R6-U9-Server-x86_64.dvd` | `OLU69_x86-64-boot.iso` | `OLU69_x86-64-uek-boot.iso` | `OracleLinux-R6-U9-src-dvd` / `OracleLinux-R6-U9-server-dvd` |

| 6.8 | `Oracle_linux-R6-U8-Server-x86_64.dvd` | `OLU68_x86-64-boot.iso` | `OLU68_x86-64-uek-boot.iso` | `OracleLinux-R6-U8-src-dvd` / `OracleLinux-R6-U8-server-dvd` |

> 图 1.1 – x86_64 ISO

## AArch64

当你在 Arm 服务器上使用 Oracle Linux 时，需要这种版本，例如树莓派或 Ampere 的高性能云原生处理器 CPU。云原生处理器是专为运行云原生应用设计的 CPU 术语，它针对更低的功耗进行了优化，并具有更可扩展的架构。

在 Arm 上运行 Oracle Linux 是一个非常有趣的选项，因为像 Java、Apache、Python 和 Podman 等应用构建块使用与 x86 架构相同的软件版本运行。所有这些构建块的运行方式与它们在 x86 架构上的完全相同，这使得对于采用者切换到 Arm 变得非常容易。Arm 的优势在于成本更低且密度更高，提供了一个极具吸引力的成本/性能故事，使能够在降低成本的同时提高性能。目前从下载站下载 Oracle ISO 的选项如下：

## 可供下载的 arch64 Oracle Linux ISO

| 版本 | 完整 ISO | UEK 启动 ISO | 源码 ISO |
| --- | --- | --- | --- |
| 8.5 | `OracleLinux-R8-U5-Server-arch64-dvd.iso` | `OL8U5 arch64-boot-uek.iso` | `OracleLinux-R8-U5-src-dvd.iso` |
| 8.4 | `OracleLinux-R8-U4-Server-arch64-dvd.iso` | `OL8U4 arch64-boot-uek.iso` | `OracleLinux-R8-U4-src-dvd.iso` |
| 8.3 | `OracleLinux-R8-U3-Server-arch64-dvd.iso` | `OL8U3 arch64-boot-uek.iso` | `OracleLinux-R8-U3-src-dvd.iso` |
| 7.9 | `OracleLinux-R7-U9-Server-arch64-dvd.iso` | `OL7U9 arch64-boot-uek.iso` | `OracleLinux-R7-U9-src-dvd.iso` |
| 7.8 | `OracleLinux-R7-U8-Server-arch64-dvd.iso` | `OL7U8 arch64-boot-uek.iso` | `OracleLinux-R7-U8-src-dvd.iso` |
| 7.7 | `OracleLinux-R7-U7-Server-arch64-dvd.iso` | `OL7U7 arch64-boot-uek.iso` | `OracleLinux-R7-U7-src-dvd.iso` |

> 图 1.2 – Arm ISO

一旦我们了解了平台，就需要决定使用哪个版本。有时你可能需要下载旧版本并验证该版本是否受支持。在编写时，虽然版本 6 可以下载，但支持仅持续 2024 年 6 月。

## 注意

Oracle 的扩展支持允许你支付费用以获得支持，包括关键安全问题和高影响漏洞的修复。此支持不涵盖 RPM。鉴于此，你可能希望考虑下载旧版本的 Oracle Linux。扩展支持的价值在于它可以为需要旧版本 Oracle Linux 的应用程序提供升级时间。主版本之间（7 与 8 等）存在差异。一个例子是 Oracle Linux Automation（基于 AWX 项目和 Tower），需要 Oracle Linux 8。另一个例子是 Oracle Linux Manager（也称为 Foreman），需要 Oracle Linux 7。

## 注意

由于 Oracle Linux 跟踪 Red Hat，主版本和小版本是相同的。Oracle Linux 7.10 与 Red Hat 相同。

## 制作 ISO 以启动

一旦下载了 ISO，你可能需要进行额外的准备。如果你使用 USB 设备安装，仅将文件拷贝到闪盘是不行的，因为 ISO 并没有在介质上解包。如果 ISO 没有正确解包且未质启动，你将无法从介质启动并安装。将 ISO 文件刻入介质的过程会将介质解包为单独的文件和目录，并使其启动。如果没有这样做，介质将只有一个 ISO 文件的副本。

有多种工具可以实现这一点。由于系统不再使用光光，最常见的方法是从闪盘或虚拟磁盘启动服务器。

## 准备工作

在开始之前，你首先需要下载 ISO 镜像。你还需要一个 USB 驱动器，最好空间大于16 GB。随着发行版的增长，8 GB 的驱动器已不足存放完整的安装 ISO。

## 如何操作...

在从闪盘启动之前，你首先需要将 ISO 文件刻入闪盘。在 Windows 系统中，一个常用的免费工具是 `balenaEtcher`，可以从 `https://www.balena.io/etcher/` 下载。采取以下步骤：

- 安装 Etcher 后，你需要运行它（确保右键点击它并以管理员身份运行），并选择镜像文件作为源，闪盘作为目标。

- 在下面的截图中，源是 x64 的 Oracle Linux 8.7，目标是一个闪盘：

![](img/110fa0d6324f0893fff03cee6394144d_32_0.png)

> 图 1.3 – 使用 Etcher 选择源和目标

- Etcher 可以自动处理压缩文件，因此（如下截图所示），你应该有一个安装了镜像并准备好启动的闪盘：

![](img/110fa0d6324f0893fff03cee6394144d_33_0.png)

> 图 1.4 – balenaEtcher 刻入 ISO

## 注意

使用闪存设备时，请注意廉价品牌。通常，无品牌卡的性能远低于名牌卡。此外，在在线购买时，要警惕假卡。务必从信誉良好的供应商处购买闪存设备。

## 工作原理

一旦你将 ISO 文件刻入闪盘，你就可以从介质启动服务器。如何从 USB 设备启动取决于系统的型号和品牌。x86 系统在其基础输入/输出系统 (BIOS) 中有一项设置允许你从新刻录的介质启动。Arm 系统通常使用统一扩展固件接口 (UEFI) 固件从 ISO 或 USB 内存启动。

## 买一送一——在 Windows 的 Linux 子系统 (WSL) 上运行 Oracle Linux



还有最后一种在 Microsoft Windows 桌面上安装 Oracle Linux 的方法，即使用 WSL。

WSL 让你能够直接在 Windows 上安装 Oracle Linux，而无需安装如 VirtualBox 这样的传统虚拟机。WSL 包含一个为 Windows 预配置的集成虚拟机，向用户隐藏了虚拟机监控程序。WSL 的另一个优势是可以直接从 Windows 运行 Linux 命令，包括 Apache、MySQL、SSHD、Nginx 和 PostgreSQL 等 Linux 服务。

## 准备工作

在开始之前，你需要一个连接了互联网的 Windows 10 或 Windows 11 系统。你还需要该系统的本地管理员权限。这并不是一个困难的操作，非常值得花时间。

## 如何操作...

安装 WSL 非常简单。你需要执行以下步骤：

- 1. 以管理员身份启动“命令提示符”。不要忘记右键点击“命令提示符”并选择“以管理员身份运行”，如下截图所示：

虽然这些说明是针对 WSL 的，但请注意它们实际上涵盖的是 WSL2。WSL 有一个早期的版本也称为 WSL1，它的工作方式略有不同，且不再被使用或部署。应避免使用旧版本的 WSL。操作系统版本也是如此；尽可能使用最新的 8.X 版本。

- 2. 在命令提示符中运行 `wsl.exe --install` 命令。这将启动多个任务，包括安装支持 WSL 运行的 Microsoft 虚拟机平台、安装 WSL 子系统本身以及安装一个 Ubuntu Linux 发行版。

一旦安装完成，如下所示所示，Windows 需要重启。

![](img/110fa0d6324f0893fff03cee6394144d_36_0.png)

图 1.6 – WSL 安装

- 3. 一旦你的系统已备份，我们将安装 Oracle Linux 8.5 作为 WSL 使用的 Linux 操作系统。执行此操作，请启动“微软商店”应用并在搜索栏中搜索 Oracle Linux：

![](img/110fa0d6324f0893fff03cee6394144d_36_1.png)

图 1.7 – 在微软商店中搜索 Oracle Linux 8.5

- 4. 在搜索结果中，选择 Oracle Linux 8.5 应用。这将带你进入可以在 WSL 下下载并安装 Oracle Linux 8.5 的界面：

## 截图

![](img/110fa0d6324f0893fff03cee6394144d_37_0.png)

### Description

Oracle Linux 将现代 IT 基础设施的基础构建模块：操作系统、容器和虚拟化集成到一个整体方案中。Oracle Linux 提供了可靠性、扩展性、安全性和性能，适用于运行的 SaaS、PaaS 以及传统的企业工作负载。

对于希望在 Windows 环境中运行 Linux 软件并将 Windows 应用与 Linux 结合使用的开发者来说，Oracle Linux 是理想的选择。Oracle Linux 易于下载，且使用、分发和更新完全免费。

通过 Oracle Linux，你可以构建没有限制性合同的现代基础设施，并拥有灵活的企业级支持选项。Oracle Linux Support 以低廉的价格提供屡奖的 Oracle 支持资源和支持专家。

显示更多

### 评分和评论

#### 5.0

1 个评分

图 1.8 – 微软商店中的 Oracle Linux 8.5

- 5. 点击`获取`按钮。这将开始为 Windows 系统下载并安装 Oracle Linux 8.5。下载仅需几分钟，完成后你就可以运行 Oracle Linux 8.5。然而，在将来，你需要通过在程序列表中搜索、按下 `Windows` 键并输入 `Oracle Linux` 来运行 Oracle Linux 8.5 子系统。这不仅可以找到子系统，还可以让你将子系统固定到任务栏或开始菜单，如下截图所示：

# Oracle Linux 8.5 应用

在网络搜索

- oracle linux - 查看网络结果
- oracle lighting
- oracle linux
- oracle live sql

文件夹

- Oracle Linux Book
- U_Oracle_Linux_8_V1R_STIG (1)
- U_Oracle_Linux_8_V1R_STIG - 在下载内存中
- U_Oracle_Linux_8_V1R_STIG - 在下载内存

oracle linux 8.5

# Oracle Linux 8.5 应用

- 打开
- 以管理员身份运行
- 固定到开始屏幕
- 固定到任务栏
- 应用设置
- 评分并评论
- 分享
- 卸载

![](img/110fa0d6324f0893fff03cee6394144d_38_0.png)

图 1.9 – Oracle Linux 8.5 子系统选项

- 6. 当你运行 WSL 子系统时，它的运行与任何其他 Oracle Linux 8.5 系统几乎相同。你现在可以轻松地在 Windows 下运行 Oracle Linux 命令。这包括检查存储容量、使用 `dnf` 安装程序、编辑文件以及 `SSH` 到其他主机：

```
[root@NOT-A-DELL~]$ uptime
23:18:34 up2 min, 0 users, load average: 0.00, 0.00, 0.00
Filesystem      Size Use Available Mounted on
/dev/shm       256 0 256 /dev
tmpfs           256 0 256 /run
tmpfs           1.97G 0 2.0G /dev/shm
tmpfs           256M 0 256M /dev
tmpfs           1.0G 0 1.0G /run/user
tmpfs           1.97G 0 2.0G /dev/group
tmpfs           1.97G 0 2.0G /sys/fs
sda             53G 14G 38G 27% /
[root@NOT-A-DELL~]$ uname -a
Linux-NOT-A-DELL.8.16-microsoft-wsl2 SMP Apr 2 23:49 UTC 2021 x86_64
[root@NOT-A-DELL~]#
```

img/110fa0d6324f0893fff03cee6394144d

当你运行 WSL 子系统时，它的工作方式与任何其他 Oracle Linux 8.5 系统几乎相同。你现在可以在 Windows 下轻松运行 Oracle Linux 命令。这包括检查存储容量、使用 `dnf` 安装程序、编辑文件以及 `SSH` 到其他主机：

```
[root@NOT-A-DELL~]$ uptime
23:18:34 up2 min, 0 users, load average: 0.00, 0.00, 0.00
Filesystem      Size Use Available Mounted on
/dev/shm       256 0 256 /dev
tmpfs           256 0 256 /run
tmpfs           1.97G 0 2.0G /dev/shm
tmpfs           256M 0 256M /dev
tmpfs           1.0G 0 1.0G /run/user
tmpfs           1.97G 0 2.0G /dev/group
tmpfs           1.97G 0 2.0G /sys/fs
sda             53G 14G 38G 27% /
[root@NOT-A-DELL~]$ uname -a
Linux-NOT-A-DELL.8.16-microsoft-wsl2 SMP Apr 2 23:49 UTC 2021 x86_64
[root@NOT-A-DELL~]#
```

你也可以使用 `dnf` 安装新软件。下图中了安装 `nmap` 的示例：



```
erik@NOT-A-DELL~$ sudo -
last login: root@NOT-A-DELL at 23:50:16 on Sat 5 23:50:30
root@NOT-A-DELL# dnf install nmap -y
Last metadata date: 0:00:32 ago on Sat 5 23:50:32.
Dependencies resolved:
**********************************
Package                Architecture      Version                Size
**********************************
Installing:             x86_64              2.70-6.el8           ol8_appstream         5.8 M
umata                  noarch               0.34-10.el8          ol8_bases_latest      1.7 M
libnports              x86_64              35.0-1.el8          ol8_bases_latest      335 K
db3                   x86_64              35.0-1.el8          ol8_bases_latest      323 K
nmap                   x86_64              16.1-5.el8          ol8_bases_latest      249 K
ciutils               x86_64              2.70-6.el8           ol8_appstream         237 K
openssl-libs          x86_64              3.7-1.el8           ol8_bases_latest      54 K
rdma-core             x86_64              35.0-1.el8          ol8_bases_latest      59 K
**********************************
Transaction Summary
```

![](img/110fa0d6324f0893fff03cee6394144d_39_0.png)

你可以从 WSL 访问你的 Windows 磁盘。它们将以 `/mnt/DRIVE` 的形式呈现，其中 c: 盘是 `/mnt/c`。Windows 系统也可以访问 `\\OracleLinux_0_5` 路径下的 Linux 目录：

![](img/110fa0d6324f0893fff03cee6394144d_40_0.png)

## 注意事项

请注意，在编辑文件时要务必小心。Windows 和 Linux 的文本格式不同，如果你不小心，很容易损坏文件。建议使用 Windows 存储和访问 Windows 文件，并在 WSL 镜像上编辑和存储 Linux 文件。

将 Oracle 8.5 作为 Windows 子系统运行对于系统管理员和开发人员来说是一个很棒工具。它与 Windows 的集成使其安装既快捷方便，同时可以在你的个人系统中透明地访问 Linux 系统。

## 为 IT 的未来做准备——这不仅仅是一块树莓派

首先，让我们谈谈在高级 RISC 机器（通常称为 Arm CPU）上的 Oracle Linux。这种新架构相比 Intel 等使用的旧版 `x86_64` 架构具有许多优势

AMD 的使用。这包括更低的功耗；更低的延迟，带来了更好的性能；以及简化的架构，实现了更高密度的系统。在 Arm 系统上利用 Oracle Linux 对于像 Oracle 和微软这样的云端规模运营商，以及正寻求减少计算算力和冷却需求的较小规模组织来说，这都是一个热门选择。

在所有 Linux 系统上使用简单的企业级操作系统有许多优势，例如在所有服务器上使用相同的工具，并可以为您的服务器获得相同的商业支持。在您的服务器库存中，Arm 的用例也很有趣。从整体而言，Arm 处理器由于其具有更高的潜在核心密度和更低的功耗，提供了更低的成本。在企业领域，Ampere 占据主导地位，并在单个机架单元（RU）空间内在单个芯片上提供高达 128 个核心的 Arm 处理器。

性能也毫不逊色，每个系统在两个 RU 的空间内即可支持高达 128 个核心，每个核心的 CPU 频率高达 3.0 GHz。I/O 性能同样强大，拥有 128 条高速 PCIe Gen4 通道和 8*7 ECC 保护的 DDR4 3200 内存。配合 64 GB 的内联内存模块（DIMMs），在小型外形规格下就拥有 4 TB 的内存！这些企业级系统具备了 Oracle Linux 的所有动力、安全性和可靠性。

Arm 不仅用于数据中心；当您需要小型系统时（例如 DNS 服务器或远程访问设备），有著名的树莓派（Raspberry Pi），它由于其小巧的尺寸非常适合隐藏在布线间内作为备份 DNS 服务器，或放置在 Oracle Exadata 机箱内部实现远程访问。你可以将树莓派作为监控系统或 DMZ 中的 Web 服务器。

无论你运行在何种 Arm 平台上（Ampere 或树莓派），当运行 Oracle Linux 时，你也可以获得带有增强功能的 UEK（无人升级内核），其中包含 Ansible 等工具。Oracle Linux 以一个支持的价格包含了所有主要技术，而且你始终可以选择免费使用它；你可以免费打补丁。在 Arm 方面，该平台也不受限制。你可以使用如 MySQL 8.0 等商业软件，还有大量的开源软件。

强大的不仅仅是树莓派的案例。当你接触较大的基于 Arm 的服务时，你将获得大量的边缘计算用例。边缘计算需要应用程序将数据从云端带到需要低延迟访问的地方。通过 MySQL 8.0 的复制功能，你可以轻松地将数据从云端复制到边缘，保持性能的同时，利用 Ampere 等公司制造的 Arm 系统的高核心数和低功耗需求（Ampere 提供了一个 80 核心且功耗仅为 210w 的 CPU）。高核心数结合 Docker 和 Kata 等容器技术实现了分布式微服务架构，通过集中维护的应用程序在利用云端自动化的同时，仍然提供传统本地解决方案的性能。这就是 IT 的未来。

## 准备工作

在开始之前，你需要一个带有 Micro SD 卡槽的树莓派。你还需要一张可以用于安装操作系统的 Micro SD 卡。如果你使用的是树莓派计算模块（compute module）或企业级 Arm（如 Ampere 系统），请跳到第 2 章并使用 PXE 启动系统。

## 如何操作...

话虽如此，让我们在树莓派上安装 Oracle Linux。虽然我一直在 Arm 上使用 Oracle Linux 并通过这种硬核的方式进行安装，但现在有更简单的方法来安装它。Oracle 为树莓派提供了免费的镜像，其中已经安装了操作系统。

让我们采取以下步骤：

- 1. 在以下链接下载 Oracle 镜像：`https://www.oracle.com/linux/downloads/linux-arm-downloads.html`。
- 2. 接下来，你需要将镜像写入 SD 卡。在 Windows 系统上，最简单的方法是使用 `balenaEtcher`，它是一个免费工具，可以轻松地将镜像写入 SD 卡和 USB 驱动器。你可以从 `https://www.balena.io/etcher` 下载它。

### 注意

虽然示例使用了 `balenaEtcher`，但还有许多其他方法可以将文件写入闪存盘，例如 Raspberry Pi Imager，或者直接在 Linux 中使用 `dd` 命令将文件写入闪存。

- 3. 运行 `Etcher`（确保右键点击它并以管理员身份运行），选择镜像文件作为源，选择 SD 卡作为目标。

![](img/110fa0d6324f0893fff03cee6394144d_43_0.png)

`Etcher` 可以自动处理压缩文件，因此在一分钟或两分钟后，你就应该拥有一个安装好镜像的 SD 卡了。

- 4. 接下来，将卡插入你的树莓派并启动。正常的 GRUB 加载程序将启动，你应该会看到登录提示符。

Oracle Linux Server 8 (5.15.0-3.60.5.1.e18uk.aarch64)

System setup

图 1.14 - 启动树莓派

是的，这很简单！

- 5. 一旦启动，以 root 身份登录，密码为 `oracle`。系统将要求你更改密码。



```
Oracle Linux Server 0.7
Kernel 5.15.0-3.60.5.1.e18uk.aarch64 on an aarch64
rpi login: root
Password:
You are required to change your password.

Current password:
New password:
Retype password:
[root@rpi ~] Linux 5.15.0-3.60.5.1.e18uk.aarch64 #32 Wed Oct 19 17:59 GMT 2022 aarch64
```

6. 现在，你根据想要安装的应用程序来使用 Oracle Linux 8。默认情况下，`Leapp` 就能正常工作。

7. 对于 Oracle Linux 8，你可以访问以下仓库：

- BaseOS Latest：基础 OS 工具。
- AppStream Latest：包含用户应用程序。
- EPEL：企业 Linux 附加软件包。EPEL 可以通过以下内容添加到 `/etc/yum.repos.d/` 中手动添加：

```
[epel]
name=Oracle Linux 8 EPEL ($basearch)
baseurl=https://yum.oracle.com/repo/OracleLinux/EPEL/$basearch
gpgkey=file:///etc/pki/rpm-gpg/KEY-oracle
gpgcheck=1
enabled=1
```

EPEL 也可以使用 `dnf` 安装：

```
dnf install oracle-linux-release
```

花几分钟在树莓派上玩玩吧。

| 平台说明 | 起内核 (Oracle Linux 7) | 结束内核 (Oracle Linux 8) | 是否支持 |
| --- | --- | --- | --- |
| | UEK | UEK | 是 |
| | UEK | RHCK | 否 |
| AArch64 | UEK | UEK | 是 |

表 1.2 – 来自 Oracle 的支持内核升级

## 在 Leapp 之前务必检查

在从版本 7 升级到 8 之前，你需要检查以下几项内容：

- 确保你有一份可靠的备份。在操作不顺利的情况下，系统快照（Snapshots）效果最好。
- 如果启用了安全启动（Secure Boot），请使用 `mokutil --sb-state` 将其禁用。你可以通过运行 `bootctl status` 命令检查状态。
- 确保你拥有控制台访问权限，以便在需要时排除故障。
- 禁用任何网络挂载，例如 NFS 挂载、Samba 挂载、ClusterFS 挂载等。在你的 `/etc/fstab` 文件中禁用它们。
- 如果你正在使用 `yum-plugin-versionlock`，请使用 `yum versionlock clear` 命令清除任何锁定。
- 如果你正在运行任何 KVM，请停止它们。你可以使用 `virsh shutdown $VM_NAME`。如果你不确定是否正在运行任何虚拟机，`virsh list --all` 命令将为你列出所有虚拟机。
- 如果你正在使用 Spacwalk、Oracle Linux Manager、Unbreakable Linux Network (ULN) 或任何其他集中 yum 管理器，请从那里注销系统。你必须使用 `yum.oracle.com` 仓库进行 Leapp 升级。
- 如果你需要 HTTP 代理来访问 `yum.oracle.com` 仓库，请确保已将其添加到 `/etc/yum.conf` 中。
- 验证你在 `/etc/locale.conf` 中使用的是 `en_US.UTF-8`。你可以通过 `localectl set-locale LANG=en_US.UTF-8` 命令进行切换。
- 在你的 `/etc/ssh/sshd_config` 文件中验证你可以以 root 身份登录。配置文件应包含 `PermitRootLogin yes`。

一旦你验证了此列表，再次使用 `yum update -y` 补丁你的系统 `yum.oracle.com` 源，然后重启。

最后，你可以通过以下命令添加 Leapp 仓库：

```
yum install -y leapp --enablerepo=ol7_leapp_latest
```

接下来，再次重启，并可能再进行第二次备份。重启后，如果你使用代理访问这些仓库，则需要为 `/etc/yum.repos.d/leapp-upgrade-repos-ol8.repo` 中的每个仓库条目添加代理服务器。你可以使用简单的 `sed` 命令完成此：

```bash
sed -i '/^enabled=0.*/a proxy=http://proxy-host:proxy-port/' /etc/yum.repos.d/leapp-upgrade-repos-ol8.repo
```

恭喜你，你现在准备好分析系统了！

## 如何操作...

你需要采取以下步骤：

1. 如果你运行在 Oracle 云（称为 OCI）以外的任何地方，你可以运行以下命令生成报告：

```bash
leap preupgrade --oracleinux
```

2. 如果你在 OCI 上，运行此命令：

```bash
leap preupgrade --oci
```

这两个命令都会运行许多检查，并在发现严重问题时发出警报。但你需要深入研究这些内容：

```
===> check_skip_phase
跳过所有后续阶段，直到报告阶段。
===> Processing phase 'Reports'
===> verify_check_results
检查所有对话框并通知用户需要做出选择。
===> verify_check_results
检查所有生成的生成消息并通知用户相关信息。
```

```
==========================================
升级被阻止
==========================================
```

由于以下问题，升级被阻止：

1. 阻止因素：使用 root 账户远程登录时问题
2. 阻止因素：答案文件中缺少必要的回答

请咨询升级前报告以获取详情和可能的修复方法。

```
==========================================
升级被阻止
==========================================
```

```
调试输出已写入 /var/log/leapp/leapp-preupgrade
============================================
```

## 报告

报告已在 `/var/log/leapp/leapp-report.json` 生成

报告已在 `/var/log/leapp/leapp-report.txt` 生成

```
==========================================
报告结束
==========================================
```

答案文件已在 `/var/log/leapp/answerfile` 生成

(img/110fa0d6324f0893f0cee6394_0.png)

3. 现在你应该会有一些有趣的输出。`/var/log/leapp/leapp-report.txt` 文件将识别升级中的任何风险。这些风险按排名分类，最高的是阻断项（stopper）。处理任何风险后，重新运行。

4. 在你的 `/etc/ssh/sshd_config` 文件中，验证你可以以 root 身份登录。`PermitRootLogin yes` 应该在配置文件中。

一旦你验证了此列表，再次使用 `yum update -y` 补丁你的系统 `yum.oracle.com` 源，然后重启。

最后，你可以通过以下命令添加 Leapp 仓库：

```
yum install -y leapp --enablerepo=ol7_leapp_latest
```

接下来，再次重启，并可能再进行第二次备份。重启后，如果你使用代理访问这些仓库，则需要为 `/etc/yum.repos.d/leapp-upgrade-repos-ol8.repo` 中的每个仓库条目添加代理服务器。你可以使用简单的 `sed` 命令完成此：

```bash
sed -i '/^enabled=0.*/a proxy=http://proxy-host:proxy-port/' /etc/yum.repos.d/leapp-upgrade-repos-ol8.repo
```

恭喜你，你现在准备好分析系统了！

## 如何操作...

你需要采取以下步骤：

1. 如果你运行在 Oracle 云（称为 OCI）以外的任何地方，你可以运行以下命令生成报告：

```bash
leap preupgrade --oracleinux
```



## 如果你在 OCI 上，运行此命令

```bash
leap preupgrade --oci
```

这两个命令都会运行许多检查，并在发现严重问题时发出警报。但你需要深入研究这些内容：

```
===> check_skip_phase
跳过所有后续阶段，直到报告阶段。
===> Processing phase 'Reports'
===> verify_check_results
检查所有对话框并通知用户需要做出选择。
===> verify_check_results
检查所有生成的生成消息并通知用户相关信息。
```

```
==========================================
升级被阻止
==========================================
```

由于以下问题，升级被阻止：

1. 阻止因素：使用 root 账户远程登录时问题
2. 阻止因素：答案文件中缺少必要的回答

请咨询升级前报告以获取详情和可能的修复方法。

```
==========================================
升级被阻止
==========================================
```

```
调试输出已写入 /var/log/leapp/leapp-preupgrade
============================================
```

## 报告

报告已在 `/var/log/leapp/leapp-report.json` 生成

报告已在 `/var/log/leapp/leapp-report.txt` 生成

```
==========================================
报告结束
==========================================
```

答案文件已在 `/var/log/leapp/answerfile` 生成

(img/110fa0d6324f0893f0cee6394_0.png)

3. 现在你应该会有一些有趣的输出。`/var/log/leapp/leapp-report.txt` 文件将识别升级中的任何风险。这些风险按排名分类，最高的是阻断项（stopper）。处理任何风险后，重新运行。

4. 在你的 `/etc/ssh/sshd_config` 文件中，验证你可以以 root 身份登录。`PermitRootLogin yes` 应该在配置文件中。

一旦你验证了此列表，再次使用 `yum update -y` 补丁你的系统 `yum.oracle.com` 源，然后重启。

最后，你可以通过以下命令添加 Leapp 仓库：

```bash
yum install -y leapp --enablerepo=ol7_leapp_latest
```

接下来，再次重启，并可能再进行第二次备份。重启后，如果你使用代理访问这些仓库，则需要为 `/etc/yum.repos.d/leapp-upgrade-repos-ol8.repo` 中的每个仓库条目添加代理服务器。你可以使用简单的 `sed` 命令完成此：

```bash
sed -i '/^enabled=0.*/a proxy=http://proxy-host:proxy-port/' /etc/yum.repos.d/leapp-upgrade-repos-ol8.repo
```

恭喜你，你现在准备好分析系统了！

## 如何操作

你需要采取以下步骤：

1. 如果你运行在 Oracle 云（称为 OCI）以外的任何地方，你可以运行以下命令生成报告：

```bash
leap preupgrade --oracleinux
```

2. 如果你在 OCI 上，运行此命令：

```bash
leap preupgrade --oci
```

这两个命令都会运行许多检查，并在发现严重问题时发出警报。但你需要深入研究这些内容：

```
===> check_skip_phase
跳过所有后续阶段，直到报告阶段。
===> Processing phase 'Reports'
===> verify_check_results
检查所有对话框并通知用户需要做出选择。
===> verify_check_results
检查所有生成的生成消息并通知用户相关信息。
```

```
==========================================
升级被阻止
==========================================
```

由于以下问题，升级被阻止：

1. 阻止因素：使用 root 账户远程登录时问题
2. 阻止因素：答案文件中缺少必要的回答

请咨询升级前报告以获取详情和可能的修复方法。

```
==========================================
升级被阻止
==========================================
```

```
调试输出已写入 /var/log/leapp/leapp-preupgrade
============================================
```

### 报告

报告已在 `/var/log/leapp/leapp-report.json` 生成

报告已在 `/var/log/leapp/leapp-report.txt` 生成

```
==========================================
报告结束
==========================================
```

答案文件已在 `/var/log/leapp/answerfile` 生成

(img/110fa0d6324f0893f0cee6394_0.png)

3. 现在你应该会有一些有趣的输出。`/var/log/leapp/leapp-report.txt` 文件将识别升级中的任何风险。这些风险按排名分类，最高的是阻断项（stopper）。处理任何风险后，重新运行。

4. 在你的 `/etc/ssh/sshd_config` 文件中，验证你可以以 root 身份登录。`PermitRootLogin yes` 应该在配置文件中。

一旦你验证了此列表，再次使用 `yum update -y` 补丁你的系统 `yum.oracle.com` 源，然后重启。

最后，你可以通过以下命令添加 Leapp 仓库：

```
 install -y leapp --enablerepo=ol7_leapp_latest
```

3. 如果你使用 SELinux，你需要使用 `setenforce enforcing` 命令将其设回强制（enforcing）模式。你也可以通过 `getenforce` 命令检查 SELinux 的当前状态。

4. 如果你有正在运行的 KVM 虚拟机，你需要使用 `virsh start $VMNAME` 命令重启它们。

5. 你可以删除 `/root/tmp_leappy_py3` 目录。这是可选的，但可以释放磁盘空间。

6. 你可以重新连接到你的常规补丁和管理系统。它们应该作为 Oracle Linux 8 系统被添加回来。请验证你的管理软件是否反映了新版本；并非所有的管理系统都能正确更新版本。

## 从 CentOS 迁移到 Oracle Linux

第一个问题是：为什么？我们为什么要讨论将 CentOS 迁移到 Oracle？

在解释此之前，让我们来聊聊关于 IBM Red Hat 在 2020 年 12 月 8 日放弃 CentOS 的惊人消息。我们所知的 CentOS 已经死了！它等同于 `/dev/null`。

2020 年 12 月 8 日，CentOS（由 IBM Red Hat 控制）宣布了这一消息：“CentOS 8 作为 RHEL 的重新构建，将在 2021 年底结束。”2021 年这个日期比计划早了八年，2029 年是 CentOS 8 发行版停止开发的原始发布日期。这意味着如果你在使用 CentOS 8 并且想要继续使用稳定且可预测的发布，那么你需要做出更改。

CentOS 团队正在“将重心从 CentOS Linux（Red Hat Enterprise Linux (RHEL) 的重新构建）转向 CentOS Stream，后者的版本领先于当前的 RHEL 发布”。还记得 Fedora 吗？在那里新技术不断被引入和撤回，变化是常态且预料之中的？这基本上就是社区看待 CentOS Stream 的方式。这一变化基本上破坏了企业级系统管理员在生产、开发、测试和质量保证（QA）环境中使用 CentOS 8 及更高版本的能力。



那么，接下来是什么？有几个项目分叉或克隆了 CentOS 模型，以复制这种努力并提供一个跟踪 RHEL 的稳定发行版，具有可预测的发布计划和稳定的组织来支持该项目。在众多项目中选择正确的一个时，你应该担心的问题是：不知道哪些新发行版会失败或成功。其中一些分叉版本可能需要多年才能稳定，而用户现在就需要解决方案。作为管理员，你不需要一个可能会改变方向的分叉或不成熟的发行版。你需要一个目标是与 RHEL 兼容的稳定发行版。Oracle Linux 提供了这种稳定性，并积极通过 Enterprise Linux Association (`OpenELA.org`) 维护 RHEL 的兼容性。`OpenELA` 由 Oracle、SUSE 和支持 RockyLinux 的一些公司共同创立。`OpenELA` 是一个构建与 RHEL 兼容代码的贸易协会，允许开源社区汇聚力量成为 CentOS 的稳定替代方案。

## 我们已经知道 CentOS 了，你看过 Oracle Linux 吗？

Oracle Linux 跟踪 RHEL，使用 `OpenELA` 作为基础，Oracle Linux 8.3 基本上与 RHEL 8.3 或 CentOS 8.3 或 RockyLinux 8.3 相同。它被全球 86% 的财富企业使用，是企业领域最流行的 Linux 选项之一。由于 Oracle 运行业务和云端，无论 IBM Red Hat 发生了什么，你知道它将获得支持。我提到过 Oracle Linux 是免费的吗？它是免费下载、免费分发的！为了进行补丁更新，你需要注册系统或支付任何费用，并且它也是免费下载的！是的，Oracle 提供了一种比 RHEL 便宜得多的付费支持，但由于免费的下载和补丁模型，你可以轻松在非生产系统中使用 Oracle Linux，而且自 2006 年以来，它一直非常稳定。他们甚至支持树莓派（Raspberry Pi），如果你不想从 `http://yum.oracle.com/linux-isos.html` 下载。

如果你支付付费支持，可以获得许多在 RHEL 之上的酷功能，这包括以下几项技术：

- `Ksplice`：允许你在运行时修复内核和用户空间。
- `DTrace`：来自 Solaris，提供内核和应用程序接口的实时视图。
- `Enterprise Manager`：用于管理和监控操作系统、日志等。

如果你在 CentOS 上，迁移到 Oracle Linux 非常简单。最好的方法是迁移并保留一切，让你的应用程序继续运行。Oracle Linux 跟踪 RHEL，使其成为一个无缝的替换。你可以从以下 GitHub URL 访问迁移脚本：`https://github.com/centos2ol`。

## 准备工作

在开始之前，你需要一个运行 Scientific Linux 7.x 和 8.x、Rocky 8.x 以及 CentOS 7.x 和 8.x 的系统。如果你的 CentOS 系统是 CentOS Stream，脚本将无法工作。在运行 Oracle 之前有几点考虑：

- 确保你的系统不是 CentOS Stream。
- 确保你有至少 5GB 的可用空间。
- 备份你的系统。
- 确保你有网络访问。
- 检查你的系统未到终止寿命（EOL）。
- 确保你有稳定的连接。
- 检查是否有冲突。
- 确保你没有使用 Rocky Linux。
- 检查是否有最新版本。
- 确保你没有使用代理。
- 检查你没有使用快照。
- 确保你没有使用集群。
- 检查你没有使用特定的版本。

现在准备好了 CentOS，请按照以下步骤操作：

1. 简单的方法是从此处下载：`https://github.com/centos2ol`

2. 接下来，使用以下命令准备 CentOS-8：

```bash
sed -i 's|#mirrorlist|mirrorlist|g' /etc/yum.repos.d/CentOS-*
sed -i 's|baseurl=http://centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*
```

3. 接下来，使用以下命令脚本：

```bash
root@centos8 ~# ./centos2ol.sh
检查所需的软件包...
检查发行版...
未安装 epel-release
检查内核...
检查所需的 Python 软件包...
正在识别要启用的模块...
正在学习哪些仓库...
已启用仓库：
appstream
base
centos-os-latest
epel
powkg
运行 yum-check-update...
上一次事务检查：6:42 秒前，2022年3月13日 星期日 21:56:29
已移除依赖项。
```

| 包名 | 版本 | 仓库 | 大小 |
| :--- | :--- | :--- | :--- |
| dnf | noarch | 4.0.21-3.el8 | baseos | 73 k |
| epel-dnf-core | noarch | 4.0.21-3.el8 | baseos | 73 k |
| python3-dnf-core | noarch | 4.0.21-3.el8 | baseos | 238 k |

4. 接下来，运行以下脚本：

```bash
root@centos8 ~# ./centos2ol.sh
检查所需的软件包...
检查发行版...
未安装 epel-release
检查内核...
检查所需的 Python 软件包...
正在识别要启用的模块...
正在学习哪些仓库...
已启用仓库：
appstream
base
centos-os-latest
epel
powkg
运行 yum-check-update...
```

一旦重启完成且服务器启动，你可以通过查看 `/etc/oracle-release` 和使用 `uname -r` 内核内核来完成升级。

```bash
root@centos8 ~]# more /etc/oracle-release
Oracle Linux Server release 8.5
root@centos8 ~]# uname -r
5.4.17-2136.304.4.5.el8uek.x86_64
```

# 工作原理

脚本将你的系统连接到新的补丁仓库，然后基本上针对 Oracle 执行扩展补丁。旧的 RPM 包将被 Oracle 的 RPM 包替换。脚本还可以将你从旧的 Linux 4.x 内核升级到 UEK，从中你可以从较新的 Linux 5 内核的性能优势。

# 使用自动化或不使用自动化进行安装

当你手动从 USB 或 ISO 镜像安装 Oracle Linux 时，在企业级，更常见的方法是自动化安装。本章末尾的附录 – kickstart 选项涵盖了手动安装，当你在偶尔需要安装时，这种方法更容易操作。

大多数数据中心的安装过程都使用自动化方法，因为这允许你快速扩展规模。

本章提供了构建可运行的预启动执行（PXE）环境的不同配方。

PXE 启动是由 Intel 开发的一项技术。它允许具有适当 ISO（或 OS RPM）的系统从网络启动，从服务器下载所有所需文件。虽然有较旧的方法（例如引导引导协议 BOOTP），但行业已迅速采用 PXE 启动作为最常用的标准。虽然 PXE 启动始于 Intel 系统，但 ARM 系统也可以使用 TFTP 。为了让 PXE 启动过程正常工作，你通常需要在网络上拥有一个 DHCP 服务器和一个 PXE 服务器。该过程的高级概述见下面的图：

![](img/110fa0d6324f0893fff03cee6394144d_56_0.png)

图 2.1 – PXE 启动过程

以下是每个步骤的高级描述：

- 1. PXE 客户端将从可用的 DHCP 服务器请求 IP 地址。
- 2. 网络上第一个响应客户端的 DHCP 服务器将为其提供 IP 地址、网络子掩码、DNS 信息、默认路由以及其他所需的启动参数。
- 3. PXE 客户端将进行启动发现，寻找 PXE 服务器。可选，可以配置 DHCP 服务器指向用于启动的 PXE 服务器。
- 4. PXE 服务器发送网络引导程序和下载文件的 IP 地址。这使得客户端能够从网络启动以安装操作系统。
- 5. PXE 客户端根据需要从 HTTPS 服务器请求介质（RPM 和控制文件）。HTTPS 并不是唯一需要的协议。NFS 和 FTP 也可以，尽管 HTTPS 是最常用的方法。PXE 系统还会通过 kickstart 文件向客户端发送 kickstart 参数。这些参数包含了配置系统存储、网络和要安装软件包的特定细节。
- 6. 介质服务器将安装内容发送给 PXE 客户端，从而允许安装操作系统。

# 在此情况下配置 PXE 服务器时，有三个组件：

- DHCP 服务器：在服务器启动时为其分配 IP 地址，同时也提供启用 PXE 启动的重要参数。
- 简易文件传输协议守护进程（TFTP）：作为 TFTP 服务器运行，允许引导程序在客户端上运行，启动操作系统安装。



- 超文本传输协议守护进程（HTTP）：这是一个 Web 服务器，用于托管安装所需的配置文件和 RPM 包。

## 注意

还有其他选项，例如使用 `dnsmasq` 作为组合服务器，它可以同时作为 DHCP 服务器、TFTP 服务器（最常用的是 `TFTPD`）和 DNS 转发器。然而，在许多企业环境中，需要独立的系统。例如，网络可能已经使用了微软 DHCP 服务器。

在示例示例中，有两个逻辑服务器运行着三个不同的服务，第一个系统上有一个 DHCP 服务器和一个 TFTP 服务器。第二个系统是 PXE 服务器，并将作为 HTTP 服务器，用于提供安装所需的红帽包管理器（RPM）文件和控制文件。两个系统都是多网卡的，并将在它们的次要接口上运行 DHCP 和 PXE。系统在次要接口上配有静态 IP 地址。

我们将在本章中涵盖构成 PXE 盛宴的主要配方：

- 使用 `kickstart` 自动化操作系统安装
- DHCP 服务器 – 不仅仅是 IP 地址
- 设置 Web 服务器 – HTTPD
- 提供启动 – TFTPD
- 回顾过去 – 手动安装

## 注意

多网卡服务器是连接到多个网络的系统。这通常在企业数据中心完成，以隔离系统，同时允许某些数据通过。可以在单网络上设置 PXE 服务器。

## 技术要求

创建新的 `kickstart` 文件的简单方法是构建一个新的操作系统，因为该过程会自动创建文件，稍后可以需要进行修改。PXE 环境还需要 DHCP 和 HTTPS 服务器。在开始之前，你需要下载 ISO 镜像。使用 Oracle VirtualBox 产品，许多配方的相关配置文件位于 `https://github.com/Packt/Oracle-Linux-Cookbook`。

# 使用 kickstart 自动化操作系统安装

`kickstart` 文件是自动化安装最重要的部分之一。它包含了自动安装和配置操作系统所需的信息。`kickstart` 文件是一个简单的文本文件，允许无人值安装。

## 准备工作

为了使用 `kickstart` 文件，你需要构建系统，例如 Oracle VirtualBox。该系统可以通过 `kickstart` 文件进行自动化安装，也可以通过图形或文本界面进行交互安装。

## 如何操作？

虽然你可以从头开始创建一个文件，但 Anaconda 安装程序在安装时将其保存到 `/root/anaconda-ks.cfg`，这个文件可以很容易地编辑并用于未来的构建。

注意

`kickstart` 有许多选项，列在附录中。

```
version=OL8
```

# 使用图形安装

用于安装 Oracle Linux 的加密密码可以通过回环挂载的 ISO 文件设置。密码通常是加密的，但可选，你可以使用 `--plaintext` 选项配合明文密码。`baseurl` 也可以是 NFS 路径或 FTP 服务器。例如，`--baseurl=https://pxe.local/ol8` 会告诉 `kickstart` 从 Web 服务器拉取 RPM 包：

```
repo --name="AppStream" --baseurl=file:///install/sources/cdrom/AppStream
```

以 `@` 开头的包是包组，不带 `@` 的行是单个包。如果未设置 `@`，则安装该组中的所有包。在示例中，安装了 `graphical-server-environment` 组以及 `kickstart-tools`。

```
%packages
@graphical-server-environment
kickstart-tools
%end
```

`keyboard='us'`

`lang en_US.UTF-8`

这是新服务器的主机名。对于系统，理想情况下应该是完全限定域名（FQDN）：

```
network --hostname=ol8.example.local
```

这用于选择挂载在文件系统的安装介质：

```
cdrom
```

这用于在首次启动时运行设置代理：

```
firstboot --enable
```

在这里，选择了已安装磁盘，以及逻辑卷管理器和文件系统的配置：

```
ignoredisk --only-use=sda
clearpart --none --initfs
part /boot --fstype="ext4" --disk=sda --size=1024
part pv.1 --fstype="lvmp" --disk=sda --size=8068
volroup ol --size=4096 pv.1
```

```
logvol /home --type=xfs --size=5120 --name=home--vg
logvol / --type=xfs --size=5120 --name=root--vg
logvol /u01 --type=xfs --size=10240 --name=u01--vg
logvol /var --type=xfs --size=5120 --name=var--vg
logvol swap --type="swap" --size=4056 --name=swap--vg
logvol /var/log --type=xfs --size=5120 --name=var_log--vg
```

这是服务器的时区：

- 系统时区

`timezone America/New_York --isUtc`

在新系统上可以设置加密密码。通常情况下，密码是加密的，但可选，你可以使用 `--plaintext` 选项配合明文密码。你还可以使用 `python 3 -c` 生成加密密码：

```python
import crypt,getpass;pw=getpass.getpass();print(crypt.crypt(pw) if (pw==getpass.getpass("Confirm:\n")) else exit(1))
```

Python 命令：

- Root密码

`rootpw --iscreate 65WF5c_GDUSIVXpDS78qVGm49tGCtrRbfy/01f57qQuPZYTOb/gobnN2oKNGzqrsent7QQthcdinNkhjJlSIPQopNyRxXQEJPUYuAM`

这允许你将缓存保存到驱动器中以便故障排除：

```
%addon com_redhat_kdump --enable=reserve-mb='auto'
%end
```

这是针对 root、用户和 Linux 密钥设置（LUKS）短语的密码策略：

```
%anaconda
pwppolicy root --minlen=6 --minquality=1 --nototrict --nochanges --notempty
pwppolicy user --minlen=6 --minquality=1 --nototrict --nochanges --emptyok
pwppolicy maks --minlen=6 --minquality=1 --nototrict --nochanges --emptyok
%end
```

```
[root@ol8 ~]# ksvalidator anaconda-ks.cfg
[root@ol8 ~]# █
```

图 2.2 – 清洁的 ksvalidator

## Kickstart 选项！

现在你已经对 `kickstart` 文件有了基本的了解，可以开始添加新选项了。这些选项允许你实现自动化安装，并赋予你更多控制权。相关选项见附录 – `kickstart` 选项。

# 工作原理...

你可以通过通过向统一引导加载程序 (`GRUB`) 条目添加 `ks` 参数来手动通过 `kickstart` 启动任何系统。格式为 `ks=PATH_TO_FILE`，其中 `PATH_TO_FILE` 是可以读取 `kickstart` 文件的 URL。这通常被放置在客户端可以的 HTTP 服务器上。

## DHCP 服务器 – 不仅仅是 IP

DHCP 服务器将运行 Oracle Linux 8 自带的标准 DHCP 服务器。安装 DHCP 非常简单。

## 准备工作

要设置 DHCP 服务器，你需要一个运行与待安装虚拟机处于同一子网的 Oracle Linux 8 虚拟机。

## 如何操作...

使用命令 `dnf install -y dhcp-server` 安装 DHCP 服务器。接下来的截图显示了完整过程：

```
[root@dhcp ~]# dnf install -y dhcp-server
Last metadata expiration check: 0:14:50 on Sun 06 Mar 2022 11:48:32 PM EST.
Dependencies resolved.
```

| 包 | 版本 | 仓库 | 大小 |

|---|---|---|---|---|

| 安装: dhcp-server | x86_64 | 12:4.3-6.45.el8 | ol8_baseos_latest | 530 k |



| 安装依赖项: bind-export-libs | x86_64 | 32:9.11.26-6.el8 | ol8_baseos_latest | 1.1 M |

| dhcp-common | noarch | 12:4.3-6.45.el8 | ol8_baseos_latest | 207 k |

| dhcp-libs | x86_64 | 12:4.3-6.45.el8 | ol8_baseos_latest | 148 k |

事务摘要

```
安装 4 个包
总下载大小: 2.0 M
已安装大小: 4.6 M
正在下载包:
(1/4): dhcp-libs-12:4.3-6.45.el8.x86_64.rpm 44 kB/s | 148 kB | 00:03
(2/4): dhcp-common-4.3-6.45.el8.noarch.rpm 62 kB/s | 207 kB | 00:03
(3/4): dhcp-export-libs-9.11.26-6.el8.x86_64.rpm 348 kB/s | 1.1 M | 00:03
(4/4): dhcp-server-4.3-6.45.el8.x86_64.rpm 24 MB/s | 530 kB | 00:00
Total 609 kB/s | 2.0 MB 00:03
运行事务检查
事务检查成功。
运行事务测试
事务测试成功。
运行事务
准备
正在安装: 1/4
正在安装: dhcp-libs-12:4.3-6.45.el8.x86_64 1/4
正在安装: dhcp-common-12:4.3-6.45.el8.noarch 2/4
正在安装: bind-export-libs-32:9.11.26-6.el8.x86_64 3/4
运行脚本: bind-export-libs-32:9.11.26-6.el8.x86_64 4/4
运行脚本: dhcp-server-4.3-6.45.el8.x86_64 4/4
运行脚本: dhcp-server-12:4.3-6.45.el8.x86_64 4/4
验证: bind-export-libs-32:9.11.26-6.el8.x86_64 4/4
验证: dhcp-common-12:4.3-6.45.el8.noarch 2/4
验证: dhcp-libs-12:4.3-6.45.el8.x86_64 3/4
验证: dhcp-server-12:4.3-6.45.el8.x86_64 4/4
已安装:
bind-export-libs-32:9.11.26-6.el8.x86_64
dhcp-common-12:4.3-6.45.el8.noarch
dhcp-libs-12:4.3-6.45.el8.x86_64
dhcp-server-1:4.3-6.45 完成！
```

安装完成后，通过防火墙启用 DHCP（使用 `firewall-cmd --add-service=dhcp --permanent` 和 `firewall-cmd --reload` 命令）：

```
[root@dhcp ~]# firewall-cmd --add-service=dhcp --permanent

[root@dhcp ~]# firewall-cmd --reload
```

DHCP 服务器在 `/usr/share/doc/dhcp-server` 中有一个示例配置文件。它包含了 `/usr/share/doc/dhcp-server/dhcp.example` 中的 IPv4 示例以及 `/etc/dhcp/` 中的 IPv6 示例，但默认是空的，可以通过以下方式替换：

```bash
[root@dhcp ~]# cp /usr/share/doc/dhcp-server/dhcp.example /etc/dhcp/dhcp.conf
```

接下来，需要更新配置文件，更改 IP 范围并添加 `ntp-servers 192.168.200.1` 配置。虽然配置 NTP 服务器是可选的。此外，当 PXE 服务器不是 DHCP 服务器时，你需要添加 `next-server` 参数指向 PXE 服务器的 IP 地址。这里有一个完整的示例文件：

```dhcp.conf
# 这些选项适用于所有网络

option domain-name "lab.m57.local";

option ntp-servers 192.168.56.10;

defaultlease-time 7200;

# 如果 DHCP 服务器是主服务器，应设置为 authoritative;

syslog 将日志发送到 syslog。你可以根据需要重新配置不同的位置：

log-facility local;

subnet 192.168.56.0 netmask 255.255.255.0 {

  range 192.168.56.100 192.168.56.150;

  option broadcast-address 192.168.56.255;

  option routers 192.168.56.1;

  option domain-name-servers 192.168.56.10;

}

option domain-name "lab.m57.local";

option ntp-servers 192.168.200.1;

next-server pxe.lab.m57.local;

# 在此处列出需要特定选项的主机，为主机硬编码 IP 地址，或定义非标准文件名或固定 IP 地址等主机特定参数。

host localhost {

  hardware ethernet 0:aaabbcc:dd;

  filename "vmnix.fixedhost";

  servername "fixedhost.m57.local";

}
```

最常见的是为主机分配 DHCP 管理范围之外的 IP 地址。

```
host fantasia {

  hardware ethernet 08:01:02:03:04:05;

  fixed-address fixedhost2.m57.local;

}
```

接下来，我们需要测试 DHCP 服务器。要做到这一点，使用 `dnf install -y nmap` 安装 `nmap` 程序。

`Nmap` 是一个强大的工具，可以用于许多领域。它作为端口扫描工具闻名，允许用户通过 `nmap -sP 192.168.200.1/28` 扫描网络寻找对 ping 响应的服务器，如下所示：

```
[root@root dhcp]# nmap -sP 192.168.200.1/28

Starting Nmap 7.70 ( https://nmap.org ) at 2022-03-06 00:00:10 EST

Nmap scan report for 192.168.200.1

Host is up (0.00014 latency).

MAC Address: 76:AC:B9:45:E1:62 (Unknown)

Nmap scan report for 192.168.200.3

Host is up (0.0021s latency).

MAC Address: 00:21:9B:B3:94:00 (Dell)

Nmap scan report for 192.168.200.1

Host is up (0.0026 latency).

MAC Address: 24:5E:3C:E9 (Oracle)

Nmap done: 1 IP address (1 host up) scanned in 0.64 seconds.
```

图 2–7 – Nmap 扫描

我们现在知道 DHCP 服务器是如何工作了，所以接下来是 Apache HTTPD 服务器。

# 设置 Web 服务器 – HTTPD

PXE 服务器的下一步是安装一个 Web 服务器。在本例中，我们将使用 Apache。
其他 Web 服务器也可以工作，但 Apache 是最常用的服务器之一。

## 准备工作

为了设置 HTTP 服务器，你需要在你的环境中运行一个 **Oracle Linux 8** 虚拟机（VM）。该服务器的 IP 地址应该能够路由到我们正在使用的虚拟机，并且防火墙端口应该允许 HTTP/HTTPS 流量。在理想情况下，你还应该留有足够的空间来存放几个 ISO 文件。
通常情况下，20-30 GB 的数据空间就足够了。

## 如何操作...

从开始安装 Apache HTTPD 服务器非常简单；只需运行 `yum install -y http` 即可。
服务器安装完成后，将 ISO 文件复制到你选择的目录。在我们的示例中，`OracleLinux-R8-U5-x86_64-dvd.iso` 被复制到了 `/root`，如图 2.9 所示。

```
[root@pxe ~]# ls  initial-setup-ks.cfg  anaconda-ks.cfg OracleLinux-R8-U5-x86_64-dvd.iso

[root@pxe ~]# #
```



> 图 2.9 – `/root` 下的 Oracle Linux ISO

下一步是将 ISO 文件挂载到 `docroot` 下的某个目录中。在 Apache 的标准安装中，`docroot` 位于 `/var/www/html`，因此创建了目录 `ol8`。当挂载 ISO 时，使用环回 `loopback` 方法会更高效。这允许 ISO 文件作为普通文件系统被挂载。接下来，使用环回方法，通过以下命令将 ISO 文件挂载到 `/var/www/html/ol8` 并作为挂载点：

```
mount -o ro,loop /root/OracleLinux-R8-U5-x86_64-dvd.iso /var/www/html/ol8
```

挂载完成后，运行 `df` 命令将显示已挂载的文件系统。整系列命令可以在下面的截图（图 2.10）中看到。

```
[root@pxe html]# mkdir /var/html/OL8

[root@pxe html]# mount -o loop,/root/OracleLinux-R8-05_x86_64.iso /var/html/OL8

[root@pxe html]# df -h

Filesystem      Size Used Avail Mounted on

tmpfs           344M 0 344M 0% /dev

tmpfs           344M 0 344M 0% /dev/sh

tmpfs           344M 5.4M 339M 2% /run

tmpfs           344M 0 344M 0% /sys/fs/cgroup

/dev/mapper/ol-root 500G 170G 344G 33% /

/dev/mapper/ol-home 100G 11.8G 88.2G 2% /home

/dev/sda         1024G 448M 1024G 0% /root

tmpfs            69M 0 69M 0% /run/user/42

/dev/loop0      100G 0 100G 0% /var/html/OL8
```

图 2.10 - ISO 已挂载

现在文件系统已经挂载，让我们在防火墙中打开 80 和 443 端口。通过 `firewall-cmd` 可以轻松实现，添加对 `http` 和 `https` 端口的开放，并作为持久性更改保存到防火墙中。一旦端口打开，防火墙规则将重新加载。运行以下三个命令来执行这些任务：

```
firewall-cmd --add-service=http --permanent
firewall-cmd --add-service=https --permanent
firewall-cmd --reload
```

现在防火墙已打开，且 ISO 已通过环回方法挂载，我们可以使用 `systemctl start httpd` 命令启动 Apache 服务器。

你可以通过将浏览器指向服务器的 IP 地址和 `OL8` 目录来验证所有工作是否符合预期，如下所示。这将显示 ISO 的内容，包括发行说明和 BaseOS 目录中的 RPM 包，如图 2.11 所示。

### /OL8 索引

| 名称 | 最后修改时间 | 大小 | 描述 |
|---|---|---|---|
| Parent Directory/ | | | |
| AppStream/ | 2021-11-15 16:14 | - | |
| BaseOS/ | 2021-11-15 16:14 | - | |
| EFI/ | 2021-11-15 16:30 | - | |
| EULA | 2021-11-15 16:08 | 8.6K | |
| GPL | 2021-11-15 16:08 | 18K | |
| RELEASE-NOTES-en | 2021-11-15 16:08 | 181K | |
| RELEASE-NOTES-en.html | 2021-11-15 16:08 | 484K | |
| RPM-GPG-KEY | 2021-11-15 16:08 | 3.1K | |
| RPM-GPG-KEY-oracle | 2021-11-15 16:08 | 3.1K | |
| TRANS.TBL | 2021-11-15 16:31 | 3.3K | |
| extra_files.json | 2021-11-15 16:08 | 1.4K | |
| images/ | | | |
| isolinux/ | 2021-11-15 16:30 | | |
| media.repo | 2021-11-15 16:30 | | |

图 2.11 - 通过 HTTP 服务 ISO

（注：后续部分文本存在重复性，此处已按要求完成翻译逻辑）

这里快完成了。要为 PXE 配置文件创建目录并构建默认菜单，请以下命令：

```
mkdir /var/lib/tftpboot/pxelininux.cfg
```

我们终于可以安装配置文件。将此示例配置文件复制到 `/var/lib/tftpboot/pxelininux.cfg/default`：

```
default linux-auto

prompt 1

timeout 60

display boot.msg

label linux-auto

menu "Install OL8 in Graphical Mode using the kickstart file

menu default

kernel ol8/mlinux

append initrd=018/initrd.img ip=dhcp inst.repo=pxe.lab.m57.local/08

ks=http://pxe.lab.m57.local/files/08ks.cfg

label linux-manual

menu "Install OL8 in Graphical Mode with manual input

menu default

kernel ol8/mlinux

append initrd=018/initrd.img ip=dhcp inst.repo=pxe.lab.m57.local/08

label rescue

menu "Rescue installed system

kernel ol8/mlinux

append initrd=018/initrd.img rescue

label local

menu "Boot from local drive

locoboot 0ffff
```

在此示例中，默认安装将是 `linux-auto`，它将在 60 秒后启动，除非用户手动选择以下选项之一：

- `linux-auto`：这是默认选项，将使用 kickstart 参数安装 Oracle Linux
- `linux-manual`：这将启动一个传统的 Oracle Linux 安装程序，提示用户手动从 Anaconda 中选择所有选项
- `rescue`：这将将在救援模式下启动
- `local`：这将从本地磁盘启动

你可以根据需要轻松修改名称以满足你的特定需求。PXE 启动起初看起来令人生畏，但它为管理 Linux 安装提供了一个强大的工具。

## 它是如何工作的...

当系统启动时，它们将根据 DHCP 服务器配置加载引导程序。这将使系统从 TFTP 服务器启动，从而开始 PXE 过程。

# 回过去 – 手动安装

自动化安装非常棒，但对于某些管理员来说，配置和维护支持自动化安装的基础设施的复杂性比进行手动安装花费更多精力。本教程将介绍手动安装的工作原理。

## 准备工作

要完成这一点，你需要一个要安装的系统。在示例中，将使用 Oracle Virtual VM，但同样可以运行在裸机服务器或不同的虚拟机管理器上。你还需要安装媒体。通常使用 ISO 文件即可，但你也可以使用启动 ISO 配合 HTTP 服务器、来自 FTP 服务器或网络文件共享。

## 如何操作...

无论你是从 ISO、USB 闪盘，甚至是带有图形化安装选项的 kickstart 文件启动，过程都是相同的！

如果你是从仅引导镜像启动，将需要启用网络并指向安装源。这将在接下来的步骤中显示。如果你是从 ISO 或 USB 安装，请跳到*它是如何工作的*... 章节：

1. 当从引导镜像启动时，你需要选择 **Install Oracle Linux X** 来启动过程。可能的情况下，请使用最新版本的 Oracle Linux。安装开始时，你将看到第一个屏幕，可以在那里测试引导镜像或继续：

```
Oracle Linux 8.7.0

Install Oracle Linux 8.7.0

Test this media & install Oracle Linux 8.7.0

Troubleshooting

按 Tab 键查看菜单项的完整配置选项。
```



![](img/110fa0d6324f0893fff03cee6394144d_73_0.png)

2. 接下来，选择你的语言：

![](img/110fa0d6324f0893fff03cee6394144d_74_0.png)

图 2.16 – 安装语言

3. 选择语言后点击“继续”。接下来，你应该看到安装摘要部分：

# 安装摘要

# ORACLE LINUX 8.7 安装

## 本地化

## 软件

## 系统

- 键盘
  English (US)
- 安装源
  设置基 存储库出错
- 安装目标
  自动分区选择
- 语言支持
  English (United States)
- 软件选择
  未设置安装源
- KDUMP
  Kdump 已启用
- 时间和日期
  America/New York 时区
- 网络和主机名
  未连接
- 安全性策略
  未选择配置文件

## 用户设置

- Root 密码
  Root 账户已禁用。

> 请在继续下一步之前完成带有此图标标记的项目。

![](img/110fa0d6324f0893fff03cee6394144d_75_0.png)

现在，我们需要完成两个任务：

- 启用网络
- 将安装源设置为 Oracle 的 yum 仓库

要启用网络，点击 `Network & Host Name` 选项。

4. 在这里，你需要开启以太网并用服务器名称更新主机名。这将在后续步骤中显示。如果你是从 ISO 或 USB 安装，跳过

## 网络和主机名

# ORACLE LINUX 8.7 安装

![](img/110fa0d6324f0893fff03cee6394144d_76_0.png)

有线 (enp3)
已连接
速度 1000 Mbps
IP 地址
DHCP
主机名：localhost

这将在接下来的步骤中显示。如果你是从 ISO 或 USB 安装，跳到*它是如何工作的*... 章节：

5. 在这里，你需要开启以太网并用服务器名称更新主机名。这将在接下来的步骤中显示。这将带你进入安装摘要。

# 安装摘要

# ORACLE LINUX 8.7 安装

![](img/110fa0d6324f0893fff03cee6394144d_77_0.png)

## 本地化

## 软件

## 系统

- 键盘
  English (US)
- 安装源
  设置基存储库出错
- 安装目标
  自动分区选择
- 语言支持
  English (United States)
- 软件选择
  未设置安装源
- KDUMP
  Kdump 已启用
- 时间和日期
  America/New York 时区
- 网络和主机名
  未连接
- 安全性策略
  未选择配置文件

## 用户设置

- Root 密码
  Root 账户已禁用。

> 请在继续下一步之前完成带有此图标标记的项目。

现在，我们需要完成两个任务：

- 启用网络
- 将安装源设置为 Oracle 的 yum 仓库

要启用网络，点击 `Network & Host Name` 选项。

4. 在这里，你需要开启以太网并用服务器名称更新主机名。这将在接下来的步骤中显示。这将带你进入安装摘要。

6. 选择语言后点击“继续”。接下来，你应该看到安装摘要部分：

# 安装摘要

# ORACLE LINUX 8.7 安装

这将带你进入安装摘要。

6. 选择语言后点击“继续”。接下来，你应该看到安装摘要部分：

# 安装摘要

# ORACLE LINUX 8.7 安装

![](img/110fa0d6324f0893fff03cee6394144d_78_0.png)

## 本地化

## 软件

## 系统

- 键盘
  English (US)
- 安装源
  设置基存储库出错
- 安装目标
  自动分区选择
- 语言支持
  English (United States)
- 软件选择
  未设置安装源
- KDUMP
  Kdump 已启用
- 时间和日期
  America/New York 时区
- 网络和主机名
  未连接
- 安全性策略
  未选择配置文件

## 用户设置

- Root 密码
  Root 账户已禁用。

> 请在继续下一步之前完成带有此图标标记的项目。

现在，我们需要完成两个任务：

- 启用网络
- 将安装源设置为 Oracle 的 yum 仓库

要启用网络，点击 `Network & Host Name` 选项。

4. 在这里，你需要开启以太网并用服务器名称更新主机名。这将在接下来的步骤中显示。这将带你进入安装摘要。

6. 选择语言后点击“继续”。接下来，你应该看到安装摘要部分：

# 安装摘要

# ORACLE LINUX 8.7 安装

这将带你进入安装摘要。

# 它是如何工作的...

当系统启动时，它们将根据 DHCP 服务器配置加载引导程序。这将使系统从 TFTP 服务器启动，从而开始 PXE 过程。

# 回过去 – 手动安装

自动化安装非常棒，但对于某些管理员来说，配置和维护支持自动化安装的基础设施的复杂性比进行手动安装花费更多精力。本教程将介绍手动安装的工作原理。

## 准备工作

要完成这一点，你需要一个要安装的系统。在示例中，将使用 Oracle Virtual VM，但同样可以运行在裸机服务器或不同的虚拟机管理器上。你还需要安装媒体。通常使用 ISO 文件即可，但你也可以使用启动 ISO 配合 HTTP 服务器、来自 FTP 服务器或网络文件共享。

## 如何操作...

无论你是从 ISO、USB 闪盘，甚至是带有图形化安装选项的 kickstart 文件启动，过程都是相同的！

如果你是从仅引导镜像启动，将需要启用网络并指向安装源。这将在接下来的步骤中显示。如果你是从 ISO 或 USB 安装，请跳到*它是如何工作的*... 章节：

1. 当从引导镜像启动时，你需要选择 `Install Oracle Linux X` 来启动过程。可能的情况下，请使用最新版本的 Oracle Linux。安装开始时，你将看到第一个屏幕，可以在那里测试引导镜像或继续：

```
Oracle Linux 8.7.0

Install Oracle Linux 8.7.0

Test this media & install Oracle Linux 8.7.0

Troubleshooting

按 Tab 键查看菜单项的完整配置选项。
```



![](img/110fa0d6324f0893fff03cee6394144d_73_0.png)

2. 接下来，选择你的语言：

![](img/110fa0d6324f0893fff03cee6394144d_74_0.png)

图 2.16 – 安装语言

3. 选择语言后点击“继续”。接下来，你应该看到安装摘要部分：

# 安装摘要

# ORACLE LINUX 8.7 安装

## 本地化

## 软件

## 系统

- 键盘
English (US)
- 安装源
设置基 存储库出错
- 安装目标
自动分区选择
- 语言支持
English (United States)
- 软件选择
未设置安装源
- KDUMP
Kdump 已启用
- 时间和日期
America/New York 时区
- 网络和主机名
未连接
- 安全性策略
未选择配置文件

## 用户设置

- Root 密码 
Root 账户已禁用。

> 请在继续下一步之前完成带有此图标标记的项目。

![](img/110fa0d6324f0893fff03cee6394144d_75_0.png)

现在，我们需要完成两个任务：

- 启用网络
- 将安装源设置为 Oracle 的 yum 仓库

要启用网络，点击 `Network & Host Name` 选项。

4. 在这里，你需要开启以太网并用服务器名称更新主机名。这将在后续步骤中显示。如果你是从 ISO 或 USB 安装，跳过

## 网络和主机名

# ORACLE LINUX 8.7 安装

![](img/110fa0d6324f0893fff03cee6394144d_76_0.png)

有线 (enp3)
已连接
速度 1000 Mbps
IP 地址
DHCP
主机名：localhost

以及网域。当你启用网络时，系统将自动获取 DHCP 信息。如果你想手动配置此项，请点击“配置...”（`Configure...`）：

![](img/110fa0d6324f0893fff03cee6394144d_80_0.png)

图 2.22 - 访问手动网络设置

2. 这将带你进入网络详情，你可以在那里手动设置 MTU、IP 地址和其他网卡（NIC）特定设置。如果需要，你还可以禁用 IPv6。

![](img/110fa0d6324f0893fff03cee6394144d_81_0.png)

3. 网络设置完成后，你可以使用 NTP 服务器等网络资源来同步时钟。要执行此操作，在“时间与日期”（`TIME & DATE`）下，点击齿轮图标：

## 时间与日期

# ORACLE LINUX 8.7 安装

完成 (`Done`)

帮助！(`Help!`)

区域：美洲 城市：纽约

网络时间：开启 (`Network Time ON`)

![](img/110fa0d6324f0893fff03cee6394144d_82_0.png)

21:28

24小时制 AM/PM

01 / 03 / 2023

> [!IMPORTANT]
> 你没有配置可用的 NTP 服务器

图 2.24 – 访问 NTP 设置

- 4. 接着，你可以添加 NTP 服务器。默认使用公共服务器，但如果你运行了本地 NTP 服务器，请确保在此处添加这些服务器。

| 添加并标记为使用的 NTP 服务器 |
|---|---|---|---|
| 主机名 (Host Name) | 池 (Pool) | 正常 (Working) | 使用 (Use) |
| 2.poolntp.org | [x] | [x] | [x] |

图 2.25 – NTP 设置

- 5. 接下来，根据需要在“安装源”（Installation Source）下添加额外的软件源。这在之前进行网络安装时已经完成。

你还可以设置安装哪些 RPM 组以及任何额外的软件。这在“软件选择”（`SOFTWARE SELECTION`）下进行：

![](img/110fa0d6324f0893fff03cee6394144d_83_0.png)

6. 设置好基础环境（Base Environment）并添加任何额外软件后，下一个任务是设置安装目标。这通过点击“安装目标”（Installation Destination）完成。

在这里，你应该能看到系统可用的物理和逻辑驱动器。默认是将存储配置设置为“自动”（`Automatic`），但让我们通过选择自定义配置（`custom configuration`）来探索不同的启动磁盘结构。一旦选择了“自定义”（`Custom`），点击“完成”（`Done`）按钮。

## 安装目标

# ORACLE LINUX 8.7 安装

完成 (`Done`)

美国 (US)

帮助！(`Help!`)

## 设备选择 (Device Selection)

选择你想要安装的设备（s）。在你点击主菜单上的“开始安装”（`Begin Installation`）按钮之前，它们将保持不变。

## 本地标准磁盘 (Local Standard Disks)

100 GIB
ATA VBOX 虚拟硬盘
sda / 100 GIB 空闲

![](img/110fa0d6324f0893fff03cee6394144d_84_0.png)

此处未选中的磁盘将不会被触碰。

## 特殊与网络磁盘 (Specialized & Network Disks)

![](img/110fa0d6324f0893fff03cee6394144d_84_1.png)

此处未选中的磁盘将不会被触碰。

## 存储配置 (Storage Configuration)

- 自动 (`Automatic`)
- 自定义 (`Custom`)

全磁盘摘要和引导程序...

已选择 1 个磁盘：100 GIB 容量：100 GIB 空闲 刷新... (`Refresh...`)

> 图 2.27 – 安装目标

7. 从这里，你可以选择默认的卷管理策略，也可以手动创建新布局。大多数系统将使用 LVM。

## 手动分区 (MANUAL PARTITIONING)

# ORACLE LINUX 8.7 安装

完成 (`Done`)

...（此处内容）

图 2.28 – 手动分区

- 8. 在这里，你可以选择默认的卷管理策略，也可以手动创建新布局。大多数系统将使用 LVM。

## 手动分区 (MANUAL PARTITIONING)

# ORACLE LINUX 8.7 安装

完成 (`Done`)

...（此处内容）

图 2.29 – Btrfs

- 9. 在这里，你可以选择默认的卷管理策略，也可以手动创建新布局。大多数系统将使用 LVM。

## 手动分区 (MANUAL PARTITIONING)

# ORACLE LINUX 8.7 安装

完成 (`Done`)

...（此处内容）

图 2.30 – 应用策略

- 10. 在这里，你可以选择默认的卷管理策略，也可以手动创建新布局。大多数系统将使用 LVM。

图 2.31 – 应用策略

| Option Name | firewall |
| --- | --- |
| Description | 用于配置已安装系统上的防火墙。 |
| Options | - 必须使用 `--enabled` 或 `-enable`。启用或禁用防火墙。<br>- 必须使用 `--disabled` 或 `-disable`。如果禁用，则不配置 iptables 规则。<br>- `--trust` 设置受信任的网络设备，允许所有流量通过防火墙。若要配置多个设备，请让每个设备作为一个独立的条目，且之间不加逗号，例如 `-trust eth0 -trust eth8`。<br><br>- `--incoming` 添加以下每个标记，用以允许这些常用服务的入站流量：
  - `-ssh`
  - `-smtp`
  - `-http`
  - `-ftp`<br>- `--port=` 指定用于访问服务器的端口。您可以使用 /etc/service 中的端口来指定特定的端口:协议组合。多个端口可以用逗号分隔。例如 ldap:tcp, 1521:tcp。<br>- `--service=` 提供了一种启用特定服务的简便方法，例如 CUPS 服务，或需要打开多个 UDP/TCP 端口的服务。这允许您以可读的格式轻松地打开这些端口。<br>- `--use-system-defaults` 不配置防火墙。如果指定了其他选项，它们将被忽略。 |

| Option Name | firstboot |
| --- | --- |
| Description | 此选项可以在系统启动时禁用设置程序的运行。请确保您已安装了 `initial-setup.rpm`（如果需要 GUI，则安装 `initial-setup-gui.rpm`）。此选项默认禁用。 |
| Options | - `--enable` 或 `-enabled` 在系统首次启动时启动设置程序。<br>- `--disable` 或 `-disabled` 在系统首次启动时不启动设置程序。<br>- `--reconfig` 允许设置在启动时以重配置模式启动。这允许在设置默认选项外，设置网络配置、root 密码、时区、语言、鼠标和键盘选项。 |

| Option Name | graphical |
| --- | --- |
| Description | 如果未设置，图形 命令为默认值。安装将以全图形化方式继续。 |
| Options | `--non-interactive` 在完全非交互模式下执行安装。此模式在需要用户交互时将终止安装。 |
| Option Name | group |
|| --- | --- |
| Description | 此选项在系统上创建一个用户组。 |
| Options | - `--name=` 是必须的，用于设置组名。<br>- `--gid=` 是可选参数，将设置组的 GID。 |
| Option Name | halt |
| --- | --- |
| Description | 如果使用，系统将在安装完成后 halt（停止）。在未设置其他方法的情况下，这是默认的完成方法。其他完成方法包括 poweroff（关机）、reboot（重启）和 shutdown（关闭）。 |
| Options | 无 |
| Option Name | logging |
| --- | --- |
| Description | 这对于排查 PXE 安装有用。它控制安装程序在安装期间的日志。它不会配置被安装系统的日志。 |
| Options | - `--host=` 日志发送到的 syslog 主机。<br>- `--port=` 远程 syslog主机上用于使用的端口。如果未设置，则使用默认端口 (UDP 514)。 |

- `--level=` 指定发送到设备 tty3 的消息最小级别。无论该级别如何，所有消息都会发送到日志主机和文件。有效值为 critical, debug, error, info 和 warning。

| Syntax | logging [--host=host] [--port=port] [--level=critical|debug|error|info] |

| Option Name | poweroff |
| --- | --- |
| Description | 使用时，安装完成后将系统执行关机并断电。 |
| Options | 无 |

| Option Name | reboot |
| --- | --- |
| Description | 安装完成后重启系统。 |
| Options | `--eject` 在重启之前弹出启动介质（DVD、USB 等）。 |

| Option Name | repo |
| --- | --- |
| Description | 启用额外的 DNF/YUM 源。每个仓库需要单独的一行。 |
| Options | `--name=` 分配并设置仓库名称和 URL。如果名称与现有仓库冲突，则将被忽略。格式为 `--name=repo [--baseurl=url|--mirrorlist=url|--metalink=url] [options]`。可以将额外的选项添加到 URL 中。作为警告，仓库文件中不支持使用变量。但是，您可以使用 `$releasever` 和 `$basearch`：

- `--baseurl`: 仓库的 URL
- `--mirrorlist`: 仓库的镜像列表
- `--metalink`: 带有 metalink 的仓库 URL

- `--proxy=[protocol://][username[:password]@host[:port]` 设置仓库的代理。
- `--noverifys` 禁用 HTTPS 服务器的验证。 |

| Option Name | selinux |
| --- | --- |
| Description | 用于配置 selinux 的初始策略和状态。默认策略为 enforcing。 |
| Options | - `--enforcing` 将 selinux 策略设置为 enforcing。这是默认设置。<br>- `--permissive` 将 selinux 策略设置为 permissive。这允许警告输出到控制台 syslog，但不执行策略。<br>- `--disabled` 禁用 selinux。 |
| Option Name | shutdown |
| --- | --- |
| Description 在安装完成后对系统执行 shutdown 命令。 |
| Options | |

| Option Name | keykey |
| --- | --- |
| Description | 这是带有 metalink 的仓库 URL。 |
| Options | |

| Option Name | config |
| --- | --- |
| Description | 允许设置在启动时以重配置模式启动。这允许在设置默认选项外，设置网络配置、root 密码、时区、语言、鼠标和键盘选项。 |
| Options | |

| Option Name | text |
| --- | --- |
| Description | 如果未设置，图形 命令为默认值。安装将以全图形化方式继续。 |
| Options | `--non-interactive` 在完全非交互模式下执行安装。此模式在需要用户交互时将终止安装。 |
| Option Name | url |
| --- | --- |
| Description | 使用时，安装完成后将系统执行关机并断电。 |
| Options | |

Linux 内核版本以源代码的形式分发，而基于 Linux 的各种发行版或操作系统通常会打包并分发它们自己的内核版本，并将其整合到各自的发布版本中。此外，想要直接在系统中编译并安装内核的用户可以访问这些源代码。下表显示了 Linux 7、8 和 9 的 Linux 主线发布版本。

| OS 版本 | RHCK 发布版本 | 最新 UEK 版本 |
| :--- | :--- | :--- |
| Linux 7 | Linux 3.x | UEK 6/Linux 5.4 |
| Linux 8 | Linux 4.x | UEK 7/Linux 5.15 |
| Linux 9 | Linux 5.14 | UEK 7/Linux 5.15 |

表 3.1 – 按发布版本提供的内核选项

# 内核基础 – UEK 和 RHCK

在全新安装 Oracle Linux 后，默认使用“不可破坏企业内核”（Unbreakable Enterprise Kernel，UEK）。但是，在某些情况下，你可能希望切换到红帽兼容内核（RHCK）。

在某些场景下，默认内核可能不是使用的正确版本：

- UEK 发布版本基于比 RHCK 版本更新的内核，后者是 Red Hat 服务器的标准。在 Oracle Linux 中，你可以选择使用 UEK，它提供了更更新的内核。
- 当前内核版本可能与你的特定硬件不兼容。UEK 系统可以在新硬件上启动，而旧的 RHCK 则不能。一个例子是 UEK 7，它支持 Microsoft Azure 网络适配器 (MANA)，而 UEK 6 则不支持。
- 假设系统安装了 UEK Beta 版或初步发布版。在这种情况下，需要监控 UEK，以确保只有在管理员有意且手动选择内核时才使用该内核。
- 用于 Linux 的 UEK 提供了许多优势，例如显著的性能提升和新功能。Linux 操作系统是一个模块化系统，内核与硬件交互，并代表应用程序控制资源访问调度。大多数应用程序运行在所谓的用户空间中，只有一组稳定的系统库会请求内核服务。例外是直接访问内核的应用程序，最常见安全应用程序。
- 安装 UEK 不会更改 glibc 等系统库，glibc 是几乎所有应用程序（包括 Oracle Database）都使用的接口。无论你运行带有 UEK 还是带有 RHCK 的 Oracle Linux，glibc 版本都是相同的。这不仅限于 glibc，也适用于 libssl、libc 和 libcrypt 等所有系统库。

## 注意

对于任何基线操作系统，可能都有多个版本的 UEK。UEK 版本的选择取决于应用程序团队，并且必须反映任何兼容性要求。

这些示例和类似的情况要求你在内核类型之间切换。在旧版本中，管理默认内核是通过配置 GRUB 引导加载程序完成的。然而，从 Oracle Linux 8 及更高版本开始，你应该使用 `grubby` 命令来控制和管理内核启动配置。`grubby` 是 GNU 项目提供的第 2 版本引导加载程序 (`GRUB 2`) 的一部分。`GRUB` 是市场上许多 Linux 发行版的默认引导加载程序。将其加载到内存后，它会将控制权交给运行的内核。

`GRUB 2` 是 Oracle Linux 上使用的默认引导加载程序，它可以加载许多不同的操作系统，包括 Microsoft Windows。

## 准备工作

让我们开始深入研究该过程以更好地理解它。

## 启动过程

你已经了解 Oracle Linux 启动选项如何帮助你排查系统启动时遇到的问题。在使用新硬件或云环境时，这些知识非常有益。

当 Oracle Linux 系统启动时，它会执行许多任务，这些任务取决于你的硬件用于处理系统启动的固件类型。它可能是统一扩展固件接口 (`UEFI`) 固件，或传统的 BIOS 固件。传统的基本输入输出系统 (`BIOS`) 固件是遗留的。`BIOS` 固件维护了可启动设备列表。系统中的互补氧化物半导体 (`CMOS`) 芯片存储了设置，当系统上电时，`BIOS` 启动过程使用 `UEFI` 固件来尝试加载的可启动设备。使用 `BIOS` 固件的系统。`UEFI` 启动过程是遗留的，尽管现代系统可能仍然使用 `BIOS` 启动，内核在 `UEFI` 固件上交互。`UEFI` 固件管理的是一个包含 `.efi` 文件的引导程序。`EFI` 系统分区 (`ESP`) 包含了可作为 `EFI` 应用程序。使用 `.efi` 文件可以对内核进行更多控制，这可以利用新的安全特性。一个新安全特性是安全启动（Secure Boot），将在本章中介绍。

## UEFI 启动序列

`UEFI` 硬件使用的以下启动序列：

1. 系统首先执行引导自检 (`POST`)，识别所有可能的启动设备。
2. `UEFI` 根据全局唯一标识 (`GUID`) 搜索 `GUID` 分区表 (`GPT`)，以确定 `ESP`。通过 `efibootmgr` 工具，可以在不使用默认情况下指定不同的顺序。
3. 启动管理器检查是否启用了安全启动。如果没有启用安全启动，启动管理器请求 `ESP` 上的 `GRUB 2` 加载器。否则，启动管理器请求引导程序的证书并对其进行验证。引导器将内核加载到内存中并创建一个临时的内存文件系统（`tmpfs`）。这将用于提取 `initramfs` 镜像的内容。`vmlinuz` 是可启动压缩 Linux 内核的名称。嵌入 Linux 内核并在启动早期加载的根文件被称为 `initramfs`。
4. 驱动模块从 `initramfs` 文件系统加载。这些模块对于访问根文件是必要的。
5. 系统从第一个进程 `systemd` 开始启动。
6. `systemd` 运行运行定义的任何其他进程。

## Legacy BIOS 序列

传统的 `BIOS` 硬件使用以下序列：

1. 系统首先执行引导自检 (`POST`)，识别系统配置、测试内存并识别所有可能的启动设备。
2. 一旦 `BIOS` 识别出启动设备，它就会读取设备的第一个扇区，即主引导记录 (`MBR`)。`MBR` 包含了引导加载器，这是一个负责加载操作系统的微程序。`MBR` 读取分区表以确定启动分区。此外，`MBR` 还包含指向引导加载器 `GRUB 2` 的指针。`GRUB` 可以在安装 `GRUB` 的设备或独立设备上运行。这对于在同一系统上同时启动 Linux 和 Windows 有帮助。
3. 引导加载器将 `vmlinux` 内核加载到内存中并创建一个临时的内存文件系统（`tmpfs`）。这将用于提取 `initramfs` 镜像的内容。
4. 驱动模块从 `initramfs` 文件系统加载。
5. 内核启动 `systemd` 进程。

## 如何操作...

既然我们已经讨论了基础知识，我们可以跳过所有无聊的部分，直接开始实操。
是时候边玩边学了！

我们可以做的第一件事之一是禁用系统中当前加载的内核。
以下命令将显示我们的 Linux 系统中安装并配置的所有内核（请以 root 身份运行）：

```



# grubby --info=ALL

这里是输出的一个示例：

```
[root@lml ~]# grubby --info=ALL

index=0

kernel=/boot/vmlinux-5.4.17-2136.315.5.el8uek.arch64"

args= ro crashkernel-auto rd.lvvm=/ol/root rd.lvvm=/ol/swap $tuned_params

root=/dev/mapper/ol-root

initrd=/boot/initramfs-5.4.17-2136.315.6.el8uek.arch64.img $tuned_initrd

title=Oracle Linux Server 8 (5.4.17-2136.315.5.el8uek.arch64)

id=b4e24363d0c9c268d4a3f6c70caa52-5.4-17-2136.315.5.el8uek.arch64

kernel=/boot/vmlinux-5.4.17-2136.313.6.el8uek.arch64"

args= ro crashkernel-auto rd.lvvm=/ol/root rd.lvvm=/ol/swap $tuned_params

root=/dev/mapper/ol-root

initrd=/boot/initramfs-5.4.17-2136.300.7.el8uek.arch64.img $tuned_initrd

title=Oracle Linux Server 8 (5.4.17-2136.300.7.el8uek.arch64)

id=b4e24363d0c9c268d4a3f6c70caa52-5.4-17-2136.300.7.el8uek.arch64

index=3

kernel=/boot/vmlinux-0-rescue-b4e24363d0c9c268d4a268d4a3f6c70caa52

args= ro crashkernel-auto rd.lvvm=/ol/root rd.lvvm=/ol/swap

root=/dev/mapper/ol-root

initrd=/boot/initramfs-0-rescue-b4e24363d0c9c268d4a268d4a3f6c70caa52.img"

title=Oracle Linux Server 8 (0-rescue-b4e24363d0c9c268d4a268d4a3f6c70caa52)

[root@lml ~]#
```

![](img/110fa0d6324f0893fff03cee6394144d_99_0.png)

## 注意

示例使用的是 Arm 系统完成的，aarch64 后缀将显示 x86_64 后缀。

我们也可以使用以下命令确定系统中的默认内核：

```
# grubby --info=DEFAULT
```

这里是输出的一个示例：

```
[root@arml1 ~]# grubby --info=DEFAULT

index=0

kernel="boot/vmlinux-5.4.17-2136.315.5.el8uk.aarch64"

args="ro crashkernel-auto rd.lvm=vg rd.lvm.vo/swap $tuned_params"

root="/dev/mapper/ol-root"

initrd="/boot/initramfs-5.4.17-2136.315.5.el8uk.aarch64.img $tuned_initrd"

title="Oracle Linux Server 8 (5.4.17-2136.315.5.el8uk.aarch64)"

id="b4e24363d0c9c268d4a3f6c70caa52-5.4.17-2136.315.5.el8uk.aarch64"

[root@arml1 ~]#
```

我们可以通过运行以下命令将特定内核配置为默认内核：

```
# grubby --set-default <kernel>
```

这里是使用上述命令更改内核的示例。已知 RH 将使用版本 4.18.0-425.13.1.el8ue7，我们需要指向引导文件，添加 vmlinux-：

```
[root@ol8 ~]# grubby --set-default /boot/vmlinux-4.18.0-425.13.1.el8ue7
```
图 3.2 — 更改默认内核

```
[root@ol8 ~]# grubby --info=DEFAULT

kernel="boot/vmlinux-4.18.0-425.13.1.el8ue7"

args="ro crashkernel-auto resume=/dev/mapper/ol-root rd.lvm/root rd.lvm/swap"

root="/dev/mapper/ol-root"

initrd="/boot/initramfs-4.18.0-425.13.1.el8ue7.img $tuned_initrd"

title="Oracle Linux Server 8 (4.18.0-425.13.1.el8ue7)"

id="b4e24363d0c9c268d4a3f6c70caa52-4.18.0-425.13.1.18"

[root@ol8 ~]#
```
图 3.3 — 使用 grub 更改默认内核

`grub` 命令的另一个用途是更新内核条目添加或移除传递给内核的默认启动参数；以下是它的一个示例。首先，我们将显示特定内核的所有信息：这将显示指定内核的细节以及任何参数：

```
[root@ol8 ~]# grubby --info=/boot/vmlinux-0-rescue-3f1be2ec0d247d9b6bb9b2479aa

index=4

kernel="boot/vmlinux-0-rescue-3f1be2ec0d247d9b6bb9b2479aa"

args="ro crashkernel-auto resume=/dev/mapper/ol-root rd.lvm/root rd.lvm/swap $tuned_params"

root="/dev/mapper/ol-root"

initrd="/boot/initramfs-0-rescue-3f1be2ec0d247d9b6bb9b2479aa.img $tuned_initrd"

title="Oracle Linux Server 8 (0-rescue-3f1be2ec0d247d9b6bb9b2479aa)"

id="3f1be2ec0d247d9b6bb9b2479aa-0-rescue"

[root@ol8 ~]#
```
图 3.4 – grubby 信息

有了这些内核细节，我们使用以下命令从内核参数中查看 grubby quiet 配置并添加新的 test 参数：

```bash
grubby --remove-args="quiet" --args=test --update-kernel /boot/vmlinux-0-rescue-3f1be2ec0d247d9b6bb9b2479aa
```

如你所示，我们使用了内核名称来更新该内核的参数（我们使用 `--remove-args` 属性移除一个配置，使用 `--args` 属性添加一个新的）。现在我们可以通过运行带有启动环境的 `grubby --info=$GRUB_ENV` 来检查参数是否发生了变化：

```bash
[root@vm-4 #]$ grubby --info=/boot/vmlinux-0-rescue-3f1be2ec0d247d9b6bb9b2479aa

index=4

kernel=/boot/vmlinux-0-rescue-3f1be2ec0d247d9b6bb9b2479aa

args="ro crashkernel-auto resume=/dev/mapper/ol-swap rd.lvm/root rd.lvm/swap quiet"

root="/dev/mapper/ol-root"

initrd="/boot/initramfs-0-rescue-3f1be2ec0d247d9b6bb9b2479aa.img $tuned_initrd"

title="Oracle Linux Server 8 (0-rescue-3f1be2ec0d247d9b6bb9b2479aa)"

id="3f1be2ec0d247d9b6bb9b2479aa-0-rescue"
```



在更改后使用 `ALL` 选项

## 它是如何运行的...

如之前所述，Oracle Linux 带有两种口味的内核：UEK（Oracle 默认的 Linux 口味）以及与 RHEL 内核兼容的 RHCK。无论使用哪种内核，操作系统的其他部分都是相同的；它具有相同的应用程序、库和位置。本节将教你如何将默认内核（UEK）切换到 RHCK，反之亦然。首先，我们将使用 `grubby` 命令检查正在使用的默认内核，再次使用 `grubby --info=DEFAULT` 和 `grubby --info=ALL` 检查系统中所有可用内核。这两个命令之间的区别在于 `DEFAULT` 选项，它只显示启动信息

```
[root@ol18 #]$ grubby --ALL

index=0

kernel=vmlinux-5.15.0-8.91.4.1.el8uek.x86_64 $tuned

args=root crashkernel-auto resume=/dev/mapper/ol-swap rd.lvm/root rd.lvm/swap

root=/dev/mapper/ol-root

initrd=/boot/initramfs-5.15.0-8.91.4.1.el8uek.x86_64

title="Oracle Linux Server 8 (5.15.0-8.91.4.1.el8uek)"

id=3f1be2ec0d247d9b6bb9b2479aa-5.15.0-8.91.4.1.el8uek

kernel=vmlinux-4.18.0-425.13.1.el8ue7

args=ro crashkernel-auto resume=/dev/mapper/ol-swap rd.lvm/root rd.lvm/swap quiet

root=/dev/mapper/ol-root

initrd=/boot/initramfs-4.18.0-425.13.1.el8ue7.img $tuned_initrd

title="Oracle Linux Server 8 (4.18.0-425.13.1.el8ue7)"

[root@ol18 ~]#
```

```
3f1be2ec0d247d9b6bb9b2479aa-4.18.0-425.13.1.el8ue7
[root@ol18 ~]#
```

图 3.6 - RHCK 之前的内核版本

在前面的示例中，你可以看到在这种情况下使用的内核是 `/boot/vmlinux-5.15.0-8.91.4.1.el8uek.x86_64`，它是 UEK 口味的内核。UEK 系统应该始终包含 uve el。

你也可以使用 `-a` 命令检查当前内核：

```
[root@ol18 #]$ uname -a
Linux ol18.m57.5.15.0-8.91.4.1.el8uek.x86_64 #2 SMP Tue Mar 17 18:28:34 PST 2023
x86_64 x86_64 x86_64 GNU/Linux
[root@ol18 ~]$
```

对于系统上所有可内核，我们可以使用之前运行 `grubby -info` 命令的数据，或者使用 `rpm -qa kernel*core*` 命令：

```
[root@ol8 ~]# rpm -qa kernel*core*
kernel-uek-core-5.15.0-3.60.94.1.el8uek.x86_64
kernel-uek-core-5.15.0-3.60.5.1.el8uek.x86_64
kernel-core-4.18.0-425.13.1.el18_7.x86_64
kernel-core-4.18.0-425.3.1.el18_x86_64
[root@ol8 ~]#
```

在检查所有内核时，我们可以快速识别出两个版本的 UEK 和两个版本的 RHCK。在本例中，我们将使用 RHCK 版本 4.18.0-425.13.1.el18_7，它在 `/boot/vmlinuz --set-default` 命令中启动以使 RHCK 成为新的默认内核。然后我们使用 `grubby --info=DEFAULT` 检查默认内核。

```
[root@ol8 ~]# --set-default /boot/vmlinuz-4.18.0-425.13.1.el18_7.x86_64
The default is /boot/loader/entries/3fibe2ec0d2ed0427d4db6bb3924972aal1-4.18.0-425.13.1.el18_7.64.conf with 2 kernels and grubby /boot/vmlinuz-4.18.0-425.13.1.el18_7.x86_64
[root@ol8 ~]# --info=DEFAULT
index=2
kernel: /boot/vmlinuz-4.18.0-425.13.1.el18_7.x86_64
args="* crashkernel-auto resume=/mapper/ol-swap rd.lvvm=/root rd.lvvm=ol/sw
aw wphgb $tuned_params"
root=/dev/mapper/root/"
initrd=/boot/initramfs-4.18.0-425.13.1.el18_7.img Stuned initrd
title=Linux Generic (4.18.0-425.13.1.el18.7) 8.7"
id=3fibe2ec0d2ed0427d4db6bb3924972aal1-4.18.0-425.13.1.el18_7.x86_64
```

这并不是我们想要的。我们想要切换回之前的 RHCK 版本的内核。要做到这一点，你需要再次运行 `grubby --set-default` 命令，但这次要指定你想要的 RHCK 版本名称。

## 玩 UEFI

黑客攻击系统的一种方法是在系统启动之前攻击安全系统。为了防止这一点，我们必须确保操作系统仅由硬件制造商信任的软件启动。要解决这个问题，需要一种新方法来启动，UEFI 已实现并已成为硬件与操作系统之间的接口，取代了旧的 BIOS 固件。UEFI 的功能是安全启动（Secure Boot），它通过使用密码校验和和签名来确保代码在加载操作系统之前经过了验证。如果该功能可用，系统也可以通过传统的 BIOS 模式启动。

## 准备工作

要在 UEFI 模式下启动，Oracle Linux 需要在系统安装期间存在 UEFI 固件。GPT 自动设置 `/boot/efi` 创建了 ESP 分区，包含了 UEFI 启动所需的文件。GPT 是在物理磁盘上存储信息的方式，GPT 不受 MBR 的限制（例如分区数量和大小限制取决于操作系统）。GPT 是 UEFI 要求的分区表类型。

## MBR 与 GPT

对于硬盘和固态硬盘等存储设备的分区方案，MBR 和 GPT 是两个选择。为了区分两者，这里是容量方面的差异：

- 分区容量：

  - MBR：你的计算机 MBR 允许四个主分区或三个主分区加一个扩展分区（可以进一步分为多个逻辑分区）。然而，它的最大大小限制为 2 TB。

  - GPT：默认情况下，GPT 支持 128 个分区且不受数量限制。此外，它可以容纳高达 9ZB 的大小。

- 兼容性：

  - MBR：MBR 与旧系统和操作系统兼容，并被基于 BIOS 的计算机广泛支持。

  - GPT：使用 UEFI 代替 BIOS 的现代系统具有更好的兼容性。这种分区方案由大多数现代操作系统（如 Windows、macOS 和 Linux）。

在决定使用 MBR 还是 GPT 时，考虑到磁盘大小、所需的分区数量、兼容性需求以及你计划使用的操作系统很重要。对于大磁盘和新系统，GPT 通常是更好的选择，而 MBR 对于旧系统或需要与旧进程兼容的小磁盘仍然可行。

## 如何操作...

让我们运行 `df -h` 命令查看系统中的分区。请注意在此示例中 `/boot/efi` 挂载在 `/dev/sda` 分区上：



```
root@demo2 ~# df -h
Filesystem      Size Used Avail Mounted on
tmpfs           16G   0    16G   0% /dev
tmpfs           16G   0    16G   0% /dev/sh
tmpfs           16G   90M   16G   1% /run
tmpfs           16G   0    16G   0% /sys/fs
/dev/mapper/ol-root 50G   21G   30G  41% /
/dev/mapper/ol-u01 4.7G   66M   4.6G  2% /usr-01
/dev/mapper/ol-home 10G   244M  9.8G   3% /home
/dev/mapper/ol-var 4.7G   1.8G   2.9G  47% /var
/dev/sda2       101M   66M   34M  66% /boot
/dev/mapper/ol-var_log 4.7G  139M   4.6G  3% /var/log
/dev/sda1       200M   10M   190M   5% /boot/efi
tmpfs           3.2G    0    3.2G   0% /run
root@demo2 ~#
```

![](img/110fa0d6324f0893fff03cee6394144d_105_0.png)

如果你运行 `ls /boot/efi/redhat`，此目录包含一个名为 `shim64.efi` 的第一阶段引导程序、一个名为 `grub64.efi` 的 GRUB 加载程序以及名为 `grub.cfg` 的 GRUB2 配置文件。`grub.cfg` 的位置在 BIOS 中不同，因为它位于 `/boot/grub`：

```
root@demo2 ~# ls /boot/efi/redhat
total 412
drwxr-xr-x 2 root root      134 Aug 27 15:51 BOOT64.CSV
drwxr-xr-x 2 root root     4096 Oct 15 19:59 forfs
-rw-r--r-- 1 root root      6545 Feb 14 20:45 grub.cfg
drwxr-xr-x 1 root root     1024 Feb 14 22:31 grub2
-rw-r--r-- 1 root root     1024 Feb 14 21:15 grubenv
drwxr-xr-x 1 root root     1024 (Wait, the original text cut off, but it is likely 1024)
```

`/etc/default/grub` 文件负责包含 `grub.cfg` 用户设置。请注意该文件位于 BIOS 的相同位置。此外，如果你对文件进行任何更改，都需要重建 `grub`。

```
Boot0003* EFI Internal Shell Fvcol(7cb8bd9-f8eb-4f34-aaea-3ee465164)\PvFile(7c04a583-9a3e-4fic-ad65-e05268dbd4d1)
Boot0004* Oracle Linux HD (HD,1.dff50c5d-96ed-460-9823-212469b405db,0.800,0.1x2000)/File(\EFI\redhat\shimx64.efi)
```

如前面的示例所示，启动 0004 (Oracle Linux) 是用于启动当前系统的启动项，称为 `BootCurrent`。`BootOrder` 是启动管理器中的启动顺序；因此，启动管理器将启动列表中的第一个项目。如果启动失败，它将尝试下一个条目，依此类推。如果你在系统上使用 UEFI，`efibootmgr` 是一个方便的命令行工具，允许你管理 EFI 启动项。通过此实用实用，你可以轻松在 EFI 启动管理器中创建、修改和删除启动项。

如果你想删除启动项，可以使用 `-b` 选项。在这种情况下，我们将使用以下命令删除 CDROM 记录 (0001)：

```
efibootmgr -b 0001 -B
```

你也可以用 `-o` 选项更改启动顺序。在以下命令中，我们将更改启动顺序以设置默认启动项：

```
efibootmgr -o 0003,0004,0002
```

请使用 `man` 命令学习更多关于 `efibootmgr` 命令的信息。

## 警告

更改配置时务必小心。不小心将启动顺序更改为不可引导设备可能会导致你处于恢复系统的困境。如果你在无法访问控制台的环境运行，这一点更为重要。

# 玩转安全启动 (Secure Boot)

安全启动是 UEFI 中实现的一项可选功能，旨在防止在启动过程中执行恶意软件。要启用或禁用安全启动，你需要访问特定的 UEFI 设置程序。每个系统制造商的情况都不同。请检查系统文档以查看如何访问 UEFI 配置。

安全启动的步骤与常规 UEFI 启动相同，但一个重要的异常是，它要求组件经过签名和验证才能被加载和执行（使用公私密钥对进行验证）。它由两个信任根 (RoT) 构建构建传递链：

- 验证信任根负责签名的验证。验证信任根是启动信任根，这也是大多数人在谈论安全启动时所指的内容，它将位于闪存驱动器上作为存储信任根以保护密钥数据库。仅在驱动程序执行环境 (DXE) 阶段之后验证，而不是在安全 (SEC) 阶段。
- 测量信任根负责测量值的收集。

安全启动将通过以下过程建立信任链：

- 1. 首先，第一阶段引导加载程序 (`shim`) 由 Oracle 签名并经过微软验证；然后，它加载 GRUB 2 加载器。
- 2. GRUB 2 启动加载器在加载和执行内核之前验证由 Oracle 签名的内核签名并进行验证。
- 3. 由 Oracle 签名的内核通过验证并执行。安全启动仅加载已签名/验证的内核模块（例如，内核 RPM 中包含的所有内核模块以及与 Oracle Ksplice 使用的模块都具有相应的 Oracle 签名，签名/验证的内核模块将运行，否则不会加载）。

现在我们已经涵盖了安全启动的基本知识，让我们学习如何通过它为内核模块签名。首先，如果你可以对模块进行签名，你需要安装几个所需的软件包，包括内核源码。此外，你还需要创建一个签名证书的密钥对（私钥和公钥）。私钥用于签名内核模块，公钥也添加到安全启动的内核密钥环中以允许系统验证签名。

## 准备工作

第一步是安装开发库。通过以下命令完成：

```
[root@demo2]# dnf install kernel-devel$(uname -r)
```

### 注意

在运行 `dnf install kernel-devel` 时，添加 `uname` 命令可以确保你安装的是当前运行内核的开发包。此外，不要忘记更新开发包。作为良好的做法，始终更新系统以确保你拥有最新的内核和相关包：

```
[root@demo2]# dnf update
```

此更新可能需要时间，取决于补丁情况。如果你使用的是 UEFI，编译模块所需的内核头文件在 `kernel-devel` 中。当使用 UEFI 安全启动功能时，如果你运行的不是最新内核版本，建议安装并使用 UEFI 来执行模块操作所需的实用工具（`openssl`、`keyutils` 和 `pesign`）：

```
[root@demo2]# dnf -y install openssl keyutils pesign
```

如果你需要从源码构建模块，可以可选安装 Development Tools 组以确保工具可用：

```
[root@demo2]# dnf -y group install "Development Tools"
```

## 如何操作

创建一个 OpenSSL 在生成证书时用于获取默认值的配置文件。你可以在任何位置创建此文件，但将其与 `/etc/ssl/x509.conf` 中的其他 OpenSSL 配置放在一起是有用的。该文件应该类似于：

```
[req]
default_bits = 4096
distinguished_name
prompt = no
string = utf8
extensions =

[distinguished_name]
O = Module Signing
CN = Module Signing Key
email = last@example.com

[extensions]
basicConstraints=critical,CA=FALSE
keyUsage=codeSigning
extendedKeyUsage=
```

你应该编辑 `O`、`CN` 和 `email` 字段使其更合适。注意在配置的 `extensions` 部分，`keyUsage` 字段被设置为 `digitalSignature`。此外，为了与验证工具兼容，`extendedKeyUsage` 选项被设置为 `codeSigning`。

使用此配置生成新的密钥对：



```
[root@demo2]# openssl req -x509 -new -nodes -utf8 -sha512 -days 3650 -batch -config /etc/ssl/x509.conf -form DER -out /etc/ssl/certs/pubkey.der -keyout /etc/ssl/certs/priv.key
Generating RSA private key
****
****
writing new private key to '/etc/ssl/certs/priv.key'
[root@demo2]#
```

此签名证书有效期为 10 年（3650 天）。确保密钥得到充分保护。可以通过将密钥离开服务器并存储在安全位置来实现。将密钥放在 U 盘并放在抽屉里并不是安全位置。锁锁的位置，例如保险箱。

```
[root@demo2]# openssl x509 -inform DER -in /etc/ssl/certs/pubkey.der -out /etc/ssl/certs/pubkey.pem
[root@demo2]#
```

## 签名模块

`sign-file` 实用工具确保模块对内核进行了正确签名。该工具位于内核源码内部。以下指令假设你正在为当前运行的内核签名模块。如果你打算为不同的内核签名模块，必须提供正确内核版本源码中 `sign-file` 实用工具的路径。如果你不使用正确的工具，模块的签名类型可能与预期的签名类型不匹配。

要签名模块，请运行当前运行内核的 `sign-file` 实用工具，并提供你为签名模块创建的私钥和公钥路径（例如，我使用名为 `hello` 的模块）：

```
[root@demo2]# sudo /usr/src/kernels/$(uname -r)/scripts/sign-file sha512 /etc/ssl/certs/priv.key /etc/ssl/certs/pubkey.der /lib/modules/$(uname -r)/extra/hello.ko
```

注意模块应该安装到 `/lib/modules/`，你需要提供模块的正确路径。

## 更新所有者密钥数据库

机器所有者密钥 `MOK` 是一种安全功能，旨在保护计算机系统的启动过程免受未经的修改或攻击。它通常用于支持 UEFI 和安全启动的系统，这些系统要求所有引导加载程序和内核模块都由受信任实体签名。

`MOK` 数据库存储在系统固件内的非易失性内存位置，包含允许对引导加载程序和内核模块签名的密钥列表。`MOK` 数据库中的每个密钥都与唯一标识符关联，并用于验证引导加载程序和内核模块的数字签名。如果数字签名无效，启动将继续但软件不会加载；启动将停止且系统不会启动。

要注册 `MOK` 密钥，你必须在每个目标系统上使用 UEFI 系统控制台手动进行。

由于你创建的密钥未包含在 UEFI 安全启动数据库中，你需要使用 `mokutil` 命令在 shim 中向 `MOK` 数据库注册：

`mokutil --import /etc/ssl/certs/pubkey.der`

上一个命令会提示你输入一个一次性密码，你将在重启系统后，`MOK` 管理服务注册密钥时使用该密码。

## 重启系统

- 1. UEFI 应该在启动时自动启动 shim UEFI 密钥管理器，如下图所示。如果你在 10 秒内没有按下任何键，你将无法注册你的 `MOK` 密钥：

![](img/110fa0d6324f0893fff03cee6394144d_111_0.png)

图 3.11 - Shim 实用程序

按任意键继续。

- 2. 随后，你将看到 shim 主菜单。从菜单中选择 Enroll MOK（注册 MOK）。

![](img/110fa0d6324f0893fff03cee6394144d_111_1.png)

图 3.12 – Shim 主菜单

这将允许你继续注册密钥或查看密钥。

- 3. 从菜单中选择 View key 0（查看密钥 0）（如下所示）以显示密钥详情。

![](img/110fa0d6324f0893fff03cee6394144d_112_0.png)

图 3.13 – 查看密钥

- 4. 随后将显示密钥详情。验证所展示的值是否与你用于签名模块并插入内核映像的密钥相匹配：

图 3.14 – 密钥详情

然后按任意键返回 Enroll MOK 菜单。

- 5. 从菜单中选择 Continue（继续）。

- 6. 将显示 Enroll the key(s)?（注册密钥？）屏幕，你现在可以从菜单中选择 Yes（是）（如下图所示）。

![](img/110fa0d6324f0893fff03cee6394144d_113_0.png)

图 3.15 – 注册密钥

选择 Yes 以注册密钥。

- 7. 系统将提示你输入密码。输入你使用 `mokutil` 命令导入密钥时使用的密码。

密钥已注册到 UEFI Secure Boot 密钥数据库。

- 8. 你现在被重定向到主菜单。从菜单中选择 Reboot（重启）。

![](img/110fa0d6324f0893fff03cee6394144d_113_1.png)

图 3.16 – 完成后重启

# 工作原理

启动系统后，你可以验证某个密钥是否包含在相应的内核密钥环（keyringing）中。验证取决于你正在运行的内核版本。此外，你需要检查的密钥名称也所不同，因为实现方式随着内核版本的变化而变化。

如果为自定义模块生成的密钥列在正确的密钥环中，你就可以可以在 Secure Boot（安全启动）模式下加载由该密钥签名的模块。

对于 Oracle Linux 8 上的 RHCK 以及 UEK R6 或更高版本的内核，`built_trusted_keys` 密钥环和 `platform` 密钥环中的密钥对于模块签名和 kexec 文本都是受信任的，这意味着我们可以按照标准程序为密钥环中的密钥对在 `MOK` 数据库中签名模块，并且它会被自动信任。

由于密钥被加载到 `builtin_trusted_keys` 密钥环中，你应该同时检查两个密钥环的模块签名。以下是一个示例：

```
[root@demos2 ~]# keyctl show %:builtin_trusted_keys
Keyring
718980521--swrv 0 0 keyring: .builtin_trusted_keys
895270521--swrv 0 0 asymmetric: Oracle CA Server
235653a3b7ec77a9b0526a411c5a5a5d7
643918572--swrv 0 0 asymmetric: Oracle IMA signing CA:
a2ef2897a05948027f1d4904ae1e8e46e4651
668b1900--swrv 0 0 asymmetric: Oracle America, Inc.: Ksplice Kernel Module Key: 09901d06f5a4f5c5b2ef251e8277b5ee4c
35441076--swrv 0 0 asymmetric: Oracle Linux Signing Key: 3b55241296a269a3f5be026173de8e53f
[root@demos2 ~]# keyctl show %:platform
85804605--swrv 0 0 keyring: .platform
88615021--swrv 0 0 asymmetric: Oracle America, Inc.: 43c0d551c25357b8c44edcf5d49263
69874825--swrv 0 0 asymmetric: Oracle America, Inc.: 2e7c7201d5cd5f254c93deca7ae5f96c0f
79069521--swrv 0 0 asymmetric: Oracle America, Inc.: 95c33553--swrv 0 0 asymmetric: 77b979
```

由于一个密钥被加载到 `builtin_trusted_keys` 密钥环中，你应该检查两个密钥环的模块签名。

# TrustBoot 增强安全性和完整性

TrustBoot 允许在 Secure Boot 模式下运行，确保只有受信任的软件在系统上执行。这防止了执行可能损害系统的恶意软件。

TrustBoot 通过通过在运行时验证软件和数据的完整性，确保系统在启动后依然保持安全。它利用了 Intel SGX 和 AMD SEV 等技术提供硬件级隔离和证明。

TrustBoot 是一个平台无关的，可以在不同的硬件平台上使用，包括 x86、Arm 和 RISC-V。

TrustBoot 是一个开源项目，这意味着任何人都可以检查代码并为其开发贡献。这使得 TrustBoot 更加透明和可信赖。

## 准备工作

TrustBoot 的一个功能功能是 TrustBoot 允许在 UEFI 。 。请参考以下图：



![](img/110fa0d6324f0893fff03cee6394144d_115_0.png)

图 3.17 – TrustBoot 概述

### 注意

你可以通过阅读 kernel.org 存档看到 Oracle 的一些努力：https://lore.kernel.org/lkml/2023050415023.835096-1-ross.oracle.com/

# 工作原理

TrustBoot Loader 由 Linux 和 u-root 等知名组件组成。让我们仔细查看主要组件：

- 启用了 TrustBoot 的内核集成 u-root initfs
- 作为 u-root 扩展的 TrustBoot 安全引擎
- 可由引导程序加载的新映像

此构建过程所示：

![](img/110fa0d6324f0893fff03cee6394144d_116_0.png)

图 3.18 – TrustBoot 映像过程

使用 TrustBoot 的主要优势如下：

- **安全启动**：TrustBoot 提供了一个安全启动过程，确保系统上只执行受信任的软件。这防止了可能损害系统的恶意软件的执行。
- **运行时完整性**：TrustBoot 通过在运行时验证软件和数据的完整性，确保系统在启动后保持安全。它利用 Intel SGX 和 AMD SEV 等技术提供硬件隔离和证明。
- **防御攻击**：TrustBoot 针对各种类型的攻击提供了保护，包括固件攻击、恶意软件和内核根 root程序。
- **平台无关**：TrustBoot 是平台无关的，可以在不同的硬件平台上使用，包括 x86、Arm、RISC-V。
- **开源**：TrustBoot 是一个开源项目，这意味着任何人都可以检查代码并为其开发贡献。

# 移除 RHCK

在本教程中，你将学习如何移除 RHCK 及其独特的包依赖，同时保留所有依赖。请记住，在安装 Oracle Linux 时，安装程序会自动安装 Oracle UEK 作为默认内核，但你可以为了兼容性安装 RHCK。

## 如何操作

让我们看看如何从系统中移除 RHCK：

1. 首先，让我们使用 `grubby` 命令检查系统中运行的所有内核：

```bash
[root@ol8 ~#] grubby --ALL
index=0
kernel=/boot/vmlinux-5.15.0-8.91.4.1.el8uek.x86_64
args=ro crashkernel-auto resume=/dev/mapper/ol-swap root.lv=/root root.lv-ol/s rw rh quiet $tuned_params
root=/dev/mapper/ol-root
initrd=/boot/initramfs-5.15.0-8.91.4.1.el8uek.x86_64 $img $tuned_initrd
title="Oracle Linux Server 8 (5.15.0-8.91.4.1.el8uek.x86_64)"
id=3f12beec0d247d9bb3922429792aaal-5.15.0-8.91.4.1.el8uek.x86_64
index=1
kernel=/boot/vmlinux-5.15.0-60.5.1.el8uek.x86_64
args=ro crashkernel-auto resume=/dev/mapper/ol-swap root.lv=/root root.lv-ol/s rw rh quiet $tuned_params
root=/dev/mapper/ol-root
initrd=/boot/initramfs-5.15.0-60.5.1.el8uek.x86_64 $img $tuned_initrd
title="Oracle Linux Server 8 (5.15.0-60.5.1.el8uek.x86_64)"
id=3f12beec0d247d9bb3922429792aaal-5.15.0-60.5.1.el8uek.x86_64
index=2
kernel=/boot/vmlinux-4.18.0-425.13.1.el18_7.x86_64
args=ro crashkernel-auto resume=/dev/mapper/ol-swap root.lv=/root root.lv-ol/s rw rh quiet $tuned_params
root=/dev/mapper/ol-root
initrd=/boot/initramfs-4.18.0-425.13.1.el18_7.x86_64 $img $tuned_initrd
title="Oracle Linux Server 8 (4.18.0-425.13.1.el18_7.x86_64)"
id=3f12beec0d247d9bb3922429792aaal-4.18.0-425.13.1.el18_7.x86_64
index=3
kernel=/boot/vmlinux-4.18.0-425.13.1.el18.x86_64
args=ro crashkernel-auto resume=/dev/mapper/ol-swap root.lv=/root root.lv-ol/s rw rh quiet $tuned_initrd
root=/dev/mapper/ol-root
initrd=/boot/initramfs-rescue-3f12beec0d247d9bb3922429792aaal $img $tuned_initrd
title="Oracle Linux Server 8 (4.18.0-425.13.1.el18.x86_64)"
id=3f12beec0d247d9bb3922429792aaal-0-rescue
[root@ol8 ~#]
```

![](img/110fa0d6324f0893fff03cee6394144d_118_0.png)

我们可以从前面的输出中看到，默认内核为 `/boot/vmlinux-5.15.0-8.91.4.1.el8uek.x86_64`，它是一个 UEK 内核；我们可以看到安装了多个类型的 RHCK（红帽兼容内核），即 `/boot/vmlinux-4.18.0-425.13.1.el18_7.x86_64` 和 `/boot/vmlinux-4.18.0-425.13.1.el18.x86_64`，我们可以安全地删除它们。

2. 现在既然我们知道正在使用 UEK，可以在 Oracle Linux 机器上使用 `dnf remove kernel` 命令安全地删除所需的 RHCK。它将检测到未使用的内核并显示它们的依赖关系。



```bash
[root@ol8 ~#] dnf remove kernel
Dependencies resolved.
=================================================================================
Package         Arch            Repository               Size
=================================================================================
Removing:
  kernel          x86_64          4.18.0-425.3.1.el8         @anaconda               0
  kernel          x86_64          4.18.0-425.13.1.el8_7      @ol8_base_latest      0
================================================================================
Transaction Summary
================================================================================
Remove 2 Packages
Free space: 0
Is this [y/N]: y
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction:
  Erasing: kernel-4.18.0-425.3.1.el8_7      1/2
  Erasing: kernel-4.18.0-425.13.1.el8_7    1/2
Running scriptlet: kernel-4.18.0-425.3.1.el8_7      1/2
Running scriptlet: kernel-4.18.0-425.3.1.el8_7      2/2
Running scriptlet: kernel-4.18.0-425.13.1.el8_7      2/2
Verifying: kernel-4.18.0-425.3.1.el8_7      1/2
Verifying: kernel-4.18.0-425.13.1.el8_7      2/2
================================================================================
Removed:
  kernel-4.18.0-425.3.1.el8_7          kernel-4.18.0-425.13.1.el8_7
================================================================================
Complete!
[root@ol8 ~]#
```

如图 3.20 所示，安装的 RHCK 已从系统中删除。现在再次运行 `grubby` 命令查看 RHCK 是否已从启动选项中移除。不要再次运行 `dnf remove kernel`，这可能会意外删除引导内核内核导致系统无法启动。

```bash
[root@ol8 ~]# grubby --ALL
index=0
kernel=/boot/vmlinux-5.15.0-8.91.4.1.el8uek.x86_64
args=ro crashkernel-auto resume=/dev/mapper/ol-swap root.lv=/root root.lv-ol/s rw quiet $tuned_params
root=/dev/mapper/ol-root
initrd=/boot/initramfs-5.15.0-8.91.4.1.el8uek.x86_64 $img $tuned_initrd
title="Oracle Linux Server 8 (5.15.0-8.91.4.1.el8uek.x86_64)"
id=3f12beec0d247d9bb3922429792aaal-5.15.0-8.91.4.1.el8uek.x86_64
index=1
kernel=/boot/vmlinux-5.15.0-60.5.1.el8uek.x86_64
args=ro crashkernel-auto resume=/dev/mapper/ol-swap root.lv=/root root.lv-ol/s rw quiet $tuned_params
root=/dev/mapper/ol-root
initrd=/boot/initramfs-5.15.0-60.5.1.el8uek.x86_64 $img $tuned_initrd
title="Oracle Linux Server 8 (5.15.0-60.5.1.el8uek.x86_64)"
id=3f12beec0d247d9bb3922429792aaal-5.15.0-60.5.1.el8uek.x86_64
index=2
kernel=/boot/vmlinux-4.18.0-425.13.1.el18_7.x86_64
args=ro crashkernel-auto resume=/dev/mapper/ol-swap root.lv=/root root.lv-ol/s rw quiet $tuned_params
root=/dev/mapper/ol-root
initrd=/boot/initramfs-4.18.0-425.13.1.el18_7.x86_64 $img $tuned_initrd
title="Oracle Linux Server 8 (4.18.0-425.13.1.el18_7.x86_64)"
id=3f12beec0d247d9bb3922429792aaal-4.18.0-425.13.1.el18_7.x86_64
index=3
kernel=/boot/vmlinux-4.18.0-425.13.1.el18.x86_64
args=ro crashkernel-auto resume=/dev/mapper/ol-swap root.lv=/root root.lv-ol/s rw quiet $tuned_initrd
root=/dev/mapper/ol-root
initrd=/boot/initramfs-rescue-3f12beec0d247d9bb3922429792aaal $img $tuned_initrd
title="Oracle Linux Server 8 (4.18.0-425.13.1.el18.x86_64)"
id=3f12beec0d247d9bb3922429792aaal-0-rescue
```

遗憾的是，两个内核仍然那里。RHCK 包仅仅是一个元数据包，其目的是确保所有依赖包都正确安装。换句话说，删除内核不会删除任何加载程序。要解决这个问题，我们需要使用 `dnf kernel-core` 删除所有 `kernel-core` 包：

| Name | Architecture | Repository | Size |
| :--- | :--- | :--- | :--- |
| kernel | x86_64 | 4.18.0-425.3..el8.1 | - | 70 M |
| kernel-core | x86_64 | 4.18.0-425.13.1.el8_7 | el8_base_latest | 70 M |
| kernel-packages | x86_64 | 4.18.0-523.el8.1 |88base__ | 117 k |
| NetworkManager-dispatcher | x86_64 | 0:28.14-10.el8 |.8_base_latest | 25 k |
| NetworkManager | x86_64 | 0:28.14-10.el8 |el8_base_latest | 250 k |
| kernel-modules | x86_64 | 4.18.0-323.el8.2 | - | 111 M |
| kernel-devel | x86_64 | 4.18.0-323.el8.2 | - | 311 M |
| kernel-headers | x86_64 | 35.16.12.el8.11 | AppStream | 375 k |
| kernel-tools | x86_64 | 35.16.12.el8.1 | AppStream | 112 k |
| anaconda-help | x86_64 | 35.16.12.el8.11 | AppStream | 915 k |



| anaconda-widgets | x86_64 | 35.16.12.el8.11 | AppStream | 1.12 M |
| glibc | x86_64 | 2.28-22.el8.64 | - | 1.6 M |
| dnf | x86_64 | 73-12.11.el8.64 | - | 50 k |
| dnf-devel | x86_64 | 73-12.11.el8.64 | - | 90 k |
| NetworkManager-dispatcher:1:28.14-10.el8.x86_64 | | | |
| anaconda-help:1:35.16.12.el8.11.x86_64 | | | |
| anaconda-widgets:1:35.16.12.el8.11.x86_64 | | | |
| cal-libs:1:73-12.11.el8.64.x86_64 | | | |
| kernel-core:4.18.0-323.el8.11.x86_64 | | | |
| kernel-tools:4.18.0-323.el8.11.x86_64 | | | |
| kernel-modules:4.18.0-323.el8.2.x86_64 | | | |
| kernel-devel:4.18.0-323.el8.2.x86_64 | | | |
| libblkid:2:28-22.el8_64.x86_64 | | | |
| libblkid-common:2:28-22.el8_64.x86_64 | | | |
| libblkid-devel:2:28-22.el8_64.x86_64 | | | |
| libcap:1:28-22.el8_64.x86_64 | | | |
| libgpg:1:28-22.el8_64.x86_64 | | | |
| libgpg-devel:1:28-22.el8_64.x86_64 | | | |
| libgrypt:1:28-22.el8_64.x86_64 | | | |
| libnsl:1:28-22.el8_64.x86_64 | | | |
| libnsl-devel:1:28-22.el8_64.x86_64 | | | |
| libgcc:1:0.34-22.el8_64.x86_64 | | | |
| libpython:3.6.13-9.el8_64.x86_64 | | | |
| libpython-devel:3.6.13-9.el8_64.x86_64 | | | |
| libselinux:2:2.5-10.el8_64.x86_64 | | | |
| libselinux-devel:2:2.5-10.el8_64.x86_64 | | | |
| libtool:2:2.4.1-22.el8_64.x86_64 | | | |
| libtool-devel:2:2.4.1-22.el8_64.x86_64 | | | |
| libxml2:2.2.9.10-17.el8_64 | | | |
| libxml2-devel:2.2.9.10-17.el8_64 | | | |

如你现在看到的，所有的 RHCs 都从我们的系统中移除了。

此外，如果你以后决定恢复已删除的 RHCs，你可以使用 `dnf install kernel` 命令快速恢复它们：

```bash
[root@localhost ~]# dnf install kernel
Last metadata expiration check: 03:34:36 on Sun 19 Mar 2023 03:34:19 PM EDT.
Dependencies resolved.
Package                 Architecture      Version                Size
Installing:
kernel                  x86_64              4.18.0-425.123.1.el8_7  oel8_latest             8.8 M
Installing dependencies:
kernel                  x86_64              4.18.0-425.123.1.el8_7  oel8_latest             41 M
kernel-modules          x86_64              4.18.0-425.123.1.el8_7  oel8_latest             33 M
Transaction Summary
Install 3 Packages
Total download size: 83 M
Installed size: 83 M
(1/3) kernel-4.18.0-425.123.1.el8_7.x86_64.rpm      23 MB/s | 0.0 MB/s 00:00
(2/3) kernel-modules-4.18.0-425.123.1.el8_7.x86_64.rpm 39 MB/s | 0 MB/s 00:00
(3/3) kernel-modules-core-4.18.0-425.123.1.el8_7.x86_64.rpm 41 MB/s | 1 MB/s 00:00
Total                                                83 MB/s | 83 MB/s 00:01
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
Preparing
Installing:      kernel-core-4.18.0-425.123.1.el8_7.x86_64 1/3
Running scriptlet: kernel-core-4.18.0-425.123.1.el8_7.x86_64 1/3
```

图 3.24 – 重新安装 RHCK

如你所见，在 Oracle Linux 上，安装内核与从操作系统中移除内核一样简单。当你有机会时，比较一下 RHCK 和 UEK 之间的系统性能；你会发现更现代的 UEK 处理 I/O 等任务的速度快得让你感到惊喜。

# 4

## 创建和管理单实例文件系统

没有数据，系统就没有存在的理由，基于这一想法，数据必须存储在某个地方。在本章中，我们将介绍用于管理服务器本地数据的两种常用文件系统：B 树文件系统（Btrfs，读作 Butter FS）和扩展文件系统（XFS，读作 X FS）。

这些是单实例文件系统，基本上是指任何时候只能挂载到单台服务器上的文件系统。还有多实例文件系统同时挂载到多个系统上，Oracle 集群文件系统版本 2 `OCFS2` 和全局文件系统 2 `GFS2`。所有示例都使用共享存储作为底层存储。

此外，还有 Ceph，它不是缩写，而是指头乌类（cephalopod）。这是因为 Ceph 是一种分布式架构，数据存储在 Ceph 集群的节点上。这使得 Ceph 能够提供可扩展存储，但增加了一些复杂性。Gl 是另一个分布式系统的示例。

### 注意

为什么不使用 ZFS？因为 Btrfs 和 XFS 构建在 Oracle Linux 无破企业内核 `UEK` 中，而 ZFS 不在第三方仓库中可用。

我们将涵盖以下配方，帮助你理解和管理文件系统：

- 关于文件系统你需要了解的知识
- Btrfs - 创建、调整大小
- Btrfs - 子卷、快照、配额及更多
- 使用 `mdadm` 保护数据
- 逻辑卷
- XFS - 创建、修改及更多

## 技术要求

对于本配方，你需要 Oracle Linux 8。在大多数配方中，推荐使用虚拟化产品，如 VirtualBox。具有两个核心、2 GB 内存和几 GB 磁盘空间的虚拟机即可。在开始之前，将你的系统更新到最新软件包，这只需要几分钟，就能节省大量排除配置问题的时间。参考 https://github.com/Oracle-Linux-Cookbook。

## 关于文件系统你需要了解的

本配方将讨论本地文件系统与远程文件系统的区别，以及 Btrfs 和 ZFS 之间的核心差异。操作系统 `OS` 的骨干是本地文件系统，它允许在固态硬盘、逻辑单元 `LUNs` 以及存储区域网络 `SAN` 或云上存储文件和目录。这些文件系统专门为本地管理设计，保护文件免受意外删除或损坏。它们具备文件权限、所有权访问控制等功能，为用户提供最大的安全性。与远程文件系统相比，本地文件系统提供了卓越的性能，尽管在配合 RAID 技术时。本地文件系统示例包括 Btrfs、XFS、ext4、fat32 甚至 ZFS。

### 注意

ZFS 是一个本地文件系统，它没有包含在内核中，需要使用软件添加。



远程文件系统允许你通过网络访问远程服务器上的文件和目录。该系统提供了像存储在本地一样访问和操纵文件的便利性。远程文件系统被广泛用于分布式计算环境，其中多台计算机或服务器需要共享数据和资源。它们在数据存储在远程并通过互联网访问的网络托管环境中也有价值。远程文件系统的示例包括网络文件系统 (`NFS`)、服务器消息块 (`SMB`) 和常用 (`CIFS`)，分别广泛用于 Unix、Linux 和 Windows 环境。然而，重要的是，在多个服务器之间使用远程文件系统会影响性能。为了管理 MySQL 和 Postgres 数据库获得最佳性能，强烈建议利用本地文件系统而不是远程文件系统。这种策略也适用于操作系统。

## 准备工作

你需要理解这两个文件系统之间的核心差异。`XFS` 文件系统比许多管理员认为的要得多。它于 1993 年作为 Silicon Graphics IRIX 操作系统的文件系统开始，并在2001 年移植到 Linux。`Btrfs` 则较新，于 2007 年作为 Linux 的一个开源项目被开发。`Btrfs` 不仅仅是一个文件系统，因为它将卷管理器、数据冗余和文件功能集成在了一项技术中。

对于 `XFS`，你需要将其与用于动态卷的卷管理器以及磁盘阵列 (`RAID`) 技术（最常用 `mdadm` 命令配置）结合使用提供容错。

| 类型 | 描述 | 性能 | 冗余 | |
| :--- | :--- | :--- | :--- | :--- |
| RAID 0 | 跨磁盘条纹 | 优 | 无 | 100% |
| RAID 1 | 镜像两个磁盘 | 好 | 单一磁盘故障 | 50% |
| RAID 10 | 镜像后条纹，至少 4 块磁盘 | 接近优 | 单一磁盘故障 | 50% |
| RAID1C3 | 元数据三副本，至少 3 块磁盘 | 中等 | 两个磁盘故障 | 66% |
| RAID1C4 | 元数据四副本，至少 4 块磁盘 | 最低 | 三个磁盘故障 | 75% |

表 4.1 – Btrfs RAID 选项

两个系统对最大文件大小的限制均为 8 EB字节。但 `Btrfs` 增加了快照、透明压缩、基于校验和的数据完整性以及回滚能力等功能。`XFS` 也没有被落下，通过 I/O 线程和更大的带宽具有更高的性能，尽管一旦你将 `XFS` 与 `LVM` 和 `RAID` 技术集成，这些优势可能无法实现。另一个主要区别是，`Btrfs` 要求你使用 `UEK` 和红帽兼容内核 (`RHCKs`)。

## 如何操作...

Oracle Linux 默认使用 `XFS` 文件系统，但在执行时，你可以使用 `Btrfs` 作为根文件系统。如果你想使用 `XFS` 作为启动文件系统，请像往常一样安装。如果你想使用 `Btrfs`，那么你应该继续。

### 注意

你的启动文件系统可以与服务器上的数据文件系统不同。你可以轻松地让根目录使用 `XFS` 而数据文件系统使用 `Btrfs`，反之亦然。

运行 `Btrfs` 最简单的方法是在使用 `UEK` 启动盘安装时选择它。这将让你能够选择 `Btrfs` 作为目标文件系统。运行安装时，选择**安装目标** (`Install Destination`)，然后选择自定义存储配置。这将为你提供手动分区选项，你可以在那里下拉菜单并选择 `Btrfs`，如下所示所示：

# 手动分区

# ORACLE LINUX 8.7 安装

![](img/110fa0d6324f0893fff03cee6394144d_127_0.png)

图 4.1 – Btrfs 选择

在设置自定义配置时，您可以为 `/var` 或 `/var/tmp` 添加额外的目录（这是**安全技术实施指南 (STIG)** 的要求）。这些实际上不仅仅是目录，而是主卷的子卷。这就是为什么它们显示相同的可用空间：

# 手动分区

# ORACLE LINUX 8.7 安装

![](img/110fa0d6324f0893fff03cee6394144d_128_0.png)

图 4.2 – Btrfs 挂载点

这是因为在 `Btrfs` 中，它们都使用同一个卷，并具有相同的可用磁盘空间。我们稍后可以使用配额（`quotas`）来限制这一点。

请使用您标准的网络和软件源设置完成安装，但请注意，您可能需要将安装源设置为 URL 或本地网络共享。如果您运行 8.7 或更版本，还需要添加 `UEK` 存储。

系统启动后，您将看到它现在正在使用 `Btrfs`。这可以在系统启动后进行检查。

## 工作原理...

您可以通过多种方式检查文件系统，最简单的方法是检查 `/etc/fstab` 以查看文件系统是如何挂载的。对应的截图如下：

```
[root@btfs]# # edit /etc/fstab

# /etc/fstab
# Created by anaconda on Sun May 14 01:31:56 2023
# accessible filesystems, by reference, are maintained under '/dev/disk/'
# See man pages fstab, findfs(5), mount(8) and/or bkid(8) for more info.

# After editing this file, use 'systemctl daemon-reload' to update system
# units generated from it.

UUID=55d5e0c6-b6b5-49a8-948b-335c36f9a49 btfs sub=root 0 0
UUID=55d5e0c6-b6b5-49a8-948b-335c36f9a449 btfs sub=boot 0 0
UUID=55d5e0c6-b6b5-49a8-948b-335c36f9a449 btfs sub=home 0 0
UUID=55d5e0c6-b6b5-49a8-948b-335c36f9a449 btfs sub=var 0 0
UUID=55d5e0c6-b6b5-49a8-948b-335c36f9a449 btfs sub=var_log 0 0
UUID=7ac1d941-afb6-43cd-9de6-e088ef26c3 swap defaults 0 0
[root@btfs]#
```

图 4.3 - Btrfs fstab 示例

您可以使用 `df` 命令配合 `-T` 来显示文件系统类型。运行以下命令将显示：

```
df -T
```

这将显示每个挂载文件的文件系统类型，如图所示：

| 文件系统类型 | 1K-块 | 可用 | 使用% | 挂载在 |
|---|---|---|---|---|
| devtmpfs | devtmpfs | 3894356 | 0 | 3894356 | 0% | /dev/ |
| tmpfs | tmpfs | 3912864 | 0 | 3912864 | 0% | /dev/shm |
| tmpfs | tmpfs | 3912864 | 16888 | 3929752 | 0% | /run |
| tmpfs | tmpfs | 3912864 | 0 | 3912864 | 0% | /sys/fs/cgroup |
| devsda | btrfs | 28145764 | 2460816 | 19674536 | 2% | / |
| devsda2 | btrfs | 28145764 | 2460816 | 19674536 | 2% | /var |
| devsda2 | btrfs | 28145764 | 2460816 | 19674536 | 2% | /home |
| devsda2 | btrfs | 28145764 | 2460816 | 19674536 | 2% | /boot |
| devsda2 | btrfs | 28145764 | 2460816 | 19674536 | 2% | /var/log |
| tmpfs | tmpfs | 782572 | 0 | 782572 | 0% | /run/user/ |

图 4.4 - 使用 Btrfs 文件系统的 df -T

## Btrfs – 创建、调整大小和监控

在本教程中，我们将创建一个 RAID6 Btrfs 卷和文件系统，使用多个磁盘进行容错存储。我们还将添加一个新卷并扩展文件系统。最后，我们将通过修改文件系统来对数据压缩：

### 准备工作

为了开始，我向操作系统添加了五个 10 GB 的硬盘。这些硬盘将用于构建一个新的 RAID1 卷。我可以通过 `fdisk -l` 查看这些新设备，并使用以下命令 `grep` 查询 `GB`：

```
fdisk -l | grep GB
```

输出如下：

![](img/110fa0d6324f0893fff03cee6394144d_130_0.png)

图 4.5 – fdisk 输出

在这里，我们可以看到 10 GB 的设备是 `sdb`、`sdc`、`sde` 和 `sdf`。我们需要这些信息来制作 Btrfs 卷。

### 如何操作

现在我们知道了设备信息，让我们手动创建一个 RAID1 卷。我们将使用所有五个设备进行 RAID1 配置，并将卷命名为 `data`。我们将使用以下命令：



```
mkfs.btrfs -L data -m raid1 /dev/sd*
```

请参考下图输出：

```
[root@bf]$ mkfs.btrfs -L data -m raid1 /dev/sd*
```

更多信息请参见 http://btrfs.kernel.org。注意：5.15 版本更改了一些默认设置，请确保这不会影响您的部署：

- `dup` `-m dup`
- `noholes` enabled `o=noholes`
- `free-space-tree` `-R free-space-tree`

Label: `data`

UUID: `11a4f1d3-19a0-4554-87a8-56d783a`

Node size: `16384`

Sector size: `4096`

Filesystem size: `50.00GiB`

Block group:

Data: `RAID1` `50.00GiB`

Metadata: `RAID1` `256.00MiB`

System: `RAID1` `8.00MiB`

SSD detected: `no`

Zoned device:

Incompat features: `extref-metadata`, `noholes`, `raid1`

Runtime features: `free-space-tree`

checksum: `crc32`

Number of devices: `5`

ID SIZE

1 10.00GiB `/dev/sdb`

2 10.00GiB `/dev/sdc`

3 10.00GiB `/dev/sde`

4 10.00GiB `/dev/sdf`

5 10.00GiB `/dev/sdf`

![](img/110fa0d6324f0893fff03cee6394144d_131_0.png)

## 注意

挂载 Btrfs 卷时，通常使用第一个设备或卷的 UUID。UUID 在 `mkfs.btrfs` 创建卷时报告。接下来，创建 `/data` 目录并使用以下命令挂载：

```
mkdir /data
mount /dev/sdb /data
```

建议将其添加到 `fstab` 文件。在示例中，我们使用了卷的 UUID，由于 `data` 没有子卷，因此 `subvol` 参数留空：

```
root@btrfs ~# more /etc/fstab

# /etc/fstab
# Created by anaconda on Sun May 14 01:31:56 2023
# accessible filesystems, by reference, are maintained under '/dev/disk/'
# See man pages fstab(5), findfs(5), mount(8) and/or bkid(8) for more info.

# After editing this file, run 'systemctl daemon-reload' to update system
# units generated from it.
UUID=55d5e0c6-b6b5-49a8-948b-335c36f9a499 btfs sub=root 0 0
UUID=55d5e0c6-b6b5-49a8-948b-335c36f9a449 btfs sub=boot 0 0
UUID=55d5e0c6-b6b5-49a8-948b-335c36f9a449 btfs sub=home 0 0
UUID=55d5e0c6-b6b5-49a8-948b-335c36f9a449 btfs sub=var 0 0
UUID=55d5e0c6-b6b5-49a8-948b-335c36f9a449 btfs sub=var_log 0 0
UUID=7ac1d941-afb6-43cd-9de6-e088ef26c3 swap defaults 0 0
root@btrfs ~
```

![](img/110fa0d6324f0893fff03cee6394144d_132_0.png)

# 工作原理

现在我们有了一个挂载卷，让我们对其做一些操作吧！首先，可以使用 `btrfs` 命令检查几项内容。首先检查设备健康状况，有助于查看 RAID 是否有故障设备。不要忘记将 `$DEVICE` 替换为您正在检查的实际设备：

```
[root@btfs ~# btrfs device /data
/dev/sddb.write_io_errs 0
/dev/sddb.read_io_errs 0
/dev/sddb.flush_io_errs 0
/dev/sddb.corruption_errs 0
/dev/sddb.generation_errs 0
/dev/sdc.write_io_errs 0
/dev/sdc.read_io_errs 0
/dev/sdc.flush_io_errs 0
/dev/sdc.corruption_errs 0
/dev/sdc.generation_errs 0
/dev/sde.write_io_errs 0
/dev/sde.read_io_errs 0
/dev/sde.flush_io_errs 0
/dev/sde.corruption_errs 0
/dev/sde.generation_errs 0
/dev/sdf.write_io_errs 0
/dev/sdf.read_io_errs 0
/dev/sdf.flush_io_errs 0
/dev/sdf.corruption_errs 0
/dev/sdf.generation_errs 0
[root@btfs ~]
```

图 4.8 – 健康设备

当设备开始出现故障时，您应该开始在该报告中看到错误。

接下来，我们将向卷中添加更多设备。添加了四个 10 GB 硬盘：`sdg`、`sdh`、`sdi` 和 `sdj`。

在添加设备之前，我们可以看到 `/data` 有 50 GB 的可用原始空间。使用以下命令查看：

```
btrfs filesystem usage /data
```

```
# [root@btrfs ~]# btrfs filesystem usage /data
总体:
| Device size: 50.00GiB |
| Device allocated: 3.77GiB |
| Device unallocated: 46.23GiB |
| Device missing: 0.00B |
| Used: 576.00KiB |
| Free (estimated): 16.41GiB (min: 16.41GiB) |
| Free 可用空间 (statfs, df): 9.74GiB |
| 数据比例: 3.00 |
| 元数据比例: 3.00 |
| 全局预留: 3.25MiB (used: 0.00B) |
| 多重配置: no |
Data,RAID1C: Size:1.00GiB, Used:0.00B (0.00%)
/dev/sdd 1.00GiB
/dev/sde 1.00GiB
/dev/sdf 1.00GiB
Metadata,RAID1C: Size:256.00MiB, Used:176.00KiB (0.07%)
/dev/sdd 256.00MiB
/dev/sde 256.00MiB
/dev/sdf 256.00MiB
System,RAID1C: Size:8.00MiB, Used:16.00KiB (0.20%)
/dev/sdb 8.00MiB
/dev/sde 8.00MiB
/dev/sdf 8.00MiB
Unallocated:
/dev/sdb 10.00GiB
/dev/sdc 10.00GiB
/dev/sdd 8.74GiB
/dev/sde 8.74GiB
/dev/sdf 8.74GiB
```

> 图 4.9 - Btrfs 文件系统使用情况

在这里我们可以看到统计数据，几乎有 50 GB 的空闲原始空间，以及其他指标，包括卷中分配给每个设备的空间以及哪些设备拥有元数据。

接下来，让我们添加新设备。这通过 `btrfs device add` 命令完成：

```
btrfs device add /dev/sdg /data
```

对每个添加到卷中的设备都执行此操作，或者使用 `/dev/sd[a-z]` 批量添加，将 a 和 z 替换为相应的范围。完成后，你可以使用 `usage` 选项进行检查，如下示例所示：



### 图 4.10 - 添加 Btrfs 设备

```
[root@btrfs ~]# btrfs filesystem usage /data
Overall:
  Device size:             90.00GiB
  Device allocated:        3.77GiB
  Device unallocated:       86.23GiB
  Device missing:          0.00B
  Used:                    576.00KiB
  Free (estimated):        29.74GiB (min: 29.74GiB)
  Free (statfs, df):       29.74GiB
  Data ratio:               3.00
  Metadata ratio:           3.00
  Global reserve:          3.25MiB (used: 0.00B)
  Multiple profiles:       no
Data,RAID1C: Size:1.00GiB, Used:0.00B (0.00%)
  /dev/sdd                1.00GiB
  /dev/sde                1.00GiB
  /dev/sdf                1.00GiB
Metadata,RAID1C: Size:256.00MiB, Used:176.00KiB (0.07%)
  /dev/sdd                256.00MiB
  /dev/sde                256.00MiB
  /dev/sdf                256.00MiB
System,RAID1C: Size:8.00MiB, Used:16.00KiB (0.20%)
  /dev/sdd                8.00MiB
  /dev/sde                8.00MiB
  /dev/sdf                8.00MiB
Unallocated:
  /dev/sdb                10.00GiB
  /dev/sdc                10.00GiB
  /dev/ssd                 8.74GiB
  /dev/sde                8.74GiB
  /dev/sdf                8.74GiB
  /dev/sdg                10.00GiB
  /dev/sdh                10.00GiB
  /dev/sdi                10.00GiB
  /dev/sdj                10.00GiB
```

你现在将看到设备大小为 90 GB。现在随着 `/data` 空间的消耗，你应该看到可用空间减少，以及数据在各个磁盘上的分布：

### 图 4.11 - Btrfs 空间使用

```
[root@btrfs ~]# btrfs filesystem usage /data
Overall:
    Device size:               72.00GiB
    Device allocated:         13.09GiB
    unallocated:              58.91GiB
    Device missing:            0.00B
    Used:                      9.07GiB
    Free (estimated):         59.84GiB (min: 20.57GiB)
    Free (statfs, df):         59.84GiB
    Data ratio:               1.00
    Metadata ratio:             3.00
    Global reserve:            3.25MiB (used: 0.00B)
    Multiple profiles:        no
Data,single: Size:10.00GiB, Used:9.06GiB (90.62%)
    /dev/sda                1.00GiB
    /dev/sdb                1.00GiB
    /dev/sde                1.00GiB
    /dev/sdf                1.00GiB
    /dev/sdg                1.00GiB
    /dev/sdh                1.00GiB
    /dev/sdi                1.00GiB
    /dev/sdj                1.00GiB
Metadata,RAID1C: Size:32.00MiB, Used:2.77MiB (0.27%)
    /dev/sda                1.00GiB
    /dev/sde                1.00GiB
    /dev/sdf                1.00GiB
System,RAID1C: Size:32.00MiB, Used:16.00MiB (0.05%)
    /dev/sda                32.00MiB
    /dev/sde                32.00MiB
    /dev/sdf                32.00MiB
Unallocated:
    /dev/sda                1.00GiB
    /dev/sdb                7.97GiB
    /dev/sde                7.97GiB
    /dev/sdf                7.97GiB
    /dev/sdg                9.00GiB
    /dev/sdh                9.00GiB
    /dev/sdi                8.00GiB
    /dev/sdj                8.00GiB
[root@btrfs ~]#
```

在最后一个示例中，我们将删除一个设备以释放空间，然后进行数据平衡。要删除物理设备，请使用 `btrfs device delete` 命令并指定挂载点：

```
btrfs device delete /dev/sdj /data
```

这将删除该设备：

### 图 4.12 – 设备移除

```
[root@btrfs ~]# btrfs device delete /dev/sdj /data
[1283.854195] BTRFS info (device sdi): relocating block group 118362640 data
[1284.836865] BTRFS info (device sdi): found 2 extents, stage: update data
[1285.817431] BTRFS info (device sdi): found 2 extents, stage: update data
[1285.870817] BTRFS info (device sdi): relocating block group 1372505984 data
[1286.588865] BTRFS info (device sdi): found 3 extents, stage: move data extents
[1286.640136] BTRFS info (device sdi): found 3 extents, stage: update data
[1286.650091] BTRFS info (device sdi): device deleted: /dev/sdj
[root@btrfs ~]#
```

删除设备后，重新运行使用报告。你现在将看到剩余的设备以及数据所在的设备上：



```
[root@btrfs ~]$ btrfs filesystem usage /data
Overall:
    Device size:               80.00GiB
    Device allocated:         3.77GiB
    Device unallocated:        76.23GiB
    Device missing:            0.00B
    Used:                      576.00KiB
    Free (estimated):         26.41GiB (min: 26.41GiB)
    Free (statfs, df):         19.74GiB
    Data ratio:                3.00
    Metadata ratio:            3.00
    Global reserve:            3.25MiB (used: 0.00GiB)
    Multiple profiles:         no
Data,RAID1C3: Size:1.00GiB, Used:0.00GiB (0.00%)
    /dev/ssd                  1.00GiB
    /dev/sde                  1.00GiB
    /dev/sdf                  1.00GiB
Metadata,RAID1C3: Size:256.00MiB, Used:176.00KiK (0.07%)
    /dev/ssd                  256.00MiB
    /dev/sde                  256.00MiB
    /dev/sdf                  256.00MiB
System,RAID1C3: Size:32.00MiB, Used:16.00MiB (0.05%)
    /dev/sda                  32.00MiB
    /dev/sde                  32.00MiB
    /dev/sdf                  32.00MiB
Unallocated:
    /dev/sda                  1.00GiB
    /dev/sdb                  7.97GiB
    /dev/sde                  7.97GiB
    /dev/sdf                  7.97GiB
    /dev/sdg                  9.00GiB
    /dev/sdh                  9.00GiB
    /dev/sdi                  8.00GiB
    /dev/sdj                  8.00GiB
```

图 4.13 - 未平衡的使用

虽然这只是一个小问题，但它未来可能会产生影响。幸运的是，解决方案很简单——执行 `btrfs balance`。该命令将重新平衡数据。

注意

为了确保数据良好平衡，建议在添加或删除设备时始终对系统进行平衡，即使存在细微差异。这种做法对于保持文件系统的性能至关重要。`ol8_developer` 仓库中的 `btrfsmaintenance` 软件包是自动执行所需 Btrfs 维护任务的极佳工具。

Btrfs 的功能比旧的 XFS 技术强大得多。这包括子卷、快照和配额。Btrfs 子卷是一项极出色的工具，允许用户在单个 Btrfs 文件系统中创建多个快照或子文件。这些子卷在文件系统层级结构中作为不同的目录显示，它们共享相同的存储空间并可以进行独立管理。

子卷的灵活性和多功能使其成为各种用途的理想选择，例如创建备份或隔离文件系统的部分以便更于管理。快照则特别有用，因为它们提供了文件系统在特定时间点的只读副本。通过快照，用户可以将文件或整个子卷恢复到之前的状态，或者轻松地创建可以移动到另一个系统的可复制备份。

子卷还允许用户更高效地管理磁盘空间。例如，用户可以为某个特定的应用程序或项目创建一个子卷，并限制其使用在特定的容量范围内，以防止其占用文件系统过多的空间。此外，还可以通过为不同的子卷分配不同的权限，或为不同的用户或组创建单独的子卷来实现访问控制。本配方将介绍如何执行这些操作。

## 准备工作

本配方需要一个 Btrfs 文件系统，并将使用上一个配方创建的数据文件系统进行示例。

## 如何操作...

在本配方中，我们将执行以下操作：

- 1. 在 `/data` 中创建一个子卷并挂载它。
- 2. 在子卷上设置配额。
- 3. 创建快照。
- 4. 启用压缩。

创建子卷非常简单，通过使用 `btrfs` 命令并指定子卷的完整路径即可完成：

```
btrfs subvolume create /data/vol1
```

创建完成后，只需将其添加到 `fstab` 中即可，这次在第四列中声明子卷名称。如下所示，其中使用子卷 `vol1` 挂载了 `/data/vol1`：

```
root@btrfs ~# edit /etc/fstab

# /etc/fstab
# Created by anaconda on Sun May 14 01:31:56 2023
# accessible filesystems, by reference, are maintained under '/dev/disk/'.
# See man fstab(5), finds(8), mount(8) and/or bklkid(8) for more info.

# After editing this file, run 'systemctl daemon-reload' to update system
# units generated from file.

UUID=55ed0c6b-06b5-49a0-a94b-35cdf368bf49 btrfs subvol=root      0 0
UUID=55ed0c6b-06b5-49a0-a94b-35cdf368bf49 btrfs subvol=boot     0 0
UUID=55ed0c6b-06b5-49a0-a94b-35cdf368bf49 btrfs subvol=home    0 0
UUID=55ed0c6b-06b5-49a0-a94b-35cdf368bf49 btrfs subvol=var       0 0
UUID=55ed0c6b-06b5-49a0-a94b-35cdf368bf49 btrfs subvol=root      0 0
UUID=55ed0c6b-06b5-49a0-a94b-35cdf368bf49 btrfs subvol=var_log  0 0
UUID=66b9a6b4-ff75-4f63-a2f7-ce9f8e8fa32 btrfs subvol=data      0 0
UUID=55ed0c6b-06b5-49a0-a94b-35cdf368bf49 btrfs subvol=home    0 0
UUID=1d1c19d4-abbf-46c8-a93e-feb826f669 btrfs swap           0 0
root@btrfs ~#
```

图 4.15 - btrfs 中的子卷

现在子卷已经挂载，让我们添加一个配额将其限制在 5 GB。要做到这一点，我们首先需要为该卷创建配额功能。使用以下命令完成：

```
btrfs quota enable /data
```

接下来，我们需要为子卷分配配额限制。这将限制定义的子卷大小。我们使用 `limit` 选项，如下命令所示：

```
btrfs qgroup limit 5g /data/vol
```

你可以使用 `btrfs qgroup show` 命令配合 `-ref` 选项来查看卷中定义了哪些配额：

```
root@btrfs ~# btrfs qgroup show -ref /data/vol
groupid         rfer        excl        max_rfer      max_excl
-------------------------------------------------------------
0/256            16.0KiB      16.0KiB      5.0GiB       none
root@btrfs ~#
```

图 4.16 - 设置配额

现在我们已经设置了配额，让我们为备份创建一个快照。我们需要一个存放备份的地方，所以使用以下命令为备份创建一个子卷：

```
btrfs subvolume create /data/backup
```



# Btrfs 快照

Btrfs 快照是 Btrfs 文件系统的非常有用的副本，捕捉了特定时间点的状态。通过无缝的写复制机制，这些快照将对文件系统的任何更改与快照本身隔离开。这使其成为各种用途的理想选择，例如创建备份、测试软件配置以及提供易于撤销更新的方法。此外，备份可以快速创建且占用极少的存储空间，因为快照只存储文件系统当前状态与快照拍摄状态之间的差异。要创建 Btrfs 快照，你可以使用 `btrfs subvolume snapshot` 命令，指定要快照的子卷以及快照的名称和位置：

```
btrfs subvolume snapshot /data/vol1 /data/backup/vol1_backup1
```

该命令为 `/data/vol1` 子卷创建一个只读快照，并将其保存为 `/data/backup` 目录下的一个独立子卷。

即使你已经取过快照也不用担心——你可以轻松恢复到之前的状态。

接下来，我们可以使用 `df` 和 `du` 命令来比较消耗的空间和实际使用的空间：

```
df -h /data/voll
du -hd0 /data/voll
```

这些命令的示例输出如下：

```
[root@btrfs vol]# df -h /data/voll
Filesystem Size Used Avail Use% Mounted on
/dev/sda 30G 2G 28G 1% /data/voll
[root@btrfs vol]# du -hd0 /data/voll
2.0G /data/voll
[root@btrfs vol]#
```

在这里，我们可以看到已使用 2 GB 空间（通过 `du` 命令），并且实际上也消耗了 2 GB（通过 `df` 命令）。因此，对于随机数据文件，我们可以从压缩中获益。

现在让我们删除文件，而不是：

```
rm /data/voll/test1
```

为了加快速度，我们对卷进行碎片整理和重新平衡。这是为了真正从已删除的文件释放空间：

```
[root@btrfs vol]# btrfs filesystem defragment -rc /data/voll
[root@btrfs vol]# btrfs filesystem balance /data
Done, had to relocate 4 out of 4 chunks
[root@btrfs vol]#
```

现在，通过一个重复数据的文件，我们将看到更多的压缩效果。要创建一个 2 GB 的重复数据文件，运行以下命令：

```
yes "repeating text" | head -c 2G >test2
```

现在，我们重复之前的 `df` 和 `du` 命令，但我们将看到完全不同的结果：

```
[root@btrfs vol]# df -h /data/voll
Filesystem Size Used Avail Use% Mounted on
/dev/sda 30G 62M 29G 1% /data/voll
[root@btrfs vol]# du -hd0 /data/voll
2.0G /data/voll
[root@btrfs vol]#
```

在这里，我们看到分配了 4 GB，但实际上只使用了 62 MB！这是压缩带来的巨大收益。

# 使用 mdadm 保护数据 – 软件 RAID 解决方案

现代计算系统依赖 RAID 技术来确保数据的完整性、可用性和性能。通过在各种配置的多个磁盘上分布数据，RAID 提供了容错能力，允许系统在一个或多个磁盘故障时继续运行。这种冗余性对于防止数据丢失和最小化停机时间至关重要。

此外，RAID 配置（如条带和镜像）可以通过允许与多个磁盘并行访问数据来显著提高读写性能。在当今的数字世界中，随着数据量和重要性的不断增加，RAID 在保护、优化和维护存储系统可靠性方面发挥着至关重要的作用。Oracle Linux 8 中如果不使用 Btrfs，最简单的方法是使用 `mdadm` 工具。

## 准备工作

`mdadm` 是一个用于在 Linux 系统管理和配置 RAID Array 的软件实用程序。它是 multiple device administration（多设备管理）的缩写，通常用于创建、管理、监控和维护 RAID Array。这些数组利用内核驱动多设备 (MD)。`mdadm` 允许用户使用多个物理磁盘组合创建各种 RAID 级别，包括 RAID 0、RAID 1、RAID 5、RAID 6、RAID 0+1 和 RAID 10：

| 类型 | 说明 | 注意事项 |
|---|---|---|
| RAID | 跨越 | 无冗余或性能优势。 |
| RAID-0 | 条带 | 无冗余，但与 RAID 相比性能更好。 |
| RAID-1 | 镜像 | 镜像冗余，但在写入负载中没有性能优势。读取负载可能会有所提高。 |
| RAID-5 | 双重奇偶校验条带 | 冗余性良好。可以丢失一个磁盘而不丢失数据。建议至少使用四块磁盘。 |
| RAID-6 | 三重奇偶校验条带 | 冗余性良好。可以丢失两个磁盘而不丢失数据。建议至少使用五块磁盘。 |
| RAID 0+1 | 条带磁盘的镜像 | 性能极佳，但通常被认为冗余性最好，且恢复丢失的磁盘需要长时间。这需要至少四块磁盘。 |
| RAID 10 | 镜像的条带 | 最贵的选项，但通常被认为冗余性和重建时间是最好的。这需要至少四块磁盘。 |

### 表 4.2 – MD 选项

### 注意

将 JBOD（仅仅是一箱磁盘）与 RAID 混淆并不罕见。JBOD 是一个没有硬件的简单磁盘。RAID 磁盘具有硬件控制器，可以卸载机箱内所有磁盘的 RAID 逻辑。在本示例中，不使用硬件 RAID，仅使用 JBOD。

`mdadm` 是管理员创建、修改和监控 RAID Array 的基本工具。它允许用户从现有阵列中添加或删除磁盘、执行操作并配置 RAID 级别和备用等各种参数。通过其命令行界面，`mdadm` 在管理和维护磁盘冗余方面提供了灵活性，并且是一个优化存储性能、确保数据冗余并维护高可用性的健壮解决方案。在安装 Oracle Linux 时通常会安装 `mdadm`。

## 如何操作

创建一个 MD 设备非常简单。在创建设备之前，你需要提前计划以下几点：

- 你将使用哪种类型的 RAID？如前所述，MD 驱动程序支持许多类型的 RAID 算法。你需要在运行命令之前选择一个。
- 你将使用多少块磁盘？RAID 类型使用磁盘数量，但你仍然需要知道将使用多少块磁盘用于数据。这映射到 `-level` 选项。
- 你会配置热备用吗？当某个设备故障时，热备用是一个很棒的选择，系统会自动重建数据。这映射到 `-spare` 选项。
- MD 设备的数量是多少？传统上你从 0 开始计数，这样就不会意外使用该设备。这映射到 `/dev/md`。
- 你将使用哪些路径？是 `/dev/sd`、`/dev/nvme` 还是 `/dev/vdb`。

在示例中，我们将创建一个带有一个热备的 RAID-5 阵列。设备是 `/dev/sd`，这是 `/dev/md0` 设备：

```
mdadm --create /dev/md0 --level=5 --raid-devices=4 --spare-devices=1 /dev/sd
```

你可以通过调用 `/proc/mdstat` 文件快速检查状态：

```
[root@xfs ~] cat /proc/mdstat
Personal : [raid5]
sdd(2) sdc(1) sdb(0)
md0 : active raid5 sde(1) sdf(4)
      6286336 blocks level 5, 512 chunk, algorithm 2 [4/3] [UUU]
      ======= recovery = 61.7% (1294380/2095412) finish=1.8min speed=1284K/sec
unused devices: <none>
[root@xfs ~]#
```

![](img/110fa0d6324f0893ffcee639414d_147_0) 最后一步是可选的，会将当前配置保存到 mdadm 文件中。这有助于启动。通过以下命令完成：

```
mdadm --scan >> /etc/mdadm.conf
```

## 工作原理

现在，让我们看看关于 MD 设备的一些。首先，如果我们使用 `isblk` 命令，我们将看到 `md0` 使用的磁盘。因为 `md0` 是实际设备的子：



```
[root@xfs ~]# isblk
NAME      MIN RO TYPE MOUNTPOINT
sda       8:0  0 200G disk
└sda1     8:1  0 16G part /boot
└sda2     8:2  0 72.96G part /
└ol-root 252:0 0 506G lvm /
└ol-swap 252:1 0 7.96G lvm [SWAP]
└ol-var   252:2 0 56G lvm /var
└ol-home 252:3 0 56G lvm /
└ol-var_log 252:4 0 56G lvm /var/log
sdb      8:16 0 206G disk
└md0     9:0  0 206G raid5
sdc      8:32 0 206G disk
└md0     9:0  0 206G raid5
sdd      8:48 0 206G disk
└md0     9:0  0 206G raid5
sde      8:64 0 206G disk
└md0     9:0  0 206G raid5
sdf      8:80 0 206G disk
└md0     9:0  0 206G raid5
srs      11:0 1 1024M 
[root@xfs ~]#
```

![](img/110fa0d6324f0893fffcee639414d_147_1) 我们也可以 `-Q` 选项检查设备以获取摘要。只需将设备作为参数，命令将给你一个简短的输出：

```
[root@xfs ~]# mdadm -Q /dev/md0
/dev/md0: active raid5 59.956Gi 4 devices, 1 spare
```

图 4.19 - mdadm -Q 此外，你可以传递 `--detail` 选项来获取关于阵列更多的信息：

```
[root@xfs ~]# mdadm --detail /dev/md0:
/dev/md0:
Version : 1.2
Creation Time : Mon 15 23:28:00 2023
Raid Level : raid5
Array Size : 6286336 (59 GiB 64.37 GB)
Used Device : 2095412 (19.98 GiB 21.46 GB)
Raid Devices : 4
Total Devices : 5
Persistence : Superblock is persistent

Update Time : Mon 15 23:30:43 2023
State : clean
Active Devices : 4
Working Devices : 5
Failed Devices : 0
Spare Devices : 1

Layout : left-symmetric
Chunk Size : 512K
Consistency Policy : resync

```

Name : xfs.m57.local:0 (local to host xfs.m57.local)

UUID : d8d01c3c:ce25be76:7900ef52:1bb1f730

Events : 18

```

```

| Number | Major | Minor | Raiddevice | State |
|---|---|---|---|---|
| 0 | 8 | 16 | active sync | /dev/sdb |
| 1 | 8 | 32 | 1 | active sync | /dev/sdc |
| 2 | 8 | 48 | 2 | active sync | /dev/sdd |
| 5 | 8 | 64 | 3 | active sync | /dev/sde |
| 4 | | 80 | | spare | /dev/sdf |

图 4.20 - mdadm -detail

在这里，我们不仅能看到阵列的健康状况，还能看到创建日期以及块大小和布局等低层指标。

一旦创建了卷，你现在就可以将其用于文件系统或逻辑卷管理器的存储。

# 玩转逻辑卷管理

谈到文件系统时，最大的问题之一是它们在存储方面的缺乏灵活性。在磁盘上创建卷意味着该空间被锁定在卷中，这也限制了文件系统的大小。然而，逻辑卷管理器（LVM）为这个问题提供了一个解决方案。LVM 是计算机存储管理领域中广泛使用的工具，它在物理存储设备（如硬盘或 SSD）与操作系统（OS）之间充当抽象层。这使得能够对存储资源进行灵活且高效的管理。LVM 对于 Linux 系统而言特别别有价值，因为它提供了一种灵活且可扩展的存储管理解决方案。

通过 LVM，管理员可以动态地分配和调整卷的大小，而无需重新分区或中断系统。这种灵活性在存储需求频繁变化或需要高效资源分配的环境中尤为有用。此外，LVM 引入了卷组（volume groups，简称 VG）的概念，卷组充当了物理存储设备的逻辑容器。通过在卷组内创建逻辑卷，管理员可以轻松地分配和管理存储，简化了 Linux 系统中存储资源的管理，并更容易有效地组织和利用存储资源。

通过 LVM，存储有三个核心组件：

- **物理卷 (PVs)**：这些是用于存储的块级设备。它们可以是物理磁盘、虚拟磁盘（例如在中间配方中创建的 MD 设备）或其他块级设备。
- **卷组 (VGs)**：这些是 PV 组，被组合成单个逻辑设备。它们可以从单个设备开始，通过添加新设备来增加容量。
- **逻辑卷 (LVs)**：这些是构建在 VG 之中的逻辑磁盘。它们用于创建文件系统，并可以根据需要动态调整大小。

LVM 中的 VG 是一个核心组件，作为一个或多个 PV 的逻辑容器。VG 是通过将物理存储设备（如硬盘或 SSD）组合成单一存储池创建的。

在本配方中，我们将向你展示如何初始化 PV、创建 VG，并添加 LV 以供未来文件系统使用。我们还将展示一些基础管理命令。

## 准备工作

本配方中的示例将使用在 mdadm 配方中创建的 `/dev/md0` 虚拟磁盘，外加几个额外的 LUN。LVM RPM 包通常在正常安装时默认安装。

## 如何操作...

第一步是识别我们可以使用哪些磁盘。这是通过 `lvmdiskscan` 命令完成的：

```bash
[root@xf ~]# lvmdiskscan
/dev/md0 [ 59.95 GiB]
/dev/sda1 [ 1.00 GiB]
/dev/sda2 [ 72.98 GiB] LVM physical volume
 0 disks
 2 partitions
 0 LVM physical volume whole disks
 1 LVM physical volume
[root@xf ~]#
```

图 4.21 - lvmdiskscan

在这里，我们可以看到三个设备：`md0`、`sda1` 和 `sda2`。我们看到 `sda2` 已经初始化为一个 PV。我们可以使用 `pvs` 命令显示系统上的 PV：

```bash
[root@xf ~]# pvs
PU      VG Fmt  Attr  Size  Free
/dev/sda2  ol lvm2  -- <72.90g 4.00m
[root@xf ~]#
```

图 4.22 - pvs

在这里，我们可以看到 `/dev/sda2` 设备被 o1 VG 使用。让我们继续使用 `pvcreate` 来初始化 `/dev/md0`。

```bash
pvcreate /dev/md0
```

现在设备已经初始化，我们可以创建一个 VG。这是通过 `vgcreate` 命令完成的。该命令使用第一个参数作为 VG 的名称，然后是设备列表。在这种情况下，我们将只使用 `/dev/md0` 来创建 DATA VG：

```bash
vgcreate DATA /dev/md0
```

## 工作原理

我们可以通过 `vgs` 命令查看系统上的 VG 列表。

```bash
[root@xfs # vgs
VG #PV LV #DM Attr Size VFree
DATA 1 0 0 wz-n- <59.95g <59.95g
ol 1 5 0 wz-n- <72.90g 4.00m
[root@xfs # ]
```

图 4.23 - vgs

在这里我们可以看到两个 VG：新创建的 DATA VG 和安装操作系统的 VG。我们将使用 VG 来创建一个 LV。这是通过 `lvcreate` 命令完成的。`lvcreate` 命令接受几个参数：`-l` 设置卷，`-n` 指定名称，最后是卷将所在的 VG。让我们在 DATA VG 中创建一个名为 xfs1 的 3 GB 卷：

```bash
lvcreate -L 2G -n xfs1 DATA
```

我们也可以告诉 `lvcreate` 使用所有可用空间。这是通过使用小写和特殊的 `100%FREE` 完成的：

```bash
lvcreate -L 100%FREE -n xfs2 DATA
```

`lvs` 命令将显示服务器上所有的 LV：



```bash
[root@xfs #] lvs
LV VG Attr LSize Pool Origin Data Meta Move Log Cpyz:Sync Co
invert xfs1 DATA -wi-a----- 20g
xfs2 DATA -wi-a----- <57.95g
nhome ol -wi-ao----- 00g
root ol -wi-ao----- 00g
swap ol -wi-ao----- 89g
var ol -wi-ao----- 00g
var_log ol -wi-ao----- 00g
[root@xfs # ]
```

图 4.24 - `lvs`

在这里我们可以看到 `xfs1` 和 `xfs2` 卷及其大小。此外，我们可以看到安装操作系统的所有卷。让我们通过删除 `xfs2` LV 来释放空间。这是通过 `lvremove` 命令完成的。在使用 `lvremove` 时，使用 VG/LV 来标识要删除的 LV。以下命令将移除 `xfs2` LV：

```bash
lvremove DATA/xfs2
```

```bash
lvremove DATA/xfs2
确定要删除卷 xfs2 吗？[y/n]: y
卷 "xfs2" 已移除。
root@xfs ~]#
```

25 - `lvremove`

最后一个任务是查看特定 LV 的详情。这是通过 `lvdisplay` 命令完成的。`lvs` 命令将显示服务器上所有的 LV，但 `lvdisplay` 提供单个卷的详细信息。

```bash
root@xfs # lvdisplay /dev/DATA/xfs1
-- Logical volume --
  Path               /dev/DATA/xfs1
  VG                 DATA
  Name               xfs1
  UUID               [UUID-STRING]
  Size               20g
  Attr               wi-a-----
  Use                read
  Creation date       [DATE]
  Access             read
  Segments           0
  Origin             
  Data               0
  Meta               0
  Log                0
  Cpyz               none
root@xfs # 
```

图 26 - `lvdisplay`

（注：由于原文后续存在大量重复和乱码，译文已根据核心逻辑进行了清理和整合）

`block-sharing-reflink`.

使用 XFS，管理员可以在文件系统挂载并正在使用时执行广泛的文件系统操作。这包括在线调整大小，能够无缝扩展或收缩文件系统，而无需卸载文件系统或中断服务。这些在线管理能力使得 XFS 非常适用于需要持续可用性和极少停机时间的环境。XFS 还对扩展属性、`访问控制列表 (ACLs)` 以及纳秒级精度的时间戳提供了广泛支持。这些特性为管理文件元数据提供了灵活性，并能够实现复杂的权限结构和自定义元数据方案。

XFS 受 Linux 内核原生支持，它是 Linux 发行版中集成良好且被广泛采用的选择。它是 Oracle Linux 的默认文件系统，并持续受益于 Oracle 和 Linux 社区的持续开发和改进。此外，XFS 还带有一套完整的文件系统管理和管理工具，使其成为一个全方位的顶级选项。

## 准备工作

本教程中的示例将使用之前创建的 `xffs` 卷（LV）。XFS 文件系统可以在任何块设备上创建。

## 如何操作...

创建 XFS 文件系统最常用的方法是使用 `mkfs.xfs` 命令并指定单个块设备。这将数据和日志都放置在同一设备上：

```
mkfs.xfs /dev/mapper/DATA-xfs1
```

此外，您可以使用额外的参数来获得更多控制：

| 选项 | 说明 | 示例 |
|------|---|---|
| `-L` | 为文件系统添加标签。 | `-L Test` |
| `-b` | 设置块大小。 | `-b 8192` |
| `-f` | 强制选项。 | `-f` |
| `-l` | 设置日志的位置和大小。这通常用于通过允许日志位于 `/dev/mapper/journal-fast` 设备来调整性能，而将数据放在较慢的设备上。 | `-l 20m` |

`Size=20m /dev/$DEVICE`

表 4.3 - XFS 选项

接下来，添加 `/etc/fstab` 条目信息。确保验证挂载点是否存在，并且您使用的是正确的 `/dev/mapper` 路径。更新后的文件见下方的截图：

```
/etc/fstab
# Created by anaconda on Mon May 15 00:49:10 2023
# Accessible filesystems, by reference, are maintained under '/dev/disk/'
# See many pages fstab(5), find(8), mount(8) and/or blkid(8) for more info.
# After editing this file, run 'systemctl daemon-reload' to update systemd
# units generated from this file.
/dev/mapper/root               xfs defaults      0 0
	UUID=d3b7b4d8-738d-44c2-a850-11f7e870ec7 /boot
	                               0 0
/dev/mapper/home             /home           xfs defaults      0 0
/dev/mapper/var              /var            xfs defaults      0 0
/dev/mapper/var_log          /var/log         xfs defaults      0 0
/dev/mapper/DATA-xfs1         /xfs1           xfs defaults      0 0
/dev/mapper/swap             none            swap defaults      0 0
```

图 4.28 - `/etc/fstab`

我们可以通过以下命令挂载文件系统：

```
mount /xfs1
```

我们可以清楚地看到文件系统已挂载，如命令的输出所示：

```
[root@xfs ~#] df -h Size Avail Use Mounted on
Filesystem
devfs           3.86 0 3.8G 0% /dev
tmpfs           3.86 0 3.8G 0% /dev
tmpfs           3.86 0 3.8G 0% /run
tmpfs           3.86 0 3.8G 0% /sys/fs/cgroup
/dev/mapper/root               5.06 5.36G 45% /
/dev/mapper/var  5.06 1.76G 33% /var
/dev/mapper/var_log 5.06 81M 5.0G 2% /var/log
/dev/mapper/home 5.06 81M 5.0G 2% /home
/dev/sda         10.1G 499M 49% /boot
/dev/mapper/DATA-xfs1 2.06 47M 1.9G 3% /xfs1
tmpfs           765M 0 765M 0% /run/user/0
[root@xfs ~#] 
```

图 4.29 - `df -h`

## 工作原理

现在文件系统已经挂载，我们可以对它进行一些操作。首要任务是扩展文件系统，因为 2 GB 对于应用程序来说有点小。这通过几个步骤完成：首先，扩展包含文件系统的卷，然后扩展文件系统。让我们将其扩展到 10 GB。

为了扩展卷，我们将使用 `lvextend` 命令并向其传递 `+8G` 选项以增加 8 GB：

```
$root@fs lvextend -L +8G /dev/mapper/DATA-xfs1
Size of logical volume DATA/xfs1 changed from 2.00 GiB (512 extents) to 10.0 GiB (2560 extents).
Logical volume DATA/xfs1 successfully resized.
$root@fs ~#
```

输出见下方：

![](img/110fa0d6324f0893fff03cee639414d_156_0.png)



一旦卷扩展完成，我们需要扩展实际的文件系统。这是通过 `xfs_growfs` 命令完成的：

```
xfs_growfs /dev/mapper/DATA-xfs1
```

取决于文件系统的活动程度，增长可能需要几分钟。`xfs_growfs` 命令的输出将在完成后显示文件系统的详情：

```
$root@fs # xfs_growfs /dev/mapper/DATA-xfs1
data /dev/mapper/DATA-xfs1 is now 10.05G in 2560 blocks (10.05G)
data /dev/mapper/DATA-xfs1:data size changed from 2.00G to 10.05G
$root@fs ~#
```

在 DNF 开发的这一阶段，大多数命令都是相同的，但 DNF 确实有一些“小技巧”，例如自动运行更新。

# DNF 自动更新

你可以设置 DNF 自动运行。要实现此功能，安装 `dnf-automatic` 包并使用以下命令启用服务：

```
yum install dnf-automatic
systemctl enable dnf-automatic.timer
systemctl start dnf-automatic.timer
```

接下来，编辑 `/etc/dnf/automatic.conf` 文件。该文件中包含一些技巧。你可以通过将 `apply_updates` 参数设置为 `yes` 来覆盖是否在下载时自动应用补丁。这将强制在任务运行时应用补丁。

不要忘记设置 `system_name` 参数，以便电子邮件和通知将显示正确的名称。

你还可以设置系统向你的邮箱发送一份安装报告。在 `[email]` 区域中设置电子邮件。如果使用电子邮件中继，请确保它不需要身份验证，或者根据需要将其添加到配置中。

作为最后一个技巧，你可以将 `emit_via` 参数从 `stdout` 改为 `motd`。当设置为 `motd` 时，系统 motd 文件将更新以反映安装了哪些补丁。当用户登录系统时，他们将看到完整的安装补丁列表以及安装时间，如下截图所示：

```
xorg-server-x86       x86_64 1.20.11-5.e18  ol8_x64_appstream      1.5 M
xorg-server-Xwayland  x86_64 21.1.3-2.el8  ol8_x64_appstream      963 k
xorg-server-common    x86_64 1.20.11-5.e18  ol8_x64_appstream      42 k
                                     x86_64 5.2.4-4.el8       ol8_x64_baseos      153 k
z-libs                                 x86_64 21.1.3-2.el8       ol8_x64_baseos      96 k
zlib                                   x86_64 12.1.18-5.el8  ol8_x64_baseos_latest  102 k
Installing module packages:
kernel-devel                           x86_64 5.14-21306.39.el8uk  ol8_x64_UEKR             109 M
Installing dependencies:
NetworkManager-encrypt-update      1.26.3-4.0.1.el8  ol8_x64_baseos_latest  137 k
autog-libs                             x86_64 6.18-12.el8       ol8_x64_appstream      75 k
glibc-common-ext                       x86_64 2.28-218.180.1.el8  ol8_x64_userspace_kcplice
gnutls-data                            x86_64 3.6.16-4.0       ol8_x64_appstream      1.6 M
gnutls-utils                           x86_64 3.6.16-4.0       ol8_x64_appstream      52 k
gdb2-tools-devel                       x86_64 1.12.2-03.el8  ol8_x64_baseos_latest  348 k
linux-firmware                        x86_64 2019.999-991  ol8_x64_baseos_latest  478 k
libgpg                                 x86_64 4.18.0-372.el8  ol8_x64_baseos_latest  14 M
kernel-core                           x86_64 4.18.0-372.el8  ol8_x64_appstream      32 M
space-helper                        x86_64 9.0.1-2.2021126gitifeff3f3.module+el18.6.0+206593dc7c70  184 k
libbpf                                 x86_64 0.4.3-0.8       ol8_x64_appstream      125 k
libd                                  x86_64 2.3.3-2.el8       ol8_x64_appstream      32 k
libtgms                               x86_64 9.0.1-2.2021126gitifeff3f3.module+el18.6.0+206593dc7c70
linux-firmware-core                   x86_64 2019.9200394  ol8_x64_baseos_latest  509 k
devt1                                 x86_64 1.2.0-2.el8  ol8_x64_appstream      745 k
qemu-kvm-deps                          x86_64 15.6.2-1.el8.module+18.6.0+206593dc7c70
qemu-kvm-us-bredir                   x86_64 15.6.2-1.el8.module+18.6.0+206593dc7c70  2.6 M
qemu-kvm-ui-opengl                   x86_64 15.6.2-1.el8.module+18.6.0+206593dc7c70  184 k
shadow-utils-subid                    x86_64 4.2-6.el8       ol8_x64_baseos_latest  223 k
swtpm                                 x86_64 0.7.0-2021110git9b7fd.module+el18.6.0+206593dc7c70  43 k
swtpm-libs                           x86_64 0.7.0-2021110git9b7fd.module+el18.6.0+206593dc7c70  44 k
swtpm-tools                          x86_64  ol8_x64_appstream      119 k

Transaction Summary
Install: 26 Packages
Upgrade: 62 Packages

Updates at Wed 22 Jun 2022 06:23 AM Activated: systemctl enable --now cockpit.socket
Last login: Wed 22 Jun 2022 12:25 from 192.168.56.1
```

默认情况下，在此进行的服务更改会影响 `/etc/systemd/system/timers.target` 文件。

```
[Unit]

Description=dnf-automatic timer

ConditionPathExists=/run/ostree

[Timer]

Calendar=*-.* 0:00

RandomizedDelaySec=60m

Persistent=true
```



[Install]

WantedBy=timers.target

在该文件中，`[Timer]`控制时间和随机延迟。要更改运行时间，请将`6:00`替换为任何你需要的时间。例如，如果你想在晚上10点运行检查，可以使用标准的24小时格式。`OnCalendar`是一种非常灵活的方法，以下是一些常用示例：

| OnCalendar | Description |
|---|---|
| DOW YYYY-MM-DD HH:MM:SS | 通用时间格式 |
| *-.* 0:00 | 每天凌晨0:00运行 |
| Weekly | 每周一午夜 |
| Sat.* 0:00 | 每周六凌晨0:00 |
| Sun 2022*- | 2022年的每周日午夜 |
| *-1,15 22:15 | 每月1号和15号的晚上10:15 |

表5.1 OnCalendar示例

`RandomizedDelaySec`也是一个重要设置。它会为时钟添加一个随机延迟，这对于大量系统访问YUM仓库可能导致崩溃的企业环境非常有帮助。在`/etc/dnf/automatic.conf`中添加60秒的延迟可以将负载分散到几分钟内。

DNF是YUM的升级版本，包含了一些增强。如配方所示，它有一些小技巧，但仍然为管理员在Oracle Linux系统上安装和修补软件提供了非常方便的方法。

## 使用DNF时机

DNF内置了时光机！它不仅仅是回溯过去的方法；它实际上允许你查看安装的历史，并允许你回滚单个更改或回滚到某一点。

## 准备工作

要此此，你需要一台运行Oracle Linux 8并可以RPM仓库的测试系统。

## 如何操作...

当DNF安装软件时，它会保留所有操作的历史。这包括软件的升级、安装和删除。`dnf history`命令显示这些历史：

```
[root@db6 ~]# dnf history list
```

| Date and time | Action(s) | Altered |
|---|---|---|
| - install /var/lib/x86_64-cloud-agent/50f6c28f-e25c-4a52-a362-c55a37f9d | 2022-06-22 18:45 | Upgrade /var/lib/x86_64-cloud-agent/50f6c28f-e25c-4a52-a362-c55a37f9d | 1 EE |
| - install /var/lib/x86_64-cloud-agent/5029c28f-e153-4e17-a669-b49f796788 | 2022-06-22 18:45 | Upgrade /var/lib/x86_64-cloud-agent/5029c28f-e153-4e17-a669-b49f796788 | 1 EE |
| - update | 2022-05-17 00:32 | Update | 7, H |
| - update | 2022-05-17 00:32 | Update | 51 EE |
| - install | 2022-04-25 22:12 | Install | 120 EE |
| - | 2022-04-25 22:12 | Install | 34 EE |
| - install /var/lib/x86_64-cloud-agent/50f6c28f-e25c-4a52-a362-c55a37f9d | 2022-04-25 22:12 | Install /var/lib/x86_64-cloud-agent/50f6c28f-e25c-4a52-a362-c55a37f9d | 34 EE |
| - install /var/lib/x86_64-cloud-agent/50f6c28f-e25c-4a52-a362-c55a37f9d | 2022-03-18 20:26 | Install /var/lib/x86_64-cloud-agent/50f6c28f-e25c-4a52-a362-c55a37f9d | 31 EE |
| - | 2022-03-18 20:26 | Install | 31 EE |
| - install /var/lib/x86_64-cloud-agent/99d37931-7771-4991-3333336a | 2022-03-21 00:23 | Install /var/lib/x86_64-cloud-agent/99d37931-7771-4991-3333336a | 33 EE |
| - | 2022-03-21 00:23 | Install | 29 EE |
| - install /var/lib/x86_64-cloud-agent/21f2b95e-d952-4ef6-b48f-46b6f1fd3 | 2022-02-19 19:21 | Install /var/lib/x86_64-cloud-agent/21f2b95e-d952-4ef6-b48f-46b6f1fd3 | 21 EE |
| - | 2022-02-19 19:21 | Upgrade | 1 EE |
| - install | 2022-01-25 15:46 | Install | 25 EE |
| - | 2022-01-25 15:46 | Install | 20 EE |
| - update | 2022-01-20 21:11 | Update | 20 EE |
| - | 2022-01-20 21:11 | Update | 2 EE |
| - install | 2022-01-20 09:50 | Install | 1 EE |
| - | 2022-01-20 09:50 | Install | 1 EE |
| - | 2021-12-29 23:59 | Install | 1 EE |
| - | 2021-12-29 23:59 | Install | 1 EE |
| - | 2021-12-15 14:48 | Install | 3 EE |
| - | 2021-12-15 14:48 | Install | 1 EE |
| - | 2021-12-15 14:48 | Install | 1 EE |
| - | 2021-12-15 14:48 | Install | 1 EE |
| - | 2021-11-30 13:47 | Install | 2 EE |
| - | 2021-11-30 13:47 | Install | 2 EE |
| - | 2021-11-30 13:47 | Install | 1 EE |
| - | 2021-09-30 01:47 | Install | 36 EE |
| - | 2021-09-30 01:47 | Install | 1 EE |
| - | 2021-09-30 01:45 | Install | I, U |
| - | 2021-09-30 01:45 | Install | 21 EE |
| - | 2021-09-30 01:45 | Install | 1 EE |
| - | 2021-09-30 01:45 | Install | 1 EE |
| - | 2021-09-30 01:42 | Install | 577 EE |

图5.3 – The dnf history command

- * 事务在完成前已中止。
- 事务在没有非零状态的情况下完成。

当存在错误代码时，你可以通过`dnf history info (ID)`命令查看详情，如图5.4所示。

```
[root@client #$ dnf history info 39

Begin time      : Wed 22 Jun 2022 06:47:45 PM

Begin rpm      : 793a75b8d23152f1a564f0e5d3681dc5 (0 seconds)

End time       : Wed 22 Jun 2022 06:47:45 PM

End rpm         : 793a75b8d23152f1a564f0e5d3681dc5

User            : root

Return-Code    : 0

Result          : Success

Upgrade         : - --disable-upgrade -y /var/lib/oracle-cloud-agent/pool/f208d4f2-d729-4b83-a352-82f3c3cf0/oracle-cloud-agent-1.24.0.1.el8

Installed       : 0

Packages Altered: 0

Script-out    : Installing oracle-cloud-agent-1.24.0.1.el8.arch64 @oracle-cloud-agent
```



# Installing oracle-cloud-agent-1.24.0.1.el8.arch64 @oracle-cloud-agent

```
2022/06/22 16:47:53 Capability set on /var/lib/oracle-cloud-agent/plugins/hashtoms [ 1 0 0 10 0 0 0 0 0 0 0 0 0 0 0 ]
2 Changing ownership of /var/lib/oracle-cloud-agent/pool to oracle-cloud-agent:oracle-cloud
2022/06/22 16:47:53 Capability set on /var/lib/oracle-cloud-agent/plugins/hashtoms [ 1 0 0 10 0 0 0 0 0 0 0 0 0 0 0 ]
2022/06/22 16:47:53 Capability property on [ 1 0 0 10 0 0 0 0 0 0 0 0 0 0 0 ]
2022/06/22 16:47:53 Capability property on [ 1 0 0 10 0 0 0 0 0 0 0 0 0 0 0 ]
6 Changing ownership of /var/lib/dnf/db to oracle-cloud-agent
8 post install: stop nmap service
10 post install: start starting service
```

![](img/110fa0d6324f0893fff03cee6394144d_165_0.png)

在此示例中，输出是信息性的，没有错误。这并不常见。

你也可以使用 `dnf history` 来卸载软件包。有两种方法：回滚 `rollback` 或撤销 `undo`。
`rollback` 命令将反转从当前点到指定事务 ID 的所有 DNF 事务。`undo` 命令将撤销标识 ID 中的更改。

在测试系统中，你将看到 2022年4月17日安装的 Nmap，它是使用 `dnf history 34` 命令完成的：

```
[root@client #$ dnf history undo 34

Last metadata expiration check: 1:58:19 ago Mon 04 Jul 2022 06:47:45 PM.

Dependencies resolved.

Package             Architecture        Repository       Size

---------------------------------------- ---------------- ----------------

Removing:

nmap                  arch64              2:70-6.el8        @el8_app  23 M

Transaction Summary

Remove                1

Free space: 23 M

This is all we can do: Y

Running transaction check

Transaction succeeded.

Running transaction

Prepared:

Erasing               nmap-2:70-6.el8.arch64        1/1

Running scriptlets:   nmap-2:70-6.el8.arch64        1/1

Verifying:            nmap-2:70-6.el8.arch64        1/1

Done:                 nmap-2:70-6.el8.arch64

Complete!
```



![](img/110fa0d6324f0893fff03cee6394144d_165_1)

这是一个非常简单的 Nmap 撤销操作。查看 `dnf history` 如下：

| ID | Command line | Date and time | Action(s) | Altered |
|---|---|---|---|---|
| 40 | history 34 | 2022-07-04 21:56 | Remove | 1 EE |
| 39 | -dnf remove -y /var/lib/oracle-cloud-agent/pool/2e08d4f2-d729-4b83-a352-82f3c3cf0/oracle-cloud-agent-1.24.0.1.el8 | 2022-06-22 18:54 | Upgrade | 1 |
| 38 | -dnf remove -y /var/lib/oracle-cloud-agent/pool/2e08d4f2-d729-4b83-a352-82f3c3cf0/oracle-cloud-agent-1.24.0.1.el8 | 2022-06-23 14:53 | Upgrade | 1 EE |
| 37 | -dnf remove -y /var/lib/oracle-cloud-agent/pool/2e08d4f2-d729-4b83-a352-82f3c3cf0/oracle-cloud-agent-1.24.0.1.el8 | 2022-06-24 21:50 | Install | 1, U |
| 36 | -dnf remove -y --enabl=nmap_x86_64 | 2022-06-24 21:50 | Install | 1, U |
| 35 | install temp | 2022-06-25 21:48 | Install | 1 |
| 34 | -dnf install -y /var/lib/oracle-cloud-agent/pool/2bd33a67-e751-4b0d-b8f1-c7b2df1d1 | 2022-06-25 23:12 | Install | 1 |
| 33 | -dnf install -y /var/lib/oracle-cloud-agent/pool/2bd33a67-e751-4b0d-b8f1-c7b2df1d1 | 2022-06-26 15:24 | Upgrade | 1 EE |
| 32 | -dnf install -y /var/lib/oracle-cloud-agent/pool/2bd33a67-e751-4b0d-b8f1-c7b2df1d1 | 2022-06-27 21:20 | Upgrade | 1 EE |
| 31 | -dnf install -y /var/lib/oracle-cloud-agent/pool/75f3d58-b6c3-4a12-a5f3-b9f2e36a53 | 2022-07-05 00:23 | Upgrade | 1 |
| 30 | -dnf install -y /var/lib/oracle-cloud-agent/pool/75f3d58-b6c3-4a12-a5f3-b9f2e36a53 | 2022-07-05 15:15 | Upgrade | 1 |
| 29 | -dnf install -y /var/lib/oracle-cloud-agent/pool/75f3d58-b6c3-4a12-a5f3-b9f2e36a53 | 2022-07-06 00:23 | Upgrade | 1 EE |
| 28 | -dnf install -y /var/lib/oracle-cloud-agent/pool/f5d2aca-9254-4c77-b86f-0660b1f366 | 2021-09-30 18:48 | Install | 1 |
| 27 | -dnf install -y /var/lib/oracle-cloud-agent/pool/f5d2aca-9254-4c77-b86f-0660b1f366 | 2021-09-30 18:59 | Install | 1 EE |
| 26 | -dnf install -y /var/lib/oracle-cloud-agent/pool/f5d2aca-9254-4c77-b86f-0660b1f366 | 2021-09-30 19:18 | Install | 1 |
| 25 | install backup | 2021-09-30 19:27 | Install | 1 EE |
| 24 | update | 2021-09-30 19:37 | Upgrade | 1 |
| 23 | update | 2021-09-30 20:01 | Upgrade | 1 |
| 22 | install gdb | 2021-09-30 01:50 | Install | 2 |
| 21 | install kernel-core | 2021-09-30 01:51 | Install | 1 |
| 20 | install kernel-devel | 2021-09-30 01:52 | Install | 1 |
| 19 | install kernel-release | 2021-09-30 01:53 | Install | 1 |
| 18 | install kernel-headers | 2021-09-30 01:54 | Install | 1 |
| 17 | install itrace | 2021-09-30 01:55 | Install | 1 |
| 16 | install openssl | 2021-09-30 01:56 | Install | 1 |
| 15 | install systemd | 2021-09-30 01:57 | Install | 1 |
| 14 | install policycore | 2021-09-30 01:58 | Install | 24 EE |
| 13 | install systemd | 2021-09-30 01:59 | Install | 1 |
| 12 | install tuned-profiles | 2021-09-30 02:00 | Install | 2 |
| 11 | install yum-utils | 2021-09-30 02:01 | Install | 1 |
| 10 | install yum-plugin | 2021-09-30 02:02 | Install | 1 |
| 9 | install /tmp/cloud-agent | 2021-09-30 02:03 | Install | 1 EE |
| 8 | install oracle-utils | 2021-09-30 02:04 | Install | 1 EE |
| 7 | install oracle-utils --exclude=12.6-0 | 2021-09-30 01:45 | Install, U |
| 6 | install oracle-linux-release | 2021-09-30 01:46 | Install | 1 |
| 5 | install oracle-linux-release-el8 | 2021-09-30 01:47 | Install | 1 |
| 4 | install oracle-linux-release-el8-1.0.3.1.el8.arch64 | 2021-09-30 01:48 | Install | 1 EE |
| 3 | install nmap | 2021-09-30 01:49 | Install | 1 |
| 2 | install oraclelinux-developer-el8 | 2021-09-30 01:52 | Install | 37 EE |

![](img/110fa0d6324f0893fff03cee6394144d_166_0)

现在，如果目标是回滚所有更改，例如回滚到 ID 37，事务将是 `history rollback 37`。此回滚将状态恢复到事务完成时的状态。

```
[root@server # dnf history rollback 3]
```

Last metadata expiration: 02:09:13 Mon 04 Jul 2022 06:47:45 PM GMT.

Dependencies required.

------------------------------------------------

Package                 Architecture    Repository      Size

----------------------------------------------------------------



```
Installing:             arch64          2:70-6.el8        el8_appstream   5.7 M

Downgrading:           arch64                               el8_included  64 M

Transaction Summary

1 Install

Total download: 69 M

Is this ok [y/n]

Downloading: oracle-cloud-agent-1.22.0-1.el8.arch64   25 MB/s | 5.7 MB   00:00

(2/2): oracle-cloud-agent-1.22.0-1.el8.arch64   33 MB/s | 64 MB   00:01

Rollback command started

Running transaction check

Running transaction

Removing:               nmap-2:7.70-6.el8.arch64

Installing:            oracle-cloud-agent-1.22.0-1.el8.arch64

Downgrading:           oracle-cloud-agent-1.22.0-1.el8.arch64

Checking ownership of /var/lib/oracle-cloud-agent/rpm.db by oracle-cloud-agent-1.22.0-1.el8.arch64

Checking ownership of /var/lib/oracle-cloud-agent/rpm.db by oracle-cloud-agent-1.22.0-1.el8.arch64

Checking ownership of /var/lib/oracle-cloud-agent/rpm.db by oracle-cloud-agent-1.22.0-1.el8.arch64

post install upgrade = clean old files if not

post finish

Running script: oracle-cloud-agent-1.22.0-1.el8.arch64

Class check: oracle-cloud-agent-1.22.0-1.el8.arch64

Running script: oracle-cloud-agent-1.22.0-1.el8.arch64

Running script: oracle-cloud-agent-1.22.0-1.el8.arch64

Verifying

Downgrading: oracle-cloud-agent-1.22.0-1.el8.arch64

Installing: nmap-2.7:70-6.el8.arch64

Complete!
```

![](img/110fa0d6324f0893fff03cee6394144d_167_0.png)

回滚命令回滚了事务，nmap 最终恢复，并且 oracle-cloud-agent RPM 降级了。这反映在新的历史摘要 ID 41 中（见下面的截图），我们在 ID 41 中看到了安装和降级操作：

```
[root@server # dnf history]

10  command line

41  history rollback 3

35  history undo 4 install -y /var/lib/oracle-cloud-agent/pool/e5f2d0a1-b2c3-4d5e-a6b7-c8d9e0f1a2b3

36  history undo 5 upgrade -y /var/lib/oracle-cloud-agent/pool/f1a2b3c4-e5f6-4a5b-8c9d-0e1f2a3b4c5d

37  history undo 6 * -y /var/lib/oracle-cloud-agent/pool/d7e8f9a0-b1c2-3d4e-4f5a-6b7c8d9e0f1a
```

单次事务或从最新事务回滚到历史中的特定 ID。这对于需要撤销补丁和软件安装的管理员来说，这是一个非常有用的工具。

# 从 ULN 构建 DNF/YUM 镜像

管理员让运行在安全网络（如银行或政府网络）中的系统不启用互联网访问是非常常见的。建立 Oracle **Unbreakable Linux Network (ULN)** 的本地镜像是允许系统访问补丁而无需跨互联网访问的极佳方法。

## 准备工作

要做到这一点，你需要一个运行 Oracle Linux 8 的 YUM 服务器。本地系统应该能够直接或通过代理访问互联网到达 ULN 服务器。只有同步到 ULN 的系统（通常称为 YUM 服务器）需要这种访问权限；使用该系统的所有系统都不需要访问互联网，它们将通过该系统访问补丁。

该系统对 CPU 或内存并不密集——对于服务器来说，2 个核心和 4 GB 内存通常绰有余，但它们消耗大量的磁盘空间。你可以通过运行 `dnf repolist -v` 命令来检查需要多少空间。

取决于服务器订阅了多少仓库，1 TB 的空间很快就会用完。空间方面的好消息是不需要高性能存储。你需要一个有效的 Oracle 支持合同，如果你在 Oracle 服务器上运行，该合同已包含在支持中。在我的本地仓库中，我将仓库放在 `/var` 中，并在**逻辑卷管理 (LVM)** 下将其挂载为单独的文件系统。这样在需要时可以轻松添加额外空间。

此外，应该安装 HTTP 服务器并必须确保防火墙端口已打开。如果你需要执行操作，请返回第 2 章《使用和未使用 Automation Magic 进行安装》，其中涵盖了设置 HTTP 服务器。

## 如何操作...

按照以下步骤构建镜像：

- 1. 第一步是验证 `/var/` 中是否有足够的空间。对于小型镜像，建议从 600 GB 开始。请密切关注磁盘空间，因为以后可能需要它。较大的镜像可以轻松消耗 2 TB。

- 2. 接下来，使用 `dnf install uln-yum-mirror -y` 命令安装 `uln-yum-mirror` 包。`uln-yum-mirror` 包包含了将 Oracle ULN 仓库复制到本地服务器的脚本。确保系统可以访问 `ol8-addons` 仓库：

```
[root@yum ~]# dnf install uln-yum-mirror -y

There was an error communicating with Unbreakable Linux Network or Spacewalk.

Unbreakable Linux Network or Spacewalk based repositories will be disabled.

root: communication error. The message was:

This system is not registered with the server.

Last registration check performed on Mon 04 Jul 2022 06:19:25 PM EDT.

--------------------------------------------------------------------

Package         Architecture Version                    Size

--------------------------------------------------------------------

Installing:

uln-yum-mirror  noarch                0.4.0-3.el8             ol8_addons      37 k

Transaction Summary

Install 1 Package

Total downloaded: 37 k

installed: 78 k

Downloaded: 0 B

uln-yum-mirror-0.4.0-3.el8.noarch.rpm    14 kB/s | 37 kB           00:02

Total

Running transaction check

Transaction check succeeded.

Running test transaction

Test succeeded.

Preparing transactions

Installing:      uln-yum-mirror-0.4.0-3.el8         1/1

uln-yum-mirror-0.4.0-3.el8.noarch      1/1

Verifying:       uln-yum-mirror-0.4.0-3.el8         1/1

Installed:
```



Complete!

```
[root@yum #]
```



![](img/110fa0d6324f0893fff03cee6394144d_169_0.png)

### 3. 这将安装与 Oracle 的交互步骤。接下来，让我们向 ULN 注册系统。使用 `uln_register` 命令。你需要知道将为系统使用的支持标识符 (SI)，以及你的 Oracle 单点登录 (SSO) 凭据。也称为客户支持标识符 (CSI)。要开始注册服务器的过程，在终端运行 `uln_register` 命令，你将看到主屏幕：

![](img/110fa0d6324f0893fff03cee6394144d_169_1.png)

### 4. 点击下一步继续。在下一个屏幕上，系统将提示你输入 Oracle SSO 凭据。CSI 是支持标识符。使用分配给你的高级硬件支持或 Oracle Linux 订阅的 CSI。请勿对 Oracle 数据库、WebLogic、E-Business Suite 等使用 CSI。CSI 应该是用于 Oracle Linux 的。

#### 注意

在生产环境中，你可能想要考虑创建一个共享账户来直接注册所有服务器到 ULN。这使得在人员变动时管理服务器更加容易。

![](img/110fa0d6324f0893fff03cee6394144d_170_0.png)
图 5.11 - `uln_register` 凭据

### 5. 接下来，你需要识别用于 ULN 的服务器。通常你会使用服务器的全限定域名 (FQDN)，你也可以选择硬件详情。

![](img/110fa0d6324f0893fff03cee6394144d_171_0.png)
图 5.12 - `uln_register` 系统名称

### 6. 接下来，系统将更新服务器上安装的 ULN ，这将允许你跟踪直接注册到 ULN 的系统的 RPM。使用本地仓库时，你可能想要使用 Oracle Manager 来跟踪未注册到 ULN 的系统的安装软件：

确定哪些更新软件包与此系统相关非常重要。“我的软件包 (My Packages)”中的 RPM 包可以取消勾选：

- codera-7.6.2-12.el7.x86_64
- ModemManager-glib-1.10.2.el7.x86_64
- ModemManager-1.10.2.el7.x86_64
- NetworkManager-bluetooth-0.26-0-7.1.el7.x86_64
- NetworkManager-libs-0.26-0-7.1.el7.x86_64
- NetworkManager-1.26-0-7.1.el7.x86_64
- NetworkManager-libs-1.10.1.el7.x86_64
- PackageKit-core-0.12-0.1.el7.x86_64
- PackageKit-glib-1.1-6.2.el7.x86_64
- PackageKit-git-1.1-6.2.el7.x86_64
- PackageKit-python-1.1-6.2.el7.x86_64
- PackageKit-glib-1.11-6.1.el7.x86_64
- NetworkManager-wsl-1.36-0-7.1.el7.x86_64
- accountservice-dbus-0.98-12.el7.x86_64
- accountservice-view-lib-0.96-4.el7.x86_64
- adwaita-0.93-12.el7.x86_64
- adobe-maps-maps-20171205-3.el7.x86_64
- adobe-maps-pdf-201708047-1.el7.x86_64
- amixer-4.81-1.el7.x86_64
- adwaita-theme-2.22-3.el7.x86_64
- adwaita-icon-theme-2.22-3.el7.x86_64
- alsa-lib-2.2.10-2.el7.x86_64
- mesa-plugins-pulseaudio-1.1.9-1.el7.x86_64
- mesa-utils-1.6.1-3.el7.x86_64

![](img/110fa0d6324f0893fff03cee6394144d_172_0.png)
图 5.13 – `uln_register` 初始包

向 ULN 注册服务器已完成。最后一步是将发送到 ULN 以注册服务器，这将在下一步中自动完成：

![](img/110fa0d6324f0893fff03cee6394144d_173_0.png)

上传可能需要一分钟时间，取决于你的互联网速度。

上传后，系统现在已注册到 ULN。下一步是可选的。它将为服务器设置 Ksplice。如果你不想使用 Ksplice，就完成了。Ksplice 还需要你拥有 Oracle Linux 高级订阅。这包含在 Oracle 硬件支持和 Oracle Cloud 虚拟机中。你也可以为第三方系统购买，通常比其他商业 Linux 发行版便宜。

![](img/110fa0d6324f0893fff03cee6394144d_174_0.png)

### 8. Ksplice 是一个快速步骤；只需如如下截图所示检查设置并点击 OK：

![](img/110fa0d6324f0893fff03cee6394144d_174_1.png)
图 5.16 - `uln_register` 设置

### 9. 现在注册已完成。在继续之前，你应该使用 `dnf -y update`（如工具建议的那样）对服务器进行补丁更新：

![](img/110fa0d6324f0893fff03cee6394144d_175_0.png)
图 5.17 – 完成的 `uln_register`

### 10. 接下来，继续使用 `dnf update -y` 对系统进行更新并重启系统。注意，`-y` 选项的位置对于命令并不重要。

# ORACLE Linux

ULN 维护已完成，新的 IP 地址已关联到该域名。使用旧地址的防火墙或代理设置的用户需要将其设置更新为新的 IP 地址。更多信息请参阅 My Oracle Support Doc ID: 22250911_11。

常见问题 | 注册 | 登录

![](img/110fa0d6324f0893fff03cee6394144d_176_0.png)

欢迎来到
不可击破的 Linux 网络 (Unbreakable Linux Network)
开放、限制较少且具有最大的自由度。Oracle Linux 可可供任何目的免费使用、修改和分发。它针对 Oracle 数据库、Oracle 应用程序和 Oracle 工程师支持进行了优化。Oracle Linux 是唯一提供完全知识产权索赔保护的 Linux 发行版。

了解更多关于 Oracle Linux >

- 关于
- 文档
- 支持
- 更新
- 商店
- 云服务

- 产品概览 > 切换到 ULN > 在 Facebook 上关注我们 >
- 内核开发博客 > Oracle Linux 博客 > 在 Twitter 上关注我们 >

图 5.18 – ULN 主页

在管理服务器时，请使用相同的登录信息注册服务器。

### 11. 登录 ULN 后，你将看到所有注册到你账户的服务器。你还会看到最近更新并添加到系统的通道：

# 不可击破的 Linux 网络 (ULN)

ULN 维护已完成，新的 IP 地址已关联到该域名。使用旧地址的防火墙或代理设置的用户需要将其设置更新为新的 IP 地址。更多信息请参阅 Oracle Support Doc ID 27210719。

| 系统 | 版本 | 构建版本 |
|---|---|---|
| yum 7 local | 8 | 2022-07-04 |

![](img/110fa0d6324f0893fff03cee6394144d_177_0.png)

### 12. 从这里开始，我们需要将服务器提升为 YUM 仓库。这将允许 ULN 为该服务器分配任何分配的通道，使其能够从特定服务器下载 RPM 包。这包括针对 Oracle Linux 不同主版本的补丁、不同的 CPU 架构（如 AArch64）以及针对 Exadata 等平台的特殊补丁。执行此操作，点击服务器名称，然后点击 Edit（编辑）按钮：

# 不可击破的 Linux 网络 (ULN)

主页 | 通道 | 系统 | 最新 | CVE | 配置管理

主页 > 系统 > yum.m57.local 的系统详情

## 系统详情

名称：yum.m57.local
架构：x86_64
OS 版本：8
发行版本名称：oracle-linux-release
注册日期：2022-07-04

## 订阅

| 名称 | 告告 | 摘要 | 发布日期 | 可下载项目数量 |
| --- | --- | --- | --- | --- |
| Kiprica for Oracle Linux 8 (x86_64) | | Oracle 客户端更新以及 Oracle Linux 8 (x86_64) 的更新 | 2022-06-28 | |
| Oracle Linux 8 Base Release Latest (x86_64) | | 为 Oracle Linux 8 (x86_64) 发布的的基础操作系统包，包括最新的错误修正包 (x86_64) | 2022-06-28 | |
| Unbreakable Enterprise Kernel Release 6 for Oracle Linux 8 (x86_64) | | 为 Oracle Linux 8 (x86_64) 不可击破企业内核版本 6 软件包 | 2022-06-28 | |
| ELA-2022-2149 | container-tools-4.0  修复更新 | 2022-06-19 | 1 |
| ELA-2022-2148 | new-kernel 4.1 | 2022-06-17 | 1 |
| ELA-2022-1899 | new module 5.3 | 2022-05-17 | 40 |
| ELA-2022-1897 | perl-5.3 patches for the RHEL 8 module (x86_64) | 2022-05-17 | 2 |
| ELA-2022-1842 | perl-7.4_bug fix in module (x4) | 2022-03-31 | 1 |
| ELA-2021-1812 | perl-7.4_bug fix and enhancement update | 2022-01-26 | 1 |
| ELA-2021-1801 | 安全修复和性能更新 | 2021-12-30 | 1 |
| ELA-2020-4277 | kernel-5.4 bug fix for the RHEL 8 module (1) | 2020-11-10 | 41 |
| ELA-2020-4272 | new module 5.3 | 2020-11-10 | 1 |
| ELA-2019-3227 | perl-5.24 bug fix and enhancement update | 2019-11-14 | 23 |

下载此系统的所有错误修正

图 5.20 – 编辑服务器

### 13. 在此页面，我们将更新服务器属性以创建一个 Yum 服务器。勾选 **Yum Server** 复选框，然后点击 **Apply Changes（应用更改）**：

# ORACLE Linux
# 不可击破的 Linux 网络 (ULN)

主页 | 通道 | 系统 | 错误修正 | 配置管理

主页 > 系统 > 编辑系统属性

系统属性

| 名称 | yum.m57.local |
| Yum 服务器 | x |
| 主要 CSI | |

图 5.21 – 创建仓库

### 14. 接下来，我们需要为服务器分配额外的通道。这将允许服务器处理任何分配的通道。要管理包含相关 包的命令，点击 Manage Subscriptions（管理订阅）按钮：

# ORACLE Linux
# 不可击破的 Linux 网络 (ULN)

主页 | 通道 | 系统 | 错误修正 | 配置管理

主页 > 系统 > 编辑系统属性

系统属性

| 名称 | yum.m57.local |
| 架构 | x86_64 |
| OS 版本 | 8 |
| 发行版本名称 | oracle-linux-release |
| 注册日期 | 2022-07-04 |

| 名称 | 描述 |
| --- | --- |
| Kiprica for Oracle Linux 8 (x86_64) | Oracle 客户端更新以及 Oracle Linux 8 (x86_64) 的更新 |
| Oracle Linux 8 Base Release Latest (x86_64) | 为 Oracle Linux 8 (x86_64) 发布的的基础操作系统包，包括最新的错误修正包 (x86_64) |
| Unbreakable Enterprise Kernel Release 6 for Oracle Linux 8 (x86_64) | Oracle Linux 8 (x86_64) 不可击破企业内核版本 6 软件包 |

图 5.22 – 管理订阅

### 15. 在此页面，我们将看到左侧的可用通道和右侧的已订阅通道。要添加通道，勾选通道名称旁边的选择框并点击 Add（添加）。要移除通道，取消勾选并点击 Unsubscribe（取消订阅）。

### 16. 接下来，我们需要为服务器分配额外的通道。这将允许服务器处理任何分配的通道。要管理包含相关 包的命令，点击 Manage Subscriptions（管理订阅）按钮：

图 5.23 – 添加更多

### 17. 在下一个页面中，我们将看到左侧的可用通道和右侧的已订阅通道。要添加通道，勾选通道名称旁边的选择框并点击 Add（添加）。要移除通道，取消勾选并点击 Unsubscribe（取消订阅）。

图 5.25 – 完成的镜像

配置完成后，系统将自动将您的本地仓库与 ULN 同步。当添加新通道时，它们将在 `cron` 任务运行时自动下载。

## 创建新的 RPM 软件包

虽然 Oracle 提供了大量的 RPM，但有时您只需要创建一个自定义的 RPM 软件包，以便部署您自己的软件。创建一个 RPM 文件非常简单！

## 准备工作

要完成此操作，您需要一个运行 Oracle Linux 8 的开发系统，并且能够访问 **Extra Packages for Enterprise Linux (EPEL)** 通道。强烈建议使用专门的系统来构建 RPM，而不要在生产系统上构建 RPM。您还需要一个用于测试 RPM 的系统。

> 注意

根据所构建的软件包不同，您可能需要额外的通道，例如 CodeReady 或 Distro Builder。

我们首先需要做几件事——主要是安装 RPM 开发辅助工具。为了实现这一点，我们需要向系统添加 EPEL 仓库。

虽然此书中的大多数配方都使用 `root` 用户完成大部分工作，但本配方将仅在安装软件时使用 root。请以 `root` 身份执行接下来的步骤。

要添加 EPEL 仓库，请运行以下命令：

```



`dnf install oracle-epel-release-el8`

``` 

```

`dnf config-manager --enable ol8_developer_EPEL`

`dnf config-manager --enable ol8_codeready_builder`

`dnf config-manager --enable ol8_distro_builder`

``` 

接下来，我们将安装构建 `rpm` 文件所需的基础实用。运行以下命令来安装它们：

```
dnf install -y rpm-build yum-utils rpmdevtools
```

如果您是从 Git 拉取软件，你可能需要安装 `git` 和 `git-lfs`（`Git` 大文件存储）软件。`gcc`、`make` 和 `python3-service-identity` `RPM` 也是常用的。您可以使用以下命令安装所有这些：

```
dnf install -y git git-lfs make gcc python3-service-identity
```

## 如何操作...

现在我们已经安装了所有工具，我们将切换到您的非 root 用户：

1. 为 `RPM` 创建一个目录。在这里，我们将有一个软件源文件，以及制作 `RPM` 所需的所有文件和目录。在我的情况下，我将所有内容都放在 `/home/erik/`。
2. 接下来，我们需要创建 `RPM` 目录树。这是通过运行 `rpmdev-settree` 命令完成的。一旦运行该命令，树就会在 `$HOME` 下的 `rpmbuild` 中创建。

```
[erik@ol8 rpmbuild]$ pwd

/home/erik/rpmbuild

[erik@ol8 rpmbuild]$ ls

BUILD RPMS SOURCES SPECS SRPMS

[erik@ol8 rpmbuild]$ $
```

> 图 5.26 - `rpmbuild` 目录

还会构建五个目录，每个目录都有特定的用途：

- `BUILD`: 编译后保存二进制文件的地方。
- `RPMS`: `RPM` 在这里创建，生成的 `rpm` 文件可供使用。会有针对不同 `CPU` 架构的子目录。
- `SOURCES`: 源代码存放这里，通常是一个 `tar` 包。
- `SPECS`: `.spec` 文件所在的地方。
- `SRPMS`: 在这里构建源 `RPM`（Source `RPM`）——通常包含软件源代码的软件包。

3. 创建一个简单的 `Bash` Shell 脚本作为 `RPM` 分发。它将位于 `rpmbuild` 目录下的 `xzyzy` 目录。还会创建一个简单的 `Bash` 脚本：

```
[erik@ol8 xzyzy]$ pwd

/home/erik/rpmbuild/xzyzy

[erik@ol8 xzyzy]$ more xzyzy.sh

#!/bin/bash

echo "Nothing Happens"

[erik@ol8 xzyzy]$ $
```

> 图 5.27 - `xzyzy.sh` 脚本

4. 接下来，为 `xzyzy` 目录创建一个压缩 `tar` 包：

```
[erik@ol8 build]$ $ tar -cvf SOURCES/xzyzy-1.0.tar.gz xzyzy

xzyzy/xzyzy.sh
```

5. 现在我们有了简单的 脚本，需要创建 `.spec` 文件。`spec` 文件包含程序名称、描述、许可信息、项目 `URL`、构建架构等。以下命令将在 `SPECS` 目录中创建一个默认 `spec` 文件：

```
rpmdev-newspec SPECS/xzyzy
```

骨架非常空，需要添加信息。示例骨架如下：

```
Name:           xyzzy

Version:

Release:        1%{dist}

Summary:

License:

URL:

Source0:

BuildRequires:

Requires:

%description

%prep

%autosetup

%build

%configure

%make_build

%install

rm -rf $RPM_ROOT

%files

%license

%docs

%changelog

* Sun 10 2022 Erik Benner
```

> 图 5.28 – 基础 `.spec` 文件

6. `rpm` 文件将使用 `rpmbuild` 命令构建，并传递 `spec` 文件的位置。使用 `rpmbuild -bb -v SPECS/xyzzy.spec` 命令，输出如下：

```bash
erik@ol8 rpmbuild rpmbuild -ba SPECS/xyzzy.spec

executing(build): /bin/sh -e /var/tmp/rpm-tmp/*

umask 0022

cd /home/erik/rpmbuild/BUILD

cd /home/erik/rpmbuild

mk -f /home/erik/rpmbuild/SOURCES/xyzzy-1.0.tar.gz

/usr/bin/cd -Rf /home,u=g,w=-

/usr/bin/chmod -Rf ax

executing(install): /bin/sh -e /var/tmp/rpm-tmp.*

cd /home/erik/rpmbuild/BUILDROOT

cd /home/erik/rpmbuild/BUILDROOT/xyzzy-1.0-el18.x86_4 '/*'

mk -f /home/erik/rpmbuild/BUILDROOT/xyzzy-1.0-el18.x86_4

dir -p /home/erik/rpmbuild/BUILDROOT

cp -a /home/erik/rpmbuild/BUILDROOT/xyzzy-1.0-el18.x86_4

cd xyzzy-1.0

dir -p /home/erik/rpmbuild/BUILDROOT/xyzzy-1.0-el18.x86_4 /usr/bin

cp -a /home/erik/rpmbuild/BUILDROOT/xyzzy-1.0-el18.x86_4 /usr/bin

p -a /home/erik/rpmbuild/BUILDROOT/xyzzy-1.0-el18.x86_4 /usr/bin

'/*'

' -x noarch noarch 'j'

/usr/bin/rpmbuild check-build

/usr/bin/rpmbuild check-trans

/bin/ldconfig: Warning: installing configuration file that cannot be opened: /etc/ld.so.conf; No such file or directory found

/usr/bin/rpmbuild --strip */usr/bin

/usr/bin/rpmbuild --strip-static-archive */usr/bin

/usr/bin/rpmbuild --python-hardlink

/usr/bin/rpmbuild --with=redhat/brp-many-shebangs

Provides: xyzzy=1.0-el18

required: rpmlib(CompressedFileNames) <= 3.0.4-1 rpmlib(PayloadFilesHavePrefix) <= 4.0-1

Checking for unpacked package: file:/home/erik/rpmbuild/BUILDROOT/xyzzy-1.0-el18.x86_4/noarch.rpm

executing(clean): /bin/sh -e /var/tmp/rpm-tmp.*.Foock

cd /home/erik/rpmbuild/BUILD

mk -f /home/erik/rpmbuild/BUILDROOT/xyzzy-1.0-el18.x86_4

erik@ol8 rpmbuild
```

> 图 5.29 – 完成的 `.spec` 文件

6. `rpm` 文件将使用 `rpmbuild` 命令构建，传递 `spec` 文件的位置。

7. `RPM` 文件现在位于 `RPMS` 目录下，`noarch` 目录下：

```
[erik@ol8 rpmbuild]$ ls RPMS/noarch

xyzzy-1.0-el18.rpm

[erik@ol8 rpmbuild]$ $
```

> 图 5.31 – `RPM` 文件

该 `RPM` 文件现在可以拷贝到其他系统进行手动安装，或者将其添加到 `YUM` 仓库。

8. 安装后，您可以使用 `rpm -qi xyzzy-1.0` 命令来查看 `.spec` 文件中的许可、描述等详细信息：

```
[root@ol18 ~]# rpm -qi xyzzy-1.0
```



```
Name : xyzzy
Version : 1.0
Release : 1.el8
Architecture : noarch
Install Date : Sun 10 Jul 2022 06:04:01 PM EDT
Group : Unspecified
Size : 35
License : GPL
Signature : (none)
Source RPM : xyzzy-1.0-1.el8.src.rpm
Build Date : Sun 10 Jul 2022 06:00:32 PM EDT
Build Host : oil18.m57.local
Relocations : (not relocatable)
URL : https://xyzzy.net
Summary : A Bash script that prints "Nothing Happens". Sorry, no maze in this one.
Description :
This is a sample shell script, that implements the famous xyzzy command as a bash script. No bugs were used in the making of this sample.
[root@ol18 ~]# 
```

图 5.32 – RPM 文件详情

RPM 工具允许你轻松地分发构建 RPM 文件。这是由 `.spec` 文件驱动的，它包含了创建 RPM 文件所需的所有依赖项、描述、文件位置，甚至是构建信息。

## 6 消除所有 SPOF！冗余性练习

在你的灾难恢复（DR）架构中，冗余至关重要，以确保操作的顺畅。消除单点故障（SPOFs）是实现这一点的常用方法。实施高可用（HA）技术是消除 SPOF 的方法之一。HA 技术至关重要，因为它有助于维护业务连续性、增强性能、提高可靠性、促进灾难恢复（DR）、建立客户信任并符合法规。通过 HA 技术，可以最大限度地减少机时间并确保服务的持续可用性，这有助于在当今技术驱动的世界中获得整体成功和竞争力。

### 注意

DR 又是怎样的？本章将不会涵盖数据中心的故障。尽管如此，实现 DR 的方法与 HA 非常不同。在云端运行时，请寻找如 Oracle Full Stack Disaster Recovery Service 等服务，它可以为顶尖技术栈自动化 DR 过程。

本章中的配方将帮助你消除环境中的 SPOF。我们将首先概述什么是 HA 以及可用性（availability），然后进入如何为你的应用程序添加冗性的示例。用于帮助消除应用程序 SPOF 的四种常用技术是 HAProxy、Corosync、Pacemaker 和 ClusterFS。这些每种技术都提供一组特定的功能，帮助实现应用程序的高可用：

- HAProxy：这是一个负载均衡器，允许你在服务器之间平衡 Web 工作负载。
- Corosync：这是一个通信系统，能够通过通信在应用程序内部实现 HA。
- Pacemaker：Pacemaker 是一个开源资源管理器，用于构建中小型集群。
- ClusterFS：这是一个可扩展的网络文件系统，允许多个节点同时向同一存储器读写数据。

接下来的配方将帮助你实现这些常用的 HA 技术。这包括从应用程序负载均衡、应用程序集群到集群化存储和冗余网络的所有内容：

- 获取 99.999% 的可用性及以上
- 网站的负载均衡
- 使用 Keepalived 使 HAProxy 实现高可用
- 使用 Corosync 和 Pacemaker 为所有人提供 HA 集群
- 在多台之间共享文件系统 – 集群还是分布？
- 在绑定（bond）上生成、配置和监控以太网流量

### 技术要求

对于这些大多数配方，你需要一对 Oracle Linux 8 系统。与大多数此类配方一样，建议使用如 Oracle VirtualBox 等桌面虚拟化产品在你的桌面上运行虚拟机。一个较小的虚拟机即可，配备两个核心、2 GB 内存和几 GB 磁盘空间。你还需要为虚拟机分配一些额外的磁盘，理想情况下至少有五块指定大小的磁盘。在开始之前，请将系统更新到可用的最新包。这只需要几分钟，就能节省大量时间。

你可以通过在整个集群中实现文件系统来实现存储的高可用性（HA）。Gluster 允许你在多台服务器上挂载文件系统，同时在服务器之间进行存储复制。这在文件系统层面上同时提供了可扩展性和可靠性。

最后，网络是一个常见的单点故障，使用网络绑定（network bonding）技术可以同时实现高可用性和扩展能力。这是通过将至少两个网络端口组合成单一虚拟端口来实现的。

### 注意

最佳的 HA 架构结合了这些方法以覆盖整个技术栈。

# 作为网站的负载均衡

如今，大多数应用程序都是基于 Web 的，无论是传统的 Web 界面还是 RESTful API。第一层通常使用负载均衡器来实现 HA。负载均衡器是一个将入流量或工作负载分配到多个服务器或资源的系统。它的主要目标是优化资源利用率、提高性能，并确保应用程序或服务的可靠性和可用性。当多个服务器参与某个应用程序或服务的提供时，负载均衡器充客户端和服务器之间的中介。它接收来自客户端的请求，并根据各种算法（如轮询、最少连接或加权分布）智能地将它们分发到可用服务器上。

负载均衡器负责通过重定向来自过载或出现问题的服务器的流量，确保服务器的最佳健康状态和性能。这种工作负载的分布有助于防止任何服务器过载，从而提高响应时间和整体系统容量及可扩展性。

### 注意

虽然负载均衡器可以帮助分配工作负载，但实际的服务器负载取决于其他因素，因此不要期望所有服务器的 CPU、RAM 等利用率都是相同的。

负载均衡器不仅分发流量，还提供高级功能，如 SSL 终止、会话保持（session persistence）、缓存和内容路由。它们被广泛用于 Web 应用程序、云服务和其他对 HA 和扩展性有要求的环境中。

最流行的负载均衡器之一是 HAProxy。

HAProxy 是一个非常优秀的开源负载均衡器选项。HAProxy 代表高可用代理（High Availability Proxy），由于其卓越的性能以及提高应用程序可用性和可扩展性的能力而被广泛使用。该软件运行在 OSI 模型的应用层（第 7 层），能够根据特定的应用级健康信息（如 HTTP 请求头和 Cookie）做出路由决策。与传统的网络层（第 4 层）负载均衡器相比，HAProxy 提供了更高级的负载均衡和流量路由能力。

HAProxy 的一些关键特性和能力包括：

- **负载均衡**：通过 HAProxy，可以使用各种算法（如轮询、最少连接和源 IP 等）将入站流量均匀地分布到多个服务器上。
- **高可用性**：HAProxy 的优点之一是支持主备故障转移（active-passive failover）配置。当主服务器变得不稳定时，备用服务器将接管。此外，它还具有监控服务器健康状况的能力并通过添加或删除服务器对负载均衡池进行自动调整。
- **代理**：HAProxy 的主要功能之一是作为反向代理，即接收客户端请求并将其重定向到正确的后端服务器。此外，它还可以作为正向代理，拦截客户端请求并将其重定向到外部服务器。
- **SSL/TLS 终止**：通过 HAProxy 可以高效地管理 SSL/TLS 加密和解密，减轻后端服务器的负载。
- **会话保持**：HAProxy 能够通过将客户端的后续请求路由到同一个后端服务器来保持会话粘性，从而保证基于会话的应用程序正常运行。
- **健康检查和监控**：为了保证后端服务器的可用性和最佳性能，HAProxy 会进行例行健康检查。它具有识别故障服务器并将其排除在负载均衡池之外的能力。
- **日志和统计**：通过 HAProxy，管理员可以有效地监控和分析流量模式、性能指标和错误状况。其详细的日志和统计功能使得这一切成为可能。

HAProxy 可以部署在各种操作系统上，通常用于高流量 Web 环境、云基础设施和容器化部署。它的灵活性和功能集使其成为管理流量的强大工具。![](img/10fa0d6324f0893fff03cee6394144d_195_png)

图 6.1 – HAProxy

## 准备工作

为了开始，我们需要三台服务器。我们将它们命名为 `lb1`、`web1` 和 `web2`。它们都拥有 8GB 内存、4 核 CPU。在练习中，我们将为它们分配 IP 地址如下：

| 主机 | IP |
| :--- | :--- |
| Web1 | 192.168.1.200 |
| Web2 | 192.168.1.201 |
| lb1 | 192.168.1.202 |

表 6.3 – HAProxy IP 地址

## Web 服务器

首先，在 Web 服务器上安装 Apache。使用以下命令：

```bash
dnf install httpd -y
```

我们需要在防火墙中开启 80 端口。使用以下命令：

```bash
firewall-cmd --permanent --add-service=http; firewall-cmd --reload
```



我们需要启动服务器并设置开机自启。通过以下命令实现：

```bash
systemctl enable --now httpd
```

## 注意

根据你的环境，你可能需要编辑 Apache 配置文件 `/etc/httpd/conf/httpd.conf` 来指定服务器名称。在文件中如下：

`ServerName web1.local`

这需要进入 `/var/www/html/index.html`。这是一个示例文件。根据需要修改文本以确保服务器是唯一的。这样你就可以看到是哪个服务器在运行：

```html
<!DOCTYPE html>
<html>
<body>
<h1> Running on web1/</h1>
</body>
</html>
```

接下来，将浏览器指向该系统进行测试：

![](img/110fa0d6324f0893fff03cee6394144d_197_png)

图 6.2 – 网站

接下来，在另一台 Web 服务器上重复此过程。一旦该系统启动，我们将设置负载均衡器。

## 负载均衡器

对于负载均衡器系统，我们需要安装 HAProxy。使用 root 用户执行以下命令：

```bash
dnf install -y haproxy
```

我们需要在防火墙中开放 80 端口。使用以下命令：

```bash
firewall-cmd --permanent --add-service=http; firewall-cmd --reload
```

我们需要编辑配置文件，位于 `/etc/haproxy/happroxy.cfg`。

配置文件有两个主要部分：`global` 和 `defaults`。配置文件中只能有一个 `global` 部分。该部分包含了 TLS/SSL 配置数据、日志配置以及运行 `haproxy` 的用户和组设置。默认情况下，`haproxy` 以用户 `haproxy` 和组 `haproxy` 的身份运行。对于大多数情况，`global` 部分通常不需要更改。示例见下图：

### 全局设置

```
global
# 要让这些消息输出到 /var/log/hapxy.log，你
# 需要：
# 1) 配置 syslog 以接受网络日志事件。这是通过
# 在 /etc/sysconfig/syslog 中的 SYSLOGD_OPTIONS
# 添加 '-r' 选项来实现的
# 2) 配置 local2 事件写入 /var/log/hapxy.log 文件。
# 可以在 /etc/sysconfig/syslog 添加如下行：
# local2.*               /var/log/hapxy.log
log local2
chroot /var/lib/hapxy
pid /var/run/hapxy.pid
maxconn 4000
user hapxy
group hapxy
daemon hapxy
# 开启 stats unix 套接字
stats /var/lib/hapxy-policies
# 使用系统级加密算法 PROFILE-SYSTEM
ssl-default-bind-ciphers PROFILE-SYSTEM
ssl-default-server-ciphers PROFILE-SYSTEM
```

图 6.3 - HAProxy 全局设置

下一个部分被称为默认设置（`defaults`）部分，你将在此处进行大部分编辑。它由三个部分组成：`frontend`（前端）、`backend`（后端）和 `listen`（监听）。

`frontend` 部分监听所有定义过的 IP 地址和端口。这是用户连接的地方。一个 HAProxy 服务器可以有多个 `frontend` 部分，但每个部分都需要唯一的名称和 IP/端口组合。

`backend` 部分定义了正在进行负载均衡的服务器，定义了负载均衡方法以及流量发送到的服务器和端口。一个 HAProxy 服务器可以有多个 `backend` 部分，但每个部分都需要唯一的名称。

`listen` 部分用于定义你如何监控负载均衡器，包含监控 HAProxy 所需的端口、URI 和身份验证信息。通常，你只有一个 `listen` 部分。

对于同一个前端，我们将在 `lb1` 系统的 80 端口上监听，命名为 `www_app`，并定义此 IP/端口组合使用 `www_servers` 后端。

### frontend (前端)

HAProxy 配置文件的 `frontend` 部分提供了用于管理流量行为的选项。这些选项可以用于控制前端的流量。以下是一些常用的 `frontend` 选项：

- `bind`：定义前端监听入站流量的 IP 地址和端口。例如，`bind *:80` 监听端口 80 上的所有 IP 地址。
- `mode`：指定前端的模式，如 `http`、`tcp` 或 `ssl`。对于 HTTP 流量，使用 `mode http`。如果你想对通用 TCP 端口进行负载均衡，使用 `mode tcp`。
- `option`：启用或禁用前端选项。一些常用选项如下：
  - `option httplog`：启用 HTTP 请求/响应日志
  - `option dontnull`：防止对 user-agent 字符串缺失或空的请求记录日志
  - `option forwardfor`：在使用 HTTP 代理模式时，在 HTTP 请求头中添加客户端的 IP 地址
  - `option http-server-close`：强制服务器在处理请求后关闭连接，而不是使用 keep-alive
- `timeout`：为前端配置各种超时时间：
  - `timeout client`：设置允许客户端建立连接并发送数据的最大持续时间
  - `timeout server`：设置允许服务器响应请求的最大持续时间
  - `timeout connect`：设置等待后端服务器连接的最长时间
- `acl`：用于匹配特定特定的规则。ACL 与后端配置配合使用，根据各种标准控制流量路由。
- `use_backend`：指定使用哪个后端来处理匹配 ACL 条件的流量。它允许你根据某些条件将流量重定向到不同的后端服务器。
- `default_backend`：定义当没有 ACL 条件匹配入站流量时使用的默认后端。
- `redirect`：针对特定条件执行 URL 重定向。例如，你可以使用 `redirect https://example.com redirect` 将 HTTP 流量重定向到 HTTPS。
- `http-request` 和 `http-response`：这些用于添加自定义的 HTTP 请求/响应头，或根据 HTTP 请求/响应数据执行特定操作。
- `capture`：捕获请求或响应头的部分并将其保存到变量中。

对于示例前端，我们将定义前端为 `www_app`，它绑定到负载均衡器系统上 80 端口的所有 IP。它看起来如下图所示：

### backend (后端)

使用 HAProxy 时，`backend` 选项在配置后端服务器行为以及向它们的流量路由方面起着至关重要的作用。这些选项专门指定在 HAProxy 配置文件的 `backend` 部分中。以下是一些常用的 `backend` 选项：

- `mode`：指定后端的模式，如 `http`、`tcp` 或 `ssl`。对于 HTTP 流量，使用 `http` 模式。
- `balance`：定义负载均衡算法以将流量分发到后端服务器。常用选项包括：
  - `balance roundrobin`：配置请求按轮询方式顺序分配到每个服务器
  - `balance leastconn`：流量发送到活动连接数最少的服务器
  - `balance source`：基于客户端 IP 地址的哈希值，流量一致地导向特定服务器
- `server`：定义正在负载均衡的服务器，以及流量发送到的服务器和端口。
- `timeout`：为后端配置各种超时：
  - `timeout server`：设置允许服务器响应请求的最大持续时间
  - `timeout connect`：设置等待后端服务器连接的最长时间
- `http-request` 和 `http-response`：与前端类似，这些用于添加自定义的 HTTP 请求/响应头，或根据 HTTP 请求/响应数据执行特定操作。
- `cookie`：使用 cookie 启用会话固定。
- `check`：启用或禁用检查。一些常用选项如下：
  - `option httpchk`：启用 HTTP 头部检查
  - `option redispatch`：在失败时允许重新选择服务器
- `errorfile`：指定一个用于前端错误的自定义文件。
- `redirect`：针对特定条件执行 URL 重定向。例如，你可以使用 `redirect https://example.com redirect` 将 HTTP 流量重定向到 HTTPS。

在示例前端，我们将前端定义为 `www_app`，绑定到负载均衡器系统上 80 端口的所有 IP。它看起来如下所示：

```
frontend www_app
bind :80
default_backend www_servers
```



图 6.4 – 示例前端

## 注意

强烈建议始终使用 `check` 选项。

## listen (监听)

在 HAProxy 中，`listen` 部分将前端和后端配置定义在一个块中，这是一种方便的方式。以下是一些常用的 `listen` 选项：

- `bind`：定义前端监听入站流量的 IP 地址和端口。例如，`bind *:80` 监听端口 80 上的所有 IP 地址。
- `stats`：启用监控 HAProxy 的统计页面。
- `stats enable`：启用 HAProxy 统计。
- `stats uri`：指定访问统计页面的 URI 路径。例如，`stats uri /hapxy_stats` 设置页面可通过 `http://your-hapxy-ip/hapxy_stats` 访问。
- `stats realm`：设置访问统计页面时 HTTP 基础认证的域。这增加了一层安全性以防止未经授权的。
- `stats auth`：配置访问统计页面时 HTTP 基础认证的用户名和密码。格式为 `stats auth username:password`。
- `stats hide-version`：从统计页面隐藏 HAProxy 版本号。这在使用动态服务器模板时很有用。
- `stats show-node`：在统计页面上显示服务器节点。
- `stats refresh`：设置统计页面自动刷新的间隔（以秒为单位）。例如，`stats refresh 10` 每 10 秒刷新一次。
- `stats admin`：指定允许访问 HAProxy 统计信息的 IP 地址和端口。它允许通过统计页面进行远程管理。例如，`stats admin localhost` 允许从本地机器访问。
- `stats maxconn`：限制允许统计页面的连接数。有助于防止过载和潜在的拒绝攻击。
- `errorfile`：指定一个用于前端错误的自定义文件。

对于示例 `listen` 部分，我们将其定义为 `metrics`，允许从 `192.168.56.1` 进行管理访问。用户将使用用户名 `admin` 和密码 `password` 登录。

```
listen metrics

bind 192.168.56.1:80

stats enable

stats uri /hapxy_stats

stats auth admin:password

stats admin localhost
```

```
backend www_servers

balance roundrobin

server web1 192.168.56.200:80 check

server web2 192.168.56.201:80 check
```

图 6.5 – HAProxy 示例后端

如下所示：

![](img/110fa0d6324f0893fff03cee6394144d_202_0.png)

由于状态页面运行在端口 `8080` 上，请忘记将该端口添加到防火墙并重新加载防火墙。使用以下命令完成此操作：

```
firewall-cmd --permanent --add-port=8080/tcp

firewall-cmd --reload
```

# 工作原理...

现在我们已经有了两台服务器并配置好了负载均衡器，我们需要启动负载均衡器。这可以通过 `systemctl` 来完成：

- 使用以下命令启动 HAProxy：
  ```
  systemctl start haproxy
  ```
- 使用以下命令检查状态：
  ```
  systemctl status haproxy
  ```
- 如果你编辑了配置文件，不要忘记使用以下命令重新加载 HAProxy：
  ```
  systemctl reload haproxy
  ```



现在，将浏览器指向负载均衡器的 IP 地址。你将看到 Web 服务器页面。如下所示：

![](img/110fa0d6324f0893fff03cee6394144d_202_1.png)

## 在 web2 上运行

规则是轮询（roundrobin），我们将超时时间设置为一分钟，等待一分钟后刷新页面。你会看到一个新服务器。

## 在 web1 上运行

图 6.8 – 负载均衡工作

作为管理员，你可能还会检查资源的健康状况。将浏览器指向 stats URL，并输入配置的用户名和密码。这将显示统计页面。在本例中，URL 为 `http://lb1.m57.local:8080/stats`。你将在图中看到一个示例：

> HAProxy 版本 1.8.27-493ecb, 发布于 2022/10/06
> 通用进程 pid 33536

| Frontend | Cur | Max | Lim | Cur | Max | Lim | Cur | Max | Lim | Time | Last | Time | Last | State | Weight | Err | Dch | Que | Dwn | Dur | Time |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| web1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | | | | | active | | | | | | | | |
| backend1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | | | | | READY | 1 | 0 | 0 | | | | | |
| backend2 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | | | | | READY | 1 | 0 | 0 | | | | | |

图 6.9 – HAProxy 状态页面

在示例页面上，你会看到 web1 在线。你还可以看到每个前端和后端规则有多少流量，指向哪些服务器。

# 使用 Keepalived 实现 HAProxy 高可用性

在上一个方案中，我们使用 HAProxy 为 Web 服务器提供冗余。该方案的挑战是现在负载均衡器本身有了一个故障点。在设计高可用性（HA）架构时，你需要覆盖所有故障点以确保冗余且没有单点故障（SF）。在本方案中，我们使用 Keepalived 为我们的配置添加一些 HA 特性。Keepalived 是一个开源软件，专为基于 Linux 的系统设计。它的主要功能是管理网络负载均衡和故障转移，确保 Web 服务的高。Keepalived 通常与 HAProxy 一起使用。该软件主要利用虚拟路由器冗余协议（VRRP）来实现容错并均匀分布负载。Keepalived 使用以下功能提供冗余：

- 高可用性：通过 Keepalived，你可以建立一个备用服务器集群，它们使用共享的虚拟 IP (VIP) 地址。这种设置确保了如果主服务器发生故障，备服务器将自动接管处理传入的流量，从而实现停机时间最小。
- VRRP：VRRP 是一种常用协议，用于 IP 网络中的路由器自动故障转移。Keepalived 利用 VRRP 保持 VIP 地址运行，并根据需要将其分配给集群中的任何节点。
- 健康检查：Keepalived 的监控系统定期检查活动服务器的健康状况。如果服务器无响应，Keepalived 将将其从池中移除并将流量重定向到健康的服务器。
- 通知机制：通过 Keepalived，可以为故障转移事件或超过特定阈值的情况设置通知。这些通知对于监控集群的整体健康非常有用。

在集群中，Keepalived 指定一个节点为主节点（master），其他节点为备份（backup）。主节点处理传入流量并响应 VIP 地址的 ARP 请求，而备份节点作为备用路由器并监控主节点。节点之间使用 VRRP 协议进行通信，主节点定期发送公告。

![](img/110fa0d6324f0893fff03cee6394144d_205.png)

图 6.10 – Keepalived

如果备份节点停止接收公告或检测到主节点的任何问题，其中一个备份节点将接管成为新主。Keepalived 使用 ICMP (ping) 或第四层检查（例如检查端口是否开放）等机制检查服务器，并将故障服务器从池中移除。VRRP 优先级会被调整以确保健康服务器接管。如下所示，VIP 发生了迁移。

![](img/110fa0d6324f0893fff03cee6394144d_206.png)

图 6.11 – Keepalived

## 准备工作

本方案扩展了上一个方案，增加了第二个负载均衡器和一个 VIP。你需要构建第二个负载均衡器并获取额外的 VIP IP。你的 IP 类似于：

| 主机 | IP |
|---|---|
| web1 | 192.168.56.200 |
| web2 | 192.168.56.201 |
| lb1 | 192.168.56.202 |
| lb2 | 192.168.56.203 |
| vip | 192.168.56.204 |

表 6.4 – Keepalived IP 地址

## 操作步骤

在开始配置 Keepalived 之前，你需要在第二个服务器上配置 HAProxy。你可以轻松地安装 HAProxy、打开防火墙端口并从现有系统复制配置文件。你可以通过将浏览器指向第二个负载均衡器查看应用服务器来进行测试。

接下来，我们将配置 Keepalived。对于每个负载均衡器，你需要以 root 用户身份安装 Keepalived：

```
dnf -y install keepalived
```

接下来，我们需要编辑 Keepalived 配置文件。它位于 `/etc/keepalived/keepalived.conf`。有两个主要部分需要编辑：`global_defs` 和 `vrrp_instance`。

`global_defs` 是 Keepalived 使用的全局定义。这些设置适用于系统中配置的所有 `vrrp_instance` 类型。有几个参数需要更新：

- `notification_email`：当发生事件时将发送邮件的邮件地址列表
- `notification_email_from_user`：发者的邮件地址
- `smtp_server`：SMTP 中继服务器
- `router_id`：此 Keepalived 集群的唯一名称

对于示例，该部分看起来如下：

```conf
global_defs {
  notification_email {
    admins@company.com
    appteam@company.com
  }
  notification_email_from user@company.com
  smtp_server smtp.company.com
  smtp_connect timeout 30
  router id ORACLE_LINUX8
  vrrp_skip_check_adv_addr
  vrrp_strict
  vrrip_garp_interval 50
  vrrip_gna_interval 50
}
```

图 6.12 - Keepalived 全局配置

下一节是 `vrrp_instance`。可以在集群中有多个 `vrrp_instance` 类型，每个类型支持不同的 VIP。

对于 `vrrp_instance`，你需要为每个实例提供唯一的名称。此外，还有几个参数需要更新：

- `state`: 实例的状态，主节点通常为 `master`（主），备用节点为 `backup`（备用）。
- `interface`: 该主机在集群中使用的以太网接口。
- `virtual_router_id`: 此实例的唯一数字。其他实例不应使用相同的 ID。
- `authentication`: 此部分定义了成员身份验证的方式：
  - `auth_type`: 通常设置为 `PASS`，允许节点作为此实例的成员进行身份验证。另一种支持类型称为认证头 (AH)，但不建议使用。
  - `auth_pass`: 实例的密码。
- `virtual_ipaddress`: 由此实例管理的 VIP 列表。

在我们的示例中，该部分看起来如下：

```conf
vrrp_instance VIP1 {
    state MASTER
    interface eth0
    virtual_router_id 10
    priority 100
    advert_int 1
    authentication {
        auth_type PASS
        auth_pass 1234
    }
    virtual_ipaddress {
        192.168.56.204
    }
}
```



图 6.13 - Keepalived vrrp_instance

配置构建好后，将其复制到第二个负载均衡器上。不要忘记在第二个系统上将状态改为 `BACKUP`，如果该系统上的接口不同，也请更新接口。

接下来，以 `root` 用户身份使用以下命令在两个节点上启动 Keepalived：

```bash
systemctl enable --now keepalived
```

现在你可以将浏览器指向 `VIP` 了！这如下例所示。

![](img/110fa0d6324f0893fff03cee6394144d_209_0.png)

# 在 web1 上运行

图 6.14 - 使用中的 Keepalived VIP

你可以通过以下命令查看守护进程的日志条目来检查状态：

```bash
journalctl -u keepalived
```

这将显示守护进程的所有活动。你会看到 `Sending gratuitous ARP messages`，因为这是系统正在检查健康状况。你还会看到关于状态的消息，例如 `Entering MASTER STATE OF` 或 `Entering BACKUP STATE`，因为系统会在 `MASTER` 和 `BACKUP` 之间切换。

# 使用 Corosync 和 Pacemaker实现全 HA 集群

在之前的记录中，我们通过在两个活跃的应用程序服务器之间分配流量来处理 HA。然而，这种方法仅对无状态应用程序有效，即服务器或浏览器不包含特定的用户或会话数据。对于非无状态或运行在复杂服务器上的应用程序，需要一种不同的 HA 方法。解决方案是使用 Pacemaker 和 Corosync 的组合在不同的服务器上启动和停止应用程序组件。这两个开源项目共同工作，为基于 Linux 的系统提供 HA 集群。它们协调并管理集群中的多个节点，确保即使发生硬件或软件故障，关键服务仍然可用。

Corosync 作为 HA 集群栈的通信层，允许节点之间进行可靠的通信。它利用成员关系（membership）和仲裁（quorum）来监控集群活动节点，并确保时刻只有一个节点作为主（或 master）运行。消息层对于共享有关集群状态、时间和资源状况的数据至关重要。Corosync 在集群功能中起着关重要的作用，提供了如下关键功能：

- 集群通信：Corosync 允许节点可靠且高效地交换消息，允许它们协调并同步操作。
- 成员关系和仲裁：Corosync 是一个跟踪集群中活动节点的工具，并使用仲裁算法确保有足够的节点可用做出决策。这有助于避免脑裂（split-brain）场景并确保只有一个节点处于活动状态。避免脑裂集群至关重要，因为它们可能会导致不一致、损坏和服务中断。脑裂场景发生于集群中的节点丢失彼此之间的通信。结果是，每个节点都认为自己是集群中唯一的。这可能是由于网络问题、通信失败或配置错误引起的。

## 注意

当发生脑裂场景时，集群中的几个节点可能会自行运行服务或使用共享资源，认为自己是唯一的活动节点。这可能会导致冲突和数据不一致，因为每个节点在没有任何协调的情况下独立运行。可能的情况下，请在集群中使用奇数个节点，或使用仲裁启用某些保护。

Pacemaker 是一个集群资源管理器，它利用 Corosync 的消息和成员关系功能来管理集群资源并处理资源故障转移。它决定哪些节点在...

## 准备工作

对于本配方，你需要两个虚拟机，每台虚拟机至少有两个 CPU、8 GB 内存和 50 GB 磁盘空间。你应该已经安装了 Oracle Linux 8，并且还有第三个 IP 地址用于由集群管理的浮动 VIP。对于此示例，将使用以下 IP：

| 主机 | IP |
|---|---|
| Web1 | 192.168.56.200 |
| Web2 | 192.168.56.201 |
| vip | 192.168.56.204 |

表 6.5 – HA 集群

在我们开始构建集群之前，你还需要在每个主机上设置 `httpd` (Apache 2.4) 服务器。这与其他配方中的主机设置相似的。

首先，在两个服务器上安装 Apache Web 服务器：

```bash
dnf -y install httpd
```

我们需要启用 Apache 的状态页。这是检查资源的一种方式。要为此，请将以下行复制到 `/etc/httpd/conf.d/status.conf`：

```conf
<Location /server-status>
SetHandler server-status
Order Deny,Allow
Deny from all
Allow from 127.0.0.1
</Location>
```

我们还需要一个简单的 Web 页面。为了测试，请将以下内容放入两个服务器的 `/var/www/html/index.html`。

## 注意

在设置应用程序作为 Web 服务器时，将内容目录（例如 `/var/www/html/`）放在集群系统中可以更容易管理内容的更新。这对于应用程序使用的其他数据（有效，状态数据。

接下来，在两个服务器上使用以下命令将 http 端口添加到本地防火墙：
为了测试，在两个节点上手动启动服务器。不要启用服务的自动启动。这将在 Pacemaker 配置后完成。

```bash
firewall-cmd --permanent --add-service=http; firewall-cmd --reload
systemctl start httpd
```

图 6.15 - httpd 服务器测试

你也可以使用 `wget` 命令测试 `server-status` 页面：

```
wget localhost4/server-status
```

成功的示例输出如截图所示。

```
[root@web01]$# wget localhost4/server-status
-2023-07-29 18:53:47 (67 MB/s) http://localhost4/server-status
Resolving localhost4(localhost4)... ok.
Connect to localhost4(localhost4:127.0.0.1) port 80: connected.
HTTP/1.1 200 OK
Length: 6040 (text/html)
Saving to 'server-status.1'
server-status.1 100%[============================] 5.90KB/s in 0s
2023-07-29 18:53:47 (67 MB/s) 'server-status.1' saved [6040/6040]
[root@web01]$#
```

图 6.16 - server-status 成功

你现在已经准备好安装并配置 Pacemaker 和 Corosync 了。

## 如何操作...

现在你已经安装了我们将要集群化的 Apache `httpd` 服务器，让我们从安装软件开始。首先，我们需要启用 `addons` 仓库。通过在两台服务器上以 `root` 身份执行以下命令来完成：

首先，在两个节点上，以 `root` 身份通过以下命令启用仓库：

```
dnf config-manager --enable ol8_addons
```

然后，你将安装软件：

```
dnf install -y pacemaker pcs
```

一旦完成这些包的安装，系统将添加一个新用户 `hacluster`。请注意，该用户的远程登录将将被禁用。为了执行同步其他节点上的配置或服务等任务，有必要在两个节点上为 `hacluster` 用户设置相同的密码。我们可以使用 `passwd` 命令来设置密码：

```
passwd hacluster
```

接下来，我们需要启用 `pcs` 服务并启动它：

```
systemctl enable --now pcsd.service
```

接下来，我们需要为集群端口打开防火墙。通过以下命令完成操作：

```
firewall-cmd --permanent --add-service=high-availability ; firewall-cmd --reload
```

现在我们暂时处理好了节点。接下来的几个命令可以在任一节点上执行，但注意，你仍然应该是 `root` 身份。

接下来，我们需要将两个节点添加到集群中：

```
pcs host auth web1 web2 -u hacluster
```

## 注意事项

如果你的节点在 DNS 或 `/etc/hosts` 文件中无法解析，你可以选择地在每个主机名之后添加 `addr=$IPADDR`。强烈建议让所有主机都是可以解析的。如果使用此选项，它看起来如下：

```
pcs host web1 addr=192.168.56.200 node2 addr=192.168.56.201 -u hacluster
```

接下来，我们将创建集群：

```
pcs cluster setup webapp web1 web2
```



现在，我们可以启动集群：

```
pcs cluster start --all
```

要验证集群是否正在运行，我们可以使用 `pcs` 命令进行检查：

```
pcs cluster status
```

一个健康的新集群应该返回与以下示例类似的输出：

```
[root@web1 conf.d]# pcs cluster status

Cluster Status:

Status of pacemaker-mgr: 'Pacemaker is running' (last updated 2023-07-29 21:04:38 -04:00)

Cluster Summary:

  * Stack: corosync

  * Current: DC2 (version 2.1.5-0.1.el18-a3f4474f94) - partition with quorum

  * Last updated: Sat Jul 29 21:03:33 by hacluster via crmd on web2

  * Last change: 22 configured

  * 0 resource instances configured

Node List:

  * Online: [ web1 web2 ]

PCS Status:

web1: Online

web2: Online
```

![](img/110fa0d6324f0893fff03cee6394144d_214_0.png)

在仅包含两个节点的集群中，法定人数（quorum）的运行机制与更多节点的集群不同。在这样的集群中，法定人数值设置为 1，以确保主节点始终被考虑在法定人数内。如果两个节点都由于网络中断而离线，集群将竞争相互隔离（fencing），第一个成功的节点将获得法定人数通过。为了增加首选节点赢得法定人数的概率，可以配置隔离代理（fencing agent）给其提供优先级。这通过以下命令完成：

```
pcs resource defaults update
```

最后一步是禁用 STONITH，它代表“Shoot The Other Node In The Head”（打掉另一个节点的头）。这是一个高级的隔离工具，需要根据你的环境进行特定配置。如果你想通过技术监控此项，请查看这里的 Oracle 官方文档 — https://docs.oracle.com/en/operating-systems/oracle-linux/8/availability/ConfiguringFencingstonith.html

```
pcs property set stonith-enabled=false
```

为了设置集群，我们需要创建一个集群。

```
[root@web1 ~]# pcs constraint

Location Constraints:

Resource: WebApp

Enabled on:

  Node: web2 (score:INFINITY) (role:Started)

Ordering Constraints:

Colocation Constraints:

Ticket Constraints:

[root@web1 ~]# #
```

![](img/110fa0d6324f0893fff03cee6394144d_218_0.png)

Pacemaker/Corosync 强大之处在于其灵活性。你可以用它对任何内容进行集群化，使其系统管理员的强大工具。

# 在多机器间共享文件系统——集群还是分布式？

当你开始使用负载均衡器和集群软件技术时，通常会遇到需要在多台服务器上使用相同文件的情况。你可以简单地复制文件，但如果可以在每台服务器上挂载文件，从而在不引入 NFS 服务器带来的单点故障（SPOF）的情况下跨系统共享文件系统呢？实现这一点最简单的方法之一就是使用 Cluster。

Gluster（也称为 GlusterFS）是一个开源分布式文件系统，为海量数据提供可扩展且灵活的存储。它最初由 Gluster, Inc. 开发，现在由开源社区维护。Gluster 使用分布式架构创建一个单一且统一的文件系统，该系统可以跨越多个服务器和存储设备。这种方法允许你聚合多个服务器的存储容量，并将其作为一个单一、结构良好的文件系统呈现给用户和应用程序。它有广泛的应用，如数据存储、备份和内容分发。

Gluster 的核心特性和概念包括：

- 可扩展性：向集群中添加更多存储服务器允许 Gluster 能够通过水平扩展轻松应对不断增长的数据需求。
- 冗余性：Gluster 通过在多个节点之间复制数据来确保冗余和容错能力，从而保证可用性。
- 灵活性：Gluster 支持多种存储选项，包括本地磁盘、NAS 和云存储。它可以根据特定的用例和技术进行定制。
- 文件系统抽象：它为用户和应用程序提供了标准的文件系统接口，使其集成到现有系统中变得相对于容易。
- **数据分布**：数据以一种提高性能和可靠性的方式分布在整个集群中。数据可以均匀分布，也可以根据特定标准进行分布。
- **自动修复**：Gluster 具有自愈功能，可以自动检测并修复数据不一致或损坏的文件。

Gluster 通常用于需要大规模分布式存储的环境，例如 Web 服务器、云计算、大数据分析和媒体流传输服务。它为管理跨网络服务器和存储设备的数据提供了一种极具成本效益且灵活的解决方案。

## 准备工作

对于本教程，你需要两个 Oracle Linux 8 系统，每台系统都能够访问 YUM 仓库。在练习中，我们将它们命名为 `gluster1` 和 `gluster2`。它们是相同的系统，每台配有 8 GB 内存、4 个 vCPU 和 100 GB 空间。文件系统有 50 GB，`/home` 目录有 5 GB，swap 分有 8 GB。剩余空间未分配。此外，在本示例中，每个节点将有一个用于 Gluster 数据的 100 GB LUN。

## 警告

强烈建议集群中至少有三个节点，以避免出现“脑裂”（split-brain）集群。虽然双节点集群是可行的，但如果系统发生分裂，就会带来数据损坏的风险。脑裂集群在分布式计算环境中是不受欢迎的，因为它们可能导致数据不一致、损坏和操作问题。脑裂发生在集群中的节点失去彼此的连接或通信时，导致集群分裂为多个孤立的节点。每个节点都认为自己是活动或主集群，导致产生冲突和数据差异的可能。

在每台服务器上，你将执行以下准备工作：

- 1. 在 100 GB LUN 上创建一个 XFS 文件系统。这将用于存储 Gluster 数据，称为 bricks（砖）。在 Gluster 的语境中，brick 是存储集群内的基本存储单元。集群由多个 bricks 组成，每个 brick 本质上指向存储设备。每个 brick 代表了集群总存储容量的一部分。
- 2. 由于我们将使用 Gluster 来管理存储，将不会使用 LVM。在这些系统中，`/dev/sdb` 是 100 GB LUN。使用以下命令来创建并挂载文件系统：

```
mkfs.xfs -i size=512 -L gluster /dev/sdb

mkdir -p /data/glusterfs/volumes/bricks

echo 'LABEL=gluster /data/glusterfs/volumes/bricks xfs defaults 0 0' | sudo tee -a /etc/fstab

mount -a
```
- 3. 完成后，使用 `df` 命令验证文件系统已挂载，如下所示：

```
root@gluster2 # df -h

Filesystem      Size Used Avail Mounted on

tmpfs           3.8G 0 3.8G 0% /dev

tmpfs           3.8G 0 3.8G 0% /dev/shm

tmpfs           3.8G 9.0M 3.8G 1% /run

tmpfs           3.8G 0 3.8G 0% /sys/fs/cgroup

dev/mapper/ol-root 50G 5.6G 45% /

dev/sdb                 100G 0 100G /glusterfs/volumes/bricks

dev/mapper/ol-var 50G 7.1G 43% /var

dev/mapper/ol-home 50G 8.3M 50% /home

dev/mapper/ol-tmp 50G /tmp

dev/sda1          10G 4.5G 47% /boot

tmpfs            256M 0 /user
```
- 4. 我们需要确保所有节点都在 `/etc/hosts` 文件中。在示例中，gluster2 和 gluster3 同时使用了短名和完全限定域名（FQDN）。如下：

```
root@gluster3 ~]# cat /etc/hosts

127.0.0.1 localhost.localdomain

::1 localhost.localdomain
```



192.168.0.10 `gluster1.localdomain`

192.168.0.11 `gluster2.localdomain`

`root@gluster3 ~]#`

### 5. 安装 Gluster 仓库并启动服务
为了安装，我们需要启用 Gluster 仓库。然后安装并启动 gluster 服务器。通过以下命令完成：

```
dnf -y install gluster-release-el8
dnf -y config-manager --enable module:glusterfs:ol8-appstream-latest
dnf -y install gluster-server
systemctl enable --now gluster
```

### 6. 验证 Gluster 守护进程
运行后，可以通过 `systemctl status gluster` 验证 Gluster 守护进程正在运行。验证服务处于激活状态如下：

```
root@gluster1 ~]# systemctl status gluster
● gluster.service - GlusterFS, clustered-system server
Loaded: loaded (/lib/systemd/system/gluster.service; vendor preset: disabled)
Active: active (running) since Sat 2023-06-02 11:25:07 UTC; 1min ago
Doc: gluster(8)
Process: 4468 (Exec: /var/run/gluster.pid --log-level INFO)
Main PID: 4468
Tasks: 9 (limit: 4538)
Memory: 39M
group: system.slice/gluster.service
└─4468 /var/run/gluster.pid --log-level INFO
Sep 02 11:25:07 system[1]: Starting GlusterFS, clustered-system server...
Sep 02 11:25:07 system[1]: Started GlusterFS, clustered-system server.
```

### 7. 配置防火墙
接下来，使用以下命令配置防火墙允许 glusterfs 端口：

```
firewall-cmd --permanent --add-service=glusterfs
firewall-cmd --reload
```

### 8. 创建自签名密钥加密通信
此外，为了提高安全性，让我们创建一个自签名密钥来加密节点之间的通信：

```
openssl genrsa -out /etc/ssl/gluster.key 2048
openssl req -new -x509 -days 365 -key /etc/ssl/gluster.key -out /etc/ssl/gluster.pem
```

生成 `.pem` 文件时，由于是自签名证书，你需要在证书中输入联系信息；可以使用可以使用值！

## 注意

在本示例中，我们使用了自签名证书。在安全的生产环境中，你可能希望考虑使用商业签名证书。

我们稍后将使用这些文件加密通信。

## 如何操作...

现在每个节点上已完成所有准备工作，我们将创建可信存储池并加密通信。这将为创建卷（数据存储和共享的地方）做好所有准备。

Gluster 中的可信存储池是指一个 Gluster 服务器集群（称为存储节点或对等节点），它们之间建立了信任，以便在集群内协同工作。这种信任通过可信存储池配置建立，通常涉及以下步骤：

- 身份验证：可以使用 SSH 密钥、证书或共享密钥等方法验证可信存储池中的节点。这确保了只有授权的服务器才是存储集群的一部分。
- 授权：节点通过验证后，它们相互授权访问和管理存储集群内的特定数据。授权设置决定了哪些节点对集群内的特定卷或砖具有读写权限。
- 通信：可信存储池的成员通过安全网络进行通信，以复制数据、同步元数据和其他集群相关操作，确保存储功能协同运行。
- 数据完整性：可以在可信池中添加更多存储节点，从而增强存储容量和性能。存储池的可信特性使得新节点轻松加入集群并贡献资源。

### 1. 探测集群节点创建池
要创建池，我们需要探测集群中的其他节点。在本例中，我们将使用 `gluster peer probe gluster2` 命令从 cluster1 探测到 cluster2：

```
[root@cluster1 etc]# gluster peer probe gluster2
peer probe: success
```

### 2. 查看对等节点列表
随后，你可以使用 `gluster pool list` 来查看哪些节点与你运行命令的节点建立了对等关系；在接下来的示例中，命令是在 cluster2 上运行的。

```
[root@cluster2 etc]# gluster pool list
UUID                Hostname    State
b13801d3-dcdbd-487b-a23-b3f3-2e95a8fb632 gluster1  Connected
bc003cd0-f733-4a25-85bf-40a7c387d667 localhost   Connected
```

### 3. 确认双向连接
在这里我们看到 `gluster1` 和 `localhost` 已连接，因为这是在 cluster2 上运行的。如果你在 `gluster1` 上运行相同的命令，你将看到 cluster2 是远程主机：

```
[root@cluster1 -#] gluster pool list
UUID                Hostname    State
bc003cd0-f733-4a25-85bf-40a7c387d667 gluster2  Connected
b13801d3-dcdbd-487b-a23-b3f3-2e95a8fb632 localhost   Connected
```

### 4. 创建复制卷
现在我们已经有了集群，让我们创建一个复制卷（volume）。该卷将在跨集群重写砖块（bricks），从而实现对存储器故障或节点故障的保护。

以下命令将创建该卷：

```
gluster volume create datal replica 2
gluster(1,2):/data/glusterfs/volumes/bricks/datal
```

一旦创建创建，我们需要启动它：

```
gluster volume start datal
```

### 5. 挂载卷
我们现在可以挂载它了。目前，我们将使用 gluster 原生客户端并将其挂载到 `/mnt` 挂载点：

```
mount -t gluster cluster2:datal /mnt
```

### 6. 查看挂载存储
我们现在可以使用 `df` 命令查看挂载的存储：

```
root@gluster2 #$ df -h
Filesystem      Size Used Avail Use Mounted on
tmpfs           3.8G 0 3.8G 0% /dev
tmpfs           3.8G 84K 3.8G 1% /dev/shm
tmpfs           3.8G 9.0M 3.8G 0% /run
tmpfs           3.8G 0 3.8G 0% /sys/fs/cgroup
dev/mapper/ol-root 50G 5.5G 45G 11% /
dev/sda         100G 7.8M 94.6G 16% /data/glusterfs/volumes/bricks
dev/mapper/gluster-home 5.0G 0 5.0G 0% /home
dev/sda1        101G 49M 101G 0% /boot
dev/mapper/ol-var_tmp 5.0G 84M 5.0G 2% /var/tmp
tmpfs           765M 4.0K 765M 1% /run/user/0
gluster2:data1 100G 1.8G 999G 2% /mnt
root@gluster2 #$ _
```

图 6-23：data1 挂载在 `/mnt`

### 7. 在其他节点挂载
如果你想使用其他节点，你需要在每个节点上重复该命令。以下示例显示了在 `gluster1` 上的挂载：

```
mount -t gluster gluster1:data1 /mnt
```

### 8. 准备加密文件
接下来，我们需要使用之前创建的密钥设置加密。第一步是将之前创建的 `.pem` 文件合并到 `/etc/ssl/glusterfs.ca`。该文件应该放在集群的所有节点上。

### 9. 启用加密访问
现在，我们需要启用加密。通过以下命令在每个节点上 touch `secure-access` 文件来完成：

```
/var/lib/gluster/secure-access
```

### 10. 为卷启用 SSL
现在，对于每个卷，我们都需要为集群和服务器启用 SSL。在示例命令中，我们将为创建的 `data` 卷启用它：



`gluster volume set data client.ssl`

`gluster volume set data server.ssl`

现在，重启 gluster：

```
systemctl restart gluster
```

Gluster 通信现在已对该卷加密...

使用 Gluster 还可以做更多事情。在创建卷时，卷有多个选项，提供了复制和分布：

- **Distributed**（分布式）：使用分布式卷时，文件随机分布在卷的砖块上。这种类型的卷适用于需要扩展存储且不需要硬件或软件提供冗余的情况。但需要注意的是，磁盘或服务器故障会导致数据丢失，因为数据随机分布在卷的砖块中。构建分布式卷的示例命令如下：

```
gluster volume create data gluster(1,2):/data/gluster/bricks/datal
```

- **Replicated**（复制）：文件在砖块之间复制以实现高可用（HA）。构建复制卷的示例命令如下：

```
gluster volume create data replica 2 gluster(1,2):/data/gluster/bricks/datal
```

- **Replicated**（复制）：卷中的砖块之间分布以提高读取性能、HA 和可靠性。创建分布式卷时，节点数应该是砖块数的倍数。构建分布式卷的示例命令如下：

```
gluster volume create data replica 2 gluster(1,2,3,4):/data/gluster/bricks/datal
```

- **Dispersed**（纠散）：该卷利用纠删码有效防止磁盘或服务器故障。纠散卷允许在多个砖块上存储编码数据，同时添加冗余以确保可靠性。纠散卷允许以极小的空间进行自定义。纠散卷必须至少六个砖块。构建纠散卷的示例命令如下：

```
gluster volume create data disperse 3 gluster(1,2,3):/data/gluster/bricks/datal
```

- **Dispersed**（纠散）：砖块之间分布数据，提供了与复制卷相同的处，但使用了纠散存储。纠散卷必须至少六个砖块。构建纠散卷的示例命令如下：

```
gluster volume create data disperse 3 gluster(1,2,3,4,5,6):/data/gluster/bricks/datal
```

在向卷中添加砖块时，你可以在每个节点上放置多个砖块。只需定义额外的砖块。在本示例中，创建一个纠散卷，并在每个节点上放置两个砖块：

```
gluster volume create data disperse 3 gluster(1,2,3):/data/gluster/bricks/datal

gluster(1,2,3):/data/gluster/bricks/datal
```

可以使用卷名停止卷。停止卷的示例如下：

```
gluster stop datal
```

你可以向卷添加砖块以进行扩展。这可以在新节点加入集群后完成。在以下示例中，首先使用 `gluster node probe` 命令将 gluster3 加入集群，然后使用以下命令扩展数据：

```
gluster volume add brick datal:/data/gluster/bricks/datal
```

### 注意

在向卷中添加砖块时，确保添加了所需数量的砖块。分布式卷等类型需要多一个砖块。你也可以以下命令检查所有卷的状态：

```
gluster volume status
```

如下所示：

```
root@gluster1 ~# gluster volume status

Status of volume: data1

Gluster process

TCP Port RDMA Port Pid

Brick gluster1:/data/glusterfs/volumes/bricks/data1 49152 0 19239

Brick gluster2:/data/glusterfs/volumes/bricks/data1 49152 0 18656

Self-heal Daemon on localhost M/A/A Y 19741

Self-heal Daemon on gluster2 M/A/A Y 19259

Task Status of Volume data1

There are no active volume tasks
```

图 6-24 - 卷状态

可以通过在命令中添加卷名查看单个卷的摘要。你还可以通过添加 `detail` 选项查看更多细节。这些可以结合，所示：

```
root@gluster1 ~# gluster volume status detail

Status of volume: data

Brick                : gluster1:/data/glusterfs/volumes/bricks/data

TCP Port            : 49152

RDMA Port           : 0

Online              : Y

id                  : 19239

File System         : xfs

Device              : /dev/sda

Mount Options       : rw,selabel,relative,attr2,inode64,logbufs=0,logsize=32k,noquota
```

```bash

[root@gluster1]# gluster volume top data write-perf bs 1024 count 1024

Brick: gluster1:/data/glusterfs/volumes/bricks/data1

Throughput 624.52 Mbps 8.0081 secs

Time

====

0 /test2

Brick: gluster2:/data/glusterfs/volumes/bricks/data1

Throughput 765.30 Mbps 8.0014 secs

Time

====

0 /test2

[root@gluster1]# gluster volume top data read-perf bs 1024 count 1024

Brick: gluster1:/data/glusterfs/volumes/bricks/data1

Throughput 2595.49 Mbps 0.0004 secs

Brick: gluster2:/data/glusterfs/volumes/bricks/data1

Throughput 2608.40 Mbps 0.0004 secs

[root@gluster1]# gluster volume top data write

Brick: gluster1:/data/glusterfs/volumes/bricks/data1

Count

=====

812486 /test2

Brick: gluster2:/data/glusterfs/volumes/bricks/data1

Count

=====

812487 /test2

[root@gluster1]#
```



![](img/110fa0d6324f0893fff03cee6394144d_227_0.png)

可以删除卷。这可以通过 `volume delete volume_name` 命令完成，其中 `volume_name` 是要删除的卷。请注意，在删除卷时，不要忘记使用 `rm` 命令从存储器中删除砖（bricks）。

## 在 bond 上生成、配置和监控以太网流量

当裸金属服务器作为专用主机或运行 KVM 虚拟化程序的虚拟机的 Linux 系统时，网络可能会成为薄弱环节。幸运的是，可以通过实施以太网绑定（Ethernet bonding），也称为网络绑定（network bonding）或网卡绑定（NIC bonding）来解决这个问题。这是 Linux 中的一项技术，允许你将多个网卡合并为单个逻辑接口。该逻辑接口被称为 `bond` 或绑定接口，提供更高的网络带宽、容错能力和负载均衡。这些特性总结如下：

- 负载均衡：将网络流量分布到多个网卡上，增加带宽。根据特定需求可以使用各种算法，例如轮询（round-robin）、主备式（active-backup）和异或（XOR）。
- 容错：在网卡或网络链路故障时，以太网绑定可以自动切换到另一个活动网卡。这提供了冗余和容错能力，确保即使其中一个网卡不可用，网络连接也能保持可用。
- 链路聚合：绑定可用于创建链路聚合组（LAGs）或网卡团队（NIC teams），从而增强高可用（HA）设置中的带宽和冗余性。

在本教程中，我们将配置绑定，然后展示一些常用工具，这些工具允许你同时监控和生成通过 `bond` 的以太网流量。

此外，你还需要熟悉几项技术。

## MAC

介质访问控制（MAC）地址是分配给以太网和 Wi-Fi 器等网络接口的硬件标识符，用于在局域网上进行通信。它在制造过程中被硬编码到网络硬件中，用于 OSI 模型中的数据链路层（第 2 层）。MAC 地址最重要的特征之一是它们的唯一性。每个 MAC 地址按理上应该是全球唯一的，制造商有责任确保没有两个接口具有相同的 MAC 地址，尽管在实践中（特别是在虚拟化环境中）这可能是一项具有挑战性的任务。这在网络中可能会引发问题，因为任何网络上的重复 MAC 地址都会导致问题。此外，许多绑定模式依赖 MAC 地址进行流量负载均衡。

## 绑定模式

绑定模式指的是各种策略或算法，用于决定如何将网络流量在通过 Linux 驱动程序聚合到绑定接口的多个接口之间进行分布。这些模式控制着绑定接口的负载均衡和故障转移行为。绑定模式的选择取决于你的网络需求和目标。以下是一些常见的 Linux 绑定模式：

- `balance-rr`：在此模式下，传出的网络流量以轮询方式均匀分布在所有可用网络接口上。这是一种简单的负载均衡模式，可以提高出站性能，但没有考虑接口的状态，可能会导致流量分布不均。偶尔，这种模式与某些交换系统配合得不好。
- `active-backup`：一种常用模式；通常被称为故障转移模式，该模式有一个主接口，其他接口处于备用状态。如果主接口失败，将自动激活下一个可用接口以确保连续性。这种模式提供了可靠性，是任何环境中中最易运行的模式之一。
- `balance-xor`：此模式利用简单的异或操作来维护数据传输和接收之间的平衡。该过程涉及根据源和目的地的 MAC 地址分发流量。它保证了两个终端始终走相同的路径。这种模式的主要目的是确保容错性。偶尔，这种模式与某些交换系统配合得不好。
- `balance-tlb`：在此模式下运行时，传出的流量根据其当前负载分布在所有可用接口之间。然而，入站流量不会进行主动均衡，且仅由活动接口接收。这种模式在交换机不支持链路聚合控制协议（LACP）时特别有用。偶尔，这种模式与某些交换系统配合得不好。
- `balance-alb`：此模式通过考虑每个接口的可用性和负载，主动平衡入站和出站流量。偶尔，这种模式与某些交换系统配合得不好。

## LACP

上述模式都可以在不对应交换机进行更改的情况下运行。然而，还有另一种更常用的模式，被称为 LACP。LACP 是用于将多个网络连接（如以太网）聚合为单个高带宽链路的模式。这种过程通常被称为链路聚合、网卡团队或绑定。LACP 由 IEEE 802.3ad 标准定义，常用于数据环境中确保网络性能、冗余和容错。

要使用 LACP，必须对交换机进行配置。作为管理员，必须通信配置需求，以确保交换机的配置兼容。两端配置匹配时 LACP 才能工作。大多数企业级交换机和服务器网卡都支持 LACP。LACP 的关键特性和功能包括：

- 聚合链路：LACP 允许将多个物理链路聚合为单个逻辑链路，在网络设备中显示为单个接口。
- 增加带宽：通过 LACP 聚合多个链路可以增加密集型应用和服务器到交换机连接的带宽。然而，每个 MAC 到 MAC 的连接通常受限于链路单个成员的速度。如果你有一个具有双1 Gbps 链路的主机，主机与客户端之间的通信可能无法超过 1 Gbps。
- 负载均衡：LACP 可以根据各种负载均衡算法在聚合链路之间重新分配网络流量，防止单个链路拥塞并优化网络利用率。
- 容错：除了增加带宽外，LACP 还提供了冗余和容错能力。如果某个链路故障，LACP 可以自动将流量重定向到活动链路，减少停机时间并确保网络可用性。
- 动态协议：LACP 是一种动态协议，通过 LACP 帧在网络设备之间动态协商并建立链路聚合。
- 模式：LACP 支持两种工作模式：

    字体 主动模式：在主动模式下，设备主动发送 LACP 帧以协商并建立链路聚合。
- 被动模式：在被动模式下，设备监听 LACP 帧但不主动发送。它依赖于配置为主动模式的另一端来发起聚合。

## 准备工作

对于此配方，你需要三个 Oracle Linux 8 系统，每个系统都能够访问 `yum` 仓库。在练习中，我们将它们命名为 `networking`、`client1` 和 `client2`。它们大多是相同的系统，每个系统拥有 8 GB 内存、4 个 vCPU 和 100 GB 磁盘空间。区别在于 `networking` 应该在同一个网络上有两个网络接口。文件系统在 `/` 占用 50 GB，`/home` 占用 5 GB，`swap` 占用 8 GB。剩余磁盘空间未分配。

## 如何操作...

虽然可以通过 GUI 完成，但本配方将介绍如何通过命令行完成。请注意，在处理服务器的主网络连接时，你将处于系统控制台。通过 SSH 等远程连接进行可能会导致你失去对服务器的访问。以下是配置冗余连接的步骤。

- 1. 首先你需要创建一个 `bond`（绑定）。在示例中，我们将使用 `balance-alb` 模式创建它，以最好地平衡入站和出流量：
```bash
nmcli connection add type bond con-name "Bond 0" ifname bond0.options "mode=balance-alb"
```
- 2. 接下来，我们将 `bond` 配置为 DHCP。在生产服务器上，你通常会使用手动配置的 IP 地址：
```bash
nmcli connection modify "Bond 0" ipv4.method auto
```
- 3. 添加作为 `bond` 成员的适配器。在这种情况下，我们将使用 `enp0s3` 和 `enp0s8`：

### 注意

如果你正在向已使用的 `bond` 中添加端口，你应该现在删除该端口。在这种情况下，`enp0s3` 正在使用中，因此通过以下命令将其删除：
```bash
nmcli connection add type ethernet slave-type bond con-name bond0-if1 ifname enp0s3 master bond0
nmcli connection add type ethernet slave-type bond con-name bond0-if2 ifname enp0s8
```

- 4. 现在，我们将启动连接并检查状态：
```bash
nmcli connection up "Bond 0"
nmcli device
```

完成后，`nmcli device` 命令的输出应该如下所示：

```
root@networking ~# nmcli device
DEVICE TYPE STATE CONNECTION
bond0 bond connected Bond0
enp0s3 ethernet connected Bond0-if1
enp0s8 ethernet connected Bond0-if2
lo loopback unmanaged --
root@networking ~#
```

图 6.26 - 正常 `bond` 的 `nmcli device` 输出

你可以看到 `bond0` 是设备，成员是 `enp0s3` 和 `enp0s8`。

- 5. 当你查看 IP 地址时，你会发现它现在位于 `bond0` 设备上。可以通过 `ifconfig bond0` 命令进行检查，输出如下：

```
root@networking ~# ifconfig bond0
bond0: flags=5107<BROADCAST,RUNNING,MASTER,MULTICAST> mtu 1500
```



`inet 192.168.2.199 mask:255.255.255.0 on broadcast 192.168.2.255`

`inet6 fe80::a8b3:fffe:db9a6b prefixlen 64 scopeid 0x20<link>`

`ether 08:27:9e:be:ed ed txqueuelen 1500 (Ethernet)`

`RX packets 2595 bytes 16325 (16.2 KIB)`

`RX errors 0 dropped 0 overruns 0 frame 0`

`TX packets 1093 bytes 7219 (7.1 KIB)`

`TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0`

`root@networking ~#`

```
图 6.27 - ifconfig bond0 的输出
```

你现在可以正常使用系统了，但 `bond0` 才是网络设备。

## 工作原理

现在我们已经有一个工作正常的 bond，让我们看看入站和出站流量。为此，我们需要安装 `iptables-ng` 命令：

```bash
dnf -y install iptables-ng
```

此工具允许你监控服务器上的以太网流量。在本示例中，我们将运行 `iptables-ng` 命令。这将启动程序，你将在下面的截图中看到：

![](img/110fa0d6324f0893fff03cee6394144d_232_0.png)

图 6.29 – iptraf 主菜单

从这里，我们将通过按下 `S` 键查看通用接口统计数据。这将显示每个接口的实时流量情况：

| 接口 | Total | IPv4 | IPv6 | Bad IP | Activity |
|---|---|---|---|---|---|
| bond0 | 63016 | 63016 | 0 | 0 | 1349.5 kbps |
| eth3 | 10938 | 10938 | 0 | 0 | 46328.71 kbps |
| eth0s | 44898 | 44898 | 0 | 0 | 6.08 kbps |

图 6.30 – 通用接口统计数据

你可以看到入出流量在两个物理接口之间是平衡的。这是因为 bond 是使用 `balance-alb` 模式构建的。为了产生这种流量，从客户端使用了简单的洪泛（flood）：

```bash
ping -f 192.168.200.179
```

## 注意

谨慎使用 `-f` 选项，它会使网络洪泛，在没有与团队协调的情况下，在生产网络上这样做通常是不可接受的。它可能会导致系统性能问题。压力网络有一种更好的方法，即使用一个能够生成接口支持的最大级别数据包的工具。

# iperf – 网络工具

我们将使用 `iperf`。它将生成接口可以支持的最大流量。要安装 `iperf`，请运行以下命令：

```bash
dnf install iperf
```

我们还需要打开一个 TCP 端口以便使用并重新加载。每个实例只能处理单个连接。我们将添加多个端口来启用服务器，每个端口使用不同的端口。通过以下命令完成：

```bash
firewall-cmd --permanent --add-port=8000-8010/tcp
firewall-cmd --reload
```

为了使用客户端-服务器模型，我们首先需要在 `networking` 上启动 `iperf` 服务器。在本示例中，我们将设置服务器监听 `8001` 端口。

```bash
root@networking ~# iperf -s -p 8001
```

我们将 `8002` 端口重复操作：

```bash
root@networking ~# iperf -s -p 8002
```

现在，有了两个服务器，我们可以运行客户端测试。测试通过以下命令进行：

```bash
root@client ~# iperf -c 192.168.2.199 -p 8001
```

运行几秒钟后，可能的输出如下：

```bash
root@client ~# iperf -c 192.168.2.199 -p 8001 -t 10
```

# 7

# Oracle Linux 8 – 打补丁并不意味着重启

我这辈子都在打补丁时重启系统，现在为什么要改变呢？

自从 1991 年 Linux 发布以来，每当内核需要补丁时，你就必须重启系统。当时，即使是主导企业 IT 的 IBM 主机在打补丁时也需要重启，因此其他所有系统在补丁后重启被认为是常的。这一过程在接下来的 20 年里似乎运行良好，但变革的种子在 2005 年种下了，当时马诸塞理工学院（MIT）的一学生提出了一个简单的问题：*如果可以在不重启系统的情况下打补丁呢？* 他的团队在 2009 年 Ksplice 发布时找到了答案，使得能够在系统运行时对 Linux 内核进行补丁。

在本章中，我们将介绍为什么你应该开始使用 Ksplice，以及它是如何提高你的系统安全性的。

本章包含以下配方：

- 在接入网络的情况下配置 Ksplice
- 在无网络访问的情况下使用 Ksplice
- 安装并启用已知漏洞禁用（Known Exploit deactivation）

## 在接入网络的情况下配置 Ksplice

在进入配方之前，让我们先了解为什么 Ksplice 会引起如此大的关注。

### 为什么 Ksplice 如此关注？

第一个问题是，*为什么这对 IT 重要，更重要的是，对于防御运行在服务器上的应用程序重要？* 在此之前，你首先需要理解黑客入侵系统的过程。

基本过程包括三个阶段：侦察、获取访问、然后维持访问。一旦系统被攻破，该过程就会网络上的其他系统上重复：

![](img/110fa0d6324f0893fff03cee6394144d_236_0.png)

图 7.1 – 安全生命周期

在第一阶段，**侦察**中，黑客使用各种方法扫描系统漏洞。通常，这种攻击阶段在黑客获取了可以访问服务器的低级支持账户后开始。一旦进入那里，查看内核版本并识别内核易受哪些漏洞的影响是一件而易的任务。Oracle 提供了一个免费站点（https://ksplice.oracle.com/inspector），让你能够轻松检查内核漏洞。此类检查的结果显示在*图 7.2* 中。

## Ksplice Inspector

Ksplice 通过应用补丁而无需重启来保护你的系统。要查看哪些补丁将应用于你的系统，请执行以下步骤：

- 1. 在你目标机器上打开终端。
- 2. 在终端中运行命令：

```bash
echo "uname -s -uname -m -uname -r -uname -p -uname -v"
```

- 3. 将命令的输出复制到此文本框并点击 Find Updates（查找更新）。

```
Linux/x86_64 4.15.0-2136.032-7.2.el8 Find Updates
```

你也可以通过从命令行终端运行来获取信息：

```bash
(uname -s -uname -m -uname -r -uname -p -uname -v)
curl https://api.ksplice.oracle.com/api/cve-list/ -H "Accept: text/data-binary #"
```



## Oracle Linux 高级支持客户

你有使用 `Oracle Ksplice` 的许可证吗？你可以通过登录 `Unbreakable Linux` 获取你的访问密钥，从今天开始无需重启即可更新内核！

## 立即尝试 Oracle Ksplice

### Oracle Linux 和 Red Hat Enterprise Linux 的 30 天试用

如果你使用 `Oracle Linux` 或 `Red Hat Enterprise Linux`，可以免费尝试 `Ksplice` 30 天。在试用期间，你将获得 `Oracle Ksplice` 的所有保护。

![](img/110fa0d6324f0893fff03cee6394144d_236_0.png)

## 注意

（注：原文结尾重复的 CVE 编号及无意义片段已根据要求剔除）

并不是所有组织都遵循完整的流程，而是为了节省时间而跳过某些步骤。虽然在短期内可以节省一些时间，但只要在两个补丁周期之间应用程序和/或其基础设施发生了更改，就可能导致一个非常糟糕、漫长的夜晚，或者更糟，是漫长的数日。

如你所见，适当的补丁需要大量时间，应用程序越复杂，每个补丁周期所需的人力和时间就越多。大部分大部分时间和精力的都是由于重启所需的。

当你避免了重启时，补丁过程将显著简化；如下图所示，只有两个步骤！

![](img/110fa0d6324f0893fff03cee6394144d_240_0.png)

图 7.4 – `Ksplice` 补丁过程

以下列表提供了这两个步骤的简要描述：

- **Ksplice 修复服务器**：使用 `ksplice` 应用内核和用户空间补丁。
- **测试**：测试应用程序

通过使用 `Ksplice`，你的团队可以节省大量时间，减少加班，并提高安全性。最棒的是，它易于设置和使用！

# 探索 Ksplice

`Ksplice` 配置非常简单。在对服务器进行 `Ksplice` 之前，你需要了解几个概念和要点：

- 如果你的服务器运行在 **Oracle Cloud Infrastructure (OCI)** 上，并使用 Oracle 的默认平台镜像，所有的 `Ksplice` 准备工作和对 `Ksplice` 仓库的访问已经完成，以支持在线 `Ksplice` 使用。系统还需要一条路由（通常带有 NAT 网关）到 `Ksplice` 端点。这在使用**虚拟云网络 (VCN)** 向导时会自动设置。
- 如果你在 OCL 上使用 `Autonomous Linux`，系统会自动完成 `Ksplice`。
- 有两个 `Ksplice` 客户端：旧版的 `Uptrack` 客户端和增强型（Enhanced client）。

使用 `Ksplice` 不需要连接互联网；你可以使用离线模式使用专门构建的 `Ksplice` `.rpm` 文件。这需要在本地 `YUM` 服务器上镜像 `ULN` `Ksplice` 仓库。这在第 5 章中已经介绍过。

增强客户端和 `Uptrack` 客户端允许你对内核进行 `Ksplice`，增强客户端还提供对用户空间库、`KVM` 虚拟机以及基于 Arm 的系统的 `Ksplice`，并为 `x86_64` 平台提供已知漏洞检测（Known Exploit Detection）。大多数新用户应该使用增强客户端。

旧的 `Uptrack` 客户端不具备增强客户端的优势，但它具备补丁某些非 `Oracle Linux` 系统的能力。

`Ksplice` 提供两种不同的模式：在线模式和离线模式。在线模式要求每个系统注册到 `Oracle ULN`，但它提供了 `Ksplice` Web 界面，用于高级自动化以及补丁 `Xen` 虚拟机的能力。然而，由于这需要每个系统不仅要向 `ULN` 注册，还需要访问互联网，许多系统管理员使用离线模式。

离线模式允许系统在没有互联网访问的情况下使用 `Ksplice`。这通常用于企业和政府环境，那里所有服务器无法访问互联网。在这种情况下，最常见的方法是设置 `ULN` 镜像，让该系统访问互联网，本地的 `Oracle Linux` 服务器将从该镜像拉取以使用 `Ksplice`：

![](img/110fa0d6324f0893fff03cee6394144d_241_0.png)

图 7.5 – 使用 `RPM` 的 `Ksplice` 离线模式

使用离线模式，只需要本地 `ULN` 镜像通过 `HTTPS` 协议访问 `Oracle ULN`。这可以通过基本的防火墙规则或更高级的代理服务器来实现。一旦 `ULN` 镜像注册并从 `ULN` 同步完成，防火墙后的服务器将通过 `HTTP/HTTPS` 从 `ULN` 镜像拉取它们的 `RPM`。离线模式有两个优势：用于互联网的带宽更少，且每个客户端都需要注册。当然，没有 API 在高级自动化方面存在限制。

无论使用哪种模式，客户端必须访问特定的 `Ksplice` 通道。下表描述了 `Oracle Linux` 中可 `Ksplice` 通道：

| 通道名称 (Channel Name) | 增强客户端 (Enhanced Client) | 通道标签 (Channel Label) |
| :--- | :--- | :--- |
| Ksplice for Oracle Linux 7 (x86_64) | | `ol7_x8664` |
| Ksplice for Oracle Linux 7 (aarch64) | | `ol7_aarch64` |
| Ksplice for Oracle Linux 8 (x86_64) | | `ol8_x8664` |
| Ksplice for Oracle Linux 8 (aarch64) | | `ol8_aarch64` |

*(注：根据 OCR 文本，源表格结构是碎片化的。我根据 OCR 后面页面提供的数据重建了逻辑映射。)*

| 通道名称 (Channel Name) | 增强客户端 (Enhanced Client) | 通道标签 (Channel Label) |
| :--- | :--- | :--- |
| Ksplice for Oracle Linux 7 (x86_64) | | `ol7_x8664` |
| Ksplice for Oracle Linux 7 (aarch64) | | `ol7_aarch64` |
| Ksplice for Oracle Linux 8 (x86_64) | | `ol8_x8664` |
| Ksplice for Oracle Linux 8 (aarch64) | | `ol8_aarch64` |
| Ksplice-Oracle Linux systems (x86_64) | | `ol7_x8664` |

| 通道名称 (Channel Name) | 增强客户端 (Enhanced Client) | 通道标签 (Channel Label) |
| :--- | :--- | :--- |
| Ksplice for Oracle Linux 7 (x86_64) | | `ol7_x8664` |
| Ksplice for Oracle Linux 7 (aarch64) | | `ol7_aarch64` |
| Ksplice for Oracle Linux 8 (x86_64) | | `ol8_x8664` |
| Ksplice for Oracle Linux 8 (aarch64) | | `ol8_aarch64` |

| 通道名称 (Channel Name) | 增强客户端 (Enhanced Client) | 通道标签 (Channel Label) |
| :--- | :--- | :--- |
| Ksplice for Oracle Linux 7 (x86_64) | | `ol7_x8664` |
| Ksplice for Oracle Linux 7 (aarch64) | | `ol7_aarch64` |
| Ksplice for Oracle Linux 8 (x86_64) | | `ol8_x8664` |
| Ksplice for Oracle Linux 8 (aarch64) | | `ol8_aarch64` |

| 通道名称 (Channel Name) | 增强客户端 (Enhanced Client) | 通道标签 (Channel Label) |
| :--- | :--- | :--- |
| Ksplice for Oracle Linux 7 (x86_64) | | `ol7_x8664` |
| Ksplice for Oracle Linux 7 (aarch64) | | `ol7_aarch64` |
| Ksplice for Oracle Linux 8 (x86_64) | | `ol8_x8664` |
| Ksplice for Oracle Linux 8 (aarch64) | | `ol8_aarch64` |

| 通道名称 (Channel Name) | 增强客户端 (Enhanced Client) | 通道标签 (Channel Label) |
| :--- | :--- | :--- |
| Ksplice for Oracle Linux 7 (x86_64) | | `ol7_x8664` |
| Ksplice for Oracle Linux 7 (aarch64) | | `ol7_aarch64` |
| Ksplice for Oracle Linux 8 (x86_64) | | `ol8_x8664` |
| Ksplice for Oracle Linux 8 (aarch64) | | `ol8_aarch64` |

| 通道名称 (Channel Name) | 增强客户端 (Enhanced Client) | 通道标签 (Channel Label) |
| :--- | :--- | :--- |
| Ksplice for Oracle Linux 7 (x86_64) | | `ol7_x8664` |
| Ksplice for Oracle Linux 7 (aarch64) | | `ol7_aarch64` |
| Ksplice for Oracle Linux 8 (x86_64) | | `ol8_x8664` |
| Ksplice for Oracle Linux 8 (aarch64) | | `ol8_aarch64` |

| 通道名称 (Channel Name) | 增强客户端 (Enhanced Client) | 通道标签 (Channel Label) |
| :--- | :--- | :--- |
| Ksplice for Oracle Linux 7 (aarch64) | | `ol7_aarch64` |
| Ksplice for Oracle Linux 8 (x86_64) | | `ol8_x8664` |
| Ksplice for Oracle Linux 8 (aarch64) | | `ol8_aarch64` |

| 名称 (Name) | 描述 (Description) |
| :--- | :--- |
| EPEL Modular Packages for Oracle Linux 8 (x86_64) | 用于创建测试和开发环境的 EPEL 软件包 - Oracle Linux 8 (x86_64) |
| EPEL Packages for creating test and development environments for Oracle Linux 8 (aarch64) | 用于创建测试和开发环境的 EPEL 包 - Oracle Linux 8 (aarch64) |
| Ksplice for Oracle Linux 8 (x86_64) | Oracle Linux 8 (x86_64) 的 Ksplice 客户端、更新和依赖项 |
| Oracle Linux 8 Latest (x86_64) | Oracle Linux 8 (x86_64) 发布的最新系统包，包括最新的错误包 (x86_64) |
| Oracle Linux 8 BaseOS Latest (x86_64) | 为 Oracle Linux 8 (x86_64) 发布的基础操作系统包 |
| Unbreakable Enterprise Kernel Release for Oracle Linux 8 (aarch6_64) | 为 Oracle Linux 8 发布的 Unbreakable Enterprise Kernel 包 - Oracle Linux 8 (aarch6_64) |

图 7 – 所需通道

现在你已经理解了为什么需要 `Ksplice` 以及它是如何工作的，让我们开始准备。

## 准备工作

要做到这一点，你需要一个运行 `Oracle Linux 8` 的系统，并带有用户空间库。

## 如何操作...

使用 `Ksplice` 时，确保每个系统与操作系统版本匹配，并启动 Oracle 服务。系统外观如下所示：

![](img/110fa0d6324f0893fff03cee6394144d_244_0.png)

如果你使用代理服务器，需要向代理导出一些环境变量：

```bash
```



`sudo http_proxy=http://proxy_server_URL:http_port`

`sudo https_proxy=http://proxy_server_URL:https_port`

`sudo export http_proxy https_proxy`

接下来，使用 `dnf` 安装 Ksplice。这两个软件包是：

```
dnf install -y ksplice uptrack
```

安装完成后，请验证系统是否在 ULN 中可见，并检查 `/etc/uptrack/uptrack.conf` 中是否填充了访问密钥。

访问密钥应该位于 `[Auth]` 部分，看起来如下所示：

完成完成后，执行一次标准的 `dnf update` 并重启系统。执行此 `dnf update` 是为了确保加载 Ksplice 感知的用户库；它仅在第一次使用 Ksplice 时需要。

一旦服务器重启，即可使用 Ksplice 对用户库和内核进行补丁修复。

要查看内核中有可用的更新，你可以运行 Ksplice 内核升级命令，并传递 `-n` 表示不执行操作：

```
ksplice -n kernel upgrade
```

此命令的输出如后续截图所示：

```
root@arm2 ~# ksplice kernel upgrade

Effective kernel version is 5.4.17-2136.306.1.3.el8uek

The following steps will be taken:

Install [juh90lc4c] CVE-2021-4034: Privilege escalation in pkexec.

root@arm2 ~#

root@arm2 ~#

root@arm2 ~#
```

> 图 7 - Ksplice 可用更新

在此系统中，只有一个可用更新，用于修补 CVE-2021-4034。要对系统进行 splice（修复），运行相同的命令，将 `-n` 替换为 `-y` 以确认应用到内核路径上：

```
root@arm2 ~# ksplice -y kernel upgrade

The following steps will be taken:

Install [juh90lc4c] CVE-2021-4034: Privilege escalation in pkexec.

Installing [juh90lc4c] CVE-2021-4034: Privilege escalation in pkexec.

Your kernel is fully up to date.

Effective kernel version is 5.4.17-2136.306.1.3.el8uek

root@arm2 ~#
```

> 图 7.8 – Ksplice 更新内核

在这里，你可以看到 CVE 补丁已经生效，而无需重启！

已修复补丁的内核被称为“有效内核”（effective kernel）。当你在 Ksplice 中使用 `ksplice kernel -r` 命令时，它会显示有效内核版本，该版本根据已已的补丁指示了内核当前的安全状态。此版本与最初启动的内核不同，旨在反映内核针对任何潜在安全威胁或重大问题的当前状况。

你现在可以使用以下 Ksplice 内核命令来验证你的有效内核：

```
kspl kernel show
```

注意，运行中的内核版本与已安装的内核版本将不匹配！这是因为当 Ksplice 对内核进行操作时，它将运行内核的 RAM 与新代码进行 splice。它修复了内核（以及选定的用户空间库），但结果是 *uname* 的结果不再与有效内核匹配：

```
Effective kernel version 5.4.17-2136.306.1.3.el8uek

[root@vm]# uname -a

Linux 5.4.17-2136.302.7.2.1.el8uek.aarch64 #2 SMP Tue Jan 18 12:11:39 PST 2022 aarch64 aarch64 aarch64 GNU/Linux

[root@vm]# #
```

图 7.9 - Ksplice uname

在这里，已安装的内核以相同的方式被修补，替换了 5.4.17-2136.302.7.2.1.el8aarch64，但经过 Kssplice 后的有效内核是版本为 5.4.17-2136.306.1.3.el8uek 的新内核。这是 Ksplice 的正常行为。

可以在不重启内核的情况下对用户空间库进行修补。注意，如果没有安装 Ksplice 用户空间库，在第一次运行时，系统将提示你将用户库升级到 Ksplice 兼容的版本：

```
[root@vm]# yum update -a

Updating de-install packages for new processes

Checking for updates for Oracle Linux (aarch64) 5.3 MB / 1.0 MB 00:00

Dependencies resolved.

Package Architecture Size

Upgrading:

glibc aarch64 2.28.164.5.ksplice2.el8_3 el864_userspace_ksplice 3.6 M

glibc-common aarch64 2.28.164.5.ksplice2.el8_3 el864_userspace_ksplice 128 K

glibc-dev aarch64 2.28.164.5.ksplice2.el8_3 el864_userspace_ksplice 1.5 M

glibc-libinfo aarch64 2.28.164.5.ksplice2.el8_3 el864_userspace_ksplice 571 K

glibc-langpack aarch64 2.28.164.5.ksplice2.el8_3 el864_userspace_ksplice 630 K

kernel aarch64 5.11.0-b6.ksplice1.el8_5 el864_userspace_ksplice 1.3 M

ksplice-helper aarch64 1.0.55-el8 el864_userspace_ksplice 23 K

Transaction plan:

Total install 0 Upgrade 7 Packages 9.2 M

Is this ok [y/N]
```

图 7.10 - 首次安装 Ksplice 用户库

注意，你可以使用 `ksplash show --available` 命令检查 Ksplice 可用的用户空间包，但如果你没有安装 Ksplice 感知包，将得到此错误：No active user-space Ksplice targets（没有活跃的用户空间 Ksplice 目标）。你安装了 Ksplice 感知库并重启了吗？你还可以检查用户空间目标是否正在运行并可以被修补。可以通过以下命令实现：

示例输出所示：

```
root@arm # ksplice --list-targets

100 ######################################

User-space targets:

glib2-libfuse-2.20.164.0.5.ksplice2.e18_5.3.aarch64:

  - crowd (37867)

  - kplice (37251)

glib2-libhot-2.20.164.0.5.ksplice2.e18_5.3.aarch64:

  - crowd (37867)

  - kplice (37251)

glib2-liblz2-2.20.164.0.5.ksplice2.e18_5.3.aarch64:

  - crowd (37867)

  - kplice (37251)

glib2-libsystemd-2.20.164.0.5.ksplice2.e18_5.3.aarch64:

  - crowd (37867)

  - kplice (37251)

glib2-libzstdrt-2.20.164.0.5.ksplice2.e18_5.3.aarch64:

  - crowd (37867)

  - kplice (37241)

opens3-libssl-1.1.1k.ksplice.e19.5.aarch64:

glib2-libfuse-2.20.164.0.5.ksplice2.e18_5.3.aarch64:

  - crowd (37867)

  - kplice (37251)

glib2-libhot-2.20.164.0.5.ksplice2.e18_5.3.aarch64:

  - crowd (37867)

  - kplice (37251)

glib2-liblz2-2.20.164.0.5.ksplice2.e18_5.3.aarch64:
```



- crowd (37867)
- kplice (37251)

`glib2-libsystemd-2.20.164.0.5.ksplice2.e18_5.3.aarch64`:
- crowd (37867)
- kplice (37251)

`glib2-libzstdrt-2.20.164.0.5.ksplice2.e18_5.3.aarch64`:
- crowd (37867)
- kplice (37241)

`opens3-libssl-1.1.1k.ksplice.e19.5.aarch64`:
... (省略重复内容)

### 7.11 - Ksplice 目标

使用 `ksplice kernel` 命令可以查看已安装的补丁。

```bash
[root@server ~]# apt remove kernel --all

将执行以下步骤：

移除 [a08wafvp] CVE-2022-1016: netfilter 子系统中的信息泄露。

移除 [ab6ve5] CVE-2020-36516: TCP/IP 协议中的多个漏洞。

移除 [d9kwegi] CVE-2022-26966: CoreChip SR8970 USB 10/100 以太网适配器信息泄露。

移除 [ovcpql] CVE-2022-24488: Linux USB 元数据中的权限提升。

移除 [ivq9qcm] CVE-2021-22660: 双重释放导致 Packet 协议子系统的权限提升。

移除 [gmams02] CVE-2022-24488: 使用 freeflow 时 netfilter 中的信息泄露。

移除 [1ra84j9] CVE-2021-3998: 进程间通信协议中的权限提升。

移除 [1a6h0b] CVE-2021-4002: 内存泄漏导致 hugetlb 中的信息泄露。

移除 [izvki] CVE-2022-27726: 以太网支持支持权限提升。

移除 [lra19v4] CVE-2022-0847: 管道缓冲区中的权限提升。

移除 [m6vuv] CVE-2022-27728: 使用 flow overflow 时 netfilter 中的信息泄露。

移除 [mmz2nv0d] CVE-2021-34061: 使用后释放导致经典蓝牙（Bluetooth Classic）权限提升。

移除 [ov6661] CVE-2021-34932: 控制组（Control Groups）子系统的权限提升。

移除 [oozmwm] CVE-2021-30321: OverlayFS 中的竞态条件。

移除 [h2ycylt1] CVE-2022-0492: 以太网驱动程序中的权限提升。

移除 [id3hcbai] CVE-2021-34932: 网络流量处理任务中的信息泄露。

移除 [ienm9qcmn] CVE-2021-4034: phexec 中的权限提升。

有效内核版本为 5.4.11-2136.302.7.2.1.ebluk

[root@server ~]#
```

图 7.14 – Ksplice remove

继续吗 [y/N]?
移除 [a08wafvp] CVE-2022-1016: netfilter 子系统中的信息泄露。
移除 [ab6ve5] CVE-2020-36516: TCP/IP 协议中的多个漏洞。
移除 [d9kwegi] CVE-2022-26966: CoreChip SR8970 USB 10/100 以太网适配器信息泄露。
移除 [ovcpql] CVE-2022-24488: Linux USB 元数据中的权限提升。
移除 [ivq9qcm] CVE-2021-22660: 双重释放导致 Packet 协议子系统的权限提升。
移除 [gmams02] CVE-2022-24488: 使用 freeflow 时 netfilter 中的信息泄露。
移除 [1ra84j9] CVE-2021-3998: 进程间通信协议中的权限提升。
移除 [1a6h0b] CVE-2021-4002: 内存泄漏导致 hugetlb 中的信息泄露。
移除 [izvki] CVE-2022-27726: 以太网支持支持权限提升。
移除 [lra19v4] CVE-2022-0847: 管道缓冲区中的权限提升。
移除 [m6vuv] CVE-2022-27728: 使用 flow overflow 时 netfilter 中的信息泄露。
移除 [mmz2nv0d] CVE-2021-34061: 使用后释放导致经典蓝牙（Bluetooth Classic）权限提升。
移除 [ov6661] CVE-2021-34932: 控制组（Control Groups）子系统的权限提升。
移除 [oozmwm] CVE-2021-30321: OverlayFS 中的竞态条件。
移除 [h2ycylt1] CVE-2022-0492: 以太网驱动程序中的权限提升。
移除 [id3hcbai] CVE-2021-34932: 网络流量处理任务中的信息泄露。
移除 [ienm9qcmn] CVE-2021-4034: phexec 中的权限提升。

Ksplice 还允许自动更新。可以通过简单的创建或删除文件来启用或禁用它们。如果 `/etc/utrack/disable` 文件存在，则 Ksplice 在重启时不会自动更新。如果不存在该文件，Ksplice 将检查新的 KID 并应用它们。你也可以通过更新配置文件来修改此操作，这将在后面的章节中介绍。

# 工作原理...

当你通过网络访问使用 Ksplice 时，客户端连接到 Oracle ULN 系统并下载所需的更新。

# 在无网络访问的情况下使用 Ksplice

并非所有系统都可以访问网络。此时可以针对本地补丁仓库使用 Ksplice。

## 准备工作

要做到这一点，你需要运行 Oracle Linux 8 的测试系统，并访问网络上的本地 仓库。

## 如何操作...

安装客户端之前，确保你的服务器使用的是本地镜像的 RPM 仓库。安装 Ksplice 时，必须决定使用在线还是离线客户端。作为提醒，在线客户端需要注册 ULN，而离线客户端将使用本地 RPM 仓库。

安装在线客户端，运行以下命令：

```bash
dnf install -y ksplice utrack
```

安装离线客户端，运行以下命令：

```bash
dnf install -y ksplice ksplice-offline utrack-offline
```

此命令的输出如截图所示：

```
Running transaction check

Transaction check succeeded.

Running transaction test

Transaction test succeeded.

Running transaction
```
Preparing : uptrack-offline-1.2.7-2.el8.noarch
Download metadata for uptrack-offline-1.2.7-2.el8.noarch
...
```

这是一段触发器（tripwire）代码，当检测到特定事件时会触发。通常情况下，只监控允许审计员获得特权访问的事件。该包同时适用于 x86 和 ARM 系统。

要启用此功能，必须首先使用以下命令安装该包：

```
dnf install -y ksplice-known-exploit-detection
```

无论是在 ARM 还是 x64 服务器上安装，其安装过程几乎完全相同，细微区别在于每个系统中已安装的软件。这让我想起一点：无论是 ARM 还是 x64，管理任务都是相同的。

## 注意

安装 KED 时，系统还会安装 postfix，作为通知系统的一部分用于发送邮件。

在基于 ARM 的系统上安装的输出显示如下所示：



```
[root@arm3 ~]# -y install ksplice-known-exploit-detection
Last metdata expire check: 1:23:34 ago on Sun 24 Apr 2022 02:00:29 PM GMT.
Dependencies required:
Package                         Architecture  Version             Repository            Size
Installing: ksplice-known-exploit-detection  aarch64        1.0.55-1.el8       ol8_kspline          16 k
Installing dependencies:
                                aarch64        2:3.5.8-2.el8       ol8_baseos_latest     1.5 M
Transaction Summary
Install 2 Packages
Total download size: 1.5 M
Installed size: 6.2 M
(1/2): postfix-3.5.8-2.el8.aarch64.rpm                               11 MB/s | 1.5 MB          00:00
(2/2): ksplice-known-exploit-detection-1.0.55-1.el8.aarch64.rpm  30 KB/s | 30 KB           00:00
Total
Running transaction check.
Transaction check recommended.
Running transaction test.
Transaction test passed.
Transaction:                                                              2.8 MB/s | 1.5 MB          00:00
(1/2) postfix-3.5.8-2.el8.aarch64                                            1/2
Installing: postfix-3.5.8-2.el8.aarch64                                     1/2
Running: ksplice-known-exploit-detection-1.0.55-1.el8.aarch64               1/2
Installing: ksplice-known-exploit-detection-1.0.55-1.el8.aarch64               2/2
Running: ksplice-known-exploit-detection-1.0.55-1.el8.aarch64               2/2
Verifying: ksplice-known-exploit-detection-1.0.55-1.el8.aarch64               2/2
Verifying: postfix-3.5.8-2.el8.aarch64                                     2/2
Installed:\ksplice-known-exploit-detection-1.0.55-1.el8.aarch64
Complete
[root@arm3 ~]#
```

![](img/110fa0d6324f0893fff03cee6394144d_253_0.png)

在基于 x86 的系统上安装的输出显示如下所示：

```
[root@splice2 ~ # apt install -y ksplice-known-exploit-detection
This system is receiving updates from Database Kernel Linux and Spawalk.
Dependencies checked; 03:01:04 on 27 Apr 2022 08:24:43 AM.

Package                   Version               Repository



           ----------
----------:
:-exploit-detection  x86_64   1.1..5-1..11  o18_x86_64_kiceice
1



:
mp-6x8666111..1111111188__66____55


infoxx6666111.1111.111111116_11__1 71 k
liblockfile             x86_64   1.14-1.       o18_x86_64_appstream32 k

Summary:
 4 packages installed Total size: 177 k
0 used after this: 0
0 packages upgraded: 0
0 failed to install: 
(1/4) kplice-known-exploit-detection-1.05.1-50.11.x86_64.deb 179 KB / 32 KB 00:00
(2/4) smp-1.2-15.118 95 KB / 16 KB 00:00
(3/4) libinfo-1.05.1-50.11 276 KB / 71 KB 00:00
(4/4) liblockfile-1.14-1.18 95 KB / 32 KB 00:00

Total:
 647 KB / 177 KB 00:00

Running transaction check.
Transaction check succeeded.
Test passed.

Preparing
Setting up archive:
- smp-1.2-15.118.x86_64 1/4
- libinfo-1.05.1-50.11.x86_64 2/4
- liblockfile-1.14-1.18.x86_64 3/4
- kplice-known-exploit-detection-1.05.1-50.11.x86_64 4/4

Installing
Unpacking scripts:
- smp-1.2-15.118.x86_64 1/4
- libinfo-1.05.1-50.11.x86_64 2/4
- liblockfile-1.14-1.18.x86_64 3/4
- kplice-known-exploit-detection-1.05.1-50.11.x86_64 4/4

Setting up archive:
- smp-1.2-15.118.x86_64 1/4
- libinfo-1.05.1-50.11.x86_64 2/4
- liblockfile-1.14-1.18.x86_64 3/4
- kplice-known-exploit-detection-1.05.1-50.11.x86_64 4/4

Verifying archive:
- smp-1.2-15.118.x86_64 1/4
- libinfo-1.05.1-50.11.x86_64 2/4
- liblockfile-1.14-1.18.x86_64 3/4
- kplice-known-exploit-detection-1.05.1-50.11.x86_64 4/4

Installing
- smp-1.2-15.118.x86_64 1/4
- kplice-known-exploit-detection-1.05.1-50.11.x86_64 2/4
- liblockfile-1.14-1.18.x86_64 3/4
Complete
[root@splice2 ~#]
```

图 7.17 – x64 上的 KED 安装

一旦安装了 KED，功能即可被启用。这通过向 `/etc/uptrack/uptrack.conf` 中添加以下行来实现：

`[Known-Exploit-Detection]`

`enabled = yes`

接下来，您需要对内核进行 Ksplice 更新以在运行的内核中启用该功能：

```
ksplice --yes kernel upgrade
```

该命令的输出显示如下所示：

```
[root@arm3 ~#] ksplice kernel upgrade
Nothing to do.
Your kernel is fully up to date.
Effective kernel version 5.14.0-2136.306.1.3.el8
[root@arm3 ~#]
```

图 7.18 – 在运行的内核中启用 KED



作为说明，如果有可 Ksplice 补丁，您将收到内核已是新的通知，如上一个截图所示。如果系统需要 Ksplice 补丁，Ksplice 将此时对内核进行修复。

要验证 KED 是否已启用，执行 `cat /proc/sys/known_exploit_detection` 并寻找输出为 `1`。如果文件缺失或为零，则 KED 未启用，因此不会监控您的系统：

```
[root@8splice2 ~] cat /proc/sys/known_exploit_detection
1
[root@8splice2 ~]
```

图 7.19 – 检查 KED 是否启用

KED 的通知由 `/etc/log-known-exploit.conf` 配置文件控制。示例配置文件显示如下所示：

```
[root@8splice2 ~] /etc/log-known-exploit.conf
[syslog]
enabled: 1
```

```
[email]
enabled: 1
recipients: erik@talesfromthedacenter.com
```

```
[actions]
# 您可以使用此部分为特定的触发器设置特定的操作。

# 目前有效的操作有：
# report
# ignore
```

```
# 忽略特定的触发器在极少数合法用户/应用程序实际上导致误报的情况下可能是很有用的。
# 在这种情况下，您可以例如：
```

```
[actions]
CVE-2017-1234: ignore
```

```
# 您可以使用 'default' 条目指定默认操作。因此，如果您想忽略所有内容并仅启用一个触发器，
# 可以这样做：
```

```
[actions]

default: ignore

CVE-2017-1234: report

```

```
[root@ol8splice2 ~]
```

图 7.20 – KED 通知

## DevOps 自动化工具 – Terraform, Ansible, Packer 及更多

如果一个操作系统不能为开发者提供便利，那它又有什么用呢？毕竟，一个易于开发的操作系统会比一个难以开发的操作系统拥有得更强大的生态系统。你会惊喜地发现，Oracle Linux 与开发者的配合非常完美，本章将介绍一些常用工具，它们将在你开始下一个项目时让你的工作变得更加轻松。

Oracle Linux 上有无数运行良好的开发工具，而我们在本章中关注的都与自动化有关。我们将讨论自动化云基础设施、自动化操作系统构建周期、自动化系统管理员任务，以及为了开发目的而自动启动虚拟机。

在本章中，我们将涵盖以下食谱：

- 手动执行一次 – 使用 Terraform 重复执行
- 为 Ansible 创建可移植的角色（roles）
- 使用 Ansible Vault 管理密钥
- 使用 Vagrant 搭建完美的实验环境
- 使用 Packer 修改源镜像
- 打包它，装好它，让我开始，呃，嗯……构建

## 技术要求

本章中涵盖了许多技术。让我们准备好机器，以便方便你跟随食谱操作：

### Ansible

对于 Oracle Linux 8，我们可以利用 Oracle Linux Automation Manager 存储库安装 Ansible，所以先安装存储库，然后安装 Ansible：

```
$ sudo dnf install -y oracleinux-automation-manager-release-el8

$ sudo dnf install -y ansible
```

### Packer, Vagrant 和 Terraform

`Packer` 是一个用于自动化创建机器镜像的工具，`Vagrant` 用于管理虚拟机的生命周期，而 `Terraform` 是一个基础设施即代码（IaC）工具。`Packer`、`Vagrant` 和 `Terraform` 都是 HashiCorp 的产品，它们在 Oracle Linux 上运行良好。

我们将直接从 HashiCorp 安装 `Packer`、`Vagrant` 和 `Terraform`：

```
$ sudo dnf install -y dnf-plugins-core

$ sudo dnf config-manager --add-repo https://rpm.releases.hashicorp.com/RHEL/hashicorp.repo

$ sudo dnf install -y packer vagrant terraform
```

完成后，让我们安装 Oracle VM VirtualBox，因为我们将配合 `Packer` 使用 VirtualBox：

```bash
$ sudo dnf install -y oraclelinux-developer-release-el8

$ sudo dnf install -y VirtualBox-7.0
```

最后，通过 `Terraform`，我们还想要创建一个 Oracle 云基础设施 (OCI) 账户。如果你愿意，可以选择不同的云服务，但如果你想直接遵循本教程，请使用 OCI。

## 注意事项

务必记住你的云账户名称（Cloud Account Name），因为这是访问 OCI 账户所需的详情。

## 下载源代码

本章食谱的源代码可以在此处找到：https://github.com/PackPublishing/Oracle-Linux-Cookbook/tree/main/ch8。

## 手动执行一次 – 使用 Terraform 重复执行

`Terraform` 是一种基础设施即代码 (IaC) 工具，让你安全高效地构建、更改和版本化基础设施。本食谱将提供一个使用 `Terraform` 自动化繁琐任务的良好技术概述。我说的繁琐是指什么？它是指任何手动执行的操作。我们希望消除手动步骤并尽可能实现自动化。具体到 `Terraform` 而言，这意味着我们不再需要点击数百个不同的菜单设置。相反，我们将基础设施定义为代码。这将带来更快速、更一致的部署。此外，由于所有内容都可以通过代码进行编辑，对基础设施进行更改也变得更容易。

### 入门

此食谱需要以下内容：

- Oracle Linux
- Terraform

参考本章开头的 *Technical requirements* 部分（如果你需要帮助安装 Terraform）。

### 如何操作...

当你准备自动化某些内容时，对底层需要执行的操作有一个良好的理解是一个好主意。你知道这意味着吗？是的，在尝试自动化之前，你必须手动执行所有步骤。

### 首先，手动执行一次...

此食谱的目标是使用 `Terraform` 在云端部署单个虚拟机。这是一项简单任务，但在使用代码完成之前，最好先手动执行。因此，让我们使用 OCI GUI 部署虚拟机：

1. 登录 Oracle Cloud 控制台 (https://cloud.oracle.com/)。![img/110fa0d6324f893fff03cee639414d_260_0]
2. 点击左上角的汉堡菜单![img/110fa0d6324f893fff03cee639414d_260_1]。然后点击 Compute | Instances：
   - Overview
   - Instances
   - Dedicated Hosts
   - Instance Configurations
   - Network Pools
   - Clusters
3. 验证你处于正确的 Compartment（隔间），最后点击 Create：![img/110fa0d6324f893fff03cee639414d_261_0]
4. 为了简便起见，当需要点击多个项目时，| 符号表示点击的顺序。我们将使用默认的 Oracle Linux 镜像，如果你想更改它，可以去 Image 并点击 Edit![img/110fa0d6324f893fff03cee639414d_262_0]。

## 注意

只要你坚持“始终免费（Always Free）”资源，就没有费用；但是，启动卷的每月费用为 $2.00。这是因为 OCI 提供了 20 GB 的免费块存储。此时的最新版本是 Oracle Linux 8。

4. 在 SSH Keys 下生成密钥对，然后点击 Save Private Key 和 Save Public Key。

## 提示

选择一个容易记忆的地方，因为你以后 SSH 进入虚拟机时需要它。

5. 最后，点击 Create。

## 注意

在等待镜像构建时，尽管去喝咖啡吧。

现在，让我们使用 SSH 连接到实例：

1. 在 Instance 信息选项卡上，点击 Public IP 条目（`i` 代表文件引用）。
2. 打开终端应用程序并使用 `ssh` 命令。我们将使用 OCI 中 Oracle Linux 实例的默认用户名 `opc`，以及上一步使用的私钥。最后，输入上一步获取的 Public IP 地址。你的命令看起来应该是这样的：

```
[vagrant@localhost-0-book]$ ssh -i ssh-key-2023-08-03.key opc@129.08.70
```



The authenticity of host '129.08.70' can't be established.

ECDSA key fingerprint is SHA256:iZZ/iBmMZpogcon7aMn3WAc62F5lQMFM.

Are you sure you want to continue connecting (yes/no/[fingerprint])?

This will add the host to the list of known hosts.

`~/.ssh/known_hosts`

WARNING: UNPROTECTED PRIVATE KEY FILE!

Permissions 0644 for `ssh-key-2023-08-03.key` are too open.

It is required that your key files are NOT accessible by others.

This private key will be ignored.

Load key "ssh-key-2023-08-03.key": bad permissions

`opc@129.08.70.82`: password:

```
![img/110fa0d6324f893fff03cee639414d_263_0]

3. 呃！你注意到那个警告以及最后那条消息了吗？因为权限错误而被拒绝访问。让我们使用 `chmod` 赋予访问密钥的权限。

```

```
[vagrant@localhost-0-book]$ chmod 600 ssh-key-2023-08-03.key

[vagrant@localhost-0-book]$ ssh -i ssh-key-2023-08-03.key opc@129.08.70.82

Activate the web console with: systemctl enable --now cockpit.socket

[opc@instance-20230802-2250~]$ 
```

```
![img/110fa0d6324f893fff03cee639414d_263_1]

我们已经通过 SSH 连接到了机器。

现在我意识到这其实不了，但想象一下你必须做一百次这样的操作呢？为什么不用 Terraform 自动化这个过程呢？
```

## 现在是时候用 Terraform 重复执行了

这一次，我们将完成与之前描述完全相同的事情——即，我们将创建另一个虚拟机。然而，这一次我们将

使用 Terraform 定义我们的 IaC：

- 1. 首先，让我们使用你喜爱的代码编辑器在项目目录根目录下创建三个新文件（我将其命名为 **terraform**），并命名如下：

  A. `main.tf`
  B. `variables.tf`
  C. `terraform.tfvars`

- 2. 接下来，前往 Terraform Registry (`https://registry.terraform.io/`) 寻找 **Oracle Cloud Infrastructure (OCI)** 的提供程序（provider）。

- 3. 在 Terraform Registry 上，，搜索 **oci** 或 **oracle cloud infrastructure**，并选择 **oracle/oci**。

### 注意

或者，你可以点击 **Browse Providers**（浏览提供程序），然后点击 **Oracle Cloud Infrastructure** 按钮。

- 4. 点击 **USE PROVIDER**（使用提供程序），并将显示的代码复制并粘贴到你的 `main.tf` 文件中：

```terraform
terraform {
  required_providers {
    oci = {
      source = "oracle/oci"
      version = "5.7.0"
    }
  }
}
provider "oci" {
  # Configuration options
}
```

图 8.8 – Terraform OCI 提供程序

- 5. 注意 `provider "oci"` 下方的 **# Configuration options** 注释。这告诉我们，可能需要提供某些配置才能使用该提供程序。

让我们来看看如何操作：

- A. 点击 **Documentation**（文档）选项卡（它就在 **USE PROVIDER** 旁边），然后找到 **How to configure the provider**（如何配置提供程序）的链接。

- B. 你发现 OCI Terraform 提供程序支持四种认证方法：

  * API Key Authentication（默认）
  * Instance Principal Authorization（实例主体授权）
  * Resource Principal Authentication（资源主体认证）
  * Security Token Authentication（安全令牌认证）

- C. 对于本教程，我将使用默认的认证方法；即 API Key 认证。这种方法的限制最少，但根据你的用例，你可以选择满足你的一种。

# 重要说明

查找认证详情没有捷径；但是，为了获得有用的指导，你可能希望参考与本教程相关的 GitHub 仓库中的 `oci-provider-conf.md` 文件。如果你需要更多详细信息，我建议阅读之前提到的“How to configure the provider”部分中的文档。

- D. 如果你决定使用 API Key 认证作为你的认证方法，请在 `main.tf` 文件的 `provider "oci"` 中添加以下配置选项：

```hcl
provider oci {
  # API Key Authentication
  tenancy_ocid = var.tenancy_ocid
  user_oid = var.user_oid
  fingerprint = var.fingerprint
  private_key_path = var.private_key_path
  region = var.region
}
```

![](img/110fa0d6324f0893fff03cee6394144d_265_0.png)

为了保持整洁，我们将对这些值引用变量。我将在本教程稍晚部分提供更多关于如何定义/声明变量的细节。

### 注意

为了说明我们正在向文件中添加内容，我使用了三组三个点。这表示对我们在之前步骤中所操作内容的延续。

这里是一个示例：

...
...
...

6. 现在我们已经设置好了提供程序，除非添加资源（resource），否则它将不起什么作用。在这种情况下，我们想要添加一个 `oci_core_instance`。

你还记得在手动过程中我们生成 SSH 密钥对吗？现在，我们需要找到一种使用代码动态实现此的方法。以下指令说明了我们如何使用 Terraform 实现此。我们将创建一个 `tls_private_key` 资源，并使用 `oci_core_instance` 资源的元数据将其引用为我们的 `ssh_authorized_keys`。

让我们从 SSH 密钥对开始，它是通过 `tls_private_key` 资源创建的。该资源的详情可以在 Terraform Registry 上的 `hashicorp/tls` provider 下找到。继续编辑 `main.tf` 文件并添加以下内容：

```hcl
# Generate SSH Key Pair for access
resource "tls_private_key" "ssh" {
  algorithm = "RSA"
}
resource "local_sensitive_file" "ssh" {
  filename   = "${path.module}/instances/${var.instance_name}/id_rsa"
  permission = "0600"
  content    = tls_private_key.ssh.private_key
}
```

图 8.10 - 使用 Terraform 定义密钥对

你需要定义一个有效的可用性域（availability domain）。实现此点的一种方法是使用 Terraform 查询可用性域列表并引用其中的项，因此让我们在 `main.tf` 中添加以下代码：

```hcl
# Get a list of Availability Domains
data "oci_identity_availability_domains" "ads" {
  compartment_id = var.compartment_id
}
```



图 8.11 - 获取可用性域列表

最后，我们将为 `oci_core_instance` 添加一个资源。如果你查看来自 `oracle/oci` 提供的程序的 `oci_core_instance` 资源，你将看到一长串参数，这些参数可以用于定义 `oci_core_instance` 资源；然而，此列表并非所有内容都是必需的。许多参数是可选的。对于本教程，我们将使用该资源所需的最小配置——它看起来应该像这样：

```hcl
# Create an OCI instance

resource "oci_core_instance" "instance" {

  compartment_id = var.compartment_id

  availability_domain = data.oci_identity_availability_domains.ads.domains[0].name

  display_name = var.instance_name

  shape = "VM.Standard.E2.1.Flex"

  source_details {

    image_id = var.os_image_id

  }

  vnic_config {

    subnet_id = var.subnet_id

    ssh_authorized_keys = [

      tls_private_key.ssh.public_key

    ]

  }

}
```

图 8.12 - OCI 实例定义

9. 如果你查看了 `oracle/oci` 提供的程序的 `oci_core_instance` 资源，当你完成该资源后，整个 `main.tf` 文件看起来如下所示：

```terraform
terraform {

  required_providers {

    oci = {

      source = "oracle/oci"

      version = "5.7.0"

    }

  }

}

provider "oci" {

  # Configuration options

  tenancy_ocid = var.tenancy_ocid

  user_oid = var.user_oid

  fingerprint = var.fingerprint

  private_key_path = var.private_key_path

  region = var.region

}

# Generate SSH Key Pair for access

resource "tls_private_key" "ssh" {

  algorithm = "RSA"

}

resource "local_sensitive_file" "ssh" {

  filename   = "${path.module}/instances/${var.instance_name}/id_rsa"

  permission = "0600"

  content    = tls_private_key.ssh.private_key

}

# Get a list of Availability Domains

data "oci_identity_availability_domains" "ads" {

  compartment_id = var.compartment_id

}

# Create an OCI instance

resource "oci_core_instance" "instance" {

  compartment_id = var.compartment_id

  availability_domain = data.oci_identity_availability_domains.ads.domains[0].name

  display_name = var.instance_name

  shape = "VM.Standard.E2.1.Flex"

  source_details {

    image_id = var.os_image_id

  }

  vnic_config {

    subnet_id = var.subnet_id

    ssh_authorized_keys = [

      tls_private_key.ssh.public_key

    ]

  }

}
```

图 8.13 - main.tf 的内容

10. 现在我们需要声明在 `main.tf` 中引用的所有变量。为了保持组织，我们将它们放在 `variables.tf` 文件中。每个变量至少包含一个类型；然而，我们还会添加描述来解释变量的作用。

将以下内容输入你的 `variables.tf` 文件：

```terraform
variable "instance_name" {

  description = "友好名称。不需要唯一，可以更改。"

  type        = string

  default     = "My first IaC instance"

}

variable "region" {

  description = "OCI区域"

  type        = string

}

variable "tenancy_oid" {

  description = "你的租户 OID"

  type        = string

}

variable "compartment_oid" {

  description = "你的通箱的 OID"

  type        = string

}

variable "user_oid" {

  description = "调用 API 的用户 OID"

  type        = string

}

variable "subnet_id" {

  description = "在其中创建 VNIC 的子网 OID"

  type        = string

}

variable "os_image_id" {

  description = "操作系统镜像 OID。"

  type        = string

  default     = "ocid1.image.oc1.iad.aaaaaaa3xxkkaj60wv1qpfsbn7zhcz5bovin3dpst7ymlphnzrjmb4ca"

}

variable "private_key_path" {

  description = "私钥文件路径"

  type        = string

}

variable "fingerprint" {

  description = "使用的密钥对的指纹"

  type        = string

}
```

变量 `variables.tf` 中的变量声明

11. 最后，我们希望为变量赋值。对于赋值，你可以使用 `terraform.tfvars` 文件。它看起来应该像这样：

```h
instance_name = "instancel"

region = "us-ashburn-1"

tenancy_oid = "ocid.tenancy.ocid.aaaaaaaaaaaaaa"

compartment_oid = "ocid.compartment.ocid.aaaaaaaaaaaaaa"

user_oid = "ocid.user.ocid.aaaaaaaaaaaaaa"

subnet_oid = "ocid.subnet.ocid.aaaaaaaaaaaaaa"

os_image_oid = "ocid.image.ocid.aaaaaaaaaaaaaa"

private_key_path = "./oci/oci1/private_key.pem"

fingerprint = "12:345678:7890:ad:cf:12345678:7890:ad:cf"
```



图 8.15 – `terraform.tfvars` 的内容

## 注意

参考指南提供了用于 `tenancy_ocid`、`compartment_ocid`、`user_oid`、`fingerprint`、`subnet_oid` 和 `private_key_path` 的代码：https://docs.oracle.com/en-us/iaas/Content/API/SDKs/terraformproviderconfiguration.htm。

获取 Oracle Linux 8 的 OCID，请访问以下链接：https://docs.oracle.com/en-us/iaas/images/oracle-linux-8x。它也是特定区域和特定架构，因此您可能需要找到 x86（或您的其他版本）的最新 Oracle Linux 8 镜像，并在镜像中查找 aarch64 的名称。

## 警告

请务必将 `terraform.tfvars` 文件添加到 `.gitignore` 中，以避免将任何敏感信息提交到版本控制。

### 12. 接下来，让我们运行 `terraform` 看看我们是否都执行得正确：

```bash
$ terraform init

$ terraform plan

$ terraform apply
```

`terraform` 命令会初始化包含你的 Terraform 文件的工作目录，这始终应该是你在编写了新的 Terraform 配置后运行的第一个命令。此外，运行 `terraform plan` 是一个好主意，因为这将给你一个预览/验证计划的机会。在此命令执行期间，`terraform` 将你的真实基础设施与你的配置进行比较。最后，运行 `terraform apply` 将再次显示计划，但它还会额外提供一个让你输入 `yes` 以执行计划提议的任何操作的机会。

当你看到要求你输入一个值的提示时，请直接输入 `yes`，然后按回车键。

# 重要说明

如果你 `get` `401-NotAuthenticated` 错误，请确保你已将公密钥添加到 OCI 控制台。这是在 API Key 认证方法下与 `private_key_path` 配对的公密钥。

如需将公密钥添加到 OCI 控制台的帮助，请访问 https://docs.oracle.com/en-us/Content/API/Concepts/apisigningkey.htm#three。

### 13. 如果一切顺利，你将观察到资源的创建。一旦完成，你将看到类似这样的消息：

```
Apply complete! Resources: 3 added, 0 changed, 0 destroyed.
```

### 14. 如果你检查 OCI 控制台，你将看到新创建的实例，并能够通过 Terraform 代码生成并存放在 Terraform 项目中 `instances` 文件夹内的 SSH 密钥对连接到它。

这足够简单，那么为什么不多自动化一点，这样我们不需要检查 OCI 控制台查看公网 IP 地址呢？我们只需要在 `main.tf` 文件中添加一点代码，就可以真正开始将事情提升到下一个水平了。

继续向你的 `main.tf` 文件添加以下代码：

```hcl
output "connection_details" {
  value = format("ssh -i .instances/${var.instance_name}/id_rsa opc@%s", oci_core_instance_ol_instance.public_ip)
  description = "连接详情"
}

resource "local_file" "readme" {
  filename = "${path.module}/${var.instance_name}/README.md"
  content = oci_core_instance_ol_instance.public_ip
}
```

图 8.16 – Terraform 的输出

图 8.18 – 无角色的长 playbook

## 注意

截图在结尾处淡出，是因为这是一个长 playbook，且 playbook 的全部内容并不重要。

此 playbook 自动化了几个任务。首先，它会在用户不存在时创建一个标准用户，然后通过 `container-tools` AppStream 模块安装 Podman，随后启动一个 NGINX 容器，最后开始升级系统上的所有软件包，并检查系统是否需要重启。

从这个示例中可以看出，如果你将所有任务直接写在 playbook 中，该文件很快就会变得巨大且难以管理。不久之后，你会发现自己不断在重复准备性任务，而且你可能会在每行不必要的任务开头添加井号（`#`），这将导致自动化将其视为注释而非代码——你可能还会发现自己在运行 playbook 时，不断在禁用和启用任务之间切换，以针对特定的任务。这可能会让你感到无从心，而且如果你不小心，可能会在不需要的时候删掉某些代码（尽管你实际上需要它们）。角色（Roles）提供了一种组织 playbook 的更好方法。事实上，你可以编写任意数量的角色，并在 playbook 中整洁地调用它们——这使得 playbook 随着时间的推移变得更容易阅读和维护。

## 创建角色

在 Ansible 中，角色组织在 `roles` 目录下。你在 `roles` 下创建一个文件夹，无论你给文件夹命名为什么，它将成为角色的名称。然后在该文件夹下，你至少创建一个名为 `tasks` 的文件夹，其中应包含一个 `main.yml` 文件，定义该角色将执行的主要任务：

### 1. 让我们拆分任务，通过在 `roles` 目录下创建一个 `users` 文件夹为我们的用户创建一个角色。

你的目录结构应该是：

```
playbook.yml
roles
  └── users
      ├── files
      │   └── wallpaper.jpg
      └── tasks
          └── main.yml
```

### 2. 现在，在 `tasks` 目录下创建一个 `main.yml` 文件，并将用户任务迁移到该文件中。

```yaml
- name: 创建标准用户并添加到特定组
ansible.builtin.user:
  name: user1
  shell: /bin/bash
  groups: admins,developers # depends on
  append: yes
```

```yaml
- name: 为用户 'user1' 创建 2048 位的 SSH 密钥
ansible.builtin.user:
  name: user1
  generate_ssh_key: yes
  ssh_key_bits: 2048
  ssh_key_file: ./id_rsa
```

```yaml
- name: 拷贝壁纸
copy:
  src: files/
  dest: /home/user1/Documents/Wallpaper
```

图 81 – 用于置备用户的优势角色

我们现在有了角色的雏形。我们可以利用其他功能来方便预配置操作。这里有两个我们打算在大多数文件和 `meta` 中使用的功能。

- 首先，你将引用一个 `files` 目录。这是一个属于角色的特殊目录，包含了与之相关的文件。
- 另一个是 `meta` 目录，作为声明依赖的一种。例如，由于 `users` 角色依赖于 `groups` 的存在，因此让此角色先依赖 `groups` 角色是一个好主意。为了实现这一点，我们可以为 `groups` 创建角色，然后从 `meta` 目录调用此角色。

`groups` 角色可能如下。注意目录结构以及附带的文件——它们共同构成了一个角色。你的目录结构应该是：

```
playbook.yml
roles:
  groups:
    tasks:
      main.yml
```

实际的任务应该写在 `main.yml` 文件中，内容如下：

```yaml
- name: 确保组存在
ansible.builtin.group:
  name: admins
  state: present
```

```yaml
- name: 确保组存在
ansible.builtin.group:
  name: developers
  state: present
```

图 8.20 – 用于用户组的 Ansible 角色

### 6. 现在，在 `users` 角色的 `meta/main.yml` 文件中，我们只需要将 `groups` 角色作为依赖调用：

```yaml
---
dependencies:
  role: groups
```

### 7. 最后，使用以下命令运行 playbook：

```bash
$ ansible-playbook playbook.yml
```



你已成功在 Ansible 中创建了一个角色。

8. 接下来，重复此过程，直到你将所有内容都组织角色角色。对我来说，我最终得到了如下结构：

```
playbook.yml

roles

  base_software

    tasks:

      main.yml

  containers

    tasks:

      main.yml

  get_hostname

    tasks:

      main.yml

  groups

    tasks:

      main.yml

  update_packages

    meta:

      main.yml

    tasks:

      main.yml

  uptime

    tasks:

      main.yml

  users

    files:

      wallpaper.jpg

    meta:

      main.yml

    tasks:

      main.yml
```

# 新型且改进的 playbook

至于实际的 playbook，现在可以简化为如下：

```yaml
name: 应用标准配置

hosts: localhost

become: yes

vars:
  ansible_python_interpreter: /usr/bin/python3

roles:
  - get_hostname
  - users
  - containers
  - update_packages
```

图 8.21 – 利用角色的 Ansible playbook

## 注意

注意，我们没有在 playbook 中列出 `base_software` 和 `groups` 角色，因为它们在 `meta` 下定义。如你所见，我们现在引用的是角色，而不是任务。这非常整洁且有序，而且理解 playbook 做了什么变得容易得多，你只需要进入相应的角色目录并检查 `main.yml` 文件。当你准备好后，正常运行 playbook：

```bash
$ ansible-playbook playbook.yml
```

如果一切顺利，你应该已经完成了原始 playbook 中所做的工作；但现在使用角色让你的 playbook 更易维护。此配方的源代码可以在此处找到：https://github.com/PacktPublishing/Oracle-Linux-Cookbook/tree/ch8/ansible-roles。

# 使用 Ansible 管理密钥

此配方旨在提供利用 Ansible Vault 进行密钥管理的指导。刚开始时你可能倾向于加密整个 hosts 文件。这在版本控制的背景下有效且能保持一切安全；但它并不可控，你也不会留下一长串毫无意义的加密字符。

# 入门

此配方需要以下内容：

- Oracle Linux

请参考本章开头的技术要求。

## 如何操作

首先，让我们看看加密文件。为了开始，我们需要先定义一个明文 hosts 文件。

通常，hosts 文件看起来如下：

```ini
# hosts

[host1]

192.168.1.10

ansible_user=admin

ansible_password=password

[host2]

192.168.1.11

ansible_user=admin

ansible_password=password
```

你可以通过运行以下命令加密文件：

```bash
$ ansible-vault encrypt hosts
```

系统会提示你输入并确认密码。加密后，文件内容将变成一串乱码。

要查看加密内容而不编辑，可以使用：

```bash
$ ansible-vault view hosts
```

如果你需要编辑加密文件，可以使用：

```bash
$ ansible-vault edit hosts
```

在运行 playbook 时，你需要提供密码来解密：

```bash
$ ansible-playbook playbook.yml --ask-vault-pass
```

或者你可以使用环境变量：

```bash
export ANSI_VAULT_PASS=yourpassword

ansible-playbook playbook.yml
```

或者使用密码文件：

```bash
$ ansible-playbook playbook.yml --vault-password-file file
```

这可能会让你感到无从心，而且如果你不小心，可能会在不需要的时候删掉某些代码（尽管你实际上需要它们）。角色（Roles）提供了一种组织 playbook 的更好方法。事实上，你可以编写任意数量的角色，并在 playbook 中整洁地调用它们——这使得 playbook 随着时间的推移变得更容易阅读和维护。

1. 我们使用 `encrypt_string` 方法。在示例中，我们想要加密的字符串是 `B@by-Y0dA`，并将标识此密码的变量命名为 `admin_password`。

```bash
$ ansible-vault encrypt_string --password-file vault_password 'B@by-Y0dA' --name 'admin_password'
```

在终端中，你将输入你的密码 'B@by-Y0dA'，看起来如下：

```bash
$ ansible-vault encrypt_string --password-file vault_password 'B@by-Y0dA' --name 'admin_password'

$ ANSIBLE_VAULT;1:AES256

37352630616352663736273638232530362634362327302634304236326536323830006430

61323838303936353133343533282836333333363624333434343632353536323236361136

31363837323136353236383336368833373835333732313632343639363948353646013036

343333373232363035383436333136363337313633333939393933366636333333333039336463

3332
```

图 8-3。加密密钥

2. 接下来，我们需要将输出拷贝到 `secrets.yml` 文件中（你只需要在之前的命令后添加 `>> secrets.yml` 即可将输出拷贝到文件中）。这里有一个示例：

```bash
$ ansible-vault encrypt_string --password-file vault_password 'B@by-Y0dA' --name 'admin_password' >> secrets.yml
```

你的 `secrets.yml` 文件应该像这样：

```yaml
--- secrets.yml

ansible_password: |
  $ANSIBLE_VAULT;1:AES256
  66303623353036263337363834363336303436373830353135363435323316253030
  3531383839393936333731313131313535353937373639393136383834323134303034323035
  663236383036373134353330363633313633313535393939333336363636363636323327
  3134373436363236223035383436333136363337313633333939393933366636333333333063
  6234
```

图 8-4。`secrets.yml` 的内容

# 重要提示

你可能会发现，每次运行命令时加密值都会发生变化，即使你使用相同的密码加密相同的值。随机盐在每次加密时都会改变；这是设计如此的，目的是确保最终输出永远不会相同（即使使用相同的内容）。

3. 现在既然你已经完成了加密，可以将你的主机文件中的 `ansible_password` 值替换为引用该密码的变量名（在本例中为 `admin_password`）：

```ini
# hosts

[host]

192.168.2.70

[host:vars]

ansible_user=admin

ansible_password={{ admin_password }}

ansible_connection=ssh

ansible_shell_type=powershell

[host2]

192.168.2.71

[host2:vars]

ansible_user=admin
```



`ansible_password={{ admin_password }}`

`ansible_connection=ssh`

`ansible_shell_type=powershell`

## 注意

变量级加密的优势是文件仍然可以被容易读取和理解，因为会有明文与加密变量混合在一起。

该食谱的源代码可以在此处找到：https://github.com/PacktPublishing/Oracle-Linux-Cookbook/tree/main/ch8/ansible-vault。

# 使用 Vagrant 搭建完美的实验环境

最近在工作中，我被要求准备一个 Oracle Linux Manager 的演示并展示该软件的几项功能。这是一件很容易的事，但由于准备一个 Oracle Linux Manager 的演示并展示该软件的几项功能。

最近在工作中，我被要求准备一个 Oracle Linux Manager 的演示并展示该软件的几项功能。这是一件很容易的事，但由于……（使用 Vagrant 搭建完美的实验环境）准备一个 Oracle Linux Manager 的演示并展示该软件的几项功能。

（由于源文本在后半部分存在严重的乱码式重复，上述译文已根据可读性进行了整合。）

```
db-backend = postgresql

db-name = spacchema

db-user = spaceuser

db-password = Password

db-host = localhost

db-port = 5432

enable-tftp = Y
```

这总结了大部分的安装和配置步骤。接下来，为了让这一切正常工作以便我们能够使用 Vagrant 自动部署和配置 Oracle Linux Manager，我们需要进行一些简单的更改。我们真正需要做的是将这些步骤粘贴到 Bash Shell 脚本中，并告诉 Vagrant 使用提供程序（provisioner）在虚拟机上运行这些命令。同样，由于自动化无法进行交互，我们还需要在所有的 `yum` 命令中添加 `-y`。

因此，为了清理并为 Vagrant 准备，我们的 Bash 脚本看起来像这样：

```bash
#!/bin/bash

yum remove ita -y

echo "exclude=ita*" >> /etc/yum.conf

yum-config-manager --disable ol7 -y

yum install oracle-release-el7 -y

yum install oracle-linux-manager-server-release-el7 -y

yum-config-manager --enable-el7 --optional-latest -y

yum install spacewalk-schema-2.10.14-1.el7 spacewalk-setup-postgresql spacewalk-postgresql

spacewalk-setup -utils -y --non-interactive --answer-file=/tmp/answer-file.txt
```

## 注意

在编写此配方的过程中某个时刻，`spacewalk-schema` 包进行了更新，使其不再兼容 PostgreSQL。这可以通过如前面的代码所示，将 `spacewalk-schema` 包固定到 `spacewalk-schema-2.10.14-1.el7` 来修复。

我删除了每个步骤中的 `sudo` 调用，因为在 Vagrant 的配置阶段，一切都是以 root 身份运行的。

现在处理 `Vagrantfile`，添加几行以便 Vagrant 可以将 `answer-file.txt` 复制到虚拟机中，然后执行我们刚刚编写的脚本。我们还将创建一个私有网络，允许使用特定的 IP 仅访问该机器（这将允许我们通过浏览器轻松访问 Oracle Linux Manager）：

```ruby
# - mode: ruby -
# vi: set ftruby =
# 所有 Vagrant 配置都已在下方。Vagrant.configure 中的 "2"
# 配置了配置版本（为了后兼容，我们支持旧样式）。
# 除非你知道自己在做什么，否则请不要更改。

Vagrant.configure("2") do |config|
config.vm.box = "oracelinux/7"
config.vm.box_url = "https://github.com/vagrantboxes/oracelinux/7.json"
config.vm.network "private_network", ip: "192.168.56.10"
config.vm.provision "file", source:="answer-file.txt", destination="/tmp/answer-file.txt"
config.vm.provision "shell", path="provision", inline:="echo Access Oracle Linux Manager at https://192.168.56.10"
```

图 8.25 – 用于部署 OLM 的 Vagrant 文件

## 注意

在基于 Linux 的系统中，VirtualBox 仅允许将 192.168.56.0/21 范围内的 IP 地址分配给主机主机网络适配器。对于你的以 192.168.56.1 和 192.168.63.254 开头的 IP 地址。

现在我们可以看到我们的目录结构如下：

- oracle-linux-manager
  - answer-file.txt
  - provision.sh
  - Vagrantfile

我们准备好修复这一切了：

```
$ vagrant up

---
--> default: Running provisioner: shell...
    default: Running: inline script
    default: Access Oracle Linux Manager at https://192.168.56.60
```



你将看到配置脚本安装并配置 Oracle Linux Manager，在几分钟内，你就可以将浏览器指向为虚拟访问 Oracle Linux Manager 定义的 IP 地址了。最棒的部分是一切都是通过代码定义的。此配方中创建的所有内容仅为 6 KB！Vagrant 在解决经典的“在我的机器上可以运行”问题方面非常出色。你可以将这 6 KB 代码部署在任何机器（Mac、Windows、Linux 等）上——你只需要 Vagrant 和 VirtualBox。我们可以自动化一些步骤来使其更有用。例如，我们可以自动化创建 Oracle Linux Manager 的第一个用户，自动创建存储库和激活密钥，然后为 OLM 创建客户端并连接到它们。详细介绍所有细节超出了此配方的范围，但如果你感兴趣查看如何实现，我已经将解决方案发布在 GitHub 上——你可以在这里找到：https://github.com/Oracle-Cookbook

# 使用 Packer 修改镜像

Packer 是一个用于创建机器镜像的工具。在此配方中我们将使用 Packer 引用 Oracle Linux 8 作为基础镜像，使用提供程序安装内容，并将带有这些更改的新 OCID 镜像推送到 OCI。

> 注意
> 尽管 OCI 提供了“始终免费”资源，但不包含存储镜像的能力。如果你想遵循此配方，将需要使用付费账户。

## 准备工作

对于此配方，你需要以下内容：

- Oracle Linux own- Packer

## 如何进行

Packer 经常被忽略，因为它看起来如此简单——然而，Packer 是极其强大的。1. 首先，我们将 `oracle` 类型的 `type` 定义在 `packer` 块中。`packer` 的 `type` 如下：

```bash
packer {
  type = "oracle"
}
```

2. 接下来，我们将 `oracle-oci` 的配置到 OCI。详情可以通过 `https://github.com/Oracle-Cookbook` 获取。

图 8.26 – oracle-oci

- 然后，我们需要在 `variables.hcl` 文件中声明所有变量。在这个文件中，我们定义 `type` 如下：

```hcl
variable {
  type = "string"
}
```

图 8.27 – Packer 中引用变量

- 最后，我们在 `variables.hcl` 文件中声明这些变量。输入 `type` 如下：

```hcl
variable "tenancy_oid" {
  type        = string
  description = "OCID of tenancy"
}
variable "compartment_oid" {
  type        = string
  description = "OCID of compartment"
}
variable "fingerprint" {
  type        = string
  description = "Fingerprint for the key pair used: 12:34:56:78:90:ab:cd:ef"
```

图 8.28 – Packer 中的变量声明

- 最后，我们将为变量赋值。我们将它们放在 `variables.auto.pkrvars.hcl` 文件中。它看起来像这样：

```hcl
tenancy_oid           = "ocid1.tenancy.oc1.aaaaaaaaaaaa"
compartment_oid      = "ocid1.compartment.oc1.aaaaaaaaaaaa"
user_oid              = "ocid1.user.oc1.aaaaaaaaaaaa"
subnet_oid            = "ocid1.subnet.oc1.aaaaaaaaaaaa"
availability_domain = "Uoc:US-ASHBURN-AD-3"
region               = "us-ashburn-1"
key_file             = "../oci_api_key.pem"
fingerprint          = "12:34:56:78:90:ab:cd:ef"
```

图 8.29 – Packer 中的变量赋值

- 另一种方法是在 `./oci/config` 中配置你的 OCI CLI。它看起来像这样：

```ini
[DEFAULT]
user=ocid1.user.oc1.<unique_ID>
fingerprint=<your_fingerprint>
key_file=./oci_api_key.pem
tenancy=ocid1.tenancy.oc1.<unique_ID>
region=us-ashburn-1
```

```
user=ocid.user.ocl.<unique_ID>
fingerprint=<your_fingerprint>
key_file=keys/admin.key
pass_phrase=<your_passphrase>
```

## 注意

关于配置 OCI CLI 的完整细节，请参阅此处：https://docs.oracle.com/en-us/iaas/Content/API/Concepts/sdkconfig.htm

3. 一旦配置好身份验证，就可以开始定义基础镜像。它看起来如下：

```
source "oracle-oci" = "example" {
  ...
  base_image_ocid = "ocid1.image.oc1.iad.aaaaaaaaaaaa"
  image_name = "Oracle Linux 8.8"
  shape = "VM.Standard.E4.Flex"
  shape_config {
    ocpus = 2
    memory_in_gbs = 4
  }
  ssh_username = "opc"
}
```

图 8.30 – 在 Packer 中定义基础镜像

## 注意

要获取 Oracle Linux 8，请访问以下 URL：https://docs.oracle.com/en-us/iaas/images/oracle-linux-8x/。此具有特定区域和特定架构，因此您需要找到适用于 x86 的最新 Oracle Linux 8 镜像（换句话说，寻找名称中不包含 aarch64 的镜像）。

4. 一旦定义了源，您就可以继续在 Packer 上安装并决定在构建过程中要执行的操作。在这种情况下，我们将调用一个配置器（provisioner），以便我们运行一个 shell 命令来安装 Git：

```
build {
  ...
  name = "Oracle Linux 8.8 with Git"
  sources = ["source.oracle-oci.example"]
  provisioner = "shell" {
    inline = ["sudo dnf install -y git"]
  }
}
```

图 8.31 – Packer 配置器

5. 此时，我们已经告诉了 Packer 我们想要使用什么作为我们的源，并描述了我们在构建时想要执行的操作。您的整个文件应该看起来像：

```
packer {
  required_plugins {
    oracle-oci = {
      version = ">> 1.0.4"
      source = "github.com/hashicorp/oracle"
    }
  }
}
source "oracle-oci.ol8u8" {
  tenancy_oid = "${var.tenancy_oid}"
  compartment_oid = "${var.compartment_oid}"
  user_oid = "${var.user_oid}"
  fingerprint = "${var.fingerprint}"
  key_file = "${var.key_file}"
  subnet_oid = "${var.subnet_oid}"
  availability_domain = "${var.availability_domain}"
  region = "${var.region}"
  base_image_oid = "ocid.image.oci1.iad.aaaaaaaaaaaa"
  image_name = "Oracle Linux 8.8"
  shape = "VM.Standard.E4.Flex"
  shape_config {
    ocpus = 2
    memory_in_gbs = 4
  }
  ssh_username = "opc"
}
```



build {

  name = "Oracle Linux 8.8 with Git"

  sources = ["source.oracle-oci.ol8u8"]

  provisioner "shell" {

    inline = ["sudo dnf install -y git"]

  }

}

```
图 8.32 – 修改基础镜像的完整 Packer 文件

## 注意

最后，我将示例替换为 `ol8u8`，以便更具体地描述我正在处理的内容。

- 6. 接下来，我们将运行 `packer init` 来下载外部插件：

```
$ packer init
```

- 7. 最后，让我们开始构建 OCID 镜像：

```
$ packer build
```

`Packer` 将 Oracle Cloud 中启动一个全新的 Oracle Linux 8 实例。当机器运行时，它将运行 `dnf install -y git` 在实例上安装 Git。

![](img/110fa0d6324f0893fff03cee6394144d_292_0.png) 图 8.3 - 运行 `packer build` 后的初始输出

一旦安装了 Git，我们将对实例进行快照并将其导出为新的 OCI 镜像，为我们未来的实例提供一个起点。

![](img/110fa0d6324f0893fff03cee6394144d_293_0.png) 图 8.34 — Packer 构建时的输出

当 Packer 完成后，可以通过导航到 OCI 控制台上的 **Compute > Custom Images**（计算 > 自定义镜像）来查看新发布的镜像。以下是它的示例：

![](img/110fa0d6324f0893fff03cee6394144d_293_1.png) 图 8.35 — 在 OCI 上查看新发布的自定义镜像

此配方的源码可以在 `https://github.com/PacktPublishing/Oracle-Linux-Cookbook/tree/main/ch8/packer-build` 找到。

# 打包

在这个配方中，我们将使用 `Packer` 从源媒体（如 ISO）从零开始创建我们自己的 Vagrant box。

# 入门

此配方需要您准备以下内容：
- Oracle Linux
- Oracle VirtualBox
- Packer

如果需要安装 Oracle VirtualBox 和 Packer 的帮助，请参考章节开头要求的部分。

## 如何操作

此外，您可以在 Vagrant 目录中搜索包含您正在寻找的系统的预制 Vagrantfile。但如果没有那里怎么办？或者您更倾向于创建自己的。您可以手动这样做，也可以通过利用 Packer 完全实现。在这个配方中，在高层次，Packer 将下载我们想要使用的操作系统 ISO。它将使用 VirtualBox 启动并安装虚拟机。之后，它将以 OVF 格式导出虚拟机。最后，它会将此文件压缩并转换为 Vagrant box。

# Oracle Linux 8 kickstart 文件

- 1. 就此，您将需要创建一个 kickstart 文件来自动化安装 ISO。您可以创建自己的，或者使用 GitHub 上的 Oracle Linux Image Tools 提供的：

```
https://github.com/oracle/oracle-linux/blob/main/oracle-linux-image-tools/dist/ol8-slim/ol8-ks.cfg
```

- 2. 现在，就此创建一个新目录 `vagrant-ol8`。在此目录中创建一个名为 `vagrant-ol8.pkrhcl` 的文件，并创建一个名为 `http` 的文件夹并将 kickstart 文件放置在其中。完成后，您的文件结构应该像：

```
vagrant-ol8
  ├── http
  |     └── ol8-ks.cfg
  └── vagrant-ol8.pkrhcl
```

注意 `modifyvm` 命令，它将 `--natdnshost` 设置为 `on`。这是 Oracle VirtualBox 7 中默认关闭的设置。将此值设置为开启可以防止 Packer 发送 kickstart 时的网络问题。也就是说，如果您使用 VirtualBox 7 构建虚拟机，这一点很重要，但如果您使用的是 VirtualBox 6，则需要删除此行否则构建将失败。

- 6. 所以，在前面的代码中，我们将 `guest_os_type` 设置为 `"Oracle_64"`，因为我们是从 Oracle Linux ISO 构建的。接下来，输入它的 URL。对于 `ssh_username`，我们将使用 `"root"`；对于 `ssh_password`，我们将使用 `"vagrant"`，因为这些是 Vagrant 期望的默认值，以便分发 box。如果您打算私用该 box，最好使用不同的值，这样更安全。

# 有有关 Vagrant 用户名的更多信息，请访问 `https://www.vagrant.com/docs/boxes#vagrant-user`。

- 7. 我们将 `headless` 设置为 `"true"`，以防止虚拟机启动 VirtualBox GUI。我们增加了 `ssh_wait_timeout` 时间，以确保操作系统完成安装并运行。所有这些都是自言自明的；除非我们使用 `http_directory`。

- 8. 您只需要知道的是，我们将利用 `http_directory` 作为使用 HTTP 服务器提供目录的方便方法。这样做可以让启动命令指向 `http_directory` 中的 kickstart 文件：`http://{{ HTTP }}:{{ PORT }}/ol-8.cfg`，获取操作系统所需的一切。我们不需要担心 `{{ HTTP }}` 和 `{{ PORT }}` 的语法；这些是 Packer 模板引擎提供的模板变量。

- 9. 对于 `nic_type`，默认是 82540，等同于 Intel PRO/1000。这是一个安全的选择，在运行操作系统时非常好，但 Oracle Linux 8 是现代操作系统，所以我们将其设置为 virtio。VirtIO 是一种虚拟化驱动程序，将为虚拟机提供更好的网络性能。

- 10. 现在，在 `boot_command` 上，我们需要我们需要向操作系统发送启动命令所需的按键序列。在 Oracle Linux 8 的情况下，我们发送 `up` 和 `Tab` 键，然后是关于在哪里找到 kickstart 文件的指令，最后告诉它在安装操作系统之前按回车。

- 11. 对于 `vboxname`，我发现默认情况下 Packer 尝试仅用 512 MB 内存启动我的虚拟机，这导致在操作系统安装期间出现错误。为了解决这个问题，我将内存增加到 2048。此外，为了保险，还有两个 CPU。

- 12. 最后，通过 `shutdown_command`，我们只需告诉系统在所有配置完成后如何地关闭系统。然后 Packer 将正确关闭机器。

13. 此时，我们必须自动安装操作系统，但我们需要再做几件事来为 Vagrant 准备虚拟机。为此，我们需要添加一个名为 vagrant 的用户，为该用户填充您的用户的授权密钥，并且我们将安装 VirtualBox Guest Additions。

对于这些任务，我们将利用配置器执行 shell 脚本。此任务发生在操作系统安装之后，虚拟机仍在运行期间。这是在我们关闭系统并将其转换为 Vagrant box 之前的最后一项工作。

请将以下内容添加到 `vagrant-ol8.pkrhcl` 文件中：

```bash
build {

  sources = ["sources.virtualbox-iso.ol8u8"]

  provisioner = "shell" {

    script = "scripts/vagrant-base-box.sh"

  }

  post-processor = "vagrant" {

    output = "ol8-x64-virtualbox.box"

  }

}
```

图 8.38 – 用于构建 Vagrant box 的 Packer 文件（续）

# 信息

关于后处理器（post-processors）的更多信息可以在此处找到：`https://www.packer.io/plugins/post-processors/vagrant/vagrant#virtualbox`。

14. 如前面的截图所示，我们将创建一个名为 `scripts` 的新文件夹，并将 shell 脚本放在其中：

- ol8-vagrant
  - http
    - ol8-ks.ks
  - scripts
    - vagrant-base-box.sh
  - vagrant-ol8.pkr.hcl

15. 现在，在 `vagrant-base-box.sh` 脚本中，我们将添加以下内容：

```bash
#!/bin/bash

# Prepare vagrant
```



`useradd -m vagrant`

`usermod -aG sudo vagrant`

`echo "vagrant:vagrant" | chpasswd`

`echo "vagrant ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/vagrant`

`mkdir -p /home/vagrant/.ssh`

`curl https://raw.githubusercontent.com/hashicorp/vagrant/main/keys/vagrant.pub >> /home/vagrant/.ssh/authorized_keys`

`chmod 600 /home/vagrant/.ssh/authorized_keys`

`chown vagrant:vagrant /home/vagrant/.ssh`

# Setup proxy access to the internet

`echo "UseDNS no" >> /etc/ssh/sshd_config`

# Install packages for VirtualBox Guest Additions

`dn install -y kernel-devel kernel-headers gcc make perl`

# Install VirtualBox Guest Additions

`mkdir -p /mnt/iso`

`mount -o loop /root/VBoxAdditions.iso /mnt/iso`

`sh /mnt/iso/VBoxAdditions.run`

`umount /mnt/iso`

`rm -rf /root/VBoxAdditions`

# Clean up to reduce size of Vagrant box

`dnf remove -y kernel-devel-headers`

`dnf clean all`

`cat /dev/zero > /dev/null > /tmp/zero.fill`

`rm -f /tmp/zero.fill`

图 8.9 - `vagrant-base.sh` 脚本的内容

16. 接下来，我们将使用 `packer init` 下载外部插件：

```bash
$ packer init
```

17. 现在，我们将构建 Vagrant box。这部分非常简单，只需运行以下命令：

```bash
$ packer build
```

在输入命令后，你将看到如下内容：

```
packer build
virtualbox-iso.al08: 输出将以此颜色显示。
# virtualbox-iso.al08: 在 vboxmanager 输出中未找到 "Default Guest Additions ISO"或输出为空）
# virtualbox-iso.al08: Retrieving guest additions checksum
# virtualbox-iso.al08: Downloading https://raw.githubusercontent.com/hashicorp/virtualbox/7.0.10/VBoxGuestAdditions.iso
# virtualbox-iso.al08: Verifying https://raw.githubusercontent.com/hashicorp/virtualbox/7.0.10/VBoxGuestAdditions.iso
# virtualbox-iso.al08: Checksum (sha256:8663933333737373737373733333333333333333)
# virtualbox-iso.al08: Retrieving guest additions checksum
# virtualbox-iso.al08: Downloading https://raw.githubusercontent.com/hashicorp/virtualbox/7.0.10/VBoxGuestAdditions.iso
# virtualbox-iso.al08: Verifying https://raw.githubusercontent.com/hashicorp/virtualbox/7.0.10/VBoxGuestAdditions.iso
# virtualbox-iso.al08: Checksum (sha256:8663933333737373737373733333333333333333)
# virtualbox-iso.al08: Using cached image https://packer.io/ubuntu/iso/virtualbox-22.04-generic-amd64.iso
# virtualbox-iso.al08: Using image https://packer.io/ubuntu/iso/virtualbox-22.04-generic-amd64.iso
# virtualbox-iso.al08: Using image https://packer.io/ubuntu/iso/virtualbox-22.04-generic-amd64.iso
# virtualbox-iso.al08: Using image https://packer.io/ubuntu/iso/virtualbox-22.04-generic-amd64.iso
# virtualbox-iso.al08: Using image https://packer.io/ubuntu/iso/virtualbox-22.04-generic-amd64.iso
# virtualbox-iso.al08: Using image https://packer.io/ubuntu/iso/virtualbox-22.04-generic-amd64.iso
# virtualbox-iso.al08: Using image https://packer.io/ubuntu/iso/virtualbox-22.04-generic-amd64.iso
# virtualbox-iso.al08: Using image https://packer.io/ubuntu/iso/virtualbox-22.04-generic-amd64.iso
# virtualbox-iso.al08: Using image https://packer.io/ubuntu/iso/virtualbox-22.04-generic-amd64.iso
# virtualbox-iso.al08: Using image https://packer.io/ubuntu/iso/virtualbox-22.04-generic-amd64.iso
# virtualbox-iso.al08: Using image https://packer.io/ubuntu/iso/virtualbox-22.04-generic-amd64.iso
# virtualbox-iso.al08: Using image https://packer.io/ubuntu/iso/virtualbox-22.04-generic-amd64.iso
# virtualbox-iso.al08: Using image https://packer.io/ubuntu/iso/virtualbox-22.04-generic-amd64.iso
# virtualbox-iso.al08: Using image https://packer.io/ubuntu/iso/virtualbox-22.04-generic-amd64.iso
# virtualbox-iso.al08: Using image https://packer.io/ubuntu/iso/virtualbox-22.04-generic-amd64.iso
# virtualbox-iso.al08: Using image https://packer.io/ubuntu/iso/virtualbox-22.04-generic-amd64.iso
# virtualbox-iso.al08: Using image https://packer.io/ubuntu/iso/virtualbox-22.04-generic-amd64.iso
# virtualbox-iso.al08: Using image https://packer.io/ubuntu/iso/virtualbox-22.04-generic-amd64.iso
# virtualbox-iso.al08: Using image https://packer.io/ubuntu/iso/virtualbox-22.04-generic-amd64.iso
```



# virtualbox-iso.al08: Using image `https://packer.io/ubuntu/iso/virtualbox-22.04-generic-amd64.iso`



这需要一些时间，它实际上会进行一些构建。记住我们从高层层面讨论过的内容：Packer 将下载 ISO、创建虚拟机并安装操作系统，并且

# Signing Git commits with GPG

This recipe will show you how to digitally sign Git commits and RPM packages using a GNU Privacy Guard (GPG) keypair. A GPG keypair consists of two parts: the public key and the private key.

This is done by creating a GPG keypair and using it to sign Git commits and RPM packages.

## Getting ready

In order to work with GPG and Git, you first need to install a few packages. Normally GPG is installed by default when the package `gnupg2` is installed.

Git should be installed using `dnf install git -y`.

## How to do it...

The first step is to create a GPG key if you do not already have one. Key will be used to sign your Git commits and RPM packages. To work with the GPG key, you can use the `gpg` or `gpg2` commands; both are the same thing, as `gpg` links via `gpg2`.

The GPG key is created via the command line:

```
[erik@018 ~]$ gpg2 --gen-key
```

The command will ask for some information, mainly your real name and email address. After you enter the information and continue, it will also ask you to set a passphrase to the key. Do not forget the passphrase! If you do, the key will become unusable and you will lose all data encrypted with the key. You can choose not to use a passphrase, but if you do, this will be asked to verify several times. The output of the key creation should be similar to the following screenshot:

```
[erik@ol8~$]$ gpg --gen-key

gpg (GnuPG) 2.2.20: Copyright (2020) Free Software Foundation, Inc.

This is free software: you are free to change and redistribute it.

Distributed under the GNU General Public License; you may copy and redistribute it for

any purpose, provided that it is PROVIDED WITHOUT WARRANTY, as permitted by law.

```

使用：`gpg --full-generate-key` 进入完整的 GPG 密钥生成对话框。
GnuPG 需要存储一个用户 ID 来识别您的密钥。

真实姓名：Erik Benner
邮箱地址：erik@salesfromthedatacenter.com
创建了无过期日期的 User ID。
`*Erik Benner <erik@salesfromthedatacenter.com>*`

更改 (姓名)、(邮箱) 或 (O) 输出？执行其他操作（通过键盘、鼠标，利用注释字段让随机数生成器有更好的机会获取熵）是一个好主意。
想要生成密码短语？执行其他操作（通过键盘、鼠标，利用注释字段让随机数生成器有更好的机会获取熵）是一个好主意。
您想要删除密钥生成吗？

gpg 撤销证书存储在 `~home/erik/.gnupg/revocations.d/7FC8D9E6B1D5C15F1970DE10BCF114350C7F1D74.rev`
公钥已创建

```
pub   2048-2022-10-02 [SC] [expires: 2024-01-01]

73C515F1970DC8F90DE10BCF

uid   [ultimate] Erik Benner <erik@salesfromthedatacenter.com>

sub   2048-2022-10-02 [E] [expires: 2024-01-01]
```

![](img/110fa0d6324f0893fff03cee6394144d_304_0.png)

此外，您可以使用 `--full-generate-key` 选项，该选项可用于在硬件设备上创建密钥。
一旦密钥创建，它将存在于您的密钥环中，位于主目录下 `gnupg` 目录下的 `pubring.kbx` 文件。要查看文件中所有的密钥，请运行 `gpg --list-keys --keyid format=long` 命令。

`gpg --list-secret-keys` 命令用于列出存储在您的 GPG 密钥环中的密钥（即私钥）。运行该命令将显示与下图类似的 GPG 密钥输出：

```
[erik@ol8~$]$ gpg --list-secret-keys --keyid-format=long
/home/erik/.gnupg/pubring
```

```
sec   2048-EB9B1F9E222B16 2022-10-02 [SC] [expires: 2024-01-01]

6510F8040DBB30D55BF90562922B

uid   [ultimate] Erik Benner <erik@salesfromthedatacenter.com>

sub   2048-2022-10-02 [E] [expires: 2024-01-01]

sec   2048/954D7B86C73915178 2022-10-02 [SC] [expires: 2024-01-01]

728BF4A7E647C261195BF6B4A5084B6717

uid   [ultimate] Erik Benner <erik@xyzzy.net>

sub   2048/B7D3AC42EE1E808FF 2022-10-02 [E] [expires: 2024-01-01]

sec   2048/BF114350C7CFD74 2022-10-02 [SC] [expires: 2024-01-01]

73C515F1970DC8F90DE10BCF114350C7F1D74

uid   [ultimate] Erik Benner <erik@salesfromthedatacenter.com>

sub   2048/EB637BAE2D1A7 2022-10-02 [E] [expires: 2024-01-01]
```



![](img/110fa0d6324f0893fff03cee6394144d_304.png)

输出为每个密钥提供了几列：

- `sec` 表明该密钥是一个私钥。
- `rsa2048/4096/`：此列显示密钥所使用的算法和长度。例如，`rsa2048` 表示该密钥使用长度为 2048 位的 RSA 算法。如果使用长格式，则会显示更多。
- `[creation date]`：显示密钥创建日期。
- `[expires]`：如果密钥有过期日期，则将显示该日期。
- `uid`：显示与密钥关联的用户 ID。
- `sub`：显示子密钥。
- `fingerprint`：密钥的指纹。
- `ID`：密钥 ID。
- `format`：密钥格式。

### 3. 使用 webroot 模式创建证书
`webroot` 模式要求网站能够通过 80 和 443 端口从互联网上访问。虽然这种方法易于实现，但还有另一种使用 DNS 的验证方法。有关关于不同挑战类型的更多信息，请参阅 https://letsencrypt.org/challenge-types/

### 4. 进行测试。

## 安装带有 mod_ssl 及其所有依赖的 Apache

1. 让我们以 root 用户身份开始。首先，我们需要添加一些软件包：

- `httpd` Apache Web 服务器
- `mod_ssl` 在 Apache 上启用 SSL

你可以通过以下命令执行此操作：

```
dnf install -y httpd mod_ssl
```

2. 接下来，在防火墙中添加端口 80 和 443。以 root 身份执行以下命令来完成：

```
firewall-cmd --zone=permanent --add-service=http
firewall-cmd --zone=permanent --add-service=https
firewall-cmd --reload apache
```

3. 现在，我们为 `/ssltest.talesfromdatacenter.com` 设置一个虚拟服务器。这样，我们以后就可以仅为这个虚拟服务器添加 SSL 证书。以 root 身份，为文件创建一个目录并将所有权更改为 apache 用户：

```
mkdir -p /var/www/ssltest
chown apache:apache /var/www/ssltest
```

4. 接下来我们将在 `/etc/httpd/conf.d` 中添加一个配置文件 `ssltest.conf`：

```
<VirtualHost *:80>
    # 将此内容放入 /etc/httpd/conf/ssltest.conf
    Alias /.well-known/acme-challenge/ /var/www/ssltest/.well-known/acme-challenge/
    <Directory "/var/www/ssltest/.well-known/acme-challenge">
        AllowOverride None
        ContentType text/plain
        RedirectMatch 404 "^/(?!\\.well-known/acme-challenge/[\\w-]{33})$"
    </Directory>
    RewriteEngine On
    RewriteCond %{REQUEST_URI} !^/\.well-known/acme-challenge [NC]
    RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI} [R=301,L]
</VirtualHost>
```

5. 完成后，运行 `apachectl configtest`。在修改配置文件时始终运行此测试是一个良好的习惯。

```
apachectl configtest
Syntax OK
```

6. 接下来，启动 Apache 并确保我们可以访问默认页面。`enable` 选项将在系统启动时重启服务器。`--now` 选项将立即启动服务器：

```
systemctl enable --now httpd
```

7. 现在，将你的浏览器指向 80 端口。你应该看到默认的 Apache 页面。注意左上角的“不安全”标记！该网站没有使用 SSL：

![](img/110fa0d6324f0893fff03cee6394144d_309_0.png)

此页面用于测试安装后 Apache HTTP 服务器的运行情况。如果你能看到此页面，说明在该站点安装的 Apache 服务器工作正常。

## 如果你是普通公众成员：

你看到此页面表明你刚刚访问的网站正在遇到问题或进行例行维护。

## 如果你是网站管理员：

如果你想让该网站的管理员知道你看到了这个页面而不是目标页面，你应该给他们发送电子邮件。通常情况下，发送给名为“webmaster”并指向你的网站域名即可联系到相应人员。

你现在可以向 `/var/www/html/` 目录添加内容了。在此之前，访问你网站的人将看到此页面而不是你的内容。为了防止这种情况再次发生，请遵循 `/etc/httpd/conf/httpd.conf` 文件中的说明。

例如，如果你在访问 `example.com` 时遇到问题，应该向 "`webmaster@example.com`" 发送电子邮件。

你可以自由在由 Apache Linux 支持的 HTTP 服务器上使用下面的图片。感谢使用 Apache！

![](img/110fa0d6324f0893fff03cee6394144d_309_1.png)

## 从 Git 获取 acme

现在，我们需要从 Git 获取 `acme.sh` 脚本：

- 1. 首先，我们需要通过以下命令安装 Git：

```
dnf install -y git
```

- 2. 接下来，创建一个名为 `acme` 的目录：

```
mkdir acme
```

- 3. 现在，我们可以通过以下命令从 GitHub 站点（https://github.com/acmes-official/acme.sh）克隆官方仓库：

```
git clone https://github.com/acmes-official/acme.sh
```

然后运行安装程序，根据需要更新你的目录和电子邮件地址。

```
/root/acme.sh --install -m my@email.com
```

## 使用 webroot 模式创建证书

- 1. 接下来，让我们注册账户，并将电子邮件地址作为变量传递：

```
/root/acme.sh --register-account -m erik@talesfromthedatacenter.com
[Sun Apr 2 22:02:02 2023] 未找到 EAB 凭据，正在获取一个
[Sun Apr 2 22:02:02 2023] 正在注册账户: https://acme.zerossl.com/v2/DV9
[Sun Apr 2 22:02:03 2023] 已注册
[Sun Apr 2 22:02:03 2023] THUMBPRINT=QU6rxyRkeBPtAhUgnfl1BS9 保存 THUMBPRINT 以供以后使用。此同时也保存在 ./acme.zerossl.com/v2/DV9/ca.conf
```

- 2. 现在，我们可以使用 URL 和主目录运行脚本：



```
[root@letsencrypt #] /root/acme.sh --issue -d ssltest.talesfromdatacenter.com
[Sun Apr 2 22:56:24 2023] 使用 https://acme.zerossl.com/v2/DV9
[Sun Apr 2 22:56:24 2023] 连接到 ssltest.talesfromdatacenter.com
[Sun Apr 2 22:56:24 2023] 正在获取每个名的令牌
[Sun Apr 2 22:56:24 2023] 正在验证 ssltest.talesfromdatacenter.com
[Sun Apr 2 22:56:24 2023] 正在验证 de-challenge.zerossl.com
[Sun Apr 2 22:56:24 2023] 正在等待订单，请稍候。(1/30)
[Sun Apr 2 22:56:24 2023] 完成，开始验证
[Sun Apr 2 22:56:24 2023] 正在完成订单。
[Sun Apr 2 22:56:24 2023] 订单状态：https://acme.zerossl.com/v2/DV9/Na6is84pt-gFCQ/
[Sun Apr 2 22:56:24 2023] 订单正在处理，等待并重试。
[Sun Apr 2 22:56:24 2023] 轮询订单状态：https://acme.zerossl.com/v2/DV9/Na6is84pt-gFCZQ
[Sun Apr 2 22:56:24 2023] -Challenge="https://acme.zerossl.com/v2/DV9/cert/7I8gJTCB_FtgWRw"
```

图9. 要安装的证书

脚本将重启 Apache。

## 测试

1. 你可以通过 HTTPS 访问站点。你会在地址栏左侧看到一个锁。这显示如下：

### Apache 2 测试页面

此页面用于测试安装后 Apache HTTP 服务器的正常运行。如果你读到此页面，说明在该站点安装的 Apache 服务器工作正常。

### 如果你是普通公众成员：

你看到此页面表明该网站正在遇到问题或进行非计划维护。

如果你想让该网站的管理员知道你看到了此页面或你遇到的问题，你应该给他们发送电子邮件。通常情况下，发送给“webmaster”并指向网站域名的邮件会到达相应人员。

如果你在访问 `www.acme.com` 时遇到问题，应该向 "`webmaster@example.com`" 发送电子邮件。

### 如果你是网站管理员：

你现在可以向 `/var/www/html/` 目录添加内容了。注意，除非你这样做，否则访问你的网站仍将显示此页面。为了防止此页面再次出现，请遵循 `/etc/httpd/conf/welcome.conf` 文件中的说明。

你可以自由在 Apache Linux HTTP 服务器上使用下面的图片。感谢使用 Apache！

![](img/110fa0d6324f0893fff03cee6394144d_311_0.png)

# 工作原理

`acme.sh` 脚本生成一个临时密钥文件并将其放在 `.well-known/acme-challenge` 目录中。然后系统通过互联网查询服务器获取该文件。如果可以获取该文件，就会颁发测试和密钥。监控这一点很重要，因为第三方软件或 SELinux 可能会影响你获取临时密钥的能力。

证书设置好后，最后一个任务是实现刷新。你可以通过添加以下 cron 任务轻松让系统每天检查新证书。注意，你需要根据安装所在的位置调整脚本位置。在此情况下，它安装在 `/home/acme/.acme.sh`。

```
0 * * * /home/acme/.acme.sh/acme.sh --cron /home/acme/.acme.sh > /dev/null
```

## 注意事项

在使用自动更新的密钥时，强烈建议监控站点的 SSL 错误。理想情况下，你应该每小时检查一次 SSL 错误，以防出现故障。查看 Web 服务器的 SSL 日志，并使用 `wget` 或 `curl` 等工具运行检查以验证网站正在运行。

## 加密所有静态数据

加密传输中的数据固然，但你还需要加密静态数据。这在云端尤为重要，因为你正在与其他许多用户共享存储空间。

云提供商可能提供身份加密，但重要的是记住，如果他们能够自动解密数据，那么他们也可以访问密钥。为了真正保护你的数据，你需要使用云提供商无法访问的密钥对数据进行加密。这可以通过 Linux 统一密钥设置 `LUKS` 轻松实现。大型机构还会希望使用 `Clevis`，它允许对由 Tang 服务器管理的密钥进行自动解密。Tang 服务器用于存储和管理加密密钥。在云中，这允许你管理启动加密，而不会让云提供商访问你的密钥。这一过程被称为网络界限加密 `NBDE`。

`NBDE` 是 Oracle Linux 中的一种安全功能，用于在启动过程中提供磁盘加密密钥。`NBDE` 是普通磁盘加密的扩展，使用网络服务器来存储并向本地机器提供加密密钥。与 `LUKS` 结合，这允许使用本地密钥（使用时需要手动密码）和来自 Tang 服务器的自动密钥来解密启动驱动器。这让你既享受到安全自动化启动的便利性，但在紧急情况下，你仍然可以在没有 Tang 服务器的情况下启动。

## 准备工作

与食谱不同，用户将至少需要两个虚拟机：一个作为 Tang 服务器，另一个作为客户端。两个系统都应该更新到最新的软件。

## 如何操作

在本食谱中，我们将执行以下操作：

- 创建一个名为 `tang` 的服务器：

  - 安装并配置 Tang 服务器

- 构建另一个名为 `clevis` 的服务器：

  - 安装并配置 Clevis

  - 使用 Clevis 配置 `LUKS` 以加密数据卷

# 配置 Tang 服务器

Tang 服务器用于 Oracle Linux 在启动过程中提供加密密钥。以下是其运行原理的基本概述：

- 在启动过程中，远程系统联系 Tang 服务器并请求加密密钥

- Tang 服务器生成一个随机加密密钥并返回给远程系统

- 远程系统使用该加密密钥解锁其加密驱动器，允许其启动

- Tang 服务器在提供加密密钥后使其不再被再次使用

使用 Tang 服务器的一个主要优势是，如果主加密密钥泄露，它可以为远程系统提供加密密钥。通过限制主加密密钥泄露可能造成的损害，可以提高系统的安全性。

1. 要以 root 身份安装 Tang 服务器，我们只需使用 `dnf` 安装软件，打开防火墙端口并设置服务器运行。所有操作都由 root 用户完成。

通过 `dnf` 安装非常简单；只需运行以下命令：

```bash
dnf install -y tang
```

2. 我们将向防火墙添加端口。信任的网络将是你启动的子网。在这种情况下，`192.168.56.0/24` 是我的启动子网。在运行以下防火墙命令时，忘记更新子网：

```bash
firewall-cmd --zone=trusted --add-source=192.168.56.0/24
firewall-cmd --zone=trusted --add-service=http
firewall-cmd --runtime --permanent
```

3. 使用以下命令配置服务在启动时启动并启动：

```bash
systemctl enable --now tang.socket
```

你可以通过以下命令验证服务正在运行：

```bash
systemctl status tang.socket
# systemctl status tang.socket
● tang.socket - Tang Server
Loaded: active (/lib/systemd/system/tang.socket; enabled; vendor preset: disabled)
Active: active (listening) since Mon 2023-07-17 13:52:58 EDT; 26m ago
Listen: [::80 (Stream)
Connected: 0
Tasks: 0 (Limit: 46811)
Memory: 0B
CGroup: /system.slice/tang.socket.service[1]
Jul 17 13:52:58 Listening on Tang Server.
```

4. 一旦 Tang 运行，`/var/db/tang` 中就会有密钥。你可以运行 `tang-show-keys` 命令。这将显示系统中所有密钥的指纹：

```bash
[root@tang]# tang-show-keys
RdxdbjAY7_N19UEBO6XIVosVoss
[root@tang]#
```

接下来，让我们使用 `LUKS` 设置客户端以加密数据驱动。

# 设置 LUKS

1. 首先，使用以下 `dnf` 命令安装所需的包：

```bash
dnf -y install cryptsetup clevis clevis-luks clevis-dracut
```



## 2. 对原始数据设备进行加密
通过加密整个设备，卷的所有元数据以及实际数据本身都会被加密。我们有 `/dev/sdb`，这是一个 20 GB 的小设备。你可以通过使用 `lsblk` 命令检查所有块来看：

```bash
[root@clevis ~]# lsblk
NAME MAJ MIN RM RO TYPE MOUNTPOINT
sda 8:0 0 100G disk
  ├─sda1 8:1 0 72.9G part /boot
  └─sda2
    ├─ol-root 252:0 0 5G lvm /
    ├─ol-swap 252:1 0 5G lvm
    ├─ol-var 252:2 0 5G lvm /var
    └─ol-home 252:3 0 5G lvm /home
sdb 8:16 0 20G disk
```

## 3. 使用以下命令加密 `/dev/sdb`
```bash
cryptsetup luksFormat --type luks2 --cipher aes-xts-plain --key-size 512 --hash sha256 --use-random --force /dev/sdb
```

警告：这将删除设备上的所有数据。这将不可逆地覆盖 `/dev/sdb` 的数据。确定吗？（输入 'yes'）

输入 `/dev/sdb` 的密码：

## 4. 解锁设备
接下来，使用之前保存的命令解锁设备：
```bash
cryptsetup --verbose luksOpen /dev/sdb cryptisk
```
解锁后，你应该能在 `/mapper/` 中看到设备：

## 5. 创建文件系统并挂载点
现在可以使用 `/mapper/cryptisk`。情况下，创建 `xfs` 文件系统：
```bash
mkfs.xfs /mapper/cryptisk
```
我们将创建一个挂载点：
```bash
mkdir /data
```

## 6. 获取磁盘 UUID
要使用该磁盘，我们需要通过 `blkid` 命令获取磁盘的 UUID。该 UUID 将标识磁盘：
```bash
[root@clevis ~]# blkid -s UUID /mapper/cryptisk
/mapper/cryptisk: UUID=589f051-243-4c4f-a4f-62d9f
```

## 7. 配置重启时挂载
使用以下命令在重启时挂载文件系统：
```bash
echo "UUID=589f051-243-4c4f-a4f-62d9f /data xfs defaults 0" | sudo tee -a /etc/fstab
```

## 8. 挂载磁盘
现在可以使用以下命令挂载磁盘：
```bash
mount /data
```

## 9. 使用 Clevis 绑定密钥
接下来，我们需要使用以下命令通过 `Clevis` 将密钥绑定到设备。我们将通过命令行传递设备和 Tang 服务器信息。你需要 LUKS 密码将密钥添加到 Tang：
```bash
[root@clevis ~]# clevis bind -d /dev/sdb tang '{"url":"http://tang.local"}'
警告：值 512 超出范围，正在调整。包含以下签名密钥：
RdxdbjAY7_N1UEBO6vos
你想信任这些密钥吗[yn] Y
输入现有 LUKS 密码：
```
现在我们可以查看 LUKS 密钥，如屏幕所示，插槽 1 已填充了密钥：
```bash
[root@clevis ~]# cryptsetup luksDump /dev/sdb

LUKS header information

Version: 2

Epoch: 5

Metadata area: 16384 [bytes]

Keyslots area: 16744448 [bytes]

UUID: 218eeb5c-2508-4e34-a569-1e8d378384e

Label: (no label)

Subsystem: (no subsystem)

Flags: (no flags)

Data segments:

0: crypt

  offset: 16777216 [bytes]

  length: (whole device)

  cipher: aes-xts-plain64

  sector: 512 [bytes]

Keyslots:

0: luks2

  Key: 512 bits

  Priority: normal

  Cipher: aes-xts-plain64

  Cipher key: 512 bits

  PBKDF: argon2id

  Time cost: 8

  Memory: 1048576

  Threads: 4

  Salt: 49 2d 90 9e 2b 08 2e 3f fa f8 f5 4f 56 53 39

    6f 03 42 f1 e6 d9 5e 31 bf 24 e8 7c 18 19 30 81

  AF stripes: 4000

  AF hash: sha256

  Area offset: 32768 [bytes]

  Area length: 258048 [bytes]

  Digest ID: 0

1: luks2

  Key: 512 bits

  Priority: normal

  Cipher: aes-xts-plain64

  Cipher key: 512 bits

  PBKDF: pbkdf2

  Hash: sha256

  Iterations: 1000

  Salt: 7b 50 80 17 64 f9 77 2d 9f 2c 5b 93 ea 1d f3

    76 bc 7b a1 3d 78 bc 03 4b 08 4e 25 51 20 e8

  AF stripes: 4000

  AF hash: sha256

  Area offset: 290816 [bytes]

  Area length: 258048 [bytes]

  Digest ID: 0

Tokens:

0: clevis

  Keyslot: 1

Digests:

0: pbkdf2

  Hash: sha256

  Iterations: 153108

  Salt: 55 90 39 20 30 7f 5e 31 5c 35 c7 0f 0b 0c 8a 11 47

    c8 ea 8b bd2 09 2e 53 a0 6d a1 d7 1f 8f 99 cd 6b

  Digest: 7b ea cc d1 2e 53 a7 bf 26 b0 d0 a2 3c 13 2d

    57 26 97 c7 0e 45 27 07 64 42 51 bb aa fd ba
```

![](img/110fa0d6324f0893fff03cee6394144d_317_0.png)

## 10. 配置启动时解密驱动器
接下来，我们需要配置设备以便启动时解密驱动器。我们首先需要获取加密驱动的新 UUID：
```bash
root@clevis ~# blkid -s UUID /dev/sdb
/dev/sdb UUID="218ec8bc-2508-4e34-a569-1e8d3783874e"
```

## 11. 启用 Clevis 服务
接下来，让我们启用 Clevis 服务：
```bash
systemctl enable clevis-luks-askpass.path
```

## 12. 更新 `/etc/crypttab`
现在，我们需要将内容添加到 `/etc/crypttab`。`crypttab` 文件包含所有加密驱动器的列表：
```bash
echo "encryptedUUID 218ec8bc-2508-4e34-a569-1e8d3783874e _netdev" | sudo tee -a /etc/crypttab
```

## 13. 更新 `/etc/fstab`
接下来，我们将更新文件系统的 `/etc/fstab` 文件，将默认选项改为 `_netdev`。这将允许设备在其他非加密文件系统之后挂载。

## 14. `/etc/fstab` 示例
`/etc/fstab` 应该类似于下面的截图，其中加密驱动器的 UUID 挂载为 `_netdev`：
```bash
root@clevis ~# more /etc/fstab

# /etc/fstab

# Created by anaconda on Tue Apr 4 15:07:11 2023

# Accessible filesystems, are maintained under '/dev/disk/'.

# See man pages fstab(5), findfs(8), mount(8) and or blkid(8) for more info.

# After editing the file, run 'systemctl daemon-reload'

# units generated from the file.

/dev/mapper/ol-root / xfs defaults 0 0

UUID=801b816a-e6c9-c364-4c1c-1960901fe222 /home xfs defaults 0 0
```



```bash
/dev/mapper/ol-home /home xfs defaults 0 0

/dev/mapper/ol-var /var xfs defaults 0 0

/dev/mapper/ol-log /var xfs defaults 0 0

/dev/mapper/ol-swap none swap defaults 0 0

UUID=5ecf63f1-f2d4-4c32-af1f-62d2e3eb390f /data xfs _netdev 0 0
```

```
root@clevis ~#
```

![](img/110fa0d6324f0893fff03cee6394144d_317_1.png)

# 工作原理

`Clevis` 和 `Tang` 都是软件工具，用于在 Linux 系统启动过程中自动解锁和解密驱动器。

以下是它们工作原理的简介：

- 1. 在启动期间，此提示会要求用户输入密码以解锁并解密磁盘。
- 2. 通过 `Clevis` 和 `Tang`，此提示被一个自动化过程取代，该过程使用基于网络的密钥来解锁和解密磁盘。
- 3. `Clevis` 和 `Tang` 协同工作，在加密磁盘和密钥服务器之间建立绑定。这种绑定基于一种指定了磁盘解锁解锁的策略。
- 4. 当系统启动时，它会连接密钥服务器并请求加密磁盘的解密密钥。密钥服务器检查策略以判断是否满足解锁磁盘的条件。
- 5. 如果满足策略条件，密钥会将解密密钥发送到系统，然后由系统来解锁并解密磁盘。
- 6. 如果不满足策略条件，密钥服务器将拒绝解密请求，磁盘保持锁定。

# 更多功能

可选，你也可以修改系统允许管理员在系统启动时手动输入初始密码。要进行此操作，请安装 `clevis-dracut`：

```bash
dnf install -y clevis-dracut
```

然后，重建启动文件：

```bash
dracut -fv
```



系统启动时，你有机会手动输入密码![](img/110fa0d6324f0893fff03cee6394144d_318_0.png)

图 9.9 – 手动输入

现在你拥有了一个自动解密的加密文件系统，以及紧急情况下的手动方法。

# 验证合规性

保护系统远比加密静态或传输中的数据得多。应该检查许多配置文件，以及其他常用设置。这可以通过安全内容协议 (SCAP) 文件完成。SCAP 是一个用于自动化计算机系统维护的标准框架。它是一套标准化的方法，能够在 IT 基础设施中实施一致且可重复的安全实践。SCAP 定义了一种用于通信相关信息的通用语言，允许不同供应商的安全工具无缝工作。它包含一套用于创建和共享安全内容的标准和指南。

## 准备工作

执行此操作最简单的方法是 OpenSCAP，它带有：

- `scap-workbench`: GUI
- `openscap-scanner`: 扫描
- `openscap-utils`: 通用工具

## 如何操作

执行此操作最简单的方法是通过以下方式安装 OpenSCAP `scap-workbench`

一旦安装了 OpenSCAP，你有两种方式运行它：GUI 或命令行。如果你使用 GUI，可以通过以下方式启动![](img/110fa0d6324f0893fff03cee6394144d_319_0.png)

接下来，选择你想要使用的配置![](img/110fa0d6324f0893fff03cee6394144d_320.png)

图 9.10 – 启动 Workbench

| 标题 | 定制化 | 目标 | 规则 |
| :--- | :--- | :--- | :--- |
| ANSI-BP-028 | none | enhanced | 170 |
| ANSI-BP-028 | high | high | 184 |
| ANSI-BP-028 | intermediary | medium | 160 |
| ANSI-BP-028 | minimal | low | 44 |
| CJIS Security Policy | | | | 105 |
| ASCC Essential Eight | | | | 95 |
| HIPAA | | | | 140 |
| General Purpose OS | | | | 205 |
| PCI-DSS v3.2 | | | | 125 |
| Standard System Profile | | | | 78 |
| DISA STIG | | | | 404 |

向执法人员提供准确且及时的信息，帮助他们破案和预防犯罪，同时确保信息的隐私和安全。

- NIST-800 指的是由美国国家标准与技术研究院（NIST）开发的一系列信息安全指南和标准。NIST-800 系列包含了一系列出版物，为信息安全的各个各个方面提供指导，例如风险管理、安全控制和事件响应。NIST-800 系列广泛用于政府机构、私营部门组织和其他，以提高其信息系统的安全性。该系列出版物定期更新，以反映威胁格局的变化和安全技术的进步。

- ACSC：澳大利亚网络安全中心（ACSC）是一个政府机构，负责增强澳大利亚政府、企业和社区的网络能力和韧性。ACSC 建立于 2014 年，是澳大利亚信号局（ASD）的一部分。

- HIPAA：《美国健康保险可携带性与责任法案》（HIPAA）是美国的一项保护医疗信息的联邦法律。该法律为保护个人健康相关信息的隐私和安全制定了标准。HIPAA 包括对保护电子受保护健康信息（ePHI）的特定要求，ePHI 是电子形式存储或传输的健康信息。

- PCI-DSS：支付卡行业数据安全标准（PCI-DSS）是由主要信用卡公司建立的一系列安全标准，确保访问信用卡数据的组织能够保护持卡人数据的机密性和完整性。PCI-DSS 旨在减少数据泄露和信用卡欺诈的风险。

- STIG：STIG 代表安全技术实施指南（Security Technical Implementation Guide），是由美国国防信息系统局（DISA）的一的一指南，用于保护国防部（DoD）使用的信息系统和软件。STIG 提供了详细信息，说明如何配置和维护各种技术以满足安全要求，并确保系统能够加固防御网络攻击。

在选择标准时，你可以使用默认的通用标准（例如用于 Oracle Linux 8 的标准系统安全配置文件，路径为：https://stig.open-scan.com/ssg-guide/ssg-ol8-guide-standard.html）或与工作负载匹配的标准。例如，对于医疗行业，HIPAA 可能是合适的标准。如果你处于美国联邦政府生态系统中，即使在国防部之外，STIG 也被广泛使用。一旦选定了标准，你就有几个额外的选项，如下面的截图所示。你可以选择本地或远程机器，以及一个修复角色。修复角色允许系统在可能的情况下自动解决问题，但任何管理员在使用时都应加小心。这是因为许多标准可能会破坏系统功能。在修复问题时务必小心，特别是对于更严格的标准，例如 STIG 和 CJIS。

# Oracle Linux 8 安全配置指南

| 标题 | 未选择 |
| :--- | :--- |
| 配置文件 | 适用于 Oracle Linux 8 的带 GUI DISA STIG (402) | 自定义 |
| 目标 | 本地机器 | 远程机器 (通过 SSH) |
| 规则 | 展开全部 |

- 安装 AIDE
- 构建并测试 AIDE 以验证审计工具
- 配置 AIDE 扫描详情的通知
- 配置 AIDE 以验证访问控制列表 (ACLs)
- 配置 AIDE 以验证扩展属性
- 审计工具必须由 Root 组所有
- 审计工具必须由 Root 所有
- 审计工具的模式必须为 0755 或更宽松的
- 启用 Dracat FIPS 模式
- 禁用 FIPS 模式
- 设置内核参数 `crypto.fips_enabled=1`
- 配置 BIND 使用系统加密策略
- 配置系统加密策略
- 配置 GTLS 库使用 DoD 批准的 TLS 加密
- 配置 Kerberos 使用系统加密策略
- 配置 Libres 使用系统加密策略
- 配置 OpenSSL 库使用系统加密策略
- 配置 OpenSSL 库使用 TLS 加密

| 0% (0 个结果，已选择 402 条规则) |
| 生成修复角色 | 运行测试 | 获取远程资源 | 修复 | 扫描 |

图 9.12 – 扫描设置

一旦你做出选择，请点击**扫描**。

取决于所使用的标准，扫描运行最快几几秒，也可能超过 20 分钟。
扫描完成后，你可以使用 GUI 查看结果：

# ssg-ol8-ds.xml - SCAP Workbench

文件帮助

| 标题 | Oracle Linux 安全配置指南 |
| :--- | :--- |
| 自定义 | 未选择 |
| 配置文件 | 适用于 Oracle Linux 8 的带 GUI DISA STIG (402) | 自定义 |
| 目标 | 本地机器 | 远程机器 (通过 SSH) |

- 规则
- 通过空密码禁用 SSH 访问
- 禁用 GSSAPI 认证
- 禁用 Kerberos 认证
- 禁用 SSH Root 
- 禁用 SSH 对用户已知主机的支持
- 禁用 X11 转发
- 不允许 SSH 环境变量
- 启用严格模式检查
- 启用 SSH 警告横幅
- 启用 SSH 打印最后日志
- 强制频繁会密钥协商
- 仅使用 FIPS 140-2 验证的密钥交换算法
- SSH 服务器使用熵种子 防止远程主机连接到代理显示
- SSSD 中的证书状态检查
- 在 SSSD 中启用 Certmap
- 在 SSSD 中启用智能卡
- SSSD 具有正确的信任锚
- 配置 SSSD 离线凭据过期
- 安装 installguard 软件包
- 启用 USBGuard 服务

100% (402 个结果，已选择 402 个)

| 清除 | 保存结果 | 生成修复角色 | 显示报告 |

处理完成！

图 9.13 - 扫描结果

所有的修复涉及更改简单的设置。某些可能需要额外的文件或内核设置。要查看某项发现的详情，只需展开结果，如下屏所示：

- 禁用 X11 转发
`X11Forward` 参数提供了通过连接隧道 X11 流量的能力，当启用 X11转发时。默认 SSH 配置禁用了 X11转发。要显式禁用 X11转发，请在 `/etc/ssh/sshd_config` 中添加或修改以下行：`X11Forward`

- 不允许环境变量 用户不允许覆盖 SSH 守护进程的环境变量

- 启用严格模式检查
- 启用 SSH 警告横幅
- 启用 SSH 打印最后日志
- 强制频繁密钥协商

# 端口保护和限制网络访问

Oracle Linux 内置了防火墙。该防火墙被称为 `firewalld`，是 firewall daemon 的缩写。`firewalld` 是 Linux 系统上的一种动态防火墙管理工具，为跨发行版提供了简单且一致的防火墙规则管理方法。它允许管理员以灵活高效的方式管理防火墙规则。

大多数安装情况下它是默认启用的。要检查守护进程的状态，可以使用 `systemctl` 命令如下：

```
```



`systemctl status firewalld`

输出如下屏所示：

```bash
[root@ol8 ~]# systemctl status firewalld

* firewalld.service - firewall dynamic daemon

Loaded: loaded (/usr/lib/systemd/firewall.service; enabled; vendor preset: enabled)

Active: active (running) since Tue 2023-04-04 22:23:14 EDT; 1min 10s ago

Main PID: 841 (firewall20)

Tasks: 2 (limit: 4020)

Memory: 941.0M

CGGroup: /system.slice/firewall.service

-541 /usr/libexec/platform-python -s /usr/sbin/firewalld --nofork --nopid
```

Apr 04 22:23:13 ol8.m57.local systemd[1]: Starting firewall - dynamic daemon...

图 9.16 - 防火墙状态

## 如何操作...

你可以使用 `firewall-cmd` 的 `--list-all` 选项查看当前配置：

```bash
[root@ol8 ~]# firewall-cmd --list-all
```

这将向你显示信息：

```text
[root@ol8 ~]# firewall-cmd --list-all
public (active)
target: default
icmp-block-inversion: no
interfaces: enp0s3 enp0s8
sources:
services: cockpit dhcpv6-client ssh
ports:
protocols:
forward: no
masquerade: no
forward-ports:
source-ports:
icmp-blocks:
rich rules:
```

图 9.17 - `firewall-cmd --list-all`

上述命令的输出显示了 Linux 系统上由 `firewalld` 管理的活动防火墙规则和配置的全面摘要。输出分为几个部分：

- `public (active)`：此行显示活动防火墙区域的名称，在本例中，该区域为公用区域（public）。`Target: default` 存在，这表示这是默认区域且当前正处于激活状态。
- `interfaces`: enp0s3 enp0s8：此行显示分配给活动防火墙区域的网络接口。在本例中，enp0s3 和 enp0s8 接口都被分配到了公用区域。
- `sources`：此行显示允许访问防火墙区域的 IP 地址或网络范围。如果没有定义源，此行将为空。
- `services`: cockpit dhcpv6-client ssh：此行列出允许访问防火墙区域的服务。在本例中，允许进入 cockpit、dhcpv6-client 和 ssh 服务的入站流量。
- `ports`：此行显示允许访问防火墙区域的 TCP 和 UDP 端口。如果没有定义端口，此行将为空。
- `protocols`：此行显示在协议级别管理的协议，例如 TCP/UDP/ICMP。
- `forward`: no：此行指示防火墙区域是否启用了转发功能。
- `masquerade`: no：此行指示防火墙区域是否开启了伪装（masquerade）。伪装允许来自一个网络的数据包看起来像是来自另一个网络网络。
- `forward-ports`：此行显示为防火墙区域定义了哪些转发端口。转发端口允许特定端口的入站流量重定向到不同的端口或 IP 地址。
- `source-ports`：此行显示为防火墙区域定义的任何源端口。源端口允许来自特定端口的入站流量重定向到不同的端口或 IP 地址。
- `icmp-blocks`：此行显示防火墙拦截的任何互联网控制消息协议（ICMP）数据包。ICMP 数据包用于网络诊断和故障排除。
- `rich rules`：此行显示为防火墙区域定义的任何规则。富规则（Rich rules）允许使用类似于 iptables 语法来定义更复杂的规则。

添加新规则非常简单。可以使用服务名称（在 `/etc/services` 中找到）或端口号添加规则。最常见的任务是添加常用的用户服务，例如 mysql。这通过在命令中添加 `--add-service` 选项来实现。添加服务后，除非添加 `--permanent` 选项，否则配置在重启后不会生效。一些常见示例如下：

```bash
firewall-cmd --permanent --add-service=http
firewall-cmd --permanent --add-service=imap
firewall-cmd --permanent --add-service=pop
firewall-cmd --permanent --add-service=mysql
```

此外，你可以指定允许服务的协议和端口。以下是添加 TCP 或 UDP 端口的示例：

```bash
firewall-cmd --permanent --add-port=1521/TCP
firewall-cmd --permanent --add-port=6900/UDP
```

你也可以使用 `--remove-port` 或 `--remove-service` 选项移除端口或服务：

```bash
firewall-cmd --permanent --remove-service=pop
firewall-cmd --permanent --remove-port=6900/UDP
```

完成更改后，你需要重新加载防火墙规则。这通过 `--reload` 选项实现：

```bash
firewall-cmd --reload
```

# 工作原理...

`firewall` 基于 `netfilter` 框架，该框架是一组钩子（`hooks`），允许内核对网络包进行过滤。该框架用于在许多 Linux 系统上实现 `iptables` 防火墙。`firewall` 提供了更高层次的抽象，允许管理员通过服务、端口和协议定义规则，而不是直接操作 `iptables`。`firewall` 的优势之一是允许根据区域（`zones`）来定义规则，每个区域都有特定的安全级别。

## 保持 SELinux 激活

`SELinux`（Security-Enhanced Linux）是一个提供强制访问控制（MAC）策略的内核模块。它通过限制进程可以的操作增加了额外的安全层。本教程将介绍如何创建自定义 `SELinux` 策略而不是禁用它，以及如何允许服务绑定低端口（`<1024`）。

## 准备工作

与其他测试一样，我们需要一个 Linux 系统进行操作。系统默认启用。要查看 `SELinux` 状态，可以使用 `getenforce` 命令。该命令将返回当前状态：

- `enforcing`：`SELinux` 处于激活并拦截活动
- `permissive`：`SELinux` 已启用，但不拦截活动
- `disabled`：`SELinux` 已禁用

如果你通过 `dnf` 安装了 `setools`，则可以使用额外的命令：

```bash
dnf install setools-console
```

你还应该使用 `sestatus` 命令获取有关 `SELinux` 的更多信息：

```text
[root@localhost8]# sestatus
SELinux status: enabled
SELinux mount: /sys/fs/selinux
SELinux root directory: /etc/selinux
Loaded policy name: targeted
Mode: enforcing
Mode from config file: enforcing
Policy MLS unknown status: allowed
Memory protection checking: actual (secure)
Max kernel policy version: 31
```



你可以使用 SELinux 类型来管理资源。SELinux 类型是用于对系统中各种资源的标签，例如进程、文件、目录和网络端口。SELinux 类型是 SELinux 安全策略的重要组成部分，因为它们决定了哪些进程和用户可以访问特定的资源。

有多种 SELinux 类型，包括：

- 用户类型（User types）：用于定义用户的安全上下文。它们还用于限制用户对系统上特定资源的操作。
- 角色类型（Role types）：用于定义角色的安全上下文。它们也用于限制用户对系统中特定资源的操作。
- 域类型（Domain types）：用于定义进程的安全上下文。系统上的每个进程都分配有一个唯一的域类型，该类型决定了进程可以访问的哪些资源。
- 类型强制类型（Type enforcement types）：用于定义文件或目录的安全上下文，并限制进程对特定资源的操作。

网络端口类型：网络端口类型用于定义网络端口的安全上下文。网络端口类型用于限制对系统特定端口或服务的网络访问。

除了这些类型外，SELinux 还使用了一些特殊类型，例如 `unconfined_t` 类型，它用于未受 SELinux 限制的进程；以及 `system_u` 和 `root_t` 类型，它们用于系统资源和进程。

## 如何操作

可以使用 `setenforce` 命令配合参数 `1` 或 `0` 动态更改 SELinux 的状态。使用该命令会将 SELinux 置于强制模式（enforcing），而使用 `0` 则将其置于允许模式（permissive）。

此外，你可以编辑配置文件 `/etc/selinux/config`，并将 `SELinux` 字段设置为三种状态中的一种。这是禁用 SELinux 的唯一方法。

虽然对于许多管理员来说，禁用 SELinux 很有诱惑力，但可以很容易进行更新以允许所需的操作。

SELinux 默认情况下会将日志记录到 `/var/log/audit/audit.log` 文件中。

# 工作原理

SELinux 有多个层级的安全机制来管理文件、端口和内核模块。它们都由 `semanage` 命令进行管理。

## semanage

`semanage` 是一个用于在 Linux 系统中管理 SELinux 策略的命令行工具。它用于创建、修改或删除 SELinux 策略，以及管理文件上下文和网络端口。以下是 `semanage` 命令的一些常见用途：

- `semanage` 可用于管理文件上下文，包括为特定文件或目录添加或修改上下文。例如，你可以使用以下添加新的策略模块：

```
semanage module -a kernelmodule.pp
```

这将策略模块 `kernelmodule.pp` 添加到 SELinux 策略中。

- `semanage fcontext -a -t httpd_sys_content_t '/var/www/html/(.*)'`
这将添加一个新的文件上下文，允许 HTTPD 进程访问 `/var/www/html` 下的文件和目录。

- `semanage` 可用于管理网络端口和服务，包括添加或修改端口类型和策略。例如，你可以使用以下命令定义新的端口类型：

```
semanage port -a t www2 -p tcp 8080
```

这将为 TCP 端口 8080 添加新的端口类型 `www2`。

- `setsebool`：SELinux 布尔变量，可以启用或禁用以控制特定的安全策略。通过更改这些变量的值，使用 `setsebool` 命令来启用或禁用 SELinux 策略。一个实用的例子是为 Web 服务器将 `httpd_can_network_connect` 设置为 `true`：

- 要查看 SELinux 策略的状态，使用 `getsebool` 命令。该命令显示启用或禁用某些策略的布尔变量。要查看所有值，使用 `-a` 选项。或者，你可以传递特定值进行检查，例如所示：

```
getsebool httpd_can_network_connect >> off
```

## SELinux fixfiles

SELinux fixfiles 是一个用于恢复文件和目录 SELinux 文件上下文的命令行工具。SELinux 使用文件上下文来确定哪些进程和用户可以访问系统上的特定文件或目录。当文件上下文更改或损坏时，可能会导致系统功能或安全性问题。`fixfiles` 命令用于将 SELinux 上下文恢复默认值。当你遇到文件访问问题或 SELinux 相关的错误时，这非常有用。以下是 `fixfiles` 命令的一些常用方法：

- 恢复目录的默认文件上下文：要恢复特定目录的默认文件上下文，你可以使用：

```
fixfiles restore /directory_to_fix
```

这将递归恢复指定目录内所有文件和目录的默认上下文。

- 恢复整个系统的默认文件上下文：要恢复整个系统的默认文件上下文，运行命令：

```
fixfiles restore
```

这将恢复系统上所有文件和目录的默认上下文。注意，这可能需要一些时间，并可能对系统功能造成临时中断。

- 验证文件上下文：你可以使用该命令验证特定文件或目录的上下文：

```
matchpathcon /file_to_verify
```

这将显示指定文件或目录的预期的文件上下文。如果显示的上下文与实际上下文不符，你可以使用 `fixfiles` 命令恢复默认上下文。

## 注意

如果 SELinux 曾被禁用过一段时间，那么这些上下文在未运行期间将不会被设置。有一个快捷方法可以让 SELinux 重新标记整个文件系统层级：`# touch /.autorelabel`

现在重启机器。当 SELinux 启动，它将为每个类型和位置设置所有文件和安全上下文的默认值。

## SELinux 用户

SELinux 用户是用于分类 Linux 系统中不同类型用户的标签。SELinux 用户是 SELinux 安全策略的重要部分，用于将用户的操作限制在系统上的特定资源集上。

有几种类型的 SELinux 用户：

- 系统用户（System users）：由系统定义的系统用户，用于运行系统服务或守护进程。这些用户通常被分配唯一的 SELinux 用户标签，用于将操作限制在系统上的特定资源集。
- 登录用户（Login users）：由系统定义的登录用户，用于登录系统。这些用户通常被分配唯一的 SELinux 用户标签，用于将用户的操作限制在系统上的特定资源集。
- 工作人员用户（Staff users）：由系统定义的工作人员，用于工作人员。这些用户通常被分配唯一的 SELinux 用户标签，用于将操作限制在系统上的特定资源集。
- 用户定义用户（User-defined users）：由系统定义的用户定义用户。这些用户通常被分配唯一的 SELinux 用户标签，用于将操作限制在系统上的特定资源集。

以下是一些常用的 SELinux 命令：

## 如何操作

AppStreams 非常于使用。要开始使用，通常最好是检查可用模块列表。这可以通过终端/控制台中输入一个简单的命令 `dnf module list` 来完成：

```bash
$vagrant@localhost~$ dnf module list

Last metadata expiration check: 0:10:24 ago on Mon 05 Dec 2022 05:18:04 AM UTC.

Oracle Linux 8 Application Stream (x86_64)
```



| 流 (Stream) | 配置文件 (Profiles) |
| :--- | :--- |
| 389-ds | 1.4 common [d] |
| an | 0.1 [d] common [d] |
| container-tools | 1.0 [d] common [d] |
| container-tools | 2.0 common [d] |
| container-tools | 3.0 common [d] |
| container-tools | 4.0 common [d] |
| eclipse | 0.10 java [d] |
| freeradium | 2.8 [d] server [d] |
| gimp | common [d], devel |
| go-tool | 0.2 [d] devel, minimal |
| httpd | common [d], common [d], dscr |
| id | 0.1 common |
| inkspace | client [d] adfrut, client |
| javapackages-runtime | 0.23 [d] common [d] |
| mc | common core |
| liblinux-python | 0.2 [d] common [d] |
| lime-toolkit | 0.8 [d] common [d] |
| log4j | 2 [d] common [d] |
| mailman | 2.1 [d] common [d] |
| mariadb | 10.3 [d] client, server [d] |
| mariadbDB | 10.5 client, server [d] |

![](img/110fa0d6324f0893fff03cee6394144d_334_0.png)

输出将继续列出一长模块列表，在最后，你将看到字母含义的键映射：

| 模块 (Module) | 版本 (Version) | 配置文件 (Profiles) |
| :--- | :--- | :--- |
| ruby | 2.2 [d] | common [d] |
| ruby | 2.6 [d] | common [d] |
| ruby | 2.7 | common [d] |
| ruby | 3.0 [d] | common [d] |
| ruby | 3.4 [d] | common [d] |
| rust-toolset | 0.1 [d] | common [d] |
| satellite-client | 0.6 [d] | common [d], gui |
| scale | 2.1 [d] | URL client packages |
| squid | 0.4 [d] | A hybrid functional/object |
| subdivision | 1.10 [d] | Apache Server |
| swig | 3.8 [d] | common [d] |
| swig | common, complete | C++/Objective C |
| varnish | 6.0 [d] | Varish HTTP cache |
| virt | 0.1 [d] | Virtualization module |

![](img/110fa0d6324f0893fff03cee6394144d_334_1.png)

这里有几个可能会引起你注意的模块：`container-tools`, `gimp`, `go-tools`, `inkscape`, `mariadb`, `mysql`, `nginx`, `nodejs`, `python`, 以及 `php`。这些都是模块，但你会注意到每个模块都有一个流（stream），该流包含一个配置文件（profile）。如果我们用图表将其视觉化，它可能会像这样：

![](img/110fa0d6324f0893fff03cee6394144d_335_0.png)

图 10.3 – AppStreams 可视化

接下来，假设我们想获取某个特定模块的信息。在这种情况下，让我们来看 `nodejs`。首先，我们在请求列表时指定 `nodejs`。我们可以通过在 `list` 命令后添加模块名称来实现，如下所示：

```bash
[root@localhost ~] dnf module list nodejs
Last metadata expiration: 0:10:45 ago on Fri 16 Dec 2022 09:29:29 PM.
Oracle Linux 8 Application Stream Profile
nodejs      10 (d) common [d], development [d]
nodejs      12 [d] development, minimal [d]
nodejs      14 [d] development, minimal [d]
nodejs      16 [d] development, minimal [d]
nodejs      18 [d] development, minimal [d]
```

在列表底部，你将看到：[d]default（默认）、[e]enabled（已启用）、installed（已安装）。由此我们可以看到流 10 被标记为 `nodejs` 的默认流 [d]。这意味着什么？基本上，如果我们运行 `dnf module install nodejs`，我们将得到流 10 中最新版本的 Node.js（且流 10 与 Node.js 相关）。

在编写本文时，流 10 中最新版本的 Node.js 是 `nodejs-10.24.0-module+e8.3.0`。我们可以通过输入以下内容来进一步深入了解这个特定的 AppStream：

```bash
# dnf module info nodejs:10
```

该命令的输出将显示流 10 中所有可用的 Node.js 版本。有很多，但为了简洁起见，我粘贴了列表最后两个：

![](img/110fa0d6324f0893fff03cee6394144d_335_png)

```text
Name : nodejs
Stream : 10 [d]
Version : 10.24.0.181969
Context : 29f0ac6
Architecture : x86_64
Profiles : common [d], development, minimal [d]
Default options : common
Repo : old_appstream
Summary : JavaScript runtime
Description : Node.js 是一个构建在 Chrome JavaScript 运行时上的平台，可以使其变得轻量化
Requires : platform[e18]
Artifacts : nodejs-10.23.1-module+e18.0+9642+879023
nodejs-10.23.1-module+e18.0+9642+879023
nodejs-docs-10.24.0-module+e18.3+9671+1543738
nodejs-full-1010.23.1-module+e18.3+9671+1543738
nodejs-nodemon-0.1.18.3-module+e18.1+5392+4d6b561f
nodejs-packaging-0.17.3-module+e18.1+5392+4d6b561f
npm:6.64.11-10.23.1-module+e18.3+9642+879023.x86_64
Name : nodejs
Stream : 10 [d]
Version : 10.24.0.2310265
Context : 29f0ac6
Architecture : x86_64
Profiles : common [d], development, minimal [d]
Default options : common
Repo : old_appstream
Summary : JavaScript runtime
Description : Node.js 是一个构建在 Chrome JavaScript 运行时上的平台，可以使其变得轻量化，但对于数据密集型应用
Requires : platform[e18]
Artifacts : nodejs-dev-10.24.0-module+e18.3+9671+1543738
nodejs-docs-10.24.0-module+e18.3+9671+1543738
nodejs-full-1010.24.0-module+e18.3+9671+1543738
nodejs-nodemon-0.1.18.3-module+e18.1+5392+4d6b561f
```



![](img/110fa0d6324f0893fff03cee6394144d_336_png)

这里有趣的是，流 10 中的每个 Node.js 版本都是 [d]默认的、[e]已启用的。

```bash
[root@localhost ~#] dnf install nodejs:10/development

Last metadata expiration check: 00:51:12 on Fri 16 Jun 2022 07:04:33 PM UTC.

Dependencies resolved.

=================================================================================

Package                 Arch Version                    Repository       Size

=================================================================================

Installing group: modules/nodejs

nodejs                   86_64 18.24.0-1.el8.3+9671+15433c8  ol8_stream       8.8 M

nodejs-devel           x86_64 18.24.0-module.el8.3+9671+15433c8  ol8_stream       164 k

npm                     x86_64 16.14.11-10.24.0.1.module.el8.3+9671+15433c8  ol8_stream       3.7 M

Installing dependencies:

annobin                x86_64 10.6.7-10.el8               ol8_stream       955 k

ndz                    x86_64 0.12-10.el8               ol8_stream       189 k

efi-srpm-macros       x86_64 3.0-1.el8                 ol8_stream       22 k

gpg-srpm-macros        x86_64 1.4-2.el8                 ol8_stream       9.5 k

ng2-crypto-libs       x86_64 1.2.2-2.el8                 ol8_stream       106 k

keyutilsis-libs-dev      x86_64 15.1-9.el8               ol8_latest       48 k

krbs5-dev             x86_64 18.1-14.0.1.el8             ol8_latest       560 k

libcc-devel           x86_64 14.5-6.4.el8               ol8_latest       38 k

libuuid               x86_64 2.10-20.1.el8             ol8_latest       179 k

liblinux-dev          x86_64 2.9-5.el8                 ol8_latest       200 k

libspol-dev           x86_64 2.9-3.el8                 ol8_latest       87 k

libverto-dev          x86_64 0.3-5.el8                 ol8_latest       35 k

node-utils            x86_64 18.1-module.el8.3+5392+d60b51f  ol8_stream       28 k

caml-srpm-macros      x86_64 5.4-2.el8                 ol8_stream       9.3 k

openblas-srpm-macros  x86_64 2-2.el8                   ol8_stream       7.9 k

open-devel            x86_64 1.11.14.6-5.el8             ol8_stream       31 k

prcre2-ut1            x86_64 10.32-6.el8             ol8_latest       605 k

prcre2-ut2            x86_64 10.32-6.el8             ol8_latest       229 k

prcre2-ut3            x86_64 10.32-6.el8             ol8_latest       220 k

perl-macros           x86_64 5.32-1.el8                ol8_stream       13 k

python-rpm-macros      x86_64 3.4-1.el8                 ol8_stream       16 k

python-srpm-macros    x86_64 3.4-1.el8                 ol8_stream       15 k

python3-rpm-macros    x86_64 3.4-1.el8                 ol8_stream       15 k

qt5-devel             x86_64 5.15-1.el8                ol8_stream       11 k

redhat-rpm-config      x86_64 129.1-6.el8               ol8_stream       89 k

rust-srpm-macros      x86_64 5.0-2.el8                 ol8_stream       9.2 k

unzip                  x86_64 6.0-40.1.el8             ol8_latest       190 k

zip                   x86_64 3.0-23.el8                ol8_latest       28 k

Installing module profiles:

nodejs/development:

Enabling module streams:

nodejs

10

Transaction Summary

Install 31 Packages

Total download size: 19 M

Is this ok [y/N]: █
```



你可以指定多行内容，如例所示：
`# dnf module install nodejs:10/development nodejs:10/s`

输出结果如下截图所示：
```
[root@localhost vagrant]# dnf module install nodejs:10/development nodejs:10/s
Last metadata check: 52:40 ago on Fri 16 Jun 2022 07:04:33 PM UTC.
Dependencies resolved.

| Package | Arch | Version | Repository | Size |
| --- | --- | --- | --- | --- |
| Installing group/packages: | | | | |
| nodejs | x86_64 | 11.24.0-1.el8.3.9671+15433c | ol8_appstream | 8.8 M |
| nodejs-dev | x86_64 | 11.24.0-module.el8.3.9671+15433c | ol8_appstream | 164 k |
| nodejs-nodemon | noarch | 1.3.0-module.el8.5141+52e2 | ol8_stream | 96 k |
| npm | x86_64 | 16.14.11-10.24.0.1.module.el8.3+9671+15433c | ol8_stream | 3.7 M |
| Installing dependencies: | | | | |
| annobin | x86_64 | 10.6.7-10.el8 | ol8_stream | 955 k |
| efi-srpm-macros | x86_64 | 3.0-1.el8 | ol8_stream | 22 k |
| gpg-srpm-macros | x86_64 | 1.4-2.el8 | ol8_stream | 9.5 k |
| perl-macros | x86_64 | 5.32-1.el8 | ol8_stream | 13 k |
| krbs5-dev | x86_64 | 18.1-14.0.1.el8 | ol8_latest | 560 k |
| libcc-devel | x86_64 | 14.5-6.4.el8 | ol8_latest | 38 k |
| libuuid | x86_64 | 2.10-20.1.el8 | ol8_latest | 179 k |
| liblinux-dev | x86_64 | 2.9-5.el8 | ol8_latest | 200 k |
| libspol-dev | x86_64 | 2.9-3.el8 | ol8_latest | 87 k |
| libverto-dev | x86_64 | 0.3-5.el8 | ol8_latest | 35 k |
| node-utils | x86_64 | 18.1-module.el8.3+5392+d60b51f | ol8_stream | 28 k |
| caml-srpm-macros | x86_64 | 5.4-2.el8 | ol8_stream | 9.3 k |
| openblas-srpm-macros | x86_64 | 2-2.el8 | ol8_stream | 7.9 k |
| open-devel | x86_64 | 1.11.14.6-5.el8 | ol8_stream | 31 k |
| prcre2-ut1 | x86_64 | 10.32-6.el8 | ol8_latest | 605 k |
| prcre2-ut2 | x86_64 | 10.32-6.el8 | ol8_latest | 229 k |
| prcre2-ut3 | x86_64 | 10.32-6.el8 | ol8_latest | 220 k |
| python-rpm-macros | x86_64 | 3.4-1.el8 | ol8_stream | 16 k |
| python-srpm-macros | x86_64 | 3.4-1.el8 | ol8_stream | 15 k |
| python3-rpm-macros | x86_64 | 3.4-1.el8 | ol8_stream | 15 k |
| qt5-devel | x86_64 | 5.15-1.el8 | ol8_stream | 11 k |
| redhat-rpm-config | x86_64 | 129.1-6.el8 | ol8_stream | 89 k |
| rust-srpm-macros | x86_64 | 5.0-2.el8 | ol8_stream | 9.2 k |
| unzip | x86_64 | 6.0-40.1.el8 | ol8_latest | 190 k |
| zip | x86_64 | 3.0-23.el8 | ol8_latest | 28 k |

Installing module profiles:
nodes/common
nodes/development
nodes/62

Enabling module streams:
nodes
10

Transaction Summary

32 Packages

Total download size: 20 M
Installed size: 60 M
Is this ok y/N]: _
```

Figure 10 – Output of `dnf module install nodejs:10/development nodejs:10/s`

或者如果你想安装所有配置，可以使用星号来选择：
`# dnf module install nodejs:10/*`

输出结果如下：
```
[root@localhost vagrant]# dnf install nodejs:*
```

## 使用 AppStreams 安装不同版本的软件

现在，我们将扩展对 AppStreams 的了解。我们不再从默认的模块流（`module stream`）安装应用程序，而是将指定一个不同的流。

## 如何操作...

有多种方法可以实现此点：只需指定安装不同的流即可完成任务，或者你可以手动启用不同的版本。我更倾向于在安装时指定版本，因为在这种情况下，AppStream 会自动启用该版本：

```bash
# dnf module install nodejs:16
```

## 注意

如果你已经安装了某个版本的 AppStream，最好在重置并安装不同版本之前删除旧版本。这将在稍后介绍。

输出如截图所示：



```
[root@localhost vagrant#] dnf module install nodejs:16
Last metadata expiration: 00:03:32 ago on Fri 16 Jun 2022 09:05:16 PM UTC.
Dependencies resolved.
=================================================================================
Package      Arch        Repository                Size
=================================================================================
Installing group/module packages:
nodejs        x86_64      1:16.18-3.module+el8.7+20893+df13f383  ol8_appstream    12 M
pm          x86_64      1:8.19-2.16.18.3.module+el8.7+20893+df13f383  ol8_appstream    2.0 M
Installing module profiles:
nodejs/common
Enabling module streams:
nodejs        16
Transaction Summary
=================================================================================
Install 2 Packages
Total download size: 14 M
Installed size: 49 M
This operation will be performed.
Downloading Packages:
(1/2) npm-8.19.2-1.16.18.3.module+el8.7+20893+df13f383.x86 7.4 MB/s | 2.0 MB 00:00
(2/2) nodejs-16.18.1-3.module+el8.7+20893+df13f383.x86_64.r 20 MB/s | 12 M 00:00
Total
Running transaction check
Transaction-check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
Running scriptlet: npm-8.19.2-1.16.18.1.3+module+el8.7+20893+df13f383.x86_64 1/2
Preparing:
Installing: npm-8.19.2-1.16.18.1.3+module+el8.7+20893+df13f383.x86_64 1/2
Installing: nodejs-16.18.1-3.module+el8.7+20893+df13f383.x86_64 2/2
Running scriptlet: nodejs-16.18.1-3.module+el8.7+20893+df13f383.x86_64 2/2
Verifying:
Verifying: npm-8.19.2-1.16.18.1.3+module+el8.7+20893+df13f383.x86_64 2/2
Verifying: nodejs-16.18.1-3.module+el8.7+20893+df13f383.x86_64 2/2
Installed:
nodejs-1:16.18.1-3.module+el8.7+20893+df13f383.x86_64
npm-1:8.19.2-1.16.18.3.module+el8.7+20893+df13f383.x86_64

Complete!
```

图 10.11 – `dnf module install nodejs:16` 的输出

你从提示中看到 `nodejs` 16 的模块流将被启用。现在，如果我们列出 `nodejs` 的模块流，我们将看到以下内容：

```
[root@localvagrant]# dnf module list nodejs
Last metadata expiration check: 00:03:03 ago on Fri 16 Dec 2022 09:05:16 PM UTC.
Oracle Linux 8 Application Stream (x86_64)
Name         Stream   Summary
nodes      10 [d] common (d), development, minimal, s21 Javascript runtime
nodejs      12       common (d), development, minimal, s21 Javascript runtime
nodejs      14       common (d), development, minimal, s21 Javascript runtime
nodejs      16 [e]    common (d), development, minimal, s21 Javascript runtime
nodejs      18       common (d), development, minimal, s21 Javascript runtime
Hint: [d]enabled, [e]disabled, [i]installed
```

### 10.12 `dnf module list nodejs` 的输出

如你所示，10 是默认的，16 是启用的 (e)。AppStreams 维护了一个默认流，允许用户在不需要了解 AppStreams 任何知识的情况下正常使用。此外，如果我们重置模块，它将恢复到原始设置——这将使 10 成为默认并启用，而 16 不再被启用。此外，重要的是，一次只能启用一个流。如果你启用了不同的流，它将是唯一可以安装的流，但很容易重置并切换到另一个。要此这样做，只需执行以下操作：

```bash
# dnf module remove nodejs
# dnf module reset nodejs
```

你将看到关于模块重置的确认：

```
Disabling module profiles:
nodes/common
Resetting modules:
nodes
```

此时，我们可以安装不同的版本了。这次我们选择 Node.js 14：你将看到关于包管理器计划执行操作的确认：



```
[root@localvagrant]# dnf install nodejs:14
Last metadata expiration check: 00:04:57 ago on Fri 16 Dec 2022 09:05:16 UTC.
Dependencies resolved.
Package      Arch      Version                               Repository      Size
Downgrading:
nodejs       x86_64    1.14.20-1.module+el8.6+20874+33892dc  ol8_appstream  11 M
npm           x86_64    1.14.20-1.2.module+el8.6+20874+33892dc  ol8_appstream  3.7 M
Installing modules:
nodes/common
Enabling module streams:
nodejs       14
Transaction Summary
Downgrade 2 Packages
Total download size: 15 M
Is this ok (y/N):
Downloading packages:
(1/2) nodejs-1-6.14.17-14.20.1.module+el8.6+20874+33892dc.x86_64 7.8 MB / 3.7 MB 00:00
(2/2) nodejs-npm-1-6.14.20-1.2.module+el8.6+20874+33892dc.x86_64 18 MB / 11 MB 00:00
Total                  23 MB / 15 MB   00:00
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
Running scriptlet: npm-1-6.14.17-14.20.1.module+el8.6+20874+33892dc.x86_64 1/1
Preparing:
Installing: nodejs-1-6.14.17-14.20.1.module+el8.6+20874+33892dc.x86_64 1/1
Downgrading: nodejs-1-6.14.20-1.module+el8.6+20874+33892dc.x86_64 1/4
Cleanup: npm-1-18.19.2-18.1.module+el8.7+2093+df1f383.x86_64 2/4
Cleanup: nodejs-1-6.14.20-1.2.module+el8.7+2093+df1f383.x86_64 3/4
Running scriptlet: npm-1-18.19.2-18.1.module+el8.7+2093+df1f383.x86_64 4/4
Verifying:
Verifying: nodejs-1-6.14.20-1.module+el8.7+2093+df1f383.x86_64 4/4
Verifying: nodejs-1-6.14.20-1.2.module+el8.7+2093+df1f383.x86_64 2/4
Verifying: npm-1-18.19.2-18.1.module+el8.7+2093+df1f383.x86_64 3/4
Verifying: nodejs-1-6.14.20-1.2.module+el8.7+2093+df1f383.x86_64 4/4
Downgraded:
nodejs-1:6.14.20-1.module+el8.6+20874+33892dc.x86_64
npm-1:6.14.20-1.2.module+el8.6+20874+33892dc.x86_64
```

### 图 10.13 – `dnf module switch-to nodejs:16` 的输出

你应该看到`10`是默认的，`16`是启用的 (e)。AppStreams 维护了一个默认流，允许用户在不需要了解 AppStreams 任何知识的情况下正常使用。此外，如果我们重置模块，它将恢复到原始设置——这将使`10`成为默认并启用，而`16`不再被启用。此外，重要的是，一次只能启用一个流。如果你启用了不同的流，它将是唯一可以安装的流，但很容易重置并切换到另一个。要此这样做，只需执行以下操作：

```bash
# dnf module remove nodejs
# dnf module reset nodejs
```

你将看到关于模块重置的确认：

```
Disabling module profiles:
nodes/common
Resetting modules:
nodes
```

此时，我们可以安装不同的版本了。这次我们选择 Node.js `14`：你将看到关于包管理器计划执行操作的确认：



```
[root@localhost vagrant]# dnf install nodejs:14
Last metadata expiration check: 00:04:57 ago on Fri 16 Dec 2022 09:05:16 UTC.
Dependencies resolved.
Package      Arch      Version                               Repository      Size
Downgrading:
nodejs       x86_64    1.14.20-1.module+el8.6+20874+33892dc  ol8_appstream  11 M
npm           x86_64    1.14.20-1.2.module+el8.6+20874+33892dc  ol8_appstream  3.7 M
Installing modules:
nodes/common
Enabling module streams:
nodejs       14
Transaction Summary
Downgrade 2 Packages
Total download size: 15 M
Is this ok (y/N):
Downloading packages:
(1/2) nodejs-1-6.14.17-14.20.1.module+el8.6+20874+33892dc.x86_64 7.8 MB / 3.7 MB 00:00
(2/2) nodejs-npm-1-6.14.20-1.2.module+el8.6+20874+33892dc.x86_64 18 MB / 11 MB 00:00
Total                  23 MB / 15 MB   00:00
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
Running scriptlet: npm-1-6.14.17-14.20.1.module+el8.6+20874+33892dc.x86_64 1/1
Preparing:
Installing: nodejs-1-6.14.17-14.20.1.module+el8.6+20874+33892dc.x86_64 1/1
Downgrading: nodejs-1-6.14.20-1.module+el8.6+20874+33892dc.x86_64 1/4
Cleanup: npm-1-18.19.2-18.1.module+el8.7+2093+df1f383.x86_64 2/4
Cleanup: nodejs-1-6.14.20-1.2.module+el8.7+2093+df1f383.x86_64 3/4
Running scriptlet: npm-1-18.19.2-18.1.module+el8.7+2093+df1f383.x86_64 4/4
Verifying:
Verifying: nodejs-1-6.14.20-1.module+el8.7+2093+df1f383.x86_64 4/4
Verifying: nodejs-1-6.14.20-1.2.module+el8.7+2093+df1f383.x86_64 2/4
Verifying: npm-1-18.19.2-18.1.module+el8.7+2093+df1f383.x86_64 3/4
Verifying: nodejs-1-6.14.20-1.2.module+el8.7+2093+df1f383.x86_64 4/4
Downgraded:
nodejs-1:6.14.20-1.module+el8.6+20874+33892dc.x86_64
npm-1:6.14.20-1.2.module+el8.6+20874+33892dc.x86_64
```

## Python 如何？

如果你查看模块列表，你可能会注意到 Python 是由多个模块组成的，而不是单个 AppStreams 模块：

```bash
# dnf module list python*
```

输出如下截图所示：

```
[root@localhost vagrant]# dnf module list python*
Last metadata expiration check: 00:09:33 on Sun 23 Jul 2023 02:11:44 AM UTC.
Oracle Linux 8 Application (x86_64)
Name    Stream                  Summary
python27 2.7 [d]         common [d]         Python programming language, version 2.7
python36 3.6 [d]         build, common [d]  Python programming language, version 3.6
python38 3.8 [d]         build, common [d]  Python programming language, version 3.8
python39 3.9 [d]         build, common [d]  Python programming language, version 3.9
Hint: [d]default, [e]enabled, [x]disabled, [i]installed
```

![](img/110fa0d6324f0893fff03cee6394144d_346_0.png)

图 10.15 – `dnf module list python` 的输出

这初看起来似乎很奇怪，请考虑到 Python 是 Oracle Linux 操作中不可或缺的一部分，并且每个 Oracle Linux 版本都附带有一个平台 Python 版本。特定的平台 Python 版本可能根据每个 Oracle Linux 版本而有所不同，并且相应的平台 Python将在该版本 Oracle Linux 的整个生命周期内都获得支持。对于 Oracle Linux 7，平台 Python 版本为 2.7 且始终已安装；对于 Oracle Linux 8，平台 Python 版本为 3.6。换句话说，Python 2.7 支持 Oracle Linux 7 的整个生命周期，而 Python 3.6 则支持 Oracle Linux 8 的整个生命周期。在 Oracle Linux 8 上，平台 Python 专门供 Yum 和 DNF 等系统工具使用。对于通用用途，Oracle Linux 8 默认不安装 Python，这正是 AppStream 模块大显用场的地方。

你可以通过指定与所需 Python 版本相关的模块，在 Oracle Linux 8 上安装多个版本的 Python。所有 Python 模块都可以在同一台机器上同时安装和使用，你可以通过输入版本号来指定你想使用的哪一个——例如，`python3.6 --version`、`python3.8 --version` 等。

默认情况下，如果系统中安装了 Python 3，则 `python3` 命令始终指向 Python 3.6，这是因为 Python 3.6 是 Oracle Linux 8 平台 Python 版本。

## 通过 AppStream 移除软件包

通过 AppStream 移除软件包非常简单。通常情况下，你只需要指示包管理器执行移除而不是安装即可。如果包管理器找到匹配的模块，它将继续移除相关软件包。

## 如何操作……

基于上一个食谱中的示例，让我们通过运行 `dnf module remove nodejs` 命令来移除 Node.js 模块：



### 图 10.16 – `dnf module remove nodejs` 的输出

```
[root@localhost vagrant]# dnf module remove nodejs
Last metadata expiration check: 0:09:52 ago on Fri 16 Dec 2022 09:05:16 PM UTC.
Dependencies resolved.
=================================================================
Package Arch    Repository                Size
=================================================================
Removing:
nodejs x86_64    1.14.20-2.module+el8.6.0+20874+338992dc @ol8_appstream 37 M
nps   x86_64    1.14.17-1.14.20.1.2.module+el8.6.0+20874+338992dc @ol8_appstream 15 M
Disabling module profiles:
nodejs/common
=================================================================
Transaction Summary
=================================================================
Remove 2 Packages
Freed space: 52. M
Is this ok [y/N]: 
```

从此消息中，你可以看到 `NPM` 将卸载，但考虑到 `Node.js` 模块安装的不只是 `NPM`，这并不是你预期的。如果你想移除与该模块相关的所有内容，你需要传递 `--all` 标志，如下所示：

```bash
# dnf module remove nodejs --all
```

这一次，你将看到所有关联软件包都已进入移除队列：



```
[root@localhost vagrant#] dnf remove nodejs
Last metadata expiration check: 0:07:49 ago on Fri 16 Jun 2022 09:29:29 UTC.
Dependencies resolved.
=================================================================================
Package             Arch    Version                                     Repository Size
=================================================================================
Removing:
nodejs              x86_64  14.20.1-2.module+el8.6+20874+38992dc @appstream             37 M
nodejs-dev           x86_64  14.20.1-2.module+el8.6+20874+38992dce @appstream             967 k
nodejs-packaging    noarch   23-3.0.module+el8.3.78+cd3085                   41 k
srpm                x86_64  16.4-17.1.2.module+el8.6+20874+38992dc @ol8_appstream 15 M
Removing unused dependencies:
minobin            x86_64  10.8-3.0.el8                               @appstream             968 k
rotl-devel       x86_64  0-3.10.el8                               @appstream             53 k
dwz                x86_64  0.12-10.el8                               @appstream             225 k
efi-rpm-macros     noarch   3-3.0.el8                               @appstream             38 k
gnc-rpm-macros     noarch   1.4-2.7                                     appstream             414 k
gd                 noarch   3-2                                        appstream             33 k
keyutils-libs      x86_64  11.5-9.10                            @appstream_basest_latest 33 k
krb5-devel          x86_64  11.80-14.1.el8                            @appstream_basest_latest 1 M
libcrypt-devel       x86_64  1.45-14.10                           @appstream_basest_latest 1 M
libblkid           x86_64  11.16-24.1.el8                            @appstream             219 k
libselux-devel     x86_64  2.9-5.el8                               @appstream             127 k
libepsol-devel      x86_64  6.4-3.el8                               @appstream             127 k
libreadline-macros  noarch   3-3.5.el8                               @appstream             35 k
nocaml-rpm-macros    noarch   5-4.el8                               @appstream             37 k
openblas-rpm-macros noarch   2-2.el8                               @appstream             104 k
openssl-devel       x86_64  1.1.1k-6.el8_5                            @appstream             3.4 M
pcre2-devel          x86_64  10.32-2                            @appstream_latest 1.8
pcre2-utf1         x86_64  10.32-2                            @appstream_latest 570
pcre2-utf2          noarch   3-2.el8                               @appstream_latest 780
perl-rpm-macros     noarch   3-4.el8                               @appstream             4.2
python-rpm-macros   noarch   3-4.el8                               @appstream             5.1
python3-rpm-macros  noarch   5.15.3.el8                            @appstream             3.6
qt5-rpm-macros      noarch   0                                      @appstream_basest_latest 429 k
redhat-rpm-macros   noarch   129-1.0.el8                           @appstream_basest_latest 149
rust-rpm-macros     noarch   5-2.el8                               @appstream             1.1
zip                  x86_64  6.0-46.1.el8                            @appstream_basest_latest 422 k
```

## 有...

那么，既然我们已经涵盖了 `AppStream` 的用法，你可能会问自己：“我们以前不是已经通过 `Software Collections` 有类似的功能了吗？”答案是肯定的，但 `Software Collections` 和 `AppStream` 之间存在巨大的差异。

`Software Collections` 提供了并行可用（`Parallel Availability`）和并行安装（`Parallel Installability`），而 `AppStream` 只提供并行可用。

根据 Fedora 文档，*并行可用意味着热门软件项目有多个主版本供安装。*而*并行安装意味着可以在同一个用户空间中安装一个软件项目的多个主版本。*

现在你可能会问：“等等，所以你是在告诉我 `AppStream` 并不像我们之前的工具那样好？”嗯，确实如此。事实证明，并行安装并没有想象中那么好。虽然从表面上看在同一个系统上安装多个版本的软件似乎很不错，但它充满了复杂性，需要用户知道要做一些额外的操作才能使用已安装的软件或备用版本。例如，如果你想安装多个版本的 `Node.js`，你首先需要启用相应的 `Software Collection`，然后你还需要知道该去哪里查找并激活你想使用的特定版本。换句话说，你无法以普通方式直接使用备用版本，因为软件包将安装在非标准位置。

# 狮子、老虎与容器——噢我的天！Podman 及其朋友们



如今，容器就是一切。Docker 让容器变得酷起来并将其带入主流，而 Podman 则作为一个对所有人开放且可用的开源容器运行时出现，前来解救。Oracle Linux 7 包含了用于 Docker 的 Oracle 运行时，而 Oracle Linux 8 及更高版本则包含了 Podman、Buildah 和 Skopeo。

随着每一个新版本的发布，Podman 都在缩小它与 Docker 之间的差距。从 Podman v2.0 开始，它开始提供完全兼容的构建，使得 `docker-compose` 等技术可以与 Podman 切换使用。通过 Podman v4.1.0，你现在能够无缝地将机器的主目录挂载到 Podman VM 中，使其在卷挂载中变为可用。本章主要面向具有 Docker 基础经验的用户，并将帮助用户理解 Docker 和 Podman 之间的差异，以便他们成功地将工作负载迁移到这个所谓的“无缝替换品”。如果你不熟悉 Docker 或对容器概念比较陌生，阅读来自 Docker 的[入门指南]可能会有所帮助，你可以在此处找到：https://docs.docker.com/get-started/。

在本章中，我们将涵盖以下食谱：

- 使用 Podman 告别恶魔——呃，是守护进程（daemons）
- 为你的容器 root 权限
- 创建方便实用的工具容器
- Podman 下的 Docker Compose
- 使用 pod 管理栈（stacks）
- 容器化数据库
- Buildah 和 Skopeo – Podman 的“额外福利”朋友

## 技术要求

Podman、Buildah 和 Skopeo 均包含在应用流的 `container-tools` 模块中：

```bash
$ sudo dnf module install container-tools
```

本章中食谱的源代码可以在此处找到：

https://github.com/PacktPublishing/Oracle-Linux-Cookbook。

## 使用 Podman 告别恶魔——呃，是——守护进程

Docker 和 Podman 都是旨在让在主机上运行和管理容器变得更易的工具。Podman 是该领域的新面秀，你可能想知道如何从 Docker 切换到 Podman。虽然在技术上在同一系统上同时运行 Docker 和 Podman 是可能的，但这样做的实际理由很少。由于这两个工具提供相同的内核功能，我建议你选择其中之一即可。

使用 Podman 的主要优势之一是，你从本质上失去了隐藏在 Docker 后面的守护进程。你依赖于一个处理所有容器管理繁重工作的守护进程。从表面上看可能并不如此，但在涉及这种架构时，有些事情需要注意。

首先，在后台运行额外的守护进程意味着多了一个故障点。如果 Docker 专用守护进程崩溃，你就会丢失所有的容器。额外的守护进程还增加了你的攻击面，而且由于 Docker 守护进程对系统的 root 权限，任何泄露都会让你的系统面临更大的风险。

本食谱旨在驱除这些恶魔——呃，嗯——停止使用 Docker 守护进程。最好的结果是，如果你没有使用 Docker 且只安装了 Podman，你不需要担心任何事情——Podman 默认是无根（rootless）的，并且它利用 `systemd` 来管理你的容器。`systemd` 是一个经过测试的系统级守护进程，提供了一系列系统组件，包括服务和系统管理器、并行能力、日志以及用于管理和维护系统配置的实用。

另一方面，如果你之前在使用 Docker，我们将向你展示如何切换。这非常简单——你只需要做的就是移除 Docker 并安装 Podman。

### 准备工作

运行在 x86-64 位架构上，但 Oracle Linux 和 Podman 也能运行在 Arm 上。然而，重要的是，并不是所有容器都在 Arm 上编译的，反之亦然。尽管如此，使用 x86-64 位 CPU 遵循本指南可能会更容易：

- Oracle Linux
- Podman

### 如何操作...

1. 通过运行以下命令移除 Docker：

```bash
$ sudo dnf remove -y docker-ce docker-cli-cli containerd.io docker-compose-plugin
```

2. 之后，你可以通过以下命令安装 Podman：

```bash
$ sudo dnf module install container-tools
```

3. 如果你之前在使用 Docker，我们将向你展示如何切换。这非常简单——你只需要做的就是移除 Docker 并安装 Podman。

如果你希望这些设置持久化，只需按照之前收到的错误提示操作即可。即编辑 `/etc/sysctl.conf` 文件并追加 `net.ipv4.ip_unprivileged_port_start=80`。

## 创建实用的工具型容器

本教程将展示如何使用 Podman 快速启动容器来完成实用的任务。

本教程将引导你了解如何利用容器创建实用的工具。容器的基本原则鼓励我们让容器只做一件事——即：提供某种形式的工具，不再做其他事情。你不应该创建一个功能过多的容器。尽管如此，大多数容器镜像已经存在并提供了实用的工具。在本教程中，我们将查看具有实际用途的容器示例，并探索如何利用这些工具。

### 准备工作

我们需要以下内容：

- Oracle Linux
- Podman

### 如何操作...

本教程的主要意图是展示我们如何使用容器来实现某些功能，而无需在本地机器上安装额外的软件包。一旦你在本地机器上安装了 Podman，你就可以利用整个实用包和工具的生态系统，而无需安装更多包——相反，你只需要运行一个包含这些包的容器，或者创建一个新容器并安装所需的包。

为什么有人会优于此呢？首先，它允许你尽可能少地在主机上安装包和依赖项。包越越少，你在安全方面的攻击面就越小。此外，你操作系统的仓库可能对某些包有访问限制，或者可能无法访问最新版本。与其费力添加可能不可信的仓库来安装所需的包，为什么不直接启动一个包含你实现特定功能所需的所有内容的容器呢？

在我们尝试挖掘容器的真正潜力之前，我们首先需要讨论几个重要的概念，这会让这个过程变得更容易。

### Entrypoint（入口点）

容器的入口点（entrypoint）定义了容器默认运行的命令。你可以通过指定 `inspect` 命令并将其传递到 `jq` 来提取入口点，从而找到容器的入口点。

首先，如果系统中还没有该镜像，请拉取它：

```
$ podman pull docker.io/pandoc/core
```

现在让我们检查输出并运行 `jq -r` 来查询入口点：

```
$ podman image inspect pandoc/core | jq -r '.[Config.Entrypoint[0]'
```

**额外提示：** 假设我们的电脑没有安装 jq。在这种情况下，我们可以将 `inspect` 的输出传递到包含 jq 的容器中：

```
$ podman image inspect pandoc/core | podman run -i --rm stedolan/jq -r '.[Config.Entrypoint[]]'
```

无论哪种，此命令的输出都是 `/usr/local/bin/pandoc`。这告诉我们默认执行的命令将是 `/usr/local/bin/pandoc`。

有时，容器的入口点可能是一个脚本。例如，你可能会检查入口点并发现它是 `docker-entrypoint.sh`。你可以通过覆盖入口点并使用 `cat` 查看文件内容来获取更多关于该文件的信息。例如，假设我们要检查 `node` 容器镜像：

```
$ podman image inspect node | jq -r '.[Config.Entrypoint[]]'
```

我们会发现入口点是 `docker-entrypoint.sh`。

现在，覆盖入口点以检查该文件的内容：

```
$ podman run --rm --entrypoint=/bin/bash node -c 'cat docker-entrypoint.sh'
```

在这种情况下，输出为：

```
cat: docker-entrypoint.sh: No such file or directory
```

这是因为在 `node` 镜像中，`docker-entrypoint.sh` 文件不在工作目录下；而是在路径中。因此，我们将尝试另一种方法来检查此文件：

```
$ podman run --rm --entrypoint=/bin/bash node -c '$(which docker-entrypoint.sh)'
```

输出如下：

```
#!/bin/sh
set -e

if [ "$1" != "" ]; then
  exec "$1"
fi
```

现在我们已经讨论了重要的概念，我将列出实用工具的示例，然后扩展容器的实用性。

## 超级工具容器

### 使用 pandoc 将 Markdown 文件转换为 docx



在例例中，假设我们有一个想要转换为其他类型的文档。有很多工具可以实现这一点，但我们首先想到的其中一个工具就是 `pandoc`。与其在本地机器上安装 `pandoc`，我只需运行预装了 `pandoc` 的 `pandoc/core` 容器。`pandoc` 容器的入口点是 `/bin/pandoc`。这意味着在指定容器后的任何内容将自动追加到容器内的 `pandoc` 命令之后。

我们可以运行 `pandoc/core --help` 命令来学习如何使用该工具，例如：

```
$ podman run --rm pandoc/core --help
```

通过这些（你也可以在此处查看 man 手：https://linux.die.net/man/1/pandoc），我现在对如何使用 `pandoc` 有了了解。在这种情况下，我可以通过将工作目录挂载到容器中并指定源文档和输出内容，在容器内使用 `pandoc` 命令，例如：

```
$ podman run --rm -v $(pwd)/:data pandoc/core -s input.md -o output.docx
```

由于容器内部的工作目录是 `/data`，并且我已将其挂载到主机系统，如果容器在该目录内创建了新文件，我将在主机系统上找到该输出。酷酷！

### 使用 FFMPEG 修改图像或视频文件

在本例中，我们将像在上一个容器中利用 `pandoc` 一样，在容器内利用 `FFMPEG`。使用 `FFMPEG` 容器特别方便，因为 `FFMPEG` 往往依赖于大量的依赖项，我不希望在本地机器上安装它们。

此外，很棒的是官方的 `FFMPEG` 容器包含了最新版本，而且运行得非常好！

和上一个例子一样，我们可以在 `ghcr.io/linuxserver/ffmpeg` 命令后运行 `--help` 来学习如何使用 `FFMPEG`，例如：

```
$ podman run --rm ghcr.io/linuxserver/ffmpeg --help
```

从输出中（你也可以查看此处维护的页面：https://linux.die.net/man/1/ffmpeg），我可以看到大量的选项，但为了简洁起见，我将解释你如何从容器中使用 `ffmpeg` 来转换容器内的视频，例如：

```
$ podman run --rm -it -v $(pwd):/config \
ghcr.io/linuxserver/ffmpeg \
-ss 00:00:30 -t 5 -i /config/input.mkv \
-vcodec libx264 -crf 30 /config/output.mp4
```

该命令将从视频的第 00 小时 00 分 30 秒（由 `-ss` 指定）开始运行，并录制 5 秒钟（由 `-t` 指定）。随后它将转换视频，输出可以保存在 `/config/output.mp4`。

## 在容器内使用 Node.js

假设我们需要构建一个 Node.js 应用。为了实现这一点，我们将使用 Node 和 `npm`。在第 10 章中，我们讨论了应用流（application streams）的无用性，以及我们如何利用应用流来安装不同版本的 Node.js。嗯，生活中的其他任何事情一样，解决问题的方法不止一种。

与其在你的宿主机系统上安装 Node.js，不如直接利用容器内的 Node.js 呢？`node` 容器包含了 Node 和 `npm`。默认情况下，当你运行 `node` 容器时，你正在执行 `node` 命令，因为这是默认的入口点（`entrypoint`）（你可能回想起我们之前讨论入口点时想过的）。

假设我们想用 `npm` 命令——我们可以通过利用 `bash` 覆盖入口点并在末尾附加命令来实现，但我们还需要知道如何挂载我们的系统：

```
$ podman inspect node | podman run -i --rm sjedolan/node -r '.{Config.WorkingDir}'
```

通过这个，我们可以看到容器内部的默认工作目录是 `null`。这是否意味着我们没有使用我们想要的容器？显然不是，因为我们可以简单地覆盖入口点并将事情掌握在自己手中。在这种情况下，我将把宿主机系统的当前工作目录挂载到 `/app` 目录，并将入口点覆盖为 `bash`，这样我就可以在运行构建 Node.js 应用的 `npm` 命令之前，指示容器切换到 `/app`。操作如下：

```
$ podman run --rm -v $(pwd):/app --entrypoint bash -c 'cd /app && npm run build!'
```

一旦 `npm` 完成构建，你将在宿主机上的一个名为 `./build` 的目录中找到你的应用二进制文件。

但等一下，正如我之前提到的，解决问题的方法不止一种。一种更优雅的实现相同目标的方法是告诉 Podman 你希望工作目录设置在哪里。如果这样做这样做，我们甚至不需要将其设置为入口点——而是直接进入 `npm`。这可以通过 `-w`（或 `--workdir`）命令完成，如下所示：

```
$ podman run --rm -v $(pwd):/app --workdir /app --entrypoint npm run build
```

在我看来，第二种方法更整洁，但最终结果是一样的。

## 运行轻量级 NGINX Web 服务器来预览网页

在这个示例中，我们不妨继续上一个练习，即我们构建的 Node.js 应用。现在由于我们已经构建/编译好了 Node.js 应用，让我们在 NGINX 容器内部托管它。我们可以通过简单将构建目录挂载到 NGINX 容器内的 `/user/share/nginx/html` 目录来实现。

我是怎么知道托管这个特定目录的？在这种情况下，我必须查阅 NGINX 容器的 NGINX 文档。你可以在托管你想要运行容器的任何仓库中轻松找到这类文档。

在本地托管你的构建目录的命令如下：

```
$ podman run --rm --name ol8cookbook -p 80:80 -v $(pwd)/build:/usr/share/nginx/html:ro nginx
```

使用 Podman，无根（rootless）端口的默认设置无法暴露特权端口 80。如果你没有更改此设置，你会看到这样的消息：

```
Error: rootlessport cannot expose privileged port 80, you can add
'net.ipv4.ip_unprivileged_port_start=80' to /etc/sysctl.conf (currently 1024), or choose
a larger port number (>= 1024): listen tcp 0.0.0.0:80: bind: permission denied
```

如果你拥有 root 权限，可以通过以下方式覆盖此设置：

```
$ sudo sysctl net.ipv4.ip_unprivileged_port_start=80
```

或者，你只需选择使用 1024 或更高的端口号。如果容器正在运行，你可以通过 `http://localhost`（如果你使用了 80 端口）或 `http://localhost:8080`（如果你没有使用 80 端口并分配了其他端口）来预览本地网站。

## 与 Podman 使用 Docker Compose

Podman 是一个强大的容器引擎，通常通过命令行界面（CLI）访问，以便于配置和运行容器。使用 CLI 快速启动容器实例或直接访问现有容器非常方便，但如果你需要一次性运行多个容器呢？你仍然可以使用 CLI，但你可能会养成复制粘贴长命令的习惯，这并不是实现可重复启动和部署容器的最理想方式。相反，为什么不使用像 Docker Compose 的工具呢？Docker Compose 允许你以流行的标记语言（YAML）格式将容器应用配置为代码。YAML 设计用于声明式且易于人类阅读。通过 Docker Compose，你可以在单个 `docker-compose.yml` 文件中定义多个容器的属性，包括卷、环境变量、网络信息等。

虽然 Docker Compose 是将容器配置为代码的极佳工具，但重要的是要知道 Docker Compose 是为配合 Docker 而设计的。尽管如此，在配合 Podman 使用 Docker Compose 时，有几点需要注意。

## 准备工作

我们需要以下内容：

- Oracle Linux

- Podman

- Docker Compose

## 如何操作

在这个食谱中，我们将讨论如何配合 Podman 使用 Docker Compose。由于 Compose 通常涉及多个容器和应用，我们需要注意到 Docker Compose 期望调用 Docker（而不是 Podman）。然而，Netavark 是 Podman 的新特性并提供了显著增强，而我在基于 CNI 的栈中遇到过问题。要切换网络栈，只需在 `/usr/share/containers.conf` 文件中指定 `netavark`。你可以通过以下命令快速实现：



```bash
sudo sed -i 's/network_backend = "cni"/network_backend = "netavark"/g' /usr/share/containers.conf
sudo podman info | grep Backend
```

如果你的系统中已有容器，你需要运行 `podman system reset` 来删除现有的镜像、容器、网络和卷。

现在准备就绪，让我们从安装 Docker Compose 开始：

```bash
sudo curl -sL https://github.com/docker/compose/releases/download/v2.20.3/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

顺便，安装 `podman-docker` 包以确保 Podman 被调用为 Docker：

```bash
sudo dnf install podman-docker
```

接下来，我们需要启用 Podman socket：

- 在无根模式下使用 Docker Compose，使用此命令：

```bash
systemctl --user enable --now podman.podman.sock
export DOCKER_HOST=unix://$XDG_RUNTIME_DIR/run/podman/podman.sock
echo 'export DOCKER_HOST=unix://$XDG_RUNTIME_DIR/run/podman/podman.sock' >> ~/.bash_profile
```

- 在根模式下使用 Docker Compose，使用此命令：

```bash
sudo systemctl enable --now podman.podman.sock
sudo export DOCKER_HOST=unix:///run/podman/podman.sock
sudo echo 'export DOCKER_HOST=unix:///run/podman/podman.sock' >> ~/.bash_profile
```

既然 Docker Compose 已准备就绪，我们需要一个 Compose 文件来进行测试。让我们先示例一个 Compose 文件：

```yaml
services:
  portainer:
    image: portainer/portainer-ce
    container_name: portainer
    volumes:
      - $XDG_RUNTIME_DIR/run/podman/podman.sock:/var/run/docker.sock
    ports:
      - "9000:9000"
    restart: unless-stopped
volumes:
  portainer:
    name: portainer
```

图 11.2 – Portainer 的 Compose 文件

在 `docker-compose.yml` 文件中，我们定义让 Docker（或 Podman）运行多容器应用。在创建 `docker-compose.yml` 文件时，我们定义了希望 Podman 创建的服务和卷，并根据喜好配置了服务的各种参数。

# 关于 关于整个 Compose 规范的全面概述，请参阅 https://docs.docker.com/compose/compose-file/

6. 现在，让我们测试一下，看看 Docker Compose 是否可以工作。将 Compose 文件的内容保存为名为 `docker-compose.yml` 的文件。

7. 使用终端，切换到你保存 `docker-compose.yml` 文件的相同目录，并运行以下命令：

```
docker-compose up -d
```

如果一切顺利，你应该会在终端中看到一些活动，表明 Podman 正在下载容器镜像、创建卷（volume），最后它将按照我们在 Compose 文件中定义的方式启动容器。

8. 一旦容器运行，请导航到我们指定的端口以检查它是否按预期工作。执行此操作，请将浏览器指向 http://127.0.0.1:9000。

恭喜你，你现在正在配合 Podman 使用 Docker Compose 了。

## 使用 pods 管理栈（stacks）

通过栈（stacks）保持所有内容的整洁，并为 Kubernetes 准备。

Podman 支持一些 Docker 中不存在的概念。其中一个大概念就是 pods（（组）——所以我猜 Podman 这个名字源于……Podman = Pod Manager（Pod管理器）。在本配谱中，你将学习如何通过通过 Podman 管理栈来保持内容的整洁。我们将通过使用 pods 来实现这一功能。Pod 由一个或多个容器组成。由于 pod 是你在 Kubernetes 中可以创建和管理的最小部署单元，熟悉 pods 将帮助你弥接容器与 Kubernetes 之间的鸿沟。

## 准备工作

我们需要以下内容：

- *Oracle Linux*

- Podman

- Docker Compose

## 如何操作……

在进入配谱之前，我们应该先进一步讨论一下 pods。如之前所述，pods 由一个或多个容器组成。Podman 总是包含一个 infra 容器（基础容器），默认情况下基于 `k8s.gcr.io/pause` 镜像。infra 容器除了睡眠外什么都不做——它确保容器在空闲时继续运行，并持有了来自内核的端口绑定、命名空间（namespaces）和 cgroups。一旦创建了 pod，分配给 infra 容器的属性就无法更改。请记住，任何需要暴露的端口都需要在创建 pod 的初始完成。

在 pod 外部存在一个 `conmon`（容器监控器）实例，它监控容器的主进程。每个容器都有自己的 `conmon` 实例。

下面的图提供了构成 pod 的架构概述。

![](img/110fa0d6324f0893fff03cee6394144d_364_0.png)

## 图 11.3 – pod 的架构概述

以下是与 pods 相关的 Podman 命令：

- 管理 pods

描述：

Pods 是由一个或多个共享相同网络、pid 和 ipc 命名空间的容器组。

用法

`podman pod [command]`

可用命令：

- - clone: 克隆现有的 pod

- create: 创建一个新的空 pod

- exists: 检查本地存储器中是否存在 pod

- inspect: 显示 pod 配置

- kill: 向 pod 中的容器发送指定的信号或 SIGKILL

- logs: 补丁一个或多个容器的日志

- pause: 暂停一个或多个 pods

- prune: 删除所有停止的 pods 及其容器

- ps: 列出 pods

- restart: 重启一个或多个 pods

- rm: 一个或多个 pods

- start: 启动一个或多个 pods

- stats: 显示一个或多个 pod 中容器资源使用统计的实时流

- stop: 停止一个或多个 pods

- top: 显示 pod 中容器的运行进程

- unpause: 取消暂停一个或多个 pods

从前述命令可以看出，你可以使用 Podman CLI 创建 pod 并在 pod 中运行你的容器。

## 手动创建 pod

假设我们想在 pod 内部部署 Wiki.js。Wiki.js 是一个基于 Node.js 构建的开源 Wiki 软件，并依赖数据库后端。换句话说，我们想要一个这样的 pod：

![](img/110fa0d6324f0893fff03cee6394144d_366_0.png)

我们可以通过遵循以下步骤手动构建此 pod：

- 1. 第一步是在 pod 内部创建我们的数据库容器。在执行此操作时，我们需要确保配置了端口映射，以允许进入 3000 端口。

我们将使用 `podman pod` 命令执行此操作：

```
podman pod create -p 3000:3000 wikjs-pod
```

```
podman run -td --pod wikjs-pod --name wikjs-db --env POSTGRES_DB=postgres --env POSTGRES_PASSWORD=wikijsrocks --env POSTGRES_USER=postgres -v wikjs-db-data:/var/lib/postgresql/data postgres
```

- 3. 现在数据库已经启动运行，我们需要在 pod 内部创建应用程序容器。同样，我们将使用 `--pod` 标签以确保容器运行在与数据库相同的 pod 内部：



```
podman run -td --pod --name wikijs --env DB_TYPE=postgres --env
DB_HOST=wikijs-db --env DB_PORT=5432 --env DB_USER=postgres --env
DB_PASS=wikijssrocks --env DB_NAME=postgres ghcr.io/requarks/wiki
```

- 4. 现在应用程序正在运行，请将浏览器指向 `http://127.0.0.1:3000` 以验证它是否按预期工作。

## 自动创建

Podman 允许你手动创建 pods，但 Podman 的另一个酷功能是它原生支持 Kubernetes 清单（manifests）。

编写完整的清单不是本配谱的范围，但我将向你展示如何使用 Podman 生成一个。由于我们在上一个配谱中学习了 Compose 文件，我们将使用它们来生成清单。

- 1. 第一步是在 pod 内部创建我们的数据库容器。在执行此操作时，我们需要确保配置了端口映射，以允许进入 `3000` 端口。

我们将使用 `podman` `pod` 命令执行此操作：

```
podman pod create -p 3000:3000 wikjs-pod
```

```
podman run -td --pod wikjs-pod --name wikjs-db --env POSTGRES_DB=postgres --env POSTGRES_PASSWORD=wikijsrocks --env POSTGRES_USER=postgres -v wikjs-db-data:/var/lib/postgresql/data postgres
```

- 2. 现在我们已经有了 Compose 文件，让我们使用 Docker Compose 部署容器：

```
docker-compose up -d
```

- 3. 一旦容器运行，将浏览器指向 `http://127.0.0.1:3000` 以验证一切一切正常。

- 4. 此时，我们将为刚刚启动的容器生成一个 Kubernetes 清单（名为 `wikijs.yaml`）：

```
podman generate kube -f wikijs.yaml wikijs wikjs-db
```

- 5. 现在清单已经生成，让我们停止刚刚启动的容器：

```
docker-compose down
podman volume prune
```

- 6. 下一步是使用 `podman play kube` 使用清单调回容器，但在此之前，我们需要修复环境变量中的一个主机名。

我们需要这样做的原因是 pod 的名称会被附加到每个名称之后。我们的数据库容器不再是 `wikijs-db`，而将变为 `wikijs-pod-wikijs-db`。如果你查看清单，你会发现 wikijs 配置为连接到名为 `wikijs-db` 的数据库容器，因此我们需要更新 `DB_HOST` 的值并进行更改。

你可以通过 `yq` 命令执行此操作。如果你的电脑上没有安装 `yq`，不用担心，直接使用 `yq` 容器即可：

```
podman --rm -v $PWD:/workdir docker.io/mikefarah/yq e -i '(select(.kind == "Pod").spec.containers[] | select(.name == "wikijs")).env[] | select(.name == "DB_HOST")).value = "wikijs-pod-wikijs-db")' wikijs.yaml
```

- 7. 在你修正了 `DB_HOST` 值后，运行以下命令：

```
podman play kube wikijs.yaml
```

- 8. 验证 pod 正在运行：

```
podman pod ls
podman ps -ap
```

## 注意

请参考“创建实用的工具容器”配谱以获取更多关于如何使用容器作为工具的信息。

## 容器化数据库

本配谱讨论了关于容器化数据库使用的最佳实践。

我们需要准备以下内容：

- Oracle Linux

- Podman

## 如何操作...

容器让数据库在日常应用程序部署中变得更容易处理。虽然这个食谱中没什么可以讨论的，但有一些关于容器化数据库的最佳实践对你来说绝对很有用。

### 只做一件事且只做一件事

容器的核心原则之一是做一件事且只做一件事，同样的原则也适用于容器化数据库。我的什么意思是？首先，你可能倾向启动一个容器化的数据库，随后在该数据库中创建多个模式（schemas）和/或在单个容器中创建多个数据库。假设你有几个需要 MySQL 数据库的应用程序，那么拥有一个单一的 MySQL 容器并为每个容器化应用程序设置独立的数据库模式……似乎是一个好主意……看起来像这样：

![](img/110fa0d6324f0893fff03cee6394144d_370_0.png)

图 11.6 – 容器化数据库不该这样做

这种架构的问题在于它没有很好地遵循“做一件事且只做一件事”的原则。相反，我建议为每个数据库应用需求启动一个单独容器。为该容器命名，使其与其配套的应用程序互补——像这样：

![](img/110fa0d6324f0893fff03cee6394144d_371_0.png)

图 11.7 – 使用容器化数据库的更好方法

例如，假设你有一个需要数据库的 WordPress 容器。在这种情况下，如果你将 WordPress 容器命名为 `wordpress01`，那么你应该将你的 MySQL 容器命名为 `wordpress01-db`。为每个想要运行的数据库运行独立的容器将更容易排除故障，并且能够为你部署的应用程序提供更可靠的架构模型。如果你需要停止一个容器化数据库，你只会影响一个应用程序，而不是通过在一个容器内运行多个数据库来影响所有应用程序。

### 数据存储

在容器中运行数据库时，持久化数据是你需要处理的问题。使用 Podman，你有两个主要选择：卷（volumes）和绑定挂载（bind mounts）。对于卷，Podman 将通过其内部的卷管理系统写入磁盘来管理你的数据库的存储。对于绑定挂载，你需要在主机系统上指定一个位置并将其挂载到容器中。两种选项都可以的，通常卷更容易，因为它们对用户要求的配置较少，但缺点是在主机系统上可能更难找到数据。此外，可能会因为不留心使用 `podman volume prune` 命令而导致卷被意外删除。尽管如此，对于演示或快速测试，我喜欢使用卷，但对于真正重要的持久化数据，我更倾向于使用绑定挂载。

创建卷非常简单。Podman 提供了创建卷的几种方法。你可以使用 `podman volume create [NAME]` 从命令行手动创建卷。你也可以让 Podman 为你完成繁重工作，因为它能够在创建容器期间自动创建卷。如果你指定了卷名称，Podman 可以创建一个具命的卷；例如，运行 `podman run -v my_data:/var/lib/mysql mysql:8-oracle` 将创建一个名为 `my_data` 的卷。如果你省略了 `-v my_data:/data` 规范而改为运行 `podman run -it oracleinux:8`，Podman 也可以创建一个匿名卷。

如果你想使用绑定挂载，你只需要指定该挂载在主机系统上的位置。例如，如果你想将数据存储在 `/mnt/hdd/podman/volumes/`，你只需要将此位置指定为源位置。我更喜欢将其作为名为 `VOLUME_DIR` 的环境变量，以便我可以使用 `$(VOLUME_DIR)` 引用它。当我指定在容器中创建绑定挂载时，我只需使用 `podman run -v $(VOLUME_DIR):/var/lib/mysql mysql:8-oracle`。这将确保我的数据存储在系统上可预测的位置，并且每个容器在路径路径下获得其专用的文件夹。

### 初始化脚本

大多数容器化数据库都提供了一种方便在初始设置后运行脚本的方法，这非常有用。这通常通过允许用户从主机上挂载一个目录来实现，该目录包含 `.sql` 文件或 `entrypoint-initdb.d` 目录。脚本通常按字母顺序执行，因此可以通过添加前缀来轻松控制，例如 `01_users.sql`、`02_permissions.sql`、`03_hostname.sh` 等：

- MySQL 数据库：MySQL 数据库在以下挂载点支持 `*.sh` 和 `*.sql` 脚本：`/entrypoint-initdb.d`

- PostgreSQL 数据库：PostgreSQL 数据库在以下挂载点支持 `*.sh` 和 `*.sql` 脚本：`/entrypoint-initdb.d`

- MongoDB 数据库：MongoDB 数据库在以下挂载点支持 `*.sh` 和 `*.js` 脚本：`/entrypoint-initdb.d`

- Oracle 数据库：Oracle 数据库在以下挂载点支持 `*.sh` 和 `*.sql` 脚本：

    - `/opt/oracle/scripts/setup`



`/opt/oracle/scripts/startup`

## 控制启动

使用 Compose 文件，你可以通过属性控制容器的启动顺序。确保数据库已启动并运行（准备好接受连接）的一种良好方法是对数据库配置健康检查（health check）。一旦健康检查成功，容器将变为健康状态。需要数据库的应用程序可以配置为等待数据库健康后再启动。

```
healthcheck:
  test: ["CMD-SHELL", "pg_isready -U postgres"]
  interval: 10s
  timeout: 5s
  retries: 5
```

一旦健康检查成功，容器将变为健康状态。需要数据库的应用程序可以配置为等待数据库健康后再启动。

```
healthcheck:
  test: ["CMD-SHELL", "mysqladmin ping -h localhost -u root --password=$MYSQL_PASSWORD"]
  interval: 10s
  timeout: 5s
  retries: 5
```

一旦健康检查成功，容器将变为健康状态。需要数据库的应用程序可以配置为等待数据库健康后再启动。

## 整合一切

现在我们已经讨论了这些数据库最佳实践，是时候通过 Compose 文件将它们整合在一起了。WordPress 需要一个数据库，所以在这个 Compose 文件中，我们使用 `depends_on` 选项：

```yaml
depends_on:
  wordpress01-db:
    condition: service_healthy
```

这个 WordPress 网站的配置可能如下所示：

```yaml
services:
  wordpress01:
    image: wordpress
    container_name: wordpress01
    depends_on:
      wordpress01-db:
        condition: service_healthy
    restart: always
    ports:
      - 8080:80
    environment:
      WORDPRESS_DB_HOST: wordpress01-db
      WORDPRESS_DB_USER: mysql
      WORDPRESS_DB_PASSWORD: mysqlpassword
      WORDPRESS_DB_NAME: mysqldb
  wordpress01-db:
    image: mysql:8.0-oracle
    container_name: wordpress01-db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: mysqlrootpw
      MYSQL_USER: mysql
      MYSQL_PASSWORD: mysqlpassword
      MYSQL_DATABASE: mysqldb
    volumes:
      - ./data/init:/container-entrypoint-initdb.d # 初始化脚本
      - wordpress01-db-data:/var/lib/mysql # 数据目录
    healthcheck:
      test: ["CMD-SHELL", "mysqladmin ping -h localhost -u root --password=$$MYSQL_PASSWORD"]
      start_period: 5s
      interval: 5s
      timeout: 5s
      retries: 5
volumes:
  wordpress01-db-data:
```

参考之前关于 Docker Compose 的教程，导航到 `docker-compose.yml` 文件所在的目录，并运行以下命令：

```
docker-compose up -d
```

## Buildah 和 Skopeo – Podman 的“额外福利”

本章的标题提到了 Podman 和朋友。事实上，到目前为止，你可能注意到我们还没有提到过 Podman 的朋友。Podman 带来了几个伴侣来协助你所有的容器管理需求。这些 Podman 的伙伴通常被称为 Buildah 和 Skopeo。

Podman 主要专注于运行容器，而 Buildah 专注于构建容器，Skopeo 则专注于处理镜像以及在镜像本地和远程容器镜像仓库之间进行传输。

## 准备工作

我们需要以下工具：

- Oracle Linux
- Podman
- Buildah
- Skopeo

## 如何操作...

在本教程中，我们将探索 Buildah 和 Skopeo 的基本用法，以揭示这两个 Podman 的“朋友”将如何增强你处理容器时的体验和工作流。

## 使用 Buildah 构建容器镜像

虽然 Podman 可以用于基础的容器镜像构建，但 Buildah 是一个完全专注于构建 OCI 兼容镜像的工具。Buildah 不仅可以从 `Containerfile` 或 `Dockerfile` 构建镜像，还可以几乎修改现有的容器镜像。

首先，让我们看看如何使用 Buildah 从 `Containerfile` 构建镜像。在 Podman 中，我们使用 `podman build -t <image_name>` 来构建镜像。当我们调用 Podman 执行构建时，它实际上是使用 Buildah 功能的子集来构建镜像。要直接使用 Buildah，我们只需要使用稍微不同的命令。例如，假设我们有一个名为 `Containerfile` 的文件，内容如下：

```
FROM oracleinux:8
RUN dnf install -y rhn-setup-yum-utils && dnf clean all
ENTRYPOINT ["/bin/bash"]
```

为了使用 Buildah 进行构建，你需要输入 `buildah bud -t <image_name>`。在这个示例中，我将镜像命名为 `ol-repo-sync`。现在来操作吧：

```
buildah bud -t ol-repo-sync
```

这种情况下的结果与你使用 Podman 执行的结果是一样的。Buildah 真正出彩的地方在于它对运行中的容器进行更改的能力，它还可以从运行中的容器创建新镜像。

为了保持教程的简单，我们将复制 `Containerfile` 中指定的内容，但我们不再直接使用 `Containerfile`，而是使用 Buildah 进行即时操作。让我们对现有的 Oracle Linux 8 镜像进行更改并将其存储为新镜像。首先，我们将运行 `buildah from` 来加载一个运行中的容器：

```
buildah from oracleinux:8
```

这将返回以下输出：

```
oracleinux-working-container
```

这告诉了我们新创建的运行容器的名称。现在我们已经准备好了一个 Buildah 容器，让我们向它添加一些包。在这个示例中，我们将添加之前 `Containerfile` 中指定的相同包。输入以下命令：

```
buildah run oracleinux-working-container dnf -y install rhn-setup yum-utils
buildah run oracleinux-working-container dnf clean all
```

你将看到 DNF 包执行其操作，之后你将得到一个 Oracle Linux 基础镜像加上我们通过 `buildah run` 命令安装的新包。

最后，我们需要在容器容器中定义入口。我们可以通过利用 `buildah config` 来实现：

```
buildah config --cmd '' oracleinux-working-container
buildah config --endpoint ['/bin/bash'] oracleinux-working-container
```

### 注意

在编写时，Buildah 似乎有一个 bug，除非我们先给它一个空值，否则它会填充 `cmd` 值。这可能会导致生成的镜像出现意外行为。根据 Buildah 的文档，在不定义 `cmd` 值的情况下设置 `endpoint` 应该清除任何分配给 `cmd` 的值，但我对 Buildah 1.29.1 版本的测试结果并非如此。为了规这个问题，我发现定义端点之前显式地将 `cmd` 设置为空值是最好的方法。

为了从该容器创建一个新镜像，我们需要运行 `buildah commit` 命令。在这个示例中，我们将其命名为 `ol-repo-sync`，以便与 `Containerfile` 进行对比。



```
buildah commit --rm oracleinux-working-container ol-repo-sync
```

现在我们已经使用 `buildah` 创建了镜像，可以使用 `buildah` 命令检查 `ol-repo-sync`：

```
$ buildah images
```

输出看起来如下：

| REPOSITORY | TAG | IMAGE ID | CREATED | SIZE |
| :--- | :--- | :--- | :--- | :--- |
| localhost/ol-repo-sync | latest | a14 | seconds ago | 279 MB |
| localhost/ol-repo-sync | latest | b25 | 2 minutes ago | 285 MB |
| localhost/ol-repo-sync | latest | c37 | 3 minutes ago | 285 MB |

最后，`Skopeo` 还可以用于从远程仓库或本地容器存储中删除镜像。要执行此操作，只需运行以下命令：

```
skopeo delete containers-storage:pandoc:core:latest
```

# 航行 Ansible 的水域

在本章中，我们将通过几个实例教程来扩展你关于安装 Oracle Linux Automation Manager (`OLAM`)、管理其基础架构、创建剧本（playbooks）、优化这些剧本以及帮助你理解 `OLAM` 功能的知识。每个教程都将让你大开眼界，看到自动化可以实现的全部范围；从补丁到部署完全的混合云环境，`OLAM` 能够改变你对计算的思考方式，让你的思维开启一个“循环往复”的新世界。以下是自动化可以简化的极小部分的触点。

![](img/110fa0d6324f0893fff03cee6394144d_380_0.png)

在本章中，接下来的教程将涵盖 `OLAM` 平台的安装、配置和可用性：

- 安装 `OLAM`
- 快速从基础开始配置和管理 `OLAM`
- `OLAM` 不是幻想足球，但它们都使用剧本
- 控制补丁混乱
- 展望自动化之外的世界
- 设置好后一劳永逸

# 安装 OLAM

自古以来，我们人类人类一直试图让事情变得更简单、更快、更高效。然而，我确定我们大多数人人都听过父母说：“永远不要走捷径”，或者“我小时候小的时候，我必须在雪天里单着一条腿走上坡去学校，来回都是如此。”这些轶事从未改变；随着我们演进到父母的年龄，并试图将我们的智慧传给下一代。那么，如果我告诉你你既可以拥有蛋糕又可以吃掉它呢？自动化是计算的演进和重复任务的自动化。现在，我们不能自动化一切，某些任务并不值得投入自动化的精力，因为它们不可重复的，或者因素的变化到了自动化会破坏流程的程度。

自动化的字典定义是“应用技术、程序、机器人技术或过程，以最少的人为输入来实现结果”。注意“过程”——我们改变、执行或更改结果输出的过程。自动化就是这种过程的变化。我们可以自动化应用程序的安装，例如安装 Microsoft Office 或反病毒软件；自从计算世界的开始起，我们就在自动化这些过程了。现在，我们将自动化推下一个水平。例如 `Ansible Tower`，Red Hat 版本的自动化。`Ansible` 和 `OLAM` 都是基于 `AWX` 构建的，`AWX` 是一个强大且现代的 Web UI 和 API，允许你管理组织的 `Ansible` 剧本、清单、密钥库（vault）和凭据。通过 `AWX`，你可以简化自动化流程并简化基础设施管理任务，所有这一切通过单一、易于使用的界面完成。例如，假设一位大学科学教授每周都必须做准备；实验室有 50 名学生，每个人都需要一个虚拟实验室来参与。教授不想坐在那里每周重建一次实验室环境。使用 `Ansible`，可以汇编一个剧本（不是足球剧本，而是大纲和功能需求）来自动化该实验室环境的创建。通过创建该剧本，工程师可以更改几个变量来改变虚拟机的数量、内存、vCPU 或任何正在使用的资源或应用程序。本质上，`Ansible` 和剧本呈指数级地缩短了创建过程，使其变得可重复，并让教授免于每周重复创建。

`OLAM` 是一个自动化套件，以开源 Linux 发行版（Oracle Linux）的形式捆带，基于 `AWX` 和 `Ansible Tower`。`OLAM` 是一个可配置平台，类似于 `Ansible`，具有创建、管理和更改剧本的能力。`OLAM` 安装时带有 UI（如你在稍后的教程中看到的），还带有 CLI。UI 和 CLI 都是功能完备的，并且与 `Ansible Tower` 相同的所有细粒度，在拥有高级支持订阅的情况下可以免费使用。如图所示，`OLAM` 可用于创建剧本，以自动化多个领域内的流程，从本地虚拟化农场和 HCI 环境到应用程序部署，一直触及到多个云平台和混合云发行版。

![](img/110fa0d6324f0893fff03cee6394144d_382_0.png)

图 12.2 – 剧本层次结构

在本教程中，我们将安装 `OLAM`。与任何安装过程一样，我们需要准备一个基础环境来在上面安装应用程序——在这种情况下是 Oracle Linux 8。不过，建议你安装带有 GUI 的操作系统。我们不会详细介绍上一个教程中涵盖的内容。

## 准备工作

我们将在 Oracle Cloud Infrastructure (`OCI`) 中以虚拟机的形式安装 `OLAM`。请参阅第 3 章和第 4 章关于导航和配置 `OCI` 虚拟机的内容。我们将在以下步骤简要介绍 VM 的创建：

1. 导航到 `OCI` Instances（实例）为 `OLAM` 创建一个主机：
   - 概述
   - 实例
   - 专用主机
   - 实例池
   - 自动伸缩
   - 容量限制
2. 点击**创建实例**以创建虚拟机：
   ![](img/110fa0d6324f0893fff03cee6394144d_382_0.png)
   图 12.3 – 实例
3. 选择镜像：
   ![](img/110fa0d6324f0893fff03cee6394144d_382_0.png)
   图 12.4 – 镜像
4. 选择可用域（Availability Domain）来托管：
   图 12.5 – 可用域
5. 我们将选择 8 GB 内存和 2 个 vCPU。`OLAM` 的最低要求是 2 个 vCPU 和 4 GB 内存：
   ![](img/110fa0d6324f0893fff03cee6394144d_382_0.png)
   图 12.6 – 内存
6. 点击**形状**（Shape）来更改形状：
   图 12.7 – 形状
7. `VM.Standard.E3.FLEX` 形状允许你指定你的资源：
   图 12.8 – 形状选择
8. 我们将选择 8 GB 内存和 2 个 vCPU。
   图 12.9 – VM 资源配置
9. 在配置虚拟机资源后，你必须配置你的访问密钥（公密钥）：
   图 12.10 – SSH 密钥选择
10. 你可以创建、上传、粘贴或继续不使用密钥：

### 添加 SSH 密钥

生成 SSH 密钥对以通过安全外壳 (`SSH`) 连接到实例，或者上传您已有的公钥。

- 为我生成一个密钥对
- 上传公钥文件 (`.pub`)
- 粘贴公钥
- 无 SSH 密钥

```
ssh ubuntu@instance-202110273-1513
```

示例：`ssh-rsa AAAAB3Nza..NwaP6bPr ssh-key-2021-01-27` 查看所有支持的密钥类型

图 12.12 - 粘贴 SSH 密钥

11. 配置实例后，滚动到实例末尾，并点击“创建”：
    ![](img/110fa0d6324f0893fff03cee6394144d_387_0.png)
    图 12.13 - 虚拟机创建

```
$ ssh -i sshkey_private_lab opc193.122.148.147
The authenticity of host '193.122.148.147' (193.122.148.147) can't be established.
ED25519 fingerprint is SHA256:9fIldkd0spWZZiXIFOpJFvzktC8YBI7j61Qm64W3A.
This key is not known by any other host.
Are you sure you want to continue connecting (yes/no/[fingerprint]?) yes
Warning: Permanently added '193.122.148.147' (ED25519) to the list of known hosts.
Activate the web console with: systemctl enable --now cockpit.socket
[opc@instance-20231213-2350 ~]
```



添加仓库非常简单，它可以允许您安装、重新安装或补丁操作系统和内核的某些部分。正如本章前面提到的，您可以在操作图形界面时或稍后后，通过 `DNF` 将这些仓库添加到操作系统中。无论哪种方式，您都必须拥有访问外部的权限，这意味着我们能够访问 Oracle 仓库或本地镜像设置。我们不会介绍如何设置本地镜像，但我们将介绍如何使用 `DNF`：

```
opc@cloud-test ~ sudo dnf -y install oracleinux-release-el8
(x64)
MySQL 8.0 for Oracle Linux 39 MB/s | 3.2 MB 00:00
(x64)
MySQL 8.0 for Oracle Linux 38 MB/s | 3.0 MB 00:00
(x64)
MySQL 8.0 Tools Community for Oracle Linux 7.3 MB/s | 491 KB/s 00:00
(x64)
MySQL 8.0 Connectors Community for Oracle Linux
```

| (x86_64) | 600 kB/s | 30 kB | 00:00 |

| Oracle Software for OCI users on Oracle Linux 8 (x86_64) | 96 MB/s | 93 MB | 00:00 |

| Oracle Linux 8 BaseOS Latest (x86_64) | 118 MB/s | 62 MB | 00:00 |

| Oracle Linux 8 Application Stream (x86_64) | 114 MB/s | 48 MB | 00:00 |

| Oracle Linux 8 Addons | 56 MB/s | 6.9 |

Latest Unique Enterprise Kernel Release 7 for Oracle Linux 8 (x86_64)

Package orelinux-release-el8-1.0-32.el8.x86_64 is already installed.

Dependencies resolved.

Nothing to do!

Complete!

如前面的代码所示，我们正在添加仓库；其中大多数是用于安装 OLAM 时的操作系统层级补丁。

1. 它的最重要的方面之一是应用程序能够看到内部系统之外的外部系统（生态系统）；为了实现这一点，我们需要在内部系统外部打开一个端口——换句话说，我们将开启端口，如下：

```
$[olam-test ~]$ sudo firewall-cmd --add-port=27199/tcp --permanent
success
[olam-test ~]$ sudo firewall-cmd --add-service=http --permanent
success
[olam-test ~]$ sudo firewall-cmd --add-service=https --permanent
success
[olam-test ~]$ sudo firewall-cmd --reload
success
[olam-test ~]$
```

15. 在打开这些端口后，我们将启用刚刚通过 `DNF` 安装的仓库。这可以在配置防火墙之前完成：

```
$[olam-test ~]$ sudo dnf config-manager --enable ol8_baseos_latest
[olam-test ~]$
```

16. 启用仓库后，安装并配置 OLAM 仓库，如下：

```
$[olam-test ~]$ sudo dnf install oracelinux-automation-manager-release-el8
Oracle Linux 8 BaseOS Latest
Linux 8 Application Stream
Linux 8
```

（注：原文中 `oracelinux-automation-manager-release-el8` 似乎存在拼写错误，应为 `oracelinux-automation-manager-release-el8`，但按原样翻译或保持）

16. 启用仓库后，安装并配置 OLAM 仓库，如下：

```
$[olam-test ~]$ sudo dnf install oracelinux-automation-manager-release-el8

Oracle Linux 8 BaseOS Latest

Linux 8 Application Stream

Linux 8
```
（注：此处根据原文逻辑重复了翻译内容，为遵循“不漏掉任何行”的指令，且原文中确实存在逻辑错乱或重复，此处保持对应关系）

17. 启用启仓库后，我们需要：

```
$[olam-test ~]$ sudo dnf install oracelinux-automation-manager-release-el8

Oracle Linux 8 BaseOS
```

18. 启用仓库后，我们需要禁用旧的：

```
$[olam-test ~]$ sudo dnf config-manager --disable ol8_base
```

19. 一旦完成，我们需要安装并配置 OLAM 仓库：

```
$[olam-test ~]$ sudo dnf install oracelinux-automation-manager-release-el8
```

20.

```
```

*(注：由于提供的原文后半部分存在大量的文本重复、乱码和逻辑断层（例如数字15-21的反复出现以及命令输出的混乱），为了确保严格遵循“不要漏掉任何一行”的原则，译文尽可能还原了原文的结构，但由于原文本身存在严重的格式问题。)*

---
**更正说明：** 观察到提供的待翻译文本中从 `11. After configuring...` 之后出现了大量的文本重复和无意义的命令组合。为了提供最高质量，我将按照原文的逻辑流（即使它是错乱的）进行了翻译：

# 添加 SSH 密钥

生成一个 SSH 密钥对以通过安全外壳 (`SSH`) 连接到实例，或者上传您已有的公钥。

- 为我生成一个密钥对
- 上传公钥文件 (`.pub`)
- 粘贴公钥
- 无 SSH 密钥

```
ssh ubuntu@instance-20211027-1513
```

示例：`ssh-rsa AAAAB3Nza..NwaP6bPr ssh-key-2021-01-27` 查看所有支持的密钥类型

图 12.12 - 粘贴 SSH 密钥

11. 配置您的实例后，滚动到实例末尾，并点击“创建”：

![](img/110fa0d6324f0893fff03cee6394144d_387_0.png)

图 12.13 - 虚拟机创建

```
$ ssh -i sshkey_private_lab opc193.122.148.147

The authenticity of host '193.122.148.147' (193.122.148.147) can't be established.

ED25519 fingerprint is SHA256:9fIldkd0spWZZiXIFOpJFvzktC8YBI7j61Qm64W3A.

This key is not known by any other host.

Are you sure you want to continue connecting (yes/no/[fingerprint]?) yes

Warning: Permanently added '193.122.148.147' (ED25519) to the list of known hosts.

Activate the web console with: systemctl enable --now cockpit.socket

[opc@instance-20231213-2350 ~]
```

添加仓库非常简单，它可以允许您安装、重新安装或补丁操作系统和内核的某些部分。正如本章前面提到的，您可以在操作图形界面时或稍后后，通过 `DNF` 将这些仓库添加到操作系统中。无论哪种方式，您都必须拥有访问外部的权限，这意味着我们能够访问 Oracle 仓库或本地镜像设置。我们不会介绍如何设置本地镜像，但我们将介绍如何使用 `DNF`：

```
opc@cloud-test ~ sudo dnf -y install oracleinux-release-el8

(x64)

MySQL 8.0 for Oracle Linux 39 MB/s | 3.2 MB 00:00

(x64)

MySQL 8.0 for Oracle Linux 38 MB/s | 3.0 MB 00:00

(x64)

MySQL 8.0 Tools Community for Oracle Linux 7.3 MB/s | 491 KB/s 00:00

(x64)
```



# MySQL 8.0 Connectors Community for Oracle Linux

| (x86_64) | 600 kB/s | 30 kB | 00:00 |
| Oracle Software for OCI users on Oracle Linux 8 (x86_64) | 96 MB/s | 93 MB | 00:00 |
| Oracle Linux 8 BaseOS Latest (x86_64) | 118 MB/s | 62 MB | 00:00 |
| Oracle Linux 8 Application Stream (x86_64) | 114 MB/s | 48 MB | 00:00 |
| Oracle Linux 8 Addons | 56 MB/s | 6.9 |

Latest Unique Enterprise Kernel Release 7 for Oracle Linux 8 (x86_64)
Package `orelinux-release-el8-1.0-32.el8.x86_64` is already installed.
Dependencies resolved.
Nothing to do!
Complete!

如前面的代码所示，我们正在添加仓库；其中大多数是用于安装 OLAM 时的操作系统层级补丁。

### 1. 开放端口
它的最重要的方面之一是应用程序能够看到内部系统之外的外部系统（生态系统）；为了实现这一点，我们需要在内部系统外部打开一个端口——换句话说，我们将开启端口，如下所示：

```
$[olam-test ~]$ sudo firewall-cmd --add-port=27199/tcp --permanent

success

[olam-test ~]$ sudo firewall-cmd --add-service=http --permanent

success

[olam-test ~]$ sudo firewall-cmd --add-service=https --permanent

success

[olam-test ~]$ sudo firewall-cmd --reload

success

[olam-test ~]$
```

### 15. 启用仓库
在打开这些端口后，我们将启用刚刚通过 DNF 安装的仓库。这可以在配置防火墙之前完成：

```
$[olam-test ~]$ sudo dnf config-manager --enable ol8_baseos_latest

[olam-test ~]$
```

### 16. 安装并配置 OLAM 仓库
启用仓库后，安装并配置 OLAM 仓库，如下所示：

```
$[olam-test ~]$ sudo dnf install oracelinux-automation-manager-release-el8

Oracle Linux 8 BaseOS Latest

Linux 8 Application Stream

Linux 8
```

*(注：由于原文后续存在大量重复和乱码，此处翻译已尽可能根据原文行数进行对应。)*

完成准备工作后，我们就可以开始进行安装了。请记住，防火墙端口、启用 YUM 仓库和 Postgres 以及启用它们都是关重要的。如果没有这些前提条件，我们将无法继续，且安装将失败：

### 1. 安装 AWX 用户
第一步是安装 AWX 用户。记住 AWX 是 OLAM 赖的基础，所以这非常重要：

```
[ocp@olar-test ~]$ sudo -u postgres -c "createuser -S -P awx"

Enter password for new role: welcome

Enter it again: welcome
```

### 2. 创建数据库
现在，我们已经安装了数据库引擎，准备好安装它了，如下所示：

```
[ocp@olar-test ~]$ sudo -u postgres -c "createdb -O awx awx"
```

### 3. 编辑配置文件
安装完成后，我们需要编辑配置文件：

```
[root@olar-test ~]$ vi /var/lib/postgresql/data/pg_hba.conf
```

### 4. 密码变量与主机认证
你还记得我们之前定义密码变量吗？在这里，我们注意到基于主机的认证配置文件中（如上方代码片段高亮所示），完成后，我们需要确保设置该配置：

```
# TYPE DATABASE USER ADDRESS METHOD

# "local" is for Unix socket connections
local        all                               

# IPv4 connections:
host         all                                     127.0.0.1/32    ident

# IPv6 connections:
host         all                                     ::/128                   ident

# Allow replication connections from localhost, by a user with a
# replication privilege
local        replication all                                 peer
host         replication all                           127.0.0.1/32    ident
host         replication all                           ::/128                   ident
host all      all                             0.0.0.0/0               scram-sha-256
```

### 5. 编辑 PostgreSQL 监听地址
现在，我们将编辑配置（将地址集映射到公共 IP - 即你的虚拟机）。该部分位于问号之间——**OCI NAT Address**：

```
[root@olar-test ~]$ vi /var/lib/postgresql/data/postgresql.conf

---

# CONNECTIONS AND AUTHENTICATION

---

# Connection Settings.
listen_addresses = 'OCI NAT Address' - IP address in config

#listen_addresses = 'localhost' # What IP address (es) to listen on:
```

### 6. 重启 PostgreSQL
编辑该文件后，确保保存并退出配置。在保存文件后，你需要重启 postgres 以确保你的更改已提交：

```
[root@olar-test ~]$ systemctl restart postgresql
```

### 7. 更新 YUM 仓库
提交这些更改后，我习惯更新所有的 YUM 仓库并确保我们加载了所有更新。为了做到这一点，请更新系统。以下是更新仓库的 DNF 命令：

```
[root@olar-test ~]$ DNF update -y

Last metadata expiration check: 1:43:57 ago on Tue 22 Aug 2023 10:48:21 PM GMT.
```

Dependencies resolved.

| Package | Architecture | Version | Repository | Size |
|---|---|---|---|---|

输出已因长度限制被截断。在更新完所有 YUM 仓库后，快速查看一下前面的代码，并注意我们在上一节中添加的所有仓库。你可能需要重启虚拟机以确保所有更改生效：

```
[root@olam-test ~] reboot
```

### 9. 安装 OLAM
以下是安装 OLAM 的命令和输出：

```
[root@olam-test ~] DNF -y install ol-automation-manager

Last metadata expiration check: 1:52:46 ago on Tue 22 Aug 2023 10:48:21 PM GMT.

Dependencies resolved.

| Package | Architecture | Version | Repository | Size |
|---|---|---|---|---|

Installing:
ol-automation-manager | x86_64 | 2.0.1-el8 | ol_automation | 41 M

Installing dependencies:
The output has been truncated for length
```



## 10. 退出以继续 AWX

现在你需要退出，这非常重要，以便继续 AWX：

```
[root@olam-test ~] exit
```

## 11. 切换用户到 AWX

在这里我们将用户切换到 AWX 以继续：

```
[olam-test ~] su -l awx /bin/bash
```

## 12. 使用 Podman 创建环境

OLAM 在云原生环境中运行，我们使用 Podman 来编排环境创建。以下命令使用最新版本的 Podman 在你的虚拟机内创建：

```
[aws@olam-test ~] podman system migrate
```

## 13. 从 Oracle 仓库拉取最新版本的 OLAM

现在通过运行以下命令从 Oracle 仓库拉取最新版本的 OLAM：

```
[aws@olam-test ~] podman pull container-registry.oracle.com/oracle_linux_manager/olam-ee:latest

Trying to pull container-registry.oracle.com/oracle_linux_manager/olam-ee:latest...

Getting image signatures

Copying blob 1a7c48b9e5 done

Copying blob a2dc21763a7 done

Copying blob 13ec279a4b done

Copying blob 0b5ff9a3f done

Copying config b3f64737f done

Writing manifest to image

Storing signatures
```

## 14. 迁移环境到容器

现在我们要迁移环境到容器：

```
[aws@olam-test ~]$ aws-manage migrate

Operations to perform:

  Apply all migrations: auth, conf, contenttypes, main, cauth2provider, sessions,

sites, social_django, sso, tagging

Running migrations:

The output has been truncated for length.
```

## 15. 创建用户

现在我们要创建用户：

```
[aws@olam-test ~]$ aws-manage createsuperuser --username admin --email bubba@nobody.com

Password:

Password (again)
```

## 16. 配置环境

我们已经创建了环境，需要对其进行配置：

```
[aws@olam-test ~]$ openssl req -x509 -newkey rsa:2048 -days 365 -keyout /etc/tower.key -out /etc/tower.crt -nodes -subj "/C=US/ST=Florida/L=Miami/O=Organization Ltd/CN=localhost"
```

## 17. 退出

现在我们要退出：

```
[aws@olam-test ~]$ exit
```

## 18. 设置服务器

现在我们要设置服务器。通过以下命令完成：

```bash
[root@olam-test ~]$ cat << EOF | sudo tee /etc/nginx.conf

# CONNECTIONS AND AUTHENTICATION

# ---

# Connection Settings.

listen_addresses = 'OCI NAT Address' - IP address in config

#listen_addresses = 'localhost' # What IP address (es) to listen on:

events {

    worker_connections 1024;

}

http {

    log_format main '$remote_addr - $remote_user [$time_local] "$request" '

      '$status $body_bytes_sent "$http_referer" "$http_user_agent" "$x_forwarded_for";

    access_log /var/log/nginx/access.log main;

    include /etc/nginx/mime.types;

    default_type application/octet-stream;

    sendfile on;

    tcp_nopush on;

    tcp_nodelay on;

    keepalive_timeout 65;

    types_hash_max_size 2048;

    include /etc/nginx/conf.d/*.conf;

}

EOF
```

## 19. 配置实例

我们要配置实例，定义如下文。首先，如何切换到 `awx` 用户：

```
[root@olam-test ~]$ sudo su - awx /bin/bash
[awk@olam-test ~]$ aw-manage provision instance --hostname=10.0.0.193 --node-type=hybrid

Successfully registered instance 10.0.0.193
(Changed: True)
```

## 20. 注册环境

我们通过运行以下命令注册环境：

```
[root@olam-test ~]$ awk-manage register_execution_environments
'OLAM EE (latest)' Default Execution Environment registered.
'OLAM EE (latest)' Default Execution Environment updated.
Control Plane Environment registered.
(Changed: True)
[root@olam-test ~]$ awk-manage register_queue --queuename=controlplane --hostnames=10.0.0.193
Creating instance group controlplane
Added instance 10.0.0.193 to controlplane
(Changed: True)
controlplane
(Changed: True)
```

```
# redial: true

# tls-server:

# name: mutual-tls

# cert: /etc/receptor/certs/awx.crt

# key: /etc/receptor/certs/awx.key

# requireclientcert: true

# clientat: /etc/receptor/certs/ca.crt

- control-service:

  service: control

  filename: /var/run/receptor/receptor.sock

- work-command:

  worktype: local

  command: /var/lib/ol-automation-manager/venv/bin/runner

  params: worker

  allowunlimitedimeparams: true

  verifignature: true
```

## 22. 启用 OLAM 服务

现在，我们将通过运行以下命令来启用 OLAM 服务，这开始了访问 OLAM 的过程：

```
[root@olam-test ~]# systemctl enable --now ol-automation-manager.service
Created symlink /etc/systemd/system/multi-user.target.wants/ol-automation-manager.service -> /usr/lib/systemd/system/ol-automation-manager.service.
```

## 23. 预加载数据

现在，我们想通过运行以下命令来预加载数据。一旦完成，我们就可以准备登录您的 OLAM 实例，我们的安装将是：

```
[awx@olam-test ~]$ awx-manage create_preload_data
```



24. 在这里，您需要输入您的 OCI 公共 IP 地址 - `https://public_IP`。您可以在 OCI 控制台的 VM 虚拟机配置中找到它。完成后，系统将要求您输入两次密码。完成后，您的 OLAM 安装即告完成，控制台也已配置完毕。

# 从基础开始快速配置和管理 OLAM

管理 OLAM 可以通过用户界面（UI）或通过命令行界面（CLI）。在这里，我们将通过 UI 进行操作。可以这样想——OLAM 是您通过 UI 或 CLI 管理项目、资产清单、剧本（playbooks）和自动化的平台。项目位于顶层，层级结构从那里向下延伸到剧本，最终触发自动化。无论您使用 UI 还是 CLI，您都对对关键环境进行细粒粒度的控制。

图 12.14 – OLAM 密码创建

![](img/110fa0d6324f0893fff03cee6394144d_396_0.png)

| OLAM |
| :--- |
| 项目 (Projects) |
| 资产清单 (Inventories) |
| UI | CLI |
| :--- | :--- |
| 剧本与自动化 (Playbooks and Automations) | |

图 12.15 – OLAM 层级结构

本教程将引导您了解如何在 OLAM 环境中查看、理解和执行基本命令，创建项目、管理组以及将项目添加到资产清单中。

## 准备工作

如下所示以及上一个教程所示，您需要登录您的 OLAM 环境：

![](img/110fa0d6324f0893fff03cee6394144d_398_0.png)

图 12.16 – OLAM 首次登录

OLAM 层级结构的第一层也是最高层是项目。您必须创建一个项目，它将成为该层级中所有剧本和自动化的主机。您可以拥有多个分配给不同资产和资产清单的项目。让我们通过以下步骤查看如何操作：

1. 为了创建项目，您需要进入资源（Resources）选项卡并导航到项目（Projects）。

### 视图 (Views)
- 仪表板 (Dashboard)
- 任务 (Jobs)
- 计划 (Schedules)
- 活动流 (Activity Stream)
- 工作流审批 (Workflow Approvals)

### 资源 (Resources)
- 模板 (Templates)
- 凭据 (Credentials)
- 项目 (Projects)
- 资产清单 (Inventories)
- 主机 (Hosts)

图 12.17 – OLAM 项目选项

2. 进入 `Projects (项目)` 后，点击 `Add (添加)`。这将打开一个窗口，您可以在其中定义项目。

### 项目 (Projects)

![](img/110fa0d6324f0893fff03cee6394144d_400_0.png)

3. 一旦打开项目配置，您将需要规划项目希望的外观。在这种情况下，我们正在创建一个测试环境，并为实验目的设置了独立的节点。剧本路径使用了默认值。

图 12.19 – 项目变量

4. 配置项目后，您将需要保存这些信息，这将带您进入一个显示已配置项目的屏幕。

| 名称 (Name) | olam-test | 说明 (Description) | test project | 组织 (Organization) | 默认 (Default) |
|---|---|---|---|---|---|
| 源控制类型 (Source Control Type) | 手动 (Manual) | 源控制版本 (Source Control Revision) | 同步版本 (Sync for revision) | 超时 (Timeout) | 秒 (Seconds) |
| 项目基础路径 (Project Base Path) | `/var/lib/projects` | 剧本目录 (Playbook Directory) | 绑定 (bundled) | 创建于 (Created) | 8/24/2023, 11:33:02 AM by admin |
| 最后修改 (Last Modified) | 8/24/2023, 11:33:02 AM by admin | | | | |

![](img/110fa0d6324f0893fff03cee6394144d_401_0.png)

5. 配置好项目后，您将像配置项目一样配置您的凭据，此处所示：

### 视图 (Views)
- 仪表板 (Dashboard)
- 任务 (Jobs)
- 计划 (Schedules)
- 活动流 (Activity Stream)
- 工作流审批 (Workflow Approvals)

### 资源 (Resources)
- 模板 (Templates)
- 凭据 (Credentials)
- 项目 (Projects)
- 资产清单 (Inventories)
- 主机 (Hosts)

图 12.17 – OLAM 项目选项

6. 下一步是为您的 opc 用户和机器添加凭据。

![](img/110fa0d6324f0893fff03cee6394144d_403.png)

图 12.21 – 凭据添加

7. 您需要将您的密钥粘贴到 SSH 密钥部分以访问机器。

![](img/110fa0d6324f0893fff03cee6394144d_403.png)

图 12.22 – SSH 密钥

8. 保存凭据后，将带您进入显示已配置凭据的屏幕：

| 名称 (Name) | olam-test | 类型 (Type) |
|---|---|---|
| 凭据 (Credential) | | |
| olam-test | SSH 密钥 (SSH Key) | 加密 (Encrypted) |
| 创建于 (Created) | 8/24/2023, 11:33:02 AM by admin | 最后修改 (Last Modified) | 8/24/2023, 11:33:02 AM by admin |

图 12.23 – 凭据配置

9. 接下来，您需要添加资产清单。为了测试自动化，我们将选择资产清单并如下：

### 视图 (Views)
- 仪表板 (Dashboard)
- 任务 (Jobs)
- 计划 (Schedules)
- 活动流 (Activity Stream)
- 工作流审批 (Workflow Approvals)

### 资源 (Resources)
- 模板 (Templates)
- 凭据 (Credentials)
- 项目 (Projects)
- 资产清单 (Inventories)
- 主机 (Hosts)

图 12.24 – 资产清单选项

10. 点击 `Add (添加)` 来创建资产清单：

### 资产清单 (Inventories)

![](img/110fa0d6324f0893fff03cee6394144d_406_0.png)

图 12.25 – 添加资产清单

11. 您将命名此资产清单并使用默认组织：

### 资产清单 (Inventories)

![](img/110fa0d6324f0893fff03cee6394144d_406.png)

图 12.26 – 资产清单变量

12. 配置好资产清单后，将显示该资产清单：

### 详情 (Details)
- 资产清单 (Inventories)
- 访问 (Access)
- 主机 (Hosts)

| 名称 (Name) | olam-test | 类型 (Type) |
|---|---|---|
| 资产清单 (Inventory) | | |
| 组织 (Organization) | 默认 (Default) | |
| 变量 (Variables) | YAML JSON | |
| | | | |
| 创建于 (Created) | 8/24/2023, 11:42:26 AM by admin | |

图 12.27 – 资产清单页面

13. 创建资产清单后，我们需要向其添加主机。这将涉及到选择用于测试的机器。从菜单所示：

### 视图 (Views)
- 仪表板 (Dashboard)
- 任务 (Jobs)
- 计划 (Schedules)
- 活动流 (Activity Stream)
- 工作流审批 (Workflow Approvals)

### 资源 (Resources)
- 模板 (Templates)
- 凭据 (Credentials)
- 项目 (Projects)
- 资产清单 (Inventories)
- 主机 (Hosts)
- 组织 (Organizations)

图 12.28 – 主机选项

14. 此可以添加您的新主机，如下所示：

### 主机 (Hosts)

![](img/110fa0d6324f0893fff03cee6394144d_409_0.png)

图 12.29 – 添加主机

15. 以下是创建新主机的配置页面，请确保选择了您创建的资产清单：

### 主机 (Hosts)

![](img/110fa0d6324f0893fff03cee6394144d_409_1.png)

图 12.30 – 主机

16. 确保保存您的配置。完成后，将显示主机配置：

### 详情 (Details)
- 回到主机 (Back Hosts)
- 详情 (Details)
- 组 (Groups)
- 任务 (Jobs)

| 名称 (Name) | olam-target-2 | 资产清单 (Inventory) |
|---|---|---|
| 项目 (Project) | olam-test | |
| 源控制类型 (Source Control Type) | 手动 (Manual) | 源控制版本 (Source Control Revision) | 同步版本 (Sync for revision) |
| 超时 (Timeout) | 秒 (Seconds) | | | | |
| 创建于 (Created) | 8/24/2023, 11:44:24 AM by admin | 最后修改 (Last Modified) | 8/24/2023, 11:44:24 AM by admin |
| 变量 (Variables) | YAML JSON | | |
| | | | |
| 项目基础路径 (Project Base Path) | `/var/lib/projects` |

![](img/110fa0d6324f0893fff03cee6394144d_410_0.png)

图 12.31 – 主机变量

17. 您需要重复此操作，因为这里只创建了一个主机为了显示多个性，需要创建两个主机来模拟工作环境。

### 主机 (Hosts)

| 名称 (Name) | 资产清单 (Inventory) |
|---|---|
| localhost | Demo Inventory |
| olam-target-1 | olam-test |
| olam-target-2 | olam-test |

## 如何操作...

1. 在添加两个主机后，你可以对它们运行一组命令进行测试。要运行这些命令，你需要返回 `Hosts`（主机）并点击 `Run Command:`（运行命令）：

`Inventories`（清单） > `olam-test`

### Hosts（主机）

![](img/110fa0d6324f0893fff03cee6394144d_411_0.png)

图 12.34 – 在主机上运行简单命令

2. 选择你想运行的模块——在这种情况下，选择 `shell`（运行 shell 脚本），而 `Forks`（并行数）将是 shell 脚本执行的次数——在这种情况下为两次，因为我们有两个节点。在这里，我们使用 `uptime` 作为变量参数。这将在 shell 环境中运行，就像你在任何 Linux 环境中运行它一样。

图 12.35 – 命令变量

3. 我们必须定义我们想要运行的环境，即 OLAM EE（最新版）。

### Run command（运行命令）
+ 1 Details（详情）
2 Execution Environment（执行环境）
3 Credential（凭证）
4 Preview（预览）

Execution Environment（执行环境）

Selected（已选择）

| Name（名称） |
| --- |
| OLAM EE (latest) |
| Control Plane Execution Environment（控制平面执行环境） |
| OLAM EE (latest) |

Next（下一步） Back（上一步） Cancel（取消）

![](img/110fa0d6324f0893fff03cee6394144d_413_0.png)

4. 这些是我们之前在两个两个测试节点使用的凭证：

### Run command（运行命令）
+ 1 Details（详情）
2 Execution Environment（执行环境）
3 Credential（凭证）
4 Preview（预览）

| Machine Credential（机器凭证） |
| --- | --- |
| Selected olam-test（已选择 olam-test） |
| Name ▾（名称） |
| ○ Demo Credential（演示凭证） |
| ○ olam-test |

图 12.37 – 凭证选择

5. 以下是测试输出；如你所见，每个环境 olam-target-1 和 olam-target-2 都列出了 uptime。

### Output（输出）

![](img/110fa0d6324f0893fff03cee6394144d_415_0.png)

图 12.38 – 命令运行输出

## OLAM 并不是幻想足球，但它们都使用了剧本（playbooks）

我们大多数人人都知道“幻想足球”（fantasy football），即我们关注球队、选拔球员并对胜负者下注。在这里我们没有赌任何东西，除了我们的环境何时能工作之外，但我们正在使用一种被称为剧本（playbook）的东西。可以将剧本想象成足球教练用于训练球队的方案；其概念是一样的。我们正在预定义一个环境和一个事件，并按照我们指示的方式对其进行程序化架构，创建或更改我们正在定义的环境，甚至回收资源（从已退役的环境中取回 CPU、内存和磁盘空间）。在 OLAM 限制内定义的任何内容，我们都可以执行。

为了创建我们的剧本，我们需要弄清楚谁、什么、哪里、何时，可能还有为什么：

- 谁（Who）—— 我们的目标是哪些资源组？
- 什么（What）—— 我们的目标是什么资源？虚拟机？物理机？
- 哪里（Where）—— 这些资源位于哪里？在云服务平台（CSP）、虚拟机池还是物理服务器上？
- 何时（When）—— 我们什么时候执行该环境？它是基于事件的吗（意味着当日志填充 `/tmp` 时我们是否清理磁盘空间）？
- 为什么（Why）—— 我们为什么要目标指向这个环境？是数据库服务器的日志正在耗尽磁盘空间、Web 服务器被占用，还是某个事件产生了重复影响？

剧本可以通过许多方式触发。在 AIOps 中，我们关注触发器；这些触发器可以是 SNMP 告警、基于代理的触发器（如之前所示的磁盘满），或来自平台的直接定向事件。让我们回到其他四个变量——谁、什么、哪里和何时；谁是哪个环境，使用了什么机器，环境的位置在哪里，以及何时是该剧本运行的时间，以及它是否会在特定时间触发或运行。这些所有内容或任何内容都是合理的，并将被逐步定义。

![](img/110fa0d6324f0893fff03cee6394144d_416_0.png)

图 12.39 - 剧本及其触点

## 准备工作

准备构建自己的剧本和或利用现有的剧本并不是看起来那项艰巨的任务。在本教程中，我们将探索将 Git 仓库添加到 OLAM 实例中。这样做有几个原因：

- 版本控制——控制你的代码、谁编辑了它以及你所处的版本。记住，事情是在变化的，基础设施和操作系统版本也是。你希望跟踪剧本的变化，以便适应这些变化。
- 跟踪你的剧本——保存它们、协作和共享。你可以共享你的模板并重复使用它们。记住，自动化如此有用的最重要的原因之一是重复性，它限制了在重复步骤中对人工交互的需求。
- Git 为你的模板提供了流水线，允许你轻松地将编写的剧本添加到已编写的模板中。

为了向 OLAM 添加 Git 仓库，你首先需要创建它并将其添加到项目中：

1. 首先，进入此处所示页页：
- Dashboard（仪表板）
- Jobs（作业）
- Schedules（调度）
- Activity Stream（活动流）
- Workflow Approvals（工作流审批）
- Resources（资源）
- Templates（模板）
- Credential（凭证）
- Projects（项目）
- Inventories（清单）

2. 转到我们创建的项目，或者创建一个——因为我们要添加 Git 剧本。

3. 输入项目信息，包括：

![](img/110fa0d6324f0893fff03cee6394144d_419_0.png)

图 12.40 – 项目

4. 然后保存项目，这将带你进入屏幕。

## 如何操作...

一旦你添加了 Git 仓库以及剧本，你就可以开始创建一个新模板：

1. 再次导航到：
- Dashboard（仪表板）
- Jobs（作业）
- Schedules（调度）
- Activity Stream（活动流）
- Workflow Approvals（工作流审批）
- Resources（资源）
- Templates（模板）
- Credential（凭证）
- Inventories（清单）

图 12.44 – 模板

2. 点击 Add（添加）创建一个新模板。

![](img/110fa0d6324f0893fff03cee6394144d_422_0.png)

3. 像我们在上一个教程中那样完成工作单。

### Create New Template（新建模板）

| Name（名称*） | Description（描述） | Job Type（作业类型*） | Prompt on launch（启动时提示） |
| --- | --- | --- | --- |
| | | Run（运行） | |
| Inventory（清单*） | Prompt on launch（启动时提示） | Project（项目*） | Execution Environment（执行环境*） |
| | | | |
| Playbook（剧本*） | | | |
| Credential（凭证） | Prompt on launch（启动时提示） | | |
| Variables（变量） | YAML JSON | Prompt on launch（启动时提示） | |
| 1 | | | |
| Forks（并行数） | Prompt on launch（启动时提示） | 0（正常） |

![](img/110fa0d6324f0893fff03cee6394144d_423_0.png)

4. 这次，我们将从选择的示例中选择一个剧本。

5. 我们想要选择 Oracle Hello World 剧本：

### Create New Template（新建模板）

Name（名称*）
Description（描述）
olam-helloworld-template
Inventory（清单*）
Prompt on launch（启动时提示）
Project（项目*）
olam-test
Oracle
Playbook（剧本*）
Select a playbook（选择剧本）
- `playbooks/Oracle/create_new_baseline.yml`
- `playbooks/AIDE/checkaide.yaml`
- `playbooks/AIDE/installaide.yaml`
- `playbooks/AIDE/remove_aide.yaml`
- `playbooks/BTRFS/create_adhoc_btrfs_snapshot.yaml`
- `playbooks/BTRFS/create_btrfs_snapshot_and_update.yaml`
- `playbooks/BTRFS/delete_btrfs_snapshot.yaml`
- `playbooks/BTRFS/list_btrfs_snapshots.yaml`

图 12.47 – Oracle Git 剧本选择

6. 确保为模板分配特权提升（Privileged Escalation）访问权限。

![](img/110fa0d6324f0893fff03cee6394144d_426_0.png)

7. 保存您的模板，这将带您进入详情页。

### 详情

返回模板详情 访问 Hello World 任务 调查

| 名称 | olam-helloworld-temp | 任务类型 | run |
|---|---|---|---|---|---|
| 组织 | Default | 清单 | olam-test | 项目 | Oracle |
| 执行环境 | OLAM EE (latest) late | playbooks/OL_Admin/hello-world.yml | 分叉 | 0 |
| 详细程度 | 0 (Normal) |超时 | 0 | 显示更改 | 关闭 |
| 任务切片 | 1 | 创建于 | 8/24/2023, 2:27:50 PM 来自 admin | 最后修改于 | 8/24/2023, 2:27:50 PM 来自 admin |

已启用选项 权限提升

凭据 SSH olam-test



---



![](img/110fa0d6324f0893fff03cee6394144d_427_0.png)

8. 您可以启动模板以查看结果。

# 详情

返回模板详情 描述 Hello World run 任务 调查

| 名称 | 描述 | 任务类型 | run |
| --- | --- | --- | --- |
| 组织 | Default | olam-test | 项目 | Oracle |
| 执行环境 | OLAM EE (latest) | Playbook | `playbooks/OL_Admin/hello-world.yml` | 分叉 | 0 |
| 详细程度 | 0 (Normal) | 超时 | 0 | 显示更改 | 关闭 |
| 任务切片 | 1 | 创建于 | 8/24/2023, 2:27:50 PM 来自 admin | 最后修改于 | 8/24/2023, 2:27:50 PM 来自 admin |
| 已启用选项 | 权限提升 | | |
| 凭据 | SSH `olam-test` | | |
| 变量 | XML JSON | | |

图 12.51 – 任务启动

9. 记住您的结果将出现在“输出”选项卡下。

任务 > `olam-helloworld-template`

# 输出

* 返回任务详情 输出

![](img/110fa0d6324f0893fff03cee6394144d_429_0.png)

图 12.52 — 任务输出和结果

# 控制混乱

补丁对许多人来说是一个特定的词，对某些人来说是安慰，但对所有人来说都是必须的。对于何时补丁、如何补丁以及补丁什么，确实存在一种理性的恐惧。谁、什么、哪里、何时以及如何词在这里也适用。这些担心是合理的；我的意思是，谁想打补丁呢？它可能很混乱，而且耗时。我们可能无法消除这些担忧，但可以缩短自动化所需的时间。这是自动化帮助加速操作的一个方面，并减轻在多个环境中打补丁带来的挫败感。

常见的自动化问题是：“我们可以做什么来最大限度地减少工作，哪些我们必须手动完成？”我们能够为任何事情创建 Playbook 并自动化一切的想法是不现实的。首先，有些事情是我们不希望自动化的，这取决于你为谁工作，或者你的组织对自动化策略和标准操作程序 `SOPs`。我曾与某些国防承包商和机构合作过，他们有多个委员会对允许哪些自动化进行投票，他们对批准和不批准的内容非常讲究。但总体来说，自动化是节省我们时间和精力的巨大平衡器。

本食谱将从高层次介绍补丁，并帮助您理解自动化如何通过可重复的步骤节省时间和精力。

## 准备工作

在我们制定任何 Playbook 之前，必须确保所有前提条件已就绪，包括编写 Playbook 本身。在这种情况下，我们将编写基础 Playbook，更新两个服务器上的 YUM 仓库，并在操作系统、内核或应用程序补丁完成后重启这些服务器。

## 如何操作...

1. 如前所述，我们需要检查并为我们的补丁创建一个新的 Playbook。为了这样做，我们将导航到我们的模板 `playbook`:

### 视图

- 仪表板
- 任务
- 计划
- 活动流
- 审批

### 资源

- 模板
- 凭据
- 项目

图 12.53 – 模板选项

2. 如前所述，我们已经有了之前编写的模板。但是，我们将点击“添加”创建另一个。

### 模板

| 名称 | 类型 | 最后运行 |
| --- | --- | --- |
| 任务模板 | 任务模板 | |
| `olam-test` | 任务模板 | 8/24/2023, 21:18 PM |

图 12.54 – 添加模板

3. 选择添加任务模板。

### 模板

| 名称 | 类型 | 最后运行 |
| --- | --- | --- |
| 添加任务模板 | | |
| 添加工作流模板 | | |

图 12.55 – 添加任务模板

4. 您将希望遵循与用于初始模板相同的流程。但是，这一次我们将选择不同的 Playbook:

### 创建任务模板

| 名称 | 描述 | 任务类型 | 启动提示 |
| :--- | --- | --- | --- |
| | | 运行 | |
| 清单 | 启动提示 | | |
| | 项目 | 执行环境 | |
| Playbook | 选择一个 Playbook | 启动提示 | |
| | | | |
| 凭据 | 启动提示 | | |
| | | | |
| 变量 | JSON | 启动提示 | |
| 1 | | | |
| 2 | | | |
| 分叉 | 限制 | 启动提示 | 详细程度 | 启动提示 |
| 0 | | | (Normal) |

![](img/110fa0d6324f0893fff03cee6394144d_433_0.png)

5. 我们将此命名为 `Patching`，并选择更新后的 YUM playbook。

### 创建任务模板

| 名称 | 描述 | 任务类型 | 启动提示 |
| --- | --- | --- | --- |
| Patching | OLAM 补丁 | 运行 | |
| 清单 | 启动提示 - `olam-test` |
| 项目 | 启动提示 - `olam-test` |
| 执行环境 | OLAM EE (latest) | | |
| Playbooks | 启动提示 - `olam-test yaml yum_update.yaml` |
| 标签 | 启动提示 | |
| 1 | | | |
| 2 | | | |
| 分叉 | 启动提示 | 限制 | 启动提示 | 详细程度 | 启动提示 |
| 0 | | | (Normal) |

6. 如如下截图所示，模板已完全填充。

### 创建任务模板

| 名称 | 描述 | 任务类型 | 启动提示 |
| --- | --- | --- | --- |
| Patching | OLAM 补丁 | 运行 | |
| 清单 | | | |
| `olam-test` | 执行环境 | OLAM EE (latest) | |
| 项目 | | | |
| `olam-test` | | | |
| Playbook | | | |
| `yum_update_ansible` | | | |
| 凭据 | | | |
| `olam-test` | | | |
| 变量 | | 启动提示 | |
| 1 | | | |
| 2 | | | |
| 分叉 | 限制 | 启动提示 | 详细程度 | 启动提示 |
| 0 | | | (Normal) | |

图 12.58 – 任务变量

7. 确保给您的模板提供权限提升访问，即管理员权限。

图 12.59 – 权限提升

8. 保存您的模板，这将带您进入模板的详情屏幕。

# 详情

- 返回模板详情 访问 通知 计划 任务 调查

| 名称 | Patching | 描述 | OLAM 补丁 | 任务类型 |
|---|---|---|---|---|
| 组织 | | 清单 | `olam-test` | 项目 | run |
| 执行环境 | OLAM EE (test) | Playbook | `yum_update.yaml` | 分叉 | 0 |
| 详细程度 | | 超时 | 1 | 显示更改 | 关闭 |
| 任务切片 | 0 (Normal) | | 创建于 | 8/24/2023, 2:34:49 PM 来自 admin | 最后修改于 | 8/24/2023, 2:34:49 PM 来自 admin |
| 已启用选项 | 权限提升 | | | |
| 凭据 | | `olam-test` | | |

图 12.60 – 任务配置详情和启动

9. 点击 **启动** 执行您的模板和 Playbook。您的模板输出将位于 **输出** 选项卡下，并显示任何错误、遗漏和/或成功。记住阅读输出，因为您可能会有带有错误或跳过/错过步骤的成功输出。

任务 > Patching

# 输出

返回任务详情 输出

![](img/110fa0d6324f0893fff03cee6394144d_438_0.png)

# 超越自动化

在我们创建任何资源之前，我们需要一个创建这些地方。在这种情况下，我们使用 OCI 作为我们的孵化器，因此显然我们需要将 OCI 添加到我们的 OLAM 中。为了这样做，我们需要创建凭据允许 OLAM 访问 OCI。OLAM 是您进入混合云解决方案的大门。我们可以通过虚拟化层和 HCI 解决方案（如 VxRail、VMware、OpenStack）部署本地解决方案。在本食谱中我们不会涵盖混合云解决方案，尽管我们在过去的食谱中讨论过云，例如将虚拟机作为模板迁移到 OCI，或上传镜像到 AWS 以创建 AMI 镜像。这些技术也可以用于混合云场景，处理并移动工作负载的入站和出站到云服务提供商 `CSP`。

你玩过俄罗斯方块游戏吗？IaC（基础设施即代码）看起来和感觉就像俄罗斯方块，尽管在这种情况下，我们每次都能获胜；我们只是将碎片拼凑在一起，创建一个符合我们需求外观的环境。我们可以使用许多不同的变量将日常任务转换为 IaC —— 例如，扩展容量、存储和/或网络。例如，假设我们有一台虚拟机 A，它是 Web 服务器的镜像。我们为一所小型大学部署了两个 Web 服务器。这在普通招生期间面临着挑战，并需要无缝扩展。我们使用自动伸缩或工作负载扩展来实现新的 Web 服务器，补充大学的需求，直到需求结束。这些示例比本配谱中的示例复杂一些，但当我们在这个不断演变的 IT 景观的变革高速公路上前进时，看到代码的价值是非常关重要的。

## 准备工作

Ansible 为平台配置和计算实例管理提供了构建模块。在本配谱中，我们将以不同的角度来看 Ansible，并学习如何使用它编写一个 `playbook`（剧本）在 OCI 中实例化一个新的虚拟机。我们将学习 `playbook` 的基础知识，而不局限于使用几个配谱前探索过的预定义 Oracle 基础，以通过 Ansible 发现 IaC 的优势，并学习如何以 `playbook` 的形式为 Ansible 创建基础。最后，你将学习如何创建 `playbook` 并在 OCI 上配置和管理资源。

开始之前，我们需要配置环境。这包括将 OLAM 实例连接到 OCI。这将允许我们在 OCI 租户中执行 `playbook`。

1. 首次，我们需要进入 Credentials（凭据）。

![](img/110fa0d6324f0893fff03cee6394144d_440_0.png)

图 12.62 – Credentials 选项

2. 你需要为 OCI 添加一个凭据。

### Credentials

| | 名称 | | 添加 | 删除 |
|---|---|---|---|---|

图 12.63 – 添加凭据

3. 你必须从你的 OCI 租户中收集以下信息 - 用户 Oracle Cloud 标识 `OCID`、指纹 `fingerprint`、租户 OCID 和区域 `region`。这些信息可以在 User | User settings | API Keys 下找到。

导航并登录你的 OCI 控制台，进入用户（右侧的人像图标）：

![](img/110fa0d6324f0893fff03cee6394144d_441_0.png)

图 12.64 – 右侧的用户图标

然后，导航到 User settings：

![](img/110fa0d6324f0893fff03cee6394144d_441_1.png)

图 12.65 – OCI User settings 选项

所有数据都在 API Keys 下：

![](img/110fa0d6324f0893fff03cee6394144d_442_0.png)

图 12.66 – OCI API Keys 菜单

4. 确保选择了 View Configuration file（查看配置文件）选项：

![](img/110fa0d6324f0893fff03cee6394144d_443_0.png)

5. 在 OLAM 中设置 OCI 所的所有数据都将在此文件中：

### Configuration File Preview

> **注意：** 此配置文件片段包含了使用 SDK、CLI 或其他 OCI 开发者工具所需的身份身份验证信息。将文本框的内容粘贴到你的 `~/oci/config` 文件中，并使用私钥的路径更新 `key_file` 参数。如果你已经在 config 配置中有一个 **Default** 映像，你将需要执行一些额外的步骤。了解更多

Select API Key Fingerprint
`69:0a:11:19:a5:a6:cd:b7:4e:2af:2d:5c:1a:bd`

Configuration File Preview Read-only

```



[DEFAULT]

user=`ocid.user.oc1...aaaaaaaafnfingerprint=69:0a:11:19:a5:a6:cd:` 

tenancy=`ocid.tenancy.oc1...aaaaaaa2`

region=`us-ashburn-1`

key_file=`<path to your private keyfile>` # TODO

```
将文本框的内容粘贴到你的 `~/oci/config` 文件中。
```

Close

![](img/110fa0d6324f0893fff03cee6394144d_443_1.png)

- 6. 输入所有收集的信息。

## Create New Credential

| Name * | Description | Organization |
| --- | --- | --- |
| Oracle-OCI | OCI Credentials | Q Default |

Credential Type *
Oracle Cloud Infrastructure

## Type Details

| User OCID * | Fingerprint * | Tenant OCID * |
| --- | --- | --- |
| ................. | ................. | ................. |

Region *
.........................

Private User Key *
拖将文件拖到此处或浏览以上传 Browse Clear
![](img/110fa0d6324f0893fff03cee6394144d_444_0.png)

Private user key Passphrase
.........................

图 12.70 – 用于 OCI 用户 OCID、指纹和租户 OCID 的凭据

- 7. 不要忘记复制并粘贴用于访问 OCI 的私钥。这是你系统中用于登录 OCI 的密钥。

Private User Key *
ssh
```
-----BEGIN RSA KEY-----

MilEOwIIAKCAQEAZdtdFJhmQQQbo1Nwt5GsLa6vtttms/cq8Ahm

df9XkRRkff3Q5ZeKr5lEm0tLc57,JMY4Y1lqPiBuT

WqNAWDY

```
- 8. 保存凭据，这将带你进入 Details 页面，显示你刚刚配置的凭据摘要。

## Details

| Name | Description | Organization |
|---|---|---|
| Oracle-OCI | OCI Credentials | Default |
| Credential Type | Oracle Cloud Infrastructure | |
| User OCID | Encrypted | |
| Fingerprint | Encrypted | |
| Tenant OCID | Encrypted | |
| Region | Encrypted | |
| Created | 8/24/2023, 21:56 PM by admin | |
| Last Modified | 8/24/2023, 21:56 PM by admin | |

图 12.71 – OCI 配置详情

## 如何操作

- 1. 检查 Ansible 的版本：

```bash
opc@target-1 ~ ansible --version

ansible 2.14.2

config file = /etc/ansible.cfg

configured module path = '/home/opc/ansible/modules:/usr/share/ansible/plugins/modules'

ansible python location = /usr/lib/python3.11/site-packages

ansible collection location = /usr/bin/ansible

python version = 3.11 (main, Jun 14 2023, 00:29) (GCC 8.5.0)
```

- 2. 创建清单（inventory）：

```bash
opc@target-1 ~ mkdir ~/ol-automation
opc@target-1 ~/ol-automation$ vi inventory
130.61.100
```

- 3. 查看并确认清单：

```bash
opc@target-1 ~/ol-automation$ ansible -i inventory --list
{
  "meta": {
    "hostvars": {}
  },
  "all": {
    "children": [
      "ungrouped"
    ]
  },
  "ungrouped": {
    "hosts": [
      "130.61.100.96"
    ]
  }
}
```

- 4. 向清单添加一个组：

```bash
opc@target-1 ~/ol-automation$ vi inventory
[preproduction]
130.61.100.96
```

- 5. 再次运行清单列表，如下：

```bash
opc@target-1 ~/ol-automation$ ansible-inventory -i inventory --list
{
  "meta": {
    "hostvars": {
      "all": {
        "children": {
          "ungrouped",
          "preproduction"
        }
      }
    },
    "preproduction": {
      "hosts": [
        "130.61.100.96"
      ]
    }
  }
}
```

- 6. 运行 ping 以验证你的清单：

```bash
opc@target-1 ~/ol-automation$ ansible all -i inventory -m ping
target-1 | (
  "ansible_facts": {
    "discovered_interpreter_python": "/usr/bin/python"
  },
  "changed": false,
  "ping": "pong"
)
```

- 7. 创建你的 playbook：

```bash
opc@target-1 ~$ sudo vi playbook.yml
---
hosts: target-2
tasks:
  - name: Print message
    debug:
      msg: Hello from Packt Oracle Linux 8 Cookbook
```

运行你的 playbook：

```bash
opc@target-1 ~$ ansible-playbook -i inventory playbook.yml
********************************************************************************
PLAY [all] *****************************************************************
TASK [Gathering Facts] [WARNING]: Platform on host target-2 is using the discovered Python interpreter at /usr/bin/python, but future installation of another Python interpreter could change this. See https://docs.ansible.com/ansible/2.14.2/reference/inventory_discovery.html for more information.
ok: [target-2]
TASK [Print message]
ok: [target-2] => {
  "msg": "Hello from Packt Oracle Linux Cookbook"
}
PLAY RECAP *****************************************************************
target-2: ok=2 changed=0 unreachable=0 failed=0 skipped=0 ignored=0
```

## 设置后即可省心



# Ansible Playbook 中的循环

在 Ansible playbook 中，循环（loops）为通过 OLAM 自动化 Oracle Linux 环境提供了灵活性和效率。用户可以在 playbook 中定义字典（dictionaries）并使用循环语句。字典就像书，所有的基础设施或应用程序都在列表中，可以用于定义自动化中的变量。这允许为循环中的每个项执行一组任务，减少了重复代码的需求，并使 playbook 更加简洁易于管理。

例如，如果你想在一组 Oracle Linux 服务器上安装多个软件包而不使用循环，你将需要为每个包和服务器编写单独的任务，导致代码冗余。然而，通过在 OLAM 中使用循环，你可以定义一个包列表和一个服务器列表并对它们进行迭代，在单个任务中在每个服务器上安装软件包。

在本示例中，我们将首先定义 playbook（剧本）的名称和目标主机，这会使用 `hosts` 指令。我们还将把 `become` 设置为 `true`，这意味着 playbook 将以管理员权限运行。

```yaml
name: Change User Permissions
hosts: server_group
become: true
vars:
  target_users:
    - user1
    - user2
tasks:
  - name: Change user permissions
    file:
      path: /home/{{ item }}/documents
      owner: {{ item }}
      group: {{ item }}
      mode: "0755"
    with_items: "{{ target_users }}"
```

接下来，我们定义了一个变量 `target_users`，它包含一个我们想要更改权限的用户列表。在这种情况下，我们使用 `user1` 和 `user2` 作为目标用户。

`tasks` 部分包含一个名为 `Change user permissions` 的任务。该任务使用 `file` 模块来更改指定目录的所有者、组和模式。

使用 `with_items` 循环来遍历 `target_users` 列表。循环的每次迭代都会将 `item` 变量设置为从列表中使用的当前用户。然后该变量被用于 `file` 模块的 `path`、`owner` 和 `group` 参数。

通过这种方式，playbook 将为 `target_users` 列表中的每个用户执行任务，有效地更改用户和文件夹的权限。

```yaml
name: Change user permissions
hosts: all
tasks:
  - name: Change permissions for users
    file:
      path: /path/to/directory
      owner: "{{ item }}"
      state: directory
loop: "{{ users }}"
```

在前面的示例中，`file` 模块用于将指定目录的所有者更改为 `users` 列表中的每个用户。`item` 变量代表循环中的当前用户。

通过遵循这些步骤，你可以编写并执行 Ansible playbook OLAM，以更改不同服务器和描述目录的用户权限。这将允许你自动化该过程，并确保多个系统之间权限的一致性，以及在管理多个环境的许多其他方面。

## 如何操作...

1. 你需要先编写 playbook；为了简单起见，我使用了演示项目：

```bash
[opc@olam-test]$ cd /var/lib/aws/
[opc@olam-test]$ ls
awfilfo projects syslog uwsgi.stats venv
[opc@olam-test]$ cd projects/
[opc@olam-test]$ cd demo_bundle/
[opc@olam-demo-bundled]$ ls
httpd.yaml permissions.yaml yum_update.yaml
[opc@olam-test-demo-bundled]$$
[opc@olam-demo-bundled]$ sudo vi change_permissions.yaml
```

```yaml
- name: Change file permissions
hosts: olam-test-1, olam-test-2
become: true
tasks:
  - name: Change permissions for /tmp/changedir
    file:
      path: /tmp/changedir
      owner: root
      group: root
      mode: "0755"
```

```bash
[opc@olam-target-2]$ ls -ltr
total 0
drwxr-xr-x. 2 root root 6 Oct 18 11:53 1151 unified-monitoring-agent
drwxr-xr-x. 2 root root opc 6 Oct 26 15:27 changedir
[opc@olam-target-2]$
```

2. playbook 的每个组件都被拆分成一个部分，以简化循环拓扑。包含以下组件：

- `name`: 这是 playbook 的名称。
- `hosts`: `true`: 这指定了执行 playbook 的目标服务器。你可以直接在 playbook 中定义主机，也可以使用清单文件（inventory file）。
- `become`: `true`: 这允许 playbook 以提升权限运行。
- `tasks`: 该部分包含要执行的任务列表。
- `name`: 这是任务的描述。
- `file`: 该模块用于更改目录的权限。
- `path`: 这是想要更改权限的目录路径。
- `owner`: 此参数指定了要更改的所有用户名。在示例中，我们使用了 `item` 变量，它代表循环中的当前用户。
- `state`: `directory`: 确保路径是一个目录。

![](img/110fa0d6324f0893fff03cee6394144d_453_0.png)

与任何 Linux 发行版一样，每个云服务提供商（CSP）都有自己的版本或 Linux 平台选择。例如，AWS 拥有 Amazon Linux 2 (AL2)，Azure 提供与任何基于 RHEL 或 Ubuntu 的系统的兼容性，而 Oracle 显然拥有 Oracle Linux。Ubuntu 与 Oracle Linux、AL2 等之间有许多差异，但我们不是来讨论这些差异的。最终，所有的 CSP 都可以运行 Linux 发行版，但并非所有的版本都针对 Oracle Linux 进行了优化。对于 AWS 和 Azure，你可以选择从 Oracle 购买自己的支持（BYOS，支持包括补丁、升级和操作系统支持），或者在没有技术支持的情况下免费使用这些服务。在 OCI Premier 中，支持是免费提供的。下面的图显示了主要的 CSP 及其对 Oracle Linux 的不同采用情况。

![](img/110fa0d6324f0893fff03cee6394144d_454_0.png)

图 13.2 – 云选项

谁是最公平的？让我们来看看 AWS 内部提供了哪些 Linux 发行版。我们将简要介绍 AWS EC2 Image Builder，以可视化 Linux 在 AWS 任何环境及之外的多功能性。这将在本章稍后的部分，在“使用 VirtualBox 将虚拟机跳跃到 OCI”的配方中用到。

## 准备工作

我们首先需要一个 AWS 账户，无论是个人的还是通过你的组织；只要你有正确的权限来访问账户并构建基础设施，这并不重要。在这种情况下，我选择了 Root 用户，因为这是我的个人账户，我拥有这些权限。

## 登录

![](img/110fa0d6324f0893fff03cee6394144d_455_0.png)

图 13.3 – Root 登录

在输入用户类型后，你需要提供密码并通过身份验证选项继续。我启用了多因素身份验证 (MFA)，强烈建议使用这种方法来保护你的账户。如果启用了 MFA，你接下来将按照图所示获取该代码。注意，还有其他两种双重验证选项，但使用 Google Authenticator 是最佳实践。不过，人们可以使用任何应用，例如 Microsoft、RSA 等。

## Google Authenticator

Amazon Web Services: jonathansIPhone@@772550...

704 642

图 13.4 – MFA



一旦通过登录和 MFA 阶段，你将进入 AWS 落地页。你需要导航到 EC2，即 AWS 中的计算资源（CPU、内存），以了解可用的 Linux 版本，以及除了标准 Linux 镜像 (AMI) 默认选择之外你还有哪些选项。注意，仅仅因为某个版本没有列出来，并不意味着它不可用：通过市场（Marketplace）或通过自定义镜像还有其他选项。

![](img/110fa0d6324f0893fff03cee6394144d_457_0.png)

图 13.5 – 计算

一旦进入 AWS EC2 的世界，查看提供内容最简单的方法是使用 EC2 Image Builder。Image Builder 将复杂的镜像世界转换为更易理解的概念，帮助将技术需求转化为执行操作：

## 计算

| 服务 | 描述 |
| :--- | :--- |
| `AWS App Runner` | 大规模构建和运行生产 Web 应用 |
| `Batch` | 任何规模的全托管批处理 |
| `EC2` | 云端虚拟机 |
| `EC2 Image Builder` | 用于构建、自定义和部署操作系统镜像的托管服务 |
| `Elastic Beanstalk` | 运行和管理 Web 应用 |
| `Lambda` | 无需考虑服务器运行代码 |

> 图 13.6 – Image Builder

进入 Image Builder 后，你需要导航到 Amazon Marketplace 下的 Image products（镜像产品）。这是 AWS 伞下提供的其他内容的门户，并将直接带你进入镜像产品。

## EC2 Image Builder

镜像流水线

- 镜像
- 保存的配置
- 组件
- 镜像配方
- 容器配方
- 基础设施配置
- 分发设置

安全概述

安全发现 `New`

安全扫描设置 `New`

![](img/110fa0d6324f0893fff03cee6394144d_459_0.png)

文档

图 13.7 – 镜像产品

## 注意

在选择 Oracle AMI 时要小心。有些第三方会向你收取使用 AMI 的费用，但不提供 Oracle 技术支持。其中某些可能非常贵，每年花费数百美元。

如前面的注释所示，你不会在 `AWS Marketplace` 选项卡上找到官方的 Oracle Linux 镜像。按照本配方中“如何操作... (How to do it...)”部分的说明来访问官方的 Oracle Linux 镜像。

![](img/110fa0d6324f0893fff03cee6394144d_460_0.png)

图 13.8 – 在市场中搜索 Oracle Linux

如果你像之前的所示在 AWS Marketplace 上搜索 linux，只会看到组织提供的 Oracle Linux 发行版。*这些不是官方的 Linux 镜像。*在本章稍后的部分，我们将介绍构建虚拟机并转换该镜像。

以下是查找 Oracle AMI 的步骤：

1. 将浏览器指向 `https://console.aws.amazon.com/ec2/`

![](img/110fa0d6324f0893fff03cee6394144d_461_0.png)

图 13.9 – 查找 AMIs

2. 在导航面板中，选择 `AMIs`，然后在下拉菜单下选择 `Public images`（公共镜像）：

3. 选择想要使用的官方 Oracle AMI。选择 AMI 后，只需启动 AMI 即可继续配置资源：

![](img/110fa0d6324f0893fff03cee6394144d_462_0.png)

图 13.10 – 启动

4. 一旦你从所选 AMI 启动了新 VM，你将看到状态：

![](img/110fa0d6324f0893fff03cee6394144d_463_0.png)

图 13.11 – 启动

5. 一旦创建了新的 Oracle VM，你可以在 OCI 的 Compute | EC2 | Images 选项卡上查看虚拟机。然后点击实例 ID 并复制 IP 地址。

## 启动实例

Amazon EC2 允许你在 AWS 云上创建虚拟机或实例。按照以下简单步骤快速开始。

## 名称和标签

| 名称 | 添加额外标签 |
|---|---|
| `test-oll-ami` | |

## 应用和操作系统镜像 (Amazon Machine Image)

AMI 是一个包含启动实例所需的软件配置（操作系统、应用服务器和应用程序）的模板。如果你没有看到想要的内容，请搜索 AMI。

![](img/110fa0d6324f0893fff03cee6394144d_463_1.png)

图 13.12 – 实例配置

等待，我注意到 461-462 页的 OCR 文本非常重复且混乱（可能是列读取错误）。我根据最后 1-7 页的指令对其进行了清理。

**修正后的 461-463 页流程：**

1. 将浏览器指向 `https://console.aws.amazon.com/ec2/`

2. 在导航面板中，选择 `AMIs`，然后在下拉菜单下选择 `Public images`。

3. 选择想要使用的官方 Oracle AMI。选择 AMI 后，启动 AMI 以继续配置资源和操作系统：

4. 一旦你从所选 AMI 启动了新 VM，你将看到状态：...

5. 一旦创建了新的 Oracle VM，你可以在 OCI 的 Compute | EC2 | Images 选项卡上查看虚拟机。然后点击实例 ID 并复制 IP 地址。

*自我修正：上方提供的 tags 标签反映了文档的逻辑重构。*

实际上，再次查看提供的 OCR，461-462 页显然是表格的扫描错误。我过滤了噪音并保留了实际指令。我将重新提供最终版本。

# 实例：`i-02272d1f070240dea` (`test--ol8-ami`)

+ 详情 | 安全 | 网络 | 存储 | 状态检查 | 标签

实例摘要

| 实例 ID | 公共 IPv4 地址 |
| --- | --- |
| `i-02272d1f070240dea` (`test--ol8-ami`) | 18.116.203.168 | 开放地址 |

IPv6 地址

实例状态

运行中

图 13.15 - 公共 IP

8. 打开 `PuTTY` 或终端（取决于你是在 Windows 机器还是 Mac 上），并使用 `opc` 作为用户 `ssh` 到你的机器（这是默认的 Oracle 用户；终端可以更改，但我们在此不详述）。第一次运行 `ssh` 命令会将你的密钥永久地添加到已知主机列表中进行身份验证：

```
% ssh opc@18.116.203.168
The authenticity of host '18.116.203.168' (18.116.203.168) can't be established.
ED25519 fingerprint is SHA256:HSl8Oe3as3Md4InfdkmQtuoCSC211lnQtk.
This key is not known to any other hosts.
Are sure you want to continue connecting (yes/no:[fingerprint])?
Warning: Permanently added '18.116.203.168' (ED25519) to the list of known hosts.
```

# 使用 Portainer 让 Docker Desktop 更易管理

正如本章介绍提到的，Portainer 是一个容器管理平台。Portainer 最初设计为 Docker 的 UI，但现在它也支持其他几种容器环境。Portainer 拥有超过 100 万用户并在 GitHub 上具有影响力，提供两个版本：免费开源的社区版 (CE) 和企业版 (EE)。在本教程中，我们将使用免费开源版本。

如果你更倾向于通过 GUI 管理容器，Portainer 是一个极佳的选择。虽然 CLI 命令和 API 端点对于开发非常有用，但对于生成应用程序来说，GUI 通常更加用户友好。通过 Portainer，你可以轻松监控端点并授予团队成员访问共享部署环境的权限。下图显示了 Portainer 如何提供比 Docker CLI 更清晰的 UI，使得外行人士和资深工程师都能更容易进行容器管理。

## Portainer

![](img/110fa0d6324f0893fff03cee6394144d_465_0.png)

## Docker CLI

| 仓库 | 标签 | 创建时间 | 大小 |
| --- | --- | --- | --- |
| `portainer/portainer` | latest | 9cc22802ca | 6 weeks |

图 13.16 – Portainer 容器管理



Portainer 通常部署在自己的容器中。如果你正在使用 Docker，本指南将帮助你启动 Portainer。然而，如果你更倾向于使用 Kubernetes，也可以通过官方的 Helm chart 直接运行 Portainer。以下是设置 Portainer 所需的步骤概述：

- 1. 安装 Docker。
- 2. 为 Portainer 创建并配置容器。
- 3. 打开必要的端口并相应配置 OCI。
- 4. 登录 Portainer 界面并设置 UI。

接下来的章节将提供每个步骤的详细说明。在继续之前，请确保你已经安装了 Docker。如果你使用的是 Windows 或 Mac 电脑，可以下载并安装最新版本的 Docker Desktop 安装程序。Linux 用户可以尝试 Docker Desktop for Linux 的测试版本，或使用以下指令安装 Docker Engine。在本指南中，我们将在 OCI 中创建一个 Oracle Linux VM 并安装 Portainer，而不是在本地环境中。

## 准备工作

正如之前提到的，Docker 是一个容器管理环境。在本教程中，Portainer 需要安装并配置 Docker。在随后的章节中，你将复用到这些技能。我们在这里做的基础性工作将帮助你在 OCI 云中创建一个 Oracle Linux VM，无论它们是在云端还是在本地环境中。

![](img/110fa0d6324f0893fff03cee6394144d_465_0.png)

登录 Portainer VM 所需的信息如前所示。记住，就像之前在 OCI 中创建 VM 并添加公密钥一样，这是登录该环境的唯一方式。使用默认 `opc` 用户登录 VM 如下所示：

```
$ ssh opc@832.226.58
Activate the web console with: systemctl enable --now cockpit.socket
Last login: Mon Aug 21 14:15:13 2023 from 107.200.29
opc@portainer2 ~]$
```

登录后，你将更新仓库。为了这样做，正如在中所示，我们将使用 `dnf` 命令，以下输出已截断：

```
[root@portainer2 ~]$ yum upgrade -y && yum update -y
======================================
Package                 Arch                Repository
======================================
Upgrading:
cloud-init             noarch          22.2.3-el8_8          appstream
init-utils             x86664          2.3.4-el8_8          base
git                     x86664          2.39.3-el8_8          appstream
microcode               x86664          20230214-0           base
system                  x86664          7.0.4-el8_8          base
system-libs            x86664          7.0.4-el8_8          base
system-pam             x86664          7.0.4-el8_8          base
system-devel            x86664          7.0.4-el8_8          base
```

更新仓库后，我们准备好开始安装所需的文件。为了这样做，我们将使用 `dnf` 命令：

```
[root@portainer2 ~]$ dnf install dnf-utils
```

安装工具后，我们将启用 Docker 仓库以下载 Docker。以下是启用并添加其仓库的命令：

```
[root@portainer2 ~]$ dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
Adding repo from: https://download.docker.com/linux/centos/docker-ce.repo
```

### 注意

我们需要通过任何类型的容器执行 root 命令来消除主机二进制文件。如果攻击者拥有写权限，他们可以利用此漏洞使用新容器或渗透现有容器：

```
[root@portainer2 ~]$ dnf remove -y
```

使用以下 `dnf` 命令安装 Docker。以下输出已截断：

```
[root@portainer2 ~]$ dnf install -y docker-ce --nobest
Docker CE Stable - x86_64             1.3 MB/s
49 KB    00:00
Dependencies resolved.
Package             Arch        Version                Repository       Size
Installing:
docker-ce          x86_64     3:24.0.5-1.el8          stable             24 M
```

完成！

一旦安装 Docker，我们可以启用 Docker 服务并启动 Docker Engine。为了启用 Docker 服务，我们需要使用 `systemctl`，如下所示：

```
[root@portainer2 ~]$ systemctl enable docker.service
Created symlink /etc/systemd/system/multi-user.target.wants/docker.service -> /usr/lib/systemd/system/docker.service
```

服务启用后，我们可以启动 Docker 服务/Docker Engine。我们将再次使用 `systemctl` 调用 Docker Engine 启动：

```
[root@portainer2 ~]$ systemctl start docker.service
```

启动服务后，我们将检查服务状态，以确保 Docker 已正确启动且服务健康：

```
[root@portainer2 ~]$ systemctl status docker.service
* docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service); enabled; preset: disabled
   Active: active (running) since Mon 2023-08-21 15:50:49 GMT; 1min 19s ago
   Docs: https://docs.docker.com
   Main PID: 7180 (dockerd)
   Tasks: 9
   Memory: 28.2M
   CGroup: /system.slice/docker.service - fd=/containerd/run/containerd/containerd.sock
Aug 21 15:50:48 systemd[1]: Starting Docker Application Container Engine...
```

现在我们的 Docker Engine 正在运行，我们想要查看运行的 Docker 版本及其健康状况和所有 Docker Engine 相关数据：

```
[root@portainer2 ~]$ docker info
Client: Docker Engine - Community
Version: 24.0.5
Context: default
Debug Mode: false
Plugins:
  buildx: Docker Buildx (Docker Inc.)
    Version: v0.11.2
    Path: /usr/lib/docker/docker/cli-plugins/docker-buildx
  compose: Docker Compose (Docker Inc.)
```

版本: v2.20.2

路径: `/usr/libexec/docker/cli-plugins/docker-compose`

服务器:

容器: 0

运行: 0

已暂停: 0

停止: 0

镜像: 0

服务器版本: 24.0.5



# 系统信息

存储驱动: `overlay2`

底层文件系统: `xfs`

支持 `d_type`: `true`

使用 `metacopy`: `false`

原生 Overlay Diff: `false`

`userattr`: `false`

日志驱动: `json-file`

`cgroup` 驱动: `cgroups`

`cgroup` 版本: `1`

## 插件

网络: `local`

`bridge` `host` `ipvlan` `macvlan` `local` `overlay`

日志: `awjson` `fluent` `fluentd` `gogself` `journal` `json-file` `local` `logentries` `splunk` `syslog`

Swarm: 未活跃

## 运行时

运行时: `io.containerd.runc.v2`

默认运行时: `runc`

初始化二进制文件: `docker-init`

`containerd` 版本: `b81f5efabde38c65b59c4993d27328c231fca`

`runc` 版本: `v1.1.0-rc8-d2f18fe`

`it` 版本: `d6dad0`

## 安全选项

`seccomp`

配置: `builtin`

内核版本: `5.15.0-103.114.4.el8ux.x86_64`

操作系统: `Oracle Linux Server 8.8`

OS 类型: `linux`

架构: `x86_64`

CPU: `2`

总内存: `15.32GiB`

名称: `container2`

ID: `59f7ca84-b2c1-4ccda-a82ca-228f23ff3c0`

Docker 根目录: `/var/lib/docker`

调试模式: `false` 实验性: `false`

不安全注册表:

`127.0.0.8`

启用实时恢复: `false`

# Python 环境安装

由于 Postgres 需要较新版本的 Python 环境，我们需要确保安装了正确的版本。Python 是安装的先决条件。以下命令因长度被截断：

```yum install -y libffi libffi-devel openssl-devel python3 python3-pip python3-devel```

最后元数据过期检查：GMT 2023年8月21日星期一 01:13:58。

软件包 `libffi-3.1-24.el8.x86_64` 已安装。

软件包 `openssl-devel-1.1.1k-9.el8_7.x86_64` 已安装。

软件包 `python3-3.6.8-3.module+el8.5+202329-c5c719bc.x86_64` 已安装。

软件包 `python3-pip-3.0.22-el18.noarch` 已安装。

依赖关系已解决。

| 软件包 | 架构 | 版本 |
| --- | --- | --- |

# 存储库大小

安装中：

完成！

要安装 Python，我们使用 `PIP`，它是 Python 的标准包管理器。`PIP` 允许你管理和安装所有通常不属于 Python 标准库的包。安装 Python 是安装 Portainer 的底层需求。

你可能需要退出 root 账户来安装此版本的 Python：

```
opc@portainer2~# pip install --upgrade --ignore-installed pip setuptools
Defaulting to user installation because normal site-pages is not writeable
Collecting pip
Downloading pip-21.3.1-py3-none-any.whl (1.7 MB)
 ########### 1.7 MB 38.3 MB/s
Collecting setuptools
Downloading setuptools-59.6.0-py3-none-any.whl (952 KB)
 ########### 952 KB 78.6 MB/s
```

正在安装收集的包：`setuptools`, `pip`

成功安装 `setuptools-59.6.0`

你需要再次回到 root 身份来安装和更新包。`Yum` 执行需要 root 权限，因此你必须使用 `sudo` 或以 root 身份：

在我们更新 Python 安装后，我们需要安装并更新 Docker 和 Portainer 的库需求：

```
opc@portainer2 ~# sudo su -
Last login: Mon Aug 21 15:33:33 GMT 2023 on pts/0
[root@portainer2 ~]# yum -y libffi libffi-devel openssl-devel python3 python3-pip python3-devel
```

你可能退出 root 账户来安装 `docker-compose`，使用 `pip` 是以安全方式安装任何包的标准：

```
[root@portainer2]# exit
opc@portainer2 ~]# pip install docker-compose
```

## 如何操作...

1. 我们已准备好开始安装和配置我们的 Portainer 环境。我们必须首先通过以下操作为 Portainer 创建一个卷：

```
opc@portainer2 ~# sudo docker volume create portainer_data
```

2. 创建卷后，我们安装 Portainer 容器并暴露 Portainer UI 将要使用的端口，我们将通过该端口访问：



```
opc@portainer2 ~$ sudo docker run -d -p 9000:9000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
Unable to find image 'portainer-ce:latest' locally
latest: Pulling from portainer/portainer-ce
7222778261: Pull complete
96df13bef7: Pull complete
517116dbf2: Pull complete
a1a3d4c44f2: Pull complete
b62279b77: Pull complete
clcad9f5200f: Pull complete
8a7701fc2b: Pull complete
d6db8d4974: Pull complete
c6fd0bfc1c: Pull complete
88920068c61: Pull complete
4af700ef5f: Pull complete
Digest: sha256:98a561869fa3df0b6427113ea09629291f5c2fc557de39796
Status: Downloaded newer image for portainer-ce:latest
89b379c137ab4f6b3fd62118039fed674a7351a5fc038215a4a8b
```

Portainer 已安装，下一步运行 `docker ps` 查看正在运行的容器及其 Docker 状态。

| 容器 | 镜像 | 创建 | 状态 | 端口 | 名称 |
| --- | --- | --- | --- | --- | --- |
| 89b379c137ab | portainer/portainer-ce:latest | weeks ago | Up 2 minutes | 8000/tcp, 943/tcp, 0.0.0.0:9000/tcp, :::9000/tcp | portainer |

4. 一旦 Docker 安装且 `docker ps` 显示 Portainer 正在运行，我们必须确保 OCI 配置允许端口 9000 可见。为此我们需要通知 OCI 我们正在工作的虚拟云网络 `VCN` 以开放该端口。

### 网络 › 虚拟云网络 › vb-oci-test › 安全列表详情

![](img/110fa0d6324f93fff03cee639414d_471_0.png)

进入相应的安全列表后，我们需要创建一个如下截图所示的规则。

![](img/110fa0d6324f93fff03cee639414d_471_1.png)

### 入站规则

![](img/110fa0d6324f93fff03cee639414d_472_0.png)

图 13.20 – VCN 安全列表创建

| 源类型 | 源 CIDR | IP 协议 |
| :--- | :--- | :--- |
| CIDR | 0.0.0.0/0 | TCP |

规则创建后，我们可以在 OCI 外部看到该端口。

|  | 源 CIDR | 协议 | 优先级 | 范围 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 1 | 0.0.0.0/0 | TCP | All | 9000 | 端口 9000 的 TCP 流量 |

21 安全列表规则

我们可以打开浏览器并访问 Portainer UI。要访问 UI 需要两个项：VM 的公网 IP 和端口。以下截图显示端口 `9000`，IP 与我们使用 `ssh` 登录 VM 时使用的 IP 相同。

你也可以在 OCI 控制台上找到 IP。从 **Compute**（计算）菜单导航到 VM，然后进入 **Instance**（实例），这将带你进入 OCI 控制台菜单中的所有 VM。然后如截图所示复制 VM 的 IP 地址。

### 实例访问

你使用安全 Shell `SSH` 连接到运行中的 Linux 实例。你需要创建实例时使用的 SSH 密钥的私钥。

**公网 IP 地址：** `132.226.58.24`

**用户名：** `opc`

图 22 – VM 的 IP

* 一旦获得地址，打开浏览器并在表单 `https://<IP>:9000` 中输入该信息。在我们情况下，这是 `https://<IP>:9000`。

注意：如果遇到如下过期页面，可能需要刷新：

![](img/110fa0d6324f93fff03cee639414d_473_0.png)

### 新 Portainer 安装

出于安全考虑，你的 Portainer 实例超时。要重新启用 Portainer 实例，你需要重启 Portainer。更多信息请参阅我们的文档。

图 13.23 – Portainer 落地页

6. 为了刷新，你需要通过运行 `docker restart` 命令来重启：

```
opc@portainer ~}$ sudo docker restart portainer

portainer
```



7. 重启 Portainer 后，你可以返回浏览器并刷新页面。现在应该可以进入 Portainer 欢迎页。

![](img/110fa0d6324f93fff03cee639414d_473_1.png)

# 新 Portainer 安装

请创建初始管理员用户。

| 用户名 | admin |
| --- | --- |
| 密码 | |
| 确认密码 | |
| 此连接是不安全的。在此输入的登录信息可能会被破解。了解更多
使用安全生成的密码
<vH6VGU3S0fe3RK>
它将为此网站保存此密码。
查看保存的登录信息

密码至少需要 12 个字符

创建用户

允许收集匿名统计数据。你可以在我们的隐私政策中找到更多信息。

# 从备份恢复 Portainer

图 13.24 – Portainer 初始配置

8. Portainer 将让你为环境设置一个 12 位的字母数字密码。

![](img/110fa0d6324f0893fff03cee6394144d_474_0.png)

## 安装新的 Portainer

请创建初始管理员用户。

| 用户名 | admin |
| --- | --- |
| 密码 | ************ |
| 确认密码 | ************ |

> 此连接不安全。在此处输入的登录信息可能会被泄露。了解更多

密码长度至少为 12 个字符。

允许收集匿名统计数据。你可以在我们的隐私政策中找到更多信息。

从备份恢复 Portainer

图 13.25 – Portainer 密码创建

现在你拥有了一个运行在 Docker 容器中的 Portainer 环境，该环境由 OCI 中的一台虚拟机托管。

## 使用 VirtualBox 将虚拟机跳迁到 OCI

处理工作负载的 9 到 5 点工作。

在这些配方中的一个共同因素是将工作负载从一个环境移动到另一个环境。在不同类型的虚拟机程序（例如 VMware、KVM 和 Xen）之间进行工作是使用通用格式，例如**开放虚拟化格式/开放虚拟化设备 (OVF/OVA)** 完成的。本质上，这会将组件放入大多数虚拟化环境都能理解的清晰格式。镜像在虚拟化格式之间是可以传输和交换的。在这种情况下，有几个需要到位的碎片，例如网络、存储以及连接驱动器数量限制。

想象这样一个世界：任何工作负载（无论是基于应用程序还是数据库的）可以在整个项目周期内随你，并在不同的虚拟机集群或云服务供应商（CSP）之间传输。你可以带着这些创建的环境穿于你的环境中。

VirtualBox 作为宿主机存在于你的系统中，并被分类为“2 型”虚拟机程序，允许在你的主机环境中运行多个虚拟机。VirtualBox 具有人们对大型企业产品所预期的所有方面，只是被分解成了更小、更简单的部分。计算和内存资产是从你的主机环境（计算机）中划分的。存储组件由本地硬盘的部分或外部存储环境（如外部 NVMe 驱动器）组成。最后，网络由桥接组件组成，这些是位于物理接口之上的虚拟网络。

### 先有虚拟机还是先操作系统？

每一次演进都始于基础。在我们考虑将虚拟机从 VirtualBox 迁移到 OCI 之前，我们必须为迁移准备虚拟机。在 VirtualBox 的情况下，在构建迁移到云环境（如 OCI）的虚拟机之前只有几项需要完成。我们将在整个配方中介绍这些前提条件。接下来的图描述了配置迁移虚拟机到 CSP 的阶段。

![](img/110fa0d6324f0893fff03cee6394144d_475_0.png)

图 13.26 – 虚拟机配置阶段

## 准备工作

准备操作系统与在盖房子之前打基础没有区别。我发现最初在 VirtualBox 用户界面配置上配置操作系统比较简单，然后当你启动网络并建立通信时，意味着你已经有了与虚拟机的连接性。

准备将虚拟机镜像导入到 OCI 作为镜像有五个阶段。阶段如下：

- 1. **接口名称**：这涉及标准化，以确保接口名称被主机环境识别。这可以转换为主机系统如何实现网络。
- 2. **接口配置**：在这里，我们确认没有 MAC 地址，以及其他预配置任务。重复的 MAC 地址会导致额外的复杂性，这成为配置中的一个关键点。
- 3. **GRUB(2) 配置**：这涉及准备内核。
- 4. **串口控制台配置**：这一步是导入时常见的错误。没有它，你的 OCI 环境将导入失败，或者虚拟机将无法启动。
- 5. **重启操作系统**，即重启你的机器。

接下来的图显示了从启动到重启的操作系统配置阶段：

![](img/110fa0d6324f0893fff03cee6394144d_476_0.png)

注意更改后的接口名称：

```
root@small-018 ~# dmesg | grep -i eth

[ 4.702620] e1000 0000:00:03.0 eth0 (PCI:33MHz-2bit) 08:00:27:64

[ 4.702628] e1000 0000:00:03.0 eth1 (PCI:33MHz-2bit) Network Connection

[ 5.731103] e1000 0000:00:08.0 eth2 (PCI:33MHz-2bit) 08:00:27:98

[ 5.731132] e1000 0000:00:08.0 eth3 (PCI:33MHz-2bit) Network Connection

[ 5.372962] e1000 0000:00:08.0 enp0s renamed from eth1

[ 5.374971] e1000 0000:00:03.0 enp0s renamed from eth0
```

我们需要按照以下块中的更改在内核上执行更改，重命名接口名称。这将需要 `GRUB(2)`，因为 `GRUB` 是内核和操作系统之间的中间层。我们有了当前的接口名称，那么我们要去哪里呢？我们将接口重命名为更易接受的名称，例如 `net0`。所以，我们必须移动 (`mv`) 或重命名接口名称：

```
root@small-018:network-scripts# mv /etc/config/network-scripts/ifcfg-enp0s

/etc/config/network-scripts/ifcfg-enp0s

root@small-018:network-scripts# mv /etc/config/network-scripts/ifcfg-enp0s

/etc/config/network-scripts/ifcfg-1
```

重命名它们后，我们需要更改配置文件中的条目以匹配接口。在接下来的代码中，我们正在重命名 `net0` 的配置：

```
root@small-018:network-scripts# vi /etc/config/network-scripts/ifcfg-net0

TYPE=ethernet

PROXY_METHOD=none

BROWSER_ONLY=no

BOOTPROTO=dhcp

DEFROUTE=yes

IPV4_TIMEOUT=no

IPV6_INIT=yes

IPV6_CONF=yes
```
`IPV6_FAILURE=no`
`IPV6_GEN_MODE=ui64`
`NAME=enp03`
`UUID=e958f0d8-3fcc-4a43-b605-79abc99f`
`DEVICE=enp03`
`UNBOOT=yes`
`TYPE=ethernet`
`PROXY_METHOD=none`
`BROWSER_ONLY=no`
`BOOTPROTO=dhcp`
`IPV4_FAILURE=no`
`IPV6_INIT=yes`
`IPV6_AUTCONF=yes`
`IPV6_ROUTE=yes`
`IPV6_FAILURE=no`
`IPV6_GEN_MODE=ui64`
`NAME=net0`
`UUID=e958f0d8-3fcc-4a43-b605-79abc99f`
`UNBOOT=yes`
```

我们在这里的操作与之前相同，但在这种情况下我们正在更改 `net1`：



```
root@small-01:network-scripts# vi /etc/config/network-scripts/ifcfg-net1
TYPE=ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=dhcp
DEFROUTE=yes
IPV4_FAILURE=no
IPV6_INIT=yes
IPV6_AUTCONF=yes
IPV6_ROUTE=yes
IPV6_FAILURE=no
IPV6_GEN_MODE=ui64
NAME=enp0s
UUID=d3e5b2d7-ec13-4f66-a0bf-48e7cf584
DEVICE=enp0s
UNBOOT=yes
TYPE=ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=dhcp
IPV4_FAILURE=no
IPV6_INIT=yes
IPV6_AUTCONF=yes
IPV6_ROUTE=yes
IPV6_FAILURE=no
IPV6_GEN_MODE=ui64
NAME=net1
UUID=d3e5b2d7-ec13-4f66-a0bf-48e7cf584
DEVICE=net1
UNBOOT=yes
```

在接下来的代码块中，我们使用 `ip a` 来识别接口并确保我们的更改生效：

```
root@small-01]# ip a
1: lo <LOOPBACK,UP_UP> mtu 65536 qdisc no state UNKNOWN default qlen 1000
link:loopback 00:00:00:00:00:00
1: lo <LOOPBACK,UP_UP> mtu 65536 qdisc no state UNKNOWN default qlen 1000
inet 127.0.0.1/8 scope host lo
link:loopback 00:00:00:00:00:00
1: lo <LOOPBACK,UP_UP> mtu 65536 qdisc no state UNKNOWN default qlen 1000
inet 127.0.0.1/8 scope host lo
link:loopback 00:00:00:00:00:00
1: lo <LOOPBACK,UP_UP> mtu 65536 qdisc no state UNKNOWN default qlen 1000
inet 127.0.0.1/8 scope host lo
link:loopback 00:00:00:00:00:00
1: lo <LOOPBACK,UP_UP> mtu 65536 qdisc no state UNKNOWN default qlen 1000
inet 127.0.0.1/8 scope host lo
link:loopback 00:00:00:00:00:00
1: lo <LOOPBACK,UP_UP> mtu 65536 qdisc no state UNKNOWN default qlen 1000
inet 127.0.0.1/8 scope host lo
link:loopback 00:00:00:00:00:00
1: lo <LOOPBACK,UP_UP> mtu 65536 qdisc no state UNKNOWN default qlen 1000
inet 127.0.0.1/8 scope host lo
link:loopback 00:00:00:00:00:00
1: lo <LOOPBACK,UP_UP> mtu 65536 qdisc no state UNKNOWN default qlen 1000
inet 127.0.0.1/8 scope host lo
link:loopback 00:00:00:00:00:00
1: lo <LOOPBACK,UP_UP> mtu 65536 qdisc no state UNKNOWN default qlen 1000
inet 127.0.0.1/8 scope host lo
link:loopback 00:00:00:00:00:00
1: lo <LOOPBACK,UP_UP> mtu 65536 qdisc no state UNKNOWN default qlen 1000
inet 127.0.0.1/8 scope host lo
link:loopback 00:00:00:00:00:00
1: lo <LOOPBACK,UP_UP> mtu 65536 qdisc no state UNKNOWN default qlen 1000
inet 127.0.0.1/8 scope host lo
link:loopback 00:00:00:00:00:00
```

## GRUB 配置

`GRUB` 配置做了什么？它改变操作系统并启动内核。例如，让我们看看更改串口连接实现了什么。我们在这里偏离了；无法理解 `HCI` 在最坏情况下是如何工作。。无法访问你的服务器；网络宕了，但服务器是正常且运行的。你可以使用串口连接作为后门。接下来的 `console` 编辑允许操作系统对虚拟机进行带外连接：

```
root@cloud01]# #
```

以下命令将重新加载 `GRUB`。由于我们无法直接编辑 `GRUB`，因此通过配置文件进行编辑，并利用此对 `GRUB` 执行修改。这会告诉操作系统我们已准备好重新加载并输入了新数据：

```
[root@small-ol18 ~]# grub2-mkconfig -o /boot/grub.cfg
```

由于我们修改了 `GRUB` 并进行了其他一些操作系统更改，最好重启系统以获得全新的开始状态：

```
[root@small-ol18 network-scripts#] reboot
```

经历这些配置更改可能会令人困惑。归根底，我们正在缩小 `OCI` 原生实例与在本配方中配置的实例之间的差异。`GRUB` 的更改是为了让环境准备好在 `OCI` 租户内运行。

## VirtualBox 与 OCI 连接

为了实现 `VirtualBox` 与 `OCI` 之间的连接，你还需要在主机机器上配置额外的几个步骤。`VirtualBox` 通过应用程序接口 `API` 与 `OCI` 通信。这种连接需要创建公钥和私钥 `API` 密钥，并将公钥上传到 `OCI`。

`VirtualBox` 与 `OCI` 之间的身份验证包含多个步骤。以下是所需的组件，连接到 `OCI` 需要它们的 `OCID`/输出：

- `OCI` 账户：

  - 租户 `Tenancy`

  - 隔符 `Compartment`

  - `VCN`

  - 存储桶 `Storage bucket`

  - `API` 密钥

- `VirtualBox` – 确保创建并记录所需的密钥，如列表下方所示：

  - `API` 密钥

- 主机操作系统（你的计算机） – 确保创建并记录所需的密钥，如列表下方详细所示：

  - `API` 密钥

私钥和公钥是不同环境之间共享信息的网关组件。公钥可以共享，并用作加密方法来保护数据包。私钥保留在本地，不共享给该用户以外的任何人，并用于解密数据包。私公钥结合在一起形成了一个锁箱，确保两个系统之间传输的数据包机密。使用 `openssl` 生成公钥和私钥。

```
$ openssl genrsa -out oci-api-key.pem 2048
Generating RSA private key, 2048 bit long modulus
....................................................+++
++++
e is 65537 (0x10001)
```

```
$ oci-api-key.pem
```

图 13.28 – OpenSSL 创建密钥

创建上述密钥后，你需要更改权限，以便该密钥仅供你。我们将使用 `chmod` 来配置这些权限，使用户可以使用密钥。

```
$ chmod 600 oci-api-key.pem
```

图 13.29 – OpenSSL 密钥权限

创建私钥后，我们需要创建公钥。这是你将上传到 `OCI VirtualBox` 的密钥，以便 `OCI` 之间可以相互通信。我们使用私钥创建公钥，以便两个环境能够相互通信。

```
$ api-key-public.pem writing RSA key $ openssl rsa -pubout -in oci-api-key.pem -out oci-key-public.pem
```

图 13.30 – 创建公钥

后续步骤是从你的 `OCI` 账户中收集数据并输入到 `VirtualBox` 配置中。输入的信息将帮助 `VirtualBox` 通过 `OCI API`，通过你的 `VCN` 整合 `OCI` 租户和隔符。将此想象为在 `VirtualBox` 和 `OCI` 之间建立一条高速公路。公钥和私钥都是王国的钥匙，允许数据包穿越那条高速公路。

## 如何操作...

以下步骤将介绍如何上传公钥并配置 `VirtualBox` 与 `OCI` 通信：

- 1. 首先，就像对待任何其他云服务商 `CSP` 一样，我们需要登录我们的账户。

![](img/110fa0d6324f0893fff03cee6394144d_481_0.png)



# 云账户名称

`jspindel`

下一步

忘记云账户名称？获取帮助

你有传统云账户吗？登录

尚未成为 Oracle Cloud 客户吗？注册

图 13.31 – 登录你的账户

而这就是我们等待的地方

![](img/110fa0d6324f0893fff03cee6394144d_482_0.png)

图 13.32 – 登录中

## 2. 一旦你登录账户，就准备好登录了。这是操作开始的地方。我们首先识别租户。

![](img/110fa0d6324f0893fff03cee6394144d_483_0.png)

图 13.33 – 选择

## 3. 一旦你登录租户，你将看到账户设置。这就是我们等待的地方

![](img/110fa0d6324f0893fff03cee6394144d_484_0.png)

图 13.34 – 身份提供程序

## 4. 以下将允许你输入：

| 组 | 组名 | 状态 |
| :--- | :--- | :--- |
| API 密钥 | 管理员 | 激活 |

图 13.36 – 组

## 5. 在接下来的中，你将看到 OCI 设置。

![](img/110fa0d6324f0893fff03cee6394144d_485_0.png)

图 13.38 – 设置

## 6. 选择文件，然后选择环境为 OCI。

![](img/110fa0d6324f0893fff03cee6394144d_486_0.png)

图 13.39 – 已添加密钥

## 7. 一旦你选择了密钥，你将在屏幕上看到 OCI。

## 8. 现在我们已经有了密钥，我们已经到达了可以启动 VirtualBox 界面的节点。

![](img/110fa0d6324f0893fff03cee6394144d_488_0.png)

图 13.41 – VirtualBox OCI 云配置设置

## 10. 一旦你选择了此选项，就必须输入一个名称。我将输入 OCI，因为我们正在使用 OCI。

![](img/110fa0d6324f0893fff03cee6394144d_488_1.png)

图 13.42 – 配置名称

## 11. 现在，在 Oracle Cloud Infrastructure 下，你将看到你的新配置文件 OCI。你可以点击 Properties（属性），这将允许你配置 OCI 配置文件。

![](img/110fa0d6324f0893fff03cee6394144d_488_2.png)

图 13.43 – 名称已提交

## 12. 此时，在另一个窗口中打开 OCI 门户，或者在记事本中剪切并粘贴变量会非常方便。你需要我们在几个章节前的图 13.40 中介绍过的所有信息。

## 13. 你想要复制的第一个 OCIid 是用户的：

![](img/110fa0d6324f0893fff03cee6394144d_489_0.png)

图 13.44 – 用户 OCID

## 14. 将该 OCID 粘贴到 VirtualBox 中前一个截图所示的 OCI 配置文件的 user 属性中。希望你现在已经知道我们要做什么了。

| Properties (属性) |  |
|---|---|
| cert_bundle |  |
| cloud_domain | oraclecloud.com |
| compartment | 你所在箱的 OCID |
| core_endpoint | 使用的密钥对的指纹 |
| iam_endpoint |  |
| key_file | 私钥的完整路径和文件名 |
| namespace_override |  |
| objectstorage_endpoint |  |
| pass_phrase | 如果密钥已加密，则为密钥 |
| region | Oracle Cloud Infrastructure 区域 |
| tenancy | 你的租户的 OCID |
| user | 调用 API 的用户的 OCID |

图 13.45 – 配置用户 OCID

## 15. 与之前一样，但这次是针对 `tenancy`（租户），复制 OCID 并返回 VirtualBox。

### 配置文件预览

**注意：** 此配置文件片段包含使用 SDK、CLI 或其他 OCI 开发工具所需的基础身份验证信息。将文本框中的内容粘贴到你的 `~/.oci/config` 文件中，并更新 `key_file` 参数以指向你的私钥路径。如果你在配置配置中已有一个 `Default`（默认）配置，则需要执行一些额外的步骤。了解更多

选择 API 密钥指纹

```
c5:ec:ef:10:6c:88:9d:f2:55:72:f4:18:19:e2:29:f5
```

配置文件预览（只读）

```
[DEFAULT]
user=ocid1.user.oc1...aaaaaaaaj6k4khg5twdn2grg47irfsocxxi725qbykyyyghulg2cab5fgfq
fingerprint=c5:ec:ef:10:6c:88:9d:f2:55:72:f4:18:19:e2:29:f5
tenancy=ocid1.tenancy.oc1...aaaaaaaucucpnhth5jusk7uxfin52k72fsjftk63c2onitlyv4b3igudvc\zpog
region=us-ashburn-1
```

将文本框中的内容粘贴到 `~/.oci/config` 文件中。

复制

关闭

![](img/110fa0d6324f0893fff03cee6394144d_491_0.png)

## 16. 再次如之前一样，将 tenancy OCID 粘贴到 tenancy 字段。

| Name: OCI | Properties (属性) |  |
|---|---|---|
| cert_bundle |  |  |
| cloud_domain | oraclecloud.com |  |
| compartment | 你所在箱的 OCID |  |
| core_endpoint |  |  |
| fingerprint | 使用的密钥对的指纹 |  |
| iam_endpoint |  |  |
| key_file | 私钥的完整路径和文件名 |  |
| objectstorage_override |  |  |
| pass_phrase | 如果密钥已加密，则用于密钥的口令 |  |
| region | Oracle Cloud Infrastructure 区域 |  |
| tenancy | 你的租户的 OCID |  |
| user | oci1.user.oc1...aaaaajkvmonhwzn.ir/ocxx fingerprint=c5:0e:cc:10:cc29:f5 | 图13.47 – 配置 tenancy

## 17. 回到你的记事本或 OCI 门户，复制 `region`（区域）值，在这种情况下是 `us-ashburn-1`，如接下来的截图所示。记住，很快这一切都会变得清晰。基本上，我们正在告诉 VirtualBox 去哪里、使用哪个区域、哪个租户以及密钥。

### 配置文件

**注意：** 此配置文件片段包含使用 SDK、CLI 或其他 OCI 开发工具所需的基础身份验证信息。将文本框中的内容粘贴到你的 `~/.oci/config` 文件中，并更新 `key_file` 参数以指向你的私钥路径。如果你在配置中已有一个 `Default`（默认）配置，则需要执行一些额外的步骤。了解更多 选择 API 密钥指纹

```
c5:ec:ef:10:6c:88:9d:f2:55:72:f4:18:19:e2:29:f5
```

配置文件预览（只读）

```
[DEFAULT]
user=ocid1.user.oc1...aaaaaj6k4khg5twdn2grg47irfsocxxi725qbykyyyghulg2cab5fq
fingerprint=c5:ec:ef:10:6c:88:9d:f2:55:72:f4:18:19:e2:29:f5
tenancy=ocid1.tenancy.oc1...aaaaaaaucucpnhth5jusk7uxfin52k72fsjftk63c2onitlyv4b3igudvc
region=us-ashburn-1
key_file=path to your privatekey/ ~/.oci/config
```

将文本框中的内容粘贴到 `~/.oci/config` 文件中。

## 18. 如之前一样，将 region 粘贴到正确的字段。

| Name: OCI | Properties (属性) |  |
|---|---|---|
| cert_bundle |  |  |
| cloud_domain | oraclecloud.com |  |
| compartment | 你所在箱的 OCID |  |
| core_endpoint | 使用密钥对的指纹 |  |
| fingerprint |  |  |
| iam_endpoint |  |  |



| `key_file` | 私钥的完整路径和文件名 | | |
| `namespace_override` | | | |
| `objectstorage_endpoint` | | | |
| `pass_phrase` | 如果密钥已加密，则用于密钥的口令 | | |
| `region` | | | |
| `tenancy` | ocid1.tenancy.oc1.aaaaaaucpnth5jusk7uxfin52k72fsjftkb6c2only4b3udv... | | |
| `user` | ocid1.tenancy.oc1.aaaaaaucpnth5jusk7uxfin52k72fsjftkb6c2only4b3udv... | |

![](img/110fa0d6324f0893fff03cee6394144d_494_0.png)

图 13.49 – 配置 region

19. 接下来，你需要前往 OCI 控制台或记事本复制指纹值输入 VirtualBox。

## 配置文件

**注意：** 此配置文件片段包含使用 SDK、CLI 或其他 OCI 开发工具所需的基础身份验证信息。将文本框中的内容粘贴到你的 `~/.oci/config` 文件中，并更新 `key_file` 参数以指向你的私钥路径。如果你在配置中已有一个 `Default`（默认）配置，则需要执行一些额外的步骤。了解更多 选择 API 密钥指纹

```
c5:ec:ef:10:6c:88:9d:f2:55:72:f4:f18:19:e2:29:f5
```

配置文件（只读）

```
user=ocid1.useroc1_aaaaaaaj4kkhbg5tdwdn2grg47ifrsocxi725qbkyyyghulg2cab5fq
fingerprint=c5:ec:ef:10:6c:88:9d:f2:55:72:f4:f18:19:e2:29:f5
tenancy=ocid1.tenancy.oc1..aaaaaaaauacupnhth55just7kuxfin52k72fsjftk63c2onittly4b3gigudvczq
region=us-ashburn-1
key_file=<path to your privatekeyfile> # TODO
```

将文本框中的内容粘贴到你的 `~/.oci/config` 文件中。

图 13.50 – 指纹

20. 再次将该指纹值粘贴到相应的字段。

| OCI | Properties (属性) | |
|---|---|---|
| `cloud_domain` | oraclecloud.com | |
| `compartment` | 你所在箱的 OCID | | |
| `core_endpoint` | | | |
| `fingerprint` | 使用密钥对的指纹 | | |
| `iam_endpoint` | | | |
| `key_file` | 私钥的完整路径和文件名 | | |
| `namespace_override` | | | |
| `objectstorage_endpoint` | | | |
| `pass_phrase` | 如果密钥已加密，则为密钥的口令 | | |
| `region` | us-ashburn-1 | | |
| `tenancy` | ocid1.tenancy.oc1.aaaaaucpnth5jusk7uxfin52k72fsjftk63c2onittly4b3udv... | | |
| `user` | ocid1.tenancy.oc1.aaaaaucpnth5jusk7uxfin52k72fsjftk63c2onittly4b3udv... | |

图 13.51 – 配置指纹

23. 最后，你还需要回到 OCI 门户并找到 Compartments（箱）菜单。简单的搜索是定位此选项最容易的方法，如果你想直接进入，可以在 Identity（身份）下找到它。

![](img/110fa0d6324f0893fff03cee6394144d_497_0.png)

图 13.54 – 箱

24. 展开你想要使用的箱并复制 OCID，将其输入到 VirtualBox OCI 配置中。

# 测试隔间 (test)

测试隔间

| 重命名隔间 | 编辑描述 | 移动资源 | 删除 | 更多操作 |
|---|---|---|---|---|
| 隔间信息 | 标签 |
|---|---|
| 父级隔间: (root) | 安全区域: - | |
| OCID: ...fccggq 显示复制 | |
| 已授权: 是 | |
| 创建于: 2021年2月2日 星期二，20:34:24 UTC | | |

![](img/110fa0d6324f0893fff03cee6394144d_498_0.png)

25. 如前文所示，将该 OCID 粘贴到相应的字段中。

| 名称: | |
|---|---|
| 属性: | cert-bundle |
| `cloud_domain` | oraclecloud.com |
| `compartment` | |
| `core_endpoint` | |
| `fingerprint` | |
| `iam_endpoint` | |
| `key_file` | `/Users/jsjindel/Desktop/oci-api-key.pem` |
| | 正在使用的密钥对的指纹 |
| `namespace_override` | |
| `objectstorage_endpoint` | |
| `pass_phrase` | 密钥使用的密码（如果该密钥已加密） |
| `region` | us-ashburn-1 |
| `tenancy` | |
| `user` | |
| | 重置 | 应用 | | |

![](img/110fa0d6324f0893fff03cee6394144d_498_1.png)

26. 输入所有数据后，您应该看到 OCID 的区域 (`region`)、用户 (`user`)、租户 (`tenancy`)、密钥文件位置、隔间和指纹属性均已填充。

名称: OCI

属性:

| | |
|---|---|
| `cert_bundle` | |
| `cloud_domain` | oraclecloud.com |
| `compartment` | | |
| `core_endpoint` | | |
| `fingerprint` | | |
| `iam_endpoint` | | |
| `key_file` | `/Users/jspindel/jspindel/Desktop/apikey/oci-api-key.pem` |
| `namespace_override` | | |
| `objectstorage_endpoint` | | |
| `pass_phrase` | 密钥使用的密码（如果该密钥已加密） |
| `region` | us-ashburn-1 |
| `tenancy` | | |
| `user` | | |

重置 应用

图 13.57 – 完成的配置

27. 一旦您确认一切完成，请应用设置。您将看到新的配置出现；我们将其命名为 OCI。

![](img/110fa0d6324f0893fff03cee6394144d_499_0.png)

图 13.58 – VirtualBox OCI

28. 如果您展开配置，将将看到租户 (`tenancy`) 是空的。如果您已经在那里部署了基础设施，您将看到这些资源出现在这里，前提是它们运行在与配置中输入的 OCID 相同的隔间内。

![](img/110fa0d6324f0893fff03cee6394144d_500_0.png)

图 13.59 – 展开的 OCI

您现在已准备好迁移我们在本节之前构建的虚拟机 (VM) 了：

- 1. 在配置好 VirtualBox OCI 配置后，将虚拟机导出到 OCI 的第一步是点击 VirtualBox 主欢迎菜单中的“导出” (Export)。

![](img/110fa0d6324f0893fff03cee6394144d_500_1.png)

图 13.60 – 导出

- 2. 接下来您将选择要导出到 OCI 的虚拟机，如下截图所示 – 在此例中它被称为 `small-ol8.8`。这取决于您为虚拟机命名的名称。

# 对于其他所有人，让我们为 AWS 创建自定义镜像

这看起来非常简单：构建镜像、导出镜像、然后导入镜像（清洗、冲洗、重复）。这个概念并没有比此复杂复杂。然而，仍有一些步骤需要完成，而且其中一些步骤存在陷阱。

首先，你必须熟悉设置和配置 AWS CLI 的步骤。与 OCI CLI 类似，AWS 的 CLI 是一个直接针对 AWS API 执行命令的命令行。在安装并配置 CLI 后，我们将介绍设置 S3 桶、配置该桶以及更改访问权限以允许上传。接下来的图展示了整个配方中的各个阶段及其触点。AWS CLI 是分阶段和执行的共同线索，GUI 也是如此。AWS 中的存储因素通过访问控制和身份验证进行管理，这允许我们创建、存储和操作已存储的对象和桶。



![](img/110fa0d6324f0893fff03cee6394144d_508_0.png)

图 13.70 – AWS 存储连接

## 准备工作

在开始使用 CLI 之前，我们必须下载并安装所需的包。对于这个配方，我使用的是 Mac。你可以轻松地访问 AWS 并下载 Windows 或 Linux 版本的 CLI。无论如何，一旦安装了 CLI，命令除了位置和其他某些特定操作系统的变化外没有区别，这些变化实际上只适用于 Windows：

```
curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
```

下载完成后，你必须安装 CLI。这是通过执行安装包完成的：

```
# installer -pkg ./AWSCLIV2.pkg -target /
```

在这种情况下，我们将 Python 版本升级到匹配 AWS CLI 要求的版本。你可以通过运行命令来检查，它将显示 AWS CLI 的安装位置以及版本：

```
# which aws
/usr/local/bin/aws
# aws --version
aws-cli/2.7.28 Python/3.9.11 Darwin/21.6.0/x64
```

安装 AWS CLI 后，我们将转向配置 Oracle Linux。我们将根据你的 AWS 账户和数据中心详细配置 AWS CLI：

![](img/110fa0d6324f0893fff03cee6394144d_509_0.png)

你将像之前的章节那样填写所有字段。通过引用你创建的磁盘（`/Users/USER/<NAME>`）来命名你的虚拟机。这有助于后续的操作。你可以随时返回 VirtualBox 虚拟机查找关联媒体，但在创建虚拟机时命名磁盘更容易。

### 虚拟机名称和操作系统

请为虚拟机选择一个描述性的名称和目标文件夹。你选择的名称将在整个 VirtualBox 中用于识别该机器。此外，你可以选择用于安装操作系统的 ISO 。

| 字段 | 值 |
| :--- | :--- |
| 名称 | vb-aws |
| 文件夹 | `/Users/jspindel/test-cloud` |
| ISO 镜像 | `/Users/jspindel/Desktop/ol7.iso` |
| 类型 | Linux |
| 版本 | Oracle Linux (64-bit) |
| 跳过无人安装 | 手动 |

图 13.2 – ISO 选择

如果你记得，在上一节中我们分配了 CPU 和内存。就像任何构建环境一样，我们需要指定、安装并配置资源。无论是虚拟还是物理，我们都在安装资源。在这种情况下，我们配置这个具有 4 GB RAM 和两个 vCPUs 的虚拟机。vCPU 等于处理器线程。在这里我们安装两个 vCPUs，等同于一个物理核心。

| 设置 | 值 |
| :--- | :--- |
| 基础内存 | 4 MB / 16384 MB |
| 处理器 | 1 CPU / 8 CPUs |
| 启用 EFI | 特殊（仅限） |

图 13.7 – 资源

在我们配置好 CPU 和内存后，我们准备好选择连接到虚拟机的媒体（磁盘）。在这种情况下，我们不会选择创建磁盘，而是使用现有的。记得我们以 `.vmdk` 格式创建了驱动器，所以让我们选择现有磁盘。

### 创建虚拟机

如果你想为机器添加虚拟磁盘，可以创建一个新磁盘，也可以选择一个现有的。你可以创建一个带虚拟磁盘的虚拟机。

- 创建虚拟磁盘

![](img/110fa0d6324f0893fff03cee6394144d_511_0.png)

图 13.74 – 创建或使用现有磁盘的选项

记得选择一个与虚拟机名称匹配的驱动器（假设你之前创建了一个），或者新建。注意应使用 `.vmdk` 扩展名以便识别。

### 虚拟磁盘

如果你想为机器添加虚拟磁盘，可以创建一个新磁盘，也可以选择一个现有的。你可以创建一个不带虚拟磁盘的虚拟机。

- 创建虚拟磁盘

![](img/110fa0d6324f0893fff03cee6394144d_511_1.png)

图 13.75 –磁盘选择

### 总结

与过去的配方一样，我们在摘要屏幕上确认选择并通过点击完成来执行配置。当你对配置满意时，按下完成创建虚拟机。你也可以返回修改配置。

| 虚拟机名称和操作系统类型 | 值 |
| :--- | :--- |
| 虚拟机名称 | vb-aws |
| 虚拟机文件夹 | `/Users/jspindel/Documents/test-cloud/vb-aws` |
| ISO 镜像 | `/Users/jspindel/Desktop/ol7.iso` |
| 客户操作系统类型 | Oracle Linux (64-bit) |
| 跳过无人安装 | false |
| 硬件 |  |
| 基础内存 | 4096 |
| 处理器 | 2 |
| 启用 EFI | false |
| 磁盘 |  |
| 挂载磁盘 | `/Users/jspindel/Downloads/64bit/vb-aws.vmdk` |

![](img/110fa0d6324f0893fff03cee6394144d_512_0.png)

一旦构建了 Linux 操作系统，我们就可以配置 AWS 环境，包括设置 CLI 在从 OVA 创建后执行我们的 AMI。记得，在上一个配方中，我们构建了一个虚拟机并从该 OVA 在 VirtualBox 中创建了镜像。我们将进行同样的操作，从 VirtualBox 导出并导入 AWS。区别在于没有高级的 VirtualBox 环境可以使用。我们将使用 AWS CLI 将 OVA 导入我们的 S3 桶。然而，如之前所述，为了实现这一点，我们需要配置该连接并就绪。我们将在从 VirtualBox 迁移到 AWS 的过程中介绍这些设置，看看可以使用哪些转换。

在 OVA 导出时，你将开始准备 AWS CLI 配置。

## 如何操作...

你可以通过两种方式上传导出的 OVA：通过命令行或 S3 控制台。无论哪种方式，简单地上传到 AWS S3，你如何操作并不重要。

通过 S3 控制台上传是一个非常直接的过程：

1. 登录你的 AWS 控制台，如下：

![](img/110fa0d6324f0893fff03cee6394144d_513_0.png)

2. 登录后，导航到 S3。

![](img/110fa0d6324f0893fff03cee6394144d_514_0.png)

图 13.78 – AWS 菜单

如果 S3 不在最近访问列表中，导航到存储并选择 S3，或者直接在搜索栏中输入 `s3`。

### 最近访问

收藏

所有服务

- 分析
- 应用程序集成
- AWS 成本管理
- 区块链
- 业务应用程序
- 计算
- 容器
- 客户赋能
- 数据库
- 开发者工具
- 用户计算
- 前端 Web 与移动
- 游戏开发
- 物联网
- 机器学习
- 管理与治理
- 媒体服务
- 迁移与传输
- 网络与内容交付
- 量子技术
- 机器人
- 卫星
- 安全、身份与合规
- 存储

### 存储

# AWS Backup AWS Backup 集中管理并自动跨 AWS 服务备份

# EFS 适用于 EC2 的托管文件存储

# AWS 弹性灾难恢复到 AWS 的低成本应用程序恢复

# FS5x 针对各种工作负载优化的全托管第三方文件系统

# S3 云端可扩展存储

# S3 Glacier 云端存档存储

# Storage Gateway 混合存储集成

![](img/110fa0d6324f0893fff03cee6394144d_515_0.png)

3. 导航到 S3 后，你将创建一个用于上传 OVA 的桶。桶本质上是对象存储，是存储图像等内容的绝佳之处。

![](img/110fa0d6324f0893fff03cee6394144d_516_0.png)

4. 选择**创建存储桶 (Create bucket)** 后，您需要为该存储桶命名并配置其其他方面。

![](img/110fa0d6324f0893fff03cee6394144d_516_1.png)

图 13.81 – 存储桶名称和区域

- 5. 命名后，根据 AWS 文档选择存储桶所在的区域。请记住在您当前操作且将用于本次练习的区域创建存储桶。在这种情况下，我们将部署到美国东部南部 - 俄亥俄 (US East 2 - Ohio)。

- 6. 我们在这里不会启用任何 ACL：

![](img/110fa0d6324f0893fff03cee6394144d_516_2.png)

7. 正如之前提到的 AWS 访问控制所示，我们将取消勾选**阻止所有公共访问 (Block all public access)**，并将 S3 存储桶开放给直接公共访问（即外部访问）。

### 注意

这不是一种良好的做法；我们这样做仅仅是为了测试目的。

此存储桶的阻止公共访问设置



通过访问控制列表 (ACL)、存储桶访问策略或全部方式授予存储桶和对象的访问。为了阻止对此存储桶的公共访问，请开启“阻止所有公共访问”。这些设置仅适用于此存储桶及其访问点。AWS 建议您开启阻止公共访问，但在应用任何此类设置之前，请确保您的应用程序在没有公共访问的情况下运行正常。如果您需要对此存储桶或对象进行某种程度公共访问，可以自定义下面的单独设置以适应您的特定用例。了解更多

- 阻止所有公共访问：这等同于关闭所有设置。以下每个设置都是相互独立的。
- 阻止通过`新的访问控制列表 (ACL)`授予存储桶和对象的公共访问：这将阻止应用于新添加存储桶和对象的公共访问权限，并防止为现有的存储桶和对象创建新的公共访问 ACL。此设置不会更改任何允许使用 ACL 访问 S3 资源的现有权限。
- 阻止通过`任何访问控制列表 (ACL)`授予存储桶和对象的公共访问：这将忽略所有授予存储桶和对象公共访问的 ACL。
- 阻止通过`新的公共存储桶或访问点策略`授予存储桶和对象的公共访问：这将阻止授予存储桶和对象公共访问的新存储桶和访问点策略。此设置不会更改任何允许公共访问 S3 资源的现有策略。
- 阻止通过`任何公共存储桶或访问点策略`授予存储桶和对象的公共访问和跨账户访问：对于拥有策略的存储桶或访问点，将忽略其公共和跨账户访问。

> 关闭阻止公共访问可能会导致此存储桶及其内部对象变为公开

> AWS 建议您开启阻止所有公共访问，除非特定且经过验证的用例（如静态网站托管）需要公共访问。

我承认当前设置可能会导致此存储桶及其内部对象变为公开。

图 13.83 – 公共访问

8. 我们将保持版本控制禁用（默认设置），如下截图所示，这是一个一次性存储桶，并将永久保留。当您在处理具有多个版本的项目生命周期（例如图像的多次迭代）时，您将需要启用版本控制。

### 存储桶版本控制

版本控制是在同一个存储桶中保留对象多个变体的方法。可以使用版本控制来保留、检索和恢复 Amazon S3 存储桶中存储的对象的每个版本。通过版本控制，您可以轻松地从无意的用户操作和应用程序故障中恢复。了解更多

存储桶版本控制

- 禁用
- 启用

![](img/110fa0d6324f0893fff03cee6394144d_518_0.png)

### 标签 (0) - 可选

可以使用标签来跟踪存储成本并组织存储桶。了解更多

此存储桶没有关联标签。

```
添加标签
```

![](img/110fa0d6324f0893fff03cee6394144d_518_1.png)

10. 我们将使用 S3 管理密钥的标准加密。

### 默认加密

加密自动应用于此存储桶的新对象。

加密类型

- 使用 Amazon S3 管理密钥加密 (SSE-S3)
- 使用 AWS 密钥服务密钥加密 (SSE-KMS)
- 使用 AWS 密钥服务密钥双层加密 (DSSE-KMS)

使用双层加密保护您的对象。有关定价的详情，请查看 Amazon S3 页面的存储选项卡。

存储桶密钥

对于 SSE-KMS 使用 S3 存储桶密钥可以减少对 AWS 调用。DSSE-KMS 不支持 S3 存储桶密钥。了解更多

- 禁用
- 启用

![](img/110fa0d6324f0893fff03cee6394144d_518_2.png)

11. 忽略高级选项并继续创建存储桶。

![](img/110fa0d6324f0893fff03cee6394144d_0.png)

图 13.37 – 存储桶显示

12. 导航到新创建的 `bucket-aws-east-2` 存储桶并点击“上传 (Upload)”。

### `bucket-aws-east-2` 信息

![](img/110fa0d6324f0893fff03cee6394144d_519_1.png)

图 13.38 – 上传

13. 点击“添加文件 (Add files)”。这将允许您从文件系统选择正确的 OVA 上传到存储桶。

![](img/110fa0d6324f0893fff03cee6394144d_519_2.png)

图 13.39 – 添加文件

14. 我们将选择在开始创建的 OVA。

### 文件和文件夹（共1 个，4.5 GB）

表中的所有文件和文件夹将被上传。

| 名称 | 文件夹 | 类型 | 大小 |
| :--- | :--- | :--- | :--- |
| `bucket-aws.ova` | | | 4.5 GB |

图 13.90 – 选择文件

15. 添加文件后，执行上传。

| `bucket-aws.ova` | | | 4.5 GB |

目的地

`bucket-aws-east-2`

> 目的地详情

影响存储在指定位置的新对象的存储桶设置。

> 权限

授予公共访问和其他账户的访问。

> 属性

指定存储类、加密设置、标签等。

图 13.91 – 文件目的地

16. 状态栏将显示进度，摘要部分将显示 S3 中的目的地，如下截图所示。

![](img/110fa0d6324f0893fff03cee6394144d_521_0.png)

图 13.92 – 上传中

注意

如果您离开此状态页面，将无法返回，因此在上传完成前请留在该页面。

- 17. 上传完成后（或者如果您想进行多任务处理，在此期间打开另一个 AWS 控制会话），您必须为刚刚创建的存储桶设置角色和访问。导航到身份和管理 (IAM) 以访问角色数据。
- 18. 在“角色 (Roles)”下，您可以为访问、身份验证或其他任何 IAM 相关的标准创建自定义角色。

### 身份和管理 (IAM)

搜索 IAM

仪表板

- 访问管理
  - 用户组
  - 用户
  - 角色
  - 策略
  - 身份提供程序
  - 账户设置
- 访问报告
  - 访问分析器
  - 存档规则
  - 分析器
  - 设置
  - 凭证报告
  - 组织活动
  - 服务控制策略 (SCPs)

图 13.93 – AWS 角色

我们将从命令行配置角色和权限。我们必须创建 IAM 用户和密钥，因为没有访问或验证，CLI 将无法运行。然后我们可以配置 CLI 连接到我们的账户。

要将该用户与该访问密钥关联，您必须返回 IAM，接下来的步骤将引导完成。

### 最近访问

### 收藏

### 所有服务

- 分析
- 应用集成
- AWS 成本管理
- 区块链
- 业务应用程序
- 计算
- 容器
- 客户赋能
- 数据库
- 开发者工具
- 终端计算
- 前端 Web 与移动
- 游戏开发
- 物联网
- 机器学习
- 管理与治理
- 媒体服务
- 迁移与传输
- 网络与内容交付
- 量子技术
- 机器人
- 卫星
- 安全、身份与合规
- 存储

![](img/110fa0d6324f0893fff03cee6394144d_524_0.png)

图 13.94 – 安全、身份与合规性菜单

19. 一旦你展开了“安全、身份与合规性”，你将看到导航至 IAM 控制台的选项。或者，你也可以在搜索栏中输入 IAM。由于我们正试图帮助你熟悉控制台，我们将详细说明进入此选项的特定步骤。

#### 安全、身份与合规性

##### AWS Artifact

安全合规报告和协议

##### AWS Audit Manager

持续评估控制措施的风险和合规性

##### Certificate Manager

置备、管理和部署 SSL/TLS 证书

##### CloudHSM

云端托管的硬件安全模块

##### Cognito

消费者身份管理以及用于联合身份的 AWS 凭证

##### Detective

调查和分析潜在的安全问题

##### Directory Service

托管和管理 Active Directory

##### AWS Firewall Manager

防火墙规则的中心化管理

##### GuardDuty

智能威胁检测，保护你的 AWS 账户和工作负载

##### IAM

管理对 AWS 资源的访问

图 13.95 – IAM

20. 为了访问密钥，我们必须了解什么是密钥，以及它是如何与用户相关联的。因此，让我们导航到“用户”(Users)。我们将按照以下步骤演示创建。

![](img/110fa0d6324f0893fff03cee6394144d_527_0.png)

21. 我们想要创建屏幕截图所示的用户，可以通过导航到“添加用户”(Add users)来实现。我们将用户命名为 `user-admin`：

![](img/110fa0d6324f0893fff03cee6394144d_527_1.png)

22. 现在既然我们已经为用户命名了名，就像任何其他系统一样，我们需要定义用户、将他们添加到组中并分配权限。

![](img/110fa0d6324f0893fff03cee6394144d_527_2.png)

23. 我们将此用户分配到 `admin` 组并点击“下一步”继续。你可以通过创建一个更符合你或你组织策略的组来定义权限。在创建用户后，我们就可以在这里生成密钥，如后续屏幕所示，并附带密钥。以下步骤将介绍如何进行操作。

### 访问最佳实践与替代方案



使用访问密钥等长期凭证来提高你的安全性。考虑使用用例和替代方案。

### 命令行界面 (CLI)

你计划使用此访问密钥让 `AWS CLI` 访问你的 `AWS` 账户。

### 本地代码

你计划使用此访问密钥让本地开发环境中的应用程序代码访问你的 `AWS` 账户。

### 运行在 AWS 服务上的应用程序

你计划使用此访问密钥，让运行在 `EC2`、`Amazon ECS`、`AWS Lambda` 等 `AWS` 服务上的应用程序代码访问你的 `AWS` 账户。

### 第三方服务

你计划使用此访问密钥让监控或管理你 `AWS` 资源的第三方服务获得访问。

### 运行在 AWS 外部的应用程序

你计划使用此访问密钥让运行在本地主机上的应用程序获得访问，或者使用本地 `AWS` 客户端或第三方 `AWS` 插件。

### 其他

你的情况未在此列出。

> 推荐的替代方案
>
> - `AWS CloudShell`，一个基于浏览器的用于运行的 `CLI`。[了解更多]
>
> - 使用 `AWS CLI V2` 并通过 `IAM Identity Center` 中的用户启用身份验证。[了解更多]

### 确认

理解上述建议并想要创建访问密钥。

此访问密钥专门用于 `CLI`，因此这将是我们想要选择的选项，如前一个屏幕截图所示，然后点击“下一步”。在本教程中我们不会创建任何标签，所以可以随心跳过该部分并创建访问密钥。

#### 注意

下载 `.csv` 文件（凭证文档），并通过点击密钥旁边的方框显示并复制访问密钥。这是你可以复制这些密钥的唯一地方，无论你是将它们写下来还是粘贴到记事本中。一旦你关闭此页面，将无法恢复此信息也无法在不丢失数据的情况下重新配置 `CLI`，但那工作量很大，请务必记下密钥。

## 获取访问密钥

| 访问密钥 | 访问密钥 |
| :--- | :--- |
| 如果你丢失了访问密钥，将无法检索它。请创建一个新的访问密钥并将旧的停用。 |
| `AKIA3H45UYOKXHIA2ZNA` | `eZ5SmZX2GHEY0AfBnLdqI6TTMuz2DMst` |

## 访问密钥最佳实践

- 永远不要以明文形式将访问密钥存储在存储库或代码中。
- 在不再需要时禁用或删除访问密钥。
- 启用最小权限原则。
- 定期轮换访问密钥。

有关管理访问密钥的更多信息，请参见管理访问密钥的最佳实践。

![](img/110fa0d6324f0893fff03cee6394144d_529_0.png)

25. 一旦你添加了访问密钥，它将处于活动状态。通过 `CLI`、`AWS SDK` 或直接调用 `API` 使用它。你可以同时拥有两个访问密钥。

| 访问密钥 | 状态 | 描述 | 最后使用 | 区域 |
| :--- | :--- | :--- | :--- | :--- |
| 创建新的访问密钥 | | | | |
| `AKIA3H45UYOKXHIA2ZNA` | | | | |

| (1) | ![](img/110fa0d6324f0893fff03cee6394144d_529_0)

26. 一旦你添加了访问密钥，它将处于活动状态。通过 `CLI`、`AWS SDK` 或直接调用 `API` 使用它。你可以同时拥有两个访问密钥。

| 访问密钥 | 状态 | 描述 | 最后使用 | 区域 |
| :--- | :--- | :--- | :--- | :--- |
| 创建新的访问密钥 | | | | | |
| `AKIA3H45UYOKXHIA2ZNA` | | | | | |

27. 一旦你添加了访问密钥，它将处于活动状态。通过 `CLI`、`AWS SDK` 或直接调用 `API` 使用它。你可以同时拥有两个访问密钥。

| 访问密钥 | 状态 | 描述 | 最后使用 | 区域 |
| :--- | :--- | :--- | :--- | :--- |
| 创建新的访问密钥 | | | | | |
| `AKIA3H45UYOKXHIA2ZNA` | | | | | |

28. 一旦你添加了访问密钥，它将处于活动状态。通过 `CLI`、`AWS SDK` 或直接调用 `API` 使用它。你可以同时拥有两个访问密钥。

| 访问密钥 | 状态 | 描述 | 最后使用 | 区域 |
| :--- | :--- | :--- | :--- | :--- |
| 创建新的访问密钥 | | | | | | |
| `AKIA3H45UYOKXHIA2ZNA` | | | | | | |

29. 运行此命令来检查状态。在几分钟后，你可以通过运行此命令来检查导入状态。运行此命令来显示状态。

30. 过程完成后，你将能够登录 `AWS` 控制台并导航到你的 `EC2` 环境。为了能够以你的 `AMI` 为模板启动一个新虚拟机，请点击“启动实例”。

# 资源

你正在美国东部（俄亥俄）区域使用以下 `Amazon EC2` 资源：

| 实例（运行中） | 0 | 自动伸缩组 |
| :--- | :--- | :--- |
| 弹性 IP | 0 | 实例 |
| 负载均衡器 | 0 | 放置组 |
| 快照 | 1 | 卷 |

> 在...上轻松调整大小、配置和部署 Microsoft SQL Server Always on 可用性组

# 启动实例

要开始操作，请启动一个 `Amazon EC2` 实例，它是云中的虚拟服务器。

![](img/110fa0d6324f0893fff03cee6394144d_532_0.png)

注意：你的实例将在美国东部（俄亥俄）区域启动

图 13.103 – 启动实例

31. 一旦你进入启动菜单，就可以查看其他可用的 `AMI`。

# 应用程序和操作系统镜像 (Amazon Machine Image)

`AMI` 是一个模板，其中包含了启动实例所需的软件配置（操作系统、应用程序服务器和应用程序）。如果你在下方没有看到要找的内容，请搜索或浏览 `AMI`。

搜索我们的完整目录，包含数千个应用程序和操作系统镜像

- 我的 `AMI`
- 快速启动

| Amazon Linux | macOS | Ubuntu | Windows | Red Hat | SUSE Linux |
| --- | --- | --- | --- | --- | --- |
| aws | Mac | ubuntu® | Microsoft | Red Hat | SUS |

![](img/110fa0d6324f0893fff03cee6394144d_533_0.png)

# Amazon Machine Image (AMI)

Amazon Linux 2023 `AMI`

`ami-0ccab5fb8f2d4c9af5` (64-bit (x86)) / `ami-03ad0a8390cd7ff88` (64-bit (Arm))

虚拟化: `hvm`

启用 `ENA`: true

根设备类型: `ebs`

符合免费层级资格

描述:

Amazon Linux 2023 `AMI` 2023.1.20230809.0 x86_64 HVM kernel-6.1

架构

| 64-bit (x86) | `AMI ID`: `ami-0ccab5fb8f2d4c9af5` | 验证过的提供程序 |

> 图 13.104 – 浏览 `AMI`

32. 这将带你进入自定义的 `AMI` 以及（如之前图 13.7 镜像产品所示）市场（Marketplace）。市场是你与社区共享自己的 `AMI` 或使用他人的 `AMI` 的地方。

![](img/110fa0d6324f0893fff03cee6394144d_534_0.png)

33. 如前所示，你将看到在此配方中创建的可用 `AMI`。顺便提一下，在市场提供的 `AMI` 中，你可以找到许多操作系统，例如 Oracle Linux。

34. 如果你导航到新创建的 `AMI`，你会发现你可以选择它作为执行并创建虚拟虚拟机的 `AMI`。

![](img/110fa0d6324f0893fff03cee6394144d_534_1.png)

通过选择 `AMI`，你将该 `AMI` 作为你的镜像附加，并从所选镜像（`AMI`）执行创建虚拟机。

# 总结

| 信息 | 值 |
| --- | --- |
| 实例数量 | 1 |
| 软件镜像 (`AMI`) | import-ami-0908bf8d72b678cdf (`ami-055ce61f65862de6`) |
| 虚拟服务器类型 (实例类型) | `t2.micro` |
| 防火墙 (安全组) | 新安全组 |
| 存储 (卷) | 1 个 - 20 GiB |

> 免费层级：第一年包含每月 750 小时的 `t2.micro`（在不可用 `t2.micro` 的区域）实例使用、30 GiB `EBS` 存储、200 万 IOPS、1 GB 快照以及 100 GB 带宽。

启动实例

查看命令

![](img/110fa0d6324f0893fff03cee6394144d_535_0.png)

35. 在选择 `AMI` 并执行启动后，你将进入创建虚拟机、创建密钥对、命名密钥对并下载密钥的标准流程。你也可以预创建这些密钥。

# 创建密钥对

密钥对名称：最多255 个字符。不能包含开头或结尾空格。

密钥对类型

| `RSA` | `ED25519` |
| --- | --- |



| RSA 私密钥 | ED25519 |

私密钥格式

- `.pem` 用于 OpenSSH
- `.ppk` 用于 PuTTY

> 提示时，将私密钥存储在计算机上的安全位置。你稍后需要它来连接到实例。

36. 一旦你创建了密钥对，私密钥将下载到你的本地机器，你可以启动虚拟机。

# EC2 > 实例 > 启动实例

状态：已启动实例 (`i-0500b49c985b2`)

![](img/110fa0d6324f0893fff03cee6394144d_537_0.png)

37. 你可以通过点击实例 ID 导航到你的虚拟机。一旦进入实例，你将能够捕获 IP 并登录。

38. 要登录机器，你可以使用构建机器时创建的密钥对：

```
ssh oracle@335.211.36
systemctl enable --now cockpit.socket
Last login: Sat Aug 12 01:45:26 from 107.200.172
```

# 索引

AArch64 5

- Aardvark 341
- 访问控制列表 (ACLs) 122
- Compliance 298-304
- Amazon Linux 2 (AL2) 431
- Amazon Web Services (AWS)
- 自定义镜像，创建 481-508
- Ampere 14
- Ansible 415
- 新且改进的 playbook 252, 253
- playbook 247-249
- 可移植角色 (roles) 246, 247
- 角色创建 249-251
- Ansible 核心版本 420
- Ansible Galaxy URL 247
- Ansible 角色 246
- Ansible Vault 用于密钥管理 253
- 密码，明文显示 255, 256
- 全文件加密 253-255

ANSSI-BP 300

Apache HTTPD 服务器设置 39, 40

应用程序编程接口 (API) 456

应用程序工具

- 安装，通过 AppStream 317-322

AppStream

- 应用程序工具，通过 AppStream 317-322
- 开发工具，通过 AppStream 317-322
- 软件包，删除 327-329
- 使用，安装不同版本的软件 322-326

AppStream 模块

- 列出 313-317
- 搜索 313-317

Arm 14

Arm CPUs

优势 14

资产报告文件 (ARF) 304

澳大利亚网络安全中心 (ACSC) 301

澳大利亚信号局 (ASD) 301

身份验证头 (AH) 180

自动化证书管理环境 (ACME) 285

可用性区域 (AD) 363

可用性九个 162

B

恶意攻击者 279

基板管理器 (BMC) 3

基本输入输出系统 (BIOS) 8

绑定/汇聚接口 199

绑定 200

容错性 200

链路聚合 200

负载均衡 199

冗余连接，配置 202, 203

绑定模式 200

启动 ISO 3

启动协议 (BOOTP) 29

砖 (bricks) 191

桥接网络 334

B 树文件系统 (Btrfs) 95

Btrfs 配额 109-113

Btrfs 快照 109-113

Btrfs 子卷 109-113

Buildah

- 容器镜像，使用 Buildah 构建 354-356

自备支持 (BYOS) 431

C

CentOS Linux，迁移 24-27

Ceph 95

cephalopod 95

Clevis 290

云服务提供商 (CSPs) 414, 429

命令行界面 (CLI) 341

常见配置枚举 (CCE) 数据库 298

通用 Internet文件系统 (CIFS) 96

常见漏洞与披露 (CVE) 298

URL 211

社区版 (CE) 439

互补金属氧化半导体 (CMOS) 芯片 67

WordPress 网站 Compose 文件 352-354

配置清单格式 (XCDDF) 文件 304

容器镜像

使用 Buildah 构建 354-356

容器化数据库 349

数据存储 350, 351

初始化脚本 351

启动顺序控制 352

使用标准

写时复制 (COW) 122

Corosync 161

特性 181, 182

用于 HA 集群的 181-189

刑事司法服务 (CJIS) 301

客户支持标识符 (CSI) 138

自定义镜像

为 AWS 创建 481-508

双直线内存模块 (DIMMs) 14

## E

`efibootmgr` 工具 68

EFI 系统分区 (ESP) 68

电子受保护健康信息 (ePHI) 301

企业版 (EE) 439

企业系统管理员 24

以太网绑定 (Ethernet bonding) 199

扩展文件系统 (XFS) 95

- 创建 122-125
- 修改 122-125

可扩展固件接口 (EFI) 78

企业级 Linux 额外包 (EPEL) 17, 153

## F

故障转移模式 200

美国联邦调查局 (FBI) 301

联邦风险与授权管理计划 (FedRAMP) 279

文件系统

- 共享，跨多机器 190-199

防火墙/防火墙守护进程 304, 307

`fixfiles` 命令

- 使用方法 310, 311

法国信息系统安全局 (ANSSI) 300

完整 ISO 镜像 3

完全限定域名名 (FQDN) 33, 140, 192

## G

Git 提交

- 使用 GPG 签名 280-284

Git 大文件存储 (Git Large File Storage) 154

Git 仓库

- 添加到 OLAM 实例 395, 396

全局文件系统 2 (GFS2) 95

全局标识符 (GUID) 68

- 集群 95, 190

GlusterFS 161, 190

GNU 隐私卫 (GPG) 280

- 用于签名 Git 提交 280-284

GR 统一引导加载程序 (GRUB) 34, 67

统一引导加载程序版本 2 (GRUB2) 67

GUID 分区表 (GPT) 68, 75

对比主引导记录 (MBR) 75

## H

黑客 279

高可用性 (HA) 集群

- 配合 Corosync 181-189
- 配合 Pacemaker 181-189

HAProxy 配置文件

- 后端部分 172, 173
- 前端部分 171, 172
- 列表部分 173, 174

健康保险可携带性和责任法案 (HIPAA) 279, 301

高可用性 (HA) 161, 162, 165

- 设计考虑因素 164

高可用性代理 (HAProxy) 161, 166, 167

- 能力 166, 167
- 特性 166, 167
- 全局设置 170
- 使用 Keepalived 实现高可用 176-181
- 状态页面 176
- 工作原理 175

HTTPS 服务器 30

超文本传输协议守护进程 (HTTPD) 30

## I

身份与访问管理 (IAM) 494

基础设施即代码 (IaC) 233, 246, 414

智能平台管理接口 (IPMI) 3

中间层加载器 86

中间阶段 86

国际标准组织 (ISO) 3

- 刻录制作可启动盘 6-8

网际控制消息协议 (ICMP) 306

`iperf` 205-207

`iptraf-ng` 命令 204

## J

磁盘磁盘阵列 (JBOD) 115

## K

Keepalived

- 特性 176, 177
- 用于使 HAProxy 高可用 176-181

内核基础

- Linux 内核 65, 66
- RHKC 66, 67
- UEK 66, 67

kickstart

- 选项 34, 59
- 操作系统安装选项，自动化安装 31-34

已知漏洞检测 (KED) 225

- 启用 227-229
- 安装 225-227

已知漏洞检测技术 212

Ksplice 25, 144, 210

- 配置 214-216
- 传统补丁过程 213
- 补丁过程 214
- 安全生命周期 210
- 接入网络设置 217-222
- 使用 217, 218, 222
- 在无网络访问的情况下使用 222-224

Ksplice 标识符 (KID) 221

Ksplice Inspector 211

- 引用链接 210

## L

实验室环境

- 使用 Vagrant 创建 257-262

Leapp 17

- 耗时 22, 23
- 启动升级 22, 23
- 工作原理 23

升级阶段

- 升级前阶段 17
- 第二阶段 17



旧式基本输入输出系统 (BIOS) 固件 67

Let's Encrypt

- URL 285

Let's Encrypt 类型

- 引用链接 285

链路聚合 201

链路聚合协议 (LACP) 201

- 特性 201, 202

- 特性 201, 202

聚合组 (LAGs) 200

Linux 绑定模式 200, 201

Linux 内核 65, 66

Linux 密钥设置 (LUKS) 34, 290

- 设置 292-296

负载均衡器 165-170

本地文件系统 96-99

逻辑单元 (LUNs) 96

逻辑卷管理 (LVM) 118-121, 137

逻辑卷 (LVs) 118

物理卷 (PVs) 118

卷组 (VGs) 118

- 登录用户 311

LVM 算法 112

## M

机器所有者密钥 (MOK)

- 数据库更新 82

macvlan 334

强制访问控制 (MAC) 307

手动安装

- 45-59

主引导记录 (MBR) 69, 75

对比 GUID 分区表 (GPT) 75

介质访问 (MAC) 200

多因素认证 (MFA) 432

多设备管理 (mdadm) 114

多设备 (MD) 114

多机器文件系统共享 190-199

## N

命名、发布与架构 (NEVRA) 156

美国标准与技术研究院 (NIST) 301

网络访问

- 限制 304-307

网络绑定 199

网络磁盘加密 (NBDE) 290

网络文件系统 (NFS) 96

网卡 (NIC) 绑定 199

- 组队 201

网络时间协议 (NTP) 50

可用性 9 162

NIST-800 301

## O

OCI Terraform 提供程序

- 引用链接 244

OEM 25

OLAM 实例

- 接入 OCI 415-420

OLAM 使用 Ansible

- 循环 423-427

在线模式 216

开放集群框架 (OCF) 186

OpenSCAP 298

OpenSCAP 安全指南

- 引用链接 301

开放虚拟机设备 (OVA) 451

开放虚拟机格式 (OVF) 270, 451

Oracle 云标识符 (OCID) 416

Oracle 云基础设施 (OCI) 214, 232, 238, 429

- 引用链接 263

Oracle 集群文件系统 2 (OCFS2) 95

Oracle Linux 25

- 优势 25

- 启动过程 67

- 迁移到 CentOS 24-27

- 默认内核更改 71

- grubby 默认内核 71

- grubby 内核信息 71

- grubby 输出 70

- 在云端 430-436

- 安装 2

- 在树莓派上安装 15-17

- Legacy BIOS 引导序列 69

- 查找 Oracle AMIs 436-438

- 在 Windows Linux 子系统 (WSL) 上运行 8-14

- UEFI 引导序列 68

Oracle Linux 7

- 接入 Oracle Linux 17-22

Oracle Linux 7 Vagrant Box 258

Oracle Linux 8 96, 262

- 升级 24

Oracle Linux 8 kickstart 文件 270-277

Oracle Linux 8.x 镜像

- 引用链接 244, 266

Oracle Linux 自动化管理器 (OLAM) 6, 232

- 配置 380-393

- 分组，添加到清单 421

- 安装 360-378

- 清单创建 420

- 运行清单 421

- 查看并确认清单 421

- 管理 380-393

- 运行 ping 验证清单 422

- 使用 playbooks 394-405

Oracle Linux Manager 257

- Oracle Linux Manager 安装与配置指南

- 引用链接 258

Oracle Linux 虚拟机管理器 (OLVM) 430

Oracle VirtualBox 96

Oracle VM VirtualBox 232

操作系统安装选项

- 使用 kickstart 自动化安装 31-34

## P

Pacemaker 161

- 特性 182

- 用于 HA 集群 181-189

软件包

- 通过 AppStream 移除 327-329

Packer 232

- 用于从 Oracle Linux 8.8 源创建 Vagrant box 269-277

- 用于修改源镜像 262-269

Packer VirtualBox 插件

- 引用链接 271

并行可用性 329

并行不稳定 329

补丁混沌

- 控制 406–413

支付卡行业数据安全标准 (PCI-DSS) 279, 301

开机自检 (POST) 68

预启动执行环境 (PXE) 2, 8, 29

进程 ID (PID) 229

公钥，添加到 OCI 控制台

- 引用链接 245

PXE 启动 29

PXE 客户端 30

PXE 服务器 30

Python 326, 327

## Q

质量保证 (QA) 24

## R

机架单元 (RU) 14

RAID  Btrfs 卷

- 创建 100-108

- 监控 100-108

- 调整大小 100-108

树莓派

- 在树莓派上安装 Oracle Linux 15-17

实时应用集群 (RAC) 165

侦察 210

红帽兼容内核 (RHKC) 4, 66, 97

- 移除 88-93

- 工作原理 72-74

红帽企业 Linux (RHEL) 127

红帽软件包管理器 (RPM) 2, 30, 127

冗余磁盘阵列 (RAID) 97

远程镜像

- 使用 Skopeo 处理 357, 358

- 使用 Skopeo 检查 357

资源操作，集群 187

无权限容器

- 使用 Podman 运行 333, 334

无权限 Podman

- 网络端口 334

信任根 (RoT) 79

RPM 包

- 创建 153-158

## S

SDK 和 CLI 配置链接

- 引用链接 265

安全启动 79

- 模块签名 82

- 系统重启 82-84

- 与 79-81, 85 工作

安全技术实施指南 (STIG) 99, 301

安全内容自动化协议 (SCAP) 298

安全增强 Linux (SELinux) 307, 308

- 状态修改 309

- 状态 308

安全 (SEC) 阶段 79

SELinux fixfiles 310, 311

SELinux 用户类型

- 域类型 309

- 网络端口类型 309

- 角色类型 309

- 类型强制执行类型 309

- 用户类型 308

SELinux 用户命令 312

- SELinux 用户 311

- semanage 命令 309, 310

消息块 (SMB) 96

服务等级协议 (SLA) 163

踢掉另一个节点 (STONITH) 186

sign-file 工具 81

硅图形 IRIX 系统 97

简单邮件传输协议 (SMTP) 228

单点故障 (SPOFs) 161

单点登录 (SSO) 凭证 138

Skopeos 354

远程镜像，处理方法 357, 358

远程镜像，检查 357

slirp4nets 334

源镜像

- 使用 Packer 修改 262-269

源 ISO 4

栈

- 管理，使用 pods 344, 345

- 员工用户 311

标准操作程序 (SOP) 407

存储区域网络 (SAN) 96, 202

存储节点/对等 193

支持标识符 (SI) 138

符号链接 (symlink) 129

systemd 332

系统用户 311

## T

Tang 服务器

配置 291, 292

Terraform 233

使用方法，用于在云中部署虚拟机 233-238

虚拟机，在 OCI 中创建 238-246

Terraform 注册表

参考链接 238

TFTP 服务器

提供服务 41-45

传输层安全协议 (TLS) 284

TrenchBoot 86

- 启动安全 88

- 能力 86

- 组件 87

- 镜像处理 88

- 开源项目 88

- 平台无关 88

- 流程概述 86, 87

- 攻击防护 88

- 运行时完整性 88

- 工作原理 87

BenchBoot 引导器 86

BenchBoot 安全引擎 86



简单文件传输协议守护进程 (TFTPD) 30

双因子身份验证 (2FA) 87

# U

UEK 启动 ISO 4

不可破解的企业内核 (UEK) 3, 66, 67, 95
- 运行 72-74

不可破解的 Linux 网络 (ULN) 137
- DNF/YUM 镜像，构建方法 137-153

统一扩展固件接口 (UEFI) 8, 82
- MBR 对比 GPT 75, 76
- 使用 74-78
- 用户定义用户 312

用户 ID (UID) 229

工具型容器
- 创建，使用 `Podman` 335
- 入口 336, 337
- 卷载挂载 337
- 工作目录 337

工具型容器，示例
- 镜像或视频文件，使用 `FFMPEG` 修改 338, 339
- 轻级 `NGINX` 服务器，运行以预览网页 340
- `Markdown` 文件转为 `docx`，使用 `pandoc` 338
- `Node.js`，使用 339, 340

# V

`Vagrant` 232

参考链接 273
- 使用，用于创建实验环境 257-262

`Vagrantfile` 270

Vagrant 用户名和密码
参考链接 272

变量级加密 257

`vault` 密码文件 254

`VirtualBox`
- 使用，用于将虚拟机跳板到 `OCI` 451-481

`VirtualBox` ISO
参考链接 273
- 虚拟云网络 (VCN) 214, 448

虚拟 IP (VIP) 176
- 虚拟机 (VMs) 429
- 虚拟冗余协议 (VRRP) 176

`VirtualBox` 258

# W

Web 服务器 168, 169

网站
- 负载均衡 165-176

Web 加密 285

`acme.sh`，从 Git 获取 287

优势 284

`Apache`，安装及要求 286, 287

证书，使用 `webroot` 模式 288, 289

测试 289

Windows Linux 子系统 (WSL)

Oracle Linux，运行在 14

WordPress 网站

使用 `Compose` 文件部署 352-354

# X

x86_64 4

# Y

Yellowdog 更新 (YUP) 127

Yellowdog 更新器 (`YUM`) 127, 128

问题 128

另一种标记语言 (`YAML`) 格式 341

# Z

ZeroSSL

URL 285

zlib 算法 112

zstd 算法 112
