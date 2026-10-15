
参考 189

- `system-config-mouse`—Fedora 的图形化鼠标配置工具
- `gdmsetup`—GNOME 显示管理器配置客户端
- `startxA`—一个用于从 shell 命令行启动一个或多个 X 会话的 脚本
- `sxri`—一个显示管理器桌面装饰客户端

![](img/d4ad9a7c85702c925b4288f587284a4f_225_0.png)

图 6.12。你可以使用 KDE 控制中心来管理 KDE 桌面会话的几乎每一个方面。

# 参考文献

http://www.x.org/—X 窗口系统的维护者。

http://www.x.org/Downloads_mirror.html—想下载 X 最新修订版本的源码吗？从这个镜像站点列表开始。

http://www.free86.org/—XFree86 项目 Inc. 的主页，该项目近 10 年来为 Linux 提供了图形化界面。

http://www.kde.org/—学习 KDE 及其最新进展的起点。

http://www.gnome.org/—关于 GNOME 更多信息的发布、新客户端链接以及 GNOME 开发项目的入口。

http://people.redhat.com/~hp/metacity/—Havoc Pennington 的 metacity 下载页面，你可以在这里获取此窗口器的最新全源码版本。

http://sawmill.sourceforge.net/—sawfish 窗口管理器（以前名为 sawmill）的主页。

http://www.windowmaker.org/—Window Maker 最新版本的源码来源。

http://www.icewm.org/—IceWM 的主页。

http://www.lestif.org/—LessTif 项目的主页，该项目旨在提供 GNU GPL 版本的 OSF/Motif 兼容软件库。

http://scwm.sourceforge.net/—一个轻量级但支持虚拟桌面的窗口管理器的主页。

http://www.fvwm.org/—FVWM2 的主页，你可以在这里下载最新版本。

http://www.novell.com/products/desktop/—学习 Ximian GNOME 的起点。

# 第 7 章

## 本章内容

# 软件管理

- 使用 RPM 进行软件管理
- 软件管理的替代方案
- 为源码编译软件
- 参考文献

在本章中，我们将介绍你在 Fedora 中管理软件的各种选项。如果你习惯于 Windows 环境，依赖于访问多个供应商网站来下载更新，那么你将大开眼界了！更新整个 Fedora 安装（包括所有应用程序软件）就像在命令行输入 `update` 一样简单。你将发现安装甚至删除各种软件包是多么而易举。

Fedora 为系统资源管理提供了多种工具。接下来的章节将介绍 RPM 软件包管理器 `RPM` 以及命令行和图形化软件管理工具。你还将学习如何监控和管理系统的内存和磁盘存储。

# 使用 RPM 进行软件管理

`RPM` 部分源自早期用 Perl 语言编写的 Linux 软件包归档——分别命名为 `RPP`、`PMS` 和 `PM`。`RPM` 首次于 1999 年随 Red Hat Linux 2.0 推出，随后在 1996 年为 Red Hat Linux 3.0.3 `Picasso` 版本用 C 语言重写。从那时起，`rpm` 命令一直是 Red Hat 独特软件管理系统的核心特性，该系统基于“纯净源码”`pristine sources` 的概念，即使用单个程序源码的初始存档来为不同的系统构建包并跟踪版本的能力。 随着 2002 年 Hat 8.0 `Psyche` 的发布，Red Hat 为其卓越的 RPM 应用提供了一个略微更新的图形化管理界面。

除了改进早期软件管理脚本的包管理功能外，`RPM 4.1` 还引入了软件特性，旨在简化从单组源码文件为不同平台构建软件的任务。更改可以被跟踪并保留在开发者的初始源码之外，并且可以同时从头构建并安装多个软件包——同时，`RPM` 还会验证依赖关系。其他功能，如校验和和 GNU 隐私卫士 `GPG` 签名，使得二进制软件包能够安全地分发，而不必担心病毒感染或包含木马代码。

`rpm` 命令使用 RPM 系统来安装、删除（擦）、升级、验证和构建名为 `.rpm` 文件的软件归档。这些存档（或软件包）包含软件包标识（签名）、校验和（通过数学推导出的值）以及软件的索引（无论是源码或二进制格式）。一个 `.rpm` 软件包还包含一些额外信息，如名称、版本和基本描述，并可以包含用于软件安装、删除或升级的预安装和后安装脚本。

安装在你上的 RPM 数据库跟踪安装了哪些版本的软件包。`RPM` 使用你系统的 `/var/lib/rpm` 目录来存储包含系统上安装软件信息的文件（实际上是数据库）。你可以使用命令来查看文件（取决于你安装的软件数量，你可能会看到这里显示的文件大小）：

```
total 49288

-rw-r--r-- 1 rpm 548860 Oct 24 21:05 Basenames

-rw-r--r-- 1 rpm 12288 Oct 23 21:05 Conflict

-rw-r--r-- 1 rpm 215080 Oct 24 21:05 Conflict

... (此处省略重复行)
```

## 使用 RPM 进行软件包管理

# RPM 也适用于程序员！

请记住，`RPM` 的创建不仅是为了提供一个易于使用的管理工具，还作为一种开发人员工具，用于多平台源码包的管理。使用 `rpm` 进行开发和分发时将需要用到 `rpmbuild` 命令，以及许多额外的命令行标记。`RPM` 可用于构建二进制文件、执行程序、安装、验证和签名软件包、构建源码包、跟踪版本，以及针对特定架构的构建目标。详细信息可以在 RPM 主页上找到（列在本文章末尾的“参考”部分）。

## 在命令行中使用 rpm

由于新颖的图形化 `rpm` 客户端目前只能安装和卸载 RPM 软件包（未来承诺提供更多功能），你最终仍然需要从命令行管理 rpm 软件包。你可以通过命令行使用 `rpm` 命令执行所有基本操作。本节将向你介绍如何执行这些操作。它还提供了如何安装、验证、查询、删除和升级软件包的示例。

最常见的 `rpm` 操作是软件安装。使用 `rpm` 是跟踪已安装软件的简单方法，并可用于快速删除不需要的软件包。使用 `-i` 选项，配合软件包的完整名称或部分名称（使用正则表达式），用 `rpm` 安装软件。例如，要安装 `unace` 压缩归档包，可以使用如下 `rpm` 命令：

```bash
# rpm -ivh http://mirrors.zoreil.com/plf.zarb.org/mandrake/10.0/i586/unace-2.2.plf.i586.rpm

Retrieving http://mirrors.zoreil.com/plf.zarb.org/mandrake/10.0/i586/unace-2.2.plf.i586.rpm

warning: /var/tmp/rpm-xfer.48amVs: V3 Dsa signature: NOKEY, key ID 8df56d05 [100%]

Preparing...

################################ [100%]

1: unace
```

此示例使用了 `v` 和 `h` 选项，它们提供了更详细的输出并显示哈希标记以显示安装进度。它展示了 `rpm` 使用 HTTP 或 FTP 服务器获取安装文件的能力。它还显示 `rpm` 可以验证有效的密钥（在我们的示例中并未安装密钥）。

你可以在安装软件包后使用 `rpm` 查询其数据库以验证系统的安装情况。使用 `-V` 选项配合软件包的名称，如下所示验证安装：

```bash
# rpm -V unace
```

## 第 7 章 管理软件

注意

如果你的软件安装无误，在你运行命令 `rpm -V` 后，系统不会任何响应；只有出现问题时才会显示。

从下面的程序输出可以看出，你可以通过向 `-V` 选项添加额外的验证选项（例如两个 `v`）来获取有关软件包的更多信息。要获取已安装软件包的更多信息，使用一个或多个 `rpm` 查询选项。例如，要显示已安装软件包的控制台信息，使用 `-q` 选项、`i` 选项和已安装软件包，如下（注意你的版本将与此处不同）：

```bash
# rpm -qi yum

Name : yum               Relocations: (not relocatable)

Version : 2.4.0            Vendor: Red Hat, Inc.

Release : 0.fc4
```
