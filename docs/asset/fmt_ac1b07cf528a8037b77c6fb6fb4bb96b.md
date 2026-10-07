
# 共享文件系统相关信息：`CLONE_FS`

如果指定了 `CLONE_FS` 标志，父进程和子进程共享文件系统相关信息——`umask`、根目录和当前工作目录。这意味着在任何一个进程中调用 `umask()`、`chdir()` 或 `chroot()` 都会影响另一个进程。如果未设置 `CLONE_FS` 标志，父进程和子进程拥有这些信息的独立拷贝（与 `fork()` 和 `vfork()` 一样）。

`CLONE_FS` 共享的属性是 POSIX 线程要求的。

# 共享信号处理方式：`CLONE_SIGHAND`

如果设置了 `CLONE_SIGHAND` 标志，父进程和子进程共享相同的信号处理表。在任何一个进程中使用 `sigaction()` 或 `signal()` 更改信号的处理方式将影响另一个进程中该信号的处理方式。如果未设置 `CLONE_SIGHAND` 标志，信号处理方式将不共享；相反，子进程将获得父进程信号表的拷贝（与 `fork()` 和 `vfork()` 一样）。`CLONE_SIGHAND` 标志不影响进程掩码和等待信号集，这些者对于两个进程始终是不同的。从 Linux 2.6 开始，如果指定了 `CLONE_SIGHAND`，则 `flags` 中必须也包含 `CLONE_VM`。

POSIX 线程要求共享信号处理方式。

# 共享父进程虚拟内存：`CLONE_VM`

如果设置了 `CLONE_VM` 标志，父进程和子进程共享相同的虚拟内存页（与 `fork()` 一样）。任何进程对 `mmap()` 或 `munmap()` 的更新或调用对另一个进程可见。如果未设置 `CLONE_VM` 标志，子进程接收父进程虚拟内存的拷贝（与 `fork()` 一样）。

共享相同的虚拟内存是线程的定义属性之一，也是 POSIX 线程要求的。

# 线程组：`CLONE_THREAD`

如果设置了 `CLONE_THREAD` 标志，子进程会被放在与父相同的相同线程组中。线程组在 Linux 2.4 中引入，允许线程库支持 POSIX 线程模型，即进程中的所有线程共享同一个进程 ID（即每个线程中的 `getpid()` 应该返回相同的值）。线程组是一组共享相同线程标识（TID）的 KSE，如图 28-1 所示。在后续关于 `CLONE_THREAD` 的讨论中，我们将这些 KSE 称为*线程*。

自 Linux 2.4 以来，`getpid()` 返回调用线程的 TID。换句话说，TID 与进程 ID 相同。

Linux 2.2 及早版本的实现没有提供 `CLONE_THREAD`。线程将 POSIX 线程实现为进程，这些进程共享各种属性（例如虚拟内存），但具有不同的进程 ID。在现代内核上，出于兼容性考虑，LinuxThreads 实现不使用 `CLONE_THREAD` 标志，因此该实现中的线程继续保持具有不同的进程 ID。

# PID 为 201 的进程

| 线程 A | 线程 B | 线程 C | 线程 D |
|---|---|---|---|
| PPID=1900 | PPID=1900 | PPID=1900 | PPID=1900 |
| TGID=2001 | TGID=2001 | TGID=2001 | TGID=2001 |
| TID=2001 | TID=2002 | TID=2003 | TID=2004 |

线程组组（TID 匹配 TGID）

**图 28-1:** 包含四个线程的线程组

线程组内的每个线程都通过唯一的线程标识（TID）来区分。Linux 2.4 引入了一个新的系统调用 `gettid()`，允许线程获取get自己的线程 ID（这与调用 `clone()` 的线程返回的值相同）。线程 ID 使用与进程 ID 相同的数据类型 `pid_t` 表示。线程 ID 是系统唯一的，内核保证没有任何线程 ID 会与系统上的任何进程 ID 相同，除非该线程是该进程的线程组组。

新线程组中的第一个线程的线程 ID 与其组 ID 相同。该线程被称为*线程组*。

我们在这里讨论的 ID 与 POSIX 线程所使用的线程 ID（`pthread_t` 数据类型）不同。后者标识符是由 POSIX 线程实现在内部（用户空间）生成并维护的。

线程组中的所有线程具有相同的进程 ID——即组组的进程 ID。只有当线程组中的所有线程都终止后，才会向父进程发送 `SIGCHLD` 信号（或其他信号）。这些语义对应 POSIX 线程的要求。

在使用 `clone()` 时，无法通过 `wait()`（或类似操作）来等待使用 `CLONE_THREAD` 创建的线程。这符合 POSIX 要求。POSIX 线程并不是进程，不能通过 `wait()` 等待；相反，它必须使用 `pthread_join()` 进行连接。为了检测使用 `CLONE_THREAD` 创建的线程的终止，使用了一种名为 `futex` 的特殊同步原语（参见 `futex` 章节）。

（注：原文此处存在大量重复段落，译文已按逻辑去重处理）

# 线程库支持：`CLONE_PARENT_SETID`, `CLONE_CHILD_SETID` 和 `CLONE_CLEARTID`

`CLONE_PARENT_SETID`、`CLONE_CHILD_SETID` 和 `CLONE_CLEARTID` 标志在 Linux 2.6 中引入，用于支持 POSIX 线程。

`CLONE_PARENT_SETID` 标志导致该位置在 `clone()` 返回之前初始化为线程 ID。这意味着如果指定了 `CLONE_VM` 标志，父进程和子进程都能看到该线程 ID。

如果设置了 `CLONE_CHILD_SETID` 标志，则 `clone()` 将子进程的线程 ID 写入指向 `ctid` 位置。`ctid` 的设置仅在子进程内存中进行，但如果也指定了 `CLONE_VM` 标志，这将影响父进程。虽然 NPTL 不需要 `CLONE_CHILD_SETID`，但提供此标志是为了为线程库实现提供灵活性。

如果设置了 `CLONE_CLEARTID` 标志，则当子进程终止时，`clone()` 将指向 `tid` 的内存位置零。

`tid` 参数是 NPTL 线程实现（后文）获取线程终止通知的机制。这种通知是 `pthread_join()` 函数要求的，该函数是 POSIX 线程中允许一个线程等待另一个线程终止的机制。

当使用 `pthread_create()` 创建线程时，NPTL 调用 `clone()`，其中 `pid` 和 `ctid` 指向同一个位置。（这就是为什么 NPTL 不需要 `CLONE_CHILD_SETID`。）

带有新的线程 ID。当子进程终止且 `cid` 清空时，更改对进程中的所有线程都是可见的（因为也指定了 `CLONE_VM` 标志）。

内核将 `cid` 指向的位置视为 `futex`，一种高效的同步机制。（有关 `futex` 的更多细节请参见 `futex(2)` 手册）。可以通过执行 `futex(1)` 系统调用来获取线程终止的通知，该调用会阻塞等待 `cid` 指向位置的值发生变化。（在底层，这就是 `pthread_join()` 所做的工作）。在内核清除 `cid` 的同时，它还会唤醒任何因在该地址上执行 `futex wait` 而阻塞的调度实体（即线程）（在 POSIX 线程层面，这会导致 `pthread_join()` 调用解除阻塞。）

## 线程本地存储：`CLONE_SETLS`

如果设置了 `CLONE_SETLS` 标志，则 `tls` 参数将指向一个 `user_desc` 结构，该结构体描述了线程本地存储缓冲区。该标志在 Linux 2.6 中引入，用于支持 NPTL 的线程本地存储实现（第 31.4 节）。有关 `user_desc` 结构的细节，请参见 2.6 内核源码中该结构的定义和用法以及 `set_thread_area(2)` 手页。

## System V 命名空间值：`CLONE_SYSVEM`

如果设置了 `CLONE_SYSVEM` 标志，父进程和子进程共享同一个 System V 命名空间值列表（第 47.8 节）。如果未设置此标志，父进程和子进程将拥有独立的列表，且子进程列表初始为空。

`CLONE_SYSVEM` 标志从内核 2.6 版本开始可用，并提供了 POSIX 线程所需的共享语义。

## 进程挂载命名空间：`CLONE_NEWNS`

从内核 2.4.19 版本开始，Linux 支持进程挂载命名空间（mount namespaces）的概念。挂载命名空间是由 `mount()` 和 `umount()` 调用维护的挂载点集。它决定了路径如何解析为实际文件，以及 `chdir()` 和 `chroot()` 等系统调的操作。

默认情况下，父进程和子进程共享一个挂载命名空间，这意味着一个进程通过 `mount()` 和 `unmount()` 对命名空间进行的更改在另一个进程中是的（类似于 `fork()` 和 `vfork()`）。特权进程（`CAP_SYS_ADMIN`）可以指定 `CLONE_NEWNS` 标志，以便子进程获得父进程挂载命名空间的副本。此后，一个进程对命名空间的更改在另一个进程中不可见（在较早的 2.4.x 内核中，以及旧内核中，我们可以认为系统上的所有进程都共享同一个系统级挂载命名空间。）

进程挂载命名空间可用于创建类似于 `chroot()` 的环境，这种环境更安全且更灵活：例如，可以为被禁的进程提供一个系统上其他进程不可见的挂载点。挂载命名空间在搭建虚拟服务器环境也有用。

在 `clone()` 中同时指定 `CLONE_NEWNS` 和 `CLONE_FS` 是没有意义的且不允许的。

## 使子进程与调用者进程相同：`CLONE_PARENT`

默认情况下，我们使用 `clone()` 创建新进程，该进程的父进程（通过 `getppid` 返回）是调用 `clone()` 的进程（类似于 `fork()` 和 `vfork()`）。如果设置了 `CLONE_PARENT` 标志，子进程的父进程将是调用者的父进程。换句话说，`CLONE_PARENT` 等于设置 `child.PPID`。在默认情况下（没有 `CLONE_PARENT`），将是 `child.PPID = caller.PID`。父进程（`child.PPID`）是子进程终止时接收信号的进程。

`CLONE_PARENT` 标志在 Linux 2.4 及更高版本可用。最初，它设计用于对 POSIX 线程实现有用，尽管 2.6 内核采用的线程方法（使用上述的 `clone()`）消除了对该标志的需求。

## 使子进程 PID 与父进程 PID 相同：`CLONE_PID`（已弃）

如果设置了 `CLONE_PID` 标志，子进程与父进程具有相同的进程 ID。如果未设置此标志，父进程和子进程具有不同的进程 ID（类似于 `fork()` 和 `vfork()`）。只有系统进程（进程 ID 0）可以指定此标志；它用于初始化多进程系统。

`CLONE_PID` 标志并非用于用户应用程序。在 Linux 2.6 中，它已被移除，并被 `CLONE_LETASK` 取代，后者会将新进程的 PID 设置为 0。`CLONE_LETASK` 仅可供内核内部使用（在 `clone()` 的 `flags` 参数中指定时它会被忽略）。它用于创建每个 CPU 的空闲进程，多进程系统中可能存在多个实例。

## 进程跟踪：`CLONE_PTRACE` 和 `CLONE_UNTRACED`

如果设置了 `CLONE_PTRACE` 标志且调用进程正在被跟踪，则子进程也会被跟踪。有关进程跟踪（供调试器和 *str* 命令使用）的细节，请参见 `ptrace(2)` 手页。

从内核 2.6 版本开始，可以设置 `CLONE_UNTRACED` 标志，这意味着跟踪无法强制对该子进程开启 `CLONE_PTRACE`。`CLONE_UNTRACED` 标志由内核在创建内核线程时内部使用。

## 子进程退出或唤醒时挂起父进程：`CLONE_VFORK`

如果设置了 `CLONE_VFORK` 标志，当子进程退出或唤醒时，父进程的执行将被挂起。

## 支持容器的新标志

Linux 2.6 添加了许多新标志以支持容器：

- `CLONE_IPC`
- `CLONE_NEWUSER`
- `CLONE_NEWPID`
- `CLONE_NEWUTS`

为了实现容器，内核开发者必须对这些资源（如进程 ID、网络栈、用户和组命名空间）提供中间层，以便每个容器提供自己的实例。容器有多种用途，包括：

- 控制系统资源，例如带宽和 CPU 时间（例如，一个容器获得 75% 的 CPU 时间，而另一个获得 25%）；
- 在主机上提供多个轻量级虚拟服务器；
- 冻结容器，以便在迁移到不同机器后重启；
- 允许应用程序的状态被转储（检查点）并在之后恢复。

## `waitpid()` 标志的使用

大致我们可以说 `fork()` 对应于带有 SIGCHLD 标志的 `clone()`，其中 `fork()` 对应于调用标志如下 `clone()`：

```
CLONE_VM | CLONE_FORK | SIGCHLD
```

从 2.3.3 版本开始，作为 NPTL 实现一部分的全局 `fork()` 绕过了内核调用并执行 `clone()`。此函数会调用调用者使用 `thread_atfork()` 建立的任何 处理器（参见第 33.3 节）。

Linux 线程实现使用 `clone()`（仅前两个参数）创建线程，指定的标志如下：

```
CLONE_VM | CLONE_FILES | CLONE_FS | CLONE_SIGHAND
```

NPTL 线程实现使用 `clone()`（所有七个参数）创建线程，指定的标志如下：

```
CLONE_VM | CLONE_FILES | CLONE_FS | CLONE_SIGHSAND | CLONE_THREAD | CLONE_SETTLDS | CLONE_PARENT_SETTID | CLONE_CHILD_CLEARTID | CLONE_SYSVSEM
```

## 28.2.2 `waitpid()` 的扩展

为了等待 `clone()` 生成的孩子，可以在 `waitpid()`、`wait3()` 和 `wait4()` 的选项位掩码参数包含以下附加值：

```
__WCLONE
```
