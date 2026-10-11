
在遍历整个 `machine_descs` 表后，`setup_machine_fdt()` 函数根据每个 `machine_desc` 匹配的 `compatible` 属性中的项返回“最兼容”的 `machine_desc`。如果没有找到匹配的 `machine_desc`，它返回 NULL。`setup_machine_fdt()` 函数还负责在选择机器后早期扫描设备树。

# 3 章

## 最简单的驱动程序

Linux 嵌入式系统设计的核心概念是将用户应用程序与底层硬件分离。用户空间应用程序不允许访问外设寄存器、存储介质甚至 RAM 内存。相反，硬件通过内核驱动程序访问，RAM 内存由内存单元 `MMU` 管理，应用程序在虚拟地址上运行。

这种分离提供了健壮性。如果假设 Linux 内核运行正常，那么只允许内核与硬件交互可以防止应用程序无意或恶意地错误配置硬件并使其处于未知状态。

这种分离还提供了移植性。如果只有内核驱动程序管理硬件特定代码，那么在将系统从一个平台迁移到另一个平台时，只需要修改这些驱动程序。应用程序访问一组跨硬件平台一致的驱动 API，允许应用程序在不修改或少修改代码的情况下进行迁移。

设备驱动程序可以是内核模块，也可以静态编译到内核映像。默认内核将大多数驱动静态编译到内核中，因此它们会自动启动。内核模块不一定是设备驱动；它是内核的扩展。内核模块加载到内核的虚拟内存中。将设备驱动程序编译为模块使得开发更容易，因为可以在不重启内核的情况下加载、测试和卸载。内核模块通常位于根文件系统的 `/lib/modules/<kernel_version>/`。

每个内核模块都有一个 `init()` 和 `exit()`。`init()` 函数在驱动加载时调用一次，`exit()` 函数在驱动移除时调用。`init()` 函数让操作系统知道驱动程序能够做什么，以及在特定事件发生时必须调用它的哪些函数（例如注册驱动程序到总线，注册字符设备）。`exit()` 函数释放 `init()` 请求的所有资源。

`module_init()` 和 `module_exit()` 宏导出 `init()` 和 `exit()` 函数的符号，以便加载你的模块的内核代码能够识别这些入口点。

# http://www.rejoiceblog.com/

## 第3章

有一组宏用于识别模块的各种属性。这些字符串被封装到模块中，并被各种工具访问。最重要的模块描述宏是 `MODULE_LICENSE` 宏。如果此宏没有设置为某些 GPL 许可证标签，当你加载模块时，内核将变为“被污染”`tainted`。当内核被污染时，意味着它处于一种社区不受支持的状态。大多数内核开发者会忽略涉及被污染内核的错误报告，社区成员可能会要求你在进行内核诊断之前修复该状况，以便处理与内核相关的诊断问题。此外，当内核被污染时，调试功能和 API 调用可能会禁用。

## 许可协议

Linux 内核根据 GNU 通用公共许可证第 2 版 `GPL2` 许可。该许可赋予你使用、研究、修改和共享软件的权利。然而，如果分发该软件（无论是否经过过修改），GPL 要求你以相同的许可证和源代码重新分发该软件。如果对 Linux 内核进行了修改（例如为了适配你的硬件），它属于内核的派生作品，因此必须根据 `GPLv2` 发布。但是，你只需要在设备开始分发给你的客户时这样做，而不是面向全世界。

本书中提供的内核模块根据 GPL 许可证发布。有关源源许可证的更多信息，请参阅 http://opensource.org/licenses。

## 实验 3.1: "helloworld" 模块

在你的第一个内核模块中，每当加载和卸载模块时，你只需向控制台发送一些信息。`hello_init()` 和 `hello_exit()` 函数包含一个 `pr_info()` 函数。这与你在应用程序中使用的 `printf` 语法相似，但 `pr_info()` 用于在内核空间打印日志消息。如果你查看真实的内核，你总是会看到类似下面的内容：

```
printk(KERN_ERR "something went wrong, return code: %d\n", ret);
```

当 `KERN_ERR` 是 `include/linux/levels.h` 中的不同日志级别之一时，它指定了错误信息的严重程度。`pr_*` 宏是位于 `include/linux/printk.h` 中的简单简写定义，对应各自的 `printk` 调用，并应该在较新的驱动程序中使用。

在第 1 章的“开发 Linux 驱动程序的 Eclipse 配置”中，你使用 Eclipse IDE 创建了 `my_modules` 项目。该项目将用于开发本书中的所有驱动程序，尽管如果你不想使用 Eclipse 工作，也可以使用你喜欢的编辑器来编写驱动程序。`helloworld.c` 和 `Makefile` 文件已创建并保存在 `modules` 目录下，但没有向它们写入任何代码。现在是给这些文件写代码了。

在后续的实验中，你将重复相同的步骤创建驱动源文件 `<模块名>.c`。通过简单将新的 `<模块名>.o` 添加到 Makefile 的 `obj-m` 中，所有实验都可以复用同一个 Makefile。

在 Build Targets（构建目标）选项卡中添加了 `all`、`deploy` 和 `clean` 按钮，用于编译、清理和部署所有已开发的模块。

查看下一个列表 3-1 中针对 i-MX7D 处理器的 "helloworld" 驱动源码 `helloworld_imx.c`。

注意：SAMA5D2 `helloworld_sam.c` 和 BCM2837 `helloworld_rpi.c` 驱动程序的源代码可以从本书的 GitHub 仓库下载。

### 列表 3-1: helloworld_imx.c

```
#include <linux/module.h>

static int __init_hello_init(void)

{

    pr_info("Hello world\n");

    return 0;

}

static void __exit_hello_exit(void)

{

    pr_info("Hello world\n");

}

module_init(hello_init);

module_exit(hello_exit);

MODULE_LICENSE("GPL")

MODULE_AUTHOR("Alberto Liberal <aliberal@arroweurope.com>");

MODULE_DESCRIPTION("This is a print Hello World module");
```

查看下一个列表 3-2 用于编译此模块的 Makefile。新开发的内核模块名称将添加到此 Makefile 中。

Makefile 中添加了安全拷贝 `SCP` 以将模块传输到目标文件系统，所示所示：

```
scp *.ko root@10.0.0.10:
```

### 列表 3-2: Makefile

```
obj-m += helloworld.o
```

```
KERNEL_DIR ?= $(HOME)/my-linux-idx
```

```
all:
    make -C $(KERNEL_DIR) \
        ARCH=arm CROSS_COMPILE=arm-poky-linux-gnueabi- \
        SUBDIRS=$(PWD) modules
```

```
clean:
    make -C $(KERNEL_DIR) \
        ARCH=arm CROSS_COMPILE=arm-poky-linux-gnueabi- \
        SUBDIRS=$(PWD) clean
```

```
deploy:
    scp *.ko root@10.0.0.10:
```

## helloworld_imx.ko

```
root@imx7dsabres~# insmod helloworld_imx.ko /* 加载模块 */
root@imx7dsabres~# modinfo helloworld_imx.ko /* 查看模块中定义的 MODULE 宏 *//
root@imx7dsabres~# cat /proc/sys/kernel/tainted /* 应该是 409 */
```

root@imx7dsabres~# cat /proc/sys/kernel/tainted /* 应该是 409 */
root@imx7dsabres~# cat /proc/sys/kernel/tainted

# 第 3 章

## 最简单的驱动程序

```c
struct timeval {
    __kernel_time_t tv_sec;      /* 秒 */
```
