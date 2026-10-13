
`dd if=/dev/zero of=/swapfile count=1024 count=1`

设置权限：

```bash
chmod 600 /swapfile
```

将其格式化为 swap：

```bash
mkswap /swapfile
```

启用该文件：

```bash
swapon /swapfile
```

为了让系统在重启后自动挂载该文件，需要在 `/etc/fstab` 中添加以下内容：

```
/swapfile swap swap defaults 0 0
```

## 检查 Swap 使用情况

使用以下命令查看正在使用的 swap：

```bash
swapon --show
```

## 第 14 章：管理分区

### 列表 14.3 使用 `blkid` 查找当前文件系统的 UUID

```bash
[root@server3 ~]# blkid
/dev/vda1: UUID="02305166-4f74-840d-a868-c549b3229e65" TYPE="xfs"
/dev/vda2: UUID="H55zq-n2F3-L2fm-xUWZs-3VEq-QVCAI" TYPE="LVM2 member"
/dev/vda5: UUID="42f419c4-633f-4ed7-b161-59a4dadd3da" TYPE="xfs"
/dev/mapper/centos-swap: UUID="5867ba02-fd889-475c-75be-560-7922febde43" TYPE="swap"
/dev/mapper/centos-root: UUID="b2022ac44-73c6-4e6-a52f-703e3e246b7" TYPE="xfs"
```

在引入 UUID 之前，文件系统通常配置为通过标签（labels）工作，可以使用 `eLabel` 或 `xfs_admin -L` 命令设置标签。这在最近的 Linux 版本中已经变得不常见了。如果文件系统有标签，`blkid` 命令也会显示它。

要使用 UUID 挂载文件系统，你需要使用 `UUID=nnnnnn` 而不是设备名。因此，如果你想根据列表 14.3 中的 UUID 挂载 `/dev/vda5`，命令如下：

```bash
mount UUID="42f419c4-633f-4ed7-b161-59a4dadd3da" /mnt
```

使用 UUID 手动挂载设备并不一定更方便。然而，如果像下一节所说的那进行自动挂载，那么使用 UUID 而不是设备名是有意义的。

要使用标签挂载文件系统，你使用 `mount LABEL=labelname` 命令。例如，使用 `mount LABEL=mylabel /mnt` 将命名为 label 的文件系统临时挂载到 `/mnt` 目录。

通常，你并不希望手动挂载文件系统。一旦你对它们满意，让它们自动挂载是一个好主意。实现此点的经典方法是通过 `/etc/fstab` 文件。列表 14.4 显示了该文件的内容。

### 列表 14.4 示例 `/etc/fstab` 内容

```bash
# root@server3 -]# cat /etc/fstab
# /etc/fstab
# Created by anaconda on Fri Jan 16 10:28:41 2015
# Accessible filesystems, by reference, are maintained under '/dev/disk'
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
#
/dev/mapper/centos-root / xfs defaults 1 1
UUID=02305166-840d-4f74 / xfs defaults 1 2
/dev/mapper/centos-swap defaults 0 0
```

在 `/etc/fstab` 中，所有内容都指定自动挂载文件系统。为此，每行有六个字段，如表 14.5 所示。

| 字段 | 描述 |
|---|---|
| Device (设备) | 必须挂载的设备。可以使用设备名、UUID 或标签。 |
| Mount Point (挂载点) | 设备挂所需的目录或内核接口。 |
| File System (文件系统) | 文件系统类型。 |
| Mount Options (挂载选项) | 挂载选项。 |
| Dump Support (备份支持) | 使用 1 启用 dump 工具。对于某些备份方案可能是必要的。 |
| Automatic Check (自动检查) | 指定启动时是否应检查文件系统。使用 0 禁用检查，如果是根系统则使用 1，所有其他需要自动检查的文件系统使用 2。网络系统应将此选项设置为 0。 |

根据之前讨论过的 `mount` 命令，理解 `/etc/fstab` 中的设备、挂载点和文件系统字段应该没有问题。注意，并不是所有的挂载点都以 `/` 开头；某些系统设备（如 swap）并不挂载在目录上，而是挂载在内核接口。`Mount Options` 字段定义了可以使用的挂载选项。如果需要特定选项，此行将只写“defaults”。表 14.6 提供了常用挂载选项的概述。

### 表 14.6 常用挂载选项

| 选项 | 使用 |
| --- | --- |
| auto/noauto | 文件系统将[自动]挂载。 |
| acl | 添加文件系统访问控制列表支持（见第 7 章“配置权限”）。 |
| user_xattr | 添加用户扩展支持。 |
| atime/noatime | 禁用或启用访问时间。 |
| noexec/exec | 禁止或允许执行程序。 |
| _netdev | 等待网络可用。 |

`/etc/fstab` 的第五列指定了对 `dump` 工具的支持。最后一列指示启动时是否应检查文件系统。使用 0 禁用检查，如果是根系统则使用 1，所有需要自动检查的文件系统使用 2。网络系统应将此选项设置为 0。

警告：如果你在 `/etc/fstab` 中犯错，可能会导致系统无法正常启动。

### 练习 14.6 通过 fstab 挂载分区

在此练习中，你将学习如何挂载分区。

- 1. 从 shell 输入 `[root@server3 ~]# blkid`。
- 2. 使用 `mkdir /mnt/data` 创建挂载点。
- 3. 用编辑器打开 `/etc/fstab` 并添加行：

```
UUID=42f419c4-633f-4ed7-b161-59a4dadd3da /mnt/data xfs defaults 0 0
```
