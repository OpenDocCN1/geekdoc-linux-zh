
# 中断

*中断* 是设备发送给操作系统的信号，用于指示需要关注。每当处理 I/O 且设备准备好处理下一个进程时，就会产生中断。Linux 使用的中断与 DOS 使用的中断类似，因此如果你熟悉 DOS 中断，就已经了解大部分情况了。

在接收到中断后，操作系统会暂停当前正在执行的任务并处理该中断。在大多数情况下，中断由设备驱动程序处理。必须检查中断以确保其有效，并且不会影响正在进行的过程的运行，除非暂时挂起该过程。

处理中断的一个问题是，中断不应挂起 Linux 内核或设备驱动程序本身的运行，除非在受控条件下。如果没有妥善处理或仔细检查，中断可能会导致正在处理该中断所请求的 I/O 的设备驱动程序被挂起。

在关键操作可能会受到影响的处理阶段，通常会暂停中断的处理。设备驱动程序代码中不允许中断停止其处理的部分被称为 *不可停止* 或 *关键* 代码。通常，在关键代码段期间通过提高 CPU 优先级至等于或高于中断优先级级别来执行中断挂起。在关键代码执行完毕后，CPU 优先级级别再次降低。

中断优先级通常通过以下四个函数进行操作：`spl5()`、`spl6()`、`spl7()` 和 `splx()`。调用前三个函数中的任何一个，都会导致在处理期间 *不* 响应中断。`spl5()` 禁用磁盘驱动器、打印机和键盘中断。`spl6()` 禁用系统时钟，而 `spl7()` 禁用所有中断，包括串行设备。这三个函数始终返回一个表示中断级别先前值的代码。`splx()` 用于将中断恢复到其先前值。

因此，在处理关键代码之前，在设备驱动程序源代码中嵌入如下命令：

```
old_level = spl5();
```

这将禁用中断，直到发出以下命令：

```
splx(old_level);
```

多个级别的变化组合在设备驱动程序中，如下例所示：

```
int level_a, level_b;
level_a = spl5();
/* 执行任何不能被 */
/* 磁盘驱动器中断的代码 */
level_b = spl7();
/* 执行任何不能被 */
/* 任何事物中断的代码   */
splx(level_b);
/* 任何最终不能被 */
/* 磁盘驱动器中断的代码 */
splx(level_a);
```

这种看似笨拙的在级别之间来回切换的方法是必要的，以避免设备驱动程序和内核冻结，从而防止系统正常运行。保护机制必须只在必要的最短时间内调用。

通常使用 spl6( ) 和 spl7( ) 函数是不明智的。在某些情况下，spl6( ) 可能导致系统时钟丢失时间，而 spl7( ) 会导致串行 I/O 中字符丢失，除非它被用于非常短的时间跨度。即使在这种情况下，通常使用 spl5( ) 来应对关键代码中的所有中断也足够了。

# Linux 设备驱动程序的剖析

设备驱动程序代码在结构上与常规代码相似。在 Linux 中，驱动程序通常用 C 语言编写，尽管汇编和 C++ 偶尔仍会使用。

## 头部文件

典型的设备驱动程序有一个头部，其中包含系统函数、设备寄存器地址、内容定义和驱动程序全局变量定义的 `#include` 语句。大多数设备驱动程序使用标准的 `#include` 文件列表，例如：

```
param.h 内核参数
dir.h 目录参数
user.h 用户区定义
tty.h 终端和 clist 定义
buf.h 缓冲区头信息
```

tty.h 文件用于字符模式驱动程序，而 buf.h 由所有块模式设备使用。

设备寄存器在设备驱动程序头部中定义，并基于设备。对于字符模式设备，这些寄存器通常指端口地址，例如 I/O 地址、状态位和控制位。设备的切换命令定义为它们的设备代码。

设备寄存器初始化在标准屏幕终端（UART）设备的设备驱动程序中有一个示例：

```
/* define the registers */
#define RRDATA		0x01		/* receive */
#define RTDATA		0x02		/* transmit */
#define RSTATUS		0x03		/* status */
#define RCONTROL	0x04		/* control */
...etc
```

```
/* define the status registers */
#define SRDY    0x01    /* received data ready */
#define STRDY   0x02    /* transmitter ready */
#define SPERR   0x08    /* parity error */
#define SCTS    0x40    /* clear to send status */
....etc
```

设备驱动程序必须执行的功能取决于设备的性质。所有设备都有 `open()` 和 `close()` 例程，允许设备执行 I/O。

## 打开设备

`open()` 例程必须检查以确保指定了有效设备，验证设备请求（访问设备的权限或设备未就绪），然后初始化设备。`open()` 例程在每次进程使用该设备时运行。

这里提供的 `open()` 例程是针对通用终端设备 td 的。

```
tdopen(device,flag)
    int device,flag;
{
/* definitions for local variables ignored */
/* details and definitions ignored in code */

/* check device number */
if ((UNMODM(device) >= NTDEVS)
{
    seterror(ENXIO);
    return;
}

/* check if device in use */
/* if so, see if superuser (suser) for override */
tp = &td_tty[UNMODM(device)];
address = td_address[UNMODM(device)];
if((tp->t_lflag & XCLUDE) && !isuser())
{
    seterror(EBBUSY);
    return;
}

/* if not open, initialize by calling ttnit() */
if((tp->t_state & (IOPEN,WOPEN)) == 0)
{
    ttnit(tp);
/* initialize flags, and call tdparam() to set line */
    tdparam(device);
}

/* if a modem is used, check carrier status */
```
