
```c
cmd = LINUX_REBOOT_CMD_HALT;

lock_kernel();

switch (cmd) {

case LINUX_REBOOT_CMD_RESTART:

    kernel_restart(NULL);

    break;

case LINUX_REBOOT_CMD_CAD_ON:

    C_A_D = 1;

    break;

case LINUX_REBOOT_CMD_CAD_OFF:

    C_A_D = 0;

    break;

case LINUX_REBOOT_CMD_HALT:

    kernel_halt();

    unlock_kernel();

    do_exit(0);

    break;

case LINUX_REBOOT_CMD_POWER_OFF:

    kernel_power_off();

    unlock_kernel();

    do_exit(0);

    break;

case LINUX_REBOOT_CMD_RESTART2:

    if (copy_from_user(&buffer[0], arg, sizeof(buffer) - 1) < 0) {

        unlock_kernel();

        return -EFAULT;

    }

    buffer[sizeof(buffer) - 1] = '\0';

    kernel_restart(buffer);

    break;

default:

    unlock_kernel();

    return -EINVAL;

}

unlock_kernel();

return 0;

}
```

参见 `<linux/capability.h>` 以获取所有能力及其包含权限的列表。

## 系统调用上下文

正如第 3 章所述，在执行系统调用期间，内核处于进程上下文中。`current` 指针指向当前任务，即发出系统调用的进程。

在进程上下文中，内核能够休眠（例如，如果系统调用在某个调用上阻塞或显式调用 `schedule()`）并且完全可抢占。这两点很重要。首先，休眠的能力意味着系统调用可以利用内核的大部分功能。正如我们将在第 7 章“中断和中断处理程序”中看到的，休眠的能力大大简化了内核编程。[^1] 进程上下文可抢占的事实意味着，与用户空间类似，当前任务可能会被其他任务抢占。由于新任务随后可能执行相同的系统调用，因此必须谨慎行事，以确保系统调用是可重入的。当然，这也是对称多处理所引入的担忧。关于同步重入的内容在第 9 章“内核同步简介”和第 10 章“内核同步方法”中涵盖。

当系统调用返回时，控制在 `sys_em_call()` 中继续，最终切换到用户空间并继续执行用户进程。

## 绑定系统调用的最后步骤

在编写系统调用之后，将其注册为官方系统调用非常容易：

- 在系统调用表的末尾添加一个条目。需要为支持该系统调用的每个架构执行此操作（对于大多数调用，这是所有架构）。系统调用在表中的位置（从零开始）就是它的系统调用号。例如，列表中的第十个条目被分配系统调用号九。
- 对于每个受支持的架构，在 `<asm/unistd.h>` 中定义系统调用号。
- 将系统调用编译到内核映像中（而不是将其编译为模块）。这可以很简单，只需将系统调用放在 `<kernel/>` 中相关的文件中，例如 `<sys.c>`，它是杂项系统调用的所在地。

让我们通过一个虚构的系统调用 `foo()` 更详细地查看这些步骤。首先，我们想要将 `sys_foo()` 添加到系统调用表中。对于大多数架构，表位于 `<entry.S>` 中，看起来像这样：

```assembly
ENTRY(sys_call_table)

    .long sys_restart_syscall    /* 0 */

    .long sys_exit

    .long sys_fork

    .long sys_read

    .long sys_write

    .long sys_open               /* 5 */

    ...

    .long sys_eventfd2

    .long sys_epoll_create1

    .long sys_dup3              /* 330 */

    .long sys_pipe2

    .long sys_inotify_init1

    .long sys_preadv

    .long sys_pwritev

    .long sys_rt_tgsigqueueinfo /* 335 */

    .long sys_perf_event_open

    .long sys_recvmmsg
```

然后将新的系统调用附加到该列表的末尾：

```assembly
.long sys_foo
```

尽管没有明确指定，但系统调用随后被赋予下一个顺序的系统调用号——在这种情况下是 338。对于想要支持的每个架构，必须将系统调用添加到该架构的系统调用表中。系统调用不需要在每个架构下获得相同的系统调用号，因为系统调用号是架构唯一 ABI 的一部分。通常，你希望让系统调用在每个架构上都可用。请注意每五个条目在注释中放置编号的约定；这使得查找哪个系统调用被分配了哪个编号变得容易。

接下来，系统调用号被添加到 `<asm/unistd.h>` 中，其当前内容大致如下：

```c
/*
 * 此文件包含系统调用号。
 */

#define _NR_restart_syscall 0

#define _NR_exit 1

#define _NR_fork 2

#define _NR_read 3

#define _NR_write 4

#define _NR_open 5

...

#define _NR_signalfd4 327

#define _NR_eventfd2 328

#define _NR_epoll_create1 329

#define _NR_dup3 330

#define _NR_pipe2 331

#define _NR_inotify_init1 332

#define _NR_preadv 333

#define _NR_pwritev 334

#define _NR_rt_tgsigqueueinfo 335

#define _NR_perf_event_open 336

#define _NR_recvmmsg 337
```

然后在列表末尾添加以下内容：

```c
#define _NR_foo 338
```

[^1]: 中断处理程序不能休眠，因此与在进程上下文中运行的系统调用相比，它们能做的事情受到更大的限制。

最后，实际的 `foo()` 系统调用得以实现。由于系统调用必须在所有配置下都被编译到核心内核镜像中，在这个示例中，我们在 `kernel/sys.c` 中定义了它。你应该将其放在该函数最相关的地方；例如，如果该函数与调度相关，你可以将其定义在 `kernel/sched.c` 中。

```c
#include <asm/page.h>

/*
 * sys_foo - 每个人都喜欢的系统调用。
 *
 * 返回每个进程的内核栈大小。
 */

asmlinkage long sys_foo(void)

{

    return THREAD_SIZE;

}
```

就这样！启动这个内核后，用户空间就可以调用 `foo()` 系统调用。

## 从用户空间访问系统调用

通常，C 语言库提供对系统调用的支持。用户应用程序可以从标准头文件中引入函数原型，并与 C 语言库链接，从而使用你的系统调用（或者由库运行时进而使用你的 `syscall.c`）。然而，如果你刚刚编写了这个系统调用，glibc 很可能尚未支持它！

幸运的是，Linux 提供了一组宏来封装对系统调用的访问。这些宏设置了寄存器内容并发出陷阱指令。这些宏被称为 `__syscall{n}()`，其中 `n` 在 0 到 6 之间。这个数字对应于传入系统调用的参数数量，因为宏需要知道预期有多少个参数，从而将这些参数推送到寄存器中。例如，考虑定义如下的 `open()`：

```c
long open(const char *filename, int flags, int mode)
```

要在没有显式库支持的情况下使用此系统调用，所使用的系统调用宏应为：

```c
#define _NR_open 5
__syscall3(long, open, const char *, filename, int, flags, int, mode)
```
