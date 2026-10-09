

请确保你的 Web 服务器使用的是高端 SCSI 硬盘控制器以及一套高端 SCSI 硬盘。最新的超宽 SCSI 硬盘是最佳选择。在 Web 服务器上使用多块硬盘是个好主意——例如，你不应该将操作系统和 Web 数据保留在同一块硬盘上。至少使用两块硬盘：一块用于操作系统，另一块用于数据。将操作系统特定的软件与 Web 服务器隔离也是一种良好的安全措施。

硬盘也是常见的故障点。如果你担心硬盘故障，建议定期备份数据。如果预算允许，可以考虑使用廉价磁盘冗余阵列（RAID）子系统，这值得深入研究。RAID 本质上是由一组较小的硬盘组成的集群，它们协同工作以模拟一块大型硬盘。如果其中一块硬盘发生故障，其他硬盘会分担负载，直到故障硬盘被更换。使用 RAID 子系统可以为你的 Web 服务器带来高性能的硬盘 I/O 和合理的数据安全性。

不要误以为慢速硬盘没问题。许多人从供应商那里购买 PC 服务器，被供应商以套餐交易吸引，这些套餐通常配备大容量 IDE 或 EIDE 硬盘。如果你希望服务器不仅仅是个玩具，我强烈建议你避免在 Web 服务器上使用 IDE/EIDE 硬盘。

## 在 Linux 中调整 EIDE/IDE 硬盘

如果你的 Apache 服务器不使用 Linux，可以跳过本节。无论你选择使用 SCSI 还是 IDE 硬盘，如果你重视性能，都必须考虑使用多块硬盘。最低限度，你应该使用两块硬盘——一块用于操作系统和软件，另一块用于数据。对于 Web 服务器，我推荐至少使用三块硬盘，第三块用于存储托管在该机器上的网站生成的日志。将硬盘 I/O 分散在多个设备上可以确保等待时间最小化。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_628_0.png)

> 如果有预算，你可以使用光纤通道硬盘或采用存储区域网络（SAN）解决方案。后者通常用于对数据存储有较高需求的企业。你也可以选择硬件/软件 RAID 解决方案，本章对此进行了讨论。

你可以从现代 EIDE 硬盘中获得更好的性能。首先，在任何调整之前，你必须确定硬盘当前的性能状况，因此你需要一个工具来测量当前硬盘子系统的性能。`hdparm` 工具正适合这项工作；你可以从 http://metalab.unc.edu/pub/Linux/system/hardware 下载该工具的源代码发行版。按照以下步骤编译并安装它：

- 以 root 身份，将源代码发行版解压到合适的目录，例如 /usr/local/src。例如，我在 /usr/local/src 目录下运行 `tar xvzf hddparm-3.9.tar.gz` 命令来解压 hddparm 版本 3.9 的源代码发行版。
- 进入新创建的子目录，运行 `make install` 命令来编译并安装 `hddparm` 二进制文件和手册页。默认情况下，二进制文件安装在 /usr/local/sbin 目录中，并被命名为 `hddparm`。

**注意**

因为 `hdparm` 允许你更改 IDE/EIDE 硬盘子系统的行为，所以不当使用或配置错误有时会导致系统挂起。我强烈建议在使用 `hdparm` 之前备份你的数据。此外，在单用户模式下测试 `hdparm` 是个非常好的主意，这样在你操作时就没有其他用户在使用硬盘。你可以在启动时，在 lilo 提示符下输入 `linux single` 来重启系统并强制其进入单用户模式。

## 使用 hdparm 检查硬盘设置

安装 `hdparm` 工具后，你就可以开始调查硬盘子系统的性能状态。假设你的 IDE 或 EIDE 硬盘是 `/dev/hda`，运行以下命令来检查硬盘配置的状态：

```bash
hdparm /dev/hda
```

你应该看到类似这样的输出：

```
/dev/hda:
 multcount    = 0 (off)
 I/O support  = 0 (default 16 bit)
 unmaskirq    = 0 (off)
 using_dma    = 0 (off)
 keepsettings = 0 (off)
 nowerr       = 0 (off)
 readonly     = 0 (off)
 readhead     = 8 (on)
 geometry     = 2494/255/63, sectors = 40079088, start = 0
```

如你所见，默认模式下几乎所有设置都是关闭的。为了提高硬盘性能，需要更改其中一些默认值。在继续之前，还需要从硬盘获取更多信息。运行以下命令：

```bash
hdparm -i /dev/hda
```

上述命令显示上次系统启动时可用的硬盘标识信息（如果有）。稍后你将使用此命令显示的部分信息。这里，该命令报告了型号、配置、硬盘几何参数（柱面、磁头、扇区）、轨道大小、扇区大小、缓冲区大小、支持的 DMA 模式、PIO 模式等。使用以下命令测试硬盘子系统：

```
/dev/hda:
 Model=WDC WD205AA, FwRev=05.05B05, SerialNo=WD-WMAA015136037
 Config| HardSector NotMFM HdSig>15/15Sec SpinMotCtl1 Fixed DTR>5MB FmtGapReq |
 RawCHS=16383/16/63, TrkSize=57600, SektSize=600, ECCbytes=40
 BuffType=DualPortCache, BuffSize=2048KB, MaxMultSect=16, MultSect=16
 CurCHS=16383/16/63, CurSects=16514064, LBA=yes, LBAsects=40079088
 IORDY=on/off, tPID=[min:120,w/IORDY:120], tDMA=[min:120,rec:120]
 PIO modes: pio0 pio1 pio2 pio3 pio4
 DMA modes: mdma0 mdma1 *mdma2 udma0 udma1 udma2 udma3 udma4
```

这里该命令报告了型号、配置、硬盘几何参数（柱面、磁头、扇区）、轨道大小、扇区大小、缓冲区大小、支持的 DMA 模式、PIO 模式等。现在，让我们使用以下命令测试磁盘子系统：

```bash
/usr/local/sbin/hdparm -Tt /dev/hda
```

你将看到类似这样的结果：

```
/dev/hda:
Timing buffered-cache reads: 128 MB in 1.01 seconds = 126.73 MB/sec
Timing buffered disk reads: 64 MB in 17.27 seconds = 3.71 MB/sec
```

当然，根据你的硬盘和控制器子系统不同，你的数值会有所不同。但是，这是你的硬盘子系统的未调整状态。`-T` 选项告诉 `hdparm` 测试缓存子系统（即内存、CPU 和缓冲区缓存）。`-t` 告诉 `hdparm` 通过读取不在缓存中的数据来报告硬盘（`/dev/hda`）的统计数据。多运行几次此命令，并计算报告的硬盘 MB/sec 的平均值。这大致是你的硬盘子系统的性能状态。在这个例子中，3.71 MB/sec 是读取性能，这个值相当低。

## 调整硬盘的多扇区模式

回顾 `hdparm -i /dev/hda` 命令的输出，查找 `MaxMultiSect` 值。在这个例子中，它是 16。回想一下，`hdparm /dev/hda` 命令显示 `multcount` 值为 `0`（关闭）。这意味着多扇区模式（即 IDE 块模式）是关闭的。

> **注**
>
> *多扇区模式是大多数现代 IDE 硬盘的一项功能。它允许硬盘在每次 I/O 中断时传输多个扇区。默认情况下它是关闭的。然而，大多数现代硬盘可以在每次 I/O 中断时传输 2、4、8 或 16 个扇区。因此，如果你将此模式设置为硬盘支持的最大值（由 `MaxMultiSect` 值显示），你应该看到吞吐量增加 5% 到 50% 甚至更多。此外，你还可以将操作系统开销减少 30% 到 50%。*

在这个例子中，`MaxMultiSect` 值为 16，因此我们可以使用 `hdparm` 工具的 `-m` 选项来设置该值，并查看性能如何提升。运行以下命令：

```bash
/usr/local/sbin/hdparm -m16 /dev/hda
```

通过使用 `hdparm` 的 `-t` `/dev/hda` 命令运行性能测试来显示变化。对于示例系统，变化如下：

```
/dev/hda:
Timing buffer-cache reads:   128 MB in  1.01 seconds = 126.73 MB/sec
Timing buffered disk reads:  64 MB in 16.53 seconds =   3.87 MB/sec
```

硬盘的性能从 3.71 MB/sec 提升到了 3.87 MB/sec。提升不多，但也不算差。也许你也类似地看到了一些变化。如果你的硬盘和控制器比较新，你完全有可能获得比这好得多的性能。你可能会达到 20 到 30MB/秒！然而，请预先警告，在使用 `hdparm` 进行探索时，你可能会损坏数据，因此，如前所述，在测试下文讨论的硬盘硬件特定选项之前，请备份你的数据。

如果 `hdparm` 报告你的系统 I/O 支持设置为 16 位，且你拥有较新的（一两年内购买的）硬盘子系统，你应该尝试 32 位 I/O 支持。你可以使用 `hdparm` 的 `-c` 选项来设置此功能。该选项有三个值：

- `0`—启用默认 16 位 I/O 支持
- `1`—启用 32 位支持
- `3`—启用 32 位支持，并附带许多 IDE/EIDE 芯片组所需的特殊同步序列。这也是大多数系统兼容性较好的值。

按以下方式设置选项：

```bash
/usr/local/sbin/hdparm -m16 -c3 /dev/hda
```

注意使用了之前的 `-m16` 选项，并添加了启用 32 位 I/O 支持的 `-c3`。使用 `-t` 选项运行该程序显示以下结果：

```
/dev/hda:
Timing buffered disk reads:  64 MB in  8.96 seconds =   7.14 MB/sec
```

硬盘子系统的性能几乎翻倍了！

## 为硬盘启用直接内存访问（DMA）

如果你的硬盘支持直接内存访问（DMA），你可能可以使用 `-d` 选项来启用 DMA 模式。

通常，`-d1 -X32` 选项或 `-d1 -X66` 选项一起使用，以利用你硬盘子系统的 DMA 功能。第一组选项（`-d1 -X32`）为硬盘启用多字 DMA 模式 2，下一组选项

