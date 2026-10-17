
我们调用 `check_region()` 来测试 I/O 端口是否可用（未被其他驱动程序使用），然后使用 `request_region()` 注册它们。这些调用接受一个基地址和连续 I/O 地址的数量。如果该区域可用，`check_region()` 函数返回零。该区域稍后用 `release_region()` 释放，该函数接受相同的参数。

接下来，根据所选的操作模式，我们将其中一个下半部（bottom half）函数放入队列以接收中断或定时 tick。`request_irq()` 函数之前已经描述过。如果我们正在使用定时 tick，我们使用 `queue_task()` 将自己放入适当的队列以接收定时 tick。如果我们正在使用来自并行口卡的硬件中断，我们告诉显卡触发硬件中断线，以便我们能从外部时钟源接收中断。

为了测试，我让驱动程序启动了一个 400 次计数的移动（我正在使用的电机旋转一圈）；这应该被注释掉。最后，我们向世界宣布我们已成功加载，并返回到加载我们的 `insmod` 或 "kmod" 程序。

`cleanup_module()` 函数被用来终止并卸载内核模块。此函数由 `rmmod` 和 `kmod` 程序启动。这本质上是 `init_module()` 操作的反向操作。内核函数 `unregister_chrdev()` 将注销我们之前注册的主设备号，而如果我们注册了中断，`free_irq()` 将释放该中断。

显然，没有办法可以从定时 tick 队列中移除自己，因此我们一直睡眠，直到下半部通过接收定时 tick 且不重新注册来有效地将我们移除。注意，在发生 `MOD_IN_USE` 事件或 `unregister_chrdev()` 失败时，我本应该使用 `sleep_on` 技巧。由于我们无法避免模块的加载，我们可能会永远等待。我们也可以让下半部偶尔唤醒我们以重试失败的操作。在合适的情况下，我们在宣布终止并返回之前，通过关闭所有转换器来关掉步进电机。

## 列表 25.16 初始化与终止

```c
int init_module(void)
{
    int rc;
    ring_buffer_init(&read_buffer);
    ring_buffer_init(&write_buffer);
    read_is_sleeping = 0;
    write_is_sleeping = 0;

    if ((stepper_major = register_chrdev(major, "step", &stepper_tops)) < 0) {
        printk("stepper: unable to get major device\n");
        return (-EIO);
    }

    if (!check_region(base, count)) {
        printk("stepper: I/O region already in use\n");
        return (-EBUSY);
    }

    if (!request_region(base, count)) {
        printk("stepper: could not acquire region\n");
        unregister_chrdev(major, "step");
        return (-EBUSY);
    }

    if (use_timer) {
        queue_task(&tick_queue_entry, &tq_timer);
    } else {
        request_irq(irq, interrupt_handler, dev_id);
    }

    /* 为了测试，启动移动 */
    move_one_step(400);

    printk("stepper: module loaded\n");
    return 0;
}

void cleanup_module(void)
{
    if (use_timer) {
        /* 等待最后一个 tick 处理程序完成 */
        while (using_jiffies) {
            sleep_on(&tick_die_wait_queue);
        }
    } else {
        free_irq(irq, dev_id);
    }

    release_region(base, count);
    unregister_chrdev(major, "step");

    if (power_down_on_exit) {
        /* 将低字节输出数据寄存器 */
        outb(word & 0x0FF, base+0);
        /* 将高字节输出控制寄存器 */
        outb(word >> 8, base+2);
    }

    if (debug) printk("stepper: module unloaded\n");
}
```

## 进程间通信与网络编程

### 第三部分

## 列表 25.17 main() 函数

```c
#ifndef __KERNEL__
{
    char c;

    /* 取消输出缓冲以便实时查看 */
    setbuf(stdout,NULL);

    printf("this program must be run as root\n");
    ioctl(3); /* Enable i/o (如果是 root) */

    printf("Here are some example motion commands:\n");
    printf("X=100,Y=100,Z=50\n");
    printf("X=100,Y=100,Z=50\n");
    printf("Y=100,Z=50\n");
    printf("X+100,Y=-100\n");
    printf(" ? (报告位置)\n");
    printf("每个命令以换行符结束\n");
    while (!feof(stdin)) {
        c = get(stdin);
        parse_one_char(c);
        move_all();
    }

if(power_down_on_exit) {
    word=flipbits;
    /* 将低字节输出到数据寄存器 */
    verbose_outb(word & 0x00FF, base+0);
    /* 将高字节输出到控制寄存器 */
    verbose_outb(word >> 8, base+2);
}

#endif
```

## 编译驱动程序

列表 25.18 显示了使用 make 程序编译驱动程序的 Makefile。

![](img/69b363a7d7f58dc8d0b8c78c0052826f_430_0.png)

### 列表 25.18 MAKEFILE

default: all

all: stepper-o stepuser

```make
stepper-o: stepper.c ring.h stepper.h
gcc -o -DMODULE -D_KERNEL,-o stepperout.o -c stepper.c
ld -r -o stepper.o stepperout.o ring.o
```

```make
stepuser: stepper.c
gcc -g -o stepuser stepper.c
```

```make
ring.o: ring.c ring.h
gcc -o -DMODULE -D_KERNEL__ -c ring.c
```

## 使用内核驱动程序

列表 25.19 中的一组简单的 shell 命令将演示如何使用驱动器。CD 光盘上还有一个 C 程序，它将执行几次移动并返回位置。

### 列表 25.19 驱动程序使用

```bash
# 创建设备（执行一次）
mkn /dev/stepper c 31 0
mkn /dev/stepper_ioctl c 31 1
```

```bash
# 加载驱动
sync; ins ./stepper.o port=0x378
```

```bash
# 执行一些操作
cat "X=100,Y=100,Z=100" > /dev/stepper
cat "X=300,Y=300,Z=300" > /dev/stepper
cat "X=0,Y=0,Z=0" > /dev/stepper
```

```bash
# 卸载驱动
sync; rmmod stepper.o
```

可以设置不同的变量来修改驱动程序的操作。仅在用户模式下，变量 `delay` 设置移动之间睡眠的微秒数；如果 `fastdelay` 为真，则将使用指定迭代次数的延迟循环。在内核模式下，可以使用 `skipticks` 通过在移动之间跳过指定数量的定时器滴答来缓慢移动。变量 `debug` 设置打印的调试信息量。变量 `verbose_io` 如果不为零，则每次调用 `out()` 时都会打印调试消息。变量 `verbose_move` 如果不为零，则每次移动 `motor()` 时都会打印调试消息。如果为内核模式驱动设置了 `verbose_io` 或 `verbose_move`，请使用 `skipticks` 值来减少 `printk()` 的调用频率。变量 `base` 设置使用的并行接口的 I/O 端口地址；值 `0x3BC`、`0x378` 和 `0x278` 是常见的。如果 `power_down_on_exit` 设置为非零值，当用户程序退出或移除内核模块时，电机将关闭。变量 `do_io` 如果设置为零，将禁用 io 调用，允许在没有空闲并行端口的情况下进行实验（设置了 `verbose_io` 和/或 `verbose_move`）。这些变量中的一些也可以通过 ioctls 设置。

> 注意
>
> 驱动程序正在发出大量的 `printk()`，你可能需要盲目地输入 `rmmod stepper` 命令，因为内核消息会导致 shell 提示符和输入回声刷屏。

注意，并行端口不能被其他设备驱动程序（如 `lp0`）占用。你可能需要卸载打印机模块，或在启动提示符带有 `reserve=0x378,4` 选项启动系统。如果你尝试使用中断并遇到问题，请检查是否与其他设备冲突（打印机上的中断通常不用于打印机），并检查你的 bios 以确保它没有被分配给 PCI 总线而不是 ISA 总线或主板。

## 未来方向

未来我可能会对此驱动程序进行一些改进。对... 的适当处理。

# 终端控制详解

## 第 26 章

终端接口不仅需要管理用户与系统、程序与系统、设备与系统之间的交互，还必须接受来自近乎无限来源的输入并发送输出。考虑所有用于传输用户输入的不同键盘型号、鼠标、操纵杆和其他设备。再加上所有不同类型的输出设备，如调制解调器、打印机、绘图仪、串口设备、卡和显示器。终端接口必须兼容所有这些设备。这种海量的硬件要求了一程度程度复杂性。

复杂性源于人性。因为终端是交互式的，用户（人）希望控制交互并根据自己的习惯、喜好和厌恶进行定制。由于这种人类倾向，接口的规模和功能集随之增大，复杂性也随之增加。

本节后续将展示如何使用 POSIX 接口操作终端行为。`termios` 对 Linux 接收和处理输入的方式提供了精细粒度的控制。通过在本章稍后的部分使用“terminfo”，你将学习如何控制控制台或 xterm 屏幕上的输出显示。

### 控制终端

POSIX 定义了一个用于查询和操作终端的标准接口。该接口称为 `termios`，定义在系统头文件 `<termios.h>` 中。`termios` 最接近 System V UNIX 的 `termio` 模型，但也包含了一些来自 Berkeley 派生的 UNIX 系统的终端特性。从程序员的角度来看，`termios` 是一个数据结构和一组操作该结构的函数。下面列出的 `termios` 数据结构包含了对终端特性的完整描述。相关的函数用于查询和更改这些特性。

```c
#include <termios.h>

struct termios {
    tcflag_t c_iflag;    /* 输入模式标志 */
    tcflag_t c_oflag;    /* 输出模式标志 */
    tcflag_t c_cflag;    /* 控制模式标志 */
    tcflag_t c_lflag;    /* 本地模式标志 */
    cc_t c_line;         /* 规程 */
    cc_t c_cc[NCS];      /* 控制字符 */
};
```

`c_iflag` 成员控制输入处理选项。它影响终端驱动程序在将输入发送到程序之前如何处理输入。`c_oflag` 成员控制输出并决定终端驱动程序在将输出发送到屏幕或其他输出设备之前如何处理输出。各种控制标志决定了终端设备的硬件特性，设置在 `c_iflag` 成员中。存储在 `c_iflag` 中的本地模式标志操作终端特性，例如输入字符是否在屏幕上回显。`c_cc` 数组包含了特殊字符序列的值（例如 `^`（退出）和 `^H`（删除））以及它们的行为。`c_line` 成员指示控制协议，例如 SLIP、PPP 或 X.25——我们不会讨论这个成员，因为它的用法超出了本书的范围。

终端运行在两种模式之一：规范模式（或称为“熟化”模式），在该模式下，终端驱动程序处理特殊字符并逐行向程序提供输入；以及非规范模式（或称为“原始”模式），在该模式下，绝大多数键盘输入是不经处理且无缓冲的。shell 是使用规范模式的应用示例。另一方面，屏幕编辑器 `vi` 在输入时即刻接收输入，并由自己处理大多数特殊字符（例如，在 `vi` 中 `^0` 会移动到文件末尾，这会向 shell 发送 EOP 信号）。

表 26.1 列出了终端控制模式中使用的标志。

| POSIX termios 标志 | 成员 | 描述 |
| :--- | :--- | :--- |
| `IGNBRK` | `c_iflag` | 输入满足条件时忽略 BREAK。 |
| `BRKINT` | `c_iflag` | 如果设置了 `IGNBRK`，在中断时产生 `SIGINT`。 |
| `INLCR` | `c_iflag` | 输入时将 NL 转换为 CR。 |
| `IGNCR` | `c_iflag` | 输入时忽略 CR。 |
| `ICRNL` | `c_iflag` | 如果未设置 `IGNCR`，则输入时将 CR 转换为 NL。 |
| `ONLCR` | `c_oflag` | 输出时将 NL 映射为 CR-NL。 |
| `OCRNL` | `c_oflag` | 输出时将 CR 映射为 NL。 |
| `ONLRET` | `c_oflag` | 不输出 CR。 |
| `HUPCL` | `c_iflag` | 在处理最后一个设备后关闭连接。 |
| `CLOCAL` | `c_iflag` | 忽略模式控制线。 |
| `ISIG` | `c_iflag` | 当接收到 INTR、UIT 或 SUSP 字符时分别产生 `SIGINT`、`SIGOUT`、`SIGSTOP`。 |
| `ICANON` | `c_iflag` | 启用规范模式。 |
| `ECHO` | `c_iflag` | 将输入字符回显到输出。 |
| `ECHON` | `c_iflag` | 在规范模式下回显 NL 字符，即使未设置 `ECHO`。 |

控制字符数组 `c_cc` 包含至少八个特殊控制字符，例如 `^D` EOF、`^INTR`、`^U` KILL。在十一个字符中，有九个可以更改。CR 始终是 `\r`，NL 始终是 `\n`；两者都无法更改。

### 属性控制函数

`termios` 接口包含了控制终端特性的函数。基本函数是 `tcgetattr()` 和 `tcsetattr()`。`tcgetattr()` 初始化一个 `termios` 数据结构，设置代表终端特性和配置的值。查询和更改这些设置意味着使用后续节讨论的函数来操作 `tcgetattr()` 返回的数据结构。一旦完成，`tcsetattr()` 将使用新值更新终端。

```c
int tcgetattr(int fd, struct termios *tp);
```

`tcgetattr()` 查询文件描述符相关的终端参数并存储在 `termios` 结构中。

```c
int tcsetattr(int fd, int action, struct termios *tp);
```

`tcsetattr()` 使用 `termios` 结构设置文件描述符相关的终端参数。`action` 参数控制更改生效的时机：

- `TCSOW`—立即生效。
- `TCSAIN`—在发送所有输出后生效。
- `TCSAFLUSH`—在丢弃所有输入后生效。

### 速度控制函数

前四个函数设置终端的输入输出速度。由于接口较旧，它以波特率定义速度。函数成对出现，用于获取和设置速率。它们在 `<termios.h>` 头文件中声明，如下所示，并带有简短的行为描述。

```c
int cfgetspeed(struct termios *tp);
```

`cfgetspeed()` 返回 `termios` 结构中的输入速率。

```c
int cfsetpeed(struct termios *tp, speed_t speed);
```

`cfsetpeed()` 设置 `termios` struct中的输入速率。`speed` 参数必须是以下常量之一：

- `B0`（关闭连接） 1800
- `B50` 2400
- `B75` 4800
- `B110` 9600
- `B134` 19200
- `B150` 38400
- `B200` 57600
- `B300` 115200
- `B600` 230400

### 行控制函数

行控制函数查询并设置关于数据如何、何时以及是否流终端设备的各种属性。这些函数允许你对终端设备的行为进行精细控制。例如，要在继续之前强制完成所有待处理输出，可以使用 `tcdrain()`，其原型如下：

```c
int tcdrain(int fd);
```

`tcdrain` 等待所有输出写入文件描述符后返回。

要强制刷新输出、输入或两者，使用 `tcflush()` 函数。其原型如下：

```c
int tcflush(int fd, int queue);
```
