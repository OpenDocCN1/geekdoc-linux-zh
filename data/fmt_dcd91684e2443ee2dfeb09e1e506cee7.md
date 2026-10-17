
### 3. 设置 `System V` 打印信息树

`System V` 打印信息存储在子树下，该子树又存储在目录上的默认 `LDAP` 信息树 (`cn=aidata`) 下。建议将打印信息存储在目录的默认位置。如需详细的设置和示例，请参考 `LDAP` 文档。

### 4. 配置在 `AIX` 上使用 `IBM Directory` 服务器进行 `System V` 打印的客户端

你应该配置在 `AIX` 上使用 `IBM Directory` 服务器进行 `System V` 打印的客户端：

a. 在作为客户端的系统上安装 `IBM Directory` 客户端软件。

b. 你可以使用以下语法的 `mkprldap` 命令：

```bash
mkprldap -c -h DirectoryServerHostname -w ACLBindPasswd [ -d PrintBindDN ] [-U]
```

- `-c` 选项指定客户端操作。

此命令创建、建立或修改客户端文件 `/etc/ldapsvc/server.print` 和 `/etc/ldapsvc/system.print`。

这可以在服务器和客户端上设置 `System V` 打印服务，从 `IBM Directory` (`LDAP`) 读取打印信息。

将打印机信息存储在 `OpenLDAP` 服务器上，并使用 `Perl` 等编程语言访问信息，以在打印机客户端上生成 `printcap` 或打印机配置文件。有一本由 `Rademacher` 等人编写《`Network Printing`》的书，可以在 [`Network Printing by Rademacher, et al.`] 中找到，它也是打印方面的极佳参考。

288

# 用于 `eServer pSeries` 和 `RS/6000` 的 `Linux`

过去几年，基于 `UNIX` 的系统 和 `Linux` 的活跃使得 `Linux` 成为了主流 `UNIX` 世界。本章将讨论 `Linux` 与 `UNIX` 的交汇点（特别是 `AIX`），以及如何兼得两者。

本章将简要介绍以下主题：

- 逻辑分区 (`LPAR`) `Linux`
- `AIX` 工具箱

本章将涵盖 `LPAR Linux` 和 `AIX` 工具箱的安装和实现。要获取更多信息，每个章节都会提供相关链接。

此外，关于 `pSeries Linux` 的信息可以在此处找到：`http://www.ibm.com/servers/eserver/pseries/linux/`

289

## 12.1 逻辑分区 (`LPAR`)

逻辑分区最初支持 `IBM zSeries` 和 `iSeries` 系统，允许将单个服务器划分为多个独立的“虚拟”服务器或分区。2001 年，`IBM` 发布了第一台具有 `LPAR` 能力的基于 `POWER4` 的 `IBM pSeries` 服务器。

`IBM pSeries 690` 引入了多项先进技术。其逻辑分区功能为分区选择资源提供了真正的灵活性，而其动态逻辑分区（`AIX 5L 5.2` 中的 `DLPAR`）允许在不中断的情况下在逻辑分区之间移动资源。每个逻辑分区与其他分区内的操作都是独立的，并且可以运行相同版本或不同的操作系统（`AIX 5L` 或 `Linux`）。

如图 12-1 所示，`LPAR` 技术最用于需要服务器合并的环境。服务器合并允许将不同的物理服务器将其工作负载合并到单一系统中。

![](img/550f8fc128bac37c2a15bd674b67bcf1_289_0.png)

图 12-1 服务器合并

`AIX` 和 `Linux` 可以在启用 `LPAR` 的系统的不同分区中并发运行。这允许不同的物理服务器将其工作负载合并到单一系统中。

使用 `LPAR` 进行服务器合并的益处如下：

- **降低成本**

通过服务器合并，你可以降低总拥有成本（`TCO`）并降低计算成本。这种配置非常适用于中等规模基础设施的合并。由于其分区具有高度灵活性（最低仅需 1 个处理器和 1 GB 内存），它也适用于小规模的服务器合并。因此，资源的使用更加高效。

它不仅降低了服务器本身的成本，还降低了电力、冷却、空间空间和软件许可的成本。

- **系统减少意味着管理需求减少**

将多个服务器的功能移动到一个物理系统中，将产生一个更经济、更容易操作且管理更不复杂的系统。实际上，你需要的地面空间更少，管理的服务器更少，管理系统所需的技能也更少。

- **更好的工作负载管理灵活性**

在使用多分区服务器时，跟踪系统资源是一项至关重要的任务。`p690` 包含了 `pSeries` 硬件管理控制台（`HMC`），如第 274 页图 12-2 所示。`HMC` 是逻辑分区系统管理的中心。它执行多项功能，包括创建和维护分区、共享资源以及对分区和受管系统进行电源控制，并为分区内的工作提供虚拟终端。它还负责监控和存储硬件更改，同时作为 `p690` 系统管理的焦点。

![](img/550f8fc128bac37c2a15bd674b67bcf1_291_0.png)

图 12-2 通过 `HMC` 进行工作负载管理

### 何时在 `LPAR` 上使用 `Linux`

参考第 275 页的图 12-3，一个典型的 `Web` 托管环境的服务商可能有几个前端服务器来处理代理、`DNS` 和防火墙。他们可能还有作为 `Web` 应用服务器的小型系统，以及作为数据库的 `UNIX` 服务器。使用 `LPAR`，可以在逻辑分区上分配多个 `Linux` 实例，将这些服务器中的合并到单个物理系统中，剩余容量可以用于数据库的 `AIX` 实例，以实现扩展性和性能。你还可以提供小型分区用于测试新版本的应用程序和操作系统（`AIX` 或 `Linux`），同时生产环境继续运行。这消除了对专用测试额外服务器的需求，并为测试版本能够平滑迁移到生产环境提供了更大的信心，因为它们在相同的硬件系统上进行了测试。

![](img/550f8fc128bac37c2a15bd674b67bcf1_292_0.png)

图 12-3 `LPAR` 上的 `AIX` 和 `Linux`

逻辑分区需要考虑的一些场景：

- `Linux` 是托管 `Web` 服务、网络、目录和安全管理、文件/打印服务、代理/缓存以及防火墙的理想选择。这些应用程序利用了 `Linux` 的优势、卓越的网络和 `Web` 服务能力以及单应用程序环境。
- `Linux` 也是邮件服务器、即时消息和组软件功能的良好选择。`Linux` 具有独特的特性，非常适合网络支持、目录管理安全以及大文件支持。
- `Linux` 具有处理数据库和数据仓库需求的存储支持。然而，如果性能和响应时间是因素，对于这类应用应考虑 `AIX`。
- `AIX` 能够更好地处理需要大量存储的事务环境、核心应用环境以及对业务影响巨大的停机情况。

## 其他相关信息和链接

有关逻辑分区技术的更多信息，您可以阅读以下文档：

- `IBM @server pSeries 690` 系统分区白皮书。以下网站提供了逻辑分区技术的概述。

`http://www.ibm.com/servers/eserver/pseries/hardware/whitepapers/lpar.html`

- `IBM @server pSeries 670` 和 `pSeries 690` 系统手册，`SG24-7040`。这本红书是支持 `p670` 和 `p690` 的技术专家的良好参考。它还包含了关于模型架构及其独特特性的信息。
- 适用于 `iSeries` 和 `pSeries` 系统的 `SuSE Linux Enterprise (SLES) 7`。该网站包含 `iSeries` 和 `pSeries` 系统的 `SLES 7` 产品详情：

`http://www.suse.com/products/suse_business/sles/sles_iSeries_pSeries/index.html`

有关在 `p690` 逻辑分区上安装 `Linux` 的说明，请阅读《`pSeries` 上的 `Linux` 应用》，`SG24-6033`；第 5 章“`pSeries` 上的原生 `Linux`”详细描述了在几种 `pSeries` 硬件类型（包括 `p690`）上安装原生 `Linux` 操作系统的步骤，包括一些常见的 `Linux` 应用程序。

## 12.2 用于 `Linux` 的 `AIX` 工具箱

为了支持 `UNIX` 和 `Linux` 这两个世界的优点，`IBM` 正将 `Linux` 应用程序互操作性引入 `AIX 5L`。在第 277 页的图 12-4 显示了提供 `Linux` 应用程序互操作性的两种互补方法：使用用于 `Linux` 的 `AIX` 工具箱，以及在 `AIX 5L` 中包含兼容 `Linux` 的应用程序接口 (`API`)、库和命令以实现稳健的性能实现。

### `AIX Power`

`AIX - Linux RPM` 附加包

| `Linux 32` 位应用程序源码 `RPM` | `Linux 32` 位应用程序源码 `RPM` (重复) |
| :--- | :--- |
| 用于 `Linux` 的 `AIX` 工具箱 | `AIX` 内核 |
| `AIX - Linux RPM` 附加包 | `AIX - Linux RPM` 包 |
| 构建时间 - 配置 | 构建时间环境 |
| `AIX` 头文件 | 额外的 `Linux` 头文件 |
| `AIX` 命令 | 额外的 `Linux` 库 |
| `AIX` 库 | 额外的 `Linux` 头文件 |
| `AIX` 媒体 | `64` 位库 |
| `AIX` 源 | `64` 位源码 |
| `AIX` 系统 | `AIX` 系统 |

用于 `Linux` 的 `AIX` 工具箱提供了在 `AIX` 上轻松编译和运行开源软件 (`OSS`) 的能力。工具箱提供了有效编译软件所需的所有工具。

以下是 `AIX` 工具箱中包含的一些工具：

- 图形桌面
- 开发工具
  - `automake`, `g++`, `make`, `autoconf`, `libtool`, `m4`, `patch`, `rpm`
- 开发库
  - `libxml`, `db`, `gtk+`, `libtiff`, `ncurses`, `qt`, `zlib`
- 用户界面
  - `Sawfish`, `control-center`, `enlightenment`
- 数据库应用
  - `MySQL`
- 加密内容 (`SSL`)
- `AIX for Linux`
- 系统应用
  - `Samba` 客户端, `Gnome` 工具, `mtools`
- 系统 `Shell`
  - `bash`, `tcsh`, `zsh`, `mc`
- 编程语言
  - `Python`, `C` 和 `C++` 编译器, `PHP`
- 互联网应用
  - `Fetch`, `lynx`, `ncpft`, `pine`, `xchat`, `ytalk`, `wget`, `elm`
- 归档应用
  - `tar`, `cpio`, `drecord`, `zip`, `unzip`, `bzip2`, `gzip`
- 图形游戏
  - `GNU` 象棋程序
- 编辑应用程序
  - `emacs`, `notepad+`, `vim`

用于 `Linux` 的 `AIX` 工具箱媒体包含在所有 `AIX` 媒体中。工具以 `RPM` 格式封装。除了随 `AIX` 附带的箱媒体外，你还可以在以下 `URL` 获取完整列表，或下载 `AIX` 工具箱中包含的所有可用工具：

`http://www.ibm.com/servers/aix/products/aixos/linux/download.html`

或直接从 `FTP` 站点：

`ftp://ftp.software.ibm.com/aix/freeSoftware/aixtoolbox`

工具的新旧版本、`spec` 文件以及用于构建工具的补丁。

对于受开源许可证（如 `GPL` 许可证）保护且需要分发源码的包，你可以从官方软件包网站获取源码，也可以在此处获取：

`http://www6.software.ibm.com/dl/tbxsrc/tbxsrc-p`

`AIX Linux` 应用工具箱中提供的图形桌面由不同的元素组成，这些元素提供了特定的图形开发框架，且不同桌面之间的框架有所不同。

安装了图形桌面后，你可以享受 `Linux` 风格的外观和界面（`KDE` 和 `Gnome`），同时利用 `AIX` 提供的功能和优势。12-5 是在安装并配置了工具箱提供的 `KDE` 软件包后，在 `AIX` 上运行的 `KDE` 显示管理器 (`KDM`) 示例。

![](img/550f8fc128bac37c2a15bd674b67bcf1_296_0.png)

图 12-5 `KDE` 显示管理器和链接

## 其他相关信息和链接

关于 `AIX Linux` 应用工具箱的更多信息，您可以阅读以下文档：

- `AIX Linux` 应用工具箱网站。这是工具箱的官方网站。该网站包含工具箱内工具的链接以及与各种软件包相关的许可证：

`http://www.ibm.com/servers/aix/products/aixos/linux/`

- `AIX` 与 `Linux` 技术亲和性白皮书。该白皮书总结了 `Linux` 应用与 `AIX 5L` 的互操作性，可以在此处找到：

`http://www.ibm.com/servers/aix/products/aixos/linux/affinity_linux.pdf`

- `IBM Linux` 和开源网站。该网站介绍了 `IBM` 提供的所有与 `Linux` 相关的产品和服务。可以在此处找到：

`http://www.ibm.com/linux`

关于在 `UNIX` 上移植应用程序的信息，您可以阅读以下文档：

- `AIX 5L` 移植指南，`SG24-6034`。这本红书（`redbook`）详细介绍了从其他基于 `UNIX` 的平台迁移到 `AIX 5L` 操作系统时可能遇到的问题类型。
- `UNIX` 移植指南网站。该网站提供了将应用程序迁移到不同 `UNIX` 平台的链接和提示。可以在此处找到：

`http://unixporting.com/porting-guides.html`

# 缩写和术语

| 缩写 | 术语 | 缩写 | 术语 |
| :--- | :--- | :--- | :--- |
| `ACL` | 访问控制列表 | `HMC` | 硬件管理控制台 |
| `AH` | 认证头 | `HTTP` | 超文传输协议 |
| `API` | 应用程序编程接口 | `IBM` | 国际业务机器公司 |
| `ASCII` | 信息交换美国标准代码 | `IETF` | 互联网工程任务组 |
| `CA` | 证书颁发机构 | `IHS` | `IBM HTTP` 服务器 |
| `CBC` | 密码块链 | `IKE` | 密钥交换 |
| `CIFS` | 通用互联网文件系统 | `IPSec` | `IP` 安全 |
| `CRL` | 证书撤销列表 | `ISAKMP` | 安全关联和密钥管理协议 |
| `DAP` | 目录访问协议 (`X.500, DS`) | `ITSO` | 国际技术支持组织 |
| `DCE` | 分布式计算环境 | `JFS` | 日志文件系统 |
| `DES` | 数据加密标准 | `KDM` | 密钥中心 |
| `DH` | `Diffie-Hellman` | `KDM` | `KDE` 显示管理器 |
| `DHCP` | 动态主机配置协议 | `LAN` | 局域网 |
| `DLPAR` | 动态逻辑分区区分名称 (`X.500`) | `LDAP` | 轻量级数据访问协议 |
| `DN` | 域名系统 | `LIFID` | `LDAP` 数据交换格式 |
| `DNSSEC` | `DNS` 安全 | `LPAR` | 逻辑分区 |
| `DSA` | 数字签名算法 | `MAC` | 消息认证码 |
| `ECB` | 电子密码块 | `MIB` | 管理信息库 |
| `EIM` | 企业身份映射 | `MIME` | 多用途互联网邮件扩展 |
| `ESP` | 封装安全载荷 | `MIT` | 马萨诸塞理工学院 |
| `FQDN` | 完全限定域名 | `NAS` | 网络身份验证服务 |
| `GID` | 组 `ID` | `NFS` | 网络文件系统 |
| `GNU` | `GNU` 不是 `UNIX` | `NIS` | 网络信息服务 |
| `GSS` | 通用安全服务 | `NS` | 名称服务器 |
| `GUI` | 图形用户界面 | `NSS` | 命名服务切换器 |
| `TLS` | 传输层安全 | `TSIG` | 事务签名 |
| `NTP` | 网络时间协议 | `UDF` | 通用数据格式 |
| `OFB` | 输出反馈 | `UID` | 用户标识符 |
| `OSI` | 开放系统互连 | `VPN` | 虚拟专用网络 |
| `OSS` | 开源软件 | `PAM` | 可插件认证模块 |
| `PEM` | 隐私增强邮件 | `PKI` | 公钥基础设施 |
| `POSIX` | 可移植操作系统接口 | `PTR` | 指针 |
| `PSK` | 公共共享密钥 | `RFC` | 征求 |
| `RPC` | 远程过程调用 | `RPM` | 红帽包管理器 |
| `RSA` | `Rivest, Shamir, and Adleman` (加密) | `SA` | 安全关联 |
| `SASL` | 简单认证和安全层 | `SDK` | 软件开发包 |
| `SMB` | 服务器消息块 | `SMBFS` | 服务器消息块文件系统 |
| `SMTP` | 简单邮件传输协议 | `SNMP` | 简单网络管理协议 |
| `SOA` | 区域起始 | `SPI` | 安全参数索引 |
| `SSH` | 安全外壳 | `SSL` | 安全套接层 |
| `SSO` | 单点登录 | `SWAT` | `Samba Web` |
| `TCP/IP` | 传输控制协议 | | |

# 相关出版物

本节列出的出版物适用于对涵盖主题进行更详细的讨论。有关订购这些出版物的信息，请参阅第 291 页。

# 其他资源

本节列出的出版物也相关。

- `AIX 5L` 移植指南
- `AIX 5L` 安全指南
- `AIX 5L` 系统管理
- `AIX 5L` 网络信息
- `AIX 5L` 通用编程
- `AIX 5L` 调试
- `AIX 5L` 命令
- `AIX 5L` 安装
- `AIX 5L` 打印机
- `AIX 5L` 创建备份
- `Bull's` 免费软件网站

`http://www.bullfreeware.com`

- `sendmail` 的 `cf/README`

`http://www.sendmail.org/m4/intro.html`

- 公钥加密中的合规性缺陷，地址见：

`http://world.std.com/?dtd/compliance/compliance`

- `Heimdal` 中不同的数据库方法

`http://www.nada.kth.se/joda/publications/heimdal-2000.pdf`

- 目录互操作性论坛 (`The Directory Interoperability Forum`)
