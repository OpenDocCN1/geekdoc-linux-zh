
| `break line` | 在行号处设置断点。 |

| `break file:line` | 在行号（指定文件）处设置断点。 |

| `break address` | 在物理地址处设置断点。 |

# 584 GNU/Linux 应用程序编程

最后一种有趣的断点方法是条件断点。考虑以下命令：

```
(gdb) break operator if op = 2
Breakpoint 2 at 0x8084445: file testapp.c, line 48.
```

这告诉 GDB 当 `op` 参数等于 2 (`OP_MULTIPLY`) 时在 `operator` 处断下。如果你正在寻找某个特定条件，这非常有用，可以避免在每次调用时都停下检查变量。

# 逐行执行源码

当你离开调试会话时，你在 `main` 函数处命中了一个断点。现在是时候向前步进源码了。根据你想实现的目标，你有几种不同的选择（表 30.2 列出了这些)。要执行下一行代码，你可以使用 `step` 命令。这也会进入函数（如果该函数是下一行执行的）。如果你倾向于跳过函数，可以使用 `next` 命令，它会执行下一行，如果该行是一个函数，它只需执行该函数并将执行行设置为该运行行之后的行。`cont` 命令（`continue` 的缩写）简单地启动程序。

## 表 30.2 逐行执行源码的方法

| 命令（快捷键） | 操作 |
| --- | --- |
| `next` (`n`) | 执行下一行，跳过函数。 |
| `step` (`s`) | 执行下一行，进入函数。 |
| `cont` (`c`) | 继续执行。 |

你还可以在 `next` 和 `step` 命令后提供一个计数，这将按照参数指定的指定的次数执行该命令。例如，执行命令 `step 5` 将执行 5 次 `step` 命令。

你可以在如下所示的调试会话中看到 `next` 和 `step` 命令的执行：

```
Breakpoint 1, main () at testapp.c:79
79 initStack(&stack);
(gdb) s
initStack(stack=0xbffffde60) at testapp.c:20
20 assert( stack );
```

```
(gdb) s
21 stack->index = 0;
(gdb) s
22 }
(gdb) s
main () at testapp.c:81
81 push(&stack, 2);
(gdb) n
82 push(&stack, 5);
(gdb)
```

在最后一个调试片段中，你进入了 `initStack` 函数。GDB 让你知道你所在的位置（函数名和栈地址）。你执行了 `initStack` 的每一行，在返回后，GDB 让你知道回到了 `main` 函数。你随后使用 `next` 命令执行值为 2 的 `push` 函数。

# 检查数据

GDB 可以方便地检查运行程序中的数据。继续你的调试会话，现在是时候查看你的栈结构了。你可以通过 `display` 命令来实现：

```
(gdb) display stack
1: stack = {2, 0, 1107383313, 134513378,
1108545272, 1108544020, -1073750392, 1345132665,
1108544020, 1073792624}, index = 1
(gdb)
```

如果你显示栈变量 `stack`，你可以看到结构的聚合组件（第一个数组本身、`index` 变量）。注意，栈的许多元素是异常巨大的数字，但这仅仅是因为结构没有初始化。你也可以使用 `display` 命令检查栈变量的特定元素：

```
(gdb) display stack.index
2: stack.index = 1
(gdb)
```

# 588 GNU/Linux 编程

## 多线程应用程序调试

没有更好的说法了：调试多线程应用程序至其多是困难的。GDB 提供了一些辅助多线程调试的功能，本节将介绍这些功能。

断点是调试中最重要的方面之一，但在多线程应用程序中的行为有所不同。如果多个线程在源代码行创建一个断点，那么每个线程都会受到断点的影响。你可以通过指定受影响的线程来限制这一点。例如：

```
(gdb) break pos.c:17 thread 5
```

这在 `myfile.c` 的第 20 行设置了一个断点，但仅针对 5 号线程。你可以使用线程限定符进一步完善这些断点。例如：

```c
11 void *posThread(void *arg )
12 {
13 int ret;
14
15 ret = checkPosition(arg);
16
17 if (ret == 0) {
18
19 ret = move(arg);
20 }
21 (gdb) b pos.c:17 thread 5 if ret > 0
    Breakpoint 1 at 0x8048550: file pos.c, line 19
    (gdb)
```

在这个示例中，你指定在 `pos.c` 文件的第 17 行为 5 号线程中断，但在这里你限定了只有当局部变量 `ret` 大于 0 时，5 号线程才会停止。

你可以使用 `info threads` 命令识别多线程应用程序中当前活跃的线程。该命令列出每个活跃线程及其当前状态。例如：

```
(gdb) info threads
5 Thread -161539152 (LWP 2819) posThread(arg=0x0) at pos.c:17
...
* 1 Thread -151046720 (LWP 2808) init at init.c:154
(gdb)
```

# 第 30 章 使用 GDB 调试

线程前的 `*` 符号标识它是调试器的当前焦点。你可以使用 `thread` 命令切换到任何线程，这允许你将调试器的焦点改为指定的线程。

```
(gdb) thread 1
[Switching to thread 1 (Thread -161539152 (LWP 2819))]#0 posThread
17 if (ret == 0) {
(gdb)
```

当你单步多线程程序时，你会发现调试器的焦点可以在任何一步发生变化。这可能会很困恼，尤其是当你感兴趣的调试恰恰是当前线程时。你可以通过锁定调度器来指示 GDB 不要抢占当前线程。例如：

```
(gdb) set scheduler-locking on
```

这告诉 GDB 不要抢占当前线程。当你想要允许其他线程抢占你的当前线程时，可以将模式设置为 `off`：

```
(gdb) set scheduler-locking off
```

最后，你可以使用 `scheduler-locking` 命令识别当前模式：

```
(gdb) show scheduler-locking
Mode for locking scheduler during execution is "on".
(gdb)
```

线程调试的一个重要命令是能够将单个命令应用到应用程序中的所有线程。`thread apply all` 命令用于此目的。例如，以下命令为每个活跃线程输出堆栈回溯：

```
(gdb) thread apply all backtrack
```

`thread apply` 命令也可以应用于特定的线程列表而不是所有线程，如下所示：

```
(gdb) thread apply 1 4 9 backtrack
```

这会对线程 1、4 和 9 执行堆栈回溯。

# 调试现有进程

你可以通过将 GDB 挂载（`attach`）到进程来调试当前运行的应用程序。你只需要要调试进程的进程标识符（PID）。在这个示例中，你在一个终端启动了应用程序，然后在另一个终端启动了 GDB。当 GDB 启动后，你发出 `attach` 命令来连接该进程。这会挂起该进程，允许对其进行控制。
