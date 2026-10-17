
- `t_next` — 全局内核线程链表的前向指针。
- `t_prev` — 上述的反向指针。
- `t_cred` — 指向当前凭据结构的指针。
- `t_system` — 系统调用号

以下内核成员被分发器用于线程调度：
- `t_lockp` — 指向分发器锁的指针。
- `t_oldspl` — 上一个优先级级别。
- `t_pre_sys` — 系统调用预处理标志。
- `t_disp_queue` — 指向分发队列的指针。
- `t_disp_time` — 在分发的时间。
- `t_kem_req` — 需要的最大内存。
- `t_maxusers` — 最大用户数。

# 进程表

## 8.3.1 进程限制

启动时，内核初始化一个维护进程的进程表。最初为 `proc` 结构分配空间。表本身实现为双向链表，因此每个 `proc` 结构包含指向下一个和上一个进程的指针。进程表的最大大小基于物理内存 `RAM` 并在启动时确定。在启动期间，内核将可调参数 `maxusers` 设置为系统安装的兆字节数，最高为 2048。拥有超过 2 GB 物理内存的系统 `maxusers` 值为 2048。小于 2 GB 的系统将 `maxusers` 设置为兆字节数的内存；例如，拥有 512 MB RAM 的系统 `maxusers` 值为 512。`maxusers` 值随后决定了若干内核资源的数量，例如最大进程表和每个用户的最大进程数。

公式非常简单：

```
max_nprocs = (10 + 16 * maxusers)
maxuprc = (max_nprocs - 5)
```

`max_nprocs` 值是全局最大进程数，`maxuprc` 决定非 root 用户占据进程表槽的最大进程数。系统实际上使用一个持有通用系统配置信息的数据结构 `var` 结构来存储这些值。有三个相关值：
- `v_proc`，设置为等于 `max_nprocs`。
- `v_maxuptl`，系统上所有非 root 用户使用的进程槽最大数。它设置为 `max_nprocs` 减去某些预留的进程槽，目前 `reserved_proc` 为 5。
- `v_maxup`，非 root 用户可以占据的最大进程槽数。它设置为 `maxuprc` 值。

你可以使用 `adb(1)` 来检查运行中的系统中 `maxusers`、`max_nprocs` 和 `max_uprc` 的值。

```
# adb -k /dev/ksys /dev/mem
phyzym bdde
maxusers/D
maxusers:
maxusers:
max_nprocs/D      189
max_nprocs:
max_nprocs:       3034
maxuprc/D
maxuprc:
maxuprc:           3029
```

你也可以使用 `crash(1)` 或系统变量结构来转储这些值。

```
# /etc/crash
> od -d maxusers
f0274dc4: 0000000253
> od -d max_nprocs
f0271e6c: 0000004058
> od -d maxuprc
f0270f28: 0000004053
> var
v_buf: 100
v_call: 0
v_proc: 4058
v_nglobpris: 110
v_maxysyspr: 99
v_clist: 0
v_maxuprc: 4053
v_hbub: 256
v_hmark: 255
v_pbuf: 0
v_sptmap: 0
v_maxmem: 0
v_autup: 30
v_bufwhm: 5196
```

注意，`/etc/crash var` 工具并没有转储 `v_maxuptl`；它只转储了 `v_proc` 和 `v_maxup`。变量虚拟地址左侧的十六进制值例如，`f0274dc4` 是在本例中 `maxusers` 内核变量的地址。

最后，带有 `-v` 标志的 `sar(1M)` 可以提供系统的最大进程表大小以及当前的进程数。

```
$ sar -v 1 1
SunOS sunsys 5.6 Generic sun4m      05/05/00
22:27:47 proc-sz ov inod-sz ov file-sz ov lock-sz
22:27:48 63/3034 0 2480/13212 0 392/392 0 0/0
```

# 进程创建

在 `proc-sz` 列下，`72/1962` 值代表当前进程数 `72` 和最大进程数 `1962`。

如果 `max_nprocs` 在 `/etc/system` 中被设置了超出范围的值，即使对于大型系统也是如此，内核会强制执行最大值。在 Solaris 版本 2.4、2.5、2.5.1、2.6 和 7 中，最大值为 30,000，这由 `param.h` 头文件中的 `MAXPID` 宏决定，该文件位于 `/usr/include/sys`。

在 `fork` 代码中，会根据 `v_proc` 进程变量检查当前进程数。如果达到限制，系统会在控制台上输出“out of processes”，并增加 `sar(IM)` 输出中 `proc-sz` 右侧维护的进程表溢出计数。对于非 root 用户，会检查 `v_maxuser` 参数，并记录“out of per users for uid (UID)”消息。在这两种情况下，调用程序都会从 `fork(2)` 获得 `-1` 值，表示错误。

## 8.3.2 LWP 限制

现在我们检查了内核对全局进程数量施加的限制，让我们来看系统中任何时候存在的 LWP/kthread 对的限制。

每个 LWP 都有一个内核栈，从 `segkp` 内核地址段中分配。内核 `segkp` 段的大小和 LWP 内核栈的分配取决于内核发布版本和硬件平台。对于运行 32 位内核的基于 UltraSPARC `sun4u` 的系统，`segkp` 大小被限制为 512 Megabytes，内核栈为 16 Kilobytes。因此，全局最大 LWP 数量为 32,768 `32K` 基于 512 MB 的 `segkp` 大小和 16 KB 的栈大小。在 64 位 Solaris 7 上，较大的 24 字节 LWP 内核栈分配将基于 UltraSPARC 的系统的 LWP 总数减少到 21,845。在基于 UltraSPARC 的系统上，栈分配略小——12 Kilobytes。内核 `segkp` 段也较小；总大小基于硬件架构和物理内存量。

## 8.4 进程创建

Solaris 中的所有进程都是使用传统的 `fork/exec` 进程模型创建的，该模型是原始 Unix 设计的一部分，并在几乎每个 Unix 版本中都有实现。Solaris 环境中的例外是启动时创建的四个守护进程，PID 0 到 3：调度器 `sched` PID 0、init PID 1、pageout PID 2 和 fsflush PID 3。这些进程是由内核内部的 `newproc()` 函数创建的。进程创建的机制如图 8.12 “Solaris 多线程进程架构”所示。

`fork(2)` 和 `exec(2)` 系统调用广泛用于随 Solaris 附的各种软件组件以及运行在 Solaris 上的数百个应用程序。然而，随着每个版本的发布，更多的 Solaris 守护进程和应用程序采用了线程化，这意味着程序使用线程作为多进程的替代。

`fork(2)` 系统调用创建一个新进程。新创建的进程分配有一个唯一标识 `PID` 并是该进程的子进程；调用进程是父进程。`exec(2)` 系统调用用执行文件覆盖进程。`fork(2)` 系统调用创建一个新进程。在执行文件覆盖进程时，`exec(2)` 模型如下伪代码所示：

```
main(int argc, char *argv[], char *envp[])
{
  pid_t child_pid;
  child_pid = fork();
  if (child_pid == -1)
    perror(fork); /* fork 失败 */
  else if (child_pid == 0)
    execv(path,argv); /* 子进程中执行 exec */
  else
    wait(); /* pid > 0，在父进程中等待 */
}
```

上述伪代码中的 `fork(2)` 检查 `fork(2)` 的返回值。一旦 `fork` 成功执行，它向子进程返回 0，向父进程返回子进程的 PID。`exec(2)` 系统调用在随 Solaris 附的各种软件组件以及运行在 Solaris 上的数百个应用程序中广泛广泛。然而，随着每个版本的发布，更多的 Solaris 守护进程和应用程序采用了线程化，这意味着程序使用线程作为多进程的替代。

`fork(2)` 系统调用创建一个新进程。新创建的进程分配有一个唯一标识 `PID` 并是该进程的子进程；调用进程是父进程。`exec(2)` 系统调用用执行文件覆盖进程。
