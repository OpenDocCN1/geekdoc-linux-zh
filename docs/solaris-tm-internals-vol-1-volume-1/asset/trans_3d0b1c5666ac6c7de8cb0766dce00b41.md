
下面的伪代码概括了 `exitlwps()` 函数。

```text
exitlwps()
    if (process LWP count == 1)
        nuke SIGWAITING
        return
    else
        for (each LWP/kthread on the process linked list)
            if (LWP/kthread is sleeping or stopped)
                make it runnable
            if (LWP/kthread is running on a processor)
                t_astflag = 1
                poke_cpu() /* cross-call, to trap into the kernel */
                    holdlwp()
                        lwp_exit()
                            place kthread/LWP on zombie list
                done (loop)
        replace zombie threads on deathrow
        return to kernel exit()
```

一旦 `exit()` 代码完成，进程就处于僵尸状态，仅占用一个进程表项和 PID 结构。当对僵尸进程发出 `wait()` 调用时，内核会调用 `freeproc()` 函数来释放进程和 PID 结构。

### 8.5.2 死亡名单（Deathrow）

`exitlwps()` 在返回 `exit()` 之前还要做最后一点工作：它将僵尸的内核线程放到*死亡名单*上。

内核维护一个称为死亡名单（deathrow）的列表，其中包含已退出的 LWP 和内核线程，目的是在需要创建新的 LWP/kthread（`fork()`）时回收已终止的 LWP/kthread。如果僵尸列表上有可用的 LWP/kthread，内核就不需要为新 kthread 分配数据结构和栈；它只需使用僵尸 kthread 的结构和栈，并将该 kthread 链接到发出 `fork(2)` 或 `thread_create()` 的进程。

在进程创建流程中，当 `forklwp()` 代码调用 `lwp_create()` 时，`lwp_create()` 首先在死亡名单上查找僵尸线程。如果存在，LWP、kthread 和栈会被链接到进程，内核在 `fork()` 过程中就无需分配新的 kthread、LWP 和栈空间。内核只需从死亡名单列表中获取这些结构，适当地链接指针，然后继续执行。`thread_create()`（内核线程创建，而非用户线程 API）由 `lwp_create()` 调用，传入 LWP 数据和栈，因此避免了任何内核内存分配。

内核线程 `thread_reaper()` 定期运行，清理死亡名单上的僵尸线程。死亡名单上的僵尸线程列表不允许无限制增长（最多 32 个僵尸），并且僵尸不会在死亡名单上停留太久。

## 8.6 Procfs — 进程文件系统

进程文件系统 procfs 是一种伪文件系统。伪文件系统为传统意义上并非文件的对象提供类文件抽象和文件 I/O 接口。Procfs 抽象了 Solaris 内核的进程架构，使得系统上运行的所有进程都出现在 /proc 目录下的根目录命名空间中；系统中的每个进程都以文件形式存在于 /proc 下，进程的 PID 作为文件名。/proc 下的 PID 文件名实际上是一个目录，其中包含其他文件和子目录，这些共同构成了完整的 /proc 目录空间。许多提供进程数据和控制点的内核数据结构以文件形式出现在 /proc/<PID> 目录层次结构中，多线程进程中的每个 LWP 都有一个子目录。每个 LWP 的数据和控制结构以文件形式存在于 /proc/<PID>/lwp/<LWP_ID> 下。/proc 下出现的对象不是磁盘上的文件；它们是存在于内核内存中的对象。当用户在 /proc 或任何 /proc 子目录中执行 ls(1) 命令时，系统实际上是在读取内核内存。

这种类文件抽象为进程提供了一种简单而优雅的方式来获取有关进程、其执行环境和内核资源利用的信息。诸如打开 /proc 文件对象以读取进程信息之类的简单操作，使用 procfs 相对容易。进程控制功能强大且相对直接；进程可以停止和启动，并且可以针对信号、陷阱和系统调用等建立事件驱动的停止。总的来说，进程管理和调试大大简化。值得注意的是，procfs 最初的设计目标是提供一组用于编写调试器的接口；自最初实现以来，它已经发生了很大的演变。

Solaris 系统附带了几条实现 /proc 的命令，用于提取信息和发出控制指令。这些命令位于 /usr/proc/bin 目录中，并在 proc(1) 手册页中有描述。我们在本书中使用了其中一些命令来提供不同内核抽象的示例，例如打开的文件或进程的地址空间。进程状态命令 ps(1) 也构建在 procfs 接口之上。

通过 /proc 文件系统提供的控制和信息数据以文件和子目录的层次结构维护。/proc 中实现的文件和子目录如下所列。有关这些文件及其使用的更多信息，请参阅 proc(4) 手册页。

- **`/proc`** — procfs 的顶级目录。
- **`/proc/<pid>`** — 特定进程的顶级目录，其中进程的 PID 就是目录名。
- **`/proc/<pid>/as`** — 进程的地址空间，由进程 proc 结构中指向地址空间结构（`struct as`）的 `p_as` 链接定义。换句话说，`/proc/<pid>/as` 文件所表示的进程地址空间并不是 /proc 特有的地址空间表示形式。相反，`/proc` 通过 proc 结构中的 `p_as` 指针提供了一条访问地址空间映射的路径。
- **`/proc/<pid>/ctl`** — 进程控制文件。可以以只写方式打开，用于向进程发送控制消息以启动特定事件或启用特定行为。示例包括停止或启动进程、在特定事件上设置停止，或打开微状态记账。

    该文件体现了 procfs 的强大与优雅；你可以通过打开目标进程的控制文件并写入一条（或多条）控制消息来注入期望的行为，从而实现进程控制和事件跟踪。有关控制消息和函数的详细列表，请参阅 proc(4) 手册页。

- **`/proc/<pid>/status`** — 关于进程的一般状态和状态信息。具体内容在 `pstatus` 结构中定义，该结构定义在 `/usr/include/sys/procfs.h` 中。`pstatus` 在 proc(4) 中也有描述。

    请注意，pstatus 内嵌了一个 `lwpstatus` 结构（pstatus 的 `pr_lwp` 字段）。该结构被描述为代表性 LWP。非线程进程只有一个 LWP，因此选择代表性 LWP 很简单。对于具有多个 LWP 的线程进程，内部内核例程会遍历进程中的所有 LWP，并根据其状态选择一个。首选是正在执行的 LWP。如果没有正在执行的 LWP，则选择条件会查找可运行、睡眠或停止的 LWP。

- **`/proc/<pid>/lstatus`** — 一个 `lwpstatus` 结构数组，进程中的每个 LWP 对应一个。
- **`/proc/<pid>/psinfo`** — 由 ps(1) 命令提供的进程信息。与上述状态数据类似，其中包含一个代表性 LWP，并内嵌 `lwpsinfo` 结构。
- **`/proc/<pid>/lpsinfo`** — 每个 LWP 的 ps(1) 信息。
- **`/proc/<pid>/map`** — 地址空间映射信息。由 pmap(1) 命令显示的数据。
- **`/proc/<pid>/rmap`** — 进程的保留地址空间段。
- **`/proc/<pid>/xmap`** — 扩展地址空间映射信息。由 pmap(1) 命令在带 `-x` 标志运行时显示的数据。
- **`/proc/<pid>/cred`** — 进程凭证，如 `prcred` 结构（`/usr/include/sys/procfs.h`）所述。
