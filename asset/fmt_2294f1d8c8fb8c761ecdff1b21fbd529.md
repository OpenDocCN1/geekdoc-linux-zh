
在此示例中，内核 (`/boot/vmlinuz`) 位于第一个磁盘的第二个分区 (`hd0,1`)。你可以通过输入 `quit` 关闭 GRUB Shell。

# 启动提示处的 GRUB Shell

通过以下步骤在启动提示处启动 GRUB Shell：

1. 从启动选择菜单中，按 `Esc`。
2. 当提示你正在离开图形化启动菜单时，选择 `OK`。显示一个文本菜单：
3. 输入 `c`（美式键盘布局）启动 GRUB Shell。

显示 GRUB Shell 提示符：

# 由 YaST2 修改。最后修改时间 UTC 2009年2月10日 00:08:12
`default 0`
`timeout 8`
## YaSTmenu -- generic_mbr
`gfxmenu (h00,1)/boot/message`
## YaSTmenu -- activate

### 不要修改此注释 - YaST2 标识符：原始名称：
###
`title SUSE Linux Enterprise Server 11 - 2.6.27.11`
`root (h00,1)`
`kernel=/boot/vmlinux-2.6.27-11-pae root=/dev/disk/by-id/ata-VMware_Virtual_IDE_Hard_Drive_0000000000000001-part`
`resume=/dev/disk/by-id/ata-VMware_Virtual_IDE_Hard_Drive_000000000000000000000001-part splash=silent showopts ega=0x332`
`initrd=/boot/initrd-2.6.27.11-pae`

### 不要修改此注释 - YaST2 标识符：原始名称：
## failsafe
`title Failsafe -- SUSE Linux Enterprise Server 11 - 2.6.27.11`
`root (h00,1)`
`kernel=/boot/vmlinux-2.6.27-11-pae root=/dev/disk/by-id/ata-VMware_Virtual_IDE_Hard_Drive_0000000000000001-part2`
`showopts ide=nopma off off= nosmp maxcpu=0 edd-off powersaved=off nohz highs=off processor.max_cstate=1 xilfailsafe ega=0x332`
`initrd=/boot/initrd-2.6.27.11-pae`

### 不要修改此注释 - YaST2 标识符：原始名称：
## floppy
`title Floppy`
`rootoverify (fd0)`
`chainloader +1`

以下是该文件的通用结构：

- 首先，是通用选项：
    - `default 0`。如果未用键盘选择其他条目，则自动启动默认。在本示例中，第一个条目（entry 0）被默认加载。
    - `timeout 8`。指定在八秒后自动启动默认引导。
    - `gfxmenu (hd00,1)/boot/message`。图形菜单存储在硬盘上的位置。

- 通用选项之后是可 GRUB 启动的各种操作系统的选项：
    - `title`。菜单条目的标题。每个操作系统的条目都以此项开始。
    - `root (hd0,1)`。操作系统所在的硬盘分区（在本示例中，是第一块硬盘 [0] 上的第二个分区 [1]）。通过定义根目录（root），你就不需要为随后的条目（如内核）指定分区。

GRUB 不区分 IDE 和 SCSI 硬盘。被 BIOS 识别为第一块的硬盘指定为 `hd0`，第二块硬盘指定为 `hd1`，依此类推。第一块硬盘上的第一个分区称为 `hd0,0`，第二个分区称为 `hd0,1`，依此类推。

- `kernel/boot/vmlinuz`。内核位置，相对于 `root` 选项。其后面跟着内核参数，例如 `root=/dev/hda=normal`。除了设备文件名外，也可以使用 id 来命名分区（如上例所示）。

- `initrd/boot/initrd`。初始内存磁盘（SLES 10 及更高版本中为 initramfs）的位置，相对于上述指定的根分区。`initrd` 包含了内核访问硬盘之前需要的硬件驱动程序（例如 IDE 或 SCSI 控制器的驱动程序）。

# 使用 YaST 配置 GRUB

GRUB 可以使用 `grub-install` 命令配置。在 SLES 11 上，不支持此操作。该二进制文件已重命名为 `/usr/sbin/grub-install.unsupported`。与其使用此命令，还应该使用 YaST，它可以简化引导加载器的配置。除非你完全理解引导加载器的工作原理，否则不应修改 GRUB 配置。

要启动 YaST 引导加载器模块，请启动 YaST，输入 root 密码，然后选择 System（系统） > Boot Loader（引导加载器）。你也可以通过登录 root 并输入 `y2 bootloader` 直接从终端窗口启动引导加载器模块。

显示如下：

# 图 5-8 YaST 引导加载器设置

![](img/1402b35afb63db85442c13e1f1f806f4_485_0.png)

点击 **Section Management**（分区管理）选项卡以查看系统的 GRUB 设置。Def（默认）列指示了在系统启动时哪个条目被选为默认项。

要添加新分区，请点击 *Add*（添加）。你将获得几种选择：

# 图 5-9 YaST 引导加载器设置：分区管理

![](img/1402b35afb63db85442c13e1f1f806f4_486_0.png)

注意：每种分区类型在帮助文本中都有解释。

点击 **Section Management**（分区管理）选项卡以查看系统的 GRUB 设置。Def（默认）列指示了在系统启动时哪个条目被选为默认项。

要添加新分区，请点击 *Add*（添加）。你将获得几种选择：

# 图 5-10 YaST 引导加载器设置：分区管理

![](img/1402b35afb63db85442c13e1f1f806f4_487_0.png)

注意：每种分区类型在帮助文本中都有解释。

点击 **Section Management**（分区管理）选项卡以查看系统的 GRUB 设置。Def（默认）列指示了在系统启动时哪个条目被选为默认项。

要添加新分区，请点击 *Add*（添加）。你将获得几种选择：

# 图 5-11 YaST 引导加载器设置：分区管理

![](img/1402b35afb63db85442c13e1f1f806f4_488_0.png)

注意：每种分区类型在帮助文本中都有解释。

# 直接引导到 Shell

GRUB 启动加载程序的启动界面允许你指定修改 Linux 内核行为的参数。在 GRUB 启动界面的底部是“Boot Options”（启动选项）字段，你可以在此处指定 GRUB 配置中未定义的其他内核选项：

**图 5-12** 启动菜单

![](img/1402b35afb63db85442c13e1f1f806f4_490_0.png)

要添加启动选项，请选择一个 GRUB 菜单项，然后在 **Boot Options** 字段中输入额外的启动选项。上图所示。

这是一个非常实用的功能。例如，访问无法启动的系统的一种方法是为 init 进程设置不同的程序。通常情况下，Linux 内核会尝试寻找名为 `init` 的程序并将其作为第一个进程启动。所有其他进程都由 `init` 启动。

通过输入 `init=new_init_program` 作为启动选项，你可以更改内核加载的第一个程序。例如，如果你输入 `init=/bin/bash` 作为启动选项，系统启动时将直接登录 Bash，而无需提示密码。当 Shell 丢失时，引导进入 Bash 也可以用于重新获取 root 。

你可以使用此 Shell 访问文件系统并修复导致系统无法启动的任何配置错误。

注意：在某些 Linux 系统上，引导进入后根文件系统会被挂载为只读。要修改配置文件，你需要使用以下命令重新挂载文件系统：

```
mount -o remount,rw,sync -t filesystem_type device_name mountpoint
```
