
### 8.1.5 安装你的设备驱动程序

现在该驱动程序已经构建完成，我们可以在运行中的内核上加载和卸载它，以观察其行为。在加载模块之前，我们需要将其复制到目标系统上的适当位置。虽然我们可以将其放在任何想要的位置，但对于内核模块在运行的 Linux 系统上的存放位置，已经形成了一种约定。与模块编译类似，让内核构建系统为我们完成这一工作是最简单的。`Makefile` 目标 `modules_install` 会自动将模块以逻辑布局放置在系统中。你只需要提供期望的位置作为默认路径的前缀。

在标准的 Linux 工作站安装中，你可能已经知道设备驱动程序模块位于 `/lib/modules/<kernel-version>/...`，其排序方式类似于 Linux 内核树中的设备驱动程序目录层次结构。¹ 默认情况下，`<kernel-version>` 字符串是通过在你的目标 Linux 系统上执行命令 `uname -r` 生成的。如果你不向内核构建系统提供安装前缀，你的模块将安装在你自己的工作站的 `/lib/modules/...` 目录中。这可能不是你本来的意图。你可以指向主目录中的一个临时位置，并手动将模块复制到目标文件系统。或者，如果你的目标嵌入式系统使用 NFS 根挂载到本地开发

> ¹ 此路径由 Red Hat 和 Fedora 发行版使用，也是本章末尾引用的文件系统层次结构标准所要求的。其他发行版可能使用文件系统中不同的位置来存放内核模块。

工作站时，你可以将模块直接安装到目标文件系统。以下示例假设采用后者。

```bash
$ make ARCH=arm CROSS_COMPILER=pacable_be- \
    INSTALL_MOD_PATH=/home/chris/sandbox/coyote-target \
    modules install
```

这将把你所有的模块放置到目录 `coyote-target` 中，在这个示例系统中，该目录通过 NFS 导出，并挂载为目标系统的根目录。[3]

### 8.1.6 加载你的模块

完成所有必要步骤后，我们现在可以加载并测试设备驱动程序模块了。列表 8-5 展示了在嵌入式系统上加载随后卸载设备驱动程序时产生的输出。

#### 列表 8-5
#### 加载和卸载模块

```bash
$ modprobe hello1     # 加载驱动程序
Hello Example Init
$ modprobe -r hello1  # 卸载驱动程序
Hello Example Exit
$
```

你应该能够将输出与我们在列表 8-1 中找到的设备驱动程序源代码对应起来。除了通过 `printk()` 向内核日志系统打印消息（我们在控制台上看到这些消息）[4] 之外，该模块不做其他工作。当模块被加载时，模块初始化函数会被调用。我们使用 `module_init()` 宏指定在插入模块时将被执行的初始化函数。我们将其声明如下：

```c
module_init(hello_init);
```

在我们的初始化函数中，我们只是打印出强制要求的问候消息并返回。在实际的设备驱动程序中，这是你执行初始资源分配和硬件设备初始化的地方。类似地，当我们卸载模块（使用 `modprobe -r` 命令）时，我们的模块退出例程会被调用。

如列表 8-1 所示，退出例程使用 `module_exit()` 宏指定。

这就是一个能够在实际内核中进行活插入的骨架设备驱动程序的全部。在随后的章节中，我们将为可加载设备驱动程序模块引入额外的功能，以说明用户空间程序如何与设备驱动程序模块进行交互。

## 8.2 模块工具

我们在列表 8-5 中简要介绍了模块工具。在那里，我们使用模块工具 `modprobe` 从 Linux 内核中插入和移除设备驱动程序模块。有许多小型工具用于管理设备驱动程序模块。本节将介绍这些工具。建议你查阅每个工具的手册页以获取完整的详细信息。事实上，那些对深入了解 Linux 可加载模块感兴趣的人应该查阅这些工具的源代码。本章末尾的 8.6.1 节“附加阅读建议”包含了可以找到这些工具的参考资料。

### 8.2.1 insmod

`insmod` 工具是向运行中的内核插入模块的最简单方法。你提供一个完整的路径名，`insmod` 完成工作。例如：

```bash
$ insmod /lib/modules/2.6.14/kernel/drivers/char/examples/hello1.ko
```

这将模块 `hello1.ko` 加载到内核中。输出将与列表 8-5 中显示的一样——即 Hello 消息。`insmod` 工具是一个简单的程序，不需要也不接受任何选项。因为它没有搜索模块的逻辑，所以需要完整的路径名。大多数时候，你会使用稍后描述的 `modprobe`，因为它具有更多的功能和能力。

### 8.2.2 模块参数

许多设备驱动程序模块可以接受参数来修改其行为。示例包括启用调试模式、设置详细报告或指定模块特定选项。`insmod` 工具通过在模块名称后指定参数（在某些上下文中也称为选项）来接受参数。列表 8-6 展示了我们修改后的 `hello1.c` 示例，添加了一个用于启用调试模式的单一模块参数。

#### 列表 8-6
#### 带参数的示例驱动程序

```c
/* Example Minimal Character Device Driver */
#include <linux/module.h>
static int debug_enable = 0; /* Added driver parameter */
module_param(debug_enable, int, 0); /* and these 2 lines */
MODULE_PARM_DESC(debug_enable, "Enable module debug mode.");
static int __init hello_init(void)
{
    /* Now print value of new module parameter */
    printk("Hello Example Init - debug mode is %s\n",
        debug_enable ? "enabled" : "disabled");
    return 0;
}
static void __exit hello_exit(void)
{
    printk("Hello Example Exit\n");
}
module_init(hello_init);
module_exit(hello_exit);
MODULE_AUTHOR("Chris Hallinan");
MODULE_DESCRIPTION("Hello World Example");
MODULE_LICENSE("GPL");
```

我们的示例设备驱动程序模块增加了三行代码。第一行声明了一个用于保存调试标志的静态整数。第二行是一个在 `.../include/linux/moduleparam.h` 中定义的宏，它将模块参数注册到内核模块子系统。第三行新代码是一个宏，它将与参数关联的字符串描述注册到内核模块子系统。当我们稍后在本章中检查 `modinfo` 命令时，这个目的将变得清晰。

如果我们现在使用 `insmod` 插入我们的示例模块，并添加 `debug_enable` 选项，我们应该会看到基于列表 8-6 中修改后的 `hello1.c` 模块的结果输出。

```bash
$ insmod /lib/modules/.../examples/hello1.ko debug_enable=1
Hello Example Init - debug mode is enabled
```

或者，如果我们省略可选的模块参数：

```bash
$ insmod /lib/modules/.../examples/hello1.ko
Hello Example Init - debug mode is disabled
```

### 8.2.3 lsmod

`lsmod` 工具也相当简单。它只是显示已插入内核的模块的格式化列表。较新的版本不接受参数，只是格式化 `/proc/modules` 的输出。[5] 列表 8-7 是 `lsmod` 输出的一个示例。

#### 列表 8-7
#### lsmod 示例输出格式

```bash
$ lsmod
Module                Size Used by
ext3                  121096 0
jbd                    49656 1 ext3
loop                   12712 0
hello1                 1412 0
$
```
