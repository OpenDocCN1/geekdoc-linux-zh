
这会将你的打印机发布到网络，并允许其他通过 Windows 客户端连接它们。

确保你使用之前显示的命令重启 Samba 服务，以便 Samba 识别到配置文件的更改。

例如，要在仅有 USB 接口的计算机上托管并行端口打印机，可以使用一个廉价的 USB 转并行转换器将打印机连接到计算机。USB 转并行转换器通常提供一个中枢（Centronics）接口；其一端插入旧式打印机，另一端插入 USB 接口。将 USB 接口插入您的集线器、台式机或网络 USB 端口。如果旧电脑没有内置 USB 端口，可以使用扩展 PCI 卡来增加对打印（或其他设备）的支持。USB 接口卡至少提供两个端口，您还可以通过集线器级联设备。

## 相关的 Ubuntu 和 Linux 命令

以下命令可以帮助您管理打印服务：

- `accept`—通过命令行控制作业对 CUPS 服务器的访问。
- `cancel`—从命令行取消打印任务。
- `disable`—从命令行控制打印功能。
- `enable`—启用 CUPS 打印机。
- `lp`—将文件发送到打印机并允许控制打印服务。
- `lpc`—在控制台显示打印机和打印服务的状态。
- `lpq`—在控制台查看打印队列（待处理的打印任务）。
- `lpr`—通过命令行从打印队列中移除任务。
- `lpstat`—显示打印机和服务器状态。

## 参考文献

- [https://help.ubuntu.com/community/SettingUpNFSHowTo](https://help.ubuntu.com/community/SettingUpNFSHowTo)—设置 NFS 的 Ubuntu 社区文档。
- [https://help.ubuntu.com/community/SettingUpSamba](https://help.ubuntu.com/community/SettingUpSamba)—设置 Samba 的 Ubuntu 社区文档。
- [https://help.ubuntu.com/community/Swat](https://help.ubuntu.com/community/Swat)—SWAT 的 Ubuntu 社区文档。
- [www.samba.org/](www.samba.org/)—获取更多关于 Samba 信息以及在 Linux、UNIX、Mac OS X 和其他操作系统上使用 SMB 协议的基础条目。
- [www.samba.org/samba/docs/man/Samba-HOWTO-Collection/SWAT.html](www.samba.org/samba/docs/man/Samba-HOWTO-Collection/SWAT.html)—使用 SWAT 的官方 Samba 文档。
- [www.linuxprinting.org/](www.linuxprinting.org/)—在此浏览特定驱动程序以及 USB 及其他类型打印机的信息。
- [www.cups.org/](www.cups.org/)—CUPS 软件和信息的综合仓库。
- [www.pwg.org/ipp/](www.pwg.org/ipp/)—互联网打印协议（IPP）标准的主页。

# 第 23 章

## 本章内容

- 关于 Apache 服务器
- 安装 Apache 服务器
- 启动和停止 Apache
- 运行时服务器配置设置
- 文件系统身份验证与访问控制
- Apache 模块
- 虚拟主机
- 日志
- 参考文献

## Apache Web 服务器管理

本章涵盖了 Apache Web 服务器的配置和管理，包括服务器一些主要组件的概述，并对基于文本和图形的服务器配置进行了讨论。在本章中，您将学习如何使用命令行启动、停止和重启 Apache。本章从介绍性信息开始，向您展示如何安装、配置和使用 Apache。

## 关于 Apache 服务器

根据 Netcraft 对 2011 年 7 月活跃网站的调查，Apache 是当今网上最广泛使用的 Web 服务器，如表 23.1 所示（来自 http://netcraft.com/archives/2011/07/08/j-2011-web-server-survey.html）。

注意，这些统计数据并不反映内部网络（即内网）。

Apache 这个名字出现于软件开发早期，是因为它是一个“打补丁的服务器（a patchy server）”，由免费提供的 NCSA HTTPd Web 服务器源代码的补丁组合而成。在 NCSA HTTPd 项目停止后的一段时间内，许多人为代码编写了各种补丁，以修复漏洞或实现他们想要的功能。许多代码在外面流传，人们自由地分享，但它们完全没有经过管理。

一段时间后，Brian Behlendorf 和 Cliff Skolnik 为这些补丁建立了一个中央仓库，Apache 项目随之诞生。

# 第 23 章 Apache 管理

（注：此处原文后续内容为大量乱码和重复信息，已根据文档工程原则终止翻译）

- `/usr/share/`——如果你已经安装了 `apache2` 软件包，你将在该目录下找到 HTML 格式的 Apache 文档。你可以通过浏览器访问 http://localhost/manual/ 来查看它。
- `/usr/share/man/`——Ubuntu 的软件包也包含了 `man` 页面，位于此目录下。例如，`apache2` man 页面位于 `man` 目录的第 8 部分。
- `/usr/bin/`——可执行程序放置在此目录。这包括服务器本身的可执行文件和各种工具。
- `/usr/bin/`——Apache 软件包中的一些工具放置在这里——例如，用于生成密码文件的 `passwd` 程序。
- `/var/log/apache2/`——服务器日志文件放置在此目录中。默认情况下，这里有两个重要的日志文件（以及多个）：`access_log` 和 `error_log`。不过，你可以定义任意包含各种信息的自定义日志。详情请参阅本章后面的“日志记录”部分。

当 Apache 运行时，它还会在`/var/run/`目录下创建`apache2.pid`，该文件包含 Apache 父进程的 ID。

> 如果你正在升级到更高版本的 Apache，APT 不会覆盖你当前的配置文件。

## 手动编译源码

你可以直接从 www.apache.org 下载源码。本文写作最新版本是 2.2.19，尽管 2.0.64 版本也完全支持并可用。由于脚本和其他兼容性原因，许多网站继续使用1.3 系列等旧版本，大多数网站正在迁移或开始使用最新稳定版本。我们强烈建议使用当前支持的稳定版本。网站提供了 2.3 beta 版本供测试使用，但不应在生产服务器上使用。

获取 tar 文件后，必须在临时目录（如 `/tmp`）中打开它。打开此 tar 文件会创建一个名为 `apache_version_number` 的目录，其中 `version_number` 是下载的版本（例如 `apache_2.2.19`）。

编译源码有两种方法：通过编辑 `make` 模板（对于我们多年多年 Apache 的人来说，这是老旧的方法），以及使用 `configure` 脚本的新方法。`configure` 脚本将首先显示如何从源码构建 Apache。然而，在构建和安装 Apache 之前手动编辑配置文件，可以更好地控制软件的安装方式以及内置 Apache 的功能或特性。

**提示**：与 Linux 和其他类 Unix 系统中许多以源码形式分发的软件包一样，提取源码会得到一个包含 `README` 和 `INSTALL` 文件的目录。在尝试构建和安装软件之前，务必仔细阅读 `INSTALL` 文件。

## 使用 ./configure 构建 Apache

要简单地构建 Apache，请在创建的目录中运行 `./configure` 脚本。你可以为它提供 `--prefix` 参数，将其安装在默认目录 `/usr/local/apache/` 以外的目录。使用此命令：

```
matthew@/usr/apache$ sudo ./configure --prefix=/preferred/directory/
```
