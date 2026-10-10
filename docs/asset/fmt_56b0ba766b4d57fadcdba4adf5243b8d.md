
在目标被调试系统上运行 GDB Server 后，是时候在调试器系统上的 IDA Pro 中加载 `myProg` 程序了。我们允许 IDA Pro 执行分析并选择“Remote GDB Debugger”选项，如图 5-19 所示。现在我们点击 IDA Pro 菜单中的 `Debugger | Process Options`。这弹出了图 5-20 所示的对话框。`Application` 和 `Input File` 选项都设置为 `myProg` 程序所在的本地文件夹。例如，如果我们正在调试由目标应用程序加载的 DLL，则 `Application` 和 `Input File` 选项将会不同。对于 `Hostname` 选项，我们输入了目标调试器系统的 IP 地址。端口号默认为 `23946`，因此我们在目标系统的 GDB Server 上使用了相同的选项。一旦接受了这些选项，我们就点击图 5-19 所示的“播放”按钮。随后会弹出一个窗口，显示：“已经有一个进程正在被调试调试。你想附加到它吗？”我们点击“是”，允许 IDA Pro 附加到远程 GDB Server。

调试尝试成功，并在附加后暂停了执行，如图 5-21 所示。

### 图 5-19 IDA 中的远程 GDB Debugger

![](img/0add480ffb73b6bc89b65d99f7d6b37a_211_0.png)

### 图 5-20 IDA 调试选项窗口

![](img/0add480ffb73b6bc89b65d99f7d6b37a_212_0.png)

### 图 5-21 IDA Pro 调试会话

调试窗口中有几个部分。如果你熟悉其他调试器，那么这些部分看起来会很熟悉。主要且较大的部分被称为 `IDA View-RIP`，是反汇编视图。目前，我们可以看到指令指针（RIP）指向持有指令 `mov rdi, rsp` 的内存地址。调试窗口内部的大部分区域都是可滚的。反汇编窗口下方的部分被称为 `Hex View-1`，以十六进制形式转储任何所需的内存段。`Hex View-1` 的右侧是栈视图（Stack view）。它默认从栈指针（RSP）地址开始，转储当前线程栈的内存内容。栈视图上方是 `Threads`（线程）和 `Modules`（模块）部分。最后，右上角是 `General Registers`（通用寄存器）部分。该部分显示通用处理器寄存器以及额外的寄存器，包括 `FLAGS` 寄存器和段寄存器。

调试器控制通过分配的快捷键、丝带菜单图标或通过调试菜单来激活。如果我们点击“播放”允许程序继续执行，它会直接终止，因为我们没有提供任何命令行参数。在查看此程序中的 `Imports` 表时，我们看到了对已弃用 `strcpy` 函数的调用，如图 5-22 所示。然后我们使用 `Proximity Browser`（邻近浏览器）来跟踪从主函数到 `strcpy` 的路径，如图 5-23 所示。查看它时，我们可以看到对 `strcpy` 的调用，以及目标 `0x40`（或 64 字节）的缓冲区大小。接下来，我们在 `strcpy` 的调用处设置断点，通过点击地址并按下 `F2` 键，如图 5-24 所示。

| 地址 (Address) | 序号 (Ordinal) | 库 (Library) |
| :--- | :--- | :--- |
| 0000555555558058 | strcpy | GLIBC |
| 0000555555558060 | puts | GLIBC |
| 0000555555558068 | printf | GLIBC |
| 0000555555558070 | _libc_start | GLIBC |
| 0000555555558078 | exit | GLIBC |
| 0000555555558080 | __xa_finalize | GLIBC |
| 0000555555558088 | __dl_init_table | GLIBC |
| 0000555555558090 | _gmon_start | GLIBC |

### 图 5-22 弃用的 strcpy 函数

![](img/0add480ffb73b6bc89b65d99f7d6b37a_214_0.png)

### 图 5-23 邻近路径

在 `strcpy` 函数处设置断点并理解目标缓冲区的大小，让我们传递 100 字节作为参数看看是否能让程序崩溃。修改我们的 `gdbserver` 命令以包含 Python 语法：

```
(kali@kali)-Desktop
$ gdbserver --once localhost:23946 ./myProg python3 -c 'print("A" * 100)'
Process ./myProg created; pid = 8439
Listening on port 23946
```

```
; Attributes: bp-based frame
func1 near
src= word ptr -48h
dest= byte ptr -40h

push rbp
mov rbp, rsp
sub rsp, 50h
mov [rbp+src], rdi
mov rdx, [rbp+src]
lea rax, [rbp+dest]
mov rsi, rdx ; src
mov rdi, rax ; dest
call strcpy
lea rax, [rbp+dest]
mov rsi, rax
lea rdi, format ; "You entered %s"
mov eax, 0
call _printf
mov eax, 0
leave
retn
func1 endp
```

### 图 5-24 strcpy 内部断点

我们在 IDA 内部点击“播放”按钮启动连接。一旦附加，我们必须再次点击“播放”按钮继续到 `strcpy` 函数断点处。结果如图 5-25 所示。源参数已转储到 `Hex View` 部分，我们可以看到将拷贝到栈目标缓冲区的内容。在 IDA 中按 `F9` 继续执行会导致预期的崩溃，如图 5-26 所示。来自调试器的片段显示了段错误警告、结果通用寄存器部分和栈部分。

![](img/0add480ffb73b6bc89b65d99f7d6b37a_216_0.png)

图 5-25 strcpy 断点

#### 警告

`5555555551A2`: 收到 `SIGSEGV` 信号 (Segmentation fault) (exc.code b, tid 0439)

OK

#### 通用寄存器

| | | 内存 |
| :--- | :--- | :--- |
| RAX | 0000000000000000 | 0000000000000000 |
| RBX | 0000000000000000 | 0000000000000000 |
| RCX | 0000000000000000 | 0000000000000000 |
| RSI | 0005555555556012 | .data:format |
| RDI | 00007FFFF8B1670 | 00007FFFF8B1670 |
| RBP | 4114141414141414 | 4114141414141414 |
| RSP | 00007FFFF8BBDF8 | 00007FFFF8BBDF8 |
| R8 | 0000000000000EF0 | 0000000000000EF0 |
| R9 | 0000000000000070 | 0000000000000070 |

#### 栈视图

| | | 内存 |
| :--- | :--- | :--- |
| 00007FFFFFD90 | 4114141414141414 | 4114141414141414 |
| 00007FFFFFD98 | 4114141414141414 | 4114141414141414 |
| 00007FFFFFDA0 | 4114141414141414 | 4114141414141414 |
| 00007FFFFFDA8 | 4114141414141414 | 4114141414141414 |
| 00007FFFFDFB8 | 4114141414141414 | 4114141414141414 |
| 00007FFFFDFC0 | 4114141414141414 | 4114141414141414 |

UNKNOWN 00007FFFFFD90: 内存: 00007FFFFFD90 (与 RSP 同步)

### 图 25-6 使用 IDA Pro 的图形界面在本地和远程调试程序，可以大大加快你的分析速度。

### 总结

本章为你提供了使用 IDA Pro 作为逆向工程工具的基础知识。要涵盖所有功能和扩展选项，在一个章节中是不可能的。我们查看了 IDA Pro 界面、IDA 的一些常用的功能，以及如何开始远程调试。我们将在后续关于 Microsoft 的章节继续使用 IDA Pro
