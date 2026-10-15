
在没有虚拟 I/O 槽位的典型导出场景中，库操作员需要站在物理库旁向 I/O 站填充磁带；系统管理员触发应用程序发送命令将磁带从 I/O 站移动到存储槽。在库填充 I/O 站后，他必须等待 I/O 槽位为空。此操作旨在优化吞吐量。如果库启用了虚拟 I/O 槽位，库会自动将磁带从 I/O 站移动到存储槽。

## 在 3584 中使用 mtlib

`mtlib`程序促进了 3584 与 3492 以及 IBM Storage Tape Saver (VTS) 之间的通信。`mtlib`程序最初设计用于控制 3492 的命令行界面。它随 3492 一起提供，类似于 `tapeutil`随 SCSI 驱动程序提供。

`mtlib`程序已增强，适用于 IBM 3584 等 SCSI 库。某些客户编写了 `mtlib`脚本来处理 3492。如果使用 3492 的客户决定迁移到 IBM 3584，`mtlib`的增强将简化迁移过程。

使用 `mtlib`的现有客户脚本可能需要更改，取决于所使用的 3492 功能。例如，SCSI 库中没有类别，任何引用类别的 `mtlib`命令可能都需要更改。

有关 `mtlib`程序的完整说明和命令语法，请参阅《IBM Storage Tape Drivers Instructions and User's Guide》，GC35-0154。

## SMI-S 支持

SMI-S 代理的设计符合存储管理规范。3584 磁带库可以使用存储管理规范 (SMI-S) 在 SAN 环境中进行通信。

为了与 SAN 环境中的存储设备进行通信，管理软件使用名为存储管理规范 (SMI-S) 代理的软件。您必须在运行 SUSE Linux Server 操作系统的 Intel® 机器上安装 SMI-S 代理。

## 1.2 硬件和操作系统平台

本节提供了有关操作系统支持、SCSI 和 FC 适配器供应商，以及支持 LTO 系列的一些应用程序的信息。

### 1.2.1 硬件服务器平台

LTO 产品在以下操作系统和服务器上运行：

- IBM @iSeries™, 运行 OS/400® 的 AS/400®
- 运行 AIX 和 Linux 的 IBM System p5, RS/6000 和 SP
- IBM @xSeries® 以及其他基于 Intel 的系统（Windows NT®, 2000 和 2003）
- 运行 Solaris 的 Sun™ SPARC
- 运行 HP-UX 的惠时（HP）
- Intel Linux (Red Hat 和 SLES)
- zSeries Linux
- True6664 (仅限 IBM 3584)
- 其他使用 SCSI 附加或光纤（Fibre Channel）连接的系统

注意，并非所有型号都支持所有的平台和连接方法——有关所有 Ultrium 型号操作系统和连接支持的当前详情，请参阅以下网站。

```
http://www.ibm.com/servers/storage/tape/3580/interop.html
http://www.ibm.com/servers/storage/tape/3581/interop.html
http://www.ibm.com/servers/storage/tape/3582/interop.html
http://www.ibm.com/servers/storage/tape/3583/interop.html
http://www.ibm.com/servers/storage/tape/3584/interop.html
```

**注意：** 请始终访问网站以获取最新、最详尽且准确的信息。

### 1.2.2 ISV 存储管理软件

虽然操作系统提供了实用程序（如 `da`、`tar` 和 `cpio`）来执行磁带驱动器的基本读写操作，但在某些情况下会使用存储管理软件包。这些软件包设计用于提供管理磁带驱动器库的高级功能。它们由名为独立软件供应商（ISV）的公司提供。我们将在第 243 页的第 2 部分“LTO 库和备份软件”中讨论一些最流行的应用程序。

IBM 在网站上发布了经过 LTO Ultrium 设备认证的 ISV 存储管理应用以及支持的操作系统：

```
http://www.ibm.com/servers/storage/tape/lto_ito_isv.html
```

您还应该向 ISV 确认详细详细支持信息。

## 1.3 Windows 2000/2003 连接

在本节中，我们将介绍使用 IBM 3584 将 LTO 型号连接到 Windows 2000/2003 的示例。

### 1.3.1 Windows 2000/2003 SCSI 直接连接

表 1-7 是摘自 IBM 网站的摘要，详细列出了 Windows 2000/2003 环境下 IBM 3584 的服务器、操作系统版本、主机总线适配器（HBA）和交换支持（截至编写时准确）。我们在第 28 页的 1.2.1“硬件软件平台”中列出了每个 LTO 型号的 URL。

点击（网站上的）详细信息按钮以读取 readme 文件。

| 表 1-7 在 L32 和 D32 3584 框架中的 LTO Ultrium 1 和 Ultrium 2 驱动器特性 | 服务器 | 操作系统 | 主机适配器 |
| :--- | :--- | :--- | :--- |
| | 2003 详情 Build 3790 或更高 Windows 2000 详情 Build 2195 或更高 | HVD Adaptec 2944 Netinity® 适配 #59H3900 LVD Adaptec 29160, 29160LP, 39160 Adaptec 39320, 39320-R, 39320D Adaptec 2940U2W LSI Logic System 22910 Netinity 适配 #19K4646 Netinity 适配 #33L5000 IBM #13N2249 |

- **备注：**
  1. 可能存在某些限制。请查看上方适用于操作系统的详细信息。
  2. Windows 支持 Ultrium 2 和 3592 驱动器的控制路径故障转移（Control Path Failover）。
  3. Windows 支持 Ultrium 2 和 3592 驱动器的数据路径故障转移（Data Path Failover）。

从表中可以看出，为了将 IBM 3584 连接到 Windows 2000 Server，需要 2195 或更高版本的操作系统，而 Windows 2003 Server 则需要 3790 或更高版本。

矩阵显示有十种 SCSI 适配器可选；其中一些使用 LVD 接口，另一些卡使用 HVD 接口。您需要为库中安装的磁带驱动器选择正确的 SCSI 接口适配器。

### 1.3.2 Windows 2000/2003 光纤连接

如果您想使用光纤连接，将将使用光纤 Ultrium 2 或 Ultrium 3 驱动器。我们现在确定 IBM 3584 支持的适配器。访问以下网站并检查选择的 Ultrium 产品和操作系统（例如，带有 Ultrium 3 FCP 驱动器的 IBM 3584 和 Windows 2000）：

```
http://knowledge.storage.ibm.com/servers/storage/support/hbasearch/hba
```

**注意：** 此 URL 区分大小写。

返回的结果在第 30 页的图 12 所示。更典型的

磁带处于高容量备份状态，通常会写入大块数据（例如，备份大型数据库文件）。在这种情况下，每个适配器配备一个驱动器将获得最佳性能。

另一种可能需要链链的情况是通过 SAN 数据网关 (SDG)（该产品已退出市场）连接多驱动器磁库。SDG 总共有四个端口，建议其中一个端口用于 SCSI 介质更换器。因此，如果磁库中安装了三个以上的驱动器，则需要链链。

## 1.6 主机总线适配器 (HBA) 和设备驱动程序

本节将涵盖以下内容：

- 什么是 HBA？
- 为什么需要它们？你需要哪一种？
- HBA 需要驱动程序吗？

> **限制：** 目前，在同一 HBA 上同时连接磁盘和磁带设备存在限制。更多信息请参阅第 228 页的 5.1.3，“同一 HBA 上的磁带和磁盘”。

### 什么是 HBA

HBA 代表主机总线适配器（Host Bus Adapter）。HBA 是一种 I/O 适配器（或卡），位于主机计算机总线与 SCSI 或光纤通道之间，负责管理这两个通道之间的信息传输。为了尽地减少对主机处理器性能的影响，HBA 以异步方式或以极少处理器参与的方式执行许多低级接口功能。

### 设备驱动程序

设备驱动程序是控制设备的程序，无论是打印机、磁盘驱动器还是键盘。许多驱动程序（如键盘驱动程序）包含在操作系统中。对于其他设备，你可能需要从操作系统 CD 加载新驱动程序，或者在首次向计算机上安装设备时由制造商提供。
