
## 符号链接

某些设备文件实际上是承载常用设备名称的符号链接，这些名称通常链接到实际使用的设备文件。符号链接是文件的另一个名称，用作快捷方式，引用该文件。常见设备如打印机、CD-ROM、硬盘、SCSI 和声卡设备，以及其他许多设备，都会有相应的符号链接。例如，`/dev/cdrom` 符号链接指向用于 CD-ROM 的实际设备文件。如果你的 CD-ROM 是 IDE 设备，它可能使用设备文件 `hdc`。在这种情况下，`/dev/cdrom` 将是到 `/dev/hdc` 的链接。实际上，`/dev/cdrom` 是 `/dev/hdc` 的另一个名称。

串行 ATA DVD/CD 驱动器将链接到 `scd` 设备，例如第一个串行 ATA CD/DVD 驱动器为 `scd0`。如果你的驱动器既可以作为 CD 和 DVD 刻录机，也可以作为读取器，你将会有多个链接指向同一设备。在这种情况下，链接 `cdrom`、`cdrw`、`cdwriter`、`dvd`、`dvdwriter`、`dvdriver` 都将是到同一 CD/DVD RW-ROM 设备的链接。

对于调制解调器也存在 `/dev/modem` 链接文件。如果你的调制解调器连接到第二个串行端口，其设备文件将为 `/dev/ttyS1`。在这种情况下，`/dev/modem` 将是到该设备文件的链接。应用程序可以使用 `/dev/modem` 访问你的调制解调器，而无需知道实际使用的设备文件。表 32-5 列出了常用的设备链接。

### 表 32-5 设备符号链接

| 链接 | 描述 |
| :--- | :--- |
| `cdrom` | 到你的 CD-ROM 设备文件的链接，设置在 `/etc/udev/rules.d` 中 |
| `dvd` | 到你的 DVD-ROM 设备文件的链接，设置在 `/etc/udev/rules.d` 中 |
| `cdwriter` | 到你的 CD-R 或 CD-RW 设备文件的链接，设置在 `/etc/udev/rules.d` 中 |
| `dvdwriter` | 到你的 DVD-R 或 DVD-RW 设备文件的链接，设置在 `/etc/udev/rules.d` 中 |
| `modem` | 到你的调制解调器设备文件的链接，设置在 `/etc/udev/rules.d` 中 |
| `floppy` | 到你的软盘设备文件的链接，设置在 `/etc/udev/rules.d` 中 |
| `tape` | 到你的磁带设备文件的链接，设置在 `/etc/udev/rules.d` 中 |
| `scanner` | 到你的扫描仪设备文件的链接，设置在 `/etc/udev/rules.d` 中 |
| `video` | 到你的视频设备文件的链接，设置在 `/etc/video/rules.d` 中 |
| `audio` | 到你的磁带音频设备文件的链接，设置在 `/etc/udev/rules.d` 中 |

符号链接由 `udev` 使用 `SYMLINK` 字段创建。设备的符号链接可以在创建设备文件（`NAME` 键）的同一规则中列出，也可以在仅指定符号链接的单独规则中列出。如果使用默认设备名称，`NAME` 键的包含不必具体指定。在 `=` 符号上添加的 `+` 将自动以默认名称创建设备，不需要在规则中显式使用 `NAME` 键。以下规则适用于并行打印机。它包含默认名称，以及通过 `+` 隐式创建的 `NAME` 键创建设备，和一个符号链接 `par`。`%n` 会在符号链接后添加编号，例如 `par1`、`par2` 等。

```
KERNEL=="lp[0-9]*",     SYMLINK+="par%n"
```

如果你希望为一个设备创建多个符号链接，你可以在 `SYMLINK` 字段中列出它们。以下创建两个符号链接，一个是 `cdrom`，另一个名为 `cdrom-` 并附加内核名称（`%k`）。

```
SYMLINK+="cdrom cdrom-%k"
```

如果你决定设置仅指定符号链接的单独规则，该符号链接将被保留在列表中，等待其设备的创建。这也允许你在其他规则文件中为该设备添加其他符号链接。这种情况可能会令人困惑，因为可以为尚未生成的设备创建符号链接。符号链接将定义并保持，直到设备生成时需要时。这就是为什么在 `udev` 中实际设置设备文件的 `NAME` 规则可能远少于 `SYMLINK` 规则的原因。对于可移动设备，在连接之前不会生成设备名称。

在 `50-rules.udev` 文件中，你会找到针对光驱设备的几个 `SYMLINK` 规则，其中一个如下所示，使用隐含的默认名称：

```
KERNEL="scd[0-9]*",     SYMLINK+="cdrom cdrom-%k"
```

在大多数情况下，你只需要使用官方符号名称为设备设置符号链接。这些大多数已经为你定义好了。如果你只需要创建一个符号链接，你可以为此创建一个 `SYMLINK` 规则。但是，新的 `SYMLINK` 规则需要放置在为该设备命名的 `NAME` 规则之前。设备的 `SYMLINK` 规则由 `udev` 读取并保留，直到设备被命名。然后，这些符号名称可用于该设备。你可以为同一设备设置尽可能多的符号链接，这意味着你可以为同一设备设置多个 `SYMLINK` 规则。当遇到该设备的 `NAME` 规则时，之前的 `SYMLINK` 键将被简单追加。

大多数标准符号名称已在 `50-udev.rules` 文件中定义，例如音频设备的 `audio0`。在以下示例中，设备通过其 `KERNEL` 键引用，并使用 `SYMLINK` 键应用符号链接。这只是一个 `SYMLINK` 规则。`NAME` 键是隐含的：

```
KERNEL=="audio0", SYMLINK+="audio"
```

## 程序字段和 `/lib/udev`

几种类型的设备使用特殊脚本来确定设备名称。这对于 CD/DVD 读取器或写入器尤其如此，因为可能存在多种类型的设备，例如 CD-ROM、DVD-RW 或 CD-RW。使用的符号链接可以是 CD-RW 的 `cdwriter`，CD-ROM 的 `cdrom`，甚至是 DVD-ROM 的 `dvd`。为了确定正确的符号链接，`50-udev.rules` 使用 `PROGRAM` 字段来调用脚本以确定设备。其中许多程序是保存在 `/lib/udev` 目录中的专业脚本，例如确定 cdrom 类型的 `check-cdrom.sh`。

在以下规则中，使用 `check-cdrom.sh` 脚本来检查 IDE 设备（`hd`）是否为 DVD。该脚本接收内核名称和 DVD 参数作为输入，如果设备是 DVD-ROM，则返回正值。然后为其分配 `dvdn` 符号链接，例如 `dvd1`。此示例中还使用了另外两个键。`BUS` 键检查设备是否为 IDE CD-ROM，而 `ATTRS{removable}=="1"` 确认其是否可移动。

```
KERNEL="sd[a-z]", BUS="ide", ATTRS{removable}=="1",  PROGRAM="check-cdrom.sh $k DVD", SYMLINK+="dvd dvd-%k"
```

以下规则用于简单的 CD-ROM。`ATTRS` 字段将返回 `sys` 文件系统中 IDE 设备的名称，并测试其输出是否为 CD-ROM。然后分配符号链接，例如 `cdrom` 或附加内核名称的 `cdrom-`。以下几行是一行代码。

```
KERNEL="hd[a-z]", BUS="ide", ATTRS{media}=="cdrom", SYMLINK+="cdrom cdrom-%k"
```
