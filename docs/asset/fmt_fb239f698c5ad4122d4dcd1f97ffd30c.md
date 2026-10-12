
```text
Electric Fence 2.2.0 Copyright (C) 1987-1999 Bruce Perens <bruce@perens.com>
p = <not 30 bytes>

Program received SIGSEV, Segmentation fault. SIGSEV: GDB 打印
[Switching to Thread 8192 (LWP 20201)]
0x00485b6 in main (argc=2, argv=0xffffff8a4) at ch15-badmeml.c:18
p[42] = 'a'; /* 触碰边界外 */
(gdb) run -f
现在尝试 -f

正在调试的程序已经启动。
从头开始启动？(y 或 n) Yes,真的的

Starting program: /home/arnold/progeg/code/ch15-badmeml -f
[New Thread 8192 (LWP 20204)]

Electric Fence 2.2.0 Copyright (C) 1987-1999 Bruce Perens <bruce@perens.com>
p = <not 30 bytes>

Program received SIGSEV, Segmentation fault. SIGSEV again
[Switching to Thread 8192 (LWP 20204)]
0x00485e8 in main (argc=2, argv=0xffffff8a4) at ch15-badmeml.c:21
p[0] = 'b'
```

在支持共享库和 `LD_PRELOAD` 环境变量的系统（包括 `GNU/Linux`）上，你不需要显式链接 `efence` 库。相反，使用 `ef` 脚本通过正确的设置来运行程序。

虽然我们没有详细描述这些机制，但 `GNU/Linux`（以及其他 `Unix` 系统）支持共享库，共享库是库例的特殊版本，它们被保留在单个文件中，而不是复制到每个可执行程序的二进制文件中。共享库节省了磁盘空间并可以节省系统内存，因为所有使用共享库的程序都使用该库的内存副本。

（注：原文此处存在大量重复段落，已根据要求完成翻译并保留核心逻辑）

除了环境变量外，`Electric Fence` 还提供了同名相似的全局变量。你可以在调试器内部更改它们的值，因此可以动态更改已经在运行的程序的行为。详见 `efence(3)`。

`fence(3)` 描述了可以设置的环境变量。

### `EF_PROTECT_BELOW`
将此变量设置为 1 会导致 `Electric Fence` 泄漏下溢而不是溢出。文中演示了访问分配区域之外内存的溢出情况。

### `EF_PROTECT_FREE`
将此变量设置为 1 可防止 `Electric Fence` 复用已释放的内存。当你认为程序可能访问内存时，这非常有帮助；如果释放的内存随后被重新分配，来自指针的访问将无法被检测。

### `EF_ALLOW_MALLOC_0`
当给定非零值时，`Electric Fence` 允许调用 `malloc(0)`。此类调用在标准 `C` 中是有效的，但通常代表软件错误。因此，默认情况下，`Electric Fence` 禁止此类调用。

# 第 15 章 • 调试

```bash
$ dmalloc () {

> eval command dmalloc -b *$

> 使用 'command' 命令将绕过 shell 函数

> ```
```

完成上述操作后，你可以向函数传递选项来设置日志文件（`-l`）、指定 `dmalloc` 验证其内部数据结构之前的迭代次数（`-i`），以及指定调试级别或其他标签（如 `'low'` 低级别）：

```bash
$ dmalloc -l dm-log -i 100 low
```

像 `Electric Fence` 一样，`dmalloc` 库可以被静态链接到应用程序中，也可以通过 `LD_PRELOAD` 动态链接。接面的示例演示了后者：

```bash
$ LD_PRELOAD=libdmalloc.so chi15-badmem1 -b
p = <300 bytes
```

注意：不要使用 `export LD_PRELOAD=libdmalloc.so!`！如果你总是这样做，那么你运行的每个程序都将在开启 `malloc()` 的情况下运行。如果你不小心这样做了，系统可能会变得不稳定；可以使用 `unset LD_PRELOAD` 来恢复正常行为。

结果将进入指定的 `dm-log` 文件：

```bash
$ cat dm-log
1062078174: 1: dmalloc version '4.8.1' from 'http://dmalloc.com/'
1062078174: 1: flags = 0x4e0a503, logfile = 'dm-log'
1062078174: 1: interval = 100, addr = 0, seen # = 0
1062078174: 1: starting time = 1062078174
1062078174: 1: free bucket count/bits: 63/6
1062078174: 1: basic-block size=496 bytes, allocation 8 bytes, heap grows up
1062078174: 1: heap: 0x80a4000 to 0x80d4000, size 122883 (3 blocks)
1062078174: 1: heap checked 0
1062078174: 1: alloc calls: malloc 1, call 0, realloc 0, malign 0, valloc 0
1062078174: 1: alloc calls: realloc 0, malign 0, valloc 0
1062078174: 1: total memory allocated 30 bytes (1 pnts)
1062078174: 1: max in use time: 30 bytes (1 pnts)
1062078174: 1: max alloc with 1 call: 30 bytes
1062078174: 1: max alloc round loss: 34 bytes (53%)
1062078174: 1: max memory space wasted: 3998 bytes (98%)
1062078174: 1: final user memory: basic 0, divided 1, 4062 bytes
1062078174: 1: final user overhead: basic 1, divided 1, 8192 bytes (66%)
1062078174: 1: final external space: 0 bytes (0 blocks)
1062078174: 1: top 10 allocations:
total-size in-use-size count source
1062078174: 1: 30 1 30 1 ra=0x80844412
1062078174: 1: 30 1 30 1 Total of 1
```

## 15.5 调试工具

```text
1062081714: 1: dumping not-free pointers changed since 0:
1062081714: 1: not freed: '0x804c008|s1 (30 bytes) from 'ra=0x8048412'
1062081714: 1: total-size count source
1062081714: 1: 30 ra=0x8048412 Allocation is here
1062081714: 1: 30 Total of 1
1062081714: 1: unknown memory: 1, 30 bytes
1062081714: 1: ending time = 1062081714, elapsed since start = 00:00:00
```

输出包含了许多统计信息，我们目前对这些并不感兴趣。我们感兴趣的行是指示内存未释放的那几行，其返回地址指向了分配内存的函数（`'ra=0x8048412'`）。`dmalloc` 文档解释了如何使用 `GDB` 获取该地址对应的源码位置：

```bash
$ gdb ch15-badmem1
GNU gdb 5.3
Start GDB
(gdb) x *0x8048412
Examine address 0x8048412 <main+26>
(gdb) info line *0x8048412
Get line
Line 11 of "ch15-badmem.c" starts at address 0x804808 <main+16>
and ends at 0x804818 <main+32>.
```

这种方法很痛苦，但如果你别无选择也可以可行。然而，如果你在程序中包含了 `"dmalloc.h"`，就可以直接在报告中获取源码。
