
# `dd` 命令

`root@localhost ~]# dd if=/dev/sda of=/dev/sdb`

`if` 选项用于指定输入设备。`of` 选项用于指定输出设备。在执行此命令时，请确保 `/dev/sdb` 硬盘的大小至少大于等于 `/dev/sda` 硬盘。

如果你没有硬盘，但在设备上有足够的空间（例如外部 USB 硬盘）怎么办？在这种情况下，将输出内容存到一个镜像文件中：

`root@localhost ~]# dd if=/dev/sda of=/mnt/had.img`

你也可以使用 `dd` 命令将 CD-ROM 或 DVD 的内容备份为 ISO 镜像：

`root@localhost ~]# dd if=/dev/cdrom of=cdrom.iso`

该 ISO 镜像文件可以用于创建更多的 CD-ROM。或者可以通过网络进行共享，使得 CD-ROM 的内容易于获取（而不是在办公室里传阅 CD-ROM 光盘）。

了解镜像和 ISO 文件在可以挂载和浏览时可以被视为普通文件系统也是很有帮助的：

```
root@localhost ~]# mkdir /test
root@localhost ~]# mount -o loop /mnt/had.img /test
```

`dd` 命令的优点之一是它可以备份硬盘上的任何内容，而不仅仅是文件和目录。例如，每个磁盘的开头都有一个被称为 MBR（主引导记录）的区域。对于引导磁盘，MBR 包含引导加载（GRUB）和分区表的副本。拥有这些数据的备份可能是有用：

```
root@localhost ~]# dd if=/dev/sda of=/mbr.img bs=512 count=1
```

`bs` 选项表示块大小，`count` 选项表示备份多少个块。512 和 1 的值是合理的，因为 MBR 的大小为 512 字节。
我建议将 MBR 镜像存储在外部设备上。如果系统因为 MBR 损坏而无法启动，你可以从恢复光盘启动并使用单个命令恢复 MBR：

`root@localhost ~]# dd if=mbr.img of=/dev/sda`

# `tar` 命令

`tar` 存档命令最初设计用于将文件系统备份到磁带设备。虽然现在许多人使用 `tar` 命令备份到非磁带设备，但你也应该了解如何使用磁带设备。

Linux 中的磁带设备名称遵循 `/dev/st*` 和 `/dev/nst*` 约定。第一个磁带设备名称被分配为 `/dev/st0`，第二个磁带设备通过 `/dev/st1` 访问。

`/dev/nst0` 也指向第一个磁带设备，但它不会向磁带发送回带信号。这在你需要向磁带写入多个卷时非常重要。磁带驱动器的默认行为是在备份完成后回带。如果你向同一块磁带写入另一个备份，除非你在执行第一次备份时使用了 `/dev/nst0` 设备，否则将覆盖第一个备份。

如果你正在操作磁带，应该了解 `mt` 命令。该命令允许你操作磁带，从一个卷移动到另一个卷以及删除磁带内容。一些示例：

```
[root@localhost #] mt -f /dev/nst0 1      # 跳过一个磁带卷
[root@localhost #] mt -f /dev/st0 rewind      # 回带磁带
[root@localhost #] mt -f /dev/st0 status      # 打印关于磁带设备的信息
[root@localhost #] mt -f /dev/nst0 erase      # 擦除磁带
```

**注意：** 在后续示例中，我假设你的系统中没有磁带驱动器。`tar` 命令提供的示例将 tar 包放在普通文件中；但如果你有磁带设备，可以将文件名替换为磁带设备文件。

要使用 `tar` 工具创建一个备份（即一个 tar 包），请使用 `-c`（创建）选项配合 `-f`（文件名）选项：

```
[root@localhost #] tar -cf /tmp/xinetd.tar /etc/xinetd.d
tar: 移除文件名开头的 '/'
```

文件名开头的 `/` 被移除，因此路径是相对路径。这使得指定恢复的位置变得更加容易。带有 `/` 会导致文件始终在完全相同的位置。

要查看 tar 包的内容，请使用 `-t`（列表）选项配合 `-f` 选项，如示例 18-1 所示。

### 示例 18-1 使用 `tar -tf` 查看 tar 包

```
[root@localhost #] tar -tf /tmp/xinetd.tar

etc/xinetd.d/
etc/xinetd.d/rsync
etc/xinetd.d/discard-stream
etc/xinetd.d/discard-dgram
etc/xinetd.d/echo-dgram
etc/xinetd.d/daytime-stream
etc/xinetd.d/chargen-stream
etc/xinetd.d/chargen-dgram
etc/xinetd.d/time-stream
etc/xinetd.d/telnet
etc/xinetd.d/echo-stream
etc/xinetd.d/tcpmux-server
```

在列出 tar 包内容时，通常你想查看详细信息。包含 `-v`（详细）选项以查看更多信息，如示例 18-2 所示。

### 示例 18-2 使用 `-v` 选项查看 tar 包详情

```
[root@localhost ~]# tar -tvf /tmp/xinetd.xinetd.tar

dr-xr-x root/root 0 2015-11-02 11:52 etc/xinetd.d/
-rw-r-- root/root 332 2014-03-28 03:54 etc/xinetd.d/rsync
-rw-r-- root/root 1159 2023-10-07 10:35 etc/xinetd.d/discard-dgram
-rw-r-- root/root 1157 2023-10-07 10:35 etc/xinetd.d/discard-dgram
-rw-r-- root/root 1149 2023-10-07 10:35 etc/xinetd.d/time-dgram
-rw-r-- root/root 1148 2023-10-07 10:35 etc/xinetd.d/echo-dgram
-rw-r-- root/root 1159 2023-10-07 10:35 etc/xinetd.d/daytime-stream
-rw-r-- root/root 1159 2023-10-07 10:35 etc/xinetd.d/chargen-stream
-rw-r-- root/root 1157 2023-10-07 10:35 etc/xinetd.d/chargen-dgram
-rw-r-- root/root 1157 2023-10-07 10:35 etc/xinetd.d/chargen-dgram
-rw-r-- root/root 1150 2023-10-07 10:35 etc/xinetd.d/time-stream
-rw-r-- root/root 302 2015-11-02 11:52 etc/xinetd.d/telnet
-rw-r-- root/root 112 2023-10-07 10:35 etc/xinetd.d/echo-stream
```

假设你的 tar 包包含了成千上万个文件，而你只需要其中几个文件。你可以通过列出 `tar` 命令的文件名来执行此部分恢复：

```bash
[root@localhost ~]# cd /tmp
[root@localhost ~]# tar -xf xinetd.tar etc/xinetd.d/rsync
[root@localhost ~]# ls etc/xinetd.d
```

```
[root@localhost #] ls etc/xinetd.d
xinetd.d
```
