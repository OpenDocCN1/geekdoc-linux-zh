
Solaris 中的所有进程都是使用传统的 `fork/exec` 进程模型创建的，该模型是原始 Unix 设计的一部分，并在几乎每个 Unix 版本中都有实现。

在 `fork` 代码中，会根据 `v_proc` 进程变量检查当前进程数。如果达到限制，系统会在控制台上输出“out of processes”，并增加 `sar(IM)` 输出中 `proc-sz` 右侧维护的进程表溢出计数。对于非 root 用户，会检查 `v_maxuser` 参数，并记录“out of per users for uid (UID)”消息。在这两种情况下，调用程序都会从 `fork(2)` 获得 `-1` 值，表示错误。

# 8.3.2 LWP 限制

现在我们检查了内核对全局进程数量施加的限制，让我们来看系统中任何时候存在的 LWP/kthread 对的限制。

每个 LWP 都有一个内核栈，从 `segkp` 内核地址段中分配。内核 `segkp` 段的大小和 LWP 内核栈的分配取决于内核发布版本和硬件平台。对于运行 32 位内核的基于 UltraSPARC (sun4u) 的系统，`segkp` 大小被限制为 512 Megabytes，内核栈为 16 Kilobytes。因此，全局最大 LWP 数量为 32,768 (32K)（基于 512 MB 的 `segkp` 大小和 16 KB 的栈大小）。在 64 位 Solaris 7 上，较大的（24 字节）LWP 内核栈分配将基于 UltraSPARC 的系统的 LWP 总数减少到 21,845。在基于 UltraSPARC 的系统上，栈分配略小——12 Kilobytes。内核 `segkp` 段也较小；总大小基于硬件架构和物理内存量。

# 8.4 进程创建

Solaris 中的所有进程都是使用传统的 `fork/exec` 进程模型创建的，该模型是原始 Unix 设计的一部分，并在几乎每个 Unix 版本中都有实现。

Solaris 环境中的例外是启动时创建的四个守护进程，PID 0 到 3：调度器 (`sched`, PID 0)、`init` (PID 1)、`pageout` (PID 2) 和 `fsflush` (PID 3)。这些进程是由内核内部的 `newproc()` 函数创建的。进程创建的机制如图 8.12 “Solaris 多线程进程架构”所示。

`fork(2)` 和 `exec(2)` 系统调用广泛用于随 Solaris 附的各种软件组件以及运行在 Solaris 上的数百个应用程序。（然而，随着每个版本的发布，更多的 Solaris 守护进程和应用程序采用了线程化，这意味着程序使用线程作为多进程的替代。）

`fork(2)` 系统调用创建一个新进程。新创建的进程分配有一个唯一标识 (PID) 并是该进程的子进程；调用进程是父进程。`exec(2)` 系统调用用执行文件覆盖进程。

在 `fork` 代码中，会根据 `v_proc` 进程变量检查当前进程数。如果达到限制，系统会在控制台上输出“out of processes”，并增加 `sar(IM)` 输出中 `proc-sz` 右侧维护的进程表溢出计数。对于非 root 用户，会检查 `v_maxuser` 参数，并记录“out of per users for uid (UID)”消息。在这两种情况下，调用程序都会从 `fork(2)` 获得 `-1` 值，表示错误。

你可以使用 `adb(1)` 来检查运行中的系统中 `maxusers`、`max_nprocs` 和 `max_uprc` 的值。也可以使用 `crash(1)` 或系统变量结构来转储这些值。

## Solaris 多线程进程架构

```
fork() or fork() or vfork()
cfork()
```

- 获取进程结构（通过 `kmem_cache_alloc(process_cache)`）。

- 将进程状态 (`p_stat`) 设置为 `SIDL`。

- 设置进程启动时间 (`p_mstart`)。

- 调用 `pid_assign()` 获取 PID。

- 获取 PID 结构。

- 获取一个 `/proc` 目录槽位。

- 获取一个可用的 PID。

- 初始化 PID 结构。

- 设置引用计数。

- 设置 proc 槽号。

- 将 PID 返回给 `getproc()`。

- 检查表是否溢出（`procs > v_nprocs`）。

- 检查是否达到每个用户的进程限制。

- 将新进程放入链表。

- 从父进程设置新进程和信号（signal）。

- 从父进程在新的（子）进程中设置以下字段：

  - 会话句指针 `p_ssess`

  - 可执行文件指针 `void p_exec`。

  - 地址空间字段 `p_brkbase`, `p_brksize`, `p_stksize`。

  - 设置子 PID。

  - 设置父子链接指针。

- 从子进程拷贝配置状态 `p_prof`。

- 增加打开文件列表中的引用计数。

- 将父进程的 `uarea` 拷贝到子进程（包括打开的文件列表）。

- 如果子进程继承跟踪标志（`p_flag` 中设置了 `PFWP`）

  - 从子进程父进程设置 `p_sigmask`。

  - 从父进程设置 `p_sigmask`。

- 否则

  - 清空子进程中的 `p_sigmask` 和 `p_itmask`（为空）。

- 如果（父进程中继承主计数标志）

  - 启用父进程中的主计数标志

  - 从 `getproc()` 返回到 `cfork()`。

- 如果 (`vfork()`)

  - 将地址空间设置为父进程（子进程 `p_as = parent_as`）。

  - 在 `p_flag` 中设置子进程 `SVFORORK`。

- 否则（不是 vfork()）

  - 为子进程复制父进程地址空间的副本（`as_dup()`）。

  - 为子进程复制父进程的共享内存。

  - 复制 LWP 和线程。

  - 如果 (`fork()`)

    - 仅复制当前线程。

    - `forkwp()`

    - `lwp_create()`

  - 否则（遍历线程列表 - `p_tlist`；对于每个线程）

    - `forkwp()`

    - `lwp_create()` - 创建一个 LWP

    - 复制父进程的调度类

    - `thread_create()` - 创建一个内核线程

  - 将子进程加入父进程的进程组（`join()`）

- 将进程状态 (`p_stat`) 设置为 `SRUN`

- 如果 (`vfork()`)

  - 增加 `cpu_sysinfo` 中的 vfork 计数（`cpu_sysinfo.sysfork`）

  - 在子进程执行前调用 `continualwps()`

- 否则

  - 增加 `cpu_sysinfo` 中的 fork 计数（`cpu_sysinfo.sysfork`，注：原文此处为 sysfork 疑似笔误）

  - 将子进程放在调度队列中父进程之前（以便其先运行）。

- 返回值：给父进程返回 PID，给子进程返回 0

### 进程创建

如上述伪代码流程所示，当进入 `fork(2)` 系统调用时，在内核内存中会分配一个进程表槽位：`process_cache`，它首次在 Solaris 2.6 中实现。（在更早的 Solaris 版本中，内核仅为进程结构获取一段内核内存。）启动时间字段（`p_mstart`）被设置，且进程状态被设置为 `SIDL`，这是一个表示进程正处于中间“创建”状态的状态标志。内核为该进程分配一个 PID，并在 `/proc` 目录中为 `procfs` 条目分配一个可用槽位。内核从会话结构（session structure）将进程数据拷贝到子进程；此过程维护了会话首进程进程和控制终端信息。内核还于父进程和子进程之间建立了进程结构指针链接，并将父进程的区域拷贝到新创建的子进程结构中。

在进程 fork 失去控并消耗大量系统资源的情况下，Solaris 内核在这里实现了一个有趣的技巧。内核获取新 PID 的 `pid_assign()` 代码失败，或者没有可用的进程表槽位，均表明存在大量的进程活动。在这种情况下，内核实现了一种延迟机制，强制进程额外睡眠一个时钟周期（tick，每 10 毫秒一个刻度）。通过实现这种机制，内核确保了每个 CPU 时钟周期内最多允许一次 fork 失败。

这种节流（throttle）还会进行扩展，使得 fork 失败率的增加会导致代码返回以及调用进程尝试重试之前的延迟增加。在那种情况下，你将看到控制台消息“out of processes”，并且 `sar -v` 输出中的 `ov`（over）列将具有非零值。你也可以用 `adb` 查看内核变量 `fork_fail_pending`。如果该值不为零，说明系统存在 fork 节流代码段。以下是使用 `adb(1)` 查看 `fork_fail_pending` 内核变量的示例。
