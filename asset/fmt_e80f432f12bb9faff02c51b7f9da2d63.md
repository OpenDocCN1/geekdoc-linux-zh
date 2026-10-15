
```
coda/

cramfs/

efs/

ext2/

fat/

hfs/

hpfs/

isofs/

jffs/

lockd/

minix/

ncpfs/

nfs/

nfsd/

nls/

msdos/

ntfs/

openpromfs/

qnx4/

ramfs/

romfs/

smbfs/

sysv/

udf/

ufs/

umsdos/

vfat/

net/

802/

appletalk/

atm/

ax25/

bridge/

decnet/

econet/

ethernet/

ipv4/

netfilter/

ipv6/

netfilter/

ipx/

irda/

ircomm/

irlan/

khttpd/

lapb/

netlink/

netrom/

packet/

rose/

sched/

sunrpc/

unix/

wanrouter/

x25/

pcmcia/
```

上面的列表并不是 `/lib/modules/2.4.x/` 目录下所有子目录的详尽列表。你在此处看到的内容将具体取决于你构建和安装的模块。`build` 条目是指向 `/usr/src/linux` 的符号链接。`kernel` 目录包含其下所有模块。`pcmcia` 目录包含符号链接，这些链接指向 `/kernel` 下方各个位置的模块。

在 `kernel` 子目录下方有四个主要子目录：`arch`、`drivers`、`fs` 和 `net`。

`arch` 目录将包含特定体系结构下的模块。像 `cpuid` 和 `apm` 这样的模块将位于 `i386/kernel/` 中。

`drivers` 目录包含众多子目录，但这里的所有模块都与物理硬件相关。如果你能触摸到它，并且为它构建了模块，它就位于 `drivers` 下方的某个位置。

`fs` 目录包含文件系统特定的驱动程序。这些驱动程序处理你编译为模块支持的任何文件系统。通常，这些模块会是 `vfat`、`msdos` 等。

`net` 目录包含所有非基于硬件的网络相关模块。在这里你可以找到 `ipv6` 模块、所有 `netfilter` 模块、内核 `httpd` 模块（`khttpd`）等等。

你可以通过仔细查看内核构建生成的 ``/lib/modules/`uname -r`/modules.dep`` 文件，很好地了解系统上安装了哪些模块。

### 模块版本

默认情况下，重新编译 Linux 内核时，所有要与新内核一起加载的模块也必须重新编译。这可能成为一个繁琐的过程，尤其是当编译内核的系统使用旧硬件时。在较慢的硬件上编译内核可能需要很长时间，因此减少编译所需时间是可取的。

然而，在内核配置过程中，有一个选项可以重用模块而无需重新编译。如果激活以下选项，则会在所有模块上设置版本信息，从而允许非内核模块与任何与其编译时所针对的内核符号版本匹配的内核一起加载：

为所有符号和模块设置版本信息

换句话说，只要模块内的符号也设置为 `2.4.1` 版本，版本为 `2.4.1` 的 Linux 内核就能加载为 `2.4.1` 内核编译的模块。在大多数情况下，这没问题，因为你会使用随内核构建的模块。但如果你没有可用于针对你的内核编译内核模块的源码，例如硬件制造商只随硬件提供二进制模块，你可能需要设置版本信息以便其能够加载。

> **注意**
>
> 内核模块本质上具有两个版本号：一个是*内部*版本号（引用模块内的符号），另一个是*外部*版本号（引用驱动程序作者分配给驱动程序的版本，并反映在符号中）。内部版本号被设置为与编译该模块时所使用的 Linux 内核相匹配。这样就建立了内核/模块之间的关联，从而防止该模块在不同版本的 Linux 内核上加载（这是一个简化的解释）。

这是一个非常有用的特性，尤其是当所使用的模块并非随内核源码一起发布时（例如 OSS Sound）。只要编译该模块时所针对的整体内核版本保持不变，内核源码之外的模块就可以被重用。从 `2.4.1` 内核切换到 `2.2.18` 内核会导致 `2.4.1` 编译的模块加载失败，因为内核的整体版本与模块内的符号不匹配。在这种情况下，会显示以下错误消息：

```
Error: The module was compiled on kernel version 2.4.1.

      This kernel is version 2.2.18. They don't match!

      Check that the module is usable with the current kernel,

      recompile the module and try again.
```

您可能还会收到另一条错误消息，如下所示：

```
Loading failed! The module symbols (from linux-2.4.1) don't match your linux-2.2.18
```
