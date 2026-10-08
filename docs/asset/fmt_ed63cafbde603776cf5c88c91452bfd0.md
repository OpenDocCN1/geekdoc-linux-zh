
找到音频文件 URL 的另一种方法是使用浏览器中的开发者工具检查获取请求（`get requests`）：

# RAINY 让一切变得更好

| 方法 | 名称 | 类型 | 状态 | 大小 | 耗 |
|---|---|---|---|---|---|
| GET | 1111515_803902476978_50738674.png | png | content.cdn.rayman.com | 200 | 0 KB | 0 ms |
| GET | 1111515_803902476979_50738675.png | png | content.cdn.rayman.com | 200 | 0 KB | 0 ms |
| GET | 11093040_446312038063_55155029.png | png | content.cdn.rayman.com | 200 | 0 KB | 0 ms |
| GET | 11093040_446312038061_711334675.png | png | content.cdn.rayman.com | 200 | 0 KB | 0 ms |
| GET | analytics.js | js | www.rayman.com | 200 | 26.27 KB | 10 ms |
| GET | background.png | png | www.rayman.com | 200 | 1.12 MB | 45 ms |
| GET | tunnel.png | png | www.rayman.com | 200 | 0.48 KB | 10 ms |
| GET | opti.gif | gif | www.rayman.com | 200 | 128 KB | 15 ms |
| GET | hero.png | png | www.rayman.com | 200 | 0.48 KB | 20 ms |
| GET | map.png | png | www.rayman.com | 200 | 0.48 KB | 10 ms |
| GET | icon.png | png | www.rayman.com | 200 | 1.00 KB | 10 ms |
| GET | copy.html | html | content.cdn.rayman.com | 200 | 0.04 KB | 5 ms |
| GET | col7.html | html | content.cdn.rayman.com | 200 | 0.04 KB | 5 ms |
| GET | copy.html | html | content.cdn.rayman.com | 200 | 0.04 KB | 5 ms |
| GET | like_this.txt | txt | content.cdn.rayman.com | 200 | 19.61 KB | 10 ms |

![](img/6b9e3d281d03852edd32056c8b57602.png)

# 驱动

## 问题

### Q: 反汇一个驱动

标签：`driver` (上一个问题)

我有几个 Solaris 2.6 驱动想要进行反向工程。我有一个 Sparc 反汇编器，可以得到信息，但它不再维护了，所以我认为它可能无法给我所有可能的信息。这些驱动是用于 Sbus 显卡的，具体来说是早期加速器的 Leo。那么我该如何反向工程这个驱动？我可以反汇编它，但不确定如何输出。此外，最终目标是获得足够的信息来设计一个系统的驱动。NetBSD 有驱动，但硬件文档缺失。此外，Windows 使用 Sbus 接口在 SparcStation 或 UltraSparc 机器上是不实际的。

标签：`driver` (上一个问题)

用户：`cb88`

回答来自 `igor-stoch`

既然是 Solaris 驱动，首先你需要找到关于 Solaris 驱动如何与内核通信的文档。快速搜索

```
_init() 初始化一个加载模块。它在其他加载模块之前被调用。init() 返回 mod_install() 的值。该模块在 mod_install() 调用之前可能会执行一些工作。如果 mod_install() 函数被调用，那么当 mod_install() 返回错误时，应该准备撤销这些操作。
```

```
_info() 返回关于加载模块的信息。info() 返回 mod_info() 的值。fini() 为卸载模块做准备。它在系统想要卸载模块时被调用。如果模块确定可以被卸载，fini() 返回 mod_remove() 的值。在 _fini() 成功返回后，其他程序在 _init() 调用之前被调用。
```

这是一个很好的代码示例。

这个指南似乎也有用。

一旦你找到了入口点，只需跟踪调用和指针即可。它在 IDA 中看起来是这样的：

## 跳过代码块

```
.text:00000000  _init;          ! XREF leo_attach+5A80
.text:00000000                ! leo_attach+5BC
.text:00000000      save             %sp, 0x66, %sp
.text:00000000      sethi            %hi{leo_debug}, %l2
.text:00000000                [leo_debug], %00
.text:00000000      cmp               %08, 4
.text:00000000                loc 38
.text:00000000      sethi            %hi{leo_state}, %00 "! compiled: %s\n"
.text:00000014                aloc{leo.c,63_jun25}, %l0 "! leo.c 6 Jun 25 1997 14:17:56"
.text:00000018      set               %a1746, %00
.text:00000020      sethi            %hi{leo_state}, %00
.text:0000002C      call             leo_print
.text:00000033      call               aj2025197, %02 "! Jun 25 1997"
.text:00000034      sethi            %hi{leo_state}, %00
.text:00000038  loc_38;          ! CODE XREF: _init+54j
.text:00000038                ! _init+0CJ
.text:0000003C      sethi            %hi{0x1800}, %l0
.text:00000040      mov               %l1, %00
.text:00000044      set               %01, %02
.text:00000048      call             ddi_soft_state_init
.text:0000004C      mov               %08, %00
.text:00000050      orcc               %l2{leo_debug & 03FF}
.text:00000053      bne, a            loc 96
.text:0000005C      sethi            %hi{0x1C0}, %l0
.text:00000060      call             leo_init
.text:00000064                ! modlinkage,
.text:00000068      orcc               %08, %00
.text:0000006D      be, a            loc 96
.text:00000070                %l2{leo_debug & 0x3FF}
.text:00000074      call             ddi_soft_state_fini
.text:00000077      mov               %l1, %00
.text:00000080  loc_80;          
.text:00000084      cmp               %09, 4
.text:00000087      nop               loc_9C
.text:0000008C      set               %ae_initDoneRef, %00 "! _init return, return(%d)\n"
.text:00000090      call             leo_print
.text:00000093      mov               %l1, %01
.text:0000009C      ret
.text:000000A      restore
.text:000000A0  End of function _init
```

在 60 处，你可以看到 `mod_init` 调用了一个指向 `modlinkage` 的指针，所以你可以跟进那里查看这些字段指向什么。

但你不需要做所有这些。在这种情况下，程序员们贴心地链接了所有符号和调试信息。这应该对你的工作有所帮助：

根据情况不同，你可能从命名良好的函数（如 `leo_bit_sync_start` 或 `leo_init_ramdac`）开始。我个人更倾向于第一种方法，即自上而下，但人人有之。

编辑：你可以做的一个相当简单的方法是将 `.data` 段开头的 `leo_debug` 变量补丁为 5 左右。这应该产生大量关于驱动程序执行的操作调试输出。

标签：`driver` (上一个问题)

# UPX

跳转到问题，

用户 `cb88` 提供的 Wiki

`UPX` 允许压缩许多不同的可执行格式。执行压缩时，使用了 `UCL` 或 `LZMA` 算法。当使用 `UCL` 时，在许多情况下可执行文件可以在原地解压，而不需要额外的内存消耗。

`UPX` 可以作为第一道混淆，因为可执行文件在分析之前必须先进行解压。

## 问题

### Q：存在哪些不同的 UPX 格式？它们有什么不同？

标签：`upx` (上一个问题)

最近我问了一个关于如何检测 `UPX` 压缩的问题。`0xC000022L` 想知道它是否是原版 `UPX`。然而，在那之前，我只知道过原版 `UPX`。所以我的问题是：

- 存在哪些版本或修改版的 `UPX`？

- 它们有什么不同？它们具有什么特性？

标签：`upx` (上一个问题)

用户：`qbi`

由 `peter-andersson` 回答

我将忽略 `UPX` 中存在多种压缩算法以及存在多个 `UPX` 版本的问题。

通常当人们询问是否为原版或原生 `UPX` 时，是因为恶意软件和其他软件喜欢使用 `UPX` 并对其进行修改，使其无法用标准的 `UPX` 可执行文件解包，从而让反病毒软件更难解包。这对于对抗逆向工程的效果并不理想。

由 `ange` 回答

首先，让我们看看 `UPX` 的结构。

# UPX 结构

1. 头部 (Prologue)

    1. 用于 DLL 参数检查的 `CMP` / `JNZ`

    2. `Pushad`，设置寄存器

    3. 可选的 `NOP` 对齐

2. 解压算法

    * 判断是 `NRV` 还是 `LZMA`

3. 调用/跳转恢复

    * `UPX` 将相对调用和跳转转换为绝对调用，以提高压缩率。

4. 导入表 (Imports)

    * 加载库，解析 API

5. 重置节标志

6. 尾部 (Epilogue)

    - 清理栈

    - 跳转到原始入口点 (`EntryPoint`)

有关更多细节，`这里` 是一个带有注释的 `UPX` 后 `PE` 文件的 `IDA`（免费版）`IDB` 文件。

# 修改过的 UPX 变体

像头部/尾部这样的简单部分很容易修改，因此经常被修改：

- 基础多态：用等效指令替换指令

- 通过跳转移动它们的位置

复杂的部分（如解压、调用恢复、导入加载）通常保持不变，因此通常在它们之间插入自定义代码：

- 反调试

- 一个额外的 `xor` 循环（在解压之后）

- 一个标记，该标记将在解包后的代码中被进一步检查，以便文件知道自己已被解包。

# 伪造 (faking)

由于头部并没有做什么，将其复制到非 `UPX` 压缩的 `PE` 文件的入口点也是容易的，以此欺骗标识符并伪造 `UPX` 压缩。

由 `effortort` 回 回答

我不确定这是否是你问的，但 `UPX` 有多种压缩给定格式的方法。例如，`ELF` - 可以解压到内存中，也可以解压到 `/tmp` 并从那里执行。

默认情况下首选第一种方案，但我认为不是强制性的。详情请参阅 `UPX 手册`。

标签：`[upx]()`(上一个问题)

# 编码

## 问题

### Q：将条码存储为 ASCII

标签：`encodings` (上一个问题)

我目前正在查看一个由显微镜供应商生成的 `TIFF` 文件。他们在 `TIFF` 内部存储了一个 `XML`（`ImageDescription` 标签）。在 `XML` 内部，我可以找到一个 `barcode` 元素。他们没有存储实际的条码（`PDF417`, `DataMatrix`）值，而是存储了其他内容。

我有三个样本，第一个是 `PDF417`，后两个是 `DataMatrix`。解码这些值得到：

1. `04050629C`

2. `H1315015411A`

3. `H1315015412A02`

而 `XML` 元素 `<barcode>` 包含：

1. `MDWNTA2Mj1D`

2. `SDEzMTUwMTUnExEx`

3. `SDEzMTUwMTUnTEyAY`

这是什么编码？

标签：`encodings` (上一个问题)

用户：`malat`

由 `anonymous` 回答

这种编码是 `Base64`。

```
$ echo MDWNTA2Mj1D | base64 -d
04050629C
```

```
$ echo SDEzMTUwMTUnExEx | base64 -d
H1315015411A1
```

标签：`encodings` (上一个问题)

# 解密

跳转到问题，

由 `perror` 回答

解密是对加密消息进行解码的过程（协议、加密算法和密钥）。它与密码分析的不同在于，你应当拥有访问所需的信息。

## 问题

# Q：解密 Windows 8 应用与 Azure 之间的 TLS 数据包

标签：`decryption` (上一个问题)

在 Windows 8 Store 应用开发中，有一个名为 `RemoteSettings` 的类，允许开发者存储批量数据，以便用户可以在多个地方访问。

（注：上述部分的 OCR 文本包含大量重复，已去重。）

# 漏洞分析

## 问题

### Q：漏洞利用开发和漏洞背后的数学背景

标签：`vulnerability-analysis` (上一个问题)

我想了解更多关于漏洞和漏洞利用开发的数学基础的信息。相关的在线资源或书籍将对我很有帮助。

标签：`vulnerability-analysis` (上一个问题)

用户：`viv`

## 回答

我会去读读静态程序分析

静态程序分析是在不实际执行程序的情况下对计算机软件进行的分析（在执行执行的程序上进行的分析被称为动态分析）。在大多数情况下，分析是对某些版本的源代码进行的，在其他情况下是对某些形式的机器代码进行的。

动态程序分析

动态程序分析是通过在真实或虚拟处理器上执行程序对计算机软件进行的分析。为了使动态程序分析有效，目标程序必须带有足够的测试输入执行，以产生有趣的行为。

抽象解释

在计算机科学中，抽象解释是一种关于计算机程序语义的完备近似理论，它基于有序集（格 Lattice）上的单调函数。它可以被看作是对计算机程序的部分执行，在不进行所有计算的情况下获取有关其语义（例如：控制流、数据流）的信息。

符号执行

在计算机科学中，符号执行（也称为符号求值）通过跟踪符号值而非实际值对程序进行分析，这是抽象解释的一种。符号仿真领域将相同的概念应用于硬件。符号计算将该概念应用于数学表达式的分析。符号执行用于推理所有通过程序相同路径的输入。

符号计算

在数学和计算机科学中，计算机代数（也称为符号计算或代数计算）是一个科学领域，指的是研究和开发用于处理数学表达式和其他数学对象的算法和软件。

符号仿真

在计算机科学中，仿真是对某些适当建模的状态转换系统的执行的计算。这通常在离散线性时间帧的各个点上处理系统的完整状态，从其前一个状态顺序计算每个状态。

模型检查

在计算机科学中，模型检查（又属性检查）指的是以下问题：给定一个系统模型，详尽且自动检查该模型是否符合给定的规范。

你可能想读《系统保证：超越漏洞检测》（System Assurance: Beyond Detecting Vulnerabilities）。Rolf 对这个主题可能有非常好的见解。在这里阅读关于他的建议。

`rolf-rolles` 回答

事实证明，大约年前有人在 reddit 上问过大致相同的问题，我当时发布了一个相当详尽的回答，并且在此期间一直在修改它。

标签：`vulnerability-analysis` (上一个问题)

# 模糊测试 (Fuzzing)

跳转到问题，用户 `aperson` 的 Wiki

模糊测试是一种软件测试技术，涉及向计算机程序提供无效、意外或随机数据，然后监控异常、断言失败或内存泄漏。模糊测试可以作为白盒测试、灰盒测试或黑盒测试的一部分。

在逆向工程的背景下，模糊测试通常用于发现未记录的特性或功能，而不是为了寻找后门。

# Q：最先进的模糊测试框架

标签：`fuzzing` (上一个问题)

我之前自己实现过一个模糊测试框架，并尝试过其他的，比如 `Peach Fuzzer`。我已经很久没有看漏洞猎了，但目前模糊测试的水平是什么？也就是说，如果我今天开始对 Acme Corp 的 PDF 阅读器进行模糊测试，我应该研究哪种工具？
