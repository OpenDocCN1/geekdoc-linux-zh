
```
# fdisk /dev/sdb
...
Command (m for help): new
Command action
  e extended
  p primary partition (1-4): p
Partition number (1-4): 1
First cylinder (1-2213, default 1): <Enter>
Using default value 1
Last cylinder (+size or +sizeM or +sizeK (1-2213, default 2213)): <Enter>
Using default value 2213
Command (m for help): type
Selected partition 1
Hex (type L to list codes): fd
Changed system type of partition 1 to fd (Linux autodetect)
Command (m for help): write
The partition table has been altered,
Calling ioctl() to re-read partition table.
Syncing disks.
```

在为另外两块磁盘写入分区标签后，是时候开始实战构建 RAID 阵列了。大多数现代发行版使用单一的 `mdadm` 命令。之前的 RHEL 使用 `raidtools` 工具包，但由于 `mdadm` 比 `raidtools` 更强大且更易使用，因此我们在这里演示它。

![](img/cb325d29f74eb66e46eaf8d38883ecfe_179_0.png)

## 第 7 章 – 添加磁盘

以下命令从我们的三个 SCSI 分区构建一个 RAID 5 阵列：

```
# mdadm --create /dev/md0 --level=5 --raid-devices=3 /dev/sdb1 /dev/sdc1
/dev/sdd1
mdadm: array /dev/md0 started.
```

在构建阵列时，`/proc/mdstat` 显示进度信息：

```
# /proc/mdstat
Personalities: [raid5]
md0: active raid5[3] sdc[1] sdd[2]
3556636 blocks level 5, 64k chunk, algorithm 2 [3/2] [UU]
=======> recovery 22.4% (399916/17783618) finish=5.1min
speed=44800/sec
unused devices: <none>
```

该文件反映内核 RAID 系统的当前状态。在添加新磁盘或更换故障驱动器后，关注此文件特别有用。`watch cat /proc/mdstat` 是一个好用法。

一旦阵列组装完成，我们会在 `/var/log/printout` 文件中看到通知消息：

```
RAID5 printout:
-- rd:3: wd=3 fd:0
disk 0, 0:1, dev:sdb
disk 1, 0:1, dev:sdc
disk 2, 0:1, dev:sdd
```

初始命令也用于“激活”（使用），但在随后的重启中，我们需要作为一个独立的步骤激活阵列，通常在启动脚本中执行。RHEL、Fedora 和 SUSE 包含了用于 RAID 的示例启动脚本。

`mdadm` 技术上并不要求配置文件，尽管如果存在配置文件（通常为 `/etc/mdadm.conf`），它会使用它。我们强烈建议使用配置文件。它以标准方式记录 RAID 配置，让管理员在出现问题时有一个明显的地方查找信息。不使用配置的替代方案是在激活阵列时在命令行中指定配置。

`mdadm --detail --scan` 将当前的 RAID 设置导出到配置文件。遗憾的是，它打印的配置并不完整。以下命令可以为你的示例创建一个完整的配置文件：

```
# ECHO /dev/sdb1 /dev/sdc1 /dev/sdd1 > /etc/mdadm.conf
# mdadm --detail --scan >> /etc/mdadm.conf
# cat /etc/mdadm.conf
```

```
DEVICE /dev/md0 level=raid5
devices /dev/sdb1 /dev/sdc1 /dev/sdd1
```

### 7.8 高级 sdb 管理：RAID 和 LVM

Disk `/dev/sdb`: 18.2 GB, 1821003676 bytes

255 heads, 63 sectors/track, 2213 cylinders

Units = cylinders of 16065 * 512 = 8225280

| Device | Boot | Start | End | Blocks | Id | System |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| System | lvm |
| :--- | :--- |
| Metadata | 1 |
| Metadata Sequence | 1 |
| VG Access | read/write |
| VG Status | resizable |
| MAX LV | 0 |
| Cur LV | 0 |
| Open LV | 0 |
| Max PV | 0 |
| Cur PV | 1 |
| Act PV | 1 |
| VG Size | 33.92 GB |
| PE Size | 4.00 MB |
| Total PE | 8683 |
| Alloc PE / Size | 0 | 0 |
| Free PE / Size | 8683 / 33.92 GB |
| VG UUID | nhkkZN-KHmY-Bf5V-6FY6-3LF8-dp5-JM5 |

由于 RAID 5 提供了一些数据冗余，我们在前面的节中构建的 RAID 5 阵列在磁盘崩溃时仍能够继续运行；用户并不一定察觉到

### 7.8 高级磁盘管理：RAID 和 LVM

任何问题。你需要密切关注系统日志以尽早发现问题（或者让一个程序为你完成此工作；参见第 220 页）。

`mdadm` 提供了一个方便的选项，可以模拟磁盘故障：

```bash
# mdadm /dev/md0 -f /dev/sdc1
mdadm: set /dev/sd1 faulty in /dev/md0

# tail /var/log/messages
30 May 16:14:55 harp kernel: raid5: Disk failure on sdc, disabling device.
Operation continuing on 2 devices
kernel: RAID5 conf printout:
kernel: -- rd:3 w:2 fd:1
kernel: disk 0, o:1, dev/sdb1
kernel: disk 1, o:0, dev/sdc1
kernel: disk 2, o:1, dev/vdd1
kernel: RAID5 conf printout:
kernel: --- rd:3 w:2 fd:1
kernel: disk 0, o:1, dev/sdb1
kernel: disk 2, o:1, dev/sdd1
```

如所示，系统日志 `/var/log/messages` 在故障（模拟）发生后立即就会包含相关信息。从 RAID 状态文件 `/proc/mdstat` 也可以获得类似的信息。此时，管理员应该采取以下行动：

- 从 RAID 阵列中移除磁盘。
- 安排停机并关闭计算机（如有必要）。
- 更换物理驱动。
- 将新驱动添加到阵列。

要从 RAID 配置中移除驱动，使用 `mdadm`：

```bash
# mdadm /dev/md0 -r /dev/sdc1
mdadm: hot removed /dev/sdc1
```

一旦磁盘在逻辑上被移除，你就可以更换驱动。热插驱动硬件允许你在无需关闭系统或重启的情况下进行更改。

如果你的 RAID 阵列是磁盘，你应该只用相同的驱动器替换它们。基于分区的组件可以用任何大小相似的分区替换，尽管为了匹配带宽，最好使用硬件驱动。如果你的 RAID 配置构建在分区之上，在将替换磁盘添加到阵列之前，你必须使用 `fdisk` 适当地定义分区。

在我们的示例中，故障只是模拟，因此我们可以在不更换任何硬件的情况下将驱动加上阵列：

```bash
# mdadm /dev/md0 -a /dev/sdc1
mdadm: hot added /dev/sdc1
```

Linux 会重建阵列并像往常一样在 `/proc/mdstat` 显示进度。

## 重新分配存储空间
