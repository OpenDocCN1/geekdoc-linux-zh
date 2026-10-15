
```
brw-r----- 1 root disk 3, 64 Apr 27 1995 hdb
brw-r----- 1 root disk 3, 65 Apr 27 1995 hdb1
brw-r----- 1 root disk 3, 74 Apr 27 1995 hdb10
brw-r----- 1 root disk 3, 75 Apr 27 1995 hdb11
brw-r----- 1 root disk 3, 76 Apr 27 1995 hdb12
brw-r----- 1 root disk 3, 77 Apr 27 1995 hdb13
brw-r----- 1 root disk 3, 78 Apr 27 1995 hdb14
brw-r----- 1 root disk 3, 79 Apr 27 1995 hdb15
brw-r----- 1 root disk 3, 80 Apr 27 1995 hdb16
brw-r----- 1 root disk 3, 66 Apr 27 1995 hdb2
brw-r----- 1 root disk 3, 67 Apr 27 1995 hdb3
brw-r----- 1 root disk 3, 68 Apr 27 1995 hdb4
brw-r----- 1 root disk 3, 69 Apr 27 1995 hdb5
brw-r----- 1 root disk 3, 70 Apr 27 1995 hdb6
brw-r----- 1 root disk 3, 71 Apr 27 1995 hdb7
brw-r----- 1 root disk 3, 72 Apr 27 1995 hdb8
brw-r----- 1 root disk 3, 73 Apr 27 1995 hdb9
```

![](img/8ad518fddafc7f5e73715a2604b61d50_117_0.png)

尽管 BIOS 不会尝试从主控制器主盘以外的任何驱动器启动，但如果必要，你可以重新配置 BIOS 以从其他硬盘启动。

## 次控制器上的主硬盘

以下列表说明次控制器上的主硬盘。CD-ROM 驱动器通常挂载在此位置（在这种情况下，前面列出的分区是不必要的）。如果你将另一块硬盘连接到 `/dev/hdc`（而不是 CD-ROM 或其他可移动介质驱动器），你可以按前面所示对驱动器进行分区。

```
brw-r----- 1 root disk 22, 0 May 8 1995 hdc
brw-r----- 1 root disk 22, 1 May 8 1995 hcd1
brw-r----- 1 root disk 22, 10 May 8 1995 hdc10
brw-r----- 1 root disk 22, 11 May 8 1995 hdc11
brw-r----- 1 root disk 22, 12 May 8 1995 hdc12
brw-r----- 1 root disk 22, 13 May 8 1995 hdc13
brw-r----- 1 root disk 22, 14 May 8 1995 hdc14
brw-r----- 1 root disk 22, 15 May 8 1995 hdc15
brw-r----- 1 root disk 22, 16 May 8 1995 hdc16
brw-r----- 1 root disk 22, 2 May 8 1995 hdc2
brw-r----- 1 root disk 22, 3 May 8 1995 hdc3
brw-r----- 1 root disk 22, 4 May 8 1995 hdc4
brw-r----- 1 root disk 22, 5 May 8 1995 hdc5
brw-r----- 1 root disk 22, 6 May 8 1995 hdc6
brw-r----- 1 root disk 22, 7 May 8 1995 hdc7
brw-r----- 1 root disk 22, 8 May 8 1995 hdc8
brw-r----- 1 root disk 22, 9 May 8 1995 hdc9
```

## 次控制器上的从硬盘

以下列表显示了次控制器上的从硬盘；有时 CD-ROM 驱动器也可以挂载在此处。不过，通常该指定标识使用其他可移动介质的驱动器——包括 CD-R 和 CD-RW（如果系统使用 IDE 设备）。

```
brw-r----- 1 root disk 22, 64 May 8 1995 hdd
brw-r----- 1 root disk 22, 65 May 8 1995 hdd1
brw-r----- 1 root disk 22, 74 May 8 1995 hdd10
brw-r----- 1 root disk 22, 75 May 8 1995 hdd11
brw-r----- 1 root disk 22, 76 May 8 1995 hdd12
brw-r----- 1 root disk 22, 77 May 8 1995 hdd13
brw-r----- 1 root disk 22, 78 May 8 1995 hdd14
brw-r----- 1 root disk 22, 79 May 8 1995 hdd15
brw-r----- 1 root disk 22, 80 May 8 1995 hdd16
brw-r----- 1 root disk 22, 66 May 8 1995 hdd2
brw-r----- 1 root disk 22, 67 May 8 1995 hdd3
brw-r----- 1 root disk 22, 68 May 8 1995 hdd4
brw-r----- 1 root disk 22, 69 May 8 1995 hdd5
brw-r----- 1 root disk 22, 70 May 8 1995 hdd6
brw-r----- 1 root disk 22, 71 May 8 1995 hdd7
brw-r----- 1 root disk 22, 72 May 8 1995 hdd8
brw-r----- 1 root disk 22, 73 May 8 1995 hdd9
```

# IDE 硬盘

你还可以添加其他四块 IDE 硬盘。它们对应 `hde` 到 `hdh`，每一块都可以拥有 1 到 16 号分区。

```
brw-r-----    1 root       disk        33,     0 Aug 18 1995 hde
brw-r-----    1 root       disk        33,    64 Aug 18 1995 hdf
brw-r-----    1 root       disk        34,     0 Aug 18 1995 hdg
brw-r-----    1 root       disk        34,    64 Aug 18 1995 hdh
```

# 网络设备文件

以下列表展示了 TCP/IP 网络设备的设备文件，以及核心 UNIX 网络（`/dev/inet` 和 `/dev/unix`）的设备文件。ICMP（即 `/dev/icmp`）是 TCP/IP 使用的消息网络（`ping` 命令使用 ICMP）。IP 设备（`/dev/ip`）是 TCP/IP 使用的寻址方式。传输层可以是 UDP 或 TCP（分别对应 `/dev/udp` 和 `/dev/tcp`）。

```
crw-------    1 root       root        18,     2 Feb 18 1994 icmp
drwxr-xr-x    2 root       root      1024 May  4 14:26 inet
crw-------    1 root       root        18,     1 Feb 18 1994 ip
crw-------    1 root       root        18,     3 Feb 18 1994 tcp
crw-------    1 root       root        18,     4 Feb 18 1994 udp
crw-------    1 root       root        17,     0 Feb 18 1994 unix
```

![](img/8ad518fddafc7f5e73715a2604b61d50_119_0.png)

有关网络的更多信息，请参阅第 11 章。

# INIT

此设备文件控制 `init`，即根进程。

```
brw-r-----    1 root       disk      1,   250 May 14 1996 initrd
```

![](img/8ad518fddafc7f5e73715a2604b61d50_119_1.png)

第 7 章解释了 `init` 进程。

# 内存访问
