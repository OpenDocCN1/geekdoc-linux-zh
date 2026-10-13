
## Alpha Miniloader 使用教程

变量。MILO 包含一些可以设置的变量，用于帮助启动过程。如果你通过 Windows NT ARC 固件加载，MILO 将利用由该固件设置的启动环境变量。对于某些系统（例如 AlphaPC64），MILO 维护自己的一组在启动之间不会改变的环境变量。这些变量是：

- `MILO> help var`

MILO 关心的变量：
- `MEMORY_SIZE` - 系统内存大小（单位：MB）
- `BOOT_DEV` - 指定默认启动设备
- `BOOT_FILE` - 指定传递给内核的启动字符串
- `BOOT_STRING` - `SCSIN_HOSTID` - 指定第 n 个 SCSI 控制器主机 ID
- `PCI_LATENCY` - 指定 PCI 主设备延迟
- `AUTOBOT` - 如果设置了此项，MILO 将尝试在通电时启动，并仅在失败时进入命令循环。
- `AUTOBOT_TIMEOUT` - 在通电后进行自动启动前等待的秒数。

**注意**：在没有设置超时的情况下设置 `AUTOBOT`，可能会导致在 0 秒超时后就自动启动，这可能不是你想要的结果。

`PCILLATENCY` 是 PCI 总线主设备在获得控制权后在 PCI 总线上等待的 PCI 周期数。默认值为 32，最大值为 255。设置高值意味着设备每次获得 PCI 总线控制权时可以传输更多数据。然而设置高值也意味着设备可能需要更长时间才能获得控制权。

### E.6.2 启动 Linux

`boot` 命令从设备启动 Linux 内核。你需要为 MILO 提供一个位于 EXT2 格式化磁盘（SCSI、IDE 或软盘）或 ISO9660 格式光光上的上的 Linux 内核镜像。镜像可以经过 gzip 压缩，在这种情况下 MILO 会自动对其解压。早期的 MILO 通过 `.gz` 后缀识别 gzip 文件，但后期的 MILO 会在镜像中查找魔数（magic numbers）。

你应该注意，MILO 的版本通常不需要与你加载的 Linux 内核版本匹配。使用以下命令语法启动 Linux：

## MILO 的用户界面

```
MILO> boot [-t file-system] device-name:file-name \
[ [boot-option] [boot-option] ...]
```

`device-name` 是你想要使用的文件名称，`file-name` 是包含 Linux 内核的文件名称。文件名之后提供的所有参数都将直接传递给 Linux 内核。

如果你正在安装 Red Hat，则你需要指定根设备等。你会使用：

```
MILO> boot fd0:vmlinux.gz root=/dev/fd0 load_ramdisk=1
```

MILO 会自动将你配置的块设备包含在你的 `vmlinux` 中。它拥有软盘驱动程序、IDE 驱动程序和许多 SCSI 驱动程序（例如 NIC 810），这些运行良好。此外，将 SCSI 控制器的主机 ID 设置为合理的值也同样重要。默认情况下，MILO 将其初始化为可能的最大值（7），这通常可以工作。然而，如果你有需要，可以通过通过设置环境变量 `SCSIN_HOSTID` 为适当的值，来显式地设置系统中第 n 个 SCSI 控制器的主 ID。例如：

```
setenv SCSIN_HOSTID 7
```

注意将 SCSI 控制器的主机 ID 设置为合理的值。

### E.6.3 重启 Linux

`boot` 命令从设备启动 Linux 内核。你需要为 MILO 提供一个位于 EXT2 格式化磁盘（SCSI、IDE 或软盘）或 ISO9660 格式光光上的上的 Linux 内核镜像。镜像可以经过 gzip 压缩，在这种情况下 MILO 会自动对其解压。早期的 MILO 通过 `.gz` 后缀识别 gzip 文件，但后期的 MILO 会在镜像中查找魔数。

你应该注意，MILO 的版本通常不需要与你加载的 Linux 内核版本匹配。使用以下命令语法启动 Linux：

```
MILO> boot [-t file-system] device-name:file-name \
[ [boot-option] [boot-option] ...]
```

`device-name` 是你想要使用的文件名称，`file-name` 是包含 Linux 内核的文件名称。文件名之后提供的所有参数都将直接传递给 Linux 内核。

如果你正在安装 Red Hat，则你需要指定根设备等。你会使用：

```
MILO> boot fd0:vmlinux.gz root=/dev/fd0 load_ramdisk=1
```

MILO 会自动将你配置的块设备包含在你的 `vmlinux` 中。

它拥有软盘驱动程序、IDE 驱动程序和许多 SCSI 驱动程序（例如 NIC 810），这些运行良好。此外，将 SCSI 控制器的主机 ID 设置为合理的值也同样重要。默认情况下，MILO 将其初始化为可能的最大值（7），这通常可以工作。然而，如果你有需要，可以通过通过设置环境变量 `SCSIN_HOSTID` 为适当的值，来显式地设置系统中第 n 个 SCSI 控制器的主 ID。例如：

```
setenv SCSIN_HOSTID 7
```

### E.6.4 "bootopt" 命令

`bootopt` 命令用于选择在通电时使用的固件类型。在像 AlphaPC64 这样的基于闪存的系统中，你需要使用该命令来更改启动的固件选项。

```
MILO> bootopt
```

**注意**：在没有设置超时的情况下设置 `AUTOBOT`，可能会导致在 0 秒超时后就自动启动，这可能不是你想要的结果。

`bootopt` 命令用于显示闪存中的内容。

```
MILO> bootopt
```

## E.7 运行闪存管理工具

`run` 命令用于运行闪存管理工具。在运行之前，你需要一个可用的设备来运行 MILO 这种压缩镜像。

```
MILO> run fd0:fmu
```

一旦加载，闪存管理工具将给你一个提示符。

### E.7.1 "help" 命令

```
FMU help
environment - 设置包含 MILO 环境变量的
program - 将镜像写入闪存
quit - 退出
list - 列出闪存的内容
bootopt - 选择通电时使用的固件
help - 打印此文本
```

### E.7.2 "list" 命令

`list` 命令显示闪存的使用情况。当存在多个闪存块时，会显示每个闪存块的情况。

```
FMU list
Listing images
Flash image starting at block: 0
Firmware Id: 0 (Evaluation Board Debug Monitor)
Image size is 19148 bytes (3 blocks)
Flash image starting at block: 3
Firmware Id: 1 (Windows NT ARC)
Image size is 277664 bytes (5 blocks)
Flash image starting at block: 8
Firmware Id: 7 (MILO/Linux)
Image size is 217896 bytes (4 blocks)
```

### E.7.3 "program" 命令

闪存管理工具包含一个 MILO 镜像的压缩副本。`program` 命令允许将此镜像写入闪存。该命令允许你退出，但在运行之前，你应该使用 `list` 命令查看放置 MILO 的。如果 MILO 已经在闪存中，那么闪存管理工具将提供覆盖选项。

```
FMU> program
Image is:
  Firmware Id: 7 (MILO/Linux)
  Image size is 217896 bytes (4 blocks)
Found existing image at block 8
Overwrite existing image? (N/y)? y
Do you really want to do this (y/N)? y
  Deleting blocks ready to program: 8 9 10 11
  Programming image into flash
  Scanning Flash blocks for usage
FMU
```

在完成之前，不要关闭系统。

**注意**：我无法强调在这里必须小心，不要覆盖任何可能需要的现有闪存镜像，否则会导致系统失效。一个非常好的规则是永远不要覆盖调试监控器。

### E.7.4 "environment" 命令

此命令选择一个闪存块来包含 MILO 的环境变量。

### E.7.5 "bootopt" 命令

这与 MILO 的 "bootopt" 命令相同，请参见（第 E.6.4 节）。

### E.7.6 "quit" 命令

这其实毫无意义。在闪存管理工具运行并重启系统后，这是返回 MILO（或其他任何程序）的唯一方法。

## E.8 限制。
