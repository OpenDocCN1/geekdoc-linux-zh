
注意，缓冲区 `buf` 位于用户地址空间，因此字节必须使用 `get_user()` 读取。如果数据字节在一定时间内无法传输，则驱动程序应该放弃尝试（超时）或在进一步的延迟后重试。可以使用以下机制来实现此点。

```c
if (current->signal & ~current->blocked) { 
    if (temp != buf)
        return temp - buf;
    else
        return -EINTR;
}
current->state = TASK_INTERRUPTIBLE;
current->timeout = jiffies + LP_TIME(minor);
schedule();
```

这首先测试当前进程是否收到了信号。如果是，函数将终止并返回传输的字节数。然后进程被切换到 `TASK_INTERRUPTIBLE` 模式，通过将等待时间（以 tick 为单位）加上当前 `jiffies` 值来确定唤醒时间。调用 `schedule()` 会在此期间保持进程，直到接收到信号。程序随后返回 `schedule()`；如果发生了超时，`current->timeout` 将为 0。

现在我们以 PC 扬声器驱动程序的简化 `write()` 函数作为中断操作的示例。

```c
static int pcsp_write(struct inode *inode, struct file *file,
                      char *buffer, int count) {
    unsigned long copy_size;
    unsigned long max_copy_size;
    unsigned long total_bytes_written = 0;
    unsigned long bytes_written;
    int i;

    max_copy_size = pcsp.frag_size 
                    ? pcsp.frag_size : pcsp.ablk_size;

    do {
        bytes_written = 0;
        copy_size = (count <= max_copy_size) 
                    ? count : max_copy_size;
        i = pcsp.in[0] ? 1 : 0;
        if (copy_size && &pcsp.in[i]) {
            memcpy_from_user(pcsp.buf[i], buffer, copy_size);
            pcsp.in[i] = copy_size;
            if (!pcsp.timer_on) pcsp_start_timer();
            bytes_written += copy_size;
            buffer += copy_size;
        }
        if (pcsp.in[0] && pcsp.in[1]) {
            interruptible_sleep(&pcsp.sleep);
            if (current->signal & ~current->blocked) { 
                if (total_bytes_written + bytes_written)
                    return total_bytes_written;
            }
        }
    } while (count > 0);
}
```

# Linux 内核原理 - 231 -

`_IOW(c, d, t)` 用于向用户地址空间写回 C 类型权值的命令；
`_IOR(c, d, t)` 用于从用户地址空间读取 C 类型 `t` 值的命令；
`_IOWR(c, d, t)` 用于既读又写的命令。
总之，我们将此作为驱动程序中某些 `IOCTL` 定义的示例。

```c
#define SNDCTL_DSP_RESET _IO('P', 0)
#define SNDCTL_DSP_SYNC _IO('P', 1)
#define SNDCTL_DSP_SPEED _IOWR('P', 2, int)
#define SNDCTL_DSP_STEREO _IOWR('P', 3, int)
```

因此，例如 `SNDCTL_DSP_RESET` 命令不需要任何参数，而 `SNDCTL_DSP_SPEED` 则从用户地址空间读取一个 `int` 类型的参数并返回一个结果。例如，`<linux/ioctl.h>` 文件也包含了用于简化 `IOCTL` 命令解码的宏：
`_IOC_DIR(CMD)` 返回它是输入还是输出命令，`_IOC_TYPE(CMD)` 返回设备标识符，`_IOC_NR(CMD)` 返回不带类型信息的命令，`__IOC_SIZE(CMD)` 返回接收到的参数的字节大小。
`Documentation/ioctl-number.txt` 文件包含了关于设备标识符的使用信息。

## 7.4.6 select

虽然 `select()` 没有实现，但这里将描述它的操作，因为该函数对字符设备特别有用。作为一个示例，我们将采用 ATI 总线鼠标驱动程序的 `select()` 实现：

```c
static int mouse_select(struct inode *inode, struct file *file,
                        int sel_type, select_table *wait) {
    if (sel_type != SEL_IN) return 0;
    if (mouse.ready) return 1;
    select_wait(&mouse.wait, wait);
    return 0;
}
```

`select` 函数的任务是检查是否可以从设备读取数据（`sel_type == SEL_IN`）或向其写入（`SEL_OUT`）。`SEL_EX` 也可以用于等待异常条件的发生。由于这几乎所有的复杂性都由虚拟文件系统（`VFS`）处理，`select` 函数的任务描述非常简单。如果参数 `wait` 为 `NULL`，则将查询设备。如果对于相关设备已就绪，`select(2)` 将返回 1，否则返回 0。如果 `wait` 不为 `NULL`，则进程必须阻塞直到设备可用。然而，并没有使用 `sleep_on()`；而是由以下函数处理任务：

```c
void select_wait(struct wait_queue **wait_address, select_table *p)
```

该函数期望一个等待队列和传递给 `select` 函数的最后一个参数。如果该参数为 `NULL`，`select_wait()` 立即返回，可以跳过查询，如上例所示提供函数结构。

如果设备可用（通常由中断指示），进程将通过 `wake_up_interruptible(wait_address)` 被唤醒。这通过驱动程序的鼠标中断来指示。

```c
void mouse_interrupt(int unused) {
    if (dx != 0 || dy != 0 || buttons != mouse.latch_buttons) {
        mouse.latch_buttons = buttons;
        mouse.dx += dx;
        mouse.dy += dy;
        mouse.ready = 1;
        wake_up_interruptible(&mouse.wait);
    }
}
```
