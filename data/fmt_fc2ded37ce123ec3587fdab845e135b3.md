
```bash
#!/usr/bin/ksh
echo "列表显示: lvdisplay -v $ARCHDIR/display_v.txt"
for lv in lvdisplay -v | grep 'LV Name' | awk '{print $3}'
do
  entry=$(lvdisplay -v | grep '$lv')
  if [ ! -z "$entry" ]; then
    echo "$lv 已挂载，来自 bdf:$entry"
  else
    echo "$lv 未挂载"
  fi
  echo "正在处理 30 行逻辑卷信息: lvdisplay -v $lv -30"
  echo "逻辑卷是:$lv"
  lvdisplay -v $lv >>$ARCHDIR/display_v.txt
done
```

我将输出重定向到 `audvis.out`，如下列表所示。仅列出了前几个逻辑卷。

# 854

## 第8章 HP-UX 系统审计

```
--- Logical extents ---
| LV | PV1 | PE1 | Status 1 |
| :--- | :--- | :--- | :--- |
| 0000/dev/disk/c0t6d | 0000 | current |
| 0001/dev/disk/c0t6d | 0001 | current |
| 0002/dev/disk/c0t6d | 0002 | current |
| 0003/dev/disk/c0t6d | 0003 | current |
| 0004/dev/disk/c0t6d | 0004 | current |
| 0005/dev/disk/c0t6d | 0005 | current |
| 0006/dev/disk/c0t6d | 0006 | current |
| 0007/dev/disk/c0t6d | 0007 | current |
```

>>> `/dev/vg00/lvol16` mounted, line from bdf:
`/dev/vg00/lvol16 1025617 605780 317275 66% /usr`
>>> documenting first 30 lines of lvm information by: `ldisplay -v /dev/vg00/lvol16 -head -30`
the logical volume is:`/dev/vg00/lvol16`
---
LV Size (Mbytes) 1024
Current LE 256
Allocated PE 256
Stripes 0
Stripe Size (Kbytes) 0
Bad block on
Allocation strict
----- Distribution of logical volume ---
| PV Name | LE on PV | PE on PV |
| :--- | :--- | :--- |
| `/dev/disk/c0t6d` | 36 | 36 |
| `/dev/disk/c0t5d` | 220 | 220 |
----- Logical extents ---
| LV | PV1 | PE1 | Status 1 |
| :--- | :--- | :--- | :--- |
| 0000/dev/disk/c0t6d | 0471 | current |
| 0001/dev/disk/c0t6d | 0472 | current |
| 0002/dev/disk/c0t6d | 0473 | current |
| 0003/dev/disk/c0t6d | 0474 | current |
| 0004/dev/disk/c0t6d | 0475 | current |
| 0005/dev/disk/c0t6d | 0476 | current |
| 0006/dev/disk/c0t6d | 0477 | current |

>>> `/dev/vg00/lvol14` mounted, line from bdf:
`/dev/vg00/lvol14 1025617 667722 255333 72% /opt`
>>> documenting first 30 lines of lvm information by: `ldisplay -v /dev/vg00/lvol14 -head -30`
the logical volume is:`/dev/vg00/lvol14`
---
LV Size (Mbytes) 1024
Current LE 256
Allocated PE 256
Stripes 0
Stripe Size (Kbytes) 0

Bad block on
Allocation strict
--- Distribution of logical volume ---
| PV Name | LE on PV | PE on PV |
| :--- | :--- | :--- |
| `/dev/dsk/c0t6d0` | 256 | 256 |
--- Logical extents ---
| LE | PV1 | PE1 | Status 1 |
| :--- | :--- | :--- | :--- |
| 0000 /dev/dsk/c0t6d0 | 0165 | current |
| 0001 /dev/dsk/c0t6d0 | 0166 | current |
| 0002 /dev/dsk/c0t6d0 | 0167 | current |
| 0003 /dev/dsk/c0t6d0 | 0168 | current |
| 0004 /dev/dsk/c0t6d0 | 0169 | current |
| 0005 /dev/dsk/c0t6d0 | 0170 | current |
| 0006 /dev/dsk/c0t6d0 | 0171 | current |
| 0007 /dev/dsk/c0t6d0 | 0172 | current |

## 补丁

以下脚本 `audpatch.sh` 用于生成系统上已安装的补丁列表。该程序会对补丁进行分类并列出。

```bash
#!/bin/ksh
echo "\nThis is a list of patches installed on system 'hostname'\n"
swlist > swlist.out

WORD_COUNT=$(cat swlist.out | grep PHKL | wc -l)
echo "\nNumber of kernel patches on 'hostname' is $WORD_COUNT."
echo "\nKernel patches : \n"
echo " Patch Number \t\t Revision \t Description"
cat swlist.out | grep PHKL

WORD_COUNT=$(cat swlist.out | grep PHCO | wc -l)
echo "\nNumber of command patches on 'hostname' is $WORD_COUNT."
echo "\nCommand patches : \n"
echo " Patch Number \t\t Revision \t Description"
cat swlist.out | grep PHCO

WORD_COUNT=$(cat swlist.out | grep PHNE | wc -l)
echo "\nNumber of network patches on 'hostname' is $WORD_COUNT."
echo "\nNetwork patches : \n"
echo " Patch Number \t\t Revision \t Description"
cat swlist.out | grep PHNE

WORD_COUNT=$(cat swlist.out | grep PHSS | wc -l)
echo "\nNumber of subsystem patches on 'hostname' is $WORD_COUNT."
echo "\nSubsystem patches : \n"
echo " Patch Number \t\t Revision \t Description"
cat swlist.out | grep PHSS
```

以下是运行 `audpatch.sh` 得到的输出：这是 huxpl 系统上安装的补丁列表。huxpl 的内核补丁数量为 25。

| Patch Number | Revision | Description |

| :--- | :--- | :--- |

| PKHL 10258 | B.10.00.00.AA | exec, ptrace, large buffer |

| PKHL 10443 | B.10.00.00.AA | SCSI Passthrough cumulative patch |
