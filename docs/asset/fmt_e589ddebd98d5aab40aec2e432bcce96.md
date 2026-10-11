
`CQ_EXIST`位仅表示驱动程序已安装。`CQ_BUSY`位用于防止多个进程同时使用设备。这在调用`open()`时进行检查，阻塞其他进程。

# 11.3.5 等待队列

等待队列的设计允许进程以某种方式挂起，以便在需要时可以被重新激活。例如，生产者可以在产生剩余时挂起操作，并在供应耗尽时由消费者重新激活。

进程可以通过调用`sleep_on()`来挂起操作。在我们的驱动中，生产者`cq_write()`填充`cq_area.buffer`（扬声器的文本缓冲区），并在完成后立即调用`sleep_on()`。定时器处理程序`cq_timer_handler`通过发送数据到扬声器使用了一个缓冲区加载，它可以调用`wake_up()`函数让`cq_write()`重新填充缓冲区。

```c
cq.write(<File>, u, n)
{
/* This program puts itself to sleep
   after it fills device memory. */
  int k, total = 0;
while(total < n)
{
  k = CQ_BUFFER_SIZE;
  copy_from_user(cq.area.buffer, k, u);
  add_timer(&cq.timer);/* Start timer handler */
  total = total + k;
  sleep_on(&cq.area.wait_q));
}
cq.timer_handler(unsigned int x)
```

```c
/* This program wakes up the user
   process when device memory is empty. */
  <Turn speaker on or off>
if(<Character dense)){
  cq.area.buffer_offset = cq.area.buffer_offset + 1;
  if(cq.area.buffer_offset == cq.area.buffer_end){
    cq.area.buffer_offset = 0;
    wake_up(&cq.area.wait_q);
    return; /* No future scheduling done here! */
  }
}
add_timer(&cq.timer);/* Continue calling timer handler */
```

## 程序 11.5

当前正在轮流使用处理器。每当运行队列上的另一个进程轮到它使用处理器的机会时，当然必须进行任务切换。`sleep_on()`和`wake_up()`必须在一个类型为`struct wait_queue **``的参数上被调用，这是一个指向等待队列结构体指针的指针。虽然这听起来很糟糕，但要设置这样一个东西其实并不难。`struct wait_queue`的定义在`/usr/src/linux/include/linux/wait.h`中。

## 章节 11.3. 摩斯密码扬声器驱动

但实际上，要使用等待队列，我们不需要知道任何关于间隔的知识。只要我们在传递给`sleep_on()`的相同指针上调用`wake_up()`，一切就绪了。我们的`struct cq_struct`中的`wait_q`组件在`cq_write()`中使用了`sleep_on()`，在`cq_timer_handler()`中使用了`wake_up()`，那么等待队列双指针必须位于这两个函数都能访问的地方。这是另一个设备内存发挥作用的例子。这就是为什么等待队列指针位于那里。一个指向该位置的指针提供了我们需要的参数：`&cq.area.wait_q`。

程序 11.5 显示了`sleep_on()`和`wake_up()`调用是如何协同工作的。在 11.5 中，`cq_write()`在填充内核内存中的设备缓冲区后会立即调用`sleep_on()`。当`cq_timer_handle()`清空设备缓冲区时，会唤醒睡眠中的`cq_write()`进程。

现在我们可以编写必要的任务切换，我们有能力编写一个运行良好的驱动程序。遗憾的是，到为止概述的驱动程序有一个致命缺陷。它不会对所谓的信号信号做出响应。

## 11.3.6 信号

Unix 中的进程有几种不同的机制可以相互通信。其中之一就是发送信号。当一个进程被 Ctrl-C 或`kill`命令杀死时，该进程就接收到了信号。为了解释什么是信号，我们需要扩展“任务”的概念。我们已经描述过任务状态段（task state segment）是在发生任务切换时保存寄存器的内存区域。任务状态段由硬件维护。但它也是 Linux 为每个进程维护的上下文信息的一部分。在`/src/linux/include/sched.h`中定义了一个`struct task_struct`结构体，它包含了 Linux 对进程所需的所有信息。当驱动程序代表进程执行时，这些信息对驱动程序是的，因为内核内存中有一个全局变量，其值始终是当前进程的任务结构。例如，在`/dev/cq`的驱动程序中，从`cq_write()`访问此变量是合理的，但从`cq_timer_handle()`则不是。`struct task_struct`的组件之一是硬件的任务状态段。该组件是运行`ps`时显示的进程 ID（PID） own。在从命令行杀死作业时需要它。`struct task_struct`的另一个组件是`signal`。该组件被定义为整数数组。数组中的每个位都可以携带一个信号。通过数组中的两个位宽整数，Linux 配置了最多 64 个信号。无论这些不同信号之间有什么种细微差别，对于设备驱动程序来说，接收到信号只意味着一件事：该停止了。

## 无法杀死的驱动程序

`signal_pending()`调用检查进程信号组件是否存在非零位。设备驱动程序编写者的责任是确保做到这一点，并且如果发现此类位，则继续退出。未能这样做会导致设备无法被杀死。这是一个很容易犯的错误，而且非常严重。Linux 中的多任务处理有时被称为协作式多任务。如`cq_write()`这样以内核权限执行的用户任务预计会自愿让出处理器。如果它们不这样做，调度程序器就不会强制它们这样做。为了履行这一责任，驱动程序必须包含如下所示的代码：

```c
signal_pending(current)
return value;
```

在代码中经常遇到的点包含这些代码，这样等待设备驱动程序在执行到达这些点时就不会引起不必要的延迟。

再修复一个细节，以确保驱动程序对信号做出响应。

## 11.3.7 进程的状态

`struct task_struct`中一个非常重要的组件是`state`。它最重要的值分配在`/usr/src/linux/include/linux/sched.h`中。

```c
#define TASK_RUNNING 0
#define TASK_INTERRUPTIBLE 1
#define TASK_UNINTERRUPTIBLE 2
#define TASK_ZOMBIE 4
#define TASK_STOPPED 8
```

位于运行队列上的任务（即当前正在使用处理器的任务）其`state`组件的值为`TASK_RUNNING`。当任务将自己放入等待队列时，`state`可能是`TASK_INTERRUPTIBLE`或`TASK_UNINTERRUPTIBLE`。

## 11.3.10 C 语言驱动代码

```c
#include <linux/errno.h>    /* 需要 ENODEV 等    */
#include <linux/kernel.h> /* 需要 printk() */
#include <linux/major.h>     /* 需要 CQ_MAJOR */
#include <linux/sched.h>      /* 需要睡眠和唤醒 */
#include <asm/uaccess.h>      /* 需要 copy_from_user() */
```

```c
#include <linux/cq.h>       /*注意 cq 文件。 */
```

```c
void cq_timer_handler(unsigned long);
static void cq_set_pitch(unsigned long);
static void cq_set_tempo(unsigned long);
```

```c
void speaker_on(void);
void speaker_off(void);
```

```c
char * morse_code[40] = {
    "-\-\
```

> /* 空字符串，紧随其后是 26 个字母代码，
> 后面是 10 个数字代码，最后是逗号、
> 句点和问号。 */

```c
```
