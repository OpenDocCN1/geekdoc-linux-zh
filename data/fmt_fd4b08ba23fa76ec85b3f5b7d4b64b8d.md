
Linux 内核开发者并不喜欢过度使用 `ioctl`，因为从本质上讲，他们认为它可以用于执行几乎任何操作，包括本质上是系统调用的任何操作。

其中 `arg` 可以可以在用户空间中直接作为 `long` 或指针使用。在后者情况下，正确的方法是使用 `put_user()`、`get_user()`、`copy_to_user()` 和 `copy_from_user()` 函数。

要使用 `ioctl()`，必须先使用 `open()` 系统调用打开设备，然后发送相应的 `ioctl()` 命令和任何必要的参数。

```c
#include <sys/ioctl.h>
```

```c
int ioctl(int fd, int command, unsigned int arg);
```

第三个参数通常写为 `char *arg`。它的使用通常意味着变数量的参数。在这里，它表示不应对对参数进行类型检查，我们使用了一种技巧。你不应该向 `ioctl()` 调用传递三个以上的参数。

成功时返回 0，错误时返回 -1 并设置 `errno`。可能的返回错误有：

### 示例：

```c
static int mydvr_ioctl(struct inode *inode, struct file *file, unsigned int cmd, unsigned long arg)
{
    if (_IOC_TYPE(cmd) != MYDVRSASH)
        return -EINVAL;
    switch (cmd) {
        case MYDVR_RESET:
            /* 执行某些操作 */
            return 0;
        case MYDVR_OFFLINE:
            /* 执行某些操作 */
            return 0;
        case MYDVR_GETSTATE:
            if (copy_to_user((void *)arg, &mydvr_state_struct, sizeof(mydvr_state_struct)))
                return -EFAULT;
            return 0;
        default:
            return -EINVAL;
    }
}
```

### 表 13.1：`ioctl()` 返回值

| 值 | 含义 |
|---|---|
| `EBADF` | 文件描述符无效。 |
| `ENOTTY` | 文件描述符未关联字符设备，或者请求不适用于文件描述符引用的对象。 |
| `EINVAL` | 无效的命令或 `argp`。 |

### 示例：

```c
int fd = open("/dev/mydvr", O_RDWR);
```

```c
if (ioctl(fd, MYDVR_SET, buf) < 0)
perror("MYDVR_SET io failed");
```

## 13.2 ioctl 的驱动入口点

`ioctl()` 的入口点看起来如下：

```c
#include <linux/ioctl.h>
static int mydvr_ioctl(struct inode *inode, struct file *file, unsigned int cmd, unsigned long arg);
```

`ioctl()` 调用在大全局内核锁（BKL）下运行，如果它们运行时间很长，可能会导致不相关区域出现延迟。

系统调用通过 `ioctl()` 传递，它调用 `/usr/src/linux/fs/ioctl.c` 中的 `vfs_ioctl()`

```c
2.6.31 37 static long vfs_ioctl(struct file *file, unsigned int cmd, unsigned long arg)
2.6.31 38 30 (
2.6.31 39 (
2.6.31 40 int error = -ENOTTY;
2.6.31 41
2.6.31 42 if (file->f_op->locked_ioctl)
2.6.31 43
2.6.31 44 if (file->f_op->locked_ioctl)
2.6.31 45
2.6.31 46
2.6.31 47
2.6.31 48
2.6.31 49
2.6.31 50
2.6.31 51
2.6.31 52
2.6.31 53
2.6.31 54
2.6.31 55
2.6.31 56
2.6.31 57
```

## 第 13 章：IOCTL

```c
2.6.31 48		error = -EINVAL;
2.6.31 49		goto out;
2.6.31 50	} else if (file->f_op->locked_ioctl)
2.6.31 51		lock_kernel();
2.6.31 52	} else
2.6.31 53	out:
	return error;
2.6.31 54		unlock_kernel();
2.6.31 55	}
2.6.31 56	return error;
```

## 13.3. 无锁 IOCTLS

Linux 内核开发者并不喜欢过度使用 `ioctl`，因为从本质上讲，他们认为它可以用于执行几乎任何操作，包括本质上是系统调用的任何操作。

## 13.4 定义 IOCTL

两个重要的文件是 `usr/include/asm-generic/ioctl.h` 和 `Documentation/user/ioctl.txt`。

目前的实现是 32 位，包含四个字段：

### 表 13.3：`ioctl` 字段

| 名称 | 含义 | 描述 |
|---|---|---|
| | `_IOC_TYPE` | 魔数数 |
| 8 | `_IOC_NR` | 编号 |
| 14 | `_IOC_SIZE` | 大小 |
| 2 | `_IOC_DIR` | 方向 |

方向可以是：

- `_IOC_NONE`
- `_IOC_READ`
- `_IOC_WRITE`
- `_IOC_READOW`

使用的宏是：

```c
_IOC_NONE
_IOC_READ
_IOC_WRITE
_IOC_READOW
```

这不是唯一的方法，但是最常用的。

命令构造如下：

```c
_IOC(type, nr, size)
```

其中 `arg` 可以在用户空间中直接作为 `long` 或指针使用。在后者情况下，正确的方法是使用 `put_user()`、`get_user()`、`copy_to_user()` 和 `copy_from_user()` 函数。

要使用 `ioctl()`，必须先使用 `open()` 系统调用打开设备，然后发送相应的 `ioctl()` 命令和任何必要的参数。

第三个参数通常写为 `char *arg`。它的使用通常意味着变数量的参数。在这里，它表示不应对参数进行类型检查，我们使用了一种技巧。你不应该向 `ioctl()` 调用传递三个以上的参数。

成功时返回 0，错误时返回 -1 并设置 `errno`。

## 13.5 实验

### 实验 1：使用 ioctl 传递数据

编写一个简单的模块，利用 `ioctl` 方向信息在驱动程序和用户空间程序之间传递固定大小的数据缓冲区。

数据传输的大小和方向应该编码在命令数中。

你需要编写一个用户空间应用程序来测试它。

### 实验 2：使用 ioctl 传递变长度数据

扩展之前的练习，以发送在运行时确定长度的缓冲区。你可能需要在用户空间中使用 `_IOC` 宏。

### 实验 3：使用 ioctl 发送信号

有时需要从内核向应用程序发送信号。执行此操作的函数是：

```c
int send_sig(int signal, struct task_struct *task, int priv);
```

其中 `signal` 是要发送的信号，`task` 指向要发送信号进程对应的任务结构，`priv` 表示权限级别（用户应用程序为 0，内核为）。

编写一个具有三个 `ioctl` 命令的字符驱动程序。

## 第 14 章

## proc 文件系统

![](img/4e539a55ab31f2c9df39e648783d8023_92_0.png)

我们将讨论 `proc` 文件系统。我们将展示如何在此文件系统中创建、读取和写入条目。最最后，我们还将讨论 `seq_file` 接口以及如何使用它创建 `proc` 文件系统条目。

- 14.1 什么是 `proc` 文件系统？............................................................................................... 161
