
## 8.1 Hello World 模块示例

```c
static int __init hello_init(void)
{
    printf("Hello Init - debug mode is %s\n",
           debug_enable ? "enabled" : "disabled");
    return 0;
}

static void __exit hello_exit(void)
{
    printf("Hello Exit\n");
}

module_init(hello_init);
module_exit(hello_exit);

MODULE_AUTHOR("Chris Hall");
MODULE_DESCRIPTION("Hello Example");
MODULE_LICENSE("GPL");
```

## 8.2 模块工具

列表 8-5 简要介绍了工具。在那里我们使用模块工具 `modprobe` 从运行的 Linux 内核中插入和移除设备驱动。许多小工具用于管理设备驱动程序。本节介绍了它们。鼓励你参考每个工具的帮助页以获取完整细节。如果你想了解更多关于加载模块和 Linux 内核交互的信息，请查看这些工具的源码。本章末尾的章节告诉你可以在哪里找到它们。

### 8.2.1 insmod

`insmod` 工具是将模块插入运行中内核的最简单方法。我们提供完整的路径，`insmod` 会完成工作。例如：

```bash
$ insmod /lib/modules/$(uname -r)/kernel/drivers/char/examples/hello.ko
```

这会将模块 `hello.ko` 加载到内核。输出将与列表 8-5 所示——即 Hello 消息。`insmod` 工具是一个简单的程序，不需要也不接受任何命令行选项。它需要完整的路径，因为它没有搜索模块的逻辑。通常情况下，你

### 8.2.2 lsmod

`lsmod` 工具也很简单。它只是显示已插入内核的模块的格式化列表。最近的版本不接受任何参数，仅格式化 `/proc/modules` 的输出。列表 8-7 是 `lsmod` 输出的示例。

**列表 8-7 lsmod 输出格式**

| 模块 | Size | Used by |
|---|---|---|
| ext3 | 121096 | 0 |
| jbd | 49656 | 1 ext3 |
| loop | 12712 | 0 |
| hellol | 1412 | 0 |

最右侧的一列“Used by”表示该设备驱动模块正在被使用，并显示依赖链。在这个示例中，`jbd` 模块（日志文件系统的日志程序）正被 `ext3` 模块使用，许多流行的 Linux 桌面发行版的默认日志文件系统。这意味着 `ext3` 设备驱动依赖于 `jbd` 的存在。

### 8.2.3 modprobe

这就是 `modprobe` 的明智之处。列表 8-7 显示了 `ext3` 和 `jbd` 模块之间的关系。`ext3` 模块依赖于 `jbd` 模块。`modprobe` 工具可以发现这种关系并按顺序加载依赖模块。以下命令同时加载 `jbd.ko` 和 `ext3.ko` 驱动模块：

```bash
$ modprobe ext3
```

`modprobe` 工具具有多个控制其行为的命令行。正如我们之前看到的，`modprobe` 可用于删除模块，包括 `/proc/modules` 中的模块（它是 `/proc` 文件系统的一部分，在第 9 章“文件系统”中介绍）。

它由名为 `modprobe.conf` 的配置文件驱动。这允许系统开发人员将设备与设备驱动关联起来。对于简单的嵌入式系统，`modprobe.conf` 可能是空的，或者只包含极少数行。`modprobe` 工具编译时带有一默认规则，在没有有效的 `modprobe.conf` 的情况下建立这些默认值。仅使用 `-c` 调用 `modprobe` 会显示 `modprobe` 使用的默认规则集。

列表 8-8 显示了一个典型的 `modprobe.conf`，它可能出现在包含两个以太网接口的系统中。一个是基于 Prism2 芯片的无线适配器，另一个是典型的 PCI 以太网卡。该系统还包含一个在集成 Intel 声学芯片上的音频子系统。

**列表 8-8 典型的 modprobe.conf 文件**

```bash
$ cat /etc/modprobe.conf
alias eth1 orinoco_pci
options eth1 orinoco_debug=9
alias eth0 e100
alias snd-card-0 snd-intel8x0
options snd-card-0 index=0
```

当内核启动并发现无线芯片组时，该配置文件指示 `modprobe` 加载 `orinoco_pci` 设备驱动，并绑定到内核设备 `eth1`。它向设备驱动传递了可选的模块参数 `orinoco_debug=9`。在发现声卡硬件时也会采取相同的操作。注意与声卡 `snd-intel8x0` 关联的可选参数。

注意，`modprobe.conf` 的功能在很大程度上已被 `udev` 的功能所取代。这在第 19 章中有介绍。然而，你可能会在旧的嵌入式系统中发现 `modprobe.conf`；了解如何配置它可能会很有帮助。

### 8.2.4 depmod

`modprobe` 如何知道给定模块的依赖关系？`depmod` 工具在此过程中起着关键作用。当执行 `modprobe` 时，它会在模块安装的相同目录中搜索名为 `modules.dep` 的文件。`depmod` 工具创建了此模块依赖文件。

该文件包含了内核构建系统配置的所有模块列表，以及每个模块的依赖信息。这是一种简单的格式，每个设备驱动模块占据文件中的一行。如果模块有依赖项，它们将按顺序在模块名称之后列出。例如，在列表 8-7 中，我们看到 `ext3` 模块依赖于 `jbd` 模块。`modules.dep` 中的依赖行看起来像这样：

```
ext3.ko: jbd.ko
```

在实践中，每个模块名称之前都有其在文件系统中的绝对路径，以避免歧义。为了可读性，我们省略了路径信息。更复杂的依赖关系（例如声学驱动）可能如下：

```
snd-intel8x0.ko: snd-ac97-codec.ko snd-pcm.ko snd-timer.ko \
snd.soundcore.ko snd-page-alloc.ko
```

再次，为了可读性，我们删除了前面的路径组件。`modules.dep` 文件中的每个模块文件名都是绝对文件名，具有完整的路径信息，并存在于单行中。之前的示例之所以跨两行是为了适应页面宽度。

通常，`depmod` 在内核构建期间自动运行。然而，在交叉开发环境中，你必须有一个交叉版本的 `depmod`，它需要知道如何读取以目标架构原生格式编译的模块。或者，大多数嵌入式发行版都有一种方法和初始化脚本条目，在每次构建时运行 `depmod`。

### 8.2.5 rmmod

`rmmod` 工具也很简单。它只是从正在运行的内核中移除一个模块。

```bash
$ modprobe -r ext3
```

这里唯一的有趣点是，当你使用 `rmmod` 时，它会执行模块的退出函数。

### 8.2.6 modinfo

`modinfo` 工具提供有关模块的信息。它对于检查模块支持哪些参数特别有用。

**列表 8-9 modinfo 输出**

```bash
$ modinfo hello.ko
filename:      /lib/modules/.../hello.ko
license:        GPL
description:   Hello World
author:         Chris Hall
ver:            2.6.0-0750
parm:           debug_enable:Enable module debug. (int)
```

## 8.3 扩展设备驱动示例

**列表 8-10 扩展的 Hello 设备驱动**

```c
static int hello_open(struct inode *inode, struct file *file)
{
    printf("hello_open: successful\n");
    return 0;
}

static int hello_release(struct inode *inode, struct file *file)
{
    printf("hello_release: successful\n");
    return 0;
}

static ssize_t hello_read(struct file *file, char *buf, size_t count,
    loff_t *ptr)
{
    printf("hello_read: returning zero bytes\n");
    return 0;
}

static ssize_t hello_write(struct file *file, const char *buf,
    size_t count, loff_t *ppos)
{
    printf("hello_write: accepting zero bytes\n");
    return 0;
}

static int hello_ioctl(struct inode *inode, struct file *file,
    unsigned int cmd, unsigned long arg)
{
    printf("hello_ioctl: cmd=%ld, arg=%ld\n", cmd, arg);
    return 0;
}

static int __init hello_init(void)
{
    int ret;
    printf("Hello Example Init - debug mode is %s\n",
        debug_enable ? "enabled" : "disabled");
    ret = register_chrdev(HELLO_MAJOR, "hello_", &hello_fops);
    if (ret < 0) {
        printf("Error registering hello device\n");
        goto hello_fail;
    }
    printf("Hello: registered module successfully!\n");
    /* Init processing here... */
    return 0;

hello_fail:
    return ret;
}

static void __exit hello_exit(void)
{
    printk("Hello Example Exit\n");
}

struct file_operations hello_fops = {
    .owner:      THIS_MODULE,
    .read:       hello_read,
    .write:      hello_write,
    .ioctl:      hello_ioctl,
    .open:       hello_open,
    .release:    hello_release,
};

module_init(hello_init);
module_exit(hello_exit);
```

## 8.3 驱动程序方法

这个扩展的设备驱动程序示例包含了许多新行。从顶部开始，我们必须添加一个新的内核头文件，以获取文件系统操作的定义。我们还为我们的设备驱动程序定义了一个魔数。这不是分配设备驱动程序编号的正确方法。请参考 Linux 内核文档 `../Documentation/devices.txt` 或关于设备驱动的优秀书籍来获取主设备号分配的指导。对于这个简单的示例，我们简单地选择了一个系统中未知的编号。

接下来我们看到了新函数的定义——我们的打开（open）、关闭（close）、读取（read）和写入方法。遵循良好的编码实践，我们采用了一致的命名方案，这将有助于代码的可读性和可维护性。我们的新方法分别称为 `hello_open()`、`hello_release()`、`hello_read()` 和 `hello_write()`。为了这个简单练习的目的，它们是“无所作为”的函数，只需向内核日志子系统打印消息。

注意，我们还添加了一个新函数来调用我们的 `hello_init()` 例程。该行向内核注册了我们的设备驱动程序。通过该注册调用，我们传递了一个包含所需方法指针的结构体。内核使用这个类型为 `struct file_operations` 的结构体，将我们的特定设备函数与文件系统的相应请求绑定。当应用程序通过我们的设备驱动程序打开设备并请求 `read()` 操作时，文件系统会将该通用的 `read()` 请求与我们模块的 `hello_read()` 函数关联。接下来的章节将详细检查这一过程。

### 8.3.2 设备号的分配

必须指出，书中的示例旨在让你对设备驱动程序的架构有一个整体的认识，以及它们是如何融入大局的。它并不是为了成为一个关于设备驱动程序开发的教程。这个主题在本章末尾列出的两本优秀书籍中有涉及。

尽管如此，但应该注意到，我们在列表 8-10 中分配主设备号的方法已被一种更健壮的方法所取代。通常情况下，你不会在驱动程序中指定设备号。我们允许内核为你指定一个设备号。这避免了设备号的冲突，并且比手动分配自己的设备号具有更好的扩展性。这一过程在本书章末尾引用的《Linux 设备驱动程序》（第3版）第 3 章中进行了详细描述。

### 8.3.3 设备节点与 mknod

为了理解应用程序如何将其请求绑定到由我们的设备驱动程序表示的特定设备，我们必须理解设备节点的概念。设备节点是 Linux 中表示设备的特殊文件类型。几乎所有的 Linux 发行版都将设备节点保留在一个公共位置（由文件系统层次结构指定），即 `/dev` 目录。使用一个专门的工具在文件系统上创建设备节点。该工具被称为 `mknod`。

> ^7 在章末尾会提到。

创建节点的示例是说明其功能及其传达信息的最佳方式。遵循我们简单的设备驱动程序示例，让我们创建一个正确的设备节点来测试它：

```bash
$ mknod /dev/hello1 c 234 0
```

在我们的目标嵌入式系统执行此命令后，我们得到了一个名为 `/dev/hello1` 的新文件，代表我们的设备模块。如果我们列出这个文件，它看起来像：

```bash
$ ls -l /dev/hello1
crw-r--r-- 1 root root 234, 0 May 14 20:05 /dev/hello1
```

## 8.5 构建树外驱动程序

这个在 ARM XScale 系统上编译的简单文件演示了如何通过设备节点将应用程序与设备驱动绑定。像设备驱动一样，它没有执行任何实际工作，但它通过练习我们在列表 8-10 节设备驱动中引入的一些方法，演示了相关概念。

首先，我们在之前创建的设备节点上使用 `open()` 系统调用。如果打开成功，我们将向控制台输出信息。接下来，我们发出 `read()` 命令并在成功后再次向控制台打印信息。注意，对于内核来说，读取 0 字节是完全可以的。在实际操作中，这表示文件结束（EOF）或无数据状态。设备驱动定义了特殊条件。完成后，我们简单地关闭文件并退出。列表 8-12 记录了在 ARM XScale 目标机上运行此示例程序的输出。

**列表 8-12 使用示例驱动**

```bash
$ modprobe helloi
Hello Example Init - debug mode is disabled
Hello: registered module successfully!
./use-hello: entered
./use-hello: open: successful
./use-hello: read: returning zero bytes!
$
```

## 8.5 构建树外驱动程序

在内核源码树之外构建设备驱动程序通常非常方便。使用一个模仿内核源码树中许多模式的简单 Makefile 可以让这项工作变得容易。Linux 内核源码树中的驱动 Makefile 通常非常简单。450 多个 Makefile 中有超过一半的内容少于十行。5% 的只有一行！

如果我们为我们的 `helloi` 示例编写一个在内核树外构建的 Makefile，它可能像这样：

```makefile
obj-$(CONFIG_EXAMPLES)      += helloi.o
```

在任选的目录中创建一个 Makefile，并将 `helloi.c` 源代码放置其中。接下来，在同一目录下创建一个名为 `Makefile` 的新文件。然后它应该包含你刚刚展示的那行代码。然后从该目录（你创建的目录）执行以下构建命令：

```bash
make ARCH=arm CROSS_COMPILE=xscale_be- -C <path/to/your/linux-2.6> SUBDIRS=$PWD modules
```

> * 实际上，`open()` 调用是 Linux `sys_open()` 系统调用的 C 库封装函数。
