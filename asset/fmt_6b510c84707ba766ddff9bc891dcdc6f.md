
![](img/c4a0ea5ab3561ff33a8da88887702720_655_0.png)

图 23.13 使用 CUPS 创建新的打印队列。

点击“继续”（`Continue`）按钮。你可以在“设备”（`Device`）页面中选择打印机访问类型（本地、远程、串口端口或互联网），如图 23.14 所示。例如，要配置向本地打印机打印，选择“并行端口 #1”；对于远程打印机，选择“`LPD/LPR` 主机”或“打印机”项。

![](img/c4a0ea5ab3561ff33a8da88887702720_656_0.png)

图 23.14 在 CUPS 管理页面中选择打印机设备。

再次点击“继续”，并按照图 23.15 所示的对话框中的要求选择打印机型号。

# 第 23 章节 文件与打印

![](img/c4a0ea5ab3561ff33a8da88887702720_657_0.png)

图 23.15 在创建新队列时选择打印机。

点击“继续”后，你将选择驱动程序。创建打印机后，你可以使用如图 23.16 所示的“打印机”页面打印测试页、停止打印服务、管理本地打印队列、修改打印机项或添加另一个打印机。

CUPS 提供了许多额外功能，在安装、配置并运行后，为 Fedora 提供了透明的传统 UNIX 打印支持。

> 注意：要了解更多关于 CUPS 的信息并获取系统的概述，请访问 http://www.cups.org/

## 避免打印机支持问题

![](img/c4a0ea5ab3561ff33a8da88887702720_658_0.png)

排查打印机问题可能会令人沮丧，尤其是当你发现打印机在 Linux 上无法正常工作时。首先，请记住，如今市面上几乎所有的打印机都能与 Linux 工作。然而，某些供应商在支持 Linux 方面表现更好。如果你想查看评分表，请访问 http://www.linuxprinting.org/vendors.html。

## 多合一（打印/传真/扫描）设备

存在问题的打印机，或者可能可能无法与 Fedora 可能的打印设备，包括了扫描、传真和打印服务的多功能（或*多合一*）打印机。你应该对任何计划中的购买进行研究，并避免任何不愿通过驱动程序或开发信息支持 Linux 的供应商。

Linux 支持多功能打印机领域的一颗亮之星是 HP 对 HP Office Linux 驱动程序项目的支持，地址为 http://hoj.sourceforge.net/。许多型号都支持打印和扫描，传真支持正在开发中。

## USB 和遗留打印机

由于缺少打印机的 USB 供应商和设备 ID 信息，可能会出现其他问题——某些 Linux 下的 USB 扫描仪已经解决了这个问题。有关关于 USB 打印机支持的信息，你可以咨询 Linux 打印相关人员（见本节开处的 URL）或 Linux USB 项目（http://www.linux-usb.org/）。

尽管许多较新的打印机需要通用串行总（USB）端口，但 Linux 对遗留并行端口（IEEE-1284）打印机提供了良好的支持，使得站点能够继续使用旧硬件。你可以利用 Linux 的变通方法来设置打印，即使主机计算机没有传统的并行打印机端口，或者你想在旧电脑上使用较新的打印机。

例如，要在仅支持 USB 的计算机上托管并行端口打印机，请使用廉价的 USB 转并行转换器将打印机连接到计算机。USB 转并行转换器通常提供一个 Centronics 接口；该连接器的一端插入旧打印机，而另一端插入 USB 接口。然后将该 USB 接口插入你的集线器、台式电脑或笔记本电脑的 USB 端口。另一方面，如果遗留计算机没有内置 USB 端口，你可以使用 PCI 扩展卡来为打印（以及其他设备）添加 USB 支持。大多数 PCI USB 接口卡至少增加两个端口，设备可以通过集线器进行级联。

## 相关的 FEDORA 和 LINUX 命令

以下命令可以帮助你管理打印服务：

- `accept`—通过命令行控制打印任务对 CUPS 服务器的访问
- `cancel`—从命令行取消打印任务
- `disable`—从命令行控制打印
- `enable`—控制 CUPS 打印机
- `ip`—将指定文件发送到打印机，并允许控制打印服务
- `ipcups`—在控制台显示打印机和打印服务的状态
- `ipq`—在控制台查看打印队列（待处理打印任务）
- `iprm`—通过命令行从打印队列中删除任务
- `ipstat`—显示打印机和服务器状态
- `system-config-printer`—显示 Fedora 的图形化配置工具
- `system-config-printer-ui`—显示 Fedora 的图形化配置工具

## 引用

- http://www.linuxprinting.org/—在此查看特定驱动程序以及 USB 和其他类型打印机的信息。
- http://www.hp.com/us-en/products/imaging/index.html—HP 关于 Linux 下打印支持的简要信息。
- http://www.linuxdoc.org/HOWTO/Printing-HOWTO/—Taylor 的打印 HOWTO，包含 Linux 下各种打印服务的信息。
- http://www.cups.org/—CUPS 软件的综合仓库，包括适用于 Red Hat 的。
- http://www.pwg.org/ipp/—互联网协议标准首页。
- http://www.linuxprinting.org/cups-doc.html—关于 CUPS 的信息。
- http://www.wisc.edu/ghost/—关于 Ghostscript（此处原文为关于 Samba 的信息）。
- http://www.linuxprinting.org/cups-doc.html—关于 CUPS 的信息。
- http://www.wisc.edu/ghost/—关于 Ghostscript（此处原文为关于 Samba 的信息）。
- http://www.linuxprinting.org/cups-doc.html—关于 CUPS 的信息。
- http://www.wisc.edu/ghost/—关于 Ghostscript（此处原文为关于 Samba 的信息）。

（注：原文示例中引用部分存在重复或混乱，翻译已按原意进行对应处理）

文件传输协议（FTP）曾是用于传输文件的主要方法，现在许多站点已转向更安全的替代方案，如 `sftp`。

# 第 24 章节 远程文件服务

## 使用 FTP 服务

- 使用 FTP 客户端
- FTP 服务器
- 安装打印软件
- 配置 FTP
- 使用 FTP 命令
- 管理
- 引用

## 使用 FTP 客户端

文件传输协议（FTP）允许用户连接到服务器，读取目录并上传数据。如果设置了正确的权限，用户还可以创建新文件夹。然而，使用 FTP 存在安全风险：用户名和密码在网络上以明文传输。许多 Linux 用户已转向更安全的替代方案，如 `sftp` 或 `sc`。

## FTP 客户端界面

使用文本形式的界面可以帮助你理解 FTP 会话中的每个操作。例如，当图形客户端无法自动检测所传输的文件类型时。在这种情况下，二进制文件作为 ASCII 文件传输，因此毫无用。ASCII 会在行尾打印 `^M` 控制字符。这种错误通常发生在从 Windows 操作系统向 Linux 传输文件时，因为 Windows FTP 客户端默认使用 ASCII 而非二进制。

## 使用文本 FTP 客户端界面

在典型的 FTP 会话中可以使用某些命令：

- `ascii`—为 FTP 会话设置 ASCII 文件传输类型。在发送或接收文本文件时使用此命令。
- `bin`—为 FTP 会话设置二进制文件传输。在发送或接收图形或压缩包等二进制文件之前使用。
- `close`—在 FTP 会话期间关闭与服务器的连接。使用此命令代替 `quit` 或 `bye` 返回 ftp 命令行提示符。
- `get`—启动从 FTP 服务器到用户本地机器的单个文件传输。使用此命令检索单个文件如 `get cartoon.jpg`）。
- `hash`—在文件传输期间设置哈希标记（`#`）。使用此命令获取传输进度的视觉指示。
- `mget`—启动从 FTP 服务器到用户本地机器的多个文件传输。使用此命令单次下载（接收）多个文件（如 `mget *.jpg`）。
- `mput`—启动从用户本地机器到 FTP 服务器的多个文件传输。使用此命令单次上传（发送）多个文件（如 `mput *.jpg`）。
- `open`—使用 IP 地址或主机名打开到远程服务器的连接。在 ftp 命令行提示符工作时使用此命令（如 `open ftp.redhat.com`）。
- `prompt`—在发布 `mput` 或 `get` 命令时，询问用户是否获取特定文件。如果用户启动 `mget *` 且开启了提示，FTP 客户端会提示用户传输通配符匹配的每个文件。
