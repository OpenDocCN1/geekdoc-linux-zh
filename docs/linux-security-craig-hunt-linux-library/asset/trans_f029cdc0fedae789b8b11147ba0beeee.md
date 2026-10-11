
# IP 认证头

在当前互联网模型中，采用一种存储转发架构，这意味着你的数据包在被保证穿过一系列你无法控制的中继系统时，内容可能会发生变化。为确保 IP 数据包的内容在传输过程中不被篡改，一种方法是添加一个包含原始数据包状态单向哈希值的头部。这个头部被称为认证头（AH）。如果攻击者修改了数据包，接收方会意识到这一点，因为头部中包含的哈希值与数据包结束状态不匹配。

IETF 为此 AH 创建了一个正式的协议，该协议由支持 IPsec 的发送方在数据包发送前插入到 IP 头部和 TCP 头部之间（见图 12.3）。该字段包含若干供远端处理的索引和参数，但 AH 的核心是一个使用整个 IP 数据包作为输入计算出的哈希值。虽然 IPsec 通常旨在容纳新的哈希算法，但 RFC2402 规范要求实现必须支持 MD5 和 SHA-1 算法以符合标准。

## 图 12.3 IPsec AH 数据包格式

![](img/3258bbaf790525f8c4eb25fabff7844a_363_0.png)

# IP 封装安全载荷（ESP）

虽然 AH 解决了 IP 数据包完整性和认证的问题，但它并未解决机密性问题。在许多情况下，你需要确保没有人在数据包经由不可信网络传输时非法访问你 IP 数据包的载荷。IP 封装安全载荷（ESP）规范允许安全网关在私有出站数据包经由公共互联网传输之前对其进行完全封装。这可以通过两种方式进行：ESP 传输模式和 ESP 隧道模式。

### ESP 传输模式

你可以使用 ESP 传输模式来保护在两个实施 IPsec 安全性的安全网关之间交换的 IP 数据包的载荷。当使用 ESP 传输模式时，安全网关会在原始 IP 头部和 TCP 头部之间插入一个 ESP 头部（见图 12.4）。该头部包含指向两个安全网关之间协商的安全联盟（SA）的指针，以及指向端点应预期的下一个 ESP 数据包的指针。

![](img/3258bbaf790525f8c4eb25fabff7844a_364_0.png)

在 TCP 头部和 TCP 载荷之后，安全网关插入一个 ESP 尾部，其中包含可变数量的填充字符，以确保待保护的数据包具有固定长度。

最后，安全网关附加一个由整个 ESP 数据包（减去认证值）作为输入计算出的哈希值组成的 ESP 认证值。其工作方式类似于 AH 协议，并确保数据包的完整性。

请注意，ESP 对原始 TCP 头部和载荷的内容进行加密，并确保整个 ESP 数据包的认证。

### ESP 隧道模式

请注意，ESP 传输模式保护原始数据包的 TCP 头部和 TCP 载荷，但不保护原始 IP 头部。如果需要确保整个原始 IP 数据包的机密性、完整性和认证，则应选择 ESP 隧道模式。ESP 隧道模式有效地将整个 IP 数据包封装并插入到一个全新的数据包中，该新数据包的源 IP 地址通常是执行 IPsec 封装的安全网关的外部可达地址。

图 12.5 中展示的 ESP 隧道模式数据包格式与用于 ESP 传输模式的格式类似，不同之处在于原始 IP 头部也被认证和加密。

![](img/3258bbaf790525f8c4eb25fabff7844a_365_0.png)

ESP 隧道模式的另一个优点是，来自 IPsec 保护网络的数据包不需要使用合法的互联网地址，因为当数据包在 Internet 上传输时，这些地址会被有效地“隐藏”。

虽然 ESP 规范（定义在 RFC2406 中）允许使用新的加密算法，但它还要求符合 IPsec 的实现必须支持 DES 加密算法，以及本章前面“IP 认证头”部分提到的 MD5 和 SHA-1 认证算法。由于 DES 算法的强度最近受到质疑，大多数 IPsec 软件供应商通常支持更强大的加密算法，如 3DES、IDEA 和 Blowfish。

通常情况下，Linux 开源社区挺身而出，开发了一个稳健的 IPsec 标准实现。FreeS/WAN Linux IPsec 软件包是本章下一节的讨论主题。

# FreeS/WAN

项目负责人 John Gilmore 于 1996 年启动了 FreeS/WAN 开发，旨在“保护 5% 的互联网流量免受被动窃听”。因此，Free Secure Wide Area Network（FreeS/WAN）的目标是利用标准的 IETF IPsec 协议，使每个 Linux 服务器都成为支持 VPN 的主机，以确保 IP 通信的机密性、完整性和认证。由于曾经严格的美国对加密材料出口的限制，FreeS/WAN 的早期大部分开发工作在美国境外进行。事实上，为了安全起见，FreeS/WAN 开发人员也避免了任何美国公民或居民的协助。

## 获取 FreeS/WAN

FreeS/WAN 软件在 GPL 许可协议下以源代码格式提供。虽然少数 Linux 发行版（例如 SuSE、Connectiva 和 Polished）将 FreeS/WAN 软件包作为标准安装的一部分提供，但大多数发行版都没有，尤其是基于美国的发行版。在安装 FreeS/WAN 的过程中有很多内容需要学习，因此我建议你从官方网站下载源代码发行版并自行构建。FreeS/WAN 可从 http://www.freeswan.org 获取（见图 12.6）。

![](img/3258bbaf790525f8c4eb25fabff7844a_366_0.png)

你可以通过 FreeS/WAN 网站上的链接下载发行版，或者使用以下命令直接从 FTP 站点获取：

```bash
[ramon]$ cd /usr/src
[ramon]$ sudo ftp ftp.xs4all.nl
Connected to reflectix.xs4all.nl.
220 Reflectix.xs4all.nl FTP server (Version wu-2.6.1(12) Tue Oct 10 18:09:22 CEST 2000) ready.
Name (ftp.xs4all.nl:ramon): **anonymous**
331 Guest login ok, send your complete e-mail address as password.
Password:
230-Welkom op de FTP server van XS4ALL
230------------------------------------------------
230 Guest login ok, access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> **cd** **pub/crypto/freeswan**
250 CWD command successful.

ftp> **get** **freeswan-1.8.tar.gz**
local: **freeswan-1.8.tar.gz** remote: **freeswan-1.8.tar.gz**
227 Entering Passive Mode (194,109,6,26,80,118)
150 Opening BINARY mode data connection for **freeswan-1.8.tar.gz**
(1447587 bytes).
226 Transfer complete.
1447587 bytes received in 96.2 secs (15 Kbytes/sec)
ftp> **bye**
```

下一步是解压缩并展开你刚下载的存档文件：

```bash
[ramon]$ **sudo tar -xzf freeswan-1.8.tar.gz**
[ramon]$ **cd freeswan-1.8**
```

在进行 FreeSWAN 安装之前，请确保你的系统上已安装 `gmp-devel` RPM 包。这是 GNU 高精度数学库。大多数发行版都带有 `libgmp.so` 库，但你只有头文件 `gmp.h`，而它只随 `gmp-devel` 包提供。以下命令在你的系统上安装 `gmp-devel` 包的 RPM 版本：

```bash
[ramon]$ **sudo rpm -i gmp-devel-3.0.1-5.i386.rpm**
```

现在你准备好安装 FreeSWAN 软件本身了。安装 FreeSWAN 软件的第一步是构建一个修改过的 Linux 内核。

## 安装 FreeS/WAN

FreeS/WAN 软件发行版有四个基本组成部分：

- 内核源代码补丁和添加项
- 称为 *pluto* 的 IKE 守护程序
- 一组管理该软件包的脚本
- 手册页和配置文件

首先安装内核补丁。进入 `/usr/src/freeswan` 目录并输入 *make xgo* 命令：

```bash
[ramon]$ cd /usr/src/freeswan-1.8
[ramon]$ sudo make xgo
```

要安装 FreeS/WAN 软件，你需要一个有效的源代码树，因为 *make xgo* 命令会重新构建内核。我建议你下载你发行版的内核源代码（包括头部文件）并先构建一个标准内核，然后再运行 *make xgo*。下载内核源代码和头部文件可以让你在修改内核以适合 FreeS/WAN 的需求之前熟悉内核构建过程。这可以节省你调试与内核构建相关问题所需的精力。*make xgo* 命令需要与任何内核构建过程相同的输入。对内核进行适合你的系统硬件的更改，并保存配置更改。

> **警告**：即使你没有修改任何默认内核值，也要确保保存配置更改。

当你退出 *make xgo* 命令的图形界面时，系统将开始使用新补丁重新编译内核。根据 CPU 速度、系统的 RAM 量以及磁盘驱动器的类型，这可能花费几分钟到几个小时不等。在编译结束时，你应该看到以下两行：

```bash
make[1]: Leaving directory `/usr/src/linux-2.2.16`
utils/errcheck out.kbuildd
```

如果你的结果不同，那么内核构建中很可能出现了问题。检查 *out.kbuildd* 文件以获取有关该问题的信息。如果一切正常，从同一目录使用以下命令完成内核安装过程：

```bash
[ramon]$ sudo make kinstall
```

