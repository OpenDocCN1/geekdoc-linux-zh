

# 进入内核模式

长度超过 8 条指令。这允许实现无分支的内联处理程序，使得整个处理程序都能放入陷阱表（trap table）槽位中。

图 2.3 显示了 UltraSPARC I & II 的陷阱表布局。

| 陷阱表内容 | 陷阱类型 |
|---|---|
| 硬件中断 (Hardware Traps) | 000...07F |
| 中断级别 = 0 | 溢出/填充中断 (Spill/Fill Traps) | 080...0FF |
| | 软件中断 (Software Traps) | 100...17F |
| | 预留 (Reserved) | 180...1FF |
| 中断级别 > 0 | 硬件中断 (Hardware Traps) | 000...07F |
| | 溢出/填充中断 (Spill/Fill Traps) | 080...0FF |
| | 软件中断 (Software Traps) | 100...17F |
| | 预留 (Reserved) | 180...1FF |

图 2.3 UltraSPARC I & II 陷阱表布局

## 2.2.3.5 软件中断

软件中断由 SPARC 陷阱指令 `Tcc` 触发。陷阱指令的机器码包含一个 6 位的软件中断编号，该编号索引到陷阱表的软件部分。软件中断主要用于 Solaris 内核中的系统调用。

系统调用有三种软件中断：一种用于原生系统调用，一种用于 32 位系统调用（当在 64 位内核上运行 32 位应用程序时），以及一种用于与 SunOS 4.x 二进制兼容的系统调用。系统调用通过在全局寄存器中设置系统调用号并发出陷阱指令，从而通过一个通用陷阱进行向量化。我们将在第 44 页的“系统调用”中更详细地讨论普通系统调用。

还有实现为独立陷阱的超快速系统调用（ultra-fast system calls）。这些系统调用通过寄存器传递其简单参数。由于系统调用不在栈上传递参数，在进入内核模式期间需要保存的进程状态较少，从而实现了更快的系统调用实现。快速系统调用（例如 `get_hrestime`）是与时间相关的调用。

表 2-2 列出了 UltraSPARC 软件中断，包括超快速系统调用。

## 表 2-2 UltraSPARC 软件中断

| 陷阱定义 | 陷阱类型值 | 优先级 |
|---|---|---|
| 陷阱指令 (SunOS 4.x 系统调用) | 100 | 16 |
| 陷阱指令 (用户断点) | 101 | 16 |
| 陷阱指令 (除零错误) | 102 | 16 |
| 陷阱指令 (刷新窗口) | 103 | 16 |
| 陷阱指令 (清理窗口) | 104 | 16 |
| 陷阱指令 (执行未对齐引用) | 106 | 16 |
| 陷阱指令 (32 位系统调用) | 108 | 16 |
| 陷阱指令 (设置 trap0) | 109 | 16 |
| 陷阱指令 (用户中断) | 110–123 | 16 |
| 陷阱指令 (get hrtime) | 124 | 16 |
| 陷阱指令 (get xrtime) | 125 | 16 |
| 陷阱指令 (self xcall) | 126 | 16 |
| 陷阱指令 (get hrestime) | 127 | 16 |
| 陷阱指令 (trace) | 130-137 | 16 |
| 陷阱指令 (64 位系统调用) | 140 | 16 |

## 2.2.3 陷阱分析工具

一个解绑工具 `trapstat` 能够动态监控陷阱活动。该工具会统计在参数指定的间隔间隔内，系统中每个处理器发生的每种类型陷阱的数量。目前，该工具实现在 UltraSPARC 和 Intel x86 处理器架构上，并适用于 Solaris 7 及以后的发布版本。

你可以从本书的网站下载 `trapstat`：http://www.solarisinternals.com。只需解压压缩包并使用 `add_drv` 命令安装驱动程序。

> 注意：Sun 不支持 `trapstat`。不要在生产机器上使用它，因为它会将代码加载到内核。

```
# tar xvf trapstat28.tar
-xr-xr-x 0/2 52668 Jan 31 03:57 2000 /usr/bin/trapstat
-rxr-xr-x 0/1 33452 Feb 10 23:17 2000 /usr/bin/sparc7/trapstat
-rwxr-xr-x 0/1 40432 Feb 10 23:16 2000 /usr/bin/sparc9/trapstat
-rw-xr--r 0/1 21225 Sep 11 22:58 1999 /usr/kernel/drv/trapstat
-rw-r--r-- 0/1 188 Aug 31 10:06 1999 /usr/kernel/drv/trapstat.conf
-rw-rw--r-- 0/1 37328 Sep 08 17:28 1999 /usr/kernel/drv/sparc9/trapstat.conf
# add_drv trapstat
```

一旦安装了 `trapstat`，可以使用它来分析在每个处理器上发生的陷阱。

| vct | name | cpu0 | cpu1 |
|---|---|---|---|
| 24 | cleanwin | 3636 | 4285 |
| 41 | level-1 | 99 | 1 |
| 45 | level-5 | 1 | 0 |
| 46 | level-6 | 60 | 0 |
| 47 | level-7 | 2 | 0 |
| 4a | dlevel-10 | 100 | 0 |
| 4d | dlevel-13 | 31 | 67 |
| 4e | dlevel-14 | 100 | 0 |
| 60 | int-vec | 161 | 90 |
| 64 | tlb-miss | 5129 | 11528 |
| 68 | dtlb-miss | 39130 | 82077 |
| 6c | dtlb-proc | | |
| 84 | spill-1-normal | 1210 | 99 |
| 8c | spill-1-normal | 1210 | 99 |
| 98 | spill-1-normal | 1210 | 99 |
| a4 | spill-1-normal | 1210 | 99 |
| ac | spill-1-normal | 1210 | 99 |
| c4 | spill-1-normal | 1210 | 99 |
| cc | spill-1-normal | 1210 | 99 |
| d8 | spill-1-normal | 1210 | 99 |
| 103 | spill-1-normal | 1210 | 99 |
| 108 | spill-1-normal | 1210 | 99 |
| 124 | spill-1-normal | 1210 | 99 |
| 127 | spill-1-normal | 1210 | 99 |

*(注：原文提供的表格数据部分似乎存在重复或错位，译文已保持原始逻辑结构)*

