

## 3.1.10 OProfile

OProfile 是一个用于 Linux 系统的开源性能分析器。它提供对 Linux 系统上所有运行代码的性能分析，包括内核、共享库、应用程序二进制文件等，并根据工作负载的不同，以低开销（范围从 1% 到 8% 不等）提供多种统计信息。它遵循 GNU GPL 许可发布。OProfile 由一个内核驱动、一个用于收集采样数据的守护进程以及用于生成报告的工具组成。

OProfile 通常在 Linux 内核 2.2、2.4、2.6 及更高版本中受到支持。但是，对于 System z 上的 Linux，OProfile 仅支持内核 2.6 或更高版本。对于 SUSE Linux，内核级别必须至少为 kernel-s390(x)-2.6.5-7.191，这始于 SLES9 SP2。对于 Red Hat Linux，内核级别必须至少为 kernel-2.6.9-22.EL，即 RHEL4 U2。

OProfile 利用 CPU 的性能计数器统计所有运行代码的事件，并将信息聚合为每个二进制映像的性能分析文件。然而，System z 硬件目前不支持 OProfile 使用的这种硬件性能计数器，因此使用计时器中断作为替代。

使用 OProfile 可以分析以下代码：

- 硬件和软件中断处理程序
- 内核模块和内核
- 共享库
- 应用程序

OProfile 的设置涉及通过启用性能分析选项来配置内核源代码。要构建和安装 OProfile，请在解压后的 oprofile 目录中执行示例 3-16 中所示的命令。如本例所示，我们使用了选项 *with-kernel-support*（包含内核支持）。当您的内核版本为 2.6 或更高时，请使用此选项。有关 OProfile 安装说明的更多信息，请参见：

http://oprofile.sourceforge.net/doc/install.html

### 示例 3-16 设置 OProfile

```
./configure --with-kernel-support
make
make install
```

要使用 OProfile 工具，应使用 sysctl 命令打开计时器。在所有性能分析完成后，关闭计时器。一旦成功安装 OProfile，必须告知 OProfile 与正在运行的内核对应的 vmlinux 文件的位置。如果不需要对内核进行性能分析，则通过传递一个参数来设置 OProfile，告知系统没有 vmlinux 文件。两个示例都显示在示例 3-17 中。

### 示例 3-17 基本性能分析配置

```
opcontrol --vmlinux=/boot/vmlinux-`uname -r`
or
opcontrol --no-vmlinux
```

一旦安装并设置好 OProfile，您可以使用 opcontrol 命令启动和停止（关闭）性能分析守护进程（参见示例 3-18）。

### 示例 3-18 OProfile 启动和停止命令

```
opcontrol --start / --shutdown
```

Opcontrol 接受一个规格说明，指示如何设置每个硬件性能计数器的细节。根据这些设置，对内核或用户空间代码进行性能分析。

示例 3-19 展示了一个 OProfile 报告的示例。

### 示例 3-19 示例 OProfile 性能分析报告

```
lnx02:~# opreport --symbols
CPU: CPU with timer interrupt, speed 0 MHz (estimated)
Profiling through timer interrupt
samples % image name app name symbol name
10181 65.8288 lib_app1 lib_app1 main
3390 21.8526 vmlinux vmlinux .text
1694 10.9199 no-vmlinux no-vmlinux (no symbols)
40 0.2578 vmlinux vmlinux cpu_idle
39 0.2514 libc-2.4.so libc-2.4.so _int_malloc
23 0.1483 vmlinux vmlinux get_page_from_freelist
8 0.0516 vmlinux vmlinux do_wp_page
7 0.0451 vmlinux vmlinux _spin_unlock_irqrestore
5 0.0322 vmlinux vmlinux __handle_mm_fault
4 0.0258 libc-2.4.so libc-2.4.so malloc
4 0.0258 libc-2.4.so libc-2.4.so mbrtowc
1 0.0064 ld-2.4.so ld-2.4.so do_lookup_x
1 0.0064 libc-2.4.so libc-2.4.so _dl_addr
1 0.0064 libc-2.4.so libc-2.4.so _int_free
1 0.0064 libc-2.4.so libc-2.4.so mblen
```

在 System z 上的 Linux 中，OProfile 仅包含内核空间调用图支持。调用图选项受 Linux 内核 2.6 及更高版本支持。使用调用图选项时，可以在输出报告中看到哪些函数正在调用其他函数。OProfile 将在每次采样时记录函数堆栈。要在 OProfile 上启用调用图支持，请设置调用图采样收集速率及最大深度。使用 '0' 可禁用调用图功能。启动调用图的示例请参见示例 3-20。

### 示例 3-20 OProfile 调用图功能

```
opcontrol --start --callgraph=<depth> --vmlinux=lib/modules/<Kernel version>/build/vmlinux
```

**注意：** 目前，在 System z 上的 Linux 中，OProfile 仅包含内核空间调用图功能。

示例 3-21 展示了 OProfile 调用图报告的示例。

### 示例 3-21 OProfile 调用图示例

```
lnx02:~ # opreport --callgraph
CPU: CPU with timer interrupt, speed 0 MHz (estimated)
Profiling through timer interrupt
samples % image name app name symbol name
------------------------------------------------------------
15272 48.0720 lib_app1 lib_app1 main
15272 100.000 lib_app1 lib_app1 main [self]
------------------------------------------------------------
14281 44.9526 vmlinux vmlinux .text
14281 100.000 vmlinux vmlinux .text [self]
------------------------------------------------------------
1694 5.3322 no-vmlinux no-vmlinux (no symbols)
1694 100.000 no-vmlinux no-vmlinux (no symbols) [self]
------------------------------------------------------------
147 0.4627 vmlinux vmlinux cpu_idle
147 100.000 vmlinux vmlinux cpu_idle [self]
------------------------------------------------------------
65 0.2046 libc-2.4.so libc-2.4.so _int_malloc
65 100.000 libc-2.4.so libc-2.4.so _int_malloc [self]
------------------------------------------------------------
48 0.1511 vmlinux vmlinux get_page_from_freelist
48 100.000 vmlinux vmlinux get_page_from_freelist [self]
------------------------------------------------------------
39 0.1228 vmlinux vmlinux page_remove_rmap
39 100.000 vmlinux vmlinux page_remove_rmap [self]
------------------------------------------------------------
```

## 3.1.11 zFCP 统计

借助 zFCP 统计，我们可以将 FCP LUN 的 I/O 活动记录为统计信息。通过此功能，我们可以收集各种统计数据，例如 I/O 请求数据大小或 I/O 延迟。有关 zFCP 统计的概览，请参见图 3-2。

![](img/f332344337ca8bf6846cb313a66ee0b3_91_0.png)

图 3-2 zFCP 统计概览

对 FCP 设备的统计数据收集始于 SUSE Linux Enterprise Server 9 SP3 + 维护更新（内核版本 2.6.5-7.283 及更高版本）和 SUSE Linux Enterprise Server 10 GA（内核版本 2.6.16.21-0.8 及更高版本）。

### 收集 zFCP 统计

要收集 zFCP 统计信息：

1.  根据您的 Linux 发行版，zFCP 统计文件的查找位置如下：
    - 对于 SLES10 及更高版本，取决于 debugfs 的挂载位置，位于 `<mount_point_debugfs>/statistics`。例如，如果 debugfs 挂载在目录 `/sys/kernel/debug/`，则所有收集的统计数据都位于 `/sys/kernel/debug/statistics/`。
    - 对于 SLES9，取决于 proc 的挂载位置（SLES9 不使用 debugfs），位于 `<mount_point_proc>/statistics`。
2.  挂载设备时，会为每个设备（适配器以及 LUN）创建一个子目录。子目录命名为：
    - 对于适配器，名为 `zfcp-<device-bus-id>`
    - 对于 LUN，名为 `zfcp-<device-bus-id><WWPN><LUN>`
3.  每个子目录包含两个文件：一个数据文件和一个定义文件。

要打开设备的数据收集，请参见示例 3-22。

### 示例 3-22 启用 zFCP 统计

```
echo on=1 > definition
```

要关闭设备的数据收集，请参见示例 3-23。

### 示例 3-23 禁用 zFCP 统计

```
echo on=0 > definition
```

表 3-1 展示了不同统计类型输出格式的示例。

### 表 3-1 统计类型示例

| 统计类型 | 输出格式 | 行数 |
|---|---|---|
| Value（值） | <name> <total> | 1 |
| range（范围） | <name> <total> <min> <avg> <max> | 1 |
| list（列表） | <name> <Xn> <total for Xn> | <= entries_max |

