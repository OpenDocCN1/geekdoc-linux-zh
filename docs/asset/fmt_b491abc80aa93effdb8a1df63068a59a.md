
| type | description |
| :--- | :--- |
| `object` | any value that is not a primitive |
| `function` | a function which is also an object |
| `primitive` | any of the primitive types |
| `any` | any of the types above |

| primitive type | description |
| :--- | :--- |
| `string` | textual data |
| `number` | IEEE 754 double-point numbers |
| `boolean` | logical values of true and false |
| `null` | an intentional absence of value |
| `undefined` | a variable that has not been assigned a value |
| `symbol` | a unique identifier |
| `bigint` | arbitrary-precision integers |

`object` values are not immutable and can be modified (e.g., by adding properties). `primitive` values are immutable and cannot be changed. They are copied as values.

## PDF 处理

北、南、东、西。我们对 `pdftk` 的能力仅触皮一角。手册页提供了更多示例和完整的语法。

### pdf2ps

```
pdf2ps [options] file.pdf [file.ps]
```

```
ps2pdf [options] file.ps [file.pdf]
```

`pdf2ps` 命令将 Adobe PDF 文件转换为 PostScript 文件（如果你不提供输出文件名，默认使用原文件名并将 `.pdf` 替换为 `.ps`）：

```
$ pdf2ps sample.pdf converted.ps
```

该命令有几个选项，但很少使用。如果你感兴趣，请参阅手册页。

要进行相反的操作，即将 PostScript 文件转换为 PDF 格式，请使用 `ps2pdf`：

```
$ ps2pdf sample.ps converted.pdf
```

## 打印

- `lpr` 打印文件。
- `lpq` 查看打印队列。
- `lprm` 从队列中移除打印任务。

Linux 有两个流行的打印系统，分别称为 `CUPS` 和 `LPRng`。这两个系统都使用名称相同的命令：`lpr`、`lpq` 和 `lprm`。然而，取决于你使用的是 `CUPS` 还是 `LPRng`，这些命令具有不同的选项。为了方便起见，我们将介绍两个系统都通用的选项。

在过去，在 Linux 上安装打印机需要编辑晦涩的配置文件，例如 `/etc/cups/printers.conf` 或 `/etc/printcap`。现在，`GNOME` 和 `KDE` 的系统设置中都有打印机配置工具，可以生成这些文件。

要排查 `CUPS` 打印机的故障，请访问 `http://localhost:631` 进入 `CUPS` 管理系统。

### lpr

```
lpr [options] [files]
```

`lpr`（行打印机）命令将文件发送到打印机：

```
$ lpr -P myprinter myfile
```

#### 有用选项

- `-P printername` 将文件发送到之前设置过的打印机 `printername`。
- `-N N` 打印文件的 `N` 份副本。
- `-J name` 设置打印在首页上的任务名称（如果你的系统设置了打印首页）。

### lpq

```
lpq [options]
```

`lpq`（行打印机队列）命令列出所有等待打印的打印任务。

#### 有用选项

- `-P printername` 列出打印机 `printername` 的队列。
- `-a` 列出所有打印机的队列。
- `-l` 详细模式：以更长的格式显示信息。

### lprm

```
lprm [options] [job_IDs]
```

`lprm`（行打印移除）命令取消一个或多个打印任务。使用 `lpq` 获取所需打印任务的 ID（例如 `61` 和 `78`），然后输入：

```
$ lprm -P printername 61 78
```

如果你不提供任何任务 ID，则取消当前的打印任务。（只有超级用户可以取消其他用户的任务。）`-P` 选项指定哪个打印队列包含该任务。

## 拼写检查

`look` 快速查找单词的拼写。
`aspell` 交互式拼写检查器。
`spell` 批处理拼写检查器。

Linux 内置了数几个拼写检查工具。如果你习惯了图形化的拼写检查器，可能会觉得 Linux 的基于文本的工具相当原始，但它们可以在管道中使用，这非常强大。

### look

```
look [options] prefix [dictionary_file]
```

`look` 命令在标准输出上打印以给定字符串前缀开头的单词。单词位于字典文件（默认 `/usr/share/dict/words`）中：

```
$ look bigg
bigger
big
Biggs
```

如果你提供自己的字典文件——任何按字母顺序排序行的文本文件——`look` 将打印所有以给定前缀开头的行。

#### 有用选项

- `-f` 忽略大小写。
- `-tx` 匹配到包含终止字符的前缀。例如，`look -ti big` 会打印所有以 "bi" 开头的单词。

### aspell

```
aspell [options] file | command
```

`aspell` 是一个交互式拼写检查器。它识别无法识别的单词并提供替代方案。几个实用的命令有：

- `aspell -c file` 交互式检查并可选地纠正文件中的所有单词的拼写。
- `aspell dump master` 在标准输出上打印 `aspell` 主字典。
- `aspell help` 输出简洁的帮助信息。更多信息见 `http://aspell.net`。

### spell

```
spell [files]
```

`spell` 命令根据其字典（不是交互式的）打印给定文件中所有拼写错误的单词：

```
$ cat badwords
此 Linux 文件包含一些拼写错误。

你可能想知道拼写检查器会发现它们。仔细的用户应该在该文件上运行：
$ spell badwords
naturally
```

## 磁盘和文件系统

- `df` 显示挂载文件系统的可用空间。
- `mount` 挂载磁盘分区。
- `umount` 卸载磁盘分区（使其不可用）。
- `fsck` 检查磁盘分区的错误。
- `eject` 弹出 CD、DVD 或其他移动磁盘。

Linux 系统可以有多个磁盘或磁盘分区。在口语中，这些被各种称为磁盘、分区、文件系统、卷和目录。磁盘是一个硬件设备，可能被分为作为独立存储设备的分区。`/dev/` 中的常见设备有：

- `sda` 第一个块设备，分区为 `sda1`, `sda2`, ...
- `sdb` 第二个块设备；分区为 `sdb1`, `sdb2`, ... 同样适用于 `sdc`, `sdd`, ...
- `scd0` 第一个 SCSI CD-ROM 驱动器（然后是 `scd1`, `scd2`, ...）

分区持有数据，由一个在上面写入文件系统的程序“格式化”（参见**分区和格式化**）。文件系统定义了文件的表示；例如 `ext3`（日志文件系统）和 `ntfs`（Windows NT 文件系统）。安装 Linux 时通常会为你完成格式化。

一旦创建了文件系统，你可以将其挂载到空目录以使其可用。例如，如果你将 Windows 文件系统挂载到目录 `/mnt/win`，它就会变成目录树的一部分，你可以创建并编辑如 `/mnt/win/myfile`。挂载通常在启动时自动完成。文件系统也可以卸载以使其不可用，用于维护。

### 分区和格式化

在 Linux 系统上，分区和格式化等磁盘操作可能是复杂的。这里是你可能需要的程序（从它们的手册开始）：

- `gparted`, `parted`, `fdisk`, 或 `sfdisk` 分区硬盘。这些程序在大多数情况下都能工作。`gparted` 拥有最简单的用户界面。
- `mkfs` 格式化硬盘（即创建一个新的文件系统）。

### df

```
df [options] [disk devices | files | directories]
```

`df` (disk free) 程序显示给定磁盘分区的大小、已用空间和可用空间。如果你提供文件或目录，`df` 会描述该文件或目录所在的磁盘设备。你可以将文件系统挂载到非空目录，但在卸载之前目录的内容将变得不可用。不带参数时，`df` 报告所有挂载文件系统：

| Filesystem | 1k-blocks | Used | Avail | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/sda | 101928 | 225464 | 735060 | 24% | / |
| /dev/sda9 | 521748 | 249148 | 246096 | 51% | /var |
| /dev/sda8 | 806472 | 4088636 | 365984 | 54% | /usr |
| /dev/sda10 | 806472 | 4586576 | 3068044 | 60% | /home |

#### 有用选项

- `-k` 列出以字节为单位的大小（默认）。
- `-m` 列出以兆字节为单位的大小。
- `-BN` 以 `N` 字节块显示大小（默认=1024）。
- `-h` 打印易读输出，为每个大小选择最合适的单位。例如，如果你的磁盘分别有 1 GB 和 25 KB 可用空间，`df -h` 会打印 `1G` 和 `25K`。`-h` 选项使用 1024 的幂，而 `-H` 使用 1000 的幂。
- `-l` 只显示本地文件系统，不显示网络文件系统。
- `-T` 在输出中包含文件系统类型（`ext3`, `vfat` 等）。
- `-t type` 只显示指定类型的文件系统。
- `-x type` 不显示指定类型的文件系统。
- `-i` Inode 模式。显示每个文件系统的总、用和空闲 inode，而不是磁盘块。

### mount

```
mount [options] device | directory
```

`mount` 命令使分区可用。最常见的是处理磁盘驱动（例如 `/dev/sda1`）和移动介质（例如 USB 密钥），使其通过现有的目录（例如 `/mnt/mydir`）访问。

```
→ sudo mkdir /mnt/mydir
→ ls /mnt/mydir
→ sudo mount /dev/sda1 /mnt/mydir
→ ls /mnt/mydir
注意，它是空的
file1 file2 file3 挂载分区上的文件
→ df /mnt/mydir
```

| 文件系统 | 1K-块 | 已用 | 可用 | 使用率 | 挂载点 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/sda1 | 1011928 | 285744 | 647880 | 30% | /mnt/mydir |

`mount` 有许多选项和用法；我们将只讨论基础用法。

在最常见的情况下，`mount` 读取文件 `/etc/fstab`（文件系统表）来学习如何挂载指定的磁盘。例如，如果你输入 `/usr`，`mount` 命令会在 `/etc/fstab` 中查找 "usr"，该行可能看起来所示：

```
/dev/sda8 /usr ext3 defaults 1 2
```

在这里，`mount` 学习到的其他信息包括：设备 `/dev/sda8` 应该挂载到 `/usr`，作为一个 Linux `ext3` 格式的文件系统。现在你可以使用以下任一命令将 `/dev/sda8` 挂载到 `/usr`：

```
→ sudo mount /dev/sda8  # 按设备
→ sudo mount /usr       # 按目录
```

`mount` 通常由超级用户运行，但常见的移除式设备（如 USB 盘和 DVD）通常可以由任何用户挂载和卸载。

#### 有用选项

- `-t` 指定文件系统类型，例如 `ext3` 或 `ntfs`。
- `-l` 列出所有挂载的文件系统；也可以与 `-t` 配合。
- `-a` 挂载 `/etc/fstab` 中列出的所有文件系统。忽略包含 `noauto` 选项的条目。也可以与 `-t` 配合。
- `-r` 以只读模式挂载文件系统（请查看手册页中的某些免责声明）。

### umount

```
umount [options] [device | directory]
```

`umount` 的作用与 `mount` 相反：它通过文件系统使磁盘分区不可用。例如，如果你已经挂载了一张 DVD，在未卸载之前，你无法弹出它：

```
→ umount "/media/smith/My Vacation Photos"
```

在弹出移除式介质之前务必卸载它，特别是当它是可写时，否则可能会导致其文件系统损坏。卸载所有挂载的设备：

```
→ sudo umount -a
```

不要卸载正在使用的文件系统；事实上，出于安全考虑，`umount` 命令将拒绝这样做。

### fsck

```
fsck [options] [devices]
```

`fsck`（文件系统检查）命令验证 Linux 磁盘分区，并在需要时修复上面发现的错误。`fsck` 在系统启动时自动运行；但如果你愿意，也可以手动运行它。通常情况下，在检查设备之前卸载它，以便没有其他程序在同时对其进行操作：

```
→ sudo umount /dev/sda10
→ sudo fsck -f /dev/sda10
第 1 遍：检查 inode、块和大小
第 2 遍：检查目录结构
第 3 遍：检查目录连通性
第 4 遍：检查引用计数
第 5 遍：检查组摘要信息
home: 172/1281696 文件 (11.6% 非连续), ...
```

> 注意拼写是 “umount”，而不是 “unmount”。

在系统正常运行期间，你无法使用 `fsck` 修复根文件系统。你需要先从 Linux CD、DVD 或其他救援介质上启动系统。

`fsck` 是位于 `/sbin` 中一组文件系统检查程序的辅助程序，其名称以 “fsck” 开头。它只支持某些类型的文件系统；你可以通过以下命令列出它们：

```
→ ls /sbin/fsck.* | cut -d. -f2
```

#### 有用选项

- `-A` 按照顺序检查 `/etc/fstab` 中列出的所有磁盘。
- `-N` 打印将要执行的检查描述，但在不执行任何检查的情况下退出。
- `-r` 交互式地修复错误，在每次修复前进行提示。
- `-a` 自动修复错误（仅在你确实清楚自己在做什么时使用；若否则，你可能会严重搞坏文件系统）。

### eject

```
eject [options] [device_name]
```

`eject` 命令的作用与按下移除驱动器（如 CD-ROM 或 DVD 驱动器）上的打开/关闭按钮相同。这在你人离开电脑时弹出光片非常方便。当然，介质必须处于可以弹出的状态。

```
→ eject
```

#### 有用选项

- `-h` 显示帮助信息。
- `-n` 不弹出任何东西，只说明将要执行的操作。结合 `-v` 使用获取详细描述。
- `-v` 产生详细输出。
- `-d` 打印要弹出的默认设备名称（例如 `/dev/cdrom`），并退出。
- `-c N` 从多盘转换器中弹出第 `N` 张光片。

## 备份与远程存储

`rsync` 高效复制文件集，即使是跨网络。
`dd` 数据的低级拷贝。
`growisofs` 刻录 DVD 或蓝光光盘。

有多种方法可以备份你珍贵的 Linux 文件：

- 将它们拷贝到备份介质，如外部硬盘。
- 将它们刻录到可写的 CD、DVD 或蓝光光盘。
- 将它们镜像到远程机器。

我们并没有介绍所有可用的 Linux 备份命令。某些用户偏于使用 `cpio` 因为其灵活性，而长期管理员则认为 `dump` 和 `restore` 是备份所有类型文件的唯一可靠方法。

### rsync

```
rsync [options] source destination
```

`rsync` 命令复制文件集。它可以创建精确副本，包括文件权限和其他属性（称为镜像），也可以只复制数据。它可以在网络上或在单台机器上运行。`rsync` 有许多用途，关于选项，我们仅介绍与备份相关的几个案例。

在单台机器上将 `mydir` 及其内容镜像到另一个目录 `my2`：

```
→ rsync -a mydir my2
```

`rsync` 对你指定第一个目录的方式非常挑剔。如果你像示例中这样写 `mydir`，目录将被拷贝到 `my2` 中，创建 `mydir/`。这可能不是你想要的。如果你希望将内容拷贝到 `my2`，请在 `mydir` 加上一个斜杠：

```
→ rsync -a mydir/
```
