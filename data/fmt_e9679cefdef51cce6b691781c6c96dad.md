
在接下来的页面中，我们不会对任务（`tasks`）和进程（`processes`）的概念进行任何精确的区分，而是使用这两个词表示相同的意思。当任务运行在特权系统模式（`System Mode`）下时，它可以处于若干状态中的一种。图 3.2 显示了这些最重要的状态。图中的箭头显示了可能的状态变化。以下是可能的状态：

![](img/04698aadad5d50fd4b3564ae373ff0bd_27_0.png)

图 3.1 从外部和内部看到的进程。

![](img/04698aadad5d50fd4b3564ae373ff0bd_28_0.png)

图 3.2 进程内部状态图。

## 运行 (Running)

任务在非特权用户模式（`User Mode`）下激活并运行。在这种情况下，进程将以完全正常的方式通过程序。这种状态只能通过中断或系统调用退出。在第 3.3 节中我们将看到系统调用实际上只是中断的特殊情况。无论哪种情况，处理器都会切换到特权系统模式（`System Mode`），并激活相应的中断例程。

## 中断例程 (Interrupt routine)

当硬件信号异常条件时，中断例程变为激活，这可能是键盘输入的新字符，可能是时钟发生每 10 毫秒发出一次信号。关于中断例程的更多信息见第 3.2.2 节。

## 系统调用 (System call)

系统调用由软件中断触发。细节见第 3.3 节。系统调用能够挂起任务以等待事件。

## 等待 (Waiting)

进程正在等待外部事件。只有在事件发生后，它才会继续工作。

## 系统调用返回 (Return from system call)

此状态在每次系统调用和某些中断后会自动被采用。在此时，会检查是否需要调用调度器以及是否有需要处理的信号。调度器可以将进程切换到“就绪”（`Ready`）状态并激活另一个进程。

- 就绪 (Ready)

进程正在竞争处理器，但目前处理器被另一个进程占用。

## 进程与线程 (Processes and threads)

在许多现代操作系统中，进程和线程是有区别的。线程是程序过程中的一种独立“线”，可以与其他线程并行处理。与进程不同，线程在同一主内存上工作，因此可以影响 `Linux`。`Linux` 并没有做这种区分。在内核中，只有任务的概念，任务可以与其他任务共享资源（例如，相同的内存）。因此，任务是普通线程概念的泛化。更多细节可以参见第 3.3.3 节。

## 3.1 重要数据结构 (Important data structures)

本章描述了 `LINUX` 内核中的重要数据结构。理解这些结构以及它们如何相互作用至关重要。

### 3.1.1 任务结构 (The task structure)

内核中只有任务可以与其他任务共享资源（例如相同的内存）的概念。任务结构包含了进程的状态。

```
struct task_struct {
volatile long counter;
```

`counter` 变量存储了进程的“节数”（见 3.2 节）。调度器使用 `counter` 来选择下一个进程。

```cpp
long priority;
```

`priority` 变量持有进程的动态优先级，而 `priority` 持有静态优先级。这两个组件由调度器修改。

```
unsigned long signal;
unsigned long blocked;
```

`signal` 变量包含信号的掩码；`blocked` 包含信号的掩码。由于这两个组件限制为 32 位，它们是长整数。

```
unsigned long flags;
int errno;
int debugreg[8];
```

`flags` 包含了标志 `PF_TRACED`、`PF_TRYS`、`PF_STARTING` 和 `PF_EXITING`。还有标志（定义在 `include/sched.h` 中），但仅用于进程统计（系统调用），在此不解释。`errno` 变量持有上次系统调用的错误代码。从系统调用返回时，它会被拷贝到全局变量（见第 3.3 节）。`debugreg` 变量包含调试寄存器。这些目前仅由系统调用 `ptrace` 使用。

```
struct exec_domain *exec_domain;
long state;
```

`state` 变量包含了进程当前的状态。如果进程正在运行，状态取值为 `TASK_RUNNING`。相反，如果进程正在等待事件，状态取值为 `TASK_INTERTIBLE` 或 `TASK_UNINTERTIBLE`。`TASK_STOPPED` 描述接收信号（`SIGSTOP` 或 `SIGTOU`）后停止的进程。`TASK_ZOMBIE` 描述一个已终止但仍存在于进程表的进程。还有 `TASK_EXITING` 状态，表示进程正在终止。

`LINUX` 可以运行来自其他符合 `i386` 和 `POSIX` 标准系统的程序。由于这些系统略有不同，每个进程要模拟的 `UNIX` 描述保存在 `exec_domain` 中。这完成了任务结构的硬编码部分。为了简单起见，任务结构的以下组件被分组考虑

双向链表：

```
struct task_struct *next_task;
struct task_struct *prev_task;
```

该列表的起始和结束保存在全局变量 `init_task` 中。

# Linux 内内核原理

`p_pptr` 变量是一个指向父进程 `task` 结构的指针。为了让进程能够访问其所有的子进程，`task` 结构保存了最后一个创建的子进程的条目——“最小子进程”。

![](img/04698aadad5d50fd4b3564ae373ff0bd_32_0.png)

图 3.3 进程之间的“家族关系”。同一个父进程的子进程同样通过 `p_ysptr`（下一个更小的兄弟）和 `p_osptr`（上一个较大的兄弟）以双向链的形式连接在一起。图 3.3 应该阐明进程之间的“家族关系”。

调度器使用一个包含所有申请处理器的进程列表。它通过以下两个组件实现为双向链表：

```c
struct task_struct *next_task;
struct task_struct *prev_task;
```

在这里，外部变量 `in_task_task` 描述了该列表的起始和结束。

## 内存管理

为了简单起见，每个进程内存管理所需的数据都收集在它们自己的子结构中：

```c
struct mm_struct mm[1];
```

其组件包括：

```c
unsigned long start_code, end_code, start_data, end_data;
unsigned long start_brk, brk, unsigned long start_stack, start_mmap;
unsigned long arg_start, arg_end, env_start, env_end;
```

它们描述了当前运行程序的代码段和数据段的起始位置和大小。更多信息见第 4 章。

`task_struct` 结构有两个与内存管理相关的组件。当进程在内核模式（`System Mode`）下运行时，它需要自己的栈（与用户模式的栈不同）。栈地址存储在：

```c
unsigned long kernel_stack_page;
```

对于 `MS-DOS` 模拟器（更准确地说，对于系统调用 `vm86`），还有

```c
unsigned long saved_kernel_stack;
```

其中存储了旧的栈指针。

## 进程 ID

每个进程都有自己的进程号 `pid`，并被分配到一个进程组 `pgrp` 和一个会话 `session`。每个会话都有一个领导进程 `leader`。

```c
int pid, pgrp, session, control, leader;
```

为了处理访问控制，每个进程都有一个用户 ID `uid` 和组 ID `gid`。当通过 `fork` 系统调用创建新进程时，这些值从父进程继承自子进程（见第 3.3.3 节和附录 A）。然而，对于实际的访问控制使用的是有效用户 ID `euid` 和有效组 ID `egid`。`LINUX` 的新功能是组件 `fsuid`。每当系统需要标识时就会使用它。根据一般规则，`(uid==euid)` 且 `(gid==gid)` 且 `(fsuid==euid)` 且 `(fsgid==gid)`。

所谓的 `set-UID` 程序会出现异常，`euid` 和 `fsuid` 的值，或 `egid` 的值被设置为可执行文件所有者的用户 ID 和 `gid`。这使得受控制的权限分配成为可能。

通常，`fsuid` 始终取 `cuid` 的值；在其他 `UNIX` 系统或旧版本的 `LINUX` 中，有效用户 ID `euid` 始终用于替代 `fsuid`。然而，`LINUX` 的 `setuid` 系统调用允许守护进程在访问带有 `setuid` 的文件时保持其权利（即它们提供服务的用户的权利），但它们将保留自己的特权。引入此项是因为 `NFS` 守护进程存在安全漏洞。为了限制其对文件系统的访问权限，将此 `euid` 设置为请求用户的用户 ID。文件访问随后按预期工作，但它也允许用户向守护进程发送信号。这不是预期的结果，现在已经进行了更改。组件 `fsgid` 也有类似的考虑。
