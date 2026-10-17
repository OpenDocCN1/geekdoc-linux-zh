
### ReiserFS 调试示例

```bash
mount -t reiserfs /dev/hdb1 /reiserfs
cd /reiserfs
cp /etc/fstab .
ls -l
```
```
total 6
drwxr-xr-x     4 root     root     104 Dec 19 06:26 .
drwxr-xr-x     30 root     root     1824 Dec 20 12:10 ..
-rw-r-- --      1 root     root     948 Dec 19 06:26 fstab
```

```bash
cd ..
umount /reiserfs
debugreiserfs d /dev/hdb1
```
```
debugreiserfs 3.6.4

Filesystem state: consistent

Reiserfs super block in block 16 on 0x341 of format 3.6
with standard journal
Count of blocks on the device: 1004054
Number of bitmaps: 31
Blocksize: 4096
Free blocks (count of blocks - used [journal, bitmaps,
data, reserved] blocks): 995812
Root block: 8211
Filesystem is clean
Tree height: 2
Hash function used to sort names: "r5"
ObjectId map size 2, max 972
Journal parameters:
Device [0x0]
Magic [0x431098f2]
Size 8193 blocks (including 1 for journal header)
(first block 18)
Max transaction length 1024 blocks
Max batch size 900 blocks
Max commit age 30
Blocks reserved by journal: 0
Fs state field: 0x0
sb_version: 2
inode generation number: 0
UUID: 1f0d2fd3-6fd6-412c-982d-4a16f0a37de9
LABEL:
Set flags in SB:
ATTRIBUTES CLEAN
===============================================================
```

```
LEAF NODE (8211) contains level=1, nr_items=6,
free_space=2692 rdeen (real items 6)
```

| 类型 | 长度 | 标志/空间 | 位置 | 格式 | fsck | 键 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | 1 2 0x0 SD (0), len 44, location 4052 entry count 0, fsck need 0, format new | | | | | |
| | (NEW SD), mode drwxr-xr-x, size 104, nlink 4, mtime 12/19/2003 06:26:51 blocks 1, uid 0 | | | | | |
| 1 | 1 2 0x1 DIR (3), len 104, location 3948 entry count 4, fsck need 0, format old | | | | | |
| | : Name length Object key Hash Gen number | | | | | |
| | 0: "." ( 1) [1 2] 0 1, loc 96 | | | | | |
| | 1: ".." ( 2) [0 1] 0 2, loc 88 | | | | | |
| | 2: "fstab" ( 5) [2 4] 293528832 0, loc 80 | | | | | |
| | 3: ".reiserfs_priv" ( 14) [2 3] 1105744768 0, loc 64 | | | | | |
| 2 | 2 3 0x0 SD (0), len 44, location 3904 entry count 65535, fsck need 0, format new | | | | | |
| | (NEW SD), mode drwx, size 48, nlink 2, mtime 12/19/2003 06:26:18 blocks 1, uid 0 | | | | | |
| 3 | 2 3 0x1 DIR (3), len 48, location 3856 entry count 2, fsck need 0, format old | | | | | |
| | : Name length Object key Hash Gen number | | | | | |
| | 0: "." ( 1) [2 3] 0 1, loc 40 | | | | | |
| | 1: ".." ( 2) [1 2] 0 2, loc 32 | | | | | |
| 4 | 2 4 0x0 SD (0), len 44, location 3812 entry count 65535, fsck need 0, format new | | | | | |
| | (NEW SD), mode -rw-r--r--, size 948, nlink 1, mtime 12/19/2003 06:26:51 blocks 8, uid 0 | | | | | |
| 5 | 2 4 0x1 DRCT (2), len 952, location 2860 entry count 65535, fsck need 0, format new | | | | | |

======================================================================

File system uses 0 internal + 1 leaves + 0 unformatted

nodes = 1 blocks

首先显示文件系统的超级块信息，然后显示叶节点 `8211`。文件 `fstab` 的高亮信息显示了一些常见的 inode 信息。权限为 `rw-r--`，大小为 `948`，修改时间为 `12/19/2003 06:26:51`。

`debugreiserfs` 的手册页包含了关于如何显示 ReiserFS 关键结构的信息。要显示 `debugreiserfs` 的手册页，请键入以下命令：

```bash
man debugreiserfs
```

#### XFS 文件布局

`xfs_db` 允许检查 XFS 文件系统的结构。`xfs_db` 工具以设备作为参数。`xfs_db` 手册页包含有关如何显示 XFS 数据结构的信息。

本节展示了如何在 XFS 系统上显示一个 inode。

XFS 文件系统位于设备 `/dev/hda5` 上。

```bash
mount -t xfs /dev/hda5 /xfs
cd /xfs
```

将位于 `/etc` 目录中的 `fstab` 文件复制到 XFS 文件系统上。

```bash
cp /etc/fstab .
ls -l
```
```
total 12
drwxr-xr-x   2 root root     18 Dec  8 10:57 .
drwxr-xr-x   24 root root   4096 Dec  8 10:54 ..
-rw-r--r--   1 root root   948 Dec  8 10:57 fstab
```

要查看文件的 inode，需要其 inode 号。使用 `ls` 命令并加上 `-i` 选项来确定该号码。在以下示例中，`fstab` 文件的 inode 号是 `131`。

```bash
ls -i
    128 .       128 ..        131 fstab
cd ..
umount /xfs
```

`xfs_db` 中查看 inode 的选项是 `inode` 命令。`inode` 命令使用 inode 号作为参数。要打印关于该 inode 的文件系统信息，请使用 `p` 命令。
