
| D2B70000 | 4 | 4 | - | rwx-- | libb.so |
| D2B80000 | 4 | 4 | 4 | r-x-- | liba.so |
| D2B90000 | 4 | 4 | 4 | rwx-- | liba.so |
| D2BB0000 | 4 | 4 | 4 | r-x-- | [ anon ] ld.so.1 |
| D2BBE000 | 184 | 184 | - | r-x-- | ld.so.1 |
| D2BFC000 | 8 | 8 | 8 | rwx-- | ld.so.1 |
| D2BPE000 | 4 | 4 | 4 | rwx-- | ld.so.1 |
| Total Kb | 1576 | 1224 | 92 |

在列表 2.12 所示的内存映射中，每个库至少有两个映射段。第一个段以读取和执行权限进行映射，包含库中的代码。第二个段包含数据，并以读、写、执行权限映射。尽管代码中没有包含对 `lib.so` 的任何调用，并且可能使用了该库，但库仍然被映射进来了。`RSS` 列表示 x86 处理器使用 4KB 的默认页大小，因此内存按 4KB 块分配的。尽管 `liba.so` 和 `lib.so` 仅包含几个字节的代码，但两个库都为指令分配了 4KB 的内存。数据部分也是如此。问题在于，当调用该页面中的例行程序时，每个 KB 都需要一个用于虚拟地址到物理地址映射的 TLB。如果 `lib.so` 和 `lib.so` 被合并，那么两个库中的函数可以被放在每个指令和数据共用的一个 4KB 段中。

通过设置环境变量 `LD_DEBUG=flags` 可以查看应用程序加载时的事件序列。列表 2.13 显示了输出的编辑形式。

### 列表 2.13 环境变量 LD_DEBUG=files 的输出

```
$ LD_DEBUG=files ./a.out

0165:file=/export/home/darryl/a.out [ ELF ]; generating link map
0165:file=a.out; analyzing
```

```
0165:file=lib.so; needed by a.out
0165:file=./lib.so [ ELF ]; generating link map
```

```
0165:file=libb.so; needed by a.out
0165:file=./libb.so [ ELF ]; generating link map
```

```
0165:file=libc.so; needed by a.out
0165:file=./libc.so [ ELF ]; generating link map
```

```
0165:file=./lib.so; analyzing
```

```
0165:file=./libb.so; analyzing
```

```
0165:file=/lib/libc.so; analyzing
```

```
0165: transferring control: a.out
```

这显示了启动应用程序的序列、运行时链接器的检查、以及识别出对库 `liba.so`、`libb.so` 和 `libc.so.1` 的需求。一旦加载了这些库，它就会检查是否存在可能需要的其他库。

链接器执行了大量工作。然而，在库上花费的时间可能会被从磁盘获取它们的时间所主导。库包含的数据和指令越多，从磁盘读取该库的时间就越长。可以使用延迟加载（lazy loading）来避免在实际使用库之前从磁盘加载这些库。列表 2.14 显示了启用延迟加载构建的应用程序以及运行时链接。

### 列表 2.14 将库链接到延迟加载

```
$ libmain.c
-linked to the current directory.
```

## 第 2.19 章 性能优化编码

### 列表 2.19 Linux 上的内存映射

```
$ pmap 14392
14392:      /a.out
08048000 4K r-x /home/darryl/a.out
08049000 4K r-- /home/darryl/a.out
0804a000 4K rw- /home/darryl/a.out
b7e43000 4K rw-- [ ]
b7e44000 1392K r-x-- /lib/tls/1686/cmov-libc-2.9.so
b7f5a000 4K r-- /lib/tls/1686/cmov-libc-2.9.so
b7f5a1000 8K r-- /lib/tls/1686/cmov-libc-2.9.so
b7f3a000 4K rw-- /lib/tls/1686/cmov-libc-2.9.so
b7f4a000 16K rw-- [ ]
b7f4b000 4K rw-- [ ]
b7f5b000 4K r-x-- /home/darryl/lib.so
b7f6b000 4K r-- /home/darryl/lib.so
b7f7b000 4K rw-- /home/darryl/lib.so
b7f8b000 4K r-x-- /home/darryl/lib.so
b7f9b000 4K rw-- /home/darryl/lib.so
b7fea000 4K rw-- [ ]
b7fbb000 8K rw-- [ ]
b7fbd000 4K r-x-- [ ]
b7f9e000 112K r-x-- /lib/1d-2.9.so
b7fda000 4K r-- /lib/1d-2.9.so
b7fdb000 4K rw-- /lib/1d-2.9.so
bffc6000 84K rw-- [ ]
total                                                               1684K
```

在这里，库开发者的便利性与库用户的便利性之间存在着平衡。关于如何使用库的粗略指南如下：

- 当库包含极少执行的代码时，使用库是有意义的。如果应用程序的常规使用中有大量代码不需要从磁盘加载，那么将这些功能放置在仅在需要时才加载的库中，就可以缩短应用程序的加载时间。
- 将多个应用程序通用的代码放在共享库中是很有用的，特别是当这些应用程序不受库开发者的控制时。大多数操作系统都是此类情况，使用库的应用程序会与核心操作系统分开开发。大多数应用程序使用 C 标准库 `libc`，因此将此库作为共享库提供给所有应用程序使用是有意义的。如果操作系统的内部发生变化或修复了错误，则可以修改库而无需更改使用这些库的应用程序。这是封装的一种形式。

### 结构如何影响性能

- 设备驱动程序通常被封装成库。人们往往倾向于产生多个库，其中一些是核心的，另一些是特定设备的。如果系统很可能只连接一种特定类型的设备，那么生成单个库会更好。如果可能连接多种类型的设备且它们共享同一个核心部分，那么将代码划分为设备特定和通用代码可能是合适的。
- 库还可以提供动态加载的功能。可以发布一个库来为现有应用程序提供新功能。将尽可能多的功能放在少数几个库中是最有效的方法，但在许多情况下，动态管理功能的开销可能会超过将功能封装成库带来的开销。

通常情况下，最好在需要时懒懒加载库，而不是在启动时加载所有库。这会提高应用程序的启动速度。列表 2.20 是一个懒加载的简单库代码。

```c
#include <stdio.h>

void initialise()
{
    printf("Initialisation code run\n");
}
#pragma init (initialise)
```

```c
void doStuff()
{
    printf("Doing stuff\n");
}
```

列表 2.21 显示的应用程序使用了列表 2.20 中的库。

```c
#include <stdio.h>
void doStuff()
void main()
{
    printf("Application now running\n");
    doStuff();
    printf("Application now exiting\n");
}
```

列表 2.22 显示在 Solaris 上不使用懒加载编译、链接和运行此应用程序的结果。

### 列表 2.22 不使用懒加载使用库代码

```
$ cc -o -G -o liba.so liba.c
$ cc -o -G -o liba.so liba.c
$ cc -o -G -o liba.so liba.c
```

# 第 2 章 针对性能的代码

加载指令加载到每个层级缓存的数据量取决于缓存行（cache line）的大小。正如第 1 章中“使用缓存存储最近使用的数据”中所讨论的，64 字节是缓存行的典型长度；然而，某些缓存的行比此长，而某些缓存的行更短。通常靠近处理器的缓存行较短，距离处理器越远的行越长。图 2.2 展示了当从内存取取行到缓存时会发生的情况。

![](img/9337ae7b0be66cc11725becaa009908f_75_0.png)

图 2.2 从内存将数据取到缓存
