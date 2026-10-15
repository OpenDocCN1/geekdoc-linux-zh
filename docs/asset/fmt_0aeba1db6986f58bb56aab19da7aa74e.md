
- 在你的 `/etc/fstab` 文件中包含有意义的注释，记录与系统逻辑标识相关的物理设备（例如，在 `/dev/c0t1s2` 条目上方添加一条注释，说明该磁盘是具有 SCSI ID 3 的外部富士通（Fujitsu）型号“foo”）。

- 在一个文件中记录以下项：
  * 物理磁盘布局，包括型号、磁盘链类型和 ID 以及电缆布局
  * 逻辑磁盘布局，包括设备和文件系统名称

- 完成后，将文档文件的内容打印在实际纸张上，并存储在中央位置（文件柜）。请记住，你不希望在最初导致你文件系统故障的那场灾难中，同时也丢失该文本文件！

### 在线参考

通用技术术语定义：http://whatis.techtarget.com

Linux 文档项目：http://www.linuxdoc.org

Solaris 文档：http://docs.sun.com

设备：

红帽 (Red Hat):
- http://www.kernel.org/pub/linux/docs/device-list/devices.html
- http://www.linuxdoc.org/HOWTO/mini/Partition/partition-2.html

Solaris:
- http://docs.sun.com/ab2/coll.47.11/TRANSITION/@Ab2PageView/idmatch (DEVADM-32137)
- http://docs.sun.com/ab2/coll.47.11/TRANSITION/@Ab2PageView/16148

文件系统：

通用：http://www.angelfire.com/myband/binusoman/Unix.html

红帽 (Red Hat):
- http://www.linuxdoc.org/LDP/gs/node6.html
- http://www.linuxdoc.org/LDP/tlk/fs/filesystem.html

逻辑卷：http://www.linuxdoc.org/HOWTO/LVM-HOWTO.html

### 分区：

红帽 (Red Hat):
- http://www.linuxdoc.org/HOWTO/mini/Partition/index.html
- http://www.redhat.com/docs/manuals/linux/RHL-7.1-Manual/ref-guide-ch-partitions.html

Solaris：http://docs.sun.com/ab2/coll.752.2/SPARCINSTALL/@Ab2PageView/931

RAID：http://www.raid-advisory.com/rabguide.html

### 交换 (Swap)：

通用：http://www.raid-advisory.com/Boot/swap.html

红帽 (Red Hat)：http://www.redhat.com/support/docs/gotchas/7.1/gotchas-71.html

## 脚注

+ 1 文件系统将在稍后的章节中讨论。
+ 2 除非你提前设置了特殊的转储专用设备。
+ 3 另一个仅仅是由于 Unix 中发生的一切都是一个进程。
+ 4 平铺文件只是 ASCII 字符。
+ 5 这个词有时写成两个单词——“file system”——有时写成一个词，我们必须在这里决定如何处理。
+ 6 意味着你会预期硬盘拥有文件系统，但流式磁带介质不是。
+ 7 因此得名为“filesystem”。
+ 8 或者，如果你愿意的话，是服务器和非服务器
+ 9 见 http://www.redhat.com/support/manuals/RHL-7.1-Manual/install-guide/s1-guimode-partitioning.html#RECOMMENDED
+ 10 见 http://docs.sun.com/ab2/coll.47.11/SYSADVI/@Ab2PageView/idmatch(DISKSCEPTS-25801)
+ 11 见 http://www.redhat.com/support/manuals/RHL-7.1-Manual/install-guide/ch-part-less.
+ 12 Curses 使用普通的 ANSI 文本来模拟图形界面，包括菜单、选择按钮等。
+ 13 见 http://www.cse.nau.edu/~rood/cse178/handout
+ 14 数据块是指存储文件内容的物理磁盘位置。
+ 15 另见 http://www.pcwebopedia.com/TERM/i/inode.html

![](img/cd7b8bd6bc2bb54927442d4cbe51a330_193_0.png)

### 基础操作

第一部分

+ 16 注意 mtime 是 ctime 的子集。
+ 17 并不是出于任何特殊原因。真的。
+ 18 见 http://www.angelfire.com/myband/binusoman/Unix.html#start
+ 19 无盘工作站是极薄的客户端。
+ 20 当然，备份的目的是为了提供同样的灵活性——见第 16 章。
+ 21 欲完整定义和更多细节，请见 http://whatis.techtarget.com/def/0,289893,sid9_gc1284007_00.html
+ 22 GPL = Gnu 公许可证 = 见 http://www.gnu.org/copyleft/
+ 23 见 http://software.ibm.com/developerworks/opensource/jfs/
+ 24 见 http://oss.com/projects/xfs/
+ 25 并不完全正确。你可以挂载文件系统，但这并不十分可靠或明智。
+ 26 Ellen Frisch, *Essential System Administration*（“章鱼书”），第 2 版，第 47 页。
+ 27 RAID 代表“独立磁盘冗余阵列”（Redundant Array of Independent Disks）或“廉价磁盘冗余阵列”，取决于问谁。
+ 28 关于各级别的良好且简单的讨论可以找到 http://whatis.techtarget.com/definition/0,289893,sid9_gc1284007_00.html。
+ 29 另见 http://www.linuxdoc.org/LDP/fs/filesystem.html
+ 30 另见 http://docs.sun.com/ab2/coll.47.11/TRANSITION/@Ab2PageView/
+ 31 以及可移动介质——见后文。
+ 32 与 Solaris 下的 `mkfs` 不同，后者被称为裸设备（raw devices）。
+ 33 另见 http://www.linuxdoc.org/LDP/gs/node6.html
+ 34 另见 http://www.me.com/notes/linux_swap.html
+ 35 交换文件有时被视为两个词——“file system”——有时是一个词，我们必须在这里决定如何处理。
+ 36 意味着你会预期硬盘拥有文件系统，但流式磁带介质不是。
+ 37 因此得名为“filesystem”。
+ 38 或者，如果你愿意的话，是服务器和非服务器
+ 39 见 http://www.redhat.com/support/manuals/RHL-7.1-Manual/install-guide/s1-guimode-partitioning.html#RECOMMENDED
+ 40 见 http://docs.sun.com/ab2/coll.47.11/SYSADVI/@Ab2PageView/idmatch(DISKSCEPTS-25801)
+ 41 见 http://www.redhat.com/support/manuals/RHL-7.1-Manual/install-guide/ch-part-less.
+ 42 Curses 使用普通的 ANSI 文本来模拟图形界面，包括菜单、选择按钮等。
+ 43 见 http://www.cse.nau.edu/~rood/cse178/handout
+ 44 数据块是指存储文件内容的物理磁盘位置。
+ 45 另见 http://www.pcwebopedia.com/TERM/i/inode.html
+ 16 注意 mtime 是 ctime 的子集。
+ 17 并不是出于任何特殊原因。真的。
+ 18 见 http://www.angelfire.com/myband/binusoman/Unix.html#start
+ 19 无盘工作站是极薄的客户端（thin clients）。
+ 20 当然，备份的目的是为了提供同样的灵活性——见第 16 章。
