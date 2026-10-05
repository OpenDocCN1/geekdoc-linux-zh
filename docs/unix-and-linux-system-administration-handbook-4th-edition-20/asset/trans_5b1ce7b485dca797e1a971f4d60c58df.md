

## 第 8 章 存储

满足大多数需求。根据美国国防部的分类，它被批准用于低于“机密（secret）”的安全级别。

为什么甚至需要这个功能呢？首先，文件系统通常不会对自身进行物理擦除，因此对磁盘数据执行 `rm -rf *` 会让所有内容完好无损，并可以使用软件工具恢复。在处理要丢弃（目的地是 Ebay 或垃圾桶）的磁盘时，记住这一点至关重要。

其次，手动重写每个扇区可能会留下磁痕迹，拥有实验室访问权限的坚决攻击者可以恢复这些痕迹。安全擦除（Secure erase）会执行所需的多次覆盖，以消除这些影子信号。对于大多数数据中心来说，磁性残留不是一个严重的问题，但知道自己没有将组织的机密数据泄露到广大的世界总是一件好事。

最后，安全擦除具有将 SSD 重置为完全擦除状态的效果。在 ATA TRIM 命令（擦除块的命令）无法发布的情况下，这可能会提高性能，可能是因为 SSD 上的文件系统不知道发布该命令，或者 SSD 是通过不支持传播 TRIM 的主机适配器或 RAID 接口连接的。

遗憾的是，UNIX 对发送安全擦除命令的支持仍然难以捉摸。在目前，最好连接到 Windows 或 Linux 系统进行擦除。用于安全擦除的 DOS 软件可以在 tiny.com/20qqqw 的磁性记录研究中心找到。MHDD 工具通过其更快的命令支持安全擦除——参见 tiny.com/2gcr98。

在 Linux 下，使用 `hard` 命令：

```bash
$ sudo hddm --user-master u --security-set-password /dev/sda8
$ sudo hddum --user-master u --security-erase password /dev/sda
```

SCSI 安全擦除命令中没有类似的命令，第 226 页“格式化和坏块管理”下描述的 SCSI “format unit”命令是一个合理的替代方案。另一个选项是使用 `dd if=/dev/zero of=disk bs=8k` 将磁盘扇区置零。

许多系统都有 `shred` 工具，尝试保护单个文件的内容。它基于这样一个假设：文件块可以在原地被覆盖。这一假设在许多情况下是的（任何 SSD 上的任何文件系统、任何带有快照的逻辑卷，或许通常情况下（在 ZFS 上）`shred` 的通用性是有疑的）。

对于对整个 PC 系统进行清理的另一个选项，该工具从自己的磁盘运行，因此它不是你每天使用的工具。它对于硬件退役非常方便，

- 8. ATA 安全擦除命令受密码保护，以增加访问难度。因此，在调用命令之前必须设置磁盘密码。不过，不必费心恢复密码；你可以随意重置它。没有锁定磁盘的危险。

### hdparm：设置磁盘和接口参数 (Linux)

# hdparm:设置磁盘和接口参数 (Linux)

Linux 的 `hdparm` 命令不仅仅可以发送安全擦除命令。它是与 SATA、IDE 和 SAS 硬盘的固件交互的通用方法。除此之外，hdparm 可以设置驱动电源选项、启用或禁用降噪选项、设置只读标志并打印详细信息。一些选项在 SCSI 磁盘上同样有效（在当前的 Linux 内内核下）。

语法为：

```bash
hdparm [options] device
```

有许多可用选项，但大多数只对驱动程序和内核开发者感兴趣。表 8.3 显示了一些与管理员相关的选项。

### 表 8.3 适用于管理员的实用 hdparm 选项

| 选项 | 功能 |
| :--- | :--- |
| -I* | 倾储大量的标识和状态信息 |
| -M value | 设置声学管理选项 |
| -S value | 设置自动待机（停转）模式的时间延迟 |
| -y | 立即将磁盘置待机模式 |
| -C | 查询磁盘当前的电源管理状态 |
| -T | 快速测试接口带宽（无实际磁盘读取） |
| -t | 快速测试整体盘片到主机的顺序读取 |

a. 这是一个大写字母 "i"，如 India 中的 i。

使用 `hdparm -I` 验证每个驱动器是否在使用最快的 DMA 传输模式。hdparm 列出了所有支持的模式并用星号标出当前激活的模式，如下例。

```bash
linux$ hdparm -I /dev/sda
```

```text
/dev/sda:
ATA device, with non-removable media
Model Number: WDC1001FALS-0OJ7B0
Serial Number: WD-WMATV0998277
Firmware Revision: 05.00K5
Transport: Serial, SATA 1.0A, SATA II Extensions, SATA Rev 2
```

```text
Capabilities:
LBA, IORY(can be disabled)
Queue depth: 32
Standby timer values: spec'd by Standard, with device specific
R/W multiple sector transfer: Max = 16 Current = 16
Recommended acoustic management value: 128, current value: 254
DMA: mdma0 mdma1 mdma2 udma0 udma1 udma2 udma3 udma4
udma5 *udma6
```

## 第 8 章 存储

周期时间: min=120ns recommended=120ns
PIO: pio0 pio1 pio2 pio3 pio4
周期时间: no flow control=120ns IORDY flow control=120ns

为什么甚至需要这个功能呢？首先，文件系统通常不会对自身进行物理擦除，因此对磁盘数据执行 `rm -rf *` 会让所有内容完好无损，并可以使用软件工具恢复。在处理要丢弃（目的地是 Ebay 或垃圾桶）的磁盘时，记住这一点至关重要。

其次，手动重写每个扇区可能会留下磁痕迹，拥有实验室访问权限的坚决攻击者可以恢复这些痕迹。安全擦除会执行所需的多次覆盖，以消除这些影子信号。对于大多数数据中心来说，磁性残留不是一个严重的问题，但知道自己没有将组织的机密数据泄露到广大的世界总是一件好事。

最后，安全擦除具有将 SSD 重置为完全擦除状态的效果。在 ATA TRIM 命令（擦除块的命令）无法发布的情况下，这可能会提高性能，可能是因为 SSD 上的文件系统不知道发布该命令，或者 SSD 是通过不支持传播 TRIM 的主机适配器或 RAID 接口连接的。

遗憾的是，UNIX 对发送安全擦除命令的支持仍然难以捉摸。在目前，最好连接到 Windows 或 Linux 系统进行擦除。用于安全擦除的 DOS 软件可以在 tiny.com/20qqqw 的磁性记录研究中心找到。MHDD 工具通过其更快的命令支持安全擦除——参见 tiny.com/2gcr98。

在 Linux 下，使用 `hard` 命令：

```bash
$ sudo hddm --user-master u --security-set-password /dev/sda8
$ sudo hddum --user-master u --security-erase password /dev/sda
```

SCSI 安全擦除命令中没有类似的命令，第 226 页“格式化和坏块管理”下描述的 SCSI “format unit”命令是一个合理的替代方案。另一个选项是使用 `dd if=/dev/zero of=disk bs=8k` 将磁盘扇区置零。

许多系统都有 `shred` 工具，尝试保护单个文件的内容。它基于这样一个假设：文件块可以在原地被覆盖。这一假设在许多情况下是的（任何 SSD 上的任何文件系统、任何带有快照的逻辑卷，或许通常情况下（在 ZFS 上）`shred` 的通用性是有疑的）。

对于对整个 PC 系统进行清理的另一个选项，该工具从自己的磁盘运行，因此它不是你每天使用的工具。它对于硬件退役非常方便，

- 8. ATA 安全擦除命令受密码保护，以增加访问难度。因此，在调用命令之前必须设置磁盘密码。不过，不必费心恢复密码；你可以随意重置它。没有锁定磁盘的危险。

### hdparm：设置磁盘和接口参数 (Linux)

# hdparm:设置磁盘和接口参数 (Linux)

Linux 的 `hdparm` 命令不仅仅可以发送安全擦除命令。它是与 SATA、IDE 和 SAS 硬盘的固件交互的通用方法。除此之外，hdparm 可以设置驱动电源选项、启用或禁用降噪选项、设置只读标志并打印详细信息。一些选项在 SCSI 磁盘上同样有效（在当前的 Linux 内内核下）。

语法为：

```bash
hdparm [options] device
```

有许多可用选项，但大多数只对驱动程序和内核开发者感兴趣。表 8.3 显示了一些与管理员相关的选项。

### 表 8.3 适用于管理员的实用 hdparm 选项

| 选项 | 功能 |
| :--- | :--- |
| -I* | 倾储大量的标识和状态信息 |
| -M value | 设置声学管理选项 |
| -S value | 设置自动待机（停转）模式的时间延迟 |
| -y | 立即将磁盘置待机模式 |
| -C | 查询磁盘当前的电源管理状态 |
| -T | 快速测试接口带宽（无实际磁盘读取） |
| -t | 快速测试整体盘片到主机的顺序读取 |

a. 这是一个大写字母 "i"，如 India 中的 i。

使用 `hdparm -I` 验证每个驱动器是否在使用最快的 DMA 传输模式。hdparm 列出了所有支持的模式并用星号标出当前激活的模式，如下例。

```bash
linux$ hdparm -I /dev/sda
```

```text
/dev/sda:
ATA device, with non-removable media
Model Number: WDC1001FALS-0OJ7B0
Serial Number: WD-WMATV0998277
Firmware Revision: 05.00K5
Transport: Serial, SATA 1.0A, SATA II Extensions, SATA Rev 2
```

```text
Capabilities:
LBA, IORY(can be disabled)
Queue depth: 32
Standby timer values: spec'd by Standard, with device specific
R/W multiple sector transfer: Max = 16 Current = 16
Recommended acoustic management value: 128, current value: 254
DMA: mdma0 mdma1 mdma2 udma0 udma1 udma2 udma3 udma4
udma5 *udma6
```

## 第 8 章 存储

周期时间: min=120ns recommended=120ns
PIO: pio0 pio1 pio2 pio3 pio4
周期时间: no flow control=120ns IORDY flow control=120ns

为什么甚至需要这个功能呢？首先，文件系统通常不会对自身进行物理擦除，因此对磁盘数据执行 `rm -rf *` 会让所有内容完好无损，并可以使用软件工具恢复。在处理要丢弃（目的地是 Ebay 或垃圾桶）的磁盘时，记住这一点至关重要。

其次，手动重写每个扇区可能会留下磁痕迹，拥有实验室访问权限的坚决攻击者可以恢复这些痕迹。安全擦除会执行所需的多次覆盖，以消除这些影子信号。对于大多数数据中心来说，磁性残留不是一个严重的问题，但知道自己没有将组织的机密数据泄露到广大的世界总是一件好事。

最后，安全擦除具有将 SSD 重置为完全擦除状态的效果。在 ATA TRIM 命令（擦除块的命令）无法发布的情况下，这可能会提高性能，可能是因为 SSD 上的文件系统不知道发布该命令，或者 SSD 是通过不支持传播 TRIM 的主机适配器或 RAID 接口连接的。

遗憾的是，UNIX 对发送安全擦除命令的支持仍然难以捉摸。在目前，最好连接到 Windows 或 Linux 系统进行擦除。用于安全擦除的 DOS 软件可以在 tiny.com/20qqqw 的磁性记录研究中心找到。MHDD 工具通过其更快的命令支持安全擦除——参见 tiny.com/2gcr98。

在 Linux 下，使用 `hard` 命令：

```bash
$ sudo hddm --user-master u --security-set-password /dev/sda8
$ sudo hddum --user-master u --security-erase password /dev/sda
```

SCSI 安全擦除命令中没有类似的命令，第 226 页“格式化和坏块管理”下描述的 SCSI “format unit”命令是一个合理的替代方案。另一个选项是使用 `dd if=/dev/zero of=disk bs=8k` 将磁盘扇区置零。

许多系统都有 `shred` 工具，尝试保护单个文件的内容。它基于这样一个假设：文件块可以在原地被覆盖。这一假设在许多情况下是的（任何 SSD 上的任何文件系统、任何带有快照的逻辑卷，或许通常情况下（在 ZFS 上）`shred` 的通用性是有疑的）。

对于对整个 PC 系统进行清理的另一个选项，该工具从自己的磁盘运行，因此它不是你每天使用的工具。它对于硬件退役非常方便，

- 8. ATA 安全擦除命令受密码保护，以增加访问难度。因此，在调用命令之前必须设置磁盘密码。不过，不必费心恢复密码；你可以随意重置它。没有锁定磁盘的危险。

### hdparm：设置磁盘和接口参数 (Linux)

# hdparm:设置磁盘和接口参数 (Linux)

Linux 的 `hdparm` 命令不仅仅可以发送安全擦除命令。它是与 SATA、IDE 和 SAS 硬盘的固件交互的通用方法。除此之外，hdparm 可以设置驱动电源选项、启用或禁用降噪选项、设置只读标志并打印详细信息。一些选项在 SCSI 磁盘上同样有效（在当前的 Linux 内内核下）。

语法为：

```bash
hdparm [options] device
```

有许多可用选项，但大多数只对驱动程序和内核开发者感兴趣。表 8.3 显示了一些与管理员相关的选项。

### 表 8.3 适用于管理员的实用 hdparm 选项

| 选项 | 功能 |
| :--- | :--- |
| -I* | 倾储大量的标识和状态信息 |
| -M value | 设置声学管理选项 |
| -S value | 设置自动待机（停转）模式的时间延迟 |
| -y | 立即将磁盘置待机模式 |
| -C | 查询磁盘当前的电源管理状态 |
| -T | 快速测试接口带宽（无实际磁盘读取） |
| -t | 快速测试整体盘片到主机的顺序读取 |

a. 这是一个大写字母 "i"，如 India 中的 i。

使用 `hdparm -I` 验证每个驱动器是否在使用最快的 DMA 传输模式。hdparm 列出了所有支持的模式并用星号标出当前激活的模式，如下例。

```bash
linux$ hdparm -I /dev/sda
```

```text
/dev/sda:
ATA device, with non-removable media
Model Number: WDC1001FALS-0OJ7B0
Serial Number: WD-WMATV0998277
Firmware Revision: 05.00K5
Transport: Serial, SATA 1.0A, SATA II Extensions, SATA Rev 2
```

```text
Capabilities:
LBA, IORY(can be disabled)
Queue depth: 32
Standby timer values: spec'd by Standard, with device specific
R/W multiple sector transfer: Max = 16 Current = 16
Recommended acoustic management value: 128, current value: 254
DMA: mdma0 mdma1 mdma2 udma0 udma1 udma2 udma3 udma4
udma5 *udma6
```

## 8.6 磁盘分区

分区和逻辑卷管理都是将磁盘（或在 LVM 的情况下为磁盘池）划分为已知大小独立块的方法。我们所有的示例都支持逻辑卷管理，但只有 Linux、Solaris 以及有时的 HP-UX 允许传统的分区。

