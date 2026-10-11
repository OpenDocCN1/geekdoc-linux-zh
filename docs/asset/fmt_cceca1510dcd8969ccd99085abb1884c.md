
或者如下所示动态定义：

```c
wait_queue_head my_queue;
init_wait_queue_head(&my_queue);
```

当进程睡眠时，它是预期某些条件在未来变为真。正如之前提到的，任何睡眠的进程都必须检查以确保在唤醒时它所等待的条件真的是真的。

在 Linux 内核中睡眠最简单的方法是称为 `wait_event` 的宏（带有几个变体）；它结合了睡眠的细节处理和对进程等待条件的检查。`wait_event` 的形式有：

```
wait_event(queue, condition)
wait_event_interruptible(queue, condition)
wait_event_timeout(queue, condition, timeout)
wait_event_interruptible_timeout(queue, condition, timeout)
```

在上述所有形式中，`queue` 是要使用的等待队列头。`condition` 是一个任意布尔表达式，宏在睡眠前后都会对其进行评估；直到该条件评估为真值，进程将继续睡眠。如果你使用 `wait_event`，你的进程将进入不可中断睡眠。首选的替代方案是 `wait_event_interruptible`，它可以被信号中断。

# 第 6 章

当然，画面的另一半是唤醒。必须有一个执行线程（另一个进程或中断处理程序）来为你执行唤醒操作，因为你的进程显然处于睡眠状态。唤醒睡眠进程的基本函数称为 `wake_up`。它有几种形式（但现在只介绍其中两种）：

```c
void wake_up(wait_queue_head_t *queue); /* 唤醒所有在给定队列上等待的进程 */
void wake_up_interruptible(wait_queue_head_t *queue); /* 仅限于处于可中断睡眠状态的进程 */
```

你将开发一个内核模块，该模块会导致进程进入睡眠，然后通过中断唤醒它。你可以通过下图检查驱动程序的行为。当用户应用程序尝试从设备进行读取（系统调用）时，进程将进入睡眠。每当我们按下或释放 SW5 按钮时，生成的中断将唤醒该进程，驱动的读取回调函数会将设置的中断类型（按下或释放）发送到用户空间。一旦你退出用户应用程序，你可以从一个文件中读取所有生成的的中。

![](img/739a35b59067f8a55eff80a58765146f_252_0.png)

## 在平台驱动程序中处理中断

现在描述驱动的主要代码部分：

### 1. 包含头文件：

```c
#include <linux/wait.h> /* DECLARE_QUEUE_HEAD() wait_event_interruptible() wake_up() */
#include <linux/sched.h>
```

### 2. 声明等待队列：

```c
static DECLARE_QUEUE_HEAD(hello_keys_wait);
```

### 3. 在内核回调函数中让进程睡眠，并将其放入等待队列等待特定事件。设置唤醒前要评估的条件：

```c
ret = wait_event_interruptible(hello_keys_wait, buf_wr != buf_rd);
```

### 4. 在中断服务程序 (ISR)中获取 P/R 值：

```c
val = gpio_get_value(gpio_nb);
pr_info("Button state: 0x%08X\n", val);
if (val == 0)
    hello_keys_buf[buf_wr++] = 'P'; /* 读取并增加 buf_wr */
if (val == 0x000020)
    hello_keys_buf[buf_wr++] = 'R';
```

### 5. ISR 在读取按钮状态后唤醒进程：

```c
wake_up(&hello_keys_wait);
```

### 6. 一旦进程被唤醒，驱动的读取回调函数会将“P”或“R”按钮状态发送到用户应用程序：

```c
char ch[2];
ch[0] = hello_keys_buf[buf_rd];
ch[1] = '\0';
ret = copy_to_user(buff, ch, 2);
if (ret)
    return -EFAULT;
buf_rd++;
if (buf_rd >= MAX_KEY_STATES)
    buf_rd = 0;
return 2;
```

### 列表 6-2: int_key_wait.c
