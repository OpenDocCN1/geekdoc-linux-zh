

## 摘要

本章旨在为您提供所需的知识，使您能够自信地在系统上添加、移除和升级软件包。您现在应该能够做到以下几点：

- 使用包管理工具定制系统上安装的软件包
- 使用包管理器直接从 .rpm 文件安装额外软件
- 使用 RPM 命令行界面查询、安装、移除、升级和验证 .rpm 文件
- 通过检查其 GnuPG 签名文件，确保从 Red Hat 接收到的更新 .rpm 文件是真实的
- 了解在系统上解压缩和安装 TAR 文件的基本原理，以便在无法使用 .rpm 文件时知道如何继续操作。

本章旨在让您对 Red Hat 的包管理软件有个初步了解和实用的知识。如果您有兴趣深入了解，以下资源将很有帮助：

- Red Hat RPM 文档：http://www.redhat.com/docs/manuals/linux/RHL-9-Manual/custom-guide/
- Max RPM：http://www.rpm.org/max-rpm/
- 开源软件门户：http://freshmeat.net/
- RPM 搜索门户：http://rpmfind.net/linux/RPM/

在下一章中，我们将探讨一些随您的 Red Hat Linux 9 发行版一起提供的众多应用程序中的几个，这些应用程序在日常使用中可能对您很有用。

## 5 日常应用程序

您已安装 Red Hat Linux 9 操作系统；您已连接到互联网；也许您还安装了一些软件包。那么，那些日常任务该怎么办呢？您如何着手使用新的操作系统来完成所有那些重要的工作，例如电子邮件、创建文档和电子表格（甚至一些更有趣的工作，如处理图形、听音乐，甚至开发应用程序）？

在本章中，我们将调查 Red Hat Linux 9 发行版中可用的众多应用程序中的一些。Red Hat Linux 9 附带了令人眼花缭乱的各种应用程序，要在单一章节中涵盖它们*全部*是不切实际的；但我们会向您展示我们认为您最可能需要用来完成那些重要日常任务并享受乐趣的应用程序。

我们将本章中的应用程序分为以下几个部分：

- 办公应用程序
- 互联网应用程序
- 个人信息管理应用程序
- 多媒体应用程序
- 系统应用程序

在每个部分中，我们将讨论安装该应用程序所需的内容（如果它尚未默认安装），以及如何根据您的需求配置安装。我们还将指出这些应用程序与您可能熟悉的其他应用程序（例如 Microsoft 操作系统上找到的应用程序）之间的一些异同。

我们还将涵盖仿真技术——这些技术能够仿真 Microsoft Windows 操作系统，或解释 Windows 应用程序并允许其在 Linux 上运行。如果您例如正在考虑开发跨平台应用程序，并希望检查其与 Linux 和 Windows 操作系统的兼容性，那么这些技术将引起您的兴趣。

作为一次概览，本章旨在展示可用的内容，而不是作为单个应用程序的用户指南。对于大多数这些应用程序，在线帮助非常全面且编写精良，可以通过应用程序的帮助菜单访问。此外，我们将提供提供进一步文档和支持的网站 URL。

### 办公应用程序

虽然这不一定是最令人兴奋的话题，但不可否认的是，我们大多数人都会花费至少一些时间来创建和维护办公文档，如文档、电子表格和演示文稿。因此，我们将以介绍 Linux 中可用的办公生产力应用程序开始本章。（作为奖励，我们将在下一节中查看互联网应用程序！）

由于这些办公任务非常重要，Red Hat Linux 9 附带了多种不同的办公应用程序。其中一些应用程序功能丰富，可与 Microsoft Office 等相媲美，而其他应用程序体积较小但仍值得一提。这些应用程序应该足以满足您的需求——如果不够，互联网上还有更多可用的 Linux 办公应用程序套件。

我们将以简要调查 Red Hat Linux 9 中包含的所有办公应用程序套件开始这一部分。我们无法深入涵盖所有这些，因为篇幅有限；但通过更仔细地查看 Red Hat Linux 9 中的标准办公套件 *OpenOffice*，我们将让您了解您可以实现的目标。

### Red Hat Linux 与办公应用程序

以下办公应用程序套件均可在 Red Hat Linux 9 中获得：

- OpenOffice 套件是在使用默认设置安装 Red Hat Linux 9 时安装的办公套件。OpenOffice 由多个应用程序组成，包括：
  - OpenWriter（用于文字处理）
  - OpenCalc（用于电子表格）
  - OpenDraw（用于图形）
  - OpenImpress（用于演示文稿）

  OpenOffice 是此处列出的套件中功能最强的，我们稍后会对其进行更详细的研究。

- **StarOffice** 套件可以说是市场上最流行的 Linux 办公套件之一。撰写时的最新版本是 **StarOffice 6.0**。这是一款商业产品，具有完整的支持计划（包括帮助台支持），并包含从第三方供应商获得的额外功能授权。有关 StarOffice 最新版本的更多信息，请访问 http://www.sun.com/staroffice。

  本书中包含的 Red Hat 出版商版，包含 OpenOffice，它与 StarOffice 6.0 共享相同的代码库。有关 OpenOffice 的更多信息，请访问 http://www.openoffice-org。

- **Koffice** 套件是最初的办公套件之一。它完全集成，并适用于 K 桌面环境（KDE）。它提供了一系列应用程序，包括：
  - KWord（用于文字处理）
  - KSpread（用于电子表格）
  - KPresenter（用于演示文稿）
  - Kivio（用于流程图）
  - Krita（用于图形应用程序）

  您可以从 http://www.koffice.org 免费获取 Koffice。撰写时版本为 1.2.1。

- **GNOME Office** 办公应用程序套件也由多个应用程序组成，包括：
  - AbiWord（用于文字处理）
  - Gnumeric（用于电子表格）
  - Gimp（用于图形）
  - MrProject（用于项目管理）

  然而，应注意 GNOME Office 不像 OpenOffice 套件那样紧密集成。更多信息可在 http://www.gnome.org/gnome-office 找到。

> OpenOffice 的开发作为开源项目继续进行，隶属于 OpenOffice.org。虽然 OpenOffice 建立在最初的 StarOffice 代码库之上，但为 OpenOffice 开发的代码将纳入 StarOffice 产品套件的 future 版本中。

> 此外，Sun Microsystems 已将 OpenOffice 整合到 Gnome Office 套件中。如果您正在比较应用程序，这将解释您可能遇到的任何相似之处！

### 安装办公应用程序

大多数默认办公和生产力应用程序的软件包都列在 **Office/Productivity** 软件包组中，您可以在我们在第 4 章中讨论的 Red Hat 包管理（RPM）应用的 **Applications** 类别下找到它。（有一两个例外；例如，GIMP 列在 **Graphics** 软件包组中。）

您可以通过启动 RPM 来查看当前机器上安装了哪些办公组件。为此，请选择 **主菜单** | **系统设置** | **添加/移除应用程序**（除非您已以 root 身份登录，否则会被提示输入 root 密码），向下滚动到 **Applications** 类别，找到 **Office/Productivity** 软件包组，然后点击 **详细信息** 按钮。您应该会看到类似以下内容：

![](img/b852150740856958b10aff9e8c9d2adc_161_0.png)

如您所见，**Office/Productivity** 软件包由 12 个软件包组成，包括 OpenOffice 套件的一个软件包，Koffice 套件的一个软件包，以及构成 GNOME 套件一部分的多个软件包。当您在任何版本中安装 Red Hat Linux 9 时，这些软件包中有四个（包括 OpenOffice 套件）是在默认安装中安装的：

