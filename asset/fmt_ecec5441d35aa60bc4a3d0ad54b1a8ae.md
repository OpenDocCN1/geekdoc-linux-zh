
## GDB 调试会话

```
(gdb) continue
sort (a=0xa8049684, n=3) at debug4.c:20

20   /* 20 */ for(i < n && s != 0; i++) {

1: array[]@ 5 = {{data = "john", '\u000' <repeats 4091 times>, key = 2},
  data = "bill", '\u000' <repeats 4091 times>, key = 3},
  data = "alex", '\u000' <repeats 4091 times>, key = 1},
  data = "neil", '\u000' <repeats 4091 times>, key = 4},
  data = "rick", '\u000' <repeats 4091 times>, key = 5}}
```

```
Breakpoint 1, sort (a=0xa8049684, n=2) at debug4.c:20

20   /* 20 */ for(i < n && s != 0; i++) {

1: array[]@ 5 = {{data = "john", '\u000' <repeats 4091 times>, key = 2},
  data = "bill", '\u000' <repeats 4091 times>, key = 3},
  data = "alex", '\u000' <repeats 4091 times>, key = 1},
  data = "neil", '\u000' <repeats 4091 times>, key = 4},
  data = "rick", '\u000' <repeats 4091 times>, key = 5}}
```

```
array[0] = {john, 2}
array[1] = {alex, 1}
array[2] = {bill, 3}
array[3] = {neil, 4}
array[4] = {rick, 5}
```

程序以退出码 `0` 退出。`gdb` 报告程序以异常退出码退出。这是因为程序本身没有调用 `exit` 也没有从 `main` 返回值。在这种情况下，退出码是没有意义的，有效的退出码由 `exit` 调用提供。

程序似乎没有按照预期执行外层循环。我们可以看到循环使用的参数 `n` 在每个断点处都在减少。这意味着循环执行的次数不够。罪祸首是第 30 行的 `n` 递减：

```
/* 30 */
n--;
```

这是尝试利用循环结束时数组最大的元素将位于底部这一事实来优化程序。但正如我们所看到的，这干扰了外层循环并导致了问题。最简单的修复（尽管还有其他方法）是删除该行。让我们测试使用调试器应用修复是否解决问题。

## 使用调试器进行修复

我们已经看到可以使用调试器设置断点并检查变量的值。通过带有操作的断点，可以在不更改源代码和重新编译的情况下尝试修复。在这种情况下，我们需要在第 30 行中断并增加变量 `n`。当执行第 30 行时，值将保持不变。

让我们从头重新运行程序。首先，必须删除我们的断点和显示。使用 `info` 命令查看我们启用了哪些断点和显示：

```
(gdb) info display
Auto-display expressions now in effect:
Num Expression
1: y array[0] @ 5

(gdb) info break
Num Type Display
1 breakpoint keep y 0x08043d in sort debug4.c:20
already hit 4 times
```

我们可以禁用或完全删除它们。如果我们禁用它们，可以在需要时保留重新启用的选项：

```
(gdb) disable break 1
(gdb) disable display 1
(gdb) break 30
Breakpoint 2 at 0x0804862: file debug4.c, line 30.
(gdb) commands 2
```

## 调试

在命中断点 2 时输入命令，每行一个。以包含 `end` 的行结束。

```
>set variable n = n+1
>cont
>end

(gdb) run
Starting program: /home/bill/debug4.c:30
Breakpoint 2, sort (a=0x8049580, n=5) at debug4.c:30
  /* 30 */
---
Breakpoint 2, sort (a=0x8049580, n=5) at debug4.c:30
  /* 30 */
---
Breakpoint 2, sort (a=0x8049580, n=5) at debug4.c:30
  /* 30 */
---
Breakpoint 2, sort (a=0x8049580, n=5) at debug4.c:30
  /* 30 */
---

array[0] = {alex, 1}
array[1] = {john, 2}
array[2] = {bill, 3}
array[3] = {neil, 4}
array[4] = {rick, 5}
```

程序以代码 `0` 退出。

程序运行完成并打印了正确的结果。我们现在可以进行更改并继续使用更多数据进行测试。

## 更多关于 `gdb`

`GNU` 调试器是一个极其强大的工具，可以提供关于执行中程序内部状态的大量信息。在支持“硬件断点”功能的系统上，可以使用 `gdb` 实时监控变量。硬件断点是某些 `CPU` 的功能；这些处理器能够在出现特定情况时自动停止，通常是对给定区域的内存访问。或者，`gdb` 可以监视表达式。这意味着在有性能损失的情况下，`gdb` 可以在表达式取特定值时停止程序，无论该计算发生在程序的哪个位置。

断点可以带有条件设置，以便仅在固定次数后或在满足条件时触发。

# 第 10 章

稍微，当你单步执行代码时，你可能会发现自己在来回跳转以实现原始源代码所预期的效果。

你可以使用 `gdb` 来调试崩溃的程序。`Linux` 和 `UNIX` 在程序失败时通常会在一个名为 `core` 的文件中产生核心转储。这是程序内存的映像，包含了程序故障时全局变量的值。你可以使用 `gdb` 来确定程序在崩溃时所在的位置。更多信息请查阅 `gdb` 手册。

`gdb` 在 `GNU` 公共许可协议下提供，`UNIX` 系统可以支持它。我们强烈建议你了解它。

## 更多调试工具

除了 `gdb` 这种纯粹的调试器外，`Linux` 系统通常提供许多其他工具可以帮助你辅助调试过程。其中一些工具提供程序的静态信息，另一些工具则提供动态分析。

静态分析提供来自程序源代码的信息。如 `ctags`、`xref` 和 `cflow` 等程序通过源文件工作，并提供关于函数调用和位置的有用信息。

动态分析提供程序在执行期间行为的信息。如 `prof` 和 `gprof` 等程序提供关于哪些函数被执行以及执行了多久的信息。

让我们来看其中的一些工具及其输出。并不是所有这些工具在所有系统上都可用，但其中许多工具都有免费版本。

## Lint：移除程序中的冗余

原始的 `UNIX` 系统提供了一个名为 `lint` 的实用程序。它本质上是一个 `C` 编译器的前端，增加了一些测试，旨在应用某些常识并产生警告。它可以检测变量在设置之前被使用的情况，以及函数参数未赋值的情况等。

更现代的编译器可以以编译性能为代价，产生类似的工具。`Lint` 本身已被 `C` 语言的标准化取代。由于该工具用于早期的 `C` 编译器，它无法很好地处理 `ANSI` 语法。`UNIX` 有一些商业版本的 `lint` 可用，对于 `Linux` 至少有一个版本，即 `splint`。这广为人知的 `LCint` 是麻省理工学院用于产生形式化规范工具的一个项目。一个类似 `lint` 的工具 `splint` 可以提供有用的代码审查意见。可以在 `http://www.splint.org` 找到 `splint`。

以下是 `splint` 在我们调试的程序早期版本上运行的编辑输出：

```
ne@beast:~BLP3/chapter10> splint -strict debug0.c
splint 3.0.1.6 --- 27 Mar 2002
debug0.c:14:22: Old style function declaration
```

函数定义使用的是旧式语法。优选使用标准原型语法。（使用 `-oldstyle` 抑制警告）

```
debug0.c: (in function)
debug0.c:20:31: 变量 s 在定义之前被使用
一个值在某些执行路径上可能未初始化为值。（使用 -usedef 抑制警告）
debug0.c:20:23: & 的左操作数不是无符号值（布尔型）：
int n & s = 0
```
