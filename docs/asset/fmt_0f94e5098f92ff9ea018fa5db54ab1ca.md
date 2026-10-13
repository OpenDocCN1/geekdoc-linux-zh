
``` 
VolGroup01 {

    id = "ZFRYS-jY1YP-UvC-eAE3-QkAN-v5vM-ZDGS1H"

    seqno = 4

    status = "RESIZEABLE", "READ", "WRITE"

    extent_size = 8192      # 4 Megabytes

    max_lv = 0

    max_pv = 0

    physical_volumes {

        pv0 {

            id = "xj3rs8-tOXA-d6f1-0ZiZ-EIT2-8r3t-QC08s"

            device = "/dev/sdb"      # Hint only

            status = "ALLOCABLE"

            dev_size = 16777216     # 8 Gigabytes

            pe_start = 384

            pe_count = 2047         # 7996 Gigabytes

        }

    }

    logical_volumes {

        lvol0 {

            id = "t1KWaN-QBlu-I2GU-71cX-edje-u7A7-xp6z6k"

            status = "READ", "WRITE", "VISIBLE"

            segment_count = 1

        }

    }

}
```

```bash
# lvreduce -L4000 /dev/VolGroup01/lvol0
# lvreduce -L125 /dev/VolGroup01/lvol0
# lvreduce -L1000 /dev/VolGroup01/lvol0
```

减小逻辑卷的大小时存在风险。在减小大小之前，请务必对逻辑卷中的数据进行备份。有关如何执行备份的详情，请参阅第 17 章“备份、恢复与压缩”。

你可以使用 LVM 配置器来减小逻辑卷。按照以下步骤减小 `lvol1`：

+ 启动 LVM 配置器并转到卷组（Volume Groups） -> `VolGroup01` -> `VolGroup01` 逻辑视图（Logical View） -> `lvol1`。点击编辑属性（Edit Properties）。指定新大小并点击确定。

## 重命名逻辑卷

重命名逻辑卷会更改该逻辑卷的名称。以下示例将 `lvol0` 重命名为 `newvol0`。使用 `lvrename` 命令执行此操作：

```bash
# lvrename /dev/VolGroup01/lvol0 /dev/VolGroup01/newvol0
卷组 "VolGroup01" 中的 "lvol0" 已重命名为 "newvol0"
```

你可以使用 LVM 配置器重命名逻辑卷。按照以下步骤重命名 `lvol1`：

+ 启动 LVM 配置器并转到卷组（Volume Groups） -> `VolGroup01` -> `VolGroup01` 逻辑视图（Logical View） -> `lvol1`。点击编辑属性（Edit Properties）。指定新名称并点击确定。

## 删除逻辑卷

删除逻辑卷是一项破坏性任务。在删除目标逻辑卷之前，请确保已对该逻辑卷中的任何数据执行了备份。你需要卸载逻辑卷中的文件系统或禁用其中的交换分区（swap）。参阅第 14 章“文件系统与交换分区”了解如何卸载文件系统和禁用交换分区。

使用 `lvremove` 命令删除 `lvol0`：

```bash
# lvremove /dev/VolGroup01/lvol0
确定确定要移除活动卷“lvol0”吗 [y/n]: y
逻辑卷“lvol0”已成功删除
```

该命令会给出一个警告信息。

你可以使用 LVM 配置器删除逻辑卷。按照以下步骤删除 `lvol1`：

+ 启动 LVM 配置器并转到卷组（Volume Groups） -> `VolGroup01` -> `VolGroup01` 逻辑视图（Logical View） -> `lvol1`。点击删除逻辑卷（Remove Logical Volume），然后点击是进行删除。

## 移动物理区（Physical Extents）

如果需要从卷组中移除一个使用了某些物理区（PE）的物理卷，则位于这些 PE 中的数据需要移动到同一卷组内可用的物理卷（s）中。目标物理卷至少具有相同数量的空闲 PE。`pvmove` 命令用于用于此目的。以下示例将 PE 从 `/dev/sdc` 移动到卷组中任何其他物理卷的空闲 PE。如果你希望将 PE 移动到那里，请指定目标物理卷的名称。此操作可以在在线的忙碌逻辑卷上安全执行。

```bash
# pvmove /dev/sdc
/dev/sdc1: 已移动: 8.0%
/dev/sdc1: 已移动: 17.9%
...
/dev/sdc1: 已移动: 100.0%
```

执行 `vgdisplay` 和 `pvdisplay` 命令来移动 PE。你可以使用 LVM 配置器并按照以下步骤移动 `/dev/sdc1` PE：

+ 启动 LVM 配置器并转到卷组（Volume Groups） -> `VolGroup01` -> `VolGroup01` 物理视图（Physical View） -> `/dev/sdc` -> 分区 1（Partition 1）。在图形界面中突出显示区并点击从卷迁移选定的区（Migrate Selected Extent(s) from Volume）。点击是确认移动。

## 减小卷组

减小卷组会从中移除一个或多个物理卷。目前，`VolGroup01` 包含三个物理卷：`/dev/sdb`、`dev/sdc1` 和 `/dev/sdd`。使用 `vgreduce` 从中移除 `/dev/sdc1`。物理卷不能在使用。

```bash
# vgreduce VolGroup01 /dev/sdc1
已从卷组 "VolGroup01" 移除了 "dev/sdc1"
```

执行带有 `-v` 的 `vgdisplay` 以查看 `VolGroup01` 的更新信息。你可以使用 LVM 配置器减小卷组。按照以下步骤移除 `/dev/sdc1` 以减小 `VolGroup01`：

+ 启动 LVM 配置器并转到卷组（Volume Groups） -> `VolGroup01` -> `VolGroup01` 物理视图（Physical View） -> `/dev/sdc` -> 分区 1。点击从卷组移除卷（Remove Volume from Volume Group），然后点击是进行移除。

## 删除卷组

删除卷组会移除该卷组内的所有逻辑卷，然后移除该卷组。目前你在 `VolGroup01` 中有 `lvol1` 和 `aravol` 逻辑卷。使用带有 `-f` (`--force`) 的 `vgremove` 命令移除逻辑卷。

```bash
# vgremove -f VolGroup01
逻辑卷“lvol1”已成功删除
逻辑卷“aravl”已成功删除
卷组“VolGroup01”已成功删除
```
