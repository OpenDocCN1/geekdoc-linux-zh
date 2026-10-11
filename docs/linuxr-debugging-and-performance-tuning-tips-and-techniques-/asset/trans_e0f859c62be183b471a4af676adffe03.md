

## 15.5.2.4 Valgrind：一款多功能工具

前一节中描述的所有工具都专注于动态内存调试，确实，对于许多程序而言，这是一个主要的问题领域。然而，动态内存问题并不是唯一的问题类型。采用 GPL 许可证的 Valgrind 程序可以捕获大量种类的问题，包括由动态内存引起的问题。

Valgrind 的手册对该程序的描述比我们要好或至少同样好，因此我们将在文中引用（并省略部分内容）。

> Valgrind 是一个用于调试和剖析 Linux-x86 可执行文件的灵活工具。该工具由核心组成，核心在软件中提供合成 x86 CPU，以及一系列“皮肤”，每一个都是一个调试或剖析工具。架构是模块化的，因此可以轻松创建新的皮肤，而不会干扰现有结构。
>
> 最实用的“皮肤”是 memcheck：memcheck 皮肤检测程序中的内存管理问题。所有内存的读取和写入都会进行检查，对 `malloc/new`/`free/delete` 的调用会被拦截。结果，memcheck 可以检测以下问题：
>
> - 使用未初始化的内存。
> - 在内存被 `free` 之后读取/写入该内存。
> - 读取/写入 `malloc` 分配的块末尾之外的区域。
> - 在堆栈上读取/写入不适当的区域。
> - 内存泄漏——即指向 `malloc` 分配块的指针永久丢失。
> - `malloc/new/new []` 与 `free/delete/delete []` 使用不匹配。
> - POSIX pthreads API 的一些误用。
>
> 这类问题通过其他方式很难找到，通常长期未被察觉，然后导致偶尔发生、难以诊断的崩溃。

其他皮肤更具专业性：

- `cachegrind` 对 CPU 中的 I1、D1 和 L2 缓存进行详细模拟，因此可以准确定位代码中缓存未命中的来源。
- **addrcheck** 皮肤与 **memcheck** 完全相同，除了一个细节：它不进行任何未初始化值检查。其他所有检查——主要是细粒度地址检查——仍然执行。缺点是，你无法捕获 **memcheck** 能发现的未初始化值错误。但优点很显著：程序运行速度大约是 **memcheck** 的两倍，并且使用的内存少得多。它仍然能发现对已释放内存、块末尾之外以及在其他无效位置的读取/写入，这些是你真想在发布前找到的 bug！
- **helgrind** 是设计用于查找多线程程序中数据竞争的调试皮肤。

最后，手册指出：

Valgrind 与 CPU、操作系统细节紧密相关，在较小程度上与编译器和基础 C 库相关。这使得使其可移植变得困难，因此我们一开始就选择集中在我们认为广泛使用的平台上：x86 上的 Linux。Valgrind 使用标准的 Unix `./configure`、`make`、`make install` 机制，我们已努力确保其在具有内核 2.2 或 2.4 以及 glibc 2.1.X、2.2.X 或 2.3.1 的机器上正常工作。这应该涵盖了绝大多数现代 Linux 安装。请注意，带有 NPTL（Native POSIX Thread Library）包的 glibc-2.3.2+ 将无法工作。我们希望能够修复此问题，但这不会容易。

如果你在不同的平台上使用 GNU/Linux，或者你使用商业 Unix 系统，那么 Valgrind 对你的帮助不大。然而，由于 x86 GNU/Linux 系统相当常见（且价格实惠），很可能你可以以适度的预算购买一台，或者至少找到一台可以借用的！此外，一旦 Valgrind 为你发现问题，无论你的程序编译后运行在*什么*平台上，问题都已被修复。因此，使用 x86 GNU/Linux 系统进行开发，使用其他商业 Unix 系统进行高端产品的部署是合理的。

虽然 Valgrind 手册可能让你期望有名为 memcheck、addrcheck 等单独的命令，但事实并非如此。相反，名为 valgrind 的驱动 shell 程序运行调试核心，通过 --skin= 选项指定适当的“皮肤”。默认皮肤是 memcheck；因此，运行普通的 valgrind 等同于 'valgrind --skin=memcheck'。（这提供了与早期仅进行内存检查的 Valgrind 版本的兼容性，并且这也最有意义，因为 memcheck 皮肤提供了最多的信息。）

Valgrind 提供了一些选项。关于完整细节，请参阅其文档。选项分为组；其中适用于核心（即适用于所有皮肤）的选项中，这些可能最有用：

| 选项 | 描述 |
| :--- | :--- |
| `--gdb-attach=no\|yes` | 启动时附带 GDB 连接到进程，用于交互式调试。默认值为 `no`。 |
| `--help` | 列出选项。 |
| `--logfile=file` | 将日志消息记录到 `file.pid`。 |
| `--num-callers=number` | 在堆栈跟踪中显示 `num` 个调用者。默认值为 `4`。 |
| `--skin=skin` | 使用名为 `skin` 的皮肤。默认值为 `memcheck`。 |
| `--trace-children=no\|yes` | 也对子进程运行跟踪。默认值为 `no`。 |
| `-v`, `--verbose` | 更加详细。这包括列出加载的库以及所有不同类型错误的计数。 |

在 memcheck 皮肤的选项中，我们认为以下这些最有用：

- `--leak-check=no\|yes`：程序结束后查找内存泄漏。默认值为 `no`。
- `--show-reachable=no\|yes`：程序结束时显示可到达的块。如果使用 `--show-reachable=yes`，Valgrind 会查找仍然有指针指向的动态分配内存。这些内存不是内存泄漏，但知道这些信息可能也有用。默认值为 `no`。

让我们看看 Valgrind 的运行效果。还记得 `ch15-badmem.c` 吗？（参见第 15.5.2.2 节“Electric Fence”，第 614 页。）`-b` 选项向通过 `malloc()` 分配的内存区域之外的内存写入。以下是 Valgrind 的报告：

```text
$ valgrind ch15-badmem1 -b
1 ==8716== Memcheck, a.k.a. Valgrind, a memory error detector for x86-linux.
2 ==8716== Copyright (C) 2002-2003, and GNU GPL'd, by Julian Seward.
3 ==8716== Using valgrind-20030725, a program supervision framework for x86-linux.
4 ==8716== Copyright (C) 2000-2003, and GNU GPL'd, by Julian Seward.
5 ==8716== Estimated CPU clock rate is 2400 MHz
6 ==8716== For more details, rerun with: -v
7 ==8716==
8 p = <not 30 bytes>
9 ==8716== Invalid write of size 1
10 ==8716== at 0x40B456: main (ch15-badmeml.c:18)
11 ==8716== by 0x42015BD3: __libc_start_main (in /lib/libc-2.2.93.so)
12 ==8716== by 0x4004368: (within /home/arolda/progex/code/ch15/ch15-badmem1)
13 ==8716== Address 0x41048405 is 12 bytes after a block of size 30 alloc'd
14 ==8716== at 0x4025488: malloc (vg_replace_malloc.c:153)
15 ==8716== by 0x4004311: main (ch15-badmeml.c:11)
16 ==8716== by 0x42015BD3: __libc_start_main (in /lib/libc-2.2.93.so)
17 ==8716== by 0x4004368: (within /home/arolda/progex/code/ch15/ch15-badmem1)
18 ==8716==
19 ==8716== ERROR SUMMARY: 1 errors from 1 contexts (suppressed: 0 from 0)
20 ==8716== malloc/free: 1 use at exit: 30 bytes in 1 blocks.
21 ==8716== malloc/free: 1 allocs, 0 frees, 30 bytes allocated.
22 ==8716== For a detailed leak analysis, rerun with: --leak-check=yes
23 ==8716== For counts of detected errors, rerun with: -v
```

（输出中的行号是添加的，以便辅助讨论。）第 8 行是程序的输出；其他行都来自 Valgrind，输出到标准错误。第 9–17 行是错误报告。它指示错误写入的字节数（第 9 行）、发生位置（第 10 行）以及堆栈跟踪。第 13–17 行描述内存是从哪里分配的。第 19–23 行提供摘要。

`ch15-badmem1` 的 `-f` 选项释放已分配的内存，然后通过悬空指针向其写入。以下是 Valgrind 对该情况的报告：

```text
$ valgrind ch15-badmem1 -f
==8719== Memcheck, a.k.a. Valgrind, a memory error detector for x86-linux.
==8719== P = <not 30 bytes>
==8719== Invalid write of size 1
==8719==    at 0x8048498: main (ch15-badmem1.c:21)
==8719==    by 0x420158D3: __libc_start_main (in /lib/i686/libc-2.2.93.so)
==8719==    by 0x4048368: (within /home/arnold/progex/code/ch15/ch15-badmem1)
==8719==    Address 0x41048024 is 0 bytes inside a block of size 30 free’d
==8719==    at 0x4025722: free (vg_replace_malloc.c:220)
==8719==    by 0x8048491: main (ch15-badmem1.c:20)
==8719==    by 0x420158D3: __libc_start_main (in /lib/i686/libc-2.2.93.so)
==8719==    by 0x4048368: (within /home/arnold/progex/code/ch15/ch15-badmem1)
```

这一次报告指示写入发生在已释放的内存上，并且对 `free()` 的调用位于 `ch15-badmem1.c` 的第 20 行。

在没有选项调用的情况下，`ch15-badmem1.c` 分配内存并使用它，但不释放它。`--leak-check=yes` 选项报告此情况：

```text
$ valgrind --leak-check=yes ch15-badmem1
1 ==8720== Memcheck, a.k.a. Valgrind, a memory error detector for x86-linux.
...
8 p = <not 30 bytes>
9 ==8720==
10 ==8720== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
11 ==8720== malloc/free: in use at exit: 30 bytes in 1 blocks.
12 ==8720== malloc/free: 1 allocs, 0 frees, 30 bytes allocated.
...
16 ==8720==
17 ==8720== 30 bytes in 1 blocks are definitely lost in loss record 1 of 1
18 ==8720==    at 0x4025488: malloc (vg_replace_malloc.c:153)
19 ==8720==    by 0x8040411: main (ch15-badmem1.c:11)
20 ==8720==    by 0x420158D3: __libc_start_main (in /lib/i686/libc-2.2.93.so)
21 ==8720==    by 0x4048368: (within /home/arnold/progex/code/ch15/ch15-badmem1)
22 ==8720==
23 ==8720== LEAK SUMMARY:
24 ==8720==    definitely lost: 30 bytes in 1 blocks.
25 ==8720==    possibly lost: 0 bytes in 0 blocks.
26 ==8720==    still reachable: 0 bytes in 0 blocks.
27 ==8720==    suppressed: 0 bytes in 0 blocks.
28 ==8720== Reachable blocks (those to which a pointer was found) are not shown.
29 ==8720== To see them, rerun with: -v-show-reachable=yes
```

第 17–29 行提供泄漏报告；泄漏的内存是在 `ch15-badmem1.c` 的第 11 行分配的。

除了提供动态内存误用的报告外，Valgrind 还可以诊断对*未初始化*内存的使用。考虑以下程序 `ch15-badmem3.c`：

