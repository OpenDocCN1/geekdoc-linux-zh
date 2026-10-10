
## /etc/fstab

/etc/fstab 是 Linux 系统上最重要的配置文件之一。它以列形式列出当前可用的块设备（参见“/etc/fstab 中的字段”表格）。该文件指定了块设备驱动程序，指示挂载点，指定文件系统类型（参见“文件系统类型”表格），并指示要执行的挂载类型（参见“挂载选项”表格）。以下是 /etc/fstab 的一个示例：

```
/dev/hda8 / ext2 defaults 1 1
/dev/hda5 /home ext2 defaults 1 2
/dev/hda1 /home/bryan/ auto defaults 0 0
/dev/hda7 /usr ext2 defaults 1 2
/dev/hda9 /usr/local ext2 defaults 1 2
/dev/hda6 swap swap defaults 0 0
/dev/fd0 /mnt/floppy ext2 noauto, user 0 0
/dev/cdrom /mnt/cdrom iso9660 user,noexec, nodev, suid,rw 0 0
none /proc proc defaults 0 0
none /dev/pts devpts gid=5, mode=620 0 0
```

### /etc/fstab 中的字段

| 使用此字段 | 用于指示 | 示例 |
| :-- | :-- | :-- |
| fs_spec | 块特殊设备或远程文件系统。 | 硬盘：/dev/hda1<br>CD-ROM 驱动器：/dev/cdrom<br>软盘驱动器：/dev/fd0<br>NFS 挂载（主机名：目录）：lothlorien.mymdomain.org: /home/suzanne<br>Proc 文件系统：proc |
| fs_file | 指定文件系统的挂载点。 | 交换分区：指定 none<br>根文件系统：/<br>CD-ROM 驱动器：/mnt/cdrom<br>软盘驱动器：/mnt/floppy |
| fs_vfstype | 文件系统类型。有关可用选项，请参见本节的“文件系统类型”表格。 | Linux 文件系统：ext2<br>MS-DOS 文件系统：MsdOS<br>Windows 95/98 文件系统：vfat |
| fs_mntops | 以逗号分隔的列表形式的挂载选项。有关可用选项，请参见本节的“挂载选项”表格。 | 硬盘：defaults<br>软盘驱动器：user, owner, exec, dev, suid, rw, noauto<br>CD-ROM 驱动器：user, owner, exec, dev, suid, ro, noauto |
| fs_freq | 转储频率。<br>0 不转储。<br>1 启用转储。 | 硬盘：1<br>CD-ROM 驱动器：0<br>软盘驱动器：0 |
| fs_passno | 启动时文件系统检查的顺序。<br>0 不检查。<br>1 首先检查。<br>2 稍后检查。 | 根分区：1<br>其他分区：2<br>CD-ROM 驱动器：0<br>软盘驱动器：0 |

### 文件系统类型

| 使用此类型 | 用于挂载此类型的文件系统 |
| :--- | :--- |
| adfs | Acorn 高级磁盘文件系统 |
| affs | Amiga 快速文件系统 |
| auto | 用户挂载的软盘（自动检测文件系统） |
| ext2 | Linux 扩展文件系统 2 |
| hfs | OS/2 文件系统 |
| iso9660 | CD-ROM 文件系统 |
| msdos | MS-DOS 磁盘或分区 |
| ncdfs | Novell NetWare 文件系统 |
| nfs | 网络文件系统 |
| ntfs | Windows NT 磁盘或分区 |
| proc | 用于系统设备的 Proc 文件系统 |
| smbfs | Windows NT 服务器文件系统 |
| smbfs | Samba 共享 |
| sysv | UNIX System V 文件系统 |
| umsdos | 位于 MS-DOS 分区上的 Linux |
| vfat | Windows 95/98 磁盘或分区 |

### 挂载选项

| 使用此选项 | 用于执行此操作 |
| :--- | :--- |
| async | 在不同时间执行输入和输出操作。 |
| atime | 更新每次访问的访问时间。这是默认设置。 |
| auto | 允许文件系统通过 **mount -a** 命令进行挂载，该命令常见于启动脚本中。 |
| defaults | 使用以下默认选项：**async**、**auto**、**dev**、**exec**、**nouser**、**rw**、**suid**。 |
| dev | 解释字符或块特殊设备。 |
| exec | 启用二进制文件的执行。 |
| noatime | 跳过在每次访问时更新访问时间。此选项可提高新闻或邮件服务器的文件系统性能。 |
| noauto | 要求手动挂载文件系统。此选项不会通过 **mount -a** 进行挂载。 |
| nodev | 跳过字符或块特殊设备。 |
| noexec | 防止执行二进制文件。 |
| nosuid | 防止使用设置用户 ID 或设置组 ID 权限。 |
| nouser | 防止普通用户挂载文件系统。 |
| remount | 尝试重新挂载已挂载的文件系统。 |
| ro | 以只读方式挂载文件系统。 |
| rw | 以读写方式挂载文件系统。 |
| suid | 允许在指定设备上使用设置用户 ID 和设置组 ID 权限。 |
| sync | 同时执行输入和输出操作。 |
| user | 允许普通用户挂载文件系统。 |

## /etc/mtab

/etc/mtab（称为挂载表）由 mount 和相关实用程序自动更新，显示系统中当前挂载的块设备。其中显示了设备名称、文件系统类型和设置。以下是 /etc/mtab 文件部分内容的一个示例：

```
/dev/hda8      /         ext2    rw   0 0
none           /proc     proc    rw   0 0
/dev/hda5      /home     ext2    rw   0 0
/dev/hda1      /home/bryan ext2   rw   0 0
/dev/hda7      /usr      ext2    rw   0 0
/dev/hda9      /usr/local ext2   rw   0 0
```

## 按字母顺序排列的命令参考

本节详细说明了用于以下任务的命令：

- 分析和修复 Linux ext2 文件系统（badblocks, debugfs, e2fsck, fsck, tune2fs）
- 创建紧急启动软盘（dd, rdev）
- 显示可用磁盘空间和磁盘使用信息（df, du, dump2fs, sync）
- 挂载和卸载文件系统（hmount, humount, mount, umount）
- 为使用准备新的硬盘（cfdisk, fdisk, mke2fs）
- 处理软盘、CD-ROM 和磁带驱动器（autorun, eject, fdformat, hformat, mt, setfdprm）

### autorun

**autorun [ 选项 ] [ 设备 ]**  
自动识别当前系统中所有可用的 CD-ROM 驱动器，在插入磁盘时将其挂载，并可选地执行指定的应用程序，例如音频 CD-ROM 播放器。要使用 autorun，必须在 /etc/fstab 中的 CD-ROM 驱动器条目中添加挂载选项 user 和 exec。

**选项**

| 使用此选项 | 用于执行此操作 |
| --- | --- |
| -a 命令 | 如果 CD-ROM 发生变化，则运行指定的命令。 |
| -c 命令 | 如果插入音频 CD-ROM，则运行指定的命令。 |
| -i 时间 | 指定检查之间等待的时间（以毫秒为单位）。 |
| -l | 锁定已挂载的介质，使其必须手动卸载。 |
| -m | 仅执行挂载和卸载操作。不执行命令。 |
| -n 字符串 | 如果 CD-ROM 发生变化，则显示指定的字符串。 |
| -t 字符串 | 如果插入 CD-ROM，则显示指定的字符串。 |
| -e 字符串 | 如果弹出 CD-ROM，则显示指定的字符串。 |
| -q | 隐藏所有输出。 |
| -v | 显示所有消息。 |
| -7, -help | 显示可用选项。 |
| -usage | 显示简短的使用说明消息。 |
| -V | 显示程序版本。 |

### badblocks

```
badblocks [ 选项 ] 设备
```

扫描指定设备中的损坏段，也称为*坏扇区*。

**选项**

| 使用此选项 | 用于执行此操作 |
| :--- | :--- |
| `-b size` | 指定默认块大小。默认为 512。 |
| `-o filename` | 将坏块列表写入指定的文件名。 |
| `-s` | 显示命令的进度。 |
| `-v` | 显示消息。 |

**示例**

| 此命令 | 执行以下操作 |
| :--- | :--- |
| `badblocks -s /dev/sda1` | 扫描指定设备中的坏扇区并显示进度指示器。 |

### cfdisk

```
cfdisk [ 选项 ] [ 设备 ]
```

启动文本模式的交互式硬盘分区实用程序（不需要 X）。需要 root 用户状态（参见第 1 章中的 su）。需要块大小。

> **警告** 不要在对包含有价值数据的磁盘上运行此实用程序。

**选项**

| 使用此选项 | 用于执行此操作 |
|:----------------|:-----------|
| -a | 使用光标突出显示当前分区，而不是使用反色 |
| -c *n* | 指定柱面数（*n*） |
| -h *n* | 指定磁头数（*n*） |
| -s *n* | 指定扇区数（*n*） |
| -Z | 不读取当前分区表 |
| -P <*r* \| *s* \| *t*> | 指定格式：<br>- r 原始数据<br>- s 扇区顺序<br>- t 格式化的原始数据 |

**命令**

| 使用此命令 | 用于执行此操作 |
|:-----------------|:-----------|
| 上箭头（↑）、下箭头（↓） | 在分区之间移动 |
| b | 切换引导标志 |
| d | 删除分区 |
| g | 指定新的磁盘几何参数（柱面、磁头或扇区） |
| h | 显示可用选项 |
| m | 使用最大可用空间 |
| n | 创建新分区 |
| p | 显示分区表 |
| q | 不保存分区信息并退出 |
| t | 指定新的文件系统类型 |
| u | 更改分区大小单位 |
| W | 保存分区信息 |

