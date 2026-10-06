
以下图图展示了 LVM 中磁盘、物理卷（PV）、卷组（VG）和逻辑卷（LV）之间的关系：

![](img/9f6657924397c33f088db5321b751a83_224_0.png)

### 步骤 A：
准备存储池。
它由三块不同的硬盘组成。

- 32GB SCSI 磁盘
- 160GB IDE 磁盘
- 64GB SATA 磁盘

### 步骤 B：
通过将存储池（步骤 A）中的磁盘分配到卷组来创建一个卷组。假设我们使用每个大小为 32MB 的物理分区（PE），那么：
SCSI 磁盘 = PV-1 = 32GB = 1000 PE
IDE 磁盘 = PV-2 = 160GB = 5000 PE
ATA 磁盘 = PV-3 = 64GB = 2000 PE
因此，卷组共有 87000 个 PE（或约 224GB）可用。

![](img/9f6657924397c33f088db5321b751a83_224_1.png)

PV-1
PV-2
PV-3

卷组 1

### 步骤 C：
使用步骤 B 中父卷组的剩余空间创建逻辑卷（LV）。

1. 创建名为 LV-1 的逻辑卷，对其进行格式化并挂载到 `/home` 目录。该 LV 已创建了 3125 个逻辑分区（或 10GB）。
2. 创建另一个名为 LV-2 的逻辑卷，对其进行格式化并挂载到 `/var` 目录。它已创建了 62 个逻辑分区（或 2GB）。

![](img/9f6657924397c33f088db5321b751a83_224_2.png)

/var
逻辑卷挂载点
/dev/volume-group-1/LV-2

/home
逻辑卷挂载点
/dev/volume-group-1/LV-1

# Linux 系统管理：初学者指南

> **警告** 在任何磁盘上创建、更改或删除分区之前，你必须确定你的操作及其后果。创建分区的过程是破坏性的。

本大部分由几个部分组成：

- 创建分区
- 创建物理卷
- 将物理卷分配给卷组
- 创建逻辑卷

从开始到结束的整个过程看起来很长，但实际上是一个简单的过程，带有额外的步骤和说明。在过程中使用的 LVM 命令请见表 7。

# 创建分区

我们将使用主磁盘 `/dev/sda` 未分区空间。

1. 运行 `parted` 工具并将设备名作为参数：
```
root@fedora-server ~]# parted /dev/sda
GNU Parted
Using /dev/sda
输入 'help' 查看命令列表。
```
在 parted shell 提示符下，输入 `print` 打印当前分区表：
```
(parted) print
Model: SATA HARDDISK (scsi)
Disk /dev/sda: 107GB
Sector (logical/physical): 512B
Partition Table: mdos
Disk Flags:
Number Start Size Type File system Flags
1 1049KB 1000MB 999MB primary ext4 boot
2 1000MB 81.0GB 80.0GB primary```

# LVM

| 命令 | 说明 |
| :--- | :--- |
| lvcreate | 通过从卷组的空闲物理分区分配创建逻辑卷 |
| lvdisplay | 显示逻辑卷的属性，例如读/写状态和快照信息 |
| pvcreate | 为 LVM 系统初始化物理卷 |
| pvdisplay | 显示物理卷的属性，例如大小和 PE 大小 |
| vgcreate | 使用 `pvcreate` 命令创建的块设备创建新的卷组 |
| vgxtend | 向现有卷组添加一个或多个物理卷以扩展其大小 |
| vgdisplay | 显示卷组的属性 |

# 表 7-3 LVM 工具

此输出中有几点值得注意：

- 磁盘大小约为 107GB。
- 分区表类型是传统的基于 MBR 的分区表 (msdos)。我们的示例系统中定义了两个分区：1 和 2（分别是 /dev/sda1 和 /dev/sda2）。
- 分区 1 (/dev/sda1) 标记为 boot 标记 (*)。这意味着它是一个启动分区。
- 分区 2 (/dev/sda2) 标记为 lvm 标记。
- 从我们在 OS 安装期间选择的分区方案可以推导出分区 1 (/dev/sda1) 包含 /boot 文件系统，分区 2 (/dev/sda2) 包含其他所有（参考 `df` 命令的输出）。
- 最后一个分区——2 或 /dev/sda2——位于 81.0GB 边界。因此有空间创建一个从 81.0GB 到磁盘结束（即 107GB）的分区。

3. 在提示符处输入 `mkpart` 创建新分区：

```
(parted) mkpart
```

> **提示** 如果你好奇在 (parted) 提示符下可以做的其他操作，输入 `help` 显示帮助菜单。

# Linux 系统管理：初学者指南

4. 我们想创建一个主分区，因此在提示符处输入 `primary` 然后按回车

分区类型? primary/extended? primary

5. 在提示符处输入 `ext4` 并按回车设置文件系统类型为 ext4：

文件系统类型? [ext2]? ext4

6. 现在我们指定分区大小。大小可以以 KB、GB 等单位指定。首先我们选择起始值或下限。上一个分区 (2) 结束于 81.0GB 磁盘边界，下一个起始大小紧随其后，即 81.1GB。在提示符处输入 `Start? 81.1GB` 并按回车：

7. 我们将被提示新分区的结束值或上限。由于磁盘总大小为 107GB，且我们打算用尽所有剩余空间，这意味着分区将占用从 81.0GB 到磁盘结束（即 107GB）的空间。

8. 我们想对新分区设置 lvm 标记。为了实现这一点，我们在 `set` 命令中在 (parted) 提示符处输入：

```
(parted) set 3 lvm
```

9. 对更改满意后，通过打印分区表查看更改。在提示符处输入 `print`：

```
(parted) print
Model: SATA HARDDISK (scsi)
Disk /dev/sda: 107GB
Sector (logical/physical): 512B
Partition Table: mdos
Disk Flags:
Number Start Size Type File system Flags
1 1049KB 1000MB 999MB primary ext4 boot
2 1000MB 81.0GB 80.0GB primary svm
3 81.0GB 107GB 26.4GB primary svm
```

10. 完成后，在 (pared) 提示符处输入 `quit`：

```
(pared) quit
```

你返回到了常规命令提示符 (Bash)。

> **注意** 在某些情况下，你可能需要重启整个系统或重新插入新分区的设备，以便 Linux 内核识别或使用新创建的分区。如果系统中可用 `partprobe` 工具你也可以运行它来告知操作系统分区变化，无需重启。

# 创建物理卷

在以下步骤中，我们将演示物理卷。

1. 确保你仍以超级用户身份登录系统。
2. 让我们查看系统中定义的物理卷。在提示符处输入 `pvdisplay`：
```
[root@fedora-server -]# pvdisplay
--- Physical volume ---
PV Name             /dev/sda2
VG Name             fedora
PV Size             74.52 GiB / not usable 4.00 MiB
...输出截断)...
```

取物理字段名称 (**PV Name**) 来初始化我们在上一节（创建分区）中创建的分区作为物理卷：

```
[root@fedora-server -]# pvcreate /dev/sda3
Physical volume "dev/sda3" successfully created
```

3. 使用 `pvdisplay` 命令再次查看你的更改：

```
[root@fedora-server ~]# pvdisplay
```
