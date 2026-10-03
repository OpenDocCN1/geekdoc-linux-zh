
## 引言

Solaris 安装过程包括三个阶段：系统配置、系统安装，以及诸如设置打印机、用户和网络等安装后任务。本章描述了各种系统配置以及在工作站上安装 Solaris 操作系统的过程。第 15 章“安装服务器”更详细地描述了安装过程，尤其是在服务器上。

## 安装 Solaris 8 软件的要求和准备工作

安装的第一步是确定您的系统类型是否在 Solaris 8 下受支持。其次，您需要决定要安装哪种系统配置，以及是否拥有足够的磁盘空间来支持该配置。

在对系统安装 Solaris 8 之前，请使用表 3.1 检查您的系统类型是否受支持。同时，确保您拥有足够的磁盘空间用于 Solaris 以及计划安装的所有软件包。 （本章后面的“软件术语”部分将帮助您估算容纳 Solaris 操作系统所需的磁盘空间量。）

要确定您的系统类型，请使用 `uname -m` 命令。系统将以平台组和平台名称的形式响应您的系统。将系统响应与表 3.1 中的平台组列进行比较。例如，要检查支持 Solaris 8 环境的 Sun 平台，请使用命令 `uname -m`。在 Sun Ultra5 上，系统返回 sun4u 作为平台名称。

### 表 3.1

### 支持 Solaris 8 环境的 Sun 平台

| 系统 | 平台名称 | 平台组 |
|---|---|---|
| x86-based | i86pc | i86pc |
| SPARCserver 1000/1000E | SUNW, SPARCserver-1000 | sun4d |
| SPARCcenter 2000/2000E | SUNW, SPARCcenter-2000 | sun4d |
| SPARCstation 4 | SUNW, SPARCstation-4 | sun4m |
| SPARCstation 5 | SUNW, SPARCstation-5 | sun4m |
| SPARCstation 10 | SUNW, SPARCstation-10 | sun4m |
| SPARCstation 10SX | SUNW, SPARCstation-10SX | sun4m |
| SPARCstation 20 | SUNW, SPARCstation-20 | sun4m |
| SPARCstation LX | SUNW, SPARCstation-LX | sun4m |
| SPARCclassic | SUNW, SPARCclassic | sun4m |
| Ultra 1 systems | SUNW, Ultra-1 | sun4u |
| Ultra Enterprise 1 systems | SUNW, Ultra-1 | sun4u |
| Ultra 2 systems | SUNW, Ultra-2 | sun4u |
| Ultra Enterprise 2 systems | SUNW, Ultra-2 | sun4u |
| Ultra Enterprise 150 | SUNW, Ultra-1 | sun4u |
| Ultra Enterprise 250 | SUNW, Ultra-2 | sun4u |
| Ultra 450 | SUNW, Ultra-4 | sun4u |
| Ultra Enterprise 450 | SUNW, Ultra-4 | sun4u |
| Ultra Enterprise 3000, 3500,4000, 4500, 5000, 5500, 6000, 6500, 10000 | SUNW, Ultra-Enterprise | sun4u |
| Ultra 5 | SUNW, Ultra-5/10 | sun4u |
| Ultra 10 | SUNW, Ultra-5/10 | sun4u |
| Ultra 30 | SUNW, Ultra-30 | sun4u |
| Ultra 60 | SUNW, Ultra-60 | sun4u |
| Ultra 80 | SUNW, Ultra-60 | sun4u |

Sun 声明本章列出的并非所有平台和外围设备都兼容。请联系您授权的 Sun 支持提供商获取支持信息。

### 表 3.1 继续

### 支持 Solaris 8 环境的 Sun 平台

| 系统 | 平台名称 | 平台组 |
|---|---|---|
| Sun Blade 100, 1000 | SUNW, Blade-100 | sun4u |
| Sun Blade 1000 | SUNW, Blade-1000 | sun4u |
| Sun Fire 280R, 880, 6800, 4810, 4800, 3800 | SUNW, Sun-Fire | sun4u |

### 不受支持的 Sun4c 架构

以下 sun4c 架构系统不再受支持：

- SPARCstation SLC
- SPARCstation ELC
- SPARCstation IPC
- SPARCstation IPX
- SPARCstation 1
- SPARCstation 1+
- SPARCstation 2
- SPARCstation Voyager
- SPARC Xterminal 1

使用 format 命令检查分区 2，以确定您的磁盘驱动器是否足够大以加载 Solaris。请参阅第 6 章“文件系统简介”，了解此命令的正确用法。如第 6 章所述，分区 2 代表整个磁盘。

### 最低系统要求

在使用交互式安装方法安装 Solaris 8 之前，计算机必须满足以下要求：

- 系统必须至少有 64MB 的 RAM。足够的内存需求由多个因素决定，包括您计划运行的活动用户和应用程序数量。
- 媒体仅以 CD-ROM 分发，因此需要本地或网络上的 CD-ROM。
- 至少需要 2.3GB 的磁盘空间。请参阅下一节，了解您计划安装的特定 Solaris 软件的磁盘空间要求。此外，增加磁盘空间以支持您环境的交换空间需求。
- 系统必须是基于 SPARC 的系统或基于 INTEL 的系统。

## 软件术语

Solaris 操作系统在 CD-ROM 上提供，并捆绑在软件包中。软件包被分组为集群。以下各节描述了 Solaris 捆绑方案。

### 软件包

软件包是一组以定义格式收集的文件和目录。它描述了一个软件应用程序，例如手册页和行式打印机支持。Solaris 8 包含大约 80 个软件包，总计约 900MB 的磁盘空间。

Solaris 软件包是交付捆绑和非捆绑软件的标准方式。软件包由软件包管理命令管理，通常以 SUNWxxx 命名约定标识。

### 软件集群和配置集群

软件包被分组为软件集群，即软件包的逻辑集合。例如，在线手册页集群包含一个软件包。某些集群包含多个软件包，例如 JavaVM 1.0 集群，其中包含 Java JIT 编译器、JavaVM 演示程序、JavaVM 开发者包、JavaVM 手册页和 JavaVM 运行时环境。

对于 SPARC 系统，集群被分组为五个配置集群，以使软件安装过程更简单。在安装过程中，您将被要求安装五个配置集群之一。这五个配置集群是核心系统支持、终端用户支持、开发者系统支持、整个发行版以及整个发行版加 OEM 系统支持。以下列表描述了每个配置集群：

- 核心系统支持。仅软件需要 258MB 的磁盘空间。然而，Sun 建议 718MB 以支持软件、交换和支持该集群所需的磁盘开销。此配置集群包含启动和运行 Solaris 系统所需的最小软件。它包括一些网络软件和运行 OpenWindows 环境所需的驱动程序，但不包括 OpenWindows 软件。
- 终端用户系统支持。仅软件需要 767MB 的磁盘空间。然而，Sun 建议 1.6GB 以支持软件、交换和支持该集群所需的磁盘开销。此配置集群包含核心系统支持软件加上终端用户软件，其中包括 OpenWindows 和通用桌面环境软件。
- 开发者系统支持。仅软件需要 1.8GB 的磁盘空间。然而，Sun 建议 1.9GB 以支持软件、交换和支持该集群所需的磁盘开销。此配置集群包含终端用户软件加上用于开发软件的库、包含文件、手册页和编程工具。编译器和调试器需单独购买，不包含在内。
- 整个发行版。仅软件需要 1.9GB 的磁盘空间。然而，Sun 建议 2.3GB 以支持软件、交换和支持该集群所需的磁盘开销。此配置集群包含整个 Solaris 8 发行版。
- 整个发行版加 OEM 系统支持。仅软件需要 1.6GB 的磁盘空间。然而，Sun 建议 2.4GB 以支持软件、交换和支持该集群所需的磁盘开销。此配置集群包含整个 Solaris 8 发行版软件加上扩展硬件支持。

此集群仅在 Sun 系统上可用，而不在 Solaris 的 Intel 版本上可用。

> 注意
交换空间和必要的<|message|> 文件系统开销已包含在每个配置集群的磁盘空间建议中。交换空间至少需要 320MB，但可能需要更多空间。默认情况下，Solaris Web Start 为交换空间分配 512MB。

### Solaris 媒体

Solaris 8 操作系统软件在 CD-ROM 上分发，被称为“安装媒体套件”。媒体套件有两种版本：Intel 版本和 SPARC 版本。如果您拥有 Sun 系统，请安装 SPARC 版本。如果您计划在个人计算机上安装 Solaris，请使用 Intel 版本。此外，每个平台类型都有媒体套件的国内版本和国际版本。SPARC 媒体套件的国内版本有四张 CD，标签如下：

- Solaris 8 安装 English SPARC 平台版
- Solaris 8 软件 CD 1 of 2 SPARC 平台版
- Solaris 8 软件 CD 2 of 2 SPARC 平台版
- Solaris 8 文档 CD（English SPARC / Intel 平台版）

还提供国际版本的媒体套件供美国境外使用。此国际版本包含国内版本中的所有内容，并额外包含以下 CD：

- Solaris 8 文档 European SPARC / Intel 平台版
- Solaris 8 文档 Asian SPARC / Intel 平台版
