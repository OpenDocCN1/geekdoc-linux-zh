

下一步是卸载软盘设备并使用 mkfs 再次对其进行格式化；然后重新挂载软盘设备。

```bash
# umount /mnt/floppy
# mkfs /dev/fd0
# mount /dev/fd0 /mnt/floppy
```

接下来，将一个文件复制到软盘设备，然后使用 debugfs 实用程序查看该文件系统的文件信息。在下面的示例中，该文件名为 fstab。fstab 的 inode 为 12。在该示例中，debugfs 中的 -i 选项用于收集文件系统信息，而 stat 选项则用于显示文件 fstab 的 inode。

```bash
# cp /etc/fstab /mnt/floppy/fstab
# umount /mnt/floppy
# debugfs /dev/fd0
```

```text
debugfs: ls -l
1.32 (09-Nov-2002)
debugfs:
        2  40755 (2) 0 0    1024  9-Jun-2003 19:43 .
        2  40755 (2) 0 0    1024  9-Jun-2003 19:43 ..
       11  40700 (2) 0 0   12288  9-Jun-2003 19:06 lost+found
       12 100644 (1) 0 0     697  9-Jun-2003 19:43 fstab
```

```text
debugfs: stat <12>
debugfs: Inode: 12  Type: regular   Mode:  0644
Flags: 0x0   Generation: 295695
User:       0   Group:     0   Size: 697
File ACL: 0   Directory ACL: 0
Links: 1   Blockcount: 2
Fragment:   Address: 0     Number: 0     Size: 0
ctime: 0x3ee537a8 Mon Jun  9 19:43:04 2003
atime: 0x3ee537a8 Mon Jun  9 19:43:04 2003
mtime: 0x3ee537a8 Mon Jun  9 19:43:04 2003
BLOCKS:
(0):41
TOTAL: 1
```

输出中显示的 Fragment（片段）信息用于确定文件是否连续。碎片化的文件无法提供最佳性能。然而，示例中的 fstab 文件并未被碎片化。

最后一步是卸载软盘设备。

```bash
# umount /mnt/floppy
```

## 日志文件系统 (JFS) 文件布局

jfs_debugfs 实用程序可用于检查日志文件系统（JFS）的结构。jfs_debugfs 实用程序仅接受设备作为参数。jfs_debugfs 的手册页（man page）包含了关于如何显示 JFS 数据结构的信息。本节展示了如何收集文件系统部分关键结构的信息。

在示例中，/dev/hda1 设备包含了要显示其结构的 JFS 文件系统。

```bash
# jfs_debugfs /dev/hda1
```

jfs_debugfs 的 su 选项可用于显示超级块。以下示例是来自某系统的样本输出：

```text
>su

[1] s_magic: 'JFS1'		[15] s_ait2.addr1:	0x00

[2] s_version: 1			[16] s_ait2.addr2:	0x00000097

[3] s_size: 0x0000000000007fa970	 s_ait2.address:	151

[4] s_bsize: 4096		[17] s_logdev:		0x00000000

[5] s_l2bsize: 12		[18] s_logserial:		0x00000000

[6] s_l2bfactor:3		[19] s_logpxd.len:		4352

[7] s_ppsize: 512		[20] s_logpxd.addr1:	0x00

[8] s_l2ppsize: 9		[21] s_logpxd.addr2:	0x000fff581

[9] pad: Not Displayed				 s_logpxd.address:	1045889

[10] s_agsize:0x00002000	[22] s_fsbkp. len:		83

[11] s_flag: 0x10200900		[23] s_fsbkp. addr1:	0x00

JFS_LINUX			[24] s_fsbkp. addr2:	0x000ff52e

JFS_COMMIT	JFS_GROUPCOMMIT	 s_fsbkp. address:	1045806

JFS_INLINELOG		[25] s_time. tv_ sec:	0x3f002d2d

		[26] s_time. tv_ msec:	0x00000000

		[27] s_fpack:		' '

[12] s_state: 0x00000000

FM_CLEAN

[13] s_compress:	0

[14] s_ait2.len:		4

display_super: [m]odify or e[x]it: x
```

以下示例使用 /jfs 作为挂载点，挂载文件系统，并复制 fstab 文件，从而得到一个可以在 JFS 文件系统中查看的文件：

```bash
# mount -t jfs /dev/hda1 /jfs
# cd /jfs
# cp /etc/fstab .
```

若要查看文件的 inode，需要知道其 inode 号。使用带有 -i 选项的 ls 命令来确定文件的 inode 号。

```bash
# ls -i

2 . . 4 fstab
```

在此示例中，该子目录中唯一的文件名为 fstab，其 inode 号为 4。

```bash
# cd ..
# umount /jfs
# jfs_debugfs /dev/hda1
```

jfs_debugfs 中的 :i 选项用于显示 fstab 文件的 inode 信息。

```text
>i 4
Inode 4 at block 155, offset 0x800:
[1] di_istamp: 0x3f002d2d [19] di_mtime.tv_nsec:
0x00000000
[2] di_fileset: 16 [20] di_otime.tv_sec:
0x3f002f06
[3] di_number: 4 [21] di_otime.tv_nsec:
0x00000000
[4] di_gen: 1 [22] di_acl.flag:
0x00
[5] di_ipxd.len: 4 [23] di_acl.rsrvd:
Not Displayed
[6] di_ipxd.addr1: 0x00 [24] di_acl.size:
0x00000000
[7] di_ipxd.addr2: 0x0000009b [25] di_acl.len: 0
di_ipxd.address: 155 [26] di_acl.addr1:
0x00
[8] di_size:0x000000000003b4 [27] di_acl.addr2:
0x00000000
[9] di_nblocks: 0x0000000000000001 di_acl.address: 0
[10] di_nlink: 1 [28] di_ea.flag:
0x00
[11] di_uid: 0 [29] di_ea.rsrvd:
Not Displayed
[12] di_gid: 0 [30] di_ea.size:
0x00000000
[13] di_mode: 0x000681a4 [31] di_ea.len: 0
0100644 -rw- [32] di_ea.addr1:
0x00
[14] di_atime.tv_sec: 0x3f002f06 [33] di_ea.addr2:
0x00000000
[15] di_atime.tv_nsec: 0x00000000 di_ea.address: 0
[16] di_ctime.tv_sec: 0x3f002f06 [34] di_next_index: 0
[17] di_ctime.tv_nsec: 0x00000000 [35] di_acltype:
0x00000000
[18] di_mtime.tv_sec: 0x3f002f06
change_inode: [m]odify or e[x]it > x
```

## ReiserFS 文件布局

本节首先介绍 ReiserFS 文件系统的布局。查看 ReiserFS 文件系统结构的实用程序是 debugreiserfs。它接受设备作为其中一个参数；可以使用额外的参数来显示文件系统结构。以下示例格式化文件系统，并将一个名为 fstab 的文件复制到 ReiserFS 文件系统中。debugreiserfs 的 d 选项打印文件系统内部树的格式化节点。

```bash
# mkreiserfs /dev/hdb1
```

以下示例使用 /reiserfs 作为挂载点，挂载文件系统，并复制 fstab 文件，从而得到一个可以在 ReiserFS 文件系统中查看的文件。

```bash
# mount -t reiserfs /dev/hdb1 /reiserfs
# cd /reiserfs
# cp /etc/fstab .
# ls -l
total 6
drwxr-xr-x     4 root     root     104 Dec 19 06:26 .
drwxr-xr-x     30 root     root     1824 Dec 20 12:10 ..
-rw-r-- --      1 root     root     948 Dec 19 06:26 fstab

# cd ..
# umount /reiserfs
# debugreiserfs d /dev/hdb1
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

```text
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

首先显示文件系统的超级块信息，然后显示叶节点 8211。文件 fstab 的高亮信息显示了一些常见的 inode 信息。权限为 rw-r--，大小为 948，修改时间为 12/19/2003 06:26:51。

debugreiserfs 的手册页包含了关于如何显示 ReiserFS 关键结构的信息。要显示 debugreiserfs 的手册页，请键入以下命令：

```bash
# man debugreiserfs
```

