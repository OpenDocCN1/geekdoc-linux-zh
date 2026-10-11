

从上面的公式可以看出，若要使 IA32（Intel x86）移植版使用例如 1000Hz 的定时器，唯一需要修改的是 `HZ` 定义，这是该公式唯一的输入参数。

```text
root@hirame:~/kernel > find 2.2.13/include/asm-* -type f -exec
egrep '# *define HZ' {} /dev/null \;
2.2.13/include/asm-alpha/param.h:# define HZ 1024
2.2.13/include/asm-arm/arch-eb2s110/param.h:#define HZ 100
2.2.13/include/asm-arm/proc-arm226/param.h:#define HZ 100
2.2.13/include/asm-arm/proc-arm235/param.h:#define HZ 100
2.2.13/include/asm-arm/arch-nexuspci/param.h:#define HZ 100
2.2.13/include/asm-arm/proc-rpc/param.h:#define HZ 100
2.2.13/include/asm-arm/proc-arm0/param.h:#define HZ 100
2.2.13/include/asm-i386/param.h:#define HZ 100
2.2.13/include/asm-m68k/param.h:#define HZ 100
2.2.13/include/asm-mips/param.h:#define HZ 100
2.2.13/include/asm-ppc/param.h:#define HZ 100
2.2.13/include/asm-sparc/param.h:#define HZ 100
2.2.13/include/asm-sparc64/param.h:#define HZ 100
```

每种架构都有一个首选的 HZ 定义值。

虽然将 HZ 更改为 1,000 后内核将使用 1,000Hz 的定时器，但请注意，用户空间中运行的任何程序（如果未相应适应）仍会认为内核是以 100Hz 定时器运行的。换句话说，某些用户空间程序（如 `top`）可能会因此出错。这是因为一些数据仍以滴答数（jiffy）为单位（每秒 100 个）从内核空间导出到用户空间。

内核内部存在的这种“可见性”问题，可以通过将目前唯一的 HZ 拆分为内部 HZ 和导出到用户空间的 HZ 来解决。已有相关的补丁实现了这一点。它们尚未集成到内核中，仅仅是因为 100Hz 定时器似乎造成的影响不大。

值得注意的是，在 IA32-SMP 系统中，定时器中断仅用于管理系统时间并启动软件中断（下半部处理程序）。所有调度核算实际上是由 IO-APIC 向所有 CPU 广播生成的 SMP 定时器中断触发的（与定时器中断不同，后者在 IA32-SMP 移植版中是单播中断）。因此，如果增加定时器频率的目的是使调度更细致，在 IA32-SMP 系统中，我们应仅通过重新编程 IO-APIC 来改变 SMP 定时器中断的频率。IO-APIC 本地定时器 IRQ 的频率是在 `linux/arch/i386/kernel/smp.c` 文件中的 `setup_APIC_timer()` 函数内设置的。

### 数据结构——linux/mc146818rtc.h

```c
/* mc146818rtc.h - register definitions for the Real-Time-Clock / CMOS RAM
 * Copyright Torsten Duwe <duwe@informatik.uni-erlangen.de> 1993
 * derived from Data Sheet, Copyright Motorola 1984 (!).
 * It was written to be part of the Linux operating system.
 */
/* permission is hereby granted to copy, modify and redistribute this code
 * in terms of the GNU Library General Public License, Version 2 or later,
 * at your option.
 */

#ifndef _MC146818RTC_H
#define _MC146818RTC_H
#include <asm/io.h>
#include <linux/rtc.h> /* get the user-level API */

#ifndef RTC_PORT
#define RTC_PORT (x)       (0x70 + (x))
#define RTC_ALWAYS_BCD     1
#endif

#define CMOS_READ (addr) (( \
outb_p ((addr) ,RTC_PORT (0)); \
inb_p (RTC_PORT (1)); \
))
#define CMOS_WRITE (val , addr) (( \
outb_p ((addr) ,RTC_PORT (0)); \
outb_p ((val) ,RTC_PORT (1)); \
))

/*****/
** register summary *
****/
#define RTC_SECONDS        0
#define RTC_SECONDS_ALARM  1
#define RTC_MINUTES        2
#define RTC_MINUTES_ALARM  3
#define RTC_HOURS          4
#define RTC_HOURS_ALARM    5
/* RTC_*_alarm is always true if 2 MSBs are set */
# define RTC_ALARM_DONT_CARE       0xC0

#define RTC_DAY_OF_WEEK  6
#define RTC_DAY_OF_MONTH 7
#define RTC_MONTH        8
#define RTC_YEAR         9

/* control registers - Moto names
*/
#define RTC_REG_A        10
#define RTC_REG_B        11
#define RTC_REG_C        12
#define RTC_REG_D        13

/*******************************************************************
 * register details
********************************************************************/
#define RTC_FREQ_SELECT RTC_REG_A

/* update-in-progress - set to "1" 244 microseconds before RTC goes off the bus,
 * reset after update (may take 1.984ms @ 32768Hz RefClock) is complete,
 * totalling to a max high interval of 2.228 ms.
 */
# define RTC_UIP         0x80
# define RTC_DIV_CTL      0x70
/* divider control; refclock values 4.194 / 1.049 MHZ / 32.768 kHz */
# define RTC_REF_CLK_4MHZ         0x00
# define RTC_REF_CLK_1MHZ         0x10
# define RTC_REF_CLK_32KHZ        0x20
/* 2 values for divider stage reset, others for "testing purposes only" */
# define RTC_DIV_RESET1   0x60
# define RTC_DIV_RESET2   0x70
/* Periodic intr. / Square wave rate select. 0=none, 1=32.8KHz,... 15=2Hz */
# define RTC_RATE_SELECT  0x0F

/*******************************************************************
#define RTC_CONTROL      RTC_REG_B
# define RTC_SET 0x80       /* disable updates for clock setting */
# define RTC_PIE 0x40       /* periodic interrupt enable */
# define RTC_AIE 0x20       /* alarm interrupt enable */
# define RTC_UIE 0x10       /* update-finished interrupt enable */
# define RTC_SOWE 0x08      /* enable square-wave output */
# define RTC_DM_BINARY 0x04 /* all time/date values are BCD if clear */
# define RTC_24H 0x02       /* 24 hour mode - else hours bit 7 means pm */
# define RTC_DST_ON 0x01    /* auto switch DST - works f. USA only */

/*******************************************************************
#define RTC_INTR_FLAGS RTC_REG_C
/* caution - cleared by read */
# define RTC_IRQF 0x80      /* any of the following 3 is active */
# define RTC_PF 0x40
# define RTC_AF 0x20
# define RTC_UF 0x10

/*******************************************************************
#define RTC_VALID        RTC_REG_D
# define RTC_VRT 0x80       /* valid RAM and time */
/*******************************************************************

/* example: !(CMOS_READ(RTC_CONTROL) & RTC_DM_BINARY)
 * determines if the following two #defines are needed
 */
#ifndef BCD_TO_BIN
#define BCD_TO_BIN (val) (((val)=((val)&15) + ((val)>>4)*10)
#endif

#ifndef BIN_TO_BCD
#define BIN_TO_BCD (val) ((val)=((val)/10)<<4) + (val)%10)
#endif

#endif /* _MC146818RTC_H */
```

## 实时性能分析

有时，希望提高程序速度和/或消除冗余或未使用代码的开发者可能需要测量其代码每段被执行了多少次。为此，可以使用一种称为*实时性能分析*的功能，内核会保留程序执行时的实时时间戳集合，并将这些时间戳写入日志文件以供后续分析。实时性能分析需要硬件的支持才能工作。Intel 架构默认提供此类功能。如何加以利用取决于操作系统。Windows 操作系统不提供实时性能分析功能。

对于 2.2.x 和 2.3.x 内核的实时性能分析，你只需在启动内核时指定参数 `profile=4` 即可，例如。其中的 4 是我通常使用的性能分析图粒度。换句话说，对于每 4 字节长的代码段，都会分配一个整数计数变量。从而生成代码段使用情况的直方图原始统计数据。

在 IA 32（Intel i386）架构上，性能分析程序在 UP（单处理器）模式下由定时器中断运行，在 SMP（多处理器）模式下由 SMP 本地 APIC 定时器中断运行（因此两个 CPU 都会被进行性能分析）。假设我们有一个内核镜像，范围从 `0xc0100000` 到 `c0154321`。内核性能分析器在此 EIP 范围内进行性能分析。对于每个性能分析中断（通常为 `IRQ0`），我们知道被中断的 EIP。其逻辑如下：

```c
/*
 * Only measure the CPU's specified by /proc/irq/prof_cpu_mask.
 * (default is all CPUs.)
 */
if (!(1<<smp_processor_id() & prof_cpu_mask))
    return;

if (prof_buffer) {
    eip -= (unsigned long) &_stext;
    eip >>= prof_shift;
    /*
    * Don't ignore out-of-bounds EIP values silently,
    * put them into the last histogram slot, so if
```

