
### RAID 1
`RAID 1` 也称为镜像（mirroring），通过向两个或多个磁盘写入数据来提供冗余。级别 1 阵列的读取性能通常更快，写入性能比单个磁盘慢，但如果任何一个磁盘故障，数据就不会丢失。这是一个很好的入门级系统，因为只需要两个磁盘。另一方面，由于数据被完全复制，每 GB 成本相对较高。

### RAID 0+1
这种级别在原始论文中从未提到过，但它是它的逻辑扩展。它是镜像与条列的结合，提供了完整的冗余，以及每个数据副本使用条列的性能。这种 RAID 级别的每 GB 成本与 `RAID 1` 相同，但性能往往更好。

### RAID 2
`RAID 2` 使用汉明纠码（Hamming error codes），旨在用于没有内置错误检测的驱动器。所有 SCSI 磁盘都支持内置错误检测，因此在使用 SCSI 磁盘时这种级别几乎没用。

### RAID 3
`RAID 3` 在字节级上在多个磁盘上进行数据条列，校验信息存储在一个磁盘上。它在其他方面与级别 4 相似。字节条列需要硬件支持才能高效使用。

### RAID 4
`RAID 4` 在块级上在多个磁盘上进行数据条列，校验信息存储在一个磁盘上。校验信息允许从单个驱动器的故障中恢复。4 级阵列的读取性能非常好（与 0 级相同）。然而，写入操作每次都需要更新校验数据。这会减慢小数据的写入，尽管大数据的写入或顺序写入相当快。由于阵列中只有一个驱动器存储冗余数据，4 级阵列的每兆字节成本可以相当低。

### RAID 5
`RAID Level 5` 与 4 级相似，但它将校验数据分布在各个驱动器之间。这在多处理系统中可以加速小数据写入，因为校验盘不会成为瓶颈。然而，由于读取时必须在每个驱动器上跳过校验数据，因此读取性能往往低于 4 级阵列。每兆字节成本与 4 级相同。

### 3.2.3 硬件 RAID 与 软件 RAID

随着 Tru64 UNIX 5.0 中实现的 LSM 更改，你会发现使用硬件和/或软件 RAID 能够做（以及应该做）的事情，其界限已变得相当模糊。像往常一样，在决定是使用软件实现还是硬件实现 RAID 时，需要考虑权衡。

在决定使用硬件还是软件实现 RAID 时，通常必须在性能、复杂性和灵活性这三个主要因素之间进行选择。这些因素中任何一个的改变都可能对其他因素产生不利影响。以下是一些（通过丰富经验获得的）建议，旨在为你决定硬件或软件 RAID 解决方案时提供帮助。

首先，作为一个通用规则，性能最高的 RAID 应该在硬件（智能控制器固件）中实现，但使用像 `LSM` 这样的卷管理器实现 RAID 可以获得更大的灵活性。因此，当性能是首要因素时，应尽可能在硬件中实现 RAID。这不仅能提供最佳性能，还能减少方案的复杂性。任何复杂性的减少都有助于系统管理人员处理设备故障。复杂系统可能会以不可预测的方式故障，因此简单往往意味着更好。另一方面，如果灵活性是首要目标，那么软件 RAID 是明显的选择。

其次，不要过度实现 RAID。我们有许多选项可以选择，包括 `LSM`、硬件 RAID 控制器和 AdvFS 文件条带（file striping）。因此，很容易在错误的层级实现 RAID，从而在无意中降低性能、增加复杂性或降低可用性。

例如，如果镜像在硬件层面实现，同时在 LSM 设备之间也实现，那么在牺牲磁盘空间的情况下，几乎没有获得可用性的提升。另一个愚蠢的例子是在硬件 RAID 控制器上的条带集（stripe set），它可以被切分成碎片并使用 `LSM` 再次条带化。这种额外的条带化实际上会降低写入性能，而不是如预期的那样提高它。这就像为了第二次获得更小的文件而对文件进行两次压缩。结果通常是更大的文件。RAID 实现中也会发生同样的情况。过好的东西实际上可能会产生适得其反的效果。

第三，注意在适当层级实现 RAID。例如，在 5.0 版本之前，`LSM` 不支持 `RAID 5`，仅支持 `RAID` 级 0、1 和 0+1。然而，区分“可以做的”和“应该实现的”之间的区别是重要的。我们认为应该实现软件 RAID 5 的情况非常有限。`LSM` 的 `RAID 5` 实现开销低且提供了冗余，但当 I/O 性能是一个重要因素时，我们不建议使用基于软件的 `RAID 5`。在这种情况下，应该使用硬件 `RAID 5` 以最大化性能并减少复杂性。

第四，在某些情况下，结合软件和硬件 RAID 可能是最佳选择。例如，硬件 RAID 无法提供某些冗余（例如跨总线的镜像），因此软件解决方案可能是唯一的选择。

## Tru64 UNIX 设备管理

本节介绍了理解 Tru64 中设备所需的概念。在很大程度上，Tru64 UNIX 在某些方面与其他 UNIX 变体相似，在另一些方面又不同。理解这些相似和不同之处非常重要，以便对文件系统进行彻底覆盖。我们将从设备管理的概括性开始，但我们的最终目标是深入讨论磁盘设备的管理，因为这些是文件系统管理中使用的设备。

我们在这里只讨论版本 5.0 的设备命名和结构。从 5.0 开始，Tru64 UNIX 设备管理发生了巨大变化，不仅是从用户的角度（因为命名方案发生了变化），而且在内核中也是如此。需要进行更改主要有两个原因。首先，这些更改是为了启用 TruCluster 5.x 单系统映像 (SSI)，这意味着磁盘和磁带设备在整个集群中是一致的。其次，这些更改是为了支持 SCSI 宽设备和光纤通道。为了支持这些新需求，必须更改旧的设备命名方案。

### 3.3.1 Tru64 UNIX 中的设备特殊文件

与任何操作系统一样，Tru64 UNIX 设备文件位于根文件系统的 `/dev` 或 `/devices` 目录。设备文件代表用户级进程进入设备驱动程序的“句柄”，驱动程序控制系统上的各种硬件设备。每个设备驱动程序都被分配一个主号（major number），该主号在内核中唯一定义了它。主号偏移到两个名为切换表（switch tables）的表中，这些表定义了在设备上允许的操作。我们之所以有两个切换表，是因为一个用于字符设备，另一个用于块设备设备文件；一个设备可能同时关联一个字符设备文件，但所支持的操作将是不同的，因此执行这些操作的代码也会不同。

Tru64 UNIX 上的 SCSI 设备命名传统上遵循 BSD 方法。Tru64 UNIX 5.0 的命名方案与旧版本相比发生了显著变化。在新方法中，所有集群设备都使用主号 19。这极大地简化了设备管理。除了设备命名外，表 3.1 列出了常用的设备类型。

### Tru64 UNIX 的设备特殊文件

| 设备 | 描述 |
| :--- | :--- |
| `/dev/disk/disk[x]` | SCSI 磁盘特殊设备 |
| `/dev/rdisk/disk[x]` | SCSI 磁盘字符设备 |
| `/dev/tape/tape[x]_d[y]` | SCSI 磁带字符（回卷）设备 |
| `/dev/ntape/tape[x]_d[y]` | SCSI 磁带字符不回卷设备 |
| `/dev/disk/floppy[x]` | 软磁盘块特殊设备 |
| `/dev/rdisk/floppy[x]` | 软磁盘字符设备 |
| `/dev/disk/cdrom[x]` | CD-ROM 块特殊设备 |
| `/dev/rdisk/cdrom[x]` | CD-ROM 字符设备 |

正如大多数 UNIX 管理员所知，设备分为两种：字符和块。字符特殊文件用于按字符读取和写入设备。这种类型设备示例是终端 (`tty`) 或 SCSI 磁带 (`tz`)。另一方面，块设备必须以磁盘块（512 字节）为单位进行访问。典型的 Tru64 UNIX 系统上看到的块设备是如 SCSI 硬盘、CD-ROM 和软磁盘。在本节中，我们将讨论这些不同的设备（磁盘和磁带）。

### 3.3.2 SCSI 磁盘

SCSI 磁盘是计算机系统中存储和检索文件的最设备。在 Tru64 UNIX 系统上，SCSI 磁盘通常包含在架上或内部安装在系统机内。根据应用程序的需求，磁盘可以使用原始方式或块面向的方式使用。如果使用原始磁盘，应用程序（例如商业数据库产品）必须跟踪磁盘结构并管理可用空间。通常，磁盘将以块面向的方式使用，因此它们上将有文件系统。

## Tru64 UNIX 中磁盘设备名称格式如下：

设备名称格式：

- `/dev/disk/dskXP`
- `/dev/rdisk/dskXP`

其中上述助符指的是以下内容：

- `P` = 分区（Partition）。这是一个从 a 到 h 的小写字母，表示第一到第八个分区。
- `X` = 簇范围内唯一的设备设备编号。

### 示例

这里我们展示了一个在 Tru64 UNIX 5.x 系统上查看设备文件的示例。该设备位于总线 #2、目标 #6、LUN 0，且设备类型为 ZR28D。

```
# cd /disk/dsk46*
# ls -1 *disk/dsk46*
brw-- 1 root  system 19593 Mar 15 11:04 disk/dsk46a
brw-- 1 root  system 19595 Mar 15 11:04 disk/dsk46b
brw-- 1 root  system 19597 Mar 15 11:04 disk/dsk46c
brw-- 1 root  system 19599 Mar 15 11:04 disk/dsk46d
brw-- 1 root  system 19601 Mar 15 11:04 disk/dsk46e
brw-- 1 root  system 19603 Mar 15 11:04 disk/dsk46f
brw-- 1 root  system 19605 Mar 15 11:04 disk/dsk46g
brw-- 1 root  system 19607 Mar 15 11:04 disk/dsk46h
crw-- 1 root  system 19594 Mar 15 11:04 rdisk/dsk46a
crw-- 1 root  system 19596 Mar 15 11:04 rdisk/dsk46b
crw-- 1 root  system 19598 Mar 15 11:04 rdisk/dsk46c
crw-- 1 root  system 19600 Mar 15 11:04 rdisk/dsk46d
crw-- 1 root  system 19602 Mar 15 11:04 rdisk/dsk46e
crw-- 1 root  system 19604 Mar 15 11:04 rdisk/dsk46f
crw-- 1 root  system 19606 Mar 15 11:04 rdisk/dsk46g
crw-- 1 root  system 19608 Mar 15 11:04 rdisk/dsk46h
# file rdisk/dsk46a
disk/dsk46a character (19/594) SCSI #2 ZR28 disk
#1 (SCSI ID #6) (SCSI LUN #0)
```

### 3.3. SCSI 磁带

SCSI 磁带设备名称如表 3.1 所示。在此表中，“x”表示设备编号，“y”表示密度代码。通常，“y”的数值越小，表示磁带设备支持的密度越高，数值越大密度越低。系统的默认设备选项由磁带 `tape0` 指定。它被许多以磁带为对象的实用程序作为第一个设备。

### 示例

此示例显示了单个磁带设备设备特殊文件的 `ls -l` 输出。这里我们展示了主设备号对所有设备保持不变，但从设备号用于指定指定的设备和密度代码。密度代码取决于所使用的磁带驱动器类型而变化很大。对于所有磁带设备，都有八密度代码，但并非所有的代码都适用于特定类型的磁带设备。有关所使用的 Tru64 UNIX 支持的磁带驱动器密度代码的更多信息，请参见 `tz(5)` 参考页面。

```
# cd /dev
# ls -l /dev/*tape/tape0*
crw-rw-rw- 1 root system 19,258 Mar 22 08:59 /dev/ntape/tape0
crw-rw-rw- 1 root system 19,262 Mar 22 08:59 /dev/ntape/tape0
crw-rw-rw- 1 root system 19,264 Mar 22 08:59 /dev/ntape/tape0_d1
crw-rw-rw- 1 root system 19,266 Mar 22 08:59 /dev/ntape/tape0_d2
crw-rw-rw- 1 root system 19,268 Mar 22 08:59 /dev/ntape/tape0_d3
crw-rw-rw- 1 root system 19,270 Mar 22 08:59 /dev/ntape/tape0_d4
crw-rw-rw- 1 root system 19,272 Mar 22 08:59 /dev/ntape/tape0_d5
crw-rw-rw- 1 root system 19,274 Mar 22 08:59 /dev/ntape/tape0_d6
crw-rw-rw- 1 root system 19,276 Mar 22 08:59 /dev/ntape/tape0_d7
crw-rw-rw- 1 root system 19,260 Mar 22 08:59 /dev/ntape/tape0_c
crw-rw-rw- 1 root system 19,257 Mar 22 08:59 /dev/tape/tape0
crw-rw-rw- 1 root system 19,261 Mar 22 08:59 /dev/ntape/tape0_d0
crw-rw-rw- 1 root system 19,265 Mar 22 08:59 /dev/ntape/tape0_d1
crw-rw-rw- 1 root system 19,267 Mar 22 08:59 /dev/ntape/tape0_d2
crw-rw-rw- 1 root system 19,269 Mar 22 08:59 /dev/ntape/tape0_d3
crw-rw-rw- 1 root system 19,267 Mar 22 08:59 /dev/ntape/tape0_d4
crw-rw-rw- 1 root system 19,271 Mar 22 08:59 /dev/ntape/tape0_d5
```

```
crw-rw-rw- 1 root system 19,273 Mar 22 08:59 /dev/tape/tape_d6
crw-rw-rw- 1 root system 19,275 Mar 22 08:59 /dev/tape/tape_d7
crw-rw-rw- 1 root system 19,259 Mar 22 08:59 /dev/tape/tape0_c
```

### 示例

此示例显示了上一个示例中磁带设备的文件(1)输出。

```
# file /dev*/tape/tape0*
/dev/ntape/tape0: character special (19/258) SCSI #1 "TZ89" tape #2 (SCSI ID #0) (SCSI LUN #2) offline
/dev/ntape/tape_d0: character special (19/262) SCSI #1 "TZ89" tape #2 (SCSI ID #0) (SCSI LUN #2) offline
/dev/ntape/tape_d1: character special (19/264) SCSI #1 "TZ89" tape #2 (SCSI ID #0) (SCSI LUN #2) offline
/dev/ntape/tape_d2: character special (19/266) SCSI #1 "TZ89" tape #2 (SCSI ID #0) (SCSI LUN #2) offline
/dev/ntape/tape_d3: character special (19/268) SCSI #1 "TZ89" tape #2 (SCSI ID #0) (SCSI LUN #2) offline
/dev/ntape/tape_d4: character special (19/270) SCSI #1 "TZ89" tape #2 (SCSI ID #0) (SCSI LUN #2) offline
/dev/ntape/tape_d5: character special (19/272) SCSI #1 "TZ89" tape #2 (SCSI ID #0) (SCSI LUN #2) offline
/dev/ntape/tape_d6: character special (19/274) SCSI #1 "TZ89" tape #2 (SCSI ID #0) (SCSI LUN #2) offline
/dev/ntape/tape_d7: character special (19/276) SCSI #1 "TZ89" tape #2 (SCSI ID #0) (SCSI LUN #2) offline
/dev/ntape/tape_d8: character special (19/278) SCSI #1 "TZ89" tape #2 (SCSI ID #0) (SCSI LUN #2) offline
/dev/tape/tape0: character special (19/257) SCSI #1 "TZ89" tape #2 (SCSI ID #0) (SCSI LUN #2) offline
/dev/tape/tape_d0: character special (19/261) SCSI #1 "TZ89" tape #2 (SCSI ID #0) (SCSI LUN #2) offline
/dev/tape/tape_d1: character special (19/263) SCSI #1 "TZ89" tape #2 (SCSI ID #0) (SCSI LUN #2) offline
/dev/tape/tape_d2: character special (19/265) SCSI #1 "TZ89" tape #2 (SCSI ID #0) (SCSI LUN #2) offline
```

### 3.3 Tru64 UNIX 设备管理
