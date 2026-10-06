
```
# mdconfig -a swap -s 5m -u 1
```

```
# newfs -U md 1
```

`/dev/md1`: 5.0MB (10240 sectors) block size 16384, fragment size 2048 using 4 cylinder groups of 1.27MB, 81 blks, 192 inodes. with soft updates super-block backups (for `fsck -b #`): 160, 2752, 5344, 7936

```
# mount /dev/md 1 /mnt
```

```
# df /mnt
```

| Filesystem | 1K-blocks | Used | Avail | Capacity | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/md1` | 4718 | 4 | 4338 | 0% | `/mnt` |

要创建一个新的文件支持的内存磁盘，请分配一个磁盘区域使用。此示例创建了一个名为 `newimage` 的空 5MB 文件：

```
# dd if=/dev/zero of=newimage bs=1k count=5k
```

`5120+0 records in`

`5120+0 records out`

接下来，将该文件附加到内存磁盘，标记内存磁盘并使用 UFS 系统对其进行格式化，挂载内存磁盘，并验证文件支持磁盘的大小：

```
# mdconfig -f newimage -u 0
```

```
# bsdlabel -w md 0
```

```
# newfs -U md 0a
```

`/dev/md0a`: 5.0MB (10224 sectors) block size 16384, fragment size 2048 using 4 cylinder groups of 12.5MB, 80 blks, 192 inodes. super-block backups (for `fsck -b #`) at: 160, 2720, 5280, 7840

```
# mount /dev/md 0a /mnt
```

```
# df /mnt
```

| Filesystem | 1K-blocks | Used | Avail | Capacity | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/md0a` | 4710 | 4 | 4330 | 0% | `/mnt` |

使用 `mdconfig` 创建文件或内存支持的系统需要多个命令。FreeBSD 还带有 `mdmfs`，它可以自动配置内存磁盘、使用 UFS 系统对其进行格式化并挂载。例如，在用 `dd` 创建 `newimage` 之后，这一个命令等同于运行上面 `bsdlabel`、`newfs` 和 `mount` 命令：

```
# mdmfs -F newimage -s 5m md 0 /mnt
```

若要用 `mdmfs` 创建新的基于内存的内存磁盘，请使用这一个命令：

```
# mdmfs -s 5m md 1 /mnt
```

如果未指定单元号，`mdmfs` 将自动选择一个未使用的内存设备。有关关于 `mdmfs` 的更多信息，请参考 `mdmfs(8)`。

## 18.10. 文件系统快照

由 Tom Rhodes 贡献。

FreeBSD 提供了一个与软更新（Soft Updates）结合使用的功能：文件系统快照。

UFS 快照允许用户创建指定文件系统的映像，并将其视为文件处理。快照文件必须在执行操作的文件系统中创建，且用户每个文件系统创建的快照不能超过 20 个。

激活的快照记录在超级块中，因此它们在卸载、重新挂载以及系统重启后仍然是持久的。当快照不再需要时，可以使用 `rm(1)` 将其移除。虽然可以按任何顺序删除快照，但可能无法获得所有使用的空间，因为另一个快照可能会占用某些已释放的块。

不可更改的快照在初始创建快照后由 `mksnap_fs(8)` 设置，`unlink(1)` 对快照是一个例外，因为它允许删除它们。

快照是使用 `mount(8)` 创建。要在 `/var/snapshot/snap` 中放置 `/var` 的快照，请使用以下命令：

```
# mount -u -o snapshot /var/snapshot/snap/var
```

或者，使用 `mksnap_fs(8)` 创建快照：

```
# mksnap_fs /var /var/snapshot/snap
```

可以使用 `find(1)` 在系统（如 `/var`）上查找快照：

```
# find /var -flags snapshot
```

### 磁盘配额（Disk Quotas）

一旦创建了快照，它就有好几个用处：

- 某些管理员将使用快照进行备份，因为快照可以传输到 CD 或磁带上。虽然快照可以被删除，但所有使用的空间可能无法获取，因为另一个快照可能会占用某些已释放的块。

## edquota -u test

用户 `test` 的配额：

`/usr`: 已用 kbytes: 65, 限制 (soft = 50, hard = 75)

已用 inodes: 7, 限制 (soft = 50, hard = 60)

/usr/var: 已用 kbytes: 0, 限制 (soft = 50, hard = 75)

已用 inodes: 0, 限制 (soft = 50, hard = 60)

对于每个启用了配额的系统，通常会有行。一行代表块限制，另一行代表 inode 限制。更改值即可修改配额限制。例如，要将 `/usr` 的块限制提高到软限制 500 和硬限制 600，请按如下方式修改该行的值：

`/usr`: 已用 kbytes: 65, 限制 (soft = 500, hard = 600)

新的配额限制在退出编辑器后生效。

## 检查配额限制和磁盘使用情况

有时希望对一组用户设置配额限制。这可以通过为用户分配所需的配额限制来实现。然后，使用 `-p` 将该配额复制到指定的用户 ID (UIDs) 范围。以下命令将为 UID 10,000 到 19,999 复制这些配额限制：

```
# edquota -p test 10000-19999
```

更多信息请参阅 `edquota(8)`。

## 18.11.3. 检查配额限制和磁盘使用情况

要检查个人或组组配额以及磁盘使用情况，请使用 `quota(1)`。用户只能检查自己的配额以及其所属组的配额。只有超级用户可以查看所有用户和组配额。要获取启用配额的系统的所有配额和磁盘使用情况摘要，请使用 `repquota(8)`。

通常情况下，用户没有使用任何磁盘空间的系统不会显示在 `quota` 的输出中，即使该用户为该系统分配了配额限制。使用 `-v` 显示这些系统。以下是一个在两个系统上有配额限制的用户的 `quota -v` 示例输出。

用户 `test` 的磁盘配额 (uid 1002):

| 文件系统 | 使用量 | 限制 | 宽限期 | 文件 | 配额 | 宽限期 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `/usr` | 65* | 50 | 75 | 5days | 7 | 50 | 60 |
| `/usr/var` | 0 | 50 | 75 | 0 | 50 | 60 |

在此示例中，用户目前超过 `/usr` 的 50 kbytes 软限制 15 kbytes，剩余 5 天宽限期。星号 `*` 表示用户当前超过了配额限制。

## 18.11.4. NFS 上的配额

配额由 NFS 服务器上的配额子系统执行。

`rpc.rqquotad(8)` 守护进程为 NFS 客户端上的配额提供信息，允许这些机器上的所有者用户查看其配额统计数据。

在 NFS 服务器上，通过删除 `/etc/inetd.conf` 中该行前面的 `#` 号来启用 `rpc.rqquotad`：

```
rqquotad/1 dgram udp wait root /usr/libexec/rpc.rqquotad rpc.rqquotad
```

然后，重启 `inetd`：

```
# service inetd restart
```

## 18.12. 加密磁盘分区

由 Lucky Green 贡献。

FreeBSD 提供了极佳的防止未经授权数据访问的在线保护。文件权限和强制性访问控制 (MAC) 有助于在操作系统运行且计算机通电时，防止未经授权的用户访问数据。然而，如果攻击者拥有计算机的物理访问权限，并可以将计算机的硬盘移动到另一个系统来复制和分析数据，那么操作系统强制的权限将毫无意义。

无论攻击者如何获得硬盘或关机状态的计算机，FreeBSD 内置的基于 GEOM 的加密子系统都能保护计算机系统中的数据，免受拥有大量资源的动力极强的攻击者的侵害。与加密单个文件的加密方法不同，内置的 `gbde` 和 `geli` 工具可用于透明地加密整个系统。明文从未接触硬盘盘片。

本章演示了如何在 FreeBSD 上创建加密系统。它首先演示了使用 `gbde` 的过程，然后使用 `geli` 演示了相同的示例。

## 18.12.1. 使用 gbde 进行磁盘加密

`gbde(4)` 功能的目标是为攻击者访问冷存储设备的内容提供严峻的挑战。然而，如果计算机在运行且存储设备处于连接状态时被攻破，且攻击者获得了有效密码，那么它对存储设备的内容无法提供任何保护。因此，在系统运行时提供物理安全并保护加密机制使用的密码至关重要。

该功能提供了若干屏障来保护存储在每个磁盘扇区中的数据。它使用 CBC 模式下的 128 位 AES 对磁盘扇区的内容进行加密。FreeBSD 为 `gbde` 提供了一个内核模块，可以通过以下命令加载它：

```
# kldload geom_bde
```

以下示例演示了如何按照 18.2 “添加磁盘”节所述向系统添加新硬盘。
