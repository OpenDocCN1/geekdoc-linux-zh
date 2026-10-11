
这可能不是你想要的结果。如“0”所示，主 dump 设备是`/dev/dsk/c0t6d0`，如“1”所示，次要 dump 设备是`/dev/dsk/c0t5d0`。我们可以选择重新执行此操作。让我们先继续对`/dev/vg00`上的`lvol`进行镜像，稍后再处理 dump 设备。

# F19

让我们现在使用`lvextend`扩展`vg00`中所有卷以用于一个镜像。

```
# lvextend -m 1 /dev/vg00/lvol1 /dev/dsk/c1t3d0
The newly allocated mirrors are now being synchronized.
This operation will take some time. Please wait . . .
Logical volume "/dev/vg00/lvol1" has been successfully extended.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
```

将以下内容放入`/tmp/mirror`并运行。`lvol1`之前已扩展：`lvol2`是交换分区，无需扩展：

```
lvextend -m 1 /dev/vg00/lvol3 /dev/dsk/c1t3d0
lvextend -m 1 /dev/vg00/lvol4 /dev/dsk/c1t3d0
lvextend -m 1 /dev/vg00/lvol5 /dev/dsk/c1t3d0
lvextend -m 1 /dev/vg00/lvol6 /dev/dsk/c1t3d0
lvextend -m 1 /dev/vg00/lvol7 /dev/dsk/c1t3d0
```

```
The newly allocated mirrors are now being synchronized.
This operation will take some time.
Please wait.... Logical volume "/dev/vg00/lvol2" has been successfully extended.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
```

# F20

让我们现在使用`lvdisplay`验证镜像是否已到位（仅显示`lvol1`和`lvol2`）。

```
# lvdisplay -v /dev/vg00/lvol* | more

--- Logical volumes ---
LV Name                 /dev/vg00/lvol1
VG Name                 /dev/vg00
LV Permission            read/write
LV Status                available/syncd
Mirror copies            1
Consistency Recovery     mwc
Schedule                 parallel
LV Size [Mbytes]         52
Current LE               23
Allocated PE             46
Stripes                  0
Stripe Size [Kbytes]     0
Bad Block                off
Allocation               strict/contiguous

--- Distribution of logical volume ---
PV Name        LE on PV  PE on PV
/dev/dsk/c0t6d0   23     23
/dev/dsk/c1t3d0   23     23

--- Logical extents ---
LE          PV1            PE1   Status
0000 /dev/dsk/c0t6d0   0000 current   /dev/dsk/c1t3d0 0000 current
0001 /dev/dsk/c0t6d0   0001 current   /dev/dsk/c1t3d0 0001 current
0002 /dev/dsk/c0t6d0   0002 current   /dev/dsk/c1t3d0 0002 current
0003 /dev/dsk/c0t6d0   0003 current   /dev/dsk/c1t3d0 0003 current
```

您可以从此列表中看出，`c0t6d0`在`c1t3d0`上进行了镜像。

# F21

重启系统以确认所有更改已生效。

重启后，执行以下操作以创建转储。对于 `^b`起作用，键必须处于“Service”位置（必须位于服务器上的系统控制台才能使其起作用）。

- 使用 `^b`获取`CM>`提示符。
- 在`CM>`提示符下使用`tc`命令创建核心转储。

# F22

系统在核心转储后会自动重启。使用以下命令将核心转储保存到磁带上。即使核心转储位于转储逻辑卷中而不是`/var/adm/crash`目录中，也需要`/var/adm/crash`文件名。

```
# savecore -t /dev/rmt/0m /var/adm/crash
```

# F23

然后使用`savecore -xt`和目录名来提取核心转储。如果您没有足够的空间容纳核心转储，或者想要更彻底的检查，您可以致电要求 HP 响应中心验证保存到磁带是否成功。

```
# savecore -xt /dev/rmt/0m /var/adm/crash
```

核心转储的空间需求是从转储的末尾向前计算的。因此，大约 1.5 GBytes 被写入转储逻辑卷，然后大约 600 MBytes 被写入`lvol2`。

### 交换转储优先级的可选步骤

该步骤使用`lvrmb` boot 从`/dev/srg00`中移除所有启动定义（包括 swap 和 dump），然后使用`lvrlnboot`重新创建它们。之所以需要这样做，是因为`lv012`是主要转储逻辑卷 (0)，而 dump 是次要转储逻辑卷 (1)。

必须重启系统才能使这些更改生效。图 9-16 展示了完成此可选步骤所需的步骤。

![Figure 9-16 更改转储优先级的步骤（可选）](img/eff8b9287a5f38c5adf538f24aacf29e_535_0.png)

## 图 9-16 更改转储优先级的步骤（可选）

- F24: 使用`lvmboot`完全从`vg00`中移除启动区域。

```
# lvmboot -r /dev/vg00
```

- F25: 使用`lvmboot`验证启动区域是否已被移除。

```
# lvmboot -v
```

卷组`/dev/vg00`的启动定义：启动数据区域为空。

- F26: 使用`lvmboot`将根逻辑卷分配给`/dev/vg00`上的`lv0l1`。

```
# lvmboot -r lv0l1 /dev/vg00
```

- F27: 将交换空间（swap）分配给`/dev/vg00`上的`lv0l2`。

```
# lvmboot -s lv0l2 /dev/vg00
```

```
# swapinfo
```

```
     Kb        Kb        Kb     PCT START/    Kb
TYPE    AVAIL   USED     FREE    USED LIMIT RESERVE PRI NAME
dev     512000      0    512000   0%    0        -   1 /dev/vg00/lv0l2
reserve -      23144   -23144             -
memory  1671008 27328  1643680  2%
```

- F28: 将转储分配给`/dev/vg00`上的逻辑卷`dump`。

```
# lvmboot -d dump /dev/vg00
```

- F29: 将次要转储设备指定为`lv0l2`（主要交换空间），位于`lv0l2`上。

```
# lvmboot -d lv0l2 /dev/vg00
```

- F30: 运行`lvmboot`以确认转储和交换空间已正确配置，优先级在 2 GByte 磁盘`c0t5d0`上为 "0"，在`c0t6d0`上为 "1"。
