
所以，故障位于 `3c574(attach)`。在本示例中，故障没有导致系统死机，因为故障发生后 `ksym` 还可以建立。在其他情况下，你可能需要以相同的顺序和相同的地址加载多个模块。如果在插入卡时发生故障，请在插入卡之前运行 `ksym`，或者在插入卡的情况下运行。你可以使用 `insmod` 手动加载卡驱动，并在插入卡之前运行 `kms`。更多背景信息请参见 `man inserted`、`man kms` 和 `man klog`。在内核源码树中，`Documentation/ops-tracing.txt` 也有帮助。以下是一些内核调试提示：

- 根据故障，翻译“调用栈（Call Trace）”中的地址可能有用，使用与主故障地址相同的步骤。

- 要诊断静默死机，需要在禁用的情况下触发问题，因为发送到控制台的内核消息将可见。

- 如果你杀死 `klog`，大多数内核消息将直接回显在控制台上，如果问题阻止了 `klog` 写入系统，这可能会有用。

- 为了允许内核消息发送到控制台，对于 2.2 及更高内核，如果 `/proc/sys/kernel/printk` 存在：

```
echo 8 > /proc/sys/kernel/printk
```

会在控制台上打印寄存器转储。即使系统完全没有响应，这可能仍然有效，且 `EIP` 地址可以解释为内核故障。

- 对于启用了 `CONFIG_STTY` 的 2.2 及更高内核，可以通过特殊的 `<Alt><SysRq>` 组合键可以使用应急函数，文档见内核源码树中的 `Documentation/sysrq.txt`。

## 7.3 低级 PCMCIA 调试辅助

PCMIA 模块包含一个条件编译的调试代码列表。这大部分由 `PCMIA_DEBUG` 预处理器定义控制。如果未定义此项，则不会编译调试代码。如果设置为 `0`，则代码被编译但未激活。数字越大，详细程度越高。每个使用 `PCMIA_DEBUG` 构建的模块都将有一个整数参数 `pc_debug`，用于控制输出的详细程度。这可以在模块加载时进行调整，无需重新编译。你的默认 `syslog` 可能会记录这些消息。为了确保它们被记录，请编辑 `syslog.conf`。PCMIA 分布的 `debug_tools` 子目录下有一些寄存器调试工具。用于 ISA 到 PCMCIA 控制器。

## 7.4 /proc/bus/pccard

在 2 及更高内核上，PCMIA 软件包会在 `/proc/bus/pccard` 下创建一个状态信息树。大部分信息只能使用主控制器的数据表来解释。其内容取决于驱动的配置方式，但可能包含全部或部分内容：

`/proc/bus/pccard/{irq,ioport,memory}`

如果存在，这些文件包含了补充内核资源表的资源信息。最近版本的 PCMIA 系统可能会根据配置从即插即用 BIOS 获取额外的资源信息。

`/proc/bus/pccard/drivers`

在最近的中，这列出了所有加载的 PCMCIA 客户端驱动。与 `/proc/modules` 不同，它还列出了可能静态链接到内核的驱动。

`/proc/bus/pccard/*info`

对于每个插槽，这描述了主机及其功能。

`/proc/bus/pccard/*/exca`

这包含了控制器的“ExCA”`Intel i82365sl` 兼容寄存器集。

`/proc/bus/pccard/*/{pci,cardbus}`

对于 CardBus 桥器，这是桥器 PCI 配置空间的转储，以及桥器 CardBus 配置寄存器的转储。

# 7. 调试技巧与编程信息

## 7.5 为新卡编写 Card Services

《Linux PCMCIA 程序员指南》是客户端驱动接口的最佳文档。最新版本可以在 `projects.sourceforge.net` 的 `/pub/pcmia-cs/doc` 中获取，或者在网页 <http://pcmia-cs.sourceforge.net> 上查看。

对于与普通 ISA 设备较相似的设备，你可能可以使用现有 Linux 驱动程序的部分。在某些情况下，最大的挑战将是修改现有的驱动程序，使其能够处理启动后的设备添加和删除。在当前的驱动中，内存卡驱动程序是“自包含”的驱动，它不依赖 Linux 内核的其他部分即可完成大部分的脏活工作。

在很多情况下，支持新卡最大的障碍是从制造商处获取技术信息。弄清楚应该问谁或解释需要哪些信息可能很困难。然而，除少数例外外，如果没有制造商提供的技术信息，为卡实现驱动程序是非常困难甚至是不可能的。

我写了一个带有大量注释的虚拟驱动，解释了驱动程序如何与 Card Services 通信；你可以在 PCMCIA 源码分发的 `clients/dummy_cs.cs` 中找到它。

## 7.6 PCMCIA 客户端驱动作者指南

我决定，将所有 PCMCIA 客户端驱动作为 PCMCIA 软件包的一部分进行分发并不可行。每个新驱动都会让主包的维护变得越来越困难，而且包含驱动程序不可避免地会将部分维护工作从作者转移给我。相反，我将根据用户需求和可维护性，具体决定是否包含贡献的驱动程序。对于未包含在核心包中的驱动，我建议作者采用以下方案对其驱动进行打包分发。

驱动程序文件应该按照 PCMCIA 源码分发相同的目录结构安排，这样驱动程序就可以解压到完整的 PCMCIA 源码树上。驱动程序应该包含源文件（位于 `/modules/`）、一个主页（位于 `/main/`）和文件（位于 `/etc/`）。顶目录还应该包含一个 `README` 文件。

顶目录应包含一个 `Makefile`，其设置应使得 `make -f all` 和 `make -f install` 编译驱动程序并安装所有适当的文件。如果此 `Makefile` 被赋予 `.mk` 扩展名，那么它将被顶层 `Makefile` 为所有的 `all` 和 `install` 目标调用。以下是此类 `Makefile` 的构建示例：

```
# Sample Makefile for contributed client driver
FILES = sample_cs.mk README.sample_cs \
modules/sample_cs.c modules/sample_cs.h \
etc/sample_cs.conf etc/sample_cs.opts \
man/sample_cs.4

all:
install:
	$(MAKE) -C modules MODULES=sample_cs.o
	$(MAKE) -C install-modules MODULES=sample_cs.o
	$(MAKE) -C etc install-clients CLIENTS=sample
	$(MAKE) -C man install-man-4 MAN4=sample_cs.4
```

`dist`:

```
tar czvf sample_cs.tar.gz $(FILES)
```

此 `Makefile` 使用 PCMCIA 软件包 `2.9.10` 及更高版本中的 `install` 目标。为了方便作者，此 `Makefile` 还包含了一个 `dist` 目标。你可能想为最终的包文件名添加版本号（例如 `sample_cs-1.5.tar.gz`）。一个完整的分发如下：

```
sample_cs.nk
README.sample_cs
modules/sample_cs.c
modules/sample_cs.h
etc/sample.conf
etc/sample
etc/sample.opts
man/sample_cs.4
```

通过这种安排，当贡献的驱动被解压时，它会成为 PCMCIA 源码树的一部分。它可以利用 PCMCIA 头文件以及检查用户系统配置的机制和自动依赖检查，就像“正常”的客户端驱动一样。

在这个示例中，`/etc/sample` 和 `/etc/sample.opts` 将是新驱动程序的配置脚本（如果需要），而 `/etc/sample.conf` 将包含对 PCMCIA 卡配置文件的任何添加。从 `3.1.6` 版本开始，`cmmgr` 将自动处理安装在 `/etc/pcmcia` 中的 `*.conf` 文件，因此安装贡献的驱动程序不再需要手动编辑配置文件。

我将接受按照此规范准备的客户端驱动，并将它们放置在 `projects.sourceforge.net` 的 `/pub/pcmia-cs` 目录下。该目录下的 `README` 将描述如何解压非贡献的驱动。

客户端驱动接口随时间推移变化不大，并且始终保持向后兼容。对于主包的微小修订，客户端驱动不需要更新。我将尝试通知贡献驱动的作者关于需要更新其驱动的更改。

## 7.7 Linux 发行版维护者指南

如果你有希望系统配置工具具备 PCMCIA 感知，请使用 `/etc/pcmcia` 中的 `*.opts` 文件，如果用户编译并安装 PCMCIA 软件包的新版本，这些文件不会被修改。如果你修改了配置脚本，全新的安装将静默地覆盖你的自定义脚本并破坏与你的配置工具的连接。如果你不确定如何编写适当的脚本，或者你需要额外的功能，请联系我。
