
- (c) **分区表所基于的几何参数。** 参见 `fdisk -l` 的输出。它受 `fdisk` 专家命令影响，并对你的数据构成极大风险。强烈建议先完整备份你的数据。
- (d) **BIOS 检测到的几何参数。** 这是系统引导后 LILO 遇到的几何参数。LILO 必须使用它。请参阅 BIOS 设置，如果适用，可能还需要参阅 SCSI 主机适配器设置。该几何参数受 BIOS 设置影响。

面对不一致时，进行调整的最佳方式往往是采取最省事的路径。在解决这些错误之前，必须先分析以下数据：
- `/etc/lilo.conf`
- `fdisk -l` 命令的输出（分区表）
- 上述日志文件
- 硬盘的 BIOS 和 SCSI-BIOS 设置

## 1024 柱面限制

> **注意**
>
> 较新的 BIOS 版本允许从 1024 柱面限制以上启动操作系统。当前 LILO 版本可以使用此 BIOS 扩展。YaST2 在配置 LILO 时会相应告知你适用于你 BIOS 的这些选项。如果你的 BIOS 不包含此扩展，请继续阅读此处。

如第 94 页 *LILO 位置* 一节所述，整个 LILO 机制——即引导所需的所有数据——必须可供 BIOS 调用。该节还讨论了可访问柱面的问题。这一限制只影响引导机制。并不要求 LILO 必须安装在 Linux 根分区上。将引导机制放在 Linux 具有读写访问权限的其他操作系统分区上也是可能的，但风险很高。

> **警告**
>
> 这不适用于 LILO 引导扇区。切勿将引导扇区安装到未知分区上，因为这会严重损坏文件系统。

- 最好的方法是创建一个主分区（在允许的区域内），并将所有 LILO 文件（包括 LILO 引导扇区）安装到此分区中。

使用 YaST2 安装时会创建一个小的 `/boot` 分区，其大小仅足以容纳 `boot.b`、`map`、`message` 文件以及 LILO 应引导的 Linux 内核。

几兆字节就足够了。其余分区放在哪里并不重要。不再有其他限制。一旦内核运行，你就可以不受限制地访问所有已安装的驱动器。

- 如果由于某种原因，第一种也是更可取的引导分区方案不可行，请将 LILO 写入引导盘，或者如果你同时运行 MS-DOS，则使用 `loadlin` 引导 Linux。
- 另一种替代方案是将 LILO 引导机制安装到允许区域内的非 Linux 分区上。Linux 必须具有写访问权限（例如 FAT 或 VFAT 驱动器）。请记住，LILO 引导扇区不能安装在该分区上。只有两个位置可以放置它：第一个驱动器上扩展分区的开头——在 1024 柱面限制之内——或 MBR 上。

假设相关分区挂载为 `/mnt`。你希望将 LILO 安装到 `/dev/hda` 的 MBR 中，并从 `/dev/hda1` 引导 DOS。请按以下步骤操作：
- 创建一个新目录（例如 `/mnt/LINUX`），并将上述 LILO 文件复制到其中：`boot.b`、`map`、`message`、用于其他操作系统的链式加载程序（通常为 `chain.b`），以及 LILO 应引导的 Linux 内核。
- 创建一个 `/mnt/LINUX/lilo.cfg`，其中所有路径都指向 `/mnt/LINUX`（参见文件 8）。

```text
# LILO Configuration file
# Start LILO global section
boot=/dev/hda                  # Installation target
backup=/mnt/LINUX/hda.xxxx    # backup of old MBR
install=/mnt/LINUX/boot.b     # Of course LILO and
map=/mnt/LINUX/map            # map file are in /mnt/LINUX!
message=/mnt/LINUX/message    # optional
prompt
timeout=100                  # Wait at prompt: 10 s
vga = normal                  #
# End LILO global section
#
# Linux bootable partition config begins
image = /mnt/LINUX/first_Kernel   # default
    root = /dev/Your_Root_Device  # Root partition!
    label = linux
# Linux bootable partition config ends
#
# System section for other kernels:
#
# End Linux
# DOS bootable partition config begins
other = /dev/hda1             # MSDOS system drive
    label = dos
    loader = /mnt/LINUX/chain.b
    table = /dev/hda
# DOS bootable partition config ends
```

*文件 8：用于其他分区的 lilo.cfg*

- 使用*这个* `lilo.cfg` 安装 LILO：

```text
earth: # /sbin/lilo -C /mnt/LINUX/lilo.cfg
```

之后，LILO 应该可以正常工作。启动 MS-DOS，并尽可能保护 LILO 文件免受写入访问（任何写入访问都会使 LILO 失效）。至少要为 `X:\LINUX` 中的所有文件（其中 'X' 是挂载到 `/mnt` 的 DOS 驱动器）设置 DOS 属性 *system* 和 *hide*。

另请阅读 `/usr/share/doc/howto/en/mini/` 中的两个 HOWTO——`LILO.gz` 和 `Large-Disk.gz`。

## 2.0 及更高版本内核的特殊引导问题

使用 LILO 引导时的问题——无论你是从软盘还是从硬盘引导——都可能在内核部分加载之后出现（例如 SuSE 安装内核）。你可以在 LILO 提示符下选择一个内核，该内核会被加载（屏幕上会输出一些点），但启动内核会失败。在到达 “uncompressing Linux” 之前，系统会以不同的行为崩溃。

可能的错误消息：
- 系统重启
- 系统只是挂起
- "crc-error"
- "no free space"
- "Error 0x00"
- "Error 0x01"
- "incomplete literal tree"

系统会尝试访问软盘，但随后挂起。原因在于大内核、LILO 和有缺陷的硬件三者的组合。这大约影响百分之一的机器。

我们推测这是由于 BIOS 存在缺陷，对快速内存访问的处理有问题。在以下情况下，不会出现此问题：
- 机器通过 `loadlin` 引导（参见第 120 页 *使用 loadlin 配置引导机制* 一节）
- 内核已使用 `dd if=/vmlinuz of=/dev/fd0` 复制到软盘，并从软盘引导
- 使用 `make zImage` 创建的较小内核通过 LILO 引导

以下 BIOS 设置也不会导致任何问题：
- 禁用内部高速缓存
- DRAM 预充电等待状态值：*1*
- DRAM 等待突发时序值：`0x3333`

## 解决方案

首先，你应该能够安装一个系统。因此，如果你无法通过 `loadlin` 或 `setup` 引导，请使用旧版内核 1.2.13 的启动盘进行安装。如果你没有这样的启动盘，请相应地更改 BIOS 设置。

将来引导时，请使用与安装时相同的中介。从 DOS 使用 `loadlin` 不应造成任何问题。如果使用启动盘，你应该输入以下参数：

```text
load_ramdisk=0 root=/dev/(rootpartition)
```

其中 *(rootpartition)* 是你的根分区（例如，`hda1`）。

## 使用 loadlin 配置引导机制

在以下章节中将介绍 `loadlin`，它是引导 SuSE Linux 的另一种方法。`loadlin` 是一个 DOS 应用程序，能够引导存储在 DOS 目录中的 Linux 内核。`loadlin` 可以无缝集成到现有的 DOS/Windows 9x 环境中，并借助 Windows 启动管理器轻松启动。由于 MBR 中没有条目，Windows 不会知道 Linux 已安装，而只会“看到”一个或多个具有 Windows 无法识别的 ID 的分区。这样，Linux 与 Windows 系统共存可能产生的不良副作用就被降到了最低。

此处描述的过程适用于 Windows 95 和 Windows 98。下面显示的配置文件是为 Windows 95 开发的。因此，以下内容仅直接涉及 Windows 95。

你需要做一些准备工作，然后才能使用 `loadlin` 引导 Linux。根据你的系统环境，你可能还需要修改某些引导文件。
