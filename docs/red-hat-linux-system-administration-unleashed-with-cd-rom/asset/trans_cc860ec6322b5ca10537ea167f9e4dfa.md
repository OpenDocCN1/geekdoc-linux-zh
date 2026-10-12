
## RAID 工具

Red Hat Linux 6.0 中可用的 RAID 支持并非原版内核中的支持。Red Hat 已将 RAID 软件驱动程序和 RAID 工具升级为比原始内核源代码中当前所见更新的版本。

> **Note**
> 
> 若要查看应用到原始 Linux 源代码树上的完整补丁集，请检查内核的源 RPM。 要安装此 SRPM，请在 Red Hat FTP 站点或随 Red Hat 发行版提供的 SRPM CD-ROM 上查找 `kernel-2.2.5-15.src.rpm`。 安装此 RPM 后，您可以通过查看 `/usr/src/redhat/SOURCES` 目录来检查应用的所有内核补丁。

Red Hat Linux 随附 RAID 工具的 0.90 版本。 这些命令与前辈相比有显著不同，并包含支持内核源代码中提供的更新 RAID 驱动程序所提供的额外功能所需的特性。 RAID 命令集位于 `/sbin` 目录中，由表 9.1 中的工具组成。

### 表 9.1 RAID 命令及其功能

| 命令 | 功能 |
|---|---|
| mkraid | 初始化 RAID 设备阵列 |
| raidstart | 在内核中配置 RAID 设备并激活它们 |
| raidhotadd | 向正在运行的 RAID 阵列添加备用设备 |
| raidhotremove | 从正在运行的 RAID 阵列中移除设备 |
| raidstop | 取消配置 RAID 设备阵列 |

要考虑的第一个命令是 `mkraid` 命令。 `mkraid` 命令用于初始化 RAID 设备，适用于 Linux 软件 RAID 驱动程序支持的所有 RAID 级别。 `mkraid` 命令在功能上类似于用于创建文件系统的 `mkfs` 命令，因为它是为 RAID 阵列准备接收数据的第一步。 在正常使用中，此命令仅在创建 RAID 阵列期间使用，因为与 `mkfs` 命令一样，此命令会破坏 RAID 阵列上的数据。 它从配置文件中读取，要么是你使用 `-c` 命令行选项指定的文件，要么是默认的 `/etc/raidtab`，以确定每个 RAID 设备的具体信息。 `mkraid` 命令的选项在手册页和表 9.2 中描述。

### 表 9.2 mkraid 的命令行选项

| 选项 | 描述 |
|---|---|
| -v, --version | 显示简短的版本信息，然后退出。 |
| -h, --help | 显示用法说明。 |
| -c, --configfile file | 使用 file 作为配置文件，而不是 /etc/raidtab。 |
| -f, --force | 即使阵列似乎已初始化，也初始化阵列。 |
| -o, --update | 而不是初始化阵列中的每个设备，此选项会使 mkraid 将存储在 RAID 阵列上的版本信息更新为当前内核的版本，尽管它是非破坏性的，但仍应谨慎使用。 |

在描述 RAID 工具集的其他命令之前，让我们检查 RAID 配置文件 /etc/raidtab。 raidtab 段包括 RAID 级别、构成阵列的分区数量和名称，以及取决于所实现 RAID 级别的其他必需信息。 /etc/raidtab 文件格式的详细说明可在本章后面找到，并附有软件 RAID 驱动程序支持的每个 RAID 级别的示例。 你必须根据 raidtab 手册页和表 9.3 中描述的严格语法创建此配置文件。

### 表 9.3 /etc/raidtab 关键字及其含义

| 关键字 | 含义 |
|---|---|
| raiddev device | 此行在 RAID 配置文件中开始一个段落，并指定分配给 RAID 的设备名称。 |
| raid-level integer | 分配给此关键字的整数值指定当前 raiddev 的 RAID 级别。可用的值有 -1、0、1、4 和 5，分别对应 linear、RAID-0、RAID-1、RAID-4 和 RAID-5。线性模式也可以使用单词 linear 而不是整数值来指定。 |
| nr-raid-disks count | 阵列中的磁盘分区数。 |
| nr-spare-disks count | 阵列中可由内核在损坏阵列的自动重建中使用备用磁盘的数量。 |
| device device file | 要添加到阵列的设备文件名称。每个定义的 RAID 阵列将有多个 device 条目。device 条目的数量必须等于 nr-raid-disks 参数给出的数量。 |
| raid-disk index | 从 0 开始，最近定义的设备在活动磁盘阵列中的位置。 |
| spare-disk index | 从 0 开始，最近定义的设备在备用磁盘阵列中的位置。 |
| parity-disk index | 从 0 开始，最近定义的设备在奇偶校验磁盘阵列中的位置。 |

### 表 9.3 继续

| 关键字 | 含义 |
|---|---|
| parity-algorithm which | 当前阵列使用的 RAID 级别 5 奇偶校验算法。此参数的可能值为 left-asymmetric、right-asymmetric、left-symmetric 或 right-symmetric。 |
| chunk-size size | 条带的 K 字节大小。 |
| persistent-superblock bool | 如果设置为 1，则会在阵列中的每个物理设备上写入一个特殊超级块，内核读取它而不是 /etc/raidtab 文件来配置 RAID 设备。如果希望能够从 RAID 设备启动，则需要值为 1。 |

与 RAID 工具集的早期版本不同，Red Hat 6.0 中包含的 RAID 工具不包含 ckraid 命令。 此命令以前是必需的，用于检查 RAID 设备阵列中的不一致并选择性地纠正。 此功能现在由内核线程处理，该线程使用空闲 CPU 周期对配置的 RAID 设备执行任何所需的更正。 重建状态现在通过检查 /proc/mdstat 文件来确定。

我们将要介绍的下一个命令统称为 RAID 管理实用程序。 这些命令适用于所有 RAID 级别，包括线性模式和 RAID 级别 0 阵列。 这些命令是 raidstart、raidhotadd、raidhotremove 和 raidstop。 实际上它们都是同一个命令，raidhotadd、raidhotremove 和 raidstop 只是 raidstart 命令的链接。 通过以不同的名称调用此命令，可以实现不同的功能。

### 注意

创建 RAID 设备阵列取决于两件事。 其中之一是内核中的 RAID 驱动程序支持，另一个是 /dev 中的适当设备文件。 md 设备的 major 号码为 9，minor 号码从 0 开始，并为每个 RAID 设备递增 1。 如果你的 /dev 目录中没有设备条目，这里是创建 md 设备驱动程序支持的默认四个 md 设备所需的命令：

```
/sbin/mknod b 9 0 /dev/md0
/sbin/mknod b 9 1 /dev/md1
/sbin/mknod b 9 2 /dev/md2
/sbin/mknod b 9 3 /dev/md3
```

虽然你可以配置你创建的任何 RAID 设备以便在启动序列期间由内核自动检测，但如果你愿意，也可以手动启动和停止它们。 你可能希望手动启动 RAID 阵列以缩短系统启动所需的时间。 此外，你可能需要在启动某些其他系统软件之前确保 RAID 完全功能。 你可能还希望即使 RAID 失败也能继续启动系统。

要手动启动 RAID 阵列，你将使用 raidstart 命令。 此命令检查 RAID 配置文件，如果提供了 -a 选项，它将激活其中描述的所有 RAID 设备。 如果没有 -a 选项，你需要指定一个对应于你想要启动的阵列的设备文件。 此一个命令取代了旧 RAID 工具集中的 raidadd 和 raidrun 命令。 你必须在 RAID 阵列上创建文件系统或交换设备、挂载现有文件系统或以任何方式访问阵列上的文件系统或交换设备之前执行 raidstart 命令。 该套件中的相反命令是 raidstop 命令，它使 RAID 阵列中的驱动器非激活并在内核中取消配置它们。 你应该仅在阵列上的所有打开文件已关闭并且 RAID 设备已卸载后才运行此命令。 这两个命令都读取默认配置文件 /etc/raidtab 或使用 -c 选项指定的配置文件。 这些命令可用的完整选项集在 raidstart 手册页和表 9.4 中描述。

### 表 9.4 raidstart 的命令行选项

| 选项 | 描述 |
|---|---|
| -a, --all | 对配置文件中指定的所有设备运行命令。 |
| -c, --configfile file | 使用 file 作为配置文件。默认值为 /etc/raidtab。 |
| -h, --help | 显示简短的用法说明然后退出。 |
| -V, --version | 显示 RAID 工具的版本号然后退出。 |

RAID 管理命令集中的另外两个命令是 raidhotadd 和 raidhotremove。 这些命令用于向正在运行的阵列添加或移除物理设备。 这允许向阵列添加备用磁盘并从阵列中移除死磁盘。 如前所述，这些命令实际上只是 raidstart 命令的链接，因此从 RAID 配置文件中读取所需的信息。

