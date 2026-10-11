

## 配置 LILO

LILO 引导程序存在的时间已经非常久了。LILO 是 “Linux LOader”（Linux 引导器）的缩写。LILO 是一个功能非常灵活的引导程序，它可以用来从计算机硬盘启动几乎任何操作系统，包括 Linux、Windows 或 DOS。

当使用 LILO 作为默认引导程序时，LILO 引导菜单会显示给最终用户，允许他们选择想要启动的操作系统内核。图 6-5 展示了一个 LILO 引导菜单的示例。

> **注意** 许多 Linux 发行版可能会以图形化方式呈现 LILO 菜单，而不是像图 6-5 中那样显示文本菜单。

早期的许多 Linux 发行版都使用 LILO 作为默认引导程序。正因为如此，LILO 可能是部署最广泛的 Linux 引导程序之一。因此，一名优秀的 Linux 管理员需要了解如何与 LILO 协同工作。

> **注意** 虽然 LILO 曾经被广泛使用，但许多当前的 Linux 发行版不再支持 LILO。大多数发行版使用 GRUB 引导程序代替 LILO。

这里我们将探讨以下关于 LILO 的主题：

- 安装 LILO
- 配置 LILO
- 关于 ELILO

让我们首先讨论如何安装 LILO 引导程序。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_231_0.png)

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_231_1.png)

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_232_0.png)

## 安装 LILO

安装 LILO 引导程序有两种不同的方式。首先，对于仍然支持 LILO 的 Linux 发行版，你可以指定在正在安装的系统中使用 LILO 引导程序。例如，在图 6-6 中，openSUSE 安装程序允许你在“引导加载器设置”界面将引导程序从默认的 GRUB 更改为 LILO。

你可以选择将 LILO 引导程序安装在 MBR 中，或者安装在启动分区内。这两种选项似乎工作效果都一样好。你也可以通过先在系统中安装 LILO 软件包，然后在 shell 提示符下输入 `lilo` 命令，将在已经配置了其他引导程序的 Linux 系统上安装 LILO 引导程序。

> **注意** 我们将在本书后面讨论安装软件包。

这将覆盖现有的引导程序并安装 LILO 引导程序。然而，在做此操作之前，你需要先配置 `/etc` 目录下的 LILO 配置文件。接下来让我们讨论如何执行此操作。

## 配置 LILO

LILO 引导程序是通过 `/etc` 目录下一个名为 `lilo.conf` 的文件进行配置的。下面展示了一个来自 SUSE Linux Enterprise Server 10 系统的 `lilo.conf` 文件示例：

```bash
$4: # cat /etc/lilo.conf
menu-scheme = Wb:Kw:Wb:Wb
timeout = 80
lba32
change-rules
reset
read-only
prompt
default = SLES_10_SP3
message = /boot/message
boot = /dev/sda2

image = /boot/vmlinuz-2.6.16.60-0.54.5-emp
###Don't change this comment - YAST2 identifier: Original name: linux##
  label = SLES_10_SP3
  append = "  resume=/dev/sda1 splash=silent showopts"

vga = 0x317
initrd = /boot/initrd-2.6.16.60-0.54.5-smp
root = /dev/sda2

image = /boot/vmlinuz-2.6.16.60-0.54.5-smp
###Don't change this comment - YaST2 identifier: Original name: failsafe###
label = Failsafe
append= "showopts ide=nodma apm=off acpi=off noresume edd=off 3"
vga = 0x317
initrd = /boot/initrd-2.6.16.60-0.54.5-smp
root = /dev/sda2

fs4:~ #
```

第一部分包含适用于文件中所有其他部分的全局选项。最后两部分包含特定于每个菜单项的选项。你可以查阅表 6-1 来了解每个选项的作用。表 6-1 中列出的选项并非包罗万象。你在 `/etc/lilo.conf` 文件中可以使用更多选项。我们没有时间或空间在这里涵盖所有选项。要查看完整列表，请参阅 `lilo.conf` 的手册页。

`lilo.conf` 文件只是一个文本文件。你可以使用任何 Linux 文本编辑器来修改它。修改完文件并退出编辑器后，你必须记得在 shell 提示符下运行 `lilo` 命令。否则，你对配置文件的更改将不会生效。这在此处展示如下：

```bash
fs4:~ # lilo
Added SL55_10_SP3 *
Added Failsafe
fs4:~ #
```

请注意，`lilo` 命令的输出表明已添加这两个映像。你可能已经注意到，我们刚才用来更新配置的 `lilo` 命令与安装 LILO 的命令是相同的。它完全就是同一个命令。实际上，每次你对 LILO 配置文件做出更改时，都必须使用 `lilo` 命令重新安装 LILO。这里我们应该指出，你可以在 `lilo` 命令中使用 `-b` 选项来指定引导程序应该安装在哪里。如果你指定一个设备，例如 `/dev/sda`，那么引导程序将安装在该设备的 MBR 中。如果你指定一个分区，例如 `/dev/sda1`，那么它将安装在该分区中，并且在 MBR 中放置一个指针。

在转换话题讨论 GRUB 引导程序之前，我们需要先回顾一下 LILO 的一个变体，称为 ELILO。接下来我们就这样做。

### 关于 ELILO

ELILO 的工作方式与 LILO 大致相同。然而，它被设计为运行在不兼容标准版本 LILO 的计算机硬件上。例如，它可以在 IA-64 (IPF) 和 IA-32 (x86) 基于 EFI 的硬件平台上启动 Linux 内核。ELILO 还向后兼容标准的 Intel x86 硬件。然而，目前只有少数 Linux 发行版使用它。

LILO 就到此为止！现在是时候开始使用 GRUB 了！

| 章节 | 选项 | 描述 |
| :--- | :--- | :--- |
| 全局选项 | menu-scheme | 描述 LILO 引导菜单中使用的颜色。语法为：**text_color**:**highlight_color**:**border_color**:**title_color**。每个值使用两个字符。第一个字符是前景色，第二个是背景色。请参阅 lilo.conf 手册页以获取此选项可用所有颜色及其相关字符的列表。 |
| | timeout | 设置默认菜单项自动运行前的超时周期（以十分之一秒为单位）。例如，如果此选项设置为 **80**，则给用户八秒时间选择菜单项。 |
| | lba32 | 指示 LILO 忽略硬盘的物理几何结构并使用逻辑块寻址。这使得 LILO 能够处理拥有超过 1023 个柱面的磁盘（所有现代硬盘都具备）。 |
| | change-rules | 定义启动时对分区类型号进行的更改。 |
| | reset | 指定删除所有默认的 change-rules。 |
| | read-only | 指定根 (/) 文件系统最初以只读方式挂载。在检查文件系统的完整性后，内核通常会以读写模式重新挂载该文件系统。 |
| | prompt | 指定显示 boot: 提示符。 |
| | default | 指定如果用户未做出选择，将加载的默认映像。 |
| | message | 指定 LILO 在启动时显示的图像文件的位置。 |
| | boot | 指定包含引导扇区的设备。例如，要将 LILO 配置为使用第一个硬盘上的第一个分区，你将此选项设置为 /dev/sda2。 |
| 映像选项 | image | 指定 Linux 内核引导映像的路径。 |
| | label | 为映像指定一个名称。 |
| | append | 将指定选项附加到由 LILO 传递给内核的参数中。这通常仅在使用内核难以自动检测的硬件的系统上使用。 |
| | vga | 指定系统启动时应使用的 VGA 文本模式。 |
| | initrd | 指定要加载的内核初始 ramdisk 映像。通常，如果你正在启动 Linux 内核，这会被设置为 /boot/initrd 或 /boot/initrd-version。 |
| | root | 指定应挂载为根的设备。例如，如果你想要将第一个硬盘上的第二个分区配置为应挂载为根分区的分区，你会将此参数设置为 /dev/sda2。 |

**表 6-1** /etc/lilo.conf 配置选项

