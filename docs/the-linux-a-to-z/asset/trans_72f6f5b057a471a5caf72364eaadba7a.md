
u_addr 指针所指向的对象类型用于确定要传输到用户内存空间的值的字节数。

在使用这些函数向用户内存写入之前，然而，重要的是要验证用户进程传递给你的用户空间地址是否实际指向用户具有写访问权限的内存区域。这是通过内核的 verify_area() 函数完成的：

```
#include <linux/mm.h>
```

```
int verify_area(int access, void *u_addr, unsigned long size);
```

其中 access 是 VERIFY_WRITE 或 VERIFY_READ 之一，具体取决于你是否希望写入或从用户内存读取，u_addr 是用户空间中的起始地址，size 是要访问的内存块的字节大小。

verify_area() 函数如果指定的访问被允许则返回零值，出错时返回 -EFAULT。

### 25.3.4 写函数

驱动程序中的 write() 函数在对属于该驱动程序的设备特殊文件执行 write() 系统调用时会被调用：

```
void write(struct inode *inode, struct file *file,
    char *buf, int count);
```

其中 inode 是指向特殊文件 inode 结构的指针，file 是指向文件结构的指针，buf 是指向用户空间缓冲区的指针，传递给 write() 系统调用，用户字符将从该缓冲区写入，count 是要传输的字节数（也传递给 write() 系统调用）。

设备驱动程序的 write() 函数的目的是将最多 count 字节的数据从用户空间的缓冲区 buf 复制到硬件（如适用）或内部缓冲区。

与 read() 类似，buf 中的值是用户空间的地址，因此再次应使用以下特殊函数之一来执行复制操作：

```
unsigned char get_user_byte(char *u_addr);
unsigned short get_user_word(short *u_addr);
unsigned long get_user_long(long *u_addr);
void memcpy_fromfs(void *k_addr, void *u_addr, unsigned long cnt);
```

其中 get_user...() 函数返回位于用户空间地址 u_addr 的 char、short 或 long 值，而对于 memcpy_fromfs()，cnt 字节将从用户空间地址 u_addr 复制到内核空间地址 k_addr。

再次，为了与旧内核向后兼容，提供了另外三个函数：

```
unsigned char get_fs_byte(char *u_addr);
unsigned short get_fs_word(short *u_addr);
unsigned long get_fs_long(long *u_addr);
```

它们等同于前面三个 get_user_XXX 函数。

新的内核还支持单个调用：

```
type get_user(type *u_addr);
```

它在 <asm/segment.h> 中实现为宏，其展开取决于指针参数 u_addr 的数据类型。u_addr 指针所指向的对象类型用于确定从用户内存空间传输多少字节的数据，以及 get_user() 调用本身的返回类型。

就像设备驱动程序的 read() 函数的情况一样，在使用前面任何函数从用户内存读取之前，你应安排调用 verify_area() 函数。

## 25.4 特殊控制函数

除了基本的 open、close、read 和 write 操作之外，你还看到有时希望向设备驱动程序发送控制信息或从中获取状态信息。例如，在串行端口上更改波特率并不适合通过基本的 open、close、read、write 模式来执行。在这种情况下（以及许多类似的情况），你看到解决方案是使用 ioctl() 系统调用。此系统调用是通过在设备驱动程序中调用 ioctl() 函数来实现的。

这是必要的，因为不同的设备驱动程序并不都希望实现相同的函数——有许多设备，尝试更改波特率毫无意义。

设备驱动程序 ioctl() 函数的原型为：

```
int ioctl(struct inode *inode, struct file *file,
unsigned int cmd, unsigned long arg);
```

其中 inode 和 file 与之前相同，cmd 是要执行的命令的设备驱动程序特定代码，arg 是任何类型的 4 字节事物（通常是 int 或 struct *），为特定 cmd 值提供参数。cmd 和 arg 参数是从 ioctl() 系统调用的第二个和第三个参数获得的。

不要忘记，如果 arg 参数是指向用户空间内存块的指针，那么你必须使用我们之前查看的特殊复制函数将值放入和取出此内存块。

通常，你可以为 cmd 值使用任何你想要的数字，除了 Linux 使用四个特殊值，在你的 ioctl() 例程被调用之前它会解释这些值：

| 宏 | 值 | 描述 |
|---|---|---|
| FIONBIO | 0x5421 | 从 arg 设置/重置 O_NONBLOCK； |
| FIONCLEX | 0x5450 | 清除 close-on-exec 标志； |
| FIOCLEX | 0x5451 | 设置 close-on-exec 标志； |
| FIOASYNC | 0x5452 | 从 arg 设置/重置 O_SYNC。 |

如果你为自己的 ioctl() 命令使用这四个 cmd 值中的任何一个，你的例程永远不会被调用，因为内核会先处理它们。

## 25.5 中断

除了通过 file_operations 结构访问的函数之外，设备驱动程序还可以提供一个 interrupt() 服务例程。只有在涉及能够生成中断信号的底层硬件时才需要此功能。

与你需要将设备驱动程序注册到内核的方式类似，以便使用你的主设备号的设备特殊文件的访问会调用你的驱动程序例程，你还需要请求内核将特定的中断请求线（IRQ）与你的中断服务例程关联起来，以便当中断发生时，你的例程会被调用。这是通过 request_irq() 函数完成的：

```
#include <linux/signal.h>
```

```
int request_irq(unsigned int irq, void (*handler)(int),
    unsigned long type, char *name);
```

其中 irq 是你尝试注册的中断（IRQ）号，handler 是指向中断服务例程的指针，type 是指定这应为正常或快速中断的标志，name 是你的设备驱动程序的名称。

正常中断和快速中断之间的区别在于，从执行正常中断例程返回后，内核可以利用机会运行调度程序（通过调用内核 schedule() 函数），以查看是否有比当前进程更合适的进程可执行。如果有，则当前进程将被抢占，新进程将运行。在快速中断的情况下，不执行此调度，以便当中断服务例程返回时，被中断的进程将被恢复。

type 的值对于正常中断为零，对于快速中断为符号常量 SA_INTERRUPT。

中断处理程序也可以通过使用 free_irq() 函数来取消注册：

```
void free_irq(unsigned int irq);
```

其中 irq 是要释放的 IRQ 号。

## 25.6 设备驱动安装

一旦你编写了设备驱动程序，下一步就是将其编译并安装到可启动的内核中。这实际上是一个相当直接的任务，按以下几个简单步骤执行：

- 第一个任务是将你的 `driver.c` 文件和任何相关的 `driver.h` 文件复制到包含字符设备驱动程序源代码的目录中。这是在顶层 Linux 源代码目录下的 `drivers/char` 中。
- 接下来，你应在文件 `drivers/char/mem.c` 中将对驱动程序的 `init()` 例程的调用添加到函数 `chr_dev_init()` 的末尾。
- 现在编辑 `drivers/char` 目录中的 Makefile，并将你的 `driver.o` 名称添加到 OBJS 定义的末尾，将你的 `driver.c` 名称添加到 SRCS 定义的末尾。
- 现在切换到顶层 Linux 源代码目录，并使用第 7.4 节中描述的步骤构建和安装你的新内核。

如果你使用 lilo 来启动系统，将新内核视为实验性并在 lilo.conf 文件中生成额外的 Linux 启动部分是个好主意，这样如果新内核无法启动或由于某种原因无法正确执行，你仍然可以从旧内核启动。

作为修改内核代码的一般预防措施，始终建议备份机器上你不准备丢失的任何内容。对于大多数问题，新代码要么根本无法工作，要么会导致内核恐慌。通常，这两种事件都不会对系统造成任何持久性损害，特别是如果你可以从旧内核重新启动机器。然而，理论上，存在缺陷的内核代码可能做任何事情，包括擦除硬盘上的数据。因此，安全总比后悔好。
