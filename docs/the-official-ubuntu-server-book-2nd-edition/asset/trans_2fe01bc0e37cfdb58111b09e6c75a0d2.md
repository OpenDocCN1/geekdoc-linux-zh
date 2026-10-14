

数组将在后台同步，但在此期间你仍可以使用系统。现在你需要更新 GRUB 配置，使其指向新的 UUID 和设备（否则每次都必须手动编辑）。过去你必须手动编辑，但现在只需输入 sudo update-grub，更新程序就会为你检测并更改所有相关条目。现在运行 sudo grub-install /dev/sda，以便更新 /dev/sda 上的 GRUB 实例。

现在你在运行软件 RAID 数组时遇到的问题是，GRUB 只会安装在第一块磁盘上。如果第一块磁盘丢失，第二块磁盘将无法自动启动系统。要解决这个问题，你必须手动将 GRUB 安装到第二块磁盘。这很容易——只需输入 sudo grub-install /dev/sdb。将设备从 /dev/sdb 更改为你的第二个 RAID 设备，如果它不同的话。如果你有第三块或第四块 RAID 设备，也只需为该设备运行 grub-install 即可。

最后一步，如果你尚未执行，则是使用 /dev/sda 上的分区工具并将两个分区都设置为分区类型 fd，以便它们能自动被检测为 RAID 设备。最后重启一次系统以确保它能启动到你的 RAID 数组。现在你的系统具有容错能力并且可以使用。

## 向 RAID 5 数组添加驱动器

为系统规划存储可能很困难。即使计划再好，有时机器的用途也会发生变化。无论如何，当你在 RAID 5 数组上需要更多存储时，你有几个选择。你可以备份所有数据，创建一个带额外驱动器的全新 RAID 5 数组，然后恢复，或者你可以尝试热扩展 RAID 5 数组。现在热扩展 RAID 5 数组可不是胆小者能做的事。我建议你尽可能备份数据，以防万一。

抛开所有警告不谈，假设我有一个标准的三磁盘系统使用 RAID 5，如我之前的 RAID 1 到 RAID 5 迁移示例中所述。我已向服务器添加了第四块磁盘 /dev/sdd，并且我想将我的 RAID 数组扩展到其上。由于我们想要扩展根分区的<|message|> 系统，我们需要从救援光盘执行所有这些步骤，因此将你的 Ubuntu Server 安装 CD 启动到恢复模式。当提示选择根文件系统时，按 Alt-F2 切换到另一个控制台。我们不想挂载任何文件系统，因为我们计划扩展它们。

进入救援模式 shell 后，使用 fdisk 为新驱动器分区，使其与其它驱动器匹配。完成后，使用 mdadm 将新分区添加到每个 RAID 数组中：

```
# mdadm /dev/md2 --add /dev/sdd1
mdadm: added /dev/sdd1
# mdadm /dev/md3 --add /dev/sdd2
mdadm: added /dev/sdd2
# mdadm /dev/md4 --add /dev/sdd5
mdadm: added /dev/sdd5
# cat /proc/mdstat
Personalities : [linear] [multipath] [raid0] [raid1] [raid6]
[raid5] [raid4] [raid10]
md4 : active raid5 sdd5[3](S) sda5[2] sdc5[1] sdb5[0]
176512 blocks level 5, 64k chunk, algorithm 2 [3/3] [UUU]

md3 : active raid5 sdd2[3](S) sda2[2] sdc2[1] sdb1[0]
16386048 blocks level 5, 64k chunk, algorithm 2 [3/3] [UUU]

md2 : active raid1 sdd1[3](S) sda1[2] sdc1[1] sdb1[0]
104320 blocks [3/3] [UUU]

unused devices: <none>
```

请注意，新分区已添加到每个数组中，但在它们后面带有 (S) 表示它们目前是热备盘。要扩展数组以同时使用这些驱动器，我们需要额外的 mdadm 命令：

```
# mdadm --grow --raid-devices=4 /dev/md2
# mdadm --grow --raid-devices=4 /dev/md3
# mdadm --grow --raid-devices=4 /dev/md4
```

此时所有驱动器都会变得非常繁忙，因为它们会在四个驱动器之间均匀地移动数据。由于 RAID 1 数组只需镜像而无需重新计算奇偶校验，因此应该完成得快得多，但扩展 RAID 5 数组可能需要数小时。在此期间，你可以监视 /proc/mdstat 来衡量进度。

```
# while [ 1 ]; do cat /proc/mdstat; sleep 15; done;
```

