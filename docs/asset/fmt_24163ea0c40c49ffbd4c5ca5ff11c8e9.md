
在基于 `BIOS` 的计算机上，安装 `GRUB Legacy` 的命令是 `grub-install`。在安装引导加载程序时，你必须通过设备名称指定引导扇区。

运行的命令格式如下：

```
# grub-install devsda
```

或者

```
# grub-install '(hd0)'
```

上述任一命令都会将 `GRUB Legacy` 安装到你第一块硬盘的第一个扇区（即 `MBR`）。在第二个示例中，你需要在设备名称周围加上单引号。如果你想将 `GRUB Legacy` 安装在分区的引导扇而非 `MBR`，请包含分区标识，例如 `devsda1(hd0,0)`。

如果你正在安装 `Fedora` 支持 `EFI` 的 `GRUB Legacy` 版本，不应使用 `grub-install` 命令；而是将 `grub.efi` 文件复制到 `ESP` 上的合适子目录下（例如 `bootEFIredhat`），如果使用的是 `Fedora` 的 `grub-efi` `RPM` 包，则复制 `grub.conf`。默认情况下，`grub.efi` 文件位于此位置。拷贝这些文件后，你需要使用 `eibootmgr` 将引导加载程序添加到 `EFI` 列表中：

```
# eibootmgr -c -l \EFI\redhat\grub.efi -L GRUB
```

此命令将存储在 `ESP` 的 `EFIred` 目录下的 `GRUB Legacy` 添加到 `EFI` 引导加载列表中。你必须使用双反斜杠（`\`）而不是 `Linux` 风格的正斜杠（`/`）作为目录分隔符。更多信息请参阅 `eibootmgr` 工具的 `man` 页面。

在更改配置文件后，你不需要重新安装 `GRUB`。（尽管某些较旧的引导加载程序需要这样做。）只有当你对磁盘配置进行某些更改时，才需要以此方式安装 `GRUB`，例如调整大小或移动 `GRUB` 根分区、将整个安装移动到新硬盘，或可能重新安装 `Windows`（这往往会擦除基于 `MBR` 的引导加载程序）。在某些情况下，你可能需要通过备份引导加载程序（例如安装在 `USB` 闪盘上的 `GRUB`）启动 `Linux`。

# 与 GRUB Legacy 交互

`GRUB Legacy` 引导加载程序显示的第一个界面是你在 `GRUB` 配置文件中通过 `title` 选项指定的所有操作系统列表。你可以等待超时以启动默认操作系统。若要选择备用系统，使用方向键高亮你想要启动的操作系统。一旦选中该选项，按下 `Enter` 键开始启动。

当你想要更改或向操作系统传递额外选项时，请遵循以下步骤：

1. 使用方向键高亮最符合你启动意图操作系统。
2. 按 `E` 键编辑此条目。你会看到一个列出该条目所有选项的新屏幕。
3. 使用方向键高亮内核选项行。
4. 按 `E` 键编辑内核选项。
5. 修改内核行以添加任何选项，例如添加 `1` 进入单用户模式。`GRUB Legacy` 会将额外选项传递给内核。
6. 按 `Enter` 键完成编辑。
7. 按 `B` 键开始启动。

你可以在第 5 步进行任何需要的更改，例如使用不同的初始化程序。通过在内核行末尾追加 `init=/bin/bash`（或你想使用的任何程序）来实现。

# 使用 GRUB 2 作为引导加载程序

从原理上说，配置 `GRUB 2` 与配置 `GRUB Legacy` 非常类似；

然而，一些重要的细节不同。首先，`GRUB 2` 的配置文件是 `/boot/grub/grub.cfg`。（某些发行版将此文件放在 `/boot/grub2`，以便同时安装 `GRUB Legacy` 和 `GRUB 2`。）

`GRUB 2` 的进一步改进在于它利用了一系列脚本和其他工具来维护 `grub.cfg` 文件。其意图是让系统管理员永远不需要显式编辑该文件。如果你需要手动更改 `GRUB 2` 配置文件，请编辑 `/etc/default/grub` 文件或 `/etc/grub.d` 文件夹中的文件，然后使用 `update-grub` 或 `grub-mkconfig` 命令（取决于你的 `Linux` 发行版）将更改移动到 `/boot/grub/grub.cfg` 文件。

当你运行 `update-grub` 或 `grub-mkconfig` 命令时，它会将新的 `grub.cfg` 文件输出到标准输出。如果你想保存更改，可以输入 `update-grub` 或 `grub-mkconfig > /boot/grub/grub.cfg`。该命令会重新读取这些配置文件并写入一个全新的 `/boot/grub/grub.cfg` 文件。（某些安装在命令名称中 `grub` 后面带有 2，例如使用 `grub2-mkconfig` 而不是 `grub-mkconfig`。）

![](img/f74c2c51e1985d4d3a6804ba2887d2f4_464_0.png)

不要忘记将 `update-grub` 或 `grub-mkconfig` 命令的输出重定向到 `grub.cfg` 文件。默认情况下，这些命令将配置发送到标准输出，不会改变 `GRUB` 配置。

与 `GRUB Legacy` 不同，`GRUB 2` 设计用于同时支持基于 `BIOS` 和 `EFI` 的计算机，以及一些更奇见的固件类型。当你首次安装 `Linux` 时，安装程序应该正确设置 `GRUB`，以与 `GRUB Legacy` 非常相同的方式使用 `grub-install`。在基于 `EFI` 的计算机上，`GRUB 2` 版本的 `grub-install` 应该将 `GRUB 2 EFI` 二进制文件安装到正确的位置，但如果你遇到问题，可能需要像早些引用 `GRUB Legacy` 时那样使用 `efibootmgr`。

## 使用替代引导程序

尽管 `GRUB Legacy` 和 `GRUB 2` 现在主导着 `Linux` 启动加载器领域，并且是考试涵盖的唯一引导程序，但还有其他你可能会遇到并值得提及的加载器：

### Syslinux

`Syslinux` 项目 (www.syslinux.org) 实际上是一个基于 `BIOS` 的加载器家族，其中每一个都比 `GRUB Legacy` 或 `GRUB 2` 小得多且更专精。该家族最著名的成员是 `ISOLINUX`，它是一个用于光盘的启动加载器，光盘具有独特的启动要求。`EXTLINUX` 引导程序是该家族的另一个成员；它可以从 `ext2`、`ext3` 或 `ext4` 文件系统启动 `Linux`。

### LILO

`LILO` 加载器是 20 世纪 90 年代常用的 `Linux` 启动加载器。按照今天的标准来看，它是原始且有限的，并且仅适用于基于 `BIOS` 的计算机。你可以通过是否存在 `/etc/lilo.conf` 配置文件来判断你的 `Linux` 系统是否使用 `LILO`。有关 `LILO` 的更多信息，请访问 http://freshmeat.net/projects/lilo。

### Linux 内核

从 3.3.0 版本开始，`Linux` 内核已为 `x86` 和 `x86-64` 系统整合了 `EFI` 引导。在基于 `EFI` 的计算机上，此功能允许内核充当自己的引导程序，不再需要像 `GRUB 2` 或 `ELILO` 这样的独立工具。

### rEFIt

该程序托管在 http://refit.sourceforge.net，技术上是一个引导管理器，而不是引导加载。它在基于 `Intel` 的 `Mac` 上很流行，但该程序的某些版本也可以用于基于 `UEFI` 的 `PC`。它提供了一个吸引人的图形界面，使用户可以选择其启动操作系统图标，而不是使用文本界面。`rEFI` 似乎已被遗弃；截至本文编写时，最后一次更新是在 2010 年。

### rEFInd

该程序源自 `rEFI`，以便使其在基于 `UEFI` 的 `PC` 上更有用并扩展其功能集。与 `rEFIt` 一样，`rEFInd` 是一个引导管理器，而不是引导加载。它的目的是向用户显示启动选项列表。它在提供糟糕引导管理器的 `EFI` 实现计算机上最有用。它还提供了设计用于与 `Linux` 内核内置 `EFI` 引导加载器工作的功能，以简化为了让内核启动而所需的选项的传递。你可以在 www.rodsbooks.com/refind/ 了解更多。

### gummiboot

这是一个开源 `EFI` 引导管理器，概念上与 `rEFI` 或 `rEFInd` 相似，但使用文本模式界面和较少的选项。你可以在 http://freesedesktop.org/wiki/Software/gummiboot 了解更多。

虽然基于 `BIOS` 的计算机的 `Linux` 启动加载器在很大程度上已经稳定，`GRUB 2` 现在主导着这一领域，但 `EFI` 引导加载器的开发非常动态。这可能是因为基于 `EFI` 的计算机正变得普遍。
