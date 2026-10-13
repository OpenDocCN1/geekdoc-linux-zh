
`mount` 命令的输出显示了你挂载的磁盘和 NFS 文件系统。第一行输出显示你的硬盘（`/dev/sda1`）挂载在根文件系统（`/`）上，具有读写权限（`rw`），文件系统类型为 `ext2`（标准 Linux 文件类型）。`/proc`、`/dev/pts` 和 `usbdevfs` 代表文件系统类型。刚刚挂载的 NFS 文件系统是 `maple` 的 `/tmp` 目录（`maple:/tmp`）。它挂载在 `/mnt/maple` 上，挂载类型为 `nfs`。文件系统是可读写的（`rw`），`maple` 的 IP 地址为 `10.0.0.11`（`addr=10.0.0.11`）。

www.unlinux.com 额外内容

我刚才展示的是使用 `mount` 操作 NFS 的简单用例。挂载是临时的，当你重启计算机时不会重新挂载。你也可以为 NFS 挂载的 `mount` 命令行添加选项：

- `-a`：挂载 `/etc/fstab` 中的所有文件系统（被标记为 `noauto` 的除外）。
- `-f`：在命令行（或 `/etc/fstab` 中）对文件系统执行模拟（伪）操作。配合 `-v` 选项使用时，`-f` 有助于在实际执行之前查看 `mount` 将执行的操作。
- `-r`：以读/写模式挂载文件系统。（要使此项生效，共享文件系统必须已以读写权限导出。）

下一节将描述如何使挂载更持久化（使用 `/etc/fstab` 文件）以及如何为 NFS 挂载选择各种选项。

## 自动挂载 NFS 文件系统 (/etc/fstab 文件)

为了设置在每次启动 Linux 系统时都自动挂载 NFS 文件系统，你需要在 `/etc/fstab` 文件中添加 NFS 文件系统的条目。`/etc/fstab` 文件包含了关于你的 Linux 系统各种可挂载文件系统的信息。

向本地系统添加 NFS 文件系统的格式如下：

```
host:directory mountpoint nfs 0 0
```

第一项（`host:directory`）识别 NFS 服务器和共享目录。`Mountpoint` 是挂载 NFS 目录的本地挂载点，后面是文件系统类型（`nfs`）。与挂载相关的任何选项出现在逗号分隔的列表中。最后两个零告诉 Linux 不要转储文件系统内容也不要执行 `fsck`（针对文件系统）。

以下是 `/etc/fstab` 中的两个 NFS 示例：

```
maple:/tmp /mnt/maple rsize=8192,wsize=8192 0 0
ok:/apps /oak/apps nfs noauto,ro 0
```

在第一个示例中，来自 `maple` 计算机的 `/tmp` 目录（`maple:/tmp`）挂载在本地目录 `/mnt/maple` 上。文件系统类型为 `nfs`，读写缓冲区设置为 `8192` 以加速关联连接的数据传输。在第二个示例中，来自 `maple` 计算机的 `/tmp` 目录（`maple:/tmp`）挂载在本地目录 `/mnt/maple` 上。文件系统类型为 `nfs`，读写缓冲区设置为 `8192` 以加速关联连接的数据传输。

## 第 18 章：设置文件服务器

`mount` 命令可以自动挂载添加到 `/etc/fstab` 文件的 NFS 目录，就像挂载本地磁盘一样。NFS 目录也可以添加到 `/etc/fstab` 文件中，但设置为不自动挂载。通过 `noatime` 选项，`etc/fstab` 中列出的 NFS 目录在系统启动后处于非活动状态，直到使用 `mount` 命令对系统进行挂载。

## 手动挂载 NFS 文件系统

如果你知道网络上某台计算机的目录已经导出（即可以挂载），你可以使用 `mount` 命令手动挂载该目录。这是在将其设置为永久挂载之前，确保其可用且运行良好的好方法。以下是从名为 `maple` 的计算机将 `/tmp` 目录挂载到本地计算机的示例：

```
# mkdir /mnt/maple
# mount maple:/mnt/maple
```

第一个命令（`mkdir`）创建了挂载点目录（`/mnt`），这是存放临时挂载磁盘和 NFS 文件系统的常用位置。然后，`mount` 命令通过冒号分隔识别远程计算机和共享文件系统（`maple:/tmp`）。接着是本地挂载点目录（`/mnt/maple`）。

如果挂载失败，请确保服务器上的 NFS 服务正在运行，并且你的防火墙规则没有阻止对该服务的访问。在服务器上，输入 `ps aux` 应该能看到 `nfs` 进程列表。如果没有，尝试通过 `/etc/init.d/nfs start` 来启动 `nfs` 守护进程。如果成功，你可以使用 SYSV 级别管理器（`tksysv` 命令）永久设置 NFS。要查看你的防火墙规则，输入 `ipchains -L`（请参第 14 章关于防火墙的描述）。

为了确保挂载已发生，输入 `mount`。此命令列出所有已挂载的磁盘和 NFS 文件系统。以下是 `mount` 命令及其输出的示例：

```
/dev/sda1 on / type ext2 (rw)
none on /proc type proc (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
usdevfs on /proc/bus/usb type usbdevfs
maple:/mnt/maple nfs (rw,addr=10.0.0.11).
```

`mount` 命令的输出显示了你挂载的磁盘和 NFS 文件系统。第一行输出显示你的硬盘（`/dev/sda1`）挂载在根文件系统（`/`）上，具有读写权限（`rw`），文件系统类型为 `ext2`（标准 Linux 文件类型）。`/proc`、`/dev/pts` 和 `usbdevfs` 代表文件系统类型。刚刚挂载的 NFS 文件系统是 `maple` 的 `/tmp` 目录（`maple:/tmp`）。它挂载在 `/mnt/maple` 上，挂载类型为 `nfs`。文件系统是可读写的（`rw`），`maple` 的 IP 地址为 `10.0.0.11`（`addr=10.0.0.11`）。

www.unlinux.com 额外内容
