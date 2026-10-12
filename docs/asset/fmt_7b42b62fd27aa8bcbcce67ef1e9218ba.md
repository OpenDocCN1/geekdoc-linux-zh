
`cua` 设备是调制解调器端口——总共 31 个，包括串行调制解调器和内置调制解调器的端口。其中 `cua0` 到 `cua3` 最常用。

```
lrwxrwxrwx 1 root    root        4 Jun 16 20:24 modem -> cua1
crw-rw---- 1 root     uucp        5,  64 Jul 17  1994 cua0
crw-rw---- 1 root     uucp        5,  65 Jul 17  1994 cua1
crw-rw---- 1 root     uucp        5,  66 Jul 17  1994 cua2
```

## 软盘驱动器

`fd` 设备是软盘驱动器。软盘驱动器对应编号 `fd0` 到 `fd3`，如下列表所示（请注意，`Compaq` 有其自身的软盘驱动器类型）。

```
lrwxrwxrwx 1 root root 13 May 4 14:25 fd -> /proc/self/fd
brw-rw---- 1 root floppy 2, 0 May 14 1996 fd0
brw-rw---- 1 root floppy 2, 36 May 14 1996 fd0Comp aQ
brw-rw---- 1 root floppy 2, 4 May 14 1996 fd0h360
brw-rw---- 1 root floppy 2, 8 May 14 1996 fd0h1200
brw-rw---- 1 root floppy 2, 40 May 14 1996 fd0h1440
brw-rw---- 1 root floppy 2, 56 May 14 1996 fd0h1476
brw-rw---- 1 root floppy 2, 72 May 14 1996 fd0h1494
brw-rw---- 1 root floppy 2, 92 May 14 1996 fd0h1600
brw-rw---- 1 root floppy 2, 20 May 14 1996 fd0h360
brw-rw---- 1 root floppy 2, 48 May 14 1996 fd0h410
brw-rw---- 1 root floppy 2, 64 May 14 1996 fd0h420
brw-rw---- 1 root floppy 2, 24 May 14 1996 fd0h720
brw-rw---- 1 root floppy 2, 80 May 14 1996 fd0h880
brw-rw---- 1 root floppy 2, 84 May 14 1996 fd0h1040
brw-rw---- 1 root floppy 2, 88 May 14 1996 fd0ul120
brw-rw---- 1 root floppy 2, 28 May 14 1996 fd0u1440
brw-rw---- 1 root floppy 2, 124 May 14 1996 fd0u1600
brw-rw---- 1 root floppy 2, 44 May 14 1996 fd0u1680
brw-rw---- 1 root floppy 2, 60 May 14 1996 fd0u1722
brw-rw---- 1 root floppy 2, 76 May 14 1996 fd0u1743
brw-rw---- 1 root floppy 2, 96 May 14 1996 fd0u1760
brw-rw---- 1 root floppy 2, 116 May 14 1996 fd0u1840
brw-rw---- 1 root floppy 2, 100 May 14 1996 fd0u1920
brw-rw---- 1 root floppy 2, 32 May 14 1996 fd0u2880
brw-rw---- 1 root floppy 2, 104 May 14 1996 fd0u3200
brw-rw---- 1 root floppy 2, 108 May 14 1996 fd0u3520
brw-rw---- 1 root floppy 2, 12 May 14 1996 fd0u360
brw-rw---- 1 root floppy 2, 112 May 14 1996 fd0u3840
brw-rw---- 1 root floppy 2, 16 May 14 1996 fd0u720
brw-rw---- 1 root floppy 2, 120 May 14 1996 fd0u800
brw-rw---- 1 root floppy 2, 52 May 14 1996 fd0u820
brw-rw---- 1 root floppy 2, 68 May 14 1996 fd0u830
brw-rw---- 1 root floppy 2, 1 May 14 1996 fd1
brw-rw---- 1 root floppy 2, 37 May 14 1996 fd1CompaQ
```

## 磁带驱动器

`rft` 和 `nrft` 设备文件是磁带驱动器。你可以指定其中四个（设备编号 `0` 到 `3`）位于以下任一位置，如下所示：

```
lrwxrwxrwx 1 root root 4 May 4 14:25 ftape -> rft0
crw-r----- 1 root disk 27, 0 Jul 17 1994 rft0
crw-r----- 1 root disk 27, 1 Jul 17 1994 rft1
crw-r----- 1 root disk 27, 2 Jul 17 1994 rft2
crw-r----- 1 root disk 27, 3 Jul 17 1994 rft3
lrwxrwxrwx 1 root root 5 May 4 14:25 nftape -> nrft0
crw-r----- 1 root disk 27, 4 Jul 17 1994 nrft0
crw-r----- 1 root disk 27, 5 Jul 17 1994 nrft1
crw-r----- 1 root disk 27, 6 Jul 17 1994 nrft2
crw-r----- 1 root disk 27, 7 Jul 17 1994 nrft3
crw-r----- 1 root disk 12, 136 Jul 18 1994 tape-d
crw-r----- 1 root disk 12, 255 Jul 18 1994 tape-reset
```

## 主控制器上的主硬盘

以下列表显示了主控制器上的主硬盘。其指定为`/dev/hda`（包含分区`/dev/hda1`到`/dev/hda16`），通常对应于你`PC`上可引导的硬盘。无论`SCSI`还是`IDE`，你都可以扩展任何驱动器的分区，直至总共 `16` 个分区。

```
brw-r----- 1 root disk 3, 0 Apr 27 1995 hda
brw-r----- 1 root disk 3, 1 Apr 27 1995 hda1
brw-r----- 1 root disk 3, 10 Apr 27 1995 hda10
brw-r----- 1 root disk 3, 11 Apr 27 1995 hda11
brw-r----- 1 root disk 3, 12 Apr 27 1995 hda12
brw-r----- 1 root disk 3, 13 Apr 27 1995 hda13
brw-r----- 1 root disk 3, 14 Apr 27 1995 hda14
brw-r----- 1 root disk 3, 15 Apr 27 1995 hda15
brw-r----- 1 root disk 3, 16 Apr 27 1995 hda16
brw-r----- 1 root disk 3, 2 Apr 27 1995 hda2
brw-r----- 1 root disk 3, 3 Apr 27 1995 hda3
brw-r----- 1 root disk 3, 4 Apr 27 1995 hda4
brw-r----- 1 root disk 3, 5 Apr 27 1995 hda5
brw-r----- 1 root disk 3, 6 Apr 27 1995 hda6
brw-r----- 1 root disk 3, 7 Apr 27 1995 hda7
brw-r----- 1 root disk 3, 8 Apr 27 1995 hda8
brw-r----- 1 root disk 3, 9 Apr 27 1995 hda9
```

## 主控制器上的从硬盘

如果向你的计算机添加第二块硬盘，通常它会被挂载为主控制器上的从盘，如下列表所示：
