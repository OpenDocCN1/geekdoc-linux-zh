
- `nfs` — 这是网络文件系统 (NFS) 类型的文件系统。从网络上另一台计算机挂载的文件系统使用这种类型的文件系统。

交叉引用：有关使用 NFS 在网络上导出和共享文件系统的信息见第 18 章。

- `hpfs` — 该文件系统用于只读挂载 OS/2 HPFS 文件系统。

- `ncpfs` — 这与 Novell Net 文件系统有关。NetWare 文件系统可以通过网络挂载。

- `ntfs` — Fedora 7 在 Fedora 存储库中添加了 NTFS 支持。许多设置双启动电脑的用户能够访问 Windows (`ntfs`) 驱动器。要为 Fedora 添加 NTFS 文件系统支持，你需要安装 `nfs-3g` 包。

- `affs` — 该文件系统由 Amiga 使用。

- `reiserfs` — 这是一个日志文件系统，曾是其他 Linux 发行版的默认文件系统（包括 SUSE、Slackware 和 Linspire）。Reiserfs 在 Red Hat 系统中被认为支持良好（在安装 Fedora 时必须在启动提示符添加 reiser 以启用 reiserfs 分区。此外，SELinux 不支持 reiserfs 文件系统）。

- `ufs` — 该文件系统在 Sun Microsystems 操作系统（即 Solaris 和 SunOS）上很流行。

## 第 10 章：理解系统管理

- `xenix` — 添加它是为了兼容 Xenix 文件系统（UNIX 最早的 PC 系统之一）。该系统已过时，最终可能会被移除。

- `xfs` — 这是一个日志文件系统，在高性能环境中非常有用。xfs 文件系统包含完整的 64 位寻址。它可以扩展到包含多个 TB 数据且每秒传输数据达到数 GB 级的系统。

- `jfs` — 该文件系统基于 IBM 用于 OS/2 Warp 的 JFS 文件系统。它在 2000 年成为一个开源项目。JFS 最适合企业级系统。与 XFS 一样，JFS 针对大型文件系统和高性能环境进行了优化。

- `squashfs` — 这是一个压缩文件系统，文件在被请求时会实时解压缩。它通常与 Live CD 使用，包括所有 Fedora Live CDs。

- `fuse` — Fuse 的行为类似于一个用户空间的远程文件系统。本地用户可以使用 ssh 工具将远程文件系统挂载到本地，完全基于用户登录的权限来使该远程文件系统可用。这是一种在无需远程端进行管理员干预的情况下挂载远程文件系统的非常酷炫的方法。

Fedora 添加了两种新的文件系统类型：`ext4` 文件系统和加密文件系统。两者目前仍被视为实验性，Fedora 9 中提供了可用工具来创建和使用这些新的文件系统类型。

`ext4` 文件系统是 ext 文件系统的最新版本（`ext3` 是当前标准）。`ext4` 文件系统可以作为 `ext3` 文件系统进行挂载。如果你想使用新的 `ext4` 特性（称为 extents），请将其挂载为 `ext4` 设备（`-t ext4dev`）。有关创建和操作 `ext4` 文件系统的信息，请参考 Ext4 FAQ：

```
http://ext4.wiki.kernel.org/index.php/Frequently_Asked_Questions
```

如果你的电脑丢失或被盗，可以使用加密文件系统来保护你的数据。偷你笔记本电脑的人如果没有你的密码，将无法挂载或访问加密文件系统上的数据。`cryptsetup-linux` 包中的 `cryptsetup` 命令用于创建加密卷。在 Fedora 中，根目录 (`/`) 之外的任何文件系统都可以加密。要了解更多信息，请参阅加密文件系统页面：

```
http://fedoraproject.org/wiki/Releases/FeatureEncryptedFilesystems
```

## 使用 fstab 定义可挂载的文件系统

你本地计算机上的磁盘以及你每天使用的远程文件系统可能被设置为在启动 Linux 时自动挂载。定义哪些文件系统被挂载包含在 `/etc/fstab` 文件中。这是一个 `/etc/fstab` 示例：

| 设备 | 挂载点 | 类型 | 选项 | 倾储 | 检查 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/VolGroup0/100` | `/` | `ext3` | `defaults` | 1 | 1 |
| `/dev/boot` | `/boot` | `ext3` | `defaults` | 1 | 2 |
| `/dev/devpts` | `/dev/pts` | `devpts` | `dev=5,mode=620` | 0 | 0 |
| `/dev/shm` | `/dev/shm` | `tmpfs` | `defaults` | 0 | 0 |
| `/dev/proc` | `/proc` | `proc` | `defaults` | 0 | 0 |
| `/dev/sys` | `/sys` | `sysfs` | `defaults` | 0 | 0 |
| `/dev/VolGroup0/swap` | `swap` | `swap` | `defaults` | 0 | 0 |
| `/dev/sda1` | `/mnt/win` | `vfat` | `noauto` | 0 |  |

你你本地计算机上的磁盘以及你每天使用的远程文件系统可能被设置为在启动 Linux 时自动挂载。定义哪些文件系统被挂载包含在 `/etc/fstab` 文件中。这是一个 `/etc/fstab` 示例：

| 设备 | 挂载点 | 类型 | 选项 | 倾储 | 检查 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/VolGroup0/100` | `/` | `ext3` | `defaults` | 1 | 1 |
| `/dev/boot` | `/boot` | `ext3` | `defaults` | 1 | 2 |
| `/dev/devpts` | `/dev/pts` | `devpts` | `dev=5,mode=620` | 0 | 0 |
| `/dev/shm` | `/dev/shm` | `tmpfs` | `defaults` | 0 | 0 |
| `/dev/proc` | `/proc` | `proc` | `defaults` | 0 | 0 |
| `/dev/sys` | `/sys` | `sysfs` | `defaults` | 0 | 0 |
| `/dev/VolGroup0/swap` | `swap` | `swap` | `defaults` | 0 | 0 |
| `/dev/sda1` | `/mnt/win` | `vfat` | `noauto` | 0 |  |

你本地计算机上的磁盘以及你每天使用的远程文件系统可能被设置为在启动 Linux 时自动挂载。定义哪些文件系统被挂载包含在 `/etc/fstab` 文件中。这是一个 `/etc/fstab` 示例：

| 设备 | 挂载点 | 类型 | 选项 | 倾储 | 检查 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/VolGroup0/100` | `/` | `ext3` | `defaults` | 1 | 1 |
| `/dev/boot` | `/boot` | `ext3` | `defaults` | 1 | 2 |
| `/dev/devpts` | `/dev/pts` | `devpts` | `dev=5,mode=620` | 0 | 0 |
| `/dev/shm` | `/dev/shm` | `tmpfs` | `defaults` | 0 | 0 |
| `/dev/proc` | `/proc` | `proc` | `defaults` | 0 | 0 |
| `/dev/sys` | `/sys` | `sysfs` | `defaults` | 0 | 0 |
| `/dev/VolGroup0/swap` | `swap` | `swap` | `defaults` | 0 | 0 |
| `/dev/sda1` | `/mnt/win` | `vfat` | `noauto` | 0 |  |

你本地计算机上的磁盘以及你每天使用的远程文件系统可能被设置为在启动 Linux 时自动挂载。定义哪些文件系统被挂载包含在 `/etc/fstab` 文件中。这是一个 `/etc/fstab` 示例：

| 设备 | 挂载点 | 类型 | 选项 | 倾储 | 检查 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/VolGroup0/100` | `/` | `ext3` | `defaults` | 1 | 1 |
| `/dev/boot` | `/boot` | `ext3` | `defaults` | 1 | 2 |
| `/dev/devpts` | `/dev/pts` | `devpts` | `dev=5,mode=620` | 0 | 0 |
| `/dev/shm` | `/dev/shm` | `tmpfs` | `defaults` | 0 | 0 |
| `/dev/proc` | `/proc` | `proc` | `defaults` | 0 | 0 |
