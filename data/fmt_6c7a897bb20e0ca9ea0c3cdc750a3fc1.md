
发送此调用时，进程的原始信号掩码被重置。BSD 中存在类似的调用：`sigpause`。它在 C 库中通过简单的 `sigsuspend` 实现。

## 5.4.2.1 alarm 系统调用

进程可以请求系统在指定时间发送一个信号。这使用了 `alarm` 系统调用。该调用的形式为：

```c
#include <unistd.h>

long alarm (long seconds);
```

参数 `seconds` 表示系统向进程发送 `SIGALRM` 的周期。系统调用的返回值表示请求报警前的剩余时间。调用 `alarm` 零对应取消报警。该系统调用通常用于控制捕捉键盘输入时的延迟。

`TempoAlarm.c`

```c
#include <stdio.h>
#include <signal.h>
#include <unistd.h>

void alarm_hdl (int sig);

int my_time;

int main ()
{
    signal (SIGALRM, alarm_hdl);
    while (1) {
        my_time = 8;
        printf("Press 'Enter' or the program will stop in 10 seconds\n");
        alarm(2);
        getchar();
        alarm(0);
    }
}

void alarm_hdl(int sig) {
    signal (SIGALRM, alarm_hdl);
    alarm(2);
    if (my_time) {
        printf("there are %d seconds remaining\n", my_time);
        my_time = 2;
    } else {
        printf("Too late, end of the program\n");
        exit(1);
    }
}
```

执行后，获得如下结果：

```bash
$ ./TempoAlarm
Press 'Enter' or the program will stop in 10 seconds
There are 8 seconds remaining
There are 6 seconds remaining
- Hit 'Enter'
Press 'Enter' or the program will stop in 10 seconds
There are 8 seconds remaining
There are 6 seconds remaining
There are 4 seconds remaining
There are 2 seconds remaining
Too late, the program has terminated
bash$
```

# 补充系统调用

此程序在检测到 `[Enter]` 键被按下时循环。每两秒显示一次程序结束前的时间。如果用户在 10 秒内按键，计时器清零并重启循环，否则程序终止。

`alarm` 指定的时间是进程处理信号的最小时间。事实上，进程只有在调度器赋予其处理器访问权限时才会处理信号。因此，处理信号没有最大限制。

## 5.4.2.2 精细的时间控制

上述系统调用具有局限性，因为它不允许自动控制报警。时间控制仅与实际时间有关，而相对于进程执行定时来控制报警可能更有意义。BSD 和 V 系统引入两个新的系统调用解决了这些问题，允许在不同的时间范围内自动控制周期报警。系统允许每个进程根据三个不同的时间参考控制三个周期报警。当一个报警过期时，信号会被发送给进程并触发报警。

报警由下表描述的三个计数器表示：

| 选项 | 含义 |
| --- | --- |
| `ITIM_REAL` | 按实际时间递减的计数器：过期后向进程发送 `SIGALARM` |
| `ITIM_VIRTUAL` | 进程执行时递减的计数器：过期后向进程发送 `SIGVTALRM` |
| `ITIM_PROF` | 进程执行及系统代表进程执行时递减的计数器：过期后向进程发送 `SIGPROF` |

这些调用形式如下：

```c
#include <sys/time.h>

int gettimer (int which, struct itimerval *value);
int setitimer (int which, const struct itimerval *value, struct itimerval *oldvalue);
```

它们分别用于接收或发布与报警相关的信息。调用的第一个参数指示涉及哪个计数器。第二个

## 信号

参数指向一个结构，该结构包含下次闹器的值和计数器的当前值：这些每个字段都由 `timeval` 结构描述，该结构描述于第 4 章第 4.2.3 节。

`itimerval` 结构如下：

| 类型 | 字段 | 描述 |
|---|---|--|
| `struct timeval` | `it_timeval` | 下次闹钟 |
| `struct timeval` | `it_value` | 当前计数器值 |

计数器从 `it_value` 递减到零；产生一个信号，然后 `it_value` 字段被重新初始化为 `it_interval` 的值，并重新倒计时。如果闹钟达到零，则停止；该值在 `it_value` 被设置为零，或者计数器耗尽且 `it_interval` 的值为空时到达。

在发生错误时，系统调用返回 -1，变量 `errno` 包含以下值：

| 选项 | 含义 |
|---|--|
| `EFAULT` | `value` 或 `ovalue` 包含无效地址 |
| `EINVAL` | 系统调用的第一个参数不是以下值之一：`ITIMER_REAL`、`ITIMER_VIRTUAL` 或 `ITIMER_PROF` |

闹钟的精度与系统时钟的精度相关（当前为 10ms）。因此，闹钟可能会在超过真实时间点稍后过期。如果进程处于活动状态，信号的传递将立即执行，或者根据系统负载稍有延迟。

在某些情况下，系统负载非常重要，因为信号的产生和接收在系统中是分离的，可能导致周期性闹钟 `ITIMER_REAL` 在进程能够注册一次过期之前已经过期了两次：因此会产生一个信号，而进程只考虑其中一个。

`alarm` 系统调用利用计数器 `ITIMER_REAL`：因此，有必要避免将此系统调用与 `setitimer` 调用一起使用。

为了说明这些系统调用，使用 `setitimer` 调用重写了上一个示例：

`TempoTimer.c`

```c
#include <stdio.h>
#include <signal.h>
#include <sys/time.h>
#include <unistd.h>

void alarm_hdl(int sig);

int my_time;
int main () {
    struct itimerval my_alarm;
    my_alarm.it_interval.tv_sec = 2;
    my_alarm.it_interval.tv_usec = 0;
    signal(SIGALRM, alarm_hdl);
    while (1) {
        my_time = 8;
        printf("press Enter or the program will exit\n");
        printf("in 10 seconds\n");
        my_alarm.it_interval.tv_sec = 2;
        my_alarm.it_interval.tv_usec = 0;
        setitimer(ITIMER_REAL, &my_alarm, NULL);
        getchar();
        my_alarm.it_interval.tv_sec = 2;
        my_alarm.it_interval.tv_usec = 0;
        setitimer(ITIMER_REAL, &my_alarm, NULL);
    }
}

void alarm_hdl(int sig) {
    signal(SIGALRM, alarm_hdl);
    if (my_time) {
        printf("you have %d seconds \n", my_time);
        temps -= 2;
    } else {
        printf("Too late, end of the program\n");
        exit(1);
    }
}
```
