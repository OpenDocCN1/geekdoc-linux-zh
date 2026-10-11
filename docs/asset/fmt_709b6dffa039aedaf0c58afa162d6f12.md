
```
mknod /dev/hda2 3 2
```

`b 3 2` 指定一个主号为 3、从号为 2 的块设备。对于字符设备或命名管道，请使用 `c` 或 `p` 代替 `b`。`mknod` 命令仅用于创建缺失的设备或命名管道。随着你升级系统并添加设备驱动程序，你可能需要创建全新的设备组。由于设备非常多，最好使用 `MAKDEV` 程序（在 `/dev` 中可以找到）来创建设备组。设备组可以根据多个设备名称的共同部分命名，例如 `hda`，或者它们有一个完全独立的名称，例如 `std-hd`。例如，要创建所有以 `hda` 开头的设备，运行此命令：

```
/dev/MAKDEV hda
```

如果设备已经存在于你的系统中，则 `MAKDEV` 命令是安全的。

## devfs

在你费力创建任何设备文件之前，应该先检查是否正在运行 `devfs`，这是一种自动设备文件生成系统。检查 `devfs` 最简单的方法是运行 `mount` 并在输出中查找 `devfs`。

如果你的系统运行着 `devfs`，你不必创建缺失的设备文件，因为内核维护了可用设备文件的目录。Linux 内核通常在启动时配置 `devfs`，启动一个名为 `devfsd` 的特殊辅助程序，赋予管理员自定义设备系统的能力。

`devfs` 是旧版 Linux 内核中的实验性功能，但在最新的 Linux 内核中已被归类为过时。

## 2.3.4 分区磁盘设备

在使用系统的新磁盘之前，你需要知道如何通过其设备文件对磁盘进行分区。如果你从未处理过分区，不要担心。磁盘分区只是磁盘的一个部分。磁盘分区是为了特定的用途，磁盘分区是磁盘的一个部分。磁盘分区是为了特定的用途，磁盘分区是磁盘的一个部分。**（此处原文存在重复内容）由于 Linux 内核通常在启动时配置 `devfs`，启动一个名为 `devfsd` 的特殊辅助程序。** 常见的磁盘设备名称如下：

- `/dev/sda`
- `/dev/sdb`
- `/dev/sdc`
- `/dev/hdd`
- `/dev/sde`
- `/dev/sdf`
- `/dev/sdg`
- `/dev/sdh`
- `/dev/sdi`
- `/dev/sdj`
- `/dev/sdk`
- `/dev/sdl`
- `/dev/sdm`
- `/dev/sdn`
- `/dev/sdo`
- `/dev/sdop`
- `/dev/sdq`
- `/dev/sdr`
- `/dev/sds`
- `/dev/sdt`
- `/dev/sdv`
- `/dev/sdw`
- `/dev/sdx`
- `/dev/sdy`
- `/dev/sdz`
- `/dev/sda1`
- `/dev/sda2`
- `/dev/sda3`
- `/dev/sda4`
- `/dev/sda5`
- `/dev/sda6`
- `/dev/sda7`
- `/dev/sda8`
- `/dev/sda9`
- `/dev/sda10`
- `/dev/sda11`
- `/dev/sda12`
- `/dev/sda13`
- `/dev/sda14`
- `/dev/sda15`
- `/dev/sda16`
- `/dev/sda17`
- `/dev/sda18`
- `/dev/sda19`
- `/dev/sda20`
- `/dev/sda21`
- `/dev/sda22`
- `/dev/sda23`
- `/dev/sda24`
- `/dev/sda25`
- `/dev/sda26`
- `/dev/sda27`
- `/dev/sda28`
- `/dev/sda29`
- `/dev/sda30`
- `/dev/sda31`
- `/dev/sda32`
- `/dev/sda33`
- `/dev/sda34`
- `/dev/sda35`
- `/dev/sda36`
- `/dev/sda37`
- `/dev/sda38`
- `/dev/sda39`
- `/dev/sda40`
- `/dev/sda41`
- `/dev/sda42`

分区是针对特定的用途，磁盘分区是磁盘的一个部分。磁盘分区是为了特定的用途，磁盘分区是磁盘的一个部分。磁盘分区是为了特定的用途，磁盘分区是磁盘的一个部分。磁盘分区是为了特定的用途，磁盘分区是磁盘的一个部分。磁盘分区是为了特定的用途，磁盘分区是磁盘的一个部分。磁盘分区是为了特定的用途，磁盘分区是磁盘的一个部分。磁盘分区是为了特定的用途，磁盘分区是磁盘的一个部分。磁盘分区是为了特定的用途，磁盘分区是磁盘的一个部分。分区例如：

- `/dev/sdb1`
- `/dev/sdb2`
- `/dev/sdb3`
- `/dev/sdb4`
- `/dev/sdb5`
- `/dev/sdb6`
- `/dev/sdb7`
- `/dev/sdb8`
- `/dev/sdb9`
- `/dev/sdb10`
- `/dev/sdb11`
- `/dev/sdb12`
- `/dev/sdb13`
- `/dev/sdb14`
- `/dev/sdb15`
- `/dev/sdb16`
- `/dev/sdb17`
- `/dev/sdb18`
- `/dev/sdb19`
- `/dev/sdb20`
- `/dev/sdb21`
- `/dev/sdb22`
- `/dev/sdb23`
- `/dev/sdb24`
- `/dev/sdb25`
- `/dev/sdb26`
- `/dev/sdb27`
- `/dev/sdb28`
- `/dev/sdb29`
- `/dev/sdb30`
- `/dev/sdb31`
- `/dev/sdb32`
- `/dev/sdb33`
- `/dev/sdb34`
- `/dev/sdb35`
- `/dev/sdb36`
- `/dev/sdb37`
- `/dev/sdb38`
- `/dev/sdb39`
- `/dev/sdb40`
- `/dev/sdb41`
- `/dev/sdb42`

分区是针对特定的用途，磁盘分区是磁盘的一个部分。磁盘分区是为了特定的用途，磁盘分区是磁盘的一个部分。磁盘分区是为了特定的用途，磁盘分区是磁盘的一个部分。磁盘分区是为了特定的用途，磁盘分区是磁盘的一个部分。磁盘分区是为了特定的用途，磁盘分区是磁盘的一个部分。磁盘分区是为了特定的用途，磁盘分区是磁盘的一个部分。磁盘分区是为了特定的用途，磁盘分区是磁盘的一个部分。分区例如：

- `/dev/sdc1`
- `/dev/sdc2`
- `/dev/sdc3`
- `/dev/sdc4`
- `/dev/sdc5`
- `/dev/sdc6`
- `/dev/sdc7`
- `/dev/sdc8`
- `/dev/sdc9`
- `/dev/sdc10`
- `/dev/sdc11`
- `/dev/sdc12`
- `/dev/sdc13`
- `/dev/sdc14`
- `/dev/sdc15`
- `/dev/sdc16`
- `/dev/sdc17`
- `/dev/sdc18`
- `/dev/sdc19`
- `/dev/sdc20`
- `/dev/sdc21`
- `/dev/sdc22`
- `/dev/sdc23`
- `/dev/sdc24`
- `/dev/sdc25`
- `/dev/sdc26`
- `/dev/sdc27`
- `/dev/sdc28`
- `/dev/sdc29`
- `/dev/sdc30`
- `/dev/sdc31`
- `/dev/sdc32`
- `/dev/sdc33`
- `/dev/sdc34`
- `/dev/sdc35`
- `/dev/sdc36`
- `/dev/sdc37`
- `/dev/sdc38`
- `/dev/sdc39`
- `/dev/sdc40`
- `/dev/sdc41`
- `/dev/sdc42`

分区是针对特定的用途，磁盘分区是磁盘的一个部分。磁盘分区是为了特定的用途，磁盘分区是磁盘的一个部分。磁盘分区是为了特定的用途，磁盘分区是磁盘的一个部分。磁盘分区是为了特定的用途，磁盘分区是磁盘的一个部分。磁盘分区是为了特定的用途，磁盘分区是磁盘的一个部分。磁盘分区是为了特定的用途，磁盘分区是磁盘的一个部分。磁盘分区是为了特定的用途，磁盘分区是磁盘的一个部分。分区例如：

- `/dev/hdd1`
- `/dev/hdd2`
- `/dev/hdd3`
- `/dev/hdd4`
- `/dev/hdd5`
- `/dev/hdd6`
- `/dev/hdd7`
- `/dev/hdd8`
- `/dev/hdd9`
- `/dev/hdd10`
- `/dev/hdd11`
- `/dev/hdd12`
- `/dev/hdd13`
- `/dev/hdd14`
- `/dev/hdd15`
