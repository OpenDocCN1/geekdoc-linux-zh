
00: DASD 0103 3390 MM953 R/W 3338 CYL ON OSD A227 BLK ON SUBCHANNEL = 0005

00: DASD 0104 3390 MM954 R/W 3338 CYL ON OSD A222 BLK ON SUBCHANNEL = 0006

```
```

=> `q 300-301`

00: DASD 0300 9336 (VDSK) R/W 52488 BLK ON OSD SUBCHANNEL = 0013

00: DASD 0301 9336 (VDSK) R/W 104856 BLK ON OSD SUBCHANNEL = 0014

```
```
- 4. 使用 `QUERY` 命令验证你在地址 600-602 有一个虚拟 OSA：

```
=> q osa
00: OSA 0600 NIC 0600 UNIT 000, SUBCHANNEL = 0007
00: 0602 DEVTY CHIPDE OSD
00: 0600 QIOID-ELIGIBLE QIOASSIST-ELIGIBLE
00: 0601 NIC 001 SUBCHANNEL = 0008
00: 0601 DEVTY CHIPDE OSD
00: 0601 QIOID-ELIGIBLE QIOASSIST-ELIGIBLE
00: 0602 NIC 002 SUBCHANNEL = 0009
00: 0602 DEVTY CHIPDE OSD
00: 0602 QIOID-ELIGIBLE QIOASSIST-ELIGIBLE
```
- 5. 使用 `STORAGE` 命令显示你有一个 256 MB 的机器：

```
=> q v stor
00: STORAGE = 256M
```
- 6. 这内存足够运行 RHEL 5。但是对于安装 Linux 往往太小。使用 `DEFINE` 命令临时将存储修改为 512 MB。然后对 IPL 的问题回答 n：

```
=> def stor 512M
00: STORAGE = 512M
00: Storage = cleared - system reset.
=> ipl cms
z/VM V5.3 2007-11-18 09:53
```

```
DMACSPT23I A (191) R/0
DMACSPT23I C (592) R/0
DIAG swap disk defined at virtual address 300 (64989 4K pages of space)
DIAG swap disk defined at virtual address 301 (129981 4K pages of space)
do you want to IPL Linux from minidisk 100 y/n
```
- 7. 验证你有一个 512 MB 的虚拟机：

```
=> q v stor
00: STORAGE = 512M
```

此更改对该用户 ID 有效。当你注销并重新登录此用户 ID 时，存储将恢复为 256 MB。

现在你准备好 Linux 安装了。

## 7.1.5 RHEL 5.2 安装阶段 1

在本节中，你把 Linux 安装到控制器。按照以下步骤开始 RHEL 5.2 的安装：

- 1. 运行 `RHEL52 EXEC`。你会看到很多问题窗口在滚动。如果你使用了 RHEL 5.2 随带的默认参数文件，你将不得不回答所有网络问题。在 `LINCONF-RHEL` 中设置了正确的参数，安装过程应该进行到你需要使用浏览器 VNC 客户端进入安装：

```
=> rhel52
00: RDR FILE 0019 SENT FROM RHEL52   PUN WAS 0019 RECS 045 CPY 001 A NO HOLD
00: RDR FILE 0020 SENT FROM RHEL52   PUN WAS 0020 RECS 003 CPY 001 A NO HOLD
00: RDR FILE 0021 SENT FROM RHEL52   PUN WAS 0021 RECS 153 CPY 001 A NO HOLD
```

```
000003 FILES CHANGED
Linux version 2.6-18.el5 (breambuild@btest1.z900.redhat.com) gcc version 4.1.2.007124 (Red Hat 4.2-11) #1 SMP Tue Aug 1 19:03:24 EDT 2008
We are running under VM (64 bit mode)
Detected 2 CPU's
Boot copy address 0
Built 1 zonelist. Total pages: 131072
Kernel line: ramdisk size=4000 root=/dev/ram0 ip=off
CMBOARD=LINCONF-RH5
vncpassword=ln4
```
