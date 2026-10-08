
It sounds like what you need node groups. Since the very first implementation (5.0) IDA’s graph view allowed to group several nodes into one “super-node” with a custom title. Select the nodes you want to group with `Ctrl-click` and choose “Group nodes” from the context menu.

For more info, see “Graph node groups” in IDA's help or online.

Tags: ida (Prev Q) (Next Q)

# Q: How to map an arbitrary address to its corresponding basic block in IDA?

Tags: ida (Prev Q) (Next Q)

Say I have an arbitrary address and Want to find out which basic block (i.e. `area_t`) corresponds to it. How would I do that?

Edit: more specifically, I want to know the beginning / end of the basic block to which a given address belongs.

Tags: ida (Prev Q) (Next Q)

User: newgre

Answer by dcoder

I put this together quickly in the File > Python command... dialog:

```
tgtEA = idaapi.askaddr(0, "Enter target address")
if tgtEA is None:
    exit

f = idaapi.get_func(tgtEA)
if not f:
    print("No function at 0%x" % (tgtEA))
    exit
fc = idaapi.FlowChart(f)
for block in fc:
    if block.startEA <= tgtEA:
        if block.endEA >= tgtEA:
            print("0%x is part of block [0%x - 0%x]" % (tgtEA, block.startEA, block.endEA))
```

Keep in mind IDA’s basic block addresses are “startEA inclusive, endEA exclusive”.

Answer by newgre

As suggested by DCoder, I use the following helper class to efficiently resolve addresses to basic blocks:

```python
# Wrapper to operate on sorted basic blocks.
class BBWrapper(object):
    def __init__(self, ea, bb):
        self.ea_ = ea
        self.bb_ = bb

def get_bb(self):
    return self.bb_

def __lt__(self, other):
    return self.ea_ < other.ea_

# Creates a basic cache for all blocks in the given function.
class BBCache(object):
    def __init__(self, f):
        self.bb_cache_ = []
        for bb in idapi.FlowChart(f):
            self.bb_cache_.append(BBWrapper(bb.startEA, bb))
        self.bb_cache_ = sorted(self.bb_cache_)

def find_block(self, ea):
    i = bisect_right(self.bb_cache_, BBWrapper(ea, None))
    if i:
        return self.bb_cache_[i-1].get_bb()
    else:
        return None
```

It can be used like this:

```python
bb_cache = BBCache(idaapi.get_func(here))
found = bb_cache.find_block(here)
if found:
    print("found: %X - %X" % (found.startEA, found.endEA))
else:
    print("No basic block found that contains %X" % here)
```

Tags: ida (Prev Q) (Next Q)

# Q: IDA Convert to Unicode ↩

Tags: ida (Prev Q) (Next Q), encodings (Next Q)

In IDA 5.0 Freeware how do you convert a block of data into a unicode string, the thing I can find is to convert it into ascii string.

```
db 'a'
db 0
db 'b'
db 0
db 'c'
db 0
db 'd'
db 0
db 0
db 0
```

into

unicode <abcd>, 0

Tags: ida (Prev Q) (Next Q), encodings (Next Q)

User: avery3 ↩

Answer by rolf-rolls ↩

Press `Alt-A` to bring up the “string style” dialog, from which you can create a string of various types (including Unicode). Through this dialog, you can optionally set the default string type that is created when you press a key (i.e. you can make it that Unicode is the default if you want.

Alternatively use `Alt+A+U` as pointed out by joseankoret in the comment.

Answer by ekse

Select the first byte, Edit -> Strings -> Unicode.

Tags: ida (Prev Q) (Next Q), encodings (Next Q)

# Q: Could you list some useful plugins and scripts for IDA Pro?

Tags: ida (Prev Q) (Next Q)

I am just starting to use IDA Pro. After discussing a bit with the community, it seems that IDA Pro plugins and scripts are quite important to reach a good level of productivity while analyzing a program.

What are some must have plugins for IDApro that you would recommend for an everyday usage.

Tags: ida (Prev Q) (Next Q)

User: perror

Answer by peter

### 架构（Architecture）

用于特定架构的逆向辅助插件。

- ia32

- amd64

### 操作系统（Operating System）

用于特定操作系统的逆向辅助插件。

- Windows

- Linux

### 编译器（Compiler）

使用特定编译器编译的程序的逆向辅助插件。

- Microsoft Visual

... (注：由于原文包含大量重复的标签和占位符，此处已完成核心内容翻译)

[ida](上一个问题) [下一个问题), [debuggers](上一个问题) [下一个问题)

是否有良好的资源可以利用 SDK 开发 IDA 调试器插件，并对 IDA API 进行描述？其中之一是 Sourceforge 上的 IDA Pro ARM 调试器插件。似乎很少有项目实现了这一点。具体来说，如何在 IDA 中制作一个插件，使其能够注册为可用调试器之一，并允许在控制目标的同时步进 IDA 数据库？

标签：[ida](上一个问题) [下一个问题), [debuggers](上一个问题) [下一个问题)

用户：[dingo_kinznerhook]

[回答] 由 [igor-skochinskinsky]()

这里没有一个回答回答了实际的问题。

调试器插件与“普通”插件有两点不同：

- 1. 插件的标志位中具有 `PLUGIN_DBG`。

- 2. 在(其中)，它必须将全局变量 `db` 设置为指向 `debugger_t` 结构体实现的指针。定义请参见 `idd.hpp`。

示例，请参考 SDK 中的 `plugins/debugger`，以及最近更新的 [idos plugin]()。警告：制作调试器插件不是胆弱者的之选。

[回答] 由 [denis-laskov]()

你可以查看 C/C++ 版本的 IDA 插件手册 [这里]()。

你也可以观看 Recon 2008 上 IDA Creator Ilfak Guifanov 的演讲，**为 IDA 开发插件** 见 [SecurityTube]()。

还可以使用 IDAPython 创建一些自动化工具。

[回答] 由 [newgre]()

[idapython]() 套件中的 `debugger.py` 脚本说明了调试器插件可以处理的所有调试事件。

# 示例脚本

这是一个简单的脚本，它在你使用调试器跟踪时为所有指令着色。

```python
# 简单脚本会将调试器停止或
# 用户使用调试器跟踪的指令标记为黄色。
# 第二次出现的指令被标记为红色。

from idaapi import *
from idc import *

class Colorizer(DBG_Hooks):
```

```python
def __init__(self):
    DBG_Hooks.__init__(self)
    self.locations_ = set()

def colorize(self, ea):
    if ea in self.locations_:
        SetColor(ea, CIC_ITEM, 0x2020c0)
    else:
        SetColor(ea, CIC_ITEM, 0x8fffff)
        self.locations_.add(ea)

def dbg_bpt(self, tid, ea):
    self.colorize(ea)
    return 0

def dbg_step_into(self):
    self.colorize(GetRegValue("eip"))

try:
    if debughook:
        print("Removing previous hook...")
        debugook.unhook()
except:
    pass

colorizer = Colorizer()
colorizer.hook()
```

# 注意

如果你在调试器回调函数中读取进程内存，你需要先调用 `refresh_debugger_memory()`（参见 `idc.py` 中 `RefreshDebuggerMemory()` 的注释）。如果可能，请避免该调用，因为它的开销较大。

你可以通过 `idautils` 包中的 `cpu` 实例轻松访问所有寄存器：

```python
EAX has the value: "%x" % cpu.Eax
```

从栈顶读取当前值，使用类似：

```python
TOS: "%x" % Dword(cpu.Esp)
```

标签：[ida](上一个问题) [下一个问题), [debuggers](上一个问题) [下一个问题)

# Q：如何在 IDA Pro 中显示内存区域的内容？

标签：[ida](上一个问题) [下一个问题), [tools](上一个问题) [下一个问题)

这是一个关于 IDA Pro 的非常基础的问题。一旦 IDA 调试器启动，我希望能够输入内存地址（或内存区域）并轻松地查看其内容（各种格式）。在 gdb 中，你会使用 `print /x *0x80456ef`，如果你想要更宽的区域，则使用 `x /6x 0x80456ef`。

标签：[ida](上一个问题) [下一个问题), [tools](上一个问题) [下一个问题)

用户：perror

[回答] 由 [newgre]

IDAPython（文档）你可以这样做来打印字节/双字：

```python
Dword(0x80845ef)
Word(0x80845ef)
Byte(0x80845ef)
```

或者，打印任意数量的字节：

```python
for b in GetManyBytes(0x4013E, 10):
    print("%X" % ord(b))
```

如果在调试器中运行，这样调用：

```python
GetManyBytes(0x4013E, 10, True)
```

[回答] 由 [rolf-rolles]

你也可以将光标置于代码、十六进制视图或栈窗口之一中，并按“g”弹出“跳转到地址”对话框。

标签：[ida](上一个问题) [下一个问题), [tools](上一个问题) [下一个问题)

# Q：如何获取未 SDK 覆盖的 IDA 数据库事件通知？

标签：[ida](上一个问题) [下一个问题)

在上一个问题中我问了这个问题，但由于这个方面被忽视了，我不得不问。SDK 中有某些未覆盖的事件。我该如何获取未 SDK 覆盖的 IDA 数据库事件通知？

# Q：跟踪函数返回值的处理情况

我写了一个简单的插件，在函数调用后，寻找 `mov MEM_LOCATION eax` 并为存储返回值的内存添加名称。我将搜索限制为仅……（注：提供的 OCR 文本在末尾截断了，我已根据提供的内容流进行了清理。）

在函数调用后有几条指令，如果在存储返回值之前我看到另一个调用，就退出。除了这些启发式方法外，是否有更严谨的方法来追踪返回值的去向？

标签：ida (上一个问题) (后一个问题)

用户：[user2142] 

[回答] 来自 rorff-roles: 这被称为“数据流分析”（data flow analysis）。例如，Hex-Rays 将函数调用的返回位置信息整合到它的函数表示中，以确定数据流向哪些其他位置。你无法获得关于想如何使用这些信息的大量细节，但凭我直觉，我可能会认为写一个 Hex-Rays 插件可能是值得的。

[回答] 来自 0xea: 那个问题的通用名称是“数据污染分析”（Data Tainting）。你将某些数据标记为受污染，然后在代码的其余部分跟踪污染的传播。关于污染分析有大量的研究，也有相当多的工具。看一眼 bitblaze（它已经不可用且过时了……），它有一部分用于污染跟踪。

如果你需要更偏向于“轻量级”的，可以看看 auto bsdamon 的 VDT，它更偏向于漏洞开发，但可能会给你一些关于它是如何工作的思路。VDT 实际上的操作和你所做的非常相似，但它是反向的。给定一个执行轨迹，你可以从某个值进行反向搜索，查看它是如何被初始化的、在哪里被使用的、以及影响了哪些代码。

对于更多学术方法，请查看《关于动态污染分析和正向符号执行你想的一切》。

这一切都是关于动态分析的，有些更简单的工具可以静态实现。我目前想不起任何具体的例子或工具。我确定有人会提出更多工具和想法的。

标签：ida (上一个问题) (后一个问题)

## Q：我如何在 IDA 中更改段的读/写/执行标记位？

标签：ida (上一个问题) (后一个问题)

有时在向 IDA 中手动加载二进制文件时，你会得到一些具有未知读、写和执行标记的段。你可以在“段”（Segments）子视图（`Shift + F7`）中看到它们。是否有方法可以在 IDA 的 GUI 中更改这些标记，而不是运行脚本并修改它们？

这似乎是一个非常基础的功能，但对于 Hex-Rays 反编译器的正常运行非常重要。我一直在使用该类来表示段权限，考虑到这些标记已经存在，这似乎有些多余。

虽然我希望这个问题能在通用情况下得到解答，但在这种特殊情况下，我处理的是代码和数据混杂的 ARM 二进制文件。所有页级权限都是软件在加载时通过直接映射 MMU 自动设置的。

标签：ida (上一个问题) (后一个问题)

用户：peter-andersson

回答来自 jason-geffner：

我不知道 GUI 内置了什么功能功能可以允许你更改段权限，但你可以轻松地使用 IDC 更改段权限。

来自 IDA 帮助文件：
