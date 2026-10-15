
允许设备驱动程序为其设备注册中断服务例程（ISR）的内核控制对象。中断对象包含内核将设备 `ISR` 与特定级别的中断关联所需的所有信息，包括 `ISR` 的地址、设备中断的中断请求级别（`IRQ`）以及 `ISR` 应与之关联的内核中断调度表条目。

## IRQ

中断请求

## job object

`Windows 2000` 中可命名、安全且可共享的对象，用于控制与作业关联的进程的各项属性。作业对象的基本功能是允许将进程组作为一个单元进行管理和操作。作业对象还记录与作业相关的所有进程以及曾经与作业相关但已终止的进程的基本核算信息。

## kernel

`Ntoskrnl.exe` 中的最低层。内核是执行体的一个组件，它决定操作系统如何使用处理器，并确保它们被审慎使用。内核提供线程调度和分发、陷阱处理和异常分发、中断处理和分发以及多处理器同步。另见执行体。

## kernel mode

处理器中的特权代码执行模式，在此模式下所有内存完全可访问，且可以发出所有 `CPU` 指令。操作系统代码（如系统服务和设备驱动程序）在内核模式下运行。另见用户模式。

## kernel objects

由 `Windows 2000` 内核实现的原始对象集合。这些对象对用户模式代码不可见，仅在执行体内部创建和使用。内核对象提供基本功能（如同步），执行体对象即建立在这些功能之上。另见执行体对象。

## kernel-mode device driver

唯一可以直接控制和访问硬件设备的驱动程序类型。

## kernel-mode graphics driver

将设备无关图形（`GDI`）请求转换为设备特定请求的 `Win32` 子系统显示或打印设备驱动程序。

## LAN

局域网；在单一管理域（如实验室或办公园区）内部使用的网络，连接个人计算机和工作站

与文件服务器、打印机和其他外围设备以及互联网一起使用。低成本局域网技术已被采用，为 `Beowulf` 级系统提供廉价的中等带宽互连

## LED

发光二极管

## Linux

一种由广泛的国际社区通过开源代码框架开发的主导的类 `Unix` 跨平台操作系统

## LOBOS

`Lots of Boxes on Shelves`（货架上许多箱子）

## 本地过程调用 (LPC)

一种用于高速消息传递的进程间通信机制（不能通过 `Win32 API` 获得，而是通过仅对 `Windows 2000` 操作系统组件可用的内部机制获得）。`LPC` 通常用于服务器进程与其一个或多个客户端进程之间。可以在两个用户模式进程之间，或者在核心模式组件与用户模式进程之间建立 `LPC` 连接。

## 本地安全授权 (LSA) 服务器

一个运行映像 `\Winnt\System32\Lsass.exe` 的用户模式进程，负责本地系统安全策略（如哪些用户被允许登录机器、密码策略、授予用户和组的权限以及系统安全审计设置）、用户认证，以及向事件日志发送安全审计消息。`LSA` 服务（`LsaSr` - `\Winnt\System32\Lsassvr.dll`），是 `Lsass` 加载的一个库，实现了这些功能的大部分。

## 登录过程

一个运行 `Winlogon.exe` 的用户模式进程，负责捕获用户名和密码，将它们发送到本地安全授权服务器进行验证，并创建用户会话中的初始进程。

## LPT

行式打印机

## MAC

媒体访问控制器

## 映射文件 I/O

将驻留在磁盘上的文件视为进程虚拟内存的一部分的能力。程序可以将文件作为大数组进行访问，而无需缓冲数据或执行磁盘 I/O。程序访问内存，内存管理器使用其分页机制从磁盘文件中加载正确的页面。如果应用程序写入其虚拟地址空间，内存管理器作为正常分页的一部分将更改写回文件。

## MAU

介质连接单元

## Mbps

每秒 100 万位的数据传输速率或带宽

## Mega

前缀，意为 100 万，或者在存储的情况下为 $2^{20}$

## 内存管理器

`Windows 2000` 执行体组件，实现按需分页的虚拟内存，给每个进程一种错觉，即它拥有 4-GB 的 32 位地址空间（同时将该地址空间的一个子集映射到物理内存）。

## 消息传递

一种基于在（通常）运行在单独计算机上的进程之间通信数据并行的方法。

## 元数据

在文件系统的背景下，这是描述文件的信息，包括所有者、权限和数据位置。

## MPI

消息传递接口，一个社区衍生的逻辑标准，用于在单独的并发进程之间传输程序消息

## MPP

或大规模并行处理器

## MSDN 微软开发者网络

微软为开发者提供支持的项目。`MSDN` 提供三种 `CD-ROM` 订阅计划：`MSDN Library`（库）、`Professional`（专业版）和 `Universal`（通用版）。欲了解更多信息，请访问 `msdn.microsoft.com`。

## MTBF

平均故障间隔时间

## 互斥锁 (mutex)

一种用于将资源访问序列化的同步机制。

## Myricom

`Myrinet` 网络的供应商、分销商和开发者，用于通用集群

## 网络

通信通道、交换机和接口控制器的组合，用于在 `Beowulf` 集群节点之间传输数字消息

## NIC

网络接口控制器；通常是硬件和软件的组合，使集群计算机节点的计算机网络传输层相匹配

## NIH

国立卫生研究院

## NOW

网络工作站，以及 `UC Berkeley` 早期有影响力的通用集群项目

## Ntkrnlmp.exe

多处理器系统的执行体和内核。

## Ntkrnlup.exe

单处理器系统的执行体和内核。

## 对象

在 `Windows 2000` 执行体中，静态定义的对象类型的单个运行时实例。

## 对象管理器

`Windows 2000` 执行体组件，负责创建、删除、保护和跟踪对象。对象管理器集中管理那些本应分散在操作系统各处的资源控制操作。

## 分页

将内存内容移动到磁盘的过程，释放物理内存，以便其他进程或操作系统本身可以使用。因为大多数系统的物理内存远小于正在运行的进程所使用的总虚拟内存（每个进程 2 GB 或 3 GB），内存管理器将部分内存内容传输或分页到磁盘。

## PC

见个人计算机

## PCI

个人计算机和工作站主导的外部接口标准，用于支持 I/O 控制器，包括网卡。

## 个人计算机 或 PC

基于微处理器的大众市场计算机，商业和消费者用户都使用它，用途从游戏到电子表格和互联网浏览器无所不包；强调性能/成本以获得最大市场份额，这些节点是低成本 `Beowulf` 级集群的基础

## PLS

物理线路信令

## 即插即用 (PnP) 管理器

执行体的主要组件，确定支持特定设备所需的驱动程序并加载这些驱动程序。`PnP` 管理器在枚举期间获取每个设备的硬件资源要求。根据每个设备的资源要求，`PnP` 管理器分配适当的硬件资源，如 I/O 端口、`IRQ`、`DMA` 通道和内存位置。它还负责发送设备变更（添加或移除设备）的系统适当事件通知。

## PnP

即插即用

## POST

开机自检

## 电源管理器

执行体的主要组件，协调电源事件并向设备驱动程序生成电源管理 I/O 通知。当系统空闲时，可以将电源管理器配置为让 `CPU` 进入睡眠状态以减少功耗。单个设备的功耗变化由设备驱动程序处理，但由电源管理器协调。

## 进程

执行一组线程对象所需的虚拟地址空间和控制信息。

## PROM

可编程只读存储器

## PVFS

并行虚拟文件系统

## PVM

并行虚拟机，一个支持高级消息传递语义的函数库

## QSW

在非常大的集群中采用的高带宽网络，特别是 `Compaq` 开发的 $SC$ 系列

## Quadrics

网络硬件和软件的商业供应商。参见 `QSW`

## RAM

随机访问存储器

## RISC

精简指令集计算机

## ROM

只读存储器

## ROMIO

`MPI-IO` 接口的可移植实现（非缩写词）

## RTC

实时时钟

## RWCP

主要日本倡议，旨在开发健壮和复杂的集群软件环境

## SCSI

小型计算机系统接口

## SDRAM

同步动态随机访问存储器

## 安全账户管理器 (SAM) 服务

负责管理包含本地机器或域（如果系统是域控制器）上定义的用户名和组的数据库的一组子例程。`SAM` 在 `Lsass` 进程的上下文中运行。

## 服务器进程

作为 `Windows 2000` 服务运行的用户进程，例如事件日志和计划任务服务。许多附加服务器应用程序，如 `Microsoft SQL Server` 和 `Microsoft Exchange Server`，也包含作为 `Windows 2000` 服务运行的组件。

## SMP

对称多处理器，紧密耦合的缓存一致多处理器，具有统一内存访问

## SRAM

静态随机访问存储器

## 对称多处理

一种多处理操作系统，其中没有主处理器——操作系统以及用户线程都可以被调度到任何处理器上运行。所有处理器共享一个内存空间。

## 线程上下文

线程的易失性寄存器、堆栈和私有存储区域。由于 `Windows 2000` 运行的每种机器架构的信息不同，此结构是特定于架构的。实际上，`Win32 GetThreadContext` 函数返回的 `CONTEXT` 结构是 `Win32 API` 中唯一的机器依赖公开数据结构。

## TLA

三字母缩写词

## 用户模式

应用程序运行的非特权处理器模式。在此模式下可用的接口集有限，且对系统数据的访问受到限制。另见核心模式。

## VGA

视频图形阵列

## 虚拟地址空间

进程可以使用的一组虚拟内存地址。

## 虚拟内存管理器

实现虚拟内存，一种为每个进程提供大型私有地址空间的内存管理方案，该地址空间可以超过可用的物理内存。

## WAN

广域网，用于连接遥远的站点，甚至是在大陆规模上

## WDM 驱动程序

遵循 `Windows` 驱动程序模型（`WDM`）的设备驱动程序。`WDM` 支持 `Windows 2000` 的电源管理、即插即用以及 `Windows` 管理仪表化（`WMI`）。`WDM` 在 `Windows 2000`、`Windows 98` 和 `Windows` 千禧版中实现，因此 `WDM` 驱动程序在这些操作系统之间具有源代码兼容性，在许多情况下也具有二进制兼容性。`WDM` 驱动程序有三种类型：总线驱动程序、功能驱动程序和过滤驱动程序。

## Win32 服务

一种在系统启动时启动进程以提供与交互式用户无关的服务的机制。服务类似于 `Unix` 守护进程，通常实现客户端/服务器应用程序的服务器端。

## WMI（Windows 管理仪表化）

执行部件的一个组件，使设备驱动程序能够发布性能和配置信息，并从用户模式的 `WMI` 服务接收命令。`WMI` 信息的消费者可以位于本地机器上，也可以通过网络远程访问。

# B 附注读物列表

本附录包含一份附注读物列表，列出了对 `Beowulf` 集群的构建者和使用者感兴趣的书籍和论文。

# C 附注 URL 列表

以下是有助于构建或使用 `Beowulf` 系统的 `URL` 示例。这不是一个详尽的列表，我们鼓励读者浏览网络以寻找其他网站。一个好的起点是通用的 `Beowulf` 网站。

## C.1 通用 Beowulf 信息

- `www.beowulf.org`：最初的 `Beowulf` 网站。

- `beowulf-underground.org`：`Beowulf Underground` 提供“关于构建和使用 `Beowulf` 系统的非正式且不受限制的信息”。这是一个允许 `Beowulf` 社区发布关于 `Beowulf` 计算相关的软件、文档和公告的简短文章的网站。每篇文章都包含指向各种项目网站和下载链接。一个独立的商业和供应商区域将免费软件划分得很清楚。版主努力保持内容简洁、切题并防止滥用。这是所有 `Beowulf` 相关事务的一站式服务站点。

## C.2 节点和网络硬件

- `www.cs.virginia.edu/stream`：`STREAM` 基准测试提供节点内存系统性能的一个简单度量。该网站还包含各种平台的结果，从适合 `Beowulf` 的 `PC` 节点，到工作站，再到超级计算机。

- `www.tomshardware.com`：面向自行组装电脑的爱好者，这是一个关于节点硬件一般背景知识的好网站，并包含自行构建节点的最新说明。

## C.3 性能工具

- `www.netlib.org/benchmark/hpl`：高性能 `Linpack` 基准测试的所在地

## C.4 并行编程与软件

- `www.mpi-forum.org`：官方 `MPI` 论坛网站，包含 `MPI-1` 和 `MPI-2` 标准的 `Postscript` 和 `HTML` 版本。

- `www.mcs.anl.gov/mpi`：关于 `MPI` 信息的起点，包括使用 `MPI` 的库和工具以及关于 `MPI` 实现或使用的论文。

- `www.mcs.anl.gov/mpich`：`MPI` 的 `MPICH` 实现的所在地。从这里下载 `MPI` 的源代码、文档以及 `Unix` 和 `Windows` 版本。还请查看 bug 列表页面以获取补丁和新版本发布的公告。

- `www.mcs.anl.gov/mpi/mptest`：`MPI` 的性能测试，包括如何不正确测量通信性能的指南。

- `www.netlib.org`：一个有价值的数学软件及相关信息集合。

- `www.csm.ornl.gov/pvm`：`PVM` 主页。

- `www.mcs.anl.gov/romio`：`MPI-2` 中 I/O 章节的 `ROMIO` 实现的所在地。`ROMIO` 包含在 `MPICH` 和 `LAM` 中，但也可以单独下载。有关调整 `ROMIO` 以优化性能的信息可在此找到。

- `hdf.ncsa.uiuc.edu`：`HDF` 的所在地。这里包括 I/O 库；用于分析、可视化和转换科学数据的工具；以及软件下载、文档和支持信息。

- `www.cs.dartmouth.edu/pario`：并行 I/O 档案的所在地。这包括并行 I/O 项目列表、从事并行 I/O 的人员以及关于并行 I/O 的会议。其最著名的成就是并行 I/O 资源的大量附注书目。

## C.5 调度与管理

- `www.openpbs.org`：`OpenPBS` 网站是 `PBS` 开源版本的官方网站。由 `Veridian` 维护，它提供软件、补丁和文档的下载，并托管常见问题解答、讨论列表、可搜索的存档以及一般的 `PBS` 社区公告。

- `www.pbspro.com`：专注于 `PBS` 专业版，`PBS Pro` 网站包括软件下载、文档、评估版本、新软件的 beta 版本、新闻以及面向 `PBS` 管理员的信息。

- `www.supercluster.org`：`Supercluster` 网站包含 `Maui` 调度器和 `Sliver` 元调度器的文档。它还包括集群相关领域的研究，如模拟、元调度、数据暂存、分配管理和资源优化。

## C.6 其他

- `www.vrco.com`：`VRCO` 提供基于虚拟现实软件，包括 `Windows 2000` 的沉浸式环境。

- `www.seattlelab.com`：`Seattle Labs` 提供 `Windows 2000` 的远程访问工具，包括 `TelnetD` 和远程控制工具。

- `www.citrix.com`：`Citrix` 提供 `Windows 2000` 终端服务器的扩展，允许非 `Windows` 平台的用户通过原生 `Windows` 界面远程访问基于 `Windows` 的系统。

- `www.cs.cornell.edu/tech2000`：此网站描述了英特尔资助的康奈尔大学教育技术 2000 项目。

- `www.tc.cornell.edu`：这是康奈尔理论中心（`CTC`）的主页，一个位于康奈尔大学的高性能集群计算和跨学科计算研究中心——拥有世界上最大规模的 `Windows`/`Intel`/`Dell` 集群复合体。

- `www.tc.cornell.edu/AC3`：`CTC` 的高级集群计算联盟（`AC3`）——一个包括计算机制造商、软件供应商、学术机构、政府机构和企业客户的联盟，他们专注于行业标准 `IT` 解决方案，以最大化运行 `Windows 2000` 的基于英特尔的服务器的性能、可靠性和可用性。

- `www.ctc-manhattan.com`：这是 `CTC` 的集群计算展示中心和计算金融解决方案中心，位于曼哈顿百老汇大街 55 号。

# 参考文献

`Cray Research`. *Application Programmer's Library Reference Manual*, 2nd edition, November 1995. Publication `SR-2165`.

`Jack Dongarra`. Performance of various computers using standard linear equations software. Technical Report Number `CS-89-85`, `University of Tennessee`, `Knoxville TN`, 37996, 2001. `http://www.netlib.org/benchmark/performance.ps`.

`G. C. Fox`, `S. W. Otto`, and `A. J. G. Hey`. Matrix algorithms on a hypercube I: Matrix multiplication. *Parallel Computing*, 4:17–31, 1987.

`William Gropp`, `Steven Huss-Lederman`, `Andrew Lumsdaine`, `Ewing Lusk`, `Bill Nitzberg`, `William Schirp`, and `Marc Snir`. *MPI – The Complete Reference: Volume 2, The MPI-2 Extensions*. `MIT Press`, `Cambridge, MA`, 1998.

`William Gropp`, `Ewing Lusk`, `Nathanboss`, and `Anthony Skjellum`. A high-performance, portable implementation of the `MPI Message-Passing Interface` standard. *Parallel Computing*, 22(6):789–828, 1996.
