

# v.4.33 Linux 作为数字取证平台的全面入门指南

请记住 `mount` 命令作用于文件系统，而不是磁盘。此镜像中的文件系统从镜像的第 2048 扇区开始，因此我们使用偏移量（offset）来进行挂载。由于我们正在检查一个 EWF 镜像，我们需要使用 `ewmount` 来融合镜像文件。所有操作必须按以下方式执行：

```
barry@forensic1:~/NTFS_Pract_2017$ su -
Password:
root@forensic1:~# cd ~barry/NTFS_Pract_2017
root@forensic1:/home/barry/NTFS_Pract_2017# ewmount NTFS_Pract_2017.E01 /mnt/ewf
ewmount 20140608
root@forensic1:/home/barry/NTFS_Pract_2017# mount -o ro,loop,offset=$((2048+512)) /mnt/ewf/ewf1 /mnt
root@forensic1:/home/barry/NTFS_Pract_2017# exit
logout
barry@forensic1:~/NTFS_Pract_2017$
```

在上述命令set中，我们使用 root 用户，通过 `ewmount` 将 EWF 镜像挂载到 `/mnt/ewf`，路径为 `/mnt/ewf/ewf1`。然后我们挂载数据分区（根据之前的练习，我们知道它位于 2048 处），最后退出²⁷。

接着，我们使用 `find` 命令获取一个简单的文件列表：

```
barry@forensic1:~/NTFS_Pract_2017$ find /mnt/evid/ -type f
/mnt/evid/ProxyLog.log
/mnt/evid/System Volume Information/Indexer
/mnt/evid/System Volume Information/WPSettings.dat
/mnt/evid/Users/AlberTE/Documents/better_access.txt
/mnt/evid/Users/AlberTE/Documents/books.txt
/mnt/evid/Users/AlberTE/Documents/cable.txt
/mnt/evid/Users/AlberTE/Documents/cable.txt
/mnt/evid/Users/AlberTE/Documents/hackabl.txt
```

`find` 命令从挂载点（`/mnt/evid`）开始，查找普通文件（`-type f`）。结果给出了挂载点上所有分配文件的长列表。

> ²⁷ 注意，你可以作为普通用户使用 `ewmount`，但在这种情况下，挂载需要 root 权限。

为了练习目的，我们只查看 Albert 的 Pictures 目录的内容（使用相同的命令，但对 AlbertE/Pictures 使用 **grep** 过滤）：

```
barry@forensic1:~/NTFS_Pract_2017$ find /mnt/evid/ -type f | grep "AlbertE/Pictures"
/mnt/evid/Users/AlbertE/Pictures/b45ac80a95617dd7e32851c7f3_refined.jpg
/mnt/evid/Users/AlbertE/Pictures/bankor1.jpg
/mnt/evid/Users/AlbertE/Pictures/desktop.ini
/mnt/evid/Users/AlbertE/Pictures/fighterama2005-ban3.jpg
/mnt/evid/Users/AlbertE/Pictures/jet.mpg <<< 注意这一个
/mnt/evid/Users/AlbertE/Pictures/orden2.jpg
```

此输出中特别感兴趣的是 `jet.mpg`。注意这个文件。我们目前的列文件方法显示了预期文件类型。这是一个 MPEG 视频。如果你愿意，可以在命令行中使用 **mplayer** 命令播放该视频。

```
barry@forensic1:~/NTFS_Pract_2017$ file /mnt/evid/Users/AlbertE/Pictures/jet.jpg
/mnt/evid/Users/AlbertE/Pictures/jet.mpg: MPEG sequence, v1, progressive Y'CbCr 4:2:0 video, CIF NTSC, NTFS 4:3, 29.97 fps, Constrained
```

```
barry@forensic1:~/NTFS_Pract_2017$ mplayer /mnt/evid/Users/AlbertE/Pictures/jet.mpg
<video plays>
正在播放 /mnt/evid/Users/AlbertE/Pictures/jet.mpg...
```

此时，我们完成了挂载点和融合镜像的操作。跟踪已挂载的磁盘和分区是此过程的重要部分：

```
barry@forensic1:~/NTFS_Pract_2017$ su -
Password:
root@forensic1:~# umount /mnt/evid && fusermount -u /mnt/ewf
root@forensic1:~# exit
logout
barry@forensic1:~/NTFS_Pract_2017$
```

同一同一行通过 `&&` 卸载 `/mnt/evid` 文件和 `/mnt/ewf` 融合磁盘镜像。这意味着只有当第一个卸载成功时，第二个命令 (**fount**) 才会执行。

回到我们的问题……为了查看为什么缺少 `jet.jpg`，尝试另一种获取文件的方法：`fls` 命令。我们可以使用 `-f` 选项只查看目录，使用 `-r` 进行递归。我们也会对 `jet.jpg` 进行 **grep**。你可以使用 MFT 记录号下载文件，这样更快且更高效：

```
barry@forensic1:/NTFS_Pract_2017$ fls -o 2048 NTFS_Pract_2017.E01 | grep jet.jpg
39-128: Users/AlbertE/Pictures/jet.jpg
39-128: Users/AlbertE/Pictures/jet.jpg:unix.txt
```

在 **fls** 的输出中，`jet.jpg` 有两个条（39-128/39-128）。两个目的具有相同的 MFT 记录号，但属性标识符不同。这是备用数据流（ADS）的一个示例。访问 `jet.jpg` 的标准内容（39-128）很容易，因为它是一个分配的文件。然而，可以使用 Sleuth Kit 的 **icat** 访问任何数据流（普通数据或 ADS），就像我们在练习中所做的那样。只需带有完整的 MFT 记录目调用 `icat` 以包含备用标识符。在这里我们指定每个数据流并使用 `icat` 将它们发送到 **file** 命令：

```
barry@forensic1:/NTFS_Pract_2017$ icat -o 2048 NTFS_Pract_2017.E01 39 | file -dev/stdin: MPEG sequence, v1, progressive Y'CbCr 4:2:0 video, CIF NTSC, NTFS 4:3, 29.97 fps, Constrained
```

在第一个（默认）流中，我们简单地使用。对于第二个流，我们包含备用标识符：

```
barry@forensic1:/NTFS_Pract_2017$ find /mnt/evid/ -type f
39 | file -dev/stdin: ASCII

```
barry@forensic1:~/NTFS_Pract_2017$ icat -o 2048 NTFS_Pract_2017.E01 39-128 | less
```

`find` 命令从挂载点（`/mnt/evid`）开始，查找普通文件（`-type f`）。结果给出了挂载点上所有分配文件的长列表。

> ²⁷ 注意，你可以作为普通用户使用 `ewmount`，但在这种情况下，挂载需要 root 权限。

为了练习目的，我们只查看 Albert 的 Pictures 目录的内容（使用相同的命令，但对 AlbertE/Pictures 使用 **grep** 过滤）：

```
barry@forensic1:~/NTFS_Pract_2017$ find /mnt/evid/ -type f | grep "AlbertE/Pictures"
/mnt/evid/Users/AlbertE/Pictures/b45ac80a95617dd7e32851c7f3_refined.jpg
/mnt/evid/Users/AlbertE/Pictures/bankor1.jpg
/mnt/evid/Users/AlbertE/Pictures/desktop.ini
/mnt/evid/Users/AlbertE/Pictures/fighterama2005-ban3.jpg
/mnt/evid/Users/AlbertE/Pictures/jet.mpg <<< 注意这一个
/mnt/evid/Users/AlbertE/Pictures/orden2.jpg
```

此输出中特别感兴趣的是 `jet.mpg`。注意这个文件。我们目前的列文件方法显示了预期文件类型。这是一个 MPEG 视频。如果你愿意，可以在命令行中使用 **mplayer** 命令播放该视频。

```
barry@forensic1:~/NTFS_Pract_2017$ file /mnt/evid/Users/AlbertE/Pictures/jet.jpg
/mnt/evid/Users/AlbertE/Pictures/jet.mpg: MPEG sequence, v1, progressive Y'CbCr 4:2:0 video, CIF NTSC, NTFS 4:3, 29.97 fps, Constrained
```

```
barry@forensic1:~/NTFS_Pract_2017$ mplayer /mnt/evid/Users/AlbertE/Pictures/jet.mpg
<video plays>
正在播放 /mnt/evid/Users/AlbertE/Pictures/jet.mpg...
```

此时，我们完成了挂载点和融合镜像的操作。跟踪已挂载的磁盘和分区是此过程的重要部分：

```
barry@forensic1:~/NTFS_Pract_2017$ su -
Password:
root@forensic1:~# umount /mnt/evid && fusermount -u /mnt/ewf
root@fore1:~# exit
logout
barry@forensic1:~/NTFS_Pract_2017$
```

同一同一同一行通过 `&&` 卸载 `/mnt/evid` 文件和 `/mnt/ewf` 融合磁盘镜像。这意味着只有当第一个卸载成功时，第二个命令 (**fount**) 才会执行。

回到我们的问题……为了查看为什么缺少 `jet.jpg`，尝试另一种获取文件的方法：`fls` 命令。我们可以使用 `-f` 选项只查看目录，使用 `-r` 进行递归。我们也会对 `jet.jpg` 进行 **grep**。你可以使用 MFT 记录号下载文件，这样更快且更高效：

```
barry@forensic1:/NTFS_Pract_2017$ fls -o 2048 NTFS_Pract_2017.E01 | grep jet.jpg
39-128: Users/AlbertE/Pictures/jet.jpg
39-128: Users/AlbertE/Pictures/jet.jpg:unix.txt
```

在 **fls** 的输出中，`jet.jpg` 有两个条（39-128/39-128）。两个目的具有相同的 MFT 记录号，但属性标识符不同。这是备用数据流（ADS）的一个示例。访问 `jet.jpg` 的标准内容（39-128）很容易，因为它是一个分配的文件。然而，可以使用 Sleuth Kit 的 **icat** 访问任何数据流（普通数据或 ADS），就像我们在练习中所做的那样。只需带有完整的 MFT 记录目调用 `icat` 以包含备用标识符。在这里我们指定每个数据流并使用 `icat` 将它们发送到 **file** 命令：

```
barry@forensic1:/NTFS_Pract_2017$ icat -o 2048 NTFS_Pract_2017.E01 39 | file -dev/stdin: MPEG sequence, v1, progressive Y'CbCr 4:2:0 video, CIF NTSC, NTFS 4:3, 29.97 fps, Constrained
```

在第一个（默认）流中，我们简单地使用。对于第二个流，我们包含备用标识符：

```
barry@forensic1:/NTFS_Pract_2017$ find /mnt/evid/ -type f
39 | file -dev/stdin: ASCII

```

```
barry@forensic1:/NTFS_Pract_2017$ icat -o 2048 NTFS_Pract_2017.E01 39-128 | less
```

`find` 命令从挂载点（`/mnt/evid`）开始，查找普通文件（`-type f`）。结果给出了挂载点上所有分配文件的长列表。

> ²⁷ 注意，你可以作为普通用户使用 `ewmount`，但在这种情况下，挂载需要 root 权限。

为了练习目的，我们只查看 Albert 的 Pictures 目录的内容（使用相同的命令，但对 AlbertE/Pictures 使用 **grep** 过滤）：

# Sleuth Kit 练习 #6 物理字符串搜索与分配状态 (NTFS)

我们已经对 NTFS 系统进行了几次字符串搜索。在对镜像进行字符串时，我们假设它们是分配的。



再次，我们正在处理 NTFS_Pract_2017.E01 镜像。而且再次，由于我们使用非 EWF 感知工具进行物理搜索，我们将挂载镜像并处理原始磁盘。这将在我们的当前目录下创建一个点——不需要循环设备和 root 权限。

```bash
$barry@forensic1:~/NTFS_Pract_2017$ mkdir ewmnt
```

```bash
$barry@forensic1:~/NTFS_Pract_2017$ ewmount NTFS_Pract_2017.E01 ewmnt/
ewmount 20140608
```

`grep` 命令指向挂载在 `ewmnt/` 的镜像。由于 ewmnt 在我们的当前目录下（我们刚刚创建了它），所以不需要开头的 `/`。

```bash
$barry@forensic1:~/NTFS_Pract_2017$ grep -abi cyberbullying ewmnt/ewf1
C€€($) |€#($) |€#@Ba>B #ULTIMATEJOURNEYDK.wmv##YYYYYY€€$?#<€#:##
9€€€€€€€€€€€€€€€€
```

```bash
D€€
Dq€€
```

代理网络欺凌是指网络欺凌者让别人替他们做脏工作……当我们执行搜索时，我们面对大量的非 ASCII 字符，这严重影响了输出的可读性。当你滚动输出时，你可以看到我们寻找的字符串，但偏移量被遮蔽了。在之前的基础课程中，在本文档早期，我们讨论过使用 `tr` 命令将“控制字符”转换为换行符。这将从我们的视图中移除不可读的内容，同时也从 grep 搜索中移除，而字符替换的操作对偏移量案例没有问题。在此处使用 tr：

