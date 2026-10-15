
在内核中，无论代码是动态生成的还是永久编译进内核的。`insmod`与用户态交互的操作是基于此的。

```
wolfgang@meitner file vfat.ko
vfat.ko: ELF 64-bit relocatable, x86-64 (SYS), not stripped
```

`file`命令的输出表明模块文件是可重地的，这是用户态中一个熟悉的术语。可重地文件没有绝对地址的引用，仅指向代码内部的相对地址，并且可以在动态链接器修改的内存偏移处加载。然而，内核本身并不是执行重定位的动态库。

在早期内核版本（直到 2-4）中，模块必须以多进程方式加载（在内核中解析内存，然后在用户态中进行数据重定位并将二进制文件复制到内核），而现在只需要一个系统调用`init_module`在内核本身执行所有操作。

## 处理未解析引用

为了与内核的其余部分工作，模块必须使用内核提供的函数。这些可能是几乎每个部分使用的通用辅助函数，如`printk`或`kalloc`。针对模块功能提出的更具体的函数也必须使用。RAMfs模块允许文件系统在内存中可用（通常作为内存磁盘），并像其他实现文件系统的代码一样——调用`register_filesystem`将其添加到内核可用文件列表中。模块还使用了（包括）`generic_file_read`和`generic_file_write`函数，这些函数存在于内核中并被内核函数使用。

当在用户态中使用库时，会出现类似的情况。程序使用外部库中定义的函数，通过在自己的二进制代码中存储指向函数的指针——而不是函数本身的实现（当然，其他符号类型如全局变量也可以代替函数）。静态库的引用在程序链接时（使用`ld`）解析，动态库在二进制文件加载时（使用`ld.so`）解析。

## 第7章：模块

`nm`工具可用于生成模块（或任何对象文件）中所有外部函数的列表。以下示例显示了`romfs`模块中使用了一些函数但被标记为外部引用的函数：

```
wolfgang@meitner nm romfs.ko
U generic_read_dir
U generic_ro_fops

U printk

U register_filesystem
..
```

输出中的`U`代表未解析引用（unresolved reference）。请注意，如果编译内核时没有启用`KALLMS_ALL`，则`generic_ro_fops`将不可见。在这种情况下，只包含函数符号，而不再包含像`generic_ro_fops`这样的常量结构体或其他符号。

显然，这些函数定义在内核基础中，因此已经存在于内存中了。但如何通过匹配地址来解析找到的引用呢？为此，内核提供了一个所有导出函数的列表；该列表显示了内存地址以及相应的函数名，可以通过`proc`文件系统访问，这就是`/proc/kallsyms`文件的作用：

```
wolfgang@meitner cat /proc/kallsyms | grep printk
ffffffff8032a7 T printk
```

上述示例中的函数可以使用以下信息完全解析，所有这些信息都在内核的符号表中：

```
ffffffff0000324aa T printk
ffffffff00003407e0 T generic_file_write
ffffffff8043c710 R generic_ro_fops
ffffffff000076d20 T register_filesystem
```

`T`表示符号位于文本段（text segment），而`D`表示它位于数据段（data segment）。关于对象文件布局的更多信息，请参阅附录 E。

从逻辑上讲，符号表中的信息不仅取决于内核配置，还取决于具体的处理器。在我们的示例中，我们使用的是 AMD64 CPU。例如，在 IA-32 CPU 上搜索符号表会产生如下结果：

```
c0119290 T printk
c012b7b0 T generic_read_dir
c0129f0c0 D generic_ro_fops
c0139340 T register_filesystem
```

地址不仅很短（毕竟 IA-32 使用的是 32 位字长），而且在逻辑上，它们指向不同的位置。

> 注意，由于引用是在内核本身而非用户空间解析的，因此该文件仅供信息参考，并没有使用模块工具。

### 7.2.2 依赖关系

模块也可以依赖于一个或多个模块。让我们看看`vfat`模块，它依赖于`fat`模块，因为后者包含了几个区分这两种文件系统变体的函数。在对象文件`vfat.o`看来，这意味着存在对定义在`fat.o`中的函数的代码引用。这种方法的优势是显而易见的：因为处理 FAT 的代码与处理 FAT 文件系统的代码仅在几个例程上不同，大部分代码可以被两个模块共享。这不仅减少了系统内存的需求，还使代码更短、更易读且更容易维护。

`nm`工具清楚地阐述了这种情况：

```
wolfgang@meitner nm vfat.ko
...
  U fat_alloc_new_dir
  U fat_attach
...
wolfgang@meitner nm fat.ko
0000000000001ad T fat_alloc_new_dir
000000000004a67 T fat_attach
...
```

我有两个例子：`fat_alloc_new_dir`和`fat_attach`（同时也提供了许多`vfat`使用的函数）。如`nm`输出所示，这两个函数被列为未解析引用，而在`fat.o`中，它们带有（不相关的）对象文件地址。

自然地，将这些地址补丁到`vfat_ko`的对象代码是没有意义的，因为在`fat.ko`重定位后，这些函数会在内存中完全不同的地方。更有意义的是`fat`模块添加后的函数地址。这些信息通过`/proc/kallsyms`给用户，但仍保留在内核中。对于内核编译的内核以及随后添加的所有模块，有一个数组将符号分配到它们在虚拟空间中的地址。

向内核添加模块时与以下项相关：

- 内核提供的函数符号列表可以在模块加载时动态扩展。如你所见，模块可以精确指定其代码中的哪些函数被发布供通用使用，哪些可能仅供内部使用。
- 如果模块之间存在相互依赖关系，向内核添加模块的顺序至关重要。例如，如果尝试在`fat`进入内核之前加载`vfat`模块，该尝试将失败，因为许多函数的地址无法解析（且代码将无法工作）。

> FAT（文件分配表）是 MS-DOS 使用的非常简单的文件系统，仍用于软磁盘；vfat 是一种（最小的）增强，具有相同的基础结构，支持最多 255 个字符的文件名，且不再限制于 8 + 3 方案。

如果用户不了解模块间依赖关系的特定结构，模块之间的依赖关系可能会在内核动态扩展期间变得极其复杂。虽然在我们的示例中这不是问题，因此需要一种自动分析依赖关系的方法。该程序在每次系统启动或安装新模块后都会运行。依赖关系存储在一个文件中。默认情况下，会生成`/lib/modules/version/modules.dep`。vfat 模块的条目如下：

```
wolfgang@meiner cat modules.dep | grep vfat
/lib/modules/2.64/kernel/fs/vfat.ko: /lib/modules/2.64/kernel/fs/fat.ko
```

这些信息由`modprobe`处理，用于在依赖关系解决后插入模块。其策略很简单：`modprobe`读取依赖文件内容，搜索描述模块的行，并编译先决模块列表。由于这些模块可能依赖于其他模块，此过程将持续到所有模块已知。

### 7.2.3 查询模块信息

额外的信息是描述模块用途的文本，它们直接存储在二进制文件中。可以使用模块发行中的`modinfo`工具进行查询。存储了各种数据：

- 驱动程序的作者，通常带有电子邮件地址。这些信息非常有用，特别是在报告 Bug 时（让开发者获得一些满足感）。
- 驱动功能的简要描述。

> 当然，还需要检查模块是否已存在内核中——逻辑上，如果是的话，则不会再次添加。

- 传递给模块的配置参数；可能包含对精确参数的描述。
- 所支持设备的设计（例如，软磁盘的`fd`）。
- 模块分发的许可证。

模块信息中还提供了一个单独的列表，用于接受驱动程序支持的不同设备类型列表。

使用`modinfo`查询信息并不困难，如下例所示：

```bash
$ wolfgangmeitner-# ~ /sbin/modinfo 8139too
filename: /lib/modules/2.6.24/kernel/net/8139too.ko
version: 0.9.28
license: GPL
description: RealTek-RTL-8139 Fast Ethernet driver
author: Jeff Garzik <jgarzik@pobox.com>
alias: 10D3CC1F162281EBRACED
alias: vci:v00008139sv*sd*bc*sc*1*
```
