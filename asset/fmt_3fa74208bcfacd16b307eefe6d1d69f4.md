
`vmemoryuse` unlimited

`descriptors` 1024

`memoryunlocked` unlimited

`maxproc`     unlimited

```
```

**图 10.30** 在 `csh` 和 `tsh` 中查看账户限制。

## 生成程序映像或 core 文件

使用 `gcore` 获取程序映像或 `core` 文件的方法首先涉及获取一个运行中的程序并获取其进程标识符。本节假设你想要分析或调试的程序已经在运行。正如第 6 节“作业与进程管理”中所述，你可以使用 `ps` 命令获取进程标识符。图 10.34 演示了获取和使用目标程序进程标识符的示例。请参考获取你特定程序的进程标识符。

# UNIX/Linux 简介

一旦获取了进程标识符（PID），你可以使用该进程标识符作为单个参数调用 `gcore`。随后，`gcore` 将将程序镜像保存到名为 `core` 的文件中，并以进程标识符作为扩展名。10.34 也通过示例进程标识符说明了这种调用方式。一旦获得 `core` 文件，你就可以继续“调试或分析程序 core 文件或镜像”章节。

```bash
Intro_to_UNIX/chap10/multi_file_c++ ps -ef grep sor

book 2630 2158 9 01:51/18 00:00:06 sor

book 2632 2158 0 01:51/18 00:00:00 grep sor

Intro_to_UNIX/chap10/multi_file_c++ gcore 2630
```

**图 10.34** 获取用于 `gcore` 程序的进程标识符。

## 在 gdb 中获取镜像或 core 文件

在 `gdb` 内部获取镜像或 `core` 文件的方法涉及内置了 `gcore` 的新版本 `gdb`。因此，在这种方法中，你通过 `gdb` 访问 `gcore`。你必须首先带有所需的程序启动 `gdb`，在本例中，就像你在图 10.12 中做的那样作为参数传入。一旦打开相应程序启动 `gdb`，你可以选择性先设置断点（原因见下文），或者直接运行程序。

假设你选择运行程序，并在一段时间后（例如几秒钟）捕捉程序的快照。图 10.35 说明了这一想法。在这里，开始运行，几秒钟后通过发送 `ctrl-c` 临时停止其执行。程序被中断后，执行 `gcore` 将当前执行点的快照捕捉到一个名为 `core` 的文件中，并以进程标识符作为扩展名。此时，你可以选择退出 `gdb`、进一步分析程序或继续执行程序。无论何种情况，你都可以像下一节所示继续分析捕获的镜像。

```gdb
(gdb) run

Starting program: /home/book/Intro_to_UNIX/chap10/multi_file_c++/sor

init...

s...

Program received signal SIGANT, Interrupt.

0x0804808 in Sort_timestep (grid=0x8049ae0, grid1=0x87eace0) at sort.cpp:43

grid1[row][col] = (grid[0][row-1][col] +

(gdb) gcore

Saved corefile,2905

(gdb)
```

**图 10.35** 在 `gdb` 中捕捉 `core` 文件或镜像。

如果你想在程序内的某个特定点捕捉程序执行的 `core` 文件镜像，可以像在本章前面的部分那样使用断点。这里的核心思想是在你想要捕捉和分析程序的地方设置断点。一旦程序在该断点处停止，你可以在 `gdb` 提示符下执行 `gcore`，以生成该断点处的快照。

由 `gcore` 捕捉的 `core` 文件或程序镜像将以“`core`”为文件名，后跟当时运行的被捕获程序的进程标识符来创建。

![](img/e3ac56d195b48617d5ae42cd57458af3_364_0.png)

## 调试或分析程序 core 文件或镜像

一旦通过上述任一方法获取了程序的 `core` 文件或镜像，你就可以结合可执行程序来调试或分析该 `core` 文件或镜像。如果源代码和对象文件也可用，调试器将能够提供程序的详细信息，例如行号和源代码名称。

要开始调试或分析该程序的 `core` 文件或镜像，你可以执行 `gdb`，如图 10.36 所示。在这种情况下，`gdb` 的参数是 `core` 文件或程序镜像的。此示例指定了之前通过 `gdb` 和 `gcore` 获取的 `core` 文件名。如果 `core` 文件是通过 `gdb` 和/或 `gcore` 获取的，请指定该情况下生成的带有进程标识符扩展名的 `core` 文件名。相反，如果 `core` 文件是因为程序异常终止而生成的，你将 `core` 文件作为参数提供。

```bash
/Intro/to_UNIX/chap10/multi_file.c++ gdb sor core.2905
```

图 10.36 通过核心 文件或镜像对程序进行调试和分析。

一旦使用 `core` 文件或镜像启动了调试器，你可能想要学习的内容之一是程序在捕捉发生时正在执行何。这在程序异常终止时特别有用，因为你可以此了解终止发生在程序的哪个位置。要了解捕捉发生时程序的执行位置，你可以执行堆栈跟踪（stack trace），如图 10.37 所示。

```gdb
(gdb) where

#0 0x08048708 in Sor_Timestep(grid0=0x8043ae0, grid1=0x87eace0) at sor.cpp:43

#1 0x0804878d in Sor_Complete(grid0=0x8043ae0, grid1=0x87eace0) at sor.cpp:43

grid1[row][col] = (grid[0][row-1][col] +

(gdb) )
```

图 10.37 捕捉发生时程序正在执行的位置。

# UNIX/Linux 简介

```
// /Intro_to_UNIX/chap10/multi_file.c++ g++ -pg -c debug.cpp
// /Intro_to_UNIX/chap10/multi_file.c++ g++ -pg -c main.cpp
// /Intro_to_UNIX/chap10/multi_file.c++ g++ -pg -c sort.cpp
// /Intro_to_UNIX/chap10/multi_file.c++ g++ -pg -o debug.o main.o sort.o
```

**图 10.38** 数据将包括其他信息、函数调用和带有时间样本的执行。

`gmon.out`。通过时间样本，程序通常会记录正在执行哪个函数。本讨论将展示这些系统每 1/100 秒产生一次的“样本”，这是许多 UNIX/Linux 系统的采样率。无论采样频率如何，在程序执行结束时，函数的计数意味着其估计执行了许多采样周期。例如，如果发现某个函数在发生 20 次时间样本时正在执行，性能分析器将估计该函数占整个程序运行时间的 20/100 秒。

![](img/e3ac56d195b48617d5ae42cd57458af3_367_0.png)

在较新的 UNIX 或 Linux 系统（如 Linux 2.6）上，采样频率可能高达 1/1000 秒。这允许性能分析工具进行更准确的运行时估计。然而，除非该类型的系统升级了性能分析程序以补偿增加的采样率，否则性能分析器报告的运行时测量可能比实际值高十倍。如果是这种情况，请升级性能分析器，或将时间数字除以 10 以查看更实用的结果。

使用时间样本可以很好地分析每个函数占程序运行时间的百分比。然而，通过时间采样估计的运行时可能与实际观察到的运行时间略有不同。尽管如此，时间采样是一种不受系统负载影响的性能分析形式。例如，无论被分析的程序是在空闲（低系统负载）还是忙碌（高系统负载）的机器上执行，估计的运行时间量和百分比变化都很小。

程序执行完成后，你随后调用性能分析器并提供被分析程序的名称，以获取性能报告，如图 10.39 所示。无论你使用 `prof` 还是 `gprof`，其输出都可能超过一个屏幕，因此可能需要将输出重定向到文件中（此处所示）或将输出通过到 `less`。

此时，你可以查看性能分析报告来分析程序的性能，如下一节所述。

## 使用 C/C++ 编程

```
$/Intro_to_UNIX/chap10/multi_file_c++$ .sor

init...

sor...

sor complete.

~/Intro_to_UNIX/chap10/multi_file_c++$ gprof sor >sor
```
