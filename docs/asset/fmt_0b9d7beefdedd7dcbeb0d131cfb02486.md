
本附录包含 SAIR/GNU Linux 认证管理员（LCA）一级的官方测试目标。这些目标称为能力，可在 `www.linuxcertification.org` 上在线获取，另有关于 SAIR/GNU LCA 认证计划的附加信息。本认证要求你通过四项考试：安装、管理和网络、安全。本书并未涵盖网络和安全考试的所有要求，但大多数至少已足够涵盖你需要了解的概念。有关这些高级主题的更多详细信息，可在同系列 Course Technology 书籍《Guide to Linux Networking and Security》（ISBN 0-619-00094-5）中找到。

在下面的表格中，通常仅为每个三级标题（例如 1.1.10）提供章节和标题引用。读者应假定更细粒度的标题（例如 1.1.50.1.d）包含在最近提供的三级标题引用中。

![](img/43f64015de86d989e30eff5bb284fb96_821_0.png)

尽管本书已尽最大努力提供及时且相关的信息以确保读者能够通过所有适用的认证考试，请注意，此处提供的能力虽直接取自 SAIR/GNU 网站，但在许多情况下指的是市场上已不再可用的旧技术。熟悉类似的当前技术应能使应试者轻松通过每项考试。

![](img/43f64015de86d989e30eff5bb284fb96_821_1.png)

此处列出的能力编号并非在所有情况下都是连续的。没有能力缺失——SAIR/GNU 网站上出现的编号也不是连续的。

## Course 3X0-101—Linux Installation and Configuration

### 1.1 Theory of Operation

| Competency | Location in This Book (Chapter, Heading) |
|---|---|
| 1.1.10 History of Open Source and Free Software | Chapter 1, "A Brief History" and "Linux in the Market" |
| 1.1.10.1 Describe the historical trends in free software | |
| 1.1.10.2 Define the cost of free software | |
| 1.1.10.3 Describe the advantages and disadvantages of free software | |
| 1.1.20 The GNU General Public License (GPL) | Chapter 1, "A Brief History" and "Linux in the Market" |
| 1.1.20.1 Briefly explain the history of the GNU GPL | |
| 1.1.20.2 Define the use of copyright to enforce copyleft | |
| 1.1.30 Third-party Analysis of open source software | |
| 1.1.30.1 Describe the Microsoft Halloween memos and conclusions | |
| 1.1.40 Living with Free Software | Chapter 1, "Linux in the Market" and "The Work of a System Administrator" |
| 1.1.40.1 Describe the nature of free software development | |
| 1.1.40.2 Explain the business of selling free software | |
| 1.1.40.3 Compare and contrast free software warranty issues with those of proprietary software | |
| 1.1.50 Linux System Concepts | See below |
| 1.1.50.1 Explain the modular structure of Linux | Chapter 1, "A Brief History" |
| 1.1.50.1.a Describe the modular concepts of the Linux kernel | Chapter 13, "Exploring Kernel Components" |
| 1.1.50.1.b Explain the modular nature of the Linux networking subsystem | Chapter 12, "Configuring Linux Networking" |
| 1.1.50.1.c Describe the role of the init process in Linux | Chapter 9, "Init and its Scripts" |
| 能力 | 本书中的位置（章节、标题） |
|---|---|
| 1.1.50.1.d 描述 Linux 操作系统中的守护进程的作用 | 第 9 章，“Init 及其脚本” |
| 1.1.50.1.e 解释用户级进程与内核级进程的区别 | 第 6 章，“定义进程” |
| 1.1.50.1.f 描述 X Windows 系统的模块化组件以及它们与 Linux 整体的关系 | 第 15 章，“X Window 系统高级配置” |
| 1.1.60 主板配置问题 | 第 8 章，“查看计算机硬件”和“安装 Linux” 第 13 章，“探索内核组件” |
| 1.1.60.1 描述 IBM-PC 总线系统架构 | |
| 1.1.60.1.a 识别并描述各种系统总线 | |
| 1.1.60.1.b 解释配置外设 I/O 地址的程序 | |
| 1.1.60.1.c 解释配置外设 IRQ 的程序 | |
| 1.1.60.1.d 描述 DMA 或共享内存 | |
| 1.1.60.2 根据特定的系统使用场景识别 RAM 需求和配置问题 | |
| 1.1.60.3 根据适当的标准确定 PCBios、内核和外设设备的设置 | |
| 1.1.60.5 外设配置问题 | |
| 1.1.60.5.1 识别需要主分区或扩展分区并适当地配置它们 | |
| 1.1.60.5.2 识别需要多启动系统并适当地配置它们 | |
| 1.1.60.5.3 描述可能影响使用旧式 CD-ROM 控制器安装的问题 | |
| 1.1.60.5.4 描述查找受支持的图形适配器并适当地配置它的过程 | |
| 1.1.60.5.5 定义分辨率及其与视频内存的关系 | |
| 1.1.60.5.6 描述刷新率以及与分辨率的权衡 | |
| 1.1.60.5.7 识别显示器的特性并适当地配置图形适配器 | |
| 1.1.60.5.8 识别需要厂商维护软盘的需要并使用它们来正确配置适配器卡 | |
| 1.1.70 网络配置 | 第 8 章，“查看计算机硬件”和“安装 Linux” 第 12 章，“配置 Linux 网络” |
| 1.1.70.1 识别并配置正确的 IP 地址 | |
| 1.1.70.2 识别并配置正确的网络掩码 | |
| 1.1.70.3 识别并配置正确的网关 | |
| 1.1.70.4 识别并配置正确的域名服务（DNS）地址 | |

### 1.2 基础系统

| 能力 | 本书中的位置（章节、标题） |
|---|---|
| 1.2.10 安装介质 | 第 8 章，“安装 Linux” 第 15 章，“使用网络服务” |
| 1.2.10.1 描述使用 CD-ROM 介质的安装程序 | |
| 1.2.10.2 描述使用安装在 MS-DOS 分区上的源的安装程序 | |
| 1.2.10.3 描述使用软盘的安装程序 | |
| 1.2.10.4 描述使用通过 FTP 远程挂载的源的安装程序 | |
| 1.2.10.5 描述使用通过 NFS 远程挂载的源的安装程序 | |
| 1.2.10.6 描述使用通过 Samba 远程可访问的源的安装程序 | |
| 1.2.20 组件兼容性和配置责任 | 第 8 章，“了解计算机硬件” |
| 1.2.20.1 识别默认配置的 Linux 支持的组件 | |
| 1.2.30 描述六种 Linux 发行版及其权衡 | 第 1 章，“Linux 在市场中” |
| 1.2.40 安装 Linux | 第 8 章，全文 |
| 1.2.40.1 描述适当的硬盘分配策略 | |
| 1.2.40.2 描述所有 Linux 安装共有的步骤 | |
| 1.2.40.3 使用 `fdisk` 或类似实用程序创建分区 | |
| 1.2.40.4 配置引导加载程序，如 `LILO` | |
