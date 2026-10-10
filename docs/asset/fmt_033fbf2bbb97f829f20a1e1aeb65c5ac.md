
后续标记标识了每一行发生了什么。例如，`AS` 表示调用了汇编器，`GZIP` 表示压缩，以此此类推。通常，这些对象模块特定于特定的架构（ARM/XScale），包含了引导内核的底层实用程序。

插图将帮助你理解这种结构和后续讨论。图 5-1 显示了构建可引导镜像过程中的组件演变。后续章节将详细描述。

### 表 5-1 ARM/XScale 对象

| 组件 | 描述 |
| :--- | :--- |
| vmlinux | ELF格式内核主体，包括符号、注释、调试信息（如果使用了 -g）和架构通用组件。 |
| System.map | vmlinux 的文本内核符号表。 |
| .tmp_System.map | 仅用于检查 System.map；否则用于最终构建镜像。 |
| Image | 二进制内核模块，去除了符号和注释。 |
| head.o |  ARM 处理器的通用启动代码。此对象由启动加载程序传递控制权。 |
| piggy.gz | 使用 gzip 压缩的镜像。 |
| piggy.o | 汇编语言格式的文件 piggy.gz，以便与后续对象 misc.o 链接（见正文）。 |
| misc.o | 解压缩内核镜像 (piggy.gz) 的程序，以及熟悉的启动信息 Uncompressing Linux . . . Done 的来源。 |
| head-xscale.o | 针对 XScale 处理器的处理器初始化。 |
| big-endian.o | 将 XScale处理器切换到大端模式的微型汇编内核程序。 |
| vmlinux | 复合内核镜像。这是一个非常遗憾的命名，与内核主体的名称重复；两者不同。该二进制文件是内核主体在此状态下与对象链接后的结果。参见正文解释。 |
| zImage | 由启动加载程序加载的复合镜像。见后续文本。 |

## 5.1 复合内核镜像：Piggy 与小伙伴 103

![](img/01fe6847ecb41916a11c291e01f06c00_138_0.png)

图 5-1 复合内核镜像的构建

### 5.1.1 Image 对象

在构建 `vmlinux` ELF 文件后，内核构建系统继续处理表 5-1 中描述的目标 `Image` 对象由 `vml-linux` 对象创建。`Image` 基本上是去除了冗余符号（注释和备注）的 `vmlinux` ELF 文件，并且去除了其中可能存在的任何调试符号。使用以下命令执行此操作：

```bash
xscale_be-objcopy -O binary -R .note -R .note.gnu.build-id -R .comment -S vmlinux arch/boot/Image
```

`-O` 选项告诉 `objcopy` 生成二进制文件；`-R` 选项移除名为 `.note`、`.note.gnu.build-id` 和 `.comment` 的 ELF 段；`-S` 选项是剥离调试符号的标志。注意，`objcopy` 以 `vmlinux` ELF 镜像作为输入并生成名为 `Image` 的目标二进制文件。总而言之，`Image` 仅仅是从 ELF 转换为二进制格式并剥离了调试符号以及上述 `.note*` 和 `.comment` 段的内核本身。

### 5.1.2 架构对象

继续后续构建序列，编译了许多小模块。每个模块包含几个汇编文件（`head.o`、`head-xscale.o` 等），用于执行低层架构和特定于处理器的任务。这些对象都总结在表 5-1 中。特别注意的是创建名为 `piggy.o` 对象的序列。首先，`Image`（二进制内核镜像）使用此 gzip 命令进行压缩：

```bash
cat Image | gzip -f -9 > piggy.gz
```

这创建了一个名为 `piggy.gz` 的新文件，它仅仅是二进制内核 `Image` 的压缩版本。接下来的步骤非常有趣。汇了一个汇编文件 `piggy.S`，它包含了对压缩后的 `piggy.gz` 的引用。从本质上说，二进制内核镜像被作为载荷（payload）附加到一个低层汇编引导加载器（bootstrap loader）中。该引导加载器初始化处理器和所需的内存区域，解压二进制内核镜像，将其加载到系统内存的正确位置并将控制权交给它。列表 5-2 完整重现了 ...arch/arm/boot/compressed/piggy.S。

# 列表 5-2 汇编文件 Piggy.S

```assembly
.section piggydata, #alloc
.global  input_data
input_data:
  .incbin "/arch/arm/boot/compressed/piggy.gz"
  .global  input_data_end
```

这个简单的汇编文件产生了一种并不显而易见的复杂性。该文件的目的是让汇器将二进制内核镜像输出名为 `.piggydata` 的 ELF 段。它是通过 `.incbin` 汇编预处理器指令触发的，可以将其视为汇器版本的 `#include` 文件，不同的是它期望的是二进制数据。总之，该汇编文件的最终结果是将压缩的二进制镜像作为载荷包含在另一个镜像——引导加载器中。注意标签 `input_data` 和 `input_data_end`。引导加载器使用它们来识别二进制载荷（内核镜像本身）的边界。

> 不要与启动程序（bootloader）混淆，引导加载器可以被视为第二阶段加载器，而启动程序本身可以被认为是第一阶段加载器。

### 5.1.3 引导加载器 (Bootstrap Loader)

不要与启动程序混淆，许多架构使用引导加载器（或第二阶段加载器）将 Linux 内核镜像加载到内存中。某些引导加载器会对内核镜像进行校验和，并解压和重定位内核镜像。在这里，启动程序和引导加载器的区别在于：启动程序在上电时控制板，完全不依赖 Linux 内核。相反，引导加载器的主要作用是作为裸机启动程序与 Linux 内核之间的胶水。引导加载器的责任是为内核运行提供适当的环境，并执行解压和重定位内核二进制镜像的必要步骤。这与 PC 架构中发现的主、次加载器的概念类似。

图 5-2 明确了这一概念。引导加载器与内核镜像连接在一起进行加载。

![](img/01fe6847ecb41916a11c291e01f06c00_140_0.png)

图 5-2 用于 ARM XScale 的复合内核镜像

106 第 5 章内核初始化

在我们研究的示例中，引导加载器由图 5-2 所示的二进制镜像组成。该引导加载器的功能包括：

- 低层汇编语言处理器初始化，包括启用处理器的内部指令和数据缓存、禁用中断以及设置 C 运行时环境。这些包括 `head.o`、`head-xscale.o`。
- 解压缩和重定位代码，体现在 `misc.o` 中。
- 其他特定处理器的初始化，例如 `big-endian.o`，它为此特定处理器启用大端模式。

值得注意的是，我们检查的细节适用于 ARM/XScale 内核实现。每个架构都有不同的细节，尽管概念是相似的。使用与此处类似的分析，你可以学习你自己的架构的要求。

### 5.1.4 启动消息

也许你见过 PC 工作站启动如 Red Hat 或 SUSE Linux 等桌面 Linux 发行版。在 PC 自身的 BIOS 消息之后，你会看到 Linux 在初始化各种内核子系统时显示出一系列控制台消息。输出的大部分在不同的架构和方法之间是通用的。两个最有趣的早期启动消息是内核版本和稍后描述的内核命令行。列表 5-3 重现了 AD Engineering Coyote Platform 在 Intel XScale IPX425 处理器上启动 Linux 的内核启动消息。列表已通过行号格式化。

# 列表 5-3 IPX425 启动消息

```
1 Using base address 0x0010000 and length 0x001cell14
2 Uncompressing Linux....... done, booting the kernel.
3 Linux version 2.6.32-07750-0-82ea67
```
（注：列表 5-3 的 OCR 文本在提示中是不完整的，我仅包含存在的内容。）

## 列表 5-3 继续

```
50 在 MTD 设备 IPX4XX-Flash.0 上找到 5 个 RedBoot 分区
51 在 "IPX4XX-Flash.0" 上创建 5 个 MTD 分区：
52 0x000000000000-0x000000600000 : "RedBoot"
53 0x000001000000-0x000002600000 : "MyKernel"
54 0x000003000000-0x000009000000 : "RootFS"
55 0x00000fc0000-0x0000ffc1000 : "RedBoot config"
56 0x00000fe00000-0x0000010000 : "FIS directory"
57 e100: Intel(R) PRO/100 Network Driver, 3.54-k2-NAPI
```
