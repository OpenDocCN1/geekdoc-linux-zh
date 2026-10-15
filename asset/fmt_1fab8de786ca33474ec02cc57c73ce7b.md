
# v.4.33 Linux 作为数字取证平台的全面入门指南

### Sleuth Kit 练习 #5 – NTFS 检查：ADS

```bash
barry@forensic1:~/NTFS_Path_2017$ fls -o 2048 -Frd NTFS_Path_2017.E01

/r * 40-1238: Users/AlbertE/Documents/Credit Report.pdf

/r * 40-1238: Users/AlbertE/Documents/Credit Report.pdf:Zone.Identifier

/r-* 0: Users/AlbertE/Documents/ManProj/World's First Atomic Bomb Manhattan Project Documentary - Films - YouTube.url

/r * 236-1238: Users/AlbertE/Documents/ManProj/MMhattan Project.docx

/r * 237-1238: Users/AlbertE/Documents/ManProj/The Manhattan Project YouTube.url

/r * 238-1238: Users/AlbertE/Documents/ManProj/World's First Atomic Bomb Manhattan Project Documentary - Films - YouTube.url

/r * 238-1238: Users/AlbertE/Documents/ManProj/Manhattan_project.zip

/r * 248-1238: Users/AlbertE/Documents/cyberbullying_by_proxy.doc

/r-* 0: Users/AlbertE/Pictures/Tails/Thumbs.db

/r * 221-228: Users/AlbertE/Pictures/Tails/Thumbs.db

/r * 216-228: Users/AlbertE/Pictures/Tails/BigBikeSiloCBR900SC33.jpg

/r * 218-228: Users/AlbertE/Pictures/Tails/BigBikeTailBandit.jpg

/r * 219-228: Users/AlbertE/Pictures/Tails/GemoTailK4.jpg

/r * 220-228: Users/AlbertE/Pictures/Tails/GemoTailUniversal.jpg

/r-* 0: Windows/Prefetch/EXPLORER.EXE-A806F497.pf

/r-* 0: Windows/Prefetch/MAINTENANCESERVICE.EXE-E411A328D.pf

d/ * 0: Windows/System32

/r * 167-228: Windows/Drop location 2.kml

/r * 168-228: Windows/Drop location 1.kml

/r * 169-228: Windows/Meeting_place.kml

/r * 170-228: Windows/Nums.txt

/r * 171-228: Windows/mycase.jpg
```

首先，为了看到我们讨论的内容，以防读者不熟悉备用数据流，我们应该比较普通文件列表的输出与通过取证工具获取的输出。

显然，在检查系统时，查看镜像中包含的所有文件可能是很有用的。我们可以通过两种方式来实现。第一种方法是简单地使用回环设备挂载我们的镜像并获取文件列表。我们将这样做是为了将使用标准命令行工具的方法与使用 Sleuth Kit 工具的方法进行对比。

这种同样的理念被扩展到文件的其他属性，最著名的是“备用数据流”（Alternate Data Streams，简称 ADS）。通过显示给定文件存在多个属性标识符，Sleuth Kit 为我们提供了一种检测潜在隐藏数据的方法。我们将在下一个练习中进行操作。

请记住`mount`命令作用于文件系统，而不是磁盘。此镜像中的文件系统从镜像的第 2048 扇区开始，因此我们使用偏移量（offset）来进行挂载。由于我们正在检查一个 EWF 镜像，我们需要使用`ewmount`来融合镜像文件。所有操作必须按以下方式执行：

```bash
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

在上述命令set中，我们使用 root 用户，通过`ewmount`将 EWF 镜像挂载到`/mnt/ewf`，路径为`/mnt/ewf/ewf1`。然后我们挂载数据分区（根据之前的练习，我们知道它位于 2048 处），最后退出²⁷。

> ²⁷ 注意，你可以作为普通用户使用`ewmount`，但在这种情况下，挂载需要 root 权限。

接着，我们使用`find`命令获取一个简单的文件列表：

```bash
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

`find`命令从挂载点（`/mnt/evid`）开始，查找普通文件（`-type f`）。结果给出了挂载点上所有分配文件的长列表。

为了练习目的，我们只查看 Albert 的 Pictures 目录的内容（使用相同的命令，但对`AlbertE/Pictures`使用`grep`过滤）：

```bash
barry@forensic1:~/NTFS_Pract_2017$ find /mnt/evid/ -type f | grep "AlbertE/Pictures"

/mnt/evid/Users/AlbertE/Pictures/b45ac80a95617dd7e32851c7f3_refined.jpg

/mnt/evid/Users/AlbertE/Pictures/bankor1.jpg

/mnt/evid/Users/AlbertE/Pictures/desktop.ini

/mnt/evid/Users/AlbertE/Pictures/fighterama2005-ban3.jpg

/mnt/evid/Users/AlbertE/Pictures/jet.mpg <<< 注意这一个

/mnt/evid/Users/AlbertE/Pictures/orden2.jpg
```

此输出中特别感兴趣的是`jet.mpg`。注意这个文件。我们目前的列文件方法显示了预期文件类型。这是一个 MPEG 视频。如果你愿意，可以在命令行中使用`mplayer`命令播放该视频。

```bash
barry@forensic1:~/NTFS_Pract_2017$ file /mnt/evid/Users/AlbertE/Pictures/jet.jpg

/mnt/evid/Users/AlbertE/Pictures/jet.mpg: MPEG sequence, v1, progressive Y'CbCr 4:2:0 video, CIF NTSC, NTFS 4:3, 29.97 fps, Constrained
```

```bash
barry@forensic1:~/NTFS_Pract_2017$ mplayer /mnt/evid/Users/AlbertE/Pictures/jet.mpg
```
