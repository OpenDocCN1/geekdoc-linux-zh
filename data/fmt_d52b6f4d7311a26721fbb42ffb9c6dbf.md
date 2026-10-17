
SUSE Linux 提供了一个图形界面来配置服务器防火墙。下节介绍了配置防火墙的可用选项。使用 `计算机` | `YaST` | `安全与用户` | 防火墙 来配置您的系统。

1. 使用启动页上的“启动时”单选按钮在服务器启动时启动防火墙。您也可以通过保存文件以后手动启动防火墙。图 2.36 显示了防火墙配置的启动界面。

操作系统加固 • 第2章

## 图 2.37 SUSE Linux 防火墙配置

![](img/b38c01d2fda8509e849e32f87ae148_87_0.png)

2. 防火墙配置的接口可以在接口页面配置。在典型的防火墙服务器中，可能会找到多个接口。图 2.38 显示了防火墙配置的选项。

## 图 2.38 防火墙接口

![](img/b38c01d2fda8509e849e32f87ae148_87_1.png)

3. 允许的服务允许为每个区域选择允许的服务。图 2.39 显示了外部区域的允许服务。您还有一个选项（图中未显示）可以启用内部区域保护。如果在列表中找不到服务，可以通过指定手动添加服务（端口）。点击“添加”提供 tcp、udp、rpc 端口和 ip 协议选项。

第2章 • 操作系统加固

## 图 2.39 允许的服务

![](img/b38c01d2fda8509e849e32f87ae148_88_0.png)

1. `伪装 (Masquerading)` 选项允许您执行地址转换（地址隐藏）。您至少需要一个外部和一个内部接口来配置伪装。

2. 除了上述选项，您还可以配置广播、IPsec 支持和 `日志` 级别。

## Novell AppArmor

AppArmor 提供了一种保护应用程序免受漏洞影响的机制。Novell 称为“免疫”。要免疫您的系统，需要安装 AppArmor（Novell SUSE Linux Enterprise Server 10 默认安装）、设置 AppArmor 配置并重启系统。本节简述了在您的 SUSE Linux 服务器上配置 AppArmor 的过程。

大多数常用应用程序和服务都有 AppArmor 默认创建的配置。当您添加新的应用程序和服务时，可以为这些应用程序单独创建配置。在创建配置之前，确保已停止应用程序。创建配置时，AppArmor 会运行自动检测以分析并为应用程序创建初始配置。非常需要您进行手动配置，以避免限制过于细致导致应用程序无法访问执行功能所需的目录。AppArmor 具有学习模式，可以在您运行程序时监控其访问情况。学习模式收集的信息包含在 AppArmor 创建的初始配置中。为关键应用程序创建配置可以确保应用程序在安全环境中运行，防止随时间推产生的漏洞对系统造成损害。

您需要配置 AppArmor 来免疫可能授予权限、打开端口、定时作业、服务器守护进程和 Web 应用程序的程序。

1. 首先，您需要如图 2.40 所示启用 AppArmor。

操作系统加固 • 第2章

## 图 2.40 启用 AppArmor

![](img/b38c01d2fda8509e849e32f87ae148_89_0.png)

2. 点击 `计算机` | `YaST` | `Novell AppArmor` 如图 2.41 所示。您有以下选项：

3. 添加配置向导、AppArmor 控制面板、AppArmor 报告、删除配置、手动添加配置和更新配置向导。

## 图 2.41 Novell AppArmor 配置

![](img/b38c01d2fda8509e849e32f87ae148_89_1.png)

第 2 章 · 加固操作系统

4. 然后点击 `Edit Profile`（编辑配置）。选择 'netstat' 条目并点击 'Edit Entry'（编辑条目）。你可以看到应用程序 netstat 在 `/etc/networks` 文件上的权限。你拥有的选项有读、写、链接、mmap、执行、继承、离散配置、无限制、未训练（纯净执行）。图 2.42 AppArmor 配置文件对话框。

## 图 2.42 AppArmor 配置文件

![](img/b38c01d2fda8509e8449e32f876ae148_90_0.png)

5. 最后，退出 `Edit Entry`（编辑条目）界面。你将看到应用程序 netstat 在服务器上运行的权限摘要。图 2.43 显示了 netstat 的配置。

## 图 2.43 用于 Netstat 的 AppArmor 配置文件

在此表中，你可以查看并修改单个配置的内容。对于现有条目，可以双击权限以访问修改对话框。

`权限定义：`

- r 读 (read)

- w 写 (write)

- m mmap_PROT_EXEC

- x 执行 (execute)

- ni 继承 (inherit)

- p 离散配置 (discrete profile)

- F : 离散配置 (discrete profile)

- *(clean exec)

- u- 无限制 (unconstrained)

- u- 无限制 (unconstrained)(clean exec)

`添加条目：`

从下拉列表中选择要添加的资源类型。

![](img/b38c01d2fda8509e8449e32f876ae148_91_0.png)

## 注意

更多信息请参阅 www.novell.com 上的 AppArmor 管理指南

## 主机入侵防御系统

主机入侵防御系统（俗称为 HIPS）通过在你的服务器周围建立一道屏障，确保系统不会发生恶意攻击或未经授权的更改。通过提供行为规则保护、基于特征的分析以及状态防火墙层级保护；HIPS 还能确保核心操作系统文件不会因未知漏洞利用而发生更改。商业级 HIPS 提供丰富的图形化报告、高级告警系统、集中化管理以及来自供应商的全天候更新和技术支持。许多安全厂商已针对 Unix/Linux 变体推出了 HIPS 解决方案。虽然讨论每个 HIPS 解决方案或其功能是本书的范围，以下是 HIPS 产品列表：Cisco、McAfee、ISS（现为 IBM ISS）和 Enterasys。还有针对 Web 服务器和数据库服务器的特定版本，帮助你防止 SQL 注入和目录遍历等攻击。这些不必也都适用于 Microsoft 平台。

Cisco Security Agent (CSA 版本 5.2) 除了 Microsoft Windows 外，还适用于以下 Linux 服务器版本。CSA 也适用于 Linux 桌面版本。

- Solaris 8 SPARC 架构（64 位内核）

- Solaris 9 SPARC 架构（64 位内核）

- Red Hat Enterprise Linux 3.0 ES 和 AS

- Red Hat Enterprise Linux 4.0 ES 和 AS

Enterasys Dragon Host Sensors 适用于以下操作系统：

- Linux

- AIX

- Solaris

- HP-UX

Enterasys Dragon Host Sensors 支持以下 Web 入侵防御：

- 适用于 Linux 的 Apache WebIPS

- 适用于 Solaris 的 WebIPS

IBM Internet Security Systems 除了 Microsoft Windows 外，还适用于以下 Unix 变体：

- Solaris 的 IBM RealSecure Server Sensor 7.0

- 适用于 HP-UX 的 IBM RealSecure Server Sensor 7.0

- 适用于 AIX 的 IBM RealSecure Server Sensor 7.0

McAfee 主机入侵防御：

可用平台包括：

- Red Hat Enterprise Linux 4.0（仅 32 位，仅服务器）支持的内核：

- 2.6.9-11.EL–2.6.9-11.EL-smp

- 2.6.9-22.EL–2.6.9-22.EL-smp

- 2.6.9-34.EL–2.6.9-34.EL-smp

- Sun Solaris（仅服务器）

- SPARC Solaris 8, sun4u（32 位或 64 位内核）

- SPARC Solaris 9, sun4u（32 位或 64 位内核）

- SPARC Solaris 10, sun4u（仅 64 位内核）

McAfee 主机入侵防御也适用于以下 Web 服务器平台：

- Apache 1.3.6 及更高版本

- Apache 2.0.42 及更高

- iPlanet 4.0 和 4.1

- Sun Java System（原 Sun ONE）6.0 和 4.1

## Linux 基准工具

互联网安全中心 (CIS) 是一家非营利组织，帮助机构降低由于安全措施不足导致的业务风险和电子商务业务中断。CIS 定期发布基准和评分工具。基准工具适用于操作系统、网络设备和应用程序。

下载基准和评分工具之前需要注册。CIS 将这些工具分为 1 级和 2 级。1 级工具适用于具有基础安全知识的管理员。这些工具在运行时不太引起任何中断，并可以通过 CIS 提供的工具进行监控。
