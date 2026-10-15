
https://t.me/CCNA_SECURITY
https://t.me/CCNPSECURITY

# 256 第 7 章 存储与文件系统管理

### 图 7-2

| Filesystem | Size | Used | Avail | % | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| [root@server1]# -h devtmpfs | 4.0M | 0 | 4.0M | 0% | |
| tmpfs | 827M | 0 | 872M | 0% | /dev/shm |
| tmpfs | 349M | 9.8M | 339M | 3% | / |
| /dev/mapper/rhel-root | 15G | 3.9G | 12G | 26% | |
| /dev/mapper/rhel-home | 1014M | 44M | 971M | 5% | /home |
| /dev/nme01 | 1014M | 28M | 730M | 29% | /boot |
| tmpfs | 175M | 104K | 175M | 1% | /root/user/1000 |
| [root@server1]# | | | | | |

`df` 命令的人类可读格式输出

若要以更易读的格式打印分区，可以使用 `-h` 命令选项，如图 7-2 所示。`-h` 命令的输出与 `-h` 类似，但虽然 `-h` 以 KB、MB 和 GB 等国际单位打印大小，而 `-h` 以 KiB（二进制千字节）、MiB（二进制兆字节）和 GiB（二进制吉字节）单位打印大小。这种差异在第 1 章中进行了简要解释。在国际单位中，倍数用 10 的幂表示。因此，1KB=1000 字节，1MB=1000000 字节，依此类推。相反，KiB、MiB 和 GiB 使用 2 的幂。因此，1KiB=1024 字节，MiB=1048576 字节，GiB=1073741824 字节。你必须根据上下文识别单位。例如，如果你被要求创建一个 1GB 的分区，它等同于 1024 MiB，或者等同于 1024 x 1024 字节。`mount` 命令列出了每个文件系统的格式和选项。检查由 `/dev/mapper/rhel-home` 表示的分区的输出。注意它挂载在 `/home`，类型为 `xfs`。该文件系统的目的是将普通用户的家目录分离到专用目录中。

```
[root@server1]# grep home
/dev/mapper/rhel-home on /home type xfs (rw,rel,seclabel,attr2,inode64
```

如果 `mount` 命令的输出让你困惑，可以考虑使用 `find` 命令，它可以以树状格式打印所有文件系统，如图 7-3 所示。在输出中，请注意 `proc` 和 `sysfs` 等“特殊文件系统”，我们将在本章后面的部分介绍。

# 存储管理与分区 257

### 图 7-3 find 命令的输出

| TARGET | SOURCE | TYPE | OPTIONS |
| :--- | :--- | :--- | :--- |
| [root@server1]# find /dev/mapper/rhel-root | | | rw,relatime,seclabel,attr2,inode64,logbuf |
| /proc | proc | xfs | rw,relatime,noduid,noexec,relatime |
| /sys/fs/binfmt_misc | proc | autofs | rw,relatime,timeout=0,min |
| /sys/kernel/security | kernel | security | rw,relatime,noduid,noexec,seclabel |
| /sys/fs/cgroup | cgroup2 | | rw,relatime,noduid,noexec,seclabel |
| /sys/fs/pstore | pstore | | rw,relatime,noduid,noexec,seclabel |
| /sys/fs/selinux | selinux | | rw,relatime,noduid,noexec,relatime=700 |
| /sys/kernel/debug | debugfs | | rw,relatime,noduid,noexec,seclabel |
| /sys/kernel/tracing | tracefs | | rw,relatime,noduid,noexec,seclabel |
| /sys/fs/connections | fusectl | | rw,relatime,noduid,noexec,seclabel |
| /sys/kernel/config | devtmpfs | | rw,relatime,seclabel,size=4096K,nr_inodes=1 |
| /dev/sh | tmpfs | | rw,relatime,noduid,noexec,seclabel |
| /dev/hugepages | devpts | | rw,relatime,noduid,seclabel,gid=5 |
| /dev/mqueue | hugetlbfs | | rw,relatime,seclabel,size=17 |
| /run | mqueue | | rw,relatime,noduid,noexec,seclabel |
| /run/credentials/systemd-users.service | | | rw,relatime,noduid,noexec,relatime=700 |
| /run/vmblock-fuse | none | fuse.vmw | rw,relatime,relative,user_id=0,id=0 |
| /run/user/1000 | tmpfs | | rw,relatime,seclabel,size=17 |
| /run/user/1000/gvfs | gvfs-fuse | | rw,relatime,noduid,relative,user_id=1000,gro |
| /home | /dev/mapper/rhel-home | | rw,relatime,seclabel,attr2,inode64,logbuf |
| /boot | /dev/nme0n1 | xfs | rw,relatime,seclabel,attr2,inode64,logbuf |

## fdisk 工具

`fdisk` 是许多操作系统通用的。macOS 拥有功能完整的 `fdisk`。Windows 版本有一个简化的系统，而 Linux 的 `fdisk` 实现包含了多种命令，你可能只需要知道其中几个。

`fdisk` 适用于使用传统主引导记录（MBR）分区方案的分区。在使用 UEFI 而非传统 BIOS 的新系统上，你可能会看到不同的分区：GUID 分区表（GPT）。虽然在 RHEL 8 的早期版本中，针对 GPT 的 `fdisk` 被认为是实验性的，但今天 `fdisk` 可以处理 GPT 分区。尽管如此，在本章中，我们将演示如何使用 `fdisk` 和 `parted` 来管理它们。

## 启动 fdisk：帮助和其他

以下屏幕输出列出了显示如何启动 `fdisk`、如何获取帮助以及如何退出提示符的命令 `getdev/sda` 与 Linux 系统上的第一个驱动器相关，但在你的机器上可能会不同，例如 NVMe 驱动器。其他系统可能配置了不同的硬盘文件名，你可能需要检查 `df` 和 `fdisk -l` 命令的输出来寻找线索。

```
# fdisk /dev/sda
```

欢迎使用 fdisk (util-linux 2.37.4)。
更改将仅留在内存中，直到你决定写入它们。
在使用写入命令之前要小心。

Command (m for help): m

Help:

+   DOS (MBR)
a 切换可启动标志
edit 嵌套 BSD disklabel
t 切换 dos 兼容性标志

+   Generic
d 删除分区
f 列出空闲分区空间
l 列出已知分区类型
n 添加新分区
p 打印分区表
t 更改分区类型
v 验证分区表
i 打印分区信息（注意：通常是 i）

+   Misc
m 打印此菜单
u 更改显示/输入单位
v 额外功能（专家专用）

+   [...]
保存并退出
w 将表写入磁盘并退出
q 不保存更改退出
...]

Command (m for help): q

如果有可用空空间，`fdisk` 通常会在第一个可用扇区或磁道处启动新分区。分区的实际大小取决于磁盘的几何结构。

## 使用 fdisk：创建分区

下面的屏幕输出示例显示了创建新 (`n`) 分区 (`p`)、将其设置为可启动 (`a`)，最后将分区信息写入 (`w`) 磁盘的步骤。（请注意，你可能指定 500MiB 的分区，但磁盘的几何结构可能不允许该精确的大小。）

```
# fdisk /dev/sdb
```
