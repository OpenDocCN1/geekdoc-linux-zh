
```text
1062080258: 1: top 10 allocations
1062080258: 1: total-size in-use-size count
1062080258: 1: 30 1 30 1 ch15-badmem2.c
1062080258: 1: 30 1 Total of 1
1062080258: 1: dumping not-free pointers changed since 0:
1062080258: 1: not freed: '0x804c008|s1 (30 bytes) from 'ch15-badmem2.c:13'
1062080258: 1: total-size count
1062080258: 1: 30 1 ch15-badmem2.c
1062080258: 1: 30 1 Total of 1
```

`ch15-badmem2.c` 文件与 `ch15-badmem1` 相同，在于包含了 "dmalloc.h"，所以我们没有费精力去做它。

单个调试功能通过使用令牌来启用或禁用——具体使用 `-p` 选项添加令牌或使用 `-m` 选项移除。预定义的组合有 `'low'`、`'med'` 和 `'high'`。你可以通过 `dmalloc -` 查看这些组合：

```bash
$ dmalloc low
$ dmalloc -Lv
```

调试 malloc 工具：http://dmalloc.com/

命令行选项列表输入：`dmalloc --usage`

调试标志 `0x4e0a503` (`0x052355`) (`low`) 当前令牌 `log-stats`, `log-non-free`, `log-bad-space`, `log-elapsed-time`, `check-fence`, `free-blank`, `error-abort`, `alloc-blank`, `catch-null` Address not-set Interval 100 Lock-On not-set Logpath `'dm-log'` Start-File not-set

完整的令牌集以及简要说明和每个令牌对应的数值可以通过 `dmalloc -DV` 获取：

```bash
$ dmalloc -DV
Debug Tokens:
- none (nil) -- 功能 (0)
- log-stats (list) -- 通用统计 (0x1)
- log-non-free (inf) -- 未释放指针 (0x2)
- log-known (lkn) -- 已知的未释放指针 (0x4)
- log-trans (ltr) -- 内存事务 (0x8)
- log-admin (lad) -- 管理信息 (0x20)
- log-blocks (lbl) -- 堆映射时的块 (0x40)
- log-bad-space (lbs) -- 坏指针空间 (0x100)
- log-non-free (ins) -- 未释放指针空间 (0x200)
- log-elapsed-time (let) -- 分配指针的经过时间 (0x400)
- log-current-time (lct) -- 分配指针的当前时间 (0x800)
- check-fence (scf) -- 源点错误 (0x100)
- check-head (che) -- 头管理结构 (0x200)
- check-lists (cli) -- 空闲列表 (0x1000)
- check-blank (clbl) -- 被 alloc-blank, free-blank 覆盖的内存 (0x2000)
- check-funcs (cfu) -- 函数 (0x4000)
- force-linear (fli) -- 强制空间线性化 (0x10000)
- catch-signals (csgi) -- 在 SIGHUP, SIGINT, SIGTERM 时关闭进程 (0x20000)
- realoc-copy (rco) -- 拷贝所有重新分配 (0x10000)
- free-blank (fbl) -- 用 BLANK_CHAR 覆盖内存空间 (0x200000)
- error-abort (ear) -- 错误立即中止 (0x400000)
- alloc-blank (abl) -- 用 BLANK_CHAR 检查分配 (0x800000)
- heap-check (hcm) -- 记录堆映射 (0x1000000)
- print-messages (pm) -- 将消息写入 stderr (0x2000000)
```

到此时，你应该对如何使用 `dmalloc` 及其灵活性有了直。。`dmalloc` 对于我们的演示程序来说大材小用，但对于更大规模的现实应用来说是无价之宝。

## 15.5.2 Valgrind: 一个多功能工具

上一节描述的工具都集中于动态内存调试，确实，这是一个重点领域。然而，动态内存问题并不是唯一的类型。GPL `Valgrind` 程序可以捕获大量问题，包括来自动态内存的问题。

`Valgrind` 手册对该程序的描述比我们写的更好，因此我们在介绍时会进行引用并缩写。

`Valgrind` 由一个核心组成，核心在软件中提供了一个合成的 `x86` CPU，以及一系列“皮肤”，每个皮肤都是一个调试或性能分析工具。

# 第 15 章 • 调试

- `addrcheck` 与 `memcheck` 完全相同，唯一区别在于它不进行任何对未初始化值的检查。所有其他检查（主要是细粒度的地址检查）仍然会被。此的缺点是，你无法捕获 `memcheck` 能发现的未初始化值错误。

- 但优点是显著的：程序的运行速度大约是 `memcheck` 的两倍，且占用的内存要少得多。它仍然能发现对已释放内存的读/写、越界块的访问以及其他无效位置的访问，这些都是你在发布版本前真正想要找到的 bug！

- `helgrind` 是一个旨在发现多线程程序中数据竞态（data races）的调试外壳。

最后，手册提到：

`Valgrind` 与 CPU 细节、操作系统以及在较小程度上与编译器和基础 C 库紧密相关。这使得它变得难以移植，因此我们从一开始就选择集中在我们认为被广泛使用的平台上：`x86` 上的 `Linux`。`Valgrind` 使用标准的 `./configure`、`make`、`make install` 机制，我们尝试确保它能在内核为 2.2 或 2.4 或 `glibc` 为 2.1.X、2.2.X 或 2.3.1 的机器上运行。这应该涵盖绝大多数现代 `Linux` 安装。请注意，带有 `NPTL`（原生 POSIX 线程库）包的 `glibc-2.3.2+` 将无法工作。我们希望能够这个问题，但目前还没有。

如果你在不同的平台上使用 `GNU/Linux`，或者你正在使用商业 Unix 系统，那么 `Valgrind` 对你可能没有太大帮助。然而，由于 `x86` `GNU/Linux` 系统非常常见（且负担得起），你可能可以用适中的预算获得一个，或者至少可以借用一个！此外，一旦 `Valgrind` 为你发现了一个问题，无论你的程序编译到在*哪个*平台运行，该问题都被修复了。因此，使用 `x86` `GNU/Linux` 系统进行开发，并使用其他商业 Unix 系统部署高端产品是合理的.¹¹⁹

¹⁹ `GNU/Linux` 越来越多地被用于高端产品的部署！

## 15.5 调试工具

尽管 `Valgrind` 手册可能会让你误认为存在名为 `memcheck`、`addrcheck` 等的独立命令，但事实并非如此。一个名为 `valgrind` 的驱动壳程序运行调试核心，并根据 `--skin` 选项指定相应的“外壳”。默认外壳是 `memcheck`；因此，运行普通的 `valgrind` 等同于运行 `valgrind --skin=memcheck。（这提供了与只进行内存检查的早期版本 Valgrind 的兼容性，而且这也是合理的，因为 memcheck 外壳提供了最多的信息。）

`Valgrind` 提供了许多选项。请参阅其文档获取完整细节。选项分为几组；在适用于核心（即适用于所有外壳）的选项中，这些可能有用：

```
--gdb-attach=no|yes
```

启动时附加 `GDB` 到进程，进行交互式调试。默认为 `no`。

```
--help
```

列出选项：

```
--logfile=file
```

将日志信息到 `file.pid`。

```
--num-callers=number
```

在堆栈跟踪中显示 `num` 个调用者。默认是 4。

```
--skin=skin
```

使用名为 `skin` 的外壳。默认是 `memcheck`。

```
--trace-children=no|yes
```

同样在子进程上运行跟踪。默认为 `no`。

```
-v. --verbose
```

更详细输出。这包括列出加载的库以及所有不同类型错误的计数。

在 `memcheck` 外壳的选项中，我们认为这些是最有用的：

```
--leak-check=no|yes
```

程序结束后查找内存泄漏。默认是 ‘no’。

```
--show-reachable=no|yes
```
