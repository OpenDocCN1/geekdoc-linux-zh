
# 监控磁盘使用情况

监控磁盘使用情况常用的命令是 `/usr/bin/df`，它默认显示所有挂载卷上的空闲块和文件数量。或者，管理员可以在 shell 初始化文件中（例如用于 C Shell 的 `~/.csh`）为 `df` 创建别名，如 `df -k`，它以千字节为单位显示空闲空间。SPARC 系统上 `df` 的基本输出如下：

| Filesystem | kbytes | used | avail | capacity | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/dsk/c0t0d0s | 245911 | 30754 | 190566 | 14% | / |
| /dev/dsk/c2t00s4 | 1015679 | 430877 | 523952 | 46% | /usr |
| /proc | 0 | 0 | 0 | | /proc |
| /dev | 0 | 0 | 0 | | /dev |
| /dev/dsk/c2t00s3 | 492871 | 226185 | 213709 | 51% | /var |
| /dev/md/d1 | 4119256 | 1539521 | 478483 | 89% | /opt |
| swap | 256000 | 43480 | 212520 | 17% | /tmp |
| /dev/dsk/c2t00d3 | 4193256 | 644820 | 393414 | 91% | /disks/vol1 |
| /dev/md/d2 | 3133332 | 713536 | 135536 | 75% | /disks/vol2 |
| /dev/md/d3 | 6126399 | 5099084 | 109742 | 99% | /disks/vol3 |
| /dev/dsk/c0t1d0s0 | 857409 | 586862 | 184857 | 77% | /disk/vol4 |
| /dev/dsk/c0t3d0s2 | 1820189 | 155618 | 177552 | 90% | /disk/vol5 |
| /dev/dsk/c0t2d0s0 | 4124422 | 345988 | 574334 | 87% | /disk/vol6 |
| /dev/dsk/c0t2d0s1 | 879425 | 875338 | 82510 | 95% | /disk/vol7 |
| /dev/md/d2 | 8181953 | 6803556 | 1296578 | 84% | /disk |
| /dev/junior_developers | 4124560 | 3463976 | 613944 | 85% | /disk/ |

对于 Intel 系统，硬盘有不同的名称：

| Filesystem | kbytes | used | avail | capacity | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /proc | 0 | 0 | 0 | | /dev |
| /dev/dsk/c0t0d0s0 | 73684 | 22107 | 44212 | 34% | /proc |
| /dev/dsk/c0t0d0s6 | 618904 | 401877 | 161326 | 72% | /usr |
| /dev | 0 | 0 | 0 | | /dev |
| /dev/dsk/c0t0d0s1 | 298065 | 4388 | 22527 | 17% | /var |
| /dev/dsk/c0t0d0s7 | 7111598 | 9 | 704074 | 1% | /export/home |
| swap | 222516 | 272 | 222444 | 1% | /tmp |
| /vol/dev/diskette0/unnamed_floppy | 1423 | 131 | 1292 | 10% | /floppy/unnamed_floppy |

`df` 有一个命令行选项用于自定义信息的收集和显示。例如：

```bash
# df -a
Filesystem     kbytes used avail capacity Mounted on
/dev/dsc000s0   245911 30754 190566 14%      /
/dev/dsc/c2t00s4 1015679 430877 523952 46%      /usr
/proc            0 0 0%               /proc
fd               0 0 0%               /dev
/dev/dsc/c2t00s3 492871 226185 213709 51%      /var
/dev/md/d1       4119256 1539521 478483 89%      /opt
swap             256000 43480 212520 17%      /tmp
/dev/dsc/c2t00d3 4193256 644820 393414 91%      /disks/vol1
/dev/md/d2       3133332 713536 135536 75%      /disks/vol2
/dev/md/d3       6126399 5099084 109742 99%      /disks/vol3
/dev/dsc/c0t1d0s0 857409 586862 184857 77%      /disk/vol4
/dev/dsc/c0t3d0s2 1820189 155618 177552 90%      /disk/vol5
/dev/dsc/c0t2d0s0 4124422 345988 574334 87%      /disk/vol6
/dev/dsc/c0t2d0s1 879425 875338 82510 95%      /disk/vol7
/dev/md/d2       8181953 6803556 1296578 84%      /disk
/dev/junior_developers 4124560 3463976 613944 85%      /disk/
```

# Sun Solaris 9.0 系统和网络管理员全合一考试指南

为了避免请求 NFS 挂载窗口信息时的延迟，也可以使用以下命令仅检查本地文件系统：

```
# df -l
```

| 文件系统 | kbytes | 已用 | 可用 | 容量 | 挂载点 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/disk/c0td0s0 | 245911 | 30754 | 190566 | 14% | / |
| /dev/disk/c0td0s4 | 0 | 0 | 523952 | 46% | /usr |
| /proc | 0 | 0 | 0 | 0% | /proc |
| fd | 0 | 0 | 0 | 0% | /dev/fd |
| /dev/disk/c0td0s3 | 492871 | 226184 | 217400 | 53% | /var |
| /dev/md/d1 | 4119256 | 359921 | 478493 | 89% | /opt |
| swap | 256000 | 43848 | 212512 | 17% | /tmp |
| /dev/disk/c0td0s2 | 4119256 | 368428 | 393414 | 91% | /disks/vol1 |
| /dev/md/d3 | 6126349 | 359091 | 134564 | 75% | /disks/vol2 |
| /dev/disk/c0t1d0s | 8574909 | 568862 | 1848557 | 77% | /disks/vol4 |
| /dev/c2t3d0s | 1180219 | 1551628 | 177552 | 90% | /disks/vol5 |
| /dev/disk/c0t2d0s | 4124422 | 354898 | 575434 | 87% | /disks/vol6 |
| /dev/disk/c2t3d0s | 8736478 | 828113 | 456531 | 95% | /disks/vol7 |
| /dev/md/d02 | 8181953 | 680356 | 1296578 | 84% | /disks/vol8 |

块设备可以使用命令行创建，其使用情况可以衡量——例如，控制器上的切片：

```
# df /dev/kld02
```
