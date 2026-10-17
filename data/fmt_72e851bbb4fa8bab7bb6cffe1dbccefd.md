
在此目录下，模块位于 `/kernel`。在 `/kernel/` 目录下有几个子目录，包括 `/drivers`，它包含了声音驱动程序或视频驱动程序的模块。这些子目录用于对你的模块进行分类，使其更容易定位。例如，`kernel/drivers/net` 目录包含以太网网卡的模块，而 `kernel/drivers/sound` 目录包含声音模块。你会注意到 `/dev` 目录中没有 `eth0` 和 `eth1` 等以太网设备的条目，因为它们实际上是 `/etc/modprobe.conf` 文件中定义的内核模块的别名。

## 使用 `/etc/modprobe.conf` 管理模块

如所述，有几个命令可以管理模块。`lsmod` 命令列出当前加载到内核的模块，`modinfo` 提供特定模块的信息。虽然你可以使用 `insmod` 和 `rmod` 命令加载或卸载模块，但这些任务你应该只使用 `modprobe`。然而，给定模块通常需要加载其他模块。例如，Sound Blast 卡模块 `sb_o` 需要 `sound.o` 模块。

## `depmod` 命令

不要手动尝试确定给定模块依赖哪些模块，而是使用 `depmod` 命令生成一个列出给定模块依赖的所有模块的文件。`depmod` 命令生成一个分级列表，说明应该加载哪些模块以及按什么顺序加载。要加载模块，你使用该文件的 `depmod` 命令。`modprobe` 读取 `depmod` 生成的文件以及你所需的任何依赖模块的正确的顺序。在使用 `modprobe` 之前，你需要带有 `-a` 选项执行 `depmod`。输入 `depmod -a` 创建所有模块依赖的完整列表。这会在当前内核版本的模块目录 `/lib/modules/version` 中创建一个名为 `modules.dep` 的文件。

```
depmod -a
```

## `modprobe` 命令

要手动安装模块，你使用 `modprobe` 命令和模块名。你可以添加模块可能需要的任何参数。以下命令安装了 Intel 高定义声音模块。`modprobe` 还支持使用 `*` 字符，允许你可以使用模式来选择多个模块。此示例使用了多个用于声卡的常用值。你应该使用针对你系统中的声卡的推荐值。大多数声音驱动程序都由 ALSA 项目支持。检查你的网站以查找你的显卡使用的是哪种驱动模块。

```
modprobe snd-hda-intel
```

要发现模块接受哪些参数，可以使用带有 `-p` 选项的 `modinfo` 命令。你可以使用 `-l` 选项列出模块并使用 `-t` 选项在指定的子目录下查找模块。声音模块排列在不同的子目录 `pci`、`isa` 或 `usb` 中。大多数内置声卡使用 `pci`。在接口目录下，可能会像 `snd_em16` 这样的目录，用于 Creative Audio 卡和高定义驱动。在下一个示例中，用户列出 `sound/pci/hda` 目录中的模块：

```
# modprobe -l -t sound/pci/hda
/lib/modules/2.6.15-1.3059_FC7/kernel/sound/pci/snd-hda-intel.o
/lib/modules/2.6.15-1.3059_FC7/kernel/sound/pci/snd-hda-codec.o
/lib/modules/2.6.15-1.3059_FC7/kernel/sound/pci/soundcore.o
/lib/modules/2.6.15-1.2054_FC5/kernel/drivers/sound/sound.o
```

`modprobe` 命令的选项放置在 `/etc/modprobe.conf` 文件中。在这里你可以配置选项，例如默认目录和别名。例如，以下条目允许你将 `3c59x.o` 以太网模块引用为 `eth0`（Kmod 自动检测 3Com 以太网卡并加载 `3c59x` 模块）：

`alias eth0 3c59x`

在 Nvidia 系统上，强制执行为：

`alias eth0 forcedeth`

## `insmod` 命令

`insmod` 命令执行模块的实际加载。`modprobe` 和内核模块加载器都可能使用此命令来加载模块。虽然首选 `modprobe`，因为它会检查依赖关系，但你可以用 `insmod` 和 `rmod` 单独加载或卸载特定模块。`insmod` 命令将模块名称作为参数，`rmod` 也是。名称可以是简单的基本名称，例如 `sb.o` 的 `sb`。你可以使用 `-o` 选项指定完整文件名。其他有用的选项是 `-p` 选项（允许你先探测系统）和 `-n` 选项（执行加载以外的所有操作，模拟运行）。`-v` 选项（详细）列出发生的所有操作。在可能需要强制加载模块的情况下，你可以使用 `-f` 选项。在下一个示例中，`insmod` 加载 `sb.o` 模块：

```
# insmod -v sb
```

## `rmmod` 命令

`rmmod` 命令执行模块的实际卸载。它是 `modprobe` 和内核模块加载器（Kernel Module Loader）用于卸载模块的命令。只要某个模块没有被使用或被其他模块需要，你就可以使用 `rmmod` 命令移除该模块。你可以使用 `-r` 选项移除模块及其所有依赖模块。使用 `-a` 选项移除所有未使用的模块。使用 `-e` 选项，`rmmod` 会卸载并将任何持久化数据（参数）保存到持久化数据目录中，通常为 `/var/lib/modules/persist`。

## `/etc/modprobe.conf` 文件

模块加载可能需要重命名，并指定加载特定模块时使用的选项。即使在删除或安装模块时，也可能需要运行某些额外的程序或指定其他选项 `/etc/modprobe.conf` 文件支持四种操作：`alias`（别名）、`options`（选项）、`install`（安装）和 `remove`（移除）。

- `alias`：为模块提供另一个名称，用于网络和声音设备。
- `options`：指定特定模块可能需要的任何选项。
- `install module`：使用指定的命令安装模块，让你控制模块的加载。
- `remove commands`：指定在模块卸载时运行的命令。
- `include config-file`：额外的配置文件。

最常见的条目之一是用于网卡的别名。注意，`/dev` 目录下的以太网设备没有设备名称。这是因为该设备名称实际上是 `modprobe.conf` 文件中定义的以太网网络模块的别名（这在之前的版本中称为 `modules.conf`）。如果你添加另一个相同类型的以太网卡，你会在 `modprobe.conf` 文件中为其放置别名。对于第二个以太网卡，你将使用设备名 `eth1` 作为别名。这里显示了一个 `modprobe.conf` 条目：

```
alias eth1 ne2k-pci
```

> 提示：更改 `/etc/modprobe.conf` 后，你应该再次运行 `depmod` 以记录模块依赖项的任何更改。

如果你有不同型号的以太网卡，你将不得不指定用于该类型显卡的模块。在以下示例中，第二块卡是标准的 PCI Realtek 卡。Kmod 已经自动检测到新显卡并为你加载了 `ne2k-pci` 模块。你只需要在 `/etc/modprobe.conf` 文件中将其识别为 `eth1` 卡即可。

```
alias eth0 forcedeth
alias eth1 ne2k-pci
```

# 第 32 章：设备与模块：udev、HAL 和 MAKEDEV

**注意**：与其使用单个 `modprobe.conf` 文件，`modprobe` 配置可以使用 `/etc/modprobe.d` 目录下的单独文件来实现。

这里显示了一个示例 `modprobe.conf` 文件。注意 Nvidia Serial ATA 控制器 `sata_nv` 和 AMD 并行 ATA 适配器 `pata_amd` 的别名。它们都被别名为 SCSI 适配器、Fire 控制器和声卡。在最后的安装和删除操作中，声卡通过模块名 `snd-hda-intel` 被引用。最后两行是一行，以 `remove` 开头。

```
alias eth0 forcedeth
alias eth1 ne2k-pci
alias scsi hostadapter sata_nv
alias scsi hostadapter pata_amd
alias snd-card-0 snd-hda-intel
options snd-card-0 index=0
options snd-hda-intel index=0
remove snd-hda-intel - /usr/sbin/alct store 0 >/dev/null 2>&1 || || ;
/bin/modprobe -r --ignore-remove snd-hda-intel
```
