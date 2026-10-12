

## 图 6.12

![](img/774d40fd20903495c5cd00e2efad3f33_219_0.png)

您可以使用 KDE 控制中心来管理 KDE 桌面会话的几乎每个方面。

## 相关的 Fedora 和 Linux 命令

您可以使用以下命令在 Fedora 中创建和配置 X 窗口系统：

- Xorg——X.Org 基金会提供的 X 窗口系统发行版中附带的 X 服务器
- mouseconfig——Fedora 基于文本的 GUI 指点设备配置程序
- kcontrol——KDE 控制中心客户端
- system-config-display——Fedora 的图形化 X11R6 配置工具
- system-config-mouse——Fedora 的图形化鼠标配置工具
- gdmsetup——GNOME 显示管理器配置客户端
- startx——用于从 shell 命令行启动一个或多个 X 会话的 shell 脚本
- xsri——显示管理器根桌面装饰客户端

## 参考链接

- http://www.x.org——X 窗口系统的维护者。
- http://www.x.org/Downloads_mirror.html——想要下载 X 最新修订版的源代码吗？请从这个镜像站点列表开始。
- http://www.xfree86.org——The XFree86 Project, Inc. 的主页，该公司在近 10 年间为 Linux 提供了图形界面。
- http://www.kde.org——学习和了解 KDE 及其最新发展的起始之地。
- http://www.gnome.org——获取更多关于 GNOME 的信息、新客户端链接以及 GNOME 开发项目的起点。
- http://people.redhat.com/~hp/metacity/——Havoc Pennington 的 metacity 下载页面，您可以在这里获取此窗口管理器的最新完整源代码版本。
- http://sawmill.sourceforge.net——sawmill 窗口管理器的主页。
- http://www.windowmaker.org——Window Maker 最新版本的来源。
- http://www.icewm.org——IceWM 的主页。
- http://www.lesstif.org——LessTif 项目的主页，该项目旨在提供与 OSF/Motif 兼容的软件库的 GNU GPL 版本。
- http://scwm.sourceforge.net——一个轻量级但支持虚拟桌面的窗口管理器的主页。
- http://www.fvwm.org——FVWM2 的主页，您可以在这里下载最新版本。
- http://www.novell.com/products/desktop/——Ximian GNOME 的入门之地。

# 第 7 章

# 管理软件和系统资源

本章介绍用于管理 Fedora Core 系统上已安装系统资源的概念、流程和软件。管理计算机的系统资源（包括软件、存储和内存）非常重要，原因有很多。良好的资源管理能够促进并支持高效、富有生产力的会话、稳定的系统以及满意的用户。管理这些资源涉及安装、移除、升级或重建软件包——每一项都是有助于增强系统安全性的重要任务。

作为 Fedora Core 系统管理员，您还应该知道如何通过管理内存和存储来最大化系统资源，以实现最高效的系统使用。妥善管理系统资源可以确保您不会因为新软件而空间不足，并且可以根据不断变化的需求和新项目扩展系统。换句话说，系统资源管理对于为用户提供最佳计算体验至关重要。

Fedora Core 提供了多种系统资源管理工具。以下部分介绍了 RPM 软件包管理器 (RPM)，以及命令行和图形化软件管理工具。您还将了解如何在系统上监控和管理内存和磁盘存储。

## 本章内容

- 使用 RPM 进行软件管理
- 使用 Red Hat Network 及其他替代方案进行软件管理
- 从源代码编译软件
- 参考链接

## 使用 RPM 进行软件管理

RPM 部分源自早期的 Linux 软件包管理软件——名为 RPP、PMS 和 PM（用 Perl 编写）。RPM 最早用于 1995 年底的 Red Hat Linux 2.0，随后在 1996 年的 Red Hat Linux 3.0.3 (Picasso) 版本中被重写为 C 语言。自那时起，rpm 命令一直是 Red Hat 独特的软件管理系统的主要功能，该系统基于“原始来源”（pristine sources）的概念，即使用程序源代码的单一初始归档文件来为不同系统构建软件包并跟踪版本。随着 2002 年 Red Hat 8.0 (Psyche) 的发布，Red Hat 为其久经考验的 RPM 应用程序提供了一个略微更新的图形管理界面。

除了改进早期软件管理脚本的软件包管理外，RPM 4.1 版本引入了旨在简化从单一源代码文件集为不同平台构建软件的特征。更改可以被跟踪并保存在开发者的初始源代码之外，并且可以从头构建多个软件包并同时安装——与此同时，RPM 还验证安装依赖项。其他功能，如校验和和 GNU 隐私卫士 (GPG) 签名，使二进制软件包能够安全分发，无需担心病毒感染或特洛伊代码的植入。

rpm 命令使用 RPM 系统来安装、移除（擦除）、升级、验证和构建被称为 .rpm 文件的软件归档。这些归档（即软件包）包含软件包标识（签名）、校验和（数学推导出的验证值）以及软件归档（形式为源代码或二进制）。.rpm 软件包还包含大量额外信息，例如名称、版本和基本描述，并且可以包含用于软件安装、擦除或升级的安装前和安装后脚本。

安装在您计算机上的 RPM 数据库会跟踪哪些版本的哪些软件包已安装。RPM 使用您系统的 /var/lib/rpm 目录来存储包含已安装软件信息的文件（实际上是数据库）。您可以使用 ls 命令查看这些文件（根据您安装的软件数量，您看到的文件大小可能与此处显示的不同）：

```bash
$ ls -1 /var/lib/rpm
total 53820
-rw-r--r--    1 rpm    rpm      5423104 Oct 14 19:53 Basenames
-rw-r--r--    1 rpm    rpm       12288 Oct 14 12:32 Conflictsname
-rw-r--r--    1 root   root      16384 Oct 14 17:31 __db.001
-rw-r--r--    1 root   root     1318912 Oct 14 17:31 __db.002
-rw-r--r--    1 root   root      458752 Oct 14 17:31 __db.003
-rw-r--r--    1 rpm    rpm     1179648 Oct 14 19:53 Dirnames
-rw-r--r--    1 rpm    rpm      5521408 Oct 14 19:53 Filenames
-rw-r--r--    1 rpm    rpm       24576 Oct 14 19:53 Group
-rw-r--r--    1 rpm    rpm       20480 Oct 14 19:53 Installtid
-rw-r--r--    1 rpm    rpm       45056 Oct 14 19:53 Name
-rw-r--r--    1 rpm    rpm     41070592 Oct 14 19:53 Packages
-rw-r--r--    1 rpm    rpm      348160 Oct 14 19:53 Providename
-rw-r--r--    1 rpm    rpm       98304 Oct 14 19:53 Provideversion
-rw-r--r--    1 rpm    rpm       12288 Oct 14 19:53 Pubkeys
-rw-r--r--    1 rpm    rpm       237568 Oct 14 19:53 Requirename
-rw-r--r--    1 rpm    rpm       176128 Oct 14 19:53 Requireversion
-rw-r--r--    1 rpm    rpm        94208 Oct 14 19:53 Sha1header
-rw-r--r--    1 rpm    rpm        49152 Oct 14 19:53 Sigmd5
-rw-r--r--    1 rpm    rpm       12288 Oct 14 19:53 Triggersname
```

已安装软件的主要数据库包含在名为 Packages 的文件中。如您从前面的示例中看到的，如果您执行 Fedora Core 的完整安装（超过 4GB 的软件），该数据库可能会增长到 33MB（甚至更大）。安装 Fedora Core Linux 后，rpm 及相关命令将在软件管理操作期间使用此目录。

### 命令行和图形化 RPM 客户端

作为 Fedora Core Linux 系统管理员，您将使用 rpm 命令或 Fedora Core 图形客户端执行五项基本任务之一。这些操作必须由 root 操作员执行，包括以下内容：

- 安装新软件
- 擦除或移除过时或不再需要的软件包
- 升级已安装的软件包
- 查询以获取有关软件包的信息
- 验证软件包安装或完整性

rpm 命令拥有 60 多个命令行选项，但其管理功能可以根据上述五种行动类型进行分组。图形 RPM 客户端为这些操作提供了易于使用的界面。作为系统管理员，您可以选择使用图形界面或使用 rpm 的各种命令行选项。rpm 命令的一般格式为

```bash
# rpm option packagename
```

基本选项如下：

- **-i**——安装选定的软件包。
- **-e**——擦除（移除）选定的软件包。
- **-U**——移除当前已安装的软件包，然后安装选定软件包内容的软件，同时保留现有配置文件。
- **-q**——查询系统或选定的软件包。
- **-V**——验证已安装或选定的软件包。

