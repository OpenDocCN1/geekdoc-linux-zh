
在第 2 章介绍的操作系统安装过程中，您被要求留出一些空空间。现在我们将使用这些空空间，通过创建逻辑卷的步骤来演示一些 LVM 概念。

特别是，我们将创建一个逻辑卷来容纳当前 `/var` 的内容。大致想法是，因为 `/var` 目录通常用于存放增长的数据，将其单独分开是明智的。创建逻辑卷的步骤可以总结如下：

1. 初始化一个分区供 LVM 使用。
2. 从磁盘创建物理卷。
3. 将物理卷分配给卷组。
4. 最后，在卷组内创建逻辑卷并分配挂载点。

下面的图显示了 LVM 中磁盘、物理卷（PV）、卷组（VG）和逻辑卷（LV）之间的关系：

# 第 7 章：文件系统

img/0878ea6dc96f88116251d331ad33_207_0

步骤 A：准备存储池。该池由三块硬盘组成。

img/0878ea6dc96f88116251d331ad33_207_1

步骤 B：通过将存储池（步骤 A）中的磁盘分配到卷组创建一个卷组。假设物理区（PE）的大小为32MB，那么：

- SCSI 硬盘 = `PV-1` = 32GB = 1000 PE
- IDE 硬盘 = `PV-2` = 160GB = 5000 PE
- SATA 硬盘 = `PV-3` = 64GB = 2000 PE

因此，卷组共有 8000 个 PE（约 224GB）可用。

img/0878ea6dc96f88116251d331ad33_207_2

步骤 C：通过使用父卷组（步骤 B）的空间创建逻辑卷（LV）。

1. 创建名为 `LV-1` 的 LV，对其进行格式化并将其文件系统挂载到 `/home` 目录。该 LV 已创建了 3125 个逻辑区（约 100GB）。
2. 创建另一个名为 `LV-2` 的 LV，对其进行格式化并将其挂载到 `/var` 目录；它创建了 62 个逻辑区（约 2GB）。

img/0878ea6dc96f88116251d331ad33_207_3

逻辑卷挂载点 `/dev/volume-group-1/LV-2`

逻辑卷挂载点 `/dev/volume-group-1/LV-1`

# Linux 管理：初学者指南

> 注意 创建分区的过程对磁盘上已有的数据具有不可逆的破坏性。在对任何磁盘进行创建、更改或删除分区之前，你必须确定你的操作内容及其后果。

接下来的章节将分为几个部分：

- 创建分区
- 创建物理卷（Physical Volume）
- 将物理卷分配给卷组（Volume Group）
- 创建逻辑卷（Logical Volume）

从开始到结束整个过程看起来有些长。实际上这是一个简单的过程，但我们在步骤之间穿插了一些*额外步骤*，以及一些注释和解释。

让我们开始这个过程。表 7-3 列出了我们在处理过程中将使用的一些 LVM 工具。

| LVM 命令 | 描述 |
|---|--|
| `lvcreate` | 用于从卷组的空闲物理区池中分配逻辑区，从而在卷组中创建新的逻辑卷。 |
| `lvdisplay` | 显示逻辑卷的属性，例如读/写状态、大小和快照信息。 |
| `pvcreate` | 初始化物理卷以供 LVM 系统使用。 |
| `pvdisplay` | 显示物理卷的属性，例如大小和 PE 大。 |
| `vgcreate` | 用于使用 `pvcreate` 命令创建的块设备创建新的卷组。 |
| `vgxtend` | 用于向现有的卷组添加一个或多个物理卷以扩展其大小。 |
| `vgdisplay` | 显示卷组的属性。 |

**表 7-3.** LVM 工具

## 创建分区

我们将使用主系统磁盘 `/dev/sda` 上的未分区空间。

1. 首先运行带有 `-l` 参数的 `fdisk` 命令来列出当前的分区表。输入：

```bash
[root@fedora-serverA]# fdisk -l /dev/sda
Disk /dev/sda: 10.7 GB, 10737418240 bytes
255 heads, 63 sectors/track, 1305 cylinders
Units = cylinders of 16065 * 512 = 8225280
Disk identifier: 0x00005158
Device Boot Start End Blocks Id System
/dev/sda              *  25 200781 83 Linux
/dev/sda2             26 1200 9438187+ 8e Linux LVM
```

2. 接下来，再次使用 `fdisk` 开始实际的分区过程。输入：

```bash
[root@fedora-serverA]# fdisk /dev/sda
The number of cylinders for this disk is set to 1305...
...(OUTPUT TRUNCATED)...
2) booting and partitioning software from other operating systems (e.g., DOS FDISK, OS/2 FDISK)
```

命令（输入 m 获取帮助）：

你将看到一个简单的 `fdisk` 提示符 “Command (m for help):”，

3. 在 `fdisk` 程序内部再次打印分区表。在 `fdisk` 提示符处输入 `p` 来打印分区表。

```bash
Command (m for help): p
Disk /dev/sda: 10.7 GB, 10737418240 bytes
255 heads, 63 sectors/track, 1305 cylinders
Units = cylinders of 16065 * 512 = 8225280
Disk identifier: 0x00005158
Device Boot Start End Blocks Id System
/dev/sda              *  25 200781 83 Linux
/dev/sda2             26 1200 9438187+ 8e Linux LVM
```

关于此输出有几点值得注意：

- 磁盘总大小约为 10.7GB。
- 示例系统中当前定义了两个分区：`/dev/sda` 和 `/dev/sda2`。
- `/dev/sda` 分区类型为“Linux”（0x83），而 `/dev/sda2` 分区类型为“Linux LVM”（0x8e）。
- 根据我们在安装操作系统期间选择的分区方案，可以推断出 `/dev/sda1` 存放了 `/boot` 文件系统，而 `/dev/sda2` 包含了其他所有内容（参考 `df` 命令的输出）。
- 整个磁盘跨越 1305 个柱道。
- 最后一个分区即 `/dev/sda2` 于 1200 柱道边界结束。因此，有空间创建一个分区，占用从 1201 到磁盘上最后一个柱道（即 1305）的空间。

4. 在提示符处输入 `n` 创建新分区。

```
Command (m for help): n
```

注意 如果你对在 `fdisk` 提示符处可以做的其他操作感兴趣，请输入 `m` 显示帮助菜单。

5. 输入 `p` 选择主分区类型。

```
Command action
e extended
P primary partition (1-4)
P
```

6. 我们想创建第三个主分区。在提示输入数字时输入 `3`。

```
Partition number (1-4): 3
```

7. 下一步是指定起始扇区。我们选择第一个扇区。接受默认值。

```
First sector: 1201
```

8. 我们不是以兆字节为指定大小，而是输入磁盘的剩余部分。接受默认值。

```
Last sector: 1305
```

9. 默认情况下，`fdisk` 创建的分区类型为“Linux”。我们想将其类型更改为“Linux LVM”。使用 `t` 命令。

```
Command (m for help): t
```

10. 输入要更改的分区号。

```
Partition number (1-4): 3
```

11. 输入新类型的十六进制代码。

```
Hex code (Type): LVM
```

12. 当你对更改满意后，将表写入磁盘。

```
Command (m for help): w
```

13. 退出 fdisk 工具。

```
Command (m for help): q
```

14. 回 shell 提示符后，重启系统以便内核正确识别新的分区表。

```bash
[root@fedora-serverA]# reboot
```

### 创建物理卷

接下来，创建物理卷本身。

1. 系统重启后，再次以超级用户身份登录。
2. 首先查看当前的物理卷。
