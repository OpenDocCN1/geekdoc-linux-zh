
# modprobe -r snd-hda-intel

除了在系统运行时加载和卸载内核模块外，还可能在内核加载期间更改模块参数，这与向命令传递选项的做法没有太大区别。每个模块都接受特定的参数，但大多数时候建议使用默认值，不需要额外的参数。然而，在某些情况下，有必要使用参数来更改模块的行为，使其按预期工作。

使用模块名称作为唯一参数，`modinfo` 命令会显示给定模块的描述、文件、作者、许可证、标识、依赖项以及可用参数。可以通过将自定义参数包含在文件 `/etc/modprobe.conf` 或目录 `/etc/modprobe.d/` 中扩展名为 `.conf` 的独立文件中，使模块的自定义参数持久化。选项 `-p` 将使命令 `modinfo` 显示所有可用参数并忽略其他信息：

```bash
# modinfo -p nouveau
vram_pushbuf:Create DMA push buffers in VRAM (int)
tv_norm:Default TV norm.
        Supported: PAL, PAL-M, PAL-N, PAL-Nc, NTSC-M, NTSC-J,
            hd480i, hd480p, hd576i, hd576p, hd720p, hd1080i.
        Default: PAL
    NOTE Ignored for cards with external TV encoders. (charp)
nofbaccel:Disable fbcon acceleration (int)
fbcon_bpp:fbcon bits-per-pixel (default: auto) (int)
mst:Enable DisplayPort multi-stream (default: enabled) (int)
tv_disable:Disable TV-out detection (int)
ignorelid:Ignore ACPI lid status (int)
duallink:Allow dual-link TMDS (default: enabled) (int)
hdmi_mhz:Force a maximum HDMI pixel Clock (in MHz) (int)
config:option string to pass to driver core (charp)
debug:debug string to pass to driver core (charp)
noaccel:disable kernel/abi16 acceleration (int)
modeset:enable driver (default: auto, 0 = disabled, 1 = enabled, 2 = headless) (int)
atomic:Expose atomic ioctl (default: disabled) (int)
runpm:disable (0), force enable (1), optimus only default (-1) (int)
```

示例输出显示了模块 `nouveau` 的所有可用参数，该模块是由 *Nouveau 项目* 提供的内核模块，作为 NVIDIA GPU 显卡专有驱动程序的替代方案。例如，选项 `modeset` 允许控制显示分辨率和深度是在内核空间还是用户空间中设置。向文件 `/etc/modprobe.d/nouveau.conf` 添加选项 `nouveau modeset=0` 将禁用 modeset 内核功能。

如果某个模块导致问题，可以使用文件 `/etc/modprobe.d/blacklist.conf` 来阻止加载该模块。例如，要防止自动加载模块 `nouveau`，必须将行 `blacklist nouveau` 添加到文件 `/etc/modprobe.d/blacklist.conf` 中。当安装了专有模块 `nvidia` 并且应使默认模块 `nouveau` 停用边时，需要执行此操作。

> **注意**
> 您可以修改系统中默认已存在的 `/etc/modprobe.d/blacklist.conf` 文件。但是，首选的方法是创建单独的配置文 `/etc/modprobe.d/<module_name>.conf`，该文件将仅包含针对给定内核模块的设置。

## 信息文件和设备文件

命令 `lspci`、`lsusb` 和 `lsmod` 充当前端，用于读取操作系统存储的硬件信息。这类信息保存在目录 `/proc` 和 `/sys` 中的特殊文件里。这些目录是挂载点，指向不存在于设备分区中，而仅存在于内核用于存储运行时配置和运行中进程信息的 RAM 空间中的文件系统。这些文件系统不用于常规文件存储，因此被称为伪文件系统，并且仅在系统运行时存在。`/proc` 目录包含有关运行中进程和硬件资源信息的文件。`/proc` 中用于检查硬件的一些重要文件包括：

- **`/proc/cpuinfo`**
  列出操作系统找到的 CPU 的详细信息。

- **`/proc/interrupts`**
  每个 IO 设备针对每个 CPU 的中断数量列表。

- **`/proc/ioports`**
  列出当前正在使用的已注册输入/输出端口区域。

- **`/proc/dma`**
  列出正在使用的已注册 DMA（直接内存访问）通道。

`/sys` 目录中的文件具有与 `/proc` 中文件类似的角色。然而，`/sys` 目录有特定的用途，即存储与硬件相关的设备信息和内核数据，而 `/proc` 还包含有关各种内核数据结构的信息，包括运行中的进程和配置。

在标准 Linux 系统中，与设备直接相关的另一个目录是 `/dev`。`/dev` 中的每个文件都与系统设备相关联，特别是存储设备。例如，当连接到主板第一个 IDE 通道的传统 IDE 硬盘时，它由文件 `/dev/hda` 表示。此磁盘中的每个分区将由 `/dev/hda1`、`/dev/hda2` 直到找到的最后一个分区来标识。

可移动设备由 udev 子系统处理，该子系统在 `/dev` 中创建相应的设备。Linux 内核捕获硬件检测事件并将其传递给 udev 进程，该进程随后识别设备，并使用预定义的规则在 `/dev` 中动态创建相应的文件。

在当前的 Linux 发行版中，udev 负责识别和配置在机器开机时已存在的设备（冷插检测）以及在系统运行时识别的设备（热插拔检测）。Udev 依赖于 SysFS，这是挂载在 `/sys` 中的用于硬件相关信息的伪文件系统。

> **注意**
> Hotplug（热插拔）是指系统在运行时检测和配置设备的术语，例如当插入 USB 设备时。Linux 内核从 2.6 版本起支持热插拔功能，允许大多数系统总线（PCI、USB 等）在设备连接或断开时触发热插拔事件。

当检测到新设备时，udev 会在存储在目录 `/etc/udev/rules.d/` 中的预定义规则中查找匹配的规则。最重要的规则由发行版提供，但可以为特定情况添加新规则。

## 存储设备

在 Linux 中，存储设备通常被称为块设备，因为数据以不同大小和位置的缓冲数据块的形式从这些设备读取和写入。每个块设备都由 `/dev` 目录中的一个文件标识，该文件的名称取决于设备类型（IDE、SATA、SCSI 等）及其分区。例如，CD/DVD 和软盘设备将在 `/dev` 中根据其类型命名：连接到第二个 IDE 通道的 CD/DVD 驱动器将被标识为 `/dev/hdc`（`/dev/hda` 和 `/dev/hdb` 保留给第一个 IDE 通道上的主设备和从设备），而旧的软盘驱动器将被标识为 `/dev/fd0`、`/dev/fd1` 等。

从 Linux 内核 2.4 版本开始，大多数存储设备现在被标识为 SCSI 设备，而不管其硬件类型如何。IDE、SSD 和 USB 块设备将以 `sd` 为前缀。对于 IDE 磁盘，将使用 `sd` 前缀，但第三个字母将根据驱动器是主设备还是从设备来选定（在第一个 IDE 通道中，主设备将是 `sda`，从设备将是 `sdb`）。分区按数字列出。路径 `/dev/sda1`、`/dev/sda2` 等用于标识第一个识别的块设备的第一和第二分区，而 `/dev/sdb1`、`/dev/sdb2` 等用于标识第二个识别的块设备的第一和第二分区。这种模式的例外情况是存储卡（SD 卡）和 NVMe 设备（连接到 PCI Express 总线的 SSD）。对于 SD 卡，路径 `/dev/mmcblk0p1`、`/dev/mmcblk0p2` 等用于标识第一个识别设备的第一和第二分区，而 `/dev/mmcblk1p1`、`/dev/mmcblk1p2` 等用于标识第二个识别设备的第一和第二分区。NVMe 设备获得 `nvme` 前缀，例如 `/dev/nvme0n1p1` 和 `/dev/nvme0n1p2`。

