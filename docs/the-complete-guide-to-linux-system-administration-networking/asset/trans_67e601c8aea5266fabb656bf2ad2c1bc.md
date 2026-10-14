

# Linux 发行版

单独的 Linux 内核并不能提供完整操作系统的功能。要真正实用，一个完整的系统应该包括：

- 硬件驱动程序，使 Linux 能够与打印机、网卡、数码相机和扫描仪、DVD 驱动器等众多外设配合使用
- 安装程序，使用户能够轻松地将所有 Linux 文件设置到计算机上
- 网络和系统管理实用程序，用于监控和配置操作系统的运行方式
- 图形环境（桌面界面），以及用于管理操作系统的图形工具
- 个人生产力应用程序，如文字处理器、计算器、日历、CD 播放器和时钟（也许还有一些游戏）
- 描述如何执行系统管理任务、如何操作图形界面以及许多其他任务的文档

一个包含操作系统内核以及上述许多或全部组件的“产品化” Linux 版本称为 Linux 发行版。Linux 发行版通常包含数千个在 Linux 上运行的独立程序。其中大多数与管理 Linux 系统有关——换句话说，它们是系统实用程序。其中许多系统实用程序取自 GNU 项目。因此，有些人将 Linux 发行版称为 GNU/Linux 操作系统。使用打包的 Linux 发行版，非技术人员可以安装和使用 Linux。图 1-3 显示了不同组件如何被收集到 Linux 发行版中。

![](img/43f64015de86d989e30eff5bb284fb96_38_0.png)

图 1-3 许多组件共同构成了一个 Linux 发行版

许多公司都创建了 Linux 发行版。根据 GPL，这些公司在其发行版中包含了 Linux 内核的源代码，以及发行版中大多数其他实用程序的源代码。它们可以自行决定为其 Linux 发行版收取多少费用；由于软件可以从其他来源免费获得，因此一种看法是 Linux 公司本质上充当包装服务，省去了用户下载和配置大量文件的麻烦。

发行版中程序免费这一事实在很大程度上使 Linux 的价格保持在较低水平——通常在 2 美元到 100 美元之间。由于许多 Linux 厂商提供的 Linux 内核和实用程序几乎相同，厂商使用商业组件（如专用实用程序）或服务（如技术支持）来使他们的产品对消费者更具吸引力。稍后描述的 Red Hat Enterprise Linux 就是一个例子。表 1-1 列出了几种 Linux 发行版。您可以通过访问 www.distrowatch.com 找到有关全球数百种 Linux 发行版的详细信息。购买 Linux 发行版廉价 CD 的一个好来源是 www.cheapbytes.com。

## 表 1-1 流行的 Linux 发行版

| Name | Comments | Web site |
|---|---|---|
| Red Hat Linux | The most widely used distribution, from Red Hat Software; currently sold as Red Hat Enterprise Linux, in several versions for different markets and hardware configurations | www.redhat.com |
| Fedora | A distribution based on Red Hat Linux, but entirely free (no commercial version exists) | fedora.redhat.com |
| SUSE Linux | Very popular in Europe; originally produced by SUSE, a German company, which was recently acquired by the networking software company, Novell | www.suse.com |
| Debian | A noncommercial Linux distribution targeted specifically to free software enthusiasts. Debian does not have a company behind it. It is created and maintained by developers of free software | www.debian.org |
| Xandros | Focused on providing a desktop operating system to replace Microsoft Windows | www.xandros.com |
| Linspire (formerly Lindows) | Focused on providing a desktop operating system to replace Microsoft Windows (also the target of a lengthy trademark lawsuit by Microsoft, in which Lindows/Linspire has so far prevailed) | www.linspire.com |

## Red Hat Software

由于本书的目的之一是帮助您通过 Red Hat 认证技术员考试，您应该更详细地了解 Red Hat Software 提供的 Linux 产品。

直到 2003 年底，Red Hat Software 销售的是 Red Hat Professional Linux，这是一款价格相对较低但备受推崇的发行版，到那时已发展到第 9 版。Red Hat Software 然后通过创建 Fedora 发行版作为免费产品和技术试验田来改变其产品线。通过维护 Fedora 发行版，Red Hat 继续为创建 Linux 内核和其他自由软件的许多开发人员提供资金支持。Red Hat Software 的商业重点现在是 Red Hat Enterprise Linux，它有三种不同的配置：

- **WS (workstation):** A product designed for power users who want to use Linux at their Intel or compatible (x86) desktop. This version does not include most of the Internet server technology provided in other Linux distributions, such as a Web server and e-mail server. A separate version called Red Hat Professional Linux is a low-cost version of the Enterprise Linux WS product. It is sold through retail stores and corporate resellers, but you cannot purchase technical support beyond basic installation support.
- **ES (enterprise server):** A midrange server product for Intel x86 and compatible computers that includes Internet server software such as a DNS server and e-mail server
- **AS (application server):** A high-end server product similar to the ES product, but which is available for seven types of hardware, including IBM mainframes (model S/390)

![](img/43f64015de86d989e30eff5bb284fb96_40_0.png)

> For simplicity, the term Red Hat Linux is used throughout this book to refer to Linux products from Red Hat Software. Specific products or differences between products are noted when appropriate.

Red Hat Enterprise Linux 以订阅服务的形式出售。假设您通过 Red Hat 网站 www.redhat.com 购买了一份 Red Hat Enterprise Linux ES 并附带了 Basic 服务协议。您可以立即下载并安装操作系统，也可以订购媒体套件（约 25 美元），其中包括 CD-ROM 和基本文档，如安装指南。安装操作系统后，它会通过互联网与 Red Hat Software 保持联系。任何安全修复、软件包升级或其他使系统平稳安全运行所需的信息都会通过此 Red Hat Network (RHN) 服务下载并配置。

您应该通过查看 www.redhat.com/software 上提供的详细信息来熟悉不同的 Red Hat 产品。请注意，与 Red Hat Enterprise Linux 捆绑的软件与任何其他 Linux 发行版中包含的软件并没有太大区别。Red Hat 添加了一些强大的实用程序，但其成功的关键在于他们为使用 Linux 的大型公司提供的服务和支持。例如，Enterprise Linux AS 产品，每份价格在 2500 美元到 18000 美元之间，提供关键问题的 1 小时响应时间，全天 24 小时、每周 7 天。本节后面讨论的 Red Hat 培训和认证计划也是考虑使用 Linux 的企业的重要因素，因为它们确保有知识的员工来维护组织的 Linux 系统。

## 硬件要求

Linux 系统可以在非常有限的硬件上运行。您可以使用一台 CPU 为 133 MHz、RAM 为 16 MB、硬盘空间为 100 MB（或更少，具体取决于您想用 Linux 系统做什么）的计算机运行 Linux 系统。然而，像表 1-1 中列出的主要发行版通常建议您的计算机至少有约 1 GB 的可用磁盘空间和 64 MB 的 RAM。这使您能够使用图形系统并安装大量常用的软件包。

现实地说，如果您购买一台更新的计算机，您很可能至少拥有 128 MB 的 RAM 和 20–40 GB 的硬盘空间。更多的硬盘空间使您能够安装更多应用程序，从而可以为服务器添加功能、存储更多数据文件，或只是尝试桌面上的有趣程序。更多的 RAM 通常使系统运行更快，因为 Linux 内核使用额外的内存来存储来自硬盘的信息，从而提高性能。

Red Hat 对 Enterprise Linux 安装提供了具体建议。它建议使用 256 MB 的 RAM（Enterprise Linux ES 最多 8 GB，Enterprise Linux AS 最多 64 GB）、300 MHz 的 CPU 和 800 MB 的可用磁盘空间（最大文件系统大小为 1 TB）。访问 www.redhat.com/software/rhel/configuration/ 可了解有关 Enterprise Linux 要求的详细信息以及 Linux 功能的有趣总结。

## 版本编号

与 Linux 产品相关的版本号可能令人困惑。Linux 内核的每个版本都被分配一个版本号。Linux 发行版的每个组件也由开发该组件的团队分配一个版本号。Linux 发行版本身也有版本号，这些版本号是出于营销原因选择的，基于发行版更新的频率。

大多数用户选择他们选择的发行版的最新可用版本。例如，截至本文撰写时，Red Hat Enterprise Linux 3 是可用的最新版本的 Red Hat Linux。但 Linux 内核的版本号也很重要，因为它定义了操作系统的一些关键功能，例如支持什么硬件以及使用什么安全模型。内核版本号包括三个部分：

- 一个很少更改的主要版本号。Linux 的主要版本在过去六七年里一直是 2。

