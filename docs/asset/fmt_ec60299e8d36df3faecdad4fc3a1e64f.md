
如果还需要 16 位的 DOS 调试器的话——请查看用于 DOS 的 `Insight` 调试器

标签：工具 (上一个) (后一个) 调试器 (上一个) (后一个)

## Q: 在进行二进制分析时，你如何存储关于二进制文件的数据？

工具 (上一个) (后一个), 二进制分析 (上一个) (后一个) 方法

现在，当我分析一个二进制文件时，我使用“笔和纸笔”的方法来定位函数的不同位置、不同类型的混淆以及我所有的发现。当我尝试分析二进制文件时，这种方法效率低下且完全没有扩展性。

我知道 `IDAPro` 有一个数据库来存储内容和一个内存区域，但如果我们不想使用 `IDAPro`，你们使用什么技术或（免费）工具来收集笔记并妥善地显示它们？

标签：工具 (上一个) (后一个) 二进制分析 (上一个) (后一个)

用户：perror

gandolf 的回答

你知道的，woodman 论坛上讨论过要制定某种标准来分享逆向工程（RE）笔记，那会很好。但我通常只是尝试尽量使用记事本，对于协作工作，我会使用 `Google Docs`。最近我也开始使用 `Evernote` 进行协作工作，仅仅是因为使用 `Google Docs` 需要我使用网页界面来处理它们的文档格式。

newgrere 的回答

当我处理一个需要创建许多结构化节点的非常复杂的项目时，我经常使用 `tidly wiki`。它的好之处在于你可以轻松备份这个 wiki，因为它直接写入其 html 文件中。

当然还有 `Google Docs`，如果你在进行协作，它特别有用。

标签：工具 (上一个) (后一个) 二进制分析 (上一个) (后一个)

## Q: 混淆 Python 程序的技术和工具有哪些？

标签：工具 (上一个) (后一个) 混淆 (上一个) (后一个) python (上一个) (后一个)

mikeazo 提到他的程序提供了一个自定义的 Python 解释器，但其他技术是什么，它们的效率如何？

标签：工具 (上一个) (后一个) 混淆 (上一个) (后一个) python (上一个) (后一个)

用户：perror

mikeazo 的回答

当你使用自定义解释器打包你的 python 应用时，可以使用这些技巧：

1. 为解释器重新映射操作码（`opcodes`）

2. 加密 `pyc` 文件（自定义解释器在导入前会进行解密）

3. 移除解释器中对 `co_code` 的访问（在解释器代码对象的 `code_memberlist` 数组声明中中删除对 `co_code` 的引用）

4. 混淆/保护解释器

5. 不要捆模块，因为这有助于逆向工程（基本上是逆向工程一个混淆程序，而不是全部）

6. 修改解释器使其只能导入 `pyc` 文件（可以通过在解释器中删除或过滤来实现）

7. `pyRE` 的那些人提供了一些进入自定义解释器的标准技术。在你的应用上测试这些方法并尝试禁用这些方法，会让逆向工程师的工作变得困难得多。

8. 从解释器中移除可以帮助逆向工程人员的函数，如 `PyRunString()`。否则，他们可以使用调试器附加并运行任意代码。

- `pyRE` – Rich Smith 编写的混淆 Python 字节码的逆向工程。DEFCON-1, Vegas, 2010.

antimony 的回答

我不知道任何 Python 混淆工具（可能因为那些想要写混淆代码的人并不会去写）。然而，如果我需要混淆 Python 代码，我可能会使用你对任何语言程序使用的相同技术。工具的缺乏意味着你可以编写自己的混淆器，但这并不困难。

- 混淆 Python 字节码的逆向工程，Rich Smith 编写。 (后一个)

标签：工具 (上一个) (后一个) 混淆 (上一个) (后一个)

## Q: 针对 Python 字节码，有哪些可以进行分析的工具？

标签：工具 (上一个) (后一个) python (上一个) (后一个)

最近在 Reddit 上发现了一个可以生成 CFG 形式的 Python 字节码：

```
off_0000000:LOAD_FAST 'a'
LOAD_FAST 'c'
LOAD_CONST 1
BINARY_ADD
COMPARE_OP '=='
JUMP_IF_FALSE 25
```

```
off_0000025:POP_TOP
LOAD_FAST 'b'
LOAD_CONST 3
COMPARE_OP '=='
JUMP_IF_FALSE 60
```

```
off_0000016:POP_TOP
LOAD_CONST 'l1'
PRINT_ITEM
JUMP_FORWARD 66
```

```
off_0000038:POP_TOP
LOAD_GLOBAL 'i'
LOAD_CONST 2
COMPARE_OP '=='
JUMP_IF_FALSE 60
```

```
off_0000060:POP_TOP
LOAD_CONST 'test!'
PRINT_ITEM
PRINT_NEWLINE
```

```
off_0000051:POP_TOP
LOAD_CONST 'lo'
PRINT_ITEM
PRINT_NEWLINE
JUMP_FORWARD 66
```

```
off_0000066:LOAD_CONST None
RETURN_VALUE
```

控制流图：'testing_1'

我在想是否有工具可以对 Python 字节码进行静态分析，并具有一些功能（例如生成 CFG 或允许操作代码）？

标签：工具 (上一个) (后一个) python (上一个) (后一个)

用户：perror

jvoisin 的回答

有几个用于 Python 字节码逆向的工具：

- `Uncompile` 和 `Uncompile2`

`uncompile` 将 Python 字节码转换为等效的 Python 源代码。它接受 Python 2.7。生成的源代码可读性很高：文档字符串、列表和元组都有漂亮的打印。

`uncompile` 还可以通过编译生成的源代码来验证其等效性。`uncompile` 基于 John Aycock 的小型语言编译器 ‘spark’ (http://www.csr.uvic.ca/~aycock/python/) 以及他之前关于 ‘decompile’ 的工作。

- `pyREtic`，更多是一个强大的框架而不是简单的程序

`pyREtic` 是一个用于 Python 语言各种逆向工程任务的可扩展框架。它帮助逆向工程师从字节码（`pyc`）中获取源代码（`py`），特别是当代码在逆向时进行了一些尝试阻止反编译的努力。

- `pycdc`，比 `uncompile` 更好且更简单 `pyREtic`

`Decompile++` 旨在将 Python 字节码翻译回有效且易读的 Python 源代码。虽然其他项目也取得了不同的成功，但 `Decompile++` 的独特之处在于它寻求支持任何版本 Python 的字节码。

`Decompile++` 了一个字节码反汇编器 (`pydatas`) 和一个反编译器 (`pycdc`)。

- 专注于 Python3 的 Maynard 框架

94c3 的回答

`Maynard` 是一个 Python 字节码的（反）汇编器，由一位 Python 核心成员和 Python 3.4 的发布者编写。阅读材料见这里和这里。我不知道（除了你链接的那个）还有什么公共工具可以像这样的 CFG 可视化，但你完全可以在 `Maynard` 之上构建一个。

# denis-laskov 的回答

来自 `Immunity Sec` 的 `pyREtic` 也可以为查看原始源代码并进行修改提供帮助。

你可能对本文中工具的能力感兴趣：由 Rich Smith 写的“pyREtic, In memory reverse engineering for obfuscated Python bytecode” [PDF]

标签：tools (上一个) (下一个) python (上一个) (下一个)

# Q：如何从旧的可执行文件 (New Executable, NE) 中提取资源？

标签：tools (上一个) (下一个)

我正尝试从一个旧的可执行文件 (NE) 中提取菜单和其他内容，就是 Windows 16 位时代的那种。我找到的工具（例如 `ResourceTuner`）只适用于 PE 文件。

有什么工具可以方便地提取资源吗？可能需要几个步骤，例如：一个程序用于提取原始资源，另一个程序用于以正确的格式显示它们。

标签：tools (上一个) (下一个)

用户：heinrich5991

# ange 的回答

你应该尝试 `OpenWatcom` 的资源编辑器 (`Resource Editor`)，也 Setup `Hiew` 和 `HT Editor`，尽管后两者可能无法以正确的格式显示它们，因为它们只是支持 NE 的十六进制编辑器。

`OpenWatcom` 包含了用于 Win-16 开发的完整工具链。

## igor-skochinskinsky 的回答

获取旧工具的一个很好的资源是 SAC 服务器。通过快速搜索，`Resource Grabber` 似乎支持 NE 资源，虽然它的 UI 很难用。

另一个选项是 `eXeScope`（共享软件）。

此外，很久以前我发现过一个名为 `dresplay.exe` 的工具。我现在没有它了，Google 似乎也不知道它……

标签：tools (上一个) (下一个)

# Q：哪里可以找到 Lua 反向工程的工具？

标签：tools (上一个) (下一个)

由于 Lua 是一种解释/编译语言，它有自己的编译器，通常不与 C 编译器一起翻译/编译。哪些工具可以用于反向工程 Lua 应用程序？

标签：tools (上一个) (下一个)

用户：cb88

# cb88 的回答

如果你的应用程序被编译成二进制文件，你可能仍然可以使用 `IDA` 这样的普通调试器。Lua 有自己的工具来反编译机器码和字节码。这些链接应该由 Lua 社区保持更新。

Lua Wiki: LuaTools

如果你需要对 Lua 5.2 支持，`LuaAssemblyTools` 是第一个支持它的工具。

标签：tools (上一个) (下一个)

# Q：哪里可以获得可靠的 RE (反向工程) 工具？

标签：tools (上一个) (下一个)

我正在寻找一个可靠的来源来下载 RE 工具，例如：

- 1. `Lordpe`

- 2. `Imprec`

- 3. `Peid`

但这意味着 Google 上的链接是不安全的，我可以在哪里从非恶意的来源购买或下载？我可以信任 http://www.woodmann.com/ 吗？

标签：tools (上一个) (下一个)

用户：0x90

## jason-geffner 的回答

存档在 http://www.woodmann.com/ 上的工具应该是安全的。

我个人见过并信任运行该网站的大多数人（Woodmann, dELTA 等），我为他们的诚信背书。

# gandolf 的回答

还有 tuts4you 这个选项。他们在那里有一个下载页面。

# pss 的回答

还有 http://www.openrce.org/downloads/。虽然它没有你寻找的特定工具，但它有 `IDA` 和 `OllyDbg` 的日志。它也是一个可靠的来源。

标签：tools (上一个) (下一个)

# Q：如何从 MS-Windows 操作系统反编译 Linux .so 库文件？

标签：tools (上一个) (下一个)

我想反编译 Linux `.so` 文件。

- 有在 MS-Windows 下反编译 `.so` 文件的工具吗？

标签：tools (上一个) (下一个)

用户：blueberry–vignesh43

# oxen 的回答

Linux 共享对象 (shared objects) 也是 ELF！任何适用于“普通”ELF 文件的反编译器对 SO 文件都是通用的。

这么说，你可以使用 `IDA` 反汇编它们。如果你有带 Hex-rays 的 `IDA`，可以使用它。如果没有，可以尝试 `ida-compiler` 插件。它是开源的，但功能远不如 Hex-rays。

反汇编和汇编的区别在于反汇编会给你汇编代码。反编译汇编代码不是一项容易的任务，因为许多抽象在汇编层面丢失了。恢复这些抽象是困难的，例如变量名。

另一方面，将字节码反编译为高级语言（如 Java）要容易一些，因为许多抽象在字节码中保留了。使用当前工具自动反编译汇编并不完美，你也可以通过识别结构（如循环、switch 语句等）手动将汇编反编译为高级语言。

# perror 的回答

正如 oxen 所说，`.so` 文件只是普通的执行文件但以动态库格式打包。我知道你专门问了 MS-Windows 工具，但我会忽略 0xeea 的回复。我会尝试解释用 UNIX 工具来实现。

## 从库提取函数

第一步是提取库中存在的所有函数名称，以便知道它是什么样的。我将使用 `/usr/lib/libao.so.4.0`（我随机找的一个库，足够小，可以作为示例）。首先，对其运行 `readelf` 查看位信息：

```
# readelf -a /usr/lib/libao.so.4.0
ELF Header:
Magic: 7f 45 4c 46 02 01 00 00 00 00 00
Class: ELF64
Data: 2' little endian
Version: 1 (current)
OS/ABI: UNIX
ABI Version: 0
Type: (Shared object)
Machine: Advanced Micro Devices X86-64
Version: 1
Entry point address: 0x1bf0
Start of program headers: 64 (bytes)
Start of section headers: 35392 (bytes)
Flags: 0x0
Size of header: 64 (bytes)
Size of program headers: 56 (bytes)
Number of program headers: 6
[...]
```

你可能会注意到 `readelf` 探测到的条目。实际上，它对应正确加载库的程序。但对我们来说没有用。

查看 `readelf -a` 的输出结果，动态符号表 (`.dynym`) 很有信息，包含如下条目：

```
43: 00000000000003be 1302 FUNC GLOBAL DEFAULT 13 ao_play@@LIBA40_1.0
```

事实上，每个动态库都在列表中，我们可以简单地提取：
