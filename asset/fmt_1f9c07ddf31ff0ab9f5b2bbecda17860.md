
在这里，你可以看到我们的系统有 PCI 设备而没有 PCI-Express 设备。列出的每一项实际上都是目录。如果你是设备驱动编写者，这些名称本身包含了有用信息。

sysfs 尝试创建一个与系统硬件紧密模拟的目录层次结构。通过符号链接，通常可以从多个视角获取相同的信息。假设你想通过总线查看 SCSI 设备。在这种情况下，你会在 `/sys/bus/scsi/devices` 中找到你想知道的内容。也许你可以查看 `/sys/block/sda/device`。这两者都链接到同一个目录，该目录包含了关于该设备的各种信息。

SCSI 总线是说明 procfs 和 sysfs 差异的良好示例。使用 procfs，你会发现一个名为 `/proc/scsi` 的驱动，它包含一个每个主机适配器的目录，每个目录通常包含一个每个 SCSI 总线的文件（命名为 0, 1, 2 等）。在其中是驱动编写者认为有用的文件。遗憾的是，编写 Adaptec 驱动的人没有与编写 LSI 驱动的人交流，而后者也从未与编写 BusLogic 驱动的人交流过。结果是，每个驱动程序以完全不同的格式产生相似的信息。这里有一个来自 `aic79xx` SCSI 模块的小示例，它显示了一个连接到 Ultra 320 磁盘阵列的系统：

```bash
$ cat /proc/scsi/aic79xx

Adaptec AIC79xx driver version: 1.3.11

Adaptec AIC7902 Ultra320 SCSI adapter

anaic7902: Ultra320 Wide Channel A, SCSI Id=7, PCI-X 67-100MHz, 512 SCBs
```

## 什么让 sysfs 与众不同？

考虑一个简单的例子，看看使用 sysfs 有么简单。在本书中，调试各种内核时，我使用了这个微不足道的模块来跟踪内部时钟，因为没有系统调用可以获取这些信息。

```c
#include "linux/module.h"

// 将 USER_HZ 宏存储在变量中

int user_hz=HZ;

// 将 HZ 宏存储在变量中

int hz=HZ;

// 只要这些代码就能在 /sys 中可见了！！！

// 我指定了名称、类型和文件权限。

module_param(user_hz,int,0444);

module_param(hz,int,0444);
```

得益于 2.6 编译系统，该模块的`Makefile`同样简单。

```makefile
Makefile:

all:

    make -C /lib/modules/`uname -r`/build M=`pwd` modules

obj-m+=hz.ko
```

要编译并安装此模块，我输入以下命令：

```bash
$ make

$ insmod ./hz.ko
```

现在到了有趣的部分。我可以使用简单的 `cat` 命令从用户空间查看这些变量：

```bash
$ cat /sys/module/hz/parameters/hz

1000

$ cat /sys/module/hz/parameters/user_hz

100
```

所以我用四行代码就有一个实用的模块。不坏。

## 5.4.4 设备与 I/O

通常，在任何数据接触你的应用程序缓冲区之前，它必须通过内核空间。例如，从设备的典型读取会导致数据至少发生两次 I/O 拷贝——一次到内核缓冲区，另一次到你的用户缓冲区。这是我们为可靠性和安全性付出的代价。为了防止一个进程导致内核崩溃或其他进程崩溃，所有的输入和输出必须由内核处理，内核充当安全检查站。

考虑到 UNIX 和 Linux 被视为高性能操作系统，这可能会让你们中的一些人感到意外。事实上，正如你将看到的，额外的拷贝对你有利。理解这些规则和原因可以帮助你最有效地进行 I/O 操作。

### 5.4.4.1 I/O 与字符设备

对于慢速的串口，拷贝所需的额外时间是微不足道的。对于高速设备，这些额外的拷贝可能会成为性能问题。对于自定义硬件，字符设备通常是驱动程序的首选，因为它最直接。读和写是同步的，这意味着通常当进程调用 `read` 或 `write` 时，它会阻塞并且在操作完成之前不会从系统返回¹¹。当你向字符设备写入数据时，驱动程序可能会将数据直接从你的用户空间缓冲区拷贝到设备。这意味着在驱动程序完成该内存之前，它不允许你继续。你的进程会被阻塞，等待写入完成。等待设备的时间是你本可以执行代码的时间，而这通常是不可希望的。我可以用 `/dev/tty` 设备来说说明这一点，它是代表当前终端的字符设备：

```bash
$ dd if=/dev/zero count=1000

1000+ records in

1000 records out
```

```
real 0m.442s

user 0m.000s

sys 0m.020s
```

我只是向终端写了几个 NULL，这除了消耗时间外，对终端什么都没做。在这里，你可以看到该命令执行了 442 毫秒，但只花费了 20 毫秒的 CPU 时间。时间都去哪儿了？花在等待驱动程序上了（阻塞）。进程消耗的极少 CPU 时间被驱动程序使用了（在这里列出为 sys）。

> ¹¹ 实际上比这要微妙一点，但这是大多数设备的默认行为。

终端和串口一样，是一个流式设备。流式设备上是不可能的随机访问的。因此，`read` 和 `write` 系统调用是你用来与此设备交互的唯一调用方法。

允许随机访问的设备通常通过 `mmap` 系统调用看到设备提供的所有数据。这允许应用程序将所有数据视为一个内存区域。字符设备驱动程序可以专门支持 `mmap` 而不允许 `read` 和 `write` 调用。当驱动程序不支持 `mmap` 时，系统调用返回 `MAP_FAILED`，并将 `errno` 设置为 `ENODEV`。

通过 `mmap`，从设备读写数据就像分配大块内存一样简单。对于字符设备，使用 `mmap` 允许你用更少的系统调用访问数据，因为你不需要调用 `read` 或 `write` 来操作数据。当你处理大量数据时，这一点尤为重要（参见侧边栏“一个简单的 `mmap` 示例”）。

### 5.4.4.2 块设备、文件系统与 I/O

块设备是磁盘和其他可以使用文件系统的存储设备的基础。因此，你可以通过两种方式访问块设备：直接访问或通过文件系统。通常，你直接使用块设备的唯一时刻是在对其进行分区或创建文件系统时。

可以在任何块设备或块设备的分区上创建文件系统。软盘驱动程序的独特之处在于它不允许分区，尽管软盘介质支持分区。相反，软盘驱动程序使用的次号（minor numbers）允许了这一点。

要创建一个文件系统，你可以使用

```bash
$ mkfs -t vfat /dev/fd0
```

注意，拷贝的是设备中的数据，而不是设备节点。这是设备节点的独特属性。这种技术用于制作可启动的光盘镜像比制作可启动的软盘镜像要常见得多。如果这是一块硬盘，拷贝整个块设备将保留分区表和主引导记录（如果有）。

如前所述，这不是存档数据的有效方法。块设备不知道多少数据是有效的，多少是空空间。文件系统知道。结果是，每个软盘镜像都是 1440K，无论磁盘上有多少文件。相反，存档将只包含使用的文件，因此潜在上它可以小得多。

```c
#include <stdio.h>

#include <stdlib.h>

#include <string.h>

#include <unistd.h>

#include <fcntl.h>

#include <sys/mman.h>

#include <sys/types.h>

#define ERROR(x) do { perror(x); exit(EXIT_FAILURE); } while (0)

int main(int argc, char *argv[]) {

    const int nbytes = 4096;

    void *ptr;

    int fd = open("/dev/zero", O_RDWR);

    if (fd == -1) ERROR("open");

    ptr = mmap(NULL, nbytes, PROT_READ | PROT_WRITE, MAP_SHARED, fd, 0);

    if (ptr == MAP_FAILED) ERROR("mmap");

    memset(ptr, 0, nbytes);

    munmap(ptr, nbytes);

    close(fd);

    return 0;

}
```
