

如果你想尝试使用 **nmap** 来扫描你的局域网，只需输入类似于以下命令的内容（请将 IP 地址范围替换为你网络中适用的地址）：

```
nmap -O -sS 192.168.0.4-8
```

以下是该命令的典型输出列表：

```
Starting nmap 3.81 ( http://www.insecure.org/nmap/ ) at 2005-08-28 16:20 EDT
Interesting ports on 192.168.0.4:
(The 1659 ports scanned but not shown below are in state: closed)
PORT STATE SERVICE
21/tcp open ftp
22/tcp open ssh
111/tcp open rpcbind
631/tcp open ipp
MAC Address: 00:C0:49:63:78:3A (U.S. Robotics)
Device type: general purpose
Running: Linux 2.4.X|2.5.X|2.6.X
OS details: Linux 2.4.18 - 2.6.7
Uptime 9.919 days (since Thu Aug 18 18:18:15 2005)
... Lines deleted ...
Nmap finished: 1 IP addresses (5 hosts up) scanned in 30.846 seconds
```

如你所见，**nmap** 显示了开放端口的名称，并猜测了操作系统名称和版本号。

## Nessus

Nessus 安全扫描器是一款模块化的安全审计工具，它使用用 Nessus 脚本语言编写的插件来检测各种各样的网络漏洞。Nessus 采用客户端/服务器软件架构，包括一个名为 **nessusd** 的服务器和一个名为 **nessus** 的客户端。

Knoppix 系统已经自带了 Nessus，因此你不需要下载或安装任何东西。要启动 Nessus，请选择主菜单 **→** 系统 **→** 安全 **→** NESSUS 安全工具。

要安装 Nessus，请首先尝试你的 Linux 发行版通常安装新软件包的方法。在 Debian、MEPIS 和 Ubuntu 中，输入 **apt-get install nessus** 来安装包。在 SUSE 中，从 YaST 控制中心的软件类别中点击“安装和删除软件”（**→** 主菜单 **→** 系统 **→** 控制中心 (YaST)），并使用 YaST 的搜索功能找到 nessus 包。选择这些包并点击“接受”以安装它们。在 Xandros 中，选择“编辑 **→** 设置应用程序源”，并将“Debian Unsupported Site”链接作为源。然后输入 **apt-get install nessus**。

![](img/792720823146d68f19fd50c99ebfce4b_584_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_585_0.png)

对于 Fedora Core，你必须从 www.nessus.org/download/ 下载并安装 Nessus。在尝试安装 Nessus 之前，你必须安装 sharutils RPM。该包包含 Nessus 安装脚本所需的 uudecode 实用程序。sharutils 包并未随 Fedora Core 的任何标准软件包组一起安装，因此你需要自己安装它。要安装 sharutils，请挂载附带的光盘，并使用以下命令安装它：

```
cd /media/cdrom/Fedora/RPMS  
rpm -ihv sharutils*.rpm
```

要下载和安装 Nessus，请遵循以下步骤。（这些说明适用于所有 Linux 发行版。）

1.  在 www.nessus.org/download 上，选择你要下载的 Nessus 版本。对于 Linux 系统，请下载 Nessus 2.2.5 安装程序。
2.  输入以下命令来安装 Nessus。（你必须已安装开发工具，包括 The GIMP Toolkit。）
    `sh nessus-installer-2.2.5.sh`

响应安装脚本的提示以完成安装。你通常可以按 Enter 键接受默认选择。

安装完成后，请遵循以下步骤使用 Nessus。（在 Knoppix 中，选择主菜单 **→** 系统 **→** 安全 **→** NESSUS 安全工具，然后转到第 8 步）。

1.  以 root 身份登录，并输入以下命令以创建用于 Nessus 客户端和 Nessus 服务器之间安全通信的 Nessus SSL 证书：
    `nessus-mkcert`
2.  提供所需的信息以完成证书生成过程。
3.  使用以下命令创建 nessusd 账户：
    `nessus-adduser`
4.  当提示时，输入你的用户名、密码和任何规则。（如果你不知道要输入什么规则，请按 Ctrl+D。）然后按 Y 键。
5.  如果需要，你可以通过编辑配置文件 /usr/local/etc/nessus/nessusd.conf 来配置 nessusd。
6.  **使用此命令启动 Nessus 服务器：**
    `nessusd -D`
7.  **通过在终端窗口中输入以下命令运行 Nessus 客户端：**
    `nessus`
    将出现 Nessus 设置窗口。
8.  **输入 nessusd 用户名和密码，然后点击登录按钮。**
9.  **当 Nessus 显示用于建立安全连接的证书并询问你是否接受它时，点击“是”。**
    客户端连接到服务器后，登录按钮变为注销，其左侧出现已连接标签。
    nessusd 提供选项以启用可以扫描特定漏洞的插件，但其中一些插件可能会使主机崩溃并在扫描过程中中断你的网络。如果你想尝试任何插件，请选择并启用它们。如果你想确保安全，请点击“启用所有但危险插件”链接。
10. **点击目标选择选项卡并输入一个 IP 地址范围，以扫描网络中的所有主机。**
    例如，要扫描私有网络 192.168.0.0 中的前八台主机，我将地址输入为
    `192.168.0.0/29`
    不要使用 Nessus 扫描任何你不拥有的网络。扫描其他网络通常违反法律，如果你违反了相关法律，可能会面临严重的后果。
11. **点击开始扫描。**
    Nessus 开始扫描 IP 地址并检查许多不同的漏洞。进度条显示扫描状态。
    在 Nessus 完成主机的漏洞扫描后，它会以图形和文本格式的精美组合显示结果。报告是交互式的——你可以选择一个主机地址来查看该主机的报告，你可以深入特定的漏洞以查找详细信息，例如标识该漏洞的 CVE 编号以及对该漏洞的描述。

# 第七卷

# 互联网服务器

# 第四浪 作者：Rich Tennant

![](img/792720823146d68f19fd50c99ebfce4b_588_0.png)

“我马上就来。让我先处理一下这个用户。他的 3 小时下载才完成了一半。”

# 内容概览

- 第 1 章：管理互联网服务器....565
- 第 2 章：运行 Web 服务器 .......583
- 第 3 章：设置 FTP 服务器 ............607
- 第 4 章：管理邮件和新闻服务器 ....613
- 第 5 章：管理 DNS ...............639
- 第 6 章：使用 Samba 和 DNS..............661

# 第 1 章：管理互联网服务

## 本章内容

- 了解互联网服务
- 通过 inetd 或 xinetd 控制服务器
- 使用 chkconfig 或 update-rc.d 管理服务器
- 使用图形实用工具配置服务以便在启动时运行

互联网是一个客户端和服务器的世界。客户端向服务器发起请求，服务器对请求作出响应。例如，你的 Web 浏览器是一个客户端，它从 Web 服务器下载信息并显示给你。当然，客户端和服务器是在各种各样的计算机上运行的计算机程序。Linux 系统是运行各种各样服务器的理想系统——从 Web 服务器到 Windows 文件和打印服务器。在本章中，我将典型互联网服务、其客户端/服务器架构以及在 Linux 中如何管理服务器进行概述。你可以使用本章中的信息来管理在你的 Linux 系统上运行的任何服务器。

## 理解互联网服务

互联网服务是旨在将一个系统的信息传递到另一个系统的网络应用程序。按设计，每个互联网服务都分为两部分实现——一个提供信息的服务器和一个或多个请求信息的客户端。

这种客户端/服务器架构是构建分布式信息系统最常见的方式。客户端和服务器是在这些计算机上运行并通过网络通信的计算机程序。其巧妙之处在于，你可以在桌面计算机上运行客户端，并访问世界上任何地方（只要它连接到互联网）计算机上运行的服务器上的信息。

