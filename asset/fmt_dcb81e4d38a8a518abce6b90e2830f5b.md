
在工程化从 C++ 编译的二进制文件时，对虚表（vtables）中的函数指针进行间接调用是很常见的，必须始终意识到此指针预期的对象类型，有时它还是类层次的一部分。在静态分析的背景下，你使用哪些工具或注释来使反汇编中的虚函数更容易跟踪？欢迎提供所有静态分析工具的解决方案。

用户：user35457 回答：igor-skochinsky

我在 2011 年在 Recon 上做过演讲（“实用逆向工程”）。在静态分析的背景下，你使用哪些工具或注释来使反汇编中的虚函数更容易跟踪？欢迎提供所有静态分析工具的解决方案。此外，我还会编写一些小的 IDC 或 Python 代码段来处理我正在逆向的二进制文件的特定操作，例如解析自定义符号表，或将某些特定的字节序列转换为代码。这些代码通常不会被重复使用。

听起来你需要的节点组（node groups）。从最早的实现（5.0）开始，IDA 的图形视图就允许将几个节点分组为一个带有自定义标题的“超级节点”（super-node）。使用 Ctrl-点击选择你想要分组的节点，并在右键菜单中选择“Group nodes”（分组节点）。

更多更多信息，请参阅 IDA 帮助文档或在线帮助中的“Graph node groups”（图形节点组）。

标签: ida (Prev Q) (Next Q)

## Q：如何在 IDA 中将任意地址映射到其对应的基本块（basic block）？

标签: ida (Prev Q) (Next Q)

假设我有一个任意地址，想找到它对应哪一个基本块（即 `area_t`）。我该如何做呢？

编辑：更具体地说，我想知道给定地址所属的基本块的起始地址 / 结束地址。

标签: ida (Prev Q) (Next Q)

用户：newgre

回答来自 dcoder

我在 `File > Python command...` 对话框中快速编写了这段代码：

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

请记住，IDA 的基本块地址是“startEA 包含，endEA 不包含”。

回答来自 newgre

正如 DCoder 所建议的，我使用了了以下辅助类来高效地将地址解析为基本块：

```python
## 用于对排序后的基本块的操作器。
class BBWrapper(object):
    def __init__(self, ea, bb):
        self.ea_ = ea
        self.bb_ = bb

def get_bb(self):
    return self.bb_

def __lt__(self, other):
    return self.ea_ < other.ea_

# 为给定函数中的所有块创建一个基础缓存。
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

可以这样使用：

```python
bb_cache = BBCache(idaapi.get_func(here))
found = bb_cache.find_block(here)
if found:
    print("found: %X - %X" % (found.startEA, found.endEA))
else:
    print("No basic block found that contains %X" % here)
```

标签: ida (Prev Q) (Next Q)

# Q：IDA 转换为 Unicode ↩

标签: ida (Prev Q) (Next Q), encodings (Next Q)

在 IDA 5.0 免费版中，如何将一个区块数据转换为 unicode 字符串？我能找到的方法是将其转换为 ascii 字符串。

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

转换为

unicode <abcd>, 0

标签: ida (Prev Q) (Next Q), encodings (Next Q)

用户：avery3 ↩

回答来自 rolf-rolls ↩

按下 Alt-A 弹出“string style”（字符串样式）对话框，通过该对话框，你可以创建各种类型的字符串（包括 Unicode）。通过此对话框，你可以选择设置按下按键时创建的默认字符串类型（也就是说，你可以设置让 Unicode 成为默认值）。

或者，正如 joseankoret 在评论中指出的那样，使用 Alt+A+U。

回答来自 ekse

选择第一个字节，Edit -> Strings -> Unicode。

标签: ida (Prev Q) (Next Q), encodings (Next Q)

# Q：你能为 IDA Pro 列出一些好插件和脚本吗？

标签: ida (Prev Q) (Next Q)

我刚开始使用 IDA Pro。在与社区讨论后，似乎 IDA Pro 插件和脚本对于在分析程序时达到良好的生产水平非常重要。

对于日常使用，你推荐哪些 IDApro 必须具备的插件？

标签: ida (Prev Q) (Next Q)

用户：perror

回答来自 peter

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

### Visual Studio

用于 Visual Studio 的逆向辅助插件。

- C++

### GCC

使用 GCC 编译的程序的逆向辅助插件。

- Delphi

### Delphi

使用 Delphi 编译的程序的逆向辅助插件。

- Borland

### Borland

使用 Borland 编译的程序的逆向辅助插件。

- C++ Builder

### C++ Builder

使用 C++ Builder 编译的程序的逆向辅助插件。

- IDC

### IDC

使用 IDC 编译的程序的逆向辅助插件。

- SEH

### SEH

使用 SEH 编译的程序的逆向辅助插件。

- RPC

### RPC

使用 RPC 编译的程序的逆向辅助插件。

- COM

### COM

使用 COM 编译的程序的逆向辅助插件。

- IDL

### IDL

使用 IDL 编译的程序的逆向辅助插件。

### 技术（Technology）

用于特定技术的逆向辅助插件。

- cryptography

### 加密（Cryptography）

用于特定加密的逆向辅助插件。

- obfuscation

### 混淆（Obfuscation）

用于特定混淆的逆向辅助插件。

- encryption

### 加密（Encryption）

用于特定加密的（Encryption）的逆向辅助插件。

- signature

### 签名（Signature）

用于特定签名的逆向辅助插件。

- script

### 脚本（Script）

用于特定脚本的逆向辅助插件。

- runtime

### 运行时（Runtime）

用于特定运行时的（Runtime）逆向辅助插件。

- constants

### 常量（Constants）

用于特定常量的逆向辅助插件。

- hash

### 哈希（Hash）

用于特定哈希的逆向辅助插件。

- disassembly

### 反汇编（Disassembly）

用于特定反汇编的逆向辅助插件。

- function

### 函数（Function）

用于特定函数的逆向辅助插件。

- block

### 块（Block）

用于特定块的逆向辅助插件。

- cache

### 缓存（Cache）

用于特定缓存的逆向辅助插件。

- flow

### 流程（Flow）

- sorted

### 排序的（Sorted）

用于特定排序的（Sorted）的逆向辅助插件。

- obfuscated

### 混淆的（Obfuscated）

用于特定混淆的（Obfuscated）的逆向辅助插件。

- dynamic

### 动态（Dynamic）

用于特定动态的（Dynamic）逆向辅助插件。

- static

### 静态（Static）

用于特定静态的（Static）逆向辅助插件。
