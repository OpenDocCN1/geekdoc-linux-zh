# Linux 内核模块编程指南；内核 2.6




















- 4.1.6. 为多个内核版本构建模块................................................................................26


















# 前言

# 1. 作者

《Linux内核模块编程指南》（The Linux Kernel Module Programming Guide）最初由 Ori Pomerantz 为 2.2 内核编写。最终，Ori 不再有时间维护该文档。毕竟，Linux 内核是一个快速变化的目标。Peter Jay Salzman 接手了维护工作并针对 2.4 内核进行了更新。最后，Peter 也没有时间跟进 2.6 内核的发展，因此 Michael Burian 成为共同维护者，为 2.6 内核更新文档。

# 2. 版本与注意事项

Linux 内核是一个不断变化的目标。一直存在一个问题：LKMPG 是否应该移除过时信息，还是为了历史原因保留它们？Michael Burian 和我决定为每个新的稳定内核版本创建一个 LKMPG 的新分支。因此，LKMPG 2.4.x 版本将针对 Linux 内核 2.4，LKMPG 2.6.x 将针对 Linux 内核 2.6。我们不会尝试存档历史信息；需要这些信息的人应该阅读对应版本的 LKMPG。

源代码和讨论适用于大多数架构，但我无法保证任何事情。例外是第 12 章“中断处理程序”，它在 x86 之外的任何架构上无法工作。

# 3. 致谢

以下人员提供了修正或良好的建议：Ignacio Martin, David Porter, Daniele Paolo Scarpazza, Dimo Velev, Francois Audeon 和 Horst Schirmeier。

# 第1章 引言

### 1.1. 什么是内核模块？

你想写一个内核模块。你熟悉 C 语言，写过几个作为进程运行的程序，现在你想进入真正的领域——在那里，一个野指针就可以抹除你的文件系统，并且需要加载核心转储（core dump）。

内核模块究竟是什么？模块是可以根据需要加载和卸载到内核的代码段。它们可以在不需要重启系统的情况下扩展内核功能。例如，模块的一种类型是设备驱动程序，它允许内核访问连接到系统的硬件。如果没有模块，我们将不得不构建单体内核，并将任何新功能直接添加到内核镜像中。由于内核变大，它的缺点是每当我们想要新功能时，都需要重新编译并重启内核。

### 1.2. 模块是如何进入内核的？

你可以通过运行 `lsmod` 查看哪些模块已经加载到内核中，该命令通过读取 `/proc/modules` 文件获取信息。

这些模块是如何进入内核的？当内核需要一个内核中未驻的功能时，内核守护进程 kmod[1] 会执行 `modprobe` 来加载模块。`modprobe` 以两种形式之一传入参数：

- * 模块名称，如 softdog 或 ppp。
- 更通用的标识符，如 char-major-10-30。

如果传递给 `modprobe` 一个通用标识符，它首先查找 `/etc/modprobe.conf[2]` 文件中的字符串。如果它找到类似下面的别名行：

```
alias char-major-10-30 softdog
```

它就知道通用标识符指的是模块 `softdog.ko`。

接下来，`modprobe` 会遍历 `/lib/modules/version/modules.dep` 文件，查看在加载请求模块之前是否必须加载其他模块。该文件由 `depmod -a` 创建，包含模块依赖关系。例如，mdsos 要求 `fat.ko` 已经加载到内核中。如果另一个模块定义了请求模块使用的符号（变量或函数），则该模块对另一个模块有依赖关系。

最后，`modprobe` 使用 `insmod` 将任何先决模块加载到内核，然后加载请求的模块。`insmod` 指向 `/lib/modules/version/[3]`，这是模块的标准目录。`insmod` 设计初衷是对模块的位置相当“迟钝的”，而 `modprobe` 则感知模块的位置、如何确定依赖关系并按正确的顺序加载模块。例如，如果你想加载 mdsos 模块，必须运行：

```
insmod /lib/modules/2.6.11/kernel/fs/fat.ko
insmod /lib/modules/2.6.11/kernel/fs/mdsos.ko
```

或者：

```
modprobe msdos
```

我们在这里看到：**insmod** 要求你传递完整路径并按正确的顺序插入模块，而 **modprobe** 只接受名称（不带扩展名），并通过解析 `/lib/modules/version/modules.dep` 来获取它需要的所有信息。

Linux 发行版通过一个名为 `module–init-tools` 的包提供了 `modprobe`、`insmod` 和 `depmod`。在之前的版本中，该包被称为 `modules`。某些发行版还设置了封装器，允许这两个包并行安装并执行正确的操作，以便处理 2.4 和 2.6 内核。用户不需要关心这些细节，因为他们运行的是这些工具最新版本。

现在你知道模块是如何进入内核的。如果你想编写依赖于其他模块的模块（这被称为“堆栈模块”），故事还有更多。但这将留到以后的章节。在讨论这个层级问题之前，我们必须涵盖更多内容。

### 1.2.1. 在开始之前

在我们引入代码之前，有几个问题需要我们涵盖。每个人的系统都是不同的，每个人都有自己的节奏。（注：原文此处存在大量重复性文本，已按要求进行逻辑处理）。






## 2.1.1. 介绍 printk()

尽管你可能认为并非如此，printk() 并不是为了向用户传递信息，尽管我们在 hello! 示例中正是为此目的使用它。它恰好是内核的日志机制，用于记录信息或警告。因此，printk() 语句带有优先级，即你看到的 `<1>` 和 `KERN_ALERT`。共有 8 种优先级，内核为它们提供了许多定义，你不需要使用晦懂的数字，可以在 `linux/kernel.h` 中查看它们。如果你不使用优先级级别，将使用默认优先级 `DEFAULT_MESSAGE_LOGLEVEL`。

花点时间阅读这些优先级宏。头文件也描述了每个优先级的含义。在实践中，请始终使用数字，例如 `<4>`，如 `KERN_WARNING`。

如果优先级小于 `const console_loglevel`，消息将打印到你当前的终端。通过 `syslog` 和 `klog`，消息也会追加到 `/var/log/messages`，无论它是否打印到控制台。我们使用高优先级 `KERN_ALERT` 来确保 printk() 消息打印到你的控制台，而不仅仅是记录到日志中。当你编写模块时，你会使用对当前情况有意义的优先级。

## 2.2. 编译内核模块

内核模块的编译与普通用户应用程序不同。旧版本的内核要求我们进行这些设置，这些设置大多存储在 Makefile 中。尽管按层级结构组织，但子级 Makefile 中累积了许多冗余赋值，导致它们变得巨大且难以维护。遗憾的是，现在有一种处理这些事务的新方法 `kbuild`，并且外部可加载模块的构建过程现在已完全集成到标准的内核构建机制中。有关如何编译不属于官方内核的模块（如本指南中找到的所有示例），请参见 `linux/Documentation/kbuild/modules.txt`。

现在，让我们来看编译名为 `hello-1.c` 模块的 Makefile：

### 示例 2–2. 基础内核模块的 Makefile

```
obj-m += hello-1.o

all:
    make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules

clean:
    make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean
```

从技术角度来看，第一行是绝对必要的，`all` 和 `clean` 目标是为了方便而添加的。

现在你可以通过执行命令 `make ..` 来编译模块。你会得到类似下面的输出：

```
hostname:~/lkmp-examples/02-HelloWorld# make
make -C /lib/modules/2.6.11/build M=/root/lkmp-examples/02-HelloWorld
[1]: Entering directory /usr/src/linux-2.6.11
CC [M] /root/lkmp-examples/02-HelloWorld/hello-1.o
Building modules, stage 2.
MODPOST
```
CC /root/kmpkg-examples/02-HelloWorld/hello-1.mod.o
LD [M] /root/kmpkg-examples/02-HelloWorld/hello-1.ko
make[1]: Leaving directory '/usr/src/linux-2.6.11'
hostname:/root/kmpkg-examples/02-HelloWorld#
```

注意，内核 2.0 引入了新的命名规范：内核模块具有 `.ko` 扩展（代替 `.o` 扩展），以将其与传统的对象文件区分开。其原因是它们可以包含一个额外的 `.modinfo` 段，其中写入了关于模块的额外信息。我们将继续这些额外信息的用途。

使用 `modinfo-*` 查看它是什么类型的信息。

```
hostname:/kmpkg-examples/02-HelloWorld# modinfo hello-1.ko
filename: hello-1.ko
vermagic: 2.6.11 SMP PREEMPT_64 gcc-3.3
depends:
```

没什么特别的，这样我们在稍后的一个示例 `hello-5.ko` 中使用了 `modinfo`。

```
hostname:/kmpkg-examples/02-HelloWorld# modinfo hello-5.ko
filename: hello-5.ko
license: GPL
author: Peter Salomon
vermagic: 2.6.11 SMP PREEMPT_64 gcc-3.3
depends:
parm: myArray: character string (array of int)
parm: mystring: character (char)
parm: mylong: long integer (long)
parm: myint: integer (int)
parm: myshort: short (short)
```

关于内核这里有很多有用信息：作者、许可证信息，甚至还有它接受的参数的简短描述。内核模块 Makefile 的更多细节可以在 `linux/Documentation/kbuild/makefiles.txt` 中找到。确保阅读该文件并开始编写 Makefile。

现在是时候用 `insmod hello-1.ko` 将你新编译的模块插入内核了（忽略任何关于内核污染的提示；稍后我们会介绍）。所有加载到内核的模块都在 `/proc/modules` 中。去检查你的模块是否真的加载到了内核。恭喜，你现在是内核代码作者了！使用 `rmmod hello-1` 从内核中移除模块。查看 `/var/log/messages` 查看它被记录到了你的系统中。这是给读者的另一个练习：关于 `init_module()` 返回语句，将其值改为负数，重新编译并加载模块。发生了什么？

## 2.3. Hello World（部分 2）

从 Linux 2.4 开始，你可以重命名模块的 init 和清理函数；它们不再需要分别调用 `init_module()` 和 `cleanup_module()`。这是通过 `module_init()` 和 `module_exit()` 宏实现的。这些宏定义在 `linux/init.h` 中。唯一的注意事项是在必须调用宏之前定义 init 和清理函数，否则你会得到编译错误。这是一个这种技术的示例：

### 示例 2-3. hello-2.c

```
/*
* hello-2.c 展示了 module_init() 和 module_exit() 宏。
* 这比 init_module() 和 cleanup_module() 更好。
 */
#include <linux/module.h>    /* 所有模块需要 */
#include <linux/kernel.h>    /* KERN_INFO 需要 */
#include <linux/init.h>      /* 宏需要 */
static int __init hello_2_init(void)
{
    printk(KERN_INFO, "Hello, world 2");
    return 0;
}
static void __exit hello_2_exit(void)
{
    printk(KERN_INFO, "Goodbye, world 2");
}
module_init(hello_2_init);
module_exit(hello_2_exit);
```

现在我们已经掌握了两个内核模块。添加另一个模块简单如下：

### 示例 2-4. 模块的 Makefile

```
obj-m += hello-1.o
obj-m += hello-2.o

all:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD)

clean:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean
```

现在看看真实世界的 `linux/drivers/char/Makefile`。如你所示，某些内容被硬化进内核（obj-y），但也有 `obj-m` 模块。熟悉脚本的人可以很容易识别它们。不熟悉的人，`obj-CONFIG_FOO` 显示随随处展开为 `obj-y` 或 `obj-m`，取决于 `CONFIG_FOO` 变量是否被设置为 `y` 或 `m`。说起来，这些正是你上一次使用 `menuconfig` 或类似工具时在 `linux/.config` 文件中设置的变量。

## 2.4 Hello World（部分 3）：__init 和 __exit 宏

这演示了内核 2.2 及更高版本的一个特性。注意 init 和清理函数定义中的变化。`__init` 宏允许函数在内置驱动程序的 init 函数完成后被丢弃并释放其内存，但对于可加载模块则不然。如果你考虑 init 函数被调用的时，这是很有意义的。还有 `__initdata`，它的工作方式类似于 `__init`，但针对初始化变量而不是函数。

`__exit` 宏导致在模块构建进内核时省略该函数，且与 `__exit` 一样，对可加载模块没有影响。再次，如果你考虑清理函数的运行，这完全合理：内置驱动程序不需要清理函数，而可加载模块需要。

这些宏定义在 `linux/init.h` 中，用于释放内核内存。当你启动内核并看到类似 `Freeing unused kernel memory: 236k freed` 时，这正是正在释放的内容。

### 示例 2-5. hello-3.c

```c
/*
* hello-3.c - 阐释 __init, __initdata 和 __exit 宏。
 */
#include <linux/module.h>    /* 所有模块需要 */
#include <linux/kernel.h>    /* KERN_INFO 需要 */
#include <linux/init.h>      /* 宏需要 */

static int hello_3_data __initdata = 3;
static int __init hello_3_init(void)
{
    printk(KERN_INFO, "Hello, world %d\n", hello_3_data);
    return 0;
}

static void __exit hello_3_exit(void)
{
    printk(KERN_INFO, "Goodbye, world 3\n");
}
```

## 2.5. Hello World（部分 4）：许可与模块文档

如果你运行内核 2.4 或更高版本，在加载专用模块时可能会看到类似的内容：

```
# insmod xxxxx.o
Warning: loading xxxxx.ko will taint the kernel: no license
See http://www.tux.org/linux/lml/#export-tainted 获取有关污染模块的信息
Module xxxxx loaded, with warnings
```

在内核 2.4 之后，设计了一种机制来识别 GPL（及其伙伴）的代码，以便警告人们代码不是开源的。这是通过 `MODULE_LICENSE()` 宏实现的，如下一段代码所示。通过将许可设置为 `GPL`，你可以防止警告的打印。这种许可机制在 `linux/module.h` 中定义并文档化：

+   * 以下许可标识目前被接受为表示自由






- 软件模块
- "GPL" [GNU 公共许可证 v2 或更高版本]
- "GPL v2" [GNU 公共许可证 v2]
- "GPL 及额外权利" [GNU 公共许可证 v2 权利及更多]
- "双 BSD/GPL" [GNU 公共许可证 v2 或 BSD 许可证可选]
- "双 MIT/GPL" [GNU 公共许可证 v2 或 MIT 许可证可选]
- "双 MPL/GPL" [GNU 公共许可证 v2 或 Mozilla 许可证可选]

- 还有其他标识可用
    - "专有" [非自由产品]
- 存在双重许可组件，但在 Linux 上运行时，相关的是 GPL，因此这不是一个问题。同样，与 GPL 关联的 LGPL 是一个 GPL 组合工作。

- 这种存在有几个原因：
    - 1. 让 modinfo 可以为想要免费验证其设置的用户显示许可证信息
    - 2. 让社区可以忽略包含私有模块在内的错误报告
    - 3. 让厂商可以同样根据自己的策略行事

同样，`MODULE_DESCRIPTION()` 用于描述模块的功能，`MODULE_AUTHOR()` 声明模块作者，而 `MODULE_SUPPORTED_DEVICE()` 声明模块支持的设备类型。

这些宏都定义在 `linux/module.h` 中，并由内核本身定义。它们对于文档来说非常简单，可以通过像 `admire` 这样的工具查看。作为一个练习，读者们，请尝试查看这些宏如何使用 `linux/drivers` 来记录它们的模块。

我建议在 `/usr/src/linux-2.6.x/` 中使用 `grep -in MODULE_AUTHOR *`。不熟悉命令行工具的用户可能更喜欢基于 Web 的解决方案，搜索内核树已被 LXR 索引的站点（或在你的本地机器上设置它）。

使用 emacs 或 vi 等传统编辑器的用户也会发现标签文件（tag files）有用。它们可以通过 `make tags` 或 `/usr/src/linux-2.6.x/` 中的 `tags` 生成。一旦你在内核树中获得了标签文件，就可以将光标放在函数调用上，并使用某些组合键直接跳转到定义函数。

### 示例 2-6. hello-4.c

```c
/*
* hello-4.c - 模块文档。
 */
#include <linux/module.h> /* 所有模块都需要 *
#include <linux/kernel.h> /* KERN_INFO 需要 *
#include <linux/init.h> /* 宏需要 *
#define DRIVER_AUTHOR "Peter Jayman <p@dirac.org>"
#define DRIVER_DESC "A 示例驱动程序"

static int __init init_hello_4(void)
{
    printk(KERN_INFO "Hello, world 4\n");
    return 0;
}
static void __exit cleanup_hello_4(void)
{
    printk(KERN_INFO "Goodbye, world 4\n");
}
module_init(init_hello_4);
module_exit(cleanup_hello_4);
```

```c
/*
 * 你可以使用字符串，如下所示：
 * 通过将代码声明为 GPL 来消除污染信息
 */
MODULE_LICENSE("GPL");

/*
 * 或者使用定义，如下所示：
 */
MODULE_AUTHOR(DRIVER_AUTHOR); /* 谁写了这个模块？ */
MODULE_DESCRIPTION(DRIVER_DESC); /* 这个模块是做什么的？ */

/*
 * 此模块使用 /dev/testdevice。MODULE_SUPPORTED_DEVICE 未来
 * 可能被用于帮助模块的自动配置，但目前除了文档目的
 * 之外未使用。
 */
MODULE_SUPPORT_DEVICE("testdevice");
```

# 2.6. 向模块传递命令行参数

模块可以接受命令行参数，但不是你可能熟悉的 `argc/argv` 方式。

要允许参数传递给你的模块，请将接收命令行参数值的变量声明为全局，并使用 `module_param()` 宏（定义在 `linux/moduleparam.h` 中）来设置机制。在运行时，`insmod` 将用给定的命令行参数填充变量，例如 `/insmod mymodule.ko variable=5`。为了清晰起见，声明和宏应该放在模块的开头。示例代码应该消除我有些松散的解释。

`module_param()` 宏接受 3 个参数：变量名、其类型以及在 sysfs 中对应文件的权限。整数类型可以标记为有符号或无符号。如果你想使用整数或字符串数组，请使用 `module_param_array()` 和 `module_param_string()`。

```c
int myint = 3;
module_param(myint, int, 0);
```

支持数组，但现在的情况与 2.4 时代有所不同。为了跟踪需要传递的参数数量，你需要将计数变量的指针作为第三参数传递。根据你的选择，你也可以忽略计数并传递 `NULL`。我们在这里展示了这两种可能性：

```c
int myintarray[2];
module_param_array(myintarray, int, NULL, 0); /* 不关心计数 */
int myshortarray[4];
int count;
module_param_array(myshortarray, short, &count, 0); /* 将计数放入 "count" 变量中 */
```

这有一个很好的用法是设置模块的默认值，例如端口或 IO 地址。如果设置了模块的默认值，则使用 `module_param()` 宏来记录变量。否则，保持值清晰。最后，`module_param()` 宏用于记录变量。`module_param()` 宏用于记录变量。

### 示例 2-7. hello-5.c

```c
/*
 * hello-5.c - 演示命令行传递
 */
#include <linux/module.h>
#include <linux/moduleparam.h>
#include <linux/kernel.h>
#include <linux/init.h>
#include <linux/fs.h>

MODULE_LICENSE("GPL")
MODULE_AUTHOR("Peter Jayman <p@dirac.org>")
MODULE_DESCRIPTION("A 示例驱动程序")

int myint = 3;
module_param(myint, int, 0);

int myintarray[2];
module_param_array(myintarray, int, NULL, 0);
int myshortarray[4];
int count;
module_param_array(myshortarray, short, &count, 0);

static int __init init_hello_5(void)
{
    int i;
    printk(KERN_INFO "myint = %d\n", myint);
    printk(KERN_INFO "myintarray[0] = %d\n", myintarray[0]);
    printk(KERN_INFO "myintarray[1] = %d\n", myintarray[1]);
    printk(KERN_INFO "myshortarray[0] = %d\n", myshortarray[0]);
    printk(KERN_INFO "myshortarray[1] = %d\n", myshortarray[1]);
    printk(KERN_INFO "myshortarray[2] = %d\n", myshortarray[2]);
    printk(KERN_INFO "myshortarray[3] = %d\n", myshortarray[3]);
    printk(KERN_INFO "count = %d\n", count);
    return 0;
}
static void __exit cleanup_hello_5(void)
{
    printk(KERN_INFO "Goodbye, world 5\n");
}

module_init(init_hello_5);
module_exit(cleanup_hello_5);
```

我建议尝试一下这段代码：

```bash
satan# insmod hello-5.ko myint=10
myint = 10

satan# insmod hello-5.ko myintarray=10,20
myintarray[0] = 10
myintarray[1] = 20

satan# insmod hello-5.ko myshortarray=1,2,3,4
myshortarray[0] = 1
myshortarray[1] = 2
myshortarray[2] = 3
myshortarray[3] = 4
count = 4
```

## 2.7 跨越多个文件的模块

有时将一个内核模块划分到多个源文件中是有意义的。






这是一个此类内核模块的示例。

### 示例 2–8. start.c

```c
/*
 * start.c - 多文件模块的示例
 */

#include <linux/kernel.h>    /* 我们正在进行内核工作 */
#include <linux/module.h>     /* 特别地，一个模块 */

int init_module(void)
{
    printk(KERN_INFO "Hello, world - this is the kernel speaking\n");
    return 0;
}

```

下一个文件是：

### 示例 2–9. stop.c

```c
/*
 * stop.c - 多文件模块的示例
 */

#include <linux/kernel.h>    /* 我们正在进行内核工作 */
#include <linux/module.h>     /* 特别地，一个模块 */

void cleanup_module()
{
    printk(KERN_INFO "Short is the life of a kernel module\n");
}

```

最后是，编译（make）文件：

### 示例 2–10. Makefile

```makefile
obj-m += hello-1.0
obj-m += hello-2.0
obj-m += hello-3.0
obj-m += hello-4.0
obj-m += hello-5.0
obj-m += startstop.o
startstop-objs := start.o stop.o

all:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules

clean:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean
```

这是我们目前为止看到的所有示例的完整 Makefile。前几行没什么特殊，但对于最后一个示例，我们需要两行。首先，我们为组合后的模块发明一个对象名称，其次，我们告诉 make 哪些对象文件属于该模块。

# 第 2 章. Hello World（你好世界）


## 2.8. 为预编译内核构建模块

显然，我们强烈建议你重新编译内核，这样你就可以启用许多用的调试功能，例如强制卸载（MODULE_FORCE_UNLOAD）：当启用此选项时，你可以通过 **rmmod -f module** 在内核认为不安全时强制其卸载模块。此选项可以在开发模块时为你节省大量时间和多次重启。

尽管尽管如此，在某些情况下，你可能想将模块加载到预编译的运行中的内核中，例如与常见 Linux 发行版自带的内核，或者你过去编译过的内核。在某些情况下，你可以编译一个模块并插入到你不允许重新编译的运行内核中，或者插入到一台需要重启的机器上。如果你想不出迫使你为预编译内核使用模块的案例，你可以跳过这里，并将剩余内容视为大麻烦。

现在，如果你安装了内核源码树，用它来编译你的内核模块并尝试将模块插入内核，在大多数情况下，你会得到如下错误：

```
insmod: error inserting 'poet_atkm.ko': -1 Invalid module format
```

不那么异常的情况等于 /var/log/messages：

```
Jun 22:07:54 localhost kernel: poet_atkm: version magic '2.6.5-1.358custom 686 REGPARM 4KSTACK gcc-3' should be '2.6.5-1.358 686 REGPARM 4KSTACK gcc-3'
```

换句话说，你的内核拒绝加载，因为你的模块版本字符串（更准确地说，版本字符串）不匹配。从 **vermagic** 开始：当链接到 **init/vermagic.c** 文件时，版本数据会以静态字符串的形式插入你的模块对象中。






程序执行、调用了哪个函数、参数是什么以及返回什么。这对于找出诸如程序尝试访问的文件等问题来说是一个无价之宝工具。在最后，你会看到一行看起来像 `write(1, "hello", 5)` 的代码。这就是 `printf()` 前面的样子。你可能对此并不熟悉，因为大多数人使用免费的库函数（如 `open`、`fopen`、`fclose`）。正是因为如此，导致了至少发生了 2 次 `write`。第二部分专门介绍系统调用（如 `kill()` 和 `read()`）。第三部分介绍库调用，你可能对这些更熟悉（如 `cosh()` 和 `random()`）。

你可以编写模块来替换内核的系统调用，我们稍后会介绍这一内容。黑客利用这一点创建后门或木马，但你也可以编写自己的模块来做更多良善的事，例如内核 `tee` 模块，它每当有人尝试删除你系统上的文件时，它就会记录。

## 3.1.3. 用户空间与内核空间

内核拥有对资源的所有访问权限，无论该资源是显卡、硬盘还是内存。程序经常会竞争同一个资源。正如我刚刚看到的，`updatedb` 正在更新 `locate` 数据库。我的视觉和 `updatedb` 都在使用硬盘连接。内核需要保持秩序井然，而不是让用户随心所欲地访问任何东西。为此，CPU 可以在不同的模式下运行。每个模式对系统操作都有不同程度的自由度。Intel x86 架构有 4 种这种模式，被称为“环”（rings）。Unix 使用两个环：最高的环（ring 0，也称为“监视模式”，其中允许任何操作发生）和最低的环（称为“用户模式”）。回想关于库函数与系统调用的讨论。通常情况下，你在用户模式下使用库函数。库函数调用一个或多个系统调用，这些系统调用根据库函数的行为执行，但在监视模式下执行，因为它们是内核本身的一部分。一旦系统调用完成任务，执行权就会传回用户空间。

## 3.1.4. 命名空间

当你写一个较小的 C 程序时，你使用的变量既方便又对读者有意义。另一方面，你编写的例程将是一个更大问题的一部分，全局变量可能属于其他人的全局变量；某些变量名会发生冲突。当程序有许多不足以区分意义的全局变量时，就会出现命名空间污染。在大型项目中，必须努力记住保留名称，并找到开发出一套唯一变量名和符号的方案。

在编写内核代码时，最小的模块也将链接到整个内核，因此这绝对是一个问题。处理此问题的最好方法是将变量声明为 `static`，并为它们使用定义良好的前缀。按照惯例，所有前缀都是小写的。如果你不想将一切都声明为 `static`，另一个选项是声明符号表并将其注册到内核。我们稍后会提到这一点。

文件 `/proc/kallsyms` 存储了内核知道的所有符号，由于它们共享内核的代码空间，因此你的模块可以访问这些符号。

## 3.1.5. 代码空间

内存管理是一个非常复杂的主题——O'Reilly 的《理解 Linux 内核》中大部分内容都在讲内存管理！我们并不打算成为内存管理专家，但在甚至开始考虑编写模块之前，我们需要知道几个因素。

如果你考虑过 `segfault`（段错误）的真正含义，你可能会对指针实际上指向内存位置的方式感到惊讶。至少不是真实的地址。当进程被创建时，内核会留出部分物理内存并将其交给该进程，用于其执行代码、变量、栈、堆以及计算机科学家熟悉的其他内容 [5]。这部分内存从 `0x0000000` 开始，延伸到它需要的任何大小。`0xffff978` 将访问真实物理内存中的不同位置！进程将访问一个名为 `0xffff978` 的索引，该索引指向该特定进程留留内存区域的某种偏移。在大多数情况下，像我们的 `Hello, World` 程序这样的进程可以访问另一个进程的空间，尽管我们稍后会讨论其他方法。

内核有它自己的内存空间。由于模块可以从内核中动态插入和移除（作为一个自主对象），内核的代码空间与其自身的空间有所不同。因此，如果你因为一个差一错误（off-by-one error）而修改了内核数据，内核就会崩溃。这比听起来的还要糟糕，所以最好要谨慎。我想指出，上述结论对于任何使用单体内核的操作系统都是成立的。微内核有自己的代码库。Hurd 和 QNX Neutrino 是两个微内核的例子。

## 3.1.6. 设备驱动程序

一类模块是设备驱动程序，它为卡或串口等硬件提供功能。在 Unix 上，每件硬件都由位于 `/dev` 中的文件表示，该文件提供了与硬件通信的手段。设备驱动可以将 `/dev/sound` 设备文件连接到像 `mpblaster` 这样的用户程序，使其在不知道安装了什么种声卡的情况下使用它。

## 3.1.6.1. 主号和次号

让我们来看看设备文件。这里是代表主硬盘分区的设备文件：

```
ls -l /dev/hda*
br-rw---- 1 root disk 3, 1 Jul 5 2000 /dev/hda1
br-rw---- 1 root disk 3, 2 Jul 5 2000 /dev/hda2
br-rw---- 1 root disk 3, 3 Jul 5 2000 /dev/hda3
```

注意输出中逗号分隔的数字。第一个数字是主号（major number），第二个数字是次号（minor number）。主号告诉你使用的是哪个驱动程序。次号则用于区分由同一驱动程序的不同硬件。





# 第 4 章 字符设备文件

## 4.1. 字符设备驱动

### 4.1.1. file_operations 结构

`file_operations` 结构定义在 linux/fs.h 中，它包含了指向驱动程序定义的函数指针，这些函数负责对设备执行各种操作。结构中的每个字段都对应驱动程序定义的用于处理请求操作的函数地址。

例如，每个字符驱动程序都需要定义一个从设备读取的函数。`file_operations` 结构持有执行该操作的模块函数地址。以下是内核 2.6.5 版本的定义：

```c
struct file_operations {
    struct module *owner;
    loff_t(*llseek) (struct file *, loff_t, int);
    ssize_t(*read) (struct file *, char __user *, size_t, loff_t);
    ssize_t(*write) (struct file *, struct ki_ack *, char __user *, size_t, loff_t);
    ssize_t(*aio_write) (struct file *, const char __user *, size_t, loff_t);
    ssize_t(*aio_read) (struct file *, const char __user *, size_t, loff_t);
    int (*add_seek) (struct file *, void *, filldir_t);
    unsigned int (*poll) (struct file *, struct poll_table_struct *);
    int (*ioctl) (struct inode *, struct file *, unsigned int);
    int (*mmap) (struct file *, struct vm_area_struct *);
    int (*open) (struct inode *, struct file *);
    int (*flush) (struct file *);
    int (*release) (struct inode *, struct file *);
    int (*fsync) (struct file *, struct destroy *, int datasync);
    int (*aio_fsync) (struct ki_ack *, int datasync);
    int (*fasync) (struct file *, int, struct file_lock *);
    int (*lock) (struct file *, const struct file_lock *);
    ssize_t(*readv) (struct file *, const struct iovec *, unsigned long, loff_t);
    ssize_t(*writev) (struct file *, struct iovec *, unsigned long, loff_t);
    ssize_t(*sendfile) (struct file *, loff_t, size_t, read_actor_t, __user *);
    ssize_t(*sendpage) (struct file *, struct page *, int_t, loff_t, int);
    unsigned long (*get_unmapped_area) (struct file *, unsigned long, unsigned long, unsigned long);
};
```

某些操作并没有由驱动程序实现。例如，处理显卡的驱动程序就不需要从目录结构中读取内容。`file_operations` 结构中的相应项应设置为 `NULL`。

有一种 gcc 扩展可以让向此结构添加内容变得更加方便。在现代驱动程序中，你会看到可能会让你感到惊讶的内容。这种向结构添加内容的方式如下：

![](img/012b87801a83171d68e1e1da140117be_23_0.png)

```c
struct file_operations fops = {
  .read = device_read,
  .write = device_write,
  .open = device_open,
  .release = device_release
};
```

然而，还有一种 C99 的方式来为结构赋值元素，这明显优于 GNU 扩展。我们编写本文时使用的 gcc 版本 2.95 已经支持这种新的 C99 语法。如果有人想移植你的驱动程序，你应该使用这种语法。这有助于兼容性：

```c
struct file_operations fops = {
  .read = device_read,
  .write = device_write,
  .open = device_open,
  .release = device_release
};
```

它的意思是（你也应该意识到这一点），结构中任何你没有显式赋值的成员都将被 gcc 初始化为 `NULL`。

一个包含实现读、写、打开等系统调用的函数指针的 `struct file_operations` 实例通常被称为 `fops`。你也会看到它被称为 `struct file`。请忍住诱惑。

### 4.1.2. file 结构

每个设备在内核中由一个 `file` 结构表示，该结构定义在 linux/fs.h 中。请注意，文件是一个内核级结构，永远不会出现在用户空间程序中。它与 glibc 定义的 `FILE` 不同，而且它的名称也有点误导性；它代表一个已打开的“文件”，而不是磁盘上的文件（后者是由名为 `inode` 的结构表示的）。

`struct file` 的实例通常被称为 `filp`。你也会看到它被称为 `struct file`。请抵制这种误惑。

去看看 `file` 的定义吧。你看到的大多数项（如 `struct entry`）并没有驱动程序使用，你可以忽略它们。这是因为驱动程序并不填充 `file`；它们只使用在其他地方创建的 `file` 结构。

### 4.1.3. 注册设备

如前，设备通过设备文件访问，通常位于 /dev/[name]。主设备告诉你哪个驱动程序处理哪个文件。设备号仅供驱动程序本身区分它正在操作哪个设备，以防驱动程序处理多个设备。

将驱动程序添加到你的系统中意味着向内核注册它。

```c
int register_dev(int major, const char *name, struct file_operations *fops);
```

### 4.1.4. 注销设备

我们不能允许内核模块随 root 的心情随时被 rmmod。如果设备文件正被某个进程打开，而我们删除了内核模块，将导致调用原本相应函数所在的内存地址。如果我们足够好，那里没有加载代码，我们会收到一条错误消息。如果我们运气不佳，另一个内核模块被加载到了相同的位置，这意味着跳转到另一个函数的中间。

### 4.1.5. chardevc

下一个代码示例创建了一个名为 `chardevc` 的字符驱动。你可以通过 `cat` 它的设备文件，或者用程序打开该文件，驱动程序将返回设备文件从文件中读取的次数。我们不支持向文件写入（例如 echo "hi" >/dev/null），但这些尝试会告诉你该操作不支持。如果你没有看到我们对读取到的数据做了什么，请不要担心。






buffer；我们对它没做什么。我们只是地读取数据并打印一条消息，确认我们已经收到了它。

示例 4-1. chardev.c

```c
/*
 * chardev.c: 创建一个只读字符设备，显示你
 * 从 dev 文件中读取了多少次
 */

#include <linux/kernel.h>
#include <linux/module.h>
#include <linux/fs.h>
#include <asm/uaccess.h>                /* 用于 put_user */

/*
 * 这些原型通常会放在 .h 文件中
 */
int init_module(void);
void cleanup_module(void);
static int device_open(struct inode *, struct file *);
static int device_release(struct inode *, struct file *);
static size_t device_read(struct file *, char *, size_t, loff_t *);
static size_t device_write(struct file *, const char *, size_t, loff_t *);

#define SUCCESS 0
#define DEVICE_NAME "chardev"        /* 在 /proc/devices 中显示的名称 */
#define BU_LEN 80                     /* 来自设备的消息的最大长度 */

/*
 * 全局变量声明为 static，因此在文件内部是全局的。
 */

static int Major;                 /* 分配给设备驱动的主设备 */
static int Device_Open = 0;       /* 设备打开了吗？ */
static char msg[BUF_LEN];          /* 用于防止多次访问设备 */
static char *msg_Ptr;              /* 当使用时将赋给 msg 设备 */

static struct file_operations fops = {
  .read = device_read,
  .write = device_write,
  .open = device_open,
  .release = device_release
};

/*
 * 该函数在模块加载时被调用
 */
int init_module(void) {
	Major = register_chardev(0, DEVICE_NAME, &fops);

	if (Major < 0) {
		printk(KERN_ALERT "注册字符设备失败，错误码为 %d\n", Major);
		return Major;
	}

	printk(KERN_INFO "我被分配了主设备号 %d。要与\n", Major);
	printk(KERN_INFO "驱动程序通信，请创建一个 dev 文件\n");
	printk(KERN_INFO, "mkmod /dev/%s c %d 0.\n", DEVICE_NAME, Major);
	printk(KERN_INFO, "尝试不同的次设备号。尝试剪切并 echo 到\n");
	printk(KERN_INFO, "设备文件。\n");
	printk(KERN_INFO, "完成后删除设备文件和模块。\n");

	return SUCCESS;
}

/*
 * 该函数在模块卸载时被调用
 */
void cleanup_module(void)
{
    /* 取消设备注册 */
    int ret = unregister_chrdev(Major, DEVICE_NAME);
    if (ret < 0)
        printk(KERN_ALERT, "unregister_chrdev 错误: %d\n", ret);
}

/*
 * 方法
 */
/*
 * 当进程尝试打开设备文件时调用，
 * "cat /dev/mycharfile"
 */
static int device_open(struct inode *inode, struct file *file)
{
    static int counter = 0;

    if (Device_Open)
        return -EBUSY;

    Device_Open++;
    sprintf(msg, "我已经告诉过你 %d 次 Hello world!\n", counter++);
    msg_Ptr = msg;
    try_module_get(THIS_MODULE);

    return SUCCESS;
}

/*
 * 当进程关闭设备文件时调用。
 */
static int device_release(struct inode *inode, struct file *file)
{
    /* 我们准备好处理下一个调用者了 */
    /*
     * 减少使用计数，否则一旦你打开了文件，
     * 永远无法移除模块。
     */
    module_put(THIS_MODULE);

    return 0;
}

/*
 * 当已经打开 dev 文件的进程尝试从其中
 * 读取时调用。
 */
static ssize_t device_read(struct file *filp,
    char *buffer,
    size_t length,
    loff_t * offset)
    /* 见 include/linux/fs.h */
    /* 用于填充数据的缓冲区 */
    /* 缓冲区的长度 */
{
    /*
     * 实际写入缓冲区的字节数
     */
    int bytes_read = 0;

    /*
     * 如果我们在消息的末尾，
     * 返回 0 表示文件结束
     */
    if (*msg_Ptr == 0)
        return 0;

    /*
     * 实际上将数据放入缓冲区
     */
    while (length & *msg_Ptr) {
        /* 缓冲区在用户数据段，而不是内核
         * 段，因此 **= 赋值将不起作用。我们必须使用
         * put_user 将数据从内核数据段拷贝
         * 到用户数据段。
         */
        put_user(*msg_Ptr++, buffer);

        length--;
        bytes_read++;
    }
    /*
     * 大多数读取函数返回写入缓冲区的字节数
     */
    return bytes_read;
}

/*
 * 当已经打开 dev 文件的进程尝试从其中
 * 写入时调用。
 */
static ssize_t device_write(struct file *filp,
    const char *buffer,
    size_t length,
    loff_t * offset)
    /* 见 include/linux/fs.h */
    /* 用于填充数据的缓冲区 */
    /* 缓冲区的长度 */
{
    /*
     * 实际写入缓冲区的字节数
     */
    int bytes_read = 0;

    /*
     * 如果我们在消息的末尾，
     * 返回 0 表示文件结束
     */
    if (*msg_Ptr == 0)
        return 0;

    /*
     * 实际上将数据放入缓冲区
     */
    while (length & *msg_Ptr) {
        /* 缓冲区在用户数据段，而不是内核
         * 段，因此 **= 赋值将不起作用。我们必须使用
         * put_user 将数据从内核数据段拷贝
         * 到用户数据段。
         */
        put_user(*msg_Ptr++, buffer);

        length--;
        bytes_read++;
    }
    /*
     * 大多数读取函数返回写入缓冲区的字节数
     */
    return bytes_read;
}





```c
/* /
#include <linux/module.h>
#include <linux/kernel.h>
#include <linux/proc_fs.h>

/* 具体来说，一个模块 /
/* 我们正在进行内核工作 */
/* 因为我们使用了 proc fs 文件系统 */

#define procs_name "helloworld"

/**
 * 此结构体包含了关于 /proc 文件的信息
 */

struct proc_dir_entry *Our_Proc_File;

/* 将数据写入 proc fs 文件。

 * 参数
 * 1. 要插入数据的缓冲区，如果
 *    你决定使用它的话。
 * 2. 指向字符指针的指针。如果你不想
 *    使用由内核分配的缓冲区，
 *    则这很有用。
 * 3. 文件中的当前位置
 * 4. 从此处 "len" 到文件结束 (EOF) 的大小。
 * 5. 在此处写入 "0" 表示文件结束 (EOF)。
 * 6. 指向数据的指针（适用于一次性读取
 *    多个 /proc/... 条目的情况）

 * 用法和返回值

 * 返回值为0表示你现在没有更多
 * 信息了（文件结束）。负返回
 * 值表示错误条件。

 * 更多信息

 * 我们发现该如何处理这个函数的初衷
 * 并不是通过阅读文档，而是通过阅读
 * 使用该函数的代码；我只是看了看什么地方使用了
 * proc_dir_entry 结构体的 _info 字段（我使用了
 * find 和 grep 的组合，如果你感兴趣的话），
 * 然后我看到它被用在 <内核源码
 * 目录>/fs/array.c 中。

 * 如果某些事情是未知的，最好的方法就是查看源码。对于内核，
 * 这通常是路。在 Linux 中，我们拥有巨大的
 * 优势，可以免费获取内核源代码 - 使用它吧。
 */
int
procfile_read(char *buffer,
	               loff_t offset, int buffer_length, int *eof, void *data)
{
	int ret;
	printk(KERN_INFO "procfile_read (/proc/%s) called\n", procs_name);

	/*
	 * 我们一次性提供所有的信息，所以如果
	 * 用户询问我们是否还有更多信息，
	 * 答案应该始终是没有。
	 * 这很重要，因为库中标准的 read
	 * 函数会继续发布 read
	 * 系统调用，直到内核回复
	 * 它没有更多信息，或者直到它的
	 * 缓冲区被填满。
	 */
if (offset != 0) {
    /* 我们已经完成读取，返回 0 */
    return 0;
} else {
    /* 填充缓冲区，返回缓冲区大小 */
    ret = sprintf(buffer, "HelloWorld!\n");
}

return ret;
}
```

```c
int init_module()
{
    Our_Proc_File = create_proc_entry(procs_name, 0644, NULL);
    if (Our_Proc_File == NULL) {
        remove_proc_entry(procs_name, &proc_root);
        printk(KERN_ALERT "Error: Could not initialize /proc/%s\n",
               procs_name);
        return -ENOMEM;
    }

    Our_Proc_File->read = procfile_read;
    Our_Proc_File->owner = THIS_MODULE;
    Our_Proc_File->mode = S_IFREG | S_IRUGO;
    Our_Proc_File->uid = 0;
    Our_Proc_File->gid = 0;
    Our_Proc_File->size = 37;

    printk(KERN_INFO "/proc/%s created\n", procs_name);
    return 0;
}
```

```c
void cleanup_module()
{
    remove_proc_entry(procs_name, &proc_root);
    printk(KERN_INFO "/proc/%s removed\n", procs_name);
}
```

# Linux 内核编程

## 5. 读取与写入

我们已经看到了对 /proc 文件进行读取和写入，通过 /proc 接口。

/proc 文件 写入一个 /proc 示例。这很重要，因为 使用了 procfs 缓冲区。

标准的 read 函数会继续发布 read 系统调用，直到内核回复它没有更多信息，或者直到它的缓冲区被填满。

## 5.2 procfs 示例

```c
/* /
#include <linux/module.h>
#include <linux/kernel.h>
#include <linux/proc_fs.h>
#include <linux/uaccess.h>

/* 具体来说，一个模块 /
/* 我们正在进行内核工作 */
/* 因为我们使用了 proc fs 文件系统 */

#define procs_name "helloworld"

/**
 * 此结构体包含了关于 /proc 文件的信息
 */

struct proc_dir_entry *Our_Proc_File;

/* 将数据写入 proc fs 文件。

 * 参数
 * 1. 要插入数据的缓冲区，如果
 *    你决定使用它的话。
 * 2. 指向字符指针的指针。如果你不想
 *    使用由内核分配的缓冲区，
 *    则这很有用。
 * 3. 文件中的当前位置
 * 4. 从此处 "len" 到文件结束 (EOF) 的大小。
 * 5. 在此处写入 "0" 表示文件结束 (EOF)。
 * 6. 指向数据的指针（适用于一次性读取
 *    多个 /proc/... 目的目的情况）

 * 用法和返回值

 * 返回值为0表示你现在没有更多
 * 信息了（文件结束）。负返回
 * 值表示错误条件。

 * 更多信息

 * 我们发现该如何处理这个函数的初衷
 * 并不是通过阅读文档，而是通过阅读
 * 使用该函数的代码；我只是看了看什么地方使用了
 * proc_dir_entry 结构体的 _info 字段（我使用了
 * find 和 grep 的组合，如果你感兴趣的话），
 * 然后我看到它被用在 <内核源码
 * 目录>/fs/array.c 中。

 * 如果某些事情是未知的，最好的方法就是查看源码。对于内核，
 * 这通常是路。在 Linux 中，我们拥有巨大的
 * 优势，可以免费获取内核源代码 - 使用它吧。
 */
int
procfile_read(char *buffer,
	               loff_t offset, int buffer_length, int *eof, void *data)
{
	int ret;
	printk(KERN_INFO "procfile_read (/proc/%s) called\n", procs_name);

	/*
	 * 我们一次性提供所有的信息，所以如果
	 * 用户询问我们是否还有更多信息，
	 * 答案应该始终是没有。
	 * 这很重要，因为库中标准的 read
	 * 函数会继续发布 read
	 * 系统调用，直到内核回复
	 * 它没有更多信息，或者直到它的
	 * 缓冲区被填满。
	 */
if (offset != 0) {
    /* 我们已经完成读取，返回 0 */
    return 0;
} else {
    /* 填充缓冲区，返回缓冲区大小 */
    ret = sprintf(buffer, "HelloWorld!\n");
}

return ret;
}
```

```c
int init_module()
{
    Our_Proc_File = create_proc_entry(procs_name, 0644, NULL);
    if (Our_Proc_File == NULL) {
        remove_proc_entry(procs_name, &proc_root);
        printk(KERN_ALERT "Error: Could not initialize /proc/%s\n",
               procs_name);
        return -ENOMEM;
    }

    Our_Proc_File->read = procfile_read;
    Our_Proc_File->owner = THIS_MODULE;
    Our_Proc_File->mode = S_IFREG | S_IRUGO;
    Our_Proc_File->uid = 0;
    Our_Proc_File->gid = 0;
    Our_Proc_File->size = 37;

    printk(KERN_INFO "/proc/%s created\n", procs_name);
    return 0;
}
```

```c
void cleanup_module()
{
    remove_proc_entry(procs_name, &proc_root);
    printk(KERN_INFO "/proc/%s removed\n", procs_name);
}
```





# Linux 内核模块编程指南

```c
/**
 * 缓冲区中持有的数据的大小
 *
 * static unsigned long procfs_buffer_size = 0;
 */
```

```c
/**
 * 保留 /proc 文件信息的结构体
 *
 * static struct proc_dir_entry *Our_Proc_File;
 */
```

```c
/**
 * 当 /proc 文件被读取时，会调用此函数
 *
 * 参见 include/linux/fs.h
 * 用于填充数据的缓冲形缓冲区
 * static ssize_t procfs_read(struct file *filp,
 *                              char *buffer,
 *                              size_t length,
 *                              loff_t *offset,
 *                              length of the buffer
 */
    int finished = 0;
    /*
     * 我们返回 0 表示文件结束，即我们没有
     * 更多信息了。否则，进程将
     * 无限地从我们这里读取。
     */
    if (finished) {
        printk(KERN_INFO "procfs-read: END\n");
        finished = 0;
        return 0;
    }
```

```c
    finished = 1;
    /*
     * 我们使用 put_to_user 将字符串从内核
     * 内存段拷贝到调用我们的进程的内存段。
     * 顺便说，get_from_user 用于
     * 反向操作。
     */
    if (copy_to_user(buffer, procfs_buffer, procfs_buffer_size)) {
        return -EFAULT;
    }
```

```c
printk(KERN_INFO "procfs-read: %lu bytes\n", procfs_buffer_size);

    return procfs_buffer_size; /* 返回已读取的字节数 */
```

```c
/**
 * 当 /proc 文件被写入时，会调用此函数
 */
static size_t
procfs_write(struct file *file, const char *buffer, size_t len, loff_t *off) {
    if (len > PROCS_MAX_SIZE) {
        procfs_buffer_size = PROCS_MAX_SIZE;
    }
    else {
        procfs_buffer_size = len;
    }
```

第 5 章. /proc 文件系统

# Linux 内核模块编程指南

```c
if (copy_from_user(procfs_buffer, buffer, procfs_buffer_size)) {
    return -EFAULT;
}

printk(KERN_INFO, "procfs_write: write %lu bytes\n", procfs_buffer_size);

return procfs_buffer_size;
```

```c
/*
* 此函数决定是否允许执行操作
*（返回零允许）或不允许（返回非零，
* 以表示为什么不被允许）。
* 操作可以是以下值之一：
* 0 - 执行/运行“文件” - 在我们的用例中没有意义
* 2 - 写入（到内核模块的输入）
* 4 - 读取（从内核模块的输出）

* 这是一个检查文件权限的
* 真实函数。ls -l 返回的权限
* 仅供参考，且
```

```c
static int module_permission(struct inode *inode, int op, struct nameidata *foo) {
    /*
     * 我们允许所有人读取我们的模块，
     * 只有 root (uid 0) 可以向其写入
     */
    if (op == 4 || op == 2 && current->uid == 0) {
        return 0;
    }

    /*
     * 如果是其他任何情况，则拒绝访问
     */
    return -EACCES;
}
```

```c
/*
* 文件被打开 - 我们并不真正关心
* 那，但它意味着我们需要增加
* 模块的引用计数。
*/
int procfs_open(struct inode *inode, struct file *file) {
    try_module_get(THIS_MODULE);
    return 0;
}
```

```c
/*
* 文件被关闭 - 同样，仅是因为
* 引用计数。
*/
int procfs_close(struct inode *inode, struct file *file) {
    module_put(THIS_MODULE);
    return 0;
}
```

第 5 章. /proc 文件系统

# Linux 内核模块编程指南

```c
static struct file_operations File_Ops_File = {
  .read = procfs_read,
  .write = procfs_write,
  .open = procfs_open,
  .release = procfs_close,
};
```

* 我们的 proc 文件的 Inode 操作。我们需要它，
* 这样我们就有地方来指定想要使用的
* 文件操作结构体，以及我们用于权限
* 的函数。也可以指定为
* 其他可以执行的操作调用的函数
*（尽管我们没有去理会，只需放在那里即可）

```c
static struct inode_operations Inode_Ops_File = {
  .permission = module_permission, /* 检查权限 */
};
```

* 模块初始化与清理

```c
Our_Proc_File->owner = THIS_MODULE;
Our_Proc_File->proc_ops = &Inode_Ops_File;
Our_Proc_File->fops = &File_Ops_File;
Our_Proc_File->mode = S_IFREG | S_IWUSR;
Our_Proc_File->uid = 0;
Our_Proc_File->gid = 0;
Our_Proc_File->size = 0;
```

```c
printk(KERN_INFO "/proc/%s created\n", PROC_NAME);

  return 0;
}
```

还对 proc 感到饥饿吗？首先请记住，它有很多其他方法，可以考虑使用 sysfs。如果你不贪婪，在 linux/Documentation/ 下方有一个非常推荐的层。

# 5.4. 使用 seq_file 管理 /proc 文件

正如我们所见，编写 /proc 文件可能相当“复杂”。因此，为了帮助人们编写 /proc 文件，有一个名为 seq_file 的 API，它可以帮助格式化 /proc文件的输出。它基于序列（sequence），由三个函数组成：start()、next() 和 stop()。当我们读取 /proc 文件时，seq_file API 会启动一个序列。

序列开始于调用 `start()` 函数。如果返回值为 NULL，则调用 `next()` 函数。此函数是一个迭代器，目标是获取所有数据。每次调用 `next()` 时，都会调用 `show()` 函数。它由读取者向缓冲区写入数据值。持续调用 `next()` 直到它返回 NULL。当 next 返回 NULL 时，序列结束，然后调用 `stop()` 函数。

注意：当一个序列完成时，另一个会开始。这意味着在 stop() 函数结束时，会再次调用 start() 函数。此循环在 start 函数返回 NULL 时结束。你可以在图“How seq_file works”中看到这种方案。

Seq_file 为 file_operations 提供了基本函数，如 seq_read、seq_lseek 等，且在 /proc 文件中无需编写内容。当然，你仍然可以使用上一个示例中的相同方法。

### 图 5–4. procfs4.c

```c
/**
* procfs4.c - 在 /proc 中创建一个“文件”
* 此程序使用 seq_file 库来管理 /proc 文件
 */
#include <linux/kernel.h>
#include <linux/module.h>
#include <linux/proc_fs.h>
#include <linux/seq_file.h>

/* 计数器 */
static int counter = 0;
#define PROC_NAME "procfs4"

static void *my_start(struct seq_file *s, struct inode *inode, loff_t *off) {
    /*  */
    if (*off == 0) {
        return &counter;
    }
    return NULL;
}

static void *my_next(struct seq_file *s, void *v) {
    /*  */
    if (*v < 10) {
        return v++;
    }
    return NULL;
}

static void my_stop(struct seq_file *s, void *v) {
    /*  */
}

static int my_show(struct seq_file *s, void *v) {
    /*  */
    loff_t *spos = (loff_t *)v;
    fprintf(s, "%d\n", *spos);
    return 0;
}

static int my_open(struct inode *inode, struct file *file)
{
    return seq_open(file, &my_seq_ops);
}

/**
 * 用于管理序列的结构体
 */
static struct seq_operations my_seq_ops = {
    .start = my_start,
    .next = my_next,
    .stop = my_stop,
    .show = my_show
};

/**
 * 用于管理 /proc 文件的结构体
 */
static struct file_operations my_file_ops = {
    .owner = THIS_MODULE,
    .open = my_open,
    .read = seq_read,
    .llseek = seq_lseek,
    .release = seq_release
};

/**
 * 当模块加载时调用此函数
 */
int init_module(void) {
    struct proc_dir_entry *entry;

    entry = create_proc_entry(PROC_NAME, 0, NULL);
    if (entry) {
        entry->proc_fops = &my_file_ops;
    }
    return 0;
}

/**
 * 当模块卸载时调用此函数
 */
void cleanup_module(void) {
    remove_proc_entry(PROC_NAME, NULL);
}
```





这里目前只是一个占位符。最后，我希望在这里看到一个关于 sysfs 的章节（尚未编写）。如果你熟悉 sysfs 并且想参与该章节的编写，请随时联系我们（LKMPG 维护者）以获取更多细节。

# 第 7 章 与设备文件通信

### 7.1. 与设备文件通信（写和 IOCTL）

设备文件本应该代表物理设备。大多数物理设备既用于输出也用于输入，因此内核中的设备驱动程序需要某种机制从进程中获取输出并发送到设备。这是通过打开设备文件进行输出并对其写入来实现的，就像写入文件一样。在接下来的示例中，这通过 `device_write` 实现。

这还不够的。想象你有一个连接到调制解调器的串口（即使你有内置调制解调器，从 CPU 的角度来看，它仍然被实现为连接到解调器的串口，所以你不需要太费想象力）。自然的做法是使用设备文件向解调器写入内容（命令或要通过电话线发送的数据），并从解调器读取内容（命令的响应或通过电话线接收的数据）。然而，当你需要与串口通信时（例如发送发送和接收数据的速率），这就留下了一个问题。

Unix 的答案是使用一个特有的函数 `ioctl`（Input Output Control，输入输出控制的缩写）。每个设备都有自己的 `ioctl` 命令，这些命令可以是读 `ioctl`（从进程向内核发送信息）、写 `ioctl`（向进程返回信息）、两者兼具或二者都不具备。调用 `ioctl` 函数时带有三个参数：适当设备文件的文件描述符、ioctl 编号以及一个参数（该参数为 `long` 类型，因此你可以使用 `case` 来传递任何内容）。

`ioctl` 编号编码了设备号、ioctl 类型、命令以及其类型。这个数字通常在头文件中通过宏调用 `_IO__IOR__OW`（取决于类型）创建。该头文件随后应该被使用 `ioctl` 的程序包含（以便它们可以生成相应的 `ioctl`）以及内核模块包含（以便它能理解它）。在示例中，文件头文件是 `chardev.h`，使用它的程序是 `ioctl.c`。

如果你想在自己的内核模块中使用 `ioctl`，最好获得一个官方的 `ioctl` 分配，否则如果你不小心拿了别人的 `ioctl`，或者他们拿了你的，你就知道出问题了。更多信息请检查内核源码树中的 `Documentation/ioctl-number.txt`。

### 示例 7-1. chardev.c

```c
/*
 * chardev.c - 创建一个输入/输出字符设备
 */

#include <linux/kernel.h>
/* * 我们正在进行内核工作 */
#include <linux/module.h>
/* * 特地，一个模块 */
#include <linux/fs.h>
#include <asm/uaccess.h>

/* * 用于 get_user 和 put_ptr */

#include <chardev.h>
#define SUCCESS 0
#define DEVICE_NAME "chardev"
#define BUF_LEN 80
```

- 设备现在打开着吗？用于防止并发访问同一个设备
```c
static int Device_Open = 0;
```

```c
/*
* 当被询问时设备将给消息
 */
static char Message[BUF_LEN];
```

```c
/*
* 读取消息的进程到了哪里？
* 如果消息大于我们在
* device_read 中填充的
* 缓冲区大小，则很有用。
 */
static char *Message_Ptr;
```

```c
/*
* 当进程尝试打开设备文件时，就会调用此函数
 */
static int device_open(struct inode *inode, struct file *file)
{
#ifdef DEBUG
    printk(KERN_INFO "device_open(%p)\n", file);
#endif

  /*
* 我们不想同时与两个进程通信
 */
 if (Device_Open)
    return -EBUSY;

  Device_Open++;

  /*
* 初始化消息
 */
  Message_Ptr = Message;
  try_module_get(THIS_MODULE);
  return SUCCESS;
}
```

```c
static int device_release(struct inode *inode, struct file *file)
#ifdef DEBUG
    printk(KERN_INFO "device_release(%p,%p)\n", inode, file);
#endif

  /*
* 我们现在准备好接受下一个调用者了
 */
  Device_Open--;

  module_put(THIS_MODULE);
  return SUCCESS;
}
```

```c
/*
* 当进程已经打开设备
* 文件并尝试从中读取时，就会调用此函数。
 */
static ssize_t device_read(struct file *file, 
    /*    /* 查看 include/linux/fs.h */
    char __user *buffer, /* 缓冲区将 */
    /* 填充数据 */
size_t length,           /* 缓冲区长度 */
loff_t * offset);                    */

/*
 * 实际写入缓冲区字节数
 */
int bytes_read = 0;

#ifdef DEBUG
printk(KERN_INFO "device_read(%p,%p,%d)\n", file, buffer, length);
#endif

/*
 * 如果我们在消息的末尾，返回 0
 *（表示文件结束）
 */
if (*Message_Ptr == 0) {
    return 0;
}

/*
 * 填充缓冲区
 */
while (length && *Message_Ptr) {

/*
 * 因为缓冲区在用户空间段，
* 不在内核空间段，赋值将
* 不起。我们必须使用 put_user
* 它将数据从内核空间段拷贝
 * 到用户空间段。
 */
    if (put_user(*(Message_Ptr++), buffer++))
        length--;
    bytes_read++;
}

#ifdef DEBUG
printk(KERN_INFO "Read %d bytes, %d left\n", bytes_read, length);
#endif

/*
 * 填充缓冲区
 */
return bytes_read;
};
```

```c
/*
* 当进程已经打开设备
* 文件并尝试从中读取时，就会调用此函数。
 */
static ssize_t device_write(struct file *file, 
    /*    /* 查看 include/linux/fs.h */
    char __user *buffer, /* 缓冲区将 */
    /* 填充数据 */
size_t length,           /* 缓冲区长度 */
loff_t * offset)                    */

/*
 * 实际写入缓冲区字节数
 */
int bytes_read = 0;

#ifdef DEBUG
printk(KERN_INFO "device_read(%p,%p,%d)\n", file, buffer, length);
#endif

/*
 * 如果我们在消息的末尾，返回 0
 *（表示文件结束）
 */
if (*Message_Ptr == 0) {
    return 0;
}

/*
 * 填充缓冲区
 */
while (length && *Message_Ptr) {

/*
 * 因为缓冲区在用户空间段，
* 不在内核空间段，赋值将
* 不起。我们必须使用 put_user
* 它将数据从内核空间段拷贝
 * 到用户空间段。
 */
    if (put_user(*(Message_Ptr++), buffer++))
        length--;
    bytes_read++;
}

#ifdef DEBUG
printk(KERN_INFO "Read %d bytes, %d left\n", bytes_read, length);
#endif

/*
 * 填充缓冲区
 */
return bytes_read;
};
```





# Linux 内核模块编程指南

```c
return 0;
/*
 * 清理 - 从 /proc 中注销适当的文件
 */
void cleanup_module() {
    int ret;

    /*
     * 取消设备注册
     */
    ret = unregister_chdev(MAJOR_NUM, DEVICE_NAME);

    /*
     * 如果发生错误，则报告错误
     */
    if (ret < 0)
        printk(KERN_ALERT "Error: unregister_chdev: %d\n", ret);
}
```

###### 示例 7–2. chardev.h

```c
/*
 * chardev.h - 包含 ioctl 定义的头文件。
 * 这里的声明必须在头文件中
```

# 第 7 章.与设备文件通信

# Linux 内核模块编程指南

```c
/*
 * 获取设备驱动的消息
 */
#define IOCTL_GET_MSG _IOR(MAJOR_NUM, 1, char *)
/*
 * 此 IOCTL 用于输出，以获取设备驱动
 * 消息。然而，我们仍然需要
 * 缓冲区作为存放消息的输入，
 * 因为它是由进程分配的。
 */
```

```c
/*
 * 获取消息的第 n 个字节
 */
#define IOCTL_GET_NTH_BYTE _IOW(MAJOR_NUM, 2, int)
/*
 * 该 IOCTL 同时用于输入和输出。它
 * 从用户接收一个数字 n，并返回
 * Message[n]。
 */
```

```c
/*
 * 获取设备文件的名称
 */
#define DEVICE_FILE_NAME "char_dev"

#endif
```

示例 7–3. ioctl.c

```c
/*
 * ioctl.c - 使用 ioctl 控制内核模块的进程
 *
 * 直到现在我们可以使用 cat 进行输入和输出。但现在
 * 我们需要使用 ioctl，这需要编写自己的进程。
 */
```

```c
/*
 * 设备规格，例如 ioctl 编号和
 * 主设备文件。
 *
#include "chardev.h"
```

```c
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <unistd.h>
#include <sys/ioctl.h>
/* open */
/* exit */
/* ioctl */
```

```c
/*
 * 用于 ioctl调用的函数
 */
```

```c
ioctl_set_msg(int file_desc, char *message)
{
    int ret_val;

    ret_val = ioctl(file_desc, IOCTL_SET_MSG, message);
```

第 7 章.与设备文件通信

```c
if (ret_val < 0) {
    printf("ioctl_set_msg failed:%d\n", ret_val);
    exit(-1);
}
```

```c
ioctl_get_msg(int file_desc) {
    int ret_val;
    char message[100];
```

- 警告 - 这是这是危险的，因为我们没有告诉内核它允许写入多远，所以它可能会溢出缓冲区。在实际生产程序中，我们会使用两个 ioctl：一个用于告诉内核缓冲区长度，另一个用于给它要填充的缓冲区。

```c
ret_val = ioctl(file_desc, IOCTL_GET_MSG, message);

if (ret_val < 0) {
    printf("ioctl_get_msg failed:%d\n", ret_val);
    exit(-1);
}
```

```c
printf("get msg message:%s\n", message);
```

```c
ioctl_get_nth_byte(int file_desc) {
    int i;
    char c;
    printf("get_nth_byte message:%s\n");
```

```c
i = 0;
do {
    c = ioctl(file_desc, IOCTL_GET_NTH_BYTE, i++);

    if (c < 0) {
        printf("ioctl_get_nth_byte failed at the %d'th byte:%d\n", i);
        exit(-1);
    }

    putchar(c);
} while (c != 0);
putchar("\n");
```

```c
/*
主函数 - 调用 ioctl 函数
*/
```

```c
main() {
    int file_desc, ret_val;
    char *msg = "Message passed by ioctl\n";

    file_desc = open(DEVICE_FILE_NAME, 0);
    if (file_desc < 0) {
        printf("Can't open device file: %s\n", DEVICE_FILE_NAME);
        exit(-1);
    }

    ioctl_get_nth_byte(file_desc);
    ioctl_get_msg(file_desc);
    ioctl_set_msg(file_desc, msg);

    close(file_desc);
```

## 第 8 章.系统调用

## 8.1. 系统调用

到目前，我们所做的唯一就是使用定义良好的内核机制来注册 /proc 文件和设备处理程序。如果你想做一些内核程序员认为你想要做的事情，比如编写设备驱动，那是没问题的。但如果你想做一些不寻常的事情，改变内核的行为呢？（注：由于提供的原文文本从此处开始出现大量重复且无意义的短语，翻译部分已根据要求对这些重复内容进行了对应处理）。





## Linux 内核模块编程指南

- * 对于当前的（进程）结构，我们需要
* 使用这个结构来知道当前用户是谁。

#include <linux/sched.h>
#include <asm/uaccess.h>

```c
/*
* 系统调用表（函数数组）。我们
* 只需要将其定义为外部的，内核会在
* 我们执行 insmod 时为我们填充它。
* sys_call_table 在 2.6.x 内核中不再导出。
* 如果你真的想尝试这个**危险的**模块，你
* 必须对你当前的内核应用提供的补丁
* 并重新编译它。
*/
extern void *sys_call_table[];
```

```c
/*
* 我们想要监视的 UID -- 将从
* 命令行中填充
*/
static int uid;
module_param(uid, int, 0664);
```

```c
/*
* 指向原始系统调用的指针。我们
* 保留这个指针而不是调用原始函数
* (sys_open)，是因为可能可能在之前
* 替换了该系统调用。注意，这
* 并不是 100% 安全的，因为如果另一个模块
* 在我们之前注册 sys_open，那么当我们在
* 时，我们将调用该模块中的函数 - 而
* 它可能在我们之前被移除。
*/
```

```c
/*
* 另一个原因是我们无法获取 sys_open。
* 它是一个静态变量，所以它没有被导出。
*/
asmlinkage int (*original_call)(const char *, int, int);
```

```c
/*
* 我们替换的 sys_open 函数（当你调用
* open 系统调用时被调用的函数）。为了
* 找到确切的原型、参数的数量
* 和类型，我们先找到原始函数
* (int (*orig_open)(...))
*/
```

```c
/*
* 在理论上，这意味着我们被绑定到了
* 当前版本的内核。在实践中，
* 系统调用几乎不会改变（这会造成混乱）
* 并需要程序重新编译，因为系统
* 调用是内核与进程之间的
* 接口。
*/
```

```c
asmlinkage int our_sys_open(const char *filename, int flags, int mode)
{
    int i = 0;
    char *ch;
    /*
    * 检查这是否是我们要监视的用户
    */
}
```

# 第 8 章 系统调用

## Linux 内核模块编程指南

```c
if (uid == current->uid) {
  /*
   * 如果相关，则报告文件
   */
  printf("Opened file by %d", uid);
  do {
    get_user(ch, filename + i);
    i++;
    printf("%c", ch);
  } while (ch != 0);
  printf("\n");
}
```

```c
/*
 * 调用原始的 sys_open - 否则，我们将失去
* 打开文件的能力
 */
return original_call(filename, flags, mode);
```

```c
/*
 * 初始化模块 - 替换系统调用
 */
int init_module() {
```

```c
/*
 * 警告 - 现在已经太晚了，但也许
 * 下一次可以...
 */
printk(KERN_ALERT "I'm dangerous. I hope you did a **");
printk(KERN_ALERT "%sync before you insmoded me.\n");
printk(KERN_ALERT "My counterpart, cleanup_module(), is even)");
printk(KERN_ALERT "More dangerous.\n");
printk(KERN_ALERT "you value your file system, it will **");
printk(KERN_ALERT "Be \sync rmodmod *\n");
printk(KERN_ALERT "When you remove this module.\n");
```

```c
/*
 * 保留原始函数的指针
* original_call，然后将系统调用
* 替换为 our_sys_open
 */
original_call = sys_call_table[__NR_OPEN];
sys_call_table[__NR_OPEN] = our_sys_open;
```

```c
/*
 * 获取 foo 函数的地址到
* sys_call_table[__NR_foo]。
 */
printk(KERN_INFO "Spying on UID:%d\n", uid);
return 0;
```

```c
/*
 * 清理 /proc 中的相应文件
 */
void cleanup_module() {
```

```c
/*
 * 将系统调用恢复为正常
 */
```

# 第 8 章 系统调用

## Linux 内核模块编程指南

```c
if (sys_call_table[__NR_open] != our_sys_open) {
    printk(KERN_ALERT "somebody played with the ");
```

---

# 第 9 章 阻塞进程

## 9.1 阻塞进程

当有人向你请求你无法提供的内容时，你该怎么办？如果你是一个人类并被另一个人类打扰，你唯一能说：“现在不行，我很忙。走开”。如果你是一个内核模块并被一个进程打扰，你还有另一种选择。你可以让进程睡眠，直到你能处理它。毕竟，进程一直被放入睡眠和唤醒（这就是多个进程看起来同时在 CPU 上运行的原因）。

这个模块就是一个例子。文件（proc/sleep）一次只能被一个进程打开。如果文件已经打开，内核会调用 wait_event_interruptible[2]。该函数会将任务（包含关于进程及其任何系统调用的信息的内核数据结构）的状态更改为 TASK_INTERRUPIBLE，这意味着该任务在被唤醒之前不会运行，并将其添加到 WaitQueue（等待访问文件的任务队列）中。然后，该函数调用调度器切换到另一个对 CPU 有用的进程。

当一个进程完成文件操作时，它关闭文件，module_close 会失败（没有机制来唤醒其中任何一个）。它允许刚刚关闭文件的进程继续运行。调度程序认为该进程没有优势，并将 CPU 控制权交给另一个进程。最终，队列中的一个进程会被调度器授予 CPU 控制权。





# Linux 内核模块编程指南

```c
/*
* 如果现在还不懂这个，那么你作为一个内核
* 程序员就没救了。
*/
printf(message, "Last input:%s\n", Message);
for (int i = 0; i < len && message[i]; i++)
    put_user(message[i], buf + i);

finished = 1; /* 返回“读取”的字节数 */
return i;
```

```c
/*
* 当用户向 /proc 文件写入时，该函数
* 从用户处接收输入。
*/
static ssize_t module_input(struct file *file, /* 文件本身 */
    const char *buf, /* 包含输入的缓冲区 * */
    size_t length, /* 缓冲区长度 */
    loff_t *offset) /* 文件的偏移量 - 忽略 * */
{
    int i;
```

```c
/*
* 将输入放入 Message 中，稍后 module_output
* 能够使用它
*/
for (int i = 0; i < MESSAGE_LENGTH - 1 && i < length; i++)
    get_user(Message[i], buf + i);

/*
* 我们需要一个标准的、零终止字符串
*/
Message[i] = '\0';

/*
* 我们需要返回使用的输入字符数
*/
return i;
```

```c
/*
* 如果文件当前被某些人打开
*/
int Already_Open = 0;
```

```c
/*
* 当 /proc 文件被打开时调用
*/
static int module_open(struct inode *inode, struct file *file)
{
    /* 如果文件的标志包含 O_NONBLOCK，则意味着进程
     * 不想等待文件。在这种情况下，如果文件已经
     * 打开，我们应该返回 -EAGAIN 导致失败，意味着‘你必须
     * 重试’，而不是阻塞一个宁愿保持唤醒状态的进程。 
     */
```

# 9. 阻塞进程

# Linux 内核编程指南

```c
if ((file->f_flags & O_NONBLOCK) && Already_Open)
    return -EAGAIN;
```

```c
/*
* 如果进程在循环中（该循环位于内核模块内部），
* 这是调用 try_module_get(THIS_MODULE) 的正确位置，
* 内核模块不能被移除。
*/
```

```c
try_module_get(THIS_MODULE);
```

```c
/*
* 如果文件已经打开，等待直到它不再打开
*/
```

```c
while (Already_Open) {
    int i, is_sig = 0;
```

```c
/*
* 此函数将当前进程（包括任何系统
* 调用，如我们）置于睡眠。执行将在函数调用
* 之后立即恢复，可能是 module_close 在文件
* 关闭时执行的，或者是因为信号（如 Ctrl-C）
* 发送给了进程
*/
```

```c
wait_interruptible(WaitQ, !Already_Open);
```

```c
/*
* 如果我们是因为收到信号唤醒而不是解除阻塞，
* 返回 -EINTR（系统调用失败）。这允许进程
* 被杀死或停止。
*/
```

- * Emmanuel Papirakis:

- * 这是针对 2.2 版本的一个小更新。信号现在包含
* 在两个字（64 位）中，并存储在一个包含
* 无符号长数组的结构中。

- * Pomerantz:
* 没有人告诉我会永远不会使用 64 位，
* 或者使用宽度为 16 位的 Linux。这段代码
* 在任何情况下都可以。

```c
for (int i = 0; i < NSIG_WORDS && is_sig; i++) {
    is_sig = current->pending[i] &
    blocked.signal[i];
}
```

```c
if (is_sig) {
    /* 在这里 module_put(THIS_MODULE) 是重要的，
    * 因为对于被中断的进程，如果我们
    * 不在这里减少引用计数，将会留下
    * 一个正数的引用计数，导致模块只能通过
    * 重启来杀死。
*/
}
```

第 9 章 阻塞进程

# Linux 内核模块编程指南

```c
module_put(THIS_MODULE);
    return -EINTR;
```

```c
/*
 * 如果我们到了这里，Already_Open 必须为 0
 */
```

```c
/*
 * 打开文件
 */
Already_Open = 1;
    return 0; /* 允许访问 */
```

```c
/*
 * 当 /proc 文件被关闭时调用
 */
int module_close(struct inode *inode, struct file *file)
{
```

```c
/*
 * 将 Already_Open 设置为 0，WaitQ 中的进程
* 将能够置回 1 并打开文件。其他
* 进程将睡眠。
 */
    Already_Open = 0;
```

```c
/*
 * 唤醒 WaitQ 中的所有进程，这样任何人
* 都可以。
 */
    wake_up(&WaitQ);
```

```c
module_put(THIS_MODULE);

    return 0; /* 成功 */
```

```c
/*
 * 此函数决定允许操作（返回零）还是
 * 禁止（返回非零表示原因）。操作可以是以下之一：
 * 0 - 执行（在我们的案例中“文件”没有意义）
 * 2 - 写入（输入内核模块）
 * 4 - 读取（从内核模块输出）
 * 这是检查文件权限的真实函数。它返回的权限
 * 仅供参考，可以在这里覆盖。
 */
```

```c
static int module_permission(struct inode *inode, int op, struct inode *nd)
{
    /* 我们允许所有人读取我们的模块，但只有 root (uid 0)
     * 可以写入 */
    if (op == 4 || (op == 2 && current->uid == 0))
        return 0;
}
```

# 第 9 章 阻塞进程

```c
/* 如果是其他情况，拒绝访问 */
return -EACCES;
```

```c
/*
* 用于 /proc 文件的结构，指向所有
* 函数。
*/
```

```c
/*
* proc 文件的文件操作。当有人对我们的文件
* 执行某些操作时，我们在这里放置所有
* 函数。NULL 表示我们不想处理某些操作。
*/
```

```c
static struct file_operations File_Ops_4_Proc_File = {
    .read = module_output, /* 从文件读取 */
    .write = module_input, /* 向文件写入 */
    .open = module_open, /* 当 /proc 文件被打开时调用 */
    .release = module_close, /* 被关闭时调用 */
};
```

```c
/*
* proc 文件的 inode 操作。我们需要一个地方
* 指定我们要使用的文件操作结构和用于
* 权限的函数也可以指定针对其他情况调用的
* 函数（尽管我们没写，直接放了 NULL）。
*/
static struct inode_operations In_Ops_4_Proc_File = {
    .permission = module_permission, /* 检查权限 */
};
```

```c
/*
* 模块初始化与清理
*/
```

```c
/* 初始化模块 - 注册 proc 文件 */
int init_module() {

    Our_Proc_File = create_proc_entry(PROC_ENTRY_FILENAME, 0644, NULL);

    if (Our_Proc_File == NULL) {
        remove_proc_entry(PROC_ENTRY_FILENAME, &proc_root);
        printk(KERN_ALERT, "Error: Could not initialize /proc/test\n");
        return -ENOMEM;
    }

    Our_Proc_File->owner = THIS_MODULE;
    Our_Proc_File->inode = &In_Ops_4_Proc_File;
    Our_Proc_File->fop = &File_Ops_4_Proc_File;
    Our_Proc_File->mode = S_IFREG | S_IRUGO | S_IWUSR;
    Our_Proc_File->uid = 0;
    Our_Proc_File->size = 80;

    printk(KERN_INFO, "/proc/test created\n");
}
```

# Linux 内核编程指南

```c
return 0;
```

```c
/*
* 清理 - 从 /proc 中注销我们的文件。如果
* WaitQ 中还有进程等待，这可能是危险的，
* 模块的移除将在第 10 章解释。
*/
void cleanup_module() {
    remove_proc_entry(PROC_ENTRY_FILENAME, &proc_root);
    printk(KERN_INFO, "/proc/test removed\n");
}
```

### 示例 9-2. cat_noblock

```c
/*
* cat_noblock.c - 打开文件并显示其内容，但退出
* 而不是等待输入 */
/* Copyright 1998 by Pomerantz */

#include <stdio.h>      /* 标准 I/O */
#include <fcntl.h>      /* 用于 open */
#include <unistd.h>     /* 用于 read */
#include <stdlib.h>     /* 用于 exit */
#include <errno.h>      /* 用于 errno */

#define MAX_BYTES 1024*4

main(int argc, char *argv[]) {
    int fd; /* 要读取的文件描述符 */
    size_t bytes; /* 读取的字节数 */
    char buffer[MAX_BYTES]; /* 字节缓冲区 */

    /* 使用 */
    if (argc != 2) {
        printf("Usage: %s <filename>\n", argv[0]);
        puts("读取文件的内容，但不等待输入\n\n        exit(-1);
    }
}
```

```c
/* 以非阻塞模式打开文件进行读取 */
    fd = open(argv[1], O_RDONLY | O_NONBLOCK);

    /* 如果打开失败 */
    if (fd == -1) {
        if (errno == EAGAIN)
            puts("打开将阻塞\n\n        else
            puts("打开失败\n\n        exit(-1);
    }
}
```



```c
/* 读取文件并输出其内容 */
do {
    int i;

    /* 从文件中读取字符 */
    bytes = read(fd, buffer, MAX_BYTES);
    
    /* 如果发生错误，报告错误并退出 */
    if (bytes == -1) {
        if (errno == EAGAIN)
            puts("通常我会阻塞，但你告诉我不要这样做*");
        else
            puts("另一个读取错误*");
            exit(-1);
    }

    /* 打印字符 */
    if (bytes > 0) {
        for(i=0; i<bytes; i++)
            putchar(buffer[i]);
    }

    /* 当没有错误且文件未结束时继续循环 */
} while (bytes > 0);
```

# 第 10 章 替换 Printk

## 10.1. 替换 printk

在第 1.2.1.2 节中，我说 X 和内核模块编程是不兼容的。这对于开发内核模块来说确实如此，但在实际操作中，你希望向加载模块命令所在的任意 tty[15] 发送消息：

实现这一方法是使用 `current`（指向当前运行任务的指针）来获取当前任务结构。然后，我们查看该 tty 结构内部，找到指向字符串写入函数的指针，我们使用该函数向 tty 写入字符串：

**示例 10-1. print_string**

```c
* print_string.c - 将输出发送到我们正在运行的 tty，无论它是
* 通过 Shell、telnet 等。我们通过向与当前任务
* 关联的 tty 打印字符串来实现。

#include <linux/kernel.h>
#include <linux/module.h>
#include <linux/init.h>
#include <linux/sched.h>      /* 用于 current */
#include <linux/tty.h>       /* 用于 tty 声明 */
#include <linux/version.h> /* 用于 LINUX_VERSION_CODE */

MODULE_LICENSE("GPL");
MODULE_AUTHOR("Peter Jay Salzman");

static void print_string(char *str)
{
    struct tty_struct *my_tty;

    /*
     * tty struct 在 2.6.6 版本中进入了 signal struct
     */
    if ( LINUX_VERSION_CODE <= KERNEL_VERSION(2,6,5) )
        /*
         * 当前任务的 tty
         */
        my_tty = current->tty;
    } else {
        /*
         * 对于 2.6.6+ 内核，当前任务的 tty
         */
        my_tty = current->signal->tty;
    }

    /*
     * 如果 my_tty 为空，则当前任务没有可以打印的 tty
     *（例如，如果它是守护进程）。如果是这样，我们无能为力。
     */
    if (my_tty != NULL) {
        /*
         * my_tty->driver 是持有 tty 函数的结构体
         */
    }
```

Linux 内核编程指南

* 其中 `(write)` 用于向 tty 写入字符串。
* 它可以从用户空间或
* 内核内存段获取字符串。
* 函数的参数是待写入的 tty，
* 因为同一个函数通常用于所有
* 相同类型的 tty。第二个参数控制
* 函数是从从内存（false/假）
* 还是从内存（true/真，非零）接收字符串。
* 顺便说一下：此参数在内核 2.6.9 中已被移除。
* 第三个参数是指向字符串的指针。
* 第四个参数是字符串的长度。
* 正如下文所示，有时需要使用
* 预处理器指令来创建适用于不同
* 内核版本的代码。我们采用的（简单）方法
* 扩展性并不好。处理此问题的正确方法
* 在第 2 部分的节中有描述：
* linux/Documentation/Submitting

```c
(my_tty->driver)->write(my_tty), /* 自身
#if ( LINUX_VERSION_CODE <= KERNEL_VERSION(2,6,9) )
    return 0, /* 不要从用户空间
* 获取字符串
*/
#endif
* ttys 原本是硬件设备，它们（通常）
* 严格遵循 ASCII 标准。在 ASCII 中，移动
* 新行需要两个字符：回车符（CR）和
* 换行的（LF）。在 Unix 上，ASCII 行符被用于
* 两种用途，因此我们只需要 `\n`，它不会包含
* 回车符，下一行将从行符后的
* 列开始。这就是为什么文本文件在
* Unix 和 MS Windows 之间存在差异。在某些变体中，如 MS-DOS 和
* MS Windows，严格遵守了 ASCII 标准，
* 因此，换行同时需要 LF 和 CR。

```c
#if (LINUX_VERSION_CODE < KERNEL_VERSION(2,6,9) )
    (my_tty->driver)->write(my_tty, "\r\n", 2);
else
    (my_tty->driver)->write(my_tty, "\r\n", 2);
#endif
```

```c
static int print_string_init(void)
{
    // 示例实现逻辑
    return 0;
}

static void print_string_exit(void)
{
    // 示例实现逻辑
}
```

```c
module_init(print_string_init);
module_exit(print_string_exit);
```

## 10.2. 闪烁 LED

在某些条件下，你可能希望以更简单的方式与 tty 交互。闪烁 LED 是通过定期调用 `ioctl` 实现的。以下代码展示了这种内核模块的用法。





# Linux 内核模块编程指南

虽然你在这里看到了很多可以辅助调试的工具，但有些事情需要注意。调试几乎总是具有侵入性的。添加调试代码可能会改变现状，导致 bug 看起来像是消失了一样。因此，你应该尽量将调试代码减少到最少，并确保它们不会出现在生产代码中。

# 第 11 章 任务调度

### 11.1. 任务调度

通常，我们有一些必须在特定时间或特定频率执行的“家务”任务（housekeeping）。如果任务由进程执行，我们通过将其放入 `crontab` 文件来完成。如果任务由内核模块执行，我们有两种可能。第一种是在 `crontab` 文件中放入一个进程，该进程在需要时通过系统调用（例如打开一个文件）来唤醒模块。然而，这种方法极其低效——我们必须运行一个新的 `crontab` 进程，将一个新的可执行文件读入内存，而这一切仅仅是为了唤醒一个远留在内存中的内核模块。

与其这样做，我们可以创建一个函数，该函数会在每次定时器中断时被调用一次。我们的方法是创建一个在 `queue_struct` 中的任务，它持有指向该函数的指针。然后，我们使用 `queue_delayed_work` 将该任务放入名为 `my_workqueue` 的列表中，该列表是将在下一次定时器中断时执行的任务列表。由于我们希望该函数持续执行，因此在调用时我们需要将其重新放回 `my_workqueue`，以便下一次定时器中断使用。

这里我们还需要记住一点点。当模块被 `rmmod` 移除时，会检查它的第一个引用计数。如果为零，则调用 `module_cleanup`。然后，模块将连同所有函数一起从内存中移除。事物需要正确关闭，否则会发生糟糕的事情。看下面的代码如何安全地实现这一点。

示例 11-1. sched.c

```c
* sched.c - 调度一个每次定时器中断时调用的函数。
* 版权所有 (2001) Peter Jay Salzman
*/
* 必要的头文件
*/

* 内核模块标准包含
#include <linux/kernel.h>
#include <linux/module.h>
#include <linux/proc_fs.h>
#include <linux/workqueue.h>
#include <linux/sched.h>
#include <linux/init.h>
#include <linux/interrupt.h>
/* 我们正在进行内核工作 */
/* 具体地，一个模块 */
/* 因为我们使用了 proc fs，所以必要的 */
/* 我们在这里调度任务 */
/* 我们需要让自己睡眠
 稍后唤醒 */
/* 用于 init 和 -exit */
/* 用于 irqreturn_ */

struct proc_dir_entry *Our_Proc_File;
#define PROC_FILENAME "sched"
#define MY_WORK_QUEUE_NAME "Wqsched.c"

/* 到目前定时器中断被调用的次数
*/
static int TimerIntrpt = 0;
```

```c
static void intrpt_routine(void *);
static int die = 0;              /* 设置为 1 表示关闭 */
/*
* 此任务的 work队列结构，来自 workqueue.h
 */
static struct workqueue_struct *my_workqueue;
static struct work_struct Task;
static DECLARE_WORK(Task, intrpt_routine, NULL);

/*
* 此函数会在每次中断时被调用。注意 void *
* 任务函数可以用于多个目的，每次
* 获得一个不同的参数。
 */
static void intrpt_routine(void *irrelevant)
{
    /*
    增加计数器
    */
    TimerIntrpt++;

    /*
    如果清理程序想要我们死
    */
    if (die == 0)
        queue_delayed_work(my_workqueue, &Task, 100);
}
/*
* 将数据放入 proc fs 文件。
 */
ssize_t
procfile_read(char *buffer,
               char **buffer,
               off_t offset, int buffer_length, int *eof, void *data)
{
    int len;                      /* 实际使用的字节数 */
    /*
    * 它是静态的，所以当我们离开此函数时
    * 它仍然留在内存中
    */
    static char my_buffer[80];

    /*
    * 一次给出我们所有的信息，所以如果有人问我们
    * 是否有更多信息，答案应该总是否。
    */
    if (offset > 0)
        return 0;

    /*
    * 填充缓冲区并获取其长度
    */
    len = sprintf(my_buffer, "Timer called %d times so far\n", TimerIntrpt);

    /*
    * 告诉函数缓冲区在哪里
    */
```

```c
/*
*buffer_location = my_buffer;

/*
* 返回长度
 */
return len;
}
```

```c
/*
* 初始化模块 - 注册 proc 文件
 */
int __init_module_()
```

```c
/*
* 创建 /proc 文件
 */
Our_Proc_File = create_proc_entry(PROC_FILENAME);

if (Our_Proc_File == NULL) {
    return -ENOMEM;
}

my_workqueue = create_delayed_workqueue(MY_WORK_QUEUE_NAME);
queue_delayed_work(my_workqueue, &Task);

return 0;
}
```

```c
/*
* 清理模块
 */
void __exit_module_()
{
    remove_proc_entry(Our_Proc_File);
    cancel_delayed_work(my_workqueue, &Task);
    destroy_workqueue(my_workqueue);
}
```

[/content]

[content]
# Linux 内核模块编程指南

虽然你在这里看到了很多可以辅助调试的工具，但有些事情需要注意。调试几乎总是具有侵入性的。添加调试代码可能会改变现状，导致 bug 看起来像是消失了一样。因此，你应该尽量将调试代码减少到最少，并确保它们不会出现在生产代码中。

# 第 11 章 任务调度

### 11.1. 任务调度

通常，我们有一些必须在特定时间或特定频率执行的“家务”任务（housekeeping）。如果任务由进程执行，我们通过将其放入 `crontab` 文件来完成。如果任务由内核模块执行，我们有两种可能。第一种是在 `crontab` 文件中放入一个进程，该进程在需要时通过系统调用（例如打开一个文件）来唤醒模块。然而，这种方法极其低效——我们必须运行一个新的 `crontab` 进程，将一个新的可执行文件读入内存，而这一切仅仅是为了唤醒一个远留在内存中的内核模块。

与其这样做，我们可以创建一个函数，该函数会在每次定时器中断时被调用一次。我们的方法是创建一个在 `queue_struct` 中的任务，它持有指向该函数的指针。然后，我们使用 `queue_delayed_work` 将该任务放入名为 `my_workqueue` 的列表中，该列表是将在下一次定时器中断时执行的任务列表。由于我们希望该函数持续执行，因此在调用时我们需要将其重新放回 `my_workqueue`，以便下一次定时器中断使用。

这里我们还需要记住一点。当模块被 `rmmod` 移除时，会检查它的第一个引用计数。如果为零，则调用 `module_cleanup`。然后，模块将连同所有函数一起从内存中移除。事物需要正确关闭，否则会发生糟糕的事情。看下面的代码如何安全地实现这一点。

示例 11-1. sched.c

```c
* sched.c - 调度一个每次定时器中断时调用的函数。
* 版权所有 (2001) Peter Jay Salzman
*/
* 必要的头文件
*/

* 内核模块标准包含
#include <linux/kernel.h>
#include <linux/module.h>
#include <linux/proc_fs.h>
#include <linux/workqueue.h>
#include <linux/sched.h>
#include <linux/init.h>
#include <linux/interrupt.h>
/* 我们正在进行内核工作 */
/* 具体地，一个模块 */
/* 因为我们使用了 proc fs，所以必要的 */
/* 我们在这里调度任务 */
/* 我们需要让自己睡眠
 稍后唤醒 */
/* 用于 init 和 -exit */
/* 用于 irqreturn_ */

struct proc_dir_entry *Our_Proc_File;
#define PROC_FILENAME "sched"
#define MY_WORK_QUEUE_NAME "Wqsched.c"

/* 到目前定时器中断被调用的次数
*/
static int TimerIntrpt = 0;
```

```c
static void intrpt_routine(void *);
static int die = 0;              /* 设置为 1 表示关闭 */
/*
* 此任务的 work队列结构，来自 workqueue.h
 */
static struct workqueue_struct *my_workqueue;
static struct work_struct Task;
static DECLARE_WORK(Task, intrpt_routine, NULL);

/*
* 此函数会在每次中断时被调用。注意 void *
* 任务函数可以用于多个目的，每次
* 获得一个不同的参数。
 */
static void intrpt_routine(void *irrelevant)
{
    /*
    增加计数器
    */
    TimerIntrpt++;

    /*
    如果清理程序想要我们死
    */
    if (die == 0)
        queue_delayed_work(my_workqueue, &Task, 100);
}
/*
* 将数据放入 proc fs 文件。
 */
ssize_t
procfile_read(char *buffer,
               char **buffer,
               off_t offset, int buffer_length, int *eof, void *data)
{
    int len;                      /* 实际使用的字节数 */
    /*
    * 它是静态的，所以当我们离开此函数时
    * 它仍然留在内存中
    */
    static char my_buffer[80];

    /*
    * 一次给出我们所有的信息，所以如果有人问我们
    * 是否有更多信息，答案应该总是否。
    */
    if (offset > 0)
        return 0;

    /*
    * 填充缓冲区并获取其长度
    */
    len = sprintf(my_buffer, "Timer called %d times so far\n", TimerIntrpt);

    /*
    * 告诉函数缓冲区在哪里
    */
```

```c
/*
*buffer_location = my_buffer;

/*
* 返回长度
 */
return len;
}
```

```c
/*
* 初始化模块 - 注册 proc 文件
 */
int __init_module_()
```

```c
/*
* 创建 /proc 文件
 */
Our_Proc_File = create_proc_entry(PROC_FILENAME);

if (Our_Proc_File == NULL) {
    return -ENOMEM;
}

my_workqueue = create_delayed_workqueue(MY_WORK_QUEUE_NAME);
queue_delayed_work(my_workqueue, &Task);

return 0;
}
```

```c
/*
* 清理模块
 */
void __exit_module_()
{
    remove_proc_entry(Our_Proc_File);
    cancel_delayed_work(my_workqueue, &Task);
    destroy_workqueue(my_workqueue);
}
```





# Linux 内核模块编程指南

我在编写本章的示例代码时遇到了一个问题。一方面，为了让一个示例有用，它必须在每个人的计算机上运行并产生意义的结果。另一方面，内核已经包含了所有常见设备的驱动程序，而这些设备将无法与我要的操作共存。我找到的解决方案是为键盘中断编写一些代码，并禁用常规键盘中断处理程序。由于它在内核源文件中被定义为静态符号（具体为 `drivers/char/keyboard.c`），因此无法恢复它。在 `insmod` 这段代码之前，请在另一个终端执行 `sleep 120`；如果你使用了文件系统，请事后重启。

这段代码将自己绑定到 IRQ 1，这是 Intel 架构下键盘受控制的 IRQ。当它接收到键盘中断时，它会读取键盘状态（`inb (0x64)` 的目的）和扫描码（键盘返回的值）。然后，一旦内核认为可行，它就会运行 `got_char`，该函数会给出按键代码（扫描码的前七位）以及按键是被按下（如果第 8 位为 0）还是释放（如果不是）。

### 示例 12-1. intprtc.c

```c
/**
 * intprtc.c - 一个中断处理程序
 * 版权所有 (C) 2001 Peter Jay Salzman
 */

/**
 * 必要的头文件
 */

```c
/* 内核模块的标准头文件
*/
#include <linux/kernel.h>
#include <linux/module.h>
#include <linux/sched.h>
#include <linux/workqueue.h>
#include <linux/interrupt.h>
#include <linux/io.h>

/* 我们正在进行内核工作 */
/* 具体来说，是一个模块 */

/* 我们想要一个中断 */

#define MY_WORK_QUEUE_NAME "WQsched.c"
static struct workqueue_struct *my_workqueue;
```

/**
 * 只要内核认为可以执行内核模块允许的所有正常操作，
 就会调用此函数。
 */

```c
static void got_char(void *scscode)
{
    printk(KERN_INFO "Scan Code %x %s.\n",
           (int)((char*)scscode) & 0x7F,
           *((char*)scscode) & 0x80 ? "Released" : "Pressed");
}
```

/**
 * 此函数处理键盘中断。它从键盘读取相关
 * 信息，并将非时间关键部分
 * 放入工作队列。这部分将在内核认为安全时运行。
 */

```c
irqreturn_t irq_handler(int irq, void *dev_id, struct pt_regs *regs)
{
  /*
   * 这些变量是静态的，因为它们需要被
   * （通过指针）供底半部分程序访问。
   */
  static int initialised = 0;
  static unsigned char scancode;
  static struct work_struct task;
  unsigned char status;

  /*
   * 读取键盘状态
   */
  status = inb(0x64);
  scancode = inb(0x60);

  if (initialised == 0) {
    INIT_WORK(&task, got_char, &scancode);
    initialised = 1;
  } else {
    PREPARE_WORK(&task, got_char, &scancode);
  }

  queue_work(my_workqueue, &task);

  return IRQ_HANDLED;
}

/* 初始化模块 - 注册 IRQ 处理程序

int init_module() {
  my_workqueue = create_workqueue(MY_WORK_QUEUE_NAME);

  /*
   * 因为键盘处理程序不会与另一个处理程序共存，
   * 我们必须在执行任何操作之前禁用它
   *（释放 IRQ）。由于我们不知道它在哪里，因此无法
   * 以后恢复它 - 所以在我们完成后必须重启计算机。
   */
  free_irq(1, NULL);

  /*
   * 请求 IRQ 1（键盘 IRQ）跳转到我们的 irq_handler。
   * SA_SHIRQ 表示我们希望在该 IRQ 上有处理程序。
   * SA_INTERRUPT 可用于将处理程序变为快速中断。
   */
  return request_irq(1, /* PC 上的键盘 IRQ  */
      irq_handler, /* 我们的处理程序 */
      SA_SHIRQ, "test_keyboard_irq_handler",
      (void *) (irq_handler));
}

/* 清理
void cleanup_module() {
  /*
   * 这只是为了完整性。它完全无关，
   */
  /*
   * 我们没有办法恢复正常的键盘中断，所以
   * 计算机完全无法使用，且必须重启。
   */
  free_irq(1, NULL);
}
/*
 * 某些与工作队列相关的函数仅对 GPL 许可的模块可用
 */
MODULE_LICENSE("GPL");
```

# 第 13 章 对称多处理

## 13.1. 对称多处理

提高硬件性能最简单且廉廉的方法之一是在板上放置多个 CPU。这可以通过让不同的 CPU 承担不同的任务（非对称多处理）或通过让它们全部并行执行相同任务（对称多处理，也称为 SMP）来实现。有效执行对称多处理需要对计算机执行的任务有专业知识，而这在 Linux 这样的通用操作系统中是不可提供的。另一方面，对称多处理的实现相对容易。

我所说的相对容易，正是指这个意思：并不是真的非常简单。在对称多处理环境中，CPU 共享相同的内存，因此在在一个 CPU 上运行可能会影响另一个 CPU 使用的内存。你无法再确定你在上一行中设置为特定值的变量是否仍然具有该值；另一个 CPU 可能在你没看的时候对它进行了操作。显然，像这样编程是不可能的。（等一下，“像这样编程是不可能的”是夸张，但它需要非常小心）。

实际上，SMP 的主要问题是多个 CPU 可以同时访问相同的数据结构。这会导致竞态条件和其他同步问题。

考虑中断的情况。如果发生中断，它可以被任何 CPU 捕获。如果两个 CPU 正在处理同一个中断，它们可能都尝试访问同一个数据结构，这可能会导致损坏。因此，我们必须确保只有一个 CPU 可以访问该数据结构。

Linux 中有几种实现同步的方法，包括锁（lock）、信号量（semaphore）和自旋锁（spinlock）。锁是一种允许一次时间只有一个线程访问资源的原语。信号量类似于锁，但它允许有限数量的线程访问资源。自旋锁是一种锁，CPU 会不断“旋转”直到锁可用。这在锁的持有时间非常短时非常有用。

在本章中，我们将讨论如何在 SMP 环境中使用这些同步原语。我们还将查看一些常见的陷阱以及避免它们的方法。

