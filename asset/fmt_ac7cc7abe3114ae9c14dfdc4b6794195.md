
`$ cc -o fence fence.c -lefence`

`$ ./fence`

```
Electric Fence 2.2.0 Copyright (C) 1987-1999 Bruce Perens <bruce@perens.com>
Segmentation fault
```

## 第10章

使用调试器运行可以确定问题所在：

```
$ cc -g -o efence efence.c -lefence

$ gdb efence

(gdb) run
```

Starting program: `/home/neil/nil/BLP3/chapter10/efence`
[Thread 1024 (LWP 1869)]

Electric Fence 2.2.0 Copyright (C) 1987-1999 Bruce Perens <bruce@perens.com>

程序收到信号`SIGSEGV`，Segmentation fault。
[Thread 1024 (LWP 1869)]
0x080484ad in main () at efence.c:10
`ptr[1024] = 0;`
(gdb)

## 工作原理

`ElectricFence`将`malloc`和相关函数替换为这些版本，利用计算机处理器的虚拟内存功能来防止非法内存访问。当发生此类访问时，系统会触发段错误信号并停止程序运行。

## valgrind

`valgrind`是一个能够检测我们讨论过的许多问题的工具。特别是，它可以检测访问错误和内存泄漏。你的 Linux 发行版可能没有包含它，但可以在`http://developer.kde.org/~seawardj`找到它。

使用`valgrind`甚至不需要重新编译程序，你甚至可以调试运行中程序的内存访问。它非常值得一看；它已用于包括`KDE`版本 3 在内的重大开发项目。

## 尝试一下——valgrind

这里有一个程序`checker.c`，它分配了一些内存，读取了超出内存限制的位置，在内存末尾之后写入了内容，然后使其不可访问。

```c
#include <stdio.h>

#include <stdlib.h>

int main() {

    char *ptr = (char *) malloc(1024);

    char ch;

    /* 未初始化的读取 */

    ch = ptr[1024];

    /* 越界写入 */

    ptr[1024] = 0;

}
```

## 调试

```c
/* 孤儿块 */

ptr = 0;

exit(0);
```

要使用`valgrind`，我们必须运行`valgrind`命令并传递我们想要检查的选项，随后是程序及其参数（如果有的话）。

当我们运行`valgrind`时，我们发现了许多标识的问题：

```
$ valgrind --leak-check=yes -v ./checker

==3436== valgrind-1.0.4, a memory error detected x86 GNU/Linux.

==3436== Copyright (C) 2000-2002, and GNU GPLv2, by Julian Seward.

==3436== Estimated VDW clock rate is 452 MHz

==3436== For more details, rerun with: -

==3436==

==3436== Invalid read of size 1

==3436== at 0x8048397: main (checker.c:10)

==3436== by 0x025274F2: __libc_start_main (in /lib/libc.so.6)

==3436== by 0x80482D1: exit@GLIBC_2.0 (in /home/neil/BLP3/chapter10/checker)

==3436== Address 0x42AD1424 is 0 bytes after a block of size 1024 alloc'd

==3436== at 0x0003CA75: malloc (vg_clientfuncs.c:100)

==3436== by 0x8048389: main (checker.c:6)

==3436== by 0x025274F2: __libc_start_main (in /lib/libc.so.6)

==3436== by 0x80482D1: exit@GLIBC_2.0 (in /home/neil/BLP3/chapter10/checker)

==3436== Invalid read of size 1

==3436== at 0x80483A4: main (checker.c:13)

==3436== by 0x025274F2: __libc_start_main (in /lib/libc.so.6)

==3436== by 0x80482D1: exit@GLIBC_2.0 (in /home/neil/BLP3/chapter10/checker)

==3436== Address 0x42AD1424 is 0 bytes after a block of size 1024 alloc'd

==3436== at 0x0003CA75: malloc (vg_clientfuncs.c:100)

==3436== by 0x8048389: main (checker.c:6)

==3436== by 0x025274F2: __libc_start_main (in /lib/libc.so.6)

==3436== by 0x80482D1: exit@GLIBC_2.0 (in /home/neil/BLP3/chapter10/checker)

==3436== ERROR SUMMARY: 2 errors from 2 contexts (suppressed: 0)

==3436== malloc/free: in use of: 1024 bytes in blocks.

==3436== malloc/free: 1 allocs, 0 frees, 1024 bytes allocated.

==3436== counts of detected errors, rerun with: -v

==3436== checked 34628 traces, 1 not-free blocks.

==3436== definitely lost: 1024 bytes in blocks.

==3436== possibly lost: 0 bytes in blocks.

==3436== still reachable: 0 bytes in blocks.

==3436== 1024 bytes in blocks are definitely lost in record 1 of

==3436== at 0x0003CA75: malloc (vg_clientfuncs.c:100)

==3436== by 0x8048389: main (checker.c:6)

==3436== by 0x025274F2: __libc_start_main (in /lib/libc.so.6)

==3436== by 0x80482D1: exit@GLIBC_2.0 (in /home/neil/BLP3/chapter10/checker)

-

==3436== LEAK SUMMARY:

==3436== definitely lost: 1024 bytes in 1 blocks.

==3436== possibly lost: 0 bytes in blocks.

==3436== still reachable: 0 bytes in blocks.

==3436== Reachable blocks (those to which a pointer was found) are not shown.

==3436== To see them, rerun with: --show-reachable=yes
```
