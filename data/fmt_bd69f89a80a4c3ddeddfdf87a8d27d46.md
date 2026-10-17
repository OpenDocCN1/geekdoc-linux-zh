
*N* 是控制器的主机 ID。您应该会看到类似下面的内容：

```text
EATA (Extended Attachment) driver version: 2.59b
queued commands:                 17664
processed interrupts:             17664

scsi0 : HBA PM3334UW
Firmware revision: V07L.0
Hardware Configuration:
IRQ: 0, edge triggered
DMA: BUSMASTER
CPU: MC68000 @ 0MHz
Base IO: 0xef90
Host Bus: PCI
SCSI Bus: Speed: 5MB/sec.
SCSI channel expansion Module: not present
SmartRAID hardware: not present.
        Type: -
        Max array groups:              7
        Max drives per RAID 0 array:   7
        Max drives per RAID 3/5 array: 7
Cache Module: not present.
        Type: -
        Bank0: 0MB without ECC
        Bank1: 0MB without ECC
        Bank2: 0MB without ECC
        Bank3: 0MB without ECC
Timer Mod.: not present
NVRAM     : not present
SmartROM  : enabled
Alarm     : off
Host<->Disk command statistics:
```

| 大小 | 读取 | 写入 |
|---:|---:|---:|
| 1k | 0 | 0 |
| 2k | 0 | 0 |
| 4k | 0 | 0 |
| 8k | 0 | 0 |
| 16k | 0 | 0 |
| 32k | 0 | 0 |
| 64k | 0 | 0 |
| 128k | 0 | 0 |
| 256k | 0 | 0 |
| 512k | 0 | 0 |
| 1024k | 0 | 0 |
| >1024k | 0 | 0 |
| 总计 | 0 | 0 |

```text
Attached devices:
Host: scsi0 Channel: 00 Id: 00 Lun: 00
      Vendor: DPT     Model: RAID-5              Rev: 07L0
      Type:  Direct-Access                         ANSI SCSI revision: 02
```

要获取高级命令统计信息，请键入以下命令：

```shell
# echo "eata_dma latency" > /proc/scsi/eata_dma/N
```

然后您可以输入以下命令：

```shell
# cat /proc/scsi/eata_dma/N
```

要获取更详细的统计信息，可使用以下内容：

```text
EATA (Extended Attachment) driver version: 2.59b
queued commands:           17737
processed interrupts:      17737

scsi0 : HBA PM3334UW
Firmware revision: V07L.0
Hardware Configuration:
IRQ:  0, edge triggered
DMA: BUSMASTER
CPU: MC68000 @ 0MHz
Base IO: 0xef90
Host Bus: PCI
SCSI Bus: Speed: 5MB/sec.
SCSI channel expansion Module: not present
SmartRAID hardware: not present.
             Type: -
       Max array groups:       7
       Max drives per RAID 0 array:     7
       Max drives per RAID 3/5 array:   7
Cache Module: not present.
             Type: -
       Bank0: 0MB without ECC
       Bank1: 0MB without ECC
       Bank2: 0MB without ECC
       Bank3: 0MB without ECC
Timer Mod.: not present
NVRAM      : not present
SmartROM   : enabled
Alarm      : off
Host Latency Command Statistics:
Current timer resolution: 10ms
```

| 大小 | 计数 | 最小 (ms) | 最大 (ms) | 平均 (ms) |
|---|---:|---:|---:|---:|
| **读取** |  |  |  |  |
| 1k | 36 | 0 | 30 | 9 |
| 2k | 0 | 0 | 0 | 0 |
| 4k | 3 | 0 | 10 | 6 |
| 8k | 0 | 0 | 0 | 0 |
| 16k | 0 | 0 | 0 | 0 |
| 32k | 0 | 0 | 0 | 0 |
| 64k | 0 | 0 | 0 | 0 |
| 128k | 0 | 0 | 0 | 0 |
| 256k | 0 | 0 | 0 | 0 |
| 512k | 0 | 0 | 0 | 0 |
| 1024k | 0 | 0 | 0 | 0 |
| >1024k | 0 | 0 | 0 | 0 |
| **写入** |  |  |  |  |
| 1k | 24 | 0 | 0 | 0 |
| 2k | 0 | 0 | 0 | 0 |
| 4k | 0 | 0 | 0 | 0 |
| 8k | 0 | 0 | 0 | 0 |
| 16k | 0 | 0 | 0 | 0 |
| 32k | 0 | 0 | 0 | 0 |
| 64k | 0 | 0 | 0 | 0 |
| 128k | 0 | 0 | 0 | 0 |
| 256k | 0 | 0 | 0 | 0 |
| 512k | 0 | 0 | 0 | 0 |
| 1024k | 0 | 0 | 0 | 0 |
| >1024k | 0 | 0 | 0 | 0 |

```text
Attached devices:
Host: scsi0 Channel: 00 Id: 00 Lun: 00
  Vendor: DPT     Model: RAID-5        Rev: 07L0
  Type: Direct-Access              ANSI SCSI revision: 02
```

要关闭高级命令统计信息，请键入以下命令：

```shell
# echo "eata_dma.nolatency" > /proc/scsi/eata_dma/N
```

## 故障排除

下面是在本节中讨论的几个典型 RAID 5 问题：

- 启动时未检测到任何 SCSI 主机
- RAID 配置显示为 N 个不同的磁盘
- 格式化过程中机器或控制器关闭
- 初始文件系统格式化期间产生 SCSI_ABORT_BUSY 错误

### 启动时未检测到任何 SCSI 主机

有时，在引导系统时不会检测到任何 SCSI 主机。这可能是多种原因造成的，但通常表明尚未配置相应的驱动程序。要解决此问题，请检查并确保已安装和配置相应的驱动程序（例如 EATA-DMA 或用于 DPT 卡的 EATA ISA/EISA/PCI）。您可以使用 `lsmod` 命令查看是否已加载相应的模块，并应参阅系统日志中有关 SCSI 驱动程序的引导时错误。

> **提示**
>
> 通常，在执行任何故障排除操作之前，最好对数据进行完整备份。

### RAID 配置显示为 N 个不同的磁盘

如果 RAID 阵列配置不当，其显示的磁盘数量可能与实际安装的磁盘数量不同。对于 DPT 存储管理器，您必须将 RAID 磁盘配置为单个逻辑阵列。使用存储管理器配置控制器时，请使用参数 `/FW0` 启动它，或选择 Solaris 作为操作系统。这将使阵列设置由控制器在内部管理。

### 格式化过程中机器或控制器关闭

如果在磁盘格式化操作期间关闭系统或控制器，某些 RAID 控制器可能会出现严重问题。问题可能非常严重，在某些情况下，磁盘不得不退回给制造商。
