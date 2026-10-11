
## 文件系统
MILO 支持三种文件系统：`MSDOS`、`EXT2` 和 `ISO9660`。只要设备可用，MILO 就可以列出、启动或运行存储在其中一个文件系统上的映像。MILO 的默认文件系统是 `EXT2`，因此你需要告诉 MILO 文件系统不是该默认值。所有使用文件名的命令都允许你使用 `-t [filesystem]` 选项传递文件系统。因此，如果你想列出 SCSI CD ROM 的内容，你可能会输入以下内容：

```
MILO> ls -t iso9660 scd0
```

## 变量
MILO 包含一些可设置的变量，有助于引导过程。如果你通过 Windows NT ARC 固件加载，则 MILO 会使用由该固件设置的启动选项环境变量。对于某些系统，MILO（例如，`AlphaPC64`）维护自己的一组环境变量，这些变量在每次启动时不会改变。这些变量是：

```
MILO> help var
MILO 关心的变量：
`MEMORY_SIZE` - 系统内存大小（以兆字节为单位）
`BOOT_DEV` - 指定默认引导设备
`BOOT_FILE` - 指定默认引导文件
`BOOT_STRING` - 指定传递给内核的引导字符串
`SCSIn_HOSTID` - 指定第 n 个 SCSI 控制器的主机 ID。
`PCI_LATENCY` - 指定 PCI 主设备延迟
`AUTOBOOT` - 如果已设置，MILO 将在加电时尝试启动，并仅在失败时进入命令循环。
`AUTOBOOT_TIMEOUT` - 加电时自动引导前等待的秒数。
```

**注意** 如果在未设置超时的情况下设置 `AUTOBOOT`，你可能会在 0 秒超时后自动启动，这可能不是你所想要的。

`PCILLATENCY` 是 PCI 总线主控设备一旦获得控制权后就保持在 PCI 总线上的 PCI 总线周期数。此值的默认值为 32，最大值为 255。设置高值意味着每次设备获得 PCI 总线控制权时都可以传输更多数据。然而，设置高值也意味着设备可能需要等待更长的时间才能获取控制权。

### D.6.2 启动 Linux
`boot` 命令从设备启动 Linux 内核。你需要在 MILO 可用的 `EXT2` 格式磁盘（`SCSI`、`IDE` 或软盘）或 `ISO9660` 格式 CD 上有一个 Linux 内核映像。该映像可以经过 `gzip` 压缩，在这种情况下，MILO 会自动将其解压缩。早期版本的 MILO 通过 `.gz` 后缀识别 `gzip` 文件，但后期的 MILO 查找映像中的魔数。

你应注意，MILO 的版本通常不需要与你加载的 Linux 内核版本匹配。你使用以下命令语法启动 Linux：

```
MILO> boot [-t file-system] device-name:file-name \
[[boot-option] [boot-option] ...]
```

其中 `device-name` 是你希望使用的设备名称，`file-name` 是包含 Linux 内核的文件名。文件名后提供的所有参数都直接传递给 Linux 内核。如果你正在安装 Red Hat，则需要指定根设备等内容。因此你可以使用：

```
MILO> boot fd0:vmlinux.gz root=/dev/fd0 load_ramdisk=1
```

MILO 将自动包含你配置到 `vmlinux` 中的块设备。我测试过软盘驱动程序、`IDE` 驱动程序和几种 `SCSI` 驱动程序（例如，`NCR 810`），它们工作正常。此外，将 `SCSI` 控制器的主机 ID 设置为合理的值也很重要。默认情况下，MILO 会将其初始化为最高可能值（7），这通常工作得很好。但是，如果你愿意，可以通过将环境变量 `SCSIn_HOSTID` 设置为适当值来显式设置系统中第 $n$ 个 `SCSI` 控制器的主机 ID。例如，要将第一个 `SCSI` 控制器的主机 ID 设置为 7，你可以在 MILO 提示符下发出以下命令：

```
setenv SCSI0_HOSTID 7
```

### D.6.3 重启 Linux
你可能想使用 `shutdown -r now` 命令重启正在运行的 Linux 系统。在这种情况下，Linux 内核将控制权返回给 MILO（通过 `HALT CallPAL` 入口点）。MILO 为了这个目的而在内存中保留自身的压缩副本，并检测系统正在通过 `HWRPB`（硬件重启参数块）中持有的信息进行重启。在这种情况下，它开始使用与上次启动 Linux 内核时完全相同的命令进行重启。有一个 30 秒的超时时间，允许你中断此过程并以你希望的任何方式启动任何你希望的内核。

### D.6.4 "bootopt" 命令
对于基于闪存的系统，如 `AlphaPC64`、`EB164` 和 `EB66+`，有几种可能的启动选项，这些选项是使用 `bootopt` 命令更改的。它有一个参数，一个十进制数，表示下次系统断电循环或重置时要启动的映像类型。

- 0 启动评估板调试监视器，
- 1 启动 Windows NT ARC 固件。

为了告诉启动代码从闪存启动 MILO 固件，你需要一个意味着启动第 N 个映像的启动选项。为此，你需要 128 加上 N，因此如果 MILO 是第三个映像，你会使用以下命令：

```
MILO> bootopt 131
```

注意：对此命令务必非常小心。一个好的规则是永远不要将 `bootopt` 设置为 0（评估板调试监视器），而是使用系统的跳线来实现相同的效果。

## D.7 运行闪存管理实用程序
`run` 命令用于运行闪存管理实用程序。在开始之前，你需要一个包含 `updateflash` 程序的对 MILO 可用的设备。这（像 `vminilux` 一样）可以经过 `gzip` 压缩。你需要使用（`run`）命令从 MILO 运行闪存管理实用程序：

```
MILO> run fd0:fm.u.gz
```

一旦加载并初始化，闪存管理实用程序将告诉你一些关于闪存设备的信息，并给你一个命令提示符。同样，`help` 命令最为有用。

```
Linux MILO 闪存管理实用程序 V1.0

闪存设备是 Intel 28f008SA
16 个段，每段 0x10000（65536）字节
正在扫描闪存块的使用情况
块 12 包含环境变量
FMU>
```

注意，在可能存储环境变量且存在多个闪存块的系统（例如，`AlphaPC64`）上，闪存管理实用程序会寻找一个块来存放 MILO 的环境变量。如果这样的块已经存在，闪存管理实用程序会告诉你它的位置。否则，你必须使用 `environment` 命令来设置并初始化一个块。在上面的示例中，闪存块 12 包含了 MILO 的环境变量。

### D.7.1 “help” 命令

```
FWU> help

FWU 命令摘要：

list				- 列出闪存的内容
program			- 将映像编程到闪存中
quit				- 退出
environment		- 设置哪个块应包含环境变量
bootopt num		- 选择下次开机时使用的固件类型
help				- 打印此帮助文本
FWU>
```

*请注意，`environment` 和 `bootopt` 命令仅适用于 `EB66+`、`AlphaPC64`、`EB164` 和 `PC164` 系统（及其克隆系统）。*

### D.7.2 “list” 命令
`list` 命令显示当前闪存的使用情况。如果有多个闪存块，将显示每个闪存块的使用情况。在下例中，你可以看到 Windows NT ARC 正在使用块 4:7 和块 15。

```
FWU> list
Flash blocks:  0:DBM 1:DBM 2:WNT 4:WNT 5:WNT 6:WNT
			7:WNT 8:MILO 9:MILO 10:MILO 11:MILO 12:MILO 13:U 14:U 15:WNT
Listing flash Images
	Flash image starting at block 0:
	Firmware Id:	0 (Alpha Evaluation Board Debug Monitor)
	Image size is 191248 bytes (3 blocks)
	Executing at 0x300000
Flash image starting at block 3:
FMU> program
Image is:
Firmware Id: 7 (MILO/Linux)
Image size is 217896 bytes (4 blocks)
Executing at 0x200000
Found existing image at block 8
Overwrite existing image? (N/Y)? Y
Do you really want to do this (Y/N)? Y
Deleting blocks ready to program: 8 9 10 11
Programming image into flash
Scanning Flash blocks for usage
FMU>
```

### D.7.3 “program” 命令
