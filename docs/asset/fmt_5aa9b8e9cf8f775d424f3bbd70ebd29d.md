
# Back Trace

### `time ()` at `/home/seyfarth/asm/testcopy.c:18`

```
# #1 0x00000000040dea in test (name=0x401197 "rep movsb",
copy=0x400f80 <copy_rebp>, a=0x2aaab8b6010, b=0x2aaac240010 "",
count=10 at /home/seyfarth/asm/testcopy.c:26
# #2 0x000000000400f10 in main (arc=1, arg=0x7ffffffffeb38)
at /home/seyfarth/asm/testcopy.c:47
```

### 控制台

`exe` 控制台提供了直接访问 `gdb` 的方法。它的文本窗口显示与 `gdb` 的所有通信。还有一个命令行输入框，你可以在其中发布 `gdb` 命令。按下“回车”后，它会执行该命令并在文本窗口中显示结果。我执行了“`p rip`”来打印指令指针寄存器。下一个执行的指令是 `0x400ed1`，它位于 `main` 中。

### 控制台

```
0x7fffffffeb38: 140737488350534
(gdb)
0x7ffffffff46: "home/seyfarth/asm/testcopy"
(gdb)
0x7ffffffff40: 0
(gdb)
$34 = (void (*)) 0x4000ed1 <main+50>
```

`gdb` command `p $rip`

# Ebe 设置

使用编辑（Edit）菜单下的“设置（Edit settings）会弹出一个包含许多 Ebe 可调功能的表单。这里是设置为灰色配色方案时的界面。

![](img/a81fe45f331f8cec874684a58e65cf74_248_0.png)

所有这些设置都以非常简单的格式存储在 `".ebe.ini"` 中，因此可以编辑设置对话框，这样更容易管理。

注意，有一个“语言（Language）”选项设置为“英语（English）”。Ebe 还可以阿拉伯语、中文、丹麦语、法语、德语、印地语、印尼语、日语、葡萄牙语、俄语和西班牙语，这些语言得到了良好的支持，但其中一些是直接使用 Google 翻译的结果。某些翻译可能非常滑稽！我希望这些都没有冒犯性。

# 附录 C

# 使用 gdb

`gdb` 调试器是自由软件基金会的的产品，其网站为 http://www.gnu.org。它支持包括 C、C++、FORTRAN 和汇编在内的多种语言。该调试器似乎最适合 C 和 C++，而调试来自 `yasm` 的代码并不理想。

`Gdb` 对 `yasm` 程序的源代码行跟踪得相当好。它的缺点（目前而言）是 `yasm` 没有为变量提供类型信息。它确实提供了变量的地址，这允许用户使用类型转换来充分检查变量，尽管这比汇编器提供完整的类型信息需要花费更多精力。

`gdb` 的一个救急功能是它的宏机制。可以创建透明执行类型转换的宏，使调试变得更简单。

更详细的文档可以在 http://sourceware.org/gdb/current/onlinedocs.gdb 找到。

## 准备 gdb

为了让 `gdb` 感知到源代码和变量，你的代码必须使用特殊选项编译，这些选项会在对象代码中添加调试符号信息。使用 `gcc` 或 `gpp` 时使用 `-g` 选项来启用调试支持。使用 `yasm` 时你使用 `-g`，但你必须指定一种调试格式，可以是 Linux 的 `dwarf2` 或 Microsoft Visual Studio 的 `cv8`。`dwarf2` 选项在 Linux 下提供了最完全的兼容性，而 `macho64` 是 OS X 的选择。

## 启动

启动 `gdb` 的典型方式是：
```
gdb program
```
其中 `program` 是程序链接时在 `-o` 选项中提供的名称。

## 退出

退出命令是 `quit`，可以简写为 `q`。如果你已经开始运行程序且程序仍在运行，`gdb` 会通知你程序仍在运行并询问你是否要杀死该进程。输入“y”来杀死进程并退出。

## 设置断点

你可以使用 `breakpoint` 命令设置断点，该命令可以简写为 `b`。你可以使用源代码中的标签或使用文件的行号来设置断点。

```
b main
b 17
```

## 运行

你使用 `run` 在 `gdb` 中开始执行程序，该命令可以简写为 `r`。如果你在运行程序途中，`gdb` 会在杀死进程并结束之前提示你确认。

如果你设置了断点，调试器将执行语句到断点处，并将控制权交回调试器。此时，你可以检查寄存器、检查内存、逐行执行代码，或执行任何 `gdb` 命令。如果你没有设置断点，程序将运行到完成或直到发生故障。这有时是学习段错误（segmentation faults）等问题的方便方法。

在调试期间，你有几种继续执行的选项。第一个选项是继续执行直到完成或到达另一个断点。这是通过 `continue` 命令完成的，该命令可以简写为 `c`。

另一种可能性是“单步”执行程序。这里有 4 种选项。首先，你可以执行一条源语句或一条机器指令。在 C/C++ 中，你可能不倾向于一次执行一条机器指令。你还可以在同一个函数内部调试，或者在调用其他函数时步入这些函数。在同一个函数中的单步执行通过 `next` 或 `nextinstruction` 完成。对于汇编代码，这两条指令的作用相同。它们可以简写为 `n` 和 `ni`。如果你使用 `next`，调试器将执行所有函数调用，而不会返回调试器，直到从函数中返回。

另一种选择是使用 `step` 或 `stepinstruction` 命令。这些命令执行一条源语句或一条机器指令，并允许在调用的函数内部调试。它们可以简写为 `s` 和 `si`。这两条命令在汇编代码中的效果相同。如果你自己写函数，你可能更倾向于使用 `step` 来调试你调用的函数。然而，你可能希望使用 `next` 来“跳过”像 `printf` 这样的函数调用。

## 打印栈帧追踪

程序在执行过程中崩溃是很常见的。以下是一个相当典型的情况。

```
seyfarth@ux:~/teaching/asm$
./testcopy
Segmentation fault
```

段错误（segmentation fault）通常是编码中的错误，你的程序试图访问它没有映射的内存。这可能是由于越过了数组边界引起的。这里是使用 `gdb` 运行的一个示例：

```
(gdb) run
Starting program: home/seyfarth/asm/testcopy
Received signal SIGSEGV, Segmentation fault.
copy_rep () at copy.asm:12
(gdb) bt
#0 copy_rep () at copy.asm:12
#1 0x0000000000405d in main (argc=value, argv=optimized) testcopy:27
```

再次获得段错误，但立即看到程序在 `copy.asm` 的第 12 行死亡。`bt` 命令（backtrace）回溯栈帧报告 `copy_rep` 是由 `test` 函数调用的。使用 `-g` 重新编译后得到了更多结果：

```
(gdb) run
Starting program: home/seyfarth/asm/testcopy
Received signal SIGSEGV, Segmentation fault.
copy_rep () at copy.asm:12
(gdb) bt
#0 copy_rep () at copy.asm:12
#1 0x0000000000405d in main (argc=value, argv=optimized) testcopy:45
```

此时，可以打印 `copy.asm` 中的变量值。我们还可以使用 `up` 命令移动栈帧到上一个函数。

```
(gdb) up
#1 0x0000000000406d8 in test (name=0x4b7d "rep movsb", copy=0x400930, a=0x7fffed210, count=100) b=0x7fff75310) testcopy:27
$1 = (unsigned char *) 0x7ffffed210 ""
```

现在正在调试 `test` 函数。`copy` 的第三个参数是 `1000000`。通常你可以从栈追踪中获得大量信息。

## 检查寄存器

你可以在 `gdb` 中使用 `info registers` 来打印寄存器。这可以简写为 `i r`：

```
(gdb) i r
rax             0x0 0
rbx             0x64 100 0x891690 894208
rcx             0x00000000
rdx             0x989680 100001407373415334
rsi             0x7ffff7ab000
rdi             0x7ffff7ca000 14073735396416
```
