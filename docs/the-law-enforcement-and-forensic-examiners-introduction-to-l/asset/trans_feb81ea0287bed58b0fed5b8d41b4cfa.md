

## Linux 作为数字取证平台的全面入门指南

索引记录大小：4096 字节
范围：0 - 293
根目录：5

内容信息

扇区大小：512
簇大小：4096

查看我们 NTFS 文件系统上的 `fsstat` 输出，我们可以发现它与我们在 Linux EXT 文件系统上运行后看到的输出有很大不同。该工具的设计初衷是根据目标文件系统提供相关信息。请注意，当在 NTFS 文件系统上运行时，`fsstat` 会向我们提供特定于 NTFS 的信息，包括关于主文件表（MFT）和特定属性值的数据。

现在我们将查看 Sleuth Kit 如何与 NTFS 文件系统上的活动文件和删除文件交互。我们第一次在镜像的根目录级别运行 `fls`：

```bash
barry@forensic1:-NTFS_Pract_2017$ fls -o 2048 NTFS_Pract_2017.E01
r/r 4-128-4: $AttrFile
r/r 8-128-2: $BadClus
r/r 8-128-1: $BadClus:$Bad
r/r 6-128-4: $Bitmap
r/r 7-128-1: $Boot
r/d 11-144-4: $Extend
r/r 2-128-1: $LogFile
r/r 0-128-6: $MFT
r/r 1-128-1: $MFTMirror
r/r 9-128-8: $Secure:$SDS
r/r 9-144-11: $Secure:$SDH
r/r 9-144-14: $Secure:$SII
r/r 10-128-1: $UpCase
r/r 10-128-4: $UpCase:$Info
r/r 3-128-3: $Volume
r/r 38-128-1: ProxyLog1.log
d/d 35-144-1: System Volume Information
d/d 64-144-2: Users
d/d 67-144-2: Windows
d/d 293: $OrphanFiles
```

注意，`fls` 为 NTFS 显示的信息比普通的目录列表要多。包含在我们的普通文件和目录中的还有 NTFS 文件系统文件（以 $ 开头），包括 `$MFT` 和 `$MFTMIRROR`（记录编号为 0 和 1）。如果你查看 MFT 编号，你会发现由于某种原因，编号为 5 的记录缺失了。MFT 记录是根目录，这正是我们在这里显示的内容。正如 `fls` 对 EXT 文件系统的默认显示是 inode 2 一样，NTFS MFT 记录 5 也是默认值。

你可以通过为 `fls` 提供一个目录来深入研究文件系统，它将显示该目录的内容。为了说明说明，重新运行命令（使用向上方向键并编辑上一条命令）并指定 MFT 记录 64（Users 目录）：

你可以深入到你感兴趣的每个目录。这是使用 `fls` “浏览”文件系统的一种方法。

我们还可以在命令行中使用选项 `-d`（仅文件条目）和 `-r`（递归）指定 `fls` 只向我们显示“已删除”的内容：

```bash
barry@forensic1:~/NTFS_Path_2017$ fls -o 2048 NTFS_Path_2017.E01 64
/d 65-144-2:
    AlbertE
/d 66-144-2:
    ElsaE
```

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

# Sleuth Kit 练习 #5 – NTFS 检查：ADS

这种同样的理念被扩展到文件的其他属性，最著名的是“备用数据流”（Alternate Data Streams，简称 ADS）。通过显示给定文件存在多个属性标识符，Sleuth Kit 为我们提供了一种检测潜在隐藏数据的方法。我们将在下一个练习中进行操作。

