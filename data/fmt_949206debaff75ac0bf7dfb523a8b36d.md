
如果你的程序运行正常，当程序运行时，你将在屏幕上看到以下十六进制字节：

67 6E 69 72 74 73 20 65 63 72 75 6F 73 20 65 68
74 20 73 69 20 73 69 68 54

（`DumpMem` 过程在第 5 章第 5.3.2 节解释。）

# 过程

- 5.1 引言
- 5.2 链接到外部库
- 5.2.1 背景信息
- 5.2.2 节复习
- 5.3 库
- 5.3.1 概述
- 5.3.2 逐一描述
- 5.3.3 程序
- 5.3.4 节复习
- 5.4 栈操作
- 5.4.1 运行时栈
- 5.4.2 PUSH 和 POP
- 5.4.3 节复习
- 5.5 定义和使用过程
- 5.5.1 PROC 指令
- 5.5.2 CALL 和 RET
- 5.5.3 示例：数组求和
- 5.5.4 流程图
- 5.5.5 保存和恢复寄存器
- 5.5.6 节复习
- 5.6 使用过程
- 5.6.1 程序（设计）
- 5.6.2 节复习
- 5.7 总结
- 5.8 编程练习

## 5.1 引言

有几个很好的理由说明你应该读这一章：

- 你需要学习汇编语言中的输入输出。
- 你需要了解运行时栈，它是实现调用和返回函数（我们称为过程）的基础机制。
- 你的程序将增长到需要逻辑上将其划分为过程的程度。
- 你需要学习如何绘制流程图，它是描绘逻辑的工具。
- 你的教授可能会对这一章进行测试。

## 5.2 链接到库

如果你愿意花时间编写简单输入输出所需的详细代码，那就像是每次想开车都要重新组装发动机。很有趣，但很耗时。在本书后面的部分，第 11 章，你将看到 MS-Windows 如何处理输入输出。当你看到这些工具时，一个新世界将开启。

但现在，在你熟悉汇编语言时，输入输出应该是相当简单的。5.3节节了如何调用书中提供的 `Irvine32.lib` 库。该库的完整源代码随书附的光盘提供，并在网站上定期更新。

> 如果在实地址模式下编写 16 位程序，`Irvine16.lib` 库包含了与 `Irvine32.lib` 相同的过程。

### 5.2.1 背景信息

库是一个包含已汇成机器码的文件。库中的代码始于一个或多个源文件，其中包含过程、常量和变量。源文件被汇成对象文件，对象文件被插入库中。

假设你想通过调用名为 `own` 的过程让你的程序在控制台上显示字符串。你的程序将有一个命名要调用过程的 `PROTO` 指令。以下指令位于 `Irvine32.inc` 文件中：

```
WriteString
```

接下来，使用 `CALL` 指令执行 `WriteString` 过程：

```
call WriteString
```

当你的程序被汇编时，汇器会留空 `CALL` 指令的目标地址，知道稍后将由链接器填充。链接器会在链接库中查找 `WriteString` 名称，并将库中相应的机器指令复制到你的程序执行文件中。此外，它会将 `WriteString` 的地址插入 `CALL` 指令中。

如果你尝试调用链接库中不存在的过程，链接器会发出错误信息且不生成可执行文件。

## 5.2 链接到外部库

链接器选项（Linker Command Options）链接器程序将你的程序对象文件与一个多个对象文件以及链接库结合。例如，以下命令将 `hello.obj` 链接到 `irvine32.lib` 和 `kernel32.lib` 库：

```
link32 hello.obj irvine32.lib kernel32.lib
```

你一直汇编和链接程序的批处理文件（`make32.bat` 或 `make16.bat`）使用了相同的命令。唯一的区别是使用了可替换参数（`%1`）来代替“hello”。这允许批处理文件链接到任何程序：

```
link32 %1.obj irvine32.lib kernel32.lib
```

整体结构（Overall Structure）你可能想知道 `kernel32.lib` 处于图中的位置。该文件由 Microsoft Windows 平台软件开发包（SDK）提供。它包含了存储在名为 `kernel32.dll` 的另一个文件中的操作系统函数的链接信息。后者是 Windows Windows 操作系统的基本部分之一，被称为动态链接库。它包含了执行基于字符的输入输出的可执行函数。你可以将 `kernel32.lib` 视为通 `kernel32.dll` 的桥梁，如图所示：

![](img/ea8a6a99b0e33c5c1bf5dd603b329094_168_0.png)

利用本章中学的知识，你的程序将链接到 `Irvine32.lib`。在后的第11章，你将学习如何将程序直接链接到 `kernel32.lib`。

## 5.2.2 节后练习

1. (对/错) 链接库由汇编语言源组成。
2. 使用 `PROTO` 指令在外部链接库中声明过程 `MyProc`。
3. 写一个 `CALL` 语句来调用外部链接库中名为 `MyProc` 的过程。
4. 本书提供的 32 位链接库名称是什么？
5. 哪个库包含了从 `Irvine32.lib` 用的函数？
6. `kernel32.dll` 是什么？
7. `make32.bat` 文件中用于可替换文件名参数的名称是什么？

## 5.3 本书的链接库

### 5.3.1 概述

表 5-1 是 `Irvine32` 链接库过程名称的快速参考。（后续章节将引入一些额外的过程）。首先，必须解释几个术语：

- console：一个 32 位控制台窗口，在 MS-Windows 中以彩色模式运行。默认情况下有 80 列 25 行。
- standard input（标准输入）：标准输入设备是键盘，尽管它可以从命令提示符重定向以从文件或串口端口读取。
- standard output（标准输出）：标准输出设备是视频显示器，尽管它可以从命令提示符重定向以写入文件、打印机或串口端口。

| Procedure | Description |
| --- | --- |
| Clrscr | 清除控制台并将光标置于左上角。 |
| Crlf | 向标准输出写入行尾序列。 |
| Delay | 暂停程序执行指定的 $n$ 毫秒间隔时间。 |
| DumpMem | 以十六进制格式向标准输出写入内存块。 |
| DumpRegs | 以十六进制显示 EAX, EBX, ECX, EDX, ESI, EDI, ESP, EFLAGS 和 EIP 寄存器。还显示进位（Carry）、符号（Sign）、零（Zero）和溢出（Overflow）标志。 |
| GetCommandtail | 将程序的命令行（称为*command tail*）拷贝到字节数组中。 |
| GetMseconds | 返回自午夜以来经过的毫秒数。 |
| Gotoxy | 定控制台上的特定行列。 |
| Random32 | 生成 0 到 FFFFFFFF 范围内的 32 位伪随机整数。 |
| Randomize | 使用唯一值设置随机数生成器的种子。 |
| RandomRange | 在指定范围内生成伪随机整数。 |
| ReadChar | 从标准输入读取单个字符。 |
| ReadHex | 从标准输入读取 32 位十六进制整数，以回车键结束。 |
| ReadInt | 从标准输入读取 32 位有符号十进制整数，以回车键结束。 |
| ReadString | 从标准输入读取字符串，以回车键结束。 |
| SetTextColor | 设置所有后续输出到控制台的前景和背景颜色。*Irvine16.lib 不可用*。 |
| WaitMsg | 显示消息并等待按下回车。 |
| WriteBin | 以 ASCII 二进制格式向标准输出写入无符号 32 位整数。 |
| WriteChar | 向标准输出写入单个字符。 |
| WriteDec | 以十进制格式向标准输出写入无符号 32 位整数。 |
| WriteHex | 以十六进制格式向标准输出写入无符号 32 位整数。 |
| WriteInt | 以十进制格式向标准输出写入有符号 32 位整数。 |
| WriteString | 向标准输出写入空终止字符串。 |

### 5.3.2 过程过程描述

`Clrscr`：`Clrscr` 过程清除屏幕。这通常在程序的开始和结束时进行。如果你在其他时间调用它，请记住在调用 `Clrscr` 之前（通过调用 `WaitMsg`）暂停程序。这将允许用户在信息被擦除之前查看。例如：

```
call Clrscr
```

`Crlf`：`Crlf` 过程将光标移动到标准输出的下一行。它通过写入包含两个字节 0Dh 和 0Ah 的字符串来实现。例如：

```
call Crlf
```

`Delay`：`Delay` 过程暂停程序指定的时间间隔。调用此函数时，将 `EAX` 设置为所需的毫秒数。（`Irvine16.lib` 版本的过程在 Windows NT 或 XP 下不起）。例如：

```
mov eax, 1000
call Delay
```

`DumpMem`：`DumpMem` 过程以十六进制格式向标准输出写入内存范围。调用它时，通过 `ESI` 传递起始地址，通过 `ECX` 传递数量（1 = 字节，2 = 字，4 = 双字）。以下语句显示一个双字数组：

```
.data
array DWORD 1,2,3,4,5,6,7,8,9,0Ah
.code
main PROC
    mov esi, OFFSET array; 起始地址
    mov ecx, LENGTH array    ; 数量
    mov ebx, TYPE array        ; 双字格式
    call DumpMem
```

使用给定的数据由 `DumpMem` 输出如下：

```
0000001 0000002 0000003 0000004 0000005 0000006
0000007 0000008 0000009 000000A
```

`DumpRegs`：`DumpRegs` 过程以十六进制显示 `EAX`, `EBX`, `ECX`, `EDX`, `EBP`, `ESP`, `EIP` 和 `EFLAGS` 寄存器。它还显示进位、符号、零和溢出标志。这是一个示例：

```
EAX=00000613 EBX=00000000 ECX=00000FF EDX=00000000
ESI=00000000 EBP=000001E0 OF=0
```

`EIP` 的显示值是调用 `DumpRegs` 之后的指令偏移。`DumpRegs` 在调试时非常有用；它可以在程序运行时显示 CPU 的快照。它没有输入参数，也没有返回值。

`GetCommandtail`：`GetCommandtail` 过程将命令行拷贝到空终止字符串中。如果发现命令行为空，则设置进位标志；否则清除进位标志。此过程非常有用，因为它允许通过命令行传递信息。例如，名为 `Encrypt` 的程序读取名为 `file1.txt` 的输入文件并产生名为 `file2.txt` 的输出文件。用户可以在运行程序时在命令行传递两个文件名：

```
Encrypt file1.txt file2.txt
```

`Encrypt` 程序启动时可以调用 `GetCommandtail` 获取两个文件名。调用 `GetCommandtail` 时，`EDX` 必须包含至少 129 字节数组的偏移：

```
.data
cmdTail BYTE 129 DUP(0)      ; 空缓冲区
.code
mov edx,OFFSET cmdTail      ; 填充缓冲区
call GetCommandtail
```

`GetMseconds`：`GetMseconds` 过程返回自午夜以来经过的毫秒数。当你需要测量事件之间的时间时，此过程非常有用。返回值位于 `EAX`。没有输入参数。在以下示例中，我们调用一次函数并存储返回的值。接下来执行一个循环。最后，我们再次调用 `GetMseconds` 并减去两个时间。我们现在知道了循环的持续时间（毫秒）：

```
.data
startTime DWORD ?
.code
call GetMseconds
mov startTime,eax
L1:
  ;(在此执行循环...)
Loop L1
call GetMseconds
  sub eax,startTime      ; EAX = 循环时间，毫秒
```

`Gotoxy`：`Gotoxy` 过程将光标位于屏幕上指定的行列。默认情况下，控制台的 X坐标范围是 0–79，Y坐标范围是 0–24。当你调用 `Gotoxy` 时，在 `DH` 中传递 Y坐标（行），在 `DL` 中传递 X坐标（列）。例如：

```
mov dh,10          ; 行 10
mov dl,20          ; 列 20
call Gotoxy        ; 定位光标
```

`Random32`：`Random32` 过程生成一个 32 位随机整数并在 `EAX` 返回。当重复调用时，Random32 生成一个模拟随机序列，其中每个数字被称为伪随机整数¹。这些数字是使用具有名为“种子”的输入的简单函数创建的。该函数在公式中使用种子生成第一个随机值。下一个随机值使用上一个随机值作为其种子生成。通常，我们使用“随机”一词来暗示伪随机。例如：

```
.data
randVal DWORD ?
.code
call Random32
mov randVal,eax
```

`Randomize`：`Randomize` 过程初始化 `Random32` 和 `RandomRange` 过程共同使用的随机数公式种子。种子等于当天的时间，精确

¹ 如果你想了解更多关于随机数生成器的信息，请参见 Donald Knuth. The Art of Computer Programming (Vol. 2). Addison-Wesley.

精确到 1/100 秒。这实际上确保了你每次运行程序时，起始的随机整数都是不同的，并且任何随机数序列也是唯一的。你只需要在程序开始时调用一次 `Randomize`。在接下来的示例中，我们生成了十个随机整数：

```
call Randomize
mov ecx,10
l1: call Random32
; 在 EAX 中使用或显示随机值...
Loop l1
```

**`RandomRange`** `RandomRange` 过程产生一个 0 到 (n-1) 范围内的随机整数，其中 n 是通过 `EAX` 寄存器传递的输入参数。随机整数返回在 `EAX`。例如，以下语句生成一个 0 到 4999 之间的单个随机整数并将其放入 `EAX` 中：

```
.data
randVal DWORD ?
.code
mov eax,5000
call RandomRange
mov randVal,eax
```

**`ReadChar`** `ReadChar` 过程从标准输入读取单个字符，并将字符返回在 `AL` 寄存器中。该字符不会在屏幕上回显。以下是一个示例调用：

```
.data
char BYTE ?
.code
call ReadChar
mov char,al
```

**`ReadHex`** `ReadHex` 过程从标准输入读取一个 32 位十六进制整数，并将值返回在 `EAX`。对于无效字符不进行错误检查。你可以对 A 到 F 使用大写或小写。最多可以输入八位数。不允许有前空格。示例：

```
.data
hexVal DWORD ?
.code
call ReadHex
mov hexVal,eax
```

**`ReadInt`** `ReadInt` 过程从标准输入读取一个 32 位符号整数，并将值返回在 `EAX`。用户可以输入可选的前导加或减号，数字部分只能由数字组成。如果输入的值无法表示为 32 位符号整数（范围：-2,147,483,648 到 +2,147,483,647），`ReadInt` 将设置溢出标志并显示错误消息。以下是一个示例调用：

```
.data
intVal SDWORD ?
.code
call ReadInt
mov intVal,eax
```

**`ReadString`** `ReadString` 从标准输入读取字符串，直到用户按下 Enter 键。它将读取的字节数返回在 `EAX` 寄存器。在调用 `ReadString` 之前，将 `EDX` 设置为存储输入字符的字节数组的偏移，并将 `ECX` 设置为最大字符数加 1（为终止空字节留出空间）。

以下语句调用 `ReadString` 并传递 `ECX` 和 `EDX`：

```
.data
buffer BYTE 50 DUP(0)      ; 存储字符
byteCount DWORD ?          ; 存储计数器
.code
mov edx,OFFSET buffer     ; 指向缓冲区
mov ecx,(SIZEOF) buffer   ; 指定最大字符
call ReadString             ; 输入字符串
mov byteCount,eax          ; 字符数
```

`ReadString` 会在字符串末尾自动插入空终止符。以下是用户输入字符串 "ABCDEFG" 后，`buffer` 前八个字节的十六进制和 ASCII 转储：

```
41 42 43 44 45 46 47 00                ABCDEFG
```

变量 `byteCount` 等于 7。

**`SetTextColor`** `SetTextColor` 设置文本输出的当前前景和背景颜色。以下是预定义的颜色常量，可同时用于前景和背景：

| black = 0 | red = 4 | gray = 8 | lightRed = 12 |
| blue = 1 | magenta = 5 | lightBlue = 9 | lightMagenta = 13 |
| green = 2 | brown = 6 | lightGreen = 10 | yellow = 14 |
| cyan = 3 | lightGray = 7 | lightCyan = 11 | white = 15 |

这些颜色常量定义在 `Irvine32.inc`（以及 `Irvine16.inc`）中。背景颜色在与前景颜色相加之前乘以 16。以下常量示例显示了蓝色背景上的黄色字符：
