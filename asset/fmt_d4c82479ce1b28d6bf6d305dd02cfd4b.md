
### prtconf 命令选项

- `-a`。显示从 `<devPath>` 指定设备到设备树根节点的祖先节点。
- `-c`。显示以 `<devPath>` 指定设备为根节点的设备子树。
- `-v`。详细模式（Verbose mode）。
- `-V`。显示关于 PROM（针对 SPARC）或启动系统（针对 x86）的版本信息。
- `-x`。报告系统固件是否支持 64 位。

注意，`prtconf` 命令提供了极大的灵活性。你可以获取关于单个设备的信息，也可以获取关于设备子树的信息。如果你在不带任何选项或参数的情况下执行该命令，它将显示连接到系统的所有设备的信息。例如，在基于 SPARC 的系统上，`prtconf` 命令将产生如下输出：

```
## prtconf
System Configuration: Sun Microsystems sun4u
Memory size: 512 Megabytes
System Peripherals (Software Nodes):
SUNW,Sun-Blade-1000
scci_vhci, instance #0
packages (driver not attached)
SUNW,builtin-drivers (driver not attached)
deblocker (driver not attached)
disk-label (driver not attached)
terminal-emulator (driver not attached)
obp-tftp (driver not attached)
dropsins (driver not attached)
kd-translator (driver not attached)
uufs-file-system (driver not attached)
chosen (driver not attached)
openprom (driver not attached)
client-services (driver not attached)

options, instance #0
aliases (driver not attached)
memory (driver not attached)
virtual-memory (driver not attached)
SUNW,UltraSPARC-III, instance #0
memory-controller, instance #0
SUNW,UltraSPARC-III, instance #1
memory-controller, instance #1
pci, instance #0
ebus, instance #0
```

输出已截断。

> `prtconf` 命令显示的“driver not attached”消息并不一定意味着驱动程序对该设备可用；它意味着驱动程序当前未附加到该实例，因为该设备未正被使用。当访问设备时，驱动程序会自动加载，当设备不再使用时，驱动程序会被卸载。

你可以使用 `dmesg`、`prtconf` 和 `sysdef` 等多个命令获取有关连接到系统的设备的信息。`dmesg` 命令显示物理设备名称与实例名称之间的映射。当然，你可以通过显示 `/etc/path_to_inst` 文件的内容来查看映射关系——例如，执行以下命令：

```
less /etc/path_to_inst
```

然而，在处理 `path_to_inst` 文件时要格外小心，因为系统以一种非常重要的方式使用该文件。

## path_to_inst 文件的问题

正如你已经从上一个节了解的那样，实例名称（内核用于引用设备的缩写词）在 `/etc/path_to_inst` 文件中映射到物理设备名称。一旦为设备分配了实例名称，系统就会在 `/etc/path_to_inst` 文件中记录该映射，以保持跨重启的一致性。

### 系统依靠此文件来查找根设备（root）和交换设备（swap）；没有它无法启动。换句话说，除非你已经想清楚了更改，否则不要删除 `/etc/path_to_inst` 文件并对其进行修改。通常情况下，你不需要修改此文件，因为该文件由系统维护。

## 第 5 章：管理磁盘

如果由于 `/etc/path_to_inst` 文件问题导致无法从启动盘启动系统，请记住 CD-ROM 中仍然有 `/etc/path_to_inst` 文件。你可以执行以下步骤：

- 从 OpenBoot 提示符中使用 `boot -sw cdomrom` 从 CD-ROM 启动。
- 从启动盘在 `/a` 上挂载根文件系统。
- 将 CD-ROM 中包含的 `/etc/path_to_inst` 复制到启动盘的 `/a/etc/path_to_inst`。
- 使用启动盘启动。

现在你已经知道如何查找当前连接到系统的设备信息。但如果系统在运行时添加了新设备怎么办？你需要做什么才能让系统识别新添加的设备？让我们接着探讨这一点。

## 练习 5-I

### 显示连接到 Solaris 系统的设备信息

1. 通过执行以下命令确定实例名称与物理设备名称之间的映射：

`dmesg`

2. 如果输出太长且滚动太快，你可以通过以下方式执行命令来浏览输出：

`dmesg | more`

按空格键逐页浏览输出。

3. 从输出中确定实例名称与物理设备名称之间的映射。设备的映射类似于：`/pci@1`

4. 现在，使用 `prtconf` 命令查看在以下设备上安装了多少内存：

```
prtconf | grep Memory
```

输出将如下所示：

`Memory size: 128 Megabytes`

## 列出和重新配置设备

在早期的 Solaris 版本中，必须重启系统才能识别新设备。`devfsadm` 命令消除了重启的需求。`devfsadm` 管理 `/devices` 文件并在 `/dev` 中创建链接。该命令的语法如下：

```
/usr/sbin/devfsadm <options>
```

常用选项如下：

- `-c <deviceClass>`。将操作限制为指定的 `<deviceClass>` 类，可选值为 `disk`（磁盘）、`tape`（磁带）、`port`（端口）、`audio`（音频）和 `pseudo`（伪设备）。
- `-C`。清理模式。清理悬挂的 `/dev`。
- `-i <driverName>`。仅加载指定的 `<driverName>` 驱动，并配置该驱动程序的设备。
- `-n`。不尝试加载驱动程序或向设备树添加新节点。
- `-s`。抑制对 `/dev` 的报告。
- `-v`。以详细模式显示 `/dev` 的更改。如果你需要调试信息，请使用此选项。

### 指定多个类

如果你想指定多个类的设备，需要如下所示重复 `-c` 选项：

```
devfsadm -c disk -c audio
```

你格式化并分区磁盘以便文件系统位于分区。在分区中创建文件系统后，通过挂载使其户可用，我们将在此探讨。

## 认证目标 5.04

## 挂载和卸载文件系统

考试目标 2.7：在 Solaris 10 OS 文件系统中执行挂载和卸载，使用卷管理访问挂载的软盘和 CD-ROM，限制访问，调试卷管理问题并解释未使用卷管理的访问方法。

对于用户来说，Solaris 系统上的所有文件系统似乎都是一个统一的目录树，根目录 (`/`) 位于顶部。当你在磁盘上创建文件系统时，你将其附加到树的某个点下，这个过程被称为挂载文件系统。挂载文件系统的不同方式有：

- 如果某个文件系统使用频率较低，你可以通过命令行执行 `mount` 命令来挂载它。
- 你可以在 `/etc/vfstab` 中为经常使用的文件系统创建条目，这些文件系统会在系统启动时自动挂载。
- 你可以使用 `AutoFS` 工具，它会在访问文件系统时自动挂载，并在用户移动到其他目录时自动卸载。

当 Solaris 系统启动时，会自动挂载 `vfstab` 文件列出的文件系统。

### 使用 /etc/vfstab 自动挂载

在启动过程中，当系统进入多用户模式时，会执行 `mountall` 命令，该命令会挂载 `/etc/vfstab` 文件指定的文件系统。

![](img/2868b3fa16f35933a30294421c5d872d_150_0.png)

| 内核挂载根命令挂载 `/etc/vfstab` 文件中列出的文件系统，其值为 | (l), `/usr` 和 `/var` 文件命令执行； | 启动时挂载（boot）字段等于 `yes`。 |

`/etc/vfstab` 文件中条项的字段描述如下：

- **要挂载设备（Device to mount）**。此字段识别与要挂载的文件系统对应的设备名称（例如 `/dev/disk/c0t0d0`）或虚拟文件系统的目录名。
- **用于 fsck 的设备（Device to fsck）**。此字段识别 `fsck` 命令用于该文件系统的原始设备名称（例如 `/dev/rdsk/c0t0d0`）。如果此字段不适用，请使用连字符 `-`——例如，在只读文件系统或网络文件系统的情况下。
- **挂载点（Mount point）**。此字段识别文件系统要挂载到目录树的哪个——例如 `/usr`。
- **文件系统类型（FS type）**。此字段识别文件系统的类型。
