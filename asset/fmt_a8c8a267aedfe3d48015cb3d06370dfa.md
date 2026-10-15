
此命令列出本地系统上打印机队列的所有状态信息。

## 使用通用 UNIX 打印系统图形界面

您可以通过启动浏览器（例如 Firefox）并浏览到 `http://localhost:631` 来使用 CUPS 创建打印机队列、获取打印服务器信息和管理队列。CUPS 提供了一个基于 Web 的管理界面，如图 23.11 所示。

如果您单击浏览器页面中的“执行管理任务”项，系统会要求您输入 root 密码，如图 23.12 所示。

![](img/2045828cf45e5632bf056f9ca99d6755_652_0.png)

**图 23.11** 使用基于 Web 的 CUPS 管理界面来配置和管理打印。

![](img/2045828cf45e5632bf056f9ca99d6755_652_1.png)

**图 23.12** 输入 root 密码以使用 CUPS 执行打印机管理。

## 创建 CUPS 打印机条目

本节提供了一个使用 CUPS 基于 Web 的界面创建 Linux 打印机条目的简短示例：使用 CUPS Web 界面创建打印机和设备队列类型（如本地、远程、串行端口或 Internet）；然后您输入设备统一资源标识符（URI），例如 `lpd://192.168.2.35:11lp`，它代表远程 UNIX 打印服务器的 IP 地址以及服务器上的远程打印队列名称。您还需要指定打印机型号或制造商及其驱动程序。一个“打印机”页面链接允许您打印测试页、停止打印服务、管理本地打印队列、修改打印机条目或添加另一台打印机。

在管理页面中，单击“添加打印机”按钮，然后在“名称”字段中输入打印机名称（如 lp），在“位置”字段中输入打印机的物理位置，在“描述”字段中输入关于打印机的简短说明（如其类型）。图 23.13 显示了 HP 2100 LaserJet 的一个示例条目。

![](img/2045828cf45e5632bf056f9ca99d6755_653_0.png)

图 23.13 使用 CUPS 创建新的打印机队列。

单击“继续”按钮。然后，您可以选择打印机访问类型（本地、远程、串行端口或 Internet），如设备页面中所示，见图 23.14。例如，要配置向本地打印机打印，请选择 Parallel Port #1，或者对于远程打印机，选择 LPD/LPR Host 或 Printer 条目。

![](img/2045828cf45e5632bf056f9ca99d6755_654_0.png)

**图 23.14** 在 CUPS 管理页面中选择打印机设备。

再次单击“继续”，并根据图 23.15 所示对话框中的要求选择打印机制造商。

![](img/2045828cf45e5632bf056f9ca99d6755_655_0.png)

图 23.15 创建新队列时选择打印机制造商。

在您单击 *Continue* 后，然后选择驱动程序。创建打印机后，您可以使用 *Printer* 页面（如图 23.16 所示）来打印测试页、停止打印服务、管理本地打印队列、修改打印机条目或添加另一台打印机。CUPS 提供了许多附加功能，在安装、配置并运行后，为 Fedora 提供透明的传统 UNIX 打印支持。

> **注意**
>
> 要了解有关 CUPS 的更多信息并获得系统的基本概述，请浏览到 `http://www.cups.org/`。

![](img/2045828cf45e5632bf056f9ca99d6755_656_0.png)

图 23.16 使用 CUPS 打印机页面轻松管理打印机。

## 避免打印机支持问题

排除打印机故障可能会令人沮丧，特别是当您发现您的新打印机在 Linux 上无法正常工作的时候。首先，请记住如今市场上几乎所有的打印机都支持 Linux。然而，某些供应商在支持 Linux 方面的成功率更高。如果您想查看记分牌，请浏览到 `http://www.linuxprinting.org/vendors.html`。

### 多功能（打印/传真/扫描）设备

存在问题的打印机，或者可能与 Fedora 兼容也可能不兼容的打印设备，包括结合扫描、传真和打印服务的多功能（或 *一体机*）打印机。您应该研究任何计划中的购买，并避免任何不愿意通过驱动程序或开发信息支持 Linux 的供应商。

在 Linux 对多功能打印机的支持领域中，一颗耀眼的明星是 HP 在 `http://hpoj.sourceforge.net/` 支持的 HP OfficeJet Linux 驱动程序项目。许多型号支持打印和扫描，传真支持正在开发中。

### 使用 USB 和传统打印机

其他问题可能源于缺少打印机的 USB 供应商和设备 ID 信息——这是 Linux 下某些 USB 扫描仪共有的问题。有关 USB 打印机支持的信息，您可以咨询 Linux 打印领域的人（在该部分开头的 URL 处）或 Linux USB 项目（`http://www.linux-usb.org/`）。

尽管许多较新的打印机需要通用串行总线（USB）端口，但对于传统并行端口（IEEE-1284）打印机，Linux 仍然提供出色的支持，使站点能够继续使用较旧的硬件。您可以利用 Linux 的变通方法来设置打印，即使主机计算机没有传统的并行打印机端口，或者您想在较旧的计算机上使用较新的 USB 打印机。

例如，要在仅支持 USB 的计算机上托管基于并行端口的打印机，请使用廉价的 USB 转并行转换器将打印机连接到计算机。USB 转并行转换器通常提供 Centronics 连接器：该连接器的一端插入较旧的打印机，而另一端插入 USB 连接器。然后，将 USB 连接器插入您的集线器、桌面或笔记本的 USB 端口。另一方面，如果传统计算机没有内置 USB 端口，您可以使用附加 PCI 卡来添加打印（及其他设备）的 USB 支持。大多数 PCI USB 接口卡至少添加两个端口，并且设备可以通过集线器链式连接。

### 相关的 Fedora 和 Linux 命令

以下命令可帮助您管理打印服务：

- `accept`—通过命令行控制对 CUPS 服务器打印作业的访问
- `cancel`—从命令行取消打印作业
- `disable`—从命令行控制打印
- `enable`—控制 CUPS 打印机
- `lp`—将指定文件发送到打印机并允许控制打印服务
- `lpc`—在控制台上显示打印机和打印服务的状态
- `lpq`—在控制台上查看打印队列（待打印作业）
- `lprm`—通过命令行从打印队列中移除打印作业
- `lptest`—显示打印机和服务器状态
- `system-config-printer`—显示 Fedora 的图形打印机配置工具
- `system-config-printer-tui`—显示 Fedora 的文本对话框打印机配置工具

## 参考链接

`http://www.linuxprinting.org/`—在此处浏览特定驱动程序以及关于 USB 和其他类型打印机的信息。

`http://www.hp.com/wwsolutions/linux/products/printing_imaging/index.html`—来自惠普（HP）的简短但权威的信息，介绍在 Linux 系统下打印产品的支持情况。

`http://www.linuxdoc.org/HOWTO/Printing-HOWTO/`—Grant Taylor 的《打印 HOWTO》，其中包含在 Linux 下使用各种打印服务的信息。

`http://www.cups.org/`—CUPS 软件的综合资料库，包括适用于红帽 Linux 的版本。

`http://www.pwg.org/ipp/`—互联网打印协议（Internet Printing Protocol）标准的首页。

`http://www.linuxprinting.org/cups-doc.html`—关于 CUPS 的信息。

`http://www.cs.wisc.edu/~ghost/`—Ghostscript 解释器的首页。

`http://www.samba.org/`—获取有关 Samba 更多信息以及使用 SMB 协议配合 Linux、UNIX、Mac OS 和其他操作系统的基础入口点。

此外，一本关于 Samba 的优秀书籍有助于你深入了解，即《Samba Unleashed》（Sams Publishing 出版社，ISBN: 0-672-31862-8）。

# 第 24 章

## 通过 FTP 进行远程文件服务

*文件传输协议（FTP）* 曾经被视为通过网络在计算机之间传输文件的主要方法。尽管如今许多图形化 FTP 客户端补充了原始基于文本界面的命令，但 FTP 至今仍被广泛使用。随着计算机的演变，FTP 也在不断发展，Fedora 提供了许多通过图形界面使用 FTP 传输文件的方式。

本章概述了 Fedora 包含的可用 FTP 软件，并详细介绍了初始设置、配置以及使用特定于 FTP 的客户端的一些细节。Fedora 还包含一个名为 `vsftpd`（非常安全的 FTP 守护进程）的 FTP 服务器软件包，以及您可以用于通过 FTP 协议提供和传输文件的若干相关程序。

### 本章内容

- 使用 FTP 客户端
- FTP 服务器
- 安装 FTP 软件
- FTP 用户
- `wu-ftpd` 的 `xinetd` 配置
- 配置非常安全的 FTP 服务器
- 配置 `wu-ftpd` 服务器
- 使用 `ftppasswd` 文件中的命令来配置 `wu-ftpd`
- 配置 FTP 服务器文件转换操作
- 使用 `ftphosts` 文件中的命令允许或拒绝 FTP 服务器连接
- 服务器管理
- 参考链接

### 使用 FTP 客户端

FTP 协议允许用户连接到服务器，读取目录和文件名，以及下载和上传数据。如果设置了正确的访问权限，用户还可以创建新文件夹并设置其访问权限。

然而，使用 FTP 会带来安全风险：用户名和密码在局域网（LAN）或互联网上传输时未加密。为了防止用户向任何窃听者泄露其身份验证详情，许多站点仅启用匿名 FTP 登录和文件检索。许多 Linux 用户已转向更安全的替代方案，例如 OpenSSH 套件中包含的 `ssh` 和 `sftp` 或 `scp`。以下部分讨论了较新的和传统的不同类型的 FTP 接口及其用法。由于它们是更大的 OpenSSH 集合的一部分：`ssh` 和 `scp` 命令在第 19 章“通过 SSH 和 Telnet 进行远程访问”中介绍。

#### FTP 客户端界面

使用基于文本的 FTP 界面有助于你了解图形化 FTP 会话中每个操作的作用。这种理解在例如图形化客户端未能自动检测正在传输的文件类型时非常有用。在这种情况下，二进制文件作为 ASCII 文件传输，因此毫无用处。相反，作为二进制传输的 ASCII 文件会在每行末尾打印“#”控制字符。这种错误通常发生在将文件从旧版 Microsoft Windows 操作系统传输到 Linux 时，因为 Windows FTP 客户端默认使用 ASCII 而非二进制传输。

#### 使用基于文本的 FTP 客户端界面

典型的 FTP 会话中可以使用以下一些常用命令：

- `ascii`—为 FTP 会话设置 ASCII 文件传输类型。在传输文本文件之前使用此命令。
- `bin`—为 FTP 会话设置二进制文件类型传输。在传输二进制文件（如图形图像或压缩归档）之前使用此命令。
- `close`—在 FTP 会话期间关闭与远程服务器的连接。使用此命令代替 `quit` 或 `bye` 返回到 `ftp` 命令提示符。
- `get`—启动从 FTP 服务器到用户本地机器的单个文件传输。使用此命令获取单个文件（例如 `get cartoon.jpg`）。
- `hash`—设置在文件传输期间使用井号（#）。使用此命令以直观了解传输进度。
- `mget`—启动从 FTP 服务器到用户本地机的多个文件传输。使用此命令通过单个命令下载（接收）多个文件（例如 `mget *.jpg`）。
- `mput`—启动从用户本地机器到 FTP 服务器的多个文件传输。使用此命令通过单个命令上传（发送）多个文件（例如 `mput *.jpg`）。
- `open`—使用 IP 地址或主机名打开到远程服务器的连接。在 `ftp` 命令提示符下工作时使用此命令（例如 `open ftp.redhat.com`）。
- `prompt`—是一个交互式命令，当发出 `mput` 或 `mget` 命令时，询问用户是否获取特定文件。如果用户发起 `mget *` 且提示处于开启状态，FTP 客户端将提示用户传输 * 通配符匹配的每个文件。当目录中需要传输几个文件，但其中一两个文件不受想要时，这特别有用。默认情况下，提示是开启的。
- `put`—启动从用户本地机器到 FTP 服务器的单个文件传输。使用此命令上传（发送）单个文件（例如 `put inventory.doc`）。
- `quit`—使用此命令关闭 FTP 连接并退出 `ftp` 命令。

这只是 FTP 会话期间可用的部分命令。通过输入 `help`，用户可以查看所有有效命令的完整列表。输入 `help command-name` 会显示该命令功能的简要描述。列表 24.1 显示了帮助输出。

**列表 24.1 FTP 会话中由 help 列出的命令**

命令可以缩写。命令如下：

| ! | cr | mkdir | proxy | send |
| :--- | :--- | :--- | :--- | :--- |
| $ | delete | mget | sendport | site |
| account | debug | mkdir | put | size |
| append | dir | mls | pwd | status |
| ascii | disconnect | mode | quit | struct |
| bell | form | modtime | quote | system |
| binary | get | mput | recv | sunique |
| bye | glob | newer | reget | tenex |
| case | hash | nmap | rstatus | trace |
| ccc | help | ntrans | rhelp | type |
| cd | idle | nlist | rename | user |
| cdup | image | open | reset | umask |
| chmod | lcd | passive | restart | verbose |
| clear | ls | private | rmdir | ? |
| close | macdef | prompt | runique | |
| cprotect | mdelete | protect | safe | |

#### 使用 ftp 命令的典型 FTP 会话

连接到远程 FTP 服务器可能需要用户名和密码，但许多服务器也提供匿名访问。配置正确的远程 FTP 服务器会快速响应 FTP 请求，并显示共享目录和文件。本节展示了一个与许多互联网站点上常见的典型服务器（在本例中，运行 `wu-ftpd` 服务器）的示例 FTP 会话。

你可以通过使用 `ftp` 命令加上远程计算机的 IP 地址或主机名来连接到远程 FTP 服务器，例如：
