
IDE 驱动器的设备名称如 `/dev/hda`、`/dev/hdb` 和 `/dev/sdb` 等。SCSI 驱动器的设备名称如 `/dev/sda`、`/dev/sdb` 等。分区用数字指定，并将 `1` 附加在驱动器名称之后。因此，第一个 IDE 驱动器的第一个分区命名为 `/dev/hda1`，第二个 SCSI 驱动器的第三个分区命名为 `/dev/sdb3`。

## 主分区、扩展分区和逻辑分区

硬盘只能有四个普通分区，称为主分区。然而，主分区中的一个可以被指定为扩展分区。扩展分区不包含文件系统；相反，它包含最多 12 个其他分区，称为逻辑分区。第一个逻辑分区始终被指定为分区 5，即使定义的分区少于四个也是如此。图 2.2 显示了典型的硬盘分区结构。

图 2.2 典型的硬盘分区结构

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_62_0.png)

## 分区类型

Linux 使用的分区是以下两种主要类型之一：

- **Linux 原生 (Linux Native)**：用于存放包含程序和数据文件的标准 Linux 文件系统。
- **Linux 交换 (Linux Swap)**：用于临时存放从物理内存交换到硬盘的内存内容。

Red Hat Linux 还支持多种分区类型，包括 MS-DOS、VFAT、HPFS 和 NTFS。标准的 Red Hat Linux 内核无法访问 HPFS 和 NTFS 文件系统；如果你需要这些支持，则必须重新编译内核。

Linux 内核支持最大为 2GB 的交换分区。最多可以定义八个交换分区。

## 挂载点

与 UNIX 一样，Linux 将块设备的分区挂载为统一系统中的子目录。存放分区内容的目录称为其挂载点。以下两个通过挂载点命名的分区尤为重要：

- *根文件系统*
- /boot 启动分区，包含 Linux 内核

根分区在系统初始化过程开始时挂载，此时内核本身已加载到内存中。内核必须知道它的身份，这通常由 Red Hat Linux 系统上的 LILO 启动加载程序传递给内核。其他分区通过被挂载为根文件系统的子目录被集成到系统中。

启动分区是一个较小的分区，用于绕过许多系统 BIOS 的 1024 柱体限制。通过将启动分区定位在前 1024 个柱体内，可以确保 Linux 内核对 BIOS 可用。

## 总结

在本章中，你学习了 Linux 对各种硬件设备的支持。以下是本章涵盖的最重要主题：

- **硬件兼容性**：Red Hat, Inc. 发布了与 Red Hat Linux 兼容并支持的硬件列表。
- **硬件配置**：硬件设备通常必须分配一个唯一的 IRQ 和基 I/O 地址。某些设备还必须分配唯一的 DMA。
- **适配器卡**：配置 PCI 适配器卡是简单的。配置其他类型的卡（特别是 ISA 即插用卡）可能会困难。

总结 39

**设备支持**：Red Hat Linux 支持多个级别中的一个。第 1 级设备完全支持。第 2 级设备部分支持。第 3 级设备兼容，但不支持。其他设备可能与 Red Hat Linux 不兼容。

**硬盘**：BIOS可以通过物理地址或逻辑块地址访问硬盘。每种方法都对 Linux 内核的位置施加限制。

**分区**：最多可以定义四个主分区。此外，一个主分区可以被指定为扩展分区，并用于存放 12 个逻辑分区。

**分区类型**：最重要的 Linux 分区类型是 Linux 原生（用于存放程序和数据文件）和 Linux 交换（用于存放完全交换到硬盘的内存内容）。

**挂载点**：Linux 通过将每个分区与挂载点关联，将分区集成到单个文件系统中。

## 关键术语

在进入下一章之前，请确保你熟悉以下术语：

- I/O 地址
- 块设备
- 总线
- 字符设备
- 直接内存访问 (DMA)
- 磁盘几何结构
- 扩展分区
- Intel 架构
- I/O 端口
- IRQ
- 逻辑块寻址
- 逻辑分区
- 挂载点

Copyright ©2000 SYBEX, Inc., Alameda, CA www.sybex.com

40 第 2 章 • 硬件基础

- 分区
- 分区类型
- 即插即用
- 主分区
- Red Hat 硬件兼容性列表
- 对称多处理
- WinModems

## 更多信息来源

如果你想获得有关本章介绍的主题更多信息，你应该咨询以下来源：

- Mark Minasi 编写的《完全 PC 升级与维护指南》，第 11 版（Syex, 2000）
- Linux HOWTOs
  - Busmouse-HOWTO, Chris Bagwell 编写
  - Ethernet-HOWTO, Paul Gortmaker 编写
  - Ftape-HOWTO, Claus-Justus Heine 编写
  - IR-HOWTO, Werner Heuser 编写
  - Modem-HOWTO, David S. Lawyer 和 Greg Hanks 编写
  - Multi-Disk-HOWTO, Stein Gjoen 编写
  - PCMCIA-HOWTO, David Hines 编写
  - Plug-and-Play-HOWTO, David S. Lawyer 编写
  - Serial-HOWTO, David S. Lawyer 和 Greg Hanks 编写
  - Sound-HOWTO, Jeff Tranter 编写
  - UPS-HOWTO, Harvey J. 编写
  - Cable-Modem-HOWTO, Stein 编写

Copyright ©2000 SYBEX, Inc., Alameda, CA

## 复习题

- 1. 配置设备时，通常必须分配哪项？
A. 总线
B. DMA
C. I/O 端口
D. IRQ

- 2. 哪种适配卡类型最容易配置？
A. EISA
B. ISA
C. 即插即用
D. PCI

- 3. 哪种寻址方法要求内核位于前 1024 个柱体内？
A. 逻辑块
B. 逻辑字节
C. 物理
D. 虚拟

- 4. 哪些设备是 Red Hat 支持的？
A. 第 1 级
B. 第 2 级
C. 第 3 级
D. 不兼容

- 5. 在 32 位架构系统上运行 Red Hat Linux 可以访问多少物理内存？
A. 2GB
B. 4GB
C. 8GB
D. 64GB

- 6. 系统最大交换内存是多少？
A. 2GB
B. 4GB
C. 16GB
D. 64GB

## 复习题答案

- 1. B、C、D。设备连接到总线，但总线不需要分配给设备。
- 2. D。PCI 卡是即插即用的，通常由 BIOS 配置。
- 3. C。逻辑块寻址 (LBA) 要求内核位于磁盘的前 8GB 内。
- 4. A 和 B。第 3 级设备与 Linux 兼容，但不被 Red Hat, Inc. 支持。
- 5. B。当 Red Hat Linux 在 32 位架构系统上运行时，它最多可以访问 4GB 内存。
- 6. A。交换分区可以大到 2GB，系统最多可以有八个交换分区。然而，当 Red Hat Linux 在 32 位架构系统上运行时，它最多可以访问 4GB 虚拟内存。

# 第 3 章
## Unix 基础

本章涵盖 RHCE 准备主题：

- 使用 Unix 命令行。
- 有效使用基础 Unix 命令。
- 理解并使用文件所有权和权限。
- 理解 Linux 文件系统结构。
- 使用并操作路径。
- 编辑文本文件。
- 打印文件。

- 管理文件系统。
- 备份和恢复文件。
- 挂载和卸载文件系统。
- 使用可移动媒体，如软盘。
- 创建文件系统。
- 对硬盘进行分区。
- 检查文件系统。

- 使用 Unix 命令设施。
- 使用流重定向和过滤器。
- 使用正则表达式指定命令选项和参数。
- 编写环境变量和控制结构的 Shell 脚本。
