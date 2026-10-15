
### 00000024 : 使用数据定义命令创建局部变量和函数参数。

`00000024` : 两个特殊字段：`"r"` 和 `"s"` 代表返回地址和保存的寄存器。

`00000024` : Frame size: 24; Saved regs: 0; Purge: 0

`00000024`

`00000024`

`00000023`

`00000022`

`00000022` : db ? : undefined

`00000022` : db ? : undefined

`00000021` : db ? : undefined

`00000021` : db ? : undefined

`00000020` : db ? : undefined

`0000001F` : db ? : undefined

`0000001E` : db ? : undefined

`0000001D` : db ? : undefined

`0000001C` : db ? : undefined

`0000001B` : db ? : undefined

`0000001A` : db ? : undefined

`00000019` : db ? : undefined

`00000018` : LastWriteTime  FILETIME ?

`00000008` : LastAccessTime  FILETIME ?

`00000008` : CreationTime FILETIME ?

`00000008` : r

`00000008` : 1pFileName db 4 dup      ; offset

`00000008` : arg_4          dd?

`0000000C` dd?

`0000000C` : end of stack variables

**示例 2.**
下面的栈帧视图再次显示了 12 字节缓冲区：

```
00000020 : D /* create structure member (data/asci)
00000020 : N : rename structure member
00000020 : U : delete structure member
00000020 : 使用数据定义命令创建局部变量和函数参数。
00000020 : 两个特殊字段："r" 和 "s" 代表地址和保存的寄存器。
00000020 : Frame size: 20; Saved regs: 4; Purge: 0
00000020
00000020
00000020
00000020
00000020
00000020
00000020
00000010
00000010
00000010
00000014 : var_14 : undefined
00000010 : var_10 : undefined
00000008 : var_8 : undefined
00000008 : Str : undefined
00000004 : db 8 dup(?) ; offset
00000004 : R : db 4 dup(?)
00000000 : arg_0 : undefined
00000000 : arg_4 : undefined
00000018 : arg_8 : undefined
00000014 : arg_C : undefined
00000018 : arg_10 : undefined
00000001 : end of stack variables
```

我理解 IDA 将其标记为 `undefined` 是因为它无法确定这些偏移是如何使用的。我也意识到 IDA 通过监控 `ESP` 来自动计算栈帧的大小。我假设这与非易变寄存器区域有关。然而在**示例 1** 中它显示 **Saved regs**: 0，而在**示例 2** 中它显示 **Saved regs**: 4。我很困惑，以下是我的问题：

为什么 IDA Pro 在栈视图中显示某些缓冲区或填充（较低地址处的）局部变量？两者都恰好显示 12 字节是巧合吗？这是因为调用约定还是编译器的原因？

标签：反汇编 (前 Q) (后 Q), ida (前 Q) (后 Q)

用户：pss
回答：jason-geffner

IDA 在对整个函数进行静态分析期间会跟踪栈指针 (`ESP`)。`ESP` 的最大值（相对于函数起始位置）用于确定栈帧的大小。对于你在顶部发布的为 "`undefined`" 的栈帧，是因为 IDA 无法自动确定那些偏移是如何使用的。

## Q: 如何在 IDA 中重新分析一个函数？

是否有方法可以重新分析单个函数并将其恢复到分析后的状态？

标签：反汇编 (前 Q) (后 Q), ida (前 Q) (后 Q)

用户：pss
回答：n00b

嗯，你必须先使用 `U` 键将代码取消定义（undefine），选择代码并右键，你会得到像 `C (code)` 等选项。IDA 还让你能够对混淆代码进行任何操作，以帮助正确理解代码。

补充：
转换为 `C (code)` 后，按 `Alt+P` 创建/编辑函数。此外，通过进入 Layout 视图，清除空间并选择“Layout graph”来重新构建布局。

标签：反汇编 (前 Q) (后 Q), ida (前 Q) (后 Q)

## Q: IDA Pro：“CREATE EXE file...”选项的作用是什么？

标签：反汇编 (前 Q) (后 Q), ida (前 Q) (后 Q)

我在 IDA 中发现了 `File -> Create EXE file...` 选项。我原以为不能用 IDA 进行补丁（patching），结果试了一下。然而它给出了以下错误：不支持此类型的输出文件。

这个选项是做什么的？可能的用途是什么？

标签：反汇编 (前 Q) (后 Q), ida (前 Q) (后 Q)

用户：pss
回答：dcoder

此选项价值有限。IDA 仅为以下格式生成执行文件：
- MS DOS `.exe`
- MS DOS `.com`
- MS DOS `.drv`
- MS DOS `.sys`
- 通用二进制
- Intel Hex Object Format
- MOS Technology Hex Object Format

—— IDA帮助文件
虽然这是最有前景的菜单选项，遗憾的是它也是受限最严重的。简而言之，它对大多数文件类型不起作用……

—— IDA Pro 书 第 14 章
该章节详细说明了为什么这个选项没有很有用。首先，IDA 没有解析并保存作为 `.rsrc` 的内容部分，也没有方法将表重新/导出回原始格式。读这本书。不是针对这个问题，它是一本很有用的读物。

标签：反汇编 (前 Q) (后 Q), ida (前 Q) (后 Q)

## Q: 调用变量地址

标签：反汇编 (前 Q) (后 Q)

我遇到了以下指令：

```
mov ecx, [ebp + var_4]
imul ecx, 4
call dword_1423d4[ecx]
```

有人能解释这可能是什么意思或者指点正确的方向？为什么要调用变量？

标签：反汇编 (前 Q) (后 Q)

用户：cream-cracker
回答：jason-geffner

`dword_1423d4` 是一个指向全局32位函数指针数组的指针。`var_4` 是该数组的索引。`call` 指令调用 `dword_1423d4` 数组中索引为 `var_4` 的函数。

## Q: 这种混淆方法是什么？

标签：反汇编 (前 Q) (后 Q), 混淆 (前 Q) (后 Q), 恶意软件 (后 Q)

我最近看到了以下代码混淆方法：

```
...
```

```
jump loc_1234
      Bunch of junk
loc_1234:
code continued...
```

混淆机制背后的逻辑相当直接。在代码跳转中插入一堆垃圾代码（Bunch of junk），然后通过跳转指令跳过它们。其目的是混淆线性反汇器并泛泛混淆文件。我想学习更多关于它的信息。有人知道这叫什么吗？这种方法对现代防病毒软件的效果如何？

标签：反汇编 (上一个 Q) (下一个 Q)，混淆 (上一个 Q) (下一个 Q)，恶意 (下一个 Q)

用户：pss

## ekse 的回答

这种反汇编技术在《实战恶意软件分析》（Practical Malware Analysis）书中描述为“带有常量条件的跳转指令”（Jump Instruction with a Constant Condition）（第一版第16章第336页）。你描述的思路是让跳转条件始终成立，并在跳转后添加代码以在跳转位置产生错误的反汇编结果。由于反汇器假设两个分支都是连贯的，它只会反汇编其中一个。

关于对防病毒软件的有效性，大多数软件都使用模拟器。如果条件始终成立，模拟器将继续执行并看到正确的指令。

标签：反汇编 (上一个 Q) (下一个 Q)，混淆 (上一个 Q) (下一个 Q)，恶意 (下一个 Q)

## Q：IDA Pro：如何导出数据为 C 风格数组？

标签：反汇编 (上一个 Q) (下一个 Q)，ida (上一个 Q) (下一个 Q)

在汇编二进制文件时，我遇到了几个 `short` 类型数组。每个数组的大小为 1024 个成员。我想将它们导出为 C 风格数组，如下：

```c
short array[1024] = { 2, 5, 8, ..., 4 }; /* 这只是一个示例 */
```

我理论上可以复制/粘贴并手动修改代码。但这似乎非常枯燥。我想知道，有没有更好的方法来实现它？可以通过脚本/插件完成吗？

标签：反汇编 (上一个 Q) (下一个 Q)，ida (上一个 Q) (下一个 Q)

用户：pss

## rolf-rolls 的回答

一个小脚本就能解决问题。在 IDC 中，类似如下的代码：

## 跳过代码块

```c
auto ea, len, i;
len = 1024;
ea = /* whatever */;
Message("short array[] = {\n ");
for(i = 0; i < len; i = i + 1)
{
    Message("0x%04lx", Word(ea+i*2));
    if (i != len - 1)
    Message(", ");
    if(i > 0 && (i % 0x1f) == 0)
    Message("\n ");
}
Message("\n\n");
```

如果要处理 Byte 而不是 Word
将 `word(...)` 替换为 `Byte(...)`
以及
将 `0x%04lx` 替换为 `0x%02lx`
以及
将 Word(ea+i*2) 替换为 Byte(ea+i)

如果要处理 Dword 而不是 WORDS
将 `word(...)` 替换为 `Dword(...)`
以及
将 `0x%04lx` 替换为 `0x%08lx`
以及
将 Word(ea+i*2) 替换为 Dword(ea+i*4)

## chris-eagle 的回答

老问题了，但在 IDA 6.5 中，有一个新的菜单选项 Edit/Export data... 可以为你处理这种情况。首先首先选择你想要导出的数据，然后通过菜单选项选择输出格式和保存数据的文件名。

标签：反汇编 (上一个 Q) (下一个 Q) ida (上一个 Q) (下一个 Q)

## Q：IDA 会话内存中类似于“@YAXPAX@”的特征

标签：反汇编 (上一个 Q) (下一个 Q) ida (上一个 Q) (下一个 Q)

在反汇二进制文件和解析内存时，我经常遇到像 `@YAXPAX@` 这样的字符串作为引用。这种约定有名称吗？

标签：反汇编 (上一个 Q) (下一个 Q) ida (上一个 Q) (下一个 Q)

用户：rekav0k

## pss 的回答

我认为这种奇怪的字符串出现是因为名称修饰（Name Mangling），它也被称为名称装饰（name decoration）。编译器使用的名称修饰机制用于将语义相关信息从编译器传递给链接器。

以下是 Wikipedia 如何描述 Visual C++ 系列编译器的名称修饰的：

Visual C++ 名称修饰是 Microsoft Visual C++ 系列编译器中使用的一种修饰（装饰）方案。它提供了一种编码名称以及关于函数、类或其他数据类型的额外的方法，以便从 Microsoft Visual C++ 编译器向其链接器传递更多的语义信息。Visual Studio 和 Windows SDK（包含命令行编译器）附带了程序，可以调用这些程序以获取修饰名称编码的 C 风格函数。以下信息是经过反向工程得的。关于实际算法没有官方文档。

## vitaly-osip 的回答

(稍微偏题)
`cfilt` 是 Unix 上非常实用的反修饰（demangling）工具。我不确定它在 Visual Studio 中是否可用，但这是一个你可以编译的简单实现。比较输出 (g)：

## 跳过代码块
```bash
$ nm out
0000000000010040 S NXArgc
0000000000010040 S NXArgv
0000000000010048 T ZNcompxC1EED
0000000000010048 T ZNcompxC1ED
0000000000010048 T ZNcompxC2EED
0000000000010070 T ZN66commplxPLKS
0000000000010058 S progname
0000000000010000 T _mh_execute_header
0000000000010150 S _environ
0000000000010000 U _exit
0000000000010020 T _main
0000000000010090 S _ovars
0000000000010090 U dyld_stub_binder
00000000000100d0 T start
```

使用 c++filt：

## 跳过代码块 c++filt
```bash
$ nm out
0000000000010040 S NXArgc
0000000000010040 S NXArgv
0000000000010048 T ZNcompxIcdouble,double>
0000000000010048 T ZNcompxIcdouble,double>
0000000000010070 T ZNoperator(complex const&)
0000000000010058 S progname
0000000000010000 T _mh_execute_header
0000000000010150 S _environ
0000000000010000 U _exit
0000000000010020 T _main
0000000000010090 S _ovars
0000000000010090 U dyld_stub_binder
00000000000100d0 T start
```

## justsome 的回答

一个小提示，如果你不知道的话：可以在 IDA 的 Options -> Demangled names... 中修饰注释中的名称，你也可以将其改为函数本身。这可以去掉一些杂质！标签：反汇编 (上一个 Q) (下一个 Q) ida (上一个 Q) (下一个 Q)

## Q：IDA 中的 nullsub 函数是什么？

标签：反汇编 (上一个 Q) (下一个 Q) ida (上一个 Q) (下一个 Q)

在几乎由 IDA 创建的反汇文件中，有几个函数被标记为 `nullsub`，它们没有任何返回（只是 `ret` 指令）。

那么，它们是什么，为什么在数据库里？

标签：反汇编 (上一个 Q) (下一个 Q) ida (上一个 Q) (下一个 Q)

用户：ph0sec

## dcoder 的回答

我从 C++ 的角度回答，其他语言有不同的原因。这些函数有合法的用途，即使它们只是：

```cpp
void func(/* any args */ {})
```

我想到的一个例子是虚函数，在基类中什么都不做，但在派生类中被重写。另一个例子是模板函数，其通用情况为空但特化情况不是。更多的是静态变量。静态析构必须在程序结束时调用，这在第一次访问变量时使用 exit 来注册析构回调。我记得 C++ 标准说没有可观测行为的析构可能不会被调用，但我见过 MSVC 6.0 仍然会将 nullsubs 注册为析构。全局变量与静态变量类似。另一种可能是根据编译器没有影响的函数。该函数存在于某处（例如不知道实现的另一个编译单元），尝试调用它，但体是空的。请注意，“根据编译器”并不等同于编码者的理解。我自己曾写过一个执行大量工作的清理函数，但错误地按值传递参数而不是引用。编译器将整个函数体优化为 {} 且没有警告。哎。

## simeon-pilgrim 的回答

DCoder 的回答很棒，但其他原因包括：该函数在发布版本中可能 #ifdef 删除了，但这可能正是你需要的。这以后可以作为指针使用，如果那是你需要的。

## Q：OllyDbg 的语法和 C 等效写法

标签：反汇编 (上一个 Q) (下一个 Q) 汇编 (上一个 Q) (下一个 Q) x86 (上一个 Q) (下一个 Q)，ollydb (上一个 Q) (下一个 Q)

用户：lfgrove

## dcoder 的回答

`DWORD PTR [expression]` 语法意味着“取表达式的值，将其解释为地址，从该地址开始访问 4 个字节（DWORD 的大小”。但汇编数据类型与 C 类型不同，因此许多类型可以通过这种方式访问。

你提供的指令基本上等同于 C 代码：

```cpp
typedef dword_t ...;
dword_t eax = (dword_t *)(char *)(esi + 0x14);
```
