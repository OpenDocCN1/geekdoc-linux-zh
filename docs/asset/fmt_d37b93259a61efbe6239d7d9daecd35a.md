
```bash
lvcreate -l 8755 /dev/vgu$vgnum ;为整个 vg 创建单一卷
```

我在此文件中使用 `set -x` 来开启跟踪。在调试 shell 程序时，我总是这样做，这样我可以在 shell 中看到执行的行。正在执行的行前面会显示 `"+"`，后面是你运行程序时通常看到的内容。程序会暂停以便查看已运行的内容。为了让此程序运行，必须稍微修改包含主磁盘的文件，并在每行开头添加卷组号。此外，我决定从包含主磁盘的文件调用程序，并一次操作一行。以下列表显示了更新后的 shell 程序（`vg.sh`），后面是卷组号，然后是每个卷组的主磁盘列表：

```bash
#vg.sh 01 c9t0d0 c9t0d1 c9t0d2 c8t0d0 c8td1
#vg.sh 02 c7t0d0 c7t0d1 c7t0d2 c100d0 c100d1
#vg.sh 03 c9t0d3 c9t0d4 c9t0d5 c8t0d3 c8t0d4
#vg.sh 04 c7t0d3 c7t0d4 c7t0d5 c100d3 c100d4
#vg.sh 05 c9t0d6 c9t0d7 c9t1d0 c8t0d6 c8t0d7
#vg.sh 06 c7t0d6 c7t0d7 c7t1d0 c100d6 c100d7
#vg.sh 07 c9t1d1 c9t1d2 c9t1d3 c8t1d1 c8t1d2
#vg.sh 08 c7t1d1 c7t1d2 c7t1d3 c101d1 c101d2
#vg.sh 09 c9t1d4 c9t1d5 c9t1d6 c8t1d4 c8t1d5
#vg.sh 10 c7t1d4 c7t1d5 c7t1d6 c101d4 c101d5
```

此文件行之间的 `read` 将暂停并等待你输入回车后再执行下一行。这样做是因为我可能决定运行几行，并想在行执行之间检查结果。

现在我们可以取消文件第一行的注释并输入文件名 `pri`，它将调用 `vg.sh` 并运行程序（你必须赋予文件适当权限，并确保 `vg.sh` 和 `pri` 都是可执行的）。我喜欢一次运行此类文件并检查创建的卷组。脚本编写为一次运行一行，但很容易修改为运行所有十行。

交替磁盘名称的工作要少得多。物理卷已经创建，卷组和单一逻辑卷已经在 `vg.sh` 中设置。我们将创建另一个名为 `vga.sh` ("a") 的交替脚本，其中我们将扩展卷组以包含每块磁盘的交替名称。该脚本所示：

```bash
#!/bin/ksh
set -x             开启跟踪
vgnum=$1           每行的第一项是卷组号
shift               移位以获取第一块磁盘

for i in $*         扩展卷以包含行中的所有五块磁盘
vgextend /dev/vgu$vgnum /dev/disk/$i
done
```

# 添加磁盘

此脚本仅执行扩展卷组 `vg` 以包含行中所有五块磁盘的任务。与 `pri` 文件类似，`alt` 文件调用脚本 `vga.alt`，如下所示：

```bash
#vga.sh 01 c10t8d c8t8d1 c8t8d2 c9t8d0 c9t8d1
#vga.sh 02 c10t8d0 c10t8d1 c10t8d2 c7t8d0 c7t8d1
#vga.sh 03 c8t8d3 c8t8d4 c8t8d5 c9t8d3 c8t8d4
#vga.sh 04 c10t8d3 c10t8d4 c10t8d5 c7t8d3 c7t8d4
#vga.sh 05 c9t8d6 c9t8d7 c9t1d0 c8t8d6 c8t8d7
#vga.sh 06 c7t8d6 c7t8d7 c7t1d0 c100d6 c100d7
#vga.sh 07 c9t1d1 c9t1d2 c9t1d3 c8t1d1 c8t1d2
#vga.sh 08 c7t1d1 c7t1d2 c7t1d3 c101d1 c101d2
#vga.sh 09 c9t1d4 c9t1d5 c9t1d6 c8t1d4 c8t1d5
#vga.sh 10 c7t1d4 c7t1d5 c7t1d6 c101d4 c101d5
```

以下 `vgdisplay` 输出显示了为卷组 `vgu01` 设置的磁盘，包含五个主磁盘和备用磁盘的组：

```bash
# vgdisplay /dev/vgu01 -v
```

| VG 名称 | /dev/vgu01 |

| :--- | :--- |

| VG 写权限 | read/write |

| VG 状态 | available |

| 最大 LV | 255 |

| 当前 LV | 1 |

| 开启 LV | 1 |

| 最大 PV | 16 |

| 当前 PV | 5 |

| 激活 PV | 5 |

| 每个 PV 的最大 PE | 1751 |

| VGDA | 10 |

| PE 大小 (Mbytes) | 4 |

| 总 PE | 8755 |

| 分配 PE | 8755 |

| 空闲 PE | 0 |

| 总 PVG | 0 |

| 总备用 PV | 0 |

| 输入备用 PV | 0 |

| --- 逻辑卷 --- | /dev/vgu01/lv0 |

| :--- | :--- |

| LV 名称 | available/syncd |

| LV 状态 | 35020 |

| LV 大小 (Mbytes) | 8755 |

| 当前 LE | 8755 |

| 分配 PE | 5 |

| 使用 PE | |

| --- 物理卷 --- | /dev/dsk/c9t0d0 |

| :--- | :--- |

| PV 名称 | /dev/dsk/c8t8d0Alternate |

| PV 状态 | available |

| 总 PE | 1751 |

| 空闲 PE | 0 |

| PV 名称 | /dev/dsk/c9t0d1 |

| :--- | :--- |

| PV 名称 | /dev/dsk/c8t8d1Alternate |

| PV 状态 | available |

| 总 PE | 1751 |

| 空闲 PE | 0 |

| PV 名称 | /dev/dsk/c9t0d2 |

| :--- | :--- |

| PV 名称 | /dev/dsk/c8t8d2Alternate |

| PV 状态 | available |

| 总 PE | 1751 |

| 空闲 PE | 0 |

## 添加磁盘

| PV 名称 | /dev/dsk/c8t0d0 |

| :--- | :--- |

| PV 名称 | /dev/dsk/c9t8d0Alternate Link |

| PV 状态 | available |

| 总 PE | 1751 |

| 空闲 PE | 0 |

| PV 名称 | /dev/dsk/c8t0d1 |

| PV 名称 | /dev/dsk/c9t8d1Alternate Link |

| PV 状态 | available |

| 总 PE | 1751 |

| 空闲 PE | 0 |

此 `vgdisplay` 输出中有一些值得关注点。首先是，同一块磁盘有主路径和备用路径，因为我们在此之前定义了它们。例如，卷组中的第一块磁盘是 `c9t0d0`，备用路径名称为 `c8t0d0`。接下来，卷组 `vgu01` 总共包含 8755 个 PE 或物理区（卷组的大小为 PE x PE 大小，在我们的案例中为 8755 x 4MB）。

我们还应该检查 `vgu01` 上的一个逻辑卷，名为 `lvol1`。我们可以使用 `lvdisplay` 命令检查该逻辑卷的参数，如下例所示：

```bash
# lvdisplay -v /dev/vgu01/lvol1*
-- 逻辑卷 --
LV Name /dev/vgu01/lvol1
VG Name /dev/vgu01
LV Permission read/write
LV Status available/synced
Mirror copies 0
Consistency Recovery
Schedule parallel
LV Size (Mbytes) 35020
Current LE 8755
Allocated PE 8755
Stripes 0
Stripe Size (Kbytes) 0
Bad block on
Allocation strict
IO Timeout (Seconds) default
-- 逻辑卷分布 --
PV Name LE on PV PE on PV
/dev/dsk/c9t0d0 1751 1751
/dev/dsk/c9t0d1 1751 1751
/dev/dsk/c9t0d2 1751 1751
```

![](img/6969df54e516231f8e64fd1177ac1127_450_0.png)

![](img/6969df54e516231f8e64fd1177ac1127_450_1.png)

# 第 8 章 逻辑卷管理器与 Veritas 卷管理器
