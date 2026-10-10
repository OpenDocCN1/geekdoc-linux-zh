

## 4.5.1 延伸阅读建议

Linux 内核 HOWTO：
www.tldp.org/HOWTO/Kernel-HOWTO

内核 Kbuild 文档：
http://sourceforge.net/projects/kbuild/

Linux 文档项目：
www.tldp.org/

*工具接口标准 (TIS)* 可执行与链接格式 (*ELF*) 规范，版本 1.2
*TIS* 委员会，1995 年 5 月

Linux 内核源码树：
`…/Documentation/kbuild/makefiles.txt`

Linux 内核源码树：
`…/Documentation/kbuild/kconfig-language.txt`

*Linux 内核开发*，第 2 版
Robert Love
Novell 出版社，2005 年

# 第 5 章

![](img/7a1144833e62564667e7dd9eb4c9f03d_130_0.png)

## 内核初始化

### 本章内容
- 复合内核镜像：Piggy 及其伙伴 ... 第 100 页
- 控制流的初始化过程 ... 第 109 页
- 内核命令行处理 ... 第 114 页
- 子系统初始化 ... 第 121 页
- init 线程 ... 第 123 页
- 本章小结 ... 第 128 页

当嵌入式 Linux 系统通电时，会启动一系列复杂的事件序列。几秒钟后，Linux 内核开始运行，并根据系统 init 脚本的指定生成了一系列应用程序。这些活动的重要组成部分由系统配置管理，并受嵌入式开发者的控制。

本章考察 Linux 内核初始事件序列。我们将详细查看内核初始化过程中使用的机制和进程。我们将描述 Linux 内核命令行及其在启动时用于定制 Linux 环境的用法。借助这些知识，您将能够定制和控制初始化序列，以满足您特定嵌入式系统的要求。

## 5.1 复合内核镜像：Piggy 及其伙伴

在嵌入式系统上电时，引导加载程序首先获得处理器控制权。在引导加载程序完成一些低级别硬件初始化后，控制权传递给 Linux 内核。这可以是手动的事件序列，以便于开发过程（例如，用户在引导加载程序提示符处输入交互式 load/boot 命令），也可能是典型生产环境中的自动化启动序列。我们专门在第 7 章“引导加载程序”中讨论了这一主题，因此将有关引导加载程序的详细讨论推迟到该章节。

在第 4 章“Linux 内核：不同的视角”中，我们考察了构成 Linux 内核镜像的组件。请记住，为每种架构构建的常见文件之一是名为 vmlinux 的 ELF 二进制文件。这个二进制文件就是单体内核本身，也就是我们所说的内核主体。实际上，当我们查看 vmlinux 链接阶段的构建时，我们指出了可能查找第一行代码的位置。在大多数架构中，它位于一个名为 head.S 或类似名称的汇编语言源文件中。在内核的 PowerPC (ppc) 分支中，根据处理器不同，存在多个版本的 head.S。例如，AMCC 440 系列处理器由名为 head_44x.S 的文件初始化。

某些架构和引导加载程序能够直接引导 vmlinux 内核镜像。例如，基于 PowerPC 架构和 U-Boot¹ 引导加载程序的平台通常可以直接引导 vmLinux 镜像（稍后您会看到，这是从 ELF 转换为二进制格式之后的结果）。在其他架构和引导加载程序组合中，可能需要额外的功能来设置适当的上下文，并提供加载和引导内核所需的实用工具。

列表 5-1 详述了基于 ADI Engineering Coyote 参考平台（包含 Intel IXP425 网络处理器）的硬件平台²内核构建过程的最后步骤序列。此列表使用内核构建系统的安静输出形式，这是默认设置。如第 4 章所述，这是一种有用的简写符号，允许更多关注构建过程中的错误和警告。

```
$ make ARCH=arm CROSS_COMPILE=xscale_be_ zimage
many build steps omitted for clarity
LD
SYMAPP
OBJCOPY
Kernel:
AS
GZIP
AS
CC
AS
LD
OBJCOPY
Kernel:
Building modules (stage 2):
```

### 列表 5-1 最终内核构建序列：ARM/IXP425 (Coyote)

在列表 5-1 的第三行中，vmlinux 镜像（内核主体）被链接。随后，处理了许多额外的目标模块。其中包括 head.o、piggy.o 和特定于架构的 head-xscale.o 等。（标签标识了每一行发生了什么。例如，AS 表示调用汇编器，GZIP 表示压缩，等等。）一般来说，这些目标模块特定于给定架构（在本例中为 ARM/XScale），并包含在此特定架构上引导内核所需的低级别实用程序例程。表 5-1 详述了列表 5-1 中的组件。

### 表 5-1 ARM/XScale 低级别架构对象

| 组件 | 功能/描述 |
|---|---|
| vmlinux | 内核主体，ELF 格式，包含符号、注释、调试信息（如果使用了 -g 编译）和架构通用组件。 |
| System.map | vmlinux 模块的基于文本的内核符号表。 |
| Image | 二进制内核模块，剥离了符号、注释和说明。 |
| head.o | 特定于 ARM 处理器的 ARM 通用启动代码。引导加载程序将此对象作为控制权的传递目标。 |
| piggy.gz | 使用 gzip 压缩的 Image 文件。 |
| piggy.o | 以汇编语言格式存在的 piggy.gz 文件，以便可以与随后的目标 misc.o 链接（参见正文）。 |
| misc.o | 用于解压缩内核镜像（piggy.gz）的例程，在某种程度上架构中也是熟悉的启动消息 “Uncompressing Linux... Done” 的来源。 |
| head-xscale.o | 特定于 XScale 处理器家族的处理器初始化。 |
| big-endian.o | 一个微小的汇编语言例程，用于将 XScale 处理器切换到大端模式。 |
| vmlinux | 复合内核镜像。请注意，这是一个不幸的命名选择，因为它与内核主体的名称重复；两者并不相同。这个二进制镜像是内核主体与此表中的对象链接后的结果。解释参见正文。 |
| zImage | 引导加载程序加载的最终复合内核镜像。参见下文。 |

> ¹ 如果内核镜像本身需要额外支持，您将需要修改 U-Boot。参见第 7 章“引导加载程序”。
> ² 术语 piggy 最初用于描述“piggyback”（搭便车）概念。在这种情况下，二进制内核镜像搭载在引导加载程序之上，以生成复合内核镜像。

插图有助于您理解这种结构以及接下来的讨论。图 5-1 显示了图像组件及其在构建过程中向可引导内核镜像的演变。以下各部分将详细描述组件和过程。

![](img/7a1144833e62564667e7dd9eb4c9f03d_134_0.png)

### 图 5-1 复合内核镜像构建

### 5.1.1 Image 对象

在 vmlinux 内核 ELF 文件构建完成后，内核构建系统继续处理表 5-1 中描述的目标。Image 对象由 vmlinux 对象创建。Image 基本上是从 vmlinux ELF 文件中剥离冗余部分（注释和说明）以及可能存在的调试符号后的文件。用于此的命令如下：

```
xscale_be-objcopy -O binary -R .note -R .comment -S \
 vmlinux arch/arm/boot/Image
```

在前面的 objcopy 命令中，-O 选项告诉 objcopy 生成二进制文件，-R 选项删除名为 .note 和 .comment 的 ELF 部分，而 -S 选项是剥离调试符号的标志。注意 objcopy 将 vmlinux ELF 镜像作为输入，并生成名为 Image 的目标二进制文件。总之，Image 只不过是二进制形式、剥离了调试符号以及 .note 和 .comment ELF 部分的内核主体。

