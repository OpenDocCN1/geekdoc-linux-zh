
# 618 第七部分：系统管理

| 命令 | 说明 |
|---|---|
| `svm` | 打开一个执行 LVM 命令的交互式 shell |
| `lvdiskscan` | 扫描所有磁盘以查找 LVM 物理分区 |
| `lvdisplay` | 显示逻辑卷的详细信息 |
| `lvcreate` | 创建逻辑卷 |
| `lvrename` | 重命名逻辑卷 |
| `lvchange` | 修改逻辑卷 |
| `lxtend` | 扩展逻辑卷的大小 |
| `lvreduce` | 减小逻辑卷的大小 |
| `lvremove` | 删除逻辑卷 |
| `lvs` | 列出带有详细信息的逻辑卷 |
| `lvresize` | 改变逻辑卷的大小 |
| `lvscan` | 扫描系统的逻辑分区 |
| `pvdisplay` | 显示 LVM 物理分区的详细信息 |
| `pvchange` | 修改 LVM 物理分区 |
| `pvcreate` | 创建 LVM 物理分区 |
| `pmove` | 将 LVM 物理分区的连接移动另一个分区 |
| `pvremove` | 删除 LVM 物理分区 |
| `pvs` | 列出带有详细信息的物理分区 |
| `pvresize` | 调整物理分区的大小 |
| `pvscan` | 扫描系统的物理分区 |
| `vgdisplay` | 显示卷组的详细信息 |
| `vgexport` | 激活卷组 |
| `vgimport` | 让导出的卷组被新系统识别。适用于将激活的卷组从一个系统移动到另一个系统。 |
| `vgmerge` | 合并卷组 |
| `vgreduce` | 从卷组移除物理分区 |
| `vgremove` | 删除卷组 |
| `vgs` | 列出带有详细信息的卷组 |
| `vgit` | 分割卷组 |
| `vgscan` | 扫描系统的卷组 |
| `vgck` | 检查卷组 |
| `vgrename` | 重命名卷组 |
| `vgcfbackup` | 备份卷组配置（元数据） |
| `vgcfrestore` | 恢复卷组配置（元数据） |

表 30-1 LVM 命令

## 第 30 章：RAID 和 LVM

### 显示 LVM 信息

你可以使用`pvdisplay`、`vgdisplay`和`lvdisplay`命令来显示物理分区、卷组和逻辑卷的详细信息。`pvscan`、`vgscan`和`lvscan`则列出你的物理卷、组和逻辑卷。

### 使用 LVM 命令管理 LVM 物理卷

物理卷（Physical Volume）可以是任何硬盘分区或`RAID`设备。`RAID`设备被视为单个物理卷。你可以从整块硬盘或硬盘上的分区创建物理卷。在具有许多硬盘的型大型系统中，你更有可能为每个物理卷使用整块硬盘。

要在整块硬盘上初始化物理卷，你使用硬盘设备名称，如下所示：

```
pvcreate /dev/sdc
```

如果你为整个驱动器使用单个分区，则使用该分区的设备名称创建一个新的物理卷，如下：

```
pvcreate /dev/sdc1
```

这将在`/dev/sdc`硬盘上创建一个名为`/dev/sdc1`的物理分区（第三个`SATA`驱动器，磁盘`c`）。要初始化多个驱动器，只需列出它们。以下命令创建了两个物理分区，`/dev/sdc1`和`/dev/sdd1`。

```
pvcreate /dev/sdc1 /dev/sdd1
```

你还可以使用不同硬盘上的多个分区。这种情况适用于你的硬盘用于不同的用途（例如运行不同的操作系统），或者你想将逻辑组分布在多个硬盘上。要一次性初始化这些分区，只需列出它们。

```
pvcreate /dev/hda3 /dev/hdb1 /dev/hdb2
```

一旦你初始化了分区，就必须创建`LVM`组。

### 管理 LVM 组

`LVM`分区用于创建卷组（Volume Group）。你可以使用`vgcreate`命令、卷组名称以及你想要的物理分区列表来手动创建卷组。

如果你正在创建一个新的卷组来容纳这些分区，那么在使用`vgcreate`命令创建卷组时，请将它们包含在组中。卷组可以使用一个或多个物理分区。之前描述的默认安装配置仅为`VolGroup00`使用了一个分区。在接下来的示例中，名为`mymedia`的卷组由两个物理卷`/dev/sdb1`和`/dev/sdc1`组成。

```
vgcreate mymedia /dev/sdb1 /dev/sdc1
```

上一个示例在两个`SATA`硬盘上设置了一个逻辑组，每个硬盘都有自己的单分区。或者，你可以设置一个跨越多个硬盘分区的卷组。如果你将分区用于不同的功能，这种方法可以让你获得利用多个硬盘所有可用空间的灵活性。接下来的示例创建了一个名为`rabbit`的逻辑组，它由三个物理分区`/dev/hda3`、`/dev/hdb2`和`/dev/hdb4`组成：

```
vgcreate rabbit /dev/hda3 /dev/hdb2 /dev/hdb4
```

如果你以后想向卷组添加物理卷，可以使用`vgextend`命令。`vgextend`命令向逻辑组添加新分区。在接下来的示例中，分区`/dev/hda3`被添加到了卷组`rabbit`中。实际上，你通过添加新的物理分区来扩展逻辑组的大小。

```
vgextend rabbit /dev/hda3
```

要向卷组添加一个新驱动器，你遵循类似的步骤。接下来的示例向卷组添加了第五个`SATA`硬盘`/dev/sde`。

注：原文中存在`vgxtend`等拼写错误，根据上下文及`LVM`标准命令，此处修正为`vgextend`。

```
vgextend rabbit /dev/hda3
```

### 激活卷组

上一个示例在两个`SATA`硬盘上设置了一个逻辑组，每个硬盘都有自己的单分区。或者，你可以设置一个跨越多个硬盘分区的卷组。如果你将分区用于不同的功能，这种方法可以让你获得利用多个硬盘可用空间的灵活性。接下来的示例创建了一个由三个物理分区`/dev/hda3`、`/dev/hdb2`和`/dev/hdb4`组成的逻辑组：

```
vgcreate rabbit /dev/hda3 /dev/hdb2 /dev/hdb4
```

如果以后要向卷组添加物理卷，你使用`vgextend`命令。`vgextend`命令向逻辑组添加新分区。在接下来的示例中，分区`/dev/hda3`被添加到了卷组`rabbit`中。实际上，你通过添加新的物理分区来扩展逻辑组的大小。

```
vgextend rabbit /dev/hda3
```

要向卷组添加一个新驱动器，你遵循类似的步骤。接下来的示例向卷组添加了第五个`SATA`硬盘`/dev/sde`。
