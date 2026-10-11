
strated 之前。欠载（underrun）是指访问位于分配区域之前的内存。

### EF_PROTECT_FREE

将该变量设置为 1 可防止 Electric Fence 重新利用已被正确释放的内存。当你怀疑程序可能正在访问已释放的内存时，这很有帮助；如果已释放的内存随后被重新分配，那么来自先前悬空指针的访问本应无法被检测到。

### EF_ALLOW_MALLOC_0

当给定一个非零值时，Electric Fence 允许 `malloc(0)` 调用。这类调用在标准 C 中在技术上是合法的，但很可能代表一个软件 bug。因此，默认情况下，Electric Fence 禁止这些调用。

除了环境变量，Electric Fence 还提供了同名全局变量。你可以在调试器中修改它们的值，从而动态更改已经启动运行的程序的行为。详情参见 *efence(3)*。

## 15.5.2.3 调试 Malloc：dmalloc

`dmalloc` 库提供了大量的调试选项。其作者是 Gray Watson，它有自己的网站[^18]。与 Electric Fence 一样，你的系统上可能已经安装了它，或者你需要获取它并自行构建。

[^18]: http://www.dmalloc.com

`dmalloc` 库检查 `DMALLOC_OPTIONS` 环境变量以获取控制信息。例如，它可能如下所示：

```bash
$ echo $DMALLOC_OPTIONS
debug=0x4e4503,inter=100,log=dm-log
```

该变量的“debug”部分是一组“或”运算（OR’d）的位标志，对于大多数人来说直接管理几乎是不可能的。因此，文档描述了一个两阶段过程，以使其更易于使用。

第一步是定义一个名为 `dmalloc` 的 shell 函数，该函数调用 `dmalloc` 驱动程序：

```bash
$ dmalloc ()
> eval 'command_dmalloc -b $*'  # command 命令绕过 shell 函数
> )
```

完成后，你可以向该函数传递选项，以设置日志文件（-l），指定 dmalloc 应验证其内部数据结构的迭代次数（-i），以及指定调试级别或其他标签（low）：

```bash
$ dmalloc -l dm-log -i 100 low
```

与 Electric Fence 类似，dmalloc 库可以静态链接到应用程序中，也可以通过 LD_PRELOAD 动态链接。以下示例演示了后者：

```bash
$ LD_PRELOAD=libdmalloc.so.8 csh -m dmtest -b    # 开启检查运行
p = <not 30 bytes>                       # 显示正常输出
```

> **注意** 不要使用 `export LD_PRELOAD=libdmalloc.so.8`！如果这样做，你运行的每个程序（如 `ls`）都将启用 `malloc()` 检查。你的系统将很快变得无法使用。如果你意外地这样做了，可以使用 `unset LD_PRELOAD` 来恢复正常行为。

结果将写入指定的 `dm-log` 文件：

```text
$ cat dm-log
1062078174: 1: dmalloc version '4.8.1' from 'http://dmalloc.com/'
1062078174: 1: flags = 0x4e40503, logfile 'dm-log'
1062078174: 1: interval = 100, addr = 0, seen # = 0
1062078174: 1: starting time = 1062078174
1062078174: 1: free bucket count/bits: 63/6
1062078174: 1: basic-block 4096 bytes, alignment 8 bytes, heap grows up
1062078174: 1: heap: 0x804a000 to 0x804d000, size 12288 bytes (3 blocks)
1062078174: 1: heap checked 0
1062078174: 1: alloc calls: malloc 1, calloc 0, realloc 0, free 0
1062078174: 1: alloc calls: realloc 0, malloc 0, realloc 0, free 0
1062078174: 1: total memory allocated: 30 bytes (1 pmts)
1062078174: 1: max in use at one time: 30 bytes (1 pmts)
1062078174: 1: max allocated with 1 call: 30 bytes
1062078174: 1: max alloc rounding loss: 34 bytes (53%)
1062078174: 1: max memory space wasted: 3998 bytes (98%)
1062078174: 1: final user memory space: basic 0, divided 1, 4062 bytes
1062078174: 1: final admin overhead: basic 1, divided 1, 8192 bytes (66%)
1062078174: 1: final external space: 0 bytes (0 blocks)
1062078174: 1: top 10 allocations:
1062078174: 1: total-size count in-use-size count source
1062078174: 1:          30        1           30        1 ra=0x8048412
1062078174: 1:          30        1           30        1 Total of 1
1062078174: 1: dumping not-freed pointers changed since 0:
1062078174: 1: not freed: '0x804c008\sl' (30 bytes) from 'ra=0x8048412'
1062078174: 1: total-size count source
1062078174: 1: 30 1 ra=0x8048412 # Allocation is here
1062078174: 1: 30 1 # Total of 1
1062078174: 1: unknown memory: 1 pointer, 30 bytes
1062078174: 1: ending time = 1062078174, elapsed since start = 0:00:00
```

输出中包含许多统计信息，我们目前对此不感兴趣。有趣的是指示未释放内存的那一行，其中包含一个返回地址，指示分配了该内存的函数（`ra=0x8048412`）。`dmalloc` 文档解释了如何使用 GDB 获取该地址的源代码位置：

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

这很痛苦，但如果别无选择，这是可行的。然而，如果你在程序中包含 `dmal1loc.h` 头文件（在所有其他 `#include` 语句*之后*），你就可以在报告中直接获取源代码信息：

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

单独的调试功能通过使用 *tokens*——特别是 *已识别的标识符*——以及用于添加 token（功能）的 `-p` 选项或用于移除 token 的 `-m` 选项来启用或禁用。有预定义的组合，`low`、`med` 和 `high`。你可以使用 `dmal1loc -Lv` 查看这些组合的内容：

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

此时你应该对如何使用 dmalloc 及其灵活性有了感觉。对于我们的简单演示程序来说，dmalloc 有些过度，但对于更大规模的实际应用程序来说，它是无价之宝。

