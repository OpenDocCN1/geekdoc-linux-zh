
- `-j`: 使用 `bzip` 压缩备份文件（`bz2` 格式），默认压缩等级为 2。
- `-W`: 显示允许备份的级别及备份时间。

例：将目录内容备份到 `/tmp/user.bak`，级别为 0，并查看备份时间：

```bash
[root@localhost ~] dump -f /tmp/user.bak /home
```

## 2) `restore` 命令

语法：`restore [选项] -f <备份文件>`

功能：还原由 `dump` 操作备份的文件或整个文件系统（一个分区）。

选项含义如下：
- `-f`: 指定要处理的文件。

例：还原 `/home` 中的备份文件：

```bash
[root@localhost ~] restore -f /tmp/user.bak /home
```

例 2：查看备份文件中的内容：

```bash
[root@localhost ~] restore -tf /tmp/user.bak
```

# 项目 6 硬盘管理

## 6.1 LVM 管理

每个 Linux 用户在安装系统时都会遇到这样的困境：在分区时如何精确地评估和分配容量？传统的分区方式在后期需要调整分区大小时变得非常不灵活。

`LVM`（Logical Volume Manager，逻辑卷管理）是一个完美的解决方案。它在硬盘和分区之上建立了一个逻辑层，管理员可以灵活地管理磁盘，并在添加新硬盘的情况下调整文件系统的大小。

### LVM 相关概念

1. **物理卷** (Physical Volume, PV)：底层单元，可以是整个硬盘或分区。
2. **卷组** (Volume Group, VG)：由多个 PV 组成的组，包含多个卷。
3. **逻辑卷** (Logical Volume, LV)：在 VG 上创建的文件系统，创建后可以扩展。
4. **物理块** (Physical Extent, PE)：每个 PV 被划分为单位，默认大小为 4MB。
5. **逻辑块** (Logical Extent, LE)：在同一个卷组中，LE 的大小与 PE 相同。

## 2. LVM 管理

利用 LVM 进行卷组管理的顺序是：`pv -> vg -> lv`。首先对应硬盘分区创建物理卷，然后将分区加入卷组，最后在卷组上创建逻辑卷并挂载。`LVM` 系统常用的命令如表 6-3 所示：

| 任务 | PV | VG | LV |
|---|---|---|---|
| 创建 | `pvcreate` | `vgcreate` | `lvcreate` |
| 删除 | `pvremove` | `vgremove` | `lvremove` |
| 显示 | `pvs` | `vgs` | `lvs` |
| 扫描 | `pvscan` | `vgscan` | `lvscan` |
| 显示属性 | `pvdisplay` | `vgdisplay` | `lvdisplay` |
| 更改属性 | `pvchange` | `vgchange` | `lvchange` |
| 扩展 | | `vgxtend` | `lvxtend` |
| 缩减 | | `vgreduce` | `lvreduce` |

## 1) 创建 LVM 类型的卷

进行 LVM 操作之前，应该在 `fdisk` 中将分区类型转换为 "Linux LVM (8e)"：

```bash
[root@localhost]# fdisk /dev/sda
(输入 n 帮助): t
(分区号 默认): 1
(输入 L 列出所有代码):8e
将分区 "Linux" 类型改为 "Linux LVM"
(输入 m 帮助): t
(分区号 默认): 2
(输入 L 列出所有代码):8e
将分区 "Linux" 类型改为 "Linux LVM"
(输入 m 帮助): p
磁盘=/dev/sdb: 107.4 GB, 107374182400 字节, 209715200 扇区
Units = 分区的 1 * 512 = 512 bytes
分区大小(逻辑/物理): 512 字节 / 512 字节
I/O 大小(最小/最大): 512 字节 / 512 字节
磁盘标识符: 0xc1dc010

| 设备 | Start | End | Blocks | Id System |
|---|---|---|---|---|
| /dev/sdb1 | 2048 | 20973567 | 10485760 | 8e Linux LVM |
| /dev/sdb2 | 20973568 | 41945087 | 10485760 | 8e Linux LVM |
```

### 2) 创建物理卷

例 1：将两个分区创建为物理卷 `/dev/sdb1`, `/dev/sdb2`：

```bash
[root@localhost ~] pvcreate /dev/sdb1 /dev/sdb2
```

例 2：显示物理卷的属性：

```bash
[root@localhost ~] pvdisplay
```

输出：

```
/dev/sdb1 is a new physical volume
"10.00 GiB"
---
...
/dev/sdb2 is a new physical volume
"10.00 GiB"
```

## 3) 创建卷组与逻辑卷

逻辑卷 "lvmm0" 已创建。

```bash
[root@localhost ~#] lvdisplay
```

输出：

```
--- vg 卷组信息 ---

| LV Path | /dev/vg0/lvm0 |
| :--- | :--- |
| LV Name | lvm0 |
| VG UUID | LGWhHt1-zrXy-afFx-yc7r-kLSM-6Wng-vYGel9 |
| LV Write Access | read/write |
| LV Creation host, time | localhost.localdomain, 2020-01-02 18:56:19+0800 |
| LV Status | available |
| # open | 0 |
| LV Size | 10.00 GiB |
| Current LE | 2560 |
| Segments | 2 |
| Allocation | inherit |
| Read ahead sectors | auto |
| - currently set to | 8192 |
| Block device | 253:0 |
```

5) 在逻辑卷中创建文件系统

将逻辑卷 `lvm0` 进行格式化，命令如下：

```bash
[root@localhost ~#] mkfs.ext3 /dev/vg0/lvm0
```

6) 挂载 `lvm0` 到目录 `/lvm0`，命令如下：

```bash
[root@localhost ~#] mount /dev/vg0/lvm0 /lvm0
[root@localhost ~#] umount /dev/vg0/lvm0
```

7) 若 LVM 无剩余空间，使用 `vgextend` 扩展卷组。

语法：`vgextend <卷组名> <物理设备名> [...]`

例：使用 `vgextend` 将物理卷加入到卷组 `vg0`，命令如下：

```bash
[root@localhost ~#] vgextend vg0 /dev/sdb3
```

其中 `/dev/sdb3` 必须是 LVM 类型。

(2) 若卷组有剩余空间，使用 `lvextend` 扩展卷组中的逻辑卷。命令如下：

```bash
# lvextend <L+卷增长> <逻辑卷名称>
# lvextend <L+PE值> <逻辑卷名称>
```

例 1：扩展逻辑卷 `lvm0` 的容量为 10 GB，命令如下：

```bash
[root@localhost ~#] lvextend -L+10G /dev/vg0/lvm0
```

例 2：减少逻辑卷 `lvm0` 的容量 10 GB，命令如下：

```bash
[root@localhost ~#] lvreduce -L-10G /dev/vg0/lvm0
```

# 学习清单 —— Linux 基本应用

(3) 按照“逻辑卷→卷组→物理硬盘”的顺序执行删除。

例 1：删除逻辑卷 `lvm0`，命令如下：

```bash
[root@localhost ~]# lvremove /dev/vg0/lvm0
Do you want to remove active logical volume Lvm0? [n/y]:
Logical volume "Lvm0" successfully removed
```

例 2：删除卷组 `vg0`，命令如下：

```bash
[root@localhost ~]# vgremove vg0
Volume group "vg0" successfully removed
```

例 3：删除物理卷 `/dev/sdb1` 和 `/dev/sdb2`，命令如下：

```bash
[root@localhost ~]# pvremove /dev/sdb1
```
