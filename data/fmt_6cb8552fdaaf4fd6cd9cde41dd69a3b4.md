
Unix 中的进程拥有几种不同的机制来相互通信。其中之一是发送*信号*。当通过 Ctrl-C 或 `kill` 命令终止一个进程时，该进程就接收到了一个信号。要解释什么是信号，我们需要稍微扩展一下任务的概念。我们将任务状态段描述为内存区域，在发生任务切换时，寄存器会被保存在这里。任务状态段由硬件维护。但这只是 Linux 为每个进程维护的上下文信息的*一部分*。有一个名为 `struct task_struct` 的结构体，定义在 `/usr/src/linux/include/linux/sched.h` 中，它保存了 Linux 关于进程所需的所有信息。当设备驱动程序代表某个进程执行时，这些信息是可用的，因为内核内存中有一个名为 `current` 的全局变量，其值始终是当前进程的任务结构体。例如，在 `/dev/cq` 的驱动程序中，从 `cq_write()` 访问这个变量是有意义的，但从 `cq_timer_handler()` 访问则不是。`struct task_struct` 的一个组件是 `tss`，即硬件的任务状态段。`pid` 组件是进程 ID 号，运行 `ps` 时会显示出来。在从命令行终止作业时需要它。`struct task_struct` 的另一个组件是 `signal`。当前该组件被定义为整数数组。数组中每个整数的每一位都可以携带一个信号。数组中有两个 32 位整数，因此 Linux 配置为最多支持 64 个信号。无论这些不同信号之间的细微差别是什么，对于设备驱动程序来说，接收信号只意味着一件事：是时候退出了。

### 无法被终止的驱动程序

`signal_pending()` 调用检查进程的 `signal` 组件是否有非零位。确保执行此检查并在发现此类位时继续退出是设备驱动程序编写者的责任。未能做到这一点会导致驱动程序无法被终止。这是一个容易犯且严重的错误。Linux 中的多任务处理有时被称为*协作式多任务处理*。在内核中作为特权任务执行的用户任务是不可抢占的。这样的具有内核权限的任务（例如 `cq_write()`）被期望自愿让出处理器。如果它不这样做，调度器不会强制其这样做。为了履行这一职责，驱动程序必须包含如下的代码：

```c
if (signal_pending(current))
    return value;
```

在代码中会频繁遇到的位置插入上述代码，以便等待驱动程序在执行时到达这些位置不会造成过度的延迟。

为了确保驱动程序响应信号，还有一个细节需要修复。

### 11.3.7 进程的状态

`struct task_struct` 的一个非常重要组件是 `state`。其最重要的值在 `/usr/src/linux/include/linux/sched.h` 中分配：

```c
#define TASK_RUNNING 0
#define TASK_INTERRUPTIBLE 1
#define TASK_UNINTERRUPTIBLE 2
#define TASK_ZOMBIE 4
#define TASK_STOPPED 8
```

位于运行队列上的任务，即那些目前正在轮流使用处理器的任务，其 `state` 组件的值为 `TASK_RUNNING`。当一个任务将自己放入等待队列时，`state` 可以取 `TASK_INTERRUPTIBLE` 或 `TASK_UNINTERRUPTIBLE` 作为值。而且这有很大的区别。

尽管我们可能会合理地认为这与中断有关，但实际上不是。这与信号有关。

如果 `state` 的值为 `TASK_UNINTERRUPTIBLE`，那么其 `signal` 组件不会因为 Ctrl-C 或 `kill` 而改变。不幸的是，这是 `sleep_on()` 函数分配给 `state` 的值。幸运的是，有一个相关的函数叫做 `sleep_on_interruptible()`，它将 `state` 分配为 `TASK_INTERRUPTIBLE`。因此，在程序 11.5 中，对 `sleep_on()` 和 `wake_up()` 的调用需要被它们可中断的对应版本替换。否则，我们将面临与省略 `signal_pending()` 检查时相同的问题。两个 `sleep_on` 函数的定义位于 `/usr/src/linux/kernel/sched.c` 中，`wake_up()` 的主要部分也在那里。两个 `wake_up` 宏定义在 `/usr/src/linux/include/linux/sched.h` 中。

在 11.4 节中的数字化仪驱动程序中，必须查阅 `wake_up_interruptible()` 宏定义以找到实际的函数调用，因为 NASM 不使用 gcc 预处理器。

摩尔斯电码扬声器驱动程序的主要特性现在已经就位，因此我们可以接下来进行有趣的部分。

### 11.3.8 摩尔斯电码计时

点和划的计时是一门艺术，而不是一门科学。如果听起来对摩尔斯电码使用者来说是正确的，那么摩尔斯电码驱动程序的计时就是好的。该驱动程序中的时间值基于以下规则：

- 所有时间值都基于 `cq_area` 中 `wholenote` 组件的持续时间，其以百分之一秒或 `jiffies` 给出。
- 一个划是 `wholenote` 的四分之一。
- 一个点是 `wholenote` 的十六分之一。
- 字母中点和划之间的静默间隔是 `wholenote` 的八分之一。
- 字母之间的静默间隔是 `wholenote` 的八分之二。
- 单词之间的静默间隔是 `wholenote` 的八分之三。
- 摩尔斯电码中未包含的字符会得到四分之一全音符的静默间隔。

### 11.3.9 汇编语言扬声器代码

为了打开和关闭扬声器，使用了程序 11.6 中显示的两个小型汇编例程。虽然驱动程序的大部分是用 C 编写的，但这通常也是可能的。很多时候，小型例程用汇编语言编写，其余部分用高级语言编写。

如果包含程序 11.6 的文件名为 `speak.asm`，则可以使用 NASM 进行汇编：

```bash
linuxbox$ nasm -f elf speak.asm
```

`-f elf` 开关决定了生成的目标代码文件（名为 `speak.o`）的格式。它应该存储在 `/usr/src/linux/drivers/char` 中。

#### 程序 11.6

```nasm
global speaker_on
global speaker_off
extern cq_area
SYSP    equ 61h ; System port for controlling speaker feed
DIVREG  equ 42h ; Port for timer divisor

speaker_off:
        IN AL, [SYSP]
        AND AL, 0FCH
        OUT [SYSP], AL
        MOV EAX, [cq_area]
        OR EAX, 4
        MOV [cq_area], EAX
        RET

speaker_on:
        MOV EAX, [cq_area + 4]
; timervid is offset by 4
        OUT [DIVREG], AL
        SHR EAX, 8
        OUT [DIVREG], AL
        IN AL, [SYSP]
        OR AL, 3
        OUT [SYSP], AL
        MOV EAX, [cq_area]
        AND EAX, 0FFFFFFFBh
        MOV [cq_area], EAX
        RET
```

### 11.3.10 C 语言驱动程序代码

#### 程序 11.7

```c
#include <linux/errno.h> /* Need this for ENODEV, etc. */
#include <linux/kernel.h> /* Need this for printk() */
#include <linux/major.h> /* Need this for CQ_MAJOR */
#include <linux/sched.h> /* Need this for sleeping and waking */
#include <asm/uaccess.h> /* Need this for copy_from_user() */

#include <linux/cq.h> /* Note the cq file. */

void cq_timer_handler(unsigned long);
static void cq_set_pitch(unsigned long);
static void cq_set_tempo(unsigned long);

void speaker_on(void);
```
