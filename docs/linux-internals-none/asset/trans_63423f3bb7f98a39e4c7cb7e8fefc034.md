

警报和/或中断频率通过 `ioctl(2)` 调用编程到实时时钟（RTC）中，如 `include/linux/mc146818rtc.h` 中所示（参见下方的数据结构）。

以下用户程序（随 RedHat 发行版的内核文档提供）最好地说明了如何使用 ioctl 控制实时时钟：

```c
/*
 * Real Time Clock Driver Test/Example Program
 *
 * Compile with:
 * gcc -s -Wall -Wstrict-prototypes rcttest.c -o rcttest
 *
 * Copyright (C) 1996, Paul Gortmaker.
 *
 * Released under the GNU General Public License, version 2,
 * included herein by reference.
 */

#include <stdio.h>
#include <linux/mc146818rtc.h>
#include <sys/ioctl.h>
#include <sys/time.h>
#include <sys/types.h>
#include <fcntl.h>
#include <unistd.h>
#include <errno.h>

void main(void) {

int i, fd, retval, irqcount = 0;
unsigned long tmp, data;
struct rtc_time rtc_tm;

fd = open ("/dev/rtc", O_RDONLY);

if (fd == -1) {
    perror("/dev/rtc");
    exit(errno);
}

fprintf(stderr, "\n\t\t\tRTC Driver Test Example.\n\n");

/* Turn on update interrupts (one per second) */
retval = ioctl(fd, RTC_UIE_ON, 0);
if (retval == -1) {
    perror("ioctl");
    exit(errno);
}

fprintf(stderr, "Counting 5 update (1/sec) interrupts from reading /dev/rtc:");
fflush(stderr);
for (i=1; i<6; i++) {
    /* This read will block */
    retval = read(fd, &data, sizeof(unsigned long));
    if (retval == -1) {
        perror("read");
        exit(errno);
    }
    fprintf(stderr, " %d",i);
    fflush(stderr);
    irqcount++;
}
fprintf(stderr, "\nAgain, from using select(2) on /dev/rtc:");
fflush(stderr);
for (i=1; i<6; i++) {
    struct timeval tv = {5, 0}; /* 5 second timeout on select */
    fd_set readfds;
    FD_ZERO(&readfds);
    FD_SET(fd, &readfds);
    /* The select will wait until an RTC interrupt happens. */
    retval = select(fd+1, &readfds, NULL, NULL, &tv);
    if (retval == -1) {
        perror("select");
        exit(errno);
    }
    /* This read won't block unlike the select-less case above. */
    retval = read(fd, &data, sizeof(unsigned long));
    if (retval == -1) {
        perror("read");
        exit(errno);
    }
    fprintf(stderr, " %d",i);
    fflush(stderr);
    irqcount++;
}
/* Turn off update interrupts */
retval = ioctl(fd, RTC_UIE_OFF, 0);
if (retval == -1) {
    perror("ioctl");
    exit(errno);
}
/* Read the RTC time/date */
retval = ioctl(fd, RTC_RD_TIME, &rtc_tm);
if (retval == -1) {
    perror("ioctl");
    exit(errno);
}
fprintf(stderr, "\n\nCurrent RTC date/time is %d-%d-%d, %02d:%02d:%02d.\n",
    rtc_tm.tm_mday, rtc_tm.tm_mon + 1, rtc_tm.tm_year + 1900,
    rtc_tm.tm_hour, rtc_tm.tm_min, rtc_tm.tm_sec);
/* Set the alarm to 5 sec in the future, and check for rollover */
rtc_tm.tm_sec += 5;
if (rtc_tm.tm_sec >= 60) {
    rtc_tm.tm_sec %= 60;
    rtc_tm.tm_min++;
}
if (rtc_tm.tm_min == 60) {
    rtc_tm.tm_min = 0;
    rtc_tm.tm_hour++;
}
if (rtc_tm.tm_hour == 24)
    rtc_tm.tm_hour = 0;

retval = ioctl(fd, RTC_ALM_SET, &rtc_tm);
if (retval == -1) {
    perror("ioctl");
    exit(errno);
}

/* Read the current alarm settings */
retval = ioctl(fd, RTC_ALM_READ, &rtc_tm);
if (retval == -1) {
    perror("ioctl");
    exit(errno);
}

fprintf(stderr, "Alarm time now set to %02d:%02d:%02d.\n",
    rtc_tm.tm_hour, rtc_tm.tm_min, rtc_tm.tm_sec);

/* Enable alarm interrupts */
retval = ioctl(fd, RTC_AIE_ON, 0);
if (retval == -1) {
    perror("ioctl");
    exit(errno);
}

fprintf(stderr, "Waiting 5 seconds for alarm...");
fflush(stderr);
/* This blocks until the alarm ring causes an interrupt */
retval = read(fd, &data, sizeof(unsigned long));
if (retval == -1) {
    perror("read");
    exit(errno);
}
irqcount++;
fprintf(stderr, " okay. Alarm rang.\n");

/* Disable alarm interrupts */
retval = ioctl(fd, RTC_AIE_OFF, 0);
if (retval == -1) {
    perror("ioctl");
    exit(errno);
}
/* Read periodic IRQ rate */
retval = ioctl(fd, RTC_IRQP_READ, &tmp);
if (retval == -1) {
    perror("ioctl");
    exit(errno);
}

fprintf(stderr, "\nPeriodic IRQ rate was %ldHz.\n", tmp);

fprintf(stderr, "Counting 20 interrupts at:");
fflush(stderr);

/* The frequencies 128Hz, 256Hz, ... 8192Hz are only allowed for root. */
for (tmp=2; tmp<=64; tmp*=2) {
    retval = ioctl(fd, RTC_IRQP_SET, tmp);
    if (retval == -1) {
        perror("ioctl");
        exit(errno);
    )

    fprintf(stderr, "\n%ldHz:\t", tmp);
    fflush(stderr);

    /* Enable periodic interrupts */
    retval = ioctl(fd, RTC_PIE_ON, 0);
    if (retval == -1) {
        perror("ioctl");
        exit(errno);
    }

    for (i=1; i<21; i++) {
        /* This blocks */
        retval = read(fd, &data, sizeof(unsigned long));
        if (retval == -1) {
            perror("read");
            exit(errno);
        }

        fprintf(stderr, " %d", i);
        fflush(stderr);
        irqcount++;
    }

    /* Disable periodic interrupts */
    retval = ioctl(fd, RTC_PIE_OFF, 0);
    if (retval == -1) {
        perror("ioctl");
        exit(errno);
    }
}

fprintf(stderr, "\n\n\t\t\t*** Test complete ***\n");
fprintf(stderr, "\nTyping `cat /proc/interrupts` will show %d more events on IRQ 8.\n\n", irqcount);
close(fd);
} /* end main */
```

与许多（但并非所有）基于 UNIX 的操作系统一样，内核在启动时将该时钟芯片设置为每 *n* 百分之一秒向内核发出中断。通常，UNIX 机器将此值设置为每秒 100 次。在类 Solaris 的操作系统中，此值是一个可调整参数。虽然在快速硬件上让时钟每秒向内核发出少于 100 次中断没有意义，但让它更频繁地发出中断（例如每秒 1,000 次）可能是有意义的。

人类可读的时间记录是基于内核的，并通过 `gettimeofday()` 和 `settimeofday()` 系统调用（例如 `arch/i386/kernel/timer.c`）进行管理。在启动时，内核将自身与 BIOS（CMOS）时钟对齐，随后基于定时器中断更新其时间。

在这个全球化的互联网世界中，准确的时间极其重要；因此，内核还具有一个*网络时间协议*（NTP）设施，配合 `xntpd` 使 Linux 能够跟上散布世界各地并通过互联网可访问的高精度原子时钟。非常复杂且非常精确的 NTP 协议本身由 `xntpd` 实现。内核提供了加速和减缓时间流动的功能，而不会引入用户可见的时间扭曲或时间跳跃。一个与原子时钟连接的此类 Linux 系统的示例是：

```
[mingo@s]$ date
Tue Jan 4 13:22:19 CET 2000
[mingo@s]$ ntptrace
localhost: stratum 4, offset -1.113059, sync distance 0.15135
goliath.eik.bme.hu: stratum 3, offset -1.039804, sync distance 0.05267
maze.bme.hu: stratum 2, offset -1.134906, sync distance 0.06520
hora.cs.tu-berlin.de: stratum 1, offset -1.132075, sync distance 0.00023, refid 'GPS'
```

上述 Linux 机器通过多个 NTP 服务器与一个原子时钟同步，该原子时钟每 *n* 毫秒发送一次中断。在 i386 架构上，此值通常设置为 10 毫秒。换句话说，内核将每秒唤醒 100 次。NTP 的精度在 100 微秒以内。

为了能够处理诸如设置时钟之类的维护任务，Linux 内核要求定时器以固定间隔向其发送 IRQ。设置此值的确切位置在内核的架构相关部分。因为每个架构可能有不同的需求，这样做的意义是显而易见的。

对于 i386，与定时器相关的一切都位于 `linux/arch/i386/kernel/time.c` 中，但实际时钟初始化发生在 `linux/arch/i386/kernel/irq.c` 中的 `init_IRQ()` 函数中：

```c
_initfunc(void init_IRQ(void))
{
[...]
/*
 * Set the clock to 100 Hz, we already have a valid
 * vector now:
 */
outb_p(0x34,0x43); /* binary, mode 2, LSB/MSB, ch 0 */
outb_p(LATCH & 0xff, 0x40); /* LSB */
outb(LATCH >> 8, 0x40); /* MSB */

[...]
}
```

其中 LATCH 是一个在 `linux/include/linux/timex.h` 中定义的宏：

```c
/* LATCH is used in the interval timer and ftape setup. */
#define LATCH ((CLOCK_TICK_RATE + HZ/2) / HZ)
/* For divider */
```

而 CLOCK_TICK_RATE 由 `linux/include/asm-i386/timex.h` 提供：

```c
#define CLOCK_TICK_RATE 1193180 /* Underlying HZ */
```

基本上公式是：

```
CLOCK_TICK_RATE / HZ --> downcount
```

然后内核将 downcount 写入定时器芯片。HZ 是我们希望实现的定时器中断频率。

在 i386 架构上，Linux 主要使用 100Hz 定时器，因为早期的 Linux 开发是在当时过时的标准下进行的，对于处理器而言，百分之一秒是一段显著的时间。现在，随着像 Alpha 芯片这样快几个数量级的处理器出现，架构在 Linux 中使用 1024Hz 定时器。

