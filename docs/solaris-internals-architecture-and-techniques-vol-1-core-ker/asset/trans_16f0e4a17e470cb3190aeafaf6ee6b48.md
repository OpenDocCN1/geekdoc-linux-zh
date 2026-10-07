

# 106

## 内核引导与初始化

- */platform/<arch>/kernel/unix* — 核心内核中依赖平台的组件。
- /platform/sun4u/kernel/genunix — 针对 UltraSPARC 优化的 genunix 二进制文件，但独立于系统（箱）类型。只有基于 UltraSPARC 的系统会加载此特定的二进制文件。
- /kernel/genunix — 与平台无关（通用）的核心内核代码。只有非 UltraSPARC 的系统会加载此文件。

请注意，启动时只会加载一个 genunix 二进制文件：可能是 sun4u 硬件上的 UltraSPARC 版本，或者是其他 SPARC 系统上的 /kernel/genunix 镜像。这些对象包含了所有的底层内核服务和其他需要驻留以初始化系统并支持动态加载环境的设施。

unix 和 genunix 镜像包含了内存管理例程、回调和输出设施、时钟计时器支持、内核内存分配器、模块设施、内核运行时链接器、同步原语、线程和轻量级进程代码以及设备驱动接口。

其余部分作为模块从第 104 页表 4-1 所示的目录加载。要查看系统当前运行的模块列表，请使用 modinfo(1M) 命令。

| id | Loadaddr | Size | Ref | Module Name |
| :--- | :--- | :--- | :--- | :--- |
| 4 | f5b28000 | 3b30 | 1 | specs (specs 的文件系统) |
| 6 | f5b2b3b0 | 2bc0b | 1 | TS (分时调度类) |
| 7 | f52b2e6f8 | 4a4 | 1 | DTSPTL (分时调度表) |
| 8 | f5ce0e00 | 31a8 | 1 | ufs (ufs 的文件系统) |
| 11 | f5d3c9d8 | 3b30 | 1 | root (unix) |
| 33 | f5b4c90 | d62 | 1 | dma (直接内存访问) |
| 14 | f5b4e6f0 | aeb | 59 | aft (管理服务) |
| 16 | f5f6a7e8 | 31a8 | 1 | lelf (elf 模块) |
| 44 | f5bc2d58 | 012f | 1 | sfs (sockets 的文件系统) |
| 57 | f57eb3b0 | b4b0 | 8 | doors (doors) |
| 63 | f5bd7da0 | 3586 | 201 | fdfs (文件系统) |
| 64 | c5f2f1d8 | 31a8 | 1 | dev (OPNR/NVAR) |
| 65 | f9f18100 | f0b8 | 1 | openpr (OPNR) |
| 72 | f52db8f68 | 6c6 | 90 | katat (内核统计) |
| 73 | f76c000f | d1ef | 11 | tmps (文件系统) |
| 92 | f5b2f4a0 | 1cc0 | 1 | shmfs (系统内存) |
| 92 | f5defa40 | 268 | 1 | ipc (通用代码) |
| 93 | f5b25cac0 | 1512 | 1 | Lance (以太网) |
| 106 | f61a9900 | 587a | 40 | mod |
| 107 | f5ffaaa8 | dl | 1 | le (le 驱动程序) |

示例输出是运行 Solaris 7 的部分列表。modinfo(1M) 提供内核名称和简要描述。每个内核模块都有一个唯一标识，显示在 Id 列中。还会显示模块的虚拟地址 (Loadaddr) 和大小，并在 Info 列中显示模块特定数据。内存中的内核是通过存在于这些目录中的二进制模块构建而成的。

## 4.2 内核引导与初始化

引导过程从可启动磁盘将组成 Solaris 内核的二进制对象加载到物理内存中，初始化内核结构，设置可调优参数，启动系统守护进程，并将系统带到已知且可用的状态。引导的基本步骤如下：

1. boot(1M) 命令读取并加载引导块 (bootblock) 到内存。
2. 引导块定位并加载二级引导程序 ufsboot 到内存中，并将控制权交给它。
3. ufsboot 定位核心内核模块和所需的运行时链接器到内存中，并将控制权交给已加载的内核。
4. 核心内核从根目录定位并加载强制性内核模块，并执行主启动代码。
5. 执行内核启动代码，按照 /etc/initstab文件的指定创建并初始化内核结构、资源和软件组件。

上述所示初步步骤是基于本地磁盘的。网络引导使用不同的二级引导程序：使用 inetboot 而不是 ufsboot。我们后续的讨论基于本地磁盘。

### 4.2.1 加载引导块

引导过程的初始阶段需要系统固件的支持，通常称为 PROM，以便能够访问可启动设备，并存在一些最小的 I/O 功能用于读取主引导块。

基于 SPARC 的系统实现了名为 OpenBoot PROM (OBP) 的系统固件，该固件用 Forth 语言编写。OBP 固件为硬件测试提供了电源自检 (POST) 功能，提供了非易失性 RAM (NVRAM) 设置系统参数（例如默认引导设备），构建反映系统硬件配置的设备树，并提供引导支持。基于 Intel 的系统使用基于 BIOS 的固件，提供类似的功能。我们的重点是基于 SPARC 的系统，一旦二级引导阶段完成并加载内核，大部分初始化过程都是与硬件无关的。

在完成 POST 测试的系统上，可以通过 OBP 提示符处的显式 boot(1M) 命令启动引导，或者如果 autoboot NVRAM 变量设置为 true，则在系统电源时启动自动引导。boot(1M) 命令支持多种选项，包括指定除默认外的引导设备和文件、标记进入内核调试器 (kadb)、以更详细的模式运行引导以获得更多输出。详情请参阅 boot(1M) 手册页。

在使用默认 UNIX 文件系统 (UFS) 作为根系统（即系统磁盘）的 SPARC 上，引导块位于物理磁盘扇区 1-15，如图 4.2 所示。这些块标记为 0 到 16，以区分文件系统块。磁盘上的物理扇区大小为 512 字节，而文件系统块通常是若干个物理扇区的组合（在 UFS 中，默认文件系统大小为 8 KB 时为 16 个）。

| sector-0 sector-1 | | sector-15 sector-16 |
| :--- | :--- | :--- | :--- |
| VTOC | . . . . . | |
| | ufs bootblock | | |

图 4.2 基于 UFS 的系统磁盘上的引导块

扇区 0，虚拟内容表 (VTOC)，包含磁盘分区信息：八个可能的磁盘分区每个每个起始和结束块号。扇区 16 是 UFS 存放主超级块（文件系统元数据）的地方。

Solaris 环境提供了 installboot(1M) 命令，用于向系统分区添加或恢复引导块。引导块维护在 /usr/platform/<arch>/lib/fs/bootblock 文件中。installboot(1M) 工具使用 dd(1) 将其拷贝到指定的分区。引导块的大小受到限制（不能超过 7680 字节——15 个扇区，每个 512 字节），因此它是读取 UFS 目录、定位文件并将其加载到内存所需的最小代码。

### 4.2.2 加载 usboot

二级引导文件名 usboot 硬编码在 UFS 引导代码中；完整路径为 /platform/<arch>/usboot。注意此字段中对 <arch> 的引用应替换 uname -m 的输出（例如 sun4m, x86）。在早期 Solaris 版本（直到 Solaris 2.4），usboot 位于根目录 /.

### 4.2.3 定位内核镜像和链接器

ufsboot 加载后定位内核镜像 unix 和所需的运行时链接器 krtld。ufsboot 加载的内核完整路径为 /platform/<arch>/kernel/unix（例如 UltraSPARC 系统上的 /platform/sun4u/kernel）。unix 文件是可执行和链接格式 (ELF) 二进制文件，这是二进制文件的标准格式。在 ELF 文件中，需要检查特定的头部信息。ufsboot 了解 ELF头部——如何提取依赖。

### 4.2.4 加载内核模块

控制权交给 krtld，它对额外的二进制对象有依赖。以下是对 /platform/sun4u/kernel/unix 文件执行 dump(1) 命令的部分输出，展示了 unix 的依赖列表：

```
# pwd
/platform/sun4u/kernel
# /usr/ccs/bin/dump -lv unix

unix:
**** DYNAMIC SECTION INFORMATION ****
dynamic:
[INDEX] Tag       Value
[1]    NEEDED  genunix
[2]    NEEDED  misc/platmod
[3]    NEEDED  cpu/$CPU
[4]    HASH    0x114
```

dump(1M) 标志转储 ELF 对象的动态段。列出的是 _PT_INTERP 条目，即 misc/krtld。

