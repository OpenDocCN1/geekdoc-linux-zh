
许多系统使用如 `kvm open`、`kvm nlist` 和 `kvm read` 等例程通过 `/dev/knem` 设备直接访问内核数据结构。通常，这些程序打开 `/dev/knem`，读取内核的符号表，通过该表定位运行中内核中的数据，并使用这些例程读取内核地址空间中相应的地址。由于这要求用户程序和内核对以这种方式读取的数据结构的大小和格式达成一致，此类程序通常需要针对每个内核修订版本、CPU 类型等进行重新编译。

### 10.4.2 ptrace 和 /proc 文件系统

`ptrace` 系统调用用于 4.BSD 和 SVID 来控制进程并从中读取信息。它在经典上被调试器用于：例如捕获运行进程的执行（trap）或检查其状态。在 SVR4 下，`ptrace` 被 `/proc` 文件系统取代，后者表现为一个目录，其中包含每个运行进程的文件条目，并以进程 ID 命名。用户程序可以打开与其感兴趣进程对应的文件，并对其执行各种 `ioctl` 调用以控制其执行或从内核获取有关进程的信息。同样，程序可以通过 `/proc` 文件系统的文件描述符直接在进程地址空间中读写数据。

### 10.4.3 Linux 下的进程控制

在 Linux 下，支持用于进程控制的 `ptrace` 系统调用，其工作方式与 4.BSD 一。为了获取进程和系统信息，Linux 也提供了 `/proc` 文件系统，但语义非常不同。在 Linux 下，`/proc` 包含许多提供通用系统信息的文件，如内存使用情况、平均负载和网络统计数据。这些文件通常使用 `read` 和 `write` 进行访问，其内容可以使用 `scanf` 解析。Linux 下的 `/proc` 文件系统还为每个运行进程提供一个以进程 ID 命名的目录条目，其中包含命令行、当前工作目录链接、可执行文件、打开的文件描述符等等信息的文件条目。内核在响应读取请求时会在文件中提供所有这些信息。这种实现与 Plan 9 Find 的 `/proc` 文件系统并不相似，但它也有缺点——例如，对于像 `ps` 这样需要列出所有运行进程信息表的工具，必须遍历许多目录并打开、读取许多文件。相比之下，其他 UNIX 系统上使用的 kvm 例程只需几次系统调用即可直接读取内核数据结构。

显然，这种实现方式差异巨大，使得迁移使用它们的应用程序被证明是一项真正的任务。应该指出，SVR4 的 `/proc` 文件系统与 Linux 的是完全不同的东西，它们可能无法在相同的语境中使用。可以争认为，任何使用 kvm 例程或 SVR4 `/proc` 文件系统的程序都是不可移植的，这些代码部分应该针对每个操作系统进行重写。

Linux 的 `ptrace` 调用与 BSD 中找到的几乎相同，但有几处不同：

- BSD 下的 `TRACEPEEKUSER` 和 `TRACEPOKEUSER` 请求在 Linux 下分别命名为 `TRACEPEEKUSR` 和 `TRACEPOKEUSR`。
- 进程寄存器可以使用 `TRACEPOKEUSER` 请求配合 `/usr/include/linux/ptrace.h` 中的找到偏移量进行设置。
- SunOS 的请求 `TRACE.{READ,WRITE}{TEXT,DATA}` 不被支持，`TRACESETACBRKPT`、`TRACESETWRBRKPT`、`TRACECLRBRKPT` 或 `TRACEDUMPCORE` 也是。这些缺失的请求只会影响少数现有程序。

Linux 没有提供从用户程序读取内核地址空间的 kvm 例程，但某些程序（最著名的 `kmem ps`）实现了这些例程的自己的版本。通常，这些是不可移植的，任何使用 kvm 例程的代码可能都依赖内核中某些符号或数据结构的可用性——这不是一个安全的假设。使用 kvm 例程应被视为特定于架构。

## 10.5 可移植的条件编译

如果你需要修改现有代码以将其迁移到 Linux，你可能需要使用 `ifdef...endif` 对来包围 Linux 特有的代码——或者说，对应于其他实现的代码。目前还没有关于选择在操作系统上编译哪些代码部分的真实标准，但许多程序使用一种约定，例如为 System V 代码定义 `SVR4`，为 BSD 代码定义 `BSD`，为 Linux 特有的代码定义 `linux`。

Linux 使用的 GNU C 库允许你在编译时定义各种宏来开启库的各种特性。这些是：

- `_STRICT_SOURCE`: 仅用于 ANSI C 功能
- `_POSIX_SOURCE`: 用于 POSIX.1 功能
- `_SOURCE`: 如果定义为 1，则为 POSIX.1 功能；如果定义为 2，则为 POSIX.2 功能。
- `_BSDSOURCE`: ANSI、POSIX 和 BSD 功能。
- `_SVIDSOURCE`: ANSI、POSIX、SVID 功能。
- `_GNU_SOURCE`: ANSI、POSIX、SVID 和 BSD 功能，加上 GNU 扩展。
- `_XGL_SOURCE`: ANSI、POSIX、SVID 和 BSD 功能，加上 X 及其 GL 扩展。

## 10.6 补充说明

本章涵盖了除上一章列出的缺失系统调用之外的大多数迁移问题。

## 第 11 章 按字母顺序排列的系统调用

- `fsync` - 将文件缓存写入磁盘 (mc)
- `ftime` - 获取自 1.1.1970 以来的秒数 (m|c)
- `truncate` - 更改文件大小 (mc)
- `fwrite` - 向流写入二进制数据数组 (m+|c)
- `get kernel syms` - 获取内核符号表或其大小 (-)
- `getdomname` - 获取系统域 (m|c)
- `getdtabsize` - 获取文件描述符表大小 (m|c)
- `getgid` - 获取有效组 ID (m+c)
- `getuid` - 获取有效用户 ID (m+c)
- `getgid` - 获取实际组 ID (m+c)
- `getgroups` - 获取附加组 (m+c)
- `gethostid` - 获取唯一主机标识符 (m|c)
- `gethostname` - 获取系统主机名 (m|c)
- `gettimer` - 获取间隔定时器的值 (mc)
- `getpagesize` - 获取系统页大小 (m-|c)
- `getpeername` - 获取已连接对端套接字的地址 (m|c)
- `getgid` - 获取进程的父组 ID (+)
- `getgrgrp` - 获取当前进程的父组 ID (m+c)
- `getpid` - 获取进程的 ID (m+c)
- `priority` - 获取进程/组/用户优先级 (mc)
- `getlimit` - 获取资源限制 (mc)
- `getrusage` - 获取资源使用情况 (m)
- `getsockname` - 获取套接字的地址 (m|c)
- `getsockopt` - 获取套接字的选项设置 (m|c)
- `getimeofday` - 获取自 1.2.1970 以来的时区+秒数 (mc)
- `getuid` - 获取实际 UID (m+c)
- `gty` - 尚未实现 ()
- `idle` - 使进程成为交换候选对象 (mc)
- `init module` - 插入可加载内核模块 (-)
- `ioctl` - 操作字符设备 (mc)
- `ioperm` - 设置某些 I/O 端口的权限 (m-c)
- `iopl` - 设置所有 I/O 端口的权限 (m-c)
- `ipc` - 进程间通信 (-c)
- `kill` - 向进程发送信号 (m+c)
- `killpg` - 向进程组发送信号 (mc!)
- `klog` - 查看系统日志 (-)
- `link` - 为现有文件创建硬链接 (m+c)
- `listen` - 监听套接字连接 (m|c)
- `llseek` - 用于大文件的 lseek (-)
- `lock` - 尚未实现 ()
- `lseek` - 更改文件描述符的指针位置 (m+c)
- `lstat` - 获取文件状态 (mc)
- `mkdir` - 创建目录 (m+c)
- `mknod` - 创建设备 (mc)
- `mmap` - 将文件映射到内存 (mc)
- `lldt` - 读取或写入本地描述符表 (-)
- `mount` - 挂载文件系统 (mc)
- `mprotect` - 读、写或执行保护的内存 (-)
- `mpx` - 尚未实现 ()
- `msgctl` - IPC 消息控制 (m|c)
- `msgget` - 获取 IPC 消息队列 ID (m|c)
- `msggrcv` - 接收 IPC 消息 (m|c)
- `msgsnd` - 发送 IPC 消息 (m|c)

| `munmap` | 从内存中取消映射文件 (mc) |

| `nice` | 更改进程优先级 (mc) |

| `oldstat` | 已不再存在 |

| `oldstat` | 已不再存在 |

| `oldolduname` | 已不再存在 |

| `oldstat` | 已不再存在 |

| `olduname` | 打开文件 (m+c) |

| `pathconf` | 获取文件信息 (m+|c) |

| `pause` | 睡眠直到信号 (m+c) |

| `personality` | 更改 ibcs 的当前执行域 (-) |

| `phys` | 尚未实现 (m) |

| `pipe` | 创建管道 (m+c) |

| `prof` | 尚未实现 () |

| `profile` | 执行时间分析 (m|c) |

| `ptrace` | 跟踪子进程 (mc) |

| `quotact` | 尚未实现 () |

| `read` | 从文件读取数据 (m+c) |

| `readv` | 从文件读取数据块 |

| `readdir` | 读取目录 (m+c) |

| `readlink` | 获取符号链接的内容 (mc) |

| `reboot` | 重启或切换 vulcan 死亡握 (-mc) |

| `recv` | 从已连接的套接字接收消息 (m!c) |

| `recvfrom` | 从套接字接收消息 (m!c) |

| `rename` | 移动/重命名文件 (m+c) |

| `rmdir` | 删除空目录 (m+c) |

| `sbrk` | 查看 brk (mc!) |

| `select` | 睡眠直到描述符上有操作 (mc) |

| `semctl` | IPC 信号量控制 (m!c) |

| `semget` | 获取 IPC 信号量标识 (m!c) |

| `semop` | 对信号集成员进行 IPC 操作 (m!c) |

| `send` | 向已连接的套接字发送消息 (m!c) |

| `sendto` | 向套接字发送消息 (m!c) |

| `setdomainname` | 设置系统主机名 (mc) |

| `setfsgid` | 设置文件系统组 ID () |

| `setuid` | 设置文件系统用户 ID () |

| `setgid` | 设置实际组 ID (m+c) |

| `setgroups` | 设置附加组 (mc) |

| `stethid` | 设置唯一主机标识符 (mc) |

| `stethname` | 设置系统主机名 (m|c) |

| `setimer` | 设置定时器 (mc) |

| `setpgid` | 设置进程组 ID (m+c) |

| `setpriority` | 没影响 (mc) |

| `setpriority` | 设置进程/组/用户优先级 (mc) |

| `setrgid` | 设置实际组 ID (m+c) |

| `setuid` | 设置有效用户 ID (m+c) |

| `setrlimit` | 设置资源限制 (mc) |

| `setsid` | 创建会话 (+c) |

| `setsockopt` | 获取套接字选项设置 (mc) |

| `setimeofday` | 获取自 1.2.1970 以来的时区+秒数 (mc) |

| `setuid` | 设置实际 UID (m+c) |

| `setup` | 初始化信号 |

| `sgetmask` | 获取信号掩码 (m) |

| `shmat` | 附加共享内存段 (mc) |

| `shmctl` | 控制共享内存 (m|c) |

| `shmdt` | 分离共享内存段 (m|c) |

| `shmget` | 获取共享内存标识 (m|c) |

| `shutdown` | 关闭套接字 (m|c) |

| `sigaction` | 设置信号处理 (m+c) |

| `sigblock` | 阻塞信号 (m|c) |

| `sig_` | 产生未阻塞的信号 (mc) |

| `sigalarm` | 设置闹钟 (mc) |

| `sigpause` | 睡眠直到信号 (mc) |

| `sigprocmask` | 设置信号掩码 (m+c) |

| `sigreturn` | 信号返回 |

| `sigsuspend` | 挂起进程 (m|c) |

| `symlink` | 创建符号链接 (m+c) |

| `sync` | 同步内存和磁盘 (mc) |

| `socket` | 创建套接字 (m|c) |

| `socketpair` | 创建套接字对 (mc) |

| `sysinfo` | 获取信息 (m) |

| `stat` | 获取文件状态 (m+c) |

| `statfs` | 获取文件系统信息 (mc) |

| `stime` | 获取自 1.1.1970 以来的秒数 (mc) |

| `stty` | 设置终端设置 |

| `swapoff` | 停止交换 (m-c) |

| `swapon` | 开启交换 (m-c) |

| `symlink` | 创建符号链接 (m+c) |

| `sync` | 同步内存和磁盘 (mc) |

| `syscall` | 执行系统调用编号 (-) |

| `sysconf` | 获取系统变量值 (m+c) |

| `sysfs` | 获取配置 |

| `sysinfo` | 获取 Linux 信息 (m-) |

| `syslog` | 系统日志 (mc) |

| `system` | 执行 shell 命令 (m!c) |

| `time` | 获取自 1.1.1970 以来的秒数 (m+c) |

| `times` | 获取进程时间 (m+c) |

| `truncate` | 更改文件大小 (mc) |

| `ulimit` | 设置限制 (mc) |

| `umask` | 设置文件创建掩码 (m+c) |

| `umount` | 卸载文件系统 (m-c) |

| `uname` | 获取系统信息 (m+c) |

| `unlink` | 删除文件时忙用 (m+c) |

| `uselib` | 使用共享库 (m-c) |

| `ustat` | 尚未实现 |

| `utime` | 修改 inode 时间 (m+c) |

| `utimes` | 查看 utime (m!c) |

| `vfork` | 查看 fork (m!c) |

| `vhangup` | 虚拟挂起当前终端 (m-c) |

| `vm86` | 进入虚拟 806 模式 (m-c) |

| `wait` | 等待进程终止 (m+!c) |

| `wait3` | BSD 等待特定进程 (m!c) |

| `wait4` | BSD 等待特定进程 (mc) |

| `waitpid` | 等待特定进程 (m+c) |

| `write` | 向文件写入数据 (m+c) |

| `writev` | 向文件写入数据块 (m!c) |

(m) 存在手册页。

(+) POSIX 兼容。

(-) Linux 特有。

(c) 在 libc 中。

(!) 不是单一系统调用。使用了不同的系统调用。

Sven Goldt Linux 程序员指南

129

## 第 12 章

## 缩写

| `ANSI` | 美国国家信息标准 |
| `API` | 应用程序接口 |
| `ASCII` | 美国信息交换编码 |
| `AT 386` | 基于 Intel 80386 的先进 PC |
| `FIPS` | 联邦信息处理标准 |
| `FSF` | 自由软件基金 |
| `IEEE` | 电电子工程师学会 |
| `IPC` | 进程间通信 |
| `ISO` | 国际标准组织 |
| `POSIX` | UNIX 的可移植操作系统接口 |
| `POSIX.1` | IEEE Std. 1003.1-1990 信息技术可移植操作系统接口标准 (POSIX) - 第一部分：系统应用编程接口 (API) |

此内容包含关于源代码查找途径及官方首页的引用。

在满足逐字复制条件下，允许复制和分发本手册的修改版本，前提是整个结果作品必须按照与此相同的许可通知条款进行分发。

在上述修改版本的条件下，允许将本手册翻译成其他语言并进行复制和分发。作者对有关修改、翻译和印刷版本的通知将不胜感激。感谢。

# 目录

- 献辞
- 可用的源代码及预格式化版本
- 1. 引言
    - Linux 文档项目 (Linux Documentation Project)
- 2. Linux 系统概述
    - 操作系统的各个部分
    - 内核的重要部分
    - UNIX中的主要服务
    - `init`
    - 从终端登录
    - `Syslog`
    - 周期性命令执行：`cron` 和 `at`
    - 图形用户界面
    - 网络
    - 网络登录
    - 网络文件系统
    - 邮件
    - 打印
    - 文件系统布局
- 3. 目录树概述
    - 背景
    - 根文件系统
    - `/etc` 目录
    - `/dev` 目录
    - `/usr` 文件系统
    - `/var` 文件系统
    - `/proc` 文件系统
- 4. 使用磁盘和其他存储介质
    - 两种设备
    - 硬盘
    - 软磁盘
    - 刻光盘
    - 磁带
    - 格式化
    - 分区
- `MBR`、`启动扇`和分区表
- 扩展分区与逻辑分区
- 分区类型
- 硬盘分区
- 设备文件与分区
- 文件系统
- 什么是文件系统？
- 琳多的文件系统
- 应该使用哪种文件系统？
- 创建文件系统
- 挂载与卸载
- 使用 `fsck` 检查文件系统完整性
- 使用 `badblocks` 检查磁盘错误
- 解决碎片
- 适用于所有文件系统的其他工具
- 适用于 ext2 文件系统的其他工具
