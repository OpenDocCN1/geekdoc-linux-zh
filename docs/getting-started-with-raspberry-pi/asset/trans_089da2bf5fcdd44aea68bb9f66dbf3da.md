

/* 使用 TSC 精确测量所消耗的时间。
* 读取 TSC 的下半部分就足够了 */
rdtsc1(ts1);
now = (ts1-ts0);

/* 更新最坏情况延迟 */
if (now > worst) worst = now;
ts0 = ts1;

/* 执行需要周期性完成的工作 */
do_work(); /* 为了测量目的而做的空操作 */
}

printf("Worst latency was %ld\n", worst);

/* 禁用周期性中断 */
ioctl(fd, RTC_PIE_OFF, 0);
}

列表 19.1 中的代码循环执行 10,000 次，并打印出执行过程中发生的最坏情况延迟。在一台奔腾 1.8Ghz 机器上，输出结果为 240899，这大致对应于 133 微秒。根据 RTC 芯片组的数据手册，8192Hz 的定时器频率应产生 122 微秒的周期性中断率。这很接近。使用 SCHED_OTHER 代替 SCHED_FIFO，在变化的负载下重新运行代码，并观察由此产生的漂移。

你还可以以实时模式（RT 模式）运行内核线程。为此，在启动线程时执行以下操作：

static int
my_kernel_thread(void *i)
{
    daemonize();
    current->policy = SCHED_FIFO;
    current->rt_priority = 1;
    /* ... */
}

## 访问 I/O 区域

PC 兼容系统有 64K 个 I/O 端口，所有端口都可以从用户空间驱动。Linux 中对 I/O 端口的用户访问由两个函数控制：ioperm() 和 iopl()。ioperm() 控制对前 0x3ff 个端口的访问权限。iopl() 更改调用进程的 I/O 特权级别，从而允许（除其他事项外）不受限制地访问所有端口。只有超级用户才能调用这两个函数。

要向 I/O 端口写入数据，请使用 outb()、outw()、outl() 或它们的类似函数。要从端口读取数据，请使用 inb()、inw()、inl() 或它们的类似函数。让我们实现一个简单的程序，用于读取 RTC 芯片内部跳动的秒数。PC CMOS（RTC 是其一部分）中的 I/O 区域通过索引端口（0x70）和数据端口（0x71）进行访问，如第 5 章“字符设备”中的表 5.1 所示。要从 I/O 地址范围内的偏移量 off 处读取一个字节的数据，请将 off 写入索引端口，并从数据端口读取相关数据。列表 19.2 读取 RTC 的秒字段；但要使用它从其他 I/O 区域获取数据，需相应地更改传递给 dump_port() 的参数。

### 列表 19.2. 从 I/O 区域转储字节的实用程序

```c
#include <linux/ioport.h>

void
dump_port(unsigned char addr_port, unsigned char data_port,
          unsigned short offset, unsigned short length)
{
    unsigned char i, *data;

    if (!(data = (unsigned char *)malloc(length))) {
        perror("Bad Malloc\n");
        exit(1);
    }

    /* 将偏移量写入索引端口
       并从数据端口读取数据 */
    for(i=offset; i<offset+length; i++) {
        outb(i, addr_port  );
        data[i-offset] = inb(data_port);
    }

    /* 转储 */
    for(i=0; i<length; i++)
        printf("%02X ", data[i]);

    free(data);
}

int
main(int argc, char *argv[])
{
    /* 获取访问权限 */
    if( iopl(3) < 0) {
        perror("iopl access error\n");
        exit(1);
    }
    dump_port(0x70, 0x71, 0x0, 1);
}
```

你还可以通过操作 /dev/port 来完成同样的任务。这会产生性能开销，因为代码流必须经过内核驱动程序，但你无需使用 iopl() 或 ioperm() 即可灵活地控制设备节点上的访问权限。以下是列表 19.2 的 /dev/port 等效代码：

```c
#include <unistd.h>
#include <fcntl.h>

int
main(int argc, char *argv[])
{
   char seconds=0;
   char data = 0;
   int fd = open("/dev/port", O_RDWR);

   lseek(fd, 0x70, SEEK_SET);
   write(fd, &data, 1);

   lseek(fd, 0x71, SEEK_SET);
   read(fd, &seconds, 1);
   printf("%02X ", seconds);
}
```

在第 5 章中，你学习了如何通过内核驱动程序与计算机的并行端口通信。现在让我们实现一个示例程序，从用户空间与并行端口设备交互。内核的并行端口子系统提供了一个名为 ppdev 的字符驱动程序，它将并行端口访问导出到用户空间。Ppdev 创建设备节点 /dev/ppportX，其中 X 是并行端口编号。应用程序可以打开 /dev/ppportX，通过 read()/write() 系统调用交换数据，并发出各种 ioctl() 命令。使用内核接口（如 ppdev）比直接使用 ioperm()、iopl() 或 /dev/port 操作 I/O 端口更可取。前一种技术更安全，适用于跨架构，并且支持不同的设备外形规格（如 USB 转并行转换器）。

考虑你在第 5 章中使用的简单 LED 板。它有 8 个 LED，连接到标准 25 针并行连接器的 2 到 9 号引脚上。列表 19.3 使用 ppdev 接口实现了一个简单的用户应用程序，在该并行端口 LED 板上点亮交替的发光二极管。它是第 5 章中列表 5.6 开发的内核驱动程序的等效用户空间版本。

### 列表 19.3. 从用户空间控制并行端口 LED 板

```c
#include <stdio.h>
#include <linux/ioctl.h>
#include <linux/parport.h>
#include <linux/ppdev.h>
#include <fcntl.h>

int main(int argc, char *argv[])
{
    int led_fd;
    char data = 0xAA; /* 用于点亮交替 LED 的位模式 */

    /* 打开 /dev/parport0。假设 LED 连接板
       连接到计算机上的第一个并行端口 */
    if ((led_fd = open("/dev/parport0", O_RDWR)) < 0) {
        perror("Bad Open\n");
        exit(1);
    }

    /* 请求该端口 */
    if (ioctl(led_fd, PPCLAIM)) {
        perror("Bad Claim\n");
        exit(2);
    }

    /* 将引脚设置为正向方向并写入一个
       字节以点亮交替 LED */
    if (ioctl(led_fd, PPWDATA, &data)) {
        perror("Bad Write\n");
        exit(3);
    }

    /* 释放该端口 */
    if (ioctl(led_fd, PPRELEASE)) {
        perror("Bad Release\n");
        exit(4);
    }

    /* 关闭 /dev/parport0 */
    close(led_fd);
}
```

## 访问内存区域

将文件映射（或 *mmaping*）到内存会将其与用户虚拟内存的一个区域关联。由于 Linux 将设备视为文件，你还可以将设备内存映射到 RAM，并直接从用户空间对其进行操作。以下是一些 Linux 上的 `mmap()` 用户：

- 1. 图形用户界面，如 X Windows（[www.xfere86.org](http://www.xfere86.org)）和 SVGAlib（[www.svgalib.org](http://www.svgalib.org)），它们映射视频内存并直接访问图形硬件。
- 2. *Madplay* 是一个仅使用整数的 MP3 播放器，可运行在多种架构上。内存映射提高了吞吐量，因此 madplay 映射 MP3 文件以实现更快的访问。这有助于维持高质量音乐播放所需的正确比特率。
- 3. MPEG（*活动图像专家组*）解码器通过直接操作映射的帧缓冲区内存来播放电影。

`mmap()` 系统调用的原型如下：

```c
void *mmap(void *start, size_t length, int prot, int flag,
int fd, off_t offset);
```

这请求内核将文件描述符 `fd` 指定的设备文件与从 `start` 开始的用户内存块关联。（`start` 只是一个首选值，通常设置为 0；实际关联的内存由 `mmap()` 返回。）内核映射从指定文件中 `offset` 处开始的 `length` 字节内存，`prot` 指定期望的访问保护，`flag` 描述映射的类型。`MAP_SHARED` 标志会将你对同一内存区域的修改镜像给其他使用者，而 `MAP_PRIVATE` 则将你的更改仅保留给你自己。

所有映射的页面都不一定存在于物理内存中。未被访问的区域可以位于交换空间中，它们会按需调入。底层设备驱动程序可以通过实现 `mmap()` 方法来控制 `mmap()` 系统调用的语义。

**列表 19.4** 是一个图像显示程序，演示了 `mmap()` 的用法如下：

- 映射帧缓冲区。（我们在**第 12 章**“视频驱动程序”中讨论了帧缓冲区驱动程序。）
- 映射图像文件。
- 根据图像文件的属性执行必要的转换后，将后者传输到前者（未在列表代码中显示）。

### 列表 19.4. 使用 Mmap 显示图像
