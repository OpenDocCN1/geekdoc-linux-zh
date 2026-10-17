
## 112 信号

由于信号是递归的，此处没有必要重复由于接收信号而产生的闹钟。

## 5.4.3 信号 SIGCHLD

当一个进程终止时，它将保持在 ZOMBIE（僵尸）状态，直到其父进程通过 `wait` 或 `wait4` 系统调用之一感知到它的终止。系统会向父进程警告一个子进程已终止，发送 `SIGCHLD` 信号。当父进程执行其中一个系统调用时，该信号会被忽略。

在 Linux 默认情况下，信号 `SIGCHLD` 被设置为 `SIGIGN`，系统不会警告父进程子进程已终止；系统会自动感知子进程的终止，后者从进程表中消失。

在编写客户端-服务器应用程序时，识别 `SIGCHLD` 信号非常重要。通常，服务器主进程识别请求的到达并建立从服务器，对其进行回复。当请求完成时，从服务器终止，服务器主进程通过读取其终止码来检查是否有问题。如果存在 ZOMBIE 状态进程导致进程表饱和的风险，则有必要读取终止状态。以下示例显示了管理 `SIGCHLD` 信号的方法。

## WaitChild.c

```
#include <stdio.h>

#include <unistd.h>

#include <signal.h>

#include <sys/types.h>

#include <sys/wait.h>

void deroute(int sig)

{

    printf("Termination of the child process %d\n", wait (NULL));

}

int main(void)

{

    struct sigaction action;

    int i;

    action.sa_handler = deroute

    action.sa_flags = 0;

    action.sa_mask = 0;

```

## 信号的通用概述

在某些情况下，系统负载非常重要，因为信号的产生和接收在系统中是分离的，可能导致周期性闹钟 `ITIMER_REAL` 在进程能够注册一次过期之前已经过期了两次：因此会产生一个信号，而进程只考虑其中一个。

`alarm` 系统调用利用计数器 `ITIMER_REAL`：因此，有必要避免将此系统调用与 `setitimer` 调用一起使用。

为了说明这些系统调用，使用 `setitimer` 调用重写了上一个示例：

## TempoTimer.c

```
#include <stdio.h>
#include <signal.h>
#include <sys/time.h>
#include <unistd.h>
```

```
void alarm_hdl(int sig);
```

```
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
```

```
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

## 信号

参数指向一个结构，该结构包含下次闹器的值和计数器的当前值：这些每个字段都由 `timeval` 结构描述，该结构描述于第 4 章第 4.2.3 节。

`itimerval` 结构如下：

| 类型 | 字段 | 描述 |
|---|---|---|
| struct timeval | it_timeval | 下次闹钟 |
| struct timeval | it_value | 当前计数器值 |

计数器从 `it_value` 递减到零；产生一个信号，然后 `it_value` 字段被重新初始化为 `it_interval` 的值，并重新倒计时。如果闹钟达到零，则停止；该值在 `it_value` 被设置为零，或者计数器耗尽且 `it_interval` 的值为空时到达。

在发生错误时，系统调用返回 -1，变量 `errno` 包含以下值：

| 选项 | 含义 |
|---|---|
| EFAULT | value 或 ovalue 包含无效地址 |
| EINVAL | 系统调用的第一个参数不是以下值之一：ITIMER_REAL、ITIMER_VIRTUAL 或 ITIMER_PROF |

闹钟的精度与系统时钟的精度相关（当前为 10ms）。因此，闹钟可能会在超过真实时间点稍后过期。如果进程处于活动状态，信号的传递将立即执行，或者根据系统负载稍有延迟。

在某些情况下，系统负载非常重要，因为信号的产生和接收在系统中是分离的，可能导致周期性闹钟 `ITIMER_REAL` 在进程能够注册一次过期之前已经过期了两次：因此会产生一个信号，而进程只考虑其中一个。

`alarm` 系统调用利用计数器 `ITIMER_REAL`：因此，有必要避免将此系统调用与 `setitimer` 调用一起使用。

为了说明这些系统调用，使用 `setitimer` 调用重写了上一个示例：

## TempoTimer.c

```
#include <stdio.h>
#include <signal.h>
#include <sys/time.h>
#include <unistd.h>
```

```
void alarm_hdl(int sig);
```

```
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
```

```
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
