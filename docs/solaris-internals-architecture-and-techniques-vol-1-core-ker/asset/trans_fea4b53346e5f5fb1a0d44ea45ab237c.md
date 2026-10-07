

# proc — 进程文件系统

这些字段，从而将请求的数据提供给调用者：例如，`pr_read_psinfo()` 会从目标进程的 proc 结构、凭据结构（credentials structure）和地址空间（as）结构中读取数据，并将其写入 psinfo 结构中相应的字段。满足客户端请求所需的内核数据访问是通过 proc 进程的互斥锁 `plock` 进行同步的。这种方法保护了同时被多个客户端访问的进程或 LWP（轻量级进程）内核数据。

对 procfs 文件的写入操作要少得多。除了创建数据文件的指令外，写入操作主要是针对进程或 LWP 控制文件（ctl）以发送控制消息。控制消息（在 proc(1) 中记录）包括停止/启动消息、信号追踪与控制、异常管理、执行控制（例如，系统调用进入和退出停止）以及地址空间监控。

**注意：** 我们之前通过标准调用讨论了 procfs 文件上的 I/O 操作，因为这些目前是开发者编写的代码访问 /proc 文件的唯一方式。然而，存在一组特定于 procfs 的接口，供 Solaris 随附的 proc(1) 命令使用。这些接口被封装在 `libproc.so` 库中，目前尚未文档或供公开使用。`libproc.so` 库包含在 /usr/lib 分中，但这些接口仍在演进中，尚未文档。目前计划记录这些 libproc.so 接口并将其作为 Solaris API 的标准部分。前几页介绍的内核 procfs 模块的接口层如图 8.20 所示。

### 图 8.20 procfs 接口层

图 8.20 显示了进入 procfs 的多条路径。典型的开发者编写的代码使用较短的系统调用路径，如前所述通过 vnode 层传递。proc(1) 命令是很大程度上基于 `libproc.so` 构建的多线程架构。需要一组特定于 procfs 的接口的原因有两点：一组易于使用的开发例程程序降低了使用强大内核设施的复杂性；特别是多线程进程，需要一层真正属于应用程序接口（而非内核级）的代码层。开发者通过向控制文件的前 8 字节（如果是 LP64 则为 16 字节）写入操作（可选）来控制进程。控制文件的写入路径通过 vnode 层并最终终止于 procfs。该实现允许在单次写入向控制文件发送多个控制消息（操作和操作数）。`pwrichtctl()` 代码将多个消息拆分为不同的操作/操作数对，并将它们传递给 `control()` 函数，在该函数中，会在进程或 LWP 级别设置适当的标志，作为控制机制注入的通知（例如，发生事件时停止）。表 8-3 列出了目前实现的可能控制消息（操作）。我们在此包含它们是为了为后续对控制函数的描述提供背景信息，并说明 proc(1) 手册页和 /usr/include/sys/procfs.h 的强大之处。

## 表 8-3 procfs 控制消息

| 控制消息 | 操作数 (arg) | 描述 |
| :--- | :--- | :--- |
| PCSTOP | n/a | 请求进程或 LWP 停止；等待停止。 |
| PCDSTOP | n/a | 请求进程或 LWP 停止。 |
| PCSTOP | n/a | 等待进程或 LWP 停止。未实现超时。 |
| PCTSTOP | timeout value | 等待停止，参数为毫秒。 |
| PCRUN | long | 设置进程或 LWP 可运行。任何参数都可以指定清除信号或异常、设置步模式等。 |
| PCSIG | n/a | 清除 LWP 的当前信号。 |
| PCFAULT | n/a | 清除 LWP 的当前异常。 |
| PCSIGSIG | siginfo_t | 从 siginfo_t 设置当前信号。 |
| PCKILL | long |向进程或 LWP 发送信号。 |
| PCUNKILL | long | 删除进程或 LWP 中的挂起信号。 |
| PCSHOLD | sigset_t | 从参数设置 LWP 信号掩码。 |
| PCTRACE | sigset_t | 从参数设置追踪的信号集。 |
| PCFAULT | flyset_t | 从参数设置追踪的异常。 |
| PCSENTRY | sysset_t | 从参数设置系统调用的追踪（进入时）。 |
| PCSEXIT | sysset_t | 从参数设置系统调用的追踪（退出时）。 |
| PCSET | long | 设置进程/LWP 中的模式。 |

## 表 8-3 procfs 控制消息（续）

| 控制消息 | 操作数 (arg) | 描述 |
| :--- | :--- | :--- |
| PCIPSET | long | 取消进程/LWP 中的模式。 |
| PCSREG | prgregset_t | 从参数设置 LWP 的通用寄存器。 |
| CSFPREG | prfregset_t | 从参数设置 LWP 的浮点寄存器。 |
| PCSXREG | prxregset_t | 从参数设置 LWP 的寄存器。 |
| PCNICE | long | 从参数设置 nice 值。 |
| PCSVADDR | long | 将 PC（程序计数器）设置为参数中的虚拟地址。 |
| PCSWATCH | pratch_t | 从参数设置或清除监控的内存区域。 |
| PCAGENT | prgregset_t | 使用参数中的寄存器值创建 LWP。 |
| PCREAD | priovec_t | 通过参数从进程空间读取。 |
| PCWRITE | priovec_t | 通过参数写入进程空间。 |
| PCSCRED | prcred_t | 从参数设置进程凭据。 |
| PCSASARS | asrt_t | 从参数设置辅助状态寄存器。 |

从从提供的各种控制消息可以看出，进程/LWP 控制的实现与进程文件系统紧密集成。

