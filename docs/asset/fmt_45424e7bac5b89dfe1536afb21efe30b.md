
通常做法是在包含文件中定义 C 程序中使用的参数。摩斯密码驱动程序的包含文件如下。

```c
#define CQ_EXIST	0x0001
#define CQ_BUSY	0x0002
#define CQ_OFF		0x0004
#define CQ_ABORT	0x0008

/* IOCTL numbers */

#define CQABORT	0x0714
#define CQSETTEMPO  0x0716  /* Store whole note int cq_area.  */
#define CQSETPITCH  0x0719  /* Store a timer divisor into cq_area.   */
#define CQRESET	0x071c  /* reset speaker */
#define CQGETFLAGS  0x071e  /* get status flags */
```

```c
#define CQ_BUFFER_SIZE         256
#define CQ_DEF_CHAR            0      /* Default character */
#define CQ_DEF_PITCH           440    /* Default pitch */
#define CQ_DEF_TEMPO           160    /* Default tempo */
/*
 *  function prototypes
 */
extern int cq_init(void);
```

定义在结构 `cq_struct` 中的函数负责处理驱动程序对内核在执行系统调用时向驱动程序发出的服务请求的响应。`cq_timer_handler()` 函数负责处理驱动程序对定时器中断的响应。这些是主要需要完成的工作。但当设备驱动程序工作时，诸如

```bash
linuxbox$ cat file > /dev/cq
```

等命令将开始让扬声器发出蜂鸣声。为了实现这一点，必须在 `/dev` 目录中有一个名为 `cq` 的条目，该条目与 `cq_write()` 等程序相关联。

### 11.3.11 收尾工作

为了完善设备驱动程序，只需执行以下操作：

- 在 `/usr/include/linux/major.h` 文件中为该设备添加一个主设备号。
- 使用 `mknod` 命令在 `/dev` 目录中为该设备创建条目。
- 编写 `cq_init()` 函数，并在 `mem.c` 文件中包含对其的调用。
- 修改包含驱动程序的目录（本例中为 `/usr/src/linux/drivers/char`）下的 `Makefile`，并重新编译内核。

`/dev` 目录包含大量文件列表，其中大多数实际上并不是常规文件。`ls -l` 命令通过每一行的第一个字符来区分不同类型的文件。真正的常规文件以 `a -` 开头列出，目录以 `ad` 开头列出，硬链接以 `l` 开头列出，等等。设备根据是块设备还是字符设备，分别以 `b` 或 `c` 列出。块设备以块为单位传输数据，即大小均匀的大数据块。为此，它们与内核的缓冲区缓存进行交互。块设备可以被挂载，即集成到 Unix 的树状文件层次结构中。硬盘是块设备的一个良好示例。字符设备不使用块，也不会被挂载。我们的小扬声器驱动程序是一个字符设备。每个设备条目，无论是块设备还是字符设备，还都列出了主设备号和次设备号。主设备号用作内核字符设备驱动程序数组 `chrdevs` 的索引。

```c
struct device_struct chrdevs[MAX_CHRDEV]
```

每个设备驱动程序仅仅是一个

```c
struct device_struct
{
    const char *name;
    const struct file_operations *fops;
};
```

设备通过定义在 `/usr/src/linux/fs/devices.c` 中的函数 `register_chrdev()` 被放入数组中。该定义中最重要的是以下几行。

#### 程序 11.8

```c
int register_chrdev(unsigned int major,
                    const char *name,
                    const struct file_operations *fops)
{
    ...
}
```

`struct file_operations *fops)`

{

    `chrdevs[major].name = name;`

    `chrdevs[major].fops = fops;`

    return 0;

}

当调用此函数时，主设备号会与设备驱动程序设置的文件操作结构体建立连接。该调用由设备驱动程序在 `cq_init()` 函数中发起。`cq_init()` 执行的另一个唯一任务就是初始化 `cq_area` 中的部分值。为了使该调用在启动期间执行，可以将对它的调用放置在 `mem.c` 程序的末尾附近，靠近对 `lp_init()` 的调用处。命令

```
linuxbox$ mknod /dev/cq c 102 0
```

会在文件系统中为 `cq` 设备创建一个条目，赋予它主设备号 102 和次设备号 0。然后，`/dev` 目录中的这个条目用于将对 `/dev/cq` 的引用转换为对文件操作结构体中列出的函数的调用。

## 11.4 串口数字化仪驱动程序

Sealex 设备是一种手持式测量设备，用于读取平坦表面的距离。它通过串口以 600 波特率输入数据。由于它没有握手硬件，因此它对将其视为调制解调器或终端的软件不做响应。它还以特殊格式处理数据，该格式将两个四比特字符打包到发送或接收的每个字节中。出于这两个原因，为其编写专用驱动程序是非常有用的。

典型设备驱动程序的一个重要组成部分，在摩尔斯电码设备驱动程序中未用到，是安装中断处理程序。摩尔斯电码驱动程序只是利用了现有的定时器中断处理程序的服务。

### 11.4.1 设置新的中断处理程序

大多数设备驱动程序需要一个 ISR 来处理来自设备的中断。Linux 函数 `request_irq()` 负责安装新的处理程序。其定义位于 `/usr/src/linux/arch/i386/kernel/irq.c`。

```
int request_irq(unsigned int irq,
```

#### 表 11.1. ASCII 码表

| 0 | Ctrl-@ | 32 | <SPC> | 64 | @ | 96 | ' |
|---|---|---|---|---|---|---|---|
| 1 | Ctrl-A | 33 | ! | 65 | A | 97 | a |
| 2 | Ctrl-B | 34 | " | 66 | B | 98 | b |
| 3 | Ctrl-C | 35 | # | 67 | C | 99 | c |
| 4 | Ctrl-D | 36 | $ | 68 | D | 100 | d |
| 5 | Ctrl-E | 37 | % | 69 | E | 101 | e |
| 6 | Ctrl-F | 38 | & | 70 | F | 102 | f |
| 7 | Ctrl-G | 39 | ' | 71 | G | 103 | g |
| 8 | Ctrl-H | 40 | ( | 72 | H | 104 | h |
| 9 | Ctrl-I | 41 | ) | 73 | I | 105 | i |
| 10 | Ctrl-J | 42 | * | 74 | J | 106 | j |
| 11 | Ctrl-K | 43 | + | 75 | K | 107 | k |
| 12 | Ctrl-L | 44 | , | 76 | L | 108 | l |
| 13 | Ctrl-M | 45 | - | 77 | M | 109 | m |
| 14 | Ctrl-N | 46 | . | 78 | N | 110 | n |
| 15 | Ctrl-O | 47 | / | 79 | O | 111 | o |
| 16 | Ctrl-P | 48 | 0 | 80 | P | 112 | p |
| 17 | Ctrl-Q | 49 | 1 | 81 | Q | 113 | q |
| 18 | Ctrl-R | 50 | 2 | 82 | R | 114 | r |
| 19 | Ctrl-S | 51 | 3 | 83 | S | 115 | s |
| 20 | Ctrl-T | 52 | 4 | 84 | T | 116 | t |
| 21 | Ctrl-U | 53 | 5 | 85 | U | 117 | u |
| 22 | Ctrl-V | 54 | 6 | 86 | V | 118 | v |
| 23 | Ctrl-W | 55 | 7 | 87 | W | 119 | w |
| 24 | Ctrl-X | 56 | 8 | 88 | X | 120 | x |
