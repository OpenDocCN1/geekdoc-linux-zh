
```
# timedetect set-time "2014-02-14 18:17:16"

# timedetect
Local time: Fri 2014-02-14 18:17:21 PST
Universal time: Sat 2014-02-15 02:17:21 UTC
RTC time: Sat 2014-02-15 02:17:21
Timezone: America/Los_Angeles (PST, -0800)
NTP enabled: n/a
NTP synchronized: no
RTC in local TZ: no
DST active: no
Last DST change: DST ended at
Sun 2013-11-03 01:59:59 PDT
Sun 2013-11-03 01:00:00 PST
Next DST change: DST begins (the clock jumps one hour forward) at
Sun 2014-03-09 01:59:59 PST
Sun 2014-03-09 03:00:00 PDT
```

## `parted`：报告并对硬盘进行分区

`parted`（分区编辑器）实用程序用于从命令行报告和操作硬盘分区。`gnome-disks` 实用程序（第 78 页）允许您使用 GUI 执行相同的任务。以下示例中，`parted print` 命令显示 `/dev/sda` 驱动器上分区的信息：

```
# parted /dev/sda print
Model: ATA Hitachi HD512345 (scsi)
Disk /dev/sda: 165GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos

Disk Flags:

Number  Start   End     Size    File system  Type  Flags
  1     32kB    1045MB  1045MB  ext4         primary boot
  2     1045MB  12GB    12GB    ext4         primary
  3     12GB    22GB    10GB    ext4         primary
  4     22GB    165GB   143GB                 extended
  5     22GB    23GB    1045MB  linux-swap(v1) logical
  6     23GB    41GB    18GB    ext4         logical
  7     41GB    82GB    41GB    ext4         logical
```

图 15-3 以图形方式描绘了本示例中显示的分区。`parted` 显示的前几行包含型号名称、设备名称、设备容量以及设备上的分区表类型。在该信息之后，`print` 命令显示以下列：

- **Number**—持有该分区的设备的主设备号码（第 517 页）。此号码与设备名称中的最后一个数字相同。在示例中，5 对应 `/dev/sda5`。

- **Start**—分区在磁盘上的起始位置。`parted` 实用程序将磁盘上的位置指定为从磁盘起始位置开始的距离（以字节为单位）。因此，分区 3 从磁盘起始位置 12 吉字节处开始。

![Figure 15-3](img/243613168ac865b539f12460d966088e_671_0.png)

- **End**—分区在磁盘上的结束位置。尽管 `parted` 显示分区 2 在距磁盘起始位置 12 吉字节处结束，而分区 3 在同一位置开始，但 `parted` 确保这两个分区在此单一字节处不会重叠。

- **Size**—分区大小，单位为千字节 (kB)、兆字节 (MB) 或吉字节 (GB)。

- **Type**—分区类型：主分区、扩展分区或逻辑分区。有关分区的更多信息，请参阅图 15-3 和第 37 页。

- **File system**—文件系统类型：`ext2`、`ext3`、`ext4`、`fat32`、`linux-swap` 等。有关文件系统类型的列表，请参阅第 519 页的表 11-1。

- **Flags**—为该分区开启的标志，包括 `boot`、`raid` 和 `lvm`。在示例中，分区 1 可引导。

在前面的示例中，分区 4 定义了一个扩展分区，包含 165 吉字节硬盘中的 143 吉字节（图 15-3）。如果不影响其中的所有逻辑分区，您无法对扩展分区进行修改。

### 注意

**`parted` 可能会破坏一切**

使用 `parted` 时要像使用格式化硬盘的实用程序一样小心。使用 `parted` 所做的更改很容易导致大量数据丢失。如果您正在使用 `parted` 并且对所做操作有任何疑问，请在进行任何更改之前使用 `q` 命令退出。当您输入命令时，`parted` 会立即执行您所请求的更改。

除了报告硬盘布局和大小之外，您还可以使用 `parted` 交互式地修改磁盘布局。以这种方式使用 `parted` 时要格外小心，并始终在开始使用此实用程序之前备份系统。

更改磁盘上的分区信息（*分区表*）可能会破坏磁盘上的信息。在尝试修改分区表之前，请阅读 `parted info` 页面。

要对磁盘进行分区，请键入命令 `parted`，后跟您想要操作的设备名称。在以下示例中，启动 `parted` 后，用户输入 `help`（或仅 `h`）命令，显示 `parted` 命令的列表：

```
# parted /dev/sda
GNU Parted 3.1
Using /dev/sda
Welcome to GNU Parted! Type 'help' to view a list of commands.
(parted) help
align-check TYPE N		check partition N for TYPE(min|opt) alignment
help [COMMAND]		print general help, or help on COMMAND
mklabel, mktable LABEL-TYPE	create a new disklabel (partition table)
mkpart PART-TYPE [FS-TYPE] START END	make a partition
name NUMBER NAME		name partition NUMBER as NAME
print [devices|free|list,all] [NUMBER]	display the partition table, available devices, free space, all found partitions, or a particular partition
quit				exit program
rescue START END		rescue a lost partition near START and END
rm NUMBER			delete partition NUMBER
select DEVICE		choose the device to edit
disk_set FLAG STATE		change the FLAG on selected device
disk_toggle [FLAG]		toggle the state of FLAG on selected device
set NUMBER FLAG STATE	change the FLAG on partition NUMBER
toggle [NUMBER [FLAG]]		toggle the state of FLAG on partition NUMBER
unit UNIT			set the default unit to UNIT
version			display the version number and copyright information ...
(parted)
```

在 `help` 命令后跟随 `parted` 命令的名称，以显示有关该命令的更多详细信息。当您输入 `print`（或仅 `p`）命令时，`parted` 会显示当前分区信息，正如在命令行上输入 `print` 命令那样。

`parted` 实用程序不允许您设置重叠的分区（逻辑分区与其包含的扩展分区重叠除外）。同样，它也不允许您创建从磁盘最开头（柱面 0）开始的分区。这两种情况都可能导致数据丢失。

以下是在为磁盘定义分区表时需记住的指导原则。更多信息请参阅第 39 页的“对磁盘进行分区”。

- 除非您愿意丢失扩展分区内所有逻辑分区上的所有数据，否则不要删除或定义扩展分区的分区。

- 如果将 `/boot` 放在单独的分区上，建议将其放在驱动器开头（分区 1），以避免 Linux 不得不从驱动器中位置过深的分区启动的问题。一旦磁盘空间允许，将每个主要文件系统放在单独的分区上是可取的。许多人选择将 `/`（根）、`/var` 和 `/usr` 合并到一个分区中，这通常会导致更少的浪费空间，但可能极少见的情况会导致问题。有关更多信息，请参阅第 39 页的“手动分区：规划分区”。

- 尽管 `parted` 可以创建某些类型的文件系统，但通常最简单的做法是使用 `parted` 创建分区，然后使用 `mkfs` 和 `mkswap` 在这些分区上创建文件系统。

以下命令序列在一个干净的磁盘上将分区 1 定义为一个 50GB 的可启动 Linux 分区：

```
# parted /dev/sd
GNU Parted 3.1
Using /dev/sd
Welcome to GNU Parted! Type 'help' to view a list of commands.
(parted) mkpart            (create new partition)
Partition type?  primary/extended?  primary      (select primary partition)
File system type?  [ext2|7] ext4                (set up an ext4 filesystem)
Start? 1                              (start at the beginning of the disk)
End? 50g                              (specify a 50-gigabyte partition)
(parted) help set              (use help to check the syntax of the set command)
   set NUMBER FLAG STATE      change the FLAG on partition NUMBER
   NUMBER is the partition number used by Linux. On MS-DOS disk labels, the
   primary partitions number from 1 to 4, logical partitions from 5 onwards.
   FLAG is one of: boot, root, swap, hidden, raid, lvm, lba, hp-service, palo, prep,
   msftres, bios_grub, atvrecb, diag, legacy_boot
   STATE is one of: on, off
(parted) set 1 boot on            (turn on the boot flag on partition 1)
(parted) print                  (verify that the partition is correct)
Model:  VMware, VMware Virtual S (scsi)
Disk /dev/sdb: 215GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags: 

Number Start  End    Size    Type   File system Flags
   1     1049kB 50.0GB 50.0GB  primary               boot

(parted) quit
Information: You may need to update /etc/fstab.
```

在 `parted` 中指定大小时，可以使用后缀 `k`（千字节）、`m`（兆字节）或 `g`（千兆字节）。创建分区后，输入 `print` 命令以查看分区结束的位置。在定义下一个连续分区之前执行此任务，以避免浪费空间。设置完所有分区后，使用 `quit` 命令退出 `parted`。

接下来，在每个需要持有文件系统的分区上创建一个文件系统（`mkfs`，第 467 页）（交换分区除外）。除非有特定理由，否则除交换分区外的所有分区类型均应设为 `ext4`。使用 `mkswap`（第 513 页）在分区上设置交换区域。你可以使用 `e2label`（第 465 页）为分区打标签。

# `logrotate`：管理日志文件

除了删除或截断日志文件外，你可能希望暂时保留这些文件，以备不时之需。`logrotate` 实用程序通过轮转（第 1271 页）、压缩、发送邮件以及按你的指定删除每个文件，自动管理系统日志（及其他）文件。`logrotate` 实用程序由 `/etc/logrotate.conf` 文件控制，该文件设置默认值，并可选择指定要轮转的文件。通常，`logrotate.conf` 中有一个 `include` 语句，指向 `/etc/logrotate.d` 中的特定于实用程序的规范文件。以下是默认的 `logrotate.conf` 文件：

```
$ cat /etc/logrotate.conf
# see "man logrotate" for details
# rotate log files weekly
weekly

# keep 4 weeks worth of backlogs
rotate 4

# create new (empty) log files after rotating old ones
create

# use date as a suffix of the rotated file
dateext

# uncomment this if you want your log files compressed
#compress

# RPM packages drop log rotation information into this directory
include /etc/logrotate.d

# no packages own wtmp and btmp -- we'll rotate them here
/var/log/wtmp {
    monthly
    create 0664 root utmp
    minsize 1M
    rotate 1
}

/var/log/btmp {
    missingok
    monthly
    create 0600 root utmp
    rotate 1
}

# system-specific logs may be also be configured here.
```

`logrotate.conf` 文件为常见参数设置默认值。每当 `logrotate` 读取这些参数之一的其他值时，它会重置默认值。你可以选择每天、每周或每月轮转文件。`rotate` 关键字后面的数字指定你要保留的已轮转日志文件的数量。`create` 关键字使 `logrotate` 创建一个新的日志文件，该文件与刚刚轮转的日志文件具有相同的名称和属性。`dateext` 关键字使 `logrotate` 使用日期作为文件名扩展名。`compress` 关键字（在默认文件中被注释掉）使日志文件使用 `gzip` 进行压缩。`include` 关键字标准的 `/etc/logrotate.d` 目录，用于存放特定于程序的 `logrotate` 规范文件。当你使用 `rpm`（第 548 页）或基于 `rpm` 的实用程序（如 `yum`，第 12 章）安装程序时，`rpm` 会将 `logrotate` 规范文件放入此目录。

`logrotate.conf` 中的最后一组指令处理 `/var/log/wtmp` 和 `/var/log/btmp` 日志文件（`wtmp` 保存登录记录，`btmp` 保存失败的[坏的!]登录尝试记录；你可以使用 `who` 查看这些文件）。关键字 `missingok` 仅*针对此文件*覆盖隐式默认值 `nomissingok`。如果日志文件缺失，此关键字会导致 `logrotate` 继续运行而不发出错误消息。关键字 `monthly` 仅*针对此文件*覆盖默认值 `weekly`。在 `create` 关键字之后，参数建立了新文件的权限、所有者和组。最后，`rotate` 建立应保留一个已轮转的日志文件。

`/etc/logrotate.d/httpd` 文件是一个特定于实用程序的 `logrotate` 规范文件的示例：

```
$ cat /etc/logrotate.d/httpd
/var/log/httpd/*log {
	missingok
	notifempty
	sharedscripts
	delaycompress
	postrotate
	/bin/systemctl reload httpd.service > /dev/null 2>/dev/null || true
	endscript
}
```
