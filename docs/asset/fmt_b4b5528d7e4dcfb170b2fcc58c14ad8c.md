
输出将暴露一百多个不同的卷设置。

### 5. 显示卷的详细统计信息，包括配置信息：

```
[user18@server2 ~]$ sudo vdo status --name vdo-vol1
VDO status:
  Date: '2019-10-24 17:07:35-04:00'
  Node: server2.example.com
Kernel module:
  Loaded: true
  Name: kvdo
  Version information:
    kvdo version: 6.2.0.293
Configuration:
  File: /etc/vdconf.yml
  Last modified: '2019-10-24 14:03:13'
VDOs:
  vdo-vol1:
    Acknowledgement threads: 1
```

该状态包含了卷、内核模块和配置信息。它还提供了卷特定元素的详细视图。

### 6. 显示压缩和去重功能的激活状态：

```
[user18@server2 ~]$ sudo vdo status --name vdo-vol1 | grep -i compression
Compression: enabled
[user18@server2 ~]$ sudo vdo status --name vdo-vol1 | grep -i deduplication
Deduplication: enabled
```

新的 VDO 卷默认激活了压缩和去重功能。练习此结束。

## 练习 13-8：删除 VDO 卷

此练习应在 `server2` 上以 `user1` 身份进行，并需要 `sudo` 权限。

在此练习中，你将删除练习 13-7 中创建的 `vdo-vol1` 卷并确认其删除。

### 1. 使用 `vdo` 和 `lsblk` 命令验证卷仍然存在：

```
[user@server2 ~]$ sudo vdo list
vdo-v01
[user@server2 ~]$ lsblk /dev/sdf
NAME MAJ:MIN SIZE RO TYPE MOUNTPOINT
sdf 8:0 4G 0 disk
└─vdo-v01 253:2 0 160 0 vdo
```

### 2. 使用 `vdo` 命令指定要删除的卷名称 (`--name`)：

```
[user@server2 ~]$ sudo vdo remove --name vdo-v01
Removing VDO-v01
Stopping VDO-v01
```

### 3. 使用 `vdo` 和 `lsblk` 命令确认删除：

```
[user@server2 ~]$ sudo vdo list

[user@server2 ~]$ lsblk /dev/sdf
NAME MAJ:MIN SIZE RO TYPE MOUNTPOINT
sdf 8:0 4G 0 disk
```

如上述输出所示，该卷已成功删除。

我们将在第 15 章“本地文件系统和交换分区”中重新创建 VDO 卷，以用于文件系统和交换区域。

## 本章总结

本章从磁盘分区信息如何存储以及存储在何处的概述开始。它介绍了两种常用方案之间的对比，并解释了在什么情况下应该使用哪种。稍后，我们简要地提到了 RHEL 中提供的常用存储管理解决方案。

我们研究了精简置备（thin provisioning）的概念，并意识到与该技术相关的益处。

接下来，我们使用 MBR 和 GPT 分区方案划分了可用的磁盘设备。我们通过直接在命令行提示符运行一个命令并在交互模式下启动另一个命令，演示了分区的创建、显示和删除操作。

本章的最后一个主题集中于不久前引入 RHEL 的一种存储管理解决方案。该解决方案利用底层的精简置备、去重和压缩技术来节省成本、确保存储空间的有效利用并提高数据吞吐量。我们在最后执行了几个练习，演示了使用该解决方案创建和删除卷。

## 检验理解

- 1. 命令 `vdo --name vdo1 --vdoLogicalSize 16GB --vdoSlabSize 128MB` 缺少什么？
- 2. 在 GPT 磁盘上可以创建的最大可用分区数量是多少？
- 3. 哪个内核模块负责 VDO 卷中的数据块压缩？
- 4. VDO 卷用于节省存储的三种技术是什么？
- 5. 命令 `parted /dev/sdc mkpart pri 1 200m` 会做什么？
- 6. 在基于 BIOS 的系统上，分区表信息存储在哪里？
- 7. VDO 消除消除数据块随机化的技术名称是什么？
- 8. `sdd3` 代表什么？
- 9. 哪个命令可以查看 VDO 卷的用法统计信息？
- 10. 精简置备技术允许我们创建大于实际物理存储大小的卷。对还是错？
- 11. 如果你在 `/dev/sdf` 磁盘上有一个名为 `vdo1` 的未用 VDO 卷并尝试删除它。你运行了 `vdo remove --device /dev/sdf` 但删除失败了。你哪里做错了？
- 12. 在 MBR 磁盘上可以创建的最大可用分区数量是多少？
- 13. 命令 `systemctl --now enable vdo` 会做什么？
- 14. `gdisk` 工具可用于 MBR 格式存储分区信息。对还是错？
- 15. 命令 `parted /dev/sdd mkllabel msdos` 会做什么？
- 16. VDO 是一个内存密集型解决方案。对还是错？
- 17. 在基于 BIOS 的系统上，分区表信息存储在哪里？
- 18. 哪个命令可以查看 VDO 卷的用法统计信息？
- 19. 去重是移除数据块的过程。

## 检验理解答案

- 1. 命令中缺少 `--name` 选项。
- 2. 12
- 3. `kvdo` 模块负责此项。
- 4. 精简置备、去重和压缩。
- 5. 提供的将在 `sdc` 磁盘上创建一个 200MB 的分区。
- 6. 分区信息存储在主引导记录（MBR）中。
- 7. VDO 使用精简置备消除随机化。
- 8. `sdd3` 代表第三个分区。
- 9. 可以使用 `vdo status` 命令查看统计。
- 10. 对。
- 11. 正确的命令应该是 `vdo remove --name vdo1`。
- 12. 14。
- 13. `systemctl --now enable vdo` 命令将启动并启用 VDO 服务。
- 14. 错。
- 15. 该命令将 `sdd` 应用 `msdos` 标签。
- 16. 错。
- 17. 分区表存储在文件中。
- 18. 可以运行 `vdo status` 命令并将输出传递给 `grep "compression"`。
- 19. 去重是移除数据块的过程。

## 自行挑战

以下实验有助于加强本章学习的大部分概念。未提供分步指南，但包含了相关主题的提示。

根据需要为 `server2` 添加存储。

### 实验 13-1：使用 parted 创建和删除分区

在 `server2` 上以 `user1` 身份运行 `sudo`，直接在命令行提示符调用 `parted` 工具，在 250MB 磁盘之一上（`lsblk` 查看）创建一个 100MB 主分区。如果磁盘是新的，则应用 `msdos` 标签。通过交互模式运行 `parted` 创建另一个 100MB 分区，确保第二个分区不会与第一个交叉。验证标签和分区。从命令行提示符移除两个分区。（提示：MBR 存储管理）。

### 实验 13-2：使用 gdisk 创建和删除分区

在 `server2` 上以 `user1` 身份运行 `sudo`，使用 `gdisk` 工具在 250MB 磁盘之一上（`lsblk` 查看）创建两个 80MB 分区。确保分区不会交叉。验证分区。如果你愿意，可以删除这些分区。（提示：GPT 存储管理）。

### 实验 13-3：创建和删除 VDO 卷

在 `server2` 上以 `user1` 身份运行 `sudo`，检查是否安装了 VDO 软件以及 VDO 服务是否启用并启动。使用 `lsblk` 命令识别 4GB 磁盘，并确保它未在使用。使用 `vdo` 命令在 4GB 磁盘上创建一个逻辑大小为 16GB 的卷 `testvdo`。为卷选择合适的 slab 大。使用 `vdo`、`lsblk` 和 `vdo status` 命令验证卷的创建。（提示：使用虚拟数据优化器优化存储）。

```
[user1@server2 ~]$ sudo vstats --verbose
/dev/mapper/vdo-vol1 :
version : 30
release version : 133524
data blocks used : 0
overhead blocks used : 723226
logical blocks used : 0
physical blocks : 1048576
logical blocks : 4194304
1K-blocks : 4194304
1K-blocks used : 2892904
1K-blocks available : 1301400
used percent : 68
```
