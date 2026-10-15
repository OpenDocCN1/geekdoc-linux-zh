
排除打印机故障可能会令人沮丧，尤其是当你发现新打印机无法在 Linux 上正常工作时。但请记住，目前市场上的几乎所有打印机都可以在 Linux 下工作。话虽如此，一些供应商在支持 Linux 方面的成功率更高。如果你想查看评分表，请访问 http://www.linuxprinting.org/vendors.html。

## 多功能（打印/传真/扫描）设备

可能存在问题的打印机，或者说那些可能无法在 Ubuntu 下正常工作的打印设备，包括将扫描、传真和打印功能合而为一的多功能（或一体机）打印机。在计划购买前，你应该进行调研，并避免选择任何不愿使用驱动程序或开发信息来支持 Linux 的供应商。

在 Linux 对多功能打印机的支持领域中，一个亮点是 HP 对 HP OfficeJet Linux 驱动程序项目的支持，该项目位于 http://hpoj.sourceforge.net/。许多型号都支持打印和扫描，而传真支持正在开发中。

## 使用 USB 和传统打印机

其他问题可能因缺少打印机的 USB 供应商和设备 ID 信息而出现——Linux 下某些 USB 扫描仪也存在这一问题。有关 USB 打印机支持的信息，请咨询 Linux 打印社区（位于本节开头的 URL）或 Linux USB 项目，网址为 http://www.linux-usb.org/。

尽管许多新型打印机需要通用串行总线（USB）端口，但 Linux 对传统的并行端口（IEEE-1284）打印机仍然提供了出色的支持，使各站点能够继续使用较旧的硬件。即使主机没有传统的并行打印机端口，或者你想在较旧的计算机上使用较新的 USB 打印机，你也可以利用 Linux 的变通方案来设置打印。

例如，要将基于并行端口的打印机连接到仅支持 USB 的计算机，可以使用廉价的 USB 转并行转换器将打印机连接到计算机。USB 转并行转换器通常提供一个 Centronics 连接器；该连接器的一端插入较旧的打印机，另一端插入 USB 连接器。然后将 USB 连接器插入你的集线器、台式机或笔记本的 USB 端口。另一方面，如果旧计算机没有内置 USB 端口，你可以使用附加的 PCI 卡来添加对打印（和其他设备）的 USB 支持。大多数 PCI USB 接口卡至少添加两个端口，并且你可以通过集线器串联设备。

## 相关的 Ubuntu 和 Linux 命令

以下命令可帮助你管理打印服务：

- `accept`—通过命令行控制对 CUPS 服务器的打印作业访问
- `cancel`—从命令行取消打印作业
- `disable`—从命令行控制打印
- `enable`—控制 CUPS 打印机
- `lp`—将指定文件发送到打印机，并允许控制打印服务
- `lpc`—在控制台显示打印机和打印服务的状态
- `lpq`—在控制台查看打印队列（待处理的打印作业）
- `lprm`—通过命令行从打印队列中移除打印作业
- `lpstat`—显示打印机和服务器状态
- `gnome-cups-manager`—显示 Ubuntu 的图形化打印机配置工具

## 参考

http://www.linuxprinting.org/—在此处浏览有关 USB 和其他类型打印机的特定驱动程序和信息。

http://www.hp.com/wwsolutions/linux/products/printing_imaging/index.html—HP 提供的关于 Linux 下打印产品支持的简短而权威的信息。

http://www.linuxdoc.org/HOWTO/Printing-HOWTO/—Grant Taylor 编写的 Printing HOWTO，其中包含在 Linux 下使用各种打印服务的信息。

http://www.cups.org/—CUPS 软件的综合性资源库，包括适用于 Red Hat Linux 的版本。

http://www.pwg.org/ipp/—Internet 打印协议标准的主页。

http://www.linuxprinting.org/cups-doc.html—有关 CUPS 的信息。

http://www.cs.wisc.edu/~ghost/—Ghostscript 解释器的主页。

http://www.samba.org/—获取有关 Samba 以及在 Linux、UNIX、Mac OS 和其他操作系统中使用 SMB 协议的更多信息的基本入口点。

此外，一本帮助你了解更多 Samba 知识的优秀书籍是 *Samba Unleashed*（Sams Publishing, 2000，ISBN: 0-672-31862-8）。

如果你想要更新近的 Samba 相关报道，我们还推荐 *Using Samba, 3rd Edition*（O'Reilly & Associates, 2007，ISBN: 0-596-00769-8）。

## 第 23 章

## 远程文件服务

使用 FTP

文件传输协议（FTP）曾被认为是网络上计算机之间传输文件的主要方法。如今 FTP 仍被广泛使用，尽管许多图形化 FTP 客户端现在已经补充了原始基于文本的界面命令。随着计算机的发展，FTP 也在不断演进，Ubuntu 提供了多种通过图形界面使用 FTP 传输文件的方式。

本章概述了 Ubuntu 随附的可用 FTP 软件，并介绍了一些有关初始设置、配置和使用特定 FTP 客户端的详细信息。Ubuntu 还包含一个名为 `vsftpd`（Very Secure FTP Daemon，非常安全的 FTP 守护进程）的 FTP 服务器软件包，以及许多可用于通过 FTP 协议提供和传输文件的关联程序。

## 使用 FTP 客户端

FTP 协议允许用户连接到服务器、读取目录和文件名，以及下载和上传数据。如果设置了正确的访问权限，用户还可以创建新文件夹并设置其访问权限。

然而，使用 FTP 存在安全风险：用户名和密码在局域网或互联网上以未加密方式传输。为了避免用户将身份验证信息泄露给任何窃听者的风险，许多站点仅启用匿名 FTP 登录和文件检索。许多 Linux 用户已转向更安全的替代方案，例如 OpenSSH 套件中包含的 `sshd` 和 `sftp` 或 `scp`。以下各节讨论新旧不同类型的 FTP 接口及其用法。因为它们是更大的

- 使用 FTP 客户端
- FTP 服务器
- 安装 FTP 软件
- FTP 用户
- 用于 wu-ftpd 的 inetd 配置
- 配置非常安全的 FTP 服务器
- 配置 Wu-FTPD 服务器
- 使用 ftpaccess 文件中的命令配置 wu-ftpd
- 配置 FTP 服务器文件转换操作
- 使用 ftphosts 文件中的命令允许或拒绝 FTP 服务器连接
- 服务器管理
- 参考

OpenSSH 套件的一部分，`sftp` 和 `scp` 命令将在第 19 章“使用 SSH 和 Telnet 进行远程访问”中介绍。

## FTP 客户端接口

使用基于文本的 FTP 接口有助于您理解图形化 FTP 会话中每个操作的作用。例如，当图形客户端无法自动检测所传输文件的类型时，这种理解就很有用。在这种情况下，二进制文件会以 ASCII 文件形式传输，因此毫无用处。相反，以二进制形式传输的 ASCII 文件会在每行末尾打印“M 控制字符”。这种错误通常出现在从较旧的 Microsoft Windows 操作系统向 Linux 传输文件时，因为 Windows FTP 客户端默认使用 ASCII 传输，而非二进制传输。

## 使用基于文本的 FTP 客户端接口

典型的 FTP 会话中可能会使用以下一些常用命令：

- `ascii`—为 FTP 会话设置 ASCII 文件传输类型。在发送或接收文本文件之前，使用此命令。
- `bin`—为 FTP 会话设置二进制文件类型传输。在传输二进制文件（如图形图像或压缩归档）之前使用它。
- `close`—在 FTP 会话期间关闭与远程服务器的连接。使用此命令而不是 `quit` 以返回 ftp 命令提示符。
- `get`—启动从 FTP 服务器到用户本地计算机的单个文件传输。使用此命令获取单个文件（例如 `get cartoon.jpg`）。
- `hash`—设置在文件传输期间使用井号标记 (#)。使用此命令可以直观地了解传输进度。
- `mget`—启动从 FTP 服务器到用户本地计算机的多个文件传输。使用此命令可通过单条命令下载（接收）多个文件（例如 `mget *.jpg`）。
- `mput`—启动从用户本地计算机到 FTP 服务器的多个文件传输。使用此命令可通过单条命令上传（发送）多个文件（例如 `mput *.jpg`）。
- `open`—使用 IP 地址或主机名打开与远程服务器的连接。在 ftp 命令提示符下工作时使用此命令（例如 `open ftp.redhat.com`）。
- `prompt`—这是一个交互式命令，当发出 `mput` 或 `mget` 命令时，会询问用户是否获取特定文件。如果用户启用提示后执行 `mget *`，FTP 客户端将提示用户传输 * 通配符匹配到的每个文件。当目录中有多个文件需要传输但有一两个文件不需要时，此功能特别有用。默认情况下，提示功能是开启的。
