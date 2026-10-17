
`/dev` 目录包含许多文件，其中大多数实际上并不是文件。`ls -l` 命令通过每行的第一个字符来区分不同类型的文件。真实文件以 `-` 开头，目录以 `d` 开头，硬链接以 `l` 开头等。设备以 `b` 或 `c` 开头，取决于它们是块设备还是字符设备。块设备按块传输数据，即均匀大小的大块。为了做到这一点，它们与内核的缓冲区缓存交互。块设备可以被挂载，即合并到 Unix 的树形文件层次结构中。硬盘是块设备的良好示例。字符设备不使用块，也不挂载。我们的小扬声器驱动就是一个字符设备。每个设备列表（块设备或字符设备）还列出了主设备号（major）和次设备号（minor）。主设备被用作 `chrdevs` 的索引，这是一个字符设备驱动的内核数组。

```
struct device_struct chrdevs[MAX_CHRDEV]
```

每个设备驱动程序仅仅是一个

```c
{
    const char * name;
    const struct file_operations * fops;
};
```

设备通过定义在 `/usr/src/linux/fs/devices.c` 中的函数 `register_chrdev()` 写入数组。该定义最重要的行如下。

```c
int register_chdev(unsigned int major,
             const char * name,
             struct file_operations *fops)
```

```c
{
    chdevs[major].name = name;
    chdevs[major].fops = fops;
    return 0;
}
```

#### 程序 11.8

当调用此函数时，主设备号将与设备驱动程序设置的文件操作结构连接。该调用是由设备驱动程序在 `cq.init()` 函数中进行的。`cq_init()` 执行的另一个任务是初始化 `cq_area` 中的某些值。为了在系统启动期间执行该调用，可以将调用放在 `mem.c` 程序末尾靠近 `lp_init()` 调用的地方。该命令

```
linuxbox$ mknod /dev/cq c 102 0
```

该命令在文件系统中为 `cq` 设备创建一个条目，赋予它主设备号 102 和次设备号 0。`/dev` 设备中的此条目用于将对 `/dev/cq` 的引用翻译为文件操作结构中列出的所有函数。

## 11.4 串口数字化器驱动程序

Scalac 设备是一种用于读取平坦表面距离的握持测量设备。它通过串口以 600 波特的速率输入数据。由于它没有手写硬件，因此不会对将其视为调制解调器或终端的软件做出响应。它还以特殊格式处理数据，将四位字符封装在每个发送或接收的字节中。由于由于这两个原因，为它编写一个特殊的驱动程序是很有用的。

典型设备驱动程序的一个重要元素（在摩斯码设备驱动程序中不需要）是中断处理程序的安装。摩斯码驱动程序只是利用了现有定时中断处理程序的服务。

### 11.4.1 设置新的中断处理程序

大多数设备驱动程序都需要一个中断服务程序（ISR）来处理来自设备的设备。Linux 的 `request_irq()` 负责安装新的处理程序。它的定义位于 `/usr/src/linux/arch/i86/kernel/irq.c`。

```c
int request_irq(unsigned int irq,
```

| | 0 Ctrl-@ | 32 <SPC> | 64 @ | 96 | i |
|---|---|---|---|---|---|

| 1 Ctrl-A | 33 ! | 65 A | 97 | a |
| 2 Ctrl-B | 34 | " | 66 B | 98 | b |
| 3 Ctrl-C | 35 # | 67 C | 99 | c |
| 4 Ctrl-D | 36 $ | 68 D | 100 | d |
| 5 Ctrl-E | 37 % | 69 E | 101 | e |
| 6 Ctrl-F | 38 & | 70 F | 102 | f |
| 7 Ctrl-G | 39 ' | 71 G | 103 | g |
| 8 Ctrl-H | 40 ( | 72 H | 104 | h |
| 9 Ctrl-I | 41 ) | 73 I | 105 | i |
| 10 Ctrl-J | 42 * | 74 J | 106 | j |
| 11 Ctrl-K | 43 + | 75 K | 107 | k |
| 12 Ctrl-L | 44 , | 76 L | 108 | l |
| 13 Ctrl-M | 45 | 77 M | 109 | m |
| 14 Ctrl-N | 46 | 78 N | 110 | n |
| 15 Ctrl-O | 47 | 79 O | 111 | o |
| 16 Ctrl-P | 48 0 | 80 P | 112 | p |
| 17 Ctrl-Q | 49 | 81 Q | 113 | q |
| 18 Ctrl-R | 50 2 | 82 R | 114 | r |
| 19 Ctrl-S | 51 3 | 83 S | 115 | s |
| 20 Ctrl-T | 52 4 | 84 T | 116 | t |
| 21 Ctrl-U | 53 5 | 85 U | 117 | u |
| 22 Ctrl-V | 54 6 | 86 V | 118 | v |
| 23 Ctrl-W | 55 7 | 87 W | 119 | w |
| 24 Ctrl-X | 56 8 | 88 X | 120 | x |
| 25 Ctrl-Y | 57 9 | 89 Y | 121 | y |
| 26 Ctrl-Z | 58 | 90 Z | 122 | z |
| 27 Ctrl-[ | 59 | 91 | 123 | { |
| 28 Ctrl-] | | | | | |
| 29 Ctrl^ | | | | | |
| 30 Ctrl_ | | | | | |
| 31 Ctrl= | | | | | |
| 32 Ctrl~ | | | | | |

## 11.4 节 串口数字化器驱动程序

```assembly
CMP EDI, [scalex_area + 12]; 结构体中的写入组件
JZ QW ; 如果跳转，则唤醒写入进程。
```

```assembly
MOV EDX, COM1 + 5 ; 线路状态寄存器
IN AL, DX;
TEST AL, 64 ; 数据已发送
JZ POL ; 应该只是短暂等待
MOV EBX, [scalex_area + 24]; ; 获取写缓冲区地址
MOV AL, COM1 ; 数据端口
OUT DX, AL ; 这里是正在发出的字节！
INC ESI
MOV EBX, [scalex_area + 16], ESI; 写入输出
JMP LEV
```

POL:

```assembly
WQW;; 写入唤醒
; _wake_up() 看起来像我们预期的函数
; 我们像接下来的两行所示推入参数。
PUSH dword 1;TASK_INTERRUPTIBLE
PUSH dword scalex_area + 32; 唤醒
; 这是一个双指针！
; 然而 _wake_up() 实际上想要参数
; 在寄存器 EDX 和 EAX 中！
MOV EDX, 1;TASK_INTERRUPTIBLE
MOV EAX, scalex_area + 32; 写入等待队列
CALL _wake_up
JMP LEV
```

RQW;; 读取队列唤醒

```assembly
; 用于读取挂等待的标志位组件
TEST dword [scalex_area], 8
JZ NEAR LEV ; 没有？假警报，保持静默即可。
MOV EDX, 1;TASK_INTERRUPTIBLE
MOV EAX, scalex_area + 28; 读取等待队列
CALL _wake_up
JMP LEV
```

RBF ;; 读取缓冲区满

```assembly
PUSH dword OVR ; 溢出
CALL printk
ADD ESP, 4
JMP LEV
```

; 错误消息：

OVR: db "Read buffer overflow!",0AH,0

; 半字节到字节的转换表：

OKC: db "0123456789AB-",0AH,".F"

LEV:

```assembly
+   POP EDI
POP ESI
POP EBX
POP EDX
POP ECX
RET
```

程序 11.9

### 11.4.3 Scalax 系统调用处理程序

以下是文件操作结构体指向的函数。
