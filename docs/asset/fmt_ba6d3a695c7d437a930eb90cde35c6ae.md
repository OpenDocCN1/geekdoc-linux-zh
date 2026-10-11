
`__kernel_susecond_t` `tv_usec`;  /* 微秒 */

};

将描述驱动程序的主要代码部分：

- 1. 包含头文件，该文件定义了 `_gettimeofday()` 函数原型：
  ```c
  #include <linux/time.h>
  ```
- 2. 在 `#include` 语句之后，声明一个 `struct timeval` 结构体，用于在模块加载和卸载时存储时间：
  ```c
  static struct timeval start_time;
  ```
- 3. 当模块加载时，计算时间差：
  ```c
  pr_info("Unloading module after %ld seconds\n",
         end_time.tv_sec - start_time.tv_sec);
  ```

请参阅接下来的列表 3-4，查看针对 i.MX7D 处理器的“helloworld 计时”驱动程序源码 (`helloworld_imx_with_timing.c`)。

注意：SAMA5D2 (`helloworld_sam_with_timing.c`) 和 BCM2837 (`helloworld_rpi_with_timing.c`) 驱动的源码可以从本书的 GitHub 仓库下载。

## 列表 3-4: helloworld_imx_with_timing

### 最简单的驱动程序

```c
pr_info("Loading first!\n");

say_hello();

return 0;

}

static void __exit_first_exit(void)

{

struct timeval end_time;

do_getimeofday(&end_time);

pr_info("Unloading module after %ld seconds\n",

      end_time.tv_sec - start_time.tv_sec);

say_hello();

}
```

`module_init(first_init);`
`module_exit(first_exit);`

`MODULE_LICENSE("GPL");`
`MODULE_AUTHOR("Alberto Liberal@arroweurope.com");`
`MODULE_DESCRIPTION("这是一个打印自加载以来 \
经过时间的模块");`

### helloworld_imx_with_timing.ko 演示

```bash
root@imx7dsabres:~# insmod helloworld_imx_with_timing.ko /* 插入模块 *
root@imx7dsabres:~# rmmod helloworld_imx_with_timing.ko /* 移除模块 *
root@imx7dsabres:~# insmod helloworld_imx_with_timing num=20 /* 带有参数值再次插入模块 */
```

```bash
/* 使用 sysfs 文件系统读取参数值 */
root@imx7dsabres:~# cat /sys/module/helloworld_imx_with_timing/parameters/num
root@imx7dsabres:~# rmmod helloworld_imx_with_timing.ko /* 移除模块 */
```

## 字符驱动程序

通常，操作系统的设计旨在向用户或应用程序隐藏底层的硬件细节。然而，应用程序确实需要访问硬件外设捕获的数据，以及通过输出驱动外设的能力。只有 Linux 内核可以访问外设寄存器，只有内核能够收集由这些外设设备采集的数据流。

Linux 需要一种从内核传输数据到用户空间的机制。这种数据传输通过设备节点（也称为虚拟文件）处理。设备节点存在于根文件系统中，尽管它们并不是真正的文件。当用户从设备节点读取数据时，内核会将底层驱动程序捕获的数据拷贝到应用程序内存空间。当用户向设备节点写入数据时，内核会将应用程序提供的数据流拷贝到驱动的数据缓冲区，最终通过底层硬件输出。用户应用程序可以使用标准系统调用对虚拟文件进行“打开”、“读取”或“写入”。

每个设备都有一个唯一的驱动程序来处理来自用户应用程序的请求，这些请求最终会传递给核心。Linux 支持三种类型的设备：字符设备、块设备和网络设备。虽然概念相同，但每种设备驱动程序的区别在于文件被“打开”、“读取”或“写入”的方式。字符设备是最常见的设备，它们被直接读写而不经过缓冲，例如键盘、显示器、打印机、串口等。块设备只能以块大小的倍数进行写入和读取，块大小通常为 512 或 1024 字节。它们可以被随机访问，即无论任何块在设备上的什么位置，都可以进行读取或写入。块设备的经典示例是硬盘驱动。网络设备通过 BSD socket 接口和网络子系统访问。

字符设备通过列表第一列中的 `c` 标识，块设备通过 `b` 标识。每个设备都提供了访问权限、所有者和组。

# 第 4 章

从应用程序的角度来看，字符设备本质上是一个文件。进程只知道 `/dev` 文件路径。进程使用 `open()` 系统调用打开文件，并执行 `read()` 和 `write()` 等标准文件操作。

为了实现这一点，字符驱动程序必须实现在 `include/linux/fs.h` 中定义的 `struct file_operations` 结构体中描述的操作并注册它们。在下方的 `struct file_operations` 结构体中仅显示了字符驱动程序的一些最常用操作：

```c
struct file_operations {
struct module *owner;
loff_t (*llseek) (struct file *, loff_t, int);
size_t (*read) (struct file *, const char __user *, size_t, loff_t *);
size_t (*write) (struct file *, const char __user *, size_t, loff_t *);
long (*unlocked_ioctl) (struct file *, unsigned int, unsigned long);
int (*mmap) (struct file *, struct vm_area_struct *);
int (*open) (struct inode *, struct file *);
int (*release) (struct inode *, struct file *);
};
```

Linux 文件系统层确保当用户应用程序调用相应的系统调用时，调用驱动的操作（在内核侧实现并注册回调）。

![](img/6ae71abd6b0ad65121457824655274b93_0.png) 第 4 章

## 字符驱动程序

内核驱动将使用特定的函数 `copy_from_user()` 和 `copy_to_user()` 与用户空间交换数据，如图。

`read()` 和 `write()` 方法在发生错误时返回负值。大于或等于 0 的返回值则告诉调用程序传输了多少字节。实现这种约定显然需要你的驱动程序记录错误以便以便后返回。

`read()` 的返回值由调用程序解释如下：

- 1. 如果值等于传递的 `count`，则请求的字节数已传输。这是理想情况。
- 2. 如果值为正数但小于 `count`，则只传输了部分数据。这出于多种原因，取决于设备。大多数应用程序会重试读取。如果值为 0，则到达文件末尾。
- 3. 负值表示发生了错误。该值指定了错误类型，根据 `<linux/errno.h>`。

在 Linux 中，每个设备通过两个数字标识：主号和设备号。这些数字可以通过执行 `ls -l /dev` 查看。每个驱动程序向内核注册其主号并完全负责管理其设备号。访问设备文件时，主号选择调用哪个驱动来执行输入输出操作。设备号的作用取决于设备，并在驱动内部处理。例如，i.MX7D 有多个硬件端口。同一个驱动可以控制所有的 UART，但每个物理 UART 都需要自己的设备节点，因此这些 UART 的设备节点将具有相同的主号，但具有唯一的设备号。

## 实验 4.1：“helloworld 字符”模块

通常 Linux 系统传统使用静态设备创建方法，无论相应的硬件设备是否存在，都会在 `/dev` 下创建大量的设备节点（有时成千上万个）。这通常通过 `MAKEDEV` 脚本完成，该脚本包含对 `mknod` 程序的多次调用。

# http://www.rejoiceblog.com/

字符驱动程序 第 4 章

带有世界上可能存在的每一个设备相关的主设备号和次设备号。

这现在不是创建设备节点的正确方法，因为你必须手动创建一个块设备或字符设备文件项并将其与设备关联，如下面的 iMX7D 目标终端命令行所示：

```
root@imx7dsabres:~# mknod /dev/mydev c 2 108
```
