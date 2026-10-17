
```bash
$ gdb ch15-badmem1 # 启动 GDB
GNU gdb 5.3
...
(gdb) x 0x8048412 # 检查地址
0x8048412: <main+26>: 0x8910c483
(gdb) info line *(0x8048412) # 获取行信息
Line 11 of 'ch15-badmem1.c' starts at address 0x804808 <main+16>
and ends at 0x804818 <main+32>.
```

这很痛苦，但如果别无选择，这是可行的。然而，如果你在程序中包含 `dmal1loc.h` 头文件（在所有其他 `#include` 语句之后），你就可以在报告中直接获取源代码信息：

```text
...
1062080258: 1: top 10 allocations:
1062080258: 1: total-size count in-use-size count source
1062080258: 1: 30 1 30 1 ch15-badmem2.c:13
1062080258: 1: 30 1 30 1 # Total of 1
1062080258: 1: dumping not-freed pointers changed since 0:
1062080258: 1: not freed: '0x804c008\sl' (30 bytes) from 'ch15-badmem2.c:13'
1062080258: 1: total-size count source
1062080258: 1: 30 1 ch15-badmem2.c:13
1062080258: 1: 30 1 # Total of 1
...
```

（`ch15-badmem2.c` 文件与 `ch15-badmem1.c` 相同，只是它包含了 `dmal1loc.h`，所以我们没有费心展示它。）

单独的调试功能通过使用 `tokens`——特别是 `已识别的标识符`——以及用于添加 token（功能）的 `-p` 选项或用于移除 token 的 `-m` 选项来启用或禁用。有预定义的组合，`low`、`med` 和 `high`。你可以使用 `dmal1loc -Lv` 查看这些组合的内容：

```bash
$ dmalloc low # 设置为低
$ dmalloc -lv # 显示设置
```

要查看命令行选项列表，请输入：`dmalloc --usage`

```text
Debug-Flags 0x4e40503 (82052355) (low)             当前 tokens
log-stats, log-non-free, log-bad-space, log-elapsed-time, check-fence,
free-blank, error-abort, alloc-blank, catch-null
Address       not-set
Interval      100
Lock-On       not-set
Logpath       'log2'
Start-File    not-set
```

完整的 token 集合，连同简要说明和每个 token 对应的数值，可以通过 `dmalloc -DV` 获取：

```bash
$ dmalloc -DV

Debug Tokens:
none (nil) -- 无功能 (0)
log-stats (lst) -- 记录一般统计信息 (0x1)
log-non-free (inf) -- 记录未释放的指针 (0x2)
log-known (lkn) -- 仅记录已知的未释放指针 (0x4)
log-trans (ltr) -- 记录内存事务 (0x8)
log-admin (lad) -- 记录管理信息 (0x20)
log-blocks (lbl) -- 在堆映射时记录块 (0x40)
log-bad-space (lbs) -- 转储来自错误指针的空间 (0x100)
log-non-free-space (lns) -- 转储来自未释放指针的空间 (0x200)
log-elapsed-time (let) -- 记录已分配指针的经过时间 (0x400000)
log-current-time (lct) -- 记录已分配指针的当前时间 (0x800000)
check-fence (cfe) -- 检查栅栏柱错误 (0x400)
check-heap (che) -- 检查堆管理结构 (0x800)
check-lists (cli) -- 检查空闲链表 (0x1000)
check-blank (cbl) -- 检查被 alloc-blank, free-blank 覆盖的内存 (0x2000)
check-funcs (cfu) -- 检查函数 (0x4000)
force-linear (fl1) -- 强制堆空间为线性 (0x10000)
catch-signals (csi) -- 在 SIGHUP, SIGINT, SIGTERM 时关闭程序 (0x20000)
realloc-copy (rcp) -- 复制所有重新分配 (0x100000)
free-blank (fbl) -- 用 BLANK_CHAR 覆盖已释放的内存空间 (0x200000)
error-abort (eab) -- 在错误时立即中止 (0x4000000)
alloc-blank (abl) -- 用 BLANK_CHAR 覆盖新分配的内存 (0x8000000)
heap-check-map (hcm) -- 在堆检查时记录堆映射 (0x10000000)
print-messages (pme) -- 将消息写入 stderr (0x20000000)
catch-null (cmu) -- 如果没有可用内存则中止 (0x40000000)
ever-reuse (nre) -- 从不重用已释放的内存 (0x80000000)
allow-free-null (afn) -- 允许释放 NULL 指针 (0x200000000)
error-dump (edn) -- 在错误时转储核心文件然后继续 (0x40000000)
```

此时你应该对如何使用 `dmalloc` 及其灵活性有了感觉。对于我们的简单演示程序来说，`dmalloc` 有些过度，但对于更大规模的实际应用程序来说，它是无价之宝。

### 15.5.2.4 Valgrind：一款多功能工具

前一节中描述的所有工具都专注于动态内存调试，确实，对于许多程序而言，这是一个主要的问题领域。然而，动态内存问题并不是唯一的问题类型。采用 GPL 许可证的 `Valgrind` 程序可以捕获大量种类的问题，包括由动态内存引起的问题。

`Valgrind` 的手册对该程序的描述比我们要好或至少同样好，因此我们将在文中引用（并省略部分内容）。

> `Valgrind` 是一个用于调试和剖析 `Linux-x86` 可执行文件的灵活工具。该工具由核心组成，核心在软件中提供合成 `x86` CPU，以及一系列“皮肤”，每一个都是一个调试或剖析工具。架构是模块化的，因此可以轻松创建新的皮肤，而不会干扰现有结构。
>
> 最实用的“皮肤”是 `memcheck`：`memcheck` 皮肤检测程序中的内存管理问题。所有内存的读取和写入都会进行检查，对 `malloc/new`/`free/delete` 的调用会被拦截。结果，`memcheck` 可以检测以下问题：
>
> - 使用未初始化的内存。
>
> - 在内存被 `free` 之后读取/写入该内存。
>
> - 读取/写入 `malloc` 分配的块末尾之外的区域。
>
> - 在堆栈上读取/写入不适当的区域。
>
> - 内存泄漏——即指向 `malloc` 分配块的指针永久丢失。
>
> - `malloc/new/new []` 与 `free/delete/delete []` 使用不匹配。
>
> - `POSIX` `pthreads` API 的一些误用。
>
> 这类问题通过其他方式很难找到，通常长期未被察觉，然后导致偶尔发生、难以诊断的崩溃。

其他皮肤更具专业性：

- `cachegrind` 对 CPU 中的 `I1`、`D1` 和 `L2` 缓存进行详细模拟，因此可以准确定位代码中缓存未命中的来源。

- `addrcheck` 皮肤与 `memcheck` 完全相同，除了一个细节：它不进行任何未初始化值检查。其他所有检查——主要是细粒度地址检查——仍然执行。缺点是，你无法捕获 `memcheck` 能发现的未初始化值错误。但优点很显著：程序运行速度大约是 `memcheck` 的两倍，并且使用的内存少得多。它仍然能发现对已释放内存、块末尾之外以及在其他无效位置的读取/写入，这些是你真想在发布前找到的 bug！

- `helgrind` 是设计用于查找多线程程序中数据竞争的调试皮肤。

最后，手册指出：
