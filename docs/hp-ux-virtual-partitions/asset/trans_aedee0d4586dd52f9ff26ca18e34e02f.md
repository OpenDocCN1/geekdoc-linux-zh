
## 第 3 章中使用的命令的手册页

以下部分包含第 3 章中使用的命令的手册页副本。这为您在进行系统管理日常工作中发出常用命令时提供了快速参考。手册页，更常见的称呼是 man 页，已完整列出。

![image](img/eff8b9287a5f38c5adf538f24aacf29e_205_0.png)

## boot

**boot** - 引导过程概述。

| boot(1M) | 仅限系列 700/800 | boot(1M) |
| :--- | :--- | :--- |
| NAME | | |

### NAME

boot - 引导过程

### DESCRIPTION

系列 700 和 800 的引导过程涉及执行三个软件组件：

- pdc（参见 pdc(1M)），
- isl（参见 isl(1M)），以及
- hpx（参见 hpx_800(1M)）。

处理器复位（RESET）后，pdc，即处理器相关代码（固件），执行自检并初始化处理器。然后它加载并转移控制权给 isl，即操作系统无关的初始系统加载器。接着，isl 加载并转移控制权给 hpx 实用工具，即 HP-UX 特定的引导加载器。随后 hpx 从 HP-UX 文件系统下载 HP-UX 内核对象文件，并将控制权转移给已加载的内核映像。

### SEE ALSO

hpx(1M), hpx_800(1M), isl(1M), pdc(1M)。

## hpx

hpx - 引导 HP-UX 操作系统。

hpxux(1M) hpxux(1M)

### NAME

- *hpx* - HP-UX 引导

### SYNOPSIS

```
hpx [-P] [-lm] [-a[C|R|S|D] devicefile] [-fn]umber] [-istring] [boot] [devicefile]
hpx ll [devicefile] (same as hpx ls -aflm)
hpx ls [-a]in] [devicefile]
hpx set autofile devicefile string
hpx show autofile [devicefile]
hpx -v
hpx restore devicefile (Series 700 only; see DEPENDENCIES.)
```

### DESCRIPTION

*hpx* 是 HP-UX 专用的二级系统加载器（SSL）实用工具，用于引导（关于初始系统加载器，参见 isli(M)）。它支持以下摘要中所示的操作，如 SYNOPSIS 中所示，并在本 DESCRIPTION 中详细说明：

- *boot*：从 HP-UX 文件系统或原始设备加载对象文件，并将控制权转移给已加载的映像。（注意：boot 操作是位置相关的。）
- *ll*：以类似于 `ls -aflm` 的格式列出 HP-UX 目录的内容。（参见 `lsli`；`ls` 仅适用于具有 HFS 文件系统的本地磁盘。）
- *ls*：列出 HP-UX 目录的内容。（参见 `lsli`；`ls` 仅适用于具有 HFS 文件系统的本地磁盘。）
- *show autofile*：显示自动执行文件的内容。
- *set autofile*：将自动执行文件的内容更改为 *string* 指定的内容。
- *-v*：显示 hpx 实用工具的版本号和发行号。
- *restore*：从格式正确的可引导磁带恢复系统。（系列 700 专用；参见 DEPENDENCIES。）

hpx 命令可以从键盘交互输入，也可以通过 isil 自动执行文件提供。

hpx 仅限于对由 pdc(1M) 初始化的接口进行操作。在大多数情况下，操作仅限于引导设备接口。

### Notation

hpux 接受许多选项中的数字（数值常量）。数字遵循 C 语言关于十进制、八进制和十六进制常量的表示法。前导 0（零）表示八进制，前导 0x 或 OX 表示十六进制。例如，037、0x1F、0x1F 和 31 都表示同一个数字，即十进制 31。

hpux 的 boot、ll、is、set autofile、show autofile 和 restore 操作接受 devicefile 规范，其格式如下：

manager/w.x.y:z/filename

devicefiles 规范由设备名和文件名组成。设备名（manager/w.x.y:z/n）包含一个 I/O 系统管理器（设备或接口驱动程序）的通用名称（例如 disc）、通往该设备的硬件路径以及次要号。如果使用默认值，可以完全省略 manager 名称。w.x.y.z 是通往设备的物理硬件路径，标识总线转换器、槽号和硬件地址。对于系列 700 机器，有一组助记符可用于替代硬件路径。n 是控制管理器依赖功能的次要号。文件名部分，filename，是标准的 HP-UX 路径名。某些 hpux 操作对特定组件有默认值。仅包含设备部分的 devicefile 规范指定一个原始设备。包含文件名的 devicefile 规范意味着该设备包含一个 HP-UX 文件系统，且该 filename 位于该文件系统中。

典型的 boot devicefile 规范是：

disc(2/4.0.0)/stand/vmunix

其中 manager 是 disc，通往磁盘设备的硬件路径是 2/4.0.0，默认显示的次要号为 0，而 /stand/vmunix 是引导设备的文件名。

hpux 现在支持合并的 manager 列表：disc、tape 和 lan。manager disc 管理所有通过 HP-IB（原为 dsic0）连接的 CS/80 磁盘；通过 HPP111 接口（原为 dsic1）连接的 CS/80 磁盘；所有通过 NIO HP-IB（原为 dsic2）连接的磁盘设备；所有通过 SCSI（原为 dsic3）连接的磁盘设备，以及所有 audiochanger 磁盘设备（原为 dsic3）。manager lan 通过基于 HP26532A NIO 的 LAN 接口（原为 lanll）管理远程引导。目前仅在此卡上支持远程引导，不支持任何基于 CIO 的 LAN 卡。manager tape 通过 HP-IB（原为 tape1）管理 HPP794、HPP797 和 HPP7980 磁带机，通过 SCSI（原为 tape2）管理磁带机。

devicefile 规范中的硬件路径是一串数字，每个数字后跟斜杠 (/)，后跟一串由点 (.) 分隔的数字，每个数字按顺序从总线地址到设备地址标识一个硬件组件。带有斜杠后缀的硬件组件表示总线转换器，在您的机器上可能不需要。例如，在 w.x.y.z 中，w 是总线转换器的地址，x 是 MIO-UBS 模块的地址，y 是 CIO 槽号，z 是 HP-IB 地址或 HPP111 总线地址。

devicefile 规范中的次要号 n 控制驱动程序相关的功能。（参见手册“Configuring HP-UX for Peripherals”中特定驱动程序的次要号位分配）。

文件名是标准的 HP-UX 路径名。不需要前导斜杠 (/)，指定前导斜杠也不会引起问题。

### Defaults

hpx 用于完成命令的默认值通过一系列步骤获取。首先，使用命令中明确指定的任何组件。如果命令不完整，hpx 尝试根据 pdc 维护的信息（参见 pdc(8M)）构建默认值。如果没有足够的信息来完成命令，则搜索自动执行文件。如果搜索失败，命令中剩余未解决的组件将由硬编码默认值满足。

没有针对 manager 的硬编码默认选择；如果无法选择，hpx 将报告错误。

当未指定通往引导设备的硬件路径时，hpx 默认使用 pdc 维护的信息。硬件路径元素没有硬编码默认值。

如果未提供次要号元素，hpx 从自动执行文件中获取默认值。如果失败，则使用硬编码默认值 0。

对于 boot 命令，没有文件名的 devicefile 规范表示引导设备不包含 HP-UX 文件系统。hpx 将此解释为 NULL（而非缺失）文件名，并且不搜索默认值。如果完全缺失 devicefile 规范，hpx 将搜索默认值；选择自动执行文件内容或硬编码默认值。

有两种可能的硬编码默认 devicefile 规范。一个硬编码默认 devicefile 规范是 /vmunix。另一个硬编码默认 devicefile 规范是 /stand/vmunix。

如果您有一个 LVM 系统，其中引导卷和根卷位于不同的逻辑卷上，则内核将是 /vmunix。这是因为系统在启动时引导卷将挂载在 /stand 下。

对于所有其他配置，内核将是 /stand/vmunix。

硬编码默认值的搜索顺序是先 /stand/vmunix，然后 /vmunix。

### boot Operation

boot 操作根据可选的 devicefile 从 HP-UX 文件系统或原始设备加载对象文件。然后它将控制权转移给已加载的映像。

指定 devicefile 中缺失的任何组件都由默认值补充。例如，devicefile 为 vmunix.new 实际上会产生：

```
disc(8.0.0.0)/vmunix.new
```

而对于从 HP-IB 地址 1 的磁盘引导，devicefile 为 (8.0.1)/stand/vmunix 会产生

```
disc(8.0.1.0)/stand/vmunix
```

无论指定的 devicefile 多么不完整，boot 都会宣布用于查找对象文件的完整 devicefile 规范。伴随此信息，boot 在转移控制权之前给出已加载映像的 TEXT、DATA 和 BSS 段的大小以及入口偏移量。

boot 操作接受多个选项。注意，boot 选项必须按照语法声明中所示的位置指定

