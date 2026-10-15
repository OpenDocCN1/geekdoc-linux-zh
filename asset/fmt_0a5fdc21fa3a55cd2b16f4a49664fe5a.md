
`PATH` 环境变量已设置，以便一旦你在 `/mnt` 上挂载了根分区，如果软盘上不存在根分区中的二进制文件，它们将被执行。同样，如果需要，`/mnt/lib` 和 `/mnt/usr/lib` 中的库也会被使用。在修复系统时，你可能希望更改你的 `PATH`，使其不包含 `/bin` 和 `/usr/bin`，保留 `/mnt/bin`、`/mnt/usr/bin` 等。如果你这样做，你需要使用 `/bin/umount` 来卸载 `/mnt`。

在挂载 `/mnt` 之前，可用的重要实用程序版本有限：

- `mount`：`mount` 命令不要求被挂载的设备节点已经存在，也不要求设备的完整名称。除非另有说明，它假设是 ext2 文件系统。
  - `mount /dev/sda1 /mnt -t ext2` 在功能上等同于 `mount sda1 /mnt`
- `ash`：完整版本
- `cat`：不接受任何选项
- `chmod`：`chmod` 命令不接受符号模式名称，只接受八进制模式。
- `cpio`：完整版本
- `e2fsck`：完整版本
- `fdisk`：完整版本
- `gzip`：完整版本
- `gunzip`：完整版本
- `insmod`：完整版本
- `ls`：完整版本
- `lsmod`：不接受任何选项
- `mkdir`：没有 GNU 长选项
- `mke2fs`：完整版本
- `mkmod`：`mkmod` 命令不接受符号模式名称，只接受八进制模式。
- `open`：完整版本
- `rm`：没有 GNU 长选项
- `rmmod`：完整版本
- `sh`：指向 `ash` 的符号链接

# 附录 A

## 硬件要求

所有在标准 Linux 内核中有驱动程序的器件在 Red Hat 内核中都是“开箱即用”支持的，除了声卡。然而，模块化内核简化了添加声卡支持的过程。有关如何执行此操作的更多信息，请参阅 Kernel-HOWTO（位于 `/usr/doc/HOWTO` 中）。

有关内核直接支持的特殊硬件的更多信息，包括 SCSI 设备，请参阅 Hardware-HOWTO 和 SCSI-HOWTO（与上述位置相同）。还有一个 XFree86 HOWTO 和一个 MetroCards 文件，列出了支持的显卡。

需要连接一个 1.44M 软驱作为第一个物理软盘设备（`a1`）。以下是各种流行软件组合的要求：

### 基于文本的最简安装

- 386sx 或更高级别的 CPU
- 8M 内存
- 40M 硬盘
- 任何可用的显卡（Hercules, CGA, VGA, SVGA 等）
- 任何支持的 CD-ROM 驱动器

### 带有 X 窗口系统的基于文本的最简安装

- 386sx 或更高级别的 CPU
- 8M 内存
- 80M 硬盘
- 任何 XFree86 支持的显卡（VGA 和 SVGA，见下文）
- 鼠标（支持大多数类型）
- 任何支持的 CD-ROM 驱动器

### 推荐配置

- 486dx 或更高级别的 CPU
- 16M 内存
- 300M 硬盘
- 任何 XFree86 或 Metro X 支持的 SVGA 卡
- 三键鼠标
- SCSI 磁带驱动器（可选）
- UPS（可选）
- 双速 CD-ROM 驱动器

支持的显卡包括：

- 大多数 Diamond 卡
- 大多数基于 S3 的卡
- 基于 ET4000 的卡
- ATI 卡
- Cirrus Logic 542x 和 543x
- 基于 Chips and Technologies 的卡
- Trident 8900 和 9400
- 大多数 #9 卡

支持的 CD-ROM 驱动器包括：

- 所有符合 IDE/ATAPI 标准的驱动器
- 所有连接到受支持控制器卡的 SCSI 驱动器
- 所有 Sound Blaster 接口驱动器（Matsushita/Kotobuki/Panasonic）
- Mitsumi 驱动器
- Sony 535, CDU 31, CDU 33

# 附录 B

## 模块参数

本附录旨在说明某些内核模块*可能*需要的*一些*可能参数。需要注意的是，在大多数情况下，不需要使用额外的参数。

### B.1 CD-ROM 参数

| 硬件 | 参数 |
| --- | --- |
| Mitsumi CD-ROM | `mcd=port,irq` |
| Sony 31&33 CD-ROM | `cdu31a=base_addr,[irq=0][,pas]` |
| Aztech CD268 | `aztcd=port` |
| SB Pro 或 16 兼容 | `sbpcd=io_addr,(SB,Laser mate,SPEA)` |
| ATAPI/IDE CD-ROM 驱动器 | `hd(a,b,c,d)=cdrom` |

上述示例如下：

| 示例 | 配置 |
| --- | --- |
| `mcd=0x340,11` | 非 IDE Mitsumi，端口 340，IRQ 11 |
| `cdu31a=0x340,0` | CDU 31 -或- 33，端口 340，无 IRQ |
| `aztcd=0x220` | Aztech CD-ROM，端口 220 |
| `hdc=cdrom` | IDE，第二接口的从设备 |
| `sbpcd=0x230,SoundBlaster` | Panasonic 类型 CD-ROM，端口 230 |

**注意：** 大多数新型 Sound Blaster 卡带有 IDE 接口。你不需要使用 "`sbpcd`" 参数，只需使用 `hd*` 参数即可。

### B.2 SCSI 参数

| 硬件 | 参数 |
| --- | --- |
| SCSI Seagate ST0x | `st0x=base_addr,irq` |
| SCSI Future Domain TMC-8xx | `tmc8xx=base_addr,irq` |
| SCSI Trantor T128 | `t128=base_addr,irq` |
| 基于 SCSI NCR-5380 | `ncr5380=port,irq,dma_channel` |
| Adaptec 151,2x, SB SCSI | `aha152x=port,irq,scsi_id,reconnect_parity` |
| Adaptec 1542 | `aha1542=base_addr` |
| Buslogic | `buslogic=base_addr` |
| Pro Audio Spectrum / Studio 16 | `pas16=port,irq` |

一些示例如下：

```
aha1542=0x330 aha152x=0x330,11,7 tmc8xx=0x330,11
```

注意：上述示例较为冗长。对于 AHA1522，请使用 "`aha152x`" 。对于 AHA1505，请使用 "`aha152x`" 。对于 TMC800，请使用 "`tmc8xx`" 。

当参数中有逗号时，请确保不要在逗号后加空格。如果你要在命令行提供参数，唯一的空格应该出现在 `11nx` 之后以及多个参数之间（例如 `11nx mcd=0x340,11 bmouse=5`）。

### B.3 以太网参数

以太网参数的格式如下：

```
ether=irq,base_addr,mem_start,mem_end
```

然而，对于许多网卡来说，这不应该必要。一个示例如下：

```
ether=11,0x360
```

注意：最后两个参数在大多数（如果不是全部）时间都可以省略。另外，`11nx` 只能识别系统中的第一个以太网卡。要让它识别两个，你必须使用如下的参数：

```
boot: linux ether=0,0,eth1
```

有关此内容的详细信息，请参阅“多以太网迷你 HOWTO”。

# 附录 C

## Metro X

### C.1 特殊功能

#### C.1.1 热键退出

Metro-X 支持通过热键退出。当您 `.xinitrc` 或 `.xsession` 中的最后一个客户端不提供退出会话的方式时，这有助于终止 X 服务器。退出组合键为 `Ctrl | Alt | Backspace`。

#### C.1.2 热键分辨率切换

在配置 Metro-X 时，您可以选择多种屏幕分辨率。然后，您可以通过按下相应的组合键在 X 服务器运行期间即时更改分辨率。要切换到下一个分辨率，请按 `Ctrl | Alt | +`。要切换到上一个分辨率，请按 `Ctrl | Alt | -`。

#### C.1.3 硬件平移

Metro-X 支持硬件平移。这允许您将虚拟分辨率设置为高于监视器的物理分辨率。这样，窗口可以延伸到屏幕的物理边界之外，并且可以通过滚动到扩展区域来查看。

#### C.1.4 多屏幕
