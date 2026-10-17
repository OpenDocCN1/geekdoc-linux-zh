
这个特定示例突出了本章中反复提到的要点之一：这是一个特定于架构的工具。你必须使用配置和编译以匹配你正在使用的目标二进制文件架构的工具。与交叉编译器一样，`addr2line`是一个交叉工具，是二进制实用工具包的一部分。

### 13.6.3 strings

`strings`实用工具检查二进制文件中的ASCII字符串数据。当源代码或调试符号可能不可用时，这对于检查内存转储特别有用。你经常会发现，通过将字符串追溯到导致问题的二进制文件，可以缩小崩溃原因的范围。虽然`strings`有一些命令行选项，但学习和使用它很容易。有关更多详细信息，请参阅`man`手册页。

### 13.6.4 ldd

虽然严格来说不是二进制实用工具，但`ldd`脚本是嵌入式开发人员的另一个有用工具。它是C库包的一部分，存在于几乎所有Linux发行版上。`ldd`列出给定目标文件或文件的共享对象库依赖项。我们在第11章“BusyBox”中介绍了`ldd`。请参见列表11-2了解使用示例。`ldd`脚本在开发`ramdisk`镜像时特别有用。在各种嵌入式Linux邮件列表中询问的最常见故障之一是在挂载根文件系统后发生的内核恐慌：

> VFS: Mounted root (nfs filesystem).  
> Freeing unused kernel memory: 96k init  
> Kernel panic - not syncing: No init found.  Try passing init=option to kernel...

最常见的原因之一是根文件系统镜像（无论是`ramdisk`、Flash还是NFS根文件系统）没有内核试图执行的二进制文件所需的支持库。使用`ldd`，你可以确定每个二进制文件需要哪些库，并确保将它们包含在你的`ramdisk`或其他根文件系统镜像中。在之前的内核恐慌示例中，`init`确实位于文件系统中，但Linux动态加载器`ld.so.1`缺失。使用`ldd`非常简单明了：

```
$ escalate_bus-ldd init  

libc.so.6 => /opt/mvl/.../lib/libc.so.6 (0xdead1000)  

ld-linux.so.3 => /opt/mvl/.../lib/ld-linux.so.3 (0xdead2000)
```

这个简单示例表明`init`二进制文件需要两个动态库对象：`libc`和`ld-linux`。两者都必须位于你的目标上，并且必须可被你的`init`二进制文件访问——也就是说，它们必须可读且可执行。

### 13.6.5 nm

`nm`实用工具显示目标文件中的符号。这对于各种任务都有用。例如，在交叉编译大型应用程序时，你会遇到未解析的符号。你可以使用`nm`找到包含这些符号的目标模块，然后修改你的构建环境以包含它。

`nm`实用工具为每个符号提供属性。例如，你可以发现该符号是局部的还是全局的，或者它是否仅在特定的目标模块中定义或引用。列表13-18复制了在对U-Boot ELF图像`u-boot`运行`nm`的输出中的几行。

#### 列表 13-18
使用`nm`显示符号

```
$ ppc_85xx-nm u-boot

...

fff23140 b _bss_address

fff24c98 B BootFile

fff06d64 T BootRequest

fff00118 t boot_warm

fff21010 d border

fff23000 A __bss_start

...
```
