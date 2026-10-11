
```
PV Name /dev/dsk/c0td0
PV Status available
Total PE 1023
Free PE 679
```

PV Name `/dev/dsk/c0t5d`

PV Status available

Total PE 1023

Free PE 679

## F1 - lvdisplay

使用 `lvdisplay` 查看详细逻辑卷。注意这些逻辑卷都是镜像，且都处于“current”状态。列表中只显示了 `lvol1` 和 `lvol2`。未显示 `lvol3`。

```
# lvdisplay -v /dev/vg00/lvol*
```

-- 逻辑卷

LV Name               `/dev/vg00/lv1`

VG Name               `/dev/vg00`

LV Permission         read/write

Mirror copies         available/synced

Consistency Recovery  MWC

Schedule              parallel

LV Size (Mbytes)      23

Current LE            23

Allocated PE          46

Stripes               0

Stripe Size (Kbytes)  off

Bad block             strict/contiguous

Allocation

-- 逻辑卷分布

PV Name               LE on PV

`/dev/dck/c0t5d`        23        23

`/dev/dck/c0t5d`        23        23

-- 逻辑事件

| LE PO | PE1 Status 12 | PE2 Status 2 |
|---|---|---|
| 0000 | 0000 | `/dev/dck/c0t5d` | 0000 current |
| 0001 | 0001 | `/dev/dck/c0t5d` | 0001 current |
| 0002 | 0002 | `/dev/dck/c0t5d` | 0002 current |
| 0003 | 0003 | `/dev/dck/c0t5d` | 0003 current |
| 0004 | 0004 | `/dev/dck/c0t5d` | 0004 current |
| 0005 | 0005 | `/dev/dck/c0t5d` | 0005 current |
| 0006 | 0006 | `/dev/dck/c0t5d` | 0006 current |
| 0007 | 0007 | `/dev/dck/c0t5d` | 0007 current |
| 0008 | 0008 | `/dev/dck/c0t5d` | 0008 current |
| 0009 | 0009 | `/dev/dck/c0t5d` | 0009 current |
| 0010 | 0010 | `/dev/dck/c0t5d` | 0010 current |
| 0011 | 0011 | `/dev/dck/c0t5d` | 0011 current |
| 0012 | 0012 | `/dev/dck/c0t5d` | 0012 current |
| 0013 | 0013 | `/dev/dck/c0t5d` | 0013 current |
| 0014 | 0014 | `/dev/dck/c0t5d` | 0014 current |
| 0015 | 0015 | `/dev/dck/c0t5d` | 0015 current |
| 0016 | 0016 | `/dev/dck/c0t5d` | 0016 current |
| 0017 | 0017 | `/dev/dck/c0t5d` | 0017 current |
| 0018 | 0018 | `/dev/dck/c0t5d` | 0018 current |

# 重配置某些磁盘 - 使用某些逻辑卷命令的示例

```
Current LE 125
Allocated PE 250
Stripes 0
Stripe Size (Kbytes) 0
Bad Block off
Allocation strict/contiguous
```

--- 逻辑卷分布 ---

| PV Name | LE on PV | PE on PV |
| :--- | :--- | :--- |
| `/dev/dak/ct06d0` | 125 | 125 |
| `/dev/dak/ct05d0` | 125 | 125 |

--- 逻辑区区 ---

| LE | PE1 | Status 1 | PE2 | Status 2 |
| :--- | :--- | :--- | :--- | :--- |
| 0000 | `/dev/dak/ct06d0` | 0023 current | `/dev/dak/ct05d0` | 0023 current |
| 0001 | `/dev/dak/ct06d0` | 0024 current | `/dev/dak/ct05d0` | 0024 current |
| 0002 | `/dev/dak/ct06d0` | 0025 current | `/dev/dak/ct05d0` | 0025 current |
| 0003 | `/dev/dak/ct06d0` | 0026 current | `/dev/dak/ct05d0` | 0026 current |
| 0004 | `/dev/dak/ct06d0` | 0027 current | `/dev/dak/ct05d0` | 0027 current |
| 0005 | `/dev/dak/ct06d0` | 0028 current | `/dev/dak/ct05d0` | 0028 current |
| 0006 | `/dev/dak/ct06d0` | 0029 current | `/dev/dak/ct05d0` | 0029 current |
| 0007 | `/dev/dak/ct06d0` | 0030 current | `/dev/dak/ct05d0` | 0030 current |
| 0008 | `/dev/dak/ct06d0` | 0031 current | `/dev/dak/ct05d0` | 0031 current |
| 0009 | `/dev/dak/ct06d0` | 0032 current | `/dev/dak/ct05d0` | 0032 current |
| 0010 | `/dev/dak/ct06d0` | 0033 current | `/dev/dak/ct05d0` | 0033 current |
| 0011 | `/dev/dak/ct06d0` | 0034 current | `/dev/dak/ct05d0` | 0034 current |
| 0012 | `/dev/dak/ct06d0` | 0035 current | `/dev/dak/ct05d0` | 0035 current |
| 0013 | `/dev/dak/ct06d0` | 0036 current | `/dev/dak/ct05d0` | 0036 current |
| 0111 | `/dev/dak/ct06d0` | 0134 current | `/dev/dak/ct05d0` | 0134 current |
| 0112 | `/dev/dak/ct06d0` | 0135 current | `/dev/dak/ct05d0` | 0135 current |
| 0113 | `/dev/dak/ct06d0` | 0136 current | `/dev/dak/ct05d0` | 0136 current |
| 0114 | `/dev/dak/ct06d0` | 0137 current | `/dev/dak/ct05d0` | 0137 current |
| 0115 | `/dev/dak/ct06d0` | 0138 current | `/dev/dak/ct05d0` | 0138 current |
| 0116 | `/dev/dak/ct06d0` | 0139 current | `/dev/dak/ct05d0` | 0139 current |
| 0117 | `/dev/dak/ct06d0` | 0140 current | `/dev/dak/ct05d0` | 0140 current |
| 0118 | `/dev/dak/ct06d0` | 0141 current | `/dev/dak/ct05d0` | 0141 current |
| 0119 | `/dev/dak/ct06d0` | 0142 current | `/dev/dak/ct05d0` | 0142 current |
| 0120 | `/dev/dak/ct06d0` | 0143 current | `/dev/dak/ct05d0` | 0143 current |
