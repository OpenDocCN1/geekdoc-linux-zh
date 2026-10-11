
另一个需要考虑的因素是，`IBM TotalStorage` 企业存储服务器磁盘解决方案比独立系统上的专用磁盘是一种独特且强大得多的解决方案。企业存储服务器的可靠性特性包括该单元提供的高级功能，例如 `FlashCopy`。该功能允许您立即创建磁盘卷的副本。这对于最小化备份停机时间或为新应用程序创建测试数据非常有用。

![](img/6b2be6cf94c5583e73925c180246991a_121_0.png)

由于 `zSeries` 引擎性能强大得多，因此所需的引擎比 `G6` 解决方案更少。这会影响某些成本，例如软件和维护成本，这些成本基于解决方案所需的引擎数量。

![](img/6b2be6cf94c5583e73925c180246991a_122_0.png)

图 15 新闻群组服务场景对比

### 4.5.3 使用 `Samba` 提供文件/打印服务

本节描述了如何使用 `Samba` 文件打印应用程序提供文件/打印服务。`Samba` 是高质量的开源代码，集成在大多数 `Linux` 发行版中。文件/打印服务对处理器的计算资源要求并不高。但当用户上传/下载文件或将其路由到打印机时，它会考验解决方案的 `I/O` 能力。服务器花费大量时间等待用户请求文件服务。

驱动此应用程序的软件是统一的，可用于所有提供解决方案的服务器。此应用程序所需的服务级别是主峰班次，每天 12 小时，每周 5 天。

在这种情况下，备选方案有：

- 150 台 `Intel` 2 双路 1000 MHz 服务器的分布式解决方案
- 9672 台 `G6 X47`

让我们像查看应用程序时一样查看这些备选方案。图 4-16 显示了分布式解决方案的逻辑原理图。注意，服务器连接到需要硬件的物理网络。同样注意，每台服务器都运行着独立的操作系统和应用程序代码副本。这在解决方案的每台服务器上都是重复的，在这种情况下即为 150 倍。如果服务器需要额外的磁盘存储，备选方案是购买并安装一个额外的整个磁盘卷，或者购买更高容量的磁盘，将所需的软件和数据移动到其中并安装。

必须对每台服务器单独进行维护。需要某种类型的操作员自动化来监控这 150 个独立的系统，并在必要时做出响应。备份由专用的备份服务器完成。每个系统上的客户端代码与服务器通信以执行备份操作。

![](img/6b2be6cf94c5583e73925c180246991a_123_0.png)

图 4-17 显示了 `zSeries` 解决方案。注意，服务器之间的通信发生在机器内部，这允许 `Linux` 实例以内存速度进行通信，而不是具有通常延迟的物理网络速度。除了改进服务器间通信外，还避免了外部网络硬件和软件的成本。

![](img/6b2be6cf94c5583e73925c180246991a_124_0.png)

图 4-17 `zSeries` 上的 `Samba` 文件和打印

操作系统和应用程序代码的磁盘存储由所有 150 台虚拟机共享，而在分布式案例中，它们必须被复制。共享代码具有控制磁盘存储成本和易于维护的优势。由于只存在一份代码副本，只需要在单处进行维护，从而节省了系统管理软件和人员成本。在仅使用一份代码副本后，150 台服务器即可投入运行。在分布式情况下，它们会发出消息，在某些情况下必须对这些进行监控和响应。`z/VM` 中的 `PROP` 函数正是为此目的而设计的，避免了执行该任务的额外软件成本。在复杂环境中，需要额外的系统管理软件。

`z/VM` 可以帮助你分区服务器可用的磁盘空间。在分布式模型中，增加磁盘空间意味着你需要购买新磁盘。如果其他服务器上有空闲磁盘空间，无法移动到需要增加磁盘存储的服务器上。在 `S/390` 解决方案中，`z/VM` 允许将磁盘分区为微磁盘（`minisks`），你可以轻松将其分配给需要额外磁盘空间的服务器。

备份再次由备份客户端完成。在 `S/390` 情况下，它由预安装在 `z/VM` 上的 `Tivoli Systems Manager Backup` 服务器完成。`Tivoli Systems Manager` 服务器与虚拟实例上的客户端通信以执行备份操作。

第 4 章 `zSeries` 和 `Linux` 101

另一个需要考虑的因素是，企业存储服务器磁盘解决方案是独特的，且性能远比独立系统上的专用磁盘强大。企业存储服务器的可靠性特性包括单元中的此类高级功能，如 `FlashCopy`，你可以瞬间创建磁盘卷的副本。这对于最小化备份停机时间或为新应用程序创建测试数据有用。

### 成本比较：三年总拥有成本 (`TCO`)

在成本比较中，停机成本的影响很大。通过减少这些潜在成本可以节省大量的费用。人员也是一个可以减少的成本成本因素。

![](img/6b2be6cf94c5583e73925c180246991a_125_0.png)

## 4.5.4 用于 `zSeries` 的 `IBM Linux` 软件

第 108 页的表 4-2 至表 4-7 列出了可以在 `zSeries Linux` 上运行的 `IBM` 中间件。预计未来会有更多解决方案。

### 表 4-2 `zSeries` 和 `DB2` 软件矩阵

| 产品名称 | 版本/发布 | 硬件 | 内核/发行版 |
| :--- | :--- | :--- | :--- |
| `DB2 Intelligent Miner Visualization` | 8.1 | `zSeries` | 查看 `DB2 for Linux` 网站获取支持的平台和 |
| `DB2 Net Search Extender` | 8.1 | `zSeries` | 查看 `DB2 for Linux` 网站获取支持的平台 |
| `DB2 NetData` | 8.1 | `zSeries` | 查看 `DB2 for Linux` 网站获取支持的平台 |
| `DB2 Personal's Edition` | 8.1 | `zSeries` | 查看 `DB2 for Linux` 网站获取支持的平台 |
| `DB2 Runtime Client` | 8.1 | `zSeries` | 查看 `DB2 for Linux` 网站获取支持的平台 |
| `DB2 Spatial Extender` | 8.1 | `zSeries` | 查看 `DB2 for Linux` 网站获取支持的平台 |
| `DB2 Universal's Edition` | 8.1 | `zSeries` | 查看 `DB2 for Linux` 网站获取支持的平台 |
| `DB2 Universal Enterprise Edition` | 8.1 | `zSeries` | 查看 `DB2 for Linux` 网站获取支持的平台 |
| `IBM` | | | |
| `IBM Workload Modeler for Linux on zSeries` | 1.1 | `zSeries` | |
| `IBM Workload Modeler for Linux on zSeries` | 1.1 | `zSeries` | `Red Hat 7.2 for zSeries` |
| `IBM Workload Modeler for Linux on zSeries` | 1.1 | `zSeries` | `Red Hat 7.2 for zSeries` |
| `IBM CICS Transaction Gateway` | 5 | `zSeries` | |
| `IBM Developer Kit for Linux, Java 2 Technology` | 1.4 | `zSeries` | |

### 表 4-3 `IMS` 和 `Informix`

| 产品名称 | 版本/发布 | 硬件 | 内核/发行版 |
| :--- | :--- | :--- | :--- |
| `IMS` | `VSE/ESA` | 2.7 | |
| `IMS` | 运行在 `z/390` 上的 `IMS` 可供在 `Linux` 上的应用程序访问 `IMS` 数据 | | |
| `Information Management System (IMS)` | `Connect` | 1.1 1.2 | `zSeries` |
| `Informix` | `C-ISAM` | 7.24 | `zSeries (GLIBC 2.1)` |

### 表 4-4 `Tivoli`

| 产品名称 | 版本/发布 | 硬件 | 内核/发行版 |
| :--- | :--- | :--- | :--- |
| `Tivoli Access Manager for e-business` | 4.1 | `zSeries` | `SLES for S/390` 和 `IBM zSeries (2.4.7 kernel, 31 bit)` 以及 `SLES for 64 bit zSeries (2.4.17 kernel, 64 bit with a 31-bit compatible mode)` |
| `Tivoli Access Manager for e-business (以前称为 Tivoli Director/Tivoli Policy Director for Application Servers)` `Access Base Manager WebSEAL` | 3.9 | `zSeries` | `SuSE Linux 7 for s/390` 和 `IBM zSeries 2.4 Client and Server` |
