

# v.4.33
Linux 作为数字取证平台的全面入门指南

完成。
Scalpel 已完成，刻出的文件 = 7，耗时 = 2 秒。

```
barry@forensic:-carve$ ls scalp_out/
0000002.jpg 0000004.jpg 0000006.jpg
0000001.jpg 0000003.jpg 0000005.jpg audit.txt
```

输出显示 scalpel 正在刻录那些定义未取消注释的文件类型。命令完成后，会生成一个列出文件的目录（带有刻出文件类型的扩展名）以及一个 audit.txt 文件。audit.txt 文件提供了包含 scalpel.conf 内容和输出结果的日志：

```
barry@forensic1:-carve less scalp_out/audit.txt
Scalpel version 2.0 audit file
Started at Fri Jun 2 15:29:39 2017
Command line:
scalpel -o scalp_out -0 -e home.blkls
```

输出目录: scalp_out
配置文件: /home/barry/carve/scalpel.conf

```
------ BEGIN COPY OF CONFIG FILE USED
# Scalpel 配置文件

# 此配置文件控制 Scalpel 刻录的文件类型和大小。注意，此文件的格式
# 在 Scalpel 1.9--!- 版本中已进行了扩展。
...
------ END COPY OF CONFIG FILE USED
```

打开目标文件 "/home/barry/carve/home.blkls"

以下是刻出的文件：

| 文件 | 起始位置 | 切分 | 长度 | 提取自 |
| :--- | :--- | :--- | :--- | :--- |
| 0000006.jpg | 6586930 | NO | 6513 | home.blkls |
| 0000005.jpg | 6586368 | NO | 6461 | home.blkls |
| 0000004.jpg | 6278144 | NO | 15373 | home.blkls |
| 0000003.jpg | 6249472 | NO | 27990 | home.blkls |
| 0000002.jpg | 6129070 | NO | 5145 | home.blkls |
| 0000001.jpg | 6128640 | NO | 94426 | home.blkls |
| 0000000.gif | 6223872 | NO | 25279 | home.blkls |

完成于 Fri Jun 2 15:29:41 2017

# v.4.33 Linux 作为数字取证平台的全面入门指南

整个 scalpel.conf 文件都包含在 audit.txt 中。输出的底部是我们刻出的文件列表，包含了发现文件头的偏移量、文件长度以及来源（被刻录的内容）。标记为 Chop 的列指的是在找到文件尾部之前刻录的最大字节数。你可以阅读 scalpel.conf 文件以获取更详细的描述。

可以使用命令行中的 display 命令查看文件，也可以使用可以提供缩略图和窗口视图的 GUI 查看器。`geeqie` 程序就是一个简单的例子。

```
barry@forensic1:~/carve$ cd scalp_out/
barry@forensic1:~/carve/scalp_out$ geeqie
```

![](img/993644c785d68ca888a5ade02ca8088d_271_0.png)

图 6：使用 geeqie 查看刻出的文件

在这些未分配数据中还可以找到其他文件。为了说明这一点，让我们再次查看 scalpel.conf 文件，并为位图文件添加不同的头部定义。打开

# v.4.33 Linux 作为数字取证平台的全面入门指南

使用文本编辑器 (vi) 打开 scalpel.conf，并在当前的 # GRAPHICS 部分下添加以下行：

# BMP 文件
- BMP (Windows 使用，只有当你认为它们值得挖掘时)
- 这经常会产生很多误报

我们将大小更改为 300000 字节，并将第一个字符串替换为 04。保存文件。重新运行 scalpel（写入不同的输出目录 scalp_out），并检查输出：

```
barry@forensic1:-carve$ scalpel -o scalp_out -e home.blkls
Scalpel version 2.0
Written by Richard Lodiale.
多核 CPU 已启用。
初始化结构。
创建线程...
线程完成。
打开目标 "/home/barry/carve/home.blkls"

```
文件处理通过 1/2。
home.blkls: 100.0% |****************************91.3 MB
00:00 分配工作队列...
工作队列分配。
工作队列构建。工作负载：
with header "\x04\x47" and footer "\x0f\xc7" --> 0 files
with header "\x04\x47" and footer "\x00\xcb" --> 0 files
with header "\x04\x49" and footer "\x0f\x00" --> 0 files
with header "\x04\x49" and footer "\x00\x00" --> 1 files
with header "\xffxd8\xffxe0" and footer "\xffxe1" --> 0 files
with header "\xffxd8\xff1" and footer "\xffxd9" --> 0 files
with header "\x89\x50" and footer "\xae\xfd\fe" --> 0 files
with header "\x42\x4d" and footer " " --> 0 files
with header "\x04\x00" and footer " " --> 1 files
with header "\x49\x49" and footer " " --> 0 files
with header "\x4d\x00" and footer " " --> 0 files
文件处理通过 2/2。
home.blkls: 100.0% |********************91.3 MB
00:00 文件处理完成。正在清理...
完成。
Scalpel 已完成，刻出的文件 = 8，耗时 = 2 秒。
```

查看上面的高亮输出，我们可以看到这次共刻出了八个文件。我们添加的位图定义清楚地表明 scalpel.conf 文件可以改进。这也不难。只需使用 xxd 在文件组中寻找匹配模式就足够你构建一个良好的头部库了。特别是当你遇到专用格式时。

鉴于刻录可以使用多种算法，将你的数据通过多个工具运行可能是个好主意。因此，我们还将查看 **photorec**。

# photore

作为 testdisk 包的一部分，**photorec** 是另一个刻录程序。然而，它采取了完全不同的方法。**photorec** 最初并不是设计取证工具，而是作为针对 SD 卡和其他介质丢失文件的人的数据恢复工具。它已变成一个从介质提取许多不同文件的有用工具。作为 testdisk 包的一部分，它与 **testdisk** 工具本身（用于恢复分区）、**identify**（与 file 命令的基本思想相同，但更简洁）一起安装，而 **qphotorec** 是 **photorec** 的 GUI 前端。

![](img/993644c785d68ca888a5ade02ca8088d_274_0.png)

PhotoRec 是免费软件，不提供任何保证。
请选择要恢复的介质

| 标记 | 类型 | 文件系统 | 大小 |
| :--- | :--- | :--- | :--- |
| D | 未知 | | 32 GB / 30 GB [整个硬盘] |
| P | 未知 | | 104 MB / 100 MB [Linux filesystem] |
| P | | Linux Swap | 4294 MB / 4096 MB [Linux swap] |
| P | 未知 | | 27 GB / 25 GB [Linux filesystem] |

# 文件系统

- Free: 从未分配空间扫描文件
- whole: 从整个分区提取文件
- FAT/NTFS/HFS+/ReiserFS

请选择一个目标来保存恢复的文件。

我们当然会在这里坚持使用命令行版本（实际上是菜单驱动的）。我们可以通过在同一个 home.bl1 磁盘镜像上运行刻录，比较从 scalpel 获取的输出与 photorec 的输出。首先，以 root 身份登录 (su -) 并使用 sbinstall 安装 testdisk 包：

```
barry@forensic1:~/carve su -
Password:
```

```
root@forensic1:~# sbinstall testdisk
TestDisk 是一款强大的免费数据恢复软件。它主要设计用于帮助恢复丢失的分区，或当这些症状是由故障软件、某些类型的病毒或人为错误（例如意外删除分区表）引起时使无法启动的磁盘能够启动。使用 TestDisk 恢复分区非常简单。
```

PhotoRec 是一种文件数据软件，旨在从硬盘和 CDROM 中恢复丢失的视频、文档和存档，以及从数字相机存储卡中恢复丢失的照片。

