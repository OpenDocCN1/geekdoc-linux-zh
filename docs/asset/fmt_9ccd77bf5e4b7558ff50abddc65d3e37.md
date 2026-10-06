
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| backup | 960M | 77K | 896M | - | 0% | 6% | 1.00x | ONLINE | - |

| mypool | 984M | 43.7M | 940M | - | - | 0% | 4% | 1.00x | ONLINE | - |

名为 `mypool` 的池是定期写入和读取的主池。主池不可用，第二个池 `backup` 作为备用。请注意，这种故障转移不是 ZFS 自动完成的，而是在需要由系统管理员手动完成。快照用于提供要复制的系统版本。一旦创建了 `mypool` 的快照，就可以将其复制到 `backup` 池。包含自上次快照以来的所有更改。

```bash
# zfs snapshot mypool @backup1
```

| NAME | USED | AVAIL | MOUNTPOINT |

| :--- | :--- | :--- | :--- |

| mypool@backup1 | 0 | 43.6M | - |

现在有了快照，`zfs send` 可以创建一个表示快照内容的流。该流可以写入标准输出，但必须重定向到文件或管道。为了备份数据集，请确保池有足够的空间来容纳发送的快照大小。

```bash
# zfs send mypool @backup1 >/backup/backup1
```

| NAME | SIZE | ALLOC | FREE | CKPOINT | EXPANSZ | FRAG | CAP | DEDUP | HEALTH | ALTROOT |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| backup | 960M | 63.7M | 896M | - | 0% | 6% | 1.00x | ONLINE | - |

| mypool | 984M | 43.7M | 940M | - | - | 0% | 4% | 1.00x | ONLINE | - |

`zfs send` 传输了名为 `backup` 的快照中的所有数据。创建和发送快照可以使用 cron 任务完成。与其将备份存储为存档，ZFS 可以将其接收为活动系统。下面的示例使用管道结合 `zfs send` 和 `zfs receive` 将数据从一个池复制到另一个池。传输完成后可以直接在接收池上使用这些数据。数据集只能复制到空数据集。

```bash
# zfs snapshot mypool @replica1
# zfs send -v mypool @replica1 | zfs receive backup/mypool
```

| NAME | SIZE | ALLOC | FREE | CKPOINT | EXPANSZ | FRAG | CAP | DEDUP | HEALTH | ALTROOT |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| backup | 960M | 63.7M | 896M | - | 0% | 6% | 1.00x | ONLINE | - |

| mypool | 984M | 43.7M | 940M | - | - | 0% | 4% | 1.00x | ONLINE | - |

## 20.4.7.1. 增量备份

`zfs send` 还可以确定两个快照之间的差异并仅发送它们之间的差异。这节省了磁盘空间和传输时间。例如：

```bash
# zfs snapshot mypool @replica2

# zfs list -t snapshot
```

| NAME | USED | AVAIL | MOUNTPOINT |

| :--- | :--- | :--- | :--- |

| mypool@replica1 | 5.72M | 43.6M | - |

| mypool@replica2 | 0 | 44.1M | - |

| NAME | SIZE | ALLOC | FREE | CKPOINT | EXPANSZ | FRAG | CAP | DEDUP | HEALTH | ALTROOT |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| backup | 960M | 61.7M | 896M | - | 0% | 6% | 1.00x | ONLINE | - |

| mypool | 960M | 50.2M | 910M | - | - | 0% | 5% | 1.00x | ONLINE | - |

创建了第二个快照 `replica2`。第二个快照仅包含了文件系统现在与之前的快照 `replica1` 之间的更改。使用 `zfs send -i` 并指定快照对可以生成一个仅包含更改数据的增量复制流。只有当初始快照在接收端已存在时，此操作才能成功。

```
# zfs send -v -i mypool @ replica1 mypool @ replica2 | zfs receive
/backup/mypool
```

从 @replica1 发送到 mypool@replica2 的估计大小为 5.02M

总估计大小为 5.02M

已发送快照

```
# zpool list
```

| NAME SIZE ALLOC FREE CKPOINT EXPANDSZ FRAG CAP DEDUP HEALTH ALTROOT |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| backup | 960M | 80.8M | 879M | - | 0% | 8% | 1.00x | ONLINE | - |

| mypool | 960M | 50.2M | 910M | - | 0% | 5% | 1.00x | ONLINE | - |

```
# zfs list
```

| NAME USED AVAIL REFER MOUNTPOINT |

| :--- | :--- | :--- | :--- | :--- |

| backup | 55.4M | 240G | 152K | /backup |

| backup/mypool | 55.3M | 240G | 55.2M | /backup/mypool |

| mypool | 55.6M | 11.6G | 55.0M | /mypool |

```
# zfs list -t snapshot own
```

| NAME USED AVAIL REFER MOUNTPOINT |

| :--- | :--- | :--- | :--- | :--- |

| backup/mypool@replica1 | 104K | - | 50.2M | - |

| backup/mypool@replica2 | 0 | - | 55.2M | - |

| mypool@replica1 | 29.9K | - | 50.0M | - |

| mypool@replica2 | 0 | - | 55.0M | - |

增量流已成功并传输。只复制了发生的数据，而不是 replica1 的全部内容。只发送了差异部分，传输所需的时间少得多，并且通过不反复复制整个池节省了磁盘空间。这在必须依赖慢网络或必须考虑每次传输成本时非常有用。

一个新的文件系统 `backup/mypool` 可用了，它包含 `mypool` 池中的所有文件和数据。如果指定 `-P`，将复制数据集的属性，包括压缩设置、配额和挂载点。当指定 `-R` 时，将复制所指示数据集的所有子数据集及其所有属性。发送和接收可以自动化，以便在第二个池上创建定期备份。

## 第 20 章 ZFS 文件系统 (ZFS)

### 20.4.7.2. 通过 SSH 发送加密备份

在网络上通过数据流传输是保留远程备份的好方法，但它也有一个缺点。通过网络链路发送的数据未加密，允许任何人在发送用户不知情的情况下拦截并将这些流转换回数据。这是不尽人愿的，特别是当通过互联网将流发送到远程主机时。可以使用 SSH 安全地加密通过网络连接发送的数据。由于 ZFS 仅要求将流从标准输出重定向，因此通过 SSH 管道传输相对容易。为了保持系统内容在传输过程中和远程系统上的加密状态，请考虑使用 ZFS。

必须完成一些设置和安全预防。这里仅显示了 `zfs send` 操作所需的必要步骤。有关 SSH 的更多信息，请参见第 14.8 节，“OpenSSH”。

需要此配置：

- 使用 SSH 密钥实现发送和接收主机之间的无密码 SSH 访问

- 通常，发送和接收流需要 root 用户权限。这需要以 root 身份登录接收系统。然而，出于安全考虑，默认禁用 root 登录。可以使用 ZFS Delegation 系统允许每个系统上的非 root 用户执行相应的发送和接收操作。

- 在发送系统上：

```
# zfs allow -u someuser,snapshot mypool
```

- 要挂载池，无权限用户必须拥有该目录，并且允许普通用户挂载文件系统。在接收系统上：

```
# sysctl vfs.usermount=1
```

vfs.usermount: 0 -> 1

```
# echo vfs.usermount=1 >> /etc/sysctl.conf
```

```
# zfs create recvpool/backup
```

```
# zfs allow -u someuser,mount,receive recvpool/backup
```

```
# chown someuser /recvpool/backup
```

无权限用户现在能够接收并挂载数据集，并且 home 数据集可以复制到远程系统。

对于数据的其余部分，如果压缩率小于12.5%，块将以未压缩的形式写入，以避免浪费 CPU 周期尝试压缩已经压缩或不可压缩的数据。有关 ZFS 中提供的不同压缩算法的详细信息，请参见术语部分中的压缩（Compression）条目。

管理员可以使用多个数据集属性监控压缩的有效性。

```bash
# zfs get used,compressratio,compression,logicalused mypool/compressed_dataset
```

| NAME | PROPERTY | VALUE | SOURCE |

| :--- | :--- | :--- | :--- |

| mypool/compressed_dataset | used | 449G | - |

| mypool/compressed_dataset | compressratio | 1.11x | - |

| mypool/compressed_dataset | compression | lz4 | local |

| mypool/compressed_dataset | logicalused | 496G | - |

该数据集目前使用 449 GB 空间（`used` 属性）。如果没有压缩，将占用 496 GB 空间（`logicalused` 属性）。这导致了 1.11:1 的压缩率。

压缩在与用户配额（User Quotas）结合时可能会产生意外的副作用。用户配额限制了用户在数据集上可以消耗的空间，但测量基于压缩后使用的空间。因此，如果一个用户拥有 10 GB 的配额，并写入 10 GB 的可压缩数据，他们仍然能够存储额外数据。如果他们以后更新了一个文件（例如数据库），写入了更多或更少的可压缩数据，他们可用的空间将会发生变化。这可能会导致一种奇怪的情况：用户没有增加实际数据量（`logicalused` 属性），但压缩的变化导致他们达到了配额限制。

压缩与备份之间也可能产生类似的意外之外的相互作用。配额通常用于限制存储的数据量，以确保有足够的备份空间。然而，由于配额不考虑压缩，写入的数据量可能比未压缩备份更多。

## 20.4.11. Zstandard 压缩

在 OpenZFS 2.0 中引入了一种新的压缩算法。Zstandard (`Zstd`) 提供了比默认 LZ4 更高的压缩率，同时提供了比替代方案 gzip 快得的速度。OpenZFS 2.0 从 FreeBSD 12.1-RELEASE 开始通过 sysutils/openzfs 提供，并自 2020 年 9 月以来一直是 FreeBSD 13-CURRENT 的默认设置，将在 FreeBSD 13.0-RELEASE 中成为默认设置。

`Zstd` 提供了大量的压缩级别选择，提供了对性能与压缩率之间细粒度的控制。`Zstd` 的主要优势之一是解压速度与压缩级别无关。对于写入一次但多次读取的数据，`Zstd` 还允许使用最高压缩级别而不会产生读取性能损失。

即使数据被频繁更新，启用压缩通常也能带来性能收益。最大的优势之一来自压缩 ARC 特性。ZFS 的自适应替换缓存（ARC）在内存中缓存数据的压缩版本，每次需要时进行解压缩。这允许相同的内存能够存储更多数据和元数据，提高缓存命中率。

ZFS 提供了 19 级 Zstd 压缩，每一级都以更慢的压缩速度换取增量的空间节省。默认级别为 `zstd-3`，提供了比 LZ4 更强的压缩效果，且不会显著变慢。10级以上的级别需要大量的内存来压缩每个块，因此在内存少于 16 GB 的系统上不建议使用这些级别。ZFS 还实现了一系列 Zstd 快速级别，这些级别相应地更快，但压缩率较低。ZFS 支持 `zstd-fast-1` 到 `zstd-fast-10`，以 10 为步增的 `zstd-fast-20` 到 `zstd-fast-100`，最后是 `zstd-fast-500` 和 `zstd-fast-1000`，它们提供了极小的压缩，但提供了极高的性能。

如果 ZFS 无法为使用 Zstd 压缩块所需的内存，它将退回到以未压缩的形式存储块。在内存受限的系统上，除 Zstd 最高级别外不太可能发生。`sysctl kstat.zfs.zstd.compress_alloc_fail` 统计自 ZFS 模块加载以来发生这种情况的次数。

## 20.4.12. 去重

启用时，去重将使用每个块的校验和来检测重复块。当新块是现有块的重复项时，ZFS 会向现有数据写入一个额外的引用，而不是重复块。如果数据包含许多重复文件或重复信息，可以实现巨大的空间节省。

警告：去重需要极大量的内存，而大多数空间节省可以通过启用压缩来实现，无需额外成本。

要激活去重，请在目标池上设置 `dedup` 属性：

```
# zfs set dedup=on pool
```

只有写入池中的新数据会被去重。已经写入池的数据不会仅仅通过激活此选项而去重。一个新激活 `dedup` 属性的池看起来像示例所示：

```
# zpool list
```

| NAME | SIZE | ALLOC | FREE | CKPOINT | EXPANSZ | FRAG | CAP | DEDUP | HEALTH | ALTROOT |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| pool | 2.84G | 2.19M | 2.83G | - | - | 0% | 0% | 1.00x | ONLINE | - |

DEDUP 列显示实际去重率。1.00x 表示数据尚未被去重。在下一个示例中，端口被复制了三次：

```
# zfs set dedup=on pool
```

被去重且：

```
# zpool list
```

| NAME | SIZE | ALLOC | FREE | CKPOINT | EXPANSZ | FRAG | CAP | DEDUP | HEALTH | ALTROOT |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| pool | 2.84G | 2.19M | 2.83G | - | - | 0% | 0% | 1.00x | ONLINE | - |

DEDUP 列显示实际去重率。1.00x 表示数据尚未被去重。

```
# zdb -S
```

可能会拥有挂载点，从而损害主机的安全性。

## 20.5. 委托管理

一个全面的权限委托系统允许非特权用户执行 ZFS 管理功能。例如，如果每个用户的家目录都是数据集，则可以授予用户创建和销毁其家目录快照的权限。可以授予备份用户使用复制功能的权限。可以允许使用统计脚本运行，但仅具有访问用户空间利用数据的权限。甚至可以委托“委托权限的能力”。对于每个子命令和大多数属性，都可以进行权限委托。

### 20.5.1. 委托创建数据集

`zfs allow someuser create mydataset` 授予指定用户在所选的父数据集下创建子数据集的权限。但需要注意：创建一个新数据集涉及对其进行挂载。这需要将 FreeBSD 的 `vfs.mountroot.sysctl(8)` 设置为 `1`，以允许所有非 root 用户挂载文件系统。为了防止滥用的另一个限制是：非 root 用户必须是要挂载文件系统的挂载点的所有者。

### 20.5.2. 委托“权限委托”

`zfs allow someuser allow mydataset` 授予指定用户将任何目标数据集（或其在目标数据集及其子数据集上的权限）分配给其他用户的能力。如果用户拥有快照权限和 `allow` 权限，则该用户可以将快照权限授予其他用户。

## 20.6. 高级主题

### 20.6.1. 调优

有许多可以调整的参数，使 ZFS 在不同的工作负载下获得最佳性能。
