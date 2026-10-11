
## 12.1 什么是 ioctls?

`ioctl`（输入输出控制）是特殊的函数，用于与设备通信。`ioctl(1)` 是可以从用户态发送或接收的命令。

`ioctl` 几乎可以执行任何操作，类似于 `read()`、`read()` 等。

为了使用 `ioctl`，必须首先使用 `open()` 系统调用打开设备，然后发送相应的 `ioctl(1)` 命令。

```c
#include <sys/ioctl.h>

int ioctl(int fd, ...);
```

参数通常是 `char *arg`。成功时返回 0，错误时返回 `errno`。

表 12.1：`ioctl()` 返回值

| 值 | 含义 |
| :--- | :--- |
| EBADF | 错误的文件符 |
| ENOTTY | 未与设备关联 |
| EINVAL | 无效命令 |

示例：

```c
int fd = open("/dev/mydrvr", O_RDWR);
if (ioctl(fd, MYDRVR_SET, buf) < 0)
    perror("MYDRVR_SET failed");
```

## 12.2 ioctls 的入口点

`ioctl()` 的入口点如下：

```c
#include <linux/ioctl.h>
static int mydrvr_unlocked_ioctl(struct file *file, unsigned int cmd, unsigned long arg)
{
    if (_IOC_TYPE(cmd) != MYDRBASE)
        return -EINVAL;

    switch (cmd) {
        case MYDRVR_RESET:
            /* 执行某些操作 */
            return 0;

        case MYDRVR_OFFLINE:
            /* 执行某些操作 */
            return 0;
    }
}
```

## 12.3 加锁与无锁的 ioctls

从 Linux 早期开始，`ioctl()` 入口点实际上具有原型：

`int ioctl(struct inode *inode, struct file *filp, unsigned int cmd, unsigned long arg);`

不幸的是这些加锁调用会导致 BKL（大锁）；如果它们运行时间长，可能会导致无关区域出现巨大的延迟。

注意，BKL 允许睡眠，与其他锁不同，加入队列不足以阻塞系统；你实际上执行了一些占用 CPU 时间的工作。引入引入无锁入口点是为了避免 BKL，如果它存在 `file_operations` 结构中，它将取代加锁版本。

在 2.6.36 内内核中，加锁版本的 `ioctl()` 入口点最终被移除。驱动程序无法再次使用它。

移除加锁的 `ioctl()` 系统调用是移除系统调用和驱动程序中 BKL 项目的一部分，目标是逐个消除。

## 12.4 定义 ioctls

在使用 `ioctl()` 之前，必须为整数命令参数选择数字。仅仅随机选择数字是一个坏主意；它们在整个系统中应该是唯一的。

至少可能出现以下两种错误：

两个设备节点可能具有相同的主设备号。

应用程序可能会犯错，打开了多个设备并混淆了文件描述符，向错误的设备发送了正确的命令。

结果可能是灾难性的，甚至损坏硬件。

```c
case MYDRVR_GET_STATE:
    if (copy_to_user((void *)arg, &mydrvr_state_struct, sizeof(mydrvr_state_struct)))
        return -EFAULT;
    return 0;

default:
    return -EINVAL;
```

两个文件是 `/usr/src/linux/include/asm-generic/ioctl.h` 和 `/src/linux/Documentation/ioctl/ioctl-number.txt`。

在当前的实现中，命令长度为 32 位；命令位于低 16 位中（这是旧的大小）。它包含四个位域：

表 12.3: `ioctl()` 命令位域

| 位数 | 名称 | 含义 | 描述 |
|---|---|---|---|
| 8 | IOC_TYPEBEITS | type | 整个驱动程序中使用的魔数 |
| 8 | IOC_NRBITS | number | 序列号 |
| 14 | IOC_SIZEBITS | size | 数据传输的大小 |
| 2 | IOC_DIRBITS | direction | 数据传输的方向 |

方向可以是以下之一：

`IOC_NONE`

`IOC_READ`

`IOC_WRITE`

`IOC_READ | IOC_WRITE`

并且从应用程序的角度来看是这样定义的。

大小和方向信息可以使用 `arg` 作为指针来简化用户空间和内核空间之间的数据传传。请注意，这里没有强制规定；你可以向任何方向发送信息，而不取决于定义命令时使用的方向。通过这种方式设置的最大传输量是 16 KB，因为你只有 14 位用于编码大小。

你不需要关注命令中位拆分的情况，但这样做是一个好主意。

### 有用的宏：

编码 `ioctl` 数字：

```
IO(type, number)
IOR(type, number, size)
IOW(type, number, size)
IOWR(type, number, size)
```

人们必须小心参数大小的使用方式。与其传递一个整数，不如传递实际的数据结构，然后对该结构应用 `sizeof()` 原语；例如：

```
MY_IOCTL = IOWR('k', 1, struct my_data_structure);
```

如果 `my_data_structure` 是动态分配的，这将行不通，因为在这种情况下 `sizeof()` 将返回指针的大小。

解码 `ioctl` 数字：

`IOC_DIR(cmd)`

`IOC_TYPE(cmd)`

`IOC_NR(cmd)`

`IOC_SIZE(cmd)`

## 12.5 实验

示例：

```
#define MYDRBASE 'k'
#define MYDR_RESET IO(MYDRBASE, 1)
#define MYDR_STOP IO(MYDRBASE, 2)
#define MYDR_READ IOR(MYDRBASE, 2, my_data_buffer)
```

### 实验 1：使用 ioctl() 传递数据

编写一个简单的模块，使用 `ioctl` 方向信息在驱动程序和用户空间程序之间传回固定大小的数据缓冲区。

数据传输的大小和方向（们）应该编码在命令数字中。

你需要编写一个用户空间应用程序来测试此。

### 实验 2：使用 ioctl() 传递变长数据

扩展上一个练习，发送一个长度在运行时确缓冲区。你可能需要在用户空间程序中直接使用 `_IOC` 宏（参见 `linux/ioctl.h`）。

### 实验 3：使用 ioctl() 发送信号

有时需要从内核向应用程序发送信号。执行此操作的函数是：

`int send_sig(int signal, struct task_struct *tsk, int priv);`

其中 `signal` 是要发送的信号，`task` 指向要发送信号的进程对应的 `task` 结构，`priv` 表示权限级别（用户应用程序为 0，内核为 1）。

编写一个具有三个 `ioctl` 命令的字符驱动程序：

设置要发送信号的进程 ID。

设置要发送的信号。

发送信号。

记住你必须使用 `pid_task(find_vpid(pid), PIDTYPE_PID)` 将 `pid` 连接到它对应的 `task` 结构。

你还需要开发发送端程序。

如果没有给出任何参数，它应该向当前进程发送 `SIGKILL`。

如果给出了一个参数，它应该设置要发送信号的进程 ID。

如果给出了两个参数，它还应该设置信号。

# 第 13 章
