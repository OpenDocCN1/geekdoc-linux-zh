
# 项目 6 磁盘管理

`/dev/sdb`: 107.4 GB, 1073418200 扇, 20971520 个扇

`Units = 1 * 512 = 512` 字节

分区大小(逻辑/物理): 512 字节 / 512 字节

`I/O` 大小(最小/最佳): 512 字节 / 512 字节

磁盘标签类型: `dos`

磁盘标识: `0xffe8c135`

设备 `Boot` `Start` `End` `Blocks` `Id` `System`

命令(输入 `m`): `w`

(5) 保存修改结果。使用 `w` 命令保存后，则在 `fdisk` 中做过的所有操作都会生效。如果分区表正确，则需要重启器才能使新的分区表生效。

命令(输入 `m`): `w`

```
The partition table has been altered!

Calling ioctl() to re-read partition table.

正在同步磁盘。
```

(6) 不保存修改结果。如果在此进行操作对磁盘分区进行了修改或删除，只需要 `q` 命令退出磁盘，则本次所有的操作都不会生效。

如果不重启就能生效以上的磁盘分区，需执行命令：

```
[root@localhost ~]# fdisk /dev/sdb
```

Linux 中养成磁盘工具是 `parted`，目前在实际环境中磁盘空间增大后，如果磁盘空间远大于 2 TB，就需要通过 `parted` 命令对磁盘分区操作。各选项的含义如下：

- `-help`: 显示帮助。
- `-l`: 列出所有设备信息。
- `-i`, `--interactive`: 在需要时提示。
- `-s`, `--script`: 不提示用户。
- `-v`, `--version`: 显示版本。

交互模式下命令的格式：

```
mkpart 分区类型 起始 结束
mkpart 分区类型 文件系统 起始 结束
quit
```

例 使用 `parted` 交互式分区。

① 选择分区的硬盘 `/dev/sdb`。

```
[root@localhost ~]# parted /dev/sdb
Welcome to GNU Parted! Type 'help' for a list of commands.
Warning: Partition table /dev/sdb exists and will be destroyed. Do you want to continue? Yes/No? Yes
```

例 3 将 `/dev/sdb2` 分区以 `xfs` 格式格式化，如图 6-2 所示，命令如下：

```bash
[root@localhost~] mkfs -t xfs /dev/sdb2
```

![](img/ec0e037f26e46c767b8ae4c4c4a36e86_118_0.png)

## 2) fsck

语法：`fsck [选项] 设备名`

功能：`fsck` 命令主要用于检查文件系统的正确性并对 Linux 磁盘进行修复。

各项选项含义如下：

- `-t`: 指定文件系统类型
- `-s`: 执行检查且时不进行提示
- `-C`: 显示检查进度条
- `-a`: 如果发现错误，则自动修复
- `-f`: 强制检查，即使文件系统干净

例 4 检查分区 `/dev/sdb1` 是否错误

```bash
[root@localhost~] fsck -a /dev/sdb1
```

通常情况下，无需用户手动执行 `fsck` 命令。在系统启动过程中，一旦系统检测到文件系统不一致，会自动运行 `fsck`。手动执行 `fsck` 命令应在用户模式且文件系统已卸载（`umount`）的情况下进行。

## 3. 文件挂载

Linux 对磁盘进行分区和格式化后，只有将分区挂载到系统目录树中的某个位置，才能被用户使用。

### 1) mount

语法：`mount [选项] 设备名`

功能：将设备挂载到挂载点处。设备是指要挂载的设备名，挂载点是指文件系统中已存在的目录。各项选项含义如下：

- `-t` 文件系统类型: 指定文件系统的类型，通常不必指定，`mount` 会自动识别正确的类型。
- `-a`: 挂载 `/etc/fstab` 文件中记录的所有设备。
- `-o<参数>`: 主要用于指定挂载分区或文件的挂载方式。通用参数有：
    - `loop`: 将一个文件当成块分区挂载到系统。
    - `ro`: 以只读方式挂载设备。
    - `rw`: 采用读写方式挂载设备。
    - `iocharset`: 指定访问系统时使用的字符集。

注意：挂载之前请先用 `fdisk -l` 或 `more /proc/partitions` 查看系统的硬盘及分区情况。

例 1 将 `/dev/sdb1` 和 `/dev/sdb2` 分别挂载到目录 `/dp1`、`/dp2`，命令如下：

```bash
[root@localhost ~] mkdir /dp1 /dp2
[root@localhost ~] mount /dev/sdb1 /dp1
[root@localhost ~] mount /dev/sdb2 /dp2
```

例 2 将光盘挂载到 `/mnt`，命令如下：

```bash
[root@localhost ~] mount /dev/cdrom /mnt
```

U盘在 Linux 中是一个非 IDE 设备，其命名规则与普通硬盘设备相同。由于系统中已经有了两块 SCSI 硬盘，插入 U 盘时其设备名为 `/dev/sdc`。由于格式为 `vfat`，

例 3 将 U 盘的第一个分区挂载到 `/dev/sdc1/mnt` 并指定文件系统类型为 `vfat`，命令如下：

```bash
[root@localhost ~] mount -t vfat /dev/sdc1 /mnt
```

### 2) unmount

对于已挂载的设备，如果不使用，可以使用 `umount` 命令将其卸载。`umount` 介绍如下：

语法：`umount [选项] [挂载点]或[设备名]`

功能：卸载通过 `mount` 命令挂载的文件系统。

```bash
[root@localhost ~] umount /dev/cdrom
[root@localhost ~] umount /mnt
```

### 3) 自动挂载

`fstab` (file system table) 是一个纯文本文件，系统启动时会自动读取该文件内容并挂载其中的文件系统。虽然可以使用 `mount` 命令手动挂载，但将挂载信息写入 `/etc/fstab` 文件可以实现开机时自动挂载。

查看 `/etc/fstab` 文件内容：

```bash
[root@localhost ~] cat /etc/fstab

#/etc/fstab
# Created by root on Tue Oct 24 10:55
# Filesystems listed on root:
# See fstab(5), mount(8) or blkid(8) for info

| device | mount | type | options | pass |
|---|---|---|---|---|
| UUID=... | / | xfs | defaults | 1 |
| UUID=... | / | xfs | defaults | 0 |
| UUID=... | /home | xfs | defaults | 1 |
| UUID=... | swap | swap | defaults | 0 |
```

## 4. 其他磁盘命令

### df

功能：检查文件系统的磁盘占用情况，获取磁盘使用了多少空间。显示块数、使用量、剩余节点（`inode`）及挂载点。选项含义如下：

- `-a`: 显示所有文件系统（包括伪文件系统）。
- `-k`: 以 KB 为单位显示。
- `-i`: 显示 `inode` 信息。
- `-t`: 显示文件系统磁盘空间。
- `-T`: 显示文件系统类型。

例 1 列出当前文件系统的占用情况：

```bash
[root@localhost ~] df
```

例 2 列出文件系统类型：

```bash
[root@localhost ~] df -T
```

### du

语法：`du [选项] [Names]`

功能：统计目录（或文件）的大小。允许逐级进入目录并显示占用数据。若给出 `Names`，则对指定目录进行统计。

- `-a`: 列出所有文件的空间。
- `-c`: 在最后输出总计。

例 以字节单位列出所有文件的占用情况：

```bash
[root@localhost ~] du -a
```

## 5. 备份与恢复

语法：`dump [选项] 备份文件名 原文件或目录`

功能：`dump` 作为备份程序，可以将目录或整个文件系统备份至指定设备或备份为文件。`dump` 命令支持 0~9 十个备份级别：0 级全备份，1~9 级增量备份。

注意：只有在备份分区或块设备时才支持 1~9 增量级别；如果只是备份单个文件，只能使用 0 级。

选项含义如下：

- `-u`: 备份完成后，在 `/var/dump` 中记录备份信息（级别、时间等）。
- `-level`: 指定级别（0~9）。
- `-v`: 显示备份过程的详细输出。
