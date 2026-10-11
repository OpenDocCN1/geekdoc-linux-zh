
### 10.2.6 为系统调用添加代码

`include/asm/unistd.h` 将系统调用与 `sys_call_table` 关联。该文件中包含协助用户程序（用 C 编写）加载寄存器的宏程序。以下是 `unistd.h` 中插入系统调用的更改：

```c
include/asm/unistd.h

1: /*
2:  此文件包含系统调用号。
3:  */

5:  #define NR_restart_syscall 0
6:  #define NR_exit            1
7:  #define NR_fork            2

9:  #define NR_utimes          271
10: #define NR_fadvise64_64    272
11: #define NR_server         273
12: #define NR_ourcall         274

14: /* #define NR_syscalls 274 这是插入系统调用之前的值 */
15: #define NR_syscalls       275
```

异常处理程序 `0x80` 索引 `sys_call_table`。表中的位置决定了系统调用号，我们必须将函数名添加到列表末尾。表的代码如下：

```asm
arch386/kernel/entry.S
    .data
608: ENTRY(sys_call_table)
    .long sys_restart_syscall /* 0 - 用于重启*/
    .long sys_tgkill      /* 270 */
    .long sys_utimes
    .long sys_fadvise64_64
    .long sys_ni_syscall  /* 我们的 sys_server */
    .long sys_ourcall     /* 我们的系统调用将是 274 */
884:  nr_syscalls=(-sys_call_table)/4
```

`kernel/sys.c` 包含了实现。我们可以修改 Makefile 来包含我们的函数，但更简单的方法是在 `kernel/sys.c` 中包含源码：

```c
kernel/sys.c
1: asmlinkage long sys_our(long num)
{
2:     printf("Inside syscall num=%d\n", num);
3:     return(1);
4: }
```

最后，我们想要创建一个用户程序来测试新的系统调用。正如在本节之前提到的，一组宏可以帮助内核开发人员将 C 代码中的参数加载到 x86 寄存器中。

在 `/usr/include/asm/unistd.h` 中，有七个宏 `_syscallx(type, name,..)`，其中 `x` 是参数数量。每个宏都专门用于加载 0 到 5 个正确数量的参数，`syscall6(...)` 则允许传递更多参数的指针。下面的示例程序接受参数。对于此示例（第 5 行），我们使用了 `/unistd.h` 中的 `_syscall1(type, name,1)` 宏，它将解析为带有正确参数的 `int 0x80` 调用：

```c
mytest.c
1: #include <stdio.h>
2: #include <stdlib.h>
3: #include "/usr/include/asm/unistd.h"
4:
5: _syscall(long, ourcall, long, num);
6:
7: main()
8:
9: printf("your syscall --> num in=5, num out = %d\n", ourcall(5));
10: }
```

## 10.3 构建与调试

将你的代码添加到内核通常涉及编程和修复 Bug 的循环。在本节中，我们将描述如何调试你编写的内核代码以及如何构建调试相关的工具。

### 10.3.1 调试设备驱动程序

在之前的章节中，我们使用 `/proc` 文件系统来收集内核信息。我们也可以通过 `/proc` 让用户访问我们设备驱动程序的信息，这是调试设备驱动部分的极佳方法。`/proc` 文件系统中的每个节点在被读取或写入时都会连接到内核。在 2.6 内核中，对内核部分（包括设备）的大多数写入是通过 `sysfs` 而不是 `/proc` 完成的。这些操作在内核运行时修改特定的内核对象属性。`/proc` 仍然是一个对于属性值对需要更多数据的只读操作的工具，本节将处理从 `/proc` 条目读取的内容。

允许读取你的设备权限的第一步是在 `/proc` 文件系统中创建一个条目，这通过 `create_proc_read_entry()` 实现：

## 总结

```c
include/linux/proc_fs.h
146 static inline struct proc_dir_entry *create_proc_read_entry(const char
*name,
147 mode_t mode, struct proc_dir_entry *base,
148 read_proc_t *read_proc, void *data)
```

`*name` 是出现在 `/proc` 中的节点条目，模式为 `0` 允许文件对世界可读。如果你为单个驱动程序创建许多不同的 proc 文件，先使用 `proc_mkdir()` 创建一个 proc 目录，然后在 `*base` 下创建每个文件可能会很有优势。`*base` 是在 `/proc` 下放置文件的目录路径；值为 `NULL` 则将文件直接存放在 `/proc` 中。`*read_proc` 函数在文件被读取时被调用，`*data` 是传回 `*read_proc` 的指针：

```c
include/linux/proc_fs.h
44 typedef int (read_proc_t) (char *page, char **start, off_t off,
45 int count, int *eof, void *data);
```
