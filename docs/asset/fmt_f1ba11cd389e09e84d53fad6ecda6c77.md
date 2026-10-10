
## cscope
`cscope`托管在`http://cscope.sourceforge.net/`，它从源码树中的所有文件构建符号数据库，因此你可以快速定位声明、定义、正则表达式等。`Cscope`可能不如`lxr`那样通用，但它提供了使用你最喜欢的文本编辑器的搜索功能而不是浏览器的灵活性。从内核树的根目录，发出`cscope -qkRv`命令以构建交叉引用数据库。`-q`选项生成更多的索引信息，使搜索速度明显加快，但代价是额外的初始启动时间。`-k`选项要求`cscope`调整其行为以适应内核源码，`-R`请求递归子目录遍历，`-v`请求详细消息。你可以从`man`页面获取详细的调用语法。

## ctags/etags
`ctags`实用工具可从`http://ctags.sourceforge.net/`下载，它为许多语言生成交叉引用标签，以便你可以通过`vi`等编辑器在源码树中定位符号和函数定义。从内核树的根目录执行`make tags`以`ctag`所有源文件。`etags`实用工具生成类似的索引信息，由`emacs`编辑器理解。发出`make etags`以`etag`你的内核源文件。

## Utilities
如`grep`、`find`、`sdiff`、`precess`、`od`、`dd`、`make`、`tar`、`file`和`objdump`等工具。

## GCC options
你可以使用`-E`选项要求`GCC`生成预处理源代码。预处理代码包含头文件扩展，减少了在嵌套包含文件中跳转跳过以展开多个宏级别的需要。这是一个预处理`drivers/char/mydrv.c`并在`mydrv.i`中产生展开输出的使用示例：
```bash
gcc -E drivers/char/mydrv.c -D__KERNEL__ -Iinclude -Iinclude/asm-x86/mach-default > mydrv.i
```

使用`-I`选项指定的包含路径取决于你的代码中包含的头文件。

如果使用`-S`选项，`GCC`会生成汇编列表。要为`drivers/char/mydrv.c`在`mydrv.s`中生成汇编列表，请执行以下操作：
```bash
gcc -S drivers/char/mydrv.c -D__KERNEL__ -Iinclude -Ianother/include/path
```

## 构建内核

现在你对源码树布局有了概念，让我们进行一个简单的代码更改，编译并使其运行。转到顶级`init/`目录，并尝试对初始化文件`main.c`进行小的代码更改。在函数`start_kernel()`的开头添加一个打印语句，声明你对北极熊的爱：

```c
asm("__init") void __init start_kernel(void)
{
    char *command_line;
    extern struct kernel_param __start___param[],
        __stop___param[];
+     printk("Penguins are cute, but so are polar bears\n");
    /* ... */
    rest_init();
}
```

你现在准备开始构建过程。转到源码树的根目录，并以干净的状态开始：

```bash
cd /usr/src/linux-X.Y.Z/
make clean
```

配置内核。这是你挑选和选择构成操作系统部件的时刻。你可以指定每个期望的组件是静态还是动态链接到内核：

```bash
make menuconfig
```

`menuconfig`是内核配置菜单的文本界面。使用`make xconfig`获取图形界面。你选择的配置信息保存在名为`.config`的文件中，位于源码树的根目录。如果你不想从头编织配置，使用文件`arch/your-arch/defconfig`（如果有多个支持的平台，使用`arch/your-arch/configs/your-machine_defconfig`）作为起点。因此，如果你正在为32位`x86`架构编译内核，请执行以下操作：

```bash
cp arch/x86/configs/i386_defconfig .config
```

编译内核并生成压缩的启动映像：

```bash
make bzImage
```

内核映像产生在`arch/x86/boot/bzImage`。更新你的启动分区：

```bash
cp arch/x86/boot/bzImage /boot/vmlinuz
```

你可能需要通知你的引导加载程序新的启动映像已到达。如果你使用的是`GRUB`引导加载程序，它会自动找出这一点；但如果你使用的是`Lilo`，请提高一个标志：

```bash
/sbin/lilo
Added linux *
```

最后，重启机器并进入你的新内核：

```bash
reboot
```

启动序列中的第一条消息启动了你为北极熊的`campaign`。

## 可加载模块

由于`Linux`运行在多种架构上并支持数以万计的`I/O`设备，将支持所有可能设备的代码永久编译到基础内核中是不可行的。发行版通常打包一个最小的内核映像，并以内核模块的形式提供其余的功能。在运行时，必要的模块根据需要动态加载。

要生成模块，请转到你的内核源码树的根目录并构建：

```bash
cd /usr/src/linux-X.Y.Z/
make modules
```

要安装生成的模块，请执行以下操作：

```bash
make modules_install
```

这会在`/lib/modules/X.Y.Z/kernel/`下创建内核源目录结构，并用可加载模块对象填充它。这也调用`depmod`实用程序，在文件`/lib/modules/X.Y.Z/modules.dep`中生成模块依赖项。

以下实用程序可用于操作模块：`insmod`、`rmmod`、`lsmod`、`modprobe`、`modinfo`和`depmod`。前两个是插入和移除模块的实用程序，而`lsmod`列出当前加载的模块。`modprobe`是`insmod`的更聪明版本，它在检查`/lib/modules/X.Y.Z/modules.dep`的内容后，也会插入依赖模块。例如，假设你需要挂载`USB`闪存驱动器上的虚拟文件分配表（`VFAT`）分区。使用`modprobe`加载`VFAT`文件系统驱动：[2]

> [2] 此示例假设该模块未被内核自动加载。如果在配置期间启用了自动内核模块加载（`CONFIG_KMOD`），当内核检测到缺失的子系统时，会自动运行带有适当参数的`modprobe`。你将在第4章“奠定基础”中学习模块自动加载。

```bash
modprobe vfat
lsmod
```

```
Module  Size  Used by
vfat  14208  0
fat   49052  1 vfat
nls_base  9728  2 vfat, fat
```

正如你在`lsmod`输出中看到的那样，`modprobe`插入了三个模块而不是一个。`modprobe`首先确定它必须插入`/lib/modules/X.Y.Z/kernel/fs/vfat/vfat.ko`。但当它查看依赖文件`/lib/modules/X.Y.Z/modules.dep`时，它发现以下行，并意识到它必须先加载另外两个依赖模块：

```text
/lib/modules/X.Y.Z/kernel/fs/vfat/vfat.ko:
  /lib/modules/X.Y.Z/kernel/fs/fat/fat.ko
  /lib/modules/X.Y.Z/kernel/fs/nls/nls_base.ko
```

然后它继续加载`fat.ko`和`nls_base.ko`，然后尝试插入`vfat.ko`，从而自动加载你挂载`VFAT`分区所需的所有模块。

## 开始之前

`Linux`已经穿越了多种地形，如今已成为业界前沿技术，因此你可以将其作为理解操作系统概念、处理器架构甚至行业领域的载体。当你学习设备驱动子系统中使用的某种技术时，不妨再深入一层，探究该设计选择背后的根本原因。

除非文中另有明确说明，否则本文假设读者熟悉32位`x86`架构。不过，本书也考虑到你更有可能为嵌入式设备而非传统`PC`兼容系统编写设备驱动这一事实。例如，关于串行驱动的章节考察了两个设备：一个`PC`衍生平台上的触摸控制器和一个手机上的`UART`。或者，关于`I²C`设备驱动的章节则查看了`PC`系统上的`EEPROM`和嵌入式设备上的实时时钟。本书还将向你介绍内核为大多数驱动类提供的核心基础设施，这些基础设施屏蔽了设备驱动对架构的依赖。

设备驱动调试技巧在本书末尾的第21章中讨论，因此当你阅读本书并开发驱动时，不妨提前跳读该章节，这会大有裨益。
