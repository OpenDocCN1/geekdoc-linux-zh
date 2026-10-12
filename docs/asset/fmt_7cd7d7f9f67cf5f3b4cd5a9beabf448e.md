
### 16. 为了在镜像中替换它，我们需要执行以下操作。为了附加另一个设备，我们指定镜像中的现有设备并使用 `zpool attach` 挂它：

```
root@raspberry:~# zpool attach data2 /home/bob/disk2 /home/bob/disk1
root@raspberry:~#
```

### 17. 检查池的状态：

```
root@raspberry:~# zpool status data2
pool: data2
state: ONLINE
scan: resilvered 167K in 00:00:00 with 0 errors on Sun Nov 19
11:26:47 2023
```

config:

| NAME | STATE | READ | WRITE | CKSUM |
|---|---|---|---|---|
| data2 | ONLINE | 0 | 0 | 0 |
| mirror-0 | ONLINE | 0 | 0 | 0 |
| /home/bob/disk2 | ONLINE | 0 | 0 | 0 |
| /home/bob/disk1 | ONLINE | 0 | 0 | 0 |

## 18. 向镜像池添加磁盘

使用 ZFS 完成的一项非常关键且极其实用的管理程序是在不离线的情况下向池添加磁盘。让我们使 `data2` 池的大小翻倍：

# 树莓派 OS 系统管理：辅助主题

```
root@raspberrypi:~# zpool list
```

```
NAME SIZE ALLOC FREE CKPOINT EXPANDZ
FRAG CAP DEDUP HEALTH ALTROOT
data2 112M 130K 112M - -
      4% 0% 1.00x ONLINE
root@raspberrypi:~#
```

### 19. 我们可以使用 `zpool add` 向现有存储池添加磁盘。

```
root@raspberrypi:~# zpool add data2 mirror /home/bob/disk3 /home/bob/disk4
root@raspberrypi:~# zpool list
NAME SIZE ALLOC FREE CKPOINT EXPANDZ
FRAG CAP DEDUP HEALTH ALTROOT
data2 224M 139K 224M - -
      2% 0% 1.00x ONLINE
root@raspberrypi:~#
```

### 20. 存储池中的文件系统始终可用。如果我们现在查看状态，它显示存储池由两个镜像组成：

```
root@raspberrypi:~# zpool status data2
pool:   data2
state:  ONLINE
scan:   resilvered 167K in 00:00:00 with 0 errors on Sun Nov 19
        11:26:47 2023
config:
NAME    STATE READ WRITE CKSUM
data2 ONLINE 0 0 0
  mirror-0 ONLINE 0 0 0
    /home/bob/disk2 ONLINE 0 0 0
    /home/bob/disk1 ONLINE 0 0 0
  mirror-1 ONLINE 0 0 0
    /home/bob/disk3 ONLINE 0 0 0
    /home/bob/disk4 ONLINE 0 0 0
```
errors: No known data errors
root@raspberrypi:~#

# ZFS 管理与使用

### 21. 我们可以使用 `zpool iostat -v` 查看数据当前写入到存储池的哪个位置：

```
root@raspberrypi:~# zpool iostat -v data2
capacity      operations bandwidth
pool          alloc free      read write
data2         139K 224M 0      0      127 1.74K
mirror-0      125K 112M 0      1     1.11K 10.9K
/home/bob/disk2  -     0      0      118 749
/home/bob/disk1  -     0      0      27 4.04K
mirror-1      144K 112M 0      0     156 15.4K
/home/bob/disk3  -     0      0      78 7.69K
/home/bob/disk4  -     0      0      78 7.69K
```

```
root@raspberrypi:~#
```

### 22. 所有数据目前都写入了第一对镜像，而没有写入第二对镜像。这是合理的，因为第二对磁盘是在数据写入后添加的。如果我们向存储池写入一些新数据，将将会使用新的镜像：

```
root@raspberrypi:~# truncate -size 64m /data2/data2file
root@raspberrypi:~# zpool iostat -v data2
capacity      operations bandwidth
pool          alloc free      read write
data2         138K 224M 0      0      121 1.68K
mirror-0      116K 112M 0      1     798 7.73K
/home/bob/disk2  -     0      0      113 7.23
/home/bob/disk1  -     0      0      19 2.87K
mirror-1      22.5K 112M 0      0      70 7.02K
/home/bob/disk3  -     0      0      35 3.51K
/home/bob/disk4  -     0      0      35 3.51K
```

### 23. 我们看到写入新镜像的数据比写入旧镜像的多了一点点：ZFS 尝试尽地利用存储池中的所有资源。现在完成本章的练习，然后继续进行下一步。

# 章末练习

- 1. 如果你还没有这样做，请执行示例 1.1 的之前所有步骤，使用正确的命令和路径。
- 2. 在示例 1.1 的第 4 步中，`datafile2` 的路径是什么？
- 3. 如果你使用像 `emacs` 这样的文本编辑器在名为 `data` 的文件系统中创建一个名为 `text.txt` 的文件，你将如何指定该文件的完整路径？
- 4. 在示例 1.1 中，在正确执行第 6 步后，当你在 `data2` 文件系统中用 `emacs` 创建了一个文本文件时，该文本文件的两个镜像版本的路径名会不同吗？换句话说，你能够通过为它们指定不同的路径来分别编辑它们吗？
- 5. 在示例 1.1 的第 19 步中，你是否可以向镜像 `data2` 存储池添加单个磁盘，而不是指定的两个磁盘？
- 6. 在示例 1.1 的第 20 步中，镜像是否命名为 `mirror-0` 和 `mirror-1`？

### 24. 清理

在完成工作后清理。

### 25. 最后，删除。

### 26. 退出

结论：ZFS 可以通过命令回滚文件系统。

# ZFS 管理与使用 示例 1.2：发送与接收

**目标：**

本示例演示了如何使用 `zfs` 命令进行快照。

**介绍：**

在本例中，我们将备份 ZFS 文件系统。这是一种安全且快速的回滚方法。

**背景：**

ZFS 快照是文件系统在某一时刻的“快照”。回滚允许我们恢复到之前的状态。

# 回滚 ZFS 文件系统

以下是回滚 ZFS 系统的详细说明：

- 1. 列出快照

首先列出要回滚的 Z 文件系统的可用快照。你可以使用 `zfs list` 命令：

```bash
zfs list pool/filesystem
```

在上述命令中，将 `pool/filesystem` 替换为实际的存储池/文件系统名称。此命令将显示快照。

- 2. 选择快照

确定你想回滚的快照。例如，假设你想回滚到快照 `@20230101`。注意该名称是快照拍摄的日期。

- 3. 执行回滚

要将 ZFS 文件系统回滚到指定的快照，使用 `zfs rollback` 命令：

```bash
zfs rollback pool/filesystem@20230101
```

将 `pool/filesystem` 替换为实际的存储池/文件系统，并将 `20230101` 替换为要回滚的快照名称。

- 4. 验证回滚

通过列出 ZFS 文件系统的内容来验证回滚是否成功：

```bash
ls /path/to/mount/point
```
