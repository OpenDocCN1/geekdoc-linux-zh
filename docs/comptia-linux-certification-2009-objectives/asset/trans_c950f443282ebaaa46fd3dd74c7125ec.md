

2. 创建软件 RAID 5。

- a. 输入 `rpm -qa | grep mdadm` 以检查系统上是否已安装 `mdadm` 软件包。
- b. 观察到 `mdadm` 软件包已列出，并显示了版本和发布号，这表明它已安装。
- c. 输入 `mdadm --create --verbose /dev/md0 --level=5 --raid-devices=3 /dev/sdb7 /dev/sdb8 /dev/sdb9` 以创建 RAID 5 阵列。
- d. 如有必要，在提示处输入 `y` 以继续创建阵列。
- e. 观察到会显示有关 RAID 的详细信息，并且阵列 /dev/md0 已启动。按 `Enter` 键继续。
- f. 输入 `mdadm --detail --scan > /etc/mdadm.conf` 以创建包含 RAID 阵列信息的 RAID 配置文件 /etc/mdadm.conf。

3. 在 mdadm.conf 文件中指定设备信息。

- a. 输入 `vi /etc/mdadm.conf` 以打开 /etc/mdadm.conf 文件。
- b. 在新行中输入 `DEVICE /dev/sdb7 /dev/sdb8 /dev/sdb9` 以指定设备信息。
- c. 按 `Esc` 键退出命令模式。
- d. 保存并关闭文件。
- e. 输入 `clear` 以清除终端屏幕。

4. 在 RAID 设备上创建文件系统，并将 RAID 设备挂载到名为 /raid 的挂载点上。

- a. 输入 `mkfs.ext3 /dev/md0` 以在 RAID 设备 /dev/md0 上创建 ext3 文件系统。
- b. 观察到 inode 表已写入，日志已创建。
- c. 输入 `mkdir /raid` 以在 /raid 目录中创建用于 RAID 的挂载点。
- d. 输入 `mount /dev/md0 /raid` 以将 RAID 设备 /dev/md0 挂载到 /raid 挂载点上。

5. 检查是否创建了一个新的 RAID 设备。

- a. 输入 `cat /proc/mdstat` 以验证 RAID 设备是否已创建。
- b. 观察到显示了活动 RAID 设备的列表。
- c. 输入 `clear` 以清除终端屏幕。

## 发现活动 15-5

### 配置大容量存储设备

**场景**：
贵公司最近将所有系统关键服务器更换为 Linux，而你的经理 Mike 希望你备份数据。他希望你检查具有冗余性的大容量存储设备的设置。

1. **哪个文件包含有关设置 RAID 阵列的信息？**
   - a) /etc/raid/raidtab
   - b) **/etc/mdadm.conf**
   - c) /etc/raid/raidtab.conf

2. **判断对错？RAID 是一种将相同数据存储在多个硬盘上以提高性能和数据安全性的方法。**
   - **对**
   - 错

3. **以下哪些设备是大容量存储设备？选择所有适用项。**
   - **a) CD-RW 驱动器**
   - b) 软盘驱动器
   - **c) DVD-RW 驱动器**
   - **d) 硬盘驱动器**

# 主题 E

# 使用逻辑卷管理器管理逻辑卷

你已添加了新的存储设备以在 Linux 系统上存储大量数据。现在，当系统空间不足时，你希望管理存储区域。在本主题中，你将借助逻辑卷管理器来管理磁盘空间。

考虑这样一个场景：你正在从网站下载源文件以安装新软件。在下载过程中，显示错误提示，称你的主目录内存不足。你希望在不中断下载的情况下增加存储空间。为了管理当前情况，你决定将分配给交换文件系统（swap filesystem）的内存移动至主目录。了解 LVM（逻辑卷管理器）将使你能够完成此任务。

## LVM

**定义**：
*逻辑卷管理器（Logical Volume Manager，LVM）* 是一种用于管理计算机系统中磁盘存储的软件工具。LVM 在系统存储区域之上创建一个抽象层，从而隐藏数据存放位置的详细信息。它通过将硬件存储与软件管理完全分离来隐藏存储细节，以便在运行时对硬件所做的任何更改都不会影响软件。卷管理器将硬盘组织为卷组，存储区域中的分区被称为*逻辑卷（Logical Volumes，LV）*。

**示例**：

![](img/477ccb2f05b6ba1b2d563ea74f18c197_771_0.png)

*图 15-7：硬盘上的逻辑卷。*

## LVM 组件

LVM 包含五个主要组件。

| 组件 | 描述 |
| :--- | :--- |
| 卷组（VG） | VG 组件是 LVM 中最高级别的抽象。物理驱动器或硬盘被组织成 VG。磁盘或分区的类型应设置为 Linux LVM。 |
| 物理卷（PV） | PV 是一种用于管理目的并带有额外数据的物理介质。pvcreate 命令用于创建包含一个或多个 PV 的 VG。 |
| 物理扩展（PE） | 每个物理卷被划分为称为 PE 的数据块。PE 的大小与卷组的逻辑扩展大小相同。PE 是 LVM 在物理存储上可寻址的最小单位。 |
| 逻辑卷（LV） | 实际数据存储在逻辑卷中。LV 被称为标准块设备。它包含一个文件系统，该文件系统是使用 mkfs 命令设置的。例如，/home、/var。 |
| 逻辑扩展（LE） | 每个逻辑卷被划分为称为 LE 的数据块。同一卷组中所有逻辑卷的 LE 大小相同。 |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_772_0.png)

## LVM 架构

在存储驱动器中，每个 PV 被划分为大小相等的 PE。每个 PE 都被分配一个在 PV 内唯一的编号。在每个 PV 中，元数据信息存储在一个称为卷组描述符区域（Volume Group Descriptor Area，VGDA）的区域中。VGDA 包括 PV 描述、VG 描述、LV 描述以及多个 PE 描述，这些描述存储在每个 PV 的开头。每个 LV 被划分为 LE。LE 的大小与该 VG 的 PE 大小相同。每个 LE 都映射到 PV 上的一个 PE。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_772_1.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_772_2.png)

图 15-8：显示 LVM 架构的卷组

![](img/477ccb2f05b6ba1b2d563ea74f18c197_773_0.png)

## LVM 管理工具

LVM 包含许多执行各种功能 的工具。

最常用的 LVM 工具列在下表中。

| 工具 | 用于 |
| :--- | :--- |
| lvcreate | 创建 LV。 |
| lvdisplay | 显示有关 LV 的信息。 |
| lvextend | 为 LV 添加空间。 |
| lvreduce | 缩小 LV 的大小。 |
| lvremove | 从系统中移除 LV。 |
| lvscan | 列出所有 VG 中的所有 LV。 |
| pvcreate | 初始化 PV 以供 LVM 使用。 |
| pvdisplay | 显示 PV 的各种属性。 |
| pvmove | 将扩展从一个 PV 移动到另一个。 |
| pvscan | 列出所有 PV。 |
| vgcreate | 创建 VG。 |
| vgdisplay | 显示 VG 信息。 |
| vgextend | 为 VG 添加 PV。 |
| vgreduce | 从 VG 中移除 PV。 |
| vgremove | 移除 VG。 |
| vgscan | 搜索所有 VG。 |
| resize2fs | 调整 ext2/ext3 文件系统的大小。 |

## 语法

使用 LVM 工具的语法为：*{工具名称} {磁盘分区}*。

## LVM 快照

在系统崩溃的情况下，可以使用 LVM 快照来恢复文件系统。LVM 快照类似于 LV 的副本。用户可以创建多个 LV 的副本形式，即块设备。LV 存储对文件系统所做的更改，而不是存储整个文件系统。可以使用 lvcreate 工具创建它们。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_774_0.png)

## 快照卷

快照卷是一个包含在创建快照时卷内存在的数据记录的卷。快照卷允许你在文件系统正在运行且正在对其进行更改时备份文件系统。这些可以挂载为 LV，以跟踪自创建快照卷以来对文件系统所做的更改。

## 如何使用逻辑卷管理器管理逻辑卷

**操作参考：使用逻辑卷管理器创建逻辑卷**

若要使用逻辑卷管理器创建逻辑卷：

1. 在 CLI 中以 root 身份登录。
2. 输入 `fdisk /dev/{设备名称}{设备编号}`。
3. 创建类型为 LVM 的分区。
   - a. 输入 `n` 并按 **Enter** 键。
   - b. 输入 `p` 并按 **Enter** 键。
   - c. 输入 `1` 并按 **Enter** 键。
   - d. 按 **Enter** 键两次。
   - e. 输入 `t` 并按 **Enter** 键。
   - f. 输入 `8e` 并按 **Enter** 键。
   - g. 输入 `w` 并按 **Enter** 键。
   - h. 输入 `partprobe` 以更新分区表。
   - i. 输入 `vgscan` 以启用 LVM 来定位类型为 Linux LVM 的分区。
   - j. 输入 `pvcreate /dev/{设备名称}{设备编号}` 以在每个硬盘上创建物理卷。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_774_1.png)

   - k. 输入 `vgcreate {卷组名称} /dev/{设备名称}{设备编号 1} ... /dev/{设备名称}{设备编号 n}`

