
`/proc` 中的几个文件和目录包含关于你 Linux PC 的信息。例如，`/proc/cpuinfo` 文件列出了系统的关键特征，例如处理器类型和浮点信息。你可以通过输入 `cat /proc/cpuinfo` 查看处理器信息。例如，当 `cat /proc/cpuinfo` 在示例系统上运行时会出现以下内容：

```
processor : 0
vendor_id : GenericIntel
cpu family : 15
model : 3
name : Intel (R) Celeron(R) CPU 2.53GHz
stepping : 3
cpu MHz : 2533.129
cache size : 256 KB
fdiv_bug : no
hlt_bug : no
f00f_bug : no
coma_bug : no
fpu : yes
fpu.exception : yes
cpuid level : 5
wp : yes
flags : fpu vme de pse tsc msr pce cx8 acpi sep mtr pge mca cmov pat pse36 clflush dts acpi mmx fxrs sse sse ss ht tm pni monitor d0_cpl
bogomips : 4997.12
```

## 324 通过 /proc 文件系统查看系统信息

此输出来自一个 2.5-GHz 的 Celeron 系统。列表显示了处理器的许多有趣特性。注意以 `fdiv_bug` 开头的行。还记得臭名昭著的 Pentium 浮点除错误吗？该错误存在于名为 `fdiv`（用于浮点除法）的指令中。而 `fdiv_bug` 表示此特定的 Pentium 是否存在该错误。

`/proc/cpuinfo` 文件的最后一行显示了处理器的 BogoMIPS，这是内核在启动时计算的。BogoMIPS 使用时间延迟循环。

表 1-7 总结了 `/proc` 文件系统中提供有关 Linux 系统信息的一些文件。你可以查看它们的内容，但请注意并非所有文件都存在于你的系统中。表 1-7 `/proc` 文件系统的具体内容取决于内核配置和加载的驱动模块（而这些模块反过来取决于你 PC 的硬件配置）。

| 表 1-7 /proc 中的一些文件和目录 |
| :--- |
| 文件名 | 内容 |
| /proc/acpi | 关于高级配置和电源接口 (ACPI) 的信息 —— 一用于笔记本电脑、桌面式电脑和服务器配置及电源管理的工业标准接口。 |
| /proc/bus | 包含每个总线类型（如 PCI）特定信息的目录。 |
| /proc/cmdline | 启动 Linux 内核时命令行（例如 `root=LABEL=/rhgb`）。 |
| /proc/cpuinfo | 关于 CPU（微处理器）的信息。 |
| /proc/devices | 系统中可用的块设备和字符设备。 |
| /proc/dma | 关于所使用的 DMA（直接内存访问）通道的信息。 |
| /proc/driver/rtc | 关于 PC 实时时钟 (RTC) 的信息。 |
| /proc/filesystems | 支持的文件系统列表。 |
| /proc/ide | 包含 IDE 设备信息的目录。 |
| /proc/interrupts | 关于中断请求 (IRQ) 编号及其使用方式的信息。 |
| /proc/ioports | 关于输入/输出 (I/O) 端口地址及其使用方式的信息。 |
| /proc/kcore | 物理内存映像。 |
| /proc/dg | 内核消息。 |
| 文件名 | 内容 | 书籍 V |
| /proc/loadavg | 平均负载（1、5 和 15 分钟内等待运行的进程数）。 | 第 1 章 |
| /proc/locks | 当前内核锁（用于确保多个进程不会同时写入一个文件）。 | 管理 |
| /proc/meminfo | 关于物理内存和交换空间使用情况的信息。 | 基础系统 |
| /proc/misc | 杂项信息。 | 导论 |
| /proc/modules | 已加载的驱动模块列表。 | |
| /proc/mounts | 已挂载的文件系统列表。 | |
| /proc/net | 包含许多网络信息的子目录的目录。 | |
| /proc/partitions | Linux 内核已知的分区列表。 | |
| /proc/pci | 系统发现的 PCI 设备信息。 | |
| /proc/scsi | 包含系统中发现的 SCSI 设备信息的目录（仅当拥有 SCSI 设备时存在）。 | |
| /proc/stat | 系统的整体统计信息。 | |
| /proc/swaps | 关于交换空间及使用量的信息。 | |
| /proc/sys | 包含向此目录文件写入参数的目录。（正确使用此方法调优系统性能需要专业知识）。 | |
| /proc/uptime | 关于系统运行时间的信息。 | |
| /proc/version | 内核版本号。 | |

![](img/71f80d7808bf5b5ad1239cc29be7bab2_344_0.png)

你可以像处理 Linux 中的任何其他目录和文件一样导航于 `/proc` 文件系统。使用 `more` 或 `cat` 命令查看文件内容。

## 理解 Linux 设备

Linux 将所有设备视为文件，并像使用设备一样对其进行操作：打开、从中写入数据、从中读取数据，并在完成后关闭。这种将每个设备视为文件的能力之所以可能，是因为设备程序的存在。

# 328 管理可载驱动程序模块

udev 程序的配置文件是 `/etc/udev/udev.conf`。根据该配置文件的设置，udev 会在 `udev_root` 参数指定的目录中自动创建设备节点。例如，为了管理 `/dev` 目录中的设备节点，应在 `/etc/udev/udev.conf` 中如下所示定义 `udev_root`：

```
udev_root="/dev"
```

## 管理可载驱动程序模块

要使用任何设备，Linux 内核必须包含相应的驱动程序。如果驱动代码以单体程序（即单个大文件的形式）链接到内核中，那么添加新驱动程序意味着要使用新驱动代码重新编译内核。重新编译内核意味着在使用新设备驱动之前，必须使用新内核重启电脑。幸运的是，Linux 内核使用了模块化设计，消除了重启的烦恼。设备驱动程序可以用模块的形式创建，内核可以在无需重启电脑的情况下加载和卸载这些模块。

驱动模块是一类被称为“可载内核模块”（loadable kernel modules）的更广泛软件模块。其他类型的内核模块还包括支持新类型文件系统的代码、网络协议模块以及解释不同格式可执行文件的模块。

### 加载和卸载模块

你可以通过一组命令来管理可载设备驱动模块。你必须以 root 身份登录才能使用其中某些命令。表 1-8 总结了一些常用的模块命令。

| 表 1-8 | 管理内核模块的命令 |
| --- | --- |
| 此命令 | 功能如下 |
| insmod | 将模块插入内核。 |
| rmmod | 从内核中移除模块。 |
| depmod | 确定模块之间的依赖关系。 |
| kym | 显示符号列表，以及定义该符号的模块名称。 |
| lsmod | 列出所有当前加载的模块。 |
| modinfo | 显示内核模块的信息。 |
| modprobe | 智能地插入或移除单个模块或一组模块。（例如，如果模块 A 需要 B，当要求加载 A 时，modprobe 会自动加载 B。） |

# 管理可载驱动程序模块 329

如果你必须使用这些命令之一，请以 root 身份登录或在终端窗口中输入 `su -` 成为 root。

要查看当前加载了哪些模块，输入：

```
lsmod
```

你会看到一个模块列表。该列表取决于你系统中安装的设备类型。

`lsmod` 显示的列表包含了所有类型的 Linux 内核模块，而不只是设备驱动程序。如果你使用 Ext3 文件系统，通常会发现两个模块——`jbd` 和 `ext3`，它们是 Ext3 文件系统（Linux 的最新系统）的一部分。

除了 `lsmod`，另一个常用命令是 `modprobe`。当你需要手动加载或删除一个或多个模块时，请使用 `modprobe`。`modprobe` 的优点在于你不需要担心模块是否需要其他模块才能工作。`modprobe` 命令会自动加载模块所需的任何模块。例如，要手动加载音频驱动，使用命令：

```
modprobe snd-card-0
```

此命令会导致 `modprobe` 加载使音频正常工作所需的所有内容。

你可以配合 `-r` 选项移除模块。例如，要移除音频模块，请使用以下命令：

```
modprobe -r snd-card-0
```

此命令去除了 `modprobe snd-card-0` 命令加载的所有模块。

# 使用 /etc/modprobe.conf 文件
