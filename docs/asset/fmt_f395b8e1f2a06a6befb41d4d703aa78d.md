
# 第8章 使用 Kubuntu

Ubuntu 是一个充满活力且多样化的社区，在全球范围内以多种语言保持活跃状态。其活动主要在在线的各种虚拟场所进行，包括邮件列表、IRC、Web 论坛、wiki 以及两个名为 The Fridge 和 Planet Ubuntu 的特殊 Web 社区门户网站。Ubuntu-com 通过现实中的会议和会议补充了这些虚拟活动。Ubuntu 社区被划分为各种团队和流程。在这个治理结构的顶端是 Ubuntu 社区委员会（Ubuntu Community Council）、技术委员会（Technical Board）以及 SABDFL Markworth。通过多种方式，该社区旨在让贡献变得容易。最终，这些贡献将通过一个最终导致官方项目成员身份和取消投票权的过程得到认可。

## 使用 Kubuntu

- Kubuntu 简介
- 安装 Kubuntu
- 在 Kubuntu 中导航
- 自定义 Kubuntu
- 系统管理
- 使用 Kubuntu 管理文件
- 常用应用程序
- 寻找帮助并回馈社区
- 总结

Kuntu 项目旨在提取 Ubuntu 的精华和 K 桌面环境（KDE）的精华，以创建一个出色的 Linux 发行版。本章涵盖了从 Kubuntu 到底是什么到如何管理并保持你的 Kubuntu 系统使用最新应用程序和修复的各种信息。Kubuntu 的目标是通过优秀的图形化工具提供一个简单易用的 Linux 操作系统，一个可以根据你的意愿轻松自定义的操作系统。

## Kubuntu 简介

Kubuntu 是 Ubuntu 的官方产品——由 Jonathan Riddell（Canonical Ltd. 的员工）和一大开发者团队领导的 Ubuntu 系统的完整实现。然而，Kubuntu 使用的是 KDE 而不是 Ubuntu 的 GNOME。Kubuntu 的主要目标是成为一个集成 Linux 发行版，拥有 Ubuntu 的优秀功能，但基于 KDE。由于 Kubuntu 是 Ubuntu 社区的官方组成，它遵循相同的 Ubuntu 宣言：优秀的软件应该是免费提供的，并且应该让人们用自己的语言使用，无论是否有残障。此外，人们应该能够以他们认为合适的方式自定义和更改他们的软件。

与 Ubuntu 类似，Kubuntu 做出了以下承诺：Kubuntu 将提供免费软件社区能提供的最佳翻译和可访问性基础设施；Kubuntu 将始终免费，且“企业”版没有额外费用；以及 Kubuntu 将始终提供来自 KDE 社区的最新最佳软件。

正在寻找某个软件吗？Kubuntu 都有它，其仓库中有超过 1000 种软件，包括最新的内核版本，当然，还有最新的 KDE。标准桌面应用程序（Web 浏览、电子邮件、文字处理和表格应用程序）让 Kubuntu 能够替换任何当前的桌面操作系统。如果你正在运行服务器——Web 服务器、电子邮件服务器或数据库服务器——Kubuntu 也可以胜任。

## KDE 历史

在1996 年，Matthias Etrich 发布了一篇新的新闻组帖子，描述了他在 UNIX 桌面上遇到的一些问题。

## Ubuntu 简介

UNIX 的流行归功于免费变体，大多数是 Linux。但仍然缺少一个持续的、美观且免费的桌面环境。目前有几个不错的免费或低价应用程序可用，如果我们能提供一个真实的图形界面（GUI），那么 Linux/X11 几乎可以满足所有人的需求……在我看来（IMHO），GUI 应该提供一个完整的图形环境。它应该允许用户用完成日常任务，如启动应用程序、读取邮件、配置桌面……所有部分必须相互契合。

目标不是为整个 UNIX 系统或系统管理员创建一个 GUI……这个想法是为终端用户创建一个 GUI。

随着那篇帖子的发布，他开始构建 KDE 项目。KDE 原本代表 Kool Desktop Environment，但后来被改为 K Desktop Environment。KDE 的吉祥物是一只名为 Konqi 的绿龙，可以在各种应用程序中找到它。

Matthias 选择围绕 Qt 工具包开发 KDE，到 1997 年，第一批大型、复杂的应用程序开始发布。然而，这引起了大量争议，因为 Qt 并没有使用免费软件许可证。这一争议产生了两个项目，一个名为 Harmony，它将仅使用免费库，另一个项目是 GNOME。1998 年，Qt 工具包根据一种名为 Q 公共许可证（QPL）的新源码许可证进行授权，并在2000 年，Qt 在 GNU 公共许可证（GPL）下发布。

KDE 主要是志愿者的努力。然而，许多公司雇用了开发者来开发此项目。这些公司包括 Novell（通过购买 SUSE Linux）和 Trolltech（生产 Qt 工具包的公司）。

在写作期间，KDE 的当前版本是 4.0.3。KDE 4.0 对桌面环境进行了大量更改，包括引入了 Plasma、Solid、Krunner 以及许多其他基础设施变化，其中大部分在本章中都得到了讨论。此时，仍有许多应用程序必须迁移到 KDE4，并且尚未利用这些功能。

有关关于 KDE 的更多信息，请访问项目网站 `www.kde.org`。项目主页还提供了有关你如何帮助和贡献项目的信息。

## Kubuntu 历史

当 Ubuntu 首次被讨论时，有传言说它将基于 GNOME，并且会排除 KDE。KDE 开发者 Jonathan Riddell 在他的博客上发表了一篇文章，该文成为了 Google 搜索热门。文章写道：

- 迹象表明这可能是一件大事，程度超过 Linscape、Xandros 或 Lycsis。与这些公司不同，他们理解自由软件和开放开发。这可能是一个基于 GNOME 的工作，但也许有一个 KDE 开发者正在为他们工作而没有声张。如果没有的话，我随时乐意帮忙。

安装 Kubuntu 就像安装 Ubuntu 一样。它非常简单。让我们从哪里可以找到它开始。

## 在哪里找到 Kubuntu

Kubuntu 可以在 `www.kubuntu.org/download.php` 获取。可以下载镜像文件并将其刻录到 DVD 或 CD-ROM 上。可以下载并使用两种不同的 Kubuntu 镜像。第一种是桌面 CD，它允许用户在不更改任何设置的情况下测试和运行 Kubuntu。第二种是备用 CD，提供了更高级的安装方式。

Kubuntu 8.04 的桌面 CD 是在系统上安装 Kubuntu 的主要方式。在朋友在他们的系统上安装之前，此 CD 是向他们展示 Kubuntu 强大功能的好方法。桌面 CD充充了光盘系统，允许 Kubuntu 在你的系统上运行而不会擦除任何已安装的内容。

## 选择适当的 Kubuntu 版本

要尝试或安装带有 KDE3 的 Kubuntu 8.04 或 Kubuntu 8.04 KDE Remix，请从 Kubuntu 网站（`www.kubuntu.org`）下载 CD 镜像。

## 如果我已经安装了 Ubuntu，我可以切换到 Kubuntu 吗？

如果你已经在系统上安装了 Ubuntu，那么安装和配置 Kubuntu 会非常简单。在 Synaptic 中，找到 `kubuntu-desktop` 包，它提供了让你的系统看起来和运行像 Kubuntu 的所有必要程序。别担心——你仍然可以在带有 GNOME 的 Ubuntu 和带有 KDE 的 Kubuntu 之间切换。一旦安装了 Kubuntu，你可以选择使用哪种桌面环境，GNOME 或 KDE。此外，如果你已经安装了 Kubuntu 并希望安装 Ubuntu，切换同样简单：只需安装 `ubuntu-desktop`，你将使用 GNOME 桌面。

一旦安装了 `kubuntu-desktop` 包，结束你的 GNOME 会话并从菜单中选择“Session”（会话）。选择 KDE 而不是 GNOME 作为你的窗口管理器，然后选择“Make Default”（设默认）。从现在起，当你登录时 KDE 将为你启动。

## 如果我目前正在运行带有 KDE3 的 8.04，我可以切换到 KDE4 吗？

如果你安装了带有 KDE3 的 Kubuntu 并对运行 KDE4 感兴趣，可以使用 Adept 安装并切换到 KDE4。打开 Adept，搜索 `kubuntu-kde4-desktop` 包并安装它。

### 从桌面 CD 安装

Kubuntu 具有直接从桌面 CD 安装的能力，因此无需下载单独的 CD；只需下载桌面 CD 并向你的朋友展示 Kubuntu 有多棒，或者进行首次测试运行。Kubuntu 的实时安装程序被称为 Ubiquity。

启动桌面 CD 后，你的桌面上会出现一个名为“Install”（安装）的图标。选择安装 Kubuntu，Ubiquity 将引导你完成安装阶段（图 8-1）。

Ubiquity 引导你设置正确的国家和时区（图 8-2）。

![](img/aa15f1f82061fdaf4ff1da575e3e1c52_317_0.png)

图 8-1 Ubiquity 欢迎界面

## 在 Kubuntu 中导航

你在哪里？

选择你所在国家和时区的一个城市。如果选择了正确的时区后显示的当前时间仍然不，你可以在重启进入已安装的系统后进行调整。
