
## 章节：进程
187

| COMMAND PID USER FD TYPE DEVICE SIZE/OFF NODE NAME |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| d | 4905 | nobody | txt | VREG | 102,0 | 17388 100789 | /dev/dsk/c0d0s0 |
| d | 4905 | nobody | txt | VREG | 102,0 | 954804 101535 | /dev/dsk/c0d0s0 |
| d | 4905 | nobody | txt | VREG | 102,0 | 95380 10153 | /dev/dsk/c0d0s0 |
| d | 4905 | nobody | txt | VREG | 102,0 | 33360  0153 | /dev/dsk/c0d0s0 |

215

# 太阳 Solaris 9.0 系统和网络管理员全能考试指南

| Signal | Code | Description |
| :--- | :--- | :--- |
| SIGHUP | 1 | Hang up |
| SIGINT | 2 | Interrupt |
| SIGQUIT | 3 | Quit |
| SIGILL | 4 | Illegal instruction |
| SIGTRAP | 5 | Trace |
| SIGABRT | 6 | Abort |
| SIGEMT | 7 | Emulation trap |
| SIGFPE | 8 | Arithmetic exception |
| SIGKILL | 9 | Killed |
| SIGBUS | 10 | Bus error |
| SIGSEGV | 11 | Segmentation fault |
| SIGSYS | 12 | Bad system call |
| SIGPIPE | 13 | Broken pipe |
| SIGALRM | 14 | Alarm clock |
| SIGTERM | 15 | Terminate |

`pgrep` 命令用于搜索名称与命令行模式匹配的进程列表。该命令返回 PID 列表。此列表可以管道到另一个命令（如 `kill`），以对进程执行某些操作。
例如，要杀死所有与“java”相关的进程，命令如下：

```bash
$ kill -9 `pgrep java`
```

`pkill` 命令用于向具有相同名称的进程发送信号。它是更特定的版本，因为它只能用于发送信号，且 PID 列表无法管道到另一个程序。
要杀死所有与“java”相关的进程，命令如下：

```bash
$ kill -9 java
```

`killall` 命令用于杀死系统上运行的所有进程。它在系统进入运行级别 0 时由 `shutdown` 调用。然而，由于可以将信号传递给 `killall`，超级用户可以向所有进程发送不同的信号（非 15）。例如，向所有进程发送 SIGHUP 信号，可以使用以下命令：

```bash
# killall 1
```

## 总结

在本章中，我们检查了如何管理和监控进程。由于进程和线程是实际执行应用程序的实体，管理员了解如何发送信号来管理它们的活动是非常重要的。

## 问题

- 1. 下列哪种说法是正确的？
  A. Shell 可以启动另一个 shell 或应用程序。
  B. Shell 可以启动另一个 shell，但不能启动应用程序。
  C. Shell 不能启动另一个 shell，但可以启动应用程序。
  D. Shell 永远无法启动另一个 shell 或应用程序。
- 2. 什么是进程 ID (PID)？
  A. 与执行的应用程序名称对应的字符串
  B. 一个用于区分不同进程的、随机生成的字符串
  C. 一个与进程所分配的优先级相关的类
  D. 一个用于区分不同进程的、按顺序分配的整型
- 3. 一个可以更改其有效所有权的进程被称为？
  A. setGID 进程
  B. 魔数（magic number）进程
  C. setUID 进程
  D. 拥有魔数的进程
- 4. 系统上所有进程的根父 PID 是什么？
  A. a
  B. 1
  C. 0
  D. init
- 5. 缩写 PPID 代表什么？
  A. Processor PID（处理器 PID）
  B. Priority PID（优先级 PID）
  C. Personal PID（个人 PID）
  D. Parent PID（父 PID）
- 6. 缩写 STIME 代表什么？
  A. Process starting time（进程启动时间）
  B. Standard process execution time（标准进程执行时间）
  C. Single process execution time（单进程执行时间）
  D. Time zone environment variable（时区环境变量）
- 7. 睡眠进程内存地址的缩写是什么？
  A. SLPADDR
  B. ADDR
  C. WCHAN
  D. CHANADDR
- 8. 使用什么命令序列挂挂进程？
  A. CTRL-C
  B. ESC-C
  C. CTRL-Z
  D. ESC-Z
- 9. 如何使用 kill 命令向 pid 2192 发送 SIGHUP？
  A. kill -1 2192
  B. kill -2 2192
  C. kill -3 2192
  D. kill -9 2192
- 10. 如何使用 kill 命令向 pid 2192 发送 SIGKILL？
  A. kill -1 2192
  B. kill -2 2192
  C. kill -3 2192
  D. kill -9 2192

## 答案

1. A. Shell 可以启动任何类型的应用程序或另一个 shell。
2. D. 一个按顺序分配的、用于区分不同进程的整型。当分配最大 PID 时，新的 PID 将从 1 开始重新分配。然而，与运行进程相关的 PID 永远不会重复。
3. C. 有效所有权的更改始终与 setUID 相关。
4. B. 所有进程从 1 开始并递增。
5. D. 启动子进程的进程被称为父进程。
6. A. STIME 代表进程启动时间。
7. C. WCHAN 是该缩写。
8. C 按住键盘上的 CTRL 并按下 z。
9. A. SIGHUP 由 1 表示。
10. D. SIGKILL 由 9 表示。

# 文件系统简介

在本章中，你将：
- 学习 Solaris 文件系统的结构
- 学习创建新的文件系统
- 学习监控磁盘空间使用情况
- 如何使用 fck 修复文件系统

文件系统是 Solaris 采用的主要数据持久化机制。通常，文件系统构建在硬盘切片（或分区）上，以存储系统和用户数据。在本章中，将检查 Solaris 文件系统的布局，并提供创建和修复文件系统的指令。

# 文件系统结构

Solaris 文件系统通常是 UFS（UNIX 文件系统）类型，尽管可以在 `/etc/default/fs` 中定义其他系统类型。UFS 文件系统存在于 Solaris 上同时具有原始设备（raw）和块设备接口的硬盘上，如 `/dev/dsk` 和 `/dev/rdsk` 目录所示。Solaris 文件系统上的每个分区在 `/dev/dsk` 和 `/dev/rdsk` 中都有自己的条目。一个 UFS 文件系统包含以下元素：
- 启动块（boot block），如果文件系统启动，则它包含启动数据
- 超级块（superblock），包含 inode 的位置、文件系统大小、块数和状态
- Inodes，存储文件系统上文件的详细信息
- 数据块（data blocks），实际存储文件的地方

为了创建一个新的 UFS 文件系统，需要将磁盘分区成不同的切片。这些切片随后可以使用 `mkfs` 或 `newfs` 命令用于创建新的文件系统。对于在分区 c0t0d0s 上创建新文件系统而言，以下两个命令是等效的：

```bash
# newfs /dev/rdsk/c0t0d0s
# mkfs -F /dev/rdsk/c0t0d0s
```
