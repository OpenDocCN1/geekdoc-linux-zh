
这是一种常见的编程错误。从这里，我们可以选择使用 backtrace 命令来查看导致此错误的调用链，这可能会将我们带回错误的真正源头。列表 13-2 显示了这些结果。

## 列表 13-2
### 回溯命令

```
(gdb) bt
#0  0x00012ac4 in ClearBlock (RealBigBlockPtr=0x0, l=100000000) at led.c:43
#1  0x00012b08 in InitBlock (ptr=0x0, n=100000000) at led.c:48
#2  0x00012b50 in ErrorInHandler (wp=0x325c8, urlPrefix=0x2f648 "/Error",
    webDir=0x2f660 "", arg=0, url=0x34f30 "/Error", path=0x34d68 "/Error",
    query=0x3212d8 "") at led.c:61
#3  0x000126cc in webIOEventHandler (wp=0x325c8) at handler.c:273
#4  0x00014518 in webSetInput (wp=0x325c8, ptext=0xbefffc40,
    pnbtegs=0xbefff6c38) at webs.c:664
#5  0x0001ed00 in websReadEvent (wp=0x325c8) at webs.c:362
#6  0x0001ed34 in webSocketEvent (sid=1, mask=2, ipp=206280) at webs.c:319
#7  0x00019740 in socketDoEvent (sp=0x34fc8) at sockGen.c:903
#8  0x00019598 in socketProcess (sid=1) at sockGen.c:845
#9  0x00012be8 in main (argc=2, argv=0xbeffee14) at main.c:99
(gdb)
```

回溯显示了从用户的程序入口 `main()` 开始的完整调用链。回溯的每一行前面都有一个栈帧编号。你可以使用 gdb 的 frame 命令切换到任意指定的栈帧。列表 13-3 就是一个示例。在这里，我们切换到栈帧 2 并显示该帧中的源代码。与之前的示例一样，以 `(gdb)` 开头的行是我们向 GDB 发出的命令，而其他行则是 GDB 的输出。

## 列表 13-3
### 在 GDB 中移动栈帧

```
(gdb) frame 2
#2  0x00012b50 in ErrorInHandler (wp=0x325c8, urlPrefix=0x2f648 "/Error",
    webDir=0x2f660 "", arg=0, url=0x34f30 "/Error", path=0x34d68 "/Error",
    query=0x3212d8 "") at led.c:61
    return InitBlock(p, size);
61      return InitBlock(p, size);
(gdb) l
56
57
58            size = 10000 * sizeof(BigBlock);
59            p = malloc(size);
60            if (p) */
61 return InitBlock(p, size);
62 /* else return (0); */
63 }
64
65
(gdb)
```

你可以看到，借助通过 list 命令获取的源代码的帮助，追踪代码回到错误空指针的来源并不会困难。事实上，精明的读者会注意到我们为这个示例制造的段错误的根源。从列表 13-3 中，我们看到对 `malloc()` 调用返回值的检查已被注释掉。在这个示例中，`malloc()` 调用失败了，导致在调用链中两个栈帧之后对空指针进行操作。尽管这个示例既人为设计又微不足道，但使用 GDB 和核心转储采用类似方法追踪此类崩溃通常非常轻松。你还可以通过查看函数调用中的参数值来看到空指针。这通常会直接将你带到空指针产生的帧。

### 13.1.3 GDB 调试会话

我们通过展示一个典型的调试会话来结束对 GDB 的介绍。在之前演示程序崩溃时，我们可以选择逐步执行代码以缩小故障原因的范围。当然，如果你获取了核心转储，你应该总是从那里开始。然而，在其他情况下，你可能希望设置断点并逐步执行正在运行的代码。列表 13-4 详细说明了如何启动 GDB 以准备调试会话。请注意，程序必须在使用 gcc 命令行时启用调试标志进行编译，GDB 在此上下文中才实用。回顾第 12 章“嵌入式开发环境”中的图 12-1；这是一个交叉调试会话，GDB 在你的开发主机上运行，调试在你的目标板上运行的程序。我们在第 15 章“调试嵌入式 Linux 应用程序”中介绍了远程应用调试的完整细节。

## 列表 13-4
### 启动 GDB 调试会话

```
$ xscale_de-gdb --silent webs
(gdb) target remote 192.168.1.21:2001
0x40000790 in ?? ()
(gdb) b main
Breakpoint 1 at 0x12b74: file main.c, line 78.
(gdb) c
Continuing.

Breakpoint 1, main (argc=1, argv=0x8effee04) at main.c:78
78                hopen(NULL, (60 * 1024), B_USE_MALLOC);
(gdb) b ErrorHandler
Breakpoint 2 at 0x12b30: file led.c, line 57.
(gdb) c
Continuing.

Breakpoint 2, ErrorHandler (wp=0x311e0, urlPrefix=0x2f48 "//Error",
webDirs=0x2f560 "", arg=0, url=0x31e88 "/Error", path=0x31918 "/Error",
query=0x311ae8 "") at led.c:57
57                size = 10000 * sizeof(BigBlock);
(gdb) next
59        p = malloc(size);
(gdb) next
61                return InitBlock(p, size);
(gdb) p p
$1 =(unsigned char *) 0x0
(gdb) p size
$2 =  100000000
(gdb)
```

通过这个简单的调试会话，首先我们使用 gdb target 命令连接到我们的目标板。我们在第 15 章中更详细地介绍了远程调试。当我们连接到目标硬件时，我们使用 gdb break（简写为 b）命令在 `main()` 处设置断点。然后我们发出 gdb continue（简写为 c）命令以恢复程序的执行。如果我们有任何程序参数，可以在调用 GDB 时在命令行上发出它们。

我们命中了设置在 `main()` 处的断点，并在 `ErrorHandler()` 处设置了另一个断点，随后再次发出简写的 continue 命令。当命中这个新断点时，我们开始使用 next 命令逐步执行代码。在那里我们遇到了对 `malloc()` 的调用。在跟随 `malloc()` 调用之后，我们检查返回值，并发现如空返回值所示的失败。最后，我们打印 `malloc()` 调用中参数的值，看到正在请求一个非常大的内存区域（1 亿字节），导致失败。

虽然微不足道，但本节中的 GDB 示例应该能够使初学者立即熟练使用 GDB。我们很少有人真正精通 GDB——它非常复杂，具有许多功能。在第 13.2 节“数据显示调试器”中，我们介绍了一个 GDB 图形前端，可以帮助不熟悉 GDB 的人轻松过渡。

关于 GDB 的最后一点说明：毫无疑问，你已注意到 GDB 在首次调用时在控制台上显示的许多横幅行，如列表 13-1 所示。在这些示例中，正如前面所述，我们使用了来自 Monta Vista 嵌入式 Linux 发行版的交叉 gdb。横幅行包含嵌入式开发者必须了解的重要信息：GDB 的主机和目标规范。从列表 13-1 中，当我们调用 GDB 时看到以下输出：

```
This GDB was configured as "--host=i686-pc-linux-gnu \
--target=arm5teb-montavista-linuxaueI"
```

在此实例中，我们调用的 GDB 版本是编译为在 Linux PC 上执行的——具体来说，是运行 GNU/Linux 操作系统的 i686 处理器。同样关键的是，这个 GDB 实例是编译用于调试由 arm5teb 大端工具链生成的 ARM 二进制代码的。

嵌入式开发新手最常犯的错误之一是在尝试调试目标可执行文件时使用了错误的 GDB。如果某些事情不对劲，你应该立即检查你的 GDB 配置，以确保它适合你的环境。你不能使用本地 GDB 来调试目标代码！

## 13.2 数据显示调试器

数据显示调试器（DDD）是 GDB 和其他命令行调试器的图形前端。除了简单地查看源代码和逐步执行调试会话外，DDD 还有许多高级功能。图 13-1 是 DDD 主屏幕的截图。

![](img/7a1144833e62564667e7dd9eb4c9f03d_349_0.png)

### 图 13-1
数据显示调试器

DDD 的调用方式如下：

$ ddd --debugger xscale_be-gdg webs

如果没有 `--debugger` 标志，DDD 将尝试在你的开发主机上调用本地 GDB，这不是你在计划调试目标系统上的应用程序时想要的。DDD 命令行中的第二个参数是你要调试的程序。有关更多细节，请参阅 DDD 的手册页。

使用如图 13-1 所示的命令工具，你可以逐步执行程序。你可以以图形方式或通过 DDD 屏幕底部的 GDB 控制台窗口设置断点。对于目标调试，你必须首先使用 target 命令将你的调试器连接到目标系统，如我们在列表 13-4 中所做的那样。此命令在 ddd 主屏幕的 GDB 窗口中发出。

