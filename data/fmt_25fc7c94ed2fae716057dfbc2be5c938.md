
# 第 13 章 开发工具

![](img/75da989fc023923ea1a768dd5ab686d4_369_0.png)

图 13-1 数据显示调试器

DDD 的调用方式如下：

```
$ ddd --debugger xscale_be-gdb webs
```

如果不使用 `--debugger` 标志，DDD 将尝试调用你开发宿主机上的原生 GDB。如果你计划在目标系统上调试应用程序，这并不是你想要的。DDD 命令行的第二个参数是你将要调试的程序。更多细节请参阅 DDD 手册。

使用如图 13-1 所示的命令行工具，你可以单步执行程序。你可以通过图形界面，也可以通过 DDD 屏幕底部的 GDB 控制窗口来设置断点。对于目标调试，你必须首先如列表 13-4 所示，使用 `target` 命令将调试器连接到目标系统。该命令在 DDD 主界面的 GDB 窗口中发出。

当你连接到目标系统后，可以执行与刚才所示序列类似的命令来隔离程序故障位置。图 13-2 显示了此调试会话后期阶段的 DDD 显示。

![](img/75da989fc023923ea1a768dd5ab686d4_370_0.png)

图 13-2 DDD 中的调试会话

注意在图 13-2 中，我们已经启动了一些重要变量的显示，这有助于我们缩小段错误的原因。在使用图中命令行工具单步执行程序时，我们可以观察这些变量。DDD 是 GDB 的一个强大前端。它相对易用，并且被许多开发宿主机支持。请参考本章最后一节获取 GNU 文档链接。需要注意的是，随着时间的推移，Eclipse 掩盖了（双关语！）成为了首选的调试器。由于空间限制无法进行详细介绍。本章末尾包含了 Eclipse 的引用，以防你需要的更多信息。

## 13.3 cscope

我们引入 cscope 是因为这个方便工具的支持已经进入 Linux 内核源码。cscope 是一个简单的源码浏览工具，可以让你根据符号在大型源码树中轻松导航。像 Ubuntu 这样的发行版在仓库中包含 cscope，但其他则没有。在 Ubuntu 上，只需输入以下：

```
sudo apt-get install cscope
```

Linux Makefile 支持构建 cscope 使用的数据库。以下是来自近期 Linux 快照的一个示例调用：

```
$ ARCH=powerpc CROSS_COMPILE=powerpc-linux-gnue- cscope
```

如果你愿意，可以单独使用 cscope。它是命令驱动的且非常强大，但不像图形化点点点击时代那么简单。如果 vi 仍然是你最喜欢的编辑器，要调用 cscope，只需在不带参数的情况下进入目录。图 13-3 显示了一个示例会话。你可以在最后一节中阅读关于这两个有用工具的介绍。

![](img/75da989fc023923ea1a768dd5ab686d4_371_0.png)

图 13-3

## 13.4 跟踪与分析工具

许多实用的工具为你提供了系统的各种视图。某些工具提供了高层次视角。你可以发现系统上正在运行哪些进程以及哪些进程正在消耗 CPU 带宽。其他工具提供了详细分析，例如内存是在哪里分配的，甚至是是否正在泄露。接下来几节介绍了该类别中最重要的工具和实用程序。我们对这些工具仅进行了简要介绍；具体的细节请参考相应的参考文献。

### 13.4.1 strace

在章早些部分为 GDB 准备示例软件时，我决定使用一个我不熟悉的项目——GoAhead 嵌入式服务器的早期版本。首次编译和链接项目的尝试为 strace 提供了一个有趣的例子。从命令行启动应用程序，它静默地返回到了控制台。没有产生错误消息，系统日志列表也没有提供任何线索。它无法运行。strace 迅速识别了问题。列表 13-5 显示了在此应用程序上调用它时的输出。由于坐标原因，输出中的许多行已被删除。未编辑的输出超过了一百行。

列表 13-5 strace 输出：GoAhead Web 演示

```
01 root@coyote:$ strace ./websdemo
02 execve("/websdemo", ["./websdemo"]) = 0
03 uname(sys="Linux", node="coyote", ...) = 0
04 brk(0) = 0x1003050
05 open("/etc/ld.preload", O_RDONLY) = -1 ENOENT (No such file or directory)
06 open("/etc/ld.cache", O_RDONLY) = -1 ENOENT (No such file or directory)
```

列表 13-5 续

```
07 open("/lib/libc.so.6", O_RDONLY) = 3
08 read(3, "\177ELF\1\2\1\0\0\0\0\3\24\0\0\1\32",..., 1024)
09 fstat(0x3, 0xfffef0c) = 0
10 mmap(0xe9f0000, 1379388, PROT_READ|PROT_EXEC, MAP_PRIVATE, 3, 0) = 0xe9f000
11 mprot(0xfffd000, 97340, PROT_NONE) = 0
12 mmap(0xfffd000, 61440, PROT_READ|PROT_WRITE|PROT_EXEC, MAP_PRIVATE, 3, 0x13000) = 0xfffd000
13 mmap(0xfffee00, 7228, PROT_READ|PROT_WRITE|PROT_EXEC, MAP_PRIVATE|MAP_ANMOUS, -1, 0) = 0xfffee00
14 close(3) = 0
15 brk(0) = 0x0103050
16 brk(0x0103200) = 0x013000
17 brk(0x0103300) = 0x013000
18 brk(0x0103400) = 0x010400
19 sigaction(SIGPIPE, SIG_IGN, 8) = 0
20 stat("/config.txt") = -1 ENOENT (No such file or directory)
21 uname(sys="Linux", node="coyote", ...) = 0
22 gettimeday(3301, 178955, NULL) = 0
23 getpid() = 156
24 open("/etc/resolv.conf", O_RDONLY) = 3
25 fstat(0x3, 0xfffef78) = 0
26 mmap(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANMOUS, -1, 0) = 0x30001700
27 read("/resolv.conf", This file is..., 4096) = 83
28 read(3, "", 4096) = 0
29 close(3) = 0
82 socket(AF_INET, SOCK_GRAM, IPPROTO_IP) = 3
83 connect(3, {sa_family=AF_INET, sin_port=htons(53), sin_addr("0.0.0.0")}, 28) = 0
85 gettimeday(3301, 549664, NULL) = 0
86 poll({3, events=POLLIN,POLLERR}, 1, 5000) = 1
87 ioctl(3, 0x040467f, 0xfffffe8) = 0
88 recvfrom(3, 0xffffff0, 1024, 0, 0xfffffe68, 0xfffffe6ac) = -1 ECONNREFUSED (Connection refused)
89 close(3) = 0
90 socket({PF_INET, SOCK_GRAM, IPPROTO_IP}) = 3
91 connect(3, {sa_family=AF_INET, sin_port=htons(53), sin_addr("0.0.0.0")}, 28) = 0
92 send(3, "\s\n\n\n\ncoyote\n\n\n\n*", 24, 0) = 24
93 gettimeday(3301, 552839, NULL) = 0
94 poll({fd=3, events=POLLIN,events=POLLERR}, 1, 5000) = 1
95 ioctl(3, 0x040067f, 0xfffffe68) = 0
96 recvfrom(3, 0xffffff0, 1024, 0, 0xfffffe68, 0xfffffe6ac) = -1 ECONNREFUSED (Connection refused)
97 close(3) = 0
98 exit(-1) = 255
99 root@coyote:/home/websdemo#
```

strace 在输出中添加了行号，使此列表更易读。应用程序在第 01 行在 strace 下启动。在最简单的情况下，只需将 `strace` 命令直接放在你想要检查的程序前面即可。这就是列表 13-5 输出的产生方式。

跟踪的每一行都代表 websdemo 应用程序向内核发送的一个离散系统调用。我们不需要分析并理解跟踪的每一行，尽管这样做非常有启发性。我们正在寻找任何可能帮助定位程序无法运行的异常。在最初几行中，准备了程序将执行的环境。我们看到对 `/etc/ld.so.*` 的 `open()` 系统调用，这是 Linux 动态链接器-加载器 (ld.so) 正在执行它的工作。事实上，链接器缓存文件大大加快了共享库引用的搜索。这随后通过运行 `ldconfig` 得到了解决。

到第 19 行是更基础的维护工作，主要由链接器和 libc 初始化完成。注意在第 20 行，程序查找配置文件但没有找到。当我们运行软件时，这可能是一个重要问题。从第 24 行开始，程序开始设置和配置所需的适当网络资源。

特别注意第 82 行开始的网络活动。在这里，程序尝试对一个全 0 的 IP 地址建立 TCP/IP 连接。为了方便起见，这里还原了第 82 行：

```
socket(PF_INET, SOCK_DGRAM, IPPROTO_IP) = 3
```

列表 13-5 有几点值得注意。我们可能不知道每个系统调用的所有细节，但我们可以对正在发生的情况有一个大致的了解。`socket()` 系统调用类似于文件系统的 `open()`。其返回值（在本例中由 `=` 号表示）代表一个 Linux 文件描述符。知道此点，我们可以将第 82 行的活动通过第 89 行的 `close()` 系统调用与描述符 3 联系起来。

我们对这组相关的系统调用感兴趣，因为我们在第 88 行看到一个错误：Connection refused（连接被拒绝）。此时，我们仍然不知道程序为什么不运行，但这看起来是不正常的。让我们来调查一下。第 82 行的 `socket()` 系统调用为 IP 通信建立了一个端点。第 83 行很可疑，因为它尝试连接到一个包含全 0 IP 地址的远程端点（socket）。我们不需要成为专家就能怀疑这可能导致了问题。第 84 行提供了另一个重要线索：端口参数被设置为 53。在互联网上快速搜索 TCP/IP 端口号可以发现端口 53 是域名系统服务（DNS）。

第 84 行提供了另一个线索。我们的开发板主机名为 `coyote`。这可以在列表 13-5 的第 01 行的命令提示符中看到。似乎这项活动是对我们开发板主机名的 DNS 查找，而该查找失败了。作为一个实验，我们在目标系统的 `/etc/hosts` 文件中添加了一个条目，将本地定义的主名与开发板的本地 IP 地址关联，如下：

```
coyote  192.168.1.21      # 我们分配的 IP 地址
```

搞定。我们的程序开始正常运行。尽管我们可能并不确切知道为什么会导致程序失败（如果我们是 TCP/IP 网络专家），但我们的输出引导我们发现了事实：对板名的 DNS 查找失败了。当我们纠正了这一点后，程序愉快地启动并开始提供 Web 页面。总结一下，这是一个我们没有源代码供参考的程序，而且它的二进制镜像中没有编译符号。通过使用 `strace`，我们能够确定程序失败的原因并实施解决方案。

4 有时在这种语境下，全 0 地址是合适的。然而，我们正在调查程序异常终止的原因，因此我们应该考虑这个疑点。

### 13.4.2 trace 变体

`strace` 工具有许多命令行选项。最实用的之一是能够选择系统调用的子集进行跟踪。例如，如果你只想查看特定进程与网络相关的活动，可以执行命令：

```
$ strace -e trace=network process_name
```

这将产生所有与网络相关的系统调用的跟踪，例如 `socket()`、`connect()`、`recvfrom()` 和 `send()`。这是查看特定程序网络活动的一种强大方法。其他子集。例如，你可以查看程序与文件相关的活动，包括 `open()`、`close()`、`read()`、`write()` 等。额外的子集还包括进程相关的系统调用、信号相关的系统调用以及 IPC（进程间通信）相关的系统调用。

值得注意的是，`strace` 可以处理产生额外进程的程序。使用 `-f` 选项调用 `strace` 会指示跟踪使用 `fork()` 系统调用创建的子进程。`strace` 命令有许多可能性。精通这个强大工具的最佳方法就是使用它。务必寻找并阅读与这些其他工具相关的最新开源文档。在这种情况下，在大多数 Linux 主机上的 `man strace` 产生的材料足够让你实验一整个下午！

使用 `strace` 的一种非常有用的方法是使用 `-c` 选项。该选项会对你的应用程序进行高层性能分析。使用 `-c` 选项，`strace` 会对每个系统调用积累统计信息，包括遇到了多少次、返回了多少错误以及在每个系统调用上花费的时间。列表 13-6 就是示例。

### 列表 13-6 strace 性能分析

```
root@coyote$ strace -c ./webs
time        seconds usecs/calls    errors syscall
```

| time | seconds | usecs/calls | errors | syscall |
|---|---|---|---|---|
| 29.80 | 0.034262 | 189 | 181 | send |
| 18.46 | 0.021226 | 1011 | 21 | 10 open |
| 14.11 | 0.016221 | 130 | 125 | read |
| 11.87 | 0.013651 | 506 | 27 | 8 stat64 |
| 5.88 | 0.006762 | 193 | 35 | select |
| 5.28 | 0.006072 | 76 | 80 | fcntl64 |
| 3.47 | 0.003994 | 65 | 61 | time |
| 2.79 | 0.003205 | 3205 | 1 | execve |

### 列表 13-6 续

| time | seconds | usecs/calls | errors | syscall |
|---|---|---|---|---|
| 1.71 | 0.001970 | 90 | 22 | recv |
| 1.62 | 0.001868 | 85 | 22 | close |
| 1.61 | 0.001856 | 169 | 11 | shutdown |
| 1.38 | 0.001586 | 144 | 11 | accept |
| 0.41 | 0.000470 | 94 | 5 | mmap |
| 0.26 | 0.000301 | 100 | 3 | mprotect |
| 0.24 | 0.000281 | 94 | 3 | brk |
| 0.17 | 0.000194 | 194 | 1 | access |
| 0.13 | 0.000150 | 150 | 1 | lseek |
| 0.12 | 0.000141 | 47 | 3 | uname |
| 0.11 | 0.000132 | 132 | 1 | listen |
| 0.11 | 0.000128 | 128 | 1 | socket |
| 0.09 | 0.000105 | 53 | 2 | fstat64 |
| 0.08 | 0.000097 | 97 | 1 | munmap |
| 0.06 | 0.000064 | 64 | 1 | getcd |
| 0.05 | 0.000063 | 63 | 1 | bind |
| 0.05 | 0.000054 | 54 | 1 | setsockopt |
| 0.04 | 0.000048 | 48 | 1 | rt_sigaction |
| 0.04 | 0.000046 | 46 | 1 | gettimeday |
| 0.03 | 0.000038 | 38 | 1 | getpid |
| 100.00 | 0.114985 | 624 | 22 | total |

这是一种非常有用的方法，可以获取你的应用程序消耗时间以及发生错误的视图。某些错误可能是应用程序运行的一部分，但另一些可能以意料之外的方式消耗时间。从列表 13-6 可以看到，持续时间最长的系统调用是 `execve()`，这是 shell 用于启动程序的调用。你可以看到，它只被调用了一次。另一个有趣的观察是 `send()` 系统调用最频繁。这是合理的，因为应用程序是一个小型 Web 服务器。

请记住，与这里讨论的其他工具一样，`strace` 必须为你的目标架构编译。它在你的开发板而不是开发主机上执行。你必须使用与架构兼容的版本。如果你购买商用嵌入式 Linux 发行版，应该确保该工具包含了你所选的架构。

### 13.4.3 ltrace
