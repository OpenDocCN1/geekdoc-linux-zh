
# Nikto

Nikto 是一个 Web 服务器扫描器，用于在 200 多台服务器上查找 2000 个潜在的危险文件/CGI 和问题。它使用了 `LibWhisker`，但更新频率比 Whisker 本身频繁。

## 分类：加密

### SSH

- **Rank**: 12
- **URL**: `www.openssl.com/`
- **Mac availability**: native, DP 3.8.1p1, Fink 4.0p1
- **Description**: 访问远程计算机的安全方法。

SSH 是一个用于在远程机器上登录或执行命令的程序。它在不安全的网络上为两个不受信任的主机之间提供安全的加密通信。X11 连接和任意传输控制协议/互联网协议 (TCP/IP) 端口也可以通过安全通道进行转发。它旨在替代 `rlogin`、`rsh` 和 `rcp`，并可用于为 `rdist` 和 `rsync` 提供安全的通信通道。OpenSSH 隶属于 OpenBSD 项目，尽管其便携版本运行在大多数 UNIX 系统上。

### GnuPG

- **Rank**: 30
- **URL**: `www.gnupg.org/`
- **Mac availability**: DP 1.4.0, Fink 1.4.0
- **Description**: 使用高级加密保护您的文件和通信。

PGP 是由 Phil Zimmermann 的著名加密程序，可帮助您的数据免受窃听者和其他风险。GnuPG 是备受推的 PGP 标准开源实现（实际的可执行文件名为 `gpg`）。虽然 GnuPG 总是免费的，但 PGP 在某些用途下需要付费。

### OpenSSL

- **Rank**: 38
- **URL**: `www.openssl.org`
- **Mac availability**: DP 0.9.7e, Fink 0.9.6m
- **Description**: 领先的 SSL/TLS 加密库。

OpenSSL 项目是一个协作项目，旨在开发一个健壮、商业级、功能全的开源工具包，实现 SSL v2/v3 和传输层安全协议 (TLS v1) ，以及一个全强度的通用加密库。该项目由全球志愿者社区管理，他们利用互联网进行通信、规划和开发 OpenSSL 工具包及其相关文档。

### stunnel

- **Rank**: 46
- **URL**: `www.stunnel.org/`
- **Mac availability**: DP 4.0.5, Fink 4.10
- **Description**: 通用的 SSL 加密封装器。

stunnel 程序设计用于在远程客户端与本地 (inetd 可启动) 或远程服务器之间作为 SSL 加密封装器。它可以通过如邮局协议 v2 (POP)、邮局协议 v3 (POP3) 和互联网消息访问协议 (IMAP) 服务器等 inetd 守护进程在不更改程序代码的情况下添加 SSL 功能。它将使用 OpenSSL 或 SSLay 库协商 SSL 连接。

## 分类：防御

### Snort

- **Rank**: 3
- **URL**: `www.snort.org`
- **Mac availability**: DP 2.2.0, Fink 2.3.3
- **Description**: 面大众的免费入侵检测系统 (IDS)。

Snort 是一个轻量级网络 IDS，能够在 IP 网络上执行实时流量分析和数据包记录。它可以执行协议分析、内容搜索/匹配，并用于检测各种攻击和探测，例如缓冲区溢出、隐藏端口扫描、CGI 攻击、SMB 探测、操作系统指纹识别等。Snort 使用灵活的基于规则的语言来描述它应该收集或通过的流量，并配备了模块化检测引擎。许多人还建议将入侵数据库分析控制台 (ACID) 与 Snort 使用。

### Honeyd

- **Rank**: 43
- **URL**: `www.citi.umich.edu/u/provos/honeyd/`
- **Mac availability**: DP 0.4
- **Description**: 自己的个人蜜罐网。

Honeyd 是一个在网络上创建虚拟主机的小型守护进程。这些主机可以配置为运行任意服务，它们的 TCP 特性可以调整，使其看起来在运行某些版本的操作系统。Honeyd 允许单个主机在局域网上声称多个地址以进行网络模拟。可以对虚拟机进行 ping，或对其进行路由追踪 (traceroute)。可以根据简单的配置文件模拟虚拟机上的任何类型的服务。也可以将服务代理到另一台机器而不是模拟它们。由于法律原因，该网页已关闭，但 0.5 版本的 tar 包仍可在 `www.citi.umich.edu/u/provos/honeyd/honeyd-0.5.tar.gz` 获取。

### TCPwrappers

- **Rank**: 52
- **URL**: `ftp://ftp.porcupine.org/pub/security/index.html`
- **Mac availability**: DP 7.6
- **Description**: 一经典的基于 IP 的访问控制和日志记录机制。

### Bastille

- **Rank**: 57
- **URL**: `www.bastille-linux.org/`
- **Mac availability**: Native
- **Description**: 用于 Linux、Mac OS X 和 HP-UX 的加固脚本。

## 分类：防御/取证

### lsof

- **Rank**: 41
- **URL**: `ftp://ftp.porcupine.org/pub/security/index.html`
- **Mac availability**: DP 4.7
- **Description**: 列出打开文件的 Unix 特有诊断工具。

## 分类：逃逸

### Fragroute

- **Rank**: 48
- **URL**: `www.insecure.org/fragroute/`
- **Mac availability**: DP 1.2
- **Description**: 用于确定远程主机操作系统的工具。

### std

- **Rank**: 22
- **URL**: N/A
- **Mac availability**: Native
- **Description**: 获取路由追踪数据并绘制在地图上。

### XProbe2

- **Rank**: 33
- **URL**: `www.insecure.com/Xprobe/`
- **Mac availability**: DP 0.3
- **Description**: 主动指纹识别工具。

### dig

- **Rank**: 65
- **URL**: `www.isc.org/products/BIND/`
- **Mac availability**: Native
- **Description**: 随 Bind 提供的便捷域名系统 (DNS) 查询工具。

## 分类：足迹

### visualroute

- **Rank**: 69
- **URL**: `www.visualroute.com/index.html`
- **Mac availability**: Native
- **Description**: 获取路由追踪数据并绘制在地图上。

## 分类：监控（嗅探）

### Ethereal

- **Rank**: 2
- **URL**: `www.ethereal.com`
- **Mac availability**: DP 0.10.8, Fink 0.10.12
- **Description**: 嗅探连接互联网的胶水。

### TCPdump

- **Rank**: 5
- **URL**: `www.tcpdump.org`
- **Mac availability**: Native
- **Description**: 用于网络监控和数据采集的经典嗅探器。

### Kismet

- **Rank**: 17
- **URL**: `www.kismetwireless.net/`
- **Mac 可用性**: Fink 3.0.1
- **描述**: 强大的无线嗅探器。

Kismet 是一款 802.11b 网络嗅探器和网络分析器。它能够使用无线网卡进行嗅探，通过用户数据报协议 (UDP)、地址解析协议 (ARP) 和动态主机配置协议 (DHCP) 包自动检测网络 IP 块，通过 Cisco 发现协议列出 Cisco 设备，弱加密数据包日志以及与 Ethereal-TCP 兼容的数据包转储文件。它还具备在下载的地图或提供的图像文件上绘制检测到的网络和估计网络范围的能力。

### ngrep

- **排名**: 35
- **URL**: `www.packetfactory.net/projects/ngrep/`
- **Mac 可用性**: DP 1.4.2, Fink 1.4.0
- **描述**: 方便的数据包匹配与显示。

ngrep 旨在旨在提供 grep 的大部分常用功能，并将其应用于网络层。grep 是一个感知 pcap 的工具，允许你指定扩展的正则表达式或十六进制表达式来匹配数据包的负载。它识别跨以太网、点对点协议 (PPP)、串口链路互联网协议 (SLIP)、光纤分布式数据接口 (FDDI)、环形网络和空接口的 TCP、UDP 和 ICMP，并以与 TCPdump 和 snoop 等更常见的数据包嗅探工具相同的方式理解 bpf 过滤器逻辑。

### ntop

- **排名**: 39
- **URL**: `www.ntop.org/`
- **Mac 可用性**: DP 3.0, Fink 1.1
- **描述**: 网络流量使用监控。

ntop 显示网络使用情况与 top 显示进程的方式类似。在交互模式下，它在用户的终端上显示网络状态。在 Web 模式下，它作为一个 Web 服务器运行，创建网络状态的 HTML 导出。它配备了 NetFlow/sFlow 发送/收集器、一个用于创建以 ntop 为中心的监控应用的 HTTP 客户端接口以及用于持久存储流量统计数据的 RRD。

### etherape

- **排名**: 64
- **URL**: `http://etherape.sourceforge.net/`
- **Mac 可用性**: Darwin 0.9.0
- **描述**: 一个以以太网为模型的 UNIX 图形网络监控器。

### arpwatch

- **排名**: 75
- **URL**: `www-nrg.ee.lbl.gov/`
- **Mac 可用性**: DP 2.1a11, Fink 2.1a11
- **描述**: 跟踪以太网/IP 地址对，并可以检测某些异常活动（如使用 dsniff）。

### tcppreplay

- **排名**: 71
- **URL**: `http://tcppreplay.sourceforge.net/`
- **Mac 可用性**: Fink 2.3.5
- **描述**: 以任意速度重放保存的 tcpdump 或 snoop 工具。

## 分类：多用途

### netcat

- **排名**: 4
- **URL**: `http://www.atstake.com/research/tools/network_utilities/`
- **Mac 可用性**: 原生 (Native)
- **描述**: 网络瑞士军刀。

这是一个简单的 UNIX 工具，通过 TCP 或 UDP 跨网络连接读取和写入数据。它被设计成一个可靠的后端工具，可以直接使用，也可以轻松地被其他程序和脚本驱动。同时，它还是一个功能丰富的网络调试和探索工具，因为它可以创建你需要的几乎任何类型的连接，并具有许多有趣的内置功能。

## 分类：密码破解

### john

- **排名**: 11
- **URL**: `http://www.openwall.com/john/`
- **Mac 可用性**: DP 1.6
- **描述**: 一个极其强大、灵活且快速的多平台密码哈希破解器。

John the Ripper 是一款快速的密码破解器，目前支持多种变体 UNIX（官方支持 11 种，不包括不同架构）、DOS、Win32、BeOS 和 OpenVM。它的主要目的是检测 UNIX 密码。它支持在各种 UNIX 变体中常见的各种 crypt(3) 密码哈希，以及 Kerberos AFS 和 Windows NT/2000/XP LM 哈希。其他两类哈希类型可以通过社区贡献的补丁进行添加。

### L0phtCrack

- **排名**: 19
- **URL**: `http://www.atstake.com/research/lc/`
- **Mac 可用性**: DP (l0phtcrack) 1.5
- **描述**: Windows 密码审计与恢复应用。L0phtCrack 尝试从独立的 Windows NT/2000 工作站、网络服务器、主域控制器或 Active Directory 获取的哈希（在获得适当权限的情况下）破解 Windows 密码。在某些情况下，它可以从线路上嗅探哈希。它有许多生成密码猜测的方法（字典攻击、暴力破解等）。L0phtCrack 目前每台机器花费 350 美元，且不提供源代码。预算紧张的公司可能会查看 John the Ripper、Cain & Abel 和 pwdump3。

### Crack

- **排名**: 66
- **URL**: `http://www.users.dircon.co.uk/~crypto/`
- **Mac 可用性**: DP (cracklib) 2.7
- **描述**: Alec Muffett 的经典本地密码破解器。

## 分类：密码破解（远程）

### hydra

- **排名**: 50
- **URL**: `http://www.thc.org/releases.php`
- **Mac 可用性**: DP 4.4
- **描述**: 并行网络身份验证破解器。

该工具允许对网络登录系统进行快速字典攻击，包括文件传输协议 (FTP)、POP3、IMAP、Netbios、Telnet、HTTP 认证、轻量级目录访问协议 (LDAP)、网络新闻传输协议 (NNTP)、VNC、ICQ、Socks5、PCNFS 等。它包含 SSL 支持，并且显然现在是 Nessus 的一部分。与 Amap 一样，此版本来自 THC (`www.thc.org`) 的优秀团队。

## 分类：编程

### Perl, Python

- **排名**: 36
- **URL**: `www.perl.org`
- **Mac 可用性**: 原生 (PERL)
- **描述**: 可移植通用脚本语言。

虽然此页面有很多安全工具，但当需要更常见的功能时，编写自己的（或修改现有）的能力很重要。Perl 和 Python 让这一切变得简单。

### libnet

- **排名**: 5
- **URL**: `www.packetfactory.net/libnet/`
- **Mac 可用性**: DP 1.0, Fink 1.1
- **描述**: 一种高级应用程序接口 (API)，允许程序员构造和注入数据包。

## 分类：扫描

### hping2

- **排名**: 6
- **URL**: `www.hping.org/`
- **Mac 可用性**: DP hping3, Fink 3
- **描述**: 类似于增强版 ping 的网络工具。

hping 组装并发送自定义的 ICMP、UDP、TCP 数据包并显示响应。它的灵感来自 ping 命令，但对探测提供了更多的控制。

### fping

- **排名**: 56
- **URL**: `www.fping.com/`
- **Mac 可用性**: DP 2.4, Fink 2.4
- **描述**: 一个并行 ping 程序。

### tcptoute

- **排名**: 59
- **URL**: `http://michael.toren.net/code/tcptoute/`
- **Mac 可用性**: DP 1.5, Fink 1.5
- **描述**: 使用 TCP 的 traceroute 实现。

# 第 5 章 • 渗透测试者的 Mac OS

## 安装与使用“大工具”

安全领域只有少数“大工具”，我们将安装其中两个：Ethereal 网络分析器和 Nessus 安全扫描器。本章的大部分内容一直致力于开发工具、包管理实用和 shell 以及各种与安全没有太关系的东西。然而，现在这些机制已经就绪，你就可以毫不费力地享受劳动成果，安装这些工具了。让我们先处理 Ethereal。

### Wireshark

Wireshark (`www.wireshark.org`) 是一款强大的网络分析器（具有非常漂亮的图形界面），它已成为任何网络安全人员的标准工具。事实上，Wireshark 变得如此流行，经常可以看到其文本版本的孪胞 tethereal 代替了 tcpdump 和 snoop 等老工具。

### 从源码在 MacOS X 上安装

在 MacOS X 上从源码编译 Wireshark 是一个漫且有时复杂的过程。然而，许多人倾向于这种方法，因为他们对包拥有控制权。我们在 MacOS X Tiger 上通过源码方法安装了 Wireshark。如果你有时间并且心勃勃，可以尝试这种安装方法；否则，请使用移植方法，如 DarwinPorts 或 Fink。如果你下载了新版本的软件，请确保在执行步骤时相应更改名称。

1. 通过安装 MacOS X CD 上的 Xcode Tools 来准备你的 Mac。这安装了编译源码所需的 gcc 编译器和其他开发工具，例如 X11 环境。如果你是运行 Tiger 系统时，在 MacOS X 安装盘 1 上找到 Xcode Tools 文件夹。双击该文件夹中的 `XcodeTools.pkg`，并按照屏幕上的指令安装 Xcode Tools。
2. 安装 X11 用户环境，它也位于你的 MacOS X 安装盘 1 上。该包位于 `System | Installation | Packages | X11User.pkg`；双击 `X11User.pkg` 并按照屏幕上的指令操作。这将 X11 应用程序安装到 `Utilities` 文件夹中。
3. 下载以下包并将它们保存到你的用户文件夹中，通常为 `/Users/username`：
   - Pkg-config `pkgconfig.freedesktop.org`
   - Gettext `www.gnu.org/software/gettext`
   - Glib `www.gtk.org/download`
   - ATK `ftp.gtk.org/pub/gtk/v2.10/dependencies`
   - Libpng `libpng.sourceforge.org`
   - Libxml `ftp://xmlsoft.org/libxml2`
   - Freetype `freetype.sourceforge.org`
   - Fontconfig `fontconfig.org`
   - Cairo `ftp.gtk.org/pub/gtk/v2.10/dependencies`
   - Pango `www.gtk.org/download`
   - Jpgsrc `ftp.gtk.org/pub/gtk/v2.10/dependencies`
   - TIFF `ftp.gtk.org/pub/gtk/v2.10/dependencies`
