
通过。当时间到时，时钟会向进程发送一个信号 `SIGALRM`。除非进程为 `SIGALRM` 安装了处理程序，否则该信号将杀死进程。因此，`sleep` 函数由这三个步骤组成：

- 1. 为 `SIGALRM` 安装处理程序。
- 2. 调用 `alarm(num_seconds)`。
- 3. 调用 `pause`。

`pause` 系统调用挂起进程，直到信号到达（任何信号，而不只是 `SIGALRM`）。我们将这些思路结合起来编写以下代码：

```c
/* sleep1.c
 * purpose 显示 sleep 如何工作
 * usage sleep1
 * outline 设置了处理程序，设置闹钟，暂停，然后返回
 */
#include <stdio.h>
#include <signal.h>
// #define SHHHH

main()
{
    void wakeup(int) {
        printf("about sleep for 4 seconds\n"); /* catch it */
        signal(SIGALRM, wakeup);               /* set clock */
        alarm(4);                              /* freeze here */
        pause();                               /* free here   */
        printf("Morning is so soon?\n");     /* back to work */
    }

    void wakeup(int signum) {
        #ifdef SHHHH
        printf("Alarm received from kernel\n");
        #endif
    }
}
```

我们调用 `signal` 为 `SIGALRM` 安装一个处理函数，然后调用 `alarm` 设置一个四秒的定时器，最后调用 `pause` 等待闹钟响铃。

`pause` 的目的是挂起进程，直到信号被处理。当闹钟定时器经过四秒后，内核向进程发送 `SIGALRM`，导致控制权从 `pause` 所在跳转到信号处理程序。处理程序中的代码被执行，然后返回返回。信号被处理后，`pause` 返回，进程继续执行。图 7.8 总结了 `pause` 的动作。

![](img/99837708330d437de319a559cfa6cda7_229_0.png)

以下是关于 `alarm` 和 `pause` 的细节：

| 目的 | 设置闹钟定时器以发送信号 |
| --- | --- |
| 包含 | `#include <unistd.h>` |
| 用法 | `unsigned old = alarm(unsigned seconds)` |
| 参数 | `seconds` 等待多久 |
| 返回 | 错误时返回 -1；定时器上剩余的时间 |

`alarm` 将调用进程的闹钟定时器设置为在几秒后过期。当该时间通过时，内核向进程发送 `SIGALRM`。如果定时器已经设置，`alarm` 返回剩余的秒数。（注意：调用 `alarm(0)` 关闭闹钟。）

| 目的 | 等待信号 |
| --- | --- |
| 包含 | `#include <unistd.h>` |
| 用法 | `result = pause()` |
| 参数 | 无参数 |
| 返回 | 始终返回 -1 |

# 第 7 章 事件驱动编程：编写视频游戏

`pause` 挂起调用进程，直到接收到信号。如果调用进程被信号终止，`pause` 不返回。如果调用进程用处理程序捕获了信号，则当控制权从处理程序返回时，`pause` 返回。在这种情况下，`errno` 被设置为 `EINTR`。

## 7.5.3 调度未来的动作

使用时间的另一种方法是为未来的某个时间调度动作，并在期间做其他事情。在未来调度动作是简单的，通过调用 `alarm` 设置定时器，然后继续做其他事情。当定时器达到零时，将发送信号，处理程序将被调用。

## 7.6 使用时间编程 II：间隔定时器

`sleep` 和 `alarm` 自早期以来就存在于 Unix 中。它们提供一秒的精度，对于许多应用来说太粗糙了。后来添加了一个更强大、更全面的定时器系统。这个新系统使用名为“间隔定时器”（interval timer）的概念，具有更高的分辨率，而且每个进程拥不是一个，而是三个独立的定时器。不仅如此，这些定时器中的每一个都有两个设置：单次闹钟设置和重复定时器。`alarm` 和 `sleep` 仍然被支持，并且对于许多应用已经足够了。这种思想如图 7.9 所示。

![](img/99837708330d437de319a559cfa6cda7_230.png)

每个进程都有三个定时器。每个定时器都有两个设置：直到第一次闹钟的时间和重复闹钟之间的间隔。

可以使用这个新系统来添加延迟和调度事件。

### 7.6.1 添加更细的延迟：usleep

要为程序添加更细的延迟，使用 `usleep`：

```
usleep (n)
```

`usleep (n)` 挂起当前进程 `n` 微秒或直到一个未忽略的信号到达。

### 7.6.2 三种定时器：实时、进程、性能

进程可以测量三种时间。考虑一个启动 30 秒后结束的程序。在分时系统中，程序并没有一直运行；其他程序也在交替使用处理器。图 7.10 显示了在这 30 秒内发生了什么：

![](img/99837708330d437de319a559cfa6cda7_231.png)

图 7.10

时间去哪了？图显示从 0 到 5 秒，进程在用户模式运行；然后从 5 到 15 秒进入休眠；直到 20 秒进入内核模式；然后回到休眠。从开始到结束的 30 秒，程序使用了 10 秒的用户时间和 5 秒的系统时间。显示了三种时间类型：实时、用户、系统。内核提供了定时器来测量这些。这些定时器的名称为：

- `ITIMER_REAL`：此定时器在实时内计时，无论进程在用户模式还是内核模式下使用多少 CPU 时间。它过期时，发送 `SIGALRM`。
- `ITIMER_VIRTUAL`：此定时器像时钟一样，只在进程处于用户模式运行时计时。虚拟定时器上的三十秒比实时更长。虚拟定时器过期时发送 `SIGALRM`。
- `ITIMER_PROF`：此定时器当进程在用户模式运行以及该进程执行系统调用时计数。它过期时，发送 `SIGPROF`。

两个间隔：初始和重复

医生给你一些药并说：“从现在开始吃一颗，然后每四小时吃一次。”你需要设置一个定时器在一小时后触发，每当它触发时，将其重置为四小时。每个间隔定时器都有两个设置：初始值和重复间隔。在间隔定时器使用的结构体中，初始间隔被称为 `it_value`，重复量被称为 `it_interval`。如果你不需要重复功能，将 `it_interval` 设置为0。要关闭两个定时器，将 `it_value` 设置为0。

### 7.6.4 使用间隔定时器编程

使用 `alarm` 编程很容易；你只需要传递秒数。间隔编程更复杂；你必须选择一种时间类型，然后决定初始间隔和重复间隔。此外，你必须在结构体中设置值。例如，为了使用间隔定时器提醒服用上段提到的药物，将 `it_value` 设置为小时，将 `it_interval` 设置为四小时，然后通过调用 `setitimer` 将该结构传递给定时器。读取定时器设置，使用 `getitimer`。该概念如图 7.11 所示。

![](img/99837708330d437de319a559cfa6cda7_232.png)

图 7.11

读取和写入定时器设置。

### 间隔定时器示例：ticker_demo.c

以下程序 `ticker_demo.c` 演示了间隔定时器的用法：

```c
/* ticker_demo.c
 * 演示使用间隔定时器产生定期
 * 信号，这些信号会被捕获并用于倒计时
 */
```

```c
int main() {
    void countdown(int);
    signal(SIGALRM, countdown);
    if (set_ticker(500) == -1)
        perror("set_ticker");
    else {
        while(1)
            pause();
    }
    return 0;
}

void countdown(int signum) {
    static int num = 10;
    printf("%d ..n", num--);
    fflush(stdout);
    if (num < 0) {
        printf("DONE!\n");
        exit(0);
    }
}
```

> /* 来自 set_ticker.c
 * set_ticker(毫秒数)
 * 安排间隔定时器定期间隔发出 SIGALRM
 * 错误时返回 -1，成功返回 0
 * 参数为毫秒，转换为整数秒和微秒
