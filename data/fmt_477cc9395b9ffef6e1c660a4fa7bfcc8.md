
`noauto` 选项导致 Linux 不自动挂载文件系统。`nosuid` 选项强制已挂载的 setuid 可执行文件在本地系统（挂载该文件系统的系统）上以常规权限运行（无有效用户 ID 更改）。

### 使用 nosuid 选项挂载可移动设备

- **安全性**

    - 始终使用 `nosuid` 选项挂载可移动设备，这样恶意用户就不会例如在磁盘上放置 setuid 版本的 bash 并获取 root shell。

除非指定 `user`、`users` 或 `owner` 选项，否则只有超级用户可以挂载和卸载文件系统。`user` 选项意味着任何用户都可以挂载文件系统，但只能由挂载该文件系统的同一用户卸载；`users` 意味着任何用户都可以挂载和卸载文件系统。这些选项通常用于 CD 和软驱。`owner` 选项仅在特殊情况下使用，类似于 `user` 选项，除了挂载设备的用户必须拥有该设备。

## 挂载 Linux 软盘

挂载 Linux 软盘类似于挂载硬盘分区。对于位于第一个软驱中的软盘，请在 `/etc/fstab` 中创建一个类似于下面条目的项：

```
/dev/fd0    /mnt/floppy    auto    noauto,users    0    0
```

指定文件系统类型为 `auto` 会导致系统探测文件系统以确定其类型，并允许用户挂载各种软盘。如有必要，请创建 `/mnt/floppy` 目录。插入软盘并尝试挂载它。软盘必须已格式化（使用 `fdformat`）。在下面的示例中，第一个命令后的错误信息通常表示软盘上没有文件系统。使用 `mkfs`（第 439 页）创建文件系统——但要小心，因为 `mkfs` 会销毁软盘上的所有数据：

```
# mount /dev/fd0
mount: you must specify the filesystem type
```

```
# mkfs /dev/fd0
mke2fs 1.41.9 (22-Aug-2009)
Filesystem label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
184 inodes, 1440 blocks
72 blocks (5.00%) reserved for the super user
First data block=1
Maximum filesystem blocks=1572864
1 block group
8192 blocks per group, 8192 fragments per group
184 inodes per group

Writing inode tables: done
Writing superblocks and filesystem accounting information: done
```

该文件系统将每 24 次挂载或 180 天自动检查一次，以先到者为准。使用 `tune2fs -C` 或 `-i` 进行覆盖。

再次尝试挂载命令：

```
# mount /dev/fd0
## mount
…
/dev/fd0 on /mnt/floppy type ext2 (rw,noexec,nosuid,nodev)

# df -h /dev/fd0
Filesystem    Size  Used Avail Use% Mounted on
/dev/fd0      1.4M  19K  1.3M  2% /mnt/floppy
```

不带任何参数的 `mount` 命令和 `df -h /dev/fd0` 显示软盘已挂载并准备就绪，可供使用。

## umount：卸载文件系统

`umount` 实用工具可以卸载文件系统，只要该文件系统不包含正在使用（打开）的文件或目录。例如，已登录用户的工作目录不能位于你希望卸载的文件系统上。下一条命令将卸载之前挂载的 CD：

```
$ umount /mnt/cdrom
```

卸载软盘或远程目录层次结构的方式与你卸载硬盘分区的方式相同。

`umount` 实用工具查询 `/etc/fstab` 以获取必要信息，然后从服务器卸载相应的文件系统。当某个进程在你试图卸载的文件系统上有打开的文件时，`umount` 会显示类似以下信息的消息：

```
umount: /home: device is busy
```

**当无法卸载设备因为其正在被使用时**

当某个进程在你需要卸载的设备上有打开的文件时，使用 `fuser` 来确定哪个进程打开了该文件并终止它。例如，当你想要卸载软盘时，输入命令 `fuser -ki /mnt/floppy`（在本地系统中将 `/mnt/floppy` 替换为软盘的挂载点）。经过确认后，该命令将终止使用软盘的进程。

使用 `umount` 的 `-a` 选项来卸载除挂载在 `/` 上的文件系统之外的所有文件系统（`/` 永远无法被卸载）。你可以将 `-a` 与 `-t` 选项结合使用，以卸载给定类型（ext3、nfs 或其他）的文件系统。例如，以下命令卸载所有已挂载且未被使用的 nfs 目录层次结构：

```
# umount -at nfs
```

## fstab：记录文件系统

系统管理员维护 `/etc/fstab` 文件，该文件列出了本地和远程目录层次结构，其中大部分在系统启动时会自动挂载。`fstab` 文件有六列，其中连字符表示没有值的列的占位符：

- 1. **名称**—本地块设备（第 484 页）的名称、标签或 UUID 号，或指向远程目录层次结构的指针。安装系统时，Fedora/RHEL 使用 UUID 号来指代固定设备。它会在 `fstab` 中指定 UUID 的每一行前加上一行注释，以说明设备名称。在安装期间在 `fstab` 中使用 UUID 号避免了需要对设备命名保持一致性的需求。由于 `udev`（第 482 页）动态管理设备命名，安装程序可能不知道第一个磁盘并非命名为 `/dev/hda1` 而是 `/dev/sda1`，但它总是知道设备的 UUID 号。使用 UUID 号来标识设备还能确保在移除或交换设备时，分区和挂载点正确关联。有关 UUID 号的更多信息，参见 `/dev/disk/by-uuid`（第 469 页）。你可以使用形式为 `LABEL=xx` 的卷标签来使用本地文件系统的卷标签，其中 `xx` 是卷标签。参见第 439 页的 `e2label`。

  远程目录层次结构显示为 *hostname*: *pathname*，其中 *hostname* 是托管该文件系统的远程系统的名称，*pathname* 是要挂载的目录在远程系统上的绝对路径名。

- 2. **挂载点**—文件系统/目录层次结构要挂载到的目录文件的名称。如果该目录尚不存在，请使用 `mkdir` 创建该目录。参见第 32 页和第 487 页。

- 3. **类型**—要挂载的文件系统/目录层次结构的类型。本地文件系统通常为 `ext2`、`ext3` 或 `iso9660` 类型，远程目录层次结构为 `nfs` 或 `cifs` 类型。第 485 页的表 12-1 列出了文件系统类型。

- 4. **挂载选项**—挂载选项的逗号分隔列表，例如文件系统是挂载为读写（`rw`，默认值）还是只读（`ro`）。参见第 488 页和第 732 页，并参考 `mount` 和 `nfs` 的手册页以获取选项列表。

- 5. **Dump**—由 `dump`（第 563 页）用于确定何时备份文件系统。

- 6. **Fsck**—指定 `fsck` 检查文件系统的顺序。根（`/`）在此列中应为 1。挂载到根目录正下方目录的文件系统应为 2。挂载在另一个已挂载文件系统（非根）上的文件系统应为 3。例如，如果 `local` 是一个独立于 `/usr` 的文件系统，并且挂载在 `/usr` 上（作为 `/usr/local`），那么 `local` 应为 3。不需要检查的文件系统和目录层次结构（例如远程挂载的目录层次结构和 CD/DVD）应为 0。

以下示例展示了一个典型的 `fstab` 文件：

```
$ cat /etc/fstab
LABEL=/1 / ext3 defaults 1 1
LABEL=/boot1 /boot ext3 defaults 1 2
devpts /dev/pts devpts gid=5,mode=620 0 0
tmpfs /dev/shm tmpfs defaults 0 0
LABEL=/home1 /home ext3 defaults 1 2
proc /proc proc defaults 0 0
sysfs /sys sysfs defaults 0 0
LABEL=SWAP-hda5 swap swap defaults 0 0
/dev/hda3 /oldhome ext3 defaults 0 0
tuna:/p04 nfs defaults 0 0
/dev/fd0 /mnt/floppy auto noauto, users 0 0
```

## fsck：检查文件系统完整性

`fsck`（fileSystem check）实用工具验证文件系统的完整性，并在可能的情况下修复发现的任何问题。由于许多文件系统修复可能会破坏数据，特别是在*非日志记录*文件系统（第 1089 页）如 `ext2` 上，因此默认情况下，`fsck` 在执行每个修复之前会要求你确认。
