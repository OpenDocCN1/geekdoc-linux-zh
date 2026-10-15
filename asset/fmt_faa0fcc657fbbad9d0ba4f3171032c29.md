
- Intel Corporation, 2013, 10. Intel 64 and IA-32 Architectures Software Developer's Manual. Computer Hardware Manual.
- Intel Corporation, 2014, 10. Intel 64 and IA-32 Architectures Optimization Reference Manual. Order Number: 248966-030.
- Marursaz, J., Cepeda, S., Yasin, A., 2013, 05. How to Tune Applications Using a Top-Down Characterization of Microarchitectural Issues. https://software.intel.com/en-us/articles/how-to-tune-applications-using-a-top-down-characterization-of-microarchitectural-issues.
- Yasin, A., 2014, March, A top-down method for performance analysis and counters architecture. 2014 IEEE International Symposium on Performance Analysis of Systems and Software (ISSPASS), pp. 35–44.

# Intel® VTune™ Amplifier XE 7

## 章节目录

- 7.1 安装与配置 ................................................................ 120
    - 7.1.1 编译内核模块 ................................................................ 121
    - 7.1.2 系统配置 ....................................................................... 122
- 7.2 数据收集与报告 ................................................................ 124
    - 7.2.1 采集操作 ....................................................................................... 125
    - 配置. ................................................................................................... 127
    - 7.2.2 完成操作 ...................................................................................... 129
    - 7.2.3 报告操作 ....................................................................................... 129
    - 命令行界面 .................................................................................... 129
    - 图形化界面 ................................................................................................ 131

参考文献 ................................................................................................................... 135

Intel® VTune™ Amplifier XE 是一款强大的跨平台分析器，能够执行算法分析、PMU 采样和功率分析。该工具由几个组件组成，包括一组 Linux 内核驱动程序（负责执行数据收集），以及用于控制驱动和生成报告的命令行和 GUI 工具。

默认情况下，VTune 会在 `${VTINSTALL}/documentation` 中安装大量文档。这包括收集数据和分析结果的引导说明和指南。此外，文档还提供了一系列参考文档，包括事件指标及其含义的参考，以及《Intel 软件开发者手册》第二卷的副本，列出了所有指令及其编码。

安装后，VTune 的更新通过 Intel® 软件管理器进行，该管理器通常安装在 `/opt/intel/ism`。通过此 Java ，可以下载并安装随着发布的所有 Intel 软件产品的更新。通常，VTune 的发布被分为“可选更新”和“推荐更新”。可选更新发生的频率更高，并提供更早访问新功能的体验。相反，推荐更新的发生频率较低，并合并了之前所有的可选更新。因此，可选更新为对最新功能感兴趣的用户设计的，而推荐更新为只需偶尔更新的用户设计的。

# 第 7 章 Intel® VTune™ Amplifier XE

在编写本文时，可以免费获得 Linux 上非商业用途的 VTune 许可证。有关该工具以及商业和非商业许可的更多信息，请访问 VTune 网站：https://software.intel.com/en-us/vtune-amplifier-xe。

## 7.1 安装与配置

VTune 提供了用于收集系统信息和编程 PMU 的外部内核驱动程序。这些驱动程序的源码随 VTune 一起提供，可以在 `$VT_INSTALL/sepdk/` 目录下找到。这允许针对系统的内核版本构建驱动模块。

作为默认安装过程的一部分，安装脚本将自动构建驱动模块并安装一个在启动时将模块插入内核的 init 脚本。可以通过自定义安装并取消所需步骤来跳过其中一个或两个步骤。为了尽可能兼容发行版，生成的脚本设计为兼容旧的 init 系统。现代系统（如 systemd）提供了这些旧样式脚本的后兼容性，因此也可以。

开始收集之前必须加载三个模块。第一个模块 `pax` 负责在多个处理器之间复用单个 PMU。该驱动程序在 `/dev/` 中创建一个特殊的设备文件。每个需要 PMU 的 VTune 进程首先打开此设备文件并使用 `ioctl(2)` 接口为指定的进程保留和释放 PMU。这种锁定机制防止一个进程干扰另一个进程的分析。

第二个模块 `sep` 处理 PMU 事件编程。它通常被称为 `sepX_Y`，其中 X 和 Y 代表驱动的主号和次要号。`sep` 提供了自己的 PMU 事件中断处理程序，并处理编程事件和配置系统分析的所有体系特定方面。该驱动程序创建一个目录 `/dev/sepX_Y/`，其中为采样创建了特殊的 cpu 设备文件。

```
$ $1 /dev/sep3_1/
c0% m0% s1% s2% s3% s4% s5% s6% s7
```

第三个模块 `vtsspp` 负责监控进程执行。该驱动程序记录被监控进程的特定细节，例如堆栈跟踪、寄存器等。这些信息与来自 PMU 中断的信息相关联，以便将 PMU 事件归因于 ELF 文件、函数和代码行。该驱动程序在 proc 文件系统中暴露一个配置目录，例如：

### 7.1 安装与配置 121

```
$ ls -alh /proc/vtsspp
total 0
dr-xr-xr-x. 2 root vtune 0 Sep 12 23:08 ./
dr-xr-xr-x. 21 root ubuntu 0 Sep 12 23:56 ../
-rw-rw-r-- 1 root vtune 0 Sep 12 23:17 .control
-rw-rw-r-- 1 root vtune 0 Sep 12 23:17 .cpu_mask
-rw-rw-r-- 1 root vtune 0 Sep 12 23:17 .debug
-rw-rw-r-- 1 root vtune 0 Sep 12 23:17 .def_sav
-rw-rw-r-- 1 root vtune 0 Sep 12 23:17 .targets
-rw-rw-r-- 1 root vtune 0 Sep 12 23:17 .time_limit
-rw-rw-r-- 1 root vtune 0 Sep 12 23:17 .time_source
```

在 VTune 的早期版本中，存在第四个驱动程序 `apwr.ko`，它是属于 `powerdk` 的，而不是另外三个驱动程序所属的 `sepdk`。该驱动程序用于测量某些指标，但最近由于缺乏使用已被移除。如果读者依赖于此驱动程序，作者建议联系 Intel 支持。

### 7.1.1 编译内核模块
