
**表 8.4 format 命令的子命令和子菜单（续）**

| 子命令或子菜单 | 说明 |
|---|---|
| `volname` | 为所选磁盘定义八字符卷名 |
| `!cmd` | 使用用户的 shell 执行 cmd，然后返回到 *format* 命令 |
| `quit` | 退出 *format* 命令 |

当 format 命令启动时，它会列出可用的磁盘驱动器，然后由你选择一个。字符串 *format>* 用作命令提示符。

以下示例演示了启动 format 命令：

```text
# format
Searching for disks...done

AVAILABLE DISK SELECTIONS:
        0.  c0t0d0 <DEFAULT cyl 38767 alt 2 hd 16 sec 63>
            /pci@0,0/pci-ide@0,1/ide@0/cmdk@0,0
        1.  c0t1d0 <DEFAULT cyl 1019 alt 2 hd 255 sec 63>
            /pci@0,0/pci-ide@0,1/ide@0/cmdk@1,0
Specify disk (enter its number): 0
selecting c0t0d0
Controller working list found
[disk formatted, defect list found]
Warning: Current Disk has mounted partitions.

FORMAT MENU:
        disk        - select a disk
        type        - select (define) a disk type
        partition   - select (define) a partition table
        current     - describe the current disk
        format      - format and analyze the disk
        fdisk       - run the fdisk program
        repair      - repair a defective sector
        show        - translate a disk address
        label       - write label to the disk
        analyze     - surface analysis
        defect      - defect list management
        backup      - search for backup labels
        verify      - read and display labels
        save        - save new disk/partition definitions
        volname     - set 8-character volume name
        !<cmd>      - execute <cmd>, then return
        quit
format>
```

![](img/b957f979417d9f16274c2eb52c8f2c9f_209_0.png)

对 *format* 命令的基本理解和一般使用是考试目标。请熟悉 *format* 子命令和子菜单及其用法。

以下示例使用了几个 **format** 子命令：**disk**、**volname**、**verify** 和 **current**。更多信息请参阅 format(1M) 手册页：

```text
format> disk

AVAILABLE DISK SELECTIONS:
       0. c0d0 <DEFAULT cyl 38767 alt 2 hd 16 sec 63>
          /pci@0,0/pci-ide@0,1/ide@0/cmdk@0,0
       1. c0d1 <DEFAULT cyl 1019 alt 2 hd 255 sec 63> solaris7
          /pci@0,0/pci-ide@0,1/ide@0/cmdk@1,0
Specify disk (enter its number) [0]: 0
selecting c0d0
Controller working list found
[disk formatted, defect list found]
Warning: Current Disk has mounted partitions.

format> volname
Enter 8-character volume name (remember quotes)[" "]: "solaris8"
Ready to label disk, continue? y

format> verify

Primary label contents:

Volume name = <solaris8>
ascii name  = <DEFAULT cyl 38767 alt 2 hd 16 sec 63>
pcyl        = 38769
ncyl        = 38767
acyl        = 2
bcyl        = 0
nhead       = 16
nsect       = 63
Part      Tag  Flag     Cylinders        Size            Blocks
  0      root  wm       1044 - 31520    14.65GB (31047/0/0) 30720816
  1      swap  wu          3 - 1043    512.37MB (1041/0/0)   1049328
  2      backup wm          0 - 38767   18.63GB (38768/0/0) 39078144
  3 unassigned wm          0               0  (0/0/0)              0
  4 unassigned wm          0               0  (0/0/0)              0
  5 unassigned wm          0               0  (0/0/0)              0
  6 unassigned wm          0               0  (0/0/0)              0
  7       home wm      31521 - 31927  200.32MB (407/0/0)      410256
  8       boot wu          0               0  (1/0/0)           1008
  9 alternates wm          0 -     2    0.98MB (2/0/0)          2016

format> current
Current Disk = c0d0: solaris8
<DEFAULT cyl 38767 alt 2 hd 16 sec 63>
/pci@0,0/pci-ide@0,1/ide@0/cmdk@0,0

format>
```

## 分区子菜单

在 **format** 的三个子菜单（分区、分析和缺陷）中，分区子菜单最常用。你不仅可以使用“分区”子菜单查看和修改所选磁盘的分区表，还可以创建新的分区表。

![](img/b957f979417d9f16274c2eb52c8f2c9f_211_0.png)

对 **format** “分区”子菜单的基本理解和一般使用是考试目标。请熟悉“分区”子菜单命令及其预期用途。

表 8.5 描述了“分区”子菜单上可用的子命令。

| 子命令 | 描述 |
|---|---|
| **0** 到 **7** | 修改与分区 0 到 7 关联的标记、标志、起始柱面和大小。 |
| **select** | 选择一个分区表。 |
| **modify** | 修改分区表。从当前分区表或未分配分区中的所有磁盘空间开始。（大的未分配分区称为“free hog”。） |
| **name** | 为当前分区表指定名称。 |
| **print** | 显示当前分区表。 |
| **label** | 将当前分区表和标签写入磁盘。 |
| **!cmd** | 使用用户的 shell 执行 **cmd**，然后返回到 **format** 命令。 |
| **quit** | 返回到 **format** 菜单。 |

以下示例使用“分区”子菜单来命名分区表、选择分区表，并显示当前选定的表：

```text
format> partition

PARTITION MENU:
      0       - change '0' partition
      1       - change '1' partition
      2       - change '2' partition
      3       - change '3' partition
      4       - change '4' partition
      5       - change '5' partition
      6       - change '6' partition
      7       - change '7' partition
select - select a predefined table
modify - modify a predefined partition table
name   - name the current table
print  - display the current table
label  - write partition map and label to the disk
!<cmd> - execute <cmd>, then return
quit   - quit
```

```text
partition> name
Enter table name (remember quotes): 'solaris 8'
```

```text
partition> select
        0. solaris 8
Specify table (enter its number)[0]: 0
```

```text
partition> print
Volume: solaris8
Current partition table (solaris 8):
Total disk cylinders available: 1019 + 2 (reserved cylinders)
```

| 分区 | 标记 | 标志 | 柱面 | 大小 | 块 |
|---:|---|---|---|---|---:|
| 0 | root | wm | 3 - 283 | 2.15GB (281/0/0) | 4514265 |
| 1 | usr | wm | 284 - 326 | 337.30MB (43/0/0) | 690795 |
| 2 | backup | wm | 0 - 1018 | 7.81GB (1019/0/0) | 16370235 |
| 3 | var | wm | 327 - 454 | 1004.06MB (128/0/0) | 2056320 |
| 4 | swap | wm | 455 - 474 | 156.88MB (20/0/0) | 321300 |
| 5 | unassigned | wm | 475 - 755 | 2.15GB (281/0/0) | 4514265 |
| 6 | usr | wm | 756 - 890 | 1.03GB (135/0/0) | 2168775 |
| 7 | home | wm | 891 - 1018 | 1004.06MB (128/0/0) | 2056320 |
| 8 | boot | wu | 0 - 0 | 7.84MB (1/0/0) | 16065 |
| 9 | alternates | wu | 1 - 2 | 15.69MB (2/0/0) | 32130 |

```text
partition>
```

## 练习题

### 问题 1

以下哪些活动可以使用 **format** 命令执行？（请选择所有适用项。）

- ☐ a. 显示分区表。
- ☐ b. 修改分区表中的单个分区。
- ☐ c. 替换整个分区表。
- ☐ d. 将分区表从一个磁盘复制到另一个磁盘。

答案 a、b 和 c 正确。使用 **format** 命令，你可以显示分区表、修改分区表中的单个分区，以及替换整个分区表。虽然可以创建、保存分区表并在另一张磁盘上使用，但 **format** 命令不提供将表从一张磁盘复制到另一张磁盘的方法。因此，答案 d 不正确。

### 问题 2

输入可用于显示文件系统挂载日期和时间的命令。

正确答案是 **mount**。

### 问题 3

哪个命令支持热插拔的动态重新配置？

- ○ a. **reconfig**
- ○ b. **configadm**
- ○ c. **cfgadm**

答案 c 正确。**cfgadm** 命令支持热插拔的动态重新配置。答案 a 和 b 中的命令不存在。

![](img/b957f979417d9f16274c2eb52c8f2c9f_213_0.png)
