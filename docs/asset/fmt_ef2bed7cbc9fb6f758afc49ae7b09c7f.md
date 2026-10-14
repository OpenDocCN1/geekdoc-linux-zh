
Memory cards: (All SRAM cards work. Unsupported flash cards are read but not written.). Intel 2 Series, 2 Series+, and Value Series 100 Flash, Maxter Maxor Mobile16MB Flash, IBM BMD Flash, RATOC SmartMedia Adapter TDK Flash, Memory SFM20W/2.

SCSI adapters: [Be careful. Many vendors, particularly CD-ROM viewers, seem switch controllers more or less at all. Generally, they’ll use different product code, but not always. Old (supported) New Bus Toaster are not easily distinguishable from the current Symfony-based cards which use the sys53c50 cs driver, distributed separately.], (content) Noteworthy Bus Toshiba SCSI CD-ROM Discman PRD-250, Future Domain SCSI2GO, IBM SCSI, Simple Technologies SCSI, Eager Labs SCSI (only cards with F/DD ID], Ejon, SCSI-2200, MACNA mpS110LP, mpS110-LP SCSI, Toshiba

# 310 附录

CN-SC43, NEC PC-9801-J03R, Qlogic FastSCSI, Panasonic KXL-D740, KLDN7440, KXL-DN740-NB 4X CD-ROM, Raven CD-Note 4X, RATOC RES-9530 SCSI-2, Toshiba NWB010ABK, SCSC200A, SCSC200B, Digital SCSI adapter, IO DATA PCSI-II, PCII-L, IO DATA CDG-PX4/PCSC CD-ROM, Logitech LPM-CSC2, Logitech LCD... (Note: repeated entries omitted as per system instructions).

## 附录 A：硬件兼容性

Adaptec/Trantor APA-460 SlimSCSi, Eiger Labs SCSI (FCC ID K36...), New Media .WAVjammer 以及所有其他声卡, New Media LiveWire+, Nikon CoolPix100, 松下 KXL-D720, KXL-D745, KXL-D0783, SMC 8016 EliteCard, Xircom CE II Ethernet/Modem, Xircom CE-108T Ethernet。

以下厂商通过贡献硬件和/或产品技术文档协助了 Linux PCMCIA 驱动包的开发。可以推断，由于这些厂商支持 Linux 开发并提供了技术帮助，他们的卡在 Linux 下可能会获得更好的支持。

- 3Com/Meghertz
- Adaptec
- Intel
- Linksys
- Ositech
- Sandisk
- Quatech
- 以太网和多功能卡
- SCSI 适配器卡
- 闪存卡
- 以太网和多功能卡
- 以太网/调制解调器组合卡
- ATA/IDE 闪存卡
- 并口适配器

## 启动时的硬件参数

如果你在启动时遇到 Linux 内核无法识别 IDE 硬件设备某些特性的问题，请查看这些启动时参数。以下是《BootPrompt HOW-TO》的节选：

IDE 驱动程序接受许多参数，范围从磁盘几何规范到对高级或损坏控制器芯片的支持。以下是所有可能的启动参数的摘要。欲需详细信息，你真的应该查阅 `linux/Documentation` 目录下的 `ide.txt` 文件，该摘要正是从该文件中提取的。

- `drive` 可能存在，但不对其进行探测
- `drive` 不存在，忽略 cmos 且不进行探测
- `hdx=nop`
- `hdx=none`

| `hdx=nowerr` | 忽略此驱动器上的 WRRRR_STAT 位 |
| `hdx=cdrom` | 驱动器存在，且是一个 CD-ROM 驱动器 |
| `hdx=cyl,head,sect` | 磁盘驱动器存在，并具有指定的几何结构 |
| `hdx=autotune` | 驱动程序将尝试将接口速度调整为最快的 PIO ，仅适用于支持的驱动器（如果的话）。并非所有芯片组都完全支持，并且可能给旧的/特殊的 IDE 驱动器带来问题 |
| `idex=noprobe` | 不要尝试访问/使用此接口 |
| `idex=base` | 在指定的地址探测接口，其中 "base" 通常是 0x1F0 或 0x70，"ctl" 假设为 "base+0x20" |
| `idex=base.ctl` | 同时指定 base 和 ctl |
| `idex=base.ctl,irq` | 指定 base，ctl 和 irq |
| `idex=autotune` | 驱动程序将尝试将此接口上所有驱动器的速度调整为支持的最快 PIO 模式。并非所有芯片组都完全支持，并且可能给特殊的 IDE 驱动器带来问题 |
| `idex=noautotune` | 驱动程序将不会尝试调整接口速度。除 cmd640 外，大多数芯片组的默认设置 |
| `idex=serialize` | 不在 index 和 ide(x1) 上重叠操作 |

# 附录 B

# Linux 手册页 (man Pages)

UNIX 和 Linux 系统很大程度上由在命令行执行的小而简洁的命令组成。通常，每个命令至少对应一个 man 页。Linux 手册页与性别无关：`man` 代表 manual（手册）。

曾几何时，手册页是 UNIX 系统附带的唯一文档。我某处仍然保留着我第一次作为 UNIX 用户和系统管理员时收到的那薄书。里面包含的所有都是手册页，而我当时 supposed安装一个 UNIX 系统。多年以后，我仍然会首先查看手册页，以快速了解某个命令的功能、在命令行上应该使用哪些参数或应该设置哪些值。

本附录将向你展示如何使用 `man(1)` 命令，如何阅读和理解手册页，以及如何找到可能帮助你理解正在研究的 Linux 命令的其他手册页。

## 使用 man 命令

要开始使用手册页，请按照以下步骤操作：

1. 在 Linux 运行后，以用户身份登录（普通用户或 root）。
2. 输入 `man` 命令。系统询问你想要哪个手册页。`man` 命令的语法（与其他许多命令一样）至少需要一个参数。
3. 通过输入 `man` 来提供参数。第一个 `man` 是命令名，第二个 `man` 告诉你想获取关于手册本身的信息。系统可能会告诉你稍等，它会将页面格式化到你的屏幕上，然后显示该命令的参考页。
4. 如果屏幕底部出现冒号（:`），按空格键查看下一页，或使用方向键移动。
5. 如需退出程序，按 `q`。

## 手册页中的章节

手册页通常位于系统中的多个目录中：每个目录又细分为若干子目录，代表手册的不同章节，如下所示：

- `man1`: 用户命令
- `man2`: 系统调用
- `man3`: 库函数
- `man4`: 特殊文件
- `man5`: 游戏
- `man7`: 杂项
- `man8`: 系统管理 nroff, troff 和 groff 宏

注意，大多数目录有多个章节。两个章节可能包含同名命令的条目。例如，第 1 部分有 `open` 命令，第 2 部分有 `open` 系统调用。为了确保你阅读的是正确的内容，你可以在 man 行上指定命令。例如：

- `man 2 open`

手册页数据库的大部分章节（它基本上就是这样）包含两个部分：

- 由名为 `intro.n` 的文件表示的介绍页，其中 `n` 对应章节号。
- 由名为 `command.n` 的文件表示的所有命令、调用、库和文件名，其中 `n` 是章节号。

# 附录 B：Linux 手册页

如果你使用 `cd` 进入 `/usr/man1` 目录并执行 `ls` 命令，你会看到 `cat.1` 和 `grep.1` 等文件。奇怪的是，你找不到名为 `cd.1` 的文件，因为 `cd` 命令内置在不同的 shell 中，其文档包含在 `bash.1` 或 `csh.1` 文件中。

如果你使用 `bash` 作为 shell，可以如下所示获取有关其他内置命令的信息：intro 简要描述了手册的章节以及你是否需要了解该章节的特殊内容。打印介绍页非常简单。例如：`man 2 intro` 或 `man 3 intro`。

## 手册页中的主题
