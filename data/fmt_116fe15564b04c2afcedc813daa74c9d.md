
| 次级 IDE 控制器 0 或主 (Master) | `/dev/hdc` or `hdc` |

| 次级 IDE 控制器 1 或从 (Slave) | `/dev/hdd` or `hdd` |

| SCSI 控制器-SCSI ID 0 | `/dev/sda` or `sda` |

| SCSI 控制器-SCSI ID 1 | `/dev/sdb` or `sdb` |

| SCSI 控制器-SCSI ID 2 | `/dev/sdc` or `sdc` |

## 148 第二部分 + 安装

当你尝试确定 Linux 中的硬盘命名时，此硬盘硬盘识别表是一个极佳的起点。然而，此表只是基础性的，因为它只考虑了单 IDE 或 SCSI 控制器。磁盘上的分区编号为 1-X，其中 X 是分区的总数。因此，在上述 `/etc/lilo.conf` 示例中，硬盘是 `/dev/hda` 或主 IDE 控制器。Microsoft Windows 9X 安装在此驱动器的第一个分区上，即 `hda1`。通过添加以下行将 Microsoft Windows 添加到 LILO 菜单：

```
other=/dev/hda1
label=dev/hda1
```

你可以通过在 LILO 启动提示符处输入 `windows` 来从 LILO 构建 Microsoft Windows。如果 Microsoft Windows 9X 已经添加到 Linux PC 电脑中，这种方法同样适用。你可能需要重新安装 LILO 才能在安装期间启动，但如果你在安装 Linux 期间创建了可引导软盘，这种情况你已经做好了准备。通过该软盘，如果 LILO 在安装 Microsoft Windows 期间损坏，你有能力恢复它。

## 带有 Microsoft Windows NT 和 2000 的 Linux

与 Windows NT 和 2000 进行双引导更为复杂。如果你使用 FAT16 或 FAT32 分区作为 Microsoft Windows NT 或 2000 操作系统，则用于 Microsoft Windows 9X 的方法应该是有效的。但是，如果你使用的是 NTFS 系统，则 NT 引导加载程序与 MBR 中的 LILO 不兼容。这意味着 LILO 不能安装在 MBR 中，否则 Microsoft 操作系统将无法启动。要解决这种情况，请将 LILO 安装在 Linux 的根分区和软盘上。完成 Linux 的安装，并使用你启动时用的软盘重启系统。进入 Linux 后，使用以下命令将启动扇区的二进制镜像拷贝到空白磁盘：

```
-t msdos /dev/fdb0 /mnt/floppy
```

```
dd if=/dev/hda5 bs=512 count=1 of=/mnt/floppy/linux.bin
```

拔掉软盘并重启系统进入 Microsoft Windows NT 或 2000。你需要编辑 `boot.ini` 文件。用纯文本编辑器打开 `boot.ini`，将其作为记事本，并添加以下行：

```
c:\linux.bin="*Windows"
```

保存 `boot.ini` 文件并退出文本编辑器。然后，将 `linux.bin` 文件从软盘拷贝到 Microsoft Windows 硬盘根目录下的 HDD 中。这允许 Microsoft Windows NT 或 2000 的启动菜单显示 Linux 行，并赋予它 `linux.bin` 文件，该文件包含了详细说明如何启动此操作系统的指令。这应该允许 Linux 与 Microsoft Windows NT 2000 进行双引导。

## Linux 与 Solaris

你可以轻松实现 Linux 与 Solaris 双引导。要在 Linux 和 Solaris 之间创建双引导：

- 1. 在系统上安装 Linux。为 Linux 根创建分区 8，为 Linux交换交换分区 7，将分区 1 留给 SunOS 根，分区 2 留给 SunOS 交换。
- 2. 在 Linux 根分区安装 SILO（Spar 实现引导器），它是 Sun 平台中等同于 LILO 的工具。
- 3. 允许 Solaris 在 `nvalias` 中创建一个项目以允许系统启动。
- 4. 启动系统以验证 Linux 安装是否成功。
- 5. 停止系统并继续安装 Solaris。当 Solaris 安装程序询问是否保留数据时，选择“是”。
- 6. 安装完成后，使用 `tar` 提取二进制文件并运行。
- 7. 使用 `tar` 对之前创建的归包提取文件、存储额外文件或更新/列出已存储的文件。
- 8. 要从 `tar` 归包中提取，使用 `tar` 命令，其格式为 `tar -xvf <name>.tar`。

```
nvalias <path_from_above>0
env boot-device default
env disk
```

这种配置允许 Solaris。

## Linux 与其他系统

Linux 可以通过多种配置方式与其他系统进行双引导。需要记住的一个主要责任是始终备份现有操作系统上的数据，以防万一。如果你有只能在特定系统中运行的应用程序或工具，与其他系统进行双引导是有用的。

## 使用 gzip 和 tar 安装额外软件

### 2.17 在安装操作系统后安装和卸载应用程序（例如 RPM, tar, gzip）

`gzip`（GNU zip）是一个旨在取代原始 Unix `compress` 的压缩工具。`gzip` 工具用于压缩文件以节省空间并传输大文件。第一步是解压文件，你可以通过 `gzip` 完成，它通过格式 `gzip<name>.gz` 解压文件。完成后，你会得到一个扩展名为 `tar` 的文件。

`tar` 文件是多个文件的单一归包，可以创建在磁盘或磁带上。它支持跨介质，可以将数据保存到软盘等多个介质上，并支持增量和差异备份以提供灵活性。因此，你可以使用 `tar` 对之前创建的归包提取文件、存储额外文件或更新/列出已存储的文件。

## 使用 RPM 安装额外软件

### 2.17 在安装操作系统后安装和卸载应用程序（例如 RPM, tar, gzip）

### 2.19 验证已安装的应用程序在测试和生产环境中均运行正常

`RPM` 代表 Red Hat 包管理器，是一个对所有人开放的开放软件包系统。`RPM` 用于检索代码并将其封装成二进制格式。这些二进制文件可以安装和跟踪，且源码易于重新构建。`RPM` 维护一个已安装软件包的可搜索数据库，用于跟踪软件包的所有文件，并可以提供有关已安装软件包的信息。`RPM` 数据库用于赋予 `RPM` 命令安装、升级和删除软件包的能力。`RPM` 使用开关来执行特定任务。表 5-3 是 `RPM` 使用的开关列表。

## 表 5-3

Red Hat 软件包管理器安装命令

| 使用的开关 | 选项执行此任务 |
|--- |---|

| `-i` 或或 `--install` | 用于从 RPM 安装 |
| `--dbpath <path>` | 使用 `<path>` 查找 RPM 数据库 |
| `--excludedocs` | 不安装文档 |
| `--force` | 忽略包和文件冲突 |
| `--ffport <port>` | 使用 `<port>` 作为 FTP 端口 |
| `--ftpproxy <host>` | 使用 `<host>` 作为 FTP 代理 |
| `-h` | 在安装期间打印哈希标记（#） |
| `--ignorearch` | 不验证包的架构 |
| `--ignoreos` | 不验证包的操作系统 |
| `--includedocs` | 安装文档 |
| `--nodeps` | 不检查依赖关系 |
| `--noscripts` | 不执行安装前和后脚本 |
| `--percent` | 在安装期间打印百分比 |
| `--prefix <path>` | 如果可能，将包重定位到另一个 `<path>` |
| `--rcfile <rcfile>` | 将备用 rpm 文件设为 `<rcfile>` |
| `--replacefiles` | 替换由另一个包所有的文件 |
| `--replacekgs` | 用新副本替换包 |
| `--root <path>` | 设置备用根目录为 `<path>` |
| `--test` | 仅执行安装测试 |
| `-v` | 显示额外信息 |
| `-w` | 显示调试信息 |

`RPM` 最基础的安装命令是 `-i filename-1.2.2.i386.rpm`。然而，最常用的安装 `RPM` 命令是 `rpm -iv filename-1:2.2.i386.rpm`，它会显示额外的哈希标记以说明 `RPM` 仍在运行，这对于安装时间较长的大型 `RPM` 包很有帮助。你可以使用其他选项，但通常情况下这是一个基础的 `RPM` 命令。

- 你需要了解与 `RPM` 命令一起使用的格式和开关。

## 使用 RPM 移除软件

`RPM` 具有从系统中删除软件包的能力。请使用表 5-4 中的开关来完成此任务。

### 表 5-4

Red Hat 软件包管理器删除命令

| `rpm` 命令中使用的开关 | 选项执行此任务 |
| --- | --- |
| `-e` | 删除一个或多个包 |
| `--dbpath <path>` | 使用 `<path>` 查找 RPM 数据库 |
