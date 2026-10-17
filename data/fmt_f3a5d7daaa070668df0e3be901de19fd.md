
```
make[1]: Entering directory /usr/src/linux-2.2.1/arch/i386/boot
make[1]: Nothing to do for 'dep'
make[1]: Leaving directory /usr/src/linux-2.2.1/arch/i386/boot
scripts/mkdep init.c
scripts/find /usr/src/linux-2.2.1/include /usr/src/linux-2.2.1/scsi /usr/src/linux-2.2.1/include -not -follow -name *.h -name version*h > .dep
make_kdep _sfdep_drivers _sfdep_mm _sfdep_fs _sfdep_ic _sfdep_lib _sfdep_arch/i386/kernel_sfdep_arch/i386/386_lib _sfdep_lib86 _sfdep_arch/i386/kernel_sfdep_arch/i386/386_lib86-make[1]: Entering directory /usr/src/linux-2.2.1
make -C kernel fastdep
make[2]: Entering directory /scripts/mkdep acct.c.capability.dma.c.exec_domain.c.exist.c.info.c.module.c.panic.c.sched.c.softirq.c.sys.c time.c > .dep
make[2]: Leaving directory /usr/src/linux-2.2.1/kernel
make -C drivers fastdep
make[2]: Entering directory /usr/src/linux-2.2.1/drivers
scripts/mkdep > .dep
```

此步骤创建两个文件：`dep` 和 `h`。这些文件在编译步骤期间使用。`dep` 文件的内容如下：

```
init/main.o:
/usr/src/linux-2.2.1/include/linux/proc_fs.h
/usr/src/linux-2.2.1/include/unistd.h
/usr/src/linux-2.2.1/include/ctype.h
/usr/src/linux-2.2.1/include/delay.h
/usr/src/linux-2.2.1/include/utsname.h
/usr/src/linux-2.2.1/include/ioport.h
/usr/src/linux-2.2.1/include/init.h
/usr/src/linux-2.2.1/include/smp_lock.h
/usr/src/linux-2.2.1/include/blk.h
/usr/src/linux-2.2.1/include/hrdg.h
/usr/src/linux-2.2.1/include/asm/io.h
/usr/src/linux-2.2.1/include/asm/bugs.h
```

```
$wildcard /usr/src/linux-2.2.1/include/config/pci.h) \
/usr/src/linux-2.2.1/include/config/pci.h
$wildcard /usr/src/linux-2.2.1/include/config/dio.h) \
/usr/src/linux-2.2.1/include/dio.h
$wildcard /usr/src/linux-2.2.1/include/config/zorro.h) \
/usr/src/linux-2.2.1/include/zorro.h
$wildcard /usr/src/linux-2.2.1/include/config/mtrr.h) \
/usr/src/linux-2.2.1/include/asm/mtrr.h
$wildcard /usr/src/linux-2.2.1/include/config/apm.h) \
/usr/src/linux-2.2.1/include/apm_bios.h
```

# 清理多余文件（步骤 4）

`clean` 步骤如其名。该步骤删除之前的内核编译期间创建的旧代码和文件。`make clean` 过程片段如下：

```
make[1]: Entering directory /usr/src/linux-2.2.1/arch/i386/boot
rm -f tools/build
rm -f Image compressed vmlinux.out
rm -f bsetup compressed bmlinux
make[2]: Entering directory /usr/src/linux-2.2.1/arch/i386/boot
compressed/
rm -f vmlinux vmlinux_*
make[2]: Leaving directory /usr/src/linux-2.2.1/arch/i386/boot
compressed/
make[1]: Leaving directory /usr/src/linux-2.2.1/include/compile.h
rm -f core/ksym.1 include/dialog/* -print
rm -f core find -name '*.*' -regex '.*dialog/*' -print
rm -f core find -type f -name '*.core' -print
rm -f core find -name '*.flags' -print
rm -f vmlinux System.map
rm -f .*
rm -f drivers/char/consolemap_detbl.c drivers/video/promcon_tbl.c
rm -f drivers/char/conmakehash
rm -f drivers/sound/bin2hex drivers/sound/hex2hex
if [-d modules ]; then
rm -f core find modules/* -type f -print;
fi
```

# 编译内核（步骤 5）

该步骤实际上编译配置步骤中所请求的每个源代码部分。根据系统的速度，并在某种程度上取决于选定的组件，此步骤可能需要一段时间。与内核配置步骤一样，完成此步骤有三种方法：

- `zImage`
- `zdisk`
- `zlImage`

之前的每个步骤都会编译一个新的内核。然而，内核编译之后发生的步骤会有所不同。

## 构建内核

`make zImage`

这是标准步骤，除了编译内核外没有其他操作。如果所有组件都正确编译成功，你可以在 `/usr/src/linux/arch/i386/boot` 目录下找到一个新的内核。该新内核被形象地命名为 `zImage`。当然，这仅仅是一个编译后的内核。你必须配置引导程序（即 `LILO`）以找到新内核并启动。这通常通过将 `zimage` 文件复制到 `/mlinux`，运行 `lilo` 重新安装新的引导程序，然后重启系统来完成。

`make zdisk`

这种方法执行的任务与 `make image` 方法完全相同，但在编译完成后，它会自动将新构建的内核拷贝到软盘中。这块新磁盘可以用于启动系统；随后新内核将处于激活状态。这种方法通常用于在构建内核的系统上测试该内核，或用于在其他硬件上测试内核。

`make zlilo`

这是构建和安装新内核的推荐方法。然而，强烈建议你遵循本章开头概述的步骤。这使你能够在某些功能无法工作时，仍然能够启动原始内核。这种方法与 `make image` 方法完全相同，不同之处在于它会自动执行上述手动列出的步骤。换句话说，在编译完成后，新构建的内核被拷贝到 `/` 目录并命名为 `vmlinux`（同时为原始 `vmlinux` 创建一个备份），然后运行 `lilo` 重新安装引导程序（以识别新内核）。

# 编译可加载模块（第 6 步）

此步骤将配置步骤中标记为模块的所有组件编译为模块。这些模块必须与它们旨在运行的内核相匹配。有关使用可加载模块的更多信息，请参阅第 18 章“内核模块”。

# 安装模块（第 7 步）

此步骤将所有新编译的模块拷贝到 `/lib/modules` 目录，以便它们可以被插入内核。由于模块必须与构建它们时使用的内核配合，OpenLinux 采用了一种特殊方法，在启动时自动加载模块。目前，需要一个手动步骤来确保模块在启动时继续加载。同样，请参阅第 18 章以学习如何完成此任务。

# 重启系统（第 8 步）

这是一个简单的步骤，只需重启即可。有时需要一点信心来相信你配置的内容能够正常，但如果你遵循了“预防性前提”部分中的步骤，即使你新构建的内核无法工作，你可能也可以恢复。

# 第 17 章 构建自定义内核

> 注意：确保你使用了 `make zlilo` 选项，或者在安装新内核后手动运行 `/sbin/lilo`。未能做到这一点（这是一个常见错误）会导致你在尝试启动时发生内核崩溃，因为引导程序无法找到新构建的内核。

## 总结

第一次尝试构建新的 Linux 内核可能看起来很危险，但不要让它阻止你。如果你遵循概述的步骤，当某些功能出现问题时，你可以恢复。有了安全网，你可以尽情探索许多可能的内核配置选项，并构建一个符合你切所需的内核。如需更多信息，请查看以下章节：

- 参阅第 18 章获取有关使用可加载模块而不是直接将支持构建内核的更多信息。
- 参阅第 20 章获取有关引导程序（`LILO`）以及它如何与 Linux 内核工作的更多信息。
- 参阅第 29 章“IP 伪装”，获取有关配置此功能所需的内核组件的更多信息。
- 参阅第 30 章“IP 防火墙”，获取有关内核中启用此功能所需的更多信息。

# 第 18 章 内核模块

# 内核模块

在本章中

- 模块版本 394
- 模块管理 395
- 未包含在内核源码中的模块 399

在诸如 DOS（位于 Windows 的许多版本等环境中）等操作系统中，内核被整合在一起以处理操作系统预期的的大部分低级任务，例如与 CPU 交互、内存管理等。对于那些由于某种原因无法编译到内核本身的项目，内核会用较小的代码块进行补充。

这的一个很好的例子是某件硬件的驱动程序。操作系统制造商如何知道你将在你的系统上使用那个特定的硬件呢？显然，没有任何设的方法可以提前得知这些信息，因此设立了相关机制，允许这些项目在操作系统发行和安装后加载。

在 DOS 系统中，可以通过向 `CONFIG.SYS` 或 `AUTOEXEC.BAT` 文件添加行来安装这些驱动程序和其他可加载的操作系统代码块。在 Windows 等环境中，有 `.INI` 文件可以完成此任务。其他系统有自己的方法，但归根结底都是同一件事：在操作系统安装后可以向其中添加功能和驱动程序。

Linux 也不例外。正如第 17 章“构建内核”所示，在添加硬件或启用新功能时，重新编译内核是一个可行的选项。如果要添加的项目（暂无更好的术语）是永久的，将支持编译到内核中可能是最好的通用选项。

然而，由于现代 Linux 发行版中包含了可加载模块设施，很少需要重新编译内核。通过模块，你只需插入你想要包含的功能或驱动程序并忽略其他部分即可。这节省了内存并允许你添加功能或驱动程序而无需重新编译内核。模块化的另一个优势是可以在重启 Linux 系统的情况下添加这些项目（见图 18）。

# 图 18.1 模块化内核。

![](img/d858127fcfbd31232945905f47a0)

当 Linux 内核编译为各种驱动程序提供模块化支持时，模块本身存储在 `/lib/modules` 下，与其关联的内核版本相匹配。因此，如果 2.2.1 版本编译为对其某些支持的驱动程序使用模块，则模块存储在 `/lib/modules`。这样，如果多个版本的 Linux 内核编译为包含可选加载模块，不同的模块就不会混杂。

模块的分类在 `/lib/modules/2.1` 下进一步细分，以便对逻辑集（见列表 18.1）。

# 列表 18.1 /LIB/MODULES/2.1 下目录

| 目录 |  |
| :--- | :--- |
| block | 各种块设备（如 IDE 硬件：磁带、光驱、移动驱动器）的驱动程序存储在这里。 |
| cdrom | 此子目录包含专的光驱驱动程序（即非 IDE/ATAPI 或 SCSI 的光驱器）。 |
| fs | 支持不同文件系统（NFS、ISO9660 等）的模块在此子目录下。 |
| ipv4 | 提供 TCP/IP 网络服务的模块典型位置，用于 PPP 和 SLIP 拨号网络以及 IP 别名的模块都在第四部分“与 Linux 网络”中讨论。 |
| misc | 当模块不符合其他任何类别时，它就在这里。这里存储的最常见模块是 IBC 模块（Intel Binary Compatibility System），它为 Linux 用户提供了与 SCO Unix 及其其他操作系统变体的一些应用程序的二进制兼容性。在这里还有声卡驱动程序和 PCMCIA 硬件的模块。 |
| net | 来说，如果有一个编译为支持网卡的模块，它就会被放在这里。 |
| scsi | 适用于 SCSI 硬件的各种模块，包括 SCSI 接口卡、硬盘、光驱以及如 CD 和刻字机等 SCSI 通用设备的驱动程序。 |

# 模块版本

默认情况下，在重新编译 Linux 内核时，所有要在新内核加载的模块也必须重新编译。这可能是一个繁琐的过程，特别是当编译内核的系统使用旧式硬件时。在缓慢的硬件上编译内核可能需要很长时间，因此缩短编译所需的时间是非常理想的。

然而，有一种方法可以在不重新编译的情况下用模块：此选项在内核配置过程中可用（见第17章，该章节详细介绍了配置）。如果你激活了以下选项，将在所有符号和模块设置版本信息

所有模块将设置版本信息，这将允许模块加载到与编译模块时的内核版本匹配的任何内核。换句话说，版本为 2.2.1 的 Linux 内核会加载为 2.2.1 内核编译的模块，只要模块内的符号版本也设置为 2.2.1。

> 内核模块本质上有两个版本号：一个是内部的（引用模块内的符号），另一个是外部的（引用驱动作者分配给驱动的版本）。内部版本号被设置为与编译该模块的 Linux 内核匹配。这种设置建立了内核/模块的关联，防止模块被加载到不同版本的 Linux 内核上。

这是一个非常有用的功能，特别是当使用的模块没有随内核源码一起发布时（例如 IBCS、PCMCIA）。只要编译该模块的整体内核版本保持不变，内核源码之外的模块就可以被重复使用。从 2.2.1 内核移动到 2.0.36 内核会导致为 2.2.1 编译的模块加载失败，因为内核的整体版本与模块内的符号不匹配。在这种情况下，会显示以下错误信息：

错误: 模块在内核版本 2.2.1 上编译。

此内核版本为 2.0.36。它们不匹配！

检查该模块是否可以在当前内核中使用，重新编译模块并重试。

你可能收到的另一个错误信息如下：

- 失败! 模块符号（来自 linux-2.2.1）与你的 linux-2.0.36 不匹配

无论何种情况，错误信息都足够详细，让你知道问题所在。为内核重新编译模块（确保在所有模块符号上设置版本），模块即可加载。

# 模块管理

内核模块可以手动加载，也可以自动加载。通常，系统管理员开始从手动加载模块，直到他熟悉该过程（以及他想要经常加载哪些模块）；然后他转为自动加载模块。

熟悉并不是这么做的唯一原因。许多模块在能够成功加载之前需要传递特定的改变行为的参数。如果没有这些参数进行实验并确切找出需要哪些参数，可能会发生几种情况。

有时模块可能会带有错误的设置加载，例如中断和 I/O 端口的设置。这两个设置并没有阻止 3c509 以太网驱动的加载，这看起来是成功添加了对该卡的支持，但实际上是一个虚假信号。

此外，自动探测过程可能会大幅延长系统启动的时间。一个很好的例子是 SoundBlaster CD 光驱驱动程序 (`sbcd.o`)，它在放弃之前会探测一个很长的驱动列表，从而为系统启动时间增加了五到十分钟。

在大多数情况下，如果不传递模块参数，模块根本不会加载。一个恰当的例子是索尼 CDU-31a 驱动 (`cdu31a.o`)，它对硬件完全没有自动探测；因此，除非明确告知，否则它不会加载。

> 区分启动参数和模块参数非常重要。模块参数是在模块加载时传递给内核的，并且仅适用于编译为模块的驱动。启动参数是传递给内核本身的，用于更改直接编译到内核中的驱动程序的行为。启动参数在 LILO 启动时传递（使用 `/etc/lilo.conf` 中的 `append=` 标签）。遗憾的是，一个模块到下一个模块的可选参数几乎没有确定性，除非它们是模块参数——某些参数在模块之间不同。因此，了解你正在自动加载的模块的适当参数可以节省很多麻烦。请参考附录 C“可加载模块参数”获取有关 OpenLinux 系统提供的参数的信息。

# 第 18 章 内核模块

## 手动加载

有三个工具常用于手动加载、卸载和列出模块：

- `insmod`—将模块加载或插入当前加载/运行的内核中
- `rmmod`—移除当前加载的模块
- `lsmod`—列出当前加载的模块

每个工具的语法都相当简单。要插入模块（例如，用于视频采集卡的 `btt` 驱动），执行类似下面的命令：

```
insmod btt
```

在加载后移除模块，运行以下：

```
rmmod btt
```

要获取模块加载时正在发生情况的详细列表，添加 `-v`：

```
insmod -v btt
```

此命令的输出类似于列表 18.2。

### insmod -v btt 的示例输出
