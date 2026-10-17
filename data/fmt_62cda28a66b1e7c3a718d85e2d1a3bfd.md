
# VMWare 使用指南（第 2 版）

## 引言

在短短一年的时间里，IT 行业发生了令人难以置信的变化。2004 年 7 月，Rob 关于使用 VMware 的指南第一版出版。现在是 2005 年 9 月，仅仅一年多一点的时间里发生了很多事情。首届 VMware 大会（VMworld）于 2004 年 10 月在圣地亚哥举行，VMware 发布了名为 ACE 的新产品，VMware Workstation 版本 5 正式推出，并且今年早些时候 VMware 开发者技术网络正式上线。最后但同样重要的是，2005 年 8 月 VMware 宣布将与 IT 行业众多领先公司联合推动虚拟化领域的开放标准发展。协议的一部分包括在名为 VMware Community Source 的新计划中与这些合作伙伴共享 ESX Server 源代码。2005 年 8 月，Sun Microsystems 还宣布将支持在 Sun Fire x64 系统上使用 VMware ESX Server。

正如您所见，对于虚拟化社区来说，这是一个有趣的时代。未来还有更多。VMware ESX Server 的新版本（v3）即将到来，来自 Intel 和 AMD 的新处理器将包含虚拟化支持，这将使该技术在性能、可扩展性和稳定性方面达到更高的水平。

凭借 Rob 关于使用 VMware 的指南的第二版，我希望我能成功帮助您充分利用 VMware 产品，并为您提供当前可用的 VMware 软件的良好概览。

## 本书涵盖的内容

这是我的 VMware 指南的第二版。第一版收到的反馈非常好，让我对新版可以添加或更改的内容有了很多了解。当然，我已更新 VMware Workstation 部分以支持 2005 年 4 月发布的版本 5。然而，我在 Linux 平台上也取得了很大进展，并在新版中添加了大量关于 Linux 平台上 VMware 的新材料。

在本新版中，物理到虚拟转换、集群以及关于安装和配置的操作系统特定章节已得到更新。

本书的新部分是 VMware ACE 以及 VMware 服务器产品：GSX Server 和 ESX Server。2005 年夏季出现了几本关于 VMware ESX Server 的新书。对于该产品的深入技术讨论，我建议您阅读其中一本新书。我尝试撰写了 VMware ESX Server 的全面介绍，这将帮助您入门，也将帮助您决定应选择哪种 VMware 产品。

## 关于作者

Rob Bastiaansen 在国际 VMware 社区中享有盛名。他自 2000 年开始使用 VMware 2 版本以来，就一直将自己的网站致力于 VMware 产品。他是第一个描述如何在 VMware 中为 NetWare 和 Windows 操作系统设置集群的人。此后他回答了许多关于 VMware 产品和集群的问题，并于 2004 年 7 月出版了他 VMware 指南的第一版。他还为居住地荷兰的技术杂志发表了关于 VMware 技术的文章。

2005 年，Rob 出版了他的第二本书《The NetWare Toolbox》。此外，2005 年初他创办了自己的出版公司 Books4Brains。除了出版自己的书籍外，Books4Brains 还为其他作者提供出版书籍的框架，其条件是大型出版公司无法提供的。

Rob 拥有自己的公司并担任顾问和讲师。他大部分工作都集中在 Novell 软件和 VMware 技术上。他是 Master Certified Novell Instructor、Certified Directory Engineer 和 Novell Certified Linux Engineer。他还通过了 Linux Professional Institute 的认证以及 Microsoft Certified Systems Engineer 认证。Rob 使用所有主要操作系统，包括 NetWare、Windows 和 Linux。

## 关于读者

显然，你阅读本书是因为你对 VMware 技术感兴趣。无论你想开始使用 VMware Workstation，还是想使用 NetWare 或 Windows 集群设置高级配置，本书都适合你。在撰写本书时，我假设你了解如何在 VMware 中安装你想要使用的操作系统。因此，你不会找到有关如何设置 Windows、Linux 或 NetWare 的详细说明。我还假设你能够阅读文档手册，因此我选择不涵盖太多基础信息，例如如何将 USB 设备或其他设备添加到你的虚拟机。

然而，如果你对 VMware 产品还不熟悉，你会找到一个部分，描述 VMware 技术是什么以及如何设置你的第一台虚拟机。这些信息之所以包含在内，并不是因为手册中没有涵盖；相反，它是包含在内的，因为许多人只需要一些基本指南即可入门，并且他们可能希望快速上手。一个例子是：当你以前没有使用过 VMware 时，如何开始在 VMware 中进行集群。

如果你是有经验的 ESX 服务器管理员，本书的介绍章节不会教你任何新东西。然而，本书涵盖的整个 VMware 产品范围的配置技巧将包含至少一些对你的环境有用的材料。

最后，你可能正在寻找有关使用 VMware 的技巧，例如如何创建 Virtual Floppy Disks。你可能还需要 VMware 的故障排除技巧，或者你可能想使用虚拟机设置路由。你可以在本书中找到所有这些信息。

## 致谢

像许多作者一样，我必须感谢我的家人，在撰写本书期间给予我的支持。谈论 VMware 技术很有趣，但在树林里度过一天或玩游戏对于保持你专注于生活中真正重要的事情非常有帮助。

特别感谢 Novell 的 Ron van Herk 和 Robert Zondervan 与我分享他们关于 VMware Workstation 更新集群配置的信息。并且我还要感谢 Ronald Beekelaar 与我分享他在转换过程中关于 Virtual PC 的知识。

我希望你能喜欢本书中的虚拟化漫画。它们是专门为 Rob 使用 VMware 指南的第二版制作的，由 Howard Tayler 创作，Howard Tayler 是在线漫画太空歌剧 Schlock Mercenary 的创作者，该漫画每天可在 www.schlockmercenary.com 上找到。

## 第 1 部分

### VMware Workstation 和 VMware ACE 简介

![](img/25fe75b93b97a021effaba85db112a52_16_0.png)

## 1 VMware 概述

本章将向你介绍 VMware 的产品线。这些产品范围从桌面解决方案到企业服务器环境。我将首先概述 VMware 技术是什么，然后介绍各个 VMware 产品。

### 1.1 VMware 的工作原理

有多种 VMware 产品可供使用。本书主要关注所谓的托管产品。这些是需要 Windows 或 Linux 作为虚拟机环境主机的产品。我还包含了 VMware ESX Server 的介绍，它不需要主机操作系统，但它自带操作系统来运行虚拟机环境。

你选择使用哪个版本其实并不重要；所有版本的 VMware 运作方式都非常相似。你需要了解的关于创建虚拟机的知识对所有 VMware 产品都基本相同。我将首先关注桌面产品，然后在本章后面简要概述服务器版本。

通过使用 VMware 技术，你可以在计算机上创建一台或多台 PC，并可同时运行。你的主机计算机仍运行其自己的操作系统（Windows 或 Linux），而虚拟机可以运行其他操作系统（Windows、Linux、NetWare）。它们都使用你 PC 的内存，其处理器指令由主机计算机的 CPU 处理。

#### 主机和客户机

这就引出了你在操作 VMware 时必须理解的一些术语。我们称运行 VMware 软件的计算机为主机。该主机 PC 可以具有 Windows 或 Linux 操作系统。你必须选择将使用哪个操作系统作为主机，因为你需要为 Windows 或 Linux 购买特定版本。

你在主机上运行的虚拟机称为客户机。它们可以运行许多操作系统，因此你的底层主机运行什么操作系统并不重要。因此，你可以在 Windows PC 上运行 Linux，在 Linux PC 上运行 NetWare，或在 Windows 主机上运行另一个版本的 Windows。下一节描述了 VMware 的一些使用场景。

#### 主机和客户机硬件使用

你运行的客户机是全新的 PC。当你开始使用 VMware 时，必须记住在真实 PC 上可以完成的事情也可以在 VMware 中完成。唯一的限制是硬件；你不能在虚拟机中添加物理设备，例如视频采集卡。然而，你可以做其他所有事情，例如网络、磁盘映像等等。你所做的一切都不会感染主机 PC。当然 PC 性能会受到影响，因为你在主机和客户机之间共享资源。
