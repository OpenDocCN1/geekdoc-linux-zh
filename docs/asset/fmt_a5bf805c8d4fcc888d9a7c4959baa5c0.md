
# 禁用对广播的响应

## 你不希望自己变成 Smurf（呆灵攻击）的放大器

`net.ipv4.icmp_echo_ignore_broadcasts` = 1

## 在所有接口上启用路由验证

`net.ipv4.conf.all.rp_filter` = 1

## 启用 ipv6 转发

`net.ipv6.conf.all.forwarding` = 1

## 增加可能的 notify(7) 监听数量

`fs.inotify.max_user_watches` = 65536

此外，该工具可以从命令行执行特定的值。这里有几个非常有用的标志：

- `-A` – 打印所有值。当存储到文件时，如果硬件和内核假设是相同的，它们可以用来比较系统配置。这是驱动环境标准化的极佳方法，也可以测试更改并尝试理解为什么两个或多个具有相同设置的主机表现出不同的结果或行为。
- `-w` – 设置 `sysctl` 配置的更改。
- `-p` – 从配置文件（通常是 `sysctl.conf`）加载更改。

命令行的使用也非常方便，例如：

```
/sbin/sysctl -a
```

```
/sbin/sysctl -w sunrpc.min_resport = 200
```

## 第 4 章 深入研究系统

### 结论 (CONCLUSIONS)

初期的问题解决围绕着使用某些应用程序和工具展开。该过程的下一步将我们带入进程空间和内核，为了使用暴露任务结构的工具，我们需要对底层块有更深入的了解。与 Linux 交互的简单方法是通过 `proc` 文件系统（`proc-filesystem`），它提供了丰富的信息，并在更改该领域方面提供了极大的自由。困难、复杂的环境问题不可避免地导致这种情况，管理员会发现自己必须钻研内核以消除问题。此外，`proc` 在性能剖析和性能优化方面具有巨大优势，这两者在大规模数据中都至关重要。对进程空间和内核的熟悉允许我们迈出下一步，直接干预系统和任务。我们将在接下来的章节中学习如何跟踪和调试甚至是内核。

### 参考文献 (REFERENCES)

- `/proc`, n.d. 获取自：http://www.ldp.org/Filesystem-Hierarchy/proc
- Bar, M., 2000. `system calls`. 获取自：http://www.linuxjournal.com/article/404
- Corbet, J., `system calls` and the `vDSO`. 获取自：http://lwn.net/Articles/46528
- Cruz, F., 2011. `core memory`. 获取自：http://www.columbia.edu/cu/computing/core
- `/proc/sys/vm/` 的文档, n.d. 获取自：https://www.kernel.org/doc/vm
- 内内核参数, n.d. 获取自：https://www.kernel.org/doc/kernel-parameters.txt
- `mmmap(2)`, n.d. 获取自：http://linux-die.net/man2/mmap
- NFS 调试, n.d. 获取自：http://nitrid.org/wiki/NFS_Debugging
- `vDSO`, n.d. 虚拟 ELF 共享对象的概述, 获取自：http://man7.linux.org/man-pages/7vdso
- Peterson, J., 2005. What is linux-gate? 获取自：http://www.trilium.com/johnan/2005/08/linux-gate
- Seibold, S., 2009. `/proc` 文件系统. 获取自：https://www.kernel.org/doc/Documentation/filesystems/proc.txt
- `sysctl(8)`, n.d. 获取自：http://linux-die.net/man8/sysctl
- `tcpdump(8)`, n.d. 获取自：http://linux-die.net/man8/tcpdump

## 极客行为 – 应用程序的跟踪与调试

### 使用 STRACE 和 LTRACE

有时，通过读取日志和检查系统行为来调查问题无法产生结果的结果。影响你的客户群或应用程序的问题根源将仍然是一个谜。在这个阶段，你需要深入挖掘，这意味着分析受影响的进程。

### STRACE

`strace(1)` – Linux 手页, n.d. 是一个跟踪系统调用和信号的工具。如果你好奇系统调用是什么，它们是进程与操作系统（内核）之间的接口翻译机制（`GNU C Library` , n.d.）。这些调用可以被拦截和读取，从而更好地理解进程在运行时做什么。

通过挂钩这些调用，我们可以更好地了解进程的行为，特别是当它运行异常时。允许跟踪的操作系统功能称为 `ptrace(2)` – Linux 手页, n.d.。

在最简单的情况下，`strace` 运行指定的命令直到其退出。由于它会拦截并记录进程调用的系统调用以及进程接收的信号。每个系统调用的名称、参数及其返回值将打印在标准错误或日志文件中。

跟踪中的每行都包含系统调用名称，后面是括号中的参数及其返回值。让我们检查一个测试用例，我们将运行并跟踪 `dd` 命令，即 `dd <输入文件> <输出文件> <选项>`。当使用 `strace` 执行时，命令如下：

```
strace /bin/dd if=/dev/zero of=/tmp/file bs=1024K count=5
```

# 76 第 5 章 极客技术——应用程序的追踪与调试

现在，让我们来看 `strace` 命令的输出并对其进行分析：

```
execve("/bin/dd", ["", "if=/dev/zero", "of=/tmp/file", "bs=1024K", "count=5"], /*\n62 vars */) = 0

brk(0) = 0x60d000

mmap(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS,-1, 0) = 0xfffffd000

access("/etc/ld.so.preload") = -1 ENOENT (No such file or directory)

open("/etc/ld.so.cache", O_RDONLY) = 3

fstat(3, [st_mode=S_IFREG|0644, st_size=127604, ...]) = 0

mmap(NULL, 127604, PROT_READ, MAP_PRIVATE, 3, 0) = 0xfffffd000

close(3) = 0

open("/lib64/librt.so.1", O_RDONLY) = 3
```

代码的第一行是 `execve`，它执行了指定的程序。命令成功完成，如退出状态 (=0) 所示。

```
execve("/bin/dd", ["", "if=/dev/zero", "of=/tmp/file", "bs=1024K", "count=5"], /*\n62 vars */) = 0
```

相反，错误（通常返回值为 -1）会返回 `errno` 符号并附加相应的错误字符串，例如：

```
open("/foo/bar", O_RDONLY) = -1 ENOENT (No such file or directory)
```

同样地，信号会以信号符号和信号字符串的形式打印。

```
sigsuspend([]) <unfinished> -->
--- SIGINT (Interrupt) ---
++++ killed by SIGINT +++
```

# 77 使用 strace 和 itrace

让我们回到示例。第二行是 `brk(0)`。它改变了数据段的大小。

```
brk(0) = 0x60d000
```

在第三行，我们在调用进程的虚拟地址空间中创建新的映射。

```
mmap(NULL, 4096, PROT_READ|PRO_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0xffffffff000
```

第四个记录的系统调用是尝试访问 `/etc` 下的 `ld.so.preload` 文件。由于文件不存在，我们得到一个失败的调用，状态标记为 -1，并带有错误 `ENOENT`。

```
open("/etc/ld.so.preload", R_OK) = -1 ENOENT (No such file or directory)
```

第五行也很有趣。在这里，我们可以看到成功以只读对象打开了 `/etc/ld.so.cache` 文件。我们还可以看到该文件映射到了文件描述符 3。确实，在日志后面，有一个 `close(3) = 0` 关闭了该描述符。

```
open("/etc/ld.so.cache", O_RDONLY) = 3
```
