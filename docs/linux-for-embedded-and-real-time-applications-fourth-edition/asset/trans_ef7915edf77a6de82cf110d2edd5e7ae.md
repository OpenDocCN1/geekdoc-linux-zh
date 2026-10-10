
选项类型由以下关键字之一指定：

- `bool` — 选项有两个值，“y”或“n”。
- `tristate` — 选项有三个值，“y”、“n”和“m”。
- `choice` — 选项取列表中列出的值之一。
- `int` — 选项取整数值。

类型关键字通常包含一个 `prompt`，即配置菜单中显示的文本。或者，可以使用 `prompt` 关键字来指定提示。还有一些“hidden”（隐藏）选项没有可显示的提示。在 `Kconfig` 的顶部，有一组不会显示在菜单中的选项，因为没有指定提示。这些是当您在 `xconfig` 中选择 **Show All Options** 时看到的选项。

配置条目中的其他关键字包括 `help`（用于指定帮助文本）和 `depends`（意味着如果其所依赖的某个其他选项被选中，该选项才有效或可见）。此外还有 `select`，它表示如果选中了此选项，则必须开启某些其他选项。

在菜单“*System Type*”行的正上方是以下行：

```
source “kernel/Kconfig.freezer”
```

`source` 关键字是扩展配置菜单以合并额外模块化特性的方式。它实际上等同于 C 语言中的 `#include`。您会在主 `Kconfig` 文件中各处发现 `source` 行。

配置语言实际上比这个简单的示例所暗示的要广泛得多。如需更多细节，请查看 `linux/Documentation/kbuild/kconfig-language.txt`。

在下一章中，我们将探讨*集成构建环境*，这是旨在为您构建嵌入式 Linux 系统的一切提供支持的项目。

## 资源

有关配置和构建内核过程的更多详细信息，请查看 `/usr/src/arm-linux/Documentation/kbuild` 中的文件。此外，`www.tldp.org` 上的以下 HOW-TO（操作指南）可能也值得关注：

- `Config-HOWTO`
  - 该操作指南主要关注系统构建完成后如何进行配置。

- `Kernel-HOWTO`
  - 提供有关本章涵盖主题的附加信息。

- `www.linuxfromscratch.org/`
  - 这是一个提供逐步指导的项目，帮助您完全从源代码构建自己的定制 Linux 系统。其中有一个子项目涉及为嵌入式环境交叉构建 Linux。

- `lxr.linux.no`
  - 这可能是我最喜欢用于 Linux 内核的网络资源。它是内核源代码树的超链接和交叉引用版本。几乎每个版本的内核都可获取。您可以查找内核中的任何符号，查看其声明位置及使用情况。您可以跟踪函数调用层次结构，以了解实际发生的事情。它非常棒。

# 第 13 章
集成构建环境

## 章节概要

- 问题 207
- Buildroot 208
- Open Embedded 210
  - OE 元数据 213
  - 测试新镜像：快速仿真器 214
  - 个人观察 214
- Yocto Project 214
  - 使用 Yocto 进行应用开发：软件开发工具包和 Eclipse 215
  - 个人观察 217
- 资源 217

> *它不是嵌入式 Linux 发行版——它为您创建一个定制的发行版*
>
> *引自 Yocto Project 网站*

在本章中，我们将探讨嵌入式 Linux 开发中日益增长的趋势——使用集成构建环境来构建嵌入式 Linux 发行版的全部或部分。

# 问题

嵌入式开发环境中包含许多元素。这些包括但不限于：

- 交叉工具链
  - 编辑器
  - 编译器
  - 链接器
  - 调试器
  - 库
- Bootloader（引导加载程序）
- Linux 内核
- 根文件系统
- 应用程序

让所有这些部分“和谐协作”并非易事。更不用说许可证问题。正如我们在第 1 章“嵌入式和实时领域”中看到的那样，开源软件是在各种具有不同条款的许可下发布的。确保各种许可证之间也能良好协作至关重要。

所有这些部分来自哪里？归根结底，它们来自互联网上的各个角落。这本身很好，但您如何找到它们？

集成构建环境的承诺是将所有这一切汇聚在一个地方。其他人已经完成了在网络中寻找所有这些部件并验证它们是否协同工作的工作。然而，无论这些项目如何实现，它们都有一个共同的特点：一旦完成配置过程，它们都会去互联网下载所需的源代码并构建您指定的组件。由此产生的一个结果是，初始构建通常需要很长时间。后续修改通常不需要很长时间，因为只下载和重新编译少量代码。它们还共享的其他特性：它们使用与内核相同的配置工具，并且拥有用于 Eclipse 的插件。

我们将浏览三个不同的项目。这些项目的网站列在“资源”部分。您可以自由地在工作站上自行跟随步骤，也可以不这样做。

# Buildroot

Buildroot 可能是最简单的集成构建环境。它是一组 Makefile、脚本和补丁，可以构建上述嵌入式 Linux 系统的所有元素，或它们的任意组合。Buildroot 可以自动构建所需的交叉编译工具链，创建根文件系统，编译 Linux 内核镜像，并为目标嵌入式系统构建引导加载程序；或者，它可以执行这些步骤的任意独立组合。

与内核不同，buildroot 的 make help 并不列出它可以构建的默认配置。相反，有一个 make list-defconfigs 目标，并且确实存在针对 BeagleBone 的默认配置。因此，执行 make beaglebone_defconfig。接下来，执行 make xconfig。菜单如图 13.1 所示。

![](img/f03d6fa2c5faefc793771df52bbb2ef9_215_0.png)

**图 13.1**
Buildroot xconfig 菜单。

Buildroot 提供了使用现有工具链而不是从源代码构建新工具链的选项。既然我们有工具链，这似乎是一个明智的选择。在 Toolchain（工具链）类别中，选择 Custom toolchain（自定义工具链）和 Pre-installed toolchain（预安装工具链）。您可以将 Toolchain path（工具链路径）设置为，因为工具链在您的 PATH 中。将 Toolchain prefix（工具链前缀）设置为 arm-unknown-linux-gnueabi。

External toolchain gcc version（外部工具链 gcc 版本）很可能是 4.9.x。在上一章中，我们构建了内核版本 3.8.13，因此您可能会选择 External toolchain kernel headers series（外部工具链内核头文件系列）的 3.8.x。然而事实证明，4.1.x 之前的大部分内容不再受支持，如果您选择它，构建将失败。因此，即使我们已经有 Linux 内核源代码树，如果您想使用 Buildroot，您将不得不选择他们的内核之一。

Buildroot 配置的大部分其余内容涉及选择在目标上安装哪些软件包。您在这里不需要选择太多，因为大多数实用程序将由 Busybox 提供，我们将在下一章详细介绍。

在菜单底部，您可以选择要生成的文件系统镜像类型以及使用何种压缩（如果有）。您还可以配置引导加载程序。我们将在后续章节中介绍 u-boot。完成后，保存配置，然后只需运行 *make*。构建完成后，内核、引导加载程序和文件系统镜像将显示在 *output/images* 中。

# Open Embedded

Open Embedded（简称 OE）可能是对真正的集成构建环境的首次尝试，但其原始实现（现称为 OpenEmbedded-Classic）已被彻底改革。该项目始于合并几个旨在支持运行 Linux 的个人数字助手的项目的努力，包括 OpenZaurus、Familiar Linux 和 OpenSIMPad。

OE 当前的形态称为 OpenEmbedded-Core，简称 OE-Core，它是与稍后我们要看到的 Yocto Project 合并的结果。尽管 OE-Core 仍然是一个活跃的项目，但大部分正在进行的工作是在 Yocto Project 的支持下进行的。特别是，最新的文档就在那里。

> 警告：OE-Core 占用大量磁盘空间。Yocto Project 建议您需要 50 GB 的空闲空间，这些空间当然必须全部位于一个分区中。因此，如果您打算使用 OE-Core 或 Yocto 实际构建某些东西，请确保您有足够的空闲空间。

OE-Core 基于一个用 Python 编写的名为 BitBake 的构建工具。BitBake 的操作可以图形化表示，如图 13.2 所示。它解释（或者如果您喜欢，也可以说是解析）*recipes*（配方）和*configuration files*（配置文件），以确定需要构建什么以及如何构建。然后，它通过网络*fetches*（获取）必要的源代码。输出是一组*packages*（软件包）和文件系统*images*（镜像）。

![](img/f03d6fa2c5faefc793771df52bbb2ef9_216_0.png)

**图 13.2**
BitBake 操作。

