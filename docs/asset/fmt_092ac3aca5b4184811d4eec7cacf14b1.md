
```c
Code View:
#define CMOS_ADJUST_CHECKSUM 1
#define CMOS_VERIFY_CHECKSUM 2

#define CMOS_BANK1_CRC_OFFSET 0x1E

/*
 * 用于调整和验证 CRC16 的 Ioctls。
 */
static int
cmos_ioctl(struct inode *inode, struct file *file,
           unsigned int cmd, unsigned long arg)
{
  unsigned short crc = 0;
  unsigned char buf;

  switch (cmd) {
  case CMOS_ADJUST_CHECKSUM:
    /* 使用种子 0 计算 bank0 的 CRC */
    crc = adjust_cmos_crc(0, 0);

    /* 使用 bank0 的 CRC 作为 bank1 的种子 */
    crc = adjust_cmos_crc(1, crc);

    /* 存储计算出的 CRC */
    port_data_out(CMOS_BANK1_CRC_OFFSET,
                   (unsigned char)(crc & 0xFF), 1);
    port_data_out((CMOS_BANK1_CRC_OFFSET + 1),
                   (unsigned char) (crc >> 8), 1);
    break;

  case CMOS_VERIFY_CHECKSUM:
    /* 使用种子 0 计算 bank0 的 CRC */
    crc = adjust_cmos_crc(0, 0);

    /* 使用 bank0 的 CRC 作为 bank1 的种子 */
    crc = adjust_cmos_crc(1, crc);

    /* 将计算出的 CRC 与存储的 CRC 进行比较 */
    buf = port_data_in(CMOS_BANK1_CRC_OFFSET, 1);
    if (buf != (unsigned char) (crc & 0xFF)) return -EINVAL;

    buf = port_data_in((CMOS_BANK1_CRC_OFFSET+1), 1);
    if (buf != (unsigned char)(crc >> 8)) return -EINVAL;
    break;

  default:
    return -EIO;
  }

  return 0;
}
```

### 感知数据可用性

许多用户应用程序非常复杂，不满足于老旧的 `open()`/`read()`/`write()`/`close()` 调用。它们希望得到同步或异步的通知，以便在设备有新数据可用或驱动程序准备好接受新数据时得到提醒。在本节中，我们将探讨两种感知数据可用性的字符驱动程序方法：`poll()` 和 `fasync()`。前者是同步的，而后者是异步的。由于这些机制相对高级，让我们先了解应用程序如何使用这些功能，然后再了解底层驱动程序如何实现它们。感知数据可用性与前面讨论的简单 CMOS 内存设备无关，因此让我们从一个人气很高的用户空间应用程序中选取几个使用场景：X Windows 服务器。

### 轮询

考虑以下来自 X Windows 源代码树的代码片段（可从 www.xfree86.org 下载），该片段处理鼠标事件：

```
xc/programs/Xserver/hw/xfree86/input/mouse/mouse.c:
case PROT_THINKING:             /* ThinkingMouse */
/* 此鼠标可能发送 PnP ID 字符串，忽略它。 */
usleep(200000); xf86FlushInput(pInfo->fd);
/* 发送命令以初始化该设备。 */
for (s = "E5E5"; *s; ++s) {
        xf86WriteSerial(pInfo->fd, s, 1);
        if ((xf86WaitForInput(pInfo->fd, 1000000) <= 0))
                break;
        xf86ReadSerial(pInfo->fd, &c, 1);
        if (c != *s) break;
}
break;
```

本质上，该代码向鼠标发送初始化命令，轮询直到检测到输入数据，然后从设备读取响应。如果你解开之前使用的 `XF86WaitForInput()` 的外壳，你会发现对 `select()` 系统调用的调用：

**代码视图：**

```
xc/programs/Xserver/hw/xfree86/os-support/shared/posix_tty.c:
int
xf86WaitForInput(int fd, int timeout)
{
        fd_set readfds;
        struct timeval to;
        int r;

        FD_ZERO(&readfds);
        if (fd >= 0) {
                FD_SET(fd, &readfds);
        }

        to.tv_sec = timeout / 1000000;
        to.tv_usec = timeout % 1000000;

        if (fd >= 0) {
SYSCALL(r = select(fd_setsize, &readfds, NULL, NULL, &to));
} else {
SYSCALL(r = select(fd_setsize, NULL, NULL, NULL, &to));
}

if (xf86Verbose >= 9)
ErrorF("select returned %d\n", r);

return (r);
}
```

你可以向 `select()` 提供一组文件描述符，并要求它密切关注这些描述符，直到相关的数据状态发生变化。你还可以请求超时以覆盖数据可用性。如果你请求的超时为 `NULL`，`select()` 将永久阻塞。有关 `select()` 的详细说明，请参阅其 man 或 info 页面。前面片段中对 `select()` 的调用促使 X 服务器在超时时间内轮询已连接鼠标的数据。

Linux 支持另一个系统调用 `poll()`，其语义与 `select()` 类似。2.6 内核支持一个名为 `epoll()` 的新非 POSIX 系统调用，它是 `poll()` 的可扩展超集。所有这些系统调用都依赖于同一个底层字符驱动程序方法 `poll()`。

大多数 I/O 系统调用符合 POSIX 标准，并非 Linux 特有（毕竟像 X Windows 这样的程序运行在许多 UNIX 变体上，而不仅仅是 Linux），但内部驱动程序方法是操作系统特定的。在 Linux 上，`poll()` 驱动程序方法是 `select()` 系统调用的支柱。在之前的 X 服务器场景中，鼠标驱动程序的 `poll()` 方法如下所示：

```
static DECLARE_WAIT_QUEUE_HEAD(mouse_wait); /* 等待队列 */
static unsigned int
mouse_poll(struct file *file, poll_table *wait)
{
 poll_wait(file, &mouse_wait, wait);
spin_lock_irq(&mouse_lock);

/* 查看数据是否已从设备到达，
或者设备是否准备好接受更多数据 */
/* ... */
spin_unlock_irq(&mouse_lock);

/* 数据可用性从中断上下文中检测 */
if (data_is_available()) return(POLLIN | POLLRDNORM);

/* 可以写入数据。对于鼠标而言不适用 */
if (data_can_be_written()) return(POLLOUT | POLLWRNORM);

return 0;
}
```

当 `Xf86WaitForInput()` 调用 `select()` 时，通用的内核轮询实现（定义在 `fs/select.c` 中）会调用 `mouse_poll()`。`mouse_poll()` 接受两个参数，常规的文件指针（`struct file *`）和一个指向内核数据结构 `poll_table` 的指针。`poll_table` 是一个由正在被轮询以获取数据的设备驱动程序拥有的等待队列表。
