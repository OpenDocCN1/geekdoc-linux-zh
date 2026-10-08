

## 第 5 章 proc 文件系统 61

### 5.3.4. /proc/fs

此目录显示已导出的文件系统。如果正在运行 NFS 服务器，输入 `cat /proc/nfs/exports` 将显示共享的文件系统以及授予这些文件系统的权限。有关更多关于使用 NFS 共享文件系统的信息，请参阅第 9 章网络文件系统 (NFS)。

### 5.3.5. /proc/ide/

此目录包含有关系统中 IDE 设备的信息。每个 IDE 通道都表示为一个单独目录，例如 `/proc/ide/ide0` 和 `/proc/ide/ide1`。此外，还有驱动文件，它提供了在 IDE 通道上使用的驱动版本号：

```
ide-cdrom version 4.59
ide-floppy version 0.97
ide-disk version 1.10
```

许多芯片组还在此目录下提供一个信息文件，给出了有关通过通道连接的驱动器的额外数据。例如，通用的 PIIX4 Ultra 33 芯片组会生成 `/proc/ide/piix`，它会告诉你 IDE 通道上的设备是否启用了 DMA 或 UDMA：

| | PIIX4 Ultra 33 芯片组 | |
|---|---|---|---|
| 主通道 | 次要通道 | |
| enabled | enabled | |
| drive0 | drive | drive0 | drive |
| DMA enabled: yes | no | yes | no |
| UDMA enabled: yes | no | no | no |
| UDMA enabled: 2 | X | X | X |
| DMA | | | |
| PIO | | | |

进入 IDE 通道的目录（例如 ide0）可以获得更多信息。channel 文件提供通道号，而 model 文件则告知该通道的总线类型（例如 pci）。

### 5.3.5.1. 设备目录

每个 IDE 通道都是一个设备目录。设备目录的名称与 `/dev/` 目录中的盘符对应。例如，ide0 上的第一个 IDE 驱动器将是 hda。

> 注意
> 在 `/proc/ide/` 目录下有一个指向这些设备目录的符号链接。

每个设备目录都包含一组信息和统计数据。这些目录的内容根据连接的设备类型而异。一些许多设备通用的最有用文件包括：

- cache — 设备缓存。
- capacity — 设备的容量，以 512 字节块为单位。
- driver — 用于控制设备的驱动程序和版本。
- geometry — 设备的物理和逻辑几何。
- media — 设备类型，例如磁盘。
- model — 设备的型号名称或编号。
- settings — 设备当前参数的集合。此文件通常包含很多用的技术信息。标准 IDE 硬盘的示例设置看起来如下：

| name | min | max | mode |
|---|---|---|---|---|
| bios_cyl | 784 | 0 | 65535 | rw |
| bios_head | 255 | 0 | 255 | rw |
| bios_sect | 63 | 0 | 63 | rw |
| breadea_readahead | 4 | 0 | 127 | rw |
| bswap | 0 | 0 | 1 | r |
| current_speed | 66 | 0 | 69 | rw |
| file_readahead | 0 | 0 | 2097151 | rw |
| ide_scsi | 0 | 0 | 1 | rw |
| init_speed | 66 | 0 | 69 | rw |
| io_32_bit | 0 | 0 | 3 | rw |
| keepseats | 0 | 0 | 1 | rw |
| lun | 0 | 0 | 7 | rw |
| max_kb_per_request | 64 | 1 | 127 | rw |
| multcount | 1 | 0 | 8 | rw |
| nicel | 1 | 0 | 1 | rw |
| nowerr | 0 | 0 | 3 | rw |
| number | 0 | 0 | 1 | rw |
| pio_mode | write-only | 0 | 255 | w |
| slow | 0 | 0 | 1 | rw |
| ummaskirq | 0 | 0 | 1 | rw |
| using_dma | 1 | 0 | 1 | rw |

### 5.3.6 /proc/irq/

此目录用于设置 IRQ 亲和性，这允许系统将特定的 IRQ 连接到单个 CPU。或者，它可以排除某个 CPU 不处理任何 IRQ。

每个 IRQ 都有自己的目录，用于对每个 IRQ 进行单独配置。`/proc/irq/proc_cpu_mask` 是一个位掩码，包含了 IRQ 目录中 `sm_affinity` 文件的默认值。sm_affinity 中的值指定了哪些 CPU 处理特定的 IRQ。

有关 `/proc/irq/` 目录的更多信息，请参阅：

```
/usr/src/linux-2.4/Documentation/filesystems/proc.txt
```

### 5.3.7. /proc/net/

此目录提供了各种网络参数和统计的全面视图。每个文件涵盖与系统网络相关的特定范围信息。以下是这些虚拟文件的部分列表：

- arp — 内核的 ARP 表。此文件对于将系统上的硬件地址连接到 IP 地址特别有用。
- atm — 包含具有各种异步传输模式 (ATM) 设置和统计文件的目录。此目录主要用于 ATM 和 ADSL 线路。
- dev — 列出系统中配置的各种网络设备，并带有发送和接收统计数据。此文件列出了每个接口接收的字节数、入站和出站包数、看到的错误数、丢弃的包数等。
- dev_multcast — 显示每个设备监听的各种二层组播组。
- igmp — 列出此系统加入的 IP 地址。
- ip_fwchains — 如果使用了 ipchains，此虚拟文件将显示任何当前规则。
- ip_fwnames — 如果使用了 ipchains，列出所有防火墙链名称。
- ip_masquerade — 提供 ipchains 下伪装信息的表。
- ip_mr_cache — 列出组播路由缓存。
- ip_mr_vif — 列出组播接口。
- netstat — 广泛的网络统计数据，包括 TCP 超、发送和接收的 SYN cookie 等。
- psched — 列出全局调度器参数。
- raw — 列出原始统计。
- route — 列出路由统计。
- rt_cache — 包含路由缓存。
- snmp — 简单网络管理协议 (SNMP) 数据。
- sockstat — 提供套接统计数据。
- tcp — 包含 TCP 统计数据。
- tr_if — 列出路由表。
- udp — 包含 UDP 统计数据。
- unix — 列出 unix 域。

### 5.3.8. /proc/scsi/

每个 IDE 通道都是一个设备目录。设备目录的名称与 `/dev/` 目录中的盘符对应。例如，ide0 上的第一个 IDE 驱动器将是 hda。

> 注意
> 在 `/proc/ide/` 目录下有一个指向这些设备目录的符号链接。

每个设备目录都包含一组信息和统计数据。这些目录的内容根据连接的设备类型而异。一些许多设备通用的最有用文件包括：

