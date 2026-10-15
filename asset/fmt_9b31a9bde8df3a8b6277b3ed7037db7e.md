
`LINK` 设置指示您想要访问调制调器卡的设备。如果您希望在安装调制调器设备时由 `init` 启动特定的应用程序，请使用 `INITTAB` 指定插入卡时启动的程序。通常情况下，如果您使用串口 PCMCIA，您可能不想对调制调器这样做，但您可能想要启动必要的软件来接受远程终端的串口连接。

如果您的调制调器在配置卡时需要向 `setscommand` 传递特殊选项，请通过 `SERIAL_OPTS` 设置指定这些选项。可能选项的详情见 `setserial` 手页，可以通过 `man setserial<ENTER>` 命令访问。通常情况下，您不需要指定任何选项。每张 PCMCIA 卡都与一类设备相关——该类别指示了如何配置该卡。当前的 Linux PCMCIA 软件提供七类卡。现代卡属于串行类。

每张 PCMCIA 卡都与一类设备相关——该类别指示了如何配置该卡。当前的 Linux PCMCIA 软件提供七类卡。调制调器使用 `/etc/pcmcm/serial.opts` 脚本配置。该脚本在插入卡时由 `/etc/pcmcm/serial` 脚本调用。您需要编辑 `/etc/pcmcm/serial.opts` 脚本来配置您的调制调器。RedHat Linux 7 上默认的 PCMIA `serial.opts` 脚本如下：

```
# 串行设备配置
#
# 地址格式为 "scheme,socket,instance"。
#
case "$ADDRESS" in
*,*,*)
  INFO="Default modem setup"
  # 指向 dialout设备的符号链接
  LINK="/dev/modem"
  # 'setserial' 的选项
  IRQ='setserial -g /dev/$DEVICE | cut -f 7 -d ' ' -'
  SERIAL_OPTS="irq $IRQ"

# 我们应该为此端口创建 inittab 条目吗？
  #INITTAB="/sbin/mgetty"
  # 弹出策略选项
  NO_CHECK=n
  NO_FUSER=n

esac
```

## 11: 外围设备与硬件的操作

地址格式为“`scheme,socket`”。

```bash
case "$ADDRESS" in
  **)
    #INFO="Sample memory setup"

    #DO_FSTAB="y"; DO_FSCK="y"; DO_MOUNT="y"

    #FSTYPE="ext2"

    #OPTS=""

    #MOUNTPT="/mnt/mem"

    # 卡片弹出策略选项

    NO_CHECK=n

    NO_FUSER=n

    ;;
esac
```

`memory.opts` 文件中的可能设置如表所示：

| 设置名称 | 描述 |
| --- | --- |
| `DO_FSTAB` | 表示是否为该卡在 `/etc/stab` 中创建条目。可能值为 `y` 或 `n`。 |
| `DO_FSCK` | 表示在插入卡时是否应使用 `fsck` 检查内存卡上的文件系统。可能值为 `y` 或 `n`。 |
| `DO_MOUNT` | 表示在插入时是否自动挂载该卡。 |
| `FSTYPE` | 表示该卡的文件系统类型。 |
| `OPTS` | 表示该卡的挂载选项。挂载选项在提示 859，“通过编辑 `fstab` 文件创建新驱动器”中讨论。 |
| `MOUNTPT` | 表示该卡的挂载点。挂载点在提示 859，“通过编辑 `fstab` 文件创建新驱动器”中讨论。 |

## 让 Linux 运行起来：核心技巧与技术

必须意识到 PCMCIA 内存卡的处理方式类似于驱动器或 `CD-ROM` 驱动器：它们被挂载到文件系统的某一点，在该挂载点创建和删除文件，并使用文件目录处理工具进行操作。任何在卡挂载点下创建的文件实际上都会保存在卡上。

某些内存卡包含电路，可以模拟标准的 `IDE` 磁盘。这类内存卡（称为闪存卡）主要分为两大类：

- 闪存转换层（`Flash Translation Layer`）。可以在卡上创建任何类型的文件系统，包括 Linux 原生的 `ext2` 文件系统和 `MS-DOS` 文件系统。
- 微软闪存文件系统（`Microsoft Flash File System`）。这些卡使用 Linux 目前不支持的特定文件系统格式。

要使用闪存转换层闪存内存卡，请执行以下步骤：

1. 使用以下命令在卡上创建一个闪存转换层分区（假设该卡是 `card 0`）：

```bash
# ftl format -i /dev/mem0c0c<Enter>
```

2. 格式化分区：

```bash
# mk2fs /dev/ftl0c0<Enter>
```

3. 将分区挂载到你的卡挂载点（例如 `/mnt/memcard/`）：

```bash
# mount -t ext2 /dev/ftl0c0 /mnt/memcard<Enter>
```

闪存转换层内存卡的设置应在 `/etc/pcmia/ftl.opts` 文件中指定。

### 提示 11.3.8：使用 PCMCIA 硬盘

每个 PCMCIA 卡都与一类设备相关——类别指示了如何配置该卡。当前的 Linux PCMCIA 软件提供七类卡。`IDE` 硬盘卡属于 `ide` 类。

硬盘卡在插入卡片时是使用 `/etc/pcmia/ide.opts` 脚本进行配置的。你需要编辑 `/etc/pcmia/ide.opts` 脚本来配置你的硬盘卡。RedHat Linux 7 上默认的 PCMCIA `ide.opts` 脚本如下：

```bash
# ATA/IDE 适配器配置
#
# 地址格式为 "scheme,socket,serial_no[,part]".
#
# 对于多分区设备，首先返回 $PARTS 中的分区列表。
# 然后，我们将为每个分区调用此脚本。
#
case "$ADDRESS" in
  *,*,*,)

    #INFO="Sample IDE setup"

    #DO_FSTAB="y"; DO_FSCK="y"; DO_MOUNT="y"

    #FSTYPE="msdos"

    #OPTS=""

    #MOUNTPT="/mnt/ide"

    ;;
  *,*,*,)

    #PARTS="1"

    # 卡片弹出策略选项

    NO_CHECK=n

    NO_FUSER=n

    ;;
esac
```

`ide.opts` 文件中的可能设置如表所示：

| 设置名称 | 描述 |
| --- | --- |
| `DO_FSTAB` | 表示是否为该卡在 `/etc/stab` 中创建条目。可能值为 `y` 或 `n`。 |
| `DO_FSCK` | 表示在插入卡时是否应使用 `fsck` 检查内存卡上的文件系统。可能值为 `y` 或 `n`。 |
| `DO_MOUNT` | 表示在插入时是否自动挂载该卡。 |
| `FTYPE` | 表示该卡的文件系统类型。 |
| `OPTS` | 表示该卡的挂载选项在提示 859，“通过编辑 `fstab` 文件创建新驱动器”中讨论。 |
| `MOUNTPT` | 表示该卡的挂载点。挂载点在提示 859，“通过编辑 `fstab` 文件创建新驱动器”中讨论。 |
