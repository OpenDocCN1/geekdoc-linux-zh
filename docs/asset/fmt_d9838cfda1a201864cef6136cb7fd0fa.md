
该系统与 AlphaPC64 非常相似，只是它不包含可从其中加载 Milo 的闪存。EB64+ 有两个 ROM，其中一个包含 Windows NT ARC 固件（第“从 Windows NT ARC 固件启动”节），另一个包含评估板调试监视器（第“从调试监视器加载”节）。

Aspen Alpine 略有不同，它只有一个 ROM；该 ROM 包含 Windows NT ARC 固件。

### 通用桌面盒（Multia）

这是一种非常紧凑的基于 21066 的预封装系统，包含一个 TGA（21030）图形设备。虽然你可以将半高 PCI 图形卡装入该盒中，但你最好等待 XFree86 对完整 TGA 的支持。它包含 Windows NT ARC 固件，因此从其启动是首选方法（第“从 Windows NT ARC 固件启动”节）。

from Windows NT")。

## EB164

EB164 与其他由 Digital 构建的 Alpha 评估板一样，包含评估板调试监视器（Evaluation Board Debug Monitor），因此可以通过该监视器加载 Milo（见 E.5.2 节：从调试监视器加载）。通常（但并非总是如此），那些设计衍生自这些评估板的系统也包含调试监视器。通常，这些板卡包含 Windows NT ARC 固件（见 E.5.1 节：从 Windows NT ARC 固件启动）。SRM 控制台也可用（见 E.5.5 节：从 SRM 控制台加载 Milo）。还有一种可从 Milo 运行的闪存管理工具，因此一旦 Milo 运行起来，就可以将其刷入闪存（见 E.7 节：运行闪存管理工具）。该系统支持 Milo 环境变量。

这些系统的闪存中有多个由跳线控制的启动映像。跳线组 J1 位于板卡的左下方（假设 Alpha 芯片在顶部）。你使用跳线的组合以及保存在 TOY 时钟 NVRAM 中的启动选项来在启动选项（以及刷入闪存后的 Milo）之间进行选择。

如果 J1 的跳线 SP-11 插入，则启动由启动选项描述的映像。如果 J1 的跳线 SP-11 拔出，则启动评估板调试监视器。

通过评估板调试监视器将映像刷入闪存的过程与 AlphaPC64 完全相同（见 E.5.6 节：AlphaPC64）。

## XL266

XL266 是被称为 Avanti 的一系列系统之一。它有一个包含 Alpha 芯片和缓存的 riser 卡，以直角插入主板。该主板可以替换等效的 Pentium 主板。

这些系统中的某些随附 SRM 控制台，但其他系统，尤其是 XL266，仅随附 Windows NT ARC 固件（见 E.5.1 节：从 Windows NT ARC 固件启动）。

以下是我列出的兼容系统：

- AlphaStation 400 (Avanti)，
- AlphaStation 250，
- AlphaStation 200 (Mustang)，
- XL。有两种型号，XL266 和 XL233，唯一区别在于处理器速度和缓存大小。

注意：我用于开发和测试 Milo 的系统是 XL266，因此这是我能保证唯一可用的系统。然而，从技术上讲，上述所有系统都是等效的；它们拥有相同的支持芯片组和相同的中断处理机制。

## Platform2000

这是一个基于 233MHz 21066 的系统。

## E.6 Milo 的用户界面

一旦你正确安装/加载/运行了 Milo，你会在屏幕上看到 MILO（MIniLOader）提示符。有一个非常简单的界面，你必须使用它来启动特定的 Linux 内核映像。输入“`help`”是个好主意，因为它提供了命令的有用摘要。

### E.6.1 "help" 命令

可能是 Milo 最有用的命令：

```text
MILO> help
MILO command summary:

ls [-t fs] [dev:[dir]]
    - List files in directory on device
boot [-t fs] [dev:file] [boot string]
    - Boot Linux from the specified device and file
run [-t fs] dev:file
    - Run the standalone program dev:file
show
    - Display all known devices and file systems
set VAR VALUE
    - Set the variable VAR to the specified VALUE
unset VAR
    - Delete the specified variable
reset
    - Delete all variables
print
    - Display current variable settings
help [var]
    - Print this help text
```

设备指定为：`fd0`, `hda1`, `hda2`, `sdal`…

如果你想使用除默认*文件系统*（'ext2'）以外的任何东西，请使用 '-t *filesystem-name*' 选项。

使用 '`show`' 命令来显示已知的设备和*文件系统*。

键入 '`help *var*'` 查看变量列表。

**注意** *`bootopt`* 命令仅出现在 AlphaPC64（及类似）系统上。请参考板卡文档以了解其具体含义。

**设备** 直到你使用需要*使用*设备的命令，否则不会发生设备初始化。第一个 *`show`、`ls`、`boot`* 或 *`run`* 命令都会导致 Linux 内部的设备被初始化。设备的命名方式（完全相同）与 Linux 本身命名的方式一样。因此，第一个 IDE 磁盘将被称为 '`hda`'，其第一个分区将是 '`hda1`'。使用 *`show`* 命令来显示可用的设备。

**文件系统** Milo 支持三种*文件系统：MS DOS、EXT2* 和 *ISO9660*。只要设备可用，Milo 就可以*列出、启动*或*运行*存储在这些*文件系统*之一的映像。Milo 的默认*文件系统*是 *EXT2*，因此你必须告诉 Milo 该*文件系统*不是其他类型。所有使用*文件名*的命令都允许你使用 *-t [filesystem]* 选项来指定*文件系统*。因此，如果你想列出 SCSI CD ROM 的内容，你可能会键入以下内容：

*MILO> ls -t iso9660 scd0:*

**变量** Milo 包含一些可设置变量，有助于*引导*过程。如果你通过 Windows NT ARC 固件加载，那么 Milo 使用该固件设置的*引导*选项环境变量。对于某些系统，Milo（例如，AlphaPC64）维护自己的一组环境变量，这些变量不会从*引导*到*引导*改变。这些变量是：

```text
MILO> help var
Variables that MILO cares about:
MEMORY_SIZE  - System memory size in megabytes
BOOT_DEV     - Specifies the default boot device
BOOT_FILE    - Specifies the default boot file
BOOT_STRING  - Specifies the boot string to pass to the kernel
SCSI0_HOSTID - Specifies the host id of the n-th SCSI controller
AUTOBOOT     - If set, MILO attempts to boot on powerup
              and enters command loop only on failure.
AUTOBOOT_TIMEOUT - Seconds to wait before auto-booting on powerup.
```

### E.6.2 启动 Linux

`boot` 命令从设备启动 Linux 内核。你需要在 EXT2 格式化的磁盘（SCSI、IDE 或软盘）或 ISO9660 格式化的 CD 上有一个 Linux 内核映像，并且该映像对 Milo 可用。映像可以是 gzip 压缩的，在这种情况下，Milo 会通过 .gz 后缀识别它是 gzip 压缩的。

你应该注意，Milo 的版本通常不需要与你要加载的 Linux 内核版本匹配。你使用以下命令语法启动 Linux：

```text
MILO> boot [-t file-system] device-name:file-name [boot-option(s)]
```

其中 `device-name` 是你想要使用的设备名称，`file-name` 是包含 Linux 内核的文件名称。在文件名之后提供的所有参数都直接传递给 Linux 内核。

如果你正在安装 Red Hat，那么你需要指定根设备等。因此你会使用：

```text
MILO> boot fd0:vmlinux.gz root=/dev/fd0 load_ramdisk=1
```
