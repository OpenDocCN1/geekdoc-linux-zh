
# IBM i5/OS Linux 集成指南

![](img/165c050f45ac58e1635258993855261a_0_0.png)

Manik Ahuja

Erwin Earley

Rico Franke

Vlatko Kosturjak

Rajeev Sharma

Yessong Johng

![](img/165c050f45ac58e1635258993855261a_2_0.png)

本版本适用于 IBM i5/OS 的 V5R4。

- AFP™
- AS/400®
- DB2 Universal Database™
- i/OS®
- Infointrint
- IPS™
- NetServer™
- OS/400™
- Power PO®
- Redbooks™
- System i™
- xSeries®

## 前言

IBM® System i 平台提供了许多集成点，支持利用 IBM i/OS 应用和数据的 Linux® 应用，例如用于 Linux 的 IBM eServer™ iSeries™ Access、带有 Samba 的 IBM i/OS NetServer™ 以及 IBM Java™ Virtual Machine 和 JTO。

本 Redbook 涵盖了所有的通信技术并附有示例代码，为您展示了可以用于连接 Linux 应用与 IBM i/OS 的方法。

本书旨在帮助具有 IBM i/OS 背景的 Linux 用户、程序员和管理员连接 Linux 与 IBM i/OS。

## 编写本 IBM Redbook 的团队

本书由来自全球普普基斯基中心（Poughkeepsie Center）的国际技术支持组织的专家团队编写。

![](img/165c050f45ac58e1635258993855261a_10_0.png)

Manik Ahuja 是 IBM 的 IT 架构师。他的工作是通过为每个需求选择软硬件组合来设计 IT 基础设施解决方案。Manik 拥有大多数操作系统的行业认可认证，并且精通硬件和软件技术。他于 1995 年从计算机实验室助理开始职业，逐渐变为系统管理员，然后成为 IT 架构师。他是公认的开源专家，并为各种杂志编写技术文章。他的专业领域包括设计和实施电子邮件系统、高可用性集群、数据整合技术和可视化解决方案。

![](img/165c050f45ac58e1635258993855261a_10_1.png)

Erwin Earley 是 IBM 的顾问软件工程师，分配在明尼苏达州罗彻斯特的系统技术中心。在 Linux 卓越中心的工作中，Erwin 负责为 IBM i 平台上的 Linux 人员提供技术赋能。Erwin 写了大量关于 System i 上 Linux 的文章，是 Linux 专业协会的认证专业人士，也是红帽认证技术员。可以通过 `erwin.earley@us.ibm.com` 联系他。

![](img/165c050f45ac58e1635258993855261a_10_2.png)

Franco Rico 是德国 IBM 的 i 技术专家。他在 iSeries Access、EIM / Kerberos、集成 IBM iSeries® 系统 (`IXA`) 和逻辑分区 (`LPAR`) 方面拥有五年经验。他为 IBM 客户提供问题确定、配置和使用方面的帮助。他拥有曼海姆合作教育大学的信息技术工程学士学位。

Vlatko Kosturjak 是位于克罗维亚 IBM 全球服务安全与隐私服务的 IT 专家。在实践中，Vlatko Kosturjak 专注于黑客攻击、IT 审计、根据 `ISO/IEC 17799` 开发的安全策略制定、企业级连续性与恢复计划的设计、实施和验证的咨询服务，并协助客户开发和实施有效的安全解决方案以保护其信息资产。他在网络安全设计和各种操作系统的服务器加固方面拥有丰富经验。

![](img/165c050f45ac58e1635258993855261a_11_0.png)

Rajeev Sharma 是 IBM 印度销售与分销部的 Linux IT 专家。他之前的工作包括 Novelle 班罗 Linux Impact 团队的技术客户经理，以及孟买 NetCore Solutions 的系统工程师和业务开发。他是 SUSE Enterprise Server 和 SUSE Linux Open Exchange 等咨询及解决方案设计实施领域的专家。

Yessong Jong 是罗彻斯特中心国际技术支持组织的 IBM 认证专家。他于 1982 年作为 S/38 系统工程师开始 IBM 职业，并一直从事 S/38 和 IBM AS/400 工作。

Monte Bruesewitz

Mark Vanderziel

Pamela Bowen

Richard Johnston

Selwyn Dickey

Steven Janssen

Vess Natchev

## 欢迎反馈

您的意见对我们至关重要。

我们希望您的 IBM Redbooks™ 尽可能为您提供帮助。您可以通过以下任一方式向我们提交对此或其他 IBM Redbooks 的反馈：

- 使用在线的“联系我们”（Contact us）来查看 IBM Redbook 反馈表，地址为：

  `ibm.com/redbooks`

- 通过电子邮件将您的意见发送至：

  `redbook@us.ibm.com`

- 邮寄邮件您的意见至：

  IBM Corporation, International Technical Support Organization

  Dept. HYTD Mail Station PO99

  2455 South Road

  Poughkeepsie, NY 55901-7829.

# Linux 与 IBM i5/OS 集成简介

本章概述了 Linux 与 IBM i5/OS 之间的连接方法。本章将讨论以下领域：

- 将 Linux 与 IBM i5/OS 集成的优势

- Linux 与 IBM i5/OS 之间通信技术的概述

## 1.1 将 Linux 与 IBM i5/OS 集成的优势

IBM 致力于在 iSeries 平台上支持 Linux 操作系统。它支持将 Linux 安装到 iSeries 分区、集成 xSeries 服务器 (`IXS`) 以及集成 xSeries 适配器 (`IXA`)，从而减少购买额外硬件的资本支出。这些配置在《IBM eSeries Server: An Implementation Guide》（SG24-6232）、《Implementing Linux on Integrated xSeries Solutions for iSeries》（SG24-6379）以及《Implementing Web Applications with CM Information Integrator for Content and OnDemand Web Enable Kit》（SG24-6338）中有详细介绍。

IBM 通过开发多种方法进一步增强了对 Linux 的支持，这些方法可以集成运行在 Linux 和 IBM i5/OS 上的实际数据和应用程序。例如 iAccess for Linux 产品，它允许 Linux 用户通过 5250 会话或启用开放数据库连接（`ODBC`）的应用程序到 IBM i5/OS。

连接 Linux 和 i5/OS 的能力结合了这两个操作系统的主要优势。例如，i5/OS 的数据库应用程序和 Linux 的 Web 特性提供了一个强大且集中的计算环境。

传统上，客户一直将 iSeries 系统及其前身 AS/400 作为数据库机器，用于存储和检索与其业务相关的大量信息。IBM DB2 Universal Database for iSeries 完全集成到 i5/OS 操作系统中。客户可以从 iSeries 的单级安全、对象、文件和打印管理、可靠性和可扩展性中受益。与其他某些系统类型不同，随着客户业务的扩大，iSeries 系统硬件可以升级，以满足对更大处理能力或存储空间的需求。

Linux 被认为是一种电子商务系统。目前，很大比例的 Linux 业务实现是使用 Apache Web Server 和 Tomcat Web Server 的 Web 服务器。Linux 操作系统为运行基于 PHP 超文本预处理器（`PHP`）和 Perl 的应用程序提供了一个极佳的环境。

然而，以下实现类型也很流行：

- 如 Sendmail 邮件网关之类的邮件服务器

- 使用 Samba 的文件和打印服务

- 防火墙

鉴于 Linux 广受欢迎的社区和开源特性，可以快速且经济地开发出反映不断变化的电子商务领域的新型、且具有吸引力的应用程序。需要访问数据库的应用程序现在可以通过访问运行在 iSeries 逻辑分区上的现有 DB2 Universal Database 来进行增强，从而缩短开发时间和成本。

## 1.2 Linux 连接技术概述

本节概述了您用于连接 Linux 操作系统与 i5/OS 的方法。这些技术和方法将在本书的后续章节中详细介绍，在某些情况下还会结合示例程序代码。



### 1.2.1 iSeries Access for Linux

`iSeries Access for Linux`提供基于`Linux`的`i/OS`set。它允许您从`Linux`系统建立到`i/OS`的`5250`会话。它还包含了用于访问`iSeries DB2 Universal Database (UDB)`的`ODBC`驱动。

`iSeries Access for Linux`支持`Intel®`和`IBM`平台。它运行在独立`PC`、`IBM PowerPC®`、`IXA`和`IXS`以及`IBM eServer`逻辑分区上。

`iSeries Access for Linux`产品在第5页的第2章“iSeries Access for Linux”中有进一步解释。

以下网站提供了有关`iSeries Access for Linux`的最新信息：

`http://www.ibm.com/servers/eserver/iseries/access/linux/`

### 1.2.2 用于 Linux 的 iSeries Access ODBC 驱动

`iSeries Linux ODBC`驱动是`iSeries Access for Linux`的一部分。它允许从`Linux`系统访问`iSeries IBM DB2 UDB`。该驱动程序基于随`iSeries Access for Windows`产品`5722XE1`提供的`ODBC`驱动，并类似地通过`socket`连接使用主机服务器接口访问系统。

`ODBC`驱动在第29页的第3章“使用 ODBC 连接 IBM i/OS”中介绍。

### 1.2.3 使用 JDBC 驱动连接 IBM i/OS

`IBM Toolbox for Java`产品`5722JC1`包含一个`Java`连接(`JDBC`)驱动，允许您使用`JDBC`编程接口(`API`)发出结构化查询语言(`SQL`)语句并处理来自`iSeries`数据库的结果。`Toolbox for Java`还包含一组`Java`类，提高了开发访问`IBM i/OS`数据程序的便利。

`JDBC`驱动在第51页的第4章“使用 JDBC 连接 IBM i/OS”中有进一步解释。

以下网站提供了有关`JDBC`驱动的信息：

`http://www.ibm.com/servers/eserver/iseries/toolbox/`

### 1.2.4 使用 Samba 的 NetServer 支持

`OS/400`已增加了对`Samba`使用服务器消息块(`SMB`)协议的支持。此处支持允许运行`Samba`的`Linux`客户端通过`smclient`和`smbmount`连接`iSeries NetServer`。

`Samba`客户端在第67页的第5章“使用 Samba 连接 iSeries NetServer”中介绍。

以下网站提供了有关`NetServer`的最新信息：

`http://www.ibm.com/servers/eserver/iseries/netserver/`

### 1.2.5 网络文件系统

网络文件系统(`NFS`)允许用户通过网协议(`IP`)网络访问远程计算机上的文件。`Linux`文件系统的性质使其能够存储在不同的位置。网络文件系统的目的是允许机器像访问本地驱动一样读写远程文件。这促进了跨网络的无缝共享。

`NFS`在第81页的第6章“使用 NFS 连接 IBM i/OS”中有进一步解释。

### 1.2.6 文件传输协议

文件传输协议(`FTP`)是传输控制协议/网协议(`TCP/IP`)的标准文件传输协议。可以使用`FTP`在`Linux`和`i5/OS`之间传输文本和二进制数据。

`FTP`在第89页的第7章“使用 FTP 连接 IBM i/OS”中进行了更详细的讨论。

### 1.2.7 编程 socket 连接

`Socket`以及在`socket`之上的程序可以处理您要在`Linux`和`i5/OS`之间提供的任何集成。

第95页的第8章“使用 socket 编程连接 IBM i/OS”提供了如何使用`socket`的示例，并让您了解如何将其用于您的目的。

# 2

# iSeries Access for Linux

`iSeries Access for Linux`是`iSeries Access`系列中的新产品。`iSeries Access for Linux`允许您使用其开放数据库连接(`ODBC`)驱动访问`iSeries DB2 Universal Database (UDB)`，并从`Linux`客户端建立到`IBM i5/OS`系统的`5250`会话。

本章涵盖以下内容：

- `iSeries Access for Linux`概述

- `iSeries Access for Linux`要求

- 安装步骤

- `5250`配置

`ODBC`主题在第29页的第3章“使用 ODBC 连接 IBM i/OS”中进行了详细讨论。

## 2.1 iSeries Access for Linux 产品概述

`iSeries Access for Linux`是`iSeries Access`系列`5722XW1`的附加产品。它提供了对`i5/OS`系统的`Linux`访问。`iSeries Access for Linux`通过将`i/OS`资源扩展到`Linux`，使用户能够利用整个企业的业务信息、应用程序和资源。

### 2.1.1 iSeries Access for Linux 产品特性

`iSeries Access for Linux`包含以下产品特性：

- `iSeries Access ODBC`驱动

基于`ODBC`编程接口(`API`)的`Linux`程序可以使用此驱动程序访问`iSeries`的`DB2`。`iSeries Access ODBC`驱动基于`iSeries Access for Windows`中的`ODBC`驱动。它使用`iSeries`数据库主机服务器作为系统的访问点。

- `5250`模拟器

它提供了等于`IBM 5250`终端的功能。该模拟器还提供了类似于`IBM PC5250`模拟器的扩展`5250`终端功能。该模拟器支持以下功能：

    - 支持自定义多选，多可达`99`个会话

    - 最佳字体：提供不同的字体且字体随窗口大小调整

    - 多语言支持

    - 宏记录/回放

    - 复制/粘贴

    - 支持`24x48`和`27x32`屏幕尺寸

    - 屏幕打印到`Postscript`打印机

    - 热点高选项

    - 自动、自定义的通信错误恢复

    - `1.8`版本支持双字节字符集(`DBCS`)

    - `1.10`版本支持单点登录和`Kerberos`

### 2.1.2 iSeries Access for Linux 数据表

本节介绍了与该产品相关的主题。在编写本文时，`iSeries Access for Linux`的实际版本为`1.10`。

最新可用版本为`5.4.0-1.0`

## 平台选择

`iSeries Access for Linux`设计用于基于`Intel`和`IBM POWER™`平台的`Linux`系统。`POWER`平台包括：

- `i5`上的`Linux`分区

- `p5`上的`Linux`分区

- `IBM OpenPower™`服务器

对于`Intel`兼容系统：

- 集成`xSeries`服务器(`IXS`)

- 通过集成`xSeries`适配器(`IXA`)连接的`xSeries`服务器

- 独立`Intel PC`和服务器

## 产品架构

该产品提供`Intel`和`POWER`实现的`32`位版本。

最新版本支持额外的`64`位平台（`PowerPC-64`和`x86-64`）。`ODBC`和扩展动态远程支持(`EDRS`)驱动均包含在`32`位和`64`位包中。`5250`模拟器包含在`32`位包中，但不包含在`64`位包中。

## 许可证要求

`iSeries Access`不是开源产品。使用`5250`模拟需要`IBM iSeries Family 5722XX`的许可证。使用`ODBC`驱动程序不需要许可证。`iSeries Access for Linux`的许可与`iSeries Access for Windows`相同。

## 可用性

`iSeries Access for Linux`以下载包的形式提供访问访问页面获取最新版本：

`http://www.ibm.com/servers/eserver/iseries/access/`

## 2.2 iSeries Access for Linux 要求

本节列出了`iSeries Access for Linux`安装前的要求。请先检查`i/OS`要求：

- 对于`5250`模拟，需要安装`IBM iSeries Access Family 5722XW1`并且你需要该产品的许可证。

- 启用`QUSER`用户配置文件。使用以下步骤验证配置文件状态。在`5250`命令输入屏幕上输入：

```
DSPUSRPRF USRPRF (QUSER)
```



此命令显示 `QUSER` 的状态，必须为 `ENABLED`。如果状态为 `DISABLED`，输入：

```
CHUSRPRF USRPRF (QUSER) STATUS (*ENABLED)
```

- 传输控制协议/网协议 (TCP/IP) 必须在你的 IBM i5/OS 上运行。
- 在 IBM i5/OS 中启动主机服务器。要启动它们，请输入：

```
STRHOSTSVR *ALL
```

Linux 客户端需要安装以下包：

- `glibc` 2.2 或更高版本

此包包含 GNU C 库。它包含了 C、数学和可移植操作系统接口 (POSIX) 最重要的标准库。使用以下命令检查已安装的版本：

```
linux:~> rpm -qa | glibc
glibc-2.4-31.2
glibc-64bit-2.4-31.2
```

- `Red Hat Package Manager (RPM)` 3.0 或更高版本

`RPM` 管理软件包。通过它你可以安装、删除和更新软件包。检查已安装的版本：

```
linux:> rpm --version
RPM version 4.4.2
```

- `openmfit` 2.0 或更高版本

`Openmfit` 是一个运行时环境。5250 模拟器需要此软件。要检查是否已安装，输入：

```
linux:> rpm -qa | grep openmfit
```

如果系统返回了其包的行，则说明已安装。

- `unixODBC` 驱动管理器版本 2.0.11 或更高版本

它在 Linux 平台上提供了应用程序与 `ODBC` 驱动之间的标准接口。要检查是否已安装，输入：

```
linux:> rpm -qa | grep openmfit
```

要获取更多信息，请访问：`http://www.unixodbc.org`

要切换到可缩放字体，请删除 `:unscaled`，这样所选 `dpi` 的行将如下所示：

```
/usr/X186/lib/X11/fonts/75dpi,

/usr/X186/lib/X11/fonts/100dpi,
```

### 2.3 在 Linux 上安装 iSeries Access

以下步骤将引导您完成在 Linux 上安装 `iSeries Access` 的过程：

1. 从以下地址下载 `iSeries Access` for Linux `RPM` 安装包：
   `http://www.ibm.com/servers/eserver/iseries/access/linux`
2. 有两种选项：使用带 5250 模拟器的 32 位 `RPM` 或不带 5250 模拟器的 64 位 `RPM` 来安装 `iSeries Access` for Linux。在 Linux 终端类型为 `linux` 的平台上，我们使用带 5250 模拟器的 32 位 `IBM PowerPC®` `RPM`：
   ```
   linux:\> rpm -ivh iSeriesAccess-5.4.0-X.YY.pc.rpm
   ```
   对于 Intel 平台：
   ```
   linux:\> rpm -ivh iSeriesAccess-5.4.0-X.YY.i386.rpm
   ```
   在这些情况下，`X.YY` 表示如示例 2-2 所示的 `iSeries Access` 版本。

   **示例 2-2 安装 Linux 版 iSeries Access RPM**

   ```
   linux:\> rpm -ivh iSeriesAccess-5.4.0-1.0.pc.rpm
   ###################################### [100%]
   Preparing...
   1:iSeriesAccess
   ###################################### [100%]
   post installing process for iSeriesAccess 1.0...1
   iSeries Access OODBC Driver 已删除（如果存在的话），因为其使用量为零
   dobcdriver: 已安装。使用量增加到 1。
   目标目录为 /etc/unixODBClinux:
   ```

   请注意以下几点：
   - 文件安装在 `/opt/ibm/iseriesAccess` 目录下。
   - 为了记录日志，请在命令末尾带有 `-vv` 参数运行 `rpm`，例如：
     ```
     linux:\> rpm -ivh iSeriesAccess-5.4.0-X.YY.pc.rpm -vv
     ```
   - 要更新旧版本的 Linux 版 `iSeries Access`，请带有 `-Uvh` 选项运行 `rpm` 命令，例如：
     ```
     linux:\> rpm -Uvh iSeriesAccess-5.4.0-X.YY.i386.rpm
     ```
   - 若要卸载，请带有 `-ev` 选项运行 `rpm` 命令，例如：
     ```
     linux:\> rpm -ev iSeriesAccess
     ```
   - 如果您使用了过时的 Linux 版 `iSeries ODBC` 驱动程序，则必须使用以下命令删除包：
     ```
     linux:> rpm -ev iSeriesODBC
     ```
   - 如果安装因为依赖 `libodbc.so` 或其他库而失败，请确保您已安装 `unixODBC` 驱动管理器。如果问题仍然存在，请带有 `-nodes` 参数运行安装以停止依赖检查：
     ```
     linux:> rpm -ivh iSeriesAccess-5.4.0-X.yy.rpm --nodes
     ```
3. 如示例 2-3 所示，使用 `cwbping` 命令测试安装。该命令 `ping` 到 `IBM i5/OS` 服务器，情况下由 IP 地址 `192.168.1.1` 指向。`ping` 成功返回表示两个系统之间的通信链路已建立。

   **示例 2-3 cwbping 命令**

   ```
   linux:> /opt/ibmSeriesAccess/bin/cwbping 192.168.1.1
   ```

   `IBM iSeries Access for Linux`

   `Version 5 Release 4 Level 0`

   `连接验证程序`

   `> (Copyright) IBM Corporation and Others 1984, 2003. 保留所有权利。`

   `美国政府受限权利 - 使用、复制或披露受与 IBM 公司签署的 GSA 计划合同限制。`

   `许可材料 - IBM 财产`

   `要取消 CWBPING 请求，请按 CTRL-C 或 CTRL-BREAK`

   `I 正在验证到系统 192.168.1.1 的连接...`

   `I 成功连接到服务器应用程序: Central Client`

   `I 成功连接到服务器应用程序: Network File`

   `I 成功连接到服务器应用程序: Data Access`

   `I 成功连接到服务器应用程序: Data Queues`

   `I 成功连接到服务器应用程序: Remote Command`

   `I 成功连接到服务器应用程序: Security`

   `I 成功连接到服务器应用程序: BDM`

   `I 成功连接到服务器应用程序: Telnet`

   `I 已验证到系统 192.168.1.1 的连接`

   > 注意：`cwbping` 命令安装在 `/opt/ibm/iSeriesAccess/bin/`。要从任何目录执行 `cwbping`，您的 `PATH` shell 变量需要包含已安装的 32 位版 `iSeries Access` 的 `/opt/ibm/iSeriesAccess/bin/` 条目以及 64 位版的 `/opt/ibm/iSeriesAccess/bin64/` 条目。

其他命令，例如用于 `ib5250` 启动 5250 仿真会话或使用 `rcmd` 运行 `i5` 命令也安装在此目录中。

### 2.4 5250 模拟器

`iSeries Access` 5250 模拟器是用于 Linux 上的多种语言实现，允许 Linux 终端用户 (`VNC`) 用户轻松使用这种语言。

本节涵盖了：

- 模块
- 某些功能

`iSeries Access` 的 5250 模拟器支持多种语言。

**表 2-1 支持语言**

| i/OS 语言 | 描述 |
| :--- | :--- |
| `et` | 阿尔巴尼亚语 |
| `bg` | 保加利亚语 |
| `cs` | 捷克语 |
| `da` | 丹麦语 |
| `es` | 西班牙语 |
| `fi` | 芬兰语 |
| `el` | 希腊语 |
| `is` | 冰岛语 |
| `ja` | 日语 |
| `nl` | 荷兰语 (比利时) |
| `hu` | 匈牙利语 |
| `lt` | 立陶宛亚语 |
| `lv` | 拉脱维亚语 |
| `lo` | 老挝语 |
| `mk` | 马其顿亚语 |
| `sr` | 塞尔维亚语 |
| `pl` | 波兰语 |
| `ro` | 罗马尼亚语 |
| `sk` | 斯洛伐克语 |
| `sq` | 阿尔巴尼亚语 |
| `pt` | 葡萄牙语 |
| `sv` | 瑞典语 |
| `tr` | 土耳其语 |
| `vi` | 越南语 |
| `zh` | 简体中文 |
| `en_CA` | 加拿大英语 |
| `en_GB` | 英语 |



| `en_HK` | 繁体中文 |
| :--- | :--- |
| `en_US` | 美式英语 |
| :--- | :--- |
| `fr_BE` | 比利时法语 |
| :--- | :--- |
| `fr_CA` | 加拿大法语 |
| :--- | :--- |
| `fr_CH` | 瑞士法语 |
| :--- | :--- |
| `de_DE` | 德国语 |
| :--- | :--- |
| `de_CH` | 瑞士德语 |
| :--- | :--- |
| `it_IT` | 意大利语 |
| :--- | :--- |
| `nl_BE` | 比利时荷兰语 |
| :--- | :--- |
| `nl_NL` | 荷兰语 |
| :--- | :--- |
| `pt_BR` | 巴西葡萄牙语 |
| :--- | :--- |
| `pt_PT` | 葡萄牙语 |
| :--- | :--- |
| `ru` | 俄语 |
| :--- | :--- |
| `zh_CN` | 简体中文 |
| :--- | :--- |
| `zh_HK` | 繁体中文 |
| :--- | :--- |
| `zh_TW` | 繁体中文 |

环境变量 `LANG` 可用于覆盖默认语言。

`iSeries` `Access` `5250` 模拟器支持多种语言，这在第 3 节中将讨论。

## 2.4.2 启动 5250 模拟器

模拟器由两个二进制文件组成：

- `ibm5250`
- `setup5250`

> 注意：我们不建议默认运行 `ibm5250`。切换到 `root` 用户时，运行应用程序所需的默认环境变量没有正确设置。作为普通用户运行 `ibm5250` 可能会导致问题（权限）。常见症状是模拟器无法读取配置文件。因此，它会恢复默认值。

### `ibm5250`

`ibm5250` 调用 5250 模拟器并打开图形用户界面 (GUI) 窗口，提示系统名称、用户和密码。这些信息用于获取系统的 572XX1 许可证，这是建立 5250 会话所需的。

输入 `<iSeriesName>` 启动模拟器或使用 `ibm5250 --help` 查看命令行选项。iSeries 名称是一个可选参数。这将如图 2-1 所示打开新建 5250 会话窗口。输入 IBM i/OS 用户配置和密码，然后点击 **打开 5250 会话**。如果出现类似 `ibm5250: command not found` 的错误，则必须将目录 `/opt/ibm/iSeriesAccess/bin/` 添加到 shell 变量中：

```bash
linux:~> ibm5250
5250: [ 信息 ]: 构建日期: 2005年7月13日 (1.10).
```

![](img/165c050f45ac58e1635258993855261a_27_0.png)

图 2-1 新 5250 会话

随后，5250 仿真如图 2-2 所示。

![](img/165c050f45ac58e1635258993855261a_28_0.png)

图 2-2 5250 会话

### `setup5250`

`setup5250` 是一个设置程序，可以使用它配置适用于当前用户 ID 的 5250 会话的设置，并定义多个连接。

1. 在 GUI 终端中，输入 `setup5250`：

   ```bash
   linux:\> setup5250

   setup5250: [ INFORMATIONAL ]: Build Date: 2005年7月13日 (1.10)

   setup5250: [ INFORMATIONAL ]: setup5250
   ```

主菜单如图 2-3 所示。

![](img/165c050f45ac58e1635258993855261a_28_1.png)

图 2-3 `setup5250`

第 2 章 Linux 下的 iSeries 15

菜单栏有 `Connection`（连接）、`Preferences`（首选项）、`Options`（选项）和 `Help`（帮助）四个列表。

- `Connection`（连接）

  使用此选项创建、编辑、浏览、复制和删除仿真器连接配置。还可以使用此选项连接到任何现有连接配置。

- `Preferences`（首选项）

  此菜单允许您开启或关闭仿真器选项。首选项设置适用于所有 5250 会话。

- `Options`（选项）

  您可以定义密码以防止他人使用 `setup5250` 工具。

- `Help`（帮助）

  使用此菜单获取设置程序的详细说明。

2. 创建新会话

从 `Connection` 菜单栏选择 `New`（新建）。如图 2-4 所示，提供连接描述以及 iSeries 的名称或 IP 地址。

![](img/165c050f45ac58e1635258993855261a_29_0.png)

图 2-4 5250 仿真器连接

随后，在同一面板上，如果您想定义其他选项，点击 `Advanced 5250 Connection` 按钮，如图 2-5 所示：

- `Session title`（会话标题）：显示为会话标题的文本值。
- `Display name`（显示名称）：此文本值决定 IBM i5/OS 中的 5250 显示设备名称。
- `Window size`（窗口大小）：指定 5250 窗口的初始大小和位置。
- `Full screen`（全屏）：勾选此框，5250 窗口将使用整个屏幕。
- `Width`（宽度）：该值决定窗口的像素水平宽度。
- `Height`（高度）：该值决定窗口的像素垂直高度。
- `Horizontal, vertical, and corner offset`（水平、垂直和角偏移）：移动窗口在屏幕上的位置。
- `Bypass sign`（跳过登录）：此选项允许您跳过 IBM i5/OS 登录屏幕。
- `Use Kerberos principal name, no prompting`（使用 Kerberos主体名称，无提示）：启用 Kerberos 身份验证。
- `Emulator User ID`（仿真器用户 ID）：此值用于跳过登录的 IBM/OS 配置文件。
- `Emulator password`（仿真器密码）：该密码经过编码存储并用于跳过登录。
- `Current library`（当前库）：此文本指定跳过登录的当前库。
- `Initial menu`（初始菜单）：允许在跳过登录后指定特定的启动菜单。
- `Initial program`（初始程序）：跳过登录后启动指定的程序。
- `Telnet port`（Telnet 端口）：指定您的 telnet 服务器的 telnet 端口。默认端口为 23。
- `Keymap filename`（键映射文件名）：指定键映射文件的完整路径。
- `Keypad filename`（数字键盘文件名）：指定键盘文件的完整路径。
- `Other parameters`（其他参数）：查看帮助获取更多参数。

![](img/165c050f45ac58e1635258993855261a_30_0.png)

图 2-5 5250 仿真器连接选项

点击 `OK` 按钮创建或提交您的选项。

3. 自定义 5250 仿真器使用 `Preferences` 下拉菜单。`Preferences` 适用于所有仿真器连接，可能会被单独配置覆盖。

在 `Global 5250 preferences` 按钮上，您可以定义如图 2-6 所示的选项（此处未显示）：

- `Keyboard remapping`（键盘映射）：此选项允许您定义 5250 键盘布局。
- `Keypad capability`（数字键盘功能）：此选项允许您创建和使用自定义数字键盘按钮。
- `Record/Playback capability`（记录/播放功能）：此选项允许您在 5250 仿真器中记录并在后播放键序列。
- `Color customization capability`（颜色自定义）：此选项允许您修改 5250 仿真器的颜色。
- `132 Columns`（132 列）：如果启用，则允许 27 行 132 列的屏幕大小。
- `Column separator`（列分隔符）：此值启用或禁用某些 5250 输入字段中的列分隔符。
- `Desktop file`（桌面文件）：此选项决定 5250 仿真器是否存储和使用的位置及字体。
- `Command menu`（命令菜单）：此选项允许您启用或禁用 5250 菜单栏命令项。如果禁用，您将无法访问 5250 会话，且无法通过命令行使用 5250 会话。
- `Edit menu`（编辑菜单）：此选项允许您启用或禁用 5250 菜单栏命令项。（注：OCR 原文中存在大量重复，此处已清理）

Linux 提供了两种主要的 Kerberos 实现版本：MIT 和 Heimdal。大多数 Linux 发行版都至少包含一个版本的 Kerberos。有关 Heimdal 的特定信息，请访问：

`http://www.pdc.kth.se/heimdal/`

请使用以下链接访问 MIT - 马萨诸塞理工学院：

`http://web.mit.edu/kerberos/www/`

要为 Linux 安装并配置 Kerberos，请参考互联网上的许多 How-to 指南。例如 Linux 文档项目：

`http://www.tldp.org/`

## 2.5 Kerberos 的前提条件和配置

以下步骤提供了一个在 Linux 工作站上设置 Kerberos 的示例。我们假设 Kerberos 和 EIM 已在带有 `iSeries Access for Windows` 的 Windows 环境中配置并正常运行。因此，我们使用 Windows Active Directory 服务器作为 Kerberos 服务器。



# iSeries for Linux 与 Kerberos 配置指南

## 1. 环境要求

`iSeries for Linux` 需要 `Kerberos` 版本 5。你可以使用 `Heimdal` 或 `MIT` 的 `Kerberos` 实现。几乎每个 Linux 发行版都包含了至少一种实现性的安装包。

## 2. PAM 认证配置

Linux 还支持使用可插拔认证模块 (`PAM`) `pam_krb` 将 `Kerberos` 作为初始登录方法。在这种情况下，`Kerberos` 用于 Linux 本地密码文件的 Linux 用户认证。对于我们的示例，我们不需要将 Linux 认证更改为 `Kerberos`，但它可以作为你环境中的另一种备用 `Kerberos` 登录方法。如果你计划使用 `pam_krb5`，请参考你发行版中关于设置的文档。

## 3. 必需组件

在 Linux 系统上安装 `Kerberos5` 及其实用工具后，你必须至少拥有以下 `Kerberos` 命令：

- `kinit`
- `klist`
- `kpasswd`

你必须拥有 `Kerberos5` 配置文件，即 `/etc/krb5.conf`。

## 4. 配置文件自定义

`krb5.conf` 包含了基础 `kerberos5` 配置，并要求根据你的环境进行自定义。需要以下关于你的 `Active Directory` 的信息：

- `Kerberos` 术语中的 Windows 登录域：默认 realm (default realm)
- Windows 服务器（域控制器）的 DNS 名称，提供以下功能：密钥分配中心 (`KDC`) 和密码服务器

如果你不确定此配置，可以在 `i5/OS` 现有的 `Kerberos` 配置中进行验证。在 IBM `i5/OS` 上，`Kerberos` 服务被称为网络认证服务 (`NAS`)，设置位于与 Linux 类似的文件中：

```
/IBM/UserData/OS400/NetworkAuthentication/krb5.conf
```

由于 `Kerberos` 和 `EIM` 必须在 IBM `i5/OS` 上已经配置，该文件必须类似于示例 2-4。双问号和括号是括号的替换，将 `??` 替换为 `<` 和 `??`，而双问号和箭头替换大括号，将 `??` 替换为 `<` 和 `>>`。

### 示例 2-4：IBM i/OS Kerberos 配置

```
<libdefaults>
default_keytab = /QIBM/UserData/DS400/NetworkAuthentication/keytab/krb5.keytab
default_realm = \ITSODOMAIN.TEST
<realms>
ITSODOMAIN.TEST = {
kdc = master.itsodomain.test:88
kpasswd_server = master.itsodomain.test:464
}
<domain_realm>
.itso.rbm = ITSODOMAIN.TEST
<capaths>
```

示例 2-4 显示了表 2-2 中使用的设置。

| 表 2-2 IBM i/OS Kerberos 配置设置 | | |
|---|---|---|
| 说明 | 参数 | 值 |
| Kerberos Realm/我们的 Active Directory 名称 | `default_realm` | `ITSODOMAIN.TEST` |
| KDC/我们的 Active Directory 服务器 | `kdc` | `master.itsodomain.test` |
| 密码服务器/与我们的 KDC 服务器相同 | `kpasswd_server` | `master.itsodomain.test` |

## 5. Linux 配置同步

在你的 Linux 系统的配置文件 `/etc/krb5.conf` 中插入你的设置，类似于示例 2-5。按照惯例，`Realm` 始终用大写字母，而 DNS 名称用小写字母。

### 示例 2-5：/etc/krb5.conf 示例

```
[libdefaults]
default_realm = ITSODOMAIN.TEST
clockskew = 300

[realms]
ITSODOMAIN.TEST = {
kdc = master.itsodomain.test
admin_server = master.itsodomain.test
kpasswd_server = master.itsodomain.test
}

[logging]
kdc = FILE:/var/log/krb5kdc.log
admin_server = FILE:/var/log/admin.log
default = FILE:/var/log/krb5libig.log

[appdefaults]
pam = {
ticket_lifetime = 1d
renew_lifetime = 1d
forwardable = true
proxable = false
retain_after_close = false
minimum_uid = 0
}
```

## 6. 域名映射

如果你的 IBM `i/OS` 使用与 Windows 域不同的域名，那么 `Kerberos` 需要知道这一点。在我们的示例中，IBM `i/OS` 在网络中的主机名为：`iseries.ito.ibm.com`，但我们的 `Kerberos Realm` 是 `ITSODOMAIN.TEST`。因此，如果服务器具有 DNS 扩展名 `.ito.ibm.com`，请在 `kerb5.conf` 文件中添加另一个部分以配置 `Kerberos` 使用 `ITSODOMAIN.TEST` 设置：

```
[domain_realm]
.itso.rbm = ITSODOMAIN.TEST
```

## 7. 注意事项

修改 `kerb5.conf` 后，检查以下注意事项：

- `Kerberos` 期望参与的系统具有一致的时间。如果系统之间的时间差超过 300 秒，建议保持低时间差。
- 如果你的 IBM `i/OS` 使用与 Windows 域不同的域名，那么 `Kerberos` 需要知道这一点。在我们的示例中，IBM `i/OS` 在网络中的主机名为 `iseries.ito.ibm.com`，但我们的 `Kerberos Realm` 是 `ITSODOMAIN.TEST`。因此，如果服务器具有 DNS 扩展名 `.ito.ibm.com`，请在 `kerb5.conf` 文件中添加另一个部分配置 `Kerberos` 使用 `ITSODOMAIN.TEST` 设置：

```
[domain_realm]
.itso.rbm = ITSODOMAIN.TEST
```

如果你计划使用 `pam_krb5`，请参考你发行版关于设置的文档。在你的 Linux 系统上安装 `Kerberos5` 及其实用工具后，你必须拥有以下 `Kerberos` 命令：

- `kinit`
- `klist`
- `kpasswd`

你必须拥有 `Kerberos5` 配置文件，即 `/etc/krb5.conf`。

`krb5.conf` 包含了基础 `kerberos5` 配置，并要求根据你的环境进行自定义。需要以下关于你的 `Active Directory` 的信息：

- `Kerberos` 术语中的 Windows 登录域：默认 realm (default realm)
- Windows 服务器（域控制器）的 DNS 名称，提供以下功能：密钥分配中心 (`KDC`) 和密码服务器

如果你不确定此配置，可以在 `i5/OS` 现有的 `Kerberos` 配置中进行验证。在 IBM `i5/OS` 上，`Kerberos` 服务被称为网络认证服务 (`NAS`)，设置位于与 Linux 类似的文件中：

```
/IBM/UserData/OS400/NetworkAuthentication/krb5.conf
```

由于 `Kerberos` 和 `EIM` 必须在 IBM `i5/OS` 上已经配置，该文件必须类似于示例 2-4。双问号和括号是括号的替换，将 `??` 替换为 `<` 和 `??`，而双问号和箭头替换大括号，将 `??` 替换为 `<` 和 `>>`。

### 示例 2-4：IBM i/OS Kerberos 配置

```
<libdefaults>
default_keytab = /QIBM/UserData/DS400/NetworkAuthentication/keytab/krb5.keytab
default_realm = \ITSODOMAIN.TEST
<realms>
ITSODOMAIN.TEST = {
kdc = master.itsodomain.test:88
kpasswd_server = master.itsodomain.test:464
}
<domain_realm>
.itso.rbm = ITSODOMAIN.TEST
<capaths>
```

示例 2-4 显示了表 2-2 中使用的设置。

| 表 2-2 IBM i/OS Kerberos 配置设置 | | |
|---|---|---|
| 说明 | 参数 | 值 |
| Kerberos Realm/我们的 Active Directory 名称 | `default_realm` | `ITSODOMAIN.TEST` |
| KDC/我们的 Active Directory 服务器 | `kdc` | `master.itsodomain.test` |



| 密码服务器/与我们的 KDC 服务器相同 | `kpasswd_server` | `master.itsodomain.test` |

在你的 Linux 系统的配置文件`/etc/krb5.conf`中插入你的设置，类似于示例 2-5。按照惯例，Realm 始终用大写字母，而 DNS 名称用小写字母。

示例 2-5`/etc/krb5.conf`示例

```
[libdefaults]
default_realm = ITSODOMAIN.TEST
clockskew = 300

[realms]
ITSODOMAIN.TEST = {
kdc = master.itsodomain.test
admin_server = master.itsodomain.test
kpasswd_server = master.itsodomain.test
}

[logging]
kdc = FILE:/var/log/krb5kdc.log
admin_server = FILE:/var/log/admin.log
default = FILE:/var/log/krb5libig.log

[appdefaults]
pam = {
ticket_lifetime = 1d
renew_lifetime = 1d
forwardable = true
proxable = false
retain_after_close = false
minimum_uid = 0
}
```

如果你的 IBM i/OS 使用与 Windows 域不同的域名，那么 Kerberos 需要知道这一点。在我们的示例中，IBM i/OS 在网络中的主机名为`iseries.ito.ibm.com`，但我们的 Kerberos Realm 是`ITSODOMAIN.TEST`。因此，如果服务器具有 DNS 扩展名`.ito.ibm.com`，请在`kerb5.conf`文件中添加另一个部分以配置 Kerberos 使用`ITSODOMAIN.TEST`设置：

```
[domain_realm]
.itso.rbm = ITSODOMAIN.TEST
```

修改`kerb5.conf`后，检查以下注意事项：

Kerberos 期望参与的系统具有一致的时间。如果系统之间的时间差超过 300 秒，我们建议保持低时间差。

如果你的 IBM i/OS 使用与 Windows 域不同的域名，那么 Kerberos 需要知道这一点。在我们的示例中，IBM i/OS 在网络中的主机名为`iseries.ito.ibm.com`，但我们的 Kerberos Realm 是`ITSODOMAIN.TEST`。因此，如果服务器具有 DNS 扩展名`.ito.ibm.com`，请在`kerb5.conf`文件中添加另一个部分配置 Kerberos 使用`ITSODOMAIN.TEST`设置：

```
[domain_realm]
.itso.rbm = ITSODOMAIN.TEST
```

如果你计划使用`pam_krb5`，请参考你发行版关于设置的文档。在你的 Linux 系统上安装 Kerberos5 及其实用工具后，你必须拥有以下 Kerberos 命令：

- `kinit`
- `klist`
- `kpasswd`

你必须拥有 Kerberos5 配置文件，即`/etc/krb5.conf`。

`krb5.conf`包含了基础 kerberos5 配置，并要求根据你的环境进行自定义。需要以下关于你的 Active Directory 的信息：

- Kerberos 术语中的 Windows 登录域：默认 realm (`default realm`)
- Windows 服务器（域控制器）的 DNS 名称，提供以下功能：密钥分配中心 (KDC) 和密码服务器

如果你不确定此配置，可以在 i5/OS 现有的 Kerberos 配置中进行验证。在 IBM i5/OS 上，Kerberos 服务被称为网络认证服务 (NAS)，设置位于与 Linux 类似的文件中：

```
/IBM/UserData/OS400/NetworkAuthentication/krb5.conf
```

由于 Kerberos 和 EIM 必须在 IBM i5/OS 上已经配置，该文件必须类似于示例 2-4。双问号和括号是括号的替换，将`??`替换为`<`和`??`，而双问号和箭头替换大括号，将`??`替换为`<`和`>>`。

## 示例 2-4：IBM i/OS Kerberos 配置

```
<libdefaults>
default_keytab = /QIBM/UserData/DS400/NetworkAuthentication/keytab/krb5.keytab
default_realm = \ITSODOMAIN.TEST
<realms>
ITSODOMAIN.TEST = {
kdc = master.itsodomain.test:88
kpasswd_server = master.itsodomain.test:464
}
<domain_realm>
.itso.rbm = ITSODOMAIN.TEST
<capaths>
```

示例 2-4 显示了表 2-2 中使用的设置。

| 表 2-2 IBM i/OS Kerberos 配置设置 | | |
|---|---|---|
| 说明 | 参数 | 值 |
| Kerberos Realm/我们的 Active Directory 名称 | `default_realm` | `ITSODOMAIN.TEST` |
| KDC/我们的 Active Directory 服务器 | `kdc` | `master.itsodomain.test` |
| 密码服务器/与我们的 KDC 服务器相同 | `kpasswd_server` | `master.itsodomain.test` |

## 2.5.2 使用 Kerberos 登录

配置完成后，你必须能够使用`kinit`命令成功对域进行认证。由于我们使用 Windows Active Directory，你的登录名是 Windows 用户。

```
linux:~ kinit windowouser
Password for windowouser@ITSODOMAIN.TEST.
```

如果你没有收到进一步的消息或关于票据寿命的信息，说明对域的认证成功。如果你在 Linux 上使用了 Kerberos 可插拔模块，你必须已经有一个 Kerberos 票据。使用命令`klist`验证你获得了票据：

```
linux:~ klist
Ticket cache: FILE:/tmp/krb5cc_1000
Default principal: windowouser@ITSODOMAIN.TEST
```

| 有效开始时间 | 过期时间 | 服务主体 |
|---|---|---|
| 08/01/05 20:01:00 | 08/02/05 06:01:00 | `krbtgt@ITSODOMAIN.TEST` |

要在不登录的情况下打开 5250 会话，你必须有一个 EIM 标识符，它将 Windows 用户名映射到 IBM/OS 用户配置文件。

使用命令`ibm5250`配合参数`-kerberos -sso`打开 5250 会话。`-kerberos`标志针对主机服务器验证用户，而`-sso`切换此认证以跳过登录：

```
/opt/ibm/iSeriesAccess/bin/ibm5250 iseries.ito.ibm.com -kerberos -sso
```

## 2.5.3 iSeries Access for Linux 支持 Kerberos

从版本 1.10 开始，iSeries Access for Linux 支持 Kerberos。包括所有命令行工具和用于 5250 仿真的 ODBC 驱动程序。要使用 Kerberos，如示例 2-6 所示，将 iSeries 用户名替换为 "kerberos"。示例 2-6 使用 Kerberos 的`rmcmd`

```
linux:~ /opt/ibm/iSeriesAccess/bin/rmcmd CRTLIB SSOTEST
system:iSeries.ito.ibm.com /user*:kerberos
```

远程系统名称为`iseries.itso.ibm.com`。

CPC2102 - 库 SSOTEST 已创建。

即使在 ODBC 数据源名称 (DSN) 中，也允许 Kerberos 用户名。这意味着每个 ODBC 应用程序都可以获得 Kerberos 单点登录的优势。

# 2 使用安全套接层 (SSL) 加密连接

如果你使用如 Kerberos 等安全登录方法，5250 Telnet 连接仍然未加密。这意味着能够访问网络环境的人员可以轻松地监控并更改每条输入数据和屏幕数据。为了防止网络中任何未经授权的数据访问，发明了安全套接层 (SSL) 协议。它提供了数据加密、完整性保护，并支持客户端和服务器的身份验证。



iSeries Access for Linux 可以通过 Linux 隧道利用 iSeries 的优势。

对于 SSL 通信，你必须为你想要使用的每个 IBM i/OS TCP/IP 服务器或主机应用证书。否则，SSL TCP/IP 端口将不可用。如何设置公/私有基础设施在 iSeries Infocenter 的“Security -> Secure Sockets Layer”下描述：

```
http://publib.ibm.com/pubs/html/a500/
```

程序隧道在服务器和客户端之间建立一个 SSL 隧道。在这种情况下，`stunnel` 连接到 IBM i/OS Telnet 端口，将加密数据传输到 Linux 客户端，进行解密并为本地应用程序提供 telnet 流。`ibm5250` 不是连接到 IBM i/OS，而是连接到 localhost 的 SSL 隧道末端。

见图 2-7：隧道建立后，Linux 客户端上的每个用户都可以使用它。相同的场景也适用于 ODBC 等主机服务器连接。

![](img/165c050f45ac58e1635258993855261a_38_0.png)

图 2-7 Stunnel 连接

`stunnel` 命令从文件中读取其配置。该文件的结构非常简单。首先指定你使用隧道的客户端方法。然后为你你想要连接的每个 SSL 服务添加一个章节：

- 服务名称：`[service]`
- 本地 IP 地址和端口：`accept = localIPAddress:localPort`
- 远程 IP 地址和端口：`connect = remoteHost:remotePort`

示例 2-7 提供了一个配置示例。

示例 2-7 Stunnel 配置文件：`stunnel.conf`

```conf
## 启用客户端模式
client = yes

## Debug 和 Foreground 用于测试 / 取消注释以调试 stunnel 问题
##debug = 5
#foreground = yes

## Services：这些章节包含用于 iSeries Access 连接的端口映射。

## 用于 5250 Telnet 模拟，ibm5250
[telnet]
accept = 127.0.0.2:23
connect = iseries.itbo.com:992

## 用于许可和转换表 (ibm5250, cwbnltbl)
[as-central]
accept = 127.0.0.2:8470
connect = iseries.itbo.com:9470

## 用于 ODBC (rdmtdoc, cwbrunsq, isql, DataManager, ...)
[as-database]
accept = 127.0.0.2:8471
connect = iseries.itbo.com:9471

## 用于远程命令 (rmtcmd)
[as-rmtcmd]
accept = 127.0.0.2:8475
connect = iseries.itbo.com:9475

## 用于 SSO 登录
[as-signon]
accept = 127.0.0.2:8476
connect = iseries.itbo.com:9476
```

首次使用 `stunnel` 时，你可以取消注释 `foreground = yes` 行，并使用命令 `stunnel stunnel.conf` 以 `root` 身份启动 SSL 隧道。使用 `ibm5250 127.0.0.2` 开启一个 5250 会话。如果一切工作运行正常，你将看到类似于示例 2-8 的 `stunnel` 输出。

示例 2-8 通过隧道成功连接的输出

```
root@linux:~ stunnel tunnel.config
2005.08.01 LOG[]: stunnel 4.07 on i686-6-linux-gnu PTHREAD+POLL+IPv4 with
OpenSSL 0.9.7e 25 Oct 2004
2005.08.01 LOG[]: 5 clients allowed
2005.08.01 LOG[]: as-central connected from 127.0.0.2:21774
2005.08.01 LOG[]: Connection closed: 783 bytes sent to SSL, 215 bytes sent to
socket
2005.08.01 LOG[]: telnet connected from 127.0.0.2:2218
```

此配置在 Linux 和 IBM/OS 之间建立了加密连接，但它并不能证明远程计算机是你想要连接的 IBM/OS。为了防止所谓的“中间人攻击”，隧道可以使用证书验证远程服务器。在建立 SSL 连接期间，服务器会向客户端提供其证书，以便客户端可以验证其真实性。在许多 IBM/OS 上，使用的是签名证书。这意味着 IBM/OS 也是证书颁发机构 (CA)。

如果使用自签名证书，隧道可以使用证书来验证远程服务器。在建立 SSL 连接期间，服务器将将其证书提供给客户端，以便客户端可以验证其真实性。在许多 IBM/OS 上，使用的是签名证书。这意味着 IBM/OS 也是证书颁发机构 (CA)。

如果使用自签名证书，证书存储在 IBM/OS 的集成文件系统 (IFS) 中。如何设置公/私有基础设施在 iSeries Infocenter 的“Security -> Secure Sockets Layer”下描述：

（注：此处原文文本存在部分乱序重复，翻译已根据逻辑语义进行处理）

## 通过 ODBC 连接 IBM i5/OS

适用于 Linux 的 iSeries Access 数据库连接 (ODBC) 驱动程序允许您从任何编写为 ODBC 应用程序编程接口 (API) 的 Linux 应用程序访问 iSeries 的 DB2 通用数据库 (UDB)。它是一个 ODBC 3.5 美国国家标准协会 (ANSI) 驱动程序，具有存储和处理 Unicode 数据的能力。与 Windows 版 iSeries Access ODBC 驱动程序类似，它使用传输控制协议/网协议 (TCP/IP) 套接到数据库服务器以访问 IBM i5/OS 的数据。

ODBC 驱动程序包含在 iSeries Access for Linux 软件包中。有关产品安装的信息，请参阅第 10 页第 2.3 节“安装 iSeries Access for Linux”。

使用此 Linux 应用程序驱动程序访问存储在 IBM i5/OS 侧数据的示例包括：

- 集成 iSeries DB2 UDB 数据库的 `OpenODBC` 应用程序
- `DataManagerII` 是用于查看和管理数据源的图形用户界面 (GUI) 应用程序
- 命令行应用程序（如 `iSQL`），用于交互式结构化查询语言 (SQL) 请求
- `cwbrunsq1`，用于运行批 SQL 脚本
- 提供各种 Web 页面服务的 PHP 超文本预处理器 (PHP) 应用程序
- 使用 C 或 Perl 编写的简单 ODBC 应用程序

## 3.1 ODBC 配置

作为 iSeries for Linux 部分的 ODBC 驱动程序的安装将在第 5 页第 2 节“iSeries Access for Linux”中讨论。请勿使用过时的 Red Hat 包管理器 (RPM) iSeries ODBC 驱动程序。该驱动程序的后续版本包含在 iSeries Access for Linux 中。

配置 iSeries Access ODBC 驱动程序有两种方法：使用如 `ODBCConfig` 等图形化工具或编辑 `odbc.ini` 文件。GUI 工具 `ODBCConfig` 紧密参考了 Microsoft ODBC 管理器，对于在 Microsoft 环境下使用 ODBC 的人员来说，它是最佳选择。

您还必须选择数据源类型 DNS。DSN 可以是用户 DSN 也可以是系统 DSN。用户 DSN 存储在创建 DSN 的用户主目录下的 `~/odbc.ini` 中，例如 `/home/itsouser/odbc.ini`。它们只能由创建它们的的用户访问。系统 DSN 只能由 `root` 配置，并存储在 `/etc/unixODBC/odbc.ini` 文件中，系统所有用户均可访问。位置在不同的 Linux 发行版中有所不同。使用以下命令获取系统上 unixODBC 配置文件的信息：

```
linux:> dbinst -j
unixODBC 2.2.11
DRIVERS:... /etc/unixODBC/odbc.ini
SYSTEM DATA SOURCES: /etc/unixODBC/odbc.ini
USER DATA SOURCES:... /root/odbc.ini
```

### 3.1.1 ODBCConfig: ODBC 配置的 GUI 方法

可以使用 ODBC 数据源 GUI 配置数据源。该 GUI 包含设置所需和常用选项的字段。以下指令说明了如何创建或配置 iSeries Access ODBC 驱动程序 - DSN。



> 注意：如果想使用 `ODBCConfig`（或您的 Linux 发行版可能使用的名称），则可能需要安装它。在 Novell SUSE 发行版中，`ODBCConfig` 工具包含在 `unixODBC-gui-qt` 中。Red Hat 在 `unixODBC-kde` 中提供 `ODBCConfig`。您的发行版可能有不同的包名或类似的工具如 `goODBC`。

执行以下步骤：

1. 在图形会话中，在 Linux 终端中使用命令 `ODBCConfig` 打开数据源管理员，或使用开始菜单 → 运行命令：

```
linux:> ODBCConfig
```

2. 决定您想要使用的数据源类型。

用户 DSN 仅由创建它们的用户访问。系统 DSN 可由机器上的任何用户访问。

系统 DSN 由 `root` 用户配置。

在所使用的示例中，点击“User DSN”以如图 3-1 所示创建一个新的用户 DSN。

![](img/165c050f45ac8e1635289931a_0.png)

图 3-1 数据源管理员

3. 在图 3-1 中，点击“Add”创建一个新的数据源，如果想配置已存在的数据源。

![](img/165c050f45ac8e1635289931a_1.png)

图 3-2 添加

4. 选择 iSeries ODBC 驱动程序。

5. 配置 DSN 属性。默认值均有效。在 `System` 字段输入数据源名称。如图 3-3 所示的 DSN 示例。在 `Name` 字段输入系统名称。

![](img/165c050f45ac8e1635289931a_2.png)

图 3-3 ODBC 配置

6. 然后，如图 3-4 所示的数据源窗口显示新的 DSN。点击 `OK` 按钮。

![](img/165c050f45ac8e1635289931a_3.png)

图 3-4 OK

### 3.1.2 编辑 `odbc.ini`: ODBC 配置的文本模式

某些驱动选项无法通过 `ODBCConfig` 使用。如果想使用它们，必须编辑 `odbc.ini` 文件。

> 注意：很容易在同一个文件中输入两次条目。例如，`Trace=0` 并在同一个文件中具有多个条目会导致不可预测的行为。

执行以下步骤：

1. 使用 `dbinst -j` 命令定位 `odbc.ini` 文件。使用您喜欢的文本编辑器编辑该文件，内容如示例 3-1 所示。

示例 3-1 编辑 `.ini`

| User | DSN |
| :--- | :--- |
| Description | |
| Driver | iSeries Access Driver |
| System | iSeries.itso.com |
| UserID | |
| Password | |
| Naming | 0 |
| DefaultLibraries | QPL |
| Database | |
| ConnectionType | 0 |
| CommitMode | 2 |
| ExtendedDynamic | 1 |
| DefaultPkgLibrary | QG |
| DefaultPackage | A/DEFAULT(IBM),2,0,1,0,512 |
| AllowDataCompression | 1 |
| LibraryView | 0 |
| AllowUnsupportedChar | 0 |
| ForceTranslation | 0 |
| Trace | 0 |
| DFT | 1 |

2. 您可以在最后一个条目之后添加行。例如，默认日期格式为 1，如示例 3-2 所示。

示例 3-2 更改连接选项

| User | |
| :--- | :--- |
| Description | |
| Driver | iSeries Access Driver |
| System | iSeries.itso.com |
| UserID | |
| Password | |
| Naming | 0 |
| DefaultLibraries | QIWS |

```
Database =
ConnectionType = 0
CommitMode = 2
ExtendedDynamic = 1
DefaultPkgLibrary = QG
DefaultPackage = A/DEFAULT(IBM),2,0,1,0,512
AllowDataCompression = 1
LibraryView = 0
AllowUnsupportedChar = 0
ForceTranslation = 0
Trace = 0
DFT = 1
```

## 3.2 数据访问工具和实用程序

有一些使用 iSeries ODBC 驱动程序访问存储在 `DB2 UDB for iSeries` 中的数据的可用工具和实用程序。本节涵盖了：

- 使用 `ISQL`

这是随 `unixODBC` 提供的小型应用程序，对于测试查询或以批模式提取到分隔符文件非常有用。它还可以用于生成封装在超文本标记语言 (`HTML`) 中的结果。

- 使用 `cwbrunsql`

`iSeries Access for Linux` 附有一个名为 `cwbrunsql` 的工具，它也允许批处理 `SQL` 脚本。

- `DataManager`

这是一个允许用户查看和管理数据源的 GUI 应用程序。它随 `unixODBC` 驱动管理器包提供。

### 3.2.1 ISQL

`ISQL` 是一个 `unixODBC` 程序，提供了交互模式和批处理的 `SQL` 接口。

本节演示如何使用 `ISQL`。

请执行以下步骤：

1. 使用数据源名称（Data Source Name）以及 `IBM i5/OS` 用户名和密码连接数据库，如示例 3-3 所示。

示例 3-3 使用 `ISQL` 连接到 `DB2 for iSeries`

```
linux:> iSeries DB2 ITSouser password
+------------------------------------------------------+
| Connected!                               |
| sql-statement                           |
| help [tablename]                        |
| quit                                |
+------------------------------------------------------+
SQL>
```

2. 这将你带 `ISQL` 提示符，可以在其中执行 `SQL` 命令。执行以下查询：

```sql
select * from qiws.qusccdct
```

参见示例 3-4。

示例 3-4 执行 `SQL` 语句 `select * qiws.qusccdct`

| CUSNUM | LSTNAM | INIT | STREET | CITY | STATE | ZIPCODE | CDTLMT | CHCGOD | BALDUE | CDTUE |
|---|---|---|---|---|---|---|---|---|---|---|
| 938472 | Henning | G K | 485 Elm Ave | Dallas | TX | 75217 | 5000 | 3 | 37.00 | 0 |
| 839283 | Jones | B D | 218 NW 135 St | Clay | NY | 13041 | 400 | 1 | 100.00 | 0 |
| 932859 | Vine | S S | PO Box 79 | Brayton | VT | 50460 | 700 | 1 | 439.00 | 0 |
| 938465 | Johnson | J A | 3 Alpine Way | Helen | GA | 30545 | 9999 | 2 | 3987.50 | 33.50 |
| 939267 | Byron | W E | 12 Myrtle Dr | Denver | CO | 80226 | 1000 | 1 | 0 | 0 |
| 839572 | Stevens | L C | 208 Snow Pass | Dexter | NY | 14824 | 0 | 56.75 | 1.50 |
| 846283 | Allison | J S | 787 Lake Id | Isle | MN | 56420 | 5000 | 3 | 10.00 | 0 |
| 475938 | Doe | J W | 59 Archer Rd | Sutter | CA | 95685 | 7000 | 2 | 250.00 | 100.00 |
| 693829 | Thomas | A N | 3 Circle Court | Casper | WY | 82609 | 9999 | 2 | 0 | 0 |



| 593029 | Williams | E D | 48 SE 2 Ave | Dallas | TX | 75218 | 2000 | 1 | 25.00 | 0 |

| 192837 | Lee | F L | 5963 Oak St | Hector | NY | 14841 | 700 | 2 | 489.50 | .50 |

| 583990 | Abraham | M T | 392 Mill St | Isle | MN | 56342 | 9999 | 3 | 500.00 | 0 |

```
SQLRowCount returns -1

12 rows fetched

SQL quit

linux:>
```

3. 示例 3-5 显示了 `isql` 在批处理模式下的用法。通过参数 `-b` 开启批处理模式，参数 `-w` 启用 HTML 输出。这次查询来自文件 `batch.sql`，结果写入 `address.html`。

示例 3-5: ISQL- 在批处理模式下运行查询

```
linux:>- echo "select cusnum, lstnam, city from qiws.cusctcdt order by lstnam" 

> batch.sql
```

```
linux:>- cat batch.sql | isql iSeriesDB ITSOuter password -b -w > address.html

linux:>
```

4. 该查询结果被格式化为 HTML 表格，即发送到 `address.html` 的文件。表 3-1 展示了生成的表格。

| CUSNAM | LSTNAM | CITY |
| --- | --- | --- |
| 583990 | Abraham | Isle |
| 846283 | Allison | Isle |
| 475938 | Doe | Sutter |
| 938472 | Henning | Dallas |
| 938485 | Johnson | Helen |
| 839283 | Jones | Clay |
| 192837 | Lee | Hector |
| 389572 | Stevens | Denver |
| 693829 | Thomas | Casper |
| 397267 | Tyron | Hector |
| 392859 | Vine | Broton |
| 593029 | Williams | Dallas |

5. 在某些情况下，可能需要逗号分隔文件（CSV）来供非 ODBC 应用程序进一步处理。`isql` 使用分隔符导出数据到文件，列名通过 `-c` 添加到文件顶部：

```
echo "select * from qiws.cusctcdt" | isql iSeriesDB ITSOuter password -b -c cust.csv
```

注意：对于更复杂的查询，可以使用 IBM i/OS 上创建的数据库 (`dbsample`)。DB2 for iSeries 自带示例表。

### 3.2.2 cwbrunsql

iSeries Access for Linux 带有一个 `cwbrunsql` 工具，允许在批处理模式下运行 SQL 脚本。它没有提供交互式 shell。你可以配合现有的 DSN 使用 `cwbrunsql`，其中 `iSeriesDB` 是 DSN，`itsouser` 是 IBM i/OS 用户：

```
cwbrunsql/DSN:iSeriesDB /USER:itsouser/PASSWORD:batch.sql
```

另一方面，你可以在不使用 DSN 但使用 IBM i/OS 主机名的情况下使用 `cwbrunsql`：

```
cwbrunsql/SYSTEM:iseries.com/USER:itsouser/PASSWORD:batch.sql
```

使用参数指定 SQL 批文件——使用了与示例 3-5 相同的批文件。结果包含了额外数据，如 IBM i/OS 作业。由于存在错误消息，该工具有助于判断问题。

示例 3-6: cwbrunsql example iSeries Access for Linux

```
****************************************************************

Connected to system: ISERIES.IT.COM

Job information: QZDOSASINTQUER 070673

****************************************************************

STATEMENT 1
```

```sql
select column, lstnam, city from qiws.cus order by lstnam
```

```
"CUSNUM", "LISTNAM", "CITY"

583990, "Abraham" "Isle"

846283, "Allison" "Isle"

47538, "Doe" "Sutter"

93842, "Henning" "Dallas"

93845, "Johnson" "Helen"

839283, "Jones" "Clay"

192837, "Lee" "Hector"

389572, "Stevens" "Denver"

693829, "Thomas" "Casper"

397267, "Tyron" "Hector"

392858, "Vine" "Brockton"

59302, "Williams", "Dallas"
```



12 rows fetched
*** 执行此语句的近似时间：36 毫秒 ***

### 3.2.3 DataManagerII

`DataManagerII` 包含在 `unixODBC` 中，是一个探索数据源的图形工具。它允许以类似于文件系统的方式探索数据源。

以下是使用 `unixODBC` `DataManagerII` 的步骤：

1. 在图形会话中，在 Linux 终端打开 `DataManagerII` 或使用开始菜单 → 运行：
   `linux:> DataManagerII`

2. 打开现有数据源并登录 `IBM i5/OS`，如图 3-5 所示。

   ![img/165c050f45ac58e1635258993855261a_51_0.png]

3. `DataManagerII` 有两个窗格。左格显示树视图。在此视图中，你可以看到表、限制键、索引和视图等元素。

   右格是详细视图。它显示所选项目的任何详细信息。在此视图中，你也可以执行 `SQL` 命令进行查询。如图 3-6 所示编写 `SQL` 查询。点击运行执行查询。

   ![img/165c050f45ac58e1635258993855261a_51_1.png]

## 3.3 通过 OpenOffice.org 访问 iSeries DB2 UDB

`OpenOffice.org` 是一个类似于 `StarOffice` 的开源办公套件。`OpenOffice.org` 项目最初由 `Sun` `StarOffice` 项目提供。`OpenOffice.org` 和 `Sun` 的 `StarOffice` 功能上非常相似，都包含了文字处理、电子表格和演示应用程序。`StarOffice` 已在 `iSeries Access DB for Linux` 上通过测试，但为了演示，我们使用开源的 `OpenOffice.org`。电子表格包含大量与 `MS Excel` 相同的功能，包括通过 `ODBC` 查询远程数据库的能力。本节描述了使用 `OpenOffice.org` 电子表格从 `DB2 UDB` 提取数据。

### 3.3.1 要求

必须安装最新版本的 `OpenOffice.org` 1.1.x 或 2。如果你的 Linux 发行版未包含 `OpenOffice`，你可以下载 `x86` 或 `PPC` 版本的 Linux。安装说明、程序代码和其他文档请参阅：

<http://www.openoffice.org/>

### 3.3.2 在 OpenOffice.org 中导入 DB2 UDB for iSeries 数据

`OpenOffice.org` 具有从 `ODBC` 数据源导入数据的能力。以下步骤提供了数据导入示例。我们使用了 `OpenOffice.org` 1.1.3。

1. 在图形会话中，使用命令 `office` 打开 `OpenOffice`。
2. 选择文件 -> 新 -> 电子表格。

   > 注意：从版本 2.0 开始，`OpenOffice` 包含了自己的数据库模块。要在版本 2.0 中配置 `ODBC` 连接的数据源，请使用数据库向导，文件 -> 新建 -> 数据库。

3. 选择工具 -> 数据源。
   `OpenOffice` 数据源管理窗口打开。此窗口帮助你配置 `OpenOffice` 数据源。此新数据源仅供 `OpenOffice` 使用。

   参见图 3-7。

   ![](img/165c050f45ac58e1635258993855261a_53_0.png)

   图 3-7 OpenOffice 数据源配置

4. 在与图 3-7 所示类似的窗口中，执行以下步骤：
   a. 点击左角的“新建数据源”（New Data Source）按钮。
      `OpenOffice` 数据源列表中将显示数据源 1。
   b. 为新数据源命名，在本例中，本书使用的名称为 `iSeriesDB over ODBC`。再次强调，此数据源仅供 `OpenOffice` 使用。
   c. 将数据库类型（Database type）更改为 `ODBC`。
   d. 在数据源 URL（Data source URL）参数中，有一个用“...”表示的按钮。点击它，将显示你在 `ODBCConfig` 中配置的 `DSN` 列表。
   e. 选择为访问 `iSeries` 数据库而配置的 `DSN` 并点击确定。在本例中，我们选择了 `DSN iSeriesDBAllUser`。
   f. 在 `ODBC` 选项卡上，你必须输入 `i/OS` 用户配置并勾选“需要密码”（Password required）框。你可以查看其他配置选项，但没有必要更改。点击确定配置数据源。
5. 现在你准备好将数据导入电子表格。点击数据（Data）→ `DataPilot` → 开始（Start）。
6. 打开“选择源”（Select Source）窗口。选择“OpenOffice.org 注册的数据源”（Data source registered in OpenOffice.org）并点击确定。
7. 将数据库（Database）更改为数据源。
8. 对于数据源参数，从列表中选择一个表。
   如果列表中 `QCQUSTED`，请选择它。

   > 注意：你看到的表列表是默认集合。默认集合由你作业的 `IBM i5/OS` 库（基于你的 `iSeries` 用户配置）以及你在 `unixODBC` 中通过 `ODBCConfig` 配置的默认库组成。

40 Linux 与 IBM i5/OS 集

9. 点击确定。
   现在进入了 `DataPilot` 屏幕。此屏幕允许你选择字段并将其放置在所需的位置。参见图 3-8。

   ![](img/165c050f45ac58e1635258993855261a_54_0.png)

   左键点击并将字段从右侧拖到行（Row）或列（Column）区域。完成后，点击确定。
   你必须有一个存储了 `DB2 UDB for iSeries` 数据的电子表格，将其保存为任何 `OpenOffice` 数据类型。

### 3.3.3 直接链接到 DB2 UDB for iSeries 

访问 `DB2 UDB for iSeries` 的另一种方法位于菜单视图（View）-> 数据源（Data Sources）或在任何 `OpenOffice` 程序中使用 `F4` 键。此外，你获得的窗口可以直接访问你的数据源。这允许你在不导入电子表格的情况下浏览、排序、复制或编辑数据。你可以使用工具（Tools）-> 邮件合并（Mail Merge）功能为 `IBM i/OS` 地址数据库生成个性化邮件。图 3-9 显示了 `Open Writer` 中的数据源视图。

![](img/165c050f45ac58e1635258993855261a_54_1.png)

图 3-9 带有数据源视图的 OpenOffice Writer

注意：`OpenOffice` 要求数据库文件具有主键以便编辑数据。如果没有主键，表将以只读方式打开。你可以通过 `iSeries Navigator` 或通过 `SQL` 使用以下命令添加主键：

```sql
ALTER TABLE tableName PRIMARY KEY (field)
```

## 3.4 编写 ODBC 

有许多编写 Linux 应用程序来访问 `IBM i/OS` 数据库的方法。本节提供了 `ODBC` 编程的概述，并带有小型示例代码演示了 `unixODBC API` 的用法。本节介绍了以下场景：

- 客户端服务器：使用 `C` 应用程序可以通过 Linux 版 `iSeries Access ODBC` 驱动程序从后端 `i/OS` 获取普通的数据库文件。
- 三层架构：这些在网页中很常见。它们使用提供内置 `ODBC` 函数并访问 `iSeries DB2` 的 `PHP` 模块。
- 使用 `Perl` 建立数据库连接

## 3.1 用 C 编写的客户端应用程序

`ODBCExample.c` 是一个示例程序，它使用 Linux 版 `iSeries Access ODBC` 驱动程序从后端 `i/OS` 获取普通的数据库文件 (`QIWS/QCUSTCDT`)。

此示例假设已安装 `unixODBC` 和 Linux 版 `iSeries Access ODBC` 驱动程序。目标 `i/OS` 数据库必须在 `unixODBC` 中注册为数据源。编译时，你可能还需要 `unixODBC-dev` 包。编译此程序的命令为：

```bash
linux:~$ gcc -o ODBCExample -lodbc ODBCExample.c
```

`-o` 切换输出可执行文件。`-lodbc` 切换链接 `ODBC` 库。`ODBCExample` 的源代码在示例 3-7 中。

示例 3-7 ODBCExample.c 源代码

```c
/* 适用于 Linux 的简单 ODBC 示例
参数：datasource（你的系统或用户 DSN 名称）
UserID
password
示例: ODBCexample datasource UserID password
Rochester, MN, 2005年7月 */

#include <sql.h>
#include <stdio.h>
#include <stdlib.h>

/* 对极可能存在的 DB 表进行简单查询。获取第一个 i/OS "成员" * */
```



`char querystring[] = "SELECT * FROM QIWS.QCUSTDT";`

```c
/* 此处定义了 die 函数用于处理错误 */
SQLRETURN code;

void die(char *reason, SQLRETURN code) {
    if (code != 0) {
        printf("Error code: %d\n", code);
    }
    printf("Failure: %s\n", reason);
    exit(1);
}

int main(int argc, char *argv[]){
    #define MAX_CONNECTIONS 5

    char field1[255]; /* 从行接收 */
    char field2[255];
    char field3[255];

    SQLINTEGER ret1; /* 为了完整性 */
    SQLINTEGER ret2; /* 为了 NULL */
    SQLINTEGER ret3; /* 足够了 */

    SQLHENV henv;
    SQLHDBC hdbc[MAX_CONNECTIONS]; /* 多个连接 */
    SQLHST statement;
    SQLRETURN sqle = 0;
    SQLRETURN res = 0;

    /* 分配环境 */
    if (SQLAllocEnv(&henv))
    die("Alloc Environment", 0);

    /* 分配连接 */
    if ((sqle = SQLAllocConnect(henv, &hdbc[0]))
    die("Alloc Connect", sqle);

    /* 连接数据 */
    if ((sqle = SQLConnect(hdbc[0], argv[1], SQL_NTS, argv[2], SQL_NTS, argv[3], SQL_NTS))
    die("Connect", sqle);

    /* 分配语句 */
    if (SQLAllocStmt(hdbc[0], &statement))
    die("Alloc stmt", 0);

    /* 执行查询 */
    if ((sqle = SQLExecDirect(statement, querystring, SQL_NTS))
    die("exec direct", sqle);

    /* 绑定字段 */
    if ((sqle = SQLBindCol(statement, 1, SQL_CHAR, field1, 255, &ret1))
    die("Bind field 1", sqle);

    if ((sqle = SQLBindCol(statement, 2, SQL_CHAR, field2, 255, &ret2))
    die("Bind field 2", sqle);

    if ((sqle = SQLBindCol(statement, 3, SQL_CHAR, field3, 255, &ret3))
    die("Bind 3", sqle);

    /* 循环获取所有记录 */
    res = SQLFetch(statement);

    /* field1,2,3 每次获取新值 */
    while (SQL_SUCCEED(res)) {
      /* 创建制表符分隔的值 */
      printf("%s\t%s\t%s\n", field1, field2, field3);
      res = SQLFetch(statement); /* 下一条记录 */
    }

    /* 完全结束处理 */
    /* 释放语句 */
    if (SQLFreeStmt(statement, SQL_DROP))
    die("Free Statement", 0);

    /* 关闭连接 */
    if ((sqle = SQLDisconnect(hdbc[0]))
    die("Disconnect", sqle);

    if ((sqle = SQLFreeConnect(hdbc[0]))
    die("Connection closed", sqle);

    /* 释放环境 */
    if (SQLFreeEnv(henv))
    die("Free Environment", 0);

    printf("Success!");

    return 0;
}
```

运行 `ODBC`，请使用示例 3-8 所示的命令，`iSeriesDB` 是 `DSN`，`itsouser` 是 `i/OS` 用户配置，`password` 是该用户的密码。

示例 3-8 运行 `testODBC` 程序

```bash
linux:"> ./ODBCexample iSeries itsouser password
938472 Henning G K
839283 Jones B D
392859 Vine S S
938485 Johnson J A
397267 Tyron W E
389572 Stevens K L
846263 Allison J S
475938 Doe J W
693829 Thomas A N
593029 Williams E D
192837 Lee F L
583990 Abraham M T
Success!
linux:">
```



## 3.4.2 用于三层应用的 PHP

PHP 代表 PHP Hypertext Preprocessor（PHP 处理器）。PHP 是一种广泛使用的通用脚本语言，特别适用于 Web 开发。它通常嵌入 HTML 中。

PHP 主要关注服务器端脚本，因此你可以执行任何其他通用网关 (CGI) 程序可以做的操作，例如收集表单数据、生成动态页面内容或发送和接收 cookie。

PHP 模块提供了带有 unixODBC 支持的内置 ODBC 函数。它可以使用 Linux 版 iSeries ODBC 驱动程序访问 DB2 UDB for iSeries。

## PHP 概述

图 30 描述了整个过程。当 Apache Web 服务器从客户端浏览器接收 PHP 请求时，它会将请求转发给 PHP 模块。PHP 模块随后找到请求的 PHP 页面的源码并解释并执行该源码。如果 PHP 模块在源码中找到数据库访问函数，它将调用 Linux 版 iSeries ODBC 驱动程序访问 DB2 UDB for iSeries 并执行相关的 SQL 语句。ODBC 驱动程序将数据集返回给 PHP 模块。PHP 模块随后将结果数据嵌入 HTML 标签和其他内容，并将其转发给 Apache 服务器。Apache 将 HTML 页面发送到客户端浏览器。

![](img/165c050f45ac58e1635258993855261a_58_0.png)

图 30 Linux 系统上带有 ODBC 驱动程序的 Apache 和 PHP

# 使用 PHP

NodeJS Linux Enterprise Server 和 Red Hat Enterprise Linux 包含了运行所需软件，以使用 unixODBC 访问数据库的带有 PHP 脚本语言的 Apache Web 服务器。

执行以下步骤：

1. 基于 SLES 9 和 SLES 10 的默认软件安装，你需要从安装源向你的服务器添加以下软件包包：
   - `apache2`
   - `apache2-prefork` 或 `apache2-worker`
   - `apache2-mod_php4`
   - `php4`
   - SLES 9 使用 `php4_unixODBC`，SLES 10 使用 `php5-unixODBC`
   在 RHEL 3 和 RHEL 4 上，你可以添加名为 `php-odbc` 的包。

2. 使用以下任一命令启动 Web 服务器：
   `root@suse-linux:-> rcapache2 start`
   `root@redhat-linux:-> /etc/init.d/httpd start`

3. 检查 Apache 服务器是否正在运行。使用浏览器打开 `http://linuxserver/`。
   由于目前没有配置，你将收到一条错误消息：
   `Access forbidden: Error 403`
   如果你收到类似“目标不可到达”（destination unreachable）的消息，则可能需要检查 Apache 是否正在运行并验证你的某些设置。

4. 通过在非 root 用户的配置文件的 public_html 目录中创建一个文件来测试 PHP 支持：
   `user@linux:-> echo "<?php phpinfo(); ?>" ~ /public_html/phpinfo.php`

   > 注意：通过将 PHP 放在 Apache 文档目录的子文件夹中，让 Apache 能够访问 PHP 应用。

   此示例使用了用户主目录下的 public_html 文件夹。你也可以将文件放置在 Apache 文档目录下的 `/www/htdocs` 中。例如，将 PHP 示例应用程序放置在 `/www/htdocs/phptest` 目录下，并使用以下地址打开网页：
   `http://linuxserver/phptest`

5. 将你的 Web 浏览器指向以下地址，并将 `~outser` 替换为你创建 phpinfo 文件时使用的自己的 Linux 用户名：
   `http://linuxserver/~outser/phpinfo.php`
   此 PHP 测试页面包含有关 PHP 如何配置以及如何编译 ODBC 支持的信息。

请参见图 3-11。

### PHP 版本 4.3.4

| 系统 | Linux amass 2.6.0-97-pseries64 #1 SMP Fri Jul 2 14:21:59 UTC 2004 pppc64 |
| :--- | :--- |
| 构建日期 | 2004年7月1日 18:34:04 |
| 配置命令 | `/configure --prefix=/usr --sharedir=/usr/share --mandir=/usr/share/man/ --with-bindir=/usr/bin --libdir=/usr/lib --includedir=/usr/include --sysconfig=/etc --with-libxml* --with-exec-dir=/usr/lib/php/bin --enable-debug="--enable-inline-optimizer --enable-memory-limit --enable-magic-quotes --enable-safe-zone --enable-session --disable-malloc --disable-cli --without-pear --with-openssl --with-apache2=/usr/sbin/apache2 --suse-linux` |
| 服务器 API | Apache 2.0 Handler |
| 版本 | 已禁用 |
| 目录 | |

图 3-11 带有 `phpinfo()` 的 PHP

现在，将示例 3-9 中的 PHP 脚本按如下路径放在 Apache 文档目录：
`/home/itsouser/public_html/ODBCexample.php`

PHP 脚本由 Apache 使用特殊的用户配置执行。请注意不同的访问权限。你的用户 DSN 无法被 PHP 脚本访问。请使用系统 DSN（System DSN）。

#### 示例 3-9 PHP ODBC 示例

```html
<html>

<body>

<h1 align="center">客户姓名列表</h1>

<table border=1 bgcolor="#FFFFFF" align="center">

<tr><th>编号</th><th>姓</th><th>余额</th></tr>

<?php

$dbname="iSerDB4aIIuser"; //unix/ODBC 系统 Dsn name/ODBC 系统 Dsn 名称

$dbuser="itsouser"; //i55/OS 用户名

$dbpassword="password"; //i55/OS 密码

$db=odbc_connect($dbname, $dbuser, $dbpassword); //连接到 iSeries 的 DB2 ODBC

if ($db==FALSE) { echo "Cannot connect!"; } //测试数据库连接是否成功

$sql="select CUSUM, LTNAM, BALDUE FROM qiws.quscctdt"; //查询语句

$result=odbc_exec($db, $sql); //执行语句

while ($row=odbc_fetch_row($result)) { //获取结果集

printf("<tr><td>%s</td><td>%s</td><td>%s</td></tr>", odbc_result($result,1),odbc_result($result,2),odbc_result($result,3));

}

odbc_close($db); //关闭连接

?>

</table>

</body>

</html>
```



7. 使用 Web 浏览器查看 PHP 脚本的结果：
`http://linuxserver/~ouser/ODBCexample.php`

请参见表 3-2。

**表 3-2：`ODBCexample.php` 的浏览器视图**

| 客户编号 | 姓 | 应付余额 |
|---|---|---|
| 938472 | Henning | 37.00 |
| 839283 | Jones | 100.00 |
| 392859 | Vine | 43.00 |
| 398485 | Johnson | 3987.50 |
| 937697 | Yelton | 113 May5 |
| 389572 | Steens | 1208 Store |
| 846283 | Allison | 459 Pden |
| 475938 | Doe | 113 Myrtle |
| 693829 | Thomas | 0218 |
| 593029 | Williams | 218 NW |
| 192837 | Lee | 315 St |
| 583990 | Abraham | 511 |

## 4.2.2 创建示例数据库

本章中的所有示例都使用示例数据库。示例数据库的创建是通过存储过程 `CREATE_SQL_SAMPLE("library")` 完成的，其中 `library` 是你是你想要创建的示例库名称。该存储过程是版本 5 Release 1 中引入的，并随操作系统发布。要创建示例数据库，请执行以下步骤：

- 1. `STRSQL`
  进入交互式 SQL 界面
- 2. `CALL QSYS/CREATE_SQL_SAMPLE("DBSAMPLE")`
  创建包含示例表的库（SQL 术语中的集合）

创建示例数据库需要几分钟时间。完成后，你将拥有 13 张表和许多逻辑视图。表中还包含示例数据。示例模式中包含两组数据库表。一组包含 `ORG`、`STAFF` 和 `SALES`。这是一组非常简单的模式，表之间的交互有限，表内的数据类型也不复杂。其余表组成了一个更复杂的数据库模式，并使用了更复杂的数据类型，例如 `BLOB` 和 `CLOB`。这些表之间的交互也更加频繁。

## 4.3 命令行 JDBC 应用程序

要在 Linux 上开始 JDBC 编程，你可以从命令行方法开始，所有输入都来自标准输入（`stdin`），所有输出都发送到标准输出（`stdout`）。这是测试 JDBC 和 SQL 代码的极佳方法，无需担心图形界面。示例命令行 JDBC 应用程序选择了 `ORG` 表的记录以获取部门列表。然后它获取部门编号并运行预编译 SQL 语句，以获取每个部门的成员、职位以及在公司的年限。这些信息会每个部门发送到标准输出，生成部门类型列表。

使用 `javac` 创建 Java 程序，程序源代码见第 54 页的示例 4-1：

```
linux:~ javac SimpleJDBC.java
```

这会执行 Java 代码。要运行程序，请运行 `java` 命令：

```
linux:~ java SimpleJDBC
```

你可能需要将当前目录添加到 `CLSPATH` 中才能找到 Java 程序。要做到这一点，请使用以下命令：

```
linux:~ export CLSPATH=$CLSPATH:./jopen/lib/jt400.jar.
```

或者使用 `classpath` 参数来包含 `jtopen` 并让程序搜索路径：

```
linux:~ java -classpath ./jopen/lib/jt400.jar:: SimpleJDBC
```

这会将当前目录（通过 `:` 标识）添加到当前路径的最后。此 Java 程序的输出将发送到标准输出。如果你想将数据发送到文件，可以使用以下命令将标准输出重定向到文件：

```
linux:~ java SimpleJDBC > jdbc.output
```

### 4.3.1 关于程序的更多

在建立 JDBC 连接时，我们嵌入了连接期间将使用的用户配置和密码。如果未提供配置和密码，则会弹出提示要求输入配置和密码。

> **注意**：如果未配置用户和密码，`Toolbox` 会生成一个图形用户界面 (GUI) 对话框进行提示。这意味着你需要 `X-Window` 环境才能看到此提示。如果你在文本模式服务器上工作，你将在命令行提示符上看到一些字体错误消息，但日志可以正常工作。

程序流是执行一个查询以识别 `ORG` 表中的所有部门。对于每个结果部门，运行一个预编译语句查询以从 `STAFF` 表获取该部门的所有成员。SQL 语句可以如示例 4-1 所示简单，该示例展示了使用 `ORG`、`STAFF` 和 `SALES` 表的 JDBC 代码。

- **示例 4-1 简单的 JDBC 源码 `Simple.JDBC.java`**

```java
import java.sql.*;

public class SimpleJDBC {

    // 将字符串格式化为固定长度
    private static String format(String s, int width) {
        String formattedString;
        if (s.length() < width) {
            StringBuilder buffer = new StringBuilder();
            for (int i = s.length(); i < width; ++i) {
                buffer.append(" ");
            }
            formattedString = buffer.toString();
        } else {
            formattedString = s.substring(0, width);
        }
        return formattedString;
    }

    public static void main(String[] args) {
        Connection connection = null;
        try {
            // 加载 Toolbox JDBC 驱动
            Class.forName("com.ibm.as400.access.AS400JDBCDriver");
            // 获取到 iSeries 数据库的连接
            // 如果未提供用户或密码，将出现提示
            String system = "iseriesname";
            String url = "jdbc:as400://" + system;
            String user = "Username";
            String password = "Password";
            connection = DriverManager.getConnection(url, user, password);
            
            DatabaseMetaData meta = connection.getMetaData();

            // 创建并执行一个简单的 SQL 选择语句语句
            Statement orgSelect = connection.createStatement();
            ResultSet orgResults = orgSelect.executeQuery("SELECT * FROM DBSAMPLE");

            PreparedStatement deptSelect = connection.prepareStatement(
                "SELECT NAME, YEARS, JOB FROM DBSAMPLE"
                + meta.getCatalogSeparator()
                + "STAFF"
                + " WHERE DEPT = ?");

            ResultSet deptResults = null;
            int deptNum = 0;

            // 输出每条记录的信息
            while (orgResults.next()) {
                deptNum = orgResults.getInt("DEPT");
                deptSelect.setInt(1, deptNum);
                deptResults = deptSelect.executeQuery();
                
                while (deptResults.next()) {
                    System.out.println(format(deptResults.getString("NAME"), 15)
                    + " | " + deptResults.getString("DIVISION")
                    + " | " + deptResults.getString("JOB")
                    + " | " + deptResults.getInt("YEARS"));
                }
            }
            }
    }
}
```



### 4.3.2 示例输出

`示例 4-2`是简单`JDBC`生成的输出示例。

`NAME` | `DIVISION` | `JOB` | `YEARS`
---------------------------------------
`JOHN DOE` | `SALES` | `MANAGER` | 5
`JANE SMITH` | `SALES` | `CLERK` | 2
`BOB JOHNSON` | `IT` | `DEV` | 10
`ALICE WHITE` | `HR` | `REP` | 3

```java
}
catch (SQLException e) {
    e.printStackTrace();
} finally {
    if (connection != null) {
        connection.close();
    }
}
```

```java
this.division = division;
}

public void setLocation(String location) {
    this.location = location;
}

public void setNumber(int number) {
    this.number = number;
}
```

```java
public GraphicalJDBC() {
    super();
    initialize();
}
```

```java
private javax.swing.JPanel getDialogContentPane() {
    if (ivJDialogContentPane == null) {
        try {
            ivJDialogContentPane = new javax.swing.JPanel();
            ivJDialogContentPane.setName("DialogContentPane");
            ivJDialogContentPane.setLayout(null);
            getJDialogContentPane().add(getTFSelection());
            getTFSelection().getName();
            getJDialogContentPane().add(getCBDepartmentName());
            getCBDepartmentName().getName();
            getJDialogContentPane().add(getTFDepartmentLocation());
            getTFDepartmentLocation().getName();
            getJDialogContentPane().add(getSPTableScrollPane());
            getSPTableScrollPane().getName();
        } catch (java.lang.Throwable exc) {
            handleException(exc);
        }
        return ivJDialogContentPane;
    }
}
```

```java
private javax.swing.JTextField getTFSelection() {
    if (ivTFSelection == null) {
        try {
            ivTFSelection = new javax.swing.JTextField();
            ivTFSelection.setName("TFSelection");
            ivTFSelection.setText("选择部门");
            ivTFSelection.setBounds(16, 35, 189, 23);
            ivTFSelection.setEditable(false);
            ivTFSelection.setHorizontalAlignment(javax.swing.JTextField.RIGHT);
        } catch (java.lang.Throwable exc) {
            handleException(exc);
        }
        return ivTFSelection;
    }
}
```

```java
private javax.swing.JComboBox getCBDepartmentName() {
    if (ivCBDepartmentName == null) {
        try {
            ivJCBDDepartmentName = new javax.swing.JComboBox();
            ivJCBDDepartmentName.setName("CBDepartmentName");
            ivJCBDDepartmentName.setBounds(221, 35, 189, 23);
        } catch (java.lang.Throwable ivExc) {
            handleException(ivExc);
        }
        return ivJCBDDepartmentName;
    }
}

private javax.swing.JTextField getTFTTFieldDepartmentLocation() {
    if (ivTFDepartmentLocation == null) {
        try {
            ivTFDepartmentLocation = new javax.swing.JTextField();
            ivTFDepartmentLocation.setName("TFDepartmentLocation");
            ivTFDepartmentLocation.setBackground(new java.awt.Color(204, 204, 204));
            ivTFDepartmentLocation.setBounds(13, 90, 400, 211);
        } catch (java.lang.Throwable ivExc) {
            handleException(ivExc);
        }
    }
    return ivTFDepartmentLocation;
}

private javax.swing.JScrollPane getJPTableScrollPane() {
    if (ivJPTableScrollPane == null) {
        try {
            ivJPTableScrollPane = new javax.swing.JScrollPane();
            ivJPTableScrollPane.setName("JPTableScrollPane");
            ivJPTableScrollPane.setVerticalScrollBarPolicy(javax.swing.JScrollPane.VERTICAL_SCROLLBAR_ALWAYS);
            ivJPTableScrollPane.setHorizontalScrollBarPolicy(javax.swing.JScrollPane.HORIZONTAL_SCROLLBAR_NEVER);
            ivJPTableScrollPane.setBounds(13, 130, 400, 187);
            getJPTableScrollPane().getViewport().getTBDepartmentTable();
        } catch (java.lang.Throwable ivExc) {
            handleException(ivExc);
        }
    }
    return ivJPTableScrollPane;
}

private javax.swing.JTable getTBDepartmentTable() {
    if (ivJTBDepartmentTable == null) {
        try {
            ivJTBDepartmentTable = new javax.swing.JTable();
            ivJTBDepartmentTable.setName("TBDepartmentTable");
```



```java
getJPTableScrollPane().getColumnHeader(ivJTBDepartmentTable.getColumnHeader());

getJPTableScrollPane().getViewport().setBackingStoreEnabled(true);

ivJTBDepartmentTable.setModel(new javax.swing.table.DefaultTableModel());

ivJTBDepartmentTable.setBounds(0, 0, 200, 200);

ivJTBDepartmentTable.getTableHeader().setReorderingAllowed(false);

ivJTBDepartmentTable.getTableHeader().setResizingAllowed(false);

((DefaultTableModel)ivJTBDepartmentTable.getModel()).addColumn("员工");

((DefaultTableModel)ivJTBDepartmentTable.getModel()).addColumn("职位");

((DefaultTableModel)ivJTBDepartmentTable.getModel()).addColumn("年限");

} catch (java.lang.Throwable ivExc) {

    handleException(ivExc);

}

return ivJTBDepartmentTable;

}

private void handleException(java.lang.Throwable exception) {

    /* 取消以下注释可以将未捕获的异常打印到标准输出 */

    // System.out.println("---------- 未捕获的异常 -------");

    // exception.printStackTrace(System.out);

}

private void initConnections() {

    // 代码片段中的实现细节

}

private void connectTo(java.awt.event.ActionEvent arg1) {

    try {

        // 代码片段中的实现细节

    } catch (java.lang.Throwable ivExc) {

        handleException(ivExc);

    }

}

public void cbDepartmentName_ActionPerformed(java.event.ActionEvent actionEvent) {

    try {

        // 代码片段中的实现细节

    } catch (java.lang.Throwable ivExc) {

        handleException(ivExc);

    }

}

private void retrieveDepartmentInfo(int selectedIndex) {

    DefaultTableModel tm = (DefaultTableModel)getDepartmentTable().getModel();

    // 移除行

    for (int x = tm.getRowCount(); x > 0; x--) {

        tm.removeRow(x);

    }

    // 如果是第一个条目则清空，否则填充表格

    if (selectedIndex == 0) {

        getTFDepartmentLocation().setText("");

    } else {

        try {

            DepartmentInfo dept = (DepartmentInfo)departments.elementAt(selectedIndex);

            getTFDepartmentLocation().setText(dept.getDivision() + "部门位于 " + dept.getLocation());

        } catch (Exception e) {

            // 处理错误

        }

    }

}

private void initialize() {

    // 创建默认的空白条目

    getCBDepartmentName().addItem("*");

    DepartmentInfo defaultDept = new DepartmentInfo();

    defaultDept.setName("*");

    defaultDept.setLocation("*");

    defaultDept.setDivision("*");

    defaultDept.setNumber(-1);

    departments.addElement(defaultDept);

    try {

        // 创建并执行 SQL 查询语句

        Statement orgSelect = connection.prepareStatement();

        ResultSet orgResults = orgSelect.executeQuery("SELECT * FROM IBMOSAMPLE"

            + meta.getCatalogSeparator()

            + "ORG");

        while (orgResults.next()) {

            getCBDepartmentName().addItem(orgResults.getString("DEPTNAME"));

            DepartmentInfo dept = new DepartmentInfo();

            dept.setName(orgResults.getString("DEPTNAME"));

            dept.setLocation(orgResults.getString("LOCATION"));

            dept.setDivision(orgResults.getString("DIVISION"));

            dept.setNumber(orgResults.getInt("DEPTNUMBER"));

            departments.addElement(dept);

        }

    } catch (Exception e) {

        // 处理错误

    }

}
```

```java
)
catch(Exception e) {
}
}
```

### 4.4.2 输出

图 4-1 显示了在 Linux 平台上使用 `ORG`、`STAFF` 和 `SALES` 表运行图形 JDBC 代码的输出。

![](img/165c050f45ac58e1635258993855261a_76_0.png)

图 4-1 图形 JDBC 示例

## 4.5 Toolbox for Java

之前的示例仅使用了 IBM Toolbox for Java 的一部分。该工具箱包含了许多其他访问 IBM i/OS 的有用类。你可以使用该工具箱执行如运行 i/OS 命令、创建用户和组、调用 IBM i/OS 程序和 API 以及访问其他对象等操作。工具箱还包含了图形类，使得展示 IBM i/OS 信息和对象变得简单且一致。该工具箱作为一个开源项目编写，源代码在 IBM 公共许可下可用。有关该工具箱和开源功能的更多信息可以在此处找到：

`http://www.ibm.com/servers/eserver/iseries/toolbox/`

### 4.5.1 运行 i/OS 命令

示例 4-4 是一个 Java 程序，展示了使用工具箱运行 i/OS 命令有多简单。在这个示例中，用户被提示创建一个库名。然后使用工具箱的 `CommandCall` 对象来创建该库。命令生成的所有消息都会返回并显示给用户。

> 注意：如果没有配置用户和密码，工具箱将为他们生成一个图形提示。这意味着你需要 X-Window 环境来获取此提示。你可能会在命令行提示符上看到一些字体错误消息，但逻辑运行没有问题。

参见示例 4-4。

#### 示例 4-4 IBM Toolbox for Java 命令示例

```java
import java.io.*;

import java.util.*;
```



```java
import com.ibm.as400.access.*;

public class ToolboxCommand {

    public static void main(String[] args) throws Exception {

        String systemName = "iseries.itso.ibm.com";

        String user = "Itsouser";

        String password = "password";

        AS400 system = new AS400(systemName, user, password);

        BufferedReader inputStream = new BufferedReader(

            InputStreamReader(System.in), 1);

        String libraryName = null;

        System.out.println(" ");

        System.out.println("Library to create: ");

        libraryName = inputStream.readLine();

        System.out.println(" ");

        CommandCall command = new CommandCall(system);

        if (command.run("cltlib " + libraryName)) {

            System.out.println("Success");

        } else {

            System.out.println("Failure");

        }

        System.out.println(" ");

    }

}

AS400Message[] messageList = command.getMessageList();

if (messageList.length > 0) {

    System.out.println("Messages returned are: ");

}
```

### 4.5.2 输出

示例 4-5 展示了编译、成功创建库以及创建失败的情况。在两种情况下，`i/OS` 命令均在与连接关联的用户配置文件（在此例中为 `ITSOUSER`）下，并在 `IBM i/OS` 上的 `QSERVER` 子系统的作业中运行。

## **示例 4-5: 工具箱命令输出示例**

```bash
linux~\> javac -classpath ./jt400.jar ToolboxCommand.java

linux~\> java -classpath ./jt400.jar.. ToolboxCommand
```

Library to create: itsotest

Success

Messages returned are:

CPC2102: Library ITSOTEST created.

linux:"> java -classpath ./jt400.jar:: ToolboxCommand

Library to create: itsotest

Failure

Messages returned are:

CPF2111: Library ITSOTEST already exists.

linux:">

![](img/165c050f45ac58e1635258993855261a_80_0.png)

## 5.1 使用 Samba 连接 iSeries NetServer

本章讨论了 Linux 上的 Samba 客户端连接到 iSeries NetServer，并提供了如何在 `IBM i5/OS` 和 Linux 环境中使用它的示例。

本章讨论了以下内容：

- iSeries NetServer Samba 客户端支持
- NetServer 与网络文件系统 (NFS) 的对比
- 使用 iSeries NetServer Samba 客户端支持的操作指南
- iSeries NetServer Samba 客户端支持的故障排除指南
- 在 `IBM i5/OS` 打印机上打印

### 5.1.1 NetServer 简介

在讨论 Samba 访问 iSeries NetServer 时有一些约定。在 Windows 中，用户将网络驱动器映射到共享资源。在 Linux 中，用户挂载一个现有目录。例如，在 Windows 中你可能会将网络驱动器映射到 I 盘，而在 Linux 中你可能会将远程 iSeries NetServer 挂载到 `/mnt/myshare`。使用任何目录作为本地挂载的能力消除了对 Linux 系统上映射驱动器数量的限制，因为你不再限于单个盘器符。

### 5.1.2 NetServer 与 NFS

NetServer 和 NFS 都允许 Linux 系统访问 `i/OS` 文件系统。

### 5.1.3 NetServer Samba 支持

## 5.2 要求与安装

## 5.3 使用 iSeries NetServer Samba

### 5.3.1 iSeries NetServer 配置

### 5.3.2 Linux Samba 客户端配置

访问 NetServer 共享有多种方法，包括通过图形用户界面 (GUI) 和控制台。GUI 方法与 Windows 操作系统非常相似，我们将讨论从 Linux 控制台访问 SMB 资源的两种方法：

- `smbmount`
- `smbclient`

`smbmount` 命令等同于 Windows 中的映射驱动器，但与 Windows 使用驱动器号不同，它将目录挂载到某个特定的上级。这些目录被称为挂载点。任何你有权限的目录都可以挂载。

执行 `smbmount` 命令会启动一个管理挂载点的 smb 守护进程。当 smb 守护进程运行时，该挂载点即处于激活状态。

为了挂载任意文件系统，你必须以 root 用户身份登录，或者使用 `smbclient` 命令（它允许非 root 用户执行）。更多信息请参见 `mount`、`smbclient` 和 `fstab` 页面。`smbclient` 挂载的文件系统类型称为 cifs。

`smbclient` 命令是一个类似于文件传输协议 (FTP) 的接口，可以用它访问远程共享。当用户需要短暂连接到远程共享或想查看可用共享列表时，通常使用它。

#### 使用 smbmount 挂载网络驱动器

由于你已经创建了新文件夹并使用 iSeries Navigator 进行了共享，你现在准备好挂载 iSeries NetServer 了。首先，你需要在 Linux 系统本地创建挂载点。大多数发行版都有名为 `/mnt` 的目录。因此，在 `/mnt/` 下创建挂载点是一个很好的选择：

1. 执行：
```bash
linux~$ mkdir /mnt/smbtest
```
目录名称不需要匹配 iSeriesOS 上的共享名称。

2. 现在，如果你以 root 身份登录，可以挂载远程共享：
```bash
linux~$ smbmount //iseries.ibm.com/mnt/smbtest -o username=itsouser
```
必须指定 `username` 参数来指定 iSeriesOS 用户。现在会提示你输入密码。你现在可以将挂载的目录视为本地文件系统进行操作。

3. 为了测试，执行：
```bash
linux~$ ls /mnt/smbtest
```

#### smbmount 命令详情

`smbmount` 命令的第一个参数是远程共享，它可以是一个 IP 地址，或者通过域名系统 (DNS)、`/etc/samba/hosts` 解析为 IP 地址。第二个参数是本地挂载点。`-o` 选项表示设置给挂载守护进程的可选参数和设置。在这种情况下，指定的唯一选项是你想要登录的 iSeriesOS 用户配置。更多 `smbmount` 选项请使用 `man smbmount`。

`umount` 命令等同于 Windows 中的取消映射网络驱动器。它从本地文件系统内核卸载远程共享。该命令的唯一参数是挂载点。使用之前提供的示例，命令为：
```bash
linux~$ umount /mnt/smbtest
```
如果实际连接不再存在，该命令将失败。在这种情况下，root 用户必须执行更通用的 `umount` 命令。

#### 使用 smbclient 在 iSeries NetServer 和 Linux 之间复制文件

如前所述，`smbclient` 是一个类似于 FTP 的客户端，可以用它向远程系统的 SMB 共享或从中复制文件。

1. 验证远程系统上有哪些可用共享：
```bash
linux~$ smbclient -U username -L //systemname
```



这将为你提供来自远程 SMB 服务器的共享列表，如示例 5-1 所示。

**示例 5-1 `smbclient` 显示可用共享**

```bash
linux~$ smbclient -U itsouser -L //iseries.ibm.com
```

| Sharename | Type | Comment |
| :--- | :--- | :--- |
| `QIBM` | Disk | IBM Product Directories |
| `ADMIN` | IPC | AS400 Resource |
| `QDIRSRV` | Disk | OS/400 Directory Services |
| `IPCS` | IPC | AS400 Resource |

| Server | Comment |
| :--- | :--- |
| Workgroup | Master |

2. 建立 `iSeries NetServer` `smbclient` 连接：
   ```bash
   linux~$ smbclient //iseries/sharename -U username
   ```
   系统会提示输入密码。随后你将看到 `smb` 提示符：`smb: `

3. 输入 `help`。
   你将看到可用命令列表。注意这些命令与 `FTP` 相似。

4. 尝试获取你已连接共享的文件列表。

5. 使用 `get` 或 `put` 从 `NetServer` 或向 `NetServer` 复制文件。

6. 要复制任何目录，必须开启目录递归并禁用提示，否则系统会对你想要复制的每一个文件进行提示。`recurse` 和 `prompt` 命令是切换开关。第一次使用 `recurse` 会开启该功能，第二次则关闭。命令提示符的作用反之。

   要启用递归并禁用提示，请执行：
   ```bash
   smb> recurse
   smb> prompt
   ```
   你现在可以使用 `mget` 和 `put` 命令在 `iSeries NetServer` 共享与本地之间复制目录。

### 5.3.3 排查到 iSeries NetServer 的 SMB 连接问题

以下是可能发生的常见问题：

- `session request to <sysname> failed`
  当用于建立 `smbmount` 连接的系统名或 IP 地址与 `iSeries NetServer` 名称不一致时，会发生此错误。你可以忽略它。`smbmount` 和 `smclient` 只需要远程系统的 IP 地址或将系统名解析为 IP 地址的能力。

- `cannot mount on /mountpoint: Operation not permitted`
  发生此错误是因为你没有权限在 `/mountpoint` 上进行挂载。

- `Input/output error`
  如果你在尝试卸载挂载点时遇到输入/输出错误，意味着连接已丢失。要找出哪些进程仍在使用该挂载点，请使用 Linux 的 `fuser` 命令：
  ```bash
  linux~$ fuser /mnt/smbtest
  ```



```
umount: /mnt/smbtest: device busy
```

- 覆盖共享上的文件会报输入/输出错误，即使权限设置正确。使用 `cp` 复制文件时：

```
cp: cannot create regular file /mnt/smbtest/test.txt: Input/output error
```

如果共享上不存在该文件，则 `cp` 或 `mv` 命令可以工作。内核为 2.4x 的 Linux 不会有这种行为。在这种情况下，你可以使用 `smclient` 工具或在复制新文件之前删除共享上的旧文件。

示例 5-3 显示了用户 `ITSOUSER` 的所有任务列表。如果你处理 `QZLSFILE` 任务，可以获取如远程 SMB 客户端的 IP 地址以及其他典型的 IBM i/OS 任务信息。

## 示例 5-3 对象锁

| 对象 | 类型 | 系统 |
| :--- | :--- | :--- |
| 库 (`Library`) | `ITSOUSER` | `*USPRF` |
| | `QSQYS` | `asp device : *SYSBAS` |

输入类型选项，按回车键。4-结束任务 5-处理任务 8-处理任务锁

| 选项 | 用户 | 锁 | 状态 | 范围 | 线程 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `QZLSFILE` | `QUSER` | `*SHRRD` | `HELD` | `*JOB` | |
| | | `*SHRRD` | `HELD` | `*JOB` | |
| | | `*SHRRD` | `HELD` | `*JOB` | |
| | | `*SHRRD` | `HELD` | `*THREAD` | `00000004` |

在 iSeries Navigator 配置中也可以获得类似的信息。

打开 iSeries Navigator 并展开 iSeries → Network → Servers → TCP/IP。双击 iSeries NetServer。

在这里，你可以获取大量关于 iSeries NetServer 共享以及所有到这些共享的活动连接的信息。

## 5.4 连接到 iSeries NetServer 打印共享

Linux 通过 `lpr`、`jpd`、`cups` 等具有自己的打印缓冲支持。然而，让 Linux 使用 IBM i/OS 的打印缓冲和打印机管理功能作为打印机，将需要打印的文件发送到 IBM i/OS 打印机可能会是有益的。

### 5.4.1 如何配置打印共享

以下示例显示了如何配置打印共享，并允许 Linux 系统上的用户共享在 IBM i/OS 上配置的打印机。我们假设 IBM i/OS 上已经配置了一个打印机，并且你可以使用该打印机的输出队列 (`OUTQ`)。

> **重要：** 由于 Linux 上的打印机驱动程序支持有限，你的 IBM i/OS 打印机必须能够打印 PCL 或 postscript 数据流。如果你打算设置打印共享并配置为 IBM `'iDPTS'`、IBM 高级功能打印™ (IBM `AFP*`) `YES`，则必须使用适用于 iSeries `75221P1` 的 IBM Infoprint® Server 将 PCL 或 Postscript 数据流转换为 AFP。

更多信息请参阅标题为 IBM eServer iSeries Printing Vi: Delivering the Output of e-business 的 SG24-6250。

在本示例中，我们使用 Novel Linux 发行版连接到 iSeries NetServer 打印共享。如果你使用的是不同的 Linux 发行版，步骤和显示可能会有所不同。

最初，在 IBM i5/OS 上选择一个合适的 `OUTQ`，或使用 `CRTOUQ` 命令创建一个。要在 IBM i5/OS 上设置打印共享，你需要 iSeries Navigator。

## 使用 iSeries Navigator 创建打印共享

要共享 i5/OS 的 `OUTQ`，请在 iSeries Navigator 界面上执行以下步骤：

1. 选择 Network -> Servers -> TCP/IP 和 iSeries NetServer。
2. 展开 iSeriesNetServer 并右键点击 Shared Objects。选择 New（新建）然后选择 Printer（打印机）。
3. 在图 5-3 所示的后续屏幕中填写 Name（名称）、Output queue（输出队列）和 library（库）字段。

![](img/165c050f45ac58e1635258993855261a_89_0.png)

图 5-3 iSeries NetServer 打印共享屏幕

4. 选择 OK（确定）。
5. 选择 Shared Objects（共享对象）以检查此打印共享是否在列表中。

## 从 Linux 连接到共享打印机

在 IBM i5/OS 的 `OUTQ` 被共享后，你可以从 Linux 客户端配置 Samba 打印机。

1. 在 Novell SUSE Linux 上启动配置工具 YaST。在左侧面板选择 Hardware（硬件）部分，点击右侧面板上的打印机图标。
2. YaST 然后将初始化打印机配置工具。当打印机设置窗口打开时，选择 Add（添加）。
3. 在 Printer Type（打印机类型）窗口中选择 Network Printer（网络打印机）。
4. 在 Connection for printer（打印机连接）窗口中，选择 Print via SMB Network Server（通过 SMB 网络服务器打印）并选择 Next（下一步）。见图 5-4。

![](img/165c050f45ac58e1635258993855261a_90_0.png)

图 5-4 使用 YaST 连接到打印共享

5. 打开 Samba/Windows 打印机屏幕。按照图 5-5 所示输入以下信息并选择 Next（下一步）：
   - Host name（主机名）：输入 IBM i5/OS 的主机名或 IP 地址。
   - Remote query（远程查询）：定义打印共享名称。
   - User（用户）：输入有效的 IBM i5/OS 用户配置文件。
   - Password（密码）：输入该用户的密码。

![](img/165c050f45ac58e1635258993855261a_90_1.png)

图 5-5 YaST 中的 Samba/Windows 打印机配置窗口

6. 在 Queue Name（队列名称）窗口中，为 Linux 指定打印机名称，并勾选 `Do Local Filtering`（进行本地过滤）选项。见图 5-6。

![](img/165c050f45ac58e1635258993855261a_91_0.png)

图 5-6 指定打印机名称

7. 在 i5/OS 上选择 Linux 机机， Linux    。 IBM i iOS 打印机 支持 PCL 或 Postscript 数据流。
8. i i5- 5555555555555555555511555555555555555555555555555555555555555511111555555555555555555555555552222222525222

## 6.2 在 IBM i/OS 上设置 NFS 服务器

本节将介绍如何使用 iSeries Navigator 在 IBM i/OS 端配置和管理 NFS 服务器。执行以下步骤：

1. 在 IFS 中创建一个目录来存放 Linux 文件，例如：
   ```
   MKDIR DIR('/nfshome')
   ```
2. 在 iSeries Navigator 上选择文件系统（File System）→ 集成文件系统（Integrated File System）→ 根目录（Root）。
   选择所需的存放 NFS 目录。右键点击，选择 NFS 导出（NFS Export），然后选择属性（Properties），如图 6-1 所示。

![](img/165c050f45ac58e1635258993855261a_96_0.png)

图 6-1 使用 iSeries Navigator 创建 NFS 导出

3. 检查详情是否正确（默认用户为 `QNFSANON`），然后如图 6-2 所示选择导出（Export）。

![](img/165c050f45ac58e1635258993855261a_96_1.png)

图 6-2 使用 iSeries Navigator 配置 NFS 导出 `/nfshome`

注意：如果选择“添加到永久定义的导出列表”（Add to list of permanently defined exports），条目将被添加到 IFS `/etc/EXPORTS` 文件。

4. 现在启动 NFS 服务器。选择网络（Network）-> 服务器（Servers）-> TCP/IP。右键点击 NFS 并选择全部（All），如图 6-3 所示。

![](img/165c050f45ac58e1635258993855261a_97_0.png)

图 6-3 启动 NFS 服务器

现在，IBM i/OS 上的 NFS 已就绪。

## 6.3 挂载 IBM i/OS NFS 导出

使用 `mount` 命令对可用的 NFS 导出进行临时连接。如果你希望在 Linux 启动期间建立 NFS 连接，请修改 `/etc/fstab` 文件以在 Linux 启动时挂载文件系统。执行以下步骤：

1. 以 `root` 用户身份登录 Linux 系统。
2. 创建一个目录作为挂载点，例如 `/mnt/iseries`：
   ```
   linux:> mkdir /mnt/iseries
   ```
3. 使用以下远程文件系统挂载系统语法 `systemname:exportname /localmountpoint` 将导出挂载到目录：
   ```
   linux:> mount iseries.ito.ibm.com/nfshare /mnt/iseries
   ```
4. 不带参数的 `mount` 命令将显示所有挂载的文件系统，如示例 6-1 所示。

示例 6-1 所有挂载的文件系统




# 6.4 高级 NFS 配置与安全

`/mount`

`/dev/sda3 on reiserfs (rw,acl,user_xattr)`

`proc on /proc type proc (rw)`

`sysfs on /sys/sys type sysfs (rw)`

`tmpfs on /dev/shm type tmpfs (rw)`

`devpts on /dev/pts type devpts (rw,mode=0620,gid=5)`

`iseries.ito.ibm.com/nfshare /mnt/iseries type nfs (rw,addr=10.1.1.1)`

## 84 Linux 与 IBM i/OS 的集成

1. 现在你可以在 NFS 目录之间进行文件复制：
   `echo "Test file for NFS" > /mnt/iseries/test.txt`
2. 在 iSeries 的 5250 会话或 iSeries Navigator 中验证该文件：
   `DSPF STMF'('/nfshome/test.txt')`
3. 使用以下命令从 Linux 系统中移除 NFS 连接：
   `mount /mnt/iseries`
4. 如果你想在启动时挂载 NFS 导出，则必须编辑 `/etc/fstab` 文件。该文件包含关于各种文件系统的信息，例如哪些系统在启动时被挂载。小心编辑，损坏的 `fstab` 文件会导致你的 Linux 无法启动。参见示例 6-2。按照正确的顺序添加关于 NFS 导出的以下信息：
   - a. 文件类型：`systemname:export`
   - b. 本地点：`/mountdirectory`
   - c. 文件类型：`nfs`
   - d. 挂载选项，即读/写权限：`rw`
   - e. 必须是备份的文件系统（仅用于备份）：`0`
   - f. `fsck` 检查文件系统的顺序：`0` 不检查

```
示例 6-2 NFS 导出

linux:~> /etc/fstab

/dev/sda3 reiserfs acl,user_xattr 1 1

/dev/sda2 swap swap pri=42 0 0

/devpts /dev/pts devpts mode=0620,gid=5 0 0

/proc proc defaults 0 0

sysfs /sys sysfs noauto 0 0

iseries.ito.ibm.com:/nfshome /mnt/iseries rw 0 0
```

前述描述的配置仅提供了简单的 NFS 配置。它不包含任何安全选项。每个人都可以在自己的电脑上挂载文件系统，因为没有配置相关的限制。此外，文件访问是由 IBM i/OS 上的一个用户执行的：`QNFS`。在这种情况下，无法实现对象级安全。IBM i/OS 不区分哪些用户访问了 NFS 导出。但有不同的选项可以扩展安全级别。

### 6.4.1 通过主机 IP 地址限制访问

第一要务是限制访问……（此处省略部分重复的引导性文字，保持逻辑一致）

1. 在 iSeries Navigator 中打开 `Network` -> `Servers` -> `TCP/IP`。
2. 右键点击 NFS 服务器并选择 `Exports`。
3. 选择导出的目录……

![](img/165c050f45ac58e1635258993855261a_99_0.png)

图 6-4 - 通过主机限制

图 6-5 通过 IP 地址限制访问

![](img/165c050f45ac58e1635258993855261a_99_1.png)

### 6.4.2 应用对象级安全

对象级安全意味着 UID 与 i/OS 相同。UID 与 i/OS 相同非常重要。在示例中创建了一个名为 `linuxuser` 的 Linux 用户，其 UID 为 1001。使用以下命令验证 UID：

```
linuxuser:~> id

uid=1001(linuxuser) gid=100(users),14(dialout)
```

使用示例 6-3 所示的命令显示 UID：

| 用户配置文件 - 基本 : `ISERIESUSR` |
| 对象审计值 . . . . . . : `*NONE` |
| 动作审计值 . . . . . : `*NONE` |
| 用户 ID 编号 . . . . . . . . : 1001 |
| 组 ID 编号 . . . . . . . . : `*NONE` |

示例 6-3 显示当前 UID

```
linuxuxer@linux:~> chmod 700 /mnt/iseries/linuxuxer/

linuxuxer@linux:~> ls -l /mnt/iseries/

drwx------ 2 linuxuxer 8192 2005-08-05 00:00 linuxuxer
```

```bash
linuxuxer@linux:~> echo "secret of linuxuxer" > /mnt/iseries/linuxuxer/secret.txt
```

当你关闭 NFS 导出的 root 权限时，Linux root 用户将映射到 `QSYS` iSeries 用户。无法在任何地方使用 root 账户访问文件：

```
root@linux:~> ls -l /mnt/iseries/
/bin/ls: Permission denied
```

现在你能够区分不同用户的数据了，例如在 IBM i/OS 上设置用户主目录。请记住，UID 是 NFS 协议中唯一的身份验证标准。如果 UID 没有映射到 IBM i/OS 上的正确用户配置文件，某些就可以获得未授权的文件访问权限。特别是，如果允许用户在连接到 NFS 的 Linux 系统上创建自己的自己的配置文件，那么他就可以创建任何想要的 UID 并访问 NFS 内部的任何文件

## 组识别

组识别的操作方式与 IBM i/OS 相同。在 Linux 系统上，每个用户组都有一个唯一的数字。GID 允许构建具有相同权限子集的用户组。

在之前提到的示例中，你没有在 IBM i/OS 上设置任何 GID。创建的文件 GID 为空。在 Linux 系统上，UID 或 GID 为 0 意味着 `root`。`ls -l` 命令显示文件的权限、所有者、大小和日期。组信息显示如下：

```
linuxuxer@linux:~> ls -l /mnt/iseries/

drwx------ 2 linuxuxer root 8192 2005-08-05 00:00 linuxuxer
```

要更改这一点，你可以在 IBM i/OS 上创建一个与 `linuxuxer` 组相同 GID 的组。使用 Linux 命令 `id` 获取组的 GID：

```bash
linux:~> id linuxuxer

uid=1001(users) gid=100(users),14(wucp),16(dialout)
```

在 IBM i/OS 上创建一个 GID 为 100 的组配置文件：

```
CRTUSPRPRF USRPRF(USERGRP) PASSWORD('MONE') TEXT('Linux users group') GID(100)
```

现在 `linuxuxer` 可以在 NFS 挂载中创建新文件：

```bash
linux:~> mkdir /mnt/iseries/linuxuxer

linux:~> echo "TEST" > /mnt/iseries/linuxuxer/gid100.txt
```

```bash
linux:~> ls -l /mnt/iseries/linuxuxer/

-rw-r--r-- 1 linuxuxer 9 2005-08-05 18:00 gid100.txt
```



## 通过 FTP 连接 IBM i5/OS

本章讨论了从 Linux 操作系统访问存储在 IBM i5/OS 系统上的数据的文件传输协议（FTP）方法。涵盖的方法包括：

- FTP 操作技巧
- 在交互模式下运行 FTP 命令
- 在批处理模式下运行 FTP 命令

### 7.1 FTP 操作

FTP 是传输控制协议/网协议（TCP/IP）的标准。FTP 包含客户端和服务器应用程序。大多数操作系统都包含客户端应用程序，并且通常在交互模式下运行。大多数操作系统也包含服务器应用程序。然而，服务器应用程序在后台或批处理模式下运行，必须显式启动。

#### 7.1.1 常用 FTP 命令

FTP 中有两种传输数据的方式。这是二进制模式和美国标准信息交换代码（ASCII）模式。在二进制模式下，文件的位将按原样复制。对对数据进行任何转换。二进制模式用于传输实际程序、图像、文件对象和其他。在非二进制模式下，数据可以在两个系统之间进行转换。非二进制模式（或 ASCII 模式）用于文本文件、程序源代码和其他人类可的文件。默认情况下，你的 FTP 会话为非二进制模式。要切换到二进制模式，输入 FTP 命令 `bin`。

要启动 FTP 会话，输入 `ftp [server]`，其中 `server` 是你想要传输文件的系统的主机名或 IP 地址。启动 FTP 会话后，你可以使用 `get` 命令从远程系统获取文件到本地系统，并使用 `put` 命令将文件从本地系统上传到远程系统。你可以在单个 FTP 会话中执行多次 `get` 和 `put` 命令。

当初始化 IBM/OS 的 FTP 时，你处于 `QSYS` 文件系统。对于文件内的对象通过 `library/file/member` 访问，对于非文件对象通过 `library/object` 访问。你也可以访问集成文件系统（IFS）中的文件。要切换到 IFS 模式，输入 FTP 命令 `quote site namefmt 1`, `cd /`。访问 QSYS 文件可以使用 `/qsys.lib/library.lib/file/member.mbr` 或 `/qsys.lib/library/object.type`。访问 IFS 中的文件可以使用 `/directory/directory2/file.name`，其中 `file.name` 是你想要的文件名。

其他 FTP 命令是 `cd` 和 `lcd`，它们分别更改远程和本地系统的目录位置。`prompt` 命令与 `mget` 或 `mput` 配合使用非常有用。

#### 7.1.2 管理 FTP

配置 i/OS 使用命令 `CHGPTBL *`。启动和停止 FTP 使用 `ENDTCPSVR *`。

或者，对于 i/OS 使用命令 `STRTCPSVR`

### 7.2 使用 Linux 作为客户端

从 IBM i/OS 传输数据与从 Linux 传输数据相同，不同在于 i/OS 拥有不同的文件系统。FTP 命令从 IBM i/OS 命令行发布，并登录到 Linux 服务器需要 Linux 系统上的 FTP 服务器正在运行。通常你使用 `QSYS` 文件系统。如果你需要更改本地目录到 IFS，则使用 FTP 命令 `quote namefmt 1`。

`cd` 命令用于更改本地系统的目录，在本例中，即 IBM i/OS 系统。`cd` 命令用于更改远程或 Linux 系统的目录。如果不使用 `prompt` 命令，在传输每个文件之前，系统会提示你是否传输该文件。

### 7.4 在批模式下运行 FTP 命令

到目前为止，我们展示了交互式运行的 FTP 命令。虽然这是常用的用法，但也可以以批处理或程序模式执行 FTP 命令。在 IBM i/OS 的控制语言 (CL) 程序或 Linux 系统的上的脚本文件中，你可以输入 FTP 命令，提供或被提示输入用户名和密码，然后运行若干 FTP 命令。你可以使用 FTP 的 `run` 命令来运行远程命令。

示例-2 是一个简单的脚本文件，它以 `ITUSER` 身份创建，提示输入密码，创建一个 IBM i/OS 库，创建多个源物理文件，放入多个源文件，创建一个刚刚下载的 CL 程序之一，并运行新创建的程序。

示例-7-2 示例 FTP 脚本文件：`download.txt`

```
quote rcmd crtlib sysymgt text('Systems Management Tools')
```

```
quote rcmd crcrcf sysymgt/qclsrc text('CL Programs')
```

```
put "iso/sysymgt/chgcmdft.cl sysymgt/qclsrc.chgcmdft
put "iso/sysymgt/startmpg.cl sysymgt/qclsrc.startmpg
put "iso/sysymgt/starttys.cl sysymgt/qclsrc.starttys
put "iso/sysymgt/startup.cl sysymgt/qclsrc.startup
put "iso/sysymgt/mapkeys.cl sysymgt/qclsrc.mapkeys
put "iso/sysymgt/create.cl sysymgt/qclsrc.create
put "iso/sysymgt/snads.cl sysymgt/qclsrc.snads
put "iso/sysymgt/ctl.cl sysymgt/qclsrc.ctl
put "iso/sysymgt/dev.cl sysymgt/qclsrc.dev
put "iso/sysymgt/lin.cl sysymgt/qclsrc.lin
put "iso/sysymgt/pt.cl sysymgt/qclsrc.pt
put "iso/sysymgt/tn.cl sysymgt/qclsrc.tn
```

```
quote rcmd crtlpg sysymgt/create sysymgt/qclsrc
```

```
quit
```

要在 Linux 上使用此 FTP 脚本文件，请使用以下命令：

```
ftp system < download.txt
```



# 使用套编程连接 IBM i5/OS

本章讨论了从 Linux 操作系统访问存储在 IBM i5/OS 中的数据的编程方法。它讨论了进程在两个平台之间通信的方法。

本章讨论了以下内容：

- 通用考虑因素
    - 美国信息交换标准代码 (ASCII) 和扩展二进制编码交换码 (EBCDIC) 字符集
    - 字节序
- 套接字 (Sockets)
    - 客户端示例
    - 服务端示例

## 8.1 通用考虑因素

在使用 C 语言开始 socket 编程之前，有几点需要注意。首先是不同平台使用的字符集，其次是不同架构使用的字节序方案。

### 8.1.1 ASCII 和 EBCDIC 字符集

你可能知道 IBM i/OS 原生以 EBCDIC 字符集运行，而 Windows 和所有的 UNIX 版本（包括 Linux）都以 ASCII 字符集运行。当你在低层处理平台间的集成时，这一点最为明显，因为高层的数据移动通常会自动处理转换。处理不同字符集的常见常用机制包括：

- 使用 Series DB2 通用数据库 (UDB) 的功能

如果数据是你需要的内容，且集成方法允许你使用数据库表，那么你必须使用它们。IBM i/OS 的数据库功能处理 ASCII 和 EBCDIC 之间的转换（以及许多其他字符集转换）。开放套数据库连接 (ODBC) 和 Java 数据库连接 (JDBC) 示例使用了这种机制。

- 使用 unicode

Unicode 是更大的字符集，在 IBM i/OS 和 Linux 平台上均可用。这是 Java 广泛使用的方法。

- 执行自定义转换

你可以在 Linux 或 IBM i/OS 上执行转换。然而，在 IBM i/OS 中进行转换可能是最简单且最好的。有很多工具可用于字符转换。socket 示例代码演示了如何使用 `iconv()` 应用接口 (API) 将一个字符集标识符 (CSID) 转换为另一个。

本文描述的示例程序使用 IBM i/OS 的 `iconv()` API 进行 ASCII-EBCDIC 转换。我们采用的方法是以 ASCII 格式发送消息。这意味着 IBM i/OS 上的程序需要进行消息转换。

### 8.1.2 字节序

IBM eServer 系统使用 Power 处理器。Power 架构与 Intel x86 架构的区别之一是字节序。

一个 32 位整数在计算机内存中始终表示为四个字节。在 PowerPC 系统上，对于如 `0xA0B8COD` 的字节，`0xA0` 字节存储在第一个内存，`0xB8` 字节存储在第二个内存中。然而，在 x86 上，最低字节存储在第一个内存中，这被称为小端 (little endian)。最高有效字节存储在第一个内存中，这被称为大端 (big endian)。

| 十进制值 | 大端序 | 小端序 |
| :--- | :--- | :--- |
| 125 | `0x0000007D` | `0x7D000000` |
| 200 | `0x000000C8` | `0xC8000000` |
| 256 | `0x00000100` | `0x00000001` |
| 292 | `0x00000124` | `0x24000001` |

```c
iconv_t convertTable;
#endif

/* socket() 变量 */
int descriptor,
addressFamily,
type,
protocol;

/* sendto() 变量 */
int bufferLength,
flags,
serverLength,
struct sockaddr_in serverAddress;

/* gethostbyname() 变量 */
struct host *host;
```

```c
/* 读取输入变量* */

if (argc > 2) {

    bufferLength = strlen(argv[2]) < BUFFER_SIZE ? argv[2] : BUFFER_SIZE;

    strncpy(buffer, argv[2], bufferLength);

} else {

    strcpy(buffer, "Default data");

    bufferLength = strlen(buffer);

}
```

```c
/* 打开 socket 描述符 */

addressFamily = AF_INET;

type = SOCK_DGRAM;

protocol = IPPROTO_IP;

if ((descriptor = socket(addressFamily, type, protocol)) < 0) {

    printf("Error getting socket descriptor\n");

    printf("errno is %s\n", errno);

    exit(-1);

}
```

```c
#ifdef _OS5400_

/* 仅在 IBM I5/OS* 上设置转换表 */

memcpy(toCCID.name, "IBMCCID", 8);

memcpy(toCCID.ccid, "01252", 5);

memset(toCCID.RESERVED, 0x00, 19);

memcpy(fromCCID.name, "IBMCCID", 8);

memcpy(fromCCID.ccid, "00037", 5);

memcpy(fromCCID.conversion, "000", 3);

memcpy(fromCCID.substitute, "0", 1);

memcpy(fromCCID.shift, "0", 1);

memcpy(fromCCID.input, "0", 1);

memcpy(fromCCID.option, "0", 1);

memset(fromCCID.RESERVED, 0x00, 12);

convertTable = iconv_open((char *)&toCCID, (char *)&fromCCID);

if (convertTable.return_value < 0) {

    printf("Error creating conversion table\n");

}
```

```c
printf("errno is %i\n", errno);

close(descriptor);

exit(-1);
```

```c
/* 转换数据 */

convertBufferLength = inBufferLength = strlen(buffer);

inBuffer = buffer;

convertBuffer = converted;

memset(converted, 0x00, sizeof(converted));

iconv(converted, &inBuffer, &inBufferLength, &convertBuffer, &convertBufferLength);

else

memcpy(converted, buffer, bufferLength);

#endif
```

```c
/* 获取服务器地址 */

memset(serverAddress, 0x00, sizeof(serverAddress));

strncpy(server, argv[1]);

if ((serverAddress.sin_addr.s_addr = inet_addr(server)) == (unsigned)

INADDR_NONE) {

    host = gethostbyname(server);

    if (host == (struct host *)NULL) {

        printf("h_errno is %d\n", errno);

        close(descriptor);

        exit(-1);

    }
```

```c
/* 向服务器发送消息 */

flags = 0;

serverAddress.sin_family = AF_INET;

serverAddress.sin_port = htons(SERVER_PORT);

serverLength = sizeof(serverAddress);

rc = sendto(descriptor, converted, bufferLength, flags,

(struct sockaddr *)&serverAddress);

if (rc < 0) {

    printf("Error sending requests\n");

    printf("errno is %i\n", errno);

    close(descriptor);

    exit(-1);

}
```

```c
/* 关闭转换表 */

iconv_close(convertTable);

#endif
```

```c
/* 关闭 socket */
```



`close(descriptor);`

`exit(0);`

`/* 结束 * */`

# 100 Linux 与 IBM i5/OS 的集成

## 8.2.2 服务器代码示例

服务器程序是等待待传入消息的程序。它将`socket`绑定到端口`30595`，然后等待入站的消息。如果程序接收到消息，它会将消息打印到标准输出。服务器程序不需要任何参数。

在IBM i/OS上创建服务器程序，请按顺序使用以下命令：

1. `CRTMOD MODULE(ITSOLIB/SERVER) SRCSTMT('/itsdir/src/server.c') TGCCSID(37)`
2. `CRTPGM PGM(ITSOLIB/SERVER) MODULE(ITSOLIB/SERVER) BNDSRPGM(QSYS/QTQICONV)`

示例8-2服务器代码显示了在特定端口等待客户端的消息。当收到消息时，它会被发送到标准输出：Linux版本与ASCII IBM i/OS版本唯一区别在于需要将入站消息转换为EBCDIC。

### 示例 8-2 服务器代码 `server.c`

```c
#include <stdio.h>

#include <stdlib.h>

#include <string.h>

#include <errno.h>

#include <sys/types.h>

#include <sys/socket.h>

#include <netinet/in.h>
```

```c
/*在此处指定服务器程序的 TCP / IP 端口 */
#define SERVER_PORT 30595
#define BACKLOG 2
#define BUFFER_SIZE 256
```

```c
/* 如果操作系统是 i5/OS，则使用以下语句 */
#ifdef _OS400

#include <iconv.h>

typedef struct {
    char name[8];
    char csid[5];
    char conversion[3];
    char substitute[1];
    char shift[1];
    char input[1];
    char option[1];
    char RESERVED[12];
} fromCode_t;

typedef struct {
    char name[8];
    char csid[5];
    char RESERVED[19];
} toCode_t;

#endif
```



```c
int main(int argc, char *argv[])
{
    int rc;
    bufferLength;
    char buffer[BUFFER_SIZE];
    converted[BUFFER_SIZE];
    *inBuffer;
    *convertBuffer;

#ifdef _OS400
/* iconv() 在 i5/OS 上将 ASCII 转换为 EBCDIC */
size_t inBufferLength;
fromCode_t fromCCID;
toCode_t toCCID;
iconv_t convertTable;
#endif

/* socket() 变量 */
int descriptor,
addressFamily,
type,
protocol;

/* bind() 变量 */
struct sockaddr_in localAddress;
int addressLength;

/* recvfrom() 变量 */
int flags,
clientLength;
struct sockaddr_in clientAddress;

/* 打开 socket 描述符 */
addressFamily = AF_INET;
type = SOCK_DGRAM;
protocol = IPPROTO_IP;
if ((descriptor = socket(addressFamily, type, protocol)) < 0) {
    printf("Error getting socket descriptor\n");
    printf("errno is %i\n", errno);
    exit(-1);
}

/* 绑定到 socket */
memset(&localAddress, 0x00, sizeof(localAddress));
localAddress.sin_family = AF_INET;
localAddress.sin_port = htons(SERVER_PORT);
localAddress.sin_addr.s_addr = htonl(INADDR_ANY);
addressLength = sizeof(localAddress);
if ((rc = bind(descriptor, (struct sockaddr *)&localAddress, addressLength)) < 0) {
    printf("Error binding to the socket\n");
    printf("errno is %i\n", errno);
    close(descriptor);
    exit(-1);
}

#ifdef _OS400
/* 仅在 IBM I5/OS 上设置转换表 */
memcpy(toCCID.name, "IBMCCID", 8);
memcpy(toCCID.ccid, "01252", 5);
memset(toCCID.RESERVED, 0x00, 19);
memcpy(fromCCID.name, "IBMCCID", 8);
memcpy(fromCCID.ccid, "00037", 5);
memcpy(fromCCID.conversion, "000", 3);
memcpy(fromCCID.substitute, "0", 1);
memcpy(fromCCID.shift, "0", 1);
memcpy(fromCCID.input, "0", 1);
memcpy(fromCCID.option, "0", 1);
memset(fromCCID.RESERVED, 0x00, 12);
convertTable = iconv_open((char *)&toCCID, (char *)&fromCCID);
if (convertTable.return_value < 0) {
    printf("Error creating conversion table\n");
    printf("errno is %i\n", errno);
    close(descriptor);
    exit(-1);
}
#endif

do {
    /* 接收任何客户端请求 */
    memset(buffer, 0x00, sizeof(buffer));
    bufferLength = sizeof(buffer);
    flags = 0;
    clientLength = sizeof(clientAddress);
    rc = recvfrom(descriptor, buffer, bufferLength, flags,
                  (struct sockaddr *)&clientAddress, &clientLength);
    if (rc < 0) {
        printf("Error receiving client requests\n");
        printf("errno is %i\n", errno);
        close(descriptor);
        exit(-1);
    }

#ifdef _OS400
/* 如果程序在 i5/OS 上运行，则转换数据 */
    convertBufferLength = strlen(buffer);
    inBuffer = buffer;
    convertBuffer = converted;
    memset(converted, 0x00, sizeof(converted));
    iconv(converted, &inBuffer, &inBufferLength, &convertBuffer, &convertBufferLength);
#else
    memcpy(converted, buffer, sizeof(buffer));
#endif

    /* 输出数据 */
    printf("Received data from: %i\n", clientAddress.sin_s_addr);
    printf("%.80s\n", converted);

    /* 当接收到的前4个字符为 'STOP' 时停止 */
} while (strncmp(converted, "STOP", 4) != 0);

#ifdef _OS400
    /* 关闭转换表 */
    iconv_close(convertTable);
#endif

/* 关闭 socket */
close(descriptor);

exit(0);
} /* 结束 * */
```

## 测试 Socket 场景

在客户端和服务器程序编译并准备好运行后，你必须启动服务器 socket 程序来接收消息。你可以以交互模式或批模式运行服务器。在 IBM i/OS 和 Linux 上，发送到服务器的消息都会输出到标准输出。要在 IBM i/OS 上交互式运行服务器，请使用命令 `CALL ITSOLIB/SERVER`。要在 Linux 上交互式运行服务器，请使用 `.server` 命令。

- 在 IBM i/OS 上：

`SBJMJOB CMD ITSOLIB/SERVER`

提交一个批处理作业，默认情况下，标准输出将进入池文件。

- 在 Linux 上：

`linux:> server > output.file &`

启动一个后台作业并将标准输出重定向到当前目录下的 `output.file`。

现在你可以向你的服务器发送消息了。要在 IBM i/OS 上运行客户端程序，可以使用以下命令：

`CALL ITSO/CLIENT PARM(Servername) "This is my text message")`

这里，`Servername` 是你想发送消息的服务器的主名或 IP 地址。要结束服务器程序，请发送 `STOP` 消息。在 Linux 上，你可以运行：

`client Servername "This is my text message"`

示例 8-3 是在 Linux 系统上运行的服务器生成的输出示例。

### 示例 8-3 服务器输出

```
linux:> server
Received data from: 1513462665
'This is a message from iSeries'
```

```
Received data from: 1513462666
'This is text from Linux'
```

```
Received data from: 1513462666
'STOP'
```

```
linux:>
```

![](img/165c050f45ac58e1635258993855261a_118_0.png)

## 使用 i5/OS 投影配置构建 SSO 场景



本章讨论了为登录 `i5/OS`、`Linux` 和 `Windows` 机器的用户提供单点登录 (SSO) 解决方案的规划与实现。这里介绍的方法是一种自定义方案，你可以构建该方案以实现用户可以使用单一的用户名或密码登录。

本章将讨论以下内容：

- 什么是单点登录：视角
- 单点登录的需求与优势
- 实施单点登录的场景
- 实施单点登录的策略
- 配置 `Linux` 和 `Samba` 服务器以进行 `Windows` 认证
- `Linux` 与 `i5/OS` 轻量级目录访问协议 (LDAP) 的集成
- 配置 `Windows` 客户端以通过 `Samba` 服务器进行认证

## 场景描述

这定义了我们所说的单点登录，并对正在实施的场景进行了简要描述。

## 什么是单点登录

另一种定义可以称为“使用相同的凭据访问整个网络中的资源，每次访问新资源时，系统可能会提示你进行认证”。为了本章的目的，我们坚持后者的定义。

## 单点登录的需求：我们的视角

尽管我们非常希望保持简单，但当今的业务需求已变得非常复杂，因此没有单一系统可以完成你可能想要的所有操作。这是一个复杂的 IT 基础设施，其中我们利用了各种软件、硬件等技术的组合。这带来了管理和集成这些关键组件的复杂性。在场景中，最痛苦的领域之一就是管理和维护所有异构进程的授权系统。这就是单点登录概念的用武之地。

简单来说，单点登录是用户能够利用单组凭据访问所有这些系统的能力。用户可以使用用户名或密码、生物识别设备、智能手表或任何机制进行认证。其基本原理是他必须能够使用同一组凭据访问资源。如果没有这种机制，一个人几乎无法记住访问不同资源可能所需的不同凭据。

发现某一个人记住并记住他所使用的各种系统的十几个不同凭据是很常见的现象。这除了是一个安全问题外，还可能是一个巨大的管理负担和个人开销。保护单一用户名/密码要比保护十几个要容易得多。

## 单点登录的优势

通过登录，其目的是减少这种复杂性，并使用相同的凭据整合所有系统。用户需要使用相同的凭据对不同的系统进行认证。单一的用户名/密码就足够让他访问他所切换的系统。同样，如果他需要更改凭据，更改一次密码就足够。

## 实施单点登录的场景

本节概述了你可以用于实施单点登录的场景。

### 当前场景

以下描述了当前场景：

- 组织名称为国际技术支持组织 (ITSO)
- ITSO 主要为其用户使用 `Windows` 客户端（`Windows XP SP2`、`Windows 2000 Professional`、`Windows SP4`、`Windows 98` 和 `Windows 95`）和 `Linux` 客户端。
- ITSO 将 `IBM i/OS` 和 `SUSE Linux Enterprise Server 10` 作为其主要操作系统。
- ITSO 在 `Linux` 上使用 `Samba` 作为其主域控制器 (PDC)，用于认证 `Windows` 客户端。域名为 `ITSODMN`。
- 所有用户至少有三组用户名/密码，使他们能够分别登录到 `i/OS`、`Linux` 和 `Samba` 服务器并利用资源。

### 预期场景

以下描述了预期场景：

- 所有用户必须有一个单一的用户名/密码来访问所有三个服务器。
- 用户创建/修改和常规维护的单一点。
- 单次密码更改必须同步到所有三个系统。

`图-1` 帮助你理解本章涉及的整体场景。

| `i5/OS` 服务器 | | `Windows` 客户端 |
| :--- | :--- | :--- |
| 通过投影配置导出用户配置到 `Linux` | | • `Windows XP SP2` |
| 通过 `Linux` 上的 `ldapmodify` 完成密码更新 | | • `Windows 2000 Professional SP` |
| `SLES 10` 上的 `Samba PDC` | 认证 | • `Windows 98` |
| • 密码通过 `/etc/samba/passwd` 检查 | | • `Windows 95` |
| • 在 `Linux` `/etc/passwd` 中更新密码 | | |
| • 在 `Linux` `/etc/samba/passwd` 中更新密码 | | |
| • 通过 `ldapmodify` 在 `i/OS` 上更新密码 | 密码更改 | | |

`图 A-1` 场景的逻辑概览

以下是设置系统的步骤，将在本章稍后部分讨论。

1. `i/OS` 托管用户配置。选定的用户配置导出到 `Linux`。
2. 使用 `Linux` 脚本从 `i/OS` 导入投影配置。
3. 在此导入过程中创建 `Linux` 和 `Samba` 用户账户/密码。
4. `Windows` 客户端使用 `i/OS` 用户名/密码进行认证。
5. `Windows` 客户端更改密码，相同的内容将同步到 `Linux/Samba` 和 `i/OS`。
6. `i/OS` 的密码更改通过 `Linux` 上的脚本完成（利用 `ldapmodify` 命令）。

## 实施单点登录的策略

本节概述了在组织中实施单点登录机制之前必须遵循的过程。这些是你评估实施单点登录可行性时必须遵循的步骤。

在设置系统之前，我们建议牢记以下几点：

- 组织名称为国际技术支持组织 (ITSO)
- ITSO 主要为其用户使用 `Windows` 客户端（`Windows XP SP2`、`Windows 2000 Professional`、`Windows SP4`、`Windows 98` 和 `Windows 95`）和 `Linux` 客户端。
- ITSO 将 `IBM i/OS` 和 `SUSE Linux Enterprise Server 10` 作为其主要操作系统。
- ITSO 在 `Linux` 上使用 `Samba` 作为其主域控制器，用于认证 `Windows` 客户端。域名为 `ITSODMN`。
- 所有用户至少有三组用户名/密码，使他们能够分别登录到 `i/OS`、`Linux` 和 `Samba` 服务器并利用资源。
- 所有的用户必须有一个单一的用户名/密码来访问所有三个服务器。
- 用户创建/修改和常规维护的单一点。
- 单次密码更改必须同步到所有三个系统。

- 单点登录，简单来说，是用户能够利用单组凭据访问所有这些系统的能力。用户可以使用用户名或密码、生物识别设备、智能手表或任何机制进行认证。其基本原理是他必须能够使用同一组凭据访问资源。如果没有这种机制，一个人几乎无法记住访问不同资源可能所需的不同凭据。
- 通过登录，其目的是减少这种复杂性，并使用相同的凭据整合所有系统。用户需要使用相同的凭据对不同的系统进行认证。单一的用户名/密码就足够让他访问他所切换的系统。同样，如果他需要更改凭据，更改一次密码就足够。
- 保护单一用户名/密码要比保护十几个要容易得多。
- 发现某一个人记住并记住他所使用的各种系统的十几个不同凭据是很常见的现象。这除了是一个安全问题外，还可能是一个巨大的管理负担和个人开销。
- 另一种定义可以称为“使用相同的凭据访问整个网络中的资源，每次访问新资源时，系统可能会提示你进行认证”。为了本章的目的，我们坚持后者的定义。

- 什么是单点登录：视角
- 单点登录的需求与优势
- 实施单点登录的场景
- 实施单点登录的策略
- 配置 `Linux` 和 `Samba` 服务器以进行 `Windows` 认证
- `Linux` 与 `i5/OS` 轻量级目录访问协议 (LDAP) 的集成
- 配置 `Windows` 客户端以通过 `Samba` 服务器进行认证
1. `i/OS` 托管用户配置。选定的用户配置导出到 `Linux`。
2. 使用 `Linux` 脚本从 `i/OS` 导入投影配置。
3. 在此导入过程中创建 `Linux` 和 `Samba` 用户账户/密码。
4. `Windows` 客户端使用 `i/OS` 用户名/密码进行认证。
5. `Windows` 客户端更改密码，相同的内容将同步到 `Linux/Samba` 和 `i/OS`。
6. `i/OS` 的密码更改通过 `Linux` 上的脚本完成（利用 `ldapmodify` 命令）。

## 实施单点登录的策略

本节概述了在组织中实施单点登录机制之前必须遵循的过程。这些是你评估实施单点登录可行性时必须遵循的步骤。

在设置系统之前，我们建议牢记以下几点：

- 组织名称为国际技术支持组织 (ITSO)
- ITSO 主要为其用户使用 `Windows` 客户端（`Windows XP SP2`、`Windows 2000 Professional`、`Windows SP4`、`Windows 98` 和 `Windows 95`）和 `Linux` 客户端。
- ITSO 将 `IBM i/OS` 和 `SUSE Linux Enterprise Server 10` 作为其主要操作系统。
- ITSO 在 `Linux` 上使用 `Samba` 作为其主域控制器，用于认证 `Windows` 客户端。域名为 `ITSODMN`。
- 所有用户至少有三组用户名/密码，使他们能够分别登录到 `i/OS`、`Linux` 和 `Samba` 服务器并利用资源。
- 所有用户必须有一个单一的用户名/密码来访问所有三个服务器。
- 用户创建/修改和常规维护的单一点。
- 单次密码更改必须同步到所有三个系统。



# 单点登录概述

- 单点登录，简单来说，是用户能够利用单组凭据访问所有这些系统的能力。用户可以使用用户名或密码、生物识别设备、智能手表或任何机制进行认证。其基本原理是他必须能够使用同一组凭据访问资源。如果没有这种机制，一个人几乎无法记住访问不同资源可能所需的不同凭据。

- 通过登录，其目的是减少这种复杂性，并使用相同的凭据整合所有系统。用户需要使用相同的凭据对不同的系统进行认证。单一的用户名/密码就足够让他访问他所切换的系统。同样，如果他需要更改凭据，更改一次密码就足够。

- 保护单一用户名/密码要比保护十几个要容易得多。

- 发现某一个人记住并记住他所使用的各种系统的十几个不同凭据是很常见的现象。这除了是一个安全问题外，还可能是一个巨大的管理负担和个人开销。

- 另一种定义可以称为“使用相同的凭据访问整个网络中的资源，每次访问新资源时，系统可能会提示你进行认证”。为了本章的目的，我们坚持后者的定义。

## 什么是单点登录：视角

- 单点登录的需求与优势
- 实施单点登录的场景
- 实施单点登录的策略
- 配置 Linux 和 Samba 服务器以进行 Windows 认证
- Linux 与 i5/OS 轻量级目录访问协议 (LDAP) 的集成
- 配置 Windows 客户端以通过 Samba 服务器进行认证

## 实施步骤

1. i/OS 托管用户配置。选定的用户配置导出到 Linux。
2. 使用 Linux 脚本从 i/OS 导入投影配置。
3. 在此导入过程中创建 Linux 和 Samba 用户账户/密码。
4. Windows 客户端使用 i/OS 用户名/密码进行认证。
5. Windows 客户端更改密码，相同的内容将同步到 Linux/Samba 和 i/OS。
6. i/OS 的密码更改通过 Linux 上的脚本完成（利用 `ldapmodify` 命令）。

# 下载场景

要获取场景包，你可以从 IBM Redbooks 网站下载。

- Go：`http://www.ibm.com/redbooks/24651`
- 下载 `scripts.zip` 文件。

![](img/165c050f45ac58e163525893855261a_121_0.png)

# i/OS 侧设置

本节讨论了如何设置 i/OS 侧的环境。

## 在 i/OS 上还原库

首先，你需要在 i/OS 上还原库。

## 配置 i/OS LDAP 支持

配置 i/OS LDAP 支持需要还原 `linuxusers.savef`。你可以通过以下步骤完成：

1. 首先使用 `ftp` 将 `linuxusers.savef` 文件传输到 i/OS 系统。在 Windows PC 上，切换到解压后的 `scripts.zip` 文件目录。
2. 建立 i/OS 系统的 `ftp` 会话，例如：
   ```
   ftp i5-os-system
   ```
3. 在 `ftp` 会话中更改格式以正确识别 DOS 样式：
   ```
   quote name fmt
   ```
4. 在 `ftp` 会话中更改传输类型以正确传输二进制文件：
   ```
   bin
   ```
5. 在 `ftp` 会话中，从 PC 将保存文件传输到 i/OS：
   ```
   put linuxusers.savef linuxusers.savef
   ```
6. 退出 `ftp` 会话：
   ```
   quit
   ```

## 还原保存文件

执行以下步骤还原已正确传输到 i/OS 分区的保存文件：

1. 在 i5/OS 中，执行以下命令以确保保存文件已正确传输到 i/OS 分区：
   ```
   DSPSAF FILE(QPL/LINUXUSERS)
   ```
2. 在 i5/OS 中，使用以下命令还原保存文件：
   ```
   RSTLIB USRPRF(LINUXUSERS) DEV(*SAVF) SAVF(*QPL/LINUXUSERS)
   ```

## 创建用户配置文件

为了在 Linux 和 i/OS LDAP 组件之间建立必要的握手，需要建立两个用户账户。第一个用户配置文件 (`linuxsys1`) 用于 Linux LDAP 访问 i/OS 的 LDAP 服务器。在 i5/OS 中必须执行以下命令来创建该用户配置文件：

```
CTRTRUSPRF USRPRF(LINUXSYS1) PASSWORD(*1dlapacc) USRLCS(*SECADM) INLMNU(*SIGNOFF) LMTCPB(*YES) G(*NONE)
```

第二个用户配置文件，我们称之为 Linux 组配置 (`linuxys1g`)，用于将所有需要赋予 Linux 访问权限的用户账户归为一个组：

```
CRUSRPPRF USRPRF (LINUXYS1G) PASSWORD(*NONE) INLNU (*SIGNOFF) LMCPB(*YES) GID(*GEN)
```

## 将用户添加到 Linux 组配置

现在，将所有现有的 i/OS 用户（你希望包含在此场景中的用户）添加到 `linuxys1g` 组配置中。要完成此操作，你必须在 i5/OS 上输入以下命令：

```
CHUGUSRPF (CURUSR) GRPPRF (LINUXYS1G)
```

将 `CURUSR` 替换为需要包含在 `linuxys1g` 组中的实际用户名。根据你的设置，对该场景中需要配置的所有用户重复此命令。

## 执行所需的命令

在 i5/OS 中的所有用户配置文件都添加到 `linuxys1g` 组后，需要使用以下命令初始化并重建 i5/OS 中的组列表：

```
CHCGIL8 LINUXERS
```

- `RMVLNXUSRS (LINUXYS1) LINUXGRP (LINUXYS)`

`RMVLNXUSRS` 命令禁用 Linux 中的用户。具体而言，`RMVLNXUSRS` 命令会清空 Linux 用户列表。

- `ADDLNXUSRS LINUXYS (LINUXYS1) LINUXGRP (LINUXYS)`

`ADDLNXUSRS` 命令启用 Linux 中的用户。具体而言，`ADDLNXUSRS` 命令会通过查找所有属于 Linux 组（如果为 `LINUXYS1G`）的 i5/OS 用户配置文件并将其添加到 Linux 列表中来重建 Linux 用户列表。

> 注意：每当有 i/OS 中的用户配置文件添加到或从 `linuxys1g` 组中移除时，请执行这些命令。

此外，运行 Linux 命令 `doall/dingle`。

# Linux 端的设置

本节描述了 Linux 侧场景的设置程序。

## OpenLDAP 客户端配置

将 OpenLDAP 客户端配置文件 (`ldap.conf`) 放在 `/etc/openldap` 目录下，并对其进行修改以反映正在使用的 LDAP 环境。

## 将 ldap.conf 文件传输到 Linux 系统

在 Windows 客户端 PC 上，切换目录到解压 zip 文件层次结构中的 OpenLDAP 目录。

使用以下步骤将 `ldap.conf` 文件传输到 Linux 系统（在已登录 PC 客户端的情况下）：

1. 登录 `ftp` 后，切换目录到 `/usr/src/linuxusers` 目录：
   ```
   cd /etc/ldap
   ```
2. 在 `ftp` 会话中传输 `ldap.conf` 文件：
   ```
   put ldap.conf
   ```
3. 退出 `ftp` 会话：
   ```
   quit
   ```

## 修改 LDAP 配置文件以匹配环境

将 `ldap.conf` 文件中的 `host` 值更改为获取用户文件的 i/OS 分区的名称（或 IP 地址）。

此外，更改 `base` 值以匹配根据你的配置设置的默认 base DN。示例场景中使用的默认值是：

`base cn=accounts,os400-sys=rchas61.rchland.ibm.com`

根据你的设置进行相应更改。

更改 "rootbindn" 值以匹配默认 base DN。此外，你还必须指定 `os400-sys` 配置。这是为了支持 LDAP 查询创建的用户配置文件 (`linuxsys1`)。这不是组名配置。

示例-1 显示了基于示例中使用的设置的 `ldap.conf` 文件。

示例：基于示例中设置的 A-1 `ldap.conf` 文件

```
# LDAP Defaults
#
# 详情请参 ldap.conf(S)
# 此文件应该是所有人可读但不可对所有人可写的。
#BASE dc=example, dc=com
#URI ldap://ldap.example.com ldap://ldap-master.example.com:666
#SIZELIMIT 12
#TIMELIMIT 15
#DEREF never

host 9.5.92.96

base cn=accounts,os400-sys=rchas61.rchland.ibm.com
```



# TLS_REQCERT allow

```
#TLS_REQCERT allow
```

# 存储 LDAP 密码

最后，你必须将用于 LDAP 查询的密码存储在`/etc/ldap.secret`文件中。确保密码末尾有一个换行（意味着返回/回车）。此外，你必须更改文件的模式（权限），使得只有`root`可以查看文件（`chmod 600 /etc/ldap.secret`）。

# Samba 配置

本节讨论了在 SUSE Linux Enterprise 10 上配置 Samba Server 3.0.xx 的步骤。将 Samba 配置为 Windows-NT PDC，并配置其将用户密码与 Linux 密码数据库同步。

在 SUSE Linux Enterprise Version 10 上需要安装以下包以实现正确的 Samba 功能。请确保安装了以下包。执行以下步骤：

1. 使用 Linux 命令检查相关软件包。在执行此命令之前，请以`root`用户登录：

   2. 登录`ftp`后，切换目录到`/etc/ldap`

   3. 在`ftp`会话中传输`ldap.conf`文件

   4. 退出`ftp`会话

# 修改配置文件以匹配环境

将`ldap.conf`文件中的`host`值更改为获取用户文件的 i/OS 分区的名称（或 IP 地址）。

此外，更改`base`值以匹配根据你的配置设置的默认 base DN。示例场景中使用的默认值是：

`base cn=accounts,os400-sys=rchas61.rchland.ibm.com`

根据你的设置进行相应更改。

更改`rootbindn`值以匹配默认 base DN。此外，你还必须指定`os400-sys`配置。这是为了支持 LDAP 查询创建的用户配置文件 (`linuxsys1`)。这不是组名配置。

示例-1 显示了基于示例中使用的设置的`ldap.conf`文件。

示例：基于示例中设置的 A-1 `ldap.conf`文件

```
# LDAP Defaults
#
```

```
# 详情请参 ldap.conf(S)
# 此文件应该是所有人可读但不可对所有人可写的。
#BASE dc=example, dc=com
#URI ldap://ldap.example.com ldap://ldap-master.example.com:666
#SIZELIMIT 12
#TIMELIMIT 15
#DEREF never
```

`host 9.5.92.96`

`base cn=accounts,os400-sys=rchas61.rchland.ibm.com`

```
rootbindn os400-profile-linuxsys1,cn=accounts,os400-sys=rchas61.rchland.ibm.com
pam_login_attribute os400-profile
ldap_version 3
SASL_SECPROPS none
```

```
#TLS_REQCERT allow
```

# 存储 LDAP 密码

最后，你必须将用于 LDAP 查询的密码存储在`/etc/ldap.secret`文件中。确保密码末尾有一个换行（意味着返回/回车）。此外，你必须更改文件的模式（权限），使得只有`root`可以查看文件（`chmod 600 /etc/ldap.secret`）。

# Samba 配置

本节讨论了在 SUSE Linux Enterprise 10 上配置 Samba Server 3.0.xx 的步骤。将 Samba 配置为 Windows-NT PDC，并配置其将用户密码与 Linux 密码数据库同步。

在 SUSE Linux Enterprise Version 10 上需要安装以下包以实现正确的 Samba 功能。请确保安装了以下包。执行以下步骤：

1. 使用 Linux 命令检查相关软件包。在执行此命令之前，请以`root`用户登录：

   2. 登录`ftp`后，切换目录到`/etc/ldap`

   3. 在`ftp`会话中传输`ldap.conf`文件

   4. 退出`ftp`会话

# 场景脚本配置

若干文件需要安装（或拷贝）到 Linux 分区。这些文件是你之前提取的`scripts.zip`文件的一部分。

# 安装 doall 脚本

使用以下命令在 Linux 中安装脚本：

1. 在 Linux 中创建一个目录来存放脚本：

   `mkdir /usr/src/linuxusers`

2. 在 Windows PC 上，切换目录到解压`scripts.zip`文件层次结构中的`bin`目录。

3. 从脚本所在的 Windows PC，启动到 Linux 系统的`ftp`会话：

   `ftp linux-system`

4. 登录`ftp`后，切换目录到`/usr/src/linuxusers`目录：

   `cd /etc/ldap`

5. 在`ftp`会话中更改类型以正确传输二进制文件：

   `bin`

6. 在`ftp`会话中传输`doall`脚本：

   `put doall doall`

7. 退出`ftp`会话：

   `quit`

# 配置脚本

在`doel`脚本中有三个值（变量）需要进行修改，以匹配`idapconf`配置文件中设置的`idap`配置值。

- 修改`$dn`值以反映之前为支持扩展用户配置文件 (`os400-profile`) 建立的 i5/OS 配置文件 (`linuxsys1`)，以及`idap`用户来源的 i5/OS 系统 (`os400-sys`)。使用我们书中的示例以及示例的`idapconf`，请更改`doel`脚本中的`$dn`值以反映以下内容：
  > `$dn = 'os400-profile=linuxsys1,cn=accounts,os400-sys=rchas61.rhland.ibmcom';`

- 此外，修改`$b`值以反映`idap`用户来源的系统名称 (`os400-sys`)。使用示例的`idapconf`，请更改`$b`脚本（此处应为`$`值）以反映以下内容：
  > `$b = 'os400-sys=rchas61.rhland.ibmcom';`

- 最后，修改`$h`值以反映`idap`用户来源的系统主机名。确保该名称可以通过域名系统 (DNS) 或 Linux 上的`/etc/hosts`文件进行解析。使用示例`$h`值将反映以下内容：
  > `$h = 'rchas61'`

# 执行 doel 脚本

你必须在完成 i5/OS 设置步骤后执行`doel`脚本。只需输入以下命令即可执行：

`# perl /usr/src/linuxusers/doall`

> 注意：此脚本旨在用于从 i5/OS 导入用户时首次运行。在导入期间，它会将这些用户的用户名和密码设置为默认值。默认密码与 Linux 服务器和 Samba 服务器上的用户名相同。

# 安装 chgi5user, chguser, smchat 和 smgbpass 脚本

将 Windows PC 上`bin`文件夹中的其余脚本安装到 Linux 的`/usr/local/bin`目录中。执行以下命令来完成相同操作：

1. 在 Windows PC 上，将目录切换到解压后的`scripts.zip`文件层级中的`bin`目录。

2. 在位于脚本的 Windows PC 上，启动到 Linux 系统的`ftp`会话：
   > `ftp linux-system`

3. 登录`ftp`后，切换目录到`/usr/local/bin`目录：
   > `cd /usr/local/bin`

4. 在`ftp`会话中更改传输类型以正确传输二进制文件：
   > `bin`

5. 在`ftp`会话中传输以下脚本：
   > `put chgi5pass`
   > `put chguser`
   > `put smchat`
   > `put smbpass`

6. 退出`ftp`会话：
   > `quit`

## 详细逻辑流

支持投影用户配置文件需要在 i/OS 和 Linux 中安装多个文件。如你现在所意识到的，整个过程相当复杂，你可能需要真正理解系统的工作原理。本节详细解释了所有脚本的作用、功能以及它们之间的关系。在你根据特定情况或需求更改或调整场景时可能可能理解此流程。

- `ldap.conf`

  Linux 客户端使用 OpenLDAP 配置文件。

- `doall`

  Perl 脚本，从 i/OS 导入带有投影配置文件的用户，并在 Linux Samba 服务器中创建相应的用户。它会创建 Linux 系统用户和 Samba 用户。旨在用于从 i/OS 导入用户时首次运行。它会将 Linux 和 Samba 用户的用户名和密码重置为默认值。密码的默认值与用户名相同。

- `smmpass`



`Bash`脚本，由`doall`调用，并初始化添加到`Samba`的新用户的密码。默认密码与用户的用户名相同。这是创建并设置所有用户`Samba`密码的脚本。它由`doall`自动调用，不需要你单独运行。

- `smbchat`

主密码同步脚本。通过`smb.conf`文件中的`passwwdm`参数调用。

- `chg5user`

`Bash`脚本，由`Samba`服务器通过`smb.conf`文件中的`passwd`参数调用。该文件的目的是查找并更改`i/OS`和本地`Linux`系统中用户的密码。`Samba`负责更改`Samba`数据库内部的密码。此脚本也会被`chguser`和`smbchat`调用。

# 向域添加新用户

本节提供了向域中添加新用户的信息，该域是在第 108 页的“初始环境设置”中设置的。

# 前提检查点

我们假设你已经安装并配置了场景包。你可以通过在`i/OS`终端上执行以下命令来检查这一点：

- 在`i/OS`侧：

```
DSPBJ0D OBJ(QSYS/LINUXUSERS) TYPE(*LIB)
```

- 在`Linux`侧：

检查`/etc/openldap/ldap.conf`文件的存在性和正确性。

检查`/etc/samba/smb.conf`文件的存在性和正确性。

检查`/usr/local/bin`目录下的以下文件的存在性和正确性：

- `chgi5user`

- `chguser`

- `smbchat`

- `smbpass`

检查`/usr/src/linuxusers`目录下的以下文件的存在性和正确性：

- `doall`

# 在 Linux 上设置

支持投影用户配置文件需要在`i/OS`和`Linux`中安装多个文件。如你现在所意识到的，整个过程相当复杂，你可能需要真正理解系统的工作原理。本节详细解释了所有脚本的作用、功能以及它们之间的关系。在你根据特定情况或需求更改或调整场景时可能需要理解此流程。

*(注：原文后续存在大量重复的段落，已按要求处理，未进行重复输出)*

注意：此脚本旨在您向`i/OS`添加新用户并希望将其用户导入到`Linux`和`Samba`时运行。此脚本的作用与`doall`脚本完全相同，但它不会为这些新用户创建密码或`Samba`账户。调用`chguser`脚本来设置`Linux`用户的密码并创建他们的`Samba`用户名/密码。我们建议您在即时添加用户过程中运行此脚本。首次使用`doall`脚本进行导入时。

## 执行 chguser 脚本

在使用先的`dosingle`脚本导入新用户后，您现在需要设置他们的密码。为了简单起见，我们假设所有`i/OS`用户在创建时使用的密码与其用户名相同，以便在将其导入`Linux`时保持其完整性。随后，调用`chguser`脚本并传入两个参数：用户名和密码。该脚本会自动为`Linux`系统中的用户和`Samba`密码文件设置密码。对您在`i/OS`中添加并使用`dosingle`脚本导入的所有用户重复此操作。

您可以如下执行`chguser`脚本。在`Linux`命令行提示符上输入以下内容：

```
# /usr/local/bin/chguser username password
```

## 详细逻辑流

支持的用户配置文件在`i/OS`和`Linux`中都要安装若干数量的文件。正如您现在可能意识到的，整个过程相当复杂，您可能需要理解系统是如何运行的。接下来的章节详细解释了所有脚本的作用、功能及其之间的关系。如果您需要更改或调整场景以适应您的特定情况或需求，您可能需要理解这一流程。

- `dosingle`: 脚本，用于从`i/OS`导入具有预设配置的新用户。此脚本导入`i/OS`中所有具有预设配置的用户，并在`Linux`服务器上创建相应的用户。它只创建`Linux`系统用户。此脚本不会重置`Linux`和`Samba`服务器中已存在的`i/OS`用户的密码。需要使用`chguser`脚本为这些新用户设置`Linux`密码并创建`Samba`密码。

- `chguser`: 调时带有两个参数：用户名（`username`）和密码（`password`）的`Bash`脚本。每运行一次此脚本，它都会将`Linux`用户的密码设置为提供的值。它还会设置`Samba`用户的密码。如果`Samba`用户不存在，则会创建`Samba`用户。此脚本旨在用于您之前已利用`doall`脚本导入了大部分`i/OS`用户的情况。这是您运行`ringle`脚本后的后续操作。

- `chgiuser`: `Samba`服务器通过`sm.conf`文件中的`passwd`参数调用的`Bash`脚本。该文件的目的是查找并更改`i/OS`和本地`Linux`系统用户的密码。`Samba`负责更改`Samba`密码数据库的密码。该脚本在相关情况下也会`chguser`和`smbchat`脚本调用。

## 配置 Windows 客户端通过 Samba 服务器认证

本节介绍了将`Windows`客户端整合到`Linux/SAMBA`托管域和文件服务器环境中需要遵循的步骤。所示步骤涵盖了以下内容：

1. 将`Windows`客户端加入域

2. 用户更改密码时遵循的过程

针对以下客户端提供了步骤：

- `Windows 95`

- `Windows 98`

- `Windows NT Workstation`

- `Windows 2000 Professional`

- `Windows XP Professional`

您必须注意，`Windows XP Home`不能参与此环境。`Windows XP Home`未提供允许加入`Windows`风格域的机制。

## Windows 95：加入域

执行以下步骤：

1. 进入“网络属性”（`Network Properties`）。

2. 选择`TCP/IP`，然后点击“属性”（`Properties`）窗口。

3. 点击“`WINS`配置”选项卡。

4. 选中“启用`WINS`解析”（`Enable WINS Resolution`）单选按钮，并如图 A-3 所示输入主`WINS`服务器的`IP`地址。这是`Linux`服务器的`IP`地址。

![](img/165c050f45ac58e1635258993855261a_133_0.png)

5. 从图 A-3 点击“绑定”（`Bindings`）选项卡。然后点击如图 A-4 所示微软网络客户端（`Client for Microsoft Networks`）前面的单选按钮。点击“确定”。

![](img/165c050f45ac58e1635258993855261a_134_0.png)

6. 选择“微软网络客户端”，然后如图 A-5 所示点击“属性”（`Properties`）按钮。

![](img/165c050f45ac58e1635258993855261a_134_1.png)

附录 A. 使用 i5/OS 预设配置构建 OS 场景 121

7. 勾选“登录`Windows NT`域”（`Log on Windows NT domain`）复选框，并在`Windows NT`域中输入`ITS0MN`，如图-6 所示选择“确定”按钮。

![](img/165c050f45ac58e1635258993855261a_135_0.png)

图 A-6 提供 Windows NT 域名

8. 回到网络对话框，点击“确定”按钮。系统提示您重启客户端系统。

9. 当客户端重启时，将如图 A-7 所示提示输入用户名、密码和域。

![](img/165c050f45ac58e1635258993855261a_135_1.png)

图 A-7 提供用户名、密码和域名

10. 输入在`Linux`系统上定义的用户名和密码。域输入`ITS0MN`作为域名，然后点击“确定”按钮。

## Windows 95：更改密码

执行以下步骤：

1. 打开“我的电脑”。

2. 如图 A-8 所示打开“控制面板”。

![](img/165c050f45ac58e1635258993855261a_136_0.png)

图 A-8 打开控制面板

3. 在控制面板中，双击“密码”（`Passwords`），进入如图 A-9 所示的屏幕。

![](img/165c050f45ac58e1635258993855261a_136_1.png)

图 A-9 更改 Windows 密码 (1-2)

4. 点击“更改`Windows`密码”（`Change Windows Password`）按钮，进入如图 A-10 所示的屏幕。

![](img/165c050f45ac58e1635258993855261a_137_0.png)

图 A-10 更改密码 (2)

5. 在更改 密码对话框中，选择“微软网络”前面的单选按钮。点击“确定”。在更改 密码对话框中提供旧密码和新密码，然后如图 A-11 所示点击“确定”。

![](img/165c050f45ac58e1635258993855261a_137_1.png)

图 A-11 更改密码后的成功对话框

6. 系统如图 A-12 所示显示密码更改后的成功对话框。



![](img/165c050f45ac58e1635258993855261a_137_2.png)

图 A-12 密码确认屏幕

## Windows 98：加入域

执行以下步骤：

1. 右键点击“网络邻域”，选择“属性”。

2. 点击“微软网络客户端”，然后点击“属性”。

3. 选中“登录 Windows NT 域”前面的复选框。

4. 如图 A-13 所示在 Windows NT 域字段输入 `ITS0MN`。

![](img/165c050f45ac58e1635258993855261a_138_0.png)

图 A-13 微软网络属性

5. 点击“确定”。

6. 回到网络对话框，点击 `TCP/IP`，然后点击“属性”。

7. 点击“WINS 配置”选项卡。

8. 选中“启用 WINS 解析”前面的单选按钮。

9. 输入 Linux 服务器的 IP 地址。

10. 如图 A-14 所示点击“添加”按钮。

![](img/165c050f45ac58e1635258993855261a_138_1.png)

图 A-14 启用 WINS 解析

11. 点击“绑定”选项卡

12. 如图 A-15 所示勾选“微软网络客户端”项。

点击“确定”。

## TCP/IP 属性

![](img/165c050f45ac58e1635258993855261a_139_0.png)

图 A-15 设置网络的传输控制协议/网协议 (`TCP/IP`) 属性

13. 回到网络对话框，点击“标识”选项卡。

14. 确保计算机名称设置正确，且工作组反映域 `ITSDOMN`，如图 A-16 所示。

![](img/165c050f45ac58e1635258993855261a_139_1.png)

图 A-16 提供域名

15. 点击 `OK` 按钮。

16. 重启客户端。

17. 客户端重启后，登录框必须显示如图 A-17 所示的域名称。

![](img/165c050f45ac58e1635258993855261a_140_0.png)

图 A-17 修改用户名、密码和域名

18. 输入用户名并点击 `OK` 按钮。

## Windows 98：更改密码

执行以下步骤：

1. 打开“我的电脑”。

2. 打开“控制面板”。

3. 双击“密码”，如图 A-18 所示。

![](img/165c050f45ac58e1635258993855261a_140_1.png)

图 A-18 修改 Windows 密码 (1-3)

4. 点击“更改 Windows 密码”按钮。

5. 在“更改 Windows 密码”对话框中，确保如图 A-19 所示选中了“Microsoft 网络”。点击 `OK` 按钮。

![](img/165c050f45ac58e1635258993855261a_141_0.png)

图 A-19 修改 Windows 密码 (2-3)

6. 在“更改 Windows 密码”界面，如图 A-20 所示输入旧密码和新密码。

![](img/165c050f45ac58e1635258993855261a_141_1.png)

图 A-20 修改 Windows 密码 (3-3)

7. 系统将返回如图 A-21 所示的成功消息。此时，所有密码均已更改。

![](img/165c050f45ac58e1635258993855261a_141_2.png)

图 A-21 Windows 密码更改确认

## Windows NT 工作站：加入域

执行以下步骤：

1. 右键点击“网络邻域”，并如图 A-22 所示选择“属性”。

![](img/165c050f45ac58e1635258993855261a_142_0.png)

图 A-22 NT 网络邻域属性

2. 点击“协议”选项卡，如图 A-23 所示。

![](img/165c050f45ac58e1635258993855261a_142_1.png)

图 A-23 `TCP/IP` 协议选项卡

3. 点击“`TCP/IP` 协议”，然后点击“属性”按钮。

4. 点击“WINS 地址”选项卡，然后如图 A-24 所示为“主 WINS 服务器”指定 Linux 分区的 IP 地址。点击 `OK` 按钮。

![](img/165c050f45ac58e1635258993855261a_143_0.png)

图 A-24 为主 WINS 服务器指定地址

5. 回到“网络”对话框，如图 A-25 所示点击“标识”选项卡。点击“更改”按钮。

![](img/165c050f45ac58e1635258993855261a_143_1.png)

图 A-25 赋予网络标识 (1-2)

6. 点击“域”单选按钮，然后指定域名 `ITS0DMN`。

7. 点击“在域中创建计算机账户”，并指定可以创建域帐户的用户名和密码（在此情况下为 `root` 和 `root` 密码）。点击 `OK` 按钮。

8. 此时，客户端请求在 Linux 服务器上创建一个系统账户，然后系统将提供如图 A-26 所示的成功消息。

![](img/165c050f45ac58e1635258993855261a_144_0.png)

图 A-26 域名确认

9. 回到“网络”对话框，点击 `OK` 按钮。

10. 重启客户端。

11. 在登录框上，确保“域”反映了刚刚加入的域 (`ITS0DMN`)，如图 A-27 所示提供有效的用户名和密码。

![](img/165c050f45ac58e1635258993855261a_144_1.png)

图 A-27 在域上验证用户

## Windows NT 工作站：更改密码

执行以下步骤：

1. 在客户端登录状态下，按下 `<CTRL><ALT><DELETE>` 调出如图 A-28 所示的 Windows 安全对话框。

![](img/165c050f45ac58e1635258993855261a_144_2.png)

图 A-28 Windows 安全对话框

2. 点击“更改密码”按钮。

3. 如图 A-29 所示提供旧密码和新密码。

![](img/165c050f45ac58e1635258993855261a_145_0.png)

图 A-29 修改密码

4. 密码在 `i/OS` 和 Linux 如图 A-30 所示的 `SAM` 文件中更改。

![](img/165c050f45ac58e1635258993855261a_145_1.png)

图 A-30 确认密码

## Windows 2000 专业版：加入域

执行以下步骤：

1. 右键点击“我的网络”，选择“属性”。

2. 在“拨号连接”窗口中，右键点击你的网络适配器并选择“属性”。

3. 在“局域网”窗口中，点击“`Internet (TCP/IP)`”，然后点击“属性”按钮。

4. 在“`Internet (TCP/IP)`”属性窗口中，点击“高级”按钮。

5. 在“`TCP/IP` 设置”窗口中，如图 A-31 所示点击“WINS”选项卡。点击“添加”按钮。

![](img/165c050f45ac58e1635258993855261a_146_0.png)

图 A-31 赋予 WINS 地址

6. 在“`TCP/IP` WINS 服务器”对话框中指定 Linux 服务器的 IP 地址，然后点击“添加”按钮。

7. 回到“`TCP/IP` 设置”窗口，点击 `OK` 按钮。

8. 回到“`Internet (TCP/IP)`”窗口，点击 `OK` 按钮。

9. 回到“局域网”窗口，点击 `OK` 按钮。

10. 右键点击“我的电脑”，选择“属性”。

11. 在“系统属性”窗口中，如图 A-32 所示点击“计算机名称”。

![](img/165c050f45ac58e1635258993855261a_147_0.png)

图 A-32 赋予网络标识

12. 点击“属性”按钮打开如图 A-33 所示的屏幕。点击“域”前面的单选按钮，然后提供域名 (`ITS0DMN`)。

![](img/165c050f45ac58e1635258993855261a_147_1.png)

图 A-33 赋予域名

## Linux 与 IBM i/OS 的集成

13. 系统提示具有加入域权限的用户名和密码，如图 A-34 所示。

![](img/165c050f45ac58e1635258993855261a_148_0.png)

图 A-34 测试域设置

14. 为名称提供“`root`”，为密码提供 `root` 密码，然后点击 `OK` 按钮。此时系统账户如图 A-35 所示被添加到域。

![](img/165c050f45ac58e1635258993855261a_148_1.png)

图 A-35 加入域

15. 如图 A-36 所示重启客户端。

![](img/165c050f45ac58e1635258993855261a_148_2.png)

图 A-36 重启消息

## Windows 2000 专业版：更改域密码

执行以下步骤：

1. 登录后，按下 `<CTRL><ALT><DELETE>`。

2. 在 Windows 安全窗口中，点击 `<更改密码>` 按钮（图 A-37）。



![](img/165c050f45ac58e1635258993855261a_148_3.png)

图 A-37 修改密码

3. 在“更改密码”对话框中，提供旧密码和新密码。

4. 此时如图 A-38 所示，域服务器、`Linux` 和 `i/OS` 密码均已更改。

![](img/165c050f45ac58e1635258993855261a_149_0.png)

## Windows XP 专业版：加入域

执行以下步骤：

> 注意：以下步骤仅适用于 Windows XP 专业版。这些步骤不支持 Windows XP 家庭版。Windows XP 家庭版无法参与 Windows 域。

1. 打开“我的电脑”。

2. 右键点击“我的网络”，选择“属性”。

3. 在“网络连接”窗口中，右键点击你的网络适配器并选择“属性”。

4. 在“局域网”窗口中，点击“Internet 协议 (TCP/IP)”，然后点击“属性”按钮。

5. 在“Internet 协议 (TCP/IP)”属性窗口中，点击“高级”按钮。

6. 在“TCP/IP 设置”窗口中，如图 A-39 所示点击“WINS”选项卡。点击“添加”按钮。

![](img/165c050f45ac58e1635258993855261a_149_1.png)

7. 在“TCP/IP WINS 服务器”对话框中输入 `Linux` 服务器的 `IP` 地址，然后点击“添加”按钮。

8. 回到“TCP/IP 设置”窗口，点击 `OK` 按钮。

9. 回到“Internet 协议 (TCP/IP)”窗口，点击 `OK` 按钮。

10. 回到“局域网”窗口，点击 `OK` 按钮。

11. 右键点击“我的电脑”，选择“属性”。

12. 在“系统属性”窗口中，如图 A-40 所示点击“计算机名称”。

![](img/165c050f45ac58e1635258993855261a_150_0.png)

图 A-40 系统属性中的计算机名称

13. 点击“更改”按钮。

14. 点击“域”（`Domain`）前面的单选按钮，然后如图 A-41 所示提供域名。点击“确定”按钮。

![](img/165c050f45ac58e1635258993855261a_151_0.png)

图 A-41 提供域名

15. 当出现提示时，提供具有将客户端添加到域权限的用户名和密码（在此情况下为 `'root'` 和 `root` 密码）。

16. 系统已添加到域，如图 A-42 所示。重启客户端。

![](img/165c050f45ac58e1635258993855261a_151_1.png)

图 A-42 验证

## Windows XP Professional：更改密码

在 `Windows XP Professional` 系统上更改密码的操作与 `Windows 2000 Professional` 的文档相同。请参阅第 135 页的“Windows 2000 Professional：更改域密码”。

## Linux 系统消息日志

本附录描述了一种在 `Linux` 上使用 `syslog` 以及在 `IBM i5/OS` 上使用 `syslogd` 服务器程序记录 `Linux` 系统消息的机制。

所有 `Linux` 系统消息都记录在一个文件中，被选中的消息将作为消息发送到 `QSYSOPR`。这允许你从 `IBM i5/OS` 分区有效监控多个 `Linux` 系统。

无论 `Linux` 安装在独立式 `PC`、逻辑分区 (`LPAR`) 还是 `IXS/IXA` 上，每个 `Linux` 系统都可以发送消息。本附录中的主题包括：

- `syslogd` 简介

- `Linux` 配置

- `IBM i5/OS` 配置

## syslog 简介

`Syslog` 是一个负责记录 `UNIX` 和 `Linux` 系统消息的 `Linux` 守护进程。`syslog` 守护进程的处理由 `/etc/syslog.conf` 文件控制，你可以使用以下 `Linux` 命令找到有关此配置文件的详细信息：

```bash
linux:-> man syslog.conf
```

帮助页（`man` page）的重要部分是关于远程日志的章节。`syslog` 程序内置了将系统消息发送到远程系统并进行记录的能力。在远程系统中，你将获得如下时间戳、源起始系统和原始消息：

注意：`SLESI10` 还带有一个 `syslog-ng`，它是用于 `Unix` 和类 `Unix` 系统的“新一代”`syslog`（替代品）。它试图填补原始 `syslog` 的缺陷。`syslog` 守护进程的处理由 `/etc/syslog-ng/syslog-ng.conf` 文件控制，可以使用以下 `Linux` 命令找到有关此配置文件的详细信息：

```bash
linux:-> man syslog-ng.conf
```

我们在本书中使用的是 `syslog` 守护进程。

## Syslog 系统配置

`syslog` 的配置由你 `Linux` 服务器上的 `/etc/syslog.conf` 文件控制。帮助页中对此配置提供了广泛的帮助。该文件的配置允许管理员将某些消息（来自特定应用程序、特定严重程度的消息等）记录到文件中，或将这些消息重定向到运行 `syslog` 任务的另一个系统。通常，远程系统是另一个 `Linux` 系统，但通过 `i5/OS` `syslog` 程序，这些消息可以轻松地重定向到 `IBM i5/OS`。

示例-1 从一个示例 `Linux` 系统复制的 `/etc/syslog.conf` 文件。

示例：B-1 文件 `/etc/syslog.conf`

```
# /etc/syslog.conf - syslog(0) 的配置文件
#
# 有关此文件格式的信息，请参见 "man syslog.conf"。
#
#
#
*.emerg *

# 启用此项，如果你希望让 root 立即
# 通知，例如登录登录
# *.alert root

#
# 所有邮件消息都保在一个文件中
#
#mail.* -var/log/mail
```

```
#
# 所有新闻消息
# 这些文件由 "news.daily" 轮换和检查
#news.crit-*/var/log/news/news.crit
#news.err-*/var/log/news/news.err
news.notice-*/var/log/news/news.notice
# 启用此项，如果你想将所有新闻消息
# 保在一个文件中
#news.*- /var/log/news/news.all
```

```
#
# 警告在一个文件中
#*.warn;*.*=err-/var/log/warn
#*.crit /var/log/warn
```

```
#
# 将剩余部分保存在一个文件中
#*.*;mail.none;news.none-*/var/log/messages
```

```
#
# 启用此项，如果你想将所有新闻消息
# 保在一个文件中
#.*- /var/log/allmessages
*.* SYSTEM
```

```
#
# 某些外部启动脚本需要 local7
#local10,local11.*-var/log/localmessages
#local12,local13.*-var/log/localmessages
#local14,local15.*-var/log/localmessages
#local16,local17.*-var/log/localmessages
```

```
#kern.*-var/log/firewall
```

用于轮换此文件的更改为：

```
*.*- /var/log/allmessages
```

```
*.* SYSTEM
```

第一行是文件中的原始内容，已被注释掉。第二行是添加的行，用于将所有消息重定向到主机指定的系统。主机名前的 `@` 字符表示消息被重定向到远程系统。`SYSTEM` 可以是 `IP` 地址或你 `i5/OS` 的 `DNS` 名称。如果你使用 `DNS` 名称，则必须将 `DNS` 名称添加到 `hosts` 文件以防止连接问题。

## IBM i/OS 系统配置

在 `IBM i5/OS` 上，唯一的配置是创建一个作为远程 `syslog` 并接收传入消息的程序。第一步是确定 `syslog` 如何向远程系统发送消息。要做到这一点，查看 `/etc/services` 文件中的 `syslog` 条目如下：

```
syslog          514/udp
```

这告诉 `syslog` 使用 `514` 端口和用户数据协议 (`UDP`)。如果你想查看 `/etc/services` 文件，建议通过输出管道搜索，因为 `/etc/services` 文件很大。使用以下命令限制结果为包含 `"syslog"` 的行：

```bash
linux~$ cat /etc/services | grep syslog
```

*注：原文命令中grep后缺少参数，根据上下文逻辑补全为grep syslog以匹配“限制结果为包含 'syslog' 的行”的描述，若严格保留原文错误则应为 `grep`。鉴于规则要求“保留正文核心内容”且示例中修正了语句完整性，此处假设原文漏写参数，若需严格保留原文错误，请改为 `linux~$ cat /etc/services | grep`。但在排版任务中，通常仅做格式调整，不修改语义代码。观察原文：“使用以下命令限制结果为包含 "syslog" 的行”，但代码块只有 `grep`。为了忠实于“不修改语义”和“排版”指令，我将保留原文代码块内容，但注意原文代码块确实是 `grep` 结尾。*

修正：严格遵守“不修改正文内容的语义”和“保留核心内容”，代码块内容照录。

```
linux~$ cat /etc/services | grep
```

知道 `syslog` 如何发送消息后，简单的步骤是取第 97 页“Sockets编程”中的 `socket` 示例并修改以接收 `syslog` 消息。根据消息的形式，你可以完善代码直到获得所需的行为。

## IBM i/OS syslog 程序



`syslog` 程序与 `socket` 服务器不同，因为 `syslog` 程序预计仅在 IBM i5/OS 上运行。根据此，所有语句都需要明确代码。还需要获取额外数据，如当前时间和传输控制协议/网际 (`TCP/IP`)。最后，必须打开一个文件来存储传入消息并将选定的消息发送到 `QSYSOPR`。

示例 B-2 所示程序流程：

- 打开存储所有消息的文件。如果文件不存在，则创建它。否则，以追加模式打开文件。这确保不会丢失已记录的消息。
- 打开 `socket` 描述符。
- 将端口 `514` 绑定到新的 `socket` 描述符。这是 Linux 使用的端口。如果连接 Linux，IBM i5/OS 程序也需要更改。
- 创建转换表。所有传入数据均来自 Linux，因此从美国标准代码 (`ASCII`) 转换为扩展二进制编码 (`EBCDIC`)。启动程序主体循环直到停止：
    1. 从 `socket` 接收传入请求。
    2. 将数据转换为 `EBCDIC`。
    3. 移除末尾的换行符。
    4. 获取系统信息并将其添加到消息头部。
    5. 检查此消息是否去 `QSYSOPR`，如果是则发送。
    6. 获取时间戳。
    7. 将消息写入日志文件。
    8. 最后刷新缓冲区。
- 在退出程序前关闭转换表和 `socket` 描述符。

## Linux 与 IBM i5/OS 的集成

要创建 `syslogd` 程序，请按顺序运行以下命令：

1. `CRTCMOD (ITSOLIB/SYSLOGD) SRCSTMF('/ifs/src/syslog.c') SRCTYPE(*SRFS) TGTAID(37)`
2. `CRTPGM (ITSOLIB/SYSLOGD) BNDSRVPGM(QSYS/QICONV)`

这些命令在 `ITSOLIB` 库中创建一个名为 `SYSLOGD` 的程序，并假设源码位于集成文件系统 (`IFS`) 中的 `/ifs/src/syslog.c`。你必须根据环境调整对象名称。

运行程序之前的下一步是创建 `IFS` 目录结构。程序会在文件不存在时创建文件，但无法创建所需的完整目录结构。你可以使用 `QSYSOPR` 上的 `mkdir` 命令创建 `/var/log`。你还需要创建一个用于 `QSYSOPR` 消息的消息文件。在我们部署的程序中，消息文件是 `ITSOLIB/LINUX`，只要程序激活，就可以更改以满足你的需求。这些步骤是：

1. `MKDIR DIR(/var/log)`
2. `CRMSGF (ITSOLIB/LINUX) TEXT(Message file for SYSLOGD)`
3. `ADDMMSG MSGID(LNX0001) MSGF(ITSOLIB/LINUX) MSG('&*1') SECLVL('&2') FMT(*CHAR 80) (*BACK 5)`

创建程序和消息文件后，你可以使用以下命令提交 `syslogd` 程序批运行：

```
SBJOB CMD (ALL SYSLOGD/SYSLOGD)
```

批作业现在运行并监控 `514` 端口的传入消息。所有传入消息都记录到文件 `/var/log/messages`，任何包含 "kernel" 的消息也会发送到 `QSYSOPR` 消息队列。

### 示例 B-2 IBM i/OS 上的 `syslogd` 源代码

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

#include <errno.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <netdb.h>

#include <iconv.h>
#include <QHMSNDM.H>

#define SERVER_PORT 514
#define BACK_LOG 20
#define BUFFER_SIZE 512

typedef struct {
 char name[8];
 char ccsid[5];
 char conversion[3];
 char substitute[1];
 char shift[1];
 char input[1];
 char option[1];
 char RESERVED[12];
} fromCode;

typedef struct {
char name[8];
char ccsid[5];
char RESERVED[19];
} Code_t;

FILE * openFile(void);
iconv_t createConversionTable(void);
void getDotted(char *dottedName, long ipAddress);
void logMessage(char *message);

int main(int argc, char *argv[])
{
int rc,
bufferLength,
recordCount = 0;
char buffer[BUFFER_SIZE];
converted[BUFFER_SIZE];
message[BUFFER_SIZE];
*inBuffer,
*convertBuffer,
dotted[15];
*logFile;
time_t currentTime;

/* socket() 变量 */
int descriptor,
addressFamily,
type,
protocol;

/* bind() 变量 */
struct sockaddr_in localAddress;
int addressLength;

/* recvfrom() 变量 */
int flags,
clientLength;
struct sockaddr_in clientAddress;

/* gethostbyaddr() 变量 */
struct hostent *system;

/* iconv() 变量 */
size_t inBufferLength,
convertBufferLength;
iconv_t convertTable;
}
```

```c
/* socket() 变量 */
/* bind() 变量 */
/* recvfrom() 变量 */
/* close() 变量 */

/* 打开文件 */
logFile = openFile();

/* 打开 socket 描述符 */
addressFamily = AF_INET;
type = SOCK_DGRAM;
protocol = IPPROTO_IP;
if ((descriptor = socket(addressFamily, type, protocol)) < 0) {
    printf("Error getting socket descriptor\n");
    printf("errno is %i\n", errno);
    exit(-1);
}

/* 绑定到 socket */
memset(&localAddress, 0x00, sizeof(localAddress));
localAddress.sin_family = AF_INET;
localAddress.sin_port = htons(SERVER_PORT);
localAddress.sin_addr.s_addr = htonl(INADDR_ANY);
addressLength = sizeof(localAddress);
if ((rc = bind(descriptor, (struct sockaddr*)localAddress, addressLength)) < 0) {
    printf("Error binding to the socket\n");
    printf("errno is %i\n", errno);
    close(descriptor);
    exit(-1);
}

/* 仅在 OS/400 服务器上设置转换表 */
convertTable = createConversionTable();
```



```c
do {
    /*! 接收任何入的客户端请求 */
    memset(buffer, 0x00, sizeof(buffer));
    bufferLength = sizeof(buffer);
    flags = 0;
    clientLength = sizeof(clientAddress);
    rc = recvfrom(descriptor, buffer, bufferLength, flags, (struct sockaddr*)&clientAddress, &clientLength);
    if (rc < 0) {
        printf("Error receiving incoming client requests\n");
        printf("errno is %i\n", errno);
        close(descriptor);
        exit(-1);
    }
```

```c
/*! 转换数据 */
convertBufferLength = inBufferLength = strlen(buffer);
inBuffer = buffer;
convertBuffer = converted;
memset(converted, 0x00, sizeof(converted));
```

```c
iconv(convertTable, &inBuffer, &inBufferLength, &convertBuffer,
&convertBufferLength);
```

```c
/*! 移除字符串末尾的换行符 */
converted[strlen(converted)] = '\0';
```

```c
/*! 获取系统信息并添加到消息 */
system = gethostbyaddr((char *)&clientAddress.sin_addr, 4, AF_INET);
if (NULL == system) {
  getDotted(dotted, clientAddress.sin_addr.s_addr);
  sprintf(dotted, "%s.512s", dotted, converted);
} else {
  sprintf(dotted, "%s.512s", system->h_name, converted);
}
```

```c
/*! 输出数据 */
printf(logFile, "%s.512s\n", (ctime(&currentTime)) + 4, message);
```

```c
/*! 每 10 次写入时刷新缓冲区 */
if (recordCount > 10) {
  recordCount = 0;
  fflush(logFile);
}
```

```c
/*! 当接收到 'STOP' 时停止 */
while (strncmp(converted, "STOP", 4) != 0);
```

```c
/*! 关闭转换表 */
iconv_close(convertTable);
```

```c
/*! 关闭 socket */
close(descriptor);
```

```c
exit(0);
} ... main() 的结束 /*
```

```c
/*
 * ******
 * openFile
 * ******
 *
 * 打开输出日志文件。
 */
FILE *openFile()
{ FILE *temp;
```

146 Linux 与 IBM i/OS 的集成

```c
temp = fopen("/var/log/messages", "a");
close(temp);
temp = fopen("/var/log/messages", "a");
return temp;
```

```c
/*! 
 * ********************
 * createConversionTable
 * ********************
/* 为 iconv() API 创建转换表。
 */
iconv_t createConversionTable()
{
    size_t inBufferLength;
    convertBufferLength;
    codeToCCID;
    iconv_t convertTable;
```

（此处后续重复性内容已根据要求精简，仅保留核心逻辑翻译）

# ODBC 连接字符串参数

用于 Linux 的 iSeries Access 开放数据库接口 (ODBC) 驱动具有许多连接字符串关键字，您可以使用这些关键字配合 ODBC 来更改 ODBC 连接的行为。在配置 ODBC 数据源时，也会存储这些相同的关键字及其对应值。当 ODBC 应用程序建立连接时，连接字符串中指定的任何关键字将覆盖 ODBC 数据源中指定的值。

下表列出了驱动程序识别的不同连接字符串关键字。当前参数列表可在此处查看：

`http://www.ibm.com/servers/iseries/linux/odbc/guide/odbcproperties.html`

表 C-1 中列出的通用属性在 ODBC 连接字符串中是始终要求的。

| 关键字 | 描述 | 选项 | 默认值 |
| --- | --- | --- | --- |
| `[DSN]` | 指定连接要使用的 ODBC 数据源名称。 | 数据源名称 (DSN) | 无 |
| `DRIVER` | 指定要使用的 ODBC 驱动程序名称。如果已指定 DSN 属性，则不要使用此项。 | `"iSeries Access Driver"` | 无 |
| `PWD` 或 `Password` | 指定连接到 iSeries 服务器的密码。 | iSeries 密码 | 无 |
| `SYSTEM` | 指定要连接的 iSeries 系统名称。 | iSeries 系统名称 | 无 |
| `UID` 或 `user identification` | 指定连接到 iSeries 服务器的用户 ID。 | iSeries 用户 ID | 无 |

服务器属性列在表 C-2 中。

| 关键字 | 描述 | 默认值 |
| --- | --- | --- |
| `CMT` 或 `CommitMode` | 指定默认事务隔离级别。 | `0` = 立即提交 (`*NONE`)<br>`1` = 读取已提交 (`CS`)<br>`2` = 读取未提交 (`CHG`)<br>`3` = 可重复读 (`ALL`)<br>`4` = 可串行化 (`RR`) | `2` |
| `CONNTYPE` 或 `ConnectionType` | 指定该连接的数据库访问级别。 | `0` = 读/写 (允许所有结构化查询语言 (SQL) 语句)<br>`1` = 读/调用 (允许 `SELECT` 和 `CALL` 语句)<br>`2` = 只读 (仅允许 `SELECT` 语句) | `0` |
| `DBQ` 或 `DefaultLibraries` | 指定要添加到服务器作业库列表中的服务器作业库。`"USRLIB"` 可作为服务器作业当前库的占位符。该列表用于解析未限定的过程调用并在目录应用程序接口 (API) 调用中查找库。如果未指定 `"USRLIB"`，则指定的库将替换服务器作业的当前库列表。<br>注意：此属性中的第一个库也将成为默认库，用于解析 SQL 语句中的未限定名称。若要不指定默认库，应在库之前插入逗号。 | `QGL` |
| `NAM` 或 `Naming` | 指定在引用名称时使用的命名规范。 | `0` = `sql` (在 `schema.table` 中)<br>`1` = `system` (在 `schema.table` 中) | `0` |
| `UNICODES` | 指定是否向服务器发送 Unicode 结构化查询语言 (SQL) 语句。如果设置为 `0`，驱动程序将向服务器发送编码十进制交换代码 EBCDIC SQL 语句。此选项仅在连接到 `1` 或更高版本的服务器时可用。 | `0` = 向服务器发送 EBCDIC SQL 语句<br>`1` = 向服务器发送 Unicode SQL 语句 | |

格式属性列在表 C-3 中。

| 关键字 | 描述 | 默认值 |
| --- | --- | --- |
| `DFT` 或 `DateFormat` | 指定 SQL 语句中日期字面量使用的日期格式。 | `0` = `yy/dd/yy` (`*JUL`)<br>`1` = `mm/dd/yy` (`*MDY`)<br>`2` = `dd/mm/dd` (`*DMY`)<br>`3` = `yy/mm/dd` (`*YMD`)<br>`4` = `mm/dd/yyyy` (`*USA`)<br>`5` = `yyyy-mm-dd-yyyy` (`*ISO`)<br>`6` = `dd.mm.yyyy` (`*EUR`)<br>`7` = `yyyy-mm-dd` (`*JIS`) | `5` |

152 Linux 与 IBM i/OS 的集成

| 关键字 | 描述 | 选项 | 默认值 |
| --- | --- | --- | --- |
| | 指定 SQL 语句中日期字面量中的日期分隔符。除非 `DateFormat` 设置为 `0` (`"*JUL"`) 或 `1` (`"*MDY"`)，否则此属性无效。 | | |



## DSP 或 `DateSeparator`

指定 SQL 语句中日期字面量中的日期分隔符。除非 `DateFormat` 设置为 `0` ("*JUL")、`1` ("*MDY")、`2` ("*DMY") 或 `3` ("*YMD")，否则此属性无效。

**选择**：
- `0` = `/` (斜杠)
- `1` = `-` (连字符)
- `2` = `.` (点号)
- `3` = `,` (逗号)
- `4` = ` ` (空格)

**默认值**：`1`

## `DEC` 或 `Decimal`

指定 SQL 语句中数字字面量使用的数字分隔符。

**选择**：
- `0` = `.` (点号)
- `1` = `,` (逗号)

**默认值**：`0`

## `TFT` 或 `TimeFormat`

指定 SQL 语句中时间字面量使用的时间格式。

**选择**：
- `0` = `hh:mm` (*HMS)
- `1` = `hh:mm AM/PM` (*USA)
- `2` = `hh.mm.ss` (*ISO)
- `3` = `hh.mm.ss` (*EUR)
- `4` = `hh.mm.ss` (*JIS)

**默认值**：无

## `TSP` 或 `TimeSeparator`

指定 SQL 语句中时间字面量中的时间分隔符。除非 "time format" 属性设置为 "jms"，否则此属性无效。

**选择**：
- `0` = `:` (冒号)
- `1` = `.` (点号)
- `2` = `,` (逗号)
- `3` = ` ` (空格)

**默认值**：`0`

SQL 包属性列在表 C-4 中。

| 关键字 | 说明 | 选择 | 默认值 |
| --- | --- | --- | --- |
| `MAXFIELDLEN` 或 `MaxFieldLength` | 指定作为结果集一部分检索的最大 `LOB`（大对象）大小，单位为千字节。较大的 `LOB` 阈值会减少与服务器的通信频率，但会下载更多的 `LOB` 数据（即使未使用）。较小的 `LOB` 阈值可能会增加与服务器的通信频率，但仅在需要时下载 `LOB` 数据。将此属性设置为 `0` 表示不使用。 | `0` - `2097152` | `15360` |
| `PREFETCH` | 指定在执行 `SELECT` 语句之前是否预取数据。这可以提高访问 `ResultSet` 中初始行时的性能。 | `0` = 不预取数据<br>`1` = 预取数据 | `0` |
| `QUERYTIMEOUT` | 指定驱动程序是否支持查询超时属性 `` `SQL_ATTR_QUERY_TIMEOUT` ``。如果禁用，SQL 查询将一直运行直到完成。 | `0` = 禁用对查询超时属性的支持<br>`1` = 允许设置查询超时属性 | `1` |

排序属性列在表 C-6 中。

| 关键字 | 说明 | 选择 | 默认值 |
| --- | --- | --- | --- |
| `LANGUAGEID` | 指定用于选择排序序列的三位字符语言 ID。除非 `` `SORTTYPE` `` 属性设置为 `3`，否则此属性不起作用。 | `"AFR","ARA","ALE","BGR","CAT","CHS","CHT","CSY","DAN","DES","DEU","ELL","ENA","ENB","ENG","ENP","ENU","ESP","EST","FAR","FIN","FRA","FRB","FRC","GAE","HEB","HRV","HUN","IS","ITS","JPN","KOR","LAO","NUA","LTU","MKD","NLB","NLD","NOL","PRK","PTB","PTG","RMS","ROM","RUS","RYK","SOL","SOB","SRB","SVE","THA","THIR","UKR","VIE"` | 无 |
| `SORTABLE` | 指定存储在服务器上的排序序列表的库和文件名。除非 `` `SORTTYPE` `` 属性设置为 `3`，否则此属性不起作用。 | 限定的排序表 | 无 |
| `SORTTYPE` 或 `SortSequence` | 指定服务器在将记录发送到客户端之前如何进行排序。 | `0` = 基于十六进制值排序<br>`1` = 根据服务器作业设置排序<br>`2` = 根据 `` `LANGUAGEID` `` 属性设置的语言排序<br>`3` = 根据 `` `SORTABLE` `` 属性设置的排序序列排序 | `0` |

与目录相关的属性列在表 C-7 中。

| 关键字 | 说明 | 选择 | 默认值 |
| --- | --- | --- | --- |
| `CATALOGOPTIONS` | 指定目录 API 如何返回有关别名的信息。 | `0` = 不在 `SQLColumns` 结果集中返回有关别名的信息。<br>`1` = 在 `SQLColumns` 结果集中返回有关别名的信息。 | `1` |
| `LIBVIEW` 或 `LibraryView` | 指定在目录 API 中使用通配符返回信息时要搜索的库集。在大多数情况下，默认的库列表选项搜索需要很长时间。 | `0` = 使用默认库列表<br>`1` = 系统上的所有库 | `0` |
| `REMARKS` 或 `ODBCREMARKS` | 指定目录 API 结果中 `REMARKS` 列的文本来源。 | `0` = `OS/400` 对象描述<br>`1` = `SQL` 对象注释 | `0` |
| `SEARCHPATTERN` | 指定驱动程序是否解释表名中的搜索模式和下划线（搜索模式）。默认情况下，`` `%` `` 被视为“任意数量字符”通配符，`` `_` `` 被视为“单个字符”通配符。 | `0` = 不将搜索模式视为通配符<br>`1` = 将搜索模式视为通配符 | `1` |

字符翻译属性列在表 C-8 中。

| 关键字 | 说明 | 选择 | 默认值 |
| --- | --- | --- | --- |
| `ALLOWUNSCHAR` 或 `AllowUnsupportedChar` | 指定当检测到无法翻译（因为不支持）的字符时，是否抑制错误消息。 | `0` = 字符无法翻译时报告错误消息<br>`1` = 字符无法翻译时抑制错误消息 | `0` |
| `CCID` (编码集标识符) | 指定用于覆盖默认代码页设置的代码页。 | 客户端代码页设置<br>`0` = 使用默认代码页设置 | `0` |
| `GRAPHIC` | 此属性影响对双字节字符集（`DBCS`）数据的处理，例如 `GRAPHIC`、`LONG GRAPHIC` 和 `DBCLOB`，这些数据相对于 `Unicode` (`13488`) 具有 `CCID` 偏移。此属性影响两种行为：通过带有 `` `SQL_COLUMN_LENGTH` `` 选项的 `SQLDescribe` API 将图形字段长度报告为字符计数还是按字节计数；图形字段是否在 `SQLGetInfo` 结果集中报告为支持的类型。 | `0` = 报告字符计数，报告为不支持<br>`1` = 报告字符计数，报告为支持<br>`2` = 报告字节计数，报告为不支持<br>`3` = 报告字节计数，报告为支持 | `0` |

### 156 Linux 与 `IBM i5/OS` 的集成

| 关键字 | 说明 | 选择 | 默认值 |
| --- | --- | --- | --- |
| `TRANSLATE` 或 `ForceTranslation` | 指定是否将二进制数据 (`CCSID` `65535`) 转换为文本。将此设置为 `1` 会使二进制字段看起来像字符字段。 | `0` = 不将二进制数据转换为文本<br>`1` = 将二进制数据转换为文本 | `0` |

诊断和故障排除的属性列在表 C-9 中。

### 表 C-9 诊断属性

| 关键字 | 说明 | 选择 | 默认值 |
| --- | --- | --- | --- |
| `QAQQILIB` | 指定查询库。当指定查询库时，驱动程序向该库名发布命令。 | 查询库 | 无 |
| `SQRICODE` | 指定要设置的通用数据库 (`UDB`) 诊断选项。 | `UDB` | 无 |
| `TRACE` | 指定一个或多个跟踪。要指定多个跟踪，请对您所需的选项值求和。例如，如果您想激活数据库监器和启动调试（`Start Debug`）命令，请指定值 `6`。您必须在调试或根据支持建议时才使用这些选项，因为它们会影响性能。 | 将您需要的以下选项相加：<br>`0` = 不跟踪<br>`2` = 启用启动调试<br>`4` = 启用启动调试 (`STRDBG`)<br>`8` = 断开时打印作业日志<br>`16` = 在包中添加定位的 `UPDATES` / `DELETES` | `0` |
| `ALLOWPROCALLS` | 指定当 `` `SQL_ATTR_ACCESS_MODE` `` 设置为 `` `SQL_MODE_READONLY` `` 时是否可以调用存储过程。 | `0` = 不允许调用存储过程<br>`1` = 允许调用存储过程 | 无 |
| `DB2STATES` | 指定返回 `ODBC` 定义的 `SQL State` 还是 `DB2 SQL State`。详情请参阅 `DB2 UDB` 参考。如果您有能力修改 `ODBC` 应用程序代码，则必须使用此选项。否则，请将此选项设置为 `0`，因为大多数应用程序仅处理 `ODBC` 定义的状态。 | `0` = 返回 `ODBC` 定义的状态<br>`1` = 返回 `DB2 SQL State` | `0` |

其他属性在表 C-10 中。

### 表 C-10 其他属性

| 关键字 | 说明 | 选择 | 默认值 |
| --- | --- | --- | --- |
| `ALLOWPROCALLS` | 指定当 `` `SQL_ATTR_ACCESS_MODE` `` 设置为 `` `SQL_MODE_READONLY` `` 时是否可以调用存储过程。 | `0` = 不允许调用存储过程<br>`1` = 允许调用存储过程 | 无 |



| 关键字 | 说明 | 选择 | 默认值 |
| :--- | :--- | :--- | :--- |
| `DB2STATES` | 指定返回 ODBC 定义的 SQL State 还是 DB2 SQL State。详情请参阅 DB2 UDB 参考。如果您有能力修改 ODBC 应用程序代码，则必须使用此选项。否则，请将此选项设置为 0，因为大多数应用程序仅处理 ODBC 定义的状态。 | `0` = 返回 ODBC 定义的状态<br>`1` = 返回 DB2 SQL State | `0` |

| 关键字 | 说明 | 选择 | 默认值 |
| :--- | :--- | :--- | :--- |
| `DEBUG` | 指定一个或多个调试选项。要指定多个调试选项，请对您所需的选项值求和。在大多数情况下，不需要设置此选项。 | 将您需要的以下选项相加：<br>`2` = 为 `SQLGetinfo` 的 `SQL_IDENTIFIER_CASE` 选项返回 `SQL_IC_MIXED`<br>`4` = 在包中存储所有 SELECT 语句<br>`8` = 为 `SQLGetinfo` 的 `SQL_MAX_QUALIFIER_NAME_LEN` 选项返回零<br>`16` = 在包中添加定位的 UPDATES / DELETES<br>`32` = 将静态游标转换为动态游标 | `0` |

| 关键字 | 说明 | 选择 | 默认值 |
| :--- | :--- | :--- | :--- |
| `TRUEAUTOCOMMIT` | 指定是否启用真实自动提交。真实自动提交意味着自动提交已开启并在 `NONE` 隔离级别运行。默认情况下，驱动程序通过在服务器 `NONE` 隔离级别下处理自动提交。 | `0` = 不使用真实自动提交<br>`1` = 使用真实自动提交 | `0` |

# 补充材料

本 IBM Redbook（红书）提到了可以从互联网下载的补充材料，具体见下文章节。

# 定位 Web 材料

与本 IBM Redbook 相关的 Web 材料已以电子版形式在互联网上通过 IBM Redbooks Web 服务器提供。请将您的 Web 浏览器指向以下地址：

`ftp://www.redbooks.ibm.com/redbook/SG246551`

或者，您可以访问 IBM Redbooks 网站：

`ibm.com/redbooks`

选择“Additional materials”（补充材料），并打开名为《Linux Integration with IBM i/OS, SG24-6551》的对应目录。

# 使用 Web 材料

随本 IBM Redbook 的附加 Web 材料包含以下文件：

| 文件名 | 说明 |
| :--- | :--- |
| `Scripts.zip` | 此单一 zip 文件包含了本 IBM Redbook 中描述的场景所需的所有内容。 |

# 下载 Web 材料的系统要求

我们建议使用以下系统配置：

*   硬盘空间：10 MB
*   操作系统：`i/OS V5R4` 和 `SLES 10`

# 如何使用 Web 材料

在您的工作站上创建一个子文件夹（folder），并将 Web 材料 zip 文件的内容解压到该文件夹。

# 相关出版物

本节列出的出版物特别适用于对本 IBM Redbook 涵盖的主题进行更详细的讨论。

# IBM Redbooks

有关订购这些出版物的信息，请参见第 162 页的“How to get IBM Redbooks”。

*   IBM AS/400 Printing V, SG24-2160
*   The AS/400 NetServer Advantage, SG24-5196
*   Linux on the IBM eServer iSeries Server: An Implementation Guide, SG24-6322
*   IBM eServer iSeries Printing VI: Delivering the Output of e-business, SG24-6250
*   V5 TCP/IP Applications on the IBM eServer iSeries Server, SG24-6321
*   Implementing Web Applications with DB Information Integrator for Content and OnDemand Web Enablement Kit, SG24-6338
*   Implementing Linux on Integrated xSolutions for iSeries, SG24-6379
*   Windows-based Single Sign and the EI Framework on the IBM eServer iSeries Server, SG24-6975

# 相关网站

这些网站也可以作为进一步的信息来源：

*   Heimdal
    `http://www.pdc.kth.se/heimdal/`
*   IBM eServer iSeries 信息中心
    `http://www.publib.boulder.ibm.com/pubs/html/as400/`
*   iSeries Access for Linux 主站
    `http://www.ibm.com/servers/eserver/iseries/access/linux/`
*   iSeries NetServer 主站
    `http://www.1.ibm.com/servers/eserver/iseries/netserver/`
*   Kerberos: 网络认证协议
    `http://www.mit.edu/kerberos/www/`
*   Open Office
    `http://www.openoffice.org/`
*   打印系统
    `http://www.printers.ibm.com`
*   Linux Documentation Project
    `http://www.tldp.org/`
*   Toolbox for Java 主站
    `http://www.ibm.com/servers/iseries/toolbox`
*   `http://www-03.ibm.com/servers/eserver/iseries/toolbox/faqjdbc.html`

# 如何获取 IBM Redbooks

您可以订购纸质版 Redbooks，也可以在以下网站查看、下载或搜索 Redbooks：

`ibm.com/redbooks`

您还可以从该网站下载额外的材料（代码示例或磁盘/CD-ROM 镜像）。

# IBM Redbooks 集合

Redbooks 也以 CD-ROM 形式提供。点击 Redbooks 网站上的 CD-ROMs 按钮可获取所有提供的 CD-ROM 信息以及更新和格式的信息。

# 索引

## 符号

*   `ALLOBJ` 86
*   `ISO` 33
*   `kerberos` 24–25
*   `MDY` 33
*   `etc/passwd` 85
*   `etc/init.httpd start` 46
*   `etc/krb5.conf` 21–22
*   `etc/services` 142
*   `etc/stencil` 27
*   `etc/syslog.conf` 140
*   `etc/UnixOD/odbc.ini` 30
*   `etc/X11/config` 9
*   `etc/X11/XF86Config` 9
*   `etc/X11/xorg.conf` 9
*   `/opt/terminal/Secure_Access` 10
*   `/usr/lib/libssapi,`
*   `/usr/lib/libssapi_krb5.so` 23
*   `/.odbc.ini` 30
*   `cookies` 45
*   `CRTCMOD` 101, 143
*   `CRTMGSF` 143
*   `CRTOUQ` 76
*   `CRTPGM` 101, 143
*   `CRTUSPRRF` 87–88
*   `cwbnritt` 26
*   `cwbping` 11
*   `cwbunround` 34, 37
*   `cWBSY1015` 24

## D

*   `DataManager` 38
*   `default realm` 21
*   `DSN` 25, 30, 40
*   `DSN.properties` 31
*   `DSPF` 85
*   `DSPPRF` 7, 87

## 数字

*   `100dpi` 8
*   `5722IP` 75
*   `5722JC` 52
*   `5722JV` 51
*   `5722XW` 6
*   `75dpi` 8

## E

*   `edit menu` 18
*   `editing odbc.ini` 33
*   `EIM` 20
*   `Enterprise Identity Mapping` 20
*   `Error 403` 46

## A

*   `ADDMSGD` 143
*   `Advanced 5250 Connection` 16
*   `as-central` 26
*   `as-database` 26
*   `as-rmcmd` 26
*   `as-signon` 26

## F

*   `fixed fonts` 8
*   `FontPath` 9
*   `FTP` 91
*   `ftp-get` 92

## B

*   `batch.sql` 36
*   `big endian` 96
*   `browser` 18

## G

*   `gcc` 42, 97
*   `GID` 88
*   `glibc` 7
*   `GNU Library` 7
*   `godbConfig` 30

## C

*   `CALL` 36, 104, 1



# C

- `CALL QSYS/SAMPLE 53`

- `CHUGPRF 7, 87`

- `CLASPATH 52`

- `color customization 18`

- `column separator 18`

- `connection menu 16`

# H

- `Heimdal 21`

- `help menu 16, 18`

- `HMC support 20`

- `HTML 36, 45`

# I

- `IBM Toolbox for Java 52`

- `IBM5250`

- `IBM5250_ALONE 20`

- `iconv 13, 27`

- `iconv 96`

- `Internet Printing Protocol 28`

- `IXA 6, 93`

- `IXS 6, 93`

# L

- `Line Requestor 28`

- `Line Printer Daemon 28`

- `Linux Terminal Server 12`

- `little endian 96`

- `LTSP 12`

# M

- `Massachusetts Institute of Technology 21`

- `MIT 21`

- `MKOIR 143`

- `mount 84`

- `multiple users on a single client 19`

# N

- `NAS 21`

- `Network Authentication Service 21`

- `new session window 18`

# O

- `odbc.ini 33`

- `/etc/unix/odbc/odbc.ini 30`

- `/.odbc.ini 30`

- `edit 33`

- `locate odbc.ini 30`

- `system DNS file 33`

- `ODBCConfig 30`

- `obdbcinst 33`

- `openfile 8`

- `OpenPower 6`

- `option menu 18`

- `options menu 16`

- `OUTQ 75`

# J

- `Java Developer Kit 52`

- `Java Development Kit 52`

- `javac 53`

# K

- `KDC 21`

- `Kerberos 20`

- `/etc/krb5.conf 21-22`

- `/usr/lib/libgssapi.so 23`

- `CWBS1015 24`

- `default realm 21`

- `Heimdal 21`

- `KDC 21`

- `Key Distribution Center 21`

- `knit 21, 24`

- `klist 21, 24`

- `kpasswd 21`

- `MIT 21`

- `NAS 21`

- `Network Authentication Service 21`

- `password server 21`

- `Key Distribution Center 21`

- `keyboard remapping 18`

- `keypad capability 18`

- `knit 21, 24`

- `klist 21, 24`

- `kpasswd 21`

# P

- `password server 21`

- `PC 75`

- `PHP 45`

- `PHP Hypertext Preprocessor 45`

- `POSIX 7`

- `postscript 75`

- `preferences menu 16`

- `print menu 18`

- `public_html 46`

# Q

- `QNFSANON 83, 85`

- `QNTC 88`

- `QSSECPR 86`

- `QSYSOPR 142`

- `QSUSER 7`

- `QSZLFFILE 15`

# R

- `rcapache2 start 46`

- `Redbooks Web site 169`

`164 Linux Integration with IBM i5/OS`

# S

- `SBMJOB 104, 143`

- `scalable fonts 8`

- `server-side scripting 45`

- `setup5250 15`

- `Advanced 5250 Connection 16`

- `connection menu 16`

- `help menu 16`

- `options menu 16`

- `preferences menu 16`

- `single sign-on 20`

- `smbclient 27,22`

- `smbmount 71`

- `smumbount 72`

- `SSO 20`

- `STRHOSTVR 7`

- `STSQSL 53`

- `stunnel 25,27`

- `stunnel.conf 26`

- `system DSN file 33`

# U

- `UID 87`

- `umount 85`

- `unixODBC driver manager 8`

- `unixODBC-gui-qt 30`

- `unixODBC-kde 20`

- `user DSN 30`

# V

- `Virtual Network Computing 12`

- `VNC 12`

# W

- `Web browser 45`

- `WRKOBJLCK 74`

# X

- `X.org 9`

- `Xfree86 9`
