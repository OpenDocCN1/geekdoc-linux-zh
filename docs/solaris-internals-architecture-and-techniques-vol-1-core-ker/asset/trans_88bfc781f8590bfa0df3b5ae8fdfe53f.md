
或 ELF，当它应用于可执行文件时。ABI 还为可重定位文件和共享对象提供了 ELF 定义。

| 文件偏移量 | 文件视图 | 可执行视图 |
|---|---|--|
| 0x0000 | ELF 头部 | 头部填充 |
| | 程序头表 | 文本段 |
| | 其他信息 | 数据填充 |
| 0x00200 | 文本段 0x1ce00 字节 | 数据填充 |
| 0x1d000 | 数据段 0x4000 字节 | 未初始化数据 |
| | 其他信息 | 页面填充 |
| 0x21000 | | |

图 8.3 ELF 对象对象视图

ELF 文件的主体由各种段组成。段是 ELF 文件中可以重定位的最小不可分单元。它们分为两个大类：程序数据（文本、数据等）和链接-编辑器信息（例如，符号表信息）。可执行侧的段（segment）是相关信息的组。文件段并不一定与可执行视图的段一一一映射。正如我们很快看到的，进程的地址空间可以分成几个文本段和数据段。ELF 段由 ELF 文件的节头表（SHT）定义。ELF 文件还实现了由程序头表（PHT）定义的结构，该表在文件被执行（execd）时用于创建进程的内存映像。

有关 ELF 文件格式的信息以及定义 ELF 头部、SHT 和 PHT 表的各种数据结构的规范，请参阅作为 Solaris 文档集一部分的《Linkers and Libraries Guide》（链接器与库指南）。另请查看 /usr/include/sys/elf.h 文件以获取结构定义。此外，Solaris 自带有一个库 libelf(3E)，用于开发可以操作 ELF 文件的代码。请参阅《Linker and Libraries Guide》获取有关使用 elf(3E) 接口的信息。

图 8.4 提供了进程的概念视图。与进程相关的各种数据项（部分显示在图 8.4 中）可以通过 /usr/proc/bin 目录下的命令进行提取（参考 proc(1)）。

# 进程结构

![](img/a86367b95bf21add858c99948ac951c6_310_0.png)

图 8.4 进程概念视图

总结前面的段落：通过 ELF 文件定义和格式，内核及相关工具（编译器和链接器）创建了一个磁盘文件，该文件是一个可执行对象，可以正确加载到内存中并转换为调度和执行的进程。

所有的进程上下文（包括硬件和软件）都维护在后续章节描述的数据结构中。

## 8.2 进程结构

在本节中，我们将查看构成 Solaris 内核中多线程进程模型的主要数据结构。

### 8.2.1 进程结构

进程结构（或 proc 结构）为 Solaris 环境中进程和线程的创建与管理提供了框架。图 8.5 展示了整体情况，包含了大部分结构成员的进程结构，以及提供整个进程执行环境的所有其他组件。

## 进程结构

![](img/a86367b95bf21add858c99948ac951c6_311_0.png)

- *p_exec
- *p_ask
- *p_lockp
- *p_clock
- *p_cred
- *p_swapcnt
- *p_stat
- *p_wcode
- *p_ppid
- *p_parent
- *p_cnid
- *p_pidp
- *p_pgid
- *p_utime
- *p_stime
- *p_cutime
- *p_cstime
- *p_rkbase
- *p_bksize
- *p_sig
- *p_sigall
- *p_signdr
- *p_aslwp
- *p_lwptot
- *p_zombcnt
- *p_zblist
- *p_trace
- *p_plist
- nu_flist
- *p_aio
- *p_itimer
- *p_door_list
- *p_sc_door
- scheduling-class
- (cl_data)

图 8.5 进程结构及相关数据结构

与任何内核结构一样，proc 结构的成员涵盖了各种数据类型，包括许多指向构成 Solaris 环境全景的指针。在接下来的页面中，我们将描述主要的结构成员和相关链接。以及头文件 /usr/include/proc.h。

- p_exec — 指向进程的指针，通常称为程序的可执行形式。所有进程都源自二进制文件。当文件被执行（execd）时，内核将二进制文件加载到内存中。p_exec 指针指向 vnode，该 vnode 链接到磁盘上的文件映像。vnode 结构定义在 /usr/include/vnode.h 中。

- p_as — 地址空间指针。分配给进程的所有内存页定义了进程的虚拟地址（见图 8.6）。你可以使用 /usr/proc/bin/pmap 转储进程的地址空间映射。

| 32位 Solaris | 64位 Solaris 7 |
|---|---|---|
| 共享库 | 共享库 | |
| 堆 | 内存空间 | 预留 |
| 数据 | 已初始化数据 | 堆 |
| 文本 | 可执行代码 | 数据 |
| 0x0000000 | 文本 | 0x000000000000000 |

图 8.6 进程地址空间

以下是 /usr/proc/bin/pmap 命令（带有 -x 标志）的示例输出，它转储了构成进程虚拟地址空间的所有段。pmap(1) 显示虚拟地址（Address）、映射以 Kbytes 为单位的大小、映射中驻留在物理内存的量、多少是共享的、多少是私有的、映射的权限以及映射的文件名。注意，栈被映射为读/写/执行，以符合 SPARC V8 应用程序接口的要求。映射具有执行权限的页面存在安全隐患，因为系统可能会受到缓冲区溢出攻击，恶意代码将自己插入进程的栈中，设置程序计数器并开始执行指令。你可以在 /etc/system 中设置名为 no_exec_user 的变量，以便在 Solaris 2.6 中映射具有权限的栈页。

```
set no_exec_user = 1
```

在 Solaris 2.6 中带有权限的栈页映射。如下转储如下：

```
/usr/proc/bin/pmap -x 256
256: tp
地址 字节 共享 私有 权限 文件
0000000000000000 8 8 8 r-x mem
0000000000010000 8 8 8 rw-x mem
0000001000100010 1040 1032 1032 rw-x [ heap ]
FFFFFFFF 696 576 416 160 r-x libc.so.1
FFFFFFFF 64 64 64 rw-x libc.so.1
FFFFFFFF 112 112 112 r-x ld.so.1
FFFFFFFF 16 16 16 r-x libc_par.so.1
FFFFFFFF 8 8 8 r-x [ anon ]
FFFFFFFF 8 8 8 rw-x libbdl.so.1
FFFFFFFF 16 16 16 rw-x [ stack ]
总 字节 256 256 256 256
```

Solaris 2.5 中带有权限的栈页映射。如下转储如下：

```
/usr/proc/bin/pmap -x 2564
2564: tp
地址 字节 共享 私有 权限 文件
0000000000000000 8 8 8 r-x mem
0000000000010000 8 8 8 rw-x mem
0000001000100010 1040 1032 1032 rw-x [ heap ]
FFFFFFFF 696 576 416 160 r-x libc.so.1
FFFFFFFF 64 64 64 rw-x libc.so.1
FFFFFFFF 112 112 112 r-x ld.so.1
FFFFFFFF 16 16 16 r-x libc_par.so.1
FFFFFFFF 8 8 8 r-x [ anon ]
FFFFFFFF 8 8 8 rw-x libbdl.so.1
FFFFFFFF 16 16 16 rw-x [ stack ]
总 字节 2564 2564 2564 2564
```

这是 Solaris 7 上 64 位可执行文件的 pmap(1) 转储，参数如下：

```
set no_exec_user = 1
```

这是 Solaris 7 上 64 位可执行文件的 pmap(1) 转储，由于 64 位，SPARC V9 应用程序接口将页面定义为只读，以阻止缓冲区溢出。

```
/usr/proc/bin/pmap -x 9964
9964: tp
地址 字节 共享 私有 权限 文件
0000000000000000 8 8 8 r-x mem
0000000000010000 8 8 8 rw-x mem
0000001000100010 1040 1032 1032 rw-x [ heap ]
FFFFFFFF 696 576 416 160 r-x libc.so.1
FFFFFFFF 64 64 64 rw-x libc.so.1
FFFFFFFF 112 112 112 r-x ld.so.1
FFFFFFFF 16 16 16 r-x libc_par.so.1
FFFFFFFF 8 8 8 r-x [ anon ]
FFFFFFFF 8 8 8 rw-x libbdl.so.1
FFFFFFFF 16 16 16 rw-x [ stack ]
总 字节 2000 1864 552 1312
```

- p_lock — 锁结构指针。p_lock 是一个内核互斥锁（mutex），用于同步对进程特定字段的访问（见第 2 章，内核服务）。这种内核的内核锁粒度增加了并行性，因为并没有对整个进程表使用单一锁。相反，它是按表锁定的，允许多个内核线程并发访问不同的 proc 结构。

