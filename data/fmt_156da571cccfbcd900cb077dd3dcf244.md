
Gnomovision 版本 69，版权所有 (C) 19yy 作者姓名

Gnomovision 绝对不提供任何保证；详情请输入 `show w`。这是自由软件，您欢迎在特定条件下重新分发它；详情请输入 `show c`。

```
假设命令 'show w' 和 'show c' 应显示通用公共许可证的相关部分。当然，您使用的命令可能不叫 'show w' 和 'show c'；它们甚至可以是鼠标点击或菜单项——无论什么适合您的程序即可。

您还应该让您的雇主（如果您作为程序员工作）或您的学校（如果有），如果需要，为程序签署一份“版权免责声明”。以下是一个示例；请更改姓名：

> Yoyodyne, Inc. 特此声明对程序 'Gnomovision'（这是一个讽刺编译器的程序，由 James Hacker 编写）的所有版权利益。
> 
> \<Ty Coon 的签名\>，1989 年 4 月 1 日
> 
> Ty Coon，Vice 公司总裁

本通用公共许可证不允许将您的程序并入专有程序中。如果您的程序是一个子程序库，您可能认为允许专有应用程序与该库链接更有用。如果您希望这样做，请使用 GNU 库通用公共许可证（GNU Library General Public License）代替本许可证。
```

### C

附录

## 逻辑卷管理器摘要

### 目标：
实现一个非常灵活的虚拟磁盘子系统来处理磁盘存储。在线分配和重新定位存储。在线扩展和缩减存储。

### 功能：
逻辑卷管理器（LVM）在物理外设和内核中的 `I/O` 接口之间添加了一个额外层，以获得磁盘的逻辑视图。

这允许连接多个磁盘（所谓的物理卷或 `PV`）以形成存储池（所谓的卷组或 `VG`），并使用称为物理扩展（`PE`）的分配单位。

来自此 `VG` 的部分可以以所谓的逻辑卷（`LV`）的形式进行分配，单位为逻辑扩展（`LE`）。每个逻辑扩展映射到相应大小的物理扩展。这些物理扩展映射到磁盘上的偏移量和块。

然后，`LV` 可以通过设备特殊文件使用，类似于 `/dev/sd[a-z]*` 或 `/dev/hd[a-z]*`，命名为 `/dev/VolumeGroupName/LogicalVolumeName`。

但不仅如此，您还能够在运行时扩展或缩减 `VG` 和 `LV`。

### 概念：
物理卷、卷组和逻辑卷的配置信息存储在每个物理卷上以及自动创建的备份文件中，这些文件存储在 `/etc/lvmtab.d` 目录中。

磁盘上的配置区域称为卷组描述符区域（`VGDA`）。

LVM 驱动程序持有 `LV` 的 `LE` 与 `PV` 的 `PE` 之间的映射表。这些表由超级用户 LVM 命令创建/更新/删除。

驱动程序的主映射功能由 `/usr/src/linux/drivers/block/ll_rw_blk.c` 中的函数（在函数 `ll_rw_block()` 和 `ll_rw_swap_file()` 中）调用，传入 `LV` 中的一个逻辑块，并在表中查找对应的物理块/磁盘对。然后它将此对返回给调用的 `ll_rw_()` 函数，导致对磁盘块的物理 `I/O` 请求进入队列。

### 示例：
如果 `LV` 的容量变得太小，且包含此 `LV` 的 `VG` 已满，您可以向该 `VG` 添加另一个 `PV`，然后简单地扩展该 `LV`。

如果您减少或删除一个 `LV`，您可以将释放的容量用于同一 `VG` 中的不同 `LV`。

上述场景如下所示：

```
      /-----------------------------------\

      /---------\   VG 1      /---------\

      |         |           |         |

      |    PV 1 |   ......   |    PV n  |

      |         |           |         |

      | /--------------------------   

      | \\----LV 1----/         

      |\-------/          \\-------/

      \
```

```
PV 1 可以是 /dev/sdc1

PV n 可以是 /dev/sde1

VG 1 可以是 vg00

LV 1 可以是 /dev/test_vg/test_lv
```

获取上述场景的配置步骤：

1. 安装 LVM 后，执行 `insmod lvm` 或设置 `kernel/d/kmod` 以自动加载（参见 INSTALL）
2. 在两个磁盘上设置分区（#1），分区类型为 `0x8e`（我使用此类型以避免使用 L1NIX 主分区等）
3. 执行 `pvcreate /dev/sd[ce]1`
   - 为了测试目的，您可以在磁盘上使用多个主分区和/或扩展分区。
   - 出于性能原因，不要在常规 LVM 操作中这样做。
   - 如果必须这样做，不要将逻辑卷条带化到与同一磁盘上的分区关联的物理卷上。
4. 执行 `vgcreate test_vg /dev/sd[ce]1`
   - （`vgcreate` 也会激活卷组）
5. 执行 `lvcreate -L100 -ntest_lv test_vg` 以获得一个 100MB 的线性 `LV`
   - 或者执行 `lvcreate -i2 -I4 -l100 -nanoher_test_lv test_vg` 以获得一个 100 个 `LE` 大的逻辑卷，具有 2 个条带和 4 KB 的条带大小。
6. 随意使用创建的 `LV`。
   - 例如，使用 `mke2fs /dev/test_vg/test_lv` 在其中生成文件系统并挂载它。

### 命令概述和概念：
我将 LVM 命令分组并命名，类似于 HP 的命令。因此，处理物理卷的命令均以 `pv` 开头，处理卷组的命令以 `vg` 开头，而处理逻辑卷的命令以 `lv` 开头。

逻辑卷以 `lv.` 开头。

- `e2fsadm` - 逻辑卷管理封装器，包括 `lvextend`、`lvreduce`、`e2fsck` 和 `resize2fs` 的文件系统调整大小功能
- `lvchange` - 更改逻辑卷的属性
- `lvcreate` - 创建逻辑卷
- `lvdisplay` - 显示逻辑卷配置数据
- `lvextend` - 扩展逻辑卷的大小
- `lvreduce` - 缩减逻辑卷的大小
- `lvremove` - 移除逻辑卷
- `lvrename` - 重命名非活动的逻辑卷
- `lvscan` - 查找所有现有的逻辑卷
- `lvmchange` - 用于更改 LVM 属性的紧急程序
- `lvm.diskscan` - 扫描所有磁盘/分区和多重设备并列出它们
- `lvm.sadc` - 统计数据收集器
- `lvm.sar` - 统计数据显示器
- `pvchange` - 更改物理卷的属性
- `pvcreate` - 创建物理卷
- `pvdata` - 调试列出物理卷组描述符区域
- `pvdlsplay` - 显示物理卷配置信息
- `pvmove` - 将逻辑区段移动到不同的物理卷
- `pvscan` - 查找所有现有的物理卷
- `vgcfgbackup` - 备份所有卷组描述符区域
- `vgcfgrestore` - 将卷组描述符区域恢复到磁盘
- `vgchange` - 激活/停用卷组
- `vgck` - 检查卷组描述符区域的一致性
- `vgcreate` - 从物理卷创建卷组
- `vgdisplay` - 显示卷组配置信息
- `vgexport` - 导出卷组（使其对系统不可见）
- `vgextend` - 通过一个或多个物理卷扩展卷组
- `vgimport` - 导入卷组（使其对当前/另一个系统可见）
- `vgmerge` - 将两个卷组合并为一个
- `vgmknodes` - 创建包含所有逻辑卷特殊文件的卷组目录
- `vgreduce` - 通过一个或多个空的物理卷缩减卷组
- `vgremove` - 移除空的卷组
- `vgrename` - 重命名非活动的卷组
- `vgscan` - 扫描卷组
- `vgsplit` - 将一个卷组拆分为两个

LVM 会话输出示例：

```
# create physical volumes on 9 SCSI disk primary partition 1

pvcreate /dev/sd[b-eg-k]1

pvcreate -- /dev/sdl has an invalid physical volume identifier

pvcreate -- physical volume on /dev/sdlb1 successfully created

pvcreate -- reinitializing physical volume

# Logical Volume Manager Abstract

pvcreate -- physical volume on /dev/sdc1 successfully created

pvcreate -- reinitializing physical volume
```
