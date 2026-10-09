
在进行系统工作时，往往会忘记其处于通电状态。这不仅存在触电危险，对电子元件也不好。

- **确保你身上的静电荷已消散。** 使用防静电腕带并确保其正确接地。始终触摸电源上的金属部分以泄放任何残留电荷。
- **切勿强行连接。** 计算机上的许多连接器被设计为一组小的金属引脚。这些引脚非常容易弯曲或折断，而且往往是在你没有察觉的情况下发生的。
- **切勿通过拉扯电线来断开电缆。** 大多数计算机连接器都很脆弱，容易分离。拉扯电线可能会导致它们从连接器上脱落。
- **给所有部件贴标签。** 直到你觉得自己擅长电脑维修之前，请给所有部件贴标签。连接器通常设有键位，只允许在正确的方向上进行连接，但一个意志坚定的人可能会强行连接。计算机系统中的硬线缆外观相同。贴标签将在稍后为你节省时间。
- **阅读手册。** 大多数系统都有服务手册可用。阅读说明并遵循其指导。

### 硬盘问题

在大多数 Linux 系统中，硬盘通常会在其额定寿命之后依然完美运行。然而，错误总是可能发生的。fsck 程序可以处理大多数问题。如果硬盘发生灾难性故障，应更换硬盘并从备份中恢复数据。更换硬盘的过程与安装第二个硬盘相同，这在第 2 章中有介绍。

**EIDE/ATA 硬盘问题**

大多数个人电脑使用 EIDE/ATA 硬盘。在硬盘安装并运行后，遇到的主要问题通常是性能问题。如果你有一个专为配合 Linux 操作系统设计的新型系统，你的硬盘可能已针对该系统进行了优化。然而，并非所有系统都为 Linux 设计，也并非所有 Linux 发行版都针对所有硬盘进行了优化。此外，Linux 发行版通常优先考虑稳定性而非性能，因此硬盘可能未发挥其最佳性能。

Linux 操作系统提供了 `hdparm` 工具来测试并提高硬盘性能；但是，**`hdparm` 可能导致意外的数据损坏。使用它需自担风险。** 在尝试对硬盘进行任何更改之前，请确保备份系统。`hdparm` 命令的语法为 `hdparm [flags] [device]`，其中 device 是硬盘设备名称，例如 /dev/hda，而 flags 是从零到多个选项。一些最常见的包括：

- **无标志**：如果没有给出任何标志，则默认使用 -acdgmrrrw 标志。运行不带任何标志的 `hdparm` 命令将显示硬盘已设置为安全值。这些值有助于确保 Linux 操作系统能在最广泛的硬盘范围内运行。

```bash
# hdparm /dev/hda

/dev/hda:
    multcount    = 16 (on)
    IO_support   = 0 (default 16-bit)
    unmaskirq    = 0 (off)
    using_dma    = 0 (off)
    keepsettings = 0 (off)
    readonly     = 0 (off)
    readahead    = 8 (on)
    geometry     = 1310/240/63, sectors=19807200, start=0
```

- **-T**：此标志指示 `hdparm` 执行缓存读取计时，用于基准测试和比较目的。此命令应在基本上处于静止状态、仅运行必要进程的机器上运行几次。此标志显示直接从 Linux 缓冲区缓存读取的速度（无需访问磁盘），这衡量了系统处理器、缓存和内存的吞吐量。包括 `-t` 标志将基于 `-T` 的结果在最终结果中提供修正系数。

- **-t**：此标志指示 `hdparm` 执行设备读取计时，用于基准测试和比较。此命令也应在静止的系统上运行几次。这显示通过缓冲区缓存读取到磁盘的速度（没有预先缓存数据）。这是对驱动器能维持顺序数据读取速度的测量。

```bash
# hdparm -Tt /dev/hda

/dev/hda:
Timing buffer-cache reads: 128 MB in 1.43 seconds = 89.51 MB/sec
Timing buffered disk reads: 64 MB in 14.12 seconds = 4.53 MB/sec
```

- **-i**：此标志使 `hdparm` 显示在启动时从硬盘获取的识别信息。

```bash
# hdparm -i /dev/hda

/dev/hda:
Model=WDC AC310100B, FwRev=32.02S32, SerialNo=WD-WTE6390094409
Config={ HardSect NotMFPM HDSw<15uSec SpinMotCtl Fixed DTR>5Mbs FmtGapReq }
RawCHS=16383/16/63, TrkSize=57600, SectSize=600, ECCbytes=22
BuffType=DualPortCache, BuffSize=512kB, MaxMultSect=16, MultSect=16
CurCHS=16383/15/63, CurSects=19807200, LBA=yes, LBAsects=19807200
PIO modes: pio0 pio1 pio2 pio3 pio4
DMA modes: mdma0 mdma1 mdma2
UDMA modes: udma0 udma1 *udma2
AdvancedPM=no WriteCache=enabled
Drive conforms to: device does not report version: 1 2 3 4
```

`hdparm -i` 命令的输出显示了关于硬盘的信息。它指出支持 DMA，且 udma2 是默认值。

- **-X `<value>`**：此标志用于设置 IDE 传输模式，通常与 `-d1` 标志结合使用，以启用直接内存访问（DMA）。DMA 是一种将数据从主内存传输到设备而不经过 CPU 的技术。（带有 DMA 通道的计算机比没有 DMA 通道的计算机更快地在设备之间传输数据。）对于多字 DMA，使用的值是所需的 DMA 模式号加 32，而对于 UDMA，值是 UltraDMA 加 64。

`hdparm /dev/hda` 命令的结果显示 DMA 已关闭。要开启 DMA2，请使用 `hdparm -d1 -X34 /dev/hda` 命令。`-d1` 标志表示启用 DMA。`-X34` 标志表示使用 DMA2。以下代码显示了禁用 DMA 时 /dev/hda 的计时情况，设置 DMA2，并显示最终计时结果。

```bash
# hdparm -Tt /dev/hda

/dev/hda:
Timing buffer-cache reads: 128 MB in 1.42 seconds = 90.14 MB/sec
Timing buffered disk reads: 64 MB in 14.10 seconds = 4.54 MB/sec
# hdparm -d1 -X34 /dev/hda

/dev/hda:
setting using_dma to 1 (on)
setting xfermode to 34 (multiword DMA mode2)
using_dma=1 (on)
# hdparm -Tt /dev/hda

/dev/hda:
Timing buffer-cache reads: 128 MB in 1.41 seconds=90.78 MB/sec
Timing buffered disk reads: 64 MB in 5.08 seconds=12.60 MB/sec
```

使用上述选项可以看到显著的性能提升。还有其他可能提高性能的设置。使用 `man hdparm` 命令查看所有可用选项。

### SCSI 硬盘问题

SCSI 硬盘多年来发生了变化，正如大多数技术一样。最初的硬盘称为 SCSI 1 或窄 SCSI，使用运行频率最高为 5 MHz 的 50 针连接器。为了增加带宽，总线速度提高到了 10 MHz，从而创建了新的标准 SCSI 1 或 Fast SCSI。目前正在开发中的最新 SCSI 技术称为 ULTRA 320，提供 320 MHz 的总线速度，或高达 320 MB/s 的数据传输率。表 13-1 列出了部分总线速度和 SCSI 术语，这些术语得到了 SCSI 贸易协会（STA）的认可。

**表 13-1：总线速度和 SCSI 术语**

| STA 术语 | 总线速度 (MB/s) | 最大支持设备数 |
| :--- | :--- | :--- |
| SCSI 1 | 5 | 8 |
| Fast SCSI | 10 | 8 |
| Fast Wide SCSI | 20 | 16 |
| Ultra SCSI | 20 | 16 |
| Wide Ultra SCSI | 40 | 16 |
| Ultra2 SCSI | 40 | 8 |
| Wide Ultra2 SCSI | 80 | 16 |
| Ultra 160 SCSI | 160 | 16 |
| Ultra 320 | 320 | 16 |

SCSI 技术的变化使得对电缆和端接的要求也发生了变化。例如，总线速度越快，连接设备的电缆必须越短。

`hdparm` 命令可用于测试性能，但不能用于更改硬盘的参数。通常，遇到的 SCSI 设备问题可以追溯到硬件问题。

SCSI 控制器通常带有用户在启动过程中可以访问的固件，这可能有助于排查 SCSI 设备问题。

**正确的端接**对 SCSI 硬盘的功能至关重要。沿 SCSI 总线传播的脉冲会从总线上任何与其余部分不同的部分反射。这些反射会以奇异的组合相加和相减，导致原始脉冲失真和损坏。为了防止或最大限度地减少来自总线两端的反射，添加端接器以吸收脉冲的能量。

端接器必须存在于 SCSI 总线的两个位置，即总线的开始和结束，并且必须发生在 SCSI 总线物理端点四英寸范围内。端接可以是内部的或外部的。

**内部端接**：SCSI 驱动器在驱动器内部提供端接，并可以通过跳线设置进行启用/禁用。

**外部端接**：使用在线端接器或馈通端接器完成。这些是连接到总线末端的封闭端端接插头。
