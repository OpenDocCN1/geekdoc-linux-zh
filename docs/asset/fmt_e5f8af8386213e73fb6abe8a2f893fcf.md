
# 第四部分 额外章节

`filezilla-project.org`，它使用了一组跨平台的小部件，因此为 Kub 系统提供了一个相对轻量的图形化 FTP 客户端（在 Ubuntu 系统上运行得也非常好）。B2-15 显示了 FileZilla 正在显示远程 FTP 服务器的内容（右侧面板）和本地目录（左侧面板），你可以通过从中拖放文件来传输它们。

Ubuntu 或 Kub 系统默认情况下没有安装任何一种图形化 FTP 客户端，但它们都非常易于使用第 23 章中提到的任何软件安装机制进行安装。

## 图 B2-14

使用 `gtk-gftp` 图形 FTP 客户端

![](img/e3248f698da647444405a34229bd9df5_1245_0.png)

## 图 B2-15

使用 FileZilla 图形 FTP 客户端

![](img/e3248f698da647444405a34229bd9df5_1245_1.png)

44 `http://filezilla-project.org`，它使用了一组跨平台的小部件，因此为 Ubuntu* 提供了一个相对轻量的图形化 FTP 客户端

# 文件传输与共享

# B2

## 设置 FTP 服务器

Ubuntu 仓库中提供了各种 FTP 服务器：`inetools-ftpd`, `krb5-ftpd`, `muddleftpd`, `proftpd`, `pure-ftpd`, `pyftpd`, `twoftpd`, `vsftpd`, `wu-ftpd` 和 `zdftpd`。FTP 协议已经存在很长时间了，人们有足够的时间开发 FTP 服务器了！我不会对比和区分其中的每一个，因为它们都有自己的特点和发布版本，而且说实话，我不认为许多人会在意。我最喜欢的是 Pure-FTPd，它作为 Ubuntu 仓库中的 `pure-ftpd` 软件包可用。它安装简单、轻量级、配置简单、安全、完全国际化，并且根据你想运行的 FTP 服务器类型，具有多种模式。

在使用第 23 章中讨论的任何软件机制安装 `pure-ftpd` 软件包后，Pure-FTPd 即可以默认配置可以使用。安装了 Pure-FTPd 的系统上的任何用户现在都可以连接到他们的主目录并通过 `ftp` 传输文件。默认情况下，`/etc/pure-ftpd/conf` 允许到单词 "anonymous" 的匿名连接（默认情况下它包含 "yes"，这允许匿名用户）。接下来，在你的系统上创建一个命名的 FTP 用户以及你希望用户能够访问的主目录。（有关创建用户的信息请参阅第 1 章）。最后，使用命令 `/etc/init.d/pure-ftpd restart` 启动 Pure-FTPd 服务器。搞定！现在支持匿名用户了。

Pure-FTPd 有许多命令行选项，可以控制它的启动方式以及所有不同的运行模式，所有这些都可以在 `/etc/init.d/shutdown` 脚本中指定。Pure-FTPd 能够于设置虚拟 FTP 服务器、特定 IP 地址的 FTP 服务器、上传和下载配额等更多功能。它还带有各种管理命令，其中最受欢迎的是 `pure-ftpd` 命令，它可以显示所有当前 FTP 用户的信息以及他们正在的操作。

如果你擅于管理自己的 FTP 服务器，可以在 Ubuntu 或 KDE 系统上安装 PureAdmin（`pureadmin` 软件包）。Ubuntu 使用 GTK+2.x 小部件，这默认没有安装。如果你在 Ubuntu 系统上运行 KDE，也可以使用名为 `Kcmpuretpd` 的 KControl 软件包，但它有一段时间没有更新，并且与最新的 Pure-FTPd 配置存在一些问题——出于原则，我也避免使用它，因为 KControl 不是最新版本 KDE 选择的系统配置框架。

## 访问 Windows 系统上的共享

你的 Ubuntu 或 Ubuntu Linux 系统可以轻松访问 Microsoft Windows 系统上的共享目录（通常称为共享），从而创建了迄今为止最受欢迎且实用的开源软件包之一。[Samba](https://www.samba.org) 最初由 Andrew Tridgil 编写，他为此获得了无数奖项和赞誉。Tridgil 今天仍在进行工作，尽管有成千上万的人也对 Samba 做出了贡献，它现在是一项团队协作的工作。有关 Samba 的更多背景信息，请参阅额外章节 14，“设置 Samba 服务器”。

Samba 的名称来源于 SMB（服务器消息块）协议，这是 Microsoft Windows 系统网络文件共享的原始底层协议。Tridgil 通过对该协议及其工作原理进行海量逆向工程创建了 Samba，因为微软的 SMB 规范是公开的（真是个大惊喜）。今天，很大程度上归功于 Tridgil 和 Samba，微软开放了 SMB 规范，它现在是其更大的 CIFS（通用互联网文件系统）规范的一部分。

正如本章引言所述，你还可以使用 Samba 从 Linux 系统共享文件，使指定的目录看起来像 Windows 共享，并且 Windows 用户可以访问。这要求你设置 Samba 服务器，这在额外章节 14 中进行了了解释。本节侧重于从你的 Ubuntu Linux 系统的桌面访问共享 Windows 目录，并在 Windows 共享之间复制文件。

## 定位 Windows 共享

如果你不确定本地网络上可用的共享目录和相关服务器，可以使用 `smclient` 命令快速列出它们，它会提示你输入 Windows 密码，如下例所示：

```
$ smclient

Password:

WVH
```
