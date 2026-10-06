
- L2 缓存 (每个 CPU): `256 KB`

- 内存: `640 MB`

- 总线速度: `133 MHz`

- 启动 ROM 版本: `4.77F0`

- 序列号: `UV34632QQE`

## 软件

### 软件概述

- 系统版本: `Mac OS X 10.3.4 (7H63)`

- 内核版本: `Darwin 7.4.0`

- 启动卷: `Mac OS X`

- 计算机名称: `Kirk's eBook`

- 用户名: `Kirk McEllearn (kirk)`

## 报告包含多个不同的部分

硬件：告诉你是什么 Mac、速度、缓存大小等。

软件：告诉你你运行的是哪个版本的 Mac OS X、启动卷名称、内核版本以及你的用户名。

网络：告诉你当前活跃的网络接口是什么，包括其硬件地址。

内存：告诉你你有多少内存以及是什么种类型的 DIMM。

PCI/AGP 卡、ATA、SCSI、USB、FireWire 等：这些部分列出了所有活跃的内部和外部设备及卷，包括 PCI 卡、USB 设备和 FireWire 设备。它还会告诉你硬盘的类型、型号和大小，以及如果你的硬盘进行了分区，则每个卷的信息。

应用程序：这是安装在你的 Mac 上所有应用程序（Classic 应用程序除）的列表。注意，这只列出安装在应用程序文件夹中的应用程序；如果你在其他地方有应用程序，则不会包含在内。

## 框架 (Frameworks)
这是可用软件框架的列表。

## 扩展 (Extensions)
这是内核扩展的列表。

## 日志 (Logs)
这些是系统和单个应用程序的日志。这里显示的崩溃日志对开发者通常很有用，提供了应用程序崩溃的时间以及当时发生了什么等详细信息。你也可以在 `/Applications/Utilities` 中的“控制台”（Console）中查看这些日志。

如果你想保存 `system_profiler` 报告，可以这样重定向命令的输出：

```
$ system_profiler > report.txt
```

这将保存一个包含报告内容的文本文件，与终端中显示的内容相同。你还可以将此报告保存为 XML 格式，生成一个具有 `.xps` 扩展名的特殊文件。如果你在 Finder 中双击此文件，它将用“系统报告”（System Profiler）应用程序打开，提供更易读的报告。要执行此操作，请运行以下命令：

```
$ system_profiler -xml > report.spx
```

## 在命令行中使用

### system_profiler 命令概览

#### 命令语法

```
system_profiler [option(s)]
```

#### Finder 等效操作

系统报告实用程序。

#### system_profiler 选项概览

`system_profiler` 命令返回关于你的硬盘和软件信息的报告。

- `-xml` 此选项告诉 `system_profiler` 命令以 XML 格式保存其输出。然后应将其重定向到具有 `.xpx` 扩展名的文件中，这样生成的报告就可以由图形化的“系统报告”应用程序读取。

- `-detailLevel` 该值可以是 `-2`、`-1`、`0` 或 `1`，每个级别都会在报告中生成不同数量的信息。使用级别 `1` 时，命令返回一份完整报告；这与在不指定详细级别的情况下运行命令相同。

#### 获取更多信息

如需了解更多关于 `system_profiler` 命令的信息，请在终端（Terminal）中输入 `man system_profiler`。

`system_profiler` 命令提供了几个级别的详细程度，允许你生成更短的报告，仅涵盖最核心的信息。例如，如果你运行该命令，仅显示前两个部分（如前面的示例所示）：

```
$ system_profiler -detailLevel -2
```

下一级别的详细程度会返回你的 Mac 的完整硬件信息，但不会包含任何软件信息：

```
$ system_profiler -detailLevel -1
```

最后，命令 man 页中称为“短报告”，它返回完整的硬件信息和应用程序列表（这比完整报告要短，完整报告还包含了框架和日志）：

```
$ system_profiler -detailLevel 0
```

你可以根据需要将这些报告中的任何一个保存为文本或 XML 文件。

# 使用 du 获取磁盘占用信息

`du` (disk usage) 命令告知给定目录使用了多少磁盘空间（如果目录包含带有资源叉的文件，则不会包含这些资源叉）。这里有一个示例：

```
$ du -sk *
```

`1309800 /Users/kirk`

我在这里使用了两个选项：`-s` 选项表示只显示目录使用的总空间，如果我没有使用该选项，命令将返回所有子目录及其空间的长列表。`-k` 选项告诉 `du` 以千字节（kilobytes）显示结果。

如示例所示，我的主目录占用了超过 `1.3 GB` 的磁盘空间。要获取此目录及其直接子目录的详细信息，我可以运行如下命令：

```
$ du -sk /Users/kirk/Desktop
```

`+ 81000 /Users/kirk`

`42192 /Users/kirk/Documents`

`251808 /Users/kirk/Library`

`309364 /Users/kirk/Movies`

`33916 /Users/kirk/Music`

`192620 /Users/kirk/Pictures`

`32 /Users/kirk/Public`

`5216 /Users/kirk/Sites`

再次，使用 `-s` 选项告诉命令只显示总计。`*` 通配符告诉 `du` 返回我主目录中每个目录和文件的信息。

你可以使用以 `du` 为前缀命令来获取整个系统或其他用户目录的磁盘占用信息。如果你运行此命令：

```
$ sudo du -sk /
20226798 /
```

该命令将遍历你文件系统中所有的目录并返回使用的总空间。这可能需要几分钟，并且包含了已挂载的卷，无论是外部卷还是网络卷。你可以使用 `-x` 选项将结果限制在当前文件系统中。该命令有几个选项，允许你选择是否跟随符号链接，并改变返回信息的详细程度。

## du 命令概览

### 命令语法

```
du [option(s)] directory(ies)
```

### Finder 等效操作

信息窗口中的“大小”（Size）部分。

## du 选项概览

- `du` 命令返回目录或文件使用的磁盘空间。

- `-s` 此选项告诉 `du` 命令只显示指定目录的总计。

- `-k` 此选项告诉 `du` 命令以千字节显示结果。

- `-x` 此选项告诉 `du` 命令仅检查当前文件系统。

#### 获取更多信息

如需了解更多关于 `du` 命令的信息，请在终端中输入 `man`。

### 使用 df 获取可用磁盘空间信息

正如 `df` 给你给定目录使用的磁盘空间一样，`df` (disk free) 告诉磁盘上有多少可用空间。当你运行此命令时，它会告诉你系统上的剩余可用空间：

| Filesystem | 1K-blocks | Used | Capacity | Mounted on |
| :--- | :--- | :--- | :--- | :--- |
| /dev/disk0 | 155960 | 117692 | 367128 | / |
| devfs | 95 | 0 | 95 | |
| /dev/disk01 | 512 | 0 | 512 | |

## 第 15 章从命令行进行系统维护

| /dev/disk3 | 类型 名称 大小 标识 |
| :--- | :--- | :--- | :--- |
| 0: Apple_partition__ | | |113.4 GB GB3 |
| 1: | Apple_partition_map | 31.5 KB |331 |
| 2: | | Apple_4 | 28.0 KB KB disk3s2 |
| 3: | Apple_Driver4 | 28.0 KB disk disk3s3 |
| 4: |____ |  2..0 KB | disk3s4 |
| 5: |____  | 28.0 KB disk3ss5 |
| 6 | |FWFW |  | 256.0 disk | disk3s6 |
| 7: | Apple_Driver_OKit | 256.0 KB | disk3s7 |
| 8: | Apple_Patches | 256.0 KB | disk3s8 |
| 9: | Apple_HFS FW160 | 153.2 GB | disk3s10 |
| /dev/disk4 | 类型 名称 大小 标识 |
| :--- | :--- | :--- | :--- |
| 0: Apple_partition_scheme | | | *124.0 MB disk4 |
| 1: | Apple_partition_map | 31.5 KB | disk4s1 |
| 2: | Apple_HFS KeyDrive | 123.9 MB disk4s2 |

如你所见，这些磁盘已经挂载。第一个是内置硬盘，它有两个分区：Mac OS X 和 Backup。第二个是外部火线（FireWire）磁盘，只有一个分区。第三个是 USB 驱动器，也只有一个分区。

但所有这些磁盘都有多个分区，如果你在检查磁盘本身时没有看到它们：这些分区存储了驱动程序和映射信息。你可以挂载的分区是在“Name”列中有名称的那些。

## 使用 diskutil

如下面的表 15.1 所示，`diskutil` 允许你对磁盘和卷进行许多操作。但请注意：`diskutil` 可能是危险的。分区磁盘会删除其所有数据；使用 `eraseDisk` 或 `eraseVolume` 选项并在磁盘名称或设备节点上出错会导致严重后果。请确保你清楚自己在做什么。

`diskutil` 命令可以从命令行处理许多磁盘维护操作。你可以验证并修复磁盘结构，也可以验证并修复权限。定期运行磁盘结构修复是一件好事，尽管 Mac OS X 会自动执行此操作。至于权限，这可以解决 Mac OS X 的许多问题，许多人每次运行系统升级时都会执行此操作。

要修复启动卷上的权限，请运行此命令：

```
$ sudo diskutil repairPermissions /
```

你会发现，这个命令几乎在每次运行时都能找到一些需要修复的内容。

要修复磁盘结构，请运行此命令：

```
$ sudo diskutil repairDisk /Volumes/Backup
```

在例例中，我在一个名为 Backup 的卷上运行了 `diskutil`。

只要使用得当，`diskutil` 命令可以让你完成使用“磁盘工具”（Disk Utility）能完成的所有操作。不过，在删除或分区磁盘之前要非常小心，因为没有安全网。在执行此类操作之前，确保你对所有磁盘都有全盘备份。

## 表 15.1：用于 diskutil 的动词

| 动词 | 功能 |
| :--- | :--- |
| list | 列出磁盘的分区。 |
| info | 获取磁盘或卷的信息。 |
| unmount | 卸载单个卷。 |
| unmountDisk | 卸载整个磁盘及其所有卷。 |
| eject | 弹出磁盘。 |
| mount | 挂载单个卷。 |
| mountDisk | 卸载整个磁盘并挂载卷。 |
| rename | 重命名卷。 |
| enableJournal | 在已挂载的 HFS+ 卷上启用 HFS+ 日志。 |
| disableJournal | 在已挂载的 HFS+ 卷上禁用 HFS+ 日志。 |
| verifyDisk | 验证卷的结构。 |
| repairDisk | 修复卷的结构。 |
| verifyPermissions | 验证卷的权限。 |
| repairPermissions | 修复卷的权限。 |
| repairS09Permissions | 修复选定的经典系统文件夹（System Folder）和应用程序文件夹的权限。 |
| eraseDisk | 擦除现有磁盘并移除卷。 |
| eraseVolume | 擦除现有卷 |
| eraseOptical | 擦除光介 CD/RW、DVD 等。 |
| zeroDisk | 通过向介质写入零来擦除磁盘。 |
| randomDisk | 向介质写入随机数据来擦除磁盘。 |
| partitionDisk | 重新分区并移除卷。 |
| createRAID | 在多个磁盘上创建 RAIDset。 |
| destroyRAID | 销毁现有 RAIDset。 |
| checkRAID | 检查 RAIDset是否存在错误。 |
| enableRAID | 将磁盘转换为未配对的镜像 RAID。 |
| repairMirror | 修复损坏的 RAIDset。 |

### diskutil 命令概述

### 命令语法

```
diskutil verb [option(s)]
```

### Finder 等等对应项

磁盘工具（Disk Utility）。

### diskutil 选项概述

> `diskutil` 命令允许你管理磁盘和卷。动词和功能列表请见表 15.1。

### 获取更多信息

要了解更多关于 `df` 命令的信息，请在终端输入 `man diskutil`。

## 使用 fsck 修复磁盘问题

虽然硬盘在机械上是可靠的（在一定范围内），但出现损坏并不罕见。磁盘使用目录来存储磁盘上文件的名称和位置。如果磁盘目录损坏，磁盘将无法找到其文件；如果损坏严重，你可能会丢失对所有文件的访问。

每次启动 Mac 时，启动过程都会包含文件系统检查，如果电脑崩溃或异常关机，或者你在未弹出的情况下断开了外部驱动器，该检查可能会修复目录的小型问题。如果你遇到了内核恐慌（一种需要重启 Mac 的崩溃），启动时间会更长，因为 `fsck` 会运行更彻底的检查和修复。虽然 Mac OS X 可以长时间不重启而运行，但单此这一点就足以我们尊重时间的价值。

但如果你遇到了更严重的问题，最好的办法是从 Mac OS X 安装光启动，并从安装程序菜单中运行“磁盘工具”。你并不总是有安装光盘。

# 386 第 15 章从命令行进行系统维护

在某些情况下，你的磁盘问题可能过于严重，`fsck` 无法进行修复。如果是这样，你需要运行第三方磁盘修复工具，例如 Alsoft DiskWarrior 或 Micromat TechTool。截至编写本文时，TechTool 已被包含在 AppleCare 合同中，因此如果你有 AppleCare 保护，请尝试运行该程序来修复你遇到的任何磁盘问题。

## 使用 bless 对系统文件夹进行祝福

Mac 计算机上的卷必须经过“祝福”（blessed），或被设置为可启动状态，这样你才能用它们启动电脑。如果你在 Mac 上有多个卷并移动了经典系统文件夹（Classic System Folder），你可能会发现经典偏好设置没有看到它，或者启动窗口（Startup pane）不允许你选择它。Mac OS 卷也可能出现这种情况。要为卷或系统文件夹启用启动功能，你可以使用 `bless` 命令。

该命令以三种模式工作：文件夹模式、设备模式和信息模式。在文件夹模式下，你选定一个系统文件夹（即使在 Mac OS 下）并对其进行启动祝福。你通常在第一次格式化和设置卷时使用设备模式。而信息模式则告诉你哪些卷或文件夹已经过祝福。

在我的情况下，我将经典系统文件夹放在单独的分区上。在所有分区上运行信息模式下的 `bless` 命令显示了以下内容：

```
$ bless -info /
finderinfo[0]: 104794 => Blessed System Folder /System/Library/CoreServices
finderinfo[1]: 0 => No Startup app (无论如何会被忽略)
finderinfo[2]: 0 => Open-folder linked entry list
finderinfo[3]: 0 => No OS 9 + X blessed 9 folder
finderinfo[4]: 0 => Unused field
finderinfo[5]: 104794 => X blessed folder is /System/Library/CoreServices
64-bit VDSB volume id: 04762A70348707693
```

```
$ bless -info /Volumes/Backup/
finderinfo[0]: 0 => Blessed System Folder
finderinfo[1]: 0 => No Startup app (无论如何会被忽略)
finderinfo[2]: 0 => Open-folder linked entry list
finderinfo[3]: 21 => 0 OS 9 blessed folder is /Volumes/Backup/System Folder
finderinfo[4]: 0 => Unused field
finderinfo[5]: 0 => OS 9 + X blessed X
64-bit VDSB volume id: 04880F1B788BAB952
```

第一种情况显示了我启动卷上经过祝福的系统文件夹，第二种显示了我经过祝福的经典（OS 9）系统文件夹。

要祝福 Mac OS 9 卷以进入 OS 9 ，请运行此命令，并将 `vol_name` 替换为你的卷的名称：

```
$ bless -folder9 "/Volumes/Mac OS 9/System Folder" -bootBlockFile "/usr/share/misc/bootblockdata"
```

## 在命令行中

### bless 命令概述

### 命令语法

```
bless [option(s)] directory
```

| Finder 等效项 (FINDER EQUIVALENT) |
| :--- |
| 无。 |

#### BLESS 选项概述

`bless`

- `bless`: 该命令让你让卷和系统文件夹变为可启动。

### 获取更多信息
