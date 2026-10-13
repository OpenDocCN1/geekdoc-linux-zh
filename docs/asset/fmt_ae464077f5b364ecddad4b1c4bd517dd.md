
![](img/92a94ba94656919835b7a50a27c9d9ba_560_0.png)

## 如果 rescue 无法找到或无法挂载你的 Linux 文件系统

如果你收到 `rescue` 无法找到或无法挂载你的 Linux 文件系统的消息，那么救回存储在 Linux 文件系统中的当前数据已无能为。

只需重置你的系统（从安装 CD 开始）并重新安装 Linux。然后，使用在本小时之前的说明从你拥有的任何备份中恢复。

## 尝试修复文件系统

如果 `rescue` 能够找到并挂载你的 Linux 文件系统，你可以尝试一种通常可以将无法启动的 Linux 系统恢复完全功能的技巧——文件系统检查。`efck` 命令可用于彻底检查你的 Linux 文件系统的结构性问题并尝试修复它们。

在 `rescue` 中使用 `efsck`，你可以通过 `-f` 参数（强制进行文件系统检查）调用它，并提供要检查的设备名称作为参数。然而，有一个陷阱——`fsck` 绝不能在已挂载的文件系统上运行。因此，要在 `rescue` 中使用 `efsck` 测试你的文件系统，请遵循以下步骤。

![](img/92a94ba94656919835b7a50a27c9d9ba_560_1.png)

> 你在第 5 “让控制台为你工作”中学习了数据管道和 `grep` 命令。

首先，输入不带参数的 `mount` 命令来列出挂载的文件系统；将输出传递给 `grep` 命令并搜索 `sysimage`。因为 `rescue` 已经告诉你，所有的 Linux 文件系统挂载在 `/mnt/sysimage` 下。

```bash
mount | grep sysimage
dev/sda2 on /mnt/sysimage ext3 (ro)
dev/sda1 on /mnt/sysimage/boot ext3 (ro)
none on /mnt/sysimage/devpts devpts (ro)
none on /mnt/sysimage/proc proc (ro)
```

## 备份、故障排除与救援

忽略以 `none` 开头的行；这些是虚拟文件系统，没有真实的设备连接。在这种情况下，Linux 文件存储在两个设备上：`/dev/sda1` 和 `/dev/sda2`。在 `rescue` 中使用 `efsck` 之前，所有文件系统必须卸载。要做到这一点，请使用：

```bash
umount /mnt/sysimage
umount /mnt/sysimage/boot
umount /mnt/sysimage/devpts
umount /mnt/sysimage/proc
```

现在你可以在设备上运行 `efsck`：

```bash
efck -f /dev/sda1
efck -f /dev/sda2
```

`efck` 的输出看起来如下：

```text
/dev/sda1:
  superblock group 0, size 32768, primary 32768, backup 98304
... (lines of output) ...
/dev/sda1: is modified.

Pass 1:
  blocks count: 262144
  free block count: 131088
  used count: 157612
  free blocks: 131556
  free count: 39.4%
... (lines of output) ...

Pass 2:
  inodes count: 65536
  free inode count: 32768
  used count: 32768
  free inodes: 32768
  free count: 50.0%
... (lines of output) ...

[此处省略 Pass 3 到 Pass 48 的重复输出]
```

在 `efsck` 结束后，你可以再次挂载文件系统：

```bash
mount /dev/sda1 /mnt/sysimage

mount /dev/sda2 /mnt/sysimage/boot
```
