
1386-redhat-linux 1486-linux-libc5 include info

`[root@server test]# cd /usr/i386-redhat-linux/`

```
```

# 设置 CD-ROM 驱动器

Linux 中并不存在 Windows 和 Macintosh 中那种“驱动器”概念。在 Linux 中使用 CD-ROM 时，必须将其挂载（grafted）到目录结构中才能进行访问。

这种挂载过程被称为“挂载”（mounting）。挂载通过 `mount` 命令执行；卸载通过 `umount` 命令执行，通常只有超级用户（Super-user）可以使用。软盘也必须挂载。

## 挂载和使用 CD-ROM 及其他驱动器

在 Linux 中，所有磁盘都构成以 `/` 为根的目录层次。Linux 目录结构是一个巨大的树，磁盘作为目录分支出来。当磁盘和驱动器在挂载操作中链接在一起，磁盘就可以作为目录的一部分被访问：

## 挂载磁盘的类型

有很多类型的磁盘。使用附加在 `mount` 命令后的 `-t` 选项指定要挂载的磁盘类型。例如，指定 `iso9660` 来挂载 CD-ROM。对于 Windows 格式的软盘，使用 `mount -t ext2 /dev/fd0 /mnt` 命令。

### 在 Linux 中使用 CD-ROM

- 插入 CD-ROM。
- 将红 Hat Linux CD-ROM 插入 CD-ROM 驱动器。

![](img/d549b948a29b14d0d8313a8ed09b5698_81_0.png)

检查要挂载 CD-ROM 驱动器的目标目录。

```
[root@server /root]# ls -lF /mnt/cdrom@
total 0
[root@server /root]#
```

- 输入命令。

注意：仅仅插入 CD-ROM 并不会将其挂载。

## 挂载 CD-ROM。

输入命令。

```
[root@server /root]# ls -lF /mnt/cdrom
total 0
[root@server /root]# mount -t iso9660 /dev/cdrom /mnt/cdrom
mount: device /dev/cdrom is write-protected, mounting read-only
ISO9660 Extensions: Microsoft Joint Level 3
[root@server /root]#
```

将显示一条消息，指示格式状态和其他信息。

输入命令。

```
[root@server /root]# mount -t iso9660 /dev/cdrom /mnt/cdrom
mount: device /dev/cdrom is write-protected, mounting read-only
ISO9660 Extensions: Microsoft Joint Level 3
[root@server /root]# ls -lF /mnt/cdrom
total 113
-drwxr-xr-x 1 root root 1986 May 29 05:14 COMING
-drwxr-xr-x 1 root root 3017 Oct 13 05:14 README
-drwxr-xr-x 5 root root 510 2751 Sep 20 19:57 RPM-PGP-KEY
-drwxr-xr-x 5 root root 2048 Jan 29 09:06 RedHat/
-drwxr-xr-x 2 root root 63488 Jan 29 09:06 SRMS2/
-drwxr-xr-x 1 root root 580 Feb 13 19:59 TRANS.TBL
-drwxr-xr-x 4 root root 2048 Jan 29 09:06 boot.cat
-drwxr-xr-x 4 root root 2048 Feb 11 05:04 dekiru/
-drwxr-xr-x 6 root root 4096 Jan 29 09:06 doc/
-drwxr-xr-x 2 root root 2048 Jan 29 09:06 images/
-drwxr-xr-x 2 root root 2048 Feb 11 05:05 macintosh/
-drwxr-xr-x 5 root root 2048 Jan 2 1970 misc/
-drwxr-xr-x 2 root root 2048 Oct 15 17:43 moved/
-drwxr-xr-x 2 root root 2048 Feb 11 05:24 windows/
[root@server /root]#
```

## 卸载移除磁盘

要移除 CD-ROM 或强制卸载处于挂载状态的磁盘，必须使用卸载命令（`umount -n`），对于 CD-ROM，命令为：

```
root@server /root]# umount /mnt/cdrom
```

## 卸载以移除磁盘

要移除 CD-ROM 或强制卸载处于挂载状态的磁盘，必须使用卸载命令（`umount -n`），对于 CD-ROM，命令为：

```
root@server /root]# umount /mnt/cdrom
```

## 卸载以移除磁盘

要移除 CD-ROM 或强制卸载处于挂载状态的磁盘，必须使用卸载命令（`umount -n`），对于 CD-ROM，命令为：

```
root@server /root]# umount /mnt/cdrom
```

## 卸载以移除磁盘

要移除 CD-ROM 或强制卸载处于挂载状态的磁盘，必须使用卸载命令（`umount -n`），对于 CD-ROM，命令为：

```
root@server /root]# umount /mnt/cdrom
```

## 卸载以移除磁盘

要移除 CD-ROM 或强制卸载处于挂载状态的磁盘，必须使用卸载命令（`umount -n`），对于 CD-ROM，命令为：

```
root@server /root]# umount /mnt/cdrom
```

# Linux 关机命令

在 Linux 中，`shutdown` 命令用于计划关机或重启系统。它会通知所有登录用户系统将要关机。

### shutdown 命令的语法

`shutdown [option] [time] [message]`

- `-h`: 关机。
- `-r`: 机后重启。
- `-c`: 取消已计划的关机。

### 关机时间

- `now`: 立即关机。
- `+30`: 在 30 分钟后关机。
- `06:00`: 在凌晨 6:00 关机。

### 消息

你可以为 `shutdown` 命令附加发送给登录用户的消息。

```bash
shutdown +5 "because of power cut"
```

### 消息

向所有通过 telnet 连接的用户显示以下消息：

```
Broadcast message from root (ttyp0) Tue Jan 26 15:07:08 1999... because of power cut The system is going DOWN to maintenance mode in 5 minutes !!
```

## 关机命令

在 Linux 中，关机命令可以通过以下方式执行：

```
root@server /root]# shutdown -h now
```

## 关机命令

在 Linux 中，关机命令可以通过以下方式执行：

```
root@server /root]# shutdown -r now
```

## 关机命令

在 Linux 中，关机命令可以通过以下方式执行：

```
root@server /root]# shutdown -c
```

## 关机命令

在 Linux 中，关机命令可以通过以下方式执行：

```
root@server /root]# shutdown +30
```

## 关机命令

在 Linux 中，关机命令可以通过以下方式执行：

```
root@server /root]# shutdown 06:00
```

## 关机命令

在 Linux 中，关机命令可以通过以下方式执行：

``` evenroot@server /root]# shutdown +5 "because of power cut"
```

### 消息

向所有通过 telnet 连接的用户显示以下消息：

```
Broadcast message from root (ttyp0) Tue Jan 26 15:07:08 1999... because of power cut The system is going DOWN to maintenance mode in 5 minutes !!
```

## 关机命令

在 Linux 中，关机命令可以通过以下方式执行：

```
root@server /root]# shutdown -h now
```
