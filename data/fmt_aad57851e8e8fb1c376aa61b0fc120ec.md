
## 问题 6

b. 存储管理器（Storage Manager）

c. 并行端口管理器（Parallel Port Manager）

d. 打印机管理器（Printer Manager）

答案 c 正确。AdminSuite 包含串口管理器，而不是并行端口管理器。数据库管理器、存储管理器和打印机管理器都包含在 AdminSuite 中。因此答案 a、b 和 d 是错误的。

## 问题 7

使用主机管理器可以以下哪些任务？[选择所有适用项]

a. 添加 OS 服务

b. OS 服务

c. 将 AutoClient 转换为独立系统

d. 设置启动服务器

e. 设置 AutoClient 系统的根密码

答案 a、b、c、d 和 e 正确。你可以使用主机管理器执行所有这些任务。

## 问题 8

识别控制台功能的名称，该功能消除了登录控制台管理的每台主机的需要。

正确答案是单登录（single login）。

## 问题 9

以下哪个命令是 AdminSuite 提供的？

a. `admsliceadd`

b. `admfilsysdel`

c. `admdbls`

d. `admserialmod`

e. `admprinteradd`

答案 d 正确。AdminSuite 包含 `admserialmod` 命令。答案 a、b、c 和 e 中的命令不存在。

# 想要了解更多吗？

Sun Microsystems, Solstice AdminSuite 2.3 管理指南。提供纸质版（部件号 802-7048）和 docs.sun.com 网页版。

Sun Microsystems, Solstice AdminSuite 2.3 安装与发布说明。提供纸质版（部件号 805-3027）和 docs.sun.com 网页版。

# 第 21 章：跨网络安装和 JumpStart

你需要理解的术语：

- 安装阶段
- 安装方法
- 软件包、集群和组
- 跨网络安装
- 安装服务器
- 启动服务器
- 自定义 JumpStart
- JumpStart 规则和配置文件

你需要掌握的技巧：

- 安装系统
- 预配置系统信息
- 设置跨网络安装
- 设置 JumpStart 配置

## 服务器安装

本节包含了安装阶段、可以在系统上安装的配置以及跨网络安装。

## 安装阶段

安装包括三个阶段：系统配置阶段识别必要的系统信息，系统安装阶段将软件复制到系统，后期阶段更新系统。

### 系统配置阶段

在系统配置阶段，识别系统的基本信息（如主机名和域名）。可以选择，这些信息可以提前设置或预配置。你可以使用两种方法预配置系统信息。第一种使用 `sysidcfg` 文件，第二种使用名称服务。

> 如果系统未预配置，将在安装期间执行 `sysidtool` 以提示信息。`sysidtool` 由五个程序组成：`sysidnet`、`sysidnis`、`sysidys`、`sysroot` 和 `sysidpm`。

### 系统安装阶段

在系统安装阶段，使用以下方法之一安装选定的 Solaris 8 软件组（后文介绍）：

- SunInstall（标准交互式安装）
- Web Start
- JumpStart
- 自定义 JumpStart

两种交互式方法（SunInstall 和 Web Start）是第一部分考试目标，已在第 3 章中讨论。两种自动安装方法（JumpStart 和自定义 JumpStart）是第二部分考试目标，将在本章后介绍。

> 所有四种安装方法都可以使用后文介绍的跨网络安装。然而，考试 310-012 仅涉及与 JumpStart 相关的跨网络安装。

如前所述，在系统配置阶段，会识别系统的基本信息（如主机名和域名）。这些信息可以在 `sysidcfg` 文件中定义、在使用的服务名称（NIS 或 NIS+）中定义，也可以在交互式对话框中手动定义。

#### 使用 sysidcfg 文件

要使用 `sysidcfg` 文件方法，你需要为每个系统创建一个文件，其中包含一组 `keyword=value` 格式的行，例如 `timezone=US-CENTRAL`。该文件可以通过网络文件系统 (NFS) 在网络上启用，也可以挂载在本地软驱驱动器的磁盘上。

在 `sysidcfg` 文件中可以定义以下信息：

- 名称服务（NIS、NIS+、DNS 或无），以及服务器的主机名和互联网协议 (IP) 地址
- 域名
- 网络接口（启用 DHCP 使用或指定 IP 地址和子网掩码；启用 IPv6）
- Root 密码
- 系统区域环境
- 终端（键盘、鼠标、显示器和显卡类型）
- 时区（时区设置和时间服务器）

#### NIS

对于名称服务方法，每个系统的条目会被添加到网络信息服务 (NIS) 或网络信息服务加 (NIS+) 数据库中。名称服务将在第 19 章介绍。

可以使用 NIS/NIS+ 定义以下系统定义信息：

- 名称服务（隐含）
- 主机名和 IP 地址
- 系统区域环境
- 时区（时区设置和时间服务器）

> **考试警示**
>
> `sysidcfg` 文件中可以定义许多在名称服务中无法定义的信息，包括域名、大多数网络接口参数（子网掩码、DHCP 使用和 IPv6 使用）、root 密码以及终端信息（显示器、键盘、鼠标等）。

系统区域环境（特定语言和区域）存储在 `/etc/locale` 文件中，可以针对系统或域名进行指定。对于 NIS，你可以通过修改和执行 NIS makefile 来构建 `locale.byname` 映射。`/etc/locale` 文件用作 `local.byname` 映射的信息源。对于 NIS+，你使用 `nistbladm(1)` 命令构建本地表并添加条目。

## 软件配置

Solaris 8 软件系统以几种不同的配置发行，如下文章节所示。

### 软件包

Solaris 8 系统和应用软件作为文件和目录的集合提供，称为软件包。这些软件包可以从 CD-ROM 或磁带作为单个压缩文件复制到系统上，然后解压进行安装。

软件包中还包含了有关该软件包的信息，例如标题、存储要求和版本。还包括了正确安装软件所需的任何自定义脚本。

### 软件集群

有时，系统软件分发在多个软件包中，但这些软件包需要作为一个单元进行分发和安装。两个或多个相关软件包的集合被称为软件集群。软件集群是软件包的逻辑分组。

### 软件组

软件组（也称为软件配置集群）是软件集群的集合。根据系统的预期用途，应选择最合适的软件组来安装操作系统。表 21.1 描述了五种软件组。

#### 表 21.1：Solaris 8 软件组

| 软件组 | 内容 |
| :--- | :--- |
| 核心 (Core) | 操作系统所需的最小文件。 |
| 用户支持系统 (End User Support System) | 支持普通用户的典型配置。由 Core 软件组加上：窗口化软件：通用桌面环境 (CDE) 和 Open Windows，基础网络和打印机支持，标准 Unix 和补丁工具，Java 虚拟机 |
| 开发者系统支持 (Developer System Support) | 旨在作为软件开发环境。由用户支持系统软件组加上：编程工具和库，扩展终端，X 和内核探测支持，CDE/Motif 开发者软件和运行时，在线帮助文档页 |
| 完整发行版 (Entire Distribution) | Solaris 8 发行版包含的所有文件。由开发者系统支持软件组加上：AnswerBook2（基于 Web 的在线文档），增强型安全功能（包括磁盘配额和系统审计），增强型网络支持（包括 Unix-to-Unix 拷贝协议 (UUCP)、动态主机配置协议 (DHCP) 服务器、点对点协议 (PPP) 和网络信息服务 (NIS) |
| 完整发行版增强 (Entire Distribution Plus) | 包含可选硬件 OEM 系统支持组件的模块和驱动程序。由完整发行版软件组加上：PCI 驱动程序，SunFastEthernet 和 FastWide SCSI 适配器驱动程序 |

## 网络安装

通常，Solaris 直接从 Solaris 发行版 CD 安装。这需要每个系统都配备 CD-ROM 驱动器。然而，还有另一种方法：可以使用远程服务器通过网络安装 Solaris，该服务器拥有 Solaris 发行版 CD，或者在其硬盘上有 Solaris 发行版 CD 文件的副本。

网络安装可以与两种交互式安装方法（Solaris 交互式安装或 Web Start，见第 3 章）或两种自动安装方法（JumpStart 和自定义 JumpStart）配合使用。

要执行网络安装，你必须设置一个或多个网络服务器，由安装服务器和可能存在的启动服务器组成。此外，你必须在本地 NIS 或 NIS+ 服务中或在相应安装服务器的 `/etc` 文件中添加安装客户端的信息。

### 安装服务器

安装服务器是提供网络安装 Solaris 所需文件的系统。网络安装可以与两种交互式安装方法（Solaris 交互式安装或 Web Start，见第 3 章）或两种自动安装方法（JumpStart 和自定义 JumpStart）配合使用。

通常，Solaris 直接从 Solaris 发行版 CD 安装。这需要每个系统都配备 CD-ROM 驱动器。然而，还有另一种方法：可以使用远程服务器通过网络安装 Solaris，该服务器拥有 Solaris 发行版 CD，或者在其硬盘上有 Solaris 发行版 CD 文件的副本。

安装服务器是提供网络安装 Solaris 所需文件的系统。网络安装可以与两种交互式安装方法（Solaris 交互式安装或 Web Start，见第 3 章）或两种自动安装方法（JumpStart 和自定义 JumpStart）配合使用。

虽然可以使用任何目录，但按照惯例目录为 `/export/install`。

由于 Intel 兼容客户端从本地软驱或本地 CD-ROM 启动，因此它们不需要启动服务器进行安装。

安装服务器是提供网络安装 Solaris 所需文件的系统。网络安装可以与两种交互式安装方法（Solaris 交互式安装或 Web Start，见第 3 章）或两种自动安装方法（JumpStart 和自定义 JumpStart）配合使用。

默认情况下，安装服务器支持 SunInstallation 程序（第 3 章）。然而，可以修改安装服务器以使用 Solaris 开始程序。`modify_install_server(1)` 命令（位于 Solaris 8 安装 CD 上）可用于启用了 Web Start 的微内核从 CD 复制到安装服务器配置中。

`setup_install_server` 将软件 CD 镜像复制到指定的目录。复制 Product 和 Tools 目录。此外会在 Tools 目录中创建一个包含网络子网掩码的 netmask 文件。

与安装服务器位于不同子网不同，启动服务器必须设置在与安装客户端相同的子网内。

启动服务器被要求与 SPARC 安装客户端位于同一子网内，因为客户端使用启动协议（BOOTP）从启动服务器获取启动信息。通常，此协议不会通过路由器（连接子网的设备）传输。

要将系统设置为启动服务器，系统必须能够通过本地 CD-ROM 驱动器或远程共享 CD-ROM 驱动器访问 Solaris 软件发行版 CD。

发行版 CD 中 Solaris_8/Tools 目录下的 `setup_install_server` 命令会将启动软件复制到启动服务器。需要两个命令行参数：`-b`，指定正在设置启动服务器；以及用于拷贝启动文件的空目录的完整 `dirname`。虽然可以是任何目录，但按照惯例，该目录命名为 `boot` 并位于 `/export/install` 目录下。以下行执行从发行 CD 中 Solaris_8/Tools 目录下的 `setup_install_server` 命令来设置启动服务器：

```
./setup_install_server -b /export/install/boot
```

### 添加安装客户端

当通过网络安装系统或安装客户端时，需要通过名称服务（NIS/NIS+）或安装服务器或启动服务器上 `/etc` 目录下的文件提供有关安装客户端的基本信息。

你可以使用 Solstice Host Manager 程序来添加这些信息，或者在没有 Host Manager 的情况下，使用 `add_install_client` 命令。

`add_install_client` 命令只能用于更新安装服务器或启动服务器上的 `/etc` 文件。请使用相应的 NIS 或 NIS+ 过程将客户端信息添加到这些名称服务中。至少，你必须添加客户端的主机名、IP 地址和以太网地址。

根据环境的不同，你可以修改以下 `/etc` 文件以支持网络安装：

- `/etc/bootparams(4)`——每个客户端的条目，用于定义启动客户端所需的各种路径和参数
- `/etc/dfs/dfstab(4)`——任何应共享的 NIS 资源的条目
- `/etc/ethers(4)`——以太网地址映射到系统主机名的条目
- `/etc/exports(4)`——任何应共享的 NFS 资源的条目
- `/etc/hosts(4)`——将主机名映射到 IP 地址的条目
- `/etc/inetd.conf(4)`——启用简易文件传输协议（FTP）守护进程的条目

以下行使用 `add_install_client` 命令为网络安装设置系统。该命令从 Solaris_8/Tools 发行 CD (2 of 2) 发行 CD 或从 Solaris 8 安装 CD 的挂载点执行。要安装的系统名称由系统平台组允许的 `host` 命令参数识别。

在这种情况下，使用命令行参数 `sun4m` 来识别要安装的系统为 SPARC5 平台：

```
## add_install_client host sun4m
```

#### 表 21.2：`add_install_client` 命令的命令行参数

| 参数 | 说明 |
| --- | --- |
| `-c server:path` | 指定 JumpStart 目录的配置文件服务器和路径。 |
| `-d` | 将客户端定义为 DHCP 客户端。 |
| `-e address` | 指定以太网地址。 |
| `-i address` | 指定 IP 地址。 |
| `-n server:service netmask` | 指定名称服务和名称服务服务器。也可以定义子掩码。 |
| `-p server:path` | 指定存放 `syscfg` 文件的服务器以及 `syscfg` 文件的绝对路径。 |
| `-s server:path` | 指定安装服务器和 CD 镜像的路径（仅当你向启动服务器添加客户端时需要）。 |

### 安装/启动服务器守护进程

安装和启动服务器使用多个网络守护进程来支持网络安装。

- `in.arpd(1M)`——反向地址解析协议（RARP）守护进程提供以太网地址到 IP 地址的解析。客户端使用此服务根据分配的以太网地址确定其 IP 地址。
- `in.tftpd(1M)`——简易文件传输协议（TFTP）守护进程为 SPARC 安装客户端提供了一种无需登录即可从服务器获取可启动镜像的方法。
- `nfd(1M)`——NFS 守护进程提供网络对文件系统的远程访问。
- `rpc.bootparam(1M)`——启动协议（BOOTP）守护进程为客户端提供来自 `/etc/bootparams` 的启动信息

#### RARP 守护进程 (in.arpd)

`/etc/sbin/rarpd` 守护进程提供以太网地址到 IP 地址的解析。当接收到 RARP 请求时，`in.arp` 程序尝试确定给指定以太网地址的 IP 地址。查找过程包括首先查找以太网地址以获取系统主机名，然后查找主机名以确定其 IP 地址。

查找主机名（基于以太网地址）的过程由名称服务开关（`/etc/nsswitch.conf`）文件中 *ethers* 关键字的配置决定。它可以从 NIS (ethers.byaddr map)、NIS+ (ethers table) 或 `/etc/ethers` 文件获取。查看 *ethers(4)* 可了解 `/ethers` 的格式。

#### TFTP 守护进程 (in.tftpd)

`/usr/sbin/tftpd` 守护进程为 SPARC 安装客户端提供了一种无需登录即可从服务器获取可启动镜像的方法。与标准文件传输协议（FTP）不同，TFTP 不需要用户身份验证。启动镜像通常存储在 `/tftp` 下。

#### NFS 守护进程 (nfd)

`/usr/lib/nfs` 守护进程提供网络对文件系统的远程访问。这些文件由 `rpc.bootparam` 识别。

#### 启动参数守护进程 (rpc.bootparam)

`/usr/sbin/rpc.bootparam` 守护进程提供启动客户端所需的参数。信息的来源由名称服务开关（`/etc/nsswitch.conf`）文件中的 *bootparams* 关键字决定。它可以从 NIS (bootparams map)、NIS+ (bootparams table) 或 `/etc/bootparams` 文件获取。查看 bootparams(4) 可了解 `/etc/bootparams` 的格式。

在安装大量系统时分发多个配置磁盘。JumpStart 目录中的两种基本类型文件是规则文件（rules file）和一个或多个配置文件（profile files）。

第二部分考试 (310-012) 继续将配置文件称为类文件（class file），尽管它早在 Solaris 2.6 系统文档中就已经被重命名了。在看到引用类文件的 JumpStart 问题时，请记住这一点。

### 规则文件

规则文件是一个文本文件，其中每个要自动安装的系统或系统组都包含一个条目或规则。每个规则根据一个或多个属性识别系统（或系统组），并标识一个该系统或系统组提供配置细节的唯一配置文件。
